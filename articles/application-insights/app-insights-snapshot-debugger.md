---
title: "Usługa Azure Application Insights migawki debuger dla aplikacji .NET | Dokumentacja firmy Microsoft"
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
ms.openlocfilehash: 56eba2ff7af228b3c44354ad43b384288b4e1972
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/18/2017
---
# <a name="debug-snapshots-on-exceptions-in-net-apps"></a><span data-ttu-id="bc04d-103">Debugowanie migawek na wyjątków w aplikacji .NET</span><span class="sxs-lookup"><span data-stu-id="bc04d-103">Debug snapshots on exceptions in .NET apps</span></span>

<span data-ttu-id="bc04d-104">Po wystąpieniu wyjątku, można automatycznie zbierać migawki debugowania aplikacji sieci web na żywo.</span><span class="sxs-lookup"><span data-stu-id="bc04d-104">When an exception occurs, you can automatically collect a debug snapshot from your live web application.</span></span> <span data-ttu-id="bc04d-105">Migawki przedstawia stan kodu źródłowego i zmiennych w momencie utworzenia zgłoszono wyjątek.</span><span class="sxs-lookup"><span data-stu-id="bc04d-105">The snapshot shows the state of source code and variables at the moment the exception was thrown.</span></span> <span data-ttu-id="bc04d-106">Debuger migawki (wersja zapoznawcza) w [Azure Application Insights](app-insights-overview.md) monitoruje dane telemetryczne wyjątku z aplikacji sieci web.</span><span class="sxs-lookup"><span data-stu-id="bc04d-106">The Snapshot Debugger (preview) in [Azure Application Insights](app-insights-overview.md) monitors exception telemetry from your web app.</span></span> <span data-ttu-id="bc04d-107">Zbiera migawki na listy wyjątków zgłaszanie top, dzięki czemu masz informacje potrzebne do diagnozowania problemów w środowisku produkcyjnym.</span><span class="sxs-lookup"><span data-stu-id="bc04d-107">It collects snapshots on your top-throwing exceptions so that you have the information you need to diagnose issues in production.</span></span> <span data-ttu-id="bc04d-108">Obejmują [pakietu NuGet modułu zbierającego migawki](http://www.nuget.org/packages/Microsoft.ApplicationInsights.SnapshotCollector) w aplikacji i opcjonalnie skonfigurować parametry kolekcji w [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md). Migawki są wyświetlane na [wyjątki](app-insights-asp-net-exceptions.md) w portalu usługi Application Insights.</span><span class="sxs-lookup"><span data-stu-id="bc04d-108">Include the [Snapshot collector NuGet package](http://www.nuget.org/packages/Microsoft.ApplicationInsights.SnapshotCollector) in your application, and optionally configure collection parameters in [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md). Snapshots appear on [exceptions](app-insights-asp-net-exceptions.md) in the Application Insights portal.</span></span>

<span data-ttu-id="bc04d-109">Migawki debugowania można wyświetlić w portalu w celu sprawdzenia wywołania stosu i sprawdzić zmiennych w każdej ramki stosu wywołań.</span><span class="sxs-lookup"><span data-stu-id="bc04d-109">You can view debug snapshots in the portal to see the call stack and inspect variables at each call stack frame.</span></span> <span data-ttu-id="bc04d-110">Aby uzyskać bardziej wydajne działanie debugowania z kodem źródłowym, otwórz migawki z programu Visual Studio Enterprise 2017 przez [pobieranie rozszerzenia migawki debugera programu Visual Studio](https://aka.ms/snapshotdebugger).</span><span class="sxs-lookup"><span data-stu-id="bc04d-110">To get a more powerful debugging experience with source code, open snapshots with Visual Studio 2017 Enterprise by [downloading the Snapshot Debugger extension for Visual Studio](https://aka.ms/snapshotdebugger).</span></span>

<span data-ttu-id="bc04d-111">Kolekcja migawki jest dostępny dla:</span><span class="sxs-lookup"><span data-stu-id="bc04d-111">Snapshot collection is available for:</span></span>
* <span data-ttu-id="bc04d-112">Aplikacje środowiska .NET framework i program ASP.NET systemem .NET Framework 4.5 lub nowszej.</span><span class="sxs-lookup"><span data-stu-id="bc04d-112">.NET Framework and ASP.NET applications running .NET Framework 4.5 or later.</span></span>
* <span data-ttu-id="bc04d-113">.NET core 2.0 i ASP.NET Core 2.0 aplikacji uruchomionych w systemie Windows.</span><span class="sxs-lookup"><span data-stu-id="bc04d-113">.NET Core 2.0 and ASP.NET Core 2.0 applications running on Windows.</span></span>

### <a name="configure-snapshot-collection-for-aspnet-applications"></a><span data-ttu-id="bc04d-114">Konfigurowanie zbierania migawek dla aplikacji ASP.NET</span><span class="sxs-lookup"><span data-stu-id="bc04d-114">Configure snapshot collection for ASP.NET applications</span></span>

1. <span data-ttu-id="bc04d-115">[Włącz usługę Application Insights w aplikacji sieci web](app-insights-asp-net.md), jeśli nie jeszcze go jeszcze gotowe.</span><span class="sxs-lookup"><span data-stu-id="bc04d-115">[Enable Application Insights in your web app](app-insights-asp-net.md), if you haven't done it yet.</span></span>

2. <span data-ttu-id="bc04d-116">Obejmują [Microsoft.ApplicationInsights.SnapshotCollector](http://www.nuget.org/packages/Microsoft.ApplicationInsights.SnapshotCollector) pakietu NuGet w aplikacji.</span><span class="sxs-lookup"><span data-stu-id="bc04d-116">Include the [Microsoft.ApplicationInsights.SnapshotCollector](http://www.nuget.org/packages/Microsoft.ApplicationInsights.SnapshotCollector) NuGet package in your app.</span></span> 

3. <span data-ttu-id="bc04d-117">Przejrzyj domyślne opcje dodane do pakietu [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md):</span><span class="sxs-lookup"><span data-stu-id="bc04d-117">Review the default options that the package added to [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md):</span></span>

    ```xml
    <TelemetryProcessors>
        <Add Type="Microsoft.ApplicationInsights.SnapshotCollector.SnapshotCollectorTelemetryProcessor, Microsoft.ApplicationInsights.SnapshotCollector">
        <!-- The default is true, but you can disable Snapshot Debugging by setting it to false -->
        <IsEnabled>true</IsEnabled>
        <!-- Snapshot Debugging is usually disabled in developer mode, but you can enable it by setting this to true. -->
        <!-- DeveloperMode is a property on the active TelemetryChannel. -->
        <IsEnabledInDeveloperMode>false</IsEnabledInDeveloperMode>
        <!-- How many times we need to see an exception before we ask for snapshots. -->
        <ThresholdForSnapshotting>5</ThresholdForSnapshotting>
        <!-- The maximum number of examples we create for a single problem. -->
        <MaximumSnapshotsRequired>3</MaximumSnapshotsRequired>
        <!-- The maximum number of problems that we can be tracking at any time. -->
        <MaximumCollectionPlanSize>50</MaximumCollectionPlanSize>
        <!-- How often to reset problem counters. -->
        <ProblemCounterResetInterval>06:00:00</ProblemCounterResetInterval>
        <!-- The maximum number of snapshots allowed in one minute. -->
        <SnapshotsPerMinuteLimit>2</SnapshotsPerMinuteLimit>
        <!-- The maximum number of snapshots allowed per day. -->
        <SnapshotsPerDayLimit>50</SnapshotsPerDayLimit>
        </Add>
    </TelemetryProcessors>
    ```

4. <span data-ttu-id="bc04d-118">Migawki są zbierane tylko na wyjątki, które są zgłaszane do usługi Application Insights.</span><span class="sxs-lookup"><span data-stu-id="bc04d-118">Snapshots are collected only on exceptions that are reported to Application Insights.</span></span> <span data-ttu-id="bc04d-119">W niektórych przypadkach (na przykład starszych wersji platformy .NET), konieczne może być [Konfigurowanie zbierania wyjątków](app-insights-asp-net-exceptions.md#exceptions) aby zobaczyć wyjątki z migawkami w portalu.</span><span class="sxs-lookup"><span data-stu-id="bc04d-119">In some cases (for example, older versions of the .NET platform), you might need to [configure exception collection](app-insights-asp-net-exceptions.md#exceptions) to see exceptions with snapshots in the portal.</span></span>


### <a name="configure-snapshot-collection-for-aspnet-core-20-applications"></a><span data-ttu-id="bc04d-120">Konfigurowanie zbierania migawek dla aplikacji platformy ASP.NET Core 2.0</span><span class="sxs-lookup"><span data-stu-id="bc04d-120">Configure snapshot collection for ASP.NET Core 2.0 applications</span></span>

1. <span data-ttu-id="bc04d-121">[Włącz usługę Application Insights w aplikacji sieci web platformy ASP.NET Core](app-insights-asp-net-core.md), jeśli nie jeszcze go jeszcze gotowe.</span><span class="sxs-lookup"><span data-stu-id="bc04d-121">[Enable Application Insights in your ASP.NET Core web app](app-insights-asp-net-core.md), if you haven't done it yet.</span></span>

2. <span data-ttu-id="bc04d-122">Obejmują [Microsoft.ApplicationInsights.SnapshotCollector](http://www.nuget.org/packages/Microsoft.ApplicationInsights.SnapshotCollector) pakietu NuGet w aplikacji.</span><span class="sxs-lookup"><span data-stu-id="bc04d-122">Include the [Microsoft.ApplicationInsights.SnapshotCollector](http://www.nuget.org/packages/Microsoft.ApplicationInsights.SnapshotCollector) NuGet package in your app.</span></span>

3. <span data-ttu-id="bc04d-123">Modyfikowanie `ConfigureServices` metody w aplikacji `Startup` klasa do dodania migawki modułu zbierającego dane telemetryczne procesora.</span><span class="sxs-lookup"><span data-stu-id="bc04d-123">Modify the `ConfigureServices` method in your application's `Startup` class to add the Snapshot Collector's telemetry processor.</span></span> <span data-ttu-id="bc04d-124">Kod, który należy dodać zależy od przywoływanego wersji pakietu Microsoft.ApplicationInsights.ASPNETCore NuGet.</span><span class="sxs-lookup"><span data-stu-id="bc04d-124">The code you should add depends on the referenced version of the Microsoft.ApplicationInsights.ASPNETCore NuGet package.</span></span>

   <span data-ttu-id="bc04d-125">W przypadku Microsoft.ApplicationInsights.AspNetCore 2.1.0 należy dodać:</span><span class="sxs-lookup"><span data-stu-id="bc04d-125">For Microsoft.ApplicationInsights.AspNetCore 2.1.0 add:</span></span>
   ```C#
   using Microsoft.ApplicationInsights.SnapshotCollector;
   ...
   class Startup
   {
       // This method is called by the runtime. Use it to add services to the container.
       public void ConfigureServices(IServiceCollection services)
       {
           services.AddSingleton<Func<ITelemetryProcessor, ITelemetryProcessor>>(next => new SnapshotCollectorTelemetryProcessor(next));
           // TODO: Add any other services your application needs here.
       }
   }
   ```

   <span data-ttu-id="bc04d-126">W przypadku Microsoft.ApplicationInsights.AspNetCore 2.1.1 należy dodać:</span><span class="sxs-lookup"><span data-stu-id="bc04d-126">For Microsoft.ApplicationInsights.AspNetCore 2.1.1 add:</span></span>
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

       // This method is called by the runtime. Use it to add services to the container.
       public void ConfigureServices(IServiceCollection services)
       {
            services.AddSingleton<ITelemetryProcessorFactory>(new SnapshotCollectorTelemetryProcessorFactory());
           // TODO: Add any other services your application needs here.
       }
   }
   ```

### <a name="configure-snapshot-collection-for-other-net-applications"></a><span data-ttu-id="bc04d-127">Konfigurowanie zbierania migawek dla innych aplikacji .NET</span><span class="sxs-lookup"><span data-stu-id="bc04d-127">Configure snapshot collection for other .NET applications</span></span>

1. <span data-ttu-id="bc04d-128">Jeśli aplikacja nie jest już instrumentowane przy użyciu usługi Application Insights, rozpoczęcie pracy przez [Włączanie usługi Application Insights i ustawienie klucza Instrumentacji](app-insights-windows-desktop.md).</span><span class="sxs-lookup"><span data-stu-id="bc04d-128">If your application is not already instrumented with Application Insights, get started by [enabling Application Insights and setting the instrumentation key](app-insights-windows-desktop.md).</span></span>

2. <span data-ttu-id="bc04d-129">Dodaj [Microsoft.ApplicationInsights.SnapshotCollector](http://www.nuget.org/packages/Microsoft.ApplicationInsights.SnapshotCollector) pakietu NuGet w aplikacji.</span><span class="sxs-lookup"><span data-stu-id="bc04d-129">Add the [Microsoft.ApplicationInsights.SnapshotCollector](http://www.nuget.org/packages/Microsoft.ApplicationInsights.SnapshotCollector) NuGet package in your app.</span></span>

3. <span data-ttu-id="bc04d-130">Migawki są zbierane tylko na wyjątki, które są zgłaszane do usługi Application Insights.</span><span class="sxs-lookup"><span data-stu-id="bc04d-130">Snapshots are collected only on exceptions that are reported to Application Insights.</span></span> <span data-ttu-id="bc04d-131">Konieczne może być swój kod, aby zgłosić je modyfikować.</span><span class="sxs-lookup"><span data-stu-id="bc04d-131">You may need to modify your code to report them.</span></span> <span data-ttu-id="bc04d-132">Kod obsługi wyjątków jest zależna od struktury aplikacji, ale przykładem jest poniżej:</span><span class="sxs-lookup"><span data-stu-id="bc04d-132">The exception handling code depends on the structure of your application, but an example is below:</span></span>
    ```C#
   TelemetryClient _telemetryClient = new TelemetryClient();

   void ExampleRequest()
   {
        try
        {
            // TODO: Handle the request.
        }
        catch (Exception ex)
        {
            // Report the exception to Application Insights.
            _telemetryClient.TrackException(ex);

            // TODO: Rethrow the exception if desired.
        }
   }
    ```
    
## <a name="grant-permissions"></a><span data-ttu-id="bc04d-133">Udzielanie uprawnień</span><span class="sxs-lookup"><span data-stu-id="bc04d-133">Grant permissions</span></span>

<span data-ttu-id="bc04d-134">Właściciele subskrypcji platformy Azure można sprawdzić migawki.</span><span class="sxs-lookup"><span data-stu-id="bc04d-134">Owners of the Azure subscription can inspect snapshots.</span></span> <span data-ttu-id="bc04d-135">Inni użytkownicy muszą mieć uprawnienie przez właściciela.</span><span class="sxs-lookup"><span data-stu-id="bc04d-135">Other users must be granted permission by an owner.</span></span>

<span data-ttu-id="bc04d-136">Aby przyznać uprawnienia, Przypisz `Application Insights Snapshot Debugger` roli do użytkowników, którzy będzie przeprowadzał inspekcję migawki.</span><span class="sxs-lookup"><span data-stu-id="bc04d-136">To grant permission, assign the `Application Insights Snapshot Debugger` role to users who will inspect snapshots.</span></span> <span data-ttu-id="bc04d-137">Tę rolę można przypisać do poszczególnych użytkowników lub grup właściciele subskrypcji dla zasobu usługi Application Insights docelowej lub grupy zasobów lub subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="bc04d-137">This role can be assigned to individual users or groups by subscription owners for the target Application Insights resource or its resource group or subscription.</span></span>

1. <span data-ttu-id="bc04d-138">Otwiera blok kontroli dostępu (IAM).</span><span class="sxs-lookup"><span data-stu-id="bc04d-138">Open the Access Control (IAM) blade.</span></span>
1. <span data-ttu-id="bc04d-139">Kliknij przycisk Dodaj +.</span><span class="sxs-lookup"><span data-stu-id="bc04d-139">Click the +Add button.</span></span>
1. <span data-ttu-id="bc04d-140">Wybierz debuger migawki Insights aplikacji z listy rozwijanej ról.</span><span class="sxs-lookup"><span data-stu-id="bc04d-140">Select Application Insights Snapshot Debugger from the Roles drop-down list.</span></span>
1. <span data-ttu-id="bc04d-141">Wyszukaj, a następnie wprowadź nazwę użytkownika do dodania.</span><span class="sxs-lookup"><span data-stu-id="bc04d-141">Search for and enter a name for the user to add.</span></span>
1. <span data-ttu-id="bc04d-142">Kliknij przycisk Zapisz, aby dodać użytkownika do roli.</span><span class="sxs-lookup"><span data-stu-id="bc04d-142">Click the Save button to add the user to the role.</span></span>


[!IMPORTANT]
    <span data-ttu-id="bc04d-143">Migawki potencjalnie może zawierać informacje osobiste i innych poufnych w zmiennej i wartości parametrów.</span><span class="sxs-lookup"><span data-stu-id="bc04d-143">Snapshots can potentially contain personal and other sensitive information in variable and parameter values.</span></span>

## <a name="debug-snapshots-in-the-application-insights-portal"></a><span data-ttu-id="bc04d-144">Debugowanie migawek w portalu usługi Application Insights</span><span class="sxs-lookup"><span data-stu-id="bc04d-144">Debug snapshots in the Application Insights portal</span></span>

<span data-ttu-id="bc04d-145">Jeśli migawka jest dostępna dla danego wyjątku lub identyfikator problemu **Otwórz migawki debugowania** na pojawi się przycisk [wyjątek](app-insights-asp-net-exceptions.md) w portalu usługi Application Insights.</span><span class="sxs-lookup"><span data-stu-id="bc04d-145">If a snapshot is available for a given exception or a problem ID, an **Open Debug Snapshot** button appears on the [exception](app-insights-asp-net-exceptions.md) in the Application Insights portal.</span></span>

![Przycisk Otwórz migawki debugowania na wyjątek](./media/app-insights-snapshot-debugger/snapshot-on-exception.png)

<span data-ttu-id="bc04d-147">W widoku debugowania migawek Zobacz stosu wywołań i okienku zmiennych.</span><span class="sxs-lookup"><span data-stu-id="bc04d-147">In the Debug Snapshot view, you see a call stack and a variables pane.</span></span> <span data-ttu-id="bc04d-148">Po wybraniu ramki stosu wywołań w okienku Stos wywołań, można wyświetlić zmiennych lokalnych i wywołać parametrów dla tej funkcji w okienku zmiennych.</span><span class="sxs-lookup"><span data-stu-id="bc04d-148">When you select frames of the call stack in the call stack pane, you can view local variables and parameters for that function call in the variables pane.</span></span>

![Widok debugowania migawki w portalu](./media/app-insights-snapshot-debugger/open-snapshot-portal.png)

<span data-ttu-id="bc04d-150">Migawki mogą zawierać poufne informacje, i domyślnie nie są widoczne.</span><span class="sxs-lookup"><span data-stu-id="bc04d-150">Snapshots might contain sensitive information, and by default they are not viewable.</span></span> <span data-ttu-id="bc04d-151">Aby wyświetlić migawki, musisz mieć `Application Insights Snapshot Debugger` rola przypisana użytkownikowi.</span><span class="sxs-lookup"><span data-stu-id="bc04d-151">To view snapshots, you must have the `Application Insights Snapshot Debugger` role assigned to you.</span></span>

## <a name="debug-snapshots-with-visual-studio-2017-enterprise"></a><span data-ttu-id="bc04d-152">Migawki z programu Visual Studio Enterprise 2017 debugowania</span><span class="sxs-lookup"><span data-stu-id="bc04d-152">Debug snapshots with Visual Studio 2017 Enterprise</span></span>
1. <span data-ttu-id="bc04d-153">Kliknij przycisk **pobrać migawki** przycisk, aby pobrać `.diagsession` pliku, który można otworzyć w programie Visual Studio Enterprise 2017 r.</span><span class="sxs-lookup"><span data-stu-id="bc04d-153">Click the **Download Snapshot** button to download a `.diagsession` file, which can be opened by Visual Studio 2017 Enterprise.</span></span> 

2. <span data-ttu-id="bc04d-154">Aby otworzyć `.diagsession` pliku, należy najpierw [Pobierz i zainstaluj rozszerzenie migawki debugera programu Visual Studio](https://aka.ms/snapshotdebugger).</span><span class="sxs-lookup"><span data-stu-id="bc04d-154">To open the `.diagsession` file, you must first [download and install the Snapshot Debugger extension for Visual Studio](https://aka.ms/snapshotdebugger).</span></span>

3. <span data-ttu-id="bc04d-155">Po otwarciu pliku migawki, zostanie wyświetlona strona debugowania minizrzutu w programie Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="bc04d-155">After you open the snapshot file, the Minidump Debugging page in Visual Studio appears.</span></span> <span data-ttu-id="bc04d-156">Kliknij przycisk **debugowania kodu zarządzanego** można rozpocząć debugowania migawki.</span><span class="sxs-lookup"><span data-stu-id="bc04d-156">Click **Debug Managed Code** to start debugging the snapshot.</span></span> <span data-ttu-id="bc04d-157">Migawka zostanie otwarty wiersz kodu, w której wystąpił wyjątek, aby umożliwić debugowanie bieżący stan procesu.</span><span class="sxs-lookup"><span data-stu-id="bc04d-157">The snapshot opens to the line of code where the exception was thrown so that you can debug the current state of the process.</span></span>

    ![Wyświetl migawkę debugowania w programie Visual Studio](./media/app-insights-snapshot-debugger/open-snapshot-visualstudio.png)

<span data-ttu-id="bc04d-159">Pobrany migawki zawiera wszystkie pliki symboli, które zostały odnalezione na serwerze aplikacji sieci web.</span><span class="sxs-lookup"><span data-stu-id="bc04d-159">The downloaded snapshot contains any symbol files that were found on your web application server.</span></span> <span data-ttu-id="bc04d-160">Te pliki symboli są wymagane, aby skojarzyć dane migawki z kodu źródłowego.</span><span class="sxs-lookup"><span data-stu-id="bc04d-160">These symbol files are required to associate snapshot data with source code.</span></span> <span data-ttu-id="bc04d-161">Dla aplikacji usługi aplikacji upewnij się, że włączyć symbol wdrożenia po opublikowaniu aplikacji sieci web.</span><span class="sxs-lookup"><span data-stu-id="bc04d-161">For App Service apps, make sure to enable symbol deployment when you publish your web apps.</span></span>

## <a name="how-snapshots-work"></a><span data-ttu-id="bc04d-162">Jak działają migawki</span><span class="sxs-lookup"><span data-stu-id="bc04d-162">How snapshots work</span></span>

<span data-ttu-id="bc04d-163">Podczas uruchamiania aplikacji, tworzony jest proces przesyłania oddzielne migawki, który monitoruje aplikację żądań migawki.</span><span class="sxs-lookup"><span data-stu-id="bc04d-163">When your application starts, a separate snapshot uploader process is created that monitors your application for snapshot requests.</span></span> <span data-ttu-id="bc04d-164">Po zażądaniu migawki kopii w tle uruchomiony proces jest przeprowadzane w około 10 do 20 minut.</span><span class="sxs-lookup"><span data-stu-id="bc04d-164">When a snapshot is requested, a shadow copy of the running process is made in about 10 to 20 minutes.</span></span> <span data-ttu-id="bc04d-165">Następnie są analizowane przez proces w tle, a migawka jest tworzona podczas procesu głównego kontynuuje działanie i obsługiwać ruch do użytkowników.</span><span class="sxs-lookup"><span data-stu-id="bc04d-165">The shadow process is then analyzed, and a snapshot is created while the main process continues to run and serve traffic to users.</span></span> <span data-ttu-id="bc04d-166">Migawki są następnie przekazywane do usługi Application Insights oraz pliki odpowiednich symboli (.pdb), które są potrzebne, aby wyświetlić migawki.</span><span class="sxs-lookup"><span data-stu-id="bc04d-166">The snapshot is then uploaded to Application Insights along with any relevant symbol (.pdb) files that are needed to view the snapshot.</span></span>

## <a name="current-limitations"></a><span data-ttu-id="bc04d-167">Bieżące ograniczenia</span><span class="sxs-lookup"><span data-stu-id="bc04d-167">Current limitations</span></span>

### <a name="publish-symbols"></a><span data-ttu-id="bc04d-168">Publikuj symbole</span><span class="sxs-lookup"><span data-stu-id="bc04d-168">Publish symbols</span></span>
<span data-ttu-id="bc04d-169">Debuger migawki wymaga plików symboli na serwerze produkcyjnym w celu zdekodowania zmienne i zapewnia środowisko debugowania w programie Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="bc04d-169">The Snapshot Debugger requires symbol files on the production server to decode variables and to provide a debugging experience in Visual Studio.</span></span> <span data-ttu-id="bc04d-170">15.2 wydanie programu Visual Studio 2017 publikuje symboli dla kompilacji wydania domyślnie po opublikowaniu go do usługi App Service.</span><span class="sxs-lookup"><span data-stu-id="bc04d-170">The 15.2 release of Visual Studio 2017 publishes symbols for release builds by default when it publishes to App Service.</span></span> <span data-ttu-id="bc04d-171">W poprzednich wersjach, należy dodać następujący wiersz do swój profil publikowania `.pubxml` plików symboli są publikowane w trybie wersji:</span><span class="sxs-lookup"><span data-stu-id="bc04d-171">In prior versions, you need to add the following line to your publish profile `.pubxml` file so that symbols are published in release mode:</span></span>

```xml
    <ExcludeGeneratedDebugSymbol>False</ExcludeGeneratedDebugSymbol>
```

<span data-ttu-id="bc04d-172">Dla rozwiązań usługi obliczenia Azure i innych typów, upewnij się, że pliki symboli są w tym samym folderze DLL aplikacji głównej (zazwyczaj `wwwroot/bin`) lub są dostępne w bieżącej ścieżce.</span><span class="sxs-lookup"><span data-stu-id="bc04d-172">For Azure Compute and other types, ensure that the symbol files are in the same folder of the main application .dll (typically, `wwwroot/bin`) or are available on the current path.</span></span>

### <a name="optimized-builds"></a><span data-ttu-id="bc04d-173">Zoptymalizowane kompilacji</span><span class="sxs-lookup"><span data-stu-id="bc04d-173">Optimized builds</span></span>
<span data-ttu-id="bc04d-174">W niektórych przypadkach zmiennych lokalnych nie można wyświetlić w kompilacjach wydania z powodu optymalizacji, które są stosowane podczas procesu kompilacji.</span><span class="sxs-lookup"><span data-stu-id="bc04d-174">In some cases, local variables cannot be viewed in release builds because of optimizations that are applied during the build process.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="bc04d-175">Rozwiązywanie problemów</span><span class="sxs-lookup"><span data-stu-id="bc04d-175">Troubleshooting</span></span>

<span data-ttu-id="bc04d-176">Te wskazówki ułatwiają rozwiązywanie problemów z debugera migawki.</span><span class="sxs-lookup"><span data-stu-id="bc04d-176">These tips help you troubleshoot problems with the Snapshot Debugger.</span></span>

### <a name="verify-the-instrumentation-key"></a><span data-ttu-id="bc04d-177">Sprawdź klucza Instrumentacji</span><span class="sxs-lookup"><span data-stu-id="bc04d-177">Verify the instrumentation key</span></span>

<span data-ttu-id="bc04d-178">Upewnij się, że używasz klucza Instrumentacji poprawne w opublikowanej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="bc04d-178">Make sure that you're using the correct instrumentation key in your published application.</span></span> <span data-ttu-id="bc04d-179">Zazwyczaj usługi Application Insights odczytuje klucza Instrumentacji z pliku ApplicationInsights.config.</span><span class="sxs-lookup"><span data-stu-id="bc04d-179">Usually, Application Insights reads the instrumentation key from the ApplicationInsights.config file.</span></span> <span data-ttu-id="bc04d-180">Sprawdź, czy wartość jest taka sama jak klucza instrumentacji dla zasobu usługi Application Insights, który zostanie wyświetlony w portalu.</span><span class="sxs-lookup"><span data-stu-id="bc04d-180">Verify that the value is the same as the instrumentation key for the Application Insights resource that you see in the portal.</span></span>

### <a name="check-the-uploader-logs"></a><span data-ttu-id="bc04d-181">Sprawdź dzienniki przesyłania</span><span class="sxs-lookup"><span data-stu-id="bc04d-181">Check the uploader logs</span></span>

<span data-ttu-id="bc04d-182">Po utworzeniu migawki, plik minizrzutu (dmp) jest tworzony na dysku.</span><span class="sxs-lookup"><span data-stu-id="bc04d-182">After a snapshot is created, a minidump file (.dmp) is created on disk.</span></span> <span data-ttu-id="bc04d-183">Proces przesyłania oddzielne przyjmuje ten plik minizrzutu i przekazuje, oraz wszystkie skojarzone pliki PDB do magazynu Application Insights migawki debugera.</span><span class="sxs-lookup"><span data-stu-id="bc04d-183">A separate uploader process takes that minidump file and uploads it, along with any associated PDBs, to Application Insights Snapshot Debugger storage.</span></span> <span data-ttu-id="bc04d-184">Po pomyślnym przekazaniu minizrzut są usuwane z dysku.</span><span class="sxs-lookup"><span data-stu-id="bc04d-184">After the minidump has uploaded successfully, it is deleted from disk.</span></span> <span data-ttu-id="bc04d-185">Pliki dzienników w celu przesyłania minizrzutu są przechowywane na dysku.</span><span class="sxs-lookup"><span data-stu-id="bc04d-185">The log files for the minidump uploader are retained on disk.</span></span> <span data-ttu-id="bc04d-186">W środowisku usługi aplikacji można znaleźć te dzienniki w `D:\Home\LogFiles\Uploader_*.log`.</span><span class="sxs-lookup"><span data-stu-id="bc04d-186">In an App Service environment, you can find these logs in `D:\Home\LogFiles\Uploader_*.log`.</span></span> <span data-ttu-id="bc04d-187">Użyj witryny zarządzania Kudu dla aplikacji usługi, aby znaleźć te pliki dziennika.</span><span class="sxs-lookup"><span data-stu-id="bc04d-187">Use the Kudu management site for App Service to find these log files.</span></span>

1. <span data-ttu-id="bc04d-188">Otwórz aplikację usługi aplikacji w portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="bc04d-188">Open your App Service application in the Azure portal.</span></span>

2. <span data-ttu-id="bc04d-189">Wybierz **zaawansowane narzędzia** bloku lub Wyszukaj **Kudu**.</span><span class="sxs-lookup"><span data-stu-id="bc04d-189">Select the **Advanced Tools** blade, or search for **Kudu**.</span></span>
3. <span data-ttu-id="bc04d-190">Kliknij przycisk **Przejdź**.</span><span class="sxs-lookup"><span data-stu-id="bc04d-190">Click **Go**.</span></span>
4. <span data-ttu-id="bc04d-191">W **konsoli debugowania** listy rozwijanej wybierz pozycję **CMD**.</span><span class="sxs-lookup"><span data-stu-id="bc04d-191">In the **Debug console** drop-down list box, select **CMD**.</span></span>
5. <span data-ttu-id="bc04d-192">Kliknij przycisk **LogFiles**.</span><span class="sxs-lookup"><span data-stu-id="bc04d-192">Click **LogFiles**.</span></span>

<span data-ttu-id="bc04d-193">Powinny pojawić się co najmniej jeden plik o nazwie, który rozpoczyna się od `Uploader_` i `.log` rozszerzenia.</span><span class="sxs-lookup"><span data-stu-id="bc04d-193">You should see at least one file with a name that begins with `Uploader_` and a `.log` extension.</span></span> <span data-ttu-id="bc04d-194">Kliknij odpowiednią ikonę, aby pobrać wszystkie pliki dziennika lub je otworzyć w przeglądarce.</span><span class="sxs-lookup"><span data-stu-id="bc04d-194">Click the appropriate icon to download any log files or open them in a browser.</span></span>
<span data-ttu-id="bc04d-195">Nazwa pliku zawiera nazwę komputera.</span><span class="sxs-lookup"><span data-stu-id="bc04d-195">The file name includes the machine name.</span></span> <span data-ttu-id="bc04d-196">Jeśli wystąpienie usługi aplikacji znajduje się na więcej niż jednej maszynie, istnieją oddzielnych plików dziennika dla każdego komputera.</span><span class="sxs-lookup"><span data-stu-id="bc04d-196">If your App Service instance is hosted on more than one machine, there are separate log files for each machine.</span></span> <span data-ttu-id="bc04d-197">Gdy przekazujący wykryje nowy plik minizrzutu, jest rejestrowany w pliku dziennika.</span><span class="sxs-lookup"><span data-stu-id="bc04d-197">When the uploader detects a new minidump file, it is recorded in the log file.</span></span> <span data-ttu-id="bc04d-198">Oto przykład pomyślne ukończenie przekazywania:</span><span class="sxs-lookup"><span data-stu-id="bc04d-198">Here's an example of a successful upload:</span></span>

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

<span data-ttu-id="bc04d-199">W poprzednim przykładzie, klucz Instrumentacji jest `c12a605e73c44346a984e00000000000`.</span><span class="sxs-lookup"><span data-stu-id="bc04d-199">In the previous example, the instrumentation key is `c12a605e73c44346a984e00000000000`.</span></span> <span data-ttu-id="bc04d-200">Ta wartość powinna być zgodna klucza instrumentacji aplikacji.</span><span class="sxs-lookup"><span data-stu-id="bc04d-200">This value should match the instrumentation key for your application.</span></span>
<span data-ttu-id="bc04d-201">Minizrzut jest skojarzony z migawki z Identyfikatorem `139e411a23934dc0b9ea08a626db16c5`.</span><span class="sxs-lookup"><span data-stu-id="bc04d-201">The minidump is associated with a snapshot with the ID `139e411a23934dc0b9ea08a626db16c5`.</span></span> <span data-ttu-id="bc04d-202">Ten identyfikator można użyć do zlokalizowania telemetrii skojarzony wyjątek w Application Insights Analytics później.</span><span class="sxs-lookup"><span data-stu-id="bc04d-202">You can use this ID later to locate the associated exception telemetry in Application Insights Analytics.</span></span>

<span data-ttu-id="bc04d-203">Przekazujący skanowania pod kątem nowych baz danych PDB o co 15 minut.</span><span class="sxs-lookup"><span data-stu-id="bc04d-203">The uploader scans for new PDBs about once every 15 minutes.</span></span> <span data-ttu-id="bc04d-204">Oto przykład:</span><span class="sxs-lookup"><span data-stu-id="bc04d-204">Here's an example:</span></span>

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

<span data-ttu-id="bc04d-205">W przypadku aplikacji, które są _nie_ hostowanych w usłudze App Service, dzienniki przesyłania znajdują się w tym samym folderze co minizrzutów: `%TEMP%\Dumps\<ikey>` (gdzie `<ikey>` jest klucz Instrumentacji).</span><span class="sxs-lookup"><span data-stu-id="bc04d-205">For applications that are _not_ hosted in App Service, the uploader logs are in the same folder as the minidumps: `%TEMP%\Dumps\<ikey>` (where `<ikey>` is your instrumentation key).</span></span>

### <a name="use-application-insights-search-to-find-exceptions-with-snapshots"></a><span data-ttu-id="bc04d-206">Użyj usługi Application Insights Wyszukaj, aby znaleźć wyjątki z migawkami</span><span class="sxs-lookup"><span data-stu-id="bc04d-206">Use Application Insights search to find exceptions with snapshots</span></span>

<span data-ttu-id="bc04d-207">Po utworzeniu migawki przerzucane wyjątek zostanie oznaczony przy użyciu identyfikatora migawki.</span><span class="sxs-lookup"><span data-stu-id="bc04d-207">When a snapshot is created, the throwing exception is tagged with a snapshot ID.</span></span> <span data-ttu-id="bc04d-208">Gdy dane telemetryczne wyjątku jest zgłaszane do usługi Application Insights, czy identyfikator migawki jest uwzględniona jako właściwości niestandardowej.</span><span class="sxs-lookup"><span data-stu-id="bc04d-208">When the exception telemetry is reported to Application Insights, that snapshot ID is included as a custom property.</span></span> <span data-ttu-id="bc04d-209">Za pomocą bloku wyszukiwania w usłudze Application Insights, można znaleźć wszystkie dane telemetryczne z `ai.snapshot.id` właściwości niestandardowej.</span><span class="sxs-lookup"><span data-stu-id="bc04d-209">Using the Search blade in Application Insights, you can find all telemetry with the `ai.snapshot.id` custom property.</span></span>

1. <span data-ttu-id="bc04d-210">Przejdź do zasobu usługi Application Insights w portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="bc04d-210">Browse to your Application Insights resource in the Azure portal.</span></span>
2. <span data-ttu-id="bc04d-211">Kliknij przycisk **wyszukiwania**.</span><span class="sxs-lookup"><span data-stu-id="bc04d-211">Click **Search**.</span></span>
3. <span data-ttu-id="bc04d-212">Typ `ai.snapshot.id` w polu tekstowym wyszukiwania i naciśnij klawisz Enter.</span><span class="sxs-lookup"><span data-stu-id="bc04d-212">Type `ai.snapshot.id` in the Search text box and press Enter.</span></span>

![Wyszukaj dane telemetryczne z Identyfikatorem migawki w portalu](./media/app-insights-snapshot-debugger/search-snapshot-portal.png)

<span data-ttu-id="bc04d-214">Jeśli wyszukiwanie nie zwróciło żadnych wyników, migawek nie zostały zgłoszone w do usługi Application Insights dla aplikacji w wybranym zakresie czasu.</span><span class="sxs-lookup"><span data-stu-id="bc04d-214">If this search returns no results, then no snapshots were reported to Application Insights for your application in the selected time range.</span></span>

<span data-ttu-id="bc04d-215">Aby wyszukać Identyfikatora określoną migawkę z dzienników przesyłania, należy wpisać ten identyfikator w polu wyszukiwania.</span><span class="sxs-lookup"><span data-stu-id="bc04d-215">To search for a specific snapshot ID from the Uploader logs, type that ID in the Search box.</span></span> <span data-ttu-id="bc04d-216">Jeśli nie możesz znaleźć dane telemetryczne dla migawki, który został przekazany, wykonaj następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="bc04d-216">If you can't find telemetry for a snapshot that you know was uploaded, follow these steps:</span></span>

1. <span data-ttu-id="bc04d-217">Sprawdź, czy przeglądania prawo zasobu usługi Application Insights, upewniając klucza instrumentacji.</span><span class="sxs-lookup"><span data-stu-id="bc04d-217">Double-check that you're looking at the right Application Insights resource by verifying the instrumentation key.</span></span>

2. <span data-ttu-id="bc04d-218">Przy użyciu sygnatury czasowej w dzienniku przekazujący, Dostosuj zakres czasu filtr wyszukiwania, aby pokrywał się tego zakresu czasu.</span><span class="sxs-lookup"><span data-stu-id="bc04d-218">Using the timestamp from the Uploader log, adjust the Time Range filter of the search to cover that time range.</span></span>

<span data-ttu-id="bc04d-219">Jeśli nadal nie widać Wystąpił wyjątek o takim identyfikatorze migawki, dane telemetryczne wyjątku nie zgłosił do usługi Application Insights.</span><span class="sxs-lookup"><span data-stu-id="bc04d-219">If you still don't see an exception with that snapshot ID, then the exception telemetry wasn't reported to Application Insights.</span></span> <span data-ttu-id="bc04d-220">Taka sytuacja może się zdarzyć, jeśli awaria aplikacji po zajęło migawki, ale przed zgłosiła ona dane telemetryczne wyjątku.</span><span class="sxs-lookup"><span data-stu-id="bc04d-220">This situation can happen if your application crashed after it took the snapshot but before it reported the exception telemetry.</span></span> <span data-ttu-id="bc04d-221">W takim wypadku zapoznaj się z dziennikami usługi aplikacji w obszarze `Diagnose and solve problems` aby zobaczyć, czy wystąpiły nieoczekiwane ponowne uruchomienia lub nieobsługiwane wyjątki.</span><span class="sxs-lookup"><span data-stu-id="bc04d-221">In this case, check the App Service logs under `Diagnose and solve problems` to see if there were unexpected restarts or unhandled exceptions.</span></span>

## <a name="next-steps"></a><span data-ttu-id="bc04d-222">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="bc04d-222">Next steps</span></span>

* <span data-ttu-id="bc04d-223">[Ustaw snappoints w kodzie](https://azure.microsoft.com/blog/snapshot-debugger-for-azure/) można pobrać migawek bez oczekiwania na wyjątek.</span><span class="sxs-lookup"><span data-stu-id="bc04d-223">[Set snappoints in your code](https://azure.microsoft.com/blog/snapshot-debugger-for-azure/) to get snapshots without waiting for an exception.</span></span>
* <span data-ttu-id="bc04d-224">[Diagnozowanie wyjątków w aplikacjach sieci web](app-insights-asp-net-exceptions.md) wyjaśniono, jak wyświetlić więcej wyjątków do usługi Application Insights.</span><span class="sxs-lookup"><span data-stu-id="bc04d-224">[Diagnose exceptions in your web apps](app-insights-asp-net-exceptions.md) explains how to make more exceptions visible to Application Insights.</span></span> 
* <span data-ttu-id="bc04d-225">[Inteligentne wykrywania](app-insights-proactive-diagnostics.md) automatycznie odnajduje anomalii wydajności.</span><span class="sxs-lookup"><span data-stu-id="bc04d-225">[Smart Detection](app-insights-proactive-diagnostics.md) automatically discovers performance anomalies.</span></span>
