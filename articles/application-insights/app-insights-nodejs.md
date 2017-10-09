---
title: "aaaMonitor Node.js usług za pomocą usługi Azure Application Insights | Dokumentacja firmy Microsoft"
description: "Monitoruj wydajność i diagnozuj problemy w usługach Node.js za pomocą usługi Application Insights."
services: application-insights
documentationcenter: nodejs
author: joshgav
manager: carmonm
ms.assetid: 2ec7f809-5e1a-41cf-9fcd-d0ed4bebd08c
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: get-started-article
ms.date: 05/01/2017
ms.author: bwren
ms.openlocfilehash: 0a7e66990cd4d3a2fcaf3fa779adb336c861f8ce
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-your-nodejs-services-and-apps-with-application-insights"></a>Monitorowanie usług i aplikacji Node.js za pomocą usługi Application Insights

[Azure Application Insights](app-insights-overview.md) monitoruje usług zaplecza i składniki po ich wdrożeniu toohelp możesz [odnajdywania i szybkie diagnozowanie inne problemy z wydajnością i](app-insights-detect-triage-diagnose.md). Usługi tej można używać z usługami Node.js hostowanymi w dowolnym miejscu: w centrum danych, na maszynach wirtualnych i aplikacjach Web Apps platformy Azure, a nawet w innych chmurach publicznych.

tooreceive, przechowywać i eksplorować dane monitorowania, wykonaj następujące instrukcje tooinclude agenta w kodzie hello i skonfiguruj odpowiadający jej zasób usługi Application Insights na platformie Azure. Witaj, agent wysyła zasobów toothat dane do dalszej analizy i eksploracja.

Hello Node.js agent można automatycznie monitorowanie przychodzących i wychodzących HTTP żądania, kilka miar systemu i wyjątki. Począwszy od wersji v0.20 agent może także monitorować niektóre popularne pakiety innych firm, takie jak `mongodb`, `mysql`, i `redis`. Wszystkie zdarzenia związane z skorelowanych tooan przychodzące żądanie HTTP do szybciej rozwiązywania problemów.

Można monitorować również inne aspekty aplikacji i systemu ręcznie instrumentując je za pomocą interfejsu API agent hello w dalszej części.

![Przykładowe wykresy monitorowania wydajności](./media/app-insights-nodejs/10-perf.png)

## <a name="getting-started"></a>Wprowadzenie

Rozważmy kroki konfigurowania na potrzeby aplikacji lub usługi.

### <a name="resource"></a> Konfigurowanie zasobu usługi App Insights

**Przed rozpoczęciem** upewnij się, że masz subskrypcję platformy Azure, lub [bezpłatnie uzyskaj nową][azure-free-offer]. Jeśli organizacja ma już subskrypcję platformy Azure, administrator może wykonać [tych instrukcji] [ add-aad-user] tooadd tooit użytkownik.

[azure-free-offer]: https://azure.microsoft.com/en-us/free/
[add-aad-user]: https://docs.microsoft.com/en-us/azure/active-directory/active-directory-users-create-azure-portal

Zaloguj się teraz toohello [portalu Azure] [ portal] i utworzyć zasobu usługi Application Insights w sposób przedstawiony poniżej hello — kliknij przycisk "Nowy" > "Developer tools" > "Usługi Application Insights". zasób Hello zawiera punktu końcowego w celu odbierania danych telemetrii, Magazyn danych, zapisane raporty i pulpity nawigacyjne, reguły i konfiguracji alertu i inne.

![Tworzenie zasobu usługi App Insights](./media/app-insights-nodejs/03-new_appinsights_resource.png)

Na stronie tworzenia zasobu hello wybierz polecenie "Aplikacji Node.js" z hello aplikacji typu listy rozwijanej. Typ aplikacji Hello określa hello domyślny zestaw pulpity nawigacyjne i raporty utworzone automatycznie. Nie należy się jednak martwić, ponieważ dowolny zasób usługi App Insights może w rzeczywistości zbierać dane dla dowolnego języka i platformy.

![Formularz nowego zasobu usługi App Insights](./media/app-insights-nodejs/04-create_appinsights_resource.png)

### <a name="agent"></a>Skonfiguruj agenta Node.js hello

Jest teraz czas tooinclude hello agenta w aplikacji, możliwe dalsze zbieranie danych.
Uruchom kopiowanie klucza Instrumentacji z zasobów (zwanej tooas Twojego `ikey`) z portalu hello, jak pokazano poniżej. Witaj App Insights system używa tego klucza toomap tooyour danych zasobów platformy Azure, więc należy toospecify w zmiennej środowiskowej lub kodu dla hello toouse agenta.  

![Kopiowanie klucza instrumentacji](./media/app-insights-nodejs/05-appinsights_ikey_portal.png)

Następnie dodaj hello Node.js agenta biblioteki tooyour zależnościach aplikacji za pomocą pliku package.json. Z folderu głównego hello aplikacji uruchom polecenie:

```bash
npm install applicationinsights --save
```

Teraz należy tooexplicitly obciążenia hello biblioteki w kodzie. Ponieważ hello agent injects Instrumentacji do innych bibliotek, należy załadować go jak najszybciej, nawet przed innymi `require` instrukcje. Rozpoczęto tooget, u góry hello pierwszego pliku js dodać:

```javascript
const appInsights = require("applicationinsights");
appInsights.setup("<instrumentation_key>");
appInsights.start();
```

Witaj `setup` metody konfiguruje klucza Instrumentacji hello (i w związku z tym zasobem platformy Azure) toobe używany domyślnie dla elementów wszystkie śledzone. Wywołanie `start` po konfiguracji toobegin Zakończono zbieranie i wysyłanie danych telemetrycznych.

Można też podać ikey za pomocą zmiennej środowiskowej hello APPINSIGHTS\_INSTRUMENTATIONKEY zamiast przekazaniem go ręcznie za `setup()` lub `getClient()`. Takie rozwiązanie pozwala zachować ikeys poza kodu źródłowego zatwierdzone i toospecify ikeys różne dla różnych środowisk.

Dodatkowe opcje konfiguracji opisano poniżej.

Możesz spróbować hello agenta bez wysyłania danych telemetrycznych przez ustawienie hello Instrumentacji klucza tooany niepustym ciągiem.

### <a name="monitor"></a> Monitorowanie aplikacji

Hello agent automatycznie zbiera dane telemetryczne dotyczące środowiska uruchomieniowego Node.js hello i niektóre typowe moduły innych firm. Korzystać z aplikacji teraz toogenerate niektóre z tych danych.

Następnie w hello [portalu Azure] [ portal] Przeglądaj toohello zasobu usługi Application Insights został utworzony wcześniej, i poszukaj pierwszego kilka punktów danych osi czasu omówienie hello, tak jak powitania po obrazu. Kliknij wykresy hello więcej szczegółów.

![Pierwsze punkty danych](./media/app-insights-nodejs/12-first-perf.png)

Kliknij przycisk hello aplikacji mapy przycisk tooview hello topologii odnalezionych dla aplikacji, tak jak powitania po obrazu. Kliknij przycisk za pośrednictwem składników w mapie hello więcej szczegółów.

![Mapa prostej aplikacji](./media/app-insights-nodejs/06-appinsights_appmap.png)

Dowiedz się więcej o aplikacji i rozwiązywanie problemów przy użyciu hello z innych widoków, które są dostępne w sekcji "Zbadaj" hello.

![Sekcja Zbadaj](./media/app-insights-nodejs/07-appinsights_investigate_blades.png)

#### <a name="no-data"></a>Brak danych?

Ponieważ hello agent partii danych do przesłania może wystąpić opóźnienie przed elementy są wyświetlane w portalu hello. Jeśli nie widzisz dane w zasobie wypróbować niektóre hello następujące poprawki:

* Użycie aplikacji hello niektóre więcej; zająć więcej toogenerate akcje więcej telemetrii.
* Kliknij przycisk **Odśwież** w widoku zasobów portalu hello. Wykresy automatycznego odświeżania się okresowo, ale odświeżanie wymusza to toohappen natychmiast.
* Upewnij się, że [potrzebne porty wychodzące](app-insights-ip-addresses.md) są otwarte.
* Otwórz hello [wyszukiwania](app-insights-diagnostic-search.md) kafelka i poszukaj poszczególnych zdarzeń.
* Sprawdź hello [— często zadawane pytania][].


## <a name="agent-configuration"></a>Konfiguracja agenta

Poniżej przedstawiono metody konfiguracji agenta hello i ich wartości domyślne.

toofully korelowanie zdarzeń w usłudze, należy się tooset `.setAutoDependencyCorrelation(true)`. Pozwala to agenta hello kontekstu tootrack między asynchronicznego wywołania zwrotne w środowisku Node.js.

```javascript
const appInsights = require("applicationinsights");
appInsights.setup("<instrumentation_key>")
    .setAutoDependencyCorrelation(false)
    .setAutoCollectRequests(true)
    .setAutoCollectPerformance(true)
    .setAutoCollectExceptions(true)
    .setAutoCollectDependencies(true)
    .start();
```

## <a name="agent-api"></a>Interfejs API agenta

<!-- TODO: Fully document agent API. -->

szczegółowo opisano Hello interfejsu API agent .NET [tutaj](app-insights-api-custom-events-metrics.md).

Można śledzić żądania, zdarzenia, metryki lub wyjątek przy użyciu powitania klienta aplikacji Node.js szczegółowych informacji. Witaj poniższy przykład przedstawia niektóre hello dostępnych interfejsach API.

```javascript
let appInsights = require("applicationinsights");
appInsights.setup().start(); // assuming ikey in env var
let client = appInsights.getClient();

client.trackEvent("my custom event", {customProperty: "custom property value"});
client.trackException(new Error("handled exceptions can be logged with this method"));
client.trackMetric("custom metric", 3);
client.trackTrace("trace message");

let http = require("http");
http.createServer( (req, res) => {
  client.trackRequest(req, res); // Place at hello beginning of your request handler
});
```

### <a name="track-your-dependencies"></a>Śledzenie zależności

```javascript
let appInsights = require("applicationinsights");
let client = appInsights.getClient();

var success = false;
let startTime = Date.now();
// execute dependency call here....
let duration = Date.now() - startTime;
success = true;

client.trackDependency("dependency name", "command name", duration, success);
```

### <a name="add-a-custom-property-tooall-events"></a>Dodawanie zdarzeń tooall właściwości niestandardowej

```javascript
appInsights.client.commonProperties = {
    environment: process.env.SOME_ENV_VARIABLE
};
```

### <a name="track-http-get-requests"></a>Śledzenie żądań HTTP GET

```javascript
var server = http.createServer((req, res) => {
    if ( req.method === "GET" ) {
            appInsights.client.trackRequest(req, res);
    }
    // other work here....
    res.end();
});
```

### <a name="track-server-startup-time"></a>Śledzenie czasu uruchamiania serwera

```javascript
let start = Date.now();
server.on("listening", () => {
    let duration = Date.now() - start;
    appInsights.client.trackMetric("server startup time", duration);
});
```

## <a name="more-resources"></a>Więcej zasobów

* [Monitorowanie telemetrii w portalu hello](app-insights-dashboards.md)
* [Zapisywanie zapytań analizy za pośrednictwem danych telemetrycznych](app-insights-analytics-tour.md)

<!--references-->

[portal]: https://portal.azure.com/
[— często zadawane pytania]: app-insights-troubleshoot-faq.md
