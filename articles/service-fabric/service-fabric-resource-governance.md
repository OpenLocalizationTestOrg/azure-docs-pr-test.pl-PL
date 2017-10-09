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
# <a name="resource-governance"></a>Zarządzanie zasobów 

Uruchamianie wielu usług na hello tego samego węzła lub klastra, jest to możliwe, że jedna usługa może zużywać więcej zasobów, starving innych usług. Ten problem jest tooas określonego hello sąsiada naprawienie problemu. Sieć szkieletowa usług umożliwia hello developer toospecify zastrzeżenia i limity dla usługi tooguarantee zasobów i również ograniczenie jego użycia zasobów. 

## <a name="resource-governance-metrics"></a>Metryki ładu zasobów 

Zarządzanie zasobów jest obsługiwane w sieci szkieletowej usług na [pakiet usługi](service-fabric-application-model.md). Witaj zasobów, które są przypisane tooService pakietu można podzielić między pakiety kodu. limity zasobów Hello to także oznaczać rezerwacji hello hello zasobów. Określanie Procesora i pamięci na pakiet usługi, za pomocą dwóch wbudowanych obsługuje sieci szkieletowej usług [metryki](service-fabric-cluster-resource-manager-metrics.md):

* Procesor (Nazwa metryki `ServiceFabric:/_CpuCores`): podstawowa jest rdzenia logicznego, który jest dostępny na komputerze-hoście hello i wszystkie rdzenie obejmujące wszystkie węzły są ważone hello takie same.
* Pamięć (Nazwa metryki `ServiceFabric:/_MemoryInMB`): pamięci jest wyrażona w megabajtach i mapowania toophysical pamięci, która jest dostępna na komputerze hello.

Tylko gwarancje rezerwacji nietrwałego znajdują — środowisko uruchomieniowe hello odrzuca otwarcie nowej usługi, które zasoby dostępne pakiety zostaną przekroczone. Jednak innego pliku wykonywalnego lub kontener jest umieszczony w węźle hello, który może naruszyć gwarancje rezerwacji oryginalnego hello.

Dla tych dwóch metryki hello [Menedżera zasobów klastra](service-fabric-cluster-resource-manager-cluster-description.md) śledzi klastra całkowitej pojemności, hello obciążenia w każdym węźle klastra hello, i pozostałych zasobów w klastrze hello. Te dwie metryki są równoważne tooany innego użytkownika lub niestandardowa Metryka i wszystkie istniejące funkcje mogą być używane z nich:
* Klaster może być [zrównoważonym](service-fabric-cluster-resource-manager-balancing.md) zgodnie z toothese dwa metryki (domyślnie).
* Klaster może być [defragmentacji](service-fabric-cluster-resource-manager-defragmentation-metrics.md) zgodnie z toothese dwa metryki.
* Gdy [opisujące klastra](service-fabric-cluster-resource-manager-cluster-description.md), buforowane pojemności może być ustawiona dla tych dwóch metryk.

[Obciążenie dynamicznego raportowania](service-fabric-cluster-resource-manager-metrics.md) nie jest obsługiwana dla tych metryk i ładuje dla tych metryk są zdefiniowane w czasie tworzenia.

## <a name="cluster-set-up-for-enabling-resource-governance"></a>Klaster zestawu do włączania zarządzania zasobów

Pojemność w powinien być zdefiniowany ręcznie każdy typ węzła w klastrze hello w następujący sposób:

```xml
    <NodeType Name="MyNodeType">
      <Capacities>
        <Capacity Name="ServiceFabric:/_CpuCores" Value="4"/>
        <Capacity Name="ServiceFabric:/_MemoryInMB" Value="2048"/>
      </Capacities>
    </NodeType>
```
 
Ładu zasobów jest dozwolona tylko dla usługi użytkownika, a nie na żadnych usług systemu. Podczas określania pojemności, niektóre rdzeni i ilości pamięci musi być lewej nieprzydzielonego dla usług systemowych. Aby uzyskać optymalną wydajność powinien również włączony hello następujące ustawienie w manifeście klastra hello: 

```xml
<Section Name="PlacementAndLoadBalancing">
    <Parameter Name="PreventTransientOvercommit" Value="true" /> 
    <Parameter Name="AllowConstraintCheckFixesDuringApplicationUpgrade" Value="true" />
</Section>
```


## <a name="specifying-resource-governance"></a>Określanie ładu zasobów 

Limity ładu zasobu określa się w manifeście aplikacji hello (sekcja ServiceManifestImport), jak pokazano w hello poniższy przykład:

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
  
W tym przykładzie pakiet usługi ServicePackageA pobiera węzły hello, gdzie jest umieszczony jednego rdzenia. Ten pakiet usługi zawiera dwa pakiety kodu (CodeA1 i CodeA2), a jednocześnie określić hello `CpuShares` parametru. część Hello CpuShares 512:256 dzieli hello core między hello dwa pakiety kodu. W związku z tym w tym przykładzie CodeA1 pobiera dwóch podstawowych i CodeA2 pobiera jedna trzecia podstawowa (i zastrzeżenia gwarancji soft hello sam). W przypadku gdy CpuShares nie są określone dla pakietów kodu, usługi sieć szkieletowa dzieli rdzeni hello równomiernie między nimi.

Limity pamięci są bezwzględne, dlatego oba pakiety kodu są ograniczone too1024 MB pamięci (i elastyczne gwarancji zastrzeżenia hello sam). Pakiety kodu (kontenery lub procesów) nie są możliwe tooallocate, który więcej pamięci niż ten limit i podjęto toodo tak powoduje wygenerowanie wyjątku braku pamięci. Toowork wymuszania limit zasobów wszystkie pakiety kodu w ramach pakietu usługi powinny mieć określone limity pamięci.


## <a name="next-steps"></a>Następne kroki
* Przeczytaj toolearn więcej o klastra Menedżera zasobów, [artykułu](service-fabric-cluster-resource-manager-introduction.md).
* Przeczytaj toolearn więcej informacji na temat modelu aplikacji, pakietów usług, pakiety kodu i sposobu replik mapowania toothem [artykułu](service-fabric-application-model.md).
