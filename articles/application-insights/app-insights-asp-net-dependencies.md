---
title: "aaaDependency śledzenia w usłudze Azure Application Insights | Dokumentacja firmy Microsoft"
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
ms.openlocfilehash: e72f5465462ae8e64363cbbaa62911aff636c504
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-application-insights-dependency-tracking"></a><span data-ttu-id="afae0-103">Skonfiguruj usługę Application Insights: Śledzenie zależności</span><span class="sxs-lookup"><span data-stu-id="afae0-103">Set up Application Insights: Dependency tracking</span></span>
<span data-ttu-id="afae0-104">A *zależności* jest składnik zewnętrzny, który jest wywoływany przez aplikację.</span><span class="sxs-lookup"><span data-stu-id="afae0-104">A *dependency* is an external component that is called by your app.</span></span> <span data-ttu-id="afae0-105">Usługa ta jest zazwyczaj wywoływana przy użyciu protokołu HTTP, lub bazy danych lub systemu plików.</span><span class="sxs-lookup"><span data-stu-id="afae0-105">It's typically a service called using HTTP, or a database, or a file system.</span></span> <span data-ttu-id="afae0-106">[Usługa Application Insights](app-insights-overview.md) mierzy czas oczekiwania zależności aplikacji i jak często wywołanie zależności nie powiedzie się.</span><span class="sxs-lookup"><span data-stu-id="afae0-106">[Application Insights](app-insights-overview.md) measures how long your application waits for dependencies and how often a dependency call fails.</span></span> <span data-ttu-id="afae0-107">Zbadaj określonych wywołań i łączyć je toorequests i wyjątki.</span><span class="sxs-lookup"><span data-stu-id="afae0-107">You can investigate specific calls, and relate them toorequests and exceptions.</span></span>

![przykładowe wykresy](./media/app-insights-asp-net-dependencies/10-intro.png)

<span data-ttu-id="afae0-109">monitor zależności poza pole Hello raportów obecnie typy toothese wywołania zależności:</span><span class="sxs-lookup"><span data-stu-id="afae0-109">hello out-of-the-box dependency monitor currently reports calls toothese  types of dependencies:</span></span>

* <span data-ttu-id="afae0-110">Serwer</span><span class="sxs-lookup"><span data-stu-id="afae0-110">Server</span></span>
  * <span data-ttu-id="afae0-111">Bazy danych SQL</span><span class="sxs-lookup"><span data-stu-id="afae0-111">SQL databases</span></span>
  * <span data-ttu-id="afae0-112">Sieci web ASP.NET i usługi WCF, które używają powiązania oparte na protokole HTTP</span><span class="sxs-lookup"><span data-stu-id="afae0-112">ASP.NET web and WCF services that use HTTP-based bindings</span></span>
  * <span data-ttu-id="afae0-113">Lokalne lub zdalne wywołania HTTP</span><span class="sxs-lookup"><span data-stu-id="afae0-113">Local or remote HTTP calls</span></span>
  * <span data-ttu-id="afae0-114">Azure DB rozwiązania Cosmos, tabeli magazynu obiektów blob i kolejki</span><span class="sxs-lookup"><span data-stu-id="afae0-114">Azure Cosmos DB, table, blob storage, and queue</span></span>
* <span data-ttu-id="afae0-115">Strony sieci Web</span><span class="sxs-lookup"><span data-stu-id="afae0-115">Web pages</span></span>
  * <span data-ttu-id="afae0-116">Wywołania AJAX</span><span class="sxs-lookup"><span data-stu-id="afae0-116">AJAX calls</span></span>

<span data-ttu-id="afae0-117">Monitorowanie działania za pomocą [Instrumentacji kodu bajtów](https://msdn.microsoft.com/library/z9z62c29.aspx) wokół wybrane metody zostaną usunięte.</span><span class="sxs-lookup"><span data-stu-id="afae0-117">Monitoring works by using [byte code instrumentation](https://msdn.microsoft.com/library/z9z62c29.aspx) around selected methods.</span></span> <span data-ttu-id="afae0-118">Obciążenie jest minimalne.</span><span class="sxs-lookup"><span data-stu-id="afae0-118">Performance overhead is minimal.</span></span>

<span data-ttu-id="afae0-119">Można również napisać własny zestaw SDK wymaga toomonitor innych zależności, zarówno w hello kod klienta i serwera, jak za pomocą hello [TrackDependency API](app-insights-api-custom-events-metrics.md#trackdependency).</span><span class="sxs-lookup"><span data-stu-id="afae0-119">You can also write your own SDK calls toomonitor other dependencies, both in hello client and server code, using hello [TrackDependency API](app-insights-api-custom-events-metrics.md#trackdependency).</span></span>

## <a name="set-up-dependency-monitoring"></a><span data-ttu-id="afae0-120">Konfigurowanie monitorowania zależności</span><span class="sxs-lookup"><span data-stu-id="afae0-120">Set up dependency monitoring</span></span>
<span data-ttu-id="afae0-121">Informacje o zależnościach częściowe są zbierane automatycznie przez hello [zestaw SDK usługi Application Insights](app-insights-asp-net.md).</span><span class="sxs-lookup"><span data-stu-id="afae0-121">Partial dependency information is collected automatically by hello [Application Insights SDK](app-insights-asp-net.md).</span></span> <span data-ttu-id="afae0-122">tooget pełnych danych, zainstaluj hello odpowiedniego agenta dla powitania serwera hosta.</span><span class="sxs-lookup"><span data-stu-id="afae0-122">tooget complete data, install hello appropriate agent for hello host server.</span></span>

| <span data-ttu-id="afae0-123">Platforma</span><span class="sxs-lookup"><span data-stu-id="afae0-123">Platform</span></span> | <span data-ttu-id="afae0-124">Instalowanie</span><span class="sxs-lookup"><span data-stu-id="afae0-124">Install</span></span> |
| --- | --- |
| <span data-ttu-id="afae0-125">Serwer usług IIS</span><span class="sxs-lookup"><span data-stu-id="afae0-125">IIS Server</span></span> |<span data-ttu-id="afae0-126">Albo [Zainstaluj Monitor stanu na serwerze](app-insights-monitor-performance-live-website-now.md) lub [uaktualnienia struktury too.NET aplikacji 4.6 lub nowszy](http://go.microsoft.com/fwlink/?LinkId=528259) i zainstaluj hello [zestaw SDK usługi Application Insights](app-insights-asp-net.md) w aplikacji.</span><span class="sxs-lookup"><span data-stu-id="afae0-126">Either [install Status Monitor on your server](app-insights-monitor-performance-live-website-now.md) or [Upgrade your application too.NET framework 4.6 or later](http://go.microsoft.com/fwlink/?LinkId=528259) and install hello [Application Insights SDK](app-insights-asp-net.md)  in your app.</span></span> |
| <span data-ttu-id="afae0-127">Aplikacja sieci Web platformy Azure</span><span class="sxs-lookup"><span data-stu-id="afae0-127">Azure Web App</span></span> |<span data-ttu-id="afae0-128">W Panelu sterowania aplikacji sieci web [hello Otwórz blok usługi Application Insights w Panelu sterowania aplikacji sieci web](app-insights-azure-web-apps.md) i wybierz opcję instalacji, jeśli zostanie wyświetlony monit.</span><span class="sxs-lookup"><span data-stu-id="afae0-128">In your web app control panel, [open hello Application Insights blade in your web app control panel](app-insights-azure-web-apps.md) and choose Install if prompted.</span></span> |
| <span data-ttu-id="afae0-129">Usługi w chmurze Azure</span><span class="sxs-lookup"><span data-stu-id="afae0-129">Azure Cloud Service</span></span> |<span data-ttu-id="afae0-130">[Zadanie uruchamiania użyj](app-insights-cloudservices.md) lub [zainstalowania środowiska .NET framework 4.6 +](../cloud-services/cloud-services-dotnet-install-dotnet.md)</span><span class="sxs-lookup"><span data-stu-id="afae0-130">[Use startup task](app-insights-cloudservices.md) or [Install .NET framework 4.6+](../cloud-services/cloud-services-dotnet-install-dotnet.md)</span></span> |

## <a name="where-toofind-dependency-data"></a><span data-ttu-id="afae0-131">Gdy dane zależności toofind</span><span class="sxs-lookup"><span data-stu-id="afae0-131">Where toofind dependency data</span></span>
* <span data-ttu-id="afae0-132">[Mapowanie aplikacji](#application-map) wizualizuje zależności między aplikacji i składniki pokrewne.</span><span class="sxs-lookup"><span data-stu-id="afae0-132">[Application Map](#application-map) visualizes dependencies between your app and neighbouring components.</span></span>
* <span data-ttu-id="afae0-133">[Bloki wydajności, przeglądarki oraz Niepowodzenie](#performance-and-blades) przedstawiono dane zależności serwera.</span><span class="sxs-lookup"><span data-stu-id="afae0-133">[Performance, browser, and failure blades](#performance-and-blades) show server dependency data.</span></span>
* <span data-ttu-id="afae0-134">[Blok przeglądarki](#ajax-calls) pokazuje wywołania AJAX z przeglądarki użytkownika.</span><span class="sxs-lookup"><span data-stu-id="afae0-134">[Browsers blade](#ajax-calls) shows AJAX calls from your users' browsers.</span></span>
* <span data-ttu-id="afae0-135">[Kliknij go, z powolnym działaniem lub nieudanych żądań](#diagnose-slow-requests) toocheck wywołania ich zależności.</span><span class="sxs-lookup"><span data-stu-id="afae0-135">[Click through from slow or failed requests](#diagnose-slow-requests) toocheck their dependency calls.</span></span>
* <span data-ttu-id="afae0-136">[Analiza](#analytics) mogą być używane tooquery zależności danych.</span><span class="sxs-lookup"><span data-stu-id="afae0-136">[Analytics](#analytics) can be used tooquery dependency data.</span></span>

## <a name="application-map"></a><span data-ttu-id="afae0-137">Mapa aplikacji</span><span class="sxs-lookup"><span data-stu-id="afae0-137">Application Map</span></span>
<span data-ttu-id="afae0-138">Mapowanie aplikacji działa jako pomoc visual toodiscovering zależności między składnikami aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="afae0-138">Application Map acts as a visual aid toodiscovering dependencies between hello components of your application.</span></span> <span data-ttu-id="afae0-139">Jest automatycznie generowany na podstawie danych telemetrycznych hello z aplikacji.</span><span class="sxs-lookup"><span data-stu-id="afae0-139">It is automatically generated from hello telemetry from your app.</span></span> <span data-ttu-id="afae0-140">Ten przykład przedstawia wywołania AJAX hello przeglądarki skryptów i wywołania REST z powitania serwera usług zewnętrznych tootwo aplikacji.</span><span class="sxs-lookup"><span data-stu-id="afae0-140">This example shows AJAX calls from hello browser scripts and REST calls from hello server app tootwo external services.</span></span>

![Mapa aplikacji](./media/app-insights-asp-net-dependencies/08.png)

* <span data-ttu-id="afae0-142">**Przejdź z pól hello** toorelevant zależności oraz inne wykresy.</span><span class="sxs-lookup"><span data-stu-id="afae0-142">**Navigate from hello boxes** toorelevant dependency and other charts.</span></span>
* <span data-ttu-id="afae0-143">**Numer PIN hello mapy** toohello [pulpitu nawigacyjnego](app-insights-dashboards.md), gdzie będzie pełną funkcjonalność.</span><span class="sxs-lookup"><span data-stu-id="afae0-143">**Pin hello map** toohello [dashboard](app-insights-dashboards.md), where it will be fully functional.</span></span>

<span data-ttu-id="afae0-144">[Dowiedz się więcej](app-insights-app-map.md).</span><span class="sxs-lookup"><span data-stu-id="afae0-144">[Learn more](app-insights-app-map.md).</span></span>

## <a name="performance-and-failure-blades"></a><span data-ttu-id="afae0-145">Wydajność i niepowodzenie bloków</span><span class="sxs-lookup"><span data-stu-id="afae0-145">Performance and failure blades</span></span>
<span data-ttu-id="afae0-146">Blok wydajności Hello pokazuje hello czas trwania wywołania zależności przez powitania serwera aplikacji.</span><span class="sxs-lookup"><span data-stu-id="afae0-146">hello performance blade shows hello duration of dependency calls made by hello server app.</span></span> <span data-ttu-id="afae0-147">Brak podsumowania wykres i tabelę segmentowanych przez wywołanie.</span><span class="sxs-lookup"><span data-stu-id="afae0-147">There's a summary chart and a table segmented by call.</span></span>

![Wykresy zależności bloku wydajności](./media/app-insights-asp-net-dependencies/dependencies-in-performance-blade.png)

<span data-ttu-id="afae0-149">Kliknij wykresy podsumowań hello lub hello tabeli elementów toosearch raw wystąpień tych wywołań.</span><span class="sxs-lookup"><span data-stu-id="afae0-149">Click through hello summary charts or hello table items toosearch raw occurrences of these calls.</span></span>

![Wystąpienia wywołanie zależności](./media/app-insights-asp-net-dependencies/dependency-call-instance.png)

<span data-ttu-id="afae0-151">**Liczba awarii** są wyświetlane na powitania **błędów** bloku.</span><span class="sxs-lookup"><span data-stu-id="afae0-151">**Failure counts** are shown on hello **Failures** blade.</span></span> <span data-ttu-id="afae0-152">Błąd jest kod powrotny, który nie znajduje się w hello zakresu 200 – 399, lub nieznany.</span><span class="sxs-lookup"><span data-stu-id="afae0-152">A failure is any return code that is not in hello range 200-399, or unknown.</span></span>

> [!NOTE]
> <span data-ttu-id="afae0-153">**100% błędów?**</span><span class="sxs-lookup"><span data-stu-id="afae0-153">**100% failures?**</span></span> <span data-ttu-id="afae0-154">-Prawdopodobnie oznacza to są dane z częściowa zależności tylko pierwsze.</span><span class="sxs-lookup"><span data-stu-id="afae0-154">- This probably indicates that you are only getting partial dependency data.</span></span> <span data-ttu-id="afae0-155">Należy zbyt[Konfigurowanie monitorowania tooyour odpowiednie platformy zależności](#set-up-dependency-monitoring).</span><span class="sxs-lookup"><span data-stu-id="afae0-155">You need too[set up dependency monitoring appropriate tooyour platform](#set-up-dependency-monitoring).</span></span>
>
>

## <a name="ajax-calls"></a><span data-ttu-id="afae0-156">Wywołania AJAX</span><span class="sxs-lookup"><span data-stu-id="afae0-156">AJAX Calls</span></span>
<span data-ttu-id="afae0-157">Blok przeglądarki Hello pokazuje czas trwania hello i częstość niepowodzeń AJAX wywołuje z [JavaScript na stronach sieci web](app-insights-javascript.md).</span><span class="sxs-lookup"><span data-stu-id="afae0-157">hello Browsers blade shows hello duration and failure rate of AJAX calls from [JavaScript in your web pages](app-insights-javascript.md).</span></span> <span data-ttu-id="afae0-158">Są wyświetlane jako zależności.</span><span class="sxs-lookup"><span data-stu-id="afae0-158">They are shown as Dependencies.</span></span>

## <span data-ttu-id="afae0-159"><a name="diagnosis"></a>Diagnozowanie powolne żądań</span><span class="sxs-lookup"><span data-stu-id="afae0-159"><a name="diagnosis"></a> Diagnose slow requests</span></span>
<span data-ttu-id="afae0-160">Każde zdarzenie żądania jest powiązany z wywołania zależności hello, wyjątków i inne zdarzenia, które są śledzone podczas przetwarzania aplikacji hello żądania.</span><span class="sxs-lookup"><span data-stu-id="afae0-160">Each request event is associated with hello dependency calls, exceptions and other events that are tracked while your app is processing hello request.</span></span> <span data-ttu-id="afae0-161">Dlatego nieprawidłowo wykonywania niektórych żądań można ustalić czy jest powodu tooslow odpowiedzi z zależności.</span><span class="sxs-lookup"><span data-stu-id="afae0-161">So if some requests are performing badly, you can find out whether it's due tooslow responses from a dependency.</span></span>

<span data-ttu-id="afae0-162">Przejdźmy przykład tego.</span><span class="sxs-lookup"><span data-stu-id="afae0-162">Let's walk through an example of that.</span></span>

### <a name="tracing-from-requests-toodependencies"></a><span data-ttu-id="afae0-163">Śledzenie za pomocą toodependencies żądań</span><span class="sxs-lookup"><span data-stu-id="afae0-163">Tracing from requests toodependencies</span></span>
<span data-ttu-id="afae0-164">Otwarcie bloku wydajności hello i przyjrzyj się siatki hello żądań:</span><span class="sxs-lookup"><span data-stu-id="afae0-164">Open hello Performance blade, and look at hello grid of requests:</span></span>

![Lista żądań ze średnimi lub liczby](./media/app-insights-asp-net-dependencies/02-reqs.png)

<span data-ttu-id="afae0-166">Witaj top, który jest zbyt długa.</span><span class="sxs-lookup"><span data-stu-id="afae0-166">hello top one is taking very long.</span></span> <span data-ttu-id="afae0-167">Zobaczmy, jeśli firma Microsoft można ustalić, gdzie jest zużywany czas hello.</span><span class="sxs-lookup"><span data-stu-id="afae0-167">Let's see if we can find out where hello time is spent.</span></span>

<span data-ttu-id="afae0-168">Kliknij ten wiersz toosee oddzielne żądanie zdarzenia:</span><span class="sxs-lookup"><span data-stu-id="afae0-168">Click that row toosee individual request events:</span></span>

![Lista wystąpień żądania](./media/app-insights-asp-net-dependencies/03-instances.png)

<span data-ttu-id="afae0-170">Kliknij tooinspect wystąpienia dowolnego długotrwałe dalszego i przewiń w dół toohello zależności zdalne wywołania toothis pokrewne żądanie:</span><span class="sxs-lookup"><span data-stu-id="afae0-170">Click any long-running instance tooinspect it further, and scroll down toohello remote dependency calls related toothis request:</span></span>

![Znajdź wywołania zależności tooRemote, zidentyfikować nietypowe czas trwania](./media/app-insights-asp-net-dependencies/04-dependencies.png)

<span data-ttu-id="afae0-172">Wygląda jak większość hello obsługi czasu poświęconego tego żądania w usłudze lokalnej tooa wywołania.</span><span class="sxs-lookup"><span data-stu-id="afae0-172">It looks like most of hello time servicing this request was spent in a call tooa local service.</span></span>

<span data-ttu-id="afae0-173">Wybierz ten wiersz tooget więcej informacji:</span><span class="sxs-lookup"><span data-stu-id="afae0-173">Select that row tooget more information:</span></span>

![Kliknij przycisk za pośrednictwem tego culprit hello tooidentify zależności zdalne](./media/app-insights-asp-net-dependencies/05-detail.png)

<span data-ttu-id="afae0-175">Wygląda na to, gdzie jest hello problem.</span><span class="sxs-lookup"><span data-stu-id="afae0-175">Looks like this is where hello problem is.</span></span> <span data-ttu-id="afae0-176">Firma Microsoft już przeprowadzana na powitania problem. należy więc teraz możemy just toofind się, dlaczego tego wywołania trwa tak długo.</span><span class="sxs-lookup"><span data-stu-id="afae0-176">We've pinpointed hello problem, so now we just need toofind out why that call is taking so long.</span></span>

### <a name="request-timeline"></a><span data-ttu-id="afae0-177">Oś czasu żądania</span><span class="sxs-lookup"><span data-stu-id="afae0-177">Request timeline</span></span>
<span data-ttu-id="afae0-178">W przypadku różnych nie ma żadnych wywołanie zależności, które są szczególnie długie.</span><span class="sxs-lookup"><span data-stu-id="afae0-178">In a different case, there is no dependency call that is particularly long.</span></span> <span data-ttu-id="afae0-179">Ale przełączając toohello widoku osi czasu, możemy stwierdzić, których opóźnienie hello wystąpiła w naszym wewnętrzne przetwarzanie:</span><span class="sxs-lookup"><span data-stu-id="afae0-179">But by switching toohello timeline view, we can see where hello delay occurred in our internal processing:</span></span>

![Znajdź wywołania zależności tooRemote, zidentyfikować nietypowe czas trwania](./media/app-insights-asp-net-dependencies/04-1.png)

<span data-ttu-id="afae0-181">Prawdopodobnie toobe big przerwę po pierwszym wywołaniu zależności hello, więc należy przyjrzymy się naszego kodu toosee dlatego oznacza to.</span><span class="sxs-lookup"><span data-stu-id="afae0-181">There seems toobe a big gap after hello first dependency call, so we should look at our code toosee why that is.</span></span>

### <a name="profile-your-live-site"></a><span data-ttu-id="afae0-182">Profil witryny na żywo</span><span class="sxs-lookup"><span data-stu-id="afae0-182">Profile your live site</span></span>

<span data-ttu-id="afae0-183">Nie wiadomo, gdzie czas hello przechodzi? Witaj [profilera usługi Application Insights](app-insights-profiler.md) najdłużej hello trwało śladów HTTP wywołuje tooyour witryny na żywo i zawiera funkcje, które w kodzie.</span><span class="sxs-lookup"><span data-stu-id="afae0-183">No idea where hello time goes? hello [Application Insights profiler](app-insights-profiler.md) traces HTTP calls tooyour live site and shows you which functions in your code took hello longest time.</span></span>

## <a name="failed-requests"></a><span data-ttu-id="afae0-184">Żądań zakończonych niepowodzeniem</span><span class="sxs-lookup"><span data-stu-id="afae0-184">Failed requests</span></span>
<span data-ttu-id="afae0-185">Żądań zakończonych niepowodzeniem może też być skojarzone z toodependencies wywołania nie powiodło się.</span><span class="sxs-lookup"><span data-stu-id="afae0-185">Failed requests might also be associated with failed calls toodependencies.</span></span> <span data-ttu-id="afae0-186">Firma Microsoft ponownie, kliknij go, tootrack dół hello problem.</span><span class="sxs-lookup"><span data-stu-id="afae0-186">Again, we can click through tootrack down hello problem.</span></span>

![Kliknij przycisk hello wykres nieudanych żądań](./media/app-insights-asp-net-dependencies/06-fail.png)

<span data-ttu-id="afae0-188">Kliknij go, wystąpienie tooan nieudanych żądań i przyjrzyj się jego skojarzonego zdarzenia.</span><span class="sxs-lookup"><span data-stu-id="afae0-188">Click through tooan occurrence of a failed request, and look at its associated events.</span></span>

![Kliknij typ żądania, kliknij przycisk hello tooget tooa inny widok wystąpienia hello tego samego wystąpienia, kliknij go tooget szczegóły wyjątku.](./media/app-insights-asp-net-dependencies/07-faildetail.png)

## <a name="analytics"></a><span data-ttu-id="afae0-190">Analiza</span><span class="sxs-lookup"><span data-stu-id="afae0-190">Analytics</span></span>
<span data-ttu-id="afae0-191">Można śledzić zależności w hello [języka zapytań usługi Analiza dzienników](https://docs.loganalytics.io/).</span><span class="sxs-lookup"><span data-stu-id="afae0-191">You can track dependencies in hello [Log Analytics query language](https://docs.loganalytics.io/).</span></span> <span data-ttu-id="afae0-192">Oto kilka przykładów.</span><span class="sxs-lookup"><span data-stu-id="afae0-192">Here are some examples.</span></span>

* <span data-ttu-id="afae0-193">Znajdź wszystkie wywołania zależności nie powiodło się:</span><span class="sxs-lookup"><span data-stu-id="afae0-193">Find any failed dependency calls:</span></span>

```

    dependencies | where success != "True" | take 10
```

* <span data-ttu-id="afae0-194">Znajdź wywołania AJAX:</span><span class="sxs-lookup"><span data-stu-id="afae0-194">Find AJAX calls:</span></span>

```

    dependencies | where client_Type == "Browser" | take 10
```

* <span data-ttu-id="afae0-195">Znajdź związanych z żądaniami wywołania zależności:</span><span class="sxs-lookup"><span data-stu-id="afae0-195">Find dependency calls associated with requests:</span></span>

```

    dependencies
    | where timestamp > ago(1d) and  client_Type != "Browser"
    | join (requests | where timestamp > ago(1d))
      on operation_Id  
```


* <span data-ttu-id="afae0-196">Znajdź wywołania AJAX skojarzone z wyświetleń strony:</span><span class="sxs-lookup"><span data-stu-id="afae0-196">Find AJAX calls associated with page views:</span></span>

```

    dependencies
    | where timestamp > ago(1d) and  client_Type == "Browser"
    | join (browserTimings | where timestamp > ago(1d))
      on operation_Id
```



## <a name="custom-dependency-tracking"></a><span data-ttu-id="afae0-197">Niestandardowe śledzenia zależności</span><span class="sxs-lookup"><span data-stu-id="afae0-197">Custom dependency tracking</span></span>
<span data-ttu-id="afae0-198">Standardowy moduł śledzenia zależności Hello automatycznie odnajduje zależności zewnętrzne, takie jak bazy danych i interfejsów API REST.</span><span class="sxs-lookup"><span data-stu-id="afae0-198">hello standard dependency-tracking module automatically discovers external dependencies such as databases and REST APIs.</span></span> <span data-ttu-id="afae0-199">Może być toobe niektóre dodatkowe składniki używane w hello sam sposób.</span><span class="sxs-lookup"><span data-stu-id="afae0-199">But you might want some additional components toobe treated in hello same way.</span></span>

<span data-ttu-id="afae0-200">Można napisać kod, który wysyła informacje o zależnościach, przy użyciu hello sam [TrackDependency API](app-insights-api-custom-events-metrics.md#trackdependency) używany przez moduły standardowe hello.</span><span class="sxs-lookup"><span data-stu-id="afae0-200">You can write code that sends dependency information, using hello same [TrackDependency API](app-insights-api-custom-events-metrics.md#trackdependency) that is used by hello standard modules.</span></span>

<span data-ttu-id="afae0-201">Na przykład że nie są pisane samodzielnie, można czasu wszystkie tooit wywołania hello w przypadku tworzenia kodu z zestawem toofind się, jakie wkład ułatwia tooyour odpowiedzi czasu.</span><span class="sxs-lookup"><span data-stu-id="afae0-201">For example, if you build your code with an assembly that you didn't write yourself, you could time all hello calls tooit, toofind out what contribution it makes tooyour response times.</span></span> <span data-ttu-id="afae0-202">toohave wysyłać te dane wyświetlane na wykresach zależności hello w usłudze Application Insights, za pomocą `TrackDependency`.</span><span class="sxs-lookup"><span data-stu-id="afae0-202">toohave this data displayed in hello dependency charts in Application Insights, send it using `TrackDependency`.</span></span>

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

<span data-ttu-id="afae0-203">Tooswitch poza modułu śledzenia zależności standardowe hello, usunąć hello tooDependencyTrackingTelemetryModule odwołania w [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md).</span><span class="sxs-lookup"><span data-stu-id="afae0-203">If you want tooswitch off hello standard dependency tracking module, remove hello reference tooDependencyTrackingTelemetryModule in [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md).</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="afae0-204">Rozwiązywanie problemów</span><span class="sxs-lookup"><span data-stu-id="afae0-204">Troubleshooting</span></span>
<span data-ttu-id="afae0-205">*Powodzenie zależności Flaga zawsze wyświetla wartość PRAWDA lub FAŁSZ.*</span><span class="sxs-lookup"><span data-stu-id="afae0-205">*Dependency success flag always shows either true or false.*</span></span>

<span data-ttu-id="afae0-206">*Zapytania SQL nie są wyświetlane w całości.*</span><span class="sxs-lookup"><span data-stu-id="afae0-206">*SQL query not shown in full.*</span></span>

* <span data-ttu-id="afae0-207">Uaktualnij toohello najnowszą wersję hello zestawu SDK.</span><span class="sxs-lookup"><span data-stu-id="afae0-207">Upgrade toohello latest version of hello SDK.</span></span> <span data-ttu-id="afae0-208">Jeśli wersja .NET jest mniejsza niż 4.6:</span><span class="sxs-lookup"><span data-stu-id="afae0-208">If your .NET version is less than 4.6:</span></span>
  * <span data-ttu-id="afae0-209">Host usługi IIS: Zainstaluj [agenta Application Insights](app-insights-monitor-performance-live-website-now.md) na serwerach hostów hello.</span><span class="sxs-lookup"><span data-stu-id="afae0-209">IIS host: Install [Application Insights Agent](app-insights-monitor-performance-live-website-now.md) on hello host servers.</span></span>
  * <span data-ttu-id="afae0-210">Aplikacja sieci web platformy Azure: Otwórz Application Insights w Panelu sterowania aplikacji hello w sieci web, a następnie zainstaluj usługę Application Insights.</span><span class="sxs-lookup"><span data-stu-id="afae0-210">Azure web app: Open Application Insights tab in hello web app control panel, and install Application Insights.</span></span>

## <a name="video"></a><span data-ttu-id="afae0-211">Połączenia wideo</span><span class="sxs-lookup"><span data-stu-id="afae0-211">Video</span></span>

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/112/player]

## <a name="next-steps"></a><span data-ttu-id="afae0-212">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="afae0-212">Next steps</span></span>
* [<span data-ttu-id="afae0-213">Wyjątki</span><span class="sxs-lookup"><span data-stu-id="afae0-213">Exceptions</span></span>](app-insights-asp-net-exceptions.md)
* [<span data-ttu-id="afae0-214">Dane użytkownika i strony</span><span class="sxs-lookup"><span data-stu-id="afae0-214">User & page data</span></span>](app-insights-javascript.md)
* [<span data-ttu-id="afae0-215">Dostępność</span><span class="sxs-lookup"><span data-stu-id="afae0-215">Availability</span></span>](app-insights-monitor-web-app-availability.md)
