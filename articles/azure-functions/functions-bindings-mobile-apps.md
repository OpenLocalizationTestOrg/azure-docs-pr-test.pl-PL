---
title: "powiązania funkcji Mobile Apps aaaAzure | Dokumentacja firmy Microsoft"
description: "Zrozumienie sposobu toouse Azure Mobile Apps powiązania usługi Azure Functions."
services: functions
documentationcenter: na
author: ggailey777
manager: erikre
editor: 
tags: 
keywords: "funkcje usługi Azure, funkcje, przetwarzania zdarzeń, dynamiczne obliczeń niekorzystającą architektury"
ms.assetid: faad1263-0fa5-41a9-964f-aecbc0be706a
ms.service: functions
ms.devlang: multiple
ms.topic: reference
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 10/31/2016
ms.author: glenga
ms.openlocfilehash: d3679a5d5c66705b32e422ec17e3a1e6d6ac063c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-functions-mobile-apps-bindings"></a><span data-ttu-id="c1bec-104">Azure powiązania funkcji Mobile Apps</span><span class="sxs-lookup"><span data-stu-id="c1bec-104">Azure Functions Mobile Apps bindings</span></span>
[!INCLUDE [functions-selector-bindings](../../includes/functions-selector-bindings.md)]

<span data-ttu-id="c1bec-105">W tym artykule opisano sposób tooconfigure i kod [Azure Mobile Apps](../app-service-mobile/app-service-mobile-value-prop.md) powiązania usługi Azure Functions.</span><span class="sxs-lookup"><span data-stu-id="c1bec-105">This article explains how tooconfigure and code [Azure Mobile Apps](../app-service-mobile/app-service-mobile-value-prop.md) bindings in Azure Functions.</span></span> <span data-ttu-id="c1bec-106">Azure Functions obsługuje wejściowa i wyjściowa powiązania dla aplikacji mobilnych.</span><span class="sxs-lookup"><span data-stu-id="c1bec-106">Azure Functions supports input and output bindings for Mobile Apps.</span></span>

<span data-ttu-id="c1bec-107">Witaj Mobile Apps argument wejściowy i powiązania danych wyjściowych pozwalają [odczytywać i zapisywać tabele toodata](../app-service-mobile/app-service-mobile-node-backend-how-to-use-server-sdk.md#TableOperations) w aplikacji mobilnej.</span><span class="sxs-lookup"><span data-stu-id="c1bec-107">hello Mobile Apps input and output bindings let you [read from and write toodata tables](../app-service-mobile/app-service-mobile-node-backend-how-to-use-server-sdk.md#TableOperations) in your mobile app.</span></span>

[!INCLUDE [intro](../../includes/functions-bindings-intro.md)]

<a name="input"></a>

## <a name="mobile-apps-input-binding"></a><span data-ttu-id="c1bec-108">Powiązania wejściowego Mobile Apps</span><span class="sxs-lookup"><span data-stu-id="c1bec-108">Mobile Apps input binding</span></span>
<span data-ttu-id="c1bec-109">Witaj powiązania wejściowego Mobile Apps ładuje rekord z punktu końcowego przenośnych tabeli i przekazuje ją do funkcji.</span><span class="sxs-lookup"><span data-stu-id="c1bec-109">hello Mobile Apps input binding loads a record from a mobile table endpoint and passes it into your function.</span></span> <span data-ttu-id="c1bec-110">W C# i F # funkcjach rekord toohello wszelkie zmiany wprowadzone są automatycznie wysyłane tabeli wstecz toohello gdy funkcja hello kończy się pomyślnie.</span><span class="sxs-lookup"><span data-stu-id="c1bec-110">In a C# and F# functions, any changes made toohello record are automatically sent back toohello table when hello function exits successfully.</span></span>

<span data-ttu-id="c1bec-111">Witaj Mobile Apps wejściowych funkcja tooa używa powitania po obiekt JSON w hello `bindings` tablicy function.json:</span><span class="sxs-lookup"><span data-stu-id="c1bec-111">hello Mobile Apps input tooa function uses hello following JSON object in hello `bindings` array of function.json:</span></span>

```json
{
    "name": "<Name of input parameter in function signature>",
    "type": "mobileTable",
    "tableName": "<Name of your mobile app's data table>",
    "id" : "<Id of hello record tooretrieve - see below>",
    "connection": "<Name of app setting that has your mobile app's URL - see below>",
    "apiKey": "<Name of app setting that has your mobile app's API key - see below>",
    "direction": "in"
}
```

<span data-ttu-id="c1bec-112">Należy uwzględnić następujące hello:</span><span class="sxs-lookup"><span data-stu-id="c1bec-112">Note hello following:</span></span>

* <span data-ttu-id="c1bec-113">`id`może być statyczna, ani może bazować na powitania wyzwalacz, który wywołuje funkcję hello.</span><span class="sxs-lookup"><span data-stu-id="c1bec-113">`id` can be static, or it can be based on hello trigger that invokes hello function.</span></span> <span data-ttu-id="c1bec-114">Na przykład, jeśli używasz [wyzwalacza kolejki]() dla funkcji, następnie `"id": "{queueTrigger}"` używa hello ciąg hello kolejki wiadomości jako hello tooretrieve identyfikator rekordu.</span><span class="sxs-lookup"><span data-stu-id="c1bec-114">For example, if you use a [queue trigger]() for your function, then `"id": "{queueTrigger}"` uses hello string value of hello queue message as hello record ID tooretrieve.</span></span>
* <span data-ttu-id="c1bec-115">`connection`powinien zawierać nazwę hello ustawienie aplikacji w aplikacji funkcji, który z kolei zawiera adres URL hello aplikacji mobilnej.</span><span class="sxs-lookup"><span data-stu-id="c1bec-115">`connection` should contain hello name of an app setting in your function app, which in turn contains hello URL of your mobile app.</span></span> <span data-ttu-id="c1bec-116">Funkcja Hello używa tego adresu URL tooconstruct hello wymagane REST operacji względem aplikacji mobilnej.</span><span class="sxs-lookup"><span data-stu-id="c1bec-116">hello function uses this URL tooconstruct hello required REST operations against your mobile app.</span></span> <span data-ttu-id="c1bec-117">Możesz [utworzyć ustawienie aplikacji w aplikacji funkcji]() zawierający adres URL aplikacji mobilnej (który wygląda podobnie `http://<appname>.azurewebsites.net`), następnie określ nazwę ustawienia aplikacji hello hello w hello `connection` właściwości w Twojej powiązania wejściowego.</span><span class="sxs-lookup"><span data-stu-id="c1bec-117">You [create an app setting in your function app]() that contains your mobile app's URL (which looks like `http://<appname>.azurewebsites.net`), then specify hello name of hello app setting in hello `connection` property in your input binding.</span></span> 
* <span data-ttu-id="c1bec-118">Należy toospecify `apiKey` Jeśli możesz [implementować klucz interfejsu API zaplecza aplikacji mobilnej Node.js](https://github.com/Azure/azure-mobile-apps-node/tree/master/samples/api-key), lub [implementować klucz interfejsu API zaplecza aplikacji mobilnej .NET](https://github.com/Azure/azure-mobile-apps-net-server/wiki/Implementing-Application-Key).</span><span class="sxs-lookup"><span data-stu-id="c1bec-118">You need toospecify `apiKey` if you [implement an API key in your Node.js mobile app backend](https://github.com/Azure/azure-mobile-apps-node/tree/master/samples/api-key), or [implement an API key in your .NET mobile app backend](https://github.com/Azure/azure-mobile-apps-net-server/wiki/Implementing-Application-Key).</span></span> <span data-ttu-id="c1bec-119">toodo, możesz [utworzyć ustawienie aplikacji w aplikacji funkcji]() zawierający klucz hello interfejsu API, następnie dodać hello `apiKey` właściwości w Twojej powiązania wejściowego o nazwie hello ustawienia aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="c1bec-119">toodo this, you [create an app setting in your function app]() that contains hello API key, then add hello `apiKey` property in your input binding with hello name of hello app setting.</span></span> 
  
  > [!IMPORTANT]
  > <span data-ttu-id="c1bec-120">Ten klucz interfejsu API nie może być udostępniany z klientami aplikacji mobilnej.</span><span class="sxs-lookup"><span data-stu-id="c1bec-120">This API key must not be shared with your mobile app clients.</span></span> <span data-ttu-id="c1bec-121">Powinno to być rozproszone bezpiecznie tooservice po stronie klientów, takie jak usługi Azure Functions.</span><span class="sxs-lookup"><span data-stu-id="c1bec-121">It should only be distributed securely tooservice-side clients, like Azure Functions.</span></span> 
  > 
  > [!NOTE]
  > <span data-ttu-id="c1bec-122">Azure Functions przechowuje informacje dotyczące połączenia, a klucze interfejsu API zgodnie z ustawieniami aplikacji, dzięki czemu nie są sprawdzane w Twoim repozytorium kontroli źródła.</span><span class="sxs-lookup"><span data-stu-id="c1bec-122">Azure Functions stores your connection information and API keys as app settings so that they are not checked into your source control repository.</span></span> <span data-ttu-id="c1bec-123">To chroni poufne informacje.</span><span class="sxs-lookup"><span data-stu-id="c1bec-123">This safeguards your sensitive information.</span></span>
  > 
  > 

<a name="inputusage"></a>

## <a name="input-usage"></a><span data-ttu-id="c1bec-124">Użycie wejściowych</span><span class="sxs-lookup"><span data-stu-id="c1bec-124">Input usage</span></span>
<span data-ttu-id="c1bec-125">W tej sekcji przedstawiono, jak toouse aplikacji mobilnej wprowadź powiązania w kodzie funkcji.</span><span class="sxs-lookup"><span data-stu-id="c1bec-125">This section shows you how toouse your Mobile Apps input binding in your function code.</span></span> 

<span data-ttu-id="c1bec-126">W przypadku hello rekord z hello jest odnaleźć Identyfikatora tabeli i rejestrowanie jest przekazywany do hello o nazwie [JObject](http://www.newtonsoft.com/json/help/html/t_newtonsoft_json_linq_jobject.htm) parametr (lub w środowisku Node.js, jest przekazywany do hello `context.bindings.<name>` obiektu).</span><span class="sxs-lookup"><span data-stu-id="c1bec-126">When hello record with hello specified table and record ID is found, it is passed into hello named [JObject](http://www.newtonsoft.com/json/help/html/t_newtonsoft_json_linq_jobject.htm) parameter (or, in Node.js, it is passed into hello `context.bindings.<name>` object).</span></span> <span data-ttu-id="c1bec-127">Gdy nie ma rekordu hello, parametr hello jest `null`.</span><span class="sxs-lookup"><span data-stu-id="c1bec-127">When hello record is not found, hello parameter is `null`.</span></span> 

<span data-ttu-id="c1bec-128">W funkcji języka C# i F # wszystkie zmiany wprowadzone rekordu toohello danych wejściowych (parametr wejściowy) są wysyłane automatycznie wstecz toohello tabeli Mobile Apps gdy funkcja hello kończy się pomyślnie.</span><span class="sxs-lookup"><span data-stu-id="c1bec-128">In C# and F# functions, any changes you make toohello input record (input parameter) is automatically sent back toohello Mobile Apps table when hello function exits successfully.</span></span> <span data-ttu-id="c1bec-129">W przypadku funkcji Node.js użyj `context.bindings.<name>` tooaccess hello rekordu wejściowego.</span><span class="sxs-lookup"><span data-stu-id="c1bec-129">In Node.js functions, use `context.bindings.<name>` tooaccess hello input record.</span></span> <span data-ttu-id="c1bec-130">Nie można zmodyfikować rekord w środowisku Node.js.</span><span class="sxs-lookup"><span data-stu-id="c1bec-130">You cannot modify a record in Node.js.</span></span>

<a name="inputsample"></a>

## <a name="input-sample"></a><span data-ttu-id="c1bec-131">Przykładowe wejściowych</span><span class="sxs-lookup"><span data-stu-id="c1bec-131">Input sample</span></span>
<span data-ttu-id="c1bec-132">Załóżmy, że masz następujące function.json hello, który pobiera rekord aplikacji mobilnej tabeli o identyfikatorze hello kolejki wyzwalacza wiadomość hello:</span><span class="sxs-lookup"><span data-stu-id="c1bec-132">Suppose you have hello following function.json, that retrieves a Mobile App table record with hello id of hello queue trigger message:</span></span>

```json
{
"bindings": [
    {
    "name": "myQueueItem",
    "queueName": "myqueue-items",
    "connection":"",
    "type": "queueTrigger",
    "direction": "in"
    },
    {
        "name": "record",
        "type": "mobileTable",
        "tableName": "MyTable",
        "id" : "{queueTrigger}",
        "connection": "My_MobileApp_Url",
        "apiKey": "My_MobileApp_Key",
        "direction": "in"
    }
],
"disabled": false
}
```

<span data-ttu-id="c1bec-133">Zobacz przykład specyficzny dla języka hello, który korzysta z rekordu wejściowego hello z hello powiązania.</span><span class="sxs-lookup"><span data-stu-id="c1bec-133">See hello language-specific sample that uses hello input record from hello binding.</span></span> <span data-ttu-id="c1bec-134">Przykłady Hello C# i F # również zmodyfikować rekord hello `text` właściwości.</span><span class="sxs-lookup"><span data-stu-id="c1bec-134">hello C# and F# samples also modify hello record's `text` property.</span></span>

* [<span data-ttu-id="c1bec-135">C#</span><span class="sxs-lookup"><span data-stu-id="c1bec-135">C#</span></span>](#inputcsharp)
* [<span data-ttu-id="c1bec-136">Node.js</span><span class="sxs-lookup"><span data-stu-id="c1bec-136">Node.js</span></span>](#inputnodejs)

<a name="inputcsharp"></a>

### <a name="input-sample-in-c"></a><span data-ttu-id="c1bec-137">Przykładowe wejściowego w języku C#</span><span class="sxs-lookup"><span data-stu-id="c1bec-137">Input sample in C#</span></span> #

```cs
#r "Newtonsoft.Json"    
using Newtonsoft.Json.Linq;

public static void Run(string myQueueItem, JObject record)
{
    if (record != null)
    {
        record["Text"] = "This has changed.";
    }    
}
```

<!--
<a name="inputfsharp"></a>
### Input sample in F# ## 

```fsharp
#r "Newtonsoft.Json"    
open Newtonsoft.Json.Linq
let Run(myQueueItem: string, record: JObject) =
  inputDocument?text <- "This has changed."
```
-->

<a name="inputnodejs"></a>

### <a name="input-sample-in-nodejs"></a><span data-ttu-id="c1bec-138">Przykładowe wejściowego w środowisku Node.js</span><span class="sxs-lookup"><span data-stu-id="c1bec-138">Input sample in Node.js</span></span>

```javascript
module.exports = function (context, myQueueItem) {    
    context.log(context.bindings.record);
    context.done();
};
```

<a name="output"></a>

## <a name="mobile-apps-output-binding"></a><span data-ttu-id="c1bec-139">Aplikacje mobilne powiązania wyjściowego</span><span class="sxs-lookup"><span data-stu-id="c1bec-139">Mobile Apps output binding</span></span>
<span data-ttu-id="c1bec-140">Użyj hello Mobile Apps dane wyjściowe powiązania toowrite nowy punkt końcowy tabeli Mobile Apps tooa rekordów.</span><span class="sxs-lookup"><span data-stu-id="c1bec-140">Use hello Mobile Apps output binding toowrite a new record tooa Mobile Apps table endpoint.</span></span>  

<span data-ttu-id="c1bec-141">Witaj Mobile Apps danych wyjściowych dla następującego obiektu JSON w hello hello używa funkcji `bindings` tablicy function.json:</span><span class="sxs-lookup"><span data-stu-id="c1bec-141">hello Mobile Apps output for a function uses hello following JSON object in hello `bindings` array of function.json:</span></span>

```json
{
    "name": "<Name of output parameter in function signature>",
    "type": "mobileTable",
    "tableName": "<Name of your mobile app's data table>",
    "connection": "<Name of app setting that has your mobile app's URL - see below>",
    "apiKey": "<Name of app setting that has your mobile app's API key - see below>",
    "direction": "out"
}
```

<span data-ttu-id="c1bec-142">Należy uwzględnić następujące hello:</span><span class="sxs-lookup"><span data-stu-id="c1bec-142">Note hello following:</span></span>

* <span data-ttu-id="c1bec-143">`connection`powinien zawierać nazwę hello ustawienie aplikacji w aplikacji funkcji, który z kolei zawiera adres URL hello aplikacji mobilnej.</span><span class="sxs-lookup"><span data-stu-id="c1bec-143">`connection` should contain hello name of an app setting in your function app, which in turn contains hello URL of your mobile app.</span></span> <span data-ttu-id="c1bec-144">Funkcja Hello używa tego adresu URL tooconstruct hello wymagane REST operacji względem aplikacji mobilnej.</span><span class="sxs-lookup"><span data-stu-id="c1bec-144">hello function uses this URL tooconstruct hello required REST operations against your mobile app.</span></span> <span data-ttu-id="c1bec-145">Możesz [utworzyć ustawienie aplikacji w aplikacji funkcji]() zawierający adres URL aplikacji mobilnej (który wygląda podobnie `http://<appname>.azurewebsites.net`), następnie określ nazwę ustawienia aplikacji hello hello w hello `connection` właściwości w Twojej powiązania wejściowego.</span><span class="sxs-lookup"><span data-stu-id="c1bec-145">You [create an app setting in your function app]() that contains your mobile app's URL (which looks like `http://<appname>.azurewebsites.net`), then specify hello name of hello app setting in hello `connection` property in your input binding.</span></span> 
* <span data-ttu-id="c1bec-146">Należy toospecify `apiKey` Jeśli możesz [implementować klucz interfejsu API zaplecza aplikacji mobilnej Node.js](https://github.com/Azure/azure-mobile-apps-node/tree/master/samples/api-key), lub [implementować klucz interfejsu API zaplecza aplikacji mobilnej .NET](https://github.com/Azure/azure-mobile-apps-net-server/wiki/Implementing-Application-Key).</span><span class="sxs-lookup"><span data-stu-id="c1bec-146">You need toospecify `apiKey` if you [implement an API key in your Node.js mobile app backend](https://github.com/Azure/azure-mobile-apps-node/tree/master/samples/api-key), or [implement an API key in your .NET mobile app backend](https://github.com/Azure/azure-mobile-apps-net-server/wiki/Implementing-Application-Key).</span></span> <span data-ttu-id="c1bec-147">toodo, możesz [utworzyć ustawienie aplikacji w aplikacji funkcji]() zawierający klucz hello interfejsu API, następnie dodać hello `apiKey` właściwości w Twojej powiązania wejściowego o nazwie hello ustawienia aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="c1bec-147">toodo this, you [create an app setting in your function app]() that contains hello API key, then add hello `apiKey` property in your input binding with hello name of hello app setting.</span></span> 
  
  > [!IMPORTANT]
  > <span data-ttu-id="c1bec-148">Ten klucz interfejsu API nie może być udostępniany z klientami aplikacji mobilnej.</span><span class="sxs-lookup"><span data-stu-id="c1bec-148">This API key must not be shared with your mobile app clients.</span></span> <span data-ttu-id="c1bec-149">Powinno to być rozproszone bezpiecznie tooservice po stronie klientów, takie jak usługi Azure Functions.</span><span class="sxs-lookup"><span data-stu-id="c1bec-149">It should only be distributed securely tooservice-side clients, like Azure Functions.</span></span> 
  > 
  > [!NOTE]
  > <span data-ttu-id="c1bec-150">Azure Functions przechowuje informacje dotyczące połączenia, a klucze interfejsu API zgodnie z ustawieniami aplikacji, dzięki czemu nie są sprawdzane w Twoim repozytorium kontroli źródła.</span><span class="sxs-lookup"><span data-stu-id="c1bec-150">Azure Functions stores your connection information and API keys as app settings so that they are not checked into your source control repository.</span></span> <span data-ttu-id="c1bec-151">To chroni poufne informacje.</span><span class="sxs-lookup"><span data-stu-id="c1bec-151">This safeguards your sensitive information.</span></span>
  > 
  > 

<a name="outputusage"></a>

## <a name="output-usage"></a><span data-ttu-id="c1bec-152">Użycie danych wyjściowych</span><span class="sxs-lookup"><span data-stu-id="c1bec-152">Output usage</span></span>
<span data-ttu-id="c1bec-153">W tej sekcji przedstawiono, jak toouse aplikacji mobilnej output powiązania w kodzie funkcji.</span><span class="sxs-lookup"><span data-stu-id="c1bec-153">This section shows you how toouse your Mobile Apps output binding in your function code.</span></span> 

<span data-ttu-id="c1bec-154">W języku C# funkcji, należy użyć parametru wyjściowego o nazwie typu `out object` tooaccess hello output rekordu.</span><span class="sxs-lookup"><span data-stu-id="c1bec-154">In C# functions, use a named output parameter of type `out object` tooaccess hello output record.</span></span> <span data-ttu-id="c1bec-155">W przypadku funkcji Node.js użyj `context.bindings.<name>` tooaccess hello output rekordu.</span><span class="sxs-lookup"><span data-stu-id="c1bec-155">In Node.js functions, use `context.bindings.<name>` tooaccess hello output record.</span></span>

<a name="outputsample"></a>

## <a name="output-sample"></a><span data-ttu-id="c1bec-156">Przykładowe dane wyjściowe</span><span class="sxs-lookup"><span data-stu-id="c1bec-156">Output sample</span></span>
<span data-ttu-id="c1bec-157">Załóżmy, że masz powitania po function.json, definiujący wyzwalacz kolejki i wyjścia Mobile Apps:</span><span class="sxs-lookup"><span data-stu-id="c1bec-157">Suppose you have hello following function.json, that defines a queue trigger and a Mobile Apps output:</span></span>

```json
{
"bindings": [
    {
    "name": "myQueueItem",
    "queueName": "myqueue-items",
    "connection":"",
    "type": "queueTrigger",
    "direction": "in"
    },
    {
    "name": "record",
    "type": "mobileTable",
    "tableName": "MyTable",
    "connection": "My_MobileApp_Url",
    "apiKey": "My_MobileApp_Key",
    "direction": "out"
    }
],
"disabled": false
}
```

<span data-ttu-id="c1bec-158">Zobacz przykład specyficzny dla języka hello, który tworzy rekord w punkt końcowy tabel Mobile Apps hello z zawartością hello hello kolejki wiadomości.</span><span class="sxs-lookup"><span data-stu-id="c1bec-158">See hello language-specific sample that creates a record in hello Mobile Apps table endpoint with hello content of hello queue message.</span></span>

* [<span data-ttu-id="c1bec-159">C#</span><span class="sxs-lookup"><span data-stu-id="c1bec-159">C#</span></span>](#outcsharp)
* [<span data-ttu-id="c1bec-160">Node.js</span><span class="sxs-lookup"><span data-stu-id="c1bec-160">Node.js</span></span>](#outnodejs)

<a name="outcsharp"></a>

### <a name="output-sample-in-c"></a><span data-ttu-id="c1bec-161">Przykładowe dane wyjściowe w języku C#</span><span class="sxs-lookup"><span data-stu-id="c1bec-161">Output sample in C#</span></span> #

```cs
public static void Run(string myQueueItem, out object record)
{
    record = new {
        Text = $"I'm running in a C# function! {myQueueItem}"
    };
}
```

<!--
<a name="outfsharp"></a>
### Output sample in F# ## 
```fsharp

```
-->
<a name="outnodejs"></a>

### <a name="output-sample-in-nodejs"></a><span data-ttu-id="c1bec-162">Przykładowe dane wyjściowe w środowisku Node.js</span><span class="sxs-lookup"><span data-stu-id="c1bec-162">Output sample in Node.js</span></span>

```javascript
module.exports = function (context, myQueueItem) {

    context.bindings.record = {
        text : "I'm running in a Node function! Data: '" + myQueueItem + "'"
    }   

    context.done();
};
```

## <a name="next-steps"></a><span data-ttu-id="c1bec-163">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="c1bec-163">Next steps</span></span>
[!INCLUDE [next steps](../../includes/functions-bindings-next-steps.md)]

