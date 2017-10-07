---
title: "Centrum IoT wysokiej dostępności i odzyskiwania po awarii aaaAzure | Dokumentacja firmy Microsoft"
description: "Zawiera opis funkcji platformy Azure i Centrum IoT hello ułatwiające toobuild wysokiej dostępności rozwiązania Azure IoT o możliwości odzyskiwania po awarii."
services: iot-hub
documentationcenter: 
author: fsautomata
manager: timlt
editor: 
ms.assetid: ae320e58-aa20-45b9-abdc-fa4faae8e6dd
ms.service: iot-hub
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 11/16/2016
ms.author: elioda
ms.openlocfilehash: 74e1fa1682258819ffb3fd84eb79e42fc6e4120f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="iot-hub-high-availability-and-disaster-recovery"></a>Centrum IoT wysokiej dostępności i odzyskiwania po awarii
Jako usługi Azure IoT Hub zapewnia wysokiej dostępności (HA), za pomocą zwolnienia na poziomie hello region platformy Azure, bez konieczności wykonywania dodatkowych działań, wymagany przez rozwiązanie hello. platformy Microsoft Azure Hello także toohelp funkcje tworzenia rozwiązań z możliwości odzyskiwanie po awarii lub dostępności między regionu. Chcąc tooprovide globalnych, region między wysoką dostępność dla urządzeń lub użytkowników, projektowania i przygotowanie rozwiązań tootake korzystać z tych funkcji Azure odzyskiwania po awarii. Artykuł Hello [wskazówki techniczne ciągłości biznesowej Azure](../resiliency/resiliency-technical-guidance.md) opisuje hello wbudowanych funkcji na platformie Azure ciągłość prowadzenia działalności biznesowej i odzyskiwania po awarii. Witaj [odzyskiwania po awarii i wysoką dostępność aplikacji Azure] [ Disaster recovery and high availability for Azure applications] papieru znajdują się wskazówki dotyczące architektury dotyczące strategii tooachieve aplikacji Azure wysokiej dostępności i odzyskiwania po awarii.

## <a name="azure-iot-hub-dr"></a>DR Centrum IoT Azure
Ponadto HA toointra region Centrum IoT implementuje mechanizmów pracy awaryjnej dla odzyskiwania po awarii, które wymagają interwencji użytkownika hello. DR Centrum IoT własnym jest inicjowane i ma celu czasu odzyskiwania (RTO), 2-26 godzin i hello następujących celów punktu odzyskiwania (RPO).

| Funkcjonalność | CEL PUNKTU ODZYSKIWANIA |
| --- | --- |
| Dostępność usługi dla operacji rejestru i komunikacji |Możliwa utrata CName |
| Danych tożsamości w rejestrze tożsamości |0 – 5 minutach utrata danych |
| Komunikaty z urządzenia do chmury |Wszystkie komunikaty nieprzeczytana zostaną utracone |
| Operacje monitorowania wiadomości |Wszystkie komunikaty nieprzeczytana zostaną utracone |
| Komunikaty chmury do urządzenia |0 – 5 minutach utrata danych |
| Kolejki opinii chmury do urządzenia |Wszystkie komunikaty nieprzeczytana zostaną utracone |

## <a name="regional-failover-with-iot-hub"></a>Regionalne trybu failover z Centrum IoT
Zakończenie traktowania topologii wdrażania w rozwiązania IoT znajduje się poza hello zakres tego artykułu. Witaj omówiono hello *regionalnej pracy awaryjnej* modelu wdrażania hello w celu wysokiej dostępności i odzyskiwania po awarii.

W modelu regionalnej pracy awaryjnej hello rozwiązania wstecz końcowy uruchomień głównie w centrum danych w jednej lokalizacji, a dodatkowej Centrum IoT i zaplecza są wdrażane w innym miejscu centrum danych. Jeśli Centrum IoT hello w centrum danych głównej hello wystąpi awaria lub hello połączenia sieciowego z hello urządzenia toohello podstawowego centrum danych zostało przerwane. Urządzenia używają punkt końcowy usługi dodatkowej zawsze, gdy nie można nawiązać połączenia z bramą głównej hello. Dzięki możliwości trybu failover między regionu można zwiększyć dostępności rozwiązania hello poza hello wysokiej dostępności z jednego regionu.

Na wysokim poziomie tooimplement modelu regionalnej pracy awaryjnej z Centrum IoT należy hello następujące czynności:

* **Dodatkowej Centrum IoT i urządzenia routingu logiki**: W przypadku hello przerw w działaniu usługi w danym regionie podstawowym, urządzenia musi rozpoczynać się łączącego tooyour regionie pomocniczym. Biorąc pod uwagę hello obsługujący stanu rodzaj większość usług, jest typowe dla rozwiązania Administratorzy tootrigger hello trybu failover między region procesu. Hello najlepsze sposób toocommunicate hello nowego punktu końcowego toodevices, przy zachowaniu kontroli procesu hello jest ich regularne sprawdzanie toohave *Konsjerż* hello bieżącego aktywnego punktu końcowego usługi. Witaj Konsjerż usługi mogą być replikowane i przechowywane dostępny aplikacji sieci web przy użyciu technik przekierowania DNS (na przykład za pomocą [usługi Azure Traffic Manager][Azure Traffic Manager]).
* **Replikacja rejestru tożsamości** -toobe można używać, pomocniczego Centrum IoT hello musi zawierać wszystkie tożsamości urządzenia, które można połączyć rozwiązanie toohello. Hello rozwiązania należy zachować replikacją geograficzną kopii zapasowych tożsamości urządzenia i przekazać je toohello dodatkowej Centrum IoT przed przełączeniem hello aktywnego punktu końcowego dla urządzeń hello. Funkcja eksportu tożsamości urządzenia Hello Centrum IoT jest przydatne w tym kontekście. Aby uzyskać więcej informacji, zobacz [Centrum IoT — przewodnik dewelopera - rejestru tożsamości][IoT Hub developer guide - identity registry].
* **Scalanie logiki** — po regionu podstawowego hello znowu dostępne, wszystkie hello stan i dane, które zostały utworzone w lokacji dodatkowej hello musi być regionu podstawowego migrowanych toohello Wstecz. Ten stan i dane dotyczy przede wszystkim toodevice tożsamości i metadane aplikacji, które muszą zostać połączone z Centrum IoT głównej hello i innych magazynach specyficzne dla aplikacji w regionie podstawowym hello. toosimplify ten krok, należy użyć operacji idempotentności. Operacje idempotentności zminimalizować hello efekty uboczne hello ostatecznego spójne dystrybucję zdarzeń i duplikatów ani poza kolejnością dostarczania zdarzeń. Ponadto logiki aplikacji hello powinien być zaprojektowana tootolerate potencjalnych niespójności lub "nieco" Data-ze stanu. Taka sytuacja może wystąpić powodu toohello dodatkowe czasu potrzebnego dla systemu hello zbyt "poprawianego" oparta na celów punktu odzyskiwania (RPO).

## <a name="next-steps"></a>Następne kroki
Wykonaj te toolearn łącza więcej informacji na temat Centrum IoT Azure:

* [Rozpoczynanie pracy z centra IoT (samouczek)][lnk-get-started]
* [Co to jest Centrum IoT Azure?][What is Azure IoT Hub?]

[Disaster recovery and high availability for Azure applications]: ../resiliency/resiliency-disaster-recovery-high-availability-azure-applications.md
[Azure Business Continuity Technical Guidance]: https://azure.microsoft.com/documentation/articles/resiliency-technical-guidance/
[Azure Traffic Manager]: https://azure.microsoft.com/documentation/services/traffic-manager/
[IoT Hub developer guide - identity registry]: iot-hub-devguide-identity-registry.md

[lnk-get-started]: iot-hub-csharp-csharp-getstarted.md
[What is Azure IoT Hub?]: iot-hub-what-is-iot-hub.md
