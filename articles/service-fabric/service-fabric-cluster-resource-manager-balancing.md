---
title: "Równoważenie klastra usługi sieć szkieletowa usług Azure | Dokumentacja firmy Microsoft"
description: "Wprowadzenie do równoważenia klastra z usługi sieć szkieletowa klastra Menedżera zasobów."
services: service-fabric
documentationcenter: .net
author: masnider
manager: timlt
editor: 
ms.assetid: 030b1465-6616-4c0b-8bc7-24ed47d054c0
ms.service: Service-Fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/18/2017
ms.author: masnider
ms.openlocfilehash: 34eacb29f324025c1d2803c9690600227d3ec457
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/18/2017
---
# <a name="balancing-your-service-fabric-cluster"></a><span data-ttu-id="d9cf8-103">Równoważenie klastra sieci szkieletowej usług</span><span class="sxs-lookup"><span data-stu-id="d9cf8-103">Balancing your service fabric cluster</span></span>
<span data-ttu-id="d9cf8-104">Menedżer zasobów klastra sieci szkieletowej usług obsługuje zmiany dynamicznego obciążenia reagowanie na dodawania i usuwania węzłów lub usług.</span><span class="sxs-lookup"><span data-stu-id="d9cf8-104">The Service Fabric Cluster Resource Manager supports dynamic load changes, reacting to additions or removals of nodes or services.</span></span> <span data-ttu-id="d9cf8-105">Automatycznie koryguje naruszenia ograniczeń i aktywne rebalances klastra.</span><span class="sxs-lookup"><span data-stu-id="d9cf8-105">It also automatically corrects constraint violations, and proactively rebalances the cluster.</span></span> <span data-ttu-id="d9cf8-106">Jak często są te akcje podjęte — a wywołujących je?</span><span class="sxs-lookup"><span data-stu-id="d9cf8-106">But how often are these actions taken, and what triggers them?</span></span>

<span data-ttu-id="d9cf8-107">Istnieją trzy różne kategorie pracy, który wykonuje Menedżera zasobów klastra.</span><span class="sxs-lookup"><span data-stu-id="d9cf8-107">There are three different categories of work that the Cluster Resource Manager performs.</span></span> <span data-ttu-id="d9cf8-108">Są to:</span><span class="sxs-lookup"><span data-stu-id="d9cf8-108">They are:</span></span>

1. <span data-ttu-id="d9cf8-109">Rozmieszczenia — ten etap dotyczy umieszczenie replik stanowe ani bezstanowych wystąpień, które nie są spełnione.</span><span class="sxs-lookup"><span data-stu-id="d9cf8-109">Placement – this stage deals with placing any stateful replicas or stateless instances that are missing.</span></span> <span data-ttu-id="d9cf8-110">Umieszczanie zawiera nowe usługi i obsługa repliki stanowego lub bezstanowego wystąpień, których nie powiodła.</span><span class="sxs-lookup"><span data-stu-id="d9cf8-110">Placement includes both new services and handling stateful replicas or stateless instances that have failed.</span></span> <span data-ttu-id="d9cf8-111">Usuwanie i usunięcie repliki lub wystąpienia są obsługiwane w tym miejscu.</span><span class="sxs-lookup"><span data-stu-id="d9cf8-111">Deleting and dropping replicas or instances are handled here.</span></span>
2. <span data-ttu-id="d9cf8-112">Ograniczenie sprawdza — ten etap sprawdza i koryguje naruszenia ograniczeń umieszczania różnych (reguły) w systemie.</span><span class="sxs-lookup"><span data-stu-id="d9cf8-112">Constraint Checks – this stage checks for and corrects violations of the different placement constraints (rules) within the system.</span></span> <span data-ttu-id="d9cf8-113">Przykłady reguł jest rzeczy, takich jak zapewnienie, że węzły nie są przeciążone i że spełnione są ograniczenia umieszczania usług.</span><span class="sxs-lookup"><span data-stu-id="d9cf8-113">Examples of rules are things like ensuring that nodes are not over capacity and that a service’s placement constraints are met.</span></span>
3. <span data-ttu-id="d9cf8-114">Równoważenie — ten etap sprawdza, czy ponowne równoważenie jest konieczne na podstawie skonfigurowanego poziomu żądaną salda dla różnych metryki.</span><span class="sxs-lookup"><span data-stu-id="d9cf8-114">Balancing – this stage checks to see if rebalancing is necessary based on the configured desired level of balance for different metrics.</span></span> <span data-ttu-id="d9cf8-115">Jeśli tak próbuje znaleźć rozmieszczenia w klastrze, który jest bardziej zrównoważone.</span><span class="sxs-lookup"><span data-stu-id="d9cf8-115">If so it attempts to find an arrangement in the cluster that is more balanced.</span></span>

## <a name="configuring-cluster-resource-manager-timers"></a><span data-ttu-id="d9cf8-116">Konfigurowanie czasomierze Menedżera zasobów klastra</span><span class="sxs-lookup"><span data-stu-id="d9cf8-116">Configuring Cluster Resource Manager Timers</span></span>
<span data-ttu-id="d9cf8-117">Pierwszy zestaw kontrolek wokół równoważenia to zbiór czasomierze.</span><span class="sxs-lookup"><span data-stu-id="d9cf8-117">The first set of controls around balancing are a set of timers.</span></span> <span data-ttu-id="d9cf8-118">Czasomierze te określają częstotliwość sprawdza klastra Menedżera zasobów klastra i wykonuje akcje naprawcze.</span><span class="sxs-lookup"><span data-stu-id="d9cf8-118">These timers govern how often the Cluster Resource Manager examines the cluster and takes corrective actions.</span></span>

<span data-ttu-id="d9cf8-119">Każdego z tych różnych typów poprawek, które ułatwia Menedżera zasobów klastra jest kontrolowana przez różnych kontroluje częstotliwość czasomierza.</span><span class="sxs-lookup"><span data-stu-id="d9cf8-119">Each of these different types of corrections the Cluster Resource Manager can make is controlled by a different timer that governs its frequency.</span></span> <span data-ttu-id="d9cf8-120">Po każdym czasomierza, jest zaplanowane zadanie.</span><span class="sxs-lookup"><span data-stu-id="d9cf8-120">When each timer fires, the task is scheduled.</span></span> <span data-ttu-id="d9cf8-121">Domyślnie Menedżer zasobów:</span><span class="sxs-lookup"><span data-stu-id="d9cf8-121">By default the Resource Manager:</span></span>

* <span data-ttu-id="d9cf8-122">skanuje stanu i stosuje aktualizacje (na przykład rejestrowania, który jest węzłem w dół) co 1/10 sekundy</span><span class="sxs-lookup"><span data-stu-id="d9cf8-122">scans its state and applies updates (like recording that a node is down) every 1/10th of a second</span></span>
* <span data-ttu-id="d9cf8-123">Ustawia flagę wyboru umieszczenia</span><span class="sxs-lookup"><span data-stu-id="d9cf8-123">sets the placement check flag</span></span> 
* <span data-ttu-id="d9cf8-124">Ustawia flagę wyboru ograniczenia co sekundę</span><span class="sxs-lookup"><span data-stu-id="d9cf8-124">sets the constraint check flag every second</span></span>
* <span data-ttu-id="d9cf8-125">Ustawia flagę równoważenia co pięć sekund.</span><span class="sxs-lookup"><span data-stu-id="d9cf8-125">sets the balancing flag every five seconds.</span></span>

<span data-ttu-id="d9cf8-126">Przykłady dotyczące tych czasomierze konfiguracji jest poniżej:</span><span class="sxs-lookup"><span data-stu-id="d9cf8-126">Examples of the configuration governing these timers are below:</span></span>

<span data-ttu-id="d9cf8-127">ClusterManifest.xml:</span><span class="sxs-lookup"><span data-stu-id="d9cf8-127">ClusterManifest.xml:</span></span>

``` xml
        <Section Name="PlacementAndLoadBalancing">
            <Parameter Name="PLBRefreshGap" Value="0.1" />
            <Parameter Name="MinPlacementInterval" Value="1.0" />
            <Parameter Name="MinConstraintCheckInterval" Value="1.0" />
            <Parameter Name="MinLoadBalancingInterval" Value="5.0" />
        </Section>
```

<span data-ttu-id="d9cf8-128">za pomocą pliku ClusterConfig.json dla autonomicznych wdrożeniach lub Template.json dla platformy Azure hostowanej klastrów:</span><span class="sxs-lookup"><span data-stu-id="d9cf8-128">via ClusterConfig.json for Standalone deployments or Template.json for Azure hosted clusters:</span></span>

```json
"fabricSettings": [
  {
    "name": "PlacementAndLoadBalancing",
    "parameters": [
      {
          "name": "PLBRefreshGap",
          "value": "0.10"
      },
      {
          "name": "MinPlacementInterval",
          "value": "1.0"
      },
      {
          "name": "MinConstraintCheckInterval",
          "value": "1.0"
      },
      {
          "name": "MinLoadBalancingInterval",
          "value": "5.0"
      }
    ]
  }
]
```

<span data-ttu-id="d9cf8-129">Dzisiaj Menedżera zasobów klastra tylko wykonuje jedno z następujących działań w czasie, po kolei.</span><span class="sxs-lookup"><span data-stu-id="d9cf8-129">Today the Cluster Resource Manager only performs one of these actions at a time, sequentially.</span></span> <span data-ttu-id="d9cf8-130">Jest to, dlaczego się te czasomierze jako "minimalna interwałów" i akcji, które uzyskać wykonania, kiedy czasomierze go jako "ustawienie flagi".</span><span class="sxs-lookup"><span data-stu-id="d9cf8-130">This is why we refer to these timers as “minimum intervals” and the actions that get taken when the timers go off as "setting flags".</span></span> <span data-ttu-id="d9cf8-131">Na przykład Menedżera zasobów klastra odpowiada on za oczekujące żądania utworzenia usługi przed równoważenia klastra.</span><span class="sxs-lookup"><span data-stu-id="d9cf8-131">For example, the Cluster Resource Manager takes care of pending requests to create services before balancing the cluster.</span></span> <span data-ttu-id="d9cf8-132">Jak widać przez określone przedziały czasu domyślnego menedżera zasobów klastra skanowania pod kątem coś, co należy zrobić często.</span><span class="sxs-lookup"><span data-stu-id="d9cf8-132">As you can see by the default time intervals specified, the Cluster Resource Manager scans for anything it needs to do frequently.</span></span> <span data-ttu-id="d9cf8-133">Zwykle oznacza to, że zestaw zmian wprowadzonych na każdym etapie ma mała.</span><span class="sxs-lookup"><span data-stu-id="d9cf8-133">Normally this means that the set of changes made during each step is small.</span></span> <span data-ttu-id="d9cf8-134">Zmiany wprowadzone w małych często umożliwia Menedżera zasobów klastra, aby odpowiadać, gdy wystąpi rzeczy w klastrze.</span><span class="sxs-lookup"><span data-stu-id="d9cf8-134">Making small changes frequently allows the Cluster Resource Manager to be responsive when things happen in the cluster.</span></span> <span data-ttu-id="d9cf8-135">Czasomierze domyślne Podaj niektórych przetwarzanie wsadowe, ponieważ wiele takich samych typach zdarzeń często występowały jednocześnie.</span><span class="sxs-lookup"><span data-stu-id="d9cf8-135">The default timers provide some batching since many of the same types of events tend to occur simultaneously.</span></span> 

<span data-ttu-id="d9cf8-136">Na przykład po awarii węzłów robią to całego domen błędów w czasie.</span><span class="sxs-lookup"><span data-stu-id="d9cf8-136">For example, when nodes fail they can do so entire fault domains at a time.</span></span> <span data-ttu-id="d9cf8-137">Wszystkie te błędy są przechwytywane podczas następnego stanu aktualizacji po *PLBRefreshGap*.</span><span class="sxs-lookup"><span data-stu-id="d9cf8-137">All these failures are captured during the next state update after the *PLBRefreshGap*.</span></span> <span data-ttu-id="d9cf8-138">Poprawki są określane podczas umieszczania następujące ograniczenia check, i Równoważenie działa.</span><span class="sxs-lookup"><span data-stu-id="d9cf8-138">The corrections are determined during the following placement, constraint check, and balancing runs.</span></span> <span data-ttu-id="d9cf8-139">Domyślnie Menedżer zasobów klastra nie jest skanowanie za pomocą godziny zmian w klastrze i próby adresów wszystkie zmiany na raz.</span><span class="sxs-lookup"><span data-stu-id="d9cf8-139">By default the Cluster Resource Manager is not scanning through hours of changes in the cluster and trying to address all changes at once.</span></span> <span data-ttu-id="d9cf8-140">W ten sposób może spowodować Seria zmian.</span><span class="sxs-lookup"><span data-stu-id="d9cf8-140">Doing so would lead to bursts of churn.</span></span>

<span data-ttu-id="d9cf8-141">Menedżer zasobów klastra musi również dodatkowe informacje, aby określić, czy imbalanced klastra.</span><span class="sxs-lookup"><span data-stu-id="d9cf8-141">The Cluster Resource Manager also needs some additional information to determine if the cluster imbalanced.</span></span> <span data-ttu-id="d9cf8-142">W tym mamy dwóch elementów konfiguracji: *BalancingThresholds* i *ActivityThresholds*.</span><span class="sxs-lookup"><span data-stu-id="d9cf8-142">For that we have two other pieces of configuration: *BalancingThresholds* and *ActivityThresholds*.</span></span>

## <a name="balancing-thresholds"></a><span data-ttu-id="d9cf8-143">Równoważenie progi</span><span class="sxs-lookup"><span data-stu-id="d9cf8-143">Balancing thresholds</span></span>
<span data-ttu-id="d9cf8-144">Próg równoważenia jest służącą do wyzwalania ponowne równoważenie formantu.</span><span class="sxs-lookup"><span data-stu-id="d9cf8-144">A Balancing Threshold is the main control for triggering rebalancing.</span></span> <span data-ttu-id="d9cf8-145">Próg równoważenia metryka jest _współczynnik_.</span><span class="sxs-lookup"><span data-stu-id="d9cf8-145">The Balancing Threshold for a metric is a _ratio_.</span></span> <span data-ttu-id="d9cf8-146">Jeśli obciążenie dla metryki w węźle najbardziej załadować podzielona przez ilość obciążenia w węźle najmniej załadować przekracza tego Metryka *BalancingThreshold*, klaster jest imbalanced.</span><span class="sxs-lookup"><span data-stu-id="d9cf8-146">If the load for a metric on the most loaded node divided by the amount of load on the least loaded node exceeds that metric's *BalancingThreshold*, then the cluster is imbalanced.</span></span> <span data-ttu-id="d9cf8-147">W związku z tym równoważenia jest wyzwalane po następnym sprawdza Menedżera zasobów klastra.</span><span class="sxs-lookup"><span data-stu-id="d9cf8-147">As a result balancing is triggered the next time the Cluster Resource Manager checks.</span></span> <span data-ttu-id="d9cf8-148">*MinLoadBalancingInterval* czasomierza Określa, jak często Menedżera zasobów klastra należy sprawdzić, czy konieczne jest ponowne równoważenie.</span><span class="sxs-lookup"><span data-stu-id="d9cf8-148">The *MinLoadBalancingInterval* timer defines how often the Cluster Resource Manager should check if rebalancing is necessary.</span></span> <span data-ttu-id="d9cf8-149">Sprawdzanie nie oznacza, że awarii.</span><span class="sxs-lookup"><span data-stu-id="d9cf8-149">Checking doesn't mean that anything happens.</span></span> 

<span data-ttu-id="d9cf8-150">Progi równoważenia są zdefiniowane w zasadzie na Metryka jako część definicji klastra.</span><span class="sxs-lookup"><span data-stu-id="d9cf8-150">Balancing Thresholds are defined on a per-metric basis as a part of the cluster definition.</span></span> <span data-ttu-id="d9cf8-151">Aby uzyskać więcej informacji dotyczących metryki, zapoznaj się [w tym artykule](service-fabric-cluster-resource-manager-metrics.md).</span><span class="sxs-lookup"><span data-stu-id="d9cf8-151">For more information on metrics, check out [this article](service-fabric-cluster-resource-manager-metrics.md).</span></span>

<span data-ttu-id="d9cf8-152">ClusterManifest.xml</span><span class="sxs-lookup"><span data-stu-id="d9cf8-152">ClusterManifest.xml</span></span>

```xml
    <Section Name="MetricBalancingThresholds">
      <Parameter Name="MetricName1" Value="2"/>
      <Parameter Name="MetricName2" Value="3.5"/>
    </Section>
```

<span data-ttu-id="d9cf8-153">za pomocą pliku ClusterConfig.json dla autonomicznych wdrożeniach lub Template.json dla platformy Azure hostowanej klastrów:</span><span class="sxs-lookup"><span data-stu-id="d9cf8-153">via ClusterConfig.json for Standalone deployments or Template.json for Azure hosted clusters:</span></span>

```json
"fabricSettings": [
  {
    "name": "MetricBalancingThresholds",
    "parameters": [
      {
          "name": "MetricName1",
          "value": "2"
      },
      {
          "name": "MetricName2",
          "value": "3.5"
      }
    ]
  }
]
```

<span data-ttu-id="d9cf8-154"><center>
![Równoważenie przykład próg][Image1]
</center></span><span class="sxs-lookup"><span data-stu-id="d9cf8-154"><center>
![Balancing Threshold Example][Image1]
</center></span></span>

<span data-ttu-id="d9cf8-155">W tym przykładzie każda usługa zajmuje jedną jednostkę niektóre metryki.</span><span class="sxs-lookup"><span data-stu-id="d9cf8-155">In this example, each service is consuming one unit of some metric.</span></span> <span data-ttu-id="d9cf8-156">W przykładzie top maksymalne obciążenie w węźle osiągnie wartość 5 i minimalna wynosi dwa.</span><span class="sxs-lookup"><span data-stu-id="d9cf8-156">In the top example, the maximum load on a node is five and the minimum is two.</span></span> <span data-ttu-id="d9cf8-157">Załóżmy, że próg równoważenia ta metryka jest trzy.</span><span class="sxs-lookup"><span data-stu-id="d9cf8-157">Let’s say that the balancing threshold for this metric is three.</span></span> <span data-ttu-id="d9cf8-158">Ponieważ współczynnik w klastrze jest 5/2 = 2.5 i który jest mniejsza niż określony próg trzech równoważenia klastra jest rozmieszczana.</span><span class="sxs-lookup"><span data-stu-id="d9cf8-158">Since the ratio in the cluster is 5/2 = 2.5 and that is less than the specified balancing threshold of three, the cluster is balanced.</span></span> <span data-ttu-id="d9cf8-159">Bez równoważenia jest wyzwalane, gdy sprawdza Menedżera zasobów klastra.</span><span class="sxs-lookup"><span data-stu-id="d9cf8-159">No balancing is triggered when the Cluster Resource Manager checks.</span></span>

<span data-ttu-id="d9cf8-160">W przykładzie dolnej maksymalne obciążenie w węźle wynosi 10, gdy jest co najmniej dwóch, co w stosunku pięć.</span><span class="sxs-lookup"><span data-stu-id="d9cf8-160">In the bottom example, the maximum load on a node is 10, while the minimum is two, resulting in a ratio of five.</span></span> <span data-ttu-id="d9cf8-161">Pięć jest większy niż próg równoważenia wyznaczonych trzech dla tej metryki.</span><span class="sxs-lookup"><span data-stu-id="d9cf8-161">Five is greater than the designated balancing threshold of three for that metric.</span></span> <span data-ttu-id="d9cf8-162">W związku z tym ponowne równoważenie Uruchom będzie następnym zaplanowanym równoważenia czasomierza wyzwala.</span><span class="sxs-lookup"><span data-stu-id="d9cf8-162">As a result, a rebalancing run will be scheduled next time the balancing timer fires.</span></span> <span data-ttu-id="d9cf8-163">W sytuacji, jak to niektóre obciążenia jest zazwyczaj dystrybuowane do Węzeł3.</span><span class="sxs-lookup"><span data-stu-id="d9cf8-163">In a situation like this some load is usually distributed to Node3.</span></span> <span data-ttu-id="d9cf8-164">Menedżera zasobów klastra sieci szkieletowej usług korzysta z podejścia intensywnie, niektóre obciążenia można również przekazać Node2.</span><span class="sxs-lookup"><span data-stu-id="d9cf8-164">Because the Service Fabric Cluster Resource Manager doesn't use a greedy approach, some load could also be distributed to Node2.</span></span> 

<span data-ttu-id="d9cf8-165"><center>
![Równoważenie akcje przykład próg][Image2]
</center></span><span class="sxs-lookup"><span data-stu-id="d9cf8-165"><center>
![Balancing Threshold Example Actions][Image2]
</center></span></span>

> [!NOTE]
> <span data-ttu-id="d9cf8-166">"" Równoważenie dwa różne strategie zarządzania obciążenia w klastrze.</span><span class="sxs-lookup"><span data-stu-id="d9cf8-166">"Balancing" handles two different strategies for managing load in your cluster.</span></span> <span data-ttu-id="d9cf8-167">Strategii domyślny, który używa Menedżera zasobów klastra jest rozłożenie obciążenia między węzłami w klastrze.</span><span class="sxs-lookup"><span data-stu-id="d9cf8-167">The default strategy that the Cluster Resource Manager uses is to distribute load across the nodes in the cluster.</span></span> <span data-ttu-id="d9cf8-168">Strategia ta jest [defragmentacji](service-fabric-cluster-resource-manager-defragmentation-metrics.md).</span><span class="sxs-lookup"><span data-stu-id="d9cf8-168">The other strategy is [defragmentation](service-fabric-cluster-resource-manager-defragmentation-metrics.md).</span></span> <span data-ttu-id="d9cf8-169">Defragmentacja jest wykonywane podczas tego samego równoważenia Uruchom.</span><span class="sxs-lookup"><span data-stu-id="d9cf8-169">Defragmentation is performed during the same balancing run.</span></span> <span data-ttu-id="d9cf8-170">Strategie równoważenia i defragmentacji może służyć do różnych metryk w tym samym klastrze.</span><span class="sxs-lookup"><span data-stu-id="d9cf8-170">The balancing and defragmentation strategies can be used for different metrics within the same cluster.</span></span> <span data-ttu-id="d9cf8-171">Usługa może mieć równoważenia i defragmentacji metryki.</span><span class="sxs-lookup"><span data-stu-id="d9cf8-171">A service can have both balancing and defragmentation metrics.</span></span> <span data-ttu-id="d9cf8-172">Dla metryki defragmentacji stosunek obciążenia w klastrze wyzwala ponowne równoważenie, gdy jest _poniżej_ równoważenia wartość progową.</span><span class="sxs-lookup"><span data-stu-id="d9cf8-172">For defragmentation metrics, the ratio of the loads in the cluster triggers rebalancing when it is _below_ the balancing threshold.</span></span> 
>

<span data-ttu-id="d9cf8-173">Pobieranie poniżej progu równoważenia nie jest celem jawnego.</span><span class="sxs-lookup"><span data-stu-id="d9cf8-173">Getting below the balancing threshold is not an explicit goal.</span></span> <span data-ttu-id="d9cf8-174">Progi równoważenia są po prostu *wyzwalacza*.</span><span class="sxs-lookup"><span data-stu-id="d9cf8-174">Balancing Thresholds are just a *trigger*.</span></span> <span data-ttu-id="d9cf8-175">Podczas równoważenia działa, Menedżera zasobów klastra określa jakie ulepszenia go, jeśli istnieją.</span><span class="sxs-lookup"><span data-stu-id="d9cf8-175">When balancing runs, the Cluster Resource Manager determines what improvements it can make, if any.</span></span> <span data-ttu-id="d9cf8-176">Tak, ponieważ zostało rozpoczęte równoważenia wyszukiwania nie oznacza niczego przenosi.</span><span class="sxs-lookup"><span data-stu-id="d9cf8-176">Just because a balancing search is kicked off doesn't mean anything moves.</span></span> <span data-ttu-id="d9cf8-177">Czasami klastra jest imbalanced, ale zbyt ograniczone, aby poprawić.</span><span class="sxs-lookup"><span data-stu-id="d9cf8-177">Sometimes the cluster is imbalanced but too constrained to correct.</span></span> <span data-ttu-id="d9cf8-178">Alternatywnie ulepszenia wymagają przesunięcia, które są zbyt [kosztowne](service-fabric-cluster-resource-manager-movement-cost.md)).</span><span class="sxs-lookup"><span data-stu-id="d9cf8-178">Alternatively, the improvements require movements that are too [costly](service-fabric-cluster-resource-manager-movement-cost.md)).</span></span>

## <a name="activity-thresholds"></a><span data-ttu-id="d9cf8-179">Progi działania</span><span class="sxs-lookup"><span data-stu-id="d9cf8-179">Activity thresholds</span></span>
<span data-ttu-id="d9cf8-180">Czasami, mimo że węzły są stosunkowo imbalanced *całkowita* obciążenie w klastrze jest niska.</span><span class="sxs-lookup"><span data-stu-id="d9cf8-180">Sometimes, although nodes are relatively imbalanced, the *total* amount of load in the cluster is low.</span></span> <span data-ttu-id="d9cf8-181">Brak obciążenia może być przejściowy dip lub załadować, ponieważ klaster jest nowy i po prostu pobierania.</span><span class="sxs-lookup"><span data-stu-id="d9cf8-181">The lack of load could be a transient dip, or because the cluster is new and just getting bootstrapped.</span></span> <span data-ttu-id="d9cf8-182">W obu przypadkach nie możesz poświęcić czas równoważenia klastra, ponieważ niewiele możliwy.</span><span class="sxs-lookup"><span data-stu-id="d9cf8-182">In either case, you may not want to spend time balancing the cluster because there’s little to be gained.</span></span> <span data-ttu-id="d9cf8-183">Jeśli klaster został poddany równoważenia, czy spędzają sieci i zasoby można przenosić elementy bez wprowadzania żadnych dużych obliczeniowe *bezwzględną* różnicy.</span><span class="sxs-lookup"><span data-stu-id="d9cf8-183">If the cluster underwent balancing, you’d spend network and compute resources to move things around without making any large *absolute* difference.</span></span> <span data-ttu-id="d9cf8-184">Aby uniknąć niepotrzebnych przenosi, istnieje inny formant znany jako progi działania.</span><span class="sxs-lookup"><span data-stu-id="d9cf8-184">To avoid unnecessary moves, there’s another control known as Activity Thresholds.</span></span> <span data-ttu-id="d9cf8-185">Progi działania można określić niektóre bezwzględnym dolnej granicy dla działania.</span><span class="sxs-lookup"><span data-stu-id="d9cf8-185">Activity Thresholds allows you to specify some absolute lower bound for activity.</span></span> <span data-ttu-id="d9cf8-186">Jeśli żaden węzeł nie jest powyżej tego progu, równoważenia nie jest wyzwalane, nawet jeśli osiągnięty jest próg równoważenia.</span><span class="sxs-lookup"><span data-stu-id="d9cf8-186">If no node is over this threshold, balancing isn't triggered even if the Balancing Threshold is met.</span></span>

<span data-ttu-id="d9cf8-187">Załóżmy, że firma Microsoft będzie przechowywała naszych próg równoważenia trzech dla tej metryki.</span><span class="sxs-lookup"><span data-stu-id="d9cf8-187">Let’s say that we retain our Balancing Threshold of three for this metric.</span></span> <span data-ttu-id="d9cf8-188">Również Załóżmy, że mamy 1536 próg działania.</span><span class="sxs-lookup"><span data-stu-id="d9cf8-188">Let's also say we have an Activity Threshold of 1536.</span></span> <span data-ttu-id="d9cf8-189">W pierwszym przypadku gdy klaster jest imbalanced na brak próg równoważenia żaden węzeł nie spełnia tego progu działania, nic się nie dzieje.</span><span class="sxs-lookup"><span data-stu-id="d9cf8-189">In the first case, while the cluster is imbalanced per the Balancing Threshold there's no node meets that Activity Threshold, so nothing happens.</span></span> <span data-ttu-id="d9cf8-190">W przykładzie dolnej Node1 jest powyżej wartości progowej działania.</span><span class="sxs-lookup"><span data-stu-id="d9cf8-190">In the bottom example, Node1 is over the Activity Threshold.</span></span> <span data-ttu-id="d9cf8-191">Ponieważ przekroczona zarówno próg równoważenia i próg działania dla metryki równoważenia według harmonogramu.</span><span class="sxs-lookup"><span data-stu-id="d9cf8-191">Since both the Balancing Threshold and the Activity Threshold for the metric are exceeded, balancing is scheduled.</span></span> <span data-ttu-id="d9cf8-192">Na przykład Przyjrzyjmy się poniższym diagramie:</span><span class="sxs-lookup"><span data-stu-id="d9cf8-192">As an example, let's look at the following diagram:</span></span> 

<span data-ttu-id="d9cf8-193"><center>
![Przykład progu działania][Image3]
</center></span><span class="sxs-lookup"><span data-stu-id="d9cf8-193"><center>
![Activity Threshold Example][Image3]
</center></span></span>

<span data-ttu-id="d9cf8-194">Podobnie jak Równoważenie progi progi działania są zdefiniowane na — pomiar za pośrednictwem definicji klastra:</span><span class="sxs-lookup"><span data-stu-id="d9cf8-194">Just like Balancing Thresholds, Activity Thresholds are defined per-metric via the cluster definition:</span></span>

<span data-ttu-id="d9cf8-195">ClusterManifest.xml</span><span class="sxs-lookup"><span data-stu-id="d9cf8-195">ClusterManifest.xml</span></span>

``` xml
    <Section Name="MetricActivityThresholds">
      <Parameter Name="Memory" Value="1536"/>
    </Section>
```

<span data-ttu-id="d9cf8-196">za pomocą pliku ClusterConfig.json dla autonomicznych wdrożeniach lub Template.json dla platformy Azure hostowanej klastrów:</span><span class="sxs-lookup"><span data-stu-id="d9cf8-196">via ClusterConfig.json for Standalone deployments or Template.json for Azure hosted clusters:</span></span>

```json
"fabricSettings": [
  {
    "name": "MetricActivityThresholds",
    "parameters": [
      {
          "name": "Memory",
          "value": "1536"
      }
    ]
  }
]
```

<span data-ttu-id="d9cf8-197">Progi równoważenie i działania są oba związana z określonej metryki - równoważenia zostanie wywołany tylko wtedy, gdy Przekroczono próg równoważenia i próg działania dla tej samej metryki.</span><span class="sxs-lookup"><span data-stu-id="d9cf8-197">Balancing and activity thresholds are both tied to a specific metric - balancing is triggered only if both the Balancing Threshold and Activity Threshold is exceeded for the same metric.</span></span>

## <a name="balancing-services-together"></a><span data-ttu-id="d9cf8-198">Razem równoważenia usług</span><span class="sxs-lookup"><span data-stu-id="d9cf8-198">Balancing services together</span></span>
<span data-ttu-id="d9cf8-199">Klaster jest imbalanced lub nie jest decyzja całego klastra.</span><span class="sxs-lookup"><span data-stu-id="d9cf8-199">Whether the cluster is imbalanced or not is a cluster-wide decision.</span></span> <span data-ttu-id="d9cf8-200">Jednak sposób rozszerzana o naprawienie go przenoszone replik poszczególnych usług i wystąpień wokół.</span><span class="sxs-lookup"><span data-stu-id="d9cf8-200">However, the way we go about fixing it is moving individual service replicas and instances around.</span></span> <span data-ttu-id="d9cf8-201">To sens, PRAWDA?</span><span class="sxs-lookup"><span data-stu-id="d9cf8-201">This makes sense, right?</span></span> <span data-ttu-id="d9cf8-202">Jeśli pamięci jest skumulowany na jednym węźle, wiele replik lub wystąpień może przyczyniać się do niego.</span><span class="sxs-lookup"><span data-stu-id="d9cf8-202">If memory is stacked up on one node, multiple replicas or instances could be contributing to it.</span></span> <span data-ttu-id="d9cf8-203">Ustalania nierównowagi może wymagać przenoszenie żadnego z repliki stanowego lub bezstanowego wystąpieniom imbalanced metryki.</span><span class="sxs-lookup"><span data-stu-id="d9cf8-203">Fixing the imbalance could require moving any of the stateful replicas or stateless instances that use the imbalanced metric.</span></span>

<span data-ttu-id="d9cf8-204">Od czasu do czasu, gdy usługi, której sam imbalanced nie pobiera przenieść (Pamiętaj dyskusji lokalnych i globalnych przeprowadzi wcześniej).</span><span class="sxs-lookup"><span data-stu-id="d9cf8-204">Occasionally though, a service that wasn’t itself imbalanced gets moved (remember the discussion of local and global weights earlier).</span></span> <span data-ttu-id="d9cf8-205">Dlaczego czy usługi są przenoszone podczas wszystkie opcje, które zostały zrównoważonym metryki usługi?</span><span class="sxs-lookup"><span data-stu-id="d9cf8-205">Why would a service get moved when all that service’s metrics were balanced?</span></span> <span data-ttu-id="d9cf8-206">Zobaczmy:</span><span class="sxs-lookup"><span data-stu-id="d9cf8-206">Let’s see an example:</span></span>

- <span data-ttu-id="d9cf8-207">Załóżmy, że istnieją cztery usług, Service1 roboczego2, Service3 i Service4.</span><span class="sxs-lookup"><span data-stu-id="d9cf8-207">Let's say there are four services, Service1, Service2, Service3, and Service4.</span></span> 
- <span data-ttu-id="d9cf8-208">Service1 raporty metryk Metric1 i Metric2.</span><span class="sxs-lookup"><span data-stu-id="d9cf8-208">Service1 reports metrics Metric1 and Metric2.</span></span> 
- <span data-ttu-id="d9cf8-209">Klienta2 raporty metryk Metric2 i Metric3.</span><span class="sxs-lookup"><span data-stu-id="d9cf8-209">Service2 reports metrics Metric2 and Metric3.</span></span> 
- <span data-ttu-id="d9cf8-210">Service3 raporty metryk Metric3 i Metric4.</span><span class="sxs-lookup"><span data-stu-id="d9cf8-210">Service3 reports metrics Metric3 and Metric4.</span></span>
- <span data-ttu-id="d9cf8-211">Service4 raporty Metric99 metryki.</span><span class="sxs-lookup"><span data-stu-id="d9cf8-211">Service4 reports metric Metric99.</span></span> 

<span data-ttu-id="d9cf8-212">Z pewnością widać, gdy chcemy tutaj: istnieje łańcuch!</span><span class="sxs-lookup"><span data-stu-id="d9cf8-212">Surely you can see where we’re going here: There's a chain!</span></span> <span data-ttu-id="d9cf8-213">Nie mamy naprawdę cztery usługi niezależne, będziemy mieć trzy usługi, które są powiązane i taki, który jest wyłączony na jego własnej.</span><span class="sxs-lookup"><span data-stu-id="d9cf8-213">We don’t really have four independent services, we have three services that are related and one that is off on its own.</span></span>

<span data-ttu-id="d9cf8-214"><center>
![Razem równoważenia usług][Image4]
</center></span><span class="sxs-lookup"><span data-stu-id="d9cf8-214"><center>
![Balancing Services Together][Image4]
</center></span></span>

<span data-ttu-id="d9cf8-215">Ze względu na tym łańcuchu jest możliwe, że nierównowaga w metryki 1-4 może spowodować repliki lub wystąpienia należące do usługi 1-3, aby poruszać się po.</span><span class="sxs-lookup"><span data-stu-id="d9cf8-215">Because of this chain, it's possible that an imbalance in metrics 1-4 can cause replicas or instances belonging to services 1-3 to move around.</span></span> <span data-ttu-id="d9cf8-216">Wiemy, również nierównowaga w metryki 1, 2 lub 3 nie może spowodować przeniesień w Service4.</span><span class="sxs-lookup"><span data-stu-id="d9cf8-216">We also know that an imbalance in Metrics 1, 2, or 3 can't cause movements in Service4.</span></span> <span data-ttu-id="d9cf8-217">Ponieważ przenoszenie replik nie byłoby żadnego punktu lub wystąpienia należące do Service4 wokół można całkowicie nic nie rób wpłynąć na saldo metryki 1-3.</span><span class="sxs-lookup"><span data-stu-id="d9cf8-217">There would be no point since moving the replicas or instances belonging to Service4 around can do absolutely nothing to impact the balance of Metrics 1-3.</span></span>

<span data-ttu-id="d9cf8-218">Menedżer zasobów klastra automatycznie danych liczbowych się tym, które usługi są powiązane.</span><span class="sxs-lookup"><span data-stu-id="d9cf8-218">The Cluster Resource Manager automatically figures out what services are related.</span></span> <span data-ttu-id="d9cf8-219">Dodawanie, usuwanie lub Zmiana metryki dla usługi może mieć wpływ na ich relacji.</span><span class="sxs-lookup"><span data-stu-id="d9cf8-219">Adding, removing, or changing the metrics for services can impact their relationships.</span></span> <span data-ttu-id="d9cf8-220">Na przykład między dwa przebiegi równoważenia klienta2 mogły zostać zaktualizowane do usunięcia Metric2.</span><span class="sxs-lookup"><span data-stu-id="d9cf8-220">For example, between two runs of balancing Service2 may have been updated to remove Metric2.</span></span> <span data-ttu-id="d9cf8-221">To spowoduje przerwanie łańcucha między Service1 i klienta2.</span><span class="sxs-lookup"><span data-stu-id="d9cf8-221">This breaks the chain between Service1 and Service2.</span></span> <span data-ttu-id="d9cf8-222">Teraz zamiast dwie grupy usług, istnieją trzy:</span><span class="sxs-lookup"><span data-stu-id="d9cf8-222">Now instead of two groups of related services, there are three:</span></span>

<span data-ttu-id="d9cf8-223"><center>
![Razem równoważenia usług][Image5]
</center></span><span class="sxs-lookup"><span data-stu-id="d9cf8-223"><center>
![Balancing Services Together][Image5]
</center></span></span>

## <a name="next-steps"></a><span data-ttu-id="d9cf8-224">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="d9cf8-224">Next steps</span></span>
* <span data-ttu-id="d9cf8-225">Metryki są zarządzaniu Menedżer zasobów klastra sieci szkieletowej usług konsumenckich i pojemności w klastrze.</span><span class="sxs-lookup"><span data-stu-id="d9cf8-225">Metrics are how the Service Fabric Cluster Resource Manger manages consumption and capacity in the cluster.</span></span> <span data-ttu-id="d9cf8-226">Aby dowiedzieć się więcej na temat metryki i sposobach ich konfigurowania, zapoznaj się [w tym artykule](service-fabric-cluster-resource-manager-metrics.md)</span><span class="sxs-lookup"><span data-stu-id="d9cf8-226">To learn more about metrics and how to configure them, check out [this article](service-fabric-cluster-resource-manager-metrics.md)</span></span>
* <span data-ttu-id="d9cf8-227">Koszt przeniesienia jest jednym ze sposobów sygnalizowania Menedżera zasobów do klastra, że niektórych usług są droższe do przeniesienia od innych.</span><span class="sxs-lookup"><span data-stu-id="d9cf8-227">Movement Cost is one way of signaling to the Cluster Resource Manager that certain services are more expensive to move than others.</span></span> <span data-ttu-id="d9cf8-228">Więcej informacji o koszt przeniesienia, można znaleźć w temacie [w tym artykule](service-fabric-cluster-resource-manager-movement-cost.md)</span><span class="sxs-lookup"><span data-stu-id="d9cf8-228">For more about movement cost, refer to [this article](service-fabric-cluster-resource-manager-movement-cost.md)</span></span>
* <span data-ttu-id="d9cf8-229">Menedżer zasobów klastra ma kilka limity, które można skonfigurować tak, aby zwolnić postęp dokonany w klastrze.</span><span class="sxs-lookup"><span data-stu-id="d9cf8-229">The Cluster Resource Manager has several throttles that you can configure to slow down churn in the cluster.</span></span> <span data-ttu-id="d9cf8-230">Nie są one zazwyczaj konieczne, ale jeśli są potrzebne informacje na temat ich [tutaj](service-fabric-cluster-resource-manager-advanced-throttling.md)</span><span class="sxs-lookup"><span data-stu-id="d9cf8-230">They're not normally necessary, but if you need them you can learn about them [here](service-fabric-cluster-resource-manager-advanced-throttling.md)</span></span>

[Image1]:./media/service-fabric-cluster-resource-manager-balancing/cluster-resrouce-manager-balancing-thresholds.png
[Image2]:./media/service-fabric-cluster-resource-manager-balancing/cluster-resource-manager-balancing-threshold-triggered-results.png
[Image3]:./media/service-fabric-cluster-resource-manager-balancing/cluster-resource-manager-activity-thresholds.png
[Image4]:./media/service-fabric-cluster-resource-manager-balancing/cluster-resource-manager-balancing-services-together1.png
[Image5]:./media/service-fabric-cluster-resource-manager-balancing/cluster-resource-manager-balancing-services-together2.png
