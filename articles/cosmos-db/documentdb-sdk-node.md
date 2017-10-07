---
title: "aaaAzure rozwiązania Cosmos interfejsu API środowiska Node.js DB, zestaw SDK i zasoby | Dokumentacja firmy Microsoft"
description: "Dowiedz się wszystkiego o hello interfejsu API środowiska Node.js i zestawu SDK, w tym daty wydania, daty wycofania i zmiany między poszczególnymi wersjami hello Azure rozwiązania Cosmos DB Node.js SDK."
services: cosmos-db
documentationcenter: nodejs
author: rnagpal
manager: jhubbard
editor: cgronlun
ms.assetid: 9d5621fa-0e11-4619-a28b-a19d872bcf37
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: article
ms.date: 08/14/2017
ms.author: rnagpal
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: d450b9a9ea7b0f4717ddae8940121fc458ea3744
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-nodejs-sdk-release-notes-and-resources"></a>Zestaw SDK platformy Azure rozwiązania Cosmos DB Node.js: Informacje o wersji i zasoby
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

<tr><td>**Pobierz zestaw SDK**</td><td>[NPM](https://www.npmjs.com/package/documentdb)</td></tr>

<tr><td>**Dokumentacja interfejsu API**</td><td>[Dokumentacji interfejsu API środowiska node.js](http://azure.github.io/azure-documentdb-node/DocumentClient.html)</td></tr>

<tr><td>**Instrukcje dotyczące instalacji zestawu SDK**</td><td>[Instrukcje dotyczące instalacji](http://azure.github.io/azure-documentdb-node/)</td></tr>

<tr><td>**Współtworzenia tooSDK**</td><td>[GitHub](https://github.com/Azure/azure-documentdb-node/tree/master/source)</td></tr>

<tr><td>**Przykłady**</td><td>[Przykłady kodu node.js](documentdb-nodejs-samples.md)</td></tr>

<tr><td>**Samouczek z wprowadzeniem**</td><td>[Rozpoczynanie pracy z hello Node.js SDK](documentdb-nodejs-get-started.md)</td></tr>

<tr><td>**Samouczek aplikacji sieci Web**</td><td>[Tworzenie aplikacji sieci web Node.js za pomocą bazy danych Azure rozwiązania Cosmos](documentdb-nodejs-application.md)</td></tr>

<tr><td>**Bieżący obsługiwanych platform**</td><td> 
[6.x node.js](https://nodejs.org/en/blog/release/v6.10.3/)<br/> 
[Node.js v4.2.0](https://nodejs.org/en/blog/release/v4.2.0/)<br/> 
[Node.js v0.12](https://nodejs.org/en/blog/release/v0.12.0/)<br/> 
[Node.js v0.10](https://nodejs.org/en/blog/release/v0.10.0/) 
</td></tr>
</table></br>

## <a name="release-notes"></a>Informacje o wersji

### <a name="1.12.2"/>1.12.2</a>
*   Dokumentacja programu npm stałej.

### <a name="1.12.1"/>1.12.1</a>
* Stała usterki executeStoredProcedure, w którym dokumenty ma specjalne znaków Unicode (LS, PS).
* Stałe usterki w obsłudze dokumenty zawierające znaki Unicode w hello klucza partycji.
* Stały obsługę tworzenia kolekcji hello nazwa nośnika. Problem Github #114.
* Stałe obsługę token autoryzacji uprawnień. Problem Github #178.

### <a name="1.12.0"/>1.12.0</a>
* Dodano nową obsługę [poziomu spójności](consistency-levels.md) o nazwie ConsistentPrefix.
* Dodano obsługę UriFactory.
* Stałe błędów obsługę standardu Unicode. Problem GitHub #171.

### <a name="1.11.0"/>1.11.0</a>
* Obsługa hello dodanych zapytań agregacji (COUNT, MIN, MAX, SUM i Śr.).
* Opcja hello dodany do kontrolowania stopień równoległości dla wielu partycji zapytań.
* Opcja dodano hello wyłączenie protokołu SSL weryfikacji podczas uruchamiania emulatora DB rozwiązania Cosmos Azure.
* Obniżony minimalnej przepustowości w kolekcji partycjonowanych z RU/s 10,100 too2500 RU/s.
* Stałe hello kontynuacji tokenu usterki dla kolekcji jednej partycji. Problem Github #107.
* Błąd executeStoredProcedure hello stałej w obsługi 0 jako pojedynczy parametr. Problem Github #155.

### <a name="1.10.2"/>1.10.2</a>
* Stałe agenta użytkownika nagłówka tooinclude hello zestawu SDK w wersji.
* Oczyszczanie kodu pomocniczych.

### <a name="1.10.1"/>1.10.1</a>
* Wyłączanie weryfikacji SSL, używając hello SDK tootarget hello emulator(hostname=localhost).
* Dodano obsługę Włączanie rejestrowania skryptu podczas wykonywania procedury składowanej.

### <a name="1.10.0"/>1.10.0</a>
* Dodano obsługę dla wielu partycji zapytania równoległe.
* Dodano obsługę TOP/ORDER BY zapytania dla kolekcji partycjonowanych.

### <a name="1.9.0"/>1.9.0</a>
* Obsługa zasad dodano ponownych prób dla żądań z ograniczeniem przepustowości. (Ograniczeniem przepustowości żądania odbierania żądania szybkość zbyt duży wyjątek, kod błędu 429.) Domyślnie bazy danych Azure rozwiązania Cosmos ponowi próbę dziewięciokrotnie dla każdego żądania po napotkaniu błędu kodu 429 ramach czasu retryAfter hello hello nagłówka odpowiedzi. Czas interwału ponawiania stałym teraz można ustawić jako część hello RetryOptions właściwości w obiekcie ConnectionPolicy hello Jeśli czas retryAfter hello tooignore zwrócony przez serwer między kolejnymi próbami hello. Azure DB rozwiązania Cosmos teraz czeka na maksymalnie 30 sekund na każde żądanie jest ograniczane (niezależnie od liczby ponownych prób) i zwracającej odpowiedź hello 429 kod błędu. Teraz zostać zastąpiona w taki sposób, w hello RetryOptions właściwości w obiekcie ConnectionPolicy.
* Rozwiązania cosmos DB teraz zwraca x-ms ograniczania liczby ponownych prób i x-ms-throttle-retry-wait-time-ms hello i liczba skumulowany czas hello żądania oczekiwano między kolejnymi próbami hello ponów próbę hello nagłówków odpowiedzi w ograniczania hello toodenote każdego żądania.
* Dodano Hello klasy RetryOptions udostępnianie właściwości RetryOptions hello na powitania ConnectionPolicy klasy, które mogą być używane toooverride niektóre hello domyślne opcje ponawiania.

### <a name="1.8.0"/>1.8.0</a>
* Hello dodano obsługę konta w przypadku bazy danych.

### <a name="1.7.0"/>1.7.0</a>
* Witaj dodano obsługę funkcji tooLive(TTL) czasu dla dokumentów.

### <a name="1.6.0"/>1.6.0</a>
* Zaimplementowane [kolekcje partycjonowane](partition-data.md) i [poziomy wydajności zdefiniowanych przez użytkownika](performance-levels.md).

### <a name="1.5.6"/>1.5.6</a>
* Stałe usterki RangePartitionResolver.resolveForRead gdzie nie został zwrócił łącza powodu tooa concat nieprawidłowych wyników.

### <a name="1.5.5"/>1.5.5</a>
* Stałe hashParitionResolver resolveForRead(): gdy nie podany klucz partycji została Zgłaszanie wyjątku, zamiast zwracać listę wszystkich zarejestrowanych łączy.

### <a name="1.5.4"/>1.5.4</a>
* Rozwiązuje problem [#100](https://github.com/Azure/azure-documentdb-node/issues/100) -agenta w wersji dedykowanej HTTPS: unikać modyfikacji hello globalne agenta do celów bazy danych Azure rozwiązania Cosmos. Użyj dedykowanych agenta dla wszystkich żądań hello lib.

### <a name="1.5.3"/>1.5.3</a>
* Rozwiązuje problem [#81](https://github.com/Azure/azure-documentdb-node/issues/81) — poprawnie obsłużyć myślniki identyfikatory nośników.

### <a name="1.5.2"/>1.5.2</a>
* Rozwiązuje problem [#95](https://github.com/Azure/azure-documentdb-node/issues/95) -odbiornika EventEmitter wyciek ostrzeżenie.

### <a name="1.5.1"/>1.5.1</a>
* Rozwiązuje problem [#92](https://github.com/Azure/azure-documentdb-node/issues/90) — Zmień nazwę folderu toohash wyznaczania wartości skrótu dla systemów z uwzględnieniem wielkości liter.

### <a name="1.5.0"/>1.5.0</a>
* Implementowanie obsługi dzielenia na fragmenty przez dodanie skrótów & zakres rozpoznawania nazw partycji.

### <a name="1.4.0"/>1.4.0</a>
* Implementuje Upsert. Nowych metod upsertXXX na documentClient.

### <a name="1.3.0"/>1.3.0</a>
* Numery wersji pominięto toobring wyrównania z innych zestawów SDK.

### <a name="1.2.2"/>1.2.2</a>
* Q podziału niesie obietnice otoki toonew repozytorium.
* Plik toopackage aktualizacji rejestru npm.

### <a name="1.2.1"/>1.2.1</a>
* Implementuje identyfikator oparte na routingu.
* Rozwiązuje problem [#49](https://github.com/Azure/azure-documentdb-node/issues/49) -bieżącej właściwości powoduje konflikt z obiekt current() metody.

### <a name="1.2.0"/>1.2.0</a>
* Dodano obsługę dla indeksu dane geograficzne.
* Weryfikuje właściwość identyfikatora dla wszystkich zasobów. Identyfikatory zasobów nie może zawierać?, /, # &#47; &#47; znaków ani kończyć spacją.
* Dodaje nowy tooResourceResponse "postępu przekształcania indeksu" nagłówka.

### <a name="1.1.0"/>1.1.0</a>
* Implementuje zasady indeksowania V2.

### <a name="1.0.3"/>1.0.3</a>
* Problem [#40](https://github.com/Azure/azure-documentdb-node/issues/40) — zaimplementowana eslint grunt konfiguracje podstawowe hello i promise zestawu SDK.

### <a name="1.0.2"/>1.0.2</a>
* Problem [#45](https://github.com/Azure/azure-documentdb-node/issues/45) -otoki ze zobowiązania nie zawiera nagłówka z powodu błędu.

### <a name="1.0.1"/>1.0.1</a>
* Możliwości implementowane tooquery konflikty, dodając readConflicts, readConflictAsync i queryConflicts.
* Zaktualizowana dokumentacja interfejsu API.
* Problem [#41](https://github.com/Azure/azure-documentdb-node/issues/41) — błąd client.createDocumentAsync.

### <a name="1.0.0"/>1.0.0</a>
* GA SDK.

## <a name="release--retirement-dates"></a>Wersja & daty wycofania
Firma Microsoft udostępnia powiadomienia co najmniej **12 miesięcy** klienta z wyprzedzeniem wycofanie SDK w kolejności toosmooth hello przejścia tooa nowszej/nieobsługiwaną wersję.

Nowe funkcje i funkcjonalność i optymalizację, które są dodawane tylko toohello bieżącego zestawu SDK, w związku zaleca się tego należy zawsze uaktualnienia toohello najnowszego zestawu SDK w wersji możliwie jak najszybciej.

Każde żądanie tooCosmos bazy danych przy użyciu wycofane zestawu SDK jest odrzucane przez usługę hello.

<br/>

| Wersja | Data wydania | Dacie wycofania |
| --- | --- | --- |
| [1.12.2](#1.12.2) |10 sierpnia 2017 r. |--- |
| [1.12.1](#1.12.1) |10 sierpnia 2017 r. |--- |
| [1.12.0](#1.12.0) |10 maja 2017 |--- |
| [1.11.0](#1.11.0) |16 marca 2017 r. |--- |
| [1.10.2](#1.10.2) |27 stycznia 2017 r. |--- |
| [1.10.1](#1.10.1) |22 grudnia 2016 r. |--- |
| [1.10.0](#1.10.0) |03 października 2016 r. |--- |
| [1.9.0](#1.9.0) |07 lipca 2016 r. |--- |
| [1.8.0](#1.8.0) |14 czerwca 2016 r. |--- |
| [1.7.0](#1.7.0) |26 kwietnia 2016 r. |--- |
| [1.6.0](#1.6.0) |29 marca 2016 r. |--- |
| [1.5.6](#1.5.6) |08 marca 2016 r. |--- |
| [1.5.5](#1.5.5) |02 lutego 2016 r. |--- |
| [1.5.4](#1.5.4) |01 lutego 2016 r. |--- |
| [1.5.2](#1.5.2) |26 stycznia 2016 r. |--- |
| [1.5.2](#1.5.2) |22 stycznia 2016 r. |--- |
| [1.5.1](#1.5.1) |4 stycznia 2016 r. |--- |
| [1.5.0](#1.5.0) |31 grudnia 2015 r. |--- |
| [1.4.0](#1.4.0) |06 października 2015 |--- |
| [1.3.0](#1.3.0) |06 października 2015 |--- |
| [1.2.2](#1.2.2) |10 września 2015 |--- |
| [1.2.1](#1.2.1) |15 sierpnia 2015 |--- |
| [1.2.0](#1.2.0) |05 sierpnia 2015 |--- |
| [1.1.0](#1.1.0) |09 lipca 2015 r. |--- |
| [1.0.3](#1.0.3) |04 czerwiec 2015 r. |--- |
| [1.0.2](#1.0.2) |23 maja 2015 r. |--- |
| [1.0.1](#1.0.1) |15 maja 2015 r. |--- |
| [1.0.0](#1.0.0) |08 kwietnia 2015 r. |--- |

## <a name="faq"></a>Często zadawane pytania
[!INCLUDE [cosmos-db-sdk-faq](../../includes/cosmos-db-sdk-faq.md)]

## <a name="see-also"></a>Zobacz też
toolearn więcej informacji na temat rozwiązania Cosmos bazy danych, zobacz [bazy danych programu Microsoft Azure rozwiązania Cosmos](https://azure.microsoft.com/services/cosmos-db/) stronę usługi.

