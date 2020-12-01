---
title: Felsök [!DNL Asset Compute Service].
description: Felsök och felsök anpassade program med [!DNL Asset Compute Service].
translation-type: tm+mt
source-git-commit: 68d910cd092fccb599c361f24daff80460129e1c
workflow-type: tm+mt
source-wordcount: '306'
ht-degree: 1%

---


# Felsök {#troubleshoot}

Några allmänna felsökningstips som kan hjälpa dig att felsöka med Asset compute Service är:

* Kontrollera att JavaScript-programmet inte kraschar vid start. Sådana krascher är vanligtvis relaterade till ett saknat bibliotek eller ett beroende.
* Kontrollera att det finns referenser till alla beroenden som ska installeras i programmets `package.json`-fil.
* Se till att eventuella fel som kan uppstå vid rensning vid fel inte genererar egna fel som döljer det ursprungliga problemet.

* När utvecklingsverktyget startas för första gången med en ny [!DNL Asset Compute Service]-integrering, kan det misslyckas med den första bearbetningsbegäran eftersom Asset compute Events-journalen kanske inte är helt inställd. Vänta en stund tills journalen har konfigurerats innan du skickar en ny begäran.
* Om det uppstår fel när du skickar begäranden från Asset compute `/register` eller `/process` måste alla nödvändiga API:er läggas till i Adobe I/O Project and Workspace, d.v.s. Asset compute, IO Events, IO Events Management och Runtime.

## Logga in problem via Adobe I/O CLI {#login-via-aio-cli}

Om du har problem med att logga in på [!DNL Adobe Developer Console] [via Adobe I/O CLI](https://github.com/AdobeDocs/project-firefly/blob/master/getting_started/first_app.md#3-signing-in-from-cli) lägger du manuellt till de autentiseringsuppgifter som krävs för att utveckla, testa och distribuera ditt anpassade program:

1. Navigera till ditt Firefoly-projekt och din arbetsyta på [Adobe Developer Console](https://console.adobe.io/) och tryck på **[!UICONTROL Hämta]** från det övre högra hörnet. Öppna den här filen och spara denna JSON på en säker plats på datorn.

1. Navigera till ENV-filen i ditt Fireworks-program.

1. Lägg till Adobe I/O Runtime-autentiseringsuppgifter. Hämta Adobe I/O Runtime-inloggningsuppgifterna från det hämtade JSON-programmet. Autentiseringsuppgifterna är under `project.workspace.services.runtime`. Lägg till I/O-körningsuppgifter i `AIO_runtime_XXX`-variablerna:

   ```json
   AIO_runtime_auth=
   AIO_runtime_namespace=
   ```

1. Lägg till den absoluta sökvägen till den hämtade JSON-filen i steg 1:

   ```json
       ASSET_COMPUTE_INTEGRATION_FILE_PATH=
   ```

1. Ställ in resten av de [obligatoriska inloggningsuppgifterna](develop-custom-application.md) som behövs för utvecklingsverktyget.

<!-- TBD for later:
Add any best practices for developers in this section:
* Any items to take care of when creating projects.
* Any naming conventions, reserved keywords, etc.?
* Any terms that can become a source of confusion later based on our OOTB naming.

* If required, add limitations for custom applications and spin those off as best practices.
* Do NOT borrow any content from https://git.corp.adobe.com/nui/nui/blob/master/doc/worker_api.md. It is outdated and irrelevant for 3rd party custom applications.
-->
