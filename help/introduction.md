---
title: Introduktion till  [!DNL Asset Compute Service].
description: '[!DNL Asset Compute Service] är en molnbaserad resurshanteringstjänst som minskar komplexiteten och förbättrar skalbarheten.'
translation-type: tm+mt
source-git-commit: d26ae470507e187249a472ececf5f08d803a636c
workflow-type: tm+mt
source-wordcount: '314'
ht-degree: 0%

---


# Översikt över [!DNL Asset Compute Service] {#overview}

[!DNL Asset Compute Service] är en skalbar och utbyggbar tjänst för  [!DNL Adobe Experience Cloud] att bearbeta digitala resurser. Det kan omvandla bild, video, dokument och andra filformat till olika renderingar, bland annat miniatyrer, extraherad text och metadata samt arkiv.

Utvecklare kan plugin-program för anpassade resurser (kallas även anpassade arbetare) för att hantera anpassade användningsfall. Tjänsten fungerar på [!DNL Adobe I/O]-miljön. Den kan utökas via [!DNL Project Firefly] headless-appar skrivna i Node.js. Dessa kan utföra anpassade åtgärder som att anropa externa API:er för att utföra bildåtgärder eller utnyttja stödet för [!DNL Adobe Sensei].

[!DNL Project Firefly] är ett ramverk för att bygga och driftsätta anpassade webbapplikationer för  [!DNL Adobe I/O] körning för att utöka Adobe Experience Cloud lösningar. Om du vill skapa anpassade program kan utvecklarna använda [!DNL React Spectrum] (Adobe’s UI toolkit), skapa mikrotjänster, skapa anpassade händelser och ordna API:er. Mer information finns i [dokumentationen för Project Fire](https://www.adobe.io/apis/experienceplatform/project-firefly/docs.html).

>[!NOTE]
>
>För närvarande kan [!DNL Asset Compute Service] bara användas via [!DNL Experience Manager] som [!DNL Cloud Service]. Administratörer skapar bearbetningsprofiler som kan anropa [!DNL Asset Compute Service] för att skicka resurser för bearbetning. Se [använda resursmikrotjänster och bearbetningsprofiler](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/assets/manage/asset-microservices-configure-and-use.html).

## Användningsexempel som stöds av [!DNL Asset Compute Service] {#possible-use-cases-benefits}

[!DNL Asset Compute Service] har stöd för ett fåtal vanliga användningsområden, t.ex. grundläggande bildbehandling, Adobe applikationsspecifika konverteringar, och skräddarsydda applikationer som tillgodoser komplexa affärsbehov.

Du kan använda webbtjänsten [!DNL Asset Compute] för att generera miniatyrer för olika filtyper, bildåtergivning med hög kvalitet för de [filformat som stöds](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/assets/file-format-support.html). Se [användningsfall som stöds via anpassad konfiguration](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/assets/manage/asset-microservices-configure-and-use.html).

>[!NOTE]
>
>Tjänsten tillhandahåller inte resurslagring. Användarna tillhandahåller den och tillhandahåller referenser till källfiler och återgivningsfiler i molnlagringen.

<!-- TBD: Should this be mentioned in the docs?

|Asset Compute Service does not do this|Expectations from implementing client|
|---|---|
| Binary uploads or API-based asset ingestion. | Use other methods to ingest assets. |
| Store binaries or any persisted data across processing requests.| Each request is independent so treat it as a standalone request by sharing binary and processing instructions. |
| Store any configurations such as processing rules or settings for a user or an organization's account. | Add processing request to each request/instruction. |
| Direct event handling of asset creation events from storage systems and processing completed notifications, and errors. | Use [!DNL Adobe I/O] Events and other methods. |

-->

>[!MORELIKETHIS]
>
>* [Översikt över tillgångsbearbetning med tillgångsmikrotjänster  [!DNL Adobe Experience Manager] som en [!DNL Cloud Service]](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/assets/asset-microservices-overview.html).
>* [Dokumentation om Project Fire](https://www.adobe.io/apis/experienceplatform/project-firefly/docs.html).
>* [Filformat som kan bearbetas](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/assets/file-format-support.html).
>* [Versionsinformation om tjänsten Asset compute](release-notes.md)


<!-- **TBD:**
* Clarify the service can only be used within AEM as Cloud Service. The docs provided as context for custom application developers. Not to be used as a standalone service.
  ** and API as that plays a role in custom applications (accepting standard params, invoking Nui itself in the future, etc. (this is an outlook))

* link to aem as cloud service docs on asset ingestion and customization with processing profiles.
-->
