---
title: "Omówienie narzędzia Monitor aaaAzure | Dokumentacja firmy Microsoft"
description: "Azure Monitor zbiera statystyki dla alertów, elementów webhook, skalowania automatycznego i automatyzacji. Artykuł listy również inne opcje monitorowania firmy Microsoft."
author: rboucher
manager: carmonm
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: 
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/12/2017
ms.author: robb
ms.openlocfilehash: ffa304e7b158f0fceb7f60ab88fab291976aa0e0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="overview-of-azure-monitor"></a><span data-ttu-id="7b23f-104">Omówienie usługi Azure monitora</span><span class="sxs-lookup"><span data-stu-id="7b23f-104">Overview of Azure Monitor</span></span>
<span data-ttu-id="7b23f-105">Ten artykuł zawiera omówienie hello Azure monitorowania usługi platformy Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="7b23f-105">This article provides an overview of hello Azure Monitor service in Microsoft Azure.</span></span> <span data-ttu-id="7b23f-106">Zawarto informacje, co Azure Monitor i zawiera wskaźniki tooadditional informacje na temat toouse Azure Monitor.</span><span class="sxs-lookup"><span data-stu-id="7b23f-106">It discusses what Azure Monitor does and provides pointers tooadditional information on how toouse Azure Monitor.</span></span>  <span data-ttu-id="7b23f-107">Jeśli wolisz wprowadzenie wideo, zobacz dalej łącza kroki na powitania dolnej części tego artykułu.</span><span class="sxs-lookup"><span data-stu-id="7b23f-107">If you prefer a video introduction, see Next steps links at hello bottom of this article.</span></span> 

## <a name="why-monitor-your-application-or-system"></a><span data-ttu-id="7b23f-108">Dlaczego monitorowania aplikacji lub systemu</span><span class="sxs-lookup"><span data-stu-id="7b23f-108">Why monitor your application or system</span></span>
<span data-ttu-id="7b23f-109">Aplikacje w chmurze są złożonych z wielu części ruchu.</span><span class="sxs-lookup"><span data-stu-id="7b23f-109">Cloud applications are complex with many moving parts.</span></span> <span data-ttu-id="7b23f-110">Monitorowania udostępnia tooensure danych, która aplikacja pozostaje w górę i uruchomiona w dobrej kondycji.</span><span class="sxs-lookup"><span data-stu-id="7b23f-110">Monitoring provides data tooensure that your application stays up and running in a healthy state.</span></span> <span data-ttu-id="7b23f-111">Pomaga również należy toostave wyłączone potencjalne problemy lub Rozwiązywanie problemów z przeszłości te.</span><span class="sxs-lookup"><span data-stu-id="7b23f-111">It also helps you toostave off potential problems or troubleshoot past ones.</span></span> <span data-ttu-id="7b23f-112">Ponadto można użyć monitorowania danych toogain szczegółowych informacji o aplikacji.</span><span class="sxs-lookup"><span data-stu-id="7b23f-112">In addition, you can use monitoring data toogain deep insights about your application.</span></span> <span data-ttu-id="7b23f-113">Wiedzy może pomóc tooimprove wydajność aplikacji lub utrzymania lub automatyzować czynności, które w przeciwnym razie wymagają ręcznej interwencji.</span><span class="sxs-lookup"><span data-stu-id="7b23f-113">That knowledge can help you tooimprove application performance or maintainability, or automate actions that would otherwise require manual intervention.</span></span>


## <a name="azure-monitor-and-microsofts-other-monitoring-products"></a><span data-ttu-id="7b23f-114">Azure Monitor a firmą Microsoft przez innych produktów monitorowania</span><span class="sxs-lookup"><span data-stu-id="7b23f-114">Azure Monitor and Microsoft's other monitoring products</span></span>
<span data-ttu-id="7b23f-115">Azure Monitor udostępnia na podstawowym poziomie infrastruktury metryki i dzienniki dla większości usług platformy Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="7b23f-115">Azure Monitor provides base level infrastructure metrics and logs for most services in Microsoft Azure.</span></span> <span data-ttu-id="7b23f-116">Usługami Azure, których nie należy jeszcze umieszczać swoje dane do monitora Azure umieści ją w tym miejscu w hello przyszłych.</span><span class="sxs-lookup"><span data-stu-id="7b23f-116">Azure services that do not yet put their data into Azure Monitor will put it there in hello future.</span></span>

<span data-ttu-id="7b23f-117">Microsoft jest dostarczany dodatkowe produkty i usługi, które zapewniają dodatkowe możliwości monitorowania dla deweloperów, metodyki DevOps lub Ops IT, który ma także w przypadku instalacji lokalnych.</span><span class="sxs-lookup"><span data-stu-id="7b23f-117">Microsoft ships additional products and services that provide additional monitoring capabilities for developers, DevOps, or IT Ops that also have on-premises installations.</span></span> <span data-ttu-id="7b23f-118">Omówienie i zrozumienia, jak te różne produkty i usługi współpracują ze sobą, zobacz [monitorowania na platformie Microsoft Azure](monitoring-overview.md).</span><span class="sxs-lookup"><span data-stu-id="7b23f-118">For an overview and understanding of how these different products and services work together, see [Monitoring in Microsoft Azure](monitoring-overview.md).</span></span>

## <a name="monitoring-sources---compute"></a><span data-ttu-id="7b23f-119">Monitorowanie źródeł - obliczeń</span><span class="sxs-lookup"><span data-stu-id="7b23f-119">Monitoring Sources - Compute</span></span>

![Model do monitorowania i diagnostyki dla zasobów obliczeniowych z systemem innym niż](./media/monitoring-overview-azure-monitor/Monitoring_Azure_Resources-compute_v6.png)

<span data-ttu-id="7b23f-121">usługi obliczeniowe Hello obejmują:</span><span class="sxs-lookup"><span data-stu-id="7b23f-121">hello Compute services include</span></span> 
- <span data-ttu-id="7b23f-122">Cloud Services</span><span class="sxs-lookup"><span data-stu-id="7b23f-122">Cloud Services</span></span> 
- <span data-ttu-id="7b23f-123">Maszyny wirtualne</span><span class="sxs-lookup"><span data-stu-id="7b23f-123">Virtual Machines</span></span> 
- <span data-ttu-id="7b23f-124">Zestawy skalowania maszyny wirtualnej</span><span class="sxs-lookup"><span data-stu-id="7b23f-124">Virtual Machine scale sets</span></span> 
- <span data-ttu-id="7b23f-125">Service Fabric</span><span class="sxs-lookup"><span data-stu-id="7b23f-125">Service Fabric</span></span>

### <a name="application---diagnostics-logs-application-logs-and-metrics"></a><span data-ttu-id="7b23f-126">Aplikacja — dzienniki diagnostyczne, dzienniki aplikacji i metryki</span><span class="sxs-lookup"><span data-stu-id="7b23f-126">Application - Diagnostics Logs, Application Logs, and Metrics</span></span>
<span data-ttu-id="7b23f-127">Aplikacje mogą działać na powitania systemu operacyjnego gościa w hello obliczeń modelu.</span><span class="sxs-lookup"><span data-stu-id="7b23f-127">Applications can run on top of hello Guest OS in hello compute model.</span></span> <span data-ttu-id="7b23f-128">Wysyłają własny zestaw dzienniki i metryki.</span><span class="sxs-lookup"><span data-stu-id="7b23f-128">They emit their own set of logs and metrics.</span></span> <span data-ttu-id="7b23f-129">Azure Monitor zależy od hello Azure diagnostics rozszerzenia (Windows lub Linux) toocollect większość dzienniki i metryki na poziomie aplikacji.</span><span class="sxs-lookup"><span data-stu-id="7b23f-129">Azure Monitor relies on hello Azure diagnostics extension (Windows or Linux) toocollect most application level metrics and logs.</span></span> <span data-ttu-id="7b23f-130">typy Hello</span><span class="sxs-lookup"><span data-stu-id="7b23f-130">hello types include</span></span>

* <span data-ttu-id="7b23f-131">Liczniki wydajności</span><span class="sxs-lookup"><span data-stu-id="7b23f-131">Performance counters</span></span>
* <span data-ttu-id="7b23f-132">Dzienniki aplikacji</span><span class="sxs-lookup"><span data-stu-id="7b23f-132">Application Logs</span></span>
* <span data-ttu-id="7b23f-133">Dzienniki zdarzeń systemu Windows</span><span class="sxs-lookup"><span data-stu-id="7b23f-133">Windows Event Logs</span></span>
* <span data-ttu-id="7b23f-134">Źródło zdarzenia platformy .NET</span><span class="sxs-lookup"><span data-stu-id="7b23f-134">.NET Event Source</span></span>
* <span data-ttu-id="7b23f-135">Dzienniki programu IIS</span><span class="sxs-lookup"><span data-stu-id="7b23f-135">IIS Logs</span></span>
* <span data-ttu-id="7b23f-136">Manifest na podstawie ETW</span><span class="sxs-lookup"><span data-stu-id="7b23f-136">Manifest based ETW</span></span>
* <span data-ttu-id="7b23f-137">Zrzuty awaryjne</span><span class="sxs-lookup"><span data-stu-id="7b23f-137">Crash Dumps</span></span>
* <span data-ttu-id="7b23f-138">Dzienniki błędów klienta</span><span class="sxs-lookup"><span data-stu-id="7b23f-138">Customer Error Logs</span></span>

<span data-ttu-id="7b23f-139">Bez rozszerzenia diagnostyki hello dostępne są tylko kilka metryk, takich jak użycie procesora CPU.</span><span class="sxs-lookup"><span data-stu-id="7b23f-139">Without hello diagnostics extension, only a few metrics like CPU usage are available.</span></span> 

### <a name="host-and-guest-vm-metrics"></a><span data-ttu-id="7b23f-140">Metryki hosta i gościa maszyny Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="7b23f-140">Host and Guest VM metrics</span></span>
<span data-ttu-id="7b23f-141">Witaj zasoby obliczeniowe wymienione wcześniej mieć dedykowanego hosta maszyny Wirtualnej i ich interakcji z system operacyjny gościa.</span><span class="sxs-lookup"><span data-stu-id="7b23f-141">hello previously listed compute resources have a dedicated host VM and guest OS they interact with.</span></span> <span data-ttu-id="7b23f-142">Hello hosta maszyny Wirtualnej i system operacyjny gościa są równoważne hello głównego maszyny Wirtualnej, jak i gościa maszyny Wirtualnej w modelu funkcji hypervisor Hyper-V hello.</span><span class="sxs-lookup"><span data-stu-id="7b23f-142">hello host VM and guest OS are hello equivalent of root VM and guest VM in hello Hyper-V hypervisor model.</span></span> <span data-ttu-id="7b23f-143">Można zbierać metryki na serwerze.</span><span class="sxs-lookup"><span data-stu-id="7b23f-143">You can collect metrics on both.</span></span> <span data-ttu-id="7b23f-144">Może również zbierać dzienniki diagnostyczne na system operacyjny gościa hello.</span><span class="sxs-lookup"><span data-stu-id="7b23f-144">You can also collect diagnostics logs on hello guest OS.</span></span>   

### <a name="activity-log"></a><span data-ttu-id="7b23f-145">Dziennik aktywności</span><span class="sxs-lookup"><span data-stu-id="7b23f-145">Activity Log</span></span>
<span data-ttu-id="7b23f-146">Możesz wyszukać hello dziennik aktywności (wcześniej nazywane Operational lub dzienniki inspekcji) informacji o zasobie widziany przez hello infrastruktury platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="7b23f-146">You can search hello Activity Log (previously called Operational or Audit Logs) for information about your resource as seen by hello Azure infrastructure.</span></span> <span data-ttu-id="7b23f-147">Witaj dziennik zawiera informacje, takie jak czas, kiedy zasoby są tworzone lub zniszczony.</span><span class="sxs-lookup"><span data-stu-id="7b23f-147">hello log contains information such as times when resources are created or destroyed.</span></span>  <span data-ttu-id="7b23f-148">Aby uzyskać więcej informacji, zobacz [omówienie dziennik aktywności](monitoring-overview-activity-logs.md).</span><span class="sxs-lookup"><span data-stu-id="7b23f-148">For more information, see [Overview of Activity Log](monitoring-overview-activity-logs.md).</span></span> 

## <a name="monitoring-sources---everything-else"></a><span data-ttu-id="7b23f-149">Monitorowanie źródeł - wszystkie inne</span><span class="sxs-lookup"><span data-stu-id="7b23f-149">Monitoring Sources - everything else</span></span>

![Model do monitorowania i diagnostyki dla zasobów obliczeniowych](./media/monitoring-overview-azure-monitor/Monitoring_Azure_Resources-non-compute_v6.png)


### <a name="resource---metrics-and-diagnostics-logs"></a><span data-ttu-id="7b23f-151">Zasobu, metryki i dzienniki diagnostyczne</span><span class="sxs-lookup"><span data-stu-id="7b23f-151">Resource - Metrics and Diagnostics Logs</span></span>
<span data-ttu-id="7b23f-152">Do zebrania metryki i informacji diagnostycznych dzienników różnić w zależności od typu zasobu hello.</span><span class="sxs-lookup"><span data-stu-id="7b23f-152">Collectable metrics and diagnostics logs vary based on hello resource type.</span></span> <span data-ttu-id="7b23f-153">Na przykład aplikacje sieci Web zawiera dane statystyczne dotyczące hello We/Wy dysku i procesora CPU w procentach.</span><span class="sxs-lookup"><span data-stu-id="7b23f-153">For example, Web Apps provides statistics on hello Disk IO and Percent CPU.</span></span> <span data-ttu-id="7b23f-154">Te metryki nie istnieje dla kolejki usługi Service Bus, która przekazuje metryk, takich jak kolejki przepływności rozmiaru i komunikatów.</span><span class="sxs-lookup"><span data-stu-id="7b23f-154">Those metrics don't exist for a Service Bus queue, which instead provides metrics like queue size and message throughput.</span></span> <span data-ttu-id="7b23f-155">Lista do zebrania metryki dla każdego zasobu jest dostępna na [obsługiwane metryki](monitoring-supported-metrics.md).</span><span class="sxs-lookup"><span data-stu-id="7b23f-155">A list of collectable metrics for each resource is available at [supported metrics](monitoring-supported-metrics.md).</span></span> 

### <a name="host-and-guest-vm-metrics"></a><span data-ttu-id="7b23f-156">Metryki hosta i gościa maszyny Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="7b23f-156">Host and Guest VM metrics</span></span>
<span data-ttu-id="7b23f-157">Nie jest zawsze mapowanie 1:1 od zasobu do określonego hosta lub maszyny Wirtualnej gościa, metryki nie są dostępne.</span><span class="sxs-lookup"><span data-stu-id="7b23f-157">There is not necessarily a 1:1 mapping between your resource and a particular Host or Guest VM so metrics are not available.</span></span>

### <a name="activity-log"></a><span data-ttu-id="7b23f-158">Dziennik aktywności</span><span class="sxs-lookup"><span data-stu-id="7b23f-158">Activity Log</span></span>
<span data-ttu-id="7b23f-159">Dziennik aktywności Hello jest hello taki sam jak dla zasobów obliczeniowych.</span><span class="sxs-lookup"><span data-stu-id="7b23f-159">hello activity log is hello same as for compute resources.</span></span>  

## <a name="uses-for-monitoring-data"></a><span data-ttu-id="7b23f-160">Używane do monitorowania danych</span><span class="sxs-lookup"><span data-stu-id="7b23f-160">Uses for Monitoring Data</span></span>
<span data-ttu-id="7b23f-161">Po zebraniu danych można wykonać hello zgodnie z nią w monitorze Azure</span><span class="sxs-lookup"><span data-stu-id="7b23f-161">Once you collect your data, you can do hello following with it in Azure Monitor</span></span>

### <a name="route"></a><span data-ttu-id="7b23f-162">Trasa</span><span class="sxs-lookup"><span data-stu-id="7b23f-162">Route</span></span>
<span data-ttu-id="7b23f-163">Można przesłać strumieniowo monitorowania lokalizacje tooother danych w czasie rzeczywistym.</span><span class="sxs-lookup"><span data-stu-id="7b23f-163">You can stream monitoring data tooother locations in real time.</span></span>

<span data-ttu-id="7b23f-164">Przykłady:</span><span class="sxs-lookup"><span data-stu-id="7b23f-164">Examples include:</span></span>

- <span data-ttu-id="7b23f-165">Wyślij tooApplication Insights, dzięki czemu można używać jej bardziej zaawansowane funkcje narzędzi wizualizacji i analizy.</span><span class="sxs-lookup"><span data-stu-id="7b23f-165">Send tooApplication Insights so you can use its richer visualization and analysis tools.</span></span>
- <span data-ttu-id="7b23f-166">Wyślij tooEvent koncentratory, można kierować toothird innych narzędzi.</span><span class="sxs-lookup"><span data-stu-id="7b23f-166">Send tooEvent Hubs so you can route toothird-party tools.</span></span> 

### <a name="store-and-archive"></a><span data-ttu-id="7b23f-167">Magazyn i archiwum</span><span class="sxs-lookup"><span data-stu-id="7b23f-167">Store and Archive</span></span>
<span data-ttu-id="7b23f-168">Niektóre dane monitorowania jest już przechowywane i dostępne w monitorze Azure dla określonej ilości czasu.</span><span class="sxs-lookup"><span data-stu-id="7b23f-168">Some monitoring data is already stored and available in Azure Monitor for a set amount of time.</span></span> 
- <span data-ttu-id="7b23f-169">Metryki są przechowywane przez 30 dni.</span><span class="sxs-lookup"><span data-stu-id="7b23f-169">Metrics are stored for 30 days.</span></span> 
- <span data-ttu-id="7b23f-170">Wpisy dziennika aktywności są przechowywane przez 90 dni.</span><span class="sxs-lookup"><span data-stu-id="7b23f-170">Activity log entries are stored for 90 days.</span></span> 
- <span data-ttu-id="7b23f-171">Dzienniki diagnostyczne nie są przechowywane w ogóle.</span><span class="sxs-lookup"><span data-stu-id="7b23f-171">Diagnostics logs are not stored at all.</span></span> 

<span data-ttu-id="7b23f-172">Jeśli chcesz toostore dane dłuższe niż hello okresów wymienionych powyżej, można użyć usługi Azure storage.</span><span class="sxs-lookup"><span data-stu-id="7b23f-172">If you want toostore data longer than hello time periods listed above, you can use an Azure storage.</span></span> <span data-ttu-id="7b23f-173">Monitorowanie danych jest przechowywana w na podstawie zasad przechowywania, które można ustawić konto magazynu.</span><span class="sxs-lookup"><span data-stu-id="7b23f-173">Monitoring data is kept in your storage acccount based on a retention policy you set.</span></span> <span data-ttu-id="7b23f-174">Masz toopay dla powitalne miejsca hello danych zajmuje w magazynie Azure.</span><span class="sxs-lookup"><span data-stu-id="7b23f-174">You do have toopay for hello space hello data takes up in Azure storage.</span></span> 

<span data-ttu-id="7b23f-175">Kilka sposobów toouse te dane:</span><span class="sxs-lookup"><span data-stu-id="7b23f-175">A few ways toouse this data:</span></span>

- <span data-ttu-id="7b23f-176">Po zapisaniu, może mieć inne narzędzia wewnątrz lub na zewnątrz Azure Przeczytaj je i go przetworzyć.</span><span class="sxs-lookup"><span data-stu-id="7b23f-176">Once written, you can have other tools within or outside of Azure read it and process it.</span></span>
- <span data-ttu-id="7b23f-177">Pobierz dane hello lokalnie archiwum lokalnego lub zmienić z zasadami przechowywania danych tookeep chmury hello przez dłuższy czas.</span><span class="sxs-lookup"><span data-stu-id="7b23f-177">You download hello data locally for a local archive or change your retention policy in hello cloud tookeep data for extended periods of time.</span></span>  
- <span data-ttu-id="7b23f-178">Możesz pozostawić hello danych w magazynie Azure przez czas nieograniczony na potrzeby archiwizacji.</span><span class="sxs-lookup"><span data-stu-id="7b23f-178">You leave hello data in Azure storage indefinitely for archive purposes.</span></span> 

### <a name="query"></a><span data-ttu-id="7b23f-179">Zapytanie</span><span class="sxs-lookup"><span data-stu-id="7b23f-179">Query</span></span>
<span data-ttu-id="7b23f-180">Można użyć hello Azure Monitor REST API, międzyplatformowego interfejsu wiersza polecenia (CLI) poleceń, w przypadku poleceń cmdlet programu PowerShell lub tooaccess zestawu .NET SDK hello hello danych w systemie hello lub magazynu Azure</span><span class="sxs-lookup"><span data-stu-id="7b23f-180">You can use hello Azure Monitor REST API, cross platform Command-Line Interface (CLI) commands, PowerShell cmdlets, or hello .NET SDK tooaccess hello data in hello system or Azure storage</span></span>

<span data-ttu-id="7b23f-181">Przykłady:</span><span class="sxs-lookup"><span data-stu-id="7b23f-181">Examples include:</span></span>

* <span data-ttu-id="7b23f-182">Pobieranie danych dla niestandardowych aplikacji monitorowania zapisane</span><span class="sxs-lookup"><span data-stu-id="7b23f-182">Getting data for a custom monitoring application you have written</span></span>
* <span data-ttu-id="7b23f-183">Tworzenie niestandardowych kwerend i wysyłanie tej aplikacji innych firm tooa danych.</span><span class="sxs-lookup"><span data-stu-id="7b23f-183">Creating custom queries and sending that data tooa third-party application.</span></span>

### <a name="visualize"></a><span data-ttu-id="7b23f-184">Wizualizowanie</span><span class="sxs-lookup"><span data-stu-id="7b23f-184">Visualize</span></span>
<span data-ttu-id="7b23f-185">Wizualizacja danych monitorowania w grafiki i wykresy ułatwia trendów szybsze niż wyszukiwanie za pomocą hello samych danych.</span><span class="sxs-lookup"><span data-stu-id="7b23f-185">Visualizing your monitoring data in graphics and charts helps you find trends quicker than looking through hello data itself.</span></span>  

<span data-ttu-id="7b23f-186">Kilka metod wizualizacji obejmują:</span><span class="sxs-lookup"><span data-stu-id="7b23f-186">A few visualization methods include:</span></span>

* <span data-ttu-id="7b23f-187">Użyj hello portalu Azure</span><span class="sxs-lookup"><span data-stu-id="7b23f-187">Use hello Azure portal</span></span>
* <span data-ttu-id="7b23f-188">TooAzure danych trasy usługi Application Insights</span><span class="sxs-lookup"><span data-stu-id="7b23f-188">Route data tooAzure Application Insights</span></span>
* <span data-ttu-id="7b23f-189">Trasy tooMicrosoft danych usługi Power BI</span><span class="sxs-lookup"><span data-stu-id="7b23f-189">Route data tooMicrosoft PowerBI</span></span>
* <span data-ttu-id="7b23f-190">Trasy hello danych tooa wizualizacji innych firm narzędzie przy użyciu albo przesyłanie strumieniowe na żywo lub przez narzędzie hello odczytywać archiwum w magazynie Azure</span><span class="sxs-lookup"><span data-stu-id="7b23f-190">Route hello data tooa third-party visualization tool using either live streaming or by having hello tool read from an archive in Azure storage</span></span>


### <a name="automate"></a><span data-ttu-id="7b23f-191">Automatyzacja</span><span class="sxs-lookup"><span data-stu-id="7b23f-191">Automate</span></span>
<span data-ttu-id="7b23f-192">Możesz użyć alertów monitorowania tootrigger danych lub nawet cały proces.</span><span class="sxs-lookup"><span data-stu-id="7b23f-192">You can use monitoring data tootrigger alerts or even whole processes.</span></span> <span data-ttu-id="7b23f-193">Przykłady:</span><span class="sxs-lookup"><span data-stu-id="7b23f-193">Examples include:</span></span>

* <span data-ttu-id="7b23f-194">Użyj wystąpienia obliczeniowe tooautoscale danych w górę lub w dół oparte na obciążenia aplikacji.</span><span class="sxs-lookup"><span data-stu-id="7b23f-194">Use data tooautoscale compute instances up or down based on application load.</span></span>
* <span data-ttu-id="7b23f-195">Wysyłaj wiadomości e-mail, gdy metryki przecina wstępnie określoną wartość progową.</span><span class="sxs-lookup"><span data-stu-id="7b23f-195">Send emails when a metric crosses a predetermined threshold.</span></span>
* <span data-ttu-id="7b23f-196">Wywołanie tooexecute (webhook) adres URL sieci web w systemie poza platformą Azure</span><span class="sxs-lookup"><span data-stu-id="7b23f-196">Call a web URL (webhook) tooexecute an action in a system outside of Azure</span></span>
* <span data-ttu-id="7b23f-197">Uruchom element runbook w automatyzacji Azure tooperform żadnych różnych zadań</span><span class="sxs-lookup"><span data-stu-id="7b23f-197">Start a runbook in Azure automation tooperform any variety of tasks</span></span>

## <a name="methods-of-accessing-azure-monitor"></a><span data-ttu-id="7b23f-198">Metody dostępu do monitora Azure</span><span class="sxs-lookup"><span data-stu-id="7b23f-198">Methods of accessing Azure Monitor</span></span>
<span data-ttu-id="7b23f-199">Ogólnie rzecz biorąc można manipulować danych śledzenia, routing i pobierania za pomocą jednej z następujących metod hello.</span><span class="sxs-lookup"><span data-stu-id="7b23f-199">In general, you can manipulate data tracking, routing, and retrieval using one of hello following methods.</span></span> <span data-ttu-id="7b23f-200">Nie wszystkie metody są dostępne dla wszystkich akcji lub typów danych.</span><span class="sxs-lookup"><span data-stu-id="7b23f-200">Not all methods are available for all actions or data types.</span></span>

* [<span data-ttu-id="7b23f-201">Witryna Azure Portal</span><span class="sxs-lookup"><span data-stu-id="7b23f-201">Azure portal</span></span>](https://portal.azure.com)
* [<span data-ttu-id="7b23f-202">PowerShell</span><span class="sxs-lookup"><span data-stu-id="7b23f-202">PowerShell</span></span>](insights-powershell-samples.md)  
* [<span data-ttu-id="7b23f-203">Interfejs wiersza polecenia i platform (CLI)</span><span class="sxs-lookup"><span data-stu-id="7b23f-203">Cross-platform Command Line Interface (CLI)</span></span>](insights-cli-samples.md)
* [<span data-ttu-id="7b23f-204">Interfejs API REST</span><span class="sxs-lookup"><span data-stu-id="7b23f-204">REST API</span></span>](https://docs.microsoft.com/rest/api/monitor/)
* [<span data-ttu-id="7b23f-205">Zestaw SDK platformy .NET</span><span class="sxs-lookup"><span data-stu-id="7b23f-205">.NET SDK</span></span>](http://www.nuget.org/packages/Microsoft.Azure.Management.Monitor)

## <a name="next-steps"></a><span data-ttu-id="7b23f-206">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="7b23f-206">Next steps</span></span>
<span data-ttu-id="7b23f-207">Dowiedz się więcej o</span><span class="sxs-lookup"><span data-stu-id="7b23f-207">Learn more about</span></span>
- <span data-ttu-id="7b23f-208">Przewodnik wideo tylko monitora Azure znajduje się w temacie</span><span class="sxs-lookup"><span data-stu-id="7b23f-208">A video walkthrough of just Azure Monitor is available at</span></span>  
<span data-ttu-id="7b23f-209">[Wprowadzenie do platformy Azure Monitor](https://channel9.msdn.com/Blogs/Azure-Monitoring/Get-Started-with-Azure-Monitor).</span><span class="sxs-lookup"><span data-stu-id="7b23f-209">[Get Started with Azure Monitor](https://channel9.msdn.com/Blogs/Azure-Monitoring/Get-Started-with-Azure-Monitor).</span></span> <span data-ttu-id="7b23f-210">Dodatkowe wideo wyjaśniający scenariusz, w których można użyć Monitora Azure znajduje się w temacie [Eksploruj Microsoft Azure, monitorowania i diagnostyki](https://channel9.msdn.com/events/Ignite/2016/BRK2234) i [Azure Monitor wideo z Ignite 2016](https://myignite.microsoft.com/videos/4977)</span><span class="sxs-lookup"><span data-stu-id="7b23f-210">An additional video explaining a scenario where you can use Azure Monitor is available at [Explore Microsoft Azure monitoring and diagnostics](https://channel9.msdn.com/events/Ignite/2016/BRK2234) and [Azure Monitor in a video from Ignite 2016](https://myignite.microsoft.com/videos/4977)</span></span>
- <span data-ttu-id="7b23f-211">Uruchom za pomocą interfejsu Azure Monitor hello w [wprowadzenie Azure Monitor](monitoring-get-started.md)</span><span class="sxs-lookup"><span data-stu-id="7b23f-211">Run through hello Azure Monitor interface in [Getting Started with Azure Monitor](monitoring-get-started.md)</span></span>
- <span data-ttu-id="7b23f-212">Konfigurowanie hello [rozszerzenia diagnostyki Azure](../azure-diagnostics.md) Jeśli próbujesz toodiagnose problemów w usłudze chmury maszyny wirtualnej maszyny wirtualnej skalowanie zestawów lub aplikacji sieci szkieletowej usług.</span><span class="sxs-lookup"><span data-stu-id="7b23f-212">Set up hello [Azure Diagnostics Extensions](../azure-diagnostics.md) if you are attempting toodiagnose problems in your Cloud Service, Virtual Machine, Virtual machine scale sets, or Service Fabric application.</span></span>
- <span data-ttu-id="7b23f-213">[Usługa Application Insights](https://azure.microsoft.com/documentation/services/application-insights/) Jeśli próbujesz toodiagnostic problemy w aplikacji sieci Web usługi aplikacji.</span><span class="sxs-lookup"><span data-stu-id="7b23f-213">[Application Insights](https://azure.microsoft.com/documentation/services/application-insights/) if you are trying toodiagnostic problems in your App Service Web app.</span></span>
- <span data-ttu-id="7b23f-214">[Rozwiązywanie problemów z magazynem Azure](../storage/common/storage-e2e-troubleshooting.md) przy użyciu magazynu obiektów blob, tabel lub kolejek</span><span class="sxs-lookup"><span data-stu-id="7b23f-214">[Troubleshooting Azure Storage](../storage/common/storage-e2e-troubleshooting.md) when using Storage Blobs, Tables, or Queues</span></span>
- <span data-ttu-id="7b23f-215">[Zaloguj się Analytics](https://azure.microsoft.com/documentation/services/log-analytics/) i hello [Operations Management Suite](https://www.microsoft.com/oms/)</span><span class="sxs-lookup"><span data-stu-id="7b23f-215">[Log Analytics](https://azure.microsoft.com/documentation/services/log-analytics/) and hello [Operations Management Suite](https://www.microsoft.com/oms/)</span></span>
