---
title: "aaaWorking hello zmiana źródła pomocy technicznej w usłudze Azure DB rozwiązania Cosmos | Dokumentacja firmy Microsoft"
description: "Bazy danych use Azure rozwiązania Cosmos zmiana źródła pomocy technicznej tootrack zmiany w dokumentach i wykonywać oparty na zdarzeniach przetwarzania, takich jak wyzwalaczy i aktualizowanie systemów pamięci podręcznych i analiza."
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
ms.openlocfilehash: a4dcf4ceb476e3e08266dbcdcbee1d75e1d1eed4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="working-with-hello-change-feed-support-in-azure-cosmos-db"></a>Praca z obsługą hello zmiany kanału informacyjnego w usłudze Azure DB rozwiązania Cosmos
[Azure DB rozwiązania Cosmos](../cosmos-db/introduction.md) jest szybkie i elastyczne globalnie replikowane usługi bazy danych, która służy do przechowywania duże ilości danych transakcyjnych i działa z przewidywalną jednocyfrowej milisekundy opóźnienia dla operacji odczytu i zapisu. Dzięki temu odpowiednie IoT gry detaliczna, i operacyjne rejestrowania aplikacji. Typowe wzorzec projektowania w tych aplikacjach jest tootrack zmiany wykonane danych tooAzure rozwiązania Cosmos bazy danych i zaktualizuj zmaterializowanych widoków, wykonywanie analiz w czasie rzeczywistym, toocold danych archiwizowanie i powiadomienia wyzwalane na określone zdarzenia na podstawie tych zmian. Witaj **zmiany źródła pomocy technicznej** w usłudze Azure DB rozwiązania Cosmos pozwala toobuild wydajne i skalowalne rozwiązania dla każdego z tych wzorców.

W przypadku zmiany źródła pomocy technicznej bazy danych rozwiązania Cosmos Azure udostępnia posortowaną listę dokumentów w kolekcji bazy danych Azure rozwiązania Cosmos w kolejności hello, w którym zostały zmodyfikowane. To źródło można toolisten używane dla toodata zmiany w kolekcji hello i wykonywać akcje, takie jak:

* Wyzwalanie tooan wywołania interfejsu API, gdy dokument zostanie wstawiony lub zmodyfikowany
* Podczas przetwarzania strumienia w czasie rzeczywistym () aktualizacji
* Synchronizowanie danych z pamięci podręcznej, aparat wyszukiwania lub magazynu danych

Zmiany w usłudze Azure DB rozwiązania Cosmos są zachowywane mogą być przetwarzane asynchronicznie i dystrybuowana do co najmniej jeden konsumentów w celu równoległego przetwarzania. Przyjrzyjmy się hello interfejsów API dla źródła danych zmian i używania ich toobuild skalowalnych aplikacji w czasie rzeczywistym. W tym artykule opisano, jak toowork z bazy danych Azure rozwiązania Cosmos zmienić źródła danych i hello interfejsu API usługi DocumentDB. 

![Przy użyciu bazy danych Azure rozwiązania Cosmos zmiany źródła danych, analiz w czasie rzeczywistym toopower i scenariuszach obliczeniowych o sterowane zdarzeniami](./media/change-feed/changefeedoverview.png)

> [!NOTE]
> Zmiana źródła danych obsługi jest tworzony tylko dla hello interfejsu API usługi DocumentDB w tej chwili; Hello interfejsu API programu Graph i interfejsu API tabeli nie są obecnie obsługiwane.

## <a name="use-cases-and-scenarios"></a>Przypadki użycia i scenariusze
Zmiana źródła umożliwia wydajne przetwarzania dużych zestawów danych z dużą liczbę operacji zapisu i oferuje alternatywne tooquerying tooidentify cały zestaw danych, co się zmieniło. Na przykład można wykonywać hello wydajnie następujące zadania:

* Aktualizacji pamięci podręcznej, indeksu wyszukiwania lub magazynu danych z danych przechowywanych w usłudze Azure DB rozwiązania Cosmos.
* Implementuje warstw i archiwizowania danych na poziomie aplikacji, oznacza to, przechowywać "gorących danych" w usłudze Azure DB rozwiązania Cosmos i przedawniają "zimnych danych" zbyt[magazyn obiektów Blob Azure](../storage/common/storage-introduction.md) lub [Azure Data Lake Store](../data-lake-store/data-lake-store-overview.md).
* Implementowanie analizach wsadowych na danych przy użyciu [Apache Hadoop](run-hadoop-with-hdinsight.md).
* Implementowanie [potoki lambda na platformie Azure](https://blogs.technet.microsoft.com/msuspartner/2016/01/27/azure-partner-community-big-data-advanced-analytics-and-lambda-architecture/) z bazy danych Azure rozwiązania Cosmos. Azure DB rozwiązania Cosmos zapewnia rozwiązanie skalowalne bazy danych, które można obsługiwać wprowadzanie i zapytań oraz implementował architektury lambda z niskim całkowitego kosztu posiadania. 
* Wykonaj zero tooanother czas przestoju migracji konta bazy danych Azure rozwiązania Cosmos z różnych schemat partycjonowania.

**Potoki lambda z bazy danych rozwiązania Cosmos Azure wprowadzanie i zapytania:**

![Potok lambda wprowadzanie i zapytań na podstawie Azure DB rozwiązania Cosmos](./media/change-feed/lambda.png)

Użyj bazy danych Azure rozwiązania Cosmos tooreceive i przechowywania danych o zdarzeniach z urządzeń, czujników, infrastruktury i aplikacji oraz przetwarzania tych zdarzeń w czasie rzeczywistym za pomocą [Azure Stream Analytics](../stream-analytics/stream-analytics-documentdb-output.md), [Apache Storm](../hdinsight/hdinsight-storm-overview.md), lub [Apache Spark](../hdinsight/hdinsight-apache-spark-overview.md). 

W ramach Twojej [niekorzystającą](http://azure.com/serverless) sieci web i aplikacji mobilnych, można Śledź zdarzenia, takie jak zmiany tooyour klienta tootrigger profilu, preferencje lub lokalizacji pewne akcje, takie jak wysyłanie powiadomień tootheir urządzeń przy użyciu wypychania[Usługę azure Functions](../azure-functions/functions-bindings-documentdb.md) lub [usługi aplikacji](https://azure.microsoft.com/services/app-service/). Jeśli używasz bazy danych Azure rozwiązania Cosmos toobuild gier, na przykład można używać zmiany tooimplement źródła strumieniowego w czasie rzeczywistym tablice wyników oparte na wyniki z gry ukończone.

## <a name="how-change-feed-works-in-azure-cosmos-db"></a>Jak działa zmiany źródła danych w usłudze Azure DB rozwiązania Cosmos
Azure DB rozwiązania Cosmos zawiera hello tooincrementally możliwości odczytu tooan aktualizacji bazy danych Azure rozwiązania Cosmos kolekcji. To źródło zmiany ma hello następujące właściwości:

* Zmiany są trwałe w usłudze Azure DB rozwiązania Cosmos i mogą być przetwarzane asynchronicznie.
* Toodocuments zmiany w kolekcji są dostępne natychmiast w hello zmian w źródle strumieniowym.
* Każdy dokument tooa zmiany pojawią się dokładnie raz hello zmiany źródła i klienci zarządzania ich logiki tworzenie punktów kontrolnych. Biblioteka źródła procesora zmianami Hello zapewnia automatyczne tworzenie punktów kontrolnych i "co najmniej raz" semantyki.
* Tylko hello ostatniej zmiany w danym dokumencie znajduje się w dzienniku zmian hello. Pośrednie zmiany mogą nie być dostępne.
* źródła danych zmian Hello jest sortowana numer modyfikacji w każdej wartości klucza partycji. Brak nie gwarantuje kolejności między wartości klucza partycji.
* Zmiany mogą być synchronizowane z dowolnego punktu w czasie, oznacza to, że istnieje nie okres przechowywania danych, dla której zmiany są dostępne.
* Zmiany są dostępne w fragmentów zakresami kluczy partycji. Ta funkcja umożliwia zmiany w dużych kolekcjach toobe przetwarzane równolegle przez wielu użytkowników/serwerów.
* Aplikacje można żądanie zmiany wielu źródeł jednocześnie na powitania sam kolekcji.

Azure DB rozwiązania Cosmos zmiany źródła jest domyślnie włączona dla wszystkich kont. Można użyć programu [udostępnionej przepływności](request-units.md) w Twoim regionie zapisu lub w dowolnej [odczytu region](distribute-data-globally.md) tooread z hello zmienić źródła danych, podobnie jak inne operacje z bazy danych Azure rozwiązania Cosmos. źródła danych zmian Hello obejmuje wstawienia i operacje aktualizacji toodocuments w kolekcji hello. Można przechwycić usuwa przez ustawienie w dokumentach zamiast usuwa flagę "soft-delete". Alternatywnie, można ustawić okresu wygaśnięcia skończoną dla dokumentów za pomocą hello [możliwości TTL](time-to-live.md), na przykład, 24 godzin i użycie hello wartość tej właściwości usuwa toocapture. W tym rozwiązaniu masz tooprocess zmiany w określonym czasie krótszy niż okres ważności TTL hello. źródła danych zmian Hello jest dostępna dla każdego zakresu klucza partycji w obrębie kolekcji dokumentów hello i w związku z tym mogą być rozproszone na co najmniej jeden konsumentów w celu równoległego przetwarzania. 

![Przetwarzanie rozproszone zmiany bazy danych Azure rozwiązania Cosmos źródła danych](./media/change-feed/changefeedvisual.png)

Istnieje kilka opcji w sposobu implementacji zmiany źródła danych w kodzie klienta. Witaj sekcje, które natychmiast wykonaj opisano sposób tooimplement hello zmiany źródła danych przy użyciu interfejsu API REST Azure rozwiązania Cosmos DB hello i hello zestawów SDK usługi DocumentDB. Jednak dla aplikacji .NET, firma Microsoft zaleca używanie hello nowe [zmiany źródła danych biblioteki procesora](#change-feed-processor) przetwarzanie zdarzeń z hello zmian źródła danych, upraszcza odczytu zmiany na partycje i umożliwia wiele wątków Praca równoległe. 

## <a id="rest-apis"></a>Praca z hello interfejsu API REST i zestawy SDK usługi DocumentDB
Azure DB rozwiązania Cosmos zapewnia elastyczne kontenery magazynu i przepustowości o nazwie **kolekcji**. Przy użyciu logicznie pogrupowane danych w kolekcjach [kluczy partycji](partition-data.md) na skalowalność i wydajność. Azure DB rozwiązania Cosmos udostępnia różne interfejsy API do uzyskiwania dostępu do tych danych, tym wyszukiwanie według Identyfikatora (odczyt/Get), kwerendy i odczytu źródła danych (skanowania). Witaj zmiany źródła danych można uzyskać za wypełnianie dwa nowe toohello nagłówki żądania usługi DocumentDB `ReadDocumentFeed` interfejsu API i mogą być przetwarzane równolegle w zakresach kluczy partycji.

### <a name="readdocumentfeed-api"></a>ReadDocumentFeed interfejsu API
Spójrzmy krótki opis działania ReadDocumentFeed. Obsługuje bazę danych systemu Azure rozwiązania Cosmos czytania źródła dokumentów w kolekcji za pomocą hello `ReadDocumentFeed` interfejsu API. Na przykład hello następujące żądania zwraca stronę dokumenty wewnątrz hello `serverlogs` kolekcji. 

    GET https://mydocumentdb.documents.azure.com/dbs/smalldb/colls/serverlogs HTTP/1.1
    x-ms-date: Tue, 22 Nov 2016 17:05:14 GMT
    authorization: type%3dmaster%26ver%3d1.0%26sig%3dgo7JEogZDn6ritWhwc5hX%2fNTV4wwM1u9V2Is1H4%2bDRg%3d
    Cache-Control: no-cache
    x-ms-consistency-level: Strong
    User-Agent: Microsoft.Azure.Documents.Client/1.10.27.5
    x-ms-version: 2016-07-11
    Accept: application/json
    Host: mydocumentdb.documents.azure.com

Wyniki mogą być ograniczone za pomocą hello `x-ms-max-item-count` nagłówka i odczytuje można wznowić, stosując Prześlij żądanie hello `x-ms-continuation` nagłówka zwracane w hello poprzedniej odpowiedzi. Gdy wykonywane z jednego klienta, `ReadDocumentFeed` iteruje wyników na partycje pojedynczo. 

**Seryjne odczytu dokumentu źródła danych**

Można również pobierać kanału informacyjnego hello dokumentów przy użyciu jednego z obsługiwanych hello [zestawów SDK DB rozwiązania Cosmos Azure](documentdb-sdk-dotnet.md). Na przykład powitania po fragment kodu przedstawia sposób toouse hello [metody ReadDocumentFeedAsync](/dotnet/api/microsoft.azure.documents.client.documentclient.readdocumentfeedasync?view=azure-dotnet) w .NET.

```csharp
FeedResponse<dynamic> feedResponse = null;
do
{
    feedResponse = await client.ReadDocumentFeedAsync(collection, new FeedOptions { MaxItemCount = -1 });
}
while (feedResponse.ResponseContinuation != null);
```

### <a name="distributed-execution-of-readdocumentfeed"></a>Rozproszonego wykonywania ReadDocumentFeed
Dla kolekcji, które zawierają terabajtów danych lub więcej lub pozyskiwania dużą liczbę aktualizacji serial wykonywanie odczytu źródła danych z maszyny jednego klienta może nie być praktyczne. W kolejności toosupport tych scenariuszy danych big data rozwiązania Cosmos Azure DB udostępnia interfejsy API toodistribute `ReadDocumentFeed` wywołania niewidocznie przez wielu klientów czytników klientów. 

**Źródło dokumentu odczytu rozproszonych**

skalowalne przetwarzania tooprovide zmiany przyrostowe rozwiązania Cosmos Azure DB obsługuje model skalowalnego w poziomie dla hello zmiany źródła danych na podstawie zakresów kluczy partycji interfejsu API.

* Można uzyskać listę partycji zakresami kluczy do wykonywania kolekcji `ReadPartitionKeyRanges` wywołania. 
* Dla każdego zakresu klucza partycji można wykonywać `ReadDocumentFeed` tooread dokumentów za pomocą kluczy partycji w ramach tego zakresu.

### <a name="retrieving-partition-key-ranges-for-a-collection"></a>Pobieranie zakresów klucza partycji dla kolekcji
Możesz pobrać zakresami kluczy partycji hello żądania hello `pkranges` zasobów w kolekcji. Na przykład hello następujące żądania pobiera listę hello zakresy klucza partycji dla hello `serverlogs` kolekcji:

    GET https://querydemo.documents.azure.com/dbs/bigdb/colls/serverlogs/pkranges HTTP/1.1
    x-ms-date: Tue, 15 Nov 2016 07:26:51 GMT
    authorization: type%3dmaster%26ver%3d1.0%26sig%3dEConYmRgDExu6q%2bZ8GjfUGOH0AcOx%2behkancw3LsGQ8%3d
    x-ms-consistency-level: Session
    x-ms-version: 2016-07-11
    Accept: application/json
    Host: querydemo.documents.azure.com

To żądanie zwraca powitania po odpowiedzi zawierający metadane o zakresach klucza partycji hello:

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


**Właściwości zakresu klucza partycji**: każdego zakresem kluczy partycji zawiera właściwości metadanych hello w hello w poniższej tabeli:

<table>
    <tr>
        <th>Nazwa nagłówka</th>
        <th>Opis</th>
    </tr>
    <tr>
        <td>id</td>
        <td>
            <p>Identyfikator Hello hello zakresem kluczy partycji. To jest stabilna i unikatowy identyfikator w ramach każdej kolekcji.</p>
            <p>Musi być używane w hello następujące zmiany tooread wywołanie przez zakresem kluczy partycji.</p>
        </td>
    </tr>
    <tr>
        <td>maxExclusive</td>
        <td>Hello wartość skrótu klucza partycji maksymalną hello zakresem kluczy partycji. Do użytku wewnętrznego.</td>
    </tr>
    <tr>
        <td>minInclusive</td>
        <td>Hello wartość skrótu klucza partycji minimalna hello zakresem kluczy partycji. Do użytku wewnętrznego.</td>
    </tr>       
</table>

Można to zrobić przy użyciu jednego z obsługiwanych hello [zestawów SDK DB rozwiązania Cosmos Azure](documentdb-sdk-dotnet.md). Na przykład hello poniższy fragment kodu przedstawia sposób tooretrieve klucza partycji z zakresów w .NET przy użyciu hello [ReadPartitionKeyRangeFeedAsync](/dotnet/api/microsoft.azure.documents.client.documentclient.readpartitionkeyrangefeedasync?view=azure-dotnet) metody.

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

Azure DB rozwiązania Cosmos obsługuje pobierania dokumentów na zakresem kluczy partycji przez ustawienie opcjonalne hello `x-ms-documentdb-partitionkeyrangeid` nagłówka. 

### <a name="performing-an-incremental-readdocumentfeed"></a>Wykonywanie przyrostowych ReadDocumentFeed
ReadDocumentFeed obsługuje następujące scenariusze/zadań przetwarzania przyrostowe zmiany w kolekcjach bazy danych Azure rozwiązania Cosmos hello:

* Odczyt wszystkich zmienia toodocuments od początku hello, czyli tworzenia kolekcji.
* Odczyt wszystkich zmienia toodocuments aktualizacje toofuture bieżący czas lub wszelkie zmiany od czasu określonego przez użytkownika.
* Odczyt wszystkich zmienia toodocuments logicznej wersji hello kolekcji (ETag). Możesz punktu kontrolnego przez użytkowników oparte na powitania zwrócony element ETag z przyrostowych żądań odczytu źródła.

Witaj zmiany obejmują toodocuments INSERT i Update. Usuwa toocapture, należy użyć właściwości "usuwania nietrwałego" w dokumencie lub użyć hello [wbudowanych właściwości TTL](time-to-live.md) toosignal Oczekujące usunięcie w hello zmienić źródła danych.

Witaj następujących hello list tabeli [żądania](/rest/api/documentdb/common-documentdb-rest-request-headers.md) i [nagłówki odpowiedzi](/rest/api/documentdb/common-documentdb-rest-response-headers.md) ReadDocumentFeed operacji.

**Nagłówki żądań dla przyrostowych ReadDocumentFeed**:

<table>
    <tr>
        <th>Nazwa nagłówka</th>
        <th>Opis</th>
    </tr>
    <tr>
        <td>WIADOMOŚCI BŁYSKAWICZNYCH A</td>
        <td>Musi być ustawiona zbyt "Przyrostowe źródła danych", lub pominięta, w przeciwnym razie</td>
    </tr>
    <tr>
        <td>If-None-Match</td>
        <td>
            <p>Brak nagłówka: zwraca wszystkie zmiany z powitania od (kolekcja tworzenia)</p>
            <p>"*": zwraca wszystkie nowe toodata zmiany w kolekcji hello</p>         
            <p>&lt;Element etag&gt;: Jeśli ustawić kolekcji tooa ETag, zwraca wszystkie zmiany wprowadzone od momentu ten znacznik logiczne</p>
        </td>
    </tr>
    <tr>    
        <td>If-Modified-Since</td> 
        <td>Format czasu RFC 1123; ignorowane, jeśli If-None-Match został określony.</td> 
    </tr> 
    <tr>
        <td>x-ms-documentdb-partitionkeyrangeid</td>
        <td>Witaj identyfikator zakresem kluczy partycji do odczytywania danych.</td>
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
            <p>numer sekwencyjny logicznej Hello (LSN) ostatniego dokumentu zwracany w odpowiedzi hello.</p>
            <p>Przy ponownym przesłaniem tej wartości w If-None-Match można wznawiać ReadDocumentFeed przyrostowe.</p>
        </td>
    </tr>
</table>

Poniżej przedstawiono przykładowe żądanie tooreturn wszystkie przyrostowe zmiany w kolekcji z wersji logicznej hello/ETag `28535` i zakresem kluczy partycji = `16`:

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

Zmiany są uporządkowane według czasu w każdej wartości klucza partycji w hello zakresem kluczy partycji. Brak nie gwarantuje kolejności między wartości klucza partycji. W przypadku więcej wyników niż można zmieścić w jednej stronie można uzyskać hello następnej strony wyników Prześlij żądanie hello hello `If-None-Match` nagłówek o wartość równa toohello `etag` z hello poprzedniej odpowiedzi. Wiele dokumentów zostały wstawione lub zaktualizowane transakcyjnie, w ramach procedury składowanej lub wyzwalacza, ich zostaną wszystkie zwrócone w hello sama strona odpowiedzi.

> [!NOTE]
> Z zmian w źródle danych może spowodować, że więcej elementów zwróconych na stronie, niż określa `x-ms-max-item-count` w przypadku hello wielu dokumentów wstawiane lub aktualizowane w ramach procedur składowanych lub wyzwalaczy. 

Korzystając z hello zestawu .NET SDK (1.17.0), ustaw pole hello `StartTime` w `ChangeFeedOptions` dokumenty toodirectly zwracany zmienione od czasu `StartTime` podczas wywoływania metody `CreateDocumentChangeFeedQuery`. Określając `If-Modified-Since` przy użyciu interfejsu API REST hello, żądanie będzie zwracać nie hello dokumentów samodzielnie, ale raczej token kontynuacji hello lub `etag` hello nagłówka odpowiedzi. dokumenty hello tooreturn zmodyfikowane hello określony czas, token kontynuacji hello `etag` musi być następnie używane w następnym żądaniu hello z `If-None-Match` tooreturn hello rzeczywiste dokumentów. 

Witaj zestawu .NET SDK udostępnia hello [CreateDocumentChangeFeedQuery](/dotnet/api/microsoft.azure.documents.client.documentclient.createdocumentchangefeedquery?view=azure-dotnet) i [ChangeFeedOptions](/dotnet/api/microsoft.azure.documents.client.changefeedoptions?view=azure-dotnet) tooaccess zmiany kolekcji tooa klas pomocy. Hello poniższy fragment kodu przedstawia sposób tooretrieve wszystkie zmiany od początku hello przy użyciu hello zestawu .NET SDK z jednego klienta.

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
I hello poniższy fragment kodu przedstawia sposób tooprocess zmienia się w czasie rzeczywistym z bazy danych rozwiązania Cosmos Azure przy użyciu hello zmiany źródła pomocy technicznej i hello poprzedzających funkcji. pierwsze wywołanie Hello zwraca wszystkie dokumenty hello w kolekcji hello, natomiast hello drugi tylko hello dwa dokumenty utworzone utworzonych od czasu ostatniego punktu kontrolnego hello.

```csharp
// Returns all documents in hello collection.
Dictionary<string, string> checkpoints = await GetChanges(client, collection, new Dictionary<string, string>());

await client.CreateDocumentAsync(collection, new DeviceReading { DeviceId = "xsensr-201", MetricType = "Temperature", Unit = "Celsius", MetricValue = 1000 });
await client.CreateDocumentAsync(collection, new DeviceReading { DeviceId = "xsensr-212", MetricType = "Pressure", Unit = "psi", MetricValue = 1000 });

// Returns only hello two documents created above.
checkpoints = await GetChanges(client, collection, checkpoints);
```

Można również filtrować hello zmiany źródła przy użyciu zdarzeń procesu tooselectively logiki po stronie klienta. Na przykład poniżej przedstawiono fragment kodu, który używa tooprocess LINQ po stronie klienta, tylko zdarzenia zmian temperatury z czujników urządzenia.

```csharp
FeedResponse<DeviceReading> readChangesResponse = query.ExecuteNextAsync<DeviceReading>().Result;

foreach (DeviceReading changedDocument in 
    readChangesResponse.AsEnumerable().Where(d => d.MetricType == "Temperature" && d.MetricValue > 1000L))
{
    // trigger an action, like call an API
}
```

## <a id="change-feed-processor"></a>Zmiana źródła procesora biblioteki
Innym rozwiązaniem jest toouse hello [biblioteki Azure rozwiązania Cosmos DB zmienić źródła procesora](https://docs.microsoft.com/azure/cosmos-db/documentdb-sdk-dotnet-changefeed), który pomoże Ci łatwo rozpowszechniaj przetwarzania ze źródła danych w wielu klientów zmiany zdarzeń. Biblioteka Hello stanowi doskonałe rozwiązanie do tworzenia zmiany na platformie .NET hello źródła danych czytników. Niektóre przepływy pracy, które może uprościć przy użyciu biblioteki procesora źródła danych zmian hello za pośrednictwem metody hello zawarte w hello innych zestawów SDK DB rozwiązania Cosmos obejmują: 

* Ściągania aktualizacji z zmiany źródła danych, gdy dane są przechowywane w wielu partycji
* Przenoszenie lub replikowanie danych z jednej kolekcji tooanother
* Równoległe wykonywanie akcji wyzwalane przez toodata aktualizacji i zmian źródła danych 

Przy użyciu hello interfejsów API w hello rozwiązania Cosmos zestawów SDK zawiera toochange dokładne dostępu podawania aktualizacje w każdej partycji, natomiast przy użyciu biblioteki procesora źródła danych zmian hello upraszcza odczytu zmiany na partycje i wiele wątków działające równolegle. Zamiast ręcznego odczytywać zmian z każdego kontenera i zapisywać token kontynuacji dla każdej partycji hello procesora źródła danych zmian automatycznie zarządza odczytu zmiany na partycje przy użyciu mechanizmu dzierżawy.

Biblioteka Hello jest dostępna jako pakietu NuGet: [Microsoft.Azure.Documents.ChangeFeedProcessor](https://www.nuget.org/packages/Microsoft.Azure.DocumentDB.ChangeFeedProcessor/) i z kodu źródłowego jako Github [próbki](https://github.com/Azure/azure-documentdb-dotnet/tree/master/samples/ChangeFeedProcessor). 

### <a name="understanding-change-feed-processor-library"></a>Opis zmiany procesora źródła danych biblioteki 

Istnieją cztery główne składniki wdrażania hello zmiany źródła procesora: hello monitorowane kolekcji, kolekcji dzierżawy hello hello procesora hosta i hello konsumentów. 

**Kolekcja monitorowanych:** kolekcja hello monitorowane jest hello danych, z których hello jest generowany zmiany źródła danych. Kolekcji toohello monitorowane wstawienia i zmiany zostaną odzwierciedlone w źródło danych zmiany hello hello kolekcji. 

**Kolekcja dzierżawy:** hello współrzędne kolekcji dzierżawy przetwarzania zmian hello źródła danych w wielu pracowników. Oddzielne kolekcja jest używana toostore hello dzierżawy jednej dzierżawy dla każdej partycji. Jest korzystne toostore tej kolekcji dzierżawy na inne konto o hello zapisu region bliżej toowhere powitalne procesor źródła danych zmian jest uruchomiony. Obiekt dzierżawy zawiera hello następujące atrybuty: 
* Właściciel: Określa hello hosta, który jest właścicielem hello dzierżawy
* Kontynuacja: Określa położenie hello (token kontynuacji) w przypadku zmiany powitania dla określonej partycji
* Znacznik czasu: Czas ostatniego dzierżawy został zaktualizowany; Sygnatura czasowa Hello można toocheck używane dzierżawy hello jest uznawany za wygasły 

**Host procesora:** każdy host Określa, ile tooprocess partycji na podstawie liczby wystąpień hostów mają aktywne dzierżawy. 
1.  Po uruchomieniu hosta, uzyskuje dzierżawy toobalance hello obciążenia na wszystkich hostach. Hosta okresowo odnowieniu dzierżawy, więc pozostaną aktywne dzierżawy. 
2.  Host punkty kontrolne hello ostatniego kontynuacji tokenu tooits dzierżawy przy każdym odczycie. tooensure współbieżności bezpieczeństwa, host sprawdza hello ETag dla każdej aktualizacji dzierżawy. Obsługiwane są także inne strategie punktu kontrolnego.  
3.  Podczas zamykania systemu host zwalnia wszystkie dzierżawy, ale zachowuje hello kontynuacji informacji, aby go ponownie odczytu z punktu kontrolnego przechowywanych hello później. 

W tym momencie hello liczby hostów nie może być większa niż liczba hello partycji (dzierżawy).

**Konsumenci:** użytkowników lub pracowników, są wątków, które przeprowadzić hello zmiany źródła przetwarzania inicjowane przez każdego hosta. Każdy host procesora może mieć wielu klientów. Każdy odbiorca odczytuje hello zmiany źródła z hello partycji jest przypisany tooand powiadamia jej hosta zmian i ważność dzierżawy.

toofurther zrozumieć, jak te cztery elementy procesora źródła danych zmian ze sobą współdziałać, Przyjrzyjmy się przykładem w powitania po diagramu. Hello monitorowane kolekcji dokumentów magazynów i używa Miasto"hello" jako klucza partycji hello. Widzimy hello niebieski partycji i tak dalej zawiera dokumentów za pomocą pola "Miasto" hello "A-E". Istnieją dwa hosty, każda z dwóch konsumentów odczytu z partycji hello czterech równolegle. Witaj strzałki oznaczają konsumentów hello czytania z określonego punktu w hello zmienić źródła danych. W pierwszej partycji hello blue ciemniejszego hello reprezentuje nieprzeczytana zmiany podczas hello koloru niebieskiego reprezentuje hello już odczytywać zmian na powitania zmiany źródła. hosty Hello używają hello dzierżawy kolekcji toostore track tookeep wartość "kontynuacji" hello bieżącego odczytywania położenia w przypadku każdego konsumenta. 

![Przy użyciu hello Azure DB rozwiązania Cosmos zmiany źródła danych hosta procesora](./media/change-feed/changefeedprocessornew.png)

### <a name="using-change-feed-processor-library"></a>Przy użyciu zmian źródła danych biblioteki procesora 
powitania po sekcji wyjaśniono, jak toouse hello biblioteki procesora źródła danych zmian w kontekście hello replikację zmian z kolekcji docelowej tooa kolekcji źródłowej. W tym miejscu hello kolekcji źródłowej jest kolekcją hello monitorowane w procesorze źródła danych zmian. 

**Zainstaluj i zawierać pakiet NuGet procesora źródła danych zmian hello** 

Przed zainstalowaniem pakietu NuGet procesora zmiany źródła danych należy najpierw zainstalować: 
* Microsoft.Azure.DocumentDB, wersja 1.13.1 lub nowszy 
* Newtonsoft.Json, wersja 9.0.1 lub powyżej instalacji `Microsoft.Azure.DocumentDB.ChangeFeedProcessor` i dołączyć go jako odwołanie.

**Utwórz kolekcję monitorowanych, dzierżawy i docelowego** 

W kolejności toouse hello biblioteki procesora źródła danych zmian hello dzierżawy kolekcji musi mieć toobe utworzyć przed uruchomieniem hello procesora hostami. Zaleca się ponownie, przechowywania kolekcji dzierżawy na inne konto z zapisu region bliżej toowhere hello się, że procesor źródła danych zmian jest uruchomiony. W tym przykładzie przepływu danych potrzebujemy kolekcji docelowej hello toocreate przed uruchomieniem hello zmiany źródła procesora hosta. W hello przykładowy kod nazywamy hello toocreate metody pomocnika monitorowane, dzierżawy i kolekcji docelowej, jeśli jeszcze nie istnieje. 

> [!WARNING]
> Tworzenie kolekcji ma cenę, jak są rezerwacji przepustowości dla toocommunicate aplikacji hello Azure DB rozwiązania Cosmos. Aby uzyskać więcej informacji, odwiedź stronę hello [stronie dotyczącej cen](https://azure.microsoft.com/pricing/details/cosmos-db/)
> 
> 

*Tworzenie hosta procesora*

Witaj `ChangeFeedProcessorHost` klasa udostępnia środowisko wątkowo, wieloprocesowe, bezpieczne środowisko uruchomieniowe dla implementacji procesora zdarzeń, które umożliwia także tworzenie punktów kontrolnych i zarządzanie dzierżawą partycji. Witaj toouse `ChangeFeedProcessorHost` klasy, można zaimplementować `IChangeFeedObserver`. Ten interfejs zawiera trzy metody:

* `OpenAsync`: Ta funkcja jest wywoływana po otwarciu źródła obserwator zmiany. Po otwarciu konsumenta/obserwatora może być zmodyfikowany tooperform określonej akcji.  
* `CloseAsync`: Ta funkcja jest wywoływana, gdy zmiana źródła obserwator jest zakończony. Po zamknięciu konsumenta/obserwatora może być zmodyfikowany tooperform określonej akcji.  
* `ProcessChangesAsync`: Ta funkcja jest wywoływana, gdy nowe zmiany w dokumencie są dostępne na zmiany źródła danych. Może być zmodyfikowany tooperform określonej akcji po każdej aktualizacji zmiany źródła danych.  

W naszym przykładzie mamy implementować interfejs hello `IChangeFeedObserver` za pośrednictwem hello `DocumentFeedObserver` klasy. W tym miejscu hello `ProcessChangesAsync` funkcji upserts (aktualizacje) do kolekcji docelowej hello strumieniowe źródło dokumentu z zmiany. W tym przykładzie jest przydatna do przenoszenia danych z tooanother jednej kolekcji w kolejności toochange hello klucz partycji zestawu danych. 

*Uruchomiona hello hosta procesora*

Przed rozpoczęciem przetwarzania zdarzeń, zmień obie opcje źródła i zmień opcje hosta źródła strumieniowego można dostosować. 
```csharp
    // Customizable change feed option and host options 
    ChangeFeedOptions feedOptions = new ChangeFeedOptions();

    // ie customize StartFromBeginning so change feed reads from beginning
    // can customize MaxItemCount, PartitonKeyRangeId, RequestContinuation, SessionToken and StartFromBeginning
    feedOptions.StartFromBeginning = true;

    ChangeFeedHostOptions feedHostOptions = new ChangeFeedHostOptions();

    // ie. customizing lease renewal interval too15 seconds
    // can customize LeaseRenewInterval, LeaseAcquireInterval, LeaseExpirationInterval, FeedPollDelay 
    feedHostOptions.LeaseRenewInterval = TimeSpan.FromSeconds(15);

```
Witaj określonych pól, które można dostosowywać przedstawiono hello następujące tabele. 

**Zmień opcje źródła**:
<table>
    <tr>
        <th>Nazwa właściwości</th>
        <th>Opis</th>
    </tr>
    <tr>
        <td>MaxItemCount</td>
        <td>Pobiera lub ustawia maksymalną liczbę elementów toobe zwracane w operacji wyliczania hello w hello Azure DB rozwiązania Cosmos bazy danych usługi hello.</td>
    </tr>
    <tr>
        <td>PartitionKeyRangeId</td>
        <td>Pobiera lub ustawia identyfikator zakresem kluczy partycji powitania dla bieżącego żądania hello hello Azure DB rozwiązania Cosmos bazy danych usługi.</td>
    </tr>
    <tr>
        <td>RequestContinuation</td>
        <td>Pobiera lub ustawia token kontynuacji żądania hello hello Azure DB rozwiązania Cosmos bazy danych usługi.</td>
    </tr>
        <tr>
        <td>SessionToken</td>
        <td>Pobiera lub ustawia hello tokenu sesji do użycia z spójność sesji w hello Azure DB rozwiązania Cosmos usługi bazy danych.</td>
    </tr>
        <tr>
        <td>StartFromBeginning</td>
        <td>Pobiera lub ustawia, czy zmiany źródła danych w usłudze baza danych bazy danych Azure rozwiązania Cosmos hello powinna zaczynać się z powitania od (true) lub bieżący (false). Domyślnie rozpoczyna się od bieżącego (false).</td>
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
        <td>Interwał powitania dla wszystkich dzierżaw dla aktualnie utrzymywane przez wystąpienie ChangeFeedEventHost hello partycji.</td>
    </tr>
    <tr>
        <td>LeaseAcquireInterval</td>
        <td>Zakres czasu</td>
        <td>Witaj tookick interwał poza toocompute zadań czy partycje są równomiernie rozłożone wystąpień znane hosta.</td>
    </tr>
    <tr>
        <td>LeaseExpirationInterval</td>
        <td>Zakres czasu</td>
        <td>Interwał powitania, dla których hello dzierżawy jest wykonywana na dzierżawę reprezentujący partycji. Jeśli w tym przedziale czasu nie odnowieniu dzierżawy hello, wygasł i własność partycji hello przenosi tooanother ChangeFeedEventHost wystąpienia.</td>
    </tr>
    <tr>
        <td>FeedPollDelay</td>
        <td>Zakres czasu</td>
        <td>Witaj opóźnienia między sondowania partycji dla nowych zmian na powitania źródła danych, po opróżnione są wszystkie bieżące zmiany.</td>
    </tr>
    <tr>
        <td>CheckpointFrequency</td>
        <td>CheckpointFrequency</td>
        <td>Witaj częstotliwość toocheckpoint dzierżawy.</td>
    </tr>
    <tr>
        <td>MinPartitionCount</td>
        <td>int</td>
        <td>Liczba partycji minimalna Hello hello hosta.</td>
    </tr>
    <tr>
        <td>MaxPartitionCount</td>
        <td>int</td>
        <td>Hello maksymalną liczbę partycji hello hostów mogą zostać użyte.</td>
    </tr>
    <tr>
        <td>DiscardExistingLeases</td>
        <td>wartość logiczna</td>
        <td>Czy na powitania Uruchom hosta hello wszystkie istniejące dzierżawy, powinien zostać usunięty, a hello host należy rozpocząć od początku.</td>
    </tr>
</table>


przetwarzanie zdarzeń toostart wystąpienia `ChangeFeedProcessorHost`, podając odpowiednie parametry hello kolekcji bazy danych Azure rozwiązania Cosmos. Następnie wywołaj metodę `RegisterObserverAsync` tooregister Twojego `IChangeFeedObserver` implementacji (DocumentFeedObserver w tym przykładzie) ze środowiskiem uruchomieniowym hello. W tym momencie hello host prób tooacquire dzierżawy na każdym zakresem kluczy partycji w kolekcji bazy danych Azure rozwiązania Cosmos hello za pomocą "zachłannego" algorytmu. Te dzierżawy trwać przez dany przedział czasu, a następnie muszą być odnowione. Jak nowe węzły wystąpień procesów roboczych, w tym przypadku przejdzie w tryb online, ich rezerwacje dzierżawy i w czasie ładowania hello przewiduje między węzłami jako każdy host próby tooacquire więcej dzierżaw. 

W przykładowym kodzie hello używamy toocreate klasy (DocumentFeedObserverFactory.cs) fabryki obserwatora i hello `RegistObserverFactoryAsync` tooregister hello obserwatora. 

```csharp
using (DocumentClient destClient = new DocumentClient(destCollInfo.Uri, destCollInfo.MasterKey))
    {
        DocumentFeedObserverFactory docObserverFactory = new DocumentFeedObserverFactory(destClient, destCollInfo);
        ChangeFeedEventHost host = new ChangeFeedEventHost(hostName, documentCollectionLocation, leaseCollectionLocation, feedOptions, feedHostOptions);

        await host.RegisterObserverFactoryAsync(docObserverFactory);

        Console.WriteLine("Running... Press enter toostop.");
        Console.ReadLine();

        await host.UnregisterObserversAsync();
    }
```
W miarę upływu czasu zostaje ustalona równowaga. Ta dynamiczna funkcja umożliwia dla systemów z procesorem CPU automatyczne skalowanie tooconsumers toobe stosowane do skalowania w górę i w dół. Jeśli zmiany są dostępne w usłudze Azure DB rozwiązania Cosmos szybkością szybciej, niż odbiorcy mogą przetworzyć, hello zwiększenie użycia procesora CPU przez odbiorców może być używane toocause automatyczne skalowanie liczby wystąpień procesu roboczego.

## <a name="next-steps"></a>Następne kroki
* Spróbuj hello [Azure rozwiązania Cosmos DB zmiany źródła przykłady kodu w witrynie GitHub](https://github.com/Azure/azure-documentdb-dotnet/tree/master/samples/code-samples/ChangeFeed)
* Rozpoczynanie pracy kodowania z hello [zestawów SDK DB rozwiązania Cosmos Azure](documentdb-sdk-dotnet.md) lub hello [interfejsu API REST](/rest/api/documentdb/).
