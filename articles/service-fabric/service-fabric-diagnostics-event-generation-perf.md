---
title: "Monitorowanie wydajności sieci szkieletowej usług aaaAzure | Dokumentacja firmy Microsoft"
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
ms.openlocfilehash: 54d4c62b7250a1f70b0898ba07ae5a37716f4cf4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="performance-metrics"></a><span data-ttu-id="8473c-103">Metryki wydajności</span><span class="sxs-lookup"><span data-stu-id="8473c-103">Performance metrics</span></span>

<span data-ttu-id="8473c-104">Metryki powinien toounderstand zebranych hello wydajności klastra można także aplikacji hello uruchomionych w niej.</span><span class="sxs-lookup"><span data-stu-id="8473c-104">Metrics should be collected toounderstand hello performance of your cluster as well as hello applications running in it.</span></span> <span data-ttu-id="8473c-105">Dla klastrów sieci szkieletowej usług firma Microsoft zaleca zbieranie hello następujące liczniki wydajności.</span><span class="sxs-lookup"><span data-stu-id="8473c-105">For Service Fabric clusters, we recommend collecting hello following performance counters.</span></span>

## <a name="nodes"></a><span data-ttu-id="8473c-106">Węzły</span><span class="sxs-lookup"><span data-stu-id="8473c-106">Nodes</span></span>

<span data-ttu-id="8473c-107">Witaj maszyn w klastrze należy wziąć pod uwagę zbieranie hello następujące liczniki wydajności toobetter zrozumieć hello obciążenia na każdej maszynie i wprowadzić odpowiednie klastra skalowanie decyzji.</span><span class="sxs-lookup"><span data-stu-id="8473c-107">For hello machines in your cluster, consider collecting hello following performance counters toobetter understand hello load on each machine and make appropriate cluster scaling decisions.</span></span>

| <span data-ttu-id="8473c-108">Kategoria licznika</span><span class="sxs-lookup"><span data-stu-id="8473c-108">Counter Category</span></span> | <span data-ttu-id="8473c-109">Nazwa licznika</span><span class="sxs-lookup"><span data-stu-id="8473c-109">Counter Name</span></span> |
| --- | --- |
| <span data-ttu-id="8473c-110">Dysk fizyczny (na dysku)</span><span class="sxs-lookup"><span data-stu-id="8473c-110">PhysicalDisk(per Disk)</span></span> | <span data-ttu-id="8473c-111">Średni Długość kolejki odczytu dysku</span><span class="sxs-lookup"><span data-stu-id="8473c-111">Avg. Disk Read Queue Length</span></span> |
| <span data-ttu-id="8473c-112">Dysk fizyczny (na dysku)</span><span class="sxs-lookup"><span data-stu-id="8473c-112">PhysicalDisk(per Disk)</span></span> | <span data-ttu-id="8473c-113">Średni Długość kolejki dysku zapisu</span><span class="sxs-lookup"><span data-stu-id="8473c-113">Avg. Disk Write Queue Length</span></span> |
| <span data-ttu-id="8473c-114">Dysk fizyczny (na dysku)</span><span class="sxs-lookup"><span data-stu-id="8473c-114">PhysicalDisk(per Disk)</span></span> | <span data-ttu-id="8473c-115">Średni Czas dysku w s/Odczyt</span><span class="sxs-lookup"><span data-stu-id="8473c-115">Avg. Disk sec/Read</span></span> |
| <span data-ttu-id="8473c-116">Dysk fizyczny (na dysku)</span><span class="sxs-lookup"><span data-stu-id="8473c-116">PhysicalDisk(per Disk)</span></span> | <span data-ttu-id="8473c-117">Średni Dysku w s/Zapis</span><span class="sxs-lookup"><span data-stu-id="8473c-117">Avg. Disk sec/Write</span></span> |
| <span data-ttu-id="8473c-118">Dysk fizyczny (na dysku)</span><span class="sxs-lookup"><span data-stu-id="8473c-118">PhysicalDisk(per Disk)</span></span> | <span data-ttu-id="8473c-119">Odczyty dysku/s</span><span class="sxs-lookup"><span data-stu-id="8473c-119">Disk Reads/sec</span></span> |
| <span data-ttu-id="8473c-120">Dysk fizyczny (na dysku)</span><span class="sxs-lookup"><span data-stu-id="8473c-120">PhysicalDisk(per Disk)</span></span> | <span data-ttu-id="8473c-121">Bajty odczytu dysku/s</span><span class="sxs-lookup"><span data-stu-id="8473c-121">Disk Read Bytes/sec</span></span> |
| <span data-ttu-id="8473c-122">Dysk fizyczny (na dysku)</span><span class="sxs-lookup"><span data-stu-id="8473c-122">PhysicalDisk(per Disk)</span></span> | <span data-ttu-id="8473c-123">Zapisy dysku/s</span><span class="sxs-lookup"><span data-stu-id="8473c-123">Disk Writes/sec</span></span> |
| <span data-ttu-id="8473c-124">Dysk fizyczny (na dysku)</span><span class="sxs-lookup"><span data-stu-id="8473c-124">PhysicalDisk(per Disk)</span></span> | <span data-ttu-id="8473c-125">Bajty zapisu dysku/s</span><span class="sxs-lookup"><span data-stu-id="8473c-125">Disk Write Bytes/sec</span></span> |
| <span data-ttu-id="8473c-126">Memory (Pamięć)</span><span class="sxs-lookup"><span data-stu-id="8473c-126">Memory</span></span> | <span data-ttu-id="8473c-127">Dostępna pamięć (MB)</span><span class="sxs-lookup"><span data-stu-id="8473c-127">Available MBytes</span></span> |
| <span data-ttu-id="8473c-128">Plik stronicowania</span><span class="sxs-lookup"><span data-stu-id="8473c-128">PagingFile</span></span> | <span data-ttu-id="8473c-129">% Użycia</span><span class="sxs-lookup"><span data-stu-id="8473c-129">% Usage</span></span> |
| <span data-ttu-id="8473c-130">Process(Total)</span><span class="sxs-lookup"><span data-stu-id="8473c-130">Process(Total)</span></span> | <span data-ttu-id="8473c-131">Czas procesora (%)</span><span class="sxs-lookup"><span data-stu-id="8473c-131">% Processor Time</span></span> |
| <span data-ttu-id="8473c-132">Proces (usługi)</span><span class="sxs-lookup"><span data-stu-id="8473c-132">Process (per service)</span></span> | <span data-ttu-id="8473c-133">Czas procesora (%)</span><span class="sxs-lookup"><span data-stu-id="8473c-133">% Processor Time</span></span> |
| <span data-ttu-id="8473c-134">Proces (usługi)</span><span class="sxs-lookup"><span data-stu-id="8473c-134">Process (per service)</span></span> | <span data-ttu-id="8473c-135">Identyfikator procesu</span><span class="sxs-lookup"><span data-stu-id="8473c-135">ID Process</span></span> |
| <span data-ttu-id="8473c-136">Proces (usługi)</span><span class="sxs-lookup"><span data-stu-id="8473c-136">Process (per service)</span></span> | <span data-ttu-id="8473c-137">Bajty prywatne</span><span class="sxs-lookup"><span data-stu-id="8473c-137">Private Bytes</span></span> |
| <span data-ttu-id="8473c-138">Proces (usługi)</span><span class="sxs-lookup"><span data-stu-id="8473c-138">Process (per service)</span></span> | <span data-ttu-id="8473c-139">Liczba wątków</span><span class="sxs-lookup"><span data-stu-id="8473c-139">Thread Count</span></span> |
| <span data-ttu-id="8473c-140">Proces (usługi)</span><span class="sxs-lookup"><span data-stu-id="8473c-140">Process (per service)</span></span> | <span data-ttu-id="8473c-141">Licznik Bajty wirtualne</span><span class="sxs-lookup"><span data-stu-id="8473c-141">Virtual Bytes</span></span> |
| <span data-ttu-id="8473c-142">Proces (usługi)</span><span class="sxs-lookup"><span data-stu-id="8473c-142">Process (per service)</span></span> | <span data-ttu-id="8473c-143">Zestaw roboczy</span><span class="sxs-lookup"><span data-stu-id="8473c-143">Working Set</span></span> |
| <span data-ttu-id="8473c-144">Proces (usługi)</span><span class="sxs-lookup"><span data-stu-id="8473c-144">Process (per service)</span></span> | <span data-ttu-id="8473c-145">Zestaw roboczy — prywatny</span><span class="sxs-lookup"><span data-stu-id="8473c-145">Working Set - Private</span></span> |

## <a name="net-applications-and-services"></a><span data-ttu-id="8473c-146">Usługi i aplikacje środowiska .NET.</span><span class="sxs-lookup"><span data-stu-id="8473c-146">.NET applications and services</span></span>

<span data-ttu-id="8473c-147">Zbierz następujące liczniki wdrażania klastra tooyour usług .NET hello.</span><span class="sxs-lookup"><span data-stu-id="8473c-147">Collect hello following counters if you are deploying .NET services tooyour cluster.</span></span> 

| <span data-ttu-id="8473c-148">Kategoria licznika</span><span class="sxs-lookup"><span data-stu-id="8473c-148">Counter Category</span></span> | <span data-ttu-id="8473c-149">Nazwa licznika</span><span class="sxs-lookup"><span data-stu-id="8473c-149">Counter Name</span></span> |
| --- | --- |
| <span data-ttu-id="8473c-150">.NET CLR pamięci (dla usługi)</span><span class="sxs-lookup"><span data-stu-id="8473c-150">.NET CLR Memory (per service)</span></span> | <span data-ttu-id="8473c-151">Identyfikator procesu</span><span class="sxs-lookup"><span data-stu-id="8473c-151">Process ID</span></span> |
| <span data-ttu-id="8473c-152">.NET CLR pamięci (dla usługi)</span><span class="sxs-lookup"><span data-stu-id="8473c-152">.NET CLR Memory (per service)</span></span> | <span data-ttu-id="8473c-153"># Całkowita liczba Zadeklarowane bajty</span><span class="sxs-lookup"><span data-stu-id="8473c-153"># Total committed Bytes</span></span> |
| <span data-ttu-id="8473c-154">.NET CLR pamięci (dla usługi)</span><span class="sxs-lookup"><span data-stu-id="8473c-154">.NET CLR Memory (per service)</span></span> | <span data-ttu-id="8473c-155"># Całkowita liczba zastrzeżone bajtów</span><span class="sxs-lookup"><span data-stu-id="8473c-155"># Total reserved Bytes</span></span> |
| <span data-ttu-id="8473c-156">.NET CLR pamięci (dla usługi)</span><span class="sxs-lookup"><span data-stu-id="8473c-156">.NET CLR Memory (per service)</span></span> | <span data-ttu-id="8473c-157">Liczba bajtów we wszystkich Stertach</span><span class="sxs-lookup"><span data-stu-id="8473c-157"># Bytes in all Heaps</span></span> |
| <span data-ttu-id="8473c-158">.NET CLR pamięci (dla usługi)</span><span class="sxs-lookup"><span data-stu-id="8473c-158">.NET CLR Memory (per service)</span></span> | <span data-ttu-id="8473c-159"># Kolekcje pokolenia 0</span><span class="sxs-lookup"><span data-stu-id="8473c-159"># Gen 0 Collections</span></span> |
| <span data-ttu-id="8473c-160">.NET CLR pamięci (dla usługi)</span><span class="sxs-lookup"><span data-stu-id="8473c-160">.NET CLR Memory (per service)</span></span> | <span data-ttu-id="8473c-161"># Kolekcje gen 1</span><span class="sxs-lookup"><span data-stu-id="8473c-161"># Gen 1 Collections</span></span> |
| <span data-ttu-id="8473c-162">.NET CLR pamięci (dla usługi)</span><span class="sxs-lookup"><span data-stu-id="8473c-162">.NET CLR Memory (per service)</span></span> | <span data-ttu-id="8473c-163"># Kolekcje gen 2</span><span class="sxs-lookup"><span data-stu-id="8473c-163"># Gen 2 Collections</span></span> |
| <span data-ttu-id="8473c-164">.NET CLR pamięci (dla usługi)</span><span class="sxs-lookup"><span data-stu-id="8473c-164">.NET CLR Memory (per service)</span></span> | <span data-ttu-id="8473c-165">% Czasu odzyskiwania pamięci</span><span class="sxs-lookup"><span data-stu-id="8473c-165">% Time in GC</span></span> |

### <a name="service-fabrics-custom-performance-counters"></a><span data-ttu-id="8473c-166">Usługa sieć szkieletowa niestandardowe liczniki wydajności</span><span class="sxs-lookup"><span data-stu-id="8473c-166">Service Fabric's custom performance counters</span></span>

<span data-ttu-id="8473c-167">Sieć szkieletowa usług generuje rozległe niestandardowe liczniki wydajności.</span><span class="sxs-lookup"><span data-stu-id="8473c-167">Service Fabric generates a substantial amount of custom performance counters.</span></span> <span data-ttu-id="8473c-168">Jeśli masz hello zainstalowany zestaw SDK, zostanie wyświetlona lista kompleksowe hello na komputerze z systemem Windows, w Monitorze wydajności aplikacji (Start > monitora wydajności).</span><span class="sxs-lookup"><span data-stu-id="8473c-168">If you have hello SDK installed, you can see hello comprehensive list on your Windows machine in your Performance Monitor application (Start > Performance Monitor).</span></span> 

<span data-ttu-id="8473c-169">W aplikacji hello wdrażasz tooyour klastra, jeśli używasz Reliable Actors, Dodaj countes z `Service Fabric Actor` i `Service Fabric Actor Method` kategorii (zobacz [usługi sieć szkieletowa niezawodnej podmiotów diagnostyki](service-fabric-reliable-actors-diagnostics.md)).</span><span class="sxs-lookup"><span data-stu-id="8473c-169">In hello applications you are deploying tooyour cluster, if you are using Reliable Actors, add countes from `Service Fabric Actor` and `Service Fabric Actor Method` categories (see [Service Fabric Reliable Actors Diagnostics](service-fabric-reliable-actors-diagnostics.md)).</span></span>

<span data-ttu-id="8473c-170">Jeśli używasz usługi niezawodnego podobnie mamy `Service Fabric Service` i `Service Fabric Service Method` kategorii licznika, które należy zebrać liczników z.</span><span class="sxs-lookup"><span data-stu-id="8473c-170">If you use Reliable Services, we similarly have `Service Fabric Service` and `Service Fabric Service Method` counter categories that you should collect counters from.</span></span> 

<span data-ttu-id="8473c-171">Jeśli używasz niezawodnej kolekcje, zaleca się dodawania hello `Avg. Transaction ms/Commit` z hello `Service Fabric Transactional Replicator` opóźnienie zatwierdzania średni hello toocollect na Metryka transakcji.</span><span class="sxs-lookup"><span data-stu-id="8473c-171">If you use Reliable Collections, we recommend adding hello `Avg. Transaction ms/Commit` from hello `Service Fabric Transactional Replicator` toocollect hello average commit latency per transaction metric.</span></span>


## <a name="next-steps"></a><span data-ttu-id="8473c-172">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="8473c-172">Next steps</span></span>

* <span data-ttu-id="8473c-173">Dowiedz się więcej o [generowania zdarzeń na poziomie platformy hello](service-fabric-diagnostics-event-generation-infra.md) w sieci szkieletowej usług</span><span class="sxs-lookup"><span data-stu-id="8473c-173">Learn more about [event generation at hello platform level](service-fabric-diagnostics-event-generation-infra.md) in Service Fabric</span></span>
* <span data-ttu-id="8473c-174">Zbieranie metryk wydajności za pośrednictwem [diagnostyki Azure](service-fabric-diagnostics-event-aggregation-wad.md)</span><span class="sxs-lookup"><span data-stu-id="8473c-174">Collect performance metrics through [Azure Diagnostics](service-fabric-diagnostics-event-aggregation-wad.md)</span></span>
