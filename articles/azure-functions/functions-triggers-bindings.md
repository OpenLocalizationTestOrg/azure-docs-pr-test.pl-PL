---
title: "Praca z wyzwalaczy i powiązań w usługi Azure Functions | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak używać wyzwalaczy i powiązań w usługi Azure Functions nawiązać połączenia z wykonanie kodu zdarzenia w sieci i usług w chmurze."
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
ms.openlocfilehash: cc41debb2523df77be4db05817a4c7ac55604439
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="azure-functions-triggers-and-bindings-concepts"></a><span data-ttu-id="8fc62-104">Azure funkcje wyzwalaczy i powiązań pojęcia</span><span class="sxs-lookup"><span data-stu-id="8fc62-104">Azure Functions triggers and bindings concepts</span></span>
<span data-ttu-id="8fc62-105">Środowisko Azure Functions umożliwia pisanie kodu w odpowiedzi na zdarzenia w Azure i innych usług za pośrednictwem *wyzwalaczy* i *powiązania*.</span><span class="sxs-lookup"><span data-stu-id="8fc62-105">Azure Functions allows you to write code in response to events in Azure and other services, through *triggers* and *bindings*.</span></span> <span data-ttu-id="8fc62-106">Ten artykuł zawiera omówienie wyzwalaczy i powiązań dla wszystkich obsługiwanych języków programowania.</span><span class="sxs-lookup"><span data-stu-id="8fc62-106">This article is a conceptual overview of triggers and bindings for all supported programming languages.</span></span> <span data-ttu-id="8fc62-107">Funkcje, które są wspólne dla wszystkich powiązań są opisane poniżej.</span><span class="sxs-lookup"><span data-stu-id="8fc62-107">Features that are common to all bindings are described here.</span></span>

## <a name="overview"></a><span data-ttu-id="8fc62-108">Omówienie</span><span class="sxs-lookup"><span data-stu-id="8fc62-108">Overview</span></span>

<span data-ttu-id="8fc62-109">Wyzwalaczy i powiązań są deklaratywne Definiowanie sposób wywoływania funkcji i co działa z danych.</span><span class="sxs-lookup"><span data-stu-id="8fc62-109">Triggers and bindings are a declarative way to define how a function is invoked and what data it works with.</span></span> <span data-ttu-id="8fc62-110">A *wyzwalacza* definiuje sposób wywoływania funkcji.</span><span class="sxs-lookup"><span data-stu-id="8fc62-110">A *trigger* defines how a function is invoked.</span></span> <span data-ttu-id="8fc62-111">Funkcja musi mieć dokładnie jeden wyzwalacz.</span><span class="sxs-lookup"><span data-stu-id="8fc62-111">A function must have exactly one trigger.</span></span> <span data-ttu-id="8fc62-112">Wyzwalacze mieć skojarzone dane, co jest zazwyczaj ładunku, który wywołał funkcję.</span><span class="sxs-lookup"><span data-stu-id="8fc62-112">Triggers have associated data, which is usually the payload that triggered the function.</span></span> 

<span data-ttu-id="8fc62-113">Wejście i wyjście *powiązania* Podaj deklaratywne, aby nawiązać połączenie danych z poziomu kodu.</span><span class="sxs-lookup"><span data-stu-id="8fc62-113">Input and output *bindings* provide a declarative way to connect to data from within your code.</span></span> <span data-ttu-id="8fc62-114">Podobnie jak wyzwalaczy, należy określić parametry połączenia i inne właściwości konfiguracji funkcji.</span><span class="sxs-lookup"><span data-stu-id="8fc62-114">Similar to triggers, you specify connection strings and other properties in your function configuration.</span></span> <span data-ttu-id="8fc62-115">Powiązania są opcjonalne i mieć wielu danych wejściowych i wyjściowych powiązania funkcji.</span><span class="sxs-lookup"><span data-stu-id="8fc62-115">Bindings are optional and a function can have multiple input and output bindings.</span></span> 

<span data-ttu-id="8fc62-116">Przy użyciu wyzwalaczy i powiązań, napisać kod, który jest więcej ogólny i nie umieszczaj szczegóły usługi, z którego nastąpi interakcja.</span><span class="sxs-lookup"><span data-stu-id="8fc62-116">Using triggers and bindings, you can write code that is more generic and does not hardcode the details of the services with which it interacts.</span></span> <span data-ttu-id="8fc62-117">Dane pochodzące z usługi po prostu stają się wartości wejściowe dla kodu funkcji.</span><span class="sxs-lookup"><span data-stu-id="8fc62-117">Data coming from services simply become input values for your function code.</span></span> <span data-ttu-id="8fc62-118">Do wysyłania danych do innej usługi (np. utworzenie nowego wiersza w magazynie tabel platformy Azure), użyj wartości zwracanej metody.</span><span class="sxs-lookup"><span data-stu-id="8fc62-118">To output data to another service (such as creating a new row in Azure Table Storage), use the return value of the method.</span></span> <span data-ttu-id="8fc62-119">Lub, jeśli zajdzie potrzeba output wiele wartości, użyj obiektu pomocnika.</span><span class="sxs-lookup"><span data-stu-id="8fc62-119">Or, if you need to output multiple values, use a helper object.</span></span> <span data-ttu-id="8fc62-120">Mieć wyzwalaczy i powiązań **nazwa** właściwość, która jest identyfikatorem w kodzie uzyskiwania dostępu za pomocą powiązania.</span><span class="sxs-lookup"><span data-stu-id="8fc62-120">Triggers and bindings have a **name** property, which is an identifier you use in your code to access the binding.</span></span>

<span data-ttu-id="8fc62-121">Można skonfigurować wyzwalaczy i powiązań w **integracji** kartę w portalu Azure Functions.</span><span class="sxs-lookup"><span data-stu-id="8fc62-121">You can configure triggers and bindings in the **Integrate** tab in the Azure Functions portal.</span></span> <span data-ttu-id="8fc62-122">W obszarze obejmuje, interfejs użytkownika modyfikuje plik o nazwie *function.json* pliku w katalogu funkcji.</span><span class="sxs-lookup"><span data-stu-id="8fc62-122">Under the covers, the UI modifies a file called *function.json* file in the function directory.</span></span> <span data-ttu-id="8fc62-123">Ten plik można edytować, zmieniając **Zaawansowany edytor**.</span><span class="sxs-lookup"><span data-stu-id="8fc62-123">You can edit this file by changing to the **Advanced editor**.</span></span>

<span data-ttu-id="8fc62-124">W poniższej tabeli przedstawiono wyzwalaczy i powiązań, które są obsługiwane w środowisku Azure Functions.</span><span class="sxs-lookup"><span data-stu-id="8fc62-124">The following table shows the triggers and bindings that are supported with Azure Functions.</span></span> 

[!INCLUDE [Full bindings table](../../includes/functions-bindings.md)]

### <a name="example-queue-trigger-and-table-output-binding"></a><span data-ttu-id="8fc62-125">Przykład: wyzwalacz kolejki i tabeli powiązania wyjściowego</span><span class="sxs-lookup"><span data-stu-id="8fc62-125">Example: queue trigger and table output binding</span></span>

<span data-ttu-id="8fc62-126">Załóżmy, że chcesz zapisać nowy wiersz do magazynu tabel Azure przy każdym wyświetleniu nowego komunikatu w magazynie kolejek Azure.</span><span class="sxs-lookup"><span data-stu-id="8fc62-126">Suppose you want to write a new row to Azure Table Storage whenever a new message appears in Azure Queue Storage.</span></span> <span data-ttu-id="8fc62-127">W tym scenariuszu można implementować przy użyciu kolejek platformy Azure i wyzwalaczy tabeli powiązania wyjściowego.</span><span class="sxs-lookup"><span data-stu-id="8fc62-127">This scenario can be implemented using an Azure Queue trigger and a Table output binding.</span></span> 

<span data-ttu-id="8fc62-128">Wyzwalacz kolejki wymaga następujących informacji w **integracji** karty:</span><span class="sxs-lookup"><span data-stu-id="8fc62-128">A queue trigger requires the following information in the **Integrate** tab:</span></span>

* <span data-ttu-id="8fc62-129">Nazwa ustawienia aplikacji, która zawiera parametry połączenia konta magazynu dla kolejki</span><span class="sxs-lookup"><span data-stu-id="8fc62-129">The name of the app setting that contains the storage account connection string for the queue</span></span>
* <span data-ttu-id="8fc62-130">Nazwa kolejki</span><span class="sxs-lookup"><span data-stu-id="8fc62-130">The queue name</span></span>
* <span data-ttu-id="8fc62-131">Identyfikator w kodzie do odczytu treści wiadomości kolejki, takich jak `order`.</span><span class="sxs-lookup"><span data-stu-id="8fc62-131">The identifier in your code to read the contents of the queue message, such as `order`.</span></span>

<span data-ttu-id="8fc62-132">Można zapisać do magazynu tabel Azure, użyj powiązania danych wyjściowych z następującymi szczegółami:</span><span class="sxs-lookup"><span data-stu-id="8fc62-132">To write to Azure Table Storage, use an output binding with the following details:</span></span>

* <span data-ttu-id="8fc62-133">Nazwa ustawienia aplikacji, który zawiera parametry połączenia konta magazynu dla tabeli</span><span class="sxs-lookup"><span data-stu-id="8fc62-133">The name of the app setting that contains the storage account connection string for the table</span></span>
* <span data-ttu-id="8fc62-134">Nazwa tabeli</span><span class="sxs-lookup"><span data-stu-id="8fc62-134">The table name</span></span>
* <span data-ttu-id="8fc62-135">Identyfikator kod w celu utworzenia elementów wyjściowych lub wartości zwracanej z funkcji.</span><span class="sxs-lookup"><span data-stu-id="8fc62-135">The identifier in your code to create output items, or the return value from the function.</span></span>

<span data-ttu-id="8fc62-136">Powiązania Użyj ustawień aplikacji parametry połączenia do wymuszania najlepszych rozwiązań, które *function.json* nie zawiera kluczy tajnych usługi.</span><span class="sxs-lookup"><span data-stu-id="8fc62-136">Bindings use app settings for connection strings to enforce the best practice that *function.json* does not contain service secrets.</span></span>

<span data-ttu-id="8fc62-137">Następnie należy użyć identyfikatorów, które są dostarczane do integracji z usługą Azure Storage w kodzie.</span><span class="sxs-lookup"><span data-stu-id="8fc62-137">Then, use the identifiers you provided to integrate with Azure Storage in your code.</span></span>

```cs
#r "Newtonsoft.Json"

using Newtonsoft.Json.Linq;

// From an incoming queue message that is a JSON object, add fields and write to Table Storage
// The method return value creates a new row in Table Storage
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
// From an incoming queue message that is a JSON object, add fields and write to Table Storage
// The second parameter to context.done is used as the value for the new row
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

<span data-ttu-id="8fc62-138">Oto *function.json* odpowiadający poprzedni kod.</span><span class="sxs-lookup"><span data-stu-id="8fc62-138">Here is the *function.json* that corresponds to the preceding code.</span></span> <span data-ttu-id="8fc62-139">Należy pamiętać, że tej samej konfiguracji mogą być używane, niezależnie od języka implementację funkcji.</span><span class="sxs-lookup"><span data-stu-id="8fc62-139">Note that the same configuration can be used, regardless of the language of the function implementation.</span></span>

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
<span data-ttu-id="8fc62-140">Aby wyświetlić i edytować zawartość *function.json* w portalu Azure kliknij **Zaawansowany edytor** opcja **integracji** kartę funkcji.</span><span class="sxs-lookup"><span data-stu-id="8fc62-140">To view and edit the contents of *function.json* in the Azure portal, click the **Advanced editor** option on the **Integrate** tab of your function.</span></span>

<span data-ttu-id="8fc62-141">Aby uzyskać więcej przykładów kodu i szczegółowe informacje o integracji z usługą Azure Storage, zobacz [usługi Azure Functions wyzwalaczy i powiązań usługi Azure Storage](functions-bindings-storage.md).</span><span class="sxs-lookup"><span data-stu-id="8fc62-141">For more code examples and details on integrating with Azure Storage, see [Azure Functions triggers and bindings for Azure Storage](functions-bindings-storage.md).</span></span>

### <a name="binding-direction"></a><span data-ttu-id="8fc62-142">Kierunek powiązania</span><span class="sxs-lookup"><span data-stu-id="8fc62-142">Binding direction</span></span>

<span data-ttu-id="8fc62-143">Wszystkich wyzwalaczy i powiązań ma `direction` właściwości:</span><span class="sxs-lookup"><span data-stu-id="8fc62-143">All triggers and bindings have a `direction` property:</span></span>

- <span data-ttu-id="8fc62-144">Wyzwalacze kierunek jest zawsze`in`</span><span class="sxs-lookup"><span data-stu-id="8fc62-144">For triggers, the direction is always `in`</span></span>
- <span data-ttu-id="8fc62-145">Użyj powiązań wejściowych i wyjściowych `in` i`out`</span><span class="sxs-lookup"><span data-stu-id="8fc62-145">Input and output bindings use `in` and `out`</span></span>
- <span data-ttu-id="8fc62-146">Niektóre powiązania obsługuje specjalne kierunku `inout`.</span><span class="sxs-lookup"><span data-stu-id="8fc62-146">Some bindings support a special direction `inout`.</span></span> <span data-ttu-id="8fc62-147">Jeśli używasz `inout`, tylko **Zaawansowany edytor** jest dostępna w **integracji** kartę.</span><span class="sxs-lookup"><span data-stu-id="8fc62-147">If you use `inout`, only the **Advanced editor** is available in the **Integrate** tab.</span></span>

## <a name="using-the-function-return-type-to-return-a-single-output"></a><span data-ttu-id="8fc62-148">Zwraca jeden z za pomocą zwracanego typu funkcji</span><span class="sxs-lookup"><span data-stu-id="8fc62-148">Using the function return type to return a single output</span></span>

<span data-ttu-id="8fc62-149">Poprzedni przykład przedstawia sposób użycia funkcji zwracana wartość zapewnienie dane wyjściowe do powiązania, które jest realizowane za pośrednictwem parametru specjalną nazwą `$return`.</span><span class="sxs-lookup"><span data-stu-id="8fc62-149">The preceding example shows how to use the function return value to provide output to a binding, which is achieved by using the special name parameter `$return`.</span></span> <span data-ttu-id="8fc62-150">(To jest tylko obsługiwana w językach, które mają wartość zwracaną, takich jak C#, JavaScript i F #.) Jeśli funkcja ma wiele powiązań danych wyjściowych, użyj `$return` tylko jednego powiązania danych wyjściowych.</span><span class="sxs-lookup"><span data-stu-id="8fc62-150">(This is only supported in languages that have a return value, such as C#, JavaScript, and F#.) If a function has multiple output bindings, use `$return` for only one of the output bindings.</span></span> 

```json
// excerpt of function.json
{
    "name": "$return",
    "type": "blob",
    "direction": "out",
    "path": "output-container/{id}"
}
```

<span data-ttu-id="8fc62-151">Przykłady poniżej Pokaż jak przywrócić typy są używane z powiązaniami danych wyjściowych w języku C#, JavaScript i F #.</span><span class="sxs-lookup"><span data-stu-id="8fc62-151">The examples below show how return types are used with output bindings in C#, JavaScript, and F#.</span></span>

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
// JavaScript: return a value in the second parameter to context.done
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

## <a name="binding-datatype-property"></a><span data-ttu-id="8fc62-152">Właściwość dataType powiązania</span><span class="sxs-lookup"><span data-stu-id="8fc62-152">Binding dataType property</span></span>

<span data-ttu-id="8fc62-153">W środowisku .NET należy użyć typów do definiowania typu danych dla danych wejściowych.</span><span class="sxs-lookup"><span data-stu-id="8fc62-153">In .NET, use the types to define the data type for input data.</span></span> <span data-ttu-id="8fc62-154">Na przykład użyć `string` powiązać tekst wyzwalacz kolejki i Tablica bajtów do odczytu jako wartość binarną.</span><span class="sxs-lookup"><span data-stu-id="8fc62-154">For instance, use `string` to bind to the text of a queue trigger and a byte array to read as binary.</span></span>

<span data-ttu-id="8fc62-155">Dla języków, które są dynamicznie wpisane takich jak JavaScript, użyj `dataType` właściwości w definicji powiązania.</span><span class="sxs-lookup"><span data-stu-id="8fc62-155">For languages that are dynamically typed such as JavaScript, use the `dataType` property in the binding definition.</span></span> <span data-ttu-id="8fc62-156">Na przykład można odczytać treści żądania HTTP w formacie binarnym, użyj typu `binary`:</span><span class="sxs-lookup"><span data-stu-id="8fc62-156">For example, to read the content of an HTTP request in binary format, use the type `binary`:</span></span>

```json
{
    "type": "httpTrigger",
    "name": "req",
    "direction": "in",
    "dataType": "binary"
}
```

<span data-ttu-id="8fc62-157">Inne opcje `dataType` są `stream` i `string`.</span><span class="sxs-lookup"><span data-stu-id="8fc62-157">Other options for `dataType` are `stream` and `string`.</span></span>

## <a name="resolving-app-settings"></a><span data-ttu-id="8fc62-158">Rozpoznawanie ustawień aplikacji</span><span class="sxs-lookup"><span data-stu-id="8fc62-158">Resolving app settings</span></span>
<span data-ttu-id="8fc62-159">Najlepszym rozwiązaniem kluczy tajnych i parametry połączenia mają być zarządzane przy użyciu ustawienia aplikacji, a nie plików konfiguracyjnych.</span><span class="sxs-lookup"><span data-stu-id="8fc62-159">As a best practice, secrets and connection strings should be managed using app settings, rather than configuration files.</span></span> <span data-ttu-id="8fc62-160">To ogranicza dostęp do tych kluczy tajnych i pozwala bezpiecznie przechowywać *function.json* w repozytorium kontroli źródła publicznego.</span><span class="sxs-lookup"><span data-stu-id="8fc62-160">This limits access to these secrets and makes it safe to store *function.json* in a public source control repository.</span></span>

<span data-ttu-id="8fc62-161">Ustawienia aplikacji są przydatne także w przypadku, gdy chcesz zmienić konfigurację na podstawie środowiska.</span><span class="sxs-lookup"><span data-stu-id="8fc62-161">App settings are also useful whenever you want to change configuration based on the environment.</span></span> <span data-ttu-id="8fc62-162">Na przykład w środowisku testowym można monitorować różne kontenera magazynu kolejek i obiektów blob.</span><span class="sxs-lookup"><span data-stu-id="8fc62-162">For example, in a test environment, you may want to monitor a different queue or blob storage container.</span></span>

<span data-ttu-id="8fc62-163">Ustawienia aplikacji zostaną rozwiązane w każdym przypadku, gdy wartość jest ujęta w znaki procentu, takich jak `%MyAppSetting%`.</span><span class="sxs-lookup"><span data-stu-id="8fc62-163">App settings are resolved whenever a value is enclosed in percent signs, such as `%MyAppSetting%`.</span></span> <span data-ttu-id="8fc62-164">Należy pamiętać, że `connection` wyzwalaczy i powiązań jest szczególnych przypadkach i automatycznie rozpoznaje wartości jako ustawienia aplikacji.</span><span class="sxs-lookup"><span data-stu-id="8fc62-164">Note that the `connection` property of triggers and bindings is a special case and automatically resolves values as app settings.</span></span> 

<span data-ttu-id="8fc62-165">Poniższy przykład jest wyzwalacz kolejki, który używa ustawienia aplikacji `%input-queue-name%` do definiowania wyzwalane w kolejce.</span><span class="sxs-lookup"><span data-stu-id="8fc62-165">The following example is a queue trigger that uses an app setting `%input-queue-name%` to define the queue to trigger on.</span></span>

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

## <a name="trigger-metadata-properties"></a><span data-ttu-id="8fc62-166">Właściwości metadanych wyzwalacza</span><span class="sxs-lookup"><span data-stu-id="8fc62-166">Trigger metadata properties</span></span>

<span data-ttu-id="8fc62-167">Oprócz ładunku danych dostarczonych przez wyzwalacz (na przykład kolejki komunikatów, który wywołał funkcję) wiele wyzwalaczy, podaj wartości dodatkowe metadane.</span><span class="sxs-lookup"><span data-stu-id="8fc62-167">In addition to the data payload provided by a trigger (such as the queue message that triggered a function), many triggers provide additional metadata values.</span></span> <span data-ttu-id="8fc62-168">Te wartości może służyć jako parametry wejściowe w języku C# i F # lub właściwości na `context.bindings` obiektu w języku JavaScript.</span><span class="sxs-lookup"><span data-stu-id="8fc62-168">These values can be used as input parameters in C# and F# or properties on the `context.bindings` object in JavaScript.</span></span> 

<span data-ttu-id="8fc62-169">Na przykład wyzwalacz kolejki obsługuje następujące właściwości:</span><span class="sxs-lookup"><span data-stu-id="8fc62-169">For example, a queue trigger supports the following properties:</span></span>

* <span data-ttu-id="8fc62-170">QueueTrigger - wyzwalania zawartość komunikatu, jeśli prawidłowy ciąg</span><span class="sxs-lookup"><span data-stu-id="8fc62-170">QueueTrigger - triggering message content if a valid string</span></span>
* <span data-ttu-id="8fc62-171">DequeueCount</span><span class="sxs-lookup"><span data-stu-id="8fc62-171">DequeueCount</span></span>
* <span data-ttu-id="8fc62-172">expirationTime</span><span class="sxs-lookup"><span data-stu-id="8fc62-172">ExpirationTime</span></span>
* <span data-ttu-id="8fc62-173">Identyfikator</span><span class="sxs-lookup"><span data-stu-id="8fc62-173">Id</span></span>
* <span data-ttu-id="8fc62-174">InsertionTime</span><span class="sxs-lookup"><span data-stu-id="8fc62-174">InsertionTime</span></span>
* <span data-ttu-id="8fc62-175">NextVisibleTime</span><span class="sxs-lookup"><span data-stu-id="8fc62-175">NextVisibleTime</span></span>
* <span data-ttu-id="8fc62-176">Elementu PopReceipt</span><span class="sxs-lookup"><span data-stu-id="8fc62-176">PopReceipt</span></span>

<span data-ttu-id="8fc62-177">Szczegółowe informacje o właściwości metadanych dla każdego wyzwalacza są opisane w odpowiedni temat odwołania.</span><span class="sxs-lookup"><span data-stu-id="8fc62-177">Details of metadata properties for each trigger are described in the corresponding reference topic.</span></span> <span data-ttu-id="8fc62-178">Dokumentacja jest również dostępna w **integracji** kartę portalu w **dokumentacji** sekcji poniżej obszar konfiguracji powiązania.</span><span class="sxs-lookup"><span data-stu-id="8fc62-178">Documentation is also available in the **Integrate** tab of the portal, in the **Documentation** section below the binding configuration area.</span></span>  

<span data-ttu-id="8fc62-179">Na przykład, ponieważ wyzwalacze obiektu blob mają pewne opóźnienia, umożliwia wyzwalacz kolejki uruchomienia funkcji (zobacz [wyzwalacza magazynu obiektów Blob](functions-bindings-storage-blob.md#storage-blob-trigger).</span><span class="sxs-lookup"><span data-stu-id="8fc62-179">For example, since blob triggers have some delays, you can use a queue trigger to run your function (see [Blob Storage Trigger](functions-bindings-storage-blob.md#storage-blob-trigger).</span></span> <span data-ttu-id="8fc62-180">Komunikat z kolejki może zawierać filename obiektu blob do wyzwolenia na.</span><span class="sxs-lookup"><span data-stu-id="8fc62-180">The queue message would contain the blob filename to trigger on.</span></span> <span data-ttu-id="8fc62-181">Przy użyciu `queueTrigger` właściwości metadanych to zachowanie można określić w konfiguracji, a nie w kodzie.</span><span class="sxs-lookup"><span data-stu-id="8fc62-181">Using the `queueTrigger` metadata property, you can specify this behavior all in your configuration, rather than your code.</span></span>

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

<span data-ttu-id="8fc62-182">Właściwości metadanych od wyzwalacza można również w *powiązanie wyrażenie* dla innego powiązania, zgodnie z opisem w poniższej sekcji.</span><span class="sxs-lookup"><span data-stu-id="8fc62-182">Metadata properties from a trigger can also be used in a *binding expression* for another binding, as described in the following section.</span></span>

## <a name="binding-expressions-and-patterns"></a><span data-ttu-id="8fc62-183">Wyrażenia wiązania i wzorce</span><span class="sxs-lookup"><span data-stu-id="8fc62-183">Binding expressions and patterns</span></span>

<span data-ttu-id="8fc62-184">Jedną z najbardziej zaawansowanych funkcji, wyzwalaczy i powiązań jest *wyrażenia powiązania*.</span><span class="sxs-lookup"><span data-stu-id="8fc62-184">One of the most powerful features of triggers and bindings is *binding expressions*.</span></span> <span data-ttu-id="8fc62-185">W ramach wiązania, można zdefiniować wzorzec wyrażenia, które mogą być następnie używane w pozostałych powiązaniach lub kodu.</span><span class="sxs-lookup"><span data-stu-id="8fc62-185">Within your binding, you can define pattern expressions which can then be used in other bindings or your code.</span></span> <span data-ttu-id="8fc62-186">Można także metadanych wyzwalacza w wyrażenia, powiązania jako Pokaż w próbce w poprzedniej sekcji.</span><span class="sxs-lookup"><span data-stu-id="8fc62-186">Trigger metadata can also be used in binding expressions, as show in the sample in the preceding section.</span></span>

<span data-ttu-id="8fc62-187">Załóżmy na przykład, aby zmienić rozmiar obrazów w kontenera magazynu obiektów blob w określonym, podobnie jak **zmiany rozmiaru obrazu** szablonu w **nową funkcję** strony.</span><span class="sxs-lookup"><span data-stu-id="8fc62-187">For example, suppose you want to resize images in particular blob storage container, similar to the **Image Resizer** template in the **New Function** page.</span></span> <span data-ttu-id="8fc62-188">Przejdź do **nową funkcję** -> języka **C#** -> Scenariusz **przykłady** -> **ImageResizer CSharp**.</span><span class="sxs-lookup"><span data-stu-id="8fc62-188">Go to **New Function** -> Language **C#** -> Scenario **Samples** -> **ImageResizer-CSharp**.</span></span> 

<span data-ttu-id="8fc62-189">Oto *function.json* definicji:</span><span class="sxs-lookup"><span data-stu-id="8fc62-189">Here is the *function.json* definition:</span></span>

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

<span data-ttu-id="8fc62-190">Zwróć uwagę, że `filename` parametr jest używany zarówno definicję wyzwalacza obiektu blob, jak również obiektu blob powiązania wyjściowego.</span><span class="sxs-lookup"><span data-stu-id="8fc62-190">Notice that the `filename` parameter is used in both the blob trigger definition as well as the blob output binding.</span></span> <span data-ttu-id="8fc62-191">Ten parametr może również w kodzie funkcji.</span><span class="sxs-lookup"><span data-stu-id="8fc62-191">This parameter can also be used in function code.</span></span>

```csharp
// C# example of binding to {filename}
public static void Run(Stream image, string filename, Stream imageSmall, TraceWriter log)  
{
    log.Info($"Blob trigger processing: {filename}");
    // ...
} 
```

<!--TODO: add JavaScript example -->
<!-- Blocked by bug https://github.com/Azure/Azure-Functions/issues/248 -->


### <a name="random-guids"></a><span data-ttu-id="8fc62-192">Losowe identyfikatory GUID</span><span class="sxs-lookup"><span data-stu-id="8fc62-192">Random GUIDs</span></span>
<span data-ttu-id="8fc62-193">Środowisko Azure Functions zapewnia składni wygody generowania identyfikatorów GUID w powiązania, za pośrednictwem `{rand-guid}` powiązanie wyrażenia.</span><span class="sxs-lookup"><span data-stu-id="8fc62-193">Azure Functions provides a convenience syntax for generating GUIDs in your bindings, through the `{rand-guid}` binding expression.</span></span> <span data-ttu-id="8fc62-194">W poniższym przykładzie użyto to nazwy obiektu blob unikatowy:</span><span class="sxs-lookup"><span data-stu-id="8fc62-194">The following example uses this to generate a unique blob name:</span></span> 

```json
{
  "type": "blob",
  "name": "blobOutput",
  "direction": "out",
  "path": "my-output-container/{rand-guid}"
}
```

### <a name="current-time"></a><span data-ttu-id="8fc62-195">Bieżący czas</span><span class="sxs-lookup"><span data-stu-id="8fc62-195">Current time</span></span>

<span data-ttu-id="8fc62-196">Można użyć wyrażenia powiązania `DateTime`, który jest rozpoznawany jako `DateTime.UtcNow`.</span><span class="sxs-lookup"><span data-stu-id="8fc62-196">You can use the binding expression `DateTime`, which resolves to `DateTime.UtcNow`.</span></span>

```json
{
  "type": "blob",
  "name": "blobOutput",
  "direction": "out",
  "path": "my-output-container/{DateTime}"
}
```

## <a name="bind-to-custom-input-properties-in-a-binding-expression"></a><span data-ttu-id="8fc62-197">Powiązania niestandardowe właściwości wejściowych w wyrażeniu powiązania</span><span class="sxs-lookup"><span data-stu-id="8fc62-197">Bind to custom input properties in a binding expression</span></span>

<span data-ttu-id="8fc62-198">Wyrażenia powiązania można także odwoływać właściwości, które są zdefiniowane w ładunku wyzwalacza samej siebie.</span><span class="sxs-lookup"><span data-stu-id="8fc62-198">Binding expressions can also reference properties that are defined in the trigger payload itself.</span></span> <span data-ttu-id="8fc62-199">Na przykład można dynamicznie powiązania do pliku magazynu obiektów blob z nazwą w elementu webhook.</span><span class="sxs-lookup"><span data-stu-id="8fc62-199">For example, you may want to dynamically bind to a blob storage file from a filename provided in a webhook.</span></span>

<span data-ttu-id="8fc62-200">Na przykład następująca *function.json* używa właściwość o nazwie `BlobName` z ładunku wyzwalacz:</span><span class="sxs-lookup"><span data-stu-id="8fc62-200">For example, the following *function.json* uses a property called `BlobName` from the trigger payload:</span></span>

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

<span data-ttu-id="8fc62-201">W tym celu w języku C# i F #, należy zdefiniować POCO, definiujący pola, które będą deserializowane w ładunku wyzwalacza.</span><span class="sxs-lookup"><span data-stu-id="8fc62-201">To accomplish this in C# and F#, you must define a POCO that defines the fields that will be deserialized in the trigger payload.</span></span>

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

<span data-ttu-id="8fc62-202">W języku JavaScript deserializacji JSON jest wykonywana automatycznie i można użyć właściwości bezpośrednio.</span><span class="sxs-lookup"><span data-stu-id="8fc62-202">In JavaScript, JSON deserialization is automatically performed and you can use the properties directly.</span></span>

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

## <a name="configuring-binding-data-at-runtime"></a><span data-ttu-id="8fc62-203">Konfigurowanie powiązania danych w czasie wykonywania</span><span class="sxs-lookup"><span data-stu-id="8fc62-203">Configuring binding data at runtime</span></span>

<span data-ttu-id="8fc62-204">W języku C# i innych języków .NET, można użyć wzorca wiązania konieczne, w przeciwieństwie do deklaratywne powiązania w *function.json*.</span><span class="sxs-lookup"><span data-stu-id="8fc62-204">In C# and other .NET languages, you can use an imperative binding pattern, as opposed to the declarative bindings in *function.json*.</span></span> <span data-ttu-id="8fc62-205">Powiązanie konieczne jest przydatne, gdy Parametry wiążące muszą ma zostać obliczony w czasie środowiska uruchomieniowego zamiast projektu.</span><span class="sxs-lookup"><span data-stu-id="8fc62-205">Imperative binding is useful when binding parameters need to be computed at runtime rather than design time.</span></span> <span data-ttu-id="8fc62-206">Aby dowiedzieć się więcej, zobacz [powiązania w czasie wykonywania za pośrednictwem powiązania imperatywnych](functions-reference-csharp.md#imperative-bindings) w dokumentacja dla deweloperów języka C#.</span><span class="sxs-lookup"><span data-stu-id="8fc62-206">To learn more, see [Binding at runtime via imperative bindings](functions-reference-csharp.md#imperative-bindings) in the C# developer reference.</span></span>

## <a name="next-steps"></a><span data-ttu-id="8fc62-207">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="8fc62-207">Next steps</span></span>
<span data-ttu-id="8fc62-208">Aby uzyskać więcej informacji na określone powiązanie zobacz następujące artykuły:</span><span class="sxs-lookup"><span data-stu-id="8fc62-208">For more information on a specific binding, see the following articles:</span></span>

- [<span data-ttu-id="8fc62-209">HTTP i elementy webhook</span><span class="sxs-lookup"><span data-stu-id="8fc62-209">HTTP and webhooks</span></span>](functions-bindings-http-webhook.md)
- [<span data-ttu-id="8fc62-210">Czasomierz</span><span class="sxs-lookup"><span data-stu-id="8fc62-210">Timer</span></span>](functions-bindings-timer.md)
- [<span data-ttu-id="8fc62-211">Queue Storage</span><span class="sxs-lookup"><span data-stu-id="8fc62-211">Queue storage</span></span>](functions-bindings-storage-queue.md)
- [<span data-ttu-id="8fc62-212">Blob Storage</span><span class="sxs-lookup"><span data-stu-id="8fc62-212">Blob storage</span></span>](functions-bindings-storage-blob.md)
- [<span data-ttu-id="8fc62-213">Table Storage</span><span class="sxs-lookup"><span data-stu-id="8fc62-213">Table storage</span></span>](functions-bindings-storage-table.md)
- [<span data-ttu-id="8fc62-214">Centrum zdarzeń</span><span class="sxs-lookup"><span data-stu-id="8fc62-214">Event Hub</span></span>](functions-bindings-event-hubs.md)
- [<span data-ttu-id="8fc62-215">Service Bus</span><span class="sxs-lookup"><span data-stu-id="8fc62-215">Service Bus</span></span>](functions-bindings-service-bus.md)
- [<span data-ttu-id="8fc62-216">Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="8fc62-216">Cosmos DB</span></span>](functions-bindings-documentdb.md)
- [<span data-ttu-id="8fc62-217">SendGrid</span><span class="sxs-lookup"><span data-stu-id="8fc62-217">SendGrid</span></span>](functions-bindings-sendgrid.md)
- [<span data-ttu-id="8fc62-218">Twilio</span><span class="sxs-lookup"><span data-stu-id="8fc62-218">Twilio</span></span>](functions-bindings-twilio.md)
- [<span data-ttu-id="8fc62-219">Notification Hubs</span><span class="sxs-lookup"><span data-stu-id="8fc62-219">Notification Hubs</span></span>](functions-bindings-notification-hubs.md)
- [<span data-ttu-id="8fc62-220">Mobile Apps</span><span class="sxs-lookup"><span data-stu-id="8fc62-220">Mobile Apps</span></span>](functions-bindings-mobile-apps.md)
- [<span data-ttu-id="8fc62-221">Plik zewnętrzny</span><span class="sxs-lookup"><span data-stu-id="8fc62-221">External file</span></span>](functions-bindings-external-file.md)
