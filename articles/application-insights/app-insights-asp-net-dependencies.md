---
title: "Zależności śledzenia w usłudze Azure Application Insights | Dokumentacja firmy Microsoft"
description: "Analizowanie użycia, dostępności i wydajności aplikacji lokalnej lub aplikacji sieci Web na platformie Microsoft Azure za pomocą usługi Application Insights."
services: application-insights
documentationcenter: .net
author: CFreemanwa
manager: carmonm
ms.assetid: d15c4ca8-4c1a-47ab-a03d-c322b4bb2a9e
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 05/04/2017
ms.author: bwren
ms.openlocfilehash: 6e0b67ba98af27017901608dde4401600eb9957f
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/18/2017
---
# <a name="set-up-application-insights-dependency-tracking"></a><span data-ttu-id="10cba-103">Skonfiguruj usługę Application Insights: Śledzenie zależności</span><span class="sxs-lookup"><span data-stu-id="10cba-103">Set up Application Insights: Dependency tracking</span></span>
<span data-ttu-id="10cba-104">A *zależności* jest składnik zewnętrzny, który jest wywoływany przez aplikację.</span><span class="sxs-lookup"><span data-stu-id="10cba-104">A *dependency* is an external component that is called by your app.</span></span> <span data-ttu-id="10cba-105">Usługa ta jest zazwyczaj wywoływana przy użyciu protokołu HTTP, lub bazy danych lub systemu plików.</span><span class="sxs-lookup"><span data-stu-id="10cba-105">It's typically a service called using HTTP, or a database, or a file system.</span></span> <span data-ttu-id="10cba-106">[Usługa Application Insights](app-insights-overview.md) mierzy czas oczekiwania zależności aplikacji i jak często wywołanie zależności nie powiedzie się.</span><span class="sxs-lookup"><span data-stu-id="10cba-106">[Application Insights](app-insights-overview.md) measures how long your application waits for dependencies and how often a dependency call fails.</span></span> <span data-ttu-id="10cba-107">Zbadaj określonych wywołań i dotyczą żądań i wyjątki.</span><span class="sxs-lookup"><span data-stu-id="10cba-107">You can investigate specific calls, and relate them to requests and exceptions.</span></span>

![przykładowe wykresy](./media/app-insights-asp-net-dependencies/10-intro.png)

<span data-ttu-id="10cba-109">Monitor zależności poza pole raportów obecnie wywołań do tych typów zależności:</span><span class="sxs-lookup"><span data-stu-id="10cba-109">The out-of-the-box dependency monitor currently reports calls to these  types of dependencies:</span></span>

* <span data-ttu-id="10cba-110">Serwer</span><span class="sxs-lookup"><span data-stu-id="10cba-110">Server</span></span>
  * <span data-ttu-id="10cba-111">Bazy danych SQL</span><span class="sxs-lookup"><span data-stu-id="10cba-111">SQL databases</span></span>
  * <span data-ttu-id="10cba-112">Sieci web ASP.NET i usługi WCF, które używają powiązania oparte na protokole HTTP</span><span class="sxs-lookup"><span data-stu-id="10cba-112">ASP.NET web and WCF services that use HTTP-based bindings</span></span>
  * <span data-ttu-id="10cba-113">Lokalne lub zdalne wywołania HTTP</span><span class="sxs-lookup"><span data-stu-id="10cba-113">Local or remote HTTP calls</span></span>
  * <span data-ttu-id="10cba-114">Azure DB rozwiązania Cosmos, tabeli magazynu obiektów blob i kolejki</span><span class="sxs-lookup"><span data-stu-id="10cba-114">Azure Cosmos DB, table, blob storage, and queue</span></span>
* <span data-ttu-id="10cba-115">Strony sieci Web</span><span class="sxs-lookup"><span data-stu-id="10cba-115">Web pages</span></span>
  * <span data-ttu-id="10cba-116">Wywołania AJAX</span><span class="sxs-lookup"><span data-stu-id="10cba-116">AJAX calls</span></span>

<span data-ttu-id="10cba-117">Monitorowanie działania za pomocą [Instrumentacji kodu bajtów](https://msdn.microsoft.com/library/z9z62c29.aspx) wokół wybrane metody zostaną usunięte.</span><span class="sxs-lookup"><span data-stu-id="10cba-117">Monitoring works by using [byte code instrumentation](https://msdn.microsoft.com/library/z9z62c29.aspx) around selected methods.</span></span> <span data-ttu-id="10cba-118">Obciążenie jest minimalne.</span><span class="sxs-lookup"><span data-stu-id="10cba-118">Performance overhead is minimal.</span></span>

<span data-ttu-id="10cba-119">Można również napisać własny wywołania SDK do monitorowania innych zależności, zarówno w kodzie klienta i serwera przy użyciu [TrackDependency API](app-insights-api-custom-events-metrics.md#trackdependency).</span><span class="sxs-lookup"><span data-stu-id="10cba-119">You can also write your own SDK calls to monitor other dependencies, both in the client and server code, using the [TrackDependency API](app-insights-api-custom-events-metrics.md#trackdependency).</span></span>

## <a name="set-up-dependency-monitoring"></a><span data-ttu-id="10cba-120">Konfigurowanie monitorowania zależności</span><span class="sxs-lookup"><span data-stu-id="10cba-120">Set up dependency monitoring</span></span>
<span data-ttu-id="10cba-121">Informacje o zależnościach częściowe są zbierane automatycznie przez [zestaw SDK usługi Application Insights](app-insights-asp-net.md).</span><span class="sxs-lookup"><span data-stu-id="10cba-121">Partial dependency information is collected automatically by the [Application Insights SDK](app-insights-asp-net.md).</span></span> <span data-ttu-id="10cba-122">Aby uzyskać pełne dane, zainstalowanie odpowiedniego agenta dla serwera hosta.</span><span class="sxs-lookup"><span data-stu-id="10cba-122">To get complete data, install the appropriate agent for the host server.</span></span>

| <span data-ttu-id="10cba-123">Platforma</span><span class="sxs-lookup"><span data-stu-id="10cba-123">Platform</span></span> | <span data-ttu-id="10cba-124">Instalowanie</span><span class="sxs-lookup"><span data-stu-id="10cba-124">Install</span></span> |
| --- | --- |
| <span data-ttu-id="10cba-125">Serwer usług IIS</span><span class="sxs-lookup"><span data-stu-id="10cba-125">IIS Server</span></span> |<span data-ttu-id="10cba-126">Albo [Zainstaluj Monitor stanu na serwerze](app-insights-monitor-performance-live-website-now.md) lub [uaktualnić aplikacji .NET Framework 4.6 lub nowszy](http://go.microsoft.com/fwlink/?LinkId=528259) i zainstaluj [zestaw SDK usługi Application Insights](app-insights-asp-net.md) w aplikacji.</span><span class="sxs-lookup"><span data-stu-id="10cba-126">Either [install Status Monitor on your server](app-insights-monitor-performance-live-website-now.md) or [Upgrade your application to .NET framework 4.6 or later](http://go.microsoft.com/fwlink/?LinkId=528259) and install the [Application Insights SDK](app-insights-asp-net.md)  in your app.</span></span> |
| <span data-ttu-id="10cba-127">Aplikacja sieci Web platformy Azure</span><span class="sxs-lookup"><span data-stu-id="10cba-127">Azure Web App</span></span> |<span data-ttu-id="10cba-128">W Panelu sterowania aplikacji sieci web [otwarcie bloku usługi Application Insights w Panelu sterowania aplikacji sieci web](app-insights-azure-web-apps.md) i wybierz opcję instalacji, jeśli zostanie wyświetlony monit.</span><span class="sxs-lookup"><span data-stu-id="10cba-128">In your web app control panel, [open the Application Insights blade in your web app control panel](app-insights-azure-web-apps.md) and choose Install if prompted.</span></span> |
| <span data-ttu-id="10cba-129">Usługi w chmurze Azure</span><span class="sxs-lookup"><span data-stu-id="10cba-129">Azure Cloud Service</span></span> |<span data-ttu-id="10cba-130">[Zadanie uruchamiania użyj](app-insights-cloudservices.md) lub [zainstalowania środowiska .NET framework 4.6 +](../cloud-services/cloud-services-dotnet-install-dotnet.md)</span><span class="sxs-lookup"><span data-stu-id="10cba-130">[Use startup task](app-insights-cloudservices.md) or [Install .NET framework 4.6+](../cloud-services/cloud-services-dotnet-install-dotnet.md)</span></span> |

## <a name="where-to-find-dependency-data"></a><span data-ttu-id="10cba-131">Gdzie można znaleźć danych zależności</span><span class="sxs-lookup"><span data-stu-id="10cba-131">Where to find dependency data</span></span>
* <span data-ttu-id="10cba-132">[Mapowanie aplikacji](#application-map) wizualizuje zależności między aplikacji i składniki pokrewne.</span><span class="sxs-lookup"><span data-stu-id="10cba-132">[Application Map](#application-map) visualizes dependencies between your app and neighbouring components.</span></span>
* <span data-ttu-id="10cba-133">[Bloki wydajności, przeglądarki oraz Niepowodzenie](#performance-and-blades) przedstawiono dane zależności serwera.</span><span class="sxs-lookup"><span data-stu-id="10cba-133">[Performance, browser, and failure blades](#performance-and-blades) show server dependency data.</span></span>
* <span data-ttu-id="10cba-134">[Blok przeglądarki](#ajax-calls) pokazuje wywołania AJAX z przeglądarki użytkownika.</span><span class="sxs-lookup"><span data-stu-id="10cba-134">[Browsers blade](#ajax-calls) shows AJAX calls from your users' browsers.</span></span>
* <span data-ttu-id="10cba-135">[Kliknij go, z powolnym działaniem lub nieudanych żądań](#diagnose-slow-requests) do sprawdzania ich zależności wywołania.</span><span class="sxs-lookup"><span data-stu-id="10cba-135">[Click through from slow or failed requests](#diagnose-slow-requests) to check their dependency calls.</span></span>
* <span data-ttu-id="10cba-136">[Analiza](#analytics) można wykonać zapytania o dane zależności.</span><span class="sxs-lookup"><span data-stu-id="10cba-136">[Analytics](#analytics) can be used to query dependency data.</span></span>

## <a name="application-map"></a><span data-ttu-id="10cba-137">Mapa aplikacji</span><span class="sxs-lookup"><span data-stu-id="10cba-137">Application Map</span></span>
<span data-ttu-id="10cba-138">Mapowanie aplikacji działa jako pomoc wizualną odnajdywanie zależności między składnikami aplikacji.</span><span class="sxs-lookup"><span data-stu-id="10cba-138">Application Map acts as a visual aid to discovering dependencies between the components of your application.</span></span> <span data-ttu-id="10cba-139">Jest automatycznie generowany na podstawie danych telemetrycznych z aplikacji.</span><span class="sxs-lookup"><span data-stu-id="10cba-139">It is automatically generated from the telemetry from your app.</span></span> <span data-ttu-id="10cba-140">Ten przykład przedstawia wywołania AJAX ze skryptów przeglądarki i wywołania REST z aplikacji serwera do dwóch usług zewnętrznych.</span><span class="sxs-lookup"><span data-stu-id="10cba-140">This example shows AJAX calls from the browser scripts and REST calls from the server app to two external services.</span></span>

![Mapa aplikacji](./media/app-insights-asp-net-dependencies/08.png)

* <span data-ttu-id="10cba-142">**Przejdź z pól** do odpowiednich zależności i innych wykresów.</span><span class="sxs-lookup"><span data-stu-id="10cba-142">**Navigate from the boxes** to relevant dependency and other charts.</span></span>
* <span data-ttu-id="10cba-143">**Przypnij mapę** do [pulpitu nawigacyjnego](app-insights-dashboards.md), gdzie będzie pełną funkcjonalność.</span><span class="sxs-lookup"><span data-stu-id="10cba-143">**Pin the map** to the [dashboard](app-insights-dashboards.md), where it will be fully functional.</span></span>

<span data-ttu-id="10cba-144">[Dowiedz się więcej](app-insights-app-map.md).</span><span class="sxs-lookup"><span data-stu-id="10cba-144">[Learn more](app-insights-app-map.md).</span></span>

## <a name="performance-and-failure-blades"></a><span data-ttu-id="10cba-145">Wydajność i niepowodzenie bloków</span><span class="sxs-lookup"><span data-stu-id="10cba-145">Performance and failure blades</span></span>
<span data-ttu-id="10cba-146">Blok wydajności przedstawia czas trwania wywołania zależności za pomocą aplikacji serwera.</span><span class="sxs-lookup"><span data-stu-id="10cba-146">The performance blade shows the duration of dependency calls made by the server app.</span></span> <span data-ttu-id="10cba-147">Brak podsumowania wykres i tabelę segmentowanych przez wywołanie.</span><span class="sxs-lookup"><span data-stu-id="10cba-147">There's a summary chart and a table segmented by call.</span></span>

![Wykresy zależności bloku wydajności](./media/app-insights-asp-net-dependencies/dependencies-in-performance-blade.png)

<span data-ttu-id="10cba-149">Kliknij wykresy podsumowań lub elementów tabeli wyszukiwania raw wystąpień tych wywołań.</span><span class="sxs-lookup"><span data-stu-id="10cba-149">Click through the summary charts or the table items to search raw occurrences of these calls.</span></span>

![Wystąpienia wywołanie zależności](./media/app-insights-asp-net-dependencies/dependency-call-instance.png)

<span data-ttu-id="10cba-151">**Liczba awarii** są wyświetlane na **błędów** bloku.</span><span class="sxs-lookup"><span data-stu-id="10cba-151">**Failure counts** are shown on the **Failures** blade.</span></span> <span data-ttu-id="10cba-152">Błąd jest kod powrotny, który nie znajduje się w zakresie 200 – 399, lub nieznany.</span><span class="sxs-lookup"><span data-stu-id="10cba-152">A failure is any return code that is not in the range 200-399, or unknown.</span></span>

> [!NOTE]
> <span data-ttu-id="10cba-153">**100% błędów?**</span><span class="sxs-lookup"><span data-stu-id="10cba-153">**100% failures?**</span></span> <span data-ttu-id="10cba-154">-Prawdopodobnie oznacza to są dane z częściowa zależności tylko pierwsze.</span><span class="sxs-lookup"><span data-stu-id="10cba-154">- This probably indicates that you are only getting partial dependency data.</span></span> <span data-ttu-id="10cba-155">Musisz [Konfigurowanie zależności monitorowania odpowiednią dla danej platformy](#set-up-dependency-monitoring).</span><span class="sxs-lookup"><span data-stu-id="10cba-155">You need to [set up dependency monitoring appropriate to your platform](#set-up-dependency-monitoring).</span></span>
>
>

## <a name="ajax-calls"></a><span data-ttu-id="10cba-156">Wywołania AJAX</span><span class="sxs-lookup"><span data-stu-id="10cba-156">AJAX Calls</span></span>
<span data-ttu-id="10cba-157">Blok przeglądarki przedstawia współczynnik czas trwania i Niepowodzenie wywołania AJAX z [JavaScript na stronach sieci web](app-insights-javascript.md).</span><span class="sxs-lookup"><span data-stu-id="10cba-157">The Browsers blade shows the duration and failure rate of AJAX calls from [JavaScript in your web pages](app-insights-javascript.md).</span></span> <span data-ttu-id="10cba-158">Są wyświetlane jako zależności.</span><span class="sxs-lookup"><span data-stu-id="10cba-158">They are shown as Dependencies.</span></span>

## <span data-ttu-id="10cba-159"><a name="diagnosis"></a>Diagnozowanie powolne żądań</span><span class="sxs-lookup"><span data-stu-id="10cba-159"><a name="diagnosis"></a> Diagnose slow requests</span></span>
<span data-ttu-id="10cba-160">Każde zdarzenie żądania jest skojarzony z wywołania zależności, wyjątków i inne zdarzenia, które są śledzone podczas przetwarzania żądania aplikacji.</span><span class="sxs-lookup"><span data-stu-id="10cba-160">Each request event is associated with the dependency calls, exceptions and other events that are tracked while your app is processing the request.</span></span> <span data-ttu-id="10cba-161">Dlatego niektórych żądań są wykonywane nieprawidłowo, można ustalić czy jest ze względu na wolne odpowiedzi z zależności.</span><span class="sxs-lookup"><span data-stu-id="10cba-161">So if some requests are performing badly, you can find out whether it's due to slow responses from a dependency.</span></span>

<span data-ttu-id="10cba-162">Przejdźmy przykład tego.</span><span class="sxs-lookup"><span data-stu-id="10cba-162">Let's walk through an example of that.</span></span>

### <a name="tracing-from-requests-to-dependencies"></a><span data-ttu-id="10cba-163">Śledzenie żądań zależności</span><span class="sxs-lookup"><span data-stu-id="10cba-163">Tracing from requests to dependencies</span></span>
<span data-ttu-id="10cba-164">Otwarcie bloku wydajności i przyjrzyj się siatki żądania:</span><span class="sxs-lookup"><span data-stu-id="10cba-164">Open the Performance blade, and look at the grid of requests:</span></span>

![Lista żądań ze średnimi lub liczby](./media/app-insights-asp-net-dependencies/02-reqs.png)

<span data-ttu-id="10cba-166">Elementem najwyższego trwa bardzo długo.</span><span class="sxs-lookup"><span data-stu-id="10cba-166">The top one is taking very long.</span></span> <span data-ttu-id="10cba-167">Zobaczmy, jeśli firma Microsoft można ustalić, gdzie jest zużywany czas.</span><span class="sxs-lookup"><span data-stu-id="10cba-167">Let's see if we can find out where the time is spent.</span></span>

<span data-ttu-id="10cba-168">Kliknij ten wiersz, aby wyświetlić poszczególne żądania zdarzenia:</span><span class="sxs-lookup"><span data-stu-id="10cba-168">Click that row to see individual request events:</span></span>

![Lista wystąpień żądania](./media/app-insights-asp-net-dependencies/03-instances.png)

<span data-ttu-id="10cba-170">Kliknij pozycję dowolnego wystąpienia długotrwałe, aby sprawdzić dodatkowe, a następnie przewiń w dół do połączenia zdalnego zależności powiązane z tym żądaniem:</span><span class="sxs-lookup"><span data-stu-id="10cba-170">Click any long-running instance to inspect it further, and scroll down to the remote dependency calls related to this request:</span></span>

![Znajdź wywołania zależności zdalnych, zidentyfikuj nietypowe czas trwania](./media/app-insights-asp-net-dependencies/04-dependencies.png)

<span data-ttu-id="10cba-172">Wygląda jak większość obsługi czasu poświęconego tego żądania podczas wywołania usługi lokalnej.</span><span class="sxs-lookup"><span data-stu-id="10cba-172">It looks like most of the time servicing this request was spent in a call to a local service.</span></span>

<span data-ttu-id="10cba-173">Wybierz ten wiersz, aby uzyskać więcej informacji:</span><span class="sxs-lookup"><span data-stu-id="10cba-173">Select that row to get more information:</span></span>

![Kliknij go, że zdalnego zależności do identyfikowania dziedziczonej z istotnymi elementami](./media/app-insights-asp-net-dependencies/05-detail.png)

<span data-ttu-id="10cba-175">Wygląda na to, gdzie jest problem.</span><span class="sxs-lookup"><span data-stu-id="10cba-175">Looks like this is where the problem is.</span></span> <span data-ttu-id="10cba-176">Firma Microsoft już przeprowadzana na ten problem, więc teraz możemy just należy dowiedzieć się, dlaczego tego wywołania trwa tak długo.</span><span class="sxs-lookup"><span data-stu-id="10cba-176">We've pinpointed the problem, so now we just need to find out why that call is taking so long.</span></span>

### <a name="request-timeline"></a><span data-ttu-id="10cba-177">Oś czasu żądania</span><span class="sxs-lookup"><span data-stu-id="10cba-177">Request timeline</span></span>
<span data-ttu-id="10cba-178">W przypadku różnych nie ma żadnych wywołanie zależności, które są szczególnie długie.</span><span class="sxs-lookup"><span data-stu-id="10cba-178">In a different case, there is no dependency call that is particularly long.</span></span> <span data-ttu-id="10cba-179">Jednak przełączyć do widoku osi czasu, możemy stwierdzić, gdzie wystąpił opóźnienie w naszym wewnętrzne przetwarzanie:</span><span class="sxs-lookup"><span data-stu-id="10cba-179">But by switching to the timeline view, we can see where the delay occurred in our internal processing:</span></span>

![Znajdź wywołania zależności zdalnych, zidentyfikuj nietypowe czas trwania](./media/app-insights-asp-net-dependencies/04-1.png)

<span data-ttu-id="10cba-181">Wydaje się duży przerwę po pierwszej zależności wywołać, więc należy przyjrzymy się naszego kodu, aby zobaczyć, dlaczego jest.</span><span class="sxs-lookup"><span data-stu-id="10cba-181">There seems to be a big gap after the first dependency call, so we should look at our code to see why that is.</span></span>

### <a name="profile-your-live-site"></a><span data-ttu-id="10cba-182">Profil witryny na żywo</span><span class="sxs-lookup"><span data-stu-id="10cba-182">Profile your live site</span></span>

<span data-ttu-id="10cba-183">Nie wiadomo, gdzie przechodzi czas?</span><span class="sxs-lookup"><span data-stu-id="10cba-183">No idea where the time goes?</span></span> <span data-ttu-id="10cba-184">[Profilera usługi Application Insights](app-insights-profiler.md) najdłużej trwało śladów HTTP wywołań witryny na żywo i zawiera funkcje, które w kodzie.</span><span class="sxs-lookup"><span data-stu-id="10cba-184">The [Application Insights profiler](app-insights-profiler.md) traces HTTP calls to your live site and shows you which functions in your code took the longest time.</span></span>

## <a name="failed-requests"></a><span data-ttu-id="10cba-185">Żądań zakończonych niepowodzeniem</span><span class="sxs-lookup"><span data-stu-id="10cba-185">Failed requests</span></span>
<span data-ttu-id="10cba-186">Żądań zakończonych niepowodzeniem może też być skojarzone z niepowodzeniem wywołania zależności.</span><span class="sxs-lookup"><span data-stu-id="10cba-186">Failed requests might also be associated with failed calls to dependencies.</span></span> <span data-ttu-id="10cba-187">Firma Microsoft ponownie, kliknij go, można wykrywać problem.</span><span class="sxs-lookup"><span data-stu-id="10cba-187">Again, we can click through to track down the problem.</span></span>

![Kliknij wykres nieudanych żądań](./media/app-insights-asp-net-dependencies/06-fail.png)

<span data-ttu-id="10cba-189">Kliknij, aby wystąpienie nieudanych żądań i przyjrzyj się jego skojarzonego zdarzenia.</span><span class="sxs-lookup"><span data-stu-id="10cba-189">Click through to an occurrence of a failed request, and look at its associated events.</span></span>

![Kliknij typ żądania, kliknij wystąpienia, aby uzyskać dostęp do innego widoku tego samego wystąpienia, kliknij go, aby uzyskać szczegóły wyjątku.](./media/app-insights-asp-net-dependencies/07-faildetail.png)

## <a name="analytics"></a><span data-ttu-id="10cba-191">Analiza</span><span class="sxs-lookup"><span data-stu-id="10cba-191">Analytics</span></span>
<span data-ttu-id="10cba-192">Można śledzić zależności w [języka zapytań usługi Analiza dzienników](https://docs.loganalytics.io/).</span><span class="sxs-lookup"><span data-stu-id="10cba-192">You can track dependencies in the [Log Analytics query language](https://docs.loganalytics.io/).</span></span> <span data-ttu-id="10cba-193">Oto kilka przykładów.</span><span class="sxs-lookup"><span data-stu-id="10cba-193">Here are some examples.</span></span>

* <span data-ttu-id="10cba-194">Znajdź wszystkie wywołania zależności nie powiodło się:</span><span class="sxs-lookup"><span data-stu-id="10cba-194">Find any failed dependency calls:</span></span>

```

    dependencies | where success != "True" | take 10
```

* <span data-ttu-id="10cba-195">Znajdź wywołania AJAX:</span><span class="sxs-lookup"><span data-stu-id="10cba-195">Find AJAX calls:</span></span>

```

    dependencies | where client_Type == "Browser" | take 10
```

* <span data-ttu-id="10cba-196">Znajdź związanych z żądaniami wywołania zależności:</span><span class="sxs-lookup"><span data-stu-id="10cba-196">Find dependency calls associated with requests:</span></span>

```

    dependencies
    | where timestamp > ago(1d) and  client_Type != "Browser"
    | join (requests | where timestamp > ago(1d))
      on operation_Id  
```


* <span data-ttu-id="10cba-197">Znajdź wywołania AJAX skojarzone z wyświetleń strony:</span><span class="sxs-lookup"><span data-stu-id="10cba-197">Find AJAX calls associated with page views:</span></span>

```

    dependencies
    | where timestamp > ago(1d) and  client_Type == "Browser"
    | join (browserTimings | where timestamp > ago(1d))
      on operation_Id
```



## <a name="custom-dependency-tracking"></a><span data-ttu-id="10cba-198">Niestandardowe śledzenia zależności</span><span class="sxs-lookup"><span data-stu-id="10cba-198">Custom dependency tracking</span></span>
<span data-ttu-id="10cba-199">Standardowy moduł śledzenia zależności automatycznie odnajduje zależności zewnętrzne, takie jak bazy danych i interfejsów API REST.</span><span class="sxs-lookup"><span data-stu-id="10cba-199">The standard dependency-tracking module automatically discovers external dependencies such as databases and REST APIs.</span></span> <span data-ttu-id="10cba-200">Jednak może być niektóre dodatkowe składniki należy traktować w taki sam sposób.</span><span class="sxs-lookup"><span data-stu-id="10cba-200">But you might want some additional components to be treated in the same way.</span></span>

<span data-ttu-id="10cba-201">Można napisać kod, który wysyła informacje o zależnościach, korzystającej z tego samego [TrackDependency API](app-insights-api-custom-events-metrics.md#trackdependency) używany przez standardowe moduły.</span><span class="sxs-lookup"><span data-stu-id="10cba-201">You can write code that sends dependency information, using the same [TrackDependency API](app-insights-api-custom-events-metrics.md#trackdependency) that is used by the standard modules.</span></span>

<span data-ttu-id="10cba-202">Na przykład jeśli kod jest kompilacji z zestawu, który nie jest pisana samodzielnie, można czasu wszystkie wywołania, aby dowiedzieć się, jakie wkład zgłasza Twoje czasy odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="10cba-202">For example, if you build your code with an assembly that you didn't write yourself, you could time all the calls to it, to find out what contribution it makes to your response times.</span></span> <span data-ttu-id="10cba-203">Te dane wyświetlane na wykresach zależności w usłudze Application Insights, aby wysyłać go za pomocą `TrackDependency`.</span><span class="sxs-lookup"><span data-stu-id="10cba-203">To have this data displayed in the dependency charts in Application Insights, send it using `TrackDependency`.</span></span>

```C#

            var startTime = DateTime.UtcNow;
            var timer = System.Diagnostics.Stopwatch.StartNew();
            try
            {
                success = dependency.Call();
            }
            finally
            {
                timer.Stop();
                telemetry.TrackDependency("myDependency", "myCall", startTime, timer.Elapsed, success);
            }
```

<span data-ttu-id="10cba-204">Jeśli chcesz wyłączyć modułu śledzenia zależności standardowe, Usuń odwołanie do DependencyTrackingTelemetryModule w [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md).</span><span class="sxs-lookup"><span data-stu-id="10cba-204">If you want to switch off the standard dependency tracking module, remove the reference to DependencyTrackingTelemetryModule in [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md).</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="10cba-205">Rozwiązywanie problemów</span><span class="sxs-lookup"><span data-stu-id="10cba-205">Troubleshooting</span></span>
<span data-ttu-id="10cba-206">*Powodzenie zależności Flaga zawsze wyświetla wartość PRAWDA lub FAŁSZ.*</span><span class="sxs-lookup"><span data-stu-id="10cba-206">*Dependency success flag always shows either true or false.*</span></span>

<span data-ttu-id="10cba-207">*Zapytania SQL nie są wyświetlane w całości.*</span><span class="sxs-lookup"><span data-stu-id="10cba-207">*SQL query not shown in full.*</span></span>

* <span data-ttu-id="10cba-208">Uaktualnij do najnowszej wersji zestawu SDK.</span><span class="sxs-lookup"><span data-stu-id="10cba-208">Upgrade to the latest version of the SDK.</span></span> <span data-ttu-id="10cba-209">Jeśli wersja .NET jest mniejsza niż 4.6:</span><span class="sxs-lookup"><span data-stu-id="10cba-209">If your .NET version is less than 4.6:</span></span>
  * <span data-ttu-id="10cba-210">Host usługi IIS: Zainstaluj [agenta Application Insights](app-insights-monitor-performance-live-website-now.md) na serwerach hostach.</span><span class="sxs-lookup"><span data-stu-id="10cba-210">IIS host: Install [Application Insights Agent](app-insights-monitor-performance-live-website-now.md) on the host servers.</span></span>
  * <span data-ttu-id="10cba-211">Aplikacja sieci web platformy Azure: Otwórz Application Insights w Panelu sterowania aplikacji sieci web, a następnie zainstaluj usługę Application Insights.</span><span class="sxs-lookup"><span data-stu-id="10cba-211">Azure web app: Open Application Insights tab in the web app control panel, and install Application Insights.</span></span>

## <a name="video"></a><span data-ttu-id="10cba-212">Połączenia wideo</span><span class="sxs-lookup"><span data-stu-id="10cba-212">Video</span></span>

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/112/player]

## <a name="next-steps"></a><span data-ttu-id="10cba-213">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="10cba-213">Next steps</span></span>
* [<span data-ttu-id="10cba-214">Wyjątki</span><span class="sxs-lookup"><span data-stu-id="10cba-214">Exceptions</span></span>](app-insights-asp-net-exceptions.md)
* [<span data-ttu-id="10cba-215">Dane użytkownika i strony</span><span class="sxs-lookup"><span data-stu-id="10cba-215">User & page data</span></span>](app-insights-javascript.md)
* [<span data-ttu-id="10cba-216">Dostępność</span><span class="sxs-lookup"><span data-stu-id="10cba-216">Availability</span></span>](app-insights-monitor-web-app-availability.md)
