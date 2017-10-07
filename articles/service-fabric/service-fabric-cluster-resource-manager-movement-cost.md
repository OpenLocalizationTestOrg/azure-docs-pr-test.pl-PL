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
ms.openlocfilehash: 65d4ac73efffcf7b25b1e95da6f9012a9238cb75
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="service-movement-cost"></a><span data-ttu-id="5a713-103">Usługa koszt przeniesienia</span><span class="sxs-lookup"><span data-stu-id="5a713-103">Service movement cost</span></span>
<span data-ttu-id="5a713-104">Współczynnik hello zasobu klastra sieci szkieletowej programu Service Manager uwzględnia podczas próby toodetermine, jakie zmiany toomake tooa klastra jest koszt hello tych zmian.</span><span class="sxs-lookup"><span data-stu-id="5a713-104">A factor that hello Service Fabric Cluster Resource Manager considers when trying toodetermine what changes toomake tooa cluster is hello cost of those changes.</span></span> <span data-ttu-id="5a713-105">pojęcie "koszt" Hello jest przedmiotem handlu wyłączone przed można zwiększyć ilość hello klastra.</span><span class="sxs-lookup"><span data-stu-id="5a713-105">hello notion of "cost" is traded off against how much hello cluster can be improved.</span></span> <span data-ttu-id="5a713-106">Koszt jest brana pod uwagę podczas przenoszenia usługi równoważenia, defragmentacji i inne wymagania.</span><span class="sxs-lookup"><span data-stu-id="5a713-106">Cost is factored in when moving services for balancing, defragmentation, and other requirements.</span></span> <span data-ttu-id="5a713-107">Celem Hello jest toomeet hello wymagań dotyczących hello co najmniej sposób destrukcyjne lub kosztowne.</span><span class="sxs-lookup"><span data-stu-id="5a713-107">hello goal is toomeet hello requirements in hello least disruptive or expensive way.</span></span> 

<span data-ttu-id="5a713-108">Przesunięcie czasu procesora CPU koszty usługi i przepustowość co najmniej sieci.</span><span class="sxs-lookup"><span data-stu-id="5a713-108">Moving services costs CPU time and network bandwidth at a minimum.</span></span> <span data-ttu-id="5a713-109">Dla stanowych usług wymaga kopiowanie hello stan tych usług, wykorzystywanie dodatkowej pamięci i dysku.</span><span class="sxs-lookup"><span data-stu-id="5a713-109">For stateful services, it requires copying hello state of those services, consuming additional memory and disk.</span></span> <span data-ttu-id="5a713-110">Minimalizowania kosztów hello rozwiązań tego powitalne Menedżera zasobów klastra sieci szkieletowej usług Azure pojawia się z pomaga, upewnij się, że zasoby hello klastra nie są poświęconego niepotrzebnie.</span><span class="sxs-lookup"><span data-stu-id="5a713-110">Minimizing hello cost of solutions that hello Azure Service Fabric Cluster Resource Manager comes up with helps ensure that hello cluster's resources aren't spent unnecessarily.</span></span> <span data-ttu-id="5a713-111">Jednak nie należy tooignore rozwiązania, które może znacznie poprawić hello alokacji zasobów w klastrze hello.</span><span class="sxs-lookup"><span data-stu-id="5a713-111">However, you also don’t want tooignore solutions that would significantly improve hello allocation of resources in hello cluster.</span></span>

<span data-ttu-id="5a713-112">Hello Menedżera zasobów klastra ma dwa sposoby obliczenie kosztów i ograniczeniem im dostępu przy próbie toomanage hello klastra.</span><span class="sxs-lookup"><span data-stu-id="5a713-112">hello Cluster Resource Manager has two ways of computing costs and limiting them while it tries toomanage hello cluster.</span></span> <span data-ttu-id="5a713-113">mechanizm pierwszy Hello jest po prostu zliczania każdy ruch, który może to spowodować.</span><span class="sxs-lookup"><span data-stu-id="5a713-113">hello first mechanism is simply counting every move that it would make.</span></span> <span data-ttu-id="5a713-114">Jeśli dwa rozwiązania są generowane z o hello hello Menedżera zasobów klastra preferuje hello jedną z hello najniższy koszt (całkowita liczba przenosi), a następnie sam równoważenie (wynik).</span><span class="sxs-lookup"><span data-stu-id="5a713-114">If two solutions are generated with about hello same balance (score), then hello Cluster Resource Manager prefers hello one with hello lowest cost (total number of moves).</span></span>

<span data-ttu-id="5a713-115">Ta strategia działa prawidłowo.</span><span class="sxs-lookup"><span data-stu-id="5a713-115">This strategy works well.</span></span> <span data-ttu-id="5a713-116">Ale tak jak w przypadku domyślnych lub obciążeń statycznych, jest mało prawdopodobne w każdym systemie złożonych, że przenoszenie wszystkich są takie same.</span><span class="sxs-lookup"><span data-stu-id="5a713-116">But as with default or static loads, it's unlikely in any complex system that all moves are equal.</span></span> <span data-ttu-id="5a713-117">Niektóre są prawdopodobnie toobe bardziej kosztowne.</span><span class="sxs-lookup"><span data-stu-id="5a713-117">Some are likely toobe much more expensive.</span></span>

## <a name="setting-move-costs"></a><span data-ttu-id="5a713-118">Ustawienie przesuwanie kosztów</span><span class="sxs-lookup"><span data-stu-id="5a713-118">Setting Move Costs</span></span> 
<span data-ttu-id="5a713-119">Możesz określić hello domyślny koszt przeniesienia usługi po utworzeniu:</span><span class="sxs-lookup"><span data-stu-id="5a713-119">You can specify hello default move cost for a service when it is created:</span></span>

<span data-ttu-id="5a713-120">Program PowerShell:</span><span class="sxs-lookup"><span data-stu-id="5a713-120">PowerShell:</span></span>

```posh
New-ServiceFabricService -ApplicationName $applicationName -ServiceName $serviceName -ServiceTypeName $serviceTypeName –Stateful -MinReplicaSetSize 3 -TargetReplicaSetSize 3 -PartitionSchemeSingleton -DefaultMoveCost Medium
```

<span data-ttu-id="5a713-121">C#:</span><span class="sxs-lookup"><span data-stu-id="5a713-121">C#:</span></span> 

```csharp
FabricClient fabricClient = new FabricClient();
StatefulServiceDescription serviceDescription = new StatefulServiceDescription();
//set up hello rest of hello ServiceDescription
serviceDescription.DefaultMoveCost = MoveCost.Medium;
await fabricClient.ServiceManager.CreateServiceAsync(serviceDescription);
```

<span data-ttu-id="5a713-122">Można również określić lub zaktualizować MoveCost dynamicznie usługi po utworzeniu usługi hello:</span><span class="sxs-lookup"><span data-stu-id="5a713-122">You can also specify or update MoveCost dynamically for a service after hello service has been created:</span></span> 

<span data-ttu-id="5a713-123">Program PowerShell:</span><span class="sxs-lookup"><span data-stu-id="5a713-123">PowerShell:</span></span> 

```posh
Update-ServiceFabricService -Stateful -ServiceName "fabric:/AppName/ServiceName" -DefaultMoveCost High
```

<span data-ttu-id="5a713-124">C#:</span><span class="sxs-lookup"><span data-stu-id="5a713-124">C#:</span></span>

```csharp
StatefulServiceUpdateDescription updateDescription = new StatefulServiceUpdateDescription();
updateDescription.DefaultMoveCost = MoveCost.High;
await fabricClient.ServiceManager.UpdateServiceAsync(new Uri("fabric:/AppName/ServiceName"), updateDescription);
```

## <a name="dynamically-specifying-move-cost-on-a-per-replica-basis"></a><span data-ttu-id="5a713-125">Dynamicznie Określanie koszt przeniesienia na podstawie na repliki</span><span class="sxs-lookup"><span data-stu-id="5a713-125">Dynamically specifying move cost on a per-replica basis</span></span>

<span data-ttu-id="5a713-126">Witaj poprzedniego fragmenty kodu są wszystkie służący do określania MoveCost dla całej usługi jednocześnie z samej usługi poza hello.</span><span class="sxs-lookup"><span data-stu-id="5a713-126">hello preceding snippets are all for specifying MoveCost for a whole service at once from outside hello service itself.</span></span> <span data-ttu-id="5a713-127">Jednak przenieść koszt jest najbardziej przydatna jest, gdy koszt przeniesienia hello obiektu określonej usługi zmienia się w jego cykl życia.</span><span class="sxs-lookup"><span data-stu-id="5a713-127">However, move cost is most useful is when hello move cost of a specific service object changes over its lifespan.</span></span> <span data-ttu-id="5a713-128">Ponieważ hello usług prawdopodobnie ma hello najważniejsze informacje o tym, jak kosztowne są toomove danym czasie, jest interfejs API dla usług tooreport własnych indywidualnych przenoszenia kosztów w czasie wykonywania.</span><span class="sxs-lookup"><span data-stu-id="5a713-128">Since hello services themselves probably have hello best idea of how costly they are toomove a given time, there's an API for services tooreport their own individual move cost during runtime.</span></span> 

<span data-ttu-id="5a713-129">C#:</span><span class="sxs-lookup"><span data-stu-id="5a713-129">C#:</span></span>

```csharp
this.Partition.ReportMoveCost(MoveCost.Medium);
```

## <a name="impact-of-move-cost"></a><span data-ttu-id="5a713-130">Wpływ koszt przeniesienia</span><span class="sxs-lookup"><span data-stu-id="5a713-130">Impact of move cost</span></span>
<span data-ttu-id="5a713-131">MoveCost zawiera cztery poziomy: Zero, niski, średni i wysoki.</span><span class="sxs-lookup"><span data-stu-id="5a713-131">MoveCost has four levels: Zero, Low, Medium, and High.</span></span> <span data-ttu-id="5a713-132">MoveCosts są względną tooeach innych, z wyjątkiem Zero.</span><span class="sxs-lookup"><span data-stu-id="5a713-132">MoveCosts are relative tooeach other, except for Zero.</span></span> <span data-ttu-id="5a713-133">Zero koszt przeniesienia oznacza, że przenoszenie jest bezpłatna i nie powinien odliczona wynik hello hello rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="5a713-133">Zero move cost means that movement is free and should not count against hello score of hello solution.</span></span> <span data-ttu-id="5a713-134">Ustawienie jest przejście koszt tooHigh *nie* gwarantuje, że repliki hello pozostaje w jednym miejscu.</span><span class="sxs-lookup"><span data-stu-id="5a713-134">Setting your move cost tooHigh does *not* guarantee that hello replica stays in one place.</span></span>

<span data-ttu-id="5a713-135"><center>
![Koszt przeniesienia jako czynnik wyborze repliki dla przepływu][Image1]
</center></span><span class="sxs-lookup"><span data-stu-id="5a713-135"><center>
![Move cost as a factor in selecting replicas for movement][Image1]
</center></span></span>

<span data-ttu-id="5a713-136">MoveCost pomaga hello rozwiązania czy przyczyna ogólne hello zakłóceń pracy i są najprostszym tooachieve podczas nadal otrzymywanych saldo równoważne.</span><span class="sxs-lookup"><span data-stu-id="5a713-136">MoveCost helps you find hello solutions that cause hello least disruption overall and are easiest tooachieve while still arriving at equivalent balance.</span></span> <span data-ttu-id="5a713-137">Pojęcie usługi koszt może być względna toomany rzeczy.</span><span class="sxs-lookup"><span data-stu-id="5a713-137">A service’s notion of cost can be relative toomany things.</span></span> <span data-ttu-id="5a713-138">Witaj najbardziej typowych czynników przy obliczaniu koszt przeniesienia są:</span><span class="sxs-lookup"><span data-stu-id="5a713-138">hello most common factors in calculating your move cost are:</span></span>

- <span data-ttu-id="5a713-139">Kwota Hello danych, że usługa hello ma toomove lub stanu.</span><span class="sxs-lookup"><span data-stu-id="5a713-139">hello amount of state or data that hello service has toomove.</span></span>
- <span data-ttu-id="5a713-140">Koszt Hello rozłączenia klientów.</span><span class="sxs-lookup"><span data-stu-id="5a713-140">hello cost of disconnection of clients.</span></span> <span data-ttu-id="5a713-141">Przenoszenie replikę podstawową jest zazwyczaj bardziej kosztowne niż koszt hello przenoszenia replikę pomocniczą.</span><span class="sxs-lookup"><span data-stu-id="5a713-141">Moving a primary replica is usually more costly than hello cost of moving a secondary replica.</span></span>
- <span data-ttu-id="5a713-142">Koszt Hello zakłócania pracy locie.</span><span class="sxs-lookup"><span data-stu-id="5a713-142">hello cost of interrupting an in-flight operation.</span></span> <span data-ttu-id="5a713-143">Niektóre operacje na danych hello magazynu poziom lub operacje wykonywane w odpowiedzi tooa klienta wywołania są kosztowne.</span><span class="sxs-lookup"><span data-stu-id="5a713-143">Some operations at hello data store level or operations performed in response tooa client call are costly.</span></span> <span data-ttu-id="5a713-144">W pewnym momencie nie chcesz toostop je, jeśli nie masz.</span><span class="sxs-lookup"><span data-stu-id="5a713-144">After a certain point, you don’t want toostop them if you don’t have to.</span></span> <span data-ttu-id="5a713-145">Gdy trwa operacja hello, więc zwiększyć hello koszt przeniesienia tej usługi obiektu tooreduce hello prawdopodobieństwo, że powoduje przeniesienie.</span><span class="sxs-lookup"><span data-stu-id="5a713-145">So while hello operation is going on, you increase hello move cost of this service object tooreduce hello likelihood that it moves.</span></span> <span data-ttu-id="5a713-146">Po zakończeniu operacji hello, należy ustawić toonormal wstecz hello kosztów.</span><span class="sxs-lookup"><span data-stu-id="5a713-146">When hello operation is done, you set hello cost back toonormal.</span></span>

## <a name="enabling-move-cost-in-your-cluster"></a><span data-ttu-id="5a713-147">Włączanie koszt przeniesienia w klastrze</span><span class="sxs-lookup"><span data-stu-id="5a713-147">Enabling move cost in your cluster</span></span>
<span data-ttu-id="5a713-148">Aby hello bardziej szczegółowego toobe MoveCosts wziąć pod uwagę, MoveCost musi być włączona w klastrze.</span><span class="sxs-lookup"><span data-stu-id="5a713-148">In order for hello more granular MoveCosts toobe taken into account, MoveCost must be enabled in your cluster.</span></span> <span data-ttu-id="5a713-149">Bez tego ustawienia hello domyślny tryb liczenia przenosi jest używany do obliczania MoveCost i MoveCost raporty są ignorowane.</span><span class="sxs-lookup"><span data-stu-id="5a713-149">Without this setting, hello default mode of counting moves is used for calculating MoveCost, and MoveCost reports are ignored.</span></span>


<span data-ttu-id="5a713-150">ClusterManifest.xml:</span><span class="sxs-lookup"><span data-stu-id="5a713-150">ClusterManifest.xml:</span></span>

``` xml
        <Section Name="PlacementAndLoadBalancing">
            <Parameter Name="UseMoveCostReports" Value="true" />
        </Section>
```

<span data-ttu-id="5a713-151">za pomocą pliku ClusterConfig.json dla autonomicznych wdrożeniach lub Template.json dla platformy Azure hostowanej klastrów:</span><span class="sxs-lookup"><span data-stu-id="5a713-151">via ClusterConfig.json for Standalone deployments or Template.json for Azure hosted clusters:</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="5a713-152">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="5a713-152">Next steps</span></span>
- <span data-ttu-id="5a713-153">Menedżer zasobów klastra sieci szkieletowej usług używa metryki toomanage użycia i pojemności hello klastra.</span><span class="sxs-lookup"><span data-stu-id="5a713-153">Service Fabric Cluster Resource Manger uses metrics toomanage consumption and capacity in hello cluster.</span></span> <span data-ttu-id="5a713-154">więcej informacji na temat metryki toolearn i jak tooconfigure, zapoznaj się z [Zarządzanie zużycia zasobów i obciążenia w sieci szkieletowej usług o metryki](service-fabric-cluster-resource-manager-metrics.md).</span><span class="sxs-lookup"><span data-stu-id="5a713-154">toolearn more about metrics and how tooconfigure them, check out [Managing resource consumption and load in Service Fabric with metrics](service-fabric-cluster-resource-manager-metrics.md).</span></span>
- <span data-ttu-id="5a713-155">toolearn dotyczące sposobu hello Menedżera zasobów klastra zarządza i równoważy obciążenie hello klastra, zapoznaj się z [równoważenia klastra usługi sieć szkieletowa](service-fabric-cluster-resource-manager-balancing.md).</span><span class="sxs-lookup"><span data-stu-id="5a713-155">toolearn about how hello Cluster Resource Manager manages and balances load in hello cluster, check out [Balancing your Service Fabric cluster](service-fabric-cluster-resource-manager-balancing.md).</span></span>

[Image1]:./media/service-fabric-cluster-resource-manager-movement-cost/service-most-cost-example.png
