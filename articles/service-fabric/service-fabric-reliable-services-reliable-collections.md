---
title: "aaaIntroduction tooReliable kolekcje w stanowe usługi sieć szkieletowa usług Azure | Dokumentacja firmy Microsoft"
description: "Usługi sieć szkieletowa usług stanowych zapewniają niezawodne kolekcje, które umożliwiają aplikacji w chmurze wysoko dostępnych, skalowalnych i małych opóźnieniach toowrite."
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
ms.openlocfilehash: 9f67c48f13e8b91b84977e127e2545cbb9d9a158
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-tooreliable-collections-in-azure-service-fabric-stateful-services"></a>Wprowadzenie tooReliable kolekcje w stanowe usługi sieć szkieletowa usług Azure
Kolekcje niezawodnej Włącz aplikacje w chmurze wysoko dostępnych, skalowalnych i małych opóźnieniach toowrite tak, jakby podczas pisania aplikacji pojedynczego komputera. Witaj klas w hello **Microsoft.ServiceFabric.Data.Collections** przestrzeni nazw udostępniają zestaw kolekcji, które automatycznie swój stan wysokiej dostępności. Deweloperzy muszą toohello tylko tooprogram niezawodnej kolekcji interfejsów API i pozwól niezawodnej kolekcje Zarządzanie replikacją hello i stanu lokalnego.

Różnica klucza Hello kolekcje niezawodnych i innymi technologiami wysokiej dostępności (np. pamięci podręcznej Redis, usługa tabeli platformy Azure i usługi kolejek platformy Azure) jest czy hello stan jest przechowywany lokalnie w wystąpieniu usługi hello podczas również wysyłanych wysokiej dostępności. Oznacza to, że:

* Wszystkie operacje odczytu są lokalne, które powoduje małe opóźnienia i odczytuje wysokiej przepustowości.
* Zapisuje wszystkie pociągnąć za sobą hello minimalną liczbę IOs sieci, co powoduje małe opóźnienia i zapisuje wysokiej przepustowości.

![Obraz zmiany kolekcji.](media/service-fabric-reliable-services-reliable-collections/ReliableCollectionsEvolution.png)

Niezawodne kolekcji można traktować jak fizyczną ewolucji hello hello **System.Collections** klasy: nowy zestaw kolekcji, które są przeznaczone dla aplikacji hello chmury i złożonym z wielu komputerów bez zwiększania złożoność Witaj developer. W efekcie niezawodnej kolekcje są:

* Replikacja: Zmiany stanu są replikowane wysokiej dostępności.
* Utrwalony: Dane są trwałe toodisk dla trwałości względem awarii na dużą skalę (na przykład awaria zasilania centrum danych).
* Asynchronous: Interfejsy API są tooensure asynchronicznych wątków nie są blokowane podczas ponoszenia we/wy.
* Transakcyjne: Hello abstrakcji transakcji używają interfejsów API, a więc można łatwo zarządzać wielu kolekcji niezawodnej w ramach usługi.

Silna spójność gwarantuje poza toomake pole hello wnioskowania o stanie aplikacji, ułatwia zapewniają niezawodnej kolekcji.
Wysoki poziom spójności uzyskuje się poprzez zapewnienie zatwierdzeń Zakończ tylko wtedy, gdy cała transakcja hello został zalogowany większość kworum replik, w tym podstawowym hello transakcji.
tooachieve słabszych spójności, aplikacje można potwierdzić wstecz toohello klienta/zleceniodawcy przed zwraca hello zatwierdzania asynchronicznego.

Hello niezawodnej API kolekcje są zmiany kolekcji współbieżnych interfejsów API (w hello **System.Collections.Concurrent** przestrzeni nazw):

* Asynchroniczne: Zwraca klasę task, ponieważ w przeciwieństwie do kolekcji współbieżnych operacji hello są replikowane i utrwalone.
* Parametry wyjściowe nie: używa `ConditionalValue<T>` tooreturn bool i wartość zamiast parametrów wyjściowych. `ConditionalValue<T>`przypomina `Nullable<T>` , ale nie wymaga toobe T struktury.
* Transakcje: Używa obiektu tooenable hello użytkownika toogroup działania na wielu kolekcji niezawodnej w transakcji.

Obecnie **Microsoft.ServiceFabric.Data.Collections** zawiera trzy kolekcje:

* [Słownik niezawodnej](https://msdn.microsoft.com/library/azure/dn971511.aspx): reprezentuje replikowane, transakcyjne i asynchroniczne kolekcję par klucz/wartość. Podobnie za**obiekt ConcurrentDictionary**, zarówno hello klucz i wartość hello mogą być dowolnego typu.
* [Kolejka niezawodnych](https://msdn.microsoft.com/library/azure/dn971527.aspx): reprezentuje replikowane, transakcyjne i asynchroniczne strict pierwszy w, FIFO (FIFO) kolejki. Podobnie za**ConcurrentQueue**, wartość hello mogą być dowolnego typu.
* [Niezawodne kolejki równoczesnych](service-fabric-reliable-services-reliable-concurrent-queue.md): reprezentuje replikowane, transakcyjne i asynchroniczne optymalnego porządkowanie kolejki wysokiej przepływności. Podobne toohello **ConcurrentQueue**, wartość hello mogą być dowolnego typu.

## <a name="next-steps"></a>Następne kroki
* [Niezawodnej kolekcji wskazówki i zalecenia](service-fabric-reliable-services-reliable-collections-guidelines.md)
* [Praca z elementami Reliable Collections](service-fabric-work-with-reliable-collections.md)
* [Transakcje i blokad](service-fabric-reliable-services-reliable-collections-transactions-locks.md)
* [Menedżer stanu niezawodnych i wewnętrzne kolekcji](service-fabric-reliable-services-reliable-collections-internals.md)
* Zarządzanie danymi
  * [Tworzenie kopii zapasowej i przywracanie](service-fabric-reliable-services-backup-restore.md)
  * [Powiadomienia](service-fabric-reliable-services-notifications.md)
  * [Serializacja elementu Reliable Collection](service-fabric-reliable-services-reliable-collections-serialization.md)
  * [Serializacja i uaktualniania](service-fabric-application-upgrade-data-serialization.md)
  * [Stan niezawodny Menedżera konfiguracji](service-fabric-reliable-services-configuration.md)
* Inne
  * [Niezawodne usługi szybki start](service-fabric-reliable-services-quick-start.md)
  * [Dokumentacja dla deweloperów niezawodnej kolekcji](https://msdn.microsoft.com/library/azure/microsoft.servicefabric.data.collections.aspx)
