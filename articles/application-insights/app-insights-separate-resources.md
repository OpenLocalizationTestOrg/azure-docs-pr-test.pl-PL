---
title: "telemetrii aaaSeparating z tworzenia, testowania i wersji w usłudze Azure Application Insights | Dokumentacja firmy Microsoft"
description: "Zasoby toodifferent bezpośredniego telemetrii dla rozwoju, testów i produkcji sygnatury."
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.assetid: 578e30f0-31ed-4f39-baa8-01b4c2f310c9
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 05/15/2017
ms.author: bwren
ms.openlocfilehash: a294c8c70f46d7c29b460461c3494c83e13a0cbe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="separating-telemetry-from-development-test-and-production"></a><span data-ttu-id="91dd8-103">Oddzielanie danych telemetrycznych z programowanie, testowego i produkcyjnego</span><span class="sxs-lookup"><span data-stu-id="91dd8-103">Separating telemetry from Development, Test, and Production</span></span>

<span data-ttu-id="91dd8-104">Wdrażając hello następnej wersji aplikacji sieci web, nie mają toomix się hello [usługi Application Insights](app-insights-overview.md) dane telemetryczne z hello nowej wersji i wersji hello już zwolniony.</span><span class="sxs-lookup"><span data-stu-id="91dd8-104">When you are developing hello next version of a web application, you don't want toomix up hello [Application Insights](app-insights-overview.md) telemetry from hello new version and hello already released version.</span></span> <span data-ttu-id="91dd8-105">pomyłek tooavoid wysyłania telemetrii hello z innej programowanie przygotuje tooseparate zasobów usługi Application Insights, z kluczami oddzielne Instrumentacji (ikeys).</span><span class="sxs-lookup"><span data-stu-id="91dd8-105">tooavoid confusion, send hello telemetry from different development stages tooseparate Application Insights resources, with separate instrumentation keys (ikeys).</span></span> <span data-ttu-id="91dd8-106">toomake go łatwiejsze klucza Instrumentacji w wersji toochange hello są przenoszone z tooanother jednego etapu, może być przydatne tooset ikey hello w kodzie, a nie w pliku konfiguracyjnym hello.</span><span class="sxs-lookup"><span data-stu-id="91dd8-106">toomake it easier toochange hello instrumentation key as a version moves from one stage tooanother, it can be useful tooset hello ikey in code instead of in hello configuration file.</span></span> 

<span data-ttu-id="91dd8-107">(Jeśli system jest usługi w chmurze Azure, Brak [innej metody ustawienia oddzielnych ikeys](app-insights-cloudservices.md).)</span><span class="sxs-lookup"><span data-stu-id="91dd8-107">(If your system is an Azure Cloud Service, there's [another method of setting separate ikeys](app-insights-cloudservices.md).)</span></span>

## <a name="about-resources-and-instrumentation-keys"></a><span data-ttu-id="91dd8-108">Dotyczące zasobów i klucze Instrumentacji</span><span class="sxs-lookup"><span data-stu-id="91dd8-108">About resources and instrumentation keys</span></span>

<span data-ttu-id="91dd8-109">Po skonfigurowaniu monitorowanie usługi Application Insights dla aplikacji sieci web, tworzenia usługi Application Insights *zasobów* platformie Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="91dd8-109">When you set up Application Insights monitoring for your web app, you create an Application Insights *resource* in Microsoft Azure.</span></span> <span data-ttu-id="91dd8-110">Otwórz ten zasób w portalu Azure w kolejności toosee hello i analizować hello dane telemetryczne zebrane z aplikacji.</span><span class="sxs-lookup"><span data-stu-id="91dd8-110">You open this resource in hello Azure portal in order toosee and analyze hello telemetry collected from your app.</span></span> <span data-ttu-id="91dd8-111">zasób Hello jest identyfikowany przez *klucza Instrumentacji* (ikey).</span><span class="sxs-lookup"><span data-stu-id="91dd8-111">hello resource is identified by an *instrumentation key* (ikey).</span></span> <span data-ttu-id="91dd8-112">Po zainstalowaniu hello usługi Application Insights pakietu toomonitor aplikacji, należy go skonfigurować z klucza Instrumentacji hello, tak aby wie, gdzie toosend hello telemetrii.</span><span class="sxs-lookup"><span data-stu-id="91dd8-112">When you install hello Application Insights package toomonitor your app, you configure it with hello instrumentation key, so that it knows where toosend hello telemetry.</span></span>

<span data-ttu-id="91dd8-113">Oddzielne zasoby toouse lub pojedynczego zasobu udostępnionego zwykle wybierz w różnych scenariuszach:</span><span class="sxs-lookup"><span data-stu-id="91dd8-113">You typically choose toouse separate resources or a single shared resource in different scenarios:</span></span>

* <span data-ttu-id="91dd8-114">Aplikacje innych, niezależnie od - używać oddzielnego zasobów i ikey dla każdej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="91dd8-114">Different, independent applications - Use a separate resource and ikey for each app.</span></span>
* <span data-ttu-id="91dd8-115">Wiele składników lub role w aplikacji biznesowej jeden — użyj [pojedynczy zasób udostępniony](app-insights-monitor-multi-role-apps.md) dla wszystkich hello składnika aplikacji.</span><span class="sxs-lookup"><span data-stu-id="91dd8-115">Multiple components or roles of one business application - Use a [single shared resource](app-insights-monitor-multi-role-apps.md) for all hello component apps.</span></span> <span data-ttu-id="91dd8-116">Można filtrować i segmentowanych przez właściwość cloud_RoleName hello telemetrii.</span><span class="sxs-lookup"><span data-stu-id="91dd8-116">Telemetry can be filtered or segmented by hello cloud_RoleName property.</span></span>
* <span data-ttu-id="91dd8-117">Programowanie, testu i Release - Użyj oddzielnych zasobów i ikey dla wersji systemu "sygnatury" hello etapie produkcji.</span><span class="sxs-lookup"><span data-stu-id="91dd8-117">Development, Test, and Release - Use a separate resource and ikey for versions of hello system in 'stamp' or stage of production.</span></span>
* <span data-ttu-id="91dd8-118">A | Testowanie B — użyj pojedynczego zasobu.</span><span class="sxs-lookup"><span data-stu-id="91dd8-118">A | B testing - Use a single resource.</span></span> <span data-ttu-id="91dd8-119">Utwórz TelemetryInitializer tooadd telemetrii toohello właściwości, identyfikujący hello wariantów.</span><span class="sxs-lookup"><span data-stu-id="91dd8-119">Create a TelemetryInitializer tooadd a property toohello telemetry that identifies hello variants.</span></span>


## <span data-ttu-id="91dd8-120"><a name="dynamic-ikey"></a>Klucz Instrumentacji dynamiczne</span><span class="sxs-lookup"><span data-stu-id="91dd8-120"><a name="dynamic-ikey"></a> Dynamic instrumentation key</span></span>

<span data-ttu-id="91dd8-121">toomake ułatwić ikey hello toochange jako kod hello Przenosi między etapach w produkcji, ustawić go w kodzie, a nie w pliku konfiguracyjnym hello.</span><span class="sxs-lookup"><span data-stu-id="91dd8-121">toomake it easier toochange hello ikey as hello code moves between stages of production, set it in code instead of in hello configuration file.</span></span>

<span data-ttu-id="91dd8-122">Ustaw klucz hello w metodzie inicjowania, takich jak pliku global.aspx.cs w usługi ASP.NET:</span><span class="sxs-lookup"><span data-stu-id="91dd8-122">Set hello key in an initialization method, such as global.aspx.cs in an ASP.NET service:</span></span>

<span data-ttu-id="91dd8-123">*C#*</span><span class="sxs-lookup"><span data-stu-id="91dd8-123">*C#*</span></span>

    protected void Application_Start()
    {
      Microsoft.ApplicationInsights.Extensibility.
        TelemetryConfiguration.Active.InstrumentationKey = 
          // - for example -
          WebConfigurationManager.AppSettings["ikey"];
      ...

<span data-ttu-id="91dd8-124">W tym przykładzie ikeys hello hello zasoby są umieszczane w różnych wersjach pliku konfiguracji sieci web hello.</span><span class="sxs-lookup"><span data-stu-id="91dd8-124">In this example, hello ikeys for hello different resources are placed in different versions of hello web configuration file.</span></span> <span data-ttu-id="91dd8-125">Trwa zamienianie hello pliku konfiguracji sieci web — co można zrobić w ramach skryptu hello - będzie wymiany hello zasobu docelowego.</span><span class="sxs-lookup"><span data-stu-id="91dd8-125">Swapping hello web configuration file - which you can do as part of hello release script - will swap hello target resource.</span></span>

### <a name="web-pages"></a><span data-ttu-id="91dd8-126">Strony sieci Web</span><span class="sxs-lookup"><span data-stu-id="91dd8-126">Web pages</span></span>
<span data-ttu-id="91dd8-127">Hello iKey jest również używany w aplikacji sieci web pages w hello [skryptu pochodzący z bloku szybki start hello](app-insights-javascript.md).</span><span class="sxs-lookup"><span data-stu-id="91dd8-127">hello iKey is also used in your app's web pages, in hello [script that you got from hello quick start blade](app-insights-javascript.md).</span></span> <span data-ttu-id="91dd8-128">Zamiast kodowania go bezpośrednio do skryptu hello, generować go z hello stanu serwera.</span><span class="sxs-lookup"><span data-stu-id="91dd8-128">Instead of coding it literally into hello script, generate it from hello server state.</span></span> <span data-ttu-id="91dd8-129">Na przykład w aplikacji ASP.NET:</span><span class="sxs-lookup"><span data-stu-id="91dd8-129">For example, in an ASP.NET app:</span></span>

<span data-ttu-id="91dd8-130">*Język JavaScript w Razor*</span><span class="sxs-lookup"><span data-stu-id="91dd8-130">*JavaScript in Razor*</span></span>

    <script type="text/javascript">
    // Standard Application Insights web page script:
    var appInsights = window.appInsights || function(config){ ...
    // Modify this part:
    }({instrumentationKey:  
      // Generate from server property:
      "@Microsoft.ApplicationInsights.Extensibility.
         TelemetryConfiguration.Active.InstrumentationKey"
    }) // ...


## <a name="create-additional-application-insights-resources"></a><span data-ttu-id="91dd8-131">Tworzenie dodatkowych zasobów usługi Application Insights</span><span class="sxs-lookup"><span data-stu-id="91dd8-131">Create additional Application Insights resources</span></span>
<span data-ttu-id="91dd8-132">dane telemetryczne tooseparate składników innej aplikacji, lub inną sygnaturą (deweloperów testu/produkcja) hello tego samego składnika, możesz będziesz mieć toocreate nowy zasób usługi Application Insights.</span><span class="sxs-lookup"><span data-stu-id="91dd8-132">tooseparate telemetry for different application components, or for different stamps (dev/test/production) of hello same component, then you'll have toocreate a new Application Insights resource.</span></span>

<span data-ttu-id="91dd8-133">W hello [portal.azure.com](https://portal.azure.com), Dodaj zasób usługi Application Insights:</span><span class="sxs-lookup"><span data-stu-id="91dd8-133">In hello [portal.azure.com](https://portal.azure.com), add an Application Insights resource:</span></span>

![Kliknij kolejno polecenia Nowy, Application Insights](./media/app-insights-separate-resources/01-new.png)

* <span data-ttu-id="91dd8-135">**Typ aplikacji** wpływa na informacje wyświetlane na powitania omówienie bloku i właściwości hello dostępnych w [Eksploratora metryk](app-insights-metrics-explorer.md).</span><span class="sxs-lookup"><span data-stu-id="91dd8-135">**Application type** affects what you see on hello overview blade and hello properties available in [metric explorer](app-insights-metrics-explorer.md).</span></span> <span data-ttu-id="91dd8-136">Jeśli nie widzisz typ aplikacji, wybierz jeden z typów sieci web powitania dla stron sieci web.</span><span class="sxs-lookup"><span data-stu-id="91dd8-136">If you don't see your type of app, choose one of hello web types for web pages.</span></span>
* <span data-ttu-id="91dd8-137">**Grupa zasobów** jest wygodne dla właściwości, takie jak zarządzanie [kontrola dostępu](app-insights-resources-roles-access-control.md).</span><span class="sxs-lookup"><span data-stu-id="91dd8-137">**Resource group** is a convenience for managing properties like [access control](app-insights-resources-roles-access-control.md).</span></span> <span data-ttu-id="91dd8-138">Można użyć oddzielnych grup zasobów dla rozwoju, testów i produkcji.</span><span class="sxs-lookup"><span data-stu-id="91dd8-138">You could use separate resource groups for development, test, and production.</span></span>
* <span data-ttu-id="91dd8-139">**Subskrypcja** Twojego konta płatności na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="91dd8-139">**Subscription** is your payment account in Azure.</span></span>
* <span data-ttu-id="91dd8-140">**Lokalizacja** jest, gdzie możemy przechowywanie danych.</span><span class="sxs-lookup"><span data-stu-id="91dd8-140">**Location** is where we keep your data.</span></span> <span data-ttu-id="91dd8-141">Obecnie nie można zmienić.</span><span class="sxs-lookup"><span data-stu-id="91dd8-141">Currently it can't be changed.</span></span> 
* <span data-ttu-id="91dd8-142">**Dodaj toodashboard** umieszcza kafelka szybkiego dostępu dla zasobu na stronie głównej Azure.</span><span class="sxs-lookup"><span data-stu-id="91dd8-142">**Add toodashboard** puts a quick-access tile for your resource on your Azure Home page.</span></span> 

<span data-ttu-id="91dd8-143">Tworzenie zasobu hello zajmuje kilka sekund.</span><span class="sxs-lookup"><span data-stu-id="91dd8-143">Creating hello resource takes a few seconds.</span></span> <span data-ttu-id="91dd8-144">Zostanie wyświetlony alert po jego zakończeniu.</span><span class="sxs-lookup"><span data-stu-id="91dd8-144">You'll see an alert when it's done.</span></span>

<span data-ttu-id="91dd8-145">(Można napisać [skrypt programu PowerShell](app-insights-powershell-script-create-resource.md) toocreate zasobu automatycznie.)</span><span class="sxs-lookup"><span data-stu-id="91dd8-145">(You can write a [PowerShell script](app-insights-powershell-script-create-resource.md) toocreate a resource automatically.)</span></span>

### <a name="getting-hello-instrumentation-key"></a><span data-ttu-id="91dd8-146">Wprowadzenie klucza Instrumentacji hello</span><span class="sxs-lookup"><span data-stu-id="91dd8-146">Getting hello instrumentation key</span></span>
<span data-ttu-id="91dd8-147">klucz Instrumentacji Hello identyfikuje hello utworzony zasób.</span><span class="sxs-lookup"><span data-stu-id="91dd8-147">hello instrumentation key identifies hello resource that you created.</span></span> 

![Kliknij Essentials, kliknij przycisk hello klucza Instrumentacji klawisze CTRL + C](./media/app-insights-separate-resources/02-props.png)

<span data-ttu-id="91dd8-149">Należy hello Instrumentacji klucze z wszystkich toowhich zasobów hello aplikacji będzie wysyłać dane.</span><span class="sxs-lookup"><span data-stu-id="91dd8-149">You need hello instrumentation keys of all hello resources toowhich your app will send data.</span></span>

## <a name="filter-on-build-number"></a><span data-ttu-id="91dd8-150">Filtrowanie według numeru kompilacji</span><span class="sxs-lookup"><span data-stu-id="91dd8-150">Filter on build number</span></span>
<span data-ttu-id="91dd8-151">Po opublikowaniu nowej wersji aplikacji, należy toobe tooseparate stanie hello telemetryczne z różnych kompilacji.</span><span class="sxs-lookup"><span data-stu-id="91dd8-151">When you publish a new version of your app, you'll want toobe able tooseparate hello telemetry from different builds.</span></span>

<span data-ttu-id="91dd8-152">Można ustawić właściwości wersji aplikacji hello, dzięki czemu można filtrować [wyszukiwania](app-insights-diagnostic-search.md) i [Eksploratora metryk](app-insights-metrics-explorer.md) wyników.</span><span class="sxs-lookup"><span data-stu-id="91dd8-152">You can set hello Application Version property so that you can filter [search](app-insights-diagnostic-search.md) and [metric explorer](app-insights-metrics-explorer.md) results.</span></span>

![Filtrowanie według właściwości](./media/app-insights-separate-resources/050-filter.png)

<span data-ttu-id="91dd8-154">Istnieje kilka różnych metod ustawiania właściwości wersji aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="91dd8-154">There are several different methods of setting hello Application Version property.</span></span>

* <span data-ttu-id="91dd8-155">Ustaw bezpośrednio:</span><span class="sxs-lookup"><span data-stu-id="91dd8-155">Set directly:</span></span>

    `telemetryClient.Context.Component.Version = typeof(MyProject.MyClass).Assembly.GetName().Version;`
* <span data-ttu-id="91dd8-156">Zawijaj tego wiersza w [inicjatora telemetrii](app-insights-api-custom-events-metrics.md#defaults) tooensure ustawioną wszystkich wystąpień TelemetryClient są spójne.</span><span class="sxs-lookup"><span data-stu-id="91dd8-156">Wrap that line in a [telemetry initializer](app-insights-api-custom-events-metrics.md#defaults) tooensure that all TelemetryClient instances are set consistently.</span></span>
* <span data-ttu-id="91dd8-157">[ASP.NET] Ustaw wersję hello w `BuildInfo.config`.</span><span class="sxs-lookup"><span data-stu-id="91dd8-157">[ASP.NET] Set hello version in `BuildInfo.config`.</span></span> <span data-ttu-id="91dd8-158">Moduł web Hello przejmą hello wersji z węzła BuildLabel hello.</span><span class="sxs-lookup"><span data-stu-id="91dd8-158">hello web module will pick up hello version from hello BuildLabel node.</span></span> <span data-ttu-id="91dd8-159">Dołączyć ten plik do projektu i zapamiętać tooset hello zawsze Kopiuj właściwości w Eksploratorze rozwiązań.</span><span class="sxs-lookup"><span data-stu-id="91dd8-159">Include this file in your project and remember tooset hello Copy Always property in Solution Explorer.</span></span>

    ```XML

    <?xml version="1.0" encoding="utf-8"?>
    <DeploymentEvent xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns="http://schemas.microsoft.com/VisualStudio/DeploymentEvent/2013/06">
      <ProjectName>AppVersionExpt</ProjectName>
      <Build type="MSBuild">
        <MSBuild>
          <BuildLabel kind="label">1.0.0.2</BuildLabel>
        </MSBuild>
      </Build>
    </DeploymentEvent>

    ```
* <span data-ttu-id="91dd8-160">[ASP.NET] BuildInfo.config ma być automatycznie wygenerowany w programie MSBuild.</span><span class="sxs-lookup"><span data-stu-id="91dd8-160">[ASP.NET] Generate BuildInfo.config automatically in MSBuild.</span></span> <span data-ttu-id="91dd8-161">toodo, dodaj kilka wierszy tooyour `.csproj` pliku:</span><span class="sxs-lookup"><span data-stu-id="91dd8-161">toodo this, add a few lines tooyour `.csproj` file:</span></span>

    ```XML

    <PropertyGroup>
      <GenerateBuildInfoConfigFile>true</GenerateBuildInfoConfigFile>    <IncludeServerNameInBuildInfo>true</IncludeServerNameInBuildInfo>
    </PropertyGroup>
    ```

    <span data-ttu-id="91dd8-162">Spowoduje to wygenerowanie pliku o nazwie *yourProjectName*. Witaj BuildInfo.config. proces publikowania zmienia tooBuildInfo.config.</span><span class="sxs-lookup"><span data-stu-id="91dd8-162">This generates a file called *yourProjectName*.BuildInfo.config. hello Publish process renames it tooBuildInfo.config.</span></span>

    <span data-ttu-id="91dd8-163">Etykieta kompilacji Hello zawiera symbol zastępczy (AutoGen_...) podczas kompilowania w programie Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="91dd8-163">hello build label contains a placeholder (AutoGen_...) when you build with Visual Studio.</span></span> <span data-ttu-id="91dd8-164">Jednak podczas tworzenia przy użyciu programu MSBuild, jest wypełniana hello numer poprawnej wersji.</span><span class="sxs-lookup"><span data-stu-id="91dd8-164">But when built with MSBuild, it is populated with hello correct version number.</span></span>

    <span data-ttu-id="91dd8-165">numery wersji programu MSBuild toogenerate tooallow, Ustaw wersję hello, takich jak `1.0.*` w AssemblyReference.cs</span><span class="sxs-lookup"><span data-stu-id="91dd8-165">tooallow MSBuild toogenerate version numbers, set hello version like `1.0.*` in AssemblyReference.cs</span></span>

## <a name="version-and-release-tracking"></a><span data-ttu-id="91dd8-166">Śledzenie wersji i wydania</span><span class="sxs-lookup"><span data-stu-id="91dd8-166">Version and release tracking</span></span>
<span data-ttu-id="91dd8-167">Wersja aplikacji hello tootrack, upewnij się, że `buildinfo.config` jest generowany przez proces aparatu kompilacji firmy Microsoft.</span><span class="sxs-lookup"><span data-stu-id="91dd8-167">tootrack hello application version, make sure `buildinfo.config` is generated by your Microsoft Build Engine process.</span></span> <span data-ttu-id="91dd8-168">W pliku .csproj dodaj ten kod:</span><span class="sxs-lookup"><span data-stu-id="91dd8-168">In your .csproj file, add:</span></span>  

```XML

    <PropertyGroup>
      <GenerateBuildInfoConfigFile>true</GenerateBuildInfoConfigFile>    <IncludeServerNameInBuildInfo>true</IncludeServerNameInBuildInfo>
    </PropertyGroup>
```

<span data-ttu-id="91dd8-169">Jeśli ma informacji o kompilacji hello, moduł sieci web usługi Application Insights hello automatycznie dodaje **wersja aplikacji** jako elementu właściwości tooevery telemetrii.</span><span class="sxs-lookup"><span data-stu-id="91dd8-169">When it has hello build info, hello Application Insights web module automatically adds **Application version** as a property tooevery item of telemetry.</span></span> <span data-ttu-id="91dd8-170">Umożliwiająca toofilter przez wersję podczas wykonywania [diagnostycznych wyszukiwania](app-insights-diagnostic-search.md), lub gdy użytkownik [Eksploruj metryki](app-insights-metrics-explorer.md).</span><span class="sxs-lookup"><span data-stu-id="91dd8-170">That allows you toofilter by version when you perform [diagnostic searches](app-insights-diagnostic-search.md), or when you [explore metrics](app-insights-metrics-explorer.md).</span></span>

<span data-ttu-id="91dd8-171">Jednak należy zauważyć, że numer wersji kompilacji hello jest generowany tylko przez hello kompilacji kompilacji aparatu firmy Microsoft, nie przez dewelopera hello w programie Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="91dd8-171">However, notice that hello build version number is generated only by hello Microsoft Build Engine, not by hello developer build in Visual Studio.</span></span>

### <a name="release-annotations"></a><span data-ttu-id="91dd8-172">Adnotacje dotyczące wersji</span><span class="sxs-lookup"><span data-stu-id="91dd8-172">Release annotations</span></span>
<span data-ttu-id="91dd8-173">Jeśli używasz programu Visual Studio Team Services, możesz [uzyskać znacznika adnotacji](app-insights-annotations.md) dodawane tooyour wykresy, po zwolnieniu nowej wersji.</span><span class="sxs-lookup"><span data-stu-id="91dd8-173">If you use Visual Studio Team Services, you can [get an annotation marker](app-insights-annotations.md) added tooyour charts whenever you release a new version.</span></span> <span data-ttu-id="91dd8-174">powitania po obraz przedstawia sposób wyświetlania tego znacznika.</span><span class="sxs-lookup"><span data-stu-id="91dd8-174">hello following image shows how this marker appears.</span></span>

![Zrzut ekranu przedstawiający przykładową adnotację dotyczącą wersji widoczną na wykresie](./media/app-insights-asp-net/release-annotation.png)
## <a name="next-steps"></a><span data-ttu-id="91dd8-176">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="91dd8-176">Next steps</span></span>

* [<span data-ttu-id="91dd8-177">Udostępnione zasoby do wielu ról</span><span class="sxs-lookup"><span data-stu-id="91dd8-177">Shared resources for multiple roles</span></span>](app-insights-monitor-multi-role-apps.md)
* [<span data-ttu-id="91dd8-178">Utwórz toodistinguish inicjatora Telemetrii A | Wariantów B</span><span class="sxs-lookup"><span data-stu-id="91dd8-178">Create a Telemetry Initializer toodistinguish A|B variants</span></span>](app-insights-api-filtering-sampling.md#add-properties)
