---
title: "aaaMonitor aplikacji kondycji i użycia za pomocą usługi Application Insights"
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
ms.openlocfilehash: 9230a6e65e5afb00c36122ff1d1de01ba19cd7f8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-performance-in-web-applications"></a><span data-ttu-id="61ffd-104">Monitorowanie wydajności w aplikacjach sieci Web</span><span class="sxs-lookup"><span data-stu-id="61ffd-104">Monitor performance in web applications</span></span>


<span data-ttu-id="61ffd-105">Upewnij się, że aplikacja działa optymalnie i Dowiedz się szybko o zakończą się niepowodzeniem.</span><span class="sxs-lookup"><span data-stu-id="61ffd-105">Make sure your application is performing well, and find out quickly about any failures.</span></span> <span data-ttu-id="61ffd-106">[Usługa Application Insights] [ start] informujące o wszelkich problemów z wydajnością oraz wyjątków i pomocy Znajdź i diagnozowanie hello główne przyczyny.</span><span class="sxs-lookup"><span data-stu-id="61ffd-106">[Application Insights][start] will tell you about any performance issues and exceptions, and help you find and diagnose hello root causes.</span></span>

<span data-ttu-id="61ffd-107">Usługa Application Insights można monitorować aplikacji sieci web zarówno Java, jak i platformy ASP.NET i usługi, usługi WCF.</span><span class="sxs-lookup"><span data-stu-id="61ffd-107">Application Insights can monitor both Java and ASP.NET web applications and services, WCF services.</span></span> <span data-ttu-id="61ffd-108">Mogą to być obsługiwana lokalnie, w przypadku maszyn wirtualnych lub jako witryny sieci Web Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="61ffd-108">They can be hosted on-premises, on virtual machines, or as Microsoft Azure websites.</span></span> 

<span data-ttu-id="61ffd-109">Po stronie klienta hello usługi Application Insights może zająć telemetrii ze stron sieci web i różnych urządzeniami, takimi jak systemy iOS, Android i aplikacji ze Sklepu Windows.</span><span class="sxs-lookup"><span data-stu-id="61ffd-109">On hello client side, Application Insights can take telemetry from web pages and a wide variety of devices including iOS, Android and Windows Store apps.</span></span>

>[!Note]
> <span data-ttu-id="61ffd-110">Wprowadzono nowe środowisko dostępne do znajdowania powolne wykonywania stron w aplikacji sieci web.</span><span class="sxs-lookup"><span data-stu-id="61ffd-110">We have made a new experience available for finding slow performing pages in your web application.</span></span> <span data-ttu-id="61ffd-111">Jeśli nie masz dostępu tooit ją włączyć, konfigurując opcje podglądu z hello [bloku Podgląd](app-insights-previews.md).</span><span class="sxs-lookup"><span data-stu-id="61ffd-111">If you don't have access tooit, enable it by configuring your preview options with hello [Preview blade](app-insights-previews.md).</span></span> <span data-ttu-id="61ffd-112">Przeczytaj informacje o nowe środowisko w [Znajdowanie i rozwiązywanie problemów wąskich gardeł wydajności hello interakcyjne wydajności postępowaniu](#Find-and-fix-performance-bottlenecks-with-an-interactive-Performance-investigation).</span><span class="sxs-lookup"><span data-stu-id="61ffd-112">Read about this new experience in [Find and fix performance bottlenecks with hello interactive Performance investigation](#Find-and-fix-performance-bottlenecks-with-an-interactive-Performance-investigation).</span></span>

## <span data-ttu-id="61ffd-113"><a name="setup"></a>Konfigurowanie monitorowania wydajności</span><span class="sxs-lookup"><span data-stu-id="61ffd-113"><a name="setup"></a>Set up performance monitoring</span></span>
<span data-ttu-id="61ffd-114">Jeśli jeszcze nie dodano tooyour usługi Application Insights projektu (Jeśli nie ma ApplicationInsights.config), wybierz jedną z następujących sposobów tooget uruchomiona:</span><span class="sxs-lookup"><span data-stu-id="61ffd-114">If you haven't yet added Application Insights tooyour project (that is, if it doesn't have ApplicationInsights.config), choose one of these ways tooget started:</span></span>

* [<span data-ttu-id="61ffd-115">Aplikacje sieci web ASP.NET</span><span class="sxs-lookup"><span data-stu-id="61ffd-115">ASP.NET web apps</span></span>](app-insights-asp-net.md)
  * [<span data-ttu-id="61ffd-116">Dodaj monitorowanie wyjątków</span><span class="sxs-lookup"><span data-stu-id="61ffd-116">Add exception monitoring</span></span>](app-insights-asp-net-exceptions.md)
  * [<span data-ttu-id="61ffd-117">Dodaj monitorowanie zależności</span><span class="sxs-lookup"><span data-stu-id="61ffd-117">Add dependency monitoring</span></span>](app-insights-monitor-performance-live-website-now.md)
* [<span data-ttu-id="61ffd-118">Aplikacje sieci web J2EE</span><span class="sxs-lookup"><span data-stu-id="61ffd-118">J2EE web apps</span></span>](app-insights-java-get-started.md)
  * [<span data-ttu-id="61ffd-119">Dodaj monitorowanie zależności</span><span class="sxs-lookup"><span data-stu-id="61ffd-119">Add dependency monitoring</span></span>](app-insights-java-agent.md)

## <span data-ttu-id="61ffd-120"><a name="view"></a>Eksploracja metryki wydajności</span><span class="sxs-lookup"><span data-stu-id="61ffd-120"><a name="view"></a>Exploring performance metrics</span></span>
<span data-ttu-id="61ffd-121">W [hello portalu Azure](https://portal.azure.com), przejdź do zasobu usługi Application Insights toohello skonfigurowanego dla aplikacji.</span><span class="sxs-lookup"><span data-stu-id="61ffd-121">In [hello Azure portal](https://portal.azure.com), browse toohello Application Insights resource that you set up for your application.</span></span> <span data-ttu-id="61ffd-122">bloku omówienie Hello przedstawia dane wydajności podstawowe:</span><span class="sxs-lookup"><span data-stu-id="61ffd-122">hello overview blade shows basic performance data:</span></span>

<span data-ttu-id="61ffd-123">Kliknij opcję żadnych toosee wykresu więcej szczegółów, a wyniki toosee przez dłuższy czas.</span><span class="sxs-lookup"><span data-stu-id="61ffd-123">Click any chart toosee more detail, and toosee results for a longer period.</span></span> <span data-ttu-id="61ffd-124">Na przykład kliknij Kafelek żądania hello, a następnie wybierz zakres czasu:</span><span class="sxs-lookup"><span data-stu-id="61ffd-124">For example, click hello Requests tile and then select a time range:</span></span>

![Kliknij za pośrednictwem toomore danych i wybierz zakres czasu](./media/app-insights-web-monitor-performance/appinsights-48metrics.png)

<span data-ttu-id="61ffd-126">Kliknij toochoose wykresu metryk, które wyświetla, lub Dodaj nowy wykres i wybrać jego metryki:</span><span class="sxs-lookup"><span data-stu-id="61ffd-126">Click a chart toochoose which metrics it displays, or add a new chart and select its metrics:</span></span>

![Kliknij przycisk metryki toochoose wykresu](./media/app-insights-web-monitor-performance/appinsights-61perfchoices.png)

> [!NOTE]
> <span data-ttu-id="61ffd-128">**Usuń zaznaczenie pola wyboru wszystkie metryki hello** toosee hello pełne zaznaczenia, która jest dostępna.</span><span class="sxs-lookup"><span data-stu-id="61ffd-128">**Uncheck all hello metrics** toosee hello full selection that is available.</span></span> <span data-ttu-id="61ffd-129">metryki Hello należą do grup; Po wybraniu dowolnego członka grupy hello innych członków tej grupy są wyświetlane tylko.</span><span class="sxs-lookup"><span data-stu-id="61ffd-129">hello metrics fall into groups; when any member of a group is selected, only hello other members of that group appear.</span></span>

## <span data-ttu-id="61ffd-130"><a name="metrics"></a>Jaki jest średnią wszystkich?</span><span class="sxs-lookup"><span data-stu-id="61ffd-130"><a name="metrics"></a>What does it all mean?</span></span> <span data-ttu-id="61ffd-131">Kafelki wydajności i raporty</span><span class="sxs-lookup"><span data-stu-id="61ffd-131">Performance tiles and reports</span></span>
<span data-ttu-id="61ffd-132">Istnieją różne metryki wydajności, które można pobrać.</span><span class="sxs-lookup"><span data-stu-id="61ffd-132">There are various performance metrics you can get.</span></span> <span data-ttu-id="61ffd-133">Zacznijmy od tych, które są wyświetlane domyślnie w bloku aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="61ffd-133">Let's start with those that appear by default on hello application blade.</span></span>

### <a name="requests"></a><span data-ttu-id="61ffd-134">Żądania</span><span class="sxs-lookup"><span data-stu-id="61ffd-134">Requests</span></span>
<span data-ttu-id="61ffd-135">Liczba Hello żądania HTTP odebrane w określonym przedziale czasu.</span><span class="sxs-lookup"><span data-stu-id="61ffd-135">hello number of HTTP requests received in a specified period.</span></span> <span data-ttu-id="61ffd-136">To porównać z wynikami hello na inne toosee raporty zachowania aplikacji jako hello obciążenia.</span><span class="sxs-lookup"><span data-stu-id="61ffd-136">Compare this with hello results on other reports toosee how your app behaves as hello load varies.</span></span>

<span data-ttu-id="61ffd-137">Żądania HTTP obejmują wszystkie żądania GET lub POST dla stron, danych i obrazów.</span><span class="sxs-lookup"><span data-stu-id="61ffd-137">HTTP requests include all GET or POST requests for pages, data, and images.</span></span>

<span data-ttu-id="61ffd-138">Polecenie hello kafelka tooget liczniki dla określonych adresów URL.</span><span class="sxs-lookup"><span data-stu-id="61ffd-138">Click on hello tile tooget counts for specific URLs.</span></span>

### <a name="average-response-time"></a><span data-ttu-id="61ffd-139">Średni czas odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="61ffd-139">Average response time</span></span>
<span data-ttu-id="61ffd-140">Środki hello czas między wprowadzania aplikacji i hello odpowiedź zwracana żądania sieci web.</span><span class="sxs-lookup"><span data-stu-id="61ffd-140">Measures hello time between a web request entering your application and hello response being returned.</span></span>

<span data-ttu-id="61ffd-141">punkty Hello pokazują, ruchomą średnią.</span><span class="sxs-lookup"><span data-stu-id="61ffd-141">hello points show a moving average.</span></span> <span data-ttu-id="61ffd-142">Jeśli istnieje wiele żądań, mogą wystąpić, które odbiegają od średniej hello bez widocznych szczytu lub zanurzyć hello wykresie.</span><span class="sxs-lookup"><span data-stu-id="61ffd-142">If there are a lot of requests, there might be some that deviate from hello average without an obvious peak or dip in hello graph.</span></span>

<span data-ttu-id="61ffd-143">Poszukaj nietypowe szczytów.</span><span class="sxs-lookup"><span data-stu-id="61ffd-143">Look for unusual peaks.</span></span> <span data-ttu-id="61ffd-144">Ogólnie rzecz biorąc można spodziewać się toorise czasu odpowiedzi z wzrost żądania.</span><span class="sxs-lookup"><span data-stu-id="61ffd-144">In general, expect response time toorise with a rise in requests.</span></span> <span data-ttu-id="61ffd-145">W przypadku nieproporcjonalnie powstanie hello aplikacji może być naciśnięcie limit zasobów, takie jak procesor CPU lub hello pojemność usługi, które są używane.</span><span class="sxs-lookup"><span data-stu-id="61ffd-145">If hello rise is disproportionate, your app might be hitting a resource limit such as CPU or hello capacity of a service it uses.</span></span>

<span data-ttu-id="61ffd-146">Kliknij przycisk hello kafelka tooget razy dla określonych adresów URL.</span><span class="sxs-lookup"><span data-stu-id="61ffd-146">Click hello tile tooget times for specific URLs.</span></span>

![](./media/app-insights-web-monitor-performance/appinsights-42reqs.png)

### <a name="slowest-requests"></a><span data-ttu-id="61ffd-147">Najwolniejsze żądań</span><span class="sxs-lookup"><span data-stu-id="61ffd-147">Slowest requests</span></span>
![](./media/app-insights-web-monitor-performance/appinsights-44slowest.png)

<span data-ttu-id="61ffd-148">Pokazuje, które żądania może być konieczne dostrojenie wydajności.</span><span class="sxs-lookup"><span data-stu-id="61ffd-148">Shows which requests might need performance tuning.</span></span>

### <a name="failed-requests"></a><span data-ttu-id="61ffd-149">Żądań zakończonych niepowodzeniem</span><span class="sxs-lookup"><span data-stu-id="61ffd-149">Failed requests</span></span>
![](./media/app-insights-web-monitor-performance/appinsights-46failed.png)

<span data-ttu-id="61ffd-150">Liczba żądań, które zwrócił nieprzechwyconych wyjątków.</span><span class="sxs-lookup"><span data-stu-id="61ffd-150">A count of requests that threw uncaught exceptions.</span></span>

<span data-ttu-id="61ffd-151">Kliknij hello kafelka toosee hello szczegółów określonych niepowodzeń i wybierz toosee oddzielne żądanie jego szczegóły.</span><span class="sxs-lookup"><span data-stu-id="61ffd-151">Click hello tile toosee hello details of specific failures, and select an individual request toosee its detail.</span></span> 

<span data-ttu-id="61ffd-152">Tylko reprezentatywnej próbki błędów jest przechowywany dla poszczególnych kontroli.</span><span class="sxs-lookup"><span data-stu-id="61ffd-152">Only a representative sample of failures is retained for individual inspection.</span></span>

### <a name="other-metrics"></a><span data-ttu-id="61ffd-153">Innych metryk</span><span class="sxs-lookup"><span data-stu-id="61ffd-153">Other metrics</span></span>
<span data-ttu-id="61ffd-154">toosee jakie inne metryki, można wyświetlać, kliknij wykres i usuń zaznaczenie wszystkich hello metryki toosee hello pełnej dostępnych zestawów.</span><span class="sxs-lookup"><span data-stu-id="61ffd-154">toosee what other metrics you can display, click a graph, and then deselect all hello metrics toosee hello full available set.</span></span> <span data-ttu-id="61ffd-155">Kliknij przycisk (i) toosee definicji wszystkie metryki.</span><span class="sxs-lookup"><span data-stu-id="61ffd-155">Click (i) toosee each metric's definition.</span></span>

![Odznacz wszystkie metryki toosee hello całego zestawu](./media/app-insights-web-monitor-performance/appinsights-62allchoices.png)

<span data-ttu-id="61ffd-157">Wybranie dowolnego hello wyłącza metryki innych osób, które nie mogą występować w hello tego samego wykresu.</span><span class="sxs-lookup"><span data-stu-id="61ffd-157">Selecting any metric disables hello others that can't appear on hello same chart.</span></span>

## <a name="set-alerts"></a><span data-ttu-id="61ffd-158">Ustawianie alertów</span><span class="sxs-lookup"><span data-stu-id="61ffd-158">Set alerts</span></span>
<span data-ttu-id="61ffd-159">powiadomienie e-mail o nietypowych wartościach dowolnej metryki toobe dodać alert.</span><span class="sxs-lookup"><span data-stu-id="61ffd-159">toobe notified by email of unusual values of any metric, add an alert.</span></span> <span data-ttu-id="61ffd-160">Można wybrać toosend hello e-mail toohello konta administratorów lub toospecific adresy e-mail.</span><span class="sxs-lookup"><span data-stu-id="61ffd-160">You can choose either toosend hello email toohello account administrators, or toospecific email addresses.</span></span>

![](./media/app-insights-web-monitor-performance/appinsights-413setMetricAlert.png)

<span data-ttu-id="61ffd-161">Ustaw zasób hello przed hello inne właściwości.</span><span class="sxs-lookup"><span data-stu-id="61ffd-161">Set hello resource before hello other properties.</span></span> <span data-ttu-id="61ffd-162">Nie wybierz hello webtest zasoby, jeśli chcesz otrzymywać alerty tooset na wydajność lub metryki użycia.</span><span class="sxs-lookup"><span data-stu-id="61ffd-162">Don't choose hello webtest resources if you want tooset alerts on performance or usage metrics.</span></span>

<span data-ttu-id="61ffd-163">Być dokładne toonote hello jednostki, w których użytkownik jest proszony wartość progowa hello tooenter.</span><span class="sxs-lookup"><span data-stu-id="61ffd-163">Be careful toonote hello units in which you're asked tooenter hello threshold value.</span></span>

<span data-ttu-id="61ffd-164">*Nie widzę Alert przycisku Dodaj hello.*</span><span class="sxs-lookup"><span data-stu-id="61ffd-164">*I don't see hello Add Alert button.*</span></span> <span data-ttu-id="61ffd-165">— To toowhich konta grupy mają dostęp tylko do odczytu?</span><span class="sxs-lookup"><span data-stu-id="61ffd-165">- Is this a group account toowhich you have read-only access?</span></span> <span data-ttu-id="61ffd-166">Skontaktuj się z administratorem konta hello.</span><span class="sxs-lookup"><span data-stu-id="61ffd-166">Check with hello account administrator.</span></span>

## <span data-ttu-id="61ffd-167"><a name="diagnosis"></a>Diagnozowanie problemów</span><span class="sxs-lookup"><span data-stu-id="61ffd-167"><a name="diagnosis"></a>Diagnosing issues</span></span>
<span data-ttu-id="61ffd-168">Poniżej przedstawiono kilka wskazówek do znajdowania i diagnozowanie problemów z wydajnością:</span><span class="sxs-lookup"><span data-stu-id="61ffd-168">Here are a few tips for finding and diagnosing performance issues:</span></span>

* <span data-ttu-id="61ffd-169">Konfigurowanie [testów sieci web] [ availability] toobe alert, jeśli witryna sieci web ulegnie awarii lub odpowiada nieprawidłowo lub powoli.</span><span class="sxs-lookup"><span data-stu-id="61ffd-169">Set up [web tests][availability] toobe alerted if your web site goes down or responds incorrectly or slowly.</span></span> 
* <span data-ttu-id="61ffd-170">Porównaj hello liczbę żądań z innych metryk toosee w przypadku awarii lub powolna odpowiedź tooload pokrewne.</span><span class="sxs-lookup"><span data-stu-id="61ffd-170">Compare hello Request count with other metrics toosee if failures or slow response are related tooload.</span></span>
* <span data-ttu-id="61ffd-171">[Wstaw i wyszukiwania instrukcji śledzenia] [ diagnostic] w toohelp Twojego kodu identyfikowanie problemów.</span><span class="sxs-lookup"><span data-stu-id="61ffd-171">[Insert and search trace statements][diagnostic] in your code toohelp pinpoint problems.</span></span>
* <span data-ttu-id="61ffd-172">Monitorowanie aplikacji sieci Web w operację, podając [strumień na żywo metryki][livestream].</span><span class="sxs-lookup"><span data-stu-id="61ffd-172">Monitor your Web app in operation with [Live Metrics Stream][livestream].</span></span>
* <span data-ttu-id="61ffd-173">Przechwyć stan hello aplikacji .net z [debugera migawki][snapshot].</span><span class="sxs-lookup"><span data-stu-id="61ffd-173">Capture hello state of your .Net application with [Snapshot Debugger][snapshot].</span></span>

## <a name="find-and-fix-performance-bottlenecks-with-an-interactive-performance-investigation"></a><span data-ttu-id="61ffd-174">Znajdź i napraw wąskich gardeł wydajności z dochodzenia interakcyjne wydajności</span><span class="sxs-lookup"><span data-stu-id="61ffd-174">Find and fix performance bottlenecks with an interactive performance investigation</span></span>

<span data-ttu-id="61ffd-175">Możesz użyć hello nowej usługi Application Insights interakcyjne wydajności dochodzenia toolocate obszary aplikacji sieci Web są spowolnieniem ogólną wydajność.</span><span class="sxs-lookup"><span data-stu-id="61ffd-175">You can use hello new Application Insights interactive performance investigation toolocate areas of your Web app that are slowing down overall performance.</span></span> <span data-ttu-id="61ffd-176">Można szybko znaleźć określonych stron, które są spowolnieniem i użyj hello [narzędzia profilowania](app-insights-profiler.md) toosee, jeśli występuje korelacja te strony.</span><span class="sxs-lookup"><span data-stu-id="61ffd-176">You can quickly find specific pages that are slowing down, and use hello [Profiling tool](app-insights-profiler.md) toosee if there is a correlation between these pages.</span></span>

### <a name="create-a-list-of-slow-performing-pages"></a><span data-ttu-id="61ffd-177">Utwórz listę powolne wykonywania strony</span><span class="sxs-lookup"><span data-stu-id="61ffd-177">Create a list of slow performing pages</span></span> 

<span data-ttu-id="61ffd-178">pierwszym krokiem Hello znajdowanie problemów z wydajnością jest tooget listę hello wolno odpowiadać stron.</span><span class="sxs-lookup"><span data-stu-id="61ffd-178">hello first step for finding performance issues is tooget a list of hello slow responding pages.</span></span> <span data-ttu-id="61ffd-179">ekranie powitania zrzut poniżej przedstawiono przy użyciu hello wydajności bloku tooget listę potencjalnych tooinvestigate więcej stron.</span><span class="sxs-lookup"><span data-stu-id="61ffd-179">hello screen shot below demonstrates using hello Performance blade tooget a list of potential pages tooinvestigate further.</span></span> <span data-ttu-id="61ffd-180">Możliwe jest szybkie wyświetlenie na tej stronie czy wystąpił spowolnienia hello czas odpowiedzi aplikacji hello na około 6:00 PM i ponownie na około 10 PM.</span><span class="sxs-lookup"><span data-stu-id="61ffd-180">You can quickly see from this page that there was a slow-down in hello response time of hello app at approximately 6:00 PM and again at approximately 10 PM.</span></span> <span data-ttu-id="61ffd-181">Można również sprawdzić, czy operacja szczegóły klienta/GET hello miał niektóre długotrwałe operacje z czasem odpowiedzi środkowej 507.05 milisekund.</span><span class="sxs-lookup"><span data-stu-id="61ffd-181">You can also see that hello GET customer/details operation had some long running operations with a median response time of 507.05 milliseconds.</span></span> 

![Wydajność interakcyjne Insights aplikacji](./media/app-insights-web-monitor-performance/performance1.png)

### <a name="drill-down-on-specific-pages"></a><span data-ttu-id="61ffd-183">Przechodzenie do określonych stron</span><span class="sxs-lookup"><span data-stu-id="61ffd-183">Drill down on specific pages</span></span>

<span data-ttu-id="61ffd-184">Po utworzeniu migawki wydajności aplikacji, więcej informacji można uzyskać na określonych powolna wykonywania operacji.</span><span class="sxs-lookup"><span data-stu-id="61ffd-184">Once you have a snapshot of your app's performance, you can get more details on specific slow-performing operations.</span></span> <span data-ttu-id="61ffd-185">Polecenie żadnej operacji w hello listy toosee hello uzyskać szczegółowe informacje, jak pokazano poniżej.</span><span class="sxs-lookup"><span data-stu-id="61ffd-185">Click on any operation in hello list toosee hello details as shown below.</span></span> <span data-ttu-id="61ffd-186">Z wykresu hello widać, jeśli wydajność hello oparto na zależność.</span><span class="sxs-lookup"><span data-stu-id="61ffd-186">From hello chart you can see if hello performance was based on a dependency.</span></span> <span data-ttu-id="61ffd-187">Możesz również sprawdzić ile hello doświadczeni użytkownicy różnych czas odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="61ffd-187">You can also see how many users experienced hello various response times.</span></span> 

![Application Insights operacji bloku](./media/app-insights-web-monitor-performance/performance5.png)

### <a name="drill-down-on-a-specific-time-period"></a><span data-ttu-id="61ffd-189">Przechodzenie w określonym przedziale czasu</span><span class="sxs-lookup"><span data-stu-id="61ffd-189">Drill down on a specific time period</span></span>

<span data-ttu-id="61ffd-190">Po zidentyfikowaniu punktu w czasie tooinvestigate przechodzenie nawet dalsze toolook na powitania określonych operacji, które mogły spowodować hello spowolnienia wydajności.</span><span class="sxs-lookup"><span data-stu-id="61ffd-190">After you have identified a point in time tooinvestigate, drill down even further toolook at hello specific operations that might have caused hello performance slow-down.</span></span> <span data-ttu-id="61ffd-191">Po kliknięciu określonego punktu w czasie otrzymasz szczegóły hello hello strony, jak pokazano poniżej.</span><span class="sxs-lookup"><span data-stu-id="61ffd-191">When you click on a specific point in time you get hello details of hello page as shown below.</span></span> <span data-ttu-id="61ffd-192">Hello przykład poniżej przedstawiono operacje hello wymienionych w danym okresie oraz kody odpowiedzi serwera hello i czasu trwania operacji hello.</span><span class="sxs-lookup"><span data-stu-id="61ffd-192">In hello example below you can see hello operations listed for a given time period along with hello server response codes and hello operation duration.</span></span> <span data-ttu-id="61ffd-193">Masz również hello adres url do otwarcia elementu roboczego TFS, jeśli potrzebujesz toosend zespół deweloperów tooyour tej informacji.</span><span class="sxs-lookup"><span data-stu-id="61ffd-193">You also have hello url for opening a TFS work item if you need toosend this information tooyour development team.</span></span>

![Przedział czasu Application Insights](./media/app-insights-web-monitor-performance/performance2.png)

### <a name="drill-down-on-a-specific-operation"></a><span data-ttu-id="61ffd-195">Przechodzenie do określonej operacji</span><span class="sxs-lookup"><span data-stu-id="61ffd-195">Drill down on a specific operation</span></span>

<span data-ttu-id="61ffd-196">Po zidentyfikowaniu punktu w czasie tooinvestigate przechodzenie nawet dalsze toolook na powitania określonych operacji, które mogły spowodować hello spowolnienia wydajności.</span><span class="sxs-lookup"><span data-stu-id="61ffd-196">After you have identified a point in time tooinvestigate, drill down even further toolook at hello specific operations that might have caused hello performance slow-down.</span></span> <span data-ttu-id="61ffd-197">Kliknij działanie od hello listy toosee hello szczegóły operacji hello, jak pokazano poniżej.</span><span class="sxs-lookup"><span data-stu-id="61ffd-197">Click on an operation from hello list toosee hello details of hello operation as shown below.</span></span> <span data-ttu-id="61ffd-198">W tym przykładzie widocznej hello operacja nie powiodła się, czy usługi Application Insights udostępnił hello szczegóły hello zgłosiła wyjątek aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="61ffd-198">In this example you can see that hello operation failed, and Application Insights has provided hello details of hello exception hello application threw.</span></span> <span data-ttu-id="61ffd-199">Ponownie można łatwo utworzyć elementu roboczego TFS z poziomu tego bloku.</span><span class="sxs-lookup"><span data-stu-id="61ffd-199">Again, you can easily create a TFS work item from this blade.</span></span>

![Application Insights operacji bloku](./media/app-insights-web-monitor-performance/performance3.png)


## <span data-ttu-id="61ffd-201"><a name="next"></a>Następne kroki</span><span class="sxs-lookup"><span data-stu-id="61ffd-201"><a name="next"></a>Next steps</span></span>
<span data-ttu-id="61ffd-202">[Testów sieci Web] [ availability] -żądań sieci web wysłali tooyour aplikacji w regularnych odstępach czasu z wokół hello world.</span><span class="sxs-lookup"><span data-stu-id="61ffd-202">[Web tests][availability] - Have web requests sent tooyour application at regular intervals from around hello world.</span></span>

<span data-ttu-id="61ffd-203">[Przechwytywanie i wyszukiwać dane śledzenia diagnostycznego] [ diagnostic] — Wstaw śledzenie wywołań i zapoznawanie hello wyniki toopinpoint problemów.</span><span class="sxs-lookup"><span data-stu-id="61ffd-203">[Capture and search diagnostic traces][diagnostic] - Insert trace calls and sift through hello results toopinpoint issues.</span></span>

<span data-ttu-id="61ffd-204">[Śledzenie użycia] [ usage] -dowiedzieć się, jak użytkownicy korzystają z aplikacji.</span><span class="sxs-lookup"><span data-stu-id="61ffd-204">[Usage tracking][usage] - Find out how people use your application.</span></span>

<span data-ttu-id="61ffd-205">[Rozwiązywanie problemów z] [ qna] -Q & A i</span><span class="sxs-lookup"><span data-stu-id="61ffd-205">[Troubleshooting][qna] - and Q & A</span></span>



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



