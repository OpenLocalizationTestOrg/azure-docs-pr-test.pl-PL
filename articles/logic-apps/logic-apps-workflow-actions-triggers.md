---
title: "Działania przepływu pracy i wyzwalaczy - Azure Logic Apps | Dokumentacja firmy Microsoft"
description: 
services: logic-apps
author: MandiOhlinger
manager: anneta
editor: 
documentationcenter: 
ms.assetid: 86a53bb3-01ba-4e83-89b7-c9a7074cb159
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: multiple
ms.topic: article
ms.date: 11/17/2016
ms.author: LADocs; mandia
ms.openlocfilehash: bd3f1d225b974ebde889738bb435825658d1e1e0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="workflow-actions-and-triggers-for-azure-logic-apps"></a><span data-ttu-id="48fb7-102">Działania przepływu pracy i Wyzwalacze dla usługi Azure Logic Apps</span><span class="sxs-lookup"><span data-stu-id="48fb7-102">Workflow actions and triggers for Azure Logic Apps</span></span>

<span data-ttu-id="48fb7-103">Aplikacje logiki składają się z wyzwalacze i akcje.</span><span class="sxs-lookup"><span data-stu-id="48fb7-103">Logic apps consist of triggers and actions.</span></span> <span data-ttu-id="48fb7-104">Istnieją typy sześciu wyzwalaczy.</span><span class="sxs-lookup"><span data-stu-id="48fb7-104">There are six types of triggers.</span></span> <span data-ttu-id="48fb7-105">Każdy typ ma inny interfejs i inaczej.</span><span class="sxs-lookup"><span data-stu-id="48fb7-105">Each type has different interface and different behavior.</span></span> <span data-ttu-id="48fb7-106">Możesz także dowiedzieć się inne szczegóły sprawdzając szczegóły [język definicji przepływu pracy](logic-apps-workflow-definition-language.md).</span><span class="sxs-lookup"><span data-stu-id="48fb7-106">You can also learn about other details by looking at the details of the [Workflow Definition Language](logic-apps-workflow-definition-language.md).</span></span>  
  
<span data-ttu-id="48fb7-107">W dalszej Dowiedz się więcej o wyzwalacze i akcje i jak można ich używać do tworzenia aplikacji logiki, aby ulepszyć Twoje procesów biznesowych i przepływów pracy.</span><span class="sxs-lookup"><span data-stu-id="48fb7-107">Read on to learn more about triggers and actions and how you might use them to build logic apps to improve your business processes and workflows.</span></span>  
  
### <a name="triggers"></a><span data-ttu-id="48fb7-108">Wyzwalacze</span><span class="sxs-lookup"><span data-stu-id="48fb7-108">Triggers</span></span>  

<span data-ttu-id="48fb7-109">Wyzwalacz określa wywołania, które mogą inicjować uruchomienia przepływu pracy aplikacji logiki.</span><span class="sxs-lookup"><span data-stu-id="48fb7-109">A trigger specifies the calls that can initiate a run of your logic app workflow.</span></span> <span data-ttu-id="48fb7-110">Poniżej przedstawiono dwa różne sposoby, aby zainicjować do uruchomienia przepływu pracy:</span><span class="sxs-lookup"><span data-stu-id="48fb7-110">Here are the two different ways to initiate a run of your workflow:</span></span>  
  
-   <span data-ttu-id="48fb7-111">Wyzwalacz sondowania</span><span class="sxs-lookup"><span data-stu-id="48fb7-111">A polling trigger</span></span>  

-   <span data-ttu-id="48fb7-112">Wyzwalacz wypychania - wywołując [interfejsu API REST usługi przepływu pracy](https://docs.microsoft.com/rest/api/logic/workflows)</span><span class="sxs-lookup"><span data-stu-id="48fb7-112">A push trigger - by calling the [Workflow Service REST API](https://docs.microsoft.com/rest/api/logic/workflows)</span></span>  
  
<span data-ttu-id="48fb7-113">Wszystkich wyzwalaczy zawierać tych elementów najwyższego poziomu:</span><span class="sxs-lookup"><span data-stu-id="48fb7-113">All triggers contain these top-level elements:</span></span>  
  
```json
"<name-of-the-trigger>" : {
    "type": "<type-of-trigger>",
    "inputs": { <settings-for-the-call> },
    "recurrence": {  
        "frequency": "Second|Minute|Hour|Week|Month|Year",
        "interval": "<recurrence interval in units of frequency>"
    },
    "conditions": [ <array-of-required-conditions > ],
    "splitOn" : "<property to create runs for>",
    "operationOptions": "<operation options on the trigger>"
}
```

### <a name="trigger-types-and-their-inputs"></a><span data-ttu-id="48fb7-114">Typy wyzwalaczy i ich dane wejściowe</span><span class="sxs-lookup"><span data-stu-id="48fb7-114">Trigger types and their inputs</span></span>  

<span data-ttu-id="48fb7-115">Można używać tych typów wyzwalaczy:</span><span class="sxs-lookup"><span data-stu-id="48fb7-115">You can use these types of triggers:</span></span>
  
-   <span data-ttu-id="48fb7-116">**Żądanie** \- sprawia, że aplikację logiki punktu końcowego, aby wywołać</span><span class="sxs-lookup"><span data-stu-id="48fb7-116">**Request** \- Makes the logic app an endpoint for you to call</span></span>  
  
-   <span data-ttu-id="48fb7-117">**Cykl** \- uruchamiany zgodnie z harmonogramem zdefiniowanym</span><span class="sxs-lookup"><span data-stu-id="48fb7-117">**Recurrence** \- Fires based on a defined schedule</span></span>  
  
-   <span data-ttu-id="48fb7-118">**HTTP** \- sonduje punkt końcowy HTTP sieci web.</span><span class="sxs-lookup"><span data-stu-id="48fb7-118">**HTTP** \- Polls an HTTP web endpoint.</span></span> <span data-ttu-id="48fb7-119">Punkt końcowy HTTP musi być zgodna z określonym kontraktem wyzwalająca \- przy użyciu 202\-wzorca asynchronicznego, lub tablicę</span><span class="sxs-lookup"><span data-stu-id="48fb7-119">The HTTP endpoint must conform to a specific triggering contract \- either by using a 202\-async pattern, or by returning an array</span></span>  
  
-   <span data-ttu-id="48fb7-120">**ApiConnection** \- wyzwolenia ankiety, takich jak HTTP, jednak ją korzysta z [zarządzany przez firmę Microsoft interfejsy API](https://docs.microsoft.com/azure/connectors/apis-list)</span><span class="sxs-lookup"><span data-stu-id="48fb7-120">**ApiConnection** \- Polls like the HTTP trigger, however, it takes advantage of the [Microsoft-managed APIs](https://docs.microsoft.com/azure/connectors/apis-list)</span></span>  
  
-   <span data-ttu-id="48fb7-121">**HTTPWebhook** \- otwiera jako punkt końcowy, podobnie jak ręczne wyzwalacza, jednak również wywołuje określony adres URL do rejestrowania i wyrejestrowania</span><span class="sxs-lookup"><span data-stu-id="48fb7-121">**HTTPWebhook** \- Opens an endpoint, similar to the Manual trigger, however, it also calls out to a specified URL to register and unregister</span></span>  
  
-   <span data-ttu-id="48fb7-122">**ApiConnectionWebhook** \- Operates, takich jak wyzwalacza HTTPWebhook dzięki wykorzystaniu interfejsów API zarządzany przez firmę Microsoft</span><span class="sxs-lookup"><span data-stu-id="48fb7-122">**ApiConnectionWebhook** \- Operates like the HTTPWebhook trigger by taking advantage of the Microsoft-managed APIs</span></span>       
    <span data-ttu-id="48fb7-123">Każdy typ wyzwalacza ma inny zestaw **dane wejściowe** definiuje zachowanie.</span><span class="sxs-lookup"><span data-stu-id="48fb7-123">Each trigger type has a different set of **inputs** that defines its behavior.</span></span>  
  
## <a name="request-trigger"></a><span data-ttu-id="48fb7-124">Wyzwalacz żądania</span><span class="sxs-lookup"><span data-stu-id="48fb7-124">Request trigger</span></span>  

<span data-ttu-id="48fb7-125">Tego wyzwalacza służy jako punkt końcowy, który należy wywołać za pomocą żądania HTTP do wywołania aplikacji logiki.</span><span class="sxs-lookup"><span data-stu-id="48fb7-125">This trigger serves as an endpoint that you call via an HTTP Request to invoke your logic app.</span></span> <span data-ttu-id="48fb7-126">Wyzwalacz żądania wygląda następująco:</span><span class="sxs-lookup"><span data-stu-id="48fb7-126">A request trigger looks like this example:</span></span>  
  
```json
"<name-of-the-trigger>" : {
    "type" : "request",
    "kind": "http",
    "inputs" : {
        "schema" : {
            "properties" : {
                "myInputProperty1" : { "type" : "string" },
                "myInputProperty2" : { "type" : "number" }
            },
        "required" : [ "myInputProperty1" ],
        "type" : "object"
        }
    }
} 
```

<span data-ttu-id="48fb7-127">Istnieje również opcjonalny właściwości o nazwie **schematu**:</span><span class="sxs-lookup"><span data-stu-id="48fb7-127">There is also an optional property called **schema**:</span></span>  
  
|<span data-ttu-id="48fb7-128">Nazwa elementu</span><span class="sxs-lookup"><span data-stu-id="48fb7-128">Element name</span></span>|<span data-ttu-id="48fb7-129">Wymagane</span><span class="sxs-lookup"><span data-stu-id="48fb7-129">Required</span></span>|<span data-ttu-id="48fb7-130">Opis</span><span class="sxs-lookup"><span data-stu-id="48fb7-130">Description</span></span>|  
|----------------|------------|---------------|  
|<span data-ttu-id="48fb7-131">Schemat</span><span class="sxs-lookup"><span data-stu-id="48fb7-131">schema</span></span>|<span data-ttu-id="48fb7-132">Nie</span><span class="sxs-lookup"><span data-stu-id="48fb7-132">No</span></span>|<span data-ttu-id="48fb7-133">Schematu JSON, która weryfikuje żądanie przychodzące.</span><span class="sxs-lookup"><span data-stu-id="48fb7-133">A JSON schema that validates the incoming request.</span></span> <span data-ttu-id="48fb7-134">Przydatne w przypadku myśl kolejnych kroków znać właściwości, które ma dotyczyć odwołanie.</span><span class="sxs-lookup"><span data-stu-id="48fb7-134">Useful for helping subsequent workflow steps know which properties to reference.</span></span>|

<span data-ttu-id="48fb7-135">Aby wywołać ten punkt końcowy, należy wywołać *listCallbackUrl* interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="48fb7-135">To invoke this endpoint, you need to call the *listCallbackUrl* API.</span></span> <span data-ttu-id="48fb7-136">Zobacz [interfejsu API REST usługi przepływu pracy](https://docs.microsoft.com/rest/api/logic/workflows).</span><span class="sxs-lookup"><span data-stu-id="48fb7-136">See [Workflow Service REST API](https://docs.microsoft.com/rest/api/logic/workflows).</span></span>  
  
## <a name="recurrence-trigger"></a><span data-ttu-id="48fb7-137">Wyzwalacz cyklu</span><span class="sxs-lookup"><span data-stu-id="48fb7-137">Recurrence trigger</span></span>  

<span data-ttu-id="48fb7-138">Wyzwalacz cyklu jest jedną, która będzie uruchamiana na zdefiniowanym harmonogramem.</span><span class="sxs-lookup"><span data-stu-id="48fb7-138">A Recurrence trigger is one that runs based on a defined schedule.</span></span> <span data-ttu-id="48fb7-139">Takie wyzwalacz może wyglądać w tym przykładzie:</span><span class="sxs-lookup"><span data-stu-id="48fb7-139">Such a trigger might look like this example:</span></span>  

```json
"dailyReport" : {
    "type": "recurrence",
    "recurrence": {
        "frequency": "Day",
        "interval": "1"
    }
}
```

<span data-ttu-id="48fb7-140">Jak widać, jest prosty sposób, aby uruchomić przepływ pracy.</span><span class="sxs-lookup"><span data-stu-id="48fb7-140">As you can see, it is a simple way to run a workflow.</span></span>  
  
|<span data-ttu-id="48fb7-141">Nazwa elementu</span><span class="sxs-lookup"><span data-stu-id="48fb7-141">Element name</span></span>|<span data-ttu-id="48fb7-142">Wymagane</span><span class="sxs-lookup"><span data-stu-id="48fb7-142">Required</span></span>|<span data-ttu-id="48fb7-143">Opis</span><span class="sxs-lookup"><span data-stu-id="48fb7-143">Description</span></span>|  
|----------------|------------|---------------|  
|<span data-ttu-id="48fb7-144">częstotliwość</span><span class="sxs-lookup"><span data-stu-id="48fb7-144">frequency</span></span>|<span data-ttu-id="48fb7-145">Tak</span><span class="sxs-lookup"><span data-stu-id="48fb7-145">Yes</span></span>|<span data-ttu-id="48fb7-146">Jak często wykonuje wyzwalacza.</span><span class="sxs-lookup"><span data-stu-id="48fb7-146">How often the trigger executes.</span></span> <span data-ttu-id="48fb7-147">Używać tylko jednej z następujących wartości: sekundy, minuty, godziny, dnia, tygodnia, miesiąc lub rok</span><span class="sxs-lookup"><span data-stu-id="48fb7-147">Use only one of these possible values: second, minute, hour, day, week, month, or year</span></span>|  
|<span data-ttu-id="48fb7-148">Interwał</span><span class="sxs-lookup"><span data-stu-id="48fb7-148">interval</span></span>|<span data-ttu-id="48fb7-149">Tak</span><span class="sxs-lookup"><span data-stu-id="48fb7-149">Yes</span></span>|<span data-ttu-id="48fb7-150">Interwał częstotliwości danego cyklu</span><span class="sxs-lookup"><span data-stu-id="48fb7-150">Interval of the given frequency for the recurrence</span></span>|  
|<span data-ttu-id="48fb7-151">startTime</span><span class="sxs-lookup"><span data-stu-id="48fb7-151">startTime</span></span>|<span data-ttu-id="48fb7-152">Nie</span><span class="sxs-lookup"><span data-stu-id="48fb7-152">No</span></span>|<span data-ttu-id="48fb7-153">Jeśli czas rozpoczęcia jest dostarczany bez przesunięcie czasu UTC, zostanie użyta tej strefy czasowej.</span><span class="sxs-lookup"><span data-stu-id="48fb7-153">If a startTime is provided without a UTC offset, this timeZone is used.</span></span>|  
|<span data-ttu-id="48fb7-154">Strefa czasowa</span><span class="sxs-lookup"><span data-stu-id="48fb7-154">timeZone</span></span>|<span data-ttu-id="48fb7-155">Brak</span><span class="sxs-lookup"><span data-stu-id="48fb7-155">no</span></span>|<span data-ttu-id="48fb7-156">Jeśli czas rozpoczęcia jest dostarczany bez przesunięcie czasu UTC, zostanie użyta tej strefy czasowej.</span><span class="sxs-lookup"><span data-stu-id="48fb7-156">If a startTime is provided without a UTC offset, this timeZone is used.</span></span>|  
  
<span data-ttu-id="48fb7-157">Można również zaplanować wyzwalacz można uruchomić wykonywania w pewnym momencie w przyszłości.</span><span class="sxs-lookup"><span data-stu-id="48fb7-157">You can also schedule a trigger to start executing at some point in the future.</span></span> <span data-ttu-id="48fb7-158">Na przykład jeśli chcesz uruchomić raport co tydzień w każdy poniedziałek można zaplanować aplikację logiki, aby uruchomić każdy poniedziałek, tworząc następujące wyzwalacz:</span><span class="sxs-lookup"><span data-stu-id="48fb7-158">For example, if you want to start a weekly report every Monday you can schedule the logic app to start every Monday by creating the following trigger:</span></span>  

```json
"dailyReport" : {
    "type": "recurrence",
    "recurrence": {
        "frequency": "Week",
        "interval": "1",
        "startTime" : "2015-06-22T00:00:00Z"
    }
}
```

## <a name="http-trigger"></a><span data-ttu-id="48fb7-159">Wyzwalacz HTTP</span><span class="sxs-lookup"><span data-stu-id="48fb7-159">HTTP trigger</span></span>  

<span data-ttu-id="48fb7-160">HTTP wyzwalacze sondowania określony punkt końcowy i sprawdź odpowiedzi, aby określić, czy można wykonać przepływu pracy.</span><span class="sxs-lookup"><span data-stu-id="48fb7-160">HTTP triggers poll a specified endpoint and check the response to determine whether the workflow should be executed.</span></span> <span data-ttu-id="48fb7-161">Obiekt dane wejściowe przyjmuje zbiór parametrów wymaganych do utworzenia połączenia HTTP:</span><span class="sxs-lookup"><span data-stu-id="48fb7-161">The inputs object takes the set of parameters required to construct an HTTP call:</span></span>  
  
|<span data-ttu-id="48fb7-162">Nazwa elementu</span><span class="sxs-lookup"><span data-stu-id="48fb7-162">Element name</span></span>|<span data-ttu-id="48fb7-163">Wymagane</span><span class="sxs-lookup"><span data-stu-id="48fb7-163">Required</span></span>|<span data-ttu-id="48fb7-164">Opis</span><span class="sxs-lookup"><span data-stu-id="48fb7-164">Description</span></span>|<span data-ttu-id="48fb7-165">Typ</span><span class="sxs-lookup"><span data-stu-id="48fb7-165">Type</span></span>|  
|----------------|------------|---------------|--------|  
|<span data-ttu-id="48fb7-166">— Metoda</span><span class="sxs-lookup"><span data-stu-id="48fb7-166">method</span></span>|<span data-ttu-id="48fb7-167">Tak</span><span class="sxs-lookup"><span data-stu-id="48fb7-167">yes</span></span>|<span data-ttu-id="48fb7-168">Może być jedną z następujących metod HTTP: GET, POST, PUT, DELETE, poprawki lub HEAD</span><span class="sxs-lookup"><span data-stu-id="48fb7-168">Can be one of the following HTTP methods: GET, POST, PUT, DELETE, PATCH, or HEAD</span></span>|<span data-ttu-id="48fb7-169">Ciąg</span><span class="sxs-lookup"><span data-stu-id="48fb7-169">String</span></span>|  
|<span data-ttu-id="48fb7-170">Identyfikator URI</span><span class="sxs-lookup"><span data-stu-id="48fb7-170">uri</span></span>|<span data-ttu-id="48fb7-171">Tak</span><span class="sxs-lookup"><span data-stu-id="48fb7-171">yes</span></span>|<span data-ttu-id="48fb7-172">Końcowy http lub https, która jest wywoływana.</span><span class="sxs-lookup"><span data-stu-id="48fb7-172">The http or https endpoint that is called.</span></span> <span data-ttu-id="48fb7-173">Maksymalnie 2 kilobajtów.</span><span class="sxs-lookup"><span data-stu-id="48fb7-173">Maximum of 2 kilobytes.</span></span>|<span data-ttu-id="48fb7-174">Ciąg</span><span class="sxs-lookup"><span data-stu-id="48fb7-174">String</span></span>|  
|<span data-ttu-id="48fb7-175">— zapytania</span><span class="sxs-lookup"><span data-stu-id="48fb7-175">queries</span></span>|<span data-ttu-id="48fb7-176">Nie</span><span class="sxs-lookup"><span data-stu-id="48fb7-176">No</span></span>|<span data-ttu-id="48fb7-177">Obiekt reprezentujący parametry zapytania, aby dodać do adresu URL.</span><span class="sxs-lookup"><span data-stu-id="48fb7-177">An object representing the query parameters to add to the URL.</span></span> <span data-ttu-id="48fb7-178">Na przykład `"queries" : { "api-version": "2015-02-01" }` dodaje `?api-version=2015-02-01` do adresu URL.</span><span class="sxs-lookup"><span data-stu-id="48fb7-178">For example, `"queries" : { "api-version": "2015-02-01" }` adds `?api-version=2015-02-01` to the URL.</span></span>|<span data-ttu-id="48fb7-179">Obiekt</span><span class="sxs-lookup"><span data-stu-id="48fb7-179">Object</span></span>|  
|<span data-ttu-id="48fb7-180">Nagłówki</span><span class="sxs-lookup"><span data-stu-id="48fb7-180">headers</span></span>|<span data-ttu-id="48fb7-181">Nie</span><span class="sxs-lookup"><span data-stu-id="48fb7-181">No</span></span>|<span data-ttu-id="48fb7-182">Obiekt reprezentujący listę nagłówków, które są wysyłane do żądania.</span><span class="sxs-lookup"><span data-stu-id="48fb7-182">An object representing each of the headers that is sent to the request.</span></span> <span data-ttu-id="48fb7-183">Na przykład, aby ustawić język i typ żądania:`"headers" : { "Accept-Language": "en-us",  "Content-Type": "application/json" }`</span><span class="sxs-lookup"><span data-stu-id="48fb7-183">For example, to set the language and type on a request: `"headers" : { "Accept-Language": "en-us",  "Content-Type": "application/json" }`</span></span>|<span data-ttu-id="48fb7-184">Obiekt</span><span class="sxs-lookup"><span data-stu-id="48fb7-184">Object</span></span>|  
|<span data-ttu-id="48fb7-185">Treści</span><span class="sxs-lookup"><span data-stu-id="48fb7-185">body</span></span>|<span data-ttu-id="48fb7-186">Nie</span><span class="sxs-lookup"><span data-stu-id="48fb7-186">No</span></span>|<span data-ttu-id="48fb7-187">Obiekt reprezentujący ładunku, które są wysyłane do punktu końcowego.</span><span class="sxs-lookup"><span data-stu-id="48fb7-187">An object representing the payload that is sent to the endpoint.</span></span>|<span data-ttu-id="48fb7-188">Obiekt</span><span class="sxs-lookup"><span data-stu-id="48fb7-188">Object</span></span>|  
|<span data-ttu-id="48fb7-189">retryPolicy</span><span class="sxs-lookup"><span data-stu-id="48fb7-189">retryPolicy</span></span>|<span data-ttu-id="48fb7-190">Nie</span><span class="sxs-lookup"><span data-stu-id="48fb7-190">No</span></span>|<span data-ttu-id="48fb7-191">Obiekt, który można dostosować zachowanie ponownych prób dla 4xx lub 5xx błędów.</span><span class="sxs-lookup"><span data-stu-id="48fb7-191">An object that lets you customize the retry behavior for 4xx or 5xx errors.</span></span>|<span data-ttu-id="48fb7-192">Obiekt</span><span class="sxs-lookup"><span data-stu-id="48fb7-192">Object</span></span>|  
|<span data-ttu-id="48fb7-193">Uwierzytelnianie</span><span class="sxs-lookup"><span data-stu-id="48fb7-193">authentication</span></span>|<span data-ttu-id="48fb7-194">Nie</span><span class="sxs-lookup"><span data-stu-id="48fb7-194">No</span></span>|<span data-ttu-id="48fb7-195">Reprezentuje metodę uwierzytelniania żądania.</span><span class="sxs-lookup"><span data-stu-id="48fb7-195">Represents the method that the request should be authenticated.</span></span> <span data-ttu-id="48fb7-196">Aby uzyskać więcej informacji na ten obiekt, zobacz [uwierzytelniania połączeń wychodzących harmonogramu](https://docs.microsoft.com/azure/scheduler/scheduler-outbound-authentication).</span><span class="sxs-lookup"><span data-stu-id="48fb7-196">For details on this object, see [Scheduler Outbound Authentication](https://docs.microsoft.com/azure/scheduler/scheduler-outbound-authentication).</span></span> <span data-ttu-id="48fb7-197">Poza harmonogramem, jest jedna właściwość więcej obsługiwanych: `authority` domyślnie ta wartość jest `https://login.windows.net` gdy nie jest określony, można używać różnych odbiorców, takich jak`https://login.windows\-ppe.net`</span><span class="sxs-lookup"><span data-stu-id="48fb7-197">Beyond scheduler, there is one more supported property: `authority` By default, this value is `https://login.windows.net` when not specified, but you can use a different audience like `https://login.windows\-ppe.net`</span></span>|<span data-ttu-id="48fb7-198">Obiekt</span><span class="sxs-lookup"><span data-stu-id="48fb7-198">Object</span></span>|  
  
<span data-ttu-id="48fb7-199">Wyzwalacza HTTP wymaga interfejsu API HTTP był zgodny z określonym wzorcem do sprawnej współpracy z aplikacji logiki.</span><span class="sxs-lookup"><span data-stu-id="48fb7-199">The HTTP trigger requires the HTTP API to conform with a specific pattern to work well with your logic app.</span></span> <span data-ttu-id="48fb7-200">Wymaga on następujące pola:</span><span class="sxs-lookup"><span data-stu-id="48fb7-200">It requires the following fields:</span></span>  
  
|<span data-ttu-id="48fb7-201">Odpowiedź</span><span class="sxs-lookup"><span data-stu-id="48fb7-201">Response</span></span>|<span data-ttu-id="48fb7-202">Opis</span><span class="sxs-lookup"><span data-stu-id="48fb7-202">Description</span></span>|  
|------------|---------------|  
|<span data-ttu-id="48fb7-203">Kod stanu</span><span class="sxs-lookup"><span data-stu-id="48fb7-203">Status code</span></span>|<span data-ttu-id="48fb7-204">Kod stanu 200 \(OK\) spowodować do uruchomienia.</span><span class="sxs-lookup"><span data-stu-id="48fb7-204">Status code 200 \(OK\) to cause a run.</span></span> <span data-ttu-id="48fb7-205">Każdy kod stanu nie powoduje uruchomienia.</span><span class="sxs-lookup"><span data-stu-id="48fb7-205">Any other status code doesn't cause a run.</span></span>|  
|<span data-ttu-id="48fb7-206">Spróbuj ponownie\-po nagłówka</span><span class="sxs-lookup"><span data-stu-id="48fb7-206">Retry\-after header</span></span>|<span data-ttu-id="48fb7-207">Liczba sekund do aplikacji logiki sonduje ponownie punkt końcowy.</span><span class="sxs-lookup"><span data-stu-id="48fb7-207">Number of seconds until the logic app polls the endpoint again.</span></span>|  
|<span data-ttu-id="48fb7-208">Nagłówek lokalizacji</span><span class="sxs-lookup"><span data-stu-id="48fb7-208">Location header</span></span>|<span data-ttu-id="48fb7-209">Adres URL do wywołania w następnym interwału sondowania.</span><span class="sxs-lookup"><span data-stu-id="48fb7-209">The URL to call on the next polling interval.</span></span> <span data-ttu-id="48fb7-210">Jeśli nie zostanie określony, używany jest oryginalny adres URL.</span><span class="sxs-lookup"><span data-stu-id="48fb7-210">If not specified, the original URL is used.</span></span>|  
  
<span data-ttu-id="48fb7-211">Oto kilka przykładów różne zachowania dla różnych typów żądań:</span><span class="sxs-lookup"><span data-stu-id="48fb7-211">Here are some examples of different behaviors for different types of requests:</span></span>  
  
|<span data-ttu-id="48fb7-212">Kod odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="48fb7-212">Response code</span></span>|<span data-ttu-id="48fb7-213">Spróbuj ponownie\-po</span><span class="sxs-lookup"><span data-stu-id="48fb7-213">Retry\-After</span></span>|<span data-ttu-id="48fb7-214">Zachowanie</span><span class="sxs-lookup"><span data-stu-id="48fb7-214">Behavior</span></span>|  
|-----------------|----------------|------------|  
|<span data-ttu-id="48fb7-215">200</span><span class="sxs-lookup"><span data-stu-id="48fb7-215">200</span></span>|<span data-ttu-id="48fb7-216">\(Brak\)</span><span class="sxs-lookup"><span data-stu-id="48fb7-216">\(none\)</span></span>|<span data-ttu-id="48fb7-217">Nie prawidłowy wyzwalacza, ponów próbę\-po jest wymagane, lub #else aparat nigdy nie sonduje dla następnego żądania.</span><span class="sxs-lookup"><span data-stu-id="48fb7-217">Not a valid trigger, Retry\-After is required, or else the engine never polls for the next request.</span></span>|  
|<span data-ttu-id="48fb7-218">202</span><span class="sxs-lookup"><span data-stu-id="48fb7-218">202</span></span>|<span data-ttu-id="48fb7-219">60</span><span class="sxs-lookup"><span data-stu-id="48fb7-219">60</span></span>|<span data-ttu-id="48fb7-220">Nie wyzwala przepływ pracy.</span><span class="sxs-lookup"><span data-stu-id="48fb7-220">Do not trigger the workflow.</span></span> <span data-ttu-id="48fb7-221">Przy następnej próbie odbywa się w jednej minuty.</span><span class="sxs-lookup"><span data-stu-id="48fb7-221">The next attempt happens in one minute.</span></span>|  
|<span data-ttu-id="48fb7-222">200</span><span class="sxs-lookup"><span data-stu-id="48fb7-222">200</span></span>|<span data-ttu-id="48fb7-223">10</span><span class="sxs-lookup"><span data-stu-id="48fb7-223">10</span></span>|<span data-ttu-id="48fb7-224">Uruchamianie przepływu pracy i sprawdź ponownie więcej zawartości za 10 sekund.</span><span class="sxs-lookup"><span data-stu-id="48fb7-224">Run the workflow, and check again for more content in 10 seconds.</span></span>|  
|<span data-ttu-id="48fb7-225">400</span><span class="sxs-lookup"><span data-stu-id="48fb7-225">400</span></span>|<span data-ttu-id="48fb7-226">\(Brak\)</span><span class="sxs-lookup"><span data-stu-id="48fb7-226">\(none\)</span></span>|<span data-ttu-id="48fb7-227">Nieprawidłowe żądanie, nie uruchamiaj przepływ pracy.</span><span class="sxs-lookup"><span data-stu-id="48fb7-227">Bad request, do not run the workflow.</span></span> <span data-ttu-id="48fb7-228">W przypadku nie **ponów zasad** zdefiniowany, zostanie użyta domyślna zasada.</span><span class="sxs-lookup"><span data-stu-id="48fb7-228">If there is no **Retry Policy** defined, then the default policy is used.</span></span> <span data-ttu-id="48fb7-229">Po osiągnięciu liczby ponownych prób wyzwalacz nie jest już prawidłowy.</span><span class="sxs-lookup"><span data-stu-id="48fb7-229">After the number of retries has been reached, the trigger is no longer valid.</span></span>|  
|<span data-ttu-id="48fb7-230">500</span><span class="sxs-lookup"><span data-stu-id="48fb7-230">500</span></span>|<span data-ttu-id="48fb7-231">\(Brak\)</span><span class="sxs-lookup"><span data-stu-id="48fb7-231">\(none\)</span></span>|<span data-ttu-id="48fb7-232">Błąd serwera, nie uruchamiaj przepływ pracy.</span><span class="sxs-lookup"><span data-stu-id="48fb7-232">Server error, do not run the workflow.</span></span>  <span data-ttu-id="48fb7-233">W przypadku nie **ponów zasad** zdefiniowany, zostanie użyta domyślna zasada.</span><span class="sxs-lookup"><span data-stu-id="48fb7-233">If there is no **Retry Policy** defined, then the default policy is used.</span></span> <span data-ttu-id="48fb7-234">Po osiągnięciu liczby ponownych prób wyzwalacz nie jest już prawidłowy.</span><span class="sxs-lookup"><span data-stu-id="48fb7-234">After the number of retries has been reached, the trigger is no longer valid.</span></span>|  
  
<span data-ttu-id="48fb7-235">Dane wyjściowe wyzwalacza HTTP wyglądać w tym przykładzie:</span><span class="sxs-lookup"><span data-stu-id="48fb7-235">The outputs of an HTTP trigger look like this example:</span></span>  
  
|<span data-ttu-id="48fb7-236">Nazwa elementu</span><span class="sxs-lookup"><span data-stu-id="48fb7-236">Element name</span></span>|<span data-ttu-id="48fb7-237">Opis</span><span class="sxs-lookup"><span data-stu-id="48fb7-237">Description</span></span>|<span data-ttu-id="48fb7-238">Typ</span><span class="sxs-lookup"><span data-stu-id="48fb7-238">Type</span></span>|  
|----------------|---------------|--------|  
|<span data-ttu-id="48fb7-239">Nagłówki</span><span class="sxs-lookup"><span data-stu-id="48fb7-239">headers</span></span>|<span data-ttu-id="48fb7-240">Nagłówki odpowiedzi http.</span><span class="sxs-lookup"><span data-stu-id="48fb7-240">The headers of the http response.</span></span>|<span data-ttu-id="48fb7-241">Obiekt</span><span class="sxs-lookup"><span data-stu-id="48fb7-241">Object</span></span>|  
|<span data-ttu-id="48fb7-242">Treści</span><span class="sxs-lookup"><span data-stu-id="48fb7-242">body</span></span>|<span data-ttu-id="48fb7-243">Treść odpowiedzi http.</span><span class="sxs-lookup"><span data-stu-id="48fb7-243">The body of the http response.</span></span>|<span data-ttu-id="48fb7-244">Obiekt</span><span class="sxs-lookup"><span data-stu-id="48fb7-244">Object</span></span>|  
  
## <a name="api-connection-trigger"></a><span data-ttu-id="48fb7-245">Połączenie z interfejsem API wyzwalacza</span><span class="sxs-lookup"><span data-stu-id="48fb7-245">API Connection trigger</span></span>  

<span data-ttu-id="48fb7-246">Wyzwalacz połączenia interfejsu API jest podobny do wyzwalacza HTTP w jego podstawowych funkcji.</span><span class="sxs-lookup"><span data-stu-id="48fb7-246">The API connection trigger is similar to the HTTP trigger in its basic functionality.</span></span> <span data-ttu-id="48fb7-247">Jednak parametry do identyfikacji akcji są różne.</span><span class="sxs-lookup"><span data-stu-id="48fb7-247">However, the parameters for identifying the action are different.</span></span> <span data-ttu-id="48fb7-248">Oto przykład:</span><span class="sxs-lookup"><span data-stu-id="48fb7-248">Here is an example:</span></span>  
  
```json
"dailyReport" : {
    "type": "ApiConnection",
    "inputs": {
        "host": {
            "api": {
                "runtimeUrl": "https://myarticles.example.com/"
            },
        }
        "connection": {
            "name": "@parameters('$connections')['myconnection'].name"
        }
    },  
    "method": "POST",
    "body": {
        "category": "awesomest"
    }
}
```

|<span data-ttu-id="48fb7-249">Nazwa elementu</span><span class="sxs-lookup"><span data-stu-id="48fb7-249">Element name</span></span>|<span data-ttu-id="48fb7-250">Wymagane</span><span class="sxs-lookup"><span data-stu-id="48fb7-250">Required</span></span>|<span data-ttu-id="48fb7-251">Typ</span><span class="sxs-lookup"><span data-stu-id="48fb7-251">Type</span></span>|<span data-ttu-id="48fb7-252">Opis</span><span class="sxs-lookup"><span data-stu-id="48fb7-252">Description</span></span>|  
|----------------|------------|--------|---------------|  
|<span data-ttu-id="48fb7-253">Host</span><span class="sxs-lookup"><span data-stu-id="48fb7-253">host</span></span>|<span data-ttu-id="48fb7-254">Tak</span><span class="sxs-lookup"><span data-stu-id="48fb7-254">Yes</span></span>||<span data-ttu-id="48fb7-255">ApiApp hostowana bramy i identyfikator.</span><span class="sxs-lookup"><span data-stu-id="48fb7-255">The ApiApp hosted gateway and id.</span></span>|  
|<span data-ttu-id="48fb7-256">— Metoda</span><span class="sxs-lookup"><span data-stu-id="48fb7-256">method</span></span>|<span data-ttu-id="48fb7-257">Tak</span><span class="sxs-lookup"><span data-stu-id="48fb7-257">Yes</span></span>|<span data-ttu-id="48fb7-258">Ciąg</span><span class="sxs-lookup"><span data-stu-id="48fb7-258">String</span></span>|<span data-ttu-id="48fb7-259">Może być jedną z następujących metod HTTP: **UZYSKAĆ**, **POST**, **PUT**, **usunąć**, **poprawka**, lub  **HEAD**</span><span class="sxs-lookup"><span data-stu-id="48fb7-259">Can be one of the following HTTP methods: **GET**, **POST**, **PUT**, **DELETE**, **PATCH**, or **HEAD**</span></span>|  
|<span data-ttu-id="48fb7-260">— zapytania</span><span class="sxs-lookup"><span data-stu-id="48fb7-260">queries</span></span>|<span data-ttu-id="48fb7-261">Nie</span><span class="sxs-lookup"><span data-stu-id="48fb7-261">No</span></span>|<span data-ttu-id="48fb7-262">Obiekt</span><span class="sxs-lookup"><span data-stu-id="48fb7-262">Object</span></span>|<span data-ttu-id="48fb7-263">Reprezentuje parametry zapytania, które mają zostać dodane do adresu URL.</span><span class="sxs-lookup"><span data-stu-id="48fb7-263">Represents the query parameters to be added to the URL.</span></span> <span data-ttu-id="48fb7-264">Na przykład `"queries" : { "api-version": "2015-02-01" }` dodaje `?api-version=2015-02-01` do adresu URL.</span><span class="sxs-lookup"><span data-stu-id="48fb7-264">For example, `"queries" : { "api-version": "2015-02-01" }` adds `?api-version=2015-02-01` to the URL.</span></span>|  
|<span data-ttu-id="48fb7-265">Nagłówki</span><span class="sxs-lookup"><span data-stu-id="48fb7-265">headers</span></span>|<span data-ttu-id="48fb7-266">Nie</span><span class="sxs-lookup"><span data-stu-id="48fb7-266">No</span></span>|<span data-ttu-id="48fb7-267">Obiekt</span><span class="sxs-lookup"><span data-stu-id="48fb7-267">Object</span></span>|<span data-ttu-id="48fb7-268">Reprezentuje listę nagłówków, które są wysyłane do żądania.</span><span class="sxs-lookup"><span data-stu-id="48fb7-268">Represents each of the headers that is sent to the request.</span></span> <span data-ttu-id="48fb7-269">Na przykład, aby ustawić język i typ żądania:`"headers" : { "Accept-Language": "en-us",  "Content-Type": "application/json" }`</span><span class="sxs-lookup"><span data-stu-id="48fb7-269">For example, to set the language and type on a request: `"headers" : { "Accept-Language": "en-us",  "Content-Type": "application/json" }`</span></span>|  
|<span data-ttu-id="48fb7-270">Treści</span><span class="sxs-lookup"><span data-stu-id="48fb7-270">body</span></span>|<span data-ttu-id="48fb7-271">Nie</span><span class="sxs-lookup"><span data-stu-id="48fb7-271">No</span></span>|<span data-ttu-id="48fb7-272">Obiekt</span><span class="sxs-lookup"><span data-stu-id="48fb7-272">Object</span></span>|<span data-ttu-id="48fb7-273">Reprezentuje ładunek, które są wysyłane do punktu końcowego.</span><span class="sxs-lookup"><span data-stu-id="48fb7-273">Represents the payload that is sent to the endpoint.</span></span>|  
|<span data-ttu-id="48fb7-274">retryPolicy</span><span class="sxs-lookup"><span data-stu-id="48fb7-274">retryPolicy</span></span>|<span data-ttu-id="48fb7-275">Nie</span><span class="sxs-lookup"><span data-stu-id="48fb7-275">No</span></span>|<span data-ttu-id="48fb7-276">Obiekt</span><span class="sxs-lookup"><span data-stu-id="48fb7-276">Object</span></span>|<span data-ttu-id="48fb7-277">Umożliwia dostosowanie zachowanie ponownych prób dla 4xx lub 5xx błędów.</span><span class="sxs-lookup"><span data-stu-id="48fb7-277">Allows you to customize the retry behavior for 4xx or 5xx errors.</span></span>|  
|<span data-ttu-id="48fb7-278">Uwierzytelnianie</span><span class="sxs-lookup"><span data-stu-id="48fb7-278">authentication</span></span>|<span data-ttu-id="48fb7-279">Nie</span><span class="sxs-lookup"><span data-stu-id="48fb7-279">No</span></span>|<span data-ttu-id="48fb7-280">Obiekt</span><span class="sxs-lookup"><span data-stu-id="48fb7-280">Object</span></span>|<span data-ttu-id="48fb7-281">Reprezentuje metodę uwierzytelniania żądania.</span><span class="sxs-lookup"><span data-stu-id="48fb7-281">Represents the method that the request should be authenticated.</span></span> <span data-ttu-id="48fb7-282">Aby uzyskać więcej informacji na ten obiekt, zobacz [uwierzytelniania połączeń wychodzących harmonogramu](https://docs.microsoft.com/azure/scheduler/scheduler-outbound-authentication)</span><span class="sxs-lookup"><span data-stu-id="48fb7-282">For details on this object, see [Scheduler Outbound Authentication](https://docs.microsoft.com/azure/scheduler/scheduler-outbound-authentication)</span></span>|  
  
<span data-ttu-id="48fb7-283">Właściwości hosta są:</span><span class="sxs-lookup"><span data-stu-id="48fb7-283">The properties for host are:</span></span>  
  
|<span data-ttu-id="48fb7-284">Nazwa elementu</span><span class="sxs-lookup"><span data-stu-id="48fb7-284">Element name</span></span>|<span data-ttu-id="48fb7-285">Wymagane</span><span class="sxs-lookup"><span data-stu-id="48fb7-285">Required</span></span>|<span data-ttu-id="48fb7-286">Opis</span><span class="sxs-lookup"><span data-stu-id="48fb7-286">Description</span></span>|  
|----------------|------------|---------------|  
|<span data-ttu-id="48fb7-287">runtimeUrl interfejsu API</span><span class="sxs-lookup"><span data-stu-id="48fb7-287">api runtimeUrl</span></span>|<span data-ttu-id="48fb7-288">Tak</span><span class="sxs-lookup"><span data-stu-id="48fb7-288">Yes</span></span>|<span data-ttu-id="48fb7-289">Punkt końcowy zarządzanego interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="48fb7-289">The endpoint of the managed API.</span></span>|  
|<span data-ttu-id="48fb7-290">Nazwa połączenia</span><span class="sxs-lookup"><span data-stu-id="48fb7-290">connection name</span></span>||<span data-ttu-id="48fb7-291">Musi być odwołaniem do parametru o nazwie `$connection` , a to nazwa zarządzanego połączenia interfejsu API, używanych przez przepływ pracy.</span><span class="sxs-lookup"><span data-stu-id="48fb7-291">Must be a reference to a parameter called `$connection` and is the name of the managed API connection that the workflow uses.</span></span>|
  
<span data-ttu-id="48fb7-292">Dostępne są następujące dane wyjściowe wyzwalacza połączenia interfejsu API:</span><span class="sxs-lookup"><span data-stu-id="48fb7-292">The outputs of an API connection trigger are:</span></span>
  
|<span data-ttu-id="48fb7-293">Nazwa elementu</span><span class="sxs-lookup"><span data-stu-id="48fb7-293">Element name</span></span>|<span data-ttu-id="48fb7-294">Typ</span><span class="sxs-lookup"><span data-stu-id="48fb7-294">Type</span></span>|<span data-ttu-id="48fb7-295">Opis</span><span class="sxs-lookup"><span data-stu-id="48fb7-295">Description</span></span>|  
|----------------|--------|---------------|  
|<span data-ttu-id="48fb7-296">Nagłówki</span><span class="sxs-lookup"><span data-stu-id="48fb7-296">headers</span></span>|<span data-ttu-id="48fb7-297">Obiekt</span><span class="sxs-lookup"><span data-stu-id="48fb7-297">Object</span></span>|<span data-ttu-id="48fb7-298">Nagłówki odpowiedzi http.</span><span class="sxs-lookup"><span data-stu-id="48fb7-298">The headers of the http response.</span></span>|  
|<span data-ttu-id="48fb7-299">Treści</span><span class="sxs-lookup"><span data-stu-id="48fb7-299">body</span></span>|<span data-ttu-id="48fb7-300">Obiekt</span><span class="sxs-lookup"><span data-stu-id="48fb7-300">Object</span></span>|<span data-ttu-id="48fb7-301">Treść odpowiedzi http.</span><span class="sxs-lookup"><span data-stu-id="48fb7-301">The body of the http response.</span></span>|  
  
## <a name="httpwebhook-trigger"></a><span data-ttu-id="48fb7-302">Wyzwalacz HTTPWebhook</span><span class="sxs-lookup"><span data-stu-id="48fb7-302">HTTPWebhook trigger</span></span>  

<span data-ttu-id="48fb7-303">Wyzwalacz HTTPWebhook otwiera punkt końcowy jest podobny do ręcznego wyzwalacza, ale określony adres URL do rejestrowania i wyrejestrowania uwidacznia również HTTPWebhook wyzwalacza.</span><span class="sxs-lookup"><span data-stu-id="48fb7-303">The HTTPWebhook trigger opens an endpoint, similar to the manual trigger, but the HTTPWebhook trigger also calls out to a specified URL to register and unregister.</span></span> <span data-ttu-id="48fb7-304">Oto przykład co wyzwalacz HTTPWebhook może wyglądać tak:</span><span class="sxs-lookup"><span data-stu-id="48fb7-304">Here's an example of what an HTTPWebhook trigger might look like:</span></span>  

```json
"myappspottrigger": {
    "type": "httpWebhook",
    "inputs": {
        "subscribe": {
            "method": "POST",
            "uri": "https://pubsubhubbub.appspot.com/subscribe",
            "headers": { },
            "body": {
                "hub.callback": "@{listCallbackUrl()}",
                "hub.mode": "subscribe",
                "hub.topic": "https://pubsubhubbub.appspot.com/articleCategories/technology"
            },
            "authentication": { },
            "retryPolicy": { }
        },
        "unsubscribe": {
            "url": "https://pubsubhubbub.appspot.com/subscribe",
            "body": {
                "hub.callback": "@{workflow().endpoint}@{listCallbackUrl()}",
                "hub.mode": "unsubscribe",
                "hub.topic": "https://pubsubhubbub.appspot.com/articleCategories/technology"
            },
            "method": "POST",
            "authentication": { }
        }
    },
    "conditions": [ ]
    }
```

<span data-ttu-id="48fb7-305">Wiele z tych sekcji są opcjonalne i zachowanie elementu Webhook jest zależna od sekcje są udostępniane lub pominięta.</span><span class="sxs-lookup"><span data-stu-id="48fb7-305">Many of these sections are optional, and the behavior of the Webhook depends on which sections are provided or omitted.</span></span>  
<span data-ttu-id="48fb7-306">Właściwości elementu Webhook są następujące:</span><span class="sxs-lookup"><span data-stu-id="48fb7-306">The properties of a Webhook are as follows:</span></span>  
  
|<span data-ttu-id="48fb7-307">Nazwa elementu</span><span class="sxs-lookup"><span data-stu-id="48fb7-307">Element name</span></span>|<span data-ttu-id="48fb7-308">Wymagane</span><span class="sxs-lookup"><span data-stu-id="48fb7-308">Required</span></span>|<span data-ttu-id="48fb7-309">Opis</span><span class="sxs-lookup"><span data-stu-id="48fb7-309">Description</span></span>|  
|----------------|------------|---------------|  
|<span data-ttu-id="48fb7-310">Subskrypcja</span><span class="sxs-lookup"><span data-stu-id="48fb7-310">subscribe</span></span>|<span data-ttu-id="48fb7-311">Nie</span><span class="sxs-lookup"><span data-stu-id="48fb7-311">No</span></span>|<span data-ttu-id="48fb7-312">Żądania wychodzącego jest wywoływane, gdy wyzwalacza jest tworzony i wykonuje początkowe rejestracyjny.</span><span class="sxs-lookup"><span data-stu-id="48fb7-312">The outgoing request that is called when the trigger is created and performs the initial registration.</span></span>|  
|<span data-ttu-id="48fb7-313">Anulowanie subskrypcji</span><span class="sxs-lookup"><span data-stu-id="48fb7-313">unsubscribe</span></span>|<span data-ttu-id="48fb7-314">Nie</span><span class="sxs-lookup"><span data-stu-id="48fb7-314">No</span></span>|<span data-ttu-id="48fb7-315">Żądania wychodzącego po usunięciu wyzwalacza.</span><span class="sxs-lookup"><span data-stu-id="48fb7-315">The outgoing request when the trigger is deleted.</span></span>|  
  
-   <span data-ttu-id="48fb7-316">**Subskrypcja** jest wywołanie wychodzących, które ma na celu rozpoczyna nasłuchiwanie zdarzeń.</span><span class="sxs-lookup"><span data-stu-id="48fb7-316">**Subscribe** is the outgoing call that's made to start listening to events.</span></span> <span data-ttu-id="48fb7-317">To wywołanie rozpoczyna się od tego samego zestawu parametrów, które wykonują normalnego działania protokołu HTTP.</span><span class="sxs-lookup"><span data-stu-id="48fb7-317">This call starts with the same set of parameters that the normal HTTP actions do.</span></span> <span data-ttu-id="48fb7-318">Ta wychodzących wywołanie żadnego zmianie przepływu pracy w dowolny sposób, na przykład, jeśli poświadczenia zostały wycofane, lub zmień parametry wejściowe tego wyzwalacza.</span><span class="sxs-lookup"><span data-stu-id="48fb7-318">This outgoing call is made any time the workflow changes in any way, for example, whenever the credentials are rolled, or the trigger's input parameters change.</span></span>
  
    <span data-ttu-id="48fb7-319">Aby zapewnić obsługę tego wywołania, jest nowa funkcja: `@listCallbackUrl()`.</span><span class="sxs-lookup"><span data-stu-id="48fb7-319">To support this call, there is a new function: `@listCallbackUrl()`.</span></span> <span data-ttu-id="48fb7-320">Ta funkcja zwraca unikatowy adres URL dla tego wyzwalacza określonych w tym przepływie pracy.</span><span class="sxs-lookup"><span data-stu-id="48fb7-320">This function returns a unique URL for this specific trigger in this workflow.</span></span> <span data-ttu-id="48fb7-321">Reprezentuje unikatowy identyfikator dla punktów końcowych, które używają usługi REST.</span><span class="sxs-lookup"><span data-stu-id="48fb7-321">It represents the unique identifier for the endpoints that use the Service REST.</span></span>  
  
-   <span data-ttu-id="48fb7-322">**Anulowanie subskrypcji** jest wywoływane, gdy operacja renderuje tego wyzwalacza nieprawidłowe, w tym:</span><span class="sxs-lookup"><span data-stu-id="48fb7-322">**Unsubscribe** is called when an operation renders this trigger invalid, including:</span></span>  
  
    -   <span data-ttu-id="48fb7-323">Usuwanie lub wyłączanie wyzwalacza</span><span class="sxs-lookup"><span data-stu-id="48fb7-323">Deleting or disabling the trigger</span></span>  
  
    -   <span data-ttu-id="48fb7-324">Usuwanie lub wyłączanie przepływu pracy</span><span class="sxs-lookup"><span data-stu-id="48fb7-324">Deleting or disabling the workflow</span></span>  
  
    -   <span data-ttu-id="48fb7-325">Usunięcie lub wyłączenie subskrypcji</span><span class="sxs-lookup"><span data-stu-id="48fb7-325">Deleting or disabling the subscription</span></span>  
  
    <span data-ttu-id="48fb7-326">Aplikacja logiki automatycznie wywołuje akcję anulowania subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="48fb7-326">The logic app automatically calls the unsubscribe action.</span></span> <span data-ttu-id="48fb7-327">Parametry tej funkcji są takie same jak wyzwalacza HTTP.</span><span class="sxs-lookup"><span data-stu-id="48fb7-327">The parameters to this function are the same as the HTTP trigger.</span></span>  
  
    <span data-ttu-id="48fb7-328">Dane wyjściowe wyzwalacza HTTPWebhook są zawartość żądania przychodzącego, jeśli:</span><span class="sxs-lookup"><span data-stu-id="48fb7-328">The outputs of the HTTPWebhook trigger are the contents of the incoming request:</span></span>  
  
|<span data-ttu-id="48fb7-329">Nazwa elementu</span><span class="sxs-lookup"><span data-stu-id="48fb7-329">Element name</span></span>|<span data-ttu-id="48fb7-330">Typ</span><span class="sxs-lookup"><span data-stu-id="48fb7-330">Type</span></span>|<span data-ttu-id="48fb7-331">Opis</span><span class="sxs-lookup"><span data-stu-id="48fb7-331">Description</span></span>|  
|-----------------|--------|---------------|  
|<span data-ttu-id="48fb7-332">Nagłówki</span><span class="sxs-lookup"><span data-stu-id="48fb7-332">headers</span></span>|<span data-ttu-id="48fb7-333">Obiekt</span><span class="sxs-lookup"><span data-stu-id="48fb7-333">Object</span></span>|<span data-ttu-id="48fb7-334">Nagłówki żądania http.</span><span class="sxs-lookup"><span data-stu-id="48fb7-334">The headers of the http request.</span></span>|  
|<span data-ttu-id="48fb7-335">Treści</span><span class="sxs-lookup"><span data-stu-id="48fb7-335">body</span></span>|<span data-ttu-id="48fb7-336">Obiekt</span><span class="sxs-lookup"><span data-stu-id="48fb7-336">Object</span></span>|<span data-ttu-id="48fb7-337">Treść żądania http.</span><span class="sxs-lookup"><span data-stu-id="48fb7-337">The body of the http request.</span></span>|  

<span data-ttu-id="48fb7-338">Można określić limity akcji elementu webhook w taki sam sposób jak [limity asynchroniczne HTTP](#asynchronous-limits).</span><span class="sxs-lookup"><span data-stu-id="48fb7-338">Limits on a webhook action can be specified in the same manner as [HTTP Asynchronous Limits](#asynchronous-limits).</span></span>
  

## <a name="conditions"></a><span data-ttu-id="48fb7-339">Warunki</span><span class="sxs-lookup"><span data-stu-id="48fb7-339">Conditions</span></span>  

<span data-ttu-id="48fb7-340">Dla dowolnego wyzwalacza można użyć co najmniej jednego warunku można określić, czy przepływ pracy, należy uruchomić lub nie.</span><span class="sxs-lookup"><span data-stu-id="48fb7-340">For any trigger, you can use one or more conditions to determine whether the workflow should run or not.</span></span> <span data-ttu-id="48fb7-341">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="48fb7-341">For example:</span></span>  

```json
"dailyReport" : {
    "type": "recurrence",
    "conditions": [ {
        "expression": "@parameters('sendReports')"
    } ],
    "recurrence": {
        "frequency": "Day",
        "interval": "1"
    }
}
```

<span data-ttu-id="48fb7-342">W takim przypadku tylko wyzwalacze raportu podczas przepływu pracy `sendReports` parametr ma wartość true.</span><span class="sxs-lookup"><span data-stu-id="48fb7-342">In this case, the report only triggers while the workflow's `sendReports` parameter is set to true.</span></span> <span data-ttu-id="48fb7-343">Na koniec warunków może odwoływać się kod stanu wyzwalacza.</span><span class="sxs-lookup"><span data-stu-id="48fb7-343">Finally, conditions may reference the status code of the trigger.</span></span> <span data-ttu-id="48fb7-344">Na przykład należy można rozpocząć wyłączyć przepływ pracy tylko w przypadku witryny sieci Web zwraca kod stanu 500, w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="48fb7-344">For example, you could kick off a workflow only when your website returns a status code 500, as follows:</span></span>
  
```  
"conditions": [  
        {  
          "expression": "@equals(triggers().code, 'InternalServerError')"  
        }  
      ]  
```  
  
> [!NOTE]  
> <span data-ttu-id="48fb7-345">Jeśli dowolne wyrażenie odwołuje się kod stanu wyzwalacza \(w żaden sposób\), domyślne zachowanie \(wyzwalacza tylko na 200 \(OK\) \) zostanie zastąpiony.</span><span class="sxs-lookup"><span data-stu-id="48fb7-345">When any expression references the status code of the trigger \(in any way\), the default behavior \(trigger only on 200 \(OK\)\) is replaced.</span></span> <span data-ttu-id="48fb7-346">Na przykład, jeśli chcesz wyzwolić na kod stanu 201 i kodem stanu 200, użytkownik musi zawierać: `@or(equals(triggers().code, 200),equals(triggers().code,201))` jako warunek.</span><span class="sxs-lookup"><span data-stu-id="48fb7-346">For example, if you want to trigger on both status code 200 and status code 201, you have to include: `@or(equals(triggers().code, 200),equals(triggers().code,201))` as your condition.</span></span>  
  
## <a name="start-multiple-runs-for-a-request"></a><span data-ttu-id="48fb7-347">Uruchom wielu uruchomień dla żądania</span><span class="sxs-lookup"><span data-stu-id="48fb7-347">Start multiple runs for a request</span></span>

<span data-ttu-id="48fb7-348">Aby rozpocząć poza wielu uruchomień dla pojedynczego żądania `splitOn` jest przydatne, na przykład, gdy chcesz przeprowadzać sondowanie punktu końcowego, który może mieć wiele nowych elementów między interwałami sondowania.</span><span class="sxs-lookup"><span data-stu-id="48fb7-348">To kick off multiple runs for a single request, `splitOn` is useful, for example, when you want to poll an endpoint that can have multiple new items between polling intervals.</span></span>
  
<span data-ttu-id="48fb7-349">Z `splitOn`, określ właściwość ładunku odpowiedzi, który zawiera tablicę elementów, z których każdy ma być używany do uruchamiania wykonywania wyzwalacza.</span><span class="sxs-lookup"><span data-stu-id="48fb7-349">With `splitOn`, you specify the property inside the response payload that contains the array of items, each of which you want to use to start a run of the trigger.</span></span> <span data-ttu-id="48fb7-350">Załóżmy na przykład, że masz interfejs API, który zwraca następującą odpowiedź:</span><span class="sxs-lookup"><span data-stu-id="48fb7-350">For example, imagine you have an API that returns the following response:</span></span>  
  
```json
{
    "Status" : "success",
    "Rows" : [
        {  
            "id" : 938109380,
            "name" : "mycoolrow"
        },
        {
            "id" : 938109381,
            "name" : "another row"
        }
    ]
}
```
  
<span data-ttu-id="48fb7-351">Aplikację logiki musi tylko zawartość wierszy, można utworzyć wyzwalacz tak jak ten przykład:</span><span class="sxs-lookup"><span data-stu-id="48fb7-351">Your logic app only needs the Rows content, so you can construct your trigger like this example:</span></span>  
  
```json
"mysplitter" : {
    "type" : "http",
    "recurrence": {
        "frequency": "Minute",
        "interval": "1"
    },
    "intputs" : {
        "uri" : "https://mydomain.com/myAPI",
        "method" : "GET"
    },
    "splitOn" : "@triggerBody()?.Rows"
}
```
  
<span data-ttu-id="48fb7-352">Następnie w definicji przepływu pracy `@triggerBody().name` zwraca `mycoolrow` dla przy pierwszym uruchomieniu i `another row` dla drugiego przebiegu.</span><span class="sxs-lookup"><span data-stu-id="48fb7-352">Then, in the workflow definition, `@triggerBody().name` returns `mycoolrow` for the first run, and `another row` for the second run.</span></span> <span data-ttu-id="48fb7-353">Wygląd danych wyjściowych wyzwalacz tak jak ten przykład:</span><span class="sxs-lookup"><span data-stu-id="48fb7-353">The trigger outputs look like this example:</span></span>  
  
```json
{
    "body" : {
        "id" : 938109381,
        "name" : "another row"
    }
}
```

<span data-ttu-id="48fb7-354">Dlatego jeśli używasz `SplitOn`, nie można pobrać właściwości, które są poza tablicy, w tym przypadku `Status` pola.</span><span class="sxs-lookup"><span data-stu-id="48fb7-354">So if you use `SplitOn`, you can't get the properties that are outside the array, in this case, the `Status` field.</span></span>  
  
> [!NOTE]  
> <span data-ttu-id="48fb7-355">W tym przykładzie używamy `?` operatora, aby można było uniknąć awarii, jeśli `Rows` nie ma właściwości.</span><span class="sxs-lookup"><span data-stu-id="48fb7-355">In this example, we use the `?` operator to be able to avoid a failure if the `Rows` property is not present.</span></span> 
  
## <a name="single-run-instance"></a><span data-ttu-id="48fb7-356">Pojedyncze wystąpienie wykonywania</span><span class="sxs-lookup"><span data-stu-id="48fb7-356">Single run instance</span></span>

<span data-ttu-id="48fb7-357">Można skonfigurować wyzwalacze, które mają właściwość cyklu uruchomienie tylko, jeśli wszystkie aktywnej przebiegi została ukończona.</span><span class="sxs-lookup"><span data-stu-id="48fb7-357">You can configure triggers that have a recurrence property to only fire if all active runs have completed.</span></span> <span data-ttu-id="48fb7-358">W przypadku podczas uruchamiania w trakcie zaplanowanego cyklu wyzwalacza pomija i czeka, aż do następnego interwał cyklu zaplanowane, aby ponownie sprawdzić.</span><span class="sxs-lookup"><span data-stu-id="48fb7-358">If a scheduled recurrence occurs while there is an in-progress run, the trigger skips and waits until the next scheduled recurrence interval to check again.</span></span>

<span data-ttu-id="48fb7-359">Można to ustawienie można skonfigurować za pomocą opcji operacji:</span><span class="sxs-lookup"><span data-stu-id="48fb7-359">You can configure this setting through the operation options:</span></span>

```json
"triggers": {
    "mytrigger": {
        "type": "http",
        "inputs": { ... },
        "recurrence": { ... },
        "operationOptions": "singleInstance"
    }
}
```

## <a name="types-and-inputs"></a><span data-ttu-id="48fb7-360">Typy i dane wejściowe</span><span class="sxs-lookup"><span data-stu-id="48fb7-360">Types and inputs</span></span>  

<span data-ttu-id="48fb7-361">Istnieje wiele typów działań, każde z nich unikatowe zachowanie.</span><span class="sxs-lookup"><span data-stu-id="48fb7-361">There are many types of actions, each with unique behavior.</span></span> <span data-ttu-id="48fb7-362">Akcje kolekcji może zawierać wielu akcji w obrębie samego.</span><span class="sxs-lookup"><span data-stu-id="48fb7-362">Collection actions may contain many other actions within itself.</span></span>

### <a name="standard-actions"></a><span data-ttu-id="48fb7-363">Działania standardowe</span><span class="sxs-lookup"><span data-stu-id="48fb7-363">Standard actions</span></span>  

-   <span data-ttu-id="48fb7-364">**HTTP** ta akcja wymaga punktu końcowego HTTP sieci web.</span><span class="sxs-lookup"><span data-stu-id="48fb7-364">**HTTP** This action calls an HTTP web endpoint.</span></span>  
  
-   <span data-ttu-id="48fb7-365">**ApiConnection** \- ta akcja działa jak akcja HTTP, ale korzysta z interfejsów API zarządzany przez firmę Microsoft.</span><span class="sxs-lookup"><span data-stu-id="48fb7-365">**ApiConnection** \- This action behaves like the HTTP action, but uses the Microsoft-managed APIs.</span></span>  
  
-   <span data-ttu-id="48fb7-366">**ApiConnectionWebhook** \- jak HTTPWebhook, ale używa interfejsów API zarządzany przez firmę Microsoft.</span><span class="sxs-lookup"><span data-stu-id="48fb7-366">**ApiConnectionWebhook** \- Like HTTPWebhook, but uses the Microsoft-managed APIs.</span></span>  
  
-   <span data-ttu-id="48fb7-367">**Odpowiedź** \- tej akcji określa odpowiedzi dla połączenia przychodzącego.</span><span class="sxs-lookup"><span data-stu-id="48fb7-367">**Response** \- This action defines a response for an incoming call.</span></span>  
  
-   <span data-ttu-id="48fb7-368">**Poczekaj** \- ta akcja proste czeka stałą lub określonego czasu.</span><span class="sxs-lookup"><span data-stu-id="48fb7-368">**Wait** \- This simple action waits a fixed amount of time or until a specific time.</span></span>  
  
-   <span data-ttu-id="48fb7-369">**Przepływ pracy** \- tej akcji reprezentuje zagnieżdżony przepływ pracy.</span><span class="sxs-lookup"><span data-stu-id="48fb7-369">**Workflow** \- This action represents a nested workflow.</span></span>  

-   <span data-ttu-id="48fb7-370">**Funkcja** \- tej akcji reprezentuje funkcję platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="48fb7-370">**Function** \- This action represents an Azure Function.</span></span>

### <a name="collection-actions"></a><span data-ttu-id="48fb7-371">Akcje kolekcji</span><span class="sxs-lookup"><span data-stu-id="48fb7-371">Collection actions</span></span>

-   <span data-ttu-id="48fb7-372">**Zakres** \- ta akcja jest logiczne grupowanie innych działań.</span><span class="sxs-lookup"><span data-stu-id="48fb7-372">**Scope** \- This action is a logical grouping of other actions.</span></span>

-   <span data-ttu-id="48fb7-373">**Warunek** \- ta akcja oblicza wyrażenie i wykonuje odpowiednie gałęzi wynik.</span><span class="sxs-lookup"><span data-stu-id="48fb7-373">**Condition** \- This action evaluates an expression and executes the corresponding result branch.</span></span>

-   <span data-ttu-id="48fb7-374">**Instrukcja ForEach** \- ta akcja pętli iteruje tablicy i wykonuje akcje wewnętrzny dla każdego elementu.</span><span class="sxs-lookup"><span data-stu-id="48fb7-374">**ForEach** \- This looping action iterates through an array and performs inner actions for each item.</span></span>

-   <span data-ttu-id="48fb7-375">**Dopóki** \- ta akcja pętli wykonuje działania wewnętrzne, dopóki warunek wyników do wartości true.</span><span class="sxs-lookup"><span data-stu-id="48fb7-375">**Until** \- This looping action executes inner actions until a condition results to true.</span></span>
  
<span data-ttu-id="48fb7-376">Każdy typ działania ma inny zestaw **dane wejściowe** definiującą zachowanie akcji.</span><span class="sxs-lookup"><span data-stu-id="48fb7-376">Each type of action has a different set of **inputs** that define an action's behavior.</span></span>  
  
## <a name="http-action"></a><span data-ttu-id="48fb7-377">Akcja HTTP</span><span class="sxs-lookup"><span data-stu-id="48fb7-377">HTTP action</span></span>  

<span data-ttu-id="48fb7-378">Akcje HTTP wywołać określony punkt końcowy i sprawdź odpowiedzi, aby określić, czy należy uruchomić przepływ pracy.</span><span class="sxs-lookup"><span data-stu-id="48fb7-378">HTTP actions call a specified endpoint and check the response to determine whether the workflow should run.</span></span> <span data-ttu-id="48fb7-379">**Dane wejściowe** obiekt ma zestaw parametrów wymaganych do utworzenia połączenia HTTP:</span><span class="sxs-lookup"><span data-stu-id="48fb7-379">The **inputs** object takes the set of parameters required to construct the HTTP call:</span></span>  
  
|<span data-ttu-id="48fb7-380">Nazwa elementu</span><span class="sxs-lookup"><span data-stu-id="48fb7-380">Element name</span></span>|<span data-ttu-id="48fb7-381">Wymagane</span><span class="sxs-lookup"><span data-stu-id="48fb7-381">Required</span></span>|<span data-ttu-id="48fb7-382">Typ</span><span class="sxs-lookup"><span data-stu-id="48fb7-382">Type</span></span>|<span data-ttu-id="48fb7-383">Opis</span><span class="sxs-lookup"><span data-stu-id="48fb7-383">Description</span></span>|  
|----------------|------------|--------|---------------|  
|<span data-ttu-id="48fb7-384">— Metoda</span><span class="sxs-lookup"><span data-stu-id="48fb7-384">method</span></span>|<span data-ttu-id="48fb7-385">Tak</span><span class="sxs-lookup"><span data-stu-id="48fb7-385">Yes</span></span>|<span data-ttu-id="48fb7-386">Ciąg</span><span class="sxs-lookup"><span data-stu-id="48fb7-386">String</span></span>|<span data-ttu-id="48fb7-387">Może być jedną z następujących metod HTTP: **UZYSKAĆ**, **POST**, **PUT**, **usunąć**, **poprawka**, lub  **HEAD**</span><span class="sxs-lookup"><span data-stu-id="48fb7-387">Can be one of the following HTTP methods: **GET**, **POST**, **PUT**, **DELETE**, **PATCH**, or **HEAD**</span></span>|  
|<span data-ttu-id="48fb7-388">Identyfikator URI</span><span class="sxs-lookup"><span data-stu-id="48fb7-388">uri</span></span>|<span data-ttu-id="48fb7-389">Tak</span><span class="sxs-lookup"><span data-stu-id="48fb7-389">Yes</span></span>|<span data-ttu-id="48fb7-390">Ciąg</span><span class="sxs-lookup"><span data-stu-id="48fb7-390">String</span></span>|<span data-ttu-id="48fb7-391">Końcowy http lub https, która jest wywoływana.</span><span class="sxs-lookup"><span data-stu-id="48fb7-391">The http or https endpoint that is called.</span></span> <span data-ttu-id="48fb7-392">Maksymalna długość wynosi 2 kilobajtów.</span><span class="sxs-lookup"><span data-stu-id="48fb7-392">Maximum length is 2 kilobytes.</span></span>|  
|<span data-ttu-id="48fb7-393">— zapytania</span><span class="sxs-lookup"><span data-stu-id="48fb7-393">queries</span></span>|<span data-ttu-id="48fb7-394">Nie</span><span class="sxs-lookup"><span data-stu-id="48fb7-394">No</span></span>|<span data-ttu-id="48fb7-395">Obiekt</span><span class="sxs-lookup"><span data-stu-id="48fb7-395">Object</span></span>|<span data-ttu-id="48fb7-396">Reprezentuje parametry zapytania, aby dodać do adresu URL.</span><span class="sxs-lookup"><span data-stu-id="48fb7-396">Represents the query parameters to add to the URL.</span></span> <span data-ttu-id="48fb7-397">Na przykład `"queries" : { "api-version": "2015-02-01" }` dodaje `?api-version=2015-02-01` do adresu URL.</span><span class="sxs-lookup"><span data-stu-id="48fb7-397">For example, `"queries" : { "api-version": "2015-02-01" }` adds `?api-version=2015-02-01` to the URL.</span></span>|  
|<span data-ttu-id="48fb7-398">Nagłówki</span><span class="sxs-lookup"><span data-stu-id="48fb7-398">headers</span></span>|<span data-ttu-id="48fb7-399">Nie</span><span class="sxs-lookup"><span data-stu-id="48fb7-399">No</span></span>|<span data-ttu-id="48fb7-400">Obiekt</span><span class="sxs-lookup"><span data-stu-id="48fb7-400">Object</span></span>|<span data-ttu-id="48fb7-401">Reprezentuje listę nagłówków, które są wysyłane do żądania.</span><span class="sxs-lookup"><span data-stu-id="48fb7-401">Represents each of the headers that is sent to the request.</span></span> <span data-ttu-id="48fb7-402">Na przykład, aby ustawić język i typ żądania:`"headers" : { "Accept-Language": "en-us",  "Content-Type": "application/json" }`</span><span class="sxs-lookup"><span data-stu-id="48fb7-402">For example, to set the language and type on a request: `"headers" : { "Accept-Language": "en-us",  "Content-Type": "application/json" }`</span></span>|  
|<span data-ttu-id="48fb7-403">Treści</span><span class="sxs-lookup"><span data-stu-id="48fb7-403">body</span></span>|<span data-ttu-id="48fb7-404">Nie</span><span class="sxs-lookup"><span data-stu-id="48fb7-404">No</span></span>|<span data-ttu-id="48fb7-405">Obiekt</span><span class="sxs-lookup"><span data-stu-id="48fb7-405">Object</span></span>|<span data-ttu-id="48fb7-406">Reprezentuje ładunek, które są wysyłane do punktu końcowego.</span><span class="sxs-lookup"><span data-stu-id="48fb7-406">Represents the payload that is sent to the endpoint.</span></span>|  
|<span data-ttu-id="48fb7-407">retryPolicy</span><span class="sxs-lookup"><span data-stu-id="48fb7-407">retryPolicy</span></span>|<span data-ttu-id="48fb7-408">Nie</span><span class="sxs-lookup"><span data-stu-id="48fb7-408">No</span></span>|<span data-ttu-id="48fb7-409">Obiekt</span><span class="sxs-lookup"><span data-stu-id="48fb7-409">Object</span></span>|<span data-ttu-id="48fb7-410">Pozwala dostosować zachowanie ponownych prób dla 4xx lub 5xx błędów.</span><span class="sxs-lookup"><span data-stu-id="48fb7-410">Lets you customize the retry behavior for 4xx or 5xx errors.</span></span>|  
|<span data-ttu-id="48fb7-411">operationsOptions</span><span class="sxs-lookup"><span data-stu-id="48fb7-411">operationsOptions</span></span>|<span data-ttu-id="48fb7-412">Nie</span><span class="sxs-lookup"><span data-stu-id="48fb7-412">No</span></span>|<span data-ttu-id="48fb7-413">Ciąg</span><span class="sxs-lookup"><span data-stu-id="48fb7-413">String</span></span>|<span data-ttu-id="48fb7-414">Definiuje zestaw specjalnego zachowania do zastąpienia.</span><span class="sxs-lookup"><span data-stu-id="48fb7-414">Defines the set of special behaviors to override.</span></span>|  
|<span data-ttu-id="48fb7-415">Uwierzytelnianie</span><span class="sxs-lookup"><span data-stu-id="48fb7-415">authentication</span></span>|<span data-ttu-id="48fb7-416">Nie</span><span class="sxs-lookup"><span data-stu-id="48fb7-416">No</span></span>|<span data-ttu-id="48fb7-417">Obiekt</span><span class="sxs-lookup"><span data-stu-id="48fb7-417">Object</span></span>|<span data-ttu-id="48fb7-418">Reprezentuje metodę uwierzytelniania żądania.</span><span class="sxs-lookup"><span data-stu-id="48fb7-418">Represents the method that the request should be authenticated.</span></span> <span data-ttu-id="48fb7-419">Aby uzyskać więcej informacji na ten obiekt, zobacz [uwierzytelniania połączeń wychodzących harmonogramu](https://docs.microsoft.com/azure/scheduler/scheduler-outbound-authentication).</span><span class="sxs-lookup"><span data-stu-id="48fb7-419">For details on this object, see [Scheduler Outbound Authentication](https://docs.microsoft.com/azure/scheduler/scheduler-outbound-authentication).</span></span> <span data-ttu-id="48fb7-420">Poza harmonogramem, jest jedna właściwość więcej obsługiwanych: `authority`.</span><span class="sxs-lookup"><span data-stu-id="48fb7-420">Beyond scheduler, there is one more supported property: `authority`.</span></span> <span data-ttu-id="48fb7-421">Domyślnie jest to `https://login.windows.net` gdy nie jest określony, ale możesz użyć innych grup odbiorców, takich jak`https://login.windows\-ppe.net`</span><span class="sxs-lookup"><span data-stu-id="48fb7-421">By default, this is `https://login.windows.net` when not specified, but you can use a different audience like `https://login.windows\-ppe.net`</span></span>|  
  
<span data-ttu-id="48fb7-422">Akcje HTTP \(i połączenie z interfejsem API\) Obsługa akcji ponów zasad.</span><span class="sxs-lookup"><span data-stu-id="48fb7-422">HTTP actions \(and API Connection\) actions support retry policies.</span></span> <span data-ttu-id="48fb7-423">Zasady ponawiania dotyczy sporadycznych błędów jest określony jako kodów stanu HTTP 408 429 i 5xx, oprócz wszelkie wyjątki łączności.</span><span class="sxs-lookup"><span data-stu-id="48fb7-423">A retry policy applies to intermittent failures, characterized as HTTP status codes 408, 429, and 5xx, in addition to any connectivity exceptions.</span></span> <span data-ttu-id="48fb7-424">Ta zasada jest opisana przy użyciu *retryPolicy* obiekt zdefiniowany w sposób pokazany poniżej:</span><span class="sxs-lookup"><span data-stu-id="48fb7-424">This policy is described using the *retryPolicy* object defined as shown here:</span></span>
  
```json
"retryPolicy" : {
    "type": "<type-of-retry-policy>",
    "interval": <retry-interval>,
    "count": <number-of-retry-attempts>
}
```
  
<span data-ttu-id="48fb7-425">Interwał ponawiania prób jest określona w formacie ISO 8601.</span><span class="sxs-lookup"><span data-stu-id="48fb7-425">The retry interval is specified in the ISO 8601 format.</span></span> <span data-ttu-id="48fb7-426">Ten interwał ma wartości domyślnej i co najmniej 20 sekund, podczas gdy wartość maksymalna to jedna godzina.</span><span class="sxs-lookup"><span data-stu-id="48fb7-426">This interval has a default and minimum value of 20 seconds, while the maximum value is one hour.</span></span> <span data-ttu-id="48fb7-427">Domyślne i maksymalnej liczby ponownych prób odpowiada czterem godzinom.</span><span class="sxs-lookup"><span data-stu-id="48fb7-427">The default and maximum retry count is four hours.</span></span> <span data-ttu-id="48fb7-428">Jeśli nie określono definicji zasad ponawiania, `fixed` strategii jest używany z domyślnej wartości interwału i liczba ponownych prób.</span><span class="sxs-lookup"><span data-stu-id="48fb7-428">If the retry policy definition is not specified, a `fixed` strategy is used with default retry count and interval values.</span></span> <span data-ttu-id="48fb7-429">Aby wyłączyć zasady ponawiania, ustaw jej typ `None`.</span><span class="sxs-lookup"><span data-stu-id="48fb7-429">To disable the retry policy, set its type to `None`.</span></span>  
  
<span data-ttu-id="48fb7-430">Na przykład następujące działania ponowne próby pobierania najnowsze dwa razy, jeśli występują sporadyczne awarie, dla wszystkich trzech wykonaniami, z 30-sekundowe opóźnienie między kolejnymi próbami:</span><span class="sxs-lookup"><span data-stu-id="48fb7-430">For example, the following action retries fetching the latest news two times, if there are intermittent failures, for a total of three executions, with a 30-second delay between each attempt:</span></span>  
  
```json
"latestNews" : {
    "type": "http",
    "inputs": {
        "method": "GET",
        "uri": "https://mynews.example.com/latest",
        "retryPolicy" : {
            "type": "fixed",
            "interval": "PT30S",
            "count": 2
        }
    }
}
```
### <a name="asynchronous-patterns"></a><span data-ttu-id="48fb7-431">Asynchroniczne wzorce</span><span class="sxs-lookup"><span data-stu-id="48fb7-431">Asynchronous patterns</span></span>

<span data-ttu-id="48fb7-432">Domyślnie wszystkie działania oparte na protokole HTTP obsługuje wzorzec standardowych operacji asynchronicznej.</span><span class="sxs-lookup"><span data-stu-id="48fb7-432">By default, all HTTP-based actions support the standard asynchronous operation pattern.</span></span> <span data-ttu-id="48fb7-433">Dlatego w przypadku zdalnego serwera wskazuje, czy żądanie jest zaakceptowano do przetwarzania z 202 \(zaakceptowane\) odpowiedzi, aparat Logic Apps śledzi sondowania adres URL określony w odpowiedzi nagłówek lokalizacji do momentu osiągnięcia terminali stanu \(bez\-202 odpowiedzi\).</span><span class="sxs-lookup"><span data-stu-id="48fb7-433">So if the remote server indicates that the request is accepted for processing with a 202 \(Accepted\) response, the Logic Apps engine keeps polling the URL specified in the response's location header until reaching a terminal state \(a non\-202 response\).</span></span>  
  
<span data-ttu-id="48fb7-434">Aby wyłączyć asynchroniczne zachowanie opisany powyżej, ustaw `DisableAsyncPattern` opcji w danych wejściowych działania.</span><span class="sxs-lookup"><span data-stu-id="48fb7-434">To disable the asynchronous behavior previously described, set a `DisableAsyncPattern` option in the action inputs.</span></span> <span data-ttu-id="48fb7-435">W takim przypadku dane wyjściowe działania jest oparty na początkowej 202 odpowiedzi z serwera.</span><span class="sxs-lookup"><span data-stu-id="48fb7-435">In this case, the output of the action is based on the initial 202 response from the server.</span></span>  
  
```json
"invokeLongRunningOperation" : {
    "type": "http",
    "inputs": {
        "method": "POST",
        "uri": "https://host.example.com/resources"
    },
    "operationOptions": "DisableAsyncPattern"
}
```

#### <a name="asynchronous-limits"></a><span data-ttu-id="48fb7-436">Limity asynchroniczne</span><span class="sxs-lookup"><span data-stu-id="48fb7-436">Asynchronous Limits</span></span>

<span data-ttu-id="48fb7-437">Asynchroniczny wzorzec może być ograniczone w jego czas trwania na określonym interwale.</span><span class="sxs-lookup"><span data-stu-id="48fb7-437">An asynchronous pattern can be limited in its duration to a specific time interval.</span></span>  <span data-ttu-id="48fb7-438">Jeśli interwał czasu musi upłynąć bez osiągnięcia terminali stanu, zostaną oznaczone jako stan akcji `Cancelled` przy użyciu kodu `ActionTimedOut`.</span><span class="sxs-lookup"><span data-stu-id="48fb7-438">If the time interval elapses without reaching a terminal state, the status of the action will be marked `Cancelled` with a code of `ActionTimedOut`.</span></span>  <span data-ttu-id="48fb7-439">Limit czasu został określony w formacie ISO 8601.</span><span class="sxs-lookup"><span data-stu-id="48fb7-439">The limit timeout is specified in ISO 8601 format.</span></span>  <span data-ttu-id="48fb7-440">Limity można określić przy użyciu następującej składni:</span><span class="sxs-lookup"><span data-stu-id="48fb7-440">Limits can be specified with the following syntax:</span></span>

``` json
"<action-name>": {
    "type": "workflow|webhook|http|apiconnectionwebhook|apiconnection",
    "inputs": { },
    "limit": {
        "timeout": "PT10S"
    }
}
```
  
## <a name="api-connection"></a><span data-ttu-id="48fb7-441">Połączenie z interfejsem API</span><span class="sxs-lookup"><span data-stu-id="48fb7-441">API Connection</span></span>  

<span data-ttu-id="48fb7-442">Połączenie z interfejsem API jest akcja, która odwołuje się do łącznika zarządzany przez firmę Microsoft.</span><span class="sxs-lookup"><span data-stu-id="48fb7-442">API Connection is an action that references a Microsoft-managed connector.</span></span>
<span data-ttu-id="48fb7-443">Ta akcja wymaga odwołania do prawidłowe połączenie, a informacje na temat interfejsu API i parametrów wymaganych.</span><span class="sxs-lookup"><span data-stu-id="48fb7-443">This action requires a reference to a valid connection, and information on the API and parameters required.</span></span>

|<span data-ttu-id="48fb7-444">Nazwa elementu</span><span class="sxs-lookup"><span data-stu-id="48fb7-444">Element name</span></span>|<span data-ttu-id="48fb7-445">Wymagane</span><span class="sxs-lookup"><span data-stu-id="48fb7-445">Required</span></span>|<span data-ttu-id="48fb7-446">Typ</span><span class="sxs-lookup"><span data-stu-id="48fb7-446">Type</span></span>|<span data-ttu-id="48fb7-447">Opis</span><span class="sxs-lookup"><span data-stu-id="48fb7-447">Description</span></span>|  
|----------------|------------|--------|---------------|  
|<span data-ttu-id="48fb7-448">Host</span><span class="sxs-lookup"><span data-stu-id="48fb7-448">host</span></span>|<span data-ttu-id="48fb7-449">Tak</span><span class="sxs-lookup"><span data-stu-id="48fb7-449">Yes</span></span>|<span data-ttu-id="48fb7-450">Obiekt</span><span class="sxs-lookup"><span data-stu-id="48fb7-450">Object</span></span>|<span data-ttu-id="48fb7-451">Reprezentuje informacje łącznika, takie jak runtimeUrl i odwołania do obiektu połączenia</span><span class="sxs-lookup"><span data-stu-id="48fb7-451">Represents the connector information such as the runtimeUrl and reference to the connection object</span></span>|
|<span data-ttu-id="48fb7-452">— Metoda</span><span class="sxs-lookup"><span data-stu-id="48fb7-452">method</span></span>|<span data-ttu-id="48fb7-453">Tak</span><span class="sxs-lookup"><span data-stu-id="48fb7-453">Yes</span></span>|<span data-ttu-id="48fb7-454">Ciąg</span><span class="sxs-lookup"><span data-stu-id="48fb7-454">String</span></span>|<span data-ttu-id="48fb7-455">Może być jedną z następujących metod HTTP: **UZYSKAĆ**, **POST**, **PUT**, **usunąć**, **poprawka**, lub  **HEAD**</span><span class="sxs-lookup"><span data-stu-id="48fb7-455">Can be one of the following HTTP methods: **GET**, **POST**, **PUT**, **DELETE**, **PATCH**, or **HEAD**</span></span>|  
|<span data-ttu-id="48fb7-456">Ścieżka</span><span class="sxs-lookup"><span data-stu-id="48fb7-456">path</span></span>|<span data-ttu-id="48fb7-457">Tak</span><span class="sxs-lookup"><span data-stu-id="48fb7-457">Yes</span></span>|<span data-ttu-id="48fb7-458">Ciąg</span><span class="sxs-lookup"><span data-stu-id="48fb7-458">String</span></span>|<span data-ttu-id="48fb7-459">Ścieżka operacji interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="48fb7-459">The path of the API operation.</span></span>|  
|<span data-ttu-id="48fb7-460">— zapytania</span><span class="sxs-lookup"><span data-stu-id="48fb7-460">queries</span></span>|<span data-ttu-id="48fb7-461">Nie</span><span class="sxs-lookup"><span data-stu-id="48fb7-461">No</span></span>|<span data-ttu-id="48fb7-462">Obiekt</span><span class="sxs-lookup"><span data-stu-id="48fb7-462">Object</span></span>|<span data-ttu-id="48fb7-463">Reprezentuje parametry zapytania, aby dodać do adresu URL.</span><span class="sxs-lookup"><span data-stu-id="48fb7-463">Represents the query parameters to add to the URL.</span></span> <span data-ttu-id="48fb7-464">Na przykład `"queries" : { "api-version": "2015-02-01" }` dodaje `?api-version=2015-02-01` do adresu URL.</span><span class="sxs-lookup"><span data-stu-id="48fb7-464">For example, `"queries" : { "api-version": "2015-02-01" }` adds `?api-version=2015-02-01` to the URL.</span></span>|  
|<span data-ttu-id="48fb7-465">Nagłówki</span><span class="sxs-lookup"><span data-stu-id="48fb7-465">headers</span></span>|<span data-ttu-id="48fb7-466">Nie</span><span class="sxs-lookup"><span data-stu-id="48fb7-466">No</span></span>|<span data-ttu-id="48fb7-467">Obiekt</span><span class="sxs-lookup"><span data-stu-id="48fb7-467">Object</span></span>|<span data-ttu-id="48fb7-468">Reprezentuje listę nagłówków, które są wysyłane do żądania.</span><span class="sxs-lookup"><span data-stu-id="48fb7-468">Represents each of the headers that is sent to the request.</span></span> <span data-ttu-id="48fb7-469">Na przykład, aby ustawić język i typ żądania:`"headers" : { "Accept-Language": "en-us",  "Content-Type": "application/json" }`</span><span class="sxs-lookup"><span data-stu-id="48fb7-469">For example, to set the language and type on a request: `"headers" : { "Accept-Language": "en-us",  "Content-Type": "application/json" }`</span></span>|  
|<span data-ttu-id="48fb7-470">Treści</span><span class="sxs-lookup"><span data-stu-id="48fb7-470">body</span></span>|<span data-ttu-id="48fb7-471">Nie</span><span class="sxs-lookup"><span data-stu-id="48fb7-471">No</span></span>|<span data-ttu-id="48fb7-472">Obiekt</span><span class="sxs-lookup"><span data-stu-id="48fb7-472">Object</span></span>|<span data-ttu-id="48fb7-473">Reprezentuje ładunek, które są wysyłane do punktu końcowego.</span><span class="sxs-lookup"><span data-stu-id="48fb7-473">Represents the payload that is sent to the endpoint.</span></span>|  
|<span data-ttu-id="48fb7-474">retryPolicy</span><span class="sxs-lookup"><span data-stu-id="48fb7-474">retryPolicy</span></span>|<span data-ttu-id="48fb7-475">Nie</span><span class="sxs-lookup"><span data-stu-id="48fb7-475">No</span></span>|<span data-ttu-id="48fb7-476">Obiekt</span><span class="sxs-lookup"><span data-stu-id="48fb7-476">Object</span></span>|<span data-ttu-id="48fb7-477">Pozwala dostosować zachowanie ponownych prób dla 4xx lub 5xx błędów.</span><span class="sxs-lookup"><span data-stu-id="48fb7-477">Lets you customize the retry behavior for 4xx or 5xx errors.</span></span>|  
|<span data-ttu-id="48fb7-478">operationsOptions</span><span class="sxs-lookup"><span data-stu-id="48fb7-478">operationsOptions</span></span>|<span data-ttu-id="48fb7-479">Nie</span><span class="sxs-lookup"><span data-stu-id="48fb7-479">No</span></span>|<span data-ttu-id="48fb7-480">Ciąg</span><span class="sxs-lookup"><span data-stu-id="48fb7-480">String</span></span>|<span data-ttu-id="48fb7-481">Definiuje zestaw specjalnego zachowania do zastąpienia.</span><span class="sxs-lookup"><span data-stu-id="48fb7-481">Defines the set of special behaviors to override.</span></span>|  

```json
"Send_Email": {
    "type": "apiconnection",
    "inputs": {
        "host": {
            "api": {
                "runtimeUrl": "https://logic-apis-df.azure-apim.net/apim/office365"
            },
            "connection": {
                "name": "@parameters('$connections')['office365']['connectionId']"
            }
        },
        "method": "post",
        "body": {
            "Subject": "New Tweet from @{triggerBody()['TweetedBy']}",
            "Body": "@{triggerBody()['TweetText']}",
            "To": "me@example.com"
        },
        "path": "/Mail"
    },
    "runAfter": {}
    }
```

## <a name="api-connection-webhook-action"></a><span data-ttu-id="48fb7-482">Połączenie z interfejsem API akcji elementu webhook</span><span class="sxs-lookup"><span data-stu-id="48fb7-482">API Connection webhook action</span></span>

```json
"Send_approval_email": {
    "type": "apiconnectionwebhook",
    "inputs": {
        "host": {
            "api": {
                "runtimeUrl": "https://logic-apis-df.azure-apim.net/apim/office365"
            },
            "connection": {
                "name": "@parameters('$connections')['office365']['connectionId']"
            }
        },
        "body": {
            "Message": {
                "Subject": "Approval Request",
                "Options": "Approve, Reject",
                "Importance": "Normal",
                "To": "me@email.com"
            }
        },
        "path": "/approvalmail",
        "authentication": "@parameters('$authentication')"
    },
    "runAfter": {}
}
```

<span data-ttu-id="48fb7-483">Można określić limity akcji elementu webhook w taki sam sposób jak [limity asynchroniczne HTTP](#asynchronous-limits).</span><span class="sxs-lookup"><span data-stu-id="48fb7-483">Limits on a webhook action can be specified in the same manner as [HTTP Asynchronous Limits](#asynchronous-limits).</span></span>
  
## <a name="response-action"></a><span data-ttu-id="48fb7-484">Akcja odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="48fb7-484">Response action</span></span>  

<span data-ttu-id="48fb7-485">Ten typ akcji zawiera ładunek całej odpowiedzi z żądania HTTP i obejmuje statusCode, treści i nagłówków:</span><span class="sxs-lookup"><span data-stu-id="48fb7-485">This action type contains the entire response payload from an HTTP request and includes a statusCode, body, and headers:</span></span>  
  
```json
"myresponse" : {
    "type" : "response",
    "inputs" : {
        "statusCode" : 200,
        "body" : {
            "contentFieldOne" : "value100",
            "anotherField" : 10.001
        },
        "headers" : {
            "x-ms-date" : "@utcnow()",
            "Content-type" : "application/json"
        }
    },
    "runAfter": {}
}
```
  
<span data-ttu-id="48fb7-486">Akcja odpowiedź ma specjalne ograniczenia, które nie dotyczą innych działań.</span><span class="sxs-lookup"><span data-stu-id="48fb7-486">The response action has special restrictions that don't apply to other actions.</span></span> <span data-ttu-id="48fb7-487">W szczególności:</span><span class="sxs-lookup"><span data-stu-id="48fb7-487">Specifically:</span></span>  
  
-   <span data-ttu-id="48fb7-488">Akcje reakcji nie może być równoległe w definicji deterministyczne odpowiedzi na żądania przychodzącego, jeśli jest wymagana.</span><span class="sxs-lookup"><span data-stu-id="48fb7-488">Response actions cannot be parallel in a definition because a deterministic response to the incoming request is required.</span></span>  
  
-   <span data-ttu-id="48fb7-489">Po osiągnięciu akcji odpowiedzi po otrzymaniu odpowiedzi żądania przychodzącego, jeśli akcja jest uznawany za nie powiodło się \(konflikt\), i w związku z tym jest uruchomienie `Failed`.</span><span class="sxs-lookup"><span data-stu-id="48fb7-489">If a response action is reached after the incoming request has received a response, the action is considered failed \(conflict\), and as a result, the run is `Failed`.</span></span>  
  
-   <span data-ttu-id="48fb7-490">Przepływ pracy z akcjami odpowiedzi nie może mieć `splitOn` w jego wyzwalacza jedno wywołanie powoduje, że wiele przebiegów.</span><span class="sxs-lookup"><span data-stu-id="48fb7-490">A workflow with Response actions cannot have `splitOn` in its trigger because one call causes many runs.</span></span> <span data-ttu-id="48fb7-491">W związku z tym to powinny być weryfikowane po przepływ, PUT i Przyczyna nieprawidłowe żądanie.</span><span class="sxs-lookup"><span data-stu-id="48fb7-491">As a result, this should be validated when the flow is PUT and cause a Bad Request.</span></span>  
  
## <a name="wait-action"></a><span data-ttu-id="48fb7-492">Poczekaj akcji</span><span class="sxs-lookup"><span data-stu-id="48fb7-492">Wait action</span></span>  

<span data-ttu-id="48fb7-493">`wait` Akcji wstrzymuje wykonywanie przepływu pracy dla określonego interwału.</span><span class="sxs-lookup"><span data-stu-id="48fb7-493">The `wait` action suspends workflow execution for the specified interval.</span></span> <span data-ttu-id="48fb7-494">Na przykład aby poczekaj 15 minut, można użyć ta Wstawka kodu:</span><span class="sxs-lookup"><span data-stu-id="48fb7-494">For example, to wait 15 minutes, you can use this snippet:</span></span>  
  
```json
"waitForFifteenMinutes" : {
    "type": "wait",
    "inputs": {
        "interval": {
            "unit" : "minute",
            "count" : 15
        }
    }
}
```  
  
<span data-ttu-id="48fb7-495">Można również czekać, aż do określonego momentu w czasie, można użyć w tym przykładzie:</span><span class="sxs-lookup"><span data-stu-id="48fb7-495">Alternatively, to wait until a specific moment in time, you can use this example:</span></span>  
  
```json
"waitUntilOctober" : {
    "type": "wait",
    "inputs": {
        "until": {
            "timestamp" : "2016-10-01T00:00:00Z"
        }
    }
}
```
  
> [!NOTE]  
> <span data-ttu-id="48fb7-496">Czas oczekiwania albo można użyć **interwał** obiektu lub **do momentu** obiektu, ale nie oba.</span><span class="sxs-lookup"><span data-stu-id="48fb7-496">The wait duration can be either specified using the **interval** object or the **until** object, but not both.</span></span>  
  
|<span data-ttu-id="48fb7-497">Nazwa</span><span class="sxs-lookup"><span data-stu-id="48fb7-497">Name</span></span>|<span data-ttu-id="48fb7-498">Wymagane</span><span class="sxs-lookup"><span data-stu-id="48fb7-498">Required</span></span>|<span data-ttu-id="48fb7-499">Typ</span><span class="sxs-lookup"><span data-stu-id="48fb7-499">Type</span></span>|<span data-ttu-id="48fb7-500">Opis</span><span class="sxs-lookup"><span data-stu-id="48fb7-500">Description</span></span>|  
|--------|------------|--------|---------------|  
|<span data-ttu-id="48fb7-501">Interwał</span><span class="sxs-lookup"><span data-stu-id="48fb7-501">interval</span></span>|<span data-ttu-id="48fb7-502">Nie</span><span class="sxs-lookup"><span data-stu-id="48fb7-502">No</span></span>|<span data-ttu-id="48fb7-503">Obiekt</span><span class="sxs-lookup"><span data-stu-id="48fb7-503">Object</span></span>|<span data-ttu-id="48fb7-504">Czas oczekiwania, oparte na czas.</span><span class="sxs-lookup"><span data-stu-id="48fb7-504">The wait duration based on amount of time.</span></span>|  
|<span data-ttu-id="48fb7-505">Interwał</span><span class="sxs-lookup"><span data-stu-id="48fb7-505">interval unit</span></span>|<span data-ttu-id="48fb7-506">Tak</span><span class="sxs-lookup"><span data-stu-id="48fb7-506">Yes</span></span>|<span data-ttu-id="48fb7-507">Ciąg</span><span class="sxs-lookup"><span data-stu-id="48fb7-507">String</span></span>|<span data-ttu-id="48fb7-508">Jeden z tych przedziałów: sekundy, minuty, godziny, dnia, tygodnia, miesiąca, roku.</span><span class="sxs-lookup"><span data-stu-id="48fb7-508">One of these intervals: second, minute, hour, day, week, month, year.</span></span>|  
|<span data-ttu-id="48fb7-509">Liczba interwale</span><span class="sxs-lookup"><span data-stu-id="48fb7-509">interval count</span></span>|<span data-ttu-id="48fb7-510">Tak</span><span class="sxs-lookup"><span data-stu-id="48fb7-510">Yes</span></span>|<span data-ttu-id="48fb7-511">Ciąg</span><span class="sxs-lookup"><span data-stu-id="48fb7-511">String</span></span>|<span data-ttu-id="48fb7-512">Czas trwania oparte na danej jednostce wewnętrznego.</span><span class="sxs-lookup"><span data-stu-id="48fb7-512">Duration based on the given internal unit.</span></span>|  
|<span data-ttu-id="48fb7-513">do czasu</span><span class="sxs-lookup"><span data-stu-id="48fb7-513">until</span></span>|<span data-ttu-id="48fb7-514">Nie</span><span class="sxs-lookup"><span data-stu-id="48fb7-514">No</span></span>|<span data-ttu-id="48fb7-515">Obiekt</span><span class="sxs-lookup"><span data-stu-id="48fb7-515">Object</span></span>|<span data-ttu-id="48fb7-516">Czas oczekiwania na podstawie punktu w czasie.</span><span class="sxs-lookup"><span data-stu-id="48fb7-516">The wait duration based on a point in time.</span></span>|  
|<span data-ttu-id="48fb7-517">do sygnatury czasowej</span><span class="sxs-lookup"><span data-stu-id="48fb7-517">until timestamp</span></span>|<span data-ttu-id="48fb7-518">Tak</span><span class="sxs-lookup"><span data-stu-id="48fb7-518">Yes</span></span>|<span data-ttu-id="48fb7-519">Ciąg</span><span class="sxs-lookup"><span data-stu-id="48fb7-519">String</span></span>|<span data-ttu-id="48fb7-520">Ciąg &#124; Do punktu w czasie w formacie UTC wygaśnięcia czas oczekiwania.</span><span class="sxs-lookup"><span data-stu-id="48fb7-520">String&#124;The point in time in UTC when the wait expires.</span></span>|  

## <a name="query-action"></a><span data-ttu-id="48fb7-521">Akcja kwerendy</span><span class="sxs-lookup"><span data-stu-id="48fb7-521">Query action</span></span>

<span data-ttu-id="48fb7-522">`query` Akcja umożliwia filtrowanie na podstawie warunku tablicy.</span><span class="sxs-lookup"><span data-stu-id="48fb7-522">The `query` action lets you filter an array based on a condition.</span></span> <span data-ttu-id="48fb7-523">Na przykład aby wybrać liczby większe niż 2, można:</span><span class="sxs-lookup"><span data-stu-id="48fb7-523">For example, to select numbers greater than 2, you can use:</span></span>

```json
"FilterNumbers" : {
    "type": "query",
    "inputs": {
        "from": [ 1, 3, 0, 5, 4, 2 ],
        "where": "@greater(item(), 2)"
    }
}
```

<span data-ttu-id="48fb7-524">Dane wyjściowe z `query` akcji jest tablicę, która ma elementy z tablicy wejściowej, które spełniają warunek.</span><span class="sxs-lookup"><span data-stu-id="48fb7-524">The output from the `query` action is an array that has elements from the input array that satisfy the condition.</span></span>

> [!NOTE]
> <span data-ttu-id="48fb7-525">Jeśli spełniać żadnych wartości `where` warunek, wynik ma być pustą tablicą.</span><span class="sxs-lookup"><span data-stu-id="48fb7-525">If no values satisfy the `where` condition, the result is an empty array.</span></span>

|<span data-ttu-id="48fb7-526">Nazwa</span><span class="sxs-lookup"><span data-stu-id="48fb7-526">Name</span></span>|<span data-ttu-id="48fb7-527">Wymagane</span><span class="sxs-lookup"><span data-stu-id="48fb7-527">Required</span></span>|<span data-ttu-id="48fb7-528">Typ</span><span class="sxs-lookup"><span data-stu-id="48fb7-528">Type</span></span>|<span data-ttu-id="48fb7-529">Opis</span><span class="sxs-lookup"><span data-stu-id="48fb7-529">Description</span></span>|
|--------|------------|--------|---------------|
|<span data-ttu-id="48fb7-530">Z</span><span class="sxs-lookup"><span data-stu-id="48fb7-530">from</span></span>|<span data-ttu-id="48fb7-531">Tak</span><span class="sxs-lookup"><span data-stu-id="48fb7-531">Yes</span></span>|<span data-ttu-id="48fb7-532">Tablica</span><span class="sxs-lookup"><span data-stu-id="48fb7-532">Array</span></span>|<span data-ttu-id="48fb7-533">Tablica źródłowa.</span><span class="sxs-lookup"><span data-stu-id="48fb7-533">The source array.</span></span>|
|<span data-ttu-id="48fb7-534">gdzie</span><span class="sxs-lookup"><span data-stu-id="48fb7-534">where</span></span>|<span data-ttu-id="48fb7-535">Tak</span><span class="sxs-lookup"><span data-stu-id="48fb7-535">Yes</span></span>|<span data-ttu-id="48fb7-536">Ciąg</span><span class="sxs-lookup"><span data-stu-id="48fb7-536">String</span></span>|<span data-ttu-id="48fb7-537">Warunek, którego chcesz zastosować do każdego elementu tablicy źródłowej.</span><span class="sxs-lookup"><span data-stu-id="48fb7-537">The condition to apply to each element of the source array.</span></span>|

## <a name="select-action"></a><span data-ttu-id="48fb7-538">Wybierz akcję</span><span class="sxs-lookup"><span data-stu-id="48fb7-538">Select action</span></span>

<span data-ttu-id="48fb7-539">`select` Pozwala projektów każdy element tablicy na nową wartość.</span><span class="sxs-lookup"><span data-stu-id="48fb7-539">The `select` action lets you project each element of an array into a new value.</span></span>
<span data-ttu-id="48fb7-540">Na przykład aby przekonwertować tablicy liczb znajdujących się na tablicę obiektów, można:</span><span class="sxs-lookup"><span data-stu-id="48fb7-540">For example, to convert an array of numbers into an array of objects, you can use:</span></span>

```json
"SelectNumbers" : {
    "type": "select",
    "inputs": {
        "from": [ 1, 3, 0, 5, 4, 2 ],
        "select": { "number": "@item()" }
    }
}
```

<span data-ttu-id="48fb7-541">Dane wyjściowe `select` akcji jest tablicą, który ma tego samego Kardynalność jako tablica wejściowa z każdym elementem przekształcone zgodnie z definicją w `select` właściwości.</span><span class="sxs-lookup"><span data-stu-id="48fb7-541">The output of the `select` action is an array that has the same cardinality as the input array, with each element transformed as defined by the `select` property.</span></span> <span data-ttu-id="48fb7-542">Jeśli dane wejściowe jest pusta tablica, dane wyjściowe jest również być pustą tablicą.</span><span class="sxs-lookup"><span data-stu-id="48fb7-542">If the input is an empty array, the output is also an empty array.</span></span>

|<span data-ttu-id="48fb7-543">Nazwa</span><span class="sxs-lookup"><span data-stu-id="48fb7-543">Name</span></span>|<span data-ttu-id="48fb7-544">Wymagane</span><span class="sxs-lookup"><span data-stu-id="48fb7-544">Required</span></span>|<span data-ttu-id="48fb7-545">Typ</span><span class="sxs-lookup"><span data-stu-id="48fb7-545">Type</span></span>|<span data-ttu-id="48fb7-546">Opis</span><span class="sxs-lookup"><span data-stu-id="48fb7-546">Description</span></span>|
|--------|------------|--------|---------------|
|<span data-ttu-id="48fb7-547">Z</span><span class="sxs-lookup"><span data-stu-id="48fb7-547">from</span></span>|<span data-ttu-id="48fb7-548">Tak</span><span class="sxs-lookup"><span data-stu-id="48fb7-548">Yes</span></span>|<span data-ttu-id="48fb7-549">Tablica</span><span class="sxs-lookup"><span data-stu-id="48fb7-549">Array</span></span>|<span data-ttu-id="48fb7-550">Tablica źródłowa.</span><span class="sxs-lookup"><span data-stu-id="48fb7-550">The source array.</span></span>|
|<span data-ttu-id="48fb7-551">Wybierz</span><span class="sxs-lookup"><span data-stu-id="48fb7-551">select</span></span>|<span data-ttu-id="48fb7-552">Tak</span><span class="sxs-lookup"><span data-stu-id="48fb7-552">Yes</span></span>|<span data-ttu-id="48fb7-553">Dowolne</span><span class="sxs-lookup"><span data-stu-id="48fb7-553">Any</span></span>|<span data-ttu-id="48fb7-554">Projekcji, które można zastosować do każdego elementu tablicy źródłowej.</span><span class="sxs-lookup"><span data-stu-id="48fb7-554">The projection to apply to each element of the source array.</span></span>|

## <a name="terminate-action"></a><span data-ttu-id="48fb7-555">Zakończenie akcji</span><span class="sxs-lookup"><span data-stu-id="48fb7-555">Terminate action</span></span>

<span data-ttu-id="48fb7-556">Akcja zakończenia zatrzymuje wykonywanie uruchomienia przepływu pracy, przerywanie wszystkie akcje locie i pomija wszystkie pozostałe akcje.</span><span class="sxs-lookup"><span data-stu-id="48fb7-556">The Terminate action stops execution of the workflow run, aborting any in-flight actions, and skipping any remaining actions.</span></span> <span data-ttu-id="48fb7-557">Na przykład, aby zakończyć wykonywania o stanie ****, można użyć następującego fragmentu kodu:</span><span class="sxs-lookup"><span data-stu-id="48fb7-557">For example, to terminate a run with status **Failed**, you can use the following snippet:</span></span>

```json
"HandleUnexpectedResponse" : {
    "type": "terminate",
    "inputs": {
        "runStatus" : "failed",
        "runError": {
            "code": "UnexpectedResponse",
            "message": "Received an unexpected response.",
        }
    }
}
```

> [!NOTE]
> <span data-ttu-id="48fb7-558">Akcja zakończenia nie dotyczy działania już zakończone.</span><span class="sxs-lookup"><span data-stu-id="48fb7-558">Actions already completed are not affected by the terminate action.</span></span>

|<span data-ttu-id="48fb7-559">Nazwa</span><span class="sxs-lookup"><span data-stu-id="48fb7-559">Name</span></span>|<span data-ttu-id="48fb7-560">Wymagane</span><span class="sxs-lookup"><span data-stu-id="48fb7-560">Required</span></span>|<span data-ttu-id="48fb7-561">Typ</span><span class="sxs-lookup"><span data-stu-id="48fb7-561">Type</span></span>|<span data-ttu-id="48fb7-562">Opis</span><span class="sxs-lookup"><span data-stu-id="48fb7-562">Description</span></span>|
|--------|------------|--------|---------------|
|<span data-ttu-id="48fb7-563">runStatus</span><span class="sxs-lookup"><span data-stu-id="48fb7-563">runStatus</span></span>|<span data-ttu-id="48fb7-564">Tak</span><span class="sxs-lookup"><span data-stu-id="48fb7-564">Yes</span></span>|<span data-ttu-id="48fb7-565">Ciąg</span><span class="sxs-lookup"><span data-stu-id="48fb7-565">String</span></span>|<span data-ttu-id="48fb7-566">Obiekt docelowy stan uruchomienia.</span><span class="sxs-lookup"><span data-stu-id="48fb7-566">The target run status.</span></span> <span data-ttu-id="48fb7-567">Albo **nie powiodło się** lub **anulowane**.</span><span class="sxs-lookup"><span data-stu-id="48fb7-567">Either **Failed** or **Cancelled**.</span></span>|
|<span data-ttu-id="48fb7-568">runError</span><span class="sxs-lookup"><span data-stu-id="48fb7-568">runError</span></span>|<span data-ttu-id="48fb7-569">Nie</span><span class="sxs-lookup"><span data-stu-id="48fb7-569">No</span></span>|<span data-ttu-id="48fb7-570">Obiekt</span><span class="sxs-lookup"><span data-stu-id="48fb7-570">Object</span></span>|<span data-ttu-id="48fb7-571">Szczegóły błędu.</span><span class="sxs-lookup"><span data-stu-id="48fb7-571">The error details.</span></span> <span data-ttu-id="48fb7-572">Tylko obsługiwane w przypadku **runStatus** ustawiono ****.</span><span class="sxs-lookup"><span data-stu-id="48fb7-572">Only supported when **runStatus** is set to **Failed**.</span></span>|
|<span data-ttu-id="48fb7-573">Kod runError</span><span class="sxs-lookup"><span data-stu-id="48fb7-573">runError code</span></span>|<span data-ttu-id="48fb7-574">Nie</span><span class="sxs-lookup"><span data-stu-id="48fb7-574">No</span></span>|<span data-ttu-id="48fb7-575">Ciąg</span><span class="sxs-lookup"><span data-stu-id="48fb7-575">String</span></span>|<span data-ttu-id="48fb7-576">Błąd podczas wykonywania kodu.</span><span class="sxs-lookup"><span data-stu-id="48fb7-576">The run error code.</span></span>|
|<span data-ttu-id="48fb7-577">komunikat runError</span><span class="sxs-lookup"><span data-stu-id="48fb7-577">runError message</span></span>|<span data-ttu-id="48fb7-578">Nie</span><span class="sxs-lookup"><span data-stu-id="48fb7-578">No</span></span>|<span data-ttu-id="48fb7-579">Ciąg</span><span class="sxs-lookup"><span data-stu-id="48fb7-579">String</span></span>|<span data-ttu-id="48fb7-580">Komunikat uruchamiania.</span><span class="sxs-lookup"><span data-stu-id="48fb7-580">The run error message.</span></span>|

## <a name="compose-action"></a><span data-ttu-id="48fb7-581">Redagowanie akcji</span><span class="sxs-lookup"><span data-stu-id="48fb7-581">Compose action</span></span>

<span data-ttu-id="48fb7-582">Redaguj pozwala utworzenia dowolnego obiektu.</span><span class="sxs-lookup"><span data-stu-id="48fb7-582">The Compose action lets you construct an arbitrary object.</span></span> <span data-ttu-id="48fb7-583">Dane wyjściowe działania Redaguj jest wynikiem obliczenia wejścia.</span><span class="sxs-lookup"><span data-stu-id="48fb7-583">The output of the compose action is the result of evaluating its inputs.</span></span> <span data-ttu-id="48fb7-584">Na przykład umożliwia akcji tworzenia Scal dane wyjściowe z wielu czynności:</span><span class="sxs-lookup"><span data-stu-id="48fb7-584">For example, you can use the compose action to merge outputs of multiple actions:</span></span>

```json
"composeUserRecord" : {
    "type": "compose",
    "inputs": {
        "firstName": "@actions('getUser').firstName",
        "alias": "@actions('getUser').alias",
        "thumbnailLink": "@actions('lookupThumbnail').url"
        }
    }
}
```

> [!NOTE]
> <span data-ttu-id="48fb7-585">**Redaguj** akcja może zostać użyta do skonstruowania żadnych danych wyjściowych, w tym obiektów, tablic i innego typu obsługiwane przez logikę aplikacji, takich jak XML i pliku binarnego.</span><span class="sxs-lookup"><span data-stu-id="48fb7-585">The **Compose** action can be used to construct any output, including objects, arrays, and any other type natively supported by logic apps like XML and binary.</span></span>

## <a name="table-action"></a><span data-ttu-id="48fb7-586">Akcja tabeli</span><span class="sxs-lookup"><span data-stu-id="48fb7-586">Table action</span></span>

<span data-ttu-id="48fb7-587">`table` Umożliwia konwertowanie tablicę elementów do **CSV** lub **HTML** tabeli.</span><span class="sxs-lookup"><span data-stu-id="48fb7-587">The `table` allows you to convert an array of items into a **CSV** or **HTML** table.</span></span>

<span data-ttu-id="48fb7-588">Załóżmy, że @triggerBodyjest)</span><span class="sxs-lookup"><span data-stu-id="48fb7-588">Suppose @triggerBody() is</span></span>

```json
[{
  "id": 0,
  "name": "apples"
},{
  "id": 1, 
  "name": "oranges"
}]
```

<span data-ttu-id="48fb7-589">Natomiast akcji można zdefiniować jako</span><span class="sxs-lookup"><span data-stu-id="48fb7-589">And let the action be defined as</span></span>

```json
"ConvertToTable" : {
    "type": "table",
    "inputs": {
        "from": "@triggerBody()",
        "format": "html"
    }
}
```

<span data-ttu-id="48fb7-590">Powyższe dałby w efekcie</span><span class="sxs-lookup"><span data-stu-id="48fb7-590">The above would produce</span></span>

<table><thead><tr><th><span data-ttu-id="48fb7-591">id</span><span class="sxs-lookup"><span data-stu-id="48fb7-591">id</span></span></th><th><span data-ttu-id="48fb7-592">name</span><span class="sxs-lookup"><span data-stu-id="48fb7-592">name</span></span></th></tr></thead><tbody><tr><td><span data-ttu-id="48fb7-593">0</span><span class="sxs-lookup"><span data-stu-id="48fb7-593">0</span></span></td><td><span data-ttu-id="48fb7-594">jabłek</span><span class="sxs-lookup"><span data-stu-id="48fb7-594">apples</span></span></td></tr><tr><td><span data-ttu-id="48fb7-595">1</span><span class="sxs-lookup"><span data-stu-id="48fb7-595">1</span></span></td><td><span data-ttu-id="48fb7-596">Pomarańcze</span><span class="sxs-lookup"><span data-stu-id="48fb7-596">oranges</span></span></td></tr></tbody></table><span data-ttu-id="48fb7-597">"</span><span class="sxs-lookup"><span data-stu-id="48fb7-597">"</span></span>

<span data-ttu-id="48fb7-598">Aby dostosować tabeli, należy określić kolumny jawnie.</span><span class="sxs-lookup"><span data-stu-id="48fb7-598">In order to customize the table, you can specify the columns explicitly.</span></span> <span data-ttu-id="48fb7-599">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="48fb7-599">For example:</span></span>

```json
"ConvertToTable" : {
    "type": "table",
    "inputs": {
        "from": "@triggerBody()",
        "format": "html",
        "columns": [{
          "header": "produce id",
          "value": "@item().id"
        },{
          "header": "description",
          "value": "@concat('fresh ', item().name)"
        }]
    }
}
```

<span data-ttu-id="48fb7-600">Powyższe dałby w efekcie</span><span class="sxs-lookup"><span data-stu-id="48fb7-600">The above would produce</span></span>

<table><thead><tr><th><span data-ttu-id="48fb7-601">Tworzy identyfikator</span><span class="sxs-lookup"><span data-stu-id="48fb7-601">produce id</span></span></th><th><span data-ttu-id="48fb7-602">Opis elementu</span><span class="sxs-lookup"><span data-stu-id="48fb7-602">description</span></span></th></tr></thead><tbody><tr><td><span data-ttu-id="48fb7-603">0</span><span class="sxs-lookup"><span data-stu-id="48fb7-603">0</span></span></td><td><span data-ttu-id="48fb7-604">Nowa jabłek</span><span class="sxs-lookup"><span data-stu-id="48fb7-604">fresh apples</span></span></td></tr><tr><td><span data-ttu-id="48fb7-605">1</span><span class="sxs-lookup"><span data-stu-id="48fb7-605">1</span></span></td><td><span data-ttu-id="48fb7-606">świeżych pomarańczy</span><span class="sxs-lookup"><span data-stu-id="48fb7-606">fresh oranges</span></span></td></tr></tbody></table><span data-ttu-id="48fb7-607">"</span><span class="sxs-lookup"><span data-stu-id="48fb7-607">"</span></span>

<span data-ttu-id="48fb7-608">Jeśli `from` wartość właściwości jest pusta tablica, dane wyjściowe jest pusta tabela.</span><span class="sxs-lookup"><span data-stu-id="48fb7-608">If the `from` property value is an empty array, the output is an empty table.</span></span>

|<span data-ttu-id="48fb7-609">Nazwa</span><span class="sxs-lookup"><span data-stu-id="48fb7-609">Name</span></span>|<span data-ttu-id="48fb7-610">Wymagane</span><span class="sxs-lookup"><span data-stu-id="48fb7-610">Required</span></span>|<span data-ttu-id="48fb7-611">Typ</span><span class="sxs-lookup"><span data-stu-id="48fb7-611">Type</span></span>|<span data-ttu-id="48fb7-612">Opis</span><span class="sxs-lookup"><span data-stu-id="48fb7-612">Description</span></span>|
|--------|------------|--------|---------------|
|<span data-ttu-id="48fb7-613">Z</span><span class="sxs-lookup"><span data-stu-id="48fb7-613">from</span></span>|<span data-ttu-id="48fb7-614">Tak</span><span class="sxs-lookup"><span data-stu-id="48fb7-614">Yes</span></span>|<span data-ttu-id="48fb7-615">Tablica</span><span class="sxs-lookup"><span data-stu-id="48fb7-615">Array</span></span>|<span data-ttu-id="48fb7-616">Tablica źródłowa.</span><span class="sxs-lookup"><span data-stu-id="48fb7-616">The source array.</span></span>|
|<span data-ttu-id="48fb7-617">Format</span><span class="sxs-lookup"><span data-stu-id="48fb7-617">format</span></span>|<span data-ttu-id="48fb7-618">Tak</span><span class="sxs-lookup"><span data-stu-id="48fb7-618">Yes</span></span>|<span data-ttu-id="48fb7-619">Ciąg</span><span class="sxs-lookup"><span data-stu-id="48fb7-619">String</span></span>|<span data-ttu-id="48fb7-620">Format, albo **CSV** lub **HTML**.</span><span class="sxs-lookup"><span data-stu-id="48fb7-620">The format, either **CSV** or **HTML**.</span></span>|
|<span data-ttu-id="48fb7-621">kolumny</span><span class="sxs-lookup"><span data-stu-id="48fb7-621">columns</span></span>|<span data-ttu-id="48fb7-622">Nie</span><span class="sxs-lookup"><span data-stu-id="48fb7-622">No</span></span>|<span data-ttu-id="48fb7-623">Tablica</span><span class="sxs-lookup"><span data-stu-id="48fb7-623">Array</span></span>|<span data-ttu-id="48fb7-624">Kolumny.</span><span class="sxs-lookup"><span data-stu-id="48fb7-624">The columns.</span></span> <span data-ttu-id="48fb7-625">Umożliwia zastąpienie domyślnego kształtu tabeli.</span><span class="sxs-lookup"><span data-stu-id="48fb7-625">Allows to override the default shape of the table.</span></span>|
|<span data-ttu-id="48fb7-626">Nagłówek kolumny</span><span class="sxs-lookup"><span data-stu-id="48fb7-626">column header</span></span>|<span data-ttu-id="48fb7-627">Nie</span><span class="sxs-lookup"><span data-stu-id="48fb7-627">No</span></span>|<span data-ttu-id="48fb7-628">Ciąg</span><span class="sxs-lookup"><span data-stu-id="48fb7-628">String</span></span>|<span data-ttu-id="48fb7-629">Nagłówek kolumny.</span><span class="sxs-lookup"><span data-stu-id="48fb7-629">The header of the column.</span></span>|
|<span data-ttu-id="48fb7-630">wartość w kolumnie</span><span class="sxs-lookup"><span data-stu-id="48fb7-630">column value</span></span>|<span data-ttu-id="48fb7-631">Tak</span><span class="sxs-lookup"><span data-stu-id="48fb7-631">Yes</span></span>|<span data-ttu-id="48fb7-632">Ciąg</span><span class="sxs-lookup"><span data-stu-id="48fb7-632">String</span></span>|<span data-ttu-id="48fb7-633">Wartość kolumny.</span><span class="sxs-lookup"><span data-stu-id="48fb7-633">The value of the column.</span></span>|

## <a name="workflow-action"></a><span data-ttu-id="48fb7-634">Działania przepływu pracy</span><span class="sxs-lookup"><span data-stu-id="48fb7-634">Workflow action</span></span>   

|<span data-ttu-id="48fb7-635">Nazwa</span><span class="sxs-lookup"><span data-stu-id="48fb7-635">Name</span></span>|<span data-ttu-id="48fb7-636">Wymagane</span><span class="sxs-lookup"><span data-stu-id="48fb7-636">Required</span></span>|<span data-ttu-id="48fb7-637">Typ</span><span class="sxs-lookup"><span data-stu-id="48fb7-637">Type</span></span>|<span data-ttu-id="48fb7-638">Opis</span><span class="sxs-lookup"><span data-stu-id="48fb7-638">Description</span></span>|  
|--------|------------|--------|---------------|  
|<span data-ttu-id="48fb7-639">Identyfikator hosta</span><span class="sxs-lookup"><span data-stu-id="48fb7-639">host id</span></span>|<span data-ttu-id="48fb7-640">Tak</span><span class="sxs-lookup"><span data-stu-id="48fb7-640">Yes</span></span>|<span data-ttu-id="48fb7-641">Ciąg</span><span class="sxs-lookup"><span data-stu-id="48fb7-641">String</span></span>|<span data-ttu-id="48fb7-642">Identyfikator zasobu przepływu pracy, który ma zostać wywołana.</span><span class="sxs-lookup"><span data-stu-id="48fb7-642">The resource ID of the workflow that you want to call.</span></span>|  
|<span data-ttu-id="48fb7-643">Nazwa_wyzwalacza hosta</span><span class="sxs-lookup"><span data-stu-id="48fb7-643">host triggerName</span></span>|<span data-ttu-id="48fb7-644">Tak</span><span class="sxs-lookup"><span data-stu-id="48fb7-644">Yes</span></span>|<span data-ttu-id="48fb7-645">Ciąg</span><span class="sxs-lookup"><span data-stu-id="48fb7-645">String</span></span>|<span data-ttu-id="48fb7-646">Nazwa wyzwalacza, który chcesz wywołać.</span><span class="sxs-lookup"><span data-stu-id="48fb7-646">The name of the trigger that you want to invoke.</span></span>|  
|<span data-ttu-id="48fb7-647">— zapytania</span><span class="sxs-lookup"><span data-stu-id="48fb7-647">queries</span></span>|<span data-ttu-id="48fb7-648">Nie</span><span class="sxs-lookup"><span data-stu-id="48fb7-648">No</span></span>|<span data-ttu-id="48fb7-649">Obiekt</span><span class="sxs-lookup"><span data-stu-id="48fb7-649">Object</span></span>|<span data-ttu-id="48fb7-650">Reprezentuje parametry zapytania, aby dodać do adresu URL.</span><span class="sxs-lookup"><span data-stu-id="48fb7-650">Represents the query parameters to add to the URL.</span></span> <span data-ttu-id="48fb7-651">Na przykład `"queries" : { "api-version": "2015-02-01" }` dodaje `?api-version=2015-02-01` do adresu URL.</span><span class="sxs-lookup"><span data-stu-id="48fb7-651">For example, `"queries" : { "api-version": "2015-02-01" }` adds `?api-version=2015-02-01` to the URL.</span></span>|  
|<span data-ttu-id="48fb7-652">Nagłówki</span><span class="sxs-lookup"><span data-stu-id="48fb7-652">headers</span></span>|<span data-ttu-id="48fb7-653">Nie</span><span class="sxs-lookup"><span data-stu-id="48fb7-653">No</span></span>|<span data-ttu-id="48fb7-654">Obiekt</span><span class="sxs-lookup"><span data-stu-id="48fb7-654">Object</span></span>|<span data-ttu-id="48fb7-655">Reprezentuje listę nagłówków, które są wysyłane do żądania.</span><span class="sxs-lookup"><span data-stu-id="48fb7-655">Represents each of the headers that is sent to the request.</span></span> <span data-ttu-id="48fb7-656">Na przykład, aby ustawić język i typ żądania:`"headers" : { "Accept-Language": "en-us",  "Content-Type": "application/json" }`</span><span class="sxs-lookup"><span data-stu-id="48fb7-656">For example, to set the language and type on a request: `"headers" : { "Accept-Language": "en-us",  "Content-Type": "application/json" }`</span></span>|  
|<span data-ttu-id="48fb7-657">Treści</span><span class="sxs-lookup"><span data-stu-id="48fb7-657">body</span></span>|<span data-ttu-id="48fb7-658">Nie</span><span class="sxs-lookup"><span data-stu-id="48fb7-658">No</span></span>|<span data-ttu-id="48fb7-659">Obiekt</span><span class="sxs-lookup"><span data-stu-id="48fb7-659">Object</span></span>|<span data-ttu-id="48fb7-660">Reprezentuje obciążenie wysyłane do punktu końcowego.</span><span class="sxs-lookup"><span data-stu-id="48fb7-660">Represents the payload sent to the endpoint.</span></span>|  
  
```json
"mynestedwf" : {
    "type" : "workflow",
    "inputs" : {
        "host" : {
            "id" : "/subscriptions/xxxxyyyyzzz/resourceGroups/rg001/providers/Microsoft.Logic/mywf001",
            "triggerName " : "mytrigger001"
        },
        "queries" : {
            "extrafield" : "specialValue"
        },  
        "headers" : {
            "x-ms-date" : "@utcnow()",
            "Content-type" : "application/json"
        },
        "body" : {
            "contentFieldOne" : "value100",
            "anotherField" : 10.001
        }
    },
    "runAfter": {}
    }
```
  
<span data-ttu-id="48fb7-661">Sprawdzanie dostępu jest wprowadzone w przepływie pracy \(dokładniej, wyzwalacz\), co oznacza, potrzebny jest dostęp do przepływu pracy.</span><span class="sxs-lookup"><span data-stu-id="48fb7-661">An access check is made on the workflow \(more specifically, the trigger\), meaning you need access to the workflow.</span></span>  
  
<span data-ttu-id="48fb7-662">Dane wyjściowe z `workflow` akcji są oparte na zdefiniowane w `response` działania w przepływie pracy podrzędnych.</span><span class="sxs-lookup"><span data-stu-id="48fb7-662">The outputs from the `workflow` action are based on what you defined in the `response` action in the child workflow.</span></span> <span data-ttu-id="48fb7-663">Jeśli nie zdefiniowano żadnego `response` akcji, a następnie dane wyjściowe są puste.</span><span class="sxs-lookup"><span data-stu-id="48fb7-663">If you have not defined any `response` action, then the outputs are empty.</span></span>  

## <a name="function-action"></a><span data-ttu-id="48fb7-664">Akcja — funkcja</span><span class="sxs-lookup"><span data-stu-id="48fb7-664">Function action</span></span>   

|<span data-ttu-id="48fb7-665">Nazwa</span><span class="sxs-lookup"><span data-stu-id="48fb7-665">Name</span></span>|<span data-ttu-id="48fb7-666">Wymagane</span><span class="sxs-lookup"><span data-stu-id="48fb7-666">Required</span></span>|<span data-ttu-id="48fb7-667">Typ</span><span class="sxs-lookup"><span data-stu-id="48fb7-667">Type</span></span>|<span data-ttu-id="48fb7-668">Opis</span><span class="sxs-lookup"><span data-stu-id="48fb7-668">Description</span></span>|  
|--------|------------|--------|---------------|  
|<span data-ttu-id="48fb7-669">id — funkcja</span><span class="sxs-lookup"><span data-stu-id="48fb7-669">function id</span></span>|<span data-ttu-id="48fb7-670">Tak</span><span class="sxs-lookup"><span data-stu-id="48fb7-670">Yes</span></span>|<span data-ttu-id="48fb7-671">Ciąg</span><span class="sxs-lookup"><span data-stu-id="48fb7-671">String</span></span>|<span data-ttu-id="48fb7-672">Identyfikator zasobu do wywołania funkcji.</span><span class="sxs-lookup"><span data-stu-id="48fb7-672">The resource ID of the function that you want to invoke.</span></span>|  
|<span data-ttu-id="48fb7-673">— Metoda</span><span class="sxs-lookup"><span data-stu-id="48fb7-673">method</span></span>|<span data-ttu-id="48fb7-674">Nie</span><span class="sxs-lookup"><span data-stu-id="48fb7-674">No</span></span>|<span data-ttu-id="48fb7-675">Ciąg</span><span class="sxs-lookup"><span data-stu-id="48fb7-675">String</span></span>|<span data-ttu-id="48fb7-676">Metoda HTTP używana do wywołania funkcji.</span><span class="sxs-lookup"><span data-stu-id="48fb7-676">The HTTP method used to invoke the function.</span></span> <span data-ttu-id="48fb7-677">Domyślnie jest `POST` gdy nie został określony.</span><span class="sxs-lookup"><span data-stu-id="48fb7-677">By default, it is `POST` when not specified.</span></span>|  
|<span data-ttu-id="48fb7-678">— zapytania</span><span class="sxs-lookup"><span data-stu-id="48fb7-678">queries</span></span>|<span data-ttu-id="48fb7-679">Nie</span><span class="sxs-lookup"><span data-stu-id="48fb7-679">No</span></span>|<span data-ttu-id="48fb7-680">Obiekt</span><span class="sxs-lookup"><span data-stu-id="48fb7-680">Object</span></span>|<span data-ttu-id="48fb7-681">Reprezentuje parametry zapytania, aby dodać do adresu URL.</span><span class="sxs-lookup"><span data-stu-id="48fb7-681">Represents the query parameters to add to the URL.</span></span> <span data-ttu-id="48fb7-682">Na przykład `"queries" : { "api-version": "2015-02-01" }` dodaje `?api-version=2015-02-01` do adresu URL.</span><span class="sxs-lookup"><span data-stu-id="48fb7-682">For example, `"queries" : { "api-version": "2015-02-01" }` adds `?api-version=2015-02-01` to the URL.</span></span>|  
|<span data-ttu-id="48fb7-683">Nagłówki</span><span class="sxs-lookup"><span data-stu-id="48fb7-683">headers</span></span>|<span data-ttu-id="48fb7-684">Nie</span><span class="sxs-lookup"><span data-stu-id="48fb7-684">No</span></span>|<span data-ttu-id="48fb7-685">Obiekt</span><span class="sxs-lookup"><span data-stu-id="48fb7-685">Object</span></span>|<span data-ttu-id="48fb7-686">Reprezentuje listę nagłówków, które są wysyłane do żądania.</span><span class="sxs-lookup"><span data-stu-id="48fb7-686">Represents each of the headers that is sent to the request.</span></span> <span data-ttu-id="48fb7-687">Na przykład, aby ustawić język i typ na żądanie: `"headers" : { "Accept-Language": "en-us" }`.</span><span class="sxs-lookup"><span data-stu-id="48fb7-687">For example, to set the language and type on a request: `"headers" : { "Accept-Language": "en-us" }`.</span></span>|  
|<span data-ttu-id="48fb7-688">Treści</span><span class="sxs-lookup"><span data-stu-id="48fb7-688">body</span></span>|<span data-ttu-id="48fb7-689">Nie</span><span class="sxs-lookup"><span data-stu-id="48fb7-689">No</span></span>|<span data-ttu-id="48fb7-690">Obiekt</span><span class="sxs-lookup"><span data-stu-id="48fb7-690">Object</span></span>|<span data-ttu-id="48fb7-691">Reprezentuje obciążenie wysyłane do punktu końcowego.</span><span class="sxs-lookup"><span data-stu-id="48fb7-691">Represents the payload sent to the endpoint.</span></span>|  

```json
"myfunc" : {
    "type" : "Function",
    "inputs" : {
        "function" : {
            "id" : "/subscriptions/xxxxyyyyzzz/resourceGroups/rg001/providers/Microsoft.Web/sites/myfuncapp/functions/myfunc"
        },
        "queries" : {
            "extrafield" : "specialValue"
        },  
        "headers" : {
            "x-ms-date" : "@utcnow()"
        },
        "method" : "POST",
    "body" : {
            "contentFieldOne" : "value100",
            "anotherField" : 10.001
        }
    },
    "runAfter": {}
}
```

<span data-ttu-id="48fb7-692">Podczas zapisywania aplikacji logiki, wykonujemy kontroli niektórych funkcji, do którego istnieje odwołanie:</span><span class="sxs-lookup"><span data-stu-id="48fb7-692">When you save the logic app, we perform some checks on the referenced function:</span></span>
-   <span data-ttu-id="48fb7-693">Musisz mieć dostęp do funkcji.</span><span class="sxs-lookup"><span data-stu-id="48fb7-693">You need to have access to the function.</span></span>
-   <span data-ttu-id="48fb7-694">Tylko standardowy wyzwalacza HTTP lub ogólny wyzwalacza elementu webhook JSON jest dozwolone.</span><span class="sxs-lookup"><span data-stu-id="48fb7-694">Only standard HTTP trigger or generic JSON webhook trigger is allowed.</span></span>
-   <span data-ttu-id="48fb7-695">Nie powinna mieć żadnej trasy zdefiniowane.</span><span class="sxs-lookup"><span data-stu-id="48fb7-695">It should not have any route defined.</span></span>
-   <span data-ttu-id="48fb7-696">Tylko "funkcji" i "anonymous" autoryzacji na poziomie jest dozwolone.</span><span class="sxs-lookup"><span data-stu-id="48fb7-696">Only "function" and "anonymous" authorization level is allowed.</span></span>

<span data-ttu-id="48fb7-697">Adres URL wyzwalacza jest pobierana, w pamięci podręcznej i używany w czasie wykonywania.</span><span class="sxs-lookup"><span data-stu-id="48fb7-697">The trigger URL is retrieved, cached, and used at runtime.</span></span> <span data-ttu-id="48fb7-698">Dlatego jeśli żadnej operacji unieważnia pamięci podręcznej adres URL, akcja zakończy się niepowodzeniem w czasie wykonywania.</span><span class="sxs-lookup"><span data-stu-id="48fb7-698">So if any operation invalidates the cached URL, the action fails at runtime.</span></span> <span data-ttu-id="48fb7-699">Aby obejść ten problem, należy zapisać aplikację logiki, co spowoduje aplikację logiki, aby pobrać i ponownie pamięci podręcznej adres URL wyzwalacza.</span><span class="sxs-lookup"><span data-stu-id="48fb7-699">To work around this, save the logic app again, which will cause logic app to retrieve and cache the trigger URL again.</span></span>

## <a name="collection-actions-scopes-and-loops"></a><span data-ttu-id="48fb7-700">Akcje kolekcji (zakresy i pętle)</span><span class="sxs-lookup"><span data-stu-id="48fb7-700">Collection actions (scopes and loops)</span></span>

<span data-ttu-id="48fb7-701">Niektóre typy działań mogą zawierać działania w ramach samodzielnie.</span><span class="sxs-lookup"><span data-stu-id="48fb7-701">Some action types can contain actions within themselves.</span></span> <span data-ttu-id="48fb7-702">Odwołanie do działań w ramach kolekcji można odwoływać się bezpośrednio poza kolekcji.</span><span class="sxs-lookup"><span data-stu-id="48fb7-702">Reference actions within a collection can be referenced directly outside of the collection.</span></span> <span data-ttu-id="48fb7-703">Jeśli zdefiniowano `http` w zakresie `@body('http')` jest nadal ważny w dowolnym miejscu w przepływie pracy.</span><span class="sxs-lookup"><span data-stu-id="48fb7-703">If you defined `http` in a scope, `@body('http')` is still valid anywhere in a workflow.</span></span> <span data-ttu-id="48fb7-704">Akcje w ramach kolekcji można `runAfter` tylko innych działań w ramach tej samej kolekcji.</span><span class="sxs-lookup"><span data-stu-id="48fb7-704">Actions within a collection can `runAfter` only other actions within the same collection.</span></span>

## <a name="scope-action"></a><span data-ttu-id="48fb7-705">Akcja zakresu</span><span class="sxs-lookup"><span data-stu-id="48fb7-705">Scope action</span></span>

<span data-ttu-id="48fb7-706">`scope` Pozwala logicznie grupy działań w przepływie pracy.</span><span class="sxs-lookup"><span data-stu-id="48fb7-706">The `scope` action lets you logically group actions in a workflow.</span></span>

|<span data-ttu-id="48fb7-707">Nazwa</span><span class="sxs-lookup"><span data-stu-id="48fb7-707">Name</span></span>|<span data-ttu-id="48fb7-708">Wymagane</span><span class="sxs-lookup"><span data-stu-id="48fb7-708">Required</span></span>|<span data-ttu-id="48fb7-709">Typ</span><span class="sxs-lookup"><span data-stu-id="48fb7-709">Type</span></span>|<span data-ttu-id="48fb7-710">Opis</span><span class="sxs-lookup"><span data-stu-id="48fb7-710">Description</span></span>|  
|--------|------------|--------|---------------|  
|<span data-ttu-id="48fb7-711">Akcje</span><span class="sxs-lookup"><span data-stu-id="48fb7-711">actions</span></span>|<span data-ttu-id="48fb7-712">Tak</span><span class="sxs-lookup"><span data-stu-id="48fb7-712">Yes</span></span>|<span data-ttu-id="48fb7-713">Obiekt</span><span class="sxs-lookup"><span data-stu-id="48fb7-713">Object</span></span>|<span data-ttu-id="48fb7-714">Wewnętrzny akcje do wykonania w zakresie</span><span class="sxs-lookup"><span data-stu-id="48fb7-714">Inner actions to execute within the scope</span></span>|

```json
{
    "myScope": {
        "type": "scope",
        "actions": {
            "call_bing": {
                "type": "http",
                "inputs": {
                    "url": "http://www.bing.com"
                }
            }
        }
    }
}
```

## <a name="foreach-action"></a><span data-ttu-id="48fb7-715">Akcja ForEach</span><span class="sxs-lookup"><span data-stu-id="48fb7-715">ForEach action</span></span>

<span data-ttu-id="48fb7-716">Ta akcja pętli iteruje tablicy i wykonuje akcje wewnętrzny dla każdego elementu.</span><span class="sxs-lookup"><span data-stu-id="48fb7-716">This looping action iterates through an array and performs inner actions for each item.</span></span> <span data-ttu-id="48fb7-717">Domyślnie pętli foreach wykonuje równoległe (20 wykonaniami równolegle w czasie).</span><span class="sxs-lookup"><span data-stu-id="48fb7-717">By default, the foreach loop executes in parallel (20 executions in parallel at a time).</span></span> <span data-ttu-id="48fb7-718">Można ustawić zasady wykonywania przy użyciu `operationOptions` parametru.</span><span class="sxs-lookup"><span data-stu-id="48fb7-718">You can set execution rules using the `operationOptions` parameter.</span></span>

|<span data-ttu-id="48fb7-719">Nazwa</span><span class="sxs-lookup"><span data-stu-id="48fb7-719">Name</span></span>|<span data-ttu-id="48fb7-720">Wymagane</span><span class="sxs-lookup"><span data-stu-id="48fb7-720">Required</span></span>|<span data-ttu-id="48fb7-721">Typ</span><span class="sxs-lookup"><span data-stu-id="48fb7-721">Type</span></span>|<span data-ttu-id="48fb7-722">Opis</span><span class="sxs-lookup"><span data-stu-id="48fb7-722">Description</span></span>|  
|--------|------------|--------|---------------|  
|<span data-ttu-id="48fb7-723">Akcje</span><span class="sxs-lookup"><span data-stu-id="48fb7-723">actions</span></span>|<span data-ttu-id="48fb7-724">Tak</span><span class="sxs-lookup"><span data-stu-id="48fb7-724">Yes</span></span>|<span data-ttu-id="48fb7-725">Obiekt</span><span class="sxs-lookup"><span data-stu-id="48fb7-725">Object</span></span>|<span data-ttu-id="48fb7-726">Wewnętrzny akcje do wykonania w pętli</span><span class="sxs-lookup"><span data-stu-id="48fb7-726">Inner actions to execute within the loop</span></span>|
|<span data-ttu-id="48fb7-727">Instrukcja foreach</span><span class="sxs-lookup"><span data-stu-id="48fb7-727">foreach</span></span>|<span data-ttu-id="48fb7-728">Tak</span><span class="sxs-lookup"><span data-stu-id="48fb7-728">Yes</span></span>|<span data-ttu-id="48fb7-729">Ciąg</span><span class="sxs-lookup"><span data-stu-id="48fb7-729">string</span></span>|<span data-ttu-id="48fb7-730">Tablicy w celu wykonania iteracji</span><span class="sxs-lookup"><span data-stu-id="48fb7-730">The array to iterate over</span></span>|
|<span data-ttu-id="48fb7-731">operationOptions</span><span class="sxs-lookup"><span data-stu-id="48fb7-731">operationOptions</span></span>|<span data-ttu-id="48fb7-732">Brak</span><span class="sxs-lookup"><span data-stu-id="48fb7-732">no</span></span>|<span data-ttu-id="48fb7-733">Ciąg</span><span class="sxs-lookup"><span data-stu-id="48fb7-733">string</span></span>|<span data-ttu-id="48fb7-734">Wszystkie opcje operacji zachowanie.</span><span class="sxs-lookup"><span data-stu-id="48fb7-734">Any operation options for behavior.</span></span> <span data-ttu-id="48fb7-735">Obsługuje obecnie tylko `sequential` do wykonywania iteracji sekwencyjnie (domyślne zachowanie to równoległych)</span><span class="sxs-lookup"><span data-stu-id="48fb7-735">Currently only supports `sequential` to execute iterations sequentially (default behavior is parallel)</span></span>|

```json
"forEach_email": {
    "type": "foreach",
    "foreach": "@body('email_filter')",
    "actions": {
        "send_email": {
            "type": "ApiConnection",
            "inputs": {
                "body": {
                    "to": "@item()",
                    "from": "me@contoso.com",
                    "message": "Hello, thank you for ordering"
                }
                "host": {
                    "connection": {
                        "id": "@parameters('$connections')['office365']['connection']['id']"
                    }
                }
            }
        }
    },
    "runAfter":{
        "email_filter": [ "Succeeded" ]
    }
}
```

## <a name="until-action"></a><span data-ttu-id="48fb7-736">Do działania</span><span class="sxs-lookup"><span data-stu-id="48fb7-736">Until action</span></span>

<span data-ttu-id="48fb7-737">Ta akcja pętli wykonuje akcje wewnętrzny dopóki warunek wyników do wartości true.</span><span class="sxs-lookup"><span data-stu-id="48fb7-737">This looping action executes inner actions until a condition results to true.</span></span>

|<span data-ttu-id="48fb7-738">Nazwa</span><span class="sxs-lookup"><span data-stu-id="48fb7-738">Name</span></span>|<span data-ttu-id="48fb7-739">Wymagane</span><span class="sxs-lookup"><span data-stu-id="48fb7-739">Required</span></span>|<span data-ttu-id="48fb7-740">Typ</span><span class="sxs-lookup"><span data-stu-id="48fb7-740">Type</span></span>|<span data-ttu-id="48fb7-741">Opis</span><span class="sxs-lookup"><span data-stu-id="48fb7-741">Description</span></span>|  
|--------|------------|--------|---------------|  
|<span data-ttu-id="48fb7-742">Akcje</span><span class="sxs-lookup"><span data-stu-id="48fb7-742">actions</span></span>|<span data-ttu-id="48fb7-743">Tak</span><span class="sxs-lookup"><span data-stu-id="48fb7-743">Yes</span></span>|<span data-ttu-id="48fb7-744">Obiekt</span><span class="sxs-lookup"><span data-stu-id="48fb7-744">Object</span></span>|<span data-ttu-id="48fb7-745">Wewnętrzny akcje do wykonania w pętli</span><span class="sxs-lookup"><span data-stu-id="48fb7-745">Inner actions to execute within the loop</span></span>|
|<span data-ttu-id="48fb7-746">wyrażenie</span><span class="sxs-lookup"><span data-stu-id="48fb7-746">expression</span></span>|<span data-ttu-id="48fb7-747">Tak</span><span class="sxs-lookup"><span data-stu-id="48fb7-747">Yes</span></span>|<span data-ttu-id="48fb7-748">Ciąg</span><span class="sxs-lookup"><span data-stu-id="48fb7-748">string</span></span>|<span data-ttu-id="48fb7-749">Wyrażenie do oceny po każdej iteracji</span><span class="sxs-lookup"><span data-stu-id="48fb7-749">The expression to evaluate after each iteration</span></span>|
|<span data-ttu-id="48fb7-750">Limit</span><span class="sxs-lookup"><span data-stu-id="48fb7-750">limit</span></span>|<span data-ttu-id="48fb7-751">Tak</span><span class="sxs-lookup"><span data-stu-id="48fb7-751">yes</span></span>|<span data-ttu-id="48fb7-752">Obiekt</span><span class="sxs-lookup"><span data-stu-id="48fb7-752">Object</span></span>|<span data-ttu-id="48fb7-753">Limity dla pętli — co najmniej jeden limit musi być zdefiniowana</span><span class="sxs-lookup"><span data-stu-id="48fb7-753">The limits for the loop - at least one limit must be defined</span></span>|
|<span data-ttu-id="48fb7-754">Liczba</span><span class="sxs-lookup"><span data-stu-id="48fb7-754">count</span></span>|<span data-ttu-id="48fb7-755">Brak</span><span class="sxs-lookup"><span data-stu-id="48fb7-755">no</span></span>|<span data-ttu-id="48fb7-756">int</span><span class="sxs-lookup"><span data-stu-id="48fb7-756">int</span></span>|<span data-ttu-id="48fb7-757">Limit liczby iteracji, które mogą być wykonywane</span><span class="sxs-lookup"><span data-stu-id="48fb7-757">The limit to the number of iterations that can be performed</span></span>|
|<span data-ttu-id="48fb7-758">Limit czasu</span><span class="sxs-lookup"><span data-stu-id="48fb7-758">timeout</span></span>|<span data-ttu-id="48fb7-759">Brak</span><span class="sxs-lookup"><span data-stu-id="48fb7-759">no</span></span>|<span data-ttu-id="48fb7-760">Ciąg</span><span class="sxs-lookup"><span data-stu-id="48fb7-760">string</span></span>|<span data-ttu-id="48fb7-761">Limit czasu na czas powinien pętli.</span><span class="sxs-lookup"><span data-stu-id="48fb7-761">The timeout for how long it should loop.</span></span>  <span data-ttu-id="48fb7-762">Formacie ISO 8601</span><span class="sxs-lookup"><span data-stu-id="48fb7-762">ISO 8601 format</span></span>|


```json
 "Until_succeeded": {
    "actions": {
        "Http": {
            "inputs": {
                "method": "GET",
                "uri": "http://myurl"
            },
            "runAfter": {},
            "type": "Http"
        }
    },
    "expression": "@equals(outputs('Http')['statusCode', 200)",
    "limit": {
        "count": 1000,
        "timeout": "PT1H"
    },
    "runAfter": {},
    "type": "Until"
}
```

## <a name="conditions---if-action"></a><span data-ttu-id="48fb7-763">Warunki — Jeśli akcja</span><span class="sxs-lookup"><span data-stu-id="48fb7-763">Conditions - If Action</span></span>

<span data-ttu-id="48fb7-764">`If` Pozwala ocenić warunku i wykonywanie gałęzi według tego, czy wyrażenie daje w wyniku `true`.</span><span class="sxs-lookup"><span data-stu-id="48fb7-764">The `If` action lets you evaluate a condition and execute a branch based on whether the expression evaluates to `true`.</span></span>

|<span data-ttu-id="48fb7-765">Nazwa</span><span class="sxs-lookup"><span data-stu-id="48fb7-765">Name</span></span>|<span data-ttu-id="48fb7-766">Wymagane</span><span class="sxs-lookup"><span data-stu-id="48fb7-766">Required</span></span>|<span data-ttu-id="48fb7-767">Typ</span><span class="sxs-lookup"><span data-stu-id="48fb7-767">Type</span></span>|<span data-ttu-id="48fb7-768">Opis</span><span class="sxs-lookup"><span data-stu-id="48fb7-768">Description</span></span>|  
|--------|------------|--------|---------------|  
|<span data-ttu-id="48fb7-769">Akcje</span><span class="sxs-lookup"><span data-stu-id="48fb7-769">actions</span></span>|<span data-ttu-id="48fb7-770">Tak</span><span class="sxs-lookup"><span data-stu-id="48fb7-770">Yes</span></span>|<span data-ttu-id="48fb7-771">Obiekt</span><span class="sxs-lookup"><span data-stu-id="48fb7-771">Object</span></span>|<span data-ttu-id="48fb7-772">Wewnętrzny akcje do wykonania, gdy wyrażenie daje w wyniku`true`</span><span class="sxs-lookup"><span data-stu-id="48fb7-772">Inner actions to execute when expression evaluates to `true`</span></span>|
|<span data-ttu-id="48fb7-773">wyrażenie</span><span class="sxs-lookup"><span data-stu-id="48fb7-773">expression</span></span>|<span data-ttu-id="48fb7-774">Tak</span><span class="sxs-lookup"><span data-stu-id="48fb7-774">Yes</span></span>|<span data-ttu-id="48fb7-775">Ciąg</span><span class="sxs-lookup"><span data-stu-id="48fb7-775">string</span></span>|<span data-ttu-id="48fb7-776">Wyrażenie do oceny</span><span class="sxs-lookup"><span data-stu-id="48fb7-776">The expression to evaluate</span></span>|
|<span data-ttu-id="48fb7-777">else</span><span class="sxs-lookup"><span data-stu-id="48fb7-777">else</span></span>|<span data-ttu-id="48fb7-778">Brak</span><span class="sxs-lookup"><span data-stu-id="48fb7-778">no</span></span>|<span data-ttu-id="48fb7-779">Obiekt</span><span class="sxs-lookup"><span data-stu-id="48fb7-779">Object</span></span>|<span data-ttu-id="48fb7-780">Wewnętrzny akcje do wykonania, gdy wyrażenie daje w wyniku`false`</span><span class="sxs-lookup"><span data-stu-id="48fb7-780">Inner actions to execute when expression evaluates to `false`</span></span>|
  
```json
"My_condition": {
    "actions": {
        "If_true": {
            "inputs": {
                "method": "GET",
                "uri": "http://myurl"
            },
            "runAfter": {},
            "type": "Http"
        }
    },
    "else": {
        "actions": {
            "if_false": {
                "inputs": {
                    "method": "GET",
                    "uri": "http://myurl"
                },
                "runAfter": {},
                "type": "Http"
            }
        }
    },
    "expression": "@equals(triggerBody(), json(true))",
    "runAfter": {},
    "type": "If"
}
```  
  
<span data-ttu-id="48fb7-781">W poniższej tabeli przedstawiono przykłady warunków użycia wyrażeń w akcji:</span><span class="sxs-lookup"><span data-stu-id="48fb7-781">The following table shows examples of how conditions can use expressions in an action:</span></span>  
  
|<span data-ttu-id="48fb7-782">Wartość JSON</span><span class="sxs-lookup"><span data-stu-id="48fb7-782">JSON value</span></span>|<span data-ttu-id="48fb7-783">wynik</span><span class="sxs-lookup"><span data-stu-id="48fb7-783">Result</span></span>|  
|--------------|----------|  
|`"expression": "@parameters('hasSpecialAction')"`|<span data-ttu-id="48fb7-784">Żadnej wartości, które są używane do oceny na wartość true powoduje, że ten stan do przekazania.</span><span class="sxs-lookup"><span data-stu-id="48fb7-784">Any value that would evaluate to true causes this condition to pass.</span></span> <span data-ttu-id="48fb7-785">Obsługiwane są tylko wyrażenia logiczne.</span><span class="sxs-lookup"><span data-stu-id="48fb7-785">Only Boolean expressions are supported.</span></span> <span data-ttu-id="48fb7-786">Aby przekonwertować inne typy Boolean, użyj funkcji `empty`, `equals`.</span><span class="sxs-lookup"><span data-stu-id="48fb7-786">To convert other types to Boolean, use functions `empty`, `equals`.</span></span>|  
|`"expression": "@greater(actions('act1').output.value, parameters('threshold'))"`|<span data-ttu-id="48fb7-787">Porównanie funkcji są obsługiwane.</span><span class="sxs-lookup"><span data-stu-id="48fb7-787">Comparison functions are supported.</span></span> <span data-ttu-id="48fb7-788">Na przykład tutaj Akcja wykonywana tylko po act1 danych wyjściowych jest większy niż próg.</span><span class="sxs-lookup"><span data-stu-id="48fb7-788">For the example here, the action only executes when the output of act1 is greater than the threshold.</span></span>|  
|`"expression": "@or(greater(actions('act1').output.value, parameters('threshold')), less(actions('act1').output.value, 100))"`|<span data-ttu-id="48fb7-789">Logika funkcje są również obsługiwane do tworzenia zagnieżdżonych wyrażeń logicznych.</span><span class="sxs-lookup"><span data-stu-id="48fb7-789">Logic functions are also supported to create nested Boolean expressions.</span></span> <span data-ttu-id="48fb7-790">W takim przypadku operacja zostanie wykonana, gdy dane wyjściowe act1 jest powyżej wartości progowej lub poniżej 100.</span><span class="sxs-lookup"><span data-stu-id="48fb7-790">In this case, the action executes when the output of act1 is above the threshold or below 100.</span></span>|  
|`"expression": "@equals(length(actions('act1').outputs.errors), 0))"`|<span data-ttu-id="48fb7-791">Możesz użyć funkcji tablicy, aby sprawdzić, czy wszystkie elementy tablicy.</span><span class="sxs-lookup"><span data-stu-id="48fb7-791">You can use array functions to check if an array has any items.</span></span> <span data-ttu-id="48fb7-792">W takim przypadku operacja zostanie wykonana, gdy macierz błędów jest pusta.</span><span class="sxs-lookup"><span data-stu-id="48fb7-792">In this case, the action executes when the errors array is empty.</span></span>| 
|`"expression": "parameters('hasSpecialAction')"`|<span data-ttu-id="48fb7-793">Błąd — nie jest prawidłowym warunku, ponieważ @ jest wymagany dla warunków.</span><span class="sxs-lookup"><span data-stu-id="48fb7-793">Error - not a valid condition because @ is required for conditions.</span></span>|  
  
<span data-ttu-id="48fb7-794">Jeśli wynikiem warunku jest pomyślnie, warunek zostanie oznaczona jako `Succeeded`.</span><span class="sxs-lookup"><span data-stu-id="48fb7-794">If a condition evaluates successfully, the condition is marked as `Succeeded`.</span></span> <span data-ttu-id="48fb7-795">Akcje w ramach jednej `actions` lub `else` obliczać obiektów `Succeeded` po wykonaniu i zakończyło się pomyślnie, `Failed` po wykonaniu i nie powiodło się, lub `Skipped` po gałąź, nie została wykonana.</span><span class="sxs-lookup"><span data-stu-id="48fb7-795">Actions within either the `actions` or `else` objects evaluate to `Succeeded` when executed and succeeded, `Failed` when executed and failed, or `Skipped` when that branch is not executed.</span></span>

## <a name="next-steps"></a><span data-ttu-id="48fb7-796">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="48fb7-796">Next steps</span></span>

[<span data-ttu-id="48fb7-797">Interfejs API REST usługi przepływu pracy</span><span class="sxs-lookup"><span data-stu-id="48fb7-797">Workflow Service REST API</span></span>](https://docs.microsoft.com/rest/api/logic/workflows)
