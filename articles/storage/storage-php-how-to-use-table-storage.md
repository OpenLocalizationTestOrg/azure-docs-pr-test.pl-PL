---
title: "Magazyn tabel toouse aaaHow za pomocą języka PHP | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toouse hello usługi tabel z PHP toocreate i usunąć tabeli i wstawiania, usuwania i tabeli hello zapytania."
services: storage
documentationcenter: php
author: mmacy
manager: timlt
editor: tysonn
ms.assetid: 1e57f371-6208-4753-b2a0-05db4aede8e3
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: php
ms.topic: article
ms.date: 12/08/2016
ms.author: marsma
ms.openlocfilehash: 1e1036118e208280b4c205da7d7eea61e79359c1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-table-storage-from-php"></a><span data-ttu-id="26ebe-103">Jak toouse tabeli magazynu w języku PHP</span><span class="sxs-lookup"><span data-stu-id="26ebe-103">How toouse table storage from PHP</span></span>
[!INCLUDE [storage-selector-table-include](../../includes/storage-selector-table-include.md)]
[!INCLUDE [storage-table-cosmos-db-langsoon-tip-include](../../includes/storage-table-cosmos-db-langsoon-tip-include.md)]

## <a name="overview"></a><span data-ttu-id="26ebe-104">Omówienie</span><span class="sxs-lookup"><span data-stu-id="26ebe-104">Overview</span></span>
<span data-ttu-id="26ebe-105">Ten przewodnik przedstawia, jak tooperform typowych scenariuszy przy użyciu hello usługi tabel Azure.</span><span class="sxs-lookup"><span data-stu-id="26ebe-105">This guide shows you how tooperform common scenarios using hello Azure Table service.</span></span> <span data-ttu-id="26ebe-106">Przykłady Hello są zapisywane w kodzie PHP i używają hello [zestaw Azure SDK for PHP][download].</span><span class="sxs-lookup"><span data-stu-id="26ebe-106">hello samples are written in PHP and use hello [Azure SDK for PHP][download].</span></span> <span data-ttu-id="26ebe-107">Witaj omówione scenariusze obejmują **tworzenia i usuwania tabeli i wstawianie, usuwanie i badania jednostek w tabeli**.</span><span class="sxs-lookup"><span data-stu-id="26ebe-107">hello scenarios covered include **creating and deleting a table, and inserting, deleting, and querying entities in a table**.</span></span> <span data-ttu-id="26ebe-108">Aby uzyskać więcej informacji na powitania usługi tabel Azure, zobacz hello [następne kroki](#next-steps) sekcji.</span><span class="sxs-lookup"><span data-stu-id="26ebe-108">For more information on hello Azure Table service, see hello [Next steps](#next-steps) section.</span></span>

[!INCLUDE [storage-table-concepts-include](../../includes/storage-table-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/storage-create-account-include.md)]

## <a name="create-a-php-application"></a><span data-ttu-id="26ebe-109">Tworzenie aplikacji PHP</span><span class="sxs-lookup"><span data-stu-id="26ebe-109">Create a PHP application</span></span>
<span data-ttu-id="26ebe-110">Witaj tylko do tworzenia aplikacji PHP, który uzyskuje dostęp do usługi Azure tabeli hello wymaganiem hello odwołuje się do klas w hello Azure SDK for PHP z w kodzie.</span><span class="sxs-lookup"><span data-stu-id="26ebe-110">hello only requirement for creating a PHP application that accesses hello Azure Table service is hello referencing of classes in hello Azure SDK for PHP from within your code.</span></span> <span data-ttu-id="26ebe-111">Można użyć dowolnego toocreate narzędzi rozwoju aplikacji, łącznie z Notatnika.</span><span class="sxs-lookup"><span data-stu-id="26ebe-111">You can use any development tools toocreate your application, including Notepad.</span></span>

<span data-ttu-id="26ebe-112">W tym przewodniku korzystanie z funkcji usługi tabeli, które mogą być wywoływane w ramach aplikacji PHP lokalnie lub w kodzie działających w roli sieci web platformy Azure, roli procesu roboczego lub witryny sieci Web.</span><span class="sxs-lookup"><span data-stu-id="26ebe-112">In this guide, you use Table service features which can be called from within a PHP application locally, or in code running within an Azure web role, worker role, or website.</span></span>

## <a name="get-hello-azure-client-libraries"></a><span data-ttu-id="26ebe-113">Pobierz bibliotek klienckich hello Azure</span><span class="sxs-lookup"><span data-stu-id="26ebe-113">Get hello Azure Client Libraries</span></span>
[!INCLUDE [get-client-libraries](../../includes/get-client-libraries.md)]

## <a name="configure-your-application-tooaccess-hello-table-service"></a><span data-ttu-id="26ebe-114">Konfigurowanie usługi aplikacji tooaccess hello tabeli</span><span class="sxs-lookup"><span data-stu-id="26ebe-114">Configure your application tooaccess hello Table service</span></span>
<span data-ttu-id="26ebe-115">Usługa tabel Azure hello toouse interfejsów API, musisz:</span><span class="sxs-lookup"><span data-stu-id="26ebe-115">toouse hello Azure Table service APIs, you need to:</span></span>

1. <span data-ttu-id="26ebe-116">Plik automatycznej ładowarki hello odwołania przy użyciu hello [require_once] [ require_once] instrukcji, i</span><span class="sxs-lookup"><span data-stu-id="26ebe-116">Reference hello autoloader file using hello [require_once][require_once] statement, and</span></span>
2. <span data-ttu-id="26ebe-117">Odwoływać się do wszystkich klas, których może używać.</span><span class="sxs-lookup"><span data-stu-id="26ebe-117">Reference any classes you might use.</span></span>

<span data-ttu-id="26ebe-118">Witaj poniższy przykład przedstawia sposób tooinclude hello hello plików i odwołanie automatycznej ładowarki **ServicesBuilder** klasy.</span><span class="sxs-lookup"><span data-stu-id="26ebe-118">hello following example shows how tooinclude hello autoloader file and reference hello **ServicesBuilder** class.</span></span>

> [!NOTE]
> <span data-ttu-id="26ebe-119">Przykłady Hello w tym artykule przyjęto założenie, że zainstalowano hello bibliotek klienckich PHP na platformie Azure za pośrednictwem Composer.</span><span class="sxs-lookup"><span data-stu-id="26ebe-119">hello examples in this article assume you have installed hello PHP Client Libraries for Azure via Composer.</span></span> <span data-ttu-id="26ebe-120">Biblioteki hello zainstalować ręcznie, konieczne będzie tooreference hello <code>WindowsAzure.php</code> automatycznej ładowarki pliku.</span><span class="sxs-lookup"><span data-stu-id="26ebe-120">If you installed hello libraries manually, you need tooreference hello <code>WindowsAzure.php</code> autoloader file.</span></span>
>
>

```php
require_once 'vendor/autoload.php';
use WindowsAzure\Common\ServicesBuilder;
```

<span data-ttu-id="26ebe-121">W poniższych przykładach hello, hello `require_once` instrukcji jest zawsze widoczne, ale odwołuje się tylko hello klasy niezbędne do tooexecute przykład hello.</span><span class="sxs-lookup"><span data-stu-id="26ebe-121">In hello examples below, hello `require_once` statement is always shown, but only hello classes necessary for hello example tooexecute are referenced.</span></span>

## <a name="set-up-an-azure-storage-connection"></a><span data-ttu-id="26ebe-122">Konfigurowanie połączenia z magazynem Azure</span><span class="sxs-lookup"><span data-stu-id="26ebe-122">Set up an Azure storage connection</span></span>
<span data-ttu-id="26ebe-123">tooinstantiate klienta usługi tabel Azure, musisz najpierw mieć prawidłowe parametry połączenia.</span><span class="sxs-lookup"><span data-stu-id="26ebe-123">tooinstantiate an Azure Table service client, you must first have a valid connection string.</span></span> <span data-ttu-id="26ebe-124">format Hello hello ciąg połączenia usługi tabeli jest:</span><span class="sxs-lookup"><span data-stu-id="26ebe-124">hello format for hello Table service connection string is:</span></span>

<span data-ttu-id="26ebe-125">Aby uzyskać dostęp do usługi na żywo:</span><span class="sxs-lookup"><span data-stu-id="26ebe-125">For accessing a live service:</span></span>

```php
DefaultEndpointsProtocol=[http|https];AccountName=[yourAccount];AccountKey=[yourKey]
```

<span data-ttu-id="26ebe-126">Aby uzyskać dostęp do magazynu emulatora hello:</span><span class="sxs-lookup"><span data-stu-id="26ebe-126">For accessing hello emulator storage:</span></span>

```php
UseDevelopmentStorage=true
```

<span data-ttu-id="26ebe-127">toocreate dowolnego klienta usługi Azure należy toouse hello **ServicesBuilder** klasy.</span><span class="sxs-lookup"><span data-stu-id="26ebe-127">toocreate any Azure service client, you need toouse hello **ServicesBuilder** class.</span></span> <span data-ttu-id="26ebe-128">Możesz:</span><span class="sxs-lookup"><span data-stu-id="26ebe-128">You can:</span></span>

* <span data-ttu-id="26ebe-129">Przekaż połączenia hello ciągu bezpośrednio tooit lub</span><span class="sxs-lookup"><span data-stu-id="26ebe-129">pass hello connection string directly tooit or</span></span>
* <span data-ttu-id="26ebe-130">Użyj hello **CloudConfigurationManager (CCM)** toocheck zewnętrzne wiele źródeł dla parametrów połączenia hello:</span><span class="sxs-lookup"><span data-stu-id="26ebe-130">use hello **CloudConfigurationManager (CCM)** toocheck multiple external sources for hello connection string:</span></span>
  * <span data-ttu-id="26ebe-131">Domyślnie pochodzi z obsługą jednego źródła zewnętrznego — zmienne środowiskowe</span><span class="sxs-lookup"><span data-stu-id="26ebe-131">by default, it comes with support for one external source - environmental variables</span></span>
  * <span data-ttu-id="26ebe-132">można dodać nowych źródeł, rozszerzając hello **ConnectionStringSource** — klasa</span><span class="sxs-lookup"><span data-stu-id="26ebe-132">you can add new sources by extending hello **ConnectionStringSource** class</span></span>

<span data-ttu-id="26ebe-133">Przykłady hello opisana w tym temacie hello parametry połączenia zostaną przekazane bezpośrednio.</span><span class="sxs-lookup"><span data-stu-id="26ebe-133">For hello examples outlined here, hello connection string will be passed directly.</span></span>

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;

$tableRestProxy = ServicesBuilder::getInstance()->createTableService($connectionString);
```

## <a name="create-a-table"></a><span data-ttu-id="26ebe-134">Tworzenie tabeli</span><span class="sxs-lookup"><span data-stu-id="26ebe-134">Create a table</span></span>
<span data-ttu-id="26ebe-135">A **TableRestProxy** obiektu pozwala utworzyć tabelę z hello **createTable** metody.</span><span class="sxs-lookup"><span data-stu-id="26ebe-135">A **TableRestProxy** object lets you create a table with hello **createTable** method.</span></span> <span data-ttu-id="26ebe-136">Podczas tworzenia tabeli, można ustawić limitu czasu usługi tabeli hello.</span><span class="sxs-lookup"><span data-stu-id="26ebe-136">When creating a table, you can set hello Table service timeout.</span></span> <span data-ttu-id="26ebe-137">(Aby uzyskać więcej informacji o tabeli hello upłynięcia limitu czasu usługi, zobacz [ustawienie przekroczeń limitu czasu dla operacji usługi tabeli][table-service-timeouts].)</span><span class="sxs-lookup"><span data-stu-id="26ebe-137">(For more information about hello Table service timeout, see [Setting Timeouts for Table Service Operations][table-service-timeouts].)</span></span>

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

<span data-ttu-id="26ebe-138">Aby uzyskać informacji o ograniczeniach dotyczących nazw tabeli, zobacz [hello opis modelu danych usługi tabel][table-data-model].</span><span class="sxs-lookup"><span data-stu-id="26ebe-138">For information about restrictions on table names, see [Understanding hello Table Service Data Model][table-data-model].</span></span>

## <a name="add-an-entity-tooa-table"></a><span data-ttu-id="26ebe-139">Dodaj tabelę tooa jednostki</span><span class="sxs-lookup"><span data-stu-id="26ebe-139">Add an entity tooa table</span></span>
<span data-ttu-id="26ebe-140">tooadd tabeli tooa jednostki, Utwórz nową **jednostki** obiektu i przekaż go za**TableRestProxy -> insertEntity**.</span><span class="sxs-lookup"><span data-stu-id="26ebe-140">tooadd an entity tooa table, create a new **Entity** object and pass it too**TableRestProxy->insertEntity**.</span></span> <span data-ttu-id="26ebe-141">Należy pamiętać, że podczas tworzenia obiektu, należy określić `PartitionKey` i `RowKey`.</span><span class="sxs-lookup"><span data-stu-id="26ebe-141">Note that when you create an entity, you must specify a `PartitionKey` and `RowKey`.</span></span> <span data-ttu-id="26ebe-142">Te są hello unikatowych identyfikatorów dla jednostek i wartości, które można wykonać zapytania znacznie szybciej niż inne właściwości jednostki.</span><span class="sxs-lookup"><span data-stu-id="26ebe-142">These are hello unique identifiers for an entity and are values that can be queried much faster than other entity properties.</span></span> <span data-ttu-id="26ebe-143">Witaj system używa `PartitionKey` tooautomatically rozpowszechniać jednostek tabeli hello przez wiele węzłów magazynu.</span><span class="sxs-lookup"><span data-stu-id="26ebe-143">hello system uses `PartitionKey` tooautomatically distribute hello table's entities over many storage nodes.</span></span> <span data-ttu-id="26ebe-144">Jednostki z hello sam `PartitionKey` są przechowywane na powitania tym samym węźle.</span><span class="sxs-lookup"><span data-stu-id="26ebe-144">Entities with hello same `PartitionKey` are stored on hello same node.</span></span> <span data-ttu-id="26ebe-145">(Operacje na wiele jednostek przechowywanych na powitania wykonać na tym samym węźle lepszym rozwiązaniem niż na jednostek przechowywanych w różnych węzłach.) Witaj `RowKey` jest unikatowy identyfikator hello jednostek w partycji.</span><span class="sxs-lookup"><span data-stu-id="26ebe-145">(Operations on multiple entities stored on hello same node perform better than on entities stored across different nodes.) hello `RowKey` is hello unique ID of an entity within a partition.</span></span>

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

<span data-ttu-id="26ebe-146">Informacje dotyczące właściwości i typów, zobacz [hello opis modelu danych usługi tabel][table-data-model].</span><span class="sxs-lookup"><span data-stu-id="26ebe-146">For information about Table properties and types, see [Understanding hello Table Service Data Model][table-data-model].</span></span>

<span data-ttu-id="26ebe-147">Witaj **TableRestProxy** klasy oferuje dwie alternatywne metody Wstawianie jednostek: **insertOrMergeEntity** i **insertOrReplaceEntity**.</span><span class="sxs-lookup"><span data-stu-id="26ebe-147">hello **TableRestProxy** class offers two alternative methods for inserting entities: **insertOrMergeEntity** and **insertOrReplaceEntity**.</span></span> <span data-ttu-id="26ebe-148">toouse tych metod, Utwórz nową **jednostki** i przekaż go jako parametru metody tooeither.</span><span class="sxs-lookup"><span data-stu-id="26ebe-148">toouse these methods, create a new **Entity** and pass it as a parameter tooeither method.</span></span> <span data-ttu-id="26ebe-149">Każda metoda powoduje wstawienie hello jednostki, jeśli nie istnieje.</span><span class="sxs-lookup"><span data-stu-id="26ebe-149">Each method will insert hello entity if it does not exist.</span></span> <span data-ttu-id="26ebe-150">Jeśli istnieje już jednostka hello, **insertOrMergeEntity** aktualizacji wartości właściwości, jeśli hello właściwości już istnieje i dodaje nowe właściwości nie są dostępne, podczas gdy **insertOrReplaceEntity** całkowicie zastępuje istniejącej jednostki.</span><span class="sxs-lookup"><span data-stu-id="26ebe-150">If hello entity already exists, **insertOrMergeEntity** updates property values if hello properties already exist and adds new properties if they do not exist, while **insertOrReplaceEntity** completely replaces an existing entity.</span></span> <span data-ttu-id="26ebe-151">powitania po przykładzie pokazano, jak toouse **insertOrMergeEntity**.</span><span class="sxs-lookup"><span data-stu-id="26ebe-151">hello following example shows how toouse **insertOrMergeEntity**.</span></span> <span data-ttu-id="26ebe-152">Jeśli hello jednostki o `PartitionKey` "tasksSeattle" i `RowKey` "1" nie istnieje, zostanie on włożony.</span><span class="sxs-lookup"><span data-stu-id="26ebe-152">If hello entity with `PartitionKey` "tasksSeattle" and `RowKey` "1" does not already exist, it will be inserted.</span></span> <span data-ttu-id="26ebe-153">Jednak jeśli wcześniej wstawione (jak pokazano w powyższym przykładzie hello), hello `DueDate` właściwość zostanie zaktualizowana i hello `Status` właściwość zostanie dodany.</span><span class="sxs-lookup"><span data-stu-id="26ebe-153">However, if it has previously been inserted (as shown in hello example above), hello `DueDate` property will be updated, and hello `Status` property will be added.</span></span> <span data-ttu-id="26ebe-154">Witaj `Description` i `Location` są również zaktualizować właściwości, ale z wartościami które skutecznie pozostaw je bez zmian.</span><span class="sxs-lookup"><span data-stu-id="26ebe-154">hello `Description` and `Location` properties are also updated, but with values that effectively leave them unchanged.</span></span> <span data-ttu-id="26ebe-155">Jeśli te dwie właściwości to drugie nie zostały dodane, jak pokazano w przykładzie hello, ale znajdował się na jednostkę docelową hello, ich istniejące wartości pozostanie bez zmian.</span><span class="sxs-lookup"><span data-stu-id="26ebe-155">If these latter two properties were not added as shown in hello example, but existed on hello target entity, their existing values would remain unchanged.</span></span>

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

## <a name="retrieve-a-single-entity"></a><span data-ttu-id="26ebe-156">Pobieranie pojedynczej jednostki</span><span class="sxs-lookup"><span data-stu-id="26ebe-156">Retrieve a single entity</span></span>
<span data-ttu-id="26ebe-157">Witaj **TableRestProxy -> getEntity** metoda pozwala tooretrieve pojedynczej jednostki przez wykonanie zapytania dotyczącego jego `PartitionKey` i `RowKey`.</span><span class="sxs-lookup"><span data-stu-id="26ebe-157">hello **TableRestProxy->getEntity** method allows you tooretrieve a single entity by querying for its `PartitionKey` and `RowKey`.</span></span> <span data-ttu-id="26ebe-158">W poniższym przykładzie hello, hello klucza partycji `tasksSeattle` i klucz wiersza `1` są przekazywane toohello **getEntity** metody.</span><span class="sxs-lookup"><span data-stu-id="26ebe-158">In hello example below, hello partition key `tasksSeattle` and row key `1` are passed toohello **getEntity** method.</span></span>

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

## <a name="retrieve-all-entities-in-a-partition"></a><span data-ttu-id="26ebe-159">Pobieranie wszystkich jednostek w partycji</span><span class="sxs-lookup"><span data-stu-id="26ebe-159">Retrieve all entities in a partition</span></span>
<span data-ttu-id="26ebe-160">Zapytania jednostki są konstruowane przy użyciu filtrów (Aby uzyskać więcej informacji, zobacz [badania tabel i jednostek][filters]).</span><span class="sxs-lookup"><span data-stu-id="26ebe-160">Entity queries are constructed using filters (for more information, see [Querying Tables and Entities][filters]).</span></span> <span data-ttu-id="26ebe-161">tooretrieve wszystkich jednostek w partycji, użyj filtru hello "PartitionKey eq *nazwa_partycji*".</span><span class="sxs-lookup"><span data-stu-id="26ebe-161">tooretrieve all entities in partition, use hello filter "PartitionKey eq *partition_name*".</span></span> <span data-ttu-id="26ebe-162">powitania po przykładzie pokazano, jak tooretrieve wszystkich jednostek w hello `tasksSeattle` partycji, przekazując toohello filtru **queryEntities** metody.</span><span class="sxs-lookup"><span data-stu-id="26ebe-162">hello following example shows how tooretrieve all entities in hello `tasksSeattle` partition by passing a filter toohello **queryEntities** method.</span></span>

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

## <a name="retrieve-a-subset-of-entities-in-a-partition"></a><span data-ttu-id="26ebe-163">Pobrać podzbiór jednostek w partycji</span><span class="sxs-lookup"><span data-stu-id="26ebe-163">Retrieve a subset of entities in a partition</span></span>
<span data-ttu-id="26ebe-164">Witaj tego samego wzorca użyty w poprzednim przykładzie hello mogą być używane tooretrieve dowolny podzbiór jednostek w partycji.</span><span class="sxs-lookup"><span data-stu-id="26ebe-164">hello same pattern used in hello previous example can be used tooretrieve any subset of entities in a partition.</span></span> <span data-ttu-id="26ebe-165">podzbiór Hello jednostek, możesz pobrać są określane przez filtr hello używasz (Aby uzyskać więcej informacji, zobacz [badania tabel i jednostek][filters]) .hello po przykładzie pokazano, jak toouse tooretrieve filtru wszystkie jednostki z określonym `Location` i `DueDate` mniej niż określona data.</span><span class="sxs-lookup"><span data-stu-id="26ebe-165">hello subset of entities you retrieve are determined by hello filter you use (for more information, see [Querying Tables and Entities][filters]).hello following example shows how toouse a filter tooretrieve all entities with a specific `Location` and a `DueDate` less than a specified date.</span></span>

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

## <a name="retrieve-a-subset-of-entity-properties"></a><span data-ttu-id="26ebe-166">Pobrać podzbioru właściwości jednostki</span><span class="sxs-lookup"><span data-stu-id="26ebe-166">Retrieve a subset of entity properties</span></span>
<span data-ttu-id="26ebe-167">Zapytania można pobrać podzbioru właściwości jednostki.</span><span class="sxs-lookup"><span data-stu-id="26ebe-167">A query can retrieve a subset of entity properties.</span></span> <span data-ttu-id="26ebe-168">Ta technika, zwana *projekcji*, redukuje przepustowość i może poprawiać wydajność zapytań, zwłaszcza w przypadku dużych jednostek.</span><span class="sxs-lookup"><span data-stu-id="26ebe-168">This technique, called *projection*, reduces bandwidth and can improve query performance, especially for large entities.</span></span> <span data-ttu-id="26ebe-169">pobrać toobe właściwości toospecify, przekazywania hello nazwy hello właściwości toohello **zapytania -> addSelectField** metody.</span><span class="sxs-lookup"><span data-stu-id="26ebe-169">toospecify a property toobe retrieved, pass hello name of hello property toohello **Query->addSelectField** method.</span></span> <span data-ttu-id="26ebe-170">Można wywołać tej metody tooadd wiele razy więcej właściwości.</span><span class="sxs-lookup"><span data-stu-id="26ebe-170">You can call this method multiple times tooadd more properties.</span></span> <span data-ttu-id="26ebe-171">Po wykonaniu **TableRestProxy -> queryEntities**, hello zwrócił jednostek będzie miał tylko hello wybrane właściwości.</span><span class="sxs-lookup"><span data-stu-id="26ebe-171">After executing **TableRestProxy->queryEntities**, hello returned entities will only have hello selected properties.</span></span> <span data-ttu-id="26ebe-172">(Tooreturn podzbiór jednostek tabeli należy użyć filtru jak pokazano w zapytaniach hello powyżej).</span><span class="sxs-lookup"><span data-stu-id="26ebe-172">(If you want tooreturn a subset of Table entities, use a filter as shown in hello queries above.)</span></span>

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

## <a name="update-an-entity"></a><span data-ttu-id="26ebe-173">Aktualizuj jednostkę</span><span class="sxs-lookup"><span data-stu-id="26ebe-173">Update an entity</span></span>
<span data-ttu-id="26ebe-174">Istniejącej jednostki można aktualizować za pomocą hello **jednostki -> setProperty** i **jednostki -> addProperty** w hello jednostki, a następnie wywołania metod **TableRestProxy -> updateEntity** .</span><span class="sxs-lookup"><span data-stu-id="26ebe-174">An existing entity can be updated by using hello **Entity->setProperty** and **Entity->addProperty** methods on hello entity, and then calling **TableRestProxy->updateEntity**.</span></span> <span data-ttu-id="26ebe-175">Witaj poniższy przykład pobiera jednostki, modyfikuje jedną właściwość usuwa innej właściwości i dodaje nową właściwość.</span><span class="sxs-lookup"><span data-stu-id="26ebe-175">hello following example retrieves an entity, modifies one property, removes another property, and adds a new property.</span></span> <span data-ttu-id="26ebe-176">Uwaga usunąć właściwość, ustawiając wartość zbyt**null**.</span><span class="sxs-lookup"><span data-stu-id="26ebe-176">Note that you can remove a property by setting its value too**null**.</span></span>

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

## <a name="delete-an-entity"></a><span data-ttu-id="26ebe-177">Usuwanie jednostki</span><span class="sxs-lookup"><span data-stu-id="26ebe-177">Delete an entity</span></span>
<span data-ttu-id="26ebe-178">toodelete jednostki, Przekaż hello nazwę tabeli i jednostki hello `PartitionKey` i `RowKey` toohello **TableRestProxy -> deleteEntity** metody.</span><span class="sxs-lookup"><span data-stu-id="26ebe-178">toodelete an entity, pass hello table name, and hello entity's `PartitionKey` and `RowKey` toohello **TableRestProxy->deleteEntity** method.</span></span>

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

<span data-ttu-id="26ebe-179">Należy pamiętać, że kontrolach współbieżności, można ustawić hello Etag dla toobe jednostki usunięte przy użyciu hello **DeleteEntityOptions -> setEtag** — metoda i przekazywanie hello **DeleteEntityOptions** obiekt zbyt**deleteEntity** jako czwartego parametru.</span><span class="sxs-lookup"><span data-stu-id="26ebe-179">Note that for concurrency checks, you can set hello Etag for an entity toobe deleted by using hello **DeleteEntityOptions->setEtag** method and passing hello **DeleteEntityOptions** object too**deleteEntity** as a fourth parameter.</span></span>

## <a name="batch-table-operations"></a><span data-ttu-id="26ebe-180">Operacje tabeli partii</span><span class="sxs-lookup"><span data-stu-id="26ebe-180">Batch table operations</span></span>
<span data-ttu-id="26ebe-181">Witaj **TableRestProxy -> partii** metoda pozwala tooexecute wiele operacji w ramach pojedynczego żądania.</span><span class="sxs-lookup"><span data-stu-id="26ebe-181">hello **TableRestProxy->batch** method allows you tooexecute multiple operations in a single request.</span></span> <span data-ttu-id="26ebe-182">Hello wzorzec tutaj obejmuje dodanie operacji za**BatchRequest** obiektu, a następnie przekazywanie hello **BatchRequest** obiekt toohello **TableRestProxy -> partii** metody.</span><span class="sxs-lookup"><span data-stu-id="26ebe-182">hello pattern here involves adding operations too**BatchRequest** object and then passing hello **BatchRequest** object toohello **TableRestProxy->batch** method.</span></span> <span data-ttu-id="26ebe-183">tooadd tooa operacji **BatchRequest** obiektu, można wywołać żadnego hello następujące metody wiele razy:</span><span class="sxs-lookup"><span data-stu-id="26ebe-183">tooadd an operation tooa **BatchRequest** object, you can call any of hello following methods multiple times:</span></span>

* <span data-ttu-id="26ebe-184">**addInsertEntity** (dodaje operację insertEntity)</span><span class="sxs-lookup"><span data-stu-id="26ebe-184">**addInsertEntity** (adds an insertEntity operation)</span></span>
* <span data-ttu-id="26ebe-185">**addUpdateEntity** (dodaje operację updateEntity)</span><span class="sxs-lookup"><span data-stu-id="26ebe-185">**addUpdateEntity** (adds an updateEntity operation)</span></span>
* <span data-ttu-id="26ebe-186">**addMergeEntity** (dodaje operacji mergeEntity)</span><span class="sxs-lookup"><span data-stu-id="26ebe-186">**addMergeEntity** (adds a mergeEntity operation)</span></span>
* <span data-ttu-id="26ebe-187">**addInsertOrReplaceEntity** (dodaje operację insertOrReplaceEntity)</span><span class="sxs-lookup"><span data-stu-id="26ebe-187">**addInsertOrReplaceEntity** (adds an insertOrReplaceEntity operation)</span></span>
* <span data-ttu-id="26ebe-188">**addInsertOrMergeEntity** (dodaje operację insertOrMergeEntity)</span><span class="sxs-lookup"><span data-stu-id="26ebe-188">**addInsertOrMergeEntity** (adds an insertOrMergeEntity operation)</span></span>
* <span data-ttu-id="26ebe-189">**addDeleteEntity** (dodaje operacji deleteEntity)</span><span class="sxs-lookup"><span data-stu-id="26ebe-189">**addDeleteEntity** (adds a deleteEntity operation)</span></span>

<span data-ttu-id="26ebe-190">powitania po przykładzie pokazano, jak tooexecute **insertEntity** i **deleteEntity** operacji w ramach pojedynczego żądania:</span><span class="sxs-lookup"><span data-stu-id="26ebe-190">hello following example shows how tooexecute **insertEntity** and **deleteEntity** operations in a single request:</span></span>

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

<span data-ttu-id="26ebe-191">Aby uzyskać więcej informacji na temat przetwarzania wsadowego operacje tabeli, zobacz [wykonywanie transakcji grupy jednostek][entity-group-transactions].</span><span class="sxs-lookup"><span data-stu-id="26ebe-191">For more information about batching Table operations, see [Performing Entity Group Transactions][entity-group-transactions].</span></span>

## <a name="delete-a-table"></a><span data-ttu-id="26ebe-192">Usuwanie tabeli</span><span class="sxs-lookup"><span data-stu-id="26ebe-192">Delete a table</span></span>
<span data-ttu-id="26ebe-193">Na koniec toodelete tabeli, Przekaż toohello nazwy tabeli hello **TableRestProxy -> deleteTable** metody.</span><span class="sxs-lookup"><span data-stu-id="26ebe-193">Finally, toodelete a table, pass hello table name toohello **TableRestProxy->deleteTable** method.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="26ebe-194">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="26ebe-194">Next steps</span></span>
<span data-ttu-id="26ebe-195">Teraz, kiedy znasz już podstawy hello hello usługi tabel Azure, wykonaj te toolearn łącza o bardziej skomplikowanych zadaniach magazynu.</span><span class="sxs-lookup"><span data-stu-id="26ebe-195">Now that you've learned hello basics of hello Azure Table service, follow these links toolearn about more complex storage tasks.</span></span>

* <span data-ttu-id="26ebe-196">[Eksplorator magazynu Microsoft Azure](../vs-azure-tools-storage-manage-with-storage-explorer.md) jest bezpłatna, aplikacja autonomiczny firmy Microsoft, który umożliwia toowork wizualnie z danymi usługi Azure Storage w systemie Windows, macOS i Linux.</span><span class="sxs-lookup"><span data-stu-id="26ebe-196">[Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md) is a free, standalone app from Microsoft that enables you toowork visually with Azure Storage data on Windows, macOS, and Linux.</span></span>

* <span data-ttu-id="26ebe-197">[Centrum deweloperów języka PHP](/develop/php/).</span><span class="sxs-lookup"><span data-stu-id="26ebe-197">[PHP Developer Center](/develop/php/).</span></span>

[download]: http://go.microsoft.com/fwlink/?LinkID=252473
[require_once]: http://php.net/require_once
[table-service-timeouts]: http://msdn.microsoft.com/library/azure/dd894042.aspx

[table-data-model]: http://msdn.microsoft.com/library/azure/dd179338.aspx
[filters]: http://msdn.microsoft.com/library/azure/dd894031.aspx
[entity-group-transactions]: http://msdn.microsoft.com/library/azure/dd894038.aspx
