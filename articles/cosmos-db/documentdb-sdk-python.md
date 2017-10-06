---
title: "aaaAzure rozwiązania Cosmos DB Python interfejsu API zestawu SDK i zasoby | Dokumentacja firmy Microsoft"
description: "Dowiedz się wszystkiego o hello interfejsu API języka Python i zestawu SDK, w tym daty wydania, daty wycofania i zmiany między poszczególnymi wersjami hello Azure rozwiązania Cosmos DB Python SDK."
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
ms.openlocfilehash: 1a164b72d2bd819de87df0229357b82e2177af2f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
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

<tr><td>**Współtworzenia tooSDK**</td><td>[GitHub](https://github.com/Azure/azure-documentdb-python)</td></tr>

<tr><td>**Wprowadzenie**</td><td>[Rozpoczynanie pracy z hello zestaw SDK Python](documentdb-python-application.md)</td></tr>

<tr><td>**Bieżący obsługiwanych platform**</td><td>[Python 2.7](https://www.python.org/downloads/) i [Python 3.5](https://www.python.org/downloads/)</td></tr>
</table></br>

## <a name="release-notes"></a>Informacje o wersji
### <a name="a-name220220"></a><a name="2.2.0"/>2.2.0
* Dodano obsługę nowego poziomu spójności o nazwie ConsistentPrefix.


### <a name="a-name210210"></a><a name="2.1.0"/>2.1.0
* Dodano obsługę zapytań agregacji (COUNT, MIN, MAX, SUM i Śr.).
* Dodano opcję wyłączenia weryfikacji protokołu SSL podczas uruchamiania emulatora DB rozwiązania Cosmos.
* Usunąć ograniczenia hello zależnych żądań modułu toobe dokładnie 2.10.0.
* Obniżony minimalnej przepustowości w kolekcji partycjonowanych z RU/s 10,100 too2500 RU/s.
* Dodano obsługę Włączanie rejestrowania skryptu podczas wykonywania procedury składowanej.
* Wersja interfejsu API REST za upadku "2017-01-19' w tej wersji.

### <a name="a-name201201"></a><a name="2.0.1"/>2.0.1
* Wprowadzone zmiany redakcyjne toodocumentation komentarze.

### <a name="a-name200200"></a><a name="2.0.0"/>2.0.0
* Dodano obsługę języka Python 3.5.
* Dodano obsługę dla puli połączeń przy użyciu modułu żądania.
* Dodano obsługę spójność sesji.
* Dodano obsługę TOP/ORDERBY zapytania dla kolekcji partycjonowanych.

### <a name="a-name190190"></a><a name="1.9.0"/>1.9.0
* Obsługa zasad dodano ponownych prób dla żądań z ograniczeniem przepustowości. (Ograniczeniem przepustowości żądania odbierania żądania szybkość zbyt duży wyjątek, kod błędu 429.) Domyślnie bazy danych Azure rozwiązania Cosmos ponowi próbę dziewięciokrotnie dla każdego żądania po napotkaniu błędu kodu 429 ramach czasu retryAfter hello hello nagłówka odpowiedzi. Czas interwału ponawiania stałym teraz można ustawić jako część hello RetryOptions właściwości w obiekcie ConnectionPolicy hello Jeśli czas retryAfter hello tooignore zwrócony przez serwer między kolejnymi próbami hello. Azure DB rozwiązania Cosmos teraz czeka na maksymalnie 30 sekund na każde żądanie jest ograniczane (niezależnie od liczby ponownych prób) i zwracającej odpowiedź hello 429 kod błędu. Teraz również może zostać zastąpiona w hello RetryOptions właściwości w obiekcie ConnectionPolicy.
* Rozwiązania cosmos DB teraz zwraca x-ms ograniczania liczby ponownych prób i x-ms-throttle-retry-wait-time-ms hello nagłówków odpowiedzi w każdego żądania toodenote hello ograniczania hello i liczba cummulative godzina ponowienia hello żądania oczekiwano między kolejnymi próbami hello.
* Klasa RetryPolicy hello usunięte i odpowiadających im właściwości hello (retry_policy) widoczne w klasie document_client hello i zamiast tego wprowadzono klasy RetryOptions udostępnianie właściwości RetryOptions hello ConnectionPolicy klasy, które mogą być używane toooverride Opcje niektóre domyślne hello ponawiania.

### <a name="a-name180180"></a><a name="1.8.0"/>1.8.0
* Hello dodano obsługę konta w przypadku bazy danych.

### <a name="a-name170170"></a><a name="1.7.0"/>1.7.0
* Witaj dodano obsługę funkcji tooLive(TTL) czasu dla dokumentów.

### <a name="a-name161161"></a><a name="1.6.1"/>1.6.1
* Poprawki błędów związanych z tooserver po stronie tooallow znaki specjalne w ścieżce partitionkey partycjonowania.

### <a name="a-name160160"></a><a name="1.6.0"/>1.6.0
* Zaimplementowane [kolekcje partycjonowane](partition-data.md) i [poziomy wydajności zdefiniowanych przez użytkownika](performance-levels.md). 

### <a name="a-name150150"></a><a name="1.5.0"/>1.5.0
* Dodaj skrót & zakres tooassist rozpoznawania nazw partycji z aplikacjami dzielenia na fragmenty między wieloma partycjami.

### <a name="a-name142142"></a><a name="1.4.2"/>1.4.2
* Implementuje Upsert. Nowych metod UpsertXXX dodać toosupport Upsert funkcji.
* Na podstawie Identyfikatora wdrożenie routingu. Brak zmian publicznego interfejsu API, wszystkie zmiany wewnętrznego.

### <a name="a-name120120"></a><a name="1.2.0"/>1.2.0
* Obsługuje dane geograficzne indeksu.
* Weryfikuje właściwość identyfikatora dla wszystkich zasobów. Identyfikatory zasobów nie może zawierać?, /, #, \, znaków ani kończyć spacją.
* Dodaje nowy tooResourceResponse "postępu przekształcania indeksu" nagłówka.

### <a name="a-name110110"></a><a name="1.1.0"/>1.1.0
* Implementuje zasady indeksowania V2.

### <a name="a-name101101"></a><a name="1.0.1"/>1.0.1
* Obsługuje połączenia serwera proxy.

### <a name="a-name100100"></a><a name="1.0.0"/>1.0.0
* GA SDK.

## <a name="release--retirement-dates"></a>Wersja & wycofania dat
Firma Microsoft udostępni powiadomienia co najmniej **12 miesięcy** klienta z wyprzedzeniem wycofanie SDK w kolejności toosmooth hello przejścia tooa nowszej/nieobsługiwaną wersję.

Nowe funkcje i funkcjonalność i optymalizację, które są dodawane tylko bieżącego toohello SDK, jak jest możliwie jak najszybciej zaleca tego należy zawsze uaktualnienia toohello najnowsze wersja zestawu SDK. 

Wszystkie żądania tooCosmos bazy danych przy użyciu wycofane zestawu SDK będą odrzucane przez usługę hello.

> [!WARNING]
> Wszystkie wersje hello zestawu SDK usługi Azure DocumentDB do poprzedniego tooversion Python **1.0.0** zostaną wycofane w **29 lutego 2016**. 
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
toolearn więcej informacji na temat rozwiązania Cosmos bazy danych, zobacz [bazy danych programu Microsoft Azure rozwiązania Cosmos](https://azure.microsoft.com/services/cosmos-db/) stronę usługi. 

