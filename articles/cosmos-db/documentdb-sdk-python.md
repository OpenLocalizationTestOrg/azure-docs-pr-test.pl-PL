---
title: "Python rozwiązania Cosmos Azure DB interfejsu API, zestaw SDK i zasoby | Dokumentacja firmy Microsoft"
description: "Dowiedz się wszystkiego o interfejsie API języka Python i zestawu SDK, w tym daty wydania, daty wycofania i zmiany wprowadzone od każdej wersji zestawu SDK Python platformy Azure rozwiązania Cosmos bazy danych."
services: cosmos-db
documentationcenter: python
author: rnagpal
manager: jhubbard
editor: cgronlun
ms.assetid: 3ac344a9-b2fa-4a3f-a4cc-02d287e05469
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: python
ms.topic: article
ms.date: 05/24/2017
ms.author: rnagpal
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 70d2550f713ff0e9daed235eb8053589b8682633
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/18/2017
---
# <a name="azure-cosmos-db-python-sdk-release-notes-and-resources"></a>Python rozwiązania Cosmos bazy danych Azure SDK: Informacje o wersji i zasoby
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

<tr><td>**Pobierz zestaw SDK**</td><td>[PyPI](https://pypi.python.org/pypi/pydocumentdb)</td></tr>

<tr><td>**Dokumentacja interfejsu API**</td><td>[Dokumentacji interfejsu API języka Python](http://azure.github.io/azure-documentdb-python/api/pydocumentdb.html)</td></tr>

<tr><td>**Instrukcje dotyczące instalacji zestawu SDK**</td><td>[Instrukcje dotyczące instalacji zestawu SDK Python](http://azure.github.io/azure-documentdb-python/)</td></tr>

<tr><td>**Przyczyniają się do zestawu SDK**</td><td>[GitHub](https://github.com/Azure/azure-documentdb-python)</td></tr>

<tr><td>**Wprowadzenie**</td><td>[Rozpoczynanie pracy z zestawem SDK Python](documentdb-python-application.md)</td></tr>

<tr><td>**Bieżący obsługiwanych platform**</td><td>[Python 2.7](https://www.python.org/downloads/) i [Python 3.5](https://www.python.org/downloads/)</td></tr>
</table></br>

## <a name="release-notes"></a>Informacje o wersji
### <a name="a-name220220"></a><a name="2.2.0"/>2.2.0
* Dodano obsługę nowego poziomu spójności o nazwie ConsistentPrefix.


### <a name="a-name210210"></a><a name="2.1.0"/>2.1.0
* Dodano obsługę zapytań agregacji (COUNT, MIN, MAX, SUM i Śr.).
* Dodano opcję wyłączenia weryfikacji protokołu SSL podczas uruchamiania emulatora DB rozwiązania Cosmos.
* Usunięte ograniczenie zależnych żądań modułu należy dokładnie 2.10.0.
* Obniżony minimalnej przepustowości w kolekcji partycjonowanych z 10,100 RU/s do 2500 RU/s.
* Dodano obsługę Włączanie rejestrowania skryptu podczas wykonywania procedury składowanej.
* Wersja interfejsu API REST upadku do "2017-01-19' w tej wersji.

### <a name="a-name201201"></a><a name="2.0.1"/>2.0.1
* Wprowadzone zmiany redakcyjne komentarzy do dokumentacji.

### <a name="a-name200200"></a><a name="2.0.0"/>2.0.0
* Dodano obsługę języka Python 3.5.
* Dodano obsługę dla puli połączeń przy użyciu modułu żądania.
* Dodano obsługę spójność sesji.
* Dodano obsługę TOP/ORDERBY zapytania dla kolekcji partycjonowanych.

### <a name="a-name190190"></a><a name="1.9.0"/>1.9.0
* Obsługa zasad dodano ponownych prób dla żądań z ograniczeniem przepustowości. (Ograniczeniem przepustowości żądania odbierania żądania szybkość zbyt duży wyjątek, kod błędu 429.) Domyślnie bazy danych Azure rozwiązania Cosmos ponowi próbę dziewięciokrotnie dla każdego żądania po napotkaniu błędu kodu 429 ramach czasu retryAfter nagłówka odpowiedzi. Czas interwału ponawiania stałym teraz można ustawić jako część właściwości RetryOptions w obiekcie ConnectionPolicy aby zignorować godzinę retryAfter zwrócony przez serwer między ponownymi próbami. Azure DB rozwiązania Cosmos teraz czeka na maksymalnie 30 sekund dla każdego żądania jest ograniczane (niezależnie od liczby ponownych prób) i zwraca odpowiedź z kodem błędu 429. Teraz można także przesłonięta we właściwości RetryOptions ConnectionPolicy obiektu.
* Rozwiązania cosmos DB teraz zwraca x-ms ograniczania liczby ponownych prób i x-ms-throttle-retry-wait-time-ms nagłówków odpowiedzi każde żądanie do oznaczania przepustnicy ponów liczba i czas cummulative żądanie oczekiwało między ponownymi próbami.
* Usunąć klasę RetryPolicy i odpowiadających im właściwości (retry_policy) udostępniane w klasie document_client i zamiast tego wprowadzono klasy RetryOptions udostępnianie właściwości RetryOptions w klasie ConnectionPolicy, który może służyć do zastępowania niektórych domyślne opcje ponownych prób.

### <a name="a-name180180"></a><a name="1.8.0"/>1.8.0
* Dodano obsługę konta w przypadku bazy danych.

### <a name="a-name170170"></a><a name="1.7.0"/>1.7.0
* Dodano obsługę funkcji czas do Live(TTL) dokumentów.

### <a name="a-name161161"></a><a name="1.6.1"/>1.6.1
* Poprawki błędów związanych z serwera partycjonowania po stronie, aby zezwalać na znaki specjalne w ścieżce partitionkey.

### <a name="a-name160160"></a><a name="1.6.0"/>1.6.0
* Zaimplementowane [kolekcje partycjonowane](partition-data.md) i [poziomy wydajności zdefiniowanych przez użytkownika](performance-levels.md). 

### <a name="a-name150150"></a><a name="1.5.0"/>1.5.0
* Dodaj skrót & zakres partycji rozwiązujący pomagające dzielenia na fragmenty aplikacji między wieloma partycjami.

### <a name="a-name142142"></a><a name="1.4.2"/>1.4.2
* Implementuje Upsert. Dodane w celu obsługi funkcji Upsert nowych metod UpsertXXX.
* Na podstawie Identyfikatora wdrożenie routingu. Brak zmian publicznego interfejsu API, wszystkie zmiany wewnętrznego.

### <a name="a-name120120"></a><a name="1.2.0"/>1.2.0
* Obsługuje dane geograficzne indeksu.
* Weryfikuje właściwość identyfikatora dla wszystkich zasobów. Identyfikatory zasobów nie może zawierać?, /, #, \, znaków ani kończyć spacją.
* Dodaje nowego nagłówka "indeksu przekształcania toku" do ResourceResponse.

### <a name="a-name110110"></a><a name="1.1.0"/>1.1.0
* Implementuje zasady indeksowania V2.

### <a name="a-name101101"></a><a name="1.0.1"/>1.0.1
* Obsługuje połączenia serwera proxy.

### <a name="a-name100100"></a><a name="1.0.0"/>1.0.0
* GA SDK.

## <a name="release--retirement-dates"></a>Wersja & wycofania dat
Firma Microsoft udostępni powiadomienia co najmniej **12 miesięcy** klienta z wyprzedzeniem wycofanie SDK w celu złagodzenia przejścia do nowszej/nieobsługiwaną wersję.

Nowe funkcje i funkcjonalność i optymalizację, które są dodawane tylko do bieżącego zestawu SDK, w związku jest zalecane, zawsze uaktualnienie SDK najnowszą tak szybko jak to możliwe. 

Każde żądanie do rozwiązania Cosmos bazy danych przy użyciu wycofane zestawu SDK będą odrzucane przez usługę.

> [!WARNING]
> Wszystkie wersje zestawu SDK usługi DocumentDB platformy Azure dla języka Python poprzedzające wersję **1.0.0** zostaną wycofane w **29 lutego 2016**. 
> 
> 

<br/>

| Wersja | Data wydania | Dacie wycofania |
| --- | --- | --- |
| [2.2.0](#2.2.0) |10 maja 2017 |--- |
| [2.1.0](#2.1.0) |01 maja 2017 r. |--- |
| [2.0.1](#2.0.1) |30 października 2016 r. |--- |
| [2.0.0](#2.0.0) |29 wrześniu 2016 r. |--- |
| [1.9.0](#1.9.0) |07 lipca 2016 r. |--- |
| [1.8.0](#1.8.0) |14 czerwca 2016 r. |--- |
| [1.7.0](#1.7.0) |26 kwietnia 2016 r. |--- |
| [1.6.1](#1.6.1) |08 kwietnia 2016 r. |--- |
| [1.6.0](#1.6.0) |29 marca 2016 r. |--- |
| [1.5.0](#1.5.0) |03 stycznia 2016 r. |--- |
| [1.4.2](#1.4.2) |06 października 2015 |--- |
| [1.4.1](#1.4.1) |06 października 2015 |--- |
| [1.2.0](#1.2.0) |06 sierpień 2015 |--- |
| [1.1.0](#1.1.0) |09 lipca 2015 r. |--- |
| [1.0.1](#1.0.1) |25 maja 2015 r. |--- |
| [1.0.0](#1.0.0) |07 kwietnia 2015 r. |--- |
| 0.9.4-prelease |14 stycznia 2015 r. |29 lutego 2016 r. |
| 0.9.3-prelease |09 grudnia 2014 r. |29 lutego 2016 r. |
| 0.9.2-prelease |25 listopada 2014 r. |29 lutego 2016 r. |
| 0.9.1-prelease |23 września 2014 r. |29 lutego 2016 r. |
| 0.9.0-prelease |21 sierpnia 2014 r. |29 lutego 2016 r. |

## <a name="faq"></a>Często zadawane pytania
[!INCLUDE [cosmos-db-sdk-faq](../../includes/cosmos-db-sdk-faq.md)]

## <a name="see-also"></a>Zobacz też
Aby dowiedzieć się więcej na temat rozwiązania Cosmos bazy danych, zobacz [bazy danych programu Microsoft Azure rozwiązania Cosmos](https://azure.microsoft.com/services/cosmos-db/) stronę usługi. 

