---
title: "toouse aaaHow magazynu tabel w języku Java | Dokumentacja firmy Microsoft"
description: "Przechowywanie danych strukturalnych w chmurze hello przy użyciu magazynu tabel Azure, Magazyn danych NoSQL."
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
ms.openlocfilehash: 20d03e867219cc254da8dad37cf3cf61bca65671
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-table-storage-from-java"></a><span data-ttu-id="40dbc-103">Jak toouse magazynu tabel w języku Java</span><span class="sxs-lookup"><span data-stu-id="40dbc-103">How toouse Table storage from Java</span></span>
[!INCLUDE [storage-selector-table-include](../../includes/storage-selector-table-include.md)]
[!INCLUDE [storage-table-cosmos-db-langsoon-tip-include](../../includes/storage-table-cosmos-db-langsoon-tip-include.md)]

## <a name="overview"></a><span data-ttu-id="40dbc-104">Omówienie</span><span class="sxs-lookup"><span data-stu-id="40dbc-104">Overview</span></span>
<span data-ttu-id="40dbc-105">W tym przewodniku opisano sposób tooperform typowych scenariuszy przy użyciu hello usługi Magazyn tabel Azure.</span><span class="sxs-lookup"><span data-stu-id="40dbc-105">This guide will show you how tooperform common scenarios using hello Azure Table storage service.</span></span> <span data-ttu-id="40dbc-106">Hello przykłady są napisane w języku Java i używają hello [Azure Storage SDK for Java][Azure Storage SDK for Java].</span><span class="sxs-lookup"><span data-stu-id="40dbc-106">hello samples are written in Java and use hello [Azure Storage SDK for Java][Azure Storage SDK for Java].</span></span> <span data-ttu-id="40dbc-107">Witaj omówione scenariusze obejmują **tworzenie**, **wyświetlania**, i **usuwanie** tabel, jak również **wstawianie**,  **wykonywanie zapytania**, **modyfikowanie**, i **usuwanie** jednostek w tabeli.</span><span class="sxs-lookup"><span data-stu-id="40dbc-107">hello scenarios covered include **creating**, **listing**, and **deleting** tables, as well as **inserting**, **querying**, **modifying**, and **deleting** entities in a table.</span></span> <span data-ttu-id="40dbc-108">Aby uzyskać więcej informacji w tabelach, zobacz hello [następne kroki](#Next-Steps) sekcji.</span><span class="sxs-lookup"><span data-stu-id="40dbc-108">For more information on tables, see hello [Next steps](#Next-Steps) section.</span></span>

<span data-ttu-id="40dbc-109">Uwaga: Zestaw SDK jest dostępny dla deweloperów, którzy korzystają z usługi Azure Storage na urządzeniach z systemem Android.</span><span class="sxs-lookup"><span data-stu-id="40dbc-109">Note: An SDK is available for developers who are using Azure Storage on Android devices.</span></span> <span data-ttu-id="40dbc-110">Aby uzyskać więcej informacji, zobacz hello [zestawu SDK usługi Magazyn Azure dla systemu Android][Azure Storage SDK for Android].</span><span class="sxs-lookup"><span data-stu-id="40dbc-110">For more information, see hello [Azure Storage SDK for Android][Azure Storage SDK for Android].</span></span>

[!INCLUDE [storage-table-concepts-include](../../includes/storage-table-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/storage-create-account-include.md)]

## <a name="create-a-java-application"></a><span data-ttu-id="40dbc-111">Tworzenie aplikacji Java</span><span class="sxs-lookup"><span data-stu-id="40dbc-111">Create a Java application</span></span>
<span data-ttu-id="40dbc-112">W tym przewodniku użyje funkcji magazynu, które mogą być uruchamiane w ramach aplikacji Java lokalnie lub w kodzie działających w roli sieci web lub roli proces roboczy na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="40dbc-112">In this guide, you will use storage features which can be run within a Java application locally, or in code running within a web role or worker role in Azure.</span></span>

<span data-ttu-id="40dbc-113">toodo tak, konieczne będzie tooinstall hello Java Development Kit (JDK) i utworzyć konto magazynu Azure w ramach subskrypcji platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="40dbc-113">toodo so, you will need tooinstall hello Java Development Kit (JDK) and create an Azure storage account in your Azure subscription.</span></span> <span data-ttu-id="40dbc-114">Po zostało to zrobione, należy tooverify spełniającym w systemie deweloperskim hello minimalne wymagania i zależności, które są wymienione w hello [Azure Storage SDK for Java] [ Azure Storage SDK for Java] repozytorium w witrynie GitHub.</span><span class="sxs-lookup"><span data-stu-id="40dbc-114">Once you have done so, you will need tooverify that your development system meets hello minimum requirements and dependencies which are listed in hello [Azure Storage SDK for Java][Azure Storage SDK for Java] repository on GitHub.</span></span> <span data-ttu-id="40dbc-115">Jeżeli komputer spełnia te wymagania, należy wykonać hello instrukcje dotyczące pobierania i instalowania hello biblioteki magazynu Azure dla języka Java w systemie z tego repozytorium.</span><span class="sxs-lookup"><span data-stu-id="40dbc-115">If your system meets those requirements, you can follow hello instructions for downloading and installing hello Azure Storage Libraries for Java on your system from that repository.</span></span> <span data-ttu-id="40dbc-116">Po wykonaniu tych zadań, będzie możliwe toocreate aplikacji Java, który używa hello przykłady w tym artykule.</span><span class="sxs-lookup"><span data-stu-id="40dbc-116">Once you have completed those tasks, you will be able toocreate a Java application which uses hello examples in this article.</span></span>

## <a name="configure-your-application-tooaccess-table-storage"></a><span data-ttu-id="40dbc-117">Konfigurowanie magazynu tabeli tooaccess aplikacji</span><span class="sxs-lookup"><span data-stu-id="40dbc-117">Configure your application tooaccess table storage</span></span>
<span data-ttu-id="40dbc-118">Dodaj powitania od góry toohello instrukcje importu miejscu toouse tabel tooaccess interfejsów API Microsoft Azure do przechowywania plików Java hello:</span><span class="sxs-lookup"><span data-stu-id="40dbc-118">Add hello following import statements toohello top of hello Java file where you want toouse Microsoft Azure storage APIs tooaccess tables:</span></span>

```java
// Include hello following imports toouse table APIs
import com.microsoft.azure.storage.*;
import com.microsoft.azure.storage.table.*;
import com.microsoft.azure.storage.table.TableQuery.*;
```

## <a name="set-up-an-azure-storage-connection-string"></a><span data-ttu-id="40dbc-119">Konfigurowanie parametrów połączenia usługi Azure storage</span><span class="sxs-lookup"><span data-stu-id="40dbc-119">Set up an Azure storage connection string</span></span>
<span data-ttu-id="40dbc-120">Klienta usługi Azure storage używa punkty końcowe magazynu połączenia ciąg toostore i poświadczeń do uzyskiwania dostępu do danych usługi zarządzania.</span><span class="sxs-lookup"><span data-stu-id="40dbc-120">An Azure storage client uses a storage connection string toostore endpoints and credentials for accessing data management services.</span></span> <span data-ttu-id="40dbc-121">Podczas uruchamiania w aplikacji klienckiej, należy podać parametry połączenia magazynu hello w hello zgodny z formatem, przy użyciu hello nazwy konta magazynu i hello podstawowy klucz dostępu dla konta magazynu hello na liście hello [portalu Azure](https://portal.azure.com)dla hello *AccountName* i *AccountKey* wartości.</span><span class="sxs-lookup"><span data-stu-id="40dbc-121">When running in a client application, you must provide hello storage connection string in hello following format, using hello name of your storage account and hello Primary access key for hello storage account listed in hello [Azure portal](https://portal.azure.com) for hello *AccountName* and *AccountKey* values.</span></span> <span data-ttu-id="40dbc-122">Ten przykład przedstawia, jak można zadeklarować ciąg połączenia pola statycznego toohold hello:</span><span class="sxs-lookup"><span data-stu-id="40dbc-122">This example shows how you can declare a static field toohold hello connection string:</span></span>

```java
// Define hello connection-string with your values.
public static final String storageConnectionString =
    "DefaultEndpointsProtocol=http;" +
    "AccountName=your_storage_account;" +
    "AccountKey=your_storage_account_key";
```

<span data-ttu-id="40dbc-123">W aplikacji działającej w ramach roli w systemie Microsoft Azure, te parametry mogą być przechowywane w pliku konfiguracji usługi hello, *pliku ServiceConfiguration.cscfg*i jest dostępny z toohello wywołania  **RoleEnvironment.getConfigurationSettings** metody.</span><span class="sxs-lookup"><span data-stu-id="40dbc-123">In an application running within a role in Microsoft Azure, this string can be stored in hello service configuration file, *ServiceConfiguration.cscfg*, and can be accessed with a call toohello **RoleEnvironment.getConfigurationSettings** method.</span></span> <span data-ttu-id="40dbc-124">Oto przykład pobierania hello parametrów połączenia z **ustawienie** elementu o nazwie *StorageConnectionString* w pliku konfiguracji usługi hello:</span><span class="sxs-lookup"><span data-stu-id="40dbc-124">Here's an example of getting hello connection string from a **Setting** element named *StorageConnectionString* in hello service configuration file:</span></span>

```java
// Retrieve storage account from connection-string.
String storageConnectionString =
    RoleEnvironment.getConfigurationSettings().get("StorageConnectionString");
```

<span data-ttu-id="40dbc-125">Hello następujące przykłady założono, że użyto jednego z tych parametrów połączenia magazynu Witaj dwie metody tooget.</span><span class="sxs-lookup"><span data-stu-id="40dbc-125">hello following samples assume that you have used one of these two methods tooget hello storage connection string.</span></span>

## <a name="how-to-create-a-table"></a><span data-ttu-id="40dbc-126">Porady: Tworzenie tabeli</span><span class="sxs-lookup"><span data-stu-id="40dbc-126">How to: Create a table</span></span>
<span data-ttu-id="40dbc-127">A **CloudTableClient** obiektu pozwala pobierać obiekty odwołania do tabel i jednostek.</span><span class="sxs-lookup"><span data-stu-id="40dbc-127">A **CloudTableClient** object lets you get reference objects for tables and entities.</span></span> <span data-ttu-id="40dbc-128">Witaj poniższy kod tworzy **CloudTableClient** obiektu i używa go toocreate nowy **CloudTable** obiekt, który reprezentuje tabeli o nazwie "osoby".</span><span class="sxs-lookup"><span data-stu-id="40dbc-128">hello following code creates a **CloudTableClient** object and uses it toocreate a new **CloudTable** object which represents a table named "people".</span></span> <span data-ttu-id="40dbc-129">(Uwaga: istnieją dodatkowe sposoby toocreate **CloudStorageAccount** obiektów; Aby uzyskać więcej informacji, zobacz **CloudStorageAccount** w hello [odwołaniazestawuSDKklientamagazynuAzure].)</span><span class="sxs-lookup"><span data-stu-id="40dbc-129">(Note: There are additional ways toocreate **CloudStorageAccount** objects; for more information, see **CloudStorageAccount** in hello [Azure Storage Client SDK Reference].)</span></span>

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount =
        CloudStorageAccount.parse(storageConnectionString);

    // Create hello table client.
    CloudTableClient tableClient = storageAccount.createCloudTableClient();

    // Create hello table if it doesn't exist.
    String tableName = "people";
    CloudTable cloudTable = tableClient.getTableReference(tableName);
    cloudTable.createIfNotExists();
}
catch (Exception e)
{
    // Output hello stack trace.
    e.printStackTrace();
}
```

## <a name="how-to-list-hello-tables"></a><span data-ttu-id="40dbc-130">Porady: Lista hello tabel</span><span class="sxs-lookup"><span data-stu-id="40dbc-130">How to: List hello tables</span></span>
<span data-ttu-id="40dbc-131">tooget listę tabel, wywołanie hello **CloudTableClient.listTables()** tooretrieve metody iterable listę nazw tabel.</span><span class="sxs-lookup"><span data-stu-id="40dbc-131">tooget a list of tables, call hello **CloudTableClient.listTables()** method tooretrieve an iterable list of table names.</span></span>

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount =
        CloudStorageAccount.parse(storageConnectionString);

    // Create hello table client.
    CloudTableClient tableClient = storageAccount.createCloudTableClient();

    // Loop through hello collection of table names.
    for (String table : tableClient.listTables())
    {
        // Output each table name.
        System.out.println(table);
    }
}
catch (Exception e)
{
    // Output hello stack trace.
    e.printStackTrace();
}
```

## <a name="how-to-add-an-entity-tooa-table"></a><span data-ttu-id="40dbc-132">Porady: Dodawanie tabeli tooa jednostki</span><span class="sxs-lookup"><span data-stu-id="40dbc-132">How to: Add an entity tooa table</span></span>
<span data-ttu-id="40dbc-133">Jednostki są mapowane tooJava obiektów za pomocą niestandardowej klasy implementacja **TableEntity**.</span><span class="sxs-lookup"><span data-stu-id="40dbc-133">Entities map tooJava objects using a custom class implementing **TableEntity**.</span></span> <span data-ttu-id="40dbc-134">Dla wygody hello **TableServiceEntity** klasa implementuje **TableEntity** i właściwości toomap odbicia używa metody toogetter i ustawiające o nazwie odpowiadającej hello właściwości.</span><span class="sxs-lookup"><span data-stu-id="40dbc-134">For convenience, hello **TableServiceEntity** class implements **TableEntity** and uses reflection toomap properties toogetter and setter methods named for hello properties.</span></span> <span data-ttu-id="40dbc-135">tooadd jednostki tooa tabeli, najpierw utworzyć klasę, która definiuje właściwości hello jednostki.</span><span class="sxs-lookup"><span data-stu-id="40dbc-135">tooadd an entity tooa table, first create a class that defines hello properties of your entity.</span></span> <span data-ttu-id="40dbc-136">Witaj poniższy kod definiuje klasę jednostki, która używa imienia klienta hello jako hello klucz wiersza i nazwiska jako klucza partycji hello.</span><span class="sxs-lookup"><span data-stu-id="40dbc-136">hello following code defines an entity class which uses hello customer's first name as hello row key, and last name as hello partition key.</span></span> <span data-ttu-id="40dbc-137">Razem klucz partycji i klucz wiersza jednoznacznie zidentyfikować hello jednostki w tabeli hello.</span><span class="sxs-lookup"><span data-stu-id="40dbc-137">Together, an entity's partition and row key uniquely identify hello entity in hello table.</span></span> <span data-ttu-id="40dbc-138">Jednostki z tym samym kluczem partycji mogą być przeszukiwane szybciej niż jednostki o różnych kluczach partycji powitalne.</span><span class="sxs-lookup"><span data-stu-id="40dbc-138">Entities with hello same partition key can be queried faster than those with different partition keys.</span></span>

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

<span data-ttu-id="40dbc-139">Operacje tabeli obejmujące jednostki wymagają **TableOperation** obiektu.</span><span class="sxs-lookup"><span data-stu-id="40dbc-139">Table operations involving entities require a **TableOperation** object.</span></span> <span data-ttu-id="40dbc-140">Ten obiekt definiuje hello toobe działania wykonywane w ramach jednostki, które mogą być wykonywane przez **CloudTable** obiektu.</span><span class="sxs-lookup"><span data-stu-id="40dbc-140">This object defines hello operation toobe performed on an entity, which can be executed with a **CloudTable** object.</span></span> <span data-ttu-id="40dbc-141">Witaj poniższy kod tworzy nowe wystąpienie klasy hello **CustomerEntity** klasy z niektórych toobe dane klienta przechowywane.</span><span class="sxs-lookup"><span data-stu-id="40dbc-141">hello following code creates a new instance of hello **CustomerEntity** class with some customer data toobe stored.</span></span> <span data-ttu-id="40dbc-142">Witaj kod wywołuje dalej **TableOperation.insertOrReplace** toocreate **TableOperation** obiekt tooinsert jednostki do tabeli, a skojarzone hello nowych **CustomerEntity**z nim.</span><span class="sxs-lookup"><span data-stu-id="40dbc-142">hello code next calls **TableOperation.insertOrReplace** toocreate a **TableOperation** object tooinsert an entity into a table, and associates hello new **CustomerEntity** with it.</span></span> <span data-ttu-id="40dbc-143">Na koniec hello kod wywołuje hello **wykonania** metody na powitania **CloudTable** obiektu, w tabeli "osoby" hello i hello nowe **TableOperation**, które wysyła następnie żądanie toohello magazynu usługi tooinsert hello nowej jednostce klienta w tabeli "osoby" hello, lub Zastąp hello jednostki, jeśli już istnieje.</span><span class="sxs-lookup"><span data-stu-id="40dbc-143">Finally, hello code calls hello **execute** method on hello **CloudTable** object, specifying hello "people" table and hello new **TableOperation**, which then sends a request toohello storage service tooinsert hello new customer entity into hello "people" table, or replace hello entity if it already exists.</span></span>

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount =
        CloudStorageAccount.parse(storageConnectionString);

    // Create hello table client.
    CloudTableClient tableClient = storageAccount.createCloudTableClient();

    // Create a cloud table object for hello table.
    CloudTable cloudTable = tableClient.getTableReference("people");

    // Create a new customer entity.
    CustomerEntity customer1 = new CustomerEntity("Harp", "Walter");
    customer1.setEmail("Walter@contoso.com");
    customer1.setPhoneNumber("425-555-0101");

    // Create an operation tooadd hello new customer toohello people table.
    TableOperation insertCustomer1 = TableOperation.insertOrReplace(customer1);

    // Submit hello operation toohello table service.
    cloudTable.execute(insertCustomer1);
}
catch (Exception e)
{
    // Output hello stack trace.
    e.printStackTrace();
}
```

## <a name="how-to-insert-a-batch-of-entities"></a><span data-ttu-id="40dbc-144">Porady: wstawianie partię jednostek</span><span class="sxs-lookup"><span data-stu-id="40dbc-144">How to: Insert a batch of entities</span></span>
<span data-ttu-id="40dbc-145">Możesz wstawić partię jednostek toohello tabeli usługi w jednej operacji zapisu.</span><span class="sxs-lookup"><span data-stu-id="40dbc-145">You can insert a batch of entities toohello table service in one write operation.</span></span> <span data-ttu-id="40dbc-146">Witaj poniższy kod tworzy **TableBatchOperation** obiekt, a następnie dodaje trzy Wstaw tooit operacji.</span><span class="sxs-lookup"><span data-stu-id="40dbc-146">hello following code creates a **TableBatchOperation** object, then adds three insert operations tooit.</span></span> <span data-ttu-id="40dbc-147">Każda operacja insert jest dodawany przez utworzenie nowego obiektu jednostki, jego wartości ustawienia, a następnie wywołując hello **Wstaw** metody na powitania **TableBatchOperation** tooassociate hello jednostki o nowy obiekt operacji wstawiania.</span><span class="sxs-lookup"><span data-stu-id="40dbc-147">Each insert operation is added by creating a new entity object, setting its values, and then calling hello **insert** method on hello **TableBatchOperation** object tooassociate hello entity with a new insert operation.</span></span> <span data-ttu-id="40dbc-148">Następnie hello kod wywołuje **wykonania** na powitania **CloudTable** obiektu, w tabeli "osoby" hello i hello **TableBatchOperation** obiektu, który wysyła partii hello tabeli operacje toohello usługi magazynu w ramach pojedynczego żądania.</span><span class="sxs-lookup"><span data-stu-id="40dbc-148">Then hello code calls **execute** on hello **CloudTable** object, specifying hello "people" table and hello **TableBatchOperation** object, which sends hello batch of table operations toohello storage service in a single request.</span></span>

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount =
        CloudStorageAccount.parse(storageConnectionString);

    // Create hello table client.
    CloudTableClient tableClient = storageAccount.createCloudTableClient();

    // Define a batch operation.
    TableBatchOperation batchOperation = new TableBatchOperation();

    // Create a cloud table object for hello table.
    CloudTable cloudTable = tableClient.getTableReference("people");

    // Create a customer entity tooadd toohello table.
    CustomerEntity customer = new CustomerEntity("Smith", "Jeff");
    customer.setEmail("Jeff@contoso.com");
    customer.setPhoneNumber("425-555-0104");
    batchOperation.insertOrReplace(customer);

    // Create another customer entity tooadd toohello table.
    CustomerEntity customer2 = new CustomerEntity("Smith", "Ben");
    customer2.setEmail("Ben@contoso.com");
    customer2.setPhoneNumber("425-555-0102");
    batchOperation.insertOrReplace(customer2);

    // Create a third customer entity tooadd toohello table.
    CustomerEntity customer3 = new CustomerEntity("Smith", "Denise");
    customer3.setEmail("Denise@contoso.com");
    customer3.setPhoneNumber("425-555-0103");
    batchOperation.insertOrReplace(customer3);

    // Execute hello batch of operations on hello "people" table.
    cloudTable.execute(batchOperation);
}
catch (Exception e)
{
    // Output hello stack trace.
    e.printStackTrace();
}
```

<span data-ttu-id="40dbc-149">Niektóre elementy toonote dotyczące operacji zbiorczych:</span><span class="sxs-lookup"><span data-stu-id="40dbc-149">Some things toonote on batch operations:</span></span>

* <span data-ttu-id="40dbc-150">Możesz wykonać too100 insert, delete, scalania, Zamień, wstawiania lub scalania i wstawianie lub zamienianie operacji w dowolnej kombinacji w pojedynczej partii.</span><span class="sxs-lookup"><span data-stu-id="40dbc-150">You can perform up too100 insert, delete, merge, replace, insert or merge, and insert or replace operations in any combination in a single batch.</span></span>
* <span data-ttu-id="40dbc-151">Operacji zbiorczej może mieć operacji pobierania, jeśli jest jedyną operacją hello w partii hello.</span><span class="sxs-lookup"><span data-stu-id="40dbc-151">A batch operation can have a retrieve operation, if it is hello only operation in hello batch.</span></span>
* <span data-ttu-id="40dbc-152">Wszystkie jednostki w jednej operacji zbiorczej muszą mieć hello tego samego klucza partycji.</span><span class="sxs-lookup"><span data-stu-id="40dbc-152">All entities in a single batch operation must have hello same partition key.</span></span>
* <span data-ttu-id="40dbc-153">Operacji zbiorczej jest ograniczona tooa 4MB danych ładunku.</span><span class="sxs-lookup"><span data-stu-id="40dbc-153">A batch operation is limited tooa 4MB data payload.</span></span>

## <a name="how-to-retrieve-all-entities-in-a-partition"></a><span data-ttu-id="40dbc-154">Porady: pobieranie wszystkich jednostek w partycji</span><span class="sxs-lookup"><span data-stu-id="40dbc-154">How to: Retrieve all entities in a partition</span></span>
<span data-ttu-id="40dbc-155">tooquery tabelę dla jednostek w partycji, można użyć **TableQuery**.</span><span class="sxs-lookup"><span data-stu-id="40dbc-155">tooquery a table for entities in a partition, you can use a **TableQuery**.</span></span> <span data-ttu-id="40dbc-156">Wywołanie **TableQuery.from** toocreate zapytania dla konkretnej tabeli, która zwraca typ określony wynik.</span><span class="sxs-lookup"><span data-stu-id="40dbc-156">Call **TableQuery.from** toocreate a query on a particular table that returns a specified result type.</span></span> <span data-ttu-id="40dbc-157">Witaj następującego kodu Określa filtr jednostek, gdzie "Smith" jest kluczem partycji hello.</span><span class="sxs-lookup"><span data-stu-id="40dbc-157">hello following code specifies a filter for entities where 'Smith' is hello partition key.</span></span> <span data-ttu-id="40dbc-158">**TableQuery.generateFilterCondition** to metoda pomocnika toocreate filtrów do zapytania.</span><span class="sxs-lookup"><span data-stu-id="40dbc-158">**TableQuery.generateFilterCondition** is a helper method toocreate filters for queries.</span></span> <span data-ttu-id="40dbc-159">Wywołanie **gdzie** na powitania Odwołanie zwrócone przez hello **TableQuery.from** metody tooapply hello filtru toohello zapytania.</span><span class="sxs-lookup"><span data-stu-id="40dbc-159">Call **where** on hello reference returned by hello **TableQuery.from** method tooapply hello filter toohello query.</span></span> <span data-ttu-id="40dbc-160">Gdy hello zapytanie jest wykonywane przy użyciu wywołania zbyt**wykonania** na powitania **CloudTable** obiektu i zwraca **Iterator** z hello **CustomerEntity**określony typ wyniku.</span><span class="sxs-lookup"><span data-stu-id="40dbc-160">When hello query is executed with a call too**execute** on hello **CloudTable** object, it returns an **Iterator** with hello **CustomerEntity** result type specified.</span></span> <span data-ttu-id="40dbc-161">Następnie można użyć hello **iteratora** zwracane w dla każdej pętli tooconsume hello wyników.</span><span class="sxs-lookup"><span data-stu-id="40dbc-161">You can then use hello **Iterator** returned in a for each loop tooconsume hello results.</span></span> <span data-ttu-id="40dbc-162">Ten kod drukuje hello pola każdej jednostki w konsoli toohello wyników zapytania hello.</span><span class="sxs-lookup"><span data-stu-id="40dbc-162">This code prints hello fields of each entity in hello query results toohello console.</span></span>

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

    // Create hello table client.
    CloudTableClient tableClient = storageAccount.createCloudTableClient();

    // Create a cloud table object for hello table.
    CloudTable cloudTable = tableClient.getTableReference("people");

    // Create a filter condition where hello partition key is "Smith".
    String partitionFilter = TableQuery.generateFilterCondition(
        PARTITION_KEY,
        QueryComparisons.EQUAL,
        "Smith");

    // Specify a partition query, using "Smith" as hello partition key filter.
    TableQuery<CustomerEntity> partitionQuery =
        TableQuery.from(CustomerEntity.class)
        .where(partitionFilter);

    // Loop through hello results, displaying information about hello entity.
    for (CustomerEntity entity : cloudTable.execute(partitionQuery)) {
        System.out.println(entity.getPartitionKey() +
            " " + entity.getRowKey() +
            "\t" + entity.getEmail() +
            "\t" + entity.getPhoneNumber());
    }
}
catch (Exception e)
{
    // Output hello stack trace.
    e.printStackTrace();
}
```

## <a name="how-to-retrieve-a-range-of-entities-in-a-partition"></a><span data-ttu-id="40dbc-163">Porady: pobieranie zakresu jednostek w partycji</span><span class="sxs-lookup"><span data-stu-id="40dbc-163">How to: Retrieve a range of entities in a partition</span></span>
<span data-ttu-id="40dbc-164">Jeśli nie chcesz tooquery wszystkie hello jednostek w partycji, możesz określić zakres przy użyciu operatory porównania w filtrze.</span><span class="sxs-lookup"><span data-stu-id="40dbc-164">If you don't want tooquery all hello entities in a partition, you can specify a range by using comparison operators in a filter.</span></span> <span data-ttu-id="40dbc-165">Witaj następujące dwa filtry tooget wszystkich jednostek w partycji "Smith" gdzie hello klucz wiersza (imię) rozpoczyna się od litery się too'E łączy kod "w hello alfabetu.</span><span class="sxs-lookup"><span data-stu-id="40dbc-165">hello following code combines two filters tooget all entities in partition "Smith" where hello row key (first name) starts with a letter up too'E' in hello alphabet.</span></span> <span data-ttu-id="40dbc-166">Następnie drukuje wyniki zapytania hello.</span><span class="sxs-lookup"><span data-stu-id="40dbc-166">Then it prints hello query results.</span></span> <span data-ttu-id="40dbc-167">Jeśli używasz tabeli toohello dodanych jednostek hello w partii hello wstawić części tego przewodnika, tylko dwie jednostki są zwracane w tej chwili (Ben i Adam Nowak); Jan Kowalski nie jest włączony.</span><span class="sxs-lookup"><span data-stu-id="40dbc-167">If you use hello entities added toohello table in hello batch insert section of this guide, only two entities are returned this time (Ben and Denise Smith); Jeff Smith is not included.</span></span>

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

    // Create hello table client.
    CloudTableClient tableClient = storageAccount.createCloudTableClient();

    // Create a cloud table object for hello table.
    CloudTable cloudTable = tableClient.getTableReference("people");

    // Create a filter condition where hello partition key is "Smith".
    String partitionFilter = TableQuery.generateFilterCondition(
        PARTITION_KEY,
        QueryComparisons.EQUAL,
        "Smith");

    // Create a filter condition where hello row key is less than hello letter "E".
    String rowFilter = TableQuery.generateFilterCondition(
        ROW_KEY,
        QueryComparisons.LESS_THAN,
        "E");

    // Combine hello two conditions into a filter expression.
    String combinedFilter = TableQuery.combineFilters(partitionFilter,
        Operators.AND, rowFilter);

    // Specify a range query, using "Smith" as hello partition key,
    // with hello row key being up toohello letter "E".
    TableQuery<CustomerEntity> rangeQuery =
        TableQuery.from(CustomerEntity.class)
        .where(combinedFilter);

    // Loop through hello results, displaying information about hello entity
    for (CustomerEntity entity : cloudTable.execute(rangeQuery)) {
        System.out.println(entity.getPartitionKey() +
            " " + entity.getRowKey() +
            "\t" + entity.getEmail() +
            "\t" + entity.getPhoneNumber());
    }
}
catch (Exception e)
{
    // Output hello stack trace.
    e.printStackTrace();
}
```

## <a name="how-to-retrieve-a-single-entity"></a><span data-ttu-id="40dbc-168">Porady: pobieranie pojedynczej jednostki</span><span class="sxs-lookup"><span data-stu-id="40dbc-168">How to: Retrieve a single entity</span></span>
<span data-ttu-id="40dbc-169">Tooretrieve kwerendy można pisać w jednej, określonej jednostki.</span><span class="sxs-lookup"><span data-stu-id="40dbc-169">You can write a query tooretrieve a single, specific entity.</span></span> <span data-ttu-id="40dbc-170">Witaj poniższy kod wywołania **TableOperation.retrieve** z partycji klucza i wiersza parametrów klucza toospecify powitania klienta "Jan Kowalski", zamiast tworzyć **TableQuery** i przy użyciu filtrów toodo hello samo.</span><span class="sxs-lookup"><span data-stu-id="40dbc-170">hello following code calls **TableOperation.retrieve** with partition key and row key parameters toospecify hello customer "Jeff Smith", instead of creating a **TableQuery** and using filters toodo hello same thing.</span></span> <span data-ttu-id="40dbc-171">Po wykonaniu hello pobrać operacji zwraca tylko jedną jednostkę zamiast kolekcji.</span><span class="sxs-lookup"><span data-stu-id="40dbc-171">When executed, hello retrieve operation returns just one entity, rather than a collection.</span></span> <span data-ttu-id="40dbc-172">Witaj **getResultAsType** metody rzutuje typu toohello wyników hello hello docelowym przypisania, **CustomerEntity** obiektu.</span><span class="sxs-lookup"><span data-stu-id="40dbc-172">hello **getResultAsType** method casts hello result toohello type of hello assignment target, a **CustomerEntity** object.</span></span> <span data-ttu-id="40dbc-173">Jeśli ten typ nie jest zgodny z typem hello określonych dla zapytania hello, zostanie wygenerowany wyjątek.</span><span class="sxs-lookup"><span data-stu-id="40dbc-173">If this type is not compatible with hello type specified for hello query, an exception will be thrown.</span></span> <span data-ttu-id="40dbc-174">Jeśli jednostka nie ma dokładnie partycji i klucz wiersza zgodne, jest zwracana wartość null.</span><span class="sxs-lookup"><span data-stu-id="40dbc-174">A null value is returned if no entity has an exact partition and row key match.</span></span> <span data-ttu-id="40dbc-175">Określenie kluczy partycji i wiersza w zapytaniu jest hello najszybszy sposób tooretrieve pojedyncza jednostka z usługi tabeli hello.</span><span class="sxs-lookup"><span data-stu-id="40dbc-175">Specifying both partition and row keys in a query is hello fastest way tooretrieve a single entity from hello Table service.</span></span>

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount =
        CloudStorageAccount.parse(storageConnectionString);

    // Create hello table client.
    CloudTableClient tableClient = storageAccount.createCloudTableClient();

    // Create a cloud table object for hello table.
    CloudTable cloudTable = tableClient.getTableReference("people");

    // Retrieve hello entity with partition key of "Smith" and row key of "Jeff"
    TableOperation retrieveSmithJeff =
        TableOperation.retrieve("Smith", "Jeff", CustomerEntity.class);

    // Submit hello operation toohello table service and get hello specific entity.
    CustomerEntity specificEntity =
        cloudTable.execute(retrieveSmithJeff).getResultAsType();

    // Output hello entity.
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
    // Output hello stack trace.
    e.printStackTrace();
}
```

## <a name="how-to-modify-an-entity"></a><span data-ttu-id="40dbc-176">Porady: modyfikowanie jednostki</span><span class="sxs-lookup"><span data-stu-id="40dbc-176">How to: Modify an entity</span></span>
<span data-ttu-id="40dbc-177">toomodify jednostki, pobrać go z usługi tabeli hello, wprowadź obiekt jednostki toohello zmiany, a następnie zapisz zmiany hello usługi tabel toohello wstecz operacji zamiany lub scalania.</span><span class="sxs-lookup"><span data-stu-id="40dbc-177">toomodify an entity, retrieve it from hello table service, make changes toohello entity object, and save hello changes back toohello table service with a replace or merge operation.</span></span> <span data-ttu-id="40dbc-178">Witaj poniższy kod zmienia numer telefonu istniejącego klienta.</span><span class="sxs-lookup"><span data-stu-id="40dbc-178">hello following code changes an existing customer's phone number.</span></span> <span data-ttu-id="40dbc-179">Zamiast wywoływać metodę **TableOperation.insert** jak robiliśmy tooinsert ten kod wywołuje **TableOperation.replace**.</span><span class="sxs-lookup"><span data-stu-id="40dbc-179">Instead of calling **TableOperation.insert** like we did tooinsert, this code calls **TableOperation.replace**.</span></span> <span data-ttu-id="40dbc-180">Witaj **CloudTable.execute** metoda wywołuje hello usługi tabel i jednostki hello są zastępowane, chyba że inna aplikacja uległ zmianie w czasie hello ponieważ pobrany tej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="40dbc-180">hello **CloudTable.execute** method calls hello table service, and hello entity is replaced, unless another application changed it in hello time since this application retrieved it.</span></span> <span data-ttu-id="40dbc-181">W takim przypadku jest zwracany wyjątek, a hello jednostki musi być pobierane, zmodyfikowane i zapisane ponownie.</span><span class="sxs-lookup"><span data-stu-id="40dbc-181">When that happens, an exception is thrown, and hello entity must be retrieved, modified, and saved again.</span></span> <span data-ttu-id="40dbc-182">Ten wzorzec ponawiania optymistycznej współbieżności jest typowe w przypadku rozproszony systemem przechowywania.</span><span class="sxs-lookup"><span data-stu-id="40dbc-182">This optimistic concurrency retry pattern is common in a distributed storage system.</span></span>

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount =
        CloudStorageAccount.parse(storageConnectionString);

    // Create hello table client.
    CloudTableClient tableClient = storageAccount.createCloudTableClient();

    // Create a cloud table object for hello table.
    CloudTable cloudTable = tableClient.getTableReference("people");

    // Retrieve hello entity with partition key of "Smith" and row key of "Jeff".
    TableOperation retrieveSmithJeff =
        TableOperation.retrieve("Smith", "Jeff", CustomerEntity.class);

    // Submit hello operation toohello table service and get hello specific entity.
    CustomerEntity specificEntity =
        cloudTable.execute(retrieveSmithJeff).getResultAsType();

    // Specify a new phone number.
    specificEntity.setPhoneNumber("425-555-0105");

    // Create an operation tooreplace hello entity.
    TableOperation replaceEntity = TableOperation.replace(specificEntity);

    // Submit hello operation toohello table service.
    cloudTable.execute(replaceEntity);
}
catch (Exception e)
{
    // Output hello stack trace.
    e.printStackTrace();
}
```

## <a name="how-to-query-a-subset-of-entity-properties"></a><span data-ttu-id="40dbc-183">Porady: Tworzenie zapytania do podzbioru właściwości jednostki</span><span class="sxs-lookup"><span data-stu-id="40dbc-183">How to: Query a subset of entity properties</span></span>
<span data-ttu-id="40dbc-184">Tabela tooa kwerend może pobrać kilka właściwości jednostki.</span><span class="sxs-lookup"><span data-stu-id="40dbc-184">A query tooa table can retrieve just a few properties from an entity.</span></span> <span data-ttu-id="40dbc-185">Ta technika, zwana projekcją, redukuje przepustowość i może poprawiać wydajność zapytań, zwłaszcza w przypadku dużych jednostek.</span><span class="sxs-lookup"><span data-stu-id="40dbc-185">This technique, called projection, reduces bandwidth and can improve query performance, especially for large entities.</span></span> <span data-ttu-id="40dbc-186">Witaj zapytanie w hello następującego kodu używa hello **wybierz** metody tooreturn tylko hello adresy e-mail jednostek w tabeli hello.</span><span class="sxs-lookup"><span data-stu-id="40dbc-186">hello query in hello following code uses hello **select** method tooreturn only hello email addresses of entities in hello table.</span></span> <span data-ttu-id="40dbc-187">Hello wyniki są przedstawione jako kolekcja **ciąg** za pomocą hello **EntityResolver**, który hello konwersji typu na jednostkach hello zwrócony z serwera hello.</span><span class="sxs-lookup"><span data-stu-id="40dbc-187">hello results are projected into a collection of **String** with hello help of an **EntityResolver**, which does hello type conversion on hello entities returned from hello server.</span></span> <span data-ttu-id="40dbc-188">Dowiedz się więcej o projekcji w [tabel Azure: Introducing Upsert i projekcji zapytań][Azure Tables: Introducing Upsert and Query Projection].</span><span class="sxs-lookup"><span data-stu-id="40dbc-188">You can learn more about projection in [Azure Tables: Introducing Upsert and Query Projection][Azure Tables: Introducing Upsert and Query Projection].</span></span> <span data-ttu-id="40dbc-189">Należy pamiętać, że projekcji nie jest obsługiwana na powitania lokalnym emulatorze magazynu, dlatego ten kod zadziała tylko w przypadku użycia konta w usłudze tabel hello.</span><span class="sxs-lookup"><span data-stu-id="40dbc-189">Note that projection is not supported on hello local storage emulator, so this code runs only when using an account on hello table service.</span></span>

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount =
        CloudStorageAccount.parse(storageConnectionString);

    // Create hello table client.
    CloudTableClient tableClient = storageAccount.createCloudTableClient();

    // Create a cloud table object for hello table.
    CloudTable cloudTable = tableClient.getTableReference("people");

    // Define a projection query that retrieves only hello Email property
    TableQuery<CustomerEntity> projectionQuery =
        TableQuery.from(CustomerEntity.class)
        .select(new String[] {"Email"});

    // Define a Entity resolver tooproject hello entity toohello Email value.
    EntityResolver<String> emailResolver = new EntityResolver<String>() {
        @Override
        public String resolve(String PartitionKey, String RowKey, Date timeStamp, HashMap<String, EntityProperty> properties, String etag) {
            return properties.get("Email").getValueAsString();
        }
    };

    // Loop through hello results, displaying hello Email values.
    for (String projectedString :
        cloudTable.execute(projectionQuery, emailResolver)) {
            System.out.println(projectedString);
    }
}
catch (Exception e)
{
    // Output hello stack trace.
    e.printStackTrace();
}
```

## <a name="how-to-insert-or-replace-an-entity"></a><span data-ttu-id="40dbc-190">Porady: wstawianie lub zastępowanie jednostki</span><span class="sxs-lookup"><span data-stu-id="40dbc-190">How to: Insert or Replace an entity</span></span>
<span data-ttu-id="40dbc-191">Często ma tooadd tabeli tooa jednostki bez wiedzy o Jeśli już istnieje w tabeli hello.</span><span class="sxs-lookup"><span data-stu-id="40dbc-191">Often you want tooadd an entity tooa table without knowing if it already exists in hello table.</span></span> <span data-ttu-id="40dbc-192">Operacja wstawiania lub Zastąp umożliwia toomake pojedynczego żądania, które powoduje wstawienie hello jednostki, jeśli nie istnieje lub Zastąp hello jedną istniejących, jeśli istnieje.</span><span class="sxs-lookup"><span data-stu-id="40dbc-192">An insert-or-replace operation allows you toomake a single request which will insert hello entity if it does not exist or replace hello existing one if it does.</span></span> <span data-ttu-id="40dbc-193">Korzystając z poprzednich przykładach, hello następujący kod wstawia lub zamienia hello jednostki dla "Walter Harp".</span><span class="sxs-lookup"><span data-stu-id="40dbc-193">Building on prior examples, hello following code inserts or replaces hello entity for "Walter Harp".</span></span> <span data-ttu-id="40dbc-194">Po utworzeniu nowego obiektu, ten kod wywołuje hello **TableOperation.insertOrReplace** metody.</span><span class="sxs-lookup"><span data-stu-id="40dbc-194">After creating a new entity, this code calls hello **TableOperation.insertOrReplace** method.</span></span> <span data-ttu-id="40dbc-195">Ten kod wywołuje **wykonania** na powitania **CloudTable** obiekt z insert tabeli i hello hello lub Zastąp operacja tabeli jako parametry hello.</span><span class="sxs-lookup"><span data-stu-id="40dbc-195">This code then calls **execute** on hello **CloudTable** object with hello table and hello insert or replace table operation as hello parameters.</span></span> <span data-ttu-id="40dbc-196">tooupdate tylko część jednostki hello **TableOperation.insertOrMerge** metody można użyć zamiast niego.</span><span class="sxs-lookup"><span data-stu-id="40dbc-196">tooupdate only part of an entity, hello **TableOperation.insertOrMerge** method can be used instead.</span></span> <span data-ttu-id="40dbc-197">Należy pamiętać, że wstawianie lub zastępowanie nie jest obsługiwana na powitania lokalnym emulatorze magazynu, dlatego ten kod zadziała tylko w przypadku użycia konta w usłudze tabel hello.</span><span class="sxs-lookup"><span data-stu-id="40dbc-197">Note that insert-or-replace is not supported on hello local storage emulator, so this code runs only when using an account on hello table service.</span></span> <span data-ttu-id="40dbc-198">Możesz dowiedzieć się więcej o Wstawianie lub zastępowanie i Wstaw lub scalania w tym [tabel Azure: Introducing Upsert i projekcji zapytań][Azure Tables: Introducing Upsert and Query Projection].</span><span class="sxs-lookup"><span data-stu-id="40dbc-198">You can learn more about insert-or-replace and insert-or-merge in this [Azure Tables: Introducing Upsert and Query Projection][Azure Tables: Introducing Upsert and Query Projection].</span></span>

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount =
        CloudStorageAccount.parse(storageConnectionString);

    // Create hello table client.
    CloudTableClient tableClient = storageAccount.createCloudTableClient();

    // Create a cloud table object for hello table.
    CloudTable cloudTable = tableClient.getTableReference("people");

    // Create a new customer entity.
    CustomerEntity customer5 = new CustomerEntity("Harp", "Walter");
    customer5.setEmail("Walter@contoso.com");
    customer5.setPhoneNumber("425-555-0106");

    // Create an operation tooadd hello new customer toohello people table.
    TableOperation insertCustomer5 = TableOperation.insertOrReplace(customer5);

    // Submit hello operation toohello table service.
    cloudTable.execute(insertCustomer5);
}
catch (Exception e)
{
    // Output hello stack trace.
    e.printStackTrace();
}
```

## <a name="how-to-delete-an-entity"></a><span data-ttu-id="40dbc-199">Porady: Usuwanie jednostki</span><span class="sxs-lookup"><span data-stu-id="40dbc-199">How to: Delete an entity</span></span>
<span data-ttu-id="40dbc-200">Po jej pobraniu można z łatwością usunąć jednostkę.</span><span class="sxs-lookup"><span data-stu-id="40dbc-200">You can easily delete an entity after you have retrieved it.</span></span> <span data-ttu-id="40dbc-201">Po pobraniu jednostki hello wywołać **TableOperation.delete** z hello toodelete jednostki.</span><span class="sxs-lookup"><span data-stu-id="40dbc-201">Once hello entity is retrieved, call **TableOperation.delete** with hello entity toodelete.</span></span> <span data-ttu-id="40dbc-202">Następnie wywołaj **wykonania** na powitania **CloudTable** obiektu.</span><span class="sxs-lookup"><span data-stu-id="40dbc-202">Then call **execute** on hello **CloudTable** object.</span></span> <span data-ttu-id="40dbc-203">powitania po kod umożliwia pobranie i usunięcie jednostki klienta.</span><span class="sxs-lookup"><span data-stu-id="40dbc-203">hello following code retrieves and deletes a customer entity.</span></span>

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount =
        CloudStorageAccount.parse(storageConnectionString);

    // Create hello table client.
    CloudTableClient tableClient = storageAccount.createCloudTableClient();

    // Create a cloud table object for hello table.
    CloudTable cloudTable = tableClient.getTableReference("people");

    // Create an operation tooretrieve hello entity with partition key of "Smith" and row key of "Jeff".
    TableOperation retrieveSmithJeff = TableOperation.retrieve("Smith", "Jeff", CustomerEntity.class);

    // Retrieve hello entity with partition key of "Smith" and row key of "Jeff".
    CustomerEntity entitySmithJeff =
        cloudTable.execute(retrieveSmithJeff).getResultAsType();

    // Create an operation toodelete hello entity.
    TableOperation deleteSmithJeff = TableOperation.delete(entitySmithJeff);

    // Submit hello delete operation toohello table service.
    cloudTable.execute(deleteSmithJeff);
}
catch (Exception e)
{
    // Output hello stack trace.
    e.printStackTrace();
}
```

## <a name="how-to-delete-a-table"></a><span data-ttu-id="40dbc-204">Porady: usuwanie tabeli</span><span class="sxs-lookup"><span data-stu-id="40dbc-204">How to: Delete a table</span></span>
<span data-ttu-id="40dbc-205">Na koniec hello następującego kodu usuwa tabelę z konta magazynu.</span><span class="sxs-lookup"><span data-stu-id="40dbc-205">Finally, hello following code deletes a table from a storage account.</span></span> <span data-ttu-id="40dbc-206">Tabeli, który został usunięty będzie niedostępna toobe odtworzone w danym okresie czasu po usunięcie hello, zazwyczaj mniej niż 40 sekund.</span><span class="sxs-lookup"><span data-stu-id="40dbc-206">A table which has been deleted will be unavailable toobe recreated for a period of time following hello deletion, usually less than forty seconds.</span></span>

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount =
        CloudStorageAccount.parse(storageConnectionString);

    // Create hello table client.
    CloudTableClient tableClient = storageAccount.createCloudTableClient();

    // Delete hello table and all its data if it exists.
    CloudTable cloudTable = tableClient.getTableReference("people");
    cloudTable.deleteIfExists();
}
catch (Exception e)
{
    // Output hello stack trace.
    e.printStackTrace();
}
```
[!INCLUDE [storage-check-out-samples-java](../../includes/storage-check-out-samples-java.md)]

## <a name="next-steps"></a><span data-ttu-id="40dbc-207">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="40dbc-207">Next steps</span></span>

* <span data-ttu-id="40dbc-208">[Eksplorator magazynu Microsoft Azure](../vs-azure-tools-storage-manage-with-storage-explorer.md) jest bezpłatna, aplikacja autonomiczny firmy Microsoft, który umożliwia toowork wizualnie z danymi usługi Azure Storage w systemie Windows, macOS i Linux.</span><span class="sxs-lookup"><span data-stu-id="40dbc-208">[Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md) is a free, standalone app from Microsoft that enables you toowork visually with Azure Storage data on Windows, macOS, and Linux.</span></span>
* <span data-ttu-id="40dbc-209">[Magazyn Azure SDK dla języka Java][Azure Storage SDK for Java]</span><span class="sxs-lookup"><span data-stu-id="40dbc-209">[Azure Storage SDK for Java][Azure Storage SDK for Java]</span></span>
* <span data-ttu-id="40dbc-210">[Odwołanie do zestawu SDK klienta usługi Azure Storage][odwołaniazestawuSDKklientamagazynuAzure]</span><span class="sxs-lookup"><span data-stu-id="40dbc-210">[Azure Storage Client SDK Reference][Azure Storage Client SDK Reference]</span></span>
* <span data-ttu-id="40dbc-211">[Interfejs API REST usługi Azure Storage][Azure Storage REST API]</span><span class="sxs-lookup"><span data-stu-id="40dbc-211">[Azure Storage REST API][Azure Storage REST API]</span></span>
* <span data-ttu-id="40dbc-212">[Blog zespołu usługi Magazyn Azure][Azure Storage Team Blog]</span><span class="sxs-lookup"><span data-stu-id="40dbc-212">[Azure Storage Team Blog][Azure Storage Team Blog]</span></span>

<span data-ttu-id="40dbc-213">Aby uzyskać więcej informacji, odwiedź stronę [Azure dla deweloperów języka Java](/java/azure).</span><span class="sxs-lookup"><span data-stu-id="40dbc-213">For more information, visit [Azure for Java developers](/java/azure).</span></span>

[Azure SDK for Java]: http://go.microsoft.com/fwlink/?LinkID=525671
[Azure Storage SDK for Java]: https://github.com/azure/azure-storage-java
[Azure Storage SDK for Android]: https://github.com/azure/azure-storage-android
[odwołaniazestawuSDKklientamagazynuAzure]: http://dl.windowsazure.com/storage/javadoc/
[Azure Storage REST API]: https://msdn.microsoft.com/library/azure/dd179355.aspx
[Azure Storage Team Blog]: http://blogs.msdn.com/b/windowsazurestorage/
[Azure Tables: Introducing Upsert and Query Projection]: http://blogs.msdn.com/b/windowsazurestorage/archive/2011/09/15/windows-azure-tables-introducing-upsert-and-query-projection.aspx
