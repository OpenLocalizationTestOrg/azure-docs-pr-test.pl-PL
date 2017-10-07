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
# <a name="azure-functions-service-bus-bindings"></a><span data-ttu-id="7ae00-104">Azure powiązania funkcji usługi Service Bus</span><span class="sxs-lookup"><span data-stu-id="7ae00-104">Azure Functions Service Bus bindings</span></span>
[!INCLUDE [functions-selector-bindings](../../includes/functions-selector-bindings.md)]

<span data-ttu-id="7ae00-105">W tym artykule opisano sposób tooconfigure i korzystanie z usługi Azure Service Bus powiązania usługi Azure Functions.</span><span class="sxs-lookup"><span data-stu-id="7ae00-105">This article explains how tooconfigure and work with Azure Service Bus bindings in Azure Functions.</span></span> 

<span data-ttu-id="7ae00-106">Usługi Azure Functions obsługuje uruchomić i dane wyjściowe powiązania dla tematów i kolejek usługi Service Bus.</span><span class="sxs-lookup"><span data-stu-id="7ae00-106">Azure Functions supports trigger and output bindings for Service Bus queues and topics.</span></span>

[!INCLUDE [intro](../../includes/functions-bindings-intro.md)]

<a name="trigger"></a>

## <a name="service-bus-trigger"></a><span data-ttu-id="7ae00-107">Wyzwalacz usługi Service Bus</span><span class="sxs-lookup"><span data-stu-id="7ae00-107">Service Bus trigger</span></span>
<span data-ttu-id="7ae00-108">Użyj hello usługi Service Bus wyzwalacza toorespond toomessages z kolejki usługi Service Bus lub temat.</span><span class="sxs-lookup"><span data-stu-id="7ae00-108">Use hello Service Bus trigger toorespond toomessages from a Service Bus queue or topic.</span></span> 

<span data-ttu-id="7ae00-109">Witaj wyzwalacze kolejki i tematu usługi Service Bus są definiowane przez następujące obiekty JSON w hello hello `bindings` tablicy function.json:</span><span class="sxs-lookup"><span data-stu-id="7ae00-109">hello Service Bus queue and topic triggers are defined by hello following JSON objects in hello `bindings` array of function.json:</span></span>

* <span data-ttu-id="7ae00-110">*kolejka* wyzwalacz:</span><span class="sxs-lookup"><span data-stu-id="7ae00-110">*queue* trigger:</span></span>

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

* <span data-ttu-id="7ae00-111">*temat* wyzwalacz:</span><span class="sxs-lookup"><span data-stu-id="7ae00-111">*topic* trigger:</span></span>

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

<span data-ttu-id="7ae00-112">Należy uwzględnić następujące hello:</span><span class="sxs-lookup"><span data-stu-id="7ae00-112">Note hello following:</span></span>

* <span data-ttu-id="7ae00-113">Dla `connection`, [utworzyć ustawienie aplikacji w aplikacji funkcji](functions-how-to-use-azure-function-app-settings.md) zawierającą przestrzeń nazw usługi Service Bus tooyour ciągu połączenia hello, określ nazwę hello ustawienia aplikacji hello w hello `connection` właściwości w wyzwalacz.</span><span class="sxs-lookup"><span data-stu-id="7ae00-113">For `connection`, [create an app setting in your function app](functions-how-to-use-azure-function-app-settings.md) that contains hello connection string tooyour Service Bus namespace, then specify hello name of hello app setting in hello `connection` property in your trigger.</span></span> <span data-ttu-id="7ae00-114">Uzyskania ciągu połączenia hello wykonując kroki hello pokazywane na [Uzyskiwanie poświadczeń zarządzania hello](../service-bus-messaging/service-bus-dotnet-get-started-with-queues.md#obtain-the-management-credentials).</span><span class="sxs-lookup"><span data-stu-id="7ae00-114">You obtain hello connection string by following hello steps shown at [Obtain hello management credentials](../service-bus-messaging/service-bus-dotnet-get-started-with-queues.md#obtain-the-management-credentials).</span></span>
  <span data-ttu-id="7ae00-115">Witaj parametry połączenia muszą mieć dla przestrzeni nazw usługi Service Bus, innymi tooa określonej kolejki lub temat.</span><span class="sxs-lookup"><span data-stu-id="7ae00-115">hello connection string must be for a Service Bus namespace, not limited tooa specific queue or topic.</span></span>
  <span data-ttu-id="7ae00-116">Jeśli opuścisz `connection` określenia domyślnego ciągu połączenia usługi Service Bus w aplikacji, ustawienie o nazwie pusta, zakłada wyzwalacza hello `AzureWebJobsServiceBus`.</span><span class="sxs-lookup"><span data-stu-id="7ae00-116">If you leave `connection` empty, hello trigger assumes that a default Service Bus connection string is specified in an app setting named `AzureWebJobsServiceBus`.</span></span>
* <span data-ttu-id="7ae00-117">Aby uzyskać `accessRights`, dostępne wartości to `manage` i `listen`.</span><span class="sxs-lookup"><span data-stu-id="7ae00-117">For `accessRights`, available values are `manage` and `listen`.</span></span> <span data-ttu-id="7ae00-118">Domyślnie Hello `manage`, co oznacza, że hello `connection` ma hello **Zarządzaj** uprawnienia.</span><span class="sxs-lookup"><span data-stu-id="7ae00-118">hello default is `manage`, which indicates that hello `connection` has hello **Manage** permission.</span></span> <span data-ttu-id="7ae00-119">Jeśli używasz parametry połączenia, które nie ma hello **Zarządzaj** zestawu uprawnień, `accessRights` zbyt`listen`.</span><span class="sxs-lookup"><span data-stu-id="7ae00-119">If you use a connection string that does not have hello **Manage** permission, set `accessRights` too`listen`.</span></span> <span data-ttu-id="7ae00-120">W przeciwnym razie hello funkcji środowiska uruchomieniowego może zakończyć się niepowodzeniem w trakcie operacji toodo wymagających zarządzania prawami.</span><span class="sxs-lookup"><span data-stu-id="7ae00-120">Otherwise, hello Functions runtime might fail trying toodo operations that require manage rights.</span></span>

## <a name="trigger-behavior"></a><span data-ttu-id="7ae00-121">Zachowanie wyzwalacza</span><span class="sxs-lookup"><span data-stu-id="7ae00-121">Trigger behavior</span></span>
* <span data-ttu-id="7ae00-122">**Wątkowość jednym** — domyślnie procesy środowiska uruchomieniowego funkcje hello wielu wiadomości jednocześnie.</span><span class="sxs-lookup"><span data-stu-id="7ae00-122">**Single-threading** - By default, hello Functions runtime processes multiple messages concurrently.</span></span> <span data-ttu-id="7ae00-123">Ustaw toodirect hello środowiska uruchomieniowego tooprocess tylko jednej kolejka lub temat wiadomości w czasie, `serviceBus.maxConcurrentCalls` too1 w *host.json*.</span><span class="sxs-lookup"><span data-stu-id="7ae00-123">toodirect hello runtime tooprocess only a single queue or topic message at a time, set `serviceBus.maxConcurrentCalls` too1 in *host.json*.</span></span> 
  <span data-ttu-id="7ae00-124">Aby uzyskać informacje o *host.json*, zobacz [struktury folderów](functions-reference.md#folder-structure) i [host.json](https://github.com/Azure/azure-webjobs-sdk-script/wiki/host.json).</span><span class="sxs-lookup"><span data-stu-id="7ae00-124">For information about *host.json*, see [Folder Structure](functions-reference.md#folder-structure) and [host.json](https://github .com/Azure/azure-webjobs-sdk-script/wiki/host.json).</span></span>
* <span data-ttu-id="7ae00-125">**Obsługa komunikatów zanieczyszczonych** -usługi Service Bus jest jego własnej obsługi uszkodzonych komunikatów, który nie może być kontrolowana ani skonfigurowana w konfiguracji usługi Azure Functions lub kod.</span><span class="sxs-lookup"><span data-stu-id="7ae00-125">**Poison message handling** - Service Bus does its own poison message handling, which can't be controlled or configured in Azure Functions configuration or code.</span></span> 
* <span data-ttu-id="7ae00-126">**Zachowanie PeekLock** — środowisko uruchomieniowe Functions hello odbiera wiadomości w [ `PeekLock` tryb](../service-bus-messaging/service-bus-performance-improvements.md#receive-mode) i wywołania `Complete` na wiadomość powitania, jeśli funkcja hello zakończy działanie pomyślnie, lub wywołania `Abandon` Jeśli hello Operacja zakończy się niepowodzeniem.</span><span class="sxs-lookup"><span data-stu-id="7ae00-126">**PeekLock behavior** - hello Functions runtime receives a message in [`PeekLock` mode](../service-bus-messaging/service-bus-performance-improvements.md#receive-mode) and calls `Complete` on hello message if hello function finishes successfully, or calls `Abandon` if hello function fails.</span></span> 
  <span data-ttu-id="7ae00-127">Jeśli funkcja hello uruchomione dłużej niż hello `PeekLock` limit czasu blokady hello jest automatycznie odnawiane.</span><span class="sxs-lookup"><span data-stu-id="7ae00-127">If hello function runs longer than hello `PeekLock` timeout, hello lock is automatically renewed.</span></span>

<a name="triggerusage"></a>

## <a name="trigger-usage"></a><span data-ttu-id="7ae00-128">Użycie wyzwalacza</span><span class="sxs-lookup"><span data-stu-id="7ae00-128">Trigger usage</span></span>
<span data-ttu-id="7ae00-129">W tej sekcji przedstawiono, jak toouse Twojego usługi Service Bus wyzwolenia w kodzie funkcji.</span><span class="sxs-lookup"><span data-stu-id="7ae00-129">This section shows you how toouse your Service Bus trigger in your function code.</span></span> 

<span data-ttu-id="7ae00-130">W języku C# i F # hello usługi Service Bus wyzwalacza komunikat może być zdeserializowany tooany z hello następujące typy wejściowe:</span><span class="sxs-lookup"><span data-stu-id="7ae00-130">In C# and F#, hello Service Bus trigger message can be deserialized tooany of hello following input types:</span></span>

* <span data-ttu-id="7ae00-131">`string`-przydatne w przypadku wiadomości ciąg</span><span class="sxs-lookup"><span data-stu-id="7ae00-131">`string` - useful for string messages</span></span>
* <span data-ttu-id="7ae00-132">`byte[]`-przydatne dla danych binarnych</span><span class="sxs-lookup"><span data-stu-id="7ae00-132">`byte[]` - useful for binary data</span></span>
* <span data-ttu-id="7ae00-133">Wszelkie [obiektu](https://msdn.microsoft.com/library/system.object.aspx) — jest to przydatne w przypadku danych serializacji JSON.</span><span class="sxs-lookup"><span data-stu-id="7ae00-133">Any [Object](https://msdn.microsoft.com/library/system.object.aspx) - useful for JSON-serialized data.</span></span>
  <span data-ttu-id="7ae00-134">Jeśli niestandardowy typ danych wejściowych, takich jak zadeklarować `CustomType`, usługi Azure Functions próbuje toodeserialize hello JSON danych w sieci określonego typu.</span><span class="sxs-lookup"><span data-stu-id="7ae00-134">If you declare a custom input type, such as `CustomType`, Azure Functions tries toodeserialize hello JSON data into your specified type.</span></span>
* <span data-ttu-id="7ae00-135">`BrokeredMessage`— zapewnia hello można przeprowadzić deserializacji wiadomość hello [BrokeredMessage.GetBody<T>()](https://msdn.microsoft.com/library/hh144211.aspx) metody.</span><span class="sxs-lookup"><span data-stu-id="7ae00-135">`BrokeredMessage` - gives you hello deserialized message with hello [BrokeredMessage.GetBody<T>()](https://msdn.microsoft.com/library/hh144211.aspx) method.</span></span>

<span data-ttu-id="7ae00-136">W środowisku Node.js komunikat wyzwalacza usługi Service Bus hello jest przekazany do funkcji hello jako ciąg lub obiekt JSON do.</span><span class="sxs-lookup"><span data-stu-id="7ae00-136">In Node.js, hello Service Bus trigger message is passed into hello function as either a string or JSON object.</span></span>

<a name="triggersample"></a>

## <a name="trigger-sample"></a><span data-ttu-id="7ae00-137">Przykładowe wyzwalacza</span><span class="sxs-lookup"><span data-stu-id="7ae00-137">Trigger sample</span></span>
<span data-ttu-id="7ae00-138">Załóżmy, że masz następujące function.json hello:</span><span class="sxs-lookup"><span data-stu-id="7ae00-138">Suppose you have hello following function.json:</span></span>

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

<span data-ttu-id="7ae00-139">Zobacz hello próbki specyficzny dla języka, który przetwarza komunikat z kolejki usługi Service Bus.</span><span class="sxs-lookup"><span data-stu-id="7ae00-139">See hello language-specific sample that processes a Service Bus queue message.</span></span>

* [<span data-ttu-id="7ae00-140">C#</span><span class="sxs-lookup"><span data-stu-id="7ae00-140">C#</span></span>](#triggercsharp)
* [<span data-ttu-id="7ae00-141">F#</span><span class="sxs-lookup"><span data-stu-id="7ae00-141">F#</span></span>](#triggerfsharp)
* [<span data-ttu-id="7ae00-142">Node.js</span><span class="sxs-lookup"><span data-stu-id="7ae00-142">Node.js</span></span>](#triggernodejs)

<a name="triggercsharp"></a>

### <a name="trigger-sample-in-c"></a><span data-ttu-id="7ae00-143">Przykładowe wyzwalacza w języku C#</span><span class="sxs-lookup"><span data-stu-id="7ae00-143">Trigger sample in C#</span></span> #

```cs
public static void Run(string myQueueItem, TraceWriter log)
{
    log.Info($"C# ServiceBus queue trigger function processed message: {myQueueItem}");
}
```

<a name="triggerfsharp"></a>

### <a name="trigger-sample-in-f"></a><span data-ttu-id="7ae00-144">Przykładowe wyzwalacza w języku F #</span><span class="sxs-lookup"><span data-stu-id="7ae00-144">Trigger sample in F#</span></span> #

```fsharp
let Run(myQueueItem: string, log: TraceWriter) =
    log.Info(sprintf "F# ServiceBus queue trigger function processed message: %s" myQueueItem)
```

<a name="triggernodejs"></a>

### <a name="trigger-sample-in-nodejs"></a><span data-ttu-id="7ae00-145">Przykładowe wyzwalacza w środowisku Node.js</span><span class="sxs-lookup"><span data-stu-id="7ae00-145">Trigger sample in Node.js</span></span>

```javascript
module.exports = function(context, myQueueItem) {
    context.log('Node.js ServiceBus queue trigger function processed message', myQueueItem);
    context.done();
};
```

<a name="output"></a>

## <a name="service-bus-output-binding"></a><span data-ttu-id="7ae00-146">Powiązania wyjściowego usługi Service Bus</span><span class="sxs-lookup"><span data-stu-id="7ae00-146">Service Bus output binding</span></span>
<span data-ttu-id="7ae00-147">Hello wyjściowego kolejek i tematów usługi Service Bus dla funkcji Użyj hello następujące obiekty JSON w hello `bindings` tablicy function.json:</span><span class="sxs-lookup"><span data-stu-id="7ae00-147">hello Service Bus queue and topic output for a function use hello following JSON objects in hello `bindings` array of function.json:</span></span>

* <span data-ttu-id="7ae00-148">*kolejka* danych wyjściowych:</span><span class="sxs-lookup"><span data-stu-id="7ae00-148">*queue* output:</span></span>

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
* <span data-ttu-id="7ae00-149">*temat* danych wyjściowych:</span><span class="sxs-lookup"><span data-stu-id="7ae00-149">*topic* output:</span></span>

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

<span data-ttu-id="7ae00-150">Należy uwzględnić następujące hello:</span><span class="sxs-lookup"><span data-stu-id="7ae00-150">Note hello following:</span></span>

* <span data-ttu-id="7ae00-151">Dla `connection`, [utworzyć ustawienie aplikacji w aplikacji funkcji](functions-how-to-use-azure-function-app-settings.md) zawierającą przestrzeń nazw usługi Service Bus tooyour ciągu połączenia hello, określ nazwę hello ustawienia aplikacji hello w hello `connection` właściwości w danych wyjściowych wiązanie.</span><span class="sxs-lookup"><span data-stu-id="7ae00-151">For `connection`, [create an app setting in your function app](functions-how-to-use-azure-function-app-settings.md) that contains hello connection string tooyour Service Bus namespace, then specify hello name of hello app setting in hello `connection` property in your output binding.</span></span> <span data-ttu-id="7ae00-152">Uzyskania ciągu połączenia hello wykonując kroki hello pokazywane na [Uzyskiwanie poświadczeń zarządzania hello](../service-bus-messaging/service-bus-dotnet-get-started-with-queues.md#obtain-the-management-credentials).</span><span class="sxs-lookup"><span data-stu-id="7ae00-152">You obtain hello connection string by following hello steps shown at [Obtain hello management credentials](../service-bus-messaging/service-bus-dotnet-get-started-with-queues.md#obtain-the-management-credentials).</span></span>
  <span data-ttu-id="7ae00-153">Witaj parametry połączenia muszą mieć dla przestrzeni nazw usługi Service Bus, innymi tooa określonej kolejki lub temat.</span><span class="sxs-lookup"><span data-stu-id="7ae00-153">hello connection string must be for a Service Bus namespace, not limited tooa specific queue or topic.</span></span>
  <span data-ttu-id="7ae00-154">Jeśli opuścisz `connection` pusta, hello powiązania wyjściowego przyjęto założenie, że domyślnego ciągu połączenia magistrali usług jest określona w aplikacji, ustawienie o nazwie `AzureWebJobsServiceBus`.</span><span class="sxs-lookup"><span data-stu-id="7ae00-154">If you leave `connection` empty, hello output binding assumes that a default Service Bus connection string is specified in an app setting named `AzureWebJobsServiceBus`.</span></span>
* <span data-ttu-id="7ae00-155">Aby uzyskać `accessRights`, dostępne wartości to `manage` i `listen`.</span><span class="sxs-lookup"><span data-stu-id="7ae00-155">For `accessRights`, available values are `manage` and `listen`.</span></span> <span data-ttu-id="7ae00-156">Domyślnie Hello `manage`, co oznacza, że hello `connection` ma hello **Zarządzaj** uprawnienia.</span><span class="sxs-lookup"><span data-stu-id="7ae00-156">hello default is `manage`, which indicates that hello `connection` has hello **Manage** permission.</span></span> <span data-ttu-id="7ae00-157">Jeśli używasz parametry połączenia, które nie ma hello **Zarządzaj** zestawu uprawnień, `accessRights` zbyt`listen`.</span><span class="sxs-lookup"><span data-stu-id="7ae00-157">If you use a connection string that does not have hello **Manage** permission, set `accessRights` too`listen`.</span></span> <span data-ttu-id="7ae00-158">W przeciwnym razie hello funkcji środowiska uruchomieniowego może zakończyć się niepowodzeniem w trakcie operacji toodo wymagających zarządzania prawami.</span><span class="sxs-lookup"><span data-stu-id="7ae00-158">Otherwise, hello Functions runtime might fail trying toodo operations that require manage rights.</span></span>

<a name="outputusage"></a>

## <a name="output-usage"></a><span data-ttu-id="7ae00-159">Użycie danych wyjściowych</span><span class="sxs-lookup"><span data-stu-id="7ae00-159">Output usage</span></span>
<span data-ttu-id="7ae00-160">W języku C# i F # usługi Azure Functions można utworzyć komunikat z kolejki usługi Service Bus za pomocą dowolnego hello następujące typy:</span><span class="sxs-lookup"><span data-stu-id="7ae00-160">In C# and F#, Azure Functions can create a Service Bus queue message from any of hello following types:</span></span>

* <span data-ttu-id="7ae00-161">Wszelkie [obiektu](https://msdn.microsoft.com/library/system.object.aspx) — definicja parametru wygląda `out T paramName` (C#).</span><span class="sxs-lookup"><span data-stu-id="7ae00-161">Any [Object](https://msdn.microsoft.com/library/system.object.aspx) - Parameter definition looks like `out T paramName` (C#).</span></span>
  <span data-ttu-id="7ae00-162">Funkcje deserializuje obiekt hello do wiadomości w formacie JSON.</span><span class="sxs-lookup"><span data-stu-id="7ae00-162">Functions deserializes hello object into a JSON message.</span></span> <span data-ttu-id="7ae00-163">Jeśli wartość wyjściowa hello ma wartość null, gdy funkcja hello jest kończona, funkcje tworzy wiadomość hello z obiektem null.</span><span class="sxs-lookup"><span data-stu-id="7ae00-163">If hello output value is null when hello function exits, Functions creates hello message with a null object.</span></span>
* <span data-ttu-id="7ae00-164">`string`-Definicja parametru wygląda `out string paraName` (C#).</span><span class="sxs-lookup"><span data-stu-id="7ae00-164">`string` - Parameter definition looks like `out string paraName` (C#).</span></span> <span data-ttu-id="7ae00-165">Jeśli wartość parametru hello jest różna od null, gdy funkcja hello jest kończona, funkcje tworzy komunikat.</span><span class="sxs-lookup"><span data-stu-id="7ae00-165">If hello parameter value is non-null when hello function exits, Functions creates a message.</span></span>
* <span data-ttu-id="7ae00-166">`byte[]`-Definicja parametru wygląda `out byte[] paraName` (C#).</span><span class="sxs-lookup"><span data-stu-id="7ae00-166">`byte[]` - Parameter definition looks like `out byte[] paraName` (C#).</span></span> <span data-ttu-id="7ae00-167">Jeśli wartość parametru hello jest różna od null, gdy funkcja hello jest kończona, funkcje tworzy komunikat.</span><span class="sxs-lookup"><span data-stu-id="7ae00-167">If hello parameter value is non-null when hello function exits, Functions creates a message.</span></span>
* <span data-ttu-id="7ae00-168">`BrokeredMessage`Definicja parametru wygląda `out BrokeredMessage paraName` (C#).</span><span class="sxs-lookup"><span data-stu-id="7ae00-168">`BrokeredMessage` Parameter definition looks like `out BrokeredMessage paraName` (C#).</span></span> <span data-ttu-id="7ae00-169">Jeśli wartość parametru hello jest różna od null, gdy funkcja hello jest kończona, funkcje tworzy komunikat.</span><span class="sxs-lookup"><span data-stu-id="7ae00-169">If hello parameter value is non-null when hello function exits, Functions creates a message.</span></span>

<span data-ttu-id="7ae00-170">W przypadku tworzenia wielu wiadomości w funkcji języka C#, można użyć `ICollector<T>` lub `IAsyncCollector<T>`.</span><span class="sxs-lookup"><span data-stu-id="7ae00-170">For creating multiple messages in a C# function, you can use `ICollector<T>` or `IAsyncCollector<T>`.</span></span> <span data-ttu-id="7ae00-171">Komunikat jest tworzony podczas wywoływania hello `Add` metody.</span><span class="sxs-lookup"><span data-stu-id="7ae00-171">A message is created when you call hello `Add` method.</span></span>

<span data-ttu-id="7ae00-172">W środowisku Node.js, można przypisać ciąg, tablica bajtów lub obiekt Javascript (deserializacji do postaci JSON) zbyt`context.binding.<paramName>`.</span><span class="sxs-lookup"><span data-stu-id="7ae00-172">In Node.js, you can assign a string, a byte array, or a Javascript object (deserialized into JSON) too`context.binding.<paramName>`.</span></span>

<a name="outputsample"></a>

## <a name="output-sample"></a><span data-ttu-id="7ae00-173">Przykładowe dane wyjściowe</span><span class="sxs-lookup"><span data-stu-id="7ae00-173">Output sample</span></span>
<span data-ttu-id="7ae00-174">Załóżmy, że masz następujące function.json hello definiuje wyjściowego kolejki usługi Service Bus:</span><span class="sxs-lookup"><span data-stu-id="7ae00-174">Suppose you have hello following function.json, that defines a Service Bus queue output:</span></span>

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

<span data-ttu-id="7ae00-175">Zobacz przykład specyficzny dla języka hello, który wysyła wiadomości toohello kolejką usługi service bus.</span><span class="sxs-lookup"><span data-stu-id="7ae00-175">See hello language-specific sample that sends a message toohello service bus queue.</span></span>

* [<span data-ttu-id="7ae00-176">C#</span><span class="sxs-lookup"><span data-stu-id="7ae00-176">C#</span></span>](#outcsharp)
* [<span data-ttu-id="7ae00-177">F#</span><span class="sxs-lookup"><span data-stu-id="7ae00-177">F#</span></span>](#outfsharp)
* [<span data-ttu-id="7ae00-178">Node.js</span><span class="sxs-lookup"><span data-stu-id="7ae00-178">Node.js</span></span>](#outnodejs)

<a name="outcsharp"></a>

### <a name="output-sample-in-c"></a><span data-ttu-id="7ae00-179">Przykładowe dane wyjściowe w języku C#</span><span class="sxs-lookup"><span data-stu-id="7ae00-179">Output sample in C#</span></span> #

```cs
public static void Run(TimerInfo myTimer, TraceWriter log, out string outputSbQueue)
{
    string message = $"Service Bus queue message created at: {DateTime.Now}";
    log.Info(message); 
    outputSbQueue = message;
}
```

<span data-ttu-id="7ae00-180">Lub toocreate wiele komunikatów:</span><span class="sxs-lookup"><span data-stu-id="7ae00-180">Or, toocreate multiple messages:</span></span>

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

### <a name="output-sample-in-f"></a><span data-ttu-id="7ae00-181">Przykładowe dane wyjściowe w języku F #</span><span class="sxs-lookup"><span data-stu-id="7ae00-181">Output sample in F#</span></span> #

```fsharp
let Run(myTimer: TimerInfo, log: TraceWriter, outputSbQueue: byref<string>) =
    let message = sprintf "Service Bus queue message created at: %s" (DateTime.Now.ToString())
    log.Info(message)
    outputSbQueue = message
```

<a name="outnodejs"></a>

### <a name="output-sample-in-nodejs"></a><span data-ttu-id="7ae00-182">Przykładowe dane wyjściowe w środowisku Node.js</span><span class="sxs-lookup"><span data-stu-id="7ae00-182">Output sample in Node.js</span></span>

```javascript
module.exports = function (context, myTimer) {
    var message = 'Service Bus queue message created at ' + timeStamp;
    context.log(message);   
    context.bindings.outputSbQueueMsg = message;
    context.done();
};
```

<span data-ttu-id="7ae00-183">Lub toocreate wiele komunikatów:</span><span class="sxs-lookup"><span data-stu-id="7ae00-183">Or, toocreate multiple messages:</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="7ae00-184">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="7ae00-184">Next steps</span></span>
[!INCLUDE [next steps](../../includes/functions-bindings-next-steps.md)]

