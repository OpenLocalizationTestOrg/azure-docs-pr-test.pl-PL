---
title: "Application Insights dla aplikacji sieci web Java, które znajdują się już na żywo"
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
ms.openlocfilehash: a2731e3e44f8f3d104d8abc7dbe71fe3a4c3a690
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/18/2017
---
# <a name="application-insights-for-java-web-apps-that-are-already-live"></a><span data-ttu-id="f0616-103">Application Insights dla aplikacji sieci web Java, które znajdują się już na żywo</span><span class="sxs-lookup"><span data-stu-id="f0616-103">Application Insights for Java web apps that are already live</span></span>


<span data-ttu-id="f0616-104">Jeśli aplikacja sieci web, która jest już uruchomiona na serwerze J2EE, można rozpocząć monitorowanie za pomocą [usługi Application Insights](app-insights-overview.md) bez konieczności zmiany kodu lub ponownie skompilować projekt.</span><span class="sxs-lookup"><span data-stu-id="f0616-104">If you have a web application that is already running on your J2EE server, you can start monitoring it with [Application Insights](app-insights-overview.md) without the need to make code changes or recompile your project.</span></span> <span data-ttu-id="f0616-105">Po wybraniu tej opcji możesz uzyskać informacje o żądaniach HTTP wysyłane do serwera, nieobsługiwanych wyjątków i liczniki wydajności.</span><span class="sxs-lookup"><span data-stu-id="f0616-105">With this option, you get information about HTTP requests sent to your server, unhandled exceptions, and performance counters.</span></span>

<span data-ttu-id="f0616-106">Potrzebna będzie subskrypcja platformy [Microsoft Azure](https://azure.com).</span><span class="sxs-lookup"><span data-stu-id="f0616-106">You'll need a subscription to [Microsoft Azure](https://azure.com).</span></span>

> [!NOTE]
> <span data-ttu-id="f0616-107">Procedury na tej stronie dodaje zestaw SDK do aplikacji sieci web w czasie wykonywania.</span><span class="sxs-lookup"><span data-stu-id="f0616-107">The procedure on this page adds the SDK to your web app at runtime.</span></span> <span data-ttu-id="f0616-108">Instrumentacja to środowisko uruchomieniowe jest przydatne, jeśli nie chcesz zaktualizować lub ponownie skompiluj kod źródłowy.</span><span class="sxs-lookup"><span data-stu-id="f0616-108">This runtime instrumentation is useful if you don't want to update or rebuild your source code.</span></span> <span data-ttu-id="f0616-109">Ale jeśli to możliwe, zalecamy [Dodaj zestaw SDK do kodu źródłowego](app-insights-java-get-started.md) zamiast tego.</span><span class="sxs-lookup"><span data-stu-id="f0616-109">But if you can, we recommend you [add the SDK to the source code](app-insights-java-get-started.md) instead.</span></span> <span data-ttu-id="f0616-110">Zapewniającą więcej opcji przykład pisania kodu, aby śledzić aktywność użytkownika.</span><span class="sxs-lookup"><span data-stu-id="f0616-110">That gives you more options such as writing code to track user activity.</span></span>
> 
> 

## <a name="1-get-an-application-insights-instrumentation-key"></a><span data-ttu-id="f0616-111">1. Uzyskiwanie klucza instrumentacji usługi Application Insights</span><span class="sxs-lookup"><span data-stu-id="f0616-111">1. Get an Application Insights instrumentation key</span></span>
1. <span data-ttu-id="f0616-112">Zaloguj się do [portalu Microsoft Azure](https://portal.azure.com)</span><span class="sxs-lookup"><span data-stu-id="f0616-112">Sign in to the [Microsoft Azure portal](https://portal.azure.com)</span></span>
2. <span data-ttu-id="f0616-113">Utwórz nowy zasób usługi Application Insights i Ustaw typ aplikacji do aplikacji sieci web Java.</span><span class="sxs-lookup"><span data-stu-id="f0616-113">Create a new Application Insights resource and set the application type to Java web application.</span></span>
   
    ![Wypełnij nazwę, wybierz aplikację sieci Web Java i kliknij przycisk Utwórz](./media/app-insights-java-live/02-create.png)

    <span data-ttu-id="f0616-115">Zasób jest tworzony w ciągu kilku sekund.</span><span class="sxs-lookup"><span data-stu-id="f0616-115">The resource is created in a few seconds.</span></span>

4. <span data-ttu-id="f0616-116">Otwórz nowy zasób i uzyskać jego klucza instrumentacji.</span><span class="sxs-lookup"><span data-stu-id="f0616-116">Open the new resource and get its instrumentation key.</span></span> <span data-ttu-id="f0616-117">Wkrótce będzie trzeba wkleić ten klucz do projektu kodu.</span><span class="sxs-lookup"><span data-stu-id="f0616-117">You'll need to paste this key into your code project shortly.</span></span>
   
    ![W opisie nowego zasobu kliknij opcję Właściwości i skopiuj klucz instrumentacji](./media/app-insights-java-live/03-key.png)

## <a name="2-download-the-sdk"></a><span data-ttu-id="f0616-119">2. Pobierz zestaw SDK</span><span class="sxs-lookup"><span data-stu-id="f0616-119">2. Download the SDK</span></span>
1. <span data-ttu-id="f0616-120">Pobierz [Zestaw SDK usługi Application Insights dla środowiska Java](https://aka.ms/aijavasdk).</span><span class="sxs-lookup"><span data-stu-id="f0616-120">Download the [Application Insights SDK for Java](https://aka.ms/aijavasdk).</span></span> 
2. <span data-ttu-id="f0616-121">Na serwerze Wyodrębnij zawartość zestawu SDK do katalogu, z którego są załadowane dane binarne Twojego projektu.</span><span class="sxs-lookup"><span data-stu-id="f0616-121">On your server, extract the SDK contents to the directory from which your project binaries are loaded.</span></span> <span data-ttu-id="f0616-122">Jeśli używasz Tomcat ten katalog będzie zazwyczaj w obszarze`webapps/<your_app_name>/WEB-INF/lib`</span><span class="sxs-lookup"><span data-stu-id="f0616-122">If you’re using Tomcat, this directory would typically be under `webapps/<your_app_name>/WEB-INF/lib`</span></span>

<span data-ttu-id="f0616-123">Należy pamiętać, że trzeba Powtórz te czynności dla każdego wystąpienia serwera, a także dla każdej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="f0616-123">Note that you need to repeat this on each server instance, and for each app.</span></span>

## <a name="3-add-an-application-insights-xml-file"></a><span data-ttu-id="f0616-124">3. Dodaj plik xml usługi Application Insights</span><span class="sxs-lookup"><span data-stu-id="f0616-124">3. Add an Application Insights xml file</span></span>
<span data-ttu-id="f0616-125">Utwórz ApplicationInsights.xml w folderze, w którym dodano zestawu SDK.</span><span class="sxs-lookup"><span data-stu-id="f0616-125">Create ApplicationInsights.xml in the folder in which you added the SDK.</span></span> <span data-ttu-id="f0616-126">Umieść w nim następujące XML.</span><span class="sxs-lookup"><span data-stu-id="f0616-126">Put into it the following XML.</span></span>

<span data-ttu-id="f0616-127">Zastąp klucz instrumentacji kluczem pobranym z portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="f0616-127">Substitute the instrumentation key that you got from the Azure portal.</span></span>

```XML

    <?xml version="1.0" encoding="utf-8"?>
    <ApplicationInsights xmlns="http://schemas.microsoft.com/ApplicationInsights/2013/Settings" schemaVersion="2014-05-30">


      <!-- The key from the portal: -->

      <InstrumentationKey>** Your instrumentation key **</InstrumentationKey>


      <!-- HTTP request component (not required for bare API) -->

      <TelemetryModules>
        <Add type="com.microsoft.applicationinsights.web.extensibility.modules.WebRequestTrackingTelemetryModule"/>
        <Add type="com.microsoft.applicationinsights.web.extensibility.modules.WebSessionTrackingTelemetryModule"/>
        <Add type="com.microsoft.applicationinsights.web.extensibility.modules.WebUserTrackingTelemetryModule"/>
      </TelemetryModules>

      <!-- Events correlation (not required for bare API) -->
      <!-- These initializers add context data to each event -->

      <TelemetryInitializers>
        <Add   type="com.microsoft.applicationinsights.web.extensibility.initializers.WebOperationIdTelemetryInitializer"/>
        <Add type="com.microsoft.applicationinsights.web.extensibility.initializers.WebOperationNameTelemetryInitializer"/>
        <Add type="com.microsoft.applicationinsights.web.extensibility.initializers.WebSessionTelemetryInitializer"/>
        <Add type="com.microsoft.applicationinsights.web.extensibility.initializers.WebUserTelemetryInitializer"/>
        <Add type="com.microsoft.applicationinsights.web.extensibility.initializers.WebUserAgentTelemetryInitializer"/>

      </TelemetryInitializers>
    </ApplicationInsights>
```

* <span data-ttu-id="f0616-128">Klucz instrumentacji jest wysyłany wraz z każdym elementem telemetrii i dzięki temu te elementy mogą być wyświetlane dla odpowiedniego zasobu usługi Application Insights.</span><span class="sxs-lookup"><span data-stu-id="f0616-128">The instrumentation key is sent along with every item of telemetry and tells Application Insights to display it in your resource.</span></span>
* <span data-ttu-id="f0616-129">Składnik żądań HTTP jest opcjonalny.</span><span class="sxs-lookup"><span data-stu-id="f0616-129">The HTTP Request component is optional.</span></span> <span data-ttu-id="f0616-130">Powoduje automatyczne wysyłanie telemetrii dotyczącej żądań i czasów odpowiedzi do portalu.</span><span class="sxs-lookup"><span data-stu-id="f0616-130">It automatically sends telemetry about requests and response times to the portal.</span></span>
* <span data-ttu-id="f0616-131">Korelacja zdarzeń jest dodatkiem do składnika żądań HTTP.</span><span class="sxs-lookup"><span data-stu-id="f0616-131">Events correlation is an addition to the HTTP request component.</span></span> <span data-ttu-id="f0616-132">Przypisuje identyfikator do każdego żądania odebranego przez serwer i dodaje go do każdego elementu telemetrii jako właściwość „Operation.Id”.</span><span class="sxs-lookup"><span data-stu-id="f0616-132">It assigns an identifier to each request received by the server, and adds this identifier as a property to every item of telemetry as the property 'Operation.Id'.</span></span> <span data-ttu-id="f0616-133">Umożliwia korelowanie telemetrycznych skojarzonych z każdym żądaniem przez ustawienie filtru [diagnostycznych wyszukiwania](app-insights-diagnostic-search.md).</span><span class="sxs-lookup"><span data-stu-id="f0616-133">It allows you to correlate the telemetry associated with each request by setting a filter in [diagnostic search](app-insights-diagnostic-search.md).</span></span>

## <a name="4-add-an-http-filter"></a><span data-ttu-id="f0616-134">4. Dodawanie filtru HTTP</span><span class="sxs-lookup"><span data-stu-id="f0616-134">4. Add an HTTP filter</span></span>
<span data-ttu-id="f0616-135">Zlokalizuj i Otwórz plik web.xml w projekcie i scal poniższy fragment kodu w węźle aplikacji sieci web, gdzie są skonfigurowane filtry aplikacji.</span><span class="sxs-lookup"><span data-stu-id="f0616-135">Locate and open the web.xml file in your project, and merge the following snippet of code under the web-app node, where your application filters are configured.</span></span>

<span data-ttu-id="f0616-136">Aby uzyskać najbardziej dokładne wyniki, ten filtr powinien być mapowany przed wszystkimi innymi filtrami.</span><span class="sxs-lookup"><span data-stu-id="f0616-136">To get the most accurate results, the filter should be mapped before all other filters.</span></span>

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

## <a name="5-check-firewall-exceptions"></a><span data-ttu-id="f0616-137">5. Sprawdź wyjątki zapory</span><span class="sxs-lookup"><span data-stu-id="f0616-137">5. Check firewall exceptions</span></span>
<span data-ttu-id="f0616-138">Konieczne może być [ustawić wyjątki, aby wysłać dane wychodzące](app-insights-ip-addresses.md).</span><span class="sxs-lookup"><span data-stu-id="f0616-138">You might need to [set exceptions to send outgoing data](app-insights-ip-addresses.md).</span></span>

## <a name="6-restart-your-web-app"></a><span data-ttu-id="f0616-139">6. Uruchom ponownie aplikację sieci web</span><span class="sxs-lookup"><span data-stu-id="f0616-139">6. Restart your web app</span></span>
## <a name="7-view-your-telemetry-in-application-insights"></a><span data-ttu-id="f0616-140">7. Wyświetlanie telemetrii w usłudze Application Insights</span><span class="sxs-lookup"><span data-stu-id="f0616-140">7. View your telemetry in Application Insights</span></span>
<span data-ttu-id="f0616-141">Wróć do zasobu usługi Application Insights w witrynie [Microsoft Azure Portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="f0616-141">Return to your Application Insights resource in [Microsoft Azure portal](https://portal.azure.com).</span></span>

<span data-ttu-id="f0616-142">W bloku omówienie pojawi się dane telemetryczne dotyczące żądania HTTP.</span><span class="sxs-lookup"><span data-stu-id="f0616-142">Telemetry about HTTP requests appears on the overview blade.</span></span> <span data-ttu-id="f0616-143">(Jeśli ich tam nie ma, odczekaj kilka sekund, a następnie kliknij przycisk Odśwież).</span><span class="sxs-lookup"><span data-stu-id="f0616-143">(If it isn't there, wait a few seconds and then click Refresh.)</span></span>

![dane przykładowe](./media/app-insights-java-live/5-results.png)

<span data-ttu-id="f0616-145">Klikaj elementy wykresów, aby wyświetlać bardziej szczegółowe metryki.</span><span class="sxs-lookup"><span data-stu-id="f0616-145">Click through any chart to see more detailed metrics.</span></span> 

![](./media/app-insights-java-live/6-barchart.png)

<span data-ttu-id="f0616-146">Podczas przeglądania właściwości żądania, może uzyskać zdarzenia telemetrii skojarzonych z nim, takich jak żądania i wyjątków i.</span><span class="sxs-lookup"><span data-stu-id="f0616-146">And when viewing the properties of a request, you can see the telemetry events associated with it such as requests and exceptions.</span></span>

![](./media/app-insights-java-live/7-instance.png)

[<span data-ttu-id="f0616-147">Dowiedz się więcej o metrykach.</span><span class="sxs-lookup"><span data-stu-id="f0616-147">Learn more about metrics.</span></span>](app-insights-metrics-explorer.md)

## <a name="next-steps"></a><span data-ttu-id="f0616-148">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="f0616-148">Next steps</span></span>
* <span data-ttu-id="f0616-149">[Dodaj telemetrię do stron sieci web](app-insights-javascript.md) wyświetleń strony monitora i metryki użytkownika.</span><span class="sxs-lookup"><span data-stu-id="f0616-149">[Add telemetry to your web pages](app-insights-javascript.md) to monitor page views and user metrics.</span></span>
* <span data-ttu-id="f0616-150">[Ustawianie testów sieci web](app-insights-monitor-web-app-availability.md) aby upewnić się, aplikacja pozostaje na żywo i szybko reagowały.</span><span class="sxs-lookup"><span data-stu-id="f0616-150">[Set up web tests](app-insights-monitor-web-app-availability.md) to make sure your application stays live and responsive.</span></span>
* [<span data-ttu-id="f0616-151">Śledzenie dziennika</span><span class="sxs-lookup"><span data-stu-id="f0616-151">Capture log traces</span></span>](app-insights-java-trace-logs.md)
* <span data-ttu-id="f0616-152">[Wyszukiwanie zdarzeń i dzienniki](app-insights-diagnostic-search.md) do diagnozowania problemów.</span><span class="sxs-lookup"><span data-stu-id="f0616-152">[Search events and logs](app-insights-diagnostic-search.md) to help diagnose problems.</span></span>

