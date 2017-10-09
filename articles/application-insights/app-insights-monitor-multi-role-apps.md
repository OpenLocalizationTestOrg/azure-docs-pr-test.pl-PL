---
title: "aaaAzure usługi Application Insights Obsługa wielu składników, mikrousług i kontenery | Dokumentacja firmy Microsoft"
description: "Monitorowanie aplikacji, które składają się z wielu składników lub ról, wydajności i użycia."
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 05/17/2017
ms.author: bwren
ms.openlocfilehash: 6185eedf32ec450d7541603b94de6c3dcdf64a85
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-multi-component-applications-with-application-insights-preview"></a><span data-ttu-id="16a89-103">Monitorowanie wielu składnika aplikacji za pomocą usługi Application Insights (wersja zapoznawcza)</span><span class="sxs-lookup"><span data-stu-id="16a89-103">Monitor multi-component applications with Application Insights (preview)</span></span>

<span data-ttu-id="16a89-104">Można monitorować aplikacje, które składają się z wielu składników serwera, ról lub usług z [Azure Application Insights](app-insights-overview.md).</span><span class="sxs-lookup"><span data-stu-id="16a89-104">You can monitor apps that consist of multiple server components, roles, or services with [Azure Application Insights](app-insights-overview.md).</span></span> <span data-ttu-id="16a89-105">Hello kondycji składników hello i hello relacji między nimi są wyświetlane na mapie jednej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="16a89-105">hello health of hello components and hello relationships between them are displayed on a single Application Map.</span></span> <span data-ttu-id="16a89-106">Można śledzić poszczególnych działań przez kilka składników z automatycznego korelacji HTTP.</span><span class="sxs-lookup"><span data-stu-id="16a89-106">You can trace individual operations through multiple components with automatic HTTP correlation.</span></span> <span data-ttu-id="16a89-107">Diagnostyka kontenera można zintegrowany i skorelowane z danych telemetrycznych aplikacji.</span><span class="sxs-lookup"><span data-stu-id="16a89-107">Container diagnostics can be integrated and correlated with application telemetry.</span></span> <span data-ttu-id="16a89-108">Użyj pojedynczego zasobu usługi Application Insights dla wszystkich składników aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="16a89-108">Use a single Application Insights resource for all hello components of your application.</span></span> 

![Mapowanie wielu składnika aplikacji](./media/app-insights-monitor-multi-role-apps/app-map.png)

<span data-ttu-id="16a89-110">Używamy "component" toomean tutaj dowolnej działa części dużych aplikacji.</span><span class="sxs-lookup"><span data-stu-id="16a89-110">We use 'component' here toomean any functioning part of a large application.</span></span> <span data-ttu-id="16a89-111">Na przykład typowa aplikacja biznesowa może składać się z kodu klienta działający w przeglądarkach sieci web, mówić tooone lub usług kończyć więcej usług aplikacji sieci web, które z kolei użyć ponownie.</span><span class="sxs-lookup"><span data-stu-id="16a89-111">For example, a typical business application may consist of client code running in web browsers, talking tooone or more web app services, which in turn use back end services.</span></span> <span data-ttu-id="16a89-112">Składniki serwera może być obsługiwana lokalnie na powitania chmury, może być Azure role sieci web i proces roboczy lub może działać w kontenerach, takich jak Docker lub sieci szkieletowej usług.</span><span class="sxs-lookup"><span data-stu-id="16a89-112">Server components may be hosted on-premises on in hello cloud, or may be Azure web and worker roles, or may run in containers such as Docker or Service Fabric.</span></span> 

### <a name="sharing-a-single-application-insights-resource"></a><span data-ttu-id="16a89-113">Udostępnianie pojedynczego zasobu usługi Application Insights</span><span class="sxs-lookup"><span data-stu-id="16a89-113">Sharing a single Application Insights resource</span></span> 

<span data-ttu-id="16a89-114">Witaj klucza technika tutaj jest toosend telemetrii od każdego składnika w Twojej aplikacji toohello tego samego zasobu usługi Application Insights, ale użyj hello `cloud_RoleName` składniki toodistinguish właściwości, gdy jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="16a89-114">hello key technique here is toosend telemetry from every component in your application toohello same Application Insights resource, but use hello `cloud_RoleName` property toodistinguish components when necessary.</span></span> <span data-ttu-id="16a89-115">zestaw SDK usługi Application Insights Hello dodaje hello `cloud_RoleName` Emituj właściwości toohello telemetrii składników.</span><span class="sxs-lookup"><span data-stu-id="16a89-115">hello Application Insights SDK adds hello `cloud_RoleName` property toohello telemetry components emit.</span></span> <span data-ttu-id="16a89-116">Na przykład hello SDK doda nazwa witryny sieci web lub usługi roli nazwa toohello `cloud_RoleName` właściwości.</span><span class="sxs-lookup"><span data-stu-id="16a89-116">For example, hello SDK will add a web site name, or service role name toohello `cloud_RoleName` property.</span></span> <span data-ttu-id="16a89-117">Można zastąpić tę wartość z telemetryinitializer.</span><span class="sxs-lookup"><span data-stu-id="16a89-117">You can override this value with a telemetryinitializer.</span></span> <span data-ttu-id="16a89-118">Mapowanie aplikacji Hello używa hello `cloud_RoleName` właściwości tooidentify hello składników na mapie hello.</span><span class="sxs-lookup"><span data-stu-id="16a89-118">hello Application Map uses hello `cloud_RoleName` property tooidentify hello components on hello map.</span></span>

<span data-ttu-id="16a89-119">Aby uzyskać więcej informacji o tym, jak zastąpić hello `cloud_RoleName` Zobacz właściwość [dodać właściwości: ITelemetryInitializer](app-insights-api-filtering-sampling.md#add-properties-itelemetryinitializer).</span><span class="sxs-lookup"><span data-stu-id="16a89-119">For more information about how do override hello `cloud_RoleName` property see [Add properties: ITelemetryInitializer](app-insights-api-filtering-sampling.md#add-properties-itelemetryinitializer).</span></span>  

<span data-ttu-id="16a89-120">W niektórych przypadkach to nie może być odpowiednie, a lepiej toouse oddzielnych zasobów dla różnych grup składników.</span><span class="sxs-lookup"><span data-stu-id="16a89-120">In some cases, this may not be appropriate, and you may prefer toouse separate resources for different groups of components.</span></span> <span data-ttu-id="16a89-121">Na przykład może być konieczne toouse różne zasoby do zarządzania lub rozliczeń do celów.</span><span class="sxs-lookup"><span data-stu-id="16a89-121">For example, you might need toouse different resources for management or billing purposes.</span></span> <span data-ttu-id="16a89-122">Korzystanie z osobnych zasobów oznacza, że nie wyświetlone wszystkie składniki hello wyświetlany w jednym mapowaniu aplikacji; oraz że nie można zbadać elementów w [Analytics](app-insights-analytics.md).</span><span class="sxs-lookup"><span data-stu-id="16a89-122">Using separate resources means that you don't see all hello components displayed on a single Application Map; and that you can't query across components in [Analytics](app-insights-analytics.md).</span></span> <span data-ttu-id="16a89-123">Masz również tooset hello oddzielnych zasobów.</span><span class="sxs-lookup"><span data-stu-id="16a89-123">You also have tooset up hello separate resources.</span></span>

<span data-ttu-id="16a89-124">Z tym ostrzeżenie przyjmiemy w hello pozostałej części tego dokumentu oznaczający toosend danych z wielu składników tooone zasobu usługi Application Insights.</span><span class="sxs-lookup"><span data-stu-id="16a89-124">With that caveat, we'll assume in hello rest of this document that you want toosend data from multiple components tooone Application Insights resource.</span></span>

## <a name="configure-multi-component-applications"></a><span data-ttu-id="16a89-125">Konfigurowanie wielu składnika aplikacji</span><span class="sxs-lookup"><span data-stu-id="16a89-125">Configure multi-component applications</span></span>

<span data-ttu-id="16a89-126">Mapowanie wielu składnika aplikacji tooget, należy tooachieve tych celów:</span><span class="sxs-lookup"><span data-stu-id="16a89-126">tooget a multi-component application map, you need tooachieve these goals:</span></span>

* <span data-ttu-id="16a89-127">**Instalowanie najnowszej wersji wstępnej hello** pakiet usługi Application Insights w poszczególnych składników aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="16a89-127">**Install hello latest pre-release** Application Insights package in each component of hello application.</span></span> 
* <span data-ttu-id="16a89-128">**Udostępnij pojedynczy zasób usługi Application Insights** dla hello wszystkich składników aplikacji.</span><span class="sxs-lookup"><span data-stu-id="16a89-128">**Share a single Application Insights resource** for all hello components of your application.</span></span>
* <span data-ttu-id="16a89-129">**Włączyć usługi roli aplikacji mapy** w bloku podglądy hello.</span><span class="sxs-lookup"><span data-stu-id="16a89-129">**Enable Multi-role Application Map** in hello Previews blade.</span></span>

<span data-ttu-id="16a89-130">Skonfiguruj poszczególnych składników aplikacji przy użyciu metody odpowiedniej powitania dla jego typu.</span><span class="sxs-lookup"><span data-stu-id="16a89-130">Configure each component of your application using hello appropriate method for its type.</span></span> <span data-ttu-id="16a89-131">([ASP.NET](app-insights-asp-net.md), [Java](app-insights-java-get-started.md), [Node.js](app-insights-nodejs.md), [JavaScript](app-insights-javascript.md).)</span><span class="sxs-lookup"><span data-stu-id="16a89-131">([ASP.NET](app-insights-asp-net.md), [Java](app-insights-java-get-started.md), [Node.js](app-insights-nodejs.md), [JavaScript](app-insights-javascript.md).)</span></span>

### <a name="1-install-hello-latest-pre-release-package"></a><span data-ttu-id="16a89-132">1. Zainstaluj najnowszy pakiet wersji wstępnej hello</span><span class="sxs-lookup"><span data-stu-id="16a89-132">1. Install hello latest pre-release package</span></span>

<span data-ttu-id="16a89-133">Zaktualizuj lub zainstaluj hello wgląd w aplikację pakietów hello projektu dla każdego składnika serwera.</span><span class="sxs-lookup"><span data-stu-id="16a89-133">Update or install hello Appication Insights packages in hello project for each server component.</span></span> <span data-ttu-id="16a89-134">Jeśli używasz programu Visual Studio:</span><span class="sxs-lookup"><span data-stu-id="16a89-134">If you're using Visual Studio:</span></span>

1. <span data-ttu-id="16a89-135">Kliknij prawym przyciskiem myszy projekt i wybierz **Zarządzaj pakietami NuGet**.</span><span class="sxs-lookup"><span data-stu-id="16a89-135">Right-click a project and select **Manage NuGet Packages**.</span></span> 
2. <span data-ttu-id="16a89-136">Wybierz **Uwzględnij wersję wstępną**.</span><span class="sxs-lookup"><span data-stu-id="16a89-136">Select **Include prerelease**.</span></span>
3. <span data-ttu-id="16a89-137">Jeśli usługi Application Insights pakiety są widoczne w aktualizacji, zaznacz je.</span><span class="sxs-lookup"><span data-stu-id="16a89-137">If Application Insights packages appear in Updates, select them.</span></span> 

    <span data-ttu-id="16a89-138">W przeciwnym razie przeglądania i instalowania hello odpowiedniego pakietu:</span><span class="sxs-lookup"><span data-stu-id="16a89-138">Otherwise, browse for and install hello appropriate package:</span></span>
    
    * <span data-ttu-id="16a89-139">Microsoft.ApplicationInsights.WindowsServer</span><span class="sxs-lookup"><span data-stu-id="16a89-139">Microsoft.ApplicationInsights.WindowsServer</span></span>
    * <span data-ttu-id="16a89-140">Microsoft.ApplicationInsights.ServiceFabric - składników uruchomiony jako gość plików wykonywalnych i kontenery Docker uruchamiania aplikacji w sieci szkieletowej usług</span><span class="sxs-lookup"><span data-stu-id="16a89-140">Microsoft.ApplicationInsights.ServiceFabric - for components running as guest executables and Docker containers running a in Service Fabric application</span></span>
    * <span data-ttu-id="16a89-141">Microsoft.ApplicationInsights.ServiceFabric.Native - niezawodnych usług w aplikacjach ServiceFabric</span><span class="sxs-lookup"><span data-stu-id="16a89-141">Microsoft.ApplicationInsights.ServiceFabric.Native - for reliable services in ServiceFabric applications</span></span>
    * <span data-ttu-id="16a89-142">Microsoft.ApplicationInsights.Kubernetes składników działających w Docker na Kubernetes</span><span class="sxs-lookup"><span data-stu-id="16a89-142">Microsoft.ApplicationInsights.Kubernetes for components running in Docker on Kubernetes</span></span>

### <a name="2-share-a-single-application-insights-resource"></a><span data-ttu-id="16a89-143">2. Udostępnij pojedynczy zasób usługi Application Insights</span><span class="sxs-lookup"><span data-stu-id="16a89-143">2. Share a single Application Insights resource</span></span>

* <span data-ttu-id="16a89-144">W programie Visual Studio, kliknij prawym przyciskiem myszy projekt i wybierz **Konfiguruj usługę Application Insights**, lub **usługi Application Insights > Konfiguruj**.</span><span class="sxs-lookup"><span data-stu-id="16a89-144">In Visual Studio, right-click a project and select **Configure Application Insights**, or **Application Insights > Configure**.</span></span> <span data-ttu-id="16a89-145">Dla pierwszego projektu hello Użyj toocreate kreatora hello zasobu usługi Application Insights.</span><span class="sxs-lookup"><span data-stu-id="16a89-145">For hello first project, use hello wizard toocreate an Application Insights resource.</span></span> <span data-ttu-id="16a89-146">W przypadku kolejnych projektów wybierz hello tego samego zasobu.</span><span class="sxs-lookup"><span data-stu-id="16a89-146">For subsequent projects, select hello same resource.</span></span>
* <span data-ttu-id="16a89-147">Jeśli nie ma żadnych menu usługi Application Insights, skonfigurować ręcznie:</span><span class="sxs-lookup"><span data-stu-id="16a89-147">If there is no Application Insights menu, configure manually:</span></span>

   1. <span data-ttu-id="16a89-148">W [portalu Azure](https://portal,azure.com), otwórz zasobu usługi Application Insights hello już utworzone dla innego składnika.</span><span class="sxs-lookup"><span data-stu-id="16a89-148">In [Azure portal](https://portal,azure.com), open hello Application Insights resource you already created for another component.</span></span>
   2. <span data-ttu-id="16a89-149">W bloku omówienie hello, otwórz hello rozwijanej Essentials kartę i hello kopiowania **klucza instrumentacji.**</span><span class="sxs-lookup"><span data-stu-id="16a89-149">In hello Overview blade, open hello Essentials drop-down tab, and copy hello **Instrumentation Key.**</span></span>
   3. <span data-ttu-id="16a89-150">W projekcie Otwórz ApplicationInsights.config i Wstaw:`<InstrumentationKey>your copied key</InstrumentationKey>`</span><span class="sxs-lookup"><span data-stu-id="16a89-150">In your project, open ApplicationInsights.config and insert: `<InstrumentationKey>your copied key</InstrumentationKey>`</span></span>

![Skopiuj plik .config toohello klucza Instrumentacji hello](./media/app-insights-monitor-multi-role-apps/copy-instrumentation-key.png)


### <a name="3-enable-multi-role-application-map"></a><span data-ttu-id="16a89-152">3. Włącz mapowanie wielu roli w aplikacji</span><span class="sxs-lookup"><span data-stu-id="16a89-152">3. Enable multi-role Application Map</span></span>

<span data-ttu-id="16a89-153">Hello portalu Azure Otwórz hello zasobów dla aplikacji.</span><span class="sxs-lookup"><span data-stu-id="16a89-153">In hello Azure portal, open hello resource for your application.</span></span> <span data-ttu-id="16a89-154">W bloku podglądy hello, Włącz *Mapa aplikacji usługi roli*.</span><span class="sxs-lookup"><span data-stu-id="16a89-154">In hello Previews blade, enable *Multi-role Application Map*.</span></span>

### <a name="4-enable-docker-metrics-optional"></a><span data-ttu-id="16a89-155">4. Włączyć metryki Docker (opcjonalnie)</span><span class="sxs-lookup"><span data-stu-id="16a89-155">4. Enable Docker metrics (Optional)</span></span> 

<span data-ttu-id="16a89-156">Jeśli składnik jest uruchomiony w Docker hostowanych na maszynie Wirtualnej Windows Azure, można zbierać dodatkowe metryki z kontenera hello.</span><span class="sxs-lookup"><span data-stu-id="16a89-156">If a component runs in a Docker hosted on an Azure Windows VM, you can collect additional metrics from hello container.</span></span> <span data-ttu-id="16a89-157">Wstawianie w Twojej [diagnostyki Azure](../monitoring-and-diagnostics/azure-diagnostics.md) pliku konfiguracji:</span><span class="sxs-lookup"><span data-stu-id="16a89-157">Insert this in your [Azure diagnostics](../monitoring-and-diagnostics/azure-diagnostics.md) configuration file:</span></span>

```
"DiagnosticMonitorConfiguration": {
        ...
        "sinks": "applicationInsights",
        "DockerSources": {
                "Stats": {
                    "enabled": true,
                    "sampleRate": "PT1M"
                }
            },
        ...
    }
    ...   
    "SinksConfig": {
        "Sink": [{
            "name": "applicationInsights",
            "ApplicationInsights": "<your instrumentation key here>"
        }]
    }
    ...
}

```

## <a name="use-cloudrolename-tooseparate-components"></a><span data-ttu-id="16a89-158">Użyj cloud_RoleName tooseparate składników</span><span class="sxs-lookup"><span data-stu-id="16a89-158">Use cloud_RoleName tooseparate components</span></span>

<span data-ttu-id="16a89-159">Witaj `cloud_RoleName` właściwość jest dołączona tooall telemetrii.</span><span class="sxs-lookup"><span data-stu-id="16a89-159">hello `cloud_RoleName` property is attached tooall telemetry.</span></span> <span data-ttu-id="16a89-160">Identyfikuje składnik hello - hello roli lub usługi -, który pochodzi hello telemetrii.</span><span class="sxs-lookup"><span data-stu-id="16a89-160">It identifies hello component - hello role or service - that originates hello telemetry.</span></span> <span data-ttu-id="16a89-161">(Jest nie hello takie same jak cloud_RoleInstance, która oddziela identyczne ról, które są uruchomione jednocześnie na wielu procesy serwera lub maszyny).</span><span class="sxs-lookup"><span data-stu-id="16a89-161">(It is not hello same as cloud_RoleInstance, which separates identical roles that are running in parallel on multiple server processes or machines.)</span></span>

<span data-ttu-id="16a89-162">W portalu hello możesz filtrować i segment telemetrii za pomocą tej właściwości.</span><span class="sxs-lookup"><span data-stu-id="16a89-162">In hello portal, you can filter or segment your telemetry using this property.</span></span> <span data-ttu-id="16a89-163">W tym przykładzie blok błędów hello jest filtrowane tooshow tylko informacje z usługi frontonu sieci web hello, filtrowanie błędów z zaplecza interfejsu API CRM hello:</span><span class="sxs-lookup"><span data-stu-id="16a89-163">In this example, hello Failures blade is filtered tooshow just information from hello front-end web service, filtering out failures from hello CRM API backend:</span></span>

![Metryki wykresu segmentowanych przez nazwę roli chmury](./media/app-insights-monitor-multi-role-apps/cloud-role-name.png)

## <a name="trace-operations-between-components"></a><span data-ttu-id="16a89-165">Operacje śledzenia między składnikami</span><span class="sxs-lookup"><span data-stu-id="16a89-165">Trace operations between components</span></span>

<span data-ttu-id="16a89-166">Można śledzić tooanother jeden składnik, hello wywołań podczas przetwarzania indywidualnych operacji.</span><span class="sxs-lookup"><span data-stu-id="16a89-166">You can trace from one component tooanother, hello calls made while processing an individual operation.</span></span>


![Pokaż dane telemetryczne dla operacji](./media/app-insights-monitor-multi-role-apps/show-telemetry-for-operation.png)

<span data-ttu-id="16a89-168">Kliknij za pośrednictwem listy skorelowane tooa dane telemetryczne dla tej operacji na powitania serwera frontonu sieci web i interfejs API zaplecza hello:</span><span class="sxs-lookup"><span data-stu-id="16a89-168">Click through tooa correlated list of telemetry for this operation across hello front-end web server and hello back-end API:</span></span>

![Wyszukaj między składnikami](./media/app-insights-monitor-multi-role-apps/search-across-components.png)


## <a name="next-steps"></a><span data-ttu-id="16a89-170">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="16a89-170">Next steps</span></span>

* [<span data-ttu-id="16a89-171">Oddzielne dane telemetryczne z programowanie, testowego i produkcyjnego</span><span class="sxs-lookup"><span data-stu-id="16a89-171">Separate telemetry from Development, Test, and Production</span></span>](app-insights-separate-resources.md)
