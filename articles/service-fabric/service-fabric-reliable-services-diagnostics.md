---
title: "aaaStateful diagnostyki niezawodne usługi | Dokumentacja firmy Microsoft"
description: "Funkcja diagnostyki dla stanowych usług Reliable Services"
services: service-fabric
documentationcenter: .net
author: dkkapur
manager: timlt
editor: 
ms.assetid: ae0e8f99-69ab-4d45-896d-1fa80ed45659
ms.service: Service-Fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/30/2017
ms.author: dekapur
ms.openlocfilehash: 6200800b858957c06039d9af062633b12a446318
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="diagnostic-functionality-for-stateful-reliable-services"></a>Funkcja diagnostyki dla stanowych usług Reliable Services
emituje Hello klasy Stateful niezawodnej usługi StatefulServiceBase [EventSource](https://msdn.microsoft.com/library/system.diagnostics.tracing.eventsource.aspx) zdarzenia, które mogą być używane toodebug hello usługi, zapewniają wgląd w sposób działania środowiska uruchomieniowego hello oraz pomóc w rozwiązywaniu problemów.

## <a name="eventsource-events"></a>Element EventSource zdarzenia
Nazwa źródła zdarzeń Hello hello Stateful niezawodnej usługi StatefulServiceBase klasy jest "Microsoft-ServiceFabric-Services". Zdarzenia z źródłem tego zdarzenia wyświetlane w [zdarzenia diagnostyczne](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md#view-service-fabric-system-events-in-visual-studio) okna, gdy usługa hello jest [debugowania w programie Visual Studio](service-fabric-debugging-your-application.md).

Narzędzia i technologie, które pomagają w zbierania i/lub wyświetlanie zdarzeń EventSource przykłady [narzędzia PerfView](http://www.microsoft.com/download/details.aspx?id=28567), [Microsoft Azure Diagnostics](../cloud-services/cloud-services-dotnet-diagnostics.md)i [Microsoft TraceEvent Library](http://www.nuget.org/packages/Microsoft.Diagnostics.Tracing.TraceEvent).

## <a name="events"></a>Zdarzenia
| Nazwa zdarzenia | Identyfikator zdarzenia | Poziom | Opis zdarzenia |
| --- | --- | --- | --- |
| StatefulRunAsyncInvocation |1 |Informacyjny |Wysyłanego po uruchomieniu zadania RunAsync usługi |
| StatefulRunAsyncCancellation |2 |Informacyjny |Podczas zadania RunAsync usługi zostało anulowane. |
| StatefulRunAsyncCompletion |3 |Informacyjny |Podczas wykonania zadania RunAsync usługi |
| StatefulRunAsyncSlowCancellation |4 |Ostrzeżenie |Podczas zadania RunAsync usługi trwa zbyt długo toocomplete anulowania |
| StatefulRunAsyncFailure |5 |Błąd |Podczas zadania RunAsync usługi zgłasza wyjątek |

## <a name="interpret-events"></a>Interpretowanie zdarzenia
Zdarzenia StatefulRunAsyncInvocation, StatefulRunAsyncCompletion i StatefulRunAsyncCancellation są przydatne toohello usługi składnika zapisywania toounderstand hello cyklem życia usługi —, a także chronometraż hello gdy usługa została uruchomiona, anulowane lub zakończone . Może to być przydatne podczas debugowania problemów dotyczących usługi lub cyklu życia usług hello opis.

Moduły zapisujące usługi zwrócić szczególną uwagę tooStatefulRunAsyncSlowCancellation i zdarzenia StatefulRunAsyncFailure ponieważ one wskazują na problemy z usługą hello.

StatefulRunAsyncFailure jest emitowany zawsze, gdy zadanie RunAsync() usługi hello zgłasza wyjątek. Zazwyczaj zgłoszono wyjątek wskazuje błąd lub usterkę w hello usługi. Ponadto wyjątek hello powoduje, że hello toofail usługi, dzięki czemu tooa przeniesiony na inny węzeł. Może to być kosztowna operacja i może opóźnić żądań przychodzących podczas przenoszenia hello usługi. Moduły zapisujące usługi należy ustalić przyczynę hello hello wyjątków i go w miarę możliwości unikać.

StatefulRunAsyncSlowCancellation jest emitowany zawsze, gdy żądanie anulowania zadania RunAsync hello trwa dłużej niż cztery sekund. Usługi trwa zbyt długo toocomplete anulowania, wpływa na możliwość hello toobe usługi hello szybko ponownie uruchomiona w innym węźle. Może to mieć wpływ hello ogólnej dostępności usługi hello.

## <a name="next-steps"></a>Następne kroki
* [Element EventSource dostawców w narzędzia PerfView](https://blogs.msdn.microsoft.com/vancem/2012/07/09/introduction-tutorial-logging-etw-events-in-c-system-diagnostics-tracing-eventsource/)
