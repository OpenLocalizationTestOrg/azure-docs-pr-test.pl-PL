---
title: "aaaAzure ładu zasobów sieci szkieletowej usług dla usług i kontenery | Dokumentacja firmy Microsoft"
description: "Sieć szkieletowa usług Azure umożliwia toospecify zasobów limity dla usług uruchomionych wewnątrz lub na zewnątrz kontenerów."
services: service-fabric
documentationcenter: .net
author: mani-ramaswamy
manager: timlt
editor: 
ms.assetid: ab49c4b9-74a8-4907-b75b-8d2ee84c6d90
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 8/9/2017
ms.author: subramar
ms.openlocfilehash: 34e368211d98ff6b5b294c9c8b3af5ca30eeb20c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="resource-governance"></a><span data-ttu-id="784ee-103">Zarządzanie zasobów</span><span class="sxs-lookup"><span data-stu-id="784ee-103">Resource governance</span></span> 

<span data-ttu-id="784ee-104">Uruchamianie wielu usług na hello tego samego węzła lub klastra, jest to możliwe, że jedna usługa może zużywać więcej zasobów, starving innych usług.</span><span class="sxs-lookup"><span data-stu-id="784ee-104">When running multiple services on hello same node or cluster, it is possible that one service might consume more resources starving other services.</span></span> <span data-ttu-id="784ee-105">Ten problem jest tooas określonego hello sąsiada naprawienie problemu.</span><span class="sxs-lookup"><span data-stu-id="784ee-105">This problem is referred tooas hello noisy-neighbor problem.</span></span> <span data-ttu-id="784ee-106">Sieć szkieletowa usług umożliwia hello developer toospecify zastrzeżenia i limity dla usługi tooguarantee zasobów i również ograniczenie jego użycia zasobów.</span><span class="sxs-lookup"><span data-stu-id="784ee-106">Service Fabric allows hello developer toospecify reservations and limits per service tooguarantee resources and also limit its resource usage.</span></span> 

## <a name="resource-governance-metrics"></a><span data-ttu-id="784ee-107">Metryki ładu zasobów</span><span class="sxs-lookup"><span data-stu-id="784ee-107">Resource governance metrics</span></span> 

<span data-ttu-id="784ee-108">Zarządzanie zasobów jest obsługiwane w sieci szkieletowej usług na [pakiet usługi](service-fabric-application-model.md).</span><span class="sxs-lookup"><span data-stu-id="784ee-108">Resource governance is supported in Service Fabric per [Service Package](service-fabric-application-model.md).</span></span> <span data-ttu-id="784ee-109">Witaj zasobów, które są przypisane tooService pakietu można podzielić między pakiety kodu.</span><span class="sxs-lookup"><span data-stu-id="784ee-109">hello resources that are assigned tooService Package can be further divided between code packages.</span></span> <span data-ttu-id="784ee-110">limity zasobów Hello to także oznaczać rezerwacji hello hello zasobów.</span><span class="sxs-lookup"><span data-stu-id="784ee-110">hello resource limits specified also mean hello reservation of hello resources.</span></span> <span data-ttu-id="784ee-111">Określanie Procesora i pamięci na pakiet usługi, za pomocą dwóch wbudowanych obsługuje sieci szkieletowej usług [metryki](service-fabric-cluster-resource-manager-metrics.md):</span><span class="sxs-lookup"><span data-stu-id="784ee-111">Service Fabric supports specifying CPU and Memory per service package, using two built-in [metrics](service-fabric-cluster-resource-manager-metrics.md):</span></span>

* <span data-ttu-id="784ee-112">Procesor (Nazwa metryki `ServiceFabric:/_CpuCores`): podstawowa jest rdzenia logicznego, który jest dostępny na komputerze-hoście hello i wszystkie rdzenie obejmujące wszystkie węzły są ważone hello takie same.</span><span class="sxs-lookup"><span data-stu-id="784ee-112">CPU (metric name `ServiceFabric:/_CpuCores`): A core is a logical core that is available on hello host machine, and all cores across all nodes are weighted hello same.</span></span>
* <span data-ttu-id="784ee-113">Pamięć (Nazwa metryki `ServiceFabric:/_MemoryInMB`): pamięci jest wyrażona w megabajtach i mapowania toophysical pamięci, która jest dostępna na komputerze hello.</span><span class="sxs-lookup"><span data-stu-id="784ee-113">Memory (metric name `ServiceFabric:/_MemoryInMB`): Memory is expressed in megabytes, and it maps toophysical memory that is available on hello machine.</span></span>

<span data-ttu-id="784ee-114">Tylko gwarancje rezerwacji nietrwałego znajdują — środowisko uruchomieniowe hello odrzuca otwarcie nowej usługi, które zasoby dostępne pakiety zostaną przekroczone.</span><span class="sxs-lookup"><span data-stu-id="784ee-114">Only soft reservation guarantees are provided - hello runtime rejects opening of new service packages available resources are exceeded.</span></span> <span data-ttu-id="784ee-115">Jednak innego pliku wykonywalnego lub kontener jest umieszczony w węźle hello, który może naruszyć gwarancje rezerwacji oryginalnego hello.</span><span class="sxs-lookup"><span data-stu-id="784ee-115">However, if another executable or container is placed on hello node, that may violate hello original reservation guarantees.</span></span>

<span data-ttu-id="784ee-116">Dla tych dwóch metryki hello [Menedżera zasobów klastra](service-fabric-cluster-resource-manager-cluster-description.md) śledzi klastra całkowitej pojemności, hello obciążenia w każdym węźle klastra hello, i pozostałych zasobów w klastrze hello.</span><span class="sxs-lookup"><span data-stu-id="784ee-116">For these two metrics, hello [Cluster Resource Manager](service-fabric-cluster-resource-manager-cluster-description.md) tracks total cluster capacity, hello load on each node in hello cluster, and, remaining resources in hello cluster.</span></span> <span data-ttu-id="784ee-117">Te dwie metryki są równoważne tooany innego użytkownika lub niestandardowa Metryka i wszystkie istniejące funkcje mogą być używane z nich:</span><span class="sxs-lookup"><span data-stu-id="784ee-117">These two metrics are equivalent tooany other user or custom metric and all existing features can be used with them:</span></span>
* <span data-ttu-id="784ee-118">Klaster może być [zrównoważonym](service-fabric-cluster-resource-manager-balancing.md) zgodnie z toothese dwa metryki (domyślnie).</span><span class="sxs-lookup"><span data-stu-id="784ee-118">Cluster can be [balanced](service-fabric-cluster-resource-manager-balancing.md) according toothese two metrics (default behavior).</span></span>
* <span data-ttu-id="784ee-119">Klaster może być [defragmentacji](service-fabric-cluster-resource-manager-defragmentation-metrics.md) zgodnie z toothese dwa metryki.</span><span class="sxs-lookup"><span data-stu-id="784ee-119">Cluster can be [defragmented](service-fabric-cluster-resource-manager-defragmentation-metrics.md) according toothese two metrics.</span></span>
* <span data-ttu-id="784ee-120">Gdy [opisujące klastra](service-fabric-cluster-resource-manager-cluster-description.md), buforowane pojemności może być ustawiona dla tych dwóch metryk.</span><span class="sxs-lookup"><span data-stu-id="784ee-120">When [describing a cluster](service-fabric-cluster-resource-manager-cluster-description.md), buffered capacity can be set for these two metrics.</span></span>

<span data-ttu-id="784ee-121">[Obciążenie dynamicznego raportowania](service-fabric-cluster-resource-manager-metrics.md) nie jest obsługiwana dla tych metryk i ładuje dla tych metryk są zdefiniowane w czasie tworzenia.</span><span class="sxs-lookup"><span data-stu-id="784ee-121">[Dynamic load reporting](service-fabric-cluster-resource-manager-metrics.md) is not supported for these metrics, and loads for these metrics are defined at creation time.</span></span>

## <a name="cluster-set-up-for-enabling-resource-governance"></a><span data-ttu-id="784ee-122">Klaster zestawu do włączania zarządzania zasobów</span><span class="sxs-lookup"><span data-stu-id="784ee-122">Cluster set up for enabling resource governance</span></span>

<span data-ttu-id="784ee-123">Pojemność w powinien być zdefiniowany ręcznie każdy typ węzła w klastrze hello w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="784ee-123">Capacity should be defined manually in each node type in hello cluster as follows:</span></span>

```xml
    <NodeType Name="MyNodeType">
      <Capacities>
        <Capacity Name="ServiceFabric:/_CpuCores" Value="4"/>
        <Capacity Name="ServiceFabric:/_MemoryInMB" Value="2048"/>
      </Capacities>
    </NodeType>
```
 
<span data-ttu-id="784ee-124">Ładu zasobów jest dozwolona tylko dla usługi użytkownika, a nie na żadnych usług systemu.</span><span class="sxs-lookup"><span data-stu-id="784ee-124">Resource governance is allowed only on user services and not on any system services.</span></span> <span data-ttu-id="784ee-125">Podczas określania pojemności, niektóre rdzeni i ilości pamięci musi być lewej nieprzydzielonego dla usług systemowych.</span><span class="sxs-lookup"><span data-stu-id="784ee-125">When specifying capacity, some cores and memory must be left unallocated for system services.</span></span> <span data-ttu-id="784ee-126">Aby uzyskać optymalną wydajność powinien również włączony hello następujące ustawienie w manifeście klastra hello:</span><span class="sxs-lookup"><span data-stu-id="784ee-126">For optimal performance, hello following setting should also be turned on in hello cluster manifest:</span></span> 

```xml
<Section Name="PlacementAndLoadBalancing">
    <Parameter Name="PreventTransientOvercommit" Value="true" /> 
    <Parameter Name="AllowConstraintCheckFixesDuringApplicationUpgrade" Value="true" />
</Section>
```


## <a name="specifying-resource-governance"></a><span data-ttu-id="784ee-127">Określanie ładu zasobów</span><span class="sxs-lookup"><span data-stu-id="784ee-127">Specifying resource governance</span></span> 

<span data-ttu-id="784ee-128">Limity ładu zasobu określa się w manifeście aplikacji hello (sekcja ServiceManifestImport), jak pokazano w hello poniższy przykład:</span><span class="sxs-lookup"><span data-stu-id="784ee-128">Resource governance limits are specified in hello application manifest (ServiceManifestImport section) as shown in hello following example:</span></span>

```xml
<?xml version='1.0' encoding='UTF-8'?>
<ApplicationManifest ApplicationTypeName='TestAppTC1' ApplicationTypeVersion='vTC1' xsi:schemaLocation='http://schemas.microsoft.com/2011/01/fabric ServiceFabricServiceModel.xsd' xmlns='http://schemas.microsoft.com/2011/01/fabric' xmlns:xsi='http://www.w3.org/2001/XMLSchema-instance'>
  <Parameters>
  </Parameters>
  <!--
  ServicePackageA has hello number of CPU cores defined, but doesn't have hello MemoryInMB defined.
  In this case, Service Fabric will sum hello limits on code packages and uses hello sum as 
  hello overall ServicePackage limit.
  -->
  <ServiceManifestImport>
    <ServiceManifestRef ServiceManifestName='ServicePackageA' ServiceManifestVersion='v1'/>
    <Policies>
      <ServicePackageResourceGovernancePolicy CpuCores="1"/>
      <ResourceGovernancePolicy CodePackageRef="CodeA1" CpuShares="512" MemoryInMB="1000" />
      <ResourceGovernancePolicy CodePackageRef="CodeA2" CpuShares="256" MemoryInMB="1000" />
    </Policies>
  </ServiceManifestImport>
```
  
<span data-ttu-id="784ee-129">W tym przykładzie pakiet usługi ServicePackageA pobiera węzły hello, gdzie jest umieszczony jednego rdzenia.</span><span class="sxs-lookup"><span data-stu-id="784ee-129">In this example, service package ServicePackageA gets one core on hello nodes where it is placed.</span></span> <span data-ttu-id="784ee-130">Ten pakiet usługi zawiera dwa pakiety kodu (CodeA1 i CodeA2), a jednocześnie określić hello `CpuShares` parametru.</span><span class="sxs-lookup"><span data-stu-id="784ee-130">This service package contains two code packages (CodeA1 and CodeA2), and both specify hello `CpuShares` parameter.</span></span> <span data-ttu-id="784ee-131">część Hello CpuShares 512:256 dzieli hello core między hello dwa pakiety kodu.</span><span class="sxs-lookup"><span data-stu-id="784ee-131">hello proportion of CpuShares 512:256  divides hello core across hello two code packages.</span></span> <span data-ttu-id="784ee-132">W związku z tym w tym przykładzie CodeA1 pobiera dwóch podstawowych i CodeA2 pobiera jedna trzecia podstawowa (i zastrzeżenia gwarancji soft hello sam).</span><span class="sxs-lookup"><span data-stu-id="784ee-132">Thus, in this example, CodeA1 gets two-thirds of a core, and  CodeA2 gets one-third of a core (and a soft-guarantee reservation of hello same).</span></span> <span data-ttu-id="784ee-133">W przypadku gdy CpuShares nie są określone dla pakietów kodu, usługi sieć szkieletowa dzieli rdzeni hello równomiernie między nimi.</span><span class="sxs-lookup"><span data-stu-id="784ee-133">In case when CpuShares are not specified for code packages, Service Fabric divides hello cores equally among them.</span></span>

<span data-ttu-id="784ee-134">Limity pamięci są bezwzględne, dlatego oba pakiety kodu są ograniczone too1024 MB pamięci (i elastyczne gwarancji zastrzeżenia hello sam).</span><span class="sxs-lookup"><span data-stu-id="784ee-134">Memory limits are absolute, so both code packages are limited too1024 MB of memory (and a soft-guarantee reservation of hello same).</span></span> <span data-ttu-id="784ee-135">Pakiety kodu (kontenery lub procesów) nie są możliwe tooallocate, który więcej pamięci niż ten limit i podjęto toodo tak powoduje wygenerowanie wyjątku braku pamięci.</span><span class="sxs-lookup"><span data-stu-id="784ee-135">Code packages (containers or processes) are not able tooallocate more memory than this limit, and attempting toodo so results in an out-of-memory exception.</span></span> <span data-ttu-id="784ee-136">Toowork wymuszania limit zasobów wszystkie pakiety kodu w ramach pakietu usługi powinny mieć określone limity pamięci.</span><span class="sxs-lookup"><span data-stu-id="784ee-136">For resource limit enforcement toowork, all code packages within a service package should have memory limits specified.</span></span>


## <a name="next-steps"></a><span data-ttu-id="784ee-137">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="784ee-137">Next steps</span></span>
* <span data-ttu-id="784ee-138">Przeczytaj toolearn więcej o klastra Menedżera zasobów, [artykułu](service-fabric-cluster-resource-manager-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="784ee-138">toolearn more about Cluster Resource Manager, read this [article](service-fabric-cluster-resource-manager-introduction.md).</span></span>
* <span data-ttu-id="784ee-139">Przeczytaj toolearn więcej informacji na temat modelu aplikacji, pakietów usług, pakiety kodu i sposobu replik mapowania toothem [artykułu](service-fabric-application-model.md).</span><span class="sxs-lookup"><span data-stu-id="784ee-139">toolearn more about application model, service packages, code packages and how replicas map toothem read this [article](service-fabric-application-model.md).</span></span>
