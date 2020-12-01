---
title: Distribuera  [!DNL Asset Compute Service] anpassat program.
description: Distribuera  [!DNL Asset Compute Service] anpassat program.
translation-type: tm+mt
source-git-commit: 78c1246f5fc42006013701a6cf4d375a1d8c9fd8
workflow-type: tm+mt
source-wordcount: '183'
ht-degree: 0%

---


# Distribuera ett anpassat program {#deploy-custom-application}

Använd kommandot [AIR App Deployment](https://github.com/adobe/aio-cli#aio-appdeploy) för att distribuera programmet. I terminalen visar kommandot en URL för att komma åt det anpassade programmet. URL:en har formatet `https://[namespace].adobeio-static.net/api/v1/web/[appname]-[appversion]/[workername]`.

Använd kommandot [`aio app get-url`](https://github.com/adobe/aio-cli#aio-appget-url-action) för att hämta samma URL utan att omdistribuera programmet.

Använd URL:en i en [bearbetningsprofil i [!DNL Experience Manager] som en [!DNL Cloud Service]](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/assets/manage/asset-microservices-configure-and-use.html) för att integrera ditt program med [!DNL Experience Manager] som en [!DNL Cloud Service].

Kontrollera att ditt Firefoly-projekt och din arbetsyta motsvarar [!DNL Experience Manager] som en [!DNL Cloud Service]-miljö där du vill använda åtgärden. Den har olika miljöer för utveckling, staging och produktion. Du kan verifiera miljön genom att kontrollera `AIO_runtime_*`-inloggningsuppgifterna som är definierade i ENV-filen i roten för Fireworks-programmet. Om du till exempel vill distribuera till en `Stage`-arbetsyta har `AIO_runtime_namespace` formatet `xxxxxx_xxxxxxxxx_stage`. Om du vill integrera med [!DNL Experience Manager] som en [!DNL Cloud Service]-produktionsmiljö använder du program-URL:er från arbetsytan i Fireworks `Production`.

>[!CAUTION]
>
>Använd inte en personlig arbetsyta i viktiga [!DNL Experience Manager]-miljöer.

>[!MORELIKETHIS]
>
>* [Förstå och hantera miljöer  [!DNL Experience Manager] som [!DNL Cloud Service]](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/manage-environments.html) en helhet.

