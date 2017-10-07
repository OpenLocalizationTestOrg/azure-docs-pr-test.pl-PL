---
title: "aaaHow tooget pracy z magazynem tabel i Visual Studio podłączonych usług (platformy ASP.NET Core) | Dokumentacja firmy Microsoft"
description: "Jak tooget pracy z magazynem tabel Azure w projekcie platformy ASP.NET Core w programie Visual Studio po łączenie tooa konto magazynu przy użyciu programu Visual Studio połączenia usługi"
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
ms.openlocfilehash: e3eb3f3e65456108dd3cde7e3e470f98ba456e35
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooget-started-with-azure-table-storage-and-visual-studio-connected-services"></a><span data-ttu-id="c5784-103">Jak tooget wprowadzenie do magazynu tabel Azure i programu Visual Studio podłączonych usług</span><span class="sxs-lookup"><span data-stu-id="c5784-103">How tooget started with Azure Table storage and Visual Studio connected services</span></span>
[!INCLUDE [storage-try-azure-tools-tables](../../includes/storage-try-azure-tools-tables.md)]

## <a name="overview"></a><span data-ttu-id="c5784-104">Omówienie</span><span class="sxs-lookup"><span data-stu-id="c5784-104">Overview</span></span>
<span data-ttu-id="c5784-105">W tym artykule opisano sposób uzyskać uruchomiony przy użyciu tabel Azure hello magazynu w programie Visual Studio po utworzony lub odwołanie do konta magazynu Azure w projekcie platformy ASP.NET Core za pomocą programu Visual Studio **dodać usług połączonych** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="c5784-105">This article describes how get started using Azure Table storage in Visual Studio after you have created or referenced an Azure storage account in an ASP.NET Core project by using hello Visual Studio **Add Connected Services** dialog.</span></span>

<span data-ttu-id="c5784-106">Usługa Azure Table storage Hello umożliwia toostore dużych ilości danych strukturalnych.</span><span class="sxs-lookup"><span data-stu-id="c5784-106">hello Azure Table storage service enables you toostore large amounts of structured data.</span></span> <span data-ttu-id="c5784-107">Usługa Hello jest magazynem danych NoSQL, który przyjmuje uwierzytelnione wywołania z wewnątrz, jak i poza hello chmury Azure.</span><span class="sxs-lookup"><span data-stu-id="c5784-107">hello service is a NoSQL data store that accepts authenticated calls from inside and outside hello Azure cloud.</span></span> <span data-ttu-id="c5784-108">Tabele Azure idealnie nadają się do przechowywania strukturalnych danych nierelacyjnych.</span><span class="sxs-lookup"><span data-stu-id="c5784-108">Azure tables are ideal for storing structured, non-relational data.</span></span>

<span data-ttu-id="c5784-109">Witaj **dodać usług połączonych** operacji instaluje hello odpowiednie NuGet pakiety tooaccess magazynu Azure w projekcie i dodaje hello parametry połączenia dla hello magazynu konta tooyour pliki konfiguracji projektu.</span><span class="sxs-lookup"><span data-stu-id="c5784-109">hello **Add Connected Services** operation installs hello appropriate NuGet packages tooaccess Azure storage in your project and adds hello connection string for hello storage account tooyour project configuration files.</span></span>

<span data-ttu-id="c5784-110">Aby uzyskać więcej ogólnych informacji o korzystaniu z magazynem tabel Azure, zobacz [Rozpoczynanie pracy z magazynem tabel Azure przy użyciu platformy .NET](../storage/storage-dotnet-how-to-use-tables.md).</span><span class="sxs-lookup"><span data-stu-id="c5784-110">For more general information about using Azure Table storage, see [Get started with Azure Table storage using .NET](../storage/storage-dotnet-how-to-use-tables.md).</span></span>

<span data-ttu-id="c5784-111">tooget uruchomiona, należy najpierw toocreate tabeli na koncie magazynu.</span><span class="sxs-lookup"><span data-stu-id="c5784-111">tooget started, you first need toocreate a table in your storage account.</span></span> <span data-ttu-id="c5784-112">Poniżej opisano sposób toocreate Azure tabeli w kodzie.</span><span class="sxs-lookup"><span data-stu-id="c5784-112">We'll show you how toocreate an Azure table in code.</span></span> <span data-ttu-id="c5784-113">Również pokażemy ci jak tabela podstawowa tooperform i jednostki operacje, takie jak dodawanie, modyfikowanie, Odczyt i odczytywania tabeli jednostek.</span><span class="sxs-lookup"><span data-stu-id="c5784-113">We'll also show you how tooperform basic table and entity operations, such as adding, modifying, reading and reading table entities.</span></span> <span data-ttu-id="c5784-114">Przykłady Hello są napisane w języku C\# kodu i użyć hello biblioteki klienta magazynu Azure dla platformy .NET.</span><span class="sxs-lookup"><span data-stu-id="c5784-114">hello samples are written in C\# code and use hello Azure Storage Client Library for .NET.</span></span>

<span data-ttu-id="c5784-115">**Uwaga** — niektóre hello interfejsów API, które wykonywania wywołań limit magazynu tooAzure w ASP.NET Core są asynchroniczne.</span><span class="sxs-lookup"><span data-stu-id="c5784-115">**NOTE** - Some of hello APIs that perform calls out tooAzure storage in ASP.NET Core are asynchronous.</span></span> <span data-ttu-id="c5784-116">Zobacz [programowanie asynchroniczne z Async i Await](http://msdn.microsoft.com/library/hh191443.aspx) Aby uzyskać więcej informacji.</span><span class="sxs-lookup"><span data-stu-id="c5784-116">See [Asynchronous Programming with Async and Await](http://msdn.microsoft.com/library/hh191443.aspx) for more information.</span></span> <span data-ttu-id="c5784-117">Poniższy kod Hello przyjęto założenie, że są używane metody programowania asynchronicznego.</span><span class="sxs-lookup"><span data-stu-id="c5784-117">hello code below assumes Async programming methods are being used.</span></span>

## <a name="access-tables-in-code"></a><span data-ttu-id="c5784-118">Dostęp do tabel w kodzie</span><span class="sxs-lookup"><span data-stu-id="c5784-118">Access tables in code</span></span>
<span data-ttu-id="c5784-119">tabele tooaccess w projektach platformy ASP.NET Core, należy hello tooinclude następujące pliki źródłowe tooany C# elementów, które uzyskują dostęp do magazynu tabel platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="c5784-119">tooaccess tables in ASP.NET Core projects, you need tooinclude hello following items tooany C# source files that access Azure table storage.</span></span>

1. <span data-ttu-id="c5784-120">Upewnij się, że deklaracje przestrzeni nazw hello u góry pliku hello C# hello Uwzględnij je **przy użyciu** instrukcje.</span><span class="sxs-lookup"><span data-stu-id="c5784-120">Make sure hello namespace declarations at hello top of hello C# file include these **using** statements.</span></span>
   
        using Microsoft.Framework.Configuration;
        using Microsoft.WindowsAzure.Storage;
        using Microsoft.WindowsAzure.Storage.Table;
        using System.Threading.Tasks;
        using LogLevel = Microsoft.Framework.Logging.LogLevel;
2. <span data-ttu-id="c5784-121">Pobierz **CloudStorageAccount** obiekt, który reprezentuje informacje o koncie magazynu.</span><span class="sxs-lookup"><span data-stu-id="c5784-121">Get a **CloudStorageAccount** object that represents your storage account information.</span></span> <span data-ttu-id="c5784-122">Witaj Użyj następującego kodu tooget hello parametry połączenia magazynu, a informacje o koncie magazynu z konfiguracji usługi Azure hello.</span><span class="sxs-lookup"><span data-stu-id="c5784-122">Use hello following code tooget hello your storage connection string and storage account information from hello Azure service configuration.</span></span>
   
        CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
            CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
   
    <span data-ttu-id="c5784-123">**Uwaga** -korzystać ze wszystkich hello powyżej kodu przed kodem hello w hello następujące przykłady.</span><span class="sxs-lookup"><span data-stu-id="c5784-123">**NOTE** - Use all of hello above code in front of hello code in hello following samples.</span></span>
3. <span data-ttu-id="c5784-124">Pobierz **CloudTableClient** obiekt tooreference hello tabeli obiektów na koncie magazynu.</span><span class="sxs-lookup"><span data-stu-id="c5784-124">Get a **CloudTableClient** object tooreference hello table objects in your storage account.</span></span>  
   
        // Create hello table client.
        CloudTableClient tableClient = storageAccount.CreateCloudTableClient();
4. <span data-ttu-id="c5784-125">Pobierz **CloudTable** odwoływać się do obiektu tooreference określonej tabeli i jednostek.</span><span class="sxs-lookup"><span data-stu-id="c5784-125">Get a **CloudTable** reference object tooreference a specific table and entities.</span></span>
   
        // Get a reference tooa table named "peopleTable"
        CloudTable table = tableClient.GetTableReference("peopleTable");

## <a name="create-a-table-in-code"></a><span data-ttu-id="c5784-126">Utwórz tabelę w kodzie</span><span class="sxs-lookup"><span data-stu-id="c5784-126">Create a table in code</span></span>
<span data-ttu-id="c5784-127">Witaj toocreate tabeli platformy Azure, po prostu dodaj wywołanie za**CreateIfNotExistsAsync()**.</span><span class="sxs-lookup"><span data-stu-id="c5784-127">toocreate hello Azure table, just add a call too**CreateIfNotExistsAsync()**.</span></span>

    // Create hello CloudTable if it does not exist
    await table.CreateIfNotExistsAsync();

## <a name="add-an-entity-tooa-table"></a><span data-ttu-id="c5784-128">Dodaj tabelę tooa jednostki</span><span class="sxs-lookup"><span data-stu-id="c5784-128">Add an entity tooa table</span></span>
<span data-ttu-id="c5784-129">tooadd tabeli tooa jednostki, Utwórz klasę, która definiuje właściwości hello jednostki.</span><span class="sxs-lookup"><span data-stu-id="c5784-129">tooadd an entity tooa table you create a class that defines hello properties of your entity.</span></span> <span data-ttu-id="c5784-130">Witaj poniższy kod definiuje klasę jednostki nazywane **CustomerEntity** imienia klienta jako hello klucz wiersza i nazwiska jako klucza partycji hello tekst hello zastosowań.</span><span class="sxs-lookup"><span data-stu-id="c5784-130">hello following code defines an entity class called **CustomerEntity** that uses hello customer's first name as hello row key and last name as hello partition key.</span></span>

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

<span data-ttu-id="c5784-131">Operacje tabeli obejmujące jednostki są wykonywane przy użyciu hello **CloudTable** obiekt został utworzony we wcześniejszej części "Dostęp do tabel w kodzie."</span><span class="sxs-lookup"><span data-stu-id="c5784-131">Table operations involving entities are done using hello **CloudTable** object you created earlier in "Access tables in code."</span></span> <span data-ttu-id="c5784-132">Witaj **TableOperation** obiekt reprezentuje toobe operacji hello gotowe.</span><span class="sxs-lookup"><span data-stu-id="c5784-132">hello **TableOperation** object represents hello operation toobe done.</span></span> <span data-ttu-id="c5784-133">Witaj, jak po przedstawia przykładowy kod toocreate **CloudTable** obiektu i **CustomerEntity** obiektu.</span><span class="sxs-lookup"><span data-stu-id="c5784-133">hello following code example shows how toocreate a **CloudTable** object and a **CustomerEntity** object.</span></span> <span data-ttu-id="c5784-134">Operacja hello tooprepare, **TableOperation** utworzeniu tooinsert powitania klienta jednostki do tabeli hello.</span><span class="sxs-lookup"><span data-stu-id="c5784-134">tooprepare hello operation, a **TableOperation** is created tooinsert hello customer entity into hello table.</span></span> <span data-ttu-id="c5784-135">Na koniec operacji hello jest wykonywana przez wywołanie CloudTable.ExecuteAsync.</span><span class="sxs-lookup"><span data-stu-id="c5784-135">Finally, hello operation is executed by calling CloudTable.ExecuteAsync.</span></span>

    // Create a new customer entity.
    CustomerEntity customer1 = new CustomerEntity("Harp", "Walter");
    customer1.Email = "Walter@contoso.com";
    customer1.PhoneNumber = "425-555-0101";

    // Create hello TableOperation that inserts hello customer entity.
    TableOperation insertOperation = TableOperation.Insert(customer1);

    // Execute hello insert operation.
    await peopleTable.ExecuteAsync(insertOperation);

## <a name="insert-a-batch-of-entities"></a><span data-ttu-id="c5784-136">Zbiorcze wstawianie jednostek</span><span class="sxs-lookup"><span data-stu-id="c5784-136">Insert a batch of entities</span></span>
<span data-ttu-id="c5784-137">Wiele jednostek można wstawiać do tabeli w operacji zapisu pojedynczego.</span><span class="sxs-lookup"><span data-stu-id="c5784-137">You can insert multiple entities into a table in a single write operation.</span></span> <span data-ttu-id="c5784-138">Witaj poniższy przykład kodu tworzy dwa obiekty jednostki ("Jan Kowalski" i "Ben Smith"), dodaje je tooa **TableBatchOperation** obiektu przy użyciu hello **Wstaw** metody, a następnie uruchamia działanie hello wywoływanie CloudTable.ExecuteBatchAsync.</span><span class="sxs-lookup"><span data-stu-id="c5784-138">hello following code example creates two entity objects ("Jeff Smith" and "Ben Smith"), adds them tooa **TableBatchOperation** object using hello **Insert** method, and then starts hello operation by calling CloudTable.ExecuteBatchAsync.</span></span>

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
    await peopleTable.ExecuteBatchAsync(batchOperation);

## <a name="get-all-of-hello-entities-in-a-partition"></a><span data-ttu-id="c5784-139">Pobierz wszystkie hello jednostek w partycji</span><span class="sxs-lookup"><span data-stu-id="c5784-139">Get all of hello entities in a partition</span></span>
<span data-ttu-id="c5784-140">tooquery tabeli dla wszystkich hello jednostek w partycji, użyj **TableQuery** obiektu.</span><span class="sxs-lookup"><span data-stu-id="c5784-140">tooquery a table for all of hello entities in a partition, use a **TableQuery** object.</span></span> <span data-ttu-id="c5784-141">Witaj poniższy przykład kodu Określa filtr jednostek, gdzie "Smith" jest hello klucza partycji.</span><span class="sxs-lookup"><span data-stu-id="c5784-141">hello following code example specifies a filter for entities where 'Smith' is hello partition key.</span></span> <span data-ttu-id="c5784-142">W tym przykładzie drukowane hello pola każdej jednostki w konsoli toohello wyników zapytania hello.</span><span class="sxs-lookup"><span data-stu-id="c5784-142">This example prints hello fields of each entity in hello query results toohello console.</span></span>

    // Construct hello query operation for all customer entities where PartitionKey="Smith".
    TableQuery<CustomerEntity> query = new TableQuery<CustomerEntity>().Where(TableQuery.GenerateFilterCondition("PartitionKey", QueryComparisons.Equal, "Smith"));

    // Print hello fields for each customer.
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

## <a name="get-a-single-entity"></a><span data-ttu-id="c5784-143">Pobierz pojedynczy element</span><span class="sxs-lookup"><span data-stu-id="c5784-143">Get a single entity</span></span>
<span data-ttu-id="c5784-144">Tooget kwerendy można pisać w jednej, określonej jednostki.</span><span class="sxs-lookup"><span data-stu-id="c5784-144">You can write a query tooget a single, specific entity.</span></span> <span data-ttu-id="c5784-145">Witaj poniższy kod używa **TableOperation** obiekt toospecify klienta o nazwie "Ben Smith".</span><span class="sxs-lookup"><span data-stu-id="c5784-145">hello following code uses a **TableOperation** object toospecify a customer named 'Ben Smith'.</span></span> <span data-ttu-id="c5784-146">Ta metoda zwraca tylko jedną jednostkę zamiast kolekcji i hello zwrócił wartość w **TableResult.Result** jest **CustomerEntity** obiektu.</span><span class="sxs-lookup"><span data-stu-id="c5784-146">This method returns just one entity, rather than a collection, and hello returned value in **TableResult.Result** is a **CustomerEntity** object.</span></span> <span data-ttu-id="c5784-147">Określenie kluczy partycji i wiersza w zapytaniu jest hello najszybszy sposób tooretrieve pojedyncza jednostka z hello **tabeli** usługi.</span><span class="sxs-lookup"><span data-stu-id="c5784-147">Specifying both partition and row keys in a query is hello fastest way tooretrieve a single entity from hello **Table** service.</span></span>

    // Create a retrieve operation that takes a customer entity.
    TableOperation retrieveOperation = TableOperation.Retrieve<CustomerEntity>("Smith", "Ben");

    // Execute hello retrieve operation.
    TableResult retrievedResult = await peopleTable.ExecuteAsync(retrieveOperation);

    // Print hello phone number of hello result.
    if (retrievedResult.Result != null)
       Console.WriteLine(((CustomerEntity)retrievedResult.Result).PhoneNumber);
    else
       Console.WriteLine("hello phone number could not be retrieved.");

## <a name="delete-an-entity"></a><span data-ttu-id="c5784-148">Usuwanie jednostki</span><span class="sxs-lookup"><span data-stu-id="c5784-148">Delete an entity</span></span>
<span data-ttu-id="c5784-149">Po możesz znaleźć, można usunąć jednostki.</span><span class="sxs-lookup"><span data-stu-id="c5784-149">You can delete an entity after you find it.</span></span> <span data-ttu-id="c5784-150">Witaj następujący kod szuka jednostki klienta o nazwie "Ben Smith" i przypadku ich znalezienia, usunięcia go.</span><span class="sxs-lookup"><span data-stu-id="c5784-150">hello following code looks for a customer entity named "Ben Smith" and if it finds it, it deletes it.</span></span>

    // Create a retrieve operation that expects a customer entity.
    TableOperation retrieveOperation = TableOperation.Retrieve<CustomerEntity>("Smith", "Ben");

    // Execute hello operation.
    TableResult retrievedResult = peopleTable.Execute(retrieveOperation);

    // Assign hello result tooa CustomerEntity object.
    CustomerEntity deleteEntity = (CustomerEntity)retrievedResult.Result;

    // Create hello Delete TableOperation and then execute it.
    if (deleteEntity != null)
    {
       TableOperation deleteOperation = TableOperation.Delete(deleteEntity);

       // Execute hello operation.
       await peopleTable.ExecuteAsync(deleteOperation);

       Console.WriteLine("Entity deleted.");
    }

    else
       Console.WriteLine("Couldn't delete hello entity.");

## <a name="next-steps"></a><span data-ttu-id="c5784-151">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="c5784-151">Next steps</span></span>
[!INCLUDE [vs-storage-dotnet-tables-next-steps](../../includes/vs-storage-dotnet-tables-next-steps.md)]

