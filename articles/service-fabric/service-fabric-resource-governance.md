---
title: "Ładu zasobów sieci szkieletowej usług Azure kontenery i usług | Dokumentacja firmy Microsoft"
description: "Sieć szkieletowa usług Azure można określić limity zasobów dla usług uruchomionych wewnątrz lub na zewnątrz kontenerów."
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
ms.openlocfilehash: 88d44953ad83f9e7401fd087a39842e4a3790124
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/18/2017
---
# <a name="resource-governance"></a>Zarządzanie zasobów 

Uruchamiając wiele usług na tym samym węźle lub klastra, jest to możliwe, że jedna usługa może zużywać więcej zasobów, starving innych usług. Ten problem jest określana jako sąsiada naprawienie problemu. Sieć szkieletowa usług umożliwia deweloperowi Określ zastrzeżenia i limity dla danej usługi, aby zagwarantować zasobów, a także ograniczenie jego użycia zasobów. 

## <a name="resource-governance-metrics"></a>Metryki ładu zasobów 

Zarządzanie zasobów jest obsługiwane w sieci szkieletowej usług na [pakiet usługi](service-fabric-application-model.md). Zasoby, które są przypisane do pakietu usług można podzielić między pakiety kodu. Określone limity zasobów to także oznaczać rezerwacji zasobów. Określanie Procesora i pamięci na pakiet usługi, za pomocą dwóch wbudowanych obsługuje sieci szkieletowej usług [metryki](service-fabric-cluster-resource-manager-metrics.md):

* Procesor (Nazwa metryki `ServiceFabric:/_CpuCores`): podstawowa jest rdzenia logicznego, który jest dostępny na komputerze-hoście, a wszystkie rdzenie obejmujące wszystkie węzły są ważone takie same.
* Pamięć (Nazwa metryki `ServiceFabric:/_MemoryInMB`): pamięci jest wyrażona w megabajtach i mapowania pamięci fizycznej, która jest dostępna na komputerze.

Tylko gwarancje rezerwacji nietrwałego znajdują — środowisko uruchomieniowe odrzuca otwierania nowe pakiety usługi, które są przekracza dostępne zasoby. Jednak innego pliku wykonywalnego lub kontener jest umieszczony na węźle, który może naruszyć oryginalnego gwarancje rezerwacji.

Dla tych dwóch metryki [Menedżera zasobów klastra](service-fabric-cluster-resource-manager-cluster-description.md) śledzi klastra całkowita pojemność, obciążenia na każdym węźle klastra, i, w pozostałych zasobów w klastrze. Te dwie metryki są równoważne innego użytkownika lub niestandardowa Metryka i wszystkie istniejące funkcje mogą być używane z nich:
* Klaster może być [zrównoważonym](service-fabric-cluster-resource-manager-balancing.md) zgodnie z tych dwóch metryk (domyślnie).
* Klaster może być [defragmentacji](service-fabric-cluster-resource-manager-defragmentation-metrics.md) zgodnie z tych dwóch metryk.
* Gdy [opisujące klastra](service-fabric-cluster-resource-manager-cluster-description.md), buforowane pojemności może być ustawiona dla tych dwóch metryk.

[Obciążenie dynamicznego raportowania](service-fabric-cluster-resource-manager-metrics.md) nie jest obsługiwana dla tych metryk i ładuje dla tych metryk są zdefiniowane w czasie tworzenia.

## <a name="cluster-set-up-for-enabling-resource-governance"></a>Klaster zestawu do włączania zarządzania zasobów

Pojemność w powinien być zdefiniowany ręcznie każdy typ węzła w klastrze w następujący sposób:

```xml
    <NodeType Name="MyNodeType">
      <Capacities>
        <Capacity Name="ServiceFabric:/_CpuCores" Value="4"/>
        <Capacity Name="ServiceFabric:/_MemoryInMB" Value="2048"/>
      </Capacities>
    </NodeType>
```
 
Ładu zasobów jest dozwolona tylko dla usługi użytkownika, a nie na żadnych usług systemu. Podczas określania pojemności, niektóre rdzeni i ilości pamięci musi być lewej nieprzydzielonego dla usług systemowych. Aby uzyskać optymalną wydajność należy również włączone następujące ustawienie w manifeście klastra: 

```xml
<Section Name="PlacementAndLoadBalancing">
    <Parameter Name="PreventTransientOvercommit" Value="true" /> 
    <Parameter Name="AllowConstraintCheckFixesDuringApplicationUpgrade" Value="true" />
</Section>
```


## <a name="specifying-resource-governance"></a>Określanie ładu zasobów 

Limity ładu zasobów są określone w manifeście aplikacji (sekcja ServiceManifestImport), jak pokazano w poniższym przykładzie:

```xml
<?xml version='1.0' encoding='UTF-8'?>
<ApplicationManifest ApplicationTypeName='TestAppTC1' ApplicationTypeVersion='vTC1' xsi:schemaLocation='http://schemas.microsoft.com/2011/01/fabric ServiceFabricServiceModel.xsd' xmlns='http://schemas.microsoft.com/2011/01/fabric' xmlns:xsi='http://www.w3.org/2001/XMLSchema-instance'>
  <Parameters>
  </Parameters>
  <!--
  ServicePackageA has the number of CPU cores defined, but doesn't have the MemoryInMB defined.
  In this case, Service Fabric will sum the limits on code packages and uses the sum as 
  the overall ServicePackage limit.
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
  
W tym przykładzie pakiet usługi ServicePackageA pobiera jeden rdzeń w węzłach, na której jest umieszczona. Ten pakiet usługi zawiera dwa pakiety kodu (CodeA1 i CodeA2), a jednocześnie określić `CpuShares` parametru. Część CpuShares 512:256 dzieli podstawowe w pakietach dwóch kodu. W związku z tym w tym przykładzie CodeA1 pobiera dwóch podstawowa i CodeA2 pobiera jedna trzecia podstawowa (i zastrzeżenie gwarancji soft tego samego). W przypadku gdy CpuShares nie są określone dla pakietów kodu, Service Fabric dzieli rdzeni równomiernie między nimi.

Limity pamięci są bezwzględne, oba pakiety kodu są ograniczone do 1024 MB pamięci (i zastrzeżenie gwarancji soft tego samego). Pakiety kodu (kontenery lub procesy) nie mogą przydzielać pamięci ponad ten limit. Podjęcie próby takiego przydzielenia spowoduje wyjątek braku pamięci. Aby wymuszanie limitu zasobów działało, wszystkie pakiety kodu w ramach pakietu usług powinny mieć określone limity pamięci.


## <a name="next-steps"></a>Następne kroki
* Aby dowiedzieć się więcej na temat Menedżera zasobów klastra, przeczytaj to [artykułu](service-fabric-cluster-resource-manager-introduction.md).
* Aby dowiedzieć się więcej na temat modelu aplikacji, pakietów usług, pakiety kodu oraz sposobu mapowania ich repliki do odczytu to [artykułu](service-fabric-application-model.md).
