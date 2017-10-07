---
title: "Magazyn tabel toouse aaaHow za pomocą języka PHP | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toouse hello usługi tabel z PHP toocreate i usunąć tabeli i wstawiania, usuwania i tabeli hello zapytania."
services: cosmos-db
documentationcenter: php
author: mimig1
manager: jhubbard
editor: tysonn
ms.assetid: 1e57f371-6208-4753-b2a0-05db4aede8e3
ms.service: cosmos-db
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: php
ms.topic: article
ms.date: 12/08/2016
ms.author: mimig
ms.openlocfilehash: 5b7c92221069d1c2a6ca951c06ae8eea8bb8478c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-table-storage-from-php"></a>Jak toouse tabeli magazynu w języku PHP
[!INCLUDE [storage-selector-table-include](../../includes/storage-selector-table-include.md)]
[!INCLUDE [storage-table-cosmos-db-langsoon-tip-include](../../includes/storage-table-cosmos-db-langsoon-tip-include.md)]

## <a name="overview"></a>Omówienie
Ten przewodnik przedstawia, jak tooperform typowych scenariuszy przy użyciu hello usługi tabel Azure. Przykłady Hello są zapisywane w kodzie PHP i używają hello [zestaw Azure SDK for PHP][download]. Witaj omówione scenariusze obejmują **tworzenia i usuwania tabeli i wstawianie, usuwanie i badania jednostek w tabeli**. Aby uzyskać więcej informacji na powitania usługi tabel Azure, zobacz hello [następne kroki](#next-steps) sekcji.

[!INCLUDE [storage-table-concepts-include](../../includes/storage-table-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/storage-create-account-include.md)]

## <a name="create-a-php-application"></a>Tworzenie aplikacji PHP
Witaj tylko do tworzenia aplikacji PHP, który uzyskuje dostęp do usługi Azure tabeli hello wymaganiem hello odwołuje się do klas w hello Azure SDK for PHP z w kodzie. Można użyć dowolnego toocreate narzędzi rozwoju aplikacji, łącznie z Notatnika.

W tym przewodniku korzystanie z funkcji usługi tabeli, które mogą być wywoływane w ramach aplikacji PHP lokalnie lub w kodzie działających w roli sieci web platformy Azure, roli procesu roboczego lub witryny sieci Web.

## <a name="get-hello-azure-client-libraries"></a>Pobierz bibliotek klienckich hello Azure
[!INCLUDE [get-client-libraries](../../includes/get-client-libraries.md)]

## <a name="configure-your-application-tooaccess-hello-table-service"></a>Konfigurowanie usługi aplikacji tooaccess hello tabeli
Usługa tabel Azure hello toouse interfejsów API, musisz:

1. Plik automatycznej ładowarki hello odwołania przy użyciu hello [require_once] [ require_once] instrukcji, i
2. Odwoływać się do wszystkich klas, których może używać.

Witaj poniższy przykład przedstawia sposób tooinclude hello hello plików i odwołanie automatycznej ładowarki **ServicesBuilder** klasy.

> [!NOTE]
> Przykłady Hello w tym artykule przyjęto założenie, że zainstalowano hello bibliotek klienckich PHP na platformie Azure za pośrednictwem Composer. Biblioteki hello zainstalować ręcznie, konieczne będzie tooreference hello <code>WindowsAzure.php</code> automatycznej ładowarki pliku.
>
>

```php
require_once 'vendor/autoload.php';
use WindowsAzure\Common\ServicesBuilder;
```

W poniższych przykładach hello, hello `require_once` instrukcji jest zawsze widoczne, ale odwołuje się tylko hello klasy niezbędne do tooexecute przykład hello.

## <a name="set-up-an-azure-storage-connection"></a>Konfigurowanie połączenia z magazynem Azure
tooinstantiate klienta usługi tabel Azure, musisz najpierw mieć prawidłowe parametry połączenia. format Hello hello ciąg połączenia usługi tabeli jest:

Aby uzyskać dostęp do usługi na żywo:

```php
DefaultEndpointsProtocol=[http|https];AccountName=[yourAccount];AccountKey=[yourKey]
```

Aby uzyskać dostęp do magazynu emulatora hello:

```php
UseDevelopmentStorage=true
```

toocreate dowolnego klienta usługi Azure należy toouse hello **ServicesBuilder** klasy. Możesz:

* Przekaż połączenia hello ciągu bezpośrednio tooit lub
* Użyj hello **CloudConfigurationManager (CCM)** toocheck zewnętrzne wiele źródeł dla parametrów połączenia hello:
  * Domyślnie pochodzi z obsługą jednego źródła zewnętrznego — zmienne środowiskowe
  * można dodać nowych źródeł, rozszerzając hello **ConnectionStringSource** — klasa

Przykłady hello opisana w tym temacie hello parametry połączenia zostaną przekazane bezpośrednio.

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;

$tableRestProxy = ServicesBuilder::getInstance()->createTableService($connectionString);
```

## <a name="create-a-table"></a>Tworzenie tabeli
A **TableRestProxy** obiektu pozwala utworzyć tabelę z hello **createTable** metody. Podczas tworzenia tabeli, można ustawić limitu czasu usługi tabeli hello. (Aby uzyskać więcej informacji o tabeli hello upłynięcia limitu czasu usługi, zobacz [ustawienie przekroczeń limitu czasu dla operacji usługi tabeli][table-service-timeouts].)

```php
require_once 'vendor\autoload.php';

use WindowsAzure\Common\ServicesBuilder;
use MicrosoftAzure\Storage\Common\ServiceException;

// Create table REST proxy.
$tableRestProxy = ServicesBuilder::getInstance()->createTableService($connectionString);

try    {
    // Create table.
    $tableRestProxy->createTable("mytable");
}
catch(ServiceException $e){
    $code = $e->getCode();
    $error_message = $e->getMessage();
    // Handle exception based on error codes and messages.
    // Error codes and messages can be found here:
    // http://msdn.microsoft.com/library/azure/dd179438.aspx
}
```

Aby uzyskać informacji o ograniczeniach dotyczących nazw tabeli, zobacz [hello opis modelu danych usługi tabel][table-data-model].

## <a name="add-an-entity-tooa-table"></a>Dodaj tabelę tooa jednostki
tooadd tabeli tooa jednostki, Utwórz nową **jednostki** obiektu i przekaż go za**TableRestProxy -> insertEntity**. Należy pamiętać, że podczas tworzenia obiektu, należy określić `PartitionKey` i `RowKey`. Te są hello unikatowych identyfikatorów dla jednostek i wartości, które można wykonać zapytania znacznie szybciej niż inne właściwości jednostki. Witaj system używa `PartitionKey` tooautomatically rozpowszechniać jednostek tabeli hello przez wiele węzłów magazynu. Jednostki z hello sam `PartitionKey` są przechowywane na powitania tym samym węźle. (Operacje na wiele jednostek przechowywanych na powitania wykonać na tym samym węźle lepszym rozwiązaniem niż na jednostek przechowywanych w różnych węzłach.) Witaj `RowKey` jest unikatowy identyfikator hello jednostek w partycji.

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;
use MicrosoftAzure\Storage\Common\ServiceException;
use MicrosoftAzure\Storage\Table\Models\Entity;
use MicrosoftAzure\Storage\Table\Models\EdmType;

// Create table REST proxy.
$tableRestProxy = ServicesBuilder::getInstance()->createTableService($connectionString);

$entity = new Entity();
$entity->setPartitionKey("tasksSeattle");
$entity->setRowKey("1");
$entity->addProperty("Description", null, "Take out hello trash.");
$entity->addProperty("DueDate",
                        EdmType::DATETIME,
                        new DateTime("2012-11-05T08:15:00-08:00"));
$entity->addProperty("Location", EdmType::STRING, "Home");

try{
    $tableRestProxy->insertEntity("mytable", $entity);
}
catch(ServiceException $e){
    // Handle exception based on error codes and messages.
    // Error codes and messages are here:
    // http://msdn.microsoft.com/library/azure/dd179438.aspx
    $code = $e->getCode();
    $error_message = $e->getMessage();
}
```

Informacje dotyczące właściwości i typów, zobacz [hello opis modelu danych usługi tabel][table-data-model].

Witaj **TableRestProxy** klasy oferuje dwie alternatywne metody Wstawianie jednostek: **insertOrMergeEntity** i **insertOrReplaceEntity**. toouse tych metod, Utwórz nową **jednostki** i przekaż go jako parametru metody tooeither. Każda metoda powoduje wstawienie hello jednostki, jeśli nie istnieje. Jeśli istnieje już jednostka hello, **insertOrMergeEntity** aktualizacji wartości właściwości, jeśli hello właściwości już istnieje i dodaje nowe właściwości nie są dostępne, podczas gdy **insertOrReplaceEntity** całkowicie zastępuje istniejącej jednostki. powitania po przykładzie pokazano, jak toouse **insertOrMergeEntity**. Jeśli hello jednostki o `PartitionKey` "tasksSeattle" i `RowKey` "1" nie istnieje, zostanie on włożony. Jednak jeśli wcześniej wstawione (jak pokazano w powyższym przykładzie hello), hello `DueDate` właściwość zostanie zaktualizowana i hello `Status` właściwość zostanie dodany. Witaj `Description` i `Location` są również zaktualizować właściwości, ale z wartościami które skutecznie pozostaw je bez zmian. Jeśli te dwie właściwości to drugie nie zostały dodane, jak pokazano w przykładzie hello, ale znajdował się na jednostkę docelową hello, ich istniejące wartości pozostanie bez zmian.

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;
use MicrosoftAzure\Storage\Common\ServiceException;
use MicrosoftAzure\Storage\Table\Models\Entity;
use MicrosoftAzure\Storage\Table\Models\EdmType;

// Create table REST proxy.
$tableRestProxy = ServicesBuilder::getInstance()->createTableService($connectionString);

//Create new entity.
$entity = new Entity();

// PartitionKey and RowKey are required.
$entity->setPartitionKey("tasksSeattle");
$entity->setRowKey("1");

// If entity exists, existing properties are updated with new values and
// new properties are added. Missing properties are unchanged.
$entity->addProperty("Description", null, "Take out hello trash.");
$entity->addProperty("DueDate", EdmType::DATETIME, new DateTime()); // Modified hello DueDate field.
$entity->addProperty("Location", EdmType::STRING, "Home");
$entity->addProperty("Status", EdmType::STRING, "Complete"); // Added Status field.

try    {
    // Calling insertOrReplaceEntity, instead of insertOrMergeEntity as shown,
    // would simply replace hello entity with PartitionKey "tasksSeattle" and RowKey "1".
    $tableRestProxy->insertOrMergeEntity("mytable", $entity);
}
catch(ServiceException $e){
    // Handle exception based on error codes and messages.
    // Error codes and messages are here:
    // http://msdn.microsoft.com/library/azure/dd179438.aspx
    $code = $e->getCode();
    $error_message = $e->getMessage();
    echo $code.": ".$error_message."<br />";
}
```

## <a name="retrieve-a-single-entity"></a>Pobieranie pojedynczej jednostki
Witaj **TableRestProxy -> getEntity** metoda pozwala tooretrieve pojedynczej jednostki przez wykonanie zapytania dotyczącego jego `PartitionKey` i `RowKey`. W poniższym przykładzie hello, hello klucza partycji `tasksSeattle` i klucz wiersza `1` są przekazywane toohello **getEntity** metody.

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;
use MicrosoftAzure\Storage\Common\ServiceException;

// Create table REST proxy.
$tableRestProxy = ServicesBuilder::getInstance()->createTableService($connectionString);

try    {
    $result = $tableRestProxy->getEntity("mytable", "tasksSeattle", 1);
}
catch(ServiceException $e){
    // Handle exception based on error codes and messages.
    // Error codes and messages are here:
    // http://msdn.microsoft.com/library/azure/dd179438.aspx
    $code = $e->getCode();
    $error_message = $e->getMessage();
    echo $code.": ".$error_message."<br />";
}

$entity = $result->getEntity();

echo $entity->getPartitionKey().":".$entity->getRowKey();
```

## <a name="retrieve-all-entities-in-a-partition"></a>Pobieranie wszystkich jednostek w partycji
Zapytania jednostki są konstruowane przy użyciu filtrów (Aby uzyskać więcej informacji, zobacz [badania tabel i jednostek][filters]). tooretrieve wszystkich jednostek w partycji, użyj filtru hello "PartitionKey eq *nazwa_partycji*". powitania po przykładzie pokazano, jak tooretrieve wszystkich jednostek w hello `tasksSeattle` partycji, przekazując toohello filtru **queryEntities** metody.

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;
use MicrosoftAzure\Storage\Common\ServiceException;

// Create table REST proxy.
$tableRestProxy = ServicesBuilder::getInstance()->createTableService($connectionString);

$filter = "PartitionKey eq 'tasksSeattle'";

try    {
    $result = $tableRestProxy->queryEntities("mytable", $filter);
}
catch(ServiceException $e){
    // Handle exception based on error codes and messages.
    // Error codes and messages are here:
    // http://msdn.microsoft.com/library/azure/dd179438.aspx
    $code = $e->getCode();
    $error_message = $e->getMessage();
    echo $code.": ".$error_message."<br />";
}

$entities = $result->getEntities();

foreach($entities as $entity){
    echo $entity->getPartitionKey().":".$entity->getRowKey()."<br />";
}
```

## <a name="retrieve-a-subset-of-entities-in-a-partition"></a>Pobrać podzbiór jednostek w partycji
Witaj tego samego wzorca użyty w poprzednim przykładzie hello mogą być używane tooretrieve dowolny podzbiór jednostek w partycji. podzbiór Hello jednostek, możesz pobrać są określane przez filtr hello używasz (Aby uzyskać więcej informacji, zobacz [badania tabel i jednostek][filters]) .hello po przykładzie pokazano, jak toouse tooretrieve filtru wszystkie jednostki z określonym `Location` i `DueDate` mniej niż określona data.

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;
use MicrosoftAzure\Storage\Common\ServiceException;

// Create table REST proxy.
$tableRestProxy = ServicesBuilder::getInstance()->createTableService($connectionString);

$filter = "Location eq 'Office' and DueDate lt '2012-11-5'";

try    {
    $result = $tableRestProxy->queryEntities("mytable", $filter);
}
catch(ServiceException $e){
    // Handle exception based on error codes and messages.
    // Error codes and messages are here:
    // http://msdn.microsoft.com/library/azure/dd179438.aspx
    $code = $e->getCode();
    $error_message = $e->getMessage();
    echo $code.": ".$error_message."<br />";
}

$entities = $result->getEntities();

foreach($entities as $entity){
    echo $entity->getPartitionKey().":".$entity->getRowKey()."<br />";
}
```

## <a name="retrieve-a-subset-of-entity-properties"></a>Pobrać podzbioru właściwości jednostki
Zapytania można pobrać podzbioru właściwości jednostki. Ta technika, zwana *projekcji*, redukuje przepustowość i może poprawiać wydajność zapytań, zwłaszcza w przypadku dużych jednostek. pobrać toobe właściwości toospecify, przekazywania hello nazwy hello właściwości toohello **zapytania -> addSelectField** metody. Można wywołać tej metody tooadd wiele razy więcej właściwości. Po wykonaniu **TableRestProxy -> queryEntities**, hello zwrócił jednostek będzie miał tylko hello wybrane właściwości. (Tooreturn podzbiór jednostek tabeli należy użyć filtru jak pokazano w zapytaniach hello powyżej).

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;
use MicrosoftAzure\Storage\Common\ServiceException;
use MicrosoftAzure\Storage\Table\Models\QueryEntitiesOptions;

// Create table REST proxy.
$tableRestProxy = ServicesBuilder::getInstance()->createTableService($connectionString);

$options = new QueryEntitiesOptions();
$options->addSelectField("Description");

try    {
    $result = $tableRestProxy->queryEntities("mytable", $options);
}
catch(ServiceException $e){
    // Handle exception based on error codes and messages.
    // Error codes and messages are here:
    // http://msdn.microsoft.com/library/azure/dd179438.aspx
    $code = $e->getCode();
    $error_message = $e->getMessage();
    echo $code.": ".$error_message."<br />";
}

// All entities in hello table are returned, regardless of whether
// they have hello Description field.
// toolimit hello results returned, use a filter.
$entities = $result->getEntities();

foreach($entities as $entity){
    $description = $entity->getProperty("Description")->getValue();
    echo $description."<br />";
}
```

## <a name="update-an-entity"></a>Aktualizuj jednostkę
Istniejącej jednostki można aktualizować za pomocą hello **jednostki -> setProperty** i **jednostki -> addProperty** w hello jednostki, a następnie wywołania metod **TableRestProxy -> updateEntity** . Witaj poniższy przykład pobiera jednostki, modyfikuje jedną właściwość usuwa innej właściwości i dodaje nową właściwość. Uwaga usunąć właściwość, ustawiając wartość zbyt**null**.

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;
use MicrosoftAzure\Storage\Common\ServiceException;
use MicrosoftAzure\Storage\Table\Models\Entity;
use MicrosoftAzure\Storage\Table\Models\EdmType;

// Create table REST proxy.
$tableRestProxy = ServicesBuilder::getInstance()->createTableService($connectionString);

$result = $tableRestProxy->getEntity("mytable", "tasksSeattle", 1);

$entity = $result->getEntity();

$entity->setPropertyValue("DueDate", new DateTime()); //Modified DueDate.

$entity->setPropertyValue("Location", null); //Removed Location.

$entity->addProperty("Status", EdmType::STRING, "In progress"); //Added Status.

try    {
    $tableRestProxy->updateEntity("mytable", $entity);
}
catch(ServiceException $e){
    // Handle exception based on error codes and messages.
    // Error codes and messages are here:
    // http://msdn.microsoft.com/library/azure/dd179438.aspx
    $code = $e->getCode();
    $error_message = $e->getMessage();
    echo $code.": ".$error_message."<br />";
}
```

## <a name="delete-an-entity"></a>Usuwanie jednostki
toodelete jednostki, Przekaż hello nazwę tabeli i jednostki hello `PartitionKey` i `RowKey` toohello **TableRestProxy -> deleteEntity** metody.

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;
use MicrosoftAzure\Storage\Common\ServiceException;

// Create table REST proxy.
$tableRestProxy = ServicesBuilder::getInstance()->createTableService($connectionString);

try    {
    // Delete entity.
    $tableRestProxy->deleteEntity("mytable", "tasksSeattle", "2");
}
catch(ServiceException $e){
    // Handle exception based on error codes and messages.
    // Error codes and messages are here:
    // http://msdn.microsoft.com/library/azure/dd179438.aspx
    $code = $e->getCode();
    $error_message = $e->getMessage();
    echo $code.": ".$error_message."<br />";
}
```

Należy pamiętać, że kontrolach współbieżności, można ustawić hello Etag dla toobe jednostki usunięte przy użyciu hello **DeleteEntityOptions -> setEtag** — metoda i przekazywanie hello **DeleteEntityOptions** obiekt zbyt**deleteEntity** jako czwartego parametru.

## <a name="batch-table-operations"></a>Operacje tabeli partii
Witaj **TableRestProxy -> partii** metoda pozwala tooexecute wiele operacji w ramach pojedynczego żądania. Hello wzorzec tutaj obejmuje dodanie operacji za**BatchRequest** obiektu, a następnie przekazywanie hello **BatchRequest** obiekt toohello **TableRestProxy -> partii** metody. tooadd tooa operacji **BatchRequest** obiektu, można wywołać żadnego hello następujące metody wiele razy:

* **addInsertEntity** (dodaje operację insertEntity)
* **addUpdateEntity** (dodaje operację updateEntity)
* **addMergeEntity** (dodaje operacji mergeEntity)
* **addInsertOrReplaceEntity** (dodaje operację insertOrReplaceEntity)
* **addInsertOrMergeEntity** (dodaje operację insertOrMergeEntity)
* **addDeleteEntity** (dodaje operacji deleteEntity)

powitania po przykładzie pokazano, jak tooexecute **insertEntity** i **deleteEntity** operacji w ramach pojedynczego żądania:

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;
use MicrosoftAzure\Storage\Common\ServiceException;
use MicrosoftAzure\Storage\Table\Models\Entity;
use MicrosoftAzure\Storage\Table\Models\EdmType;
use MicrosoftAzure\Storage\Table\Models\BatchOperations;

    // Create table REST proxy.
$tableRestProxy = ServicesBuilder::getInstance()->createTableService($connectionString);

// Create list of batch operation.
$operations = new BatchOperations();

$entity1 = new Entity();
$entity1->setPartitionKey("tasksSeattle");
$entity1->setRowKey("2");
$entity1->addProperty("Description", null, "Clean roof gutters.");
$entity1->addProperty("DueDate",
                        EdmType::DATETIME,
                        new DateTime("2012-11-05T08:15:00-08:00"));
$entity1->addProperty("Location", EdmType::STRING, "Home");

// Add operation toolist of batch operations.
$operations->addInsertEntity("mytable", $entity1);

// Add operation toolist of batch operations.
$operations->addDeleteEntity("mytable", "tasksSeattle", "1");

try    {
    $tableRestProxy->batch($operations);
}
catch(ServiceException $e){
    // Handle exception based on error codes and messages.
    // Error codes and messages are here:
    // http://msdn.microsoft.com/library/azure/dd179438.aspx
    $code = $e->getCode();
    $error_message = $e->getMessage();
    echo $code.": ".$error_message."<br />";
}
```

Aby uzyskać więcej informacji na temat przetwarzania wsadowego operacje tabeli, zobacz [wykonywanie transakcji grupy jednostek][entity-group-transactions].

## <a name="delete-a-table"></a>Usuwanie tabeli
Na koniec toodelete tabeli, Przekaż toohello nazwy tabeli hello **TableRestProxy -> deleteTable** metody.

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;
use MicrosoftAzure\Storage\Common\ServiceException;

// Create table REST proxy.
$tableRestProxy = ServicesBuilder::getInstance()->createTableService($connectionString);

try    {
    // Delete table.
    $tableRestProxy->deleteTable("mytable");
}
catch(ServiceException $e){
    // Handle exception based on error codes and messages.
    // Error codes and messages are here:
    // http://msdn.microsoft.com/library/azure/dd179438.aspx
    $code = $e->getCode();
    $error_message = $e->getMessage();
    echo $code.": ".$error_message."<br />";
}
```

## <a name="next-steps"></a>Następne kroki
Teraz, kiedy znasz już podstawy hello hello usługi tabel Azure, wykonaj te toolearn łącza o bardziej skomplikowanych zadaniach magazynu.

* [Eksplorator magazynu Microsoft Azure](../vs-azure-tools-storage-manage-with-storage-explorer.md) jest bezpłatna, aplikacja autonomiczny firmy Microsoft, który umożliwia toowork wizualnie z danymi usługi Azure Storage w systemie Windows, macOS i Linux.

* [Centrum deweloperów języka PHP](/develop/php/).

[download]: http://go.microsoft.com/fwlink/?LinkID=252473
[require_once]: http://php.net/require_once
[table-service-timeouts]: http://msdn.microsoft.com/library/azure/dd894042.aspx

[table-data-model]: http://msdn.microsoft.com/library/azure/dd179338.aspx
[filters]: http://msdn.microsoft.com/library/azure/dd894031.aspx
[entity-group-transactions]: http://msdn.microsoft.com/library/azure/dd894038.aspx
