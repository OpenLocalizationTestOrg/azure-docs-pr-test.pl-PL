---
title: "Praca z zmiany źródła pomocy technicznej w usłudze Azure DB rozwiązania Cosmos | Dokumentacja firmy Microsoft"
description: "Obsługa kanału informacyjnego zmiany bazy danych Azure rozwiązania Cosmos umożliwia śledzenie zmian w dokumentach i wykonywać oparty na zdarzeniach przetwarzania, takich jak wyzwalaczy i aktualizowanie systemów pamięci podręcznych i analiza."
keywords: "Zmiana źródła danych"
services: cosmos-db
author: arramac
manager: jhubbard
editor: mimig
documentationcenter: 
ms.assetid: 2d7798db-857f-431a-b10f-3ccbc7d93b50
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: rest-api
ms.topic: article
ms.date: 08/15/2017
ms.author: arramac
ms.openlocfilehash: 160fbc98e0f3dcc7d17cbe0c7f7425811596a896
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
# <a name="working-with-the-change-feed-support-in-azure-cosmos-db"></a>Praca z zmiany źródła pomocy technicznej w usłudze Azure DB rozwiązania Cosmos
[Azure DB rozwiązania Cosmos](../cosmos-db/introduction.md) jest szybkie i elastyczne globalnie replikowane usługi bazy danych, która służy do przechowywania duże ilości danych transakcyjnych i działa z przewidywalną jednocyfrowej milisekundy opóźnienia dla operacji odczytu i zapisu. Dzięki temu odpowiednie IoT gry detaliczna, i operacyjne rejestrowania aplikacji. Typowe wzorzec projektowania w tych aplikacjach jest śledzić zmiany wprowadzone w danych bazy danych Azure rozwiązania Cosmos i zaktualizować zmaterializowanych widoków, wykonywać analizy w czasie rzeczywistym, archiwizowanie danych do magazynu chłodni i powiadomienia wyzwalane na określone zdarzenia na podstawie tych zmian. **Zmiany źródła pomocy technicznej** w usłudze Azure DB rozwiązania Cosmos umożliwia tworzenie wydajnych i skalowalne rozwiązania dla każdego z tych wzorców.

W przypadku zmiany źródła pomocy technicznej bazy danych Azure rozwiązania Cosmos zapewnia posortowaną listę dokumentów w kolekcji usługi Azure DB rozwiązania Cosmos w kolejności, w którym zostały zmodyfikowane. To źródło może służyć do nasłuchiwania zmian danych w kolekcji i wykonywać akcje, takie jak:

* Wyzwala wywołanie interfejsu API, gdy dokument zostanie wstawiony lub zmodyfikowany
* Podczas przetwarzania strumienia w czasie rzeczywistym () aktualizacji
* Synchronizowanie danych z pamięci podręcznej, aparat wyszukiwania lub magazynu danych

Zmiany w usłudze Azure DB rozwiązania Cosmos są zachowywane mogą być przetwarzane asynchronicznie i dystrybuowana do co najmniej jeden konsumentów w celu równoległego przetwarzania. Przyjrzyjmy się interfejsy API do zmiany źródła danych i jak ich używać do tworzenia skalowalnych aplikacji w czasie rzeczywistym. W tym artykule przedstawiono sposób pracy z bazy danych Azure rozwiązania Cosmos zmiany źródła danych i interfejsu API usługi DocumentDB. 

![Przy użyciu bazy danych Azure rozwiązania Cosmos zmiany źródła danych do analizy w czasie rzeczywistym zasilania i scenariuszach obliczeniowych o sterowane zdarzeniami](./media/change-feed/changefeedoverview.png)

> [!NOTE]
> Zmiana źródła danych obsługi jest tworzony tylko dla interfejsu API usługi DocumentDB w tej chwili; Interfejs API programu Graph i interfejsu API tabeli nie są obecnie obsługiwane.

## <a name="use-cases-and-scenarios"></a>Przypadki użycia i scenariusze
Zmiana źródła umożliwia wydajne przetwarzania dużych zestawów danych z dużą liczbę operacji zapisu i oferuje alternatywę do badania cały zestaw danych do identyfikacji, co się zmieniło. Na przykład można efektywnie wykonywać następujące zadania:

* Aktualizacji pamięci podręcznej, indeksu wyszukiwania lub magazynu danych z danych przechowywanych w usłudze Azure DB rozwiązania Cosmos.
* Implementuje warstw i archiwizowania danych na poziomie aplikacji, czyli przechowywać "gorących danych" w usłudze Azure DB rozwiązania Cosmos i przedawniają "zimnych danych", aby [magazyn obiektów Blob Azure](../storage/common/storage-introduction.md) lub [Azure Data Lake Store](../data-lake-store/data-lake-store-overview.md).
* Implementowanie analizach wsadowych na danych przy użyciu [Apache Hadoop](run-hadoop-with-hdinsight.md).
* Implementowanie [potoki lambda na platformie Azure](https://blogs.technet.microsoft.com/msuspartner/2016/01/27/azure-partner-community-big-data-advanced-analytics-and-lambda-architecture/) z bazy danych Azure rozwiązania Cosmos. Azure DB rozwiązania Cosmos zapewnia rozwiązanie skalowalne bazy danych, które można obsługiwać wprowadzanie i zapytań oraz implementował architektury lambda z niskim całkowitego kosztu posiadania. 
* Wykonywać zero czas przestoju migracji na inne konto bazy danych Azure rozwiązania Cosmos z różnych schemat partycjonowania.

**Potoki lambda z bazy danych rozwiązania Cosmos Azure wprowadzanie i zapytania:**

![Potok lambda wprowadzanie i zapytań na podstawie Azure DB rozwiązania Cosmos](./media/change-feed/lambda.png)

Użyj bazy danych Azure rozwiązania Cosmos do pobierania i przechowywania danych o zdarzeniach z urządzeń, czujników, infrastruktury i aplikacji, a przetwarzanie tych zdarzeń w czasie rzeczywistym za pomocą [Azure Stream Analytics](../stream-analytics/stream-analytics-documentdb-output.md), [Apache Storm](../hdinsight/hdinsight-storm-overview.md), lub [Apache Spark](../hdinsight/hdinsight-apache-spark-overview.md). 

W ramach Twojej [niekorzystającą](http://azure.com/serverless) sieci web i aplikacji mobilnych można Śledź zdarzenia, takie jak zmiany do klienta profilu, preferencje lub lokalizacji do wyzwalania określonych akcji, takich jak wysyłanie powiadomień wypychanych do urządzeń przy użyciu [ Środowisko Azure Functions](../azure-functions/functions-bindings-documentdb.md) lub [usługi aplikacji](https://azure.microsoft.com/services/app-service/). Jeśli używasz bazy danych Azure rozwiązania Cosmos do tworzenia gier, można wykonywać następujące czynności, na przykład używanie zmiany źródła danych do zaimplementowania w czasie rzeczywistym tablice wyników oparte na wyniki z gry ukończone.

## <a name="how-change-feed-works-in-azure-cosmos-db"></a>Jak działa zmiany źródła danych w usłudze Azure DB rozwiązania Cosmos
Azure DB rozwiązania Cosmos pozwala przyrostowo odczytać aktualizacje wprowadzone w kolekcji usługi Azure DB rozwiązania Cosmos. To źródło zmiany ma następujące właściwości:

* Zmiany są trwałe w usłudze Azure DB rozwiązania Cosmos i mogą być przetwarzane asynchronicznie.
* Zmiany do dokumentów w kolekcji są dostępne natychmiast w zmiany źródła danych.
* Każdej zmiany do dokumentu zostanie wyświetlone tylko raz w przypadku zmiany źródła danych, a klienci zarządzania ich logiki tworzenie punktów kontrolnych. Biblioteka źródła procesora zmianami zapewnia automatyczne tworzenie punktów kontrolnych i "co najmniej raz" semantyki.
* Tylko najnowsze zmiany w danym dokumencie znajduje się w dzienniku zmian. Pośrednie zmiany mogą nie być dostępne.
* Zmiana źródła danych jest sortowana numer modyfikacji w każdej wartości klucza partycji. Brak nie gwarantuje kolejności między wartości klucza partycji.
* Zmiany mogą być synchronizowane z dowolnego punktu w czasie, oznacza to, że istnieje nie okres przechowywania danych, dla której zmiany są dostępne.
* Zmiany są dostępne w fragmentów zakresami kluczy partycji. Ta funkcja umożliwia zmiany w dużych kolekcjach do przetworzenia równolegle przez wielu użytkowników/serwerów.
* Aplikacje mogą żądać wiele źródeł zmiany równocześnie w tej samej kolekcji.

Azure DB rozwiązania Cosmos zmiany źródła jest domyślnie włączona dla wszystkich kont. Można użyć programu [udostępnionej przepływności](request-units.md) w Twoim regionie zapisu lub w dowolnej [odczytu region](distribute-data-globally.md) odczytywać zmian źródła danych, podobnie jak inne operacje z bazy danych Azure rozwiązania Cosmos. Zmiana źródła strumieniowego obejmuje wstawienia i operacje aktualizacji do dokumentów w kolekcji. Można przechwycić usuwa przez ustawienie w dokumentach zamiast usuwa flagę "soft-delete". Alternatywnie, można ustawić okresu wygaśnięcia skończoną dla dokumentów za pomocą [możliwości TTL](time-to-live.md), na przykład, 24 godzin i użyj wartości tej właściwości, aby przechwycić usuwa. W tym rozwiązaniu ma przetwarzać zmiany w określonym czasie krótszy niż okres ważności TTL. Zmiany źródła danych jest dostępne dla każdego zakresu klucza partycji w obrębie kolekcji dokumentów i w związku z tym mogą być rozproszone na co najmniej jeden konsumentów w celu równoległego przetwarzania. 

![Przetwarzanie rozproszone zmiany bazy danych Azure rozwiązania Cosmos źródła danych](./media/change-feed/changefeedvisual.png)

Istnieje kilka opcji w sposobu implementacji zmiany źródła danych w kodzie klienta. W kolejnych sekcjach natychmiast opisano sposób wdrażania zmian źródła danych przy użyciu interfejsu API REST Azure rozwiązania Cosmos bazy danych i zestawy SDK usługi DocumentDB. Jednak dla aplikacji .NET, firma Microsoft zaleca używanie nowego [zmiany źródła danych biblioteki procesora](#change-feed-processor) do przetwarzania zdarzeń z zmiany źródła upraszcza odczytu zmiany na partycje i umożliwia wiele wątków pracy w równoległe. 

## <a id="rest-apis"></a>Praca z interfejsu API REST i zestawów SDK usługi DocumentDB
Azure DB rozwiązania Cosmos zapewnia elastyczne kontenery magazynu i przepustowości o nazwie **kolekcji**. Przy użyciu logicznie pogrupowane danych w kolekcjach [kluczy partycji](partition-data.md) na skalowalność i wydajność. Azure DB rozwiązania Cosmos udostępnia różne interfejsy API do uzyskiwania dostępu do tych danych, tym wyszukiwanie według Identyfikatora (odczyt/Get), kwerendy i odczytu źródła danych (skanowania). Zmiana źródła danych można uzyskać za wypełnianie dwa nowe nagłówki żądania do usługi DocumentDB `ReadDocumentFeed` interfejsu API i mogą być przetwarzane równolegle w zakresach kluczy partycji.

### <a name="readdocumentfeed-api"></a>ReadDocumentFeed interfejsu API
Spójrzmy krótki opis działania ReadDocumentFeed. Obsługuje bazę danych systemu Azure rozwiązania Cosmos czytania źródła dokumentów w kolekcji za pomocą `ReadDocumentFeed` interfejsu API. Na przykład następujące żądania zwraca stronę dokumenty wewnątrz `serverlogs` kolekcji. 

    GET https://mydocumentdb.documents.azure.com/dbs/smalldb/colls/serverlogs HTTP/1.1
    x-ms-date: Tue, 22 Nov 2016 17:05:14 GMT
    authorization: type%3dmaster%26ver%3d1.0%26sig%3dgo7JEogZDn6ritWhwc5hX%2fNTV4wwM1u9V2Is1H4%2bDRg%3d
    Cache-Control: no-cache
    x-ms-consistency-level: Strong
    User-Agent: Microsoft.Azure.Documents.Client/1.10.27.5
    x-ms-version: 2016-07-11
    Accept: application/json
    Host: mydocumentdb.documents.azure.com

Wyniki mogą być ograniczone za pomocą `x-ms-max-item-count` nagłówka i odczytuje można wznowić, stosując Prześlij żądanie z `x-ms-continuation` nagłówka zwracane w poprzedniej odpowiedzi. Gdy wykonywane z jednego klienta, `ReadDocumentFeed` iteruje wyników na partycje pojedynczo. 

**Seryjne odczytu dokumentu źródła danych**

Można również pobierać źródła dokumentów przy użyciu jednego z obsługiwanych [zestawów SDK DB rozwiązania Cosmos Azure](documentdb-sdk-dotnet.md). Na przykład poniższy fragment kodu przedstawia sposób użycia [metody ReadDocumentFeedAsync](/dotnet/api/microsoft.azure.documents.client.documentclient.readdocumentfeedasync?view=azure-dotnet) w .NET.

```csharp
FeedResponse<dynamic> feedResponse = null;
do
{
    feedResponse = await client.ReadDocumentFeedAsync(collection, new FeedOptions { MaxItemCount = -1 });
}
while (feedResponse.ResponseContinuation != null);
```

### <a name="distributed-execution-of-readdocumentfeed"></a>Rozproszonego wykonywania ReadDocumentFeed
Dla kolekcji, które zawierają terabajtów danych lub więcej lub pozyskiwania dużą liczbę aktualizacji serial wykonywanie odczytu źródła danych z maszyny jednego klienta może nie być praktyczne. Aby zapewnić obsługę tych scenariuszy danych big data, bazy danych rozwiązania Cosmos Azure udostępnia interfejsy API do dystrybucji `ReadDocumentFeed` wywołania niewidocznie przez wielu klientów czytników klientów. 

**Źródło dokumentu odczytu rozproszonych**

Aby zapewnić skalowalne, przetwarzanie zmiany przyrostowe bazy danych Azure rozwiązania Cosmos obsługuje skalowalnego w poziomie model zmian źródła danych na podstawie zakresów kluczy partycji interfejsu API.

* Można uzyskać listę partycji zakresami kluczy do wykonywania kolekcji `ReadPartitionKeyRanges` wywołania. 
* Dla każdego zakresu klucza partycji można wykonywać `ReadDocumentFeed` odczytać dokumenty z kluczami partycji w ramach tego zakresu.

### <a name="retrieving-partition-key-ranges-for-a-collection"></a>Pobieranie zakresów klucza partycji dla kolekcji
Zakresy klucza partycji można pobrać przez zażądanie `pkranges` zasobów w kolekcji. Na przykład następujące żądania pobiera listę zakresy klucza partycji dla `serverlogs` kolekcji:

    GET https://querydemo.documents.azure.com/dbs/bigdb/colls/serverlogs/pkranges HTTP/1.1
    x-ms-date: Tue, 15 Nov 2016 07:26:51 GMT
    authorization: type%3dmaster%26ver%3d1.0%26sig%3dEConYmRgDExu6q%2bZ8GjfUGOH0AcOx%2behkancw3LsGQ8%3d
    x-ms-consistency-level: Session
    x-ms-version: 2016-07-11
    Accept: application/json
    Host: querydemo.documents.azure.com

To żądanie zwraca następującą odpowiedź zawierający metadane o zakresach klucza partycji:

    HTTP/1.1 200 Ok
    Content-Type: application/json
    x-ms-item-count: 25
    x-ms-schemaversion: 1.1
    Date: Tue, 15 Nov 2016 07:26:51 GMT

    {
       "_rid":"qYcAAPEvJBQ=",
       "PartitionKeyRanges":[
          {
             "_rid":"qYcAAPEvJBQCAAAAAAAAUA==",
             "id":"0",
             "_etag":"\"00002800-0000-0000-0000-580ac4ea0000\"",
             "minInclusive":"",
             "maxExclusive":"05C1CFFFFFFFF8",
             "_self":"dbs\/qYcAAA==\/colls\/qYcAAPEvJBQ=\/pkranges\/qYcAAPEvJBQCAAAAAAAAUA==\/",
             "_ts":1477100776
          },
          ...
       ],
       "_count": 25
    }


**Właściwości zakresu klucza partycji**: każdego zakresem kluczy partycji zawiera właściwości metadanych w poniższej tabeli:

<table>
    <tr>
        <th>Nazwa nagłówka</th>
        <th>Opis</th>
    </tr>
    <tr>
        <td>id</td>
        <td>
            <p>Identyfikator zakresu klucza partycji. To jest stabilna i unikatowy identyfikator w ramach każdej kolekcji.</p>
            <p>Może posłużyć w poniższym wywołaniu odczytać zmiany zakresem kluczy partycji.</p>
        </td>
    </tr>
    <tr>
        <td>maxExclusive</td>
        <td>Wartość skrótu klucza partycji maksymalną zakresem kluczy partycji. Do użytku wewnętrznego.</td>
    </tr>
    <tr>
        <td>minInclusive</td>
        <td>Wartość skrótu klucza partycji minimalna zakresem kluczy partycji. Do użytku wewnętrznego.</td>
    </tr>       
</table>

Można to zrobić przy użyciu jednego z obsługiwanych [zestawów SDK DB rozwiązania Cosmos Azure](documentdb-sdk-dotnet.md). Na przykład poniższy fragment kodu przedstawia sposób pobrać zakresami kluczy partycji w .NET przy użyciu [ReadPartitionKeyRangeFeedAsync](/dotnet/api/microsoft.azure.documents.client.documentclient.readpartitionkeyrangefeedasync?view=azure-dotnet) metody.

```csharp
string pkRangesResponseContinuation = null;
List<PartitionKeyRange> partitionKeyRanges = new List<PartitionKeyRange>();

do
{
    FeedResponse<PartitionKeyRange> pkRangesResponse = await client.ReadPartitionKeyRangeFeedAsync(
        collectionUri, 
        new FeedOptions { RequestContinuation = pkRangesResponseContinuation });

    partitionKeyRanges.AddRange(pkRangesResponse);
    pkRangesResponseContinuation = pkRangesResponse.ResponseContinuation;
}
while (pkRangesResponseContinuation != null);
```

Azure DB rozwiązania Cosmos obsługuje pobierania dokumentów na zakresem kluczy partycji przez ustawienie opcjonalne `x-ms-documentdb-partitionkeyrangeid` nagłówka. 

### <a name="performing-an-incremental-readdocumentfeed"></a>Wykonywanie przyrostowych ReadDocumentFeed
ReadDocumentFeed obsługuje następujące scenariusze/zadania przetwarzania przyrostowe zmiany w kolekcjach bazy danych rozwiązania Cosmos Azure:

* Odczytywać wszystkie zmiany do dokumentów od początku, czyli tworzenia kolekcji.
* Przeczytaj wszystkie zmiany do przyszłych aktualizacji do dokumentów z bieżącej godziny lub wszelkie zmiany od czasu określonego przez użytkownika.
* Odczytywać wszystkie zmiany do dokumentów logicznej wersji kolekcji (ETag). Punkt kontrolny można użytkowników oparte na zwrócony element ETag z przyrostowych żądań odczytu źródła.

Wstawia obejmują zmiany i aktualizacje do dokumentów. Aby przechwycić usuwa, należy użyć właściwości "usuwania nietrwałego" w dokumencie, lub użyj [wbudowanych właściwości TTL](time-to-live.md) sygnalizują Oczekujące usunięcie zmian źródła danych.

W poniższej tabeli wymieniono [żądania](/rest/api/documentdb/common-documentdb-rest-request-headers.md) i [nagłówki odpowiedzi](/rest/api/documentdb/common-documentdb-rest-response-headers.md) ReadDocumentFeed operacji.

**Nagłówki żądań dla przyrostowych ReadDocumentFeed**:

<table>
    <tr>
        <th>Nazwa nagłówka</th>
        <th>Opis</th>
    </tr>
    <tr>
        <td>WIADOMOŚCI BŁYSKAWICZNYCH A</td>
        <td>Musi być ustawiona na "Przyrostowe źródła strumieniowego" lub w przeciwnym razie pominięcia</td>
    </tr>
    <tr>
        <td>If-None-Match</td>
        <td>
            <p>Brak nagłówka: zwraca wszystkie zmiany od początku (kolekcja tworzenia)</p>
            <p>"*": zwraca wszystkie nowe zmiany danych w kolekcji</p>           
            <p>&lt;Element etag&gt;: Jeśli zestaw kolekcji ETag, zwraca wszystkie zmiany wprowadzone od momentu ten znacznik logiczne</p>
        </td>
    </tr>
    <tr>    
        <td>If-Modified-Since</td> 
        <td>Format czasu RFC 1123; ignorowane, jeśli If-None-Match został określony.</td> 
    </tr> 
    <tr>
        <td>x-ms-documentdb-partitionkeyrangeid</td>
        <td>Identyfikator zakresem kluczy partycji do odczytywania danych.</td>
    </tr>
</table>

**Nagłówki odpowiedzi dla przyrostowych ReadDocumentFeed**:

<table> <tr>
        <th>Nazwa nagłówka</th>
        <th>Opis</th>
    </tr>
    <tr>
        <td>Element etag</td>
        <td>
            <p>Numer sekwencyjny logiczne (LSN) ostatniego dokumentu zwrócił w odpowiedzi.</p>
            <p>Przy ponownym przesłaniem tej wartości w If-None-Match można wznawiać ReadDocumentFeed przyrostowe.</p>
        </td>
    </tr>
</table>

Poniżej przedstawiono przykładowe żądanie, aby zwrócić wszystkie zmiany przyrostowe w kolekcji z logiczną wersji/ETag `28535` i zakresem kluczy partycji = `16`:

    GET https://mydocumentdb.documents.azure.com/dbs/bigdb/colls/bigcoll/docs HTTP/1.1
    x-ms-max-item-count: 1
    If-None-Match: "28535"
    A-IM: Incremental feed
    x-ms-documentdb-partitionkeyrangeid: 16
    x-ms-date: Tue, 22 Nov 2016 20:43:01 GMT
    authorization: type%3dmaster%26ver%3d1.0%26sig%3dzdpL2QQ8TCfiNbW%2fEcT88JHNvWeCgDA8gWeRZ%2btfN5o%3d
    x-ms-version: 2016-07-11
    Accept: application/json
    Host: mydocumentdb.documents.azure.com

Zmiany są uporządkowane według czasu w każdym wartość klucza partycji w zakresie klucza partycji. Brak nie gwarantuje kolejności między wartości klucza partycji. Jeśli istnieje więcej wyników niż można zmieścić w jednej strony, można uzyskać następnej strony wyników Prześlij żądanie z `If-None-Match` nagłówek o wartości równej `etag` z poprzedniej odpowiedzi. Jeśli wiele dokumentów zostały wstawione lub zaktualizowane transakcyjnie, w ramach procedury składowanej lub wyzwalacza, ich zostaną wszystkie zwrócone w ramach tej samej stronie odpowiedzi.

> [!NOTE]
> Z zmian w źródle danych może spowodować, że więcej elementów zwróconych na stronie, niż określa `x-ms-max-item-count` w przypadku wielu dokumentów wstawiane lub aktualizowane w ramach procedur składowanych lub wyzwalaczy. 

Podczas korzystania z zestawu .NET SDK (1.17.0), ustaw dla pola `StartTime` w `ChangeFeedOptions` do zwrócenia bezpośrednio dokumenty zmienione od czasu `StartTime` podczas wywoływania metody `CreateDocumentChangeFeedQuery`. Określając `If-Modified-Since` przy użyciu interfejsu API REST, żądanie będzie zwracać nie dokumentów samodzielnie, ale raczej token kontynuacji lub `etag` nagłówka odpowiedzi. Aby zwrócić określonego czasu token kontynuacji zmodyfikowane dokumenty `etag` następnie musi być używany w następnym żądaniu z `If-None-Match` do zwrócenia rzeczywistego dokumentów. 

Zestaw .NET SDK zawiera [CreateDocumentChangeFeedQuery](/dotnet/api/microsoft.azure.documents.client.documentclient.createdocumentchangefeedquery?view=azure-dotnet) i [ChangeFeedOptions](/dotnet/api/microsoft.azure.documents.client.changefeedoptions?view=azure-dotnet) klasy pomocy do zmiany wprowadzone do kolekcji. Poniższy fragment kodu przedstawia sposób pobrać wszystkie zmiany od początku przy użyciu zestawu .NET SDK z jednego klienta.

```csharp
private async Task<Dictionary<string, string>> GetChanges(
    DocumentClient client,
    string collection,
    Dictionary<string, string> checkpoints)
{
    string pkRangesResponseContinuation = null;
    List<PartitionKeyRange> partitionKeyRanges = new List<PartitionKeyRange>();

    do
    {
        FeedResponse<PartitionKeyRange> pkRangesResponse = await client.ReadPartitionKeyRangeFeedAsync(
            collectionUri, 
            new FeedOptions { RequestContinuation = pkRangesResponseContinuation });

        partitionKeyRanges.AddRange(pkRangesResponse);
        pkRangesResponseContinuation = pkRangesResponse.ResponseContinuation;
    }
    while (pkRangesResponseContinuation != null);

    foreach (PartitionKeyRange pkRange in partitionKeyRanges)
    {
        string continuation = null;
        checkpoints.TryGetValue(pkRange.Id, out continuation);

        IDocumentQuery<Document> query = client.CreateDocumentChangeFeedQuery(
            collection,
            new ChangeFeedOptions
            {
                PartitionKeyRangeId = pkRange.Id,
                StartFromBeginning = true,
                RequestContinuation = continuation,
                MaxItemCount = 1
            });

        while (query.HasMoreResults)
        {
            FeedResponse<DeviceReading> readChangesResponse = query.ExecuteNextAsync<DeviceReading>().Result;

            foreach (DeviceReading changedDocument in readChangesResponse)
            {
                Console.WriteLine(changedDocument.Id);
            }

            checkpoints[pkRange.Id] = readChangesResponse.ResponseContinuation;
        }
    }

    return checkpoints;
}
```
I poniższy fragment kodu przedstawia sposób przetwarzaniem zmian w w czasie rzeczywistym z bazy danych rozwiązania Cosmos Azure za pomocą zmiany źródła pomocy technicznej i poprzedniego funkcji. Pierwsze wywołanie zwraca wszystkie dokumenty w kolekcji, natomiast drugi tylko dwa dokumenty utworzone utworzonych od czasu ostatniego punktu kontrolnego.

```csharp
// Returns all documents in the collection.
Dictionary<string, string> checkpoints = await GetChanges(client, collection, new Dictionary<string, string>());

await client.CreateDocumentAsync(collection, new DeviceReading { DeviceId = "xsensr-201", MetricType = "Temperature", Unit = "Celsius", MetricValue = 1000 });
await client.CreateDocumentAsync(collection, new DeviceReading { DeviceId = "xsensr-212", MetricType = "Pressure", Unit = "psi", MetricValue = 1000 });

// Returns only the two documents created above.
checkpoints = await GetChanges(client, collection, checkpoints);
```

Można również filtrować zmiany źródła danych przy użyciu logiki po stronie klienta można selektywnie przetworzyć zdarzenia. Na przykład poniżej przedstawiono fragment kodu, który używa po stronie klienta LINQ do przetwarzania zdarzeń zmiany temperatury tylko z czujników urządzenia.

```csharp
FeedResponse<DeviceReading> readChangesResponse = query.ExecuteNextAsync<DeviceReading>().Result;

foreach (DeviceReading changedDocument in 
    readChangesResponse.AsEnumerable().Where(d => d.MetricType == "Temperature" && d.MetricValue > 1000L))
{
    // trigger an action, like call an API
}
```

## <a id="change-feed-processor"></a>Zmiana źródła procesora biblioteki
Inną opcją jest użycie [biblioteki Azure rozwiązania Cosmos DB zmienić źródła procesora](https://docs.microsoft.com/azure/cosmos-db/documentdb-sdk-dotnet-changefeed), który pomoże Ci łatwo rozpowszechniaj przetwarzania ze źródła danych w wielu klientów zmiany zdarzeń. Biblioteka jest doskonały dla tworzenia zmiany źródła czytników na platformie .NET. Niektóre przepływy pracy, które może uprościć przy użyciu biblioteki zmiany procesora źródła danych za pośrednictwem metody zawarte w innych zestawów SDK DB rozwiązania Cosmos obejmują: 

* Ściągania aktualizacji z zmiany źródła danych, gdy dane są przechowywane w wielu partycji
* Przenoszenie lub replikowanie danych z jednej kolekcji do innego
* Równoległe wykonywanie akcji wyzwalane przez aktualizacje do danych i zmiany źródła danych 

Za pomocą interfejsów API w zestawy SDK rozwiązania Cosmos zawiera dokładne dostęp do zmiany źródła aktualizacji w każdej partycji, natomiast za pomocą biblioteki zmienić źródła procesora upraszcza odczytu zmiany na partycje i wiele wątków działające równolegle. Zamiast ręcznego odczytywać zmian z każdego kontenera i zapisywać token kontynuacji dla każdej partycji procesor źródła danych zmian automatycznie zarządza odczytu zmiany na partycje przy użyciu mechanizmu dzierżawy.

Biblioteka jest dostępna jako pakietu NuGet: [Microsoft.Azure.Documents.ChangeFeedProcessor](https://www.nuget.org/packages/Microsoft.Azure.DocumentDB.ChangeFeedProcessor/) i z kodu źródłowego jako Github [próbki](https://github.com/Azure/azure-documentdb-dotnet/tree/master/samples/ChangeFeedProcessor). 

### <a name="understanding-change-feed-processor-library"></a>Opis zmiany procesora źródła danych biblioteki 

Istnieją cztery główne składniki wdrażania procesora źródła danych zmian: monitorowanych kolekcję, Kolekcja dzierżawy hosta procesora i konsumentów. 

**Kolekcja monitorowanych:** monitorowanych kolekcja jest danych, z którego jest generowany zmiany źródła danych. Żadnych instrukcji INSERT i zmiany w kolekcji monitorowane są uwzględniane w źródle danych zmiany kolekcji. 

**Kolekcja dzierżawy:** współrzędne kolekcji dzierżawy przetwarzania zmian źródła danych w wielu pracowników. Oddzielne kolekcji jest używany do przechowywania dzierżaw z jednej dzierżawy dla każdej partycji. Jest korzystne w przypadku przechowywania tej kolekcji dzierżawy na inne konto o regionowi zapisu na którym jest uruchomiona procesora źródła danych zmian. Obiekt dzierżawy zawiera następujące atrybuty: 
* Właściciel: Określa hosta, który jest właścicielem dzierżawy
* Kontynuacja: Określa położenie (token kontynuacji) w przypadku zmiany dla określonej partycji
* Znacznik czasu: Czas ostatniego dzierżawy został zaktualizowany; Sygnatura czasowa może służyć do sprawdzenia, czy dzierżawy jest uznawany za wygasły 

**Host procesora:** każdy host Określa, ile partycje do przetworzenia na podstawie liczby wystąpień hostów mają aktywne dzierżawy. 
1.  Po uruchomieniu hosta, uzyskuje dzierżawy w celu zrównoważenia obciążenia na wszystkich hostach. Hosta okresowo odnowieniu dzierżawy, więc pozostaną aktywne dzierżawy. 
2.  Punkty kontrolne hosta ostatniego token kontynuacji do dzierżawy dla każdego do odczytu. Do zapewnienia bezpieczeństwa współbieżności, host sprawdza ETag dla każdej aktualizacji dzierżawy. Obsługiwane są także inne strategie punktu kontrolnego.  
3.  Podczas zamykania systemu host zwalnia wszystkie dzierżawy, ale przechowuje informacje kontynuacji, aby go ponownie później odczytu z przechowywanych punktu kontrolnego. 

W tym momencie liczba hostów nie może być większa niż liczba partycji (dzierżawy).

**Konsumenci:** użytkowników lub pracowników, są wątki przetwarzania zmian źródła danych inicjowane przez każdego hosta. Każdy host procesora może mieć wielu klientów. Każdy odbiorca odczytuje zmiany źródła danych z partycji, który jest przypisany do powiadamia jej hosta zmian i ważność dzierżawy.

Aby jeszcze lepiej zrozumieć, jak te cztery elementy procesora źródła danych zmian współdziałać ze sobą, Przyjrzyjmy się przykład na poniższym diagramie. Kolekcja monitorowanych przechowuje dokumenty i używa "Miasto" jako klucza partycji. Widzimy niebieski partycji i tak dalej zawiera dokumenty z polem "Miasto" od "A-E". Istnieją dwa hosty, każda z dwóch konsumentów odczytu z cztery partycje równolegle. Strzałki oznaczają konsumentów czytania z określonego punktu w przypadku zmiany źródła danych. W pierwszej partycji niebieski ciemniejszego reprezentuje nieprzeczytana zmiany podczas koloru niebieskiego reprezentuje już odczytu zmiany w przypadku zmiany źródła danych. Hosty używają kolekcji dzierżawy do przechowywania wartości "kontynuacji", aby śledzić bieżącą pozycję odczytu dla każdego konsumenta. 

![Przy użyciu zmian bazy danych Azure rozwiązania Cosmos źródła danych hosta procesora](./media/change-feed/changefeedprocessornew.png)

### <a name="using-change-feed-processor-library"></a>Przy użyciu zmian źródła danych biblioteki procesora 
Poniższej sekcji opisano sposób korzystania z biblioteki procesora źródła danych zmian w kontekście replikacji zmian z kolekcji źródłowej do docelowej kolekcji. W tym miejscu kolekcji źródłowej jest kolekcją monitorowanych w procesorze źródła danych zmian. 

**Zainstaluj i zawierać pakiet NuGet procesora źródła danych zmian** 

Przed zainstalowaniem pakietu NuGet procesora zmiany źródła danych należy najpierw zainstalować: 
* Microsoft.Azure.DocumentDB, wersja 1.13.1 lub nowszy 
* Newtonsoft.Json, wersja 9.0.1 lub powyżej instalacji `Microsoft.Azure.DocumentDB.ChangeFeedProcessor` i dołączyć go jako odwołanie.

**Utwórz kolekcję monitorowanych, dzierżawy i docelowego** 

Aby można było używać biblioteki procesora zmiany źródła danych, kolekcji dzierżawy musi zostać utworzona przed uruchomieniem hostami procesora. Zaleca się ponownie, przechowywania kolekcji dzierżawy na inne konto, za pomocą zapisu obszaru bliżej na którym jest uruchomiona procesora źródła danych zmian. W tym przykładzie przepływu danych należy utworzyć przed uruchomieniem hosta procesora źródła danych zmiany kolekcji docelowej. W przykładowym kodzie nazywamy metoda pomocnika umożliwiająca tworzenie monitorowanych, dzierżawy, i kolekcji docelowej, jeśli jeszcze nie istnieje. 

> [!WARNING]
> Tworzenie kolekcji ma cenę, jak są rezerwacji przepustowości dla aplikacji do komunikowania się z bazy danych Azure rozwiązania Cosmos. Aby uzyskać więcej informacji, odwiedź stronę [stronie dotyczącej cen](https://azure.microsoft.com/pricing/details/cosmos-db/)
> 
> 

*Tworzenie hosta procesora*

`ChangeFeedProcessorHost` Klasa udostępnia środowisko wątkowo, wieloprocesowe, bezpieczne środowisko uruchomieniowe dla implementacji procesora zdarzeń, które umożliwia także tworzenie punktów kontrolnych i zarządzanie dzierżawą partycji. Aby użyć `ChangeFeedProcessorHost` klasy, można zaimplementować `IChangeFeedObserver`. Ten interfejs zawiera trzy metody:

* `OpenAsync`: Ta funkcja jest wywoływana po otwarciu źródła obserwator zmiany. Można go zmodyfikować, aby wykonywać konkretną akcję po otwarciu konsumenta/obserwatora.  
* `CloseAsync`: Ta funkcja jest wywoływana, gdy zmiana źródła obserwator jest zakończony. Można go zmodyfikować, aby wykonywać konkretną akcję po zamknięciu konsumenta/obserwatora.  
* `ProcessChangesAsync`: Ta funkcja jest wywoływana, gdy nowe zmiany w dokumencie są dostępne na zmiany źródła danych. Można go zmodyfikować, aby wykonywać konkretną akcję po każdej zmiany źródła aktualizacji.  

W naszym przykładzie mamy implementować interfejs `IChangeFeedObserver` za pośrednictwem `DocumentFeedObserver` klasy. W tym miejscu `ProcessChangesAsync` funkcji upserts (aktualizacje), za pomocą zmian źródła danych w kolekcji docelowej. W tym przykładzie jest przydatna do przenoszenia danych z jednej kolekcji do innego, aby zmienić wartość klucza partycji zestawu danych. 

*Uruchomiona hosta procesora*

Przed rozpoczęciem przetwarzania zdarzeń, zmień obie opcje źródła i zmień opcje hosta źródła strumieniowego można dostosować. 
```csharp
    // Customizable change feed option and host options 
    ChangeFeedOptions feedOptions = new ChangeFeedOptions();

    // ie customize StartFromBeginning so change feed reads from beginning
    // can customize MaxItemCount, PartitonKeyRangeId, RequestContinuation, SessionToken and StartFromBeginning
    feedOptions.StartFromBeginning = true;

    ChangeFeedHostOptions feedHostOptions = new ChangeFeedHostOptions();

    // ie. customizing lease renewal interval to 15 seconds
    // can customize LeaseRenewInterval, LeaseAcquireInterval, LeaseExpirationInterval, FeedPollDelay 
    feedHostOptions.LeaseRenewInterval = TimeSpan.FromSeconds(15);

```
Określonych pól, które można dostosowywać podsumowano w poniższych tabelach. 

**Zmień opcje źródła**:
<table>
    <tr>
        <th>Nazwa właściwości</th>
        <th>Opis</th>
    </tr>
    <tr>
        <td>MaxItemCount</td>
        <td>Pobiera lub ustawia maksymalną liczbę elementów, które mają być zwracane w operacji wyliczenia w usłudze Azure DB rozwiązania Cosmos bazy danych.</td>
    </tr>
    <tr>
        <td>PartitionKeyRangeId</td>
        <td>Pobiera lub ustawia identyfikator zakresem kluczy partycji dla bieżącego żądania w usłudze Azure DB rozwiązania Cosmos bazy danych.</td>
    </tr>
    <tr>
        <td>RequestContinuation</td>
        <td>Pobiera lub ustawia token kontynuacji żądania w usłudze Azure DB rozwiązania Cosmos bazy danych.</td>
    </tr>
        <tr>
        <td>SessionToken</td>
        <td>Pobiera lub ustawia tokenu sesji do użycia z spójność sesji w usłudze Azure DB rozwiązania Cosmos bazy danych.</td>
    </tr>
        <tr>
        <td>StartFromBeginning</td>
        <td>Pobiera lub ustawia, czy zmiany źródła danych w usłudze Azure DB rozwiązania Cosmos bazy danych powinna zaczynać się od początku (true) lub od bieżącego (false). Domyślnie rozpoczyna się od bieżącego (false).</td>
    </tr>
</table>

**Zmień opcje hosta źródła**:
<table>
    <tr>
        <th>Nazwa właściwości</th>
        <th>Typ</th>
        <th>Opis</th>
    </tr>
    <tr>
        <td>LeaseRenewInterval</td>
        <td>Zakres czasu</td>
        <td>Interwał wszystkie dzierżawy dla aktualnie utrzymywane przez wystąpienie ChangeFeedEventHost partycji.</td>
    </tr>
    <tr>
        <td>LeaseAcquireInterval</td>
        <td>Zakres czasu</td>
        <td>Odstęp czasu, aby rozpocząć wyłączyć zadanie do obliczenia, czy partycje są rozmieszczone równomiernie wystąpień znane hosta.</td>
    </tr>
    <tr>
        <td>LeaseExpirationInterval</td>
        <td>Zakres czasu</td>
        <td>Interwał, dla którego podjęto dzierżawy na dzierżawę reprezentujący partycji. Jeśli dzierżawa nie zostanie odnowiony w tym przedziale czasu, wygasł i własność partycji są przenoszone do innego wystąpienia ChangeFeedEventHost.</td>
    </tr>
    <tr>
        <td>FeedPollDelay</td>
        <td>Zakres czasu</td>
        <td>Opóźnienie między sondowania partycji dla nowych zmian na zmiany źródła, gdy wszyscy bieżący zostały opróżnione.</td>
    </tr>
    <tr>
        <td>CheckpointFrequency</td>
        <td>CheckpointFrequency</td>
        <td>Częstotliwość dzierżawy punktu kontrolnego.</td>
    </tr>
    <tr>
        <td>MinPartitionCount</td>
        <td>int</td>
        <td>Liczba partycji minimalną dla hosta.</td>
    </tr>
    <tr>
        <td>MaxPartitionCount</td>
        <td>int</td>
        <td>Maksymalna liczba partycji, który może obsługiwać hosta.</td>
    </tr>
    <tr>
        <td>DiscardExistingLeases</td>
        <td>wartość logiczna</td>
        <td>Czy na początku hosta należy usunąć wszystkie istniejące dzierżawy i host ma się rozpoczynać od zera.</td>
    </tr>
</table>


Aby rozpocząć przetwarzanie zdarzeń, Utwórz wystąpienie `ChangeFeedProcessorHost`, podając odpowiednie parametry dla kolekcji bazy danych Azure rozwiązania Cosmos. Następnie wywołaj metodę `RegisterObserverAsync` zarejestrować Twoje `IChangeFeedObserver` implementacji (DocumentFeedObserver w tym przykładzie) ze środowiskiem uruchomieniowym. W tym momencie host podejmie próbę uzyskania dzierżawy na każdym zakresem kluczy partycji w kolekcji bazy danych rozwiązania Cosmos Azure za pomocą "zachłannego" algorytmu. Te dzierżawy trwać przez dany przedział czasu, a następnie muszą być odnowione. Jak nowe węzły wystąpień procesów roboczych, w tym przypadku przejdzie w tryb online, one rezerwacje dzierżawy i wraz z upływem czasu ładowania Przenosi między węzłami jako każdy host próbuje uzyskać więcej dzierżaw. 

W przykładowym kodzie używamy klasę fabryki (DocumentFeedObserverFactory.cs) do utworzenia obserwatora i `RegistObserverFactoryAsync` zarejestrować obserwatora. 

```csharp
using (DocumentClient destClient = new DocumentClient(destCollInfo.Uri, destCollInfo.MasterKey))
    {
        DocumentFeedObserverFactory docObserverFactory = new DocumentFeedObserverFactory(destClient, destCollInfo);
        ChangeFeedEventHost host = new ChangeFeedEventHost(hostName, documentCollectionLocation, leaseCollectionLocation, feedOptions, feedHostOptions);

        await host.RegisterObserverFactoryAsync(docObserverFactory);

        Console.WriteLine("Running... Press enter to stop.");
        Console.ReadLine();

        await host.UnregisterObserversAsync();
    }
```
W miarę upływu czasu zostaje ustalona równowaga. Ta dynamiczna funkcja umożliwia Procesora na podstawie automatycznego skalowania ma zostać zastosowany do konsumentów do skalowania w górę i w dół. Jeśli zmiany są dostępne w usłudze Azure DB rozwiązania Cosmos szybkością szybciej, niż odbiorcy mogą przetworzyć, zwiększenie użycia procesora CPU przez odbiorców może służyć do powodują automatyczne skalowanie liczby wystąpień procesu roboczego.

## <a name="next-steps"></a>Następne kroki
* Spróbuj [Azure rozwiązania Cosmos DB zmiany źródła przykłady kodu w witrynie GitHub](https://github.com/Azure/azure-documentdb-dotnet/tree/master/samples/code-samples/ChangeFeed)
* Rozpoczynanie pracy kodowanie dzięki funkcjom [zestawów SDK DB rozwiązania Cosmos Azure](documentdb-sdk-dotnet.md) lub [interfejsu API REST](/rest/api/documentdb/).
