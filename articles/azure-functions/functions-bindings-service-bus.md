---
title: "Funkcje usługi Service Bus aaaAzure wyzwalaczy i powiązań | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak wyzwala toouse Azure Service Bus i powiązania usługi Azure Functions."
services: functions
documentationcenter: na
author: christopheranderson
manager: erikre
editor: 
tags: 
keywords: "funkcje usługi Azure, funkcje, przetwarzania zdarzeń, dynamiczne obliczeń niekorzystającą architektury"
ms.assetid: daedacf0-6546-4355-a65c-50873e74f66b
ms.service: functions
ms.devlang: multiple
ms.topic: reference
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 04/01/2017
ms.author: glenga
ms.openlocfilehash: dff9e89bd3840b8c11f91cae41e13502afc7aa60
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-functions-service-bus-bindings"></a>Azure powiązania funkcji usługi Service Bus
[!INCLUDE [functions-selector-bindings](../../includes/functions-selector-bindings.md)]

W tym artykule opisano sposób tooconfigure i korzystanie z usługi Azure Service Bus powiązania usługi Azure Functions. 

Usługi Azure Functions obsługuje uruchomić i dane wyjściowe powiązania dla tematów i kolejek usługi Service Bus.

[!INCLUDE [intro](../../includes/functions-bindings-intro.md)]

<a name="trigger"></a>

## <a name="service-bus-trigger"></a>Wyzwalacz usługi Service Bus
Użyj hello usługi Service Bus wyzwalacza toorespond toomessages z kolejki usługi Service Bus lub temat. 

Witaj wyzwalacze kolejki i tematu usługi Service Bus są definiowane przez następujące obiekty JSON w hello hello `bindings` tablicy function.json:

* *kolejka* wyzwalacz:

    ```json
    {
        "name" : "<Name of input parameter in function signature>",
        "queueName" : "<Name of hello queue>",
        "connection" : "<Name of app setting that has your queue's connection string - see below>",
        "accessRights" : "<Access rights for hello connection string - see below>",
        "type" : "serviceBusTrigger",
        "direction" : "in"
    }
    ```

* *temat* wyzwalacz:

    ```json
    {
        "name" : "<Name of input parameter in function signature>",
        "topicName" : "<Name of hello topic>",
        "subscriptionName" : "<Name of hello subscription>",
        "connection" : "<Name of app setting that has your topic's connection string - see below>",
        "accessRights" : "<Access rights for hello connection string - see below>",
        "type" : "serviceBusTrigger",
        "direction" : "in"
    }
    ```

Należy uwzględnić następujące hello:

* Dla `connection`, [utworzyć ustawienie aplikacji w aplikacji funkcji](functions-how-to-use-azure-function-app-settings.md) zawierającą przestrzeń nazw usługi Service Bus tooyour ciągu połączenia hello, określ nazwę hello ustawienia aplikacji hello w hello `connection` właściwości w wyzwalacz. Uzyskania ciągu połączenia hello wykonując kroki hello pokazywane na [Uzyskiwanie poświadczeń zarządzania hello](../service-bus-messaging/service-bus-dotnet-get-started-with-queues.md#obtain-the-management-credentials).
  Witaj parametry połączenia muszą mieć dla przestrzeni nazw usługi Service Bus, innymi tooa określonej kolejki lub temat.
  Jeśli opuścisz `connection` określenia domyślnego ciągu połączenia usługi Service Bus w aplikacji, ustawienie o nazwie pusta, zakłada wyzwalacza hello `AzureWebJobsServiceBus`.
* Aby uzyskać `accessRights`, dostępne wartości to `manage` i `listen`. Domyślnie Hello `manage`, co oznacza, że hello `connection` ma hello **Zarządzaj** uprawnienia. Jeśli używasz parametry połączenia, które nie ma hello **Zarządzaj** zestawu uprawnień, `accessRights` zbyt`listen`. W przeciwnym razie hello funkcji środowiska uruchomieniowego może zakończyć się niepowodzeniem w trakcie operacji toodo wymagających zarządzania prawami.

## <a name="trigger-behavior"></a>Zachowanie wyzwalacza
* **Wątkowość jednym** — domyślnie procesy środowiska uruchomieniowego funkcje hello wielu wiadomości jednocześnie. Ustaw toodirect hello środowiska uruchomieniowego tooprocess tylko jednej kolejka lub temat wiadomości w czasie, `serviceBus.maxConcurrentCalls` too1 w *host.json*. 
  Aby uzyskać informacje o *host.json*, zobacz [struktury folderów](functions-reference.md#folder-structure) i [host.json](https://github.com/Azure/azure-webjobs-sdk-script/wiki/host.json).
* **Obsługa komunikatów zanieczyszczonych** -usługi Service Bus jest jego własnej obsługi uszkodzonych komunikatów, który nie może być kontrolowana ani skonfigurowana w konfiguracji usługi Azure Functions lub kod. 
* **Zachowanie PeekLock** — środowisko uruchomieniowe Functions hello odbiera wiadomości w [ `PeekLock` tryb](../service-bus-messaging/service-bus-performance-improvements.md#receive-mode) i wywołania `Complete` na wiadomość powitania, jeśli funkcja hello zakończy działanie pomyślnie, lub wywołania `Abandon` Jeśli hello Operacja zakończy się niepowodzeniem. 
  Jeśli funkcja hello uruchomione dłużej niż hello `PeekLock` limit czasu blokady hello jest automatycznie odnawiane.

<a name="triggerusage"></a>

## <a name="trigger-usage"></a>Użycie wyzwalacza
W tej sekcji przedstawiono, jak toouse Twojego usługi Service Bus wyzwolenia w kodzie funkcji. 

W języku C# i F # hello usługi Service Bus wyzwalacza komunikat może być zdeserializowany tooany z hello następujące typy wejściowe:

* `string`-przydatne w przypadku wiadomości ciąg
* `byte[]`-przydatne dla danych binarnych
* Wszelkie [obiektu](https://msdn.microsoft.com/library/system.object.aspx) — jest to przydatne w przypadku danych serializacji JSON.
  Jeśli niestandardowy typ danych wejściowych, takich jak zadeklarować `CustomType`, usługi Azure Functions próbuje toodeserialize hello JSON danych w sieci określonego typu.
* `BrokeredMessage`— zapewnia hello można przeprowadzić deserializacji wiadomość hello [BrokeredMessage.GetBody<T>()](https://msdn.microsoft.com/library/hh144211.aspx) metody.

W środowisku Node.js komunikat wyzwalacza usługi Service Bus hello jest przekazany do funkcji hello jako ciąg lub obiekt JSON do.

<a name="triggersample"></a>

## <a name="trigger-sample"></a>Przykładowe wyzwalacza
Załóżmy, że masz następujące function.json hello:

```json
{
"bindings": [
    {
    "queueName": "testqueue",
    "connection": "MyServiceBusConnection",
    "name": "myQueueItem",
    "type": "serviceBusTrigger",
    "direction": "in"
    }
],
"disabled": false
}
```

Zobacz hello próbki specyficzny dla języka, który przetwarza komunikat z kolejki usługi Service Bus.

* [C#](#triggercsharp)
* [F#](#triggerfsharp)
* [Node.js](#triggernodejs)

<a name="triggercsharp"></a>

### <a name="trigger-sample-in-c"></a>Przykładowe wyzwalacza w języku C# #

```cs
public static void Run(string myQueueItem, TraceWriter log)
{
    log.Info($"C# ServiceBus queue trigger function processed message: {myQueueItem}");
}
```

<a name="triggerfsharp"></a>

### <a name="trigger-sample-in-f"></a>Przykładowe wyzwalacza w języku F # #

```fsharp
let Run(myQueueItem: string, log: TraceWriter) =
    log.Info(sprintf "F# ServiceBus queue trigger function processed message: %s" myQueueItem)
```

<a name="triggernodejs"></a>

### <a name="trigger-sample-in-nodejs"></a>Przykładowe wyzwalacza w środowisku Node.js

```javascript
module.exports = function(context, myQueueItem) {
    context.log('Node.js ServiceBus queue trigger function processed message', myQueueItem);
    context.done();
};
```

<a name="output"></a>

## <a name="service-bus-output-binding"></a>Powiązania wyjściowego usługi Service Bus
Hello wyjściowego kolejek i tematów usługi Service Bus dla funkcji Użyj hello następujące obiekty JSON w hello `bindings` tablicy function.json:

* *kolejka* danych wyjściowych:

    ```json
    {
        "name" : "<Name of output parameter in function signature>",
        "queueName" : "<Name of hello queue>",
        "connection" : "<Name of app setting that has your queue's connection string - see below>",
        "accessRights" : "<Access rights for hello connection string - see below>",
        "type" : "serviceBus",
        "direction" : "out"
    }
    ```
* *temat* danych wyjściowych:

    ```json
    {
        "name" : "<Name of output parameter in function signature>",
        "topicName" : "<Name of hello topic>",
        "subscriptionName" : "<Name of hello subscription>",
        "connection" : "<Name of app setting that has your topic's connection string - see below>",
        "accessRights" : "<Access rights for hello connection string - see below>",
        "type" : "serviceBus",
        "direction" : "out"
    }
    ```

Należy uwzględnić następujące hello:

* Dla `connection`, [utworzyć ustawienie aplikacji w aplikacji funkcji](functions-how-to-use-azure-function-app-settings.md) zawierającą przestrzeń nazw usługi Service Bus tooyour ciągu połączenia hello, określ nazwę hello ustawienia aplikacji hello w hello `connection` właściwości w danych wyjściowych wiązanie. Uzyskania ciągu połączenia hello wykonując kroki hello pokazywane na [Uzyskiwanie poświadczeń zarządzania hello](../service-bus-messaging/service-bus-dotnet-get-started-with-queues.md#obtain-the-management-credentials).
  Witaj parametry połączenia muszą mieć dla przestrzeni nazw usługi Service Bus, innymi tooa określonej kolejki lub temat.
  Jeśli opuścisz `connection` pusta, hello powiązania wyjściowego przyjęto założenie, że domyślnego ciągu połączenia magistrali usług jest określona w aplikacji, ustawienie o nazwie `AzureWebJobsServiceBus`.
* Aby uzyskać `accessRights`, dostępne wartości to `manage` i `listen`. Domyślnie Hello `manage`, co oznacza, że hello `connection` ma hello **Zarządzaj** uprawnienia. Jeśli używasz parametry połączenia, które nie ma hello **Zarządzaj** zestawu uprawnień, `accessRights` zbyt`listen`. W przeciwnym razie hello funkcji środowiska uruchomieniowego może zakończyć się niepowodzeniem w trakcie operacji toodo wymagających zarządzania prawami.

<a name="outputusage"></a>

## <a name="output-usage"></a>Użycie danych wyjściowych
W języku C# i F # usługi Azure Functions można utworzyć komunikat z kolejki usługi Service Bus za pomocą dowolnego hello następujące typy:

* Wszelkie [obiektu](https://msdn.microsoft.com/library/system.object.aspx) — definicja parametru wygląda `out T paramName` (C#).
  Funkcje deserializuje obiekt hello do wiadomości w formacie JSON. Jeśli wartość wyjściowa hello ma wartość null, gdy funkcja hello jest kończona, funkcje tworzy wiadomość hello z obiektem null.
* `string`-Definicja parametru wygląda `out string paraName` (C#). Jeśli wartość parametru hello jest różna od null, gdy funkcja hello jest kończona, funkcje tworzy komunikat.
* `byte[]`-Definicja parametru wygląda `out byte[] paraName` (C#). Jeśli wartość parametru hello jest różna od null, gdy funkcja hello jest kończona, funkcje tworzy komunikat.
* `BrokeredMessage`Definicja parametru wygląda `out BrokeredMessage paraName` (C#). Jeśli wartość parametru hello jest różna od null, gdy funkcja hello jest kończona, funkcje tworzy komunikat.

W przypadku tworzenia wielu wiadomości w funkcji języka C#, można użyć `ICollector<T>` lub `IAsyncCollector<T>`. Komunikat jest tworzony podczas wywoływania hello `Add` metody.

W środowisku Node.js, można przypisać ciąg, tablica bajtów lub obiekt Javascript (deserializacji do postaci JSON) zbyt`context.binding.<paramName>`.

<a name="outputsample"></a>

## <a name="output-sample"></a>Przykładowe dane wyjściowe
Załóżmy, że masz następujące function.json hello definiuje wyjściowego kolejki usługi Service Bus:

```json
{
    "bindings": [
        {
            "schedule": "0/15 * * * * *",
            "name": "myTimer",
            "runsOnStartup": true,
            "type": "timerTrigger",
            "direction": "in"
        },
        {
            "name": "outputSbQueue",
            "type": "serviceBus",
            "queueName": "testqueue",
            "connection": "MyServiceBusConnection",
            "direction": "out"
        }
    ],
    "disabled": false
}
```

Zobacz przykład specyficzny dla języka hello, który wysyła wiadomości toohello kolejką usługi service bus.

* [C#](#outcsharp)
* [F#](#outfsharp)
* [Node.js](#outnodejs)

<a name="outcsharp"></a>

### <a name="output-sample-in-c"></a>Przykładowe dane wyjściowe w języku C# #

```cs
public static void Run(TimerInfo myTimer, TraceWriter log, out string outputSbQueue)
{
    string message = $"Service Bus queue message created at: {DateTime.Now}";
    log.Info(message); 
    outputSbQueue = message;
}
```

Lub toocreate wiele komunikatów:

```cs
public static void Run(TimerInfo myTimer, TraceWriter log, ICollector<string> outputSbQueue)
{
    string message = $"Service Bus queue message created at: {DateTime.Now}";
    log.Info(message); 
    outputSbQueue.Add("1 " + message);
    outputSbQueue.Add("2 " + message);
}
```

<a name="outfsharp"></a>

### <a name="output-sample-in-f"></a>Przykładowe dane wyjściowe w języku F # #

```fsharp
let Run(myTimer: TimerInfo, log: TraceWriter, outputSbQueue: byref<string>) =
    let message = sprintf "Service Bus queue message created at: %s" (DateTime.Now.ToString())
    log.Info(message)
    outputSbQueue = message
```

<a name="outnodejs"></a>

### <a name="output-sample-in-nodejs"></a>Przykładowe dane wyjściowe w środowisku Node.js

```javascript
module.exports = function (context, myTimer) {
    var message = 'Service Bus queue message created at ' + timeStamp;
    context.log(message);   
    context.bindings.outputSbQueueMsg = message;
    context.done();
};
```

Lub toocreate wiele komunikatów:

```javascript
module.exports = function (context, myTimer) {
    var message = 'Service Bus queue message created at ' + timeStamp;
    context.log(message);   
    context.bindings.outputSbQueueMsg = [];
    context.bindings.outputSbQueueMsg.push("1 " + message);
    context.bindings.outputSbQueueMsg.push("2 " + message);
    context.done();
};
```

## <a name="next-steps"></a>Następne kroki
[!INCLUDE [next steps](../../includes/functions-bindings-next-steps.md)]

