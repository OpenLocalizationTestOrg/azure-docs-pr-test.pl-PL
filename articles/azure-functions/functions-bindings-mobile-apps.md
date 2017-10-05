---
title: "Azure powiązania funkcji Mobile Apps | Dokumentacja firmy Microsoft"
description: "Zrozumienie, jak używać usługi Azure Mobile Apps powiązania w usługi Azure Functions."
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
ms.openlocfilehash: c5e1c02984f9773b263c0bee7685c7d5ff62e658
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="azure-functions-mobile-apps-bindings"></a><span data-ttu-id="5fd38-104">Azure powiązania funkcji Mobile Apps</span><span class="sxs-lookup"><span data-stu-id="5fd38-104">Azure Functions Mobile Apps bindings</span></span>
[!INCLUDE [functions-selector-bindings](../../includes/functions-selector-bindings.md)]

<span data-ttu-id="5fd38-105">W tym artykule opisano sposób konfigurowania i kodu [Azure Mobile Apps](../app-service-mobile/app-service-mobile-value-prop.md) powiązania usługi Azure Functions.</span><span class="sxs-lookup"><span data-stu-id="5fd38-105">This article explains how to configure and code [Azure Mobile Apps](../app-service-mobile/app-service-mobile-value-prop.md) bindings in Azure Functions.</span></span> <span data-ttu-id="5fd38-106">Azure Functions obsługuje wejściowa i wyjściowa powiązania dla aplikacji mobilnych.</span><span class="sxs-lookup"><span data-stu-id="5fd38-106">Azure Functions supports input and output bindings for Mobile Apps.</span></span>

<span data-ttu-id="5fd38-107">Wejściowy Mobile Apps i powiązania danych wyjściowych pozwalają [odczytywać i zapisywać do tabel danych](../app-service-mobile/app-service-mobile-node-backend-how-to-use-server-sdk.md#TableOperations) w aplikacji mobilnej.</span><span class="sxs-lookup"><span data-stu-id="5fd38-107">The Mobile Apps input and output bindings let you [read from and write to data tables](../app-service-mobile/app-service-mobile-node-backend-how-to-use-server-sdk.md#TableOperations) in your mobile app.</span></span>

[!INCLUDE [intro](../../includes/functions-bindings-intro.md)]

<a name="input"></a>

## <a name="mobile-apps-input-binding"></a><span data-ttu-id="5fd38-108">Powiązania wejściowego Mobile Apps</span><span class="sxs-lookup"><span data-stu-id="5fd38-108">Mobile Apps input binding</span></span>
<span data-ttu-id="5fd38-109">Powiązania wejściowego Mobile Apps ładuje rekord z punktu końcowego przenośnych tabeli i przekazuje ją do funkcji.</span><span class="sxs-lookup"><span data-stu-id="5fd38-109">The Mobile Apps input binding loads a record from a mobile table endpoint and passes it into your function.</span></span> <span data-ttu-id="5fd38-110">C# i F # funkcje wszelkie zmiany wprowadzone do rekordu są automatycznie wysyłane powrót do tabeli, gdy funkcja kończy się pomyślnie.</span><span class="sxs-lookup"><span data-stu-id="5fd38-110">In a C# and F# functions, any changes made to the record are automatically sent back to the table when the function exits successfully.</span></span>

<span data-ttu-id="5fd38-111">Dane wejściowe funkcji Mobile Apps używa następujący obiekt JSON w `bindings` tablicy function.json:</span><span class="sxs-lookup"><span data-stu-id="5fd38-111">The Mobile Apps input to a function uses the following JSON object in the `bindings` array of function.json:</span></span>

```json
{
    "name": "<Name of input parameter in function signature>",
    "type": "mobileTable",
    "tableName": "<Name of your mobile app's data table>",
    "id" : "<Id of the record to retrieve - see below>",
    "connection": "<Name of app setting that has your mobile app's URL - see below>",
    "apiKey": "<Name of app setting that has your mobile app's API key - see below>",
    "direction": "in"
}
```

<span data-ttu-id="5fd38-112">Pamiętaj o następujących kwestiach:</span><span class="sxs-lookup"><span data-stu-id="5fd38-112">Note the following:</span></span>

* <span data-ttu-id="5fd38-113">`id`może być statyczna, ani może bazować na wyzwalacz, który wywołuje funkcję.</span><span class="sxs-lookup"><span data-stu-id="5fd38-113">`id` can be static, or it can be based on the trigger that invokes the function.</span></span> <span data-ttu-id="5fd38-114">Na przykład, jeśli używasz [wyzwalacza kolejki]() dla funkcji, następnie `"id": "{queueTrigger}"` używa wartości ciągu komunikatu w kolejce jako identyfikator rekordu do pobrania.</span><span class="sxs-lookup"><span data-stu-id="5fd38-114">For example, if you use a [queue trigger]() for your function, then `"id": "{queueTrigger}"` uses the string value of the queue message as the record ID to retrieve.</span></span>
* <span data-ttu-id="5fd38-115">`connection`powinna zawierać nazwę ustawienia aplikacji w aplikacji funkcji, który z kolei zawiera adres URL aplikacji mobilnej.</span><span class="sxs-lookup"><span data-stu-id="5fd38-115">`connection` should contain the name of an app setting in your function app, which in turn contains the URL of your mobile app.</span></span> <span data-ttu-id="5fd38-116">Funkcja używa tego adresu URL do skonstruowania wymagane operacje REST względem aplikacji mobilnej.</span><span class="sxs-lookup"><span data-stu-id="5fd38-116">The function uses this URL to construct the required REST operations against your mobile app.</span></span> <span data-ttu-id="5fd38-117">Możesz [utworzyć ustawienie aplikacji w aplikacji funkcji]() zawierający adres URL aplikacji mobilnej (który wygląda podobnie `http://<appname>.azurewebsites.net`), określ nazwę ustawienia aplikacji w `connection` właściwości w Twojej powiązania wejściowego.</span><span class="sxs-lookup"><span data-stu-id="5fd38-117">You [create an app setting in your function app]() that contains your mobile app's URL (which looks like `http://<appname>.azurewebsites.net`), then specify the name of the app setting in the `connection` property in your input binding.</span></span> 
* <span data-ttu-id="5fd38-118">Należy określić `apiKey` Jeśli możesz [implementować klucz interfejsu API zaplecza aplikacji mobilnej Node.js](https://github.com/Azure/azure-mobile-apps-node/tree/master/samples/api-key), lub [implementować klucz interfejsu API zaplecza aplikacji mobilnej .NET](https://github.com/Azure/azure-mobile-apps-net-server/wiki/Implementing-Application-Key).</span><span class="sxs-lookup"><span data-stu-id="5fd38-118">You need to specify `apiKey` if you [implement an API key in your Node.js mobile app backend](https://github.com/Azure/azure-mobile-apps-node/tree/master/samples/api-key), or [implement an API key in your .NET mobile app backend](https://github.com/Azure/azure-mobile-apps-net-server/wiki/Implementing-Application-Key).</span></span> <span data-ttu-id="5fd38-119">W tym celu należy [utworzyć ustawienie aplikacji w aplikacji funkcji]() zawierający klucz interfejsu API, następnie dodać `apiKey` właściwości w Twojej powiązania wejściowego o nazwie ustawienia aplikacji.</span><span class="sxs-lookup"><span data-stu-id="5fd38-119">To do this, you [create an app setting in your function app]() that contains the API key, then add the `apiKey` property in your input binding with the name of the app setting.</span></span> 
  
  > [!IMPORTANT]
  > <span data-ttu-id="5fd38-120">Ten klucz interfejsu API nie może być udostępniany z klientami aplikacji mobilnej.</span><span class="sxs-lookup"><span data-stu-id="5fd38-120">This API key must not be shared with your mobile app clients.</span></span> <span data-ttu-id="5fd38-121">Go tylko należy rozdzielić bezpiecznie klientom po stronie serwera, takie jak usługi Azure Functions.</span><span class="sxs-lookup"><span data-stu-id="5fd38-121">It should only be distributed securely to service-side clients, like Azure Functions.</span></span> 
  > 
  > [!NOTE]
  > <span data-ttu-id="5fd38-122">Azure Functions przechowuje informacje dotyczące połączenia, a klucze interfejsu API zgodnie z ustawieniami aplikacji, dzięki czemu nie są sprawdzane w Twoim repozytorium kontroli źródła.</span><span class="sxs-lookup"><span data-stu-id="5fd38-122">Azure Functions stores your connection information and API keys as app settings so that they are not checked into your source control repository.</span></span> <span data-ttu-id="5fd38-123">To chroni poufne informacje.</span><span class="sxs-lookup"><span data-stu-id="5fd38-123">This safeguards your sensitive information.</span></span>
  > 
  > 

<a name="inputusage"></a>

## <a name="input-usage"></a><span data-ttu-id="5fd38-124">Użycie wejściowych</span><span class="sxs-lookup"><span data-stu-id="5fd38-124">Input usage</span></span>
<span data-ttu-id="5fd38-125">W tej sekcji przedstawiono sposób użycia Twojego powiązania wejściowego Mobile Apps w kodzie funkcji.</span><span class="sxs-lookup"><span data-stu-id="5fd38-125">This section shows you how to use your Mobile Apps input binding in your function code.</span></span> 

<span data-ttu-id="5fd38-126">Po znalezieniu rekordu z określonej tabeli i identyfikator rekordu jest przekazywana do nazwanego [JObject](http://www.newtonsoft.com/json/help/html/t_newtonsoft_json_linq_jobject.htm) parametr (lub w środowisku Node.js, są przekazywane do `context.bindings.<name>` obiektu).</span><span class="sxs-lookup"><span data-stu-id="5fd38-126">When the record with the specified table and record ID is found, it is passed into the named [JObject](http://www.newtonsoft.com/json/help/html/t_newtonsoft_json_linq_jobject.htm) parameter (or, in Node.js, it is passed into the `context.bindings.<name>` object).</span></span> <span data-ttu-id="5fd38-127">Jeśli rekord nie zostanie znaleziony, jest parametr `null`.</span><span class="sxs-lookup"><span data-stu-id="5fd38-127">When the record is not found, the parameter is `null`.</span></span> 

<span data-ttu-id="5fd38-128">W funkcji języka C# i F #, zmiany wprowadzone w danych wejściowych rekordu (parametr wejściowy) są wysyłane automatycznie powrót do tabeli Mobile Apps, gdy funkcja kończy się pomyślnie.</span><span class="sxs-lookup"><span data-stu-id="5fd38-128">In C# and F# functions, any changes you make to the input record (input parameter) is automatically sent back to the Mobile Apps table when the function exits successfully.</span></span> <span data-ttu-id="5fd38-129">W przypadku funkcji Node.js użyj `context.bindings.<name>` uzyskać dostęp do rekordu wejściowego.</span><span class="sxs-lookup"><span data-stu-id="5fd38-129">In Node.js functions, use `context.bindings.<name>` to access the input record.</span></span> <span data-ttu-id="5fd38-130">Nie można zmodyfikować rekord w środowisku Node.js.</span><span class="sxs-lookup"><span data-stu-id="5fd38-130">You cannot modify a record in Node.js.</span></span>

<a name="inputsample"></a>

## <a name="input-sample"></a><span data-ttu-id="5fd38-131">Przykładowe wejściowych</span><span class="sxs-lookup"><span data-stu-id="5fd38-131">Input sample</span></span>
<span data-ttu-id="5fd38-132">Załóżmy, że masz następujące function.json, pobierający rekord tabeli aplikacji mobilnej z identyfikatorem komunikatu wyzwalacza w kolejce:</span><span class="sxs-lookup"><span data-stu-id="5fd38-132">Suppose you have the following function.json, that retrieves a Mobile App table record with the id of the queue trigger message:</span></span>

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

<span data-ttu-id="5fd38-133">Zobacz przykładowe specyficzny dla języka, który korzysta z rekordu wejściowego z powiązania.</span><span class="sxs-lookup"><span data-stu-id="5fd38-133">See the language-specific sample that uses the input record from the binding.</span></span> <span data-ttu-id="5fd38-134">Przykłady w języku C# i F # również zmodyfikować rekordu `text` właściwości.</span><span class="sxs-lookup"><span data-stu-id="5fd38-134">The C# and F# samples also modify the record's `text` property.</span></span>

* [<span data-ttu-id="5fd38-135">C#</span><span class="sxs-lookup"><span data-stu-id="5fd38-135">C#</span></span>](#inputcsharp)
* [<span data-ttu-id="5fd38-136">Node.js</span><span class="sxs-lookup"><span data-stu-id="5fd38-136">Node.js</span></span>](#inputnodejs)

<a name="inputcsharp"></a>

### <a name="input-sample-in-c"></a><span data-ttu-id="5fd38-137">Przykładowe wejściowego w języku C#</span><span class="sxs-lookup"><span data-stu-id="5fd38-137">Input sample in C#</span></span> #

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

### <a name="input-sample-in-nodejs"></a><span data-ttu-id="5fd38-138">Przykładowe wejściowego w środowisku Node.js</span><span class="sxs-lookup"><span data-stu-id="5fd38-138">Input sample in Node.js</span></span>

```javascript
module.exports = function (context, myQueueItem) {    
    context.log(context.bindings.record);
    context.done();
};
```

<a name="output"></a>

## <a name="mobile-apps-output-binding"></a><span data-ttu-id="5fd38-139">Aplikacje mobilne powiązania wyjściowego</span><span class="sxs-lookup"><span data-stu-id="5fd38-139">Mobile Apps output binding</span></span>
<span data-ttu-id="5fd38-140">Za pomocą raportu Mobile Apps powiązanie można zapisać rekordu punktu końcowego tabeli Mobile Apps.</span><span class="sxs-lookup"><span data-stu-id="5fd38-140">Use the Mobile Apps output binding to write a new record to a Mobile Apps table endpoint.</span></span>  

<span data-ttu-id="5fd38-141">Aplikacje mobilne, dane wyjściowe dla funkcji używa następujący obiekt JSON w `bindings` tablicy function.json:</span><span class="sxs-lookup"><span data-stu-id="5fd38-141">The Mobile Apps output for a function uses the following JSON object in the `bindings` array of function.json:</span></span>

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

<span data-ttu-id="5fd38-142">Pamiętaj o następujących kwestiach:</span><span class="sxs-lookup"><span data-stu-id="5fd38-142">Note the following:</span></span>

* <span data-ttu-id="5fd38-143">`connection`powinna zawierać nazwę ustawienia aplikacji w aplikacji funkcji, który z kolei zawiera adres URL aplikacji mobilnej.</span><span class="sxs-lookup"><span data-stu-id="5fd38-143">`connection` should contain the name of an app setting in your function app, which in turn contains the URL of your mobile app.</span></span> <span data-ttu-id="5fd38-144">Funkcja używa tego adresu URL do skonstruowania wymagane operacje REST względem aplikacji mobilnej.</span><span class="sxs-lookup"><span data-stu-id="5fd38-144">The function uses this URL to construct the required REST operations against your mobile app.</span></span> <span data-ttu-id="5fd38-145">Możesz [utworzyć ustawienie aplikacji w aplikacji funkcji]() zawierający adres URL aplikacji mobilnej (który wygląda podobnie `http://<appname>.azurewebsites.net`), określ nazwę ustawienia aplikacji w `connection` właściwości w Twojej powiązania wejściowego.</span><span class="sxs-lookup"><span data-stu-id="5fd38-145">You [create an app setting in your function app]() that contains your mobile app's URL (which looks like `http://<appname>.azurewebsites.net`), then specify the name of the app setting in the `connection` property in your input binding.</span></span> 
* <span data-ttu-id="5fd38-146">Należy określić `apiKey` Jeśli możesz [implementować klucz interfejsu API zaplecza aplikacji mobilnej Node.js](https://github.com/Azure/azure-mobile-apps-node/tree/master/samples/api-key), lub [implementować klucz interfejsu API zaplecza aplikacji mobilnej .NET](https://github.com/Azure/azure-mobile-apps-net-server/wiki/Implementing-Application-Key).</span><span class="sxs-lookup"><span data-stu-id="5fd38-146">You need to specify `apiKey` if you [implement an API key in your Node.js mobile app backend](https://github.com/Azure/azure-mobile-apps-node/tree/master/samples/api-key), or [implement an API key in your .NET mobile app backend](https://github.com/Azure/azure-mobile-apps-net-server/wiki/Implementing-Application-Key).</span></span> <span data-ttu-id="5fd38-147">W tym celu należy [utworzyć ustawienie aplikacji w aplikacji funkcji]() zawierający klucz interfejsu API, następnie dodać `apiKey` właściwości w Twojej powiązania wejściowego o nazwie ustawienia aplikacji.</span><span class="sxs-lookup"><span data-stu-id="5fd38-147">To do this, you [create an app setting in your function app]() that contains the API key, then add the `apiKey` property in your input binding with the name of the app setting.</span></span> 
  
  > [!IMPORTANT]
  > <span data-ttu-id="5fd38-148">Ten klucz interfejsu API nie może być udostępniany z klientami aplikacji mobilnej.</span><span class="sxs-lookup"><span data-stu-id="5fd38-148">This API key must not be shared with your mobile app clients.</span></span> <span data-ttu-id="5fd38-149">Go tylko należy rozdzielić bezpiecznie klientom po stronie serwera, takie jak usługi Azure Functions.</span><span class="sxs-lookup"><span data-stu-id="5fd38-149">It should only be distributed securely to service-side clients, like Azure Functions.</span></span> 
  > 
  > [!NOTE]
  > <span data-ttu-id="5fd38-150">Azure Functions przechowuje informacje dotyczące połączenia, a klucze interfejsu API zgodnie z ustawieniami aplikacji, dzięki czemu nie są sprawdzane w Twoim repozytorium kontroli źródła.</span><span class="sxs-lookup"><span data-stu-id="5fd38-150">Azure Functions stores your connection information and API keys as app settings so that they are not checked into your source control repository.</span></span> <span data-ttu-id="5fd38-151">To chroni poufne informacje.</span><span class="sxs-lookup"><span data-stu-id="5fd38-151">This safeguards your sensitive information.</span></span>
  > 
  > 

<a name="outputusage"></a>

## <a name="output-usage"></a><span data-ttu-id="5fd38-152">Użycie danych wyjściowych</span><span class="sxs-lookup"><span data-stu-id="5fd38-152">Output usage</span></span>
<span data-ttu-id="5fd38-153">W tej sekcji przedstawiono sposób użycia powiązania w kodzie funkcji Mobile Apps dane wyjściowe.</span><span class="sxs-lookup"><span data-stu-id="5fd38-153">This section shows you how to use your Mobile Apps output binding in your function code.</span></span> 

<span data-ttu-id="5fd38-154">W języku C# funkcji, należy użyć parametru wyjściowego o nazwie typu `out object` uzyskać dostęp do rekordu danych wyjściowych.</span><span class="sxs-lookup"><span data-stu-id="5fd38-154">In C# functions, use a named output parameter of type `out object` to access the output record.</span></span> <span data-ttu-id="5fd38-155">W przypadku funkcji Node.js użyj `context.bindings.<name>` uzyskać dostęp do rekordu danych wyjściowych.</span><span class="sxs-lookup"><span data-stu-id="5fd38-155">In Node.js functions, use `context.bindings.<name>` to access the output record.</span></span>

<a name="outputsample"></a>

## <a name="output-sample"></a><span data-ttu-id="5fd38-156">Przykładowe dane wyjściowe</span><span class="sxs-lookup"><span data-stu-id="5fd38-156">Output sample</span></span>
<span data-ttu-id="5fd38-157">Załóżmy, że masz następujące function.json, definiujący wyzwalacz kolejki i wyjścia Mobile Apps:</span><span class="sxs-lookup"><span data-stu-id="5fd38-157">Suppose you have the following function.json, that defines a queue trigger and a Mobile Apps output:</span></span>

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

<span data-ttu-id="5fd38-158">Zobacz próbka specyficzny dla języka, która tworzy rekord w punkcie końcowym tabeli aplikacje mobilne z zawartością komunikatu w kolejce.</span><span class="sxs-lookup"><span data-stu-id="5fd38-158">See the language-specific sample that creates a record in the Mobile Apps table endpoint with the content of the queue message.</span></span>

* [<span data-ttu-id="5fd38-159">C#</span><span class="sxs-lookup"><span data-stu-id="5fd38-159">C#</span></span>](#outcsharp)
* [<span data-ttu-id="5fd38-160">Node.js</span><span class="sxs-lookup"><span data-stu-id="5fd38-160">Node.js</span></span>](#outnodejs)

<a name="outcsharp"></a>

### <a name="output-sample-in-c"></a><span data-ttu-id="5fd38-161">Przykładowe dane wyjściowe w języku C#</span><span class="sxs-lookup"><span data-stu-id="5fd38-161">Output sample in C#</span></span> #

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

### <a name="output-sample-in-nodejs"></a><span data-ttu-id="5fd38-162">Przykładowe dane wyjściowe w środowisku Node.js</span><span class="sxs-lookup"><span data-stu-id="5fd38-162">Output sample in Node.js</span></span>

```javascript
module.exports = function (context, myQueueItem) {

    context.bindings.record = {
        text : "I'm running in a Node function! Data: '" + myQueueItem + "'"
    }   

    context.done();
};
```

## <a name="next-steps"></a><span data-ttu-id="5fd38-163">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="5fd38-163">Next steps</span></span>
[!INCLUDE [next steps](../../includes/functions-bindings-next-steps.md)]

