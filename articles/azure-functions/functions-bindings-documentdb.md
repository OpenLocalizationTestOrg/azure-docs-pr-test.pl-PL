---
title: "powiązania funkcji rozwiązania Cosmos DB aaaAzure | Dokumentacja firmy Microsoft"
description: "Zrozumienie sposobu toouse bazy danych Azure rozwiązania Cosmos powiązania usługi Azure Functions."
services: functions
documentationcenter: na
author: christopheranderson
manager: erikre
editor: 
tags: 
keywords: "funkcje usługi Azure, funkcje, przetwarzania zdarzeń, dynamiczne obliczeń niekorzystającą architektury"
ms.assetid: 3d8497f0-21f3-437d-ba24-5ece8c90ac85
ms.service: functions
ms.devlang: multiple
ms.topic: reference
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 04/18/2016
ms.author: glenga
ms.openlocfilehash: 76b89e8296db1dd28dff9528903b1f6a28f55232
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-functions-cosmos-db-bindings"></a><span data-ttu-id="19b90-104">Azure powiązania funkcji DB rozwiązania Cosmos</span><span class="sxs-lookup"><span data-stu-id="19b90-104">Azure Functions Cosmos DB bindings</span></span>
[!INCLUDE [functions-selector-bindings](../../includes/functions-selector-bindings.md)]

<span data-ttu-id="19b90-105">W tym artykule opisano sposób powiązania bazy danych Azure rozwiązania Cosmos tooconfigure i kodu w funkcji platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="19b90-105">This article explains how tooconfigure and code Azure Cosmos DB bindings in Azure Functions.</span></span> <span data-ttu-id="19b90-106">Azure Functions obsługuje wejściowa i wyjściowa powiązania dla DB rozwiązania Cosmos.</span><span class="sxs-lookup"><span data-stu-id="19b90-106">Azure Functions supports input and output bindings for Cosmos DB.</span></span>

[!INCLUDE [intro](../../includes/functions-bindings-intro.md)]

<span data-ttu-id="19b90-107">Aby uzyskać więcej informacji na rozwiązania Cosmos bazy danych, zobacz [tooCosmos wprowadzenie DB](../documentdb/documentdb-introduction.md) i [tworzenia aplikacji konsoli DB rozwiązania Cosmos](../documentdb/documentdb-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="19b90-107">For more information on Cosmos DB, see [Introduction tooCosmos DB](../documentdb/documentdb-introduction.md) and [Build a Cosmos DB console application](../documentdb/documentdb-get-started.md).</span></span>

<a id="docdbinput"></a>

## <a name="documentdb-api-input-binding"></a><span data-ttu-id="19b90-108">Powiązania wejściowego interfejsu API usługi DocumentDB</span><span class="sxs-lookup"><span data-stu-id="19b90-108">DocumentDB API input binding</span></span>
<span data-ttu-id="19b90-109">Hello powiązania wejściowego interfejsu API usługi DocumentDB pobiera dokument DB rozwiązania Cosmos i przekazuje je toohello o nazwie parametr wejściowy funkcji hello.</span><span class="sxs-lookup"><span data-stu-id="19b90-109">hello DocumentDB API input binding retrieves a Cosmos DB document and passes it toohello named input parameter of hello function.</span></span> <span data-ttu-id="19b90-110">Witaj dokument, który można ustalić Identyfikatora oparte na powitania wyzwalacz, który wywołuje funkcję hello.</span><span class="sxs-lookup"><span data-stu-id="19b90-110">hello document ID can be determined based on hello trigger that invokes hello function.</span></span> 

<span data-ttu-id="19b90-111">Hello powiązania wejściowego interfejsu API usługi DocumentDB ma następujące właściwości w hello *function.json*:</span><span class="sxs-lookup"><span data-stu-id="19b90-111">hello DocumentDB API input binding has hello following properties in *function.json*:</span></span>

- <span data-ttu-id="19b90-112">`name`: Nazwa identyfikator używane w kodzie funkcja hello dokumentu</span><span class="sxs-lookup"><span data-stu-id="19b90-112">`name` : Identifier name used in function code for hello document</span></span>
- <span data-ttu-id="19b90-113">`type`: musi być ustawiona zbyt "documentdb"</span><span class="sxs-lookup"><span data-stu-id="19b90-113">`type` : must be set too"documentdb"</span></span>
- <span data-ttu-id="19b90-114">`databaseName`: hello bazy danych zawierającej hello dokument</span><span class="sxs-lookup"><span data-stu-id="19b90-114">`databaseName` : hello database containing hello document</span></span>
- <span data-ttu-id="19b90-115">`collectionName`: hello kolekcja zawierająca hello dokumentu</span><span class="sxs-lookup"><span data-stu-id="19b90-115">`collectionName` : hello collection containing hello document</span></span>
- <span data-ttu-id="19b90-116">`id`: hello identyfikator hello tooretrieve dokumentu.</span><span class="sxs-lookup"><span data-stu-id="19b90-116">`id` : hello Id of hello document tooretrieve.</span></span> <span data-ttu-id="19b90-117">Ta właściwość obsługuje wiązania parametrów; zobacz [powiązać toocustom właściwości wejściowych w wyrażeniu powiązania](functions-triggers-bindings.md#bind-to-custom-input-properties-in-a-binding-expression) w artykule hello [usługi Azure Functions wyzwalaczy i powiązań pojęcia](functions-triggers-bindings.md).</span><span class="sxs-lookup"><span data-stu-id="19b90-117">This property supports bindings parameters; see [Bind toocustom input properties in a binding expression](functions-triggers-bindings.md#bind-to-custom-input-properties-in-a-binding-expression) in hello article [Azure Functions triggers and bindings concepts](functions-triggers-bindings.md).</span></span>
- <span data-ttu-id="19b90-118">`sqlQuery`: Rozwiązania Cosmos DB kwerendy SQL używane do pobierania wielu dokumentów.</span><span class="sxs-lookup"><span data-stu-id="19b90-118">`sqlQuery` : A Cosmos DB SQL query used for retrieving multiple documents.</span></span> <span data-ttu-id="19b90-119">Zapytanie Hello obsługuje powiązań czasu wykonywania.</span><span class="sxs-lookup"><span data-stu-id="19b90-119">hello query supports runtime bindings.</span></span> <span data-ttu-id="19b90-120">Na przykład: `SELECT * FROM c where c.departmentId = {departmentId}`</span><span class="sxs-lookup"><span data-stu-id="19b90-120">For example: `SELECT * FROM c where c.departmentId = {departmentId}`</span></span>
- <span data-ttu-id="19b90-121">`connection`: hello Nazwa ustawienia aplikacji hello zawierający parametry połączenia bazy danych rozwiązania Cosmos</span><span class="sxs-lookup"><span data-stu-id="19b90-121">`connection` : hello name of hello app setting containing your Cosmos DB connection string</span></span>
- <span data-ttu-id="19b90-122">`direction`: musi być ustawiona zbyt`"in"`.</span><span class="sxs-lookup"><span data-stu-id="19b90-122">`direction`  : must be set too`"in"`.</span></span>

<span data-ttu-id="19b90-123">Witaj właściwości `id` i `sqlQuery` nie może być jednocześnie określone.</span><span class="sxs-lookup"><span data-stu-id="19b90-123">hello properties `id` and `sqlQuery` cannot both be specified.</span></span> <span data-ttu-id="19b90-124">Jeśli żadna `id` ani `sqlQuery` jest ustawiona, hello całej kolekcji są pobierane.</span><span class="sxs-lookup"><span data-stu-id="19b90-124">If neither `id` nor `sqlQuery` is set, hello entire collection is retrieved.</span></span>

## <a name="using-a-documentdb-api-input-binding"></a><span data-ttu-id="19b90-125">Przy użyciu interfejsu API usługi DocumentDB powiązania wejściowego</span><span class="sxs-lookup"><span data-stu-id="19b90-125">Using a DocumentDB API input binding</span></span>

* <span data-ttu-id="19b90-126">W języku C# i F # funkcjach gdy funkcja hello kończy się pomyślnie, wszystkie zmiany wprowadzone toohello dokument wejściowy za pośrednictwem nazwanych parametrów wejściowych automatycznie są zachowywane.</span><span class="sxs-lookup"><span data-stu-id="19b90-126">In C# and F# functions, when hello function exits successfully, any changes made toohello input document via named input parameters are automatically persisted.</span></span> 
* <span data-ttu-id="19b90-127">W funkcji JavaScript aktualizacje nie będą automatycznie po wyjściu z funkcji.</span><span class="sxs-lookup"><span data-stu-id="19b90-127">In JavaScript functions, updates are not made automatically upon function exit.</span></span> <span data-ttu-id="19b90-128">Zamiast tego należy użyć `context.bindings.<documentName>In` i `context.bindings.<documentName>Out` toomake aktualizacji.</span><span class="sxs-lookup"><span data-stu-id="19b90-128">Instead, use `context.bindings.<documentName>In` and `context.bindings.<documentName>Out` toomake updates.</span></span> <span data-ttu-id="19b90-129">Zobacz hello [próbki JavaScript](#injavascript).</span><span class="sxs-lookup"><span data-stu-id="19b90-129">See hello [JavaScript sample](#injavascript).</span></span>

<a name="inputsample"></a>

## <a name="input-sample-for-single-document"></a><span data-ttu-id="19b90-130">Przykład wejściowego dla pojedynczego dokumentu</span><span class="sxs-lookup"><span data-stu-id="19b90-130">Input sample for single document</span></span>
<span data-ttu-id="19b90-131">Załóżmy, że masz następujące hello interfejsu API usługi DocumentDB wejściowych powiązanie w hello `bindings` tablicy function.json:</span><span class="sxs-lookup"><span data-stu-id="19b90-131">Suppose you have hello following DocumentDB API input binding in hello `bindings` array of function.json:</span></span>

```json
{
  "name": "inputDocument",
  "type": "documentDB",
  "databaseName": "MyDatabase",
  "collectionName": "MyCollection",
  "id" : "{queueTrigger}",
  "connection": "MyAccount_COSMOSDB",     
  "direction": "in"
}
```

<span data-ttu-id="19b90-132">Zobacz przykład specyficzny dla języka hello, który korzysta z wartości tekstowej powiązania wejściowego tooupdate hello tego dokumentu.</span><span class="sxs-lookup"><span data-stu-id="19b90-132">See hello language-specific sample that uses this input binding tooupdate hello document's text value.</span></span>

* [<span data-ttu-id="19b90-133">C#</span><span class="sxs-lookup"><span data-stu-id="19b90-133">C#</span></span>](#incsharp)
* [<span data-ttu-id="19b90-134">F#</span><span class="sxs-lookup"><span data-stu-id="19b90-134">F#</span></span>](#infsharp)
* [<span data-ttu-id="19b90-135">JavaScript</span><span class="sxs-lookup"><span data-stu-id="19b90-135">JavaScript</span></span>](#injavascript)

<a name="incsharp"></a>
### <a name="input-sample-in-c"></a><span data-ttu-id="19b90-136">Przykładowe wejściowego w języku C#</span><span class="sxs-lookup"><span data-stu-id="19b90-136">Input sample in C#</span></span> #

```cs
// Change input document contents using DocumentDB API input binding 
public static void Run(string myQueueItem, dynamic inputDocument)
{   
  inputDocument.text = "This has changed.";
}
```
<a name="infsharp"></a>

### <a name="input-sample-in-f"></a><span data-ttu-id="19b90-137">Przykładowe wejściowego w języku F #</span><span class="sxs-lookup"><span data-stu-id="19b90-137">Input sample in F#</span></span> #

```fsharp
(* Change input document contents using DocumentDB API input binding *)
open FSharp.Interop.Dynamic
let Run(myQueueItem: string, inputDocument: obj) =
  inputDocument?text <- "This has changed."
```

<span data-ttu-id="19b90-138">W tym przykładzie wymaga `project.json` pliku, który określa hello `FSharp.Interop.Dynamic` i `Dynamitey` zależności NuGet:</span><span class="sxs-lookup"><span data-stu-id="19b90-138">This sample requires a `project.json` file that specifies hello `FSharp.Interop.Dynamic` and `Dynamitey` NuGet dependencies:</span></span>

```json
{
  "frameworks": {
    "net46": {
      "dependencies": {
        "Dynamitey": "1.0.2",
        "FSharp.Interop.Dynamic": "3.0.0"
      }
    }
  }
}
```

<span data-ttu-id="19b90-139">tooadd `project.json` plików, zobacz [zarządzania pakietami F #](functions-reference-fsharp.md#package).</span><span class="sxs-lookup"><span data-stu-id="19b90-139">tooadd a `project.json` file, see [F# package management](functions-reference-fsharp.md#package).</span></span>

<a name="injavascript"></a>

### <a name="input-sample-in-javascript"></a><span data-ttu-id="19b90-140">Przykładowe wejściowego w języku JavaScript</span><span class="sxs-lookup"><span data-stu-id="19b90-140">Input sample in JavaScript</span></span>

```javascript
// Change input document contents using DocumentDB API input binding, using context.bindings.inputDocumentOut
module.exports = function (context) {   
  context.bindings.inputDocumentOut = context.bindings.inputDocumentIn;
  context.bindings.inputDocumentOut.text = "This was updated!";
  context.done();
};
```

## <a name="input-sample-with-multiple-documents"></a><span data-ttu-id="19b90-141">Przykładowe wejściowy z wieloma dokumentami</span><span class="sxs-lookup"><span data-stu-id="19b90-141">Input sample with multiple documents</span></span>

<span data-ttu-id="19b90-142">Załóżmy, że chcesz tooretrieve wielu dokumentów określonych przez zapytanie SQL, za pomocą parametrów zapytania hello toocustomize kolejki wyzwalacza.</span><span class="sxs-lookup"><span data-stu-id="19b90-142">Suppose that you wish tooretrieve multiple documents specified by a SQL query, using a queue trigger toocustomize hello query parameters.</span></span> 

<span data-ttu-id="19b90-143">W tym przykładzie hello kolejki wyzwalacza zawiera parametr `departmentId`. Komunikat z kolejki z `{ "departmentId" : "Finance" }` zwróci wszystkie rekordy dotyczące hello działu finansowego.</span><span class="sxs-lookup"><span data-stu-id="19b90-143">In this example, hello queue trigger provides a parameter `departmentId`.A queue message of `{ "departmentId" : "Finance" }` would return all records for hello finance department.</span></span> <span data-ttu-id="19b90-144">Użyj następujących hello w *function.json*:</span><span class="sxs-lookup"><span data-stu-id="19b90-144">Use hello following in *function.json*:</span></span>

```
{
    "name": "documents",
    "type": "documentdb",
    "direction": "in",
    "databaseName": "MyDb",
    "collectionName": "MyCollection",
    "sqlQuery": "SELECT * from c where c.departmentId = {departmentId}"
    "connection": "CosmosDBConnection"
}
```

### <a name="input-sample-with-multiple-documents-in-c"></a><span data-ttu-id="19b90-145">Przykładowe wejściowy z wieloma dokumentami w języku C#</span><span class="sxs-lookup"><span data-stu-id="19b90-145">Input sample with multiple documents in C#</span></span>

```csharp
public static void Run(QueuePayload myQueueItem, IEnumerable<dynamic> documents)
{   
    foreach (var doc in documents)
    {
        // operate on each document
    }    
}

public class QueuePayload
{
    public string departmentId { get; set; }
}
```

### <a name="input-sample-with-multiple-documents-in-javascript"></a><span data-ttu-id="19b90-146">Przykładowe wejściowy z wieloma dokumentami w języku JavaScript</span><span class="sxs-lookup"><span data-stu-id="19b90-146">Input sample with multiple documents in JavaScript</span></span>

```javascript
module.exports = function (context, input) {    
    var documents = context.bindings.documents;
    for (var i = 0; i < documents.length; i++) {
        var document = documents[i];
        // operate on each document
    }       
    context.done();
};
```

## <span data-ttu-id="19b90-147"><a id="docdboutput"></a>Powiązania wyjściowego interfejsu API usługi DocumentDB</span><span class="sxs-lookup"><span data-stu-id="19b90-147"><a id="docdboutput"></a>DocumentDB API output binding</span></span>
<span data-ttu-id="19b90-148">Powiązanie umożliwia zapisanie nowej bazy danych Azure DB rozwiązania Cosmos tooan dokumentu wyjściowe Hello interfejsu API usługi DocumentDB.</span><span class="sxs-lookup"><span data-stu-id="19b90-148">hello DocumentDB API output binding lets you write a new document tooan Azure Cosmos DB database.</span></span> <span data-ttu-id="19b90-149">Ma następujące właściwości w hello *function.json*:</span><span class="sxs-lookup"><span data-stu-id="19b90-149">It has hello following properties in *function.json*:</span></span>

- <span data-ttu-id="19b90-150">`name`: Identyfikator używane w kodzie funkcja hello nowego dokumentu.</span><span class="sxs-lookup"><span data-stu-id="19b90-150">`name` : Identifier used in function code for hello new document</span></span>
- <span data-ttu-id="19b90-151">`type`: musi być ustawiona zbyt`"documentdb"`</span><span class="sxs-lookup"><span data-stu-id="19b90-151">`type` : must be set too`"documentdb"`</span></span>
- <span data-ttu-id="19b90-152">`databaseName`: hello bazy danych zawierające kolekcji hello, w której zostanie utworzony nowy dokument hello.</span><span class="sxs-lookup"><span data-stu-id="19b90-152">`databaseName` : hello database containing hello collection where hello new document will be created.</span></span>
- <span data-ttu-id="19b90-153">`collectionName`: hello kolekcji, w której zostanie utworzony nowy dokument hello.</span><span class="sxs-lookup"><span data-stu-id="19b90-153">`collectionName` : hello collection where hello new document will be created.</span></span>
- <span data-ttu-id="19b90-154">`createIfNotExists`: Wartość logiczna tooindicate czy hello Kolekcja zostanie utworzona, jeśli nie istnieje.</span><span class="sxs-lookup"><span data-stu-id="19b90-154">`createIfNotExists` : A boolean value tooindicate whether hello collection will be created if it does not exist.</span></span> <span data-ttu-id="19b90-155">Domyślnie Hello *false*.</span><span class="sxs-lookup"><span data-stu-id="19b90-155">hello default is *false*.</span></span> <span data-ttu-id="19b90-156">Witaj przyczyn jest to nowe kolekcje są tworzone z zarezerwowaną przepływnością, co ma implikacje cenowe.</span><span class="sxs-lookup"><span data-stu-id="19b90-156">hello reason for this is new collections are created with reserved throughput, which has pricing implications.</span></span> <span data-ttu-id="19b90-157">Aby uzyskać więcej informacji, odwiedź stronę hello [cennikiem](https://azure.microsoft.com/pricing/details/documentdb/).</span><span class="sxs-lookup"><span data-stu-id="19b90-157">For more details, please visit hello [pricing page](https://azure.microsoft.com/pricing/details/documentdb/).</span></span>
- <span data-ttu-id="19b90-158">`connection`: hello Nazwa ustawienia aplikacji hello zawierający parametry połączenia bazy danych rozwiązania Cosmos</span><span class="sxs-lookup"><span data-stu-id="19b90-158">`connection` : hello name of hello app setting containing your Cosmos DB connection string</span></span>
- <span data-ttu-id="19b90-159">`direction`: musi być ustawiona zbyt`"out"`</span><span class="sxs-lookup"><span data-stu-id="19b90-159">`direction` : must be set too`"out"`</span></span>

## <a name="using-a-documentdb-api-output-binding"></a><span data-ttu-id="19b90-160">Powiązania wyjściowego przy użyciu interfejsu API usługi DocumentDB</span><span class="sxs-lookup"><span data-stu-id="19b90-160">Using a DocumentDB API output binding</span></span>
<span data-ttu-id="19b90-161">W tej sekcji przedstawiono, jak toouse interfejsu API usługi DocumentDB output powiązania w kodzie funkcji.</span><span class="sxs-lookup"><span data-stu-id="19b90-161">This section shows you how toouse your DocumentDB API output binding in your function code.</span></span>

<span data-ttu-id="19b90-162">Podczas pisania toohello parametru wyjściowego w funkcji, domyślnie nowy dokument jest generowana w bazie danych, z automatycznie generowanym identyfikatorze GUID jako hello dokumentu identyfikatora.</span><span class="sxs-lookup"><span data-stu-id="19b90-162">When you write toohello output parameter in your function, by default a new document is generated in your database, with an automatically generated GUID as hello document ID.</span></span> <span data-ttu-id="19b90-163">Identyfikator dokumentu hello dokumentu wyjściowego można określić, podając hello `id` właściwości JSON w hello parametru wyjściowego.</span><span class="sxs-lookup"><span data-stu-id="19b90-163">You can specify hello document ID of output document by specifying hello `id` JSON property in hello output parameter.</span></span> 

>[!Note]  
><span data-ttu-id="19b90-164">Po określeniu Identyfikatora hello istniejącego dokumentu zostaje zastąpiona przez hello nowy dokument danych wyjściowych.</span><span class="sxs-lookup"><span data-stu-id="19b90-164">When you specify hello ID of an existing document, it gets overwritten by hello new output document.</span></span> 

<span data-ttu-id="19b90-165">toooutput wielu dokumentów, możesz także powiązać zbyt`ICollector<T>` lub `IAsyncCollector<T>` gdzie `T` hello obsługiwanych typów.</span><span class="sxs-lookup"><span data-stu-id="19b90-165">toooutput multiple documents, you can also bind too`ICollector<T>` or `IAsyncCollector<T>` where `T` is one of hello supported types.</span></span>

<a name="outputsample"></a>

## <a name="documentdb-api-output-binding-sample"></a><span data-ttu-id="19b90-166">Przykładowe powiązania danych wyjściowych interfejsu API usługi DocumentDB</span><span class="sxs-lookup"><span data-stu-id="19b90-166">DocumentDB API output binding sample</span></span>
<span data-ttu-id="19b90-167">Załóżmy, że masz następujące hello interfejsu API usługi DocumentDB output powiązanie w hello `bindings` tablicy function.json:</span><span class="sxs-lookup"><span data-stu-id="19b90-167">Suppose you have hello following DocumentDB API output binding in hello `bindings` array of function.json:</span></span>

```json
{
  "name": "employeeDocument",
  "type": "documentDB",
  "databaseName": "MyDatabase",
  "collectionName": "MyCollection",
  "createIfNotExists": true,
  "connection": "MyAccount_COSMOSDB",     
  "direction": "out"
}
```

<span data-ttu-id="19b90-168">I mają powiązania wejściowego kolejki dla kolejki, która odbiera JSON w hello następującego formatu:</span><span class="sxs-lookup"><span data-stu-id="19b90-168">And you have a queue input binding for a queue that receives JSON in hello following format:</span></span>

```json
{
  "name": "John Henry",
  "employeeId": "123456",
  "address": "A town nearby"
}
```

<span data-ttu-id="19b90-169">I mają toocreate dokumenty DB rozwiązania Cosmos w następującego formatu dla każdego rekordu hello:</span><span class="sxs-lookup"><span data-stu-id="19b90-169">And you want toocreate Cosmos DB documents in hello following format for each record:</span></span>

```json
{
  "id": "John Henry-123456",
  "name": "John Henry",
  "employeeId": "123456",
  "address": "A town nearby"
}
```

<span data-ttu-id="19b90-170">Zobacz przykład specyficzny dla języka hello, który używa tej bazy danych wyjściowych powiązania tooadd dokumenty tooyour danych.</span><span class="sxs-lookup"><span data-stu-id="19b90-170">See hello language-specific sample that uses this output binding tooadd documents tooyour database.</span></span>

* [<span data-ttu-id="19b90-171">C#</span><span class="sxs-lookup"><span data-stu-id="19b90-171">C#</span></span>](#outcsharp)
* [<span data-ttu-id="19b90-172">F#</span><span class="sxs-lookup"><span data-stu-id="19b90-172">F#</span></span>](#outfsharp)
* [<span data-ttu-id="19b90-173">JavaScript</span><span class="sxs-lookup"><span data-stu-id="19b90-173">JavaScript</span></span>](#outjavascript)

<a name="outcsharp"></a>

### <a name="output-sample-in-c"></a><span data-ttu-id="19b90-174">Przykładowe dane wyjściowe w języku C#</span><span class="sxs-lookup"><span data-stu-id="19b90-174">Output sample in C#</span></span> #

```cs
#r "Newtonsoft.Json"

using System;
using Newtonsoft.Json;
using Newtonsoft.Json.Linq;

public static void Run(string myQueueItem, out object employeeDocument, TraceWriter log)
{
  log.Info($"C# Queue trigger function processed: {myQueueItem}");

  dynamic employee = JObject.Parse(myQueueItem);

  employeeDocument = new {
    id = employee.name + "-" + employee.employeeId,
    name = employee.name,
    employeeId = employee.employeeId,
    address = employee.address
  };
}
```

<a name="outfsharp"></a>

### <a name="output-sample-in-f"></a><span data-ttu-id="19b90-175">Przykładowe dane wyjściowe w języku F #</span><span class="sxs-lookup"><span data-stu-id="19b90-175">Output sample in F#</span></span> #

```fsharp
open FSharp.Interop.Dynamic
open Newtonsoft.Json

type Employee = {
  id: string
  name: string
  employeeId: string
  address: string
}

let Run(myQueueItem: string, employeeDocument: byref<obj>, log: TraceWriter) =
  log.Info(sprintf "F# Queue trigger function processed: %s" myQueueItem)
  let employee = JObject.Parse(myQueueItem)
  employeeDocument <-
    { id = sprintf "%s-%s" employee?name employee?employeeId
      name = employee?name
      employeeId = employee?employeeId
      address = employee?address }
```

<span data-ttu-id="19b90-176">W tym przykładzie wymaga `project.json` pliku, który określa hello `FSharp.Interop.Dynamic` i `Dynamitey` zależności NuGet:</span><span class="sxs-lookup"><span data-stu-id="19b90-176">This sample requires a `project.json` file that specifies hello `FSharp.Interop.Dynamic` and `Dynamitey` NuGet dependencies:</span></span>

```json
{
  "frameworks": {
    "net46": {
      "dependencies": {
        "Dynamitey": "1.0.2",
        "FSharp.Interop.Dynamic": "3.0.0"
      }
    }
  }
}
```

<span data-ttu-id="19b90-177">tooadd `project.json` plików, zobacz [zarządzania pakietami F #](functions-reference-fsharp.md#package).</span><span class="sxs-lookup"><span data-stu-id="19b90-177">tooadd a `project.json` file, see [F# package management](functions-reference-fsharp.md#package).</span></span>

<a name="outjavascript"></a>

### <a name="output-sample-in-javascript"></a><span data-ttu-id="19b90-178">Przykładowe dane wyjściowe w języku JavaScript</span><span class="sxs-lookup"><span data-stu-id="19b90-178">Output sample in JavaScript</span></span>

```javascript
module.exports = function (context) {

  context.bindings.employeeDocument = JSON.stringify({ 
    id: context.bindings.myQueueItem.name + "-" + context.bindings.myQueueItem.employeeId,
    name: context.bindings.myQueueItem.name,
    employeeId: context.bindings.myQueueItem.employeeId,
    address: context.bindings.myQueueItem.address
  });

  context.done();
};
```
