---
title: "aaaGet pracy z magazynem tabel Azure przy użyciu platformy .NET | Dokumentacja firmy Microsoft"
description: "Przechowywanie danych strukturalnych w chmurze hello przy użyciu magazynu tabel Azure, Magazyn danych NoSQL."
services: storage
documentationcenter: .net
author: mmacy
manager: timlt
editor: tysonn
ms.assetid: fe46d883-7bed-49dd-980e-5c71df36adb3
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 04/10/2017
ms.author: marsma
ms.openlocfilehash: 9635079d61d874ff7f4bc9e7d610e0ad54b4fd6f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-table-storage-using-net"></a><span data-ttu-id="dbd31-103">Rozpoczynanie pracy z usługą Azure Table Storage przy użyciu platformy .NET</span><span class="sxs-lookup"><span data-stu-id="dbd31-103">Get started with Azure Table storage using .NET</span></span>
[!INCLUDE [storage-selector-table-include](../../includes/storage-selector-table-include.md)]
[!INCLUDE [storage-table-cosmos-db-tip-include](../../includes/storage-table-cosmos-db-tip-include.md)]

<span data-ttu-id="dbd31-104">Magazyn tabel Azure to usługa, która przechowuje strukturalne NoSQL przechowywania danych w chmurze hello, zapewniając kluczy/atrybutów bez schematu.</span><span class="sxs-lookup"><span data-stu-id="dbd31-104">Azure Table storage is a service that stores structured NoSQL data in hello cloud, providing a key/attribute store with a schemaless design.</span></span> <span data-ttu-id="dbd31-105">Magazyn tabel nie korzysta ze schematów, dlatego jest łatwe tooadapt dane jako hello wymagają aplikacji.</span><span class="sxs-lookup"><span data-stu-id="dbd31-105">Because Table storage is schemaless, it's easy tooadapt your data as hello needs of your application evolve.</span></span> <span data-ttu-id="dbd31-106">Uzyskiwanie dostępu do magazynu tooTable danych jest szybki i ekonomiczny dla wielu typów aplikacji i jest zwykle tańszy niż tradycyjne bazy SQL dla podobnych ilości danych.</span><span class="sxs-lookup"><span data-stu-id="dbd31-106">Access tooTable storage data is fast and cost-effective for many types of applications, and is typically lower in cost than traditional SQL for similar volumes of data.</span></span>

<span data-ttu-id="dbd31-107">Używając tabeli magazynu toostore elastycznych zestawów danych takich jak dane użytkownika dla aplikacji sieci web, książki adresowe, informacje o urządzeniu lub inne rodzaje metadanych, których wymaga Twoja usługa.</span><span class="sxs-lookup"><span data-stu-id="dbd31-107">You can use Table storage toostore flexible datasets like user data for web applications, address books, device information, or other types of metadata your service requires.</span></span> <span data-ttu-id="dbd31-108">W tabeli można przechowywać dowolną liczbę jednostek, a konto magazynu może zawierać dowolną liczbę tabel w górę toohello limitu pojemności konta magazynu hello.</span><span class="sxs-lookup"><span data-stu-id="dbd31-108">You can store any number of entities in a table, and a storage account may contain any number of tables, up toohello capacity limit of hello storage account.</span></span>

### <a name="about-this-tutorial"></a><span data-ttu-id="dbd31-109">Informacje o tym samouczku</span><span class="sxs-lookup"><span data-stu-id="dbd31-109">About this tutorial</span></span>
<span data-ttu-id="dbd31-110">W tym samouczku przedstawiono sposób toouse hello [biblioteki klienta magazynu Azure dla platformy .NET](https://www.nuget.org/packages/WindowsAzure.Storage/) w niektórych typowych scenariuszy magazynu tabel Azure.</span><span class="sxs-lookup"><span data-stu-id="dbd31-110">This tutorial shows you how toouse hello [Azure Storage Client Library for .NET](https://www.nuget.org/packages/WindowsAzure.Storage/) in some common Azure Table storage scenarios.</span></span> <span data-ttu-id="dbd31-111">Te scenariusze są przedstawiane za pomocą przykładów w języku C# tworzących i usuwających tabelę oraz wstawiających, aktualizujących i usuwających dane w tabeli oraz wykonujących zapytania o nie.</span><span class="sxs-lookup"><span data-stu-id="dbd31-111">These scenarios are presented using C# examples for creating and deleting a table, and inserting, updating, deleting, and querying table data.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="dbd31-112">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="dbd31-112">Prerequisites</span></span>

<span data-ttu-id="dbd31-113">Użytkownik musi hello następujących toocomplete w tym samouczku pomyślnie:</span><span class="sxs-lookup"><span data-stu-id="dbd31-113">You need hello following toocomplete this tutorial successfully:</span></span>

* [<span data-ttu-id="dbd31-114">Program Microsoft Visual Studio</span><span class="sxs-lookup"><span data-stu-id="dbd31-114">Microsoft Visual Studio</span></span>](https://www.visualstudio.com/downloads/)
* [<span data-ttu-id="dbd31-115">Biblioteka klienta usługi Azure Storage dla programu .NET</span><span class="sxs-lookup"><span data-stu-id="dbd31-115">Azure Storage Client Library for .NET</span></span>](https://www.nuget.org/packages/WindowsAzure.Storage/)
* [<span data-ttu-id="dbd31-116">Menedżer konfiguracji Azure dla programu .NET</span><span class="sxs-lookup"><span data-stu-id="dbd31-116">Azure Configuration Manager for .NET</span></span>](https://www.nuget.org/packages/Microsoft.WindowsAzure.ConfigurationManager/)
* [<span data-ttu-id="dbd31-117">Konto usługi Azure Storage</span><span class="sxs-lookup"><span data-stu-id="dbd31-117">Azure storage account</span></span>](storage-create-storage-account.md#create-a-storage-account)

[!INCLUDE [storage-dotnet-client-library-version-include](../../includes/storage-dotnet-client-library-version-include.md)]

### <a name="more-samples"></a><span data-ttu-id="dbd31-118">Więcej przykładów</span><span class="sxs-lookup"><span data-stu-id="dbd31-118">More samples</span></span>
<span data-ttu-id="dbd31-119">Dodatkowe przykłady użycia usługi Table Storage znajdziesz w temacie [Getting Started with Azure Table Storage in .NET](https://azure.microsoft.com/documentation/samples/storage-table-dotnet-getting-started/) (Rozpoczynanie pracy z usługą Azure Table Storage w programie .NET).</span><span class="sxs-lookup"><span data-stu-id="dbd31-119">For additional examples using Table storage, see [Getting Started with Azure Table Storage in .NET](https://azure.microsoft.com/documentation/samples/storage-table-dotnet-getting-started/).</span></span> <span data-ttu-id="dbd31-120">Możesz pobrać hello przykładowej aplikacji i uruchom go lub Przeglądaj hello kodu w witrynie GitHub.</span><span class="sxs-lookup"><span data-stu-id="dbd31-120">You can download hello sample application and run it, or browse hello code on GitHub.</span></span>

[!INCLUDE [storage-table-concepts-include](../../includes/storage-table-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/storage-create-account-include.md)]

[!INCLUDE [storage-development-environment-include](../../includes/storage-development-environment-include.md)]

### <a name="add-using-directives"></a><span data-ttu-id="dbd31-121">Dodawanie dyrektyw using</span><span class="sxs-lookup"><span data-stu-id="dbd31-121">Add using directives</span></span>
<span data-ttu-id="dbd31-122">Dodaj następujące hello **przy użyciu** dyrektywy toohello początku hello `Program.cs` pliku:</span><span class="sxs-lookup"><span data-stu-id="dbd31-122">Add hello following **using** directives toohello top of hello `Program.cs` file:</span></span>

```csharp
using Microsoft.Azure; // Namespace for CloudConfigurationManager
using Microsoft.WindowsAzure.Storage; // Namespace for CloudStorageAccount
using Microsoft.WindowsAzure.Storage.Table; // Namespace for Table storage types
```

### <a name="parse-hello-connection-string"></a><span data-ttu-id="dbd31-123">Przeanalizować parametrów połączenia hello</span><span class="sxs-lookup"><span data-stu-id="dbd31-123">Parse hello connection string</span></span>
[!INCLUDE [storage-cloud-configuration-manager-include](../../includes/storage-cloud-configuration-manager-include.md)]

### <a name="create-hello-table-service-client"></a><span data-ttu-id="dbd31-124">Tworzenie klienta usługi hello tabeli</span><span class="sxs-lookup"><span data-stu-id="dbd31-124">Create hello Table service client</span></span>
<span data-ttu-id="dbd31-125">Witaj [CloudTableClient] [ dotnet_CloudTableClient] klasy pozwala tooretrieve tabel i jednostek przechowywanych w magazynie tabel.</span><span class="sxs-lookup"><span data-stu-id="dbd31-125">hello [CloudTableClient][dotnet_CloudTableClient] class enables you tooretrieve tables and entities stored in Table storage.</span></span> <span data-ttu-id="dbd31-126">Oto klienta usługi tabel hello toocreate jednym ze sposobów:</span><span class="sxs-lookup"><span data-stu-id="dbd31-126">Here's one way toocreate hello Table service client:</span></span>

```csharp
// Create hello table client.
CloudTableClient tableClient = storageAccount.CreateCloudTableClient();
```

<span data-ttu-id="dbd31-127">Teraz wszystko jest gotowe toowrite kod odczytuje i zapisuje tooTable magazynu danych.</span><span class="sxs-lookup"><span data-stu-id="dbd31-127">Now you are ready toowrite code that reads data from and writes data tooTable storage.</span></span>

## <a name="create-a-table"></a><span data-ttu-id="dbd31-128">Tworzenie tabeli</span><span class="sxs-lookup"><span data-stu-id="dbd31-128">Create a table</span></span>
<span data-ttu-id="dbd31-129">W tym przykładzie pokazano sposób toocreate tabeli, jeśli jeszcze nie istnieje:</span><span class="sxs-lookup"><span data-stu-id="dbd31-129">This example shows how toocreate a table if it does not already exist:</span></span>

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

## <a name="add-an-entity-tooa-table"></a><span data-ttu-id="dbd31-130">Dodaj tabelę tooa jednostki</span><span class="sxs-lookup"><span data-stu-id="dbd31-130">Add an entity tooa table</span></span>
<span data-ttu-id="dbd31-131">Jednostki są mapowane tooC # obiektów za pomocą niestandardowej klasy pochodzącej od [TableEntity][dotnet_TableEntity].</span><span class="sxs-lookup"><span data-stu-id="dbd31-131">Entities map tooC# objects by using a custom class derived from [TableEntity][dotnet_TableEntity].</span></span> <span data-ttu-id="dbd31-132">tooadd tabeli tooa jednostki, Utwórz klasę, która definiuje właściwości hello jednostki.</span><span class="sxs-lookup"><span data-stu-id="dbd31-132">tooadd an entity tooa table, create a class that defines hello properties of your entity.</span></span> <span data-ttu-id="dbd31-133">Witaj poniższy kod definiuje klasę jednostki, która używa imienia klienta hello jako hello klucz wiersza i nazwiska jako klucza partycji hello.</span><span class="sxs-lookup"><span data-stu-id="dbd31-133">hello following code defines an entity class that uses hello customer's first name as hello row key and last name as hello partition key.</span></span> <span data-ttu-id="dbd31-134">Razem klucz partycji i klucz wiersza jednoznacznej identyfikacji hello tabeli.</span><span class="sxs-lookup"><span data-stu-id="dbd31-134">Together, an entity's partition and row key uniquely identify it in hello table.</span></span> <span data-ttu-id="dbd31-135">Klucze partycji jednostki z tym samym kluczem partycji mogą być przeszukiwane szybciej niż jednostki z różnymi powitalne, ale przy użyciu różnych kluczy partycji umożliwia zwiększenie skalowalności operacji równoległych.</span><span class="sxs-lookup"><span data-stu-id="dbd31-135">Entities with hello same partition key can be queried faster than entities with different partition keys, but using diverse partition keys allows for greater scalability of parallel operations.</span></span> <span data-ttu-id="dbd31-136">Toobe jednostek przechowywane w tabelach muszą być obsługiwane, na przykład typ pochodny typu hello [TableEntity] [ dotnet_TableEntity] klasy.</span><span class="sxs-lookup"><span data-stu-id="dbd31-136">Entities toobe stored in tables must be of a supported type, for example derived from hello [TableEntity][dotnet_TableEntity] class.</span></span> <span data-ttu-id="dbd31-137">Właściwości jednostki, które chcesz toostore w tabeli musi być publiczny właściwości typu hello i obsługują pobierania i ustawienie wartości.</span><span class="sxs-lookup"><span data-stu-id="dbd31-137">Entity properties you'd like toostore in a table must be public properties of hello type, and support both getting and setting of values.</span></span> <span data-ttu-id="dbd31-138">Ponadto typ jednostki *musi* ujawniać konstruktor bez parametrów.</span><span class="sxs-lookup"><span data-stu-id="dbd31-138">Also, your entity type *must* expose a parameter-less constructor.</span></span>

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

<span data-ttu-id="dbd31-139">Operacje tabeli obejmujące jednostki są wykonywane za pośrednictwem hello [CloudTable] [ dotnet_CloudTable] obiekt, który został wcześniej utworzony w sekcji "Tworzenie tabeli" hello.</span><span class="sxs-lookup"><span data-stu-id="dbd31-139">Table operations that involve entities are performed via hello [CloudTable][dotnet_CloudTable] object that you created earlier in hello "Create a table" section.</span></span> <span data-ttu-id="dbd31-140">Witaj toobe działania wykonywane jest reprezentowana przez [TableOperation] [ dotnet_TableOperation] obiektu.</span><span class="sxs-lookup"><span data-stu-id="dbd31-140">hello operation toobe performed is represented by a [TableOperation][dotnet_TableOperation] object.</span></span> <span data-ttu-id="dbd31-141">Witaj Poniższy przykładowy kod przedstawia tworzenie hello hello [CloudTable] [ dotnet_CloudTable] obiektu, a następnie **CustomerEntity** obiektu.</span><span class="sxs-lookup"><span data-stu-id="dbd31-141">hello following code example shows hello creation of hello [CloudTable][dotnet_CloudTable] object and then a **CustomerEntity** object.</span></span> <span data-ttu-id="dbd31-142">Operacja hello tooprepare, [TableOperation] [ dotnet_TableOperation] obiekt jest tworzony tooinsert powitania klienta jednostki do tabeli hello.</span><span class="sxs-lookup"><span data-stu-id="dbd31-142">tooprepare hello operation, a [TableOperation][dotnet_TableOperation] object is created tooinsert hello customer entity into hello table.</span></span> <span data-ttu-id="dbd31-143">Na koniec operacji hello jest wykonywana przez wywołanie [CloudTable][dotnet_CloudTable].[ Wykonanie][dotnet_CloudTable_Execute].</span><span class="sxs-lookup"><span data-stu-id="dbd31-143">Finally, hello operation is executed by calling [CloudTable][dotnet_CloudTable].[Execute][dotnet_CloudTable_Execute].</span></span>

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

## <a name="insert-a-batch-of-entities"></a><span data-ttu-id="dbd31-144">Zbiorcze wstawianie jednostek</span><span class="sxs-lookup"><span data-stu-id="dbd31-144">Insert a batch of entities</span></span>
<span data-ttu-id="dbd31-145">Możesz wstawić partię jednostek do tabeli w jednej operacji zapisu.</span><span class="sxs-lookup"><span data-stu-id="dbd31-145">You can insert a batch of entities into a table in one write operation.</span></span> <span data-ttu-id="dbd31-146">Inne wybrane uwagi dotyczące operacji zbiorczych:</span><span class="sxs-lookup"><span data-stu-id="dbd31-146">Some other notes on batch operations:</span></span>

* <span data-ttu-id="dbd31-147">Można wykonać aktualizacji, usuwania i wstawia w hello same z jednym operacji zbiorczej.</span><span class="sxs-lookup"><span data-stu-id="dbd31-147">You can perform updates, deletes, and inserts in hello same single batch operation.</span></span>
* <span data-ttu-id="dbd31-148">Jedna operacja zbiorcza może zawierać zapasowej too100 jednostek.</span><span class="sxs-lookup"><span data-stu-id="dbd31-148">A single batch operation can include up too100 entities.</span></span>
* <span data-ttu-id="dbd31-149">Wszystkie jednostki w jednej operacji zbiorczej muszą mieć hello tego samego klucza partycji.</span><span class="sxs-lookup"><span data-stu-id="dbd31-149">All entities in a single batch operation must have hello same partition key.</span></span>
* <span data-ttu-id="dbd31-150">Mimo że jest możliwe tooperform zapytania w operacji zbiorczej, musi być jedyną operacją hello w partii hello.</span><span class="sxs-lookup"><span data-stu-id="dbd31-150">While it is possible tooperform a query as a batch operation, it must be hello only operation in hello batch.</span></span>

<span data-ttu-id="dbd31-151">Witaj poniższy przykład kodu tworzy dwa obiekty jednostki i dodaje zbyt[TableBatchOperation] [ dotnet_TableBatchOperation] przy użyciu hello [Wstaw] [ dotnet_TableBatchOperation_Insert] Metoda.</span><span class="sxs-lookup"><span data-stu-id="dbd31-151">hello following code example creates two entity objects and adds each too[TableBatchOperation][dotnet_TableBatchOperation] by using hello [Insert][dotnet_TableBatchOperation_Insert] method.</span></span> <span data-ttu-id="dbd31-152">Następnie [CloudTable][dotnet_CloudTable].[ ExecuteBatch] [ dotnet_CloudTable_ExecuteBatch] jest nazywany tooexecute hello operacji.</span><span class="sxs-lookup"><span data-stu-id="dbd31-152">Then, [CloudTable][dotnet_CloudTable].[ExecuteBatch][dotnet_CloudTable_ExecuteBatch] is called tooexecute hello operation.</span></span>

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

## <a name="retrieve-all-entities-in-a-partition"></a><span data-ttu-id="dbd31-153">Pobieranie wszystkich jednostek w partycji</span><span class="sxs-lookup"><span data-stu-id="dbd31-153">Retrieve all entities in a partition</span></span>
<span data-ttu-id="dbd31-154">tooquery tabeli dla wszystkich jednostek w partycji, użyj [TableQuery] [ dotnet_TableQuery] obiektu.</span><span class="sxs-lookup"><span data-stu-id="dbd31-154">tooquery a table for all entities in a partition, use a [TableQuery][dotnet_TableQuery] object.</span></span> <span data-ttu-id="dbd31-155">Witaj poniższy przykład kodu Określa filtr jednostek, gdzie "Smith" jest hello klucza partycji.</span><span class="sxs-lookup"><span data-stu-id="dbd31-155">hello following code example specifies a filter for entities where 'Smith' is hello partition key.</span></span> <span data-ttu-id="dbd31-156">W tym przykładzie drukowane hello pola każdej jednostki w konsoli toohello wyników zapytania hello.</span><span class="sxs-lookup"><span data-stu-id="dbd31-156">This example prints hello fields of each entity in hello query results toohello console.</span></span>

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

## <a name="retrieve-a-range-of-entities-in-a-partition"></a><span data-ttu-id="dbd31-157">Pobieranie zakresu jednostek w partycji</span><span class="sxs-lookup"><span data-stu-id="dbd31-157">Retrieve a range of entities in a partition</span></span>
<span data-ttu-id="dbd31-158">Jeśli nie chcesz tooquery wszystkich jednostek w partycji, możesz określić zakres, łącząc filtr klucza partycji hello z filtrem klucza wiersza.</span><span class="sxs-lookup"><span data-stu-id="dbd31-158">If you don't want tooquery all entities in a partition, you can specify a range by combining hello partition key filter with a row key filter.</span></span> <span data-ttu-id="dbd31-159">Witaj poniższy przykład kodu wykorzystuje dwa filtry tooget wszystkich jednostek w partycji "Smith", gdzie hello klucz wiersza (imię) rozpoczyna się od litery przed "E" w alfabecie hello, a następnie drukuje wyniki zapytania hello.</span><span class="sxs-lookup"><span data-stu-id="dbd31-159">hello following code example uses two filters tooget all entities in partition 'Smith' where hello row key (first name) starts with a letter before 'E' in hello alphabet, then prints hello query results.</span></span>

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

## <a name="retrieve-a-single-entity"></a><span data-ttu-id="dbd31-160">Pobieranie pojedynczej jednostki</span><span class="sxs-lookup"><span data-stu-id="dbd31-160">Retrieve a single entity</span></span>
<span data-ttu-id="dbd31-161">Tooretrieve kwerendy można pisać w jednej, określonej jednostki.</span><span class="sxs-lookup"><span data-stu-id="dbd31-161">You can write a query tooretrieve a single, specific entity.</span></span> <span data-ttu-id="dbd31-162">Witaj poniższy kod używa [TableOperation] [ dotnet_TableOperation] toospecify powitania klienta "Ben Smith".</span><span class="sxs-lookup"><span data-stu-id="dbd31-162">hello following code uses [TableOperation][dotnet_TableOperation] toospecify hello customer 'Ben Smith'.</span></span> <span data-ttu-id="dbd31-163">Ta metoda zwraca tylko jedną jednostkę zamiast kolekcji i hello zwrócił wartość w [TableResult][dotnet_TableResult].[ Wynik] [ dotnet_TableResult_Result] jest **CustomerEntity** obiektu.</span><span class="sxs-lookup"><span data-stu-id="dbd31-163">This method returns just one entity rather than a collection, and hello returned value in [TableResult][dotnet_TableResult].[Result][dotnet_TableResult_Result] is a **CustomerEntity** object.</span></span> <span data-ttu-id="dbd31-164">Określenie kluczy partycji i wiersza w zapytaniu jest hello najszybszy sposób tooretrieve pojedyncza jednostka z usługi tabeli hello.</span><span class="sxs-lookup"><span data-stu-id="dbd31-164">Specifying both partition and row keys in a query is hello fastest way tooretrieve a single entity from hello Table service.</span></span>

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

## <a name="replace-an-entity"></a><span data-ttu-id="dbd31-165">Zastępowanie jednostki</span><span class="sxs-lookup"><span data-stu-id="dbd31-165">Replace an entity</span></span>
<span data-ttu-id="dbd31-166">tooupdate jednostki, pobrać hello usługi tabel, zmodyfikuj obiekt jednostki hello i następnie zapisz zmiany hello ponownie toohello usługi tabel.</span><span class="sxs-lookup"><span data-stu-id="dbd31-166">tooupdate an entity, retrieve it from hello Table service, modify hello entity object, and then save hello changes back toohello Table service.</span></span> <span data-ttu-id="dbd31-167">Witaj poniższy kod zmienia numer telefonu istniejącego klienta.</span><span class="sxs-lookup"><span data-stu-id="dbd31-167">hello following code changes an existing customer's phone number.</span></span> <span data-ttu-id="dbd31-168">Zamiast wywoływać metodę [Insert][dotnet_TableOperation_Insert], ten kod używa metody [Replace][dotnet_TableOperation_Replace].</span><span class="sxs-lookup"><span data-stu-id="dbd31-168">Instead of calling [Insert][dotnet_TableOperation_Insert], this code uses [Replace][dotnet_TableOperation_Replace].</span></span> <span data-ttu-id="dbd31-169">[Zastąp] [ dotnet_TableOperation_Replace] przyczyny hello toobe jednostki całkowicie zastąpiona na powitania serwera, chyba że hello jednostki na powitania serwera została zmieniona, ponieważ został on pobrany, w którym to przypadku hello operacja zakończy się niepowodzeniem.</span><span class="sxs-lookup"><span data-stu-id="dbd31-169">[Replace][dotnet_TableOperation_Replace] causes hello entity toobe fully replaced on hello server, unless hello entity on hello server has changed since it was retrieved, in which case hello operation will fail.</span></span> <span data-ttu-id="dbd31-170">Ten błąd jest tooprevent aplikacji nieodwracalne nadpisanie zmiany wprowadzone od hello pobierania i aktualizowania przez inny składnik aplikacji.</span><span class="sxs-lookup"><span data-stu-id="dbd31-170">This failure is tooprevent your application from inadvertently overwriting a change made between hello retrieval and update by another component of your application.</span></span> <span data-ttu-id="dbd31-171">Hello prawidłowego obsługi tego błędu jest jednostki hello tooretrieve ponownie, wprowadź żądane zmiany (jeśli jest nadal ważny), a następnie wykonaj inną [Zastąp] [ dotnet_TableOperation_Replace] operacji.</span><span class="sxs-lookup"><span data-stu-id="dbd31-171">hello proper handling of this failure is tooretrieve hello entity again, make your changes (if still valid), and then perform another [Replace][dotnet_TableOperation_Replace] operation.</span></span> <span data-ttu-id="dbd31-172">Witaj w następnej sekcji opisano, jak toooverride to zachowanie.</span><span class="sxs-lookup"><span data-stu-id="dbd31-172">hello next section will show you how toooverride this behavior.</span></span>

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

## <a name="insert-or-replace-an-entity"></a><span data-ttu-id="dbd31-173">Wstawianie lub zastępowanie jednostki</span><span class="sxs-lookup"><span data-stu-id="dbd31-173">Insert-or-replace an entity</span></span>
<span data-ttu-id="dbd31-174">[Zastąp] [ dotnet_TableOperation_Replace] operacji zakończy się niepowodzeniem, jeśli jednostka hello została zmieniona, ponieważ został on pobrany z serwera hello.</span><span class="sxs-lookup"><span data-stu-id="dbd31-174">[Replace][dotnet_TableOperation_Replace] operations will fail if hello entity has been changed since it was retrieved from hello server.</span></span> <span data-ttu-id="dbd31-175">Ponadto należy pobrać jednostki hello z serwera hello najpierw aby hello [Zastąp] [ dotnet_TableOperation_Replace] toobe operacji powiodło się.</span><span class="sxs-lookup"><span data-stu-id="dbd31-175">Furthermore, you must retrieve hello entity from hello server first in order for hello [Replace][dotnet_TableOperation_Replace] operation toobe successful.</span></span> <span data-ttu-id="dbd31-176">Czasami jednak nie wiadomo Jeśli hello jednostka istnieje na serwerze hello i hello bieżące wartości znajdujące się w niej nie mają znaczenia.</span><span class="sxs-lookup"><span data-stu-id="dbd31-176">Sometimes, however, you don't know if hello entity exists on hello server and hello current values stored in it are irrelevant.</span></span> <span data-ttu-id="dbd31-177">Aktualizacja powinna nadpisać je wszystkie.</span><span class="sxs-lookup"><span data-stu-id="dbd31-177">Your update should overwrite them all.</span></span> <span data-ttu-id="dbd31-178">tooaccomplish, należy użyć [InsertOrReplace] [ dotnet_TableOperation_InsertOrReplace] operacji.</span><span class="sxs-lookup"><span data-stu-id="dbd31-178">tooaccomplish this, you would use an [InsertOrReplace][dotnet_TableOperation_InsertOrReplace] operation.</span></span> <span data-ttu-id="dbd31-179">Ta operacja wstawi hello jednostki, jeśli nie istnieje, lub zastąpi ją, jeśli tak jest, niezależnie od tego, kiedy dokonano hello ostatniej aktualizacji.</span><span class="sxs-lookup"><span data-stu-id="dbd31-179">This operation inserts hello entity if it doesn't exist, or replaces it if it does, regardless of when hello last update was made.</span></span>

<span data-ttu-id="dbd31-180">Jednostki klienta dla "Nowak Krzysztof" hello poniższy przykład kodu, jest tworzony i wstawione do tabeli "osoby" hello.</span><span class="sxs-lookup"><span data-stu-id="dbd31-180">In hello following code example, a customer entity for 'Fred Jones' is created and inserted into hello 'people' table.</span></span> <span data-ttu-id="dbd31-181">Następnie używamy hello [InsertOrReplace] [ dotnet_TableOperation_InsertOrReplace] toosave operacji jednostki z hello tego samego klucza partycji (Nowak) i wiersz klucza serwera toohello (Krzysztof), czas, podając inną wartość hello numer telefonu Właściwość.</span><span class="sxs-lookup"><span data-stu-id="dbd31-181">Next, we use hello [InsertOrReplace][dotnet_TableOperation_InsertOrReplace] operation toosave an entity with hello same partition key (Jones) and row key (Fred) toohello server, this time with a different value for hello PhoneNumber property.</span></span> <span data-ttu-id="dbd31-182">Ponieważ używamy operacji [InsertOrReplace][dotnet_TableOperation_InsertOrReplace], wszystkie wartości właściwości tej jednostki są zastępowane.</span><span class="sxs-lookup"><span data-stu-id="dbd31-182">Because we use [InsertOrReplace][dotnet_TableOperation_InsertOrReplace], all of its property values are replaced.</span></span> <span data-ttu-id="dbd31-183">Jednak jeśli jednostki 'Krzysztof Nowak' nie istnieje w tabeli hello, jego czy wstawiono.</span><span class="sxs-lookup"><span data-stu-id="dbd31-183">However, if a 'Fred Jones' entity hadn't already existed in hello table, it would have been inserted.</span></span>

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

## <a name="query-a-subset-of-entity-properties"></a><span data-ttu-id="dbd31-184">Tworzenie zapytania do podzbioru właściwości jednostki</span><span class="sxs-lookup"><span data-stu-id="dbd31-184">Query a subset of entity properties</span></span>
<span data-ttu-id="dbd31-185">Zapytanie tabeli może pobrać kilka właściwości jednostki zamiast wszystkich właściwości jednostki hello.</span><span class="sxs-lookup"><span data-stu-id="dbd31-185">A table query can retrieve just a few properties from an entity instead of all hello entity properties.</span></span> <span data-ttu-id="dbd31-186">Ta technika, zwana projekcją, redukuje przepustowość i może poprawiać wydajność zapytań, zwłaszcza w przypadku dużych jednostek.</span><span class="sxs-lookup"><span data-stu-id="dbd31-186">This technique, called projection, reduces bandwidth and can improve query performance, especially for large entities.</span></span> <span data-ttu-id="dbd31-187">Zapytanie Hello w hello następującego kodu zwraca tylko hello adresy e-mail jednostek w tabeli hello.</span><span class="sxs-lookup"><span data-stu-id="dbd31-187">hello query in hello following code returns only hello email addresses of entities in hello table.</span></span> <span data-ttu-id="dbd31-188">Operację tę przeprowadza się za pomocą zapytania [DynamicTableEntity][dotnet_DynamicTableEntity] lub [EntityResolver][dotnet_EntityResolver].</span><span class="sxs-lookup"><span data-stu-id="dbd31-188">This is done by using a query of [DynamicTableEntity][dotnet_DynamicTableEntity] and also [EntityResolver][dotnet_EntityResolver].</span></span> <span data-ttu-id="dbd31-189">Dowiedz się więcej o projekcji w hello [post na blogu Introducing Upsert i projekcji zapytań][blog_post_upsert].</span><span class="sxs-lookup"><span data-stu-id="dbd31-189">You can learn more about projection in hello [Introducing Upsert and Query Projection blog post][blog_post_upsert].</span></span> <span data-ttu-id="dbd31-190">Projekcja nie jest obsługiwana przez emulator magazynu hello, dlatego ten kod zadziała tylko wtedy, gdy używasz konta w usłudze tabel hello.</span><span class="sxs-lookup"><span data-stu-id="dbd31-190">Projection is not supported by hello storage emulator, so this code runs only when you're using an account in hello Table service.</span></span>

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

## <a name="delete-an-entity"></a><span data-ttu-id="dbd31-191">Usuwanie jednostki</span><span class="sxs-lookup"><span data-stu-id="dbd31-191">Delete an entity</span></span>
<span data-ttu-id="dbd31-192">Można z łatwością usunąć jednostkę po jej pobraniu przy użyciu hello tego samego wzorca co w przypadku aktualizowania jednostki.</span><span class="sxs-lookup"><span data-stu-id="dbd31-192">You can easily delete an entity after you have retrieved it by using hello same pattern shown for updating an entity.</span></span> <span data-ttu-id="dbd31-193">powitania po kod umożliwia pobranie i usunięcie jednostki klienta.</span><span class="sxs-lookup"><span data-stu-id="dbd31-193">hello following code retrieves and deletes a customer entity.</span></span>

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

## <a name="delete-a-table"></a><span data-ttu-id="dbd31-194">Usuwanie tabeli</span><span class="sxs-lookup"><span data-stu-id="dbd31-194">Delete a table</span></span>
<span data-ttu-id="dbd31-195">Na koniec hello poniższy przykład kodu usuwa tabelę z konta magazynu.</span><span class="sxs-lookup"><span data-stu-id="dbd31-195">Finally, hello following code example deletes a table from a storage account.</span></span> <span data-ttu-id="dbd31-196">Tabela, która została usunięta będzie niedostępna toobe ponownie utworzone w danym okresie czasu po usunięciu hello.</span><span class="sxs-lookup"><span data-stu-id="dbd31-196">A table that has been deleted will be unavailable toobe re-created for a period of time following hello deletion.</span></span>

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

## <a name="retrieve-entities-in-pages-asynchronously"></a><span data-ttu-id="dbd31-197">Pobieranie asynchroniczne jednostek na stronach</span><span class="sxs-lookup"><span data-stu-id="dbd31-197">Retrieve entities in pages asynchronously</span></span>
<span data-ttu-id="dbd31-198">Jeśli odczytujesz dużą liczbę jednostek i chcesz tooprocess/wyświetlić jednostki, zgodnie z ich pobraniu, zamiast oczekiwania na ich tooreturn wszystkich, możesz pobierać jednostki za pomocą zapytania segmentowanego.</span><span class="sxs-lookup"><span data-stu-id="dbd31-198">If you are reading a large number of entities, and you want tooprocess/display entities as they are retrieved rather than waiting for them all tooreturn, you can retrieve entities by using a segmented query.</span></span> <span data-ttu-id="dbd31-199">Ten przykład przedstawia, jak tooreturn wyników na stronach za pomocą wzorca Async-Await hello, dzięki czemu wykonanie nie jest blokowane podczas oczekiwania dla dużych zestawów wyników tooreturn.</span><span class="sxs-lookup"><span data-stu-id="dbd31-199">This example shows how tooreturn results in pages by using hello Async-Await pattern so that execution is not blocked while you're waiting for a large set of results tooreturn.</span></span> <span data-ttu-id="dbd31-200">Aby uzyskać więcej informacji na temat używania hello wzorca Async-Await w programie .NET, zobacz [programowanie asynchroniczne z Async i Await (C# i Visual Basic)](https://msdn.microsoft.com/library/hh191443.aspx).</span><span class="sxs-lookup"><span data-stu-id="dbd31-200">For more details on using hello Async-Await pattern in .NET, see [Asynchronous programming with Async and Await (C# and Visual Basic)](https://msdn.microsoft.com/library/hh191443.aspx).</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="dbd31-201">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="dbd31-201">Next steps</span></span>
<span data-ttu-id="dbd31-202">Teraz, kiedy znasz już podstawy magazynu tabel hello, wykonaj te toolearn łącza o bardziej skomplikowanych zadaniach magazynu:</span><span class="sxs-lookup"><span data-stu-id="dbd31-202">Now that you've learned hello basics of Table storage, follow these links toolearn about more complex storage tasks:</span></span>

* <span data-ttu-id="dbd31-203">[Eksplorator magazynu Microsoft Azure](../vs-azure-tools-storage-manage-with-storage-explorer.md) jest bezpłatna, aplikacja autonomiczny firmy Microsoft, który umożliwia toowork wizualnie z danymi usługi Azure Storage w systemie Windows, macOS i Linux.</span><span class="sxs-lookup"><span data-stu-id="dbd31-203">[Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md) is a free, standalone app from Microsoft that enables you toowork visually with Azure Storage data on Windows, macOS, and Linux.</span></span>
* <span data-ttu-id="dbd31-204">Więcej przykładów użycia usługi Table Storage znajdziesz w temacie [Getting Started with Azure Table Storage in .NET](https://azure.microsoft.com/documentation/samples/storage-table-dotnet-getting-started/) (Rozpoczynanie pracy z usługą Azure Table Storage w programie .NET)</span><span class="sxs-lookup"><span data-stu-id="dbd31-204">See more Table storage samples in [Getting Started with Azure Table Storage in .NET](https://azure.microsoft.com/documentation/samples/storage-table-dotnet-getting-started/)</span></span>
* <span data-ttu-id="dbd31-205">Widok hello dokumentację referencyjną usługi tabel, aby uzyskać szczegółowe informacje o dostępnych interfejsach API:</span><span class="sxs-lookup"><span data-stu-id="dbd31-205">View hello Table service reference documentation for complete details about available APIs:</span></span>
* [<span data-ttu-id="dbd31-206">Dokumentacja biblioteki klienta usługi Storage dla programu .NET</span><span class="sxs-lookup"><span data-stu-id="dbd31-206">Storage Client Library for .NET reference</span></span>](http://go.microsoft.com/fwlink/?LinkID=390731&clcid=0x409)
* [<span data-ttu-id="dbd31-207">Dokumentacja interfejsu API REST</span><span class="sxs-lookup"><span data-stu-id="dbd31-207">REST API reference</span></span>](http://msdn.microsoft.com/library/azure/dd179355)
* <span data-ttu-id="dbd31-208">Dowiedz się, jak kod hello toosimplify pisania toowork z usługą Azure Storage za pomocą hello [Azure WebJobs SDK](../app-service-web/websites-dotnet-webjobs-sdk-get-started.md)</span><span class="sxs-lookup"><span data-stu-id="dbd31-208">Learn how toosimplify hello code you write toowork with Azure Storage by using hello [Azure WebJobs SDK](../app-service-web/websites-dotnet-webjobs-sdk-get-started.md)</span></span>
* <span data-ttu-id="dbd31-209">Wyświetl więcej funkcji toolearn przewodników o dodatkowych opcjach przechowywania danych na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="dbd31-209">View more feature guides toolearn about additional options for storing data in Azure.</span></span>
* <span data-ttu-id="dbd31-210">[Rozpoczynanie pracy z magazynem obiektów Blob platformy Azure przy użyciu platformy .NET](storage-dotnet-how-to-use-blobs.md) toostore danych bez struktury.</span><span class="sxs-lookup"><span data-stu-id="dbd31-210">[Get started with Azure Blob storage using .NET](storage-dotnet-how-to-use-blobs.md) toostore unstructured data.</span></span>
* <span data-ttu-id="dbd31-211">[Połącz tooSQL bazy danych przy użyciu programu .NET (C#)](../sql-database/sql-database-develop-dotnet-simple.md) toostore relacyjnej bazie danych.</span><span class="sxs-lookup"><span data-stu-id="dbd31-211">[Connect tooSQL Database by using .NET (C#)](../sql-database/sql-database-develop-dotnet-simple.md) toostore relational data.</span></span>

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
