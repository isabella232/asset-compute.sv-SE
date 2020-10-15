---
title: Introduktion till [!DNL Asset Compute Service]programmet.
description: '[!DNL Asset Compute Service] är en molnbaserad resurshanteringstjänst som minskar komplexiteten och förbättrar skalbarheten.'
translation-type: tm+mt
source-git-commit: 54afa44d8d662ee1499a385f504fca073ab6c347
workflow-type: tm+mt
source-wordcount: '332'
ht-degree: 0%

---


# Översikt över [!DNL Asset Compute Service] {#overview}

[!DNL Asset Compute Service] är en skalbar och utbyggbar tjänst för [!DNL Adobe Experience Cloud] att bearbeta digitala resurser. Det kan omvandla bild, video, dokument och andra filformat till olika renderingar, bland annat miniatyrer, extraherad text och metadata samt arkiv.

Utvecklare kan plugin-program för anpassade resurser (kallas även anpassade arbetare) för att hantera anpassade användningsfall. Tjänsten fungerar på [!DNL Adobe I/O] körningsmiljön. Den kan utökas via [!DNL Project Firefly] headless-appar skrivna i Node.js. Dessa kan utföra anpassade åtgärder som att anropa externa API:er för att utföra bildåtgärder eller utnyttja [!DNL Adobe Sensei] stödet.

[!DNL Project Firefly] är ett ramverk för att bygga och driftsätta anpassade webbapplikationer på [!DNL Adobe I/O] runtime för att utöka Adobe Experience Cloud lösningar. För att skapa anpassade program kan utvecklarna använda [!DNL React Spectrum] (Adobe’s UI toolkit), skapa mikrotjänster, skapa anpassade händelser och skapa programmeringsgränssnitt. Se [dokumentationen om Project Fire](https://www.adobe.io/apis/experienceplatform/project-firefly/docs.html).

>[!NOTE]
>
>För närvarande [!DNL Asset Compute Service] kan du bara använda den via [!DNL Experience Manager] en Cloud Service. Administratörer skapar bearbetningsprofiler som kan anropa [!DNL Asset Compute Service] för att skicka resurser för bearbetning. Se [Använda mikrotjänster och bearbetningsprofiler](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/assets/manage/asset-microservices-configure-and-use.html).

## Användningsexempel som stöds av [!DNL Asset Compute Service] {#possible-use-cases-benefits}

[!DNL Asset Compute Service] har stöd för ett fåtal vanliga användningsområden, t.ex. grundläggande bildbehandling, Adobe applikationsspecifika konverteringar, och skräddarsydda applikationer som tillgodoser komplexa affärsbehov.

Du kan använda [!DNL Asset Compute] webbtjänsten för att generera miniatyrbilder för olika filtyper, bildåtergivningar med hög kvalitet för de [filformat](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/assets/file-format-support.html)som stöds. Se [användningsexempel som stöds via anpassad konfiguration](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/assets/manage/asset-microservices-configure-and-use.html#custom-config).

>[!NOTE]
>
>Tjänsten tillhandahåller inte resurslagring. Användarna tillhandahåller den och tillhandahåller referenser till källfiler och återgivningsfiler i molnlagringen.

<!-- TBD: Should this be mentioned in the docs?

|Asset Compute Service does not do this|Expectations from implementing client|
|---|---|
| Binary uploads or API-based asset ingestion. | Use other methods to ingest assets. |
| Store binaries or any persisted data across processing requests.| Each request is independent so treat it as a standalone request by sharing binary and processing instructions. |
| Store any configurations such as processing rules or settings for a user or an organization's account. | Add processing request to each request/instruction. |
| Direct event handling of asset creation events from storage systems and processing completed notifications, and errors. | Use Adobe I/O Events and other methods. |

-->

>[!MORELIKETHIS]
>
>* [Översikt över bearbetning av resurser med hjälp av mikrotjänster i Adobe Experience Manager som Cloud Service](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/assets/asset-microservices-overview.html).
>* [Dokumentation om Project Fire](https://www.adobe.io/apis/experienceplatform/project-firefly/docs.html).
>* [Filformat som kan bearbetas](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/assets/file-format-support.html).
>* [Versionsinformation om tjänsten Resursberäkning](release-notes.md)


<!-- **TBD:**
* Clarify the service can only be used within AEM as Cloud Service. The docs provided as context for custom application developers. Not to be used as a standalone service.
  ** and API as that plays a role in custom applications (accepting standard params, invoking Nui itself in the future, etc. (this is an outlook))

* link to aem as cloud service docs on asset ingestion and customization with processing profiles.
-->
