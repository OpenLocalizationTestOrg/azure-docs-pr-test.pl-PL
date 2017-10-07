---
title: "aaaDefinine i zarządzania stanem w programie Azure mikrousług | Dokumentacja firmy Microsoft"
description: "Jak toodefine i zarządzanie stanem usługi w sieci szkieletowej usług"
services: service-fabric
documentationcenter: .net
author: masnider
manager: timlt
editor: 
ms.assetid: f5e618a5-3ea3-4404-94af-122278f91652
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/18/2017
ms.author: masnider
ms.openlocfilehash: 4a24696da71753d0f343a86df3556b5b7c964834
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="service-state"></a>Stan usługi
**Usługa stanu** odwołuje się toohello w pamięci lub na dysku danych, że usługa wymaga toofunction. Obejmuje on, na przykład struktur danych hello zmienne Członkowskie usługi hello odczytuje i zapisuje toodo pracy. W zależności od tego, jak usługa hello została zaprojektowana on może również obejmować plików lub innych zasobów, które są przechowywane na dysku. Na przykład hello pliki bazy danych użyje toostore danych i dzienników transakcji.

Jako przykład usługi zastanówmy Kalkulator. Kalkulator podstawowe usługi ma dwie liczby i zwraca ich sumę. Wykonywanie tego obliczenia pociąga za sobą żadnych zmiennych Członkowskich lub inne informacje.

Teraz Rozważmy hello tego samego Kalkulator, ale z dodatkową metodę przechowywania i zwracanie hello ostatniego suma jest obliczana. Ta usługa jest teraz stanowych. Wartość oznacza, że zawiera niektóre stan, który zapisuje toowhen oblicza sumę nowe i odczytuje z podczas poproś tooreturn hello ostatniego obliczona sum.

Sieć szkieletowa usług Azure hello pierwszej usługi nosi usługę bezstanową. Usługa drugi Hello jest nazywany usługi stanowej.

## <a name="storing-service-state"></a>Przechowywanie stanu usługi
Stan można externalized lub wspólnie z kodem hello, który jest manipulowanie hello stanu. Externalization stan jest zazwyczaj wykonywane za pomocą zewnętrznej bazy danych lub innych danych przechowywania, że działa na różnych komputerach za pośrednictwem sieci hello lub pozaprocesowa na hello tym samym komputerze. W naszym przykładzie Kalkulator magazynu danych hello można bazy danych SQL lub wystąpienie magazynu tabel Azure. Suma hello toocompute każdego żądania przeprowadzi aktualizację na tych danych i żądań toohello usługi tooreturn hello wartość doprowadzi do bieżącej wartości hello są pobierane z magazynu hello. 

Stan można także wspólnie z hello obsługujące hello stanu. Stanowych usług w sieci szkieletowej usług są zazwyczaj tworzone przy użyciu tego modelu. Usługa Service Fabric realizuje hello tooensure infrastruktury, że ten stan jest wysoko dostępnych, spójne i trwałe i że usługi hello wbudowane w ten sposób można łatwo skalować.

## <a name="next-steps"></a>Następne kroki
Aby uzyskać więcej informacji dotyczących pojęć sieci szkieletowej usług zobacz następujące artykuły hello:

* [Dostępność usług sieci szkieletowej usług](service-fabric-availability-services.md)
* [Skalowalność usługi sieci szkieletowej usług](service-fabric-concepts-scalability.md)
* [Partycjonowanie usług sieci szkieletowej usług](service-fabric-concepts-partitioning.md)
* [Niezawodne usługi sieci szkieletowej usług](service-fabric-reliable-services-introduction.md)
