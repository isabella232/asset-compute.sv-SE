---
title: Distribuera [!DNL Asset Compute Service] anpassat program
description: Distribuera [!DNL Asset Compute Service] anpassat program.
exl-id: a68d4f59-8a8f-43b2-8bc6-19320ac8c9ef
source-git-commit: 129651ba432b75703bc27baa7081da60302f828d
workflow-type: tm+mt
source-wordcount: '184'
ht-degree: 0%

---

# Distribuera ett anpassat program {#deploy-custom-application}

Använd [driftsättning av aio-appar](https://github.com/adobe/aio-cli#aio-appdeploy) -kommando. I terminalen visar kommandot en URL för att komma åt det anpassade programmet. URL:en har formatet `https://[namespace].adobeio-static.net/api/v1/web/[appname]-[appversion]/[workername]`.

Om du vill hämta samma URL utan att distribuera om programmet använder du [`aio app get-url`](https://github.com/adobe/aio-cli#aio-app-get-url-action) -kommando.

Använd URL:en i en [Bearbetar profil i [!DNL Experience Manager] som [!DNL Cloud Service]](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/assets/manage/asset-microservices-configure-and-use.html) integrera applikationen med [!DNL Experience Manager] som [!DNL Cloud Service].

Kontrollera att ditt App Builder-projekt och din arbetsyta motsvarar [!DNL Experience Manager] som [!DNL Cloud Service] miljö där du vill använda åtgärden. Den har olika miljöer för utveckling, staging och produktion. Du kan verifiera miljön genom att kontrollera `AIO_runtime_*` inloggningsuppgifter som definieras i ENV-filen i roten för Firefoly-programmet. Till exempel för att distribuera till en `Stage` arbetsytan `AIO_runtime_namespace` har formatet `xxxxxx_xxxxxxxxx_stage`. Integrera med [!DNL Experience Manager] som [!DNL Cloud Service] Produktionsmiljö, använd program-URL:er från din Firefoly `Production` arbetsyta.

>[!CAUTION]
>
>Använd inte en personlig arbetsyta på viktiga [!DNL Experience Manager] miljöer.

>[!MORELIKETHIS]
>
>* [Förstå och hantera miljöer i [!DNL Experience Manager] som [!DNL Cloud Service]](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/manage-environments.html).

