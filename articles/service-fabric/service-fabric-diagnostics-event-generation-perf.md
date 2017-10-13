---
title: "Wydajność sieci szkieletowej Azure usługi monitorowania | Dokumentacja firmy Microsoft"
description: "Więcej informacji na temat liczników wydajności dla monitorowania i diagnostyki klastrów sieci szkieletowej usług Azure."
services: service-fabric
documentationcenter: .net
author: dkkapur
manager: timlt
editor: 
ms.assetid: 
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/30/2017
ms.author: dekapur
ms.openlocfilehash: 9d63148c182c705b6b49733c59ed8fdd13872d72
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="performance-metrics"></a>Metryki wydajności

Aby zrozumieć działanie klastra, a także aplikacji uruchomionych w niej powinny być gromadzone metryki. Dla klastrów sieci szkieletowej usług firma Microsoft zaleca zbieranie następujących liczników wydajności.

## <a name="nodes"></a>Węzły

Dla maszyn w klastrze należy wziąć pod uwagę następujące liczniki wydajności do lepszego zrozumienia obciążenia na każdej maszynie i wprowadzić odpowiednie klastra skalowanie decyzje dotyczące zbierania.

| Kategoria licznika | Nazwa licznika |
| --- | --- |
| Dysk fizyczny (na dysku) | Średni Długość kolejki odczytu dysku |
| Dysk fizyczny (na dysku) | Średni Długość kolejki dysku zapisu |
| Dysk fizyczny (na dysku) | Średni Czas dysku w s/Odczyt |
| Dysk fizyczny (na dysku) | Średni Dysku w s/Zapis |
| Dysk fizyczny (na dysku) | Odczyty dysku/s |
| Dysk fizyczny (na dysku) | Bajty odczytu dysku/s |
| Dysk fizyczny (na dysku) | Zapisy dysku/s |
| Dysk fizyczny (na dysku) | Bajty zapisu dysku/s |
| Memory (Pamięć) | Dostępna pamięć (MB) |
| Plik stronicowania | % Użycia |
| Process(Total) | Czas procesora (%) |
| Proces (usługi) | Czas procesora (%) |
| Proces (usługi) | Identyfikator procesu |
| Proces (usługi) | Bajty prywatne |
| Proces (usługi) | Liczba wątków |
| Proces (usługi) | Licznik Bajty wirtualne |
| Proces (usługi) | Zestaw roboczy |
| Proces (usługi) | Zestaw roboczy — prywatny |

## <a name="net-applications-and-services"></a>Usługi i aplikacje środowiska .NET.

Zbierz następujące liczniki, Jeżeli wdrażasz usług .NET do klastra. 

| Kategoria licznika | Nazwa licznika |
| --- | --- |
| .NET CLR pamięci (dla usługi) | Identyfikator procesu |
| .NET CLR pamięci (dla usługi) | # Całkowita liczba Zadeklarowane bajty |
| .NET CLR pamięci (dla usługi) | # Całkowita liczba zastrzeżone bajtów |
| .NET CLR pamięci (dla usługi) | Liczba bajtów we wszystkich Stertach |
| .NET CLR pamięci (dla usługi) | # Kolekcje pokolenia 0 |
| .NET CLR pamięci (dla usługi) | # Kolekcje gen 1 |
| .NET CLR pamięci (dla usługi) | # Kolekcje gen 2 |
| .NET CLR pamięci (dla usługi) | % Czasu odzyskiwania pamięci |

### <a name="service-fabrics-custom-performance-counters"></a>Usługa sieć szkieletowa niestandardowe liczniki wydajności

Sieć szkieletowa usług generuje rozległe niestandardowe liczniki wydajności. Jeśli masz zainstalowany zestaw SDK, zostanie wyświetlona lista kompleksowe na komputerze z systemem Windows, w Monitorze wydajności aplikacji (Start > monitora wydajności). 

W aplikacjach wdrażasz do klastra, jeśli używasz Reliable Actors, Dodaj countes z `Service Fabric Actor` i `Service Fabric Actor Method` kategorii (zobacz [usługi sieć szkieletowa niezawodnej podmiotów diagnostyki](service-fabric-reliable-actors-diagnostics.md)).

Jeśli używasz usługi niezawodnego podobnie mamy `Service Fabric Service` i `Service Fabric Service Method` kategorii licznika, które należy zebrać liczników z. 

Użycie niezawodnej kolekcje, zaleca się dodawania `Avg. Transaction ms/Commit` z `Service Fabric Transactional Replicator` zbierać opóźnienie zatwierdzania średni na Metryka transakcji.


## <a name="next-steps"></a>Następne kroki

* Dowiedz się więcej o [generowania zdarzeń na poziomie platformy](service-fabric-diagnostics-event-generation-infra.md) w sieci szkieletowej usług
* Zbieranie metryk wydajności za pośrednictwem [diagnostyki Azure](service-fabric-diagnostics-event-aggregation-wad.md)
