---
title: "aaaAzure funkcje kolejki magazynu powiązania | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak wyzwala toouse usługi Azure Storage i powiązania usługi Azure Functions."
services: functions
documentationcenter: na
author: lindydonna
manager: erikre
editor: 
tags: 
keywords: "funkcje usługi Azure, funkcje, przetwarzania zdarzeń, dynamiczne obliczeń niekorzystającą architektury"
ms.assetid: 4e6a837d-e64f-45a0-87b7-aa02688a75f3
ms.service: functions
ms.devlang: multiple
ms.topic: reference
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 05/30/2017
ms.author: glenga
ms.openlocfilehash: 438b4f63e823149072c86fdefa7e15bfd2a2c4df
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-functions-queue-storage-bindings"></a>Powiązania funkcji magazynu kolejek Azure
[!INCLUDE [functions-selector-bindings](../../includes/functions-selector-bindings.md)]

W tym artykule opisano sposób tooconfigure i kod powiązania magazynu kolejek Azure w funkcji platformy Azure. Usługi Azure Functions obsługuje uruchomić i dane wyjściowe powiązań dla kolejek platformy Azure. Na temat funkcji, które są dostępne w wszystkie powiązania [usługi Azure Functions wyzwalaczy i powiązań pojęcia](functions-triggers-bindings.md).

[!INCLUDE [intro](../../includes/functions-bindings-intro.md)]

<a name="trigger"></a>

## <a name="queue-storage-trigger"></a>Kolejki magazynu wyzwalacza
wyzwalacz magazynu kolejek Azure Hello umożliwia toomonitor magazynu kolejek, nowe wiadomości i reagowania toothem. 

Zdefiniuj wyzwalacz kolejki przy użyciu hello **integracji** kartę w hello funkcje portalu. Witaj portal tworzy powitania po definicji w hello **powiązania** sekcji *function.json*:

```json
{
    "type": "queueTrigger",
    "direction": "in",
    "name": "<hello name used tooidentify hello trigger data in your code>",
    "queueName": "<Name of queue toopoll>",
    "connection":"<Name of app setting - see below>"
}
```

* Witaj `connection` właściwości musi zawierać nazwę hello ustawienia aplikacji, która zawiera parametry połączenia magazynu. W portalu Azure hello, hello standardowego edytora w hello **integracji** kartę konfiguruje to ustawienie aplikacji, można wybrać konto magazynu.

Można podać dodatkowe ustawienia w [pliku host.json](https://github.com/Azure/azure-webjobs-sdk-script/wiki/host.json) toofurther dostosowywać kolejki magazynu wyzwalaczy. Na przykład można zmienić interwał sondowania kolejki hello w host.json.

<a name="triggerusage"></a>

## <a name="using-a-queue-trigger"></a>Użycie wyzwalacza kolejki
W przypadku funkcji Node.js uzyskiwać dostęp za pomocą danych kolejki hello `context.bindings.<name>`.


W funkcji .NET dostęp hello ładunku kolejki przy użyciu parametru metody, takich jak `CloudQueueMessage paramName`. W tym miejscu `paramName` jest wartością hello określone w hello [konfiguracji wyzwalacza](#trigger). wiadomości powitania kolejki może być zdeserializowany tooany z hello następujące typy:

* Obiekt POCO. Użyj, jeśli ładunek kolejki hello jest obiekt JSON. środowisko uruchomieniowe Functions Hello deserializuje hello ładunku w obiekcie POCO hello. 
* `string`
* `byte[]`
* [`CloudQueueMessage`]

<a name="meta"></a>

### <a name="queue-trigger-metadata"></a>Metadane wyzwalacza kolejki
wyzwalacz kolejki Hello udostępnia kilka właściwości metadanych. Te właściwości mogą służyć jako część wyrażenia powiązania w pozostałych powiązaniach lub parametrów w kodzie. wartości Hello mają hello tej samej semantyki jako [ `CloudQueueMessage` ].

* **QueueTrigger** -ładunku kolejki (jeśli prawidłowy ciąg)
* **DequeueCount** — typ `int`. Witaj, ile razy ten komunikat został usuniętej.
* **ExpirationTime** — typ `DateTimeOffset?`. Witaj czas wygaśnięcia wiadomości powitania.
* **Identyfikator** — typ `string`. Identyfikator kolejki wiadomości.
* **InsertionTime** — typ `DateTimeOffset?`. czas Hello tę wiadomość hello dodano toohello kolejki.
* **NextVisibleTime** — typ `DateTimeOffset?`. czas Hello tę wiadomość hello obok będą widoczne.
* **Elementu PopReceipt** — typ `string`. wiadomości powitania pop potwierdzenia.

Zobacz, jak toouse hello metadanych kolejki w [próbki wyzwalacza](#triggersample).

<a name="triggersample"></a>

## <a name="trigger-sample"></a>Przykładowe wyzwalacza
Załóżmy, że masz powitania po function.json, który definiuje wyzwalacz kolejki:

```json
{
    "disabled": false,
    "bindings": [
        {
            "type": "queueTrigger",
            "direction": "in",
            "name": "myQueueItem",
            "queueName": "myqueue-items",
            "connection":"MyStorageConnectionString"
        }
    ]
}
```

Zobacz przykład specyficzny dla języka hello, który pobiera i rejestruje metadanych kolejki.

* [C#](#triggercsharp)
* [Node.js](#triggernodejs)

<a name="triggercsharp"></a>

### <a name="trigger-sample-in-c"></a>Przykładowe wyzwalacza w języku C# #
```csharp
#r "Microsoft.WindowsAzure.Storage"

using Microsoft.WindowsAzure.Storage.Queue;
using System;

public static void Run(CloudQueueMessage myQueueItem, 
    DateTimeOffset expirationTime, 
    DateTimeOffset insertionTime, 
    DateTimeOffset nextVisibleTime,
    string queueTrigger,
    string id,
    string popReceipt,
    int dequeueCount,
    TraceWriter log)
{
    log.Info($"C# Queue trigger function processed: {myQueueItem.AsString}\n" +
        $"queueTrigger={queueTrigger}\n" +
        $"expirationTime={expirationTime}\n" +
        $"insertionTime={insertionTime}\n" +
        $"nextVisibleTime={nextVisibleTime}\n" +
        $"id={id}\n" +
        $"popReceipt={popReceipt}\n" + 
        $"dequeueCount={dequeueCount}");
}
```

<!--
<a name="triggerfsharp"></a>
### Trigger sample in F# ## 
```fsharp

```
-->

<a name="triggernodejs"></a>

### <a name="trigger-sample-in-nodejs"></a>Przykładowe wyzwalacza w środowisku Node.js

```javascript
module.exports = function (context) {
    context.log('Node.js queue trigger function processed work item', context.bindings.myQueueItem);
    context.log('queueTrigger =', context.bindingData.queueTrigger);
    context.log('expirationTime =', context.bindingData.expirationTime);
    context.log('insertionTime =', context.bindingData.insertionTime);
    context.log('nextVisibleTime =', context.bindingData.nextVisibleTime);
    context.log('id=', context.bindingData.id);
    context.log('popReceipt =', context.bindingData.popReceipt);
    context.log('dequeueCount =', context.bindingData.dequeueCount);
    context.done();
};
```

### <a name="handling-poison-queue-messages"></a>Obsługa wiadomości w kolejce skażone
W przypadku awarii funkcja wyzwalacza kolejki usługi Azure Functions ponowi próbę tej funkcji w górę toofive razy dla danej kolejki wiadomości, tym hello najpierw spróbować. Jeśli nie wszystkie próby pięć, środowisko uruchomieniowe functions hello dodaje magazynu kolejek tooa komunikatu o nazwie  *&lt;originalqueuename >-skażone*. Można napisać tooprocess funkcji wiadomości z kolejki skażone hello rejestrowania ich lub wysyłania powiadomienia, że wymagana jest ręczne uwagi. 

skażone wiadomości toohandle ręcznie, sprawdź hello `dequeueCount` hello kolejki wiadomości (zobacz [kolejki wyzwalacza metadanych](#meta)).

<a name="output"></a>

## <a name="queue-storage-output-binding"></a>Magazyn kolejek powiązania wyjściowego
Powiązanie umożliwia toowrite wiadomości tooa kolejki danych wyjściowych Hello magazynu kolejek Azure. 

Zdefiniuj kolejki powiązania wyjściowego przy użyciu hello **integracji** kartę w hello funkcje portalu. Witaj portal tworzy powitania po definicji w hello **powiązania** sekcji *function.json*:

```json
{
   "type": "queue",
   "direction": "out",
   "name": "<hello name used tooidentify hello trigger data in your code>",
   "queueName": "<Name of queue toowrite to>",
   "connection":"<Name of app setting - see below>"
}
```

* Witaj `connection` właściwości musi zawierać nazwę hello ustawienia aplikacji, która zawiera parametry połączenia magazynu. W portalu Azure hello, hello standardowego edytora w hello **integracji** kartę konfiguruje to ustawienie aplikacji, można wybrać konto magazynu.

<a name="outputusage"></a>

## <a name="using-a-queue-output-binding"></a>Przy użyciu kolejki powiązania wyjściowego
W przypadku funkcji Node.js dostęp przy użyciu kolejki danych wyjściowych hello `context.bindings.<name>`.

W przypadku funkcji .NET dane wyjściowe tooany hello następujące typy. Po parametrze typu `T`, `T` musi mieć jedną z hello obsługiwane typy danych wyjściowych, takich jak `string` lub POCO.

* `out T`(zserializowanym w formacie JSON)
* `out string`
* `out byte[]`
* `out` [`CloudQueueMessage`] 
* `ICollector<T>`
* `IAsyncCollector<T>`
* [`CloudQueue`](/dotnet/api/microsoft.windowsazure.storage.queue.cloudqueue)

Zwracany typ metody hello można także używać jako hello powiązania wyjściowego.

<a name="outputsample"></a>

## <a name="queue-output-sample"></a>Przykładowe dane wyjściowe kolejki
następujące Hello *function.json* definiuje wyzwalacza HTTP z kolejki powiązania wyjściowego:

```json
{
  "bindings": [
    {
      "type": "httpTrigger",
      "direction": "in",
      "authLevel": "function",
      "name": "input"
    },
    {
      "type": "http",
      "direction": "out",
      "name": "return"
    },
    {
      "type": "queue",
      "direction": "out",
      "name": "$return",
      "queueName": "outqueue",
      "connection": "MyStorageConnectionString",
    }
  ]
}
``` 

Zobacz hello próbki specyficzny dla języka, który wyprowadza kolejki wiadomość hello przychodzące ładunku HTTP.

* [C#](#outcsharp)
* [Node.js](#outnodejs)

<a name="outcsharp"></a>

### <a name="queue-output-sample-in-c"></a>Przykładowe dane wyjściowe kolejek w języku C# #

```cs
// C# example of HTTP trigger binding tooa custom POCO, with a queue output binding
public class CustomQueueMessage
{
    public string PersonName { get; set; }
    public string Title { get; set; }
}

public static CustomQueueMessage Run(CustomQueueMessage input, TraceWriter log)
{
    return input;
}
```

Użyj wielu wiadomości toosend `ICollector`:

```cs
public static void Run(CustomQueueMessage input, ICollector<CustomQueueMessage> myQueueItem, TraceWriter log)
{
    myQueueItem.Add(input);
    myQueueItem.Add(new CustomQueueMessage { PersonName = "You", Title = "None" });
}
```

<a name="outnodejs"></a>

### <a name="queue-output-sample-in-nodejs"></a>Przykładowe dane wyjściowe kolejki w środowisku Node.js

```javascript
module.exports = function (context, input) {
    context.done(null, input.body);
};
```

Lub toosend wiele komunikatów

```javascript
module.exports = function(context) {
    // Define a message array for hello myQueueItem output binding. 
    context.bindings.myQueueItem = ["message 1","message 2"];
    context.done();
};
```

## <a name="next-steps"></a>Następne kroki

Na przykład funkcja, która używa kolejki magazynu wyzwalaczy i powiązań zobacz [utworzyć tooan funkcji platformy Azure połączona usługa Azure](functions-create-an-azure-connected-function.md).

[!INCLUDE [next steps](../../includes/functions-bindings-next-steps.md)]

<!-- LINKS -->

["CloudQueueMessage"]: /dotnet/api/microsoft.windowsazure.storage.queue.cloudqueuemessage
