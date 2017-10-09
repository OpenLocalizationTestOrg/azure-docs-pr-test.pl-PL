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
# <a name="monitor-your-nodejs-services-and-apps-with-application-insights"></a><span data-ttu-id="e86f1-103">Monitorowanie usług i aplikacji Node.js za pomocą usługi Application Insights</span><span class="sxs-lookup"><span data-stu-id="e86f1-103">Monitor your Node.js services and apps with Application Insights</span></span>

<span data-ttu-id="e86f1-104">[Azure Application Insights](app-insights-overview.md) monitoruje usług zaplecza i składniki po ich wdrożeniu toohelp możesz [odnajdywania i szybkie diagnozowanie inne problemy z wydajnością i](app-insights-detect-triage-diagnose.md).</span><span class="sxs-lookup"><span data-stu-id="e86f1-104">[Azure Application Insights](app-insights-overview.md) monitors your backend services and components after you deploy them toohelp you [discover and rapidly diagnose performance and other issues](app-insights-detect-triage-diagnose.md).</span></span> <span data-ttu-id="e86f1-105">Usługi tej można używać z usługami Node.js hostowanymi w dowolnym miejscu: w centrum danych, na maszynach wirtualnych i aplikacjach Web Apps platformy Azure, a nawet w innych chmurach publicznych.</span><span class="sxs-lookup"><span data-stu-id="e86f1-105">Use it for Node.js services hosted anywhere: your datacenter, Azure VMs and Web Apps, and even other public clouds.</span></span>

<span data-ttu-id="e86f1-106">tooreceive, przechowywać i eksplorować dane monitorowania, wykonaj następujące instrukcje tooinclude agenta w kodzie hello i skonfiguruj odpowiadający jej zasób usługi Application Insights na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="e86f1-106">tooreceive, store, and explore your monitoring data, follow hello following instructions tooinclude an agent in your code and set up a corresponding Application Insights resource in Azure.</span></span> <span data-ttu-id="e86f1-107">Witaj, agent wysyła zasobów toothat dane do dalszej analizy i eksploracja.</span><span class="sxs-lookup"><span data-stu-id="e86f1-107">hello agent sends data toothat resource for further analysis and exploration.</span></span>

<span data-ttu-id="e86f1-108">Hello Node.js agent można automatycznie monitorowanie przychodzących i wychodzących HTTP żądania, kilka miar systemu i wyjątki.</span><span class="sxs-lookup"><span data-stu-id="e86f1-108">hello Node.js agent can automatically monitor incoming and outgoing HTTP requests, several system metrics, and exceptions.</span></span> <span data-ttu-id="e86f1-109">Począwszy od wersji v0.20 agent może także monitorować niektóre popularne pakiety innych firm, takie jak `mongodb`, `mysql`, i `redis`.</span><span class="sxs-lookup"><span data-stu-id="e86f1-109">Beginning in v0.20, it can also monitor some common third-party packages such as `mongodb`, `mysql`, and `redis`.</span></span> <span data-ttu-id="e86f1-110">Wszystkie zdarzenia związane z skorelowanych tooan przychodzące żądanie HTTP do szybciej rozwiązywania problemów.</span><span class="sxs-lookup"><span data-stu-id="e86f1-110">All events related tooan incoming HTTP request are correlated for faster troubleshooting.</span></span>

<span data-ttu-id="e86f1-111">Można monitorować również inne aspekty aplikacji i systemu ręcznie instrumentując je za pomocą interfejsu API agent hello w dalszej części.</span><span class="sxs-lookup"><span data-stu-id="e86f1-111">You can monitor more aspects of your app and system by manually instrumenting them using hello agent API described later.</span></span>

![Przykładowe wykresy monitorowania wydajności](./media/app-insights-nodejs/10-perf.png)

## <a name="getting-started"></a><span data-ttu-id="e86f1-113">Wprowadzenie</span><span class="sxs-lookup"><span data-stu-id="e86f1-113">Getting Started</span></span>

<span data-ttu-id="e86f1-114">Rozważmy kroki konfigurowania na potrzeby aplikacji lub usługi.</span><span class="sxs-lookup"><span data-stu-id="e86f1-114">Let's step through setting up monitoring for an app or service.</span></span>

### <span data-ttu-id="e86f1-115"><a name="resource"></a> Konfigurowanie zasobu usługi App Insights</span><span class="sxs-lookup"><span data-stu-id="e86f1-115"><a name="resource"></a> Set up an App Insights resource</span></span>

<span data-ttu-id="e86f1-116">**Przed rozpoczęciem** upewnij się, że masz subskrypcję platformy Azure, lub [bezpłatnie uzyskaj nową][azure-free-offer].</span><span class="sxs-lookup"><span data-stu-id="e86f1-116">**Before you start**, make sure you have an Azure subscription or [get a new one for free][azure-free-offer].</span></span> <span data-ttu-id="e86f1-117">Jeśli organizacja ma już subskrypcję platformy Azure, administrator może wykonać [tych instrukcji] [ add-aad-user] tooadd tooit użytkownik.</span><span class="sxs-lookup"><span data-stu-id="e86f1-117">If your organization already has an Azure subscription, an administrator can follow [these instructions][add-aad-user] tooadd you tooit.</span></span>

[azure-free-offer]: https://azure.microsoft.com/en-us/free/
[add-aad-user]: https://docs.microsoft.com/en-us/azure/active-directory/active-directory-users-create-azure-portal

<span data-ttu-id="e86f1-118">Zaloguj się teraz toohello [portalu Azure] [ portal] i utworzyć zasobu usługi Application Insights w sposób przedstawiony poniżej hello — kliknij przycisk "Nowy" > "Developer tools" > "Usługi Application Insights".</span><span class="sxs-lookup"><span data-stu-id="e86f1-118">Now log in toohello [Azure portal][portal] and create an Application Insights resource as illustrated in hello following - click "New" > "Developer tools" > "Application Insights".</span></span> <span data-ttu-id="e86f1-119">zasób Hello zawiera punktu końcowego w celu odbierania danych telemetrii, Magazyn danych, zapisane raporty i pulpity nawigacyjne, reguły i konfiguracji alertu i inne.</span><span class="sxs-lookup"><span data-stu-id="e86f1-119">hello resource includes an endpoint for receiving telemetry data, storage for this data, saved reports and dashboards, rule and alert configuration, and more.</span></span>

![Tworzenie zasobu usługi App Insights](./media/app-insights-nodejs/03-new_appinsights_resource.png)

<span data-ttu-id="e86f1-121">Na stronie tworzenia zasobu hello wybierz polecenie "Aplikacji Node.js" z hello aplikacji typu listy rozwijanej.</span><span class="sxs-lookup"><span data-stu-id="e86f1-121">On hello resource creation page, choose "Node.js Application" from hello application type drop-down.</span></span> <span data-ttu-id="e86f1-122">Typ aplikacji Hello określa hello domyślny zestaw pulpity nawigacyjne i raporty utworzone automatycznie.</span><span class="sxs-lookup"><span data-stu-id="e86f1-122">hello app type determines hello default set of dashboards and reports created for you.</span></span> <span data-ttu-id="e86f1-123">Nie należy się jednak martwić, ponieważ dowolny zasób usługi App Insights może w rzeczywistości zbierać dane dla dowolnego języka i platformy.</span><span class="sxs-lookup"><span data-stu-id="e86f1-123">Don't worry though, any App Insights resource can in fact collect data from any language and platform.</span></span>

![Formularz nowego zasobu usługi App Insights](./media/app-insights-nodejs/04-create_appinsights_resource.png)

### <span data-ttu-id="e86f1-125"><a name="agent"></a>Skonfiguruj agenta Node.js hello</span><span class="sxs-lookup"><span data-stu-id="e86f1-125"><a name="agent"></a> Set up hello Node.js agent</span></span>

<span data-ttu-id="e86f1-126">Jest teraz czas tooinclude hello agenta w aplikacji, możliwe dalsze zbieranie danych.</span><span class="sxs-lookup"><span data-stu-id="e86f1-126">Now it's time tooinclude hello agent in your app so it can gather data.</span></span>
<span data-ttu-id="e86f1-127">Uruchom kopiowanie klucza Instrumentacji z zasobów (zwanej tooas Twojego `ikey`) z portalu hello, jak pokazano poniżej.</span><span class="sxs-lookup"><span data-stu-id="e86f1-127">Start by copying your resource's Instrumentation Key (hereinafter referred tooas your `ikey`) from hello portal as shown below.</span></span> <span data-ttu-id="e86f1-128">Witaj App Insights system używa tego klucza toomap tooyour danych zasobów platformy Azure, więc należy toospecify w zmiennej środowiskowej lub kodu dla hello toouse agenta.</span><span class="sxs-lookup"><span data-stu-id="e86f1-128">hello App Insights system uses this key toomap data tooyour Azure resource so you need toospecify it in an environment variable or your code for hello agent toouse.</span></span>  

![Kopiowanie klucza instrumentacji](./media/app-insights-nodejs/05-appinsights_ikey_portal.png)

<span data-ttu-id="e86f1-130">Następnie dodaj hello Node.js agenta biblioteki tooyour zależnościach aplikacji za pomocą pliku package.json.</span><span class="sxs-lookup"><span data-stu-id="e86f1-130">Next, add hello Node.js agent library tooyour app's dependencies via package.json.</span></span> <span data-ttu-id="e86f1-131">Z folderu głównego hello aplikacji uruchom polecenie:</span><span class="sxs-lookup"><span data-stu-id="e86f1-131">From hello root folder of your app, run:</span></span>

```bash
npm install applicationinsights --save
```

<span data-ttu-id="e86f1-132">Teraz należy tooexplicitly obciążenia hello biblioteki w kodzie.</span><span class="sxs-lookup"><span data-stu-id="e86f1-132">Now you need tooexplicitly load hello library in your code.</span></span> <span data-ttu-id="e86f1-133">Ponieważ hello agent injects Instrumentacji do innych bibliotek, należy załadować go jak najszybciej, nawet przed innymi `require` instrukcje.</span><span class="sxs-lookup"><span data-stu-id="e86f1-133">Because hello agent injects instrumentation into many other libraries, you should load it as early as possible, even before other `require` statements.</span></span> <span data-ttu-id="e86f1-134">Rozpoczęto tooget, u góry hello pierwszego pliku js dodać:</span><span class="sxs-lookup"><span data-stu-id="e86f1-134">tooget started, at hello top of your first .js file add:</span></span>

```javascript
const appInsights = require("applicationinsights");
appInsights.setup("<instrumentation_key>");
appInsights.start();
```

<span data-ttu-id="e86f1-135">Witaj `setup` metody konfiguruje klucza Instrumentacji hello (i w związku z tym zasobem platformy Azure) toobe używany domyślnie dla elementów wszystkie śledzone.</span><span class="sxs-lookup"><span data-stu-id="e86f1-135">hello `setup` method configures hello instrumentation key (and thus Azure resource) toobe used by default for all tracked items.</span></span> <span data-ttu-id="e86f1-136">Wywołanie `start` po konfiguracji toobegin Zakończono zbieranie i wysyłanie danych telemetrycznych.</span><span class="sxs-lookup"><span data-stu-id="e86f1-136">Call `start` after configuration is finished toobegin gathering and sending telemetry data.</span></span>

<span data-ttu-id="e86f1-137">Można też podać ikey za pomocą zmiennej środowiskowej hello APPINSIGHTS\_INSTRUMENTATIONKEY zamiast przekazaniem go ręcznie za `setup()` lub `getClient()`.</span><span class="sxs-lookup"><span data-stu-id="e86f1-137">You can also provide an ikey via hello environment variable APPINSIGHTS\_INSTRUMENTATIONKEY instead of passing it manually too `setup()` or `getClient()`.</span></span> <span data-ttu-id="e86f1-138">Takie rozwiązanie pozwala zachować ikeys poza kodu źródłowego zatwierdzone i toospecify ikeys różne dla różnych środowisk.</span><span class="sxs-lookup"><span data-stu-id="e86f1-138">This practice lets you keep ikeys out of committed source code and toospecify different ikeys for different environments.</span></span>

<span data-ttu-id="e86f1-139">Dodatkowe opcje konfiguracji opisano poniżej.</span><span class="sxs-lookup"><span data-stu-id="e86f1-139">Additional configuration options are documented below.</span></span>

<span data-ttu-id="e86f1-140">Możesz spróbować hello agenta bez wysyłania danych telemetrycznych przez ustawienie hello Instrumentacji klucza tooany niepustym ciągiem.</span><span class="sxs-lookup"><span data-stu-id="e86f1-140">You can try hello agent without sending telemetry by setting hello instrumentation key tooany non-empty string.</span></span>

### <span data-ttu-id="e86f1-141"><a name="monitor"></a> Monitorowanie aplikacji</span><span class="sxs-lookup"><span data-stu-id="e86f1-141"><a name="monitor"></a> Monitor your app</span></span>

<span data-ttu-id="e86f1-142">Hello agent automatycznie zbiera dane telemetryczne dotyczące środowiska uruchomieniowego Node.js hello i niektóre typowe moduły innych firm.</span><span class="sxs-lookup"><span data-stu-id="e86f1-142">hello agent automatically gathers telemetry about hello Node.js runtime and some common third-party modules.</span></span> <span data-ttu-id="e86f1-143">Korzystać z aplikacji teraz toogenerate niektóre z tych danych.</span><span class="sxs-lookup"><span data-stu-id="e86f1-143">Use your application now toogenerate some of this data.</span></span>

<span data-ttu-id="e86f1-144">Następnie w hello [portalu Azure] [ portal] Przeglądaj toohello zasobu usługi Application Insights został utworzony wcześniej, i poszukaj pierwszego kilka punktów danych osi czasu omówienie hello, tak jak powitania po obrazu.</span><span class="sxs-lookup"><span data-stu-id="e86f1-144">Then, in hello [Azure portal][portal] browse toohello Application Insights resource you created earlier and look for your first few data points in hello Overview timeline, as in hello following image.</span></span> <span data-ttu-id="e86f1-145">Kliknij wykresy hello więcej szczegółów.</span><span class="sxs-lookup"><span data-stu-id="e86f1-145">Click through hello charts for more details.</span></span>

![Pierwsze punkty danych](./media/app-insights-nodejs/12-first-perf.png)

<span data-ttu-id="e86f1-147">Kliknij przycisk hello aplikacji mapy przycisk tooview hello topologii odnalezionych dla aplikacji, tak jak powitania po obrazu.</span><span class="sxs-lookup"><span data-stu-id="e86f1-147">Click hello Application map button tooview hello topology discovered for your app, as in hello following image.</span></span> <span data-ttu-id="e86f1-148">Kliknij przycisk za pośrednictwem składników w mapie hello więcej szczegółów.</span><span class="sxs-lookup"><span data-stu-id="e86f1-148">Click through components in hello map for more details.</span></span>

![Mapa prostej aplikacji](./media/app-insights-nodejs/06-appinsights_appmap.png)

<span data-ttu-id="e86f1-150">Dowiedz się więcej o aplikacji i rozwiązywanie problemów przy użyciu hello z innych widoków, które są dostępne w sekcji "Zbadaj" hello.</span><span class="sxs-lookup"><span data-stu-id="e86f1-150">Learn more about your app and troubleshoot problems using hello other views available under hello "Investigate" section.</span></span>

![Sekcja Zbadaj](./media/app-insights-nodejs/07-appinsights_investigate_blades.png)

#### <a name="no-data"></a><span data-ttu-id="e86f1-152">Brak danych?</span><span class="sxs-lookup"><span data-stu-id="e86f1-152">No data?</span></span>

<span data-ttu-id="e86f1-153">Ponieważ hello agent partii danych do przesłania może wystąpić opóźnienie przed elementy są wyświetlane w portalu hello.</span><span class="sxs-lookup"><span data-stu-id="e86f1-153">Because hello agent batches data for submission there may be a delay before items are displayed in hello portal.</span></span> <span data-ttu-id="e86f1-154">Jeśli nie widzisz dane w zasobie wypróbować niektóre hello następujące poprawki:</span><span class="sxs-lookup"><span data-stu-id="e86f1-154">If you don't see data in your resource try some of hello following fixes:</span></span>

* <span data-ttu-id="e86f1-155">Użycie aplikacji hello niektóre więcej; zająć więcej toogenerate akcje więcej telemetrii.</span><span class="sxs-lookup"><span data-stu-id="e86f1-155">Use hello application some more; take more actions toogenerate more telemetry.</span></span>
* <span data-ttu-id="e86f1-156">Kliknij przycisk **Odśwież** w widoku zasobów portalu hello.</span><span class="sxs-lookup"><span data-stu-id="e86f1-156">Click **Refresh** in hello portal resource view.</span></span> <span data-ttu-id="e86f1-157">Wykresy automatycznego odświeżania się okresowo, ale odświeżanie wymusza to toohappen natychmiast.</span><span class="sxs-lookup"><span data-stu-id="e86f1-157">Charts automatically refresh themselves periodically but refreshing forces this toohappen immediately.</span></span>
* <span data-ttu-id="e86f1-158">Upewnij się, że [potrzebne porty wychodzące](app-insights-ip-addresses.md) są otwarte.</span><span class="sxs-lookup"><span data-stu-id="e86f1-158">Verify that [needed outgoing ports](app-insights-ip-addresses.md) are open.</span></span>
* <span data-ttu-id="e86f1-159">Otwórz hello [wyszukiwania](app-insights-diagnostic-search.md) kafelka i poszukaj poszczególnych zdarzeń.</span><span class="sxs-lookup"><span data-stu-id="e86f1-159">Open hello [Search](app-insights-diagnostic-search.md) tile and look for individual events.</span></span>
* <span data-ttu-id="e86f1-160">Sprawdź hello [— często zadawane pytania][].</span><span class="sxs-lookup"><span data-stu-id="e86f1-160">Check hello [FAQ][].</span></span>


## <a name="agent-configuration"></a><span data-ttu-id="e86f1-161">Konfiguracja agenta</span><span class="sxs-lookup"><span data-stu-id="e86f1-161">Agent Configuration</span></span>

<span data-ttu-id="e86f1-162">Poniżej przedstawiono metody konfiguracji agenta hello i ich wartości domyślne.</span><span class="sxs-lookup"><span data-stu-id="e86f1-162">Following are hello agent's configuration methods and their default values.</span></span>

<span data-ttu-id="e86f1-163">toofully korelowanie zdarzeń w usłudze, należy się tooset `.setAutoDependencyCorrelation(true)`.</span><span class="sxs-lookup"><span data-stu-id="e86f1-163">toofully correlate events in a service, be sure tooset `.setAutoDependencyCorrelation(true)`.</span></span> <span data-ttu-id="e86f1-164">Pozwala to agenta hello kontekstu tootrack między asynchronicznego wywołania zwrotne w środowisku Node.js.</span><span class="sxs-lookup"><span data-stu-id="e86f1-164">This allows hello agent tootrack context across asynchronous callbacks in Node.js.</span></span>

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

## <a name="agent-api"></a><span data-ttu-id="e86f1-165">Interfejs API agenta</span><span class="sxs-lookup"><span data-stu-id="e86f1-165">Agent API</span></span>

<!-- TODO: Fully document agent API. -->

<span data-ttu-id="e86f1-166">szczegółowo opisano Hello interfejsu API agent .NET [tutaj](app-insights-api-custom-events-metrics.md).</span><span class="sxs-lookup"><span data-stu-id="e86f1-166">hello .NET agent API is fully described [here](app-insights-api-custom-events-metrics.md).</span></span>

<span data-ttu-id="e86f1-167">Można śledzić żądania, zdarzenia, metryki lub wyjątek przy użyciu powitania klienta aplikacji Node.js szczegółowych informacji.</span><span class="sxs-lookup"><span data-stu-id="e86f1-167">You can track any request, event, metric, or exception using hello Application Insights Node.js client.</span></span> <span data-ttu-id="e86f1-168">Witaj poniższy przykład przedstawia niektóre hello dostępnych interfejsach API.</span><span class="sxs-lookup"><span data-stu-id="e86f1-168">hello following example demonstrates some of hello available APIs.</span></span>

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

### <a name="track-your-dependencies"></a><span data-ttu-id="e86f1-169">Śledzenie zależności</span><span class="sxs-lookup"><span data-stu-id="e86f1-169">Track your dependencies</span></span>

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

### <a name="add-a-custom-property-tooall-events"></a><span data-ttu-id="e86f1-170">Dodawanie zdarzeń tooall właściwości niestandardowej</span><span class="sxs-lookup"><span data-stu-id="e86f1-170">Add a custom property tooall events</span></span>

```javascript
appInsights.client.commonProperties = {
    environment: process.env.SOME_ENV_VARIABLE
};
```

### <a name="track-http-get-requests"></a><span data-ttu-id="e86f1-171">Śledzenie żądań HTTP GET</span><span class="sxs-lookup"><span data-stu-id="e86f1-171">Track HTTP GET requests</span></span>

```javascript
var server = http.createServer((req, res) => {
    if ( req.method === "GET" ) {
            appInsights.client.trackRequest(req, res);
    }
    // other work here....
    res.end();
});
```

### <a name="track-server-startup-time"></a><span data-ttu-id="e86f1-172">Śledzenie czasu uruchamiania serwera</span><span class="sxs-lookup"><span data-stu-id="e86f1-172">Track server startup time</span></span>

```javascript
let start = Date.now();
server.on("listening", () => {
    let duration = Date.now() - start;
    appInsights.client.trackMetric("server startup time", duration);
});
```

## <a name="more-resources"></a><span data-ttu-id="e86f1-173">Więcej zasobów</span><span class="sxs-lookup"><span data-stu-id="e86f1-173">More resources</span></span>

* [<span data-ttu-id="e86f1-174">Monitorowanie telemetrii w portalu hello</span><span class="sxs-lookup"><span data-stu-id="e86f1-174">Monitor your telemetry in hello portal</span></span>](app-insights-dashboards.md)
* [<span data-ttu-id="e86f1-175">Zapisywanie zapytań analizy za pośrednictwem danych telemetrycznych</span><span class="sxs-lookup"><span data-stu-id="e86f1-175">Write Analytics queries over your telemetry</span></span>](app-insights-analytics-tour.md)

<!--references-->

[portal]: https://portal.azure.com/
[— często zadawane pytania]: app-insights-troubleshoot-faq.md
