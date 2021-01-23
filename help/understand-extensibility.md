---
title: Förstå om att utöka [!DNL Asset Compute Service]
description: När och hur du ska utöka funktionen [!DNL Asset Compute Service] för att utföra anpassad resurshantering.
translation-type: tm+mt
source-git-commit: 95e384d2a298b3237d4f93673161272744e7f44a
workflow-type: tm+mt
source-wordcount: '259'
ht-degree: 0%

---


# Introduktion till utökningsbarhet {#introduction-to-extensibilty}

Många återgivningskrav, som konvertering till format och storleksändring av bilder, uppfylls av [Bearbetningsprofiler i [!DNL Experience Manager] som en [!DNL Cloud Service]](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/assets/asset-microservices-overview.html). Mer komplexa affärsbehov kan behöva en skräddarsydd lösning som passar organisationens behov. [!DNL Asset Compute Service] kan utökas genom att skapa anpassade program som anropas från Bearbeta profiler i  [!DNL Experience Manager]. Dessa anpassade program uppfyller [användningsexemplen](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/assets/manage/asset-microservices-configure-and-use.html) som stöds.

>[!NOTE]
>
>[!DNL Asset Compute Service] är endast tillgängligt för användning med  [!DNL Experience Manager] som  [!DNL Cloud Service]en.

De anpassade programmen är headless [Project Fire](https://github.com/AdobeDocs/project-firefly)-program. Det är enkelt att utöka [!DNL Asset Compute Service] med anpassade program via utvecklarverktygen [Asset compute SDK](https://github.com/adobe/asset-compute-sdk) och Project Firefly. Detta gör att utvecklare kan fokusera på affärslogik. Att skapa anpassade program är lika enkelt som att skapa en enkel serverlös [!DNL Adobe I/O]-körningsåtgärd. Det är en enda Node.js JavaScript-funktion. Det [grundläggande anpassade programexemplet](https://github.com/adobe/asset-compute-example-workers/blob/master/projects/worker-basic/worker-basic.js) illustrerar det.

## Krav och etableringskrav {#prerequisites-and-provisioning}

Kontrollera att du uppfyller följande krav:

* Project Fire-verktygen är installerade på datorn.
* En [!DNL Experience Cloud]-organisation. Mer information [här](https://github.com/AdobeDocs/project-firefly/blob/master/getting_started/setup.md#acquire-access-and-credentials).
* Experience Organization måste ha [!DNL Experience Manager] som [!DNL Cloud Service] aktiverat.
* [!DNL Adobe Experience Cloud] är en del av förhandsgranskningsprogrammet för  [!DNL Project Firefly] utvecklare. Se [hur du ansöker om åtkomst](https://github.com/AdobeDocs/project-firefly/blob/master/overview/getting_access.md).
* Se till att utvecklarrollen eller administratörsbehörigheten finns i organisationen för utvecklaren.
* Kontrollera att [[!DNL Adobe I/O] CLI](https://github.com/adobe/aio-cli) är installerat lokalt.

<!-- TBD for later:

* What all accesses and licenses are required?
* What all permissions are required to create, debug, and deploy custom applications?
* How do developers get access and provision the required apps?
* What is repository management?
* Anything on security and data transfer?
* What about handling personal or sensitive information?
* Custom application SLA is dependent on SLAs of various services it depends on.
* Document how the devs can get to know the KPIs of their custom applications. The KPIs are dependent on the performance at Adobe's side, amongst other things.
-->
