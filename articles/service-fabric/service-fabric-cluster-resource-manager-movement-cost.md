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
# <a name="service-movement-cost"></a>Usługa koszt przeniesienia
Współczynnik hello zasobu klastra sieci szkieletowej programu Service Manager uwzględnia podczas próby toodetermine, jakie zmiany toomake tooa klastra jest koszt hello tych zmian. pojęcie "koszt" Hello jest przedmiotem handlu wyłączone przed można zwiększyć ilość hello klastra. Koszt jest brana pod uwagę podczas przenoszenia usługi równoważenia, defragmentacji i inne wymagania. Celem Hello jest toomeet hello wymagań dotyczących hello co najmniej sposób destrukcyjne lub kosztowne. 

Przesunięcie czasu procesora CPU koszty usługi i przepustowość co najmniej sieci. Dla stanowych usług wymaga kopiowanie hello stan tych usług, wykorzystywanie dodatkowej pamięci i dysku. Minimalizowania kosztów hello rozwiązań tego powitalne Menedżera zasobów klastra sieci szkieletowej usług Azure pojawia się z pomaga, upewnij się, że zasoby hello klastra nie są poświęconego niepotrzebnie. Jednak nie należy tooignore rozwiązania, które może znacznie poprawić hello alokacji zasobów w klastrze hello.

Hello Menedżera zasobów klastra ma dwa sposoby obliczenie kosztów i ograniczeniem im dostępu przy próbie toomanage hello klastra. mechanizm pierwszy Hello jest po prostu zliczania każdy ruch, który może to spowodować. Jeśli dwa rozwiązania są generowane z o hello hello Menedżera zasobów klastra preferuje hello jedną z hello najniższy koszt (całkowita liczba przenosi), a następnie sam równoważenie (wynik).

Ta strategia działa prawidłowo. Ale tak jak w przypadku domyślnych lub obciążeń statycznych, jest mało prawdopodobne w każdym systemie złożonych, że przenoszenie wszystkich są takie same. Niektóre są prawdopodobnie toobe bardziej kosztowne.

## <a name="setting-move-costs"></a>Ustawienie przesuwanie kosztów 
Możesz określić hello domyślny koszt przeniesienia usługi po utworzeniu:

Program PowerShell:

```posh
New-ServiceFabricService -ApplicationName $applicationName -ServiceName $serviceName -ServiceTypeName $serviceTypeName –Stateful -MinReplicaSetSize 3 -TargetReplicaSetSize 3 -PartitionSchemeSingleton -DefaultMoveCost Medium
```

C#: 

```csharp
FabricClient fabricClient = new FabricClient();
StatefulServiceDescription serviceDescription = new StatefulServiceDescription();
//set up hello rest of hello ServiceDescription
serviceDescription.DefaultMoveCost = MoveCost.Medium;
await fabricClient.ServiceManager.CreateServiceAsync(serviceDescription);
```

Można również określić lub zaktualizować MoveCost dynamicznie usługi po utworzeniu usługi hello: 

Program PowerShell: 

```posh
Update-ServiceFabricService -Stateful -ServiceName "fabric:/AppName/ServiceName" -DefaultMoveCost High
```

C#:

```csharp
StatefulServiceUpdateDescription updateDescription = new StatefulServiceUpdateDescription();
updateDescription.DefaultMoveCost = MoveCost.High;
await fabricClient.ServiceManager.UpdateServiceAsync(new Uri("fabric:/AppName/ServiceName"), updateDescription);
```

## <a name="dynamically-specifying-move-cost-on-a-per-replica-basis"></a>Dynamicznie Określanie koszt przeniesienia na podstawie na repliki

Witaj poprzedniego fragmenty kodu są wszystkie służący do określania MoveCost dla całej usługi jednocześnie z samej usługi poza hello. Jednak przenieść koszt jest najbardziej przydatna jest, gdy koszt przeniesienia hello obiektu określonej usługi zmienia się w jego cykl życia. Ponieważ hello usług prawdopodobnie ma hello najważniejsze informacje o tym, jak kosztowne są toomove danym czasie, jest interfejs API dla usług tooreport własnych indywidualnych przenoszenia kosztów w czasie wykonywania. 

C#:

```csharp
this.Partition.ReportMoveCost(MoveCost.Medium);
```

## <a name="impact-of-move-cost"></a>Wpływ koszt przeniesienia
MoveCost zawiera cztery poziomy: Zero, niski, średni i wysoki. MoveCosts są względną tooeach innych, z wyjątkiem Zero. Zero koszt przeniesienia oznacza, że przenoszenie jest bezpłatna i nie powinien odliczona wynik hello hello rozwiązania. Ustawienie jest przejście koszt tooHigh *nie* gwarantuje, że repliki hello pozostaje w jednym miejscu.

<center>
![Koszt przeniesienia jako czynnik wyborze repliki dla przepływu][Image1]
</center>

MoveCost pomaga hello rozwiązania czy przyczyna ogólne hello zakłóceń pracy i są najprostszym tooachieve podczas nadal otrzymywanych saldo równoważne. Pojęcie usługi koszt może być względna toomany rzeczy. Witaj najbardziej typowych czynników przy obliczaniu koszt przeniesienia są:

- Kwota Hello danych, że usługa hello ma toomove lub stanu.
- Koszt Hello rozłączenia klientów. Przenoszenie replikę podstawową jest zazwyczaj bardziej kosztowne niż koszt hello przenoszenia replikę pomocniczą.
- Koszt Hello zakłócania pracy locie. Niektóre operacje na danych hello magazynu poziom lub operacje wykonywane w odpowiedzi tooa klienta wywołania są kosztowne. W pewnym momencie nie chcesz toostop je, jeśli nie masz. Gdy trwa operacja hello, więc zwiększyć hello koszt przeniesienia tej usługi obiektu tooreduce hello prawdopodobieństwo, że powoduje przeniesienie. Po zakończeniu operacji hello, należy ustawić toonormal wstecz hello kosztów.

## <a name="enabling-move-cost-in-your-cluster"></a>Włączanie koszt przeniesienia w klastrze
Aby hello bardziej szczegółowego toobe MoveCosts wziąć pod uwagę, MoveCost musi być włączona w klastrze. Bez tego ustawienia hello domyślny tryb liczenia przenosi jest używany do obliczania MoveCost i MoveCost raporty są ignorowane.


ClusterManifest.xml:

``` xml
        <Section Name="PlacementAndLoadBalancing">
            <Parameter Name="UseMoveCostReports" Value="true" />
        </Section>
```

za pomocą pliku ClusterConfig.json dla autonomicznych wdrożeniach lub Template.json dla platformy Azure hostowanej klastrów:

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

## <a name="next-steps"></a>Następne kroki
- Menedżer zasobów klastra sieci szkieletowej usług używa metryki toomanage użycia i pojemności hello klastra. więcej informacji na temat metryki toolearn i jak tooconfigure, zapoznaj się z [Zarządzanie zużycia zasobów i obciążenia w sieci szkieletowej usług o metryki](service-fabric-cluster-resource-manager-metrics.md).
- toolearn dotyczące sposobu hello Menedżera zasobów klastra zarządza i równoważy obciążenie hello klastra, zapoznaj się z [równoważenia klastra usługi sieć szkieletowa](service-fabric-cluster-resource-manager-balancing.md).

[Image1]:./media/service-fabric-cluster-resource-manager-movement-cost/service-most-cost-example.png
