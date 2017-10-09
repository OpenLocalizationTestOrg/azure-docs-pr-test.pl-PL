---
title: "aaaDefragmentation metryki w sieci szkieletowej usług Azure | Dokumentacja firmy Microsoft"
description: "Omówienie przy użyciu defragmentacji lub pakowania jako strategię metryki w sieci szkieletowej usług"
services: service-fabric
documentationcenter: .net
author: masnider
manager: timlt
editor: 
ms.assetid: e5ebfae5-c8f7-4d6c-9173-3e22a9730552
ms.service: Service-Fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/18/2017
ms.author: masnider
ms.openlocfilehash: d09045a6cf196d2771f1a0794637f4579d3eb96b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="defragmentation-of-metrics-and-load-in-service-fabric"></a>Defragmentacja metryki i obciążenia w sieci szkieletowej usług
Strategia domyślne Hello usługi sieć szkieletowa klastra Menedżera zasobów do zarządzania metryki obciążenia w klastrze hello jest toodistribute hello obciążenia. Zapewnienie, że węzły są wykorzystywane równomiernie pozwala uniknąć gorącego i zimnych miejsc prowadzących rywalizacji tooboth i nieużywanego zasobów. Dystrybucji obciążeń w klastrze hello jest również hello najbezpieczniejszy pod względem pozostałych błędy, ponieważ gwarantuje, że błąd nie Wyjmij znaczną część danego obciążenia. 

Hello zasobu klastra sieci szkieletowej programu Service Manager obsługuje innych strategii zarządzania obciążenia, który jest defragmentacji. Defragmentacja oznacza, że zamiast w trakcie wykorzystania hello toodistribute metryki w klastrze hello, jego są konsolidowane. Konsolidacja jest po prostu odwracanie domyślne hello równoważenia strategii — zamiast minimalizując hello średni odchylenie standardowe metryki obciążenia, hello Menedżera zasobów klastra próbuje tooincrease go.

## <a name="when-toouse-defragmentation"></a>Gdy defragmentacji toouse
Dystrybucja obciążenia w klastrze hello zużywa niektórych zasobów hello w każdym węźle. Niektórych zadań tworzenia usług, które są wyjątkowo dużą i używać większości lub wszystkich węzła. W takich przypadkach jest to możliwe, że w przypadku dużych pobierania utworzone obciążeń, które nie ma wystarczającej ilości miejsca w toorun dowolnego węzła je. Duże obciążenia nie są problem w sieci szkieletowej usług; w tych przypadkach hello Cluster Resource Manager ustala, że potrzebuje tooreorganize hello klastra toomake miejsca na tym duże obciążenie. Jednak w hello międzyczasie aby obciążenie ma toobe toowait zaplanowane hello klastra.

Jeśli istnieje wiele usług i stan toomove wokół, jego może potrwać długo toobe duże obciążenie hello umieszczone w klastrze hello. Jest to bardziej prawdopodobne, jeśli inne obciążenia w klastrze hello są także duży i dlatego trwać dłużej tooreorganize. zespołu usługi sieć szkieletowa Hello mierzone czasy tworzenia w symulacji tego scenariusza. Znaleziono się, że tworzenie dużych usług trwało dłużej zaraz po wykorzystaniu klastra otrzymano powyżej od 30% do 50%. toohandle tego scenariusza, wprowadzono defragmentacji jako równoważenia strategii. Znaleziono się, że w przypadku dużych obciążeń, zwłaszcza tych, których czas utworzenia było ważne defragmentacji naprawdę pomocne te nowe obciążenia są planowane hello klastra.

Defragmentacja metryki toohave hello tooproactively Menedżera zasobów klastra spróbuj toocondense hello obciążenia hello usług można skonfigurować do mniej węzłów. Pomaga to zapewnić, że jest prawie zawsze miejsca dla dużych usług bez reorganizacja hello klastra. Nie ma tooreorganize hello klastra umożliwia szybkie tworzenie dużych obciążeń.

Defragmentacja nie ma potrzeby większości użytkowników. Usług są zwykle jest mały, więc nie twardych toofind miejsca dla nich w klastrze hello. Gdy reorganizacji jest możliwe, przechodzi ona szybko ponownie ponieważ większość usług są małe i mogą zostać przeniesione szybkie i równolegle. Jednak jeśli dużych usług i należy je szybko utworzyć hello strategii defragmentacji jest dla Ciebie. Omówiono wady i zalety korzystania defragmentacji obok hello. 

## <a name="defragmentation-tradeoffs"></a>Defragmentacja wady i zalety
Defragmentacji może zwiększyć impactfulness błędy, ponieważ w węzłach, które nie są uruchomione usługi więcej. Defragmentacja także może zwiększyć koszty, ponieważ zasobów w klastrze hello musi być przechowywany w rezerwy czeka na utworzenie hello dużych obciążeń.

Witaj poniższym diagramie zapewnia wizualną reprezentację dwa klastry, który defragmentacji i jedną, która nie jest. 

<center>
![Porównywanie zrównoważonym i defragmentacji klastrów][Image1]
</center>

W przypadku hello zrównoważonym należy wziąć pod uwagę liczbę hello przemieszczania, które mogą być niezbędne tooplace, jeden z największych obiektów usługi hello. W klastrze zdefragmentowanej hello hello duże obciążenie można umieścić w węzłach czterech lub pięciu bez konieczności toowait dla innych toomove usług.

## <a name="defragmentation-pros-and-cons"></a>Defragmentacja zalet i wad
Co to są tych pojęć kompromisy? Poniżej przedstawiono szybki spis toothink rzeczy, o:

| Specjaliści defragmentacji | Defragmentacja wad |
| --- | --- |
| Umożliwia szybsze tworzenie dużych usług |Koncentraty obciążenia na mniejszą liczbę węzłów, zwiększenie rywalizacji |
| Umożliwia obniżyć przenoszenia danych podczas tworzenia |Błędy może mieć wpływ na inne usługi i przenoszenie więcej |
| Umożliwia zaawansowane opis wymagań i odzyskiwanie miejsca |Bardziej złożonych konfiguracji ogólnej zarządzanie zasobami |

Można mieszać zdefragmentowanej i normalnym metryki w hello tego samego klastra. Witaj Menedżera zasobów klastra prób tooconsolidate hello defragmentacji metryki możliwie często podczas rozkładanie hello innych użytkowników. wyniki Hello mieszanie defragmentacji oraz równoważenia strategii zależy od kilka czynników, takich jak:
  - Liczba Hello równoważenia metryki a hello liczby metryk defragmentacji
  - Określa, czy usługi używa obu typów metryk 
  - metryki wag Hello
  - ładuje bieżący metryki
  
Eksperymenty jest wymagana toodetermine hello dokładnej konfiguracji niezbędne. Zalecamy dokładne pomiary obciążeń przed włączeniem metryki defragmentacji w środowisku produkcyjnym. Jest to szczególnie istotne, jeśli mieszanie defragmentacji i zrównoważonym metryki w hello tę samą usługę. 

## <a name="configuring-defragmentation-metrics"></a>Konfigurowanie metryki defragmentacji
Konfigurowanie metryki defragmentacji jest globalne decyzji w klastrze hello i do defragmentacji można wybrać poszczególnych metryki. powitania po konfiguracji wstawki pokazują, jak metryki tooconfigure defragmentacji. W takim przypadku "Metric1" jest skonfigurowana jako metrykę defragmentacji "Metric2" będzie nadal toobe zrównoważonym normalnie. 

ClusterManifest.xml:

```xml
<Section Name="DefragmentationMetrics">
    <Parameter Name="Metric1" Value="true" />
    <Parameter Name="Metric2" Value="false" />
</Section>
```

za pomocą pliku ClusterConfig.json dla autonomicznych wdrożeniach lub Template.json dla platformy Azure hostowanej klastrów:

```json
"fabricSettings": [
  {
    "name": "DefragmentationMetrics",
    "parameters": [
      {
          "name": "Metric1",
          "value": "true"
      },
      {
          "name": "Metric2",
          "value": "false"
      }
    ]
  }
]
```


## <a name="next-steps"></a>Następne kroki
- Hello Menedżera zasobów klastra ma opcje man opisujące hello klastra. toofind się więcej na ich temat, zapoznaj się w tym artykule na [opisujące klastra sieci szkieletowej usług](service-fabric-cluster-resource-manager-cluster-description.md)
- Metryki są zarządzaniu hello Menedżer zasobów klastra sieci szkieletowej usług konsumenckich i pojemności w klastrze hello. więcej informacji na temat metryki toolearn i jak tooconfigure, zapoznaj się z [w tym artykule](service-fabric-cluster-resource-manager-metrics.md)

[Image1]:./media/service-fabric-cluster-resource-manager-defragmentation-metrics/balancing-defrag-compared.png
