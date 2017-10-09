---
title: "powiązania tabeli magazynu funkcji aaaAzure | Dokumentacja firmy Microsoft"
description: "Zrozumienie sposobu toouse powiązań usługi Azure Storage w funkcji platformy Azure."
services: functions
documentationcenter: na
author: christopheranderson
manager: erikre
editor: 
tags: 
keywords: "funkcje usługi Azure, funkcje, przetwarzania zdarzeń, dynamiczne obliczeń niekorzystającą architektury"
ms.assetid: 65b3437e-2571-4d3f-a996-61a74b50a1c2
ms.service: functions
ms.devlang: multiple
ms.topic: reference
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 10/28/2016
ms.author: chrande
ms.openlocfilehash: 90c2a73329139d4ab3504bc0e2c90370133158bf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-functions-storage-table-bindings"></a>Azure powiązania tabeli w funkcji magazynu
[!INCLUDE [functions-selector-bindings](../../includes/functions-selector-bindings.md)]

W tym artykule opisano, jak tabela powiązania usługi Azure Functions tooconfigure i kodu usługi Azure Storage. Azure Functions obsługuje wejściowa i wyjściowa powiązań dla tabel usługi Azure Storage.

Powiązanie tabeli magazynu Hello obsługuje hello następujące scenariusze:

* **Przeczytaj pojedynczy wiersz w funkcji języka C# lub Node.js** — skonfiguruj `partitionKey` i `rowKey`. Witaj `filter` i `take` właściwości nie są używane w tym scenariuszu.
* **Odczytuje wiele wierszy w funkcji języka C#** -udostępnia środowisko uruchomieniowe Functions hello `IQueryable<T>` obiekt powiązany toohello tabeli. Typ `T` musi pochodzić od `TableEntity` , lub zaimplementuj `ITableEntity`. Witaj `partitionKey`, `rowKey`, `filter`, i `take` właściwości nie są używane w tym scenariuszu; można użyć hello `IQueryable` obiekt toodo żadnego filtrowania wymagane. 
* **Odczytuje wiele wierszy w funkcji węzła** — skonfiguruj hello `filter` i `take` właściwości. Nie należy ustawiać `partitionKey` lub `rowKey`.
* **Wpisz jeden lub więcej wierszy w funkcji języka C#** — udostępnia środowisko uruchomieniowe Functions hello `ICollector<T>` lub `IAsyncCollector<T>` toohello powiązanej tabeli, gdzie `T` Określa schemat hello jednostek hello ma tooadd. Zwykle, wpisz `T` pochodzi z `TableEntity` lub implementuje `ITableEntity`, ale nie ma. Witaj `partitionKey`, `rowKey`, `filter`, i `take` właściwości nie są używane w tym scenariuszu.

[!INCLUDE [intro](../../includes/functions-bindings-intro.md)]

<a name="input"></a>

## <a name="storage-table-input-binding"></a>Powiązania wejściowego tabeli magazynu
Witaj powiązania wejściowego tabeli magazynu Azure umożliwia toouse tabeli w funkcji magazynu. 

Hello funkcji tooa wejściowej tabeli magazynu używa hello następujące obiekty JSON w hello `bindings` tablicy function.json:

```json
{
    "name": "<Name of input parameter in function signature>",
    "type": "table",
    "direction": "in",
    "tableName": "<Name of Storage table>",
    "partitionKey": "<PartitionKey of table entity tooread - see below>",
    "rowKey": "<RowKey of table entity tooread - see below>",
    "take": "<Maximum number of entities tooread in Node.js - optional>",
    "filter": "<OData filter expression for table input in Node.js - optional>",
    "connection": "<Name of app setting - see below>",
}
```

Należy uwzględnić następujące hello: 

* Użyj `partitionKey` i `rowKey` razem tooread pojedynczej jednostki. Te właściwości są opcjonalne. 
* `connection`musi zawierać nazwę hello ustawienia aplikacji, która zawiera parametry połączenia magazynu. W portalu Azure hello, hello standardowego edytora w hello **integracji** kartę konfiguruje to ustawienie aplikacji do tworzenia magazynu konta lub wybiera istniejący. Możesz również [konfigurowania tej aplikacji ręcznie ustawienie](functions-how-to-use-azure-function-app-settings.md#settings).  

<a name="inputusage"></a>

## <a name="input-usage"></a>Użycie wejściowych
W języku C# funkcji, możesz powiązać toohello wejściowej tabeli (lub jednostek) przy użyciu nazwanego parametru w podpisu funkcji tak samo, jak `<T> <name>`.
Gdzie `T` jest typ danych hello, które mają toodeserialize hello dane, i `paramName` jest nazwą hello określone w hello [wejściowych powiązania](#input). W przypadku funkcji Node.js dostępu hello wejściowej tabeli (lub jednostek) przy użyciu `context.bindings.<name>`.

dane wejściowe Hello może być zdeserializowany w funkcjach Node.js lub C#. obiekty Hello rozszeregować mają `RowKey` i `PartitionKey` właściwości.

W języku C# funkcje może także powiązać tooany hello następujące typy i funkcje hello środowiska uruchomieniowego podejmie próbę deserializacji zbyt hello tabeli danych przy użyciu tego typu:

* Dowolnego typu, który implementuje`ITableEntity`
* `IQueryable<T>`

<a name="inputsample"></a>

## <a name="input-sample"></a>Przykładowe wejściowych
Powinien mieć powitania po function.json, używający kolejki wyzwalacza tooread wiersza pojedynczej tabeli. Witaj JSON Określa `PartitionKey`  
 `RowKey`. `"rowKey": "{queueTrigger}"`Wskazuje, że ten klucz wiersza hello pochodzi z hello kolejki wiadomości ciąg.

```json
{
  "bindings": [
    {
      "queueName": "myqueue-items",
      "connection": "MyStorageConnection",
      "name": "myQueueItem",
      "type": "queueTrigger",
      "direction": "in"
    },
    {
      "name": "personEntity",
      "type": "table",
      "tableName": "Person",
      "partitionKey": "Test",
      "rowKey": "{queueTrigger}",
      "connection": "MyStorageConnection",
      "direction": "in"
    }
  ],
  "disabled": false
}
```

Zobacz hello próbka specyficzny dla języka, która odczytuje jednostki pojedynczej tabeli.

* [C#](#inputcsharp)
* [F#](#inputfsharp)
* [Node.js](#inputnodejs)

<a name="inputcsharp"></a>

### <a name="input-sample-in-c"></a>Przykładowe wejściowego w języku C# #
```csharp
public static void Run(string myQueueItem, Person personEntity, TraceWriter log)
{
    log.Info($"C# Queue trigger function processed: {myQueueItem}");
    log.Info($"Name in Person entity: {personEntity.Name}");
}

public class Person
{
    public string PartitionKey { get; set; }
    public string RowKey { get; set; }
    public string Name { get; set; }
}
```

<a name="inputfsharp"></a>

### <a name="input-sample-in-f"></a>Przykładowe wejściowego w języku F # #
```fsharp
[<CLIMutable>]
type Person = {
  PartitionKey: string
  RowKey: string
  Name: string
}

let Run(myQueueItem: string, personEntity: Person) =
    log.Info(sprintf "F# Queue trigger function processed: %s" myQueueItem)
    log.Info(sprintf "Name in Person entity: %s" personEntity.Name)
```

<a name="inputnodejs"></a>

### <a name="input-sample-in-nodejs"></a>Przykładowe wejściowego w środowisku Node.js
```javascript
module.exports = function (context, myQueueItem) {
    context.log('Node.js queue trigger function processed work item', myQueueItem);
    context.log('Person entity name: ' + context.bindings.personEntity.Name);
    context.done();
};
```

<a name="output"></a>

## <a name="storage-table-output-binding"></a>Tabela magazynu powiązania wyjściowego
Powiązanie umożliwia toowrite jednostek tooa magazynu tabeli w funkcji wyjściowe Hello tabeli magazynu Azure. 

Witaj magazynu w tabeli danych wyjściowych dla funkcji używa hello następujące obiekty JSON w hello `bindings` tablicy function.json:

```json
{
    "name": "<Name of input parameter in function signature>",
    "type": "table",
    "direction": "out",
    "tableName": "<Name of Storage table>",
    "partitionKey": "<PartitionKey of table entity toowrite - see below>",
    "rowKey": "<RowKey of table entity toowrite - see below>",
    "connection": "<Name of app setting - see below>",
}
```

Należy uwzględnić następujące hello: 

* Użyj `partitionKey` i `rowKey` razem toowrite pojedynczej jednostki. Te właściwości są opcjonalne. Można również określić `PartitionKey` i `RowKey` podczas tworzenia hello obiektów jednostek w kodzie funkcji.
* `connection`musi zawierać nazwę hello ustawienia aplikacji, która zawiera parametry połączenia magazynu. W portalu Azure hello, hello standardowego edytora w hello **integracji** kartę konfiguruje to ustawienie aplikacji do tworzenia magazynu konta lub wybiera istniejący. Możesz również [konfigurowania tej aplikacji ręcznie ustawienie](functions-how-to-use-azure-function-app-settings.md#settings). 

<a name="outputusage"></a>

## <a name="output-usage"></a>Użycie danych wyjściowych
W języku C# funkcji, powiązania toohello w tabeli danych wyjściowych za pomocą hello o nazwie `out` parametru w podpisu funkcji, takich jak `out <T> <name>`, gdzie `T` jest typ danych hello, które mają tooserialize hello dane, i `paramName` jest hello wybraną nazwę określony w hello [powiązania wyjściowego](#output). W przypadku funkcji Node.js dostępu tabeli hello wyjściowe `context.bindings.<name>`.

Może serializować obiektów w funkcjach Node.js lub C#. W języku C# funkcji można także powiązać toohello następujące typy:

* Dowolnego typu, który implementuje`ITableEntity`
* `ICollector<T>`(toooutput wiele jednostek. Zobacz [próbki](#outcsharp).)
* `IAsyncCollector<T>`(wersja async `ICollector<T>`)
* `CloudTable`(przy użyciu hello zestawu SDK usługi Magazyn Azure. Zobacz [próbki](#readmulti).)

<a name="outputsample"></a>

## <a name="output-sample"></a>Przykładowe dane wyjściowe
następujące Hello *function.json* i *run.csx* przykładzie pokazano sposób toowrite wiele jednostek tabeli.

```json
{
  "bindings": [
    {
      "name": "input",
      "type": "manualTrigger",
      "direction": "in"
    },
    {
      "tableName": "Person",
      "connection": "MyStorageConnection",
      "name": "tableBinding",
      "type": "table",
      "direction": "out"
    }
  ],
  "disabled": false
}
```

Zobacz hello przykład specyficzny dla języka, który tworzy wiele jednostek tabeli.

* [C#](#outcsharp)
* [F#](#outfsharp)
* [Node.js](#outnodejs)

<a name="outcsharp"></a>

### <a name="output-sample-in-c"></a>Przykładowe dane wyjściowe w języku C# #
```csharp
public static void Run(string input, ICollector<Person> tableBinding, TraceWriter log)
{
    for (int i = 1; i < 10; i++)
        {
            log.Info($"Adding Person entity {i}");
            tableBinding.Add(
                new Person() { 
                    PartitionKey = "Test", 
                    RowKey = i.ToString(), 
                    Name = "Name" + i.ToString() }
                );
        }

}

public class Person
{
    public string PartitionKey { get; set; }
    public string RowKey { get; set; }
    public string Name { get; set; }
}

```
<a name="outfsharp"></a>

### <a name="output-sample-in-f"></a>Przykładowe dane wyjściowe w języku F # #
```fsharp
[<CLIMutable>]
type Person = {
  PartitionKey: string
  RowKey: string
  Name: string
}

let Run(input: string, tableBinding: ICollector<Person>, log: TraceWriter) =
    for i = 1 too10 do
        log.Info(sprintf "Adding Person entity %d" i)
        tableBinding.Add(
            { PartitionKey = "Test"
              RowKey = i.ToString()
              Name = "Name" + i.ToString() })
```

<a name="outnodejs"></a>

### <a name="output-sample-in-nodejs"></a>Przykładowe dane wyjściowe w środowisku Node.js
```javascript
module.exports = function (context) {

    context.bindings.tableBinding = [];

    for (var i = 1; i < 10; i++) {
        context.bindings.tableBinding.push({
            PartitionKey: "Test",
            RowKey: i.toString(),
            Name: "Name " + i
        });
    }
    
    context.done();
};
```

<a name="readmulti"></a>

## <a name="sample-read-multiple-table-entities-in-c"></a>Przykład: Odczytu wiele jednostek tabeli w języku C#  #
następujące Hello *function.json* i jednostek dla klucza partycji, który jest określony w komunikacie kolejki hello odczytuje przykładowego kodu w języku C#.

```json
{
  "bindings": [
    {
      "queueName": "myqueue-items",
      "connection": "MyStorageConnection",
      "name": "myQueueItem",
      "type": "queueTrigger",
      "direction": "in"
    },
    {
      "name": "tableBinding",
      "type": "table",
      "connection": "MyStorageConnection",
      "tableName": "Person",
      "direction": "in"
    }
  ],
  "disabled": false
}
```

Hello kod w języku C# dodaje toohello odwołanie do zestawu SDK usługi Magazyn Azure, aby typ jednostki hello może pochodzić od `TableEntity`.

```csharp
#r "Microsoft.WindowsAzure.Storage"
using Microsoft.WindowsAzure.Storage.Table;

public static void Run(string myQueueItem, IQueryable<Person> tableBinding, TraceWriter log)
{
    log.Info($"C# Queue trigger function processed: {myQueueItem}");
    foreach (Person person in tableBinding.Where(p => p.PartitionKey == myQueueItem).ToList())
    {
        log.Info($"Name: {person.Name}");
    }
}

public class Person : TableEntity
{
    public string Name { get; set; }
}
```

## <a name="next-steps"></a>Następne kroki
[!INCLUDE [next steps](../../includes/functions-bindings-next-steps.md)]

