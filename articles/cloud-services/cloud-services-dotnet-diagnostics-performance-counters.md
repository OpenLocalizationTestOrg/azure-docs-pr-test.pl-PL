---
title: "Użyj liczników wydajności w diagnostyce Azure | Dokumentacja firmy Microsoft"
description: "Użyj liczników wydajności usługi w chmurze platformy Azure lub maszyny wirtualnej, aby znaleźć wąskich gardeł i dostrajania wydajności."
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
ms.openlocfilehash: 2cf765cb034725199127c547a9b8b997a4a6089c
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
# <a name="create-and-use-performance-counters-in-an-azure-application"></a><span data-ttu-id="8a9f5-103">Tworzenie i używanie liczników wydajności w aplikacji Azure</span><span class="sxs-lookup"><span data-stu-id="8a9f5-103">Create and use performance counters in an Azure application</span></span>
<span data-ttu-id="8a9f5-104">W tym artykule opisano zalet i jak poddane liczniki wydajności aplikacji platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="8a9f5-104">This article describes the benefits of and how to put performance counters into your Azure application.</span></span> <span data-ttu-id="8a9f5-105">Można używać ich do zbierania danych, Znajdź wąskich gardeł i dostrajania wydajności systemu i aplikacji.</span><span class="sxs-lookup"><span data-stu-id="8a9f5-105">You can use them to collect data, find bottlenecks, and tune system and application performance.</span></span>

<span data-ttu-id="8a9f5-106">Można również zebranych liczników wydajności dostępnych dla systemu Windows Server, IIS i platformy ASP.NET i używany w celu określenia kondycji role sieci web platformy Azure, roli proces roboczy i maszyny wirtualne.</span><span class="sxs-lookup"><span data-stu-id="8a9f5-106">Performance counters available for Windows Server, IIS, and ASP.NET can also be collected and used to determine the health of your Azure web roles, worker roles, and Virtual Machines.</span></span> <span data-ttu-id="8a9f5-107">Można również utworzyć i używać niestandardowe liczniki wydajności.</span><span class="sxs-lookup"><span data-stu-id="8a9f5-107">You can also create and use custom performance counters.</span></span>  

<span data-ttu-id="8a9f5-108">Należy zbadać dane licznika wydajności</span><span class="sxs-lookup"><span data-stu-id="8a9f5-108">You can examine performance counter data</span></span>

1. <span data-ttu-id="8a9f5-109">Bezpośrednio na hoście aplikacji za pomocą narzędzia Monitor wydajności dostęp za pomocą pulpitu zdalnego</span><span class="sxs-lookup"><span data-stu-id="8a9f5-109">Directly on the application host with the Performance Monitor tool accessed using Remote Desktop</span></span>
2. <span data-ttu-id="8a9f5-110">Za pomocą programu System Center Operations Manager przy użyciu pakietu administracyjnego platformy Azure</span><span class="sxs-lookup"><span data-stu-id="8a9f5-110">With System Center Operations Manager using the Azure Management Pack</span></span>
3. <span data-ttu-id="8a9f5-111">Przy użyciu innych narzędzi monitorowania, które uzyskują dostęp do danych diagnostycznych przekazywane do magazynu Azure.</span><span class="sxs-lookup"><span data-stu-id="8a9f5-111">With other monitoring tools that access the diagnostic data transferred to Azure storage.</span></span> <span data-ttu-id="8a9f5-112">Zobacz [magazynu i widoku danych diagnostycznych w usłudze Azure Storage](https://msdn.microsoft.com/library/azure/hh411534.aspx) Aby uzyskać więcej informacji.</span><span class="sxs-lookup"><span data-stu-id="8a9f5-112">See [Store and View Diagnostic Data in Azure Storage](https://msdn.microsoft.com/library/azure/hh411534.aspx) for more information.</span></span>  

<span data-ttu-id="8a9f5-113">Aby uzyskać więcej informacji na temat monitorowania wydajności aplikacji w [portalu Azure](http://portal.azure.com/), zobacz [jak usługi w chmurze Monitor](https://www.azure.com/manage/services/cloud-services/how-to-monitor-a-cloud-service/).</span><span class="sxs-lookup"><span data-stu-id="8a9f5-113">For more information on monitoring the performance of your application in the [Azure portal](http://portal.azure.com/), see [How to Monitor Cloud Services](https://www.azure.com/manage/services/cloud-services/how-to-monitor-a-cloud-service/).</span></span>

<span data-ttu-id="8a9f5-114">Aby uzyskać dodatkowe szczegółowe wskazówki dotyczące tworzenia rejestrowania i śledzenia strategii i przy użyciu diagnostyki i innych technik rozwiązywania problemów i optymalizowanie aplikacji Azure, zobacz [Rozwiązywanie problemów z najlepszych rozwiązań dotyczących tworzenia Azure Aplikacje](https://msdn.microsoft.com/library/azure/hh771389.aspx).</span><span class="sxs-lookup"><span data-stu-id="8a9f5-114">For additional in-depth guidance on creating a logging and tracing strategy and using diagnostics and other techniques to troubleshoot problems and optimize Azure applications, see [Troubleshooting Best Practices for Developing Azure Applications](https://msdn.microsoft.com/library/azure/hh771389.aspx).</span></span>

## <a name="enable-performance-counter-monitoring"></a><span data-ttu-id="8a9f5-115">Aby włączyć monitorowanie licznika wydajności</span><span class="sxs-lookup"><span data-stu-id="8a9f5-115">Enable performance counter monitoring</span></span>
<span data-ttu-id="8a9f5-116">Liczniki wydajności nie są domyślnie włączone.</span><span class="sxs-lookup"><span data-stu-id="8a9f5-116">Performance counters are not enabled by default.</span></span> <span data-ttu-id="8a9f5-117">Aplikacja lub zadanie uruchamiania należy zmodyfikować domyślną konfigurację agenta diagnostyki uwzględnienie liczniki wydajności zależnych, które chcesz monitorować dla każdego wystąpienia roli.</span><span class="sxs-lookup"><span data-stu-id="8a9f5-117">Your application or a startup task must modify the default diagnostics agent configuration to include the specific performance counters that you wish to monitor for each role instance.</span></span>

### <a name="performance-counters-available-for-microsoft-azure"></a><span data-ttu-id="8a9f5-118">Liczniki wydajności dostępne platformy Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="8a9f5-118">Performance counters available for Microsoft Azure</span></span>
<span data-ttu-id="8a9f5-119">Platforma Azure udostępnia podzbioru dostępnych liczników wydajności dla systemu Windows Server, IIS i stosu ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="8a9f5-119">Azure provides a subset of the performance counters available for Windows Server, IIS and the ASP.NET stack.</span></span> <span data-ttu-id="8a9f5-120">W poniższej tabeli wymieniono niektóre liczniki wydajności szczególne znaczenie dla aplikacji platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="8a9f5-120">The following table lists some of the performance counters of particular interest for Azure applications.</span></span>

| <span data-ttu-id="8a9f5-121">Kategoria licznika: Obiektu (wystąpienia)</span><span class="sxs-lookup"><span data-stu-id="8a9f5-121">Counter Category: Object (Instance)</span></span> | <span data-ttu-id="8a9f5-122">Nazwa licznika</span><span class="sxs-lookup"><span data-stu-id="8a9f5-122">Counter Name</span></span> | <span data-ttu-id="8a9f5-123">Dokumentacja</span><span class="sxs-lookup"><span data-stu-id="8a9f5-123">Reference</span></span> |
| --- | --- | --- |
| <span data-ttu-id="8a9f5-124">Wyjątki środowiska CLR platformy .NET (*globalne*)</span><span class="sxs-lookup"><span data-stu-id="8a9f5-124">.NET CLR Exceptions(*Global*)</span></span> |<span data-ttu-id="8a9f5-125"># Clr\\liczba wyjątków / s</span><span class="sxs-lookup"><span data-stu-id="8a9f5-125"># Exceps Thrown / sec</span></span> |<span data-ttu-id="8a9f5-126">Liczniki wydajności wyjątku</span><span class="sxs-lookup"><span data-stu-id="8a9f5-126">Exception Performance Counters</span></span> |
| <span data-ttu-id="8a9f5-127">.NET CLR pamięci (*globalne*)</span><span class="sxs-lookup"><span data-stu-id="8a9f5-127">.NET CLR Memory(*Global*)</span></span> |<span data-ttu-id="8a9f5-128">% Czasu odzyskiwania pamięci</span><span class="sxs-lookup"><span data-stu-id="8a9f5-128">% Time in GC</span></span> |<span data-ttu-id="8a9f5-129">Liczniki wydajności pamięci</span><span class="sxs-lookup"><span data-stu-id="8a9f5-129">Memory Performance Counters</span></span> |
| <span data-ttu-id="8a9f5-130">ASP.NET</span><span class="sxs-lookup"><span data-stu-id="8a9f5-130">ASP.NET</span></span> |<span data-ttu-id="8a9f5-131">Aplikacja zostanie uruchomiona ponownie</span><span class="sxs-lookup"><span data-stu-id="8a9f5-131">Application Restarts</span></span> |<span data-ttu-id="8a9f5-132">Liczniki wydajności dla programu ASP.NET</span><span class="sxs-lookup"><span data-stu-id="8a9f5-132">Performance Counters for ASP.NET</span></span> |
| <span data-ttu-id="8a9f5-133">ASP.NET</span><span class="sxs-lookup"><span data-stu-id="8a9f5-133">ASP.NET</span></span> |<span data-ttu-id="8a9f5-134">Czas wykonania żądania</span><span class="sxs-lookup"><span data-stu-id="8a9f5-134">Request Execution Time</span></span> |<span data-ttu-id="8a9f5-135">Liczniki wydajności dla programu ASP.NET</span><span class="sxs-lookup"><span data-stu-id="8a9f5-135">Performance Counters for ASP.NET</span></span> |
| <span data-ttu-id="8a9f5-136">ASP.NET</span><span class="sxs-lookup"><span data-stu-id="8a9f5-136">ASP.NET</span></span> |<span data-ttu-id="8a9f5-137">Liczba żądań rozłączonych</span><span class="sxs-lookup"><span data-stu-id="8a9f5-137">Requests Disconnected</span></span> |<span data-ttu-id="8a9f5-138">Liczniki wydajności dla programu ASP.NET</span><span class="sxs-lookup"><span data-stu-id="8a9f5-138">Performance Counters for ASP.NET</span></span> |
| <span data-ttu-id="8a9f5-139">ASP.NET</span><span class="sxs-lookup"><span data-stu-id="8a9f5-139">ASP.NET</span></span> |<span data-ttu-id="8a9f5-140">Ponowne uruchomienie procesu roboczego</span><span class="sxs-lookup"><span data-stu-id="8a9f5-140">Worker Process Restarts</span></span> |<span data-ttu-id="8a9f5-141">Liczniki wydajności dla programu ASP.NET</span><span class="sxs-lookup"><span data-stu-id="8a9f5-141">Performance Counters for ASP.NET</span></span> |
| <span data-ttu-id="8a9f5-142">Aplikacji programu ASP.NET (**całkowita**)</span><span class="sxs-lookup"><span data-stu-id="8a9f5-142">ASP.NET Applications(**Total**)</span></span> |<span data-ttu-id="8a9f5-143">Całkowita liczba żądań</span><span class="sxs-lookup"><span data-stu-id="8a9f5-143">Requests Total</span></span> |<span data-ttu-id="8a9f5-144">Liczniki wydajności dla programu ASP.NET</span><span class="sxs-lookup"><span data-stu-id="8a9f5-144">Performance Counters for ASP.NET</span></span> |
| <span data-ttu-id="8a9f5-145">Aplikacji programu ASP.NET (**całkowita**)</span><span class="sxs-lookup"><span data-stu-id="8a9f5-145">ASP.NET Applications(**Total**)</span></span> |<span data-ttu-id="8a9f5-146">Żądania na sekundę</span><span class="sxs-lookup"><span data-stu-id="8a9f5-146">Requests/Sec</span></span> |<span data-ttu-id="8a9f5-147">Liczniki wydajności dla programu ASP.NET</span><span class="sxs-lookup"><span data-stu-id="8a9f5-147">Performance Counters for ASP.NET</span></span> |
| <span data-ttu-id="8a9f5-148">ASP.NET 4.0.30319</span><span class="sxs-lookup"><span data-stu-id="8a9f5-148">ASP.NET v4.0.30319</span></span> |<span data-ttu-id="8a9f5-149">Czas wykonania żądania</span><span class="sxs-lookup"><span data-stu-id="8a9f5-149">Request Execution Time</span></span> |<span data-ttu-id="8a9f5-150">Liczniki wydajności dla programu ASP.NET</span><span class="sxs-lookup"><span data-stu-id="8a9f5-150">Performance Counters for ASP.NET</span></span> |
| <span data-ttu-id="8a9f5-151">ASP.NET 4.0.30319</span><span class="sxs-lookup"><span data-stu-id="8a9f5-151">ASP.NET v4.0.30319</span></span> |<span data-ttu-id="8a9f5-152">Czas oczekiwania na żądanie</span><span class="sxs-lookup"><span data-stu-id="8a9f5-152">Request Wait Time</span></span> |<span data-ttu-id="8a9f5-153">Liczniki wydajności dla programu ASP.NET</span><span class="sxs-lookup"><span data-stu-id="8a9f5-153">Performance Counters for ASP.NET</span></span> |
| <span data-ttu-id="8a9f5-154">ASP.NET 4.0.30319</span><span class="sxs-lookup"><span data-stu-id="8a9f5-154">ASP.NET v4.0.30319</span></span> |<span data-ttu-id="8a9f5-155">Bieżące żądania</span><span class="sxs-lookup"><span data-stu-id="8a9f5-155">Requests Current</span></span> |<span data-ttu-id="8a9f5-156">Liczniki wydajności dla programu ASP.NET</span><span class="sxs-lookup"><span data-stu-id="8a9f5-156">Performance Counters for ASP.NET</span></span> |
| <span data-ttu-id="8a9f5-157">ASP.NET 4.0.30319</span><span class="sxs-lookup"><span data-stu-id="8a9f5-157">ASP.NET v4.0.30319</span></span> |<span data-ttu-id="8a9f5-158">Liczba żądań w kolejce</span><span class="sxs-lookup"><span data-stu-id="8a9f5-158">Requests Queued</span></span> |<span data-ttu-id="8a9f5-159">Liczniki wydajności dla programu ASP.NET</span><span class="sxs-lookup"><span data-stu-id="8a9f5-159">Performance Counters for ASP.NET</span></span> |
| <span data-ttu-id="8a9f5-160">ASP.NET 4.0.30319</span><span class="sxs-lookup"><span data-stu-id="8a9f5-160">ASP.NET v4.0.30319</span></span> |<span data-ttu-id="8a9f5-161">Liczba żądań odrzuconych</span><span class="sxs-lookup"><span data-stu-id="8a9f5-161">Requests Rejected</span></span> |<span data-ttu-id="8a9f5-162">Liczniki wydajności dla programu ASP.NET</span><span class="sxs-lookup"><span data-stu-id="8a9f5-162">Performance Counters for ASP.NET</span></span> |
| <span data-ttu-id="8a9f5-163">Memory (Pamięć)</span><span class="sxs-lookup"><span data-stu-id="8a9f5-163">Memory</span></span> |<span data-ttu-id="8a9f5-164">Dostępna pamięć (MB)</span><span class="sxs-lookup"><span data-stu-id="8a9f5-164">Available MBytes</span></span> |<span data-ttu-id="8a9f5-165">Liczniki wydajności pamięci</span><span class="sxs-lookup"><span data-stu-id="8a9f5-165">Memory Performance Counters</span></span> |
| <span data-ttu-id="8a9f5-166">Memory (Pamięć)</span><span class="sxs-lookup"><span data-stu-id="8a9f5-166">Memory</span></span> |<span data-ttu-id="8a9f5-167">Zadeklarowane bajty</span><span class="sxs-lookup"><span data-stu-id="8a9f5-167">Committed Bytes</span></span> |<span data-ttu-id="8a9f5-168">Liczniki wydajności pamięci</span><span class="sxs-lookup"><span data-stu-id="8a9f5-168">Memory Performance Counters</span></span> |
| <span data-ttu-id="8a9f5-169">Procesor(_Total)</span><span class="sxs-lookup"><span data-stu-id="8a9f5-169">Processor(_Total)</span></span> |<span data-ttu-id="8a9f5-170">Czas procesora (%)</span><span class="sxs-lookup"><span data-stu-id="8a9f5-170">% Processor Time</span></span> |<span data-ttu-id="8a9f5-171">Liczniki wydajności dla programu ASP.NET</span><span class="sxs-lookup"><span data-stu-id="8a9f5-171">Performance Counters for ASP.NET</span></span> |
| <span data-ttu-id="8a9f5-172">TCPv4</span><span class="sxs-lookup"><span data-stu-id="8a9f5-172">TCPv4</span></span> |<span data-ttu-id="8a9f5-173">Liczba błędów połączenia</span><span class="sxs-lookup"><span data-stu-id="8a9f5-173">Connection Failures</span></span> |<span data-ttu-id="8a9f5-174">Obiekt TCP</span><span class="sxs-lookup"><span data-stu-id="8a9f5-174">TCP Object</span></span> |
| <span data-ttu-id="8a9f5-175">TCPv4</span><span class="sxs-lookup"><span data-stu-id="8a9f5-175">TCPv4</span></span> |<span data-ttu-id="8a9f5-176">Połączeń</span><span class="sxs-lookup"><span data-stu-id="8a9f5-176">Connections Established</span></span> |<span data-ttu-id="8a9f5-177">Obiekt TCP</span><span class="sxs-lookup"><span data-stu-id="8a9f5-177">TCP Object</span></span> |
| <span data-ttu-id="8a9f5-178">TCPv4</span><span class="sxs-lookup"><span data-stu-id="8a9f5-178">TCPv4</span></span> |<span data-ttu-id="8a9f5-179">Resetowanie połączenia</span><span class="sxs-lookup"><span data-stu-id="8a9f5-179">Connections Reset</span></span> |<span data-ttu-id="8a9f5-180">Obiekt TCP</span><span class="sxs-lookup"><span data-stu-id="8a9f5-180">TCP Object</span></span> |
| <span data-ttu-id="8a9f5-181">TCPv4</span><span class="sxs-lookup"><span data-stu-id="8a9f5-181">TCPv4</span></span> |<span data-ttu-id="8a9f5-182">Segmenty wysłane/s</span><span class="sxs-lookup"><span data-stu-id="8a9f5-182">Segments Sent/sec</span></span> |<span data-ttu-id="8a9f5-183">Obiekt TCP</span><span class="sxs-lookup"><span data-stu-id="8a9f5-183">TCP Object</span></span> |
| <span data-ttu-id="8a9f5-184">Interface(*) sieci</span><span class="sxs-lookup"><span data-stu-id="8a9f5-184">Network Interface(*)</span></span> |<span data-ttu-id="8a9f5-185">Bajty odebrane/s</span><span class="sxs-lookup"><span data-stu-id="8a9f5-185">Bytes Received/sec</span></span> |<span data-ttu-id="8a9f5-186">Obiekt interfejsu sieciowego</span><span class="sxs-lookup"><span data-stu-id="8a9f5-186">Network Interface Object</span></span> |
| <span data-ttu-id="8a9f5-187">Interface(*) sieci</span><span class="sxs-lookup"><span data-stu-id="8a9f5-187">Network Interface(*)</span></span> |<span data-ttu-id="8a9f5-188">Bajty wysłane/s</span><span class="sxs-lookup"><span data-stu-id="8a9f5-188">Bytes Sent/sec</span></span> |<span data-ttu-id="8a9f5-189">Obiekt interfejsu sieciowego</span><span class="sxs-lookup"><span data-stu-id="8a9f5-189">Network Interface Object</span></span> |
| <span data-ttu-id="8a9f5-190">Interfejs sieciowy (_2 karty magistrali maszyny wirtualnej Microsoft sieci)</span><span class="sxs-lookup"><span data-stu-id="8a9f5-190">Network Interface(Microsoft Virtual Machine Bus Network Adapter _2)</span></span> |<span data-ttu-id="8a9f5-191">Bajty odebrane/s</span><span class="sxs-lookup"><span data-stu-id="8a9f5-191">Bytes Received/sec</span></span> |<span data-ttu-id="8a9f5-192">Obiekt interfejsu sieciowego</span><span class="sxs-lookup"><span data-stu-id="8a9f5-192">Network Interface Object</span></span> |
| <span data-ttu-id="8a9f5-193">Interfejs sieciowy (_2 karty magistrali maszyny wirtualnej Microsoft sieci)</span><span class="sxs-lookup"><span data-stu-id="8a9f5-193">Network Interface(Microsoft Virtual Machine Bus Network Adapter _2)</span></span> |<span data-ttu-id="8a9f5-194">Bajty wysłane/s</span><span class="sxs-lookup"><span data-stu-id="8a9f5-194">Bytes Sent/sec</span></span> |<span data-ttu-id="8a9f5-195">Obiekt interfejsu sieciowego</span><span class="sxs-lookup"><span data-stu-id="8a9f5-195">Network Interface Object</span></span> |
| <span data-ttu-id="8a9f5-196">Interfejs sieciowy (_2 karty magistrali maszyny wirtualnej Microsoft sieci)</span><span class="sxs-lookup"><span data-stu-id="8a9f5-196">Network Interface(Microsoft Virtual Machine Bus Network Adapter _2)</span></span> |<span data-ttu-id="8a9f5-197">Całkowita liczba bajtów/s</span><span class="sxs-lookup"><span data-stu-id="8a9f5-197">Bytes Total/sec</span></span> |<span data-ttu-id="8a9f5-198">Obiekt interfejsu sieciowego</span><span class="sxs-lookup"><span data-stu-id="8a9f5-198">Network Interface Object</span></span> |

## <a name="create-and-add-custom-performance-counters-to-your-application"></a><span data-ttu-id="8a9f5-199">Utwórz i Dodaj niestandardowe liczniki wydajności do aplikacji</span><span class="sxs-lookup"><span data-stu-id="8a9f5-199">Create and add custom performance counters to your application</span></span>
<span data-ttu-id="8a9f5-200">Platforma Azure ma techniczną w celu tworzenia i modyfikowania niestandardowe liczniki wydajności dla ról sieci web i proces roboczy.</span><span class="sxs-lookup"><span data-stu-id="8a9f5-200">Azure has support to create and modify custom performance counters for web roles and worker roles.</span></span> <span data-ttu-id="8a9f5-201">Liczniki mogą służyć do śledzenie i monitorowanie zachowania specyficzne dla aplikacji.</span><span class="sxs-lookup"><span data-stu-id="8a9f5-201">The counters may be used to track and monitor application-specific behavior.</span></span> <span data-ttu-id="8a9f5-202">Można tworzyć i usuwanie kategorii licznika wydajności niestandardowych i specyfikatory zadanie uruchamiania, rola sieci web lub roli proces roboczy z podwyższonym poziomem uprawnień.</span><span class="sxs-lookup"><span data-stu-id="8a9f5-202">You can create and delete custom performance counter categories and specifiers from a startup task, web role, or worker role with elevated permissions.</span></span>

> [!NOTE]
> <span data-ttu-id="8a9f5-203">Kod, który zmienia niestandardowe liczniki wydajności mają podwyższony poziom uprawnień do uruchomienia.</span><span class="sxs-lookup"><span data-stu-id="8a9f5-203">Code that makes changes to custom performance counters must have elevated permissions to run.</span></span> <span data-ttu-id="8a9f5-204">Jeśli kod jest w roli sieci web lub roli proces roboczy, rola musi zawierać znacznik <Runtime executionContext="elevated" /> w pliku ServiceDefinition.csdef dla roli, aby został poprawnie zainicjowany.</span><span class="sxs-lookup"><span data-stu-id="8a9f5-204">If the code is in a web role or worker role, the role must include the tag <Runtime executionContext="elevated" /> in the ServiceDefinition.csdef file for the role to initialize properly.</span></span>
>
>

<span data-ttu-id="8a9f5-205">Możesz wysłać dane licznika wydajności niestandardowych do magazynu platformy Azure przy użyciu agenta diagnostyki.</span><span class="sxs-lookup"><span data-stu-id="8a9f5-205">You can send custom performance counter data to Azure storage using the diagnostics agent.</span></span>

<span data-ttu-id="8a9f5-206">Dane licznika wydajności standardowe jest generowany przez procesy Azure.</span><span class="sxs-lookup"><span data-stu-id="8a9f5-206">The standard performance counter data is generated by the Azure processes.</span></span> <span data-ttu-id="8a9f5-207">Dane licznika wydajności niestandardowych muszą być utworzone przez aplikację sieci web roli lub procesu roboczego roli.</span><span class="sxs-lookup"><span data-stu-id="8a9f5-207">Custom performance counter data must be created by your web role or worker role application.</span></span> <span data-ttu-id="8a9f5-208">Zobacz [typy licznika wydajności](https://msdn.microsoft.com/library/z573042h.aspx) informacje o typach danych, które mogą być przechowywane w niestandardowe liczniki wydajności.</span><span class="sxs-lookup"><span data-stu-id="8a9f5-208">See [Performance Counter Types](https://msdn.microsoft.com/library/z573042h.aspx) for information on the types of data that can be stored in custom performance counters.</span></span> <span data-ttu-id="8a9f5-209">Zobacz [próbki liczniki wydajności](http://code.msdn.microsoft.com/azure/) na przykład, które tworzy i ustawia dane licznika wydajności niestandardowych w roli sieci web.</span><span class="sxs-lookup"><span data-stu-id="8a9f5-209">See [PerformanceCounters Sample](http://code.msdn.microsoft.com/azure/) for an example that creates and sets custom performance counter data in a web role.</span></span>

## <a name="store-and-view-performance-counter-data"></a><span data-ttu-id="8a9f5-210">Magazyn i widoku danych licznika wydajności</span><span class="sxs-lookup"><span data-stu-id="8a9f5-210">Store and view performance counter data</span></span>
<span data-ttu-id="8a9f5-211">Azure przechowuje dane licznika wydajności z innych informacji diagnostycznych.</span><span class="sxs-lookup"><span data-stu-id="8a9f5-211">Azure caches performance counter data with other diagnostic information.</span></span> <span data-ttu-id="8a9f5-212">Te dane są dostępne dla monitorowania zdalnego uruchomionej dla wystąpienia roli przy użyciu zdalnego dostępu do pulpitu. Aby wyświetlić narzędzi, takich jak monitora wydajności.</span><span class="sxs-lookup"><span data-stu-id="8a9f5-212">This data is available for remote monitoring while the role instance is running using remote desktop access to view tools such as Performance Monitor.</span></span> <span data-ttu-id="8a9f5-213">Do utrwalenia danych poza wystąpienia roli, agenta diagnostyki należy przenieść dane do magazynu Azure.</span><span class="sxs-lookup"><span data-stu-id="8a9f5-213">To persist the data outside of the role instance, the diagnostics agent must transfer the data to Azure storage.</span></span> <span data-ttu-id="8a9f5-214">Limit rozmiaru danych licznika wydajności pamięci podręcznej można skonfigurować w agencie diagnostyki lub może być skonfigurowany jako część udostępnionego limit dla wszystkich danych diagnostycznych.</span><span class="sxs-lookup"><span data-stu-id="8a9f5-214">The size limit of the cached performance counter data can be configured in the diagnostics agent, or it may be configured to be part of a shared limit for all the diagnostic data.</span></span> <span data-ttu-id="8a9f5-215">Aby uzyskać więcej informacji na temat ustawiania rozmiaru buforu, zobacz [OverallQuotaInMB](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.diagnostics.diagnosticmonitorconfiguration.overallquotainmb.aspx) i [DirectoriesBufferConfiguration](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.diagnostics.directoriesbufferconfiguration.aspx).</span><span class="sxs-lookup"><span data-stu-id="8a9f5-215">For more information about setting the buffer size, see [OverallQuotaInMB](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.diagnostics.diagnosticmonitorconfiguration.overallquotainmb.aspx) and [DirectoriesBufferConfiguration](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.diagnostics.directoriesbufferconfiguration.aspx).</span></span> <span data-ttu-id="8a9f5-216">Zobacz [magazynu i widoku danych diagnostycznych w usłudze Azure Storage](https://msdn.microsoft.com/library/azure/hh411534.aspx) omówienie konfigurowania agenta diagnostyki na przesyłanie danych do konta magazynu.</span><span class="sxs-lookup"><span data-stu-id="8a9f5-216">See [Store and View Diagnostic Data in Azure Storage](https://msdn.microsoft.com/library/azure/hh411534.aspx) for an overview of setting up the diagnostics agent to transfer data to a storage account.</span></span>

<span data-ttu-id="8a9f5-217">Każde wystąpienie licznika wydajności skonfigurowany jest rejestrowana w określonym próbkowania, a próbki danych jest przekazywana do konta magazynu przez żądanie transferu zaplanowanego lub żądanie transferu na żądanie.</span><span class="sxs-lookup"><span data-stu-id="8a9f5-217">Each configured performance counter instance is recorded at a specified sampling rate, and the sampled data is transferred to the storage account either by a scheduled transfer request or an on-demand transfer request.</span></span> <span data-ttu-id="8a9f5-218">Przeniesienia automatyczne może zostać zaplanowane tak często, jak jeden raz na minutę.</span><span class="sxs-lookup"><span data-stu-id="8a9f5-218">Automatic transfers may be scheduled as often as once per minute.</span></span> <span data-ttu-id="8a9f5-219">Przekazywane przez agenta diagnostyki danych licznika wydajności są przechowywane w tabeli, WADPerformanceCountersTable, w ramach konta magazynu.</span><span class="sxs-lookup"><span data-stu-id="8a9f5-219">Performance counter data transferred by the diagnostics agent is stored in a table, WADPerformanceCountersTable, in the storage account.</span></span> <span data-ttu-id="8a9f5-220">Ta tabela może uzyskać dostępu do i wykonać zapytania z metody interfejsu API magazynu Azure w warstwie standardowa.</span><span class="sxs-lookup"><span data-stu-id="8a9f5-220">This table may be accessed and queried with standard Azure storage API methods.</span></span> <span data-ttu-id="8a9f5-221">Zobacz [przykład liczniki wydajności programu Microsoft Azure](http://code.msdn.microsoft.com/Windows-Azure-PerformanceCo-7d80ebf9) przykład kwerend i wyświetlanie danych licznika wydajności z tabeli WADPerformanceCountersTable.</span><span class="sxs-lookup"><span data-stu-id="8a9f5-221">See [Microsoft Azure PerformanceCounters Sample](http://code.msdn.microsoft.com/Windows-Azure-PerformanceCo-7d80ebf9) for an example of querying and displaying performance counter data from the WADPerformanceCountersTable table.</span></span>

> [!NOTE]
> <span data-ttu-id="8a9f5-222">W zależności od Diagnostyka agenta transferu częstotliwość i czas oczekiwania w kolejce najnowsze dane licznika wydajności w ramach konta magazynu może potrwać kilka minut nieaktualny.</span><span class="sxs-lookup"><span data-stu-id="8a9f5-222">Depending on the diagnostics agent transfer frequency and queue latency, the most recent performance counter data in the storage account may be several minutes out of date.</span></span>
>
>

## <a name="enable-performance-counters-using-diagnostics-configuration-file"></a><span data-ttu-id="8a9f5-223">Włącz użycie pliku konfiguracji diagnostyki liczniki wydajności</span><span class="sxs-lookup"><span data-stu-id="8a9f5-223">Enable performance counters using diagnostics configuration file</span></span>
<span data-ttu-id="8a9f5-224">Aby włączyć liczniki wydajności w aplikacji platformy Azure, użyj poniższej procedury.</span><span class="sxs-lookup"><span data-stu-id="8a9f5-224">Use the following procedure to enable performance counters in your Azure application.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8a9f5-225">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="8a9f5-225">Prerequisites</span></span>
<span data-ttu-id="8a9f5-226">W tej sekcji założono, że zaimportowane monitor diagnostyki aplikacji i plik konfiguracji diagnostyki dodany do rozwiązania Visual Studio (diagnostics.wadcfg w 2.4 zestawu SDK i poniżej lub diagnostics.wadcfgx w zestawie SDK, 2.5 lub nowszej).</span><span class="sxs-lookup"><span data-stu-id="8a9f5-226">This section assumes that you have imported the Diagnostics monitor into your application and added the diagnostics configuration file to your Visual Studio solution (diagnostics.wadcfg in SDK 2.4 and below or diagnostics.wadcfgx in SDK 2.5 and above).</span></span> <span data-ttu-id="8a9f5-227">Zobacz kroki 1 i 2 w [Włączanie diagnostyki w usług Azure Cloud Services i maszyn wirtualnych](cloud-services-dotnet-diagnostics.md)) Aby uzyskać więcej informacji.</span><span class="sxs-lookup"><span data-stu-id="8a9f5-227">See steps 1 and 2 in [Enabling Diagnostics in Azure Cloud Services and Virtual Machines](cloud-services-dotnet-diagnostics.md)) for more information.</span></span>

## <a name="step-1-collect-and-store-data-from-performance-counters"></a><span data-ttu-id="8a9f5-228">Krok 1: Zbieranie i przechowywanie danych z liczników wydajności</span><span class="sxs-lookup"><span data-stu-id="8a9f5-228">Step 1: Collect and store data from performance counters</span></span>
<span data-ttu-id="8a9f5-229">Po dodaniu pliku diagnostyki do rozwiązania Visual Studio, można skonfigurować zbieranie i przechowywanie danych licznika wydajności w aplikacji Azure.</span><span class="sxs-lookup"><span data-stu-id="8a9f5-229">After you have added the diagnostics file to your Visual Studio solution, you can configure the collection and storage of performance counter data in an Azure application.</span></span> <span data-ttu-id="8a9f5-230">Jest to realizowane przez dodanie liczników wydajności do pliku diagnostyki.</span><span class="sxs-lookup"><span data-stu-id="8a9f5-230">This is done by adding performance counters to the diagnostics file.</span></span> <span data-ttu-id="8a9f5-231">Dane diagnostyczne, łącznie z liczników wydajności, najpierw są zbierane w wystąpieniu.</span><span class="sxs-lookup"><span data-stu-id="8a9f5-231">Diagnostics data, including performance counters, is first collected on the instance.</span></span> <span data-ttu-id="8a9f5-232">Dane następnie jest trwały do tabeli WADPerformanceCountersTable w usłudze tabel Azure, więc należy również określić konto magazynu w aplikacji.</span><span class="sxs-lookup"><span data-stu-id="8a9f5-232">The data is then persisted to the WADPerformanceCountersTable table in the Azure Table service, so you will also need to specify the storage account in your application.</span></span> <span data-ttu-id="8a9f5-233">W przypadku testowania lokalnie aplikację w emulatorze obliczeniowe, można również przechowywać dane diagnostyczne lokalnie w emulatorze magazynu.</span><span class="sxs-lookup"><span data-stu-id="8a9f5-233">If you're testing your application locally in the Compute Emulator, you can also store diagnostics data locally in the Storage Emulator.</span></span> <span data-ttu-id="8a9f5-234">Przed zapisaniem danych diagnostycznych, należy najpierw przejść do [portalu Azure](http://portal.azure.com/) i Utwórz konto magazynu klasycznego.</span><span class="sxs-lookup"><span data-stu-id="8a9f5-234">Before you store diagnostics data, you must first go to the [Azure portal](http://portal.azure.com/) and create a classic storage account.</span></span> <span data-ttu-id="8a9f5-235">Najlepszym rozwiązaniem jest można znaleźć konta magazynu w tej samej lokalizacji geograficznej jako aplikacji platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="8a9f5-235">A best practice is to locate your storage account in the same geo-location as your Azure application.</span></span> <span data-ttu-id="8a9f5-236">Przez zachowanie aplikacji Azure i konto magazynu znajdują się w tej samej lokalizacji geograficznej, uniknąć kosztów przepustowości zewnętrznych płatności i zmniejszenia opóźnień.</span><span class="sxs-lookup"><span data-stu-id="8a9f5-236">By keeping the Azure application and storage account are in the same geo-location, you avoid paying external bandwidth costs and reduce latency.</span></span>

### <a name="add-performance-counters-to-the-diagnostics-file"></a><span data-ttu-id="8a9f5-237">Dodaj liczniki wydajności do pliku diagnostyki</span><span class="sxs-lookup"><span data-stu-id="8a9f5-237">Add performance counters to the diagnostics file</span></span>
<span data-ttu-id="8a9f5-238">Istnieje wiele liczników, których można użyć.</span><span class="sxs-lookup"><span data-stu-id="8a9f5-238">There are many counters you can use.</span></span> <span data-ttu-id="8a9f5-239">W poniższym przykładzie przedstawiono kilka liczniki wydajności, które są zalecane sieci web i monitorowania roli procesu roboczego.</span><span class="sxs-lookup"><span data-stu-id="8a9f5-239">The following example shows several performance counters that are recommended for web and worker role monitoring.</span></span>

<span data-ttu-id="8a9f5-240">Otwórz plik diagnostyki (diagnostics.wadcfg w 2.4 zestawu SDK i poniżej lub diagnostics.wadcfgx w zestawie SDK, 2.5 lub nowszym) i dodaj następującą wartość do elementu DiagnosticMonitorConfiguration:</span><span class="sxs-lookup"><span data-stu-id="8a9f5-240">Open the diagnostics file (diagnostics.wadcfg in SDK 2.4 and below or diagnostics.wadcfgx in SDK 2.5 and above) and add the following to the DiagnosticMonitorConfiguration element:</span></span>

```xml
<PerformanceCounters bufferQuotaInMB="0" scheduledTransferPeriod="PT30M">
    <PerformanceCounterConfiguration counterSpecifier="\Memory\Available Bytes" sampleRate="PT30S" />
    <PerformanceCounterConfiguration counterSpecifier="\Processor(_Total)\% Processor Time" sampleRate="PT30S" />

    <!-- Use the Process(w3wp) category counters in a web role -->

    <PerformanceCounterConfiguration counterSpecifier="\Process(w3wp)\% Processor Time" sampleRate="PT30S" />
    <PerformanceCounterConfiguration counterSpecifier="\Process(w3wp)\Private Bytes" sampleRate="PT30S" />
    <PerformanceCounterConfiguration counterSpecifier="\Process(w3wp)\Thread Count" sampleRate="PT30S" />

    <!-- Use the Process(WaWorkerHost) category counters in a worker role.
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

<span data-ttu-id="8a9f5-241">Atrybut bufferQuotaInMB, która określa maksymalną ilość pamięci systemu plików, która jest dostępna dla tego typu kolekcji danych (Azure dzienniki, dzienniki programu IIS, itp.).</span><span class="sxs-lookup"><span data-stu-id="8a9f5-241">The bufferQuotaInMB attribute, which specifies the maximum amount of file system storage that is available for the data collection type (Azure logs, IIS logs, etc.).</span></span> <span data-ttu-id="8a9f5-242">Wartość domyślna to 0.</span><span class="sxs-lookup"><span data-stu-id="8a9f5-242">The default is 0.</span></span> <span data-ttu-id="8a9f5-243">Po osiągnięciu limitu przydziału najstarsze dane zostaną usunięte po dodaniu nowych danych.</span><span class="sxs-lookup"><span data-stu-id="8a9f5-243">When the quota is reached, the oldest data is deleted as new data is added.</span></span> <span data-ttu-id="8a9f5-244">Suma wszystkich właściwości bufferQuotaInMB musi być większa niż wartość atrybutu OverallQuotaInMB.</span><span class="sxs-lookup"><span data-stu-id="8a9f5-244">The sum of all the bufferQuotaInMB properties must be greater than the value of the OverallQuotaInMB attribute.</span></span> <span data-ttu-id="8a9f5-245">Bardziej szczegółowe omówienie określania, ile miejsca do magazynowania jest wymagana w przypadku zbierania danych diagnostycznych, zobacz sekcję konfiguracji WAD [Rozwiązywanie problemów z najlepszych rozwiązań dotyczących tworzenia aplikacji Azure](https://msdn.microsoft.com/library/windowsazure/hh771389.aspx).</span><span class="sxs-lookup"><span data-stu-id="8a9f5-245">For a more detailed discussion of determining how much storage will be required for the collection of diagnostics data, see the Setup WAD section of [Troubleshooting Best Practices for Developing Azure Applications](https://msdn.microsoft.com/library/windowsazure/hh771389.aspx).</span></span>

<span data-ttu-id="8a9f5-246">Atrybut scheduledTransferPeriod, który określa interwał między zaplanowane transferów danych, zaokrąglona w górę do najbliższej minutę.</span><span class="sxs-lookup"><span data-stu-id="8a9f5-246">The scheduledTransferPeriod attribute, which specifies the interval between scheduled transfers of data, rounded up to the nearest minute.</span></span> <span data-ttu-id="8a9f5-247">W poniższych przykładach jest ustawiona na PT30M (30 minut).</span><span class="sxs-lookup"><span data-stu-id="8a9f5-247">In the following examples, it is set to PT30M (30 minutes).</span></span> <span data-ttu-id="8a9f5-248">Ustawienie okresu transfer mała wartość, na przykład 1 minutę, obniży wydajności aplikacji w środowisku produkcyjnym, ale może być przydatne w przypadku diagnostyki oglądanie Postaramy się szybko podczas testowania.</span><span class="sxs-lookup"><span data-stu-id="8a9f5-248">Setting the transfer period to a small value, such as 1 minute, will adversely impact your application's performance in production but can be useful for seeing diagnostics working quickly when you are testing.</span></span> <span data-ttu-id="8a9f5-249">Wartość okresu zaplanowanego transferu powinna być duże, aby upewnić się, że danych diagnostycznych nie jest zastępowana wystąpienia, ale wystarczająco duży, że nie ma wpływu na wydajność aplikacji.</span><span class="sxs-lookup"><span data-stu-id="8a9f5-249">The scheduled transfer period should be small enough to ensure that diagnostic data is not overwritten on the instance, but large enough that it will not impact the performance of your application.</span></span>

<span data-ttu-id="8a9f5-250">Atrybut counterSpecifier Określa licznik wydajności do zbierania.</span><span class="sxs-lookup"><span data-stu-id="8a9f5-250">The counterSpecifier attribute specifies the performance counter to collect.</span></span> <span data-ttu-id="8a9f5-251">Atrybut sampleRate określa szybkość, w którym licznik wydajności powinny być pobrane, w tym przypadku 30 sekund.</span><span class="sxs-lookup"><span data-stu-id="8a9f5-251">The sampleRate attribute specifies the rate at which the performance counter should be sampled, in this case 30 seconds.</span></span>

<span data-ttu-id="8a9f5-252">Po dodaniu liczniki wydajności, które chcesz zebrać, Zapisz zmiany w pliku diagnostyki.</span><span class="sxs-lookup"><span data-stu-id="8a9f5-252">Once you've added the performance counters that you want to collect, save your changes to the diagnostics file.</span></span> <span data-ttu-id="8a9f5-253">Następnie należy określić konto magazynu, które zostaną utrwalone danych diagnostycznych.</span><span class="sxs-lookup"><span data-stu-id="8a9f5-253">Next, you need to specify the storage account that the diagnostics data will be persisted to.</span></span>

### <a name="specify-the-storage-account"></a><span data-ttu-id="8a9f5-254">Określ konto magazynu</span><span class="sxs-lookup"><span data-stu-id="8a9f5-254">Specify the storage account</span></span>
<span data-ttu-id="8a9f5-255">Aby utrwalić danych diagnostycznych do konta magazynu Azure, należy określić parametry połączenia w pliku konfiguracyjnym (pliku ServiceConfiguration.cscfg) usługi.</span><span class="sxs-lookup"><span data-stu-id="8a9f5-255">To persist your diagnostics information to your Azure Storage account, you must specify a connection string in your service configuration (ServiceConfiguration.cscfg) file.</span></span>

<span data-ttu-id="8a9f5-256">2.5 zestawu SDK platformy Azure konta magazynu można określić w pliku diagnostics.wadcfgx.</span><span class="sxs-lookup"><span data-stu-id="8a9f5-256">For Azure SDK 2.5, the Storage Account can be specified in the diagnostics.wadcfgx file.</span></span>

> [!NOTE]
> <span data-ttu-id="8a9f5-257">Te instrukcje dotyczą tylko, 2.4 zestawu SDK platformy Azure i poniżej.</span><span class="sxs-lookup"><span data-stu-id="8a9f5-257">These instructions only apply to Azure SDK 2.4 and below.</span></span> <span data-ttu-id="8a9f5-258">2.5 zestawu SDK platformy Azure konta magazynu można określić w pliku diagnostics.wadcfgx.</span><span class="sxs-lookup"><span data-stu-id="8a9f5-258">For Azure SDK 2.5, the Storage Account can be specified in the diagnostics.wadcfgx file.</span></span>
>
>

<span data-ttu-id="8a9f5-259">Aby ustawić parametry połączenia:</span><span class="sxs-lookup"><span data-stu-id="8a9f5-259">To set the connection strings:</span></span>

1. <span data-ttu-id="8a9f5-260">Otwórz plik ServiceConfiguration.Cloud.cscfg przy użyciu w ulubionym edytorze tekstów i ustaw parametry połączenia magazynu.</span><span class="sxs-lookup"><span data-stu-id="8a9f5-260">Open the ServiceConfiguration.Cloud.cscfg file using your favorite text editor and set the connection string for your storage.</span></span> <span data-ttu-id="8a9f5-261">*AccountName* i *AccountKey* wartości znajdują się w portalu Azure na pulpicie nawigacyjnym konta magazynu, w obszarze klucze dostępu.</span><span class="sxs-lookup"><span data-stu-id="8a9f5-261">The *AccountName* and *AccountKey* values are found in the Azure portal in the storage account dashboard, under Access keys.</span></span>

    ```xml
    <ConfigurationSettings>
      <Setting name="Microsoft.WindowsAzure.Plugins.Diagnostics.ConnectionString" value="DefaultEndpointsProtocol=https;AccountName=<name>;AccountKey=<key>"/>
    </ConfigurationSettings>
    ```
2. <span data-ttu-id="8a9f5-262">Zapisz plik ServiceConfiguration.Cloud.cscfg.</span><span class="sxs-lookup"><span data-stu-id="8a9f5-262">Save the ServiceConfiguration.Cloud.cscfg file.</span></span>
3. <span data-ttu-id="8a9f5-263">Otwórz plik ServiceConfiguration.Local.cscfg i sprawdź, czy UseDevelopmentStorage jest ustawiony na wartość true.</span><span class="sxs-lookup"><span data-stu-id="8a9f5-263">Open the ServiceConfiguration.Local.cscfg file and verify that UseDevelopmentStorage is set to true.</span></span>

    ```xml
    <ConfigurationSettings>
      <Settingname="Microsoft.WindowsAzure.Plugins.Diagnostics.ConnectionString" value="UseDevelopmentStorage=true"/>
    </ConfigurationSettings>
    ```
   <span data-ttu-id="8a9f5-264">Teraz, gdy parametry połączenia są ustawione, aplikacji zachować dane diagnostyczne do konta magazynu, po wdrożeniu aplikacji.</span><span class="sxs-lookup"><span data-stu-id="8a9f5-264">Now that the connection strings are set, your application will persist diagnostics data to your storage account when your application is deployed.</span></span>
4. <span data-ttu-id="8a9f5-265">Zapisz i skompilowanie projektu, a następnie wdrożyć aplikację.</span><span class="sxs-lookup"><span data-stu-id="8a9f5-265">Save and build your project, then deploy your application.</span></span>

## <a name="step-2-optional-create-custom-performance-counters"></a><span data-ttu-id="8a9f5-266">Krok 2: (Opcjonalnie) Utwórz niestandardowe liczniki wydajności</span><span class="sxs-lookup"><span data-stu-id="8a9f5-266">Step 2: (Optional) Create custom performance counters</span></span>
<span data-ttu-id="8a9f5-267">Oprócz liczniki wydajności wstępnie zdefiniowane można dodać własne niestandardowe liczniki wydajności do monitorowania role sieci web lub procesu roboczego.</span><span class="sxs-lookup"><span data-stu-id="8a9f5-267">In addition to the pre-defined performance counters, you can add your own custom performance counters to monitor web or worker roles.</span></span> <span data-ttu-id="8a9f5-268">Niestandardowe liczniki wydajności mogą służyć do śledzenia i monitorowanie zachowania specyficzne dla aplikacji i może być utworzone lub usunięte zadanie uruchamiania, rola sieci web lub roli proces roboczy z podwyższonym poziomem uprawnień.</span><span class="sxs-lookup"><span data-stu-id="8a9f5-268">Custom performance counters may be used to track and monitor application-specific behavior and can be created or deleted in a startup task, web role, or worker role with elevated permissions.</span></span>

<span data-ttu-id="8a9f5-269">Agent Azure diagnostics odświeża konfigurację liczników wydajności z pliku .wadcfg minutę po uruchomieniu.</span><span class="sxs-lookup"><span data-stu-id="8a9f5-269">The Azure diagnostics agent refreshes the performance counter configuration from the .wadcfg file one minute after starting.</span></span>  <span data-ttu-id="8a9f5-270">Utwórz niestandardowe liczniki wydajności w przypadku metody OnStart, uruchamiania zadań trwać dłużej niż minutę do wykonania Twoje niestandardowe liczniki wydajności zostaną nie utworzono podczas diagnostyki Azure agent próbuje załadować je.</span><span class="sxs-lookup"><span data-stu-id="8a9f5-270">If you create custom performance counters in the OnStart method and your startup tasks take longer than one minute to execute, your custom performance counters will not have been created when the Azure Diagnostics agent tries to load them.</span></span>  <span data-ttu-id="8a9f5-271">W tym scenariuszu zobaczysz, że diagnostyki Azure poprawnie przechwytuje wszystkie dane diagnostyczne, z wyjątkiem Twojego niestandardowe liczniki wydajności.</span><span class="sxs-lookup"><span data-stu-id="8a9f5-271">In this scenario, you will see that Azure Diagnostics correctly captures all diagnostics data except your custom performance counters.</span></span>  <span data-ttu-id="8a9f5-272">Aby rozwiązać ten problem, należy utworzyć liczniki wydajności w zadanie uruchamiania lub Przenieś niektóre zadania uruchamiania działają metody OnStart po utworzeniu liczników wydajności.</span><span class="sxs-lookup"><span data-stu-id="8a9f5-272">To resolve this issue, create the performance counters in a startup task or move some of your startup task work to the OnStart method after creating the performance counters.</span></span>

<span data-ttu-id="8a9f5-273">Wykonaj poniższe kroki, aby utworzyć prosty wydajności niestandardowych licznik o nazwie "\MyCustomCounterCategory\MyButton1Counter":</span><span class="sxs-lookup"><span data-stu-id="8a9f5-273">Perform the following steps to create a simple custom performance counter named "\MyCustomCounterCategory\MyButton1Counter":</span></span>

1. <span data-ttu-id="8a9f5-274">Otwórz plik definicji usługi (CSDEF) dla aplikacji.</span><span class="sxs-lookup"><span data-stu-id="8a9f5-274">Open the service definition file (CSDEF) for your application.</span></span>
2. <span data-ttu-id="8a9f5-275">Dodaj element środowiska uruchomieniowego do sieć Web lub proces roboczy elementu umożliwia wykonanie z podwyższonym poziomem uprawnień:</span><span class="sxs-lookup"><span data-stu-id="8a9f5-275">Add the Runtime element to the WebRole or WorkerRole element to allow execution with elevated privileges:</span></span>

    ```xml
    <runtime executioncontext="elevated"/>
    ```
3. <span data-ttu-id="8a9f5-276">Zapisz plik.</span><span class="sxs-lookup"><span data-stu-id="8a9f5-276">Save the file.</span></span>
4. <span data-ttu-id="8a9f5-277">Otwórz plik diagnostyki (diagnostics.wadcfg w 2.4 zestawu SDK i poniżej lub diagnostics.wadcfgx w zestawie SDK, 2.5 lub nowszym) i dodaj następującą wartość do DiagnosticMonitorConfiguration</span><span class="sxs-lookup"><span data-stu-id="8a9f5-277">Open the diagnostics file (diagnostics.wadcfg in SDK 2.4 and below or diagnostics.wadcfgx in SDK 2.5 and above) and add the following to the DiagnosticMonitorConfiguration</span></span>

    ```xml
    <PerformanceCounters bufferQuotaInMB="0" scheduledTransferPeriod="PT30M">
      <PerformanceCounterConfiguration counterSpecifier="\MyCustomCounterCategory\MyButton1Counter" sampleRate="PT30S"/>
    </PerformanceCounters>
    ```
5. <span data-ttu-id="8a9f5-278">Zapisz plik.</span><span class="sxs-lookup"><span data-stu-id="8a9f5-278">Save the file.</span></span>
6. <span data-ttu-id="8a9f5-279">Tworzenie kategorii licznika wydajności niestandardowe metody OnStart roli użytkownika przed wywołaniem bazy. OnStart.</span><span class="sxs-lookup"><span data-stu-id="8a9f5-279">Create the custom performance counter category in the OnStart method of your role, before invoking base.OnStart.</span></span> <span data-ttu-id="8a9f5-280">W poniższym przykładzie C# tworzy kategorię niestandardową, jeśli jeszcze nie istnieje:</span><span class="sxs-lookup"><span data-stu-id="8a9f5-280">The following C# example creates a custom category, if it does not already exist:</span></span>

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
7. <span data-ttu-id="8a9f5-281">Aktualizuj liczniki w aplikacji.</span><span class="sxs-lookup"><span data-stu-id="8a9f5-281">Update the counters within your application.</span></span> <span data-ttu-id="8a9f5-282">Poniższy przykład aktualizacje licznika wydajności niestandardowych zdarzeń Button1_Click:</span><span class="sxs-lookup"><span data-stu-id="8a9f5-282">The following example updates a custom performance counter on Button1_Click events:</span></span>

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
8. <span data-ttu-id="8a9f5-283">Zapisz plik.</span><span class="sxs-lookup"><span data-stu-id="8a9f5-283">Save the file.</span></span>  

<span data-ttu-id="8a9f5-284">Dane licznika wydajności niestandardowych teraz zostaną zebrane przez monitor diagnostycznych platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="8a9f5-284">Custom performance counter data will now be collected by the Azure diagnostics monitor.</span></span>

## <a name="step-3-query-performance-counter-data"></a><span data-ttu-id="8a9f5-285">Krok 3: Wykonywanie zapytań danych licznika wydajności</span><span class="sxs-lookup"><span data-stu-id="8a9f5-285">Step 3: Query performance counter data</span></span>
<span data-ttu-id="8a9f5-286">Po wdrożeniu aplikacji i uruchomiona, monitor diagnostyki rozpocznie się zbierania liczników wydajności i przechowywanie danych do magazynu Azure.</span><span class="sxs-lookup"><span data-stu-id="8a9f5-286">Once your application is deployed and running, the Diagnostics monitor will begin collecting performance counters and persisting that data to Azure storage.</span></span> <span data-ttu-id="8a9f5-287">Użyj narzędzi takich jak Eksplorator serwera w programie Visual Studio, [Eksploratora usługi Storage Azure](http://azurestorageexplorer.codeplex.com/), lub [Menedżera diagnostyki Azure](http://www.cerebrata.com/Products/AzureDiagnosticsManager/Default.aspx) przez Cerebrata, aby wyświetlić dane w WADPerformanceCountersTable liczniki wydajności Tabela.</span><span class="sxs-lookup"><span data-stu-id="8a9f5-287">You use tools such as Server Explorer in Visual Studio,  [Azure Storage Explorer](http://azurestorageexplorer.codeplex.com/), or [Azure Diagnostics Manager](http://www.cerebrata.com/Products/AzureDiagnosticsManager/Default.aspx) by Cerebrata to view the performance counters data in the WADPerformanceCountersTable table.</span></span> <span data-ttu-id="8a9f5-288">Można również programowo zapytania przy użyciu usługi tabeli [C#](../cosmos-db/table-storage-how-to-use-dotnet.md), [Java](../cosmos-db/table-storage-how-to-use-java.md), [Node.js](../cosmos-db/table-storage-how-to-use-nodejs.md), [Python](../cosmos-db/table-storage-how-to-use-python.md), [Ruby](../cosmos-db/table-storage-how-to-use-ruby.md), lub [PHP](../cosmos-db/table-storage-how-to-use-php.md).</span><span class="sxs-lookup"><span data-stu-id="8a9f5-288">You can also programmatically query the Table service using [C#](../cosmos-db/table-storage-how-to-use-dotnet.md),  [Java](../cosmos-db/table-storage-how-to-use-java.md),  [Node.js](../cosmos-db/table-storage-how-to-use-nodejs.md), [Python](../cosmos-db/table-storage-how-to-use-python.md), [Ruby](../cosmos-db/table-storage-how-to-use-ruby.md), or [PHP](../cosmos-db/table-storage-how-to-use-php.md).</span></span>

<span data-ttu-id="8a9f5-289">W poniższym przykładzie C# zawiera zapytania podstawowego w tabeli WADPerformanceCountersTable i zapisuje dane diagnostyczne do pliku CSV.</span><span class="sxs-lookup"><span data-stu-id="8a9f5-289">The following C# example shows a basic query against the WADPerformanceCountersTable table and saves the diagnostics data to a CSV file.</span></span> <span data-ttu-id="8a9f5-290">Liczniki wydajności są zapisane do pliku CSV, można użyć graficznych możliwości programu Microsoft Excel lub inne narzędzie do wizualizacji danych.</span><span class="sxs-lookup"><span data-stu-id="8a9f5-290">Once the performance counters are saved to a CSV file, you can use the graphing capabilities in Microsoft Excel or some other tool to visualize the data.</span></span> <span data-ttu-id="8a9f5-291">Pamiętaj dodać odwołania do Microsoft.WindowsAzure.Storage.dll, która jest uwzględniona w zestawie Azure SDK dla platformy .NET października 2012 lub nowszym.</span><span class="sxs-lookup"><span data-stu-id="8a9f5-291">Be sure to add a reference to Microsoft.WindowsAzure.Storage.dll, which is included in the Azure SDK for .NET October 2012 and later.</span></span> <span data-ttu-id="8a9f5-292">Zestaw jest instalowany w katalogu % Program Files%\Microsoft SDKs\Microsoft Azure.NET SDK\version-num\ref\.</span><span class="sxs-lookup"><span data-stu-id="8a9f5-292">The assembly is installed to the %Program Files%\Microsoft SDKs\Microsoft Azure.NET SDK\version-num\ref\ directory.</span></span>

```csharp
using Microsoft.WindowsAzure.Storage;
using Microsoft.WindowsAzure.Storage.Auth;
using Microsoft.WindowsAzure.Storage.Table;
...

// Get the connection string. When using Microsoft Azure Cloud Services, it is recommended
// you store your connection string using the Microsoft Azure service configuration
// system (*.csdef and *.cscfg files). You can you use the CloudConfigurationManager type
// to retrieve your storage connection string.  If you're not using Cloud Services, it's
// recommended that you store the connection string in your web.config or app.config file.
// Use the ConfigurationManager type to retrieve your storage connection string.

string connectionString = Microsoft.WindowsAzure.CloudConfigurationManager.GetSetting("StorageConnectionString");
//string connectionString = System.Configuration.ConfigurationManager.ConnectionStrings["StorageConnectionString"].ConnectionString;

// Get a reference to the storage account using the connection string.  You can also use the development
// storage account (Storage Emulator) for local debugging.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(connectionString);
//CloudStorageAccount storageAccount = CloudStorageAccount.DevelopmentStorageAccount;

// Create the table client.
CloudTableClient tableClient = storageAccount.CreateCloudTableClient();

// Create the CloudTable object that represents the "WADPerformanceCountersTable" table.
CloudTable table = tableClient.GetTableReference("WADPerformanceCountersTable");

// Create the table query, filter on a specific CounterName, DeploymentId and RoleInstance.
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

// Execute the table query.
IEnumerable<PerformanceCountersEntity> result = table.ExecuteQuery(query);

// Process the query results and build a CSV file.
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

<span data-ttu-id="8a9f5-293">Jednostki są mapowane do obiektów C# za pomocą niestandardowej klasy pochodzącej od **TableEntity**.</span><span class="sxs-lookup"><span data-stu-id="8a9f5-293">Entities map to C# objects using a custom class derived from **TableEntity**.</span></span> <span data-ttu-id="8a9f5-294">Poniższy kod definiuje klasę jednostki, która reprezentuje licznika wydajności w **WADPerformanceCountersTable** tabeli.</span><span class="sxs-lookup"><span data-stu-id="8a9f5-294">The following code defines an entity class that represents a performance counter in the **WADPerformanceCountersTable** table.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="8a9f5-295">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="8a9f5-295">Next Steps</span></span>
[<span data-ttu-id="8a9f5-296">Przeglądanie dodatkowych artykułów na diagnostyki Azure</span><span class="sxs-lookup"><span data-stu-id="8a9f5-296">View additional articles on Azure Diagnostics</span></span>](../azure-diagnostics.md)
