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
# <a name="azure-functions-cosmos-db-bindings"></a>Azure powiązania funkcji DB rozwiązania Cosmos
[!INCLUDE [functions-selector-bindings](../../includes/functions-selector-bindings.md)]

W tym artykule opisano sposób powiązania bazy danych Azure rozwiązania Cosmos tooconfigure i kodu w funkcji platformy Azure. Azure Functions obsługuje wejściowa i wyjściowa powiązania dla DB rozwiązania Cosmos.

[!INCLUDE [intro](../../includes/functions-bindings-intro.md)]

Aby uzyskać więcej informacji na rozwiązania Cosmos bazy danych, zobacz [tooCosmos wprowadzenie DB](../documentdb/documentdb-introduction.md) i [tworzenia aplikacji konsoli DB rozwiązania Cosmos](../documentdb/documentdb-get-started.md).

<a id="docdbinput"></a>

## <a name="documentdb-api-input-binding"></a>Powiązania wejściowego interfejsu API usługi DocumentDB
Hello powiązania wejściowego interfejsu API usługi DocumentDB pobiera dokument DB rozwiązania Cosmos i przekazuje je toohello o nazwie parametr wejściowy funkcji hello. Witaj dokument, który można ustalić Identyfikatora oparte na powitania wyzwalacz, który wywołuje funkcję hello. 

Hello powiązania wejściowego interfejsu API usługi DocumentDB ma następujące właściwości w hello *function.json*:

- `name`: Nazwa identyfikator używane w kodzie funkcja hello dokumentu
- `type`: musi być ustawiona zbyt "documentdb"
- `databaseName`: hello bazy danych zawierającej hello dokument
- `collectionName`: hello kolekcja zawierająca hello dokumentu
- `id`: hello identyfikator hello tooretrieve dokumentu. Ta właściwość obsługuje wiązania parametrów; zobacz [powiązać toocustom właściwości wejściowych w wyrażeniu powiązania](functions-triggers-bindings.md#bind-to-custom-input-properties-in-a-binding-expression) w artykule hello [usługi Azure Functions wyzwalaczy i powiązań pojęcia](functions-triggers-bindings.md).
- `sqlQuery`: Rozwiązania Cosmos DB kwerendy SQL używane do pobierania wielu dokumentów. Zapytanie Hello obsługuje powiązań czasu wykonywania. Na przykład: `SELECT * FROM c where c.departmentId = {departmentId}`
- `connection`: hello Nazwa ustawienia aplikacji hello zawierający parametry połączenia bazy danych rozwiązania Cosmos
- `direction`: musi być ustawiona zbyt`"in"`.

Witaj właściwości `id` i `sqlQuery` nie może być jednocześnie określone. Jeśli żadna `id` ani `sqlQuery` jest ustawiona, hello całej kolekcji są pobierane.

## <a name="using-a-documentdb-api-input-binding"></a>Przy użyciu interfejsu API usługi DocumentDB powiązania wejściowego

* W języku C# i F # funkcjach gdy funkcja hello kończy się pomyślnie, wszystkie zmiany wprowadzone toohello dokument wejściowy za pośrednictwem nazwanych parametrów wejściowych automatycznie są zachowywane. 
* W funkcji JavaScript aktualizacje nie będą automatycznie po wyjściu z funkcji. Zamiast tego należy użyć `context.bindings.<documentName>In` i `context.bindings.<documentName>Out` toomake aktualizacji. Zobacz hello [próbki JavaScript](#injavascript).

<a name="inputsample"></a>

## <a name="input-sample-for-single-document"></a>Przykład wejściowego dla pojedynczego dokumentu
Załóżmy, że masz następujące hello interfejsu API usługi DocumentDB wejściowych powiązanie w hello `bindings` tablicy function.json:

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

Zobacz przykład specyficzny dla języka hello, który korzysta z wartości tekstowej powiązania wejściowego tooupdate hello tego dokumentu.

* [C#](#incsharp)
* [F#](#infsharp)
* [JavaScript](#injavascript)

<a name="incsharp"></a>
### <a name="input-sample-in-c"></a>Przykładowe wejściowego w języku C# #

```cs
// Change input document contents using DocumentDB API input binding 
public static void Run(string myQueueItem, dynamic inputDocument)
{   
  inputDocument.text = "This has changed.";
}
```
<a name="infsharp"></a>

### <a name="input-sample-in-f"></a>Przykładowe wejściowego w języku F # #

```fsharp
(* Change input document contents using DocumentDB API input binding *)
open FSharp.Interop.Dynamic
let Run(myQueueItem: string, inputDocument: obj) =
  inputDocument?text <- "This has changed."
```

W tym przykładzie wymaga `project.json` pliku, który określa hello `FSharp.Interop.Dynamic` i `Dynamitey` zależności NuGet:

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

tooadd `project.json` plików, zobacz [zarządzania pakietami F #](functions-reference-fsharp.md#package).

<a name="injavascript"></a>

### <a name="input-sample-in-javascript"></a>Przykładowe wejściowego w języku JavaScript

```javascript
// Change input document contents using DocumentDB API input binding, using context.bindings.inputDocumentOut
module.exports = function (context) {   
  context.bindings.inputDocumentOut = context.bindings.inputDocumentIn;
  context.bindings.inputDocumentOut.text = "This was updated!";
  context.done();
};
```

## <a name="input-sample-with-multiple-documents"></a>Przykładowe wejściowy z wieloma dokumentami

Załóżmy, że chcesz tooretrieve wielu dokumentów określonych przez zapytanie SQL, za pomocą parametrów zapytania hello toocustomize kolejki wyzwalacza. 

W tym przykładzie hello kolejki wyzwalacza zawiera parametr `departmentId`. Komunikat z kolejki z `{ "departmentId" : "Finance" }` zwróci wszystkie rekordy dotyczące hello działu finansowego. Użyj następujących hello w *function.json*:

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

### <a name="input-sample-with-multiple-documents-in-c"></a>Przykładowe wejściowy z wieloma dokumentami w języku C#

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

### <a name="input-sample-with-multiple-documents-in-javascript"></a>Przykładowe wejściowy z wieloma dokumentami w języku JavaScript

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

## <a id="docdboutput"></a>Powiązania wyjściowego interfejsu API usługi DocumentDB
Powiązanie umożliwia zapisanie nowej bazy danych Azure DB rozwiązania Cosmos tooan dokumentu wyjściowe Hello interfejsu API usługi DocumentDB. Ma następujące właściwości w hello *function.json*:

- `name`: Identyfikator używane w kodzie funkcja hello nowego dokumentu.
- `type`: musi być ustawiona zbyt`"documentdb"`
- `databaseName`: hello bazy danych zawierające kolekcji hello, w której zostanie utworzony nowy dokument hello.
- `collectionName`: hello kolekcji, w której zostanie utworzony nowy dokument hello.
- `createIfNotExists`: Wartość logiczna tooindicate czy hello Kolekcja zostanie utworzona, jeśli nie istnieje. Domyślnie Hello *false*. Witaj przyczyn jest to nowe kolekcje są tworzone z zarezerwowaną przepływnością, co ma implikacje cenowe. Aby uzyskać więcej informacji, odwiedź stronę hello [cennikiem](https://azure.microsoft.com/pricing/details/documentdb/).
- `connection`: hello Nazwa ustawienia aplikacji hello zawierający parametry połączenia bazy danych rozwiązania Cosmos
- `direction`: musi być ustawiona zbyt`"out"`

## <a name="using-a-documentdb-api-output-binding"></a>Powiązania wyjściowego przy użyciu interfejsu API usługi DocumentDB
W tej sekcji przedstawiono, jak toouse interfejsu API usługi DocumentDB output powiązania w kodzie funkcji.

Podczas pisania toohello parametru wyjściowego w funkcji, domyślnie nowy dokument jest generowana w bazie danych, z automatycznie generowanym identyfikatorze GUID jako hello dokumentu identyfikatora. Identyfikator dokumentu hello dokumentu wyjściowego można określić, podając hello `id` właściwości JSON w hello parametru wyjściowego. 

>[!Note]  
>Po określeniu Identyfikatora hello istniejącego dokumentu zostaje zastąpiona przez hello nowy dokument danych wyjściowych. 

toooutput wielu dokumentów, możesz także powiązać zbyt`ICollector<T>` lub `IAsyncCollector<T>` gdzie `T` hello obsługiwanych typów.

<a name="outputsample"></a>

## <a name="documentdb-api-output-binding-sample"></a>Przykładowe powiązania danych wyjściowych interfejsu API usługi DocumentDB
Załóżmy, że masz następujące hello interfejsu API usługi DocumentDB output powiązanie w hello `bindings` tablicy function.json:

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

I mają powiązania wejściowego kolejki dla kolejki, która odbiera JSON w hello następującego formatu:

```json
{
  "name": "John Henry",
  "employeeId": "123456",
  "address": "A town nearby"
}
```

I mają toocreate dokumenty DB rozwiązania Cosmos w następującego formatu dla każdego rekordu hello:

```json
{
  "id": "John Henry-123456",
  "name": "John Henry",
  "employeeId": "123456",
  "address": "A town nearby"
}
```

Zobacz przykład specyficzny dla języka hello, który używa tej bazy danych wyjściowych powiązania tooadd dokumenty tooyour danych.

* [C#](#outcsharp)
* [F#](#outfsharp)
* [JavaScript](#outjavascript)

<a name="outcsharp"></a>

### <a name="output-sample-in-c"></a>Przykładowe dane wyjściowe w języku C# #

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

### <a name="output-sample-in-f"></a>Przykładowe dane wyjściowe w języku F # #

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

W tym przykładzie wymaga `project.json` pliku, który określa hello `FSharp.Interop.Dynamic` i `Dynamitey` zależności NuGet:

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

tooadd `project.json` plików, zobacz [zarządzania pakietami F #](functions-reference-fsharp.md#package).

<a name="outjavascript"></a>

### <a name="output-sample-in-javascript"></a>Przykładowe dane wyjściowe w języku JavaScript

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
