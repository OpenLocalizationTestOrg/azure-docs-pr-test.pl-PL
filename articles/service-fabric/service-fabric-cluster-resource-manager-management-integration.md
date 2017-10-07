---
title: "aaaService Menedżer zasobów klastra sieci szkieletowej — integracji zarządzania | Dokumentacja firmy Microsoft"
description: "Przegląd hello punkty integracji między hello Menedżera zasobów klastra i zarządzania sieci szkieletowej usług."
services: service-fabric
documentationcenter: .net
author: masnider
manager: timlt
editor: 
ms.assetid: 956cd0b8-b6e3-4436-a224-8766320e8cd7
ms.service: Service-Fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/18/2017
ms.author: masnider
ms.openlocfilehash: 9a24c9de121fbe2e8e5e8e4d117e64686918936a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="cluster-resource-manager-integration-with-service-fabric-cluster-management"></a>Integracji Menedżera zasobów klastra z zarządzania klastrem sieci szkieletowej usług
Witaj zasobu klastra sieci szkieletowej programu Service Manager nie dysku uaktualnień w sieci szkieletowej usług, ale zostało ono uwzględnione. Witaj pierwszy sposób hello pomaga Menedżera zasobów klastra z zarządzania przez hello śledzenia żądany stan hello klastra i usług hello wewnątrz niej. gdy go nie można wstawić hello klastra do hello wymaganą konfiguracją Hello Menedżera zasobów klastra wysyła raporty kondycji. Na przykład jeśli są niewystarczające hello pojemności Menedżera zasobów klastra wysyła ostrzeżeń i błędów wskazujących hello problem. Inny element integracji ma toodo o sposób działania uaktualnienia. Witaj Menedżera zasobów klastra nieco zmienia jego zachowanie podczas uaktualniania.  

## <a name="health-integration"></a>Integracja kondycji
Witaj Menedżera zasobów klastra śledzi stale hello reguł, które zostały określone dla wprowadzenie do usługi. Pozwala również śledzić hello pozostałych pojemności dla każdej metryki na powitania węzłów w klastrze hello i w hello klastra jako całość. Jeśli nie spełniają tych zasad lub są niewystarczające, są emitowane ostrzeżeń i błędów. Na przykład jeśli węzeł znajduje się nad pojemności i hello Menedżera zasobów klastra zostanie ponowiona sytuacji hello toofix przenosząc usług. Jeśli nie rozwiąże sytuacji hello emituje ostrzeżenie kondycji wskazująca, który węzeł jest za pośrednictwem pojemności i dla których metryki.

Innym przykładem ostrzeżeń menedżera zasobów hello jest naruszenia ograniczeń umieszczania. Na przykład, jeśli zdefiniowano ograniczenia umieszczania (takie jak `“NodeColor == Blue”`) i hello Resource Manager wykryje naruszenie takiego ograniczenia, jego emituje ostrzeżenie kondycji. Dotyczy to niestandardowe ograniczenia i hello domyślne ograniczenia (na przykład hello ograniczenia domeny błędów i domeny uaktualnienia).

Oto przykład jeden taki raport o kondycji. W takim przypadku raport o kondycji hello jest dla jednej partycji usługi systemowej hello. wiadomości powitania kondycji wskazuje powitalne replik tej partycji tymczasowo są pakować na zbyt mało domeny uaktualnienia.

```posh
PS C:\Users\User > Get-WindowsFabricPartitionHealth -PartitionId '00000000-0000-0000-0000-000000000001'


PartitionId           : 00000000-0000-0000-0000-000000000001
AggregatedHealthState : Warning
UnhealthyEvaluations  :
                        Unhealthy event: SourceId='System.PLB', Property='ReplicaConstraintViolation_UpgradeDomain', HealthState='Warning', ConsiderWarningAsError=false.

ReplicaHealthStates   :
                        ReplicaId             : 130766528804733380
                        AggregatedHealthState : Ok

                        ReplicaId             : 130766528804577821
                        AggregatedHealthState : Ok

                        ReplicaId             : 130766528854889931
                        AggregatedHealthState : Ok

                        ReplicaId             : 130766528804577822
                        AggregatedHealthState : Ok

                        ReplicaId             : 130837073190680024
                        AggregatedHealthState : Ok

HealthEvents          :
                        SourceId              : System.PLB
                        Property              : ReplicaConstraintViolation_UpgradeDomain
                        HealthState           : Warning
                        SequenceNumber        : 130837100116930204
                        SentAt                : 8/10/2015 7:53:31 PM
                        ReceivedAt            : 8/10/2015 7:53:33 PM
                        TTL                   : 00:01:05
                        Description           : hello Load Balancer has detected a Constraint Violation for this Replica: fabric:/System/FailoverManagerService Secondary Partition 00000000-0000-0000-0000-000000000001 is
                        violating hello Constraint: UpgradeDomain Details: UpgradeDomain ID -- 4, Replica on NodeName -- Node.8 Currently Upgrading -- false Distribution Policy -- Packing
                        RemoveWhenExpired     : True
                        IsExpired             : False
                        Transitions           : Ok->Warning = 8/10/2015 7:13:02 PM, LastError = 1/1/0001 12:00:00 AM
```

Oto, co ten komunikat kondycji informuje NAS jest:

1. Wszystkie repliki hello sami są w dobrej kondycji: każdy ma AggregatedHealthState: Ok
2. obecnie trwa naruszenia Hello ograniczenia dystrybucji domeny uaktualnienia. Oznacza to, że konkretnej domeny uaktualnienia zawiera więcej repliki z tej partycji niż powinien.
3. Węzeł, który zawiera powoduje naruszenie hello hello repliki. W takim przypadku jest hello węzeł z nazwą hello "Node.8"
4. Określa, czy uaktualnienie aktualnie wykonywane dla partycji to ("obecnie uaktualnianie — false")
5. Witaj zasad dystrybucji dla tej usługi: "Pakowania — zasady dystrybucji". To jest objęte hello `RequireDomainDistribution` [zasady rozmieszczania](service-fabric-cluster-resource-manager-advanced-placement-rules-placement-policies.md#requiring-replica-distribution-and-disallowing-packing). "Pakowanie" oznacza, że w takim przypadku DomainDistribution była _nie_ wymagane, aby było wiadomo, że zasady rozmieszczania nie został określony dla tej usługi. 
6. Gdy raport hello się stało - 2015-8-10 19:13:02: 00

Informacje o tej alerty uprawnień, że fire w toolet produkcyjnych, które znasz coś niepowodzenia i jest również używana toodetect, takich jak i zatrzymanie zły uaktualnienia. W takim przypadku czy chcemy toosee Jeśli firma Microsoft może dowiedzieć się, dlaczego hello Menedżera zasobów ma toopack hello replik na powitania domeny uaktualnienia. Zazwyczaj pakowania jest przejściowe, ponieważ hello węzłów hello innych domen uaktualnienia, na przykład.

Załóżmy, że hello Menedżera zasobów klastra jest w trakcie tooplace niektórych usług, ale nie ma żadnych rozwiązań, które działają. Gdy nie można umieścić usługi, są zazwyczaj z jednej hello z następujących powodów:

1. Niektóre stan przejściowy wprowadził go tooplace niemożliwe to wystąpienie usługi lub repliki poprawnie
2. wymagania dotyczące umieszczania usług Hello są unsatisfiable.

W takich przypadkach raportów o kondycji z hello Menedżera zasobów klastra pomóc w określeniu, dlaczego nie można umieścić hello usługi. Nazywamy to proces hello ograniczenia eliminacji sekwencji. Podczas jego hello system przeprowadzi Cię przez hello skonfigurowane ograniczenia wpływu na usługi hello i rekordy one usunąć. Dzięki temu po usługi będą mogli toobe umieszczone, widać węzły, które zostały usunięte i dlaczego.

## <a name="constraint-types"></a>Ograniczenia typów
Załóżmy porozmawiać na temat każdego z różnych ograniczeń hello w tych raportach o kondycji. Ograniczenia toothese powiązane komunikaty kondycji będzie wyświetlany po replik nie może zostać umieszczona.

* **ReplicaExclusionStatic** i **ReplicaExclusionDynamic**: tych warunków ograniczających wskazuje, że rozwiązanie zostało odrzucone, ponieważ hello dwa obiekty usługi z tej samej partycji zostaną toobe umieszczone na powitania sam węzeł. To nie jest dozwolona, ponieważ, a następnie awarii tego węzła zbyt będzie mieć wpływ na tej partycji. ReplicaExclusionStatic i ReplicaExclusionDynamic są prawie powitalne samą regułę i hello różnice naprawdę nie ma znaczenia. Jeśli pojawia się, że sekwencja eliminacji ograniczenia zawierające albo hello ograniczenie ReplicaExclusionStatic lub ReplicaExclusionDynamic hello Menedżera zasobów klastra sądzi, że nie ma wystarczającej liczby węzłów. Wymaga to pozostałych toouse rozwiązania te nieprawidłowe rozmieszczanie, które są niedozwolone. Hello innych ograniczeń w sekwencji hello będzie zazwyczaj Powiedz nam Dlaczego w miejscu pierwszego hello wyłącza się węzłów.
* **PlacementConstraint**: Jeśli ten komunikat zostanie wyświetlony, oznacza to, ponieważ nie odpowiadają one ograniczenia umieszczania usług hello możemy wyeliminować niektóre węzły. Firma Microsoft śledzenia limit ograniczenia umieszczania hello skonfigurowana jako część tego komunikatu. Jest to normalne, jeśli ma zdefiniowane ograniczenia umieszczania. Jednak jeśli ograniczenia umieszczania niepoprawnie powoduje zbyt wiele węzłów toobe, wyeliminowana jest to, jak można będzie zauważyć.
* **NodeCapacity**: to ograniczenie oznacza, że hello Menedżera zasobów klastra nie można umieścić hello replik na hello wskazanych węzłów, ponieważ który spowodowałaby je za pośrednictwem pojemności.
* **Koligacja**: to ograniczenie wskazuje, że firma Microsoft nie umieszczać hello repliki na węzłach wpływ hello ponieważ spowodowałoby to naruszenie ograniczenia koligacji hello. Więcej informacji o koligacji jest [w tym artykule](service-fabric-cluster-resource-manager-advanced-placement-rules-affinity.md)
* **FaultDomain** i **UpgradeDomain**: to ograniczenie eliminuje węzłów, jeżeli wprowadzanie repliki hello na powitania węzłów spowodowałoby pakowania w domenie uaktualnienia lub określonego błędu. Kilka przykładów dyskutować tego ograniczenia są przedstawione w temacie hello na [ograniczenia domeny awarii i uaktualniania i efekty](service-fabric-cluster-resource-manager-cluster-description.md)
* **PreferredLocation**: zwykle niepowołanymi to ograniczenie usuwania węzłów z hello rozwiązania, ponieważ jest on optymalizacji domyślnie. Witaj preferowane ograniczenia lokalizacji jest również obecny podczas uaktualniania. Podczas uaktualniania jest używane toomove usług wstecz toowhere zainstalowanych przy uruchamianiu hello uaktualnienia.

## <a name="blocklisting-nodes"></a>Węzły Blocklisting
Inny kondycji wiadomość hello Menedżera zasobów klastra raportów jest w przypadku węzły są blocklisted. Blocklisting można traktować jako tymczasowe ograniczenie, które zostanie automatycznie zastosowana dla Ciebie. Węzły Pobierz blocklisted po wystąpieniu błędów wielokrotnego podczas uruchamiania wystąpienia danego typu usługi. Węzły są blocklisted na podstawie na — typ usługi. Węzeł może być blocklisted dla typu w jednej usłudze, ale nie inna. 

Zobaczysz blocklisting zaczną działać często podczas tworzenia: niektóre usterki powoduje, że Twoje toocrash hosta usługi podczas uruchamiania. Sieć szkieletowa usług próbuje hosta usługi hello toocreate kilka razy, a hello błąd będzie się powtarzał. Mimo kilku prób węzła hello pobiera blocklisted i hello Menedżera zasobów klastra zostanie ponowiona w innym miejscu toocreate hello usługi. Jeśli błąd ten problem będzie nadal występować na wielu węzłach, prawdopodobnie zablokowany przez wszystkie węzły prawidłowy hello w końcu klastra hello w górę. Blocklisting można również usunąć tak wiele węzłów, że nie ma wystarczającej ilości pomyślnie uruchomić hello usługi toomeet hello potrzeby skalowania. Zwykle zobaczysz dodatkowe błędy lub ostrzeżenia hello Menedżera zasobów klastra wskazujący, że usługa hello poniżej hello żądanej repliki lub liczba wystąpień, jak również wiadomości kondycji informujący o niepowodzeniu jakie hello jest która prowadzi toohello blocklisting w miejscu pierwszego hello.

Blocklisting nie jest trwały warunek. Po kilku minutach hello węzeł zostanie usunięty z hello blocklist i sieci szkieletowej usług ponownie uaktywnić hello usług w tym węźle. Usług kontynuowania toofail węzeł hello jest ponownie blocklisted dla danego typu usługi. 

### <a name="constraint-priorities"></a>Ograniczenie priorytetów

> [!WARNING]
> Zmiana ograniczenia priorytetów nie jest zalecane i może mieć negatywnego wpływu na klastrze. Witaj poniżej informacji podano do hello domyślne ograniczenia priorytety i ich zachowanie. 
>

Biorąc pod uwagę następujące ograniczenia możesz może mieć zostały myśląc "Witaj — myślę, że ograniczenia domeny błędów są hello najważniejsze w systemie. W kolejności tooensure hello ograniczenia domeny błędów nie jest naruszone, jestem gotowi tooviolate inne ograniczenia. "

Ograniczenia można skonfigurować za pomocą różnych poziomów priorytetu. Są to:

   - "twardych" (0)
   - "soft" (1)
   - "optymalizacji" [2]
   - "off" (-1). 
   
Większość ograniczenia hello są domyślnie skonfigurowane jako twardych ograniczeń.

Zmiana priorytetu hello ograniczeń jest rzadko. Było razy, gdy ograniczenia priorytetów potrzebne toochange, zwykle toowork wokół inne usterki lub zachowanie wpływał hello środowiska. Zazwyczaj bardzo dobrze działa elastyczność hello hello ograniczenia priorytet infrastruktury, ale nie jest często potrzebne. W większości przypadków hello wszystko, co znajduje się w ich priorytety domyślnych. 

poziomy priorytetu Hello nie oznaczają, że dany ograniczenia _będzie_ naruszone, ani zawsze będą spełnione. Ograniczenie priorytetów określić kolejność, w którym wymuszone są ograniczenia. Priorytety zdefiniować wady i zalety hello podczas jest niemożliwe toosatisfy wszystkie ograniczenia. Zwykle wszystkie ograniczenia hello można spełnić, chyba że coś else dzieje się w środowisku hello jest. Przykładowe scenariusze, które spowoduje naruszeń tooconstraint to powodujące konflikt ograniczenia lub dużą liczbą jednoczesnych awarii.

W sytuacjach, zaawansowane można zmienić priorytety ograniczenia hello. Na przykład, że użytkownik chciał tooensure czy koligacji zostałyby zawsze naruszone gdy wysyła niezbędne toosolve pojemność węzła. tooachieve, można ustawić priorytet hello hello koligacji ograniczenia zbyt słowo "soft" (1) i pozostawić hello pojemności ograniczający ustawiony za "bardzo" (0).

Hello domyślne wartości priorytetu różnych ograniczeń hello są określone w hello następującej konfiguracji:

ClusterManifest.xml

```xml
        <Section Name="PlacementAndLoadBalancing">
            <Parameter Name="PlacementConstraintPriority" Value="0" />
            <Parameter Name="CapacityConstraintPriority" Value="0" />
            <Parameter Name="AffinityConstraintPriority" Value="0" />
            <Parameter Name="FaultDomainConstraintPriority" Value="0" />
            <Parameter Name="UpgradeDomainConstraintPriority" Value="1" />
            <Parameter Name="PreferredLocationConstraintPriority" Value="2" />
        </Section>
```

za pomocą pliku ClusterConfig.json dla autonomicznych wdrożeniach lub Template.json dla platformy Azure hostowanej klastrów:

```json
"fabricSettings": [
  {
    "name": "PlacementAndLoadBalancing",
    "parameters": [
      {
          "name": "PlacementConstraintPriority",
          "value": "0"
      },
      {
          "name": "CapacityConstraintPriority",
          "value": "0"
      },
      {
          "name": "AffinityConstraintPriority",
          "value": "0"
      },
      {
          "name": "FaultDomainConstraintPriority",
          "value": "0"
      },
      {
          "name": "UpgradeDomainConstraintPriority",
          "value": "1"
      },
      {
          "name": "PreferredLocationConstraintPriority",
          "value": "2"
      }
    ]
  }
]
```

## <a name="fault-domain-and-upgrade-domain-constraints"></a>Błąd ograniczenia domeny domeny i uaktualnienia
Hello Menedżera zasobów klastra chce, aby rozłożyć między domenach awarii i uaktualniania usług tookeep. To jej modele jako ograniczenia wewnątrz aparatu Menedżera hello klastra zasobu. Aby uzyskać więcej informacji na temat sposobu ich używania i ich określone zachowanie, zapoznaj się artykułem hello na [konfiguracji klastra](service-fabric-cluster-resource-manager-cluster-description.md#fault-and-upgrade-domain-constraints-and-resulting-behavior).

Witaj Menedżera zasobów klastra może być konieczne toopack kilka replik w domenie uaktualnienia w toodeal kolejność uaktualnień, błędów lub innych naruszenia ograniczenia. Pakowanie w domenach awarii lub uaktualnienia zwykle odbywa się tylko wtedy, gdy istnieje kilka błędów lub innych zmian w systemie hello uniemożliwia poprawne umieszczania. W razie potrzeby tooprevent pakowania nawet w takich przypadkach mogą wykorzystywać hello `RequireDomainDistribution` [zasady rozmieszczania](service-fabric-cluster-resource-manager-advanced-placement-rules-placement-policies.md#requiring-replica-distribution-and-disallowing-packing). Należy pamiętać, może to mieć wpływ na dostępność usługi i niezawodność jako efekt uboczny, dlatego należy dokładnie należy rozważyć.

Jeśli środowisko hello jest skonfigurowane poprawnie, wszystkie ograniczenia są w pełni uwzględniona, nawet podczas uaktualniania. Witaj klucza się tym powitalne Menedżera zasobów klastra obserwuje się dla użytkownika ograniczenia. Po wykryciu naruszenia natychmiast zgłasza i próbuje toocorrect hello problem.

## <a name="hello-preferred-location-constraint"></a>ograniczenie lokalizacji Hello preferowane
ograniczenie PreferredLocation Hello jest nieco inny, ponieważ składa się z dwóch różnych zastosowań. Jedno użycie to ograniczenie jest podczas uaktualniania aplikacji. Hello Cluster Resource Manager automatycznie zarządza to ograniczenie podczas uaktualniania. Jest używana tooensure że w przypadku uaktualnienia są spełnione, że repliki zwracać tootheir lokalizacji początkowej. Witaj innego użytku hello PreferredLocation ograniczenie dotyczy hello [ `PreferredPrimaryDomain` zasady rozmieszczania](service-fabric-cluster-resource-manager-advanced-placement-rules-placement-policies.md). Oba te optymalizacje, i dlatego hello ograniczenia PreferredLocation hello ograniczenie tylko ustawić także "Optymalizacji" domyślnie.

## <a name="upgrades"></a>Uaktualnienia
pomaga również Hello Menedżera zasobów klastra podczas aplikacji i uaktualnienia klastra, w których ma dwa zadania:

* Upewnij się, że reguły hello hello klastra nie są uszkodzone
* Spróbuj go uaktualnienia hello toohelp sprawnie

### <a name="keep-enforcing-hello-rules"></a>Zachowaj wymuszania reguł hello
świadomość toobe główny element Hello jest czy hello reguły — Witaj ograniczenia strict jak ograniczenia dotyczące umieszczania i pojemności - nadal są wymuszane podczas uaktualniania. Ograniczenia dotyczące umieszczania upewnij się, że obciążeń tylko uruchomiony, gdy mogą one, nawet podczas uaktualniania. Gdy usługi są bardzo ograniczone, uaktualnienia może trwać dłużej. Gdy usługa hello lub hello węzła, który jest uruchomiony na jest obniżył aktualizacji może być kilka opcji, których można go.

### <a name="smart-replacements"></a>Zamienianie inteligentne
Po uruchomieniu uaktualniania hello Resource Manager tworzy migawkę bieżącego rozmieszczenia hello hello klastra. Zgodnie z każdej domeny uaktualnienia zakończeniu podejmie tooreturn hello usług, które znajdowały się w tej domeny uaktualnienia tootheir oryginalny układ. W ten sposób jest co najwyżej dwa przejścia usługi podczas uaktualniania hello. Przenieś jednego węzła hello, których dotyczy problem, a jeden przenieść z powrotem. Zwracanie toohow klastra lub usługi hello przed uaktualnienia hello gwarantuje również uaktualnienie hello bez wpływu na układ hello hello klastra. 

### <a name="reduced-churn"></a>Postęp dokonany w obniżonej
Innym czynnikiem, która jest wywoływana podczas uaktualniania jest tego powitalne wyłącza równoważenia Menedżera zasobów klastra. Zapobieganie równoważenia zapobiega uaktualnienia toohello niepotrzebne reakcji, takich jak przeniesienie usług w węzłach, które zostały opróżnione do uaktualnienia hello. Uaktualnienie hello w przypadku uaktualniania klastra hello całego klastra nie jest rozmieszczana podczas uaktualniania hello. Ograniczenia kontroli pozostają aktywne, tylko przepływu oparte na powitania aktywnego równoważenie metryki jest wyłączona.

### <a name="buffered-capacity--upgrade"></a>Pojemność buforowanego & uaktualnienia
Zwykle ma toocomplete uaktualnienia hello nawet, jeśli klaster hello jest ograniczone lub zamknij toofull. Zarządzanie pojemności hello klastra hello jest szczególnie ważne podczas uaktualniania niż zwykle. W zależności od hello liczba domen uaktualnienia od 5 do 20% pojemności muszą być migrowane jako hello uaktualnienia przedstawia za pośrednictwem hello klastra. Pracy ma miejsce toogo. Gdzie jest to hello pojęcie [buforowane możliwości](service-fabric-cluster-resource-manager-cluster-description.md#buffered-capacity) jest użyteczne. Pojemność buforowany jest wzięty pod uwagę podczas normalnego działania. Witaj Menedżera zasobów klastra mogą wypełnić węzłów w zapasowej całkowita pojemność tootheir (Korzystanie z buforu hello) podczas uaktualniania, jeśli to konieczne.

## <a name="next-steps"></a>Następne kroki
* Rozpocznij od początku hello i [uzyskać toohello wprowadzenie zasobu klastra sieci szkieletowej programu Service Manager](service-fabric-cluster-resource-manager-introduction.md)
