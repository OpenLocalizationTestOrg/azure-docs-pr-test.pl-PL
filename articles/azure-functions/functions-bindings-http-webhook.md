---
title: "powiązania HTTP funkcje i elementu webhook aaaAzure | Dokumentacja firmy Microsoft"
description: "Zrozumienie, jak wyzwala toouse HTTP i elementu webhook i powiązania usługi Azure Functions."
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
ms.openlocfilehash: c23b7a1443d492ed78c595e97d1d778a7ab12416
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-functions-http-and-webhook-bindings"></a><span data-ttu-id="55253-104">Azure powiązania HTTP funkcje i elementu webhook</span><span class="sxs-lookup"><span data-stu-id="55253-104">Azure Functions HTTP and webhook bindings</span></span>
[!INCLUDE [functions-selector-bindings](../../includes/functions-selector-bindings.md)]

<span data-ttu-id="55253-105">W tym artykule opisano, jak wyzwala tooconfigure i korzystają z protokołu HTTP i powiązania usługi Azure Functions.</span><span class="sxs-lookup"><span data-stu-id="55253-105">This article explains how tooconfigure and work with HTTP triggers and bindings in Azure Functions.</span></span>
<span data-ttu-id="55253-106">Z tych opcji możesz użyć usługi Azure Functions toobuild niekorzystającą interfejsów API i odpowiedź toowebhooks.</span><span class="sxs-lookup"><span data-stu-id="55253-106">With these, you can use Azure Functions toobuild serverless APIs and respond toowebhooks.</span></span>

<span data-ttu-id="55253-107">Środowisko Azure Functions zapewnia następujące powiązania hello:</span><span class="sxs-lookup"><span data-stu-id="55253-107">Azure Functions provides hello following bindings:</span></span>
- <span data-ttu-id="55253-108">[Wyzwalacza HTTP](#httptrigger) umożliwia wywołanie funkcji z żądania HTTP.</span><span class="sxs-lookup"><span data-stu-id="55253-108">An [HTTP trigger](#httptrigger) lets you invoke a function with an HTTP request.</span></span> <span data-ttu-id="55253-109">Może to być dostosowane toorespond zbyt[elementów webhook](#hooktrigger).</span><span class="sxs-lookup"><span data-stu-id="55253-109">This can be customized toorespond too[webhooks](#hooktrigger).</span></span>
- <span data-ttu-id="55253-110">[Powiązania wyjściowego HTTP](#output) pozwala toorespond toohello żądania.</span><span class="sxs-lookup"><span data-stu-id="55253-110">An [HTTP output binding](#output) allows you toorespond toohello request.</span></span>

[!INCLUDE [intro](../../includes/functions-bindings-intro.md)]

[!INCLUDE [HTTP client best practices](../../includes/functions-http-client-best-practices.md)]

<a name="httptrigger"></a>

## <a name="http-trigger"></a><span data-ttu-id="55253-111">Wyzwalacz HTTP</span><span class="sxs-lookup"><span data-stu-id="55253-111">HTTP trigger</span></span>
<span data-ttu-id="55253-112">wyzwalacza HTTP Hello wykona funkcja w żądaniu HTTP tooan odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="55253-112">hello HTTP trigger will execute your function in response tooan HTTP request.</span></span> <span data-ttu-id="55253-113">Można go dostosować toorespond tooa określonego adresu URL lub zestawu metod HTTP.</span><span class="sxs-lookup"><span data-stu-id="55253-113">You can customize it toorespond tooa particular URL or set of HTTP methods.</span></span> <span data-ttu-id="55253-114">Wyzwalacz HTTP może być również skonfigurowany toorespond toowebhooks.</span><span class="sxs-lookup"><span data-stu-id="55253-114">An HTTP trigger can also be configured toorespond toowebhooks.</span></span> 

<span data-ttu-id="55253-115">Jeśli za pomocą portalu funkcje hello, można również rozpocząć od razu przy użyciu predefiniowanych szablonów.</span><span class="sxs-lookup"><span data-stu-id="55253-115">If using hello Functions portal, you can also get started right away using a pre-made template.</span></span> <span data-ttu-id="55253-116">Wybierz **nową funkcję** i wybierz polecenie "Interfejsu API i elementów Webhook" z hello **scenariusza** listy rozwijanej.</span><span class="sxs-lookup"><span data-stu-id="55253-116">Select **New function** and choose "API & Webhooks" from hello **Scenario** dropdown.</span></span> <span data-ttu-id="55253-117">Wybierz jeden z szablonów hello, a następnie kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="55253-117">Select one of hello templates and click **Create**.</span></span>

<span data-ttu-id="55253-118">Domyślnie wyzwalacza HTTP będzie odpowiadać na żądania toohello z kodem stanu HTTP 200 OK i pustej treści.</span><span class="sxs-lookup"><span data-stu-id="55253-118">By default, an HTTP trigger will respond toohello request with an HTTP 200 OK status code and an empty body.</span></span> <span data-ttu-id="55253-119">toomodify hello odpowiedzi, skonfigurować [powiązania wyjściowego HTTP](#output)</span><span class="sxs-lookup"><span data-stu-id="55253-119">toomodify hello response, configure an [HTTP output binding](#output)</span></span>

### <a name="configuring-an-http-trigger"></a><span data-ttu-id="55253-120">Konfigurowanie wyzwalacza HTTP</span><span class="sxs-lookup"><span data-stu-id="55253-120">Configuring an HTTP trigger</span></span>
<span data-ttu-id="55253-121">Wyzwalacz protokołu HTTP jest zdefiniowany przez dołączenie JSON obiektu toohello podobne, po w hello `bindings` tablicy function.json:</span><span class="sxs-lookup"><span data-stu-id="55253-121">An HTTP trigger is defined by including a JSON object similar toohello following in hello `bindings` array of function.json:</span></span>

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
<span data-ttu-id="55253-122">Powiązanie Hello obsługuje hello następujące właściwości:</span><span class="sxs-lookup"><span data-stu-id="55253-122">hello binding supports hello following properties:</span></span>

* <span data-ttu-id="55253-123">**Nazwa** : wymagana — nazwa zmiennej hello używane w kodzie funkcji żądania hello lub treści żądania.</span><span class="sxs-lookup"><span data-stu-id="55253-123">**name** : Required - hello variable name used in function code for hello request or request body.</span></span> <span data-ttu-id="55253-124">Zobacz [Praca z wyzwalacza HTTP z kodu](#httptriggerusage).</span><span class="sxs-lookup"><span data-stu-id="55253-124">See [Working with an HTTP trigger from code](#httptriggerusage).</span></span>
* <span data-ttu-id="55253-125">**Typ** : wymagana — musi być ustawiona zbyt "httpTrigger".</span><span class="sxs-lookup"><span data-stu-id="55253-125">**type** : Required - must be set too"httpTrigger".</span></span>
* <span data-ttu-id="55253-126">**kierunek** : wymagana — musi być ustawiona zbyt "w".</span><span class="sxs-lookup"><span data-stu-id="55253-126">**direction** : Required - must be set too"in".</span></span>
* <span data-ttu-id="55253-127">_authLevel_ : Określa, jakie klucze, należy toobe obecne w żądaniu hello w kolejności tooinvoke hello funkcji.</span><span class="sxs-lookup"><span data-stu-id="55253-127">_authLevel_ : This determines what keys, if any, need toobe present on hello request in order tooinvoke hello function.</span></span> <span data-ttu-id="55253-128">Zobacz [Praca z kluczami](#keys) poniżej.</span><span class="sxs-lookup"><span data-stu-id="55253-128">See [Working with keys](#keys) below.</span></span> <span data-ttu-id="55253-129">wartość Hello może być jedną z następujących hello:</span><span class="sxs-lookup"><span data-stu-id="55253-129">hello value can be one of hello following:</span></span>
    * <span data-ttu-id="55253-130">_anonimowe_: klucz interfejsu API nie jest wymagana.</span><span class="sxs-lookup"><span data-stu-id="55253-130">_anonymous_: No API key is required.</span></span>
    * <span data-ttu-id="55253-131">_Funkcja_: wymagany jest klucz interfejsu API właściwe dla funkcji.</span><span class="sxs-lookup"><span data-stu-id="55253-131">_function_: A function-specific API key is required.</span></span> <span data-ttu-id="55253-132">Jeśli nie zostanie podana jest wartość domyślna hello.</span><span class="sxs-lookup"><span data-stu-id="55253-132">This is hello default value if none is provided.</span></span>
    * <span data-ttu-id="55253-133">_Administrator_ : jest wymagany klucz główny hello.</span><span class="sxs-lookup"><span data-stu-id="55253-133">_admin_ : hello master key is required.</span></span>
* <span data-ttu-id="55253-134">**metody** : to jest tablica metod hello HTTP będzie odpowiadać toowhich hello funkcji.</span><span class="sxs-lookup"><span data-stu-id="55253-134">**methods** : This is an array of hello HTTP methods toowhich hello function will respond.</span></span> <span data-ttu-id="55253-135">Jeśli nie zostanie określony, funkcja hello będzie odpowiadać metody tooall HTTP.</span><span class="sxs-lookup"><span data-stu-id="55253-135">If not specified, hello function will respond tooall HTTP methods.</span></span> <span data-ttu-id="55253-136">Zobacz [Dostosowywanie punktu końcowego hello HTTP](#url).</span><span class="sxs-lookup"><span data-stu-id="55253-136">See [Customizing hello HTTP endpoint](#url).</span></span>
* <span data-ttu-id="55253-137">**trasy** : Określa szablon trasy hello, kontrolowanie toowhich adresów URL będzie odpowiadać funkcji żądań.</span><span class="sxs-lookup"><span data-stu-id="55253-137">**route** : This defines hello route template, controlling toowhich request URLs your function will respond.</span></span> <span data-ttu-id="55253-138">Witaj wartość domyślną, jeśli nie zostanie podana jest `<functionname>`.</span><span class="sxs-lookup"><span data-stu-id="55253-138">hello default value if none is provided is `<functionname>`.</span></span> <span data-ttu-id="55253-139">Zobacz [Dostosowywanie punktu końcowego hello HTTP](#url).</span><span class="sxs-lookup"><span data-stu-id="55253-139">See [Customizing hello HTTP endpoint](#url).</span></span>
* <span data-ttu-id="55253-140">**webHookType** : spowoduje to skonfigurowanie tooact wyzwalacza hello HTTP jako reciever elementu webhook dla hello określonego dostawcy.</span><span class="sxs-lookup"><span data-stu-id="55253-140">**webHookType** : This configures hello HTTP trigger tooact as a webhook reciever for hello specified provider.</span></span> <span data-ttu-id="55253-141">Witaj _metody_ właściwość nie powinna być ustawiona, jeśli to jest wybrane.</span><span class="sxs-lookup"><span data-stu-id="55253-141">hello _methods_ property should not be set if this is chosen.</span></span> <span data-ttu-id="55253-142">Zobacz [toowebhooks odpowiada](#hooktrigger).</span><span class="sxs-lookup"><span data-stu-id="55253-142">See [Responding toowebhooks](#hooktrigger).</span></span> <span data-ttu-id="55253-143">wartość Hello może być jedną z następujących hello:</span><span class="sxs-lookup"><span data-stu-id="55253-143">hello value can be one of hello following:</span></span>
    * <span data-ttu-id="55253-144">_genericJson_ : punkt końcowy elementu webhook ogólnego przeznaczenia bez logiki dla określonego dostawcy.</span><span class="sxs-lookup"><span data-stu-id="55253-144">_genericJson_ : A general purpose webhook endpoint without logic for a specific provider.</span></span>
    * <span data-ttu-id="55253-145">_github_ : funkcja hello będzie odpowiadać tooGitHub elementów webhook.</span><span class="sxs-lookup"><span data-stu-id="55253-145">_github_ : hello function will respond tooGitHub webhooks.</span></span> <span data-ttu-id="55253-146">Witaj _authLevel_ właściwość nie powinna być ustawiona, jeśli to jest wybrane.</span><span class="sxs-lookup"><span data-stu-id="55253-146">hello _authLevel_ property should not be set if this is chosen.</span></span>
    * <span data-ttu-id="55253-147">_zapas czasu_ : funkcja hello będzie odpowiadać tooSlack elementów webhook.</span><span class="sxs-lookup"><span data-stu-id="55253-147">_slack_ : hello function will respond tooSlack webhooks.</span></span> <span data-ttu-id="55253-148">Witaj _authLevel_ właściwość nie powinna być ustawiona, jeśli to jest wybrane.</span><span class="sxs-lookup"><span data-stu-id="55253-148">hello _authLevel_ property should not be set if this is chosen.</span></span>

<a name="httptriggerusage"></a>
### <a name="working-with-an-http-trigger-from-code"></a><span data-ttu-id="55253-149">Praca z wyzwalacza HTTP z kodu</span><span class="sxs-lookup"><span data-stu-id="55253-149">Working with an HTTP trigger from code</span></span>
<span data-ttu-id="55253-150">Dla funkcji języka C# i F #, mogą zadeklarować typu hello Twojej toobe wejściowych wyzwalacza albo `HttpRequestMessage` lub typu niestandardowego.</span><span class="sxs-lookup"><span data-stu-id="55253-150">For C# and F# functions, you can declare hello type of your trigger input toobe either `HttpRequestMessage` or a custom type.</span></span> <span data-ttu-id="55253-151">Jeśli wybierzesz `HttpRequestMessage`, a następnie pobierze obiektu żądania toohello pełny dostęp.</span><span class="sxs-lookup"><span data-stu-id="55253-151">If you choose `HttpRequestMessage`, then you will get full access toohello request object.</span></span> <span data-ttu-id="55253-152">Dla typu niestandardowego (na przykład POCO) funkcje podejmie treści żądania hello tooparse jako właściwości obiektu hello toopopulate JSON.</span><span class="sxs-lookup"><span data-stu-id="55253-152">For a custom type (such as a POCO), Functions will attempt tooparse hello request body as JSON toopopulate hello object properties.</span></span>

<span data-ttu-id="55253-153">W przypadku funkcji Node.js środowisko uruchomieniowe Functions hello zapewnia treści żądania hello zamiast obiektu żądania hello.</span><span class="sxs-lookup"><span data-stu-id="55253-153">For Node.js functions, hello Functions runtime provides hello request body instead of hello request object.</span></span>

<span data-ttu-id="55253-154">Zobacz [przykłady wyzwalacza HTTP](#httptriggersample) na przykład sposobu użycia.</span><span class="sxs-lookup"><span data-stu-id="55253-154">See [HTTP trigger samples](#httptriggersample) for example usages.</span></span>


<a name="output"></a>
## <a name="http-response-output-binding"></a><span data-ttu-id="55253-155">Powiązania wyjściowego odpowiedzi HTTP</span><span class="sxs-lookup"><span data-stu-id="55253-155">HTTP response output binding</span></span>
<span data-ttu-id="55253-156">Użyj hello HTTP dane wyjściowe powiązania toorespond toohello HTTP żądania nadawcy.</span><span class="sxs-lookup"><span data-stu-id="55253-156">Use hello HTTP output binding toorespond toohello HTTP request sender.</span></span> <span data-ttu-id="55253-157">To powiązanie wymaga wyzwalacza HTTP i pozwala odpowiedź hello toocustomize skojarzony z żądaniem hello wyzwalacza.</span><span class="sxs-lookup"><span data-stu-id="55253-157">This binding requires an HTTP trigger and allows you toocustomize hello response associated with hello trigger's request.</span></span> <span data-ttu-id="55253-158">Jeśli powiązania wyjściowego HTTP nie zostanie podany, wyzwalacz HTTP zwróci o pustej treści HTTP 200 OK.</span><span class="sxs-lookup"><span data-stu-id="55253-158">If an HTTP output binding is not provided, an HTTP trigger will return HTTP 200 OK with an empty body.</span></span> 

### <a name="configuring-an-http-output-binding"></a><span data-ttu-id="55253-159">Konfigurowanie protokołu HTTP powiązania wyjściowego</span><span class="sxs-lookup"><span data-stu-id="55253-159">Configuring an HTTP output binding</span></span>
<span data-ttu-id="55253-160">Hello HTTP output powiązania jest definiowana za pomocą tym JSON obiektu toohello podobne, po w hello `bindings` tablicy function.json:</span><span class="sxs-lookup"><span data-stu-id="55253-160">hello HTTP output binding is defined by including a JSON object similar toohello following in hello `bindings` array of function.json:</span></span>

```json
{
    "name": "res",
    "type": "http",
    "direction": "out"
}
```
<span data-ttu-id="55253-161">Powiązanie Hello zawiera hello następujące właściwości:</span><span class="sxs-lookup"><span data-stu-id="55253-161">hello binding contains hello following properties:</span></span>

* <span data-ttu-id="55253-162">**Nazwa** : wymagana — Witaj używane w kodzie funkcja odpowiedź hello nazwy zmiennej.</span><span class="sxs-lookup"><span data-stu-id="55253-162">**name** : Required - hello variable name used in function code for hello response.</span></span> <span data-ttu-id="55253-163">Zobacz [powiązania z kodu wyjściowego roboczych protokołu HTTP z](#outputusage).</span><span class="sxs-lookup"><span data-stu-id="55253-163">See [Working with an HTTP output binding from code](#outputusage).</span></span>
* <span data-ttu-id="55253-164">**Typ** : wymagana — musi być ustawiona zbyt "http".</span><span class="sxs-lookup"><span data-stu-id="55253-164">**type** : Required - must be set too"http".</span></span>
* <span data-ttu-id="55253-165">**kierunek** : wymagana — musi być ustawiona zbyt "out".</span><span class="sxs-lookup"><span data-stu-id="55253-165">**direction** : Required - must be set too"out".</span></span>

<a name="outputusage"></a>
### <a name="working-with-an-http-output-binding-from-code"></a><span data-ttu-id="55253-166">Praca z HTTP output powiązania z kodu</span><span class="sxs-lookup"><span data-stu-id="55253-166">Working with an HTTP output binding from code</span></span>
<span data-ttu-id="55253-167">Możesz użyć hello dane wyjściowe parametru (np. "res") toorespond toohello http lub elementu webhook wywołującego.</span><span class="sxs-lookup"><span data-stu-id="55253-167">You can use hello output parameter (e.g., "res") toorespond toohello http or webhook caller.</span></span> <span data-ttu-id="55253-168">Alternatywnie można użyć standardowego `Request.CreateResponse()` (C#) lub `context.res` tooreturn wzorca (Node.JS) do odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="55253-168">Alternatively, you can use the standard `Request.CreateResponse()` (C#) or `context.res` (Node.JS) pattern tooreturn your response.</span></span> <span data-ttu-id="55253-169">Przykłady w sposób toouse hello druga metoda, zobacz [przykłady wyzwalacza HTTP](#httptriggersample) i [przykłady wyzwalacza elementu Webhook](#hooktriggersample).</span><span class="sxs-lookup"><span data-stu-id="55253-169">For examples on how toouse hello latter method, see [HTTP trigger samples](#httptriggersample) and [Webhook trigger samples](#hooktriggersample).</span></span>


<a name="hooktrigger"></a>
## <a name="responding-toowebhooks"></a><span data-ttu-id="55253-170">Odpowiada toowebhooks</span><span class="sxs-lookup"><span data-stu-id="55253-170">Responding toowebhooks</span></span>
<span data-ttu-id="55253-171">Wyzwalacz protokołu HTTP z hello _webHookType_ właściwość będzie skonfigurowany toorespond zbyt[elementów webhook](https://en.wikipedia.org/wiki/Webhook).</span><span class="sxs-lookup"><span data-stu-id="55253-171">An HTTP trigger with hello _webHookType_ property will be configured toorespond too[webhooks](https://en.wikipedia.org/wiki/Webhook).</span></span> <span data-ttu-id="55253-172">Podstawowa konfiguracja Hello używa ustawienia "genericJson" hello.</span><span class="sxs-lookup"><span data-stu-id="55253-172">hello basic configuration uses hello "genericJson" setting.</span></span> <span data-ttu-id="55253-173">Umożliwia ograniczenie żądań tooonly tych przy użyciu protokołu HTTP POST i hello `application/json` typ zawartości.</span><span class="sxs-lookup"><span data-stu-id="55253-173">This restricts requests tooonly those using HTTP POST and with hello `application/json` content type.</span></span>

<span data-ttu-id="55253-174">Witaj wyzwalacza można dodatkowo dopasowane tooa webhook określonego dostawcy (np. [GitHub](https://developer.github.com/webhooks/) i [Slack](https://api.slack.com/outgoing-webhooks)).</span><span class="sxs-lookup"><span data-stu-id="55253-174">hello trigger can additionally be tailored tooa specific webhook provider (e.g., [GitHub](https://developer.github.com/webhooks/) and [Slack](https://api.slack.com/outgoing-webhooks)).</span></span> <span data-ttu-id="55253-175">Jeśli jest określony dostawca, środowisko uruchomieniowe Functions hello zająć się dostawcy hello logikę weryfikacji dla Ciebie.</span><span class="sxs-lookup"><span data-stu-id="55253-175">If a provider is specified, hello Functions runtime can take care of hello provider's validation logic for you.</span></span>  

### <a name="configuring-github-as-a-webhook-provider"></a><span data-ttu-id="55253-176">Konfigurowanie dostawcy elementu webhook GitHub</span><span class="sxs-lookup"><span data-stu-id="55253-176">Configuring GitHub as a webhook provider</span></span>
<span data-ttu-id="55253-177">toorespond tooGitHub elementów webhook, najpierw utwórz funkcji z wyzwalaczem HTTP i ustaw hello _webHookType_ właściwości zbyt "github".</span><span class="sxs-lookup"><span data-stu-id="55253-177">toorespond tooGitHub webhooks, first create your function with an HTTP Trigger, and set hello _webHookType_ property too"github".</span></span> <span data-ttu-id="55253-178">Następnie skopiuj jej [adres URL](#url) i [klucz interfejsu API](#keys) w repozytorium GitHub **Dodawanie elementu webhook** strony.</span><span class="sxs-lookup"><span data-stu-id="55253-178">Then copy its [URL](#url) and [API key](#keys) into your GitHub repository's **Add webhook** page.</span></span> <span data-ttu-id="55253-179">Zobacz GitHub [tworzenia elementów Webhook](http://go.microsoft.com/fwlink/?LinkID=761099&clcid=0x409) dokumentacji, aby uzyskać więcej informacji.</span><span class="sxs-lookup"><span data-stu-id="55253-179">See GitHub's [Creating Webhooks](http://go.microsoft.com/fwlink/?LinkID=761099&clcid=0x409) documentation for more.</span></span>

![](./media/functions-bindings-http-webhook/github-add-webhook.png)

### <a name="configuring-slack-as-a-webhook-provider"></a><span data-ttu-id="55253-180">Konfigurowanie zapas czasu jako dostawca elementu webhook</span><span class="sxs-lookup"><span data-stu-id="55253-180">Configuring Slack as a webhook provider</span></span>
<span data-ttu-id="55253-181">Hello Slack webhook generuje token dla Ciebie zamiast czekać na określeniu, dlatego należy skonfigurować klucz właściwe dla funkcji z tokenem hello z zapas czasu.</span><span class="sxs-lookup"><span data-stu-id="55253-181">hello Slack webhook generates a token for you instead of letting you specify it, so you must configure a function-specific key with hello token from Slack.</span></span> <span data-ttu-id="55253-182">Zobacz [Praca z kluczami](#keys).</span><span class="sxs-lookup"><span data-stu-id="55253-182">See [Working with keys](#keys).</span></span>

<a name="url"></a>
## <a name="customizing-hello-http-endpoint"></a><span data-ttu-id="55253-183">Dostosowywanie hello punkt końcowy HTTP</span><span class="sxs-lookup"><span data-stu-id="55253-183">Customizing hello HTTP endpoint</span></span>
<span data-ttu-id="55253-184">Domyślnie podczas tworzenia funkcja wyzwalacza HTTP lub elementu WebHook, funkcja hello jest adresowanego trasa hello formularza:</span><span class="sxs-lookup"><span data-stu-id="55253-184">By default when you create a function for an HTTP trigger, or WebHook, hello function is addressable with a route of hello form:</span></span>

    http://<yourapp>.azurewebsites.net/api/<funcname> 

<span data-ttu-id="55253-185">Można dostosować tej trasy, używając hello opcjonalne `route` wejściowych powiązania właściwości dla elementu trigger hello HTTP.</span><span class="sxs-lookup"><span data-stu-id="55253-185">You can customize this route using hello optional `route` property on hello HTTP trigger's input binding.</span></span> <span data-ttu-id="55253-186">Przykład Witaj po *function.json* plik definiuje `route` właściwości dla wyzwalacza HTTP:</span><span class="sxs-lookup"><span data-stu-id="55253-186">As an example, hello following *function.json* file defines a `route` property for an HTTP trigger:</span></span>

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

<span data-ttu-id="55253-187">Za pomocą tej konfiguracji, funkcja hello jest teraz adresowanego z hello następujące trasy zamiast hello oryginalnego trasy.</span><span class="sxs-lookup"><span data-stu-id="55253-187">Using this configuration, hello function is now addressable with hello following route instead of hello original route.</span></span>

    http://<yourapp>.azurewebsites.net/api/products/electronics/357

<span data-ttu-id="55253-188">Dzięki temu kod funkcji hello toosupport dwa parametry adres Witaj, "kategorii" i "id".</span><span class="sxs-lookup"><span data-stu-id="55253-188">This allows hello function code toosupport two parameters in hello address, "category" and "id".</span></span> <span data-ttu-id="55253-189">Można użyć dowolnego [ograniczenia trasy interfejsu API sieci Web](https://www.asp.net/web-api/overview/web-api-routing-and-actions/attribute-routing-in-web-api-2#constraints) z parametrami.</span><span class="sxs-lookup"><span data-stu-id="55253-189">You can use any [Web API Route Constraint](https://www.asp.net/web-api/overview/web-api-routing-and-actions/attribute-routing-in-web-api-2#constraints) with your parameters.</span></span> <span data-ttu-id="55253-190">Witaj następującego kodu funkcji języka C# korzysta z obu tych parametrów.</span><span class="sxs-lookup"><span data-stu-id="55253-190">hello following C# function code makes use of both parameters.</span></span>

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

<span data-ttu-id="55253-191">Oto hello toouse kodu funkcji Node.js takie same parametry trasy.</span><span class="sxs-lookup"><span data-stu-id="55253-191">Here is Node.js function code toouse hello same route parameters.</span></span>

```javascript
    module.exports = function (context, req) {

        var category = context.bindingData.category;
        var id = context.bindingData.id;

        if (!id) {
            context.res = {
                // status: 200, /* Defaults too200 */
                body: "All " + category + " items were requested."
            };
        }
        else {
            context.res = {
                // status: 200, /* Defaults too200 */
                body: category + " item with id = " + id + " was requested."
            };
        }

        context.done();
    } 
```

<span data-ttu-id="55253-192">Domyślnie wszystkie trasy funkcji są poprzedzane prefiksem *interfejsu api*.</span><span class="sxs-lookup"><span data-stu-id="55253-192">By default, all function routes are prefixed with *api*.</span></span> <span data-ttu-id="55253-193">Można również dostosować lub usuń prefiks hello przy użyciu hello `http.routePrefix` właściwości w Twojej *host.json* pliku.</span><span class="sxs-lookup"><span data-stu-id="55253-193">You can also customize or remove hello prefix using hello `http.routePrefix` property in your *host.json* file.</span></span> <span data-ttu-id="55253-194">Witaj poniższy przykład umożliwia usunięcie hello *interfejsu api* prefiks trasy przy użyciu pustego ciągu dla prefiksu hello w hello *host.json* pliku.</span><span class="sxs-lookup"><span data-stu-id="55253-194">hello following example removes hello *api* route prefix by using an empty string for hello prefix in hello *host.json* file.</span></span>

```json
    {
      "http": {
        "routePrefix": ""
      }
    }
```

<span data-ttu-id="55253-195">Aby uzyskać szczegółowe informacje na temat tooupdate hello *host.json* plików dla funkcji, zobacz [jak tooupdate funkcji pliki aplikacji](functions-reference.md#fileupdate).</span><span class="sxs-lookup"><span data-stu-id="55253-195">For detailed information on how tooupdate hello *host.json* file for your function, See, [How tooupdate function app files](functions-reference.md#fileupdate).</span></span> 

<span data-ttu-id="55253-196">Aby uzyskać informacje na temat innych właściwości można skonfigurować w sieci *host.json* plików, zobacz [odwołania host.json](https://github.com/Azure/azure-webjobs-sdk-script/wiki/host.json).</span><span class="sxs-lookup"><span data-stu-id="55253-196">For information on other properties you can configure in your *host.json* file, see [host.json reference](https://github.com/Azure/azure-webjobs-sdk-script/wiki/host.json).</span></span>


<a name="keys"></a>
## <a name="working-with-keys"></a><span data-ttu-id="55253-197">Praca z kluczy</span><span class="sxs-lookup"><span data-stu-id="55253-197">Working with keys</span></span>
<span data-ttu-id="55253-198">HttpTriggers mogą korzystać z kluczy w celu zwiększenia bezpieczeństwa.</span><span class="sxs-lookup"><span data-stu-id="55253-198">HttpTriggers can leverage keys for added security.</span></span> <span data-ttu-id="55253-199">Standardowe HttpTrigger można użyć je jako klucz interfejsu API, wymagających hello klucza toobe na powitania żądania.</span><span class="sxs-lookup"><span data-stu-id="55253-199">A standard HttpTrigger can use these as an API key, requiring hello key toobe present on hello request.</span></span> <span data-ttu-id="55253-200">Elementów Webhook użyć klawiszy tooauthorize żądań na różne sposoby, w zależności od tego, jakie hello dostawca obsługuje.</span><span class="sxs-lookup"><span data-stu-id="55253-200">Webhooks can use keys tooauthorize requests in a variety of ways, depending on what hello provider supports.</span></span>

<span data-ttu-id="55253-201">Klucze są przechowywane w ramach funkcji aplikacji na platformie Azure i są szyfrowane, gdy.</span><span class="sxs-lookup"><span data-stu-id="55253-201">Keys are stored as part of your function app in Azure and are encrypted at rest.</span></span> <span data-ttu-id="55253-202">tooview klucze, tworzenie nowych lub toonew wartości kluczy zbiorczego, przejdź tooone funkcji hello portalu i wybierz "Manage".</span><span class="sxs-lookup"><span data-stu-id="55253-202">tooview your keys, create new ones, or roll keys toonew values, navigate tooone of your functions within hello portal and select "Manage."</span></span> 

<span data-ttu-id="55253-203">Istnieją dwa typy kluczy:</span><span class="sxs-lookup"><span data-stu-id="55253-203">There are two types of keys:</span></span>
- <span data-ttu-id="55253-204">**Klucze hosta**: klucze te są współużytkowane przez wszystkie funkcje w hello funkcji aplikacji.</span><span class="sxs-lookup"><span data-stu-id="55253-204">**Host keys**: These keys are shared by all functions within hello function app.</span></span> <span data-ttu-id="55253-205">Gdy jest używany jako klucz interfejsu API, umożliwiają one funkcja tooany dostępu w hello funkcji aplikacji.</span><span class="sxs-lookup"><span data-stu-id="55253-205">When used as an API key, these allow access tooany function within hello function app.</span></span>
- <span data-ttu-id="55253-206">**Klawisze funkcyjne**: te klucze zastosować tylko toohello określone funkcje, zgodnie z którymi są zdefiniowane.</span><span class="sxs-lookup"><span data-stu-id="55253-206">**Function keys**: These keys apply only toohello specific functions under which they are defined.</span></span> <span data-ttu-id="55253-207">Gdy jest używany jako klucz interfejsu API, te tylko Zezwalaj funkcja toothat dostępu.</span><span class="sxs-lookup"><span data-stu-id="55253-207">When used as an API key, these only allow access toothat function.</span></span>

<span data-ttu-id="55253-208">Każdy klucz nosi nazwę odwołania, a na poziomie funkcji oraz hosta hello jest domyślny klucz (o nazwie "domyślne").</span><span class="sxs-lookup"><span data-stu-id="55253-208">Each key is named for reference, and there is a default key (named "default") at hello function and host level.</span></span> <span data-ttu-id="55253-209">Witaj **klucza głównego** domyślny klucz hosta o nazwie "_master", który jest zdefiniowany dla każdej funkcji aplikacji i nie może zostać odwołany.</span><span class="sxs-lookup"><span data-stu-id="55253-209">hello **master key** is a default host key named "_master" that is defined for each function app and cannot be revoked.</span></span> <span data-ttu-id="55253-210">Zapewnia dostęp administracyjny toohello runtime interfejsów API.</span><span class="sxs-lookup"><span data-stu-id="55253-210">It provides administrative access toohello runtime APIs.</span></span> <span data-ttu-id="55253-211">Przy użyciu `"authLevel": "admin"` w hello powiązanie JSON będzie wymagać tego klucza toobe przedstawionych na żądanie hello; innego klucza spowoduje błąd autoryzacji.</span><span class="sxs-lookup"><span data-stu-id="55253-211">Using `"authLevel": "admin"` in hello binding JSON will require this key toobe presented on hello request; any other key will result in a authorization failure.</span></span>

> [!NOTE]
> <span data-ttu-id="55253-212">Z powodu toohello podniesione uprawnienia przyznane przez klucz główny hello, nie należy udostępniać tego klucza osobom trzecim ani rozpowszechnienie go w aplikacjach klienckich natywnego.</span><span class="sxs-lookup"><span data-stu-id="55253-212">Due toohello elevated permissions granted by hello master key, you should not share this key with third parties or distribute it in native client applications.</span></span> <span data-ttu-id="55253-213">Należy zachować ostrożność podczas wybierania hello autoryzacji na poziomie administratora.</span><span class="sxs-lookup"><span data-stu-id="55253-213">Exercise caution when choosing hello admin authorization level.</span></span>
> 
> 

### <a name="api-key-authorization"></a><span data-ttu-id="55253-214">Autoryzacji klucza interfejsu API</span><span class="sxs-lookup"><span data-stu-id="55253-214">API key authorization</span></span>
<span data-ttu-id="55253-215">Domyślnie HttpTrigger wymaga klucza interfejsu API w hello żądania HTTP.</span><span class="sxs-lookup"><span data-stu-id="55253-215">By default, an HttpTrigger requires an API key in hello HTTP request.</span></span> <span data-ttu-id="55253-216">Dlatego żądanie HTTP zwykle wygląda następująco:</span><span class="sxs-lookup"><span data-stu-id="55253-216">So your HTTP request normally looks like this:</span></span>

    https://<yourapp>.azurewebsites.net/api/<function>?code=<ApiKey>

<span data-ttu-id="55253-217">klucz Hello może być uwzględniony w zmiennej ciągu zapytania o nazwie `code`, zgodnie z powyższym, lub można je uwzględnić w `x-functions-key` nagłówka HTTP.</span><span class="sxs-lookup"><span data-stu-id="55253-217">hello key can be included in a query string variable named `code`, as above, or it can be included in an `x-functions-key` HTTP header.</span></span> <span data-ttu-id="55253-218">wartość Hello hello klucza może być dowolny klawisz funkcji zdefiniowany dla funkcji hello lub dowolnego klucz hosta.</span><span class="sxs-lookup"><span data-stu-id="55253-218">hello value of hello key can be any function key defined for hello function, or any host key.</span></span>

<span data-ttu-id="55253-219">Możesz wybrać tooallow żądań bez kluczy lub określ hello klucza głównego musi być używana przez zmianę hello `authLevel` właściwości w hello powiązanie JSON (zobacz [wyzwalacza HTTP](#httptrigger)).</span><span class="sxs-lookup"><span data-stu-id="55253-219">You can choose tooallow requests without keys or specify that hello master key must be used by changing hello `authLevel` property in hello binding JSON (see [HTTP trigger](#httptrigger)).</span></span>

### <a name="keys-and-webhooks"></a><span data-ttu-id="55253-220">Klucze i elementów webhook</span><span class="sxs-lookup"><span data-stu-id="55253-220">Keys and webhooks</span></span>
<span data-ttu-id="55253-221">Autoryzacji elementu Webhook jest obsługiwane przez składnik reciever elementu webhook hello, część hello HttpTrigger i mechanizmu hello w zależności od typu elementu webhook hello.</span><span class="sxs-lookup"><span data-stu-id="55253-221">Webhook authorization is handled by hello webhook reciever component, part of hello HttpTrigger, and hello mechanism varies based on hello webhook type.</span></span> <span data-ttu-id="55253-222">Nie mechanizmu, jednak zależne od klucza.</span><span class="sxs-lookup"><span data-stu-id="55253-222">Each mechanism does, however rely on a key.</span></span> <span data-ttu-id="55253-223">Domyślnie posłuży hello funkcja klucz o nazwie "domyślny".</span><span class="sxs-lookup"><span data-stu-id="55253-223">By default, hello function key named "default" will be used.</span></span> <span data-ttu-id="55253-224">W razie potrzeby toouse inny klucz należy tooconfigure hello nazwa elementu webhook dostawcy toosend hello klucza z żądaniem hello w jednym z hello następujące sposoby:</span><span class="sxs-lookup"><span data-stu-id="55253-224">If you wish toouse a different key, you will need tooconfigure hello webhook provider toosend hello key name with hello request in one of hello following ways:</span></span>

- <span data-ttu-id="55253-225">**Długość ciągu zapytania**: hello dostawcy przekazuje nazwę klucza hello w hello `clientid` parametr ciągu zapytania (np. `https://<yourapp>.azurewebsites.net/api/<funcname>?clientid=<keyname>`).</span><span class="sxs-lookup"><span data-stu-id="55253-225">**Query string**: hello provider passes hello key name in hello `clientid` query string parameter (e.g., `https://<yourapp>.azurewebsites.net/api/<funcname>?clientid=<keyname>`).</span></span>
- <span data-ttu-id="55253-226">**Nagłówek żądania**: hello dostawcy przekazuje nazwę klucza hello w hello `x-functions-clientid` nagłówka.</span><span class="sxs-lookup"><span data-stu-id="55253-226">**Request header**: hello provider passes hello key name in hello `x-functions-clientid` header.</span></span>

> [!NOTE]
> <span data-ttu-id="55253-227">Klawisze funkcyjne mają pierwszeństwo przed klucze hosta.</span><span class="sxs-lookup"><span data-stu-id="55253-227">Function keys take precedence over host keys.</span></span> <span data-ttu-id="55253-228">Jeśli dwa klucze są zdefiniowane z hello takie same nazwy, hello funkcja klucz będzie używany.</span><span class="sxs-lookup"><span data-stu-id="55253-228">If two keys are defined with hello same name, hello function key will be used.</span></span>
> 
> 


<a name="httptriggersample"></a>
## <a name="http-trigger-samples"></a><span data-ttu-id="55253-229">Przykłady wyzwalacza HTTP</span><span class="sxs-lookup"><span data-stu-id="55253-229">HTTP trigger samples</span></span>
<span data-ttu-id="55253-230">Załóżmy, że masz następujące wyzwalacza HTTP w hello hello `bindings` tablicy function.json:</span><span class="sxs-lookup"><span data-stu-id="55253-230">Suppose you have hello following HTTP trigger in hello `bindings` array of function.json:</span></span>

```json
{
    "name": "req",
    "type": "httpTrigger",
    "direction": "in",
    "authLevel": "function"
},
```

<span data-ttu-id="55253-231">Witaj przykładu specyficzny dla języka, która sprawdza, czy `name` parametru ciągu zapytania hello lub hello treści żądania hello HTTP.</span><span class="sxs-lookup"><span data-stu-id="55253-231">See hello language-specific sample that looks for a `name` parameter either in hello query string or hello body of hello HTTP request.</span></span>

* [<span data-ttu-id="55253-232">C#</span><span class="sxs-lookup"><span data-stu-id="55253-232">C#</span></span>](#httptriggercsharp)
* [<span data-ttu-id="55253-233">F#</span><span class="sxs-lookup"><span data-stu-id="55253-233">F#</span></span>](#httptriggerfsharp)
* [<span data-ttu-id="55253-234">Node.js</span><span class="sxs-lookup"><span data-stu-id="55253-234">Node.js</span></span>](#httptriggernodejs)


<a name="httptriggercsharp"></a>
### <a name="http-trigger-sample-in-c"></a><span data-ttu-id="55253-235">Przykładowe wyzwalacza HTTP w języku C#</span><span class="sxs-lookup"><span data-stu-id="55253-235">HTTP trigger sample in C#</span></span> #
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

    // Set name tooquery string or body data
    name = name ?? data?.name;

    return name == null
        ? req.CreateResponse(HttpStatusCode.BadRequest, "Please pass a name on hello query string or in hello request body")
        : req.CreateResponse(HttpStatusCode.OK, "Hello " + name);
}
```

<span data-ttu-id="55253-236">Może także powiązać tooa POCO zamiast `HttpRequestMessage`.</span><span class="sxs-lookup"><span data-stu-id="55253-236">You can also bind tooa POCO instead of `HttpRequestMessage`.</span></span> <span data-ttu-id="55253-237">Spowoduje to uwodniony, z hello treści żądania hello, być analizowana jako JSON.</span><span class="sxs-lookup"><span data-stu-id="55253-237">This will be hydrated from hello body of hello request, parsed as JSON.</span></span> <span data-ttu-id="55253-238">Podobnie typu mogą być przekazywane dane wyjściowe odpowiedzi toohello HTTP powiązanie, a ta wartość jest zwracana jako treść odpowiedzi hello, z kodem stanu 200.</span><span class="sxs-lookup"><span data-stu-id="55253-238">Similarly, a type can be passed toohello HTTP response output binding, and this will be returned as hello response body, with a 200 status code.</span></span>
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
### <a name="http-trigger-sample-in-f"></a><span data-ttu-id="55253-239">Przykładowe wyzwalacza HTTP w języku F #</span><span class="sxs-lookup"><span data-stu-id="55253-239">HTTP trigger sample in F#</span></span> #
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
                return req.CreateErrorResponse(HttpStatusCode.BadRequest, "Please pass a name on hello query string or in hello request body")
    } |> Async.StartAsTask
```

<span data-ttu-id="55253-240">Należy `project.json` pliku, który używa NuGet tooreference hello `FSharp.Interop.Dynamic` i `Dynamitey` zestawów, w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="55253-240">You need a `project.json` file that uses NuGet tooreference hello `FSharp.Interop.Dynamic` and `Dynamitey` assemblies, like this:</span></span>

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

<span data-ttu-id="55253-241">Zostanie użyty NuGet toofetch zależności i odwoływać je w skrypcie.</span><span class="sxs-lookup"><span data-stu-id="55253-241">This will use NuGet toofetch your dependencies and will reference them in your script.</span></span>

<a name="httptriggernodejs"></a>
### <a name="http-trigger-sample-in-nodejs"></a><span data-ttu-id="55253-242">Przykładowe wyzwalacza HTTP w środowisku Node.JS</span><span class="sxs-lookup"><span data-stu-id="55253-242">HTTP trigger sample in Node.JS</span></span>
```javascript
module.exports = function(context, req) {
    context.log('Node.js HTTP trigger function processed a request. RequestUri=%s', req.originalUrl);

    if (req.query.name || (req.body && req.body.name)) {
        context.res = {
            // status: 200, /* Defaults too200 */
            body: "Hello " + (req.query.name || req.body.name)
        };
    }
    else {
        context.res = {
            status: 400,
            body: "Please pass a name on hello query string or in hello request body"
        };
    }
    context.done();
};
```



<a name="hooktriggersample"></a>
## <a name="webhook-samples"></a><span data-ttu-id="55253-243">Przykłady elementu Webhook</span><span class="sxs-lookup"><span data-stu-id="55253-243">Webhook samples</span></span>
<span data-ttu-id="55253-244">Załóżmy, że masz hello następującego elementu webhook wyzwalacza w hello `bindings` tablicy function.json:</span><span class="sxs-lookup"><span data-stu-id="55253-244">Suppose you have hello following webhook trigger in hello `bindings` array of function.json:</span></span>

```json
{
    "webHookType": "github",
    "name": "req",
    "type": "httpTrigger",
    "direction": "in",
},
```

<span data-ttu-id="55253-245">Zobacz przykład specyficzny dla języka hello, który rejestruje komentarze problem GitHub.</span><span class="sxs-lookup"><span data-stu-id="55253-245">See hello language-specific sample that logs GitHub issue comments.</span></span>

* [<span data-ttu-id="55253-246">C#</span><span class="sxs-lookup"><span data-stu-id="55253-246">C#</span></span>](#hooktriggercsharp)
* [<span data-ttu-id="55253-247">F#</span><span class="sxs-lookup"><span data-stu-id="55253-247">F#</span></span>](#hooktriggerfsharp)
* [<span data-ttu-id="55253-248">Node.js</span><span class="sxs-lookup"><span data-stu-id="55253-248">Node.js</span></span>](#hooktriggernodejs)

<a name="hooktriggercsharp"></a>

### <a name="webhook-sample-in-c"></a><span data-ttu-id="55253-249">Przykład elementu Webhook w języku C#</span><span class="sxs-lookup"><span data-stu-id="55253-249">Webhook sample in C#</span></span> #
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

### <a name="webhook-sample-in-f"></a><span data-ttu-id="55253-250">Przykład elementu Webhook w języku F #</span><span class="sxs-lookup"><span data-stu-id="55253-250">Webhook sample in F#</span></span> #
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

### <a name="webhook-sample-in-nodejs"></a><span data-ttu-id="55253-251">Przykład elementu Webhook w środowisku Node.JS</span><span class="sxs-lookup"><span data-stu-id="55253-251">Webhook sample in Node.JS</span></span>
```javascript
module.exports = function (context, data) {
    context.log('GitHub WebHook triggered!', data.comment.body);
    context.res = { body: 'New GitHub comment: ' + data.comment.body };
    context.done();
};
```


## <a name="next-steps"></a><span data-ttu-id="55253-252">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="55253-252">Next steps</span></span>
[!INCLUDE [next steps](../../includes/functions-bindings-next-steps.md)]

