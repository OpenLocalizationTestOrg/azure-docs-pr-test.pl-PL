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
# <a name="azure-functions-event-hubs-bindings"></a><span data-ttu-id="ca3cd-104">Azure powiązania centra zdarzeń funkcji</span><span class="sxs-lookup"><span data-stu-id="ca3cd-104">Azure Functions Event Hubs bindings</span></span>
[!INCLUDE [functions-selector-bindings](../../includes/functions-selector-bindings.md)]

<span data-ttu-id="ca3cd-105">W tym artykule opisano sposób tooconfigure i użyj [Azure Event Hubs](../event-hubs/event-hubs-what-is-event-hubs.md) powiązania dla usługi Azure Functions.</span><span class="sxs-lookup"><span data-stu-id="ca3cd-105">This article explains how tooconfigure and use [Azure Event Hubs](../event-hubs/event-hubs-what-is-event-hubs.md) bindings for Azure Functions.</span></span>
<span data-ttu-id="ca3cd-106">Usługi Azure Functions obsługuje uruchomić i dane wyjściowe powiązania usługi Event hubs.</span><span class="sxs-lookup"><span data-stu-id="ca3cd-106">Azure Functions supports trigger and output bindings for Event Hubs.</span></span>

[!INCLUDE [intro](../../includes/functions-bindings-intro.md)]

<span data-ttu-id="ca3cd-107">Jeśli nowy tooAzure Event Hubs, zobacz hello [Przegląd usługi Event Hubs](../event-hubs/event-hubs-what-is-event-hubs.md).</span><span class="sxs-lookup"><span data-stu-id="ca3cd-107">If you are new tooAzure Event Hubs, see hello [Event Hubs overview](../event-hubs/event-hubs-what-is-event-hubs.md).</span></span>

<a name="trigger"></a>

## <a name="event-hub-trigger"></a><span data-ttu-id="ca3cd-108">Wyzwalacz Centrum zdarzeń</span><span class="sxs-lookup"><span data-stu-id="ca3cd-108">Event hub trigger</span></span>
<span data-ttu-id="ca3cd-109">Centra zdarzeń hello Użyj wyzwala zdarzenia tooan toorespond wysyłane strumienia zdarzeń w Centrum zdarzeń tooan.</span><span class="sxs-lookup"><span data-stu-id="ca3cd-109">Use hello Event Hubs trigger toorespond tooan event sent tooan event hub event stream.</span></span> <span data-ttu-id="ca3cd-110">Musi mieć dostęp do odczytu toohello zdarzenia koncentratora tooset się hello wyzwalacza.</span><span class="sxs-lookup"><span data-stu-id="ca3cd-110">You must have read access toohello event hub tooset up hello trigger.</span></span>

<span data-ttu-id="ca3cd-111">wyzwalacz funkcji usługi Event Hubs Hello wykorzystuje powitania po obiekt JSON w hello `bindings` tablicy function.json:</span><span class="sxs-lookup"><span data-stu-id="ca3cd-111">hello Event Hubs function trigger uses hello following JSON object in hello `bindings` array of function.json:</span></span>

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

<span data-ttu-id="ca3cd-112">`consumerGroup`jest opcjonalna właściwość używane tooset hello [grupy odbiorców](../event-hubs/event-hubs-features.md#event-consumers) używane toosubscribe tooevents hello Centrum.</span><span class="sxs-lookup"><span data-stu-id="ca3cd-112">`consumerGroup` is an optional property used tooset hello [consumer group](../event-hubs/event-hubs-features.md#event-consumers) used toosubscribe tooevents in hello hub.</span></span> <span data-ttu-id="ca3cd-113">Witaj w przypadku jego pominięcia `$Default` służy grupy odbiorców.</span><span class="sxs-lookup"><span data-stu-id="ca3cd-113">If omitted, hello `$Default` consumer group is used.</span></span>  
<span data-ttu-id="ca3cd-114">`connection`musi być nazwą hello ustawienia aplikacji, które zawiera hello połączenia ciąg toohello Centrum zdarzeń w przestrzeni nazw.</span><span class="sxs-lookup"><span data-stu-id="ca3cd-114">`connection` must be hello name of an app setting that contains hello connection string toohello event hub's namespace.</span></span>
<span data-ttu-id="ca3cd-115">Skopiować te parametry połączenia, klikając hello **informacje o połączeniu** przycisk hello *przestrzeni nazw*, nie Centrum zdarzeń hello, samej siebie.</span><span class="sxs-lookup"><span data-stu-id="ca3cd-115">Copy this connection string by clicking hello **Connection Information** button for hello *namespace*, not hello event hub itself.</span></span> <span data-ttu-id="ca3cd-116">Ten ciąg połączenia musi mieć co najmniej odczytu uprawnienia tooactivate hello wyzwalacza.</span><span class="sxs-lookup"><span data-stu-id="ca3cd-116">This connection string must have at least read permissions tooactivate hello trigger.</span></span>

<span data-ttu-id="ca3cd-117">[Dodatkowe ustawienia](https://github.com/Azure/azure-webjobs-sdk-script/wiki/host.json) można podać w host.json pliku toofurther poprawnie dostroić wyzwalaczy usługi Event Hubs.</span><span class="sxs-lookup"><span data-stu-id="ca3cd-117">[Additional settings](https://github.com/Azure/azure-webjobs-sdk-script/wiki/host.json) can be provided in a host.json file toofurther fine tune Event Hubs triggers.</span></span>  

<a name="triggerusage"></a>

## <a name="trigger-usage"></a><span data-ttu-id="ca3cd-118">Użycie wyzwalacza</span><span class="sxs-lookup"><span data-stu-id="ca3cd-118">Trigger usage</span></span>
<span data-ttu-id="ca3cd-119">Po wyzwoleniu funkcja wyzwalacza usługi Event Hubs wiadomość hello je uruchamia jest przekazany do funkcji hello jako ciąg.</span><span class="sxs-lookup"><span data-stu-id="ca3cd-119">When an Event Hubs trigger function is triggered, hello message that triggers it is passed into hello function as a string.</span></span>

<a name="triggersample"></a>

## <a name="trigger-sample"></a><span data-ttu-id="ca3cd-120">Przykładowe wyzwalacza</span><span class="sxs-lookup"><span data-stu-id="ca3cd-120">Trigger sample</span></span>
<span data-ttu-id="ca3cd-121">Załóżmy, że masz hello wyzwalacz następujące centra zdarzeń w hello `bindings` tablicy function.json:</span><span class="sxs-lookup"><span data-stu-id="ca3cd-121">Suppose you have hello following Event Hubs trigger in hello `bindings` array of function.json:</span></span>

```json
{
  "type": "eventHubTrigger",
  "name": "myEventHubMessage",
  "direction": "in",
  "path": "MyEventHub",
  "connection": "myEventHubReadConnectionString"
}
```

<span data-ttu-id="ca3cd-122">Zobacz przykład specyficzny dla języka hello, który rejestruje treści wiadomości powitania wyzwalacz Centrum zdarzeń hello.</span><span class="sxs-lookup"><span data-stu-id="ca3cd-122">See hello language-specific sample that logs hello message body of hello event hub trigger.</span></span>

* [<span data-ttu-id="ca3cd-123">C#</span><span class="sxs-lookup"><span data-stu-id="ca3cd-123">C#</span></span>](#triggercsharp)
* [<span data-ttu-id="ca3cd-124">F#</span><span class="sxs-lookup"><span data-stu-id="ca3cd-124">F#</span></span>](#triggerfsharp)
* [<span data-ttu-id="ca3cd-125">Node.js</span><span class="sxs-lookup"><span data-stu-id="ca3cd-125">Node.js</span></span>](#triggernodejs)

<a name="triggercsharp"></a>

### <a name="trigger-sample-in-c"></a><span data-ttu-id="ca3cd-126">Przykładowe wyzwalacza w języku C#</span><span class="sxs-lookup"><span data-stu-id="ca3cd-126">Trigger sample in C#</span></span> #

```cs
using System;

public static void Run(string myEventHubMessage, TraceWriter log)
{
    log.Info($"C# Event Hub trigger function processed a message: {myEventHubMessage}");
}
```

<span data-ttu-id="ca3cd-127">Można również odbierać zdarzenia hello [EventData](/dotnet/api/microsoft.servicebus.messaging.eventdata) obiektu, który umożliwia dostęp do metadanych zdarzeń toohello.</span><span class="sxs-lookup"><span data-stu-id="ca3cd-127">You can also receive hello event as an [EventData](/dotnet/api/microsoft.servicebus.messaging.eventdata) object, which gives you access toohello event metadata.</span></span>

```cs
#r "Microsoft.ServiceBus"
using System.Text;
using Microsoft.ServiceBus.Messaging;

public static void Run(EventData myEventHubMessage, TraceWriter log)
{
    log.Info($"{Encoding.UTF8.GetString(myEventHubMessage.GetBytes())}");
}
```

<span data-ttu-id="ca3cd-128">zdarzenia tooreceive w partii, Zmień podpis metody hello zbyt`string[]` lub `EventData[]`.</span><span class="sxs-lookup"><span data-stu-id="ca3cd-128">tooreceive events in a batch, change hello method signature too`string[]` or `EventData[]`.</span></span>

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

### <a name="trigger-sample-in-f"></a><span data-ttu-id="ca3cd-129">Przykładowe wyzwalacza w języku F #</span><span class="sxs-lookup"><span data-stu-id="ca3cd-129">Trigger sample in F#</span></span> #

```fsharp
let Run(myEventHubMessage: string, log: TraceWriter) =
    log.Info(sprintf "F# eventhub trigger function processed work item: %s" myEventHubMessage)
```

<a name="triggernodejs"></a>

### <a name="trigger-sample-in-nodejs"></a><span data-ttu-id="ca3cd-130">Przykładowe wyzwalacza w środowisku Node.js</span><span class="sxs-lookup"><span data-stu-id="ca3cd-130">Trigger sample in Node.js</span></span>

```javascript
module.exports = function (context, myEventHubMessage) {
    context.log('Node.js eventhub trigger function processed work item', myEventHubMessage);    
    context.done();
};
```

<a name="output"></a>

## <a name="event-hubs-output-binding"></a><span data-ttu-id="ca3cd-131">Centra zdarzeń powiązania wyjściowego</span><span class="sxs-lookup"><span data-stu-id="ca3cd-131">Event Hubs output binding</span></span>
<span data-ttu-id="ca3cd-132">Użyj hello centra zdarzeń w danych wyjściowych zdarzenia toowrite powiązania tooan strumienia zdarzeń Centrum zdarzeń.</span><span class="sxs-lookup"><span data-stu-id="ca3cd-132">Use hello Event Hubs output binding toowrite events tooan event hub event stream.</span></span> <span data-ttu-id="ca3cd-133">Musi mieć tooit zdarzenia toowrite wysyłania uprawnienia tooan zdarzenia koncentratora.</span><span class="sxs-lookup"><span data-stu-id="ca3cd-133">You must have send permission tooan event hub toowrite events tooit.</span></span>

<span data-ttu-id="ca3cd-134">Witaj powiązania wyjściowego używa powitania po obiekt JSON w hello `bindings` tablicy function.json:</span><span class="sxs-lookup"><span data-stu-id="ca3cd-134">hello output binding uses hello following JSON object in hello `bindings` array of function.json:</span></span>

```json
{
    "type": "eventHub",
    "name": "<Name of output parameter in function signature>",
    "path": "<Name of event hub>",
    "connection": "<Name of app setting with connection string - see below>"
    "direction": "out"
}
```

<span data-ttu-id="ca3cd-135">`connection`musi być nazwą hello ustawienia aplikacji, które zawiera hello połączenia ciąg toohello Centrum zdarzeń w przestrzeni nazw.</span><span class="sxs-lookup"><span data-stu-id="ca3cd-135">`connection` must be hello name of an app setting that contains hello connection string toohello event hub's namespace.</span></span>
<span data-ttu-id="ca3cd-136">Skopiować te parametry połączenia, klikając hello **informacje o połączeniu** przycisk hello *przestrzeni nazw*, nie Centrum zdarzeń hello, samej siebie.</span><span class="sxs-lookup"><span data-stu-id="ca3cd-136">Copy this connection string by clicking hello **Connection Information** button for hello *namespace*, not hello event hub itself.</span></span> <span data-ttu-id="ca3cd-137">Ten ciąg połączenia musi mieć strumienia zdarzeń toohello wiadomość hello wysyłania uprawnienia toosend.</span><span class="sxs-lookup"><span data-stu-id="ca3cd-137">This connection string must have send permissions toosend hello message toohello event stream.</span></span>

## <a name="output-usage"></a><span data-ttu-id="ca3cd-138">Użycie danych wyjściowych</span><span class="sxs-lookup"><span data-stu-id="ca3cd-138">Output usage</span></span>
<span data-ttu-id="ca3cd-139">W tej sekcji przedstawiono, jak toouse centrów zdarzeń output powiązania w kodzie funkcji.</span><span class="sxs-lookup"><span data-stu-id="ca3cd-139">This section shows you how toouse your Event Hubs output binding in your function code.</span></span>

<span data-ttu-id="ca3cd-140">Można danych wyjściowych Centrum zdarzeń toohello skonfigurowane wiadomości z hello następujące typy parametrów:</span><span class="sxs-lookup"><span data-stu-id="ca3cd-140">You can output messages toohello configured event hub with hello following parameter types:</span></span>

* `out string`
* <span data-ttu-id="ca3cd-141">`ICollector<string>`(toooutput wiele komunikatów)</span><span class="sxs-lookup"><span data-stu-id="ca3cd-141">`ICollector<string>` (toooutput multiple messages)</span></span>
* <span data-ttu-id="ca3cd-142">`IAsyncCollector<string>`(wersja async `ICollector<T>`)</span><span class="sxs-lookup"><span data-stu-id="ca3cd-142">`IAsyncCollector<string>` (async version of `ICollector<T>`)</span></span>

<a name="outputsample"></a>

## <a name="output-sample"></a><span data-ttu-id="ca3cd-143">Przykładowe dane wyjściowe</span><span class="sxs-lookup"><span data-stu-id="ca3cd-143">Output sample</span></span>
<span data-ttu-id="ca3cd-144">Załóżmy, że masz następujące hello centra zdarzeń w danych wyjściowych powiązanie w hello `bindings` tablicy function.json:</span><span class="sxs-lookup"><span data-stu-id="ca3cd-144">Suppose you have hello following Event Hubs output binding in hello `bindings` array of function.json:</span></span>

```json
{
    "type": "eventHub",
    "name": "outputEventHubMessage",
    "path": "myeventhub",
    "connection": "MyEventHubSend",
    "direction": "out"
}
```

<span data-ttu-id="ca3cd-145">Zobacz przykład specyficzny dla języka hello, który zapisuje zdarzenia toohello nawet strumienia.</span><span class="sxs-lookup"><span data-stu-id="ca3cd-145">See hello language-specific sample that writes an event toohello even stream.</span></span>

* [<span data-ttu-id="ca3cd-146">C#</span><span class="sxs-lookup"><span data-stu-id="ca3cd-146">C#</span></span>](#outcsharp)
* [<span data-ttu-id="ca3cd-147">F#</span><span class="sxs-lookup"><span data-stu-id="ca3cd-147">F#</span></span>](#outfsharp)
* [<span data-ttu-id="ca3cd-148">Node.js</span><span class="sxs-lookup"><span data-stu-id="ca3cd-148">Node.js</span></span>](#outnodejs)

<a name="outcsharp"></a>

### <a name="output-sample-in-c"></a><span data-ttu-id="ca3cd-149">Przykładowe dane wyjściowe w języku C#</span><span class="sxs-lookup"><span data-stu-id="ca3cd-149">Output sample in C#</span></span> #

```cs
using System;

public static void Run(TimerInfo myTimer, out string outputEventHubMessage, TraceWriter log)
{
    String msg = $"TimerTriggerCSharp1 executed at: {DateTime.Now}";
    log.Verbose(msg);   
    outputEventHubMessage = msg;
}
```

<span data-ttu-id="ca3cd-150">Lub toocreate wiele komunikatów:</span><span class="sxs-lookup"><span data-stu-id="ca3cd-150">Or, toocreate multiple messages:</span></span>

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

### <a name="output-sample-in-f"></a><span data-ttu-id="ca3cd-151">Przykładowe dane wyjściowe w języku F #</span><span class="sxs-lookup"><span data-stu-id="ca3cd-151">Output sample in F#</span></span> #

```fsharp
let Run(myTimer: TimerInfo, outputEventHubMessage: byref<string>, log: TraceWriter) =
    let msg = sprintf "TimerTriggerFSharp1 executed at: %s" DateTime.Now.ToString()
    log.Verbose(msg);
    outputEventHubMessage <- msg;
```

<a name="outnodejs"></a>

### <a name="output-sample-for-nodejs"></a><span data-ttu-id="ca3cd-152">Przykładowe dane wyjściowe dla środowiska Node.js</span><span class="sxs-lookup"><span data-stu-id="ca3cd-152">Output sample for Node.js</span></span>

```javascript
module.exports = function (context, myTimer) {
    var timeStamp = new Date().toISOString();
    context.log('Event Hub message created at: ', timeStamp);   
    context.bindings.outputEventHubMessage = "Event Hub message created at: " + timeStamp;
    context.done();
};
```

<span data-ttu-id="ca3cd-153">Lub toosend wiele komunikatów</span><span class="sxs-lookup"><span data-stu-id="ca3cd-153">Or, toosend multiple messages,</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="ca3cd-154">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="ca3cd-154">Next steps</span></span>
[!INCLUDE [next steps](../../includes/functions-bindings-next-steps.md)]
