---
title: "aaaService Menedżer zasobów klastra sieci szkieletowej — zasady umieszczania | Dokumentacja firmy Microsoft"
description: "Omówienie zasad umieszczania dodatkowe i zasady usługi sieci szkieletowej usług"
services: service-fabric
documentationcenter: .net
author: masnider
manager: timlt
editor: 
ms.assetid: 5c2d19c6-dd40-4c4b-abd3-5c5ec0abed38
ms.service: Service-Fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/18/2017
ms.author: masnider
ms.openlocfilehash: bb58642520085ab3000f3929cf9aea7a8f6e3070
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="placement-policies-for-service-fabric-services"></a><span data-ttu-id="10577-103">Zasady umieszczania dla usługi sieci szkieletowej usług</span><span class="sxs-lookup"><span data-stu-id="10577-103">Placement policies for service fabric services</span></span>
<span data-ttu-id="10577-104">Zasady umieszczania są dodatkowe reguły, które mogą być rozmieszczenie usługi toogovern używane w niektórych scenariuszach określone, typowe mniej.</span><span class="sxs-lookup"><span data-stu-id="10577-104">Placement policies are additional rules that can be used toogovern service placement in some specific, less-common scenarios.</span></span> <span data-ttu-id="10577-105">Przykłady takich scenariuszy to:</span><span class="sxs-lookup"><span data-stu-id="10577-105">Some examples of those scenarios are:</span></span>

- <span data-ttu-id="10577-106">Klaster usługi Service Fabric obejmuje odległości geograficznego, takich jak wiele lokalnych centrów danych lub w regionach platformy Azure</span><span class="sxs-lookup"><span data-stu-id="10577-106">Your Service Fabric cluster spans geographic distances, such as multiple on-premises datacenters or across Azure regions</span></span>
- <span data-ttu-id="10577-107">Środowiska obejmuje wiele obszarów kontrolki geograficznymi lub prawnych lub innym przypadku, gdy masz zasada granic należy tooenforce</span><span class="sxs-lookup"><span data-stu-id="10577-107">Your environment spans multiple areas of geopolitical or legal control, or some other case where you have policy boundaries you need tooenforce</span></span>
- <span data-ttu-id="10577-108">Brak komunikacji wydajności lub opóźnień zagadnienia odległości toolarge lub użyj łączy sieciowych wolniejszych lub bardziej zawodne</span><span class="sxs-lookup"><span data-stu-id="10577-108">There are communication performance or latency considerations due toolarge distances or use of slower or less reliable network links</span></span>
- <span data-ttu-id="10577-109">Należy tookeep dla określonych obciążeń rozmieszczony wspólnie jako starań, z innymi obciążeniami lub w sąsiedztwie toocustomers</span><span class="sxs-lookup"><span data-stu-id="10577-109">You need tookeep certain workloads collocated as a best effort, either with other workloads or in proximity toocustomers</span></span>

<span data-ttu-id="10577-110">Większość wymagań dostosowanie hello fizycznego układu hello klastra, reprezentowany jako hello domen błędów hello klastra.</span><span class="sxs-lookup"><span data-stu-id="10577-110">Most of these requirements align with hello physical layout of hello cluster, represented as hello fault domains of hello cluster.</span></span> 

<span data-ttu-id="10577-111">Witaj umieszczania zaawansowanych zasad, które wyjść naprzeciw te scenariusze są następujące:</span><span class="sxs-lookup"><span data-stu-id="10577-111">hello advanced placement policies that help address these scenarios are:</span></span>

1. <span data-ttu-id="10577-112">Nieprawidłowy domen</span><span class="sxs-lookup"><span data-stu-id="10577-112">Invalid domains</span></span>
2. <span data-ttu-id="10577-113">Wymagane domen</span><span class="sxs-lookup"><span data-stu-id="10577-113">Required domains</span></span>
3. <span data-ttu-id="10577-114">Wykorzystanie preferowanych domen</span><span class="sxs-lookup"><span data-stu-id="10577-114">Preferred domains</span></span>
4. <span data-ttu-id="10577-115">Brak zezwolenia pakowania repliki</span><span class="sxs-lookup"><span data-stu-id="10577-115">Disallowing replica packing</span></span>

<span data-ttu-id="10577-116">Większość powitania po formantów można skonfigurować za pomocą właściwości węzła i ograniczenia dotyczące umieszczania, ale niektóre są bardziej skomplikowane.</span><span class="sxs-lookup"><span data-stu-id="10577-116">Most of hello following controls could be configured via node properties and placement constraints, but some are more complicated.</span></span> <span data-ttu-id="10577-117">rzeczy toomake prostszy, hello zasobu klastra sieci szkieletowej programu Service Manager zawiera zasady te dodatkowe umieszczania.</span><span class="sxs-lookup"><span data-stu-id="10577-117">toomake things simpler, hello Service Fabric Cluster Resource Manager provides these additional placement policies.</span></span> <span data-ttu-id="10577-118">Zasady umieszczania są konfigurowane na podstawie wystąpienia na nazwę usługi.</span><span class="sxs-lookup"><span data-stu-id="10577-118">Placement policies are configured on a per-named service instance basis.</span></span> <span data-ttu-id="10577-119">Mogą być aktualizowane również dynamicznie.</span><span class="sxs-lookup"><span data-stu-id="10577-119">They can also be updated dynamically.</span></span>

## <a name="specifying-invalid-domains"></a><span data-ttu-id="10577-120">Określanie domen nieprawidłowy</span><span class="sxs-lookup"><span data-stu-id="10577-120">Specifying invalid domains</span></span>
<span data-ttu-id="10577-121">Witaj **InvalidDomain** zasady rozmieszczania umożliwia toospecify że określonej domeny błędów jest nieprawidłowa dla określonej usługi.</span><span class="sxs-lookup"><span data-stu-id="10577-121">hello **InvalidDomain** placement policy allows you toospecify that a particular Fault Domain is invalid for a specific service.</span></span> <span data-ttu-id="10577-122">Ta zasada zapewnia, że określonej usługi nigdy nie uruchamia się w określonym obszarze, na przykład z powodów polityki geograficznymi lub firmowych.</span><span class="sxs-lookup"><span data-stu-id="10577-122">This policy ensures that a particular service never runs in a particular area, for example for geopolitical or corporate policy reasons.</span></span> <span data-ttu-id="10577-123">Przy użyciu oddzielnych zasad można określić wielu domen nieprawidłowy.</span><span class="sxs-lookup"><span data-stu-id="10577-123">Multiple invalid domains may be specified via separate policies.</span></span>

<span data-ttu-id="10577-124"><center>
![Nieprawidłowa domena przykład][Image1]
</center></span><span class="sxs-lookup"><span data-stu-id="10577-124"><center>
![Invalid Domain Example][Image1]
</center></span></span>

<span data-ttu-id="10577-125">Kod:</span><span class="sxs-lookup"><span data-stu-id="10577-125">Code:</span></span>

```csharp
ServicePlacementInvalidDomainPolicyDescription invalidDomain = new ServicePlacementInvalidDomainPolicyDescription();
invalidDomain.DomainName = "fd:/DCEast"; //regulations prohibit this workload here
serviceDescription.PlacementPolicies.Add(invalidDomain);
```

<span data-ttu-id="10577-126">Środowiska PowerShell:</span><span class="sxs-lookup"><span data-stu-id="10577-126">Powershell:</span></span>

```posh
New-ServiceFabricService -ApplicationName $applicationName -ServiceName $serviceName -ServiceTypeName $serviceTypeName –Stateful -MinReplicaSetSize 3 -TargetReplicaSetSize 3 -PartitionSchemeSingleton -PlacementPolicy @("InvalidDomain,fd:/DCEast”)
```
## <a name="specifying-required-domains"></a><span data-ttu-id="10577-127">Określanie wymaganego domen</span><span class="sxs-lookup"><span data-stu-id="10577-127">Specifying required domains</span></span>
<span data-ttu-id="10577-128">Witaj wymagane zasady rozmieszczania domeny wymaga, aby usługa hello występuje tylko w określonej domenie hello.</span><span class="sxs-lookup"><span data-stu-id="10577-128">hello required domain placement policy requires that hello service is present only in hello specified domain.</span></span> <span data-ttu-id="10577-129">Przy użyciu oddzielnych zasad można określić wielu domen wymagana.</span><span class="sxs-lookup"><span data-stu-id="10577-129">Multiple required domains can be specified via separate policies.</span></span>

<span data-ttu-id="10577-130"><center>
![Przykład wymaganej domeny][Image2]
</center></span><span class="sxs-lookup"><span data-stu-id="10577-130"><center>
![Required Domain Example][Image2]
</center></span></span>

<span data-ttu-id="10577-131">Kod:</span><span class="sxs-lookup"><span data-stu-id="10577-131">Code:</span></span>

```csharp
ServicePlacementRequiredDomainPolicyDescription requiredDomain = new ServicePlacementRequiredDomainPolicyDescription();
requiredDomain.DomainName = "fd:/DC01/RK03/BL2";
serviceDescription.PlacementPolicies.Add(requiredDomain);
```

<span data-ttu-id="10577-132">Środowiska PowerShell:</span><span class="sxs-lookup"><span data-stu-id="10577-132">Powershell:</span></span>

```posh
New-ServiceFabricService -ApplicationName $applicationName -ServiceName $serviceName -ServiceTypeName $serviceTypeName –Stateful -MinReplicaSetSize 3 -TargetReplicaSetSize 3 -PartitionSchemeSingleton -PlacementPolicy @("RequiredDomain,fd:/DC01/RK03/BL2")
```

## <a name="specifying-a-preferred-domain-for-hello-primary-replicas-of-a-stateful-service"></a><span data-ttu-id="10577-133">Określanie preferowanych domeny dla repliki podstawowej hello usługi stanowej</span><span class="sxs-lookup"><span data-stu-id="10577-133">Specifying a preferred domain for hello primary replicas of a stateful service</span></span>
<span data-ttu-id="10577-134">Hello preferowane domena podstawowa określa tooplace domeny błędów hello hello Primary in.</span><span class="sxs-lookup"><span data-stu-id="10577-134">hello Preferred Primary Domain specifies hello fault domain tooplace hello Primary in.</span></span> <span data-ttu-id="10577-135">Witaj podstawowy kończy się w tej domenie, gdy wszystko jest w dobrej kondycji.</span><span class="sxs-lookup"><span data-stu-id="10577-135">hello Primary ends up in this domain when everything is healthy.</span></span> <span data-ttu-id="10577-136">Jeśli hello domeny lub replika podstawowa hello nie powiedzie się lub kończy pracę, hello podstawowy przenosi toosome innych lokalizacji, najlepiej na powitania tej samej domenie.</span><span class="sxs-lookup"><span data-stu-id="10577-136">If hello domain or hello Primary replica fails or shuts down, hello Primary moves toosome other location, ideally in hello same domain.</span></span> <span data-ttu-id="10577-137">Jeśli to nowa lokalizacja nie jest w domenie preferowanych hello, hello Menedżera zasobów klastra przenosi kopii toohello preferowanych domen tak szybko, jak to możliwe.</span><span class="sxs-lookup"><span data-stu-id="10577-137">If this new location isn't in hello preferred domain, hello Cluster Resource Manager moves it back toohello preferred domain as soon as possible.</span></span> <span data-ttu-id="10577-138">Oczywiście to ustawienie ma sens tylko dla stanowych usług.</span><span class="sxs-lookup"><span data-stu-id="10577-138">Naturally this setting only makes sense for stateful services.</span></span> <span data-ttu-id="10577-139">Ta zasada jest najbardziej przydatna w klastrach, które są łączone w regionach platformy Azure lub wiele centrów danych, ale ma usług, które preferowane umieszczania w określonej lokalizacji.</span><span class="sxs-lookup"><span data-stu-id="10577-139">This policy is most useful in clusters that are spanned across Azure regions or multiple datacenters but have services that prefer placement in a certain location.</span></span> <span data-ttu-id="10577-140">Utrzymywanie kolory podstawowe Zamknij tootheir użytkowników lub innych usług, które pomaga zapewnić mniejsze opóźnienia, zwłaszcza w przypadku odczytów, które są obsługiwane przez kolory podstawowe domyślnie.</span><span class="sxs-lookup"><span data-stu-id="10577-140">Keeping Primaries close tootheir users or other services helps provide lower latency, especially for reads, which are handled by Primaries by default.</span></span>

<span data-ttu-id="10577-141"><center>
![Wykorzystanie preferowanych domen podstawowe i pracy awaryjnej][Image3]
</center></span><span class="sxs-lookup"><span data-stu-id="10577-141"><center>
![Preferred Primary Domains and Failover][Image3]
</center></span></span>

```csharp
ServicePlacementPreferPrimaryDomainPolicyDescription primaryDomain = new ServicePlacementPreferPrimaryDomainPolicyDescription();
primaryDomain.DomainName = "fd:/EastUS/";
serviceDescription.PlacementPolicies.Add(invalidDomain);
```

<span data-ttu-id="10577-142">Środowiska PowerShell:</span><span class="sxs-lookup"><span data-stu-id="10577-142">Powershell:</span></span>

```posh
New-ServiceFabricService -ApplicationName $applicationName -ServiceName $serviceName -ServiceTypeName $serviceTypeName –Stateful -MinReplicaSetSize 3 -TargetReplicaSetSize 3 -PartitionSchemeSingleton -PlacementPolicy @("PreferredPrimaryDomain,fd:/EastUS")
```

## <a name="requiring-replica-distribution-and-disallowing-packing"></a><span data-ttu-id="10577-143">Wymaganie dystrybucji repliki i brak zezwolenia pakowania</span><span class="sxs-lookup"><span data-stu-id="10577-143">Requiring replica distribution and disallowing packing</span></span>
<span data-ttu-id="10577-144">Repliki są _zwykle_ rozproszonych w domenach awarii i uaktualniania, gdy hello klastra jest w dobrej kondycji.</span><span class="sxs-lookup"><span data-stu-id="10577-144">Replicas are _normally_ distributed across fault and upgrade domains when hello cluster is healthy.</span></span> <span data-ttu-id="10577-145">Istnieją jednak przypadki, w których może mieć więcej niż jednej repliki dla danej partycji tymczasowo spakowana do jednej domeny.</span><span class="sxs-lookup"><span data-stu-id="10577-145">However, there are cases where more than one replica for a given partition may end up temporarily packed into a single domain.</span></span> <span data-ttu-id="10577-146">Na przykład, załóżmy, że ten klaster hello ma dziewięć węzłów w trzech domen błędów, fd: / 0, fd: / 1 i fd: / 2.</span><span class="sxs-lookup"><span data-stu-id="10577-146">For example, let's say that hello cluster has nine nodes in three fault domains, fd:/0, fd:/1, and fd:/2.</span></span> <span data-ttu-id="10577-147">Również Załóżmy, że usługa ma trzy repliki.</span><span class="sxs-lookup"><span data-stu-id="10577-147">Let's also say that your service has three replicas.</span></span> <span data-ttu-id="10577-148">Załóżmy, że hello węzłów, które były używane przez te repliki w fd: / 1 i fd: / 2 zakończył działanie.</span><span class="sxs-lookup"><span data-stu-id="10577-148">Let's say that hello nodes that were being used for those replicas in fd:/1 and fd:/2 went down.</span></span> <span data-ttu-id="10577-149">Zwykle hello Menedżera zasobów klastra wolisz inne węzły w tych samym domen błędów.</span><span class="sxs-lookup"><span data-stu-id="10577-149">Normally hello Cluster Resource Manager would prefer other nodes in those same fault domains.</span></span> <span data-ttu-id="10577-150">W takim przypadku Załóżmy, że ze względu na problemy toocapacity żadna z hello były ważne inne węzły w tych domenach.</span><span class="sxs-lookup"><span data-stu-id="10577-150">In this case, let's say due toocapacity issues none of hello other nodes in those domains were valid.</span></span> <span data-ttu-id="10577-151">Jeśli hello Menedżera zasobów klastra kompilacje zastępujące tych replik, miałoby toochoose węzłów w fd: / 0.</span><span class="sxs-lookup"><span data-stu-id="10577-151">If hello Cluster Resource Manager builds replacements for those replicas, it would have toochoose nodes in fd:/0.</span></span> <span data-ttu-id="10577-152">Jednak podczas _który_ tworzy sytuacji, gdy jest naruszone hello ograniczenia domeny błędów.</span><span class="sxs-lookup"><span data-stu-id="10577-152">However, doing _that_ creates a situation where hello Fault Domain constraint is violated.</span></span> <span data-ttu-id="10577-153">Pakowanie zwiększa replik hello ryzyko, że hello zestawu replik całego można wyłączenia lub zostać utracone.</span><span class="sxs-lookup"><span data-stu-id="10577-153">Packing replicas increases hello chance that hello whole replica set could go down or be lost.</span></span> 

> [!NOTE]
> <span data-ttu-id="10577-154">Aby uzyskać więcej informacji na temat ograniczeń oraz ograniczenia, priorytetów ogólnie rzecz biorąc, zapoznaj się z [w tym temacie](service-fabric-cluster-resource-manager-management-integration.md#constraint-priorities).</span><span class="sxs-lookup"><span data-stu-id="10577-154">For more information on constraints and constraint priorities generally, check out [this topic](service-fabric-cluster-resource-manager-management-integration.md#constraint-priorities).</span></span>
>

<span data-ttu-id="10577-155">Jeśli kiedykolwiek w tym samouczku komunikat kondycji takich jak "`hello Load Balancer has detected a Constraint Violation for this Replica:fabric:/<some service name> Secondary Partition <some partition ID> is violating hello Constraint: FaultDomain`", a następnie został trafiony tego warunku lub przypominać go.</span><span class="sxs-lookup"><span data-stu-id="10577-155">If you've ever seen a health message such as "`hello Load Balancer has detected a Constraint Violation for this Replica:fabric:/<some service name> Secondary Partition <some partition ID> is violating hello Constraint: FaultDomain`", then you've hit this condition or something like it.</span></span> <span data-ttu-id="10577-156">Zwykle tylko jedną lub dwie repliki są pakowane tymczasowo.</span><span class="sxs-lookup"><span data-stu-id="10577-156">Usually only one or two replicas are packed together temporarily.</span></span> <span data-ttu-id="10577-157">Tak długo, jak są mniej niż kworum replik w danej domenie, możesz bezpieczne.</span><span class="sxs-lookup"><span data-stu-id="10577-157">So long as there are fewer than a quorum of replicas in a given domain, you're safe.</span></span> <span data-ttu-id="10577-158">Opakowanie jest rzadko, jednak może się zdarzyć, oraz zwykle tych sytuacji przejściowej ponieważ węzłów hello wrócić.</span><span class="sxs-lookup"><span data-stu-id="10577-158">Packing is rare, but it can happen, and usually these situations are transient since hello nodes come back.</span></span> <span data-ttu-id="10577-159">Jeśli węzły hello pozostać w dół i hello Menedżera zasobów klastra musi zamiany toobuild, zazwyczaj dostępne są inne węzły w domenach awarii idealne hello.</span><span class="sxs-lookup"><span data-stu-id="10577-159">If hello nodes do stay down and hello Cluster Resource Manager needs toobuild replacements, usually there are other nodes available in hello ideal fault domains.</span></span>

<span data-ttu-id="10577-160">Niektórych obciążeń wolisz zawsze używania hello docelowej liczby replik, nawet jeśli ich są pakować do mniejszej liczby domen.</span><span class="sxs-lookup"><span data-stu-id="10577-160">Some workloads would prefer always having hello target number of replicas, even if they are packed into fewer domains.</span></span> <span data-ttu-id="10577-161">Te obciążenia są stawiając przed awariami całkowita liczba jednoczesnych domeny stałe i zwykle można odzyskać stanu lokalnego.</span><span class="sxs-lookup"><span data-stu-id="10577-161">These workloads are betting against total simultaneous permanent domain failures and can usually recover local state.</span></span> <span data-ttu-id="10577-162">Innych obciążeń raczej wymagałoby wcześniejszej niż poprawności ryzyko lub utraty danych hello przestoju.</span><span class="sxs-lookup"><span data-stu-id="10577-162">Other workloads would rather take hello downtime earlier than risk correctness or loss of data.</span></span> <span data-ttu-id="10577-163">Uruchom większości obciążeń produkcyjnych z więcej niż trzy repliki, więcej niż trzy domen błędów i wiele węzłów prawidłowy na domeny błędów.</span><span class="sxs-lookup"><span data-stu-id="10577-163">Most production workloads run with more than three replicas, more than three fault domains, and many valid nodes per fault domain.</span></span> <span data-ttu-id="10577-164">W związku z tym hello domyślne zachowanie umożliwia pakowania domeny domyślnie.</span><span class="sxs-lookup"><span data-stu-id="10577-164">Because of this, hello default behavior allows domain packing by default.</span></span> <span data-ttu-id="10577-165">Hello domyślne zachowanie umożliwia równoważenia normalnym i pracy awaryjnej toohandle te ekstremalnych przypadkach, nawet w przypadku oznacza to, że tymczasowe domeny pakowania.</span><span class="sxs-lookup"><span data-stu-id="10577-165">hello default behavior allows normal balancing and failover toohandle these extreme cases, even if that means temporary domain packing.</span></span>

<span data-ttu-id="10577-166">Jeśli chcesz toodisable takie pakowania dla danego obciążenia, można określić hello `RequireDomainDistribution` zasad w usłudze hello.</span><span class="sxs-lookup"><span data-stu-id="10577-166">If you want toodisable such packing for a given workload, you can specify hello `RequireDomainDistribution` policy on hello service.</span></span> <span data-ttu-id="10577-167">Gdy ta zasada jest ustawiona, hello Cluster Resource Manager zapewnia nie dwóch replik z hello uruchamiania tej samej partycji w hello tej samej usterki lub domena uaktualnienia.</span><span class="sxs-lookup"><span data-stu-id="10577-167">When this policy is set, hello Cluster Resource Manager ensures no two replicas from hello same partition run in hello same fault or upgrade domain.</span></span>

<span data-ttu-id="10577-168">Kod:</span><span class="sxs-lookup"><span data-stu-id="10577-168">Code:</span></span>

```csharp
ServicePlacementRequireDomainDistributionPolicyDescription distributeDomain = new ServicePlacementRequireDomainDistributionPolicyDescription();
serviceDescription.PlacementPolicies.Add(distributeDomain);
```

<span data-ttu-id="10577-169">Środowiska PowerShell:</span><span class="sxs-lookup"><span data-stu-id="10577-169">Powershell:</span></span>

```posh
New-ServiceFabricService -ApplicationName $applicationName -ServiceName $serviceName -ServiceTypeName $serviceTypeName –Stateful -MinReplicaSetSize 3 -TargetReplicaSetSize 3 -PartitionSchemeSingleton -PlacementPolicy @("RequiredDomainDistribution")
```

<span data-ttu-id="10577-170">Teraz, może on być możliwe toouse te konfiguracje dla usług w klastrze, który nie został geograficznie łączone?</span><span class="sxs-lookup"><span data-stu-id="10577-170">Now, would it be possible toouse these configurations for services in a cluster that was not geographically spanned?</span></span> <span data-ttu-id="10577-171">Użytkownik może, ale nie ma dużą Przyczyna zbyt.</span><span class="sxs-lookup"><span data-stu-id="10577-171">You could, but there’s not a great reason too.</span></span> <span data-ttu-id="10577-172">Witaj konfiguracjach wymaganych, nieprawidłowy i preferowanych domen należy unikać o ile nie wymagają hello scenariuszy.</span><span class="sxs-lookup"><span data-stu-id="10577-172">hello required, invalid, and preferred domain configurations should be avoided unless hello scenarios require them.</span></span> <span data-ttu-id="10577-173">Nie rozsądne żadnych tooforce tootry znaczeniu toorun danego obciążenia w jednej lub tooprefer niektórych segmentu klastra lokalnego zamiast innego.</span><span class="sxs-lookup"><span data-stu-id="10577-173">It doesn't make any sense tootry tooforce a given workload toorun in a single rack, or tooprefer some segment of your local cluster over another.</span></span> <span data-ttu-id="10577-174">Różne konfiguracje sprzętu należy rozłożyć na domenach awarii i obsługiwane za pośrednictwem ograniczenia umieszczania normalne i właściwości węzła.</span><span class="sxs-lookup"><span data-stu-id="10577-174">Different hardware configurations should be spread across fault domains and handled via normal placement constraints and node properties.</span></span>

## <a name="next-steps"></a><span data-ttu-id="10577-175">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="10577-175">Next steps</span></span>
- <span data-ttu-id="10577-176">Aby uzyskać więcej informacji na temat konfigurowania usługi [Dowiedz się więcej o konfigurowaniu usługi](service-fabric-cluster-resource-manager-configure-services.md)</span><span class="sxs-lookup"><span data-stu-id="10577-176">For more information on configuring services, [Learn about configuring Services](service-fabric-cluster-resource-manager-configure-services.md)</span></span>

[Image1]:./media/service-fabric-cluster-resource-manager-advanced-placement-rules-placement-policies/cluster-invalid-placement-domain.png
[Image2]:./media/service-fabric-cluster-resource-manager-advanced-placement-rules-placement-policies/cluster-required-placement-domain.png
[Image3]:./media/service-fabric-cluster-resource-manager-advanced-placement-rules-placement-policies/cluster-preferred-primary-domain.png
