---
title: "Usługa Azure Application Insights dla aplikacji sieci Web w języku JavaScript | Microsoft Docs"
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
ms.openlocfilehash: 4e8a77e3644bb726d1b8e2050dab61893ccfa3c9
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/18/2017
---
# <a name="application-insights-for-web-pages"></a><span data-ttu-id="9d9ce-104">Usługa Application Insights dla stron sieci Web</span><span class="sxs-lookup"><span data-stu-id="9d9ce-104">Application Insights for web pages</span></span>
<span data-ttu-id="9d9ce-105">Poznaj wydajność i użycie strony sieci Web lub aplikacji.</span><span class="sxs-lookup"><span data-stu-id="9d9ce-105">Find out about the performance and usage of your web page or app.</span></span> <span data-ttu-id="9d9ce-106">Jeśli dodasz usługę [Application Insights](app-insights-overview.md) do skryptu strony, uzyskasz chronometraż ładowania strony i wywołań AJAX, liczniki i szczegóły dotyczące wyjątków przeglądarki i błędów AJAX, a także liczniki użytkowników i sesji.</span><span class="sxs-lookup"><span data-stu-id="9d9ce-106">If you add [Application Insights](app-insights-overview.md) to your page script, you get timings of page loads and AJAX calls, counts and details of browser exceptions and AJAX failures, as well as users and session counts.</span></span> <span data-ttu-id="9d9ce-107">Wszystkie te dane możesz rozdzielić według strony, systemu operacyjnego klienta i wersji przeglądarki, lokalizacji geograficznej i innych wymiarów.</span><span class="sxs-lookup"><span data-stu-id="9d9ce-107">All these can be segmented by page, client OS and browser version, geo location, and other dimensions.</span></span> <span data-ttu-id="9d9ce-108">Możesz ustawić alerty związane z liczbami błędów lub powolnym ładowaniem strony.</span><span class="sxs-lookup"><span data-stu-id="9d9ce-108">You can set alerts on failure counts or slow page loading.</span></span> <span data-ttu-id="9d9ce-109">A wstawiając wywołania śledzenia w kodzie JavaScript, możesz śledzić sposób użycia różnych funkcji aplikacji strony sieci Web.</span><span class="sxs-lookup"><span data-stu-id="9d9ce-109">And by inserting trace calls in your JavaScript code, you can track how the different features of your web page application are used.</span></span>

<span data-ttu-id="9d9ce-110">Usługi Application Insights można używać z dowolnymi stronami sieci Web — wystarczy dodać krótki fragment kodu JavaScript.</span><span class="sxs-lookup"><span data-stu-id="9d9ce-110">Application Insights can be used with any web pages - you just add a short piece of JavaScript.</span></span> <span data-ttu-id="9d9ce-111">Jeśli Twoja usługa sieci Web jest zaprogramowana w technologii [Java](app-insights-java-get-started.md) lub [ASP.NET](app-insights-asp-net.md), możesz zintegrować telemetrię pochodzącą z serwera i klientów.</span><span class="sxs-lookup"><span data-stu-id="9d9ce-111">If your web service is [Java](app-insights-java-get-started.md) or [ASP.NET](app-insights-asp-net.md), you can integrate telemetry from your server and clients.</span></span>

![W witrynie portal.azure.com otwórz zasób swojej aplikacji, a następnie kliknij pozycję Przeglądarka](./media/app-insights-javascript/03.png)

<span data-ttu-id="9d9ce-113">Potrzebna jest subskrypcja platformy [Microsoft Azure](https://azure.com).</span><span class="sxs-lookup"><span data-stu-id="9d9ce-113">You need a subscription to [Microsoft Azure](https://azure.com).</span></span> <span data-ttu-id="9d9ce-114">Jeśli zespół ma subskrypcję organizacyjną, poproś właściciela, aby dodał do niej Twoje konto Microsoft.</span><span class="sxs-lookup"><span data-stu-id="9d9ce-114">If your team has an organizational subscription, ask the owner to add your Microsoft Account to it.</span></span> <span data-ttu-id="9d9ce-115">Tworząc strony i używając ich na małą skalę, nie poniesiesz żadnych kosztów.</span><span class="sxs-lookup"><span data-stu-id="9d9ce-115">Development and small-scale use won't cost anything.</span></span>

## <a name="set-up-application-insights-for-your-web-page"></a><span data-ttu-id="9d9ce-116">Konfigurowanie usługi Application Insights dla strony sieci Web</span><span class="sxs-lookup"><span data-stu-id="9d9ce-116">Set up Application Insights for your web page</span></span>
<span data-ttu-id="9d9ce-117">Dodaj fragment kodu modułu ładującego do stron sieci Web w opisany poniżej sposób.</span><span class="sxs-lookup"><span data-stu-id="9d9ce-117">Add the loader code snippet to your web pages, as follows.</span></span>

### <a name="open-or-create-application-insights-resource"></a><span data-ttu-id="9d9ce-118">Otwieranie lub tworzenie zasobu usługi Application Insights</span><span class="sxs-lookup"><span data-stu-id="9d9ce-118">Open or create Application Insights resource</span></span>
<span data-ttu-id="9d9ce-119">Zasób usługi Application Insights jest miejscem, w którym będą wyświetlane dane dotyczące wydajności i użycia strony.</span><span class="sxs-lookup"><span data-stu-id="9d9ce-119">The Application Insights resource is where data about your page's performance and usage is displayed.</span></span> 

<span data-ttu-id="9d9ce-120">Zaloguj się do [portalu Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="9d9ce-120">Sign into [Azure portal](https://portal.azure.com).</span></span>

<span data-ttu-id="9d9ce-121">Jeśli skonfigurowano już monitorowanie po stronie serwera aplikacji, zasób jest już utworzony:</span><span class="sxs-lookup"><span data-stu-id="9d9ce-121">If you already set up monitoring for the server side of your app, you already have a resource:</span></span>

![Wybierz kolejno opcje Przeglądaj, Usługi dla deweloperów, Application Insights.](./media/app-insights-javascript/01-find.png)

<span data-ttu-id="9d9ce-123">Jeśli nie ma zasobu, utwórz go:</span><span class="sxs-lookup"><span data-stu-id="9d9ce-123">If you don't have one, create it:</span></span>

![Wybierz kolejno opcje Nowe, Usługi dla deweloperów, Application Insights.](./media/app-insights-javascript/01-create.png)

<span data-ttu-id="9d9ce-125">*Już masz pytania?*</span><span class="sxs-lookup"><span data-stu-id="9d9ce-125">*Questions already?*</span></span> <span data-ttu-id="9d9ce-126">[Więcej informacji na temat tworzenia zasobu](app-insights-create-new-resource.md).</span><span class="sxs-lookup"><span data-stu-id="9d9ce-126">[More about creating a resource](app-insights-create-new-resource.md).</span></span>

### <a name="add-the-sdk-script-to-your-app-or-web-pages"></a><span data-ttu-id="9d9ce-127">Dodawanie skryptu zestawu SDK do aplikacji lub stron sieci Web</span><span class="sxs-lookup"><span data-stu-id="9d9ce-127">Add the SDK script to your app or web pages</span></span>
<span data-ttu-id="9d9ce-128">Ze strony Szybki start pobierz skrypt dla stron sieci Web:</span><span class="sxs-lookup"><span data-stu-id="9d9ce-128">In Quick Start, get the script for web pages:</span></span>

![W bloku przeglądu aplikacji wybierz kolejno opcje Szybki start, Pobierz kod umożliwiający monitorowanie stron sieci Web.](./media/app-insights-javascript/02-monitor-web-page.png)

<span data-ttu-id="9d9ce-131">Wstaw skrypt tuż przed tagiem `</head>` na każdej stronie, którą chcesz śledzić. Jeśli witryna ma stronę wzorcową, możesz umieścić skrypt na tej stronie.</span><span class="sxs-lookup"><span data-stu-id="9d9ce-131">Insert the script just before the `</head>` tag of every page you want to track. If your website has a master page, you can put the script there.</span></span> <span data-ttu-id="9d9ce-132">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="9d9ce-132">For example:</span></span>

* <span data-ttu-id="9d9ce-133">W projekcie ASP.NET MVC możesz umieścić go w pliku `View\Shared\_Layout.cshtml`</span><span class="sxs-lookup"><span data-stu-id="9d9ce-133">In an ASP.NET MVC project, you'd put it in `View\Shared\_Layout.cshtml`</span></span>
* <span data-ttu-id="9d9ce-134">W przypadku witryny programu SharePoint w panelu sterowania otwórz plik [Ustawienia witryny / Strona wzorcowa](app-insights-sharepoint.md).</span><span class="sxs-lookup"><span data-stu-id="9d9ce-134">In a SharePoint site, on the control panel, open [Site Settings / Master Page](app-insights-sharepoint.md).</span></span>

<span data-ttu-id="9d9ce-135">Skrypt zawiera klucz instrumentacji, który kieruje dane do odpowiedniego zasobu usługi Application Insights.</span><span class="sxs-lookup"><span data-stu-id="9d9ce-135">The script contains the instrumentation key that directs the data to your Application Insights resource.</span></span> 

<span data-ttu-id="9d9ce-136">([Dokładniejsze objaśnienia dotyczące skryptu](http://apmtips.com/blog/2015/03/18/javascript-snippet-explained/)).</span><span class="sxs-lookup"><span data-stu-id="9d9ce-136">([Deeper explanation of the script.](http://apmtips.com/blog/2015/03/18/javascript-snippet-explained/))</span></span>

<span data-ttu-id="9d9ce-137">*(Jeśli używasz dobrze znanej struktury stron sieci Web, poszukaj adapterów usługi Application Insights. Takim adapterem jest na przykład [moduł AngularJS](http://ngmodules.org/modules/angular-appinsights)).*</span><span class="sxs-lookup"><span data-stu-id="9d9ce-137">*(If you're using a well-known web page framework, look around for Application Insights adaptors. For example, there's [an AngularJS module](http://ngmodules.org/modules/angular-appinsights).)*</span></span>

## <a name="detailed-configuration"></a><span data-ttu-id="9d9ce-138">Konfiguracja szczegółowa</span><span class="sxs-lookup"><span data-stu-id="9d9ce-138">Detailed configuration</span></span>
<span data-ttu-id="9d9ce-139">Istnieje kilka [parametrów](https://github.com/Microsoft/ApplicationInsights-JS/blob/master/API-reference.md#config), które można ustawić, chociaż w większości przypadków nie jest to potrzebne.</span><span class="sxs-lookup"><span data-stu-id="9d9ce-139">There are several [parameters](https://github.com/Microsoft/ApplicationInsights-JS/blob/master/API-reference.md#config) you can set, though in most cases, you shouldn't need to.</span></span> <span data-ttu-id="9d9ce-140">Na przykład można wyłączyć zgłaszanie wywołań Ajax lub ograniczyć liczbę tych wywołań zgłaszanych na wyświetlenie strony (w celu zmniejszenia ruchu).</span><span class="sxs-lookup"><span data-stu-id="9d9ce-140">For example, you can disable or limit the number of Ajax calls reported per page view (to reduce traffic).</span></span> <span data-ttu-id="9d9ce-141">Można także ustawić tryb debugowania, aby dane telemetrii były szybciej przesyłane przez potok, a nie przekazywane w trybie wsadowym.</span><span class="sxs-lookup"><span data-stu-id="9d9ce-141">Or you can set debug mode to have telemetry move rapidly through the pipeline without being batched.</span></span>

<span data-ttu-id="9d9ce-142">Aby ustawić te parametry, poszukaj tego wiersza we fragmencie kodu i dodaj po nim więcej elementów rozdzielonych przecinkami:</span><span class="sxs-lookup"><span data-stu-id="9d9ce-142">To set these parameters, look for this line in the code snippet, and add more comma-separated items after it:</span></span>

    })({
      instrumentationKey: "..."
      // Insert here
    });

<span data-ttu-id="9d9ce-143">[Dostępne parametry](https://github.com/Microsoft/ApplicationInsights-JS/blob/master/API-reference.md#config) obejmują:</span><span class="sxs-lookup"><span data-stu-id="9d9ce-143">The [available parameters](https://github.com/Microsoft/ApplicationInsights-JS/blob/master/API-reference.md#config) include:</span></span>

    // Send telemetry immediately without batching.
    // Remember to remove this when no longer required, as it
    // can affect browser performance.
    enableDebug: boolean,

    // Don't log browser exceptions.
    disableExceptionTracking: boolean,

    // Don't log ajax calls.
    disableAjaxTracking: boolean,

    // Limit number of Ajax calls logged, to reduce traffic.
    maxAjaxCallsPerView: 10, // default is 500

    // Time page load up to execution of first trackPageView().
    overridePageViewDuration: boolean,

    // Set these dynamically for an authenticated user.
    appUserId: string,
    accountId: string,



## <span data-ttu-id="9d9ce-144"><a name="run"></a>Uruchamianie aplikacji</span><span class="sxs-lookup"><span data-stu-id="9d9ce-144"><a name="run"></a>Run your app</span></span>
<span data-ttu-id="9d9ce-145">Uruchom aplikację sieci Web, używaj jej przez pewien czas, aby wygenerować dane telemetryczne, i odczekaj kilka sekund.</span><span class="sxs-lookup"><span data-stu-id="9d9ce-145">Run your web app, use it a while to generate telemetry, and wait a few seconds.</span></span> <span data-ttu-id="9d9ce-146">Aplikację możesz uruchomić za pomocą klawisza **F5** na maszynie deweloperskiej lub opublikować ją i pozwolić na korzystanie z niej przez użytkowników.</span><span class="sxs-lookup"><span data-stu-id="9d9ce-146">You can either run it using the **F5** key on your development machine, or publish it and let users play with it.</span></span>

<span data-ttu-id="9d9ce-147">Jeśli chcesz sprawdzić telemetrię, którą aplikacja sieci Web wysyła do usługi Application Insights, użyj narzędzi debugowania w przeglądarce (**F12** w wielu przeglądarkach).</span><span class="sxs-lookup"><span data-stu-id="9d9ce-147">If you want to check the telemetry that a web app is sending to Application Insights, use your browser's debugging tools (**F12** on many browsers).</span></span> <span data-ttu-id="9d9ce-148">Dane są przesyłane do witryny dc.services.visualstudio.com.</span><span class="sxs-lookup"><span data-stu-id="9d9ce-148">Data is sent to dc.services.visualstudio.com.</span></span>

## <a name="explore-your-browser-performance-data"></a><span data-ttu-id="9d9ce-149">Eksplorowanie danych wydajności przeglądarki</span><span class="sxs-lookup"><span data-stu-id="9d9ce-149">Explore your browser performance data</span></span>
<span data-ttu-id="9d9ce-150">Otwórz blok Przeglądarka, aby wyświetlić agregowane dane wydajności z przeglądarek użytkowników.</span><span class="sxs-lookup"><span data-stu-id="9d9ce-150">Open the Browser blade to show aggregated performance data from your users' browsers.</span></span>

![W witrynie portal.azure.com otwórz zasób swojej aplikacji, a następnie kliknij kolejno opcje Ustawienia, Przeglądarki](./media/app-insights-javascript/03.png)

<span data-ttu-id="9d9ce-152">*Jeszcze nie ma danych? Kliknij przycisk **Odśwież** w górnej części strony. Nadal nic? Zobacz [Rozwiązywanie problemów ](app-insights-troubleshoot-faq.md).*</span><span class="sxs-lookup"><span data-stu-id="9d9ce-152">*No data yet? Click **Refresh** at the top of the page. Still nothing? See [Troubleshooting](app-insights-troubleshoot-faq.md).*</span></span>

<span data-ttu-id="9d9ce-153">Blok Przeglądarka jest [blokiem Eksploratora metryk](app-insights-metrics-explorer.md) z wstępnie ustawionymi filtrami i wybranymi wykresami.</span><span class="sxs-lookup"><span data-stu-id="9d9ce-153">The Browser blade is a [Metrics Explorer blade](app-insights-metrics-explorer.md) with preset filters and chart selections.</span></span> <span data-ttu-id="9d9ce-154">Jeśli chcesz, możesz edytować przedział czasu, filtry i konfiguracje wykresów, a następnie zapisać wynik jako ulubiony.</span><span class="sxs-lookup"><span data-stu-id="9d9ce-154">You can edit the time range, filters, and chart configuration if you want, and save the result as a favorite.</span></span> <span data-ttu-id="9d9ce-155">Kliknij przycisk **Przywróć domyślne**, aby wrócić do oryginalnej konfiguracji bloku.</span><span class="sxs-lookup"><span data-stu-id="9d9ce-155">Click **Restore defaults** to get back to the original blade configuration.</span></span>

## <a name="page-load-performance"></a><span data-ttu-id="9d9ce-156">Wydajność ładowania strony</span><span class="sxs-lookup"><span data-stu-id="9d9ce-156">Page load performance</span></span>
<span data-ttu-id="9d9ce-157">U góry znajduje się segmentowany wykres czasów ładowania strony.</span><span class="sxs-lookup"><span data-stu-id="9d9ce-157">At the top is a segmented chart of page load times.</span></span> <span data-ttu-id="9d9ce-158">Całkowita wysokość wykresu reprezentuje średni czas ładowania oraz wyświetlania stron z aplikacji w przeglądarkach użytkowników.</span><span class="sxs-lookup"><span data-stu-id="9d9ce-158">The total height of the chart represents the average time to load and display pages from your app in your users' browsers.</span></span> <span data-ttu-id="9d9ce-159">Czas jest mierzony od momentu wysłania z przeglądarki początkowego żądania HTTP do momentu przetworzenia wszystkich synchronicznych zdarzeń ładowania, wraz z układem i uruchamianiem skryptów.</span><span class="sxs-lookup"><span data-stu-id="9d9ce-159">The time is measured from when the browser sends the initial HTTP request until all synchronous load events have been processed, including layout and running scripts.</span></span> <span data-ttu-id="9d9ce-160">Nie obejmuje zadań asynchronicznych, takich jak ładowanie składników Web Part z wywołań AJAX.</span><span class="sxs-lookup"><span data-stu-id="9d9ce-160">It doesn't include asynchronous tasks such as loading web parts from AJAX calls.</span></span>

<span data-ttu-id="9d9ce-161">Na wykresie całkowity czas ładowania strony jest podzielony na segmenty obejmujące [standardowe chronometraże zdefiniowane przez organizację W3C](http://www.w3.org/TR/navigation-timing/#processing-model).</span><span class="sxs-lookup"><span data-stu-id="9d9ce-161">The chart segments the total page load time into the [standard timings defined by W3C](http://www.w3.org/TR/navigation-timing/#processing-model).</span></span> 

![](./media/app-insights-javascript/08-client-split.png)

<span data-ttu-id="9d9ce-162">Zauważ, że czas *nawiązywania połączenia sieciowego* często jest krótszy niż spodziewany, ponieważ jest średnią dla wszystkich żądań z przeglądarki do serwera.</span><span class="sxs-lookup"><span data-stu-id="9d9ce-162">Note that the *network connect* time is often lower than you might expect, because it's an average over all requests from the browser to the server.</span></span> <span data-ttu-id="9d9ce-163">Wiele indywidualnych żądań ma czas nawiązywania połączenia równy 0, ponieważ połączenie z serwerem jest już aktywne.</span><span class="sxs-lookup"><span data-stu-id="9d9ce-163">Many individual requests have a connect time of 0 because there is already an active connection to the server.</span></span>

### <a name="slow-loading"></a><span data-ttu-id="9d9ce-164">Powolne ładowanie?</span><span class="sxs-lookup"><span data-stu-id="9d9ce-164">Slow loading?</span></span>
<span data-ttu-id="9d9ce-165">Powolne ładowanie stron jest głównym powodem niezadowolenia użytkowników.</span><span class="sxs-lookup"><span data-stu-id="9d9ce-165">Slow page loads are a major source of dissatisfaction for your users.</span></span> <span data-ttu-id="9d9ce-166">Jeśli wykres wskazuje powolne ładowanie stron, łatwo można wykonać badania diagnostyczne.</span><span class="sxs-lookup"><span data-stu-id="9d9ce-166">If the chart indicates slow page loads, it's easy to do some diagnostic research.</span></span>

<span data-ttu-id="9d9ce-167">Wykres ten przedstawia średnią dla wszystkich operacji ładowania stron w aplikacji.</span><span class="sxs-lookup"><span data-stu-id="9d9ce-167">The chart shows the average of all page loads in your app.</span></span> <span data-ttu-id="9d9ce-168">Aby sprawdzić, czy problem jest ograniczony do konkretnych stron, spójrz dalej na dół bloku, gdzie znajduje się siatka posegmentowana według adresów URL stron:</span><span class="sxs-lookup"><span data-stu-id="9d9ce-168">To see if the problem is confined to particular pages, look further down the blade, where there's a grid segmented by page URL:</span></span>

![](./media/app-insights-javascript/09-page-perf.png)

<span data-ttu-id="9d9ce-169">Zwróć uwagę na liczbę wyświetleń stron i odchylenie standardowe.</span><span class="sxs-lookup"><span data-stu-id="9d9ce-169">Notice the page view count and standard deviation.</span></span> <span data-ttu-id="9d9ce-170">Jeśli liczba wyświetleń stron jest bardzo niska, problem nie ma znacznego wpływu na użytkowników.</span><span class="sxs-lookup"><span data-stu-id="9d9ce-170">If the page count is very low, then the issue isn't affecting users much.</span></span> <span data-ttu-id="9d9ce-171">Wysokie odchylenie standardowe (porównywalne do samej średniej) wskazuje na znaczne różnice między poszczególnymi pomiarami.</span><span class="sxs-lookup"><span data-stu-id="9d9ce-171">A high standard deviation (comparable to the average itself) indicates a lot of variation between individual measurements.</span></span>

<span data-ttu-id="9d9ce-172">**Wyświetl szczegóły dla jednego adresu URL i jednej strony.**</span><span class="sxs-lookup"><span data-stu-id="9d9ce-172">**Zoom in on one URL and one page view.**</span></span> <span data-ttu-id="9d9ce-173">Kliknij nazwę dowolnej strony, aby zobaczyć blok wykresów dotyczących przeglądarki filtrowanych według tego adresu URL, a następnie kliknij wystąpienie wyświetlenia strony.</span><span class="sxs-lookup"><span data-stu-id="9d9ce-173">Click any page name to see a blade of browser charts filtered just to that URL; and then on an instance of a page view.</span></span>

![](./media/app-insights-javascript/35.png)

<span data-ttu-id="9d9ce-174">Kliknij przycisk `...`, aby uzyskać pełną listę właściwości tego zdarzenia, lub zbadaj wywołania Ajax i powiązane z nimi zdarzenia.</span><span class="sxs-lookup"><span data-stu-id="9d9ce-174">Click `...` for a full list of properties for that event, or inspect the Ajax calls and related events.</span></span> <span data-ttu-id="9d9ce-175">Powolne wywołania Ajax, jeśli są synchroniczne, wpływają na ogólny czas ładowania strony.</span><span class="sxs-lookup"><span data-stu-id="9d9ce-175">Slow Ajax calls affect the overall page load time if they are synchronous.</span></span> <span data-ttu-id="9d9ce-176">Powiązane zdarzenia obejmują żądania serwera dotyczące tego samego adresu URL (jeśli skonfigurowano usługę Application Insights na serwerze sieci Web).</span><span class="sxs-lookup"><span data-stu-id="9d9ce-176">Related events include server requests for the same URL (if you've set up Application Insights on your web server).</span></span>

<span data-ttu-id="9d9ce-177">**Wydajność stron w czasie.**</span><span class="sxs-lookup"><span data-stu-id="9d9ce-177">**Page performance over time.**</span></span> <span data-ttu-id="9d9ce-178">Wróć do bloku Przeglądarki i zmień siatkę Wyświetlenie strony — czas ładowania na wykres liniowy, aby zobaczyć, czy wystąpiły wartości szczytowe w określonym czasie:</span><span class="sxs-lookup"><span data-stu-id="9d9ce-178">Back at the Browsers blade, change the Page View Load Time grid into a line chart to see if there were peaks at particular times:</span></span>

![Kliknij nagłówek siatki i wybierz nowy typ wykresu](./media/app-insights-javascript/10-page-perf-area.png)

<span data-ttu-id="9d9ce-180">**Segmentowanie według innych wymiarów.**</span><span class="sxs-lookup"><span data-stu-id="9d9ce-180">**Segment by other dimensions.**</span></span> <span data-ttu-id="9d9ce-181">Może strony są ładowane wolniej w konkretnej przeglądarce, systemie operacyjnym klienta lub lokalizacji użytkownika?</span><span class="sxs-lookup"><span data-stu-id="9d9ce-181">Maybe your pages are slower to load on a particular browser, client OS, or user locality?</span></span> <span data-ttu-id="9d9ce-182">Dodaj nowy wykres i poeksperymentuj z operacją **Grupuj według** wymiaru.</span><span class="sxs-lookup"><span data-stu-id="9d9ce-182">Add a new chart and experiment with the **Group-by** dimension.</span></span>

![](./media/app-insights-javascript/21.png)

## <a name="ajax-performance"></a><span data-ttu-id="9d9ce-183">Wydajność wywołań AJAX</span><span class="sxs-lookup"><span data-stu-id="9d9ce-183">AJAX Performance</span></span>
<span data-ttu-id="9d9ce-184">Upewnij się. że dowolne wywołania AJAX na stronach sieci Web działają poprawnie.</span><span class="sxs-lookup"><span data-stu-id="9d9ce-184">Make sure any AJAX calls in your web pages are performing well.</span></span> <span data-ttu-id="9d9ce-185">Często są one używane do asynchronicznego wypełniania elementów na stronie.</span><span class="sxs-lookup"><span data-stu-id="9d9ce-185">They are often used to fill parts of your page asynchronously.</span></span> <span data-ttu-id="9d9ce-186">Chociaż cała strona może ładować się szybko, użytkownicy mogą być sfrustrowani, jeśli muszą wpatrywać się w puste składniki Web Part w oczekiwaniu na wyświetlenie w nich danych.</span><span class="sxs-lookup"><span data-stu-id="9d9ce-186">Although the overall page might load promptly, your users could be frustrated by staring at blank web parts, waiting for data to appear in them.</span></span>

<span data-ttu-id="9d9ce-187">Wywołania AJAX ze strony sieci Web są wyświetlane w bloku Przeglądarki jako zależności.</span><span class="sxs-lookup"><span data-stu-id="9d9ce-187">AJAX calls made from your web page are shown on the Browsers blade as dependencies.</span></span>

<span data-ttu-id="9d9ce-188">W górnej części bloku znajdują się wykresy podsumowujące:</span><span class="sxs-lookup"><span data-stu-id="9d9ce-188">There are summary charts in the upper part of the blade:</span></span>

![](./media/app-insights-javascript/31.png)

<span data-ttu-id="9d9ce-189">a poniżej szczegółowe siatki:</span><span class="sxs-lookup"><span data-stu-id="9d9ce-189">and detailed grids lower down:</span></span>

![](./media/app-insights-javascript/33.png)

<span data-ttu-id="9d9ce-190">Klikaj poszczególne wiersze, aby uzyskać szczegółowe informacje.</span><span class="sxs-lookup"><span data-stu-id="9d9ce-190">Click any row for specific details.</span></span>

> [!NOTE]
> <span data-ttu-id="9d9ce-191">Jeśli usuniesz filtr Przeglądarki w bloku, zarówno serwer, jak i zależności AJAX zostaną uwzględnione na tych wykresach.</span><span class="sxs-lookup"><span data-stu-id="9d9ce-191">If you delete the Browsers filter on the blade, both server and AJAX dependencies are included in these charts.</span></span> <span data-ttu-id="9d9ce-192">Kliknij przycisk Przywróć domyślne, aby ponownie skonfigurować filtr.</span><span class="sxs-lookup"><span data-stu-id="9d9ce-192">Click Restore Defaults to reconfigure the filter.</span></span>
> 
> 

<span data-ttu-id="9d9ce-193">**Aby przejść do szczegółów niepowodzeń wywołań Ajax** przewiń w dół do siatki błędów zależności, a następnie kliknij wiersz, aby wyświetlić określone wystąpienia.</span><span class="sxs-lookup"><span data-stu-id="9d9ce-193">**To drill into failed Ajax calls** scroll down to the Dependency failures grid, and then click a row to see specific instances.</span></span>

![](./media/app-insights-javascript/37.png)


<span data-ttu-id="9d9ce-194">Kliknij przycisk `...`, aby uzyskać pełną telemetrię wywołania Ajax.</span><span class="sxs-lookup"><span data-stu-id="9d9ce-194">Click `...` for the full telemetry for an Ajax call.</span></span>

### <a name="no-ajax-calls-reported"></a><span data-ttu-id="9d9ce-195">Brak zgłoszonych wywołań Ajax?</span><span class="sxs-lookup"><span data-stu-id="9d9ce-195">No Ajax calls reported?</span></span>
<span data-ttu-id="9d9ce-196">Wywołania AJAX obejmują dowolne wywołania HTTP/HTTPS dokonywane ze skryptu na stronie sieci Web.</span><span class="sxs-lookup"><span data-stu-id="9d9ce-196">Ajax calls include any HTTP/HTTPS  calls made from the script of your web page.</span></span> <span data-ttu-id="9d9ce-197">Jeśli nie widzisz ich w raporcie, sprawdź, czy we fragmencie kodu nie zostały ustawione [parametry](https://github.com/Microsoft/ApplicationInsights-JS/blob/master/API-reference.md#config) `disableAjaxTracking` lub `maxAjaxCallsPerView`.</span><span class="sxs-lookup"><span data-stu-id="9d9ce-197">If you don't see them reported, check that the code snippet doesn't set the `disableAjaxTracking` or `maxAjaxCallsPerView` [parameters](https://github.com/Microsoft/ApplicationInsights-JS/blob/master/API-reference.md#config).</span></span>

## <a name="browser-exceptions"></a><span data-ttu-id="9d9ce-198">Wyjątki przeglądarki</span><span class="sxs-lookup"><span data-stu-id="9d9ce-198">Browser exceptions</span></span>
<span data-ttu-id="9d9ce-199">W bloku Przeglądarki znajduje się wykres podsumowania wyjątków, a poniżej niego siatka typów wyjątków.</span><span class="sxs-lookup"><span data-stu-id="9d9ce-199">On the Browsers blade, there's an exceptions summary chart, and a grid of exception types further down the blade.</span></span>

![](./media/app-insights-javascript/39.png)

<span data-ttu-id="9d9ce-200">Jeśli nie widzisz wyjątków przeglądarki w raporcie, sprawdź, czy we fragmencie kodu nie został ustawiony [parametr](https://github.com/Microsoft/ApplicationInsights-JS/blob/master/API-reference.md#config) `disableExceptionTracking`.</span><span class="sxs-lookup"><span data-stu-id="9d9ce-200">If you don't see browser exceptions reported, check that the code snippet doesn't set the `disableExceptionTracking` [parameter](https://github.com/Microsoft/ApplicationInsights-JS/blob/master/API-reference.md#config).</span></span>

## <a name="inspect-individual-page-view-events"></a><span data-ttu-id="9d9ce-201">Badanie zdarzeń wyświetlania pojedynczej strony</span><span class="sxs-lookup"><span data-stu-id="9d9ce-201">Inspect individual page view events</span></span>

<span data-ttu-id="9d9ce-202">Zazwyczaj telemetria wyświetlania strony jest analizowana w usłudze Application Insights i widoczne są jedynie raporty zbiorcze, uśrednione dla wszystkich użytkowników.</span><span class="sxs-lookup"><span data-stu-id="9d9ce-202">Usually page view telemetry is analyzed by Application Insights and you see only cumulative reports, averaged over all your users.</span></span> <span data-ttu-id="9d9ce-203">Jednak na potrzeby debugowania, możesz zapoznać się ze zdarzeniami wyświetlania pojedynczej strony.</span><span class="sxs-lookup"><span data-stu-id="9d9ce-203">But for debugging purposes, you can also look at individual page view events.</span></span>

<span data-ttu-id="9d9ce-204">W bloku Wyszukiwanie diagnostyczne jako Filtry ustaw Wyświetlenie strony.</span><span class="sxs-lookup"><span data-stu-id="9d9ce-204">In the Diagnostic Search blade, set Filters to Page View.</span></span>

![](./media/app-insights-javascript/12-search-pages.png)

<span data-ttu-id="9d9ce-205">Wybierz dowolne zdarzenie, aby wyświetlić więcej szczegółów.</span><span class="sxs-lookup"><span data-stu-id="9d9ce-205">Select any event to see more detail.</span></span> <span data-ttu-id="9d9ce-206">Na stronie szczegółów kliknij przycisk „...”, aby wyświetlić jeszcze więcej szczegółów.</span><span class="sxs-lookup"><span data-stu-id="9d9ce-206">In the details page, click "..." to see even more detail.</span></span>

> [!NOTE]
> <span data-ttu-id="9d9ce-207">Jeśli używasz pola [Wyszukiwanie](app-insights-diagnostic-search.md), zauważ, że musisz dopasowywać całe wyrazy: wpisy „Abou” i „bout” nie odpowiadają słowu „About”.</span><span class="sxs-lookup"><span data-stu-id="9d9ce-207">If you use [Search](app-insights-diagnostic-search.md), notice that you have to match whole words: "Abou" and "bout" do not match "About".</span></span>
> 
> 

<span data-ttu-id="9d9ce-208">Można także użyć zaawansowanego [języka zapytań usługi Log Analytics](https://docs.microsoft.com/azure/application-insights/app-insights-analytics-tour#browser-timings-table) do przeszukiwania wyświetleń stron.</span><span class="sxs-lookup"><span data-stu-id="9d9ce-208">You can also use the powerful [Log Analytics query language](https://docs.microsoft.com/azure/application-insights/app-insights-analytics-tour#browser-timings-table) to search page views.</span></span>

### <a name="page-view-properties"></a><span data-ttu-id="9d9ce-209">Właściwości wyświetlania stron</span><span class="sxs-lookup"><span data-stu-id="9d9ce-209">Page view properties</span></span>
* <span data-ttu-id="9d9ce-210">**Czas trwania wyświetlania stron**</span><span class="sxs-lookup"><span data-stu-id="9d9ce-210">**Page view duration**</span></span> 
  
  * <span data-ttu-id="9d9ce-211">Domyślnie czas potrzebny do załadowania strony, od żądania klienta do pełnego załadowania (w tym plików pomocniczych, ale z wyłączeniem zadań asynchronicznych, takich jak wywołania Ajax).</span><span class="sxs-lookup"><span data-stu-id="9d9ce-211">By default, the time it takes to load the page, from client request to full load (including auxiliary files but excluding asynchronous tasks such as Ajax calls).</span></span> 
  * <span data-ttu-id="9d9ce-212">Jeśli ustawisz parametr `overridePageViewDuration` w [konfiguracji strony](#detailed-configuration), czas ten jest liczony od żądania klienta do wykonania pierwszego wywołania `trackPageView`.</span><span class="sxs-lookup"><span data-stu-id="9d9ce-212">If you set `overridePageViewDuration` in the [page configuration](#detailed-configuration), the interval between client request to execution of the first `trackPageView`.</span></span> <span data-ttu-id="9d9ce-213">W przypadku przeniesienia wywołania trackPageView ze zwykłej pozycji po zainicjowaniu skryptu ta wartość będzie inna.</span><span class="sxs-lookup"><span data-stu-id="9d9ce-213">If you moved trackPageView from its usual position after the initialization of the script, it will reflect a different value.</span></span>
  * <span data-ttu-id="9d9ce-214">Jeśli parametr `overridePageViewDuration` jest ustawiony, a argument czasu trwania jest podany w wywołaniu `trackPageView()`, zastępczo zostanie użyta wartość argumentu.</span><span class="sxs-lookup"><span data-stu-id="9d9ce-214">If `overridePageViewDuration` is set and a duration argument is provided in the `trackPageView()` call, then the argument value is used instead.</span></span> 

## <a name="custom-page-counts"></a><span data-ttu-id="9d9ce-215">Niestandardowe liczby stron</span><span class="sxs-lookup"><span data-stu-id="9d9ce-215">Custom page counts</span></span>
<span data-ttu-id="9d9ce-216">Domyślnie strony są zliczane przy każdym załadowaniu nowej strony do przeglądarki klienta.</span><span class="sxs-lookup"><span data-stu-id="9d9ce-216">By default, a page count occurs each time a new page loads into the client browser.</span></span>  <span data-ttu-id="9d9ce-217">Jednak warto zliczać dodatkowe wyświetlenia stron.</span><span class="sxs-lookup"><span data-stu-id="9d9ce-217">But you might want to count additional page views.</span></span> <span data-ttu-id="9d9ce-218">Na przykład zawartość strony może być wyświetlana na kartach i warto zliczać strony, gdy użytkownik zmienia karty.</span><span class="sxs-lookup"><span data-stu-id="9d9ce-218">For example, a page might display its content in tabs and you want to count a page when the user switches tabs.</span></span> <span data-ttu-id="9d9ce-219">Ponadto kod JavaScript na stronie może ładować nową zawartość bez zmiany adresu URL w przeglądarce.</span><span class="sxs-lookup"><span data-stu-id="9d9ce-219">Or JavaScript code in the page might load new content without changing the browser's URL.</span></span>

<span data-ttu-id="9d9ce-220">Wstaw takie wywołanie JavaScript we właściwym miejscu w kodzie klienta:</span><span class="sxs-lookup"><span data-stu-id="9d9ce-220">Insert a JavaScript call like this at the appropriate point in your client code:</span></span>

    appInsights.trackPageView(myPageName);

<span data-ttu-id="9d9ce-221">Nazwa strony może zawierać te same znaki co adres URL, ale wszystko po znakach „#” i „?” będzie ignorowane.</span><span class="sxs-lookup"><span data-stu-id="9d9ce-221">The page name can contain the same characters as a URL, but anything after "#" or "?" is ignored.</span></span>

## <a name="usage-tracking"></a><span data-ttu-id="9d9ce-222">Śledzenie użycia</span><span class="sxs-lookup"><span data-stu-id="9d9ce-222">Usage tracking</span></span>
<span data-ttu-id="9d9ce-223">Chcesz dowiedzieć się, w jaki sposób użytkownicy korzystają z aplikacji?</span><span class="sxs-lookup"><span data-stu-id="9d9ce-223">Want to find out what your users do with your app?</span></span>

* [<span data-ttu-id="9d9ce-224">Informacje na temat śledzenia użycia</span><span class="sxs-lookup"><span data-stu-id="9d9ce-224">Learn about usage tracking</span></span>](app-insights-web-track-usage.md)
* <span data-ttu-id="9d9ce-225">[Informacje o interfejsie API do monitorowania niestandardowych zdarzeń i metryk](app-insights-api-custom-events-metrics.md).</span><span class="sxs-lookup"><span data-stu-id="9d9ce-225">[Learn about custom events and metrics API](app-insights-api-custom-events-metrics.md).</span></span>

## <span data-ttu-id="9d9ce-226"><a name="video"></a> Wideo</span><span class="sxs-lookup"><span data-stu-id="9d9ce-226"><a name="video"></a> Video</span></span>


> [!VIDEO https://channel9.msdn.com/events/Connect/2016/100/player]



## <span data-ttu-id="9d9ce-227"><a name="next"></a> Następne kroki</span><span class="sxs-lookup"><span data-stu-id="9d9ce-227"><a name="next"></a> Next steps</span></span>
* [<span data-ttu-id="9d9ce-228">Śledzenie użycia</span><span class="sxs-lookup"><span data-stu-id="9d9ce-228">Track usage</span></span>](app-insights-web-track-usage.md)
* [<span data-ttu-id="9d9ce-229">Niestandardowe zdarzenia i metryki</span><span class="sxs-lookup"><span data-stu-id="9d9ce-229">Custom events and metrics</span></span>](app-insights-api-custom-events-metrics.md)
* [<span data-ttu-id="9d9ce-230">Tworzenie — pomiar— nauka</span><span class="sxs-lookup"><span data-stu-id="9d9ce-230">Build-measure-learn</span></span>](app-insights-web-track-usage.md)

