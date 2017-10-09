---
title: "aaaWork z wyzwalaczy i powiązań w usługi Azure Functions | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toouse wyzwalaczy i powiązań w tooconnect usługi Azure Functions Twojej zdarzenia tooonline wykonanie kodu i usług w chmurze."
services: functions
documentationcenter: na
author: lindydonna
manager: erikre
editor: 
tags: 
keywords: "usługa Azure Functions, funkcje, przetwarzanie zdarzeń, elementy webhook, obliczanie dynamiczne, architektura bez serwera"
ms.assetid: cbc7460a-4d8a-423f-a63e-1cd33fef7252
ms.service: functions
ms.devlang: multiple
ms.topic: reference
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 05/30/2017
ms.author: donnam
ms.openlocfilehash: eb2ebfca172fcc8c0f479adbcfec99e90fc33615
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-functions-triggers-and-bindings-concepts"></a>Azure funkcje wyzwalaczy i powiązań pojęcia
Środowisko Azure Functions umożliwia toowrite kodu w tooevents odpowiedzi na platformie Azure i innych usług za pośrednictwem *wyzwalaczy* i *powiązania*. Ten artykuł zawiera omówienie wyzwalaczy i powiązań dla wszystkich obsługiwanych języków programowania. Funkcje, które są typowe powiązania tooall są opisane w tym miejscu.

## <a name="overview"></a>Omówienie

Wyzwalaczy i powiązań są toodefine deklaratywne sposób wywoływania funkcji i jakie dane działa z. A *wyzwalacza* definiuje sposób wywoływania funkcji. Funkcja musi mieć dokładnie jeden wyzwalacz. Wyzwalacze mieć skojarzone dane, co jest zazwyczaj ładunku hello, która wyzwoliła hello funkcji. 

Wejście i wyjście *powiązania* Podaj deklaratywne tooconnect toodata od w kodzie. Podobne tootriggers, należy określić parametry połączenia i inne właściwości konfiguracji funkcji. Powiązania są opcjonalne i mieć wielu danych wejściowych i wyjściowych powiązania funkcji. 

Przy użyciu wyzwalaczy i powiązań, można napisać kod, który jest bardziej ogólnym i wykonuje nie umieszczaj hello szczegóły hello usług, z którymi współpracuje. Dane pochodzące z usługi po prostu stają się wartości wejściowe dla kodu funkcji. Usługa tooanother danych toooutput (takich jak tworzenie nowego wiersza w usłudze Azure Table Storage) Użyj hello wartości zwracanej przez metodę hello. Lub toooutput wiele wartości, należy użyć obiektu pomocnika. Mieć wyzwalaczy i powiązań **nazwa** właściwość, która jest identyfikatorem użyć w powiązaniu hello tooaccess Twojego kodu.

Można skonfigurować wyzwalaczy i powiązań w hello **integracji** kartę w portalu Azure Functions hello. W obszarze obejmuje hello hello interfejsu użytkownika modyfikuje plik o nazwie *function.json* pliku w katalogu funkcji hello. Ten plik można edytować, zmieniając toohello **Zaawansowany edytor**.

Witaj poniższej tabeli przedstawiono hello wyzwalaczy i powiązań, które są obsługiwane w środowisku Azure Functions. 

[!INCLUDE [Full bindings table](../../includes/functions-bindings.md)]

### <a name="example-queue-trigger-and-table-output-binding"></a>Przykład: wyzwalacz kolejki i tabeli powiązania wyjściowego

Załóżmy, że ma toowrite nowe tooAzure wiersza tabeli magazynu przy każdym wyświetleniu nowego komunikatu w magazynie kolejek Azure. W tym scenariuszu można implementować przy użyciu kolejek platformy Azure i wyzwalaczy tabeli powiązania wyjściowego. 

Wyzwalacz kolejki wymaga następujących informacji w hello hello **integracji** karty:

* Witaj Nazwa ustawienia aplikacji hello, zawierający parametry połączenia konta magazynu hello hello kolejki
* Nazwa kolejki Hello
* Witaj identyfikator w zawartości hello tooread kodu z hello kolejki wiadomości, takie jak `order`.

tooAzure toowrite magazyn tabel za pomocą powiązania wyjściowego hello poniższe informacje:

* Witaj Nazwa ustawienia aplikacji hello, zawierający parametry połączenia konta magazynu hello hello tabeli
* Nazwa tabeli Hello
* Identyfikator Hello w Twojej toocreate kod wyjścia elementy lub hello wartość zwrócona przez funkcję hello.

Powiązania użyj ustawienia aplikacji dla hello tooenforce ciągów połączenia najlepszym rozwiązaniem, które *function.json* nie zawiera kluczy tajnych usługi.

Następnie należy użyć identyfikatorów hello podane toointegrate z usługą Azure Storage w kodzie.

```cs
#r "Newtonsoft.Json"

using Newtonsoft.Json.Linq;

// From an incoming queue message that is a JSON object, add fields and write tooTable Storage
// hello method return value creates a new row in Table Storage
public static Person Run(JObject order, TraceWriter log)
{
    return new Person() { 
            PartitionKey = "Orders", 
            RowKey = Guid.NewGuid().ToString(),  
            Name = order["Name"].ToString(),
            MobileNumber = order["MobileNumber"].ToString() };  
}
 
public class Person
{
    public string PartitionKey { get; set; }
    public string RowKey { get; set; }
    public string Name { get; set; }
    public string MobileNumber { get; set; }
}
```

```javascript
// From an incoming queue message that is a JSON object, add fields and write tooTable Storage
// hello second parameter toocontext.done is used as hello value for hello new row
module.exports = function (context, order) {
    order.PartitionKey = "Orders";
    order.RowKey = generateRandomId(); 

    context.done(null, order);
};

function generateRandomId() {
    return Math.random().toString(36).substring(2, 15) +
        Math.random().toString(36).substring(2, 15);
}
```

Oto hello *function.json* toohello poprzedzających kodu, który odpowiada. Należy pamiętać, że hello tej samej konfiguracji mogą być używane, niezależnie od języka hello hello implementacji funkcji.

```json
{
  "bindings": [
    {
      "name": "order",
      "type": "queueTrigger",
      "direction": "in",
      "queueName": "myqueue-items",
      "connection": "MY_STORAGE_ACCT_APP_SETTING"
    },
    {
      "name": "$return",
      "type": "table",
      "direction": "out",
      "tableName": "outTable",
      "connection": "MY_TABLE_STORAGE_ACCT_APP_SETTING"
    }
  ]
}
```
tooview i edytowanie hello zawartość *function.json* w hello portalu Azure kliknij hello **Zaawansowany edytor** opcji na powitania **integracji** kartę funkcji.

Aby uzyskać więcej przykładów kodu i szczegółowe informacje o integracji z usługą Azure Storage, zobacz [usługi Azure Functions wyzwalaczy i powiązań usługi Azure Storage](functions-bindings-storage.md).

### <a name="binding-direction"></a>Kierunek powiązania

Wszystkich wyzwalaczy i powiązań ma `direction` właściwości:

- Wyzwalacze kierunku hello jest zawsze`in`
- Użyj powiązań wejściowych i wyjściowych `in` i`out`
- Niektóre powiązania obsługuje specjalne kierunku `inout`. Jeśli używasz `inout`, tylko hello **Zaawansowany edytor** jest dostępna w hello **integracji** kartę.

## <a name="using-hello-function-return-type-tooreturn-a-single-output"></a>Przy użyciu tooreturn zwracany typ funkcji hello pojedynczego wyjścia

Hello poprzednim przykładzie pokazano, jak toouse hello funkcja wartości zwracanej tooprovide output tooa powiązania, które jest realizowane za pośrednictwem hello specjalną nazwą parametru `$return`. (To jest tylko obsługiwana w językach, które mają wartość zwracaną, takich jak C#, JavaScript i F #.) Jeśli funkcja ma wiele powiązań danych wyjściowych, użyj `$return` tylko jednego hello powiązań danych wyjściowych. 

```json
// excerpt of function.json
{
    "name": "$return",
    "type": "blob",
    "direction": "out",
    "path": "output-container/{id}"
}
```

Przykłady Hello poniżej Pokaż jak przywrócić typy są używane z powiązaniami danych wyjściowych w języku C#, JavaScript i F #.

```cs
// C# example: use method return value for output binding
public static string Run(WorkItem input, TraceWriter log)
{
    string json = string.Format("{{ \"id\": \"{0}\" }}", input.Id);
    log.Info($"C# script processed queue message. Item={json}");
    return json;
}
```

```cs
// C# example: async method, using return value for output binding
public static Task<string> Run(WorkItem input, TraceWriter log)
{
    string json = string.Format("{{ \"id\": \"{0}\" }}", input.Id);
    log.Info($"C# script processed queue message. Item={json}");
    return json;
}
```

```javascript
// JavaScript: return a value in hello second parameter toocontext.done
module.exports = function (context, input) {
    var json = JSON.stringify(input);
    context.log('Node.js script processed queue message', json);
    context.done(null, json);
}
```

```fsharp
// F# example: use return value for output binding
let Run(input: WorkItem, log: TraceWriter) =
    let json = String.Format("{{ \"id\": \"{0}\" }}", input.Id)   
    log.Info(sprintf "F# script processed queue message '%s'" json)
    json
```

## <a name="binding-datatype-property"></a>Właściwość dataType powiązania

W środowisku .NET należy użyć hello typy toodefine hello — typ danych dla danych wejściowych. Na przykład użyć `string` toobind toohello tekst wyzwalacz kolejki i tooread tablicy typu byte, jako wartość binarną.

Dla języków, które są dynamicznie wpisane takich jak JavaScript, użyj hello `dataType` właściwości w definicji powiązania hello. Na przykład tooread hello zawartości żądania HTTP w formacie binarnym, użyj typu hello `binary`:

```json
{
    "type": "httpTrigger",
    "name": "req",
    "direction": "in",
    "dataType": "binary"
}
```

Inne opcje `dataType` są `stream` i `string`.

## <a name="resolving-app-settings"></a>Rozpoznawanie ustawień aplikacji
Najlepszym rozwiązaniem kluczy tajnych i parametry połączenia mają być zarządzane przy użyciu ustawienia aplikacji, a nie plików konfiguracyjnych. To ogranicza dostęp do kluczy tajnych z toothese i umożliwia bezpieczne toostore *function.json* w repozytorium kontroli źródła publicznego.

Ustawienia aplikacji są przydatne także w przypadku, gdy konfiguracja toochange opartych na środowisku hello. Na przykład w środowisku testowym można toomonitor innego kontenera magazynu kolejek i obiektów blob.

Ustawienia aplikacji zostaną rozwiązane w każdym przypadku, gdy wartość jest ujęta w znaki procentu, takich jak `%MyAppSetting%`. Należy pamiętać, że hello `connection` wyzwalaczy i powiązań jest szczególnych przypadkach i automatycznie rozpoznaje wartości jako ustawienia aplikacji. 

Witaj poniższym przykładzie jest wyzwalacz kolejki, który używa ustawienia aplikacji `%input-queue-name%` toodefine hello kolejki tootrigger na.

```json
{
  "bindings": [
    {
      "name": "order",
      "type": "queueTrigger",
      "direction": "in",
      "queueName": "%input-queue-name%",
      "connection": "MY_STORAGE_ACCT_APP_SETTING"
    }
  ]
}
```

## <a name="trigger-metadata-properties"></a>Właściwości metadanych wyzwalacza

W ładunku danych toohello dodanie udostępniane przez wyzwalacz (na przykład hello kolejki wiadomości, który wywołał funkcję) wiele wyzwalaczy, podaj wartości dodatkowe metadane. Te wartości może służyć jako parametry wejściowe w C# i F # lub we właściwościach hello `context.bindings` obiektu w języku JavaScript. 

Na przykład wyzwalacz kolejki obsługuje hello następujące właściwości:

* QueueTrigger - wyzwalania zawartość komunikatu, jeśli prawidłowy ciąg
* DequeueCount
* expirationTime
* Identyfikator
* InsertionTime
* NextVisibleTime
* Elementu PopReceipt

Szczegółowe informacje o właściwości metadanych dla każdego wyzwalacza są opisane w hello odpowiedni temat odwołania. Dokumentacja jest również dostępna w hello **integracji** kartę hello portal hello **dokumentacji** sekcji poniżej obszar konfiguracji powiązania hello.  

Na przykład, ponieważ wyzwalacze obiektu blob mają pewne opóźnienia, funkcja toorun wyzwalacza kolejki użytkownika (zobacz [wyzwalacza magazynu obiektów Blob](functions-bindings-storage-blob.md#storage-blob-trigger). wiadomości powitania kolejki może zawierać tootrigger filename obiektu blob hello na. Przy użyciu hello `queueTrigger` właściwości metadanych to zachowanie można określić w konfiguracji, a nie w kodzie.

```json
  "bindings": [
    {
      "name": "myQueueItem",
      "type": "queueTrigger",
      "queueName": "myqueue-items",
      "connection": "MyStorageConnection",
    },
    {
      "name": "myInputBlob",
      "type": "blob",
      "path": "samples-workitems/{queueTrigger}",
      "direction": "in",
      "connection": "MyStorageConnection"
    }
  ]
```

Właściwości metadanych od wyzwalacza można również w *powiązanie wyrażenie* dla powiązania innego, jako hello opisane w następującej sekcji.

## <a name="binding-expressions-and-patterns"></a>Wyrażenia wiązania i wzorce

Jedną z najbardziej zaawansowanych funkcji wyzwalaczy i powiązań hello jest *wyrażenia powiązania*. W ramach wiązania, można zdefiniować wzorzec wyrażenia, które mogą być następnie używane w pozostałych powiązaniach lub kodu. Można także metadanych wyzwalacza w wyrażenia, powiązania jako Pokaż w próbce hello hello powyższej sekcji.

Na przykład, załóżmy, że ma tooresize obrazów w kontenera magazynu obiektów blob w szczególności, toohello podobne **zmiany rozmiaru obrazu** szablonu w hello **nową funkcję** strony. Przejdź za**nową funkcję** -> języka **C#** -> Scenariusz **przykłady** -> **ImageResizer CSharp**. 

Oto hello *function.json* definicji:

```json
{
  "bindings": [
    {
      "name": "image",
      "type": "blobTrigger",
      "path": "sample-images/{filename}",
      "direction": "in",
      "connection": "MyStorageConnection"
    },
    {
      "name": "imageSmall",
      "type": "blob",
      "path": "sample-images-sm/{filename}",
      "direction": "out",
      "connection": "MyStorageConnection"
    }
  ],
}
```

Zwróć uwagę, że hello `filename` parametr jest używany w zarówno definicję wyzwalacza hello obiektów blob, jak i obiektów blob hello powiązania wyjściowego. Ten parametr może również w kodzie funkcji.

```csharp
// C# example of binding too{filename}
public static void Run(Stream image, string filename, Stream imageSmall, TraceWriter log)  
{
    log.Info($"Blob trigger processing: {filename}");
    // ...
} 
```

<!--TODO: add JavaScript example -->
<!-- Blocked by bug https://github.com/Azure/Azure-Functions/issues/248 -->


### <a name="random-guids"></a>Losowe identyfikatory GUID
Środowisko Azure Functions zapewnia składni wygody generowania identyfikatorów GUID w powiązania, za pośrednictwem hello `{rand-guid}` powiązanie wyrażenia. Witaj poniższym przykładzie użyto tego toogenerate nazwę unikatową obiektów blob: 

```json
{
  "type": "blob",
  "name": "blobOutput",
  "direction": "out",
  "path": "my-output-container/{rand-guid}"
}
```

### <a name="current-time"></a>Bieżący czas

Można użyć wyrażenia powiązania hello `DateTime`, która rozwiązuje zbyt`DateTime.UtcNow`.

```json
{
  "type": "blob",
  "name": "blobOutput",
  "direction": "out",
  "path": "my-output-container/{DateTime}"
}
```

## <a name="bind-toocustom-input-properties-in-a-binding-expression"></a>Powiąż właściwości wejściowe toocustom wyrażenia powiązania

Wyrażenia powiązania można także odwoływać właściwości, które są zdefiniowane w ładunku wyzwalacza hello, sama. Na przykład można toodynamically pliku magazynu obiektów blob tooa powiązania z nazwą w elementu webhook.

Na przykład Witaj po *function.json* używa właściwość o nazwie `BlobName` z ładunku wyzwalacza hello:

```json
{
  "bindings": [
    {
      "name": "info",
      "type": "httpTrigger",
      "direction": "in",
      "webHookType": "genericJson",
    },
    {
      "name": "blobContents",
      "type": "blob",
      "direction": "in",
      "path": "strings/{BlobName}",
      "connection": "AzureWebJobsStorage"
    },
    {
      "name": "res",
      "type": "http",
      "direction": "out"
    }
  ]
}
```

tooaccomplish ten w języku C# i F #, należy zdefiniować POCO, definiujący hello pola, które będą deserializowane w ładunku wyzwalacza hello.

```csharp
using System.Net;

public class BlobInfo
{
    public string BlobName { get; set; }
}
  
public static HttpResponseMessage Run(HttpRequestMessage req, BlobInfo info, string blobContents)
{
    if (blobContents == null) {
        return req.CreateResponse(HttpStatusCode.NotFound);
    } 

    return req.CreateResponse(HttpStatusCode.OK, new {
        data = $"{blobContents}"
    });
}
```

W języku JavaScript deserializacji JSON jest wykonywana automatycznie i można używać właściwości hello bezpośrednio.

```javascript
module.exports = function (context, info) {
    if ('BlobName' in info) {
        context.res = {
            body: { 'data': context.bindings.blobContents }
        }
    }
    else {
        context.res = {
            status: 404
        };
    }
    context.done();
}
```

## <a name="configuring-binding-data-at-runtime"></a>Konfigurowanie powiązania danych w czasie wykonywania

W języku C# i innych języków .NET, można użyć wzorca wiązania konieczne jako min. toohello deklaratywne powiązania w *function.json*. Powiązanie konieczne jest przydatne, gdy Parametry wiążące muszą toobe obliczane w czasie środowiska uruchomieniowego zamiast projektu. toolearn więcej, zobacz [powiązania w czasie wykonywania za pośrednictwem powiązania imperatywnych](functions-reference-csharp.md#imperative-bindings) w dokumentacja dla deweloperów hello C#.

## <a name="next-steps"></a>Następne kroki
Aby uzyskać więcej informacji na określone powiązanie Zobacz hello następujące artykuły:

- [HTTP i elementy webhook](functions-bindings-http-webhook.md)
- [Czasomierz](functions-bindings-timer.md)
- [Queue Storage](functions-bindings-storage-queue.md)
- [Blob Storage](functions-bindings-storage-blob.md)
- [Table Storage](functions-bindings-storage-table.md)
- [Centrum zdarzeń](functions-bindings-event-hubs.md)
- [Service Bus](functions-bindings-service-bus.md)
- [Cosmos DB](functions-bindings-documentdb.md)
- [SendGrid](functions-bindings-sendgrid.md)
- [Twilio](functions-bindings-twilio.md)
- [Notification Hubs](functions-bindings-notification-hubs.md)
- [Mobile Apps](functions-bindings-mobile-apps.md)
- [Plik zewnętrzny](functions-bindings-external-file.md)
