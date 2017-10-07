---
title: role serwera i proces roboczy Insights aplikacji dla systemu Windows aaaAzure | Dokumentacja firmy Microsoft
description: "Ręcznie Dodaj użycia tooanalyze aplikacji ASP.NET tooyour hello zestaw SDK usługi Application Insights, dostępności i wydajności."
services: application-insights
documentationcenter: .net
author: CFreemanwa
manager: carmonm
ms.assetid: 106ba99b-b57a-43b8-8866-e02f626c8190
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: get-started-article
ms.date: 05/15/2017
ms.author: bwren
ms.openlocfilehash: 64643ef637195d10f87fc6020a77169bca66c1f1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="manually-configure-application-insights-for-net-applications"></a><span data-ttu-id="70d28-103">Ręczne konfigurowanie aplikacji Application Insights dla aplikacji platformy .NET</span><span class="sxs-lookup"><span data-stu-id="70d28-103">Manually configure Application Insights for .NET applications</span></span>

<span data-ttu-id="70d28-104">Można skonfigurować [usługi Application Insights](app-insights-overview.md) toomonitor szerokiej gamy aplikacje lub role w aplikacji, składników lub mikrousług.</span><span class="sxs-lookup"><span data-stu-id="70d28-104">You can configure [Application Insights](app-insights-overview.md) toomonitor a wide variety of applications or application roles, components, or microservices.</span></span> <span data-ttu-id="70d28-105">Program Visual Studio oferuje [jednoetapową konfigurację](app-insights-asp-net.md) usług i aplikacji sieci Web.</span><span class="sxs-lookup"><span data-stu-id="70d28-105">For web apps and services, Visual Studio offers [one-step configuration](app-insights-asp-net.md).</span></span> <span data-ttu-id="70d28-106">W przypadku innych typów aplikacji platformy .NET, takich jak role serwera wewnętrznej bazy danych lub aplikacje klasyczne, można ręcznie skonfigurować usługi Application Insights.</span><span class="sxs-lookup"><span data-stu-id="70d28-106">For other types of .NET application, such as backend server roles or desktop applications, you can configure Application Insights manually.</span></span>

![Przykładowe wykresy monitorowania wydajności](./media/app-insights-windows-services/10-perf.png)

#### <a name="before-you-start"></a><span data-ttu-id="70d28-108">Przed rozpoczęciem</span><span class="sxs-lookup"><span data-stu-id="70d28-108">Before you start</span></span>

<span data-ttu-id="70d28-109">Potrzebne elementy:</span><span class="sxs-lookup"><span data-stu-id="70d28-109">You need:</span></span>

* <span data-ttu-id="70d28-110">Subskrypcja zbyt[Microsoft Azure](http://azure.com).</span><span class="sxs-lookup"><span data-stu-id="70d28-110">A subscription too[Microsoft Azure](http://azure.com).</span></span> <span data-ttu-id="70d28-111">Jeśli zespół lub organizacja ma subskrypcję platformy Azure, hello może dodać możesz tooit, za pomocą programu [konta Microsoft](http://live.com).</span><span class="sxs-lookup"><span data-stu-id="70d28-111">If your team or organization has an Azure subscription, hello owner can add you tooit, using your [Microsoft account](http://live.com).</span></span>
* <span data-ttu-id="70d28-112">Program Visual Studio 2013 lub nowszy.</span><span class="sxs-lookup"><span data-stu-id="70d28-112">Visual Studio 2013 or later.</span></span>

## <span data-ttu-id="70d28-113"><a name="add"></a>1. Wybieranie zasobu usługi Application Insights</span><span class="sxs-lookup"><span data-stu-id="70d28-113"><a name="add"></a>1. Choose an Application Insights resource</span></span>

<span data-ttu-id="70d28-114">zasób"Hello" jest których dane są zbierane i wyświetlane w portalu Azure hello.</span><span class="sxs-lookup"><span data-stu-id="70d28-114">hello 'resource' is where your data is collected and displayed in hello Azure portal.</span></span> <span data-ttu-id="70d28-115">Określa, czy należy toodecide toocreate nowy lub istniejący udział.</span><span class="sxs-lookup"><span data-stu-id="70d28-115">You need toodecide whether toocreate a new one, or share an existing one.</span></span>

### <a name="part-of-a-larger-app-use-existing-resource"></a><span data-ttu-id="70d28-116">Część większej aplikacji: użyj istniejącego zasobu</span><span class="sxs-lookup"><span data-stu-id="70d28-116">Part of a larger app: Use existing resource</span></span>

<span data-ttu-id="70d28-117">Jeśli aplikacja sieci web ma kilka składników — na przykład aplikacji frontonu sieci web i co najmniej jednej usługi zaplecza -, należy wysłać dane telemetryczne z wszystkich toohello składniki hello tego samego zasobu.</span><span class="sxs-lookup"><span data-stu-id="70d28-117">If your web application has several components - for example, a front-end web app and one or more back-end services - then you should send telemetry from all hello components toohello same resource.</span></span> <span data-ttu-id="70d28-118">Spowoduje to je włączyć toobe wyświetlone na mapie jednej aplikacji i była możliwa tootrace żądania tooanother jeden składnik.</span><span class="sxs-lookup"><span data-stu-id="70d28-118">This will enable them toobe displayed on a single Application Map, and make it possible tootrace a request from one component tooanother.</span></span>

<span data-ttu-id="70d28-119">Tak, jeśli jest już monitorowania innych składników tej aplikacji, następnie użyj tylko hello sam zasobów.</span><span class="sxs-lookup"><span data-stu-id="70d28-119">So, if you're already monitoring other components of this app, then just use hello same resource.</span></span>

<span data-ttu-id="70d28-120">Otwórz hello zasobów w hello [portalu Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="70d28-120">Open hello resource in hello [Azure portal](https://portal.azure.com/).</span></span> 

### <a name="self-contained-app-create-a-new-resource"></a><span data-ttu-id="70d28-121">Aplikacja samodzielna: utwórz nowy zasób</span><span class="sxs-lookup"><span data-stu-id="70d28-121">Self-contained app: Create a new resource</span></span>

<span data-ttu-id="70d28-122">Jeśli nowa aplikacja hello jest aplikacji niezwiązanych ze sobą tooother powinny mieć własny zasobów.</span><span class="sxs-lookup"><span data-stu-id="70d28-122">If hello new app is unrelated tooother applications, then it should have its own resource.</span></span>

<span data-ttu-id="70d28-123">Zaloguj się toohello [portalu Azure](https://portal.azure.com/)i utworzyć nowy zasób usługi Application Insights.</span><span class="sxs-lookup"><span data-stu-id="70d28-123">Sign in toohello [Azure portal](https://portal.azure.com/), and create a new Application Insights resource.</span></span> <span data-ttu-id="70d28-124">Wybierz platformy ASP.NET, jako typ aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="70d28-124">Choose ASP.NET as hello application type.</span></span>

![Kliknij kolejno polecenia Nowy, Application Insights](./media/app-insights-windows-services/01-new-asp.png)

<span data-ttu-id="70d28-126">Wybrany typ aplikacji Hello ustawia zawartości domyślnej hello hello zasobów kart.</span><span class="sxs-lookup"><span data-stu-id="70d28-126">hello choice of application type sets hello default content of hello resource blades.</span></span>

## <a name="2-copy-hello-instrumentation-key"></a><span data-ttu-id="70d28-127">2. Skopiuj hello klucza Instrumentacji</span><span class="sxs-lookup"><span data-stu-id="70d28-127">2. Copy hello Instrumentation Key</span></span>
<span data-ttu-id="70d28-128">klucz Hello identyfikuje hello zasobów.</span><span class="sxs-lookup"><span data-stu-id="70d28-128">hello key identifies hello resource.</span></span> <span data-ttu-id="70d28-129">Zainstaluj ją szybko w hello zestawu SDK, w kolejności toodirect danych toohello zasobów.</span><span class="sxs-lookup"><span data-stu-id="70d28-129">You'll install it soon in hello SDK, in order toodirect data toohello resource.</span></span>

![Kliknij polecenie Właściwości, wybierz hello klucza, a następnie naciśnij klawisze ctrl + C](./media/app-insights-windows-services/02-props-asp.png)

## <span data-ttu-id="70d28-131"><a name="sdk"></a>3. Zainstaluj pakiet usługi Application Insights hello w aplikacji</span><span class="sxs-lookup"><span data-stu-id="70d28-131"><a name="sdk"></a>3. Install hello Application Insights package in your application</span></span>
<span data-ttu-id="70d28-132">Instalowanie i konfigurowanie usługi Application Insights hello pakietu różni się w zależności od platformy hello, nad którymi pracuje.</span><span class="sxs-lookup"><span data-stu-id="70d28-132">Installing and configuring hello Application Insights package varies depending on hello platform you're working on.</span></span> 

1. <span data-ttu-id="70d28-133">W programie Visual Studio kliknij projekt prawym przyciskiem myszy i wybierz polecenie **Zarządzaj pakietami Nuget**.</span><span class="sxs-lookup"><span data-stu-id="70d28-133">In Visual Studio, right-click your project and choose **Manage Nuget Packages**.</span></span>
   
    ![Kliknij prawym przyciskiem myszy projekt hello i wybierz opcję Zarządzaj pakietami Nuget](./media/app-insights-windows-services/03-nuget.png)
2. <span data-ttu-id="70d28-135">Zainstaluj hello pakiet usługi Application Insights dla aplikacji serwera systemu Windows, "Microsoft.ApplicationInsights.WindowsServer."</span><span class="sxs-lookup"><span data-stu-id="70d28-135">Install hello Application Insights package for Windows server apps, "Microsoft.ApplicationInsights.WindowsServer."</span></span>
   
    ![Wyszukaj „Application Insights”](./media/app-insights-windows-services/04-ai-nuget.png)
   
    <span data-ttu-id="70d28-137">*Która wersja?*</span><span class="sxs-lookup"><span data-stu-id="70d28-137">*Which version?*</span></span>

    <span data-ttu-id="70d28-138">Sprawdź **Uwzględnij wersję wstępną** Jeśli chcesz tootry naszych najnowszych funkcji.</span><span class="sxs-lookup"><span data-stu-id="70d28-138">Check **Include prerelease** if you want tootry our latest features.</span></span> <span data-ttu-id="70d28-139">dokumenty Hello lub blogów należy pamiętać, czy potrzebujesz wersji wstępnej.</span><span class="sxs-lookup"><span data-stu-id="70d28-139">hello relevant documents or blogs note whether you need a prerelease version.</span></span>
    
    <span data-ttu-id="70d28-140">*Czy mogę użyć innych pakietów?*</span><span class="sxs-lookup"><span data-stu-id="70d28-140">*Can I use other packages?*</span></span>
   
    <span data-ttu-id="70d28-141">Tak.</span><span class="sxs-lookup"><span data-stu-id="70d28-141">Yes.</span></span> <span data-ttu-id="70d28-142">Wybierz "Microsoft.ApplicationInsights", jeśli mają toouse hello interfejsu API toosend własnych danych telemetrycznych.</span><span class="sxs-lookup"><span data-stu-id="70d28-142">Choose "Microsoft.ApplicationInsights" if you only want toouse hello API toosend your own telemetry.</span></span> <span data-ttu-id="70d28-143">Hello pakietu systemu Windows Server zawiera hello interfejsu API oraz wiele innych pakietów, takich jak zbieranie danych licznika wydajności i monitorowania zależności.</span><span class="sxs-lookup"><span data-stu-id="70d28-143">hello Windows Server package includes hello API plus a number of other packages such as performance counter collection and dependency monitoring.</span></span> 

### <a name="tooupgrade-toofuture-package-versions"></a><span data-ttu-id="70d28-144">wersje pakietów toofuture tooupgrade</span><span class="sxs-lookup"><span data-stu-id="70d28-144">tooupgrade toofuture package versions</span></span>
<span data-ttu-id="70d28-145">Wydania nowej wersji hello zestawu SDK z tootime czasu.</span><span class="sxs-lookup"><span data-stu-id="70d28-145">We release a new version of hello SDK from time tootime.</span></span>

<span data-ttu-id="70d28-146">tooupgrade tooa [nową wersję pakietu hello](https://github.com/Microsoft/ApplicationInsights-dotnet-server/releases/), otwórz ponownie Menedżera pakietów NuGet i odfiltrować zainstalowanych pakietów.</span><span class="sxs-lookup"><span data-stu-id="70d28-146">tooupgrade tooa [new release of hello package](https://github.com/Microsoft/ApplicationInsights-dotnet-server/releases/), open NuGet package manager again and filter on installed packages.</span></span> <span data-ttu-id="70d28-147">Wybierz pakiet **Microsoft.ApplicationInsights.WindowsServer** i kliknij pozycję **Uaktualnij**.</span><span class="sxs-lookup"><span data-stu-id="70d28-147">Select **Microsoft.ApplicationInsights.WindowsServer** and choose **Upgrade**.</span></span>

<span data-ttu-id="70d28-148">Jeśli wprowadzono tooApplicationInsights.config wszelkie dostosowania Zapisz jego kopię przed uaktualniania, a następnie scal zmiany w hello nowej wersji.</span><span class="sxs-lookup"><span data-stu-id="70d28-148">If you made any customizations tooApplicationInsights.config, save a copy of it before you upgrade, and afterwards merge your changes into hello new version.</span></span>

## <a name="4-send-telemetry"></a><span data-ttu-id="70d28-149">4. Wysyłanie danych telemetrycznych</span><span class="sxs-lookup"><span data-stu-id="70d28-149">4. Send telemetry</span></span>
<span data-ttu-id="70d28-150">**Jeśli zainstalowano tylko pakiet hello interfejsu API:**</span><span class="sxs-lookup"><span data-stu-id="70d28-150">**If you installed only hello API package:**</span></span>

* <span data-ttu-id="70d28-151">Ustaw hello klucza Instrumentacji w kodzie, na przykład `main()`:</span><span class="sxs-lookup"><span data-stu-id="70d28-151">Set hello instrumentation key in code, for example in `main()`:</span></span> 
  
    <span data-ttu-id="70d28-152">`TelemetryConfiguration.Active.InstrumentationKey = "` *Twój klucz* `";`</span><span class="sxs-lookup"><span data-stu-id="70d28-152">`TelemetryConfiguration.Active.InstrumentationKey = "` *your key* `";`</span></span> 
* <span data-ttu-id="70d28-153">[Pisanie własnych telemetrii przy użyciu interfejsu API hello](app-insights-api-custom-events-metrics.md#ikey).</span><span class="sxs-lookup"><span data-stu-id="70d28-153">[Write your own telemetry using hello API](app-insights-api-custom-events-metrics.md#ikey).</span></span>

<span data-ttu-id="70d28-154">**Jeśli zainstalowano innych pakietów usługi Application Insights** można również używać klucza Instrumentacji hello tooset pliku .config hello:</span><span class="sxs-lookup"><span data-stu-id="70d28-154">**If you installed other Application Insights packages,** you can, if you prefer, use hello .config file tooset hello instrumentation key:</span></span>

* <span data-ttu-id="70d28-155">Edytuj ApplicationInsights.config (który został dodany przez hello instalowania NuGet).</span><span class="sxs-lookup"><span data-stu-id="70d28-155">Edit ApplicationInsights.config (which was added by hello NuGet install).</span></span> <span data-ttu-id="70d28-156">Wstaw to bezpośrednio przed hello tagu zamykającego:</span><span class="sxs-lookup"><span data-stu-id="70d28-156">Insert this just before hello closing tag:</span></span>
  
    <span data-ttu-id="70d28-157">`<InstrumentationKey>`*klucza Instrumentacji hello skopiowany*`</InstrumentationKey>`</span><span class="sxs-lookup"><span data-stu-id="70d28-157">`<InstrumentationKey>` *hello instrumentation key you copied* `</InstrumentationKey>`</span></span>
* <span data-ttu-id="70d28-158">Upewnij się, że zbyt ustawić właściwości hello ApplicationInsights.config w Eksploratorze rozwiązań**Akcja kompilacji = zawartość, tooOutput kopiowania katalogu = kopiowania**.</span><span class="sxs-lookup"><span data-stu-id="70d28-158">Make sure that hello properties of ApplicationInsights.config in Solution Explorer are set too**Build Action = Content, Copy tooOutput Directory = Copy**.</span></span>

<span data-ttu-id="70d28-159">Jeśli ma zbyt jest przydatne tooset klucza Instrumentacji hello w kodzie[przełącznika hello klucz dla konfiguracji kompilacji różnych](app-insights-separate-resources.md).</span><span class="sxs-lookup"><span data-stu-id="70d28-159">It's useful tooset hello instrumentation key in code if you want too[switch hello key for different build configurations](app-insights-separate-resources.md).</span></span> <span data-ttu-id="70d28-160">Po ustawieniu klucza hello w kodzie nie ma tooset w hello `.config` pliku.</span><span class="sxs-lookup"><span data-stu-id="70d28-160">If you set hello key in code, you don't have tooset it in hello `.config` file.</span></span>

## <span data-ttu-id="70d28-161"><a name="run"></a> Uruchamianie projektu</span><span class="sxs-lookup"><span data-stu-id="70d28-161"><a name="run"></a> Run your project</span></span>
<span data-ttu-id="70d28-162">Użyj hello **F5** toorun aplikacji i wypróbować jej możliwości: otwarte innej strony toogenerate niektóre telemetrii.</span><span class="sxs-lookup"><span data-stu-id="70d28-162">Use hello **F5** toorun your application and try it out: open different pages toogenerate some telemetry.</span></span>

<span data-ttu-id="70d28-163">W programie Visual Studio zostanie wyświetlona liczba hello zdarzenia, które zostały wysłane.</span><span class="sxs-lookup"><span data-stu-id="70d28-163">In Visual Studio, you'll see a count of hello events that have been sent.</span></span>

![Liczba zdarzeń w programie Visual Studio](./media/app-insights-windows-services/appinsights-09eventcount.png)

## <span data-ttu-id="70d28-165"><a name="monitor"></a> Wyświetlanie telemetrii</span><span class="sxs-lookup"><span data-stu-id="70d28-165"><a name="monitor"></a> View your telemetry</span></span>
<span data-ttu-id="70d28-166">Zwraca toohello [portalu Azure](https://portal.azure.com/) i Przeglądaj tooyour zasobu usługi Application Insights.</span><span class="sxs-lookup"><span data-stu-id="70d28-166">Return toohello [Azure portal](https://portal.azure.com/) and browse tooyour Application Insights resource.</span></span>

<span data-ttu-id="70d28-167">Wyszukiwać dane na wykresach omówienie hello.</span><span class="sxs-lookup"><span data-stu-id="70d28-167">Look for data in hello Overview charts.</span></span> <span data-ttu-id="70d28-168">Na początku zobaczysz tylko jeden lub dwa punkty.</span><span class="sxs-lookup"><span data-stu-id="70d28-168">At first, you'll just see one or two points.</span></span> <span data-ttu-id="70d28-169">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="70d28-169">For example:</span></span>

![Kliknij go, toomore danych](./media/app-insights-windows-services/12-first-perf.png)

<span data-ttu-id="70d28-171">Kliknij przycisk za pomocą dowolnego toosee wykresu bardziej szczegółowe metryki.</span><span class="sxs-lookup"><span data-stu-id="70d28-171">Click through any chart toosee more detailed metrics.</span></span> [<span data-ttu-id="70d28-172">Dowiedz się więcej o metrykach.</span><span class="sxs-lookup"><span data-stu-id="70d28-172">Learn more about metrics.</span></span>](app-insights-web-monitor-performance.md)

### <a name="no-data"></a><span data-ttu-id="70d28-173">Brak danych?</span><span class="sxs-lookup"><span data-stu-id="70d28-173">No data?</span></span>
* <span data-ttu-id="70d28-174">Za pomocą aplikacji hello, otwieranie stron różnych, dzięki czemu generuje niektóre dane telemetryczne.</span><span class="sxs-lookup"><span data-stu-id="70d28-174">Use hello application, opening different pages so that it generates some telemetry.</span></span>
* <span data-ttu-id="70d28-175">Otwórz hello [wyszukiwania](app-insights-diagnostic-search.md) kafelka toosee pojedynczych zdarzeń.</span><span class="sxs-lookup"><span data-stu-id="70d28-175">Open hello [Search](app-insights-diagnostic-search.md) tile, toosee individual events.</span></span> <span data-ttu-id="70d28-176">Czasami potrzebny zdarzenia nieco podczas dłużej tooget przez potok metryki hello.</span><span class="sxs-lookup"><span data-stu-id="70d28-176">Sometimes it takes events a little while longer tooget through hello metrics pipeline.</span></span>
* <span data-ttu-id="70d28-177">Odczekaj kilka sekund, a następnie kliknij przycisk **Odśwież**.</span><span class="sxs-lookup"><span data-stu-id="70d28-177">Wait a few seconds and click **Refresh**.</span></span> <span data-ttu-id="70d28-178">Wykresy odświeżania się okresowo, ale użytkownik może odświeżać ręcznie oczekiwania dla niektórych danych tooshow.</span><span class="sxs-lookup"><span data-stu-id="70d28-178">Charts refresh themselves periodically, but you can refresh manually if you're waiting for some data tooshow up.</span></span>
* <span data-ttu-id="70d28-179">Zobacz [Rozwiązywanie problemów](app-insights-troubleshoot-faq.md).</span><span class="sxs-lookup"><span data-stu-id="70d28-179">See [Troubleshooting](app-insights-troubleshoot-faq.md).</span></span>

## <a name="publish-your-app"></a><span data-ttu-id="70d28-180">Publikowanie aplikacji</span><span class="sxs-lookup"><span data-stu-id="70d28-180">Publish your app</span></span>
<span data-ttu-id="70d28-181">Teraz wdrożyć serwer tooyour aplikacji lub tooAzure i obejrzyj hello dane gromadzone.</span><span class="sxs-lookup"><span data-stu-id="70d28-181">Now deploy your application tooyour server or tooAzure and watch hello data accumulate.</span></span>

![Użyj programu Visual Studio toopublish aplikacji](./media/app-insights-windows-services/15-publish.png)

<span data-ttu-id="70d28-183">Podczas uruchamiania w trybie debugowania, telemetrii jest przyspieszone przez potok hello tak, aby powinny być widoczne dane znajdujące się w ciągu kilku sekund.</span><span class="sxs-lookup"><span data-stu-id="70d28-183">When you run in debug mode, telemetry is expedited through hello pipeline, so that you should see data appearing within seconds.</span></span> <span data-ttu-id="70d28-184">Po wdrożeniu aplikacji w konfiguracji wydania dane są gromadzone wolniej.</span><span class="sxs-lookup"><span data-stu-id="70d28-184">When you deploy your app in Release configuration, data accumulates more slowly.</span></span>

### <a name="no-data-after-you-publish-tooyour-server"></a><span data-ttu-id="70d28-185">Brak danych po opublikowaniu tooyour serwera?</span><span class="sxs-lookup"><span data-stu-id="70d28-185">No data after you publish tooyour server?</span></span>
<span data-ttu-id="70d28-186">Otwórz porty dla ruchu wychodzącego w zaporze serwera.</span><span class="sxs-lookup"><span data-stu-id="70d28-186">Open ports for outgoing traffic in your server's firewall.</span></span> <span data-ttu-id="70d28-187">Zobacz [tej strony](https://docs.microsoft.com/azure/application-insights/app-insights-ip-addresses) hello listę wymaganych adresów</span><span class="sxs-lookup"><span data-stu-id="70d28-187">See [this page](https://docs.microsoft.com/azure/application-insights/app-insights-ip-addresses) for hello list of required addresses</span></span> 

### <a name="trouble-on-your-build-server"></a><span data-ttu-id="70d28-188">Problem z serwerem kompilacji?</span><span class="sxs-lookup"><span data-stu-id="70d28-188">Trouble on your build server?</span></span>
<span data-ttu-id="70d28-189">Zobacz [ten punkt rozwiązywania problemów](app-insights-asp-net-troubleshoot-no-data.md#NuGetBuild).</span><span class="sxs-lookup"><span data-stu-id="70d28-189">Please see [this Troubleshooting item](app-insights-asp-net-troubleshoot-no-data.md#NuGetBuild).</span></span>

> [!NOTE]
> <span data-ttu-id="70d28-190">Jeśli aplikacja generuje wiele telemetrii, hello adaptacyjną próbkowania modułu automatycznie zmniejsza hello wolumin, który jest wysyłany portalu toohello wysyłając reprezentatywny część zdarzeń.</span><span class="sxs-lookup"><span data-stu-id="70d28-190">If your app generates a lot of telemetry, hello adaptive sampling module will automatically reduce hello volume that is sent toohello portal by sending only a representative fraction of events.</span></span> <span data-ttu-id="70d28-191">Jednak zdarzenia będące pokrewne toohello w jednym żądaniu będzie być zaznaczany lub odznaczany jako grupa, dzięki czemu można przechodzić między powiązanych zdarzeń.</span><span class="sxs-lookup"><span data-stu-id="70d28-191">However, events that are related toohello same request will be selected or deselected as a group, so that you can navigate between related events.</span></span> 
> <span data-ttu-id="70d28-192">[Więcej informacji na temat próbkowania](app-insights-sampling.md).</span><span class="sxs-lookup"><span data-stu-id="70d28-192">[Learn about sampling](app-insights-sampling.md).</span></span>
> 
> 

## <a name="video"></a><span data-ttu-id="70d28-193">Połączenia wideo</span><span class="sxs-lookup"><span data-stu-id="70d28-193">Video</span></span>

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/100/player]

## <a name="next-steps"></a><span data-ttu-id="70d28-194">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="70d28-194">Next steps</span></span>
* <span data-ttu-id="70d28-195">[Dodaj więcej danych telemetrycznych](app-insights-asp-net-more.md) tooget hello widok 360 stopni aplikacji.</span><span class="sxs-lookup"><span data-stu-id="70d28-195">[Add more telemetry](app-insights-asp-net-more.md) tooget hello full 360-degree view of your application.</span></span>

