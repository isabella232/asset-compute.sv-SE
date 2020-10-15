---
title: Förstå om att utöka [!DNL Asset Compute Service].
description: När och hur [!DNL Asset Compute Service] funktionaliteten ska utökas för att utföra anpassad mediebearbetning.
translation-type: tm+mt
source-git-commit: 54afa44d8d662ee1499a385f504fca073ab6c347
workflow-type: tm+mt
source-wordcount: '275'
ht-degree: 0%

---


# Introduktion till utökningsbarhet {#introduction-to-extensibilty}

Många återgivningskrav, som konvertering till format och storleksändring av bilder, hanteras av [Bearbeta profiler [!DNL Experience Manager] som en Cloud Service](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/assets/asset-microservices-overview.html). Mer komplexa affärsbehov kan behöva en skräddarsydd lösning som passar organisationens behov. [!DNL Asset Compute Service] kan utökas genom att skapa anpassade program som anropas från Bearbeta profiler i [!DNL Experience Manager]. Dessa anpassade program uppfyller de [användningsfall](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/assets/manage/asset-microservices-configure-and-use.html)som stöds.

>[!NOTE]
>
>[!DNL Asset Compute Service] är bara tillgängligt för användning med [!DNL Experience Manager] som Cloud Service.

De anpassade programmen är headless [Project Fire](https://github.com/AdobeDocs/project-firefly) -appar. Att bygga ut [!DNL Asset Compute Service] med anpassade program är enkelt tack vare utvecklingsverktygen [Asset Compute SDK](https://github.com/adobe/asset-compute-sdk) och Project Fire. Detta gör att utvecklare kan fokusera på affärslogik. Att skapa anpassade program är enkelt än att skapa en Adobe I/O Runtime-åtgärd utan vanliga servrar. Det är en enda Node.js JavaScript-funktion. Det [grundläggande anpassade programexemplet](https://github.com/adobe/asset-compute-example-workers/blob/master/projects/worker-basic/worker-basic.js) visar det.

## Krav och etableringskrav {#prerequisites-and-provisioning}

Kontrollera att du uppfyller följande krav:

* Project Fire-verktygen är installerade på datorn.
* En [!DNL Experience Cloud] organisation. Mer information [här](https://github.com/AdobeDocs/project-firefly/blob/master/getting_started/setup.md#acquire-access-and-credentials).
* Experience Organization måste ha [!DNL Experience Manager] som Cloud Service aktiverat.
* [!DNL Adobe Experience Cloud] är en del av programmet för förhandsgranskning av [!DNL Project Firefly] utvecklare. Se [hur du ansöker om åtkomst](https://github.com/AdobeDocs/project-firefly/blob/master/overview/getting_access.md).
* Se till att utvecklarrollen eller administratörsbehörigheten finns i organisationen för utvecklaren.
* Kontrollera att [Adobe I/O CLI](https://github.com/adobe/aio-cli) är installerat lokalt.

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
