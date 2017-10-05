---
title: "Obsługa wielu składników, mikrousług i kontenery Azure Application Insights | Dokumentacja firmy Microsoft"
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
ms.openlocfilehash: ca1bb8ee886c4b4e69be9dd653d6a52b874e1f5a
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/18/2017
---
# <a name="monitor-multi-component-applications-with-application-insights-preview"></a><span data-ttu-id="ec4a3-103">Monitorowanie wielu składnika aplikacji za pomocą usługi Application Insights (wersja zapoznawcza)</span><span class="sxs-lookup"><span data-stu-id="ec4a3-103">Monitor multi-component applications with Application Insights (preview)</span></span>

<span data-ttu-id="ec4a3-104">Można monitorować aplikacje, które składają się z wielu składników serwera, ról lub usług z [Azure Application Insights](app-insights-overview.md).</span><span class="sxs-lookup"><span data-stu-id="ec4a3-104">You can monitor apps that consist of multiple server components, roles, or services with [Azure Application Insights](app-insights-overview.md).</span></span> <span data-ttu-id="ec4a3-105">Kondycji składników i relacji między nimi są wyświetlane na mapie jednej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="ec4a3-105">The health of the components and the relationships between them are displayed on a single Application Map.</span></span> <span data-ttu-id="ec4a3-106">Można śledzić poszczególnych działań przez kilka składników z automatycznego korelacji HTTP.</span><span class="sxs-lookup"><span data-stu-id="ec4a3-106">You can trace individual operations through multiple components with automatic HTTP correlation.</span></span> <span data-ttu-id="ec4a3-107">Diagnostyka kontenera można zintegrowany i skorelowane z danych telemetrycznych aplikacji.</span><span class="sxs-lookup"><span data-stu-id="ec4a3-107">Container diagnostics can be integrated and correlated with application telemetry.</span></span> <span data-ttu-id="ec4a3-108">Użyj pojedynczego zasobu usługi Application Insights dla wszystkich składników aplikacji.</span><span class="sxs-lookup"><span data-stu-id="ec4a3-108">Use a single Application Insights resource for all the components of your application.</span></span> 

![Mapowanie wielu składnika aplikacji](./media/app-insights-monitor-multi-role-apps/app-map.png)

<span data-ttu-id="ec4a3-110">"Component" używana tutaj oznacza dowolną działa część dużych aplikacji.</span><span class="sxs-lookup"><span data-stu-id="ec4a3-110">We use 'component' here to mean any functioning part of a large application.</span></span> <span data-ttu-id="ec4a3-111">Na przykład typowa aplikacja biznesowa może składać się z kodu klienta działający w przeglądarkach sieci web, rozmowie z jedną lub więcej usług aplikacji sieci web, które z kolei Użyj ponownie zakończenia usługi.</span><span class="sxs-lookup"><span data-stu-id="ec4a3-111">For example, a typical business application may consist of client code running in web browsers, talking to one or more web app services, which in turn use back end services.</span></span> <span data-ttu-id="ec4a3-112">Składniki serwera może być obsługiwana lokalnie na w chmurze lub może być Azure role sieci web i proces roboczy lub może działać w kontenerach, takich jak Docker lub sieci szkieletowej usług.</span><span class="sxs-lookup"><span data-stu-id="ec4a3-112">Server components may be hosted on-premises on in the cloud, or may be Azure web and worker roles, or may run in containers such as Docker or Service Fabric.</span></span> 

### <a name="sharing-a-single-application-insights-resource"></a><span data-ttu-id="ec4a3-113">Udostępnianie pojedynczego zasobu usługi Application Insights</span><span class="sxs-lookup"><span data-stu-id="ec4a3-113">Sharing a single Application Insights resource</span></span> 

<span data-ttu-id="ec4a3-114">W tym miejscu klucza technika jest wysłać dane telemetryczne z każdym składniku aplikacji do tego samego zasobu usługi Application Insights, ale `cloud_RoleName` właściwości odróżnienie składniki, gdy jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="ec4a3-114">The key technique here is to send telemetry from every component in your application to the same Application Insights resource, but use the `cloud_RoleName` property to distinguish components when necessary.</span></span> <span data-ttu-id="ec4a3-115">Dodaje zestaw SDK usługi Application Insights `cloud_RoleName` Emituj właściwości ze składnikami telemetrii.</span><span class="sxs-lookup"><span data-stu-id="ec4a3-115">The Application Insights SDK adds the `cloud_RoleName` property to the telemetry components emit.</span></span> <span data-ttu-id="ec4a3-116">Na przykład zestawu SDK doda nazwa witryny sieci web lub nazwę roli usługi `cloud_RoleName` właściwości.</span><span class="sxs-lookup"><span data-stu-id="ec4a3-116">For example, the SDK will add a web site name, or service role name to the `cloud_RoleName` property.</span></span> <span data-ttu-id="ec4a3-117">Można zastąpić tę wartość z telemetryinitializer.</span><span class="sxs-lookup"><span data-stu-id="ec4a3-117">You can override this value with a telemetryinitializer.</span></span> <span data-ttu-id="ec4a3-118">Mapowanie aplikacji używa `cloud_RoleName` właściwość do identyfikacji składników na mapie.</span><span class="sxs-lookup"><span data-stu-id="ec4a3-118">The Application Map uses the `cloud_RoleName` property to identify the components on the map.</span></span>

<span data-ttu-id="ec4a3-119">Aby uzyskać więcej informacji o tym, jak zastąpić `cloud_RoleName` Zobacz właściwość [dodać właściwości: ITelemetryInitializer](app-insights-api-filtering-sampling.md#add-properties-itelemetryinitializer).</span><span class="sxs-lookup"><span data-stu-id="ec4a3-119">For more information about how do override the `cloud_RoleName` property see [Add properties: ITelemetryInitializer](app-insights-api-filtering-sampling.md#add-properties-itelemetryinitializer).</span></span>  

<span data-ttu-id="ec4a3-120">W niektórych przypadkach to nie może być odpowiednie, a użytkownik może chcieć użyć oddzielnych zasobów dla różnych grup składników.</span><span class="sxs-lookup"><span data-stu-id="ec4a3-120">In some cases, this may not be appropriate, and you may prefer to use separate resources for different groups of components.</span></span> <span data-ttu-id="ec4a3-121">Na przykład może być konieczne używania różnych zasobów zarządzania lub rozliczeń do celów.</span><span class="sxs-lookup"><span data-stu-id="ec4a3-121">For example, you might need to use different resources for management or billing purposes.</span></span> <span data-ttu-id="ec4a3-122">Korzystanie z osobnych zasobów oznacza, że nie wyświetlane wszystkie składniki, które są wyświetlane w jednym mapowaniu aplikacji; oraz że nie można zbadać elementów w [Analytics](app-insights-analytics.md).</span><span class="sxs-lookup"><span data-stu-id="ec4a3-122">Using separate resources means that you don't see all the components displayed on a single Application Map; and that you can't query across components in [Analytics](app-insights-analytics.md).</span></span> <span data-ttu-id="ec4a3-123">Należy również skonfigurować oddzielne zasoby.</span><span class="sxs-lookup"><span data-stu-id="ec4a3-123">You also have to set up the separate resources.</span></span>

<span data-ttu-id="ec4a3-124">Z tym ostrzeżenie przyjmiemy w pozostałej części tego dokumentu, który chcesz wysyłać dane z wielu składników do jednego zasobu usługi Application Insights.</span><span class="sxs-lookup"><span data-stu-id="ec4a3-124">With that caveat, we'll assume in the rest of this document that you want to send data from multiple components to one Application Insights resource.</span></span>

## <a name="configure-multi-component-applications"></a><span data-ttu-id="ec4a3-125">Konfigurowanie wielu składnika aplikacji</span><span class="sxs-lookup"><span data-stu-id="ec4a3-125">Configure multi-component applications</span></span>

<span data-ttu-id="ec4a3-126">Aby uzyskać mapy wielu składnika aplikacji, należy na osiągnięcie tych celów:</span><span class="sxs-lookup"><span data-stu-id="ec4a3-126">To get a multi-component application map, you need to achieve these goals:</span></span>

* <span data-ttu-id="ec4a3-127">**Zainstalowanie najnowszej wersji wstępnej** pakiet usługi Application Insights w poszczególnych składników aplikacji.</span><span class="sxs-lookup"><span data-stu-id="ec4a3-127">**Install the latest pre-release** Application Insights package in each component of the application.</span></span> 
* <span data-ttu-id="ec4a3-128">**Udostępnij pojedynczy zasób usługi Application Insights** dla wszystkich składników aplikacji.</span><span class="sxs-lookup"><span data-stu-id="ec4a3-128">**Share a single Application Insights resource** for all the components of your application.</span></span>
* <span data-ttu-id="ec4a3-129">**Włączyć usługi roli aplikacji mapy** w bloku podglądów.</span><span class="sxs-lookup"><span data-stu-id="ec4a3-129">**Enable Multi-role Application Map** in the Previews blade.</span></span>

<span data-ttu-id="ec4a3-130">Skonfiguruj poszczególnych składników aplikacji przy użyciu metody odpowiedniej dla jego typu.</span><span class="sxs-lookup"><span data-stu-id="ec4a3-130">Configure each component of your application using the appropriate method for its type.</span></span> <span data-ttu-id="ec4a3-131">([ASP.NET](app-insights-asp-net.md), [Java](app-insights-java-get-started.md), [Node.js](app-insights-nodejs.md), [JavaScript](app-insights-javascript.md).)</span><span class="sxs-lookup"><span data-stu-id="ec4a3-131">([ASP.NET](app-insights-asp-net.md), [Java](app-insights-java-get-started.md), [Node.js](app-insights-nodejs.md), [JavaScript](app-insights-javascript.md).)</span></span>

### <a name="1-install-the-latest-pre-release-package"></a><span data-ttu-id="ec4a3-132">1. Zainstaluj najnowszy pakiet wersji wstępnej</span><span class="sxs-lookup"><span data-stu-id="ec4a3-132">1. Install the latest pre-release package</span></span>

<span data-ttu-id="ec4a3-133">Zaktualizuj lub zainstalować te pakiety aplikację Insights do projektu dla każdego składnika serwera.</span><span class="sxs-lookup"><span data-stu-id="ec4a3-133">Update or install the Appication Insights packages in the project for each server component.</span></span> <span data-ttu-id="ec4a3-134">Jeśli używasz programu Visual Studio:</span><span class="sxs-lookup"><span data-stu-id="ec4a3-134">If you're using Visual Studio:</span></span>

1. <span data-ttu-id="ec4a3-135">Kliknij prawym przyciskiem myszy projekt i wybierz **Zarządzaj pakietami NuGet**.</span><span class="sxs-lookup"><span data-stu-id="ec4a3-135">Right-click a project and select **Manage NuGet Packages**.</span></span> 
2. <span data-ttu-id="ec4a3-136">Wybierz **Uwzględnij wersję wstępną**.</span><span class="sxs-lookup"><span data-stu-id="ec4a3-136">Select **Include prerelease**.</span></span>
3. <span data-ttu-id="ec4a3-137">Jeśli usługi Application Insights pakiety są widoczne w aktualizacji, zaznacz je.</span><span class="sxs-lookup"><span data-stu-id="ec4a3-137">If Application Insights packages appear in Updates, select them.</span></span> 

    <span data-ttu-id="ec4a3-138">W przeciwnym razie przeglądania i instalowania odpowiedniego pakietu:</span><span class="sxs-lookup"><span data-stu-id="ec4a3-138">Otherwise, browse for and install the appropriate package:</span></span>
    
    * <span data-ttu-id="ec4a3-139">Microsoft.ApplicationInsights.WindowsServer</span><span class="sxs-lookup"><span data-stu-id="ec4a3-139">Microsoft.ApplicationInsights.WindowsServer</span></span>
    * <span data-ttu-id="ec4a3-140">Microsoft.ApplicationInsights.ServiceFabric - składników uruchomiony jako gość plików wykonywalnych i kontenery Docker uruchamiania aplikacji w sieci szkieletowej usług</span><span class="sxs-lookup"><span data-stu-id="ec4a3-140">Microsoft.ApplicationInsights.ServiceFabric - for components running as guest executables and Docker containers running a in Service Fabric application</span></span>
    * <span data-ttu-id="ec4a3-141">Microsoft.ApplicationInsights.ServiceFabric.Native - niezawodnych usług w aplikacjach ServiceFabric</span><span class="sxs-lookup"><span data-stu-id="ec4a3-141">Microsoft.ApplicationInsights.ServiceFabric.Native - for reliable services in ServiceFabric applications</span></span>
    * <span data-ttu-id="ec4a3-142">Microsoft.ApplicationInsights.Kubernetes składników działających w Docker na Kubernetes</span><span class="sxs-lookup"><span data-stu-id="ec4a3-142">Microsoft.ApplicationInsights.Kubernetes for components running in Docker on Kubernetes</span></span>

### <a name="2-share-a-single-application-insights-resource"></a><span data-ttu-id="ec4a3-143">2. Udostępnij pojedynczy zasób usługi Application Insights</span><span class="sxs-lookup"><span data-stu-id="ec4a3-143">2. Share a single Application Insights resource</span></span>

* <span data-ttu-id="ec4a3-144">W programie Visual Studio, kliknij prawym przyciskiem myszy projekt i wybierz **Konfiguruj usługę Application Insights**, lub **usługi Application Insights > Konfiguruj**.</span><span class="sxs-lookup"><span data-stu-id="ec4a3-144">In Visual Studio, right-click a project and select **Configure Application Insights**, or **Application Insights > Configure**.</span></span> <span data-ttu-id="ec4a3-145">Dla pierwszego projektu Kreator można utworzyć zasobu usługi Application Insights.</span><span class="sxs-lookup"><span data-stu-id="ec4a3-145">For the first project, use the wizard to create an Application Insights resource.</span></span> <span data-ttu-id="ec4a3-146">W przypadku kolejnych projektów wybrać tego samego zasobu.</span><span class="sxs-lookup"><span data-stu-id="ec4a3-146">For subsequent projects, select the same resource.</span></span>
* <span data-ttu-id="ec4a3-147">Jeśli nie ma żadnych menu usługi Application Insights, skonfigurować ręcznie:</span><span class="sxs-lookup"><span data-stu-id="ec4a3-147">If there is no Application Insights menu, configure manually:</span></span>

   1. <span data-ttu-id="ec4a3-148">W [portalu Azure](https://portal,azure.com), otwórz zasobu usługi Application Insights już utworzone dla innego składnika.</span><span class="sxs-lookup"><span data-stu-id="ec4a3-148">In [Azure portal](https://portal,azure.com), open the Application Insights resource you already created for another component.</span></span>
   2. <span data-ttu-id="ec4a3-149">W bloku Przegląd, Otwórz listę rozwijaną Essentials kartę i skopiuj **klucza instrumentacji.**</span><span class="sxs-lookup"><span data-stu-id="ec4a3-149">In the Overview blade, open the Essentials drop-down tab, and copy the **Instrumentation Key.**</span></span>
   3. <span data-ttu-id="ec4a3-150">W projekcie Otwórz ApplicationInsights.config i Wstaw:`<InstrumentationKey>your copied key</InstrumentationKey>`</span><span class="sxs-lookup"><span data-stu-id="ec4a3-150">In your project, open ApplicationInsights.config and insert: `<InstrumentationKey>your copied key</InstrumentationKey>`</span></span>

![Skopiuj klucz Instrumentacji do pliku .config](./media/app-insights-monitor-multi-role-apps/copy-instrumentation-key.png)


### <a name="3-enable-multi-role-application-map"></a><span data-ttu-id="ec4a3-152">3. Włącz mapowanie wielu roli w aplikacji</span><span class="sxs-lookup"><span data-stu-id="ec4a3-152">3. Enable multi-role Application Map</span></span>

<span data-ttu-id="ec4a3-153">Otwórz zasobów aplikacji w portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="ec4a3-153">In the Azure portal, open the resource for your application.</span></span> <span data-ttu-id="ec4a3-154">W bloku podglądy włączyć *Mapa aplikacji usługi roli*.</span><span class="sxs-lookup"><span data-stu-id="ec4a3-154">In the Previews blade, enable *Multi-role Application Map*.</span></span>

### <a name="4-enable-docker-metrics-optional"></a><span data-ttu-id="ec4a3-155">4. Włączyć metryki Docker (opcjonalnie)</span><span class="sxs-lookup"><span data-stu-id="ec4a3-155">4. Enable Docker metrics (Optional)</span></span> 

<span data-ttu-id="ec4a3-156">Jeśli składnik jest uruchomiony w Docker hostowanych na maszynie Wirtualnej Windows Azure, można zbierać dodatkowe metryki z kontenera.</span><span class="sxs-lookup"><span data-stu-id="ec4a3-156">If a component runs in a Docker hosted on an Azure Windows VM, you can collect additional metrics from the container.</span></span> <span data-ttu-id="ec4a3-157">Wstawianie w Twojej [diagnostyki Azure](../monitoring-and-diagnostics/azure-diagnostics.md) pliku konfiguracji:</span><span class="sxs-lookup"><span data-stu-id="ec4a3-157">Insert this in your [Azure diagnostics](../monitoring-and-diagnostics/azure-diagnostics.md) configuration file:</span></span>

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

## <a name="use-cloudrolename-to-separate-components"></a><span data-ttu-id="ec4a3-158">Użyj cloud_RoleName do oddzielania składników</span><span class="sxs-lookup"><span data-stu-id="ec4a3-158">Use cloud_RoleName to separate components</span></span>

<span data-ttu-id="ec4a3-159">`cloud_RoleName` Wszystkie dane telemetryczne zostanie dołączona właściwość.</span><span class="sxs-lookup"><span data-stu-id="ec4a3-159">The `cloud_RoleName` property is attached to all telemetry.</span></span> <span data-ttu-id="ec4a3-160">Identyfikuje składnik - roli lub usługi -, który pochodzi telemetrii.</span><span class="sxs-lookup"><span data-stu-id="ec4a3-160">It identifies the component - the role or service - that originates the telemetry.</span></span> <span data-ttu-id="ec4a3-161">(Go nie jest taka sama jak cloud_RoleInstance, która oddziela identyczne ról, które są uruchomione jednocześnie na wielu procesy serwera lub maszyny.)</span><span class="sxs-lookup"><span data-stu-id="ec4a3-161">(It is not the same as cloud_RoleInstance, which separates identical roles that are running in parallel on multiple server processes or machines.)</span></span>

<span data-ttu-id="ec4a3-162">W portalu możesz filtrować i segment telemetrii za pomocą tej właściwości.</span><span class="sxs-lookup"><span data-stu-id="ec4a3-162">In the portal, you can filter or segment your telemetry using this property.</span></span> <span data-ttu-id="ec4a3-163">W tym przykładzie bloku błędów jest filtrowana w celu wyświetlania tylko informacje z usługi frontonu sieci web, filtrowanie błędów z zaplecza interfejsu API CRM:</span><span class="sxs-lookup"><span data-stu-id="ec4a3-163">In this example, the Failures blade is filtered to show just information from the front-end web service, filtering out failures from the CRM API backend:</span></span>

![Metryki wykresu segmentowanych przez nazwę roli chmury](./media/app-insights-monitor-multi-role-apps/cloud-role-name.png)

## <a name="trace-operations-between-components"></a><span data-ttu-id="ec4a3-165">Operacje śledzenia między składnikami</span><span class="sxs-lookup"><span data-stu-id="ec4a3-165">Trace operations between components</span></span>

<span data-ttu-id="ec4a3-166">Z jednego składnika można śledzić na inny wywołań podczas przetwarzania indywidualnych operacji.</span><span class="sxs-lookup"><span data-stu-id="ec4a3-166">You can trace from one component to another, the calls made while processing an individual operation.</span></span>


![Pokaż dane telemetryczne dla operacji](./media/app-insights-monitor-multi-role-apps/show-telemetry-for-operation.png)

<span data-ttu-id="ec4a3-168">Kliknij, aby listę skorelowane dane telemetryczne dla tej operacji na serwerze frontonu sieci web i zaplecza interfejsu API:</span><span class="sxs-lookup"><span data-stu-id="ec4a3-168">Click through to a correlated list of telemetry for this operation across the front-end web server and the back-end API:</span></span>

![Wyszukaj między składnikami](./media/app-insights-monitor-multi-role-apps/search-across-components.png)


## <a name="next-steps"></a><span data-ttu-id="ec4a3-170">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="ec4a3-170">Next steps</span></span>

* [<span data-ttu-id="ec4a3-171">Oddzielne dane telemetryczne z programowanie, testowego i produkcyjnego</span><span class="sxs-lookup"><span data-stu-id="ec4a3-171">Separate telemetry from Development, Test, and Production</span></span>](app-insights-separate-resources.md)
