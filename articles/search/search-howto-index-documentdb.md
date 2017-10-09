---
title: "aaaIndexing DB rozwiązania Cosmos źródła danych dla usługi Azure Search | Dokumentacja firmy Microsoft"
description: "W tym artykule opisano sposób toocreate indeksator usługi Azure Search DB rozwiązania Cosmos w postaci źródła danych."
services: search
documentationcenter: 
author: chaosrealm
manager: pablocas
editor: 
ms.assetid: 
ms.service: search
ms.devlang: rest-api
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: search
ms.date: 08/10/2017
ms.author: eugenesh
ms.openlocfilehash: 195c9bc026ee1591679dc425ef083a32a3c86be6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="connecting-cosmos-db-with-azure-search-using-indexers"></a>Łączenie z usługi Azure Search przy użyciu indeksatorów DB rozwiązania Cosmos

Jeśli chcesz tooimplement wyszukiwania doskonałe środowisko za pośrednictwem danych DB rozwiązania Cosmos, można użyć danych toopull indeksator usługi Azure Search do indeksu usługi Azure Search. W tym artykule zostanie przedstawiony zostanie sposób toointegrate Azure DB rozwiązania Cosmos z usługi Azure Search bez konieczności toowrite dowolnej infrastruktury indeksowania toomaintain kodu.

tooset się indeksatora rozwiązania Cosmos bazy danych, musisz mieć [usługi Azure Search](search-create-service-portal.md)i Utwórz indeks, źródła danych, a na końcu hello indeksatora. Można utworzyć te obiekty przy użyciu hello [portal](search-import-data-portal.md), [zestawu .NET SDK](/dotnet/api/microsoft.azure.search), lub [interfejsu API REST](/rest/api/searchservice/) dla wszystkich języków innych niż .NET. 

Jeśli wybierzesz portalu hello hello [Kreatora importu danych](search-import-data-portal.md) prowadzi użytkownika przez utworzenie hello wszystkich tych zasobów.

> [!NOTE]
> Rozwiązania cosmos bazy danych jest hello generacji usługi documentdb. Mimo że nazwa produktu hello została zmieniona, składnia jest hello sam jak poprzednio. Kontynuuj toospecify `documentdb` zgodnie ze wskazówkami zawartymi w tym artykule indeksatora. 

> [!TIP]
> Możesz uruchomić hello **importowania danych** kreatora z toosimplify pulpitu nawigacyjnego rozwiązania Cosmos DB hello indeksowania dla tego źródła danych. W lewym okienku nawigacji przejdź zbyt**kolekcje** > **Dodaj usługi Azure Search** tooget uruchomiona.

<a name="Concepts"></a>
## <a name="azure-search-indexer-concepts"></a>Azure pojęcia indeksatora wyszukiwania
Azure Search obsługuje hello tworzenie i zarządzanie źródeł danych (w tym rozwiązania Cosmos bazy danych) i indeksatorów, które działają na tych źródeł danych.

A **źródła danych** określa tooindex danych hello, poświadczeń i zasad do identyfikacji zmiany hello danych (takich jak dokumenty zmodyfikowany lub usunięty w kolekcji). źródło danych Hello jest zdefiniowany jako niezależnym zasobem, dzięki czemu mogą być używane przez wiele indeksatorów.

**Indeksatora** w tym artykule opisano, jak dane hello przepływają ze źródła danych do indeksu wyszukiwania docelowego. Indeksator może służyć do:

* Należy wykonać kopię jednorazowe hello danych toopopulate indeksu.
* Synchronizowanie indeksu ze zmianami w źródle danych hello zgodnie z harmonogramem. Harmonogram Hello jest częścią definicji indeksatora hello.
* Wywołaj indeksu tooan aktualizacje na żądanie, zgodnie z potrzebami.

<a name="CreateDataSource"></a>
## <a name="step-1-create-a-data-source"></a>Krok 1: Tworzenie źródła danych
toocreate źródła danych, wykonaj ogłoszenie (POST):

    POST https://[service name].search.windows.net/datasources?api-version=2016-09-01
    Content-Type: application/json
    api-key: [Search service admin key]

    {
        "name": "mydocdbdatasource",
        "type": "documentdb",
        "credentials": {
            "connectionString": "AccountEndpoint=https://myDocDbEndpoint.documents.azure.com;AccountKey=myDocDbAuthKey;Database=myDocDbDatabaseId"
        },
        "container": { "name": "myDocDbCollectionId", "query": null },
        "dataChangeDetectionPolicy": {
            "@odata.type": "#Microsoft.Azure.Search.HighWaterMarkChangeDetectionPolicy",
            "highWaterMarkColumnName": "_ts"
        }
    }

Witaj treści żądania hello zawiera definicję źródła danych hello, które powinny zawierać następujące pola hello:

* **Nazwa**: Wybierz wszystkie toorepresent Nazwa bazy danych DB rozwiązania Cosmos.
* **Typ**: musi być `documentdb`.
* **poświadczenia**:
  
  * **connectionString**: wymagane. Określ bazy danych Azure DB rozwiązania Cosmos tooyour hello połączenia informacji w hello następującego formatu:`AccountEndpoint=<Cosmos DB endpoint url>;AccountKey=<Cosmos DB auth key>;Database=<Cosmos DB database id>`
* **kontener**:
  
  * **Nazwa**: wymagane. Określ identyfikator hello toobe kolekcji DB rozwiązania Cosmos hello indeksowane.
  * **Zapytanie**: opcjonalne. Można określić zapytania tooflatten dowolnych dokumentów JSON na płaskiej schemat, który można indeksu usługi Azure Search.
* **dataChangeDetectionPolicy**: zalecane. Zobacz [indeksowania dokumentów zmienić](#DataChangeDetectionPolicy) sekcji.
* **dataDeletionDetectionPolicy**: opcjonalne. Zobacz [indeksowania dokumentów usunięte](#DataDeletionDetectionPolicy) sekcji.

### <a name="using-queries-tooshape-indexed-data"></a>Przy użyciu kwerend tooshape indeksowane danych
Można określić właściwości zagnieżdżone tooflatten zapytania DB rozwiązania Cosmos lub tablic, JSON właściwości projektu i filtrować toobe danych hello indeksowane. 

Przykładowy dokument:

    {
        "userId": 10001,
        "contact": {
            "firstName": "andy",
            "lastName": "hoh"
        },
        "company": "microsoft",
        "tags": ["azure", "documentdb", "search"]
    }

Filtr zapytania:

    SELECT * FROM c WHERE c.company = "microsoft" and c._ts >= @HighWaterMark ORDER BY c._ts

Spłaszczanie zapytania:

    SELECT c.id, c.userId, c.contact.firstName, c.contact.lastName, c.company, c._ts FROM c WHERE c._ts >= @HighWaterMark ORDER BY c._ts
    
    
Projekcja zapytanie:

    SELECT VALUE { "id":c.id, "Name":c.contact.firstName, "Company":c.company, "_ts":c._ts } FROM c WHERE c._ts >= @HighWaterMark ORDER BY c._ts


Tablica spłaszczania zapytanie:

    SELECT c.id, c.userId, tag, c._ts FROM c JOIN tag IN c.tags WHERE c._ts >= @HighWaterMark ORDER BY c._ts

<a name="CreateIndex"></a>
## <a name="step-2-create-an-index"></a>Krok 2: Tworzenie indeksu
Tworzenie indeksu usługi Azure Search docelowego, jeśli nie masz już. Można utworzyć indeksu przy użyciu hello [interfejsu użytkownika portalu Azure](search-create-index-portal.md), hello [tworzenia indeksu interfejsu API REST](/rest/api/searchservice/create-index) lub [indeksu klasy](/dotnet/api/microsoft.azure.search.models.index).

Witaj poniższy przykład tworzy indeks z polem Identyfikator i opis:

    POST https://[service name].search.windows.net/indexes?api-version=2016-09-01
    Content-Type: application/json
    api-key: [Search service admin key]

    {
       "name": "mysearchindex",
       "fields": [{
         "name": "id",
         "type": "Edm.String",
         "key": true,
         "searchable": false
       }, {
         "name": "description",
         "type": "Edm.String",
         "filterable": false,
         "sortable": false,
         "facetable": false,
         "suggestions": true
       }]
     }

Upewnij się, że hello schematu indeksu docelowego jest zgodny z hello schematu dokumentów JSON źródłowych hello lub hello dane wyjściowe z projekcji zapytań niestandardowych.

> [!NOTE]
> Dla kolekcji partycjonowanych klucz dokumentu domyślnego hello jest DB rozwiązania Cosmos `_rid` właściwość, która pobiera zmieniona zbyt`rid` w usłudze Azure Search. Ponadto rozwiązania Cosmos bazy danych w `_rid` wartości zawiera znaki, które nie są prawidłowe w kluczach usługi Azure Search. Z tego powodu hello `_rid` wartości są kodowany w standardzie Base64.
> 
> 

### <a name="mapping-between-json-data-types-and-azure-search-data-types"></a>Mapowanie między typami danych JSON i typy danych w usłudze Azure Search
| TYP DANYCH JSON | TYPY ELEMENTÓW DOCELOWYCH ZGODNY INDEKS POLA |
| --- | --- |
| wartość logiczna |Typem Edm.Boolean, typem Edm.String |
| Numery, które wyglądają jak liczby całkowite |Typem Edm.String z typem Edm.Int32, Edm.Int64, |
| Numery tego wygląd zmiennoprzecinkową punkty |Edm.Double, typem Edm.String |
| Ciąg |Edm.String |
| Tablice typów pierwotnych, na przykład ["a", "b", "c"] |Collection(Edm.String) |
| Ciągi, które wyglądają dat |Edm.DateTimeOffset, typem Edm.String |
| Obiekty GeoJSON, na przykład {"type": "Point", "coordinates": [długie, lat]} |Edm.GeographyPoint |
| Inne obiekty JSON |Nie dotyczy |

<a name="CreateIndexer"></a>
## <a name="step-3-create-an-indexer"></a>Krok 3: Utwórz indeksator

Po utworzeniu hello indeks i źródło danych jest gotowy toocreate hello indeksatora:

    POST https://[service name].search.windows.net/indexers?api-version=2016-09-01
    Content-Type: application/json
    api-key: [admin key]

    {
      "name" : "mydocdbindexer",
      "dataSourceName" : "mydocdbdatasource",
      "targetIndexName" : "mysearchindex",
      "schedule" : { "interval" : "PT2H" }
    }

Ten indeksator działa co dwie godziny (interwał harmonogramu jest ustawiona zbyt "PT2H"). toorun indeksatora co 30 minut, ustawić interwał powitania także "PT30M". Witaj najkrótszy obsługiwany interwał wynosi 5 minut. Hello harmonogram jest opcjonalny — w przypadku jego pominięcia, indeksatora działa tylko wtedy, gdy po utworzeniu. Jednak w dowolnym momencie można uruchomić indeksatora na żądanie.   

Aby uzyskać więcej informacji na temat hello Tworzenie interfejsu API indeksatora, zapoznaj się z [Utwórz indeksator](https://docs.microsoft.com/rest/api/searchservice/create-indexer).

<a id="RunIndexer"></a>
### <a name="running-indexer-on-demand"></a>Uruchomiona indeksatora na żądanie
W przypadku dodawania toorunning okresowo zgodnie z harmonogramem indeksatora może być wywoływana na żądanie:

    POST https://[service name].search.windows.net/indexers/[indexer name]/run?api-version=2016-09-01
    api-key: [Search service admin key]

> [!NOTE]
> Podczas uruchamiania interfejsu API zwraca pomyślnie, wywołanie indeksatora hello zostało zaplanowane, ale aktualnie przetwarzanego hello sytuacji asynchronicznie. 

Można monitorować stan indeksatora hello w portalu hello lub przy użyciu hello uzyskać indeksatora stan interfejsu API, który opisano dalej. 

<a name="GetIndexerStatus"></a>
### <a name="getting-indexer-status"></a>Pobieranie stanu indeksatora
Można pobrać historii stanu i wykonywanie indeksatora hello:

    GET https://[service name].search.windows.net/indexers/[indexer name]/status?api-version=2016-09-01
    api-key: [Search service admin key]

odpowiedź Hello zawiera ogólny stan indeksatora, hello wywołanie indeksatora ostatniego (lub w toku) i hello historię ostatnich wywołań indeksatora.

    {
        "status":"running",
        "lastResult": {
            "status":"success",
            "errorMessage":null,
            "startTime":"2014-11-26T03:37:18.853Z",
            "endTime":"2014-11-26T03:37:19.012Z",
            "errors":[],
            "itemsProcessed":11,
            "itemsFailed":0,
            "initialTrackingState":null,
            "finalTrackingState":null
         },
        "executionHistory":[ {
            "status":"success",
             "errorMessage":null,
            "startTime":"2014-11-26T03:37:18.853Z",
            "endTime":"2014-11-26T03:37:19.012Z",
            "errors":[],
            "itemsProcessed":11,
            "itemsFailed":0,
            "initialTrackingState":null,
            "finalTrackingState":null
        }]
    }

Zawiera historię wykonywania zapasową toohello 50 najnowszych ukończone wykonaniami, które są sortowane w kolejności odwrotnej (aby wykonywania najnowszego hello zostanie osiągnięty jako pierwszy w odpowiedzi hello).

<a name="DataChangeDetectionPolicy"></a>
## <a name="indexing-changed-documents"></a>Indeksowanie dokumentów zmienione
cel Hello danych zmienić zasady wykrywania jest tooefficiently zidentyfikować elementy zmienione dane. Witaj obsługiwane tylko zasady jest obecnie hello `High Water Mark` zasady za pomocą hello `_ts` właściwości (sygnatury czasowej) udostępniane przez rozwiązania Cosmos bazy danych, które jest określone w następujący sposób:

    {
        "@odata.type" : "#Microsoft.Azure.Search.HighWaterMarkChangeDetectionPolicy",
        "highWaterMarkColumnName" : "_ts"
    }

Przy użyciu tych zasad jest zalecany tooensure indeksatora dobrą wydajność. 

Jeśli używasz niestandardowe zapytanie, upewnij się, że hello `_ts` właściwości jest chroniony przez hello zapytania.

<a name="IncrementalProgress"></a>
### <a name="incremental-progress-and-custom-queries"></a>Postęp przyrostowych i zapytań niestandardowych
Przyrostowe postępu podczas indeksowania gwarantuje, że jeśli wykonywanie indeksatora jest przerwane z powodu błędów przejściowych lub limit czasu wykonywania, indeksatora hello mogą odbierać którym przerwał następnym go uruchamia zamiast indeksu toore hello całą kolekcję od początku. Jest to szczególnie ważne w przypadku, gdy przeprowadzane jest indeksowanie dużych kolekcjach. 

postęp przyrostowe tooenable niestandardowe zapytanie, używając upewnij się, że kwerenda porządkuje wyniki hello przez hello `_ts` kolumny. Dzięki temu okresowe wyboru wskazującą czy usługi Azure Search używa tooprovide przyrostowego postępu w hello występowania błędów.   

W niektórych przypadkach, nawet jeśli zapytanie zawiera `ORDER BY [collection alias]._ts` klauzuli, wyszukiwanie Azure mogą są rozpoznawane przez tę kwerendę hello jest uporządkowanych według hello `_ts`. Można ustalić usługi Azure Search że wyniki są uporządkowane przy użyciu hello `assumeOrderByHighWaterMarkColumn` właściwości konfiguracji. toospecify wskazówka, Utwórz lub zaktualizuj indeksator w następujący sposób: 

    {
     ... other indexer definition properties
     "parameters" : {
            "configuration" : { "assumeOrderByHighWaterMarkColumn" : true } }
    } 

<a name="DataDeletionDetectionPolicy"></a>
## <a name="indexing-deleted-documents"></a>Indeksowanie usunięte dokumentów
Usunięcie wierszy z kolekcji hello zwykle mają toodelete te wiersze z hello również indeksu wyszukiwania. Witaj zasady wykrywania usuwania danych służy tooefficiently zidentyfikować elementy usunięte dane. Witaj obsługiwane tylko zasady jest obecnie hello `Soft Delete` zasad (usuwanie jest oznaczony przy użyciu flagi jakiegoś), który został określony w następujący sposób:

    {
        "@odata.type" : "#Microsoft.Azure.Search.SoftDeleteColumnDeletionDetectionPolicy",
        "softDeleteColumnName" : "hello property that specifies whether a document was deleted",
        "softDeleteMarkerValue" : "hello value that identifies a document as deleted"
    }

Jeśli używasz niestandardowe zapytanie, upewnij się, tej właściwości hello odwołuje się `softDeleteColumnName` jest chroniony przez hello zapytania.

Hello poniższy przykład powoduje utworzenie źródła danych za pomocą zasad usuwania nietrwałego:

    POST https://[Search service name].search.windows.net/datasources?api-version=2016-09-01
    Content-Type: application/json
    api-key: [Search service admin key]

    {
        "name": "mydocdbdatasource",
        "type": "documentdb",
        "credentials": {
            "connectionString": "AccountEndpoint=https://myDocDbEndpoint.documents.azure.com;AccountKey=myDocDbAuthKey;Database=myDocDbDatabaseId"
        },
        "container": { "name": "myDocDbCollectionId" },
        "dataChangeDetectionPolicy": {
            "@odata.type": "#Microsoft.Azure.Search.HighWaterMarkChangeDetectionPolicy",
            "highWaterMarkColumnName": "_ts"
        },
        "dataDeletionDetectionPolicy": {
            "@odata.type": "#Microsoft.Azure.Search.SoftDeleteColumnDeletionDetectionPolicy",
            "softDeleteColumnName": "isDeleted",
            "softDeleteMarkerValue": "true"
        }
    }

## <a name="NextSteps"></a>Następne kroki
Gratulacje! Wiesz już, jak toointegrate bazy danych rozwiązania Cosmos Azure przy użyciu usługi Azure Search hello indeksatora dla DB rozwiązania Cosmos.

* toolearn jak więcej informacji na temat bazy danych rozwiązania Cosmos platformy Azure, zobacz hello [stronę usługi DB rozwiązania Cosmos](https://azure.microsoft.com/services/documentdb/).
* toolearn jak więcej informacji na temat usługi Azure Search, zobacz hello [strony usługi wyszukiwania](https://azure.microsoft.com/services/search/).
