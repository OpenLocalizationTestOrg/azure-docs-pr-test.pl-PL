---
title: "tooAzure aaaIntroduction DB rozwiązania Cosmos | Dokumentacja firmy Microsoft"
description: "Zapoznaj się z informacjami na temat usługi Azure Cosmos DB. Ta dostępna w skali światowej, wielomodelowa baza danych zapewnia małe opóźnienia, elastyczną skalowalność i wysoką dostępność."
services: cosmos-db
author: mimig1
manager: jhubbard
editor: monicar
documentationcenter: 
ms.assetid: a855183f-34d4-49cc-9609-1478e465c3b7
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/14/2017
ms.author: mimig
ms.custom: mvc
ms.openlocfilehash: f2acbe99f425b2f07a62bbbb4324aa48f1037481
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="welcome-tooazure-cosmos-db"></a>Zapraszamy tooAzure DB rozwiązania Cosmos

Azure Cosmos DB to dostępna w skali światowej, wielomodelowa baza danych firmy Microsoft. Witaj kliknięcie przycisku bazy danych Azure rozwiązania Cosmos pozwala tooelastically i niezależnie skali przepływność i Magazyn przez dowolną liczbę regionów geograficznych platformy Azure. W odróżnieniu od wszelkich innych usług baz danych, oferuje ona gwarancje dotyczące przepływności, opóźnienia, dostępności i spójności dzięki kompleksowym [umowom dotyczącym poziomu usług](https://aka.ms/acdbsla) (SLA, Service Level Agreement).

![Azure Cosmos DB to dostępna w skali światowej usługa bazy danych firmy Microsoft z elastycznym skalowaniem, gwarantowanymi małymi opóźnieniami, pięcioma modelami spójności oraz kompleksowymi, gwarantowanymi umowami SLA](./media/introduction/azure-cosmos-db.png)

## <a name="solutions-that-benefit-from-azure-cosmos-db"></a>Rozwiązania, które korzystają z zalet usługi Azure Cosmos DB

Wszelkie [w sieci web, mobilnych, gier i aplikacji IoT](use-cases.md) wymagające toohandle olbrzymich ilości odczyty i zapisy na [globalne](distribute-data-globally.md) skalować wraz z czasem odpowiedzi niski dla różnych danych będą korzystać z usługi Azure rozwiązania Cosmos DB [gwarantowane](https://azure.microsoft.com/support/legal/sla/cosmos-db/) dostępności, wysokiej przepływności, małych opóźnień i dostosowywalne spójności.

## <a name="key-capabilities"></a>Najważniejsze możliwości
Jako usługa globalnie rozproszoną bazę danych bazy danych rozwiązania Cosmos Azure zapewnia następujące możliwości toohelp kompilacji skalowalne, wysoko reakcji aplikacji hello:

* **Gotowa do użytku dystrybucja globalna**
    * Możesz [dystrybucji danych](distribute-data-globally.md) tooany liczbę [regiony platformy Azure](https://azure.microsoft.com/regions/), z hello [kliknij przycisku](tutorial-global-distribution-documentdb.md). Dzięki temu można tooput dane, których użytkownicy zapewnienie hello można uzyskać najmniejsze opóźnienia możliwe tooyour klientów. 
    * Za pomocą usługi Azure rozwiązania Cosmos DB wielu interfejsów API aplikacji hello zawsze wie, gdzie hello najbliższy region jest i będzie wysyłać żądań toohello najbliższego centrum danych. Wszystko to jest możliwe bez zmian konfiguracji, należy ustawić regionu zapisu i odczytywać wiele regionów, a hello rest jest już obsługiwane.

* **Wiele modeli danych i popularnych interfejsów API na potrzeby uzyskiwania dostępu do danych i wykonywania względem nich zapytań**
    * Hello atom rekordu sekwencji (ARS) na podstawie danych modelu, który bazy danych Azure rozwiązania Cosmos jest natywnie oparty na obsługuje wiele modeli danych, w tym między innymi toodocument, wykres klucz wartość, tabeli i kolumnowy danych modeli.
    * Interfejsy API do powitania po modelach danych są obsługiwane przez zestaw SDK jest dostępny w wielu językach:
        * [Interfejs API usługi DocumentDB](documentdb-introduction.md)
        * [Interfejs API usługi MongoDB](mongodb-introduction.md)
        * [Interfejs API tabel](table-introduction.md)
        * [Interfejs API programu Graph (Gremlin)](graph-introduction.md)
        * Dodatkowe modele danych będą dostępne wkrótce 

* **Elastycznie skalowana przepływność i przestrzeń dyskowa na żądanie, na całym świecie**
    * Łatwe skalowanie przepływności bazy danych z [sekundową](request-units.md) dokładnością i możliwość jej zmiany w dowolnym momencie. 
    * Skaluj rozmiar magazynu [przezroczyste i automatycznie](partition-data.md) toohandle wymagań rozmiar teraz i nieskończona.

* **Tworzenie szybko reagujących aplikacji o kluczowym znaczeniu**
    * Azure DB rozwiązania Cosmos gwarantuje end-to-end małych opóźnieniach na powitania 99-ty percentyl tooits klientów. 
    * Typowe 1 KB elementu, DB rozwiązania Cosmos gwarantuje czas oczekiwania na trasie odczytów poniżej 10 ms i indeksowane zapisy na powitania 99-ty percentyl, w obszarze 15 ms poziomu hello sam region platformy Azure. opóźnienia środkowej Hello są znacznie niższe (w obszarze 5 ms).

* **Zapewnienie dostępności na poziomie „zawsze włączona”**
    * Dostępność na poziomie 99,99% w obrębie jednego regionu.
    * Wdrażanie tooany liczbę [regiony platformy Azure](https://azure.microsoft.com/regions) potrzeby wyższej dostępności.
    * [Symulowanie awarii](regional-failover.md) co najmniej jednego regionu z gwarancją, że nie nastąpi utrata żadnych danych. 

* **Pisanie aplikacji rozproszonych globalnie hello prawym przyciskiem myszy sposób**
    * Pięć [modeli spójności](consistency-levels.md) modele umożliwiają liczne silna spójność przypominającego SQL wszystkie hello sposób tooNoSQL przypominającej spójność ostateczna, a każdy element między. 
  
* **Gwarancja zwrotu pieniędzy**
    * Szybkie dostarczanie danych lub zwrot pieniędzy. 
    * [Umowy dotyczące poziomu usług](https://aka.ms/acdbsla) obejmujące dostępność, opóźnienie, przepływność i spójność. 

* **Brak potrzeby zarządzania schematami i indeksami bazy danych**
    * Nie musisz już martwić się o synchronizowanie indeksów i schematu bazy danych ze schematem aplikacji. U nas nie ma schematów. 
    * Aparat bazy danych Azure DB rozwiązania Cosmos pełni schematu niezwiązane z żadnym — automatycznie indeksuje wszystkie dane hello go wysyła strumień bez żadnego schematu lub indeksy i służy błyskawicznie szybkie zapytania. 

* **Niski koszt posiadania**
    * Pięć razy tooten [bardziej ekonomiczne](https://aka.ms/cosmos-db-tco-paper) niż rozwiązania niezarządzanego.
    * Trzy razy taniej niż w przypadku usługi DynamoDB.

## <a name="capability-comparison"></a>Porównanie możliwości

Azure DB rozwiązania Cosmos oferuje najlepsze możliwości hello baz danych relacyjnych i nierelacyjnych.

| Możliwości | Relacyjne bazy danych   | Nierelacyjne bazy danych (NoSQL) |    Azure Cosmos DB |
| --- | --- | --- | --- |
| Dystrybucja globalna | Nie | Nie | Tak, gotowa do użycia dystrybucja w ponad 30 regionach z międzyregionalnymi interfejsami API|
| Skalowanie w poziomie | Nie | Tak | Tak, możliwe jest niezależne skalowanie magazynu i przepływności | 
| Gwarancje dot. opóźnienia | Nie | Tak | Tak, 99% odczytów trwa poniżej 10 ms, a 99% zapisów poniżej 15 ms | 
| Wysoka dostępność | Nie | Tak | Tak, usługa Cosmos DB jest zawsze włączona, umożliwia wymiany zgodne z modelem PACELC oraz udostępnia opcje automatycznego i ręcznego przechodzenia w tryb failover|
| Model danych + interfejs API | Relacyjny + SQL | Wiele modeli + OSS API | Wiele modeli + SQL + OSS API (więcej wkrótce) |
| Umowy SLA | Tak | Nie | Tak, kompleksowe umowy SLA dotyczące opóźnienia, przepływności, spójności i dostępności |


## <a name="next-steps"></a>Następne kroki
Rozpocznij pracę z usługą Azure Cosmos DB, korzystając z jednego z naszych przewodników:

* [Rozpoczynanie pracy z interfejsem API DocumentDB usługi Azure Cosmos DB](create-documentdb-dotnet.md)
* [Rozpoczynanie pracy z interfejsem API MongoDB usługi Azure Cosmos DB](create-mongodb-nodejs.md)
* [Rozpoczynanie pracy z interfejsem API Graph usługi Azure Cosmos DB](create-graph-dotnet.md)
* [Rozpoczynanie pracy z interfejsem API tabeli usługi Azure Cosmos DB](create-table-dotnet.md)
