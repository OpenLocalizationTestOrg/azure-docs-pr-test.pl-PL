---
title: "Indeksowanie źródła danych interfejsu API Azure rozwiązania Cosmos bazy danych SQL dla usługi Azure Search | Dokumentacja firmy Microsoft"
description: "W tym artykule przedstawiono sposób tworzenia indeksator usługi Azure Search ze źródłem danych bazy danych Azure rozwiązania Cosmos (interfejsu API SQL)."
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
ms.date: 01/08/2018
ms.author: eugenesh
robot: noindex
ms.openlocfilehash: e449f13adcd1a3651e1cac852b23f21d0227038a
ms.sourcegitcommit: 176c575aea7602682afd6214880aad0be6167c52
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 01/09/2018
---
# <a name="connecting-cosmos-db-with-azure-search-using-indexers"></a>Łączenie z usługi Azure Search przy użyciu indeksatorów DB rozwiązania Cosmos

[Azure DB rozwiązania Cosmos](../cosmos-db/introduction.md) jest bazą danych globalnie rozproszone i wiele modeli firmy Microsoft. Z jego [interfejsu API SQL](../cosmos-db/sql-api-introduction.md), bazy danych rozwiązania Cosmos Azure udostępnia znane i zaawansowanych możliwości zapytania SQL z stale małe opóźnienia w porównaniu z danych JSON bez schematu. Usługa wyszukiwanie Azure bezproblemowo integruje się z interfejsu API SQL. Dokumentów JSON można pobierać bezpośrednio do indeksu usługi Azure Search przy użyciu [indeksator usługi Azure Search](search-indexer-overview.md), zaprojektowany specjalnie z myślą o interfejsu API Azure rozwiązania Cosmos bazy danych SQL. 

W tym artykule przedstawiono sposób:

> [!div class="checklist"]
> * Konfigurowanie usługi Azure Search do używania bazy danych interfejsu API Azure rozwiązania Cosmos bazy danych SQL jako źródła danych. Opcjonalnie możesz podać kwerendę do wybierania podzbioru.
> * Tworzenie indeksu wyszukiwania z typami danych zgodnego JSON.
> * Skonfiguruj indeksator na żądanie i indeksowania cyklicznego.
> * Odśwież przyrostowo indeksu na podstawie zmian w danych źródłowych.

> [!NOTE]
> Interfejsu API Azure rozwiązania Cosmos bazy danych SQL to nowa generacja usługi documentdb. Mimo że nazwa produktu została zmieniona, `documentdb` składni w indeksatory usługi Azure Search nadal istnieje dla zapewnienia zgodności z interfejsów API usługi Azure Search i na stronach portalu. Podczas konfigurowania indeksatorów, należy określić `documentdb` składni zgodnie z instrukcją w tym artykule.

<a name="supportedAPIs"></a>

## <a name="supported-api-types"></a>Obsługiwane typy interfejsu API

Mimo że bazy danych rozwiązania Cosmos Azure obsługuje wiele interfejsów API i modeli danych, obsługa indeksatora rozszerza do interfejsu API SQL. 

Nadchodzi obsługę dodatkowych interfejsów API. W celu ułatwienia określenia priorytetu, które z nich do obsługi najpierw, wykonaj najpierw rzutowanie w witrynie sieci web głos użytkownika:

* [Obsługa źródła danych interfejsu API tabeli](https://feedback.azure.com/forums/263029-azure-search/suggestions/32759746-azure-search-should-be-able-to-index-cosmos-db-tab)
* [Obsługa źródła danych wykresu interfejsu API](https://feedback.azure.com/forums/263029-azure-search/suggestions/13285011-add-graph-databases-to-your-data-sources-eg-neo4)
* [Obsługa źródła danych bazy danych MongoDB interfejsu API](https://feedback.azure.com/forums/263029-azure-search/suggestions/18861421-documentdb-indexer-should-be-able-to-index-mongodb)
* [Obsługa źródła danych Apache Cassandra API](https://feedback.azure.com/forums/263029-azure-search/suggestions/32857525-indexer-crawler-for-apache-cassandra-api-in-azu)

## <a name="prerequisites"></a>Wymagania wstępne

Aby skonfigurować indeksator bazy danych rozwiązania Cosmos platformy Azure, musi mieć [usługi Azure Search](search-create-service-portal.md)i Utwórz indeks, źródła danych, a na końcu indeksatora. Można utworzyć te obiekty przy użyciu [portal](search-import-data-portal.md), [zestawu .NET SDK](/dotnet/api/microsoft.azure.search), lub [interfejsu API REST](/rest/api/searchservice/) dla wszystkich języków innych niż .NET. 

Jeśli wybierzesz portalu, [Kreatora importu danych](search-import-data-portal.md) prowadzi użytkownika przez utworzenie wszystkich tych zasobów, w tym indeksu.

> [!TIP]
> W celu uproszczenia indeksowania dla danego źródła danych można uruchomić kreator **Importuj dane** na pulpicie nawigacyjnym usługi Azure Cosmos DB. Aby rozpocząć, w obszarze nawigacyjnym po lewej stronie przejdź do pozycji **Kolekcje** > **Dodaj usługę Azure Search**.

<a name="Concepts"></a>

## <a name="azure-search-indexer-concepts"></a>Azure pojęcia indeksatora wyszukiwania
Azure Search obsługuje tworzenie i zarządzanie nimi danych źródła (łącznie z interfejsu API Azure rozwiązania Cosmos bazy danych SQL) i indeksatorów, które działają na tych źródłach danych.

A **źródła danych** Określa dane do indeksu, poświadczenia i zasad do identyfikowania zmian w danych (takich jak dokumenty zmodyfikowany lub usunięty w kolekcji). Źródło danych jest zdefiniowany jako niezależnym zasobem, dzięki czemu mogą być używane przez wiele indeksatorów.

**Indeksatora** w tym artykule opisano, jak przepływ danych ze źródła danych do indeksu wyszukiwania docelowego. Indeksator może służyć do:

* Wykonywać jednorazowe kopię danych do wypełniania indeksu.
* Synchronizowanie indeksu ze zmianami w źródle danych, zgodnie z harmonogramem. Harmonogram jest częścią definicji indeksatora.
* Wywołaj aktualizacje na żądanie do indeksu w razie potrzeby.

<a name="CreateDataSource"></a>

## <a name="step-1-create-a-data-source"></a>Krok 1. Tworzenie źródła danych
Aby utworzyć źródło danych, wykonaj ogłoszenie (POST):

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

Treść żądania zawiera definicję źródła danych, które powinny zawierać następujące pola:

* **Nazwa**: Nazwa do reprezentowania bazy danych.
* **Typ**: musi być `documentdb`.
* **poświadczenia**:
  
  * **connectionString**: wymagane. Określ informacje o połączeniu z bazą danych Azure DB rozwiązania Cosmos w następującym formacie:`AccountEndpoint=<Cosmos DB endpoint url>;AccountKey=<Cosmos DB auth key>;Database=<Cosmos DB database id>`
* **kontener**:
  
  * **Nazwa**: wymagane. Określ identyfikator kolekcji bazy danych do indeksowania.
  * **Zapytanie**: opcjonalne. Można określić zapytania do spłaszczenia dowolnych dokumentów JSON na płaskiej schemat, który można indeksu usługi Azure Search.
* **dataChangeDetectionPolicy**: zalecane. Zobacz [indeksowania dokumentów zmienić](#DataChangeDetectionPolicy) sekcji.
* **dataDeletionDetectionPolicy**: opcjonalne. Zobacz [indeksowania dokumentów usunięte](#DataDeletionDetectionPolicy) sekcji.

### <a name="using-queries-to-shape-indexed-data"></a>Za pomocą zapytań do kształtu indeksowane danych
Określ zapytanie SQL do spłaszczenia właściwości zagnieżdżonych lub tablic, właściwości projektu JSON i filtrowanie danych do indeksowania. 

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
## <a name="step-2-create-an-index"></a>Krok 2. Tworzenie indeksu
Tworzenie indeksu usługi Azure Search docelowego, jeśli nie masz już. Można utworzyć indeksu przy użyciu [interfejsu użytkownika portalu Azure](search-create-index-portal.md), [tworzenia indeksu interfejsu API REST](/rest/api/searchservice/create-index) lub [indeksu klasy](/dotnet/api/microsoft.azure.search.models.index).

Poniższy przykład tworzy indeks z polem Identyfikator i opis:

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

Upewnij się, że schemat indeksu docelowego jest zgodna z schematu dokumentów JSON źródła lub dane wyjściowe z projekcji zapytań niestandardowych.

> [!NOTE]
> Dla kolekcji partycjonowanych domyślny klucz dokumentu jest Azure rozwiązania Cosmos DB `_rid` właściwość, która pobiera zmieniona na `rid` w usłudze Azure Search. Ponadto rozwiązania Cosmos bazy danych Azure w `_rid` wartości zawiera znaki, które nie są prawidłowe w kluczach usługi Azure Search. Z tego powodu `_rid` wartości są kodowany w standardzie Base64.
> 
> 

### <a name="mapping-between-json-data-types-and-azure-search-data-types"></a>Mapowanie między typami danych JSON i typy danych w usłudze Azure Search
| Typ danych JSON | Typy elementów docelowych zgodny indeks pola |
| --- | --- |
| wartość logiczna |Typem Edm.Boolean, typem Edm.String |
| Numery, które wyglądają jak liczby całkowite |Typem Edm.String z typem Edm.Int32, Edm.Int64, |
| Numery tego wygląd zmiennoprzecinkową punkty |Edm.Double, typem Edm.String |
| Ciąg |Edm.String |
| Tablice typów pierwotnych, na przykład ["a", "b", "c"] |Collection(Edm.String) |
| Ciągi, które wyglądają dat |Edm.DateTimeOffset, typem Edm.String |
| Obiekty GeoJSON, na przykład {"type": "Point", "coordinates": [długie, lat]} |Edm.GeographyPoint |
| Inne obiekty JSON |ND |

<a name="CreateIndexer"></a>

## <a name="step-3-create-an-indexer"></a>Krok 3: Utwórz indeksator

Po utworzeniu indeks i źródło danych, możesz przystąpić do tworzenia indeksatora:

    POST https://[service name].search.windows.net/indexers?api-version=2016-09-01
    Content-Type: application/json
    api-key: [admin key]

    {
      "name" : "mydocdbindexer",
      "dataSourceName" : "mydocdbdatasource",
      "targetIndexName" : "mysearchindex",
      "schedule" : { "interval" : "PT2H" }
    }

Ten indeksator jest uruchamiane co dwie godziny (interwał harmonogramu jest ustawiony na "PT2H"). Aby uruchomić indeksatora co 30 minut, należy ustawić interwał o "PT30M". Najkrótszy obsługiwany interwał wynosi 5 minut. Harmonogram jest opcjonalny — w przypadku pominięcia, indeksatora działa tylko wtedy, gdy po jego utworzeniu. Jednak w dowolnym momencie można uruchomić indeksatora na żądanie.   

Aby uzyskać więcej szczegółów na tworzenie interfejsu API indeksatora, zapoznaj się [Utwórz indeksator](https://docs.microsoft.com/rest/api/searchservice/create-indexer).

<a id="RunIndexer"></a>
### <a name="running-indexer-on-demand"></a>Uruchomiona indeksatora na żądanie
Poza uruchamianiem okresowo, zgodnie z harmonogramem, indeksatora może być wywoływana na żądanie:

    POST https://[service name].search.windows.net/indexers/[indexer name]/run?api-version=2016-09-01
    api-key: [Search service admin key]

> [!NOTE]
> Podczas uruchamiania interfejsu API zwraca pomyślnie, zaplanowano wywołanie indeksatora, ale aktualnie przetwarzanego sytuacji asynchronicznie. 

Możesz monitorować stan indeksator w portalu lub przy użyciu uzyskać indeksatora stan interfejsu API, który opisano dalej. 

<a name="GetIndexerStatus"></a>
### <a name="getting-indexer-status"></a>Pobieranie stanu indeksatora
Można pobrać historii stanu i wykonywanie indeksatora:

    GET https://[service name].search.windows.net/indexers/[indexer name]/status?api-version=2016-09-01
    api-key: [Search service admin key]

Odpowiedź zawiera ogólny stan indeksatora, wywołanie indeksatora ostatniego (lub w toku) i historię ostatnich wywołań indeksatora.

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

Historii wykonywania zawiera maksymalnie 50 najnowszych wykonaniami zakończonych, które są sortowane w kolejności odwrotnej (aby najnowsze wykonywania zostanie osiągnięty jako pierwszy w odpowiedzi).

<a name="DataChangeDetectionPolicy"></a>
## <a name="indexing-changed-documents"></a>Indeksowanie dokumentów zmienione
Zasady wykrywania zmian danych ma na celu wydajnie zidentyfikować elementy zmienione dane. Obecnie jest obsługiwane tylko zasady `High Water Mark` przy użyciu zasad `_ts` właściwości (sygnatury czasowej) udostępniane przez DB rozwiązania Cosmos Azure, którą określono w następujący sposób:

    {
        "@odata.type" : "#Microsoft.Azure.Search.HighWaterMarkChangeDetectionPolicy",
        "highWaterMarkColumnName" : "_ts"
    }

Aby zapewnić wydajność indeksatora dobrej zdecydowanie zaleca przy użyciu tych zasad. 

Jeśli używasz niestandardowe zapytanie, upewnij się, że `_ts` właściwości jest chroniony przez zapytanie.

<a name="IncrementalProgress"></a>
### <a name="incremental-progress-and-custom-queries"></a>Postęp przyrostowych i zapytań niestandardowych
Przyrostowe postępu podczas indeksowania gwarantuje, że jeśli wykonywanie indeksatora jest przerwane z powodu błędów przejściowych lub limit czasu wykonywania, indeksatora mogą odbierać którym przerwał następnym uruchomieniu, zamiast ponownego indeksowania całą kolekcję od początku. Jest to szczególnie ważne w przypadku, gdy przeprowadzane jest indeksowanie dużych kolekcjach. 

Aby włączyć przyrostowego postępu, za pomocą niestandardowe zapytanie, upewnij się, że kwerenda porządkuje wyniki według `_ts` kolumny. Dzięki temu okresowego sprawdzania wskazującej, która używa usługi Azure Search, aby zapewnić przyrostowego postępu obecności błędów.   

W niektórych przypadkach, nawet jeśli zapytanie zawiera `ORDER BY [collection alias]._ts` klauzuli, wyszukiwanie Azure może nie wnioskować że zapytania są uporządkowane według `_ts`. Można ustalić usługi Azure Search że wyniki są uporządkowane przy użyciu `assumeOrderByHighWaterMarkColumn` właściwości konfiguracji. Aby określić tę wskazówkę, należy utworzyć lub zaktualizować indeksator w następujący sposób: 

    {
     ... other indexer definition properties
     "parameters" : {
            "configuration" : { "assumeOrderByHighWaterMarkColumn" : true } }
    } 

<a name="DataDeletionDetectionPolicy"></a>
## <a name="indexing-deleted-documents"></a>Indeksowanie usunięte dokumentów
Jeśli wiersze są usuwane z kolekcji, zwykle chcesz usunąć te wiersze z z indeksu wyszukiwania. Zasady wykrywania usuwania danych ma na celu wydajnie zidentyfikować elementy usunięte dane. Obecnie jest obsługiwane tylko zasady `Soft Delete` zasad (usuwanie jest oznaczony przy użyciu flagi jakiegoś), który został określony w następujący sposób:

    {
        "@odata.type" : "#Microsoft.Azure.Search.SoftDeleteColumnDeletionDetectionPolicy",
        "softDeleteColumnName" : "the property that specifies whether a document was deleted",
        "softDeleteMarkerValue" : "the value that identifies a document as deleted"
    }

Jeśli używasz niestandardowe zapytanie, upewnij się, że właściwość odwołuje się `softDeleteColumnName` jest chroniony przez zapytanie.

Poniższy przykład tworzy źródła danych za pomocą zasad usuwania nietrwałego:

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
Gratulacje! Znasz sposobu integracji z usługi Azure Search przy użyciu indeksatora przeszukiwania i przekazywania dokumentów z modelem danych SQL Azure DB rozwiązania Cosmos.

* Aby dowiedzieć się więcej na temat bazy danych rozwiązania Cosmos Azure, zobacz [stronę usługi bazy danych Azure rozwiązania Cosmos](https://azure.microsoft.com/services/cosmos-db/).
* Aby dowiedzieć się więcej na temat usługi Azure Search, zobacz [strony usługi wyszukiwania](https://azure.microsoft.com/services/search/).
