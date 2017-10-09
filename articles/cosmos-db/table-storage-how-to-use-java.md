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
# <a name="how-toouse-table-storage-from-java"></a>Jak toouse magazynu tabel w języku Java
[!INCLUDE [storage-selector-table-include](../../includes/storage-selector-table-include.md)]
[!INCLUDE [storage-table-cosmos-db-langsoon-tip-include](../../includes/storage-table-cosmos-db-langsoon-tip-include.md)]

## <a name="overview"></a>Omówienie
W tym przewodniku opisano sposób tooperform typowych scenariuszy przy użyciu hello usługi Magazyn tabel Azure. Hello przykłady są napisane w języku Java i używają hello [Azure Storage SDK for Java][Azure Storage SDK for Java]. Witaj omówione scenariusze obejmują **tworzenie**, **wyświetlania**, i **usuwanie** tabel, jak również **wstawianie**,  **wykonywanie zapytania**, **modyfikowanie**, i **usuwanie** jednostek w tabeli. Aby uzyskać więcej informacji w tabelach, zobacz hello [następne kroki](#Next-Steps) sekcji.

Uwaga: Zestaw SDK jest dostępny dla deweloperów, którzy korzystają z usługi Azure Storage na urządzeniach z systemem Android. Aby uzyskać więcej informacji, zobacz hello [zestawu SDK usługi Magazyn Azure dla systemu Android][Azure Storage SDK for Android].

[!INCLUDE [storage-table-concepts-include](../../includes/storage-table-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/storage-create-account-include.md)]

## <a name="create-a-java-application"></a>Tworzenie aplikacji Java
W tym przewodniku użyje funkcji magazynu, które mogą być uruchamiane w ramach aplikacji Java lokalnie lub w kodzie działających w roli sieci web lub roli proces roboczy na platformie Azure.

toodo tak, konieczne będzie tooinstall hello Java Development Kit (JDK) i utworzyć konto magazynu Azure w ramach subskrypcji platformy Azure. Po zostało to zrobione, należy tooverify spełniającym w systemie deweloperskim hello minimalne wymagania i zależności, które są wymienione w hello [Azure Storage SDK for Java] [ Azure Storage SDK for Java] repozytorium w witrynie GitHub. Jeżeli komputer spełnia te wymagania, należy wykonać hello instrukcje dotyczące pobierania i instalowania hello biblioteki magazynu Azure dla języka Java w systemie z tego repozytorium. Po wykonaniu tych zadań, będzie możliwe toocreate aplikacji Java, który używa hello przykłady w tym artykule.

## <a name="configure-your-application-tooaccess-table-storage"></a>Konfigurowanie magazynu tabeli tooaccess aplikacji
Dodaj powitania od góry toohello instrukcje importu miejscu toouse tabel tooaccess interfejsów API Microsoft Azure do przechowywania plików Java hello:

```java
// Include hello following imports toouse table APIs
import com.microsoft.azure.storage.*;
import com.microsoft.azure.storage.table.*;
import com.microsoft.azure.storage.table.TableQuery.*;
```

## <a name="set-up-an-azure-storage-connection-string"></a>Konfigurowanie parametrów połączenia usługi Azure storage
Klienta usługi Azure storage używa punkty końcowe magazynu połączenia ciąg toostore i poświadczeń do uzyskiwania dostępu do danych usługi zarządzania. Podczas uruchamiania w aplikacji klienckiej, należy podać parametry połączenia magazynu hello w hello zgodny z formatem, przy użyciu hello nazwy konta magazynu i hello podstawowy klucz dostępu dla konta magazynu hello na liście hello [portalu Azure](https://portal.azure.com)dla hello *AccountName* i *AccountKey* wartości. Ten przykład przedstawia, jak można zadeklarować ciąg połączenia pola statycznego toohold hello:

```java
// Define hello connection-string with your values.
public static final String storageConnectionString =
    "DefaultEndpointsProtocol=http;" +
    "AccountName=your_storage_account;" +
    "AccountKey=your_storage_account_key";
```

W aplikacji działającej w ramach roli w systemie Microsoft Azure, te parametry mogą być przechowywane w pliku konfiguracji usługi hello, *pliku ServiceConfiguration.cscfg*i jest dostępny z toohello wywołania  **RoleEnvironment.getConfigurationSettings** metody. Oto przykład pobierania hello parametrów połączenia z **ustawienie** elementu o nazwie *StorageConnectionString* w pliku konfiguracji usługi hello:

```java
// Retrieve storage account from connection-string.
String storageConnectionString =
    RoleEnvironment.getConfigurationSettings().get("StorageConnectionString");
```

Hello następujące przykłady założono, że użyto jednego z tych parametrów połączenia magazynu Witaj dwie metody tooget.

## <a name="how-to-create-a-table"></a>Porady: Tworzenie tabeli
A **CloudTableClient** obiektu pozwala pobierać obiekty odwołania do tabel i jednostek. Witaj poniższy kod tworzy **CloudTableClient** obiektu i używa go toocreate nowy **CloudTable** obiekt, który reprezentuje tabeli o nazwie "osoby". (Uwaga: istnieją dodatkowe sposoby toocreate **CloudStorageAccount** obiektów; Aby uzyskać więcej informacji, zobacz **CloudStorageAccount** w hello [odwołaniazestawuSDKklientamagazynuAzure].)

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

## <a name="how-to-list-hello-tables"></a>Porady: Lista hello tabel
tooget listę tabel, wywołanie hello **CloudTableClient.listTables()** tooretrieve metody iterable listę nazw tabel.

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

## <a name="how-to-add-an-entity-tooa-table"></a>Porady: Dodawanie tabeli tooa jednostki
Jednostki są mapowane tooJava obiektów za pomocą niestandardowej klasy implementacja **TableEntity**. Dla wygody hello **TableServiceEntity** klasa implementuje **TableEntity** i właściwości toomap odbicia używa metody toogetter i ustawiające o nazwie odpowiadającej hello właściwości. tooadd jednostki tooa tabeli, najpierw utworzyć klasę, która definiuje właściwości hello jednostki. Witaj poniższy kod definiuje klasę jednostki, która używa imienia klienta hello jako hello klucz wiersza i nazwiska jako klucza partycji hello. Razem klucz partycji i klucz wiersza jednoznacznie zidentyfikować hello jednostki w tabeli hello. Jednostki z tym samym kluczem partycji mogą być przeszukiwane szybciej niż jednostki o różnych kluczach partycji powitalne.

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

Operacje tabeli obejmujące jednostki wymagają **TableOperation** obiektu. Ten obiekt definiuje hello toobe działania wykonywane w ramach jednostki, które mogą być wykonywane przez **CloudTable** obiektu. Witaj poniższy kod tworzy nowe wystąpienie klasy hello **CustomerEntity** klasy z niektórych toobe dane klienta przechowywane. Witaj kod wywołuje dalej **TableOperation.insertOrReplace** toocreate **TableOperation** obiekt tooinsert jednostki do tabeli, a skojarzone hello nowych **CustomerEntity**z nim. Na koniec hello kod wywołuje hello **wykonania** metody na powitania **CloudTable** obiektu, w tabeli "osoby" hello i hello nowe **TableOperation**, które wysyła następnie żądanie toohello magazynu usługi tooinsert hello nowej jednostce klienta w tabeli "osoby" hello, lub Zastąp hello jednostki, jeśli już istnieje.

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

## <a name="how-to-insert-a-batch-of-entities"></a>Porady: wstawianie partię jednostek
Możesz wstawić partię jednostek toohello tabeli usługi w jednej operacji zapisu. Witaj poniższy kod tworzy **TableBatchOperation** obiekt, a następnie dodaje trzy Wstaw tooit operacji. Każda operacja insert jest dodawany przez utworzenie nowego obiektu jednostki, jego wartości ustawienia, a następnie wywołując hello **Wstaw** metody na powitania **TableBatchOperation** tooassociate hello jednostki o nowy obiekt operacji wstawiania. Następnie hello kod wywołuje **wykonania** na powitania **CloudTable** obiektu, w tabeli "osoby" hello i hello **TableBatchOperation** obiektu, który wysyła partii hello tabeli operacje toohello usługi magazynu w ramach pojedynczego żądania.

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

Niektóre elementy toonote dotyczące operacji zbiorczych:

* Możesz wykonać too100 insert, delete, scalania, Zamień, wstawiania lub scalania i wstawianie lub zamienianie operacji w dowolnej kombinacji w pojedynczej partii.
* Operacji zbiorczej może mieć operacji pobierania, jeśli jest jedyną operacją hello w partii hello.
* Wszystkie jednostki w jednej operacji zbiorczej muszą mieć hello tego samego klucza partycji.
* Operacji zbiorczej jest ograniczona tooa 4MB danych ładunku.

## <a name="how-to-retrieve-all-entities-in-a-partition"></a>Porady: pobieranie wszystkich jednostek w partycji
tooquery tabelę dla jednostek w partycji, można użyć **TableQuery**. Wywołanie **TableQuery.from** toocreate zapytania dla konkretnej tabeli, która zwraca typ określony wynik. Witaj następującego kodu Określa filtr jednostek, gdzie "Smith" jest kluczem partycji hello. **TableQuery.generateFilterCondition** to metoda pomocnika toocreate filtrów do zapytania. Wywołanie **gdzie** na powitania Odwołanie zwrócone przez hello **TableQuery.from** metody tooapply hello filtru toohello zapytania. Gdy hello zapytanie jest wykonywane przy użyciu wywołania zbyt**wykonania** na powitania **CloudTable** obiektu i zwraca **Iterator** z hello **CustomerEntity**określony typ wyniku. Następnie można użyć hello **iteratora** zwracane w dla każdej pętli tooconsume hello wyników. Ten kod drukuje hello pola każdej jednostki w konsoli toohello wyników zapytania hello.

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

## <a name="how-to-retrieve-a-range-of-entities-in-a-partition"></a>Porady: pobieranie zakresu jednostek w partycji
Jeśli nie chcesz tooquery wszystkie hello jednostek w partycji, możesz określić zakres przy użyciu operatory porównania w filtrze. Witaj następujące dwa filtry tooget wszystkich jednostek w partycji "Smith" gdzie hello klucz wiersza (imię) rozpoczyna się od litery się too'E łączy kod "w hello alfabetu. Następnie drukuje wyniki zapytania hello. Jeśli używasz tabeli toohello dodanych jednostek hello w partii hello wstawić części tego przewodnika, tylko dwie jednostki są zwracane w tej chwili (Ben i Adam Nowak); Jan Kowalski nie jest włączony.

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

## <a name="how-to-retrieve-a-single-entity"></a>Porady: pobieranie pojedynczej jednostki
Tooretrieve kwerendy można pisać w jednej, określonej jednostki. Witaj poniższy kod wywołania **TableOperation.retrieve** z partycji klucza i wiersza parametrów klucza toospecify powitania klienta "Jan Kowalski", zamiast tworzyć **TableQuery** i przy użyciu filtrów toodo hello samo. Po wykonaniu hello pobrać operacji zwraca tylko jedną jednostkę zamiast kolekcji. Witaj **getResultAsType** metody rzutuje typu toohello wyników hello hello docelowym przypisania, **CustomerEntity** obiektu. Jeśli ten typ nie jest zgodny z typem hello określonych dla zapytania hello, zostanie wygenerowany wyjątek. Jeśli jednostka nie ma dokładnie partycji i klucz wiersza zgodne, jest zwracana wartość null. Określenie kluczy partycji i wiersza w zapytaniu jest hello najszybszy sposób tooretrieve pojedyncza jednostka z usługi tabeli hello.

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

## <a name="how-to-modify-an-entity"></a>Porady: modyfikowanie jednostki
toomodify jednostki, pobrać go z usługi tabeli hello, wprowadź obiekt jednostki toohello zmiany, a następnie zapisz zmiany hello usługi tabel toohello wstecz operacji zamiany lub scalania. Witaj poniższy kod zmienia numer telefonu istniejącego klienta. Zamiast wywoływać metodę **TableOperation.insert** jak robiliśmy tooinsert ten kod wywołuje **TableOperation.replace**. Witaj **CloudTable.execute** metoda wywołuje hello usługi tabel i jednostki hello są zastępowane, chyba że inna aplikacja uległ zmianie w czasie hello ponieważ pobrany tej aplikacji. W takim przypadku jest zwracany wyjątek, a hello jednostki musi być pobierane, zmodyfikowane i zapisane ponownie. Ten wzorzec ponawiania optymistycznej współbieżności jest typowe w przypadku rozproszony systemem przechowywania.

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

## <a name="how-to-query-a-subset-of-entity-properties"></a>Porady: Tworzenie zapytania do podzbioru właściwości jednostki
Tabela tooa kwerend może pobrać kilka właściwości jednostki. Ta technika, zwana projekcją, redukuje przepustowość i może poprawiać wydajność zapytań, zwłaszcza w przypadku dużych jednostek. Witaj zapytanie w hello następującego kodu używa hello **wybierz** metody tooreturn tylko hello adresy e-mail jednostek w tabeli hello. Hello wyniki są przedstawione jako kolekcja **ciąg** za pomocą hello **EntityResolver**, który hello konwersji typu na jednostkach hello zwrócony z serwera hello. Dowiedz się więcej o projekcji w [tabel Azure: Introducing Upsert i projekcji zapytań][Azure Tables: Introducing Upsert and Query Projection]. Należy pamiętać, że projekcji nie jest obsługiwana na powitania lokalnym emulatorze magazynu, dlatego ten kod zadziała tylko w przypadku użycia konta w usłudze tabel hello.

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

## <a name="how-to-insert-or-replace-an-entity"></a>Porady: wstawianie lub zastępowanie jednostki
Często ma tooadd tabeli tooa jednostki bez wiedzy o Jeśli już istnieje w tabeli hello. Operacja wstawiania lub Zastąp umożliwia toomake pojedynczego żądania, które powoduje wstawienie hello jednostki, jeśli nie istnieje lub Zastąp hello jedną istniejących, jeśli istnieje. Korzystając z poprzednich przykładach, hello następujący kod wstawia lub zamienia hello jednostki dla "Walter Harp". Po utworzeniu nowego obiektu, ten kod wywołuje hello **TableOperation.insertOrReplace** metody. Ten kod wywołuje **wykonania** na powitania **CloudTable** obiekt z insert tabeli i hello hello lub Zastąp operacja tabeli jako parametry hello. tooupdate tylko część jednostki hello **TableOperation.insertOrMerge** metody można użyć zamiast niego. Należy pamiętać, że wstawianie lub zastępowanie nie jest obsługiwana na powitania lokalnym emulatorze magazynu, dlatego ten kod zadziała tylko w przypadku użycia konta w usłudze tabel hello. Możesz dowiedzieć się więcej o Wstawianie lub zastępowanie i Wstaw lub scalania w tym [tabel Azure: Introducing Upsert i projekcji zapytań][Azure Tables: Introducing Upsert and Query Projection].

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

## <a name="how-to-delete-an-entity"></a>Porady: Usuwanie jednostki
Po jej pobraniu można z łatwością usunąć jednostkę. Po pobraniu jednostki hello wywołać **TableOperation.delete** z hello toodelete jednostki. Następnie wywołaj **wykonania** na powitania **CloudTable** obiektu. powitania po kod umożliwia pobranie i usunięcie jednostki klienta.

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

## <a name="how-to-delete-a-table"></a>Porady: usuwanie tabeli
Na koniec hello następującego kodu usuwa tabelę z konta magazynu. Tabeli, który został usunięty będzie niedostępna toobe odtworzone w danym okresie czasu po usunięcie hello, zazwyczaj mniej niż 40 sekund.

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

## <a name="next-steps"></a>Następne kroki

* [Eksplorator magazynu Microsoft Azure](../vs-azure-tools-storage-manage-with-storage-explorer.md) jest bezpłatna, aplikacja autonomiczny firmy Microsoft, który umożliwia toowork wizualnie z danymi usługi Azure Storage w systemie Windows, macOS i Linux.
* [Magazyn Azure SDK dla języka Java][Azure Storage SDK for Java]
* [Odwołanie do zestawu SDK klienta usługi Azure Storage][odwołaniazestawuSDKklientamagazynuAzure]
* [Interfejs API REST usługi Azure Storage][Azure Storage REST API]
* [Blog zespołu usługi Magazyn Azure][Azure Storage Team Blog]

Aby uzyskać więcej informacji, odwiedź stronę [Azure dla deweloperów języka Java](/java/azure).

[Azure SDK for Java]: http://go.microsoft.com/fwlink/?LinkID=525671
[Azure Storage SDK for Java]: https://github.com/azure/azure-storage-java
[Azure Storage SDK for Android]: https://github.com/azure/azure-storage-android
[odwołaniazestawuSDKklientamagazynuAzure]: http://dl.windowsazure.com/storage/javadoc/
[Azure Storage REST API]: https://msdn.microsoft.com/library/azure/dd179355.aspx
[Azure Storage Team Blog]: http://blogs.msdn.com/b/windowsazurestorage/
[Azure Tables: Introducing Upsert and Query Projection]: http://blogs.msdn.com/b/windowsazurestorage/archive/2011/09/15/windows-azure-tables-introducing-upsert-and-query-projection.aspx
