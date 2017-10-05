---
title: "Monitorowanie kondycji i użycia za pomocą usługi Application Insights aplikacji"
description: "Wprowadzenie do usługi Application Insights. Analizowanie użycia, dostępności i wydajności lokalnej lub w aplikacji Microsoft Azure."
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.assetid: 40650472-e860-4c1b-a589-9956245df307
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 11/25/2015
ms.author: bwren
ms.openlocfilehash: 5b7b1f4a53cd2624ee8e2ab684ba6ba63252674f
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/18/2017
---
# <a name="monitor-performance-in-web-applications"></a><span data-ttu-id="30ed3-104">Monitorowanie wydajności w aplikacjach sieci Web</span><span class="sxs-lookup"><span data-stu-id="30ed3-104">Monitor performance in web applications</span></span>


<span data-ttu-id="30ed3-105">Upewnij się, że aplikacja działa optymalnie i Dowiedz się szybko o zakończą się niepowodzeniem.</span><span class="sxs-lookup"><span data-stu-id="30ed3-105">Make sure your application is performing well, and find out quickly about any failures.</span></span> <span data-ttu-id="30ed3-106">[Usługa Application Insights] [ start] informujące o wszelkich problemów z wydajnością oraz wyjątków i ułatwiają znajdowanie i diagnozowanie głównej przyczyny.</span><span class="sxs-lookup"><span data-stu-id="30ed3-106">[Application Insights][start] will tell you about any performance issues and exceptions, and help you find and diagnose the root causes.</span></span>

<span data-ttu-id="30ed3-107">Usługa Application Insights można monitorować aplikacji sieci web zarówno Java, jak i platformy ASP.NET i usługi, usługi WCF.</span><span class="sxs-lookup"><span data-stu-id="30ed3-107">Application Insights can monitor both Java and ASP.NET web applications and services, WCF services.</span></span> <span data-ttu-id="30ed3-108">Mogą to być obsługiwana lokalnie, w przypadku maszyn wirtualnych lub jako witryny sieci Web Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="30ed3-108">They can be hosted on-premises, on virtual machines, or as Microsoft Azure websites.</span></span> 

<span data-ttu-id="30ed3-109">Po stronie klienta usługi Application Insights może zająć telemetrii ze stron sieci web i różnych urządzeniami, takimi jak systemy iOS, Android i aplikacji ze Sklepu Windows.</span><span class="sxs-lookup"><span data-stu-id="30ed3-109">On the client side, Application Insights can take telemetry from web pages and a wide variety of devices including iOS, Android and Windows Store apps.</span></span>

>[!Note]
> <span data-ttu-id="30ed3-110">Wprowadzono nowe środowisko dostępne do znajdowania powolne wykonywania stron w aplikacji sieci web.</span><span class="sxs-lookup"><span data-stu-id="30ed3-110">We have made a new experience available for finding slow performing pages in your web application.</span></span> <span data-ttu-id="30ed3-111">Jeśli nie masz do niego dostęp, ją włączyć, konfigurując opcje podglądu z [bloku Podgląd](app-insights-previews.md).</span><span class="sxs-lookup"><span data-stu-id="30ed3-111">If you don't have access to it, enable it by configuring your preview options with the [Preview blade](app-insights-previews.md).</span></span> <span data-ttu-id="30ed3-112">Przeczytaj informacje o nowe środowisko w [Znajdowanie i rozwiązywanie problemów wąskich gardeł wydajności interakcyjne postępowaniu wydajności](#Find-and-fix-performance-bottlenecks-with-an-interactive-Performance-investigation).</span><span class="sxs-lookup"><span data-stu-id="30ed3-112">Read about this new experience in [Find and fix performance bottlenecks with the interactive Performance investigation](#Find-and-fix-performance-bottlenecks-with-an-interactive-Performance-investigation).</span></span>

## <span data-ttu-id="30ed3-113"><a name="setup"></a>Konfigurowanie monitorowania wydajności</span><span class="sxs-lookup"><span data-stu-id="30ed3-113"><a name="setup"></a>Set up performance monitoring</span></span>
<span data-ttu-id="30ed3-114">Jeśli nie zostały jeszcze dodane usługi Application Insights do projektu (Jeśli nie ma ApplicationInsights.config), wybierz jedną z tych sposobów na rozpoczęcie pracy:</span><span class="sxs-lookup"><span data-stu-id="30ed3-114">If you haven't yet added Application Insights to your project (that is, if it doesn't have ApplicationInsights.config), choose one of these ways to get started:</span></span>

* [<span data-ttu-id="30ed3-115">Aplikacje sieci web ASP.NET</span><span class="sxs-lookup"><span data-stu-id="30ed3-115">ASP.NET web apps</span></span>](app-insights-asp-net.md)
  * [<span data-ttu-id="30ed3-116">Dodaj monitorowanie wyjątków</span><span class="sxs-lookup"><span data-stu-id="30ed3-116">Add exception monitoring</span></span>](app-insights-asp-net-exceptions.md)
  * [<span data-ttu-id="30ed3-117">Dodaj monitorowanie zależności</span><span class="sxs-lookup"><span data-stu-id="30ed3-117">Add dependency monitoring</span></span>](app-insights-monitor-performance-live-website-now.md)
* [<span data-ttu-id="30ed3-118">Aplikacje sieci web J2EE</span><span class="sxs-lookup"><span data-stu-id="30ed3-118">J2EE web apps</span></span>](app-insights-java-get-started.md)
  * [<span data-ttu-id="30ed3-119">Dodaj monitorowanie zależności</span><span class="sxs-lookup"><span data-stu-id="30ed3-119">Add dependency monitoring</span></span>](app-insights-java-agent.md)

## <span data-ttu-id="30ed3-120"><a name="view"></a>Eksploracja metryki wydajności</span><span class="sxs-lookup"><span data-stu-id="30ed3-120"><a name="view"></a>Exploring performance metrics</span></span>
<span data-ttu-id="30ed3-121">W [portalu Azure](https://portal.azure.com), przejdź do zasobu usługi Application Insights, skonfigurowanego dla aplikacji.</span><span class="sxs-lookup"><span data-stu-id="30ed3-121">In [the Azure portal](https://portal.azure.com), browse to the Application Insights resource that you set up for your application.</span></span> <span data-ttu-id="30ed3-122">Blok omówienie przedstawia dane wydajności podstawowe:</span><span class="sxs-lookup"><span data-stu-id="30ed3-122">The overview blade shows basic performance data:</span></span>

<span data-ttu-id="30ed3-123">Kliknij przycisk dowolnego wykresu, aby zobaczyć więcej szczegółów, a także aby zobaczyć wyniki przez dłuższy czas.</span><span class="sxs-lookup"><span data-stu-id="30ed3-123">Click any chart to see more detail, and to see results for a longer period.</span></span> <span data-ttu-id="30ed3-124">Na przykład kliknij Kafelek żądania, a następnie wybierz zakres czasu:</span><span class="sxs-lookup"><span data-stu-id="30ed3-124">For example, click the Requests tile and then select a time range:</span></span>

![Kliknij, aby większej ilości danych, a następnie wybierz zakres czasu](./media/app-insights-web-monitor-performance/appinsights-48metrics.png)

<span data-ttu-id="30ed3-126">Kliknij wykres, aby wybrać metryki, które wyświetla, lub Dodaj nowy wykres i wybrać jego metryki:</span><span class="sxs-lookup"><span data-stu-id="30ed3-126">Click a chart to choose which metrics it displays, or add a new chart and select its metrics:</span></span>

![Kliknij wykres, aby wybrać metryki](./media/app-insights-web-monitor-performance/appinsights-61perfchoices.png)

> [!NOTE]
> <span data-ttu-id="30ed3-128">**Usuń zaznaczenie pola wyboru wszystkie metryki** oglądanie pełnej zaznaczenia, która jest dostępna.</span><span class="sxs-lookup"><span data-stu-id="30ed3-128">**Uncheck all the metrics** to see the full selection that is available.</span></span> <span data-ttu-id="30ed3-129">Metryki należą do grup; Po wybraniu dowolnego członka grupy są wyświetlane tylko innych członków tej grupy.</span><span class="sxs-lookup"><span data-stu-id="30ed3-129">The metrics fall into groups; when any member of a group is selected, only the other members of that group appear.</span></span>

## <span data-ttu-id="30ed3-130"><a name="metrics"></a>Jaki jest średnią wszystkich?</span><span class="sxs-lookup"><span data-stu-id="30ed3-130"><a name="metrics"></a>What does it all mean?</span></span> <span data-ttu-id="30ed3-131">Kafelki wydajności i raporty</span><span class="sxs-lookup"><span data-stu-id="30ed3-131">Performance tiles and reports</span></span>
<span data-ttu-id="30ed3-132">Istnieją różne metryki wydajności, które można pobrać.</span><span class="sxs-lookup"><span data-stu-id="30ed3-132">There are various performance metrics you can get.</span></span> <span data-ttu-id="30ed3-133">Zacznijmy od tych, które są wyświetlane domyślnie w bloku aplikacji.</span><span class="sxs-lookup"><span data-stu-id="30ed3-133">Let's start with those that appear by default on the application blade.</span></span>

### <a name="requests"></a><span data-ttu-id="30ed3-134">Żądania</span><span class="sxs-lookup"><span data-stu-id="30ed3-134">Requests</span></span>
<span data-ttu-id="30ed3-135">Liczba żądań HTTP odebrane w określonym przedziale czasu.</span><span class="sxs-lookup"><span data-stu-id="30ed3-135">The number of HTTP requests received in a specified period.</span></span> <span data-ttu-id="30ed3-136">Porównaj te wyniki na inne raporty, aby wyświetlić zachowania aplikacji jako obciążenia zmienia się.</span><span class="sxs-lookup"><span data-stu-id="30ed3-136">Compare this with the results on other reports to see how your app behaves as the load varies.</span></span>

<span data-ttu-id="30ed3-137">Żądania HTTP obejmują wszystkie żądania GET lub POST dla stron, danych i obrazów.</span><span class="sxs-lookup"><span data-stu-id="30ed3-137">HTTP requests include all GET or POST requests for pages, data, and images.</span></span>

<span data-ttu-id="30ed3-138">Kliknij Kafelek, aby uzyskać liczby dla określonych adresów URL.</span><span class="sxs-lookup"><span data-stu-id="30ed3-138">Click on the tile to get counts for specific URLs.</span></span>

### <a name="average-response-time"></a><span data-ttu-id="30ed3-139">Średni czas odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="30ed3-139">Average response time</span></span>
<span data-ttu-id="30ed3-140">Mierzy czas między żądania sieci web wprowadzania aplikacji i odpowiedzi zostały zwrócone.</span><span class="sxs-lookup"><span data-stu-id="30ed3-140">Measures the time between a web request entering your application and the response being returned.</span></span>

<span data-ttu-id="30ed3-141">Punkty Pokaż, ruchomą średnią.</span><span class="sxs-lookup"><span data-stu-id="30ed3-141">The points show a moving average.</span></span> <span data-ttu-id="30ed3-142">Jeśli istnieje wiele żądań, mogą wystąpić, które odbiegają od średniej bez widocznych szczytu lub zanurzyć na wykresie.</span><span class="sxs-lookup"><span data-stu-id="30ed3-142">If there are a lot of requests, there might be some that deviate from the average without an obvious peak or dip in the graph.</span></span>

<span data-ttu-id="30ed3-143">Poszukaj nietypowe szczytów.</span><span class="sxs-lookup"><span data-stu-id="30ed3-143">Look for unusual peaks.</span></span> <span data-ttu-id="30ed3-144">Ogólnie rzecz biorąc oczekiwany czas odpowiedzi wzrasta z wzrost żądania.</span><span class="sxs-lookup"><span data-stu-id="30ed3-144">In general, expect response time to rise with a rise in requests.</span></span> <span data-ttu-id="30ed3-145">W przypadku nieproporcjonalnie wzrostu aplikacji może być naciśnięcie limit zasobów, takie jak Procesor lub pojemność usługi, które są używane.</span><span class="sxs-lookup"><span data-stu-id="30ed3-145">If the rise is disproportionate, your app might be hitting a resource limit such as CPU or the capacity of a service it uses.</span></span>

<span data-ttu-id="30ed3-146">Kliknij Kafelek, aby pobrać razy dla określonych adresów URL.</span><span class="sxs-lookup"><span data-stu-id="30ed3-146">Click the tile to get times for specific URLs.</span></span>

![](./media/app-insights-web-monitor-performance/appinsights-42reqs.png)

### <a name="slowest-requests"></a><span data-ttu-id="30ed3-147">Najwolniejsze żądań</span><span class="sxs-lookup"><span data-stu-id="30ed3-147">Slowest requests</span></span>
![](./media/app-insights-web-monitor-performance/appinsights-44slowest.png)

<span data-ttu-id="30ed3-148">Pokazuje, które żądania może być konieczne dostrojenie wydajności.</span><span class="sxs-lookup"><span data-stu-id="30ed3-148">Shows which requests might need performance tuning.</span></span>

### <a name="failed-requests"></a><span data-ttu-id="30ed3-149">Żądań zakończonych niepowodzeniem</span><span class="sxs-lookup"><span data-stu-id="30ed3-149">Failed requests</span></span>
![](./media/app-insights-web-monitor-performance/appinsights-46failed.png)

<span data-ttu-id="30ed3-150">Liczba żądań, które zwrócił nieprzechwyconych wyjątków.</span><span class="sxs-lookup"><span data-stu-id="30ed3-150">A count of requests that threw uncaught exceptions.</span></span>

<span data-ttu-id="30ed3-151">Kliknij Kafelek, aby wyświetlić szczegóły określonych niepowodzeń, a następnie wybierz indywidualne żądanie, aby wyświetlić jego szczegóły.</span><span class="sxs-lookup"><span data-stu-id="30ed3-151">Click the tile to see the details of specific failures, and select an individual request to see its detail.</span></span> 

<span data-ttu-id="30ed3-152">Tylko reprezentatywnej próbki błędów jest przechowywany dla poszczególnych kontroli.</span><span class="sxs-lookup"><span data-stu-id="30ed3-152">Only a representative sample of failures is retained for individual inspection.</span></span>

### <a name="other-metrics"></a><span data-ttu-id="30ed3-153">Innych metryk</span><span class="sxs-lookup"><span data-stu-id="30ed3-153">Other metrics</span></span>
<span data-ttu-id="30ed3-154">Aby zobaczyć, ustaw innych metryk można wyświetlać, kliknij wykres i usuń zaznaczenie opcji wszystkie metryki, aby wyświetlić dostępne pełnej.</span><span class="sxs-lookup"><span data-stu-id="30ed3-154">To see what other metrics you can display, click a graph, and then deselect all the metrics to see the full available set.</span></span> <span data-ttu-id="30ed3-155">Kliknij (i), aby zobaczyć wszystkie metryki definicji.</span><span class="sxs-lookup"><span data-stu-id="30ed3-155">Click (i) to see each metric's definition.</span></span>

![Odznacz wszystkie metryki, aby zobaczyć cały zestaw](./media/app-insights-web-monitor-performance/appinsights-62allchoices.png)

<span data-ttu-id="30ed3-157">Wybranie dowolnego Metryka wyłącza innych, które nie mogą występować w tym samym wykresie.</span><span class="sxs-lookup"><span data-stu-id="30ed3-157">Selecting any metric disables the others that can't appear on the same chart.</span></span>

## <a name="set-alerts"></a><span data-ttu-id="30ed3-158">Ustawianie alertów</span><span class="sxs-lookup"><span data-stu-id="30ed3-158">Set alerts</span></span>
<span data-ttu-id="30ed3-159">Aby otrzymywać powiadomienia pocztą e-mail o nietypowych wartościach dowolnej metryki, należy dodać alert.</span><span class="sxs-lookup"><span data-stu-id="30ed3-159">To be notified by email of unusual values of any metric, add an alert.</span></span> <span data-ttu-id="30ed3-160">Można wybrać do wysyłania wiadomości e-mail do administratorów, kont lub na adresy e-mail określone.</span><span class="sxs-lookup"><span data-stu-id="30ed3-160">You can choose either to send the email to the account administrators, or to specific email addresses.</span></span>

![](./media/app-insights-web-monitor-performance/appinsights-413setMetricAlert.png)

<span data-ttu-id="30ed3-161">Ustaw zasób przed inne właściwości.</span><span class="sxs-lookup"><span data-stu-id="30ed3-161">Set the resource before the other properties.</span></span> <span data-ttu-id="30ed3-162">Nie należy wybierać zasoby w teście sieci Web, aby ustawić alertów dla metryki wydajności i użycia.</span><span class="sxs-lookup"><span data-stu-id="30ed3-162">Don't choose the webtest resources if you want to set alerts on performance or usage metrics.</span></span>

<span data-ttu-id="30ed3-163">Należy zachować ostrożność, należy pamiętać, jednostki, w których użytkownik jest proszony o wprowadź wartość progu.</span><span class="sxs-lookup"><span data-stu-id="30ed3-163">Be careful to note the units in which you're asked to enter the threshold value.</span></span>

<span data-ttu-id="30ed3-164">*Przycisk Dodaj alertu nie jest widoczny.*</span><span class="sxs-lookup"><span data-stu-id="30ed3-164">*I don't see the Add Alert button.*</span></span> <span data-ttu-id="30ed3-165">-To jest grupa kont, do których masz dostęp tylko do odczytu?</span><span class="sxs-lookup"><span data-stu-id="30ed3-165">- Is this a group account to which you have read-only access?</span></span> <span data-ttu-id="30ed3-166">Skontaktuj się z administratorem konta.</span><span class="sxs-lookup"><span data-stu-id="30ed3-166">Check with the account administrator.</span></span>

## <span data-ttu-id="30ed3-167"><a name="diagnosis"></a>Diagnozowanie problemów</span><span class="sxs-lookup"><span data-stu-id="30ed3-167"><a name="diagnosis"></a>Diagnosing issues</span></span>
<span data-ttu-id="30ed3-168">Poniżej przedstawiono kilka wskazówek do znajdowania i diagnozowanie problemów z wydajnością:</span><span class="sxs-lookup"><span data-stu-id="30ed3-168">Here are a few tips for finding and diagnosing performance issues:</span></span>

* <span data-ttu-id="30ed3-169">Konfigurowanie [testów sieci web] [ availability] alertów, jeśli witryna sieci web ulegnie awarii lub odpowiada nieprawidłowo lub powoli.</span><span class="sxs-lookup"><span data-stu-id="30ed3-169">Set up [web tests][availability] to be alerted if your web site goes down or responds incorrectly or slowly.</span></span> 
* <span data-ttu-id="30ed3-170">Porównuje liczbę żądań z innych metryk w celu sprawdzenia, czy błędy lub powolna odpowiedź dotyczą obciążenia.</span><span class="sxs-lookup"><span data-stu-id="30ed3-170">Compare the Request count with other metrics to see if failures or slow response are related to load.</span></span>
* <span data-ttu-id="30ed3-171">[Wstaw i wyszukiwania instrukcji śledzenia] [ diagnostic] w kodzie, aby ułatwić identyfikowanie problemów.</span><span class="sxs-lookup"><span data-stu-id="30ed3-171">[Insert and search trace statements][diagnostic] in your code to help pinpoint problems.</span></span>
* <span data-ttu-id="30ed3-172">Monitorowanie aplikacji sieci Web w operację, podając [strumień na żywo metryki][livestream].</span><span class="sxs-lookup"><span data-stu-id="30ed3-172">Monitor your Web app in operation with [Live Metrics Stream][livestream].</span></span>
* <span data-ttu-id="30ed3-173">Przechwyć stan z aplikacji .net [debugera migawki][snapshot].</span><span class="sxs-lookup"><span data-stu-id="30ed3-173">Capture the state of your .Net application with [Snapshot Debugger][snapshot].</span></span>

## <a name="find-and-fix-performance-bottlenecks-with-an-interactive-performance-investigation"></a><span data-ttu-id="30ed3-174">Znajdź i napraw wąskich gardeł wydajności z dochodzenia interakcyjne wydajności</span><span class="sxs-lookup"><span data-stu-id="30ed3-174">Find and fix performance bottlenecks with an interactive performance investigation</span></span>

<span data-ttu-id="30ed3-175">Nowym postępowaniem interakcyjne wydajności usługi Application Insights umożliwia zlokalizować obszary aplikacji sieci Web, które są spowolnieniem ogólną wydajność.</span><span class="sxs-lookup"><span data-stu-id="30ed3-175">You can use the new Application Insights interactive performance investigation to locate areas of your Web app that are slowing down overall performance.</span></span> <span data-ttu-id="30ed3-176">Można szybko znaleźć określonych stron, które są spowolnieniem i użyj [narzędzia profilowania](app-insights-profiler.md) czy jest korelacja te strony.</span><span class="sxs-lookup"><span data-stu-id="30ed3-176">You can quickly find specific pages that are slowing down, and use the [Profiling tool](app-insights-profiler.md) to see if there is a correlation between these pages.</span></span>

### <a name="create-a-list-of-slow-performing-pages"></a><span data-ttu-id="30ed3-177">Utwórz listę powolne wykonywania strony</span><span class="sxs-lookup"><span data-stu-id="30ed3-177">Create a list of slow performing pages</span></span> 

<span data-ttu-id="30ed3-178">Pierwszym krokiem do znajdowania problemy z wydajnością jest w celu uzyskania listy powolne odpowiada strony.</span><span class="sxs-lookup"><span data-stu-id="30ed3-178">The first step for finding performance issues is to get a list of the slow responding pages.</span></span> <span data-ttu-id="30ed3-179">Zrzut poniżej ekranu pokazuje, używając bloku wydajności, aby uzyskać listę potencjalnych strony, aby zbadać dokładnie.</span><span class="sxs-lookup"><span data-stu-id="30ed3-179">The screen shot below demonstrates using the Performance blade to get a list of potential pages to investigate further.</span></span> <span data-ttu-id="30ed3-180">Możliwe jest szybkie wyświetlenie na tej stronie czy wystąpił spowolnienia czas odpowiedzi aplikacji na około 6:00 PM i ponownie na około 10 PM.</span><span class="sxs-lookup"><span data-stu-id="30ed3-180">You can quickly see from this page that there was a slow-down in the response time of the app at approximately 6:00 PM and again at approximately 10 PM.</span></span> <span data-ttu-id="30ed3-181">Można również sprawdzić, czy operacja szczegóły klienta/GET miał niektórych długotrwałe operacje z czasem odpowiedzi środkowej 507.05 milisekund.</span><span class="sxs-lookup"><span data-stu-id="30ed3-181">You can also see that the GET customer/details operation had some long running operations with a median response time of 507.05 milliseconds.</span></span> 

![Wydajność interakcyjne Insights aplikacji](./media/app-insights-web-monitor-performance/performance1.png)

### <a name="drill-down-on-specific-pages"></a><span data-ttu-id="30ed3-183">Przechodzenie do określonych stron</span><span class="sxs-lookup"><span data-stu-id="30ed3-183">Drill down on specific pages</span></span>

<span data-ttu-id="30ed3-184">Po utworzeniu migawki wydajności aplikacji, więcej informacji można uzyskać na określonych powolna wykonywania operacji.</span><span class="sxs-lookup"><span data-stu-id="30ed3-184">Once you have a snapshot of your app's performance, you can get more details on specific slow-performing operations.</span></span> <span data-ttu-id="30ed3-185">Polecenie żadnej operacji na liście, aby wyświetlić szczegóły, jak pokazano poniżej.</span><span class="sxs-lookup"><span data-stu-id="30ed3-185">Click on any operation in the list to see the details as shown below.</span></span> <span data-ttu-id="30ed3-186">Z wykresu jest widoczny czy wydajność oparto na zależność.</span><span class="sxs-lookup"><span data-stu-id="30ed3-186">From the chart you can see if the performance was based on a dependency.</span></span> <span data-ttu-id="30ed3-187">Można również sprawdzić, ilu użytkowników działa w różnym czasie odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="30ed3-187">You can also see how many users experienced the various response times.</span></span> 

![Application Insights operacji bloku](./media/app-insights-web-monitor-performance/performance5.png)

### <a name="drill-down-on-a-specific-time-period"></a><span data-ttu-id="30ed3-189">Przechodzenie w określonym przedziale czasu</span><span class="sxs-lookup"><span data-stu-id="30ed3-189">Drill down on a specific time period</span></span>

<span data-ttu-id="30ed3-190">Po zidentyfikowaniu punktu w czasie, aby zbadać, przejść do szczegółów nawet w przypadku znajduje się w określonej operacji, które mogły spowodować spowolnienia wydajności.</span><span class="sxs-lookup"><span data-stu-id="30ed3-190">After you have identified a point in time to investigate, drill down even further to look at the specific operations that might have caused the performance slow-down.</span></span> <span data-ttu-id="30ed3-191">Po kliknięciu określonego punktu w czasie otrzymasz szczegóły strony, jak pokazano poniżej.</span><span class="sxs-lookup"><span data-stu-id="30ed3-191">When you click on a specific point in time you get the details of the page as shown below.</span></span> <span data-ttu-id="30ed3-192">W poniższym przykładzie widoczny operacje wymienione w danym okresie oraz kody odpowiedzi serwera i czas trwania operacji.</span><span class="sxs-lookup"><span data-stu-id="30ed3-192">In the example below you can see the operations listed for a given time period along with the server response codes and the operation duration.</span></span> <span data-ttu-id="30ed3-193">Masz również adres url do otwarcia elementu roboczego TFS, aby wysyłać tych informacji do zespołu deweloperów.</span><span class="sxs-lookup"><span data-stu-id="30ed3-193">You also have the url for opening a TFS work item if you need to send this information to your development team.</span></span>

![Przedział czasu Application Insights](./media/app-insights-web-monitor-performance/performance2.png)

### <a name="drill-down-on-a-specific-operation"></a><span data-ttu-id="30ed3-195">Przechodzenie do określonej operacji</span><span class="sxs-lookup"><span data-stu-id="30ed3-195">Drill down on a specific operation</span></span>

<span data-ttu-id="30ed3-196">Po zidentyfikowaniu punktu w czasie, aby zbadać, przejść do szczegółów nawet w przypadku znajduje się w określonej operacji, które mogły spowodować spowolnienia wydajności.</span><span class="sxs-lookup"><span data-stu-id="30ed3-196">After you have identified a point in time to investigate, drill down even further to look at the specific operations that might have caused the performance slow-down.</span></span> <span data-ttu-id="30ed3-197">Polecenie operacji z listy, aby wyświetlić szczegóły operacji, jak pokazano poniżej.</span><span class="sxs-lookup"><span data-stu-id="30ed3-197">Click on an operation from the list to see the details of the operation as shown below.</span></span> <span data-ttu-id="30ed3-198">W tym przykładzie widać, operacja nie powiodła się, czy usługa Application Insights udostępnił szczegóły aplikacja zgłosiła wyjątek.</span><span class="sxs-lookup"><span data-stu-id="30ed3-198">In this example you can see that the operation failed, and Application Insights has provided the details of the exception the application threw.</span></span> <span data-ttu-id="30ed3-199">Ponownie można łatwo utworzyć elementu roboczego TFS z poziomu tego bloku.</span><span class="sxs-lookup"><span data-stu-id="30ed3-199">Again, you can easily create a TFS work item from this blade.</span></span>

![Application Insights operacji bloku](./media/app-insights-web-monitor-performance/performance3.png)


## <span data-ttu-id="30ed3-201"><a name="next"></a>Następne kroki</span><span class="sxs-lookup"><span data-stu-id="30ed3-201"><a name="next"></a>Next steps</span></span>
<span data-ttu-id="30ed3-202">[Testów sieci Web] [ availability] -żądania sieci web wysyłanych do aplikacji w regularnych odstępach czasu w całym świecie.</span><span class="sxs-lookup"><span data-stu-id="30ed3-202">[Web tests][availability] - Have web requests sent to your application at regular intervals from around the world.</span></span>

<span data-ttu-id="30ed3-203">[Przechwytywanie i wyszukiwać dane śledzenia diagnostycznego] [ diagnostic] — Wstaw śledzenie wywołań i zapoznawanie wyników, aby zidentyfikować problemy.</span><span class="sxs-lookup"><span data-stu-id="30ed3-203">[Capture and search diagnostic traces][diagnostic] - Insert trace calls and sift through the results to pinpoint issues.</span></span>

<span data-ttu-id="30ed3-204">[Śledzenie użycia] [ usage] -dowiedzieć się, jak użytkownicy korzystają z aplikacji.</span><span class="sxs-lookup"><span data-stu-id="30ed3-204">[Usage tracking][usage] - Find out how people use your application.</span></span>

<span data-ttu-id="30ed3-205">[Rozwiązywanie problemów z] [ qna] -Q & A i</span><span class="sxs-lookup"><span data-stu-id="30ed3-205">[Troubleshooting][qna] - and Q & A</span></span>



<!--Link references-->

[availability]: app-insights-monitor-web-app-availability.md
[diagnostic]: app-insights-diagnostic-search.md
[greenbrown]: app-insights-asp-net.md
[qna]: app-insights-troubleshoot-faq.md
[redfield]: app-insights-monitor-performance-live-website-now.md
[start]: app-insights-overview.md
[usage]: app-insights-web-track-usage.md
[livestream]: app-insights-live-stream.md
[snapshot]: app-insights-snapshot-debugger.md



