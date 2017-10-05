---
title: "Jak rozpocząć pracę z magazynu tabel i Visual Studio połączone usługi (platformy ASP.NET Core) | Dokumentacja firmy Microsoft"
description: "Jak rozpocząć pracę z magazynem tabel Azure w projekcie platformy ASP.NET Core w programie Visual Studio po połączeniu z kontem magazynu za pomocą programu Visual Studio połączone usługi"
services: storage
documentationcenter: 
author: kraigb
manager: ghogen
editor: 
ms.assetid: c3c451d1-71ff-4222-a348-c41c98a02b85
ms.service: storage
ms.workload: web
ms.tgt_pltfrm: vs-getting-started
ms.devlang: na
ms.topic: article
ms.date: 12/02/2016
ms.author: kraigb
ms.openlocfilehash: 8d05fe3ed9a5c66f186a930d4107162c1f322c05
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
# <a name="how-to-get-started-with-azure-table-storage-and-visual-studio-connected-services"></a><span data-ttu-id="5ae69-103">Jak rozpocząć pracę z magazynem tabel Azure i programu Visual Studio połączone usługi</span><span class="sxs-lookup"><span data-stu-id="5ae69-103">How to get started with Azure Table storage and Visual Studio connected services</span></span>
[!INCLUDE [storage-try-azure-tools-tables](../../includes/storage-try-azure-tools-tables.md)]

## <a name="overview"></a><span data-ttu-id="5ae69-104">Omówienie</span><span class="sxs-lookup"><span data-stu-id="5ae69-104">Overview</span></span>
<span data-ttu-id="5ae69-105">W tym artykule opisano sposób rozpoczęcie pracy z magazynem tabel Azure w programie Visual Studio po utworzony lub odwołanie do konta magazynu Azure w projekcie platformy ASP.NET Core za pomocą programu Visual Studio **dodać usług połączonych** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="5ae69-105">This article describes how get started using Azure Table storage in Visual Studio after you have created or referenced an Azure storage account in an ASP.NET Core project by using the Visual Studio **Add Connected Services** dialog.</span></span>

<span data-ttu-id="5ae69-106">Usługa Azure Table storage umożliwia przechowywania dużych ilości danych strukturalnych.</span><span class="sxs-lookup"><span data-stu-id="5ae69-106">The Azure Table storage service enables you to store large amounts of structured data.</span></span> <span data-ttu-id="5ae69-107">Usługa jest magazynem danych NoSQL, który przyjmuje uwierzytelnione wywołania z wewnątrz lub na zewnątrz w chmurze Azure.</span><span class="sxs-lookup"><span data-stu-id="5ae69-107">The service is a NoSQL data store that accepts authenticated calls from inside and outside the Azure cloud.</span></span> <span data-ttu-id="5ae69-108">Tabele Azure idealnie nadają się do przechowywania strukturalnych danych nierelacyjnych.</span><span class="sxs-lookup"><span data-stu-id="5ae69-108">Azure tables are ideal for storing structured, non-relational data.</span></span>

<span data-ttu-id="5ae69-109">**Dodać usług połączonych** operacji instaluje odpowiednie pakiety NuGet dostęp do magazynu Azure do projektu i dodaje ten ciąg połączenia dla konta magazynu do plików konfiguracji projektu.</span><span class="sxs-lookup"><span data-stu-id="5ae69-109">The **Add Connected Services** operation installs the appropriate NuGet packages to access Azure storage in your project and adds the connection string for the storage account to your project configuration files.</span></span>

<span data-ttu-id="5ae69-110">Aby uzyskać więcej ogólnych informacji o korzystaniu z magazynem tabel Azure, zobacz [Rozpoczynanie pracy z magazynem tabel Azure przy użyciu platformy .NET](../storage/storage-dotnet-how-to-use-tables.md).</span><span class="sxs-lookup"><span data-stu-id="5ae69-110">For more general information about using Azure Table storage, see [Get started with Azure Table storage using .NET](../storage/storage-dotnet-how-to-use-tables.md).</span></span>

<span data-ttu-id="5ae69-111">Aby rozpocząć pracę, należy najpierw utwórz tabelę na koncie magazynu.</span><span class="sxs-lookup"><span data-stu-id="5ae69-111">To get started, you first need to create a table in your storage account.</span></span> <span data-ttu-id="5ae69-112">Poniżej opisano sposób tworzenia tabeli platformy Azure w kodzie.</span><span class="sxs-lookup"><span data-stu-id="5ae69-112">We'll show you how to create an Azure table in code.</span></span> <span data-ttu-id="5ae69-113">Możemy również opisano sposób wykonywania tabeli podstawowej i jednostki operacje, takie jak dodawanie, modyfikowanie, Odczyt i Odczyt jednostek tabeli.</span><span class="sxs-lookup"><span data-stu-id="5ae69-113">We'll also show you how to perform basic table and entity operations, such as adding, modifying, reading and reading table entities.</span></span> <span data-ttu-id="5ae69-114">Przykłady są napisane w języku C\# kodu i używanie biblioteki klienta magazynu Azure dla platformy .NET.</span><span class="sxs-lookup"><span data-stu-id="5ae69-114">The samples are written in C\# code and use the Azure Storage Client Library for .NET.</span></span>

<span data-ttu-id="5ae69-115">**Uwaga** -niektórych interfejsów API, które wykonywania wywołań limit magazynu Azure w ASP.NET Core są asynchroniczne.</span><span class="sxs-lookup"><span data-stu-id="5ae69-115">**NOTE** - Some of the APIs that perform calls out to Azure storage in ASP.NET Core are asynchronous.</span></span> <span data-ttu-id="5ae69-116">Zobacz [programowanie asynchroniczne z Async i Await](http://msdn.microsoft.com/library/hh191443.aspx) Aby uzyskać więcej informacji.</span><span class="sxs-lookup"><span data-stu-id="5ae69-116">See [Asynchronous Programming with Async and Await](http://msdn.microsoft.com/library/hh191443.aspx) for more information.</span></span> <span data-ttu-id="5ae69-117">Poniższy kod przyjęto założenie, że są używane metody programowania asynchronicznego.</span><span class="sxs-lookup"><span data-stu-id="5ae69-117">The code below assumes Async programming methods are being used.</span></span>

## <a name="access-tables-in-code"></a><span data-ttu-id="5ae69-118">Dostęp do tabel w kodzie</span><span class="sxs-lookup"><span data-stu-id="5ae69-118">Access tables in code</span></span>
<span data-ttu-id="5ae69-119">Aby uzyskać dostęp do tabel w projektach platformy ASP.NET Core, musisz obejmują następujące elementy do plików źródłowych C# które uzyskują dostęp do magazynu tabel platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="5ae69-119">To access tables in ASP.NET Core projects, you need to include the following items to any C# source files that access Azure table storage.</span></span>

1. <span data-ttu-id="5ae69-120">Upewnij się, że deklaracje przestrzeni nazw w górnej części pliku C# Uwzględnij je **przy użyciu** instrukcje.</span><span class="sxs-lookup"><span data-stu-id="5ae69-120">Make sure the namespace declarations at the top of the C# file include these **using** statements.</span></span>
   
        using Microsoft.Framework.Configuration;
        using Microsoft.WindowsAzure.Storage;
        using Microsoft.WindowsAzure.Storage.Table;
        using System.Threading.Tasks;
        using LogLevel = Microsoft.Framework.Logging.LogLevel;
2. <span data-ttu-id="5ae69-121">Pobierz **CloudStorageAccount** obiekt, który reprezentuje informacje o koncie magazynu.</span><span class="sxs-lookup"><span data-stu-id="5ae69-121">Get a **CloudStorageAccount** object that represents your storage account information.</span></span> <span data-ttu-id="5ae69-122">Użyj następującego kodu można pobrać parametry połączenia magazynu, a informacje o koncie magazynu z konfiguracji usługi Azure.</span><span class="sxs-lookup"><span data-stu-id="5ae69-122">Use the following code to get the your storage connection string and storage account information from the Azure service configuration.</span></span>
   
        CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
            CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
   
    <span data-ttu-id="5ae69-123">**Uwaga** -korzystać ze wszystkich powyższych kodu przed kod w następujących przykładach.</span><span class="sxs-lookup"><span data-stu-id="5ae69-123">**NOTE** - Use all of the above code in front of the code in the following samples.</span></span>
3. <span data-ttu-id="5ae69-124">Pobierz **CloudTableClient** obiekt, aby odwoływać się do obiektów tabeli na koncie magazynu.</span><span class="sxs-lookup"><span data-stu-id="5ae69-124">Get a **CloudTableClient** object to reference the table objects in your storage account.</span></span>  
   
        // Create the table client.
        CloudTableClient tableClient = storageAccount.CreateCloudTableClient();
4. <span data-ttu-id="5ae69-125">Pobierz **CloudTable** obiektu odwołania, aby odwoływać się do określonej tabeli i jednostek.</span><span class="sxs-lookup"><span data-stu-id="5ae69-125">Get a **CloudTable** reference object to reference a specific table and entities.</span></span>
   
        // Get a reference to a table named "peopleTable"
        CloudTable table = tableClient.GetTableReference("peopleTable");

## <a name="create-a-table-in-code"></a><span data-ttu-id="5ae69-126">Utwórz tabelę w kodzie</span><span class="sxs-lookup"><span data-stu-id="5ae69-126">Create a table in code</span></span>
<span data-ttu-id="5ae69-127">Aby utworzyć tabeli platformy Azure, po prostu dodaj wywołanie **CreateIfNotExistsAsync()**.</span><span class="sxs-lookup"><span data-stu-id="5ae69-127">To create the Azure table, just add a call to **CreateIfNotExistsAsync()**.</span></span>

    // Create the CloudTable if it does not exist
    await table.CreateIfNotExistsAsync();

## <a name="add-an-entity-to-a-table"></a><span data-ttu-id="5ae69-128">Dodawanie jednostki do tabeli</span><span class="sxs-lookup"><span data-stu-id="5ae69-128">Add an entity to a table</span></span>
<span data-ttu-id="5ae69-129">Aby dodać jednostkę do tabeli należy utworzyć klasę, która definiuje właściwości jednostki.</span><span class="sxs-lookup"><span data-stu-id="5ae69-129">To add an entity to a table you create a class that defines the properties of your entity.</span></span> <span data-ttu-id="5ae69-130">Poniższy kod definiuje klasę jednostki nazywane **CustomerEntity** używającej imienia klienta jako klucza wiersza i nazwiska jako klucza partycji.</span><span class="sxs-lookup"><span data-stu-id="5ae69-130">The following code defines an entity class called **CustomerEntity** that uses the customer's first name as the row key and last name as the partition key.</span></span>

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

<span data-ttu-id="5ae69-131">Operacje tabeli obejmujące jednostki są wykonywane przy użyciu **CloudTable** obiekt został utworzony we wcześniejszej części "Dostęp do tabel w kodzie."</span><span class="sxs-lookup"><span data-stu-id="5ae69-131">Table operations involving entities are done using the **CloudTable** object you created earlier in "Access tables in code."</span></span> <span data-ttu-id="5ae69-132">**TableOperation** obiekt reprezentuje operacji do wykonania.</span><span class="sxs-lookup"><span data-stu-id="5ae69-132">The **TableOperation** object represents the operation to be done.</span></span> <span data-ttu-id="5ae69-133">W poniższym przykładzie przedstawiono sposób tworzenia **CloudTable** obiektu i **CustomerEntity** obiektu.</span><span class="sxs-lookup"><span data-stu-id="5ae69-133">The following code example shows how to create a **CloudTable** object and a **CustomerEntity** object.</span></span> <span data-ttu-id="5ae69-134">Aby przygotować operację, **TableOperation** służy do wstawiania jednostek klienta w tabeli.</span><span class="sxs-lookup"><span data-stu-id="5ae69-134">To prepare the operation, a **TableOperation** is created to insert the customer entity into the table.</span></span> <span data-ttu-id="5ae69-135">Na koniec operacji jest wykonywana przez wywołanie CloudTable.ExecuteAsync.</span><span class="sxs-lookup"><span data-stu-id="5ae69-135">Finally, the operation is executed by calling CloudTable.ExecuteAsync.</span></span>

    // Create a new customer entity.
    CustomerEntity customer1 = new CustomerEntity("Harp", "Walter");
    customer1.Email = "Walter@contoso.com";
    customer1.PhoneNumber = "425-555-0101";

    // Create the TableOperation that inserts the customer entity.
    TableOperation insertOperation = TableOperation.Insert(customer1);

    // Execute the insert operation.
    await peopleTable.ExecuteAsync(insertOperation);

## <a name="insert-a-batch-of-entities"></a><span data-ttu-id="5ae69-136">Zbiorcze wstawianie jednostek</span><span class="sxs-lookup"><span data-stu-id="5ae69-136">Insert a batch of entities</span></span>
<span data-ttu-id="5ae69-137">Wiele jednostek można wstawiać do tabeli w operacji zapisu pojedynczego.</span><span class="sxs-lookup"><span data-stu-id="5ae69-137">You can insert multiple entities into a table in a single write operation.</span></span> <span data-ttu-id="5ae69-138">Poniższy przykład kodu tworzy dwa obiekty jednostki ("Jan Kowalski" i "Ben Smith"), dodanie ich do **TableBatchOperation** przy użyciu **Wstaw** metody, a następnie uruchamia przez wywołanie operacji CloudTable.ExecuteBatchAsync.</span><span class="sxs-lookup"><span data-stu-id="5ae69-138">The following code example creates two entity objects ("Jeff Smith" and "Ben Smith"), adds them to a **TableBatchOperation** object using the **Insert** method, and then starts the operation by calling CloudTable.ExecuteBatchAsync.</span></span>

    // Create the batch operation.
    TableBatchOperation batchOperation = new TableBatchOperation();

    // Create a customer entity and add it to the table.
    CustomerEntity customer1 = new CustomerEntity("Smith", "Jeff");
    customer1.Email = "Jeff@contoso.com";
    customer1.PhoneNumber = "425-555-0104";

    // Create another customer entity and add it to the table.
    CustomerEntity customer2 = new CustomerEntity("Smith", "Ben");
    customer2.Email = "Ben@contoso.com";
    customer2.PhoneNumber = "425-555-0102";

    // Add both customer entities to the batch insert operation.
    batchOperation.Insert(customer1);
    batchOperation.Insert(customer2);

    // Execute the batch operation.
    await peopleTable.ExecuteBatchAsync(batchOperation);

## <a name="get-all-of-the-entities-in-a-partition"></a><span data-ttu-id="5ae69-139">Pobieranie wszystkich jednostek w partycji</span><span class="sxs-lookup"><span data-stu-id="5ae69-139">Get all of the entities in a partition</span></span>
<span data-ttu-id="5ae69-140">Aby sprawdzić tabeli dla wszystkich jednostek w partycji, użyj **TableQuery** obiektu.</span><span class="sxs-lookup"><span data-stu-id="5ae69-140">To query a table for all of the entities in a partition, use a **TableQuery** object.</span></span> <span data-ttu-id="5ae69-141">Poniższy przykład kodu określa filtr jednostek, gdzie „Smith” jest kluczem partycji.</span><span class="sxs-lookup"><span data-stu-id="5ae69-141">The following code example specifies a filter for entities where 'Smith' is the partition key.</span></span> <span data-ttu-id="5ae69-142">W tym przykładzie drukowane są pola każdej jednostki w wynikach zapytania w konsoli.</span><span class="sxs-lookup"><span data-stu-id="5ae69-142">This example prints the fields of each entity in the query results to the console.</span></span>

    // Construct the query operation for all customer entities where PartitionKey="Smith".
    TableQuery<CustomerEntity> query = new TableQuery<CustomerEntity>().Where(TableQuery.GenerateFilterCondition("PartitionKey", QueryComparisons.Equal, "Smith"));

    // Print the fields for each customer.
    TableContinuationToken token = null;
    do
    {
        TableQuerySegment<CustomerEntity> resultSegment = await peopleTable.ExecuteQuerySegmentedAsync(query, token);
        token = resultSegment.ContinuationToken;

        foreach (CustomerEntity entity in resultSegment.Results)
        {
            Console.WriteLine("{0}, {1}\t{2}\t{3}", entity.PartitionKey, entity.RowKey,
            entity.Email, entity.PhoneNumber);
        }
    } while (token != null);

## <a name="get-a-single-entity"></a><span data-ttu-id="5ae69-143">Pobierz pojedynczy element</span><span class="sxs-lookup"><span data-stu-id="5ae69-143">Get a single entity</span></span>
<span data-ttu-id="5ae69-144">Można napisać zapytanie do pobrania jednej, określonej jednostki.</span><span class="sxs-lookup"><span data-stu-id="5ae69-144">You can write a query to get a single, specific entity.</span></span> <span data-ttu-id="5ae69-145">Poniższy kod używa **TableOperation** obiekt, aby określić klienta o nazwie "Ben Smith".</span><span class="sxs-lookup"><span data-stu-id="5ae69-145">The following code uses a **TableOperation** object to specify a customer named 'Ben Smith'.</span></span> <span data-ttu-id="5ae69-146">Ta metoda zwraca tylko jedną jednostkę zamiast kolekcji, a zwrócona wartość w **TableResult.Result** jest **CustomerEntity** obiektu.</span><span class="sxs-lookup"><span data-stu-id="5ae69-146">This method returns just one entity, rather than a collection, and the returned value in **TableResult.Result** is a **CustomerEntity** object.</span></span> <span data-ttu-id="5ae69-147">Określenie kluczy partycji i wiersza w zapytaniu jest najszybszym sposobem na pobranie jednej jednostki z **tabeli** usługi.</span><span class="sxs-lookup"><span data-stu-id="5ae69-147">Specifying both partition and row keys in a query is the fastest way to retrieve a single entity from the **Table** service.</span></span>

    // Create a retrieve operation that takes a customer entity.
    TableOperation retrieveOperation = TableOperation.Retrieve<CustomerEntity>("Smith", "Ben");

    // Execute the retrieve operation.
    TableResult retrievedResult = await peopleTable.ExecuteAsync(retrieveOperation);

    // Print the phone number of the result.
    if (retrievedResult.Result != null)
       Console.WriteLine(((CustomerEntity)retrievedResult.Result).PhoneNumber);
    else
       Console.WriteLine("The phone number could not be retrieved.");

## <a name="delete-an-entity"></a><span data-ttu-id="5ae69-148">Usuwanie jednostki</span><span class="sxs-lookup"><span data-stu-id="5ae69-148">Delete an entity</span></span>
<span data-ttu-id="5ae69-149">Po możesz znaleźć, można usunąć jednostki.</span><span class="sxs-lookup"><span data-stu-id="5ae69-149">You can delete an entity after you find it.</span></span> <span data-ttu-id="5ae69-150">Następujący kod szuka jednostki klienta o nazwie "Ben Smith", a następnie przypadku ich znalezienia, usuwa ją.</span><span class="sxs-lookup"><span data-stu-id="5ae69-150">The following code looks for a customer entity named "Ben Smith" and if it finds it, it deletes it.</span></span>

    // Create a retrieve operation that expects a customer entity.
    TableOperation retrieveOperation = TableOperation.Retrieve<CustomerEntity>("Smith", "Ben");

    // Execute the operation.
    TableResult retrievedResult = peopleTable.Execute(retrieveOperation);

    // Assign the result to a CustomerEntity object.
    CustomerEntity deleteEntity = (CustomerEntity)retrievedResult.Result;

    // Create the Delete TableOperation and then execute it.
    if (deleteEntity != null)
    {
       TableOperation deleteOperation = TableOperation.Delete(deleteEntity);

       // Execute the operation.
       await peopleTable.ExecuteAsync(deleteOperation);

       Console.WriteLine("Entity deleted.");
    }

    else
       Console.WriteLine("Couldn't delete the entity.");

## <a name="next-steps"></a><span data-ttu-id="5ae69-151">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="5ae69-151">Next steps</span></span>
[!INCLUDE [vs-storage-dotnet-tables-next-steps](../../includes/vs-storage-dotnet-tables-next-steps.md)]

