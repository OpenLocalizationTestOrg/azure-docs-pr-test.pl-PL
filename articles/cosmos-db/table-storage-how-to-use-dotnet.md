---
title: "aaaGet pracy z magazynem tabel Azure przy użyciu platformy .NET | Dokumentacja firmy Microsoft"
description: "Przechowywanie danych strukturalnych w chmurze hello przy użyciu magazynu tabel Azure, Magazyn danych NoSQL."
services: cosmos-db
documentationcenter: .net
author: mimig1
manager: jhubbard
editor: tysonn
ms.assetid: fe46d883-7bed-49dd-980e-5c71df36adb3
ms.service: cosmos-db
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 04/10/2017
ms.author: mimig
ms.openlocfilehash: a3e9a4c6f6fd5e724535b86a3f99cd4c161de6de
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-table-storage-using-net"></a>Rozpoczynanie pracy z usługą Azure Table Storage przy użyciu platformy .NET
[!INCLUDE [storage-selector-table-include](../../includes/storage-selector-table-include.md)]
[!INCLUDE [storage-table-cosmos-db-tip-include](../../includes/storage-table-cosmos-db-tip-include.md)]

Magazyn tabel Azure to usługa, która przechowuje strukturalne NoSQL przechowywania danych w chmurze hello, zapewniając kluczy/atrybutów bez schematu. Magazyn tabel nie korzysta ze schematów, dlatego jest łatwe tooadapt dane jako hello wymagają aplikacji. Uzyskiwanie dostępu do magazynu tooTable danych jest szybki i ekonomiczny dla wielu typów aplikacji i jest zwykle tańszy niż tradycyjne bazy SQL dla podobnych ilości danych.

Używając tabeli magazynu toostore elastycznych zestawów danych takich jak dane użytkownika dla aplikacji sieci web, książki adresowe, informacje o urządzeniu lub inne rodzaje metadanych, których wymaga Twoja usługa. W tabeli można przechowywać dowolną liczbę jednostek, a konto magazynu może zawierać dowolną liczbę tabel w górę toohello limitu pojemności konta magazynu hello.

### <a name="about-this-tutorial"></a>Informacje o tym samouczku
W tym samouczku przedstawiono sposób toouse hello [biblioteki klienta magazynu Azure dla platformy .NET](https://www.nuget.org/packages/WindowsAzure.Storage/) w niektórych typowych scenariuszy magazynu tabel Azure. Te scenariusze są przedstawiane za pomocą przykładów w języku C# tworzących i usuwających tabelę oraz wstawiających, aktualizujących i usuwających dane w tabeli oraz wykonujących zapytania o nie.

## <a name="prerequisites"></a>Wymagania wstępne

Użytkownik musi hello następujących toocomplete w tym samouczku pomyślnie:

* [Program Microsoft Visual Studio](https://www.visualstudio.com/downloads/)
* [Biblioteka klienta usługi Azure Storage dla programu .NET](https://www.nuget.org/packages/WindowsAzure.Storage/)
* [Menedżer konfiguracji Azure dla programu .NET](https://www.nuget.org/packages/Microsoft.WindowsAzure.ConfigurationManager/)
* [Konto usługi Azure Storage](../storage/common/storage-create-storage-account.md#create-a-storage-account)

[!INCLUDE [storage-dotnet-client-library-version-include](../../includes/storage-dotnet-client-library-version-include.md)]

### <a name="more-samples"></a>Więcej przykładów
Dodatkowe przykłady użycia usługi Table Storage znajdziesz w temacie [Getting Started with Azure Table Storage in .NET](https://azure.microsoft.com/documentation/samples/storage-table-dotnet-getting-started/) (Rozpoczynanie pracy z usługą Azure Table Storage w programie .NET). Możesz pobrać hello przykładowej aplikacji i uruchom go lub Przeglądaj hello kodu w witrynie GitHub.

[!INCLUDE [storage-table-concepts-include](../../includes/storage-table-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/storage-create-account-include.md)]

[!INCLUDE [storage-development-environment-include](../../includes/storage-development-environment-include.md)]

### <a name="add-using-directives"></a>Dodawanie dyrektyw using
Dodaj następujące hello **przy użyciu** dyrektywy toohello początku hello `Program.cs` pliku:

```csharp
using Microsoft.Azure; // Namespace for CloudConfigurationManager
using Microsoft.WindowsAzure.Storage; // Namespace for CloudStorageAccount
using Microsoft.WindowsAzure.Storage.Table; // Namespace for Table storage types
```

### <a name="parse-hello-connection-string"></a>Przeanalizować parametrów połączenia hello
[!INCLUDE [storage-cloud-configuration-manager-include](../../includes/storage-cloud-configuration-manager-include.md)]

### <a name="create-hello-table-service-client"></a>Tworzenie klienta usługi hello tabeli
Witaj [CloudTableClient] [ dotnet_CloudTableClient] klasy pozwala tooretrieve tabel i jednostek przechowywanych w magazynie tabel. Oto klienta usługi tabel hello toocreate jednym ze sposobów:

```csharp
// Create hello table client.
CloudTableClient tableClient = storageAccount.CreateCloudTableClient();
```

Teraz wszystko jest gotowe toowrite kod odczytuje i zapisuje tooTable magazynu danych.

## <a name="create-a-table"></a>Tworzenie tabeli
W tym przykładzie pokazano sposób toocreate tabeli, jeśli jeszcze nie istnieje:

```csharp
// Retrieve hello storage account from hello connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create hello table client.
CloudTableClient tableClient = storageAccount.CreateCloudTableClient();

// Retrieve a reference toohello table.
CloudTable table = tableClient.GetTableReference("people");

// Create hello table if it doesn't exist.
table.CreateIfNotExists();
```

## <a name="add-an-entity-tooa-table"></a>Dodaj tabelę tooa jednostki
Jednostki są mapowane tooC # obiektów za pomocą niestandardowej klasy pochodzącej od [TableEntity][dotnet_TableEntity]. tooadd tabeli tooa jednostki, Utwórz klasę, która definiuje właściwości hello jednostki. Witaj poniższy kod definiuje klasę jednostki, która używa imienia klienta hello jako hello klucz wiersza i nazwiska jako klucza partycji hello. Razem klucz partycji i klucz wiersza jednoznacznej identyfikacji hello tabeli. Klucze partycji jednostki z tym samym kluczem partycji mogą być przeszukiwane szybciej niż jednostki z różnymi powitalne, ale przy użyciu różnych kluczy partycji umożliwia zwiększenie skalowalności operacji równoległych. Toobe jednostek przechowywane w tabelach muszą być obsługiwane, na przykład typ pochodny typu hello [TableEntity] [ dotnet_TableEntity] klasy. Właściwości jednostki, które chcesz toostore w tabeli musi być publiczny właściwości typu hello i obsługują pobierania i ustawienie wartości. Ponadto typ jednostki *musi* ujawniać konstruktor bez parametrów.

```csharp
public class CustomerEntity : TableEntity
{
    public CustomerEntity(string lastName, string firstName)
    {
        this.PartitionKey = lastName;
        this.RowKey = firstName;
    }

    public CustomerEntity() { }

    public string Email { get; set; }

    public string PhoneNumber { get; set; }
}
```

Operacje tabeli obejmujące jednostki są wykonywane za pośrednictwem hello [CloudTable] [ dotnet_CloudTable] obiekt, który został wcześniej utworzony w sekcji "Tworzenie tabeli" hello. Witaj toobe działania wykonywane jest reprezentowana przez [TableOperation] [ dotnet_TableOperation] obiektu. Witaj Poniższy przykładowy kod przedstawia tworzenie hello hello [CloudTable] [ dotnet_CloudTable] obiektu, a następnie **CustomerEntity** obiektu. Operacja hello tooprepare, [TableOperation] [ dotnet_TableOperation] obiekt jest tworzony tooinsert powitania klienta jednostki do tabeli hello. Na koniec operacji hello jest wykonywana przez wywołanie [CloudTable][dotnet_CloudTable].[ Wykonanie][dotnet_CloudTable_Execute].

```csharp
// Retrieve hello storage account from hello connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create hello table client.
CloudTableClient tableClient = storageAccount.CreateCloudTableClient();

// Create hello CloudTable object that represents hello "people" table.
CloudTable table = tableClient.GetTableReference("people");

// Create a new customer entity.
CustomerEntity customer1 = new CustomerEntity("Harp", "Walter");
customer1.Email = "Walter@contoso.com";
customer1.PhoneNumber = "425-555-0101";

// Create hello TableOperation object that inserts hello customer entity.
TableOperation insertOperation = TableOperation.Insert(customer1);

// Execute hello insert operation.
table.Execute(insertOperation);
```

## <a name="insert-a-batch-of-entities"></a>Zbiorcze wstawianie jednostek
Możesz wstawić partię jednostek do tabeli w jednej operacji zapisu. Inne wybrane uwagi dotyczące operacji zbiorczych:

* Można wykonać aktualizacji, usuwania i wstawia w hello same z jednym operacji zbiorczej.
* Jedna operacja zbiorcza może zawierać zapasowej too100 jednostek.
* Wszystkie jednostki w jednej operacji zbiorczej muszą mieć hello tego samego klucza partycji.
* Mimo że jest możliwe tooperform zapytania w operacji zbiorczej, musi być jedyną operacją hello w partii hello.

Witaj poniższy przykład kodu tworzy dwa obiekty jednostki i dodaje zbyt[TableBatchOperation] [ dotnet_TableBatchOperation] przy użyciu hello [Wstaw] [ dotnet_TableBatchOperation_Insert] Metoda. Następnie [CloudTable][dotnet_CloudTable].[ ExecuteBatch] [ dotnet_CloudTable_ExecuteBatch] jest nazywany tooexecute hello operacji.

```csharp
// Retrieve hello storage account from hello connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create hello table client.
CloudTableClient tableClient = storageAccount.CreateCloudTableClient();

// Create hello CloudTable object that represents hello "people" table.
CloudTable table = tableClient.GetTableReference("people");

// Create hello batch operation.
TableBatchOperation batchOperation = new TableBatchOperation();

// Create a customer entity and add it toohello table.
CustomerEntity customer1 = new CustomerEntity("Smith", "Jeff");
customer1.Email = "Jeff@contoso.com";
customer1.PhoneNumber = "425-555-0104";

// Create another customer entity and add it toohello table.
CustomerEntity customer2 = new CustomerEntity("Smith", "Ben");
customer2.Email = "Ben@contoso.com";
customer2.PhoneNumber = "425-555-0102";

// Add both customer entities toohello batch insert operation.
batchOperation.Insert(customer1);
batchOperation.Insert(customer2);

// Execute hello batch operation.
table.ExecuteBatch(batchOperation);
```

## <a name="retrieve-all-entities-in-a-partition"></a>Pobieranie wszystkich jednostek w partycji
tooquery tabeli dla wszystkich jednostek w partycji, użyj [TableQuery] [ dotnet_TableQuery] obiektu. Witaj poniższy przykład kodu Określa filtr jednostek, gdzie "Smith" jest hello klucza partycji. W tym przykładzie drukowane hello pola każdej jednostki w konsoli toohello wyników zapytania hello.

```csharp
// Retrieve hello storage account from hello connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create hello table client.
CloudTableClient tableClient = storageAccount.CreateCloudTableClient();

// Create hello CloudTable object that represents hello "people" table.
CloudTable table = tableClient.GetTableReference("people");

// Construct hello query operation for all customer entities where PartitionKey="Smith".
TableQuery<CustomerEntity> query = new TableQuery<CustomerEntity>().Where(TableQuery.GenerateFilterCondition("PartitionKey", QueryComparisons.Equal, "Smith"));

// Print hello fields for each customer.
foreach (CustomerEntity entity in table.ExecuteQuery(query))
{
    Console.WriteLine("{0}, {1}\t{2}\t{3}", entity.PartitionKey, entity.RowKey,
        entity.Email, entity.PhoneNumber);
}
```

## <a name="retrieve-a-range-of-entities-in-a-partition"></a>Pobieranie zakresu jednostek w partycji
Jeśli nie chcesz tooquery wszystkich jednostek w partycji, możesz określić zakres, łącząc filtr klucza partycji hello z filtrem klucza wiersza. Witaj poniższy przykład kodu wykorzystuje dwa filtry tooget wszystkich jednostek w partycji "Smith", gdzie hello klucz wiersza (imię) rozpoczyna się od litery przed "E" w alfabecie hello, a następnie drukuje wyniki zapytania hello.

```csharp
// Retrieve hello storage account from hello connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create hello table client.
CloudTableClient tableClient = storageAccount.CreateCloudTableClient();

// Create hello CloudTable object that represents hello "people" table.
CloudTable table = tableClient.GetTableReference("people");

// Create hello table query.
TableQuery<CustomerEntity> rangeQuery = new TableQuery<CustomerEntity>().Where(
    TableQuery.CombineFilters(
        TableQuery.GenerateFilterCondition("PartitionKey", QueryComparisons.Equal, "Smith"),
        TableOperators.And,
        TableQuery.GenerateFilterCondition("RowKey", QueryComparisons.LessThan, "E")));

// Loop through hello results, displaying information about hello entity.
foreach (CustomerEntity entity in table.ExecuteQuery(rangeQuery))
{
    Console.WriteLine("{0}, {1}\t{2}\t{3}", entity.PartitionKey, entity.RowKey,
        entity.Email, entity.PhoneNumber);
}
```

## <a name="retrieve-a-single-entity"></a>Pobieranie pojedynczej jednostki
Tooretrieve kwerendy można pisać w jednej, określonej jednostki. Witaj poniższy kod używa [TableOperation] [ dotnet_TableOperation] toospecify powitania klienta "Ben Smith". Ta metoda zwraca tylko jedną jednostkę zamiast kolekcji i hello zwrócił wartość w [TableResult][dotnet_TableResult].[ Wynik] [ dotnet_TableResult_Result] jest **CustomerEntity** obiektu. Określenie kluczy partycji i wiersza w zapytaniu jest hello najszybszy sposób tooretrieve pojedyncza jednostka z usługi tabeli hello.

```csharp
// Retrieve hello storage account from hello connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create hello table client.
CloudTableClient tableClient = storageAccount.CreateCloudTableClient();

// Create hello CloudTable object that represents hello "people" table.
CloudTable table = tableClient.GetTableReference("people");

// Create a retrieve operation that takes a customer entity.
TableOperation retrieveOperation = TableOperation.Retrieve<CustomerEntity>("Smith", "Ben");

// Execute hello retrieve operation.
TableResult retrievedResult = table.Execute(retrieveOperation);

// Print hello phone number of hello result.
if (retrievedResult.Result != null)
{
    Console.WriteLine(((CustomerEntity)retrievedResult.Result).PhoneNumber);
}
else
{
    Console.WriteLine("hello phone number could not be retrieved.");
}
```

## <a name="replace-an-entity"></a>Zastępowanie jednostki
tooupdate jednostki, pobrać hello usługi tabel, zmodyfikuj obiekt jednostki hello i następnie zapisz zmiany hello ponownie toohello usługi tabel. Witaj poniższy kod zmienia numer telefonu istniejącego klienta. Zamiast wywoływać metodę [Insert][dotnet_TableOperation_Insert], ten kod używa metody [Replace][dotnet_TableOperation_Replace]. [Zastąp] [ dotnet_TableOperation_Replace] przyczyny hello toobe jednostki całkowicie zastąpiona na powitania serwera, chyba że hello jednostki na powitania serwera została zmieniona, ponieważ został on pobrany, w którym to przypadku hello operacja zakończy się niepowodzeniem. Ten błąd jest tooprevent aplikacji nieodwracalne nadpisanie zmiany wprowadzone od hello pobierania i aktualizowania przez inny składnik aplikacji. Hello prawidłowego obsługi tego błędu jest jednostki hello tooretrieve ponownie, wprowadź żądane zmiany (jeśli jest nadal ważny), a następnie wykonaj inną [Zastąp] [ dotnet_TableOperation_Replace] operacji. Witaj w następnej sekcji opisano, jak toooverride to zachowanie.

```csharp
// Retrieve hello storage account from hello connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create hello table client.
CloudTableClient tableClient = storageAccount.CreateCloudTableClient();

// Create hello CloudTable object that represents hello "people" table.
CloudTable table = tableClient.GetTableReference("people");

// Create a retrieve operation that takes a customer entity.
TableOperation retrieveOperation = TableOperation.Retrieve<CustomerEntity>("Smith", "Ben");

// Execute hello operation.
TableResult retrievedResult = table.Execute(retrieveOperation);

// Assign hello result tooa CustomerEntity object.
CustomerEntity updateEntity = (CustomerEntity)retrievedResult.Result;

if (updateEntity != null)
{
    // Change hello phone number.
    updateEntity.PhoneNumber = "425-555-0105";

    // Create hello Replace TableOperation.
    TableOperation updateOperation = TableOperation.Replace(updateEntity);

    // Execute hello operation.
    table.Execute(updateOperation);

    Console.WriteLine("Entity updated.");
}
else
{
    Console.WriteLine("Entity could not be retrieved.");
}
```

## <a name="insert-or-replace-an-entity"></a>Wstawianie lub zastępowanie jednostki
[Zastąp] [ dotnet_TableOperation_Replace] operacji zakończy się niepowodzeniem, jeśli jednostka hello została zmieniona, ponieważ został on pobrany z serwera hello. Ponadto należy pobrać jednostki hello z serwera hello najpierw aby hello [Zastąp] [ dotnet_TableOperation_Replace] toobe operacji powiodło się. Czasami jednak nie wiadomo Jeśli hello jednostka istnieje na serwerze hello i hello bieżące wartości znajdujące się w niej nie mają znaczenia. Aktualizacja powinna nadpisać je wszystkie. tooaccomplish, należy użyć [InsertOrReplace] [ dotnet_TableOperation_InsertOrReplace] operacji. Ta operacja wstawi hello jednostki, jeśli nie istnieje, lub zastąpi ją, jeśli tak jest, niezależnie od tego, kiedy dokonano hello ostatniej aktualizacji.

Jednostki klienta dla "Nowak Krzysztof" hello poniższy przykład kodu, jest tworzony i wstawione do tabeli "osoby" hello. Następnie używamy hello [InsertOrReplace] [ dotnet_TableOperation_InsertOrReplace] toosave operacji jednostki z hello tego samego klucza partycji (Nowak) i wiersz klucza serwera toohello (Krzysztof), czas, podając inną wartość hello numer telefonu Właściwość. Ponieważ używamy operacji [InsertOrReplace][dotnet_TableOperation_InsertOrReplace], wszystkie wartości właściwości tej jednostki są zastępowane. Jednak jeśli jednostki 'Krzysztof Nowak' nie istnieje w tabeli hello, jego czy wstawiono.

```csharp
// Retrieve hello storage account from hello connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create hello table client.
CloudTableClient tableClient = storageAccount.CreateCloudTableClient();

// Create hello CloudTable object that represents hello "people" table.
CloudTable table = tableClient.GetTableReference("people");

// Create a customer entity.
CustomerEntity customer3 = new CustomerEntity("Jones", "Fred");
customer3.Email = "Fred@contoso.com";
customer3.PhoneNumber = "425-555-0106";

// Create hello TableOperation object that inserts hello customer entity.
TableOperation insertOperation = TableOperation.Insert(customer3);

// Execute hello operation.
table.Execute(insertOperation);

// Create another customer entity with hello same partition key and row key.
// We've already created a 'Fred Jones' entity and saved it toothe
// 'people' table, but here we're specifying a different value for the
// PhoneNumber property.
CustomerEntity customer4 = new CustomerEntity("Jones", "Fred");
customer4.Email = "Fred@contoso.com";
customer4.PhoneNumber = "425-555-0107";

// Create hello InsertOrReplace TableOperation.
TableOperation insertOrReplaceOperation = TableOperation.InsertOrReplace(customer4);

// Execute hello operation. Because a 'Fred Jones' entity already exists in the
// 'people' table, its property values will be overwritten by those in this
// CustomerEntity. If 'Fred Jones' didn't already exist, hello entity would be
// added toohello table.
table.Execute(insertOrReplaceOperation);
```

## <a name="query-a-subset-of-entity-properties"></a>Tworzenie zapytania do podzbioru właściwości jednostki
Zapytanie tabeli może pobrać kilka właściwości jednostki zamiast wszystkich właściwości jednostki hello. Ta technika, zwana projekcją, redukuje przepustowość i może poprawiać wydajność zapytań, zwłaszcza w przypadku dużych jednostek. Zapytanie Hello w hello następującego kodu zwraca tylko hello adresy e-mail jednostek w tabeli hello. Operację tę przeprowadza się za pomocą zapytania [DynamicTableEntity][dotnet_DynamicTableEntity] lub [EntityResolver][dotnet_EntityResolver]. Dowiedz się więcej o projekcji w hello [post na blogu Introducing Upsert i projekcji zapytań][blog_post_upsert]. Projekcja nie jest obsługiwana przez emulator magazynu hello, dlatego ten kod zadziała tylko wtedy, gdy używasz konta w usłudze tabel hello.

```csharp
// Retrieve hello storage account from hello connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create hello table client.
CloudTableClient tableClient = storageAccount.CreateCloudTableClient();

// Create hello CloudTable that represents hello "people" table.
CloudTable table = tableClient.GetTableReference("people");

// Define hello query, and select only hello Email property.
TableQuery<DynamicTableEntity> projectionQuery = new TableQuery<DynamicTableEntity>().Select(new string[] { "Email" });

// Define an entity resolver toowork with hello entity after retrieval.
EntityResolver<string> resolver = (pk, rk, ts, props, etag) => props.ContainsKey("Email") ? props["Email"].StringValue : null;

foreach (string projectedEmail in table.ExecuteQuery(projectionQuery, resolver, null, null))
{
    Console.WriteLine(projectedEmail);
}
```

## <a name="delete-an-entity"></a>Usuwanie jednostki
Można z łatwością usunąć jednostkę po jej pobraniu przy użyciu hello tego samego wzorca co w przypadku aktualizowania jednostki. powitania po kod umożliwia pobranie i usunięcie jednostki klienta.

```csharp
// Retrieve hello storage account from hello connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create hello table client.
CloudTableClient tableClient = storageAccount.CreateCloudTableClient();

// Create hello CloudTable that represents hello "people" table.
CloudTable table = tableClient.GetTableReference("people");

// Create a retrieve operation that expects a customer entity.
TableOperation retrieveOperation = TableOperation.Retrieve<CustomerEntity>("Smith", "Ben");

// Execute hello operation.
TableResult retrievedResult = table.Execute(retrieveOperation);

// Assign hello result tooa CustomerEntity.
CustomerEntity deleteEntity = (CustomerEntity)retrievedResult.Result;

// Create hello Delete TableOperation.
if (deleteEntity != null)
{
    TableOperation deleteOperation = TableOperation.Delete(deleteEntity);

    // Execute hello operation.
    table.Execute(deleteOperation);

    Console.WriteLine("Entity deleted.");
}
else
{
    Console.WriteLine("Could not retrieve hello entity.");
}
```

## <a name="delete-a-table"></a>Usuwanie tabeli
Na koniec hello poniższy przykład kodu usuwa tabelę z konta magazynu. Tabela, która została usunięta będzie niedostępna toobe ponownie utworzone w danym okresie czasu po usunięciu hello.

```csharp
// Retrieve hello storage account from hello connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create hello table client.
CloudTableClient tableClient = storageAccount.CreateCloudTableClient();

// Create hello CloudTable that represents hello "people" table.
CloudTable table = tableClient.GetTableReference("people");

// Delete hello table it if exists.
table.DeleteIfExists();
```

## <a name="retrieve-entities-in-pages-asynchronously"></a>Pobieranie asynchroniczne jednostek na stronach
Jeśli odczytujesz dużą liczbę jednostek i chcesz tooprocess/wyświetlić jednostki, zgodnie z ich pobraniu, zamiast oczekiwania na ich tooreturn wszystkich, możesz pobierać jednostki za pomocą zapytania segmentowanego. Ten przykład przedstawia, jak tooreturn wyników na stronach za pomocą wzorca Async-Await hello, dzięki czemu wykonanie nie jest blokowane podczas oczekiwania dla dużych zestawów wyników tooreturn. Aby uzyskać więcej informacji na temat używania hello wzorca Async-Await w programie .NET, zobacz [programowanie asynchroniczne z Async i Await (C# i Visual Basic)](https://msdn.microsoft.com/library/hh191443.aspx).

```csharp
// Initialize a default TableQuery tooretrieve all hello entities in hello table.
TableQuery<CustomerEntity> tableQuery = new TableQuery<CustomerEntity>();

// Initialize hello continuation token toonull toostart from hello beginning of hello table.
TableContinuationToken continuationToken = null;

do
{
    // Retrieve a segment (up too1,000 entities).
    TableQuerySegment<CustomerEntity> tableQueryResult =
        await table.ExecuteQuerySegmentedAsync(tableQuery, continuationToken);

    // Assign hello new continuation token tootell hello service where to
    // continue on hello next iteration (or null if it has reached hello end).
    continuationToken = tableQueryResult.ContinuationToken;

    // Print hello number of rows retrieved.
    Console.WriteLine("Rows retrieved {0}", tableQueryResult.Results.Count);

// Loop until a null continuation token is received, indicating hello end of hello table.
} while(continuationToken != null);
```

## <a name="next-steps"></a>Następne kroki
Teraz, kiedy znasz już podstawy magazynu tabel hello, wykonaj te toolearn łącza o bardziej skomplikowanych zadaniach magazynu:

* [Eksplorator magazynu Microsoft Azure](../vs-azure-tools-storage-manage-with-storage-explorer.md) jest bezpłatna, aplikacja autonomiczny firmy Microsoft, który umożliwia toowork wizualnie z danymi usługi Azure Storage w systemie Windows, macOS i Linux.
* Więcej przykładów użycia usługi Table Storage znajdziesz w temacie [Getting Started with Azure Table Storage in .NET](https://azure.microsoft.com/documentation/samples/storage-table-dotnet-getting-started/) (Rozpoczynanie pracy z usługą Azure Table Storage w programie .NET)
* Widok hello dokumentację referencyjną usługi tabel, aby uzyskać szczegółowe informacje o dostępnych interfejsach API:
* [Dokumentacja biblioteki klienta usługi Storage dla programu .NET](http://go.microsoft.com/fwlink/?LinkID=390731&clcid=0x409)
* [Dokumentacja interfejsu API REST](http://msdn.microsoft.com/library/azure/dd179355)
* Dowiedz się, jak kod hello toosimplify pisania toowork z usługą Azure Storage za pomocą hello [Azure WebJobs SDK](../app-service-web/websites-dotnet-webjobs-sdk-get-started.md)
* Wyświetl więcej funkcji toolearn przewodników o dodatkowych opcjach przechowywania danych na platformie Azure.
* [Rozpoczynanie pracy z magazynem obiektów Blob platformy Azure przy użyciu platformy .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md) toostore danych bez struktury.
* [Połącz tooSQL bazy danych przy użyciu programu .NET (C#)](../sql-database/sql-database-develop-dotnet-simple.md) toostore relacyjnej bazie danych.

[Download and install hello Azure SDK for .NET]: /develop/net/
[Creating an Azure Project in Visual Studio]: http://msdn.microsoft.com/library/azure/ee405487.aspx

[blog_post_upsert]: http://blogs.msdn.com/b/windowsazurestorage/archive/2011/09/15/windows-azure-tables-introducing-upsert-and-query-projection.aspx

[dotnet_api_ref]: https://msdn.microsoft.com/library/azure/mt347887.aspx
[dotnet_CloudTableClient]: https://msdn.microsoft.com/library/microsoft.windowsazure.storage.table.cloudtableclient.aspx
[dotnet_CloudTable]: https://msdn.microsoft.com/library/microsoft.windowsazure.storage.table.cloudtable.aspx
[dotnet_CloudTable_Execute]: https://msdn.microsoft.com/library/microsoft.windowsazure.storage.table.cloudtable.execute.aspx
[dotnet_CloudTable_ExecuteBatch]: https://msdn.microsoft.com/library/microsoft.windowsazure.storage.table.cloudtable.executebatch.aspx
[dotnet_DynamicTableEntity]: https://msdn.microsoft.com/library/microsoft.windowsazure.storage.table.dynamictableentity.aspx
[dotnet_EntityResolver]: https://msdn.microsoft.com/library/jj733144.aspx
[dotnet_TableBatchOperation]: https://msdn.microsoft.com/library/microsoft.windowsazure.storage.table.tablebatchoperation.aspx
[dotnet_TableBatchOperation_Insert]: https://msdn.microsoft.com/library/microsoft.windowsazure.storage.table.tablebatchoperation.insert.aspx
[dotnet_TableEntity]: https://msdn.microsoft.com/library/microsoft.windowsazure.storage.table.tableentity.aspx
[dotnet_TableOperation]: https://msdn.microsoft.com/library/microsoft.windowsazure.storage.table.tableoperation.aspx
[dotnet_TableOperation_Insert]: https://msdn.microsoft.com/library/microsoft.windowsazure.storage.table.tableoperation.insert.aspx
[dotnet_TableOperation_InsertOrReplace]: https://msdn.microsoft.com/library/microsoft.windowsazure.storage.table.tableoperation.insertorreplace.aspx
[dotnet_TableOperation_Replace]: https://msdn.microsoft.com/library/microsoft.windowsazure.storage.table.tableoperation.replace.aspx
[dotnet_TableQuery]: https://msdn.microsoft.com/library/microsoft.windowsazure.storage.table.tablequery.aspx
[dotnet_TableResult]: https://msdn.microsoft.com/library/microsoft.windowsazure.storage.table.tableresult.aspx
[dotnet_TableResult_Result]: https://msdn.microsoft.com/library/microsoft.windowsazure.storage.table.tableresult.result.aspx
