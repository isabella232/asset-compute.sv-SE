---
title: Utveckla för [!DNL Asset Compute Service].
description: Skapa anpassade program med [!DNL Asset Compute Service].
translation-type: tm+mt
source-git-commit: 127895cf1bab59546f9ba0be2b3b7a935627effb
workflow-type: tm+mt
source-wordcount: '1496'
ht-degree: 0%

---


# Utveckla ett anpassat program {#develop}

Innan du börjar utveckla ett anpassat program:

* Kontrollera att alla [krav](/help/understand-extensibility.md#prerequisites-and-provisioning) uppfylls.
* Installera de [programverktyg](/help/setup-environment.md#create-dev-environment)som krävs.
* Se [Konfigurera miljön](setup-environment.md) för att kontrollera att du är redo att skapa ett anpassat program.

## Skapa ett anpassat program {#create-custom-application}

Kontrollera att [Adobe I/O CLI](https://github.com/adobe/aio-cli) är installerat lokalt.

1. Om du vill skapa ett anpassat program [skapar du ett Fireworks-program](https://github.com/AdobeDocs/project-firefly/blob/master/getting_started/first_app.md#4-bootstrapping-new-app-using-the-cli). Gör det genom att köra `aio app init <app-name>` i terminalen.

   Om du inte redan har loggat in uppmanas du att logga in på [Adobe Developer Console](https://console.adobe.io/) med din Adobe ID via den här funktionen. Mer information om hur du loggar in från klippet finns [här](https://github.com/AdobeDocs/project-firefly/blob/master/getting_started/first_app.md#3-signing-in-from-cli) .

   Adobe rekommenderar att du loggar in. Om du har problem följer du instruktionerna [för att skapa ett program utan att logga in](https://github.com/AdobeDocs/project-firefly/blob/master/getting_started/first_app.md#42-developer-is-not-logged-in-as-enterprise-organization-user).

1. När du har loggat in följer du instruktionerna i CLI och väljer `Organization`, `Project`och `Workspace` ska använda för programmet. Välj det projekt och den arbetsyta du skapade när du [konfigurerade miljön](setup-environment.md).

   ```sh
   $ aio app init <app-name>
   Retrieving information from Adobe I/O Console..
   ? Select Org My Adobe Org
   ? Select Project MyFireflyProject
   ? Select Workspace myworkspace
   create console.json
   ```

1. När du uppmanas till `Which Adobe I/O App features do you want to enable for this project?`det väljer du minst `Actions`:

   ```bash
   ? Which Adobe I/O App features do you want to enable for this project?
   select components to include (Press <space> to select, <a> to toggle all, <i> to invert selection)
   ❯◉ Actions: Deploy Runtime actions
   ◯ Events: Publish to Adobe I/O Events
   ◯ Web Assets: Deploy hosted static assets
   ◯ CI/CD: Include GitHub Actions based workflows for Build, Test and Deploy
   ```

1. När du uppmanas `Which type of sample actions do you want to create?`till det väljer du `Adobe Asset Compute Worker`:

   ```bash
   ? Which type of sample actions do you want to create?
   Select type of actions to generate
   ❯◉ Adobe Asset Compute Worker
   ◯ Generic
   ```

1. Följ resten av instruktionerna och öppna det nya programmet i Visual Studio Code (eller din favoritkodredigerare). Den innehåller ställningar och exempelkod för ett anpassat program.

   Läs här om [huvudkomponenterna i en Fireworks-app](https://github.com/AdobeDocs/project-firefly/blob/master/getting_started/first_app.md#5-anatomy-of-a-project-firefly-application).

   Mallapplikationen utnyttjar vår SDK för [tillgångsberäkning](https://github.com/adobe/asset-compute-sdk#asset-compute-sdk) för att ladda upp, ladda ned och organisera programåtergivningar så att utvecklarna bara behöver implementera den anpassade programlogiken. I `actions/<worker-name>` mappen finns den plats där den anpassade programkoden ska läggas till i `index.js` filen.

Se [exempel på anpassade program](#try-sample) för exempel och idéer på anpassade program.

### Lägg till autentiseringsuppgifter {#add-credentials}

När du loggar in när du skapar programmet, samlas de flesta av referenserna i din ENV-fil in. Om du använder utvecklingsverktyget måste du dock ha ytterligare autentiseringsuppgifter.

<!-- TBD: Check if manual setup of credentials is required.
Manual set up of credentials is removed from troubleshooting and best practices page. Link was broken.
If you did not log in, refer to our troubleshooting guide to [set up credentials manually](troubleshooting.md).
-->

#### Lagringsuppgifter för utvecklingsverktyget {#developer-tool-credentials}

Utvecklarverktyget som används för att testa anpassade program med det faktiska [!DNL Asset Compute service] kräver en molnlagringsbehållare för testfiler och för att ta emot och visa återgivningar som genererats av program.

>[!NOTE]
>
>Detta är skilt från molnlagringen av [!DNL Adobe Experience Manager] som en Cloud Service. Det gäller endast för utveckling och testning med utvecklingsverktyget för beräkning av tillgångar.

Kontrollera att du har tillgång till en molnlagringsbehållare [som](https://github.com/adobe/asset-compute-devtool#prerequisites)stöds. Den här behållaren kan delas av flera utvecklare i olika projekt efter behov.

#### Lägg till autentiseringsuppgifter i ENV-filen {#add-credentials-env-file}

Lägg till följande inloggningsuppgifter för utvecklingsverktyget i ENV-filen i roten för ditt Fireworks:

1. Lägg till den absoluta sökvägen till den privata nyckelfilen som skapades när du lade till tjänster i ditt Fireworks:

   ```conf
   ASSET_COMPUTE_PRIVATE_KEY_FILE_PATH=
   ```

1. Lägg till autentiseringsuppgifter för S3 eller Azure Storage. Du behöver bara tillgång till en molnlagringslösning.

   ```conf
   # S3 credentials
   S3_BUCKET=
   AWS_ACCESS_KEY_ID=
   AWS_SECRET_ACCESS_KEY=
   AWS_REGION=
   
   # Azure Storage credentials
   AZURE_STORAGE_ACCOUNT=
   AZURE_STORAGE_KEY=
   AZURE_STORAGE_CONTAINER_NAME=
   ```

## Kör programmet {#run-custom-application}

Konfigurera [autentiseringsuppgifterna](#developer-tool-credentials)korrekt innan du kör programmet med verktyget Resursberäkning.

Om du vill köra programmet i utvecklingsverktyget använder du `aio app run` kommando. Den distribuerar åtgärden till Adobe I/O Runtime och startar utvecklingsverktyget på den lokala datorn. Det här verktyget används för att testa programbegäranden under utveckling. Här är ett exempel på en renderingsförfrågan:

```json
"renditions": [
    {
        "worker": "https://1234_my_namespace.adobeioruntime.net/api/v1/web/example-custom-worker-master/worker",
        "name": "image.jpg"
    }
]
```

>[!NOTE]
>
>Använd inte `--local` flaggan med `run` kommandot. Det fungerar inte med [!DNL Asset Compute] anpassade program och verktyget Resursberäknare. Anpassade program anropas av [!DNL Asset Compute Service] som inte har åtkomst till åtgärder som körs på utvecklarens lokala datorer.

Se [här](test-custom-application.md) hur du testar och felsöker programmet. När du är klar med utvecklingen av ditt anpassade program ska du [distribuera ditt anpassade program](deploy-custom-application.md).

## Prova exempelprogrammet från Adobe {#try-sample}

Följande är exempel på anpassade program:

* [worker-basic](https://github.com/adobe/asset-compute-example-workers/tree/master/projects/worker-basic)
* [djurbilder](https://github.com/adobe/asset-compute-example-workers/tree/master/projects/worker-animal-pictures)

### Anpassat mallprogram {#template-custom-application}

Arbetarbasen [är ett](https://github.com/adobe/asset-compute-example-workers/tree/master/projects/worker-basic) mallprogram. Det genererar en återgivning genom att bara kopiera källfilen. Innehållet i det här programmet är den mall som tas emot när du väljer `Adobe Asset Compute` att skapa AIR-programmet.

Programfilen [`worker-basic.js`](https://github.com/adobe/asset-compute-example-workers/blob/master/projects/worker-basic/worker-basic.js) använder [`asset-compute-sdk`](https://github.com/adobe/asset-compute-sdk#overview) för att hämta källfilen, ordna varje renderingsbearbetning och överföra de resulterande renderingarna tillbaka till molnlagringen.

Det [`renditionCallback`](https://github.com/adobe/asset-compute-sdk#rendition-callback-for-worker-required) som definieras inuti programkoden är var all programbearbetningslogik ska utföras. Återgivningsåteranropet i kopierar `worker-basic` bara källfilens innehåll till återgivningsfilen.

```javascript
const { worker } = require('@adobe/asset-compute-sdk');
const fs = require('fs').promises;

exports.main = worker(async (source, rendition) => {
    // copy source to rendition to transfer 1:1
    await fs.copyFile(source.path, rendition.path);
});
```

## Anropa ett externt API {#call-external-api}

I programkoden kan du göra externa API-anrop som hjälp vid programbearbetning. Ett exempel på en programfil som anropar ett externt API visas nedan.

```javascript
exports.main = worker(async function (source, rendition) {

    const response = await fetch('https://adobe.com', {
        method: 'GET',
        Authorization: params.AUTH_KEY
    })
});
```

Exempelvis skickar [`worker-animal-pictures`](https://github.com/adobe/asset-compute-example-workers/blob/master/projects/worker-animal-pictures/worker-animal-pictures.js#L46) programmet en hämtningsbegäran till en statisk URL från Wikimedia med hjälp av [`node-httptransfer`](https://github.com/adobe/node-httptransfer#node-httptransfer) biblioteket.

<!-- TBD: Revisit later to see if this note is required.
>[!NOTE]
>
>For extra authorization for these API calls, see [custom authorization checks](#custom-authorization-checks).
-->

### Skicka egna parametrar {#pass-custom-parameters}

Du kan skicka egna definierade parametrar via återgivningsobjekten. De kan refereras inuti programmet i [`rendition` instruktioner](https://github.com/adobe/asset-compute-sdk#rendition). Ett exempel på ett återgivningsobjekt är:

```json
"renditions": [
    {
        "worker": "https://1234_my_namespace.adobeioruntime.net/api/v1/web/example-custom-worker-master/worker",
        "name": "image.jpg",
        "my-custom-parameter": "my-custom-parameter-value"
    }
]
```

Ett exempel på en programfil som använder en anpassad parameter är:

```javascript
exports.main = worker(async function (source, rendition) {

    const customParam = rendition.instructions['my-custom-parameter'];
    console.log('Custom paramter:', customParam);
    // should print out `Custom parameter: "my-custom-parameter-value"`
});
```

Den `example-worker-animal-pictures` skickar en anpassad parameter [`animal`](https://github.com/adobe/asset-compute-example-workers/blob/master/projects/worker-animal-pictures/worker-animal-pictures.js#L39) för att avgöra vilken fil som ska hämtas från Wikimedia.

## Stöd för autentisering och auktorisering {#authentication-authorization-support}

Som standard levereras anpassade program för tillgångsberäkning med behörighets- och autentiseringskontroller för felsökningsprogram. Detta aktiveras genom att `require-adobe-auth` anteckningen ställs in på `true` i `manifest.yml`.

### Åtkomst till andra Adobe-API:er {#access-adobe-apis}

<!-- TBD: Revisit this section. Where do we document console workspace creation?
-->

Lägg till API-tjänsterna på den [!DNL Asset Compute] konsolarbetsyta som skapades i konfigurationen. Dessa tjänster ingår i JWT-åtkomsttoken som genereras av [!DNL Asset Compute Service]. Token och andra inloggningsuppgifter är tillgängliga inuti `params` programåtgärdsobjektet.

```javascript
const accessToken = params.auth.accessToken; // JWT token for Technical Account with entitlements from the console workspace to the API service
const clientId = params.auth.clientId; // Technical Account client Id
const orgId = params.auth.orgId; // Experience Cloud Organization
```

### Skicka autentiseringsuppgifter för system från tredje part {#pass-credentials-for-tp}

Om du vill hantera autentiseringsuppgifter för andra externa tjänster skickar du dessa som standardparametrar för åtgärderna. Dessa krypteras automatiskt under överföring. Mer information finns i [Skapa åtgärder i Utvecklarhandbok](https://www.adobe.io/apis/experienceplatform/runtime/docs.html#!adobedocs/adobeio-runtime/master/guides/creating_actions.md)för körtid. Ange dem sedan med hjälp av miljövariabler under distributionen. De här parametrarna kan nås i `params` objektet inuti funktionsmakrot.

Ange standardparametrarna i `inputs` i `manifest.yml`:

```yaml
packages:
  __APP_PACKAGE__:
    actions:
      worker:
        function: 'index.js'
        runtime: 'nodejs:10'
        web: true
        inputs:
           secretKey: $SECRET_KEY
        annotations:
          require-adobe-auth: true
```

Uttrycket läser `$VAR` värdet från en miljövariabel med namnet `VAR`.

Under utvecklingen kan värdet anges i den lokala ENV-filen så att miljövariabler från ENV-filer läses automatiskt, förutom de variabler som anges från anropsgränssnittet. `aio` I det här exemplet ser ENV-filen ut så här:

```CONF
#...
SECRET_KEY=secret-value
```

För produktionsdistribution kan du ange miljövariabler i CI-systemet, till exempel med hjälp av hemligheter i GitHub-åtgärder. Slutligen får du tillgång till standardparametrarna i själva programmet:

```javascript
const key = params.secretKey;
```

## Storleksändra program {#sizing-workers}

Ett program körs i en behållare i Adobe I/O Runtime med [begränsningar](https://www.adobe.io/apis/experienceplatform/runtime/docs.html#!adobedocs/adobeio-runtime/master/guides/system_settings.md) som kan konfigureras via `manifest.yml`:

```yaml
    actions:
      myworker:
        function: /actions/myworker/index.js
        limits:
          timeout: 300000
          memorySize: 512
          concurrency: 1
```

På grund av den mer omfattande bearbetning som vanligtvis utförs av program för tillgångsberäkning är det mer sannolikt att man måste justera dessa gränser för optimala prestanda (tillräckligt stor för att hantera binära resurser) och effektivitet (inte slösa resurser på grund av oanvänt behållarminne).

Standardtidsgränsen för åtgärder i körtid är en minut, men den kan ökas genom att `timeout` gränsen anges (i millisekunder). Om du förväntar dig att bearbeta större filer ökar du den här tiden. Tänk på hur lång tid det tar att hämta källan, bearbeta filen och överföra återgivningen. Om en åtgärd gör timeout, d.v.s. inte returnerar aktiveringen före den angivna tidsgränsen, ignoreras behållaren och återanvänds inte.

Tillgångsberäkningsprogram brukar vara nätverks- och disk-I/O-bundna. Källfilen måste hämtas först, bearbetningen är ofta IO-tung och sedan överförs återgivningarna igen.

Minnet som är tillgängligt för en åtgärdsbehållare anges av `memorySize` MB. För närvarande definierar detta även hur mycket processoråtkomst behållaren får, och viktigast av allt är det en viktig del av kostnaden för att använda körningsversionen (större behållare kostar mer). Använd ett större värde här när bearbetningen kräver mer minne eller processorkapacitet, men var noga med att inte slösa bort resurser eftersom ju större behållare det är, desto lägre blir den totala genomströmningen.

Dessutom är det möjligt att styra åtgärdssamtidighet i en behållare med hjälp av `concurrency` inställningen. Detta är antalet samtidiga aktiveringar som en enskild behållare (av samma åtgärd) får. I den här modellen fungerar åtgärdsbehållaren som en Node.js-server som tar emot flera samtidiga begäranden, upp till den gränsen. Om den inte anges är standardvärdet 200, vilket är bra för mindre Firefoly-åtgärder, men vanligtvis för stort för Asset Compute-program med tanke på deras mer intensiva lokala bearbetning och diskaktivitet. Vissa program kanske inte fungerar bra med samtidig aktivitet beroende på implementering. SDK:n för beräkning av tillgångar ser till att aktiveringarna separeras genom att filer skrivs till olika unika mappar.

Testa program för att hitta de optimala siffrorna för `concurrency` och `memorySize`. Större behållare = högre minnesgräns kan möjliggöra mer samtidighet men kan också vara onödigt för lägre trafik.
