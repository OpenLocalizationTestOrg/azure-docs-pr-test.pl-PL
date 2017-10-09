---
title: "aaaSQL zapytania metryki dla usługi interfejsu API Azure rozwiązania Cosmos bazy danych usługi DocumentDB | Dokumentacja firmy Microsoft"
description: "Więcej informacji na temat sposobu tooinstrument i debugowania hello wydajność kwerend SQL Azure DB rozwiązania Cosmos żądań."
keywords: "Składnia SQL, zapytanie sql, zapytania sql, język zapytań json, koncepcje bazy danych i zapytania sql, funkcje agregujące"
services: cosmos-db
documentationcenter: 
author: arramac
manager: jhubbard
editor: monicar
ms.assetid: b2fa8e8f-7291-45a3-9bd1-7284ed9077f8
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/15/2017
ms.author: arramac
ms.openlocfilehash: 2fee3786b7d48d254162699471943e316764b003
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tuning-query-performance-with-azure-cosmos-db"></a>Dostrajanie wydajności kwerend z bazy danych Azure rozwiązania Cosmos
Udostępnia bazę danych systemu Azure rozwiązania Cosmos [interfejsu API SQL na potrzeby zapytań o dane](documentdb-sql-query.md), bez konieczności schematu lub indeksów pomocniczych. Ten artykuł zawiera następujące informacje dla deweloperów hello:

* Ogólne szczegóły dotyczące sposobu działania wykonanie kwerendy SQL Azure rozwiązania Cosmos DB
* Szczegółowe informacje o nagłówkach żądań i odpowiedzi zapytania i opcje zestawu SDK klienta
* Wskazówki i najlepsze rozwiązania dotyczące wydajności zapytań
* Przykłady sposobu toodebug statystyk wykonywania SQL tooutilize kwerendy wydajności

## <a name="about-sql-query-execution"></a>Wykonanie kwerendy SQL — informacje

W usłudze Azure DB rozwiązania Cosmos, przechowywanie danych w kontenerach, które mogą rosnąć tooany [rozmiaru lub żądania przepływności](partition-data.md). Azure DB rozwiązania Cosmos bezproblemowo skaluje danych przez fizyczne partycji w ramach przyrostu danych toohandle obejmuje hello lub wzrost udostępnionej przepływności. Można wydać kontenera tooany zapytań SQL przy użyciu hello interfejsu API REST lub jednego z obsługiwanych hello [zestawów SDK usługi DocumentDB](documentdb-sdk-dotnet.md).

Krótki przegląd partycjonowania: Definiowanie klucza partycji, takich jak "Miasto", który określa sposób danych jest podzielić na partycje fizycznych. Klucz jednej partycji tooa należące danych (na przykład "Miasto" == "Seattle") są przechowywane w partycji fizycznej, ale zwykle jednej partycji fizycznej ma wiele kluczy partycji. Gdy partycji osiągnie rozmiar magazynu, hello usługa bezproblemowo dzieli partycji hello na dwóch nowych partycji i dzieli klucza partycji hello równomiernie między tych partycji. Ponieważ partycje są przejściowe, hello interfejsów API użyć abstrakcję "zakresem kluczy partycji", oznaczająca hello zakresy wartości skrótów klucza partycji. 

Podczas generowania zapytania tooAzure DB rozwiązania Cosmos hello SDK wykonuje te kroki logiczne:

* Przeanalizować plan wykonania zapytania hello toodetermine hello SQL zapytań. 
* Jeśli zapytanie hello zawiera filtru względem hello klucza partycji, takich jak `SELECT * FROM c WHERE c.city = "Seattle"`, jest kierowany tooa pojedynczy partycji. Jeśli hello zapytanie nie ma filtr klucza partycji, a następnie jest wykonywany w wszystkie partycje, a wyniki są łączone po stronie klienta.
* Hello zapytanie jest wykonywane w ramach każdej partycji w serii lub równoległego, na podstawie konfiguracji klienta. W ramach każdej partycji hello zapytanie może być jeden lub więcej rund w zależności od złożoności zapytania hello, skonfigurowany rozmiar strony, a elastycznie przepływność kolekcji hello. Każde wykonanie zwraca liczbę hello [jednostek żądania](request-units.md) używane przez wykonanie zapytania i opcjonalnie statystyk wykonywania zapytań. 
* Hello SDK wykonuje podsumowania wyników zapytania hello na partycje. Na przykład jeśli zapytanie hello obejmuje ORDER BY w partycji, wyniki z poszczególnych partycji są sortowane scalania tooreturn wyniki globalnie posortowane. Jeśli zapytanie hello jest agregacją, takich jak `COUNT`, liczby hello z poszczególnych partycji jest równy określonemu procentowi tooproduce hello ogólnej liczby.

Witaj zestawy SDK zapewniają różne opcje w celu wykonywania zapytań. Na przykład w środowisku .NET te opcje są dostępne w hello `FeedOptions` klasy. Witaj poniższej tabeli opisano te opcje i ich wpływ na czas wykonania zapytania. 

| Opcja | Opis |
| ------ | ----------- |
| `EnableCrossPartitionQuery` | Należy ustawić tootrue dla dowolnego zapytania, które wymaga toobe wykonywane przez więcej niż jednej partycji. Jest to jawne flagi tooenable możesz toomake kompromisy świadome wydajności w czasie tworzenia. |
| `EnableScanInQuery` | Musi być ustawiona tootrue, jeśli zdecydowano poza indeksowania, ale mimo to chcesz toorun hello zapytania za pomocą skanowania. Tylko dotyczy indeksowania hello zażądał filtr ścieżki jest wyłączona. | 
| `MaxItemCount` | Witaj maksymalną liczbę elementów tooreturn na serwer toohello obiegu. Ustawienie zbyt-1, możesz pozwolić, aby powitania serwera zarządzania hello liczbę elementów. Alternatywnie można obniżyć tooretrieve to wartość tylko niewielka liczba elementów na obiegu. 
| `MaxBufferedItemCount` | Jest to opcja po stronie klienta i używane zużycie pamięci hello toolimit, podczas wykonywania różnych partycji ORDER BY. Wyższa wartość pomaga zmniejszenia opóźnienia hello sortowania różnych partycji. |
| `MaxDegreeOfParallelism` | Pobiera lub ustawia hello liczba jednoczesnych operacji podczas równoległego wykonywania zapytań w hello usługi Azure DocumentDB bazy danych należy uruchomić po stronie klienta. Wartość właściwości dodatnią ogranicza hello liczbę jednoczesnych operacji toohello ustaw wartość. Jeśli jest ustawiona tooless niż 0, hello system automatycznie decyduje hello liczba jednoczesnych operacji toorun. |
| `PopulateQueryMetrics` | Czas ładowania umożliwia szczegółowe rejestrowanie statystyk czasu trwania fazy wykonywania zapytania, takie jak czas kompilacji, czas pętli indeksu i dokumentu. Problemy z wydajnością zapytania toodiagnose pomocą techniczną platformy Azure mogą udostępniać dane wyjściowe statystyki zapytania. |
| `RequestContinuation` | Wykonanie kwerendy można wznowić przez przekazywanie token kontynuacji nieprzezroczyste hello zwrócony przez każde zapytanie. token kontynuacji Hello hermetyzuje stan wszystkich wymaganych do wykonywania zapytań. |
| `ResponseContinuationTokenLimitInKb` | Można ograniczyć hello maksymalny rozmiar hello token kontynuacji zwrócony przez serwer hello. Może być potrzebny tooset tego hosta aplikacji ma limity rozmiaru nagłówka odpowiedzi. To ustawienie może zwiększyć hello ogólny czas trwania i RUs używane dla hello zapytania.  |

Na przykład wytłumaczone przedstawiono przykładowe zapytanie na klucz partycji, Żądana kolekcja o `/city` jako partycja hello klucza i elastycznie o 100 000 RU/s przepustowości. To zapytanie przy użyciu żądania `CreateDocumentQuery<T>` w środowisku .NET, takie jak następujące hello:

```cs
IDocumentQuery<dynamic> query = client.CreateDocumentQuery(
    UriFactory.CreateDocumentCollectionUri(DatabaseName, CollectionName), 
    "SELECT * FROM c WHERE c.city = 'Seattle'", 
    new FeedOptions 
    { 
        PopulateQueryMetrics = true, 
        MaxItemCount = -1, 
        MaxDegreeOfParallelism = -1, 
        EnableCrossPartitionQuery = true 
    }).AsDocumentQuery();

FeedResponse<dynamic> result = await query.ExecuteNextAsync();
```

Witaj fragment SDK przedstawionych powyżej, odpowiada toohello następujące żądania interfejsu API REST:

```
POST https://arramacquerymetrics-westus.documents.azure.com/dbs/db/colls/sample/docs HTTP/1.1
x-ms-continuation: 
x-ms-documentdb-isquery: True
x-ms-max-item-count: -1
x-ms-documentdb-query-enablecrosspartition: True
x-ms-documentdb-query-parallelizecrosspartitionquery: True
x-ms-documentdb-query-iscontinuationexpected: True
x-ms-documentdb-populatequerymetrics: True
x-ms-date: Tue, 27 Jun 2017 21:52:18 GMT
authorization: type%3dmaster%26ver%3d1.0%26sig%3drp1Hi83Y8aVV5V6LzZ6xhtQVXRAMz0WNMnUuvriUv%2b4%3d
x-ms-session-token: 7:8,6:2008,5:8,4:2008,3:8,2:2008,1:8,0:8,9:8,8:4008
Cache-Control: no-cache
x-ms-consistency-level: Session
User-Agent: documentdb-dotnet-sdk/1.14.1 Host/32-bit MicrosoftWindowsNT/6.2.9200.0
x-ms-version: 2017-02-22
Accept: application/json
Content-Type: application/query+json
Host: arramacquerymetrics-westus.documents.azure.com
Content-Length: 52
Expect: 100-continue

{"query":"SELECT * FROM c WHERE c.city = 'Seattle'"}
```

Każdej stronie wykonywania zapytania odpowiada tooa interfejsu API REST `POST` z hello `Accept: application/query+json` nagłówka i hello zapytanie SQL w treści hello. Każde zapytanie sprawia, że jeden lub więcej server toohello komunikacji dwustronnej z hello `x-ms-continuation` token powtarzana między wykonaniem tooresume powitania klienta i serwera. Opcje konfiguracji Hello w FeedOptions są przekazywane toohello serwera w formie hello nagłówki żądania. Na przykład `MaxItemCount` odpowiada za`x-ms-max-item-count`. 

Witaj żądania zwraca następujące hello (obcięty dla czytelności) odpowiedzi:

```
HTTP/1.1 200 Ok
Cache-Control: no-store, no-cache
Pragma: no-cache
Transfer-Encoding: chunked
Content-Type: application/json
Server: Microsoft-HTTPAPI/2.0
Strict-Transport-Security: max-age=31536000
x-ms-last-state-change-utc: Tue, 27 Jun 2017 21:01:57.561 GMT
x-ms-resource-quota: documentSize=10240;documentsSize=10485760;documentsCount=-1;collectionSize=10485760;
x-ms-resource-usage: documentSize=1;documentsSize=884;documentsCount=2000;collectionSize=1408;
x-ms-item-count: 2000
x-ms-schemaversion: 1.3
x-ms-alt-content-path: dbs/db/colls/sample
x-ms-content-path: +9kEANVq0wA=
x-ms-xp-role: 1
x-ms-documentdb-query-metrics: totalExecutionTimeInMs=33.67;queryCompileTimeInMs=0.06;queryLogicalPlanBuildTimeInMs=0.02;queryPhysicalPlanBuildTimeInMs=0.10;queryOptimizationTimeInMs=0.00;VMExecutionTimeInMs=32.56;indexLookupTimeInMs=0.36;documentLoadTimeInMs=9.58;systemFunctionExecuteTimeInMs=0.00;userFunctionExecuteTimeInMs=0.00;retrievedDocumentCount=2000;retrievedDocumentSize=1125600;outputDocumentCount=2000;writeOutputTimeInMs=18.10;indexUtilizationRatio=1.00
x-ms-request-charge: 604.42
x-ms-serviceversion: version=1.14.34.4
x-ms-activity-id: 0df8b5f6-83b9-4493-abda-cce6d0f91486
x-ms-session-token: 2:2008
x-ms-gatewayversion: version=1.14.33.2
Date: Tue, 27 Jun 2017 21:59:49 GMT
```

nagłówki odpowiedzi klucza Hello zwracane z kwerendy hello Uwzględnij hello następujące elementy:

| Opcja | Opis |
| ------ | ----------- |
| `x-ms-item-count` | Witaj liczbę zwracanych w odpowiedzi hello elementów. To jest zależna od hello dostarczony `x-ms-max-item-count`, hello liczba elementów, które można zmieścić w ramach rozmiar ładunku odpowiedzi maksymalną hello, hello udostępnionej przepływności i czasu wykonywania zapytania. |  
| `x-ms-continuation:` | wykonanie token tooresume kontynuacji Hello hello zapytania, jeśli dostępne są dodatkowe wyniki. | 
| `x-ms-documentdb-query-metrics` | Statystyka zapytania Hello hello wykonywania. Jest to ciąg rozdzielany zawierający statystyk czasu poświęcony na powitania fazy wykonywania zapytania. Jeśli zwrócony `x-ms-documentdb-populatequerymetrics` ustawiono zbyt`True`. | 
| `x-ms-request-charge` | Witaj liczba [jednostek żądania](request-units.md) używane przez hello zapytania. | 

Aby uzyskać więcej informacji o opcjach i nagłówki żądania interfejsu API REST hello, zobacz [zapytań zasobów przy użyciu interfejsu API REST usługi DocumentDB hello](https://docs.microsoft.com/rest/api/documentdb/querying-documentdb-resources-using-the-rest-api).

## <a name="best-practices-for-query-performance"></a>Najlepsze rozwiązania dotyczące wydajności zapytań
Oto Hello hello najbardziej typowych czynników, które mają wpływ na wydajność kwerend bazy danych Azure rozwiązania Cosmos. Firma Microsoft głębiej do szczegółów każdego z tych tematów w tym artykule.

| Współczynnik | Porada | 
| ------ | -----| 
| Aprowizowana przepływność | Zmierz RU dla kwerendy i zapewnić hello wymagane udostępnionej przepływności dla zapytań. | 
| Partycjonowanie i kluczy partycji | Preferuj zapytania o wartości klucza partycji hello w klauzuli filtru powitania dla małych opóźnieniach. |
| Opcje zestawu SDK i zapytań | Postępuj zgodnie z zestawu SDK najlepszych rozwiązań, takich jak bezpośrednie połączenie między i Dostosuj opcje wykonywania zapytania po stronie klienta. |
| Opóźnienie sieci | Konta dla sieci obciążenie w pomiaru i używać wielu interfejsów API tooread z hello najbliżej regionu. |
| Zasady indeksowania | Upewnij się, że masz wymagane hello ścieżki/zasady indeksowania dla zapytania hello. |
| Metryki wykonywania kwerendy | Przeanalizuj hello zapytania wykonywania metryki tooidentify potencjalnych ponownego kształtów zapytań i danych.  |

### <a name="provisioned-throughput"></a>Aprowizowana przepływność
Do rozwiązania Cosmos bazy danych możesz utworzyć kontenery danych, każda z zarezerwowaną przepływnością wyrażoną w żądaniu jednostki (RU) na sekundę. Odczyt dokumentu 1 KB jest 1 RU i każdej operacji (w tym zapytań) jest znormalizowana tooa stała liczba RUs w oparciu o jego złożoność. Na przykład, jeśli masz 1000 elastycznie RU/s dla Twojego kontenera i masz zapytania, takie jak `SELECT * FROM c WHERE c.city = 'Seattle'` która zużywa 5 RUs, a następnie przeprowadzić (1000 RU/s) / (5 RU na zapytanie) = 200 zapytania/s takie zapytania na sekundę. 

Po przesłaniu zapytania więcej niż 200 na sekundę hello usługa jest uruchamiana limitów szybkości żądań przychodzących ponad 200/s. Hello zestawy SDK automatycznie obsługi przypadek, wykonując wycofywania/ponów próbę, w związku z tym można zauważyć większego opóźnienia dla tych zapytań. Zwiększenie toohello przepływności hello udostępniane wymagana wartość zwiększa Twojego zapytania opóźnienia i przepływności. 

Zobacz toolearn więcej informacji na temat jednostek żądania [jednostek żądania](request-units.md).

### <a name="partitioning-and-partition-keys"></a>Partycjonowanie i kluczy partycji
Z bazy danych rozwiązania Cosmos platformy Azure zwykle zapytania wykonaj w powitania po zamówienia najszybszym/najbardziej efektywne tooslower/mniej wydajne. 

* Pobierz klucz jednej partycji i klucz
* Zapytanie z klauzuli filtru dla klucza jednej partycji
* Zapytanie bez klauzuli filtru równości lub zakres na dowolną właściwość
* Zapytanie bez filtrów

Bada tego tooconsult potrzeby wszystkie partycje muszą większego opóźnienia i może wykorzystać RUs wyższy. Ponieważ każda partycja zawiera automatycznego indeksowania względem wszystkich właściwości, hello zapytania mogą być przekazywane wydajnie z hello indeksu w tym przypadku. Można wykonać zapytania, obejmujące szybsze partycje przy użyciu opcji równoległości hello.

Zobacz toolearn więcej informacji na temat partycjonowania i kluczy partycji [partycjonowania w usłudze Azure DB rozwiązania Cosmos](partition-data.md).

### <a name="sdk-and-query-options"></a>Opcje zestawu SDK i zapytań
Zobacz [porady dotyczące wydajności](performance-tips.md) i [testowania wydajności](performance-testing.md) dla jak tooget hello najlepszej wydajności po stronie klienta z bazy danych usługi Azure rozwiązania Cosmos. Obejmuje to przy użyciu hello najnowsze zestawów SDK, konfigurowanie konfiguracje specyficzne dla platformy, takich jak domyślną liczbę połączeń, częstotliwość operacji wyrzucania elementów bezużytecznych i przy użyciu opcji łączności lekkie, takich jak bezpośrednio/TCP. 


#### <a name="max-item-count"></a>Liczba maksymalna liczba elementów.
W przypadku kwerend hello wartość `MaxItemCount` może mieć znaczący wpływ na czas kwerendy end-to-end. Każdy Rundy serwera toohello zwróci nie więcej niż hello liczba elementów w `MaxItemCount` (domyślnie: 100 elementów). Ustawienie tej wartości wyższej tooa (-1 jest maksymalną i zalecanym) poprawia ogólną czasu trwania kwerendy poprzez ograniczenie hello liczby rund między serwerem a klientem, szczególnie w przypadku zapytań dotyczących dużych zestawów wyników.

```cs
IDocumentQuery<dynamic> query = client.CreateDocumentQuery(
    UriFactory.CreateDocumentCollectionUri(DatabaseName, CollectionName), 
    "SELECT * FROM c WHERE c.city = 'Seattle'", 
    new FeedOptions 
    { 
        MaxItemCount = -1, 
    }).AsDocumentQuery();
```

#### <a name="max-degree-of-parallelism"></a>Maksymalny stopień równoległości
Dla zapytań, dostroić hello `MaxDegreeOfParallelism` tooidentify hello konfiguracje najlepsze dla aplikacji, zwłaszcza jeśli wykonywania zapytań między partycji (bez filtr na wartość klucza partycji hello). `MaxDegreeOfParallelism`Steruje hello maksymalną liczbę równoległych zadań, tj. hello maksymalnie toobe partycje odwiedzi równolegle. 

```cs
IDocumentQuery<dynamic> query = client.CreateDocumentQuery(
    UriFactory.CreateDocumentCollectionUri(DatabaseName, CollectionName), 
    "SELECT * FROM c WHERE c.city = 'Seattle'", 
    new FeedOptions 
    { 
        MaxDegreeOfParallelism = -1, 
        EnableCrossPartitionQuery = true 
    }).AsDocumentQuery();
```

Załóżmy, że
* D = Domyślna maksymalna liczba zadań równoległych (łączna liczba procesorów na powitania klienta maszynie =)
* P = określone przez użytkownika maksymalną liczbę równoległych zadań
* N = liczba partycji, które wymaga toobe odwiedzi odpowiedzi na kwerendę

Poniżej przedstawiono efekty zapytania równoległe hello spowoduje zachowanie dla różnych wartości P.
* (P == 0) = > Tryb szeregowe
* (P == 1) = > maksymalna jednego zadania
* (P > 1) = > zadań równoległych Min (P, N) 
* (P < 1) = > zadań równoległych Min (N, D)

Informacje o wersji zestawu SDK i Zobacz szczegóły dotyczące zaimplementowanych klasy i metody [zestawów SDK usługi DocumentDB](documentdb-sdk-dotnet.md)

### <a name="network-latency"></a>Opóźnienie sieci
Zobacz [dystrybucji globalnej bazy danych Azure rozwiązania Cosmos](tutorial-global-distribution-documentdb.md) jak tooset Konfigurowanie dystrybucji globalne i połączyć toohello najbliżej regionu. Opóźnienie sieci ma znaczący wpływ na wydajność zapytań, muszą toomake wiele rund lub pobrać dużych zestawu wyników z kwerendy hello. 

Witaj sekcji metryki wykonywania zapytania wyjaśniono, jak tooretrieve hello serwera czas wykonywania kwerend ( `totalExecutionTimeInMs`), dzięki czemu można odróżnić czas przeznaczony na wykonanie kwerendy i czas przesyłania w sieci.

### <a name="indexing-policy"></a>Zasady indeksowania
Zobacz [Konfigurowanie zasady indeksowania](indexing-policies.md) indeksowania ścieżki, rodzajów i tryby i ich wpływ na wykonanie kwerendy. Domyślnie hello indeksowania zasad używa skrótu indeksowania dla ciągów, które obowiązuje dla zapytań o równość, ale nie dla zakresu zapytania/order przez zapytania. Jeśli potrzebujesz kwerendy zakresu dla ciągów, zaleca się określenie hello typ indeksu zakresu dla wszystkich ciągów. 

## <a name="query-execution-metrics"></a>Metryki wykonywania kwerendy
Szczegółowe metryki na wykonanie kwerendy można uzyskać przez przekazywanie hello opcjonalne `x-ms-documentdb-populatequerymetrics` nagłówka (`FeedOptions.PopulateQueryMetrics` w hello zestawu .NET SDK). Wartość zwracana w Hello `x-ms-documentdb-query-metrics` ma powitania po pary klucz wartość przeznaczone do zaawansowanego rozwiązywania problemów wykonanie zapytania. 

```cs
IDocumentQuery<dynamic> query = client.CreateDocumentQuery(
    UriFactory.CreateDocumentCollectionUri(DatabaseName, CollectionName), 
    "SELECT * FROM c WHERE c.city = 'Seattle'", 
    new FeedOptions 
    { 
        PopulateQueryMetrics = true, 
    }).AsDocumentQuery();

FeedResponse<dynamic> result = await query.ExecuteNextAsync();

// Returns metrics by partition key range Id
IReadOnlyDictionary<string, QueryMetrics> metrics = result.QueryMetrics;

```

| Metryka | Jednostka | Opis | 
| ------ | -----| ----------- |
| `totalExecutionTimeInMs` | milisekundy | Czas wykonywania kwerendy | 
| `queryCompileTimeInMs` | milisekundy | Czas kompilacji kwerendy  | 
| `queryLogicalPlanBuildTimeInMs` | milisekundy | Plan logicznej zapytania toobuild czasu | 
| `queryPhysicalPlanBuildTimeInMs` | milisekundy | Plan zapytania fizycznych toobuild czasu | 
| `queryOptimizationTimeInMs` | milisekundy | Czas spędzony w zapytaniu optymalizacji | 
| `VMExecutionTimeInMs` | milisekundy | Czas spędzony w czasie wykonywania kwerendy | 
| `indexLookupTimeInMs` | milisekundy | Czas spędzony w warstwie fizycznej indeksu | 
| `documentLoadTimeInMs` | milisekundy | Czas ładowania dokumentów  | 
| `systemFunctionExecuteTimeInMs` | milisekundy | Łączny czas podczas wykonywania funkcji (wbudowane) systemu w milisekundach  | 
| `userFunctionExecuteTimeInMs` | milisekundy | Łączny czas podczas wykonywania funkcji zdefiniowanej przez użytkownika (w milisekundach) | 
| `retrievedDocumentCount` | milisekundy | Całkowita liczba pobranych dokumentów  | 
| `retrievedDocumentSize` | Bajty | Całkowity rozmiar pobrane dokumentów w bajtach  | 
| `outputDocumentCount` | Liczba | Liczba dokumentów, dane wyjściowe | 
| `writeOutputTimeInMs` | milisekundy | Czas wykonywania kwerendy w milisekundach | 
| `indexUtilizationRatio` | stosunek (< = 1) | Załadowano stosunek liczby dokumentów, które są dopasowane wg hello filtru toohello liczba dokumentów  | 

Hello klient zestawów SDK może wewnętrznie utworzyć wiele operacji tooserve hello zapytania w ramach każdej partycji. Witaj klient wysyła więcej niż jedno wywołanie każdej partycji o większym hello całkowita liczba wyników `x-ms-max-item-count`, jeśli zapytanie hello przekracza hello udostępnionej przepływności dla partycji hello, lub jeśli hello ładunek zapytania osiągnie maksymalny rozmiar hello na stronie lub jeśli hello zapytania osiągnie hello System przydzielony limit czasu. Zwraca każde wykonanie zapytania z częściowa `x-ms-documentdb-query-metrics` dla tej strony. 

Poniżej przedstawiono niektóre przykładowe zapytania i w jaki sposób toointerpret niektóre metryki hello zwrócone przez wykonanie zapytania: 

| Zapytanie | Metryka próbki | Opis | 
| ------ | -----| ----------- |
| `SELECT TOP 100 * FROM c` | `"RetrievedDocumentCount": 101` | Witaj liczba dokumentów pobierana jest 100 + 1 klauzuli TOP hello toomatch. Przede wszystkim jest zużywany czas kwerendy w `WriteOutputTime` i `DocumentLoadTime` ponieważ skanowania. | 
| `SELECT TOP 500 * FROM c` | `"RetrievedDocumentCount": 501` | RetrievedDocumentCount jest teraz nowszej (500 + 1 toomatch hello klauzuli TOP). | 
| `SELECT * FROM c WHERE c.N = 55` | `"IndexLookupTime": "00:00:00.0009500"` | Około 0,9 ms odbywa się w IndexLookupTime dla klucza wyszukiwania, ponieważ jest on wyszukiwania indeksu `/N/?`. | 
| `SELECT * FROM c WHERE c.N > 55` | `"IndexLookupTime": "00:00:00.0017700"` | Nieco więcej (1.7 ms) czas, w IndexLookupTime za pośrednictwem skanowania zakresu, ponieważ jest on wyszukiwania indeksu `/N/?`. | 
| `SELECT TOP 500 c.N FROM c` | `"IndexLookupTime": "00:00:00.0017700"` | Sam czas spędzony na `DocumentLoadTime` jako poprzednich zapytań, ale niższe `WriteOutputTime` ponieważ możemy Cię projekcji tylko jedną właściwość. | 
| `SELECT TOP 500 udf.toPercent(c.N) FROM c` | `"UserDefinedFunctionExecutionTime": "00:00:00.2136500"` | Działania o 213 ms `UserDefinedFunctionExecutionTime` wykonywania hello UDF w każdej wartości `c.N`. |
| `SELECT TOP 500 c.Name FROM c WHERE STARTSWITH(c.Name, 'Den')` | `"IndexLookupTime": "00:00:00.0006400", "SystemFunctionExecutionTime": "00:00:00.0074100"` | Działania około 0,6 ms `IndexLookupTime` na `/Name/?`. Większość hello zapytania czas wykonania (ms ~ 7) w `SystemFunctionExecutionTime`. |
| `SELECT TOP 500 c.Name FROM c WHERE STARTSWITH(LOWER(c.Name), 'den')` | `"IndexLookupTime": "00:00:00", "RetrievedDocumentCount": 2491,  "OutputDocumentCount": 500` | Ponieważ jest on używany jako skanowania jest przeprowadzana kwerenda `LOWER`, a 500 poza 2491 pobrane dokumenty zostaną zwrócone. |


## <a name="next-steps"></a>Następne kroki
* toolearn o operatorów zapytań SQL hello obsługiwane i słów kluczowych, zobacz [zapytania SQL](documentdb-sql-query.md). 
* Zobacz toolearn o jednostkach żądania [jednostek żądania](request-units.md).
* toolearn o zasady indeksowania, zobacz [indeksowania zasad](indexing-policies.md) 


