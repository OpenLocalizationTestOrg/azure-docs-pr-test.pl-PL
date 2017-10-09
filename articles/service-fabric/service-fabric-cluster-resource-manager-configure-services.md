---
title: "Ustawienia metryki i umieszczania aaaSpecify w Azure mikrousług | Dokumentacja firmy Microsoft"
description: "Opisujące usługi Service Fabric, określając metryki, ograniczenia umieszczania i inne zasady umieszczania."
services: service-fabric
documentationcenter: .net
author: masnider
manager: timlt
editor: 
ms.assetid: 16e135c1-a00a-4c6f-9302-6651a090571a
ms.service: Service-Fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/18/2017
ms.author: masnider
ms.openlocfilehash: c633518b5dbf0c7b84e0d46c06bf1f92365d184d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="configuring-cluster-resource-manager-settings-for-service-fabric-services"></a>Konfigurowanie ustawień Menedżera zasobów klastra dla usługi sieci szkieletowej usług
Witaj zasobu klastra sieci szkieletowej programu Service Manager umożliwia precyzyjną kontrolę nad hello reguły, które kontrolują każdego użytkownika, nazwę usługi. Każda usługa o nazwie można określić zasady jak powinna zostać przydzielona w klastrze hello. Każda usługa o nazwie można również zdefiniować hello zbiór metryki chce tooreport, w tym, jak ważne są toothat usługi. Konfigurowanie usług dzieli na trzy różne zadania:

1. Konfigurowanie ograniczeń umieszczania
2. Konfigurowanie metryki
3. Konfigurowanie zasad umieszczania zaawansowane i innymi regułami (mniej typowe)

## <a name="placement-constraints"></a>Ograniczenia dotyczące umieszczania
Ograniczenia dotyczące umieszczania są używane toocontrol których węzłów w klastrze hello usługi faktycznie można uruchomić na. Zwykle określonego nazwane wystąpienie usługi lub wszystkich usług danego typu ograniczonego toorun na określony typ węzła. Ograniczenia dotyczące umieszczania są rozszerzalne. Można określić dowolny zbiór właściwości dla węzła typu, a następnie wybierz dla nich z ograniczeniami podczas tworzenia usługi. Można również zmienić ograniczenia umieszczania usług jest uruchomiona. Dzięki temu toochanges toorespond hello klastra lub wymagania hello hello usługi. w klastrze hello również można dynamicznie zaktualizować Hello właściwości danego węzła. Więcej informacji na temat ograniczeń umieszczania i jak tooconfigure ich znajduje się w [w tym artykule](service-fabric-cluster-resource-manager-cluster-description.md#node-properties-and-placement-constraints)

## <a name="metrics"></a>Metryki
Metryki są hello zestaw zasobów, które wymaga dana usługa o nazwie. Konfiguracja metryki usługi obejmuje ilość tego zasobu każdej repliki stanowego lub bezstanowego wystąpienie tej usługi wykorzystuje domyślnie. Metryki obejmują również wagi, która wskazuje, jak ważne jest, że metryki równoważenia jest toothat usługi, w przypadku, gdy niezbędne są wady i zalety.

## <a name="advanced-placement-rules"></a>Reguły umieszczania zaawansowane
Istnieją inne typy zasad umieszczania, które są przydatne w mniej typowych scenariuszy. Przykłady to:
- Ograniczenia, które pomagają w geograficznie rozproszonej klastrów
- Niektóre architektury aplikacji

Inne zasady umieszczania są skonfigurowane za pośrednictwem korelacji lub zasad.

## <a name="next-steps"></a>Następne kroki
- Metryki są zarządzaniu hello Menedżer zasobów klastra sieci szkieletowej usług konsumenckich i pojemności w klastrze hello. więcej informacji na temat metryki toolearn i jak tooconfigure, zapoznaj się z [w tym artykule](service-fabric-cluster-resource-manager-metrics.md)
- Koligacja jest jeden tryb, które można skonfigurować dla usług. Nie jest często, ale jeśli potrzebne informacje na temat jego [tutaj](service-fabric-cluster-resource-manager-advanced-placement-rules-affinity.md)
- Istnieje wiele reguł różnych umieszczania można skonfigurować na dodatkowych scenariuszy toohandle usługi. Można znaleźć informacje dotyczące tych zasad umieszczania różnych [tutaj](service-fabric-cluster-resource-manager-advanced-placement-rules-placement-policies.md)
- Rozpocznij od początku hello i [uzyskać toohello wprowadzenie zasobu klastra sieci szkieletowej programu Service Manager](service-fabric-cluster-resource-manager-introduction.md)
- toofind limit o jak hello Menedżera zasobów klastra zarządza i równoważy obciążenie klastra hello wyewidencjonować hello artykułu na [równoważenia obciążenia](service-fabric-cluster-resource-manager-balancing.md)
- Witaj Menedżera zasobów klastra ma wiele opcji opisujące hello klastra. toofind się więcej na ich temat, zapoznaj się w tym artykule na [opisujące klastra sieci szkieletowej usług](service-fabric-cluster-resource-manager-cluster-description.md)
