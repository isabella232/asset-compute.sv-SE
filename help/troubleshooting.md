---
title: Felsök [!DNL Asset Compute Service]
description: Felsök och felsök anpassade program med [!DNL Asset Compute Service].
exl-id: 017fff91-e5e9-4a30-babf-5faa1ebefc2f
source-git-commit: eed9da4b20fe37a4e44ba270c197505b50cfe77f
workflow-type: tm+mt
source-wordcount: '285'
ht-degree: 1%

---

# Felsök {#troubleshoot}

Några allmänna felsökningstips som kan hjälpa dig att felsöka med Asset compute Service är:

* Kontrollera att JavaScript-programmet inte kraschar vid start. Sådana krascher är vanligtvis relaterade till ett saknat bibliotek eller ett beroende.
* Kontrollera att det finns referenser till alla beroenden som ska installeras i programmets `package.json`-fil.
* Se till att eventuella fel som kan uppstå vid rensning vid fel inte genererar egna fel som döljer det ursprungliga problemet.

* När utvecklingsverktyget startas för första gången med en ny [!DNL Asset Compute Service]-integrering kan det misslyckas med den första bearbetningsbegäran om Asset compute Events-journalen inte är helt inställd. Vänta en stund tills journalen har konfigurerats innan du skickar en ny begäran.
* Om du stöter på fel när du skickar begäranden från Asset compute `/register` eller `/process` måste du se till att alla nödvändiga API:er läggs till i [!DNL Adobe I/O] Project and Workspace, d.v.s. Asset compute, [!DNL Adobe I/O] Events, [!DNL Adobe I/O] Events Management och [!DNL Adobe I/O] Runtime.

## Logga in problem via CLI[!DNL Adobe I/O] {#login-via-aio-cli}

Om du har problem med att logga in på [!DNL Adobe Developer Console] [via  [!DNL Adobe I/O] CLI](https://www.adobe.io/project-firefly/docs/getting_started/first_app/#3-signing-in-from-cli) lägger du manuellt till de autentiseringsuppgifter som krävs för utveckling, testning och distribution av ditt anpassade program:

1. Navigera till ditt Firefoly-projekt och din arbetsyta på [Adobe Developer Console](https://console.adobe.io/) och tryck på **[!UICONTROL Hämta]** från det övre högra hörnet. Öppna den här filen och spara denna JSON på en säker plats på datorn.

1. Navigera till ENV-filen i ditt Fireworks-program.

1. Lägg till inloggningsuppgifterna för [!DNL Adobe I/O]-miljön. Hämta inloggningsuppgifterna för [!DNL Adobe I/O] A Runtime från den hämtade JSON:n. Autentiseringsuppgifterna är under `project.workspace.services.runtime`. Lägg till [!DNL Adobe I/O]-autentiseringsuppgifterna för körning i `AIO_runtime_XXX`-variablerna:

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
