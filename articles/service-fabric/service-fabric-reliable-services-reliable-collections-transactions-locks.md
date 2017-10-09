---
title: "aaaTransactions i tryby blokady w kolekcjach niezawodnej sieci szkieletowej usług Azure | Dokumentacja firmy Microsoft"
description: "Menedżer niezawodnej stanu sieci szkieletowej usługi Azure i transakcji niezawodnej kolekcje i blokowania."
services: service-fabric
documentationcenter: .net
author: mcoskun
manager: timlt
editor: masnider,rajak
ms.assetid: 62857523-604b-434e-bd1c-2141ea4b00d1
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: required
ms.date: 5/1/2017
ms.author: mcoskun
ms.openlocfilehash: 340e029aa98f43ad6e46b48f687dad01f9d96f69
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="transactions-and-lock-modes-in-azure-service-fabric-reliable-collections"></a>Transakcje i tryby blokady w kolekcjach niezawodnej sieci szkieletowej usług Azure

## <a name="transaction"></a>Transakcji
Sekwencja operacji wykonywanych jako pojedyncza jednostka logiczna pracy jest transakcja.
Transakcji musi mieć następujące właściwości ACID hello. (zobacz: https://technet.microsoft.com/en-us/library/ms190612)
* **Niepodzielność**: transakcji musi być Atomowej jednostki pracy. Innymi słowy wszystkie zmiany danych są wykonywane albo żadna z nich jest wykonywana.
* **Spójność**: po zakończeniu transakcji musi pozostać wszystkie dane w spójnym stanie. Wszystkie struktur danych wewnętrznych musi być prawidłowy na końcu hello hello transakcji.
* **Izolacja**: zmiany dokonane przez równoczesnych transakcji musi być odizolowany od hello zmiany dokonane przez równoczesnych transakcji. poziom izolacji Hello używane dla operacji w ramach ITransaction jest określana przez hello IReliableState zostanie wykonana operacja hello.
* **Trwałość**: po zakończeniu transakcji jego skutków są trwale w miejscu systemu hello. modyfikacje Hello utrwalić nawet w przypadku hello awarii systemu.

### <a name="isolation-levels"></a>Poziom izolacji
Stopień hello określa poziom izolacji transakcji hello toowhich musi być odizolowany od zmiany dokonane przez inne transakcje.
Istnieją dwa poziomy izolacji, które są obsługiwane w kolekcjach niezawodnej:

* **Odczyt powtarzalny**: Określa, że instrukcji nie można odczytać danych, które zostały zmodyfikowane, ale nie zostały jeszcze zatwierdzone przez inne transakcje i że żadne inne transakcje można modyfikować danych został odczytany przez hello bieżącej transakcji do bieżącego hello Zakończenie transakcji. Aby uzyskać więcej informacji, zobacz [https://msdn.microsoft.com/library/ms173763.aspx](https://msdn.microsoft.com/library/ms173763.aspx).
* **Migawki**: Określa, że dane odczytane przez żadnej instrukcji w transakcji jest spójna transakcyjnie wersji hello hello danych, które istniały na początku hello hello transakcji.
  Transakcja Hello może rozpoznawać tylko zmiany danych, które zostały zatwierdzone przed rozpoczęciem powitalne hello transakcji.
  Modyfikacje dane wprowadzane przez inne transakcje po hello początek hello bieżącej transakcji nie są widoczne toostatements wykonywania w bieżącej transakcji hello.
  efekt Hello jest tak, jakby instrukcje hello w transakcji migawki danych hello zatwierdzone znajdowały się na początku hello hello transakcji.
  Migawki są spójne w kolekcjach wiarygodne.
  Aby uzyskać więcej informacji, zobacz [https://msdn.microsoft.com/library/ms173763.aspx](https://msdn.microsoft.com/library/ms173763.aspx).

Kolekcje niezawodnej automatycznie wybrać hello toouse poziom izolacji dla danej operacji odczytu, w zależności od operacji hello i roli hello hello repliki bazy danych w czasie hello tworzenia transakcji.
Poniżej znajduje się hello tabeli, która przedstawia wartości domyślnych poziomu izolacji operacje słownika niezawodnych i kolejki.

| Operacja \ roli | Podstawowy | Pomocniczy |
| --- |:--- |:--- |
| Odczyt pojedynczej jednostki |Powtarzalnego odczytu |Snapshot |
| Wyliczenie, liczba |Snapshot |Snapshot |

> [!NOTE]
> Typowe przykłady dla jednej operacji jednostki `IReliableDictionary.TryGetValueAsync`, `IReliableQueue.TryPeekAsync`.
> 

Zarówno hello słownika niezawodnych i hello kolejka niezawodnych obsługuje zapisuje swój odczytu.
Innymi słowy, wszelkie zapisu w obrębie transakcji będą widoczne tooa następujące odczytywane należący toohello tej samej transakcji.

## <a name="locks"></a>Blokady
W kolekcjach niezawodnej wszystkie transakcje wdrożenie rygorystyczne dwie fazy blokowania: transakcji zwolnienia blokad hello ustawił aż do zakończenia hello transakcji z przerwania lub zatwierdzenia.

Słownik niezawodnej używa blokowania dla wszystkich operacji pojedynczy element na poziomie wiersza.
Kolejka niezawodnych zamienia poza współbieżności dla właściwości FIFO transakcyjnej strict.
Kolejka niezawodnych używa operacji blokad poziomu umożliwiające utworzenie jednej transakcji `TryPeekAsync` i/lub `TryDequeueAsync` i transakcja o `EnqueueAsync` naraz.
Należy pamiętać, że toopreserve FIFO, jeśli `TryPeekAsync` lub `TryDequeueAsync` kiedykolwiek przestrzega czy hello niezawodnej kolejka jest pusta, również spowoduje to zablokowanie `EnqueueAsync`.

Zawsze mieć blokady na wyłączność operacje zapisu.
Dla operacji odczytu hello blokowania zależy od kilka czynników.
Żadnej operacji odczytu wykonywane przy użyciu izolacji migawki jest nieblokującą.
Wszelkie operacje odczytu powtarzalne domyślnie przyjmuje współużytkowane blokady.
Jednak do żadnej operacji odczytu obsługującego powtarzalnego odczytu hello użytkownika można uzyskać blokady aktualizacji zamiast hello blokady współużytkowane.
Blokady aktualizacji jest asymetrycznego blokady używane tooprevent wspólnej formy zakleszczenia, gdy wiele transakcji blokowania zasobów potencjalnych aktualizacji w późniejszym czasie.

macierz zgodności blokad Hello znajdują się w hello w poniższej tabeli:

| Żądanie \ przyznane | Brak | Udostępniona | Aktualizacja | Wyłączności |
| --- |:--- |:--- |:--- |:--- |
| Udostępniona |Nie konfliktów |Nie konfliktów |Konflikt |Konflikt |
| Aktualizacja |Nie konfliktów |Nie konfliktów |Konflikt |Konflikt |
| Wyłączności |Nie konfliktów |Konflikt |Konflikt |Konflikt |

Argument limitu czasu w hello niezawodnej kolekcji interfejsów API jest używany do wykrywania zakleszczeń.
Na przykład dwie transakcje (T1 a T2) próbujesz tooread i zaktualizuj K1.
Istnieje możliwość ich toodeadlock, ponieważ oba mających hello udostępnione blokady.
W takim przypadku jednego lub obu z operacji hello będzie upłynął limit czasu.

W tym scenariuszu zakleszczenie jest doskonałym przykładem jak blokady aktualizacji można zapobiec zakleszczenia.

## <a name="next-steps"></a>Następne kroki
* [Praca z elementami Reliable Collections](service-fabric-work-with-reliable-collections.md)
* [Niezawodne usługi powiadomień](service-fabric-reliable-services-notifications.md)
* [Niezawodne usługi Kopia zapasowa i przywracanie (odzyskiwania po awarii)](service-fabric-reliable-services-backup-restore.md)
* [Stan niezawodny Menedżera konfiguracji](service-fabric-reliable-services-configuration.md)
* [Dokumentacja dla deweloperów niezawodnej kolekcji](https://msdn.microsoft.com/library/azure/microsoft.servicefabric.data.collections.aspx)

