---
title: "aplikacje sieci web usługi Application Insights aaaAzure JavaScript | Dokumentacja firmy Microsoft"
description: "Pobieranie liczników wyświetleń stron i sesji, danych klienta sieci Web oraz śledzenie wzorców użycia. Wykrywanie wyjątków i problemów z wydajnością na stronach sieci Web w języku JavaScript."
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.assetid: 3b710d09-6ab4-4004-b26a-4fa840039500
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: get-started-article
ms.date: 03/14/2017
ms.author: bwren
ms.openlocfilehash: 986db3c3776471f9f8556f4e09f2d02aad022549
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="application-insights-for-web-pages"></a><span data-ttu-id="dc6b0-104">Usługa Application Insights dla stron sieci Web</span><span class="sxs-lookup"><span data-stu-id="dc6b0-104">Application Insights for web pages</span></span>
<span data-ttu-id="dc6b0-105">Dowiedz się o hello wydajności i użycia aplikacji lub strony sieci web.</span><span class="sxs-lookup"><span data-stu-id="dc6b0-105">Find out about hello performance and usage of your web page or app.</span></span> <span data-ttu-id="dc6b0-106">Jeśli dodasz [usługi Application Insights](app-insights-overview.md) tooyour skrypt strony, możesz uzyskać chronometrażu ładunków strona i wywołania AJAX, liczby i szczegóły błędów AJAX, a także użytkowników i liczby sesji w wyjątków przeglądarki.</span><span class="sxs-lookup"><span data-stu-id="dc6b0-106">If you add [Application Insights](app-insights-overview.md) tooyour page script, you get timings of page loads and AJAX calls, counts and details of browser exceptions and AJAX failures, as well as users and session counts.</span></span> <span data-ttu-id="dc6b0-107">Wszystkie te dane możesz rozdzielić według strony, systemu operacyjnego klienta i wersji przeglądarki, lokalizacji geograficznej i innych wymiarów.</span><span class="sxs-lookup"><span data-stu-id="dc6b0-107">All these can be segmented by page, client OS and browser version, geo location, and other dimensions.</span></span> <span data-ttu-id="dc6b0-108">Możesz ustawić alerty związane z liczbami błędów lub powolnym ładowaniem strony.</span><span class="sxs-lookup"><span data-stu-id="dc6b0-108">You can set alerts on failure counts or slow page loading.</span></span> <span data-ttu-id="dc6b0-109">I zaznaczając śledzenie wywołań kodu JavaScript, można śledzić używania różnych funkcji hello aplikacji strony sieci web.</span><span class="sxs-lookup"><span data-stu-id="dc6b0-109">And by inserting trace calls in your JavaScript code, you can track how hello different features of your web page application are used.</span></span>

<span data-ttu-id="dc6b0-110">Usługi Application Insights można używać z dowolnymi stronami sieci Web — wystarczy dodać krótki fragment kodu JavaScript.</span><span class="sxs-lookup"><span data-stu-id="dc6b0-110">Application Insights can be used with any web pages - you just add a short piece of JavaScript.</span></span> <span data-ttu-id="dc6b0-111">Jeśli Twoja usługa sieci Web jest zaprogramowana w technologii [Java](app-insights-java-get-started.md) lub [ASP.NET](app-insights-asp-net.md), możesz zintegrować telemetrię pochodzącą z serwera i klientów.</span><span class="sxs-lookup"><span data-stu-id="dc6b0-111">If your web service is [Java](app-insights-java-get-started.md) or [ASP.NET](app-insights-asp-net.md), you can integrate telemetry from your server and clients.</span></span>

![W witrynie portal.azure.com otwórz zasób swojej aplikacji, a następnie kliknij pozycję Przeglądarka](./media/app-insights-javascript/03.png)

<span data-ttu-id="dc6b0-113">Musisz mieć subskrypcję za[Microsoft Azure](https://azure.com).</span><span class="sxs-lookup"><span data-stu-id="dc6b0-113">You need a subscription too[Microsoft Azure](https://azure.com).</span></span> <span data-ttu-id="dc6b0-114">Jeśli zespół ma organizacyjnej subskrypcji, poproś hello właściciela tooadd Twojego tooit Account firmy Microsoft.</span><span class="sxs-lookup"><span data-stu-id="dc6b0-114">If your team has an organizational subscription, ask hello owner tooadd your Microsoft Account tooit.</span></span> <span data-ttu-id="dc6b0-115">Tworząc strony i używając ich na małą skalę, nie poniesiesz żadnych kosztów.</span><span class="sxs-lookup"><span data-stu-id="dc6b0-115">Development and small-scale use won't cost anything.</span></span>

## <a name="set-up-application-insights-for-your-web-page"></a><span data-ttu-id="dc6b0-116">Konfigurowanie usługi Application Insights dla strony sieci Web</span><span class="sxs-lookup"><span data-stu-id="dc6b0-116">Set up Application Insights for your web page</span></span>
<span data-ttu-id="dc6b0-117">Dodaj hello modułu ładującego kodu fragment tooyour stron sieci web, w następujący sposób.</span><span class="sxs-lookup"><span data-stu-id="dc6b0-117">Add hello loader code snippet tooyour web pages, as follows.</span></span>

### <a name="open-or-create-application-insights-resource"></a><span data-ttu-id="dc6b0-118">Otwieranie lub tworzenie zasobu usługi Application Insights</span><span class="sxs-lookup"><span data-stu-id="dc6b0-118">Open or create Application Insights resource</span></span>
<span data-ttu-id="dc6b0-119">Hello zasobu usługi Application Insights jest, gdzie są wyświetlane dane dotyczące wydajności i użycia ze strony.</span><span class="sxs-lookup"><span data-stu-id="dc6b0-119">hello Application Insights resource is where data about your page's performance and usage is displayed.</span></span> 

<span data-ttu-id="dc6b0-120">Zaloguj się do [portalu Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="dc6b0-120">Sign into [Azure portal](https://portal.azure.com).</span></span>

<span data-ttu-id="dc6b0-121">Jeśli już skonfigurowane monitorowania po stronie serwera na powitania aplikacji, masz już zasobu:</span><span class="sxs-lookup"><span data-stu-id="dc6b0-121">If you already set up monitoring for hello server side of your app, you already have a resource:</span></span>

![Wybierz kolejno opcje Przeglądaj, Usługi dla deweloperów, Application Insights.](./media/app-insights-javascript/01-find.png)

<span data-ttu-id="dc6b0-123">Jeśli nie ma zasobu, utwórz go:</span><span class="sxs-lookup"><span data-stu-id="dc6b0-123">If you don't have one, create it:</span></span>

![Wybierz kolejno opcje Nowe, Usługi dla deweloperów, Application Insights.](./media/app-insights-javascript/01-create.png)

<span data-ttu-id="dc6b0-125">*Już masz pytania?*</span><span class="sxs-lookup"><span data-stu-id="dc6b0-125">*Questions already?*</span></span> <span data-ttu-id="dc6b0-126">[Więcej informacji na temat tworzenia zasobu](app-insights-create-new-resource.md).</span><span class="sxs-lookup"><span data-stu-id="dc6b0-126">[More about creating a resource](app-insights-create-new-resource.md).</span></span>

### <a name="add-hello-sdk-script-tooyour-app-or-web-pages"></a><span data-ttu-id="dc6b0-127">Dodaj hello SDK skryptu tooyour aplikacji lub strony sieci web</span><span class="sxs-lookup"><span data-stu-id="dc6b0-127">Add hello SDK script tooyour app or web pages</span></span>
<span data-ttu-id="dc6b0-128">W Szybki Start Pobierz hello skryptu dla stron sieci web:</span><span class="sxs-lookup"><span data-stu-id="dc6b0-128">In Quick Start, get hello script for web pages:</span></span>

![W bloku Omówienie aplikacji wybierz pozycję Szybki Start, Pobierz kod toomonitor stron sieci web.](./media/app-insights-javascript/02-monitor-web-page.png)

<span data-ttu-id="dc6b0-131">Wstaw skrypt hello tuż przed hello `</head>` tag każdej strony ma tootrack.</span><span class="sxs-lookup"><span data-stu-id="dc6b0-131">Insert hello script just before hello `</head>` tag of every page you want tootrack.</span></span> <span data-ttu-id="dc6b0-132">Jeśli strony głównej witryny sieci Web, można umieścić hello skryptu.</span><span class="sxs-lookup"><span data-stu-id="dc6b0-132">If your website has a master page, you can put hello script there.</span></span> <span data-ttu-id="dc6b0-133">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="dc6b0-133">For example:</span></span>

* <span data-ttu-id="dc6b0-134">W projekcie ASP.NET MVC możesz umieścić go w pliku `View\Shared\_Layout.cshtml`</span><span class="sxs-lookup"><span data-stu-id="dc6b0-134">In an ASP.NET MVC project, you'd put it in `View\Shared\_Layout.cshtml`</span></span>
* <span data-ttu-id="dc6b0-135">W witrynie programu SharePoint, na panelu sterowania hello, otwórz [ustawienia witryny / strony wzorcowej](app-insights-sharepoint.md).</span><span class="sxs-lookup"><span data-stu-id="dc6b0-135">In a SharePoint site, on hello control panel, open [Site Settings / Master Page](app-insights-sharepoint.md).</span></span>

<span data-ttu-id="dc6b0-136">skrypt Hello zawiera klucz Instrumentacji hello kieruje zasobu usługi Application Insights tooyour danych hello.</span><span class="sxs-lookup"><span data-stu-id="dc6b0-136">hello script contains hello instrumentation key that directs hello data tooyour Application Insights resource.</span></span> 

<span data-ttu-id="dc6b0-137">([Bardziej szczegółowy opis hello skryptu. ](http://apmtips.com/blog/2015/03/18/javascript-snippet-explained/))</span><span class="sxs-lookup"><span data-stu-id="dc6b0-137">([Deeper explanation of hello script.](http://apmtips.com/blog/2015/03/18/javascript-snippet-explained/))</span></span>

<span data-ttu-id="dc6b0-138">*(Jeśli używasz dobrze znanej struktury stron sieci Web, poszukaj adapterów usługi Application Insights. Takim adapterem jest na przykład [moduł AngularJS](http://ngmodules.org/modules/angular-appinsights)).*</span><span class="sxs-lookup"><span data-stu-id="dc6b0-138">*(If you're using a well-known web page framework, look around for Application Insights adaptors. For example, there's [an AngularJS module](http://ngmodules.org/modules/angular-appinsights).)*</span></span>

## <a name="detailed-configuration"></a><span data-ttu-id="dc6b0-139">Konfiguracja szczegółowa</span><span class="sxs-lookup"><span data-stu-id="dc6b0-139">Detailed configuration</span></span>
<span data-ttu-id="dc6b0-140">Istnieje kilka [parametrów](https://github.com/Microsoft/ApplicationInsights-JS/blob/master/API-reference.md#config), które można ustawić, chociaż w większości przypadków nie jest to potrzebne.</span><span class="sxs-lookup"><span data-stu-id="dc6b0-140">There are several [parameters](https://github.com/Microsoft/ApplicationInsights-JS/blob/master/API-reference.md#config) you can set, though in most cases, you shouldn't need to.</span></span> <span data-ttu-id="dc6b0-141">Na przykład można wyłączyć lub Ogranicz liczbę hello wywołania Ajax zgłaszanych w ciągu widok strony (tooreduce ruch).</span><span class="sxs-lookup"><span data-stu-id="dc6b0-141">For example, you can disable or limit hello number of Ajax calls reported per page view (tooreduce traffic).</span></span> <span data-ttu-id="dc6b0-142">Można także ustawić debugowania trybu toohave telemetrii Przenieś szybko przez potok hello bez jest umieścić w zadaniu wsadowym.</span><span class="sxs-lookup"><span data-stu-id="dc6b0-142">Or you can set debug mode toohave telemetry move rapidly through hello pipeline without being batched.</span></span>

<span data-ttu-id="dc6b0-143">tooset tych parametrów, Wyszukaj ten wiersz w hello fragment kodu i dodać więcej elementów oddzielonych przecinkami po nim:</span><span class="sxs-lookup"><span data-stu-id="dc6b0-143">tooset these parameters, look for this line in hello code snippet, and add more comma-separated items after it:</span></span>

    })({
      instrumentationKey: "..."
      // Insert here
    });

<span data-ttu-id="dc6b0-144">Witaj [dostępne parametry](https://github.com/Microsoft/ApplicationInsights-JS/blob/master/API-reference.md#config) obejmują:</span><span class="sxs-lookup"><span data-stu-id="dc6b0-144">hello [available parameters](https://github.com/Microsoft/ApplicationInsights-JS/blob/master/API-reference.md#config) include:</span></span>

    // Send telemetry immediately without batching.
    // Remember tooremove this when no longer required, as it
    // can affect browser performance.
    enableDebug: boolean,

    // Don't log browser exceptions.
    disableExceptionTracking: boolean,

    // Don't log ajax calls.
    disableAjaxTracking: boolean,

    // Limit number of Ajax calls logged, tooreduce traffic.
    maxAjaxCallsPerView: 10, // default is 500

    // Time page load up tooexecution of first trackPageView().
    overridePageViewDuration: boolean,

    // Set these dynamically for an authenticated user.
    appUserId: string,
    accountId: string,



## <span data-ttu-id="dc6b0-145"><a name="run"></a>Uruchamianie aplikacji</span><span class="sxs-lookup"><span data-stu-id="dc6b0-145"><a name="run"></a>Run your app</span></span>
<span data-ttu-id="dc6b0-146">Uruchom aplikację sieci web i używać go podczas toogenerate telemetrii i zaczekaj kilka sekund.</span><span class="sxs-lookup"><span data-stu-id="dc6b0-146">Run your web app, use it a while toogenerate telemetry, and wait a few seconds.</span></span> <span data-ttu-id="dc6b0-147">Możesz uruchomić go za pomocą hello **F5** klucza na komputerze deweloperskim lub opublikować go, pozwalając użytkownikom na odtwarzania z nim.</span><span class="sxs-lookup"><span data-stu-id="dc6b0-147">You can either run it using hello **F5** key on your development machine, or publish it and let users play with it.</span></span>

<span data-ttu-id="dc6b0-148">Toocheck hello telemetrii, że aplikacja sieci web wysyła tooApplication szczegółowe informacje, należy użyć narzędzia debugowania w przeglądarce (**F12** w wielu przeglądarkach).</span><span class="sxs-lookup"><span data-stu-id="dc6b0-148">If you want toocheck hello telemetry that a web app is sending tooApplication Insights, use your browser's debugging tools (**F12** on many browsers).</span></span> <span data-ttu-id="dc6b0-149">Dane są wysyłane toodc.services.visualstudio.com.</span><span class="sxs-lookup"><span data-stu-id="dc6b0-149">Data is sent toodc.services.visualstudio.com.</span></span>

## <a name="explore-your-browser-performance-data"></a><span data-ttu-id="dc6b0-150">Eksplorowanie danych wydajności przeglądarki</span><span class="sxs-lookup"><span data-stu-id="dc6b0-150">Explore your browser performance data</span></span>
<span data-ttu-id="dc6b0-151">Otwórz hello tooshow bloku przeglądarki zagregowane dane dotyczące wydajności z przeglądarki użytkownika.</span><span class="sxs-lookup"><span data-stu-id="dc6b0-151">Open hello Browser blade tooshow aggregated performance data from your users' browsers.</span></span>

![W witrynie portal.azure.com otwórz zasób swojej aplikacji, a następnie kliknij kolejno opcje Ustawienia, Przeglądarki](./media/app-insights-javascript/03.png)

<span data-ttu-id="dc6b0-153">*Jeszcze nie ma danych? Kliknij przycisk **Odśwież** u góry hello hello strony. Nadal nic? Zobacz [Rozwiązywanie problemów ](app-insights-troubleshoot-faq.md).*</span><span class="sxs-lookup"><span data-stu-id="dc6b0-153">*No data yet? Click **Refresh** at hello top of hello page. Still nothing? See [Troubleshooting](app-insights-troubleshoot-faq.md).*</span></span>

<span data-ttu-id="dc6b0-154">Blok przeglądarki Hello jest [bloku Eksploratora metryk](app-insights-metrics-explorer.md) filtry ustawień wstępnych i wyboru wykresu.</span><span class="sxs-lookup"><span data-stu-id="dc6b0-154">hello Browser blade is a [Metrics Explorer blade](app-insights-metrics-explorer.md) with preset filters and chart selections.</span></span> <span data-ttu-id="dc6b0-155">Zakres czasu hello, filtrów i konfiguracji wykresu można edytować, jeśli i zapisać wynik hello jako ulubioną.</span><span class="sxs-lookup"><span data-stu-id="dc6b0-155">You can edit hello time range, filters, and chart configuration if you want, and save hello result as a favorite.</span></span> <span data-ttu-id="dc6b0-156">Kliknij przycisk **przywrócić ustawienia domyślne** tooget toohello wstecz oryginalną konfigurację bloku.</span><span class="sxs-lookup"><span data-stu-id="dc6b0-156">Click **Restore defaults** tooget back toohello original blade configuration.</span></span>

## <a name="page-load-performance"></a><span data-ttu-id="dc6b0-157">Wydajność ładowania strony</span><span class="sxs-lookup"><span data-stu-id="dc6b0-157">Page load performance</span></span>
<span data-ttu-id="dc6b0-158">Na powitania top jest segmentowanych wykres czasy ładowania stron.</span><span class="sxs-lookup"><span data-stu-id="dc6b0-158">At hello top is a segmented chart of page load times.</span></span> <span data-ttu-id="dc6b0-159">Witaj całkowita wysokość wykresu hello reprezentuje hello Średni czas tooload i wyświetlania stron z aplikacji w przeglądarce użytkownika.</span><span class="sxs-lookup"><span data-stu-id="dc6b0-159">hello total height of hello chart represents hello average time tooload and display pages from your app in your users' browsers.</span></span> <span data-ttu-id="dc6b0-160">Witaj czas jest mierzony z, gdy przeglądarka hello wysyła hello początkowe żądanie HTTP do wszystkich synchroniczne obciążenia, który zdarzenia są przetwarzane w tym układ i uruchamianie skryptów.</span><span class="sxs-lookup"><span data-stu-id="dc6b0-160">hello time is measured from when hello browser sends hello initial HTTP request until all synchronous load events have been processed, including layout and running scripts.</span></span> <span data-ttu-id="dc6b0-161">Nie obejmuje zadań asynchronicznych, takich jak ładowanie składników Web Part z wywołań AJAX.</span><span class="sxs-lookup"><span data-stu-id="dc6b0-161">It doesn't include asynchronous tasks such as loading web parts from AJAX calls.</span></span>

<span data-ttu-id="dc6b0-162">Wykres Hello segmenty czas ładowania strony całkowita hello na powitania [standardowe czasy określone przez W3C](http://www.w3.org/TR/navigation-timing/#processing-model).</span><span class="sxs-lookup"><span data-stu-id="dc6b0-162">hello chart segments hello total page load time into hello [standard timings defined by W3C](http://www.w3.org/TR/navigation-timing/#processing-model).</span></span> 

![](./media/app-insights-javascript/08-client-split.png)

<span data-ttu-id="dc6b0-163">Należy pamiętać, że hello *połączeń sieciowych* czasu jest niższa niż oczekujesz może często, ponieważ jest to wartość średnia za pośrednictwem wszystkich żądań z serwera toohello przeglądarki hello.</span><span class="sxs-lookup"><span data-stu-id="dc6b0-163">Note that hello *network connect* time is often lower than you might expect, because it's an average over all requests from hello browser toohello server.</span></span> <span data-ttu-id="dc6b0-164">Wiele żądań poszczególnych ma czas połączenia, 0, ponieważ istnieje już serwer toohello aktywnego połączenia.</span><span class="sxs-lookup"><span data-stu-id="dc6b0-164">Many individual requests have a connect time of 0 because there is already an active connection toohello server.</span></span>

### <a name="slow-loading"></a><span data-ttu-id="dc6b0-165">Powolne ładowanie?</span><span class="sxs-lookup"><span data-stu-id="dc6b0-165">Slow loading?</span></span>
<span data-ttu-id="dc6b0-166">Powolne ładowanie stron jest głównym powodem niezadowolenia użytkowników.</span><span class="sxs-lookup"><span data-stu-id="dc6b0-166">Slow page loads are a major source of dissatisfaction for your users.</span></span> <span data-ttu-id="dc6b0-167">Jeśli hello wykres wskazuje powolne obciążeń, jest łatwe toodo przeanalizować diagnostycznych.</span><span class="sxs-lookup"><span data-stu-id="dc6b0-167">If hello chart indicates slow page loads, it's easy toodo some diagnostic research.</span></span>

<span data-ttu-id="dc6b0-168">Witaj wykres pokazuje średnią hello ładunków strona w aplikacji.</span><span class="sxs-lookup"><span data-stu-id="dc6b0-168">hello chart shows hello average of all page loads in your app.</span></span> <span data-ttu-id="dc6b0-169">toosee, jeśli hello problem jest ograniczone tooparticular stron, wygląd dalsze dół hello bloku, w przypadku, gdy istnieje siatka segmentowanych przez adres URL strony:</span><span class="sxs-lookup"><span data-stu-id="dc6b0-169">toosee if hello problem is confined tooparticular pages, look further down hello blade, where there's a grid segmented by page URL:</span></span>

![](./media/app-insights-javascript/09-page-perf.png)

<span data-ttu-id="dc6b0-170">Zwróć uwagę, liczba widoku strony hello i odchylenie standardowe.</span><span class="sxs-lookup"><span data-stu-id="dc6b0-170">Notice hello page view count and standard deviation.</span></span> <span data-ttu-id="dc6b0-171">Jeśli liczba stron hello jest bardzo niskie, następnie hello problem nie ma wpływu na użytkowników znacznie.</span><span class="sxs-lookup"><span data-stu-id="dc6b0-171">If hello page count is very low, then hello issue isn't affecting users much.</span></span> <span data-ttu-id="dc6b0-172">Wysoka odchylenie standardowe (średnia porównywalne toohello, sam) wskazuje wiele odmiany między pojedynczych pomiarów.</span><span class="sxs-lookup"><span data-stu-id="dc6b0-172">A high standard deviation (comparable toohello average itself) indicates a lot of variation between individual measurements.</span></span>

<span data-ttu-id="dc6b0-173">**Wyświetl szczegóły dla jednego adresu URL i jednej strony.**</span><span class="sxs-lookup"><span data-stu-id="dc6b0-173">**Zoom in on one URL and one page view.**</span></span> <span data-ttu-id="dc6b0-174">Kliknij pozycję wszystkie strony toosee Nazwa bloku przeglądarki wykresy filtrowane toothat tylko adres URL; a następnie na wystąpienie strony widoku.</span><span class="sxs-lookup"><span data-stu-id="dc6b0-174">Click any page name toosee a blade of browser charts filtered just toothat URL; and then on an instance of a page view.</span></span>

![](./media/app-insights-javascript/35.png)

<span data-ttu-id="dc6b0-175">Kliknij przycisk `...` pełną listę właściwości dla tego zdarzenia, lub zbadać wywołania Ajax hello oraz powiązanych zdarzeń.</span><span class="sxs-lookup"><span data-stu-id="dc6b0-175">Click `...` for a full list of properties for that event, or inspect hello Ajax calls and related events.</span></span> <span data-ttu-id="dc6b0-176">Powolnych połączeń Ajax hello mają wpływ na ogólne strony czas ładowania, jeśli są one synchronicznego.</span><span class="sxs-lookup"><span data-stu-id="dc6b0-176">Slow Ajax calls affect hello overall page load time if they are synchronous.</span></span> <span data-ttu-id="dc6b0-177">Powiązane zdarzenia zawierają żądań serwera na powitania tego samego adresu URL (Jeśli po skonfigurowaniu usługi Application Insights na serwerze sieci web).</span><span class="sxs-lookup"><span data-stu-id="dc6b0-177">Related events include server requests for hello same URL (if you've set up Application Insights on your web server).</span></span>

<span data-ttu-id="dc6b0-178">**Wydajność stron w czasie.**</span><span class="sxs-lookup"><span data-stu-id="dc6b0-178">**Page performance over time.**</span></span> <span data-ttu-id="dc6b0-179">W bloku przeglądarki hello zmienić hello czas ładowania strony widoku siatki w toosee wykresu wiersza, jeśli wystąpiły pików w określonym czasie:</span><span class="sxs-lookup"><span data-stu-id="dc6b0-179">Back at hello Browsers blade, change hello Page View Load Time grid into a line chart toosee if there were peaks at particular times:</span></span>

![Kliknij nagłówek hello hello siatki i wybierz nowy typ wykresu](./media/app-insights-javascript/10-page-perf-area.png)

<span data-ttu-id="dc6b0-181">**Segmentowanie według innych wymiarów.**</span><span class="sxs-lookup"><span data-stu-id="dc6b0-181">**Segment by other dimensions.**</span></span> <span data-ttu-id="dc6b0-182">Może być stron sieci są wolniejszej tooload w określonej lokalizacji przeglądarki, system operacyjny klienta lub użytkownika?</span><span class="sxs-lookup"><span data-stu-id="dc6b0-182">Maybe your pages are slower tooload on a particular browser, client OS, or user locality?</span></span> <span data-ttu-id="dc6b0-183">Dodaj nowy wykres i eksperymentować hello **Group by** wymiaru.</span><span class="sxs-lookup"><span data-stu-id="dc6b0-183">Add a new chart and experiment with hello **Group-by** dimension.</span></span>

![](./media/app-insights-javascript/21.png)

## <a name="ajax-performance"></a><span data-ttu-id="dc6b0-184">Wydajność wywołań AJAX</span><span class="sxs-lookup"><span data-stu-id="dc6b0-184">AJAX Performance</span></span>
<span data-ttu-id="dc6b0-185">Upewnij się. że dowolne wywołania AJAX na stronach sieci Web działają poprawnie.</span><span class="sxs-lookup"><span data-stu-id="dc6b0-185">Make sure any AJAX calls in your web pages are performing well.</span></span> <span data-ttu-id="dc6b0-186">Są często używane toofill elementów na stronie asynchronicznie.</span><span class="sxs-lookup"><span data-stu-id="dc6b0-186">They are often used toofill parts of your page asynchronously.</span></span> <span data-ttu-id="dc6b0-187">Mimo że hello całej strony może załadować natychmiast, użytkowników można można frustracji przez uruchomieniem w części sieci web puste oczekiwanie na dane tooappear w nich.</span><span class="sxs-lookup"><span data-stu-id="dc6b0-187">Although hello overall page might load promptly, your users could be frustrated by staring at blank web parts, waiting for data tooappear in them.</span></span>

<span data-ttu-id="dc6b0-188">Wywołania AJAX ze strony sieci web są wyświetlane w bloku przeglądarki hello jako zależności.</span><span class="sxs-lookup"><span data-stu-id="dc6b0-188">AJAX calls made from your web page are shown on hello Browsers blade as dependencies.</span></span>

<span data-ttu-id="dc6b0-189">Istnieją wykresy podsumowań w górnej części bloku hello hello:</span><span class="sxs-lookup"><span data-stu-id="dc6b0-189">There are summary charts in hello upper part of hello blade:</span></span>

![](./media/app-insights-javascript/31.png)

<span data-ttu-id="dc6b0-190">a poniżej szczegółowe siatki:</span><span class="sxs-lookup"><span data-stu-id="dc6b0-190">and detailed grids lower down:</span></span>

![](./media/app-insights-javascript/33.png)

<span data-ttu-id="dc6b0-191">Klikaj poszczególne wiersze, aby uzyskać szczegółowe informacje.</span><span class="sxs-lookup"><span data-stu-id="dc6b0-191">Click any row for specific details.</span></span>

> [!NOTE]
> <span data-ttu-id="dc6b0-192">Jeśli usuniesz hello filtru przeglądarki w bloku hello zarówno serwera, jak i zależności AJAX zostaną uwzględnione w wykresach.</span><span class="sxs-lookup"><span data-stu-id="dc6b0-192">If you delete hello Browsers filter on hello blade, both server and AJAX dependencies are included in these charts.</span></span> <span data-ttu-id="dc6b0-193">Kliknij przycisk Przywróć domyślne filtrów hello tooreconfigure.</span><span class="sxs-lookup"><span data-stu-id="dc6b0-193">Click Restore Defaults tooreconfigure hello filter.</span></span>
> 
> 

<span data-ttu-id="dc6b0-194">**toodrill do wywołania Ajax nie powiodło się** przewiń w dół siatki błędów zależności toohello, a następnie kliknij określonych wystąpień toosee wiersza.</span><span class="sxs-lookup"><span data-stu-id="dc6b0-194">**toodrill into failed Ajax calls** scroll down toohello Dependency failures grid, and then click a row toosee specific instances.</span></span>

![](./media/app-insights-javascript/37.png)


<span data-ttu-id="dc6b0-195">Kliknij przycisk `...` dla hello pełne dane telemetryczne dla wywołania Ajax.</span><span class="sxs-lookup"><span data-stu-id="dc6b0-195">Click `...` for hello full telemetry for an Ajax call.</span></span>

### <a name="no-ajax-calls-reported"></a><span data-ttu-id="dc6b0-196">Brak zgłoszonych wywołań Ajax?</span><span class="sxs-lookup"><span data-stu-id="dc6b0-196">No Ajax calls reported?</span></span>
<span data-ttu-id="dc6b0-197">Wywołania AJAX obejmują wszystkie wywołania HTTP/HTTPS ze skryptu hello strony sieci web.</span><span class="sxs-lookup"><span data-stu-id="dc6b0-197">Ajax calls include any HTTP/HTTPS  calls made from hello script of your web page.</span></span> <span data-ttu-id="dc6b0-198">Jeśli nie widzisz ich zgłoszone, Sprawdź ten fragment kodu hello nie ustawia hello `disableAjaxTracking` lub `maxAjaxCallsPerView` [parametry](https://github.com/Microsoft/ApplicationInsights-JS/blob/master/API-reference.md#config).</span><span class="sxs-lookup"><span data-stu-id="dc6b0-198">If you don't see them reported, check that hello code snippet doesn't set hello `disableAjaxTracking` or `maxAjaxCallsPerView` [parameters](https://github.com/Microsoft/ApplicationInsights-JS/blob/master/API-reference.md#config).</span></span>

## <a name="browser-exceptions"></a><span data-ttu-id="dc6b0-199">Wyjątki przeglądarki</span><span class="sxs-lookup"><span data-stu-id="dc6b0-199">Browser exceptions</span></span>
<span data-ttu-id="dc6b0-200">W bloku przeglądarki hello jest wykres podsumowania wyjątki oraz siatka typów wyjątków dalsze dół hello bloku.</span><span class="sxs-lookup"><span data-stu-id="dc6b0-200">On hello Browsers blade, there's an exceptions summary chart, and a grid of exception types further down hello blade.</span></span>

![](./media/app-insights-javascript/39.png)

<span data-ttu-id="dc6b0-201">Jeśli nie widzisz zgłaszane wyjątki przeglądarki, Sprawdź ten fragment kodu hello nie ustawia hello `disableExceptionTracking` [parametru](https://github.com/Microsoft/ApplicationInsights-JS/blob/master/API-reference.md#config).</span><span class="sxs-lookup"><span data-stu-id="dc6b0-201">If you don't see browser exceptions reported, check that hello code snippet doesn't set hello `disableExceptionTracking` [parameter](https://github.com/Microsoft/ApplicationInsights-JS/blob/master/API-reference.md#config).</span></span>

## <a name="inspect-individual-page-view-events"></a><span data-ttu-id="dc6b0-202">Badanie zdarzeń wyświetlania pojedynczej strony</span><span class="sxs-lookup"><span data-stu-id="dc6b0-202">Inspect individual page view events</span></span>

<span data-ttu-id="dc6b0-203">Zazwyczaj telemetria wyświetlania strony jest analizowana w usłudze Application Insights i widoczne są jedynie raporty zbiorcze, uśrednione dla wszystkich użytkowników.</span><span class="sxs-lookup"><span data-stu-id="dc6b0-203">Usually page view telemetry is analyzed by Application Insights and you see only cumulative reports, averaged over all your users.</span></span> <span data-ttu-id="dc6b0-204">Jednak na potrzeby debugowania, możesz zapoznać się ze zdarzeniami wyświetlania pojedynczej strony.</span><span class="sxs-lookup"><span data-stu-id="dc6b0-204">But for debugging purposes, you can also look at individual page view events.</span></span>

<span data-ttu-id="dc6b0-205">W bloku diagnostycznych wyszukiwania hello ustawić filtry tooPage widoku.</span><span class="sxs-lookup"><span data-stu-id="dc6b0-205">In hello Diagnostic Search blade, set Filters tooPage View.</span></span>

![](./media/app-insights-javascript/12-search-pages.png)

<span data-ttu-id="dc6b0-206">Wybierz wszystkie zdarzenia toosee więcej szczegółów.</span><span class="sxs-lookup"><span data-stu-id="dc6b0-206">Select any event toosee more detail.</span></span> <span data-ttu-id="dc6b0-207">Na stronie szczegółów hello kliknij toosee "..." jeszcze więcej szczegółów.</span><span class="sxs-lookup"><span data-stu-id="dc6b0-207">In hello details page, click "..." toosee even more detail.</span></span>

> [!NOTE]
> <span data-ttu-id="dc6b0-208">Jeśli używasz [wyszukiwania](app-insights-diagnostic-search.md), powiadomienia, że masz toomatch całe wyrazy: "Formacje o programie" i "informacje" nie odpowiada "Temat".</span><span class="sxs-lookup"><span data-stu-id="dc6b0-208">If you use [Search](app-insights-diagnostic-search.md), notice that you have toomatch whole words: "Abou" and "bout" do not match "About".</span></span>
> 
> 

<span data-ttu-id="dc6b0-209">Można również użyć hello zaawansowanych [języka zapytań usługi Analiza dzienników](https://docs.microsoft.com/azure/application-insights/app-insights-analytics-tour#browser-timings-table) toosearch wyświetleń strony.</span><span class="sxs-lookup"><span data-stu-id="dc6b0-209">You can also use hello powerful [Log Analytics query language](https://docs.microsoft.com/azure/application-insights/app-insights-analytics-tour#browser-timings-table) toosearch page views.</span></span>

### <a name="page-view-properties"></a><span data-ttu-id="dc6b0-210">Właściwości wyświetlania stron</span><span class="sxs-lookup"><span data-stu-id="dc6b0-210">Page view properties</span></span>
* <span data-ttu-id="dc6b0-211">**Czas trwania wyświetlania stron**</span><span class="sxs-lookup"><span data-stu-id="dc6b0-211">**Page view duration**</span></span> 
  
  * <span data-ttu-id="dc6b0-212">Domyślnie program hello czasu zajmuje tooload hello strony, toofull żądania klienta obciążenia (w tym plików pomocniczych, ale z wyłączeniem zadania asynchroniczne, takie jak wywołania Ajax).</span><span class="sxs-lookup"><span data-stu-id="dc6b0-212">By default, hello time it takes tooload hello page, from client request toofull load (including auxiliary files but excluding asynchronous tasks such as Ajax calls).</span></span> 
  * <span data-ttu-id="dc6b0-213">Jeśli ustawisz `overridePageViewDuration` w hello [konfigurację strony](#detailed-configuration), najpierw hello odstęp między tooexecution żądania klienta z hello `trackPageView`.</span><span class="sxs-lookup"><span data-stu-id="dc6b0-213">If you set `overridePageViewDuration` in hello [page configuration](#detailed-configuration), hello interval between client request tooexecution of hello first `trackPageView`.</span></span> <span data-ttu-id="dc6b0-214">Jeśli trackPageView jest przenoszony z położenia zwykle po zainicjowaniu hello hello skryptu, zostaną one zastosowane inną wartość.</span><span class="sxs-lookup"><span data-stu-id="dc6b0-214">If you moved trackPageView from its usual position after hello initialization of hello script, it will reflect a different value.</span></span>
  * <span data-ttu-id="dc6b0-215">Jeśli `overridePageViewDuration` jest ustawiony, a czas trwania argument znajduje się w hello `trackPageView()` wywołań, a następnie zamiast niego jest używana wartość argumentu hello.</span><span class="sxs-lookup"><span data-stu-id="dc6b0-215">If `overridePageViewDuration` is set and a duration argument is provided in hello `trackPageView()` call, then hello argument value is used instead.</span></span> 

## <a name="custom-page-counts"></a><span data-ttu-id="dc6b0-216">Niestandardowe liczby stron</span><span class="sxs-lookup"><span data-stu-id="dc6b0-216">Custom page counts</span></span>
<span data-ttu-id="dc6b0-217">Domyślnie liczba stron występuje zawsze, gdy ładuje nowej strony do przeglądarki klienta hello.</span><span class="sxs-lookup"><span data-stu-id="dc6b0-217">By default, a page count occurs each time a new page loads into hello client browser.</span></span>  <span data-ttu-id="dc6b0-218">Ale może być toocount dodatkowa strona widoków.</span><span class="sxs-lookup"><span data-stu-id="dc6b0-218">But you might want toocount additional page views.</span></span> <span data-ttu-id="dc6b0-219">Na przykład strona może wyświetlać zawartość w kartach i mają toocount strony, gdy użytkownik hello przełącza karty.</span><span class="sxs-lookup"><span data-stu-id="dc6b0-219">For example, a page might display its content in tabs and you want toocount a page when hello user switches tabs.</span></span> <span data-ttu-id="dc6b0-220">Lub kodu JavaScript na stronie powitania może załadować nowej zawartości bez zmiany adresu URL hello przeglądarki.</span><span class="sxs-lookup"><span data-stu-id="dc6b0-220">Or JavaScript code in hello page might load new content without changing hello browser's URL.</span></span>

<span data-ttu-id="dc6b0-221">Wstawianie wywołania języka JavaScript takie punkcie odpowiednie hello w kodzie klienta:</span><span class="sxs-lookup"><span data-stu-id="dc6b0-221">Insert a JavaScript call like this at hello appropriate point in your client code:</span></span>

    appInsights.trackPageView(myPageName);

<span data-ttu-id="dc6b0-222">Nazwa strony Hello może zawierać hello same znaki jako adres URL, ale cokolwiek po "#" lub "?" zostanie zignorowany.</span><span class="sxs-lookup"><span data-stu-id="dc6b0-222">hello page name can contain hello same characters as a URL, but anything after "#" or "?" is ignored.</span></span>

## <a name="usage-tracking"></a><span data-ttu-id="dc6b0-223">Śledzenie użycia</span><span class="sxs-lookup"><span data-stu-id="dc6b0-223">Usage tracking</span></span>
<span data-ttu-id="dc6b0-224">Chcesz toofind limit użytkowników czy z aplikacją?</span><span class="sxs-lookup"><span data-stu-id="dc6b0-224">Want toofind out what your users do with your app?</span></span>

* [<span data-ttu-id="dc6b0-225">Informacje na temat śledzenia użycia</span><span class="sxs-lookup"><span data-stu-id="dc6b0-225">Learn about usage tracking</span></span>](app-insights-web-track-usage.md)
* <span data-ttu-id="dc6b0-226">[Informacje o interfejsie API do monitorowania niestandardowych zdarzeń i metryk](app-insights-api-custom-events-metrics.md).</span><span class="sxs-lookup"><span data-stu-id="dc6b0-226">[Learn about custom events and metrics API](app-insights-api-custom-events-metrics.md).</span></span>

## <span data-ttu-id="dc6b0-227"><a name="video"></a> Wideo</span><span class="sxs-lookup"><span data-stu-id="dc6b0-227"><a name="video"></a> Video</span></span>


> [!VIDEO https://channel9.msdn.com/events/Connect/2016/100/player]



## <span data-ttu-id="dc6b0-228"><a name="next"></a> Następne kroki</span><span class="sxs-lookup"><span data-stu-id="dc6b0-228"><a name="next"></a> Next steps</span></span>
* [<span data-ttu-id="dc6b0-229">Śledzenie użycia</span><span class="sxs-lookup"><span data-stu-id="dc6b0-229">Track usage</span></span>](app-insights-web-track-usage.md)
* [<span data-ttu-id="dc6b0-230">Niestandardowe zdarzenia i metryki</span><span class="sxs-lookup"><span data-stu-id="dc6b0-230">Custom events and metrics</span></span>](app-insights-api-custom-events-metrics.md)
* [<span data-ttu-id="dc6b0-231">Tworzenie — pomiar— nauka</span><span class="sxs-lookup"><span data-stu-id="dc6b0-231">Build-measure-learn</span></span>](app-insights-web-track-usage.md)

