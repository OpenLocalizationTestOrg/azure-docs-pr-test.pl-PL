---
title: "aaaGuidelines & zalecenia dotyczące niezawodnej kolekcji w sieci szkieletowej usług Azure | Dokumentacja firmy Microsoft"
description: "Wskazówki i zalecenia dotyczące używania kolekcji niezawodnej sieci szkieletowej usług"
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
ms.date: 5/3/2017
ms.author: mcoskun
ms.openlocfilehash: bcdbc9d013bc044e06c43761e7f515c7e4bf340c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="guidelines-and-recommendations-for-reliable-collections-in-azure-service-fabric"></a>Wskazówki i zalecenia dotyczące niezawodnej kolekcji w sieci szkieletowej usług Azure
Ta sekcja zawiera wskazówki dotyczące korzystania niezawodnej Menedżer stanu i niezawodne kolekcji. Celem Hello jest toohelp użytkownikom uniknąć typowych problemów.

wytyczne Hello są zorganizowane jako proste zalecenia prefiksem warunki hello *czy*, *rozważ*, *należy unikać* i *nie*.

* Nie należy modyfikować niestandardowego typu zwrócone przez operacje odczytu obiektu (na przykład `TryPeekAsync` lub `TryGetValueAsync`). Niezawodne kolekcje, podobnie jak kolekcji współbieżnych zwracać obiekty toohello odwołania, a nie kopię.
* Czy hello bezpośrednich kopii zwrócił obiekt typu niestandardowego przed zmodyfikowaniem go. Ponieważ wbudowane typy i struktury są przebiegu przez wartość, nie trzeba toodo bezpośrednich kopii na nich.
* Nie używaj `TimeSpan.MaxValue` dla limitu czasu. Limity czasu powinna być używana toodetect zakleszczenie.
* Nie używaj transakcji po została zatwierdzona, zostało przerwane lub usunięty.
* Nie należy używać wyliczenie poza zasięgiem transakcji hello, który został utworzony.
* Nie twórz transakcji w innej transakcji `using` instrukcji, ponieważ może to spowodować zakleszczenie.
* Upewnij się, że Twoje `IComparable<TKey>` implementacja jest prawidłowa. Hello system przejmuje zależności `IComparable<TKey>` do scalenia punkty kontrolne i wierszy.
* Należy używać blokowania aktualizacji podczas odczytywania elementu tooupdate zamiar go tooprevent klasy zakleszczenia.
* Pomyśl o pozostawieniu elementów (na przykład TKey + TValue niezawodnej słownika) poniżej 80 KB: hello mniejszych lepiej. Zmniejsza ilość hello wymagań we/wy sterty dużych obiektów użycia jak również dysków i sieci. Często zmniejsza replikowanie danych zduplikowanych, gdy tylko jeden niewielką część hello wartość jest aktualizowana. Typowe tooachieve sposób w słowniku niezawodnej to toobreak Twojego wierszy w toomultiple wierszy.
* Należy wziąć pod uwagę przy użyciu kopii zapasowej i przywracania odzyskiwania po awarii toohave funkcji.
* Unikaj mieszanie operacje pojedynczej jednostki i operacje obejmujące wiele urządzeń (np. `GetCountAsync`, `CreateEnumerableAsync`) w hello transakcji tego samego powodu toohello izolacji różnych poziomów.
* Obsługa InvalidOperationException. Transakcje użytkowników może zostać przerwane przez system hello różnych powodów. Na przykład gdy hello niezawodnej Menedżer stanów jest zmiana jego rolą poza podstawowej lub transakcji długotrwałe blokuje obcinania dziennika transakcyjne hello. W takich przypadkach użytkownik może odbierać InvalidOperationException wskazujący, że ich transakcji został już zakończony. Przy założeniu, nie zażądano zakończenia hello hello transakcji przez użytkownika hello, najlepsze sposób toohandle tego wyjątku jest toodispose hello transakcji, sprawdź, czy token anulowania hello zostały sygnalizowane (lub zostały zmienione hello roli repliki hello), a jeśli nie Utwórz nową transakcję i spróbuj ponownie.  

Poniżej przedstawiono niektóre tookeep rzeczy pamiętać:

* Hello domyślny limit czasu wynosi cztery sekund dla wszystkich hello niezawodnej kolekcji interfejsów API. Większość użytkowników należy używać hello domyślny limit czasu.
* Witaj domyślny token anulowania jest `CancellationToken.None` w wszystkich interfejsów API niezawodnej kolekcji.
* Parametr typu klucza Hello (*TKey*) dla słownika niezawodnej poprawnie musi implementować `GetHashCode()` i `Equals()`. Klucze muszą być niezmienialne.
* tooachieve wysoka dostępność dla hello niezawodnej kolekcje, każda usługa powinna mieć co najmniej docelowej i repliki minimalny rozmiar 3.
* Operacje odczytu na powitania dodatkowej może odczytać wersje, które nie są zatwierdzone kworum.
  Oznacza to, że wersji danych, które są odczytywane z jednej dodatkowej może FAŁSZ postępem.
  Odczyty z podstawowego zawsze są stabilne: może nie być false biegiem czasu.

### <a name="next-steps"></a>Następne kroki
* [Praca z elementami Reliable Collections](service-fabric-work-with-reliable-collections.md)
* [Transakcje i blokad](service-fabric-reliable-services-reliable-collections-transactions-locks.md)
* [Menedżer stanu niezawodnych i wewnętrzne kolekcji](service-fabric-reliable-services-reliable-collections-internals.md)
* Zarządzanie danymi
  * [Tworzenie kopii zapasowej i przywracanie](service-fabric-reliable-services-backup-restore.md)
  * [Powiadomienia](service-fabric-reliable-services-notifications.md)
  * [Serializacja i uaktualniania](service-fabric-application-upgrade-data-serialization.md)
  * [Stan niezawodny Menedżera konfiguracji](service-fabric-reliable-services-configuration.md)
* Inne
  * [Niezawodne usługi szybki start](service-fabric-reliable-services-quick-start.md)
  * [Dokumentacja dla deweloperów niezawodnej kolekcji](https://msdn.microsoft.com/library/azure/microsoft.servicefabric.data.collections.aspx)
