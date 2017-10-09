---
title: "Liczniki wydajności w diagnostyce Azure aaaUse | Dokumentacja firmy Microsoft"
description: "Użyj liczników wydajności usługi w chmurze platformy Azure lub wąskich gardeł toofind maszyny wirtualnej i dostrajania wydajności."
services: cloud-services
documentationcenter: .net
author: rboucher
manager: jwhit
editor: tysonn
ms.assetid: fc4c61e9-d49d-4ed9-a32c-b91cdf851909
ms.service: cloud-services
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 02/29/2016
ms.author: robb
ms.openlocfilehash: f3250816c01fc6e164a6aae48da5035845e6d2b3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-use-performance-counters-in-an-azure-application"></a><span data-ttu-id="c8e3b-103">Tworzenie i używanie liczników wydajności w aplikacji Azure</span><span class="sxs-lookup"><span data-stu-id="c8e3b-103">Create and use performance counters in an Azure application</span></span>
<span data-ttu-id="c8e3b-104">W tym artykule opisano hello zalet i jak liczniki wydajności tooput do aplikacji platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="c8e3b-104">This article describes hello benefits of and how tooput performance counters into your Azure application.</span></span> <span data-ttu-id="c8e3b-105">Można ich używać danych toocollect, Znajdź wąskich gardeł i dostrajania wydajności systemu i aplikacji.</span><span class="sxs-lookup"><span data-stu-id="c8e3b-105">You can use them toocollect data, find bottlenecks, and tune system and application performance.</span></span>

<span data-ttu-id="c8e3b-106">Liczniki wydajności są dostępne dla systemu Windows Server, IIS i platformy ASP.NET można także gromadzić i używane kondycji hello toodetermine role sieci web platformy Azure, roli proces roboczy i maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="c8e3b-106">Performance counters available for Windows Server, IIS, and ASP.NET can also be collected and used toodetermine hello health of your Azure web roles, worker roles, and Virtual Machines.</span></span> <span data-ttu-id="c8e3b-107">Można również utworzyć i używać niestandardowe liczniki wydajności.</span><span class="sxs-lookup"><span data-stu-id="c8e3b-107">You can also create and use custom performance counters.</span></span>  

<span data-ttu-id="c8e3b-108">Należy zbadać dane licznika wydajności</span><span class="sxs-lookup"><span data-stu-id="c8e3b-108">You can examine performance counter data</span></span>

1. <span data-ttu-id="c8e3b-109">Bezpośrednio na hoście aplikacji hello za pomocą narzędzia Monitor wydajności hello dostęp za pomocą pulpitu zdalnego</span><span class="sxs-lookup"><span data-stu-id="c8e3b-109">Directly on hello application host with hello Performance Monitor tool accessed using Remote Desktop</span></span>
2. <span data-ttu-id="c8e3b-110">Przy użyciu programu System Center Operations Manager hello Azure pakietu administracyjnego</span><span class="sxs-lookup"><span data-stu-id="c8e3b-110">With System Center Operations Manager using hello Azure Management Pack</span></span>
3. <span data-ttu-id="c8e3b-111">Przy użyciu innych narzędzi monitorowania, które uzyskują dostęp do hello danych diagnostycznych transferu tooAzure magazynu.</span><span class="sxs-lookup"><span data-stu-id="c8e3b-111">With other monitoring tools that access hello diagnostic data transferred tooAzure storage.</span></span> <span data-ttu-id="c8e3b-112">Zobacz [magazynu i widoku danych diagnostycznych w usłudze Azure Storage](https://msdn.microsoft.com/library/azure/hh411534.aspx) Aby uzyskać więcej informacji.</span><span class="sxs-lookup"><span data-stu-id="c8e3b-112">See [Store and View Diagnostic Data in Azure Storage](https://msdn.microsoft.com/library/azure/hh411534.aspx) for more information.</span></span>  

<span data-ttu-id="c8e3b-113">Aby uzyskać więcej informacji na temat monitorowania wydajności aplikacji hello hello [portalu Azure](http://portal.azure.com/), zobacz [jak usług w chmurze tooMonitor](https://www.azure.com/manage/services/cloud-services/how-to-monitor-a-cloud-service/).</span><span class="sxs-lookup"><span data-stu-id="c8e3b-113">For more information on monitoring hello performance of your application in hello [Azure portal](http://portal.azure.com/), see [How tooMonitor Cloud Services](https://www.azure.com/manage/services/cloud-services/how-to-monitor-a-cloud-service/).</span></span>

<span data-ttu-id="c8e3b-114">Aby uzyskać dodatkowe szczegółowe wskazówki na temat tworzenia rejestrowania i śledzenia strategii i przy użyciu innych technik tootroubleshoot problemów i Diagnostyka i optymalizowanie aplikacji Azure, zobacz [Rozwiązywanie problemów z najlepszych rozwiązań dotyczących tworzenia Azure Aplikacje](https://msdn.microsoft.com/library/azure/hh771389.aspx).</span><span class="sxs-lookup"><span data-stu-id="c8e3b-114">For additional in-depth guidance on creating a logging and tracing strategy and using diagnostics and other techniques tootroubleshoot problems and optimize Azure applications, see [Troubleshooting Best Practices for Developing Azure Applications](https://msdn.microsoft.com/library/azure/hh771389.aspx).</span></span>

## <a name="enable-performance-counter-monitoring"></a><span data-ttu-id="c8e3b-115">Aby włączyć monitorowanie licznika wydajności</span><span class="sxs-lookup"><span data-stu-id="c8e3b-115">Enable performance counter monitoring</span></span>
<span data-ttu-id="c8e3b-116">Liczniki wydajności nie są domyślnie włączone.</span><span class="sxs-lookup"><span data-stu-id="c8e3b-116">Performance counters are not enabled by default.</span></span> <span data-ttu-id="c8e3b-117">Aplikacja lub zadanie uruchamiania należy zmodyfikować diagnostyki domyślne hello liczników wydajności zależnych hello tooinclude konfiguracji agenta, że chcesz toomonitor dla każdego wystąpienia roli.</span><span class="sxs-lookup"><span data-stu-id="c8e3b-117">Your application or a startup task must modify hello default diagnostics agent configuration tooinclude hello specific performance counters that you wish toomonitor for each role instance.</span></span>

### <a name="performance-counters-available-for-microsoft-azure"></a><span data-ttu-id="c8e3b-118">Liczniki wydajności dostępne platformy Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="c8e3b-118">Performance counters available for Microsoft Azure</span></span>
<span data-ttu-id="c8e3b-119">Platforma Azure udostępnia podzbiór hello dostępnych liczników wydajności dla systemu Windows Server, IIS i hello stosu ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="c8e3b-119">Azure provides a subset of hello performance counters available for Windows Server, IIS and hello ASP.NET stack.</span></span> <span data-ttu-id="c8e3b-120">Witaj poniższej tabeli wymieniono niektóre liczniki wydajności hello szczególne znaczenie dla aplikacji platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="c8e3b-120">hello following table lists some of hello performance counters of particular interest for Azure applications.</span></span>

| <span data-ttu-id="c8e3b-121">Kategoria licznika: Obiektu (wystąpienia)</span><span class="sxs-lookup"><span data-stu-id="c8e3b-121">Counter Category: Object (Instance)</span></span> | <span data-ttu-id="c8e3b-122">Nazwa licznika</span><span class="sxs-lookup"><span data-stu-id="c8e3b-122">Counter Name</span></span> | <span data-ttu-id="c8e3b-123">Dokumentacja</span><span class="sxs-lookup"><span data-stu-id="c8e3b-123">Reference</span></span> |
| --- | --- | --- |
| <span data-ttu-id="c8e3b-124">Wyjątki środowiska CLR platformy .NET (*globalne*)</span><span class="sxs-lookup"><span data-stu-id="c8e3b-124">.NET CLR Exceptions(*Global*)</span></span> |<span data-ttu-id="c8e3b-125"># Clr\\liczba wyjątków / s</span><span class="sxs-lookup"><span data-stu-id="c8e3b-125"># Exceps Thrown / sec</span></span> |<span data-ttu-id="c8e3b-126">Liczniki wydajności wyjątku</span><span class="sxs-lookup"><span data-stu-id="c8e3b-126">Exception Performance Counters</span></span> |
| <span data-ttu-id="c8e3b-127">.NET CLR pamięci (*globalne*)</span><span class="sxs-lookup"><span data-stu-id="c8e3b-127">.NET CLR Memory(*Global*)</span></span> |<span data-ttu-id="c8e3b-128">% Czasu odzyskiwania pamięci</span><span class="sxs-lookup"><span data-stu-id="c8e3b-128">% Time in GC</span></span> |<span data-ttu-id="c8e3b-129">Liczniki wydajności pamięci</span><span class="sxs-lookup"><span data-stu-id="c8e3b-129">Memory Performance Counters</span></span> |
| <span data-ttu-id="c8e3b-130">ASP.NET</span><span class="sxs-lookup"><span data-stu-id="c8e3b-130">ASP.NET</span></span> |<span data-ttu-id="c8e3b-131">Aplikacja zostanie uruchomiona ponownie</span><span class="sxs-lookup"><span data-stu-id="c8e3b-131">Application Restarts</span></span> |<span data-ttu-id="c8e3b-132">Liczniki wydajności dla programu ASP.NET</span><span class="sxs-lookup"><span data-stu-id="c8e3b-132">Performance Counters for ASP.NET</span></span> |
| <span data-ttu-id="c8e3b-133">ASP.NET</span><span class="sxs-lookup"><span data-stu-id="c8e3b-133">ASP.NET</span></span> |<span data-ttu-id="c8e3b-134">Czas wykonania żądania</span><span class="sxs-lookup"><span data-stu-id="c8e3b-134">Request Execution Time</span></span> |<span data-ttu-id="c8e3b-135">Liczniki wydajności dla programu ASP.NET</span><span class="sxs-lookup"><span data-stu-id="c8e3b-135">Performance Counters for ASP.NET</span></span> |
| <span data-ttu-id="c8e3b-136">ASP.NET</span><span class="sxs-lookup"><span data-stu-id="c8e3b-136">ASP.NET</span></span> |<span data-ttu-id="c8e3b-137">Liczba żądań rozłączonych</span><span class="sxs-lookup"><span data-stu-id="c8e3b-137">Requests Disconnected</span></span> |<span data-ttu-id="c8e3b-138">Liczniki wydajności dla programu ASP.NET</span><span class="sxs-lookup"><span data-stu-id="c8e3b-138">Performance Counters for ASP.NET</span></span> |
| <span data-ttu-id="c8e3b-139">ASP.NET</span><span class="sxs-lookup"><span data-stu-id="c8e3b-139">ASP.NET</span></span> |<span data-ttu-id="c8e3b-140">Ponowne uruchomienie procesu roboczego</span><span class="sxs-lookup"><span data-stu-id="c8e3b-140">Worker Process Restarts</span></span> |<span data-ttu-id="c8e3b-141">Liczniki wydajności dla programu ASP.NET</span><span class="sxs-lookup"><span data-stu-id="c8e3b-141">Performance Counters for ASP.NET</span></span> |
| <span data-ttu-id="c8e3b-142">Aplikacji programu ASP.NET (**całkowita**)</span><span class="sxs-lookup"><span data-stu-id="c8e3b-142">ASP.NET Applications(**Total**)</span></span> |<span data-ttu-id="c8e3b-143">Całkowita liczba żądań</span><span class="sxs-lookup"><span data-stu-id="c8e3b-143">Requests Total</span></span> |<span data-ttu-id="c8e3b-144">Liczniki wydajności dla programu ASP.NET</span><span class="sxs-lookup"><span data-stu-id="c8e3b-144">Performance Counters for ASP.NET</span></span> |
| <span data-ttu-id="c8e3b-145">Aplikacji programu ASP.NET (**całkowita**)</span><span class="sxs-lookup"><span data-stu-id="c8e3b-145">ASP.NET Applications(**Total**)</span></span> |<span data-ttu-id="c8e3b-146">Żądania na sekundę</span><span class="sxs-lookup"><span data-stu-id="c8e3b-146">Requests/Sec</span></span> |<span data-ttu-id="c8e3b-147">Liczniki wydajności dla programu ASP.NET</span><span class="sxs-lookup"><span data-stu-id="c8e3b-147">Performance Counters for ASP.NET</span></span> |
| <span data-ttu-id="c8e3b-148">ASP.NET 4.0.30319</span><span class="sxs-lookup"><span data-stu-id="c8e3b-148">ASP.NET v4.0.30319</span></span> |<span data-ttu-id="c8e3b-149">Czas wykonania żądania</span><span class="sxs-lookup"><span data-stu-id="c8e3b-149">Request Execution Time</span></span> |<span data-ttu-id="c8e3b-150">Liczniki wydajności dla programu ASP.NET</span><span class="sxs-lookup"><span data-stu-id="c8e3b-150">Performance Counters for ASP.NET</span></span> |
| <span data-ttu-id="c8e3b-151">ASP.NET 4.0.30319</span><span class="sxs-lookup"><span data-stu-id="c8e3b-151">ASP.NET v4.0.30319</span></span> |<span data-ttu-id="c8e3b-152">Czas oczekiwania na żądanie</span><span class="sxs-lookup"><span data-stu-id="c8e3b-152">Request Wait Time</span></span> |<span data-ttu-id="c8e3b-153">Liczniki wydajności dla programu ASP.NET</span><span class="sxs-lookup"><span data-stu-id="c8e3b-153">Performance Counters for ASP.NET</span></span> |
| <span data-ttu-id="c8e3b-154">ASP.NET 4.0.30319</span><span class="sxs-lookup"><span data-stu-id="c8e3b-154">ASP.NET v4.0.30319</span></span> |<span data-ttu-id="c8e3b-155">Bieżące żądania</span><span class="sxs-lookup"><span data-stu-id="c8e3b-155">Requests Current</span></span> |<span data-ttu-id="c8e3b-156">Liczniki wydajności dla programu ASP.NET</span><span class="sxs-lookup"><span data-stu-id="c8e3b-156">Performance Counters for ASP.NET</span></span> |
| <span data-ttu-id="c8e3b-157">ASP.NET 4.0.30319</span><span class="sxs-lookup"><span data-stu-id="c8e3b-157">ASP.NET v4.0.30319</span></span> |<span data-ttu-id="c8e3b-158">Liczba żądań w kolejce</span><span class="sxs-lookup"><span data-stu-id="c8e3b-158">Requests Queued</span></span> |<span data-ttu-id="c8e3b-159">Liczniki wydajności dla programu ASP.NET</span><span class="sxs-lookup"><span data-stu-id="c8e3b-159">Performance Counters for ASP.NET</span></span> |
| <span data-ttu-id="c8e3b-160">ASP.NET 4.0.30319</span><span class="sxs-lookup"><span data-stu-id="c8e3b-160">ASP.NET v4.0.30319</span></span> |<span data-ttu-id="c8e3b-161">Liczba żądań odrzuconych</span><span class="sxs-lookup"><span data-stu-id="c8e3b-161">Requests Rejected</span></span> |<span data-ttu-id="c8e3b-162">Liczniki wydajności dla programu ASP.NET</span><span class="sxs-lookup"><span data-stu-id="c8e3b-162">Performance Counters for ASP.NET</span></span> |
| <span data-ttu-id="c8e3b-163">Memory (Pamięć)</span><span class="sxs-lookup"><span data-stu-id="c8e3b-163">Memory</span></span> |<span data-ttu-id="c8e3b-164">Dostępna pamięć (MB)</span><span class="sxs-lookup"><span data-stu-id="c8e3b-164">Available MBytes</span></span> |<span data-ttu-id="c8e3b-165">Liczniki wydajności pamięci</span><span class="sxs-lookup"><span data-stu-id="c8e3b-165">Memory Performance Counters</span></span> |
| <span data-ttu-id="c8e3b-166">Memory (Pamięć)</span><span class="sxs-lookup"><span data-stu-id="c8e3b-166">Memory</span></span> |<span data-ttu-id="c8e3b-167">Zadeklarowane bajty</span><span class="sxs-lookup"><span data-stu-id="c8e3b-167">Committed Bytes</span></span> |<span data-ttu-id="c8e3b-168">Liczniki wydajności pamięci</span><span class="sxs-lookup"><span data-stu-id="c8e3b-168">Memory Performance Counters</span></span> |
| <span data-ttu-id="c8e3b-169">Procesor(_Total)</span><span class="sxs-lookup"><span data-stu-id="c8e3b-169">Processor(_Total)</span></span> |<span data-ttu-id="c8e3b-170">Czas procesora (%)</span><span class="sxs-lookup"><span data-stu-id="c8e3b-170">% Processor Time</span></span> |<span data-ttu-id="c8e3b-171">Liczniki wydajności dla programu ASP.NET</span><span class="sxs-lookup"><span data-stu-id="c8e3b-171">Performance Counters for ASP.NET</span></span> |
| <span data-ttu-id="c8e3b-172">TCPv4</span><span class="sxs-lookup"><span data-stu-id="c8e3b-172">TCPv4</span></span> |<span data-ttu-id="c8e3b-173">Liczba błędów połączenia</span><span class="sxs-lookup"><span data-stu-id="c8e3b-173">Connection Failures</span></span> |<span data-ttu-id="c8e3b-174">Obiekt TCP</span><span class="sxs-lookup"><span data-stu-id="c8e3b-174">TCP Object</span></span> |
| <span data-ttu-id="c8e3b-175">TCPv4</span><span class="sxs-lookup"><span data-stu-id="c8e3b-175">TCPv4</span></span> |<span data-ttu-id="c8e3b-176">Połączeń</span><span class="sxs-lookup"><span data-stu-id="c8e3b-176">Connections Established</span></span> |<span data-ttu-id="c8e3b-177">Obiekt TCP</span><span class="sxs-lookup"><span data-stu-id="c8e3b-177">TCP Object</span></span> |
| <span data-ttu-id="c8e3b-178">TCPv4</span><span class="sxs-lookup"><span data-stu-id="c8e3b-178">TCPv4</span></span> |<span data-ttu-id="c8e3b-179">Resetowanie połączenia</span><span class="sxs-lookup"><span data-stu-id="c8e3b-179">Connections Reset</span></span> |<span data-ttu-id="c8e3b-180">Obiekt TCP</span><span class="sxs-lookup"><span data-stu-id="c8e3b-180">TCP Object</span></span> |
| <span data-ttu-id="c8e3b-181">TCPv4</span><span class="sxs-lookup"><span data-stu-id="c8e3b-181">TCPv4</span></span> |<span data-ttu-id="c8e3b-182">Segmenty wysłane/s</span><span class="sxs-lookup"><span data-stu-id="c8e3b-182">Segments Sent/sec</span></span> |<span data-ttu-id="c8e3b-183">Obiekt TCP</span><span class="sxs-lookup"><span data-stu-id="c8e3b-183">TCP Object</span></span> |
| <span data-ttu-id="c8e3b-184">Interface(*) sieci</span><span class="sxs-lookup"><span data-stu-id="c8e3b-184">Network Interface(*)</span></span> |<span data-ttu-id="c8e3b-185">Bajty odebrane/s</span><span class="sxs-lookup"><span data-stu-id="c8e3b-185">Bytes Received/sec</span></span> |<span data-ttu-id="c8e3b-186">Obiekt interfejsu sieciowego</span><span class="sxs-lookup"><span data-stu-id="c8e3b-186">Network Interface Object</span></span> |
| <span data-ttu-id="c8e3b-187">Interface(*) sieci</span><span class="sxs-lookup"><span data-stu-id="c8e3b-187">Network Interface(*)</span></span> |<span data-ttu-id="c8e3b-188">Bajty wysłane/s</span><span class="sxs-lookup"><span data-stu-id="c8e3b-188">Bytes Sent/sec</span></span> |<span data-ttu-id="c8e3b-189">Obiekt interfejsu sieciowego</span><span class="sxs-lookup"><span data-stu-id="c8e3b-189">Network Interface Object</span></span> |
| <span data-ttu-id="c8e3b-190">Interfejs sieciowy (_2 karty magistrali maszyny wirtualnej Microsoft sieci)</span><span class="sxs-lookup"><span data-stu-id="c8e3b-190">Network Interface(Microsoft Virtual Machine Bus Network Adapter _2)</span></span> |<span data-ttu-id="c8e3b-191">Bajty odebrane/s</span><span class="sxs-lookup"><span data-stu-id="c8e3b-191">Bytes Received/sec</span></span> |<span data-ttu-id="c8e3b-192">Obiekt interfejsu sieciowego</span><span class="sxs-lookup"><span data-stu-id="c8e3b-192">Network Interface Object</span></span> |
| <span data-ttu-id="c8e3b-193">Interfejs sieciowy (_2 karty magistrali maszyny wirtualnej Microsoft sieci)</span><span class="sxs-lookup"><span data-stu-id="c8e3b-193">Network Interface(Microsoft Virtual Machine Bus Network Adapter _2)</span></span> |<span data-ttu-id="c8e3b-194">Bajty wysłane/s</span><span class="sxs-lookup"><span data-stu-id="c8e3b-194">Bytes Sent/sec</span></span> |<span data-ttu-id="c8e3b-195">Obiekt interfejsu sieciowego</span><span class="sxs-lookup"><span data-stu-id="c8e3b-195">Network Interface Object</span></span> |
| <span data-ttu-id="c8e3b-196">Interfejs sieciowy (_2 karty magistrali maszyny wirtualnej Microsoft sieci)</span><span class="sxs-lookup"><span data-stu-id="c8e3b-196">Network Interface(Microsoft Virtual Machine Bus Network Adapter _2)</span></span> |<span data-ttu-id="c8e3b-197">Całkowita liczba bajtów/s</span><span class="sxs-lookup"><span data-stu-id="c8e3b-197">Bytes Total/sec</span></span> |<span data-ttu-id="c8e3b-198">Obiekt interfejsu sieciowego</span><span class="sxs-lookup"><span data-stu-id="c8e3b-198">Network Interface Object</span></span> |

## <a name="create-and-add-custom-performance-counters-tooyour-application"></a><span data-ttu-id="c8e3b-199">Tworzenie i dodawanie aplikacji tooyour liczniki wydajności niestandardowych</span><span class="sxs-lookup"><span data-stu-id="c8e3b-199">Create and add custom performance counters tooyour application</span></span>
<span data-ttu-id="c8e3b-200">Azure ma toocreate pomocy technicznej i zmodyfikuj niestandardowe liczniki wydajności dla ról sieci web i proces roboczy.</span><span class="sxs-lookup"><span data-stu-id="c8e3b-200">Azure has support toocreate and modify custom performance counters for web roles and worker roles.</span></span> <span data-ttu-id="c8e3b-201">Hello liczniki mogą być używane tootrack i monitorowanie zachowania specyficzne dla aplikacji.</span><span class="sxs-lookup"><span data-stu-id="c8e3b-201">hello counters may be used tootrack and monitor application-specific behavior.</span></span> <span data-ttu-id="c8e3b-202">Można tworzyć i usuwanie kategorii licznika wydajności niestandardowych i specyfikatory zadanie uruchamiania, rola sieci web lub roli proces roboczy z podwyższonym poziomem uprawnień.</span><span class="sxs-lookup"><span data-stu-id="c8e3b-202">You can create and delete custom performance counter categories and specifiers from a startup task, web role, or worker role with elevated permissions.</span></span>

> [!NOTE]
> <span data-ttu-id="c8e3b-203">Kod, który zmienia toocustom liczników wydajności mają podwyższony poziom uprawnień toorun.</span><span class="sxs-lookup"><span data-stu-id="c8e3b-203">Code that makes changes toocustom performance counters must have elevated permissions toorun.</span></span> <span data-ttu-id="c8e3b-204">Jeśli kod hello jest w roli sieci web lub roli proces roboczy, hello roli musi zawierać znacznik hello <Runtime executionContext="elevated" /> w hello ServiceDefinition.csdef plików dla tooinitialize roli hello poprawnie.</span><span class="sxs-lookup"><span data-stu-id="c8e3b-204">If hello code is in a web role or worker role, hello role must include hello tag <Runtime executionContext="elevated" /> in hello ServiceDefinition.csdef file for hello role tooinitialize properly.</span></span>
>
>

<span data-ttu-id="c8e3b-205">Możesz wysłać wydajność — niestandardowy licznik tooAzure zapisywanie danych przy użyciu hello Diagnostyka agenta.</span><span class="sxs-lookup"><span data-stu-id="c8e3b-205">You can send custom performance counter data tooAzure storage using hello diagnostics agent.</span></span>

<span data-ttu-id="c8e3b-206">dane licznika wydajności standardowe Hello jest generowany przez hello Azure przetwarzania.</span><span class="sxs-lookup"><span data-stu-id="c8e3b-206">hello standard performance counter data is generated by hello Azure processes.</span></span> <span data-ttu-id="c8e3b-207">Dane licznika wydajności niestandardowych muszą być utworzone przez aplikację sieci web roli lub procesu roboczego roli.</span><span class="sxs-lookup"><span data-stu-id="c8e3b-207">Custom performance counter data must be created by your web role or worker role application.</span></span> <span data-ttu-id="c8e3b-208">Zobacz [typy licznika wydajności](https://msdn.microsoft.com/library/z573042h.aspx) informacje o typach hello danych, które mogą być przechowywane w niestandardowe liczniki wydajności.</span><span class="sxs-lookup"><span data-stu-id="c8e3b-208">See [Performance Counter Types](https://msdn.microsoft.com/library/z573042h.aspx) for information on hello types of data that can be stored in custom performance counters.</span></span> <span data-ttu-id="c8e3b-209">Zobacz [próbki liczniki wydajności](http://code.msdn.microsoft.com/azure/) na przykład, które tworzy i ustawia dane licznika wydajności niestandardowych w roli sieci web.</span><span class="sxs-lookup"><span data-stu-id="c8e3b-209">See [PerformanceCounters Sample](http://code.msdn.microsoft.com/azure/) for an example that creates and sets custom performance counter data in a web role.</span></span>

## <a name="store-and-view-performance-counter-data"></a><span data-ttu-id="c8e3b-210">Magazyn i widoku danych licznika wydajności</span><span class="sxs-lookup"><span data-stu-id="c8e3b-210">Store and view performance counter data</span></span>
<span data-ttu-id="c8e3b-211">Azure przechowuje dane licznika wydajności z innych informacji diagnostycznych.</span><span class="sxs-lookup"><span data-stu-id="c8e3b-211">Azure caches performance counter data with other diagnostic information.</span></span> <span data-ttu-id="c8e3b-212">Te dane są dostępne dla monitorowania zdalnego wystąpienia roli hello jest uruchomiona za pomocą narzędzi tooview dostępu do pulpitu zdalnego, takich jak monitora wydajności.</span><span class="sxs-lookup"><span data-stu-id="c8e3b-212">This data is available for remote monitoring while hello role instance is running using remote desktop access tooview tools such as Performance Monitor.</span></span> <span data-ttu-id="c8e3b-213">toopersist hello poza hello wystąpienia roli, agenta diagnostyki hello musi transferu danych hello tooAzure pamięci masowej.</span><span class="sxs-lookup"><span data-stu-id="c8e3b-213">toopersist hello data outside of hello role instance, hello diagnostics agent must transfer hello data tooAzure storage.</span></span> <span data-ttu-id="c8e3b-214">limit rozmiaru Hello danych licznika wydajności hello w pamięci podręcznej, można skonfigurować w hello Diagnostyka agenta lub może być skonfigurowane toobe częścią udostępnionego limit hello wszystkich danych diagnostycznych.</span><span class="sxs-lookup"><span data-stu-id="c8e3b-214">hello size limit of hello cached performance counter data can be configured in hello diagnostics agent, or it may be configured toobe part of a shared limit for all hello diagnostic data.</span></span> <span data-ttu-id="c8e3b-215">Aby uzyskać więcej informacji na temat ustawiania rozmiaru buforu hello, zobacz [OverallQuotaInMB](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.diagnostics.diagnosticmonitorconfiguration.overallquotainmb.aspx) i [DirectoriesBufferConfiguration](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.diagnostics.directoriesbufferconfiguration.aspx).</span><span class="sxs-lookup"><span data-stu-id="c8e3b-215">For more information about setting hello buffer size, see [OverallQuotaInMB](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.diagnostics.diagnosticmonitorconfiguration.overallquotainmb.aspx) and [DirectoriesBufferConfiguration](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.diagnostics.directoriesbufferconfiguration.aspx).</span></span> <span data-ttu-id="c8e3b-216">Zobacz [magazynu i widoku danych diagnostycznych w usłudze Azure Storage](https://msdn.microsoft.com/library/azure/hh411534.aspx) omówienie konfigurowania konta magazynu tooa danych tootransfer hello Diagnostyka agenta.</span><span class="sxs-lookup"><span data-stu-id="c8e3b-216">See [Store and View Diagnostic Data in Azure Storage](https://msdn.microsoft.com/library/azure/hh411534.aspx) for an overview of setting up hello diagnostics agent tootransfer data tooa storage account.</span></span>

<span data-ttu-id="c8e3b-217">Każde wystąpienie licznika wydajności skonfigurowany jest rejestrowana w określonym próbkowania i hello pobrane dane są przesyłane toohello konta magazynu przez żądanie transferu zaplanowanego lub żądanie transferu na żądanie.</span><span class="sxs-lookup"><span data-stu-id="c8e3b-217">Each configured performance counter instance is recorded at a specified sampling rate, and hello sampled data is transferred toohello storage account either by a scheduled transfer request or an on-demand transfer request.</span></span> <span data-ttu-id="c8e3b-218">Przeniesienia automatyczne może zostać zaplanowane tak często, jak jeden raz na minutę.</span><span class="sxs-lookup"><span data-stu-id="c8e3b-218">Automatic transfers may be scheduled as often as once per minute.</span></span> <span data-ttu-id="c8e3b-219">Dane licznika wydajności przekazywane przez agenta diagnostyki hello są przechowywane w tabeli, WADPerformanceCountersTable, hello konta magazynu.</span><span class="sxs-lookup"><span data-stu-id="c8e3b-219">Performance counter data transferred by hello diagnostics agent is stored in a table, WADPerformanceCountersTable, in hello storage account.</span></span> <span data-ttu-id="c8e3b-220">Ta tabela może uzyskać dostępu do i wykonać zapytania z metody interfejsu API magazynu Azure w warstwie standardowa.</span><span class="sxs-lookup"><span data-stu-id="c8e3b-220">This table may be accessed and queried with standard Azure storage API methods.</span></span> <span data-ttu-id="c8e3b-221">Zobacz [przykład liczniki wydajności programu Microsoft Azure](http://code.msdn.microsoft.com/Windows-Azure-PerformanceCo-7d80ebf9) przykład kwerend i wyświetlanie danych licznika wydajności z hello WADPerformanceCountersTable tabeli.</span><span class="sxs-lookup"><span data-stu-id="c8e3b-221">See [Microsoft Azure PerformanceCounters Sample](http://code.msdn.microsoft.com/Windows-Azure-PerformanceCo-7d80ebf9) for an example of querying and displaying performance counter data from hello WADPerformanceCountersTable table.</span></span>

> [!NOTE]
> <span data-ttu-id="c8e3b-222">W zależności od hello Diagnostyka agenta transferu częstotliwość i czas oczekiwania w kolejce hello najnowsze dane liczników wydajności na koncie magazynu hello może potrwać kilka minut nieaktualny.</span><span class="sxs-lookup"><span data-stu-id="c8e3b-222">Depending on hello diagnostics agent transfer frequency and queue latency, hello most recent performance counter data in hello storage account may be several minutes out of date.</span></span>
>
>

## <a name="enable-performance-counters-using-diagnostics-configuration-file"></a><span data-ttu-id="c8e3b-223">Włącz użycie pliku konfiguracji diagnostyki liczniki wydajności</span><span class="sxs-lookup"><span data-stu-id="c8e3b-223">Enable performance counters using diagnostics configuration file</span></span>
<span data-ttu-id="c8e3b-224">Użyj hello następujące liczniki wydajności tooenable procedury w aplikacji platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="c8e3b-224">Use hello following procedure tooenable performance counters in your Azure application.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c8e3b-225">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="c8e3b-225">Prerequisites</span></span>
<span data-ttu-id="c8e3b-226">W tej sekcji założono, że zaimportowane hello monitor diagnostyki aplikacji i dodać hello diagnostyki konfiguracji pliku tooyour rozwiązania Visual Studio (diagnostics.wadcfg w 2.4 zestawu SDK i poniżej lub diagnostics.wadcfgx w zestawie SDK, 2.5 lub nowszym).</span><span class="sxs-lookup"><span data-stu-id="c8e3b-226">This section assumes that you have imported hello Diagnostics monitor into your application and added hello diagnostics configuration file tooyour Visual Studio solution (diagnostics.wadcfg in SDK 2.4 and below or diagnostics.wadcfgx in SDK 2.5 and above).</span></span> <span data-ttu-id="c8e3b-227">Zobacz kroki 1 i 2 w [Włączanie diagnostyki w usług Azure Cloud Services i maszyn wirtualnych](cloud-services-dotnet-diagnostics.md)) Aby uzyskać więcej informacji.</span><span class="sxs-lookup"><span data-stu-id="c8e3b-227">See steps 1 and 2 in [Enabling Diagnostics in Azure Cloud Services and Virtual Machines](cloud-services-dotnet-diagnostics.md)) for more information.</span></span>

## <a name="step-1-collect-and-store-data-from-performance-counters"></a><span data-ttu-id="c8e3b-228">Krok 1: Zbieranie i przechowywanie danych z liczników wydajności</span><span class="sxs-lookup"><span data-stu-id="c8e3b-228">Step 1: Collect and store data from performance counters</span></span>
<span data-ttu-id="c8e3b-229">Po dodaniu diagnostyki hello plików rozwiązania Visual Studio tooyour hello zbieranie i przechowywanie danych licznika wydajności można skonfigurować w aplikacji Azure.</span><span class="sxs-lookup"><span data-stu-id="c8e3b-229">After you have added hello diagnostics file tooyour Visual Studio solution, you can configure hello collection and storage of performance counter data in an Azure application.</span></span> <span data-ttu-id="c8e3b-230">Jest to realizowane przez dodanie pliku diagnostyki toohello liczników wydajności.</span><span class="sxs-lookup"><span data-stu-id="c8e3b-230">This is done by adding performance counters toohello diagnostics file.</span></span> <span data-ttu-id="c8e3b-231">W wystąpieniu hello najpierw zbieranych danych diagnostycznych, łącznie z liczników wydajności.</span><span class="sxs-lookup"><span data-stu-id="c8e3b-231">Diagnostics data, including performance counters, is first collected on hello instance.</span></span> <span data-ttu-id="c8e3b-232">Hello dane są następnie utrwalonego toohello WADPerformanceCountersTable tabeli w hello usługi tabel Azure, więc będzie również konieczne toospecify hello konta magazynu w aplikacji.</span><span class="sxs-lookup"><span data-stu-id="c8e3b-232">hello data is then persisted toohello WADPerformanceCountersTable table in hello Azure Table service, so you will also need toospecify hello storage account in your application.</span></span> <span data-ttu-id="c8e3b-233">Jeśli testujesz aplikację w lokalnie w hello obliczeniowe emulatora, można również przechowywać dane diagnostyczne lokalnie w hello emulatora magazynu.</span><span class="sxs-lookup"><span data-stu-id="c8e3b-233">If you're testing your application locally in hello Compute Emulator, you can also store diagnostics data locally in hello Storage Emulator.</span></span> <span data-ttu-id="c8e3b-234">Przed zapisaniem danych diagnostycznych, należy najpierw przejść toohello [portalu Azure](http://portal.azure.com/) i Utwórz konto magazynu klasycznego.</span><span class="sxs-lookup"><span data-stu-id="c8e3b-234">Before you store diagnostics data, you must first go toohello [Azure portal](http://portal.azure.com/) and create a classic storage account.</span></span> <span data-ttu-id="c8e3b-235">Najlepszym rozwiązaniem jest toolocate konta magazynu w hello tej samej lokalizacji geograficznej jako aplikacji platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="c8e3b-235">A best practice is toolocate your storage account in hello same geo-location as your Azure application.</span></span> <span data-ttu-id="c8e3b-236">Przy zachowaniu hello Azure aplikacji i konto magazynu są w hello tej samej lokalizacji geograficznej, uniknąć kosztów przepustowości zewnętrznych płatności i zmniejszenia opóźnień.</span><span class="sxs-lookup"><span data-stu-id="c8e3b-236">By keeping hello Azure application and storage account are in hello same geo-location, you avoid paying external bandwidth costs and reduce latency.</span></span>

### <a name="add-performance-counters-toohello-diagnostics-file"></a><span data-ttu-id="c8e3b-237">Dodaj plik diagnostyki toohello liczników wydajności</span><span class="sxs-lookup"><span data-stu-id="c8e3b-237">Add performance counters toohello diagnostics file</span></span>
<span data-ttu-id="c8e3b-238">Istnieje wiele liczników, których można użyć.</span><span class="sxs-lookup"><span data-stu-id="c8e3b-238">There are many counters you can use.</span></span> <span data-ttu-id="c8e3b-239">Witaj poniższym przykładzie pokazano kilka liczniki wydajności, które są zalecane sieci web i monitorowania roli procesu roboczego.</span><span class="sxs-lookup"><span data-stu-id="c8e3b-239">hello following example shows several performance counters that are recommended for web and worker role monitoring.</span></span>

<span data-ttu-id="c8e3b-240">Otwórz plik diagnostyki hello (diagnostics.wadcfg w 2.4 zestawu SDK i poniżej lub diagnostics.wadcfgx w zestawie SDK, 2.5 lub nowszym) i Dodaj hello następującego elementu DiagnosticMonitorConfiguration toohello:</span><span class="sxs-lookup"><span data-stu-id="c8e3b-240">Open hello diagnostics file (diagnostics.wadcfg in SDK 2.4 and below or diagnostics.wadcfgx in SDK 2.5 and above) and add hello following toohello DiagnosticMonitorConfiguration element:</span></span>

```xml
<PerformanceCounters bufferQuotaInMB="0" scheduledTransferPeriod="PT30M">
    <PerformanceCounterConfiguration counterSpecifier="\Memory\Available Bytes" sampleRate="PT30S" />
    <PerformanceCounterConfiguration counterSpecifier="\Processor(_Total)\% Processor Time" sampleRate="PT30S" />

    <!-- Use hello Process(w3wp) category counters in a web role -->

    <PerformanceCounterConfiguration counterSpecifier="\Process(w3wp)\% Processor Time" sampleRate="PT30S" />
    <PerformanceCounterConfiguration counterSpecifier="\Process(w3wp)\Private Bytes" sampleRate="PT30S" />
    <PerformanceCounterConfiguration counterSpecifier="\Process(w3wp)\Thread Count" sampleRate="PT30S" />

    <!-- Use hello Process(WaWorkerHost) category counters in a worker role.
        <PerformanceCounterConfiguration counterSpecifier="\Process(WaWorkerHost)\% Processor Time" sampleRate="PT30S" />
        <PerformanceCounterConfiguration counterSpecifier="\Process(WaWorkerHost)\Private Bytes" sampleRate="PT30S" />
        <PerformanceCounterConfiguration counterSpecifier="\Process(WaWorkerHost)\Thread Count" sampleRate="PT30S" />
    -->

    <PerformanceCounterConfiguration counterSpecifier="\.NET CLR Interop(_Global_)\# of marshalling" sampleRate="PT30S" />
    <PerformanceCounterConfiguration counterSpecifier="\.NET CLR Loading(_Global_)\% Time Loading" sampleRate="PT30S" />
    <PerformanceCounterConfiguration counterSpecifier="\.NET CLR LocksAndThreads(_Global_)\Contention Rate / sec" sampleRate="PT30S" />
    <PerformanceCounterConfiguration counterSpecifier="\.NET CLR Memory(_Global_)\# Bytes in all Heaps" sampleRate="PT30S" />
    <PerformanceCounterConfiguration counterSpecifier="\.NET CLR Networking(_Global_)\Connections Established" sampleRate="PT30S" />
    <PerformanceCounterConfiguration counterSpecifier="\.NET CLR Remoting(_Global_)\Remote Calls/sec" sampleRate="PT30S" />
    <PerformanceCounterConfiguration counterSpecifier="\.NET CLR Jit(_Global_)\% Time in Jit" sampleRate="PT30S" />
</PerformanceCounters>
```

<span data-ttu-id="c8e3b-241">Atrybut bufferQuotaInMB Hello, który określa hello maksymalną ilość pamięci systemu plików, która jest dostępna dla typu kolekcji danych hello (Azure dzienniki, dzienniki programu IIS, itp.).</span><span class="sxs-lookup"><span data-stu-id="c8e3b-241">hello bufferQuotaInMB attribute, which specifies hello maximum amount of file system storage that is available for hello data collection type (Azure logs, IIS logs, etc.).</span></span> <span data-ttu-id="c8e3b-242">Witaj domyślna to 0.</span><span class="sxs-lookup"><span data-stu-id="c8e3b-242">hello default is 0.</span></span> <span data-ttu-id="c8e3b-243">Zostanie osiągnięty przydział hello, hello najstarsze dane są usuwane po dodaniu nowych danych.</span><span class="sxs-lookup"><span data-stu-id="c8e3b-243">When hello quota is reached, hello oldest data is deleted as new data is added.</span></span> <span data-ttu-id="c8e3b-244">Witaj sumę wszystkich właściwości bufferQuotaInMB hello musi być większa niż wartość hello hello OverallQuotaInMB atrybutu.</span><span class="sxs-lookup"><span data-stu-id="c8e3b-244">hello sum of all hello bufferQuotaInMB properties must be greater than hello value of hello OverallQuotaInMB attribute.</span></span> <span data-ttu-id="c8e3b-245">Bardziej szczegółowe omówienie określania, ile miejsca do magazynowania jest wymagana w przypadku hello zbierania danych diagnostycznych, zobacz hello sekcji konfiguracji WAD [Rozwiązywanie problemów z najlepszych rozwiązań dotyczących tworzenia aplikacji Azure](https://msdn.microsoft.com/library/windowsazure/hh771389.aspx).</span><span class="sxs-lookup"><span data-stu-id="c8e3b-245">For a more detailed discussion of determining how much storage will be required for hello collection of diagnostics data, see hello Setup WAD section of [Troubleshooting Best Practices for Developing Azure Applications](https://msdn.microsoft.com/library/windowsazure/hh771389.aspx).</span></span>

<span data-ttu-id="c8e3b-246">Witaj scheduledTransferPeriod atrybut, który określa interwał powitania między zaplanowane transferów danych, zaokrąglona w górę toohello najbliższej minutę.</span><span class="sxs-lookup"><span data-stu-id="c8e3b-246">hello scheduledTransferPeriod attribute, which specifies hello interval between scheduled transfers of data, rounded up toohello nearest minute.</span></span> <span data-ttu-id="c8e3b-247">W hello następujące przykłady jest ustawiona tooPT30M (30 minut).</span><span class="sxs-lookup"><span data-stu-id="c8e3b-247">In hello following examples, it is set tooPT30M (30 minutes).</span></span> <span data-ttu-id="c8e3b-248">Ustawienie hello transfer okresu tooa mała wartość, na przykład 1 minutę, obniży wydajności aplikacji w środowisku produkcyjnym, ale może być przydatne przy przeglądaniu diagnostyki Postaramy się szybko podczas testowania.</span><span class="sxs-lookup"><span data-stu-id="c8e3b-248">Setting hello transfer period tooa small value, such as 1 minute, will adversely impact your application's performance in production but can be useful for seeing diagnostics working quickly when you are testing.</span></span> <span data-ttu-id="c8e3b-249">okres zaplanowanego transferu Hello powinien być duże tooensure danych diagnostycznych nie jest zastąpione na powitania wystąpienia, ale wystarczająco duży, że nie ma wpływu hello wydajność aplikacji.</span><span class="sxs-lookup"><span data-stu-id="c8e3b-249">hello scheduled transfer period should be small enough tooensure that diagnostic data is not overwritten on hello instance, but large enough that it will not impact hello performance of your application.</span></span>

<span data-ttu-id="c8e3b-250">Atrybut counterSpecifier Hello określa toocollect licznika wydajności hello.</span><span class="sxs-lookup"><span data-stu-id="c8e3b-250">hello counterSpecifier attribute specifies hello performance counter toocollect.</span></span> <span data-ttu-id="c8e3b-251">Atrybut sampleRate Hello określa szybkość hello, w którym licznik wydajności hello powinny być pobrane, w tym przypadku 30 sekund.</span><span class="sxs-lookup"><span data-stu-id="c8e3b-251">hello sampleRate attribute specifies hello rate at which hello performance counter should be sampled, in this case 30 seconds.</span></span>

<span data-ttu-id="c8e3b-252">Po dodaniu się, że liczniki wydajności hello, które mają toocollect zapisać zmiany toohello diagnostyki.</span><span class="sxs-lookup"><span data-stu-id="c8e3b-252">Once you've added hello performance counters that you want toocollect, save your changes toohello diagnostics file.</span></span> <span data-ttu-id="c8e3b-253">Następnie należy konto magazynu hello toospecify zostaną utrwalone hello danych diagnostycznych.</span><span class="sxs-lookup"><span data-stu-id="c8e3b-253">Next, you need toospecify hello storage account that hello diagnostics data will be persisted to.</span></span>

### <a name="specify-hello-storage-account"></a><span data-ttu-id="c8e3b-254">Określ konto magazynu hello</span><span class="sxs-lookup"><span data-stu-id="c8e3b-254">Specify hello storage account</span></span>
<span data-ttu-id="c8e3b-255">toopersist konta użytkownika tooyour informacji diagnostyki Azure Storage, należy określić parametry połączenia w pliku konfiguracyjnym (pliku ServiceConfiguration.cscfg) usługi.</span><span class="sxs-lookup"><span data-stu-id="c8e3b-255">toopersist your diagnostics information tooyour Azure Storage account, you must specify a connection string in your service configuration (ServiceConfiguration.cscfg) file.</span></span>

<span data-ttu-id="c8e3b-256">Dla 2.5 zestawu SDK platformy Azure można określić w pliku diagnostics.wadcfgx hello hello konta magazynu.</span><span class="sxs-lookup"><span data-stu-id="c8e3b-256">For Azure SDK 2.5, hello Storage Account can be specified in hello diagnostics.wadcfgx file.</span></span>

> [!NOTE]
> <span data-ttu-id="c8e3b-257">Te instrukcje mają zastosowanie tylko tooAzure 2.4 zestawu SDK i poniżej.</span><span class="sxs-lookup"><span data-stu-id="c8e3b-257">These instructions only apply tooAzure SDK 2.4 and below.</span></span> <span data-ttu-id="c8e3b-258">Dla 2.5 zestawu SDK platformy Azure można określić w pliku diagnostics.wadcfgx hello hello konta magazynu.</span><span class="sxs-lookup"><span data-stu-id="c8e3b-258">For Azure SDK 2.5, hello Storage Account can be specified in hello diagnostics.wadcfgx file.</span></span>
>
>

<span data-ttu-id="c8e3b-259">Parametry połączenia hello tooset:</span><span class="sxs-lookup"><span data-stu-id="c8e3b-259">tooset hello connection strings:</span></span>

1. <span data-ttu-id="c8e3b-260">Otwórz plik ServiceConfiguration.Cloud.cscfg hello przy użyciu ulubionym edytorze tekstów i parametry połączenia hello zestaw magazynu.</span><span class="sxs-lookup"><span data-stu-id="c8e3b-260">Open hello ServiceConfiguration.Cloud.cscfg file using your favorite text editor and set hello connection string for your storage.</span></span> <span data-ttu-id="c8e3b-261">Witaj *AccountName* i *AccountKey* wartości znajdują się w hello portalu Azure w hello konta pulpitu nawigacyjnego magazynu, w obszarze klucze dostępu.</span><span class="sxs-lookup"><span data-stu-id="c8e3b-261">hello *AccountName* and *AccountKey* values are found in hello Azure portal in hello storage account dashboard, under Access keys.</span></span>

    ```xml
    <ConfigurationSettings>
      <Setting name="Microsoft.WindowsAzure.Plugins.Diagnostics.ConnectionString" value="DefaultEndpointsProtocol=https;AccountName=<name>;AccountKey=<key>"/>
    </ConfigurationSettings>
    ```
2. <span data-ttu-id="c8e3b-262">Zapisz plik ServiceConfiguration.Cloud.cscfg hello.</span><span class="sxs-lookup"><span data-stu-id="c8e3b-262">Save hello ServiceConfiguration.Cloud.cscfg file.</span></span>
3. <span data-ttu-id="c8e3b-263">Otwórz plik ServiceConfiguration.Local.cscfg hello i sprawdź, czy UseDevelopmentStorage jest ustawiony tootrue.</span><span class="sxs-lookup"><span data-stu-id="c8e3b-263">Open hello ServiceConfiguration.Local.cscfg file and verify that UseDevelopmentStorage is set tootrue.</span></span>

    ```xml
    <ConfigurationSettings>
      <Settingname="Microsoft.WindowsAzure.Plugins.Diagnostics.ConnectionString" value="UseDevelopmentStorage=true"/>
    </ConfigurationSettings>
    ```
   <span data-ttu-id="c8e3b-264">Teraz, gdy parametry połączenia hello są ustawione, aplikacji zachować konta magazynu tooyour danych diagnostycznych, po wdrożeniu aplikacji.</span><span class="sxs-lookup"><span data-stu-id="c8e3b-264">Now that hello connection strings are set, your application will persist diagnostics data tooyour storage account when your application is deployed.</span></span>
4. <span data-ttu-id="c8e3b-265">Zapisz i skompilowanie projektu, a następnie wdrożyć aplikację.</span><span class="sxs-lookup"><span data-stu-id="c8e3b-265">Save and build your project, then deploy your application.</span></span>

## <a name="step-2-optional-create-custom-performance-counters"></a><span data-ttu-id="c8e3b-266">Krok 2: (Opcjonalnie) Utwórz niestandardowe liczniki wydajności</span><span class="sxs-lookup"><span data-stu-id="c8e3b-266">Step 2: (Optional) Create custom performance counters</span></span>
<span data-ttu-id="c8e3b-267">Ponadto toohello wstępnie zdefiniowana liczniki wydajności, można dodawać role sieci web lub procesu roboczego toomonitor liczników wydajności niestandardowych.</span><span class="sxs-lookup"><span data-stu-id="c8e3b-267">In addition toohello pre-defined performance counters, you can add your own custom performance counters toomonitor web or worker roles.</span></span> <span data-ttu-id="c8e3b-268">Niestandardowe liczniki wydajności mogą być używane tootrack i monitorowanie zachowania specyficzne dla aplikacji i można utworzyć lub usunąć zadanie uruchamiania, rola sieci web lub roli proces roboczy z podwyższonym poziomem uprawnień.</span><span class="sxs-lookup"><span data-stu-id="c8e3b-268">Custom performance counters may be used tootrack and monitor application-specific behavior and can be created or deleted in a startup task, web role, or worker role with elevated permissions.</span></span>

<span data-ttu-id="c8e3b-269">agent Azure diagnostics Hello odświeża hello konfigurację liczników wydajności z pliku .wadcfg hello minutę po uruchomieniu.</span><span class="sxs-lookup"><span data-stu-id="c8e3b-269">hello Azure diagnostics agent refreshes hello performance counter configuration from hello .wadcfg file one minute after starting.</span></span>  <span data-ttu-id="c8e3b-270">Utwórz niestandardowe liczniki wydajności w hello — metoda OnStart, uruchamiania zadań trwać dłużej niż minutę tooexecute Twoje niestandardowe liczniki wydajności będą nie została utworzona podczas agenta diagnostyki Azure hello tooload je.</span><span class="sxs-lookup"><span data-stu-id="c8e3b-270">If you create custom performance counters in hello OnStart method and your startup tasks take longer than one minute tooexecute, your custom performance counters will not have been created when hello Azure Diagnostics agent tries tooload them.</span></span>  <span data-ttu-id="c8e3b-271">W tym scenariuszu zobaczysz, że diagnostyki Azure poprawnie przechwytuje wszystkie dane diagnostyczne, z wyjątkiem Twojego niestandardowe liczniki wydajności.</span><span class="sxs-lookup"><span data-stu-id="c8e3b-271">In this scenario, you will see that Azure Diagnostics correctly captures all diagnostics data except your custom performance counters.</span></span>  <span data-ttu-id="c8e3b-272">tooresolve ten problem, Utwórz hello liczników wydajności w zadanie uruchamiania lub Przenieś niektóre zadania uruchamiania działają — metoda OnStart toohello po utworzeniu hello liczników wydajności.</span><span class="sxs-lookup"><span data-stu-id="c8e3b-272">tooresolve this issue, create hello performance counters in a startup task or move some of your startup task work toohello OnStart method after creating hello performance counters.</span></span>

<span data-ttu-id="c8e3b-273">Wykonaj następujące kroki toocreate proste wydajności niestandardowych licznik o nazwie "\MyCustomCounterCategory\MyButton1Counter" hello:</span><span class="sxs-lookup"><span data-stu-id="c8e3b-273">Perform hello following steps toocreate a simple custom performance counter named "\MyCustomCounterCategory\MyButton1Counter":</span></span>

1. <span data-ttu-id="c8e3b-274">Otwórz plik definicji usługi hello (CSDEF) dla aplikacji.</span><span class="sxs-lookup"><span data-stu-id="c8e3b-274">Open hello service definition file (CSDEF) for your application.</span></span>
2. <span data-ttu-id="c8e3b-275">Dodaj hello środowiska uruchomieniowego element toohello sieć Web lub proces roboczy elementu tooallow wykonywania z podwyższonym poziomem uprawnień:</span><span class="sxs-lookup"><span data-stu-id="c8e3b-275">Add hello Runtime element toohello WebRole or WorkerRole element tooallow execution with elevated privileges:</span></span>

    ```xml
    <runtime executioncontext="elevated"/>
    ```
3. <span data-ttu-id="c8e3b-276">Zapisz plik hello.</span><span class="sxs-lookup"><span data-stu-id="c8e3b-276">Save hello file.</span></span>
4. <span data-ttu-id="c8e3b-277">Otwórz plik diagnostyki hello (diagnostics.wadcfg w 2.4 zestawu SDK i poniżej lub diagnostics.wadcfgx w zestawie SDK, 2.5 lub nowszym) i dodaj następujące toohello DiagnosticMonitorConfiguration hello</span><span class="sxs-lookup"><span data-stu-id="c8e3b-277">Open hello diagnostics file (diagnostics.wadcfg in SDK 2.4 and below or diagnostics.wadcfgx in SDK 2.5 and above) and add hello following toohello DiagnosticMonitorConfiguration</span></span>

    ```xml
    <PerformanceCounters bufferQuotaInMB="0" scheduledTransferPeriod="PT30M">
      <PerformanceCounterConfiguration counterSpecifier="\MyCustomCounterCategory\MyButton1Counter" sampleRate="PT30S"/>
    </PerformanceCounters>
    ```
5. <span data-ttu-id="c8e3b-278">Zapisz plik hello.</span><span class="sxs-lookup"><span data-stu-id="c8e3b-278">Save hello file.</span></span>
6. <span data-ttu-id="c8e3b-279">Utwórz kategorii licznika wydajności niestandardowych hello w — metoda OnStart hello swojej roli przed wywołaniem base. OnStart.</span><span class="sxs-lookup"><span data-stu-id="c8e3b-279">Create hello custom performance counter category in hello OnStart method of your role, before invoking base.OnStart.</span></span> <span data-ttu-id="c8e3b-280">Witaj poniższy przykład C# tworzy kategorię niestandardową, jeśli jeszcze nie istnieje:</span><span class="sxs-lookup"><span data-stu-id="c8e3b-280">hello following C# example creates a custom category, if it does not already exist:</span></span>

    ```csharp
    public override bool OnStart()
    {
      if (!PerformanceCounterCategory.Exists("MyCustomCounterCategory"))
      {
         CounterCreationDataCollection counterCollection = new CounterCreationDataCollection();

         // add a counter tracking user button1 clicks
         CounterCreationData operationTotal1 = new CounterCreationData();
         operationTotal1.CounterName = "MyButton1Counter";
         operationTotal1.CounterHelp = "My Custom Counter for Button1";
         operationTotal1.CounterType = PerformanceCounterType.NumberOfItems32;
         counterCollection.Add(operationTotal1);

         PerformanceCounterCategory.Create(
           "MyCustomCounterCategory",
           "My Custom Counter Category",
           PerformanceCounterCategoryType.SingleInstance, counterCollection);

         Trace.WriteLine("Custom counter category created.");
      }
      else {
        Trace.WriteLine("Custom counter category already exists.");
      }

    return base.OnStart();
    }
    ```
7. <span data-ttu-id="c8e3b-281">Aktualizuj liczniki hello w aplikacji.</span><span class="sxs-lookup"><span data-stu-id="c8e3b-281">Update hello counters within your application.</span></span> <span data-ttu-id="c8e3b-282">Poniższy przykład Hello aktualizacje licznika wydajności niestandardowych zdarzeń Button1_Click:</span><span class="sxs-lookup"><span data-stu-id="c8e3b-282">hello following example updates a custom performance counter on Button1_Click events:</span></span>

    ```csharp
    protected void Button1_Click(object sender, EventArgs e)
    {
      PerformanceCounter button1Counter = new PerformanceCounter(
        "MyCustomCounterCategory",
        "MyButton1Counter",
        string.Empty,
        false);
      button1Counter.Increment();
      this.Button1.Text = "Button 1 count: " +
        button1Counter.RawValue.ToString();
    }
    ```
8. <span data-ttu-id="c8e3b-283">Zapisz plik hello.</span><span class="sxs-lookup"><span data-stu-id="c8e3b-283">Save hello file.</span></span>  

<span data-ttu-id="c8e3b-284">Dane licznika wydajności niestandardowych teraz zostaną zebrane przez monitor diagnostyki Azure hello.</span><span class="sxs-lookup"><span data-stu-id="c8e3b-284">Custom performance counter data will now be collected by hello Azure diagnostics monitor.</span></span>

## <a name="step-3-query-performance-counter-data"></a><span data-ttu-id="c8e3b-285">Krok 3: Wykonywanie zapytań danych licznika wydajności</span><span class="sxs-lookup"><span data-stu-id="c8e3b-285">Step 3: Query performance counter data</span></span>
<span data-ttu-id="c8e3b-286">Po wdrożeniu aplikacji i uruchomiona, monitor diagnostyki hello rozpocznie się zbierania liczników wydajności i przechowywanie tego tooAzure pamięci masowej.</span><span class="sxs-lookup"><span data-stu-id="c8e3b-286">Once your application is deployed and running, hello Diagnostics monitor will begin collecting performance counters and persisting that data tooAzure storage.</span></span> <span data-ttu-id="c8e3b-287">Użyj narzędzi takich jak Eksplorator serwera w programie Visual Studio, [Eksploratora usługi Storage Azure](http://azurestorageexplorer.codeplex.com/), lub [Menedżera diagnostyki Azure](http://www.cerebrata.com/Products/AzureDiagnosticsManager/Default.aspx) przez Cerebrata danych w hello liczniki wydajności hello tooview Tabela WADPerformanceCountersTable.</span><span class="sxs-lookup"><span data-stu-id="c8e3b-287">You use tools such as Server Explorer in Visual Studio,  [Azure Storage Explorer](http://azurestorageexplorer.codeplex.com/), or [Azure Diagnostics Manager](http://www.cerebrata.com/Products/AzureDiagnosticsManager/Default.aspx) by Cerebrata tooview hello performance counters data in hello WADPerformanceCountersTable table.</span></span> <span data-ttu-id="c8e3b-288">Można również programowo zapytania przy użyciu usługi tabeli hello [C#](../cosmos-db/table-storage-how-to-use-dotnet.md), [Java](../cosmos-db/table-storage-how-to-use-java.md), [Node.js](../cosmos-db/table-storage-how-to-use-nodejs.md), [Python](../cosmos-db/table-storage-how-to-use-python.md), [Ruby](../cosmos-db/table-storage-how-to-use-ruby.md), lub [PHP](../cosmos-db/table-storage-how-to-use-php.md).</span><span class="sxs-lookup"><span data-stu-id="c8e3b-288">You can also programmatically query hello Table service using [C#](../cosmos-db/table-storage-how-to-use-dotnet.md),  [Java](../cosmos-db/table-storage-how-to-use-java.md),  [Node.js](../cosmos-db/table-storage-how-to-use-nodejs.md), [Python](../cosmos-db/table-storage-how-to-use-python.md), [Ruby](../cosmos-db/table-storage-how-to-use-ruby.md), or [PHP](../cosmos-db/table-storage-how-to-use-php.md).</span></span>

<span data-ttu-id="c8e3b-289">Hello poniższy przykład C# zawiera podstawowe zapytanie tabeli WADPerformanceCountersTable hello i zapisuje plik CSV tooa hello diagnostyki danych.</span><span class="sxs-lookup"><span data-stu-id="c8e3b-289">hello following C# example shows a basic query against hello WADPerformanceCountersTable table and saves hello diagnostics data tooa CSV file.</span></span> <span data-ttu-id="c8e3b-290">Po hello liczniki wydajności zostaną zapisane w pliku CSV tooa, można użyć hello Tworzenie wykresów możliwości programu Microsoft Excel lub pewne inne narzędzie toovisualize hello dane.</span><span class="sxs-lookup"><span data-stu-id="c8e3b-290">Once hello performance counters are saved tooa CSV file, you can use hello graphing capabilities in Microsoft Excel or some other tool toovisualize hello data.</span></span> <span data-ttu-id="c8e3b-291">Należy się tooadd tooMicrosoft.WindowsAzure.Storage.dll odwołania, który jest dostępny w hello Azure SDK dla platformy .NET października 2012 lub nowszy.</span><span class="sxs-lookup"><span data-stu-id="c8e3b-291">Be sure tooadd a reference tooMicrosoft.WindowsAzure.Storage.dll, which is included in hello Azure SDK for .NET October 2012 and later.</span></span> <span data-ttu-id="c8e3b-292">zestaw Hello jest zainstalowana toohello % Program Files%\Microsoft SDKs\Microsoft Azure.NET SDK\version-num\ref\ katalogu.</span><span class="sxs-lookup"><span data-stu-id="c8e3b-292">hello assembly is installed toohello %Program Files%\Microsoft SDKs\Microsoft Azure.NET SDK\version-num\ref\ directory.</span></span>

```csharp
using Microsoft.WindowsAzure.Storage;
using Microsoft.WindowsAzure.Storage.Auth;
using Microsoft.WindowsAzure.Storage.Table;
...

// Get hello connection string. When using Microsoft Azure Cloud Services, it is recommended
// you store your connection string using hello Microsoft Azure service configuration
// system (*.csdef and *.cscfg files). You can you use hello CloudConfigurationManager type
// tooretrieve your storage connection string.  If you're not using Cloud Services, it's
// recommended that you store hello connection string in your web.config or app.config file.
// Use hello ConfigurationManager type tooretrieve your storage connection string.

string connectionString = Microsoft.WindowsAzure.CloudConfigurationManager.GetSetting("StorageConnectionString");
//string connectionString = System.Configuration.ConfigurationManager.ConnectionStrings["StorageConnectionString"].ConnectionString;

// Get a reference toohello storage account using hello connection string.  You can also use hello development
// storage account (Storage Emulator) for local debugging.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(connectionString);
//CloudStorageAccount storageAccount = CloudStorageAccount.DevelopmentStorageAccount;

// Create hello table client.
CloudTableClient tableClient = storageAccount.CreateCloudTableClient();

// Create hello CloudTable object that represents hello "WADPerformanceCountersTable" table.
CloudTable table = tableClient.GetTableReference("WADPerformanceCountersTable");

// Create hello table query, filter on a specific CounterName, DeploymentId and RoleInstance.
TableQuery<PerformanceCountersEntity> query = new TableQuery<PerformanceCountersEntity>()
  .Where(
    TableQuery.CombineFilters(
      TableQuery.GenerateFilterCondition("CounterName", QueryComparisons.Equal, @"\Processor(_Total)\% Processor Time"),
      TableOperators.And,
      TableQuery.CombineFilters(
      TableQuery.GenerateFilterCondition("DeploymentId", QueryComparisons.Equal, "ec26b7a1720447e1bcdeefc41c4892a3"),
      TableOperators.And,
      TableQuery.GenerateFilterCondition("RoleInstance", QueryComparisons.Equal, "WebRole1_IN_0")
    )
  )
);

// Execute hello table query.
IEnumerable<PerformanceCountersEntity> result = table.ExecuteQuery(query);

// Process hello query results and build a CSV file.
StringBuilder sb = new StringBuilder("TimeStamp,EventTickCount,DeploymentId,Role,RoleInstance,CounterName,CounterValue\n");

foreach (PerformanceCountersEntity entity in result)
{
  sb.Append(entity.Timestamp + "," + entity.EventTickCount + "," + entity.DeploymentId + ","
    + entity.Role + "," + entity.RoleInstance + "," + entity.CounterName + "," + entity.CounterValue+"\n");
}

StreamWriter sw = File.CreateText(@"C:\temp\PerfCounters.csv");
sw.Write(sb.ToString());
sw.Close();
```

<span data-ttu-id="c8e3b-293">Jednostki są mapowane tooC # obiektów za pomocą niestandardowej klasy pochodzącej od **TableEntity**.</span><span class="sxs-lookup"><span data-stu-id="c8e3b-293">Entities map tooC# objects using a custom class derived from **TableEntity**.</span></span> <span data-ttu-id="c8e3b-294">Witaj poniższy kod definiuje klasę jednostki, która reprezentuje licznika wydajności w hello **WADPerformanceCountersTable** tabeli.</span><span class="sxs-lookup"><span data-stu-id="c8e3b-294">hello following code defines an entity class that represents a performance counter in hello **WADPerformanceCountersTable** table.</span></span>

```csharp
public class PerformanceCountersEntity : TableEntity
{
  public long EventTickCount { get; set; }
  public string DeploymentId { get; set; }
  public string Role { get; set; }
  public string RoleInstance { get; set; }
  public string CounterName { get; set; }
  public double CounterValue { get; set; }
}
```

## <a name="next-steps"></a><span data-ttu-id="c8e3b-295">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="c8e3b-295">Next Steps</span></span>
[<span data-ttu-id="c8e3b-296">Przeglądanie dodatkowych artykułów na diagnostyki Azure</span><span class="sxs-lookup"><span data-stu-id="c8e3b-296">View additional articles on Azure Diagnostics</span></span>](../azure-diagnostics.md)
