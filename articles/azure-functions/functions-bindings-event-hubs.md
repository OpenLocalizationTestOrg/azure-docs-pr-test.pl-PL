---
title: "powiązania funkcji Event Hubs aaaAzure | Dokumentacja firmy Microsoft"
description: "Zrozumienie sposobu toouse powiązań usługi Azure Event Hubs w funkcji platformy Azure."
services: functions
documentationcenter: na
author: wesmc7777
manager: erikre
editor: 
tags: 
keywords: "funkcje usługi Azure, funkcje, przetwarzania zdarzeń, dynamiczne obliczeń niekorzystającą architektury"
ms.assetid: daf81798-7acc-419a-bc32-b5a41c6db56b
ms.service: functions
ms.devlang: multiple
ms.topic: reference
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 06/20/2017
ms.author: wesmc
ms.openlocfilehash: e864f032ad5ac58d318c9843c3844b5642733a70
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-functions-event-hubs-bindings"></a>Azure powiązania centra zdarzeń funkcji
[!INCLUDE [functions-selector-bindings](../../includes/functions-selector-bindings.md)]

W tym artykule opisano sposób tooconfigure i użyj [Azure Event Hubs](../event-hubs/event-hubs-what-is-event-hubs.md) powiązania dla usługi Azure Functions.
Usługi Azure Functions obsługuje uruchomić i dane wyjściowe powiązania usługi Event hubs.

[!INCLUDE [intro](../../includes/functions-bindings-intro.md)]

Jeśli nowy tooAzure Event Hubs, zobacz hello [Przegląd usługi Event Hubs](../event-hubs/event-hubs-what-is-event-hubs.md).

<a name="trigger"></a>

## <a name="event-hub-trigger"></a>Wyzwalacz Centrum zdarzeń
Centra zdarzeń hello Użyj wyzwala zdarzenia tooan toorespond wysyłane strumienia zdarzeń w Centrum zdarzeń tooan. Musi mieć dostęp do odczytu toohello zdarzenia koncentratora tooset się hello wyzwalacza.

wyzwalacz funkcji usługi Event Hubs Hello wykorzystuje powitania po obiekt JSON w hello `bindings` tablicy function.json:

```json
{
    "type": "eventHubTrigger",
    "name": "<Name of trigger parameter in function signature>",
    "direction": "in",
    "path": "<Name of hello event hub>",
    "consumerGroup": "Consumer group toouse - see below",
    "connection": "<Name of app setting with connection string - see below>"
}
```

`consumerGroup`jest opcjonalna właściwość używane tooset hello [grupy odbiorców](../event-hubs/event-hubs-features.md#event-consumers) używane toosubscribe tooevents hello Centrum. Witaj w przypadku jego pominięcia `$Default` służy grupy odbiorców.  
`connection`musi być nazwą hello ustawienia aplikacji, które zawiera hello połączenia ciąg toohello Centrum zdarzeń w przestrzeni nazw.
Skopiować te parametry połączenia, klikając hello **informacje o połączeniu** przycisk hello *przestrzeni nazw*, nie Centrum zdarzeń hello, samej siebie. Ten ciąg połączenia musi mieć co najmniej odczytu uprawnienia tooactivate hello wyzwalacza.

[Dodatkowe ustawienia](https://github.com/Azure/azure-webjobs-sdk-script/wiki/host.json) można podać w host.json pliku toofurther poprawnie dostroić wyzwalaczy usługi Event Hubs.  

<a name="triggerusage"></a>

## <a name="trigger-usage"></a>Użycie wyzwalacza
Po wyzwoleniu funkcja wyzwalacza usługi Event Hubs wiadomość hello je uruchamia jest przekazany do funkcji hello jako ciąg.

<a name="triggersample"></a>

## <a name="trigger-sample"></a>Przykładowe wyzwalacza
Załóżmy, że masz hello wyzwalacz następujące centra zdarzeń w hello `bindings` tablicy function.json:

```json
{
  "type": "eventHubTrigger",
  "name": "myEventHubMessage",
  "direction": "in",
  "path": "MyEventHub",
  "connection": "myEventHubReadConnectionString"
}
```

Zobacz przykład specyficzny dla języka hello, który rejestruje treści wiadomości powitania wyzwalacz Centrum zdarzeń hello.

* [C#](#triggercsharp)
* [F#](#triggerfsharp)
* [Node.js](#triggernodejs)

<a name="triggercsharp"></a>

### <a name="trigger-sample-in-c"></a>Przykładowe wyzwalacza w języku C# #

```cs
using System;

public static void Run(string myEventHubMessage, TraceWriter log)
{
    log.Info($"C# Event Hub trigger function processed a message: {myEventHubMessage}");
}
```

Można również odbierać zdarzenia hello [EventData](/dotnet/api/microsoft.servicebus.messaging.eventdata) obiektu, który umożliwia dostęp do metadanych zdarzeń toohello.

```cs
#r "Microsoft.ServiceBus"
using System.Text;
using Microsoft.ServiceBus.Messaging;

public static void Run(EventData myEventHubMessage, TraceWriter log)
{
    log.Info($"{Encoding.UTF8.GetString(myEventHubMessage.GetBytes())}");
}
```

zdarzenia tooreceive w partii, Zmień podpis metody hello zbyt`string[]` lub `EventData[]`.

```cs
public static void Run(string[] eventHubMessages, TraceWriter log)
{
    foreach (var message in eventHubMessages)
    {
        log.Info($"C# Event Hub trigger function processed a message: {message}");
    }
}
```

<a name="triggerfsharp"></a>

### <a name="trigger-sample-in-f"></a>Przykładowe wyzwalacza w języku F # #

```fsharp
let Run(myEventHubMessage: string, log: TraceWriter) =
    log.Info(sprintf "F# eventhub trigger function processed work item: %s" myEventHubMessage)
```

<a name="triggernodejs"></a>

### <a name="trigger-sample-in-nodejs"></a>Przykładowe wyzwalacza w środowisku Node.js

```javascript
module.exports = function (context, myEventHubMessage) {
    context.log('Node.js eventhub trigger function processed work item', myEventHubMessage);    
    context.done();
};
```

<a name="output"></a>

## <a name="event-hubs-output-binding"></a>Centra zdarzeń powiązania wyjściowego
Użyj hello centra zdarzeń w danych wyjściowych zdarzenia toowrite powiązania tooan strumienia zdarzeń Centrum zdarzeń. Musi mieć tooit zdarzenia toowrite wysyłania uprawnienia tooan zdarzenia koncentratora.

Witaj powiązania wyjściowego używa powitania po obiekt JSON w hello `bindings` tablicy function.json:

```json
{
    "type": "eventHub",
    "name": "<Name of output parameter in function signature>",
    "path": "<Name of event hub>",
    "connection": "<Name of app setting with connection string - see below>"
    "direction": "out"
}
```

`connection`musi być nazwą hello ustawienia aplikacji, które zawiera hello połączenia ciąg toohello Centrum zdarzeń w przestrzeni nazw.
Skopiować te parametry połączenia, klikając hello **informacje o połączeniu** przycisk hello *przestrzeni nazw*, nie Centrum zdarzeń hello, samej siebie. Ten ciąg połączenia musi mieć strumienia zdarzeń toohello wiadomość hello wysyłania uprawnienia toosend.

## <a name="output-usage"></a>Użycie danych wyjściowych
W tej sekcji przedstawiono, jak toouse centrów zdarzeń output powiązania w kodzie funkcji.

Można danych wyjściowych Centrum zdarzeń toohello skonfigurowane wiadomości z hello następujące typy parametrów:

* `out string`
* `ICollector<string>`(toooutput wiele komunikatów)
* `IAsyncCollector<string>`(wersja async `ICollector<T>`)

<a name="outputsample"></a>

## <a name="output-sample"></a>Przykładowe dane wyjściowe
Załóżmy, że masz następujące hello centra zdarzeń w danych wyjściowych powiązanie w hello `bindings` tablicy function.json:

```json
{
    "type": "eventHub",
    "name": "outputEventHubMessage",
    "path": "myeventhub",
    "connection": "MyEventHubSend",
    "direction": "out"
}
```

Zobacz przykład specyficzny dla języka hello, który zapisuje zdarzenia toohello nawet strumienia.

* [C#](#outcsharp)
* [F#](#outfsharp)
* [Node.js](#outnodejs)

<a name="outcsharp"></a>

### <a name="output-sample-in-c"></a>Przykładowe dane wyjściowe w języku C# #

```cs
using System;

public static void Run(TimerInfo myTimer, out string outputEventHubMessage, TraceWriter log)
{
    String msg = $"TimerTriggerCSharp1 executed at: {DateTime.Now}";
    log.Verbose(msg);   
    outputEventHubMessage = msg;
}
```

Lub toocreate wiele komunikatów:

```cs
public static void Run(TimerInfo myTimer, ICollector<string> outputEventHubMessage, TraceWriter log)
{
    string message = $"Event Hub message created at: {DateTime.Now}";
    log.Info(message);
    outputEventHubMessage.Add("1 " + message);
    outputEventHubMessage.Add("2 " + message);
}
```

<a name="outfsharp"></a>

### <a name="output-sample-in-f"></a>Przykładowe dane wyjściowe w języku F # #

```fsharp
let Run(myTimer: TimerInfo, outputEventHubMessage: byref<string>, log: TraceWriter) =
    let msg = sprintf "TimerTriggerFSharp1 executed at: %s" DateTime.Now.ToString()
    log.Verbose(msg);
    outputEventHubMessage <- msg;
```

<a name="outnodejs"></a>

### <a name="output-sample-for-nodejs"></a>Przykładowe dane wyjściowe dla środowiska Node.js

```javascript
module.exports = function (context, myTimer) {
    var timeStamp = new Date().toISOString();
    context.log('Event Hub message created at: ', timeStamp);   
    context.bindings.outputEventHubMessage = "Event Hub message created at: " + timeStamp;
    context.done();
};
```

Lub toosend wiele komunikatów

```javascript
module.exports = function(context) {
    var timeStamp = new Date().toISOString();
    var message = 'Event Hub message created at: ' + timeStamp;

    context.bindings.outputEventHubMessage = [];

    context.bindings.outputEventHubMessage.push("1 " + message);
    context.bindings.outputEventHubMessage.push("2 " + message);
    context.done();
};
```

## <a name="next-steps"></a>Następne kroki
[!INCLUDE [next steps](../../includes/functions-bindings-next-steps.md)]
