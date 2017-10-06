---
title: "aaaApplication szczegółowych informacji dla języka Java sieci web aplikacji, które znajdują się już na żywo"
description: "Rozpocznij monitorowanie aplikacji sieci web, która jest już uruchomiona na serwerze"
services: application-insights
documentationcenter: java
author: harelbr
manager: carmonm
ms.assetid: 12f3dbb9-915f-4087-87c9-807286030b0b
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 11/10/2016
ms.author: bwren
ms.openlocfilehash: 2b01cd61657522ccf1d2d97b2a29cdeb08ec9a18
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="application-insights-for-java-web-apps-that-are-already-live"></a><span data-ttu-id="ba8bd-103">Application Insights dla aplikacji sieci web Java, które znajdują się już na żywo</span><span class="sxs-lookup"><span data-stu-id="ba8bd-103">Application Insights for Java web apps that are already live</span></span>


<span data-ttu-id="ba8bd-104">Jeśli aplikacja sieci web, która jest już uruchomiona na serwerze J2EE, można rozpocząć monitorowanie za pomocą [usługi Application Insights](app-insights-overview.md) bez hello toomake kodu zmiany lub ponownie skompilować projekt.</span><span class="sxs-lookup"><span data-stu-id="ba8bd-104">If you have a web application that is already running on your J2EE server, you can start monitoring it with [Application Insights](app-insights-overview.md) without hello need toomake code changes or recompile your project.</span></span> <span data-ttu-id="ba8bd-105">Po wybraniu tej opcji możesz uzyskać informacje o żądaniach HTTP wysyłane tooyour serwera, nieobsługiwanych wyjątków i liczniki wydajności.</span><span class="sxs-lookup"><span data-stu-id="ba8bd-105">With this option, you get information about HTTP requests sent tooyour server, unhandled exceptions, and performance counters.</span></span>

<span data-ttu-id="ba8bd-106">Będziesz potrzebować subskrypcji zbyt[Microsoft Azure](https://azure.com).</span><span class="sxs-lookup"><span data-stu-id="ba8bd-106">You'll need a subscription too[Microsoft Azure](https://azure.com).</span></span>

> [!NOTE]
> <span data-ttu-id="ba8bd-107">procedury Hello na tej stronie dodaje aplikacji sieci web tooyour SDK hello w czasie wykonywania.</span><span class="sxs-lookup"><span data-stu-id="ba8bd-107">hello procedure on this page adds hello SDK tooyour web app at runtime.</span></span> <span data-ttu-id="ba8bd-108">Tego środowiska uruchomieniowego Instrumentacji jest przydatne, jeśli nie chcesz tooupdate lub Odbuduj kodu źródłowego.</span><span class="sxs-lookup"><span data-stu-id="ba8bd-108">This runtime instrumentation is useful if you don't want tooupdate or rebuild your source code.</span></span> <span data-ttu-id="ba8bd-109">Ale jeśli to możliwe, zalecamy [Dodaj kod źródłowy toohello SDK hello](app-insights-java-get-started.md) zamiast tego.</span><span class="sxs-lookup"><span data-stu-id="ba8bd-109">But if you can, we recommend you [add hello SDK toohello source code](app-insights-java-get-started.md) instead.</span></span> <span data-ttu-id="ba8bd-110">Która zapewnia dodatkowe opcje, takie jak zapisywanie aktywności użytkownika tootrack kodu.</span><span class="sxs-lookup"><span data-stu-id="ba8bd-110">That gives you more options such as writing code tootrack user activity.</span></span>
> 
> 

## <a name="1-get-an-application-insights-instrumentation-key"></a><span data-ttu-id="ba8bd-111">1. Uzyskiwanie klucza instrumentacji usługi Application Insights</span><span class="sxs-lookup"><span data-stu-id="ba8bd-111">1. Get an Application Insights instrumentation key</span></span>
1. <span data-ttu-id="ba8bd-112">Zaloguj się toohello [portalu Microsoft Azure](https://portal.azure.com)</span><span class="sxs-lookup"><span data-stu-id="ba8bd-112">Sign in toohello [Microsoft Azure portal](https://portal.azure.com)</span></span>
2. <span data-ttu-id="ba8bd-113">Utwórz nowy zasób usługi Application Insights i ustaw aplikacji sieci web tooJava typu aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="ba8bd-113">Create a new Application Insights resource and set hello application type tooJava web application.</span></span>
   
    ![Wypełnij nazwę, wybierz aplikację sieci Web Java i kliknij przycisk Utwórz](./media/app-insights-java-live/02-create.png)

    <span data-ttu-id="ba8bd-115">Witaj zasób został utworzony w ciągu kilku sekund.</span><span class="sxs-lookup"><span data-stu-id="ba8bd-115">hello resource is created in a few seconds.</span></span>

4. <span data-ttu-id="ba8bd-116">Otwórz nowy zasób hello i uzyskać jego klucza instrumentacji.</span><span class="sxs-lookup"><span data-stu-id="ba8bd-116">Open hello new resource and get its instrumentation key.</span></span> <span data-ttu-id="ba8bd-117">Należy toopaste tego klucza w projekcie kodu wkrótce.</span><span class="sxs-lookup"><span data-stu-id="ba8bd-117">You'll need toopaste this key into your code project shortly.</span></span>
   
    ![W obszarze Przegląd nowych zasobów powitania kliknij polecenie Właściwości i skopiuj hello klucza Instrumentacji](./media/app-insights-java-live/03-key.png)

## <a name="2-download-hello-sdk"></a><span data-ttu-id="ba8bd-119">2. Pobierz hello zestawu SDK</span><span class="sxs-lookup"><span data-stu-id="ba8bd-119">2. Download hello SDK</span></span>
1. <span data-ttu-id="ba8bd-120">Pobierz hello [zestaw SDK usługi Application Insights dla języka Java](https://aka.ms/aijavasdk).</span><span class="sxs-lookup"><span data-stu-id="ba8bd-120">Download hello [Application Insights SDK for Java](https://aka.ms/aijavasdk).</span></span> 
2. <span data-ttu-id="ba8bd-121">Na serwerze Wyodrębnij hello SDK zawartość toohello katalogu z którego są załadowane dane binarne Twojego projektu.</span><span class="sxs-lookup"><span data-stu-id="ba8bd-121">On your server, extract hello SDK contents toohello directory from which your project binaries are loaded.</span></span> <span data-ttu-id="ba8bd-122">Jeśli używasz Tomcat ten katalog będzie zazwyczaj w obszarze`webapps/<your_app_name>/WEB-INF/lib`</span><span class="sxs-lookup"><span data-stu-id="ba8bd-122">If you’re using Tomcat, this directory would typically be under `webapps/<your_app_name>/WEB-INF/lib`</span></span>

<span data-ttu-id="ba8bd-123">Należy pamiętać, że toorepeat to konieczne w każdym wystąpieniu serwera i dla każdej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="ba8bd-123">Note that you need toorepeat this on each server instance, and for each app.</span></span>

## <a name="3-add-an-application-insights-xml-file"></a><span data-ttu-id="ba8bd-124">3. Dodaj plik xml usługi Application Insights</span><span class="sxs-lookup"><span data-stu-id="ba8bd-124">3. Add an Application Insights xml file</span></span>
<span data-ttu-id="ba8bd-125">Utwórz ApplicationInsights.xml w folderze hello, w którym dodano hello zestawu SDK.</span><span class="sxs-lookup"><span data-stu-id="ba8bd-125">Create ApplicationInsights.xml in hello folder in which you added hello SDK.</span></span> <span data-ttu-id="ba8bd-126">Umieść w nim hello następujących XML.</span><span class="sxs-lookup"><span data-stu-id="ba8bd-126">Put into it hello following XML.</span></span>

<span data-ttu-id="ba8bd-127">Zastąp klucza Instrumentacji hello pochodzący z hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="ba8bd-127">Substitute hello instrumentation key that you got from hello Azure portal.</span></span>

```XML

    <?xml version="1.0" encoding="utf-8"?>
    <ApplicationInsights xmlns="http://schemas.microsoft.com/ApplicationInsights/2013/Settings" schemaVersion="2014-05-30">


      <!-- hello key from hello portal: -->

      <InstrumentationKey>** Your instrumentation key **</InstrumentationKey>


      <!-- HTTP request component (not required for bare API) -->

      <TelemetryModules>
        <Add type="com.microsoft.applicationinsights.web.extensibility.modules.WebRequestTrackingTelemetryModule"/>
        <Add type="com.microsoft.applicationinsights.web.extensibility.modules.WebSessionTrackingTelemetryModule"/>
        <Add type="com.microsoft.applicationinsights.web.extensibility.modules.WebUserTrackingTelemetryModule"/>
      </TelemetryModules>

      <!-- Events correlation (not required for bare API) -->
      <!-- These initializers add context data tooeach event -->

      <TelemetryInitializers>
        <Add   type="com.microsoft.applicationinsights.web.extensibility.initializers.WebOperationIdTelemetryInitializer"/>
        <Add type="com.microsoft.applicationinsights.web.extensibility.initializers.WebOperationNameTelemetryInitializer"/>
        <Add type="com.microsoft.applicationinsights.web.extensibility.initializers.WebSessionTelemetryInitializer"/>
        <Add type="com.microsoft.applicationinsights.web.extensibility.initializers.WebUserTelemetryInitializer"/>
        <Add type="com.microsoft.applicationinsights.web.extensibility.initializers.WebUserAgentTelemetryInitializer"/>

      </TelemetryInitializers>
    </ApplicationInsights>
```

* <span data-ttu-id="ba8bd-128">klucz Instrumentacji Hello przesyłany wraz każdy element telemetrii i informuje toodisplay usługi Application Insights w zasobie.</span><span class="sxs-lookup"><span data-stu-id="ba8bd-128">hello instrumentation key is sent along with every item of telemetry and tells Application Insights toodisplay it in your resource.</span></span>
* <span data-ttu-id="ba8bd-129">Witaj składnika żądania HTTP jest opcjonalna.</span><span class="sxs-lookup"><span data-stu-id="ba8bd-129">hello HTTP Request component is optional.</span></span> <span data-ttu-id="ba8bd-130">Automatycznie wysyła dane telemetryczne dotyczące żądań i odpowiedzi razy toohello portalu.</span><span class="sxs-lookup"><span data-stu-id="ba8bd-130">It automatically sends telemetry about requests and response times toohello portal.</span></span>
* <span data-ttu-id="ba8bd-131">Korelacji zdarzeń to składnik dodawania toohello HTTP żądania.</span><span class="sxs-lookup"><span data-stu-id="ba8bd-131">Events correlation is an addition toohello HTTP request component.</span></span> <span data-ttu-id="ba8bd-132">Przypisuje identyfikator żądania tooeach odebranych przez serwer hello i dodaje ten identyfikator jako elementu właściwości tooevery dane telemetryczne jako właściwość hello "Operation.Id".</span><span class="sxs-lookup"><span data-stu-id="ba8bd-132">It assigns an identifier tooeach request received by hello server, and adds this identifier as a property tooevery item of telemetry as hello property 'Operation.Id'.</span></span> <span data-ttu-id="ba8bd-133">Umożliwia telemetrii hello toocorrelate skojarzone z każdym żądaniem przez ustawienie filtru [diagnostycznych wyszukiwania](app-insights-diagnostic-search.md).</span><span class="sxs-lookup"><span data-stu-id="ba8bd-133">It allows you toocorrelate hello telemetry associated with each request by setting a filter in [diagnostic search](app-insights-diagnostic-search.md).</span></span>

## <a name="4-add-an-http-filter"></a><span data-ttu-id="ba8bd-134">4. Dodawanie filtru HTTP</span><span class="sxs-lookup"><span data-stu-id="ba8bd-134">4. Add an HTTP filter</span></span>
<span data-ttu-id="ba8bd-135">Zlokalizuj i Otwórz plik web.xml hello w projekcie i po fragment kodu w węźle hello aplikacji sieci web, z której skonfigurowano filtry aplikacji hello scalania.</span><span class="sxs-lookup"><span data-stu-id="ba8bd-135">Locate and open hello web.xml file in your project, and merge hello following snippet of code under hello web-app node, where your application filters are configured.</span></span>

<span data-ttu-id="ba8bd-136">tooget hello najdokładniejszych wyników, filtr hello należy mapować przed wszystkie inne filtry.</span><span class="sxs-lookup"><span data-stu-id="ba8bd-136">tooget hello most accurate results, hello filter should be mapped before all other filters.</span></span>

```XML

    <filter>
      <filter-name>ApplicationInsightsWebFilter</filter-name>
      <filter-class>
        com.microsoft.applicationinsights.web.internal.WebRequestTrackingFilter
      </filter-class>
    </filter>
    <filter-mapping>
       <filter-name>ApplicationInsightsWebFilter</filter-name>
       <url-pattern>/*</url-pattern>
    </filter-mapping>
```

## <a name="5-check-firewall-exceptions"></a><span data-ttu-id="ba8bd-137">5. Sprawdź wyjątki zapory</span><span class="sxs-lookup"><span data-stu-id="ba8bd-137">5. Check firewall exceptions</span></span>
<span data-ttu-id="ba8bd-138">Może być konieczne zbyt[ustawić wyjątki, danych wychodzących toosend](app-insights-ip-addresses.md).</span><span class="sxs-lookup"><span data-stu-id="ba8bd-138">You might need too[set exceptions toosend outgoing data](app-insights-ip-addresses.md).</span></span>

## <a name="6-restart-your-web-app"></a><span data-ttu-id="ba8bd-139">6. Uruchom ponownie aplikację sieci web</span><span class="sxs-lookup"><span data-stu-id="ba8bd-139">6. Restart your web app</span></span>
## <a name="7-view-your-telemetry-in-application-insights"></a><span data-ttu-id="ba8bd-140">7. Wyświetlanie telemetrii w usłudze Application Insights</span><span class="sxs-lookup"><span data-stu-id="ba8bd-140">7. View your telemetry in Application Insights</span></span>
<span data-ttu-id="ba8bd-141">Zwraca tooyour zasobu usługi Application Insights w [portalu Microsoft Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="ba8bd-141">Return tooyour Application Insights resource in [Microsoft Azure portal](https://portal.azure.com).</span></span>

<span data-ttu-id="ba8bd-142">Dane telemetryczne dotyczące żądań HTTP jest wyświetlane na powitania omówienie bloku.</span><span class="sxs-lookup"><span data-stu-id="ba8bd-142">Telemetry about HTTP requests appears on hello overview blade.</span></span> <span data-ttu-id="ba8bd-143">(Jeśli ich tam nie ma, odczekaj kilka sekund, a następnie kliknij przycisk Odśwież).</span><span class="sxs-lookup"><span data-stu-id="ba8bd-143">(If it isn't there, wait a few seconds and then click Refresh.)</span></span>

![dane przykładowe](./media/app-insights-java-live/5-results.png)

<span data-ttu-id="ba8bd-145">Kliknij przycisk za pomocą dowolnego toosee wykresu bardziej szczegółowe metryki.</span><span class="sxs-lookup"><span data-stu-id="ba8bd-145">Click through any chart toosee more detailed metrics.</span></span> 

![](./media/app-insights-java-live/6-barchart.png)

<span data-ttu-id="ba8bd-146">Podczas przeglądania właściwości hello żądania, może uzyskać zdarzenia telemetrii hello skojarzonych z nim, takich jak żądania i wyjątków i.</span><span class="sxs-lookup"><span data-stu-id="ba8bd-146">And when viewing hello properties of a request, you can see hello telemetry events associated with it such as requests and exceptions.</span></span>

![](./media/app-insights-java-live/7-instance.png)

[<span data-ttu-id="ba8bd-147">Dowiedz się więcej o metrykach.</span><span class="sxs-lookup"><span data-stu-id="ba8bd-147">Learn more about metrics.</span></span>](app-insights-metrics-explorer.md)

## <a name="next-steps"></a><span data-ttu-id="ba8bd-148">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="ba8bd-148">Next steps</span></span>
* <span data-ttu-id="ba8bd-149">[Dodawanie stron sieci web tooyour telemetrii](app-insights-javascript.md) toomonitor strony widoki i metryki użytkownika.</span><span class="sxs-lookup"><span data-stu-id="ba8bd-149">[Add telemetry tooyour web pages](app-insights-javascript.md) toomonitor page views and user metrics.</span></span>
* <span data-ttu-id="ba8bd-150">[Ustawianie testów sieci web](app-insights-monitor-web-app-availability.md) toomake się, że aplikacja pozostaje na żywo i szybko reagowały.</span><span class="sxs-lookup"><span data-stu-id="ba8bd-150">[Set up web tests](app-insights-monitor-web-app-availability.md) toomake sure your application stays live and responsive.</span></span>
* [<span data-ttu-id="ba8bd-151">Śledzenie dziennika</span><span class="sxs-lookup"><span data-stu-id="ba8bd-151">Capture log traces</span></span>](app-insights-java-trace-logs.md)
* <span data-ttu-id="ba8bd-152">[Wyszukiwanie zdarzeń i dzienniki](app-insights-diagnostic-search.md) toohelp diagnozowania problemów.</span><span class="sxs-lookup"><span data-stu-id="ba8bd-152">[Search events and logs](app-insights-diagnostic-search.md) toohelp diagnose problems.</span></span>

