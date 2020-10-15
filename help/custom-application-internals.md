---
title: Förstå hur ett anpassat program fungerar.
description: Internt arbete [!DNL Asset Compute Service] med anpassade program för att förstå hur det fungerar.
translation-type: tm+mt
source-git-commit: 54afa44d8d662ee1499a385f504fca073ab6c347
workflow-type: tm+mt
source-wordcount: '774'
ht-degree: 0%

---


# Internt i ett anpassat program {#how-custom-application-works}

Använd följande bild för att förstå hela arbetsflödet när en digital resurs bearbetas med ett anpassat program av en klient.

![Anpassat arbetsflöde för program](assets/customworker.png)

*Bild: Steg som ska användas för att bearbeta en resurs med [!DNL Asset Compute Service].*

## Registrering {#registration}

Klienten måste ringa [`/register`](api.md#register) en gång före den första begäran [`/process`](api.md#process-request) för att kunna ställa in och hämta journalens URL för att ta emot Adobe I/O-händelser för beräkning av Adobe-tillgångar.

```sh
curl -X POST \
  https://asset-compute.adobe.io/register \
  -H "x-ims-org-id: $ORG_ID" \
  -H "x-gw-ims-org-id: $ORG_ID" \
  -H "Authorization: Bearer $JWT_TOKEN" \
  -H "x-api-key: $API_KEY"
```

JavaScript- [`@adobe/asset-compute-client`](https://github.com/adobe/asset-compute-client#usage) biblioteket kan användas i NodeJS-program för att hantera alla nödvändiga steg från registrering, bearbetning till asynkron händelsehantering. Mer information om obligatoriska rubriker finns i [Autentisering och auktorisering](api.md).

## Bearbetar {#processing}

Klienten skickar en [bearbetningsbegäran](api.md#process-request) .

```sh
curl -X POST \
  https://asset-compute.adobe.io/process \
  -H "x-ims-org-id: $ORG_ID" \
  -H "x-gw-ims-org-id: $ORG_ID" \
  -H "Authorization: Bearer $JWT_TOKEN" \
  -H "x-api-key: $API_KEY" \
  -d "<RENDITION_JSON>
```

Klienten ansvarar för att formatera återgivningarna korrekt med försignerade URL:er. JavaScript- [`@adobe/node-cloud-blobstore-wrapper`](https://github.com/adobe/node-cloud-blobstore-wrapper#presigned-urls) biblioteket kan användas i NodeJS-program för att försignera URL:er. För närvarande stöder biblioteket endast Azure Blob Storage och AWS S3-behållare.

Bearbetningsbegäran returnerar en `requestId` som kan användas för avsökning av Adobe I/O-händelser.

Nedan följer ett exempel på en anpassad begäran om programbearbetning.

```json
{
    "source": "https://www.adobe.com/some-source-file.jpg",
    "renditions" : [
        {
            "worker": "https://my-project-namespace.adobeioruntime.net/api/v1/web/my-namespace-version/my-worker",
            "name": "rendition1.jpg",
            "target": "https://some-presigned-put-url-for-rendition1.jpg",
        }
    ],
    "userData": {
        "my-asset-id": "1234567890"
    }
}
```

Den anpassade programåtergivningsbegäran skickas [!DNL Asset Compute Service] till det anpassade programmet. Den använder en HTTP-POST till den angivna program-URL:en, som är den skyddade webbåtgärds-URL:en från Project Fire. Alla förfrågningar använder HTTPS-protokollet för att maximera datasäkerheten.

Den SDK för [tillgångsberäkning](https://github.com/adobe/asset-compute-sdk#adobe-asset-compute-worker-sdk) som används av ett anpassat program hanterar HTTP-POSTENS begäran. Den hanterar också nedladdning av källan, överföring av återgivningar, sändning av I/O-händelser och felhantering.

<!-- TBD: Add the application diagram. -->

### Programkod {#application-code}

Anpassad kod behöver bara tillhandahålla ett återanrop som tar den lokalt tillgängliga källfilen (`source.path`). Det `rendition.path` är platsen där det slutliga resultatet av en begäran om bearbetning av tillgångar ska placeras. Det anpassade programmet använder återanropet för att omvandla de lokalt tillgängliga källfilerna till en återgivningsfil med det namn som skickades (`rendition.path`). Ett anpassat program måste skriva till `rendition.path` för att skapa en återgivning:

```javascript
const { worker } = require('@adobe/asset-compute-sdk');
const fs = require('fs').promises;

// worker() is the entry point in the SDK "framework".
// The asynchronous function defined is the rendition callback.
exports.main = worker(async (source, rendition) => {

    // Tip: custom worker parameters are available in rendition.instructions.
    console.log(rendition.instructions.name); // should print out `rendition.jpg`.

    // Simplest example: copy the source file to the rendition file destination so as to transfer the asset as is without processing.
    await fs.copyFile(source.path, rendition.path);
});
```

### Hämta källfiler {#download-source}

Ett anpassat program hanterar bara lokala filer. Hämtningen av källfilen hanteras av SDK:n för [resursberäkning](https://github.com/adobe/asset-compute-sdk#adobe-asset-compute-worker-sdk).

### Skapa återgivning {#rendition-creation}

SDK anropar en asynkron [återgivningsåtergivningsfunktion](https://github.com/adobe/asset-compute-sdk#rendition-callback-for-worker-required) för varje återgivning.

Callback-funktionen har åtkomst till [käll](https://github.com/adobe/asset-compute-sdk#source) - och [återgivningsobjekten](https://github.com/adobe/asset-compute-sdk#rendition) . Den finns `source.path` redan och är sökvägen till den lokala kopian av källfilen. Sökvägen `rendition.path` där den bearbetade återgivningen måste lagras. Om inte flaggan [](https://github.com/adobe/asset-compute-sdk#worker-options-optional) disableSourceDownload anges måste programmet använda exakt `rendition.path`. Annars kan SDK inte hitta eller identifiera återgivningsfilen och misslyckas.

Den alltför enkla framställningen av exemplet görs för att illustrera och fokusera på anatomin i ett anpassat program. Programmet kopierar bara källfilen till återgivningsmålet.

Mer information om återgivningens återanropsparametrar finns i [Resursberäknings-SDK API](https://github.com/adobe/asset-compute-sdk#api-details).

### Överför renderingar {#upload-rendition}

När varje återgivning har skapats och lagrats i en fil med sökvägen som tillhandahålls av `rendition.path`, överför [Asset Compute SDK](https://github.com/adobe/asset-compute-sdk#adobe-asset-compute-worker-sdk) varje återgivning till ett molnlagringsutrymme (antingen AWS eller Azure). Ett anpassat program hämtar flera återgivningar samtidigt om, och bara om, den inkommande begäran har flera återgivningar som pekar på samma program-URL. Överföringen till molnlagringen görs efter varje återgivning och innan återanropet för nästa återgivning körs.

Programmet `batchWorker()` har ett annat beteende eftersom det faktiskt bearbetar alla återgivningar och först när alla har bearbetats överför dessa.

## Adobe I/O-händelser {#aio-events}

SDK skickar Adobe I/O-händelser för varje återgivning. Dessa händelser är antingen av typen `rendition_created` eller `rendition_failed` beroende på resultatet. Mer information om händelser finns i [Asynkrona händelser](api.md#asynchronous-events) för beräkning av resurser.

## Ta emot Adobe I/O-händelser {#receive-aio-events}

Klienten avsöker [Adobe I/O Events Journal](https://www.adobe.io/apis/experienceplatform/events/ioeventsapi.html#/Journaling) enligt dess konsumtionslogik. Den inledande journaladressen är den som anges i API- `/register` svaret. Händelser kan identifieras med hjälp av `requestId` den som finns i händelserna och är densamma som returneras i `/process`. Varje återgivning har en separat händelse som skickas så snart återgivningen har överförts (eller misslyckats). När klienten tar emot en matchande händelse kan den visa eller på annat sätt hantera de resulterande återgivningarna.

JavaScript-biblioteket [`asset-compute-client`](https://github.com/adobe/asset-compute-client#usage) gör journalavsökningen enkel med `waitActivation()` metoden för att hämta alla händelser.

```javascript
const events = await assetCompute.waitActivation(requestId);
await Promise.all(events.map(event => {
    if (event.type === "rendition_created") {
        // get rendition from cloud storage location
    }
    else if (event.type === "rendition_failed") {
        // failed to process
    }
    else {
        // other event types
        // (could be added in the future)
    }
}));
```

Mer information om hur du hämtar journalhändelser finns i API:t för [Adobe I/O-händelser](https://www.adobe.io/apis/experienceplatform/events/ioeventsapi.html#!adobedocs/adobeio-events/master/events-api-reference.yaml).

<!-- TBD:
* Illustration of the controls/data flow.
* Basic overview, in text and not code, of how an application works.
-->
