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
# <a name="azure-functions-queue-storage-bindings"></a><span data-ttu-id="1f484-104">Powiązania funkcji magazynu kolejek Azure</span><span class="sxs-lookup"><span data-stu-id="1f484-104">Azure Functions Queue Storage bindings</span></span>
[!INCLUDE [functions-selector-bindings](../../includes/functions-selector-bindings.md)]

<span data-ttu-id="1f484-105">W tym artykule opisano sposób tooconfigure i kod powiązania magazynu kolejek Azure w funkcji platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="1f484-105">This article describes how tooconfigure and code Azure Queue storage bindings in Azure Functions.</span></span> <span data-ttu-id="1f484-106">Usługi Azure Functions obsługuje uruchomić i dane wyjściowe powiązań dla kolejek platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="1f484-106">Azure Functions supports trigger and output bindings for Azure queues.</span></span> <span data-ttu-id="1f484-107">Na temat funkcji, które są dostępne w wszystkie powiązania [usługi Azure Functions wyzwalaczy i powiązań pojęcia](functions-triggers-bindings.md).</span><span class="sxs-lookup"><span data-stu-id="1f484-107">For features that are available in all bindings, see [Azure Functions triggers and bindings concepts](functions-triggers-bindings.md).</span></span>

[!INCLUDE [intro](../../includes/functions-bindings-intro.md)]

<a name="trigger"></a>

## <a name="queue-storage-trigger"></a><span data-ttu-id="1f484-108">Kolejki magazynu wyzwalacza</span><span class="sxs-lookup"><span data-stu-id="1f484-108">Queue storage trigger</span></span>
<span data-ttu-id="1f484-109">wyzwalacz magazynu kolejek Azure Hello umożliwia toomonitor magazynu kolejek, nowe wiadomości i reagowania toothem.</span><span class="sxs-lookup"><span data-stu-id="1f484-109">hello Azure Queue storage trigger enables you toomonitor a queue storage for new messages and react toothem.</span></span> 

<span data-ttu-id="1f484-110">Zdefiniuj wyzwalacz kolejki przy użyciu hello **integracji** kartę w hello funkcje portalu.</span><span class="sxs-lookup"><span data-stu-id="1f484-110">Define a queue trigger using hello **Integrate** tab in hello Functions portal.</span></span> <span data-ttu-id="1f484-111">Witaj portal tworzy powitania po definicji w hello **powiązania** sekcji *function.json*:</span><span class="sxs-lookup"><span data-stu-id="1f484-111">hello portal creates hello following definition in hello  **bindings** section of *function.json*:</span></span>

```json
{
    "type": "queueTrigger",
    "direction": "in",
    "name": "<hello name used tooidentify hello trigger data in your code>",
    "queueName": "<Name of queue toopoll>",
    "connection":"<Name of app setting - see below>"
}
```

* <span data-ttu-id="1f484-112">Witaj `connection` właściwości musi zawierać nazwę hello ustawienia aplikacji, która zawiera parametry połączenia magazynu.</span><span class="sxs-lookup"><span data-stu-id="1f484-112">hello `connection` property must contain hello name of an app setting that contains a storage connection string.</span></span> <span data-ttu-id="1f484-113">W portalu Azure hello, hello standardowego edytora w hello **integracji** kartę konfiguruje to ustawienie aplikacji, można wybrać konto magazynu.</span><span class="sxs-lookup"><span data-stu-id="1f484-113">In hello Azure portal, hello standard editor in hello **Integrate** tab configures this app setting for you when you select a storage account.</span></span>

<span data-ttu-id="1f484-114">Można podać dodatkowe ustawienia w [pliku host.json](https://github.com/Azure/azure-webjobs-sdk-script/wiki/host.json) toofurther dostosowywać kolejki magazynu wyzwalaczy.</span><span class="sxs-lookup"><span data-stu-id="1f484-114">Additional settings can be provided in a [host.json file](https://github.com/Azure/azure-webjobs-sdk-script/wiki/host.json) toofurther fine-tune queue storage triggers.</span></span> <span data-ttu-id="1f484-115">Na przykład można zmienić interwał sondowania kolejki hello w host.json.</span><span class="sxs-lookup"><span data-stu-id="1f484-115">For example, you can change hello queue polling interval in host.json.</span></span>

<a name="triggerusage"></a>

## <a name="using-a-queue-trigger"></a><span data-ttu-id="1f484-116">Użycie wyzwalacza kolejki</span><span class="sxs-lookup"><span data-stu-id="1f484-116">Using a queue trigger</span></span>
<span data-ttu-id="1f484-117">W przypadku funkcji Node.js uzyskiwać dostęp za pomocą danych kolejki hello `context.bindings.<name>`.</span><span class="sxs-lookup"><span data-stu-id="1f484-117">In Node.js functions, access hello queue data using `context.bindings.<name>`.</span></span>


<span data-ttu-id="1f484-118">W funkcji .NET dostęp hello ładunku kolejki przy użyciu parametru metody, takich jak `CloudQueueMessage paramName`.</span><span class="sxs-lookup"><span data-stu-id="1f484-118">In .NET functions, access hello queue payload using a method parameter such as `CloudQueueMessage paramName`.</span></span> <span data-ttu-id="1f484-119">W tym miejscu `paramName` jest wartością hello określone w hello [konfiguracji wyzwalacza](#trigger).</span><span class="sxs-lookup"><span data-stu-id="1f484-119">Here, `paramName` is hello value you specified in hello [trigger configuration](#trigger).</span></span> <span data-ttu-id="1f484-120">wiadomości powitania kolejki może być zdeserializowany tooany z hello następujące typy:</span><span class="sxs-lookup"><span data-stu-id="1f484-120">hello queue message can be deserialized tooany of hello following types:</span></span>

* <span data-ttu-id="1f484-121">Obiekt POCO.</span><span class="sxs-lookup"><span data-stu-id="1f484-121">POCO object.</span></span> <span data-ttu-id="1f484-122">Użyj, jeśli ładunek kolejki hello jest obiekt JSON.</span><span class="sxs-lookup"><span data-stu-id="1f484-122">Use if hello queue payload is a JSON object.</span></span> <span data-ttu-id="1f484-123">środowisko uruchomieniowe Functions Hello deserializuje hello ładunku w obiekcie POCO hello.</span><span class="sxs-lookup"><span data-stu-id="1f484-123">hello Functions runtime deserializes hello payload into hello POCO object.</span></span> 
* `string`
* `byte[]`
* [`CloudQueueMessage`]

<a name="meta"></a>

### <a name="queue-trigger-metadata"></a><span data-ttu-id="1f484-124">Metadane wyzwalacza kolejki</span><span class="sxs-lookup"><span data-stu-id="1f484-124">Queue trigger metadata</span></span>
<span data-ttu-id="1f484-125">wyzwalacz kolejki Hello udostępnia kilka właściwości metadanych.</span><span class="sxs-lookup"><span data-stu-id="1f484-125">hello queue trigger provides several metadata properties.</span></span> <span data-ttu-id="1f484-126">Te właściwości mogą służyć jako część wyrażenia powiązania w pozostałych powiązaniach lub parametrów w kodzie.</span><span class="sxs-lookup"><span data-stu-id="1f484-126">These properties can be used as part of binding expressions in other bindings or as parameters in your code.</span></span> <span data-ttu-id="1f484-127">wartości Hello mają hello tej samej semantyki jako [ `CloudQueueMessage` ].</span><span class="sxs-lookup"><span data-stu-id="1f484-127">hello values have hello same semantics as [`CloudQueueMessage`].</span></span>

* <span data-ttu-id="1f484-128">**QueueTrigger** -ładunku kolejki (jeśli prawidłowy ciąg)</span><span class="sxs-lookup"><span data-stu-id="1f484-128">**QueueTrigger** - queue payload (if a valid string)</span></span>
* <span data-ttu-id="1f484-129">**DequeueCount** — typ `int`.</span><span class="sxs-lookup"><span data-stu-id="1f484-129">**DequeueCount** - Type `int`.</span></span> <span data-ttu-id="1f484-130">Witaj, ile razy ten komunikat został usuniętej.</span><span class="sxs-lookup"><span data-stu-id="1f484-130">hello number of times this message has been dequeued.</span></span>
* <span data-ttu-id="1f484-131">**ExpirationTime** — typ `DateTimeOffset?`.</span><span class="sxs-lookup"><span data-stu-id="1f484-131">**ExpirationTime** - Type `DateTimeOffset?`.</span></span> <span data-ttu-id="1f484-132">Witaj czas wygaśnięcia wiadomości powitania.</span><span class="sxs-lookup"><span data-stu-id="1f484-132">hello time that hello message expires.</span></span>
* <span data-ttu-id="1f484-133">**Identyfikator** — typ `string`.</span><span class="sxs-lookup"><span data-stu-id="1f484-133">**Id** - Type `string`.</span></span> <span data-ttu-id="1f484-134">Identyfikator kolejki wiadomości.</span><span class="sxs-lookup"><span data-stu-id="1f484-134">Queue message ID.</span></span>
* <span data-ttu-id="1f484-135">**InsertionTime** — typ `DateTimeOffset?`.</span><span class="sxs-lookup"><span data-stu-id="1f484-135">**InsertionTime** - Type `DateTimeOffset?`.</span></span> <span data-ttu-id="1f484-136">czas Hello tę wiadomość hello dodano toohello kolejki.</span><span class="sxs-lookup"><span data-stu-id="1f484-136">hello time that hello message was added toohello queue.</span></span>
* <span data-ttu-id="1f484-137">**NextVisibleTime** — typ `DateTimeOffset?`.</span><span class="sxs-lookup"><span data-stu-id="1f484-137">**NextVisibleTime** - Type `DateTimeOffset?`.</span></span> <span data-ttu-id="1f484-138">czas Hello tę wiadomość hello obok będą widoczne.</span><span class="sxs-lookup"><span data-stu-id="1f484-138">hello time that hello message will next be visible.</span></span>
* <span data-ttu-id="1f484-139">**Elementu PopReceipt** — typ `string`.</span><span class="sxs-lookup"><span data-stu-id="1f484-139">**PopReceipt** - Type `string`.</span></span> <span data-ttu-id="1f484-140">wiadomości powitania pop potwierdzenia.</span><span class="sxs-lookup"><span data-stu-id="1f484-140">hello message's pop receipt.</span></span>

<span data-ttu-id="1f484-141">Zobacz, jak toouse hello metadanych kolejki w [próbki wyzwalacza](#triggersample).</span><span class="sxs-lookup"><span data-stu-id="1f484-141">See how toouse hello queue metadata in [Trigger sample](#triggersample).</span></span>

<a name="triggersample"></a>

## <a name="trigger-sample"></a><span data-ttu-id="1f484-142">Przykładowe wyzwalacza</span><span class="sxs-lookup"><span data-stu-id="1f484-142">Trigger sample</span></span>
<span data-ttu-id="1f484-143">Załóżmy, że masz powitania po function.json, który definiuje wyzwalacz kolejki:</span><span class="sxs-lookup"><span data-stu-id="1f484-143">Suppose you have hello following function.json that defines a queue trigger:</span></span>

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

<span data-ttu-id="1f484-144">Zobacz przykład specyficzny dla języka hello, który pobiera i rejestruje metadanych kolejki.</span><span class="sxs-lookup"><span data-stu-id="1f484-144">See hello language-specific sample that retrieves and logs queue metadata.</span></span>

* [<span data-ttu-id="1f484-145">C#</span><span class="sxs-lookup"><span data-stu-id="1f484-145">C#</span></span>](#triggercsharp)
* [<span data-ttu-id="1f484-146">Node.js</span><span class="sxs-lookup"><span data-stu-id="1f484-146">Node.js</span></span>](#triggernodejs)

<a name="triggercsharp"></a>

### <a name="trigger-sample-in-c"></a><span data-ttu-id="1f484-147">Przykładowe wyzwalacza w języku C#</span><span class="sxs-lookup"><span data-stu-id="1f484-147">Trigger sample in C#</span></span> #
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

### <a name="trigger-sample-in-nodejs"></a><span data-ttu-id="1f484-148">Przykładowe wyzwalacza w środowisku Node.js</span><span class="sxs-lookup"><span data-stu-id="1f484-148">Trigger sample in Node.js</span></span>

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

### <a name="handling-poison-queue-messages"></a><span data-ttu-id="1f484-149">Obsługa wiadomości w kolejce skażone</span><span class="sxs-lookup"><span data-stu-id="1f484-149">Handling poison queue messages</span></span>
<span data-ttu-id="1f484-150">W przypadku awarii funkcja wyzwalacza kolejki usługi Azure Functions ponowi próbę tej funkcji w górę toofive razy dla danej kolejki wiadomości, tym hello najpierw spróbować.</span><span class="sxs-lookup"><span data-stu-id="1f484-150">When a queue trigger function fails, Azure Functions retries that function up toofive times for a given queue message, including hello first try.</span></span> <span data-ttu-id="1f484-151">Jeśli nie wszystkie próby pięć, środowisko uruchomieniowe functions hello dodaje magazynu kolejek tooa komunikatu o nazwie  *&lt;originalqueuename >-skażone*.</span><span class="sxs-lookup"><span data-stu-id="1f484-151">If all five attempts fail, hello functions runtime adds a message tooa queue storage named *&lt;originalqueuename>-poison*.</span></span> <span data-ttu-id="1f484-152">Można napisać tooprocess funkcji wiadomości z kolejki skażone hello rejestrowania ich lub wysyłania powiadomienia, że wymagana jest ręczne uwagi.</span><span class="sxs-lookup"><span data-stu-id="1f484-152">You can write a function tooprocess messages from hello poison queue by logging them or sending a  notification that manual attention is needed.</span></span> 

<span data-ttu-id="1f484-153">skażone wiadomości toohandle ręcznie, sprawdź hello `dequeueCount` hello kolejki wiadomości (zobacz [kolejki wyzwalacza metadanych](#meta)).</span><span class="sxs-lookup"><span data-stu-id="1f484-153">toohandle poison messages manually, check hello `dequeueCount` of hello queue message (see [Queue trigger metadata](#meta)).</span></span>

<a name="output"></a>

## <a name="queue-storage-output-binding"></a><span data-ttu-id="1f484-154">Magazyn kolejek powiązania wyjściowego</span><span class="sxs-lookup"><span data-stu-id="1f484-154">Queue storage output binding</span></span>
<span data-ttu-id="1f484-155">Powiązanie umożliwia toowrite wiadomości tooa kolejki danych wyjściowych Hello magazynu kolejek Azure.</span><span class="sxs-lookup"><span data-stu-id="1f484-155">hello Azure queue storage output binding enables you toowrite messages tooa queue.</span></span> 

<span data-ttu-id="1f484-156">Zdefiniuj kolejki powiązania wyjściowego przy użyciu hello **integracji** kartę w hello funkcje portalu.</span><span class="sxs-lookup"><span data-stu-id="1f484-156">Define a queue output binding using hello **Integrate** tab in hello Functions portal.</span></span> <span data-ttu-id="1f484-157">Witaj portal tworzy powitania po definicji w hello **powiązania** sekcji *function.json*:</span><span class="sxs-lookup"><span data-stu-id="1f484-157">hello portal creates hello following definition in hello  **bindings** section of *function.json*:</span></span>

```json
{
   "type": "queue",
   "direction": "out",
   "name": "<hello name used tooidentify hello trigger data in your code>",
   "queueName": "<Name of queue toowrite to>",
   "connection":"<Name of app setting - see below>"
}
```

* <span data-ttu-id="1f484-158">Witaj `connection` właściwości musi zawierać nazwę hello ustawienia aplikacji, która zawiera parametry połączenia magazynu.</span><span class="sxs-lookup"><span data-stu-id="1f484-158">hello `connection` property must contain hello name of an app setting that contains a storage connection string.</span></span> <span data-ttu-id="1f484-159">W portalu Azure hello, hello standardowego edytora w hello **integracji** kartę konfiguruje to ustawienie aplikacji, można wybrać konto magazynu.</span><span class="sxs-lookup"><span data-stu-id="1f484-159">In hello Azure portal, hello standard editor in hello **Integrate** tab configures this app setting for you when you select a storage account.</span></span>

<a name="outputusage"></a>

## <a name="using-a-queue-output-binding"></a><span data-ttu-id="1f484-160">Przy użyciu kolejki powiązania wyjściowego</span><span class="sxs-lookup"><span data-stu-id="1f484-160">Using a queue output binding</span></span>
<span data-ttu-id="1f484-161">W przypadku funkcji Node.js dostęp przy użyciu kolejki danych wyjściowych hello `context.bindings.<name>`.</span><span class="sxs-lookup"><span data-stu-id="1f484-161">In Node.js functions, you access hello output queue using `context.bindings.<name>`.</span></span>

<span data-ttu-id="1f484-162">W przypadku funkcji .NET dane wyjściowe tooany hello następujące typy.</span><span class="sxs-lookup"><span data-stu-id="1f484-162">In .NET functions, you can output tooany of hello following types.</span></span> <span data-ttu-id="1f484-163">Po parametrze typu `T`, `T` musi mieć jedną z hello obsługiwane typy danych wyjściowych, takich jak `string` lub POCO.</span><span class="sxs-lookup"><span data-stu-id="1f484-163">When there is a type parameter `T`, `T` must be one of hello supported output types, such as `string` or a POCO.</span></span>

* <span data-ttu-id="1f484-164">`out T`(zserializowanym w formacie JSON)</span><span class="sxs-lookup"><span data-stu-id="1f484-164">`out T` (serialized as JSON)</span></span>
* `out string`
* `out byte[]`
* <span data-ttu-id="1f484-165">`out` [`CloudQueueMessage`]</span><span class="sxs-lookup"><span data-stu-id="1f484-165">`out` [`CloudQueueMessage`]</span></span> 
* `ICollector<T>`
* `IAsyncCollector<T>`
* [`CloudQueue`](/dotnet/api/microsoft.windowsazure.storage.queue.cloudqueue)

<span data-ttu-id="1f484-166">Zwracany typ metody hello można także używać jako hello powiązania wyjściowego.</span><span class="sxs-lookup"><span data-stu-id="1f484-166">You can also use hello method return type as hello output binding.</span></span>

<a name="outputsample"></a>

## <a name="queue-output-sample"></a><span data-ttu-id="1f484-167">Przykładowe dane wyjściowe kolejki</span><span class="sxs-lookup"><span data-stu-id="1f484-167">Queue output sample</span></span>
<span data-ttu-id="1f484-168">następujące Hello *function.json* definiuje wyzwalacza HTTP z kolejki powiązania wyjściowego:</span><span class="sxs-lookup"><span data-stu-id="1f484-168">hello following *function.json* defines an HTTP trigger with a queue output binding:</span></span>

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

<span data-ttu-id="1f484-169">Zobacz hello próbki specyficzny dla języka, który wyprowadza kolejki wiadomość hello przychodzące ładunku HTTP.</span><span class="sxs-lookup"><span data-stu-id="1f484-169">See hello language-specific sample that outputs a queue message with hello incoming HTTP payload.</span></span>

* [<span data-ttu-id="1f484-170">C#</span><span class="sxs-lookup"><span data-stu-id="1f484-170">C#</span></span>](#outcsharp)
* [<span data-ttu-id="1f484-171">Node.js</span><span class="sxs-lookup"><span data-stu-id="1f484-171">Node.js</span></span>](#outnodejs)

<a name="outcsharp"></a>

### <a name="queue-output-sample-in-c"></a><span data-ttu-id="1f484-172">Przykładowe dane wyjściowe kolejek w języku C#</span><span class="sxs-lookup"><span data-stu-id="1f484-172">Queue output sample in C#</span></span> #

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

<span data-ttu-id="1f484-173">Użyj wielu wiadomości toosend `ICollector`:</span><span class="sxs-lookup"><span data-stu-id="1f484-173">toosend multiple messages, use an `ICollector`:</span></span>

```cs
public static void Run(CustomQueueMessage input, ICollector<CustomQueueMessage> myQueueItem, TraceWriter log)
{
    myQueueItem.Add(input);
    myQueueItem.Add(new CustomQueueMessage { PersonName = "You", Title = "None" });
}
```

<a name="outnodejs"></a>

### <a name="queue-output-sample-in-nodejs"></a><span data-ttu-id="1f484-174">Przykładowe dane wyjściowe kolejki w środowisku Node.js</span><span class="sxs-lookup"><span data-stu-id="1f484-174">Queue output sample in Node.js</span></span>

```javascript
module.exports = function (context, input) {
    context.done(null, input.body);
};
```

<span data-ttu-id="1f484-175">Lub toosend wiele komunikatów</span><span class="sxs-lookup"><span data-stu-id="1f484-175">Or, toosend multiple messages,</span></span>

```javascript
module.exports = function(context) {
    // Define a message array for hello myQueueItem output binding. 
    context.bindings.myQueueItem = ["message 1","message 2"];
    context.done();
};
```

## <a name="next-steps"></a><span data-ttu-id="1f484-176">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="1f484-176">Next steps</span></span>

<span data-ttu-id="1f484-177">Na przykład funkcja, która używa kolejki magazynu wyzwalaczy i powiązań zobacz [utworzyć tooan funkcji platformy Azure połączona usługa Azure](functions-create-an-azure-connected-function.md).</span><span class="sxs-lookup"><span data-stu-id="1f484-177">For an example of a function that uses queue storage triggers and bindings, see [Create an Azure Function connected tooan Azure service](functions-create-an-azure-connected-function.md).</span></span>

[!INCLUDE [next steps](../../includes/functions-bindings-next-steps.md)]

<!-- LINKS -->

["CloudQueueMessage"]: /dotnet/api/microsoft.windowsazure.storage.queue.cloudqueuemessage
