---
title: "dane wyjściowe aaaJSON Stream Analytics | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak Stream Analytics można kierować bazy danych rozwiązania Cosmos Azure dla danych wyjściowych JSON archiwizowania danych i zapytania o małych opóźnieniach na dane JSON bez struktury."
keywords: "Dane wyjściowe JSON"
documentationcenter: 
services: stream-analytics,documentdb
author: samacha
manager: jhubbard
editor: cgronlun
ms.assetid: 5d2a61a6-0dbf-4f1b-80af-60a80eb25dd1
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 03/28/2017
ms.author: samacha
ms.openlocfilehash: fa717818c839ecd7a60fcee33d22011990fd5878
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="target-azure-cosmos-db-for-json-output-from-stream-analytics"></a>Docelowej bazy danych rozwiązania Cosmos Azure dla danych wyjściowych JSON z usługi Stream Analytics
Analiza strumienia może kierować [bazy danych Azure rozwiązania Cosmos](https://azure.microsoft.com/services/documentdb/) dla danych wyjściowych JSON, włączanie archiwizacji i małych opóźnieniach kwerend danych na dane JSON bez struktury. W tym dokumencie opisano najważniejsze wskazówki dotyczące implementowania tej konfiguracji.

Dla osób, które znają rozwiązania Cosmos DB, Przyjrzyjmy się [ścieżka szkoleniowa dotycząca usługi Azure rozwiązania Cosmos DB](https://azure.microsoft.com/documentation/learning-paths/documentdb/) tooget uruchomiona. 

Uwaga: DB rozwiązania Cosmos oparty na interfejsach API DB Mongo kolekcji nie jest obecnie obsługiwany. 

## <a name="basics-of-cosmos-db-as-an-output-target"></a>Podstawy DB rozwiązania Cosmos jako miejsce docelowe danych wyjściowych
Hello wydajności bazy danych Azure rozwiązania Cosmos w Stream Analytics umożliwia zapisywanie strumienia przetwarzanie wyników jako dane wyjściowe JSON do kolekcji z bazy danych rozwiązania Cosmos. Analiza strumienia nie tworzenia kolekcji w bazie danych, zamiast konieczności toocreate ich nabywanych usług. Jest to, aby hello rozliczeń koszty DB rozwiązania Cosmos kolekcje są tooyou przezroczysty i tak, aby dostroić hello wydajności, spójność i pojemność kolekcji bezpośrednio przy użyciu hello [rozwiązania Cosmos DB API](https://msdn.microsoft.com/library/azure/dn781481.aspx). Zalecamy użycie jednej bazy danych DB rozwiązania Cosmos na przesyłanie strumieniowe oddzielne toologically zadania kolekcji dla zadania przesyłania strumieniowego.

Niektóre opcje kolekcji DB rozwiązania Cosmos hello są szczegółowo opisane poniżej.

## <a name="tune-consistency-availability-and-latency"></a>Dostosuj spójności, dostępnością i opóźnieniem
toomatch wymagań aplikacji DB rozwiązania Cosmos pozwala toofine strojenia hello w bazie danych i kolekcji, kompromisy upewnij między spójności, dostępności i opóźnień. W zależności od tego, jakiego poziomu spójności odczytu potrzeb scenariusz przed zapisu i odczytu opóźnienia, możesz wybrać poziom spójności na konta bazy danych. Domyślnie DB rozwiązania Cosmos umożliwia również synchroniczne indeksowania w każdej kolekcji tooyour operacji CRUD. Jest to inny przydatna opcja hello toocontrol zapisu/odczytu wydajności do bazy danych rozwiązania Cosmos. Aby uzyskać więcej informacji na ten temat, zapoznaj się z hello [Zmień poziomy spójności bazy danych i zapytania](../documentdb/documentdb-consistency-levels.md) artykułu.

## <a name="upserts-from-stream-analytics"></a>Upserts z usługi Stream Analytics
Stream Analytics integracji z rozwiązania Cosmos DB umożliwia tooinsert lub aktualizacja rekordów w kolekcji rozwiązania Cosmos bazy danych na podstawie danego kolumny Identyfikator dokumentu. Dotyczy to również określonego tooas *Upsert*.

Stream Analytics wykorzystuje optymistycznej podejście Upsert, w której aktualizacje są wykonywane tylko po insert nie powiedzie się ze względu na konflikt identyfikatorów dokumentów tooa. Ta aktualizacja jest wykonywane przez Stream Analytics poprawek, więc umożliwia aktualizacje częściowe toohello dokumentu, tj. dodanie nowych właściwości lub zastąpienie istniejącej właściwości jest wykonywana stopniowo. Należy pamiętać, że zmiany w wartości właściwości tablicy w dokumencie JSON hello skutkować całą macierz hello pobierania zastąpione tj. nie jest scalany hello tablicy.

## <a name="data-partitioning-in-cosmos-db"></a>Partycjonowanie danych w bazie danych rozwiązania Cosmos
Rozwiązania cosmos DB [kolekcje partycjonowane](../cosmos-db/partition-data.md) są hello zalecane podejście do podziału danych. 

Dla jednej kolekcji rozwiązania Cosmos DB Stream Analytics nadal pozwala toopartition danych na podstawie zarówno hello wzorców zapytań i wymagania dotyczące wydajności aplikacji. Każda kolekcja może zawierać zapasowej too10GB danych (maksymalnie) i obecnie nie działa bez tooscale sposób (lub przepełnienie) kolekcji. Skalowanie w poziomie, Stream Analytics można w przypadku kolekcji toomultiple toowrite z danego prefiksu (zobacz poniżej szczegóły obciążenia). Stream Analytics korzysta hello spójne [rozpoznawania partycji skrótu](https://msdn.microsoft.com/library/azure/microsoft.azure.documents.partitioning.hashpartitionresolver.aspx) strategii na podstawie użytkownika hello toopartition kolumny PartitionKey pod warunkiem jego rekordów danych wyjściowych. Hello liczby kolekcji z hello podany prefiks na powitania przesyłania strumieniowego godzina rozpoczęcia zadania jest używany jako liczba partycji danych wyjściowych hello, zadanie hello toowhich zapisuje tooin równoległe (kolekcje DB rozwiązania Cosmos = partycje dane wyjściowe). Dla jednej kolekcji z opóźnieniem indeksowania czynności tylko wstawia, można oczekiwać o 0,4 przepływność zapisu MB/s. Przy użyciu wielu kolekcji umożliwiają możesz tooachieve wyższą przepływność i zwiększenia pojemności.

Jeśli planujesz liczba partycji hello tooincrease w przyszłości hello, może być konieczne toostop partycje, jego hello danych z istniejącej kolekcji do nowej kolekcji, a następnie zadanie usługi Stream Analytics hello ponownego uruchomienia zadania. Więcej informacji na temat przy użyciu PartitionResolver i ponownie partycjonowania wraz z przykładowym kodzie będą uwzględniane w kolejnych post. Artykuł Hello [dzielenia na partycje i skalowania w bazie danych rozwiązania Cosmos](../documentdb/documentdb-partition-data.md) także szczegółowe informacje na ten.

## <a name="cosmos-db-settings-for-json-output"></a>Ustawienia rozwiązania cosmos bazy danych dla danych wyjściowych JSON
Tworzenie rozwiązania Cosmos bazy danych jako dane wyjściowe w Stream Analytics generuje monit o podanie informacji, jak pokazano poniżej. Ta sekcja zawiera wyjaśnienie hello definicji właściwości.

Kolekcja podzielonym na partycje | Wiele kolekcji "Jednej partycji"
---|---
![documentdb stream analytics dane wyjściowe ekranu](media/stream-analytics-documentdb-output/stream-analytics-documentdb-output-1.png) |  ![documentdb stream analytics dane wyjściowe ekranu](media/stream-analytics-documentdb-output/stream-analytics-documentdb-output-2.png)


  
> [!NOTE]
> Witaj **wielu kolekcji "Jednej partycji"** scenariusz wymaga klucza partycji i konfiguracja jest obsługiwana. 

* **Dane wyjściowe Alias** — toorefer alias output to zapytanie ASA  
* **Nazwa konta** — hello nazwę lub identyfikator URI hello konto bazy danych rozwiązania Cosmos punktu końcowego.  
* **Klucz konta** — Witaj udostępniony klucz dostępu dla hello konto bazy danych rozwiązania Cosmos.  
* **Baza danych** — Nazwa bazy danych DB rozwiązania Cosmos hello.  
* **Wzorzec nazwy kolekcji** — Nazwa kolekcji hello lub ich wzorzec toobe kolekcje hello używane. format nazwy Hello kolekcji można skonstruować przy użyciu hello tokenu opcjonalne {partition}, gdzie partycje zaczynają się od 0. Poniżej przedstawiono przykładowe prawidłowe wartości wejściowe:  
  1\) MyCollection — jedną kolekcję o nazwie "MyCollection" musi istnieć.  
  2\) MyCollection {partition} — takie kolekcje muszą istnieć — "MyCollection0", "MyCollection1", "MyCollection2" itd.  
* **Klucz partycji** — jest to opcjonalne. Jest to potrzebne tylko, jeśli używasz tokenu {partycjonowania} we wzorcu nazwy Twojej kolekcji. Nazwa Hello hello pola w danych wyjściowych zdarzenia używane toospecify hello klucza do partycjonowania danych wyjściowych na kolekcje. Dla danych wyjściowych jednej kolekcji, wszystkie kolumny wyjściowej dowolnego mogą być używane np. PartitionId.  
* **Identyfikator dokumentu** — jest to opcjonalne. Nazwa Hello hello pola w zdarzeniach wyjściowych używana hello klucz podstawowy toospecify, na które insert lub update bazują operacje.  
