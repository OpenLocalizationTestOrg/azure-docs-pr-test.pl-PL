---
title: "Dokumentacja dla deweloperów aaaJavaScript dla usługi Azure Functions | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak działa toodevelop przy użyciu języka JavaScript."
services: functions
documentationcenter: na
author: christopheranderson
manager: erikre
editor: 
tags: 
keywords: "usługa Azure Functions, funkcje, przetwarzanie zdarzeń, elementy webhook, obliczanie dynamiczne, architektura bez serwera"
ms.assetid: 45dedd78-3ff9-411f-bb4b-16d29a11384c
ms.service: functions
ms.devlang: nodejs
ms.topic: reference
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 05/25/2017
ms.author: glenga
ms.openlocfilehash: 6220b42f965b6ee2463341aaf270836623fdf7fa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-functions-javascript-developer-guide"></a><span data-ttu-id="ef65e-104">Przewodnik dewelopera usługi Azure funkcji JavaScript</span><span class="sxs-lookup"><span data-stu-id="ef65e-104">Azure Functions JavaScript developer guide</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="ef65e-105">Skryptu C#</span><span class="sxs-lookup"><span data-stu-id="ef65e-105">C# script</span></span>](functions-reference-csharp.md)
> * [<span data-ttu-id="ef65e-106">Skrypt F #</span><span class="sxs-lookup"><span data-stu-id="ef65e-106">F# script</span></span>](functions-reference-fsharp.md)
> * [<span data-ttu-id="ef65e-107">JavaScript</span><span class="sxs-lookup"><span data-stu-id="ef65e-107">JavaScript</span></span>](functions-reference-node.md)
> 
> 

<span data-ttu-id="ef65e-108">Witaj obsługi języka JavaScript dla usługi Azure Functions umożliwia łatwe tooexport funkcję, która jest przekazywany jako `context` obiekt do komunikowania się ze środowiskiem uruchomieniowym hello i odbieranie i wysyłanie danych za pośrednictwem powiązania.</span><span class="sxs-lookup"><span data-stu-id="ef65e-108">hello JavaScript experience for Azure Functions makes it easy tooexport a function, which is passed as a `context` object for communicating with hello runtime and for receiving and sending data via bindings.</span></span>

<span data-ttu-id="ef65e-109">W tym artykule przyjęto, że został już przeczytany hello [dokumentacja dla deweloperów usługi Azure Functions](functions-reference.md).</span><span class="sxs-lookup"><span data-stu-id="ef65e-109">This article assumes that you've already read hello [Azure Functions developer reference](functions-reference.md).</span></span>

## <a name="exporting-a-function"></a><span data-ttu-id="ef65e-110">Eksportowanie funkcji</span><span class="sxs-lookup"><span data-stu-id="ef65e-110">Exporting a function</span></span>
<span data-ttu-id="ef65e-111">Wszystkie funkcje kodu JavaScript, należy wyeksportować pojedynczy `function` za pośrednictwem `module.exports` dla środowiska uruchomieniowego hello toofind hello funkcji i uruchom go.</span><span class="sxs-lookup"><span data-stu-id="ef65e-111">All JavaScript functions must export a single `function` via `module.exports` for hello runtime toofind hello function and run it.</span></span> <span data-ttu-id="ef65e-112">Ta funkcja musi zawsze zawierać `context` obiektu.</span><span class="sxs-lookup"><span data-stu-id="ef65e-112">This function must always include a `context` object.</span></span>

```javascript
// You must include a context, but other arguments are optional
module.exports = function(context) {
    // Additional inputs can be accessed by hello arguments property
    if(arguments.length === 4) {
        context.log('This function has 4 inputs');
    }
};
// or you can include additional inputs in your arguments
module.exports = function(context, myTrigger, myInput, myOtherInput) {
    // function logic goes here :)
};
```

<span data-ttu-id="ef65e-113">Powiązania `direction === "in"` są przekazywane jako argumenty funkcji, co oznacza, że można używać [ `arguments` ](https://msdn.microsoft.com/library/87dw3w1k.aspx) toodynamically obsługi nowych danych wejściowych (na przykład za pomocą `arguments.length` tooiterate za pośrednictwem wszystkich danych wejściowych).</span><span class="sxs-lookup"><span data-stu-id="ef65e-113">Bindings of `direction === "in"` are passed along as function arguments, which means that you can use [`arguments`](https://msdn.microsoft.com/library/87dw3w1k.aspx) toodynamically handle new inputs (for example, by using `arguments.length` tooiterate over all your inputs).</span></span> <span data-ttu-id="ef65e-114">Ta funkcja jest wygodne tylko wyzwalacz i nie dodatkowe dane wejściowe, ponieważ może jednoznacznie uzyskać dostęp do danych wyzwalacza bez odwołania do Twojej `context` obiektu.</span><span class="sxs-lookup"><span data-stu-id="ef65e-114">This functionality is convenient when you have only a trigger and no additional inputs, because you can predictably access your trigger data without referencing your `context` object.</span></span>

<span data-ttu-id="ef65e-115">argumenty Hello zawsze są przekazywane funkcji toohello w kolejności hello, w którym występują w *function.json*, nawet jeśli nie określisz ich w instrukcji eksportu.</span><span class="sxs-lookup"><span data-stu-id="ef65e-115">hello arguments are always passed along toohello function in hello order in which they occur in *function.json*, even if you don't specify them in your exports statement.</span></span> <span data-ttu-id="ef65e-116">Na przykład, jeśli masz `function(context, a, b)` i zmień je za`function(context, a)`, nadal można uzyskać wartość hello `b` w kodzie funkcji, odwołując się zbyt`arguments[3]`.</span><span class="sxs-lookup"><span data-stu-id="ef65e-116">For example, if you have `function(context, a, b)` and change it too`function(context, a)`, you can still get hello value of `b` in function code by referring too`arguments[3]`.</span></span>

<span data-ttu-id="ef65e-117">Wszystkie powiązania, niezależnie od kierunku, również są przekazywane na powitania `context` obiektu (zobacz hello następującego skryptu).</span><span class="sxs-lookup"><span data-stu-id="ef65e-117">All bindings, regardless of direction, are also passed along on hello `context` object (see hello following script).</span></span> 

## <a name="context-object"></a><span data-ttu-id="ef65e-118">Obiekt kontekstu</span><span class="sxs-lookup"><span data-stu-id="ef65e-118">context object</span></span>
<span data-ttu-id="ef65e-119">używa środowiska wykonawczego Hello `context` tooand danych toopass obiektu z funkcji i toolet komunikacji ze środowiskiem uruchomieniowym hello.</span><span class="sxs-lookup"><span data-stu-id="ef65e-119">hello runtime uses a `context` object toopass data tooand from your function and toolet you communicate with hello runtime.</span></span>

<span data-ttu-id="ef65e-120">Witaj obiekt kontekstu jest zawsze hello pierwszy parametr tooa funkcji i muszą być uwzględnione, ponieważ ma ona metody takie jak `context.done` i `context.log`, które są wymagane toouse hello runtime poprawnie.</span><span class="sxs-lookup"><span data-stu-id="ef65e-120">hello context object is always hello first parameter tooa function and must be included because it has methods such as `context.done` and `context.log`, which are required toouse hello runtime correctly.</span></span> <span data-ttu-id="ef65e-121">Można określić nazwę obiektu hello niezależnie od chcesz (na przykład `ctx` lub `c`).</span><span class="sxs-lookup"><span data-stu-id="ef65e-121">You can name hello object whatever you would like (for example, `ctx` or `c`).</span></span>

```javascript
// You must include a context, but other arguments are optional
module.exports = function(context) {
    // function logic goes here :)
};
```

### <a name="contextbindings-property"></a><span data-ttu-id="ef65e-122">właściwość Context.Bindings</span><span class="sxs-lookup"><span data-stu-id="ef65e-122">context.bindings property</span></span>

```
context.bindings
```
<span data-ttu-id="ef65e-123">Zwraca nazwanego obiektu, który zawiera wszystkie dane wejściowe i wyjściowe.</span><span class="sxs-lookup"><span data-stu-id="ef65e-123">Returns a named object that contains all your input and output data.</span></span> <span data-ttu-id="ef65e-124">Na przykład Witaj po definicji powiązania w Twojej *function.json* pozwala korzystać z hello zawartość hello kolejki z hello `context.bindings.myInput` obiektu.</span><span class="sxs-lookup"><span data-stu-id="ef65e-124">For example, hello following binding definition in your *function.json* lets you access hello contents of hello queue from hello `context.bindings.myInput` object.</span></span> 

```json
{
    "type":"queue",
    "direction":"in",
    "name":"myInput"
    ...
}
```

```javascript
// myInput contains hello input data, which may have properties such as "name"
var author = context.bindings.myInput.name;
// Similarly, you can set your output data
context.bindings.myOutput = { 
        some_text: 'hello world', 
        a_number: 1 };
```

### <a name="contextdone-method"></a><span data-ttu-id="ef65e-125">context.Done — metoda</span><span class="sxs-lookup"><span data-stu-id="ef65e-125">context.done method</span></span>
```
context.done([err],[propertyBag])
```

<span data-ttu-id="ef65e-126">Informuje o obsługi hello kodu zostało zakończone.</span><span class="sxs-lookup"><span data-stu-id="ef65e-126">Informs hello runtime that your code has finished.</span></span> <span data-ttu-id="ef65e-127">Należy wywołać `context.done`, lub inny hello środowiska uruchomieniowego nie wie, że funkcja została ukończona wykonanie hello upłynął limit czasu.</span><span class="sxs-lookup"><span data-stu-id="ef65e-127">You must call `context.done`, or else hello runtime never knows that your function is complete, and hello execution will time out.</span></span> 

<span data-ttu-id="ef65e-128">Witaj `context.done` metoda pozwala toopass kopii zarówno runtime toohello błąd zdefiniowany przez użytkownika, jak i właściwość zbiór właściwości, które właściwości hello na powitania zastąpione `context.bindings` obiektu.</span><span class="sxs-lookup"><span data-stu-id="ef65e-128">hello `context.done` method allows you toopass back both a user-defined error toohello runtime and a property bag of properties that overwrite hello properties on hello `context.bindings` object.</span></span>

```javascript
// Even though we set myOutput toohave:
//  -> text: hello world, number: 123
context.bindings.myOutput = { text: 'hello world', number: 123 };
// If we pass an object toohello done function...
context.done(null, { myOutput: { text: 'hello there, world', noNumber: true }});
// hello done method will overwrite hello myOutput binding toobe: 
//  -> text: hello there, world, noNumber: true
```

### <a name="contextlog-method"></a><span data-ttu-id="ef65e-129">context.log — metoda</span><span class="sxs-lookup"><span data-stu-id="ef65e-129">context.log method</span></span>  

```
context.log(message)
```
<span data-ttu-id="ef65e-130">Umożliwia toowrite toohello dzienniki przesyłania strumieniowego konsoli na powitania domyślny poziom śledzenia.</span><span class="sxs-lookup"><span data-stu-id="ef65e-130">Allows you toowrite toohello streaming console logs at hello default trace level.</span></span> <span data-ttu-id="ef65e-131">Na `context.log`, dodatkowe opcje rejestrowania metody są dostępne, które umożliwiają zapisać dziennik konsoli toohello na innych poziomach śledzenia:</span><span class="sxs-lookup"><span data-stu-id="ef65e-131">On `context.log`, additional logging methods are available that let you write toohello console log at other trace levels:</span></span>


| <span data-ttu-id="ef65e-132">Metoda</span><span class="sxs-lookup"><span data-stu-id="ef65e-132">Method</span></span>                 | <span data-ttu-id="ef65e-133">Opis</span><span class="sxs-lookup"><span data-stu-id="ef65e-133">Description</span></span>                                |
| ---------------------- | ------------------------------------------ |
| <span data-ttu-id="ef65e-134">**Błąd (_komunikat_)**</span><span class="sxs-lookup"><span data-stu-id="ef65e-134">**error(_message_)**</span></span>   | <span data-ttu-id="ef65e-135">Zapisuje poziom tooerror rejestrowanie lub niższy.</span><span class="sxs-lookup"><span data-stu-id="ef65e-135">Writes tooerror level logging, or lower.</span></span>   |
| <span data-ttu-id="ef65e-136">**Ostrzegaj (_komunikat_)**</span><span class="sxs-lookup"><span data-stu-id="ef65e-136">**warn(_message_)**</span></span>    | <span data-ttu-id="ef65e-137">Zapisuje poziom toowarning rejestrowanie lub niższy.</span><span class="sxs-lookup"><span data-stu-id="ef65e-137">Writes toowarning level logging, or lower.</span></span> |
| <span data-ttu-id="ef65e-138">**informacje o (_komunikat_)**</span><span class="sxs-lookup"><span data-stu-id="ef65e-138">**info(_message_)**</span></span>    | <span data-ttu-id="ef65e-139">Zapisuje poziom tooinfo rejestrowanie lub niższy.</span><span class="sxs-lookup"><span data-stu-id="ef65e-139">Writes tooinfo level logging, or lower.</span></span>    |
| <span data-ttu-id="ef65e-140">**pełne (_komunikat_)**</span><span class="sxs-lookup"><span data-stu-id="ef65e-140">**verbose(_message_)**</span></span> | <span data-ttu-id="ef65e-141">Zapisuje tooverbose poziomu rejestrowania.</span><span class="sxs-lookup"><span data-stu-id="ef65e-141">Writes tooverbose level logging.</span></span>           |

<span data-ttu-id="ef65e-142">Witaj poniższy przykład zapisuje konsoli toohello na poziomie śledzenia ostrzeżenie hello:</span><span class="sxs-lookup"><span data-stu-id="ef65e-142">hello following example writes toohello console at hello warning trace level:</span></span>

```javascript
context.log.warn("Something has happened."); 
```
<span data-ttu-id="ef65e-143">Ustaw poziom śledzenia hello próg rejestrowania w pliku host.json hello lub ją wyłączyć.</span><span class="sxs-lookup"><span data-stu-id="ef65e-143">You can set hello trace-level threshold for logging in hello host.json file, or turn it off.</span></span>  <span data-ttu-id="ef65e-144">Aby uzyskać więcej informacji na temat sposobu logowania toowrite toohello zobacz następną sekcję hello.</span><span class="sxs-lookup"><span data-stu-id="ef65e-144">For more information about how toowrite toohello logs, see hello next section.</span></span>

## <a name="binding-data-type"></a><span data-ttu-id="ef65e-145">Typ danych powiązania</span><span class="sxs-lookup"><span data-stu-id="ef65e-145">Binding data type</span></span>

<span data-ttu-id="ef65e-146">toodefine typ danych hello powiązania wejściowego, użyj hello `dataType` właściwości w definicji powiązania hello.</span><span class="sxs-lookup"><span data-stu-id="ef65e-146">toodefine hello data type for an input binding, use hello `dataType` property in hello binding definition.</span></span> <span data-ttu-id="ef65e-147">Na przykład tooread hello zawartości żądania HTTP w formacie binarnym, użyj typu hello `binary`:</span><span class="sxs-lookup"><span data-stu-id="ef65e-147">For example, tooread hello content of an HTTP request in binary format, use hello type `binary`:</span></span>

```json
{
    "type": "httpTrigger",
    "name": "req",
    "direction": "in",
    "dataType": "binary"
}
```

<span data-ttu-id="ef65e-148">Inne opcje `dataType` są `stream` i `string`.</span><span class="sxs-lookup"><span data-stu-id="ef65e-148">Other options for `dataType` are `stream` and `string`.</span></span>

## <a name="writing-trace-output-toohello-console"></a><span data-ttu-id="ef65e-149">Zapisywanie śledzenia danych wyjściowych toohello konsoli</span><span class="sxs-lookup"><span data-stu-id="ef65e-149">Writing trace output toohello console</span></span> 

<span data-ttu-id="ef65e-150">W przypadku funkcji, użyj hello `context.log` metody toowrite śledzenia danych wyjściowych toohello konsoli.</span><span class="sxs-lookup"><span data-stu-id="ef65e-150">In Functions, you use hello `context.log` methods toowrite trace output toohello console.</span></span> <span data-ttu-id="ef65e-151">W tym momencie nie można użyć `console.log` toowrite toohello konsoli.</span><span class="sxs-lookup"><span data-stu-id="ef65e-151">At this point, you cannot use `console.log` toowrite toohello console.</span></span>

<span data-ttu-id="ef65e-152">Podczas wywoływania `context.log()`, wiadomości są zapisywane konsoli toohello na poziomie śledzenia domyślnego hello, co jest hello _informacji_ poziom śledzenia.</span><span class="sxs-lookup"><span data-stu-id="ef65e-152">When you call `context.log()`, your message is written toohello console at hello default trace level, which is hello _info_ trace level.</span></span> <span data-ttu-id="ef65e-153">Witaj następujący kod zapisuje konsoli toohello na poziomie śledzenia informacji hello:</span><span class="sxs-lookup"><span data-stu-id="ef65e-153">hello following code writes toohello console at hello info trace level:</span></span>

```javascript
context.log({hello: 'world'});  
```

<span data-ttu-id="ef65e-154">Witaj poprzedni kod jest równoważne toohello następującego kodu:</span><span class="sxs-lookup"><span data-stu-id="ef65e-154">hello preceding code is equivalent toohello following code:</span></span>

```javascript
context.log.info({hello: 'world'});  
```

<span data-ttu-id="ef65e-155">Witaj następujący kod zapisuje konsoli toohello na poziomie błąd hello:</span><span class="sxs-lookup"><span data-stu-id="ef65e-155">hello following code writes toohello console at hello error level:</span></span>

```javascript
context.log.error("An error has occurred.");  
```

<span data-ttu-id="ef65e-156">Ponieważ _błąd_ hello śledzenia najwyższego poziomu, to śledzenia są zapisywane dane wyjściowe toohello na wszystkich poziomach śledzenia tak długo, jak rejestrowanie jest włączone.</span><span class="sxs-lookup"><span data-stu-id="ef65e-156">Because _error_ is hello highest trace level, this trace is written toohello output at all trace levels as long as logging is enabled.</span></span>  


<span data-ttu-id="ef65e-157">Wszystkie `context.log` metody obsługują hello sam format parametru obsługiwaną przez hello Node.js [metody util.format](https://nodejs.org/api/util.html#util_util_format_format).</span><span class="sxs-lookup"><span data-stu-id="ef65e-157">All `context.log` methods support hello same parameter format that's supported by hello Node.js [util.format method](https://nodejs.org/api/util.html#util_util_format_format).</span></span> <span data-ttu-id="ef65e-158">Należy wziąć pod uwagę hello następującego kodu, który zapisuje toohello konsoli za pomocą hello domyślny poziom śledzenia:</span><span class="sxs-lookup"><span data-stu-id="ef65e-158">Consider hello following code, which writes toohello console by using hello default trace level:</span></span>

```javascript
context.log('Node.js HTTP trigger function processed a request. RequestUri=' + req.originalUrl);
context.log('Request Headers = ' + JSON.stringify(req.headers));
```

<span data-ttu-id="ef65e-159">Możesz również hello zapisu sam kod w hello następującego formatu:</span><span class="sxs-lookup"><span data-stu-id="ef65e-159">You can also write hello same code in hello following format:</span></span>

```javascript
context.log('Node.js HTTP trigger function processed a request. RequestUri=%s', req.originalUrl);
context.log('Request Headers = ', JSON.stringify(req.headers));
```

### <a name="configure-hello-trace-level-for-console-logging"></a><span data-ttu-id="ef65e-160">Skonfiguruj hello poziom śledzenia dla konsoli rejestrowania</span><span class="sxs-lookup"><span data-stu-id="ef65e-160">Configure hello trace level for console logging</span></span>

<span data-ttu-id="ef65e-161">Funkcje pozwala zdefiniować poziom śledzenia próg hello do pisania toohello konsoli, co pozwala na łatwe toocontrol hello sposób śledzenia są zapisywane toohello konsoli z funkcji.</span><span class="sxs-lookup"><span data-stu-id="ef65e-161">Functions lets you define hello threshold trace level for writing toohello console, which makes it easy toocontrol hello way traces are written toohello console from your functions.</span></span> <span data-ttu-id="ef65e-162">Próg hello tooset wszystkie ślady zapisywane toohello konsoli, użyj hello `tracing.consoleLevel` właściwość w pliku host.json hello.</span><span class="sxs-lookup"><span data-stu-id="ef65e-162">tooset hello threshold for all traces written toohello console, use hello `tracing.consoleLevel` property in hello host.json file.</span></span> <span data-ttu-id="ef65e-163">To ustawienie dotyczy funkcji tooall w funkcji aplikacji.</span><span class="sxs-lookup"><span data-stu-id="ef65e-163">This setting applies tooall functions in your function app.</span></span> <span data-ttu-id="ef65e-164">Witaj poniższy przykład przedstawia hello śledzenia próg tooenable pełne rejestrowanie:</span><span class="sxs-lookup"><span data-stu-id="ef65e-164">hello following example sets hello trace threshold tooenable verbose logging:</span></span>

```json
{ 
    "tracing": {      
        "consoleLevel": "verbose"     
    }
}  
```

<span data-ttu-id="ef65e-165">Wartości typu **consoleLevel** odpowiada toohello nazwy hello `context.log` metody.</span><span class="sxs-lookup"><span data-stu-id="ef65e-165">Values of **consoleLevel** correspond toohello names of hello `context.log` methods.</span></span> <span data-ttu-id="ef65e-166">Ustaw wszystkie śledzenia rejestrowania konsoli toohello toodisable **consoleLevel** too_off_.</span><span class="sxs-lookup"><span data-stu-id="ef65e-166">toodisable all trace logging toohello console, set **consoleLevel** too_off_.</span></span> <span data-ttu-id="ef65e-167">Aby uzyskać więcej informacji o pliku host.json hello, zobacz hello [temat referencyjny host.json](https://github.com/Azure/azure-webjobs-sdk-script/wiki/host.json).</span><span class="sxs-lookup"><span data-stu-id="ef65e-167">For more information about hello host.json file, see hello [host.json reference topic](https://github.com/Azure/azure-webjobs-sdk-script/wiki/host.json).</span></span>

## <a name="http-triggers-and-bindings"></a><span data-ttu-id="ef65e-168">HTTP wyzwalaczy i powiązań</span><span class="sxs-lookup"><span data-stu-id="ef65e-168">HTTP triggers and bindings</span></span>

<span data-ttu-id="ef65e-169">HTTP i wyzwalaczy elementu webhook HTTP wyjściowe i powiązania Użyj żądania i odpowiedzi obiektów toorepresent hello HTTP wiadomości.</span><span class="sxs-lookup"><span data-stu-id="ef65e-169">HTTP and webhook triggers and HTTP output bindings use request and response objects toorepresent hello HTTP messaging.</span></span>  

### <a name="request-object"></a><span data-ttu-id="ef65e-170">Obiekt żądania</span><span class="sxs-lookup"><span data-stu-id="ef65e-170">Request object</span></span>

<span data-ttu-id="ef65e-171">Witaj `request` obiekt ma hello następujące właściwości:</span><span class="sxs-lookup"><span data-stu-id="ef65e-171">hello `request` object has hello following properties:</span></span>

| <span data-ttu-id="ef65e-172">Właściwość</span><span class="sxs-lookup"><span data-stu-id="ef65e-172">Property</span></span>      | <span data-ttu-id="ef65e-173">Opis</span><span class="sxs-lookup"><span data-stu-id="ef65e-173">Description</span></span>                                                    |
| ------------- | -------------------------------------------------------------- |
| <span data-ttu-id="ef65e-174">_treści_</span><span class="sxs-lookup"><span data-stu-id="ef65e-174">_body_</span></span>        | <span data-ttu-id="ef65e-175">Obiekt, który zawiera hello treści żądania hello.</span><span class="sxs-lookup"><span data-stu-id="ef65e-175">An object that contains hello body of hello request.</span></span>               |
| <span data-ttu-id="ef65e-176">_nagłówki_</span><span class="sxs-lookup"><span data-stu-id="ef65e-176">_headers_</span></span>     | <span data-ttu-id="ef65e-177">Obiekt, który zawiera hello nagłówki żądania.</span><span class="sxs-lookup"><span data-stu-id="ef65e-177">An object that contains hello request headers.</span></span>                   |
| <span data-ttu-id="ef65e-178">_— Metoda_</span><span class="sxs-lookup"><span data-stu-id="ef65e-178">_method_</span></span>      | <span data-ttu-id="ef65e-179">Metoda HTTP żądania hello Hello.</span><span class="sxs-lookup"><span data-stu-id="ef65e-179">hello HTTP method of hello request.</span></span>                                |
| <span data-ttu-id="ef65e-180">_originalUrl_</span><span class="sxs-lookup"><span data-stu-id="ef65e-180">_originalUrl_</span></span> | <span data-ttu-id="ef65e-181">adres URL Hello hello żądania.</span><span class="sxs-lookup"><span data-stu-id="ef65e-181">hello URL of hello request.</span></span>                                        |
| <span data-ttu-id="ef65e-182">_Parametry_</span><span class="sxs-lookup"><span data-stu-id="ef65e-182">_params_</span></span>      | <span data-ttu-id="ef65e-183">Obiekt zawierający parametry routingu hello hello żądania.</span><span class="sxs-lookup"><span data-stu-id="ef65e-183">An object that contains hello routing parameters of hello request.</span></span> |
| <span data-ttu-id="ef65e-184">_zapytania_</span><span class="sxs-lookup"><span data-stu-id="ef65e-184">_query_</span></span>       | <span data-ttu-id="ef65e-185">Obiekt zawierający parametry zapytania hello.</span><span class="sxs-lookup"><span data-stu-id="ef65e-185">An object that contains hello query parameters.</span></span>                  |
| <span data-ttu-id="ef65e-186">_rawBody_</span><span class="sxs-lookup"><span data-stu-id="ef65e-186">_rawBody_</span></span>     | <span data-ttu-id="ef65e-187">Witaj treść wiadomości powitania jako ciąg.</span><span class="sxs-lookup"><span data-stu-id="ef65e-187">hello body of hello message as a string.</span></span>                           |


### <a name="response-object"></a><span data-ttu-id="ef65e-188">Obiekt odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="ef65e-188">Response object</span></span>

<span data-ttu-id="ef65e-189">Witaj `response` obiekt ma hello następujące właściwości:</span><span class="sxs-lookup"><span data-stu-id="ef65e-189">hello `response` object has hello following properties:</span></span>

| <span data-ttu-id="ef65e-190">Właściwość</span><span class="sxs-lookup"><span data-stu-id="ef65e-190">Property</span></span>  | <span data-ttu-id="ef65e-191">Opis</span><span class="sxs-lookup"><span data-stu-id="ef65e-191">Description</span></span>                                               |
| --------- | --------------------------------------------------------- |
| <span data-ttu-id="ef65e-192">_treści_</span><span class="sxs-lookup"><span data-stu-id="ef65e-192">_body_</span></span>    | <span data-ttu-id="ef65e-193">Obiekt, który zawiera treść hello hello odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="ef65e-193">An object that contains hello body of hello response.</span></span>         |
| <span data-ttu-id="ef65e-194">_nagłówki_</span><span class="sxs-lookup"><span data-stu-id="ef65e-194">_headers_</span></span> | <span data-ttu-id="ef65e-195">Obiekt, który zawiera nagłówki odpowiedzi hello.</span><span class="sxs-lookup"><span data-stu-id="ef65e-195">An object that contains hello response headers.</span></span>             |
| <span data-ttu-id="ef65e-196">_isRaw_</span><span class="sxs-lookup"><span data-stu-id="ef65e-196">_isRaw_</span></span>   | <span data-ttu-id="ef65e-197">Wskazuje, że formatowanie zostało pominięte dla hello odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="ef65e-197">Indicates that formatting is skipped for hello response.</span></span>    |
| <span data-ttu-id="ef65e-198">_Stan_</span><span class="sxs-lookup"><span data-stu-id="ef65e-198">_status_</span></span>  | <span data-ttu-id="ef65e-199">Kod stanu HTTP odpowiedzi hello Hello.</span><span class="sxs-lookup"><span data-stu-id="ef65e-199">hello HTTP status code of hello response.</span></span>                     |

### <a name="accessing-hello-request-and-response"></a><span data-ttu-id="ef65e-200">Uzyskiwanie dostępu do hello żądań i odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="ef65e-200">Accessing hello request and response</span></span> 

<span data-ttu-id="ef65e-201">Podczas pracy z wyzwalaczy HTTP, aby dostęp do hello obiektów żądań i odpowiedzi HTTP w dowolnej z trzech sposobów:</span><span class="sxs-lookup"><span data-stu-id="ef65e-201">When you work with HTTP triggers, you can access hello HTTP request and response objects in any of three ways:</span></span>

+ <span data-ttu-id="ef65e-202">Z hello o nazwie danych wejściowych i wyjściowych powiązania.</span><span class="sxs-lookup"><span data-stu-id="ef65e-202">From hello named input and output bindings.</span></span> <span data-ttu-id="ef65e-203">W ten sposób hello wyzwalacza HTTP i powiązania pracy hello takie same jak wszelkie inne powiązania.</span><span class="sxs-lookup"><span data-stu-id="ef65e-203">In this way, hello HTTP trigger and bindings work hello same as any other binding.</span></span> <span data-ttu-id="ef65e-204">Witaj poniższy przykład przedstawia hello obiekt odpowiedzi przy użyciu nazwane `response` powiązania:</span><span class="sxs-lookup"><span data-stu-id="ef65e-204">hello following example sets hello response object by using a named `response` binding:</span></span> 

    ```javascript
    context.bindings.response = { status: 201, body: "Insert succeeded." };
    ```

+ <span data-ttu-id="ef65e-205">Z `req` i `res` właściwości na powitania `context` obiektu.</span><span class="sxs-lookup"><span data-stu-id="ef65e-205">From `req` and `res` properties on hello `context` object.</span></span> <span data-ttu-id="ef65e-206">W ten sposób można użyć hello wzorca z konwencjonalnej tooaccess HTTP danych z obiektu kontekstu hello, zamiast pełnej hello toouse `context.bindings.name` wzorca.</span><span class="sxs-lookup"><span data-stu-id="ef65e-206">In this way, you can use hello conventional pattern tooaccess HTTP data from hello context object, instead of having toouse hello full `context.bindings.name` pattern.</span></span> <span data-ttu-id="ef65e-207">powitania po przykładzie pokazano, jak tooaccess hello `req` i `res` obiektów na powitania `context`:</span><span class="sxs-lookup"><span data-stu-id="ef65e-207">hello following example shows how tooaccess hello `req` and `res` objects on hello `context`:</span></span>

    ```javascript
    // You can access your http request off hello context ...
    if(context.req.body.emoji === ':pizza:') context.log('Yay!');
    // and also set your http response
    context.res = { status: 202, body: 'You successfully ordered more coffee!' }; 
    ```

+ <span data-ttu-id="ef65e-208">Wywołując `context.done()`.</span><span class="sxs-lookup"><span data-stu-id="ef65e-208">By calling `context.done()`.</span></span> <span data-ttu-id="ef65e-209">Specjalny rodzaj powiązanie HTTP zwraca odpowiedź hello, który jest przekazywany toohello `context.done()` metody.</span><span class="sxs-lookup"><span data-stu-id="ef65e-209">A special kind of HTTP binding returns hello response that is passed toohello `context.done()` method.</span></span> <span data-ttu-id="ef65e-210">powitania po HTTP output definiuje powiązanie `$return` parametru wyjściowego:</span><span class="sxs-lookup"><span data-stu-id="ef65e-210">hello following HTTP output binding defines a `$return` output parameter:</span></span>

    ```json
    {
      "type": "http",
      "direction": "out",
      "name": "$return"
    }
    ``` 
    <span data-ttu-id="ef65e-211">To powiązanie danych wyjściowych oczekuje odpowiedź hello toosupply podczas wywoływania `done()`w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="ef65e-211">This output binding expects you toosupply hello response when you call `done()`, as follows:</span></span>

    ```javascript
     // Define a valid response object.
    res = { status: 201, body: "Insert succeeded." };
    context.done(null, res);   
    ```  

## <a name="node-version-and-package-management"></a><span data-ttu-id="ef65e-212">Wersja węzła i zarządzania pakietami</span><span class="sxs-lookup"><span data-stu-id="ef65e-212">Node version and Package Management</span></span>
<span data-ttu-id="ef65e-213">Wersja węzła Hello jest obecnie zablokowana na `6.5.0`.</span><span class="sxs-lookup"><span data-stu-id="ef65e-213">hello node version is currently locked at `6.5.0`.</span></span> <span data-ttu-id="ef65e-214">Firma Microsoft badanie włączenie obsługi więcej wersji i co można skonfigurować.</span><span class="sxs-lookup"><span data-stu-id="ef65e-214">We're investigating adding support for more versions and making it configurable.</span></span>

<span data-ttu-id="ef65e-215">Witaj, wykonaj czynności pozwalają na wybranie pakietów w aplikacji funkcji:</span><span class="sxs-lookup"><span data-stu-id="ef65e-215">hello following steps let you include packages in your function app:</span></span> 

1. <span data-ttu-id="ef65e-216">Przejdź do zbyt`https://<function_app_name>.scm.azurewebsites.net`.</span><span class="sxs-lookup"><span data-stu-id="ef65e-216">Go too`https://<function_app_name>.scm.azurewebsites.net`.</span></span>

2. <span data-ttu-id="ef65e-217">Kliknij przycisk **Konsola debugowania** > **CMD**.</span><span class="sxs-lookup"><span data-stu-id="ef65e-217">Click **Debug Console** > **CMD**.</span></span>

3. <span data-ttu-id="ef65e-218">Go za`D:\home\site\wwwroot`, a następnie przeciągnij z toohello pliku package.json **wwwroot** folderu w górnej połowie hello hello strony.</span><span class="sxs-lookup"><span data-stu-id="ef65e-218">Go too`D:\home\site\wwwroot`, and then drag your package.json file toohello **wwwroot** folder at hello top half of hello page.</span></span>  
    <span data-ttu-id="ef65e-219">Możesz również przekazać pliki tooyour funkcji aplikacji w inny sposób.</span><span class="sxs-lookup"><span data-stu-id="ef65e-219">You can upload files tooyour function app in other ways also.</span></span> <span data-ttu-id="ef65e-220">Aby uzyskać więcej informacji, zobacz [jak tooupdate funkcji pliki aplikacji](functions-reference.md#fileupdate).</span><span class="sxs-lookup"><span data-stu-id="ef65e-220">For more information, see [How tooupdate function app files](functions-reference.md#fileupdate).</span></span> 

4. <span data-ttu-id="ef65e-221">Po przekazaniu pliku package.json hello Uruchom hello `npm install` w hello **konsoli zdalne wykonywanie kodu Kudu**.</span><span class="sxs-lookup"><span data-stu-id="ef65e-221">After hello package.json file is uploaded, run hello `npm install` command in hello **Kudu remote execution console**.</span></span>  
    <span data-ttu-id="ef65e-222">Ta akcja spowoduje pobranie pakietów hello określonej w pliku package.json hello i ponownego uruchomienia hello funkcji aplikacji.</span><span class="sxs-lookup"><span data-stu-id="ef65e-222">This action downloads hello packages indicated in hello package.json file and restarts hello function app.</span></span>

<span data-ttu-id="ef65e-223">Po hello pakiety potrzebne są zainstalowane, podczas ich importu funkcji tooyour przez wywołanie metody `require('packagename')`w hello poniższy przykład:</span><span class="sxs-lookup"><span data-stu-id="ef65e-223">After hello packages you need are installed, you import them tooyour function by calling `require('packagename')`, as in hello following example:</span></span>

```javascript
// Import hello underscore.js library
var _ = require('underscore');
var version = process.version; // version === 'v6.5.0'

module.exports = function(context) {
    // Using our imported underscore.js library
    var matched_names = _
        .where(context.bindings.myInput.names, {first: 'Carla'});
```

<span data-ttu-id="ef65e-224">Należy zdefiniować `package.json` pliku w katalogu głównym hello aplikacji funkcji.</span><span class="sxs-lookup"><span data-stu-id="ef65e-224">You should define a `package.json` file at hello root of your function app.</span></span> <span data-ttu-id="ef65e-225">Definiowanie pliku hello umożliwia wszystkich funkcji w udostępnionej aplikacji hello hello same pakiety w pamięci podręcznej, co daje hello najlepszą wydajność.</span><span class="sxs-lookup"><span data-stu-id="ef65e-225">Defining hello file lets all functions in hello app share hello same cached packages, which gives hello best performance.</span></span> <span data-ttu-id="ef65e-226">Jeśli wystąpi konflikt wersji, można rozwiązać go przez dodanie `package.json` plik w folderze hello określonych funkcji.</span><span class="sxs-lookup"><span data-stu-id="ef65e-226">If a version conflict arises, you can resolve it by adding a `package.json` file in hello folder of a specific function.</span></span>  

## <a name="environment-variables"></a><span data-ttu-id="ef65e-227">Zmienne środowiskowe</span><span class="sxs-lookup"><span data-stu-id="ef65e-227">Environment variables</span></span>
<span data-ttu-id="ef65e-228">tooget zmienną środowiskową lub wartość ustawienia aplikacji, użyj `process.env`, jak pokazano w hello poniższy przykład kodu:</span><span class="sxs-lookup"><span data-stu-id="ef65e-228">tooget an environment variable or an app setting value, use `process.env`, as shown in hello following code example:</span></span>

```javascript
module.exports = function (context, myTimer) {
    var timeStamp = new Date().toISOString();

    context.log('Node.js timer trigger function ran!', timeStamp);   
    context.log(GetEnvironmentVariable("AzureWebJobsStorage"));
    context.log(GetEnvironmentVariable("WEBSITE_SITE_NAME"));

    context.done();
};

function GetEnvironmentVariable(name)
{
    return name + ": " + process.env[name];
}
```
## <a name="considerations-for-javascript-functions"></a><span data-ttu-id="ef65e-229">Zagadnienia dotyczące funkcji JavaScript</span><span class="sxs-lookup"><span data-stu-id="ef65e-229">Considerations for JavaScript functions</span></span>

<span data-ttu-id="ef65e-230">Podczas pracy z funkcji JavaScript, należy pamiętać o kwestiach hello w hello następujące dwie sekcje.</span><span class="sxs-lookup"><span data-stu-id="ef65e-230">When you work with JavaScript functions, be aware of hello considerations in hello following two sections.</span></span>

### <a name="choose-single-core-app-service-plans"></a><span data-ttu-id="ef65e-231">Wybierz jednordzeniowy planów usługi aplikacji</span><span class="sxs-lookup"><span data-stu-id="ef65e-231">Choose single-core App Service plans</span></span>

<span data-ttu-id="ef65e-232">Podczas tworzenia aplikacji funkcji, który używa hello planu usługi aplikacji zaleca się wybranie planu jednordzeniowy zamiast planu z wieloma rdzeniami.</span><span class="sxs-lookup"><span data-stu-id="ef65e-232">When you create a function app that uses hello App Service plan, we recommend that you select a single-core plan rather than a plan with multiple cores.</span></span> <span data-ttu-id="ef65e-233">Obecnie funkcji uruchamia funkcji JavaScript wydajniej na maszynach wirtualnych jednordzeniowy i przy użyciu większe maszyny wirtualne nie tworzy hello oczekiwano ulepszenia wydajności.</span><span class="sxs-lookup"><span data-stu-id="ef65e-233">Today, Functions runs JavaScript functions more efficiently on single-core VMs, and using larger VMs does not produce hello expected performance improvements.</span></span> <span data-ttu-id="ef65e-234">Jeśli to konieczne, można ręcznie skalować w poziomie przez dodanie więcej wystąpień maszyny Wirtualnej jednordzeniowy, lub można włączyć automatycznego skalowania.</span><span class="sxs-lookup"><span data-stu-id="ef65e-234">When necessary, you can manually scale out by adding more single-core VM instances, or you can enable auto-scale.</span></span> <span data-ttu-id="ef65e-235">Aby uzyskać więcej informacji, zobacz [skalowanie liczby wystąpień ręcznie lub automatycznie](../monitoring-and-diagnostics/insights-how-to-scale.md?toc=%2fazure%2fapp-service-web%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="ef65e-235">For more information, see [Scale instance count manually or automatically](../monitoring-and-diagnostics/insights-how-to-scale.md?toc=%2fazure%2fapp-service-web%2ftoc.json).</span></span>    

### <a name="typescript-and-coffeescript-support"></a><span data-ttu-id="ef65e-236">Obsługa języka typeScript i CoffeeScript</span><span class="sxs-lookup"><span data-stu-id="ef65e-236">TypeScript and CoffeeScript support</span></span>
<span data-ttu-id="ef65e-237">Ponieważ wsparcia bezpośredniego jeszcze nie istnieje maszynie lub CoffeeScript kompilowanie automatycznie za pomocą środowiska uruchomieniowego hello, wsparcie takie musi toobe obsługiwane poza hello środowiska uruchomieniowego, w czasie wdrażania.</span><span class="sxs-lookup"><span data-stu-id="ef65e-237">Because direct support does not yet exist for auto-compiling TypeScript or CoffeeScript via hello runtime, such support needs toobe handled outside hello runtime, at deployment time.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="ef65e-238">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="ef65e-238">Next steps</span></span>
<span data-ttu-id="ef65e-239">Aby uzyskać więcej informacji zobacz następujące zasoby hello:</span><span class="sxs-lookup"><span data-stu-id="ef65e-239">For more information, see hello following resources:</span></span>

* [<span data-ttu-id="ef65e-240">Najlepsze rozwiązania dotyczące usługi Azure Functions</span><span class="sxs-lookup"><span data-stu-id="ef65e-240">Best practices for Azure Functions</span></span>](functions-best-practices.md)
* [<span data-ttu-id="ef65e-241">Dokumentacja usługi Azure Functions dla deweloperów</span><span class="sxs-lookup"><span data-stu-id="ef65e-241">Azure Functions developer reference</span></span>](functions-reference.md)
* [<span data-ttu-id="ef65e-242">Azure dokumentacja dla deweloperów funkcje C#</span><span class="sxs-lookup"><span data-stu-id="ef65e-242">Azure Functions C# developer reference</span></span>](functions-reference-csharp.md)
* [<span data-ttu-id="ef65e-243">Azure dokumentacja dla deweloperów funkcje F #</span><span class="sxs-lookup"><span data-stu-id="ef65e-243">Azure Functions F# developer reference</span></span>](functions-reference-fsharp.md)
* [<span data-ttu-id="ef65e-244">Azure funkcje wyzwalaczy i powiązań</span><span class="sxs-lookup"><span data-stu-id="ef65e-244">Azure Functions triggers and bindings</span></span>](functions-triggers-bindings.md)

