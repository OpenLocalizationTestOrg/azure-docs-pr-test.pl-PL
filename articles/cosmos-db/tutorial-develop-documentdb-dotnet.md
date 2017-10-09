---
title: "Azure DB rozwiązania Cosmos: Opracowywania hello interfejs API .NET usługi DocumentDB | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toodevelop z interfejsem API usługi DocumentDB DB rozwiązania Cosmos Azure przy użyciu platformy .NET"
services: cosmos-db
documentationcenter: 
author: mimig1
manager: jhubbard
editor: 
tags: 
ms.assetid: 
ms.service: cosmos-db
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: 
ms.date: 05/10/2017
ms.author: mimig
ms.custom: mvc
ms.openlocfilehash: 0d3d17afa782054c8fdf3cbac421e5a5d0a6800c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmosdb-develop-with-hello-documentdb-api-in-net"></a>Azure CosmosDB: Opracowywania hello interfejsu API usługi DocumentDB w .NET

Azure Cosmos DB to rozproszona globalnie wielomodelowa usługa bazy danych firmy Microsoft. Można szybko utworzyć i wyszukiwać dokumentu, klucza i wartości i wykres baz danych, które korzystają z dystrybucji globalne hello i możliwości skalowanie w poziomie na podstawowe hello Azure DB rozwiązania Cosmos. 

Ten samouczek pokazuje, jak toocreate konta bazy danych rozwiązania Cosmos Azure przy użyciu hello portalu Azure, a następnie utwórz bazą danych dokumentów i kolekcji z [klucza partycji](documentdb-partition-data.md#partition-keys) przy użyciu hello [interfejsu API platformy .NET usługi DocumentDB](documentdb-introduction.md). Definiując klucza partycji podczas tworzenia kolekcji, aplikacja jest przygotowana tooscale wysiłku, wraz z rozwojem danych. 

Ten samouczek obejmuje hello następujące zadania za pomocą hello [interfejsu API platformy .NET usługi DocumentDB](documentdb-sdk-dotnet.md):

> [!div class="checklist"]
> * Tworzenie konta usługi Azure Cosmos DB
> * Tworzenie bazy danych i kolekcji z użyciem klucza partycji
> * Tworzenie dokumentów JSON
> * Aktualizowanie dokumentu
> * Zapytanie względem kolekcji podzielone na partycje
> * Uruchamianie procedury składowane
> * Usuwanie dokumentu
> * Usuwanie bazy danych

## <a name="prerequisites"></a>Wymagania wstępne
Upewnij się, że masz następujące hello:

* Aktywne konto platformy Azure. Jeśli go nie masz, możesz zarejestrować się w celu [utworzenia bezpłatnego konta](https://azure.microsoft.com/free/). 
    * Alternatywnie można użyć hello [Azure rozwiązania Cosmos DB emulatora](local-emulator.md) w tym samouczku, jeśli chcesz toouse środowisko lokalne, które emuluje hello usługi Azure DocumentDB do celów programistycznych.
* Program [Visual Studio](http://www.visualstudio.com/).

## <a name="create-an-azure-cosmos-db-account"></a>Tworzenie konta usługi Azure Cosmos DB

Zacznijmy od utworzenia konta Azure DB rozwiązania Cosmos w hello portalu Azure.

> [!TIP]
> * Masz już konto bazy danych rozwiązania Cosmos Azure? Jeśli tak, przejść od razu zbyt[konfigurowanie rozwiązania Visual Studio](#SetupVS)
> * Czy miał konto usługi Azure DocumentDB? Jeśli tak, Twoje konto jest kontem bazy danych Azure rozwiązania Cosmos i możesz przejść od razu zbyt[konfigurowanie rozwiązania Visual Studio](#SetupVS).  
> * Jeśli używasz hello Azure rozwiązania Cosmos DB emulatora, należy wykonać czynności hello na [Azure rozwiązania Cosmos DB emulatora](local-emulator.md) toosetup hello emulatora i przejść od razu zbyt[konfigurowanie rozwiązania Visual Studio](#SetupVS). 
>
>

[!INCLUDE [cosmos-db-create-dbaccount](../../includes/cosmos-db-create-dbaccount.md)]

## <a id="SetupVS"></a>Konfigurowanie rozwiązania programu Visual Studio
1. Otwórz program **Visual Studio** na komputerze.
2. Na powitania **pliku** menu, wybierz opcję **nowy**, a następnie wybierz pozycję **projektu**.
3. W hello **nowy projekt** okno dialogowe, wybierz opcję **szablony** / **Visual C#** / **aplikacji konsoli (.NET Framework)**, nazwy projektu, a następnie kliknij przycisk **OK**.
   ![Zrzut ekranu okna nowy projekt hello](./media/tutorial-develop-documentdb-dotnet/nosql-tutorial-new-project-2.png)

4. W hello **Eksploratora rozwiązań**, kliknij prawym przyciskiem myszy nową aplikację konsolową, która znajduje się w obrębie rozwiązania Visual Studio, a następnie kliknij przycisk **Zarządzaj pakietami NuGet...**
    
    ![Zrzut ekranu przedstawiający hello prawo kliknięto element Menu hello projektu](./media/tutorial-develop-documentdb-dotnet/nosql-tutorial-manage-nuget-pacakges.png)
5. W hello **NuGet** , kliknij pozycję **Przeglądaj**i wpisz **documentdb** hello pola wyszukiwania.
<!---stopped here--->
6. W wynikach hello znaleźć **Microsoft.Azure.DocumentDB** i kliknij przycisk **zainstalować**.
   Identyfikator pakietu Hello hello biblioteki klienta usługi Azure rozwiązania Cosmos bazy danych jest [Microsoft.Azure.DocumentDB](https://www.nuget.org/packages/Microsoft.Azure.DocumentDB).
   ![Zrzut ekranu przedstawiający hello NuGet Menu do znajdowania zestawu SDK klienta usługi Azure rozwiązania Cosmos bazy danych](./media/tutorial-develop-documentdb-dotnet/nosql-tutorial-manage-nuget-pacakges-2.png)

    Jeśli zostanie wyświetlony komunikat o przegląd zmian toohello rozwiązania, kliknij przycisk **OK**. Jeśli wyświetlany jest komunikat o akceptacji licencji, kliknij pozycję **Akceptuję**.

## <a id="Connect"></a>Dodawanie odwołań do projektu tooyour
Witaj pozostałych czynnościach w ramach tego samouczka Podaj hello interfejsu API usługi DocumentDB kodu wstawki wymaganych toocreate i aktualizacji bazy danych Azure rozwiązania Cosmos zasobów w projekcie.

Najpierw dodaj te odwołania tooyour aplikacji.
<!---These aren't added by default when you install hello pkg?--->

```csharp
using System.Net;
using Microsoft.Azure.Documents;
using Microsoft.Azure.Documents.Client;
using Newtonsoft.Json;
```

## <a id="add-references"></a>Łączenie aplikacji

Następnie dodaj te dwie stałe i *klienta* zmiennej w aplikacji.

```csharp
private const string EndpointUrl = "<your endpoint URL>";
private const string PrimaryKey = "<your primary key>";
private DocumentClient client;
```

Następnie, head ponownie toohello [portalu Azure](https://portal.azure.com) tooretrieve Twojego adresu URL punktu końcowego i klucz podstawowy. adres URL punktu końcowego Hello i klucza podstawowego są niezbędne do Twojej aplikacji toounderstand gdzie tooconnect na oraz bazy danych Azure rozwiązania Cosmos tootrust połączeniu aplikacji.

W hello portalu Azure, przejdź do konta bazy danych Azure rozwiązania Cosmos tooyour, kliknij przycisk **klucze**, a następnie kliknij przycisk **odczytu i zapisu kluczy**.

Skopiuj hello identyfikatora URI z portalu hello i wklej go za pośrednictwem `<your endpoint URL>` w pliku program.cs hello. Następnie kopiowania hello klucza podstawowego z portalu hello i wklej go za pośrednictwem `<your primary key>`. Należy się hello tooremove `<` i `>` z własnymi wartościami.

![Zrzut ekranu przedstawiający hello Azure portal używany przez toocreate samouczka NoSQL hello aplikacji konsolowej C#. Pokazuje konta bazy danych Azure rozwiązania Cosmos, z hello KLUCZE wyróżnionym w bloku konta usługi Azure DB rozwiązania Cosmos hello i hello identyfikatora URI i wartości klucza podstawowego wyróżnionym w bloku klucze hello](./media/tutorial-develop-documentdb-dotnet/nosql-tutorial-keys.png)

## <a id="instantiate"></a>Utwórz wystąpienie hello DocumentClient

Teraz, Utwórz nowe wystąpienie klasy hello **DocumentClient**.

```csharp
DocumentClient client = new DocumentClient(new Uri(endpoint), authKey);
```

## <a id="create-database"></a>Tworzenie bazy danych

Następnie należy utworzyć bazy danych Azure rozwiązania Cosmos [bazy danych](documentdb-resources.md#databases) przy użyciu hello [CreateDatabaseAsync](https://msdn.microsoft.com/library/azure/microsoft.azure.documents.client.documentclient.createdatabaseasync.aspx) metody lub [CreateDatabaseIfNotExistsAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdatabaseifnotexistsasync.aspx) metody hello  **DocumentClient** klasy z hello [zestawu SDK .NET usługi DocumentDB](documentdb-sdk-dotnet.md). Baza danych jest hello kontenerem logicznym magazynu dokumentów JSON podzielonym na partycje w kolekcjach.

```csharp
await client.CreateDatabaseAsync(new Database { Id = "db" });
```
## <a name="decide-on-a-partition-key"></a>Podejmowanie decyzji o klucza partycji 

Kolekcje są kontenerami do przechowywania dokumentów. Zasoby logiczne i można je [obejmować co najmniej jednej partycji fizycznej](partition-data.md). A [klucza partycji](documentdb-partition-data.md) jest właściwość (lub ścieżki) w dokumencie, które jest używane toodistribute danych między serwerami hello lub partycji. Wszystkie dokumenty z hello tego samego klucza partycji są przechowywane w hello tej samej partycji. 

Określania klucza partycji jest toomake bardzo ważne, aby utworzyć kolekcję. Klucze partycji są właściwości (lub ścieżki) w dokumencie, które mogą być używane przez toodistribute bazy danych Azure rozwiązania Cosmos danych między wieloma serwerami lub partycji. Rozwiązania cosmos DB skróty hello wartość klucza partycji i używa hello mieszany wynik toodetermine hello partycji w toostore hello dokumentów. Wszystkie dokumenty z hello tego samego klucza partycji są przechowywane w hello tej samej partycji, a klucze partycji nie można zmienić po utworzeniu kolekcji. 

W tym samouczku zamierzamy klucza partycji hello tooset zbyt`/deviceId` tak że hello wszystkie dane hello na jednym urządzeniu są przechowywane w jednej partycji. Ma toochoose klucza partycji, który ma wiele wartości, które są używane w o hello tooensure częstotliwości tego samego rozwiązania Cosmos DB może równoważyć obciążenie danych rozwoju lub osiągnięcia pełnej przepływności hello hello kolekcji. 

Aby uzyskać więcej informacji na temat partycjonowania, zobacz [jak toopartition i skali w usłudze Azure DB rozwiązania Cosmos?](partition-data.md) 

## <a id="CreateColl"></a>Tworzenie kolekcji 

Teraz, wiemy naszych klucza partycji `/deviceId`, umożliwia tworzenie [kolekcji](documentdb-resources.md#collections) przy użyciu hello [CreateDocumentCollectionAsync](https://msdn.microsoft.com/library/azure/microsoft.azure.documents.client.documentclient.createdocumentcollectionasync.aspx) metody lub [ CreateDocumentCollectionIfNotExistsAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdocumentcollectionifnotexistsasync.aspx) metody hello **DocumentClient** klasy. Kolekcja jest kontenerem dokumentów JSON i wszelkie skojarzonej logiki aplikacji JavaScript. 

> [!WARNING]
> Tworzenie kolekcji ma cenę, jak są rezerwacji przepustowości dla toocommunicate aplikacji hello Azure DB rozwiązania Cosmos. Aby uzyskać więcej informacji, odwiedź stronę naszych [stronie dotyczącej cen](https://azure.microsoft.com/pricing/details/cosmos-db/)
> 
> 

```csharp
// Collection for device telemetry. Here hello JSON property deviceId is used  
// as hello partition key toospread across partitions. Configured for 2500 RU/s  
// throughput and an indexing policy that supports sorting against any  
// number or string property. .
DocumentCollection myCollection = new DocumentCollection();
myCollection.Id = "coll";
myCollection.PartitionKey.Paths.Add("/deviceId");

await client.CreateDocumentCollectionAsync(
    UriFactory.CreateDatabaseUri("db"),
    myCollection,
    new RequestOptions { OfferThroughput = 2500 });
```

To sprawia, że metoda interfejsu API REST wywołać tooAzure DB rozwiązania Cosmos i hello liczba partycji na podstawie przepływności żądanego hello przepisów dotyczących usług. W razie rozwoju, przy użyciu zestawu SDK hello lub hello potrzeb wydajność można zmienić hello przepływność kolekcji [portalu Azure](set-throughput.md).

## <a id="CreateDoc"></a>Tworzenie dokumentów JSON
Teraz można wstawić niektórych dokumentów JSON do bazy danych Azure rozwiązania Cosmos. A [dokumentu](documentdb-resources.md#documents) można tworzyć przy użyciu hello [CreateDocumentAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdocumentasync.aspx) metody hello **DocumentClient** klasy. Dokumenty są zawartością JSON zdefiniowaną przez użytkownika (dowolną). Ta klasa próbki zawiera odczytu urządzenia i tooinsert tooCreateDocumentAsync wywołania nowe urządzenie odczytu do kolekcji.

```csharp
public class DeviceReading
{
    [JsonProperty("id")]
    public string Id;

    [JsonProperty("deviceId")]
    public string DeviceId;

    [JsonConverter(typeof(IsoDateTimeConverter))]
    [JsonProperty("readingTime")]
    public DateTime ReadingTime;

    [JsonProperty("metricType")]
    public string MetricType;

    [JsonProperty("unit")]
    public string Unit;

    [JsonProperty("metricValue")]
    public double MetricValue;
  }

// Create a document. Here hello partition key is extracted 
// as "XMS-0001" based on hello collection definition
await client.CreateDocumentAsync(
    UriFactory.CreateDocumentCollectionUri("db", "coll"),
    new DeviceReading
    {
        Id = "XMS-001-FE24C",
        DeviceId = "XMS-0001",
        MetricType = "Temperature",
        MetricValue = 105.00,
        Unit = "Fahrenheit",
        ReadingTime = DateTime.UtcNow
    });
```
## <a name="read-data"></a>Odczyt danych

Załóżmy odczytu dokumentu hello przez klucz partycji i identyfikator przy użyciu metody ReadDocumentAsync hello. Należy pamiętać, że odczyty hello zawierają wartość PartitionKey (odpowiedniego toohello `x-ms-documentdb-partitionkey` nagłówek żądania w hello interfejsu API REST).

```csharp
// Read document. Needs hello partition key and hello Id toobe specified
Document result = await client.ReadDocumentAsync(
  UriFactory.CreateDocumentUri("db", "coll", "XMS-001-FE24C"), 
  new RequestOptions { PartitionKey = new PartitionKey("XMS-0001") });

DeviceReading reading = (DeviceReading)(dynamic)result;
```

## <a name="update-data"></a>Aktualizowanie danych

Teraz załóżmy zaktualizować niektóre dane przy użyciu metody ReplaceDocumentAsync hello.

```csharp
// Update hello document. Partition key is not required, again extracted from hello document
reading.MetricValue = 104;
reading.ReadingTime = DateTime.UtcNow;

await client.ReplaceDocumentAsync(
  UriFactory.CreateDocumentUri("db", "coll", "XMS-001-FE24C"), 
  reading);
```

## <a name="delete-data"></a>Usuwanie danych

Umożliwia teraz usunąć przy użyciu metody DeleteDocumentAsync hello dokumentu przez klucz partycji i identyfikator.

```csharp
// Delete a document. hello partition key is required.
await client.DeleteDocumentAsync(
  UriFactory.CreateDocumentUri("db", "coll", "XMS-001-FE24C"), 
  new RequestOptions { PartitionKey = new PartitionKey("XMS-0001") });
```
## <a name="query-partitioned-collections"></a>Zapytanie względem kolekcji podzielone na partycje

Automatycznie kwerendy danych w kolekcjach podzielonym na partycje, bazy danych Azure rozwiązania Cosmos trasy hello partycji toohello zapytań odpowiadającą wartości klucza partycji toohello określony w filtrze hello (jeśli istnieją). Na przykład to zapytanie jest kierowany toojust hello partycji zawierającego hello klucza partycji "XMS 0001".

```csharp
// Query using partition key
IQueryable<DeviceReading> query = client.CreateDocumentQuery<DeviceReading>(
    UriFactory.CreateDocumentCollectionUri("db", "coll"))
    .Where(m => m.MetricType == "Temperature" && m.DeviceId == "XMS-0001");
```
    
Witaj następujące zapytanie nie ma filtr klucza partycji hello (DeviceId) i jest rozwiniętym tooall partycji, którym jest wykonywany przed hello partycjonowania indeksu. Należy pamiętać, że program toospecify hello EnableCrossPartitionQuery (`x-ms-documentdb-query-enablecrosspartition` w hello interfejsu API REST) toohave hello SDK tooexecute zapytania na partycje.

```csharp
// Query across partition keys
IQueryable<DeviceReading> crossPartitionQuery = client.CreateDocumentQuery<DeviceReading>(
    UriFactory.CreateDocumentCollectionUri("db", "coll"), 
    new FeedOptions { EnableCrossPartitionQuery = true })
    .Where(m => m.MetricType == "Temperature" && m.MetricValue > 100);
```

## <a name="parallel-query-execution"></a>Równoległego wykonywania zapytań
Hello Azure rozwiązania Cosmos bazy danych DocumentDB SDK 1.9.0 i powyżej Obsługa opcje wykonywania zapytania równoległe, umożliwiających tooperform małe opóźnienia zapytanie względem kolekcji partycjonowanych, nawet wtedy, gdy potrzebna jest tootouch dużą liczbę partycji. Na przykład hello następującego zapytania jest skonfigurowany toorun równolegle na partycje.

```csharp
// Cross-partition Order By queries
IQueryable<DeviceReading> crossPartitionQuery = client.CreateDocumentQuery<DeviceReading>(
    UriFactory.CreateDocumentCollectionUri("db", "coll"), 
    new FeedOptions { EnableCrossPartitionQuery = true, MaxDegreeOfParallelism = 10, MaxBufferedItemCount = 100})
    .Where(m => m.MetricType == "Temperature" && m.MetricValue > 100)
    .OrderBy(m => m.MetricValue);
```
    
Możesz zarządzać równoległego wykonywania zapytań przez dostrajanie hello następujące parametry:

* Przez ustawienie `MaxDegreeOfParallelism`, można kontrolować hello stopień równoległości, tj. Data hello maksymalną liczbę kolekcji sieci równoczesnych połączeń toohello partycji. Jeśli ustawisz to zbyt-1, hello stopień równoległości jest zarządzana przez hello zestawu SDK. Jeśli hello `MaxDegreeOfParallelism` nie jest określony lub ustaw too0, która jest wartością domyślną hello, będzie partycje jednej sieci połączenia toohello kolekcji.
* Przez ustawienie `MaxBufferedItemCount`, można kompromis wykorzystanie pamięci zapytania opóźnienia i po stronie klienta. Jeśli ten parametr lub ustaw tę wartość za 1 hello liczbę elementów buforowane podczas równoległego wykonywania zapytań jest zarządzana przez hello zestawu SDK.

Podane hello niezmienionym hello kolekcji, równoległe zapytania zostanie zwracają wyniki w hello kolejność takie same jak wykonanie szeregowego. Podczas wykonywania kwerendy między partycji zawierającej, sortowanie (ORDER BY i/lub góry), hello zestawu SDK usługi DocumentDB wystawia hello zapytania równolegle na partycje i scala częściowo sortowane wyniki w tooproduce po stronie klienta hello globalnie uporządkowanych wyników.

## <a name="execute-stored-procedures"></a>Wykonanie procedury składowane
Ponadto można wykonywać transakcje atomic względem dokumentów za pomocą hello tego samego Identyfikatora urządzenia, np. Jeśli jest utrzymanie agreguje lub hello najnowszy stan urządzeń w jednym dokumencie przez dodanie hello następującego projektu tooyour kodu.

```csharp
await client.ExecuteStoredProcedureAsync<DeviceReading>(
    UriFactory.CreateStoredProcedureUri("db", "coll", "SetLatestStateAcrossReadings"),
    new RequestOptions { PartitionKey = new PartitionKey("XMS-001") }, 
    "XMS-001-FE24C");
```

I to już wszystko! są to hello głównymi składnikami aplikacji bazy danych Azure rozwiązania Cosmos, która używa dystrybucji danych skali tooefficiently klucza partycji na partycje.  

## <a name="clean-up-resources"></a>Oczyszczanie zasobów

Jeśli nie ma toocontinue toouse tej aplikacji, należy usunąć wszystkie zasoby utworzone przez tego samouczka w hello portalu Azure z hello następujące kroki:

1. Z menu po lewej stronie powitania w hello portalu Azure, kliknij przycisk **grup zasobów** a następnie kliknij przycisk hello unikatową nazwę zasobu hello został utworzony. 
2. Na stronie grupy zasobów, kliknij przycisk **usunąć**, wpisz nazwę hello toodelete zasobów hello w polu tekstowym hello, a następnie kliknij **usunąć**.

## <a name="next-steps"></a>Następne kroki

W tym samouczku wykonaniu hello następujące czynności: 

> [!div class="checklist"]
> * Utworzone konto bazy danych Azure rozwiązania Cosmos
> * Utworzony z użyciem klucza partycji bazy danych i kolekcji
> * Utworzony dokumentów JSON
> * Zaktualizowano dokumentu
> * Zapytanie kolekcji partycjonowanych
> * Uruchomiono procedurę składowaną
> * Usunąć dokumentu
> * Usunięte z bazy danych

Można teraz kontynuować toohello następny samouczek i zaimportować konto bazy danych rozwiązania Cosmos tooyour dodatkowe dane. 

> [!div class="nextstepaction"]
> [Importowanie danych do usługi Azure Cosmos DB](import-data.md)
