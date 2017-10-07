---
title: "Monitorowanie wydajności sieci szkieletowej usług aaaAzure | Dokumentacja firmy Microsoft"
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
ms.openlocfilehash: 54d4c62b7250a1f70b0898ba07ae5a37716f4cf4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="performance-metrics"></a>Metryki wydajności

Metryki powinien toounderstand zebranych hello wydajności klastra można także aplikacji hello uruchomionych w niej. Dla klastrów sieci szkieletowej usług firma Microsoft zaleca zbieranie hello następujące liczniki wydajności.

## <a name="nodes"></a>Węzły

Witaj maszyn w klastrze należy wziąć pod uwagę zbieranie hello następujące liczniki wydajności toobetter zrozumieć hello obciążenia na każdej maszynie i wprowadzić odpowiednie klastra skalowanie decyzji.

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

Zbierz następujące liczniki wdrażania klastra tooyour usług .NET hello. 

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

Sieć szkieletowa usług generuje rozległe niestandardowe liczniki wydajności. Jeśli masz hello zainstalowany zestaw SDK, zostanie wyświetlona lista kompleksowe hello na komputerze z systemem Windows, w Monitorze wydajności aplikacji (Start > monitora wydajności). 

W aplikacji hello wdrażasz tooyour klastra, jeśli używasz Reliable Actors, Dodaj countes z `Service Fabric Actor` i `Service Fabric Actor Method` kategorii (zobacz [usługi sieć szkieletowa niezawodnej podmiotów diagnostyki](service-fabric-reliable-actors-diagnostics.md)).

Jeśli używasz usługi niezawodnego podobnie mamy `Service Fabric Service` i `Service Fabric Service Method` kategorii licznika, które należy zebrać liczników z. 

Jeśli używasz niezawodnej kolekcje, zaleca się dodawania hello `Avg. Transaction ms/Commit` z hello `Service Fabric Transactional Replicator` opóźnienie zatwierdzania średni hello toocollect na Metryka transakcji.


## <a name="next-steps"></a>Następne kroki

* Dowiedz się więcej o [generowania zdarzeń na poziomie platformy hello](service-fabric-diagnostics-event-generation-infra.md) w sieci szkieletowej usług
* Zbieranie metryk wydajności za pośrednictwem [diagnostyki Azure](service-fabric-diagnostics-event-aggregation-wad.md)
