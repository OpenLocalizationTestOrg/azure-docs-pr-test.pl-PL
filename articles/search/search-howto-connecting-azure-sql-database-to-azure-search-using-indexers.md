---
title: "aaaConnecting tooAzure bazy danych SQL Azure Search przy użyciu indeksatorów | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toopull dane z bazy danych SQL Azure tooan usługi Azure Search index używanie indeksatorów."
services: search
documentationcenter: 
author: chaosrealm
manager: pablocas
editor: 
ms.assetid: e9bbf352-dfff-4872-9b17-b1351aae519f
ms.service: search
ms.devlang: rest-api
ms.workload: search
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 07/13/2017
ms.author: eugenesh
ms.openlocfilehash: b28a11cf18ef994de99e09af90bbfeb171ef3cde
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="connecting-azure-sql-database-tooazure-search-using-indexers"></a>Połączenie bazy danych SQL Azure tooAzure wyszukiwanie przy użyciu indeksatorów

Zanim można zbadać [indeksu usługi Azure Search](search-what-is-an-index.md), musisz wypełnić je z danymi. Jeśli dane hello znajduje się w bazie danych Azure SQL **indeksator usługi Azure Search bazy danych SQL Azure** (lub **indeksatora Azure SQL** skrócie) można zautomatyzować proces indeksowania hello, czyli mniej toowrite kodu i mniej Infrastruktura toocare o.

W tym artykule omówiono mechanika hello przy użyciu [indeksatory](search-indexer-overview.md), ale także w tym artykule opisano funkcje dostępne tylko w przypadku baz danych Azure SQL (na przykład zintegrowane śledzenie zmian). 

W tooAzure Dodawanie baz danych, usługi Azure Search udostępnia indeksatory dla [bazy danych Azure rozwiązania Cosmos](search-howto-index-documentdb.md), [magazynu obiektów Blob Azure](search-howto-indexing-azure-blob-storage.md), i [magazynu tabel Azure](search-howto-indexing-azure-tables.md). Obsługa toorequest dla innych źródeł danych, które zapewniają swoją opinię na powitania [forum opinii usługi Azure Search](https://feedback.azure.com/forums/263029-azure-search/).

## <a name="indexers-and-data-sources"></a>Indeksatorami i źródłami danych

A **źródła danych** Określa, które tooindex danych, poświadczenia dostępu do danych i zasad, które skutecznie zidentyfikować zmiany danych hello (nowych, zmodyfikowanych lub usuniętych wierszy). Jest on zdefiniowany jako niezależnym zasobem, dzięki czemu mogą być używane przez wiele indeksatorów.

**Indeksatora** jest z zasobem, który nawiązuje połączenie z jednym źródłem danych z indeksem wyszukiwania docelowych. Indeksator jest używany w hello następujące sposoby:

* Należy wykonać kopię jednorazowe hello danych toopopulate indeksu.
* Aktualizowanie indeksu ze zmianami w źródle danych hello zgodnie z harmonogramem.
* Uruchom na żądanie tooupdate indeksu zgodnie z potrzebami.

Jeden indeksator zajmowane tylko jedną tabelę lub widok, ale można utworzyć wiele indeksatorów, jeśli chcesz toopopulate wiele indeksów wyszukiwania. Aby uzyskać więcej informacji dotyczących pojęć, zobacz [Operacje indeksatora: typowy przepływ pracy](https://docs.microsoft.com/rest/api/searchservice/Indexer-operations#typical-workflow).

Można skonfigurować i skonfigurować indeksator Azure SQL za pomocą:

* Kreator importu danych w hello [portalu Azure](https://portal.azure.com)
* Usługa Azure Search [zestawu .NET SDK](https://docs.microsoft.com/dotnet/api/microsoft.azure.search.models.indexer?view=azure-dotnet)
* Usługa Azure Search [interfejsu API REST](https://docs.microsoft.com/en-us/rest/api/searchservice/indexer-operations)

W tym artykule, użyjemy hello interfejsu API REST toocreate **indeksatory** i **źródeł danych**.

## <a name="when-toouse-azure-sql-indexer"></a>Gdy toouse indeksatora SQL Azure
W zależności od powiązane dane tooyour kilka czynników Użyj hello indeksatora Azure SQL może lub nie może być odpowiednie. Jeśli dane spełnia następujące wymagania hello, można używać indeksatora Azure SQL.

| Kryteria | Szczegóły |
|----------|---------|
| Dane pochodzą z pojedynczej tabeli lub widoku | Jeśli dane hello są rozproszone w wielu tabel, można utworzyć jednolity obraz danych hello. Jednak jeśli używasz widoku, nie będzie możliwe toouse programu SQL Server zintegrowanego zmiany wykrywania toorefresh indeksu o zmiany przyrostowe. Aby uzyskać więcej informacji, zobacz [Przechwytywanie zmienione i usunąć wiersze](#CaptureChangedRows) poniżej. |
| Typy danych są zgodne | Większość, ale nie wszystkie typy SQL hello są obsługiwane w indeksie usługi wyszukiwanie Azure. Aby uzyskać listę, zobacz [mapowania typów danych](#TypeMapping). |
| Synchronizacja danych w czasie rzeczywistym nie jest wymagane | Indeksator można ponownie indeksu tabeli, co najwyżej co pięć minut. W przypadku zmiany danych często i hello zmiany zostaną uwzględnione w indeksie hello w ciągu sekund lub minut pojedynczego toobe muszą, firma Microsoft zaleca używanie hello [interfejsu API REST](https://docs.microsoft.com/rest/api/searchservice/AddUpdate-or-Delete-Documents) lub [zestawu .NET SDK](search-import-data-dotnet.md) toopush bezpośrednio zaktualizować wierszy. |
| Możliwe jest przyrostowe indeksowania | Jeśli masz dużych zestawów danych i indeksatora hello toorun plan zgodnie z harmonogramem, usługi Azure Search musi być w stanie tooefficiently zidentyfikować wierszy nowe, zmodyfikowane lub usunięte. Indeksowanie przyrostowe nie jest dozwolona tylko indeksowania na żądanie (nie zgodnie z harmonogramem), lub indeksowania mniej niż 100 000 wierszy. Aby uzyskać więcej informacji, zobacz [Przechwytywanie zmienione i usunąć wiersze](#CaptureChangedRows) poniżej. |

## <a name="create-an-azure-sql-indexer"></a>Utwórz indeksator Azure SQL

1. Utwórz źródło danych hello:

   ```
    POST https://myservice.search.windows.net/datasources?api-version=2016-09-01
    Content-Type: application/json
    api-key: admin-key

    {
        "name" : "myazuresqldatasource",
        "type" : "azuresql",
        "credentials" : { "connectionString" : "Server=tcp:<your server>.database.windows.net,1433;Database=<your database>;User ID=<your user name>;Password=<your password>;Trusted_Connection=False;Encrypt=True;Connection Timeout=30;" },
        "container" : { "name" : "name of hello table or view that you want tooindex" }
    }
   ```

   Można pobrać ciągu połączenia hello z hello [portalu Azure](https://portal.azure.com); Użyj hello `ADO.NET connection string` opcji.

2. Tworzenie indeksu usługi Azure Search docelowego hello, jeśli nie masz już. Można utworzyć indeksu przy użyciu hello [portal](https://portal.azure.com) lub hello [utworzyć indeks API](https://docs.microsoft.com/rest/api/searchservice/Create-Index). Upewnij się, że hello schematu indeksu docelowego jest zgodny ze schematem hello tabeli źródłowej hello — zobacz [mapowanie między SQL i usługa Azure search typy danych](#TypeMapping).

3. Utwórz indeksator hello przez nadanie mu nazwy i odwołuje się do danych hello indeksu źródłowej i docelowej:

    ```
    POST https://myservice.search.windows.net/indexers?api-version=2016-09-01
    Content-Type: application/json
    api-key: admin-key

    {
        "name" : "myindexer",
        "dataSourceName" : "myazuresqldatasource",
        "targetIndexName" : "target index name"
    }
    ```

Utworzone w ten sposób indeksatora nie ma zgodnie z harmonogramem. Automatycznie uruchomiony po po jego utworzeniu. Uruchom go ponownie w dowolnej chwili za pomocą **uruchomić indeksatora** żądania:

    POST https://myservice.search.windows.net/indexers/myindexer/run?api-version=2016-09-01
    api-key: admin-key

Można dostosować kilka aspektów zachowanie indeksatora, takich jak rozmiar partii i liczby dokumentów można pominięty zanim wykonywanie indeksatora nie powiedzie się. Aby uzyskać więcej informacji, zobacz [Tworzenie interfejsu API indeksatora](https://docs.microsoft.com/rest/api/searchservice/Create-Indexer).

Może być konieczne tooallow usług Azure tooconnect tooyour w bazie danych. Zobacz [łączenie z Azure](https://docs.microsoft.com/azure/sql-database/sql-database-firewall-configure) instrukcje na temat toodo który.

Witaj toomonitor indeksatora stan i historię wykonywania (liczba elementów indeksowane, błędów, itp.), użyj **stan indeksatora** żądania:

    GET https://myservice.search.windows.net/indexers/myindexer/status?api-version=2016-09-01
    api-key: admin-key

odpowiedź Hello powinien wyglądać podobnie toohello następujące:

    {
        "@odata.context":"https://myservice.search.windows.net/$metadata#Microsoft.Azure.Search.V2015_02_28.IndexerExecutionInfo",
        "status":"running",
        "lastResult": {
            "status":"success",
            "errorMessage":null,
            "startTime":"2015-02-21T00:23:24.957Z",
            "endTime":"2015-02-21T00:36:47.752Z",
            "errors":[],
            "itemsProcessed":1599501,
            "itemsFailed":0,
            "initialTrackingState":null,
            "finalTrackingState":null
        },
        "executionHistory":
        [
            {
                "status":"success",
                "errorMessage":null,
                "startTime":"2015-02-21T00:23:24.957Z",
                "endTime":"2015-02-21T00:36:47.752Z",
                "errors":[],
                "itemsProcessed":1599501,
                "itemsFailed":0,
                "initialTrackingState":null,
                "finalTrackingState":null
            },
            ... earlier history items
        ]
    }

Zawiera historię wykonywania zapasową too50 wykonaniami hello ostatnio zakończone, które są sortowane w kolejności chronologicznej odwrotnej hello (dzięki czemu wykonanie najnowsze hello zostanie osiągnięty jako pierwszy w odpowiedzi hello).
Dodatkowe informacje o odpowiedzi hello znajdują się w [pobierania stanu indeksatora](http://go.microsoft.com/fwlink/p/?LinkId=528198)

## <a name="run-indexers-on-a-schedule"></a>Uruchom indeksatory zgodnie z harmonogramem
Można także porządkować toorun indeksatora hello okresowo zgodnie z harmonogramem. toodo, Dodaj hello **harmonogram** właściwości podczas tworzenia lub aktualizowania hello indeksatora. przykład Witaj poniżej przedstawia PUT żądania tooupdate hello indeksatora:

    PUT https://myservice.search.windows.net/indexers/myindexer?api-version=2016-09-01
    Content-Type: application/json
    api-key: admin-key

    {
        "dataSourceName" : "myazuresqldatasource",
        "targetIndexName" : "target index name",
        "schedule" : { "interval" : "PT10M", "startTime" : "2015-01-01T00:00:00Z" }
    }

Witaj **interwał** parametr jest wymagany. Interwał powitania odwołuje się czas toohello od początku hello dwóch kolejnych indeksatora wykonaniami. najmniejsza Hello dozwolony interwał wynosi 5 minut; Najdłuższy Hello jest jeden dzień. Musi być sformatowany jako wartość XSD "dayTimeDuration" (ograniczony podzestaw [czasu trwania ISO 8601](http://www.w3.org/TR/xmlschema11-2/#dayTimeDuration) wartości). wzór Hello: `P(nD)(T(nH)(nM))`. Przykłady: `PT15M` co 15 minut, `PT2H` co 2 godziny.

opcjonalne Hello **startTime** wskazuje, kiedy hello zaplanowane wykonaniami należy rozpocząć. Jeśli zostanie pominięty, bieżący czas UTC hello jest używany. Teraz można w hello poza — w takim przypadku wykonanie pierwszej hello jest zaplanowane tak, jakby indeksatora hello działa nieprzerwanie od hello startTime.  

Tylko jeden wykonywanie indeksatora można uruchamiać jednocześnie. Jeśli indeksatora działa podczas jego wykonywania, wykonanie hello zostanie odłożona do momentu hello następnym zaplanowanym terminie.

Zastanówmy toomake przykład to bardziej konkretną. Załóżmy, że firma Microsoft hello po co godzinę skonfigurowany harmonogram:

    "schedule" : { "interval" : "PT1H", "startTime" : "2015-03-01T00:00:00Z" }

Oto, co się stanie:

1. pierwszy wykonywanie indeksatora Hello rozpoczyna się w tym miejscu lub wokół 1 marca 2015 od 12:00 CZAS UTC.
2. Załóżmy, że wykonanie tego ma 20 minut (lub w dowolnym momencie mniej niż 1 godzina).
3. Wykonanie drugiej Hello rozpoczyna się w tym miejscu lub wokół 1 marca 2015 od godziny 1:00
4. Teraz załóżmy, że wykonanie tego ma ponad godzinę — na przykład 70 minut —, więc ukończy około 2:10:00
5. Jest teraz 2:00:00, godzina hello trzeci toostart wykonywania. Jednak ponieważ hello drugiego wykonywania od 01: 00 jest nadal uruchomiony, wykonanie trzeci hello jest pominięte. wykonanie trzeci Hello rozpoczyna się od 3: 00.

Można dodać, zmienić lub usunąć harmonogram dla istniejącego indeksatora za pomocą **indeksatora PUT** żądania.

<a name="CaptureChangedRows"></a>

## <a name="capture-new-changed-and-deleted-rows"></a>Przechwytywanie nowego, zmiany i usunięcia wierszy

Usługa Azure Search korzysta **przyrostowe indeksowania** tooavoid o indeksie toore hello całej tabeli lub widoku każdym uruchomieniu indeksatora. Wyszukiwanie Azure oferuje dwa zmienić wykrywania zasady toosupport przyrostowe indeksowania. 

### <a name="sql-integrated-change-tracking-policy"></a>Zasad śledzenia zmian zintegrowane ze środowiskiem SQL
Jeśli baza danych SQL obsługuje [śledzenie zmian](https://docs.microsoft.com/sql/relational-databases/track-changes/about-change-tracking-sql-server), zaleca się używanie **SQL zintegrowane zmienić zasady śledzenia**. Jest to hello najbardziej efektywny zasad. Ponadto umożliwia wierszy tooidentify usunięte usługi Azure Search bez konieczności tooadd kolumny tabeli tooyour explicit "usuwania nietrwałego".

#### <a name="requirements"></a>Wymagania 

+ Wymagania dotyczące wersji bazy danych:
  * SQL Server 2012 z dodatkiem SP3 lub nowszym, jeśli używasz programu SQL Server na maszynach wirtualnych platformy Azure.
  * Azure SQL Database V12, jeśli używasz bazy danych SQL Azure.
+ Tabele tylko (Brak widoków). 
+ W bazie danych hello [śledzenia zmian Włącz](https://docs.microsoft.com/sql/relational-databases/track-changes/enable-and-disable-change-tracking-sql-server) hello tabeli. 
+ Nie złożonego klucza podstawowego (klucza podstawowego zawierające więcej niż jedną kolumnę) hello tabeli.  

#### <a name="usage"></a>Sposób użycia

toouse te zasady, tworzenie lub aktualizowanie źródła danych w następujący sposób:

    {
        "name" : "myazuresqldatasource",
        "type" : "azuresql",
        "credentials" : { "connectionString" : "connection string" },
        "container" : { "name" : "table or view name" },
        "dataChangeDetectionPolicy" : {
           "@odata.type" : "#Microsoft.Azure.Search.SqlIntegratedChangeTrackingPolicy"
      }
    }

Gdy za pomocą zasad, śledzenia zmian programu SQL zintegrowane nie określaj odrębne zasady usuwania i wykrywania — ta zasada ma wbudowaną obsługę identyfikowanie usuniętych wierszy. Jednak dla automagically"hello usuwa toobe wykryto" hello klucz dokumentu w indeksie wyszukiwania musi być hello taki sam jak hello klucza podstawowego w tabeli SQL hello. 

<a name="HighWaterMarkPolicy"></a>

### <a name="high-water-mark-change-detection-policy"></a>Zasady wykrywania zmian znacznik limitu górnego

Te zasady wykrywania zmian polega na kolumnę "znacznik limitu górnego" Przechwytywanie wersji hello lub godzinę ostatniej aktualizacji wiersza. Jeśli używasz widoku, musisz użyć zasad znacznik limitu górnego. Kolumna znacznik limitu górnego Hello musi spełniać hello następujące wymagania.

#### <a name="requirements"></a>Wymagania 

* Wstawia wszystkie Określ wartość dla kolumny hello.
* Elementu tooan wszystkie aktualizacje także zmienić wartość hello hello kolumny.
* Witaj wartości tej kolumny zwiększa się wraz z każdym insert lub update.
* Zapytania z hello po WHERE i klauzuli ORDER BY, które mogą być wykonywane wydajnie:`WHERE [High Water Mark Column] > [Current High Water Mark Value] ORDER BY [High Water Mark Column]`

> [!IMPORTANT] 
> Zdecydowanie zaleca się używanie hello [rowversion](https://docs.microsoft.com/sql/t-sql/data-types/rowversion-transact-sql) typu danych dla kolumny znacznik limitu górnego hello. Jeśli jest używany inny typ danych, śledzenie zmian nie jest gwarantowana toocapture wszystkie zmiany w obecności hello transakcji wykonywanych równocześnie z zapytania indeksatora. Korzystając z **rowversion** w konfiguracji z replikami tylko do odczytu, indeksatora hello musi wskazywać na powitania repliki podstawowej. Tylko replika podstawowa może służyć do scenariuszy synchronizacji danych.

#### <a name="usage"></a>Sposób użycia

toouse zasad znacznik limitu górnego, utworzyć lub zaktualizować źródła danych w następujący sposób:

    {
        "name" : "myazuresqldatasource",
        "type" : "azuresql",
        "credentials" : { "connectionString" : "connection string" },
        "container" : { "name" : "table or view name" },
        "dataChangeDetectionPolicy" : {
           "@odata.type" : "#Microsoft.Azure.Search.HighWaterMarkChangeDetectionPolicy",
           "highWaterMarkColumnName" : "[a rowversion or last_updated column name]"
      }
    }

> [!WARNING]
> Jeśli tabela źródłowa hello nie ma indeksu w kolumnie znacznik limitu górnego hello, zapytania używane przez hello SQL indeksatora może upłynął limit czasu. W szczególności hello `ORDER BY [High Water Mark Column]` klauzula wymaga wydajnie toorun indeks, gdy tabela hello zawiera wiele wierszy.
>
>

Jeśli wystąpią błędy przekroczenia limitu czasu, można użyć hello `queryTimeout` indeksatora konfiguracji ustawienie tooset hello wartość limitu czasu kwerendy tooa wyższe niż hello domyślny 5-minutowy limit czasu. Na przykład tooset hello limitu czasu too10 minut, Utwórz lub zaktualizuj indeksatora hello z hello następującej konfiguracji:

    {
      ... other indexer definition properties
     "parameters" : {
            "configuration" : { "queryTimeout" : "00:10:00" } }
    }

Można również wyłączyć hello `ORDER BY [High Water Mark Column]` klauzuli. Jednak nie jest to zalecane, ponieważ wykonywanie indeksatora hello zostało przerwane z powodu błędu, indeksatora hello czy toore proces wszystkie wiersze jeśli była uruchamiana później — nawet jeśli indeksatora hello zostały już przetworzone prawie wszystkie wiersze hello przez hello razem, gdy zostało ono przerwane. Witaj toodisable `ORDER BY` klauzuli, użyj hello `disableOrderByHighWaterMarkColumn` ustawienie w definicji indeksatora hello:  

    {
     ... other indexer definition properties
     "parameters" : {
            "configuration" : { "disableOrderByHighWaterMarkColumn" : true } }
    }

### <a name="soft-delete-column-deletion-detection-policy"></a>Elastyczne zasady usunąć wykrywania usuwanie kolumn
Usunięcie wierszy z tabeli źródłowej hello prawdopodobnie potrzebna będzie toodelete te wiersze z hello również indeksu wyszukiwania. Jeśli używasz hello SQL zintegrowane zasad śledzenia zmian, to jest poświęcony na obsługę dla Ciebie. Jednak zasad śledzenia zmian znacznik limitu górnego hello nie będą pomocne z usuniętymi wierszami. Jakie toodo?

Jeśli wierszy hello fizycznie są usuwane z tabeli hello, usługi Azure Search nie ma żadnych sposób tooinfer hello obecności rekordów, które już istnieją.  Jednak można użyć hello "soft-delete" techniki toologically usuwania wierszy bez ich usuwania z tabeli hello. Dodaj kolumny tooyour tabeli lub widoku i oznacz wierszy, jak usunąć przy użyciu tej kolumny.

Korzystając z techniki usuwania nietrwałego hello, można określić zasady usuwania nietrwałego hello w następujący sposób podczas tworzenia lub aktualizowania hello źródła danych:

    {
        …,
        "dataDeletionDetectionPolicy" : {
           "@odata.type" : "#Microsoft.Azure.Search.SoftDeleteColumnDeletionDetectionPolicy",
           "softDeleteColumnName" : "[a column name]",
           "softDeleteMarkerValue" : "[hello value that indicates that a row is deleted]"
        }
    }

Witaj **softDeleteMarkerValue** musi być ciągiem — Użyj hello reprezentacja ciągu wartości rzeczywistych. Na przykład, jeśli kolumna liczb całkowitych, w którym usuniętych wierszy są oznaczone ikoną z hello wartość 1, użyj `"1"`. Jeśli masz kolumny BIT, gdzie usuniętych wierszy są oznaczone ikoną z hello wartość logiczną PRAWDA, użyj `"True"`.

<a name="TypeMapping"></a>

## <a name="mapping-between-sql-and-azure-search-data-types"></a>Mapowanie między typy danych SQL i usługi Azure Search
| Typ danych SQL | Dozwolone typy pól indeksu docelowego | Uwagi |
| --- | --- | --- |
| bitowe |Typem Edm.Boolean, typem Edm.String | |
| int, smallint, tinyint |Typem Edm.String z typem Edm.Int32, Edm.Int64, | |
| bigint |Edm.Int64, typem Edm.String | |
| rzeczywiste, float |Edm.Double, typem Edm.String | |
| Smallmoney, pieniędzy dziesiętną liczbowe |Edm.String |Usługa Azure Search nie obsługuje konwersji typu decimal do Edm.Double, ponieważ spowoduje to utratę dokładności |
| char, nchar, varchar, nvarchar |Edm.String<br/>Collection(Edm.String) |Ciąg SQL można toopopulate używane pole Collection(Edm.String), jeśli ciąg hello reprezentuje tablicę JSON ciągów:`["red", "white", "blue"]` |
| smalldatetime, datetime, datetime2, date, datetimeoffset |Edm.DateTimeOffset, typem Edm.String | |
| uniqueidentifer |Edm.String | |
| Lokalizacja geograficzna |Edm.GeographyPoint |Obsługiwane są tylko geograficzne wystąpienia typu punktu z 4326 SRID, (który jest domyślnym hello) |
| ROWVERSION |Nie dotyczy |Kolumny wersji wiersza nie mogą być przechowywane w hello indeksu wyszukiwania, ale może służyć do śledzenia zmian |
| czas, timespan, binary, varbinary, obraz, xml, geometry, typy CLR |Nie dotyczy |Nieobsługiwane |

## <a name="configuration-settings"></a>Ustawienia konfiguracji
Indeksator SQL udostępnia kilka ustawień konfiguracji:

| Ustawienie | Typ danych | Przeznaczenie | Wartość domyślna |
| --- | --- | --- | --- |
| queryTimeout |Ciąg |Ustawia hello limitu czasu w celu wykonywania zapytań SQL |5 minut ("00: 05:00") |
| disableOrderByHighWaterMarkColumn |wartość logiczna |Powoduje, że zapytania SQL hello używanego przez hello znacznik limitu górnego zasad tooomit hello klauzuli ORDER BY. Zobacz [zasad znacznik limitu górnego](#HighWaterMarkPolicy) |wartość false |

Te ustawienia są używane w hello `parameters.configuration` obiektu w definicji indeksatora hello. Na przykład minut too10 tooset hello zapytania limitu czasu, Utwórz lub zaktualizuj indeksatora hello z hello następującej konfiguracji:

    {
      ... other indexer definition properties
     "parameters" : {
            "configuration" : { "queryTimeout" : "00:10:00" } }
    }

## <a name="faq"></a>Często zadawane pytania

**Pytanie: czy można użyć indeksatora Azure SQL z bazy danych SQL działające na maszynach wirtualnych IaaS na platformie Azure?**

Tak. Jednak należy tooallow Twojego tooconnect tooyour bazy danych usługi wyszukiwania. Aby uzyskać więcej informacji, zobacz [skonfigurować połączenie z tooSQL indeksator usługi Azure Search Server na maszynie Wirtualnej platformy Azure](search-howto-connecting-azure-sql-iaas-to-azure-search-using-indexers.md).

**Pytanie: czy można użyć indeksatora Azure SQL z bazy danych SQL, uruchamiane lokalnie?**

Nie bezpośrednio. Firma Microsoft nie zaleca się ani nie obsługuje bezpośredniego połączenia, jak to będzie wymagają tooopen możesz ruchu tooInternet baz danych. Klienci pomyślnie w tym scenariuszu przy użyciu technologii mostek, takich jak fabryki danych Azure. Aby uzyskać więcej informacji, zobacz [wypychania danych tooan indeksu usługi Azure Search przy użyciu fabryki danych Azure](https://docs.microsoft.com/azure/data-factory/data-factory-azure-search-connector).

**Pytanie: czy można użyć indeksatora Azure SQL z bazami danych innych niż SQL Server działającego w IaaS na platformie Azure?**

Nie. Ten scenariusz nie jest obsługiwane, ponieważ nie zostało to jeszcze przetestowaliśmy hello indeksator o żadnych baz danych innych niż SQL Server.  

**Pytanie: czy można utworzyć wiele indeksatorów uruchomionych na podstawie harmonogramu?**

Tak. Jednak tylko jeden indeksator mogą działać na jednym węźle jednocześnie. Wiele indeksatorów równoczesne działanie, należy wziąć pod uwagę skalowaniu Twojej toomore usługi wyszukiwania niż jedna jednostka wyszukiwania.

**Pytanie: czy pracą indeksator mają wpływ na Moje zapytania?**

Tak. Indeksator działa w jednym z węzłów hello w swojej usłudze wyszukiwania i zasobów w tym węźle są udostępniane między indeksowania oraz obsługująca ruch zapytania i inne żądania interfejsu API. Uruchom intensywnych obciążeń indeksowanie i zapytania i wystąpi wysoki współczynnik błędów 503 lub zwiększa czasy odpowiedzi, warto rozważyć [skalowaniu usługi wyszukiwania](search-capacity-planning.md).

**Pytanie: czy można używać repliki pomocniczej w [klastra pracy awaryjnej](https://docs.microsoft.com/azure/sql-database/sql-database-geo-replication-overview) jako źródło danych?**

To zależy. Pełna indeksowaniu tabelę lub widok, można użyć replikę pomocniczą. 

Przyrostowe indeksowania obsługuje usługi Azure Search, dwie zmiany zasad wykrywania: SQL zintegrowane zmienić śledzeniem i wysoki znacznik limitu górnego.

W trybie tylko do odczytu replikach baza danych SQL nie obsługuje śledzenie zmian zintegrowane. W związku z tym musisz użyć zasad znacznik limitu górnego. 

Nasze zalecenie, standardowe jest typem danych rowversion toouse hello, hello znacznik limitu górnego kolumny. Jednak przy użyciu rowversion zależy od usługi SQL Database `MIN_ACTIVE_ROWVERSION` funkcja, która nie jest obsługiwana w trybie tylko do odczytu replikach. W związku z tym musi wskazywać hello indeksatora tooa podstawowej repliki, jeśli używasz rowversion.

Jeśli rowversion toouse repliki tylko do odczytu, zostanie wyświetlony następujący błąd hello: 

    "Using a rowversion column for change tracking is not supported on secondary (read-only) availability replicas. Please update hello datasource and specify a connection toohello primary availability replica.Current database 'Updateability' property is 'READ_ONLY'".

**Pytanie: czy śledzenie zmian znacznik limitu górnego można użyć alternatywnych, kolumny z systemem innym niż rowversion?**

Nie jest zalecane. Tylko **rowversion** umożliwia synchronizacji danych. Jednak w zależności od logika aplikacji może być bezpieczne czy:

+ Można zapewnić, że po uruchomieniu indeksatora hello, nie ma żadnych oczekujących transakcji na powitania tabeli, która jest indeksowany (na przykład wszystkie aktualizacje tabeli powstawania jako plik wsadowy zgodnie z harmonogramem i ustawiono harmonogramu indeksator usługi Azure Search hello tooavoid nakładać się na powitania tabeli Harmonogram aktualizacji).  

+ Okresowo należy toopick pełne indeksowanie się żadnych brakujących wierszy. 
