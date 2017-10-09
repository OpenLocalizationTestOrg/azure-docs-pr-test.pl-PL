---
title: "aaaGet pracy z magazynem tabel i Visual Studio podłączonych usług (usługi w chmurze) | Dokumentacja firmy Microsoft"
description: "Jak tooget pracy z magazynem tabel Azure w projektu usługi w chmurze w programie Visual Studio, po łączenie tooa konto magazynu przy użyciu programu Visual Studio połączenia usługi"
services: storage
documentationcenter: 
author: kraigb
manager: ghogen
editor: 
ms.assetid: a3a11ed8-ba7f-4193-912b-e555f5b72184
ms.service: storage
ms.workload: web
ms.tgt_pltfrm: vs-getting-started
ms.devlang: na
ms.topic: article
ms.date: 12/02/2016
ms.author: kraigb
ms.openlocfilehash: 36da6ed4a12a3595e7234482e3040ecee8c33b8a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="getting-started-with-azure-table-storage-and-visual-studio-connected-services-cloud-services-projects"></a><span data-ttu-id="fe085-103">Wprowadzenie do korzystania z magazynu tabel platformy Azure i programu Visual Studio połączone usługi (usług w chmurze projekty)</span><span class="sxs-lookup"><span data-stu-id="fe085-103">Getting started with Azure table storage and Visual Studio connected services (cloud services projects)</span></span>
[!INCLUDE [storage-try-azure-tools-tables](../../includes/storage-try-azure-tools-tables.md)]

## <a name="overview"></a><span data-ttu-id="fe085-104">Omówienie</span><span class="sxs-lookup"><span data-stu-id="fe085-104">Overview</span></span>
<span data-ttu-id="fe085-105">W tym artykule opisano sposób uruchamiania przy użyciu magazynu tabel platformy Azure w programie Visual Studio po utworzony lub odwołanie do konta magazynu Azure w projekcie usługi w chmurze przy użyciu programu Visual Studio hello tooget **dodać usług połączonych** okna dialogowego .</span><span class="sxs-lookup"><span data-stu-id="fe085-105">This article describes how tooget started using Azure table storage in Visual Studio after you have created or referenced an Azure storage account in a cloud services project by using hello Visual Studio **Add Connected Services** dialog.</span></span> <span data-ttu-id="fe085-106">Witaj **dodać usług połączonych** operacji instaluje hello odpowiednie NuGet pakiety tooaccess magazynu Azure w projekcie i dodaje hello parametry połączenia dla hello magazynu konta tooyour pliki konfiguracji projektu.</span><span class="sxs-lookup"><span data-stu-id="fe085-106">hello **Add Connected Services** operation installs hello appropriate NuGet packages tooaccess Azure storage in your project and adds hello connection string for hello storage account tooyour project configuration files.</span></span>

<span data-ttu-id="fe085-107">Usługa Azure Table storage Hello umożliwia toostore dużych ilości danych strukturalnych.</span><span class="sxs-lookup"><span data-stu-id="fe085-107">hello Azure Table storage service enables you toostore large amounts of structured data.</span></span> <span data-ttu-id="fe085-108">Usługa Hello jest magazynem danych NoSQL, który przyjmuje uwierzytelnione wywołania z wewnątrz, jak i poza hello chmury Azure.</span><span class="sxs-lookup"><span data-stu-id="fe085-108">hello service is a NoSQL datastore that accepts authenticated calls from inside and outside hello Azure cloud.</span></span> <span data-ttu-id="fe085-109">Tabele Azure idealnie nadają się do przechowywania strukturalnych danych nierelacyjnych.</span><span class="sxs-lookup"><span data-stu-id="fe085-109">Azure tables are ideal for storing structured, non-relational data.</span></span>

<span data-ttu-id="fe085-110">tooget uruchomiona, należy najpierw toocreate tabeli na koncie magazynu.</span><span class="sxs-lookup"><span data-stu-id="fe085-110">tooget started, you first need toocreate a table in your storage account.</span></span> <span data-ttu-id="fe085-111">Pokażemy ci, jak tabela toocreate platformy Azure w kodzie, a także sposób tooperform tabeli podstawowej i jednostki operacje, takie jak dodawanie, modyfikowanie, Odczyt i odczytywania tabeli jednostek.</span><span class="sxs-lookup"><span data-stu-id="fe085-111">We'll show you how toocreate an Azure table in code, and also how tooperform basic table and entity operations, such as adding, modifying, reading and reading table entities.</span></span> <span data-ttu-id="fe085-112">Przykłady Hello są napisane w języku C\# kodu i użyć hello [biblioteki klienta usługi Magazyn Microsoft Azure dla platformy .NET](https://msdn.microsoft.com/library/azure/dn261237.aspx).</span><span class="sxs-lookup"><span data-stu-id="fe085-112">hello samples are written in C\# code and use hello [Microsoft Azure Storage client library for .NET](https://msdn.microsoft.com/library/azure/dn261237.aspx).</span></span>

<span data-ttu-id="fe085-113">**Uwaga:** niektóre hello interfejsów API, które wykonywania wywołań limit magazynu tooAzure są asynchroniczne.</span><span class="sxs-lookup"><span data-stu-id="fe085-113">**NOTE:** Some of hello APIs that perform calls out tooAzure storage are asynchronous.</span></span> <span data-ttu-id="fe085-114">Zobacz [programowanie asynchroniczne z Async i Await](http://msdn.microsoft.com/library/hh191443.aspx) Aby uzyskać więcej informacji.</span><span class="sxs-lookup"><span data-stu-id="fe085-114">See [Asynchronous programming with Async and Await](http://msdn.microsoft.com/library/hh191443.aspx) for more information.</span></span> <span data-ttu-id="fe085-115">Poniższy kod Hello przyjęto założenie, że są używane metody programowania asynchronicznego.</span><span class="sxs-lookup"><span data-stu-id="fe085-115">hello code below assumes async programming methods are being used.</span></span>

* <span data-ttu-id="fe085-116">Zobacz [Rozpoczynanie pracy z magazynem tabel Azure przy użyciu platformy .NET](../storage/storage-dotnet-how-to-use-tables.md) uzyskać więcej informacji o programowo manipulowanie tabel.</span><span class="sxs-lookup"><span data-stu-id="fe085-116">See [Get started with Azure Table storage using .NET](../storage/storage-dotnet-how-to-use-tables.md) for more information on programmatically manipulating tables.</span></span>
* <span data-ttu-id="fe085-117">Zobacz [dokumentacji magazynu](https://azure.microsoft.com/documentation/services/storage/) ogólne informacje na temat usługi Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="fe085-117">See [Storage documentation](https://azure.microsoft.com/documentation/services/storage/) for general information about Azure Storage.</span></span>
* <span data-ttu-id="fe085-118">Zobacz [dokumentacji usługi w chmurze](https://azure.microsoft.com/documentation/services/cloud-services/) ogólne informacje dotyczące usług w chmurze Azure.</span><span class="sxs-lookup"><span data-stu-id="fe085-118">See [Cloud Services documentation](https://azure.microsoft.com/documentation/services/cloud-services/) for general information about Azure cloud services.</span></span>
* <span data-ttu-id="fe085-119">Zobacz [ASP.NET](http://www.asp.net) Aby uzyskać więcej informacji na temat programowania aplikacji ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="fe085-119">See [ASP.NET](http://www.asp.net) for more information about programming ASP.NET applications.</span></span>

## <a name="access-tables-in-code"></a><span data-ttu-id="fe085-120">Dostęp do tabel w kodzie</span><span class="sxs-lookup"><span data-stu-id="fe085-120">Access tables in code</span></span>
<span data-ttu-id="fe085-121">tabele tooaccess w projekty usługi w chmurze, należy hello tooinclude następujące pliki źródłowe tooany C# elementów, które uzyskują dostęp do magazynu tabel platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="fe085-121">tooaccess tables in cloud service projects, you need tooinclude hello following items tooany C# source files that access Azure table storage.</span></span>

1. <span data-ttu-id="fe085-122">Upewnij się, że deklaracje przestrzeni nazw hello u góry pliku hello C# hello Uwzględnij je **przy użyciu** instrukcje.</span><span class="sxs-lookup"><span data-stu-id="fe085-122">Make sure hello namespace declarations at hello top of hello C# file include these **using** statements.</span></span>
   
        using Microsoft.Framework.Configuration;
        using Microsoft.WindowsAzure.Storage;
        using Microsoft.WindowsAzure.Storage.Table;
        using System.Threading.Tasks;
        using LogLevel = Microsoft.Framework.Logging.LogLevel;
2. <span data-ttu-id="fe085-123">Pobierz **CloudStorageAccount** obiekt, który reprezentuje informacje o koncie magazynu.</span><span class="sxs-lookup"><span data-stu-id="fe085-123">Get a **CloudStorageAccount** object that represents your storage account information.</span></span> <span data-ttu-id="fe085-124">Użyj następującego kodu tooget hello połączenia ciągu i przechowywania informacji o koncie magazynu z konfiguracji usługi Azure hello hello.</span><span class="sxs-lookup"><span data-stu-id="fe085-124">Use hello following code tooget hello storage connection string and storage account information from hello Azure service configuration.</span></span>
   
         CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
           CloudConfigurationManager.GetSetting("<storage account name>
         _AzureStorageConnectionString"));
   > [!NOTE]
   > <span data-ttu-id="fe085-125">Użyj wszystkich hello powyżej kodu przed kodem hello w hello następujące przykłady.</span><span class="sxs-lookup"><span data-stu-id="fe085-125">Use all of hello above code in front of hello code in hello following samples.</span></span>
   > 
   > 
3. <span data-ttu-id="fe085-126">Pobierz **CloudTableClient** obiekt tooreference hello tabeli obiektów na koncie magazynu.</span><span class="sxs-lookup"><span data-stu-id="fe085-126">Get a **CloudTableClient** object tooreference hello table objects in your storage account.</span></span>
   
         // Create hello table client.
         CloudTableClient tableClient = storageAccount.CreateCloudTableClient();
4. <span data-ttu-id="fe085-127">Pobierz **CloudTable** odwoływać się do obiektu tooreference określonej tabeli i jednostek.</span><span class="sxs-lookup"><span data-stu-id="fe085-127">Get a **CloudTable** reference object tooreference a specific table and entities.</span></span>
   
        // Get a reference tooa table named "peopleTable".
        CloudTable peopleTable = tableClient.GetTableReference("peopleTable");

## <a name="create-a-table-in-code"></a><span data-ttu-id="fe085-128">Utwórz tabelę w kodzie</span><span class="sxs-lookup"><span data-stu-id="fe085-128">Create a table in code</span></span>
<span data-ttu-id="fe085-129">Witaj toocreate tabeli platformy Azure, po prostu dodaj wywołanie za**CreateIfNotExistsAsync** toohello po uzyskaniu **CloudTable** obiekt zgodnie z opisem w sekcji "Dostęp do tabel w kodzie" hello.</span><span class="sxs-lookup"><span data-stu-id="fe085-129">toocreate hello Azure table, just add a call too**CreateIfNotExistsAsync** toohello after you get a **CloudTable** object as described in hello "Access tables in code" section.</span></span>

    // Create hello CloudTable if it does not exist.
    await peopleTable.CreateIfNotExistsAsync();

## <a name="add-an-entity-tooa-table"></a><span data-ttu-id="fe085-130">Dodaj tabelę tooa jednostki</span><span class="sxs-lookup"><span data-stu-id="fe085-130">Add an entity tooa table</span></span>
<span data-ttu-id="fe085-131">tooadd tabeli tooa jednostki, Utwórz klasę, która definiuje właściwości hello jednostki.</span><span class="sxs-lookup"><span data-stu-id="fe085-131">tooadd an entity tooa table, create a class that defines hello properties of your entity.</span></span> <span data-ttu-id="fe085-132">Witaj poniższy kod definiuje klasę jednostki nazywane **CustomerEntity** imienia klienta jako klucza wiersza hello i hello nazwiska jako klucza partycji hello tekst hello zastosowań.</span><span class="sxs-lookup"><span data-stu-id="fe085-132">hello following code defines an entity class called **CustomerEntity** that uses hello customer's first name as hello row key and hello last name as hello partition key.</span></span>

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

<span data-ttu-id="fe085-133">Operacje tabeli obejmujące jednostki są wykonywane przy użyciu hello **CloudTable** obiekt, który został utworzony we wcześniejszej części "Dostęp do tabel w kodzie."</span><span class="sxs-lookup"><span data-stu-id="fe085-133">Table operations involving entities are done using hello **CloudTable** object that you created earlier in "Access tables in code."</span></span> <span data-ttu-id="fe085-134">Witaj **TableOperation** obiekt reprezentuje toobe operacji hello gotowe.</span><span class="sxs-lookup"><span data-stu-id="fe085-134">hello **TableOperation** object represents hello operation toobe done.</span></span> <span data-ttu-id="fe085-135">Witaj, jak po przedstawia przykładowy kod toocreate **CloudTable** obiektu i **CustomerEntity** obiektu.</span><span class="sxs-lookup"><span data-stu-id="fe085-135">hello following code example shows how toocreate a **CloudTable** object and a **CustomerEntity** object.</span></span> <span data-ttu-id="fe085-136">Operacja hello tooprepare, **TableOperation** utworzeniu tooinsert powitania klienta jednostki do tabeli hello.</span><span class="sxs-lookup"><span data-stu-id="fe085-136">tooprepare hello operation, a **TableOperation** is created tooinsert hello customer entity into hello table.</span></span> <span data-ttu-id="fe085-137">Na koniec operacji hello jest wykonywana przez wywołanie **CloudTable.ExecuteAsync**.</span><span class="sxs-lookup"><span data-stu-id="fe085-137">Finally, hello operation is executed by calling **CloudTable.ExecuteAsync**.</span></span>

    // Create a new customer entity.
    CustomerEntity customer1 = new CustomerEntity("Harp", "Walter");
    customer1.Email = "Walter@contoso.com";
    customer1.PhoneNumber = "425-555-0101";

    // Create hello TableOperation that inserts hello customer entity.
    TableOperation insertOperation = TableOperation.Insert(customer1);

    // Execute hello insert operation.
    await peopleTable.ExecuteAsync(insertOperation);


## <a name="insert-a-batch-of-entities"></a><span data-ttu-id="fe085-138">Zbiorcze wstawianie jednostek</span><span class="sxs-lookup"><span data-stu-id="fe085-138">Insert a batch of entities</span></span>
<span data-ttu-id="fe085-139">Wiele jednostek można wstawiać do tabeli w operacji zapisu pojedynczego.</span><span class="sxs-lookup"><span data-stu-id="fe085-139">You can insert multiple entities into a table in a single write operation.</span></span> <span data-ttu-id="fe085-140">Witaj poniższy przykład kodu tworzy dwa obiekty jednostki ("Jan Kowalski" i "Ben Smith"), dodaje je tooa **TableBatchOperation** obiekt przy użyciu hello metody Insert, a następnie uruchamia hello operacji przez wywołanie metody  **CloudTable.ExecuteBatchAsync**.</span><span class="sxs-lookup"><span data-stu-id="fe085-140">hello following code example creates two entity objects ("Jeff Smith" and "Ben Smith"), adds them tooa **TableBatchOperation** object using hello Insert method, and then starts hello operation by calling **CloudTable.ExecuteBatchAsync**.</span></span>

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

## <a name="get-all-of-hello-entities-in-a-partition"></a><span data-ttu-id="fe085-141">Pobierz wszystkie hello jednostek w partycji</span><span class="sxs-lookup"><span data-stu-id="fe085-141">Get all of hello entities in a partition</span></span>
<span data-ttu-id="fe085-142">tooquery tabeli dla wszystkich hello jednostek w partycji, użyj **TableQuery** obiektu.</span><span class="sxs-lookup"><span data-stu-id="fe085-142">tooquery a table for all of hello entities in a partition, use a **TableQuery** object.</span></span> <span data-ttu-id="fe085-143">Witaj poniższy przykład kodu Określa filtr jednostek, gdzie "Smith" jest hello klucza partycji.</span><span class="sxs-lookup"><span data-stu-id="fe085-143">hello following code example specifies a filter for entities where 'Smith' is hello partition key.</span></span> <span data-ttu-id="fe085-144">W tym przykładzie drukowane hello pola każdej jednostki w konsoli toohello wyników zapytania hello.</span><span class="sxs-lookup"><span data-stu-id="fe085-144">This example prints hello fields of each entity in hello query results toohello console.</span></span>

    // Construct hello query operation for all customer entities where PartitionKey="Smith".
    TableQuery<CustomerEntity> query = new TableQuery<CustomerEntity>()
        .Where(TableQuery.GenerateFilterCondition("PartitionKey", QueryComparisons.Equal, "Smith"));

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

    return View();


## <a name="get-a-single-entity"></a><span data-ttu-id="fe085-145">Pobierz pojedynczy element</span><span class="sxs-lookup"><span data-stu-id="fe085-145">Get a single entity</span></span>
<span data-ttu-id="fe085-146">Tooget kwerendy można pisać w jednej, określonej jednostki.</span><span class="sxs-lookup"><span data-stu-id="fe085-146">You can write a query tooget a single, specific entity.</span></span> <span data-ttu-id="fe085-147">Witaj poniższy kod używa **TableOperation** obiekt toospecify klienta o nazwie "Ben Smith".</span><span class="sxs-lookup"><span data-stu-id="fe085-147">hello following code uses a **TableOperation** object toospecify a customer named 'Ben Smith'.</span></span> <span data-ttu-id="fe085-148">Ta metoda zwraca tylko jedną jednostkę zamiast kolekcji i hello zwrócił wartość w **TableResult.Result** jest **CustomerEntity** obiektu.</span><span class="sxs-lookup"><span data-stu-id="fe085-148">This method returns just one entity, rather than a collection, and hello returned value in **TableResult.Result** is a **CustomerEntity** object.</span></span> <span data-ttu-id="fe085-149">Określenie kluczy partycji i wiersza w zapytaniu jest hello najszybszy sposób tooretrieve pojedyncza jednostka z hello **tabeli** usługi.</span><span class="sxs-lookup"><span data-stu-id="fe085-149">Specifying both partition and row keys in a query is hello fastest way tooretrieve a single entity from hello **Table** service.</span></span>

    // Create a retrieve operation that takes a customer entity.
    TableOperation retrieveOperation = TableOperation.Retrieve<CustomerEntity>("Smith", "Ben");

    // Execute hello retrieve operation.
    TableResult retrievedResult = await peopleTable.ExecuteAsync(retrieveOperation);

    // Print hello phone number of hello result.
    if (retrievedResult.Result != null)
       Console.WriteLine(((CustomerEntity)retrievedResult.Result).PhoneNumber);
    else
       Console.WriteLine("hello phone number could not be retrieved.");

## <a name="delete-an-entity"></a><span data-ttu-id="fe085-150">Usuwanie jednostki</span><span class="sxs-lookup"><span data-stu-id="fe085-150">Delete an entity</span></span>
<span data-ttu-id="fe085-151">Po możesz znaleźć, można usunąć jednostki.</span><span class="sxs-lookup"><span data-stu-id="fe085-151">You can delete an entity after you find it.</span></span> <span data-ttu-id="fe085-152">Witaj następujący kod szuka jednostki klienta o nazwie "Ben Smith", i przypadku ich znalezienia, usunięcia go.</span><span class="sxs-lookup"><span data-stu-id="fe085-152">hello following code looks for a customer entity named "Ben Smith", and if it finds it, it deletes it.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="fe085-153">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="fe085-153">Next steps</span></span>
[!INCLUDE [vs-storage-dotnet-tables-next-steps](../../includes/vs-storage-dotnet-tables-next-steps.md)]

