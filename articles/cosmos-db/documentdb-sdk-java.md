---
title: "Azure DB rozwiązania Cosmos: Java usługi DocumentDB interfejsu API zestawu SDK i zasoby | Dokumentacja firmy Microsoft"
description: "Dowiedz się wszystkiego o hello interfejsu API języka Java i zestawu SDK, w tym daty wydania, daty wycofania i zmiany między poszczególnymi wersjami hello zestawu SDK Java usługi DocumentDB Azure rozwiązania Cosmos bazy danych."
services: cosmos-db
documentationcenter: java
author: rnagpal
manager: jhubbard
editor: cgronlun
ms.assetid: 7861cadf-2a05-471a-9925-0fec0599351b
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: java
ms.topic: article
ms.date: 07/11/2017
ms.author: khdang
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 8ef43ebeb7ae1bfc55512c4a7489c1b7930122d6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-documentdb-java-sdk-release-notes-and-resources"></a>Azure DB rozwiązania Cosmos: Zestawu SDK Java usługi DocumentDB informacje o wersji i zasoby
> [!div class="op_single_selector"]
> * [.NET](documentdb-sdk-dotnet.md)
> * [Źródła danych zmian .NET](documentdb-sdk-dotnet-changefeed.md)
> * [.NET Core](documentdb-sdk-dotnet-core.md)
> * [Node.js](documentdb-sdk-node.md)
> * [Java](documentdb-sdk-java.md)
> * [Python](documentdb-sdk-python.md)
> * [REST](https://docs.microsoft.com/rest/api/documentdb/)
> * [Dostawca zasobów REST](https://docs.microsoft.com/rest/api/documentdbresourceprovider/)
> * [SQL](https://msdn.microsoft.com/library/azure/dn782250.aspx)
> 
> 

<table>

<tr><td>**Pobierz zestaw SDK**</td><td>[Maven](http://search.maven.org/#search%7Cgav%7C1%7Cg%3A%22com.microsoft.azure%22%20AND%20a%3A%22azure-documentdb%22)</td></tr>

<tr><td>**Dokumentacja interfejsu API**</td><td>[Dokumentacji interfejsu API języka Java](/java/api/com.microsoft.azure.documentdb)</td></tr>

<tr><td>**Współtworzenia tooSDK**</td><td>[GitHub](https://github.com/Azure/azure-documentdb-java/)</td></tr>

<tr><td>**Wprowadzenie**</td><td>[Rozpoczynanie pracy z hello zestawu Java SDK](documentdb-java-get-started.md)</td></tr>

<tr><td>**Samouczek aplikacji sieci Web**</td><td>[Tworzenie aplikacji sieci Web z bazy danych Azure rozwiązania Cosmos](documentdb-java-application.md)</td></tr>

<tr><td>**Bieżącego środowiska uruchomieniowego obsługiwane**</td><td>[JDK 7](http://www.oracle.com/technetwork/java/javase/downloads/jdk7-downloads-1880260.html)</td></tr>
</table></br>

## <a name="release-notes"></a>Informacje o wersji

### <a name="a-name11201120"></a><a name="1.12.0"/>1.12.0
* Dzieli toorequest krytycznych poprawek przetwarzania podczas partycji.
* Rozwiązano problem z hello silne i BoundedStaleness poziomy spójności.

### <a name="a-name11101110"></a><a name="1.11.0"/>1.11.0
* Dodano obsługę nowego poziomu spójności o nazwie ConsistentPrefix.
* Stałe błędów w kolekcji sesji w trybie odczytu.

### <a name="a-name11001100"></a><a name="1.10.0"/>1.10.0
* Włączona obsługa kolekcji partycjonowanych jako niskie jako 2500 RU/s i skalować z przyrostem 100 RU/s.
* Rozwiązane usterki w hello natywny zestaw, co może spowodować wyjątek NullRef niektórych kwerend.

### <a name="a-name196196"></a><a name="1.9.6"/>1.9.6
* Stała usterki w hello zapytań aparatu konfiguracji, które mogą powodować wyjątki dla zapytań w trybie bramy.
* Stałe kilka błędów w kontenerze hello sesji, która może spowodować wyjątek "Nie można odnaleźć zasobu właściciela" żądań natychmiast po utworzeniu kolekcji.

### <a name="a-name195195"></a><a name="1.9.5"/>1.9.5
* Dodano obsługę zapytań agregacji (COUNT, MIN, MAX, SUM i Śr.). Zobacz [Obsługa agregacji](documentdb-sql-query.md#Aggregates).
* Dodano obsługę zmiany źródła danych.
* Dodano obsługę za pośrednictwem RequestOptions.setPopulateQuotaInfo, informacje o limicie przydziału kolekcji.
* Dodano obsługę rejestrowania skryptu procedury składowanej za pośrednictwem RequestOptions.setScriptLoggingEnabled.
* Stałe usterki, gdzie mogą wykraczać zapytania w trybie DirectHttps, gdy wystąpią błędy ograniczania.
* Rozwiązane usterki w tryb spójność sesji.
* Stałe błędów, które mogą spowodować NullReferenceException element HttpContext po wysoki współczynnik żądań.
* Lepsza wydajność DirectHttps tryb.

### <a name="a-name194194"></a><a name="1.9.4"/>1.9.4
* Dodano proste klienta oparte na wystąpienie obsługi serwera proxy z interfejsem API ConnectionPolicy.setProxy().
* Dodano DocumentClient.close() API tooproperly zamknięcia DocumentClient wystąpienie.
* Wydajność ulepszone zapytań w trybie bezpośrednie połączenie między przez pochodny planu zapytania hello hello natywny zestaw zamiast hello bramy.
* Ustaw FAIL_ON_UNKNOWN_PROPERTIES = false, dzięki czemu użytkownicy nie muszą toodefine JsonIgnoreProperties w ich typu POJO.
* Rejestrowanie refaktoryzowane toouse SLF4J.
* Stała kilka innych błędów spójności czytnika.

### <a name="a-name193193"></a><a name="1.9.3"/>1.9.3
* Rozwiązane usterki w hello przecieki połączenia tooprevent zarządzania połączenia w trybie bezpośredniego połączenia.
* Stała usterki hello zapytania TOP, w którym może zgłosić wyjątek NullReferenece.
* Lepszą wydajność dzięki zmniejszeniu liczby hello wywołania sieci dla hello wewnętrznych pamięci podręcznych.
* Kod stanu dodany, ActivityID i identyfikator URI żądania w DocumentClientException w celu ułatwienia rozwiązywania problemów.

### <a name="a-name192192"></a><a name="1.9.2"/>1.9.2
* Rozwiązano problem z zarządzaniem połączeniami hello stabilności.

### <a name="a-name191191"></a><a name="1.9.1"/>1.9.1
* Dodano obsługę BoundedStaleness poziomu spójności.
* Dodano obsługę bezpośrednie połączenie między dla operacji CRUD dla kolekcji partycjonowanych.
* Stałe błędów badania bazy danych z programu SQL.
* Rozwiązane usterki w pamięci podręcznej sesji hello gdzie może być niepoprawna tokenu sesji.

### <a name="a-name190190"></a><a name="1.9.0"/>1.9.0
* Dodano obsługę dla wielu partycji zapytania równoległe.
* Dodano obsługę TOP/ORDER BY zapytania dla kolekcji partycjonowanych.
* Dodano obsługę wysoki poziom spójności.
* Dodano obsługę żądań na podstawie nazwy przy użyciu bezpośrednie połączenie między.
* Stałe toomake ActivityId pozostaną niezmienione we wszystkich ponownych prób wykonania żądania.
* Stałe błędów związane z pamięci podręcznej toohello sesji podczas odtwarzania Kolekcja o hello tej samej nazwy.
* Dodano wielokąta i typy danych LineString podczas określania kolekcji indeksowania zasad dla zapytań przestrzennych grodzenia.
* Rozwiązane problemy z dokumentem Java dla języka Java 1.8.

### <a name="a-name181181"></a><a name="1.8.1"/>1.8.1
* Rozwiązane usterki w PartitionKeyDefinitionMap toocache kolekcje z jedną partycją i nie dokonywać dodatkowe pobrać partycji żądania klucza.
* Stała ponowna próba toonot usterki, gdy została podana wartość klucza partycji niepoprawne.

### <a name="a-name180180"></a><a name="1.8.0"/>1.8.0
* Hello dodano obsługę konta w przypadku bazy danych.
* Dodano obsługę automatycznego próbowania na ograniczeniem przepustowości żądania za pomocą opcji toocustomize hello max ponowienia i maksymalna czas oczekiwania.  Zobacz RetryOptions i ConnectionPolicy.getRetryOptions().
* Przestarzałe IPartitionResolver na podstawie niestandardowych kodów partycjonowania. Użyj kolekcji partycjonowanych wyżej magazynu i przepustowości.

### <a name="a-name171171"></a><a name="1.7.1"/>1.7.1
* Obsługa zasad ponawiania dodano ograniczania.  

### <a name="a-name170170"></a><a name="1.7.0"/>1.7.0
* Czas toolive (TTL) Obsługa dokumentów.

### <a name="a-name160160"></a><a name="1.6.0"/>1.6.0
* Zaimplementowane [kolekcje partycjonowane](partition-data.md) i [poziomy wydajności zdefiniowanych przez użytkownika](performance-levels.md).

### <a name="a-name151151"></a><a name="1.5.1"/>1.5.1
* Rozwiązane usterki w wartości skrótu toogenerate HashPartitionResolver w toobe little endian zgodne z innych zestawów SDK.

### <a name="a-name150150"></a><a name="1.5.0"/>1.5.0
* Dodaj skrót & zakres tooassist rozpoznawania nazw partycji z aplikacjami dzielenia na fragmenty między wieloma partycjami.

### <a name="a-name140140"></a><a name="1.4.0"/>1.4.0
* Implementuje Upsert. Nowych metod upsertXXX dodać toosupport Upsert funkcji.
* Na podstawie Identyfikatora wdrożenie routingu. Brak zmian publicznego interfejsu API, wszystkie zmiany wewnętrznego.

### <a name="a-name130130"></a><a name="1.3.0"/>1.3.0
* Numer wersji toobring wyrównania z innych zestawów SDK pominięte zlecenia

### <a name="a-name120120"></a><a name="1.2.0"/>1.2.0
* Obsługuje dane geograficzne indeksu
* Weryfikuje właściwość identyfikatora dla wszystkich zasobów. Identyfikatory zasobów nie może zawierać?, /, #, \, znaków ani kończyć spacją.
* Dodaje nowy tooResourceResponse "postępu przekształcania indeksu" nagłówka.

### <a name="a-name110110"></a><a name="1.1.0"/>1.1.0
* Implementuje zasady indeksowania V2

### <a name="a-name100100"></a><a name="1.0.0"/>1.0.0
* GA SDK

## <a name="release--retirement-dates"></a>Wersja & daty wycofania
Firma Microsoft udostępni powiadomienia co najmniej **12 miesięcy** klienta z wyprzedzeniem wycofanie SDK w kolejności toosmooth hello przejścia tooa nowszej/nieobsługiwaną wersję.

Nowe funkcje i funkcjonalność i optymalizację, które są dodawane tylko bieżącego toohello SDK, jak jest możliwie jak najszybciej zaleca tego należy zawsze uaktualnienia toohello najnowsze wersja zestawu SDK.

Wszystkie żądania tooCosmos bazy danych przy użyciu wycofane zestawu SDK będą odrzucane przez usługę hello.

> [!WARNING]
> Wszystkie wersje hello zestawu SDK usługi DocumentDB dla poprzedniego tooversion Java **1.0.0** zostaną wycofane w **29 lutego 2016**.
> 
> 

<br/>

| Wersja | Data wydania | Dacie wycofania |
| --- | --- | --- |
| [1.12.0](#1.12.0) |11 lipca 2017 r. |--- |
| [1.11.0](#1.11.0) |10 maja 2017 |--- |
| [1.10.0](#1.10.0) |11 marca 2017 r. |--- |
| [1.9.6](#1.9.6) |21 lutego 2017 r. |--- |
| [1.9.5](#1.9.5) |31 stycznia 2017 r. |--- |
| [1.9.4](#1.9.4) |24 listopada 2016 r. |--- |
| [1.9.3](#1.9.3) |30 października 2016 r. |--- |
| [1.9.2](#1.9.2) |28 października 2016 r. |--- |
| [1.9.1](#1.9.1) |26 października 2016 r. |--- |
| [1.9.0](#1.9.0) |03 października 2016 r. |--- |
| [1.8.1](#1.8.1) |30 czerwca 2016 r. |--- |
| [1.8.0](#1.8.0) |14 czerwca 2016 r. |--- |
| [1.7.1](#1.7.1) |30 kwietnia 2016 r. |--- |
| [1.7.0](#1.7.0) |27 kwietnia 2016 r. |--- |
| [1.6.0](#1.6.0) |29 marca 2016 r. |--- |
| [1.5.1](#1.5.1) |31 grudnia 2015 r. |--- |
| [1.5.0](#1.5.0) |04 grudnia 2015 r. |--- |
| [1.4.0](#1.4.0) |05 października 2015 |--- |
| [1.3.0](#1.3.0) |05 października 2015 |--- |
| [1.2.0](#1.2.0) |05 sierpnia 2015 |--- |
| [1.1.0](#1.1.0) |09 lipca 2015 r. |--- |
| [1.0.1](#1.0.1) |12 maja 2015 r. |--- |
| [1.0.0](#1.0.0) |07 kwietnia 2015 r. |--- |
| 0.9.5-prelease |09 marca 2015 roku. |29 lutego 2016 r. |
| 0.9.4-prelease |17 lutego 2015 |29 lutego 2016 r. |
| 0.9.3-prelease |13 stycznia 2015 r. |29 lutego 2016 r. |
| 0.9.2-prelease |19 grudnia 2014 r. |29 lutego 2016 r. |
| 0.9.1-prelease |19 grudnia 2014 r. |29 lutego 2016 r. |
| 0.9.0-prelease |10 grudnia 2014 r. |29 lutego 2016 r. |

## <a name="faq"></a>Często zadawane pytania
[!INCLUDE [cosmos-db-sdk-faq](../../includes/cosmos-db-sdk-faq.md)]

## <a name="see-also"></a>Zobacz też
toolearn więcej informacji na temat rozwiązania Cosmos bazy danych, zobacz [bazy danych programu Microsoft Azure rozwiązania Cosmos](https://azure.microsoft.com/services/cosmos-db/) stronę usługi.

