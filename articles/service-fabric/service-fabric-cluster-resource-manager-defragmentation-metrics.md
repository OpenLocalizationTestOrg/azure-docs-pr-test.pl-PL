---
title: "Defragmentacja metryki w sieci szkieletowej usług Azure | Dokumentacja firmy Microsoft"
description: "Omówienie przy użyciu defragmentacji lub pakowania jako strategię metryki w sieci szkieletowej usług"
services: service-fabric
documentationcenter: .net
author: masnider
manager: timlt
editor: 
ms.assetid: e5ebfae5-c8f7-4d6c-9173-3e22a9730552
ms.service: Service-Fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/18/2017
ms.author: masnider
ms.openlocfilehash: b253cc07066092aa82d218c9c82c8aac502245a8
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/18/2017
---
# <a name="defragmentation-of-metrics-and-load-in-service-fabric"></a><span data-ttu-id="dd2e2-103">Defragmentacja metryki i obciążenia w sieci szkieletowej usług</span><span class="sxs-lookup"><span data-stu-id="dd2e2-103">Defragmentation of metrics and load in Service Fabric</span></span>
<span data-ttu-id="dd2e2-104">Strategię domyślnego menedżera zasobów klastra sieci szkieletowej usług zarządzania metryki obciążenia w klastrze jest rozkładanie obciążenia.</span><span class="sxs-lookup"><span data-stu-id="dd2e2-104">The Service Fabric Cluster Resource Manager's default strategy for managing load metrics in the cluster is to distribute the load.</span></span> <span data-ttu-id="dd2e2-105">Zapewnienie, że węzły są wykorzystywane równomiernie pozwala uniknąć gorącego i zimnych miejsc prowadzących do rywalizacji i nieużywanego zasobów.</span><span class="sxs-lookup"><span data-stu-id="dd2e2-105">Ensuring that nodes are evenly utilized avoids hot and cold spots that lead to both contention and wasted resources.</span></span> <span data-ttu-id="dd2e2-106">Dystrybucji obciążeń w klastrze jest również najbezpieczniejszy pod względem pozostałych błędy, ponieważ gwarantuje, że błąd nie Wyjmij znaczną część danego obciążenia.</span><span class="sxs-lookup"><span data-stu-id="dd2e2-106">Distributing workloads in the cluster is also the safest in terms of surviving failures since it ensures that a failure doesn’t take out a large percentage of a given workload.</span></span> 

<span data-ttu-id="dd2e2-107">Menedżer zasobów klastra sieci szkieletowej usług obsługę zarządzania obciążenia, który jest defragmentacji innych strategii.</span><span class="sxs-lookup"><span data-stu-id="dd2e2-107">The Service Fabric Cluster Resource Manager does support a different strategy for managing load, which is defragmentation.</span></span> <span data-ttu-id="dd2e2-108">Defragmentacja oznacza, że zamiast w trakcie rozpowszechniają wykorzystania metryki klastra, jego są konsolidowane.</span><span class="sxs-lookup"><span data-stu-id="dd2e2-108">Defragmentation means that instead of trying to distribute the utilization of a metric across the cluster, it is consolidated.</span></span> <span data-ttu-id="dd2e2-109">Konsolidacji jest po prostu odwracanie domyślne równoważenie strategii — zamiast minimalizując odchylenie standardowe średni metryki obciążenia, próbuje powinna ona być Menedżera zasobów klastra.</span><span class="sxs-lookup"><span data-stu-id="dd2e2-109">Consolidation is just an inversion of the default balancing strategy – instead of minimizing the average standard deviation of metric load, the Cluster Resource Manager tries to increase it.</span></span>

## <a name="when-to-use-defragmentation"></a><span data-ttu-id="dd2e2-110">Kiedy należy używać defragmentacji</span><span class="sxs-lookup"><span data-stu-id="dd2e2-110">When to use defragmentation</span></span>
<span data-ttu-id="dd2e2-111">Dystrybucja obciążenia w klastrze zużywa niektórych zasobów w każdym węźle.</span><span class="sxs-lookup"><span data-stu-id="dd2e2-111">Distributing load in the cluster consumes some of the resources on each node.</span></span> <span data-ttu-id="dd2e2-112">Niektórych zadań tworzenia usług, które są wyjątkowo dużą i używać większości lub wszystkich węzła.</span><span class="sxs-lookup"><span data-stu-id="dd2e2-112">Some workloads create services that are exceptionally large and consume most or all of a node.</span></span> <span data-ttu-id="dd2e2-113">W takich przypadkach jest to możliwe, że w przypadku dużych obciążeń, uzyskiwanie utworzony nie ma wystarczającej ilości miejsca na dowolnym węźle, aby uruchomić je.</span><span class="sxs-lookup"><span data-stu-id="dd2e2-113">In these cases, it's possible that when there are large workloads getting created that there isn't enough space on any node to run them.</span></span> <span data-ttu-id="dd2e2-114">Duże obciążenia nie są problem w sieci szkieletowej usług; w takich przypadkach klaster Resource Manager ustala, że potrzebuje do klastra, aby zwolnić miejsce dla to duże obciążenie reorganizowanie.</span><span class="sxs-lookup"><span data-stu-id="dd2e2-114">Large workloads aren't a problem in Service Fabric; in these cases the Cluster Resource Manager determines that it needs to reorganize the cluster to make room for this large workload.</span></span> <span data-ttu-id="dd2e2-115">Jednak w tym samym czasie aby obciążenie ma czekać do zaplanowania w klastrze.</span><span class="sxs-lookup"><span data-stu-id="dd2e2-115">However, in the meantime that workload has to wait to be scheduled in the cluster.</span></span>

<span data-ttu-id="dd2e2-116">Jeśli istnieje wiele usług i stanie, aby przenosić, jego może potrwać długo duże obciążenie można umieścić w klastrze.</span><span class="sxs-lookup"><span data-stu-id="dd2e2-116">If there are many services and state to move around, then it could take a long time for the large workload to be placed in the cluster.</span></span> <span data-ttu-id="dd2e2-117">Jest to bardziej prawdopodobne, jeśli inne obciążenia w klastrze są także duży i dlatego trwać dłużej reorganizować.</span><span class="sxs-lookup"><span data-stu-id="dd2e2-117">This is more likely if other workloads in the cluster are also large and so take longer to reorganize.</span></span> <span data-ttu-id="dd2e2-118">Zespół usługi sieć szkieletowa mierzone czasy tworzenia w symulacji tego scenariusza.</span><span class="sxs-lookup"><span data-stu-id="dd2e2-118">The Service Fabric team measured creation times in simulations of this scenario.</span></span> <span data-ttu-id="dd2e2-119">Znaleziono się, że tworzenie dużych usług trwało dłużej zaraz po wykorzystaniu klastra otrzymano powyżej od 30% do 50%.</span><span class="sxs-lookup"><span data-stu-id="dd2e2-119">We found that creating large services took much longer as soon as cluster utilization got above between 30% and 50%.</span></span> <span data-ttu-id="dd2e2-120">Aby obsługiwać ten scenariusz, wprowadzono defragmentacji jako równoważenia strategii.</span><span class="sxs-lookup"><span data-stu-id="dd2e2-120">To handle this scenario, we introduced defragmentation as a balancing strategy.</span></span> <span data-ttu-id="dd2e2-121">Znaleziono się, że w przypadku dużych obciążeń, zwłaszcza tych, których czas utworzenia było ważne defragmentacji naprawdę pomocne te nowe obciążenia są planowane w klastrze.</span><span class="sxs-lookup"><span data-stu-id="dd2e2-121">We found that for large workloads, especially ones where creation time was important, defragmentation really helped those new workloads get scheduled in the cluster.</span></span>

<span data-ttu-id="dd2e2-122">Można skonfigurować metryki defragmentacji mają Menedżera zasobów klastra, aby aktywnie spróbuj zmniejszyć obciążenie usługi do mniej węzłów.</span><span class="sxs-lookup"><span data-stu-id="dd2e2-122">You can configure defragmentation metrics to have the Cluster Resource Manager to proactively try to condense the load of the services into fewer nodes.</span></span> <span data-ttu-id="dd2e2-123">Pomaga to zapewnić, że jest prawie zawsze miejsca dla dużych usług bez reorganizacja klastra.</span><span class="sxs-lookup"><span data-stu-id="dd2e2-123">This helps ensure that there is almost always room for large services without reorganizing the cluster.</span></span> <span data-ttu-id="dd2e2-124">Brak konieczności reorganizować klastra umożliwia szybkie tworzenie dużych obciążeń.</span><span class="sxs-lookup"><span data-stu-id="dd2e2-124">Not having to reorganize the cluster allows creating large workloads quickly.</span></span>

<span data-ttu-id="dd2e2-125">Defragmentacja nie ma potrzeby większości użytkowników.</span><span class="sxs-lookup"><span data-stu-id="dd2e2-125">Most people don’t need defragmentation.</span></span> <span data-ttu-id="dd2e2-126">Usług są zwykle jest mały, więc nie jest trudne do odszukania miejsce dla nich w klastrze.</span><span class="sxs-lookup"><span data-stu-id="dd2e2-126">Services are usually be small, so it’s not hard to find room for them in the cluster.</span></span> <span data-ttu-id="dd2e2-127">Gdy reorganizacji jest możliwe, przechodzi ona szybko ponownie ponieważ większość usług są małe i mogą zostać przeniesione szybkie i równolegle.</span><span class="sxs-lookup"><span data-stu-id="dd2e2-127">When reorganization is possible, it goes quickly, again because most services are small and can be moved quickly and in parallel.</span></span> <span data-ttu-id="dd2e2-128">Jeśli jednak duże usług i należy je szybko utworzyć następnie strategii defragmentacji jest dla Ciebie.</span><span class="sxs-lookup"><span data-stu-id="dd2e2-128">However, if you have large services and need them created quickly then the defragmentation strategy is for you.</span></span> <span data-ttu-id="dd2e2-129">Omówiono wady i zalety używania defragmentacji dalej.</span><span class="sxs-lookup"><span data-stu-id="dd2e2-129">We'll discuss the tradeoffs of using defragmentation next.</span></span> 

## <a name="defragmentation-tradeoffs"></a><span data-ttu-id="dd2e2-130">Defragmentacja wady i zalety</span><span class="sxs-lookup"><span data-stu-id="dd2e2-130">Defragmentation tradeoffs</span></span>
<span data-ttu-id="dd2e2-131">Defragmentacji może zwiększyć impactfulness błędy, ponieważ w węzłach, które nie są uruchomione usługi więcej.</span><span class="sxs-lookup"><span data-stu-id="dd2e2-131">Defragmentation can increase impactfulness of failures, since more services are running on nodes that fail.</span></span> <span data-ttu-id="dd2e2-132">Defragmentacji także może zwiększyć koszty, ponieważ zasobów w klastrze, musi być przechowywany w rezerwy oczekiwanie na tworzenie dużych obciążeń.</span><span class="sxs-lookup"><span data-stu-id="dd2e2-132">Defragmentation can also increase costs, since resources in the cluster must be held in reserve, waiting for the creation of large workloads.</span></span>

<span data-ttu-id="dd2e2-133">Poniższy diagram zapewnia wizualną reprezentację dwa klastry, który defragmentacji i jedną, która nie jest.</span><span class="sxs-lookup"><span data-stu-id="dd2e2-133">The following diagram gives a visual representation of two clusters, one that is defragmented and one that is not.</span></span> 

<span data-ttu-id="dd2e2-134"><center>
![Porównywanie zrównoważonym i defragmentacji klastrów][Image1]
</center></span><span class="sxs-lookup"><span data-stu-id="dd2e2-134"><center>
![Comparing Balanced and Defragmented Clusters][Image1]
</center></span></span>

<span data-ttu-id="dd2e2-135">W przypadku zrównoważonym należy wziąć pod uwagę liczbę przesunięcia, które należy umieścić jedną z największych obiektów usługi.</span><span class="sxs-lookup"><span data-stu-id="dd2e2-135">In the balanced case, consider the number of movements that would be necessary to place one of the largest service objects.</span></span> <span data-ttu-id="dd2e2-136">W klastrze zdefragmentowanej duże obciążenie może umieścić w węzłów czterech lub pięciu bez potrzeby czekania na inne usługi przenieść.</span><span class="sxs-lookup"><span data-stu-id="dd2e2-136">In the defragmented cluster, the large workload could be placed on nodes four or five without having to wait for any other services to move.</span></span>

## <a name="defragmentation-pros-and-cons"></a><span data-ttu-id="dd2e2-137">Defragmentacja zalet i wad</span><span class="sxs-lookup"><span data-stu-id="dd2e2-137">Defragmentation pros and cons</span></span>
<span data-ttu-id="dd2e2-138">Co to są tych pojęć kompromisy?</span><span class="sxs-lookup"><span data-stu-id="dd2e2-138">So what are those other conceptual tradeoffs?</span></span> <span data-ttu-id="dd2e2-139">Poniżej przedstawiono szybki spis kwestii:</span><span class="sxs-lookup"><span data-stu-id="dd2e2-139">Here’s a quick table of things to think about:</span></span>

| <span data-ttu-id="dd2e2-140">Specjaliści defragmentacji</span><span class="sxs-lookup"><span data-stu-id="dd2e2-140">Defragmentation Pros</span></span> | <span data-ttu-id="dd2e2-141">Defragmentacja wad</span><span class="sxs-lookup"><span data-stu-id="dd2e2-141">Defragmentation Cons</span></span> |
| --- | --- |
| <span data-ttu-id="dd2e2-142">Umożliwia szybsze tworzenie dużych usług</span><span class="sxs-lookup"><span data-stu-id="dd2e2-142">Allows faster creation of large services</span></span> |<span data-ttu-id="dd2e2-143">Koncentraty obciążenia na mniejszą liczbę węzłów, zwiększenie rywalizacji</span><span class="sxs-lookup"><span data-stu-id="dd2e2-143">Concentrates load onto fewer nodes, increasing contention</span></span> |
| <span data-ttu-id="dd2e2-144">Umożliwia obniżyć przenoszenia danych podczas tworzenia</span><span class="sxs-lookup"><span data-stu-id="dd2e2-144">Enables lower data movement during creation</span></span> |<span data-ttu-id="dd2e2-145">Błędy może mieć wpływ na inne usługi i przenoszenie więcej</span><span class="sxs-lookup"><span data-stu-id="dd2e2-145">Failures can impact more services and cause more churn</span></span> |
| <span data-ttu-id="dd2e2-146">Umożliwia zaawansowane opis wymagań i odzyskiwanie miejsca</span><span class="sxs-lookup"><span data-stu-id="dd2e2-146">Allows rich description of requirements and reclamation of space</span></span> |<span data-ttu-id="dd2e2-147">Bardziej złożonych konfiguracji ogólnej zarządzanie zasobami</span><span class="sxs-lookup"><span data-stu-id="dd2e2-147">More complex overall Resource Management configuration</span></span> |

<span data-ttu-id="dd2e2-148">Można mieszać zdefragmentowanej i normalnym metryki w tym samym klastrze.</span><span class="sxs-lookup"><span data-stu-id="dd2e2-148">You can mix defragmented and normal metrics in the same cluster.</span></span> <span data-ttu-id="dd2e2-149">Menedżer zasobów klastra próbuje konsolidować możliwie często podczas rozkładanie innych metryk defragmentacji.</span><span class="sxs-lookup"><span data-stu-id="dd2e2-149">The Cluster Resource Manager tries to consolidate the defragmentation metrics as much as possible while spreading out the others.</span></span> <span data-ttu-id="dd2e2-150">Wyniki mieszanie defragmentacji i równoważenie strategii zależy od kilka czynników, takich jak:</span><span class="sxs-lookup"><span data-stu-id="dd2e2-150">The results of mixing defragmentation and balancing strategies depends on several factors, including:</span></span>
  - <span data-ttu-id="dd2e2-151">Liczba równoważenia metryki, a liczba defragmentacji metryk</span><span class="sxs-lookup"><span data-stu-id="dd2e2-151">the number of balancing metrics vs. the number of defragmentation metrics</span></span>
  - <span data-ttu-id="dd2e2-152">Określa, czy usługi używa obu typów metryk</span><span class="sxs-lookup"><span data-stu-id="dd2e2-152">Whether any service uses both types of metrics</span></span> 
  - <span data-ttu-id="dd2e2-153">metryki wag</span><span class="sxs-lookup"><span data-stu-id="dd2e2-153">the metric weights</span></span>
  - <span data-ttu-id="dd2e2-154">ładuje bieżący metryki</span><span class="sxs-lookup"><span data-stu-id="dd2e2-154">current metric loads</span></span>
  
<span data-ttu-id="dd2e2-155">Eksperymenty jest niezbędne do określenia dokładnej konfiguracji niezbędne.</span><span class="sxs-lookup"><span data-stu-id="dd2e2-155">Experimentation is required to determine the exact configuration necessary.</span></span> <span data-ttu-id="dd2e2-156">Zalecamy dokładne pomiary obciążeń przed włączeniem metryki defragmentacji w środowisku produkcyjnym.</span><span class="sxs-lookup"><span data-stu-id="dd2e2-156">We recommend thorough measurement of your workloads before you enable defragmentation metrics in production.</span></span> <span data-ttu-id="dd2e2-157">Dotyczy to zwłaszcza mieszanie defragmentacji i zrównoważonym metryki w ramach tej samej usługi.</span><span class="sxs-lookup"><span data-stu-id="dd2e2-157">This is especially true when mixing defragmentation and balanced metrics within the same service.</span></span> 

## <a name="configuring-defragmentation-metrics"></a><span data-ttu-id="dd2e2-158">Konfigurowanie metryki defragmentacji</span><span class="sxs-lookup"><span data-stu-id="dd2e2-158">Configuring defragmentation metrics</span></span>
<span data-ttu-id="dd2e2-159">Konfigurowanie metryki defragmentacji jest globalne decyzji w klastrze, a do defragmentacji można wybrać poszczególnych metryki.</span><span class="sxs-lookup"><span data-stu-id="dd2e2-159">Configuring defragmentation metrics is a global decision in the cluster, and individual metrics can be selected for defragmentation.</span></span> <span data-ttu-id="dd2e2-160">Poniższe fragmenty kodu config przedstawiają sposób konfigurowania metryki dla defragmentacji.</span><span class="sxs-lookup"><span data-stu-id="dd2e2-160">The following config snippets show how to configure metrics for defragmentation.</span></span> <span data-ttu-id="dd2e2-161">W takim przypadku "Metric1" jest skonfigurowana jako metrykę defragmentacji "Metric2" będzie nadal normalnie zrównoważenia.</span><span class="sxs-lookup"><span data-stu-id="dd2e2-161">In this case, "Metric1" is configured as a defragmentation metric, while "Metric2" will continue to be balanced normally.</span></span> 

<span data-ttu-id="dd2e2-162">ClusterManifest.xml:</span><span class="sxs-lookup"><span data-stu-id="dd2e2-162">ClusterManifest.xml:</span></span>

```xml
<Section Name="DefragmentationMetrics">
    <Parameter Name="Metric1" Value="true" />
    <Parameter Name="Metric2" Value="false" />
</Section>
```

<span data-ttu-id="dd2e2-163">za pomocą pliku ClusterConfig.json dla autonomicznych wdrożeniach lub Template.json dla platformy Azure hostowanej klastrów:</span><span class="sxs-lookup"><span data-stu-id="dd2e2-163">via ClusterConfig.json for Standalone deployments or Template.json for Azure hosted clusters:</span></span>

```json
"fabricSettings": [
  {
    "name": "DefragmentationMetrics",
    "parameters": [
      {
          "name": "Metric1",
          "value": "true"
      },
      {
          "name": "Metric2",
          "value": "false"
      }
    ]
  }
]
```


## <a name="next-steps"></a><span data-ttu-id="dd2e2-164">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="dd2e2-164">Next steps</span></span>
- <span data-ttu-id="dd2e2-165">Menedżer zasobów klastra ma opcje man opisujące klastra.</span><span class="sxs-lookup"><span data-stu-id="dd2e2-165">The Cluster Resource Manager has man options for describing the cluster.</span></span> <span data-ttu-id="dd2e2-166">Aby dowiedzieć się więcej na ich temat, zapoznaj się w tym artykule na [opisujące klastra sieci szkieletowej usług](service-fabric-cluster-resource-manager-cluster-description.md)</span><span class="sxs-lookup"><span data-stu-id="dd2e2-166">To find out more about them, check out this article on [describing a Service Fabric cluster](service-fabric-cluster-resource-manager-cluster-description.md)</span></span>
- <span data-ttu-id="dd2e2-167">Metryki są zarządzaniu Menedżer zasobów klastra sieci szkieletowej usług konsumenckich i pojemności w klastrze.</span><span class="sxs-lookup"><span data-stu-id="dd2e2-167">Metrics are how the Service Fabric Cluster Resource Manger manages consumption and capacity in the cluster.</span></span> <span data-ttu-id="dd2e2-168">Aby dowiedzieć się więcej na temat metryki i sposobach ich konfigurowania, zapoznaj się [w tym artykule](service-fabric-cluster-resource-manager-metrics.md)</span><span class="sxs-lookup"><span data-stu-id="dd2e2-168">To learn more about metrics and how to configure them, check out [this article](service-fabric-cluster-resource-manager-metrics.md)</span></span>

[Image1]:./media/service-fabric-cluster-resource-manager-defragmentation-metrics/balancing-defrag-compared.png
