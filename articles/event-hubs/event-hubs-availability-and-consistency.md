---
title: "aaaAvailability i spójność Azure Event Hubs | Dokumentacja firmy Microsoft"
description: "Jak partycje tooprovide hello maksymalną ilość dostępności i spójności z przy użyciu usługi Azure Event Hubs."
services: event-hubs
documentationcenter: na
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 8f3637a1-bbd7-481e-be49-b3adf9510ba1
ms.service: event-hubs
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/15/2017
ms.author: sethm
ms.openlocfilehash: a8ededaae1589830da21cb8910ca694d2d628bd2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="availability-and-consistency-in-event-hubs"></a>Dostępność i spójności w usłudze Event Hubs

## <a name="overview"></a>Omówienie
Usługa Azure Event Hubs używa [partycjonowania modelu](event-hubs-features.md#partitions) tooimprove dostępności i paralelizacja w obrębie jednego zdarzenia koncentratora. Na przykład jeśli Centrum zdarzeń zawiera cztery partycje, a jeden z tych partycji jest przenoszone z jednego serwera tooanother w operacji z równoważeniem obciążenia, użytkownik może nadal wysyłania i odbierania z trzech innych partycji. Ponadto posiadanie więcej partycji umożliwia toohave więcej jednoczesnych czytników przetwarzania danych, poprawy z łącznej przepływności. Opis skutków hello partycjonowanie i kolejność w rozproszonym systemie jest krytyczne aspektów projektu rozwiązania.

toohelp wyjaśnić hello kompromis między porządkowania i dostępności, zobacz hello [Newtona zakończenia](https://en.wikipedia.org/wiki/CAP_theorem), znanej również jako Newtona Brewera firmy. Ta Newtona omówiono hello wybór między spójności, dostępności i tolerancję partycji.

Newtona firmy Brewera definiuje spójności i dostępności w następujący sposób:
* Partycji tolerancji: hello możliwości toocontinue systemu przetwarzania danych, przetwarzanie danych, nawet jeśli wystąpi błąd partycji.
* Dostępność: węzłem z systemem innym niż niepowodzenie zwraca odpowiedź uzasadnione w rozsądnym czasie (z nie błędów lub przekroczenia limitu czasu).
* Spójności: odczytu jest gwarantowana tooreturn hello ostatniego zapisu dla danego klienta.

## <a name="partition-tolerance"></a>Tolerancja partycji
Centra zdarzeń jest oparty na modelu danych podzielonej na partycje. Witaj liczby partycji w Centrum zdarzeń można skonfigurować podczas instalacji, ale nie można później zmienić tę wartość. Ponieważ partycje musi korzystać z usługą Event Hubs, masz toomake decyzji o dostępności i spójności aplikacji.

## <a name="availability"></a>Dostępność
Hello najprostszy sposób tooget wprowadzenie do usługi Event Hubs jest toouse hello domyślne zachowanie. Jeśli tworzysz nową `EventHubClient` obiektu i użyj hello `Send` metody zdarzeń są automatycznie dystrybuowane między partycji w Centrum zdarzeń. Takie zachowanie umożliwia hello największą ilość czasu.

Dla przypadków użycia, które wymagają hello maksymalny czas działania ten model jest preferowany.

## <a name="consistency"></a>Spójność
W niektórych scenariuszach hello uporządkowania zdarzeń może być istotne. Na przykład można tooprocess Twojego systemu zaplecza polecenie aktualizacji przed polecenia delete. W takim przypadku można ustawić klucz partycji hello na zdarzenie, lub użyj `PartitionSender` tooonly obiektu wysyłania zdarzeń tooa partycji. Daje to gwarancję, że gdy zdarzenia te są odczytywane z hello partycji, są one odczytu w kolejności.

W tej konfiguracji należy pamiętać, że jeśli hello toowhich określonej partycji, który jest wysyłany jest niedostępny, zostanie wyświetlony błąd odpowiedzi. Jako punkt odniesienia Jeśli nie masz jednej partycji tooa koligacji hello usługi Event Hubs wysyła zdarzenia toohello dalej partycja dostępne.

Jeden tooensure możliwe rozwiązanie porządkowanie zwiększają również czasu, będzie tooaggregate zdarzenia w ramach wydarzenia przetwarzania aplikacji. Najprostszym sposobem tooaccomplish Witaj, to jest zdarzenie z właściwością numer sekwencji niestandardowych toostamp. przykład Hello następującego kodu:

```csharp
// Get hello latest sequence number from your application
var sequenceNumber = GetNextSequenceNumber();
// Create a new EventData object by encoding a string as a byte array
var data = new EventData(Encoding.UTF8.GetBytes("This is my message..."));
// Set a custom sequence number property
data.Properties.Add("SequenceNumber", sequenceNumber);
// Send single message async
await eventHubClient.SendAsync(data);
```

W tym przykładzie wysyła tooone Twojego zdarzeń hello dostępnych partycji w Centrum zdarzeń i ustawia jej numer sekwencji hello z aplikacji. To rozwiązanie wymaga toobe stanu zachowana przez aplikację przetwarzania, ale zapewnia Twojej nadawców punktu końcowego, który jest bardziej prawdopodobne toobe dostępne.

## <a name="next-steps"></a>Następne kroki
Więcej informacji na temat usługi Event Hubs można poznać, przechodząc na stronę hello następującego łącza:

* [Omówienie usługi Event Hubs usługi](event-hubs-what-is-event-hubs.md)
* [Tworzenie centrum zdarzeń](event-hubs-create.md)
