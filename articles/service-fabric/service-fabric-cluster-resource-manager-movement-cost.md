---
title: "Koszt przeniesienia usługi Menedżer zasobów klastra sieci szkieletowej: | Dokumentacja firmy Microsoft"
description: "Omówienie koszt przeniesienia dla usług sieci szkieletowej usług"
services: service-fabric
documentationcenter: .net
author: masnider
manager: timlt
editor: 
ms.assetid: f022f258-7bc0-4db4-aa85-8c6c8344da32
ms.service: Service-Fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/18/2017
ms.author: masnider
ms.openlocfilehash: 5de07c259d1d327d0211338c2911804445dd6b60
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/18/2017
---
# <a name="service-movement-cost"></a><span data-ttu-id="68d9b-103">Usługa koszt przeniesienia</span><span class="sxs-lookup"><span data-stu-id="68d9b-103">Service movement cost</span></span>
<span data-ttu-id="68d9b-104">Współczynnik Menedżera zasobów klastra sieci szkieletowej usług pod uwagę podczas próby określenia, jakie zmiany można wprowadzać w klastrze jest koszt tych zmian.</span><span class="sxs-lookup"><span data-stu-id="68d9b-104">A factor that the Service Fabric Cluster Resource Manager considers when trying to determine what changes to make to a cluster is the cost of those changes.</span></span> <span data-ttu-id="68d9b-105">Pojęcie "koszt" jest przedmiotem handlu wyłączone przed można zwiększyć ilość klastra.</span><span class="sxs-lookup"><span data-stu-id="68d9b-105">The notion of "cost" is traded off against how much the cluster can be improved.</span></span> <span data-ttu-id="68d9b-106">Koszt jest brana pod uwagę podczas przenoszenia usługi równoważenia, defragmentacji i inne wymagania.</span><span class="sxs-lookup"><span data-stu-id="68d9b-106">Cost is factored in when moving services for balancing, defragmentation, and other requirements.</span></span> <span data-ttu-id="68d9b-107">Celem jest w celu spełnienia wymagań w zakresie zakłócenie najmniej kosztowne.</span><span class="sxs-lookup"><span data-stu-id="68d9b-107">The goal is to meet the requirements in the least disruptive or expensive way.</span></span> 

<span data-ttu-id="68d9b-108">Przesunięcie czasu procesora CPU koszty usługi i przepustowość co najmniej sieci.</span><span class="sxs-lookup"><span data-stu-id="68d9b-108">Moving services costs CPU time and network bandwidth at a minimum.</span></span> <span data-ttu-id="68d9b-109">W przypadku usług stanowych wymaga kopiowanie stan tych usług, wykorzystywanie dodatkowej pamięci i dysku.</span><span class="sxs-lookup"><span data-stu-id="68d9b-109">For stateful services, it requires copying the state of those services, consuming additional memory and disk.</span></span> <span data-ttu-id="68d9b-110">Minimalizowania kosztów rozwiązania, które Menedżer zasobów klastra sieci szkieletowej usług Azure pojawia się z pomaga, upewnij się, że zasobów klastra nie są poświęconego niepotrzebnie.</span><span class="sxs-lookup"><span data-stu-id="68d9b-110">Minimizing the cost of solutions that the Azure Service Fabric Cluster Resource Manager comes up with helps ensure that the cluster's resources aren't spent unnecessarily.</span></span> <span data-ttu-id="68d9b-111">Jednak również nie chcesz zignorować rozwiązania, które może znacznie poprawić alokacji zasobów w klastrze.</span><span class="sxs-lookup"><span data-stu-id="68d9b-111">However, you also don’t want to ignore solutions that would significantly improve the allocation of resources in the cluster.</span></span>

<span data-ttu-id="68d9b-112">Menedżer zasobów klastra ma dwa sposoby obliczenie kosztów i ograniczeniem im dostępu przy próbie do zarządzania klastrem.</span><span class="sxs-lookup"><span data-stu-id="68d9b-112">The Cluster Resource Manager has two ways of computing costs and limiting them while it tries to manage the cluster.</span></span> <span data-ttu-id="68d9b-113">Mechanizm pierwszy jest po prostu zliczania każdy ruch, który może to spowodować.</span><span class="sxs-lookup"><span data-stu-id="68d9b-113">The first mechanism is simply counting every move that it would make.</span></span> <span data-ttu-id="68d9b-114">Jeśli dwa rozwiązania są generowane z o taka sama waga (wynik), a następnie Menedżera zasobów klastra preferuje jedną z najniższy koszt (całkowita liczba przenosi).</span><span class="sxs-lookup"><span data-stu-id="68d9b-114">If two solutions are generated with about the same balance (score), then the Cluster Resource Manager prefers the one with the lowest cost (total number of moves).</span></span>

<span data-ttu-id="68d9b-115">Ta strategia działa prawidłowo.</span><span class="sxs-lookup"><span data-stu-id="68d9b-115">This strategy works well.</span></span> <span data-ttu-id="68d9b-116">Ale tak jak w przypadku domyślnych lub obciążeń statycznych, jest mało prawdopodobne w każdym systemie złożonych, że przenoszenie wszystkich są takie same.</span><span class="sxs-lookup"><span data-stu-id="68d9b-116">But as with default or static loads, it's unlikely in any complex system that all moves are equal.</span></span> <span data-ttu-id="68d9b-117">Niektóre są mogą być bardziej kosztowne.</span><span class="sxs-lookup"><span data-stu-id="68d9b-117">Some are likely to be much more expensive.</span></span>

## <a name="setting-move-costs"></a><span data-ttu-id="68d9b-118">Ustawienie przesuwanie kosztów</span><span class="sxs-lookup"><span data-stu-id="68d9b-118">Setting Move Costs</span></span> 
<span data-ttu-id="68d9b-119">Można określić domyślny Przenieś koszt usługi po utworzeniu:</span><span class="sxs-lookup"><span data-stu-id="68d9b-119">You can specify the default move cost for a service when it is created:</span></span>

<span data-ttu-id="68d9b-120">Program PowerShell:</span><span class="sxs-lookup"><span data-stu-id="68d9b-120">PowerShell:</span></span>

```posh
New-ServiceFabricService -ApplicationName $applicationName -ServiceName $serviceName -ServiceTypeName $serviceTypeName –Stateful -MinReplicaSetSize 3 -TargetReplicaSetSize 3 -PartitionSchemeSingleton -DefaultMoveCost Medium
```

<span data-ttu-id="68d9b-121">C#:</span><span class="sxs-lookup"><span data-stu-id="68d9b-121">C#:</span></span> 

```csharp
FabricClient fabricClient = new FabricClient();
StatefulServiceDescription serviceDescription = new StatefulServiceDescription();
//set up the rest of the ServiceDescription
serviceDescription.DefaultMoveCost = MoveCost.Medium;
await fabricClient.ServiceManager.CreateServiceAsync(serviceDescription);
```

<span data-ttu-id="68d9b-122">Można również określić lub zaktualizować MoveCost dynamicznie usługi po utworzeniu usługi:</span><span class="sxs-lookup"><span data-stu-id="68d9b-122">You can also specify or update MoveCost dynamically for a service after the service has been created:</span></span> 

<span data-ttu-id="68d9b-123">Program PowerShell:</span><span class="sxs-lookup"><span data-stu-id="68d9b-123">PowerShell:</span></span> 

```posh
Update-ServiceFabricService -Stateful -ServiceName "fabric:/AppName/ServiceName" -DefaultMoveCost High
```

<span data-ttu-id="68d9b-124">C#:</span><span class="sxs-lookup"><span data-stu-id="68d9b-124">C#:</span></span>

```csharp
StatefulServiceUpdateDescription updateDescription = new StatefulServiceUpdateDescription();
updateDescription.DefaultMoveCost = MoveCost.High;
await fabricClient.ServiceManager.UpdateServiceAsync(new Uri("fabric:/AppName/ServiceName"), updateDescription);
```

## <a name="dynamically-specifying-move-cost-on-a-per-replica-basis"></a><span data-ttu-id="68d9b-125">Dynamicznie Określanie koszt przeniesienia na podstawie na repliki</span><span class="sxs-lookup"><span data-stu-id="68d9b-125">Dynamically specifying move cost on a per-replica basis</span></span>

<span data-ttu-id="68d9b-126">Poprzedni fragmenty kodu są wszystkie służący do określania MoveCost dla całej usługi jednocześnie z poza samej usługi.</span><span class="sxs-lookup"><span data-stu-id="68d9b-126">The preceding snippets are all for specifying MoveCost for a whole service at once from outside the service itself.</span></span> <span data-ttu-id="68d9b-127">Jednak przenieść koszt jest najbardziej przydatna jest, gdy koszt przeniesienia obiektu określonej usługi zmienia się w jego cykl życia.</span><span class="sxs-lookup"><span data-stu-id="68d9b-127">However, move cost is most useful is when the move cost of a specific service object changes over its lifespan.</span></span> <span data-ttu-id="68d9b-128">Ponieważ uwierzytelnienia usługi prawdopodobnie najważniejsze informacje o tym, jak kosztowne są można przenieść w danym momencie, jest interfejsem API usługi własnych poszczególne Przenieś koszt podczas wykonywania raportu.</span><span class="sxs-lookup"><span data-stu-id="68d9b-128">Since the services themselves probably have the best idea of how costly they are to move a given time, there's an API for services to report their own individual move cost during runtime.</span></span> 

<span data-ttu-id="68d9b-129">C#:</span><span class="sxs-lookup"><span data-stu-id="68d9b-129">C#:</span></span>

```csharp
this.Partition.ReportMoveCost(MoveCost.Medium);
```

## <a name="impact-of-move-cost"></a><span data-ttu-id="68d9b-130">Wpływ koszt przeniesienia</span><span class="sxs-lookup"><span data-stu-id="68d9b-130">Impact of move cost</span></span>
<span data-ttu-id="68d9b-131">MoveCost zawiera cztery poziomy: Zero, niski, średni i wysoki.</span><span class="sxs-lookup"><span data-stu-id="68d9b-131">MoveCost has four levels: Zero, Low, Medium, and High.</span></span> <span data-ttu-id="68d9b-132">MoveCosts są względem siebie, z wyjątkiem Zero.</span><span class="sxs-lookup"><span data-stu-id="68d9b-132">MoveCosts are relative to each other, except for Zero.</span></span> <span data-ttu-id="68d9b-133">Zero koszt przeniesienia oznacza, że przenoszenie jest bezpłatna i nie powinien odliczona wynik rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="68d9b-133">Zero move cost means that movement is free and should not count against the score of the solution.</span></span> <span data-ttu-id="68d9b-134">Ustawianie wysokiego jest koszt przeniesienia *nie* gwarancji, że replika pozostanie w jednym miejscu.</span><span class="sxs-lookup"><span data-stu-id="68d9b-134">Setting your move cost to High does *not* guarantee that the replica stays in one place.</span></span>

<span data-ttu-id="68d9b-135"><center>
![Koszt przeniesienia jako czynnik wyborze repliki dla przepływu][Image1]
</center></span><span class="sxs-lookup"><span data-stu-id="68d9b-135"><center>
![Move cost as a factor in selecting replicas for movement][Image1]
</center></span></span>

<span data-ttu-id="68d9b-136">MoveCost pomaga znaleźć rozwiązania, które powodują ogólną zakłóceń pracy i są najłatwiej osiągnięcia jednocześnie nadal otrzymywanych saldo równoważne.</span><span class="sxs-lookup"><span data-stu-id="68d9b-136">MoveCost helps you find the solutions that cause the least disruption overall and are easiest to achieve while still arriving at equivalent balance.</span></span> <span data-ttu-id="68d9b-137">Pojęcie usługi koszt może być względem wiele rzeczy.</span><span class="sxs-lookup"><span data-stu-id="68d9b-137">A service’s notion of cost can be relative to many things.</span></span> <span data-ttu-id="68d9b-138">Najbardziej typowe czynniki obliczając koszt przeniesienia są następujące:</span><span class="sxs-lookup"><span data-stu-id="68d9b-138">The most common factors in calculating your move cost are:</span></span>

- <span data-ttu-id="68d9b-139">Kwota stan lub danych, aby przenieść usługę.</span><span class="sxs-lookup"><span data-stu-id="68d9b-139">The amount of state or data that the service has to move.</span></span>
- <span data-ttu-id="68d9b-140">Koszt rozłączenia klientów.</span><span class="sxs-lookup"><span data-stu-id="68d9b-140">The cost of disconnection of clients.</span></span> <span data-ttu-id="68d9b-141">Przenoszenie replikę podstawową jest zazwyczaj bardziej kosztowne niż koszt przenoszenia replikę pomocniczą.</span><span class="sxs-lookup"><span data-stu-id="68d9b-141">Moving a primary replica is usually more costly than the cost of moving a secondary replica.</span></span>
- <span data-ttu-id="68d9b-142">Koszt zakłócania pracy locie.</span><span class="sxs-lookup"><span data-stu-id="68d9b-142">The cost of interrupting an in-flight operation.</span></span> <span data-ttu-id="68d9b-143">Niektóre operacje na danych magazynu poziom lub są kosztowne operacje wykonywane w odpowiedzi na wywołanie przez klienta.</span><span class="sxs-lookup"><span data-stu-id="68d9b-143">Some operations at the data store level or operations performed in response to a client call are costly.</span></span> <span data-ttu-id="68d9b-144">W pewnym momencie nie chcesz ich zatrzymania, jeśli nie masz.</span><span class="sxs-lookup"><span data-stu-id="68d9b-144">After a certain point, you don’t want to stop them if you don’t have to.</span></span> <span data-ttu-id="68d9b-145">Dlatego podczas operacji trwa, zwiększyć koszt przeniesienia tego obiektu usługi, aby zmniejszyć prawdopodobieństwo, że powoduje przeniesienie.</span><span class="sxs-lookup"><span data-stu-id="68d9b-145">So while the operation is going on, you increase the move cost of this service object to reduce the likelihood that it moves.</span></span> <span data-ttu-id="68d9b-146">Po zakończeniu operacji, ustawisz koszt do normalnego.</span><span class="sxs-lookup"><span data-stu-id="68d9b-146">When the operation is done, you set the cost back to normal.</span></span>

## <a name="enabling-move-cost-in-your-cluster"></a><span data-ttu-id="68d9b-147">Włączanie koszt przeniesienia w klastrze</span><span class="sxs-lookup"><span data-stu-id="68d9b-147">Enabling move cost in your cluster</span></span>
<span data-ttu-id="68d9b-148">Aby bardziej szczegółowego MoveCosts należy wziąć pod uwagę należy włączyć MoveCost w klastrze.</span><span class="sxs-lookup"><span data-stu-id="68d9b-148">In order for the more granular MoveCosts to be taken into account, MoveCost must be enabled in your cluster.</span></span> <span data-ttu-id="68d9b-149">Bez tego ustawienia to domyślny tryb liczenia przenosi jest używany do obliczania MoveCost i MoveCost raporty są ignorowane.</span><span class="sxs-lookup"><span data-stu-id="68d9b-149">Without this setting, the default mode of counting moves is used for calculating MoveCost, and MoveCost reports are ignored.</span></span>


<span data-ttu-id="68d9b-150">ClusterManifest.xml:</span><span class="sxs-lookup"><span data-stu-id="68d9b-150">ClusterManifest.xml:</span></span>

``` xml
        <Section Name="PlacementAndLoadBalancing">
            <Parameter Name="UseMoveCostReports" Value="true" />
        </Section>
```

<span data-ttu-id="68d9b-151">za pomocą pliku ClusterConfig.json dla autonomicznych wdrożeniach lub Template.json dla platformy Azure hostowanej klastrów:</span><span class="sxs-lookup"><span data-stu-id="68d9b-151">via ClusterConfig.json for Standalone deployments or Template.json for Azure hosted clusters:</span></span>

```json
"fabricSettings": [
  {
    "name": "PlacementAndLoadBalancing",
    "parameters": [
      {
          "name": "UseMoveCostReports",
          "value": "true"
      }
    ]
  }
]
```

## <a name="next-steps"></a><span data-ttu-id="68d9b-152">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="68d9b-152">Next steps</span></span>
- <span data-ttu-id="68d9b-153">Menedżer zasobów klastra sieci szkieletowej usług wykorzystuje metryki Zarządzanie użycia i pojemności w klastrze.</span><span class="sxs-lookup"><span data-stu-id="68d9b-153">Service Fabric Cluster Resource Manger uses metrics to manage consumption and capacity in the cluster.</span></span> <span data-ttu-id="68d9b-154">Aby dowiedzieć się więcej na temat metryki i sposobach ich konfigurowania, zapoznaj się [Zarządzanie zużycia zasobów i obciążenia w sieci szkieletowej usług o metryki](service-fabric-cluster-resource-manager-metrics.md).</span><span class="sxs-lookup"><span data-stu-id="68d9b-154">To learn more about metrics and how to configure them, check out [Managing resource consumption and load in Service Fabric with metrics](service-fabric-cluster-resource-manager-metrics.md).</span></span>
- <span data-ttu-id="68d9b-155">Aby dowiedzieć się, jak Menedżer zasobów klastra zarządza i równoważy obciążenie klastra, zapoznaj się [równoważenia klastra usługi sieć szkieletowa](service-fabric-cluster-resource-manager-balancing.md).</span><span class="sxs-lookup"><span data-stu-id="68d9b-155">To learn about how the Cluster Resource Manager manages and balances load in the cluster, check out [Balancing your Service Fabric cluster](service-fabric-cluster-resource-manager-balancing.md).</span></span>

[Image1]:./media/service-fabric-cluster-resource-manager-movement-cost/service-most-cost-example.png
