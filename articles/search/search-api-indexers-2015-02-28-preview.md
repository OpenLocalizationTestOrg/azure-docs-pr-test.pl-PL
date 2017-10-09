---
title: "Operacje indeksatora (interfejsu API REST usługi Azure Search: 2015-02-28-Preview) | Dokumentacja firmy Microsoft"
description: "Operacje indeksatora (interfejsu API REST usługi Azure Search: 2015-02-28-Preview)"
services: search
documentationcenter: 
author: chaosrealm
manager: pablocas
editor: 
ms.assetid: 42b5f85c-8304-4bc7-8e1e-a9c76b8ca25a
ms.service: search
ms.devlang: rest-api
ms.workload: search
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 05/01/2017
ms.author: eugenesh
ms.openlocfilehash: 4dd9591072b44eeabae6eac1182b4eea10fd4a22
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="indexer-operations-azure-search-service-rest-api-2015-02-28-preview"></a>Operacje indeksatora (interfejsu API REST usługi Azure Search: 2015-02-28-Preview)
> [!NOTE]
> W tym artykule opisano indeksatorów w hello [interfejsu API REST 2015-02-28-Preview](search-api-2015-02-28-preview.md). Ta wersja interfejsu API dodaje wersji preview programów indeksator magazynu obiektów Blob Azure o wyodrębniania dokumentu indeksatora magazynu tabel Azure, a także inne ulepszenia. Witaj interfejs API obsługuje również ogólnie dostępna indeksatorów (GA), w tym indeksatory dla bazy danych SQL Azure, programu SQL Server na maszynach wirtualnych platformy Azure i bazy danych Azure rozwiązania Cosmos.
> 
> 

## <a name="overview"></a>Omówienie
Wyszukiwanie Azure można łączyć bezpośrednio z niektórych wspólnych źródeł danych, usuwanie hello potrzeby toowrite kodu tooindex danych. tooset się to w górę, można wywołać hello toocreate interfejsu API usługi Azure Search i zarządzać **indeksatory** i **źródeł danych**. 

**Indeksatora** jest z zasobem, który łączy źródeł danych z docelowym indeksy wyszukiwania. Indeksator jest używany w hello następujące sposoby: 

* Należy wykonać kopię jednorazowe hello danych toopopulate indeksu.
* Synchronizowanie indeksu ze zmianami w źródle danych hello zgodnie z harmonogramem. Harmonogram Hello jest częścią definicji indeksatora hello.
* Wywołania na żądanie tooupdate indeksu zgodnie z potrzebami. 

**Indeksatora** jest przydatne, gdy ma indeks tooan regularne aktualizacje. Można albo ustaw harmonogram wbudowanego jako część definicji indeksatora lub uruchomić ją na żądanie przy użyciu [uruchomić indeksatora](#RunIndexer). 

A **źródła danych** Określa, jakie dane należy toobe indeksowane, poświadczenia tooaccess hello danych i zasady tooenable usługi Azure Search tooefficiently zidentyfikować zmiany danych hello (takie jak zmodyfikowane lub usunięte wiersze w tabeli bazy danych). Jest on zdefiniowany jako niezależnym zasobem, dzięki czemu mogą być używane przez wiele indeksatorów.

Witaj następujące źródła danych są obecnie obsługiwane:

* **Baza danych Azure SQL** i **programu SQL Server na maszynach wirtualnych Azure**. Dla docelowej przewodnika [w tym artykule](search-howto-connecting-azure-sql-database-to-azure-search-using-indexers.md). 
* **Rozwiązania Cosmos Azure DB**. Dla docelowej przewodnika [w tym artykule](search-howto-index-documentdb.md). 
* **Magazyn obiektów Blob Azure**, w tym następujące hello dokumentu formaty: PDF, Microsoft Office (DOCX/DOC, XSLX/XLS, PPTX/PPT, MSG), HTML, XML, ZIP i zwykły tekst plików (w tym JSON). Dla docelowej przewodnika [w tym artykule](search-howto-indexing-azure-blob-storage.md).
* **Magazyn tabel Azure**. Dla docelowej przewodnika [w tym artykule](search-howto-indexing-azure-tables.md).

Firma Microsoft jest uwzględnieniu Dodawanie obsługi dodatkowych źródeł danych w przyszłości hello. toohelp nam priorytety tych decyzji, Dodaj swoją opinię na powitania [forum opinii usługi Azure Search](http://feedback.azure.com/forums/263029-azure-search).

Zobacz [ograniczenia usługi](search-limits-quotas-capacity.md) dla maksymalnie ogranicza powiązane zasoby źródła danych i tooindexer.

## <a name="typical-usage-flow"></a>Typowy sposób przepływu
Możesz utworzyć i zarządzać indeksatorów i źródeł danych za pomocą prostego żądania HTTP (POST, GET, PUT, DELETE) przed danym `data source` lub `indexer` zasobów.

Konfigurowanie automatycznego indeksowania jest zwykle proces krok 4:

1. Zidentyfikuj hello źródła danych, które zawiera dane hello musi toobe indeksowane. Należy pamiętać, że usługi Azure Search może nie obsługiwać wszystkich typów danych hello jest obecny w źródle danych. Zobacz [obsługiwane typy danych](https://msdn.microsoft.com/library/azure/dn798938.aspx) hello listy.
2. Tworzenie indeksu usługi Azure Search, do którego schemat jest zgodny z źródła danych.
3. Utwórz źródło danych usługi Azure Search, zgodnie z opisem w [Utwórz źródło danych](#CreateDataSource).
4. Utwórz indeksator usługi Azure Search, zgodnie z opisem [Utwórz indeksator](#CreateIndexer).

Należy zaplanować na tworzenie jeden indeksator dla każdej kombinacji źródła docelowej, jak indeksu i danych. Może mieć wiele indeksatorów zapisywania do hello sam indeks i może zostać ponownie użyty hello tego samego źródła danych dla wielu indeksatorów. Jednak indeksatora może używać tylko jednego źródła danych w czasie i można zapisywać tylko jeden indeks tooa. 

Po utworzeniu indeksatora, możesz pobrać jego stan wykonania przy użyciu hello [pobierania stanu indeksatora](#GetIndexerStatus) operacji. Można również uruchomić indeksatora w dowolnym momencie (zamiast lub dodanie toorunning ją okresowo zgodnie z harmonogramem) przy użyciu hello [uruchomić indeksatora](#RunIndexer) operacji.

<!-- MSDN has 2 art files plus a API topic link list -->


## <a name="create-data-source"></a>Utwórz źródło danych
W usłudze Azure Search źródło danych jest używany z indeksatorów, dostarczanie informacji połączenia hello odświeżania danych ad hoc ani zaplanowanego indeksu docelowego. Można utworzyć nowego źródła danych w ramach usługi Azure Search przy użyciu żądania HTTP POST.

    POST https://[service name].search.windows.net/datasources?api-version=[api-version]
    Content-Type: application/json
    api-key: [admin key]

Alternatywnie można użyć PUT i określ nazwę źródła danych hello na powitania identyfikatora URI. Witaj źródła danych nie istnieje, zostanie utworzona.

    PUT https://[service name].search.windows.net/datasources/[datasource name]?api-version=[api-version]

> [!NOTE]
> Hello maksymalna liczba źródeł danych, dozwolone jest zależna od warstwy cenowej. Witaj bezpłatnej usługi umożliwia too3 źródeł danych. Standardowa usługa umożliwia 50 źródeł danych. Zobacz [ograniczenia usługi](search-limits-quotas-capacity.md) szczegółowe informacje.
> 
> 

**Żądanie**

HTTPS jest wymagana dla wszystkich żądań obsługi. Witaj **Utwórz źródło danych** żądania może być skonstruowany przy użyciu metody POST i PUT. Korzystając z POST, musisz podać nazwę źródła danych w treści żądania hello wraz z definicji źródła danych hello. Z PUT nazwa hello jest częścią hello adresu URL. Jeśli hello źródła danych nie istnieje, jest tworzony. Jeśli już istnieje, jest nowa definicja toohello zaktualizowane. 

Nazwa źródła danych Hello muszą być małe litery, zaczynać się literą lub cyfrą nie ukośniki lub kropki i mniej niż 128 znaków. Po uruchomieniu nazwa źródła danych hello literą lub cyfrą hello reszty hello nazwa może zawierać żadnych list, numer i kreski, tak długo, jak hello łączniki nie są kolejne. Zobacz [reguły nazewnictwa](https://msdn.microsoft.com/library/azure/dn857353.aspx) szczegółowe informacje.

Witaj `api-version` jest wymagana. Bieżąca wersja Hello jest `2015-02-28`.

**Nagłówki żądania**

powitania po liście opisano hello wymagane i opcjonalne żądania nagłówków. 

* `Content-Type`: Wymagane. Ustaw tę wartość za`application/json`
* `api-key`: Wymagane. Witaj `api-key` jest używane tooauthenticate hello żądania tooyour usługi wyszukiwania. Jest to wartość ciągu, usługa tooyour unikatowy. Witaj **Utwórz źródło danych** żądanie musi zawierać `api-key` nagłówka ustawić tooyour klucza administratora (jako klucz zapytania min. tooa). 

Należy również adres URL hello usługi nazwa tooconstruct hello żądania. Możesz uzyskać zarówno hello nazwy usługi i `api-key` z pulpitu nawigacyjnego usługi w hello [Azure Portal](https://portal.azure.com/). Zobacz [Utwórz usługę wyszukiwania, w portalu hello](search-create-service-portal.md) dla pomocy nawigacji strony.

<a name="CreateDataSourceRequestSyntax"></a>
**Składnia treść żądania**

Witaj treści żądania hello zawiera definicję źródła danych, w tym typ źródła danych hello poświadczenia tooread hello danych, jak również opcjonalne dane wykrywania zmian i zmienić wykrywania usunięcia danych, które identyfikowanie zasad, które są używane tooefficiently lub usuniętych danych w źródle danych hello, gdy jest używany z okresowo zaplanowane indeksatora. 

Witaj dla struktury ładunku żądania hello ma następującą składnię. Przykładowe żądanie znajduje się bardziej szczegółowo na, w tym temacie.

    { 
        "name" : "Required for POST, optional for PUT. hello name of hello data source",
        "description" : "Optional. Anything you want, or nothing at all",
        "type" : "Required. Must be one of 'azuresql', 'documentdb', 'azureblob', or 'azuretable'",
        "credentials" : { "connectionString" : "Required. Connection string for your data source" },
        "container" : { "name" : "Required. hello name of hello table, collection, or blob container you wish tooindex" },
        "dataChangeDetectionPolicy" : { Optional. See below for details }, 
        "dataDeletionDetectionPolicy" : { Optional. See below for details }
    }

Żądanie zawiera hello następujące właściwości: 

* `name`: Wymagane. Nazwa Hello hello źródła danych. Nazwa źródła danych musi jedynie zawierać małe litery, cyfry i łączniki, nie może zaczynać się ani kończyć łączników i ma ograniczone too128 znaków.
* `description`: Opcjonalny opis. 
* `type`: Wymagane. Musi to być jeden z typów źródła danych hello obsługiwane:
  * `azuresql`-Azure SQL Database lub SQL Server na maszynach wirtualnych Azure
  * `documentdb`-DB azure rozwiązania Cosmos
  * `azureblob`-Azure Blob Storage
  * `azuretable`-Azure Table Storage
* `credentials`:
  * Witaj wymagane `connectionString` właściwości określa parametry połączenia hello hello źródła danych. format Hello parametrów połączenia hello zależy od typu źródła danych hello: 
    * Dla bazy danych SQL Azure to hello zwykle parametry połączenia SQL Server. Jeśli używasz parametry połączenia hello Azure tooretrieve portalu hello, użyj hello `ADO.NET connection string` opcji.
    * Dla bazy danych Azure rozwiązania Cosmos, hello parametry połączenia muszą mieć w hello następującego formatu: `"AccountEndpoint=https://[your account name].documents.azure.com;AccountKey=[your account key];Database=[your database id]"`. Wszystkie wartości hello są wymagane. Można je znaleźć w hello [portalu Azure](https://portal.azure.com/).  
    * W przypadku obiektów Blob platformy Azure i Magazyn tabel jest parametry połączenia konta magazynu hello. Hello format jest opisany [tutaj](https://azure.microsoft.com/documentation/articles/storage-configure-connection-string/). Wymagany jest protokół punktu końcowego protokołu HTTPS.  
* `container`, wymagane: Określa hello tooindex danych przy użyciu hello `name` i `query` właściwości: 
  * `name`Wymagane:
    * Azure SQL: Określa hello tabeli lub widoku. Można użyć nazwy kwalifikowanej schematu, takie jak `[dbo].[mytable]`.
    * DocumentDB: Określa kolekcję hello. 
    * Azure Blob Storage: Określa hello kontenera magazynu.
    * Magazyn tabel Azure: Określa nazwę hello hello tabeli. 
  * `query`, opcjonalne:
    * Usługa DocumentDB: umożliwia toospecify kwerendę, która spłaszcza dowolnego układu dokumentu JSON na płaskiej schemat, który można indeksu usługi Azure Search.  
    * Azure Blob Storage: umożliwia toospecify folder wirtualny hello kontenera obiektów blob. Na przykład dla obiekt blob ścieżki `mycontainer/documents/blob.pdf`, `documents` mogą być używane jako folder wirtualny hello.
    * Magazyn tabel Azure: umożliwia toospecify zapytania, że filtry hello zestawu wierszy toobe zaimportowane.
    * Azure SQL: zapytanie nie jest obsługiwane. Jeśli chcesz dodać tę funkcję, proszę Zagłosuj na [sugestia ta](https://feedback.azure.com/forums/263029-azure-search/suggestions/9893490-support-user-provided-query-in-sql-indexer)
* opcjonalne Hello `dataChangeDetectionPolicy` i `dataDeletionDetectionPolicy` właściwości są opisane poniżej.

<a name="DataChangeDetectionPolicies"></a>
**Zasady wykrywania zmian danych**

cel Hello danych zmienić zasady wykrywania jest tooefficiently zidentyfikować elementy zmienione dane. Obsługiwane zasady różnić w zależności od typu źródła danych hello. Poniższe rozdziały zawierają opis poszczególnych zasad. 

***Zasady wykrywania zmian górnego limitu*** 

Użyj tych zasad, gdy źródło danych zawiera kolumny lub właściwości, które spełnia następujące kryteria hello:

* Wstawia wszystkie Określ wartość dla kolumny hello. 
* Elementu tooan wszystkie aktualizacje także zmienić wartość hello hello kolumny. 
* zwiększa wartość Hello tej kolumny przy każdej zmianie.
* Zapytania, które filtru klauzuli podobne toohello poniższych `WHERE [High Water Mark Column] > [Current High Water Mark Value]` mogą być wykonywane wydajnie.

Na przykład używając źródeł danych Azure SQL, indeksowanego `rowversion` kolumna jest hello candidate nadaje się doskonale dla systemu hello znacznik limitu górnego zasad. 

Te zasady można określić w następujący sposób:

    { 
        "@odata.type" : "#Microsoft.Azure.Search.HighWaterMarkChangeDetectionPolicy",
        "highWaterMarkColumnName" : "[a row version or last_updated column name]" 
    } 

Podczas korzystania z bazy danych Azure rozwiązania Cosmos źródeł danych, należy użyć hello `_ts` właściwości udostępniane przez bazy danych Azure rozwiązania Cosmos. 

Używając źródeł danych obiektów Blob platformy Azure, Azure Search automatycznie używa górny limit zmienić zasady wykrywania oparte na sygnatura czasowa ostatniej modyfikacji obiektu blob; nie trzeba toospecify takie zasady samodzielnie.   

***Zasady wykrywania zmian zintegrowane ze środowiskiem SQL***

Jeśli baza danych SQL obsługuje [śledzenie zmian](https://msdn.microsoft.com/library/bb933875.aspx), firma Microsoft zaleca używanie SQL zintegrowane zmienić zasady śledzenia. Ta zasada umożliwia śledzenie zmian najbardziej efektywne hello i umożliwia wierszy tooidentify usunięte usługi Azure Search bez konieczności toohave explicit "usuwania nietrwałego" kolumny w schemat.

Zintegrowane śledzenie zmian jest obsługiwane począwszy od powitania po wersji bazy danych programu SQL Server: 

* SQL Server 2008 R2, jeśli używasz programu SQL Server na maszynach wirtualnych platformy Azure.
* Azure SQL Database V12, jeśli używasz bazy danych SQL Azure.  

Gdy za pomocą zintegrowanego śledzenia zmian programu SQL zasad, nie określaj odrębne zasady usuwania i wykrywania — ta zasada ma wbudowaną obsługę identyfikowanie usuniętych wierszy. 

Te zasady można używać tylko z tabelami; Nie można używać z widokami. Należy tooenable śledzenia zmian dla tabeli hello, używanego przed użyciem tych zasad. Zobacz [włączyć lub wyłączyć śledzenie zmian](https://msdn.microsoft.com/library/bb964713.aspx) instrukcje.    

Przy tworzeniu struktury hello **Utwórz źródło danych** żądania SQL zintegrowane zasad śledzenia zmian można określić w następujący sposób:

    { 
        "@odata.type" : "#Microsoft.Azure.Search.SqlIntegratedChangeTrackingPolicy" 
    }

<a name="DataDeletionDetectionPolicies"></a>
**Zasady wykrywania usunięcia danych**

Witaj zasady wykrywania usuwania danych służy tooefficiently zidentyfikować elementy usunięte dane. Witaj obsługiwane tylko zasady jest obecnie hello `Soft Delete` zasada, która umożliwia zidentyfikowanie usuniętych elementów na podstawie wartości hello `soft delete` kolumny lub właściwości w źródle danych hello. Te zasady można określić w następujący sposób:

    { 
        "@odata.type" : "#Microsoft.Azure.Search.SoftDeleteColumnDeletionDetectionPolicy",
        "softDeleteColumnName" : "hello column that specifies whether a row was deleted", 
        "softDeleteMarkerValue" : "hello value that identifies a row as deleted" 
    }

> [!NOTE]
> Obsługiwane są tylko kolumny z ciągiem, liczbą całkowitą lub wartości logiczne. Witaj użyta jako wartość `softDeleteMarkerValue` musi być ciągiem, nawet wtedy, gdy odpowiednia kolumna hello przechowuje liczb całkowitych lub wartości logiczne. Na przykład, jeśli wartość hello, która pojawia się w źródle danych 1, użyj `"1"` jako hello `softDeleteMarkerValue`.    
> 
> 

<a name="CreateDataSourceRequestExamples"></a>
**Przykłady treść żądania**

Jeśli planujesz źródło danych hello toouse o indeksatorze, który jest uruchamiany zgodnie z harmonogramem, w tym przykładzie pokazano, jak zmienić toospecify i usuwanie zasad wykrywania: 

    { 
        "name" : "asqldatasource",
        "description" : "a description",
        "type" : "azuresql",
        "credentials" : { "connectionString" : "Server=tcp:....database.windows.net,1433;Database=...;User ID=...;Password=...;Trusted_Connection=False;Encrypt=True;Connection Timeout=30;" },
        "container" : { "name" : "sometable" },
        "dataChangeDetectionPolicy" : { "@odata.type" : "#Microsoft.Azure.Search.HighWaterMarkChangeDetectionPolicy", "highWaterMarkColumnName" : "RowVersion" }, 
        "dataDeletionDetectionPolicy" : { "@odata.type" : "#Microsoft.Azure.Search.SoftDeleteColumnDeletionDetectionPolicy", "softDeleteColumnName" : "IsDeleted", "softDeleteMarkerValue" : "true" }
    }

Jeśli planujesz tylko źródła danych hello toouse jednorazowych kopii danych hello, można pominąć hello zasad:

    { 
        "name" : "asqldatasource",
        "description" : "anything you want, or nothing at all",
        "type" : "azuresql",
        "credentials" : { "connectionString" : "Server=tcp:....database.windows.net,1433;Database=...;User ID=...;Password=...;Trusted_Connection=False;Encrypt=True;Connection Timeout=30;" },
        "container" : { "name" : "sometable" }
    } 

**Odpowiedź**

Żądanie powiodło się: 201 utworzono. 

<a name="UpdateDataSource"></a>

## <a name="update-data-source"></a>Aktualizacja źródła danych
Można aktualizować istniejącego źródła danych za pomocą żądania HTTP PUT. Należy określić nazwę hello tooupdate źródła danych hello na powitania identyfikatora URI żądania:

    PUT https://[service name].search.windows.net/datasources/[datasource name]?api-version=[api-version]
    Content-Type: application/json
    api-key: [admin key]

Witaj `api-version` jest wymagana. Bieżąca wersja Hello jest `2015-02-28`. [Azure wersji interfejsu API Search](https://msdn.microsoft.com/library/azure/dn864560.aspx) ma szczegóły i dodatkowe informacje o alternatywne wersje.

Witaj `api-key` musi mieć klucz administratora (jako klucz zapytania min. tooa). Zobacz sekcja authentication toohello w [interfejsu API REST usługi wyszukiwania](https://msdn.microsoft.com/library/azure/dn798935.aspx) toolearn więcej informacji na temat kluczy. [Utwórz usługę wyszukiwania, w portalu hello](search-create-service-portal.md) wyjaśniono, jak użyć adresu URL usługi hello tooget i właściwości klucza w żądaniu hello.

**Żądanie**

Witaj składni treść żądania jest hello takie same jak w przypadku [Utwórz źródło danych żądań](#CreateDataSourceRequestSyntax).

Nie można zaktualizować niektóre właściwości w istniejącym źródle danych. Na przykład nie można zmienić typu hello istniejącego źródła danych.  

Jeśli nie chcesz parametry połączenia hello toochange dla istniejącego źródła danych, można określić hello literału `<unchanged>` hello ciągu połączenia. Jest to przydatne w sytuacjach, gdy konieczne tooupdate źródła danych, ale nie ma parametrów połączenia toohello najwygodniejszy dostęp, ponieważ są to dane dotyczące zabezpieczeń.

**Odpowiedź**

Dla pomyślnego żądania: 201 utworzono Jeśli nowego źródła danych został utworzony i 204 nr zawartości, jeśli źródło danych zostało zaktualizowane.

<a name="ListDataSource"></a>

## <a name="list-data-sources"></a>Lista źródeł danych
Witaj **listy źródeł danych** operacji zwraca listę hello źródeł danych w usłudze Azure Search. 

    GET https://[service name].search.windows.net/datasources?api-version=[api-version]
    api-key: [admin key]

Witaj `api-version` jest wymagana. Bieżąca wersja Hello jest `2015-02-28`. 

Witaj `api-key` musi mieć klucz administratora (jako klucz zapytania min. tooa). Zobacz sekcja authentication toohello w [interfejsu API REST usługi wyszukiwania](https://msdn.microsoft.com/library/azure/dn798935.aspx) toolearn więcej informacji na temat kluczy. [Utwórz usługę wyszukiwania, w portalu hello](search-create-service-portal.md) wyjaśniono, jak użyć adresu URL usługi hello tooget i właściwości klucza w żądaniu hello.

**Odpowiedź**

Żądanie powiodło się: 200 OK.

Oto przykład treści odpowiedzi:

    {
      "value" : [
        {
          "name": "datasource1",
          "type": "azuresql",
          ... other data source properties
        }]
    }

Należy pamiętać, filtrować odpowiedź hello toojust hello właściwości, które interesują Cię w dół. Na przykład, jeśli chcesz tylko listę nazw źródeł danych, użyj hello OData `$select` opcji zapytania:

    GET /datasources?api-version=205-02-28&$select=name

W takim przypadku hello odpowiedzi z hello powyżej przykład będzie wyglądać następująco: 

    {
      "value" : [ { "name": "datasource1" }, ... ]
    }

Jest to przepustowości toosave technika przydatne, jeśli masz wiele źródeł danych w usłudze wyszukiwania.

<a name="GetDataSource"></a>

## <a name="get-data-source"></a>Pobierz źródła danych
Witaj **pobrać źródła danych** operacji definicji źródła danych hello są pobierane z usługi Azure Search.

    GET https://[service name].search.windows.net/datasources/[datasource name]?api-version=[api-version]
    api-key: [admin key]

Witaj `api-version` jest wymagana. Bieżąca wersja Hello jest `2015-02-28`. 

Witaj `api-key` musi mieć klucz administratora (jako klucz zapytania min. tooa). Zobacz sekcja authentication toohello w [interfejsu API REST usługi wyszukiwania](https://msdn.microsoft.com/library/azure/dn798935.aspx) toolearn więcej informacji na temat kluczy. [Utwórz usługę wyszukiwania, w portalu hello](search-create-service-portal.md) wyjaśniono, jak użyć adresu URL usługi hello tooget i właściwości klucza w żądaniu hello.

**Odpowiedź**

Kod stanu: 200 OK jest zwracana dla pomyślnej odpowiedzi.

odpowiedź Hello jest podobne tooexamples w [Utwórz źródło danych żądań przykład](#CreateDataSourceRequestExamples): 

    { 
        "name" : "asqldatasource",
        "description" : "a description",
        "type" : "azuresql",
        "credentials" : { "connectionString" : "Server=tcp:....database.windows.net,1433;Database=...;User ID=...;Password=...;Trusted_Connection=False;Encrypt=True;Connection Timeout=30;" },
        "container" : { "name" : "sometable" },
        "dataChangeDetectionPolicy" : { 
            "@odata.type" : "#Microsoft.Azure.Search.HighWaterMarkChangeDetectionPolicy",
            "highWaterMarkColumnName" : "RowVersion" }, 
        "dataDeletionDetectionPolicy" : { 
            "@odata.type" : "#Microsoft.Azure.Search.SoftDeleteColumnDeletionDetectionPolicy",
            "softDeleteColumnName" : "IsDeleted", 
            "softDeleteMarkerValue" : "true" }
    }

> [!NOTE]
> Nie ustawiaj hello `Accept` nagłówek żądania zbyt`application/json;odata.metadata=none` po wywołujący ten interfejs API jako w ten sposób spowoduje, że `@odata.type` toobe atrybutu pominięte hello odpowiedzi i nie będzie możliwe toodifferentiate między zmianami danych i dane wykrywania usunięcia zasady różnych typów. 
> 
> 

<a name="DeleteDataSource"></a>

## <a name="delete-data-source"></a>Usunąć źródła danych
Witaj **usunąć źródło danych** operacji usuwa źródła danych z usługi Azure Search.

    DELETE https://[service name].search.windows.net/datasources/[datasource name]?api-version=[api-version]
    api-key: [admin key]

> [!NOTE]
> Jeśli wszystkie indeksatory odwołać hello źródła danych, które usuwane, operacja usuwania hello nadal będzie kontynuowana. Jednak te indeksatory przechodzi w stan błędu po jego następnym uruchomieniu.  
> 
> 

Witaj `api-version` jest wymagana. Bieżąca wersja Hello jest `2015-02-28`. 

Witaj `api-key` musi mieć klucz administratora (jako klucz zapytania min. tooa). Zobacz sekcja authentication toohello w [interfejsu API REST usługi wyszukiwania](https://msdn.microsoft.com/library/azure/dn798935.aspx) toolearn więcej informacji na temat kluczy. [Utwórz usługę wyszukiwania, w portalu hello](search-create-service-portal.md) wyjaśniono, jak użyć adresu URL usługi hello tooget i właściwości klucza w żądaniu hello.

**Odpowiedź**

Kod stanu: 204 nr zawartości jest zwracana dla pomyślnej odpowiedzi.

<a name="CreateIndexer"></a>

## <a name="create-indexer"></a>Utwórz indeksator
Można utworzyć nowego indeksatora w ramach usługi Azure Search przy użyciu żądania HTTP POST.

    POST https://[service name].search.windows.net/indexers?api-version=[api-version]
    Content-Type: application/json
    api-key: [admin key]

Alternatywnie można użyć PUT i określ nazwę źródła danych hello na powitania identyfikatora URI. Witaj źródła danych nie istnieje, zostanie utworzona.

    PUT https://[service name].search.windows.net/indexers/[indexer name]?api-version=[api-version]

> [!NOTE]
> Maksymalna liczba indeksatorów dozwolone Hello jest zależna od warstwy cenowej. Usługa wolnego Hello umożliwia się too3 indeksatorów. Standardowa usługa umożliwia indeksatory 50. Zobacz [ograniczenia usługi](search-limits-quotas-capacity.md) szczegółowe informacje.
> 
> 

Witaj `api-version` jest wymagana. Bieżąca wersja Hello jest `2015-02-28`. 

Witaj `api-key` musi mieć klucz administratora (jako klucz zapytania min. tooa). Zobacz sekcja authentication toohello w [interfejsu API REST usługi wyszukiwania](https://msdn.microsoft.com/library/azure/dn798935.aspx) toolearn więcej informacji na temat kluczy. [Utwórz usługę wyszukiwania, w portalu hello](search-create-service-portal.md) wyjaśniono, jak użyć adresu URL usługi hello tooget i właściwości klucza w żądaniu hello.

<a name="CreateIndexerRequestSyntax"></a>
**Składnia treść żądania**

Witaj treści żądania hello zawiera definicję indeksatora, który określa źródło danych hello i indeksu docelowego hello indeksowania, a także opcjonalnie harmonogram indeksowania i parametrów. 

Witaj dla struktury ładunku żądania hello ma następującą składnię. Przykładowe żądanie znajduje się bardziej szczegółowo na, w tym temacie.

    { 
        "name" : "Required for POST, optional for PUT. hello name of hello indexer",
        "description" : "Optional. Anything you want, or null",
        "dataSourceName" : "Required. hello name of an existing data source",
        "targetIndexName" : "Required. hello name of an existing index",
        "schedule" : { Optional. See Indexing Schedule below. },
        "parameters" : { Optional. See Indexing Parameters below. },
        "fieldMappings" : { Optional. See Field Mappings below. },
        "disabled" : Optional boolean value indicating whether hello indexer is disabled. False by default.  
    }

**Planowanie uruchamiania indeksatora**

Indeksator Opcjonalnie można określić harmonogramu. Jeśli harmonogram, hello indeksator będzie uruchamiana okresowo zgodnie z harmonogramem. Harmonogram ma hello następujące atrybuty:

* `interval`: Wymagane. Uruchamia wartości czasu trwania, który określa interwał lub okres indeksatora. najmniejsza Hello dozwolony interwał wynosi 5 minut; Najdłuższy Hello jest jeden dzień. Musi być sformatowany jako wartość XSD "dayTimeDuration" (ograniczony podzestaw [czasu trwania ISO 8601](http://www.w3.org/TR/xmlschema11-2/#dayTimeDuration) wartości). wzór Hello: `"P[nD][T[nH][nM]]"`. Przykłady: `PT15M` co 15 minut, `PT2H` co 2 godziny. 
* `startTime`: Wymagane. Element datetime UTC podczas hello indeksator powinien rozpocząć uruchamianie. 

**Parametry indeksatora**

Indeksator Opcjonalnie można określić kilka parametrów, które mają wpływ na jego zachowania. Wszystkie parametry hello są opcjonalne.  

* `maxFailedItems`: hello liczba elementów, które mogą nie toobe indeksowane, zanim uruchomienie indeksatora zostanie uznane za błąd. Domyślna to 0. Zwraca informacje o elementach nie powiodło się hello [pobierania stanu indeksatora](#GetIndexerStatus) operacji. 
* `maxFailedItemsPerBatch`: hello liczba elementów, które mogą nie toobe pomyślnie zindeksowane w każdej z partii, zanim uruchomienie indeksatora zostanie uznane za błąd. Domyślna to 0.
* `base64EncodeKeys`: Określa, czy klucze dokumentu będą algorytmem base-64. Wyszukiwanie Azure nakłada ograniczenia dotyczące znaków, które mogą być obecne w kluczu dokumentu. Jednak wartości hello w źródle danych może zawierać znaków, które nie są prawidłowe. Jeśli jest konieczne tooindex takie wartości jako klucze dokumentu, tę flagę można ustawić tootrue. Domyślnie jest `false`.
* `batchSize`: Określa numer hello elementy, które są odczytywane hello źródła danych i indeksowane jako pojedyncza partia w kolejności tooimprove wydajności. Domyślna Hello zależy od typu źródła danych hello: 1000 Azure SQL i bazy danych Azure rozwiązania Cosmos i 10 dla magazynu obiektów Blob Azure.

**Mapowania pól**

W hello danych źródła tooa inną nazwę pola w indeksie docelowy hello służy toomap mapowania pola nazwę pola. Rozważmy na przykład tabeli źródłowej z polem `_id`. Usługa Azure Search nie zezwala na nazwę pola, począwszy od znaku podkreślenia, można zmienić nazwy pola hello. Można to zrobić przy użyciu hello `fieldMappings` właściwości indeksatora hello w następujący sposób: 

    "fieldMappings" : [ { "sourceFieldName" : "_id", "targetFieldName" : "id" } ] 

Można określić wiele mapowań pól: 

    "fieldMappings" : [ 
        { "sourceFieldName" : "_id", "targetFieldName" : "id" },
        { "sourceFieldName" : "_timestamp", "targetFieldName" : "timestamp" },
     ]

Nazwy pól w pliku źródłowym i docelowym jest rozróżniana wielkość liter.

<a name="FieldMappingFunctions"></a>
***Funkcje mapowania pól***

Mapowania pól mogą być również wartości pól źródła tootransform używane przy użyciu *mapowania funkcji*.

Tylko jeden taki funkcja jest obecnie obsługiwany: `jsonArrayToStringCollection`. Analizuje pola, które zawiera ciąg sformatowany jako tablica JSON pola Collection(Edm.String) hello indeksu docelowego. Ma ona do użycia z programem Azure SQL indeksatora w szczególności, ponieważ SQL nie ma typu natywnego kolekcji danych. Mogą być używane w następujący sposób: 

    "fieldMappings" : [ { "sourceFieldName" : "tags", "mappingFunction" : { "name" : "jsonArrayToStringCollection" } } ] 

Na przykład jeśli hello źródła pole zawiera ciąg hello `["red", "white", "blue"]`, a następnie hello pola docelowego typu `Collection(Edm.String)` zostaną wypełnione wartościami hello trzech `"red"`, `"white"` i `"blue"`.

Należy pamiętać, że hello `targetFieldName` właściwość jest opcjonalna; Jeśli, hello `sourceFieldName` wartość jest używana. 

<a name="CreateIndexerRequestExamples"></a>
**Przykłady treść żądania**

Witaj poniższy przykład tworzy indeksatorze, który kopiuje dane z tabeli hello odwołuje się hello `ordersds` toohello źródła danych `orders` indeksu zgodnie z harmonogramem, który rozpoczyna się 1 stycznia 2015 UTC i jest uruchamiana co godzinę. Każde wywołanie indeksatora zakończy się pomyślnie, jeśli elementy nie więcej niż 5 nie toobe pomyślnie zindeksowane w każdej partii, i nie więcej niż 10 elementów nie toobe indeksowane w sumie. 

    {
        "name" : "myindexer",
        "description" : "a cool indexer",
        "dataSourceName" : "ordersds",
        "targetIndexName" : "orders",
        "schedule" : { "interval" : "PT1H", "startTime" : "2015-01-01T00:00:00Z" },
        "parameters" : { "maxFailedItems" : 10, "maxFailedItemsPerBatch" : 5, "base64EncodeKeys": false }
    }

**Odpowiedź**

201 utworzono dla pomyślnego żądania.

<a name="UpdateIndexer"></a>

## <a name="update-indexer"></a>Aktualizacja indeksatora
Można aktualizować istniejącego indeksatora za pomocą żądania HTTP PUT. Należy określić nazwę hello tooupdate indeksatora hello na powitania identyfikatora URI żądania:

    PUT https://[service name].search.windows.net/indexers/[indexer name]?api-version=[api-version]
    Content-Type: application/json
    api-key: [admin key]

Witaj `api-version` jest wymagana. Bieżąca wersja Hello jest `2015-02-28`. 

Witaj `api-key` musi mieć klucz administratora (jako klucz zapytania min. tooa). Zobacz sekcja authentication toohello w [interfejsu API REST usługi wyszukiwania](https://msdn.microsoft.com/library/azure/dn798935.aspx) toolearn więcej informacji na temat kluczy. [Utwórz usługę wyszukiwania, w portalu hello](search-create-service-portal.md) wyjaśniono, jak użyć adresu URL usługi hello tooget i właściwości klucza w żądaniu hello.

**Żądanie**

Witaj składni treść żądania jest hello takie same jak w przypadku [żądań tworzenia indeksatora](#CreateIndexerRequestSyntax).

**Odpowiedź**

Dla pomyślnego żądania: 201 utworzono, jeśli nowy indeksator został utworzony i 204 nr zawartości jeśli istniejącego indeksatora został zaktualizowany.

<a name="ListIndexers"></a>

## <a name="list-indexers"></a>Indeksatory listy
Witaj **indeksatory listy** operacji zwraca listę hello indeksatory w usłudze Azure Search. 

    GET https://[service name].search.windows.net/indexers?api-version=[api-version]
    api-key: [admin key]


Witaj `api-version` jest wymagana. Wersja zapoznawcza Hello jest `2015-02-28-Preview`. [Azure versioning wyszukiwania](https://msdn.microsoft.com/library/azure/dn864560.aspx) ma szczegóły i dodatkowe informacje o alternatywne wersje.

Witaj `api-key` musi mieć klucz administratora (jako klucz zapytania min. tooa). Zobacz sekcja authentication toohello w [interfejsu API REST usługi wyszukiwania](https://msdn.microsoft.com/library/azure/dn798935.aspx) toolearn więcej informacji na temat kluczy. [Utwórz usługę wyszukiwania, w portalu hello](search-create-service-portal.md) wyjaśniono, jak użyć adresu URL usługi hello tooget i właściwości klucza w żądaniu hello.

**Odpowiedź**

Żądanie powiodło się: 200 OK.

Oto przykład treści odpowiedzi:

    {
      "value" : [
      {
        "name" : "myindexer",
        "description" : "a cool indexer",
        "dataSourceName" : "ordersds",
        "targetIndexName" : "orders",
        ... other indexer properties
      }]
    }

Należy pamiętać, filtrować odpowiedź hello toojust hello właściwości, które interesują Cię w dół. Na przykład, jeśli chcesz tylko listę nazw indeksatora, użyj hello OData `$select` opcji zapytania:

    GET /indexers?api-version=2014-10-20-Preview&$select=name

W takim przypadku hello odpowiedzi z hello powyżej przykład będzie wyglądać następująco: 

    {
      "value" : [ { "name": "myindexer" } ]
    }

Jest to przepustowości toosave technika przydatne, jeśli masz wiele indeksatorów w swojej usłudze wyszukiwania.

<a name="GetIndexer"></a>

## <a name="get-indexer"></a>Pobierz indeksatora
Witaj **uzyskać indeksatora** operacji definicji indeksatora hello są pobierane z usługi Azure Search.

    GET https://[service name].search.windows.net/indexers/[indexer name]?api-version=[api-version]
    api-key: [admin key]

Witaj `api-version` jest wymagana. Wersja zapoznawcza Hello jest `2015-02-28-Preview`. 

Witaj `api-key` musi mieć klucz administratora (jako klucz zapytania min. tooa). Zobacz sekcja authentication toohello w [interfejsu API REST usługi wyszukiwania](https://msdn.microsoft.com/library/azure/dn798935.aspx) toolearn więcej informacji na temat kluczy. [Utwórz usługę wyszukiwania, w portalu hello](search-create-service-portal.md) wyjaśniono, jak użyć adresu URL usługi hello tooget i właściwości klucza w żądaniu hello.

**Odpowiedź**

Kod stanu: 200 OK jest zwracana dla pomyślnej odpowiedzi.

odpowiedź Hello jest podobne tooexamples w [żądań przykład utwórz indeksator](#CreateIndexerRequestExamples): 

    {
        "name" : "myindexer",
        "description" : "a cool indexer",
        "dataSourceName" : "ordersds",
        "targetIndexName" : "orders",
        "schedule" : { "interval" : "PT1H", "startTime" : "2015-01-01T00:00:00Z" },
        "parameters" : { "maxFailedItems" : 10, "maxFailedItemsPerBatch" : 5, "base64EncodeKeys": false }
    }


<a name="DeleteIndexer"></a>

## <a name="delete-indexer"></a>Usuń indeksatora
Witaj **usunąć indeksator** operacji usuwa indeksatora z usługi Azure Search.

    DELETE https://[service name].search.windows.net/indexers/[indexer name]?api-version=[api-version]
    api-key: [admin key]

Po usunięciu indeksatora hello wykonaniami indeksatora w toku w tym czasie będą działać toocompletion, ale nie dalsze wykonaniami zostanie zaplanowane. Nie można odnaleźć toouse prób, indeksatora nieistniejącą spowoduje kod stanu HTTP 404. 

Witaj `api-version` jest wymagana. Wersja zapoznawcza Hello jest `2015-02-28-Preview`. 

Witaj `api-key` musi mieć klucz administratora (jako klucz zapytania min. tooa). Zobacz sekcja authentication toohello w [interfejsu API REST usługi wyszukiwania](https://msdn.microsoft.com/library/azure/dn798935.aspx) toolearn więcej informacji na temat kluczy. [Utwórz usługę wyszukiwania, w portalu hello](search-create-service-portal.md) wyjaśniono, jak użyć adresu URL usługi hello tooget i właściwości klucza w żądaniu hello.

**Odpowiedź**

Kod stanu: 204 nr zawartości jest zwracana dla pomyślnej odpowiedzi.

<a name="RunIndexer"></a>

## <a name="run-indexer"></a>Uruchomić indeksatora
W dodatku toorunning okresowo zgodnie z harmonogramem, indeksatora może być wywoływana na żądanie za pośrednictwem hello **uruchomić indeksatora** operacji: 

    POST https://[service name].search.windows.net/indexers/[indexer name]/run?api-version=[api-version]
    api-key: [admin key]

Witaj `api-version` jest wymagana. Wersja zapoznawcza Hello jest `2015-02-28-Preview`. 

Witaj `api-key` musi mieć klucz administratora (jako klucz zapytania min. tooa). Zobacz sekcja authentication toohello w [interfejsu API REST usługi wyszukiwania](https://msdn.microsoft.com/library/azure/dn798935.aspx) toolearn więcej informacji na temat kluczy. [Utwórz usługę wyszukiwania, w portalu hello](search-create-service-portal.md) wyjaśniono, jak użyć adresu URL usługi hello tooget i właściwości klucza w żądaniu hello.

**Odpowiedź**

Kod stanu: 202 zaakceptowane jest zwracana dla pomyślnej odpowiedzi.

<a name="GetIndexerStatus"></a>

## <a name="get-indexer-status"></a>Pobierz stan indeksatora
Witaj **pobierania stanu indeksatora** hello bieżący stan i wykonywanie historię indeksator pobiera operacji: 

    GET https://[service name].search.windows.net/indexers/[indexer name]/status?api-version=[api-version]
    api-key: [admin key]


Witaj `api-version` jest wymagana. Wersja zapoznawcza Hello jest `2015-02-28-Preview`. 

Witaj `api-key` musi mieć klucz administratora (jako klucz zapytania min. tooa). Zobacz sekcja authentication toohello w [interfejsu API REST usługi wyszukiwania](https://msdn.microsoft.com/library/azure/dn798935.aspx) toolearn więcej informacji na temat kluczy. [Utwórz usługę wyszukiwania, w portalu hello](search-create-service-portal.md) wyjaśniono, jak użyć adresu URL usługi hello tooget i właściwości klucza w żądaniu hello.

**Odpowiedź**

Kod stanu: 200 OK dla pomyślnej odpowiedzi.

treść odpowiedzi Hello informacjami o ogólny stan kondycji indeksatora hello ostatniego wywołanie indeksatora, jak również historię hello ostatnie wywołań indeksatora (jeśli istnieje). 

Treść odpowiedzi próbki wygląda następująco: 

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

**Stan indeksatora**

Stan indeksatora może być jedną z hello następujące wartości:

* `running`Wskazuje, że ten indeksator hello działa normalnie. Pamiętaj, że nadal mogą niektóre hello wykonaniami indeksatora nie, więc hello toocheck dobrze `lastResult` również właściwość. 
* `error`Wskazuje, że ten indeksator hello wystąpił błąd, których nie można rozwiązać bez udziału człowieka. Na przykład poświadczenia źródła danych hello mogło wygasnąć lub hello schematu źródła danych hello lub indeksu docelowego hello została zmieniona w podziału sposób. 

**Wynik wykonywania indeksatora**

Wynik wykonania indeksatora zawiera informacje o wykonanie jednej indeksatora. Najnowsze wyniki Hello jest wyświetlana jako hello `lastResult` właściwości hello stan indeksatora. Inne ostatnie wyniki, jeśli jest obecny, są zwracane jako hello `executionHistory` właściwości hello stan indeksatora. 

Wynik wykonywania indeksatora zawiera hello następujące właściwości: 

* `status`: hello stanu wykonywania. Zobacz [stan wykonania indeksatora](#IndexerExecutionStatus) poniżej szczegółowe informacje. 
* `errorMessage`: komunikat o błędzie dla wykonanie nie powiodło się. 
* `startTime`: hello czasu UTC podczas uruchamiania to wykonanie.
* `endTime`: hello czasu UTC, po zakończeniu wykonywania tej. Ta wartość nie jest ustawiona, jeśli wykonanie hello jest nadal w toku.
* `errors`: tablica błędy na poziomie elementu, jeśli istnieje. Każdy wpis zawiera klucz dokumentu (`key` właściwości) oraz komunikat o błędzie (`errorMessage` właściwości). 
* `itemsProcessed`: hello liczbę elementów źródła danych (na przykład wiersze tabeli), które hello tooindex indeksatora podjęto podczas wykonywania tego. 
* `itemsFailed`: liczba elementów, których nie powiodła się podczas wykonywania tego hello.  
* `initialTrackingState`: zawsze `null` hello pierwszy wykonywanie indeksatora, lub jeśli danych hello zmienić zasady śledzenia nie jest włączona na powitania źródło danych używane. Po włączeniu tych zasad podczas kolejnych wykonań kodu ta wartość oznacza hello pierwsza zmiana (najniższy) śledzenia wartość przetwarzane przez to wykonanie. 
* `finalTrackingState`: zawsze `null` hello danych zmiany zasad śledzenia nie jest włączona na powitania źródło danych używane. Wskazuje, w przeciwnym razie hello najnowsze zmiany (najwyższy) śledzenia wartość pomyślnie przetworzone przez wykonanie tego. 

<a name="IndexerExecutionStatus"></a>
**Stan wykonania indeksatora**

Stan wykonania indeksatora przechwytuje stan hello wykonanie jednej indeksatora. Może mieć hello następujące wartości:

* `success`Wskazuje, czy wykonywanie indeksatora hello zostało zakończone pomyślnie.
* `inProgress`Wskazuje, że wykonywanie indeksatora hello jest w toku. 
* `transientFailure`Wskazuje, że wykonywanie indeksatora nie powiodła się. Zobacz `errorMessage` właściwości, aby uzyskać szczegółowe informacje. Błąd Hello może lub nie może wymagać interwencji człowieka toofix — wymaga na przykład ustalenia niezgodności między źródłem danych hello i indeksu docelowego hello schematów akcja ze strony użytkownika, a przestoju źródła danych tymczasowych nie. Wywołania indeksator będzie według harmonogramu, jeśli występuje. 
* `persistentFailure`Wskazuje, że ten indeksator hello nie powiodło się w taki sposób, który wymaga udziału człowieka. Zatrzymaj wykonaniami zaplanowane indeksatora. Po rozwiązaniu problemu hello, użyj wykonaniami hello zaplanowane toorestart zresetować indeksatora API. 
* `reset`Wskazuje, że ten indeksator hello zostało zresetowane przez tooReset wywołania interfejsu API indeksatora (patrz poniżej). 

<a name="ResetIndexer"></a>

## <a name="reset-indexer"></a>Zresetować indeksatora
Witaj **zresetować indeksatora** operacji resetuje stan skojarzony z indeksatora hello zmian hello. Umożliwia ponowne indeksowanie (na przykład w przypadku zmiany schematu źródła danych) z podstaw dla tootrigger lub toochange hello danych zasad wykrywania zmian dla źródła danych skojarzone z indeksatora hello.   

    POST https://[service name].search.windows.net/indexers/[indexer name]/reset?api-version=[api-version]
    api-key: [admin key]

Witaj `api-version` jest wymagana. Wersja zapoznawcza Hello jest `2015-02-28-Preview`. 

Witaj `api-key` musi mieć klucz administratora (jako klucz zapytania min. tooa). Zobacz sekcja authentication toohello w [interfejsu API REST usługi wyszukiwania](https://msdn.microsoft.com/library/azure/dn798935.aspx) toolearn więcej informacji na temat kluczy. [Utwórz usługę wyszukiwania, w portalu hello](search-create-service-portal.md) wyjaśniono, jak użyć adresu URL usługi hello tooget i właściwości klucza w żądaniu hello.

**Odpowiedź**

Kod stanu: 204 nr zawartości dla pomyślnej odpowiedzi.

## <a name="mapping-between-sql-data-types-and-azure-search-data-types"></a>Mapowanie między typy danych SQL i typy danych w usłudze Azure Search
<table style="font-size:12">
<tr>
<td>Typ danych SQL</td>    
<td>Dozwolone typy pól indeksu docelowego</td>
<td>Uwagi</td>
</tr>
<tr>
<td>bitowe</td>
<td>Typem Edm.Boolean, typem Edm.String</td>
<td></td>
</tr>
<tr>
<td>int, smallint, tinyint</td>
<td>Typem Edm.String z typem Edm.Int32, Edm.Int64,</td>
<td></td>
</tr>
<tr>
<td>bigint</td>
<td>Edm.Int64, typem Edm.String</td>
<td></td>
</tr>
<tr>
<td>rzeczywiste, float</td>
<td>Edm.Double, typem Edm.String</td>
<td></td>
</tr>
<tr>
<td>Smallmoney, pieniędzy<br>Decimal<br>numeryczne
</td>
<td>Edm.String</td>
<td>Usługa Azure Search nie obsługuje konwersji typu decimal do Edm.Double, ponieważ spowoduje to utratę dokładności
</td>
</tr>
<tr>
<td>char, nchar, varchar, nvarchar</td>
<td>Edm.String<br/>Collection(Edm.String)</td>
<td>Zobacz [funkcje mapowania pól](#FieldMappingFunctions) w tym dokumencie, aby uzyskać więcej informacji na temat tootransform kolumny ciągu na Collection(Edm.String)</td>
</tr>
<tr>
<td>smalldatetime, datetime, datetime2, date, datetimeoffset</td>
<td>Edm.DateTimeOffset, typem Edm.String</td>
<td></td>
</tr>
<tr>
<td>uniqueidentifer</td>
<td>Edm.String</td>
<td></td>
</tr>
<tr>
<td>Lokalizacja geograficzna</td>
<td>Edm.GeographyPoint</td>
<td>Obsługiwane są tylko geograficzne wystąpienia typu punktu z 4326 SRID, (który jest domyślnym hello)</td>
</tr>
<tr>
<td>ROWVERSION</td>
<td>Nie dotyczy</td>
<td>Kolumny wersji wiersza nie mogą być przechowywane w hello indeksu wyszukiwania, ale może służyć do śledzenia zmian</td>
</tr>
<tr>
<td>czas, timespan<br>Binary, varbinary, obraz,<br>Kod XML, geometry, typy CLR</td>
<td>Nie dotyczy</td>
<td>Nieobsługiwane</td>
</tr>
</table>

## <a name="mapping-between-json-data-types-and-azure-search-data-types"></a>Mapowanie między typami danych JSON i typy danych w usłudze Azure Search
<table style="font-size:12">
<tr>
<td>Typ danych JSON</td>    
<td>Dozwolone typy pól indeksu docelowego</td>
<td>Uwagi</td>
</tr>
<tr>
<td>wartość logiczna</td>
<td>Typem Edm.Boolean, typem Edm.String</td>
<td></td>
</tr>
<tr>
<td>Liczby całkowite</td>
<td>Typem Edm.String z typem Edm.Int32, Edm.Int64,</td>
<td></td>
</tr>
<tr>
<td>Liczby zmiennoprzecinkowe</td>
<td>Edm.Double, typem Edm.String</td>
<td></td>
</tr>
<tr>
<td>Ciąg</td>
<td>Edm.String</td>
<td></td>
</tr>
<tr>
<td>Tablice typów pierwotnych typów, np. ["a", "b", "c"]</td>
<td>Collection(Edm.String)</td>
<td></td>
</tr>
<tr>
<td>Ciągi, które wyglądają dat</td>
<td>Edm.DateTimeOffset, typem Edm.String</td>
<td></td>
</tr>
<tr>
<td>Obiekty punktu GeoJSON</td>
<td>Edm.GeographyPoint</td>
<td>Punkty GeoJSON są obiektami JSON w hello następującego formatu: {"type": "Point", "coordinates": [długie, lat]} </td>
</tr>
<tr>
<td>Inne obiekty JSON</td>
<td>Nie dotyczy</td>
<td>Nieobsługiwane. Usługa Azure Search aktualnie obsługuje tylko typy pierwotne i kolekcji ciągów</td>
</tr>
</table>
