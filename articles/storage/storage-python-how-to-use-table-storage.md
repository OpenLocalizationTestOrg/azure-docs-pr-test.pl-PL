---
title: "Jak używać magazynu tabel Azure języka Python | Dokumentacja firmy Microsoft"
description: "Przechowywanie danych strukturalnych w chmurze za pomocą Magazynu tabel Azure, magazyn danych NoSQL."
services: storage
documentationcenter: python
author: mmacy
manager: timlt
editor: tysonn
ms.assetid: 7ddb9f3e-4e6d-4103-96e6-f0351d69a17b
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: python
ms.topic: article
ms.date: 05/16/2017
ms.author: marsma
ms.openlocfilehash: c310a52182bbc3cf44ed4dc6a04e97aa59200a64
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-use-table-storage-in-python"></a><span data-ttu-id="aaacd-103">Jak używać magazynu tabel w języku Python</span><span class="sxs-lookup"><span data-stu-id="aaacd-103">How to use Table storage in Python</span></span>

[!INCLUDE [storage-selector-table-include](../../includes/storage-selector-table-include.md)]
[!INCLUDE [storage-table-cosmos-db-langsoon-tip-include](../../includes/storage-table-cosmos-db-langsoon-tip-include.md)]

<span data-ttu-id="aaacd-104">W tym przewodniku opisano sposób wykonywania typowych scenariuszy magazynu tabel Azure przy użyciu języka Python [Microsoft Azure magazynu SDK dla języka Python](https://github.com/Azure/azure-storage-python).</span><span class="sxs-lookup"><span data-stu-id="aaacd-104">This guide shows you how to perform common Azure Table storage scenarios in Python using the [Microsoft Azure Storage SDK for Python](https://github.com/Azure/azure-storage-python).</span></span> <span data-ttu-id="aaacd-105">Omówione scenariusze obejmują tworzenie i usuwania tabeli, wstawianie i badania jednostek.</span><span class="sxs-lookup"><span data-stu-id="aaacd-105">The scenarios covered include creating and deleting a table, and inserting and querying entities.</span></span>

<span data-ttu-id="aaacd-106">Podczas pracy nad scenariusze w tym samouczku, możesz odwoływać się do [Azure Storage SDK for Python API reference](https://azure-storage.readthedocs.io/en/latest/index.html).</span><span class="sxs-lookup"><span data-stu-id="aaacd-106">While working through the scenarios in this tutorial, you may wish to refer to the [Azure Storage SDK for Python API reference](https://azure-storage.readthedocs.io/en/latest/index.html).</span></span>

[!INCLUDE [storage-table-concepts-include](../../includes/storage-table-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/storage-create-account-include.md)]

## <a name="install-the-azure-storage-sdk-for-python"></a><span data-ttu-id="aaacd-107">Zainstalować magazynu Azure SDK dla języka Python</span><span class="sxs-lookup"><span data-stu-id="aaacd-107">Install the Azure Storage SDK for Python</span></span>

<span data-ttu-id="aaacd-108">Po utworzeniu konta magazynu, następnym krokiem jest zainstalowanie [Microsoft Azure magazynu SDK dla języka Python](https://github.com/Azure/azure-storage-python).</span><span class="sxs-lookup"><span data-stu-id="aaacd-108">Once you've created a storage account, your next step is to install the [Microsoft Azure Storage SDK for Python](https://github.com/Azure/azure-storage-python).</span></span> <span data-ttu-id="aaacd-109">Aby uzyskać więcej informacji na temat instalowania zestawu SDK, zapoznaj się [README.rst](https://github.com/Azure/azure-storage-python/blob/master/README.rst) pliku w zestawie SDK magazynu dla repozytorium Python w witrynie GitHub.</span><span class="sxs-lookup"><span data-stu-id="aaacd-109">For details on installing the SDK, refer to the [README.rst](https://github.com/Azure/azure-storage-python/blob/master/README.rst) file in the Storage SDK for Python repository on GitHub.</span></span>

## <a name="create-a-table"></a><span data-ttu-id="aaacd-110">Tworzenie tabeli</span><span class="sxs-lookup"><span data-stu-id="aaacd-110">Create a table</span></span>

<span data-ttu-id="aaacd-111">Aby pracować z usługi Azure tabel w języku Python, należy zaimportować [TableService] [ py_TableService] modułu.</span><span class="sxs-lookup"><span data-stu-id="aaacd-111">To work with the Azure Table service in Python, you must import the [TableService][py_TableService] module.</span></span> <span data-ttu-id="aaacd-112">Ponieważ będzie działać z jednostek tabeli, należy również [jednostki] [ py_Entity] klasy.</span><span class="sxs-lookup"><span data-stu-id="aaacd-112">Since you'll be working with Table entities, you also need the [Entity][py_Entity] class.</span></span> <span data-ttu-id="aaacd-113">Dodaj ten kod u góry pliku Python do zaimportowania zarówno:</span><span class="sxs-lookup"><span data-stu-id="aaacd-113">Add this code near the top your Python file to import both:</span></span>

```python
from azure.storage.table import TableService, Entity
```

<span data-ttu-id="aaacd-114">Utwórz [TableService] [ py_TableService] obiektu, przekazując klucz konta magazynu nazwy i konta.</span><span class="sxs-lookup"><span data-stu-id="aaacd-114">Create a [TableService][py_TableService] object, passing in your storage account name and account key.</span></span> <span data-ttu-id="aaacd-115">Zastąp `myaccount` i `mykey` z nazwą konta i klucz i wywołanie [create_table] [ py_create_table] do utworzenia tabeli w usłudze Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="aaacd-115">Replace `myaccount` and `mykey` with your account name and key, and call [create_table][py_create_table] to create the table in Azure Storage.</span></span>

```python
table_service = TableService(account_name='myaccount', account_key='mykey')

table_service.create_table('tasktable')
```

## <a name="add-an-entity-to-a-table"></a><span data-ttu-id="aaacd-116">Dodawanie jednostki do tabeli</span><span class="sxs-lookup"><span data-stu-id="aaacd-116">Add an entity to a table</span></span>

<span data-ttu-id="aaacd-117">Aby dodać jednostkę, najpierw utwórz obiekt, który reprezentuje jednostki, a następnie przekaż obiekt do [TableService][py_TableService].[ insert_entity] [ py_insert_entity] metody.</span><span class="sxs-lookup"><span data-stu-id="aaacd-117">To add an entity, you first create an object that represents your entity, then pass the object to the [TableService][py_TableService].[insert_entity][py_insert_entity] method.</span></span> <span data-ttu-id="aaacd-118">Obiekt jednostki można słownika lub typu obiektu [jednostki][py_Entity]i definiuje użytkownika jednostki nazwy i wartości właściwości.</span><span class="sxs-lookup"><span data-stu-id="aaacd-118">The entity object can be a dictionary or an object of type [Entity][py_Entity], and defines your entity's property names and values.</span></span> <span data-ttu-id="aaacd-119">Każdy podmiot musi zawierać wymaganych [PartitionKey i RowKey](#partitionkey-and-rowkey) właściwości, oprócz innych właściwości, należy zdefiniować dla jednostki.</span><span class="sxs-lookup"><span data-stu-id="aaacd-119">Every entity must include the required [PartitionKey and RowKey](#partitionkey-and-rowkey) properties, in addition to any other properties you define for the entity.</span></span>

<span data-ttu-id="aaacd-120">Ten przykład tworzy obiekt słownik reprezentujący jednostkę, następnie przekazuje ją do [insert_entity] [ py_insert_entity] metody, aby dodać go do tabeli:</span><span class="sxs-lookup"><span data-stu-id="aaacd-120">This example creates a dictionary object representing an entity, then passes it to the [insert_entity][py_insert_entity] method to add it to the table:</span></span>

```python
task = {'PartitionKey': 'tasksSeattle', 'RowKey': '001', 'description' : 'Take out the trash', 'priority' : 200}
table_service.insert_entity('tasktable', task)
```

<span data-ttu-id="aaacd-121">Ten przykład tworzy [jednostki] [ py_Entity] obiekt, a następnie przekazuje go do [insert_entity] [ py_insert_entity] metody, aby dodać go do tabeli:</span><span class="sxs-lookup"><span data-stu-id="aaacd-121">This example creates an [Entity][py_Entity] object, then passes it to the [insert_entity][py_insert_entity] method to add it to the table:</span></span>

```python
task = Entity()
task.PartitionKey = 'tasksSeattle'
task.RowKey = '002'
task.description = 'Wash the car'
task.priority = 100
table_service.insert_entity('tasktable', task)
```

### <a name="partitionkey-and-rowkey"></a><span data-ttu-id="aaacd-122">PartitionKey i RowKey</span><span class="sxs-lookup"><span data-stu-id="aaacd-122">PartitionKey and RowKey</span></span>

<span data-ttu-id="aaacd-123">Należy określić zarówno **PartitionKey** i **RowKey** właściwości dla każdej jednostki.</span><span class="sxs-lookup"><span data-stu-id="aaacd-123">You must specify both a **PartitionKey** and a **RowKey** property for every entity.</span></span> <span data-ttu-id="aaacd-124">Jak razem są unikatowe identyfikatory jednostki, tworzą one klucza podstawowego jednostki.</span><span class="sxs-lookup"><span data-stu-id="aaacd-124">These are the unique identifiers of your entities, as together they form the primary key of an entity.</span></span> <span data-ttu-id="aaacd-125">Można badać przy użyciu następujących wartości szybciej, niż można zapytania innych właściwości jednostki, ponieważ tylko te właściwości są indeksowane.</span><span class="sxs-lookup"><span data-stu-id="aaacd-125">You can query using these values much faster than you can query any other entity properties because only these properties are indexed.</span></span>

<span data-ttu-id="aaacd-126">Używane przez usługę tabeli **PartitionKey** do inteligentnie rozpowszechniają jednostek tabeli węzłów magazynu.</span><span class="sxs-lookup"><span data-stu-id="aaacd-126">The Table service uses **PartitionKey** to intelligently distribute table entities across storage nodes.</span></span> <span data-ttu-id="aaacd-127">Jednostki, które mają taki sam **PartitionKey** są przechowywane w tym samym węźle.</span><span class="sxs-lookup"><span data-stu-id="aaacd-127">Entities that have the same  **PartitionKey** are stored on the same node.</span></span> <span data-ttu-id="aaacd-128">**RowKey** jest unikatowy identyfikator w partycji, należy do jednostki.</span><span class="sxs-lookup"><span data-stu-id="aaacd-128">**RowKey** is the unique ID of the entity within the partition it belongs to.</span></span>

## <a name="update-an-entity"></a><span data-ttu-id="aaacd-129">Aktualizuj jednostkę</span><span class="sxs-lookup"><span data-stu-id="aaacd-129">Update an entity</span></span>

<span data-ttu-id="aaacd-130">Aby zaktualizować wszystkie wartości właściwości jednostki, należy wywołać [update_entity] [ py_update_entity] metody.</span><span class="sxs-lookup"><span data-stu-id="aaacd-130">To update all of an entity's property values, call the [update_entity][py_update_entity] method.</span></span> <span data-ttu-id="aaacd-131">W tym przykładzie pokazano, jak zastąpić istniejącą jednostkę zaktualizowanej wersji:</span><span class="sxs-lookup"><span data-stu-id="aaacd-131">This example shows how to replace an existing entity with an updated version:</span></span>

```python
task = {'PartitionKey': 'tasksSeattle', 'RowKey': '001', 'description' : 'Take out the garbage', 'priority' : 250}
table_service.update_entity('tasktable', task)
```

<span data-ttu-id="aaacd-132">Jeśli jednostka, która jest aktualizowana już nie istnieje, następnie operacji aktualizacji zakończy się niepowodzeniem.</span><span class="sxs-lookup"><span data-stu-id="aaacd-132">If the entity that is being updated doesn't already exist, then the update operation will fail.</span></span> <span data-ttu-id="aaacd-133">Jeśli chcesz przechowywać jednostki tego, czy istnieje lub nie, użyj [insert_or_replace_entity][py_insert_or_replace_entity].</span><span class="sxs-lookup"><span data-stu-id="aaacd-133">If you want to store an entity whether it exists or not, use [insert_or_replace_entity][py_insert_or_replace_entity].</span></span> <span data-ttu-id="aaacd-134">W poniższym przykładzie pierwsze wywołanie spowoduje zastąpienie istniejącej jednostki.</span><span class="sxs-lookup"><span data-stu-id="aaacd-134">In the following example, the first call will replace the existing entity.</span></span> <span data-ttu-id="aaacd-135">Drugie wywołanie będzie wstawić nową jednostkę, ponieważ brak jednostki z określonym PartitionKey i RowKey nie istnieje w tabeli.</span><span class="sxs-lookup"><span data-stu-id="aaacd-135">The second call will insert a new entity, since no entity with the specified PartitionKey and RowKey exists in the table.</span></span>

```python
# Replace the entity created earlier
task = {'PartitionKey': 'tasksSeattle', 'RowKey': '001', 'description' : 'Take out the garbage again', 'priority' : 250}
table_service.insert_or_replace_entity('tasktable', task)

# Insert a new entity
task = {'PartitionKey': 'tasksSeattle', 'RowKey': '003', 'description' : 'Buy detergent', 'priority' : 300}
table_service.insert_or_replace_entity('tasktable', task)
```

> [!TIP]
> <span data-ttu-id="aaacd-136">[Update_entity] [ py_update_entity] metoda zastępuje wszystkie właściwości i wartości istniejącej jednostki, która umożliwia także usunąć właściwości z istniejącej jednostki.</span><span class="sxs-lookup"><span data-stu-id="aaacd-136">The [update_entity][py_update_entity] method replaces all properties and values of an existing entity, which you can also use to remove properties from an existing entity.</span></span> <span data-ttu-id="aaacd-137">Można użyć [merge_entity] [ py_merge_entity] metody do zaktualizowania istniejącej jednostki z wartościami właściwości nowe lub zmodyfikowane bez całkowicie zastępowania jednostki.</span><span class="sxs-lookup"><span data-stu-id="aaacd-137">You can use the [merge_entity][py_merge_entity] method to update an existing entity with new or modified property values without completely replacing the entity.</span></span>

## <a name="modify-multiple-entities"></a><span data-ttu-id="aaacd-138">Modyfikowanie wiele jednostek</span><span class="sxs-lookup"><span data-stu-id="aaacd-138">Modify multiple entities</span></span>

<span data-ttu-id="aaacd-139">W celu zapewnienia atomic przetwarzania żądania przez usługę tabeli, możesz przesłać wiele operacji ze sobą w partii.</span><span class="sxs-lookup"><span data-stu-id="aaacd-139">To ensure the atomic processing of a request by the Table service, you can submit multiple operations together in a batch.</span></span> <span data-ttu-id="aaacd-140">Najpierw użyj [TableBatch] [ py_TableBatch] klasy, aby dodać wiele operacji do pojedynczej partii.</span><span class="sxs-lookup"><span data-stu-id="aaacd-140">First, use the [TableBatch][py_TableBatch] class to add multiple operations to a single batch.</span></span> <span data-ttu-id="aaacd-141">Następnie wywołaj [TableService][py_TableService].[ commit_batch] [ py_commit_batch] przesłać operacje w niepodzielną operację.</span><span class="sxs-lookup"><span data-stu-id="aaacd-141">Next, call [TableService][py_TableService].[commit_batch][py_commit_batch] to submit the operations in an atomic operation.</span></span> <span data-ttu-id="aaacd-142">Wszystkie jednostki można zmodyfikować w partii musi należeć do tej samej partycji.</span><span class="sxs-lookup"><span data-stu-id="aaacd-142">All entities to be modified in batch must be in the same partition.</span></span>

<span data-ttu-id="aaacd-143">W tym przykładzie dodaje dwie jednostki w partii:</span><span class="sxs-lookup"><span data-stu-id="aaacd-143">This example adds two entities together in a batch:</span></span>

```python
from azure.storage.table import TableBatch
batch = TableBatch()
task004 = {'PartitionKey': 'tasksSeattle', 'RowKey': '004', 'description' : 'Go grocery shopping', 'priority' : 400}
task005 = {'PartitionKey': 'tasksSeattle', 'RowKey': '005', 'description' : 'Clean the bathroom', 'priority' : 100}
batch.insert_entity(task004)
batch.insert_entity(task005)
table_service.commit_batch('tasktable', batch)
```

<span data-ttu-id="aaacd-144">Partie można również przy użyciu składni Menedżera kontekstu:</span><span class="sxs-lookup"><span data-stu-id="aaacd-144">Batches can also be used with the context manager syntax:</span></span>

```python
task006 = {'PartitionKey': 'tasksSeattle', 'RowKey': '006', 'description' : 'Go grocery shopping', 'priority' : 400}
task007 = {'PartitionKey': 'tasksSeattle', 'RowKey': '007', 'description' : 'Clean the bathroom', 'priority' : 100}

with table_service.batch('tasktable') as batch:
    batch.insert_entity(task006)
    batch.insert_entity(task007)
```

## <a name="query-for-an-entity"></a><span data-ttu-id="aaacd-145">Zapytanie dla jednostki</span><span class="sxs-lookup"><span data-stu-id="aaacd-145">Query for an entity</span></span>

<span data-ttu-id="aaacd-146">Aby wyszukać jednostkę w tabeli, należy przekazać jego PartitionKey i RowKey do [TableService][py_TableService].[ get_entity] [ py_get_entity] metody.</span><span class="sxs-lookup"><span data-stu-id="aaacd-146">To query for an entity in a table, pass its PartitionKey and RowKey to the [TableService][py_TableService].[get_entity][py_get_entity] method.</span></span>

```python
task = table_service.get_entity('tasktable', 'tasksSeattle', '001')
print(task.description)
print(task.priority)
```

## <a name="query-a-set-of-entities"></a><span data-ttu-id="aaacd-147">Zapytanie zestawu jednostek</span><span class="sxs-lookup"><span data-stu-id="aaacd-147">Query a set of entities</span></span>

<span data-ttu-id="aaacd-148">Można wyszukać zestawu jednostek, podając ciąg filtru z **filtru** parametru.</span><span class="sxs-lookup"><span data-stu-id="aaacd-148">You can query for a set of entities by supplying a filter string with the **filter** parameter.</span></span> <span data-ttu-id="aaacd-149">W tym przykładzie znajduje wszystkie zadania w Seattle, stosując filtr na PartitionKey:</span><span class="sxs-lookup"><span data-stu-id="aaacd-149">This example finds all tasks in Seattle by applying a filter on PartitionKey:</span></span>

```python
tasks = table_service.query_entities('tasktable', filter="PartitionKey eq 'tasksSeattle'")
for task in tasks:
    print(task.description)
    print(task.priority)
```

## <a name="query-a-subset-of-entity-properties"></a><span data-ttu-id="aaacd-150">Tworzenie zapytania do podzbioru właściwości jednostki</span><span class="sxs-lookup"><span data-stu-id="aaacd-150">Query a subset of entity properties</span></span>

<span data-ttu-id="aaacd-151">Można również ograniczyć, właściwości, które są zwracane dla każdej jednostki w zapytaniu.</span><span class="sxs-lookup"><span data-stu-id="aaacd-151">You can also restrict which properties are returned for each entity in a query.</span></span> <span data-ttu-id="aaacd-152">Ta technika, zwana *projekcji*, redukuje przepustowość i może poprawiać wydajność zapytań, zwłaszcza w przypadku dużych jednostek lub zestawów wyników.</span><span class="sxs-lookup"><span data-stu-id="aaacd-152">This technique, called *projection*, reduces bandwidth and can improve query performance, especially for large entities or result sets.</span></span> <span data-ttu-id="aaacd-153">Użyj **wybierz** parametru i przekazać nazwy właściwości, które jest zwracana do klienta.</span><span class="sxs-lookup"><span data-stu-id="aaacd-153">Use the **select** parameter and pass the names of the properties you want returned to the client.</span></span>

<span data-ttu-id="aaacd-154">Zapytanie w poniższym kodzie zwraca tylko opisy jednostek w tabeli.</span><span class="sxs-lookup"><span data-stu-id="aaacd-154">The query in the following code returns only the descriptions of entities in the table.</span></span>

> [!NOTE]
> <span data-ttu-id="aaacd-155">Poniższy fragment działa tylko w usłudze Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="aaacd-155">The following snippet works only against the Azure Storage.</span></span> <span data-ttu-id="aaacd-156">Nie jest obsługiwana przez emulator magazynu.</span><span class="sxs-lookup"><span data-stu-id="aaacd-156">It is not supported by the storage emulator.</span></span>

```python
tasks = table_service.query_entities('tasktable', filter="PartitionKey eq 'tasksSeattle'", select='description')
for task in tasks:
    print(task.description)
```

## <a name="delete-an-entity"></a><span data-ttu-id="aaacd-157">Usuwanie jednostki</span><span class="sxs-lookup"><span data-stu-id="aaacd-157">Delete an entity</span></span>

<span data-ttu-id="aaacd-158">Usuwanie jednostki przez przekazanie jej PartitionKey i RowKey do [delete_entity] [ py_delete_entity] metody.</span><span class="sxs-lookup"><span data-stu-id="aaacd-158">Delete an entity by passing its PartitionKey and RowKey to the [delete_entity][py_delete_entity] method.</span></span>

```python
table_service.delete_entity('tasktable', 'tasksSeattle', '001')
```

## <a name="delete-a-table"></a><span data-ttu-id="aaacd-159">Usuwanie tabeli</span><span class="sxs-lookup"><span data-stu-id="aaacd-159">Delete a table</span></span>

<span data-ttu-id="aaacd-160">Jeśli nie są już potrzebne tabeli lub dowolnej jednostki w niej wywołanie [delete_table] [ py_delete_table] metodę, aby trwale usunąć tabelę z usługi Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="aaacd-160">If you no longer need a table or any of the entities within it, call the [delete_table][py_delete_table] method to permanently delete the table from Azure Storage.</span></span>

```python
table_service.delete_table('tasktable')
```

## <a name="next-steps"></a><span data-ttu-id="aaacd-161">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="aaacd-161">Next steps</span></span>

* [<span data-ttu-id="aaacd-162">Azure Storage SDK for Python API reference</span><span class="sxs-lookup"><span data-stu-id="aaacd-162">Azure Storage SDK for Python API reference</span></span>](https://azure-storage.readthedocs.io/en/latest/index.html)
* [<span data-ttu-id="aaacd-163">Magazyn Azure SDK dla języka Python</span><span class="sxs-lookup"><span data-stu-id="aaacd-163">Azure Storage SDK for Python</span></span>](https://github.com/Azure/azure-storage-python)
* [<span data-ttu-id="aaacd-164">Centrum deweloperów języka Python</span><span class="sxs-lookup"><span data-stu-id="aaacd-164">Python Developer Center</span></span>](https://azure.microsoft.com/develop/python/)
* <span data-ttu-id="aaacd-165">[Eksplorator magazynu Microsoft Azure](../vs-azure-tools-storage-manage-with-storage-explorer.md): wolne, i platform aplikacji do pracy wizualnie z danymi usługi Azure Storage w systemie Windows, macOS i Linux.</span><span class="sxs-lookup"><span data-stu-id="aaacd-165">[Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md): A free, cross-platform application for working visually with Azure Storage data on Windows, macOS, and Linux.</span></span>

[py_commit_batch]: https://azure-storage.readthedocs.io/en/latest/ref/azure.storage.table.tableservice.html#azure.storage.table.tableservice.TableService.commit_batch
[py_create_table]: https://azure-storage.readthedocs.io/en/latest/ref/azure.storage.table.tableservice.html#azure.storage.table.tableservice.TableService.create_table
[py_delete_entity]: https://azure-storage.readthedocs.io/en/latest/ref/azure.storage.table.tableservice.html#azure.storage.table.tableservice.TableService.delete_entity
[py_delete_table]: https://azure-storage.readthedocs.io/en/latest/ref/azure.storage.table.tableservice.html#azure.storage.table.tableservice.TableService.delete_table
[py_Entity]: https://azure-storage.readthedocs.io/en/latest/ref/azure.storage.table.models.html#azure.storage.table.models.Entity
[py_get_entity]: https://azure-storage.readthedocs.io/en/latest/ref/azure.storage.table.tableservice.html#azure.storage.table.tableservice.TableService.get_entity
[py_insert_entity]: https://azure-storage.readthedocs.io/en/latest/ref/azure.storage.table.tableservice.html#azure.storage.table.tableservice.TableService.insert_entity
[py_insert_or_replace_entity]: https://azure-storage.readthedocs.io/en/latest/ref/azure.storage.table.tableservice.html#azure.storage.table.tableservice.TableService.insert_or_replace_entity
[py_merge_entity]: https://azure-storage.readthedocs.io/en/latest/ref/azure.storage.table.tableservice.html#azure.storage.table.tableservice.TableService.merge_entity
[py_update_entity]: https://azure-storage.readthedocs.io/en/latest/ref/azure.storage.table.tableservice.html#azure.storage.table.tableservice.TableService.update_entity
[py_TableService]: https://azure-storage.readthedocs.io/en/latest/ref/azure.storage.table.tableservice.html
[py_TableBatch]: https://azure-storage.readthedocs.io/en/latest/ref/azure.storage.table.tablebatch.html#azure.storage.table.tablebatch.TableBatch
