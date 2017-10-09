---
title: "aaaResource architektury Menedżera | Dokumentacja firmy Microsoft"
description: "Przegląd architektury programu usługi sieć szkieletowa klastra Menedżera zasobów."
services: service-fabric
documentationcenter: .net
author: masnider
manager: timlt
editor: 
ms.assetid: 6c4421f9-834b-450c-939f-1cb4ff456b9b
ms.service: Service-Fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/18/2017
ms.author: masnider
ms.openlocfilehash: 9ea80273d0566a2ac25143ada3662875656b57b8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="cluster-resource-manager-architecture-overview"></a>Przegląd architektury Menedżera zasobów klastra
Hello zasobu klastra sieci szkieletowej programu Service Manager jest usługą centralnej, która działa w klastrze hello. Zarządza hello żądany stan usług hello w klastrze hello, zwłaszcza w przypadku względem tooresource konsumenckich i wszystkie reguły umieszczania. 

toomanage hello zasobów w klastrze, hello Menedżera zasobów klastra sieci szkieletowej usług wymaga kilku informacji:

- Usługi, które obecnie istnieje.
- Każda usługa bieżącej (lub domyślna) zużycie zasobów 
- Witaj pozostałe zasoby klastra 
- pojemność Hello hello węzłów w klastrze hello 
- Witaj ilość zasobów używanych w każdym węźle

zużycie zasobów Hello danej usługi mogą ulec zmianie, a usługi zazwyczaj się o więcej niż jednego typu zasobu. W różnych usługach może być rzeczywistym fizyczne i fizyczne zasoby mierzony. Usługi mogą śledzić metryki fizycznych, takich jak użycie pamięci i dysku. Zazwyczaj usług mogą interesujących logicznej metryki - np. "WorkQueueDepth" lub "TotalRequests". Metryki zarówno logicznych, jak i fizycznych mogą być używane w hello tego samego klastra. Metryki mogą być współużytkowane przez wiele usług lub być określonych tooa określonej usługi.

## <a name="other-considerations"></a>Inne zagadnienia
Witaj właścicieli i operatory hello klastra może się różnić od hello autorów usług i aplikacji lub w są minimalne hello sam sobie Kapelusze innej osoby. Podczas opracowywania aplikacji znasz kilka rzeczy, o co wymaga. Jest to wartość szacowana z hello różnych usług i zasobów, które będą korzystać z jego powinny zostać wdrożone. Na przykład warstwa sieci web hello musi toorun na toohello węzłów widoczne Internet, podczas hello bazy danych usługi nie powinny. Inny przykład usługi sieci web hello prawdopodobnie są ograniczone przez procesor CPU i sieci, podczas hello danych warstwy usługi opieki więcej informacji na temat zużycia pamięci i dysku. Jednak osoba hello obsługi zdarzenia na żywo lokacji, dla tej usługi w środowisku produkcyjnym lub który zarządza usługi uaktualniania toohello ma toodo różne zadania i wymaga różnych narzędzi. 

Zarówno hello klastra, jak i usługi są dynamiczne:

- Hello liczby węzłów w klastrze hello można zwiększyć lub zmniejszyć
- Węzły o różnych rozmiarach i typy mogą pochodzić i przejść
- Usługi można utworzyć, usunąć i zmiany ich zasobem alokacji i reguły umieszczania
- Uaktualnienia lub innych operacji zarządzania można przywracać za pomocą klastra hello aplikacji hello na poziomach infrastruktury
- Błędy możliwe, w dowolnym momencie.

## <a name="cluster-resource-manager-components-and-data-flow"></a>Składniki Menedżera zasobów klastra i przepływu danych
Witaj Menedżera zasobów klastra ma wymagania hello tootrack poszczególnych usług i hello zużycia zasobów przez każdy z obiektów usługi w tych usług. Hello Menedżera zasobów klastra ma dwie części koncepcyjnego: agentów uruchomionych na każdym węźle i usługą odpornej na uszkodzenia. agenci Hello na każdy węzeł Śledź obciążenia raporty z usług, łączny je i okresowo Raportuj je. Hello usługi Menedżer zasobów klastra agreguje wszystkie informacje hello czynnikami lokalne powitania i reaguje w zależności od bieżącej konfiguracji.

Przyjrzyjmy się powitania po diagramu:

<center>
![Architektura usługi równoważenia zasobów][Image1]
</center>

W czasie wykonywania istnieje wiele zmian, które mogą wystąpić. Na przykład, załóżmy, że ilość hello zasobów niektóre usługi zużywają zmiany, niektórych usług kończyć się niepowodzeniem i niektóre węzły join i pozostawić hello klastra. Wszystkie zmiany hello w węźle są agregowane i okresowo wysyłane toohello Menedżera zasobów klastra usługi (1,2) gdzie są agregowane ponownie, analizy i przechowywane. Co kilka sekund, które usługa sprawdza zmiany hello i określa, czy wszystkie akcje są niezbędne (3). Na przykład można zauważyć, że niektóre węzły pusty dodano toohello klastra. W związku z tym zdecyduje toomove niektóre węzły toothose usług. Hello Menedżera zasobów klastra można również Zwróć uwagę, czy określony węzeł jest przeciążony lub że pewnych usług ma nie powiodło się lub zostało usunięte, zwolnić zasoby w innym miejscu.

Załóżmy Spójrz na powitania po diagram i zobacz, co dalej. Załóżmy powiedz tego hello Menedżera zasobów klastra Określa, czy konieczne jest wprowadzenie zmian. Współrzędne go z innych usług (w szczególności hello menedżera trybu Failover) toomake hello niezbędne zmiany w systemie. Następnie hello niezbędne polecenia są wysyłane toohello odpowiednich węzłów (4). Na przykład załóżmy, że powitalne Resource Manager zauważyć, że Węzeł5 przeciążony i sie toomove usługi B z tooNode4 Węzeł5. Na końcu hello hello ponownej konfiguracji (5) hello klastra wygląda następująco:

<center>
![Architektura usługi równoważenia zasobów][Image2]
</center>

## <a name="next-steps"></a>Następne kroki
- Witaj Menedżera zasobów klastra ma wiele opcji opisujące hello klastra. toofind się więcej na ich temat, zapoznaj się w tym artykule na [opisujące klastra sieci szkieletowej usług](./service-fabric-cluster-resource-manager-cluster-description.md)
- Menedżer Hello klastra zasobu podstawowego obowiązki są ponowne równoważenie hello klastra i wymuszanie reguły umieszczania. Aby uzyskać więcej informacji na temat konfigurowania te zachowania, zobacz [równoważenia klastra sieci szkieletowej usług](./service-fabric-cluster-resource-manager-balancing.md)

[Image1]:./media/service-fabric-cluster-resource-manager-architecture/Service-Fabric-Resource-Manager-Architecture-Activity-1.png
[Image2]:./media/service-fabric-cluster-resource-manager-architecture/Service-Fabric-Resource-Manager-Architecture-Activity-2.png
