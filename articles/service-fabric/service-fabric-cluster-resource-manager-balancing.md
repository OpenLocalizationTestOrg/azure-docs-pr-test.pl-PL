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
# <a name="balancing-your-service-fabric-cluster"></a>Równoważenie klastra sieci szkieletowej usług
Hello zasobu klastra sieci szkieletowej programu Service Manager obsługuje dynamicznego obciążenia zmian, dające dodatnią reakcję tooadditions lub usuwania węzłów lub usług. Automatycznie koryguje naruszenia ograniczeń i aktywne rebalances hello klastra. Jak często są te akcje podjęte — a wywołujących je?

Istnieją trzy różne kategorie pracy tego powitalne Menedżer zasobów klastra. Są to:

1. Rozmieszczenia — ten etap dotyczy umieszczenie replik stanowe ani bezstanowych wystąpień, które nie są spełnione. Umieszczanie zawiera nowe usługi i obsługa repliki stanowego lub bezstanowego wystąpień, których nie powiodła. Usuwanie i usunięcie repliki lub wystąpienia są obsługiwane w tym miejscu.
2. Ograniczenie sprawdza — ten etap sprawdza i koryguje naruszenia ograniczeń umieszczania różnych hello (reguły) w systemie hello. Przykłady reguł jest rzeczy, takich jak zapewnienie, że węzły nie są przeciążone i że spełnione są ograniczenia umieszczania usług.
3. Równoważenie — ten etap sprawdza toosee, jeśli ponowne równoważenie niezbędne jest oparte na powitania skonfigurowane żądany poziom saldo dla różnych metryki. Jeśli tak podejmie toofind rozmieszczenia w hello klastra to znaczy więcej zrównoważonym.

## <a name="configuring-cluster-resource-manager-timers"></a>Konfigurowanie czasomierze Menedżera zasobów klastra
pierwszy zestaw kontrolek wokół równoważenia Hello są zestawem czasomierze. Czasomierze te określają, jak często hello Cluster Resource Manager sprawdza hello klastra i wykonuje akcje naprawcze.

Każdy z tych różnego rodzaju powitalne poprawki Menedżera zasobów klastra można wprowadzać jest kontrolowana przez inną czasomierza kontroluje częstotliwość. Po każdym czasomierza, hello zadanie zostało zaplanowane. Domyślnie hello Menedżera zasobów:

* skanuje stanu i stosuje aktualizacje (na przykład rejestrowania, który jest węzłem w dół) co 1/10 sekundy
* Ustawia flagę wyboru umieszczenia hello 
* Ustawia flagę wyboru ograniczenia hello co sekundę
* Ustawia hello równoważenia flagi co pięć sekund.

Przykłady dotyczące tych czasomierze konfiguracji hello jest poniżej:

ClusterManifest.xml:

``` xml
        <Section Name="PlacementAndLoadBalancing">
            <Parameter Name="PLBRefreshGap" Value="0.1" />
            <Parameter Name="MinPlacementInterval" Value="1.0" />
            <Parameter Name="MinConstraintCheckInterval" Value="1.0" />
            <Parameter Name="MinLoadBalancingInterval" Value="5.0" />
        </Section>
```

za pomocą pliku ClusterConfig.json dla autonomicznych wdrożeniach lub Template.json dla platformy Azure hostowanej klastrów:

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

Dzisiaj hello Menedżera zasobów klastra tylko wykonuje jedno z następujących działań w czasie, po kolei. To dlatego firma Microsoft można znaleźć czasomierze toothese "minimalna interwałem" i działania, które uzyskać wykonane podczas czasomierze hello go jako "ustawienie flagi" hello. Na przykład powitalne Menedżera zasobów klastra zajmuje się oczekujące żądania usług toocreate przed hello klastra równoważenia. Jak widać według przedziałów czasu domyślne hello określonych hello Menedżera zasobów klastra szuka niczego go toodo potrzeb często. Zwykle oznacza to, że zestaw hello zmiany wprowadzone podczas każdego kroku ma mała. Zmiany wprowadzone w małych często umożliwia hello toobe Menedżera zasobów klastra odpowiadać podczas to wiele problemów w klastrze hello. Hello czasomierze domyślne podać niektóre przetwarzanie wsadowe od wielu hello same rodzaje zdarzeń zwykle toooccur jednocześnie. 

Na przykład po awarii węzłów robią to całego domen błędów w czasie. Wszystkie te błędy są przechwytywane podczas hello następny stan aktualizacji po hello *PLBRefreshGap*. poprawki Hello są określane podczas powitania po umieszczania, sprawdzanie ograniczenia i Równoważenie działa. Przez domyślny hello Menedżera zasobów klastra nie jest skanowanie za pomocą godziny zmian w klastrze hello i podjęcie próby tooaddress wszystkie zmiany na raz. W ten sposób może spowodować toobursts zmian.

Hello Menedżera zasobów klastra musi także niektóre toodetermine dodatkowe informacje klastrowania hello imbalanced. W tym mamy dwóch elementów konfiguracji: *BalancingThresholds* i *ActivityThresholds*.

## <a name="balancing-thresholds"></a>Równoważenie progi
Próg równoważenia jest formantu hello służącą do wyzwalania ponowne równoważenie. Witaj równoważenia próg dla metryki jest _współczynnik_. Jeśli hello obciążenia dla metryki na powitania najbardziej załadowany węzła rozdzielonych hello wielkość obciążenia na powitania najmniej załadować węzła przekracza tego Metryka *BalancingThreshold*, klaster hello jest imbalanced. W związku z tym równoważenia jest wyzwalana hello dalej czasu powitalne sprawdza Menedżera zasobów klastra. Witaj *MinLoadBalancingInterval* czasomierza Określa, jak często hello Menedżera zasobów klastra powinna Sprawdź, czy konieczne jest ponowne równoważenie. Sprawdzanie nie oznacza, że awarii. 

Progi równoważenia są zdefiniowane w zasadzie na Metryka jako część definicji klastra hello. Aby uzyskać więcej informacji dotyczących metryki, zapoznaj się [w tym artykule](service-fabric-cluster-resource-manager-metrics.md).

ClusterManifest.xml

```xml
    <Section Name="MetricBalancingThresholds">
      <Parameter Name="MetricName1" Value="2"/>
      <Parameter Name="MetricName2" Value="3.5"/>
    </Section>
```

za pomocą pliku ClusterConfig.json dla autonomicznych wdrożeniach lub Template.json dla platformy Azure hostowanej klastrów:

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

<center>
![Równoważenie przykład próg][Image1]
</center>

W tym przykładzie każda usługa zajmuje jedną jednostkę niektóre metryki. W górnym przykład Witaj hello maksymalne obciążenie w węźle osiągnie wartość 5 i hello minimalna wynosi dwa. Załóżmy, że ten hello równoważenia próg ta metryka jest trzy. Ponieważ współczynnik hello w klastrze hello jest 5/2 = 2.5 i który jest mniejszy niż określony hello równoważenia próg trzy, klaster hello jest rozmieszczana. Bez równoważenia jest wyzwalane, gdy sprawdza hello Menedżera zasobów klastra.

W przykładzie dolnej hello hello maksymalne obciążenie w węźle wynosi 10, gdy hello jest co najmniej dwóch, co w stosunku pięć. Pięć jest większa niż hello wyznaczonych próg równoważenia trzech dla tej metryki. W związku z tym rebalancing Uruchom będzie zaplanowane hello czas następnego równoważenia uruchamiany czasomierza. W sytuacji, jak to niektóre obciążenia jest zwykle rozproszonej tooNode3. Witaj zasobu klastra sieci szkieletowej programu Service Manager korzysta z podejścia intensywnie, niektóre obciążenia mogą być również tooNode2 rozproszonych. 

<center>
![Równoważenie akcje przykład próg][Image2]
</center>

> [!NOTE]
> "" Równoważenie dwa różne strategie zarządzania obciążenia w klastrze. strategii domyślne Hello hello używa Menedżera zasobów klastra jest toodistribute obciążenia w węzłach klastra hello hello. Witaj innych strategii jest [defragmentacji](service-fabric-cluster-resource-manager-defragmentation-metrics.md). Defragmentacja jest wykonywane podczas hello równoważenia tego samego uruchomienia. Hello strategii równoważenia i defragmentacji może służyć do różnych metryk w hello tego samego klastra. Usługa może mieć równoważenia i defragmentacji metryki. Dla metryki defragmentacji hello stosunek hello jest ładowane w hello klastra wyzwala ponowne równoważenie, gdy jest _poniżej_ hello równoważenia próg. 
>

Pobieranie poniżej hello równoważenia próg nie jest celem jawnego. Progi równoważenia są po prostu *wyzwalacza*. Podczas równoważenia działa, hello Menedżera zasobów klastra określa jakie ulepszenia go, jeśli istnieją. Tak, ponieważ zostało rozpoczęte równoważenia wyszukiwania nie oznacza niczego przenosi. Czasami hello klastra jest toocorrect imbalanced, ale zbyt ograniczone. Alternatywnie ulepszenia hello wymagają przesunięcia, które są zbyt [kosztowne](service-fabric-cluster-resource-manager-movement-cost.md)).

## <a name="activity-thresholds"></a>Progi działania
Czasami, mimo że węzły są stosunkowo imbalanced, hello *całkowita* obciążenie klastra hello jest niska. Brak Hello obciążenia może być przejściowy dip lub załadować, ponieważ klaster hello jest nowy i po prostu pobierania. W obu przypadkach nie może być czas toospend hello klastra równoważenia, ponieważ brak małego toobe zdobytych. Jeśli klaster hello zostały poddane równoważenia, czy spędzają sieci i obliczeniowe elementy toomove zasobów wokół bez wprowadzania żadnych dużych *bezwzględną* różnicy. Przenosi tooavoid niepotrzebne, istnieje inny formant znany jako progi działania. Progi działania umożliwia toospecify niektórych bezwzględną dolna granica dla działania. Jeśli żaden węzeł nie jest powyżej tego progu, równoważenia nie jest wyzwalane, nawet jeśli hello równoważenia osiągnięty jest próg.

Załóżmy, że firma Microsoft będzie przechowywała naszych próg równoważenia trzech dla tej metryki. Również Załóżmy, że mamy 1536 próg działania. W pierwszym przypadku hello podczas gdy klaster hello jest imbalanced na powitania równoważenia próg nie jest nie spełnia węzła progu działania, więc nic się nie dzieje. Przykład Witaj dolnej Node1 znajduje się nad hello próg działania. Ponieważ oba hello równoważenia próg i hello próg działania dla metryki hello zostaną przekroczone, równoważenia według harmonogramu. Na przykład Przyjrzyjmy się powitania po diagramu: 

<center>
![Przykład progu działania][Image3]
</center>

Podobnie jak Równoważenie progi progi działania są zdefiniowane na — pomiar za pośrednictwem definicji klastra hello:

ClusterManifest.xml

``` xml
    <Section Name="MetricActivityThresholds">
      <Parameter Name="Memory" Value="1536"/>
    </Section>
```

za pomocą pliku ClusterConfig.json dla autonomicznych wdrożeniach lub Template.json dla platformy Azure hostowanej klastrów:

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

Progi równoważenie i działania są określonej metryki wiązanej tooa - równoważenia zostanie wywołany tylko wtedy, gdy oba hello równoważenia próg i przekroczeniu progu działania dla hello tę samą metrykę.

## <a name="balancing-services-together"></a>Razem równoważenia usług
Czy klaster hello jest imbalanced lub nie jest decyzja całego klastra. Jednak sposób hello rozszerzana o naprawienie go przenoszone replik poszczególnych usług i wystąpień wokół. To sens, PRAWDA? Jeśli na jednym węźle umieszczany jest pamięć, wiele replik lub wystąpień może przyczyniać się tooit. Nierównowaga hello ustalające może wymagać przenoszenie tych hello repliki stanowego lub bezstanowego wystąpieniom Metryka imbalanced hello.

Od czasu do czasu, gdy usługi, której sam imbalanced nie pobiera przenieść (Pamiętaj dyskusji hello lokalnych i globalnych przeprowadzi wcześniej). Dlaczego czy usługi są przenoszone podczas wszystkie opcje, które zostały zrównoważonym metryki usługi? Zobaczmy:

- Załóżmy, że istnieją cztery usług, Service1 roboczego2, Service3 i Service4. 
- Service1 raporty metryk Metric1 i Metric2. 
- Klienta2 raporty metryk Metric2 i Metric3. 
- Service3 raporty metryk Metric3 i Metric4.
- Service4 raporty Metric99 metryki. 

Z pewnością widać, gdy chcemy tutaj: istnieje łańcuch! Nie mamy naprawdę cztery usługi niezależne, będziemy mieć trzy usługi, które są powiązane i taki, który jest wyłączony na jego własnej.

<center>
![Razem równoważenia usług][Image4]
</center>

Ze względu na tym łańcuchu jest możliwe, że nierównowaga w metryki 1-4 może spowodować repliki lub wystąpień tooservices toomove 1 – 3 wokół. Wiemy, również nierównowaga w metryki 1, 2 lub 3 nie może spowodować przeniesień w Service4. Ponieważ przenoszenie hello replik nie byłoby żaden punkt i wystąpień tooService4 wokół może nic nie absolutnie saldo hello tooimpact metryki 1-3.

Witaj Menedżera zasobów klastra automatycznie danych liczbowych się tym, które usługi są powiązane. Dodawanie, usuwanie lub zmiana hello metryki dla usługi mogą mieć wpływ na ich relacji. Na przykład między dwa przebiegi równoważenia klienta2 mogły zostać zaktualizowane tooremove Metric2. To spowoduje przerwanie łańcucha hello między Service1 i klienta2. Teraz zamiast dwie grupy usług, istnieją trzy:

<center>
![Razem równoważenia usług][Image5]
</center>

## <a name="next-steps"></a>Następne kroki
* Metryki są zarządzaniu hello Menedżer zasobów klastra sieci szkieletowej usług konsumenckich i pojemności w klastrze hello. więcej informacji na temat metryki toolearn i jak tooconfigure, zapoznaj się z [w tym artykule](service-fabric-cluster-resource-manager-metrics.md)
* Koszt przeniesienia jest jednym ze sposobów sygnalizowania toohello Menedżera zasobów klastra, że niektóre usługi są toomove droższe niż inne. Aby uzyskać więcej informacji o koszt przeniesienia odwoływać się za[w tym artykule](service-fabric-cluster-resource-manager-movement-cost.md)
* Witaj Menedżera zasobów klastra ma kilka limity skonfigurowania tooslow dół przenoszenie hello klastra. Nie są one zazwyczaj konieczne, ale jeśli są potrzebne informacje na temat ich [tutaj](service-fabric-cluster-resource-manager-advanced-throttling.md)

[Image1]:./media/service-fabric-cluster-resource-manager-balancing/cluster-resrouce-manager-balancing-thresholds.png
[Image2]:./media/service-fabric-cluster-resource-manager-balancing/cluster-resource-manager-balancing-threshold-triggered-results.png
[Image3]:./media/service-fabric-cluster-resource-manager-balancing/cluster-resource-manager-activity-thresholds.png
[Image4]:./media/service-fabric-cluster-resource-manager-balancing/cluster-resource-manager-balancing-services-together1.png
[Image5]:./media/service-fabric-cluster-resource-manager-balancing/cluster-resource-manager-balancing-services-together2.png
