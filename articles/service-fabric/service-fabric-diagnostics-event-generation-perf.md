---
title: "Wydajność sieci szkieletowej Azure usługi monitorowania | Dokumentacja firmy Microsoft"
description: "Więcej informacji na temat liczników wydajności dla monitorowania i diagnostyki klastrów sieci szkieletowej usług Azure."
services: service-fabric
documentationcenter: .net
author: dkkapur
manager: timlt
editor: 
ms.assetid: 
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/30/2017
ms.author: dekapur
ms.openlocfilehash: 9d63148c182c705b6b49733c59ed8fdd13872d72
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="performance-metrics"></a><span data-ttu-id="c6ed3-103">Metryki wydajności</span><span class="sxs-lookup"><span data-stu-id="c6ed3-103">Performance metrics</span></span>

<span data-ttu-id="c6ed3-104">Aby zrozumieć działanie klastra, a także aplikacji uruchomionych w niej powinny być gromadzone metryki.</span><span class="sxs-lookup"><span data-stu-id="c6ed3-104">Metrics should be collected to understand the performance of your cluster as well as the applications running in it.</span></span> <span data-ttu-id="c6ed3-105">Dla klastrów sieci szkieletowej usług firma Microsoft zaleca zbieranie następujących liczników wydajności.</span><span class="sxs-lookup"><span data-stu-id="c6ed3-105">For Service Fabric clusters, we recommend collecting the following performance counters.</span></span>

## <a name="nodes"></a><span data-ttu-id="c6ed3-106">Węzły</span><span class="sxs-lookup"><span data-stu-id="c6ed3-106">Nodes</span></span>

<span data-ttu-id="c6ed3-107">Dla maszyn w klastrze należy wziąć pod uwagę następujące liczniki wydajności do lepszego zrozumienia obciążenia na każdej maszynie i wprowadzić odpowiednie klastra skalowanie decyzje dotyczące zbierania.</span><span class="sxs-lookup"><span data-stu-id="c6ed3-107">For the machines in your cluster, consider collecting the following performance counters to better understand the load on each machine and make appropriate cluster scaling decisions.</span></span>

| <span data-ttu-id="c6ed3-108">Kategoria licznika</span><span class="sxs-lookup"><span data-stu-id="c6ed3-108">Counter Category</span></span> | <span data-ttu-id="c6ed3-109">Nazwa licznika</span><span class="sxs-lookup"><span data-stu-id="c6ed3-109">Counter Name</span></span> |
| --- | --- |
| <span data-ttu-id="c6ed3-110">Dysk fizyczny (na dysku)</span><span class="sxs-lookup"><span data-stu-id="c6ed3-110">PhysicalDisk(per Disk)</span></span> | <span data-ttu-id="c6ed3-111">Średni</span><span class="sxs-lookup"><span data-stu-id="c6ed3-111">Avg.</span></span> <span data-ttu-id="c6ed3-112">Długość kolejki odczytu dysku</span><span class="sxs-lookup"><span data-stu-id="c6ed3-112">Disk Read Queue Length</span></span> |
| <span data-ttu-id="c6ed3-113">Dysk fizyczny (na dysku)</span><span class="sxs-lookup"><span data-stu-id="c6ed3-113">PhysicalDisk(per Disk)</span></span> | <span data-ttu-id="c6ed3-114">Średni</span><span class="sxs-lookup"><span data-stu-id="c6ed3-114">Avg.</span></span> <span data-ttu-id="c6ed3-115">Długość kolejki dysku zapisu</span><span class="sxs-lookup"><span data-stu-id="c6ed3-115">Disk Write Queue Length</span></span> |
| <span data-ttu-id="c6ed3-116">Dysk fizyczny (na dysku)</span><span class="sxs-lookup"><span data-stu-id="c6ed3-116">PhysicalDisk(per Disk)</span></span> | <span data-ttu-id="c6ed3-117">Średni</span><span class="sxs-lookup"><span data-stu-id="c6ed3-117">Avg.</span></span> <span data-ttu-id="c6ed3-118">Czas dysku w s/Odczyt</span><span class="sxs-lookup"><span data-stu-id="c6ed3-118">Disk sec/Read</span></span> |
| <span data-ttu-id="c6ed3-119">Dysk fizyczny (na dysku)</span><span class="sxs-lookup"><span data-stu-id="c6ed3-119">PhysicalDisk(per Disk)</span></span> | <span data-ttu-id="c6ed3-120">Średni</span><span class="sxs-lookup"><span data-stu-id="c6ed3-120">Avg.</span></span> <span data-ttu-id="c6ed3-121">Dysku w s/Zapis</span><span class="sxs-lookup"><span data-stu-id="c6ed3-121">Disk sec/Write</span></span> |
| <span data-ttu-id="c6ed3-122">Dysk fizyczny (na dysku)</span><span class="sxs-lookup"><span data-stu-id="c6ed3-122">PhysicalDisk(per Disk)</span></span> | <span data-ttu-id="c6ed3-123">Odczyty dysku/s</span><span class="sxs-lookup"><span data-stu-id="c6ed3-123">Disk Reads/sec</span></span> |
| <span data-ttu-id="c6ed3-124">Dysk fizyczny (na dysku)</span><span class="sxs-lookup"><span data-stu-id="c6ed3-124">PhysicalDisk(per Disk)</span></span> | <span data-ttu-id="c6ed3-125">Bajty odczytu dysku/s</span><span class="sxs-lookup"><span data-stu-id="c6ed3-125">Disk Read Bytes/sec</span></span> |
| <span data-ttu-id="c6ed3-126">Dysk fizyczny (na dysku)</span><span class="sxs-lookup"><span data-stu-id="c6ed3-126">PhysicalDisk(per Disk)</span></span> | <span data-ttu-id="c6ed3-127">Zapisy dysku/s</span><span class="sxs-lookup"><span data-stu-id="c6ed3-127">Disk Writes/sec</span></span> |
| <span data-ttu-id="c6ed3-128">Dysk fizyczny (na dysku)</span><span class="sxs-lookup"><span data-stu-id="c6ed3-128">PhysicalDisk(per Disk)</span></span> | <span data-ttu-id="c6ed3-129">Bajty zapisu dysku/s</span><span class="sxs-lookup"><span data-stu-id="c6ed3-129">Disk Write Bytes/sec</span></span> |
| <span data-ttu-id="c6ed3-130">Memory (Pamięć)</span><span class="sxs-lookup"><span data-stu-id="c6ed3-130">Memory</span></span> | <span data-ttu-id="c6ed3-131">Dostępna pamięć (MB)</span><span class="sxs-lookup"><span data-stu-id="c6ed3-131">Available MBytes</span></span> |
| <span data-ttu-id="c6ed3-132">Plik stronicowania</span><span class="sxs-lookup"><span data-stu-id="c6ed3-132">PagingFile</span></span> | <span data-ttu-id="c6ed3-133">% Użycia</span><span class="sxs-lookup"><span data-stu-id="c6ed3-133">% Usage</span></span> |
| <span data-ttu-id="c6ed3-134">Process(Total)</span><span class="sxs-lookup"><span data-stu-id="c6ed3-134">Process(Total)</span></span> | <span data-ttu-id="c6ed3-135">Czas procesora (%)</span><span class="sxs-lookup"><span data-stu-id="c6ed3-135">% Processor Time</span></span> |
| <span data-ttu-id="c6ed3-136">Proces (usługi)</span><span class="sxs-lookup"><span data-stu-id="c6ed3-136">Process (per service)</span></span> | <span data-ttu-id="c6ed3-137">Czas procesora (%)</span><span class="sxs-lookup"><span data-stu-id="c6ed3-137">% Processor Time</span></span> |
| <span data-ttu-id="c6ed3-138">Proces (usługi)</span><span class="sxs-lookup"><span data-stu-id="c6ed3-138">Process (per service)</span></span> | <span data-ttu-id="c6ed3-139">Identyfikator procesu</span><span class="sxs-lookup"><span data-stu-id="c6ed3-139">ID Process</span></span> |
| <span data-ttu-id="c6ed3-140">Proces (usługi)</span><span class="sxs-lookup"><span data-stu-id="c6ed3-140">Process (per service)</span></span> | <span data-ttu-id="c6ed3-141">Bajty prywatne</span><span class="sxs-lookup"><span data-stu-id="c6ed3-141">Private Bytes</span></span> |
| <span data-ttu-id="c6ed3-142">Proces (usługi)</span><span class="sxs-lookup"><span data-stu-id="c6ed3-142">Process (per service)</span></span> | <span data-ttu-id="c6ed3-143">Liczba wątków</span><span class="sxs-lookup"><span data-stu-id="c6ed3-143">Thread Count</span></span> |
| <span data-ttu-id="c6ed3-144">Proces (usługi)</span><span class="sxs-lookup"><span data-stu-id="c6ed3-144">Process (per service)</span></span> | <span data-ttu-id="c6ed3-145">Licznik Bajty wirtualne</span><span class="sxs-lookup"><span data-stu-id="c6ed3-145">Virtual Bytes</span></span> |
| <span data-ttu-id="c6ed3-146">Proces (usługi)</span><span class="sxs-lookup"><span data-stu-id="c6ed3-146">Process (per service)</span></span> | <span data-ttu-id="c6ed3-147">Zestaw roboczy</span><span class="sxs-lookup"><span data-stu-id="c6ed3-147">Working Set</span></span> |
| <span data-ttu-id="c6ed3-148">Proces (usługi)</span><span class="sxs-lookup"><span data-stu-id="c6ed3-148">Process (per service)</span></span> | <span data-ttu-id="c6ed3-149">Zestaw roboczy — prywatny</span><span class="sxs-lookup"><span data-stu-id="c6ed3-149">Working Set - Private</span></span> |

## <a name="net-applications-and-services"></a><span data-ttu-id="c6ed3-150">Usługi i aplikacje środowiska .NET.</span><span class="sxs-lookup"><span data-stu-id="c6ed3-150">.NET applications and services</span></span>

<span data-ttu-id="c6ed3-151">Zbierz następujące liczniki, Jeżeli wdrażasz usług .NET do klastra.</span><span class="sxs-lookup"><span data-stu-id="c6ed3-151">Collect the following counters if you are deploying .NET services to your cluster.</span></span> 

| <span data-ttu-id="c6ed3-152">Kategoria licznika</span><span class="sxs-lookup"><span data-stu-id="c6ed3-152">Counter Category</span></span> | <span data-ttu-id="c6ed3-153">Nazwa licznika</span><span class="sxs-lookup"><span data-stu-id="c6ed3-153">Counter Name</span></span> |
| --- | --- |
| <span data-ttu-id="c6ed3-154">.NET CLR pamięci (dla usługi)</span><span class="sxs-lookup"><span data-stu-id="c6ed3-154">.NET CLR Memory (per service)</span></span> | <span data-ttu-id="c6ed3-155">Identyfikator procesu</span><span class="sxs-lookup"><span data-stu-id="c6ed3-155">Process ID</span></span> |
| <span data-ttu-id="c6ed3-156">.NET CLR pamięci (dla usługi)</span><span class="sxs-lookup"><span data-stu-id="c6ed3-156">.NET CLR Memory (per service)</span></span> | <span data-ttu-id="c6ed3-157"># Całkowita liczba Zadeklarowane bajty</span><span class="sxs-lookup"><span data-stu-id="c6ed3-157"># Total committed Bytes</span></span> |
| <span data-ttu-id="c6ed3-158">.NET CLR pamięci (dla usługi)</span><span class="sxs-lookup"><span data-stu-id="c6ed3-158">.NET CLR Memory (per service)</span></span> | <span data-ttu-id="c6ed3-159"># Całkowita liczba zastrzeżone bajtów</span><span class="sxs-lookup"><span data-stu-id="c6ed3-159"># Total reserved Bytes</span></span> |
| <span data-ttu-id="c6ed3-160">.NET CLR pamięci (dla usługi)</span><span class="sxs-lookup"><span data-stu-id="c6ed3-160">.NET CLR Memory (per service)</span></span> | <span data-ttu-id="c6ed3-161">Liczba bajtów we wszystkich Stertach</span><span class="sxs-lookup"><span data-stu-id="c6ed3-161"># Bytes in all Heaps</span></span> |
| <span data-ttu-id="c6ed3-162">.NET CLR pamięci (dla usługi)</span><span class="sxs-lookup"><span data-stu-id="c6ed3-162">.NET CLR Memory (per service)</span></span> | <span data-ttu-id="c6ed3-163"># Kolekcje pokolenia 0</span><span class="sxs-lookup"><span data-stu-id="c6ed3-163"># Gen 0 Collections</span></span> |
| <span data-ttu-id="c6ed3-164">.NET CLR pamięci (dla usługi)</span><span class="sxs-lookup"><span data-stu-id="c6ed3-164">.NET CLR Memory (per service)</span></span> | <span data-ttu-id="c6ed3-165"># Kolekcje gen 1</span><span class="sxs-lookup"><span data-stu-id="c6ed3-165"># Gen 1 Collections</span></span> |
| <span data-ttu-id="c6ed3-166">.NET CLR pamięci (dla usługi)</span><span class="sxs-lookup"><span data-stu-id="c6ed3-166">.NET CLR Memory (per service)</span></span> | <span data-ttu-id="c6ed3-167"># Kolekcje gen 2</span><span class="sxs-lookup"><span data-stu-id="c6ed3-167"># Gen 2 Collections</span></span> |
| <span data-ttu-id="c6ed3-168">.NET CLR pamięci (dla usługi)</span><span class="sxs-lookup"><span data-stu-id="c6ed3-168">.NET CLR Memory (per service)</span></span> | <span data-ttu-id="c6ed3-169">% Czasu odzyskiwania pamięci</span><span class="sxs-lookup"><span data-stu-id="c6ed3-169">% Time in GC</span></span> |

### <a name="service-fabrics-custom-performance-counters"></a><span data-ttu-id="c6ed3-170">Usługa sieć szkieletowa niestandardowe liczniki wydajności</span><span class="sxs-lookup"><span data-stu-id="c6ed3-170">Service Fabric's custom performance counters</span></span>

<span data-ttu-id="c6ed3-171">Sieć szkieletowa usług generuje rozległe niestandardowe liczniki wydajności.</span><span class="sxs-lookup"><span data-stu-id="c6ed3-171">Service Fabric generates a substantial amount of custom performance counters.</span></span> <span data-ttu-id="c6ed3-172">Jeśli masz zainstalowany zestaw SDK, zostanie wyświetlona lista kompleksowe na komputerze z systemem Windows, w Monitorze wydajności aplikacji (Start > monitora wydajności).</span><span class="sxs-lookup"><span data-stu-id="c6ed3-172">If you have the SDK installed, you can see the comprehensive list on your Windows machine in your Performance Monitor application (Start > Performance Monitor).</span></span> 

<span data-ttu-id="c6ed3-173">W aplikacjach wdrażasz do klastra, jeśli używasz Reliable Actors, Dodaj countes z `Service Fabric Actor` i `Service Fabric Actor Method` kategorii (zobacz [usługi sieć szkieletowa niezawodnej podmiotów diagnostyki](service-fabric-reliable-actors-diagnostics.md)).</span><span class="sxs-lookup"><span data-stu-id="c6ed3-173">In the applications you are deploying to your cluster, if you are using Reliable Actors, add countes from `Service Fabric Actor` and `Service Fabric Actor Method` categories (see [Service Fabric Reliable Actors Diagnostics](service-fabric-reliable-actors-diagnostics.md)).</span></span>

<span data-ttu-id="c6ed3-174">Jeśli używasz usługi niezawodnego podobnie mamy `Service Fabric Service` i `Service Fabric Service Method` kategorii licznika, które należy zebrać liczników z.</span><span class="sxs-lookup"><span data-stu-id="c6ed3-174">If you use Reliable Services, we similarly have `Service Fabric Service` and `Service Fabric Service Method` counter categories that you should collect counters from.</span></span> 

<span data-ttu-id="c6ed3-175">Użycie niezawodnej kolekcje, zaleca się dodawania `Avg. Transaction ms/Commit` z `Service Fabric Transactional Replicator` zbierać opóźnienie zatwierdzania średni na Metryka transakcji.</span><span class="sxs-lookup"><span data-stu-id="c6ed3-175">If you use Reliable Collections, we recommend adding the `Avg. Transaction ms/Commit` from the `Service Fabric Transactional Replicator` to collect the average commit latency per transaction metric.</span></span>


## <a name="next-steps"></a><span data-ttu-id="c6ed3-176">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="c6ed3-176">Next steps</span></span>

* <span data-ttu-id="c6ed3-177">Dowiedz się więcej o [generowania zdarzeń na poziomie platformy](service-fabric-diagnostics-event-generation-infra.md) w sieci szkieletowej usług</span><span class="sxs-lookup"><span data-stu-id="c6ed3-177">Learn more about [event generation at the platform level](service-fabric-diagnostics-event-generation-infra.md) in Service Fabric</span></span>
* <span data-ttu-id="c6ed3-178">Zbieranie metryk wydajności za pośrednictwem [diagnostyki Azure](service-fabric-diagnostics-event-aggregation-wad.md)</span><span class="sxs-lookup"><span data-stu-id="c6ed3-178">Collect performance metrics through [Azure Diagnostics](service-fabric-diagnostics-event-aggregation-wad.md)</span></span>
