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
# <a name="azure-functions-http-and-webhook-bindings"></a>Azure powiązania HTTP funkcje i elementu webhook
[!INCLUDE [functions-selector-bindings](../../includes/functions-selector-bindings.md)]

W tym artykule opisano, jak wyzwala tooconfigure i korzystają z protokołu HTTP i powiązania usługi Azure Functions.
Z tych opcji możesz użyć usługi Azure Functions toobuild niekorzystającą interfejsów API i odpowiedź toowebhooks.

Środowisko Azure Functions zapewnia następujące powiązania hello:
- [Wyzwalacza HTTP](#httptrigger) umożliwia wywołanie funkcji z żądania HTTP. Może to być dostosowane toorespond zbyt[elementów webhook](#hooktrigger).
- [Powiązania wyjściowego HTTP](#output) pozwala toorespond toohello żądania.

[!INCLUDE [intro](../../includes/functions-bindings-intro.md)]

[!INCLUDE [HTTP client best practices](../../includes/functions-http-client-best-practices.md)]

<a name="httptrigger"></a>

## <a name="http-trigger"></a>Wyzwalacz HTTP
wyzwalacza HTTP Hello wykona funkcja w żądaniu HTTP tooan odpowiedzi. Można go dostosować toorespond tooa określonego adresu URL lub zestawu metod HTTP. Wyzwalacz HTTP może być również skonfigurowany toorespond toowebhooks. 

Jeśli za pomocą portalu funkcje hello, można również rozpocząć od razu przy użyciu predefiniowanych szablonów. Wybierz **nową funkcję** i wybierz polecenie "Interfejsu API i elementów Webhook" z hello **scenariusza** listy rozwijanej. Wybierz jeden z szablonów hello, a następnie kliknij przycisk **Utwórz**.

Domyślnie wyzwalacza HTTP będzie odpowiadać na żądania toohello z kodem stanu HTTP 200 OK i pustej treści. toomodify hello odpowiedzi, skonfigurować [powiązania wyjściowego HTTP](#output)

### <a name="configuring-an-http-trigger"></a>Konfigurowanie wyzwalacza HTTP
Wyzwalacz protokołu HTTP jest zdefiniowany przez dołączenie JSON obiektu toohello podobne, po w hello `bindings` tablicy function.json:

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
Powiązanie Hello obsługuje hello następujące właściwości:

* **Nazwa** : wymagana — nazwa zmiennej hello używane w kodzie funkcji żądania hello lub treści żądania. Zobacz [Praca z wyzwalacza HTTP z kodu](#httptriggerusage).
* **Typ** : wymagana — musi być ustawiona zbyt "httpTrigger".
* **kierunek** : wymagana — musi być ustawiona zbyt "w".
* _authLevel_ : Określa, jakie klucze, należy toobe obecne w żądaniu hello w kolejności tooinvoke hello funkcji. Zobacz [Praca z kluczami](#keys) poniżej. wartość Hello może być jedną z następujących hello:
    * _anonimowe_: klucz interfejsu API nie jest wymagana.
    * _Funkcja_: wymagany jest klucz interfejsu API właściwe dla funkcji. Jeśli nie zostanie podana jest wartość domyślna hello.
    * _Administrator_ : jest wymagany klucz główny hello.
* **metody** : to jest tablica metod hello HTTP będzie odpowiadać toowhich hello funkcji. Jeśli nie zostanie określony, funkcja hello będzie odpowiadać metody tooall HTTP. Zobacz [Dostosowywanie punktu końcowego hello HTTP](#url).
* **trasy** : Określa szablon trasy hello, kontrolowanie toowhich adresów URL będzie odpowiadać funkcji żądań. Witaj wartość domyślną, jeśli nie zostanie podana jest `<functionname>`. Zobacz [Dostosowywanie punktu końcowego hello HTTP](#url).
* **webHookType** : spowoduje to skonfigurowanie tooact wyzwalacza hello HTTP jako reciever elementu webhook dla hello określonego dostawcy. Witaj _metody_ właściwość nie powinna być ustawiona, jeśli to jest wybrane. Zobacz [toowebhooks odpowiada](#hooktrigger). wartość Hello może być jedną z następujących hello:
    * _genericJson_ : punkt końcowy elementu webhook ogólnego przeznaczenia bez logiki dla określonego dostawcy.
    * _github_ : funkcja hello będzie odpowiadać tooGitHub elementów webhook. Witaj _authLevel_ właściwość nie powinna być ustawiona, jeśli to jest wybrane.
    * _zapas czasu_ : funkcja hello będzie odpowiadać tooSlack elementów webhook. Witaj _authLevel_ właściwość nie powinna być ustawiona, jeśli to jest wybrane.

<a name="httptriggerusage"></a>
### <a name="working-with-an-http-trigger-from-code"></a>Praca z wyzwalacza HTTP z kodu
Dla funkcji języka C# i F #, mogą zadeklarować typu hello Twojej toobe wejściowych wyzwalacza albo `HttpRequestMessage` lub typu niestandardowego. Jeśli wybierzesz `HttpRequestMessage`, a następnie pobierze obiektu żądania toohello pełny dostęp. Dla typu niestandardowego (na przykład POCO) funkcje podejmie treści żądania hello tooparse jako właściwości obiektu hello toopopulate JSON.

W przypadku funkcji Node.js środowisko uruchomieniowe Functions hello zapewnia treści żądania hello zamiast obiektu żądania hello.

Zobacz [przykłady wyzwalacza HTTP](#httptriggersample) na przykład sposobu użycia.


<a name="output"></a>
## <a name="http-response-output-binding"></a>Powiązania wyjściowego odpowiedzi HTTP
Użyj hello HTTP dane wyjściowe powiązania toorespond toohello HTTP żądania nadawcy. To powiązanie wymaga wyzwalacza HTTP i pozwala odpowiedź hello toocustomize skojarzony z żądaniem hello wyzwalacza. Jeśli powiązania wyjściowego HTTP nie zostanie podany, wyzwalacz HTTP zwróci o pustej treści HTTP 200 OK. 

### <a name="configuring-an-http-output-binding"></a>Konfigurowanie protokołu HTTP powiązania wyjściowego
Hello HTTP output powiązania jest definiowana za pomocą tym JSON obiektu toohello podobne, po w hello `bindings` tablicy function.json:

```json
{
    "name": "res",
    "type": "http",
    "direction": "out"
}
```
Powiązanie Hello zawiera hello następujące właściwości:

* **Nazwa** : wymagana — Witaj używane w kodzie funkcja odpowiedź hello nazwy zmiennej. Zobacz [powiązania z kodu wyjściowego roboczych protokołu HTTP z](#outputusage).
* **Typ** : wymagana — musi być ustawiona zbyt "http".
* **kierunek** : wymagana — musi być ustawiona zbyt "out".

<a name="outputusage"></a>
### <a name="working-with-an-http-output-binding-from-code"></a>Praca z HTTP output powiązania z kodu
Możesz użyć hello dane wyjściowe parametru (np. "res") toorespond toohello http lub elementu webhook wywołującego. Alternatywnie można użyć standardowego `Request.CreateResponse()` (C#) lub `context.res` tooreturn wzorca (Node.JS) do odpowiedzi. Przykłady w sposób toouse hello druga metoda, zobacz [przykłady wyzwalacza HTTP](#httptriggersample) i [przykłady wyzwalacza elementu Webhook](#hooktriggersample).


<a name="hooktrigger"></a>
## <a name="responding-toowebhooks"></a>Odpowiada toowebhooks
Wyzwalacz protokołu HTTP z hello _webHookType_ właściwość będzie skonfigurowany toorespond zbyt[elementów webhook](https://en.wikipedia.org/wiki/Webhook). Podstawowa konfiguracja Hello używa ustawienia "genericJson" hello. Umożliwia ograniczenie żądań tooonly tych przy użyciu protokołu HTTP POST i hello `application/json` typ zawartości.

Witaj wyzwalacza można dodatkowo dopasowane tooa webhook określonego dostawcy (np. [GitHub](https://developer.github.com/webhooks/) i [Slack](https://api.slack.com/outgoing-webhooks)). Jeśli jest określony dostawca, środowisko uruchomieniowe Functions hello zająć się dostawcy hello logikę weryfikacji dla Ciebie.  

### <a name="configuring-github-as-a-webhook-provider"></a>Konfigurowanie dostawcy elementu webhook GitHub
toorespond tooGitHub elementów webhook, najpierw utwórz funkcji z wyzwalaczem HTTP i ustaw hello _webHookType_ właściwości zbyt "github". Następnie skopiuj jej [adres URL](#url) i [klucz interfejsu API](#keys) w repozytorium GitHub **Dodawanie elementu webhook** strony. Zobacz GitHub [tworzenia elementów Webhook](http://go.microsoft.com/fwlink/?LinkID=761099&clcid=0x409) dokumentacji, aby uzyskać więcej informacji.

![](./media/functions-bindings-http-webhook/github-add-webhook.png)

### <a name="configuring-slack-as-a-webhook-provider"></a>Konfigurowanie zapas czasu jako dostawca elementu webhook
Hello Slack webhook generuje token dla Ciebie zamiast czekać na określeniu, dlatego należy skonfigurować klucz właściwe dla funkcji z tokenem hello z zapas czasu. Zobacz [Praca z kluczami](#keys).

<a name="url"></a>
## <a name="customizing-hello-http-endpoint"></a>Dostosowywanie hello punkt końcowy HTTP
Domyślnie podczas tworzenia funkcja wyzwalacza HTTP lub elementu WebHook, funkcja hello jest adresowanego trasa hello formularza:

    http://<yourapp>.azurewebsites.net/api/<funcname> 

Można dostosować tej trasy, używając hello opcjonalne `route` wejściowych powiązania właściwości dla elementu trigger hello HTTP. Przykład Witaj po *function.json* plik definiuje `route` właściwości dla wyzwalacza HTTP:

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

Za pomocą tej konfiguracji, funkcja hello jest teraz adresowanego z hello następujące trasy zamiast hello oryginalnego trasy.

    http://<yourapp>.azurewebsites.net/api/products/electronics/357

Dzięki temu kod funkcji hello toosupport dwa parametry adres Witaj, "kategorii" i "id". Można użyć dowolnego [ograniczenia trasy interfejsu API sieci Web](https://www.asp.net/web-api/overview/web-api-routing-and-actions/attribute-routing-in-web-api-2#constraints) z parametrami. Witaj następującego kodu funkcji języka C# korzysta z obu tych parametrów.

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

Oto hello toouse kodu funkcji Node.js takie same parametry trasy.

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

Domyślnie wszystkie trasy funkcji są poprzedzane prefiksem *interfejsu api*. Można również dostosować lub usuń prefiks hello przy użyciu hello `http.routePrefix` właściwości w Twojej *host.json* pliku. Witaj poniższy przykład umożliwia usunięcie hello *interfejsu api* prefiks trasy przy użyciu pustego ciągu dla prefiksu hello w hello *host.json* pliku.

```json
    {
      "http": {
        "routePrefix": ""
      }
    }
```

Aby uzyskać szczegółowe informacje na temat tooupdate hello *host.json* plików dla funkcji, zobacz [jak tooupdate funkcji pliki aplikacji](functions-reference.md#fileupdate). 

Aby uzyskać informacje na temat innych właściwości można skonfigurować w sieci *host.json* plików, zobacz [odwołania host.json](https://github.com/Azure/azure-webjobs-sdk-script/wiki/host.json).


<a name="keys"></a>
## <a name="working-with-keys"></a>Praca z kluczy
HttpTriggers mogą korzystać z kluczy w celu zwiększenia bezpieczeństwa. Standardowe HttpTrigger można użyć je jako klucz interfejsu API, wymagających hello klucza toobe na powitania żądania. Elementów Webhook użyć klawiszy tooauthorize żądań na różne sposoby, w zależności od tego, jakie hello dostawca obsługuje.

Klucze są przechowywane w ramach funkcji aplikacji na platformie Azure i są szyfrowane, gdy. tooview klucze, tworzenie nowych lub toonew wartości kluczy zbiorczego, przejdź tooone funkcji hello portalu i wybierz "Manage". 

Istnieją dwa typy kluczy:
- **Klucze hosta**: klucze te są współużytkowane przez wszystkie funkcje w hello funkcji aplikacji. Gdy jest używany jako klucz interfejsu API, umożliwiają one funkcja tooany dostępu w hello funkcji aplikacji.
- **Klawisze funkcyjne**: te klucze zastosować tylko toohello określone funkcje, zgodnie z którymi są zdefiniowane. Gdy jest używany jako klucz interfejsu API, te tylko Zezwalaj funkcja toothat dostępu.

Każdy klucz nosi nazwę odwołania, a na poziomie funkcji oraz hosta hello jest domyślny klucz (o nazwie "domyślne"). Witaj **klucza głównego** domyślny klucz hosta o nazwie "_master", który jest zdefiniowany dla każdej funkcji aplikacji i nie może zostać odwołany. Zapewnia dostęp administracyjny toohello runtime interfejsów API. Przy użyciu `"authLevel": "admin"` w hello powiązanie JSON będzie wymagać tego klucza toobe przedstawionych na żądanie hello; innego klucza spowoduje błąd autoryzacji.

> [!NOTE]
> Z powodu toohello podniesione uprawnienia przyznane przez klucz główny hello, nie należy udostępniać tego klucza osobom trzecim ani rozpowszechnienie go w aplikacjach klienckich natywnego. Należy zachować ostrożność podczas wybierania hello autoryzacji na poziomie administratora.
> 
> 

### <a name="api-key-authorization"></a>Autoryzacji klucza interfejsu API
Domyślnie HttpTrigger wymaga klucza interfejsu API w hello żądania HTTP. Dlatego żądanie HTTP zwykle wygląda następująco:

    https://<yourapp>.azurewebsites.net/api/<function>?code=<ApiKey>

klucz Hello może być uwzględniony w zmiennej ciągu zapytania o nazwie `code`, zgodnie z powyższym, lub można je uwzględnić w `x-functions-key` nagłówka HTTP. wartość Hello hello klucza może być dowolny klawisz funkcji zdefiniowany dla funkcji hello lub dowolnego klucz hosta.

Możesz wybrać tooallow żądań bez kluczy lub określ hello klucza głównego musi być używana przez zmianę hello `authLevel` właściwości w hello powiązanie JSON (zobacz [wyzwalacza HTTP](#httptrigger)).

### <a name="keys-and-webhooks"></a>Klucze i elementów webhook
Autoryzacji elementu Webhook jest obsługiwane przez składnik reciever elementu webhook hello, część hello HttpTrigger i mechanizmu hello w zależności od typu elementu webhook hello. Nie mechanizmu, jednak zależne od klucza. Domyślnie posłuży hello funkcja klucz o nazwie "domyślny". W razie potrzeby toouse inny klucz należy tooconfigure hello nazwa elementu webhook dostawcy toosend hello klucza z żądaniem hello w jednym z hello następujące sposoby:

- **Długość ciągu zapytania**: hello dostawcy przekazuje nazwę klucza hello w hello `clientid` parametr ciągu zapytania (np. `https://<yourapp>.azurewebsites.net/api/<funcname>?clientid=<keyname>`).
- **Nagłówek żądania**: hello dostawcy przekazuje nazwę klucza hello w hello `x-functions-clientid` nagłówka.

> [!NOTE]
> Klawisze funkcyjne mają pierwszeństwo przed klucze hosta. Jeśli dwa klucze są zdefiniowane z hello takie same nazwy, hello funkcja klucz będzie używany.
> 
> 


<a name="httptriggersample"></a>
## <a name="http-trigger-samples"></a>Przykłady wyzwalacza HTTP
Załóżmy, że masz następujące wyzwalacza HTTP w hello hello `bindings` tablicy function.json:

```json
{
    "name": "req",
    "type": "httpTrigger",
    "direction": "in",
    "authLevel": "function"
},
```

Witaj przykładu specyficzny dla języka, która sprawdza, czy `name` parametru ciągu zapytania hello lub hello treści żądania hello HTTP.

* [C#](#httptriggercsharp)
* [F#](#httptriggerfsharp)
* [Node.js](#httptriggernodejs)


<a name="httptriggercsharp"></a>
### <a name="http-trigger-sample-in-c"></a>Przykładowe wyzwalacza HTTP w języku C# #
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

Może także powiązać tooa POCO zamiast `HttpRequestMessage`. Spowoduje to uwodniony, z hello treści żądania hello, być analizowana jako JSON. Podobnie typu mogą być przekazywane dane wyjściowe odpowiedzi toohello HTTP powiązanie, a ta wartość jest zwracana jako treść odpowiedzi hello, z kodem stanu 200.
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
### <a name="http-trigger-sample-in-f"></a>Przykładowe wyzwalacza HTTP w języku F # #
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

Należy `project.json` pliku, który używa NuGet tooreference hello `FSharp.Interop.Dynamic` i `Dynamitey` zestawów, w następujący sposób:

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

Zostanie użyty NuGet toofetch zależności i odwoływać je w skrypcie.

<a name="httptriggernodejs"></a>
### <a name="http-trigger-sample-in-nodejs"></a>Przykładowe wyzwalacza HTTP w środowisku Node.JS
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
## <a name="webhook-samples"></a>Przykłady elementu Webhook
Załóżmy, że masz hello następującego elementu webhook wyzwalacza w hello `bindings` tablicy function.json:

```json
{
    "webHookType": "github",
    "name": "req",
    "type": "httpTrigger",
    "direction": "in",
},
```

Zobacz przykład specyficzny dla języka hello, który rejestruje komentarze problem GitHub.

* [C#](#hooktriggercsharp)
* [F#](#hooktriggerfsharp)
* [Node.js](#hooktriggernodejs)

<a name="hooktriggercsharp"></a>

### <a name="webhook-sample-in-c"></a>Przykład elementu Webhook w języku C# #
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

### <a name="webhook-sample-in-f"></a>Przykład elementu Webhook w języku F # #
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

### <a name="webhook-sample-in-nodejs"></a>Przykład elementu Webhook w środowisku Node.JS
```javascript
module.exports = function (context, data) {
    context.log('GitHub WebHook triggered!', data.comment.body);
    context.res = { body: 'New GitHub comment: ' + data.comment.body };
    context.done();
};
```


## <a name="next-steps"></a>Następne kroki
[!INCLUDE [next steps](../../includes/functions-bindings-next-steps.md)]

