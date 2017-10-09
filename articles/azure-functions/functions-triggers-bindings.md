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
# <a name="azure-functions-triggers-and-bindings-concepts"></a><span data-ttu-id="b251f-104">Azure funkcje wyzwalaczy i powiązań pojęcia</span><span class="sxs-lookup"><span data-stu-id="b251f-104">Azure Functions triggers and bindings concepts</span></span>
<span data-ttu-id="b251f-105">Środowisko Azure Functions umożliwia toowrite kodu w tooevents odpowiedzi na platformie Azure i innych usług za pośrednictwem *wyzwalaczy* i *powiązania*.</span><span class="sxs-lookup"><span data-stu-id="b251f-105">Azure Functions allows you toowrite code in response tooevents in Azure and other services, through *triggers* and *bindings*.</span></span> <span data-ttu-id="b251f-106">Ten artykuł zawiera omówienie wyzwalaczy i powiązań dla wszystkich obsługiwanych języków programowania.</span><span class="sxs-lookup"><span data-stu-id="b251f-106">This article is a conceptual overview of triggers and bindings for all supported programming languages.</span></span> <span data-ttu-id="b251f-107">Funkcje, które są typowe powiązania tooall są opisane w tym miejscu.</span><span class="sxs-lookup"><span data-stu-id="b251f-107">Features that are common tooall bindings are described here.</span></span>

## <a name="overview"></a><span data-ttu-id="b251f-108">Omówienie</span><span class="sxs-lookup"><span data-stu-id="b251f-108">Overview</span></span>

<span data-ttu-id="b251f-109">Wyzwalaczy i powiązań są toodefine deklaratywne sposób wywoływania funkcji i jakie dane działa z.</span><span class="sxs-lookup"><span data-stu-id="b251f-109">Triggers and bindings are a declarative way toodefine how a function is invoked and what data it works with.</span></span> <span data-ttu-id="b251f-110">A *wyzwalacza* definiuje sposób wywoływania funkcji.</span><span class="sxs-lookup"><span data-stu-id="b251f-110">A *trigger* defines how a function is invoked.</span></span> <span data-ttu-id="b251f-111">Funkcja musi mieć dokładnie jeden wyzwalacz.</span><span class="sxs-lookup"><span data-stu-id="b251f-111">A function must have exactly one trigger.</span></span> <span data-ttu-id="b251f-112">Wyzwalacze mieć skojarzone dane, co jest zazwyczaj ładunku hello, która wyzwoliła hello funkcji.</span><span class="sxs-lookup"><span data-stu-id="b251f-112">Triggers have associated data, which is usually hello payload that triggered hello function.</span></span> 

<span data-ttu-id="b251f-113">Wejście i wyjście *powiązania* Podaj deklaratywne tooconnect toodata od w kodzie.</span><span class="sxs-lookup"><span data-stu-id="b251f-113">Input and output *bindings* provide a declarative way tooconnect toodata from within your code.</span></span> <span data-ttu-id="b251f-114">Podobne tootriggers, należy określić parametry połączenia i inne właściwości konfiguracji funkcji.</span><span class="sxs-lookup"><span data-stu-id="b251f-114">Similar tootriggers, you specify connection strings and other properties in your function configuration.</span></span> <span data-ttu-id="b251f-115">Powiązania są opcjonalne i mieć wielu danych wejściowych i wyjściowych powiązania funkcji.</span><span class="sxs-lookup"><span data-stu-id="b251f-115">Bindings are optional and a function can have multiple input and output bindings.</span></span> 

<span data-ttu-id="b251f-116">Przy użyciu wyzwalaczy i powiązań, można napisać kod, który jest bardziej ogólnym i wykonuje nie umieszczaj hello szczegóły hello usług, z którymi współpracuje.</span><span class="sxs-lookup"><span data-stu-id="b251f-116">Using triggers and bindings, you can write code that is more generic and does not hardcode hello details of hello services with which it interacts.</span></span> <span data-ttu-id="b251f-117">Dane pochodzące z usługi po prostu stają się wartości wejściowe dla kodu funkcji.</span><span class="sxs-lookup"><span data-stu-id="b251f-117">Data coming from services simply become input values for your function code.</span></span> <span data-ttu-id="b251f-118">Usługa tooanother danych toooutput (takich jak tworzenie nowego wiersza w usłudze Azure Table Storage) Użyj hello wartości zwracanej przez metodę hello.</span><span class="sxs-lookup"><span data-stu-id="b251f-118">toooutput data tooanother service (such as creating a new row in Azure Table Storage), use hello return value of hello method.</span></span> <span data-ttu-id="b251f-119">Lub toooutput wiele wartości, należy użyć obiektu pomocnika.</span><span class="sxs-lookup"><span data-stu-id="b251f-119">Or, if you need toooutput multiple values, use a helper object.</span></span> <span data-ttu-id="b251f-120">Mieć wyzwalaczy i powiązań **nazwa** właściwość, która jest identyfikatorem użyć w powiązaniu hello tooaccess Twojego kodu.</span><span class="sxs-lookup"><span data-stu-id="b251f-120">Triggers and bindings have a **name** property, which is an identifier you use in your code tooaccess hello binding.</span></span>

<span data-ttu-id="b251f-121">Można skonfigurować wyzwalaczy i powiązań w hello **integracji** kartę w portalu Azure Functions hello.</span><span class="sxs-lookup"><span data-stu-id="b251f-121">You can configure triggers and bindings in hello **Integrate** tab in hello Azure Functions portal.</span></span> <span data-ttu-id="b251f-122">W obszarze obejmuje hello hello interfejsu użytkownika modyfikuje plik o nazwie *function.json* pliku w katalogu funkcji hello.</span><span class="sxs-lookup"><span data-stu-id="b251f-122">Under hello covers, hello UI modifies a file called *function.json* file in hello function directory.</span></span> <span data-ttu-id="b251f-123">Ten plik można edytować, zmieniając toohello **Zaawansowany edytor**.</span><span class="sxs-lookup"><span data-stu-id="b251f-123">You can edit this file by changing toohello **Advanced editor**.</span></span>

<span data-ttu-id="b251f-124">Witaj poniższej tabeli przedstawiono hello wyzwalaczy i powiązań, które są obsługiwane w środowisku Azure Functions.</span><span class="sxs-lookup"><span data-stu-id="b251f-124">hello following table shows hello triggers and bindings that are supported with Azure Functions.</span></span> 

[!INCLUDE [Full bindings table](../../includes/functions-bindings.md)]

### <a name="example-queue-trigger-and-table-output-binding"></a><span data-ttu-id="b251f-125">Przykład: wyzwalacz kolejki i tabeli powiązania wyjściowego</span><span class="sxs-lookup"><span data-stu-id="b251f-125">Example: queue trigger and table output binding</span></span>

<span data-ttu-id="b251f-126">Załóżmy, że ma toowrite nowe tooAzure wiersza tabeli magazynu przy każdym wyświetleniu nowego komunikatu w magazynie kolejek Azure.</span><span class="sxs-lookup"><span data-stu-id="b251f-126">Suppose you want toowrite a new row tooAzure Table Storage whenever a new message appears in Azure Queue Storage.</span></span> <span data-ttu-id="b251f-127">W tym scenariuszu można implementować przy użyciu kolejek platformy Azure i wyzwalaczy tabeli powiązania wyjściowego.</span><span class="sxs-lookup"><span data-stu-id="b251f-127">This scenario can be implemented using an Azure Queue trigger and a Table output binding.</span></span> 

<span data-ttu-id="b251f-128">Wyzwalacz kolejki wymaga następujących informacji w hello hello **integracji** karty:</span><span class="sxs-lookup"><span data-stu-id="b251f-128">A queue trigger requires hello following information in hello **Integrate** tab:</span></span>

* <span data-ttu-id="b251f-129">Witaj Nazwa ustawienia aplikacji hello, zawierający parametry połączenia konta magazynu hello hello kolejki</span><span class="sxs-lookup"><span data-stu-id="b251f-129">hello name of hello app setting that contains hello storage account connection string for hello queue</span></span>
* <span data-ttu-id="b251f-130">Nazwa kolejki Hello</span><span class="sxs-lookup"><span data-stu-id="b251f-130">hello queue name</span></span>
* <span data-ttu-id="b251f-131">Witaj identyfikator w zawartości hello tooread kodu z hello kolejki wiadomości, takie jak `order`.</span><span class="sxs-lookup"><span data-stu-id="b251f-131">hello identifier in your code tooread hello contents of hello queue message, such as `order`.</span></span>

<span data-ttu-id="b251f-132">tooAzure toowrite magazyn tabel za pomocą powiązania wyjściowego hello poniższe informacje:</span><span class="sxs-lookup"><span data-stu-id="b251f-132">toowrite tooAzure Table Storage, use an output binding with hello following details:</span></span>

* <span data-ttu-id="b251f-133">Witaj Nazwa ustawienia aplikacji hello, zawierający parametry połączenia konta magazynu hello hello tabeli</span><span class="sxs-lookup"><span data-stu-id="b251f-133">hello name of hello app setting that contains hello storage account connection string for hello table</span></span>
* <span data-ttu-id="b251f-134">Nazwa tabeli Hello</span><span class="sxs-lookup"><span data-stu-id="b251f-134">hello table name</span></span>
* <span data-ttu-id="b251f-135">Identyfikator Hello w Twojej toocreate kod wyjścia elementy lub hello wartość zwrócona przez funkcję hello.</span><span class="sxs-lookup"><span data-stu-id="b251f-135">hello identifier in your code toocreate output items, or hello return value from hello function.</span></span>

<span data-ttu-id="b251f-136">Powiązania użyj ustawienia aplikacji dla hello tooenforce ciągów połączenia najlepszym rozwiązaniem, które *function.json* nie zawiera kluczy tajnych usługi.</span><span class="sxs-lookup"><span data-stu-id="b251f-136">Bindings use app settings for connection strings tooenforce hello best practice that *function.json* does not contain service secrets.</span></span>

<span data-ttu-id="b251f-137">Następnie należy użyć identyfikatorów hello podane toointegrate z usługą Azure Storage w kodzie.</span><span class="sxs-lookup"><span data-stu-id="b251f-137">Then, use hello identifiers you provided toointegrate with Azure Storage in your code.</span></span>

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

<span data-ttu-id="b251f-138">Oto hello *function.json* toohello poprzedzających kodu, który odpowiada.</span><span class="sxs-lookup"><span data-stu-id="b251f-138">Here is hello *function.json* that corresponds toohello preceding code.</span></span> <span data-ttu-id="b251f-139">Należy pamiętać, że hello tej samej konfiguracji mogą być używane, niezależnie od języka hello hello implementacji funkcji.</span><span class="sxs-lookup"><span data-stu-id="b251f-139">Note that hello same configuration can be used, regardless of hello language of hello function implementation.</span></span>

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
<span data-ttu-id="b251f-140">tooview i edytowanie hello zawartość *function.json* w hello portalu Azure kliknij hello **Zaawansowany edytor** opcji na powitania **integracji** kartę funkcji.</span><span class="sxs-lookup"><span data-stu-id="b251f-140">tooview and edit hello contents of *function.json* in hello Azure portal, click hello **Advanced editor** option on hello **Integrate** tab of your function.</span></span>

<span data-ttu-id="b251f-141">Aby uzyskać więcej przykładów kodu i szczegółowe informacje o integracji z usługą Azure Storage, zobacz [usługi Azure Functions wyzwalaczy i powiązań usługi Azure Storage](functions-bindings-storage.md).</span><span class="sxs-lookup"><span data-stu-id="b251f-141">For more code examples and details on integrating with Azure Storage, see [Azure Functions triggers and bindings for Azure Storage](functions-bindings-storage.md).</span></span>

### <a name="binding-direction"></a><span data-ttu-id="b251f-142">Kierunek powiązania</span><span class="sxs-lookup"><span data-stu-id="b251f-142">Binding direction</span></span>

<span data-ttu-id="b251f-143">Wszystkich wyzwalaczy i powiązań ma `direction` właściwości:</span><span class="sxs-lookup"><span data-stu-id="b251f-143">All triggers and bindings have a `direction` property:</span></span>

- <span data-ttu-id="b251f-144">Wyzwalacze kierunku hello jest zawsze`in`</span><span class="sxs-lookup"><span data-stu-id="b251f-144">For triggers, hello direction is always `in`</span></span>
- <span data-ttu-id="b251f-145">Użyj powiązań wejściowych i wyjściowych `in` i`out`</span><span class="sxs-lookup"><span data-stu-id="b251f-145">Input and output bindings use `in` and `out`</span></span>
- <span data-ttu-id="b251f-146">Niektóre powiązania obsługuje specjalne kierunku `inout`.</span><span class="sxs-lookup"><span data-stu-id="b251f-146">Some bindings support a special direction `inout`.</span></span> <span data-ttu-id="b251f-147">Jeśli używasz `inout`, tylko hello **Zaawansowany edytor** jest dostępna w hello **integracji** kartę.</span><span class="sxs-lookup"><span data-stu-id="b251f-147">If you use `inout`, only hello **Advanced editor** is available in hello **Integrate** tab.</span></span>

## <a name="using-hello-function-return-type-tooreturn-a-single-output"></a><span data-ttu-id="b251f-148">Przy użyciu tooreturn zwracany typ funkcji hello pojedynczego wyjścia</span><span class="sxs-lookup"><span data-stu-id="b251f-148">Using hello function return type tooreturn a single output</span></span>

<span data-ttu-id="b251f-149">Hello poprzednim przykładzie pokazano, jak toouse hello funkcja wartości zwracanej tooprovide output tooa powiązania, które jest realizowane za pośrednictwem hello specjalną nazwą parametru `$return`.</span><span class="sxs-lookup"><span data-stu-id="b251f-149">hello preceding example shows how toouse hello function return value tooprovide output tooa binding, which is achieved by using hello special name parameter `$return`.</span></span> <span data-ttu-id="b251f-150">(To jest tylko obsługiwana w językach, które mają wartość zwracaną, takich jak C#, JavaScript i F #.) Jeśli funkcja ma wiele powiązań danych wyjściowych, użyj `$return` tylko jednego hello powiązań danych wyjściowych.</span><span class="sxs-lookup"><span data-stu-id="b251f-150">(This is only supported in languages that have a return value, such as C#, JavaScript, and F#.) If a function has multiple output bindings, use `$return` for only one of hello output bindings.</span></span> 

```json
// excerpt of function.json
{
    "name": "$return",
    "type": "blob",
    "direction": "out",
    "path": "output-container/{id}"
}
```

<span data-ttu-id="b251f-151">Przykłady Hello poniżej Pokaż jak przywrócić typy są używane z powiązaniami danych wyjściowych w języku C#, JavaScript i F #.</span><span class="sxs-lookup"><span data-stu-id="b251f-151">hello examples below show how return types are used with output bindings in C#, JavaScript, and F#.</span></span>

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

## <a name="binding-datatype-property"></a><span data-ttu-id="b251f-152">Właściwość dataType powiązania</span><span class="sxs-lookup"><span data-stu-id="b251f-152">Binding dataType property</span></span>

<span data-ttu-id="b251f-153">W środowisku .NET należy użyć hello typy toodefine hello — typ danych dla danych wejściowych.</span><span class="sxs-lookup"><span data-stu-id="b251f-153">In .NET, use hello types toodefine hello data type for input data.</span></span> <span data-ttu-id="b251f-154">Na przykład użyć `string` toobind toohello tekst wyzwalacz kolejki i tooread tablicy typu byte, jako wartość binarną.</span><span class="sxs-lookup"><span data-stu-id="b251f-154">For instance, use `string` toobind toohello text of a queue trigger and a byte array tooread as binary.</span></span>

<span data-ttu-id="b251f-155">Dla języków, które są dynamicznie wpisane takich jak JavaScript, użyj hello `dataType` właściwości w definicji powiązania hello.</span><span class="sxs-lookup"><span data-stu-id="b251f-155">For languages that are dynamically typed such as JavaScript, use hello `dataType` property in hello binding definition.</span></span> <span data-ttu-id="b251f-156">Na przykład tooread hello zawartości żądania HTTP w formacie binarnym, użyj typu hello `binary`:</span><span class="sxs-lookup"><span data-stu-id="b251f-156">For example, tooread hello content of an HTTP request in binary format, use hello type `binary`:</span></span>

```json
{
    "type": "httpTrigger",
    "name": "req",
    "direction": "in",
    "dataType": "binary"
}
```

<span data-ttu-id="b251f-157">Inne opcje `dataType` są `stream` i `string`.</span><span class="sxs-lookup"><span data-stu-id="b251f-157">Other options for `dataType` are `stream` and `string`.</span></span>

## <a name="resolving-app-settings"></a><span data-ttu-id="b251f-158">Rozpoznawanie ustawień aplikacji</span><span class="sxs-lookup"><span data-stu-id="b251f-158">Resolving app settings</span></span>
<span data-ttu-id="b251f-159">Najlepszym rozwiązaniem kluczy tajnych i parametry połączenia mają być zarządzane przy użyciu ustawienia aplikacji, a nie plików konfiguracyjnych.</span><span class="sxs-lookup"><span data-stu-id="b251f-159">As a best practice, secrets and connection strings should be managed using app settings, rather than configuration files.</span></span> <span data-ttu-id="b251f-160">To ogranicza dostęp do kluczy tajnych z toothese i umożliwia bezpieczne toostore *function.json* w repozytorium kontroli źródła publicznego.</span><span class="sxs-lookup"><span data-stu-id="b251f-160">This limits access toothese secrets and makes it safe toostore *function.json* in a public source control repository.</span></span>

<span data-ttu-id="b251f-161">Ustawienia aplikacji są przydatne także w przypadku, gdy konfiguracja toochange opartych na środowisku hello.</span><span class="sxs-lookup"><span data-stu-id="b251f-161">App settings are also useful whenever you want toochange configuration based on hello environment.</span></span> <span data-ttu-id="b251f-162">Na przykład w środowisku testowym można toomonitor innego kontenera magazynu kolejek i obiektów blob.</span><span class="sxs-lookup"><span data-stu-id="b251f-162">For example, in a test environment, you may want toomonitor a different queue or blob storage container.</span></span>

<span data-ttu-id="b251f-163">Ustawienia aplikacji zostaną rozwiązane w każdym przypadku, gdy wartość jest ujęta w znaki procentu, takich jak `%MyAppSetting%`.</span><span class="sxs-lookup"><span data-stu-id="b251f-163">App settings are resolved whenever a value is enclosed in percent signs, such as `%MyAppSetting%`.</span></span> <span data-ttu-id="b251f-164">Należy pamiętać, że hello `connection` wyzwalaczy i powiązań jest szczególnych przypadkach i automatycznie rozpoznaje wartości jako ustawienia aplikacji.</span><span class="sxs-lookup"><span data-stu-id="b251f-164">Note that hello `connection` property of triggers and bindings is a special case and automatically resolves values as app settings.</span></span> 

<span data-ttu-id="b251f-165">Witaj poniższym przykładzie jest wyzwalacz kolejki, który używa ustawienia aplikacji `%input-queue-name%` toodefine hello kolejki tootrigger na.</span><span class="sxs-lookup"><span data-stu-id="b251f-165">hello following example is a queue trigger that uses an app setting `%input-queue-name%` toodefine hello queue tootrigger on.</span></span>

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

## <a name="trigger-metadata-properties"></a><span data-ttu-id="b251f-166">Właściwości metadanych wyzwalacza</span><span class="sxs-lookup"><span data-stu-id="b251f-166">Trigger metadata properties</span></span>

<span data-ttu-id="b251f-167">W ładunku danych toohello dodanie udostępniane przez wyzwalacz (na przykład hello kolejki wiadomości, który wywołał funkcję) wiele wyzwalaczy, podaj wartości dodatkowe metadane.</span><span class="sxs-lookup"><span data-stu-id="b251f-167">In addition toohello data payload provided by a trigger (such as hello queue message that triggered a function), many triggers provide additional metadata values.</span></span> <span data-ttu-id="b251f-168">Te wartości może służyć jako parametry wejściowe w C# i F # lub we właściwościach hello `context.bindings` obiektu w języku JavaScript.</span><span class="sxs-lookup"><span data-stu-id="b251f-168">These values can be used as input parameters in C# and F# or properties on hello `context.bindings` object in JavaScript.</span></span> 

<span data-ttu-id="b251f-169">Na przykład wyzwalacz kolejki obsługuje hello następujące właściwości:</span><span class="sxs-lookup"><span data-stu-id="b251f-169">For example, a queue trigger supports hello following properties:</span></span>

* <span data-ttu-id="b251f-170">QueueTrigger - wyzwalania zawartość komunikatu, jeśli prawidłowy ciąg</span><span class="sxs-lookup"><span data-stu-id="b251f-170">QueueTrigger - triggering message content if a valid string</span></span>
* <span data-ttu-id="b251f-171">DequeueCount</span><span class="sxs-lookup"><span data-stu-id="b251f-171">DequeueCount</span></span>
* <span data-ttu-id="b251f-172">expirationTime</span><span class="sxs-lookup"><span data-stu-id="b251f-172">ExpirationTime</span></span>
* <span data-ttu-id="b251f-173">Identyfikator</span><span class="sxs-lookup"><span data-stu-id="b251f-173">Id</span></span>
* <span data-ttu-id="b251f-174">InsertionTime</span><span class="sxs-lookup"><span data-stu-id="b251f-174">InsertionTime</span></span>
* <span data-ttu-id="b251f-175">NextVisibleTime</span><span class="sxs-lookup"><span data-stu-id="b251f-175">NextVisibleTime</span></span>
* <span data-ttu-id="b251f-176">Elementu PopReceipt</span><span class="sxs-lookup"><span data-stu-id="b251f-176">PopReceipt</span></span>

<span data-ttu-id="b251f-177">Szczegółowe informacje o właściwości metadanych dla każdego wyzwalacza są opisane w hello odpowiedni temat odwołania.</span><span class="sxs-lookup"><span data-stu-id="b251f-177">Details of metadata properties for each trigger are described in hello corresponding reference topic.</span></span> <span data-ttu-id="b251f-178">Dokumentacja jest również dostępna w hello **integracji** kartę hello portal hello **dokumentacji** sekcji poniżej obszar konfiguracji powiązania hello.</span><span class="sxs-lookup"><span data-stu-id="b251f-178">Documentation is also available in hello **Integrate** tab of hello portal, in hello **Documentation** section below hello binding configuration area.</span></span>  

<span data-ttu-id="b251f-179">Na przykład, ponieważ wyzwalacze obiektu blob mają pewne opóźnienia, funkcja toorun wyzwalacza kolejki użytkownika (zobacz [wyzwalacza magazynu obiektów Blob](functions-bindings-storage-blob.md#storage-blob-trigger).</span><span class="sxs-lookup"><span data-stu-id="b251f-179">For example, since blob triggers have some delays, you can use a queue trigger toorun your function (see [Blob Storage Trigger](functions-bindings-storage-blob.md#storage-blob-trigger).</span></span> <span data-ttu-id="b251f-180">wiadomości powitania kolejki może zawierać tootrigger filename obiektu blob hello na.</span><span class="sxs-lookup"><span data-stu-id="b251f-180">hello queue message would contain hello blob filename tootrigger on.</span></span> <span data-ttu-id="b251f-181">Przy użyciu hello `queueTrigger` właściwości metadanych to zachowanie można określić w konfiguracji, a nie w kodzie.</span><span class="sxs-lookup"><span data-stu-id="b251f-181">Using hello `queueTrigger` metadata property, you can specify this behavior all in your configuration, rather than your code.</span></span>

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

<span data-ttu-id="b251f-182">Właściwości metadanych od wyzwalacza można również w *powiązanie wyrażenie* dla powiązania innego, jako hello opisane w następującej sekcji.</span><span class="sxs-lookup"><span data-stu-id="b251f-182">Metadata properties from a trigger can also be used in a *binding expression* for another binding, as described in hello following section.</span></span>

## <a name="binding-expressions-and-patterns"></a><span data-ttu-id="b251f-183">Wyrażenia wiązania i wzorce</span><span class="sxs-lookup"><span data-stu-id="b251f-183">Binding expressions and patterns</span></span>

<span data-ttu-id="b251f-184">Jedną z najbardziej zaawansowanych funkcji wyzwalaczy i powiązań hello jest *wyrażenia powiązania*.</span><span class="sxs-lookup"><span data-stu-id="b251f-184">One of hello most powerful features of triggers and bindings is *binding expressions*.</span></span> <span data-ttu-id="b251f-185">W ramach wiązania, można zdefiniować wzorzec wyrażenia, które mogą być następnie używane w pozostałych powiązaniach lub kodu.</span><span class="sxs-lookup"><span data-stu-id="b251f-185">Within your binding, you can define pattern expressions which can then be used in other bindings or your code.</span></span> <span data-ttu-id="b251f-186">Można także metadanych wyzwalacza w wyrażenia, powiązania jako Pokaż w próbce hello hello powyższej sekcji.</span><span class="sxs-lookup"><span data-stu-id="b251f-186">Trigger metadata can also be used in binding expressions, as show in hello sample in hello preceding section.</span></span>

<span data-ttu-id="b251f-187">Na przykład, załóżmy, że ma tooresize obrazów w kontenera magazynu obiektów blob w szczególności, toohello podobne **zmiany rozmiaru obrazu** szablonu w hello **nową funkcję** strony.</span><span class="sxs-lookup"><span data-stu-id="b251f-187">For example, suppose you want tooresize images in particular blob storage container, similar toohello **Image Resizer** template in hello **New Function** page.</span></span> <span data-ttu-id="b251f-188">Przejdź za**nową funkcję** -> języka **C#** -> Scenariusz **przykłady** -> **ImageResizer CSharp**.</span><span class="sxs-lookup"><span data-stu-id="b251f-188">Go too**New Function** -> Language **C#** -> Scenario **Samples** -> **ImageResizer-CSharp**.</span></span> 

<span data-ttu-id="b251f-189">Oto hello *function.json* definicji:</span><span class="sxs-lookup"><span data-stu-id="b251f-189">Here is hello *function.json* definition:</span></span>

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

<span data-ttu-id="b251f-190">Zwróć uwagę, że hello `filename` parametr jest używany w zarówno definicję wyzwalacza hello obiektów blob, jak i obiektów blob hello powiązania wyjściowego.</span><span class="sxs-lookup"><span data-stu-id="b251f-190">Notice that hello `filename` parameter is used in both hello blob trigger definition as well as hello blob output binding.</span></span> <span data-ttu-id="b251f-191">Ten parametr może również w kodzie funkcji.</span><span class="sxs-lookup"><span data-stu-id="b251f-191">This parameter can also be used in function code.</span></span>

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


### <a name="random-guids"></a><span data-ttu-id="b251f-192">Losowe identyfikatory GUID</span><span class="sxs-lookup"><span data-stu-id="b251f-192">Random GUIDs</span></span>
<span data-ttu-id="b251f-193">Środowisko Azure Functions zapewnia składni wygody generowania identyfikatorów GUID w powiązania, za pośrednictwem hello `{rand-guid}` powiązanie wyrażenia.</span><span class="sxs-lookup"><span data-stu-id="b251f-193">Azure Functions provides a convenience syntax for generating GUIDs in your bindings, through hello `{rand-guid}` binding expression.</span></span> <span data-ttu-id="b251f-194">Witaj poniższym przykładzie użyto tego toogenerate nazwę unikatową obiektów blob:</span><span class="sxs-lookup"><span data-stu-id="b251f-194">hello following example uses this toogenerate a unique blob name:</span></span> 

```json
{
  "type": "blob",
  "name": "blobOutput",
  "direction": "out",
  "path": "my-output-container/{rand-guid}"
}
```

### <a name="current-time"></a><span data-ttu-id="b251f-195">Bieżący czas</span><span class="sxs-lookup"><span data-stu-id="b251f-195">Current time</span></span>

<span data-ttu-id="b251f-196">Można użyć wyrażenia powiązania hello `DateTime`, która rozwiązuje zbyt`DateTime.UtcNow`.</span><span class="sxs-lookup"><span data-stu-id="b251f-196">You can use hello binding expression `DateTime`, which resolves too`DateTime.UtcNow`.</span></span>

```json
{
  "type": "blob",
  "name": "blobOutput",
  "direction": "out",
  "path": "my-output-container/{DateTime}"
}
```

## <a name="bind-toocustom-input-properties-in-a-binding-expression"></a><span data-ttu-id="b251f-197">Powiąż właściwości wejściowe toocustom wyrażenia powiązania</span><span class="sxs-lookup"><span data-stu-id="b251f-197">Bind toocustom input properties in a binding expression</span></span>

<span data-ttu-id="b251f-198">Wyrażenia powiązania można także odwoływać właściwości, które są zdefiniowane w ładunku wyzwalacza hello, sama.</span><span class="sxs-lookup"><span data-stu-id="b251f-198">Binding expressions can also reference properties that are defined in hello trigger payload itself.</span></span> <span data-ttu-id="b251f-199">Na przykład można toodynamically pliku magazynu obiektów blob tooa powiązania z nazwą w elementu webhook.</span><span class="sxs-lookup"><span data-stu-id="b251f-199">For example, you may want toodynamically bind tooa blob storage file from a filename provided in a webhook.</span></span>

<span data-ttu-id="b251f-200">Na przykład Witaj po *function.json* używa właściwość o nazwie `BlobName` z ładunku wyzwalacza hello:</span><span class="sxs-lookup"><span data-stu-id="b251f-200">For example, hello following *function.json* uses a property called `BlobName` from hello trigger payload:</span></span>

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

<span data-ttu-id="b251f-201">tooaccomplish ten w języku C# i F #, należy zdefiniować POCO, definiujący hello pola, które będą deserializowane w ładunku wyzwalacza hello.</span><span class="sxs-lookup"><span data-stu-id="b251f-201">tooaccomplish this in C# and F#, you must define a POCO that defines hello fields that will be deserialized in hello trigger payload.</span></span>

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

<span data-ttu-id="b251f-202">W języku JavaScript deserializacji JSON jest wykonywana automatycznie i można używać właściwości hello bezpośrednio.</span><span class="sxs-lookup"><span data-stu-id="b251f-202">In JavaScript, JSON deserialization is automatically performed and you can use hello properties directly.</span></span>

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

## <a name="configuring-binding-data-at-runtime"></a><span data-ttu-id="b251f-203">Konfigurowanie powiązania danych w czasie wykonywania</span><span class="sxs-lookup"><span data-stu-id="b251f-203">Configuring binding data at runtime</span></span>

<span data-ttu-id="b251f-204">W języku C# i innych języków .NET, można użyć wzorca wiązania konieczne jako min. toohello deklaratywne powiązania w *function.json*.</span><span class="sxs-lookup"><span data-stu-id="b251f-204">In C# and other .NET languages, you can use an imperative binding pattern, as opposed toohello declarative bindings in *function.json*.</span></span> <span data-ttu-id="b251f-205">Powiązanie konieczne jest przydatne, gdy Parametry wiążące muszą toobe obliczane w czasie środowiska uruchomieniowego zamiast projektu.</span><span class="sxs-lookup"><span data-stu-id="b251f-205">Imperative binding is useful when binding parameters need toobe computed at runtime rather than design time.</span></span> <span data-ttu-id="b251f-206">toolearn więcej, zobacz [powiązania w czasie wykonywania za pośrednictwem powiązania imperatywnych](functions-reference-csharp.md#imperative-bindings) w dokumentacja dla deweloperów hello C#.</span><span class="sxs-lookup"><span data-stu-id="b251f-206">toolearn more, see [Binding at runtime via imperative bindings](functions-reference-csharp.md#imperative-bindings) in hello C# developer reference.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b251f-207">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="b251f-207">Next steps</span></span>
<span data-ttu-id="b251f-208">Aby uzyskać więcej informacji na określone powiązanie Zobacz hello następujące artykuły:</span><span class="sxs-lookup"><span data-stu-id="b251f-208">For more information on a specific binding, see hello following articles:</span></span>

- [<span data-ttu-id="b251f-209">HTTP i elementy webhook</span><span class="sxs-lookup"><span data-stu-id="b251f-209">HTTP and webhooks</span></span>](functions-bindings-http-webhook.md)
- [<span data-ttu-id="b251f-210">Czasomierz</span><span class="sxs-lookup"><span data-stu-id="b251f-210">Timer</span></span>](functions-bindings-timer.md)
- [<span data-ttu-id="b251f-211">Queue Storage</span><span class="sxs-lookup"><span data-stu-id="b251f-211">Queue storage</span></span>](functions-bindings-storage-queue.md)
- [<span data-ttu-id="b251f-212">Blob Storage</span><span class="sxs-lookup"><span data-stu-id="b251f-212">Blob storage</span></span>](functions-bindings-storage-blob.md)
- [<span data-ttu-id="b251f-213">Table Storage</span><span class="sxs-lookup"><span data-stu-id="b251f-213">Table storage</span></span>](functions-bindings-storage-table.md)
- [<span data-ttu-id="b251f-214">Centrum zdarzeń</span><span class="sxs-lookup"><span data-stu-id="b251f-214">Event Hub</span></span>](functions-bindings-event-hubs.md)
- [<span data-ttu-id="b251f-215">Service Bus</span><span class="sxs-lookup"><span data-stu-id="b251f-215">Service Bus</span></span>](functions-bindings-service-bus.md)
- [<span data-ttu-id="b251f-216">Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="b251f-216">Cosmos DB</span></span>](functions-bindings-documentdb.md)
- [<span data-ttu-id="b251f-217">SendGrid</span><span class="sxs-lookup"><span data-stu-id="b251f-217">SendGrid</span></span>](functions-bindings-sendgrid.md)
- [<span data-ttu-id="b251f-218">Twilio</span><span class="sxs-lookup"><span data-stu-id="b251f-218">Twilio</span></span>](functions-bindings-twilio.md)
- [<span data-ttu-id="b251f-219">Notification Hubs</span><span class="sxs-lookup"><span data-stu-id="b251f-219">Notification Hubs</span></span>](functions-bindings-notification-hubs.md)
- [<span data-ttu-id="b251f-220">Mobile Apps</span><span class="sxs-lookup"><span data-stu-id="b251f-220">Mobile Apps</span></span>](functions-bindings-mobile-apps.md)
- [<span data-ttu-id="b251f-221">Plik zewnętrzny</span><span class="sxs-lookup"><span data-stu-id="b251f-221">External file</span></span>](functions-bindings-external-file.md)
