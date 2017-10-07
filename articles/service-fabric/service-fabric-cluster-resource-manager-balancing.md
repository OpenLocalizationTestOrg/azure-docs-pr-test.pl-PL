---
title: "aaaBalance klastra usługi sieć szkieletowa usług Azure | Dokumentacja firmy Microsoft"
description: "Wprowadzenie toobalancing klastra za pomocą hello zasobu klastra sieci szkieletowej programu Service Manager."
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
ms.openlocfilehash: 5f7ad2f5cf4cfb3751a860f5293b03d2d5266d99
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="balancing-your-service-fabric-cluster"></a><span data-ttu-id="0d079-103">Równoważenie klastra sieci szkieletowej usług</span><span class="sxs-lookup"><span data-stu-id="0d079-103">Balancing your service fabric cluster</span></span>
<span data-ttu-id="0d079-104">Hello zasobu klastra sieci szkieletowej programu Service Manager obsługuje dynamicznego obciążenia zmian, dające dodatnią reakcję tooadditions lub usuwania węzłów lub usług.</span><span class="sxs-lookup"><span data-stu-id="0d079-104">hello Service Fabric Cluster Resource Manager supports dynamic load changes, reacting tooadditions or removals of nodes or services.</span></span> <span data-ttu-id="0d079-105">Automatycznie koryguje naruszenia ograniczeń i aktywne rebalances hello klastra.</span><span class="sxs-lookup"><span data-stu-id="0d079-105">It also automatically corrects constraint violations, and proactively rebalances hello cluster.</span></span> <span data-ttu-id="0d079-106">Jak często są te akcje podjęte — a wywołujących je?</span><span class="sxs-lookup"><span data-stu-id="0d079-106">But how often are these actions taken, and what triggers them?</span></span>

<span data-ttu-id="0d079-107">Istnieją trzy różne kategorie pracy tego powitalne Menedżer zasobów klastra.</span><span class="sxs-lookup"><span data-stu-id="0d079-107">There are three different categories of work that hello Cluster Resource Manager performs.</span></span> <span data-ttu-id="0d079-108">Są to:</span><span class="sxs-lookup"><span data-stu-id="0d079-108">They are:</span></span>

1. <span data-ttu-id="0d079-109">Rozmieszczenia — ten etap dotyczy umieszczenie replik stanowe ani bezstanowych wystąpień, które nie są spełnione.</span><span class="sxs-lookup"><span data-stu-id="0d079-109">Placement – this stage deals with placing any stateful replicas or stateless instances that are missing.</span></span> <span data-ttu-id="0d079-110">Umieszczanie zawiera nowe usługi i obsługa repliki stanowego lub bezstanowego wystąpień, których nie powiodła.</span><span class="sxs-lookup"><span data-stu-id="0d079-110">Placement includes both new services and handling stateful replicas or stateless instances that have failed.</span></span> <span data-ttu-id="0d079-111">Usuwanie i usunięcie repliki lub wystąpienia są obsługiwane w tym miejscu.</span><span class="sxs-lookup"><span data-stu-id="0d079-111">Deleting and dropping replicas or instances are handled here.</span></span>
2. <span data-ttu-id="0d079-112">Ograniczenie sprawdza — ten etap sprawdza i koryguje naruszenia ograniczeń umieszczania różnych hello (reguły) w systemie hello.</span><span class="sxs-lookup"><span data-stu-id="0d079-112">Constraint Checks – this stage checks for and corrects violations of hello different placement constraints (rules) within hello system.</span></span> <span data-ttu-id="0d079-113">Przykłady reguł jest rzeczy, takich jak zapewnienie, że węzły nie są przeciążone i że spełnione są ograniczenia umieszczania usług.</span><span class="sxs-lookup"><span data-stu-id="0d079-113">Examples of rules are things like ensuring that nodes are not over capacity and that a service’s placement constraints are met.</span></span>
3. <span data-ttu-id="0d079-114">Równoważenie — ten etap sprawdza toosee, jeśli ponowne równoważenie niezbędne jest oparte na powitania skonfigurowane żądany poziom saldo dla różnych metryki.</span><span class="sxs-lookup"><span data-stu-id="0d079-114">Balancing – this stage checks toosee if rebalancing is necessary based on hello configured desired level of balance for different metrics.</span></span> <span data-ttu-id="0d079-115">Jeśli tak podejmie toofind rozmieszczenia w hello klastra to znaczy więcej zrównoważonym.</span><span class="sxs-lookup"><span data-stu-id="0d079-115">If so it attempts toofind an arrangement in hello cluster that is more balanced.</span></span>

## <a name="configuring-cluster-resource-manager-timers"></a><span data-ttu-id="0d079-116">Konfigurowanie czasomierze Menedżera zasobów klastra</span><span class="sxs-lookup"><span data-stu-id="0d079-116">Configuring Cluster Resource Manager Timers</span></span>
<span data-ttu-id="0d079-117">pierwszy zestaw kontrolek wokół równoważenia Hello są zestawem czasomierze.</span><span class="sxs-lookup"><span data-stu-id="0d079-117">hello first set of controls around balancing are a set of timers.</span></span> <span data-ttu-id="0d079-118">Czasomierze te określają, jak często hello Cluster Resource Manager sprawdza hello klastra i wykonuje akcje naprawcze.</span><span class="sxs-lookup"><span data-stu-id="0d079-118">These timers govern how often hello Cluster Resource Manager examines hello cluster and takes corrective actions.</span></span>

<span data-ttu-id="0d079-119">Każdy z tych różnego rodzaju powitalne poprawki Menedżera zasobów klastra można wprowadzać jest kontrolowana przez inną czasomierza kontroluje częstotliwość.</span><span class="sxs-lookup"><span data-stu-id="0d079-119">Each of these different types of corrections hello Cluster Resource Manager can make is controlled by a different timer that governs its frequency.</span></span> <span data-ttu-id="0d079-120">Po każdym czasomierza, hello zadanie zostało zaplanowane.</span><span class="sxs-lookup"><span data-stu-id="0d079-120">When each timer fires, hello task is scheduled.</span></span> <span data-ttu-id="0d079-121">Domyślnie hello Menedżera zasobów:</span><span class="sxs-lookup"><span data-stu-id="0d079-121">By default hello Resource Manager:</span></span>

* <span data-ttu-id="0d079-122">skanuje stanu i stosuje aktualizacje (na przykład rejestrowania, który jest węzłem w dół) co 1/10 sekundy</span><span class="sxs-lookup"><span data-stu-id="0d079-122">scans its state and applies updates (like recording that a node is down) every 1/10th of a second</span></span>
* <span data-ttu-id="0d079-123">Ustawia flagę wyboru umieszczenia hello</span><span class="sxs-lookup"><span data-stu-id="0d079-123">sets hello placement check flag</span></span> 
* <span data-ttu-id="0d079-124">Ustawia flagę wyboru ograniczenia hello co sekundę</span><span class="sxs-lookup"><span data-stu-id="0d079-124">sets hello constraint check flag every second</span></span>
* <span data-ttu-id="0d079-125">Ustawia hello równoważenia flagi co pięć sekund.</span><span class="sxs-lookup"><span data-stu-id="0d079-125">sets hello balancing flag every five seconds.</span></span>

<span data-ttu-id="0d079-126">Przykłady dotyczące tych czasomierze konfiguracji hello jest poniżej:</span><span class="sxs-lookup"><span data-stu-id="0d079-126">Examples of hello configuration governing these timers are below:</span></span>

<span data-ttu-id="0d079-127">ClusterManifest.xml:</span><span class="sxs-lookup"><span data-stu-id="0d079-127">ClusterManifest.xml:</span></span>

``` xml
        <Section Name="PlacementAndLoadBalancing">
            <Parameter Name="PLBRefreshGap" Value="0.1" />
            <Parameter Name="MinPlacementInterval" Value="1.0" />
            <Parameter Name="MinConstraintCheckInterval" Value="1.0" />
            <Parameter Name="MinLoadBalancingInterval" Value="5.0" />
        </Section>
```

<span data-ttu-id="0d079-128">za pomocą pliku ClusterConfig.json dla autonomicznych wdrożeniach lub Template.json dla platformy Azure hostowanej klastrów:</span><span class="sxs-lookup"><span data-stu-id="0d079-128">via ClusterConfig.json for Standalone deployments or Template.json for Azure hosted clusters:</span></span>

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

<span data-ttu-id="0d079-129">Dzisiaj hello Menedżera zasobów klastra tylko wykonuje jedno z następujących działań w czasie, po kolei.</span><span class="sxs-lookup"><span data-stu-id="0d079-129">Today hello Cluster Resource Manager only performs one of these actions at a time, sequentially.</span></span> <span data-ttu-id="0d079-130">To dlatego firma Microsoft można znaleźć czasomierze toothese "minimalna interwałem" i działania, które uzyskać wykonane podczas czasomierze hello go jako "ustawienie flagi" hello.</span><span class="sxs-lookup"><span data-stu-id="0d079-130">This is why we refer toothese timers as “minimum intervals” and hello actions that get taken when hello timers go off as "setting flags".</span></span> <span data-ttu-id="0d079-131">Na przykład powitalne Menedżera zasobów klastra zajmuje się oczekujące żądania usług toocreate przed hello klastra równoważenia.</span><span class="sxs-lookup"><span data-stu-id="0d079-131">For example, hello Cluster Resource Manager takes care of pending requests toocreate services before balancing hello cluster.</span></span> <span data-ttu-id="0d079-132">Jak widać według przedziałów czasu domyślne hello określonych hello Menedżera zasobów klastra szuka niczego go toodo potrzeb często.</span><span class="sxs-lookup"><span data-stu-id="0d079-132">As you can see by hello default time intervals specified, hello Cluster Resource Manager scans for anything it needs toodo frequently.</span></span> <span data-ttu-id="0d079-133">Zwykle oznacza to, że zestaw hello zmiany wprowadzone podczas każdego kroku ma mała.</span><span class="sxs-lookup"><span data-stu-id="0d079-133">Normally this means that hello set of changes made during each step is small.</span></span> <span data-ttu-id="0d079-134">Zmiany wprowadzone w małych często umożliwia hello toobe Menedżera zasobów klastra odpowiadać podczas to wiele problemów w klastrze hello.</span><span class="sxs-lookup"><span data-stu-id="0d079-134">Making small changes frequently allows hello Cluster Resource Manager toobe responsive when things happen in hello cluster.</span></span> <span data-ttu-id="0d079-135">Hello czasomierze domyślne podać niektóre przetwarzanie wsadowe od wielu hello same rodzaje zdarzeń zwykle toooccur jednocześnie.</span><span class="sxs-lookup"><span data-stu-id="0d079-135">hello default timers provide some batching since many of hello same types of events tend toooccur simultaneously.</span></span> 

<span data-ttu-id="0d079-136">Na przykład po awarii węzłów robią to całego domen błędów w czasie.</span><span class="sxs-lookup"><span data-stu-id="0d079-136">For example, when nodes fail they can do so entire fault domains at a time.</span></span> <span data-ttu-id="0d079-137">Wszystkie te błędy są przechwytywane podczas hello następny stan aktualizacji po hello *PLBRefreshGap*.</span><span class="sxs-lookup"><span data-stu-id="0d079-137">All these failures are captured during hello next state update after hello *PLBRefreshGap*.</span></span> <span data-ttu-id="0d079-138">poprawki Hello są określane podczas powitania po umieszczania, sprawdzanie ograniczenia i Równoważenie działa.</span><span class="sxs-lookup"><span data-stu-id="0d079-138">hello corrections are determined during hello following placement, constraint check, and balancing runs.</span></span> <span data-ttu-id="0d079-139">Przez domyślny hello Menedżera zasobów klastra nie jest skanowanie za pomocą godziny zmian w klastrze hello i podjęcie próby tooaddress wszystkie zmiany na raz.</span><span class="sxs-lookup"><span data-stu-id="0d079-139">By default hello Cluster Resource Manager is not scanning through hours of changes in hello cluster and trying tooaddress all changes at once.</span></span> <span data-ttu-id="0d079-140">W ten sposób może spowodować toobursts zmian.</span><span class="sxs-lookup"><span data-stu-id="0d079-140">Doing so would lead toobursts of churn.</span></span>

<span data-ttu-id="0d079-141">Hello Menedżera zasobów klastra musi także niektóre toodetermine dodatkowe informacje klastrowania hello imbalanced.</span><span class="sxs-lookup"><span data-stu-id="0d079-141">hello Cluster Resource Manager also needs some additional information toodetermine if hello cluster imbalanced.</span></span> <span data-ttu-id="0d079-142">W tym mamy dwóch elementów konfiguracji: *BalancingThresholds* i *ActivityThresholds*.</span><span class="sxs-lookup"><span data-stu-id="0d079-142">For that we have two other pieces of configuration: *BalancingThresholds* and *ActivityThresholds*.</span></span>

## <a name="balancing-thresholds"></a><span data-ttu-id="0d079-143">Równoważenie progi</span><span class="sxs-lookup"><span data-stu-id="0d079-143">Balancing thresholds</span></span>
<span data-ttu-id="0d079-144">Próg równoważenia jest formantu hello służącą do wyzwalania ponowne równoważenie.</span><span class="sxs-lookup"><span data-stu-id="0d079-144">A Balancing Threshold is hello main control for triggering rebalancing.</span></span> <span data-ttu-id="0d079-145">Witaj równoważenia próg dla metryki jest _współczynnik_.</span><span class="sxs-lookup"><span data-stu-id="0d079-145">hello Balancing Threshold for a metric is a _ratio_.</span></span> <span data-ttu-id="0d079-146">Jeśli hello obciążenia dla metryki na powitania najbardziej załadowany węzła rozdzielonych hello wielkość obciążenia na powitania najmniej załadować węzła przekracza tego Metryka *BalancingThreshold*, klaster hello jest imbalanced.</span><span class="sxs-lookup"><span data-stu-id="0d079-146">If hello load for a metric on hello most loaded node divided by hello amount of load on hello least loaded node exceeds that metric's *BalancingThreshold*, then hello cluster is imbalanced.</span></span> <span data-ttu-id="0d079-147">W związku z tym równoważenia jest wyzwalana hello dalej czasu powitalne sprawdza Menedżera zasobów klastra.</span><span class="sxs-lookup"><span data-stu-id="0d079-147">As a result balancing is triggered hello next time hello Cluster Resource Manager checks.</span></span> <span data-ttu-id="0d079-148">Witaj *MinLoadBalancingInterval* czasomierza Określa, jak często hello Menedżera zasobów klastra powinna Sprawdź, czy konieczne jest ponowne równoważenie.</span><span class="sxs-lookup"><span data-stu-id="0d079-148">hello *MinLoadBalancingInterval* timer defines how often hello Cluster Resource Manager should check if rebalancing is necessary.</span></span> <span data-ttu-id="0d079-149">Sprawdzanie nie oznacza, że awarii.</span><span class="sxs-lookup"><span data-stu-id="0d079-149">Checking doesn't mean that anything happens.</span></span> 

<span data-ttu-id="0d079-150">Progi równoważenia są zdefiniowane w zasadzie na Metryka jako część definicji klastra hello.</span><span class="sxs-lookup"><span data-stu-id="0d079-150">Balancing Thresholds are defined on a per-metric basis as a part of hello cluster definition.</span></span> <span data-ttu-id="0d079-151">Aby uzyskać więcej informacji dotyczących metryki, zapoznaj się [w tym artykule](service-fabric-cluster-resource-manager-metrics.md).</span><span class="sxs-lookup"><span data-stu-id="0d079-151">For more information on metrics, check out [this article](service-fabric-cluster-resource-manager-metrics.md).</span></span>

<span data-ttu-id="0d079-152">ClusterManifest.xml</span><span class="sxs-lookup"><span data-stu-id="0d079-152">ClusterManifest.xml</span></span>

```xml
    <Section Name="MetricBalancingThresholds">
      <Parameter Name="MetricName1" Value="2"/>
      <Parameter Name="MetricName2" Value="3.5"/>
    </Section>
```

<span data-ttu-id="0d079-153">za pomocą pliku ClusterConfig.json dla autonomicznych wdrożeniach lub Template.json dla platformy Azure hostowanej klastrów:</span><span class="sxs-lookup"><span data-stu-id="0d079-153">via ClusterConfig.json for Standalone deployments or Template.json for Azure hosted clusters:</span></span>

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

<span data-ttu-id="0d079-154"><center>
![Równoważenie przykład próg][Image1]
</center></span><span class="sxs-lookup"><span data-stu-id="0d079-154"><center>
![Balancing Threshold Example][Image1]
</center></span></span>

<span data-ttu-id="0d079-155">W tym przykładzie każda usługa zajmuje jedną jednostkę niektóre metryki.</span><span class="sxs-lookup"><span data-stu-id="0d079-155">In this example, each service is consuming one unit of some metric.</span></span> <span data-ttu-id="0d079-156">W górnym przykład Witaj hello maksymalne obciążenie w węźle osiągnie wartość 5 i hello minimalna wynosi dwa.</span><span class="sxs-lookup"><span data-stu-id="0d079-156">In hello top example, hello maximum load on a node is five and hello minimum is two.</span></span> <span data-ttu-id="0d079-157">Załóżmy, że ten hello równoważenia próg ta metryka jest trzy.</span><span class="sxs-lookup"><span data-stu-id="0d079-157">Let’s say that hello balancing threshold for this metric is three.</span></span> <span data-ttu-id="0d079-158">Ponieważ współczynnik hello w klastrze hello jest 5/2 = 2.5 i który jest mniejszy niż określony hello równoważenia próg trzy, klaster hello jest rozmieszczana.</span><span class="sxs-lookup"><span data-stu-id="0d079-158">Since hello ratio in hello cluster is 5/2 = 2.5 and that is less than hello specified balancing threshold of three, hello cluster is balanced.</span></span> <span data-ttu-id="0d079-159">Bez równoważenia jest wyzwalane, gdy sprawdza hello Menedżera zasobów klastra.</span><span class="sxs-lookup"><span data-stu-id="0d079-159">No balancing is triggered when hello Cluster Resource Manager checks.</span></span>

<span data-ttu-id="0d079-160">W przykładzie dolnej hello hello maksymalne obciążenie w węźle wynosi 10, gdy hello jest co najmniej dwóch, co w stosunku pięć.</span><span class="sxs-lookup"><span data-stu-id="0d079-160">In hello bottom example, hello maximum load on a node is 10, while hello minimum is two, resulting in a ratio of five.</span></span> <span data-ttu-id="0d079-161">Pięć jest większa niż hello wyznaczonych próg równoważenia trzech dla tej metryki.</span><span class="sxs-lookup"><span data-stu-id="0d079-161">Five is greater than hello designated balancing threshold of three for that metric.</span></span> <span data-ttu-id="0d079-162">W związku z tym rebalancing Uruchom będzie zaplanowane hello czas następnego równoważenia uruchamiany czasomierza.</span><span class="sxs-lookup"><span data-stu-id="0d079-162">As a result, a rebalancing run will be scheduled next time hello balancing timer fires.</span></span> <span data-ttu-id="0d079-163">W sytuacji, jak to niektóre obciążenia jest zwykle rozproszonej tooNode3.</span><span class="sxs-lookup"><span data-stu-id="0d079-163">In a situation like this some load is usually distributed tooNode3.</span></span> <span data-ttu-id="0d079-164">Witaj zasobu klastra sieci szkieletowej programu Service Manager korzysta z podejścia intensywnie, niektóre obciążenia mogą być również tooNode2 rozproszonych.</span><span class="sxs-lookup"><span data-stu-id="0d079-164">Because hello Service Fabric Cluster Resource Manager doesn't use a greedy approach, some load could also be distributed tooNode2.</span></span> 

<span data-ttu-id="0d079-165"><center>
![Równoważenie akcje przykład próg][Image2]
</center></span><span class="sxs-lookup"><span data-stu-id="0d079-165"><center>
![Balancing Threshold Example Actions][Image2]
</center></span></span>

> [!NOTE]
> <span data-ttu-id="0d079-166">"" Równoważenie dwa różne strategie zarządzania obciążenia w klastrze.</span><span class="sxs-lookup"><span data-stu-id="0d079-166">"Balancing" handles two different strategies for managing load in your cluster.</span></span> <span data-ttu-id="0d079-167">strategii domyślne Hello hello używa Menedżera zasobów klastra jest toodistribute obciążenia w węzłach klastra hello hello.</span><span class="sxs-lookup"><span data-stu-id="0d079-167">hello default strategy that hello Cluster Resource Manager uses is toodistribute load across hello nodes in hello cluster.</span></span> <span data-ttu-id="0d079-168">Witaj innych strategii jest [defragmentacji](service-fabric-cluster-resource-manager-defragmentation-metrics.md).</span><span class="sxs-lookup"><span data-stu-id="0d079-168">hello other strategy is [defragmentation](service-fabric-cluster-resource-manager-defragmentation-metrics.md).</span></span> <span data-ttu-id="0d079-169">Defragmentacja jest wykonywane podczas hello równoważenia tego samego uruchomienia.</span><span class="sxs-lookup"><span data-stu-id="0d079-169">Defragmentation is performed during hello same balancing run.</span></span> <span data-ttu-id="0d079-170">Hello strategii równoważenia i defragmentacji może służyć do różnych metryk w hello tego samego klastra.</span><span class="sxs-lookup"><span data-stu-id="0d079-170">hello balancing and defragmentation strategies can be used for different metrics within hello same cluster.</span></span> <span data-ttu-id="0d079-171">Usługa może mieć równoważenia i defragmentacji metryki.</span><span class="sxs-lookup"><span data-stu-id="0d079-171">A service can have both balancing and defragmentation metrics.</span></span> <span data-ttu-id="0d079-172">Dla metryki defragmentacji hello stosunek hello jest ładowane w hello klastra wyzwala ponowne równoważenie, gdy jest _poniżej_ hello równoważenia próg.</span><span class="sxs-lookup"><span data-stu-id="0d079-172">For defragmentation metrics, hello ratio of hello loads in hello cluster triggers rebalancing when it is _below_ hello balancing threshold.</span></span> 
>

<span data-ttu-id="0d079-173">Pobieranie poniżej hello równoważenia próg nie jest celem jawnego.</span><span class="sxs-lookup"><span data-stu-id="0d079-173">Getting below hello balancing threshold is not an explicit goal.</span></span> <span data-ttu-id="0d079-174">Progi równoważenia są po prostu *wyzwalacza*.</span><span class="sxs-lookup"><span data-stu-id="0d079-174">Balancing Thresholds are just a *trigger*.</span></span> <span data-ttu-id="0d079-175">Podczas równoważenia działa, hello Menedżera zasobów klastra określa jakie ulepszenia go, jeśli istnieją.</span><span class="sxs-lookup"><span data-stu-id="0d079-175">When balancing runs, hello Cluster Resource Manager determines what improvements it can make, if any.</span></span> <span data-ttu-id="0d079-176">Tak, ponieważ zostało rozpoczęte równoważenia wyszukiwania nie oznacza niczego przenosi.</span><span class="sxs-lookup"><span data-stu-id="0d079-176">Just because a balancing search is kicked off doesn't mean anything moves.</span></span> <span data-ttu-id="0d079-177">Czasami hello klastra jest toocorrect imbalanced, ale zbyt ograniczone.</span><span class="sxs-lookup"><span data-stu-id="0d079-177">Sometimes hello cluster is imbalanced but too constrained toocorrect.</span></span> <span data-ttu-id="0d079-178">Alternatywnie ulepszenia hello wymagają przesunięcia, które są zbyt [kosztowne](service-fabric-cluster-resource-manager-movement-cost.md)).</span><span class="sxs-lookup"><span data-stu-id="0d079-178">Alternatively, hello improvements require movements that are too [costly](service-fabric-cluster-resource-manager-movement-cost.md)).</span></span>

## <a name="activity-thresholds"></a><span data-ttu-id="0d079-179">Progi działania</span><span class="sxs-lookup"><span data-stu-id="0d079-179">Activity thresholds</span></span>
<span data-ttu-id="0d079-180">Czasami, mimo że węzły są stosunkowo imbalanced, hello *całkowita* obciążenie klastra hello jest niska.</span><span class="sxs-lookup"><span data-stu-id="0d079-180">Sometimes, although nodes are relatively imbalanced, hello *total* amount of load in hello cluster is low.</span></span> <span data-ttu-id="0d079-181">Brak Hello obciążenia może być przejściowy dip lub załadować, ponieważ klaster hello jest nowy i po prostu pobierania.</span><span class="sxs-lookup"><span data-stu-id="0d079-181">hello lack of load could be a transient dip, or because hello cluster is new and just getting bootstrapped.</span></span> <span data-ttu-id="0d079-182">W obu przypadkach nie może być czas toospend hello klastra równoważenia, ponieważ brak małego toobe zdobytych.</span><span class="sxs-lookup"><span data-stu-id="0d079-182">In either case, you may not want toospend time balancing hello cluster because there’s little toobe gained.</span></span> <span data-ttu-id="0d079-183">Jeśli klaster hello zostały poddane równoważenia, czy spędzają sieci i obliczeniowe elementy toomove zasobów wokół bez wprowadzania żadnych dużych *bezwzględną* różnicy.</span><span class="sxs-lookup"><span data-stu-id="0d079-183">If hello cluster underwent balancing, you’d spend network and compute resources toomove things around without making any large *absolute* difference.</span></span> <span data-ttu-id="0d079-184">Przenosi tooavoid niepotrzebne, istnieje inny formant znany jako progi działania.</span><span class="sxs-lookup"><span data-stu-id="0d079-184">tooavoid unnecessary moves, there’s another control known as Activity Thresholds.</span></span> <span data-ttu-id="0d079-185">Progi działania umożliwia toospecify niektórych bezwzględną dolna granica dla działania.</span><span class="sxs-lookup"><span data-stu-id="0d079-185">Activity Thresholds allows you toospecify some absolute lower bound for activity.</span></span> <span data-ttu-id="0d079-186">Jeśli żaden węzeł nie jest powyżej tego progu, równoważenia nie jest wyzwalane, nawet jeśli hello równoważenia osiągnięty jest próg.</span><span class="sxs-lookup"><span data-stu-id="0d079-186">If no node is over this threshold, balancing isn't triggered even if hello Balancing Threshold is met.</span></span>

<span data-ttu-id="0d079-187">Załóżmy, że firma Microsoft będzie przechowywała naszych próg równoważenia trzech dla tej metryki.</span><span class="sxs-lookup"><span data-stu-id="0d079-187">Let’s say that we retain our Balancing Threshold of three for this metric.</span></span> <span data-ttu-id="0d079-188">Również Załóżmy, że mamy 1536 próg działania.</span><span class="sxs-lookup"><span data-stu-id="0d079-188">Let's also say we have an Activity Threshold of 1536.</span></span> <span data-ttu-id="0d079-189">W pierwszym przypadku hello podczas gdy klaster hello jest imbalanced na powitania równoważenia próg nie jest nie spełnia węzła progu działania, więc nic się nie dzieje.</span><span class="sxs-lookup"><span data-stu-id="0d079-189">In hello first case, while hello cluster is imbalanced per hello Balancing Threshold there's no node meets that Activity Threshold, so nothing happens.</span></span> <span data-ttu-id="0d079-190">Przykład Witaj dolnej Node1 znajduje się nad hello próg działania.</span><span class="sxs-lookup"><span data-stu-id="0d079-190">In hello bottom example, Node1 is over hello Activity Threshold.</span></span> <span data-ttu-id="0d079-191">Ponieważ oba hello równoważenia próg i hello próg działania dla metryki hello zostaną przekroczone, równoważenia według harmonogramu.</span><span class="sxs-lookup"><span data-stu-id="0d079-191">Since both hello Balancing Threshold and hello Activity Threshold for hello metric are exceeded, balancing is scheduled.</span></span> <span data-ttu-id="0d079-192">Na przykład Przyjrzyjmy się powitania po diagramu:</span><span class="sxs-lookup"><span data-stu-id="0d079-192">As an example, let's look at hello following diagram:</span></span> 

<span data-ttu-id="0d079-193"><center>
![Przykład progu działania][Image3]
</center></span><span class="sxs-lookup"><span data-stu-id="0d079-193"><center>
![Activity Threshold Example][Image3]
</center></span></span>

<span data-ttu-id="0d079-194">Podobnie jak Równoważenie progi progi działania są zdefiniowane na — pomiar za pośrednictwem definicji klastra hello:</span><span class="sxs-lookup"><span data-stu-id="0d079-194">Just like Balancing Thresholds, Activity Thresholds are defined per-metric via hello cluster definition:</span></span>

<span data-ttu-id="0d079-195">ClusterManifest.xml</span><span class="sxs-lookup"><span data-stu-id="0d079-195">ClusterManifest.xml</span></span>

``` xml
    <Section Name="MetricActivityThresholds">
      <Parameter Name="Memory" Value="1536"/>
    </Section>
```

<span data-ttu-id="0d079-196">za pomocą pliku ClusterConfig.json dla autonomicznych wdrożeniach lub Template.json dla platformy Azure hostowanej klastrów:</span><span class="sxs-lookup"><span data-stu-id="0d079-196">via ClusterConfig.json for Standalone deployments or Template.json for Azure hosted clusters:</span></span>

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

<span data-ttu-id="0d079-197">Progi równoważenie i działania są określonej metryki wiązanej tooa - równoważenia zostanie wywołany tylko wtedy, gdy oba hello równoważenia próg i przekroczeniu progu działania dla hello tę samą metrykę.</span><span class="sxs-lookup"><span data-stu-id="0d079-197">Balancing and activity thresholds are both tied tooa specific metric - balancing is triggered only if both hello Balancing Threshold and Activity Threshold is exceeded for hello same metric.</span></span>

## <a name="balancing-services-together"></a><span data-ttu-id="0d079-198">Razem równoważenia usług</span><span class="sxs-lookup"><span data-stu-id="0d079-198">Balancing services together</span></span>
<span data-ttu-id="0d079-199">Czy klaster hello jest imbalanced lub nie jest decyzja całego klastra.</span><span class="sxs-lookup"><span data-stu-id="0d079-199">Whether hello cluster is imbalanced or not is a cluster-wide decision.</span></span> <span data-ttu-id="0d079-200">Jednak sposób hello rozszerzana o naprawienie go przenoszone replik poszczególnych usług i wystąpień wokół.</span><span class="sxs-lookup"><span data-stu-id="0d079-200">However, hello way we go about fixing it is moving individual service replicas and instances around.</span></span> <span data-ttu-id="0d079-201">To sens, PRAWDA?</span><span class="sxs-lookup"><span data-stu-id="0d079-201">This makes sense, right?</span></span> <span data-ttu-id="0d079-202">Jeśli na jednym węźle umieszczany jest pamięć, wiele replik lub wystąpień może przyczyniać się tooit.</span><span class="sxs-lookup"><span data-stu-id="0d079-202">If memory is stacked up on one node, multiple replicas or instances could be contributing tooit.</span></span> <span data-ttu-id="0d079-203">Nierównowaga hello ustalające może wymagać przenoszenie tych hello repliki stanowego lub bezstanowego wystąpieniom Metryka imbalanced hello.</span><span class="sxs-lookup"><span data-stu-id="0d079-203">Fixing hello imbalance could require moving any of hello stateful replicas or stateless instances that use hello imbalanced metric.</span></span>

<span data-ttu-id="0d079-204">Od czasu do czasu, gdy usługi, której sam imbalanced nie pobiera przenieść (Pamiętaj dyskusji hello lokalnych i globalnych przeprowadzi wcześniej).</span><span class="sxs-lookup"><span data-stu-id="0d079-204">Occasionally though, a service that wasn’t itself imbalanced gets moved (remember hello discussion of local and global weights earlier).</span></span> <span data-ttu-id="0d079-205">Dlaczego czy usługi są przenoszone podczas wszystkie opcje, które zostały zrównoważonym metryki usługi?</span><span class="sxs-lookup"><span data-stu-id="0d079-205">Why would a service get moved when all that service’s metrics were balanced?</span></span> <span data-ttu-id="0d079-206">Zobaczmy:</span><span class="sxs-lookup"><span data-stu-id="0d079-206">Let’s see an example:</span></span>

- <span data-ttu-id="0d079-207">Załóżmy, że istnieją cztery usług, Service1 roboczego2, Service3 i Service4.</span><span class="sxs-lookup"><span data-stu-id="0d079-207">Let's say there are four services, Service1, Service2, Service3, and Service4.</span></span> 
- <span data-ttu-id="0d079-208">Service1 raporty metryk Metric1 i Metric2.</span><span class="sxs-lookup"><span data-stu-id="0d079-208">Service1 reports metrics Metric1 and Metric2.</span></span> 
- <span data-ttu-id="0d079-209">Klienta2 raporty metryk Metric2 i Metric3.</span><span class="sxs-lookup"><span data-stu-id="0d079-209">Service2 reports metrics Metric2 and Metric3.</span></span> 
- <span data-ttu-id="0d079-210">Service3 raporty metryk Metric3 i Metric4.</span><span class="sxs-lookup"><span data-stu-id="0d079-210">Service3 reports metrics Metric3 and Metric4.</span></span>
- <span data-ttu-id="0d079-211">Service4 raporty Metric99 metryki.</span><span class="sxs-lookup"><span data-stu-id="0d079-211">Service4 reports metric Metric99.</span></span> 

<span data-ttu-id="0d079-212">Z pewnością widać, gdy chcemy tutaj: istnieje łańcuch!</span><span class="sxs-lookup"><span data-stu-id="0d079-212">Surely you can see where we’re going here: There's a chain!</span></span> <span data-ttu-id="0d079-213">Nie mamy naprawdę cztery usługi niezależne, będziemy mieć trzy usługi, które są powiązane i taki, który jest wyłączony na jego własnej.</span><span class="sxs-lookup"><span data-stu-id="0d079-213">We don’t really have four independent services, we have three services that are related and one that is off on its own.</span></span>

<span data-ttu-id="0d079-214"><center>
![Razem równoważenia usług][Image4]
</center></span><span class="sxs-lookup"><span data-stu-id="0d079-214"><center>
![Balancing Services Together][Image4]
</center></span></span>

<span data-ttu-id="0d079-215">Ze względu na tym łańcuchu jest możliwe, że nierównowaga w metryki 1-4 może spowodować repliki lub wystąpień tooservices toomove 1 – 3 wokół.</span><span class="sxs-lookup"><span data-stu-id="0d079-215">Because of this chain, it's possible that an imbalance in metrics 1-4 can cause replicas or instances belonging tooservices 1-3 toomove around.</span></span> <span data-ttu-id="0d079-216">Wiemy, również nierównowaga w metryki 1, 2 lub 3 nie może spowodować przeniesień w Service4.</span><span class="sxs-lookup"><span data-stu-id="0d079-216">We also know that an imbalance in Metrics 1, 2, or 3 can't cause movements in Service4.</span></span> <span data-ttu-id="0d079-217">Ponieważ przenoszenie hello replik nie byłoby żaden punkt i wystąpień tooService4 wokół może nic nie absolutnie saldo hello tooimpact metryki 1-3.</span><span class="sxs-lookup"><span data-stu-id="0d079-217">There would be no point since moving hello replicas or instances belonging tooService4 around can do absolutely nothing tooimpact hello balance of Metrics 1-3.</span></span>

<span data-ttu-id="0d079-218">Witaj Menedżera zasobów klastra automatycznie danych liczbowych się tym, które usługi są powiązane.</span><span class="sxs-lookup"><span data-stu-id="0d079-218">hello Cluster Resource Manager automatically figures out what services are related.</span></span> <span data-ttu-id="0d079-219">Dodawanie, usuwanie lub zmiana hello metryki dla usługi mogą mieć wpływ na ich relacji.</span><span class="sxs-lookup"><span data-stu-id="0d079-219">Adding, removing, or changing hello metrics for services can impact their relationships.</span></span> <span data-ttu-id="0d079-220">Na przykład między dwa przebiegi równoważenia klienta2 mogły zostać zaktualizowane tooremove Metric2.</span><span class="sxs-lookup"><span data-stu-id="0d079-220">For example, between two runs of balancing Service2 may have been updated tooremove Metric2.</span></span> <span data-ttu-id="0d079-221">To spowoduje przerwanie łańcucha hello między Service1 i klienta2.</span><span class="sxs-lookup"><span data-stu-id="0d079-221">This breaks hello chain between Service1 and Service2.</span></span> <span data-ttu-id="0d079-222">Teraz zamiast dwie grupy usług, istnieją trzy:</span><span class="sxs-lookup"><span data-stu-id="0d079-222">Now instead of two groups of related services, there are three:</span></span>

<span data-ttu-id="0d079-223"><center>
![Razem równoważenia usług][Image5]
</center></span><span class="sxs-lookup"><span data-stu-id="0d079-223"><center>
![Balancing Services Together][Image5]
</center></span></span>

## <a name="next-steps"></a><span data-ttu-id="0d079-224">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="0d079-224">Next steps</span></span>
* <span data-ttu-id="0d079-225">Metryki są zarządzaniu hello Menedżer zasobów klastra sieci szkieletowej usług konsumenckich i pojemności w klastrze hello.</span><span class="sxs-lookup"><span data-stu-id="0d079-225">Metrics are how hello Service Fabric Cluster Resource Manger manages consumption and capacity in hello cluster.</span></span> <span data-ttu-id="0d079-226">więcej informacji na temat metryki toolearn i jak tooconfigure, zapoznaj się z [w tym artykule](service-fabric-cluster-resource-manager-metrics.md)</span><span class="sxs-lookup"><span data-stu-id="0d079-226">toolearn more about metrics and how tooconfigure them, check out [this article](service-fabric-cluster-resource-manager-metrics.md)</span></span>
* <span data-ttu-id="0d079-227">Koszt przeniesienia jest jednym ze sposobów sygnalizowania toohello Menedżera zasobów klastra, że niektóre usługi są toomove droższe niż inne.</span><span class="sxs-lookup"><span data-stu-id="0d079-227">Movement Cost is one way of signaling toohello Cluster Resource Manager that certain services are more expensive toomove than others.</span></span> <span data-ttu-id="0d079-228">Aby uzyskać więcej informacji o koszt przeniesienia odwoływać się za[w tym artykule](service-fabric-cluster-resource-manager-movement-cost.md)</span><span class="sxs-lookup"><span data-stu-id="0d079-228">For more about movement cost, refer too[this article](service-fabric-cluster-resource-manager-movement-cost.md)</span></span>
* <span data-ttu-id="0d079-229">Witaj Menedżera zasobów klastra ma kilka limity skonfigurowania tooslow dół przenoszenie hello klastra.</span><span class="sxs-lookup"><span data-stu-id="0d079-229">hello Cluster Resource Manager has several throttles that you can configure tooslow down churn in hello cluster.</span></span> <span data-ttu-id="0d079-230">Nie są one zazwyczaj konieczne, ale jeśli są potrzebne informacje na temat ich [tutaj](service-fabric-cluster-resource-manager-advanced-throttling.md)</span><span class="sxs-lookup"><span data-stu-id="0d079-230">They're not normally necessary, but if you need them you can learn about them [here](service-fabric-cluster-resource-manager-advanced-throttling.md)</span></span>

[Image1]:./media/service-fabric-cluster-resource-manager-balancing/cluster-resrouce-manager-balancing-thresholds.png
[Image2]:./media/service-fabric-cluster-resource-manager-balancing/cluster-resource-manager-balancing-threshold-triggered-results.png
[Image3]:./media/service-fabric-cluster-resource-manager-balancing/cluster-resource-manager-activity-thresholds.png
[Image4]:./media/service-fabric-cluster-resource-manager-balancing/cluster-resource-manager-balancing-services-together1.png
[Image5]:./media/service-fabric-cluster-resource-manager-balancing/cluster-resource-manager-balancing-services-together2.png
