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
# <a name="how-tooget-started-with-azure-table-storage-and-visual-studio-connected-services"></a>Jak tooget wprowadzenie do magazynu tabel Azure i programu Visual Studio podłączonych usług
[!INCLUDE [storage-try-azure-tools-tables](../../includes/storage-try-azure-tools-tables.md)]

## <a name="overview"></a>Omówienie
W tym artykule opisano sposób uzyskać uruchomiony przy użyciu tabel Azure hello magazynu w programie Visual Studio po utworzony lub odwołanie do konta magazynu Azure w projekcie platformy ASP.NET Core za pomocą programu Visual Studio **dodać usług połączonych** okna dialogowego.

Usługa Azure Table storage Hello umożliwia toostore dużych ilości danych strukturalnych. Usługa Hello jest magazynem danych NoSQL, który przyjmuje uwierzytelnione wywołania z wewnątrz, jak i poza hello chmury Azure. Tabele Azure idealnie nadają się do przechowywania strukturalnych danych nierelacyjnych.

Witaj **dodać usług połączonych** operacji instaluje hello odpowiednie NuGet pakiety tooaccess magazynu Azure w projekcie i dodaje hello parametry połączenia dla hello magazynu konta tooyour pliki konfiguracji projektu.

Aby uzyskać więcej ogólnych informacji o korzystaniu z magazynem tabel Azure, zobacz [Rozpoczynanie pracy z magazynem tabel Azure przy użyciu platformy .NET](../storage/storage-dotnet-how-to-use-tables.md).

tooget uruchomiona, należy najpierw toocreate tabeli na koncie magazynu. Poniżej opisano sposób toocreate Azure tabeli w kodzie. Również pokażemy ci jak tabela podstawowa tooperform i jednostki operacje, takie jak dodawanie, modyfikowanie, Odczyt i odczytywania tabeli jednostek. Przykłady Hello są napisane w języku C\# kodu i użyć hello biblioteki klienta magazynu Azure dla platformy .NET.

**Uwaga** — niektóre hello interfejsów API, które wykonywania wywołań limit magazynu tooAzure w ASP.NET Core są asynchroniczne. Zobacz [programowanie asynchroniczne z Async i Await](http://msdn.microsoft.com/library/hh191443.aspx) Aby uzyskać więcej informacji. Poniższy kod Hello przyjęto założenie, że są używane metody programowania asynchronicznego.

## <a name="access-tables-in-code"></a>Dostęp do tabel w kodzie
tabele tooaccess w projektach platformy ASP.NET Core, należy hello tooinclude następujące pliki źródłowe tooany C# elementów, które uzyskują dostęp do magazynu tabel platformy Azure.

1. Upewnij się, że deklaracje przestrzeni nazw hello u góry pliku hello C# hello Uwzględnij je **przy użyciu** instrukcje.
   
        using Microsoft.Framework.Configuration;
        using Microsoft.WindowsAzure.Storage;
        using Microsoft.WindowsAzure.Storage.Table;
        using System.Threading.Tasks;
        using LogLevel = Microsoft.Framework.Logging.LogLevel;
2. Pobierz **CloudStorageAccount** obiekt, który reprezentuje informacje o koncie magazynu. Witaj Użyj następującego kodu tooget hello parametry połączenia magazynu, a informacje o koncie magazynu z konfiguracji usługi Azure hello.
   
        CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
            CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
   
    **Uwaga** -korzystać ze wszystkich hello powyżej kodu przed kodem hello w hello następujące przykłady.
3. Pobierz **CloudTableClient** obiekt tooreference hello tabeli obiektów na koncie magazynu.  
   
        // Create hello table client.
        CloudTableClient tableClient = storageAccount.CreateCloudTableClient();
4. Pobierz **CloudTable** odwoływać się do obiektu tooreference określonej tabeli i jednostek.
   
        // Get a reference tooa table named "peopleTable"
        CloudTable table = tableClient.GetTableReference("peopleTable");

## <a name="create-a-table-in-code"></a>Utwórz tabelę w kodzie
Witaj toocreate tabeli platformy Azure, po prostu dodaj wywołanie za**CreateIfNotExistsAsync()**.

    // Create hello CloudTable if it does not exist
    await table.CreateIfNotExistsAsync();

## <a name="add-an-entity-tooa-table"></a>Dodaj tabelę tooa jednostki
tooadd tabeli tooa jednostki, Utwórz klasę, która definiuje właściwości hello jednostki. Witaj poniższy kod definiuje klasę jednostki nazywane **CustomerEntity** imienia klienta jako hello klucz wiersza i nazwiska jako klucza partycji hello tekst hello zastosowań.

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

Operacje tabeli obejmujące jednostki są wykonywane przy użyciu hello **CloudTable** obiekt został utworzony we wcześniejszej części "Dostęp do tabel w kodzie." Witaj **TableOperation** obiekt reprezentuje toobe operacji hello gotowe. Witaj, jak po przedstawia przykładowy kod toocreate **CloudTable** obiektu i **CustomerEntity** obiektu. Operacja hello tooprepare, **TableOperation** utworzeniu tooinsert powitania klienta jednostki do tabeli hello. Na koniec operacji hello jest wykonywana przez wywołanie CloudTable.ExecuteAsync.

    // Create a new customer entity.
    CustomerEntity customer1 = new CustomerEntity("Harp", "Walter");
    customer1.Email = "Walter@contoso.com";
    customer1.PhoneNumber = "425-555-0101";

    // Create hello TableOperation that inserts hello customer entity.
    TableOperation insertOperation = TableOperation.Insert(customer1);

    // Execute hello insert operation.
    await peopleTable.ExecuteAsync(insertOperation);

## <a name="insert-a-batch-of-entities"></a>Zbiorcze wstawianie jednostek
Wiele jednostek można wstawiać do tabeli w operacji zapisu pojedynczego. Witaj poniższy przykład kodu tworzy dwa obiekty jednostki ("Jan Kowalski" i "Ben Smith"), dodaje je tooa **TableBatchOperation** obiektu przy użyciu hello **Wstaw** metody, a następnie uruchamia działanie hello wywoływanie CloudTable.ExecuteBatchAsync.

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

## <a name="get-all-of-hello-entities-in-a-partition"></a>Pobierz wszystkie hello jednostek w partycji
tooquery tabeli dla wszystkich hello jednostek w partycji, użyj **TableQuery** obiektu. Witaj poniższy przykład kodu Określa filtr jednostek, gdzie "Smith" jest hello klucza partycji. W tym przykładzie drukowane hello pola każdej jednostki w konsoli toohello wyników zapytania hello.

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

## <a name="get-a-single-entity"></a>Pobierz pojedynczy element
Tooget kwerendy można pisać w jednej, określonej jednostki. Witaj poniższy kod używa **TableOperation** obiekt toospecify klienta o nazwie "Ben Smith". Ta metoda zwraca tylko jedną jednostkę zamiast kolekcji i hello zwrócił wartość w **TableResult.Result** jest **CustomerEntity** obiektu. Określenie kluczy partycji i wiersza w zapytaniu jest hello najszybszy sposób tooretrieve pojedyncza jednostka z hello **tabeli** usługi.

    // Create a retrieve operation that takes a customer entity.
    TableOperation retrieveOperation = TableOperation.Retrieve<CustomerEntity>("Smith", "Ben");

    // Execute hello retrieve operation.
    TableResult retrievedResult = await peopleTable.ExecuteAsync(retrieveOperation);

    // Print hello phone number of hello result.
    if (retrievedResult.Result != null)
       Console.WriteLine(((CustomerEntity)retrievedResult.Result).PhoneNumber);
    else
       Console.WriteLine("hello phone number could not be retrieved.");

## <a name="delete-an-entity"></a>Usuwanie jednostki
Po możesz znaleźć, można usunąć jednostki. Witaj następujący kod szuka jednostki klienta o nazwie "Ben Smith" i przypadku ich znalezienia, usunięcia go.

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

## <a name="next-steps"></a>Następne kroki
[!INCLUDE [vs-storage-dotnet-tables-next-steps](../../includes/vs-storage-dotnet-tables-next-steps.md)]

