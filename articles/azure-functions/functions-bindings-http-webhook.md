---
title: "Azure powiązania HTTP funkcje i elementu webhook | Dokumentacja firmy Microsoft"
description: "Zrozumienie, jak używać protokołu HTTP i elementu webhook wyzwalaczy i powiązań w usługi Azure Functions."
services: functions
documentationcenter: na
author: mattchenderson
manager: erikre
editor: 
tags: 
keywords: "funkcje platformy Azure, funkcje, zdarzenia przetwarzania elementów webhook, dynamicznych zasobów obliczeniowych, API niekorzystającą architektury, protokołu HTTP, REST"
ms.assetid: 2b12200d-63d8-4ec1-9da8-39831d5a51b1
ms.service: functions
ms.devlang: multiple
ms.topic: reference
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 11/18/2016
ms.author: mahender
ms.openlocfilehash: 71c0d22c4b1824078982b9d1cc76645f947ae603
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/18/2017
---
# <a name="azure-functions-http-and-webhook-bindings"></a><span data-ttu-id="af485-104">Azure powiązania HTTP funkcje i elementu webhook</span><span class="sxs-lookup"><span data-stu-id="af485-104">Azure Functions HTTP and webhook bindings</span></span>
[!INCLUDE [functions-selector-bindings](../../includes/functions-selector-bindings.md)]

<span data-ttu-id="af485-105">W tym artykule opisano sposób konfigurowania i pracować z HTTP wyzwalaczy i powiązań w usługi Azure Functions.</span><span class="sxs-lookup"><span data-stu-id="af485-105">This article explains how to configure and work with HTTP triggers and bindings in Azure Functions.</span></span>
<span data-ttu-id="af485-106">Z tych opcji możesz użyć funkcji Azure kompilacji niekorzystającą interfejsów API i reagowanie na elementów webhook.</span><span class="sxs-lookup"><span data-stu-id="af485-106">With these, you can use Azure Functions to build serverless APIs and respond to webhooks.</span></span>

<span data-ttu-id="af485-107">Środowisko Azure Functions zapewnia następujące powiązania:</span><span class="sxs-lookup"><span data-stu-id="af485-107">Azure Functions provides the following bindings:</span></span>
- <span data-ttu-id="af485-108">[Wyzwalacza HTTP](#httptrigger) umożliwia wywołanie funkcji z żądania HTTP.</span><span class="sxs-lookup"><span data-stu-id="af485-108">An [HTTP trigger](#httptrigger) lets you invoke a function with an HTTP request.</span></span> <span data-ttu-id="af485-109">To można dostosować, aby odpowiadać na [elementów webhook](#hooktrigger).</span><span class="sxs-lookup"><span data-stu-id="af485-109">This can be customized to respond to [webhooks](#hooktrigger).</span></span>
- <span data-ttu-id="af485-110">[Powiązania wyjściowego HTTP](#output) pozwala odpowiedzieć na żądanie.</span><span class="sxs-lookup"><span data-stu-id="af485-110">An [HTTP output binding](#output) allows you to respond to the request.</span></span>

[!INCLUDE [intro](../../includes/functions-bindings-intro.md)]

[!INCLUDE [HTTP client best practices](../../includes/functions-http-client-best-practices.md)]

<a name="httptrigger"></a>

## <a name="http-trigger"></a><span data-ttu-id="af485-111">Wyzwalacz HTTP</span><span class="sxs-lookup"><span data-stu-id="af485-111">HTTP trigger</span></span>
<span data-ttu-id="af485-112">Wyzwalacza HTTP będzie wykonywał funkcji w odpowiedzi na żądania HTTP.</span><span class="sxs-lookup"><span data-stu-id="af485-112">The HTTP trigger will execute your function in response to an HTTP request.</span></span> <span data-ttu-id="af485-113">Można dostosować go do odpowiedzi z określonego adresu URL lub zestaw metod HTTP.</span><span class="sxs-lookup"><span data-stu-id="af485-113">You can customize it to respond to a particular URL or set of HTTP methods.</span></span> <span data-ttu-id="af485-114">Wyzwalacz HTTP można skonfigurować w taki sposób, aby odpowiedzieć na elementów webhook.</span><span class="sxs-lookup"><span data-stu-id="af485-114">An HTTP trigger can also be configured to respond to webhooks.</span></span> 

<span data-ttu-id="af485-115">Jeśli za pomocą portalu funkcji, można również rozpocząć od razu przy użyciu predefiniowanych szablonów.</span><span class="sxs-lookup"><span data-stu-id="af485-115">If using the Functions portal, you can also get started right away using a pre-made template.</span></span> <span data-ttu-id="af485-116">Wybierz **nową funkcję** i wybierz polecenie "Interfejsu API i elementów Webhook" z **scenariusza** listy rozwijanej.</span><span class="sxs-lookup"><span data-stu-id="af485-116">Select **New function** and choose "API & Webhooks" from the **Scenario** dropdown.</span></span> <span data-ttu-id="af485-117">Wybierz jeden z szablonów i kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="af485-117">Select one of the templates and click **Create**.</span></span>

<span data-ttu-id="af485-118">Domyślnie wyzwalacza HTTP będzie odpowiadać na żądania z kodem stanu HTTP 200 OK i pustej treści.</span><span class="sxs-lookup"><span data-stu-id="af485-118">By default, an HTTP trigger will respond to the request with an HTTP 200 OK status code and an empty body.</span></span> <span data-ttu-id="af485-119">Aby zmodyfikować odpowiedzi, należy skonfigurować [powiązania wyjściowego HTTP](#output)</span><span class="sxs-lookup"><span data-stu-id="af485-119">To modify the response, configure an [HTTP output binding](#output)</span></span>

### <a name="configuring-an-http-trigger"></a><span data-ttu-id="af485-120">Konfigurowanie wyzwalacza HTTP</span><span class="sxs-lookup"><span data-stu-id="af485-120">Configuring an HTTP trigger</span></span>
<span data-ttu-id="af485-121">Wyzwalacz protokołu HTTP jest zdefiniowane przez obiekt JSON, podobnie jak poniżej w tym `bindings` tablicy function.json:</span><span class="sxs-lookup"><span data-stu-id="af485-121">An HTTP trigger is defined by including a JSON object similar to the following in the `bindings` array of function.json:</span></span>

```json
{
    "name": "req",
    "type": "httpTrigger",
    "direction": "in",
    "authLevel": "function",
    "methods": [ "get" ],
    "route": "values/{id}"
},
```
<span data-ttu-id="af485-122">Wiązanie obsługuje następujące właściwości:</span><span class="sxs-lookup"><span data-stu-id="af485-122">The binding supports the following properties:</span></span>

* <span data-ttu-id="af485-123">**Nazwa** : wymagana — nazwa zmiennej używane w kodzie funkcji żądania lub treści żądania.</span><span class="sxs-lookup"><span data-stu-id="af485-123">**name** : Required - the variable name used in function code for the request or request body.</span></span> <span data-ttu-id="af485-124">Zobacz [Praca z wyzwalacza HTTP z kodu](#httptriggerusage).</span><span class="sxs-lookup"><span data-stu-id="af485-124">See [Working with an HTTP trigger from code](#httptriggerusage).</span></span>
* <span data-ttu-id="af485-125">**Typ** : wymagana — musi być ustawiona na "httpTrigger".</span><span class="sxs-lookup"><span data-stu-id="af485-125">**type** : Required - must be set to "httpTrigger".</span></span>
* <span data-ttu-id="af485-126">**kierunek** : wymagana — musi być ustawiona na "w".</span><span class="sxs-lookup"><span data-stu-id="af485-126">**direction** : Required - must be set to "in".</span></span>
* <span data-ttu-id="af485-127">_authLevel_ : Określa, jakie klucze, jeśli taki występuje, musi być obecny na żądanie, aby można było wywołać funkcję.</span><span class="sxs-lookup"><span data-stu-id="af485-127">_authLevel_ : This determines what keys, if any, need to be present on the request in order to invoke the function.</span></span> <span data-ttu-id="af485-128">Zobacz [Praca z kluczami](#keys) poniżej.</span><span class="sxs-lookup"><span data-stu-id="af485-128">See [Working with keys](#keys) below.</span></span> <span data-ttu-id="af485-129">Wartość może być jedną z następujących czynności:</span><span class="sxs-lookup"><span data-stu-id="af485-129">The value can be one of the following:</span></span>
    * <span data-ttu-id="af485-130">_anonimowe_: klucz interfejsu API nie jest wymagana.</span><span class="sxs-lookup"><span data-stu-id="af485-130">_anonymous_: No API key is required.</span></span>
    * <span data-ttu-id="af485-131">_Funkcja_: wymagany jest klucz interfejsu API właściwe dla funkcji.</span><span class="sxs-lookup"><span data-stu-id="af485-131">_function_: A function-specific API key is required.</span></span> <span data-ttu-id="af485-132">Jeśli nie zostanie podana jest wartość domyślna.</span><span class="sxs-lookup"><span data-stu-id="af485-132">This is the default value if none is provided.</span></span>
    * <span data-ttu-id="af485-133">_Administrator_ : jest wymagany klucz główny.</span><span class="sxs-lookup"><span data-stu-id="af485-133">_admin_ : The master key is required.</span></span>
* <span data-ttu-id="af485-134">**metody** : to jest tablica metod HTTP, na które będzie odpowiadać funkcji.</span><span class="sxs-lookup"><span data-stu-id="af485-134">**methods** : This is an array of the HTTP methods to which the function will respond.</span></span> <span data-ttu-id="af485-135">Jeśli nie zostanie określony, wszystkie metody HTTP będzie odpowiadać funkcji.</span><span class="sxs-lookup"><span data-stu-id="af485-135">If not specified, the function will respond to all HTTP methods.</span></span> <span data-ttu-id="af485-136">Zobacz [Dostosowywanie punkt końcowy HTTP](#url).</span><span class="sxs-lookup"><span data-stu-id="af485-136">See [Customizing the HTTP endpoint](#url).</span></span>
* <span data-ttu-id="af485-137">**trasy** : Określa szablon trasy, kontrolowanie, do którego adresów URL żądań funkcji będzie odpowiadać.</span><span class="sxs-lookup"><span data-stu-id="af485-137">**route** : This defines the route template, controlling to which request URLs your function will respond.</span></span> <span data-ttu-id="af485-138">Jeśli nie zostanie podana wartość domyślna to `<functionname>`.</span><span class="sxs-lookup"><span data-stu-id="af485-138">The default value if none is provided is `<functionname>`.</span></span> <span data-ttu-id="af485-139">Zobacz [Dostosowywanie punkt końcowy HTTP](#url).</span><span class="sxs-lookup"><span data-stu-id="af485-139">See [Customizing the HTTP endpoint](#url).</span></span>
* <span data-ttu-id="af485-140">**webHookType** : spowoduje to skonfigurowanie wyzwalacza HTTP do działania jako reciever elementu webhook dla określonego dostawcy.</span><span class="sxs-lookup"><span data-stu-id="af485-140">**webHookType** : This configures the HTTP trigger to act as a webhook reciever for the specified provider.</span></span> <span data-ttu-id="af485-141">_Metody_ właściwość nie powinna być ustawiona, jeśli to jest wybrane.</span><span class="sxs-lookup"><span data-stu-id="af485-141">The _methods_ property should not be set if this is chosen.</span></span> <span data-ttu-id="af485-142">Zobacz [odpowiada na żądania elementów webhook](#hooktrigger).</span><span class="sxs-lookup"><span data-stu-id="af485-142">See [Responding to webhooks](#hooktrigger).</span></span> <span data-ttu-id="af485-143">Wartość może być jedną z następujących czynności:</span><span class="sxs-lookup"><span data-stu-id="af485-143">The value can be one of the following:</span></span>
    * <span data-ttu-id="af485-144">_genericJson_ : punkt końcowy elementu webhook ogólnego przeznaczenia bez logiki dla określonego dostawcy.</span><span class="sxs-lookup"><span data-stu-id="af485-144">_genericJson_ : A general purpose webhook endpoint without logic for a specific provider.</span></span>
    * <span data-ttu-id="af485-145">_github_ : funkcja będzie odpowiadać elementów webhook GitHub.</span><span class="sxs-lookup"><span data-stu-id="af485-145">_github_ : The function will respond to GitHub webhooks.</span></span> <span data-ttu-id="af485-146">_AuthLevel_ właściwość nie powinna być ustawiona, jeśli to jest wybrane.</span><span class="sxs-lookup"><span data-stu-id="af485-146">The _authLevel_ property should not be set if this is chosen.</span></span>
    * <span data-ttu-id="af485-147">_zapas czasu_ : funkcja będzie odpowiadać elementów webhook Slack.</span><span class="sxs-lookup"><span data-stu-id="af485-147">_slack_ : The function will respond to Slack webhooks.</span></span> <span data-ttu-id="af485-148">_AuthLevel_ właściwość nie powinna być ustawiona, jeśli to jest wybrane.</span><span class="sxs-lookup"><span data-stu-id="af485-148">The _authLevel_ property should not be set if this is chosen.</span></span>

<a name="httptriggerusage"></a>
### <a name="working-with-an-http-trigger-from-code"></a><span data-ttu-id="af485-149">Praca z wyzwalacza HTTP z kodu</span><span class="sxs-lookup"><span data-stu-id="af485-149">Working with an HTTP trigger from code</span></span>
<span data-ttu-id="af485-150">Dla funkcji języka C# i F #, mogą zadeklarować typ danych wejściowych musi mieć przypisany wyzwalacz `HttpRequestMessage` lub typu niestandardowego.</span><span class="sxs-lookup"><span data-stu-id="af485-150">For C# and F# functions, you can declare the type of your trigger input to be either `HttpRequestMessage` or a custom type.</span></span> <span data-ttu-id="af485-151">Jeśli wybierzesz `HttpRequestMessage`, a następnie pobierze pełny dostęp do obiektu żądania.</span><span class="sxs-lookup"><span data-stu-id="af485-151">If you choose `HttpRequestMessage`, then you will get full access to the request object.</span></span> <span data-ttu-id="af485-152">Dla typu niestandardowego (na przykład POCO) funkcje podejmie próbę przeanalizować treść żądania jako ciąg JSON do wypełniania właściwości obiektu.</span><span class="sxs-lookup"><span data-stu-id="af485-152">For a custom type (such as a POCO), Functions will attempt to parse the request body as JSON to populate the object properties.</span></span>

<span data-ttu-id="af485-153">W przypadku funkcji Node.js środowisko uruchomieniowe Functions zapewnia treści żądania, zamiast obiektu żądania.</span><span class="sxs-lookup"><span data-stu-id="af485-153">For Node.js functions, the Functions runtime provides the request body instead of the request object.</span></span>

<span data-ttu-id="af485-154">Zobacz [przykłady wyzwalacza HTTP](#httptriggersample) na przykład sposobu użycia.</span><span class="sxs-lookup"><span data-stu-id="af485-154">See [HTTP trigger samples](#httptriggersample) for example usages.</span></span>


<a name="output"></a>
## <a name="http-response-output-binding"></a><span data-ttu-id="af485-155">Powiązania wyjściowego odpowiedzi HTTP</span><span class="sxs-lookup"><span data-stu-id="af485-155">HTTP response output binding</span></span>
<span data-ttu-id="af485-156">Za pomocą raportu HTTP powiązanie odpowiedź do nadawcy żądania HTTP.</span><span class="sxs-lookup"><span data-stu-id="af485-156">Use the HTTP output binding to respond to the HTTP request sender.</span></span> <span data-ttu-id="af485-157">To powiązanie wymaga wyzwalacza HTTP i umożliwia dostosowanie odpowiedzi skojarzony z żądaniem tego wyzwalacza.</span><span class="sxs-lookup"><span data-stu-id="af485-157">This binding requires an HTTP trigger and allows you to customize the response associated with the trigger's request.</span></span> <span data-ttu-id="af485-158">Jeśli powiązania wyjściowego HTTP nie zostanie podany, wyzwalacz HTTP zwróci o pustej treści HTTP 200 OK.</span><span class="sxs-lookup"><span data-stu-id="af485-158">If an HTTP output binding is not provided, an HTTP trigger will return HTTP 200 OK with an empty body.</span></span> 

### <a name="configuring-an-http-output-binding"></a><span data-ttu-id="af485-159">Konfigurowanie protokołu HTTP powiązania wyjściowego</span><span class="sxs-lookup"><span data-stu-id="af485-159">Configuring an HTTP output binding</span></span>
<span data-ttu-id="af485-160">HTTP powiązania danych wyjściowych jest zdefiniowane przez obiekt JSON, podobnie jak poniżej w tym `bindings` tablicy function.json:</span><span class="sxs-lookup"><span data-stu-id="af485-160">The HTTP output binding is defined by including a JSON object similar to the following in the `bindings` array of function.json:</span></span>

```json
{
    "name": "res",
    "type": "http",
    "direction": "out"
}
```
<span data-ttu-id="af485-161">Wiązanie zawiera następujące właściwości:</span><span class="sxs-lookup"><span data-stu-id="af485-161">The binding contains the following properties:</span></span>

* <span data-ttu-id="af485-162">**Nazwa** : wymagana — nazwa zmiennej używane w kodzie funkcja odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="af485-162">**name** : Required - the variable name used in function code for the response.</span></span> <span data-ttu-id="af485-163">Zobacz [powiązania z kodu wyjściowego roboczych protokołu HTTP z](#outputusage).</span><span class="sxs-lookup"><span data-stu-id="af485-163">See [Working with an HTTP output binding from code](#outputusage).</span></span>
* <span data-ttu-id="af485-164">**Typ** : wymagana — musi być ustawiona na "http".</span><span class="sxs-lookup"><span data-stu-id="af485-164">**type** : Required - must be set to "http".</span></span>
* <span data-ttu-id="af485-165">**kierunek** : wymagana — musi być ustawiona na "out".</span><span class="sxs-lookup"><span data-stu-id="af485-165">**direction** : Required - must be set to "out".</span></span>

<a name="outputusage"></a>
### <a name="working-with-an-http-output-binding-from-code"></a><span data-ttu-id="af485-166">Praca z HTTP output powiązania z kodu</span><span class="sxs-lookup"><span data-stu-id="af485-166">Working with an HTTP output binding from code</span></span>
<span data-ttu-id="af485-167">Można użyć parametru wyjściowego (np. "res") odpowiedź do obiektu wywołującego http lub elementu webhook.</span><span class="sxs-lookup"><span data-stu-id="af485-167">You can use the output parameter (e.g., "res") to respond to the http or webhook caller.</span></span> <span data-ttu-id="af485-168">Alternatywnie można użyć standardowego `Request.CreateResponse()` (C#) lub `context.res` wzorca (Node.JS), aby powrócić do odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="af485-168">Alternatively, you can use the standard `Request.CreateResponse()` (C#) or `context.res` (Node.JS) pattern to return your response.</span></span> <span data-ttu-id="af485-169">Przykłady dotyczące sposobu używania druga metoda, zobacz [przykłady wyzwalacza HTTP](#httptriggersample) i [przykłady wyzwalacza elementu Webhook](#hooktriggersample).</span><span class="sxs-lookup"><span data-stu-id="af485-169">For examples on how to use the latter method, see [HTTP trigger samples](#httptriggersample) and [Webhook trigger samples](#hooktriggersample).</span></span>


<a name="hooktrigger"></a>
## <a name="responding-to-webhooks"></a><span data-ttu-id="af485-170">Odpowiada na żądania elementów webhook</span><span class="sxs-lookup"><span data-stu-id="af485-170">Responding to webhooks</span></span>
<span data-ttu-id="af485-171">Wyzwalacz protokołu HTTP z _webHookType_ właściwości będzie skonfigurowanego do reagowania na [elementów webhook](https://en.wikipedia.org/wiki/Webhook).</span><span class="sxs-lookup"><span data-stu-id="af485-171">An HTTP trigger with the _webHookType_ property will be configured to respond to [webhooks](https://en.wikipedia.org/wiki/Webhook).</span></span> <span data-ttu-id="af485-172">Konfiguracja podstawowa używana do określania "genericJson".</span><span class="sxs-lookup"><span data-stu-id="af485-172">The basic configuration uses the "genericJson" setting.</span></span> <span data-ttu-id="af485-173">To ogranicza żądania tylko do tych przy użyciu protokołu HTTP POST i z `application/json` typ zawartości.</span><span class="sxs-lookup"><span data-stu-id="af485-173">This restricts requests to only those using HTTP POST and with the `application/json` content type.</span></span>

<span data-ttu-id="af485-174">Wyzwalacz dodatkowo umożliwia dostosowanie dostawcy określonego elementu webhook (np. [GitHub](https://developer.github.com/webhooks/) i [Slack](https://api.slack.com/outgoing-webhooks)).</span><span class="sxs-lookup"><span data-stu-id="af485-174">The trigger can additionally be tailored to a specific webhook provider (e.g., [GitHub](https://developer.github.com/webhooks/) and [Slack](https://api.slack.com/outgoing-webhooks)).</span></span> <span data-ttu-id="af485-175">Jeśli jest określony dostawca, środowisko uruchomieniowe Functions zająć się dostawcy logikę weryfikacji dla Ciebie.</span><span class="sxs-lookup"><span data-stu-id="af485-175">If a provider is specified, the Functions runtime can take care of the provider's validation logic for you.</span></span>  

### <a name="configuring-github-as-a-webhook-provider"></a><span data-ttu-id="af485-176">Konfigurowanie dostawcy elementu webhook GitHub</span><span class="sxs-lookup"><span data-stu-id="af485-176">Configuring GitHub as a webhook provider</span></span>
<span data-ttu-id="af485-177">Aby odpowiedzieć elementów webhook GitHub, najpierw utwórz funkcji z wyzwalaczem HTTP i ustaw _webHookType_ dla właściwości "github".</span><span class="sxs-lookup"><span data-stu-id="af485-177">To respond to GitHub webhooks, first create your function with an HTTP Trigger, and set the _webHookType_ property to "github".</span></span> <span data-ttu-id="af485-178">Następnie skopiuj jej [adres URL](#url) i [klucz interfejsu API](#keys) w repozytorium GitHub **Dodawanie elementu webhook** strony.</span><span class="sxs-lookup"><span data-stu-id="af485-178">Then copy its [URL](#url) and [API key](#keys) into your GitHub repository's **Add webhook** page.</span></span> <span data-ttu-id="af485-179">Zobacz GitHub [tworzenia elementów Webhook](http://go.microsoft.com/fwlink/?LinkID=761099&clcid=0x409) dokumentacji, aby uzyskać więcej informacji.</span><span class="sxs-lookup"><span data-stu-id="af485-179">See GitHub's [Creating Webhooks](http://go.microsoft.com/fwlink/?LinkID=761099&clcid=0x409) documentation for more.</span></span>

![](./media/functions-bindings-http-webhook/github-add-webhook.png)

### <a name="configuring-slack-as-a-webhook-provider"></a><span data-ttu-id="af485-180">Konfigurowanie zapas czasu jako dostawca elementu webhook</span><span class="sxs-lookup"><span data-stu-id="af485-180">Configuring Slack as a webhook provider</span></span>
<span data-ttu-id="af485-181">Slack elementu webhook generuje token dla Ciebie, zamiast czekać na określeniu, dlatego należy skonfigurować klucz właściwe dla funkcji przy użyciu tokenu z zapas czasu.</span><span class="sxs-lookup"><span data-stu-id="af485-181">The Slack webhook generates a token for you instead of letting you specify it, so you must configure a function-specific key with the token from Slack.</span></span> <span data-ttu-id="af485-182">Zobacz [Praca z kluczami](#keys).</span><span class="sxs-lookup"><span data-stu-id="af485-182">See [Working with keys](#keys).</span></span>

<a name="url"></a>
## <a name="customizing-the-http-endpoint"></a><span data-ttu-id="af485-183">Dostosowywanie punkt końcowy HTTP</span><span class="sxs-lookup"><span data-stu-id="af485-183">Customizing the HTTP endpoint</span></span>
<span data-ttu-id="af485-184">Domyślnie podczas tworzenia funkcja wyzwalacza HTTP lub elementu WebHook, funkcja jest adresowanego trasa formularza:</span><span class="sxs-lookup"><span data-stu-id="af485-184">By default when you create a function for an HTTP trigger, or WebHook, the function is addressable with a route of the form:</span></span>

    http://<yourapp>.azurewebsites.net/api/<funcname> 

<span data-ttu-id="af485-185">Można dostosować tej trasy przy użyciu opcjonalnego `route` wejściowych powiązania właściwości wyzwalacza HTTP.</span><span class="sxs-lookup"><span data-stu-id="af485-185">You can customize this route using the optional `route` property on the HTTP trigger's input binding.</span></span> <span data-ttu-id="af485-186">Na przykład następujące *function.json* plik definiuje `route` właściwości dla wyzwalacza HTTP:</span><span class="sxs-lookup"><span data-stu-id="af485-186">As an example, the following *function.json* file defines a `route` property for an HTTP trigger:</span></span>

```json
    {
      "bindings": [
        {
          "type": "httpTrigger",
          "name": "req",
          "direction": "in",
          "methods": [ "get" ],
          "route": "products/{category:alpha}/{id:int?}"
        },
        {
          "type": "http",
          "name": "res",
          "direction": "out"
        }
      ]
    }
```

<span data-ttu-id="af485-187">Za pomocą tej konfiguracji, funkcja jest teraz adresowanego trasa następujących zamiast oryginalnej trasy.</span><span class="sxs-lookup"><span data-stu-id="af485-187">Using this configuration, the function is now addressable with the following route instead of the original route.</span></span>

    http://<yourapp>.azurewebsites.net/api/products/electronics/357

<span data-ttu-id="af485-188">Dzięki temu funkcja kodu do obsługi dwóch parametrów w adres, "kategorii" i "id".</span><span class="sxs-lookup"><span data-stu-id="af485-188">This allows the function code to support two parameters in the address, "category" and "id".</span></span> <span data-ttu-id="af485-189">Można użyć dowolnego [ograniczenia trasy interfejsu API sieci Web](https://www.asp.net/web-api/overview/web-api-routing-and-actions/attribute-routing-in-web-api-2#constraints) z parametrami.</span><span class="sxs-lookup"><span data-stu-id="af485-189">You can use any [Web API Route Constraint](https://www.asp.net/web-api/overview/web-api-routing-and-actions/attribute-routing-in-web-api-2#constraints) with your parameters.</span></span> <span data-ttu-id="af485-190">Poniższy kod funkcji języka C# korzysta z obu tych parametrów.</span><span class="sxs-lookup"><span data-stu-id="af485-190">The following C# function code makes use of both parameters.</span></span>

```csharp
    public static Task<HttpResponseMessage> Run(HttpRequestMessage req, string category, int? id, 
                                                    TraceWriter log)
    {
        if (id == null)
           return  req.CreateResponse(HttpStatusCode.OK, $"All {category} items were requested.");
        else
           return  req.CreateResponse(HttpStatusCode.OK, $"{category} item with id = {id} has been requested.");
    }
```

<span data-ttu-id="af485-191">Oto kod funkcji Node.js do korzystania z tego samego parametrów trasy.</span><span class="sxs-lookup"><span data-stu-id="af485-191">Here is Node.js function code to use the same route parameters.</span></span>

```javascript
    module.exports = function (context, req) {

        var category = context.bindingData.category;
        var id = context.bindingData.id;

        if (!id) {
            context.res = {
                // status: 200, /* Defaults to 200 */
                body: "All " + category + " items were requested."
            };
        }
        else {
            context.res = {
                // status: 200, /* Defaults to 200 */
                body: category + " item with id = " + id + " was requested."
            };
        }

        context.done();
    } 
```

<span data-ttu-id="af485-192">Domyślnie wszystkie trasy funkcji są poprzedzane prefiksem *interfejsu api*.</span><span class="sxs-lookup"><span data-stu-id="af485-192">By default, all function routes are prefixed with *api*.</span></span> <span data-ttu-id="af485-193">Można również dostosować lub usunąć przy użyciu prefiksu `http.routePrefix` właściwości w Twojej *host.json* pliku.</span><span class="sxs-lookup"><span data-stu-id="af485-193">You can also customize or remove the prefix using the `http.routePrefix` property in your *host.json* file.</span></span> <span data-ttu-id="af485-194">Poniższy przykład umożliwia usunięcie *interfejsu api* prefiks trasy przy użyciu pustego ciągu dla prefiksu w *host.json* pliku.</span><span class="sxs-lookup"><span data-stu-id="af485-194">The following example removes the *api* route prefix by using an empty string for the prefix in the *host.json* file.</span></span>

```json
    {
      "http": {
        "routePrefix": ""
      }
    }
```

<span data-ttu-id="af485-195">Aby uzyskać szczegółowe informacje na temat aktualizowania *host.json* plików dla funkcji, zobacz [jak zaktualizować pliki aplikacji funkcji](functions-reference.md#fileupdate).</span><span class="sxs-lookup"><span data-stu-id="af485-195">For detailed information on how to update the *host.json* file for your function, See, [How to update function app files](functions-reference.md#fileupdate).</span></span> 

<span data-ttu-id="af485-196">Aby uzyskać informacje na temat innych właściwości można skonfigurować w sieci *host.json* plików, zobacz [odwołania host.json](https://github.com/Azure/azure-webjobs-sdk-script/wiki/host.json).</span><span class="sxs-lookup"><span data-stu-id="af485-196">For information on other properties you can configure in your *host.json* file, see [host.json reference](https://github.com/Azure/azure-webjobs-sdk-script/wiki/host.json).</span></span>


<a name="keys"></a>
## <a name="working-with-keys"></a><span data-ttu-id="af485-197">Praca z kluczy</span><span class="sxs-lookup"><span data-stu-id="af485-197">Working with keys</span></span>
<span data-ttu-id="af485-198">HttpTriggers mogą korzystać z kluczy w celu zwiększenia bezpieczeństwa.</span><span class="sxs-lookup"><span data-stu-id="af485-198">HttpTriggers can leverage keys for added security.</span></span> <span data-ttu-id="af485-199">Standardowe HttpTrigger służy je jako klucz interfejsu API wymagające klucza, który ma być obecne w żądaniu.</span><span class="sxs-lookup"><span data-stu-id="af485-199">A standard HttpTrigger can use these as an API key, requiring the key to be present on the request.</span></span> <span data-ttu-id="af485-200">Elementów Webhook można używać kluczy do autoryzowania żądań na różne sposoby, w zależności od tego, czy dostawca obsługuje.</span><span class="sxs-lookup"><span data-stu-id="af485-200">Webhooks can use keys to authorize requests in a variety of ways, depending on what the provider supports.</span></span>

<span data-ttu-id="af485-201">Klucze są przechowywane w ramach funkcji aplikacji na platformie Azure i są szyfrowane, gdy.</span><span class="sxs-lookup"><span data-stu-id="af485-201">Keys are stored as part of your function app in Azure and are encrypted at rest.</span></span> <span data-ttu-id="af485-202">Aby wyświetlić klucze, tworzenie nowych, lub Przywróć do nowych wartości kluczy, przejdź do jednej z funkcji w portalu i wybierz "Manage".</span><span class="sxs-lookup"><span data-stu-id="af485-202">To view your keys, create new ones, or roll keys to new values, navigate to one of your functions within the portal and select "Manage."</span></span> 

<span data-ttu-id="af485-203">Istnieją dwa typy kluczy:</span><span class="sxs-lookup"><span data-stu-id="af485-203">There are two types of keys:</span></span>
- <span data-ttu-id="af485-204">**Klucze hosta**: klucze te są współużytkowane przez wszystkie funkcje w ramach funkcji aplikacji.</span><span class="sxs-lookup"><span data-stu-id="af485-204">**Host keys**: These keys are shared by all functions within the function app.</span></span> <span data-ttu-id="af485-205">Gdy jest używany jako klucz interfejsu API, umożliwiają one dostęp do dowolnej funkcji w funkcji aplikacji.</span><span class="sxs-lookup"><span data-stu-id="af485-205">When used as an API key, these allow access to any function within the function app.</span></span>
- <span data-ttu-id="af485-206">**Klawisze funkcyjne**: te klucze mają zastosowanie tylko do określonych funkcji, w których są zdefiniowane.</span><span class="sxs-lookup"><span data-stu-id="af485-206">**Function keys**: These keys apply only to the specific functions under which they are defined.</span></span> <span data-ttu-id="af485-207">Gdy jest używany jako klucz interfejsu API, te tylko zezwolić na dostęp do tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="af485-207">When used as an API key, these only allow access to that function.</span></span>

<span data-ttu-id="af485-208">Każdy klucz nosi nazwę odwołania, a jest domyślny klucz (o nazwie "domyślne") na poziomie funkcji i hosta.</span><span class="sxs-lookup"><span data-stu-id="af485-208">Each key is named for reference, and there is a default key (named "default") at the function and host level.</span></span> <span data-ttu-id="af485-209">**Klucza głównego** domyślny klucz hosta o nazwie "_master", który jest zdefiniowany dla każdej funkcji aplikacji i nie może zostać odwołany.</span><span class="sxs-lookup"><span data-stu-id="af485-209">The **master key** is a default host key named "_master" that is defined for each function app and cannot be revoked.</span></span> <span data-ttu-id="af485-210">Zapewnia dostęp administracyjny do interfejsów API środowiska wykonawczego.</span><span class="sxs-lookup"><span data-stu-id="af485-210">It provides administrative access to the runtime APIs.</span></span> <span data-ttu-id="af485-211">Przy użyciu `"authLevel": "admin"` powiązanie JSON będzie wymagać tego klucza, aby być prezentowana na żądanie; innego klucza spowoduje błąd autoryzacji.</span><span class="sxs-lookup"><span data-stu-id="af485-211">Using `"authLevel": "admin"` in the binding JSON will require this key to be presented on the request; any other key will result in a authorization failure.</span></span>

> [!NOTE]
> <span data-ttu-id="af485-212">Z powodu podwyższonym poziomem uprawnień przyznanych przez klucz główny nie należy udostępnić ten klucz osobom trzecim ani rozpowszechnienie go w aplikacjach klienckich natywnego.</span><span class="sxs-lookup"><span data-stu-id="af485-212">Due to the elevated permissions granted by the master key, you should not share this key with third parties or distribute it in native client applications.</span></span> <span data-ttu-id="af485-213">Należy zachować ostrożność podczas wybierania poziom dostępu administratora.</span><span class="sxs-lookup"><span data-stu-id="af485-213">Exercise caution when choosing the admin authorization level.</span></span>
> 
> 

### <a name="api-key-authorization"></a><span data-ttu-id="af485-214">Autoryzacji klucza interfejsu API</span><span class="sxs-lookup"><span data-stu-id="af485-214">API key authorization</span></span>
<span data-ttu-id="af485-215">Domyślnie HttpTrigger wymaga klucza interfejsu API w żądaniu HTTP.</span><span class="sxs-lookup"><span data-stu-id="af485-215">By default, an HttpTrigger requires an API key in the HTTP request.</span></span> <span data-ttu-id="af485-216">Dlatego żądanie HTTP zwykle wygląda następująco:</span><span class="sxs-lookup"><span data-stu-id="af485-216">So your HTTP request normally looks like this:</span></span>

    https://<yourapp>.azurewebsites.net/api/<function>?code=<ApiKey>

<span data-ttu-id="af485-217">Klucz może być uwzględniony w zmiennej ciągu zapytania o nazwie `code`, zgodnie z powyższym, lub można je uwzględnić w `x-functions-key` nagłówka HTTP.</span><span class="sxs-lookup"><span data-stu-id="af485-217">The key can be included in a query string variable named `code`, as above, or it can be included in an `x-functions-key` HTTP header.</span></span> <span data-ttu-id="af485-218">Wartość klucza może być dowolny klawisz funkcji zdefiniowany dla funkcji lub dowolnego klucz hosta.</span><span class="sxs-lookup"><span data-stu-id="af485-218">The value of the key can be any function key defined for the function, or any host key.</span></span>

<span data-ttu-id="af485-219">Możesz zezwolić na żądania bez kluczy lub określ, że klucz główny musi być używane przez zmiana `authLevel` właściwości w powiązaniu JSON (zobacz [wyzwalacza HTTP](#httptrigger)).</span><span class="sxs-lookup"><span data-stu-id="af485-219">You can choose to allow requests without keys or specify that the master key must be used by changing the `authLevel` property in the binding JSON (see [HTTP trigger](#httptrigger)).</span></span>

### <a name="keys-and-webhooks"></a><span data-ttu-id="af485-220">Klucze i elementów webhook</span><span class="sxs-lookup"><span data-stu-id="af485-220">Keys and webhooks</span></span>
<span data-ttu-id="af485-221">Autoryzacji elementu Webhook jest obsługiwany przez składnik reciever elementu webhook część HttpTrigger, i mechanizmu w zależności od typu elementu webhook.</span><span class="sxs-lookup"><span data-stu-id="af485-221">Webhook authorization is handled by the webhook reciever component, part of the HttpTrigger, and the mechanism varies based on the webhook type.</span></span> <span data-ttu-id="af485-222">Nie mechanizmu, jednak zależne od klucza.</span><span class="sxs-lookup"><span data-stu-id="af485-222">Each mechanism does, however rely on a key.</span></span> <span data-ttu-id="af485-223">Domyślnie funkcja klucz o nazwie "domyślne" będzie używany.</span><span class="sxs-lookup"><span data-stu-id="af485-223">By default, the function key named "default" will be used.</span></span> <span data-ttu-id="af485-224">Jeśli chcesz użyć innego klucza, należy skonfigurować dostawcę elementu webhook można wysłać nazwę klucza z żądaniem w jednym z następujących sposobów:</span><span class="sxs-lookup"><span data-stu-id="af485-224">If you wish to use a different key, you will need to configure the webhook provider to send the key name with the request in one of the following ways:</span></span>

- <span data-ttu-id="af485-225">**Długość ciągu zapytania**: dostawca przekazuje nazwę klucza w `clientid` parametr ciągu zapytania (np. `https://<yourapp>.azurewebsites.net/api/<funcname>?clientid=<keyname>`).</span><span class="sxs-lookup"><span data-stu-id="af485-225">**Query string**: The provider passes the key name in the `clientid` query string parameter (e.g., `https://<yourapp>.azurewebsites.net/api/<funcname>?clientid=<keyname>`).</span></span>
- <span data-ttu-id="af485-226">**Nagłówek żądania**: dostawca przekazuje nazwę klucza w `x-functions-clientid` nagłówka.</span><span class="sxs-lookup"><span data-stu-id="af485-226">**Request header**: The provider passes the key name in the `x-functions-clientid` header.</span></span>

> [!NOTE]
> <span data-ttu-id="af485-227">Klawisze funkcyjne mają pierwszeństwo przed klucze hosta.</span><span class="sxs-lookup"><span data-stu-id="af485-227">Function keys take precedence over host keys.</span></span> <span data-ttu-id="af485-228">Jeśli dwa klucze są zdefiniowane z tą samą nazwą, będzie używany klawisze funkcyjne.</span><span class="sxs-lookup"><span data-stu-id="af485-228">If two keys are defined with the same name, the function key will be used.</span></span>
> 
> 


<a name="httptriggersample"></a>
## <a name="http-trigger-samples"></a><span data-ttu-id="af485-229">Przykłady wyzwalacza HTTP</span><span class="sxs-lookup"><span data-stu-id="af485-229">HTTP trigger samples</span></span>
<span data-ttu-id="af485-230">Załóżmy, że masz następujące wyzwalacza HTTP `bindings` tablicy function.json:</span><span class="sxs-lookup"><span data-stu-id="af485-230">Suppose you have the following HTTP trigger in the `bindings` array of function.json:</span></span>

```json
{
    "name": "req",
    "type": "httpTrigger",
    "direction": "in",
    "authLevel": "function"
},
```

<span data-ttu-id="af485-231">Zobacz przykład specyficzny dla języka, która sprawdza, czy `name` parametru w ciągu zapytania lub w treści żądania HTTP.</span><span class="sxs-lookup"><span data-stu-id="af485-231">See the language-specific sample that looks for a `name` parameter either in the query string or the body of the HTTP request.</span></span>

* [<span data-ttu-id="af485-232">C#</span><span class="sxs-lookup"><span data-stu-id="af485-232">C#</span></span>](#httptriggercsharp)
* [<span data-ttu-id="af485-233">F#</span><span class="sxs-lookup"><span data-stu-id="af485-233">F#</span></span>](#httptriggerfsharp)
* [<span data-ttu-id="af485-234">Node.js</span><span class="sxs-lookup"><span data-stu-id="af485-234">Node.js</span></span>](#httptriggernodejs)


<a name="httptriggercsharp"></a>
### <a name="http-trigger-sample-in-c"></a><span data-ttu-id="af485-235">Przykładowe wyzwalacza HTTP w języku C#</span><span class="sxs-lookup"><span data-stu-id="af485-235">HTTP trigger sample in C#</span></span> #
```csharp
using System.Net;
using System.Threading.Tasks;

public static async Task<HttpResponseMessage> Run(HttpRequestMessage req, TraceWriter log)
{
    log.Info($"C# HTTP trigger function processed a request. RequestUri={req.RequestUri}");

    // parse query parameter
    string name = req.GetQueryNameValuePairs()
        .FirstOrDefault(q => string.Compare(q.Key, "name", true) == 0)
        .Value;

    // Get request body
    dynamic data = await req.Content.ReadAsAsync<object>();

    // Set name to query string or body data
    name = name ?? data?.name;

    return name == null
        ? req.CreateResponse(HttpStatusCode.BadRequest, "Please pass a name on the query string or in the request body")
        : req.CreateResponse(HttpStatusCode.OK, "Hello " + name);
}
```

<span data-ttu-id="af485-236">Można także powiązać POCO zamiast `HttpRequestMessage`.</span><span class="sxs-lookup"><span data-stu-id="af485-236">You can also bind to a POCO instead of `HttpRequestMessage`.</span></span> <span data-ttu-id="af485-237">Spowoduje to uwodniony, z treści żądania jako JSON.</span><span class="sxs-lookup"><span data-stu-id="af485-237">This will be hydrated from the body of the request, parsed as JSON.</span></span> <span data-ttu-id="af485-238">Podobnie typu mogą być przekazywane dane wyjściowe odpowiedzi HTTP, powiązania i ta wartość jest zwracana jako treść odpowiedzi z kodem stanu 200.</span><span class="sxs-lookup"><span data-stu-id="af485-238">Similarly, a type can be passed to the HTTP response output binding, and this will be returned as the response body, with a 200 status code.</span></span>
```csharp
using System.Net;
using System.Threading.Tasks;

public static string Run(CustomObject req, TraceWriter log)
{
    return "Hello " + req?.name;
}

public class CustomObject {
     public String name {get; set;}
}
}
```

<a name="httptriggerfsharp"></a>
### <a name="http-trigger-sample-in-f"></a><span data-ttu-id="af485-239">Przykładowe wyzwalacza HTTP w języku F #</span><span class="sxs-lookup"><span data-stu-id="af485-239">HTTP trigger sample in F#</span></span> #
```fsharp
open System.Net
open System.Net.Http
open FSharp.Interop.Dynamic

let Run(req: HttpRequestMessage) =
    async {
        let q =
            req.GetQueryNameValuePairs()
                |> Seq.tryFind (fun kv -> kv.Key = "name")
        match q with
        | Some kv ->
            return req.CreateResponse(HttpStatusCode.OK, "Hello " + kv.Value)
        | None ->
            let! data = Async.AwaitTask(req.Content.ReadAsAsync<obj>())
            try
                return req.CreateResponse(HttpStatusCode.OK, "Hello " + data?name)
            with e ->
                return req.CreateErrorResponse(HttpStatusCode.BadRequest, "Please pass a name on the query string or in the request body")
    } |> Async.StartAsTask
```

<span data-ttu-id="af485-240">Należy `project.json` pliku, który używa NuGet, aby odwołać `FSharp.Interop.Dynamic` i `Dynamitey` zestawów, w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="af485-240">You need a `project.json` file that uses NuGet to reference the `FSharp.Interop.Dynamic` and `Dynamitey` assemblies, like this:</span></span>

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

<span data-ttu-id="af485-241">Zostanie użyty NuGet na pobieranie zależności i odwoływać je w skrypcie.</span><span class="sxs-lookup"><span data-stu-id="af485-241">This will use NuGet to fetch your dependencies and will reference them in your script.</span></span>

<a name="httptriggernodejs"></a>
### <a name="http-trigger-sample-in-nodejs"></a><span data-ttu-id="af485-242">Przykładowe wyzwalacza HTTP w środowisku Node.JS</span><span class="sxs-lookup"><span data-stu-id="af485-242">HTTP trigger sample in Node.JS</span></span>
```javascript
module.exports = function(context, req) {
    context.log('Node.js HTTP trigger function processed a request. RequestUri=%s', req.originalUrl);

    if (req.query.name || (req.body && req.body.name)) {
        context.res = {
            // status: 200, /* Defaults to 200 */
            body: "Hello " + (req.query.name || req.body.name)
        };
    }
    else {
        context.res = {
            status: 400,
            body: "Please pass a name on the query string or in the request body"
        };
    }
    context.done();
};
```



<a name="hooktriggersample"></a>
## <a name="webhook-samples"></a><span data-ttu-id="af485-243">Przykłady elementu Webhook</span><span class="sxs-lookup"><span data-stu-id="af485-243">Webhook samples</span></span>
<span data-ttu-id="af485-244">Załóżmy, że masz następujące wyzwalacza elementu webhook `bindings` tablicy function.json:</span><span class="sxs-lookup"><span data-stu-id="af485-244">Suppose you have the following webhook trigger in the `bindings` array of function.json:</span></span>

```json
{
    "webHookType": "github",
    "name": "req",
    "type": "httpTrigger",
    "direction": "in",
},
```

<span data-ttu-id="af485-245">Patrz zaloguje się komentarze problem GitHub próbki specyficzny dla języka.</span><span class="sxs-lookup"><span data-stu-id="af485-245">See the language-specific sample that logs GitHub issue comments.</span></span>

* [<span data-ttu-id="af485-246">C#</span><span class="sxs-lookup"><span data-stu-id="af485-246">C#</span></span>](#hooktriggercsharp)
* [<span data-ttu-id="af485-247">F#</span><span class="sxs-lookup"><span data-stu-id="af485-247">F#</span></span>](#hooktriggerfsharp)
* [<span data-ttu-id="af485-248">Node.js</span><span class="sxs-lookup"><span data-stu-id="af485-248">Node.js</span></span>](#hooktriggernodejs)

<a name="hooktriggercsharp"></a>

### <a name="webhook-sample-in-c"></a><span data-ttu-id="af485-249">Przykład elementu Webhook w języku C#</span><span class="sxs-lookup"><span data-stu-id="af485-249">Webhook sample in C#</span></span> #
```csharp
#r "Newtonsoft.Json"

using System;
using System.Net;
using System.Threading.Tasks;
using Newtonsoft.Json;

public static async Task<object> Run(HttpRequestMessage req, TraceWriter log)
{
    string jsonContent = await req.Content.ReadAsStringAsync();
    dynamic data = JsonConvert.DeserializeObject(jsonContent);

    log.Info($"WebHook was triggered! Comment: {data.comment.body}");

    return req.CreateResponse(HttpStatusCode.OK, new {
        body = $"New GitHub comment: {data.comment.body}"
    });
}
```

<a name="hooktriggerfsharp"></a>

### <a name="webhook-sample-in-f"></a><span data-ttu-id="af485-250">Przykład elementu Webhook w języku F #</span><span class="sxs-lookup"><span data-stu-id="af485-250">Webhook sample in F#</span></span> #
```fsharp
open System.Net
open System.Net.Http
open FSharp.Interop.Dynamic
open Newtonsoft.Json

type Response = {
    body: string
}

let Run(req: HttpRequestMessage, log: TraceWriter) =
    async {
        let! content = req.Content.ReadAsStringAsync() |> Async.AwaitTask
        let data = content |> JsonConvert.DeserializeObject
        log.Info(sprintf "GitHub WebHook triggered! %s" data?comment?body)
        return req.CreateResponse(
            HttpStatusCode.OK,
            { body = sprintf "New GitHub comment: %s" data?comment?body })
    } |> Async.StartAsTask
```

<a name="hooktriggernodejs"></a>

### <a name="webhook-sample-in-nodejs"></a><span data-ttu-id="af485-251">Przykład elementu Webhook w środowisku Node.JS</span><span class="sxs-lookup"><span data-stu-id="af485-251">Webhook sample in Node.JS</span></span>
```javascript
module.exports = function (context, data) {
    context.log('GitHub WebHook triggered!', data.comment.body);
    context.res = { body: 'New GitHub comment: ' + data.comment.body };
    context.done();
};
```


## <a name="next-steps"></a><span data-ttu-id="af485-252">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="af485-252">Next steps</span></span>
[!INCLUDE [next steps](../../includes/functions-bindings-next-steps.md)]

