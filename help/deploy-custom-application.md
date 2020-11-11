---
title: Distribuera [!DNL Asset Compute Service] anpassat program.
description: Distribuera [!DNL Asset Compute Service] anpassat program.
translation-type: tm+mt
source-git-commit: 79630efa8cee2c8919d11e9bb3c14ee4ef54d0f3
workflow-type: tm+mt
source-wordcount: '197'
ht-degree: 0%

---


# Distribuera ett anpassat program {#deploy-custom-application}

Om du vill distribuera ditt program använder du [AIR-kommandot för](https://github.com/adobe/aio-cli#aio-appdeploy) programdistribution. I terminalen visar kommandot en URL för att komma åt det anpassade programmet. URL:en har formatet `https://[namespace].adobeio-static.net/api/v1/web/[appname]-[appversion]/[workername]`.

Använd [`aio app get-url`](https://github.com/adobe/aio-cli#aio-appget-url-action) kommando för att få samma URL utan att omdistribuera programmet.

Använd URL:en i en [bearbetningsprofil i Experience Manager som Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/assets/manage/asset-microservices-configure-and-use.html) för att integrera programmet med [!DNL Experience Manager] som en Cloud Service.

Se till att ditt Firefoly-projekt och din arbetsyta motsvarar den [!DNL Experience Manager] som en Cloud Service där du vill använda åtgärden. Den har olika miljöer för utveckling, staging och produktion. Du kan verifiera miljön genom att kontrollera `AIO_runtime_*` inloggningsuppgifter som är definierade i ENV-filen i roten av ditt Fireworks-program. Om du till exempel vill distribuera till en `Stage` arbetsyta `AIO_runtime_namespace` har den formatet `xxxxxx_xxxxxxxxx_stage`. Om du vill integrera med [!DNL Experience Manager] som en Cloud Service Production-miljö använder du program-URL:er från din Fireworks- `Production` arbetsyta.

>[!CAUTION]
>
>Använd inte en personlig arbetsyta i kritiska [!DNL Experience Manager] miljöer.

>[!MORELIKETHIS]
>
>* [Förstå och hantera miljöer i Experience Manager som en Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/manage-environments.html).

