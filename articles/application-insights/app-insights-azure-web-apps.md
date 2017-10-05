---
title: "Monitorowanie wydajności aplikacji sieci Web platformy Azure | Microsoft Docs"
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
ms.openlocfilehash: f2bbadfbcb93873ed910aeff050bd6896e2e8fec
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/18/2017
---
# <a name="monitor-azure-web-app-performance"></a><span data-ttu-id="d8567-104">Monitorowanie wydajności aplikacji sieci Web platformy Azure</span><span class="sxs-lookup"><span data-stu-id="d8567-104">Monitor Azure web app performance</span></span>
<span data-ttu-id="d8567-105">W witrynie [Azure Portal](https://portal.azure.com) możesz skonfigurować monitorowanie wydajności [aplikacji sieci Web platformy Azure](../app-service-web/app-service-web-overview.md).</span><span class="sxs-lookup"><span data-stu-id="d8567-105">In the [Azure Portal](https://portal.azure.com) you can set up application performance monitoring for your [Azure web apps](../app-service-web/app-service-web-overview.md).</span></span> <span data-ttu-id="d8567-106">[Usługa Azure Application Insights](app-insights-overview.md) umożliwia instrumentację aplikacji w celu wysyłania danych telemetrii do usługi Application Insights, gdzie są one przechowywane i analizowane.</span><span class="sxs-lookup"><span data-stu-id="d8567-106">[Azure Application Insights](app-insights-overview.md) instruments your app to send telemetry about its activities to the Application Insights service, where it is stored and analyzed.</span></span> <span data-ttu-id="d8567-107">W usłudze tej można używać wykresów metryki i narzędzi wyszukiwania do ułatwiania diagnozowania problemów, zwiększania wydajności i oceny użycia.</span><span class="sxs-lookup"><span data-stu-id="d8567-107">There, metric charts and search tools can be used to help diagnose issues, improve performance, and assess usage.</span></span>

## <a name="run-time-or-build-time"></a><span data-ttu-id="d8567-108">W czasie wykonywania lub czasie kompilacji</span><span class="sxs-lookup"><span data-stu-id="d8567-108">Run time or build time</span></span>
<span data-ttu-id="d8567-109">Możesz skonfigurować monitorowanie, instrumentując aplikację na jeden z dwóch sposobów:</span><span class="sxs-lookup"><span data-stu-id="d8567-109">You can configure monitoring by instrumenting the app in either of two ways:</span></span>

* <span data-ttu-id="d8567-110">**Czas wykonywania** — możesz wybrać rozszerzenie monitorowania wydajności, gdy aplikacja sieci Web już działa.</span><span class="sxs-lookup"><span data-stu-id="d8567-110">**Run-time** - You can select a performance monitoring extension when your web app is already live.</span></span> <span data-ttu-id="d8567-111">Nie trzeba ponownie kompilować ani instalować aplikacji.</span><span class="sxs-lookup"><span data-stu-id="d8567-111">It isn't necessary to rebuild or re-install your app.</span></span> <span data-ttu-id="d8567-112">Uzyskujesz standardowy zestaw pakietów, które monitorują czasy odpowiedzi, współczynniki sukcesu, wyjątki, zależności itd.</span><span class="sxs-lookup"><span data-stu-id="d8567-112">You get a standard set of packages that monitor response times, success rates, exceptions, dependencies, and so on.</span></span> 
* <span data-ttu-id="d8567-113">**Czas kompilacji** — możesz zainstalować pakiet w aplikacji podczas programowania.</span><span class="sxs-lookup"><span data-stu-id="d8567-113">**Build time** - You can install a package in your app in development.</span></span> <span data-ttu-id="d8567-114">Ta opcja jest bardziej wszechstronna.</span><span class="sxs-lookup"><span data-stu-id="d8567-114">This option is more versatile.</span></span> <span data-ttu-id="d8567-115">Oprócz tych samych pakietów standardowych możesz napisać kod w celu dostosowania telemetrii lub wysłania własnych danych telemetrii.</span><span class="sxs-lookup"><span data-stu-id="d8567-115">In addition to the same standard packages, you can write code to customize the telemetry or to send your own telemetry.</span></span> <span data-ttu-id="d8567-116">Możesz rejestrować określone działania lub zdarzenia zgodnie z semantyką domeny aplikacji.</span><span class="sxs-lookup"><span data-stu-id="d8567-116">You can log specific activities or record events according to the semantics of your app domain.</span></span> 

## <a name="run-time-instrumentation-with-application-insights"></a><span data-ttu-id="d8567-117">Instrumentacja w czasie wykonywania za pomocą usługi Application Insights</span><span class="sxs-lookup"><span data-stu-id="d8567-117">Run time instrumentation with Application Insights</span></span>
<span data-ttu-id="d8567-118">Jeśli już masz uruchomioną aplikację sieci Web na platformie Azure, otrzymujesz pewne informacje monitorowania: żądania i współczynniki błędów.</span><span class="sxs-lookup"><span data-stu-id="d8567-118">If you're already running a web app in Azure, you already get some monitoring: request and error rates.</span></span> <span data-ttu-id="d8567-119">Dodaj usługę Application Insights, aby uzyskać więcej informacji, na przykład czasy odpowiedzi, monitorowanie wywołań dla zależności, inteligentne wykrywanie i zaawansowany język zapytań usługi Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="d8567-119">Add Application Insights to get more, such as response times, monitoring calls to dependencies, smart detection, and the powerful Log Analytics query language.</span></span> 

1. <span data-ttu-id="d8567-120">**Wybierz usługę Application Insights** w Panelu sterowania platformy Azure dla aplikacji sieci Web.</span><span class="sxs-lookup"><span data-stu-id="d8567-120">**Select Application Insights** in the Azure control panel for your web app.</span></span>
   
    ![W obszarze Monitorowanie wybierz pozycję Application Insights](./media/app-insights-azure-web-apps/05-extend.png)
   
   * <span data-ttu-id="d8567-122">Wybierz opcję tworzenia nowego zasobu, chyba że zasób usługi Application Insights dla tej aplikacji został już skonfigurowany inną drogą.</span><span class="sxs-lookup"><span data-stu-id="d8567-122">Choose to create a new resource, unless you already set up an Application Insights resource for this app by another route.</span></span>
2. <span data-ttu-id="d8567-123">**Zastosuj instrumentację aplikacji sieci Web** po zainstalowaniu usługi Application Insights.</span><span class="sxs-lookup"><span data-stu-id="d8567-123">**Instrument your web app** after Application Insights has been installed.</span></span> 
   
    ![Instrumentacja aplikacji sieci Web](./media/app-insights-azure-web-apps/restart-web-app-for-insights.png)

   <span data-ttu-id="d8567-125">**Włącz monitorowanie po stronie klienta** dla telemetrii widoku strony i użytkownika.</span><span class="sxs-lookup"><span data-stu-id="d8567-125">**Enable client side monitoring** for page view and user telemetry.</span></span>

   * <span data-ttu-id="d8567-126">Wybierz kolejno pozycje Ustawienia > Ustawienia aplikacji</span><span class="sxs-lookup"><span data-stu-id="d8567-126">Select Settings > Application Settings</span></span>
   * <span data-ttu-id="d8567-127">W obszarze Ustawienia aplikacji dodaj nową parę klucz-wartość:</span><span class="sxs-lookup"><span data-stu-id="d8567-127">Under App Settings, add a new key value pair:</span></span> 
   
    <span data-ttu-id="d8567-128">Klucz: `APPINSIGHTS_JAVASCRIPT_ENABLED`</span><span class="sxs-lookup"><span data-stu-id="d8567-128">Key: `APPINSIGHTS_JAVASCRIPT_ENABLED`</span></span> 
    
    <span data-ttu-id="d8567-129">Wartość:`true`</span><span class="sxs-lookup"><span data-stu-id="d8567-129">Value: `true`</span></span>
   * <span data-ttu-id="d8567-130">**Zapisz** ustawienia i **ponownie uruchom** aplikację.</span><span class="sxs-lookup"><span data-stu-id="d8567-130">**Save** the settings and **Restart** your app.</span></span>
3. <span data-ttu-id="d8567-131">**Monitoruj aplikację**.</span><span class="sxs-lookup"><span data-stu-id="d8567-131">**Monitor your app**.</span></span>  <span data-ttu-id="d8567-132">[Eksploruj dane](#explore-the-data).</span><span class="sxs-lookup"><span data-stu-id="d8567-132">[Expore the data](#explore-the-data).</span></span>

<span data-ttu-id="d8567-133">W razie potrzeby możesz później utworzyć aplikację za pomocą usługi Application Insights.</span><span class="sxs-lookup"><span data-stu-id="d8567-133">Later, you can build the app with Application Insights if you want.</span></span>

<span data-ttu-id="d8567-134">*Jak usunąć usługę Application Insights lub przełączyć się na wysyłanie do innego zasobu?*</span><span class="sxs-lookup"><span data-stu-id="d8567-134">*How do I remove Application Insights, or switch to sending to another resource?*</span></span>

* <span data-ttu-id="d8567-135">Na platformie Azure otwórz blok sterowania aplikacji sieci Web i w obszarze Narzędzia programistyczne otwórz pozycję **Rozszerzenia**.</span><span class="sxs-lookup"><span data-stu-id="d8567-135">In Azure, open the web app control blade, and under Development Tools, open **Extensions**.</span></span> <span data-ttu-id="d8567-136">Usuń rozszerzenie usługi Application Insights.</span><span class="sxs-lookup"><span data-stu-id="d8567-136">Delete the Application Insights extension.</span></span> <span data-ttu-id="d8567-137">Następnie w obszarze Monitorowanie wybierz pozycję Application Insights i utwórz lub wybierz żądany zasób.</span><span class="sxs-lookup"><span data-stu-id="d8567-137">Then under Monitoring, choose Application Insights and create or select the resource you want.</span></span>

## <a name="build-the-app-with-application-insights"></a><span data-ttu-id="d8567-138">Skompiluj aplikację za pomocą usługi Application Insights</span><span class="sxs-lookup"><span data-stu-id="d8567-138">Build the app with Application Insights</span></span>
<span data-ttu-id="d8567-139">Usługa Application Insights może zapewnić bardziej szczegółową telemetrię dzięki instalacji zestawu SDK w Twojej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="d8567-139">Application Insights can provide more detailed telemetry by installing an SDK into your app.</span></span> <span data-ttu-id="d8567-140">W szczególności możesz gromadzić dzienniki śledzenia, [zapisywać niestandardową telemetrię](app-insights-api-custom-events-metrics.md) i uzyskiwać bardziej szczegółowe raporty o wyjątkach.</span><span class="sxs-lookup"><span data-stu-id="d8567-140">In particular, you can collect trace logs, [write custom telemetry](app-insights-api-custom-events-metrics.md), and get more detailed exception reports.</span></span>

1. <span data-ttu-id="d8567-141">**W programie Visual Studio** (2013 Update 2 lub nowszym) skonfiguruj usługę Application Insights dla projektu.</span><span class="sxs-lookup"><span data-stu-id="d8567-141">**In Visual Studio** (2013 update 2 or later), configure Application Insights for your project.</span></span>

    <span data-ttu-id="d8567-142">Kliknij prawym przyciskiem myszy projekt sieci Web i wybierz pozycje **Dodaj > Application Insights** lub **Konfiguruj usługę Application Insights**.</span><span class="sxs-lookup"><span data-stu-id="d8567-142">Right-click the web project, and select **Add > Application Insights** or **Configure Application Insights**.</span></span>
   
    ![Kliknij prawym przyciskiem myszy projekt sieci Web i pozycję Dodaj lub Konfiguruj usługę Application Insights](./media/app-insights-azure-web-apps/03-add.png)
   
    <span data-ttu-id="d8567-144">Jeśli pojawi się prośba o zalogowanie, użyj poświadczeń konta platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="d8567-144">If you're asked to sign in, use the credentials for your Azure account.</span></span>
   
    <span data-ttu-id="d8567-145">Operacja ma dwa skutki:</span><span class="sxs-lookup"><span data-stu-id="d8567-145">The operation has two effects:</span></span>
   
   1. <span data-ttu-id="d8567-146">Tworzy zasób usługi Application Insights na platformie Azure, gdzie telemetria jest przechowywana, analizowana i wyświetlana.</span><span class="sxs-lookup"><span data-stu-id="d8567-146">Creates an Application Insights resource in Azure, where telemetry is stored, analyzed and displayed.</span></span>
   2. <span data-ttu-id="d8567-147">Dodaje pakiet aplikacji NuGet usługi Application Insights do kodu (jeśli jeszcze go tam nie ma) i konfiguruje go do wysyłania telemetrii do zasobu platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="d8567-147">Adds the Application Insights NuGet package to your code (if it isn't there already), and configures it to send telemetry to the Azure resource.</span></span>
2. <span data-ttu-id="d8567-148">**Przetestuj telemetrię**, uruchamiając aplikację na komputerze deweloperskim (F5).</span><span class="sxs-lookup"><span data-stu-id="d8567-148">**Test the telemetry** by running the app in your development machine (F5).</span></span>
3. <span data-ttu-id="d8567-149">**Opublikuj aplikację** na platformie Azure w zwykły sposób.</span><span class="sxs-lookup"><span data-stu-id="d8567-149">**Publish the app** to Azure in the usual way.</span></span> 

<span data-ttu-id="d8567-150">*Jak przełączyć się na wysyłanie do innego zasobu usługi Application Insights?*</span><span class="sxs-lookup"><span data-stu-id="d8567-150">*How do I switch to sending to a different Application Insights resource?*</span></span>

* <span data-ttu-id="d8567-151">W programie Visual Studio kliknij prawym przyciskiem myszy projekt, wybierz pozycję **Konfiguruj usługę Application Insights**, a następnie wybierz żądany zasób.</span><span class="sxs-lookup"><span data-stu-id="d8567-151">In Visual Studio, right-click the project, choose **Configure Application Insights** and choose the resource you want.</span></span> <span data-ttu-id="d8567-152">Uzyskasz opcję tworzenia nowego zasobu.</span><span class="sxs-lookup"><span data-stu-id="d8567-152">You get the option to create a new resource.</span></span> <span data-ttu-id="d8567-153">Ponownie skompiluj i wdróż.</span><span class="sxs-lookup"><span data-stu-id="d8567-153">Rebuild and redeploy.</span></span>

## <a name="explore-the-data"></a><span data-ttu-id="d8567-154">Eksplorowanie danych</span><span class="sxs-lookup"><span data-stu-id="d8567-154">Explore the data</span></span>
1. <span data-ttu-id="d8567-155">W bloku usługi Application Insights panelu sterowania aplikacji sieci Web pojawi się obszar Metryki na żywo, który pokazuje żądania i błędy po upływie sekundy lub dwóch od chwili ich wystąpienia.</span><span class="sxs-lookup"><span data-stu-id="d8567-155">On the Application Insights blade of your web app control panel, you see Live Metrics, which shows requests and failures within a second or two of them occurring.</span></span> <span data-ttu-id="d8567-156">Jest to bardzo przydatny widok w przypadku ponownego publikowania aplikacji — natychmiast zobaczysz wszelkie problemy.</span><span class="sxs-lookup"><span data-stu-id="d8567-156">It's very useful display when you're republishing your app - you can see any problems immediately.</span></span>
2. <span data-ttu-id="d8567-157">Kliknij elementy, aby przejść do pełnego zasobu usługi Application Insights.</span><span class="sxs-lookup"><span data-stu-id="d8567-157">Click through to the full Application Insights resource.</span></span>

    ![Kliknij elementy](./media/app-insights-azure-web-apps/view-in-application-insights.png)

    <span data-ttu-id="d8567-159">Możesz tam przejść również bezpośrednio z nawigacji zasobów platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="d8567-159">You can also go there either directly from Azure resource navigation.</span></span>

1. <span data-ttu-id="d8567-160">Kliknij elementy któregokolwiek z wykresów, aby uzyskać więcej szczegółów:</span><span class="sxs-lookup"><span data-stu-id="d8567-160">Click through any chart to get more detail:</span></span>
   
    ![W bloku przeglądu usługi Application Insights kliknij wykres](./media/app-insights-azure-web-apps/07-dependency.png)
   
    <span data-ttu-id="d8567-162">Możesz [dostosować bloki metryk](app-insights-metrics-explorer.md).</span><span class="sxs-lookup"><span data-stu-id="d8567-162">You can [customize metrics blades](app-insights-metrics-explorer.md).</span></span>
2. <span data-ttu-id="d8567-163">Klikaj dalej elementy, aby zobaczyć poszczególne zdarzenia i ich właściwości:</span><span class="sxs-lookup"><span data-stu-id="d8567-163">Click through further to see individual events and their properties:</span></span>
   
    ![Kliknij typ zdarzenia, aby otworzyć wyszukiwanie filtrowane według danego typu](./media/app-insights-azure-web-apps/08-requests.png)
   
    <span data-ttu-id="d8567-165">Zwróć uwagę na link „...”, aby otworzyć wszystkie właściwości.</span><span class="sxs-lookup"><span data-stu-id="d8567-165">Notice the "..." link to open all properties.</span></span>
   
    <span data-ttu-id="d8567-166">Możesz [dostosować wyszukiwania](app-insights-diagnostic-search.md).</span><span class="sxs-lookup"><span data-stu-id="d8567-166">You can [customize searches](app-insights-diagnostic-search.md).</span></span>

<span data-ttu-id="d8567-167">Aby skorzystać z bardziej zaawansowanego wyszukiwania w ramach telemetrii, użyj [języka zapytań usługi Log Analytics](app-insights-analytics-tour.md).</span><span class="sxs-lookup"><span data-stu-id="d8567-167">For more powerful searches over your telemetry, use the [Log Analytics query language](app-insights-analytics-tour.md).</span></span>

## <a name="more-telemetry"></a><span data-ttu-id="d8567-168">Dalsze funkcje telemetrii</span><span class="sxs-lookup"><span data-stu-id="d8567-168">More telemetry</span></span>

* [<span data-ttu-id="d8567-169">Dane ładowania strony sieci Web</span><span class="sxs-lookup"><span data-stu-id="d8567-169">Web page load data</span></span>](app-insights-javascript.md)
* [<span data-ttu-id="d8567-170">Telemetria niestandardowa</span><span class="sxs-lookup"><span data-stu-id="d8567-170">Custom telemetry</span></span>](app-insights-api-custom-events-metrics.md)

## <a name="video"></a><span data-ttu-id="d8567-171">Połączenia wideo</span><span class="sxs-lookup"><span data-stu-id="d8567-171">Video</span></span>

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/100/player]

## <a name="next-steps"></a><span data-ttu-id="d8567-172">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="d8567-172">Next steps</span></span>
* <span data-ttu-id="d8567-173">[Uruchom profilera aplikacji na żywo](app-insights-profiler.md).</span><span class="sxs-lookup"><span data-stu-id="d8567-173">[Run the profiler on your live app](app-insights-profiler.md).</span></span>
* <span data-ttu-id="d8567-174">[Azure Functions](https://github.com/christopheranderson/azure-functions-app-insights-sample) — monitorowanie usługi Azure Functions za pomocą usługi Application Insights</span><span class="sxs-lookup"><span data-stu-id="d8567-174">[Azure Functions](https://github.com/christopheranderson/azure-functions-app-insights-sample) - monitor Azure Functions with Application Insights</span></span>
* <span data-ttu-id="d8567-175">[Włącz diagnostykę platformy Azure](app-insights-azure-diagnostics.md), która ma być wysyłana do usługi Application Insights.</span><span class="sxs-lookup"><span data-stu-id="d8567-175">[Enable Azure diagnostics](app-insights-azure-diagnostics.md) to be sent to Application Insights.</span></span>
* <span data-ttu-id="d8567-176">[Monitoruj metryki kondycji usługi](../monitoring-and-diagnostics/insights-how-to-customize-monitoring.md), aby upewnić się, że usługa jest dostępna i szybko reaguje.</span><span class="sxs-lookup"><span data-stu-id="d8567-176">[Monitor service health metrics](../monitoring-and-diagnostics/insights-how-to-customize-monitoring.md) to make sure your service is available and responsive.</span></span>
* <span data-ttu-id="d8567-177">[Odbieraj powiadomienia o alertach](../monitoring-and-diagnostics/insights-receive-alert-notifications.md) zawsze, gdy wystąpią zdarzenia operacyjne lub metryki przekroczą próg.</span><span class="sxs-lookup"><span data-stu-id="d8567-177">[Receive alert notifications](../monitoring-and-diagnostics/insights-receive-alert-notifications.md) whenever operational events happen or metrics cross a threshold.</span></span>
* <span data-ttu-id="d8567-178">Użyj pozycji [Usługa Application Insights dla aplikacji JavaScript i stron sieci Web](app-insights-javascript.md), aby pobrać telemetrię klienta z przeglądarek, w których odwiedzono stronę sieci Web.</span><span class="sxs-lookup"><span data-stu-id="d8567-178">Use [Application Insights for JavaScript apps and web pages](app-insights-javascript.md) to get client telemetry from the browsers that visit a web page.</span></span>
* <span data-ttu-id="d8567-179">[Konfiguruj testy sieci Web dostępności](app-insights-monitor-web-app-availability.md), aby otrzymywać alerty, gdy witryna nie działa.</span><span class="sxs-lookup"><span data-stu-id="d8567-179">[Set up Availability web tests](app-insights-monitor-web-app-availability.md) to be alerted if your site is down.</span></span>

