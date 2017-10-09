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
# <a name="how-toouse-table-storage-in-python"></a>Jak toouse magazynu tabel w języku Python

[!INCLUDE [storage-selector-table-include](../../includes/storage-selector-table-include.md)]
[!INCLUDE [storage-table-cosmos-db-langsoon-tip-include](../../includes/storage-table-cosmos-db-langsoon-tip-include.md)]

Ten przewodnik przedstawia, jak hello tooperform tabel Azure magazynu scenariuszach w języku Python za pomocą [Microsoft Azure magazynu SDK dla języka Python](https://github.com/Azure/azure-storage-python). omówione scenariusze Hello obejmują tworzenia i usuwania tabeli, wstawianie i badania jednostek.

Podczas pracy nad hello scenariusze w tym samouczku, warto zapoznać się z toorefer toohello [Azure Storage SDK for Python API reference](https://azure-storage.readthedocs.io/en/latest/index.html).

[!INCLUDE [storage-table-concepts-include](../../includes/storage-table-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/storage-create-account-include.md)]

## <a name="install-hello-azure-storage-sdk-for-python"></a>Zainstaluj hello zestawu SDK usługi Magazyn Azure dla języka Python

Po utworzeniu konta magazynu, następnym krokiem jest tooinstall hello [Microsoft Azure magazynu SDK dla języka Python](https://github.com/Azure/azure-storage-python). Aby uzyskać więcej informacji na temat instalowania hello zestawu SDK, zobacz toohello [README.rst](https://github.com/Azure/azure-storage-python/blob/master/README.rst) pliku w hello zestawu SDK usługi Magazyn dla języka Python repozytorium w witrynie GitHub.

## <a name="create-a-table"></a>Tworzenie tabeli

toowork z hello usługi Azure tabel w języku Python, należy zaimportować hello [TableService] [ py_TableService] modułu. Ponieważ będzie działać z jednostek tabeli, należy również hello [jednostki] [ py_Entity] klasy. Dodaj ten kod na górze hello programu Python pliku tooimport zarówno:

```python
from azure.storage.table import TableService, Entity
```

Utwórz [TableService] [ py_TableService] obiektu, przekazując klucz konta magazynu nazwy i konta. Zastąp `myaccount` i `mykey` z nazwą konta i klucz i wywołanie [create_table] [ py_create_table] toocreate hello tabeli w usłudze Azure Storage.

```python
table_service = TableService(account_name='myaccount', account_key='mykey')

table_service.create_table('tasktable')
```

## <a name="add-an-entity-tooa-table"></a>Dodaj tabelę tooa jednostki

tooadd jednostki, należy najpierw utworzyć obiekt, który reprezentuje jednostki, następnie przebiegu hello obiektu toohello [TableService][py_TableService].[ insert_entity] [ py_insert_entity] metody. Obiekt jednostki Hello może być słownika lub typu obiektu [jednostki][py_Entity]i definiuje użytkownika jednostki nazwy i wartości właściwości. Każdy podmiot musi zawierać hello wymagane [PartitionKey i RowKey](#partitionkey-and-rowkey) właściwości, w tooany dodanie innych właściwości można zdefiniować hello jednostki.

Ten przykład tworzy obiekt słownika następnie reprezentujący jednostkę, przekazuje on toohello [insert_entity] [ py_insert_entity] tooadd metody go toohello tabeli:

```python
task = {'PartitionKey': 'tasksSeattle', 'RowKey': '001', 'description' : 'Take out hello trash', 'priority' : 200}
table_service.insert_entity('tasktable', task)
```

Ten przykład tworzy [jednostki] [ py_Entity] obiekt, a następnie przechodzi on toohello [insert_entity] [ py_insert_entity] tooadd — metoda go toohello tabeli:

```python
task = Entity()
task.PartitionKey = 'tasksSeattle'
task.RowKey = '002'
task.description = 'Wash hello car'
task.priority = 100
table_service.insert_entity('tasktable', task)
```

### <a name="partitionkey-and-rowkey"></a>PartitionKey i RowKey

Należy określić zarówno **PartitionKey** i **RowKey** właściwości dla każdej jednostki. Jak razem są unikatowe identyfikatory hello jednostki, tworzą one hello klucza podstawowego jednostki. Można badać przy użyciu następujących wartości szybciej, niż można zapytania innych właściwości jednostki, ponieważ tylko te właściwości są indeksowane.

Witaj używa usługi tabeli **PartitionKey** toointelligently rozpowszechniają jednostek tabeli węzłów magazynu. Tekst hello obiektów, które mają takie same **PartitionKey** są przechowywane na powitania tym samym węźle. **RowKey** jest unikatowy identyfikator hello hello jednostek w partycji hello należy.

## <a name="update-an-entity"></a>Aktualizuj jednostkę

tooupdate wszystkich wartości właściwości jednostki, wywołaj hello [update_entity] [ py_update_entity] metody. W tym przykładzie pokazano sposób tooreplace istniejącej jednostki zaktualizowaną wersją:

```python
task = {'PartitionKey': 'tasksSeattle', 'RowKey': '001', 'description' : 'Take out hello garbage', 'priority' : 250}
table_service.update_entity('tasktable', task)
```

Jeśli hello jednostki, która jest aktualizowana już nie istnieje, nie będą hello operacji aktualizacji. Toostore jednostki czy istnieje lub nie, należy użyć [insert_or_replace_entity][py_insert_or_replace_entity]. W hello poniższy przykład pierwsze wywołanie hello spowoduje zastąpienie istniejącej jednostki hello. drugie wywołanie Hello powoduje wstawienie nowego obiektu, ponieważ nie jednostki o hello określone PartitionKey i RowKey istnieje w tabeli hello.

```python
# Replace hello entity created earlier
task = {'PartitionKey': 'tasksSeattle', 'RowKey': '001', 'description' : 'Take out hello garbage again', 'priority' : 250}
table_service.insert_or_replace_entity('tasktable', task)

# Insert a new entity
task = {'PartitionKey': 'tasksSeattle', 'RowKey': '003', 'description' : 'Buy detergent', 'priority' : 300}
table_service.insert_or_replace_entity('tasktable', task)
```

> [!TIP]
> Witaj [update_entity] [ py_update_entity] metoda zastępuje wszystkie właściwości i wartości istniejącej jednostki, które można również użyć właściwości tooremove z istniejącej jednostki. Można użyć hello [merge_entity] [ py_merge_entity] tooupdate metody istniejącej jednostki z wartościami właściwości nowe lub zmodyfikowane bez całkowicie zastępowania hello jednostki.

## <a name="modify-multiple-entities"></a>Modyfikowanie wiele jednostek

tooensure hello atomic przetwarzania żądania przez usługę tabeli hello, mogą przesyłać wiele operacji ze sobą w partii. Najpierw użyj hello [TableBatch] [ py_TableBatch] klasy tooadd wiele operacji tooa pojedyncza partia. Następnie wywołaj [TableService][py_TableService].[ commit_batch] [ py_commit_batch] toosubmit hello operacje w niepodzielną operację. Wszystkie toobe jednostek zmodyfikowane w partii musi należeć do hello tej samej partycji.

W tym przykładzie dodaje dwie jednostki w partii:

```python
from azure.storage.table import TableBatch
batch = TableBatch()
task004 = {'PartitionKey': 'tasksSeattle', 'RowKey': '004', 'description' : 'Go grocery shopping', 'priority' : 400}
task005 = {'PartitionKey': 'tasksSeattle', 'RowKey': '005', 'description' : 'Clean hello bathroom', 'priority' : 100}
batch.insert_entity(task004)
batch.insert_entity(task005)
table_service.commit_batch('tasktable', batch)
```

Partie można również ze składnią Menedżera kontekstu hello:

```python
task006 = {'PartitionKey': 'tasksSeattle', 'RowKey': '006', 'description' : 'Go grocery shopping', 'priority' : 400}
task007 = {'PartitionKey': 'tasksSeattle', 'RowKey': '007', 'description' : 'Clean hello bathroom', 'priority' : 100}

with table_service.batch('tasktable') as batch:
    batch.insert_entity(task006)
    batch.insert_entity(task007)
```

## <a name="query-for-an-entity"></a>Zapytanie dla jednostki

tooquery dla jednostki w tabeli, Przekaż jego toohello PartitionKey i RowKey [TableService][py_TableService].[ get_entity] [ py_get_entity] metody.

```python
task = table_service.get_entity('tasktable', 'tasksSeattle', '001')
print(task.description)
print(task.priority)
```

## <a name="query-a-set-of-entities"></a>Zapytanie zestawu jednostek

Można zapytania dla zestawu jednostek, podając ciąg filtru z hello **filtru** parametru. W tym przykładzie znajduje wszystkie zadania w Seattle, stosując filtr na PartitionKey:

```python
tasks = table_service.query_entities('tasktable', filter="PartitionKey eq 'tasksSeattle'")
for task in tasks:
    print(task.description)
    print(task.priority)
```

## <a name="query-a-subset-of-entity-properties"></a>Tworzenie zapytania do podzbioru właściwości jednostki

Można również ograniczyć, właściwości, które są zwracane dla każdej jednostki w zapytaniu. Ta technika, zwana *projekcji*, redukuje przepustowość i może poprawiać wydajność zapytań, zwłaszcza w przypadku dużych jednostek lub zestawów wyników. Użyj hello **wybierz** parametru i przekazać hello nazwy właściwości hello mają zwrócił toohello klienta.

Zapytanie Hello w hello następującego kodu zwraca tylko hello opisy jednostek w tabeli hello.

> [!NOTE]
> powitania po fragment działa tylko wobec hello Azure Storage. Nie jest obsługiwana przez emulator magazynu hello.

```python
tasks = table_service.query_entities('tasktable', filter="PartitionKey eq 'tasksSeattle'", select='description')
for task in tasks:
    print(task.description)
```

## <a name="delete-an-entity"></a>Usuwanie jednostki

Usuwanie jednostki przez przekazanie jej toohello PartitionKey i RowKey [delete_entity] [ py_delete_entity] metody.

```python
table_service.delete_entity('tasktable', 'tasksSeattle', '001')
```

## <a name="delete-a-table"></a>Usuwanie tabeli

Jeśli nie są już potrzebne tabeli ani żadnych jednostek hello w niej wywołanie hello [delete_table] [ py_delete_table] toopermanently metody Usuń tabelę hello z usługi Magazyn Azure.

```python
table_service.delete_table('tasktable')
```

## <a name="next-steps"></a>Następne kroki

* [Azure Storage SDK for Python API reference](https://azure-storage.readthedocs.io/en/latest/index.html)
* [Magazyn Azure SDK dla języka Python](https://github.com/Azure/azure-storage-python)
* [Centrum deweloperów języka Python](https://azure.microsoft.com/develop/python/)
* [Eksplorator magazynu Microsoft Azure](../vs-azure-tools-storage-manage-with-storage-explorer.md): wolne, i platform aplikacji do pracy wizualnie z danymi usługi Azure Storage w systemie Windows, macOS i Linux.

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
