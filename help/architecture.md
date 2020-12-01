---
title: Arkitektur för [!DNL Asset Compute Service].
description: Hur [!DNL Asset Compute Service] API, program och SDK fungerar tillsammans för att tillhandahålla en molnbaserad resurshanteringstjänst.
translation-type: tm+mt
source-git-commit: c392b8588929f7b13db13e42a3f17bbc4f68a376
workflow-type: tm+mt
source-wordcount: '494'
ht-degree: 0%

---


# Arkitektur för [!DNL Asset Compute Service] {#overview}

[!DNL Asset Compute Service] är byggt ovanpå den serverlösa Adobe I/O Runtime-plattformen. Det ger stöd för Adobe Sensei innehållstjänster för resurser. Den anropande klienten (endast [!DNL Experience Manager] som [!DNL Cloud Service] stöds) får den Adobe Sensei-genererade information som den sökte efter resursen. Den returnerade informationen är i JSON-format.

[!DNL Asset Compute Service] går att utöka genom att skapa anpassade program baserade på  [!DNL Project Firefly]. Dessa anpassade program är [!DNL Project Firefly] headless-appar och utför uppgifter som att lägga till anpassade konverteringsverktyg eller anropa externa API:er för att utföra bildåtgärder.

[!DNL Project Firefly] är ett ramverk för att skapa och distribuera anpassade webbprogram på  [!DNL Adobe I/O] körningsmiljön. Om du vill skapa anpassade program kan utvecklarna använda [!DNL React Spectrum] (Adobe’s UI toolkit), skapa mikrotjänster, skapa anpassade händelser och ordna API:er. Mer information finns i [dokumentationen för Project Fire](https://www.adobe.io/apis/experienceplatform/project-firefly/docs.html).

Arkitekturen bygger på följande:

* Programmets modularitet - som bara innehåller det som behövs för en viss uppgift - gör att du kan koppla ihop program från varandra och hålla dem lätta.

* Adobe I/O Runtime serverlösa koncept ger många fördelar: asynkron, mycket skalbar, isolerad, jobbbaserad bearbetning som är perfekt för materialbearbetning.

* Binär molnlagring innehåller de funktioner som krävs för att lagra och komma åt resursfiler och återgivningar individuellt, utan att fullständiga behörigheter krävs för lagringen, med hjälp av försignerade URL-referenser. Överföringsacceleration, CDN-cachning och samlokalisering av datorprogram med molnlagring ger optimal åtkomst till innehåll med låg latens. Både AWS- och Azure-moln stöds.

![Arkitektur för Asset compute Service](assets/architecture-diagram.png)

*Bild: Arkitektur för  [!DNL Asset Compute Service] och hur det integreras med program  [!DNL Experience Manager]för lagring och bearbetning.*

Arkitekturen består av följande delar:

* **Ett API- och** orkestreringslager tar emot begäranden (i JSON-format) som instruerar tjänsten att omvandla en källresurs till flera renderingar. Dessa begäranden är asynkrona och returneras med ett aktiverings-ID (även kallat jobb-ID). Instruktionerna är enbart deklarativa och för allt standardbearbetningsarbete (t.ex. generering av miniatyrbilder och textrahering) anger konsumenterna bara önskat resultat, men inte de program som hanterar vissa återgivningar. Allmänna API-funktioner som autentisering, analys och hastighetsbegränsning hanteras med Adobe API Gateway framför tjänsten och hanterar alla förfrågningar som går till I/O-miljön. Programdirigeringen görs dynamiskt av orkestreringslagret. Anpassade program kan anges av klienter för specifika renderingar och innehålla anpassade parametrar. Programkörningen kan vara helt parallell eftersom de är separata serverlösa funktioner i I/O-miljön.

* **Program för att bearbeta** resurser som är specialiserade på vissa typer av filformat eller målåtergivningar. Ett program är som Unix pipe-konceptet: en indatafil omvandlas till en eller flera utdatafiler.

* **Ett  [vanligt ](https://github.com/adobe/asset-compute-sdk)** programbibliotek hanterar vanliga åtgärder som att hämta källfilen, överföra återgivningar, felrapportering, skicka händelser och övervaka . Detta är utformat så att utvecklingen av ett program förblir så enkel som möjligt, enligt den serverlösa idén, och kan begränsas till lokala interaktioner i filsystemet.

<!-- TBD:

* About the YAML file?
* See [https://github.com/AdobeDocs/project-firefly/blob/master/getting_started/first_app.md#5-anatomy-of-a-project-firefly-application](https://github.com/AdobeDocs/project-firefly/blob/master/getting_started/first_app.md#5-anatomy-of-a-project-firefly-application).

* minimize description to custom applications
* remove all internal stuff (e.g. Photoshop application, API Gateway) from text and diagram
* update diagram to focus on 3rd party custom applications ONLY
* Explain important transactions/handshakes?
* Flow of assets/control? See the illustration on the Nui diagrams wiki.
* Illustrations. See the SVG shared by Alex.
* Exceptions? Limitations? Call-outs? Gotchas?
* Do we want to add what basic processing is not available currently, that is expected by existing AEM customers?
-->
