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
# <a name="placement-policies-for-service-fabric-services"></a>Zasady umieszczania dla usługi sieci szkieletowej usług
Zasady umieszczania są dodatkowe reguły, które mogą być rozmieszczenie usługi toogovern używane w niektórych scenariuszach określone, typowe mniej. Przykłady takich scenariuszy to:

- Klaster usługi Service Fabric obejmuje odległości geograficznego, takich jak wiele lokalnych centrów danych lub w regionach platformy Azure
- Środowiska obejmuje wiele obszarów kontrolki geograficznymi lub prawnych lub innym przypadku, gdy masz zasada granic należy tooenforce
- Brak komunikacji wydajności lub opóźnień zagadnienia odległości toolarge lub użyj łączy sieciowych wolniejszych lub bardziej zawodne
- Należy tookeep dla określonych obciążeń rozmieszczony wspólnie jako starań, z innymi obciążeniami lub w sąsiedztwie toocustomers

Większość wymagań dostosowanie hello fizycznego układu hello klastra, reprezentowany jako hello domen błędów hello klastra. 

Witaj umieszczania zaawansowanych zasad, które wyjść naprzeciw te scenariusze są następujące:

1. Nieprawidłowy domen
2. Wymagane domen
3. Wykorzystanie preferowanych domen
4. Brak zezwolenia pakowania repliki

Większość powitania po formantów można skonfigurować za pomocą właściwości węzła i ograniczenia dotyczące umieszczania, ale niektóre są bardziej skomplikowane. rzeczy toomake prostszy, hello zasobu klastra sieci szkieletowej programu Service Manager zawiera zasady te dodatkowe umieszczania. Zasady umieszczania są konfigurowane na podstawie wystąpienia na nazwę usługi. Mogą być aktualizowane również dynamicznie.

## <a name="specifying-invalid-domains"></a>Określanie domen nieprawidłowy
Witaj **InvalidDomain** zasady rozmieszczania umożliwia toospecify że określonej domeny błędów jest nieprawidłowa dla określonej usługi. Ta zasada zapewnia, że określonej usługi nigdy nie uruchamia się w określonym obszarze, na przykład z powodów polityki geograficznymi lub firmowych. Przy użyciu oddzielnych zasad można określić wielu domen nieprawidłowy.

<center>
![Nieprawidłowa domena przykład][Image1]
</center>

Kod:

```csharp
ServicePlacementInvalidDomainPolicyDescription invalidDomain = new ServicePlacementInvalidDomainPolicyDescription();
invalidDomain.DomainName = "fd:/DCEast"; //regulations prohibit this workload here
serviceDescription.PlacementPolicies.Add(invalidDomain);
```

Środowiska PowerShell:

```posh
New-ServiceFabricService -ApplicationName $applicationName -ServiceName $serviceName -ServiceTypeName $serviceTypeName –Stateful -MinReplicaSetSize 3 -TargetReplicaSetSize 3 -PartitionSchemeSingleton -PlacementPolicy @("InvalidDomain,fd:/DCEast”)
```
## <a name="specifying-required-domains"></a>Określanie wymaganego domen
Witaj wymagane zasady rozmieszczania domeny wymaga, aby usługa hello występuje tylko w określonej domenie hello. Przy użyciu oddzielnych zasad można określić wielu domen wymagana.

<center>
![Przykład wymaganej domeny][Image2]
</center>

Kod:

```csharp
ServicePlacementRequiredDomainPolicyDescription requiredDomain = new ServicePlacementRequiredDomainPolicyDescription();
requiredDomain.DomainName = "fd:/DC01/RK03/BL2";
serviceDescription.PlacementPolicies.Add(requiredDomain);
```

Środowiska PowerShell:

```posh
New-ServiceFabricService -ApplicationName $applicationName -ServiceName $serviceName -ServiceTypeName $serviceTypeName –Stateful -MinReplicaSetSize 3 -TargetReplicaSetSize 3 -PartitionSchemeSingleton -PlacementPolicy @("RequiredDomain,fd:/DC01/RK03/BL2")
```

## <a name="specifying-a-preferred-domain-for-hello-primary-replicas-of-a-stateful-service"></a>Określanie preferowanych domeny dla repliki podstawowej hello usługi stanowej
Hello preferowane domena podstawowa określa tooplace domeny błędów hello hello Primary in. Witaj podstawowy kończy się w tej domenie, gdy wszystko jest w dobrej kondycji. Jeśli hello domeny lub replika podstawowa hello nie powiedzie się lub kończy pracę, hello podstawowy przenosi toosome innych lokalizacji, najlepiej na powitania tej samej domenie. Jeśli to nowa lokalizacja nie jest w domenie preferowanych hello, hello Menedżera zasobów klastra przenosi kopii toohello preferowanych domen tak szybko, jak to możliwe. Oczywiście to ustawienie ma sens tylko dla stanowych usług. Ta zasada jest najbardziej przydatna w klastrach, które są łączone w regionach platformy Azure lub wiele centrów danych, ale ma usług, które preferowane umieszczania w określonej lokalizacji. Utrzymywanie kolory podstawowe Zamknij tootheir użytkowników lub innych usług, które pomaga zapewnić mniejsze opóźnienia, zwłaszcza w przypadku odczytów, które są obsługiwane przez kolory podstawowe domyślnie.

<center>
![Wykorzystanie preferowanych domen podstawowe i pracy awaryjnej][Image3]
</center>

```csharp
ServicePlacementPreferPrimaryDomainPolicyDescription primaryDomain = new ServicePlacementPreferPrimaryDomainPolicyDescription();
primaryDomain.DomainName = "fd:/EastUS/";
serviceDescription.PlacementPolicies.Add(invalidDomain);
```

Środowiska PowerShell:

```posh
New-ServiceFabricService -ApplicationName $applicationName -ServiceName $serviceName -ServiceTypeName $serviceTypeName –Stateful -MinReplicaSetSize 3 -TargetReplicaSetSize 3 -PartitionSchemeSingleton -PlacementPolicy @("PreferredPrimaryDomain,fd:/EastUS")
```

## <a name="requiring-replica-distribution-and-disallowing-packing"></a>Wymaganie dystrybucji repliki i brak zezwolenia pakowania
Repliki są _zwykle_ rozproszonych w domenach awarii i uaktualniania, gdy hello klastra jest w dobrej kondycji. Istnieją jednak przypadki, w których może mieć więcej niż jednej repliki dla danej partycji tymczasowo spakowana do jednej domeny. Na przykład, załóżmy, że ten klaster hello ma dziewięć węzłów w trzech domen błędów, fd: / 0, fd: / 1 i fd: / 2. Również Załóżmy, że usługa ma trzy repliki. Załóżmy, że hello węzłów, które były używane przez te repliki w fd: / 1 i fd: / 2 zakończył działanie. Zwykle hello Menedżera zasobów klastra wolisz inne węzły w tych samym domen błędów. W takim przypadku Załóżmy, że ze względu na problemy toocapacity żadna z hello były ważne inne węzły w tych domenach. Jeśli hello Menedżera zasobów klastra kompilacje zastępujące tych replik, miałoby toochoose węzłów w fd: / 0. Jednak podczas _który_ tworzy sytuacji, gdy jest naruszone hello ograniczenia domeny błędów. Pakowanie zwiększa replik hello ryzyko, że hello zestawu replik całego można wyłączenia lub zostać utracone. 

> [!NOTE]
> Aby uzyskać więcej informacji na temat ograniczeń oraz ograniczenia, priorytetów ogólnie rzecz biorąc, zapoznaj się z [w tym temacie](service-fabric-cluster-resource-manager-management-integration.md#constraint-priorities).
>

Jeśli kiedykolwiek w tym samouczku komunikat kondycji takich jak "`hello Load Balancer has detected a Constraint Violation for this Replica:fabric:/<some service name> Secondary Partition <some partition ID> is violating hello Constraint: FaultDomain`", a następnie został trafiony tego warunku lub przypominać go. Zwykle tylko jedną lub dwie repliki są pakowane tymczasowo. Tak długo, jak są mniej niż kworum replik w danej domenie, możesz bezpieczne. Opakowanie jest rzadko, jednak może się zdarzyć, oraz zwykle tych sytuacji przejściowej ponieważ węzłów hello wrócić. Jeśli węzły hello pozostać w dół i hello Menedżera zasobów klastra musi zamiany toobuild, zazwyczaj dostępne są inne węzły w domenach awarii idealne hello.

Niektórych obciążeń wolisz zawsze używania hello docelowej liczby replik, nawet jeśli ich są pakować do mniejszej liczby domen. Te obciążenia są stawiając przed awariami całkowita liczba jednoczesnych domeny stałe i zwykle można odzyskać stanu lokalnego. Innych obciążeń raczej wymagałoby wcześniejszej niż poprawności ryzyko lub utraty danych hello przestoju. Uruchom większości obciążeń produkcyjnych z więcej niż trzy repliki, więcej niż trzy domen błędów i wiele węzłów prawidłowy na domeny błędów. W związku z tym hello domyślne zachowanie umożliwia pakowania domeny domyślnie. Hello domyślne zachowanie umożliwia równoważenia normalnym i pracy awaryjnej toohandle te ekstremalnych przypadkach, nawet w przypadku oznacza to, że tymczasowe domeny pakowania.

Jeśli chcesz toodisable takie pakowania dla danego obciążenia, można określić hello `RequireDomainDistribution` zasad w usłudze hello. Gdy ta zasada jest ustawiona, hello Cluster Resource Manager zapewnia nie dwóch replik z hello uruchamiania tej samej partycji w hello tej samej usterki lub domena uaktualnienia.

Kod:

```csharp
ServicePlacementRequireDomainDistributionPolicyDescription distributeDomain = new ServicePlacementRequireDomainDistributionPolicyDescription();
serviceDescription.PlacementPolicies.Add(distributeDomain);
```

Środowiska PowerShell:

```posh
New-ServiceFabricService -ApplicationName $applicationName -ServiceName $serviceName -ServiceTypeName $serviceTypeName –Stateful -MinReplicaSetSize 3 -TargetReplicaSetSize 3 -PartitionSchemeSingleton -PlacementPolicy @("RequiredDomainDistribution")
```

Teraz, może on być możliwe toouse te konfiguracje dla usług w klastrze, który nie został geograficznie łączone? Użytkownik może, ale nie ma dużą Przyczyna zbyt. Witaj konfiguracjach wymaganych, nieprawidłowy i preferowanych domen należy unikać o ile nie wymagają hello scenariuszy. Nie rozsądne żadnych tooforce tootry znaczeniu toorun danego obciążenia w jednej lub tooprefer niektórych segmentu klastra lokalnego zamiast innego. Różne konfiguracje sprzętu należy rozłożyć na domenach awarii i obsługiwane za pośrednictwem ograniczenia umieszczania normalne i właściwości węzła.

## <a name="next-steps"></a>Następne kroki
- Aby uzyskać więcej informacji na temat konfigurowania usługi [Dowiedz się więcej o konfigurowaniu usługi](service-fabric-cluster-resource-manager-configure-services.md)

[Image1]:./media/service-fabric-cluster-resource-manager-advanced-placement-rules-placement-policies/cluster-invalid-placement-domain.png
[Image2]:./media/service-fabric-cluster-resource-manager-advanced-placement-rules-placement-policies/cluster-required-placement-domain.png
[Image3]:./media/service-fabric-cluster-resource-manager-advanced-placement-rules-placement-policies/cluster-preferred-primary-domain.png
