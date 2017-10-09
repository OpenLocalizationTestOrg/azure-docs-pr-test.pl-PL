---
title: aaaAzure Application Insights migawki debugera w przypadku aplikacji .NET | Dokumentacja firmy Microsoft
description: "Debugowanie migawki są zbierane automatycznie, gdy wyjątki zostaną zgłoszone w aplikacjach .NET produkcji"
services: application-insights
documentationcenter: 
author: qubitron
manager: carmonm
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 07/03/2017
ms.author: bwren
ms.openlocfilehash: f0173a752b5795d934fbab1bd53eb077433edc90
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="debug-snapshots-on-exceptions-in-net-apps"></a><span data-ttu-id="d71a8-103">Debugowanie migawek na wyjątków w aplikacji .NET</span><span class="sxs-lookup"><span data-stu-id="d71a8-103">Debug snapshots on exceptions in .NET apps</span></span>

<span data-ttu-id="d71a8-104">Po wystąpieniu wyjątku, można automatycznie zbierać migawki debugowania aplikacji sieci web na żywo.</span><span class="sxs-lookup"><span data-stu-id="d71a8-104">When an exception occurs, you can automatically collect a debug snapshot from your live web application.</span></span> <span data-ttu-id="d71a8-105">migawki Hello pokazuje stan hello kodu źródłowego i zmiennych w hello obecnie hello wyjątek został zgłoszony.</span><span class="sxs-lookup"><span data-stu-id="d71a8-105">hello snapshot shows hello state of source code and variables at hello moment hello exception was thrown.</span></span> <span data-ttu-id="d71a8-106">Witaj migawki debugera (wersja zapoznawcza) w [Azure Application Insights](app-insights-overview.md) monitoruje dane telemetryczne wyjątku z aplikacji sieci web.</span><span class="sxs-lookup"><span data-stu-id="d71a8-106">hello Snapshot Debugger (preview) in [Azure Application Insights](app-insights-overview.md) monitors exception telemetry from your web app.</span></span> <span data-ttu-id="d71a8-107">Zbiera migawki na listy wyjątków zgłaszanie top, dzięki czemu masz hello informacje potrzebne toodiagnose problemów w środowisku produkcyjnym.</span><span class="sxs-lookup"><span data-stu-id="d71a8-107">It collects snapshots on your top-throwing exceptions so that you have hello information you need toodiagnose issues in production.</span></span> <span data-ttu-id="d71a8-108">Zawierają hello [pakietu NuGet modułu zbierającego migawki](http://www.nuget.org/packages/Microsoft.ApplicationInsights.SnapshotCollector) w aplikacji i opcjonalnie skonfigurować parametry kolekcji w [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md). Migawki są wyświetlane na [wyjątki](app-insights-asp-net-exceptions.md) w portalu usługi Application Insights hello.</span><span class="sxs-lookup"><span data-stu-id="d71a8-108">Include hello [Snapshot collector NuGet package](http://www.nuget.org/packages/Microsoft.ApplicationInsights.SnapshotCollector) in your application, and optionally configure collection parameters in [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md). Snapshots appear on [exceptions](app-insights-asp-net-exceptions.md) in hello Application Insights portal.</span></span>

<span data-ttu-id="d71a8-109">Można wyświetlić migawki debugowania w stosie wywołań hello portalu toosee hello i sprawdzić zmiennych w każdej ramki stosu wywołań.</span><span class="sxs-lookup"><span data-stu-id="d71a8-109">You can view debug snapshots in hello portal toosee hello call stack and inspect variables at each call stack frame.</span></span> <span data-ttu-id="d71a8-110">tooget bardziej wydajne działanie debugowania z kodem źródłowym, otwórz migawki z programu Visual Studio Enterprise 2017 przez [pobieranie hello debugera migawki rozszerzenia dla programu Visual Studio](https://aka.ms/snapshotdebugger).</span><span class="sxs-lookup"><span data-stu-id="d71a8-110">tooget a more powerful debugging experience with source code, open snapshots with Visual Studio 2017 Enterprise by [downloading hello Snapshot Debugger extension for Visual Studio](https://aka.ms/snapshotdebugger).</span></span>

<span data-ttu-id="d71a8-111">Kolekcja migawki jest dostępny dla:</span><span class="sxs-lookup"><span data-stu-id="d71a8-111">Snapshot collection is available for:</span></span>
* <span data-ttu-id="d71a8-112">Aplikacje środowiska .NET framework i program ASP.NET systemem .NET Framework 4.5 lub nowszej.</span><span class="sxs-lookup"><span data-stu-id="d71a8-112">.NET Framework and ASP.NET applications running .NET Framework 4.5 or later.</span></span>
* <span data-ttu-id="d71a8-113">.NET core 2.0 i ASP.NET Core 2.0 aplikacji uruchomionych w systemie Windows.</span><span class="sxs-lookup"><span data-stu-id="d71a8-113">.NET Core 2.0 and ASP.NET Core 2.0 applications running on Windows.</span></span>

### <a name="configure-snapshot-collection-for-aspnet-applications"></a><span data-ttu-id="d71a8-114">Konfigurowanie zbierania migawek dla aplikacji ASP.NET</span><span class="sxs-lookup"><span data-stu-id="d71a8-114">Configure snapshot collection for ASP.NET applications</span></span>

1. <span data-ttu-id="d71a8-115">[Włącz usługę Application Insights w aplikacji sieci web](app-insights-asp-net.md), jeśli nie jeszcze go jeszcze gotowe.</span><span class="sxs-lookup"><span data-stu-id="d71a8-115">[Enable Application Insights in your web app](app-insights-asp-net.md), if you haven't done it yet.</span></span>

2. <span data-ttu-id="d71a8-116">Zawierają hello [Microsoft.ApplicationInsights.SnapshotCollector](http://www.nuget.org/packages/Microsoft.ApplicationInsights.SnapshotCollector) pakietu NuGet w aplikacji.</span><span class="sxs-lookup"><span data-stu-id="d71a8-116">Include hello [Microsoft.ApplicationInsights.SnapshotCollector](http://www.nuget.org/packages/Microsoft.ApplicationInsights.SnapshotCollector) NuGet package in your app.</span></span> 

3. <span data-ttu-id="d71a8-117">Przejrzyj opcje domyślne hello hello pakietu dodane za[ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md):</span><span class="sxs-lookup"><span data-stu-id="d71a8-117">Review hello default options that hello package added too[ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md):</span></span>

    ```xml
    <TelemetryProcessors>
        <Add Type="Microsoft.ApplicationInsights.SnapshotCollector.SnapshotCollectorTelemetryProcessor, Microsoft.ApplicationInsights.SnapshotCollector">
        <!-- hello default is true, but you can disable Snapshot Debugging by setting it toofalse -->
        <IsEnabled>true</IsEnabled>
        <!-- Snapshot Debugging is usually disabled in developer mode, but you can enable it by setting this tootrue. -->
        <!-- DeveloperMode is a property on hello active TelemetryChannel. -->
        <IsEnabledInDeveloperMode>false</IsEnabledInDeveloperMode>
        <!-- How many times we need toosee an exception before we ask for snapshots. -->
        <ThresholdForSnapshotting>5</ThresholdForSnapshotting>
        <!-- hello maximum number of examples we create for a single problem. -->
        <MaximumSnapshotsRequired>3</MaximumSnapshotsRequired>
        <!-- hello maximum number of problems that we can be tracking at any time. -->
        <MaximumCollectionPlanSize>50</MaximumCollectionPlanSize>
        <!-- How often tooreset problem counters. -->
        <ProblemCounterResetInterval>06:00:00</ProblemCounterResetInterval>
        <!-- hello maximum number of snapshots allowed in one minute. -->
        <SnapshotsPerMinuteLimit>2</SnapshotsPerMinuteLimit>
        <!-- hello maximum number of snapshots allowed per day. -->
        <SnapshotsPerDayLimit>50</SnapshotsPerDayLimit>
        </Add>
    </TelemetryProcessors>
    ```

4. <span data-ttu-id="d71a8-118">Migawki są zbierane tylko na wyjątki, które zostały zgłoszone tooApplication szczegółowych informacji.</span><span class="sxs-lookup"><span data-stu-id="d71a8-118">Snapshots are collected only on exceptions that are reported tooApplication Insights.</span></span> <span data-ttu-id="d71a8-119">W niektórych przypadkach (na przykład starszych wersji platformy .NET hello) może być konieczne, zbyt[Konfigurowanie zbierania wyjątków](app-insights-asp-net-exceptions.md#exceptions) toosee wyjątki z migawkami w portalu hello.</span><span class="sxs-lookup"><span data-stu-id="d71a8-119">In some cases (for example, older versions of hello .NET platform), you might need too[configure exception collection](app-insights-asp-net-exceptions.md#exceptions) toosee exceptions with snapshots in hello portal.</span></span>


### <a name="configure-snapshot-collection-for-aspnet-core-20-applications"></a><span data-ttu-id="d71a8-120">Konfigurowanie zbierania migawek dla aplikacji platformy ASP.NET Core 2.0</span><span class="sxs-lookup"><span data-stu-id="d71a8-120">Configure snapshot collection for ASP.NET Core 2.0 applications</span></span>

1. <span data-ttu-id="d71a8-121">[Włącz usługę Application Insights w aplikacji sieci web platformy ASP.NET Core](app-insights-asp-net-core.md), jeśli nie jeszcze go jeszcze gotowe.</span><span class="sxs-lookup"><span data-stu-id="d71a8-121">[Enable Application Insights in your ASP.NET Core web app](app-insights-asp-net-core.md), if you haven't done it yet.</span></span>

2. <span data-ttu-id="d71a8-122">Zawierają hello [Microsoft.ApplicationInsights.SnapshotCollector](http://www.nuget.org/packages/Microsoft.ApplicationInsights.SnapshotCollector) pakietu NuGet w aplikacji.</span><span class="sxs-lookup"><span data-stu-id="d71a8-122">Include hello [Microsoft.ApplicationInsights.SnapshotCollector](http://www.nuget.org/packages/Microsoft.ApplicationInsights.SnapshotCollector) NuGet package in your app.</span></span>

3. <span data-ttu-id="d71a8-123">Modyfikowanie hello `ConfigureServices` metody w aplikacji `Startup` klasy tooadd hello migawki modułu zbierającego dane telemetryczne procesora.</span><span class="sxs-lookup"><span data-stu-id="d71a8-123">Modify hello `ConfigureServices` method in your application's `Startup` class tooadd hello Snapshot Collector's telemetry processor.</span></span> <span data-ttu-id="d71a8-124">należy dodać kodu Hello zależy od hello wersja przywoływanego hello pakietu Microsoft.ApplicationInsights.ASPNETCore NuGet.</span><span class="sxs-lookup"><span data-stu-id="d71a8-124">hello code you should add depends on hello referenced version of hello Microsoft.ApplicationInsights.ASPNETCore NuGet package.</span></span>

   <span data-ttu-id="d71a8-125">W przypadku Microsoft.ApplicationInsights.AspNetCore 2.1.0 należy dodać:</span><span class="sxs-lookup"><span data-stu-id="d71a8-125">For Microsoft.ApplicationInsights.AspNetCore 2.1.0 add:</span></span>
   ```C#
   using Microsoft.ApplicationInsights.SnapshotCollector;
   ...
   class Startup
   {
       // This method is called by hello runtime. Use it tooadd services toohello container.
       public void ConfigureServices(IServiceCollection services)
       {
           services.AddSingleton<Func<ITelemetryProcessor, ITelemetryProcessor>>(next => new SnapshotCollectorTelemetryProcessor(next));
           // TODO: Add any other services your application needs here.
       }
   }
   ```

   <span data-ttu-id="d71a8-126">W przypadku Microsoft.ApplicationInsights.AspNetCore 2.1.1 należy dodać:</span><span class="sxs-lookup"><span data-stu-id="d71a8-126">For Microsoft.ApplicationInsights.AspNetCore 2.1.1 add:</span></span>
   ```C#
   using Microsoft.ApplicationInsights.SnapshotCollector;
   ...
   class Startup
   {
       private class SnapshotCollectorTelemetryProcessorFactory : ITelemetryProcessorFactory
       {
           public ITelemetryProcessor Create(ITelemetryProcessor next) =>
               new SnapshotCollectorTelemetryProcessor(next);
       }

       // This method is called by hello runtime. Use it tooadd services toohello container.
       public void ConfigureServices(IServiceCollection services)
       {
            services.AddSingleton<ITelemetryProcessorFactory>(new SnapshotCollectorTelemetryProcessorFactory());
           // TODO: Add any other services your application needs here.
       }
   }
   ```

### <a name="configure-snapshot-collection-for-other-net-applications"></a><span data-ttu-id="d71a8-127">Konfigurowanie zbierania migawek dla innych aplikacji .NET</span><span class="sxs-lookup"><span data-stu-id="d71a8-127">Configure snapshot collection for other .NET applications</span></span>

1. <span data-ttu-id="d71a8-128">Jeśli aplikacja nie jest już instrumentowane przy użyciu usługi Application Insights, rozpoczęcie pracy przez [włączenie usługi Application Insights i ustawienie hello Instrumentacji klucza](app-insights-windows-desktop.md).</span><span class="sxs-lookup"><span data-stu-id="d71a8-128">If your application is not already instrumented with Application Insights, get started by [enabling Application Insights and setting hello instrumentation key](app-insights-windows-desktop.md).</span></span>

2. <span data-ttu-id="d71a8-129">Dodaj hello [Microsoft.ApplicationInsights.SnapshotCollector](http://www.nuget.org/packages/Microsoft.ApplicationInsights.SnapshotCollector) pakietu NuGet w aplikacji.</span><span class="sxs-lookup"><span data-stu-id="d71a8-129">Add hello [Microsoft.ApplicationInsights.SnapshotCollector](http://www.nuget.org/packages/Microsoft.ApplicationInsights.SnapshotCollector) NuGet package in your app.</span></span>

3. <span data-ttu-id="d71a8-130">Migawki są zbierane tylko na wyjątki, które zostały zgłoszone tooApplication szczegółowych informacji.</span><span class="sxs-lookup"><span data-stu-id="d71a8-130">Snapshots are collected only on exceptions that are reported tooApplication Insights.</span></span> <span data-ttu-id="d71a8-131">Może być konieczne toomodify Twojego tooreport kodu je.</span><span class="sxs-lookup"><span data-stu-id="d71a8-131">You may need toomodify your code tooreport them.</span></span> <span data-ttu-id="d71a8-132">Obsługa kodu wyjątków Hello zależy hello struktury aplikacji, ale przykładem jest poniżej:</span><span class="sxs-lookup"><span data-stu-id="d71a8-132">hello exception handling code depends on hello structure of your application, but an example is below:</span></span>
    ```C#
   TelemetryClient _telemetryClient = new TelemetryClient();

   void ExampleRequest()
   {
        try
        {
            // TODO: Handle hello request.
        }
        catch (Exception ex)
        {
            // Report hello exception tooApplication Insights.
            _telemetryClient.TrackException(ex);

            // TODO: Rethrow hello exception if desired.
        }
   }
    ```
    
## <a name="grant-permissions"></a><span data-ttu-id="d71a8-133">Udzielanie uprawnień</span><span class="sxs-lookup"><span data-stu-id="d71a8-133">Grant permissions</span></span>

<span data-ttu-id="d71a8-134">Właściciele hello subskrypcji platformy Azure można sprawdzić migawki.</span><span class="sxs-lookup"><span data-stu-id="d71a8-134">Owners of hello Azure subscription can inspect snapshots.</span></span> <span data-ttu-id="d71a8-135">Inni użytkownicy muszą mieć uprawnienie przez właściciela.</span><span class="sxs-lookup"><span data-stu-id="d71a8-135">Other users must be granted permission by an owner.</span></span>

<span data-ttu-id="d71a8-136">toogrant uprawnienia, przypisz hello `Application Insights Snapshot Debugger` toousers roli, który będzie przeprowadzał inspekcję migawki.</span><span class="sxs-lookup"><span data-stu-id="d71a8-136">toogrant permission, assign hello `Application Insights Snapshot Debugger` role toousers who will inspect snapshots.</span></span> <span data-ttu-id="d71a8-137">Tę rolę można przypisać tooindividual użytkowników lub grup właściciele subskrypcji dla docelowego hello zasobu usługi Application Insights lub grupy zasobów lub subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="d71a8-137">This role can be assigned tooindividual users or groups by subscription owners for hello target Application Insights resource or its resource group or subscription.</span></span>

1. <span data-ttu-id="d71a8-138">Otwiera blok kontroli dostępu (IAM) hello.</span><span class="sxs-lookup"><span data-stu-id="d71a8-138">Open hello Access Control (IAM) blade.</span></span>
1. <span data-ttu-id="d71a8-139">Kliknij przycisk Dodaj + hello.</span><span class="sxs-lookup"><span data-stu-id="d71a8-139">Click hello +Add button.</span></span>
1. <span data-ttu-id="d71a8-140">Wybierz debuger migawki Insights aplikacji z listy rozwijanej hello ról.</span><span class="sxs-lookup"><span data-stu-id="d71a8-140">Select Application Insights Snapshot Debugger from hello Roles drop-down list.</span></span>
1. <span data-ttu-id="d71a8-141">Wyszukaj, a następnie wprowadź nazwę hello tooadd użytkownika.</span><span class="sxs-lookup"><span data-stu-id="d71a8-141">Search for and enter a name for hello user tooadd.</span></span>
1. <span data-ttu-id="d71a8-142">Kliknij przycisk Zapisz hello tooadd roli toohello użytkownika hello.</span><span class="sxs-lookup"><span data-stu-id="d71a8-142">Click hello Save button tooadd hello user toohello role.</span></span>


[!IMPORTANT]
    <span data-ttu-id="d71a8-143">Migawki potencjalnie może zawierać informacje osobiste i innych poufnych w zmiennej i wartości parametrów.</span><span class="sxs-lookup"><span data-stu-id="d71a8-143">Snapshots can potentially contain personal and other sensitive information in variable and parameter values.</span></span>

## <a name="debug-snapshots-in-hello-application-insights-portal"></a><span data-ttu-id="d71a8-144">Debugowanie migawek w portalu usługi Application Insights hello</span><span class="sxs-lookup"><span data-stu-id="d71a8-144">Debug snapshots in hello Application Insights portal</span></span>

<span data-ttu-id="d71a8-145">Jeśli migawka jest dostępna dla danego wyjątku lub identyfikator problemu **Otwórz migawki debugowania** na powitania pojawi się przycisk [wyjątek](app-insights-asp-net-exceptions.md) w portalu usługi Application Insights hello.</span><span class="sxs-lookup"><span data-stu-id="d71a8-145">If a snapshot is available for a given exception or a problem ID, an **Open Debug Snapshot** button appears on hello [exception](app-insights-asp-net-exceptions.md) in hello Application Insights portal.</span></span>

![Przycisk Otwórz migawki debugowania na wyjątek](./media/app-insights-snapshot-debugger/snapshot-on-exception.png)

<span data-ttu-id="d71a8-147">W widoku debugowania migawki hello Zobacz stosu wywołań i okienku zmiennych.</span><span class="sxs-lookup"><span data-stu-id="d71a8-147">In hello Debug Snapshot view, you see a call stack and a variables pane.</span></span> <span data-ttu-id="d71a8-148">Po wybraniu ramki wywołania hello stosu w okienku Stos wywołań hello, można wyświetlić zmiennych lokalnych i wywołać parametrów dla tej funkcji w okienku zmienne hello.</span><span class="sxs-lookup"><span data-stu-id="d71a8-148">When you select frames of hello call stack in hello call stack pane, you can view local variables and parameters for that function call in hello variables pane.</span></span>

![Widok debugowania migawka w portalu hello](./media/app-insights-snapshot-debugger/open-snapshot-portal.png)

<span data-ttu-id="d71a8-150">Migawki mogą zawierać poufne informacje, i domyślnie nie są widoczne.</span><span class="sxs-lookup"><span data-stu-id="d71a8-150">Snapshots might contain sensitive information, and by default they are not viewable.</span></span> <span data-ttu-id="d71a8-151">migawki tooview musi mieć hello `Application Insights Snapshot Debugger` tooyou przypisanej roli.</span><span class="sxs-lookup"><span data-stu-id="d71a8-151">tooview snapshots, you must have hello `Application Insights Snapshot Debugger` role assigned tooyou.</span></span>

## <a name="debug-snapshots-with-visual-studio-2017-enterprise"></a><span data-ttu-id="d71a8-152">Migawki z programu Visual Studio Enterprise 2017 debugowania</span><span class="sxs-lookup"><span data-stu-id="d71a8-152">Debug snapshots with Visual Studio 2017 Enterprise</span></span>
1. <span data-ttu-id="d71a8-153">Kliknij przycisk hello **pobieranie migawki** toodownload przycisk `.diagsession` pliku, który można otworzyć w programie Visual Studio Enterprise 2017 r.</span><span class="sxs-lookup"><span data-stu-id="d71a8-153">Click hello **Download Snapshot** button toodownload a `.diagsession` file, which can be opened by Visual Studio 2017 Enterprise.</span></span> 

2. <span data-ttu-id="d71a8-154">Witaj tooopen `.diagsession` pliku, należy najpierw [Pobierz i zainstaluj rozszerzenie debugera migawki hello for Visual Studio](https://aka.ms/snapshotdebugger).</span><span class="sxs-lookup"><span data-stu-id="d71a8-154">tooopen hello `.diagsession` file, you must first [download and install hello Snapshot Debugger extension for Visual Studio](https://aka.ms/snapshotdebugger).</span></span>

3. <span data-ttu-id="d71a8-155">Po otwarciu pliku migawki hello, zostanie wyświetlona strona debugowania minizrzutu hello, w programie Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="d71a8-155">After you open hello snapshot file, hello Minidump Debugging page in Visual Studio appears.</span></span> <span data-ttu-id="d71a8-156">Kliknij przycisk **debugowania kodu zarządzanego** toostart debugowania hello migawki.</span><span class="sxs-lookup"><span data-stu-id="d71a8-156">Click **Debug Managed Code** toostart debugging hello snapshot.</span></span> <span data-ttu-id="d71a8-157">migawki Hello otwiera toohello wiersz kodu, w którym został zgłoszony wyjątek hello tak, aby umożliwić debugowanie hello bieżący stan procesu hello.</span><span class="sxs-lookup"><span data-stu-id="d71a8-157">hello snapshot opens toohello line of code where hello exception was thrown so that you can debug hello current state of hello process.</span></span>

    ![Wyświetl migawkę debugowania w programie Visual Studio](./media/app-insights-snapshot-debugger/open-snapshot-visualstudio.png)

<span data-ttu-id="d71a8-159">migawki pobrany Hello zawiera wszystkie pliki symboli, które zostały odnalezione na serwerze aplikacji sieci web.</span><span class="sxs-lookup"><span data-stu-id="d71a8-159">hello downloaded snapshot contains any symbol files that were found on your web application server.</span></span> <span data-ttu-id="d71a8-160">Te pliki symboli są wymagane tooassociate dane migawki z kodem źródłowym.</span><span class="sxs-lookup"><span data-stu-id="d71a8-160">These symbol files are required tooassociate snapshot data with source code.</span></span> <span data-ttu-id="d71a8-161">Dla aplikacji usługi aplikacji upewnij się, że wdrożenie symbol tooenable podczas publikowania aplikacji sieci web.</span><span class="sxs-lookup"><span data-stu-id="d71a8-161">For App Service apps, make sure tooenable symbol deployment when you publish your web apps.</span></span>

## <a name="how-snapshots-work"></a><span data-ttu-id="d71a8-162">Jak działają migawki</span><span class="sxs-lookup"><span data-stu-id="d71a8-162">How snapshots work</span></span>

<span data-ttu-id="d71a8-163">Podczas uruchamiania aplikacji, tworzony jest proces przesyłania oddzielne migawki, który monitoruje aplikację żądań migawki.</span><span class="sxs-lookup"><span data-stu-id="d71a8-163">When your application starts, a separate snapshot uploader process is created that monitors your application for snapshot requests.</span></span> <span data-ttu-id="d71a8-164">Po zażądaniu migawki kopii w tle hello uruchomiony proces jest przeprowadzane w około 10 minut too20.</span><span class="sxs-lookup"><span data-stu-id="d71a8-164">When a snapshot is requested, a shadow copy of hello running process is made in about 10 too20 minutes.</span></span> <span data-ttu-id="d71a8-165">proces tle Hello następnie są analizowane i migawki jest tworzony podczas hello główny proces jest kontynuowany toorun i obsługiwać ruch toousers.</span><span class="sxs-lookup"><span data-stu-id="d71a8-165">hello shadow process is then analyzed, and a snapshot is created while hello main process continues toorun and serve traffic toousers.</span></span> <span data-ttu-id="d71a8-166">Witaj migawka jest następnie przekazane tooApplication Insights wraz z odpowiednimi symboli (.pdb) pliki, które są potrzebne tooview hello migawki.</span><span class="sxs-lookup"><span data-stu-id="d71a8-166">hello snapshot is then uploaded tooApplication Insights along with any relevant symbol (.pdb) files that are needed tooview hello snapshot.</span></span>

## <a name="current-limitations"></a><span data-ttu-id="d71a8-167">Bieżące ograniczenia</span><span class="sxs-lookup"><span data-stu-id="d71a8-167">Current limitations</span></span>

### <a name="publish-symbols"></a><span data-ttu-id="d71a8-168">Publikuj symbole</span><span class="sxs-lookup"><span data-stu-id="d71a8-168">Publish symbols</span></span>
<span data-ttu-id="d71a8-169">Witaj debugera migawki wymaga plików symboli na zmiennych toodecode serwera produkcyjnego hello i tooprovide działanie debugowania w programie Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="d71a8-169">hello Snapshot Debugger requires symbol files on hello production server toodecode variables and tooprovide a debugging experience in Visual Studio.</span></span> <span data-ttu-id="d71a8-170">Witaj 15,2 wersji programu Visual Studio 2017 publikuje symboli dla kompilacji wydania domyślnie po jej opublikowaniu tooApp usługi.</span><span class="sxs-lookup"><span data-stu-id="d71a8-170">hello 15.2 release of Visual Studio 2017 publishes symbols for release builds by default when it publishes tooApp Service.</span></span> <span data-ttu-id="d71a8-171">W poprzednich wersjach, należy tooadd hello następujące profilu publikowania tooyour wiersza `.pubxml` plików symboli są publikowane w trybie wersji:</span><span class="sxs-lookup"><span data-stu-id="d71a8-171">In prior versions, you need tooadd hello following line tooyour publish profile `.pubxml` file so that symbols are published in release mode:</span></span>

```xml
    <ExcludeGeneratedDebugSymbol>False</ExcludeGeneratedDebugSymbol>
```

<span data-ttu-id="d71a8-172">W przypadku rozwiązań usługi obliczenia Azure i innych typów zapewnić pliki symboli hello hello tego samego folderu .dll głównej aplikacji hello (zazwyczaj `wwwroot/bin`) lub są dostępne w bieżącej ścieżce hello.</span><span class="sxs-lookup"><span data-stu-id="d71a8-172">For Azure Compute and other types, ensure that hello symbol files are in hello same folder of hello main application .dll (typically, `wwwroot/bin`) or are available on hello current path.</span></span>

### <a name="optimized-builds"></a><span data-ttu-id="d71a8-173">Zoptymalizowane kompilacji</span><span class="sxs-lookup"><span data-stu-id="d71a8-173">Optimized builds</span></span>
<span data-ttu-id="d71a8-174">W niektórych przypadkach zmiennych lokalnych nie można wyświetlić w kompilacjach wydania z powodu optymalizacji, które są stosowane podczas procesu kompilacji hello.</span><span class="sxs-lookup"><span data-stu-id="d71a8-174">In some cases, local variables cannot be viewed in release builds because of optimizations that are applied during hello build process.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="d71a8-175">Rozwiązywanie problemów</span><span class="sxs-lookup"><span data-stu-id="d71a8-175">Troubleshooting</span></span>

<span data-ttu-id="d71a8-176">Te wskazówki ułatwiają rozwiązywanie problemów z hello debugera migawki.</span><span class="sxs-lookup"><span data-stu-id="d71a8-176">These tips help you troubleshoot problems with hello Snapshot Debugger.</span></span>

### <a name="verify-hello-instrumentation-key"></a><span data-ttu-id="d71a8-177">Sprawdź hello klucza Instrumentacji</span><span class="sxs-lookup"><span data-stu-id="d71a8-177">Verify hello instrumentation key</span></span>

<span data-ttu-id="d71a8-178">Upewnij się, że używasz klucza Instrumentacji poprawne hello w opublikowanej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="d71a8-178">Make sure that you're using hello correct instrumentation key in your published application.</span></span> <span data-ttu-id="d71a8-179">Zazwyczaj usługi Application Insights odczytuje hello klucza Instrumentacji z hello pliku ApplicationInsights.config.</span><span class="sxs-lookup"><span data-stu-id="d71a8-179">Usually, Application Insights reads hello instrumentation key from hello ApplicationInsights.config file.</span></span> <span data-ttu-id="d71a8-180">Upewnij się, że wartość hello jest sama hello jako klucz Instrumentacji hello hello zasobu usługi Application Insights, które widać w portalu hello.</span><span class="sxs-lookup"><span data-stu-id="d71a8-180">Verify that hello value is hello same as hello instrumentation key for hello Application Insights resource that you see in hello portal.</span></span>

### <a name="check-hello-uploader-logs"></a><span data-ttu-id="d71a8-181">Sprawdź dzienniki przesyłania hello</span><span class="sxs-lookup"><span data-stu-id="d71a8-181">Check hello uploader logs</span></span>

<span data-ttu-id="d71a8-182">Po utworzeniu migawki, plik minizrzutu (dmp) jest tworzony na dysku.</span><span class="sxs-lookup"><span data-stu-id="d71a8-182">After a snapshot is created, a minidump file (.dmp) is created on disk.</span></span> <span data-ttu-id="d71a8-183">Proces przesyłania oddzielne przyjmuje ten plik minizrzutu i przekazuje, oraz wszystkie skojarzone pliki PDB tooApplication magazynu debugera migawki szczegółowych informacji.</span><span class="sxs-lookup"><span data-stu-id="d71a8-183">A separate uploader process takes that minidump file and uploads it, along with any associated PDBs, tooApplication Insights Snapshot Debugger storage.</span></span> <span data-ttu-id="d71a8-184">Po pomyślnym przekazaniu minizrzutu hello są usuwane z dysku.</span><span class="sxs-lookup"><span data-stu-id="d71a8-184">After hello minidump has uploaded successfully, it is deleted from disk.</span></span> <span data-ttu-id="d71a8-185">pliki dziennika Hello przekazujący minizrzutu hello są przechowywane na dysku.</span><span class="sxs-lookup"><span data-stu-id="d71a8-185">hello log files for hello minidump uploader are retained on disk.</span></span> <span data-ttu-id="d71a8-186">W środowisku usługi aplikacji można znaleźć te dzienniki w `D:\Home\LogFiles\Uploader_*.log`.</span><span class="sxs-lookup"><span data-stu-id="d71a8-186">In an App Service environment, you can find these logs in `D:\Home\LogFiles\Uploader_*.log`.</span></span> <span data-ttu-id="d71a8-187">Użyj hello Kudu zarządzania witryny dla usług aplikacji toofind te pliki dziennika.</span><span class="sxs-lookup"><span data-stu-id="d71a8-187">Use hello Kudu management site for App Service toofind these log files.</span></span>

1. <span data-ttu-id="d71a8-188">Otwórz aplikację usługi aplikacji w hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="d71a8-188">Open your App Service application in hello Azure portal.</span></span>

2. <span data-ttu-id="d71a8-189">Wybierz hello **zaawansowane narzędzia** bloku lub Wyszukaj **Kudu**.</span><span class="sxs-lookup"><span data-stu-id="d71a8-189">Select hello **Advanced Tools** blade, or search for **Kudu**.</span></span>
3. <span data-ttu-id="d71a8-190">Kliknij przycisk **Przejdź**.</span><span class="sxs-lookup"><span data-stu-id="d71a8-190">Click **Go**.</span></span>
4. <span data-ttu-id="d71a8-191">W hello **konsoli debugowania** listy rozwijanej wybierz pozycję **CMD**.</span><span class="sxs-lookup"><span data-stu-id="d71a8-191">In hello **Debug console** drop-down list box, select **CMD**.</span></span>
5. <span data-ttu-id="d71a8-192">Kliknij przycisk **LogFiles**.</span><span class="sxs-lookup"><span data-stu-id="d71a8-192">Click **LogFiles**.</span></span>

<span data-ttu-id="d71a8-193">Powinny pojawić się co najmniej jeden plik o nazwie, który rozpoczyna się od `Uploader_` i `.log` rozszerzenia.</span><span class="sxs-lookup"><span data-stu-id="d71a8-193">You should see at least one file with a name that begins with `Uploader_` and a `.log` extension.</span></span> <span data-ttu-id="d71a8-194">Kliknij przycisk toodownload odpowiednią ikonę hello wszystkie pliki dziennika lub je otworzyć w przeglądarce.</span><span class="sxs-lookup"><span data-stu-id="d71a8-194">Click hello appropriate icon toodownload any log files or open them in a browser.</span></span>
<span data-ttu-id="d71a8-195">Nazwa pliku Hello zawiera hello nazwy komputera.</span><span class="sxs-lookup"><span data-stu-id="d71a8-195">hello file name includes hello machine name.</span></span> <span data-ttu-id="d71a8-196">Jeśli wystąpienie usługi aplikacji znajduje się na więcej niż jednej maszynie, istnieją oddzielnych plików dziennika dla każdego komputera.</span><span class="sxs-lookup"><span data-stu-id="d71a8-196">If your App Service instance is hosted on more than one machine, there are separate log files for each machine.</span></span> <span data-ttu-id="d71a8-197">Gdy moduł przesyłający hello wykryje nowy plik minizrzutu, jest rejestrowany w pliku dziennika hello.</span><span class="sxs-lookup"><span data-stu-id="d71a8-197">When hello uploader detects a new minidump file, it is recorded in hello log file.</span></span> <span data-ttu-id="d71a8-198">Oto przykład pomyślne ukończenie przekazywania:</span><span class="sxs-lookup"><span data-stu-id="d71a8-198">Here's an example of a successful upload:</span></span>

```
MinidumpUploader.exe Information: 0 : Dump available 139e411a23934dc0b9ea08a626db16c5.dmp
    DateTime=2017-05-25T14:25:08.0349846Z
MinidumpUploader.exe Information: 0 : Uploading D:\local\Temp\Dumps\c12a605e73c44346a984e00000000000\139e411a23934dc0b9ea08a626db16c5.dmp, 329.12 MB
    DateTime=2017-05-25T14:25:16.0145444Z
MinidumpUploader.exe Information: 0 : Upload successful.
    DateTime=2017-05-25T14:25:42.9164120Z
MinidumpUploader.exe Information: 0 : Extracting PDB info from D:\local\Temp\Dumps\c12a605e73c44346a984e00000000000\139e411a23934dc0b9ea08a626db16c5.dmp.
    DateTime=2017-05-25T14:25:42.9164120Z
MinidumpUploader.exe Information: 0 : Matched 2 PDB(s) with local files.
    DateTime=2017-05-25T14:25:44.2310982Z
MinidumpUploader.exe Information: 0 : Stamp does not want any of our matched PDBs.
    DateTime=2017-05-25T14:25:44.5435948Z
MinidumpUploader.exe Information: 0 : Deleted D:\local\Temp\Dumps\c12a605e73c44346a984e00000000000\139e411a23934dc0b9ea08a626db16c5.dmp
    DateTime=2017-05-25T14:25:44.6095821Z
```

<span data-ttu-id="d71a8-199">W poprzednim przykładzie hello jest klucza Instrumentacji hello `c12a605e73c44346a984e00000000000`.</span><span class="sxs-lookup"><span data-stu-id="d71a8-199">In hello previous example, hello instrumentation key is `c12a605e73c44346a984e00000000000`.</span></span> <span data-ttu-id="d71a8-200">Ta wartość powinna być zgodna hello klucza instrumentacji aplikacji.</span><span class="sxs-lookup"><span data-stu-id="d71a8-200">This value should match hello instrumentation key for your application.</span></span>
<span data-ttu-id="d71a8-201">Witaj minizrzutu jest skojarzony z migawki o identyfikatorze hello `139e411a23934dc0b9ea08a626db16c5`.</span><span class="sxs-lookup"><span data-stu-id="d71a8-201">hello minidump is associated with a snapshot with hello ID `139e411a23934dc0b9ea08a626db16c5`.</span></span> <span data-ttu-id="d71a8-202">Można użyć tego Identyfikatora nowsze hello toolocate skojarzone dane telemetryczne dotyczące wyjątków w aplikacji Analytics szczegółowych informacji.</span><span class="sxs-lookup"><span data-stu-id="d71a8-202">You can use this ID later toolocate hello associated exception telemetry in Application Insights Analytics.</span></span>

<span data-ttu-id="d71a8-203">Moduł przesyłający Hello skanowania pod kątem nowych baz danych PDB o co 15 minut.</span><span class="sxs-lookup"><span data-stu-id="d71a8-203">hello uploader scans for new PDBs about once every 15 minutes.</span></span> <span data-ttu-id="d71a8-204">Oto przykład:</span><span class="sxs-lookup"><span data-stu-id="d71a8-204">Here's an example:</span></span>

```
MinidumpUploader.exe Information: 0 : PDB rescan requested.
    DateTime=2017-05-25T15:11:38.8003886Z
MinidumpUploader.exe Information: 0 : Scanning D:\home\site\wwwroot\ for local PDBs.
    DateTime=2017-05-25T15:11:38.8003886Z
MinidumpUploader.exe Information: 0 : Scanning D:\local\Temporary ASP.NET Files\root\a6554c94\e3ad6f22\assembly\dl3\81d5008b\00b93cc8_dec5d201 for local PDBs.
    DateTime=2017-05-25T15:11:38.8160276Z
MinidumpUploader.exe Information: 0 : Local PDB scan complete. Found 2 PDB(s).
    DateTime=2017-05-25T15:11:38.8316450Z
MinidumpUploader.exe Information: 0 : Deleted PDB scan marker D:\local\Temp\Dumps\c12a605e73c44346a984e00000000000\.pdbscan.
    DateTime=2017-05-25T15:11:38.8316450Z
```

<span data-ttu-id="d71a8-205">Dla aplikacji, które są _nie_ hostowanych w usłudze App Service, są dzienniki przesyłania hello hello tym samym folderze co minizrzutów hello: `%TEMP%\Dumps\<ikey>` (gdzie `<ikey>` jest klucz Instrumentacji).</span><span class="sxs-lookup"><span data-stu-id="d71a8-205">For applications that are _not_ hosted in App Service, hello uploader logs are in hello same folder as hello minidumps: `%TEMP%\Dumps\<ikey>` (where `<ikey>` is your instrumentation key).</span></span>

### <a name="use-application-insights-search-toofind-exceptions-with-snapshots"></a><span data-ttu-id="d71a8-206">Użyj Application Insights wyszukiwania toofind wyjątki z migawkami</span><span class="sxs-lookup"><span data-stu-id="d71a8-206">Use Application Insights search toofind exceptions with snapshots</span></span>

<span data-ttu-id="d71a8-207">Po utworzeniu migawki hello Zgłaszanie wyjątku jest oznaczone przy użyciu identyfikatora migawki.</span><span class="sxs-lookup"><span data-stu-id="d71a8-207">When a snapshot is created, hello throwing exception is tagged with a snapshot ID.</span></span> <span data-ttu-id="d71a8-208">Telemetria wyjątków powitania po Insights tooApplication zgłoszone ten identyfikator migawki jest uwzględniona jako właściwości niestandardowej.</span><span class="sxs-lookup"><span data-stu-id="d71a8-208">When hello exception telemetry is reported tooApplication Insights, that snapshot ID is included as a custom property.</span></span> <span data-ttu-id="d71a8-209">Za pomocą bloku wyszukiwania hello w usłudze Application Insights, można znaleźć wszystkie dane telemetryczne z hello `ai.snapshot.id` właściwości niestandardowej.</span><span class="sxs-lookup"><span data-stu-id="d71a8-209">Using hello Search blade in Application Insights, you can find all telemetry with hello `ai.snapshot.id` custom property.</span></span>

1. <span data-ttu-id="d71a8-210">Przeglądaj tooyour zasobu usługi Application Insights w hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="d71a8-210">Browse tooyour Application Insights resource in hello Azure portal.</span></span>
2. <span data-ttu-id="d71a8-211">Kliknij przycisk **wyszukiwania**.</span><span class="sxs-lookup"><span data-stu-id="d71a8-211">Click **Search**.</span></span>
3. <span data-ttu-id="d71a8-212">Typ `ai.snapshot.id` w polu tekstowym wyszukiwania hello i naciśnij klawisz Enter.</span><span class="sxs-lookup"><span data-stu-id="d71a8-212">Type `ai.snapshot.id` in hello Search text box and press Enter.</span></span>

![Wyszukaj dane telemetryczne z Identyfikatorem migawki w portalu hello](./media/app-insights-snapshot-debugger/search-snapshot-portal.png)

<span data-ttu-id="d71a8-214">Jeśli to wyszukiwanie nie zwróciło żadnych wyników, migawek nie zostały zgłoszone tooApplication Insights dla aplikacji hello wybrany zakres czasu.</span><span class="sxs-lookup"><span data-stu-id="d71a8-214">If this search returns no results, then no snapshots were reported tooApplication Insights for your application in hello selected time range.</span></span>

<span data-ttu-id="d71a8-215">w polu wyszukiwania hello toosearch identyfikator określoną migawkę z dzienników przesyłania hello, wpisz ten identyfikator.</span><span class="sxs-lookup"><span data-stu-id="d71a8-215">toosearch for a specific snapshot ID from hello Uploader logs, type that ID in hello Search box.</span></span> <span data-ttu-id="d71a8-216">Jeśli nie możesz znaleźć dane telemetryczne dla migawki, który został przekazany, wykonaj następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="d71a8-216">If you can't find telemetry for a snapshot that you know was uploaded, follow these steps:</span></span>

1. <span data-ttu-id="d71a8-217">Sprawdź, czy przeglądania hello prawo zasobu usługi Application Insights, upewniając hello klucza instrumentacji.</span><span class="sxs-lookup"><span data-stu-id="d71a8-217">Double-check that you're looking at hello right Application Insights resource by verifying hello instrumentation key.</span></span>

2. <span data-ttu-id="d71a8-218">Przy użyciu sygnatury czasowej hello z dziennika przekazujący hello, Dostosuj filtru zakresu czasu hello toocover wyszukiwania hello zakresu czasu.</span><span class="sxs-lookup"><span data-stu-id="d71a8-218">Using hello timestamp from hello Uploader log, adjust hello Time Range filter of hello search toocover that time range.</span></span>

<span data-ttu-id="d71a8-219">Jeśli nadal nie widać Wystąpił wyjątek o takim identyfikatorze migawki, hello dane telemetryczne dotyczące wyjątków nie został zgłoszony tooApplication szczegółowych informacji.</span><span class="sxs-lookup"><span data-stu-id="d71a8-219">If you still don't see an exception with that snapshot ID, then hello exception telemetry wasn't reported tooApplication Insights.</span></span> <span data-ttu-id="d71a8-220">Taka sytuacja może się zdarzyć, jeśli awaria aplikacji po zajęło hello migawki, ale przed zgłosiła ona hello dane telemetryczne dotyczące wyjątków.</span><span class="sxs-lookup"><span data-stu-id="d71a8-220">This situation can happen if your application crashed after it took hello snapshot but before it reported hello exception telemetry.</span></span> <span data-ttu-id="d71a8-221">W takim przypadku sprawdź hello dzienniki usługi aplikacji w obszarze `Diagnose and solve problems` toosee Jeśli wystąpiły nieoczekiwane ponowne uruchomienie lub nieobsługiwane wyjątki.</span><span class="sxs-lookup"><span data-stu-id="d71a8-221">In this case, check hello App Service logs under `Diagnose and solve problems` toosee if there were unexpected restarts or unhandled exceptions.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d71a8-222">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="d71a8-222">Next steps</span></span>

* <span data-ttu-id="d71a8-223">[Ustaw snappoints w kodzie](https://azure.microsoft.com/blog/snapshot-debugger-for-azure/) migawki tooget bez oczekiwania na wyjątek.</span><span class="sxs-lookup"><span data-stu-id="d71a8-223">[Set snappoints in your code](https://azure.microsoft.com/blog/snapshot-debugger-for-azure/) tooget snapshots without waiting for an exception.</span></span>
* <span data-ttu-id="d71a8-224">[Diagnozowanie wyjątków w aplikacjach sieci web](app-insights-asp-net-exceptions.md) wyjaśniono, jak toomake więcej widocznych wyjątki tooApplication szczegółowych informacji.</span><span class="sxs-lookup"><span data-stu-id="d71a8-224">[Diagnose exceptions in your web apps](app-insights-asp-net-exceptions.md) explains how toomake more exceptions visible tooApplication Insights.</span></span> 
* <span data-ttu-id="d71a8-225">[Inteligentne wykrywania](app-insights-proactive-diagnostics.md) automatycznie odnajduje anomalii wydajności.</span><span class="sxs-lookup"><span data-stu-id="d71a8-225">[Smart Detection](app-insights-proactive-diagnostics.md) automatically discovers performance anomalies.</span></span>
