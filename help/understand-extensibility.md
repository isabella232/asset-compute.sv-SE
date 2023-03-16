---
title: Förstå om att utöka [!DNL Asset Compute Service]
description: När och hur du ska utöka [!DNL Asset Compute Service] funktioner för att hantera egna resurser.
exl-id: 3b903364-34cc-44d5-9a03-24a0102cf85d
source-git-commit: 2dde177933477dc9ac2ff5a55af1fd2366e18359
workflow-type: tm+mt
source-wordcount: '260'
ht-degree: 0%

---

# Introduktion till utökningsbarhet {#introduction-to-extensibilty}

Många krav på återgivning, till exempel konvertering till format och storleksändring av bilder, hanteras av [Bearbetar profiler i [!DNL Experience Manager] som [!DNL Cloud Service]](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/assets/asset-microservices-overview.html). Mer komplexa affärsbehov kan behöva en skräddarsydd lösning som passar organisationens behov. [!DNL Asset Compute Service] kan utökas genom att skapa anpassade program som anropas från Bearbeta profiler i [!DNL Experience Manager]. Dessa anpassade program är anpassade till [användningsfall som stöds](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/assets/manage/asset-microservices-configure-and-use.html).

>[!NOTE]
>
>[!DNL Asset Compute Service] är endast tillgänglig för användning med [!DNL Experience Manager] som [!DNL Cloud Service].

De anpassade programmen är headless [Adobe Developer App Builder](https://github.com/AdobeDocs/app-builder) appar. Utöka [!DNL Asset Compute Service] med skräddarsydda program på ett enkelt sätt via [asset compute SDK](https://github.com/adobe/asset-compute-sdk) och utvecklingsverktygen i Adobe Developer App Builder. Detta gör att utvecklare kan fokusera på affärslogik. Att skapa anpassade program är lika enkelt som att skapa en ren serverlös [!DNL Adobe I/O] Körningsåtgärd. Det är en enda Node.js JavaScript-funktion. The [exempel på grundläggande anpassad applikation](https://github.com/adobe/asset-compute-example-workers/blob/master/projects/worker-basic/worker-basic.js) illustrerar det.

## Krav och etableringskrav {#prerequisites-and-provisioning}

Kontrollera att du uppfyller följande krav:

* Adobe Developer App Builder-verktygen är installerade på datorn.
* An [!DNL Experience Cloud] organisation. Mer information [här](https://developer.adobe.com/app-builder/docs/getting_started/#acquire-access-and-credentials).
* Experience Organization måste ha [!DNL Experience Manager] som [!DNL Cloud Service] aktiverat.
* [!DNL Adobe Experience Cloud] organisationen ingår i [!DNL Adobe Developer App Builder] förhandsgranskningsprogram för utvecklare. Se [hur man ansöker om åtkomst](https://developer.adobe.com/app-builder/docs/overview/getting_access).
* Se till att utvecklarrollen eller administratörsbehörigheten finns i organisationen för utvecklaren.
* Se till att [[!DNL Adobe I/O] CLI](https://github.com/adobe/aio-cli) installeras lokalt.

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
