---
title: Arkitektur för [!DNL Asset Compute Service]
description: Hur [!DNL Asset Compute Service] API, program och SDK fungerar tillsammans för att tillhandahålla en molnbaserad resurshanteringstjänst.
exl-id: 658ee4b7-5eb1-4109-b263-1b7d705e49d6
source-git-commit: 2dde177933477dc9ac2ff5a55af1fd2366e18359
workflow-type: tm+mt
source-wordcount: '486'
ht-degree: 0%

---

# Arkitektur för [!DNL Asset Compute Service] {#overview}

The [!DNL Asset Compute Service] byggs ovanpå serverlösa [!DNL Adobe I/O] Runtime-plattform. Det ger stöd för Adobe Sensei innehållstjänster för resurser. Den anropande klienten (endast [!DNL Experience Manager] som [!DNL Cloud Service] stöds) tillhandahålls med den Adobe Sensei-genererade information som efterfrågas för tillgången. Den returnerade informationen är i JSON-format.

[!DNL Asset Compute Service] går att utöka genom att skapa anpassade program baserade på [!DNL Project Adobe Developer App Builder]. Dessa anpassade program [!DNL Project Adobe Developer App Builder] headless-appar och utföra uppgifter som att lägga till anpassade konverteringsverktyg eller anropa externa API:er för att utföra bildåtgärder.

[!DNL Project Adobe Developer App Builder] är ett ramverk för att bygga och driftsätta anpassade webbapplikationer på [!DNL Adobe I/O] runtime. För att skapa anpassade program kan utvecklarna utnyttja [!DNL React Spectrum] (Adobe’s UI toolkit), skapa mikrotjänster, skapa anpassade händelser och samordna API:er. Se [dokumentation för Adobe Developer App Builder](https://developer.adobe.com/app-builder/docs/overview).

Arkitekturen bygger på följande:

* Programmets modularitet - som bara innehåller det som behövs för en viss uppgift - gör att du kan koppla ihop program från varandra och hålla dem lätta.

* Det serverlösa konceptet med [!DNL Adobe I/O] Körningsmiljön har många fördelar: asynkron, mycket skalbar, isolerad, jobbbaserad bearbetning som är perfekt för materialbearbetning.

* Binär molnlagring innehåller de funktioner som krävs för att lagra och komma åt resursfiler och återgivningar individuellt, utan att fullständiga behörigheter krävs för lagringen, med hjälp av försignerade URL-referenser. Överföringsacceleration, CDN-cachning och samlokalisering av datorprogram med molnlagring ger optimal åtkomst till innehåll med låg latens. Både AWS- och Azure-moln stöds.

![Arkitektur för Asset compute Service](assets/architecture-diagram.png)

*Bild: Arkitektur för [!DNL Asset Compute Service] och hur det integreras med [!DNL Experience Manager], lagring och bearbetningsprogram.*

Arkitekturen består av följande delar:

* **Ett API- och orkestreringslager** tar emot begäranden (i JSON-format) som instruerar tjänsten att omvandla en källresurs till flera återgivningar. Förfrågningarna är asynkrona och returneras med ett aktiverings-ID, det vill säga jobb-ID. Instruktionerna är enbart deklarativa och för allt standardbearbetningsarbete (t.ex. generering av miniatyrbilder och textrahering) anger konsumenterna bara önskat resultat, men inte de program som hanterar vissa återgivningar. Allmänna API-funktioner som autentisering, analys och hastighetsbegränsning hanteras med Adobe API Gateway framför tjänsten och hanterar alla begäranden som ska [!DNL Adobe I/O] Körningsmiljö. Programdirigeringen görs dynamiskt av orkestreringslagret. Anpassade program kan anges av klienter för specifika renderingar och innehålla anpassade parametrar. Programkörningen kan vara helt parallell eftersom de är separata serverlösa funktioner i [!DNL Adobe I/O] Körningsmiljö.

* **Program som bearbetar resurser** som är specialiserade på vissa typer av filformat eller målåtergivningar. Ett program är som Unix pipe-konceptet: en indatafil omvandlas till en eller flera utdatafiler.

* **A [allmänt programbibliotek](https://github.com/adobe/asset-compute-sdk)** hanterar vanliga uppgifter som att hämta källfilen, överföra återgivningar, felrapportering, skicka händelser och övervaka . Detta är utformat så att utvecklingen av ett program förblir så enkel som möjligt, enligt den serverlösa idén, och kan begränsas till lokala interaktioner i filsystemet.

<!-- TBD:

* About the YAML file?
* See [https://developer.adobe.com/app-builder/docs/getting_started/first_app/#5-anatomy-of-a-project-firefly-application](https://www.adobe.io/project-firefly/docs/getting_started/first_app/#5-anatomy-of-a-project-firefly-application).

* minimize description to custom applications
* remove all internal stuff (e.g. Photoshop application, API Gateway) from text and diagram
* update diagram to focus on 3rd party custom applications ONLY
* Explain important transactions/handshakes?
* Flow of assets/control? See the illustration on the Nui diagrams wiki.
* Illustrations. See the SVG shared by Alex.
* Exceptions? Limitations? Call-outs? Gotchas?
* Do we want to add what basic processing is not available currently, that is expected by existing AEM customers?
-->
