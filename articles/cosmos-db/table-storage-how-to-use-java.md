---
title: "Jak używać magazynu tabel w języku Java | Dokumentacja firmy Microsoft"
description: "Przechowywanie danych strukturalnych w chmurze za pomocą Magazynu tabel Azure, magazyn danych NoSQL."
services: cosmos-db
documentationcenter: java
author: mimig1
manager: jhubbard
editor: tysonn
ms.assetid: 45145189-e67f-4ca6-b15d-43af7bfd3f97
ms.service: cosmos-db
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: Java
ms.topic: article
ms.date: 12/08/2016
ms.author: mimig
ms.openlocfilehash: 7f92b1e14a514e9eda39f7ca94f63fc761dfdf41
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
# <a name="how-to-use-table-storage-from-java"></a><span data-ttu-id="05188-103">Jak używać Magazynu tabel w języku Java</span><span class="sxs-lookup"><span data-stu-id="05188-103">How to use Table storage from Java</span></span>
[!INCLUDE [storage-selector-table-include](../../includes/storage-selector-table-include.md)]
[!INCLUDE [storage-table-cosmos-db-langsoon-tip-include](../../includes/storage-table-cosmos-db-langsoon-tip-include.md)]

## <a name="overview"></a><span data-ttu-id="05188-104">Omówienie</span><span class="sxs-lookup"><span data-stu-id="05188-104">Overview</span></span>
<span data-ttu-id="05188-105">W tym przewodniku opisano sposób wykonywania typowych scenariuszy przy użyciu usługi Magazyn tabel Azure.</span><span class="sxs-lookup"><span data-stu-id="05188-105">This guide will show you how to perform common scenarios using the Azure Table storage service.</span></span> <span data-ttu-id="05188-106">Przykłady są napisane w języku Java i użyj [Azure Storage SDK for Java][Azure Storage SDK for Java].</span><span class="sxs-lookup"><span data-stu-id="05188-106">The samples are written in Java and use the [Azure Storage SDK for Java][Azure Storage SDK for Java].</span></span> <span data-ttu-id="05188-107">Omówione scenariusze obejmują **tworzenie**, **wyświetlania**, i **usuwanie** tabel, a także **wstawianie**, **zapytań**, **modyfikowanie**, i **usuwanie** jednostek w tabeli.</span><span class="sxs-lookup"><span data-stu-id="05188-107">The scenarios covered include **creating**, **listing**, and **deleting** tables, as well as **inserting**, **querying**, **modifying**, and **deleting** entities in a table.</span></span> <span data-ttu-id="05188-108">Aby uzyskać więcej informacji o tabelach zobacz [następne kroki](#Next-Steps) sekcji.</span><span class="sxs-lookup"><span data-stu-id="05188-108">For more information on tables, see the [Next steps](#Next-Steps) section.</span></span>

<span data-ttu-id="05188-109">Uwaga: Zestaw SDK jest dostępny dla deweloperów, którzy korzystają z usługi Azure Storage na urządzeniach z systemem Android.</span><span class="sxs-lookup"><span data-stu-id="05188-109">Note: An SDK is available for developers who are using Azure Storage on Android devices.</span></span> <span data-ttu-id="05188-110">Aby uzyskać więcej informacji, zobacz [zestawu SDK usługi Magazyn Azure dla systemu Android][Azure Storage SDK for Android].</span><span class="sxs-lookup"><span data-stu-id="05188-110">For more information, see the [Azure Storage SDK for Android][Azure Storage SDK for Android].</span></span>

[!INCLUDE [storage-table-concepts-include](../../includes/storage-table-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/storage-create-account-include.md)]

## <a name="create-a-java-application"></a><span data-ttu-id="05188-111">Tworzenie aplikacji Java</span><span class="sxs-lookup"><span data-stu-id="05188-111">Create a Java application</span></span>
<span data-ttu-id="05188-112">W tym przewodniku użyje funkcji magazynu, które mogą być uruchamiane w ramach aplikacji Java lokalnie lub w kodzie działających w roli sieci web lub roli proces roboczy na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="05188-112">In this guide, you will use storage features which can be run within a Java application locally, or in code running within a web role or worker role in Azure.</span></span>

<span data-ttu-id="05188-113">Aby to zrobić, należy zainstalować zestaw Java Development Kit (JDK) i utworzyć konta magazynu platformy Azure w ramach subskrypcji platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="05188-113">To do so, you will need to install the Java Development Kit (JDK) and create an Azure storage account in your Azure subscription.</span></span> <span data-ttu-id="05188-114">Po zostało to zrobione, należy sprawdzić, czy platformie programistycznej spełnia minimalne wymagania i zależności, które są wymienione w [Azure Storage SDK for Java] [ Azure Storage SDK for Java] repozytorium w witrynie GitHub.</span><span class="sxs-lookup"><span data-stu-id="05188-114">Once you have done so, you will need to verify that your development system meets the minimum requirements and dependencies which are listed in the [Azure Storage SDK for Java][Azure Storage SDK for Java] repository on GitHub.</span></span> <span data-ttu-id="05188-115">Jeżeli system spełnia te wymagania, należy wykonać instrukcje dotyczące pobierania i instalowania biblioteki magazynu Azure dla języka Java w systemie z tego repozytorium.</span><span class="sxs-lookup"><span data-stu-id="05188-115">If your system meets those requirements, you can follow the instructions for downloading and installing the Azure Storage Libraries for Java on your system from that repository.</span></span> <span data-ttu-id="05188-116">Po wykonaniu tych zadań, można utworzyć aplikacji Java, który używa przykłady w tym artykule.</span><span class="sxs-lookup"><span data-stu-id="05188-116">Once you have completed those tasks, you will be able to create a Java application which uses the examples in this article.</span></span>

## <a name="configure-your-application-to-access-table-storage"></a><span data-ttu-id="05188-117">Konfigurowanie aplikacji na dostęp do magazynu tabel</span><span class="sxs-lookup"><span data-stu-id="05188-117">Configure your application to access table storage</span></span>
<span data-ttu-id="05188-118">Dodaj następujące instrukcje import u góry pliku języka Java, której chcesz użyć interfejsów API magazynu Microsoft Azure na dostęp do tabel:</span><span class="sxs-lookup"><span data-stu-id="05188-118">Add the following import statements to the top of the Java file where you want to use Microsoft Azure storage APIs to access tables:</span></span>

```java
// Include the following imports to use table APIs
import com.microsoft.azure.storage.*;
import com.microsoft.azure.storage.table.*;
import com.microsoft.azure.storage.table.TableQuery.*;
```

## <a name="set-up-an-azure-storage-connection-string"></a><span data-ttu-id="05188-119">Konfigurowanie parametrów połączenia usługi Azure storage</span><span class="sxs-lookup"><span data-stu-id="05188-119">Set up an Azure storage connection string</span></span>
<span data-ttu-id="05188-120">Klienta usługi Azure storage używa parametrów połączenia magazynu do przechowywania punktów końcowych i poświadczeń do uzyskiwania dostępu do danych usługi zarządzania.</span><span class="sxs-lookup"><span data-stu-id="05188-120">An Azure storage client uses a storage connection string to store endpoints and credentials for accessing data management services.</span></span> <span data-ttu-id="05188-121">Podczas uruchamiania w aplikacji klienckiej, należy podać parametry połączenia magazynu w następującym formacie, przy użyciu nazwy konta magazynu i podstawowy klucz dostępu dla konta magazynu na liście [portalu Azure](https://portal.azure.com) dla *AccountName* i *AccountKey* wartości.</span><span class="sxs-lookup"><span data-stu-id="05188-121">When running in a client application, you must provide the storage connection string in the following format, using the name of your storage account and the Primary access key for the storage account listed in the [Azure portal](https://portal.azure.com) for the *AccountName* and *AccountKey* values.</span></span> <span data-ttu-id="05188-122">Ten przykład przedstawia, jak można zadeklarować pola statycznego do przechowywania parametrów połączenia:</span><span class="sxs-lookup"><span data-stu-id="05188-122">This example shows how you can declare a static field to hold the connection string:</span></span>

```java
// Define the connection-string with your values.
public static final String storageConnectionString =
    "DefaultEndpointsProtocol=http;" +
    "AccountName=your_storage_account;" +
    "AccountKey=your_storage_account_key";
```

<span data-ttu-id="05188-123">W aplikacji działającej w ramach roli w systemie Microsoft Azure, te parametry mogą być przechowywane w pliku konfiguracji usługi *pliku ServiceConfiguration.cscfg*i jest dostępny w wyniku wywołania **RoleEnvironment.getConfigurationSettings** metody.</span><span class="sxs-lookup"><span data-stu-id="05188-123">In an application running within a role in Microsoft Azure, this string can be stored in the service configuration file, *ServiceConfiguration.cscfg*, and can be accessed with a call to the **RoleEnvironment.getConfigurationSettings** method.</span></span> <span data-ttu-id="05188-124">Oto przykład pobierania parametrów połączenia z **ustawienie** elementu o nazwie *StorageConnectionString* w pliku konfiguracji usługi:</span><span class="sxs-lookup"><span data-stu-id="05188-124">Here's an example of getting the connection string from a **Setting** element named *StorageConnectionString* in the service configuration file:</span></span>

```java
// Retrieve storage account from connection-string.
String storageConnectionString =
    RoleEnvironment.getConfigurationSettings().get("StorageConnectionString");
```

<span data-ttu-id="05188-125">Poniższe przykłady założono użycie jednej z tych dwóch metod można pobrać parametry połączenia magazynu.</span><span class="sxs-lookup"><span data-stu-id="05188-125">The following samples assume that you have used one of these two methods to get the storage connection string.</span></span>

## <a name="how-to-create-a-table"></a><span data-ttu-id="05188-126">Porady: Tworzenie tabeli</span><span class="sxs-lookup"><span data-stu-id="05188-126">How to: Create a table</span></span>
<span data-ttu-id="05188-127">A **CloudTableClient** obiektu pozwala pobierać obiekty odwołania do tabel i jednostek.</span><span class="sxs-lookup"><span data-stu-id="05188-127">A **CloudTableClient** object lets you get reference objects for tables and entities.</span></span> <span data-ttu-id="05188-128">Poniższy kod tworzy **CloudTableClient** obiektu i używa go do tworzenia nowego **CloudTable** obiekt, który reprezentuje tabeli o nazwie "osoby".</span><span class="sxs-lookup"><span data-stu-id="05188-128">The following code creates a **CloudTableClient** object and uses it to create a new **CloudTable** object which represents a table named "people".</span></span> <span data-ttu-id="05188-129">(Uwaga: istnieją dodatkowe sposoby tworzenia **CloudStorageAccount** obiektów; Aby uzyskać więcej informacji, zobacz **CloudStorageAccount** w [odwołania do zestawu SDK klienta magazynu Azure].)</span><span class="sxs-lookup"><span data-stu-id="05188-129">(Note: There are additional ways to create **CloudStorageAccount** objects; for more information, see **CloudStorageAccount** in the [Azure Storage Client SDK Reference].)</span></span>

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount =
        CloudStorageAccount.parse(storageConnectionString);

    // Create the table client.
    CloudTableClient tableClient = storageAccount.createCloudTableClient();

    // Create the table if it doesn't exist.
    String tableName = "people";
    CloudTable cloudTable = tableClient.getTableReference(tableName);
    cloudTable.createIfNotExists();
}
catch (Exception e)
{
    // Output the stack trace.
    e.printStackTrace();
}
```

## <a name="how-to-list-the-tables"></a><span data-ttu-id="05188-130">Porady: Lista tabel</span><span class="sxs-lookup"><span data-stu-id="05188-130">How to: List the tables</span></span>
<span data-ttu-id="05188-131">Aby uzyskać listę tabel, należy wywołać **CloudTableClient.listTables()** metoda pobierania iterable listę nazw tabel.</span><span class="sxs-lookup"><span data-stu-id="05188-131">To get a list of tables, call the **CloudTableClient.listTables()** method to retrieve an iterable list of table names.</span></span>

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount =
        CloudStorageAccount.parse(storageConnectionString);

    // Create the table client.
    CloudTableClient tableClient = storageAccount.createCloudTableClient();

    // Loop through the collection of table names.
    for (String table : tableClient.listTables())
    {
        // Output each table name.
        System.out.println(table);
    }
}
catch (Exception e)
{
    // Output the stack trace.
    e.printStackTrace();
}
```

## <a name="how-to-add-an-entity-to-a-table"></a><span data-ttu-id="05188-132">Porady: Dodawanie jednostki do tabeli</span><span class="sxs-lookup"><span data-stu-id="05188-132">How to: Add an entity to a table</span></span>
<span data-ttu-id="05188-133">Jednostki są mapowane do obiektów języka Java przy użyciu niestandardowej klasy implementacja **TableEntity**.</span><span class="sxs-lookup"><span data-stu-id="05188-133">Entities map to Java objects using a custom class implementing **TableEntity**.</span></span> <span data-ttu-id="05188-134">Dla wygody **TableServiceEntity** klasa implementuje **TableEntity** i używa odbicia do mapowania właściwości do metody pobierającej i ustawiającej o nazwie właściwości.</span><span class="sxs-lookup"><span data-stu-id="05188-134">For convenience, the **TableServiceEntity** class implements **TableEntity** and uses reflection to map properties to getter and setter methods named for the properties.</span></span> <span data-ttu-id="05188-135">Aby dodać jednostkę do tabeli, należy najpierw utworzyć klasę, która definiuje właściwości jednostki.</span><span class="sxs-lookup"><span data-stu-id="05188-135">To add an entity to a table, first create a class that defines the properties of your entity.</span></span> <span data-ttu-id="05188-136">Poniższy kod definiuje klasę jednostki, która używa imienia klienta jako klucza wiersza i nazwiska jako klucza partycji.</span><span class="sxs-lookup"><span data-stu-id="05188-136">The following code defines an entity class which uses the customer's first name as the row key, and last name as the partition key.</span></span> <span data-ttu-id="05188-137">Razem klucz partycji i klucz wiersza jednostki jednoznacznie identyfikują jednostkę w tabeli.</span><span class="sxs-lookup"><span data-stu-id="05188-137">Together, an entity's partition and row key uniquely identify the entity in the table.</span></span> <span data-ttu-id="05188-138">Jednostki z tym samym kluczem partycji mogą być przeszukiwane szybciej niż jednostki o różnych kluczach partycji.</span><span class="sxs-lookup"><span data-stu-id="05188-138">Entities with the same partition key can be queried faster than those with different partition keys.</span></span>

```java
public class CustomerEntity extends TableServiceEntity {
    public CustomerEntity(String lastName, String firstName) {
        this.partitionKey = lastName;
        this.rowKey = firstName;
    }

    public CustomerEntity() { }

    String email;
    String phoneNumber;

    public String getEmail() {
        return this.email;
    }

    public void setEmail(String email) {
        this.email = email;
    }

    public String getPhoneNumber() {
        return this.phoneNumber;
    }

    public void setPhoneNumber(String phoneNumber) {
        this.phoneNumber = phoneNumber;
    }
}
```

<span data-ttu-id="05188-139">Operacje tabeli obejmujące jednostki wymagają **TableOperation** obiektu.</span><span class="sxs-lookup"><span data-stu-id="05188-139">Table operations involving entities require a **TableOperation** object.</span></span> <span data-ttu-id="05188-140">Ten obiekt definiuje operacji wykonywanych w ramach jednostki, które mogą być wykonywane przez **CloudTable** obiektu.</span><span class="sxs-lookup"><span data-stu-id="05188-140">This object defines the operation to be performed on an entity, which can be executed with a **CloudTable** object.</span></span> <span data-ttu-id="05188-141">Poniższy kod tworzy nowe wystąpienie klasy **CustomerEntity** klasy z niektóre dane klienta mają być przechowywane.</span><span class="sxs-lookup"><span data-stu-id="05188-141">The following code creates a new instance of the **CustomerEntity** class with some customer data to be stored.</span></span> <span data-ttu-id="05188-142">Kod wywołuje dalej **TableOperation.insertOrReplace** utworzyć **TableOperation** obiekt do wstawiania jednostek do tabeli i kojarzy nowe **CustomerEntity** z nim.</span><span class="sxs-lookup"><span data-stu-id="05188-142">The code next calls **TableOperation.insertOrReplace** to create a **TableOperation** object to insert an entity into a table, and associates the new **CustomerEntity** with it.</span></span> <span data-ttu-id="05188-143">Na koniec kod wywołuje **wykonania** metoda **CloudTable** obiektu, określając w tabeli "osoby" i nowych **TableOperation**, który następnie wysyła żądanie do usługi magazynu, aby wstawić nową jednostkę klienta do tabeli "osoby", lub Zastąp jednostki, jeśli już istnieje.</span><span class="sxs-lookup"><span data-stu-id="05188-143">Finally, the code calls the **execute** method on the **CloudTable** object, specifying the "people" table and the new **TableOperation**, which then sends a request to the storage service to insert the new customer entity into the "people" table, or replace the entity if it already exists.</span></span>

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount =
        CloudStorageAccount.parse(storageConnectionString);

    // Create the table client.
    CloudTableClient tableClient = storageAccount.createCloudTableClient();

    // Create a cloud table object for the table.
    CloudTable cloudTable = tableClient.getTableReference("people");

    // Create a new customer entity.
    CustomerEntity customer1 = new CustomerEntity("Harp", "Walter");
    customer1.setEmail("Walter@contoso.com");
    customer1.setPhoneNumber("425-555-0101");

    // Create an operation to add the new customer to the people table.
    TableOperation insertCustomer1 = TableOperation.insertOrReplace(customer1);

    // Submit the operation to the table service.
    cloudTable.execute(insertCustomer1);
}
catch (Exception e)
{
    // Output the stack trace.
    e.printStackTrace();
}
```

## <a name="how-to-insert-a-batch-of-entities"></a><span data-ttu-id="05188-144">Porady: wstawianie partię jednostek</span><span class="sxs-lookup"><span data-stu-id="05188-144">How to: Insert a batch of entities</span></span>
<span data-ttu-id="05188-145">Możesz wstawić partię jednostek do usługi tabel w jednej operacji zapisu.</span><span class="sxs-lookup"><span data-stu-id="05188-145">You can insert a batch of entities to the table service in one write operation.</span></span> <span data-ttu-id="05188-146">Poniższy kod tworzy **TableBatchOperation** obiekt, a następnie dodaje Wstaw trzy operacje do niego.</span><span class="sxs-lookup"><span data-stu-id="05188-146">The following code creates a **TableBatchOperation** object, then adds three insert operations to it.</span></span> <span data-ttu-id="05188-147">Każda operacja insert jest dodawany przez utworzenie nowego obiektu jednostki, jego wartości ustawienia, a następnie wywołując **Wstaw** metoda **TableBatchOperation** obiektu jednostki z nowej operacji insert.</span><span class="sxs-lookup"><span data-stu-id="05188-147">Each insert operation is added by creating a new entity object, setting its values, and then calling the **insert** method on the **TableBatchOperation** object to associate the entity with a new insert operation.</span></span> <span data-ttu-id="05188-148">Następnie kod wywołuje **wykonania** na **CloudTable** obiektu, określając w tabeli "osoby" i **TableBatchOperation** obiektu, który wysyła do usługi magazynu w ramach pojedynczego żądania partii operacje tabeli.</span><span class="sxs-lookup"><span data-stu-id="05188-148">Then the code calls **execute** on the **CloudTable** object, specifying the "people" table and the **TableBatchOperation** object, which sends the batch of table operations to the storage service in a single request.</span></span>

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount =
        CloudStorageAccount.parse(storageConnectionString);

    // Create the table client.
    CloudTableClient tableClient = storageAccount.createCloudTableClient();

    // Define a batch operation.
    TableBatchOperation batchOperation = new TableBatchOperation();

    // Create a cloud table object for the table.
    CloudTable cloudTable = tableClient.getTableReference("people");

    // Create a customer entity to add to the table.
    CustomerEntity customer = new CustomerEntity("Smith", "Jeff");
    customer.setEmail("Jeff@contoso.com");
    customer.setPhoneNumber("425-555-0104");
    batchOperation.insertOrReplace(customer);

    // Create another customer entity to add to the table.
    CustomerEntity customer2 = new CustomerEntity("Smith", "Ben");
    customer2.setEmail("Ben@contoso.com");
    customer2.setPhoneNumber("425-555-0102");
    batchOperation.insertOrReplace(customer2);

    // Create a third customer entity to add to the table.
    CustomerEntity customer3 = new CustomerEntity("Smith", "Denise");
    customer3.setEmail("Denise@contoso.com");
    customer3.setPhoneNumber("425-555-0103");
    batchOperation.insertOrReplace(customer3);

    // Execute the batch of operations on the "people" table.
    cloudTable.execute(batchOperation);
}
catch (Exception e)
{
    // Output the stack trace.
    e.printStackTrace();
}
```

<span data-ttu-id="05188-149">Należy pamiętać, dotyczące operacji zbiorczych w kilku kwestiach:</span><span class="sxs-lookup"><span data-stu-id="05188-149">Some things to note on batch operations:</span></span>

* <span data-ttu-id="05188-150">Można wykonać wstawiania do 100, Usuń, scalić, Zastąp, Wstaw lub scalania i Wstaw lub zamienianie operacji w dowolnej kombinacji w pojedynczej partii.</span><span class="sxs-lookup"><span data-stu-id="05188-150">You can perform up to 100 insert, delete, merge, replace, insert or merge, and insert or replace operations in any combination in a single batch.</span></span>
* <span data-ttu-id="05188-151">Operacji zbiorczej może mieć operacji pobierania, jeśli jest jedyną operacją w partii.</span><span class="sxs-lookup"><span data-stu-id="05188-151">A batch operation can have a retrieve operation, if it is the only operation in the batch.</span></span>
* <span data-ttu-id="05188-152">Wszystkie jednostki w jednej operacji zbiorczej muszą mieć ten sam klucz partycji.</span><span class="sxs-lookup"><span data-stu-id="05188-152">All entities in a single batch operation must have the same partition key.</span></span>
* <span data-ttu-id="05188-153">Operacji zbiorczej jest ograniczony do 4MB danych ładunku.</span><span class="sxs-lookup"><span data-stu-id="05188-153">A batch operation is limited to a 4MB data payload.</span></span>

## <a name="how-to-retrieve-all-entities-in-a-partition"></a><span data-ttu-id="05188-154">Porady: pobieranie wszystkich jednostek w partycji</span><span class="sxs-lookup"><span data-stu-id="05188-154">How to: Retrieve all entities in a partition</span></span>
<span data-ttu-id="05188-155">Aby odpytać tabeli dla jednostek w partycji, można użyć **TableQuery**.</span><span class="sxs-lookup"><span data-stu-id="05188-155">To query a table for entities in a partition, you can use a **TableQuery**.</span></span> <span data-ttu-id="05188-156">Wywołanie **TableQuery.from** utworzyć zapytanie dla konkretnej tabeli, która zwraca typ określony wynik.</span><span class="sxs-lookup"><span data-stu-id="05188-156">Call **TableQuery.from** to create a query on a particular table that returns a specified result type.</span></span> <span data-ttu-id="05188-157">Poniższy kod określa filtr jednostek, gdzie "Smith" jest kluczem partycji.</span><span class="sxs-lookup"><span data-stu-id="05188-157">The following code specifies a filter for entities where 'Smith' is the partition key.</span></span> <span data-ttu-id="05188-158">**TableQuery.generateFilterCondition** metodę pomocnika, aby utworzyć filtry dla zapytań.</span><span class="sxs-lookup"><span data-stu-id="05188-158">**TableQuery.generateFilterCondition** is a helper method to create filters for queries.</span></span> <span data-ttu-id="05188-159">Wywołanie **gdzie** na odwołanie zwrócone przez **TableQuery.from** metody, aby zastosować filtr do zapytania.</span><span class="sxs-lookup"><span data-stu-id="05188-159">Call **where** on the reference returned by the **TableQuery.from** method to apply the filter to the query.</span></span> <span data-ttu-id="05188-160">Podczas wykonywania zapytania w wyniku wywołania **wykonania** na **CloudTable** obiektu i zwraca **Iterator** z **CustomerEntity** określony typ wyniku.</span><span class="sxs-lookup"><span data-stu-id="05188-160">When the query is executed with a call to **execute** on the **CloudTable** object, it returns an **Iterator** with the **CustomerEntity** result type specified.</span></span> <span data-ttu-id="05188-161">Następnie można użyć **iteratora** zwracane w dla każdej pętli do pracy z wyników.</span><span class="sxs-lookup"><span data-stu-id="05188-161">You can then use the **Iterator** returned in a for each loop to consume the results.</span></span> <span data-ttu-id="05188-162">Ten kod drukowane są pola każdej jednostki w wynikach zapytania do konsoli.</span><span class="sxs-lookup"><span data-stu-id="05188-162">This code prints the fields of each entity in the query results to the console.</span></span>

```java
try
{
    // Define constants for filters.
    final String PARTITION_KEY = "PartitionKey";
    final String ROW_KEY = "RowKey";
    final String TIMESTAMP = "Timestamp";

    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount =
        CloudStorageAccount.parse(storageConnectionString);

    // Create the table client.
    CloudTableClient tableClient = storageAccount.createCloudTableClient();

    // Create a cloud table object for the table.
    CloudTable cloudTable = tableClient.getTableReference("people");

    // Create a filter condition where the partition key is "Smith".
    String partitionFilter = TableQuery.generateFilterCondition(
        PARTITION_KEY,
        QueryComparisons.EQUAL,
        "Smith");

    // Specify a partition query, using "Smith" as the partition key filter.
    TableQuery<CustomerEntity> partitionQuery =
        TableQuery.from(CustomerEntity.class)
        .where(partitionFilter);

    // Loop through the results, displaying information about the entity.
    for (CustomerEntity entity : cloudTable.execute(partitionQuery)) {
        System.out.println(entity.getPartitionKey() +
            " " + entity.getRowKey() +
            "\t" + entity.getEmail() +
            "\t" + entity.getPhoneNumber());
    }
}
catch (Exception e)
{
    // Output the stack trace.
    e.printStackTrace();
}
```

## <a name="how-to-retrieve-a-range-of-entities-in-a-partition"></a><span data-ttu-id="05188-163">Porady: pobieranie zakresu jednostek w partycji</span><span class="sxs-lookup"><span data-stu-id="05188-163">How to: Retrieve a range of entities in a partition</span></span>
<span data-ttu-id="05188-164">Jeśli nie chcesz zbadać wszystkich jednostek w partycji, możesz określić zakres przy użyciu operatory porównania w filtrze.</span><span class="sxs-lookup"><span data-stu-id="05188-164">If you don't want to query all the entities in a partition, you can specify a range by using comparison operators in a filter.</span></span> <span data-ttu-id="05188-165">Poniższy kod łączy dwa filtry do pobrania wszystkich jednostek w partycji "Smith", gdzie klucz wiersza (imię) rozpoczyna się od litery do "E" alfabetu.</span><span class="sxs-lookup"><span data-stu-id="05188-165">The following code combines two filters to get all entities in partition "Smith" where the row key (first name) starts with a letter up to 'E' in the alphabet.</span></span> <span data-ttu-id="05188-166">Następnie drukuje wyniki zapytania.</span><span class="sxs-lookup"><span data-stu-id="05188-166">Then it prints the query results.</span></span> <span data-ttu-id="05188-167">Jeśli używasz dodane do tabeli w partii jednostek wstawić części tego przewodnika, tylko dwie jednostki są zwracane w tej chwili (Ben i Adam Nowak); Jan Kowalski nie jest włączony.</span><span class="sxs-lookup"><span data-stu-id="05188-167">If you use the entities added to the table in the batch insert section of this guide, only two entities are returned this time (Ben and Denise Smith); Jeff Smith is not included.</span></span>

```java
try
{
    // Define constants for filters.
    final String PARTITION_KEY = "PartitionKey";
    final String ROW_KEY = "RowKey";
    final String TIMESTAMP = "Timestamp";

    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount =
        CloudStorageAccount.parse(storageConnectionString);

    // Create the table client.
    CloudTableClient tableClient = storageAccount.createCloudTableClient();

    // Create a cloud table object for the table.
    CloudTable cloudTable = tableClient.getTableReference("people");

    // Create a filter condition where the partition key is "Smith".
    String partitionFilter = TableQuery.generateFilterCondition(
        PARTITION_KEY,
        QueryComparisons.EQUAL,
        "Smith");

    // Create a filter condition where the row key is less than the letter "E".
    String rowFilter = TableQuery.generateFilterCondition(
        ROW_KEY,
        QueryComparisons.LESS_THAN,
        "E");

    // Combine the two conditions into a filter expression.
    String combinedFilter = TableQuery.combineFilters(partitionFilter,
        Operators.AND, rowFilter);

    // Specify a range query, using "Smith" as the partition key,
    // with the row key being up to the letter "E".
    TableQuery<CustomerEntity> rangeQuery =
        TableQuery.from(CustomerEntity.class)
        .where(combinedFilter);

    // Loop through the results, displaying information about the entity
    for (CustomerEntity entity : cloudTable.execute(rangeQuery)) {
        System.out.println(entity.getPartitionKey() +
            " " + entity.getRowKey() +
            "\t" + entity.getEmail() +
            "\t" + entity.getPhoneNumber());
    }
}
catch (Exception e)
{
    // Output the stack trace.
    e.printStackTrace();
}
```

## <a name="how-to-retrieve-a-single-entity"></a><span data-ttu-id="05188-168">Porady: pobieranie pojedynczej jednostki</span><span class="sxs-lookup"><span data-stu-id="05188-168">How to: Retrieve a single entity</span></span>
<span data-ttu-id="05188-169">Można napisać zapytanie do pobrania jednej, określonej jednostki.</span><span class="sxs-lookup"><span data-stu-id="05188-169">You can write a query to retrieve a single, specific entity.</span></span> <span data-ttu-id="05188-170">Poniższy kod wywołania **TableOperation.retrieve** z partycją klucza i wiersz klucza parametrów do określenia klienta "Jan Kowalski", zamiast tworzyć **TableQuery** i za pomocą filtrów, aby zrobić to samo.</span><span class="sxs-lookup"><span data-stu-id="05188-170">The following code calls **TableOperation.retrieve** with partition key and row key parameters to specify the customer "Jeff Smith", instead of creating a **TableQuery** and using filters to do the same thing.</span></span> <span data-ttu-id="05188-171">Po wykonaniu operacji pobierania zwraca tylko jedną jednostkę zamiast kolekcji.</span><span class="sxs-lookup"><span data-stu-id="05188-171">When executed, the retrieve operation returns just one entity, rather than a collection.</span></span> <span data-ttu-id="05188-172">**GetResultAsType** metody rzutuje wynik, który ma typ elementu docelowego przypisania **CustomerEntity** obiektu.</span><span class="sxs-lookup"><span data-stu-id="05188-172">The **getResultAsType** method casts the result to the type of the assignment target, a **CustomerEntity** object.</span></span> <span data-ttu-id="05188-173">Jeśli ten typ nie jest zgodny z typem określonym w zapytaniu, zostanie wygenerowany wyjątek.</span><span class="sxs-lookup"><span data-stu-id="05188-173">If this type is not compatible with the type specified for the query, an exception will be thrown.</span></span> <span data-ttu-id="05188-174">Jeśli jednostka nie ma dokładnie partycji i klucz wiersza zgodne, jest zwracana wartość null.</span><span class="sxs-lookup"><span data-stu-id="05188-174">A null value is returned if no entity has an exact partition and row key match.</span></span> <span data-ttu-id="05188-175">Określenie kluczy partycji i wiersza w pojedynczym zapytaniu jest najszybszym sposobem na pobranie jednej jednostki z usługi tabel.</span><span class="sxs-lookup"><span data-stu-id="05188-175">Specifying both partition and row keys in a query is the fastest way to retrieve a single entity from the Table service.</span></span>

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount =
        CloudStorageAccount.parse(storageConnectionString);

    // Create the table client.
    CloudTableClient tableClient = storageAccount.createCloudTableClient();

    // Create a cloud table object for the table.
    CloudTable cloudTable = tableClient.getTableReference("people");

    // Retrieve the entity with partition key of "Smith" and row key of "Jeff"
    TableOperation retrieveSmithJeff =
        TableOperation.retrieve("Smith", "Jeff", CustomerEntity.class);

    // Submit the operation to the table service and get the specific entity.
    CustomerEntity specificEntity =
        cloudTable.execute(retrieveSmithJeff).getResultAsType();

    // Output the entity.
    if (specificEntity != null)
    {
        System.out.println(specificEntity.getPartitionKey() +
            " " + specificEntity.getRowKey() +
            "\t" + specificEntity.getEmail() +
            "\t" + specificEntity.getPhoneNumber());
    }
}
catch (Exception e)
{
    // Output the stack trace.
    e.printStackTrace();
}
```

## <a name="how-to-modify-an-entity"></a><span data-ttu-id="05188-176">Porady: modyfikowanie jednostki</span><span class="sxs-lookup"><span data-stu-id="05188-176">How to: Modify an entity</span></span>
<span data-ttu-id="05188-177">Aby zmodyfikować jednostkę, pobierz ją z usługi tabel zmiany obiektu jednostki i zapisać zmian z powrotem do usługi tabel za pomocą operacji zamiany lub scalania.</span><span class="sxs-lookup"><span data-stu-id="05188-177">To modify an entity, retrieve it from the table service, make changes to the entity object, and save the changes back to the table service with a replace or merge operation.</span></span> <span data-ttu-id="05188-178">Poniższy kod zmienia istniejący numer telefonu klienta.</span><span class="sxs-lookup"><span data-stu-id="05188-178">The following code changes an existing customer's phone number.</span></span> <span data-ttu-id="05188-179">Zamiast wywoływać metodę **TableOperation.insert** jak robiliśmy Wstaw ten kod wywołuje **TableOperation.replace**.</span><span class="sxs-lookup"><span data-stu-id="05188-179">Instead of calling **TableOperation.insert** like we did to insert, this code calls **TableOperation.replace**.</span></span> <span data-ttu-id="05188-180">**CloudTable.execute** metoda wywołuje usługi tabel, a jednostka zostanie zastąpiony, chyba że inna aplikacja uległ zmianie w czasie od pobrany tej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="05188-180">The **CloudTable.execute** method calls the table service, and the entity is replaced, unless another application changed it in the time since this application retrieved it.</span></span> <span data-ttu-id="05188-181">W takim przypadku jest zwracany wyjątek, a jednostka musi być pobierane, zmodyfikowane i zapisane ponownie.</span><span class="sxs-lookup"><span data-stu-id="05188-181">When that happens, an exception is thrown, and the entity must be retrieved, modified, and saved again.</span></span> <span data-ttu-id="05188-182">Ten wzorzec ponawiania optymistycznej współbieżności jest typowe w przypadku rozproszony systemem przechowywania.</span><span class="sxs-lookup"><span data-stu-id="05188-182">This optimistic concurrency retry pattern is common in a distributed storage system.</span></span>

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount =
        CloudStorageAccount.parse(storageConnectionString);

    // Create the table client.
    CloudTableClient tableClient = storageAccount.createCloudTableClient();

    // Create a cloud table object for the table.
    CloudTable cloudTable = tableClient.getTableReference("people");

    // Retrieve the entity with partition key of "Smith" and row key of "Jeff".
    TableOperation retrieveSmithJeff =
        TableOperation.retrieve("Smith", "Jeff", CustomerEntity.class);

    // Submit the operation to the table service and get the specific entity.
    CustomerEntity specificEntity =
        cloudTable.execute(retrieveSmithJeff).getResultAsType();

    // Specify a new phone number.
    specificEntity.setPhoneNumber("425-555-0105");

    // Create an operation to replace the entity.
    TableOperation replaceEntity = TableOperation.replace(specificEntity);

    // Submit the operation to the table service.
    cloudTable.execute(replaceEntity);
}
catch (Exception e)
{
    // Output the stack trace.
    e.printStackTrace();
}
```

## <a name="how-to-query-a-subset-of-entity-properties"></a><span data-ttu-id="05188-183">Porady: Tworzenie zapytania do podzbioru właściwości jednostki</span><span class="sxs-lookup"><span data-stu-id="05188-183">How to: Query a subset of entity properties</span></span>
<span data-ttu-id="05188-184">Zapytanie do tabeli może pobrać kilka właściwości jednostki.</span><span class="sxs-lookup"><span data-stu-id="05188-184">A query to a table can retrieve just a few properties from an entity.</span></span> <span data-ttu-id="05188-185">Ta technika, zwana projekcją, redukuje przepustowość i może poprawiać wydajność zapytań, zwłaszcza w przypadku dużych jednostek.</span><span class="sxs-lookup"><span data-stu-id="05188-185">This technique, called projection, reduces bandwidth and can improve query performance, especially for large entities.</span></span> <span data-ttu-id="05188-186">Zapytanie w poniższym kodzie używa **wybierz** metodę, aby zwrócić tylko adresy e-mail jednostek w tabeli.</span><span class="sxs-lookup"><span data-stu-id="05188-186">The query in the following code uses the **select** method to return only the email addresses of entities in the table.</span></span> <span data-ttu-id="05188-187">Wyniki są przedstawione jako kolekcja **ciąg** za pomocą **EntityResolver**, która działa konwersji typu na jednostkach zwrócone z serwera.</span><span class="sxs-lookup"><span data-stu-id="05188-187">The results are projected into a collection of **String** with the help of an **EntityResolver**, which does the type conversion on the entities returned from the server.</span></span> <span data-ttu-id="05188-188">Dowiedz się więcej o projekcji w [tabel Azure: Introducing Upsert i projekcji zapytań][Azure Tables: Introducing Upsert and Query Projection].</span><span class="sxs-lookup"><span data-stu-id="05188-188">You can learn more about projection in [Azure Tables: Introducing Upsert and Query Projection][Azure Tables: Introducing Upsert and Query Projection].</span></span> <span data-ttu-id="05188-189">Należy pamiętać, że projekcji nie jest obsługiwana w lokalnym emulatorze magazynu, dlatego ten kod zadziała tylko wtedy, gdy przy użyciu konta w usłudze tabel.</span><span class="sxs-lookup"><span data-stu-id="05188-189">Note that projection is not supported on the local storage emulator, so this code runs only when using an account on the table service.</span></span>

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount =
        CloudStorageAccount.parse(storageConnectionString);

    // Create the table client.
    CloudTableClient tableClient = storageAccount.createCloudTableClient();

    // Create a cloud table object for the table.
    CloudTable cloudTable = tableClient.getTableReference("people");

    // Define a projection query that retrieves only the Email property
    TableQuery<CustomerEntity> projectionQuery =
        TableQuery.from(CustomerEntity.class)
        .select(new String[] {"Email"});

    // Define a Entity resolver to project the entity to the Email value.
    EntityResolver<String> emailResolver = new EntityResolver<String>() {
        @Override
        public String resolve(String PartitionKey, String RowKey, Date timeStamp, HashMap<String, EntityProperty> properties, String etag) {
            return properties.get("Email").getValueAsString();
        }
    };

    // Loop through the results, displaying the Email values.
    for (String projectedString :
        cloudTable.execute(projectionQuery, emailResolver)) {
            System.out.println(projectedString);
    }
}
catch (Exception e)
{
    // Output the stack trace.
    e.printStackTrace();
}
```

## <a name="how-to-insert-or-replace-an-entity"></a><span data-ttu-id="05188-190">Porady: wstawianie lub zastępowanie jednostki</span><span class="sxs-lookup"><span data-stu-id="05188-190">How to: Insert or Replace an entity</span></span>
<span data-ttu-id="05188-191">Często chcesz dodać jednostkę do tabeli bez wiedzy o Jeśli już istnieje w tabeli.</span><span class="sxs-lookup"><span data-stu-id="05188-191">Often you want to add an entity to a table without knowing if it already exists in the table.</span></span> <span data-ttu-id="05188-192">Operacja wstawiania lub Zastąp pozwala na zapewnienie pojedynczego żądania, które powoduje wstawienie jednostki, jeśli nie istnieje lub Zastąp istniejącą, jeśli tak.</span><span class="sxs-lookup"><span data-stu-id="05188-192">An insert-or-replace operation allows you to make a single request which will insert the entity if it does not exist or replace the existing one if it does.</span></span> <span data-ttu-id="05188-193">Korzystając z poprzednich przykładach, poniższy kod wstawia lub zamienia jednostki dla "Walter Harp".</span><span class="sxs-lookup"><span data-stu-id="05188-193">Building on prior examples, the following code inserts or replaces the entity for "Walter Harp".</span></span> <span data-ttu-id="05188-194">Po utworzeniu nowego obiektu, ten kod wywołuje **TableOperation.insertOrReplace** metody.</span><span class="sxs-lookup"><span data-stu-id="05188-194">After creating a new entity, this code calls the **TableOperation.insertOrReplace** method.</span></span> <span data-ttu-id="05188-195">Ten kod wywołuje **wykonania** na **CloudTable** obiekt z tabeli i Wstaw lub Zastąp operacja tabeli jako parametry.</span><span class="sxs-lookup"><span data-stu-id="05188-195">This code then calls **execute** on the **CloudTable** object with the table and the insert or replace table operation as the parameters.</span></span> <span data-ttu-id="05188-196">Aby zaktualizować tylko część jednostki **TableOperation.insertOrMerge** metody można użyć zamiast niego.</span><span class="sxs-lookup"><span data-stu-id="05188-196">To update only part of an entity, the **TableOperation.insertOrMerge** method can be used instead.</span></span> <span data-ttu-id="05188-197">Należy pamiętać, że wstawianie lub zastępowanie nie jest obsługiwane w emulatorze magazynu lokalnego, dlatego ten kod zadziała tylko wtedy, gdy przy użyciu konta w usłudze tabel.</span><span class="sxs-lookup"><span data-stu-id="05188-197">Note that insert-or-replace is not supported on the local storage emulator, so this code runs only when using an account on the table service.</span></span> <span data-ttu-id="05188-198">Możesz dowiedzieć się więcej o Wstawianie lub zastępowanie i Wstaw lub scalania w tym [tabel Azure: Introducing Upsert i projekcji zapytań][Azure Tables: Introducing Upsert and Query Projection].</span><span class="sxs-lookup"><span data-stu-id="05188-198">You can learn more about insert-or-replace and insert-or-merge in this [Azure Tables: Introducing Upsert and Query Projection][Azure Tables: Introducing Upsert and Query Projection].</span></span>

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount =
        CloudStorageAccount.parse(storageConnectionString);

    // Create the table client.
    CloudTableClient tableClient = storageAccount.createCloudTableClient();

    // Create a cloud table object for the table.
    CloudTable cloudTable = tableClient.getTableReference("people");

    // Create a new customer entity.
    CustomerEntity customer5 = new CustomerEntity("Harp", "Walter");
    customer5.setEmail("Walter@contoso.com");
    customer5.setPhoneNumber("425-555-0106");

    // Create an operation to add the new customer to the people table.
    TableOperation insertCustomer5 = TableOperation.insertOrReplace(customer5);

    // Submit the operation to the table service.
    cloudTable.execute(insertCustomer5);
}
catch (Exception e)
{
    // Output the stack trace.
    e.printStackTrace();
}
```

## <a name="how-to-delete-an-entity"></a><span data-ttu-id="05188-199">Porady: Usuwanie jednostki</span><span class="sxs-lookup"><span data-stu-id="05188-199">How to: Delete an entity</span></span>
<span data-ttu-id="05188-200">Po jej pobraniu można z łatwością usunąć jednostkę.</span><span class="sxs-lookup"><span data-stu-id="05188-200">You can easily delete an entity after you have retrieved it.</span></span> <span data-ttu-id="05188-201">Po pobraniu jednostki wywołać **TableOperation.delete** z jednostką do usunięcia.</span><span class="sxs-lookup"><span data-stu-id="05188-201">Once the entity is retrieved, call **TableOperation.delete** with the entity to delete.</span></span> <span data-ttu-id="05188-202">Następnie wywołaj **wykonania** na **CloudTable** obiektu.</span><span class="sxs-lookup"><span data-stu-id="05188-202">Then call **execute** on the **CloudTable** object.</span></span> <span data-ttu-id="05188-203">Poniższy kod umożliwia pobranie i usunięcie jednostki klienta.</span><span class="sxs-lookup"><span data-stu-id="05188-203">The following code retrieves and deletes a customer entity.</span></span>

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount =
        CloudStorageAccount.parse(storageConnectionString);

    // Create the table client.
    CloudTableClient tableClient = storageAccount.createCloudTableClient();

    // Create a cloud table object for the table.
    CloudTable cloudTable = tableClient.getTableReference("people");

    // Create an operation to retrieve the entity with partition key of "Smith" and row key of "Jeff".
    TableOperation retrieveSmithJeff = TableOperation.retrieve("Smith", "Jeff", CustomerEntity.class);

    // Retrieve the entity with partition key of "Smith" and row key of "Jeff".
    CustomerEntity entitySmithJeff =
        cloudTable.execute(retrieveSmithJeff).getResultAsType();

    // Create an operation to delete the entity.
    TableOperation deleteSmithJeff = TableOperation.delete(entitySmithJeff);

    // Submit the delete operation to the table service.
    cloudTable.execute(deleteSmithJeff);
}
catch (Exception e)
{
    // Output the stack trace.
    e.printStackTrace();
}
```

## <a name="how-to-delete-a-table"></a><span data-ttu-id="05188-204">Porady: usuwanie tabeli</span><span class="sxs-lookup"><span data-stu-id="05188-204">How to: Delete a table</span></span>
<span data-ttu-id="05188-205">Na koniec następującego kodu usuwa tabelę z konta magazynu.</span><span class="sxs-lookup"><span data-stu-id="05188-205">Finally, the following code deletes a table from a storage account.</span></span> <span data-ttu-id="05188-206">Tabela, który został usunięty będą niedostępne do odtworzenia w danym okresie czasu po usunięciu, zazwyczaj mniej niż 40 sekund.</span><span class="sxs-lookup"><span data-stu-id="05188-206">A table which has been deleted will be unavailable to be recreated for a period of time following the deletion, usually less than forty seconds.</span></span>

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount =
        CloudStorageAccount.parse(storageConnectionString);

    // Create the table client.
    CloudTableClient tableClient = storageAccount.createCloudTableClient();

    // Delete the table and all its data if it exists.
    CloudTable cloudTable = tableClient.getTableReference("people");
    cloudTable.deleteIfExists();
}
catch (Exception e)
{
    // Output the stack trace.
    e.printStackTrace();
}
```
[!INCLUDE [storage-check-out-samples-java](../../includes/storage-check-out-samples-java.md)]

## <a name="next-steps"></a><span data-ttu-id="05188-207">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="05188-207">Next steps</span></span>

* <span data-ttu-id="05188-208">[Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md) jest bezpłatną aplikacją autonomiczną oferowaną przez firmę Microsoft, która umożliwia wizualną pracę z danymi w usłudze Azure Storage w systemach Windows, macOS i Linux.</span><span class="sxs-lookup"><span data-stu-id="05188-208">[Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md) is a free, standalone app from Microsoft that enables you to work visually with Azure Storage data on Windows, macOS, and Linux.</span></span>
* <span data-ttu-id="05188-209">[Magazyn Azure SDK dla języka Java][Azure Storage SDK for Java]</span><span class="sxs-lookup"><span data-stu-id="05188-209">[Azure Storage SDK for Java][Azure Storage SDK for Java]</span></span>
* <span data-ttu-id="05188-210">[Odwołanie do zestawu SDK klienta usługi Azure Storage][odwołania do zestawu SDK klienta magazynu Azure]</span><span class="sxs-lookup"><span data-stu-id="05188-210">[Azure Storage Client SDK Reference][Azure Storage Client SDK Reference]</span></span>
* <span data-ttu-id="05188-211">[Interfejs API REST usługi Azure Storage][Azure Storage REST API]</span><span class="sxs-lookup"><span data-stu-id="05188-211">[Azure Storage REST API][Azure Storage REST API]</span></span>
* <span data-ttu-id="05188-212">[Blog zespołu usługi Magazyn Azure][Azure Storage Team Blog]</span><span class="sxs-lookup"><span data-stu-id="05188-212">[Azure Storage Team Blog][Azure Storage Team Blog]</span></span>

<span data-ttu-id="05188-213">Aby uzyskać więcej informacji, odwiedź stronę [Azure dla deweloperów języka Java](/java/azure).</span><span class="sxs-lookup"><span data-stu-id="05188-213">For more information, visit [Azure for Java developers](/java/azure).</span></span>

[Azure SDK for Java]: http://go.microsoft.com/fwlink/?LinkID=525671
[Azure Storage SDK for Java]: https://github.com/azure/azure-storage-java
[Azure Storage SDK for Android]: https://github.com/azure/azure-storage-android
[odwołania do zestawu SDK klienta magazynu Azure]: http://dl.windowsazure.com/storage/javadoc/
[Azure Storage REST API]: https://msdn.microsoft.com/library/azure/dd179355.aspx
[Azure Storage Team Blog]: http://blogs.msdn.com/b/windowsazurestorage/
[Azure Tables: Introducing Upsert and Query Projection]: http://blogs.msdn.com/b/windowsazurestorage/archive/2011/09/15/windows-azure-tables-introducing-upsert-and-query-projection.aspx
