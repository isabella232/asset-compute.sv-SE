---
title: Ange den utvecklingsmiljö som krävs för [!DNL Asset Compute Service]
description: Konfigurera utvecklarmiljön för [!DNL Asset Compute Service] att börja skapa och testa anpassad kod.
translation-type: tm+mt
source-git-commit: 95e384d2a298b3237d4f93673161272744e7f44a
workflow-type: tm+mt
source-wordcount: '372'
ht-degree: 0%

---


# Konfigurera en utvecklarmiljö {#create-dev-environment}

Om du vill skapa en konfiguration som gör att du kan utveckla för [!DNL Asset Compute Service] följer du dessa krav och instruktioner.

1. [Hämta åtkomst och ](https://github.com/AdobeDocs/project-firefly/blob/master/getting_started/setup.md#acquire-access-and-credentials) autentiseringsuppgifter för Project Fire.

1. [Konfigurera den lokala ](https://github.com/AdobeDocs/project-firefly/blob/master/getting_started/setup.md#local-environment-set-up) miljön och de verktyg som krävs.

1. Några andra verktyg som hjälper dig att komma igång smidigt är:

   * [Git](https://git-scm.com/).
   * [Docker Desktop](https://www.docker.com/get-started).
   * [NodeJS](https://nodejs.org) (v10 till v12 LTS, udda versioner rekommenderas inte) och  [NPM](https://www.npmjs.com). Användare av OSX HomeBrew kan göra `brew install node` för att installera båda. Annars kan du hämta den från [NodJS-hämtningssidan](https://nodejs.org/en/).
   * En IDE som är bra för NodeJS rekommenderar vi [Visual Studio Code (VS Code)](https://code.visualstudio.com) eftersom det är den IDE som stöds för felsökaren. Du kan använda vilken annan utvecklingsmiljö som helst som kodredigerare, men avancerad användning (t.ex. felsökare) stöds ännu inte.
   * [[!DNL Adobe I/O] CLI](https://github.com/adobe/aio-cli) (`aio`) - installera med  `npm install -g @adobe/aio-cli`.

1. Kontrollera att [kraven](/help/understand-extensibility.md#prerequisites-and-provisioning) uppfylls.

## Konfigurera ett Firefoly-projekt {#create-firefly-project}

1. Ge systemadministratör eller utvecklarroll åtkomst i Experience Organization. Detta kan anges av en systemadministratör i [Admin Console](https://adminconsole.adobe.com/overview).

1. Logga in på [Adobe Developer Console](https://console.adobe.io/). Se till att du är en del av samma Adobe Experience Cloud-organisation som [!DNL Experience Manager] som en [!DNL Cloud Service]-integrering. Mer information om Adobe Developer Console finns i [Konsoldokumentation](https://www.adobe.io/apis/experienceplatform/console/docs.html).

1. [Skapa ett Firefoly-projekt](https://www.adobe.io/apis/experienceplatform/project-firefly/docs.html#!AdobeDocs/project-firefly/master/getting_started/first_app.md). Klicka på **[!UICONTROL Skapa nytt projekt]** > **[!UICONTROL Projekt från mall]**. Välj eldfluga. Ett nytt Fireworks-projekt med två arbetsytor skapas: `Production` och `Stage`. Lägg till ytterligare arbetsytor, till exempel `Development`, efter behov.

1. I Fireworks väljer du en arbetsyta och prenumererar på de tjänster som behövs för Asset compute. Klicka på **Lägg till i projekt** > **API** och lägg till `Asset Compute`-, `IO Events`- och `IO Events Management`-tjänster. När du lägger till det första API:t uppmanas du att skapa en privat nyckel. Spara informationen på datorn när du behöver den här nyckeln för att testa det anpassade programmet med utvecklingsverktyget.

## Nästa steg {#next-step}

Nu när miljön är klar är du redo att [skapa ett anpassat program](develop-custom-application.md).

<!-- TBD items for later:
 
* Any steps in the beginning that lead to gotchas later should be called out for caution? For example,
  * don't change some defaults initially
  * know risks when deviating from standard path
  * naming conventions to follow
  * Retrieve and format credentials (YAML file details)
-->
