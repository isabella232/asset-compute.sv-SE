---
title: Felsök [!DNL Asset Compute Service].
description: Felsöka och felsöka anpassade program med [!DNL Asset Compute Service].
translation-type: tm+mt
source-git-commit: 68d910cd092fccb599c361f24daff80460129e1c
workflow-type: tm+mt
source-wordcount: '306'
ht-degree: 1%

---


# Felsök {#troubleshoot}

Några allmänna felsökningstips som kan hjälpa dig att felsöka med tjänsten Resursberäkning är:

* Kontrollera att JavaScript-programmet inte kraschar vid start. Sådana krascher är vanligtvis relaterade till ett saknat bibliotek eller ett beroende.
* Kontrollera att det finns referenser till alla beroenden som ska installeras i programmets `package.json` fil.
* Se till att eventuella fel som kan uppstå vid rensning vid fel inte genererar egna fel som döljer det ursprungliga problemet.

* När utvecklingsverktyget startas för första gången med en ny [!DNL Asset Compute Service] integrering, kan det misslyckas med den första bearbetningsbegäran eftersom resursberäkningsjournalen kanske inte är helt inställd. Vänta en stund tills journalen har konfigurerats innan du skickar en ny begäran.
* Om det uppstår fel när du skickar tillgångsberäkning `/register` eller `/process` begäranden ska du se till att alla nödvändiga API:er läggs till i Adobe I/O-projekt och arbetsyta, det vill säga Resursberäkning, IO-händelser, IO-händelsehantering och körningsmiljö.

## Logga in problem via Adobe I/O CLI {#login-via-aio-cli}

Om du har problem med att logga in [!DNL Adobe Developer Console] via Adobe I/O CLI [](https://github.com/AdobeDocs/project-firefly/blob/master/getting_started/first_app.md#3-signing-in-from-cli)lägger du manuellt till de inloggningsuppgifter som krävs för att utveckla, testa och distribuera ditt anpassade program:

1. Navigera till ditt Firefoly-projekt och din arbetsyta på [Adobe Developer Console](https://console.adobe.io/) och tryck på **[!UICONTROL Download]** (Ladda ned) längst upp till höger. Öppna den här filen och spara denna JSON på en säker plats på datorn.

1. Navigera till ENV-filen i ditt Fireworks-program.

1. Lägg till Adobe I/O Runtime-autentiseringsuppgifter. Hämta Adobe I/O Runtime-inloggningsuppgifterna från det hämtade JSON-programmet. Autentiseringsuppgifterna är under `project.workspace.services.runtime`. Lägg till I/O Runtime-autentiseringsuppgifterna i `AIO_runtime_XXX` variablerna:

   ```json
   AIO_runtime_auth=
   AIO_runtime_namespace=
   ```

1. Lägg till den absoluta sökvägen till den hämtade JSON-filen i steg 1:

   ```json
       ASSET_COMPUTE_INTEGRATION_FILE_PATH=
   ```

1. Ställ in resten av de [nödvändiga autentiseringsuppgifterna](develop-custom-application.md) som krävs för utvecklingsverktyget.

<!-- TBD for later:
Add any best practices for developers in this section:
* Any items to take care of when creating projects.
* Any naming conventions, reserved keywords, etc.?
* Any terms that can become a source of confusion later based on our OOTB naming.

* If required, add limitations for custom applications and spin those off as best practices.
* Do NOT borrow any content from https://git.corp.adobe.com/nui/nui/blob/master/doc/worker_api.md. It is outdated and irrelevant for 3rd party custom applications.
-->
