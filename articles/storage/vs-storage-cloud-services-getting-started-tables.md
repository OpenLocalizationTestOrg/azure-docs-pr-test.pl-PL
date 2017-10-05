---
title: "Rozpoczynanie pracy z magazynem tabel i Visual Studio połączone usługi (usługi w chmurze) | Dokumentacja firmy Microsoft"
description: "Jak rozpocząć korzystanie z magazynu tabel Azure projektu usługi w chmurze w programie Visual Studio, po połączeniu z kontem magazynu za pomocą programu Visual Studio połączone usługi"
services: storage
documentationcenter: 
author: TomArcher
manager: douge
editor: 
ms.assetid: a3a11ed8-ba7f-4193-912b-e555f5b72184
ms.service: storage
ms.workload: web
ms.tgt_pltfrm: vs-getting-started
ms.devlang: na
ms.topic: article
ms.date: 12/02/2016
ms.author: tarcher
ms.openlocfilehash: 3208ddb1a1246a5ff25d272bfc7d8ba842348a36
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="getting-started-with-azure-table-storage-and-visual-studio-connected-services-cloud-services-projects"></a><span data-ttu-id="92956-103">Wprowadzenie do korzystania z magazynu tabel platformy Azure i programu Visual Studio połączone usługi (usług w chmurze projekty)</span><span class="sxs-lookup"><span data-stu-id="92956-103">Getting started with Azure table storage and Visual Studio connected services (cloud services projects)</span></span>
[!INCLUDE [storage-try-azure-tools-tables](../../includes/storage-try-azure-tools-tables.md)]

## <a name="overview"></a><span data-ttu-id="92956-104">Omówienie</span><span class="sxs-lookup"><span data-stu-id="92956-104">Overview</span></span>
<span data-ttu-id="92956-105">W tym artykule opisano, jak rozpocząć pracę przy użyciu magazynu tabel platformy Azure w programie Visual Studio po utworzony lub odwołanie do konta magazynu Azure w projekcie usługi w chmurze przy użyciu programu Visual Studio **dodać usług połączonych** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="92956-105">This article describes how to get started using Azure table storage in Visual Studio after you have created or referenced an Azure storage account in a cloud services project by using the Visual Studio **Add Connected Services** dialog.</span></span> <span data-ttu-id="92956-106">**Dodać usług połączonych** operacji instaluje odpowiednie pakiety NuGet dostęp do magazynu Azure do projektu i dodaje ten ciąg połączenia dla konta magazynu do plików konfiguracji projektu.</span><span class="sxs-lookup"><span data-stu-id="92956-106">The **Add Connected Services** operation installs the appropriate NuGet packages to access Azure storage in your project and adds the connection string for the storage account to your project configuration files.</span></span>

<span data-ttu-id="92956-107">Usługa Azure Table storage umożliwia przechowywania dużych ilości danych strukturalnych.</span><span class="sxs-lookup"><span data-stu-id="92956-107">The Azure Table storage service enables you to store large amounts of structured data.</span></span> <span data-ttu-id="92956-108">Usługa jest magazynem danych NoSQL, który przyjmuje uwierzytelnione wywołania z wewnątrz lub na zewnątrz w chmurze Azure.</span><span class="sxs-lookup"><span data-stu-id="92956-108">The service is a NoSQL datastore that accepts authenticated calls from inside and outside the Azure cloud.</span></span> <span data-ttu-id="92956-109">Tabele Azure idealnie nadają się do przechowywania strukturalnych danych nierelacyjnych.</span><span class="sxs-lookup"><span data-stu-id="92956-109">Azure tables are ideal for storing structured, non-relational data.</span></span>

<span data-ttu-id="92956-110">Aby rozpocząć pracę, należy najpierw utwórz tabelę na koncie magazynu.</span><span class="sxs-lookup"><span data-stu-id="92956-110">To get started, you first need to create a table in your storage account.</span></span> <span data-ttu-id="92956-111">Poniżej opisano sposób tworzenia tabeli platformy Azure w kodzie, a także wykonywać tabeli podstawowej i jednostki operacje, takie jak dodawanie, modyfikowanie, Odczyt i Odczyt jednostek tabeli.</span><span class="sxs-lookup"><span data-stu-id="92956-111">We'll show you how to create an Azure table in code, and also how to perform basic table and entity operations, such as adding, modifying, reading and reading table entities.</span></span> <span data-ttu-id="92956-112">Przykłady są napisane w języku C\# kodu i użyć [biblioteki klienta usługi Magazyn Microsoft Azure dla platformy .NET](https://msdn.microsoft.com/library/azure/dn261237.aspx).</span><span class="sxs-lookup"><span data-stu-id="92956-112">The samples are written in C\# code and use the [Microsoft Azure Storage client library for .NET](https://msdn.microsoft.com/library/azure/dn261237.aspx).</span></span>

<span data-ttu-id="92956-113">**Uwaga:** niektórych interfejsów API, które wykonywania wywołań limit magazynu Azure są asynchroniczne.</span><span class="sxs-lookup"><span data-stu-id="92956-113">**NOTE:** Some of the APIs that perform calls out to Azure storage are asynchronous.</span></span> <span data-ttu-id="92956-114">Zobacz [programowanie asynchroniczne z Async i Await](http://msdn.microsoft.com/library/hh191443.aspx) Aby uzyskać więcej informacji.</span><span class="sxs-lookup"><span data-stu-id="92956-114">See [Asynchronous programming with Async and Await](http://msdn.microsoft.com/library/hh191443.aspx) for more information.</span></span> <span data-ttu-id="92956-115">Poniższy kod przyjęto założenie, że są używane metody programowania asynchronicznego.</span><span class="sxs-lookup"><span data-stu-id="92956-115">The code below assumes async programming methods are being used.</span></span>

* <span data-ttu-id="92956-116">Zobacz [Rozpoczynanie pracy z magazynem tabel Azure przy użyciu platformy .NET](storage-dotnet-how-to-use-tables.md) uzyskać więcej informacji o programowo manipulowanie tabel.</span><span class="sxs-lookup"><span data-stu-id="92956-116">See [Get started with Azure Table storage using .NET](storage-dotnet-how-to-use-tables.md) for more information on programmatically manipulating tables.</span></span>
* <span data-ttu-id="92956-117">Zobacz [dokumentacji magazynu](https://azure.microsoft.com/documentation/services/storage/) ogólne informacje na temat usługi Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="92956-117">See [Storage documentation](https://azure.microsoft.com/documentation/services/storage/) for general information about Azure Storage.</span></span>
* <span data-ttu-id="92956-118">Zobacz [dokumentacji usługi w chmurze](https://azure.microsoft.com/documentation/services/cloud-services/) ogólne informacje dotyczące usług w chmurze Azure.</span><span class="sxs-lookup"><span data-stu-id="92956-118">See [Cloud Services documentation](https://azure.microsoft.com/documentation/services/cloud-services/) for general information about Azure cloud services.</span></span>
* <span data-ttu-id="92956-119">Zobacz [ASP.NET](http://www.asp.net) Aby uzyskać więcej informacji na temat programowania aplikacji ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="92956-119">See [ASP.NET](http://www.asp.net) for more information about programming ASP.NET applications.</span></span>

## <a name="access-tables-in-code"></a><span data-ttu-id="92956-120">Dostęp do tabel w kodzie</span><span class="sxs-lookup"><span data-stu-id="92956-120">Access tables in code</span></span>
<span data-ttu-id="92956-121">Dostęp do tabel w projekty usługi w chmurze, należy uwzględnić następujące elementy do plików źródłowych C# które uzyskują dostęp do magazynu tabel platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="92956-121">To access tables in cloud service projects, you need to include the following items to any C# source files that access Azure table storage.</span></span>

1. <span data-ttu-id="92956-122">Upewnij się, że deklaracje przestrzeni nazw w górnej części pliku C# Uwzględnij je **przy użyciu** instrukcje.</span><span class="sxs-lookup"><span data-stu-id="92956-122">Make sure the namespace declarations at the top of the C# file include these **using** statements.</span></span>
   
        using Microsoft.Framework.Configuration;
        using Microsoft.WindowsAzure.Storage;
        using Microsoft.WindowsAzure.Storage.Table;
        using System.Threading.Tasks;
        using LogLevel = Microsoft.Framework.Logging.LogLevel;
2. <span data-ttu-id="92956-123">Pobierz **CloudStorageAccount** obiekt, który reprezentuje informacje o koncie magazynu.</span><span class="sxs-lookup"><span data-stu-id="92956-123">Get a **CloudStorageAccount** object that represents your storage account information.</span></span> <span data-ttu-id="92956-124">Użyj następującego kodu, aby pobrać parametry połączenia magazynu i informacji o koncie magazynu z konfiguracji usługi Azure.</span><span class="sxs-lookup"><span data-stu-id="92956-124">Use the following code to get the storage connection string and storage account information from the Azure service configuration.</span></span>
   
         CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
           CloudConfigurationManager.GetSetting("<storage account name>
         _AzureStorageConnectionString"));
   > [!NOTE]
   > <span data-ttu-id="92956-125">Korzystać ze wszystkich powyższych kodu przed kod w następujących przykładach.</span><span class="sxs-lookup"><span data-stu-id="92956-125">Use all of the above code in front of the code in the following samples.</span></span>
   > 
   > 
3. <span data-ttu-id="92956-126">Pobierz **CloudTableClient** obiekt, aby odwoływać się do obiektów tabeli na koncie magazynu.</span><span class="sxs-lookup"><span data-stu-id="92956-126">Get a **CloudTableClient** object to reference the table objects in your storage account.</span></span>
   
         // Create the table client.
         CloudTableClient tableClient = storageAccount.CreateCloudTableClient();
4. <span data-ttu-id="92956-127">Pobierz **CloudTable** obiektu odwołania, aby odwoływać się do określonej tabeli i jednostek.</span><span class="sxs-lookup"><span data-stu-id="92956-127">Get a **CloudTable** reference object to reference a specific table and entities.</span></span>
   
        // Get a reference to a table named "peopleTable".
        CloudTable peopleTable = tableClient.GetTableReference("peopleTable");

## <a name="create-a-table-in-code"></a><span data-ttu-id="92956-128">Utwórz tabelę w kodzie</span><span class="sxs-lookup"><span data-stu-id="92956-128">Create a table in code</span></span>
<span data-ttu-id="92956-129">Aby utworzyć tabeli platformy Azure, po prostu dodaj wywołanie **CreateIfNotExistsAsync** do po uzyskaniu **CloudTable** obiekt zgodnie z opisem w sekcji "Dostęp do tabel w kodzie".</span><span class="sxs-lookup"><span data-stu-id="92956-129">To create the Azure table, just add a call to **CreateIfNotExistsAsync** to the after you get a **CloudTable** object as described in the "Access tables in code" section.</span></span>

    // Create the CloudTable if it does not exist.
    await peopleTable.CreateIfNotExistsAsync();

## <a name="add-an-entity-to-a-table"></a><span data-ttu-id="92956-130">Dodawanie jednostki do tabeli</span><span class="sxs-lookup"><span data-stu-id="92956-130">Add an entity to a table</span></span>
<span data-ttu-id="92956-131">Aby dodać jednostkę do tabeli, należy utworzyć klasę, która definiuje właściwości jednostki.</span><span class="sxs-lookup"><span data-stu-id="92956-131">To add an entity to a table, create a class that defines the properties of your entity.</span></span> <span data-ttu-id="92956-132">Poniższy kod definiuje klasę jednostki nazywane **CustomerEntity** używającej imienia klienta jako klucza wiersza i nazwiska jako klucza partycji.</span><span class="sxs-lookup"><span data-stu-id="92956-132">The following code defines an entity class called **CustomerEntity** that uses the customer's first name as the row key and the last name as the partition key.</span></span>

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

<span data-ttu-id="92956-133">Operacje tabeli obejmujące jednostki są wykonywane przy użyciu **CloudTable** obiekt, który został utworzony we wcześniejszej części "Dostęp do tabel w kodzie."</span><span class="sxs-lookup"><span data-stu-id="92956-133">Table operations involving entities are done using the **CloudTable** object that you created earlier in "Access tables in code."</span></span> <span data-ttu-id="92956-134">**TableOperation** obiekt reprezentuje operacji do wykonania.</span><span class="sxs-lookup"><span data-stu-id="92956-134">The **TableOperation** object represents the operation to be done.</span></span> <span data-ttu-id="92956-135">W poniższym przykładzie przedstawiono sposób tworzenia **CloudTable** obiektu i **CustomerEntity** obiektu.</span><span class="sxs-lookup"><span data-stu-id="92956-135">The following code example shows how to create a **CloudTable** object and a **CustomerEntity** object.</span></span> <span data-ttu-id="92956-136">Aby przygotować operację, **TableOperation** służy do wstawiania jednostek klienta w tabeli.</span><span class="sxs-lookup"><span data-stu-id="92956-136">To prepare the operation, a **TableOperation** is created to insert the customer entity into the table.</span></span> <span data-ttu-id="92956-137">Na koniec operacji jest wykonywana przez wywołanie **CloudTable.ExecuteAsync**.</span><span class="sxs-lookup"><span data-stu-id="92956-137">Finally, the operation is executed by calling **CloudTable.ExecuteAsync**.</span></span>

    // Create a new customer entity.
    CustomerEntity customer1 = new CustomerEntity("Harp", "Walter");
    customer1.Email = "Walter@contoso.com";
    customer1.PhoneNumber = "425-555-0101";

    // Create the TableOperation that inserts the customer entity.
    TableOperation insertOperation = TableOperation.Insert(customer1);

    // Execute the insert operation.
    await peopleTable.ExecuteAsync(insertOperation);


## <a name="insert-a-batch-of-entities"></a><span data-ttu-id="92956-138">Zbiorcze wstawianie jednostek</span><span class="sxs-lookup"><span data-stu-id="92956-138">Insert a batch of entities</span></span>
<span data-ttu-id="92956-139">Wiele jednostek można wstawiać do tabeli w operacji zapisu pojedynczego.</span><span class="sxs-lookup"><span data-stu-id="92956-139">You can insert multiple entities into a table in a single write operation.</span></span> <span data-ttu-id="92956-140">Poniższy przykład kodu tworzy dwa obiekty jednostki ("Jan Kowalski" i "Ben Smith"), dodanie ich do **TableBatchOperation** przy użyciu metody Insert, a następnie rozpoczyna operację wywołując **CloudTable.ExecuteBatchAsync**.</span><span class="sxs-lookup"><span data-stu-id="92956-140">The following code example creates two entity objects ("Jeff Smith" and "Ben Smith"), adds them to a **TableBatchOperation** object using the Insert method, and then starts the operation by calling **CloudTable.ExecuteBatchAsync**.</span></span>

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

## <a name="get-all-of-the-entities-in-a-partition"></a><span data-ttu-id="92956-141">Pobieranie wszystkich jednostek w partycji</span><span class="sxs-lookup"><span data-stu-id="92956-141">Get all of the entities in a partition</span></span>
<span data-ttu-id="92956-142">Aby sprawdzić tabeli dla wszystkich jednostek w partycji, użyj **TableQuery** obiektu.</span><span class="sxs-lookup"><span data-stu-id="92956-142">To query a table for all of the entities in a partition, use a **TableQuery** object.</span></span> <span data-ttu-id="92956-143">Poniższy przykład kodu określa filtr jednostek, gdzie „Smith” jest kluczem partycji.</span><span class="sxs-lookup"><span data-stu-id="92956-143">The following code example specifies a filter for entities where 'Smith' is the partition key.</span></span> <span data-ttu-id="92956-144">W tym przykładzie drukowane są pola każdej jednostki w wynikach zapytania w konsoli.</span><span class="sxs-lookup"><span data-stu-id="92956-144">This example prints the fields of each entity in the query results to the console.</span></span>

    // Construct the query operation for all customer entities where PartitionKey="Smith".
    TableQuery<CustomerEntity> query = new TableQuery<CustomerEntity>()
        .Where(TableQuery.GenerateFilterCondition("PartitionKey", QueryComparisons.Equal, "Smith"));

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

    return View();


## <a name="get-a-single-entity"></a><span data-ttu-id="92956-145">Pobierz pojedynczy element</span><span class="sxs-lookup"><span data-stu-id="92956-145">Get a single entity</span></span>
<span data-ttu-id="92956-146">Można napisać zapytanie do pobrania jednej, określonej jednostki.</span><span class="sxs-lookup"><span data-stu-id="92956-146">You can write a query to get a single, specific entity.</span></span> <span data-ttu-id="92956-147">Poniższy kod używa **TableOperation** obiekt, aby określić klienta o nazwie "Ben Smith".</span><span class="sxs-lookup"><span data-stu-id="92956-147">The following code uses a **TableOperation** object to specify a customer named 'Ben Smith'.</span></span> <span data-ttu-id="92956-148">Ta metoda zwraca tylko jedną jednostkę zamiast kolekcji, a zwrócona wartość w **TableResult.Result** jest **CustomerEntity** obiektu.</span><span class="sxs-lookup"><span data-stu-id="92956-148">This method returns just one entity, rather than a collection, and the returned value in **TableResult.Result** is a **CustomerEntity** object.</span></span> <span data-ttu-id="92956-149">Określenie kluczy partycji i wiersza w zapytaniu jest najszybszym sposobem na pobranie jednej jednostki z **tabeli** usługi.</span><span class="sxs-lookup"><span data-stu-id="92956-149">Specifying both partition and row keys in a query is the fastest way to retrieve a single entity from the **Table** service.</span></span>

    // Create a retrieve operation that takes a customer entity.
    TableOperation retrieveOperation = TableOperation.Retrieve<CustomerEntity>("Smith", "Ben");

    // Execute the retrieve operation.
    TableResult retrievedResult = await peopleTable.ExecuteAsync(retrieveOperation);

    // Print the phone number of the result.
    if (retrievedResult.Result != null)
       Console.WriteLine(((CustomerEntity)retrievedResult.Result).PhoneNumber);
    else
       Console.WriteLine("The phone number could not be retrieved.");

## <a name="delete-an-entity"></a><span data-ttu-id="92956-150">Usuwanie jednostki</span><span class="sxs-lookup"><span data-stu-id="92956-150">Delete an entity</span></span>
<span data-ttu-id="92956-151">Po możesz znaleźć, można usunąć jednostki.</span><span class="sxs-lookup"><span data-stu-id="92956-151">You can delete an entity after you find it.</span></span> <span data-ttu-id="92956-152">Poniższy kod szuka jednostki klienta o nazwie "Ben Smith", i przypadku ich znalezienia, usunięcia go.</span><span class="sxs-lookup"><span data-stu-id="92956-152">The following code looks for a customer entity named "Ben Smith", and if it finds it, it deletes it.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="92956-153">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="92956-153">Next steps</span></span>
[!INCLUDE [vs-storage-dotnet-tables-next-steps](../../includes/vs-storage-dotnet-tables-next-steps.md)]

