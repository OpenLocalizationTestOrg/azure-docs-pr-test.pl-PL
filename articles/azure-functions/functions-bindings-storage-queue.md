---
title: "Środowisko Azure Functions kolejki magazynu powiązania | Dokumentacja firmy Microsoft"
description: "Zrozumienie, jak używać usługi Azure Storage wyzwalaczy i powiązań w funkcji platformy Azure."
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
ms.openlocfilehash: e007acd75a2210d54f512e2c6698c90919f0fcd2
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
# <a name="azure-functions-queue-storage-bindings"></a><span data-ttu-id="e7f1f-104">Powiązania funkcji magazynu kolejek Azure</span><span class="sxs-lookup"><span data-stu-id="e7f1f-104">Azure Functions Queue Storage bindings</span></span>
[!INCLUDE [functions-selector-bindings](../../includes/functions-selector-bindings.md)]

<span data-ttu-id="e7f1f-105">W tym artykule opisano sposób konfigurowania i powiązania magazynu kolejek Azure kodu usługi Azure Functions.</span><span class="sxs-lookup"><span data-stu-id="e7f1f-105">This article describes how to configure and code Azure Queue storage bindings in Azure Functions.</span></span> <span data-ttu-id="e7f1f-106">Usługi Azure Functions obsługuje uruchomić i dane wyjściowe powiązań dla kolejek platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="e7f1f-106">Azure Functions supports trigger and output bindings for Azure queues.</span></span> <span data-ttu-id="e7f1f-107">Na temat funkcji, które są dostępne w wszystkie powiązania [usługi Azure Functions wyzwalaczy i powiązań pojęcia](functions-triggers-bindings.md).</span><span class="sxs-lookup"><span data-stu-id="e7f1f-107">For features that are available in all bindings, see [Azure Functions triggers and bindings concepts](functions-triggers-bindings.md).</span></span>

[!INCLUDE [intro](../../includes/functions-bindings-intro.md)]

<a name="trigger"></a>

## <a name="queue-storage-trigger"></a><span data-ttu-id="e7f1f-108">Kolejki magazynu wyzwalacza</span><span class="sxs-lookup"><span data-stu-id="e7f1f-108">Queue storage trigger</span></span>
<span data-ttu-id="e7f1f-109">Wyzwalacz magazynu kolejek Azure umożliwia monitorowanie magazynu kolejek, nowe wiadomości i szybkiego reagowania na.</span><span class="sxs-lookup"><span data-stu-id="e7f1f-109">The Azure Queue storage trigger enables you to monitor a queue storage for new messages and react to them.</span></span> 

<span data-ttu-id="e7f1f-110">Zdefiniuj wyzwalacza kolejki przy użyciu **integracji** kartę w portalu funkcji.</span><span class="sxs-lookup"><span data-stu-id="e7f1f-110">Define a queue trigger using the **Integrate** tab in the Functions portal.</span></span> <span data-ttu-id="e7f1f-111">Portal tworzy następującą definicję w **powiązania** sekcji *function.json*:</span><span class="sxs-lookup"><span data-stu-id="e7f1f-111">The portal creates the following definition in the  **bindings** section of *function.json*:</span></span>

```json
{
    "type": "queueTrigger",
    "direction": "in",
    "name": "<The name used to identify the trigger data in your code>",
    "queueName": "<Name of queue to poll>",
    "connection":"<Name of app setting - see below>"
}
```

* <span data-ttu-id="e7f1f-112">`connection` Właściwości musi zawierać nazwę ustawienia aplikacji, która zawiera parametry połączenia magazynu.</span><span class="sxs-lookup"><span data-stu-id="e7f1f-112">The `connection` property must contain the name of an app setting that contains a storage connection string.</span></span> <span data-ttu-id="e7f1f-113">W portalu Azure, standardowego edytora w **integracji** kartę konfiguruje to ustawienie aplikacji, można wybrać konto magazynu.</span><span class="sxs-lookup"><span data-stu-id="e7f1f-113">In the Azure portal, the standard editor in the **Integrate** tab configures this app setting for you when you select a storage account.</span></span>

<span data-ttu-id="e7f1f-114">Można podać dodatkowe ustawienia w [pliku host.json](https://github.com/Azure/azure-webjobs-sdk-script/wiki/host.json) dopasować kolejki magazynu wyzwalaczy.</span><span class="sxs-lookup"><span data-stu-id="e7f1f-114">Additional settings can be provided in a [host.json file](https://github.com/Azure/azure-webjobs-sdk-script/wiki/host.json) to further fine-tune queue storage triggers.</span></span> <span data-ttu-id="e7f1f-115">Na przykład można zmienić interwał w host.json sondowania kolejki.</span><span class="sxs-lookup"><span data-stu-id="e7f1f-115">For example, you can change the queue polling interval in host.json.</span></span>

<a name="triggerusage"></a>

## <a name="using-a-queue-trigger"></a><span data-ttu-id="e7f1f-116">Użycie wyzwalacza kolejki</span><span class="sxs-lookup"><span data-stu-id="e7f1f-116">Using a queue trigger</span></span>
<span data-ttu-id="e7f1f-117">W przypadku funkcji Node.js uzyskiwać dostęp za pomocą danych kolejki `context.bindings.<name>`.</span><span class="sxs-lookup"><span data-stu-id="e7f1f-117">In Node.js functions, access the queue data using `context.bindings.<name>`.</span></span>


<span data-ttu-id="e7f1f-118">W przypadku funkcji .NET dostępu ładunku kolejki przy użyciu parametru metody, takich jak `CloudQueueMessage paramName`.</span><span class="sxs-lookup"><span data-stu-id="e7f1f-118">In .NET functions, access the queue payload using a method parameter such as `CloudQueueMessage paramName`.</span></span> <span data-ttu-id="e7f1f-119">W tym miejscu `paramName` jest wartością określoną w [konfiguracji wyzwalacza](#trigger).</span><span class="sxs-lookup"><span data-stu-id="e7f1f-119">Here, `paramName` is the value you specified in the [trigger configuration](#trigger).</span></span> <span data-ttu-id="e7f1f-120">Komunikat z kolejki może być zdeserializowany do żadnej z następujących typów:</span><span class="sxs-lookup"><span data-stu-id="e7f1f-120">The queue message can be deserialized to any of the following types:</span></span>

* <span data-ttu-id="e7f1f-121">Obiekt POCO.</span><span class="sxs-lookup"><span data-stu-id="e7f1f-121">POCO object.</span></span> <span data-ttu-id="e7f1f-122">Użyj, jeśli ładunek kolejki jest obiekt JSON.</span><span class="sxs-lookup"><span data-stu-id="e7f1f-122">Use if the queue payload is a JSON object.</span></span> <span data-ttu-id="e7f1f-123">Środowisko uruchomieniowe Functions deserializuje ładunku w obiekcie POCO.</span><span class="sxs-lookup"><span data-stu-id="e7f1f-123">The Functions runtime deserializes the payload into the POCO object.</span></span> 
* `string`
* `byte[]`
* [`CloudQueueMessage`]

<a name="meta"></a>

### <a name="queue-trigger-metadata"></a><span data-ttu-id="e7f1f-124">Metadane wyzwalacza kolejki</span><span class="sxs-lookup"><span data-stu-id="e7f1f-124">Queue trigger metadata</span></span>
<span data-ttu-id="e7f1f-125">Wyzwalacz kolejki zawiera kilka właściwości metadanych.</span><span class="sxs-lookup"><span data-stu-id="e7f1f-125">The queue trigger provides several metadata properties.</span></span> <span data-ttu-id="e7f1f-126">Te właściwości mogą służyć jako część wyrażenia powiązania w pozostałych powiązaniach lub parametrów w kodzie.</span><span class="sxs-lookup"><span data-stu-id="e7f1f-126">These properties can be used as part of binding expressions in other bindings or as parameters in your code.</span></span> <span data-ttu-id="e7f1f-127">Wartości mają tej samej semantyki jako [ `CloudQueueMessage` ].</span><span class="sxs-lookup"><span data-stu-id="e7f1f-127">The values have the same semantics as [`CloudQueueMessage`].</span></span>

* <span data-ttu-id="e7f1f-128">**QueueTrigger** -ładunku kolejki (jeśli prawidłowy ciąg)</span><span class="sxs-lookup"><span data-stu-id="e7f1f-128">**QueueTrigger** - queue payload (if a valid string)</span></span>
* <span data-ttu-id="e7f1f-129">**DequeueCount** — typ `int`.</span><span class="sxs-lookup"><span data-stu-id="e7f1f-129">**DequeueCount** - Type `int`.</span></span> <span data-ttu-id="e7f1f-130">Ile razy ten komunikat został usuniętej.</span><span class="sxs-lookup"><span data-stu-id="e7f1f-130">The number of times this message has been dequeued.</span></span>
* <span data-ttu-id="e7f1f-131">**ExpirationTime** — typ `DateTimeOffset?`.</span><span class="sxs-lookup"><span data-stu-id="e7f1f-131">**ExpirationTime** - Type `DateTimeOffset?`.</span></span> <span data-ttu-id="e7f1f-132">Czas wygaśnięcia wiadomości.</span><span class="sxs-lookup"><span data-stu-id="e7f1f-132">The time that the message expires.</span></span>
* <span data-ttu-id="e7f1f-133">**Identyfikator** — typ `string`.</span><span class="sxs-lookup"><span data-stu-id="e7f1f-133">**Id** - Type `string`.</span></span> <span data-ttu-id="e7f1f-134">Identyfikator kolejki wiadomości.</span><span class="sxs-lookup"><span data-stu-id="e7f1f-134">Queue message ID.</span></span>
* <span data-ttu-id="e7f1f-135">**InsertionTime** — typ `DateTimeOffset?`.</span><span class="sxs-lookup"><span data-stu-id="e7f1f-135">**InsertionTime** - Type `DateTimeOffset?`.</span></span> <span data-ttu-id="e7f1f-136">Godzina dodania wiadomości do kolejki.</span><span class="sxs-lookup"><span data-stu-id="e7f1f-136">The time that the message was added to the queue.</span></span>
* <span data-ttu-id="e7f1f-137">**NextVisibleTime** — typ `DateTimeOffset?`.</span><span class="sxs-lookup"><span data-stu-id="e7f1f-137">**NextVisibleTime** - Type `DateTimeOffset?`.</span></span> <span data-ttu-id="e7f1f-138">Czas, który następnie będzie widoczny komunikat.</span><span class="sxs-lookup"><span data-stu-id="e7f1f-138">The time that the message will next be visible.</span></span>
* <span data-ttu-id="e7f1f-139">**Elementu PopReceipt** — typ `string`.</span><span class="sxs-lookup"><span data-stu-id="e7f1f-139">**PopReceipt** - Type `string`.</span></span> <span data-ttu-id="e7f1f-140">Pop odbieranie komunikatu.</span><span class="sxs-lookup"><span data-stu-id="e7f1f-140">The message's pop receipt.</span></span>

<span data-ttu-id="e7f1f-141">Jak używać metadanych kolejki w [próbki wyzwalacza](#triggersample).</span><span class="sxs-lookup"><span data-stu-id="e7f1f-141">See how to use the queue metadata in [Trigger sample](#triggersample).</span></span>

<a name="triggersample"></a>

## <a name="trigger-sample"></a><span data-ttu-id="e7f1f-142">Przykładowe wyzwalacza</span><span class="sxs-lookup"><span data-stu-id="e7f1f-142">Trigger sample</span></span>
<span data-ttu-id="e7f1f-143">Załóżmy, że masz następujące function.json, który definiuje wyzwalacz kolejki:</span><span class="sxs-lookup"><span data-stu-id="e7f1f-143">Suppose you have the following function.json that defines a queue trigger:</span></span>

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

<span data-ttu-id="e7f1f-144">Przykładu specyficzny dla języka, które są pobierane i dzienniki kolejka metadanych.</span><span class="sxs-lookup"><span data-stu-id="e7f1f-144">See the language-specific sample that retrieves and logs queue metadata.</span></span>

* [<span data-ttu-id="e7f1f-145">C#</span><span class="sxs-lookup"><span data-stu-id="e7f1f-145">C#</span></span>](#triggercsharp)
* [<span data-ttu-id="e7f1f-146">Node.js</span><span class="sxs-lookup"><span data-stu-id="e7f1f-146">Node.js</span></span>](#triggernodejs)

<a name="triggercsharp"></a>

### <a name="trigger-sample-in-c"></a><span data-ttu-id="e7f1f-147">Przykładowe wyzwalacza w języku C#</span><span class="sxs-lookup"><span data-stu-id="e7f1f-147">Trigger sample in C#</span></span> #
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

### <a name="trigger-sample-in-nodejs"></a><span data-ttu-id="e7f1f-148">Przykładowe wyzwalacza w środowisku Node.js</span><span class="sxs-lookup"><span data-stu-id="e7f1f-148">Trigger sample in Node.js</span></span>

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

### <a name="handling-poison-queue-messages"></a><span data-ttu-id="e7f1f-149">Obsługa wiadomości w kolejce skażone</span><span class="sxs-lookup"><span data-stu-id="e7f1f-149">Handling poison queue messages</span></span>
<span data-ttu-id="e7f1f-150">Gdy funkcja wyzwalacza kolejki nie powiodło się, usługi Azure Functions ponowi próbę funkcji maksymalnie pięć razy dla danej kolejki wiadomości, czyli pierwszej próby.</span><span class="sxs-lookup"><span data-stu-id="e7f1f-150">When a queue trigger function fails, Azure Functions retries that function up to five times for a given queue message, including the first try.</span></span> <span data-ttu-id="e7f1f-151">Jeśli wszystkie próby pięć zakończą się niepowodzeniem, środowisko uruchomieniowe functions dodaje komunikat do kolejki magazynu o nazwie  *&lt;originalqueuename >-skażone*.</span><span class="sxs-lookup"><span data-stu-id="e7f1f-151">If all five attempts fail, the functions runtime adds a message to a queue storage named *&lt;originalqueuename>-poison*.</span></span> <span data-ttu-id="e7f1f-152">Można wpisać funkcji do przetwarzania komunikatów z kolejki skażone przez rejestrowania ich lub wysyłania powiadomienia tej uwagi ręczne jest wymagane.</span><span class="sxs-lookup"><span data-stu-id="e7f1f-152">You can write a function to process messages from the poison queue by logging them or sending a  notification that manual attention is needed.</span></span> 

<span data-ttu-id="e7f1f-153">Do obsługi wiadomości, ręcznie, sprawdź `dequeueCount` wiadomości w kolejce (zobacz [kolejki wyzwalacza metadanych](#meta)).</span><span class="sxs-lookup"><span data-stu-id="e7f1f-153">To handle poison messages manually, check the `dequeueCount` of the queue message (see [Queue trigger metadata](#meta)).</span></span>

<a name="output"></a>

## <a name="queue-storage-output-binding"></a><span data-ttu-id="e7f1f-154">Magazyn kolejek powiązania wyjściowego</span><span class="sxs-lookup"><span data-stu-id="e7f1f-154">Queue storage output binding</span></span>
<span data-ttu-id="e7f1f-155">Magazyn kolejek Azure powiązania danych wyjściowych umożliwia pisanie wiadomości do kolejki.</span><span class="sxs-lookup"><span data-stu-id="e7f1f-155">The Azure queue storage output binding enables you to write messages to a queue.</span></span> 

<span data-ttu-id="e7f1f-156">Zdefiniuj kolejki danych wyjściowych powiązanie using **integracji** kartę w portalu funkcji.</span><span class="sxs-lookup"><span data-stu-id="e7f1f-156">Define a queue output binding using the **Integrate** tab in the Functions portal.</span></span> <span data-ttu-id="e7f1f-157">Portal tworzy następującą definicję w **powiązania** sekcji *function.json*:</span><span class="sxs-lookup"><span data-stu-id="e7f1f-157">The portal creates the following definition in the  **bindings** section of *function.json*:</span></span>

```json
{
   "type": "queue",
   "direction": "out",
   "name": "<The name used to identify the trigger data in your code>",
   "queueName": "<Name of queue to write to>",
   "connection":"<Name of app setting - see below>"
}
```

* <span data-ttu-id="e7f1f-158">`connection` Właściwości musi zawierać nazwę ustawienia aplikacji, która zawiera parametry połączenia magazynu.</span><span class="sxs-lookup"><span data-stu-id="e7f1f-158">The `connection` property must contain the name of an app setting that contains a storage connection string.</span></span> <span data-ttu-id="e7f1f-159">W portalu Azure, standardowego edytora w **integracji** kartę konfiguruje to ustawienie aplikacji, można wybrać konto magazynu.</span><span class="sxs-lookup"><span data-stu-id="e7f1f-159">In the Azure portal, the standard editor in the **Integrate** tab configures this app setting for you when you select a storage account.</span></span>

<a name="outputusage"></a>

## <a name="using-a-queue-output-binding"></a><span data-ttu-id="e7f1f-160">Przy użyciu kolejki powiązania wyjściowego</span><span class="sxs-lookup"><span data-stu-id="e7f1f-160">Using a queue output binding</span></span>
<span data-ttu-id="e7f1f-161">W przypadku funkcji Node.js dostęp przy użyciu kolejki danych wyjściowych `context.bindings.<name>`.</span><span class="sxs-lookup"><span data-stu-id="e7f1f-161">In Node.js functions, you access the output queue using `context.bindings.<name>`.</span></span>

<span data-ttu-id="e7f1f-162">W przypadku funkcji .NET można dane wyjściowe do żadnego z następujących typów.</span><span class="sxs-lookup"><span data-stu-id="e7f1f-162">In .NET functions, you can output to any of the following types.</span></span> <span data-ttu-id="e7f1f-163">Po parametrze typu `T`, `T` musi być jednego z typów obsługiwanych wyjścia, takich jak `string` lub POCO.</span><span class="sxs-lookup"><span data-stu-id="e7f1f-163">When there is a type parameter `T`, `T` must be one of the supported output types, such as `string` or a POCO.</span></span>

* <span data-ttu-id="e7f1f-164">`out T`(zserializowanym w formacie JSON)</span><span class="sxs-lookup"><span data-stu-id="e7f1f-164">`out T` (serialized as JSON)</span></span>
* `out string`
* `out byte[]`
* <span data-ttu-id="e7f1f-165">`out` [`CloudQueueMessage`]</span><span class="sxs-lookup"><span data-stu-id="e7f1f-165">`out` [`CloudQueueMessage`]</span></span> 
* `ICollector<T>`
* `IAsyncCollector<T>`
* [`CloudQueue`](/dotnet/api/microsoft.windowsazure.storage.queue.cloudqueue)

<span data-ttu-id="e7f1f-166">Umożliwia także typ zwracany metody w powiązaniu danych wyjściowych.</span><span class="sxs-lookup"><span data-stu-id="e7f1f-166">You can also use the method return type as the output binding.</span></span>

<a name="outputsample"></a>

## <a name="queue-output-sample"></a><span data-ttu-id="e7f1f-167">Przykładowe dane wyjściowe kolejki</span><span class="sxs-lookup"><span data-stu-id="e7f1f-167">Queue output sample</span></span>
<span data-ttu-id="e7f1f-168">Następujące *function.json* definiuje wyzwalacza HTTP z kolejki powiązania wyjściowego:</span><span class="sxs-lookup"><span data-stu-id="e7f1f-168">The following *function.json* defines an HTTP trigger with a queue output binding:</span></span>

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

<span data-ttu-id="e7f1f-169">Zobacz przykładowe specyficzny dla języka, który wyprowadza komunikatu w kolejce Przychodzące ładunek HTTP.</span><span class="sxs-lookup"><span data-stu-id="e7f1f-169">See the language-specific sample that outputs a queue message with the incoming HTTP payload.</span></span>

* [<span data-ttu-id="e7f1f-170">C#</span><span class="sxs-lookup"><span data-stu-id="e7f1f-170">C#</span></span>](#outcsharp)
* [<span data-ttu-id="e7f1f-171">Node.js</span><span class="sxs-lookup"><span data-stu-id="e7f1f-171">Node.js</span></span>](#outnodejs)

<a name="outcsharp"></a>

### <a name="queue-output-sample-in-c"></a><span data-ttu-id="e7f1f-172">Przykładowe dane wyjściowe kolejek w języku C#</span><span class="sxs-lookup"><span data-stu-id="e7f1f-172">Queue output sample in C#</span></span> #

```cs
// C# example of HTTP trigger binding to a custom POCO, with a queue output binding
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

<span data-ttu-id="e7f1f-173">Aby wysłać wiele wiadomości, należy użyć `ICollector`:</span><span class="sxs-lookup"><span data-stu-id="e7f1f-173">To send multiple messages, use an `ICollector`:</span></span>

```cs
public static void Run(CustomQueueMessage input, ICollector<CustomQueueMessage> myQueueItem, TraceWriter log)
{
    myQueueItem.Add(input);
    myQueueItem.Add(new CustomQueueMessage { PersonName = "You", Title = "None" });
}
```

<a name="outnodejs"></a>

### <a name="queue-output-sample-in-nodejs"></a><span data-ttu-id="e7f1f-174">Przykładowe dane wyjściowe kolejki w środowisku Node.js</span><span class="sxs-lookup"><span data-stu-id="e7f1f-174">Queue output sample in Node.js</span></span>

```javascript
module.exports = function (context, input) {
    context.done(null, input.body);
};
```

<span data-ttu-id="e7f1f-175">Lub, w celu wysłania wiele komunikatów</span><span class="sxs-lookup"><span data-stu-id="e7f1f-175">Or, to send multiple messages,</span></span>

```javascript
module.exports = function(context) {
    // Define a message array for the myQueueItem output binding. 
    context.bindings.myQueueItem = ["message 1","message 2"];
    context.done();
};
```

## <a name="next-steps"></a><span data-ttu-id="e7f1f-176">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="e7f1f-176">Next steps</span></span>

<span data-ttu-id="e7f1f-177">Na przykład funkcja, która używa kolejki magazynu wyzwalaczy i powiązań zobacz [Tworzenie funkcji platformy Azure jest podłączony do usługi Azure](functions-create-an-azure-connected-function.md).</span><span class="sxs-lookup"><span data-stu-id="e7f1f-177">For an example of a function that uses queue storage triggers and bindings, see [Create an Azure Function connected to an Azure service](functions-create-an-azure-connected-function.md).</span></span>

[!INCLUDE [next steps](../../includes/functions-bindings-next-steps.md)]

<!-- LINKS -->

["CloudQueueMessage"]: /dotnet/api/microsoft.windowsazure.storage.queue.cloudqueuemessage
