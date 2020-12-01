---
title: Versionsinformation för [!DNL Asset Compute Service].
description: Nya funktioner, förbättringar och kända fel i [!DNL Asset Compute Service].
translation-type: tm+mt
source-git-commit: 68d910cd092fccb599c361f24daff80460129e1c
workflow-type: tm+mt
source-wordcount: '193'
ht-degree: 0%

---


# Versionsinformation om [!DNL Asset Compute Service] {#release-notes}

Den senaste versionen av [!DNL Asset Compute Service] släpptes 30 juli 2020.

<!--

To test your custom applications with the [developer tool](https://github.com/adobe/asset-compute-devtool), you need access to a [cloud storage container](https://github.com/adobe/asset-compute-devtool#prerequisites). Currently, Adobe supports Azure Blob Storage and AWS S3.

>[!NOTE]
>
>Cloud storage access is only required for using the developer tool. You can still create, test and deploy custom applications with out using the developer tool.
-->

## Nyheter {#what-is-new}

Detta är den första versionen av [!DNL Asset Compute Service]. Det är en skalbar och utbyggbar tjänst på [!DNL Adobe Experience Cloud] som bearbetar digitala resurser. Det kan omvandla bild, video, dokument och andra filformat till olika renderingar, bland annat miniatyrer, extraherad text och metadata samt arkiv.

För närvarande kan [!DNL Asset Compute Service] bara användas i [!DNL Experience Manager] som en Cloud Service.

## Begränsningar och kända fel {#known-limitations}

Om du vill testa ditt anpassade program med [utvecklarverktyget](https://github.com/adobe/asset-compute-devtool) behöver du åtkomst till en [molnlagringsbehållare](https://github.com/adobe/asset-compute-devtool#prerequisites).

* Åtkomsten till molnlagringen (som skiljer sig från blobbutiken [!DNL Experience Manager]) behövs bara för utvecklingsverktyget. Du kan fortfarande skapa, testa och distribuera anpassade program utan utvecklarverktyget.
* Det kan vara en delad behållare som används av flera utvecklare i olika projekt.

## Contribute {#contribute-open-source}

[!DNL Asset Compute Service] Utbyggbarhet utvecklas under en öppen utvecklingsmodell på  [github.com/](https://github.com/adobe) adobebe som tar emot bidrag från utbyggnadsutvecklare. Alla komponenter som är relevanta för att utveckla, skapa, testa och distribuera anpassade program är öppen källkod. Se [hur och var du ska bidra till beräkningstjänsten](contribute-to-compute-service.md).

<!-- **TBD:**
* Are we versioning the releases?
* Is there any compatibility information to be added? With Project Firefly versions, or AEMaaCS releases, or other offerings/integrations such as InDesign Server?
-->
