---
title: toouse aaaHow magazynu tabel Azure z Python | Dokumentacja firmy Microsoft
description: "Przechowywanie danych strukturalnych w chmurze hello przy użyciu magazynu tabel Azure, Magazyn danych NoSQL."
services: cosmos-db
documentationcenter: python
author: mimig1
manager: jhubbard
editor: tysonn
ms.assetid: 7ddb9f3e-4e6d-4103-96e6-f0351d69a17b
ms.service: cosmos-db
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: python
ms.topic: article
ms.date: 05/16/2017
ms.author: mimig
ms.openlocfilehash: 3382fcd5667a93d5533b5f8fad1d3d1c27f23482
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-table-storage-in-python"></a><span data-ttu-id="61c48-103">Jak toouse magazynu tabel w języku Python</span><span class="sxs-lookup"><span data-stu-id="61c48-103">How toouse Table storage in Python</span></span>

[!INCLUDE [storage-selector-table-include](../../includes/storage-selector-table-include.md)]
[!INCLUDE [storage-table-cosmos-db-langsoon-tip-include](../../includes/storage-table-cosmos-db-langsoon-tip-include.md)]

<span data-ttu-id="61c48-104">Ten przewodnik przedstawia, jak hello tooperform tabel Azure magazynu scenariuszach w języku Python za pomocą [Microsoft Azure magazynu SDK dla języka Python](https://github.com/Azure/azure-storage-python).</span><span class="sxs-lookup"><span data-stu-id="61c48-104">This guide shows you how tooperform common Azure Table storage scenarios in Python using hello [Microsoft Azure Storage SDK for Python](https://github.com/Azure/azure-storage-python).</span></span> <span data-ttu-id="61c48-105">omówione scenariusze Hello obejmują tworzenia i usuwania tabeli, wstawianie i badania jednostek.</span><span class="sxs-lookup"><span data-stu-id="61c48-105">hello scenarios covered include creating and deleting a table, and inserting and querying entities.</span></span>

<span data-ttu-id="61c48-106">Podczas pracy nad hello scenariusze w tym samouczku, warto zapoznać się z toorefer toohello [Azure Storage SDK for Python API reference](https://azure-storage.readthedocs.io/en/latest/index.html).</span><span class="sxs-lookup"><span data-stu-id="61c48-106">While working through hello scenarios in this tutorial, you may wish toorefer toohello [Azure Storage SDK for Python API reference](https://azure-storage.readthedocs.io/en/latest/index.html).</span></span>

[!INCLUDE [storage-table-concepts-include](../../includes/storage-table-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/storage-create-account-include.md)]

## <a name="install-hello-azure-storage-sdk-for-python"></a><span data-ttu-id="61c48-107">Zainstaluj hello zestawu SDK usługi Magazyn Azure dla języka Python</span><span class="sxs-lookup"><span data-stu-id="61c48-107">Install hello Azure Storage SDK for Python</span></span>

<span data-ttu-id="61c48-108">Po utworzeniu konta magazynu, następnym krokiem jest tooinstall hello [Microsoft Azure magazynu SDK dla języka Python](https://github.com/Azure/azure-storage-python).</span><span class="sxs-lookup"><span data-stu-id="61c48-108">Once you've created a storage account, your next step is tooinstall hello [Microsoft Azure Storage SDK for Python](https://github.com/Azure/azure-storage-python).</span></span> <span data-ttu-id="61c48-109">Aby uzyskać więcej informacji na temat instalowania hello zestawu SDK, zobacz toohello [README.rst](https://github.com/Azure/azure-storage-python/blob/master/README.rst) pliku w hello zestawu SDK usługi Magazyn dla języka Python repozytorium w witrynie GitHub.</span><span class="sxs-lookup"><span data-stu-id="61c48-109">For details on installing hello SDK, refer toohello [README.rst](https://github.com/Azure/azure-storage-python/blob/master/README.rst) file in hello Storage SDK for Python repository on GitHub.</span></span>

## <a name="create-a-table"></a><span data-ttu-id="61c48-110">Tworzenie tabeli</span><span class="sxs-lookup"><span data-stu-id="61c48-110">Create a table</span></span>

<span data-ttu-id="61c48-111">toowork z hello usługi Azure tabel w języku Python, należy zaimportować hello [TableService] [ py_TableService] modułu.</span><span class="sxs-lookup"><span data-stu-id="61c48-111">toowork with hello Azure Table service in Python, you must import hello [TableService][py_TableService] module.</span></span> <span data-ttu-id="61c48-112">Ponieważ będzie działać z jednostek tabeli, należy również hello [jednostki] [ py_Entity] klasy.</span><span class="sxs-lookup"><span data-stu-id="61c48-112">Since you'll be working with Table entities, you also need hello [Entity][py_Entity] class.</span></span> <span data-ttu-id="61c48-113">Dodaj ten kod na górze hello programu Python pliku tooimport zarówno:</span><span class="sxs-lookup"><span data-stu-id="61c48-113">Add this code near hello top your Python file tooimport both:</span></span>

```python
from azure.storage.table import TableService, Entity
```

<span data-ttu-id="61c48-114">Utwórz [TableService] [ py_TableService] obiektu, przekazując klucz konta magazynu nazwy i konta.</span><span class="sxs-lookup"><span data-stu-id="61c48-114">Create a [TableService][py_TableService] object, passing in your storage account name and account key.</span></span> <span data-ttu-id="61c48-115">Zastąp `myaccount` i `mykey` z nazwą konta i klucz i wywołanie [create_table] [ py_create_table] toocreate hello tabeli w usłudze Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="61c48-115">Replace `myaccount` and `mykey` with your account name and key, and call [create_table][py_create_table] toocreate hello table in Azure Storage.</span></span>

```python
table_service = TableService(account_name='myaccount', account_key='mykey')

table_service.create_table('tasktable')
```

## <a name="add-an-entity-tooa-table"></a><span data-ttu-id="61c48-116">Dodaj tabelę tooa jednostki</span><span class="sxs-lookup"><span data-stu-id="61c48-116">Add an entity tooa table</span></span>

<span data-ttu-id="61c48-117">tooadd jednostki, należy najpierw utworzyć obiekt, który reprezentuje jednostki, następnie przebiegu hello obiektu toohello [TableService][py_TableService].[ insert_entity] [ py_insert_entity] metody.</span><span class="sxs-lookup"><span data-stu-id="61c48-117">tooadd an entity, you first create an object that represents your entity, then pass hello object toohello [TableService][py_TableService].[insert_entity][py_insert_entity] method.</span></span> <span data-ttu-id="61c48-118">Obiekt jednostki Hello może być słownika lub typu obiektu [jednostki][py_Entity]i definiuje użytkownika jednostki nazwy i wartości właściwości.</span><span class="sxs-lookup"><span data-stu-id="61c48-118">hello entity object can be a dictionary or an object of type [Entity][py_Entity], and defines your entity's property names and values.</span></span> <span data-ttu-id="61c48-119">Każdy podmiot musi zawierać hello wymagane [PartitionKey i RowKey](#partitionkey-and-rowkey) właściwości, w tooany dodanie innych właściwości można zdefiniować hello jednostki.</span><span class="sxs-lookup"><span data-stu-id="61c48-119">Every entity must include hello required [PartitionKey and RowKey](#partitionkey-and-rowkey) properties, in addition tooany other properties you define for hello entity.</span></span>

<span data-ttu-id="61c48-120">Ten przykład tworzy obiekt słownika następnie reprezentujący jednostkę, przekazuje on toohello [insert_entity] [ py_insert_entity] tooadd metody go toohello tabeli:</span><span class="sxs-lookup"><span data-stu-id="61c48-120">This example creates a dictionary object representing an entity, then passes it toohello [insert_entity][py_insert_entity] method tooadd it toohello table:</span></span>

```python
task = {'PartitionKey': 'tasksSeattle', 'RowKey': '001', 'description' : 'Take out hello trash', 'priority' : 200}
table_service.insert_entity('tasktable', task)
```

<span data-ttu-id="61c48-121">Ten przykład tworzy [jednostki] [ py_Entity] obiekt, a następnie przechodzi on toohello [insert_entity] [ py_insert_entity] tooadd — metoda go toohello tabeli:</span><span class="sxs-lookup"><span data-stu-id="61c48-121">This example creates an [Entity][py_Entity] object, then passes it toohello [insert_entity][py_insert_entity] method tooadd it toohello table:</span></span>

```python
task = Entity()
task.PartitionKey = 'tasksSeattle'
task.RowKey = '002'
task.description = 'Wash hello car'
task.priority = 100
table_service.insert_entity('tasktable', task)
```

### <a name="partitionkey-and-rowkey"></a><span data-ttu-id="61c48-122">PartitionKey i RowKey</span><span class="sxs-lookup"><span data-stu-id="61c48-122">PartitionKey and RowKey</span></span>

<span data-ttu-id="61c48-123">Należy określić zarówno **PartitionKey** i **RowKey** właściwości dla każdej jednostki.</span><span class="sxs-lookup"><span data-stu-id="61c48-123">You must specify both a **PartitionKey** and a **RowKey** property for every entity.</span></span> <span data-ttu-id="61c48-124">Jak razem są unikatowe identyfikatory hello jednostki, tworzą one hello klucza podstawowego jednostki.</span><span class="sxs-lookup"><span data-stu-id="61c48-124">These are hello unique identifiers of your entities, as together they form hello primary key of an entity.</span></span> <span data-ttu-id="61c48-125">Można badać przy użyciu następujących wartości szybciej, niż można zapytania innych właściwości jednostki, ponieważ tylko te właściwości są indeksowane.</span><span class="sxs-lookup"><span data-stu-id="61c48-125">You can query using these values much faster than you can query any other entity properties because only these properties are indexed.</span></span>

<span data-ttu-id="61c48-126">Witaj używa usługi tabeli **PartitionKey** toointelligently rozpowszechniają jednostek tabeli węzłów magazynu.</span><span class="sxs-lookup"><span data-stu-id="61c48-126">hello Table service uses **PartitionKey** toointelligently distribute table entities across storage nodes.</span></span> <span data-ttu-id="61c48-127">Tekst hello obiektów, które mają takie same **PartitionKey** są przechowywane na powitania tym samym węźle.</span><span class="sxs-lookup"><span data-stu-id="61c48-127">Entities that have hello same  **PartitionKey** are stored on hello same node.</span></span> <span data-ttu-id="61c48-128">**RowKey** jest unikatowy identyfikator hello hello jednostek w partycji hello należy.</span><span class="sxs-lookup"><span data-stu-id="61c48-128">**RowKey** is hello unique ID of hello entity within hello partition it belongs to.</span></span>

## <a name="update-an-entity"></a><span data-ttu-id="61c48-129">Aktualizuj jednostkę</span><span class="sxs-lookup"><span data-stu-id="61c48-129">Update an entity</span></span>

<span data-ttu-id="61c48-130">tooupdate wszystkich wartości właściwości jednostki, wywołaj hello [update_entity] [ py_update_entity] metody.</span><span class="sxs-lookup"><span data-stu-id="61c48-130">tooupdate all of an entity's property values, call hello [update_entity][py_update_entity] method.</span></span> <span data-ttu-id="61c48-131">W tym przykładzie pokazano sposób tooreplace istniejącej jednostki zaktualizowaną wersją:</span><span class="sxs-lookup"><span data-stu-id="61c48-131">This example shows how tooreplace an existing entity with an updated version:</span></span>

```python
task = {'PartitionKey': 'tasksSeattle', 'RowKey': '001', 'description' : 'Take out hello garbage', 'priority' : 250}
table_service.update_entity('tasktable', task)
```

<span data-ttu-id="61c48-132">Jeśli hello jednostki, która jest aktualizowana już nie istnieje, nie będą hello operacji aktualizacji.</span><span class="sxs-lookup"><span data-stu-id="61c48-132">If hello entity that is being updated doesn't already exist, then hello update operation will fail.</span></span> <span data-ttu-id="61c48-133">Toostore jednostki czy istnieje lub nie, należy użyć [insert_or_replace_entity][py_insert_or_replace_entity].</span><span class="sxs-lookup"><span data-stu-id="61c48-133">If you want toostore an entity whether it exists or not, use [insert_or_replace_entity][py_insert_or_replace_entity].</span></span> <span data-ttu-id="61c48-134">W hello poniższy przykład pierwsze wywołanie hello spowoduje zastąpienie istniejącej jednostki hello.</span><span class="sxs-lookup"><span data-stu-id="61c48-134">In hello following example, hello first call will replace hello existing entity.</span></span> <span data-ttu-id="61c48-135">drugie wywołanie Hello powoduje wstawienie nowego obiektu, ponieważ nie jednostki o hello określone PartitionKey i RowKey istnieje w tabeli hello.</span><span class="sxs-lookup"><span data-stu-id="61c48-135">hello second call will insert a new entity, since no entity with hello specified PartitionKey and RowKey exists in hello table.</span></span>

```python
# Replace hello entity created earlier
task = {'PartitionKey': 'tasksSeattle', 'RowKey': '001', 'description' : 'Take out hello garbage again', 'priority' : 250}
table_service.insert_or_replace_entity('tasktable', task)

# Insert a new entity
task = {'PartitionKey': 'tasksSeattle', 'RowKey': '003', 'description' : 'Buy detergent', 'priority' : 300}
table_service.insert_or_replace_entity('tasktable', task)
```

> [!TIP]
> <span data-ttu-id="61c48-136">Witaj [update_entity] [ py_update_entity] metoda zastępuje wszystkie właściwości i wartości istniejącej jednostki, które można również użyć właściwości tooremove z istniejącej jednostki.</span><span class="sxs-lookup"><span data-stu-id="61c48-136">hello [update_entity][py_update_entity] method replaces all properties and values of an existing entity, which you can also use tooremove properties from an existing entity.</span></span> <span data-ttu-id="61c48-137">Można użyć hello [merge_entity] [ py_merge_entity] tooupdate metody istniejącej jednostki z wartościami właściwości nowe lub zmodyfikowane bez całkowicie zastępowania hello jednostki.</span><span class="sxs-lookup"><span data-stu-id="61c48-137">You can use hello [merge_entity][py_merge_entity] method tooupdate an existing entity with new or modified property values without completely replacing hello entity.</span></span>

## <a name="modify-multiple-entities"></a><span data-ttu-id="61c48-138">Modyfikowanie wiele jednostek</span><span class="sxs-lookup"><span data-stu-id="61c48-138">Modify multiple entities</span></span>

<span data-ttu-id="61c48-139">tooensure hello atomic przetwarzania żądania przez usługę tabeli hello, mogą przesyłać wiele operacji ze sobą w partii.</span><span class="sxs-lookup"><span data-stu-id="61c48-139">tooensure hello atomic processing of a request by hello Table service, you can submit multiple operations together in a batch.</span></span> <span data-ttu-id="61c48-140">Najpierw użyj hello [TableBatch] [ py_TableBatch] klasy tooadd wiele operacji tooa pojedyncza partia.</span><span class="sxs-lookup"><span data-stu-id="61c48-140">First, use hello [TableBatch][py_TableBatch] class tooadd multiple operations tooa single batch.</span></span> <span data-ttu-id="61c48-141">Następnie wywołaj [TableService][py_TableService].[ commit_batch] [ py_commit_batch] toosubmit hello operacje w niepodzielną operację.</span><span class="sxs-lookup"><span data-stu-id="61c48-141">Next, call [TableService][py_TableService].[commit_batch][py_commit_batch] toosubmit hello operations in an atomic operation.</span></span> <span data-ttu-id="61c48-142">Wszystkie toobe jednostek zmodyfikowane w partii musi należeć do hello tej samej partycji.</span><span class="sxs-lookup"><span data-stu-id="61c48-142">All entities toobe modified in batch must be in hello same partition.</span></span>

<span data-ttu-id="61c48-143">W tym przykładzie dodaje dwie jednostki w partii:</span><span class="sxs-lookup"><span data-stu-id="61c48-143">This example adds two entities together in a batch:</span></span>

```python
from azure.storage.table import TableBatch
batch = TableBatch()
task004 = {'PartitionKey': 'tasksSeattle', 'RowKey': '004', 'description' : 'Go grocery shopping', 'priority' : 400}
task005 = {'PartitionKey': 'tasksSeattle', 'RowKey': '005', 'description' : 'Clean hello bathroom', 'priority' : 100}
batch.insert_entity(task004)
batch.insert_entity(task005)
table_service.commit_batch('tasktable', batch)
```

<span data-ttu-id="61c48-144">Partie można również ze składnią Menedżera kontekstu hello:</span><span class="sxs-lookup"><span data-stu-id="61c48-144">Batches can also be used with hello context manager syntax:</span></span>

```python
task006 = {'PartitionKey': 'tasksSeattle', 'RowKey': '006', 'description' : 'Go grocery shopping', 'priority' : 400}
task007 = {'PartitionKey': 'tasksSeattle', 'RowKey': '007', 'description' : 'Clean hello bathroom', 'priority' : 100}

with table_service.batch('tasktable') as batch:
    batch.insert_entity(task006)
    batch.insert_entity(task007)
```

## <a name="query-for-an-entity"></a><span data-ttu-id="61c48-145">Zapytanie dla jednostki</span><span class="sxs-lookup"><span data-stu-id="61c48-145">Query for an entity</span></span>

<span data-ttu-id="61c48-146">tooquery dla jednostki w tabeli, Przekaż jego toohello PartitionKey i RowKey [TableService][py_TableService].[ get_entity] [ py_get_entity] metody.</span><span class="sxs-lookup"><span data-stu-id="61c48-146">tooquery for an entity in a table, pass its PartitionKey and RowKey toohello [TableService][py_TableService].[get_entity][py_get_entity] method.</span></span>

```python
task = table_service.get_entity('tasktable', 'tasksSeattle', '001')
print(task.description)
print(task.priority)
```

## <a name="query-a-set-of-entities"></a><span data-ttu-id="61c48-147">Zapytanie zestawu jednostek</span><span class="sxs-lookup"><span data-stu-id="61c48-147">Query a set of entities</span></span>

<span data-ttu-id="61c48-148">Można zapytania dla zestawu jednostek, podając ciąg filtru z hello **filtru** parametru.</span><span class="sxs-lookup"><span data-stu-id="61c48-148">You can query for a set of entities by supplying a filter string with hello **filter** parameter.</span></span> <span data-ttu-id="61c48-149">W tym przykładzie znajduje wszystkie zadania w Seattle, stosując filtr na PartitionKey:</span><span class="sxs-lookup"><span data-stu-id="61c48-149">This example finds all tasks in Seattle by applying a filter on PartitionKey:</span></span>

```python
tasks = table_service.query_entities('tasktable', filter="PartitionKey eq 'tasksSeattle'")
for task in tasks:
    print(task.description)
    print(task.priority)
```

## <a name="query-a-subset-of-entity-properties"></a><span data-ttu-id="61c48-150">Tworzenie zapytania do podzbioru właściwości jednostki</span><span class="sxs-lookup"><span data-stu-id="61c48-150">Query a subset of entity properties</span></span>

<span data-ttu-id="61c48-151">Można również ograniczyć, właściwości, które są zwracane dla każdej jednostki w zapytaniu.</span><span class="sxs-lookup"><span data-stu-id="61c48-151">You can also restrict which properties are returned for each entity in a query.</span></span> <span data-ttu-id="61c48-152">Ta technika, zwana *projekcji*, redukuje przepustowość i może poprawiać wydajność zapytań, zwłaszcza w przypadku dużych jednostek lub zestawów wyników.</span><span class="sxs-lookup"><span data-stu-id="61c48-152">This technique, called *projection*, reduces bandwidth and can improve query performance, especially for large entities or result sets.</span></span> <span data-ttu-id="61c48-153">Użyj hello **wybierz** parametru i przekazać hello nazwy właściwości hello mają zwrócił toohello klienta.</span><span class="sxs-lookup"><span data-stu-id="61c48-153">Use hello **select** parameter and pass hello names of hello properties you want returned toohello client.</span></span>

<span data-ttu-id="61c48-154">Zapytanie Hello w hello następującego kodu zwraca tylko hello opisy jednostek w tabeli hello.</span><span class="sxs-lookup"><span data-stu-id="61c48-154">hello query in hello following code returns only hello descriptions of entities in hello table.</span></span>

> [!NOTE]
> <span data-ttu-id="61c48-155">powitania po fragment działa tylko wobec hello Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="61c48-155">hello following snippet works only against hello Azure Storage.</span></span> <span data-ttu-id="61c48-156">Nie jest obsługiwana przez emulator magazynu hello.</span><span class="sxs-lookup"><span data-stu-id="61c48-156">It is not supported by hello storage emulator.</span></span>

```python
tasks = table_service.query_entities('tasktable', filter="PartitionKey eq 'tasksSeattle'", select='description')
for task in tasks:
    print(task.description)
```

## <a name="delete-an-entity"></a><span data-ttu-id="61c48-157">Usuwanie jednostki</span><span class="sxs-lookup"><span data-stu-id="61c48-157">Delete an entity</span></span>

<span data-ttu-id="61c48-158">Usuwanie jednostki przez przekazanie jej toohello PartitionKey i RowKey [delete_entity] [ py_delete_entity] metody.</span><span class="sxs-lookup"><span data-stu-id="61c48-158">Delete an entity by passing its PartitionKey and RowKey toohello [delete_entity][py_delete_entity] method.</span></span>

```python
table_service.delete_entity('tasktable', 'tasksSeattle', '001')
```

## <a name="delete-a-table"></a><span data-ttu-id="61c48-159">Usuwanie tabeli</span><span class="sxs-lookup"><span data-stu-id="61c48-159">Delete a table</span></span>

<span data-ttu-id="61c48-160">Jeśli nie są już potrzebne tabeli ani żadnych jednostek hello w niej wywołanie hello [delete_table] [ py_delete_table] toopermanently metody Usuń tabelę hello z usługi Magazyn Azure.</span><span class="sxs-lookup"><span data-stu-id="61c48-160">If you no longer need a table or any of hello entities within it, call hello [delete_table][py_delete_table] method toopermanently delete hello table from Azure Storage.</span></span>

```python
table_service.delete_table('tasktable')
```

## <a name="next-steps"></a><span data-ttu-id="61c48-161">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="61c48-161">Next steps</span></span>

* [<span data-ttu-id="61c48-162">Azure Storage SDK for Python API reference</span><span class="sxs-lookup"><span data-stu-id="61c48-162">Azure Storage SDK for Python API reference</span></span>](https://azure-storage.readthedocs.io/en/latest/index.html)
* [<span data-ttu-id="61c48-163">Magazyn Azure SDK dla języka Python</span><span class="sxs-lookup"><span data-stu-id="61c48-163">Azure Storage SDK for Python</span></span>](https://github.com/Azure/azure-storage-python)
* [<span data-ttu-id="61c48-164">Centrum deweloperów języka Python</span><span class="sxs-lookup"><span data-stu-id="61c48-164">Python Developer Center</span></span>](https://azure.microsoft.com/develop/python/)
* <span data-ttu-id="61c48-165">[Eksplorator magazynu Microsoft Azure](../vs-azure-tools-storage-manage-with-storage-explorer.md): wolne, i platform aplikacji do pracy wizualnie z danymi usługi Azure Storage w systemie Windows, macOS i Linux.</span><span class="sxs-lookup"><span data-stu-id="61c48-165">[Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md): A free, cross-platform application for working visually with Azure Storage data on Windows, macOS, and Linux.</span></span>

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
