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
# <a name="azure-functions-storage-table-bindings"></a><span data-ttu-id="434f5-104">Azure powiązania tabeli w funkcji magazynu</span><span class="sxs-lookup"><span data-stu-id="434f5-104">Azure Functions Storage table bindings</span></span>
[!INCLUDE [functions-selector-bindings](../../includes/functions-selector-bindings.md)]

<span data-ttu-id="434f5-105">W tym artykule opisano, jak tabela powiązania usługi Azure Functions tooconfigure i kodu usługi Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="434f5-105">This article explains how tooconfigure and code Azure Storage table bindings in Azure Functions.</span></span> <span data-ttu-id="434f5-106">Azure Functions obsługuje wejściowa i wyjściowa powiązań dla tabel usługi Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="434f5-106">Azure Functions supports input and output bindings for Azure Storage tables.</span></span>

<span data-ttu-id="434f5-107">Powiązanie tabeli magazynu Hello obsługuje hello następujące scenariusze:</span><span class="sxs-lookup"><span data-stu-id="434f5-107">hello Storage table binding supports hello following scenarios:</span></span>

* <span data-ttu-id="434f5-108">**Przeczytaj pojedynczy wiersz w funkcji języka C# lub Node.js** — skonfiguruj `partitionKey` i `rowKey`.</span><span class="sxs-lookup"><span data-stu-id="434f5-108">**Read a single row in a C# or Node.js function** - Set `partitionKey` and `rowKey`.</span></span> <span data-ttu-id="434f5-109">Witaj `filter` i `take` właściwości nie są używane w tym scenariuszu.</span><span class="sxs-lookup"><span data-stu-id="434f5-109">hello `filter` and `take` properties are not used in this scenario.</span></span>
* <span data-ttu-id="434f5-110">**Odczytuje wiele wierszy w funkcji języka C#** -udostępnia środowisko uruchomieniowe Functions hello `IQueryable<T>` obiekt powiązany toohello tabeli.</span><span class="sxs-lookup"><span data-stu-id="434f5-110">**Read multiple rows in a C# function** - hello Functions runtime provides an `IQueryable<T>` object bound toohello table.</span></span> <span data-ttu-id="434f5-111">Typ `T` musi pochodzić od `TableEntity` , lub zaimplementuj `ITableEntity`.</span><span class="sxs-lookup"><span data-stu-id="434f5-111">Type `T` must derive from `TableEntity` or implement `ITableEntity`.</span></span> <span data-ttu-id="434f5-112">Witaj `partitionKey`, `rowKey`, `filter`, i `take` właściwości nie są używane w tym scenariuszu; można użyć hello `IQueryable` obiekt toodo żadnego filtrowania wymagane.</span><span class="sxs-lookup"><span data-stu-id="434f5-112">hello `partitionKey`, `rowKey`, `filter`, and `take` properties are not used in this scenario; you can use hello `IQueryable` object toodo any filtering required.</span></span> 
* <span data-ttu-id="434f5-113">**Odczytuje wiele wierszy w funkcji węzła** — skonfiguruj hello `filter` i `take` właściwości.</span><span class="sxs-lookup"><span data-stu-id="434f5-113">**Read multiple rows in a Node function** - Set hello `filter` and `take` properties.</span></span> <span data-ttu-id="434f5-114">Nie należy ustawiać `partitionKey` lub `rowKey`.</span><span class="sxs-lookup"><span data-stu-id="434f5-114">Don't set `partitionKey` or `rowKey`.</span></span>
* <span data-ttu-id="434f5-115">**Wpisz jeden lub więcej wierszy w funkcji języka C#** — udostępnia środowisko uruchomieniowe Functions hello `ICollector<T>` lub `IAsyncCollector<T>` toohello powiązanej tabeli, gdzie `T` Określa schemat hello jednostek hello ma tooadd.</span><span class="sxs-lookup"><span data-stu-id="434f5-115">**Write one or more rows in a C# function** - hello Functions runtime provides an `ICollector<T>` or `IAsyncCollector<T>` bound toohello table, where `T` specifies hello schema of hello entities you want tooadd.</span></span> <span data-ttu-id="434f5-116">Zwykle, wpisz `T` pochodzi z `TableEntity` lub implementuje `ITableEntity`, ale nie ma.</span><span class="sxs-lookup"><span data-stu-id="434f5-116">Typically, type `T` derives from `TableEntity` or implements `ITableEntity`, but it doesn't have to.</span></span> <span data-ttu-id="434f5-117">Witaj `partitionKey`, `rowKey`, `filter`, i `take` właściwości nie są używane w tym scenariuszu.</span><span class="sxs-lookup"><span data-stu-id="434f5-117">hello `partitionKey`, `rowKey`, `filter`, and `take` properties are not used in this scenario.</span></span>

[!INCLUDE [intro](../../includes/functions-bindings-intro.md)]

<a name="input"></a>

## <a name="storage-table-input-binding"></a><span data-ttu-id="434f5-118">Powiązania wejściowego tabeli magazynu</span><span class="sxs-lookup"><span data-stu-id="434f5-118">Storage table input binding</span></span>
<span data-ttu-id="434f5-119">Witaj powiązania wejściowego tabeli magazynu Azure umożliwia toouse tabeli w funkcji magazynu.</span><span class="sxs-lookup"><span data-stu-id="434f5-119">hello Azure Storage table input binding enables you toouse a storage table in your function.</span></span> 

<span data-ttu-id="434f5-120">Hello funkcji tooa wejściowej tabeli magazynu używa hello następujące obiekty JSON w hello `bindings` tablicy function.json:</span><span class="sxs-lookup"><span data-stu-id="434f5-120">hello Storage table input tooa function uses hello following JSON objects in hello `bindings` array of function.json:</span></span>

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

<span data-ttu-id="434f5-121">Należy uwzględnić następujące hello:</span><span class="sxs-lookup"><span data-stu-id="434f5-121">Note hello following:</span></span> 

* <span data-ttu-id="434f5-122">Użyj `partitionKey` i `rowKey` razem tooread pojedynczej jednostki.</span><span class="sxs-lookup"><span data-stu-id="434f5-122">Use `partitionKey` and `rowKey` together tooread a single entity.</span></span> <span data-ttu-id="434f5-123">Te właściwości są opcjonalne.</span><span class="sxs-lookup"><span data-stu-id="434f5-123">These properties are optional.</span></span> 
* <span data-ttu-id="434f5-124">`connection`musi zawierać nazwę hello ustawienia aplikacji, która zawiera parametry połączenia magazynu.</span><span class="sxs-lookup"><span data-stu-id="434f5-124">`connection` must contain hello name of an app setting that contains a storage connection string.</span></span> <span data-ttu-id="434f5-125">W portalu Azure hello, hello standardowego edytora w hello **integracji** kartę konfiguruje to ustawienie aplikacji do tworzenia magazynu konta lub wybiera istniejący.</span><span class="sxs-lookup"><span data-stu-id="434f5-125">In hello Azure portal, hello standard editor in hello **Integrate** tab configures this app setting for you when you create a Storage account or selects an existing one.</span></span> <span data-ttu-id="434f5-126">Możesz również [konfigurowania tej aplikacji ręcznie ustawienie](functions-how-to-use-azure-function-app-settings.md#settings).</span><span class="sxs-lookup"><span data-stu-id="434f5-126">You can also [configure this app setting manually](functions-how-to-use-azure-function-app-settings.md#settings).</span></span>  

<a name="inputusage"></a>

## <a name="input-usage"></a><span data-ttu-id="434f5-127">Użycie wejściowych</span><span class="sxs-lookup"><span data-stu-id="434f5-127">Input usage</span></span>
<span data-ttu-id="434f5-128">W języku C# funkcji, możesz powiązać toohello wejściowej tabeli (lub jednostek) przy użyciu nazwanego parametru w podpisu funkcji tak samo, jak `<T> <name>`.</span><span class="sxs-lookup"><span data-stu-id="434f5-128">In C# functions, you bind toohello input table entity (or entities) by using a named parameter in your function signature, like `<T> <name>`.</span></span>
<span data-ttu-id="434f5-129">Gdzie `T` jest typ danych hello, które mają toodeserialize hello dane, i `paramName` jest nazwą hello określone w hello [wejściowych powiązania](#input).</span><span class="sxs-lookup"><span data-stu-id="434f5-129">Where `T` is hello data type that you want toodeserialize hello data into, and `paramName` is hello name you specified in hello [input binding](#input).</span></span> <span data-ttu-id="434f5-130">W przypadku funkcji Node.js dostępu hello wejściowej tabeli (lub jednostek) przy użyciu `context.bindings.<name>`.</span><span class="sxs-lookup"><span data-stu-id="434f5-130">In Node.js functions, you access hello input table entity (or entities) using `context.bindings.<name>`.</span></span>

<span data-ttu-id="434f5-131">dane wejściowe Hello może być zdeserializowany w funkcjach Node.js lub C#.</span><span class="sxs-lookup"><span data-stu-id="434f5-131">hello input data can be deserialized in Node.js or C# functions.</span></span> <span data-ttu-id="434f5-132">obiekty Hello rozszeregować mają `RowKey` i `PartitionKey` właściwości.</span><span class="sxs-lookup"><span data-stu-id="434f5-132">hello deserialized objects have `RowKey` and `PartitionKey` properties.</span></span>

<span data-ttu-id="434f5-133">W języku C# funkcje może także powiązać tooany hello następujące typy i funkcje hello środowiska uruchomieniowego podejmie próbę deserializacji zbyt hello tabeli danych przy użyciu tego typu:</span><span class="sxs-lookup"><span data-stu-id="434f5-133">In C# functions, you can also bind tooany of hello following types, and hello Functions runtime will attempt too deserialize hello table data using that type:</span></span>

* <span data-ttu-id="434f5-134">Dowolnego typu, który implementuje`ITableEntity`</span><span class="sxs-lookup"><span data-stu-id="434f5-134">Any type that implements `ITableEntity`</span></span>
* `IQueryable<T>`

<a name="inputsample"></a>

## <a name="input-sample"></a><span data-ttu-id="434f5-135">Przykładowe wejściowych</span><span class="sxs-lookup"><span data-stu-id="434f5-135">Input sample</span></span>
<span data-ttu-id="434f5-136">Powinien mieć powitania po function.json, używający kolejki wyzwalacza tooread wiersza pojedynczej tabeli.</span><span class="sxs-lookup"><span data-stu-id="434f5-136">Supposed you have hello following function.json, which uses a queue trigger tooread a single table row.</span></span> <span data-ttu-id="434f5-137">Witaj JSON Określa `PartitionKey`  
 `RowKey`.</span><span class="sxs-lookup"><span data-stu-id="434f5-137">hello JSON specifies `PartitionKey` 
`RowKey`.</span></span> <span data-ttu-id="434f5-138">`"rowKey": "{queueTrigger}"`Wskazuje, że ten klucz wiersza hello pochodzi z hello kolejki wiadomości ciąg.</span><span class="sxs-lookup"><span data-stu-id="434f5-138">`"rowKey": "{queueTrigger}"` indicates that hello row key comes from hello queue message string.</span></span>

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

<span data-ttu-id="434f5-139">Zobacz hello próbka specyficzny dla języka, która odczytuje jednostki pojedynczej tabeli.</span><span class="sxs-lookup"><span data-stu-id="434f5-139">See hello language-specific sample that reads a single table entity.</span></span>

* [<span data-ttu-id="434f5-140">C#</span><span class="sxs-lookup"><span data-stu-id="434f5-140">C#</span></span>](#inputcsharp)
* [<span data-ttu-id="434f5-141">F#</span><span class="sxs-lookup"><span data-stu-id="434f5-141">F#</span></span>](#inputfsharp)
* [<span data-ttu-id="434f5-142">Node.js</span><span class="sxs-lookup"><span data-stu-id="434f5-142">Node.js</span></span>](#inputnodejs)

<a name="inputcsharp"></a>

### <a name="input-sample-in-c"></a><span data-ttu-id="434f5-143">Przykładowe wejściowego w języku C#</span><span class="sxs-lookup"><span data-stu-id="434f5-143">Input sample in C#</span></span> #
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

### <a name="input-sample-in-f"></a><span data-ttu-id="434f5-144">Przykładowe wejściowego w języku F #</span><span class="sxs-lookup"><span data-stu-id="434f5-144">Input sample in F#</span></span> #
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

### <a name="input-sample-in-nodejs"></a><span data-ttu-id="434f5-145">Przykładowe wejściowego w środowisku Node.js</span><span class="sxs-lookup"><span data-stu-id="434f5-145">Input sample in Node.js</span></span>
```javascript
module.exports = function (context, myQueueItem) {
    context.log('Node.js queue trigger function processed work item', myQueueItem);
    context.log('Person entity name: ' + context.bindings.personEntity.Name);
    context.done();
};
```

<a name="output"></a>

## <a name="storage-table-output-binding"></a><span data-ttu-id="434f5-146">Tabela magazynu powiązania wyjściowego</span><span class="sxs-lookup"><span data-stu-id="434f5-146">Storage table output binding</span></span>
<span data-ttu-id="434f5-147">Powiązanie umożliwia toowrite jednostek tooa magazynu tabeli w funkcji wyjściowe Hello tabeli magazynu Azure.</span><span class="sxs-lookup"><span data-stu-id="434f5-147">hello Azure Storage table output binding enables you toowrite entities tooa Storage table in your function.</span></span> 

<span data-ttu-id="434f5-148">Witaj magazynu w tabeli danych wyjściowych dla funkcji używa hello następujące obiekty JSON w hello `bindings` tablicy function.json:</span><span class="sxs-lookup"><span data-stu-id="434f5-148">hello Storage table output for a function uses hello following JSON objects in hello `bindings` array of function.json:</span></span>

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

<span data-ttu-id="434f5-149">Należy uwzględnić następujące hello:</span><span class="sxs-lookup"><span data-stu-id="434f5-149">Note hello following:</span></span> 

* <span data-ttu-id="434f5-150">Użyj `partitionKey` i `rowKey` razem toowrite pojedynczej jednostki.</span><span class="sxs-lookup"><span data-stu-id="434f5-150">Use `partitionKey` and `rowKey` together toowrite a single entity.</span></span> <span data-ttu-id="434f5-151">Te właściwości są opcjonalne.</span><span class="sxs-lookup"><span data-stu-id="434f5-151">These properties are optional.</span></span> <span data-ttu-id="434f5-152">Można również określić `PartitionKey` i `RowKey` podczas tworzenia hello obiektów jednostek w kodzie funkcji.</span><span class="sxs-lookup"><span data-stu-id="434f5-152">You can also specify `PartitionKey` and `RowKey` when you create hello entity objects in your function code.</span></span>
* <span data-ttu-id="434f5-153">`connection`musi zawierać nazwę hello ustawienia aplikacji, która zawiera parametry połączenia magazynu.</span><span class="sxs-lookup"><span data-stu-id="434f5-153">`connection` must contain hello name of an app setting that contains a storage connection string.</span></span> <span data-ttu-id="434f5-154">W portalu Azure hello, hello standardowego edytora w hello **integracji** kartę konfiguruje to ustawienie aplikacji do tworzenia magazynu konta lub wybiera istniejący.</span><span class="sxs-lookup"><span data-stu-id="434f5-154">In hello Azure portal, hello standard editor in hello **Integrate** tab configures this app setting for you when you create a Storage account or selects an existing one.</span></span> <span data-ttu-id="434f5-155">Możesz również [konfigurowania tej aplikacji ręcznie ustawienie](functions-how-to-use-azure-function-app-settings.md#settings).</span><span class="sxs-lookup"><span data-stu-id="434f5-155">You can also [configure this app setting manually](functions-how-to-use-azure-function-app-settings.md#settings).</span></span> 

<a name="outputusage"></a>

## <a name="output-usage"></a><span data-ttu-id="434f5-156">Użycie danych wyjściowych</span><span class="sxs-lookup"><span data-stu-id="434f5-156">Output usage</span></span>
<span data-ttu-id="434f5-157">W języku C# funkcji, powiązania toohello w tabeli danych wyjściowych za pomocą hello o nazwie `out` parametru w podpisu funkcji, takich jak `out <T> <name>`, gdzie `T` jest typ danych hello, które mają tooserialize hello dane, i `paramName` jest hello wybraną nazwę określony w hello [powiązania wyjściowego](#output).</span><span class="sxs-lookup"><span data-stu-id="434f5-157">In C# functions, you bind toohello table output by using hello named `out` parameter in your function signature, like `out <T> <name>`, where `T` is hello data type that you want tooserialize hello data into, and `paramName` is hello name you specified in hello [output binding](#output).</span></span> <span data-ttu-id="434f5-158">W przypadku funkcji Node.js dostępu tabeli hello wyjściowe `context.bindings.<name>`.</span><span class="sxs-lookup"><span data-stu-id="434f5-158">In Node.js functions, you access hello table output using `context.bindings.<name>`.</span></span>

<span data-ttu-id="434f5-159">Może serializować obiektów w funkcjach Node.js lub C#.</span><span class="sxs-lookup"><span data-stu-id="434f5-159">You can serialize objects in Node.js or C# functions.</span></span> <span data-ttu-id="434f5-160">W języku C# funkcji można także powiązać toohello następujące typy:</span><span class="sxs-lookup"><span data-stu-id="434f5-160">In C# functions, you can also bind toohello following types:</span></span>

* <span data-ttu-id="434f5-161">Dowolnego typu, który implementuje`ITableEntity`</span><span class="sxs-lookup"><span data-stu-id="434f5-161">Any type that implements `ITableEntity`</span></span>
* <span data-ttu-id="434f5-162">`ICollector<T>`(toooutput wiele jednostek.</span><span class="sxs-lookup"><span data-stu-id="434f5-162">`ICollector<T>` (toooutput multiple entities.</span></span> <span data-ttu-id="434f5-163">Zobacz [próbki](#outcsharp).)</span><span class="sxs-lookup"><span data-stu-id="434f5-163">See [sample](#outcsharp).)</span></span>
* <span data-ttu-id="434f5-164">`IAsyncCollector<T>`(wersja async `ICollector<T>`)</span><span class="sxs-lookup"><span data-stu-id="434f5-164">`IAsyncCollector<T>` (async version of `ICollector<T>`)</span></span>
* <span data-ttu-id="434f5-165">`CloudTable`(przy użyciu hello zestawu SDK usługi Magazyn Azure.</span><span class="sxs-lookup"><span data-stu-id="434f5-165">`CloudTable` (using hello Azure Storage SDK.</span></span> <span data-ttu-id="434f5-166">Zobacz [próbki](#readmulti).)</span><span class="sxs-lookup"><span data-stu-id="434f5-166">See [sample](#readmulti).)</span></span>

<a name="outputsample"></a>

## <a name="output-sample"></a><span data-ttu-id="434f5-167">Przykładowe dane wyjściowe</span><span class="sxs-lookup"><span data-stu-id="434f5-167">Output sample</span></span>
<span data-ttu-id="434f5-168">następujące Hello *function.json* i *run.csx* przykładzie pokazano sposób toowrite wiele jednostek tabeli.</span><span class="sxs-lookup"><span data-stu-id="434f5-168">hello following *function.json* and *run.csx* example shows how toowrite multiple table entities.</span></span>

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

<span data-ttu-id="434f5-169">Zobacz hello przykład specyficzny dla języka, który tworzy wiele jednostek tabeli.</span><span class="sxs-lookup"><span data-stu-id="434f5-169">See hello language-specific sample that creates multiple table entities.</span></span>

* [<span data-ttu-id="434f5-170">C#</span><span class="sxs-lookup"><span data-stu-id="434f5-170">C#</span></span>](#outcsharp)
* [<span data-ttu-id="434f5-171">F#</span><span class="sxs-lookup"><span data-stu-id="434f5-171">F#</span></span>](#outfsharp)
* [<span data-ttu-id="434f5-172">Node.js</span><span class="sxs-lookup"><span data-stu-id="434f5-172">Node.js</span></span>](#outnodejs)

<a name="outcsharp"></a>

### <a name="output-sample-in-c"></a><span data-ttu-id="434f5-173">Przykładowe dane wyjściowe w języku C#</span><span class="sxs-lookup"><span data-stu-id="434f5-173">Output sample in C#</span></span> #
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

### <a name="output-sample-in-f"></a><span data-ttu-id="434f5-174">Przykładowe dane wyjściowe w języku F #</span><span class="sxs-lookup"><span data-stu-id="434f5-174">Output sample in F#</span></span> #
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

### <a name="output-sample-in-nodejs"></a><span data-ttu-id="434f5-175">Przykładowe dane wyjściowe w środowisku Node.js</span><span class="sxs-lookup"><span data-stu-id="434f5-175">Output sample in Node.js</span></span>
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

## <a name="sample-read-multiple-table-entities-in-c"></a><span data-ttu-id="434f5-176">Przykład: Odczytu wiele jednostek tabeli w języku C#</span><span class="sxs-lookup"><span data-stu-id="434f5-176">Sample: Read multiple table entities in C#</span></span>  #
<span data-ttu-id="434f5-177">następujące Hello *function.json* i jednostek dla klucza partycji, który jest określony w komunikacie kolejki hello odczytuje przykładowego kodu w języku C#.</span><span class="sxs-lookup"><span data-stu-id="434f5-177">hello following *function.json* and C# code example reads entities for a partition key that is specified in hello queue message.</span></span>

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

<span data-ttu-id="434f5-178">Hello kod w języku C# dodaje toohello odwołanie do zestawu SDK usługi Magazyn Azure, aby typ jednostki hello może pochodzić od `TableEntity`.</span><span class="sxs-lookup"><span data-stu-id="434f5-178">hello C# code adds a reference toohello Azure Storage SDK so that hello entity type can derive from `TableEntity`.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="434f5-179">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="434f5-179">Next steps</span></span>
[!INCLUDE [next steps](../../includes/functions-bindings-next-steps.md)]

