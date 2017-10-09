---
title: "aaaService Menedżer zasobów klastra sieci szkieletowej — koligacja | Dokumentacja firmy Microsoft"
description: "Omówienie konfigurowania koligacji dla usługi sieci szkieletowej usług"
services: service-fabric
documentationcenter: .net
author: masnider
manager: timlt
editor: 
ms.assetid: 678073e1-d08d-46c4-a811-826e70aba6c4
ms.service: Service-Fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/18/2017
ms.author: masnider
ms.openlocfilehash: 7dc9b6d9c18d9d615d39cff7de9d7cba1c040474
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="configuring-and-using-service-affinity-in-service-fabric"></a>Konfigurowanie i używanie koligację usługi w sieci szkieletowej usług
Koligacja jest formant, który znajduje się głównie toohelp łatwość hello przejście większych wbudowanymi aplikacji w chmurze i mikrousług Witaj, świecie. Również służy do optymalizacji dla poprawy wydajności hello usług, chociaż może to mieć skutki uboczne.

Załóżmy, że w przypadku wprowadzenia większych aplikacji lub taki, który właśnie nie został zaprojektowany z mikrousług w uwadze (tooService sieci szkieletowej lub dowolnym środowisku rozproszonym). Ten typ przejścia jest wspólnej. Należy rozpocząć od podnoszenia hello całą aplikację do środowiska hello, pakowanie i upewnić się, że działa bez problemów. Następnie możesz uruchomić podzielenie go na różnych usług mniejszych, że wszystkie komunikować tooeach innych.

Po pewnym czasie może się okazać czy aplikacji hello występują problemy. Witaj problemów zwykle należą do jednej z tych kategorii:

1. Inny składnik X wbudowanymi aplikacji hello ma zależność nieudokumentowanej składnika Y, i tylko włączone tych składników do poszczególnych usług. Ponieważ te usługi są uruchomione w różnych węzłach w klastrze hello, są one uszkodzone.
2. Te składniki komunikują się za pośrednictwem (lokalnej nazwane potoki | współużytkowana pamięć | pliki na dysku) i naprawdę potrzebują zasobu lokalnego tooa udostępnionych stanie toowrite toobe ze względu na wydajność w tej chwili. Zależność twardych ta zostanie usunięta później, może być.
3. Wszystko działa poprawnie, ale włącza się, że te dwa składniki są faktycznie chatty wydajności poufnych. Gdy są przenoszone do poszczególnych usług ogólne tanked wydajność aplikacji lub opóźnienia zwiększyć. W związku z tym hello ogólną aplikacja jest nie spełnia oczekiwania.

W takich przypadkach firma Microsoft nie mają toolose refaktoryzacji pracę i nie mają toogo monolityczna toohello Wstecz. ostatni warunek Hello może być pożądane zwykły optymalizacji. Jednak do czasu firma Microsoft może naturalnie zmodyfikowanie toowork składniki hello jako usługi (lub do czasu firma Microsoft może rozwiązać oczekiwania dotyczące wydajności hello inny sposób) zamierzamy tooneed pewnym sensie lokalizacji.

Jakie toodo? Można również spróbuj Włączenie koligacji.

## <a name="how-tooconfigure-affinity"></a>Jak tooconfigure koligacji
tooset się koligacji, należy zdefiniować relację koligację między dwóch różnych usług. Można potraktować koligacji jako "wskazuje" jedną usługę w innej i informacją "tej usługi można uruchamiać tylko gdy czy usługa jest uruchomiona." Czasami firma Microsoft można znaleźć tooaffinity jako relacji nadrzędny/podrzędny (gdzie wskażesz podrzędnych hello na powitania nadrzędnego). Koligacja gwarantuje, że repliki hello lub wystąpień jednej usługi są umieszczane na powitania takie same węzły, które innej usługi.

```csharp
ServiceCorrelationDescription affinityDescription = new ServiceCorrelationDescription();
affinityDescription.Scheme = ServiceCorrelationScheme.Affinity;
affinityDescription.ServiceName = new Uri("fabric:/otherApplication/parentService");
serviceDescription.Correlations.Add(affinityDescription);
await fabricClient.ServiceManager.CreateServiceAsync(serviceDescription);
```

> [!NOTE]
> Usługa podrzędne tylko mogą uczestniczyć w relacji jeden koligacji. Jeśli jednocześnie chce hello podrzędnych toobe skoligowanych tootwo nadrzędnej usługi masz kilka opcji:
> - Wycofaj relacje hello (mają parentService1 i parentService2 punkt w bieżącej usługi podrzędnych hello), lub
> - Wyznaczanie jeden z elementów nadrzędnych hello koncentratora Konwencja i wszystkich usług punkt w tej usłudze. 
>
> Hello wynikowa zachowanie przy umieszczaniu w klastrze hello powinien hello w tej samej.
>

## <a name="different-affinity-options"></a>Koligacja różnych opcji
Koligacja jest reprezentowany przez jeden z kilku systemów korelacji i ma dwa różne tryby. najbardziej typowe tryb koligacji Hello jest określane mianem NonAlignedAffinity. W NonAlignedAffinity, hello repliki lub wystąpień hello różnych usług są umieszczane na powitania sam węzłów. Witaj innych tryb jest AlignedAffinity. Wyrównane koligacji przydaje się tylko z usług stanowych. Konfigurowanie dwóch stateful koligacji toohave wyrównane usług gwarantuje, czy kolory podstawowe hello tych usług są umieszczane na hello samych węzłów jako wzajemnie. Powoduje także każda para pomocnicze bazy danych dla tych usług toobe dotyczącymi hello sam węzłów. Istnieje również możliwość (mimo że mniej typowych) tooconfigure NonAlignedAffinity dla stanowych usług. NonAlignedAffinity innej repliki powitalne dwie usługi stanowej są uruchamiane na powitania hello samych węzłów, ale może to spowodować ich kolory podstawowe w różnych węzłach.

<center>
![Tryby koligacji i ich wpływ][Image1]
</center>

### <a name="best-effort-desired-state"></a>Najlepszy stan potrzeby nakładu pracy
Relacja koligacji to optymalne rozwiązanie. Nie zapewnia ona hello takie same gwarancje kolokacji lub niezawodności, która działa w hello jest tego samego pliku wykonywalnego procesu. usługi Hello w relacja koligacji są zasadniczo różne jednostki, które może zakończyć się niepowodzeniem i można przenosić niezależnie. Relacja koligacji może również spowodować przerwanie, chociaż te podziały są tymczasowe. Na przykład ograniczenia dotyczące pojemności może oznaczać tylko niektóre obiekty usługi hello relacja koligacji hello można zmieścić w danym węźle. W takich przypadkach, mimo że istnieje relacja koligacji w miejscu, go nie można wymusić termin toohello inne ograniczenia. Toodo możliwe jest tak, naruszenie hello jest automatycznie rozwiązany później.

### <a name="chains-vs-stars"></a>Łańcuchy a gwiazdek
Dzisiaj hello Menedżera zasobów klastra nie jest łańcuchów stanie toomodel koligacji relacji. Co to oznacza, że jest to, że usługa, która jest elementem podrzędnym w jednej relacji koligacji nie może być elementem nadrzędnym w innej relacji koligacji. Jeśli chcesz toomodel tego typu relacji, efektywnie masz toomodel go jako gwiazdy zamiast łańcucha. toomove z gwiazdką tooa łańcucha, podrzędne znajdujących się najniżej hello zamiast tego będzie nadrzędnego nadrzędnego toohello pierwszy podrzędny. W zależności od hello rozmieszczenie usług może być toodo wielokrotnie. Jeśli nie ma usługi rodzica, może być toocreate, który służy jako symbol zastępczy. W zależności od wymagań, konieczne może być również toolook do [grup aplikacji](service-fabric-cluster-resource-manager-application-groups.md).

<center>
![Łańcuchy vs. Gwiazdki w hello relacje kontekstu koligacji][Image2]
</center>

Inny element toonote o relacjach koligacji obecnie jest czy dwukierunkowego. Oznacza to, że w tej regule koligacji hello tylko wymusza dzieckiem hello umieszczane z nadrzędnego hello. Nie zapewnia się, że elementem nadrzędnym hello jest znajdują się w tym hello podrzędnych. Jest również istotne toonote, który hello relacja koligacji nie jest doskonała lub natychmiast wymuszana od różnych usług z różnych cykle i może zakończyć się niepowodzeniem, a przenosić niezależnie. Załóżmy na przykład, że nadrzędny hello nagła awaria nad węzłem tooanother ponieważ uległ awarii. Hello Menedżera zasobów klastra i dojścia menedżera trybu Failover hello trybu failover, ponieważ zatrzymując hello usług, spójne i dostępna jest hello priorytet. Po zakończeniu pracy awaryjnej hello hello relacja koligacji zostało przerwane, ale powitalne Menedżera zasobów klastra sądzi, że wszystko jest poprawnie do czasu jej powiadomienia dzieckiem hello nie znajduje się z nadrzędnym hello. Tego rodzaju testy są wykonywane okresowo. Więcej informacji na temat sposobu hello Cluster Resource Manager ocenia ograniczenia jest dostępna w [w tym artykule](service-fabric-cluster-resource-manager-management-integration.md#constraint-types), i [tego](service-fabric-cluster-resource-manager-balancing.md) zawiera więcej informacji na temat sposobu tooconfigure hello okresach, na którym są tych warunków ograniczających obliczone.   


### <a name="partitioning-support"></a>Partycjonowanie pomocy technicznej
toonotice końcowego operacją Hello o koligacji jest relacje koligacji nie są obsługiwane, gdy nadrzędne hello jest podzielona na partycje. Usługi nadrzędnej podzielonym na partycje, które mogą być obsługiwane po pewnym czasie, ale obecnie nie jest dozwolone.

## <a name="next-steps"></a>Następne kroki
- Aby uzyskać więcej informacji na temat konfigurowania usługi [Dowiedz się więcej o konfigurowaniu usługi](service-fabric-cluster-resource-manager-configure-services.md)
- toolimit usługi tooa niewielki zestaw komputerów lub agregację obciążenia hello usług, użyj [grup aplikacji](service-fabric-cluster-resource-manager-application-groups.md)

[Image1]:./media/service-fabric-cluster-resource-manager-advanced-placement-rules-affinity/cluster-resrouce-manager-affinity-modes.png
[Image2]:./media/service-fabric-cluster-resource-manager-advanced-placement-rules-affinity/cluster-resource-manager-chains-vs-stars.png