---
title: "aaaThrottling w Menedżerze zasobów klastra usługi sieć szkieletowa hello | Dokumentacja firmy Microsoft"
description: "Dowiedz się, limity hello tooconfigure podał hello zasobu klastra sieci szkieletowej programu Service Manager."
services: service-fabric
documentationcenter: .net
author: masnider
manager: timlt
editor: 
ms.assetid: 4a44678b-a5aa-4d30-958f-dc4332ebfb63
ms.service: Service-Fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/18/2017
ms.author: masnider
ms.openlocfilehash: f418536911d3e3814e78a4d9f057dfb867ca7c63
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="throttling-hello-service-fabric-cluster-resource-manager"></a>Ograniczanie hello zasobu klastra sieci szkieletowej programu Service Manager
Nawet jeśli hello Cluster Resource Manager został prawidłowo skonfigurowany, można pobrać zakłócona hello klastra. Na przykład może być jednocześnie węzła błędów domeny awarii i — co się stanie po, który wystąpił podczas uaktualniania? Hello Menedżera zasobów klastra zawsze próbuje toofix wszystko, korzysta z zasobów klastra hello próby tooreorganize i popraw hello klastra. Limity zapewniają backstop tak, aby klaster hello można używać zasobów toostabilize — węzły hello wrócić, partycje sieciowe hello poprawianego, wdrożony poprawiony usługi bits.

toohelp z tego rodzaju sytuacje, hello zasobu klastra sieci szkieletowej programu Service Manager obejmuje kilka limity. Te limity są wszystkie młotów dość duży. Zazwyczaj nie można zmienić bez zachować ostrożność podczas planowania i testowania.

Jeśli zmienisz limity Menedżera hello klastra zasobów możesz powinien dostroić ich tooyour oczekiwanego rzeczywiste obciążenie. Mogą określić potrzebne toohave niektóre ogranicza w miejscu, nawet w przypadku oznacza to, że klaster hello trwa dłużej toostabilize w niektórych sytuacjach. Testowanie jest wymagana toodetermine hello poprawne wartości dla limity. Limity muszą toobe wystarczająco duża tooallow hello klastra toorespond toochanges w rozsądnym czasie, a niski za mało tooactually zapobiec zużycie zbyt dużej ilości zasobów. 

W większości przypadków hello możemy w tym samouczku klientów za pomocą limity została ponieważ już zostały w środowisku ograniczonego zasobów. Przykłady będzie ograniczona przepustowość sieci dla poszczególnych węzłów lub dyski, które nie są wiele stanowe replik w stanie toobuild równoległych powodu toothroughput ograniczenia. Bez limity operacje można przeciąży tych zasobów, powodując toofail operacji lub powolne. W takich sytuacjach klienci używane limity i wiedziały, że rozszerzeniu hello ilość czasu zajmuje tooreach klastra hello stabilności. Klienci również Rozumiem, że ich może służyć do wykonywania w dolnym ogólną niezawodność, podczas gdy zostały one ograniczany.


## <a name="configuring-hello-throttles"></a>Konfigurowanie hello ogranicza

Sieć szkieletowa usług ma dwa mechanizmy ograniczania hello liczba przeniesień repliki. Hello domyślnego mechanizmu, które istniały przed usługi sieć szkieletowa 5.7 reprezentuje ograniczenie w postaci bezwzględną liczbę przenosi dozwolone. Nie działa w przypadku klastrów wszystkich rozmiarów. W szczególności w dużych klastrach hello domyślnych wartość może być za mały, znacznie spowolnieniem równoważenie nawet wtedy, gdy jest to konieczne, a jednocześnie ma efektu w mniejszych klastrów. Ten mechanizm uprzedniego została zastąpiona procentowych ograniczania przepustowości, która skaluje się lepiej z klastrami dynamicznych w numer hello usług i węzły regularne zmiany.

limity Hello są oparte na procent hello liczba replik w klastrach hello. Limity Percetage na podstawie włączyć określającej reguły hello: "nie przenoś więcej niż 10% replik w 10-minutowych interwałach", np.

ustawienia konfiguracji Hello procentowych ograniczania są:

  - GlobalMovementThrottleThresholdPercentage — maksymalna liczba przeniesień dozwolone w klastrze, w dowolnym momencie, wyrażony jako procent całkowitej liczby replik hello klastra. 0 oznacza brak limitu. Witaj, wartość domyślna to 0. Jeśli zostały określone zarówno tego ustawienia, jak i GlobalMovementThrottleThreshold, następnie hello więcej zachowawcze limit jest używany.
  - GlobalMovementThrottleThresholdPercentageForPlacement — maksymalna liczba przeniesień dozwolone w fazie umieszczania hello, wyrażony jako procent całkowitej liczby replik hello klastra. 0 oznacza brak limitu. Witaj, wartość domyślna to 0. Jeśli zostały określone zarówno tego ustawienia, jak i GlobalMovementThrottleThresholdForPlacement, następnie hello więcej zachowawcze limit jest używany.
  - GlobalMovementThrottleThresholdPercentageForBalancing — maksymalna liczba przeniesień dozwolone podczas hello równoważenia fazy, wyrażony jako procent całkowitej liczby replik w klastrze hello. 0 oznacza brak limitu. Witaj, wartość domyślna to 0. Jeśli zostały określone zarówno tego ustawienia, jak i GlobalMovementThrottleThresholdForBalancing, następnie hello więcej zachowawcze limit jest używany.

Podczas określania hello procent przepustowości, należy określić jako 0,05 5%. Interwał powitania zarządzane te limity jest hello GlobalMovementThrottleCountingInterval, która została określona w sekundach.


``` xml
<Section Name="PlacementAndLoadBalancing">
     <Parameter Name="GlobalMovementThrottleThresholdPercentage" Value="0" />
     <Parameter Name="GlobalMovementThrottleThresholdPercentageForPlacement" Value="0" />
     <Parameter Name="GlobalMovementThrottleThresholdPercentageForBalancing" Value="0" />
     <Parameter Name="GlobalMovementThrottleCountingInterval" Value="600" />
</Section>
```

za pomocą pliku ClusterConfig.json dla autonomicznych wdrożeniach lub Template.json dla platformy Azure hostowanej klastrów:

```json
"fabricSettings": [
  {
    "name": "PlacementAndLoadBalancing",
    "parameters": [
      {
          "name": "GlobalMovementThrottleThresholdPercentage",
          "value": "0.0"
      },
      {
          "name": "GlobalMovementThrottleThresholdPercentageForPlacement",
          "value": "0.0"
      },
      {
          "name": "GlobalMovementThrottleThresholdPercentageForBalancing",
          "value": "0.0"
      },
      {
          "name": "GlobalMovementThrottleCountingInterval",
          "value": "600"
      }
    ]
  }
]
```

### <a name="default-count-based-throttles"></a>Limity liczby na podstawie domyślnego
Te informacje są dostarczane w przypadku, gdy masz starszą klastrów lub nadal zachować te konfiguracje klastrów, ponieważ zostały uaktualnione. Ogólnie rzecz biorąc zaleca się, że te są zastępowane limity procentowych hello powyżej. Procentowych ograniczania przepustowości jest domyślnie wyłączona, te limity pozostają hello domyślne limity dla klastra, dopóki nie są wyłączone i zastąpione hello procentowych limity. 

  - GlobalMovementThrottleThreshold — to ustawienie określa hello łączna liczba przeniesień w klastrze hello trochę czasu. Witaj ilość czasu został określony w sekundach jako hello GlobalMovementThrottleCountingInterval. Wartość domyślna Hello hello GlobalMovementThrottleThreshold wynosi 1000, a wartość domyślna hello hello GlobalMovementThrottleCountingInterval to 600.
  - MovementPerPartitionThrottleThreshold — to ustawienie określa hello łączna liczba przeniesień do żadnej partycji usługi trochę czasu. Witaj ilość czasu został określony w sekundach jako hello MovementPerPartitionThrottleCountingInterval. Wartość domyślna Hello hello MovementPerPartitionThrottleThreshold to 50, a hello domyślna wartość dla hello MovementPerPartitionThrottleCountingInterval 600.

Konfiguracja Hello hello następujące limity, te same wzorca jako hello procentowych ograniczania.

## <a name="next-steps"></a>Następne kroki
- toofind limit o jak hello Menedżera zasobów klastra zarządza i równoważy obciążenie klastra hello wyewidencjonować hello artykułu na [równoważenia obciążenia](service-fabric-cluster-resource-manager-balancing.md)
- Witaj Menedżera zasobów klastra ma wiele opcji opisujące hello klastra. toofind się więcej na ich temat, zapoznaj się w tym artykule na [opisujące klastra sieci szkieletowej usług](service-fabric-cluster-resource-manager-cluster-description.md)
