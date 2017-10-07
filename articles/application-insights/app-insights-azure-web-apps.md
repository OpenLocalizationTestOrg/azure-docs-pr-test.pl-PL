---
title: "aaaMonitor wydajność aplikacji sieci web platformy Azure | Dokumentacja firmy Microsoft"
description: "Monitorowanie wydajności aplikacji dla aplikacji sieci Web platformy Azure. Udostępnianie wykresów czasu ładowania i odpowiedzi oraz informacji o zależnościach oraz ustawianie alertów dotyczących wydajności."
services: application-insights
documentationcenter: .net
author: CFreemanwa
manager: carmonm
ms.assetid: 0b2deb30-6ea8-4bc4-8ed0-26765b85149f
ms.service: azure-portal
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 05/05/2017
ms.author: bwren
ms.openlocfilehash: d1083254e5c504b18f2ac5ae2368610dc2790436
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-azure-web-app-performance"></a><span data-ttu-id="8fe89-104">Monitorowanie wydajności aplikacji sieci Web platformy Azure</span><span class="sxs-lookup"><span data-stu-id="8fe89-104">Monitor Azure web app performance</span></span>
<span data-ttu-id="8fe89-105">W hello [Azure Portal](https://portal.azure.com) można skonfigurować monitorowanie wydajności aplikacji dla programu [aplikacje sieci web Azure](../app-service-web/app-service-web-overview.md).</span><span class="sxs-lookup"><span data-stu-id="8fe89-105">In hello [Azure Portal](https://portal.azure.com) you can set up application performance monitoring for your [Azure web apps](../app-service-web/app-service-web-overview.md).</span></span> <span data-ttu-id="8fe89-106">[Azure Application Insights](app-insights-overview.md) instruments telemetrii toosend aplikacji o jego toohello działania usługi Application Insights, gdzie są przechowywane i przeanalizowane.</span><span class="sxs-lookup"><span data-stu-id="8fe89-106">[Azure Application Insights](app-insights-overview.md) instruments your app toosend telemetry about its activities toohello Application Insights service, where it is stored and analyzed.</span></span> <span data-ttu-id="8fe89-107">Istnieje, można użyć narzędzia wyszukiwania i wykresy metryki toohelp diagnozowanie problemów, zwiększenia wydajności i użycia do oceny.</span><span class="sxs-lookup"><span data-stu-id="8fe89-107">There, metric charts and search tools can be used toohelp diagnose issues, improve performance, and assess usage.</span></span>

## <a name="run-time-or-build-time"></a><span data-ttu-id="8fe89-108">W czasie wykonywania lub czasie kompilacji</span><span class="sxs-lookup"><span data-stu-id="8fe89-108">Run time or build time</span></span>
<span data-ttu-id="8fe89-109">Można skonfigurować monitorowanie przez instrumentacji aplikacji hello na dwa sposoby:</span><span class="sxs-lookup"><span data-stu-id="8fe89-109">You can configure monitoring by instrumenting hello app in either of two ways:</span></span>

* <span data-ttu-id="8fe89-110">**Czas wykonywania** — możesz wybrać rozszerzenie monitorowania wydajności, gdy aplikacja sieci Web już działa.</span><span class="sxs-lookup"><span data-stu-id="8fe89-110">**Run-time** - You can select a performance monitoring extension when your web app is already live.</span></span> <span data-ttu-id="8fe89-111">Go nie jest konieczne toorebuild lub zainstaluj ponownie aplikację.</span><span class="sxs-lookup"><span data-stu-id="8fe89-111">It isn't necessary toorebuild or re-install your app.</span></span> <span data-ttu-id="8fe89-112">Uzyskujesz standardowy zestaw pakietów, które monitorują czasy odpowiedzi, współczynniki sukcesu, wyjątki, zależności itd.</span><span class="sxs-lookup"><span data-stu-id="8fe89-112">You get a standard set of packages that monitor response times, success rates, exceptions, dependencies, and so on.</span></span> 
* <span data-ttu-id="8fe89-113">**Czas kompilacji** — możesz zainstalować pakiet w aplikacji podczas programowania.</span><span class="sxs-lookup"><span data-stu-id="8fe89-113">**Build time** - You can install a package in your app in development.</span></span> <span data-ttu-id="8fe89-114">Ta opcja jest bardziej wszechstronna.</span><span class="sxs-lookup"><span data-stu-id="8fe89-114">This option is more versatile.</span></span> <span data-ttu-id="8fe89-115">W przypadku dodawania toohello same pakiety standardowe, można napisać kod toocustomize hello telemetrii lub toosend własnych danych telemetrycznych.</span><span class="sxs-lookup"><span data-stu-id="8fe89-115">In addition toohello same standard packages, you can write code toocustomize hello telemetry or toosend your own telemetry.</span></span> <span data-ttu-id="8fe89-116">Możesz zalogować się konkretne działania lub zdarzenia rekordu zgodnie z semantyki toohello domeny aplikacji.</span><span class="sxs-lookup"><span data-stu-id="8fe89-116">You can log specific activities or record events according toohello semantics of your app domain.</span></span> 

## <a name="run-time-instrumentation-with-application-insights"></a><span data-ttu-id="8fe89-117">Instrumentacja w czasie wykonywania za pomocą usługi Application Insights</span><span class="sxs-lookup"><span data-stu-id="8fe89-117">Run time instrumentation with Application Insights</span></span>
<span data-ttu-id="8fe89-118">Jeśli już masz uruchomioną aplikację sieci Web na platformie Azure, otrzymujesz pewne informacje monitorowania: żądania i współczynniki błędów.</span><span class="sxs-lookup"><span data-stu-id="8fe89-118">If you're already running a web app in Azure, you already get some monitoring: request and error rates.</span></span> <span data-ttu-id="8fe89-119">Dodaj więcej, takich jak czas reakcji, monitorowania toodependencies wywołania inteligentne wykrywanie i hello zaawansowanych język zapytań usługi Analiza dzienników tooget usługi Application Insights.</span><span class="sxs-lookup"><span data-stu-id="8fe89-119">Add Application Insights tooget more, such as response times, monitoring calls toodependencies, smart detection, and hello powerful Log Analytics query language.</span></span> 

1. <span data-ttu-id="8fe89-120">**Wybierz usługi Application Insights** w Panelu sterowania Azure powitania dla aplikacji sieci web.</span><span class="sxs-lookup"><span data-stu-id="8fe89-120">**Select Application Insights** in hello Azure control panel for your web app.</span></span>
   
    ![W obszarze Monitorowanie wybierz pozycję Application Insights](./media/app-insights-azure-web-apps/05-extend.png)
   
   * <span data-ttu-id="8fe89-122">Wybierz toocreate nowy zasób, chyba że — konfiguracja zasobu usługi Application Insights dla tej aplikacji jest już w innej trasy.</span><span class="sxs-lookup"><span data-stu-id="8fe89-122">Choose toocreate a new resource, unless you already set up an Application Insights resource for this app by another route.</span></span>
2. <span data-ttu-id="8fe89-123">**Zastosuj instrumentację aplikacji sieci Web** po zainstalowaniu usługi Application Insights.</span><span class="sxs-lookup"><span data-stu-id="8fe89-123">**Instrument your web app** after Application Insights has been installed.</span></span> 
   
    ![Instrumentacja aplikacji sieci Web](./media/app-insights-azure-web-apps/restart-web-app-for-insights.png)

   <span data-ttu-id="8fe89-125">**Włącz monitorowanie po stronie klienta** dla telemetrii widoku strony i użytkownika.</span><span class="sxs-lookup"><span data-stu-id="8fe89-125">**Enable client side monitoring** for page view and user telemetry.</span></span>

   * <span data-ttu-id="8fe89-126">Wybierz kolejno pozycje Ustawienia > Ustawienia aplikacji</span><span class="sxs-lookup"><span data-stu-id="8fe89-126">Select Settings > Application Settings</span></span>
   * <span data-ttu-id="8fe89-127">W obszarze Ustawienia aplikacji dodaj nową parę klucz-wartość:</span><span class="sxs-lookup"><span data-stu-id="8fe89-127">Under App Settings, add a new key value pair:</span></span> 
   
    <span data-ttu-id="8fe89-128">Klucz: `APPINSIGHTS_JAVASCRIPT_ENABLED`</span><span class="sxs-lookup"><span data-stu-id="8fe89-128">Key: `APPINSIGHTS_JAVASCRIPT_ENABLED`</span></span> 
    
    <span data-ttu-id="8fe89-129">Wartość:`true`</span><span class="sxs-lookup"><span data-stu-id="8fe89-129">Value: `true`</span></span>
   * <span data-ttu-id="8fe89-130">**Zapisz** hello ustawienia i **ponowne uruchomienie** aplikacji.</span><span class="sxs-lookup"><span data-stu-id="8fe89-130">**Save** hello settings and **Restart** your app.</span></span>
3. <span data-ttu-id="8fe89-131">**Monitoruj aplikację**.</span><span class="sxs-lookup"><span data-stu-id="8fe89-131">**Monitor your app**.</span></span>  <span data-ttu-id="8fe89-132">[Dane hello Expore](#explore-the-data).</span><span class="sxs-lookup"><span data-stu-id="8fe89-132">[Expore hello data](#explore-the-data).</span></span>

<span data-ttu-id="8fe89-133">Później można utworzyć aplikacji hello za pomocą usługi Application Insights, jeśli chcesz.</span><span class="sxs-lookup"><span data-stu-id="8fe89-133">Later, you can build hello app with Application Insights if you want.</span></span>

<span data-ttu-id="8fe89-134">*Jak usunąć usługi Application Insights, lub przełączyć zasób tooanother toosending?*</span><span class="sxs-lookup"><span data-stu-id="8fe89-134">*How do I remove Application Insights, or switch toosending tooanother resource?*</span></span>

* <span data-ttu-id="8fe89-135">Na platformie Azure, otwórz hello bloku kontroli aplikacja sieci web, a w obszarze Narzędzia deweloperskie, otwórz **rozszerzenia**.</span><span class="sxs-lookup"><span data-stu-id="8fe89-135">In Azure, open hello web app control blade, and under Development Tools, open **Extensions**.</span></span> <span data-ttu-id="8fe89-136">Usuń hello rozszerzenia usługi Application Insights.</span><span class="sxs-lookup"><span data-stu-id="8fe89-136">Delete hello Application Insights extension.</span></span> <span data-ttu-id="8fe89-137">Następnie w obszarze monitorowania, wybierz usługę Application Insights i Utwórz lub wybierz hello żądanego zasobu.</span><span class="sxs-lookup"><span data-stu-id="8fe89-137">Then under Monitoring, choose Application Insights and create or select hello resource you want.</span></span>

## <a name="build-hello-app-with-application-insights"></a><span data-ttu-id="8fe89-138">Tworzenie aplikacji hello za pomocą usługi Application Insights</span><span class="sxs-lookup"><span data-stu-id="8fe89-138">Build hello app with Application Insights</span></span>
<span data-ttu-id="8fe89-139">Usługa Application Insights może zapewnić bardziej szczegółową telemetrię dzięki instalacji zestawu SDK w Twojej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="8fe89-139">Application Insights can provide more detailed telemetry by installing an SDK into your app.</span></span> <span data-ttu-id="8fe89-140">W szczególności możesz gromadzić dzienniki śledzenia, [zapisywać niestandardową telemetrię](app-insights-api-custom-events-metrics.md) i uzyskiwać bardziej szczegółowe raporty o wyjątkach.</span><span class="sxs-lookup"><span data-stu-id="8fe89-140">In particular, you can collect trace logs, [write custom telemetry](app-insights-api-custom-events-metrics.md), and get more detailed exception reports.</span></span>

1. <span data-ttu-id="8fe89-141">**W programie Visual Studio** (2013 Update 2 lub nowszym) skonfiguruj usługę Application Insights dla projektu.</span><span class="sxs-lookup"><span data-stu-id="8fe89-141">**In Visual Studio** (2013 update 2 or later), configure Application Insights for your project.</span></span>

    <span data-ttu-id="8fe89-142">Kliknij prawym przyciskiem myszy projekt sieci web hello, a następnie wybierz **Dodaj > usługi Application Insights** lub **Konfiguruj usługę Application Insights**.</span><span class="sxs-lookup"><span data-stu-id="8fe89-142">Right-click hello web project, and select **Add > Application Insights** or **Configure Application Insights**.</span></span>
   
    ![Kliknij prawym przyciskiem myszy projekt sieci web hello i wybierz polecenie Dodaj i Konfiguruj usługę Application Insights](./media/app-insights-azure-web-apps/03-add.png)
   
    <span data-ttu-id="8fe89-144">Jeśli użytkownik jest proszony toosign w, należy użyć hello poświadczeń dla konta platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="8fe89-144">If you're asked toosign in, use hello credentials for your Azure account.</span></span>
   
    <span data-ttu-id="8fe89-145">Operacja Hello zawiera dwa efekty:</span><span class="sxs-lookup"><span data-stu-id="8fe89-145">hello operation has two effects:</span></span>
   
   1. <span data-ttu-id="8fe89-146">Tworzy zasób usługi Application Insights na platformie Azure, gdzie telemetria jest przechowywana, analizowana i wyświetlana.</span><span class="sxs-lookup"><span data-stu-id="8fe89-146">Creates an Application Insights resource in Azure, where telemetry is stored, analyzed and displayed.</span></span>
   2. <span data-ttu-id="8fe89-147">Dodaje hello NuGet usługi Application Insights tooyour kod pakietu (jeśli go nie ma już) i skonfiguruje je toosend telemetrii toohello zasobów platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="8fe89-147">Adds hello Application Insights NuGet package tooyour code (if it isn't there already), and configures it toosend telemetry toohello Azure resource.</span></span>
2. <span data-ttu-id="8fe89-148">**Testowanie telemetrii hello** w uruchomionej aplikacji hello w komputerze deweloperskim (F5).</span><span class="sxs-lookup"><span data-stu-id="8fe89-148">**Test hello telemetry** by running hello app in your development machine (F5).</span></span>
3. <span data-ttu-id="8fe89-149">**Publikowanie aplikacji hello** tooAzure hello — w zwykły sposób.</span><span class="sxs-lookup"><span data-stu-id="8fe89-149">**Publish hello app** tooAzure in hello usual way.</span></span> 

<span data-ttu-id="8fe89-150">*Jak zmienić toosending tooa innego zasobu usługi Application Insights?*</span><span class="sxs-lookup"><span data-stu-id="8fe89-150">*How do I switch toosending tooa different Application Insights resource?*</span></span>

* <span data-ttu-id="8fe89-151">W programie Visual Studio, kliknij prawym przyciskiem myszy projekt hello, wybierz **Konfiguruj usługę Application Insights** i wybierz zasób hello ma.</span><span class="sxs-lookup"><span data-stu-id="8fe89-151">In Visual Studio, right-click hello project, choose **Configure Application Insights** and choose hello resource you want.</span></span> <span data-ttu-id="8fe89-152">Pobierz toocreate opcji hello nowy zasób.</span><span class="sxs-lookup"><span data-stu-id="8fe89-152">You get hello option toocreate a new resource.</span></span> <span data-ttu-id="8fe89-153">Ponownie skompiluj i wdróż.</span><span class="sxs-lookup"><span data-stu-id="8fe89-153">Rebuild and redeploy.</span></span>

## <a name="explore-hello-data"></a><span data-ttu-id="8fe89-154">Eksplorowanie danych hello</span><span class="sxs-lookup"><span data-stu-id="8fe89-154">Explore hello data</span></span>
1. <span data-ttu-id="8fe89-155">W bloku usługi Application Insights hello Twojej aplikacji sieci web w Panelu sterowania, zobacz Live metryki przedstawiającego żądań i błędów w ciągu sekundy lub dwóch ich wystąpienia.</span><span class="sxs-lookup"><span data-stu-id="8fe89-155">On hello Application Insights blade of your web app control panel, you see Live Metrics, which shows requests and failures within a second or two of them occurring.</span></span> <span data-ttu-id="8fe89-156">Jest to bardzo przydatny widok w przypadku ponownego publikowania aplikacji — natychmiast zobaczysz wszelkie problemy.</span><span class="sxs-lookup"><span data-stu-id="8fe89-156">It's very useful display when you're republishing your app - you can see any problems immediately.</span></span>
2. <span data-ttu-id="8fe89-157">Kliknij toohello pełne zasobu usługi Application Insights.</span><span class="sxs-lookup"><span data-stu-id="8fe89-157">Click through toohello full Application Insights resource.</span></span>

    ![Kliknij elementy](./media/app-insights-azure-web-apps/view-in-application-insights.png)

    <span data-ttu-id="8fe89-159">Możesz tam przejść również bezpośrednio z nawigacji zasobów platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="8fe89-159">You can also go there either directly from Azure resource navigation.</span></span>

1. <span data-ttu-id="8fe89-160">Kliknij za pomocą dowolnego tooget wykresu więcej szczegółów:</span><span class="sxs-lookup"><span data-stu-id="8fe89-160">Click through any chart tooget more detail:</span></span>
   
    ![W bloku Omówienie usługi Application Insights hello kliknij wykres](./media/app-insights-azure-web-apps/07-dependency.png)
   
    <span data-ttu-id="8fe89-162">Możesz [dostosować bloki metryk](app-insights-metrics-explorer.md).</span><span class="sxs-lookup"><span data-stu-id="8fe89-162">You can [customize metrics blades](app-insights-metrics-explorer.md).</span></span>
2. <span data-ttu-id="8fe89-163">Kliknij go, dalsze toosee pojedynczych zdarzeń i ich właściwości:</span><span class="sxs-lookup"><span data-stu-id="8fe89-163">Click through further toosee individual events and their properties:</span></span>
   
    ![Kliknij przycisk tooopen typu zdarzenia wyszukiwania filtrowane wg typu](./media/app-insights-azure-web-apps/08-requests.png)
   
    <span data-ttu-id="8fe89-165">Zwróć uwagę, Witaj "..." tooopen łącze wszystkich właściwości.</span><span class="sxs-lookup"><span data-stu-id="8fe89-165">Notice hello "..." link tooopen all properties.</span></span>
   
    <span data-ttu-id="8fe89-166">Możesz [dostosować wyszukiwania](app-insights-diagnostic-search.md).</span><span class="sxs-lookup"><span data-stu-id="8fe89-166">You can [customize searches](app-insights-diagnostic-search.md).</span></span>

<span data-ttu-id="8fe89-167">Bardziej zaawansowane wyszukiwanie za pośrednictwem telemetrii, użyj hello [języka zapytań usługi Analiza dzienników](app-insights-analytics-tour.md).</span><span class="sxs-lookup"><span data-stu-id="8fe89-167">For more powerful searches over your telemetry, use hello [Log Analytics query language](app-insights-analytics-tour.md).</span></span>

## <a name="more-telemetry"></a><span data-ttu-id="8fe89-168">Dalsze funkcje telemetrii</span><span class="sxs-lookup"><span data-stu-id="8fe89-168">More telemetry</span></span>

* [<span data-ttu-id="8fe89-169">Dane ładowania strony sieci Web</span><span class="sxs-lookup"><span data-stu-id="8fe89-169">Web page load data</span></span>](app-insights-javascript.md)
* [<span data-ttu-id="8fe89-170">Telemetria niestandardowa</span><span class="sxs-lookup"><span data-stu-id="8fe89-170">Custom telemetry</span></span>](app-insights-api-custom-events-metrics.md)

## <a name="video"></a><span data-ttu-id="8fe89-171">Połączenia wideo</span><span class="sxs-lookup"><span data-stu-id="8fe89-171">Video</span></span>

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/100/player]

## <a name="next-steps"></a><span data-ttu-id="8fe89-172">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="8fe89-172">Next steps</span></span>
* <span data-ttu-id="8fe89-173">[Uruchom w aktywnej aplikacji hello profilera](app-insights-profiler.md).</span><span class="sxs-lookup"><span data-stu-id="8fe89-173">[Run hello profiler on your live app](app-insights-profiler.md).</span></span>
* <span data-ttu-id="8fe89-174">[Azure Functions](https://github.com/christopheranderson/azure-functions-app-insights-sample) — monitorowanie usługi Azure Functions za pomocą usługi Application Insights</span><span class="sxs-lookup"><span data-stu-id="8fe89-174">[Azure Functions](https://github.com/christopheranderson/azure-functions-app-insights-sample) - monitor Azure Functions with Application Insights</span></span>
* <span data-ttu-id="8fe89-175">[Włącz diagnostykę Azure](app-insights-azure-diagnostics.md) tooApplication toobe wysyłane szczegółowe informacje.</span><span class="sxs-lookup"><span data-stu-id="8fe89-175">[Enable Azure diagnostics](app-insights-azure-diagnostics.md) toobe sent tooApplication Insights.</span></span>
* <span data-ttu-id="8fe89-176">[Monitorowanie usługi kondycji metryk](../monitoring-and-diagnostics/insights-how-to-customize-monitoring.md) toomake się, że usługa jest dostępna i elastyczny.</span><span class="sxs-lookup"><span data-stu-id="8fe89-176">[Monitor service health metrics](../monitoring-and-diagnostics/insights-how-to-customize-monitoring.md) toomake sure your service is available and responsive.</span></span>
* <span data-ttu-id="8fe89-177">[Odbieraj powiadomienia o alertach](../monitoring-and-diagnostics/insights-receive-alert-notifications.md) zawsze, gdy wystąpią zdarzenia operacyjne lub metryki przekroczą próg.</span><span class="sxs-lookup"><span data-stu-id="8fe89-177">[Receive alert notifications](../monitoring-and-diagnostics/insights-receive-alert-notifications.md) whenever operational events happen or metrics cross a threshold.</span></span>
* <span data-ttu-id="8fe89-178">Użyj [usługi Application Insights dla aplikacji JavaScript i stron sieci web](app-insights-javascript.md) tooget klienta telemetrii hello przeglądarek, które strony sieci web.</span><span class="sxs-lookup"><span data-stu-id="8fe89-178">Use [Application Insights for JavaScript apps and web pages](app-insights-javascript.md) tooget client telemetry from hello browsers that visit a web page.</span></span>
* <span data-ttu-id="8fe89-179">[Konfigurowanie testów sieci web dostępności](app-insights-monitor-web-app-availability.md) toobe alert, jeśli witryna jest wyłączony.</span><span class="sxs-lookup"><span data-stu-id="8fe89-179">[Set up Availability web tests](app-insights-monitor-web-app-availability.md) toobe alerted if your site is down.</span></span>

