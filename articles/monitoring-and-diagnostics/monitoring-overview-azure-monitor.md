---
title: "Omówienie narzędzia Monitor systemu Azure | Dokumentacja firmy Microsoft"
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
ms.openlocfilehash: 619a004b9aff99be68988e1f7be3ccad400a8a0e
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
# <a name="overview-of-azure-monitor"></a><span data-ttu-id="34e24-104">Omówienie usługi Azure monitora</span><span class="sxs-lookup"><span data-stu-id="34e24-104">Overview of Azure Monitor</span></span>
<span data-ttu-id="34e24-105">Ten artykuł zawiera omówienie usługi Azure Monitor w Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="34e24-105">This article provides an overview of the Azure Monitor service in Microsoft Azure.</span></span> <span data-ttu-id="34e24-106">Zawarto informacje, co Azure Monitor i zawiera łącza do dodatkowych informacji na temat korzystania z monitora Azure.</span><span class="sxs-lookup"><span data-stu-id="34e24-106">It discusses what Azure Monitor does and provides pointers to additional information on how to use Azure Monitor.</span></span>  <span data-ttu-id="34e24-107">Jeśli wolisz wprowadzenie wideo, zobacz dalej łącza kroki w dolnej części tego artykułu.</span><span class="sxs-lookup"><span data-stu-id="34e24-107">If you prefer a video introduction, see Next steps links at the bottom of this article.</span></span> 

## <a name="why-monitor-your-application-or-system"></a><span data-ttu-id="34e24-108">Dlaczego monitorowania aplikacji lub systemu</span><span class="sxs-lookup"><span data-stu-id="34e24-108">Why monitor your application or system</span></span>
<span data-ttu-id="34e24-109">Aplikacje w chmurze są złożonych z wielu części ruchu.</span><span class="sxs-lookup"><span data-stu-id="34e24-109">Cloud applications are complex with many moving parts.</span></span> <span data-ttu-id="34e24-110">Monitorowanie zawiera danych, aby upewnić się, że aplikacja pozostaje w górę i działa w dobrej kondycji.</span><span class="sxs-lookup"><span data-stu-id="34e24-110">Monitoring provides data to ensure that your application stays up and running in a healthy state.</span></span> <span data-ttu-id="34e24-111">Pomaga również umożliwia stave potencjalne problemy i rozwiązywanie problemów w przeszłości te.</span><span class="sxs-lookup"><span data-stu-id="34e24-111">It also helps you to stave off potential problems or troubleshoot past ones.</span></span> <span data-ttu-id="34e24-112">Ponadto można użyć danych monitorowania w celu uzyskania szczegółowych informacji o aplikacji.</span><span class="sxs-lookup"><span data-stu-id="34e24-112">In addition, you can use monitoring data to gain deep insights about your application.</span></span> <span data-ttu-id="34e24-113">Wiedzy może pomóc zwiększyć wydajność aplikacji lub utrzymania lub automatyzować czynności, które w przeciwnym razie wymagają ręcznej interwencji.</span><span class="sxs-lookup"><span data-stu-id="34e24-113">That knowledge can help you to improve application performance or maintainability, or automate actions that would otherwise require manual intervention.</span></span>


## <a name="azure-monitor-and-microsofts-other-monitoring-products"></a><span data-ttu-id="34e24-114">Azure Monitor a firmą Microsoft przez innych produktów monitorowania</span><span class="sxs-lookup"><span data-stu-id="34e24-114">Azure Monitor and Microsoft's other monitoring products</span></span>
<span data-ttu-id="34e24-115">Azure Monitor udostępnia na podstawowym poziomie infrastruktury metryki i dzienniki dla większości usług platformy Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="34e24-115">Azure Monitor provides base level infrastructure metrics and logs for most services in Microsoft Azure.</span></span> <span data-ttu-id="34e24-116">Usługami Azure, których nie należy jeszcze umieszczać swoje dane do monitora Azure będzie umieszczono go w przyszłości.</span><span class="sxs-lookup"><span data-stu-id="34e24-116">Azure services that do not yet put their data into Azure Monitor will put it there in the future.</span></span>

<span data-ttu-id="34e24-117">Microsoft jest dostarczany dodatkowe produkty i usługi, które zapewniają dodatkowe możliwości monitorowania dla deweloperów, metodyki DevOps lub Ops IT, który ma także w przypadku instalacji lokalnych.</span><span class="sxs-lookup"><span data-stu-id="34e24-117">Microsoft ships additional products and services that provide additional monitoring capabilities for developers, DevOps, or IT Ops that also have on-premises installations.</span></span> <span data-ttu-id="34e24-118">Omówienie i zrozumienia, jak te różne produkty i usługi współpracują ze sobą, zobacz [monitorowania na platformie Microsoft Azure](monitoring-overview.md).</span><span class="sxs-lookup"><span data-stu-id="34e24-118">For an overview and understanding of how these different products and services work together, see [Monitoring in Microsoft Azure](monitoring-overview.md).</span></span>

## <a name="monitoring-sources---compute"></a><span data-ttu-id="34e24-119">Monitorowanie źródeł - obliczeń</span><span class="sxs-lookup"><span data-stu-id="34e24-119">Monitoring Sources - Compute</span></span>

![Model do monitorowania i diagnostyki dla zasobów obliczeniowych z systemem innym niż](./media/monitoring-overview-azure-monitor/Monitoring_Azure_Resources-compute_v6.png)

<span data-ttu-id="34e24-121">Usługi obliczeniowe obejmują:</span><span class="sxs-lookup"><span data-stu-id="34e24-121">The Compute services include</span></span> 
- <span data-ttu-id="34e24-122">Cloud Services</span><span class="sxs-lookup"><span data-stu-id="34e24-122">Cloud Services</span></span> 
- <span data-ttu-id="34e24-123">Maszyny wirtualne</span><span class="sxs-lookup"><span data-stu-id="34e24-123">Virtual Machines</span></span> 
- <span data-ttu-id="34e24-124">Zestawy skalowania maszyny wirtualnej</span><span class="sxs-lookup"><span data-stu-id="34e24-124">Virtual Machine scale sets</span></span> 
- <span data-ttu-id="34e24-125">Service Fabric</span><span class="sxs-lookup"><span data-stu-id="34e24-125">Service Fabric</span></span>

### <a name="application---diagnostics-logs-application-logs-and-metrics"></a><span data-ttu-id="34e24-126">Aplikacja — dzienniki diagnostyczne, dzienniki aplikacji i metryki</span><span class="sxs-lookup"><span data-stu-id="34e24-126">Application - Diagnostics Logs, Application Logs, and Metrics</span></span>
<span data-ttu-id="34e24-127">Aplikacje mogą działać na podstawie systemu operacyjnego gościa w modelu obliczeń.</span><span class="sxs-lookup"><span data-stu-id="34e24-127">Applications can run on top of the Guest OS in the compute model.</span></span> <span data-ttu-id="34e24-128">Wysyłają własny zestaw dzienniki i metryki.</span><span class="sxs-lookup"><span data-stu-id="34e24-128">They emit their own set of logs and metrics.</span></span> <span data-ttu-id="34e24-129">Azure Monitor polega na rozszerzenia diagnostyki Azure (Windows lub Linux) do zbierania większości dzienniki i metryki na poziomie aplikacji.</span><span class="sxs-lookup"><span data-stu-id="34e24-129">Azure Monitor relies on the Azure diagnostics extension (Windows or Linux) to collect most application level metrics and logs.</span></span> <span data-ttu-id="34e24-130">Typy</span><span class="sxs-lookup"><span data-stu-id="34e24-130">The types include</span></span>

* <span data-ttu-id="34e24-131">Liczniki wydajności</span><span class="sxs-lookup"><span data-stu-id="34e24-131">Performance counters</span></span>
* <span data-ttu-id="34e24-132">Dzienniki aplikacji</span><span class="sxs-lookup"><span data-stu-id="34e24-132">Application Logs</span></span>
* <span data-ttu-id="34e24-133">Dzienniki zdarzeń systemu Windows</span><span class="sxs-lookup"><span data-stu-id="34e24-133">Windows Event Logs</span></span>
* <span data-ttu-id="34e24-134">Źródło zdarzenia platformy .NET</span><span class="sxs-lookup"><span data-stu-id="34e24-134">.NET Event Source</span></span>
* <span data-ttu-id="34e24-135">Dzienniki programu IIS</span><span class="sxs-lookup"><span data-stu-id="34e24-135">IIS Logs</span></span>
* <span data-ttu-id="34e24-136">Manifest na podstawie ETW</span><span class="sxs-lookup"><span data-stu-id="34e24-136">Manifest based ETW</span></span>
* <span data-ttu-id="34e24-137">Zrzuty awaryjne</span><span class="sxs-lookup"><span data-stu-id="34e24-137">Crash Dumps</span></span>
* <span data-ttu-id="34e24-138">Dzienniki błędów klienta</span><span class="sxs-lookup"><span data-stu-id="34e24-138">Customer Error Logs</span></span>

<span data-ttu-id="34e24-139">Bez rozszerzenia diagnostyki dostępne są tylko kilka metryk, takich jak użycie procesora CPU.</span><span class="sxs-lookup"><span data-stu-id="34e24-139">Without the diagnostics extension, only a few metrics like CPU usage are available.</span></span> 

### <a name="host-and-guest-vm-metrics"></a><span data-ttu-id="34e24-140">Metryki hosta i gościa maszyny Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="34e24-140">Host and Guest VM metrics</span></span>
<span data-ttu-id="34e24-141">Zasoby obliczeniowe wymienione wcześniej mieć dedykowanego hosta maszyny Wirtualnej i ich interakcji z system operacyjny gościa.</span><span class="sxs-lookup"><span data-stu-id="34e24-141">The previously listed compute resources have a dedicated host VM and guest OS they interact with.</span></span> <span data-ttu-id="34e24-142">Host maszyny Wirtualnej i system operacyjny gościa są równoważne głównych maszyny Wirtualnej i gościa maszyny Wirtualnej w funkcji Hyper-V modelu funkcji hypervisor.</span><span class="sxs-lookup"><span data-stu-id="34e24-142">The host VM and guest OS are the equivalent of root VM and guest VM in the Hyper-V hypervisor model.</span></span> <span data-ttu-id="34e24-143">Można zbierać metryki na serwerze.</span><span class="sxs-lookup"><span data-stu-id="34e24-143">You can collect metrics on both.</span></span> <span data-ttu-id="34e24-144">Może również zbierać dzienniki diagnostyczne na system operacyjny gościa.</span><span class="sxs-lookup"><span data-stu-id="34e24-144">You can also collect diagnostics logs on the guest OS.</span></span>   

### <a name="activity-log"></a><span data-ttu-id="34e24-145">Dziennik aktywności</span><span class="sxs-lookup"><span data-stu-id="34e24-145">Activity Log</span></span>
<span data-ttu-id="34e24-146">Możesz wyszukać dziennik aktywności (wcześniej nazywane Operational lub dzienniki inspekcji) informacji o zasobie widziany przez infrastrukturę platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="34e24-146">You can search the Activity Log (previously called Operational or Audit Logs) for information about your resource as seen by the Azure infrastructure.</span></span> <span data-ttu-id="34e24-147">Dziennik zawiera informacje, takie jak czas, kiedy zasoby są tworzone lub zniszczony.</span><span class="sxs-lookup"><span data-stu-id="34e24-147">The log contains information such as times when resources are created or destroyed.</span></span>  <span data-ttu-id="34e24-148">Aby uzyskać więcej informacji, zobacz [omówienie dziennik aktywności](monitoring-overview-activity-logs.md).</span><span class="sxs-lookup"><span data-stu-id="34e24-148">For more information, see [Overview of Activity Log](monitoring-overview-activity-logs.md).</span></span> 

## <a name="monitoring-sources---everything-else"></a><span data-ttu-id="34e24-149">Monitorowanie źródeł - wszystkie inne</span><span class="sxs-lookup"><span data-stu-id="34e24-149">Monitoring Sources - everything else</span></span>

![Model do monitorowania i diagnostyki dla zasobów obliczeniowych](./media/monitoring-overview-azure-monitor/Monitoring_Azure_Resources-non-compute_v6.png)


### <a name="resource---metrics-and-diagnostics-logs"></a><span data-ttu-id="34e24-151">Zasobu, metryki i dzienniki diagnostyczne</span><span class="sxs-lookup"><span data-stu-id="34e24-151">Resource - Metrics and Diagnostics Logs</span></span>
<span data-ttu-id="34e24-152">Do zebrania metryki i informacji diagnostycznych dzienników różnić w zależności od typu zasobu.</span><span class="sxs-lookup"><span data-stu-id="34e24-152">Collectable metrics and diagnostics logs vary based on the resource type.</span></span> <span data-ttu-id="34e24-153">Na przykład aplikacje sieci Web zawiera dane statystyczne dotyczące operacji We/Wy dysku i procesora CPU w procentach.</span><span class="sxs-lookup"><span data-stu-id="34e24-153">For example, Web Apps provides statistics on the Disk IO and Percent CPU.</span></span> <span data-ttu-id="34e24-154">Te metryki nie istnieje dla kolejki usługi Service Bus, która przekazuje metryk, takich jak kolejki przepływności rozmiaru i komunikatów.</span><span class="sxs-lookup"><span data-stu-id="34e24-154">Those metrics don't exist for a Service Bus queue, which instead provides metrics like queue size and message throughput.</span></span> <span data-ttu-id="34e24-155">Lista do zebrania metryki dla każdego zasobu jest dostępna na [obsługiwane metryki](monitoring-supported-metrics.md).</span><span class="sxs-lookup"><span data-stu-id="34e24-155">A list of collectable metrics for each resource is available at [supported metrics](monitoring-supported-metrics.md).</span></span> 

### <a name="host-and-guest-vm-metrics"></a><span data-ttu-id="34e24-156">Metryki hosta i gościa maszyny Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="34e24-156">Host and Guest VM metrics</span></span>
<span data-ttu-id="34e24-157">Nie jest zawsze mapowanie 1:1 od zasobu do określonego hosta lub maszyny Wirtualnej gościa, metryki nie są dostępne.</span><span class="sxs-lookup"><span data-stu-id="34e24-157">There is not necessarily a 1:1 mapping between your resource and a particular Host or Guest VM so metrics are not available.</span></span>

### <a name="activity-log"></a><span data-ttu-id="34e24-158">Dziennik aktywności</span><span class="sxs-lookup"><span data-stu-id="34e24-158">Activity Log</span></span>
<span data-ttu-id="34e24-159">Dziennik aktywności jest taka sama, jak w przypadku zasobów obliczeniowych.</span><span class="sxs-lookup"><span data-stu-id="34e24-159">The activity log is the same as for compute resources.</span></span>  

## <a name="uses-for-monitoring-data"></a><span data-ttu-id="34e24-160">Używane do monitorowania danych</span><span class="sxs-lookup"><span data-stu-id="34e24-160">Uses for Monitoring Data</span></span>
<span data-ttu-id="34e24-161">Po zebraniu danych można wykonywać następujące z nim w monitorze Azure</span><span class="sxs-lookup"><span data-stu-id="34e24-161">Once you collect your data, you can do the following with it in Azure Monitor</span></span>

### <a name="route"></a><span data-ttu-id="34e24-162">Trasa</span><span class="sxs-lookup"><span data-stu-id="34e24-162">Route</span></span>
<span data-ttu-id="34e24-163">Można przesyłać strumieniowo dane monitorowania do innych lokalizacji w czasie rzeczywistym.</span><span class="sxs-lookup"><span data-stu-id="34e24-163">You can stream monitoring data to other locations in real time.</span></span>

<span data-ttu-id="34e24-164">Przykłady:</span><span class="sxs-lookup"><span data-stu-id="34e24-164">Examples include:</span></span>

- <span data-ttu-id="34e24-165">Wyślij do usługi Application Insights, dzięki czemu można używać jej bardziej zaawansowane funkcje narzędzi wizualizacji i analizy.</span><span class="sxs-lookup"><span data-stu-id="34e24-165">Send to Application Insights so you can use its richer visualization and analysis tools.</span></span>
- <span data-ttu-id="34e24-166">Wyślij do usługi Event Hubs, można kierować do narzędzi innych firm.</span><span class="sxs-lookup"><span data-stu-id="34e24-166">Send to Event Hubs so you can route to third-party tools.</span></span> 

### <a name="store-and-archive"></a><span data-ttu-id="34e24-167">Magazyn i archiwum</span><span class="sxs-lookup"><span data-stu-id="34e24-167">Store and Archive</span></span>
<span data-ttu-id="34e24-168">Niektóre dane monitorowania jest już przechowywane i dostępne w monitorze Azure dla określonej ilości czasu.</span><span class="sxs-lookup"><span data-stu-id="34e24-168">Some monitoring data is already stored and available in Azure Monitor for a set amount of time.</span></span> 
- <span data-ttu-id="34e24-169">Metryki są przechowywane przez 30 dni.</span><span class="sxs-lookup"><span data-stu-id="34e24-169">Metrics are stored for 30 days.</span></span> 
- <span data-ttu-id="34e24-170">Wpisy dziennika aktywności są przechowywane przez 90 dni.</span><span class="sxs-lookup"><span data-stu-id="34e24-170">Activity log entries are stored for 90 days.</span></span> 
- <span data-ttu-id="34e24-171">Dzienniki diagnostyczne nie są przechowywane w ogóle.</span><span class="sxs-lookup"><span data-stu-id="34e24-171">Diagnostics logs are not stored at all.</span></span> 

<span data-ttu-id="34e24-172">Jeśli chcesz przechowywać dane dłużej niż okresów wymienionych powyżej, można użyć usługi Azure storage.</span><span class="sxs-lookup"><span data-stu-id="34e24-172">If you want to store data longer than the time periods listed above, you can use an Azure storage.</span></span> <span data-ttu-id="34e24-173">Monitorowanie danych jest przechowywana w na podstawie zasad przechowywania, które można ustawić konto magazynu.</span><span class="sxs-lookup"><span data-stu-id="34e24-173">Monitoring data is kept in your storage acccount based on a retention policy you set.</span></span> <span data-ttu-id="34e24-174">Trzeba płacić za obszar danych zajmuje w magazynie Azure.</span><span class="sxs-lookup"><span data-stu-id="34e24-174">You do have to pay for the space the data takes up in Azure storage.</span></span> 

<span data-ttu-id="34e24-175">Na kilka sposobów, aby użyć tych danych:</span><span class="sxs-lookup"><span data-stu-id="34e24-175">A few ways to use this data:</span></span>

- <span data-ttu-id="34e24-176">Po zapisaniu, może mieć inne narzędzia wewnątrz lub na zewnątrz Azure Przeczytaj je i go przetworzyć.</span><span class="sxs-lookup"><span data-stu-id="34e24-176">Once written, you can have other tools within or outside of Azure read it and process it.</span></span>
- <span data-ttu-id="34e24-177">Pobierz dane lokalnie archiwum lokalnego lub zmień Twoje zasady przechowywania w chmurze i Zachowaj dane przez dłuższy czas.</span><span class="sxs-lookup"><span data-stu-id="34e24-177">You download the data locally for a local archive or change your retention policy in the cloud to keep data for extended periods of time.</span></span>  
- <span data-ttu-id="34e24-178">Możesz pozostawić dane w magazynie Azure przez czas nieograniczony na potrzeby archiwizacji.</span><span class="sxs-lookup"><span data-stu-id="34e24-178">You leave the data in Azure storage indefinitely for archive purposes.</span></span> 

### <a name="query"></a><span data-ttu-id="34e24-179">Zapytanie</span><span class="sxs-lookup"><span data-stu-id="34e24-179">Query</span></span>
<span data-ttu-id="34e24-180">Azure monitora interfejsu API REST, krzyżyk polecenia interfejsu wiersza polecenia (CLI) platformy, poleceń cmdlet programu PowerShell lub zestawu .NET SDK służy do uzyskiwania dostępu do danych w systemie lub magazynu Azure</span><span class="sxs-lookup"><span data-stu-id="34e24-180">You can use the Azure Monitor REST API, cross platform Command-Line Interface (CLI) commands, PowerShell cmdlets, or the .NET SDK to access the data in the system or Azure storage</span></span>

<span data-ttu-id="34e24-181">Przykłady:</span><span class="sxs-lookup"><span data-stu-id="34e24-181">Examples include:</span></span>

* <span data-ttu-id="34e24-182">Pobieranie danych dla niestandardowych aplikacji monitorowania zapisane</span><span class="sxs-lookup"><span data-stu-id="34e24-182">Getting data for a custom monitoring application you have written</span></span>
* <span data-ttu-id="34e24-183">Tworzenie niestandardowych kwerend i wysyłania danych do aplikacji innych firm.</span><span class="sxs-lookup"><span data-stu-id="34e24-183">Creating custom queries and sending that data to a third-party application.</span></span>

### <a name="visualize"></a><span data-ttu-id="34e24-184">Wizualizowanie</span><span class="sxs-lookup"><span data-stu-id="34e24-184">Visualize</span></span>
<span data-ttu-id="34e24-185">Wizualizacja danych monitorowania w grafiki i wykresy ułatwia trendów szybsze niż wyszukiwanie za pomocą samych danych.</span><span class="sxs-lookup"><span data-stu-id="34e24-185">Visualizing your monitoring data in graphics and charts helps you find trends quicker than looking through the data itself.</span></span>  

<span data-ttu-id="34e24-186">Kilka metod wizualizacji obejmują:</span><span class="sxs-lookup"><span data-stu-id="34e24-186">A few visualization methods include:</span></span>

* <span data-ttu-id="34e24-187">Korzystanie z witryny Azure Portal</span><span class="sxs-lookup"><span data-stu-id="34e24-187">Use the Azure portal</span></span>
* <span data-ttu-id="34e24-188">Dane trasy do usługi Azure Application Insights</span><span class="sxs-lookup"><span data-stu-id="34e24-188">Route data to Azure Application Insights</span></span>
* <span data-ttu-id="34e24-189">Dane trasy do Microsoft PowerBI</span><span class="sxs-lookup"><span data-stu-id="34e24-189">Route data to Microsoft PowerBI</span></span>
* <span data-ttu-id="34e24-190">Dane trasy, narzędzie wizualizacji innych firm przy użyciu albo transmisja strumieniowa na żywo lub przez narzędzie odczytywać archiwum w magazynie Azure</span><span class="sxs-lookup"><span data-stu-id="34e24-190">Route the data to a third-party visualization tool using either live streaming or by having the tool read from an archive in Azure storage</span></span>


### <a name="automate"></a><span data-ttu-id="34e24-191">Automatyzacja</span><span class="sxs-lookup"><span data-stu-id="34e24-191">Automate</span></span>
<span data-ttu-id="34e24-192">Można użyć danych monitorowania do wyzwalania alertów lub nawet cały proces.</span><span class="sxs-lookup"><span data-stu-id="34e24-192">You can use monitoring data to trigger alerts or even whole processes.</span></span> <span data-ttu-id="34e24-193">Przykłady:</span><span class="sxs-lookup"><span data-stu-id="34e24-193">Examples include:</span></span>

* <span data-ttu-id="34e24-194">Użyj danych do wystąpienia obliczeniowe automatycznego skalowania w górę lub w dół oparte na obciążenia aplikacji.</span><span class="sxs-lookup"><span data-stu-id="34e24-194">Use data to autoscale compute instances up or down based on application load.</span></span>
* <span data-ttu-id="34e24-195">Wysyłaj wiadomości e-mail, gdy metryki przecina wstępnie określoną wartość progową.</span><span class="sxs-lookup"><span data-stu-id="34e24-195">Send emails when a metric crosses a predetermined threshold.</span></span>
* <span data-ttu-id="34e24-196">Wywołaj adres URL sieci web (webhook) do wykonywania akcji w systemie poza platformą Azure</span><span class="sxs-lookup"><span data-stu-id="34e24-196">Call a web URL (webhook) to execute an action in a system outside of Azure</span></span>
* <span data-ttu-id="34e24-197">Uruchom element runbook w automatyzacji Azure, aby wykonać wszelkie różnych zadań</span><span class="sxs-lookup"><span data-stu-id="34e24-197">Start a runbook in Azure automation to perform any variety of tasks</span></span>

## <a name="methods-of-accessing-azure-monitor"></a><span data-ttu-id="34e24-198">Metody dostępu do monitora Azure</span><span class="sxs-lookup"><span data-stu-id="34e24-198">Methods of accessing Azure Monitor</span></span>
<span data-ttu-id="34e24-199">Ogólnie rzecz biorąc można manipulować danych śledzenia, routingu i pobierania za pomocą jednej z poniższych metod.</span><span class="sxs-lookup"><span data-stu-id="34e24-199">In general, you can manipulate data tracking, routing, and retrieval using one of the following methods.</span></span> <span data-ttu-id="34e24-200">Nie wszystkie metody są dostępne dla wszystkich akcji lub typów danych.</span><span class="sxs-lookup"><span data-stu-id="34e24-200">Not all methods are available for all actions or data types.</span></span>

* [<span data-ttu-id="34e24-201">Witryna Azure Portal</span><span class="sxs-lookup"><span data-stu-id="34e24-201">Azure portal</span></span>](https://portal.azure.com)
* [<span data-ttu-id="34e24-202">PowerShell</span><span class="sxs-lookup"><span data-stu-id="34e24-202">PowerShell</span></span>](insights-powershell-samples.md)  
* [<span data-ttu-id="34e24-203">Interfejs wiersza polecenia i platform (CLI)</span><span class="sxs-lookup"><span data-stu-id="34e24-203">Cross-platform Command Line Interface (CLI)</span></span>](insights-cli-samples.md)
* [<span data-ttu-id="34e24-204">Interfejs API REST</span><span class="sxs-lookup"><span data-stu-id="34e24-204">REST API</span></span>](https://docs.microsoft.com/rest/api/monitor/)
* [<span data-ttu-id="34e24-205">Zestaw SDK platformy .NET</span><span class="sxs-lookup"><span data-stu-id="34e24-205">.NET SDK</span></span>](http://www.nuget.org/packages/Microsoft.Azure.Management.Monitor)

## <a name="next-steps"></a><span data-ttu-id="34e24-206">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="34e24-206">Next steps</span></span>
<span data-ttu-id="34e24-207">Dowiedz się więcej o</span><span class="sxs-lookup"><span data-stu-id="34e24-207">Learn more about</span></span>
- <span data-ttu-id="34e24-208">Przewodnik wideo tylko monitora Azure znajduje się w temacie</span><span class="sxs-lookup"><span data-stu-id="34e24-208">A video walkthrough of just Azure Monitor is available at</span></span>  
<span data-ttu-id="34e24-209">[Wprowadzenie do platformy Azure Monitor](https://channel9.msdn.com/Blogs/Azure-Monitoring/Get-Started-with-Azure-Monitor).</span><span class="sxs-lookup"><span data-stu-id="34e24-209">[Get Started with Azure Monitor](https://channel9.msdn.com/Blogs/Azure-Monitoring/Get-Started-with-Azure-Monitor).</span></span> <span data-ttu-id="34e24-210">Dodatkowe wideo wyjaśniający scenariusz, w których można użyć Monitora Azure znajduje się w temacie [Eksploruj Microsoft Azure, monitorowania i diagnostyki](https://channel9.msdn.com/events/Ignite/2016/BRK2234) i [Azure Monitor wideo z Ignite 2016](https://myignite.microsoft.com/videos/4977)</span><span class="sxs-lookup"><span data-stu-id="34e24-210">An additional video explaining a scenario where you can use Azure Monitor is available at [Explore Microsoft Azure monitoring and diagnostics](https://channel9.msdn.com/events/Ignite/2016/BRK2234) and [Azure Monitor in a video from Ignite 2016](https://myignite.microsoft.com/videos/4977)</span></span>
- <span data-ttu-id="34e24-211">Uruchom za pomocą interfejsu Azure Monitor w [wprowadzenie Azure Monitor](monitoring-get-started.md)</span><span class="sxs-lookup"><span data-stu-id="34e24-211">Run through the Azure Monitor interface in [Getting Started with Azure Monitor](monitoring-get-started.md)</span></span>
- <span data-ttu-id="34e24-212">Konfigurowanie [rozszerzenia diagnostyki Azure](../azure-diagnostics.md) Jeśli próbujesz do diagnozowania problemów w usłudze chmury maszyny wirtualnej maszyny wirtualnej skalowanie zestawów lub aplikacji sieci szkieletowej usług.</span><span class="sxs-lookup"><span data-stu-id="34e24-212">Set up the [Azure Diagnostics Extensions](../azure-diagnostics.md) if you are attempting to diagnose problems in your Cloud Service, Virtual Machine, Virtual machine scale sets, or Service Fabric application.</span></span>
- <span data-ttu-id="34e24-213">[Usługa Application Insights](https://azure.microsoft.com/documentation/services/application-insights/) Jeśli próbujesz diagnostycznych problemy w aplikacji sieci Web usługi aplikacji.</span><span class="sxs-lookup"><span data-stu-id="34e24-213">[Application Insights](https://azure.microsoft.com/documentation/services/application-insights/) if you are trying to diagnostic problems in your App Service Web app.</span></span>
- <span data-ttu-id="34e24-214">[Rozwiązywanie problemów z magazynem Azure](../storage/common/storage-e2e-troubleshooting.md) przy użyciu magazynu obiektów blob, tabel lub kolejek</span><span class="sxs-lookup"><span data-stu-id="34e24-214">[Troubleshooting Azure Storage](../storage/common/storage-e2e-troubleshooting.md) when using Storage Blobs, Tables, or Queues</span></span>
- <span data-ttu-id="34e24-215">[Zaloguj się Analytics](https://azure.microsoft.com/documentation/services/log-analytics/) i [Operations Management Suite](https://www.microsoft.com/oms/)</span><span class="sxs-lookup"><span data-stu-id="34e24-215">[Log Analytics](https://azure.microsoft.com/documentation/services/log-analytics/) and the [Operations Management Suite](https://www.microsoft.com/oms/)</span></span>
