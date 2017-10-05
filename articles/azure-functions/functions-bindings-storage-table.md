---
title: "Powiązania tabeli magazynu funkcji platformy Azure | Dokumentacja firmy Microsoft"
description: "Zrozumienie, jak używać usługi Azure Storage powiązania w usługi Azure Functions."
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
ms.openlocfilehash: bb01be3ee044f60376e0c9c2de7b3dd34f3b7aca
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="azure-functions-storage-table-bindings"></a><span data-ttu-id="33aea-104">Azure powiązania tabeli w funkcji magazynu</span><span class="sxs-lookup"><span data-stu-id="33aea-104">Azure Functions Storage table bindings</span></span>
[!INCLUDE [functions-selector-bindings](../../includes/functions-selector-bindings.md)]

<span data-ttu-id="33aea-105">W tym artykule opisano sposób konfigurowania i powiązania tabeli usługi Azure Storage kodu w usługi Azure Functions.</span><span class="sxs-lookup"><span data-stu-id="33aea-105">This article explains how to configure and code Azure Storage table bindings in Azure Functions.</span></span> <span data-ttu-id="33aea-106">Azure Functions obsługuje wejściowa i wyjściowa powiązań dla tabel usługi Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="33aea-106">Azure Functions supports input and output bindings for Azure Storage tables.</span></span>

<span data-ttu-id="33aea-107">Powiązanie tabeli magazynu obsługuje następujące scenariusze:</span><span class="sxs-lookup"><span data-stu-id="33aea-107">The Storage table binding supports the following scenarios:</span></span>

* <span data-ttu-id="33aea-108">**Przeczytaj pojedynczy wiersz w funkcji języka C# lub Node.js** — skonfiguruj `partitionKey` i `rowKey`.</span><span class="sxs-lookup"><span data-stu-id="33aea-108">**Read a single row in a C# or Node.js function** - Set `partitionKey` and `rowKey`.</span></span> <span data-ttu-id="33aea-109">`filter` i `take` właściwości nie są używane w tym scenariuszu.</span><span class="sxs-lookup"><span data-stu-id="33aea-109">The `filter` and `take` properties are not used in this scenario.</span></span>
* <span data-ttu-id="33aea-110">**Odczytuje wiele wierszy w funkcji języka C#** — środowisko uruchomieniowe Functions zapewnia `IQueryable<T>` obiekt powiązany z tabelą.</span><span class="sxs-lookup"><span data-stu-id="33aea-110">**Read multiple rows in a C# function** - The Functions runtime provides an `IQueryable<T>` object bound to the table.</span></span> <span data-ttu-id="33aea-111">Typ `T` musi pochodzić od `TableEntity` , lub zaimplementuj `ITableEntity`.</span><span class="sxs-lookup"><span data-stu-id="33aea-111">Type `T` must derive from `TableEntity` or implement `ITableEntity`.</span></span> <span data-ttu-id="33aea-112">`partitionKey`, `rowKey`, `filter`, I `take` właściwości nie są używane w tym scenariuszu; można użyć `IQueryable` obiekt do dowolnego filtrowanie wymagane.</span><span class="sxs-lookup"><span data-stu-id="33aea-112">The `partitionKey`, `rowKey`, `filter`, and `take` properties are not used in this scenario; you can use the `IQueryable` object to do any filtering required.</span></span> 
* <span data-ttu-id="33aea-113">**Odczytuje wiele wierszy w funkcji węzła** — skonfiguruj `filter` i `take` właściwości.</span><span class="sxs-lookup"><span data-stu-id="33aea-113">**Read multiple rows in a Node function** - Set the `filter` and `take` properties.</span></span> <span data-ttu-id="33aea-114">Nie należy ustawiać `partitionKey` lub `rowKey`.</span><span class="sxs-lookup"><span data-stu-id="33aea-114">Don't set `partitionKey` or `rowKey`.</span></span>
* <span data-ttu-id="33aea-115">**Zapis co najmniej jeden wiersz w funkcji języka C#** — środowisko uruchomieniowe Functions zapewnia `ICollector<T>` lub `IAsyncCollector<T>` powiązany z tabelą, gdzie `T` Określa schemat jednostek, które chcesz dodać.</span><span class="sxs-lookup"><span data-stu-id="33aea-115">**Write one or more rows in a C# function** - The Functions runtime provides an `ICollector<T>` or `IAsyncCollector<T>` bound to the table, where `T` specifies the schema of the entities you want to add.</span></span> <span data-ttu-id="33aea-116">Zwykle, wpisz `T` pochodzi z `TableEntity` lub implementuje `ITableEntity`, ale nie ma.</span><span class="sxs-lookup"><span data-stu-id="33aea-116">Typically, type `T` derives from `TableEntity` or implements `ITableEntity`, but it doesn't have to.</span></span> <span data-ttu-id="33aea-117">`partitionKey`, `rowKey`, `filter`, I `take` właściwości nie są używane w tym scenariuszu.</span><span class="sxs-lookup"><span data-stu-id="33aea-117">The `partitionKey`, `rowKey`, `filter`, and `take` properties are not used in this scenario.</span></span>

[!INCLUDE [intro](../../includes/functions-bindings-intro.md)]

<a name="input"></a>

## <a name="storage-table-input-binding"></a><span data-ttu-id="33aea-118">Powiązania wejściowego tabeli magazynu</span><span class="sxs-lookup"><span data-stu-id="33aea-118">Storage table input binding</span></span>
<span data-ttu-id="33aea-119">Powiązania wejściowego tabeli magazynu Azure umożliwia korzystanie z tabeli magazynu w funkcji.</span><span class="sxs-lookup"><span data-stu-id="33aea-119">The Azure Storage table input binding enables you to use a storage table in your function.</span></span> 

<span data-ttu-id="33aea-120">Dane wejściowe funkcji tabeli magazynu używa następujących obiektów JSON w `bindings` tablicy function.json:</span><span class="sxs-lookup"><span data-stu-id="33aea-120">The Storage table input to a function uses the following JSON objects in the `bindings` array of function.json:</span></span>

```json
{
    "name": "<Name of input parameter in function signature>",
    "type": "table",
    "direction": "in",
    "tableName": "<Name of Storage table>",
    "partitionKey": "<PartitionKey of table entity to read - see below>",
    "rowKey": "<RowKey of table entity to read - see below>",
    "take": "<Maximum number of entities to read in Node.js - optional>",
    "filter": "<OData filter expression for table input in Node.js - optional>",
    "connection": "<Name of app setting - see below>",
}
```

<span data-ttu-id="33aea-121">Pamiętaj o następujących kwestiach:</span><span class="sxs-lookup"><span data-stu-id="33aea-121">Note the following:</span></span> 

* <span data-ttu-id="33aea-122">Użyj `partitionKey` i `rowKey` ze sobą w celu odczytu pojedynczej jednostki.</span><span class="sxs-lookup"><span data-stu-id="33aea-122">Use `partitionKey` and `rowKey` together to read a single entity.</span></span> <span data-ttu-id="33aea-123">Te właściwości są opcjonalne.</span><span class="sxs-lookup"><span data-stu-id="33aea-123">These properties are optional.</span></span> 
* <span data-ttu-id="33aea-124">`connection`musi zawierać nazwę ustawienia aplikacji, która zawiera parametry połączenia magazynu.</span><span class="sxs-lookup"><span data-stu-id="33aea-124">`connection` must contain the name of an app setting that contains a storage connection string.</span></span> <span data-ttu-id="33aea-125">W portalu Azure, standardowego edytora w **integracji** kartę konfiguruje to ustawienie aplikacji do tworzenia magazynu konta lub wybiera istniejący.</span><span class="sxs-lookup"><span data-stu-id="33aea-125">In the Azure portal, the standard editor in the **Integrate** tab configures this app setting for you when you create a Storage account or selects an existing one.</span></span> <span data-ttu-id="33aea-126">Możesz również [konfigurowania tej aplikacji ręcznie ustawienie](functions-how-to-use-azure-function-app-settings.md#settings).</span><span class="sxs-lookup"><span data-stu-id="33aea-126">You can also [configure this app setting manually](functions-how-to-use-azure-function-app-settings.md#settings).</span></span>  

<a name="inputusage"></a>

## <a name="input-usage"></a><span data-ttu-id="33aea-127">Użycie wejściowych</span><span class="sxs-lookup"><span data-stu-id="33aea-127">Input usage</span></span>
<span data-ttu-id="33aea-128">W języku C# funkcji, można powiązać tabeli wejściowej (lub jednostek) przy użyciu nazwanego parametru w podpisu funkcji tak samo, jak `<T> <name>`.</span><span class="sxs-lookup"><span data-stu-id="33aea-128">In C# functions, you bind to the input table entity (or entities) by using a named parameter in your function signature, like `<T> <name>`.</span></span>
<span data-ttu-id="33aea-129">Gdzie `T` jest typ danych chcesz danych do deserializacji i `paramName` jest nazwa określona w [wejściowych powiązania](#input).</span><span class="sxs-lookup"><span data-stu-id="33aea-129">Where `T` is the data type that you want to deserialize the data into, and `paramName` is the name you specified in the [input binding](#input).</span></span> <span data-ttu-id="33aea-130">W przypadku funkcji Node.js dostępu tabeli wejściowej (lub jednostek) przy użyciu `context.bindings.<name>`.</span><span class="sxs-lookup"><span data-stu-id="33aea-130">In Node.js functions, you access the input table entity (or entities) using `context.bindings.<name>`.</span></span>

<span data-ttu-id="33aea-131">Może być zdeserializowany danych wejściowych w funkcjach Node.js lub C#.</span><span class="sxs-lookup"><span data-stu-id="33aea-131">The input data can be deserialized in Node.js or C# functions.</span></span> <span data-ttu-id="33aea-132">Zdeserializowana obiekty mają `RowKey` i `PartitionKey` właściwości.</span><span class="sxs-lookup"><span data-stu-id="33aea-132">The deserialized objects have `RowKey` and `PartitionKey` properties.</span></span>

<span data-ttu-id="33aea-133">W języku C# funkcji można również wiązać z dowolnej z następujących typów, a środowisko uruchomieniowe Functions podejmie próbę deserializacji danych tabeli za pomocą tego typu:</span><span class="sxs-lookup"><span data-stu-id="33aea-133">In C# functions, you can also bind to any of the following types, and the Functions runtime will attempt to deserialize the table data using that type:</span></span>

* <span data-ttu-id="33aea-134">Dowolnego typu, który implementuje`ITableEntity`</span><span class="sxs-lookup"><span data-stu-id="33aea-134">Any type that implements `ITableEntity`</span></span>
* `IQueryable<T>`

<a name="inputsample"></a>

## <a name="input-sample"></a><span data-ttu-id="33aea-135">Przykładowe wejściowych</span><span class="sxs-lookup"><span data-stu-id="33aea-135">Input sample</span></span>
<span data-ttu-id="33aea-136">Powinien mieć następujące function.json, używający wyzwalacz kolejki można odczytać wiersza pojedynczej tabeli.</span><span class="sxs-lookup"><span data-stu-id="33aea-136">Supposed you have the following function.json, which uses a queue trigger to read a single table row.</span></span> <span data-ttu-id="33aea-137">Określa JSON `PartitionKey`  
 `RowKey`.</span><span class="sxs-lookup"><span data-stu-id="33aea-137">The JSON specifies `PartitionKey` 
`RowKey`.</span></span> <span data-ttu-id="33aea-138">`"rowKey": "{queueTrigger}"`Wskazuje, czy klucz wiersza pochodzą z ciągu kolejki wiadomości.</span><span class="sxs-lookup"><span data-stu-id="33aea-138">`"rowKey": "{queueTrigger}"` indicates that the row key comes from the queue message string.</span></span>

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

<span data-ttu-id="33aea-139">Zobacz próbka specyficzny dla języka, która odczytuje jednostki pojedynczej tabeli.</span><span class="sxs-lookup"><span data-stu-id="33aea-139">See the language-specific sample that reads a single table entity.</span></span>

* [<span data-ttu-id="33aea-140">C#</span><span class="sxs-lookup"><span data-stu-id="33aea-140">C#</span></span>](#inputcsharp)
* [<span data-ttu-id="33aea-141">F#</span><span class="sxs-lookup"><span data-stu-id="33aea-141">F#</span></span>](#inputfsharp)
* [<span data-ttu-id="33aea-142">Node.js</span><span class="sxs-lookup"><span data-stu-id="33aea-142">Node.js</span></span>](#inputnodejs)

<a name="inputcsharp"></a>

### <a name="input-sample-in-c"></a><span data-ttu-id="33aea-143">Przykładowe wejściowego w języku C#</span><span class="sxs-lookup"><span data-stu-id="33aea-143">Input sample in C#</span></span> #
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

### <a name="input-sample-in-f"></a><span data-ttu-id="33aea-144">Przykładowe wejściowego w języku F #</span><span class="sxs-lookup"><span data-stu-id="33aea-144">Input sample in F#</span></span> #
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

### <a name="input-sample-in-nodejs"></a><span data-ttu-id="33aea-145">Przykładowe wejściowego w środowisku Node.js</span><span class="sxs-lookup"><span data-stu-id="33aea-145">Input sample in Node.js</span></span>
```javascript
module.exports = function (context, myQueueItem) {
    context.log('Node.js queue trigger function processed work item', myQueueItem);
    context.log('Person entity name: ' + context.bindings.personEntity.Name);
    context.done();
};
```

<a name="output"></a>

## <a name="storage-table-output-binding"></a><span data-ttu-id="33aea-146">Tabela magazynu powiązania wyjściowego</span><span class="sxs-lookup"><span data-stu-id="33aea-146">Storage table output binding</span></span>
<span data-ttu-id="33aea-147">Dane wyjściowe tabeli magazynu Azure umożliwia powiązanie, możesz zapisać jednostek magazynu tabeli w funkcji.</span><span class="sxs-lookup"><span data-stu-id="33aea-147">The Azure Storage table output binding enables you to write entities to a Storage table in your function.</span></span> 

<span data-ttu-id="33aea-148">Tabela magazynu danych wyjściowych dla funkcji używa następujących obiektów JSON w `bindings` tablicy function.json:</span><span class="sxs-lookup"><span data-stu-id="33aea-148">The Storage table output for a function uses the following JSON objects in the `bindings` array of function.json:</span></span>

```json
{
    "name": "<Name of input parameter in function signature>",
    "type": "table",
    "direction": "out",
    "tableName": "<Name of Storage table>",
    "partitionKey": "<PartitionKey of table entity to write - see below>",
    "rowKey": "<RowKey of table entity to write - see below>",
    "connection": "<Name of app setting - see below>",
}
```

<span data-ttu-id="33aea-149">Pamiętaj o następujących kwestiach:</span><span class="sxs-lookup"><span data-stu-id="33aea-149">Note the following:</span></span> 

* <span data-ttu-id="33aea-150">Użyj `partitionKey` i `rowKey` ze sobą w celu zapisania pojedynczej jednostki.</span><span class="sxs-lookup"><span data-stu-id="33aea-150">Use `partitionKey` and `rowKey` together to write a single entity.</span></span> <span data-ttu-id="33aea-151">Te właściwości są opcjonalne.</span><span class="sxs-lookup"><span data-stu-id="33aea-151">These properties are optional.</span></span> <span data-ttu-id="33aea-152">Można również określić `PartitionKey` i `RowKey` podczas tworzenia obiektów jednostek w kodzie funkcji.</span><span class="sxs-lookup"><span data-stu-id="33aea-152">You can also specify `PartitionKey` and `RowKey` when you create the entity objects in your function code.</span></span>
* <span data-ttu-id="33aea-153">`connection`musi zawierać nazwę ustawienia aplikacji, która zawiera parametry połączenia magazynu.</span><span class="sxs-lookup"><span data-stu-id="33aea-153">`connection` must contain the name of an app setting that contains a storage connection string.</span></span> <span data-ttu-id="33aea-154">W portalu Azure, standardowego edytora w **integracji** kartę konfiguruje to ustawienie aplikacji do tworzenia magazynu konta lub wybiera istniejący.</span><span class="sxs-lookup"><span data-stu-id="33aea-154">In the Azure portal, the standard editor in the **Integrate** tab configures this app setting for you when you create a Storage account or selects an existing one.</span></span> <span data-ttu-id="33aea-155">Możesz również [konfigurowania tej aplikacji ręcznie ustawienie](functions-how-to-use-azure-function-app-settings.md#settings).</span><span class="sxs-lookup"><span data-stu-id="33aea-155">You can also [configure this app setting manually](functions-how-to-use-azure-function-app-settings.md#settings).</span></span> 

<a name="outputusage"></a>

## <a name="output-usage"></a><span data-ttu-id="33aea-156">Użycie danych wyjściowych</span><span class="sxs-lookup"><span data-stu-id="33aea-156">Output usage</span></span>
<span data-ttu-id="33aea-157">W języku C# funkcji, należy powiązać z tabeli danych wyjściowych przy użyciu nazwanego `out` parametru w podpisu funkcji, takich jak `out <T> <name>`, gdzie `T` jest mają do serializowania danych do typów danych i `paramName` jest nazwa określona w [powiązania wyjściowego](#output).</span><span class="sxs-lookup"><span data-stu-id="33aea-157">In C# functions, you bind to the table output by using the named `out` parameter in your function signature, like `out <T> <name>`, where `T` is the data type that you want to serialize the data into, and `paramName` is the name you specified in the [output binding](#output).</span></span> <span data-ttu-id="33aea-158">W przypadku funkcji Node.js dostępu tabeli wyjściowe `context.bindings.<name>`.</span><span class="sxs-lookup"><span data-stu-id="33aea-158">In Node.js functions, you access the table output using `context.bindings.<name>`.</span></span>

<span data-ttu-id="33aea-159">Może serializować obiektów w funkcjach Node.js lub C#.</span><span class="sxs-lookup"><span data-stu-id="33aea-159">You can serialize objects in Node.js or C# functions.</span></span> <span data-ttu-id="33aea-160">W języku C# funkcji można powiązać następujących typów:</span><span class="sxs-lookup"><span data-stu-id="33aea-160">In C# functions, you can also bind to the following types:</span></span>

* <span data-ttu-id="33aea-161">Dowolnego typu, który implementuje`ITableEntity`</span><span class="sxs-lookup"><span data-stu-id="33aea-161">Any type that implements `ITableEntity`</span></span>
* <span data-ttu-id="33aea-162">`ICollector<T>`(do wyjściowego wiele jednostek.</span><span class="sxs-lookup"><span data-stu-id="33aea-162">`ICollector<T>` (to output multiple entities.</span></span> <span data-ttu-id="33aea-163">Zobacz [próbki](#outcsharp).)</span><span class="sxs-lookup"><span data-stu-id="33aea-163">See [sample](#outcsharp).)</span></span>
* <span data-ttu-id="33aea-164">`IAsyncCollector<T>`(wersja async `ICollector<T>`)</span><span class="sxs-lookup"><span data-stu-id="33aea-164">`IAsyncCollector<T>` (async version of `ICollector<T>`)</span></span>
* <span data-ttu-id="33aea-165">`CloudTable`(przy użyciu zestawu SDK usługi Magazyn Azure.</span><span class="sxs-lookup"><span data-stu-id="33aea-165">`CloudTable` (using the Azure Storage SDK.</span></span> <span data-ttu-id="33aea-166">Zobacz [próbki](#readmulti).)</span><span class="sxs-lookup"><span data-stu-id="33aea-166">See [sample](#readmulti).)</span></span>

<a name="outputsample"></a>

## <a name="output-sample"></a><span data-ttu-id="33aea-167">Przykładowe dane wyjściowe</span><span class="sxs-lookup"><span data-stu-id="33aea-167">Output sample</span></span>
<span data-ttu-id="33aea-168">Następujące *function.json* i *run.csx* przykład przedstawia sposób zapisania wiele jednostek tabeli.</span><span class="sxs-lookup"><span data-stu-id="33aea-168">The following *function.json* and *run.csx* example shows how to write multiple table entities.</span></span>

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

<span data-ttu-id="33aea-169">Zobacz próbka specyficzny dla języka, która tworzy wiele jednostek tabeli.</span><span class="sxs-lookup"><span data-stu-id="33aea-169">See the language-specific sample that creates multiple table entities.</span></span>

* [<span data-ttu-id="33aea-170">C#</span><span class="sxs-lookup"><span data-stu-id="33aea-170">C#</span></span>](#outcsharp)
* [<span data-ttu-id="33aea-171">F#</span><span class="sxs-lookup"><span data-stu-id="33aea-171">F#</span></span>](#outfsharp)
* [<span data-ttu-id="33aea-172">Node.js</span><span class="sxs-lookup"><span data-stu-id="33aea-172">Node.js</span></span>](#outnodejs)

<a name="outcsharp"></a>

### <a name="output-sample-in-c"></a><span data-ttu-id="33aea-173">Przykładowe dane wyjściowe w języku C#</span><span class="sxs-lookup"><span data-stu-id="33aea-173">Output sample in C#</span></span> #
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

### <a name="output-sample-in-f"></a><span data-ttu-id="33aea-174">Przykładowe dane wyjściowe w języku F #</span><span class="sxs-lookup"><span data-stu-id="33aea-174">Output sample in F#</span></span> #
```fsharp
[<CLIMutable>]
type Person = {
  PartitionKey: string
  RowKey: string
  Name: string
}

let Run(input: string, tableBinding: ICollector<Person>, log: TraceWriter) =
    for i = 1 to 10 do
        log.Info(sprintf "Adding Person entity %d" i)
        tableBinding.Add(
            { PartitionKey = "Test"
              RowKey = i.ToString()
              Name = "Name" + i.ToString() })
```

<a name="outnodejs"></a>

### <a name="output-sample-in-nodejs"></a><span data-ttu-id="33aea-175">Przykładowe dane wyjściowe w środowisku Node.js</span><span class="sxs-lookup"><span data-stu-id="33aea-175">Output sample in Node.js</span></span>
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

## <a name="sample-read-multiple-table-entities-in-c"></a><span data-ttu-id="33aea-176">Przykład: Odczytu wiele jednostek tabeli w języku C#</span><span class="sxs-lookup"><span data-stu-id="33aea-176">Sample: Read multiple table entities in C#</span></span>  #
<span data-ttu-id="33aea-177">Następujące *function.json* i przykładowy kod w języku C# odczytuje jednostek dla klucza partycji, który jest określony w komunikacie kolejki.</span><span class="sxs-lookup"><span data-stu-id="33aea-177">The following *function.json* and C# code example reads entities for a partition key that is specified in the queue message.</span></span>

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

<span data-ttu-id="33aea-178">Kod C# dodaje odwołanie do zestawu SDK usługi Magazyn Azure, aby typ jednostki mogą dziedziczyć po `TableEntity`.</span><span class="sxs-lookup"><span data-stu-id="33aea-178">The C# code adds a reference to the Azure Storage SDK so that the entity type can derive from `TableEntity`.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="33aea-179">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="33aea-179">Next steps</span></span>
[!INCLUDE [next steps](../../includes/functions-bindings-next-steps.md)]

