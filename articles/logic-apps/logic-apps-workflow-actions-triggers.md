---
title: "aaaWorkflow działań i wyzwalaczy - Azure Logic Apps | Dokumentacja firmy Microsoft"
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
ms.openlocfilehash: 857927b7d7df3fc9cdc4931ffdb613efde0db9f9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="workflow-actions-and-triggers-for-azure-logic-apps"></a><span data-ttu-id="dba86-102">Działania przepływu pracy i Wyzwalacze dla usługi Azure Logic Apps</span><span class="sxs-lookup"><span data-stu-id="dba86-102">Workflow actions and triggers for Azure Logic Apps</span></span>

<span data-ttu-id="dba86-103">Aplikacje logiki składają się z wyzwalacze i akcje.</span><span class="sxs-lookup"><span data-stu-id="dba86-103">Logic apps consist of triggers and actions.</span></span> <span data-ttu-id="dba86-104">Istnieją typy sześciu wyzwalaczy.</span><span class="sxs-lookup"><span data-stu-id="dba86-104">There are six types of triggers.</span></span> <span data-ttu-id="dba86-105">Każdy typ ma inny interfejs i inaczej.</span><span class="sxs-lookup"><span data-stu-id="dba86-105">Each type has different interface and different behavior.</span></span> <span data-ttu-id="dba86-106">Również informacje na temat innych szczegółów sprawdzając szczegóły hello hello [język definicji przepływu pracy](logic-apps-workflow-definition-language.md).</span><span class="sxs-lookup"><span data-stu-id="dba86-106">You can also learn about other details by looking at hello details of hello [Workflow Definition Language](logic-apps-workflow-definition-language.md).</span></span>  
  
<span data-ttu-id="dba86-107">Poniżej toolearn więcej informacji na temat wyzwalacze i akcje i jak można ich używać toobuild logic apps tooimprove Twojego procesów biznesowych i przepływów pracy.</span><span class="sxs-lookup"><span data-stu-id="dba86-107">Read on toolearn more about triggers and actions and how you might use them toobuild logic apps tooimprove your business processes and workflows.</span></span>  
  
### <a name="triggers"></a><span data-ttu-id="dba86-108">Wyzwalacze</span><span class="sxs-lookup"><span data-stu-id="dba86-108">Triggers</span></span>  

<span data-ttu-id="dba86-109">Wyzwalacz określa hello wywołania, które mogą inicjować uruchomienia przepływu pracy aplikacji logiki.</span><span class="sxs-lookup"><span data-stu-id="dba86-109">A trigger specifies hello calls that can initiate a run of your logic app workflow.</span></span> <span data-ttu-id="dba86-110">Poniżej przedstawiono hello tooinitiate dwa sposoby uruchomienia przepływu pracy:</span><span class="sxs-lookup"><span data-stu-id="dba86-110">Here are hello two different ways tooinitiate a run of your workflow:</span></span>  
  
-   <span data-ttu-id="dba86-111">Wyzwalacz sondowania</span><span class="sxs-lookup"><span data-stu-id="dba86-111">A polling trigger</span></span>  

-   <span data-ttu-id="dba86-112">Wyzwalacz wypychania - przez wywołanie hello [interfejsu API REST usługi przepływu pracy](https://docs.microsoft.com/rest/api/logic/workflows)</span><span class="sxs-lookup"><span data-stu-id="dba86-112">A push trigger - by calling hello [Workflow Service REST API](https://docs.microsoft.com/rest/api/logic/workflows)</span></span>  
  
<span data-ttu-id="dba86-113">Wszystkich wyzwalaczy zawierać tych elementów najwyższego poziomu:</span><span class="sxs-lookup"><span data-stu-id="dba86-113">All triggers contain these top-level elements:</span></span>  
  
```json
"<name-of-the-trigger>" : {
    "type": "<type-of-trigger>",
    "inputs": { <settings-for-the-call> },
    "recurrence": {  
        "frequency": "Second|Minute|Hour|Week|Month|Year",
        "interval": "<recurrence interval in units of frequency>"
    },
    "conditions": [ <array-of-required-conditions > ],
    "splitOn" : "<property toocreate runs for>",
    "operationOptions": "<operation options on hello trigger>"
}
```

### <a name="trigger-types-and-their-inputs"></a><span data-ttu-id="dba86-114">Typy wyzwalaczy i ich dane wejściowe</span><span class="sxs-lookup"><span data-stu-id="dba86-114">Trigger types and their inputs</span></span>  

<span data-ttu-id="dba86-115">Można używać tych typów wyzwalaczy:</span><span class="sxs-lookup"><span data-stu-id="dba86-115">You can use these types of triggers:</span></span>
  
-   <span data-ttu-id="dba86-116">**Żądanie** \- sprawia, że aplikacja logiki hello punktu końcowego dla toocall możesz</span><span class="sxs-lookup"><span data-stu-id="dba86-116">**Request** \- Makes hello logic app an endpoint for you toocall</span></span>  
  
-   <span data-ttu-id="dba86-117">**Cykl** \- uruchamiany zgodnie z harmonogramem zdefiniowanym</span><span class="sxs-lookup"><span data-stu-id="dba86-117">**Recurrence** \- Fires based on a defined schedule</span></span>  
  
-   <span data-ttu-id="dba86-118">**HTTP** \- sonduje punkt końcowy HTTP sieci web.</span><span class="sxs-lookup"><span data-stu-id="dba86-118">**HTTP** \- Polls an HTTP web endpoint.</span></span> <span data-ttu-id="dba86-119">Hello HTTP punktu końcowego musi być zgodna określonym kontraktem wyzwalająca tooa \- przy użyciu 202\-wzorca asynchronicznego, lub tablicę</span><span class="sxs-lookup"><span data-stu-id="dba86-119">hello HTTP endpoint must conform tooa specific triggering contract \- either by using a 202\-async pattern, or by returning an array</span></span>  
  
-   <span data-ttu-id="dba86-120">**ApiConnection** \- wyzwolenia ankiety, takich jak hello HTTP, jednak jego zalet hello [zarządzany przez firmę Microsoft interfejsy API](https://docs.microsoft.com/azure/connectors/apis-list)</span><span class="sxs-lookup"><span data-stu-id="dba86-120">**ApiConnection** \- Polls like hello HTTP trigger, however, it takes advantage of hello [Microsoft-managed APIs](https://docs.microsoft.com/azure/connectors/apis-list)</span></span>  
  
-   <span data-ttu-id="dba86-121">**HTTPWebhook** \- otwiera jako punkt końcowy, podobne toohello ręczne wyzwalacza, jednak również wywołuje limit tooa określony adres URL tooregister i wyrejestrować</span><span class="sxs-lookup"><span data-stu-id="dba86-121">**HTTPWebhook** \- Opens an endpoint, similar toohello Manual trigger, however, it also calls out tooa specified URL tooregister and unregister</span></span>  
  
-   <span data-ttu-id="dba86-122">**ApiConnectionWebhook** \- działa jak hello wyzwalacza HTTPWebhook dzięki wykorzystaniu hello zarządzany przez firmę Microsoft interfejsy API</span><span class="sxs-lookup"><span data-stu-id="dba86-122">**ApiConnectionWebhook** \- Operates like hello HTTPWebhook trigger by taking advantage of hello Microsoft-managed APIs</span></span>       
    <span data-ttu-id="dba86-123">Każdy typ wyzwalacza ma inny zestaw **dane wejściowe** definiuje zachowanie.</span><span class="sxs-lookup"><span data-stu-id="dba86-123">Each trigger type has a different set of **inputs** that defines its behavior.</span></span>  
  
## <a name="request-trigger"></a><span data-ttu-id="dba86-124">Wyzwalacz żądania</span><span class="sxs-lookup"><span data-stu-id="dba86-124">Request trigger</span></span>  

<span data-ttu-id="dba86-125">Tego wyzwalacza służy jako punkt końcowy, który należy wywołać za pomocą żądania HTTP tooinvoke aplikacji logiki.</span><span class="sxs-lookup"><span data-stu-id="dba86-125">This trigger serves as an endpoint that you call via an HTTP Request tooinvoke your logic app.</span></span> <span data-ttu-id="dba86-126">Wyzwalacz żądania wygląda następująco:</span><span class="sxs-lookup"><span data-stu-id="dba86-126">A request trigger looks like this example:</span></span>  
  
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

<span data-ttu-id="dba86-127">Istnieje również opcjonalny właściwości o nazwie **schematu**:</span><span class="sxs-lookup"><span data-stu-id="dba86-127">There is also an optional property called **schema**:</span></span>  
  
|<span data-ttu-id="dba86-128">Nazwa elementu</span><span class="sxs-lookup"><span data-stu-id="dba86-128">Element name</span></span>|<span data-ttu-id="dba86-129">Wymagane</span><span class="sxs-lookup"><span data-stu-id="dba86-129">Required</span></span>|<span data-ttu-id="dba86-130">Opis</span><span class="sxs-lookup"><span data-stu-id="dba86-130">Description</span></span>|  
|----------------|------------|---------------|  
|<span data-ttu-id="dba86-131">Schemat</span><span class="sxs-lookup"><span data-stu-id="dba86-131">schema</span></span>|<span data-ttu-id="dba86-132">Nie</span><span class="sxs-lookup"><span data-stu-id="dba86-132">No</span></span>|<span data-ttu-id="dba86-133">Weryfikuje żądanie przychodzące hello schematu JSON.</span><span class="sxs-lookup"><span data-stu-id="dba86-133">A JSON schema that validates hello incoming request.</span></span> <span data-ttu-id="dba86-134">Przydatne w przypadku kolejnych kroków wiedzieć, który tooreference właściwości Pomoc.</span><span class="sxs-lookup"><span data-stu-id="dba86-134">Useful for helping subsequent workflow steps know which properties tooreference.</span></span>|

<span data-ttu-id="dba86-135">tooinvoke ten punkt końcowy należy toocall hello *listCallbackUrl* interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="dba86-135">tooinvoke this endpoint, you need toocall hello *listCallbackUrl* API.</span></span> <span data-ttu-id="dba86-136">Zobacz [interfejsu API REST usługi przepływu pracy](https://docs.microsoft.com/rest/api/logic/workflows).</span><span class="sxs-lookup"><span data-stu-id="dba86-136">See [Workflow Service REST API](https://docs.microsoft.com/rest/api/logic/workflows).</span></span>  
  
## <a name="recurrence-trigger"></a><span data-ttu-id="dba86-137">Wyzwalacz cyklu</span><span class="sxs-lookup"><span data-stu-id="dba86-137">Recurrence trigger</span></span>  

<span data-ttu-id="dba86-138">Wyzwalacz cyklu jest jedną, która będzie uruchamiana na zdefiniowanym harmonogramem.</span><span class="sxs-lookup"><span data-stu-id="dba86-138">A Recurrence trigger is one that runs based on a defined schedule.</span></span> <span data-ttu-id="dba86-139">Takie wyzwalacz może wyglądać w tym przykładzie:</span><span class="sxs-lookup"><span data-stu-id="dba86-139">Such a trigger might look like this example:</span></span>  

```json
"dailyReport" : {
    "type": "recurrence",
    "recurrence": {
        "frequency": "Day",
        "interval": "1"
    }
}
```

<span data-ttu-id="dba86-140">Jak widać, jest prosty sposób toorun przepływ pracy.</span><span class="sxs-lookup"><span data-stu-id="dba86-140">As you can see, it is a simple way toorun a workflow.</span></span>  
  
|<span data-ttu-id="dba86-141">Nazwa elementu</span><span class="sxs-lookup"><span data-stu-id="dba86-141">Element name</span></span>|<span data-ttu-id="dba86-142">Wymagane</span><span class="sxs-lookup"><span data-stu-id="dba86-142">Required</span></span>|<span data-ttu-id="dba86-143">Opis</span><span class="sxs-lookup"><span data-stu-id="dba86-143">Description</span></span>|  
|----------------|------------|---------------|  
|<span data-ttu-id="dba86-144">frequency</span><span class="sxs-lookup"><span data-stu-id="dba86-144">frequency</span></span>|<span data-ttu-id="dba86-145">Tak</span><span class="sxs-lookup"><span data-stu-id="dba86-145">Yes</span></span>|<span data-ttu-id="dba86-146">Jak często hello wyzwalacza wykonuje.</span><span class="sxs-lookup"><span data-stu-id="dba86-146">How often hello trigger executes.</span></span> <span data-ttu-id="dba86-147">Używać tylko jednej z następujących wartości: sekundy, minuty, godziny, dnia, tygodnia, miesiąc lub rok</span><span class="sxs-lookup"><span data-stu-id="dba86-147">Use only one of these possible values: second, minute, hour, day, week, month, or year</span></span>|  
|<span data-ttu-id="dba86-148">interval</span><span class="sxs-lookup"><span data-stu-id="dba86-148">interval</span></span>|<span data-ttu-id="dba86-149">Tak</span><span class="sxs-lookup"><span data-stu-id="dba86-149">Yes</span></span>|<span data-ttu-id="dba86-150">Interwał hello podana częstotliwość cyklu hello</span><span class="sxs-lookup"><span data-stu-id="dba86-150">Interval of hello given frequency for hello recurrence</span></span>|  
|<span data-ttu-id="dba86-151">startTime</span><span class="sxs-lookup"><span data-stu-id="dba86-151">startTime</span></span>|<span data-ttu-id="dba86-152">Nie</span><span class="sxs-lookup"><span data-stu-id="dba86-152">No</span></span>|<span data-ttu-id="dba86-153">Jeśli czas rozpoczęcia jest dostarczany bez przesunięcie czasu UTC, zostanie użyta tej strefy czasowej.</span><span class="sxs-lookup"><span data-stu-id="dba86-153">If a startTime is provided without a UTC offset, this timeZone is used.</span></span>|  
|<span data-ttu-id="dba86-154">Strefa czasowa</span><span class="sxs-lookup"><span data-stu-id="dba86-154">timeZone</span></span>|<span data-ttu-id="dba86-155">Brak</span><span class="sxs-lookup"><span data-stu-id="dba86-155">no</span></span>|<span data-ttu-id="dba86-156">Jeśli czas rozpoczęcia jest dostarczany bez przesunięcie czasu UTC, zostanie użyta tej strefy czasowej.</span><span class="sxs-lookup"><span data-stu-id="dba86-156">If a startTime is provided without a UTC offset, this timeZone is used.</span></span>|  
  
<span data-ttu-id="dba86-157">Można również zaplanować toostart wyzwalacza w pewnym momencie w przyszłości hello wykonywania.</span><span class="sxs-lookup"><span data-stu-id="dba86-157">You can also schedule a trigger toostart executing at some point in hello future.</span></span> <span data-ttu-id="dba86-158">Na przykład jeśli chcesz toostart co tydzień raport w każdy poniedziałek można zaplanować toostart aplikacji logiki hello w każdy poniedziałek, tworząc następujące wyzwalacza hello:</span><span class="sxs-lookup"><span data-stu-id="dba86-158">For example, if you want toostart a weekly report every Monday you can schedule hello logic app toostart every Monday by creating hello following trigger:</span></span>  

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

## <a name="http-trigger"></a><span data-ttu-id="dba86-159">Wyzwalacz HTTP</span><span class="sxs-lookup"><span data-stu-id="dba86-159">HTTP trigger</span></span>  

<span data-ttu-id="dba86-160">HTTP wyzwalacze sondowania określony punkt końcowy i hello odpowiedzi toodetermine Sprawdź, czy mają zostać wykonane hello przepływu pracy.</span><span class="sxs-lookup"><span data-stu-id="dba86-160">HTTP triggers poll a specified endpoint and check hello response toodetermine whether hello workflow should be executed.</span></span> <span data-ttu-id="dba86-161">Obiekt danych wejściowych Hello przyjmuje hello zbiór tooconstruct wymagane parametry połączenia HTTP:</span><span class="sxs-lookup"><span data-stu-id="dba86-161">hello inputs object takes hello set of parameters required tooconstruct an HTTP call:</span></span>  
  
|<span data-ttu-id="dba86-162">Nazwa elementu</span><span class="sxs-lookup"><span data-stu-id="dba86-162">Element name</span></span>|<span data-ttu-id="dba86-163">Wymagane</span><span class="sxs-lookup"><span data-stu-id="dba86-163">Required</span></span>|<span data-ttu-id="dba86-164">Opis</span><span class="sxs-lookup"><span data-stu-id="dba86-164">Description</span></span>|<span data-ttu-id="dba86-165">Typ</span><span class="sxs-lookup"><span data-stu-id="dba86-165">Type</span></span>|  
|----------------|------------|---------------|--------|  
|<span data-ttu-id="dba86-166">— Metoda</span><span class="sxs-lookup"><span data-stu-id="dba86-166">method</span></span>|<span data-ttu-id="dba86-167">Tak</span><span class="sxs-lookup"><span data-stu-id="dba86-167">yes</span></span>|<span data-ttu-id="dba86-168">Może być jedną z następujących metod HTTP hello: GET, POST, PUT, DELETE, poprawki lub HEAD</span><span class="sxs-lookup"><span data-stu-id="dba86-168">Can be one of hello following HTTP methods: GET, POST, PUT, DELETE, PATCH, or HEAD</span></span>|<span data-ttu-id="dba86-169">Ciąg</span><span class="sxs-lookup"><span data-stu-id="dba86-169">String</span></span>|  
|<span data-ttu-id="dba86-170">Identyfikator URI</span><span class="sxs-lookup"><span data-stu-id="dba86-170">uri</span></span>|<span data-ttu-id="dba86-171">Tak</span><span class="sxs-lookup"><span data-stu-id="dba86-171">yes</span></span>|<span data-ttu-id="dba86-172">Witaj punkt końcowy http lub https, który jest wywoływana.</span><span class="sxs-lookup"><span data-stu-id="dba86-172">hello http or https endpoint that is called.</span></span> <span data-ttu-id="dba86-173">Maksymalnie 2 kilobajtów.</span><span class="sxs-lookup"><span data-stu-id="dba86-173">Maximum of 2 kilobytes.</span></span>|<span data-ttu-id="dba86-174">Ciąg</span><span class="sxs-lookup"><span data-stu-id="dba86-174">String</span></span>|  
|<span data-ttu-id="dba86-175">— zapytania</span><span class="sxs-lookup"><span data-stu-id="dba86-175">queries</span></span>|<span data-ttu-id="dba86-176">Nie</span><span class="sxs-lookup"><span data-stu-id="dba86-176">No</span></span>|<span data-ttu-id="dba86-177">Obiekt reprezentujący adres URL toohello tooadd hello kwerendy parametrów.</span><span class="sxs-lookup"><span data-stu-id="dba86-177">An object representing hello query parameters tooadd toohello URL.</span></span> <span data-ttu-id="dba86-178">Na przykład `"queries" : { "api-version": "2015-02-01" }` dodaje `?api-version=2015-02-01` toohello adresu URL.</span><span class="sxs-lookup"><span data-stu-id="dba86-178">For example, `"queries" : { "api-version": "2015-02-01" }` adds `?api-version=2015-02-01` toohello URL.</span></span>|<span data-ttu-id="dba86-179">Obiekt</span><span class="sxs-lookup"><span data-stu-id="dba86-179">Object</span></span>|  
|<span data-ttu-id="dba86-180">Nagłówki</span><span class="sxs-lookup"><span data-stu-id="dba86-180">headers</span></span>|<span data-ttu-id="dba86-181">Nie</span><span class="sxs-lookup"><span data-stu-id="dba86-181">No</span></span>|<span data-ttu-id="dba86-182">Obiekt reprezentujący każdego hello nagłówki, które są wysyłane żądania toohello.</span><span class="sxs-lookup"><span data-stu-id="dba86-182">An object representing each of hello headers that is sent toohello request.</span></span> <span data-ttu-id="dba86-183">Na przykład tooset hello język i typ żądania:`"headers" : { "Accept-Language": "en-us",  "Content-Type": "application/json" }`</span><span class="sxs-lookup"><span data-stu-id="dba86-183">For example, tooset hello language and type on a request: `"headers" : { "Accept-Language": "en-us",  "Content-Type": "application/json" }`</span></span>|<span data-ttu-id="dba86-184">Obiekt</span><span class="sxs-lookup"><span data-stu-id="dba86-184">Object</span></span>|  
|<span data-ttu-id="dba86-185">Treści</span><span class="sxs-lookup"><span data-stu-id="dba86-185">body</span></span>|<span data-ttu-id="dba86-186">Nie</span><span class="sxs-lookup"><span data-stu-id="dba86-186">No</span></span>|<span data-ttu-id="dba86-187">Obiekt reprezentujący ładunku hello, wysyłany toohello punktu końcowego.</span><span class="sxs-lookup"><span data-stu-id="dba86-187">An object representing hello payload that is sent toohello endpoint.</span></span>|<span data-ttu-id="dba86-188">Obiekt</span><span class="sxs-lookup"><span data-stu-id="dba86-188">Object</span></span>|  
|<span data-ttu-id="dba86-189">retryPolicy</span><span class="sxs-lookup"><span data-stu-id="dba86-189">retryPolicy</span></span>|<span data-ttu-id="dba86-190">Nie</span><span class="sxs-lookup"><span data-stu-id="dba86-190">No</span></span>|<span data-ttu-id="dba86-191">Obiekt, który można dostosować zachowanie przy ponownych prób hello 4xx lub 5xx błędów.</span><span class="sxs-lookup"><span data-stu-id="dba86-191">An object that lets you customize hello retry behavior for 4xx or 5xx errors.</span></span>|<span data-ttu-id="dba86-192">Obiekt</span><span class="sxs-lookup"><span data-stu-id="dba86-192">Object</span></span>|  
|<span data-ttu-id="dba86-193">Uwierzytelnianie</span><span class="sxs-lookup"><span data-stu-id="dba86-193">authentication</span></span>|<span data-ttu-id="dba86-194">Nie</span><span class="sxs-lookup"><span data-stu-id="dba86-194">No</span></span>|<span data-ttu-id="dba86-195">Reprezentuje metodę hello hello żądania uwierzytelniania.</span><span class="sxs-lookup"><span data-stu-id="dba86-195">Represents hello method that hello request should be authenticated.</span></span> <span data-ttu-id="dba86-196">Aby uzyskać więcej informacji na ten obiekt, zobacz [uwierzytelniania połączeń wychodzących harmonogramu](https://docs.microsoft.com/azure/scheduler/scheduler-outbound-authentication).</span><span class="sxs-lookup"><span data-stu-id="dba86-196">For details on this object, see [Scheduler Outbound Authentication](https://docs.microsoft.com/azure/scheduler/scheduler-outbound-authentication).</span></span> <span data-ttu-id="dba86-197">Poza harmonogramem, jest jedna właściwość więcej obsługiwanych: `authority` domyślnie ta wartość jest `https://login.windows.net` gdy nie jest określony, można używać różnych odbiorców, takich jak`https://login.windows\-ppe.net`</span><span class="sxs-lookup"><span data-stu-id="dba86-197">Beyond scheduler, there is one more supported property: `authority` By default, this value is `https://login.windows.net` when not specified, but you can use a different audience like `https://login.windows\-ppe.net`</span></span>|<span data-ttu-id="dba86-198">Obiekt</span><span class="sxs-lookup"><span data-stu-id="dba86-198">Object</span></span>|  
  
<span data-ttu-id="dba86-199">Witaj wyzwalacza HTTP wymaga hello tooconform HTTP API z określonym wzorcem toowork z aplikacji logiki.</span><span class="sxs-lookup"><span data-stu-id="dba86-199">hello HTTP trigger requires hello HTTP API tooconform with a specific pattern toowork well with your logic app.</span></span> <span data-ttu-id="dba86-200">Wymaga hello następujące pola:</span><span class="sxs-lookup"><span data-stu-id="dba86-200">It requires hello following fields:</span></span>  
  
|<span data-ttu-id="dba86-201">Odpowiedź</span><span class="sxs-lookup"><span data-stu-id="dba86-201">Response</span></span>|<span data-ttu-id="dba86-202">Opis</span><span class="sxs-lookup"><span data-stu-id="dba86-202">Description</span></span>|  
|------------|---------------|  
|<span data-ttu-id="dba86-203">Kod stanu</span><span class="sxs-lookup"><span data-stu-id="dba86-203">Status code</span></span>|<span data-ttu-id="dba86-204">Kod stanu 200 \(OK\) toocause Uruchom.</span><span class="sxs-lookup"><span data-stu-id="dba86-204">Status code 200 \(OK\) toocause a run.</span></span> <span data-ttu-id="dba86-205">Każdy kod stanu nie powoduje uruchomienia.</span><span class="sxs-lookup"><span data-stu-id="dba86-205">Any other status code doesn't cause a run.</span></span>|  
|<span data-ttu-id="dba86-206">Spróbuj ponownie\-po nagłówka</span><span class="sxs-lookup"><span data-stu-id="dba86-206">Retry\-after header</span></span>|<span data-ttu-id="dba86-207">Liczba sekund do aplikacji logiki hello ponownie sonduje hello punktu końcowego.</span><span class="sxs-lookup"><span data-stu-id="dba86-207">Number of seconds until hello logic app polls hello endpoint again.</span></span>|  
|<span data-ttu-id="dba86-208">Nagłówek lokalizacji</span><span class="sxs-lookup"><span data-stu-id="dba86-208">Location header</span></span>|<span data-ttu-id="dba86-209">Witaj toocall adres URL na powitania dalej interwału sondowania.</span><span class="sxs-lookup"><span data-stu-id="dba86-209">hello URL toocall on hello next polling interval.</span></span> <span data-ttu-id="dba86-210">Jeśli nie zostanie określony, oryginalny adres URL hello jest używany.</span><span class="sxs-lookup"><span data-stu-id="dba86-210">If not specified, hello original URL is used.</span></span>|  
  
<span data-ttu-id="dba86-211">Oto kilka przykładów różne zachowania dla różnych typów żądań:</span><span class="sxs-lookup"><span data-stu-id="dba86-211">Here are some examples of different behaviors for different types of requests:</span></span>  
  
|<span data-ttu-id="dba86-212">Kod odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="dba86-212">Response code</span></span>|<span data-ttu-id="dba86-213">Spróbuj ponownie\-po</span><span class="sxs-lookup"><span data-stu-id="dba86-213">Retry\-After</span></span>|<span data-ttu-id="dba86-214">Zachowanie</span><span class="sxs-lookup"><span data-stu-id="dba86-214">Behavior</span></span>|  
|-----------------|----------------|------------|  
|<span data-ttu-id="dba86-215">200</span><span class="sxs-lookup"><span data-stu-id="dba86-215">200</span></span>|<span data-ttu-id="dba86-216">\(Brak\)</span><span class="sxs-lookup"><span data-stu-id="dba86-216">\(none\)</span></span>|<span data-ttu-id="dba86-217">Nie prawidłowy wyzwalacza, ponów próbę\-po sond dla następnego żądania hello jest nigdy nie hello wymagane lub inny aparat.</span><span class="sxs-lookup"><span data-stu-id="dba86-217">Not a valid trigger, Retry\-After is required, or else hello engine never polls for hello next request.</span></span>|  
|<span data-ttu-id="dba86-218">202</span><span class="sxs-lookup"><span data-stu-id="dba86-218">202</span></span>|<span data-ttu-id="dba86-219">60</span><span class="sxs-lookup"><span data-stu-id="dba86-219">60</span></span>|<span data-ttu-id="dba86-220">Nie wyzwalają hello przepływu pracy.</span><span class="sxs-lookup"><span data-stu-id="dba86-220">Do not trigger hello workflow.</span></span> <span data-ttu-id="dba86-221">Witaj następnej próbie odbywa się w jednej minuty.</span><span class="sxs-lookup"><span data-stu-id="dba86-221">hello next attempt happens in one minute.</span></span>|  
|<span data-ttu-id="dba86-222">200</span><span class="sxs-lookup"><span data-stu-id="dba86-222">200</span></span>|<span data-ttu-id="dba86-223">10</span><span class="sxs-lookup"><span data-stu-id="dba86-223">10</span></span>|<span data-ttu-id="dba86-224">Uruchamianie przepływu pracy hello i sprawdź ponownie więcej zawartości za 10 sekund.</span><span class="sxs-lookup"><span data-stu-id="dba86-224">Run hello workflow, and check again for more content in 10 seconds.</span></span>|  
|<span data-ttu-id="dba86-225">400</span><span class="sxs-lookup"><span data-stu-id="dba86-225">400</span></span>|<span data-ttu-id="dba86-226">\(Brak\)</span><span class="sxs-lookup"><span data-stu-id="dba86-226">\(none\)</span></span>|<span data-ttu-id="dba86-227">Nieprawidłowe żądanie, nie uruchamiaj hello przepływu pracy.</span><span class="sxs-lookup"><span data-stu-id="dba86-227">Bad request, do not run hello workflow.</span></span> <span data-ttu-id="dba86-228">W przypadku nie **ponów zasad** zdefiniowany, zostanie użyty hello domyślne zasady.</span><span class="sxs-lookup"><span data-stu-id="dba86-228">If there is no **Retry Policy** defined, then hello default policy is used.</span></span> <span data-ttu-id="dba86-229">Po osiągnięciu hello liczby ponownych prób hello wyzwalacz nie jest już prawidłowy.</span><span class="sxs-lookup"><span data-stu-id="dba86-229">After hello number of retries has been reached, hello trigger is no longer valid.</span></span>|  
|<span data-ttu-id="dba86-230">500</span><span class="sxs-lookup"><span data-stu-id="dba86-230">500</span></span>|<span data-ttu-id="dba86-231">\(Brak\)</span><span class="sxs-lookup"><span data-stu-id="dba86-231">\(none\)</span></span>|<span data-ttu-id="dba86-232">Błąd serwera, nie uruchamiaj hello przepływu pracy.</span><span class="sxs-lookup"><span data-stu-id="dba86-232">Server error, do not run hello workflow.</span></span>  <span data-ttu-id="dba86-233">W przypadku nie **ponów zasad** zdefiniowany, zostanie użyty hello domyślne zasady.</span><span class="sxs-lookup"><span data-stu-id="dba86-233">If there is no **Retry Policy** defined, then hello default policy is used.</span></span> <span data-ttu-id="dba86-234">Po osiągnięciu hello liczby ponownych prób hello wyzwalacz nie jest już prawidłowy.</span><span class="sxs-lookup"><span data-stu-id="dba86-234">After hello number of retries has been reached, hello trigger is no longer valid.</span></span>|  
  
<span data-ttu-id="dba86-235">dane wyjściowe Hello wyzwalacza HTTP wyglądać w tym przykładzie:</span><span class="sxs-lookup"><span data-stu-id="dba86-235">hello outputs of an HTTP trigger look like this example:</span></span>  
  
|<span data-ttu-id="dba86-236">Nazwa elementu</span><span class="sxs-lookup"><span data-stu-id="dba86-236">Element name</span></span>|<span data-ttu-id="dba86-237">Opis</span><span class="sxs-lookup"><span data-stu-id="dba86-237">Description</span></span>|<span data-ttu-id="dba86-238">Typ</span><span class="sxs-lookup"><span data-stu-id="dba86-238">Type</span></span>|  
|----------------|---------------|--------|  
|<span data-ttu-id="dba86-239">Nagłówki</span><span class="sxs-lookup"><span data-stu-id="dba86-239">headers</span></span>|<span data-ttu-id="dba86-240">Witaj nagłówki odpowiedzi http hello.</span><span class="sxs-lookup"><span data-stu-id="dba86-240">hello headers of hello http response.</span></span>|<span data-ttu-id="dba86-241">Obiekt</span><span class="sxs-lookup"><span data-stu-id="dba86-241">Object</span></span>|  
|<span data-ttu-id="dba86-242">Treści</span><span class="sxs-lookup"><span data-stu-id="dba86-242">body</span></span>|<span data-ttu-id="dba86-243">Treść Hello hello odpowiedzi http.</span><span class="sxs-lookup"><span data-stu-id="dba86-243">hello body of hello http response.</span></span>|<span data-ttu-id="dba86-244">Obiekt</span><span class="sxs-lookup"><span data-stu-id="dba86-244">Object</span></span>|  
  
## <a name="api-connection-trigger"></a><span data-ttu-id="dba86-245">Połączenie z interfejsem API wyzwalacza</span><span class="sxs-lookup"><span data-stu-id="dba86-245">API Connection trigger</span></span>  

<span data-ttu-id="dba86-246">Witaj interfejsu API połączenia wyzwalacz jest podobne wyzwalacza HTTP toohello w jego podstawowych funkcji.</span><span class="sxs-lookup"><span data-stu-id="dba86-246">hello API connection trigger is similar toohello HTTP trigger in its basic functionality.</span></span> <span data-ttu-id="dba86-247">Jednak parametry hello identyfikowanie akcji hello są różne.</span><span class="sxs-lookup"><span data-stu-id="dba86-247">However, hello parameters for identifying hello action are different.</span></span> <span data-ttu-id="dba86-248">Oto przykład:</span><span class="sxs-lookup"><span data-stu-id="dba86-248">Here is an example:</span></span>  
  
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

|<span data-ttu-id="dba86-249">Nazwa elementu</span><span class="sxs-lookup"><span data-stu-id="dba86-249">Element name</span></span>|<span data-ttu-id="dba86-250">Wymagane</span><span class="sxs-lookup"><span data-stu-id="dba86-250">Required</span></span>|<span data-ttu-id="dba86-251">Typ</span><span class="sxs-lookup"><span data-stu-id="dba86-251">Type</span></span>|<span data-ttu-id="dba86-252">Opis</span><span class="sxs-lookup"><span data-stu-id="dba86-252">Description</span></span>|  
|----------------|------------|--------|---------------|  
|<span data-ttu-id="dba86-253">Host</span><span class="sxs-lookup"><span data-stu-id="dba86-253">host</span></span>|<span data-ttu-id="dba86-254">Tak</span><span class="sxs-lookup"><span data-stu-id="dba86-254">Yes</span></span>||<span data-ttu-id="dba86-255">Witaj ApiApp hostowana bramy i identyfikator.</span><span class="sxs-lookup"><span data-stu-id="dba86-255">hello ApiApp hosted gateway and id.</span></span>|  
|<span data-ttu-id="dba86-256">— Metoda</span><span class="sxs-lookup"><span data-stu-id="dba86-256">method</span></span>|<span data-ttu-id="dba86-257">Tak</span><span class="sxs-lookup"><span data-stu-id="dba86-257">Yes</span></span>|<span data-ttu-id="dba86-258">Ciąg</span><span class="sxs-lookup"><span data-stu-id="dba86-258">String</span></span>|<span data-ttu-id="dba86-259">Może być jedną z następujących metod HTTP hello: **UZYSKAĆ**, **POST**, **PUT**, **usunąć**, **poprawka**, lub  **HEAD**</span><span class="sxs-lookup"><span data-stu-id="dba86-259">Can be one of hello following HTTP methods: **GET**, **POST**, **PUT**, **DELETE**, **PATCH**, or **HEAD**</span></span>|  
|<span data-ttu-id="dba86-260">— zapytania</span><span class="sxs-lookup"><span data-stu-id="dba86-260">queries</span></span>|<span data-ttu-id="dba86-261">Nie</span><span class="sxs-lookup"><span data-stu-id="dba86-261">No</span></span>|<span data-ttu-id="dba86-262">Obiekt</span><span class="sxs-lookup"><span data-stu-id="dba86-262">Object</span></span>|<span data-ttu-id="dba86-263">Reprezentuje hello zapytania parametry toobe dodać toohello adresu URL.</span><span class="sxs-lookup"><span data-stu-id="dba86-263">Represents hello query parameters toobe added toohello URL.</span></span> <span data-ttu-id="dba86-264">Na przykład `"queries" : { "api-version": "2015-02-01" }` dodaje `?api-version=2015-02-01` toohello adresu URL.</span><span class="sxs-lookup"><span data-stu-id="dba86-264">For example, `"queries" : { "api-version": "2015-02-01" }` adds `?api-version=2015-02-01` toohello URL.</span></span>|  
|<span data-ttu-id="dba86-265">Nagłówki</span><span class="sxs-lookup"><span data-stu-id="dba86-265">headers</span></span>|<span data-ttu-id="dba86-266">Nie</span><span class="sxs-lookup"><span data-stu-id="dba86-266">No</span></span>|<span data-ttu-id="dba86-267">Obiekt</span><span class="sxs-lookup"><span data-stu-id="dba86-267">Object</span></span>|<span data-ttu-id="dba86-268">Reprezentuje wszystkich nagłówków hello, które są wysyłane żądania toohello.</span><span class="sxs-lookup"><span data-stu-id="dba86-268">Represents each of hello headers that is sent toohello request.</span></span> <span data-ttu-id="dba86-269">Na przykład tooset hello język i typ żądania:`"headers" : { "Accept-Language": "en-us",  "Content-Type": "application/json" }`</span><span class="sxs-lookup"><span data-stu-id="dba86-269">For example, tooset hello language and type on a request: `"headers" : { "Accept-Language": "en-us",  "Content-Type": "application/json" }`</span></span>|  
|<span data-ttu-id="dba86-270">Treści</span><span class="sxs-lookup"><span data-stu-id="dba86-270">body</span></span>|<span data-ttu-id="dba86-271">Nie</span><span class="sxs-lookup"><span data-stu-id="dba86-271">No</span></span>|<span data-ttu-id="dba86-272">Obiekt</span><span class="sxs-lookup"><span data-stu-id="dba86-272">Object</span></span>|<span data-ttu-id="dba86-273">Reprezentuje ładunek hello, wysyłany toohello punktu końcowego.</span><span class="sxs-lookup"><span data-stu-id="dba86-273">Represents hello payload that is sent toohello endpoint.</span></span>|  
|<span data-ttu-id="dba86-274">retryPolicy</span><span class="sxs-lookup"><span data-stu-id="dba86-274">retryPolicy</span></span>|<span data-ttu-id="dba86-275">Nie</span><span class="sxs-lookup"><span data-stu-id="dba86-275">No</span></span>|<span data-ttu-id="dba86-276">Obiekt</span><span class="sxs-lookup"><span data-stu-id="dba86-276">Object</span></span>|<span data-ttu-id="dba86-277">Umożliwia zachowanie ponawiania hello toocustomize 4xx lub 5xx błędów.</span><span class="sxs-lookup"><span data-stu-id="dba86-277">Allows you toocustomize hello retry behavior for 4xx or 5xx errors.</span></span>|  
|<span data-ttu-id="dba86-278">Uwierzytelnianie</span><span class="sxs-lookup"><span data-stu-id="dba86-278">authentication</span></span>|<span data-ttu-id="dba86-279">Nie</span><span class="sxs-lookup"><span data-stu-id="dba86-279">No</span></span>|<span data-ttu-id="dba86-280">Obiekt</span><span class="sxs-lookup"><span data-stu-id="dba86-280">Object</span></span>|<span data-ttu-id="dba86-281">Reprezentuje metodę hello hello żądania uwierzytelniania.</span><span class="sxs-lookup"><span data-stu-id="dba86-281">Represents hello method that hello request should be authenticated.</span></span> <span data-ttu-id="dba86-282">Aby uzyskać więcej informacji na ten obiekt, zobacz [uwierzytelniania połączeń wychodzących harmonogramu](https://docs.microsoft.com/azure/scheduler/scheduler-outbound-authentication)</span><span class="sxs-lookup"><span data-stu-id="dba86-282">For details on this object, see [Scheduler Outbound Authentication](https://docs.microsoft.com/azure/scheduler/scheduler-outbound-authentication)</span></span>|  
  
<span data-ttu-id="dba86-283">Witaj właściwości hosta są:</span><span class="sxs-lookup"><span data-stu-id="dba86-283">hello properties for host are:</span></span>  
  
|<span data-ttu-id="dba86-284">Nazwa elementu</span><span class="sxs-lookup"><span data-stu-id="dba86-284">Element name</span></span>|<span data-ttu-id="dba86-285">Wymagane</span><span class="sxs-lookup"><span data-stu-id="dba86-285">Required</span></span>|<span data-ttu-id="dba86-286">Opis</span><span class="sxs-lookup"><span data-stu-id="dba86-286">Description</span></span>|  
|----------------|------------|---------------|  
|<span data-ttu-id="dba86-287">runtimeUrl interfejsu API</span><span class="sxs-lookup"><span data-stu-id="dba86-287">api runtimeUrl</span></span>|<span data-ttu-id="dba86-288">Tak</span><span class="sxs-lookup"><span data-stu-id="dba86-288">Yes</span></span>|<span data-ttu-id="dba86-289">punkt końcowy Hello hello zarządzanego interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="dba86-289">hello endpoint of hello managed API.</span></span>|  
|<span data-ttu-id="dba86-290">Nazwa połączenia</span><span class="sxs-lookup"><span data-stu-id="dba86-290">connection name</span></span>||<span data-ttu-id="dba86-291">Musi być odwołanie tooa parametr o nazwie `$connection` i jest nazwą hello hello zarządzane połączenia interfejsu API, które hello używa przepływu pracy.</span><span class="sxs-lookup"><span data-stu-id="dba86-291">Must be a reference tooa parameter called `$connection` and is hello name of hello managed API connection that hello workflow uses.</span></span>|
  
<span data-ttu-id="dba86-292">dane wyjściowe Hello wyzwalacza połączenia interfejsu API są:</span><span class="sxs-lookup"><span data-stu-id="dba86-292">hello outputs of an API connection trigger are:</span></span>
  
|<span data-ttu-id="dba86-293">Nazwa elementu</span><span class="sxs-lookup"><span data-stu-id="dba86-293">Element name</span></span>|<span data-ttu-id="dba86-294">Typ</span><span class="sxs-lookup"><span data-stu-id="dba86-294">Type</span></span>|<span data-ttu-id="dba86-295">Opis</span><span class="sxs-lookup"><span data-stu-id="dba86-295">Description</span></span>|  
|----------------|--------|---------------|  
|<span data-ttu-id="dba86-296">Nagłówki</span><span class="sxs-lookup"><span data-stu-id="dba86-296">headers</span></span>|<span data-ttu-id="dba86-297">Obiekt</span><span class="sxs-lookup"><span data-stu-id="dba86-297">Object</span></span>|<span data-ttu-id="dba86-298">Witaj nagłówki odpowiedzi http hello.</span><span class="sxs-lookup"><span data-stu-id="dba86-298">hello headers of hello http response.</span></span>|  
|<span data-ttu-id="dba86-299">Treści</span><span class="sxs-lookup"><span data-stu-id="dba86-299">body</span></span>|<span data-ttu-id="dba86-300">Obiekt</span><span class="sxs-lookup"><span data-stu-id="dba86-300">Object</span></span>|<span data-ttu-id="dba86-301">Treść Hello hello odpowiedzi http.</span><span class="sxs-lookup"><span data-stu-id="dba86-301">hello body of hello http response.</span></span>|  
  
## <a name="httpwebhook-trigger"></a><span data-ttu-id="dba86-302">Wyzwalacz HTTPWebhook</span><span class="sxs-lookup"><span data-stu-id="dba86-302">HTTPWebhook trigger</span></span>  

<span data-ttu-id="dba86-303">Otwiera wyzwalacza HTTPWebhook Hello punktu końcowego, podobne toohello wyzwalacza ręczne, ale hello wyzwalacza HTTPWebhook również uwidacznia tooa określony adres URL tooregister i wyrejestrować.</span><span class="sxs-lookup"><span data-stu-id="dba86-303">hello HTTPWebhook trigger opens an endpoint, similar toohello manual trigger, but hello HTTPWebhook trigger also calls out tooa specified URL tooregister and unregister.</span></span> <span data-ttu-id="dba86-304">Oto przykład co wyzwalacz HTTPWebhook może wyglądać tak:</span><span class="sxs-lookup"><span data-stu-id="dba86-304">Here's an example of what an HTTPWebhook trigger might look like:</span></span>  

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

<span data-ttu-id="dba86-305">Wiele z tych sekcji są opcjonalne i zachowanie hello hello elementu Webhook jest zależna od sekcje są udostępniane lub pominięta.</span><span class="sxs-lookup"><span data-stu-id="dba86-305">Many of these sections are optional, and hello behavior of hello Webhook depends on which sections are provided or omitted.</span></span>  
<span data-ttu-id="dba86-306">właściwości elementu Webhook Hello są następujące:</span><span class="sxs-lookup"><span data-stu-id="dba86-306">hello properties of a Webhook are as follows:</span></span>  
  
|<span data-ttu-id="dba86-307">Nazwa elementu</span><span class="sxs-lookup"><span data-stu-id="dba86-307">Element name</span></span>|<span data-ttu-id="dba86-308">Wymagane</span><span class="sxs-lookup"><span data-stu-id="dba86-308">Required</span></span>|<span data-ttu-id="dba86-309">Opis</span><span class="sxs-lookup"><span data-stu-id="dba86-309">Description</span></span>|  
|----------------|------------|---------------|  
|<span data-ttu-id="dba86-310">Subskrypcja</span><span class="sxs-lookup"><span data-stu-id="dba86-310">subscribe</span></span>|<span data-ttu-id="dba86-311">Nie</span><span class="sxs-lookup"><span data-stu-id="dba86-311">No</span></span>|<span data-ttu-id="dba86-312">Witaj wychodzące żądania, które jest wywoływane, gdy wyzwalacz hello jest tworzony i wykonuje hello początkowej rejestracji.</span><span class="sxs-lookup"><span data-stu-id="dba86-312">hello outgoing request that is called when hello trigger is created and performs hello initial registration.</span></span>|  
|<span data-ttu-id="dba86-313">Anulowanie subskrypcji</span><span class="sxs-lookup"><span data-stu-id="dba86-313">unsubscribe</span></span>|<span data-ttu-id="dba86-314">Nie</span><span class="sxs-lookup"><span data-stu-id="dba86-314">No</span></span>|<span data-ttu-id="dba86-315">Witaj wychodzące żądanie usunięcia hello wyzwalacza.</span><span class="sxs-lookup"><span data-stu-id="dba86-315">hello outgoing request when hello trigger is deleted.</span></span>|  
  
-   <span data-ttu-id="dba86-316">**Subskrypcja** jest Witaj wychodzące połączenia, który wprowadził toostart tooevents nasłuchiwania.</span><span class="sxs-lookup"><span data-stu-id="dba86-316">**Subscribe** is hello outgoing call that's made toostart listening tooevents.</span></span> <span data-ttu-id="dba86-317">To wywołanie rozpoczyna się od hello są tego samego zestawu parametrów, które hello normalne akcji HTTP.</span><span class="sxs-lookup"><span data-stu-id="dba86-317">This call starts with hello same set of parameters that hello normal HTTP actions do.</span></span> <span data-ttu-id="dba86-318">Ten wychodzących wywołanie żadnych hello czas przepływu pracy zmiany w dowolny sposób, na przykład po każdej zmianie poświadczeń hello są wycofane lub zmiany parametrów wejściowych hello wyzwalacza.</span><span class="sxs-lookup"><span data-stu-id="dba86-318">This outgoing call is made any time hello workflow changes in any way, for example, whenever hello credentials are rolled, or hello trigger's input parameters change.</span></span>
  
    <span data-ttu-id="dba86-319">toosupport to wywołanie, jest nowa funkcja: `@listCallbackUrl()`.</span><span class="sxs-lookup"><span data-stu-id="dba86-319">toosupport this call, there is a new function: `@listCallbackUrl()`.</span></span> <span data-ttu-id="dba86-320">Ta funkcja zwraca unikatowy adres URL dla tego wyzwalacza określonych w tym przepływie pracy.</span><span class="sxs-lookup"><span data-stu-id="dba86-320">This function returns a unique URL for this specific trigger in this workflow.</span></span> <span data-ttu-id="dba86-321">Reprezentuje hello Unikatowy identyfikator dla punktów końcowych hello, używających hello usługi REST.</span><span class="sxs-lookup"><span data-stu-id="dba86-321">It represents hello unique identifier for hello endpoints that use hello Service REST.</span></span>  
  
-   <span data-ttu-id="dba86-322">**Anulowanie subskrypcji** jest wywoływane, gdy operacja renderuje tego wyzwalacza nieprawidłowe, w tym:</span><span class="sxs-lookup"><span data-stu-id="dba86-322">**Unsubscribe** is called when an operation renders this trigger invalid, including:</span></span>  
  
    -   <span data-ttu-id="dba86-323">Usuwanie lub wyłączanie hello wyzwalacza</span><span class="sxs-lookup"><span data-stu-id="dba86-323">Deleting or disabling hello trigger</span></span>  
  
    -   <span data-ttu-id="dba86-324">Usuwanie lub wyłączanie hello przepływu pracy</span><span class="sxs-lookup"><span data-stu-id="dba86-324">Deleting or disabling hello workflow</span></span>  
  
    -   <span data-ttu-id="dba86-325">Usuwanie lub wyłączanie hello subskrypcji</span><span class="sxs-lookup"><span data-stu-id="dba86-325">Deleting or disabling hello subscription</span></span>  
  
    <span data-ttu-id="dba86-326">Aplikacja logiki Hello automatycznie wywołuje hello subskrypcję akcji.</span><span class="sxs-lookup"><span data-stu-id="dba86-326">hello logic app automatically calls hello unsubscribe action.</span></span> <span data-ttu-id="dba86-327">Parametry Hello są funkcja toothis hello sam hello wyzwalacza HTTP.</span><span class="sxs-lookup"><span data-stu-id="dba86-327">hello parameters toothis function are hello same as hello HTTP trigger.</span></span>  
  
    <span data-ttu-id="dba86-328">Witaj dane wyjściowe wyzwalacza HTTPWebhook hello są hello treść żądania przychodzące hello:</span><span class="sxs-lookup"><span data-stu-id="dba86-328">hello outputs of hello HTTPWebhook trigger are hello contents of hello incoming request:</span></span>  
  
|<span data-ttu-id="dba86-329">Nazwa elementu</span><span class="sxs-lookup"><span data-stu-id="dba86-329">Element name</span></span>|<span data-ttu-id="dba86-330">Typ</span><span class="sxs-lookup"><span data-stu-id="dba86-330">Type</span></span>|<span data-ttu-id="dba86-331">Opis</span><span class="sxs-lookup"><span data-stu-id="dba86-331">Description</span></span>|  
|-----------------|--------|---------------|  
|<span data-ttu-id="dba86-332">Nagłówki</span><span class="sxs-lookup"><span data-stu-id="dba86-332">headers</span></span>|<span data-ttu-id="dba86-333">Obiekt</span><span class="sxs-lookup"><span data-stu-id="dba86-333">Object</span></span>|<span data-ttu-id="dba86-334">nagłówki Hello hello żądania http.</span><span class="sxs-lookup"><span data-stu-id="dba86-334">hello headers of hello http request.</span></span>|  
|<span data-ttu-id="dba86-335">Treści</span><span class="sxs-lookup"><span data-stu-id="dba86-335">body</span></span>|<span data-ttu-id="dba86-336">Obiekt</span><span class="sxs-lookup"><span data-stu-id="dba86-336">Object</span></span>|<span data-ttu-id="dba86-337">Treść Hello hello żądania http.</span><span class="sxs-lookup"><span data-stu-id="dba86-337">hello body of hello http request.</span></span>|  

<span data-ttu-id="dba86-338">Można określić limity akcji elementu webhook w hello taki sam jak [limity asynchroniczne HTTP](#asynchronous-limits).</span><span class="sxs-lookup"><span data-stu-id="dba86-338">Limits on a webhook action can be specified in hello same manner as [HTTP Asynchronous Limits](#asynchronous-limits).</span></span>
  

## <a name="conditions"></a><span data-ttu-id="dba86-339">Warunki</span><span class="sxs-lookup"><span data-stu-id="dba86-339">Conditions</span></span>  

<span data-ttu-id="dba86-340">Dla dowolnego wyzwalacza można użyć co najmniej jeden toodetermine warunki czy uruchamiania przepływu pracy hello lub nie.</span><span class="sxs-lookup"><span data-stu-id="dba86-340">For any trigger, you can use one or more conditions toodetermine whether hello workflow should run or not.</span></span> <span data-ttu-id="dba86-341">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="dba86-341">For example:</span></span>  

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

<span data-ttu-id="dba86-342">W takim przypadku hello tylko wyzwalaczy raportu podczas przepływu hello `sendReports` parametr ma wartość tootrue.</span><span class="sxs-lookup"><span data-stu-id="dba86-342">In this case, hello report only triggers while hello workflow's `sendReports` parameter is set tootrue.</span></span> <span data-ttu-id="dba86-343">Na koniec warunków może odwoływać się hello kod stanu hello wyzwalacza.</span><span class="sxs-lookup"><span data-stu-id="dba86-343">Finally, conditions may reference hello status code of hello trigger.</span></span> <span data-ttu-id="dba86-344">Na przykład należy można rozpocząć wyłączyć przepływ pracy tylko w przypadku witryny sieci Web zwraca kod stanu 500, w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="dba86-344">For example, you could kick off a workflow only when your website returns a status code 500, as follows:</span></span>
  
```  
"conditions": [  
        {  
          "expression": "@equals(triggers().code, 'InternalServerError')"  
        }  
      ]  
```  
  
> [!NOTE]  
> <span data-ttu-id="dba86-345">Gdy dowolne wyrażenie odwołuje się kod stanu hello wyzwalacza hello \(w żaden sposób\), hello domyślne zachowanie \(wyzwalacza tylko na 200 \(OK\) \) zostanie zastąpiony.</span><span class="sxs-lookup"><span data-stu-id="dba86-345">When any expression references hello status code of hello trigger \(in any way\), hello default behavior \(trigger only on 200 \(OK\)\) is replaced.</span></span> <span data-ttu-id="dba86-346">Na przykład, jeśli chcesz tootrigger na kod stanu 200 i kod stanu 201 masz tooinclude: `@or(equals(triggers().code, 200),equals(triggers().code,201))` jako warunek.</span><span class="sxs-lookup"><span data-stu-id="dba86-346">For example, if you want tootrigger on both status code 200 and status code 201, you have tooinclude: `@or(equals(triggers().code, 200),equals(triggers().code,201))` as your condition.</span></span>  
  
## <a name="start-multiple-runs-for-a-request"></a><span data-ttu-id="dba86-347">Uruchom wielu uruchomień dla żądania</span><span class="sxs-lookup"><span data-stu-id="dba86-347">Start multiple runs for a request</span></span>

<span data-ttu-id="dba86-348">tookick poza wielu uruchomień dla pojedynczego żądania `splitOn` jest przydatne, na przykład, jeśli chcesz toopoll punktu końcowego, który może mieć wiele nowych elementów między interwałami sondowania.</span><span class="sxs-lookup"><span data-stu-id="dba86-348">tookick off multiple runs for a single request, `splitOn` is useful, for example, when you want toopoll an endpoint that can have multiple new items between polling intervals.</span></span>
  
<span data-ttu-id="dba86-349">Z `splitOn`, określ właściwość hello ładunku odpowiedzi hello zawierający hello tablicę elementów, z których każdy ma toostart toouse Uruchom hello wyzwalacza.</span><span class="sxs-lookup"><span data-stu-id="dba86-349">With `splitOn`, you specify hello property inside hello response payload that contains hello array of items, each of which you want toouse toostart a run of hello trigger.</span></span> <span data-ttu-id="dba86-350">Załóżmy na przykład, że masz interfejs API, który zwraca powitania po odpowiedzi:</span><span class="sxs-lookup"><span data-stu-id="dba86-350">For example, imagine you have an API that returns hello following response:</span></span>  
  
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
  
<span data-ttu-id="dba86-351">Aplikację logiki tylko musi hello wierszy zawartości, więc można konstruować wyzwalacz tak jak ten przykład:</span><span class="sxs-lookup"><span data-stu-id="dba86-351">Your logic app only needs hello Rows content, so you can construct your trigger like this example:</span></span>  
  
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
  
<span data-ttu-id="dba86-352">Następnie w definicji przepływu pracy hello, `@triggerBody().name` zwraca `mycoolrow` dla pierwszego uruchomienia hello i `another row` dla hello drugim przebiegu.</span><span class="sxs-lookup"><span data-stu-id="dba86-352">Then, in hello workflow definition, `@triggerBody().name` returns `mycoolrow` for hello first run, and `another row` for hello second run.</span></span> <span data-ttu-id="dba86-353">wygląd danych wyjściowych wyzwalacza Hello tak jak ten przykład:</span><span class="sxs-lookup"><span data-stu-id="dba86-353">hello trigger outputs look like this example:</span></span>  
  
```json
{
    "body" : {
        "id" : 938109381,
        "name" : "another row"
    }
}
```

<span data-ttu-id="dba86-354">Dlatego jeśli używasz `SplitOn`, nie można pobrać właściwości hello, które są poza hello tablicy, w tym przypadku hello `Status` pola.</span><span class="sxs-lookup"><span data-stu-id="dba86-354">So if you use `SplitOn`, you can't get hello properties that are outside hello array, in this case, hello `Status` field.</span></span>  
  
> [!NOTE]  
> <span data-ttu-id="dba86-355">W tym przykładzie używamy hello `?` tooavoid stanie operator toobe awarii, jeśli hello `Rows` nie ma właściwości.</span><span class="sxs-lookup"><span data-stu-id="dba86-355">In this example, we use hello `?` operator toobe able tooavoid a failure if hello `Rows` property is not present.</span></span> 
  
## <a name="single-run-instance"></a><span data-ttu-id="dba86-356">Pojedyncze wystąpienie wykonywania</span><span class="sxs-lookup"><span data-stu-id="dba86-356">Single run instance</span></span>

<span data-ttu-id="dba86-357">Można skonfigurować wyzwalacze, które ma fire tooonly właściwości cyklu, jeśli wszystkie aktywnej przebiegi została ukończona.</span><span class="sxs-lookup"><span data-stu-id="dba86-357">You can configure triggers that have a recurrence property tooonly fire if all active runs have completed.</span></span> <span data-ttu-id="dba86-358">W przypadku podczas uruchamiania w trakcie zaplanowanego cyklu wyzwalacz hello pomija i czekać na powitania następnego zaplanowanego cyklu interwału toocheck ponownie.</span><span class="sxs-lookup"><span data-stu-id="dba86-358">If a scheduled recurrence occurs while there is an in-progress run, hello trigger skips and waits until hello next scheduled recurrence interval toocheck again.</span></span>

<span data-ttu-id="dba86-359">Można to ustawienie można skonfigurować za pomocą opcji operacji hello:</span><span class="sxs-lookup"><span data-stu-id="dba86-359">You can configure this setting through hello operation options:</span></span>

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

## <a name="types-and-inputs"></a><span data-ttu-id="dba86-360">Typy i dane wejściowe</span><span class="sxs-lookup"><span data-stu-id="dba86-360">Types and inputs</span></span>  

<span data-ttu-id="dba86-361">Istnieje wiele typów działań, każde z nich unikatowe zachowanie.</span><span class="sxs-lookup"><span data-stu-id="dba86-361">There are many types of actions, each with unique behavior.</span></span> <span data-ttu-id="dba86-362">Akcje kolekcji może zawierać wielu akcji w obrębie samego.</span><span class="sxs-lookup"><span data-stu-id="dba86-362">Collection actions may contain many other actions within itself.</span></span>

### <a name="standard-actions"></a><span data-ttu-id="dba86-363">Działania standardowe</span><span class="sxs-lookup"><span data-stu-id="dba86-363">Standard actions</span></span>  

-   <span data-ttu-id="dba86-364">**HTTP** ta akcja wymaga punktu końcowego HTTP sieci web.</span><span class="sxs-lookup"><span data-stu-id="dba86-364">**HTTP** This action calls an HTTP web endpoint.</span></span>  
  
-   <span data-ttu-id="dba86-365">**ApiConnection** \- ta akcja działa jak hello akcji HTTP, ale używa hello API zarządzany przez firmę Microsoft.</span><span class="sxs-lookup"><span data-stu-id="dba86-365">**ApiConnection** \- This action behaves like hello HTTP action, but uses hello Microsoft-managed APIs.</span></span>  
  
-   <span data-ttu-id="dba86-366">**ApiConnectionWebhook** \- jak HTTPWebhook, ale używa hello API zarządzany przez firmę Microsoft.</span><span class="sxs-lookup"><span data-stu-id="dba86-366">**ApiConnectionWebhook** \- Like HTTPWebhook, but uses hello Microsoft-managed APIs.</span></span>  
  
-   <span data-ttu-id="dba86-367">**Odpowiedź** \- tej akcji określa odpowiedzi dla połączenia przychodzącego.</span><span class="sxs-lookup"><span data-stu-id="dba86-367">**Response** \- This action defines a response for an incoming call.</span></span>  
  
-   <span data-ttu-id="dba86-368">**Poczekaj** \- ta akcja proste czeka stałą lub określonego czasu.</span><span class="sxs-lookup"><span data-stu-id="dba86-368">**Wait** \- This simple action waits a fixed amount of time or until a specific time.</span></span>  
  
-   <span data-ttu-id="dba86-369">**Przepływ pracy** \- tej akcji reprezentuje zagnieżdżony przepływ pracy.</span><span class="sxs-lookup"><span data-stu-id="dba86-369">**Workflow** \- This action represents a nested workflow.</span></span>  

-   <span data-ttu-id="dba86-370">**Funkcja** \- tej akcji reprezentuje funkcję platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="dba86-370">**Function** \- This action represents an Azure Function.</span></span>

### <a name="collection-actions"></a><span data-ttu-id="dba86-371">Akcje kolekcji</span><span class="sxs-lookup"><span data-stu-id="dba86-371">Collection actions</span></span>

-   <span data-ttu-id="dba86-372">**Zakres** \- ta akcja jest logiczne grupowanie innych działań.</span><span class="sxs-lookup"><span data-stu-id="dba86-372">**Scope** \- This action is a logical grouping of other actions.</span></span>

-   <span data-ttu-id="dba86-373">**Warunek** \- ta akcja oblicza wyrażenie i wykonuje hello odpowiednich wyników w oddziale firmy.</span><span class="sxs-lookup"><span data-stu-id="dba86-373">**Condition** \- This action evaluates an expression and executes hello corresponding result branch.</span></span>

-   <span data-ttu-id="dba86-374">**Instrukcja ForEach** \- ta akcja pętli iteruje tablicy i wykonuje akcje wewnętrzny dla każdego elementu.</span><span class="sxs-lookup"><span data-stu-id="dba86-374">**ForEach** \- This looping action iterates through an array and performs inner actions for each item.</span></span>

-   <span data-ttu-id="dba86-375">**Dopóki** \- ta akcja pętli wykonuje działania wewnętrzny dopóki tootrue powoduje warunek.</span><span class="sxs-lookup"><span data-stu-id="dba86-375">**Until** \- This looping action executes inner actions until a condition results tootrue.</span></span>
  
<span data-ttu-id="dba86-376">Każdy typ działania ma inny zestaw **dane wejściowe** definiującą zachowanie akcji.</span><span class="sxs-lookup"><span data-stu-id="dba86-376">Each type of action has a different set of **inputs** that define an action's behavior.</span></span>  
  
## <a name="http-action"></a><span data-ttu-id="dba86-377">Akcja HTTP</span><span class="sxs-lookup"><span data-stu-id="dba86-377">HTTP action</span></span>  

<span data-ttu-id="dba86-378">HTTP działania Wywołaj określony punkt końcowy i toodetermine odpowiedzi hello Sprawdź, czy powinno być ono uruchomione hello przepływu pracy.</span><span class="sxs-lookup"><span data-stu-id="dba86-378">HTTP actions call a specified endpoint and check hello response toodetermine whether hello workflow should run.</span></span> <span data-ttu-id="dba86-379">Witaj **dane wejściowe** obiektu przyjmuje hello zbiór wywołania hello HTTP tooconstruct wymaganych parametrów:</span><span class="sxs-lookup"><span data-stu-id="dba86-379">hello **inputs** object takes hello set of parameters required tooconstruct hello HTTP call:</span></span>  
  
|<span data-ttu-id="dba86-380">Nazwa elementu</span><span class="sxs-lookup"><span data-stu-id="dba86-380">Element name</span></span>|<span data-ttu-id="dba86-381">Wymagane</span><span class="sxs-lookup"><span data-stu-id="dba86-381">Required</span></span>|<span data-ttu-id="dba86-382">Typ</span><span class="sxs-lookup"><span data-stu-id="dba86-382">Type</span></span>|<span data-ttu-id="dba86-383">Opis</span><span class="sxs-lookup"><span data-stu-id="dba86-383">Description</span></span>|  
|----------------|------------|--------|---------------|  
|<span data-ttu-id="dba86-384">— Metoda</span><span class="sxs-lookup"><span data-stu-id="dba86-384">method</span></span>|<span data-ttu-id="dba86-385">Tak</span><span class="sxs-lookup"><span data-stu-id="dba86-385">Yes</span></span>|<span data-ttu-id="dba86-386">Ciąg</span><span class="sxs-lookup"><span data-stu-id="dba86-386">String</span></span>|<span data-ttu-id="dba86-387">Może być jedną z następujących metod HTTP hello: **UZYSKAĆ**, **POST**, **PUT**, **usunąć**, **poprawka**, lub  **HEAD**</span><span class="sxs-lookup"><span data-stu-id="dba86-387">Can be one of hello following HTTP methods: **GET**, **POST**, **PUT**, **DELETE**, **PATCH**, or **HEAD**</span></span>|  
|<span data-ttu-id="dba86-388">Identyfikator URI</span><span class="sxs-lookup"><span data-stu-id="dba86-388">uri</span></span>|<span data-ttu-id="dba86-389">Tak</span><span class="sxs-lookup"><span data-stu-id="dba86-389">Yes</span></span>|<span data-ttu-id="dba86-390">Ciąg</span><span class="sxs-lookup"><span data-stu-id="dba86-390">String</span></span>|<span data-ttu-id="dba86-391">Witaj punkt końcowy http lub https, który jest wywoływana.</span><span class="sxs-lookup"><span data-stu-id="dba86-391">hello http or https endpoint that is called.</span></span> <span data-ttu-id="dba86-392">Maksymalna długość wynosi 2 kilobajtów.</span><span class="sxs-lookup"><span data-stu-id="dba86-392">Maximum length is 2 kilobytes.</span></span>|  
|<span data-ttu-id="dba86-393">— zapytania</span><span class="sxs-lookup"><span data-stu-id="dba86-393">queries</span></span>|<span data-ttu-id="dba86-394">Nie</span><span class="sxs-lookup"><span data-stu-id="dba86-394">No</span></span>|<span data-ttu-id="dba86-395">Obiekt</span><span class="sxs-lookup"><span data-stu-id="dba86-395">Object</span></span>|<span data-ttu-id="dba86-396">Reprezentuje adres URL toohello tooadd hello kwerendy parametrów.</span><span class="sxs-lookup"><span data-stu-id="dba86-396">Represents hello query parameters tooadd toohello URL.</span></span> <span data-ttu-id="dba86-397">Na przykład `"queries" : { "api-version": "2015-02-01" }` dodaje `?api-version=2015-02-01` toohello adresu URL.</span><span class="sxs-lookup"><span data-stu-id="dba86-397">For example, `"queries" : { "api-version": "2015-02-01" }` adds `?api-version=2015-02-01` toohello URL.</span></span>|  
|<span data-ttu-id="dba86-398">Nagłówki</span><span class="sxs-lookup"><span data-stu-id="dba86-398">headers</span></span>|<span data-ttu-id="dba86-399">Nie</span><span class="sxs-lookup"><span data-stu-id="dba86-399">No</span></span>|<span data-ttu-id="dba86-400">Obiekt</span><span class="sxs-lookup"><span data-stu-id="dba86-400">Object</span></span>|<span data-ttu-id="dba86-401">Reprezentuje wszystkich nagłówków hello, które są wysyłane żądania toohello.</span><span class="sxs-lookup"><span data-stu-id="dba86-401">Represents each of hello headers that is sent toohello request.</span></span> <span data-ttu-id="dba86-402">Na przykład tooset hello język i typ żądania:`"headers" : { "Accept-Language": "en-us",  "Content-Type": "application/json" }`</span><span class="sxs-lookup"><span data-stu-id="dba86-402">For example, tooset hello language and type on a request: `"headers" : { "Accept-Language": "en-us",  "Content-Type": "application/json" }`</span></span>|  
|<span data-ttu-id="dba86-403">Treści</span><span class="sxs-lookup"><span data-stu-id="dba86-403">body</span></span>|<span data-ttu-id="dba86-404">Nie</span><span class="sxs-lookup"><span data-stu-id="dba86-404">No</span></span>|<span data-ttu-id="dba86-405">Obiekt</span><span class="sxs-lookup"><span data-stu-id="dba86-405">Object</span></span>|<span data-ttu-id="dba86-406">Reprezentuje ładunek hello, wysyłany toohello punktu końcowego.</span><span class="sxs-lookup"><span data-stu-id="dba86-406">Represents hello payload that is sent toohello endpoint.</span></span>|  
|<span data-ttu-id="dba86-407">retryPolicy</span><span class="sxs-lookup"><span data-stu-id="dba86-407">retryPolicy</span></span>|<span data-ttu-id="dba86-408">Nie</span><span class="sxs-lookup"><span data-stu-id="dba86-408">No</span></span>|<span data-ttu-id="dba86-409">Obiekt</span><span class="sxs-lookup"><span data-stu-id="dba86-409">Object</span></span>|<span data-ttu-id="dba86-410">Umożliwia dostosowanie hello zachowanie ponownych prób dla 4xx lub 5xx błędów.</span><span class="sxs-lookup"><span data-stu-id="dba86-410">Lets you customize hello retry behavior for 4xx or 5xx errors.</span></span>|  
|<span data-ttu-id="dba86-411">operationsOptions</span><span class="sxs-lookup"><span data-stu-id="dba86-411">operationsOptions</span></span>|<span data-ttu-id="dba86-412">Nie</span><span class="sxs-lookup"><span data-stu-id="dba86-412">No</span></span>|<span data-ttu-id="dba86-413">Ciąg</span><span class="sxs-lookup"><span data-stu-id="dba86-413">String</span></span>|<span data-ttu-id="dba86-414">Definiuje zestaw hello toooverride specjalnego zachowania.</span><span class="sxs-lookup"><span data-stu-id="dba86-414">Defines hello set of special behaviors toooverride.</span></span>|  
|<span data-ttu-id="dba86-415">Uwierzytelnianie</span><span class="sxs-lookup"><span data-stu-id="dba86-415">authentication</span></span>|<span data-ttu-id="dba86-416">Nie</span><span class="sxs-lookup"><span data-stu-id="dba86-416">No</span></span>|<span data-ttu-id="dba86-417">Obiekt</span><span class="sxs-lookup"><span data-stu-id="dba86-417">Object</span></span>|<span data-ttu-id="dba86-418">Reprezentuje metodę hello hello żądania uwierzytelniania.</span><span class="sxs-lookup"><span data-stu-id="dba86-418">Represents hello method that hello request should be authenticated.</span></span> <span data-ttu-id="dba86-419">Aby uzyskać więcej informacji na ten obiekt, zobacz [uwierzytelniania połączeń wychodzących harmonogramu](https://docs.microsoft.com/azure/scheduler/scheduler-outbound-authentication).</span><span class="sxs-lookup"><span data-stu-id="dba86-419">For details on this object, see [Scheduler Outbound Authentication](https://docs.microsoft.com/azure/scheduler/scheduler-outbound-authentication).</span></span> <span data-ttu-id="dba86-420">Poza harmonogramem, jest jedna właściwość więcej obsługiwanych: `authority`.</span><span class="sxs-lookup"><span data-stu-id="dba86-420">Beyond scheduler, there is one more supported property: `authority`.</span></span> <span data-ttu-id="dba86-421">Domyślnie jest to `https://login.windows.net` gdy nie jest określony, ale możesz użyć innych grup odbiorców, takich jak`https://login.windows\-ppe.net`</span><span class="sxs-lookup"><span data-stu-id="dba86-421">By default, this is `https://login.windows.net` when not specified, but you can use a different audience like `https://login.windows\-ppe.net`</span></span>|  
  
<span data-ttu-id="dba86-422">Akcje HTTP \(i połączenie z interfejsem API\) Obsługa akcji ponów zasad.</span><span class="sxs-lookup"><span data-stu-id="dba86-422">HTTP actions \(and API Connection\) actions support retry policies.</span></span> <span data-ttu-id="dba86-423">Zasady ponawiania stosuje toointermittent błędów, jak stan HTTP jest określony kodów 408 429 i 5xx w wyjątki łączności tooany dodanie.</span><span class="sxs-lookup"><span data-stu-id="dba86-423">A retry policy applies toointermittent failures, characterized as HTTP status codes 408, 429, and 5xx, in addition tooany connectivity exceptions.</span></span> <span data-ttu-id="dba86-424">Ta zasada jest opisana przy użyciu hello *retryPolicy* obiekt zdefiniowany w sposób pokazany poniżej:</span><span class="sxs-lookup"><span data-stu-id="dba86-424">This policy is described using hello *retryPolicy* object defined as shown here:</span></span>
  
```json
"retryPolicy" : {
    "type": "<type-of-retry-policy>",
    "interval": <retry-interval>,
    "count": <number-of-retry-attempts>
}
```
  
<span data-ttu-id="dba86-425">Interwał ponawiania prób Hello jest określona w formacie ISO 8601 hello.</span><span class="sxs-lookup"><span data-stu-id="dba86-425">hello retry interval is specified in hello ISO 8601 format.</span></span> <span data-ttu-id="dba86-426">Ten interwał ma domyślne i minimalna wartość 20 sekund, podczas hello wartość maksymalna to jedna godzina.</span><span class="sxs-lookup"><span data-stu-id="dba86-426">This interval has a default and minimum value of 20 seconds, while hello maximum value is one hour.</span></span> <span data-ttu-id="dba86-427">Hello domyślne, a maksymalna liczba ponowień to cztery godziny.</span><span class="sxs-lookup"><span data-stu-id="dba86-427">hello default and maximum retry count is four hours.</span></span> <span data-ttu-id="dba86-428">Jeśli nie określono definicji zasad ponawiania hello, `fixed` strategii jest używany z domyślnej wartości interwału i liczba ponownych prób.</span><span class="sxs-lookup"><span data-stu-id="dba86-428">If hello retry policy definition is not specified, a `fixed` strategy is used with default retry count and interval values.</span></span> <span data-ttu-id="dba86-429">zasady ponawiania hello toodisable, ustaw jej typ zbyt`None`.</span><span class="sxs-lookup"><span data-stu-id="dba86-429">toodisable hello retry policy, set its type too`None`.</span></span>  
  
<span data-ttu-id="dba86-430">Na przykład hello następującej akcji ponowi próbę pobrano najnowsze wiadomości powitania dwa razy, jeśli występują sporadyczne awarie, dla wszystkich trzech wykonaniami, z 30-sekundowe opóźnienie między kolejnymi próbami:</span><span class="sxs-lookup"><span data-stu-id="dba86-430">For example, hello following action retries fetching hello latest news two times, if there are intermittent failures, for a total of three executions, with a 30-second delay between each attempt:</span></span>  
  
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
### <a name="asynchronous-patterns"></a><span data-ttu-id="dba86-431">Asynchroniczne wzorce</span><span class="sxs-lookup"><span data-stu-id="dba86-431">Asynchronous patterns</span></span>

<span data-ttu-id="dba86-432">Domyślnie wszystkie działania oparte na protokole HTTP obsługuje hello wzorzec standardowych operacji asynchronicznej.</span><span class="sxs-lookup"><span data-stu-id="dba86-432">By default, all HTTP-based actions support hello standard asynchronous operation pattern.</span></span> <span data-ttu-id="dba86-433">Dlatego jeśli powitania serwera zdalnego wskazuje Żądanie hello jest zaakceptowano do przetwarzania z 202 \(zaakceptowane\) odpowiedzi, aparat Logic Apps hello śledzi sondowania hello adres URL określony w nagłówku lokalizacji odpowiedź hello aż do osiągnięcia terminal Stan \(bez\-202 odpowiedzi\).</span><span class="sxs-lookup"><span data-stu-id="dba86-433">So if hello remote server indicates that hello request is accepted for processing with a 202 \(Accepted\) response, hello Logic Apps engine keeps polling hello URL specified in hello response's location header until reaching a terminal state \(a non\-202 response\).</span></span>  
  
<span data-ttu-id="dba86-434">zachowanie asynchroniczne hello toodisable wcześniej opisane, ustaw `DisableAsyncPattern` opcję hello akcji w danych wejściowych.</span><span class="sxs-lookup"><span data-stu-id="dba86-434">toodisable hello asynchronous behavior previously described, set a `DisableAsyncPattern` option in hello action inputs.</span></span> <span data-ttu-id="dba86-435">W takim przypadku dane wyjściowe hello akcji hello jest oparta na hello początkowej 202 odpowiedzi z serwera hello.</span><span class="sxs-lookup"><span data-stu-id="dba86-435">In this case, hello output of hello action is based on hello initial 202 response from hello server.</span></span>  
  
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

#### <a name="asynchronous-limits"></a><span data-ttu-id="dba86-436">Limity asynchroniczne</span><span class="sxs-lookup"><span data-stu-id="dba86-436">Asynchronous Limits</span></span>

<span data-ttu-id="dba86-437">Asynchroniczny wzorzec może być ograniczone w jego czas trwania tooa określonego interwału czasu.</span><span class="sxs-lookup"><span data-stu-id="dba86-437">An asynchronous pattern can be limited in its duration tooa specific time interval.</span></span>  <span data-ttu-id="dba86-438">Jeśli hello czas upływający bez osiągnięcia terminali stanu, zostaną oznaczone jako hello stan akcji hello `Cancelled` przy użyciu kodu `ActionTimedOut`.</span><span class="sxs-lookup"><span data-stu-id="dba86-438">If hello time interval elapses without reaching a terminal state, hello status of hello action will be marked `Cancelled` with a code of `ActionTimedOut`.</span></span>  <span data-ttu-id="dba86-439">limit czasu limit Hello jest określony w formacie ISO 8601.</span><span class="sxs-lookup"><span data-stu-id="dba86-439">hello limit timeout is specified in ISO 8601 format.</span></span>  <span data-ttu-id="dba86-440">Można określić limity z hello następującej składni:</span><span class="sxs-lookup"><span data-stu-id="dba86-440">Limits can be specified with hello following syntax:</span></span>

``` json
"<action-name>": {
    "type": "workflow|webhook|http|apiconnectionwebhook|apiconnection",
    "inputs": { },
    "limit": {
        "timeout": "PT10S"
    }
}
```
  
## <a name="api-connection"></a><span data-ttu-id="dba86-441">Połączenie z interfejsem API</span><span class="sxs-lookup"><span data-stu-id="dba86-441">API Connection</span></span>  

<span data-ttu-id="dba86-442">Połączenie z interfejsem API jest akcja, która odwołuje się do łącznika zarządzany przez firmę Microsoft.</span><span class="sxs-lookup"><span data-stu-id="dba86-442">API Connection is an action that references a Microsoft-managed connector.</span></span>
<span data-ttu-id="dba86-443">Ta akcja wymaga odwołania tooa prawidłowe połączenie, a informacje o hello interfejsu API i parametrów wymaganych.</span><span class="sxs-lookup"><span data-stu-id="dba86-443">This action requires a reference tooa valid connection, and information on hello API and parameters required.</span></span>

|<span data-ttu-id="dba86-444">Nazwa elementu</span><span class="sxs-lookup"><span data-stu-id="dba86-444">Element name</span></span>|<span data-ttu-id="dba86-445">Wymagane</span><span class="sxs-lookup"><span data-stu-id="dba86-445">Required</span></span>|<span data-ttu-id="dba86-446">Typ</span><span class="sxs-lookup"><span data-stu-id="dba86-446">Type</span></span>|<span data-ttu-id="dba86-447">Opis</span><span class="sxs-lookup"><span data-stu-id="dba86-447">Description</span></span>|  
|----------------|------------|--------|---------------|  
|<span data-ttu-id="dba86-448">Host</span><span class="sxs-lookup"><span data-stu-id="dba86-448">host</span></span>|<span data-ttu-id="dba86-449">Tak</span><span class="sxs-lookup"><span data-stu-id="dba86-449">Yes</span></span>|<span data-ttu-id="dba86-450">Obiekt</span><span class="sxs-lookup"><span data-stu-id="dba86-450">Object</span></span>|<span data-ttu-id="dba86-451">Reprezentuje hello łącznika informacje, takie jak hello runtimeUrl i odwołanie toohello obiektu połączenia</span><span class="sxs-lookup"><span data-stu-id="dba86-451">Represents hello connector information such as hello runtimeUrl and reference toohello connection object</span></span>|
|<span data-ttu-id="dba86-452">— Metoda</span><span class="sxs-lookup"><span data-stu-id="dba86-452">method</span></span>|<span data-ttu-id="dba86-453">Tak</span><span class="sxs-lookup"><span data-stu-id="dba86-453">Yes</span></span>|<span data-ttu-id="dba86-454">Ciąg</span><span class="sxs-lookup"><span data-stu-id="dba86-454">String</span></span>|<span data-ttu-id="dba86-455">Może być jedną z następujących metod HTTP hello: **UZYSKAĆ**, **POST**, **PUT**, **usunąć**, **poprawka**, lub  **HEAD**</span><span class="sxs-lookup"><span data-stu-id="dba86-455">Can be one of hello following HTTP methods: **GET**, **POST**, **PUT**, **DELETE**, **PATCH**, or **HEAD**</span></span>|  
|<span data-ttu-id="dba86-456">Ścieżka</span><span class="sxs-lookup"><span data-stu-id="dba86-456">path</span></span>|<span data-ttu-id="dba86-457">Tak</span><span class="sxs-lookup"><span data-stu-id="dba86-457">Yes</span></span>|<span data-ttu-id="dba86-458">Ciąg</span><span class="sxs-lookup"><span data-stu-id="dba86-458">String</span></span>|<span data-ttu-id="dba86-459">Ścieżka Hello operacji hello interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="dba86-459">hello path of hello API operation.</span></span>|  
|<span data-ttu-id="dba86-460">— zapytania</span><span class="sxs-lookup"><span data-stu-id="dba86-460">queries</span></span>|<span data-ttu-id="dba86-461">Nie</span><span class="sxs-lookup"><span data-stu-id="dba86-461">No</span></span>|<span data-ttu-id="dba86-462">Obiekt</span><span class="sxs-lookup"><span data-stu-id="dba86-462">Object</span></span>|<span data-ttu-id="dba86-463">Reprezentuje adres URL toohello tooadd hello kwerendy parametrów.</span><span class="sxs-lookup"><span data-stu-id="dba86-463">Represents hello query parameters tooadd toohello URL.</span></span> <span data-ttu-id="dba86-464">Na przykład `"queries" : { "api-version": "2015-02-01" }` dodaje `?api-version=2015-02-01` toohello adresu URL.</span><span class="sxs-lookup"><span data-stu-id="dba86-464">For example, `"queries" : { "api-version": "2015-02-01" }` adds `?api-version=2015-02-01` toohello URL.</span></span>|  
|<span data-ttu-id="dba86-465">Nagłówki</span><span class="sxs-lookup"><span data-stu-id="dba86-465">headers</span></span>|<span data-ttu-id="dba86-466">Nie</span><span class="sxs-lookup"><span data-stu-id="dba86-466">No</span></span>|<span data-ttu-id="dba86-467">Obiekt</span><span class="sxs-lookup"><span data-stu-id="dba86-467">Object</span></span>|<span data-ttu-id="dba86-468">Reprezentuje wszystkich nagłówków hello, które są wysyłane żądania toohello.</span><span class="sxs-lookup"><span data-stu-id="dba86-468">Represents each of hello headers that is sent toohello request.</span></span> <span data-ttu-id="dba86-469">Na przykład tooset hello język i typ żądania:`"headers" : { "Accept-Language": "en-us",  "Content-Type": "application/json" }`</span><span class="sxs-lookup"><span data-stu-id="dba86-469">For example, tooset hello language and type on a request: `"headers" : { "Accept-Language": "en-us",  "Content-Type": "application/json" }`</span></span>|  
|<span data-ttu-id="dba86-470">Treści</span><span class="sxs-lookup"><span data-stu-id="dba86-470">body</span></span>|<span data-ttu-id="dba86-471">Nie</span><span class="sxs-lookup"><span data-stu-id="dba86-471">No</span></span>|<span data-ttu-id="dba86-472">Obiekt</span><span class="sxs-lookup"><span data-stu-id="dba86-472">Object</span></span>|<span data-ttu-id="dba86-473">Reprezentuje ładunek hello, wysyłany toohello punktu końcowego.</span><span class="sxs-lookup"><span data-stu-id="dba86-473">Represents hello payload that is sent toohello endpoint.</span></span>|  
|<span data-ttu-id="dba86-474">retryPolicy</span><span class="sxs-lookup"><span data-stu-id="dba86-474">retryPolicy</span></span>|<span data-ttu-id="dba86-475">Nie</span><span class="sxs-lookup"><span data-stu-id="dba86-475">No</span></span>|<span data-ttu-id="dba86-476">Obiekt</span><span class="sxs-lookup"><span data-stu-id="dba86-476">Object</span></span>|<span data-ttu-id="dba86-477">Umożliwia dostosowanie hello zachowanie ponownych prób dla 4xx lub 5xx błędów.</span><span class="sxs-lookup"><span data-stu-id="dba86-477">Lets you customize hello retry behavior for 4xx or 5xx errors.</span></span>|  
|<span data-ttu-id="dba86-478">operationsOptions</span><span class="sxs-lookup"><span data-stu-id="dba86-478">operationsOptions</span></span>|<span data-ttu-id="dba86-479">Nie</span><span class="sxs-lookup"><span data-stu-id="dba86-479">No</span></span>|<span data-ttu-id="dba86-480">Ciąg</span><span class="sxs-lookup"><span data-stu-id="dba86-480">String</span></span>|<span data-ttu-id="dba86-481">Definiuje zestaw hello toooverride specjalnego zachowania.</span><span class="sxs-lookup"><span data-stu-id="dba86-481">Defines hello set of special behaviors toooverride.</span></span>|  

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

## <a name="api-connection-webhook-action"></a><span data-ttu-id="dba86-482">Połączenie z interfejsem API akcji elementu webhook</span><span class="sxs-lookup"><span data-stu-id="dba86-482">API Connection webhook action</span></span>

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

<span data-ttu-id="dba86-483">Można określić limity akcji elementu webhook w hello taki sam jak [limity asynchroniczne HTTP](#asynchronous-limits).</span><span class="sxs-lookup"><span data-stu-id="dba86-483">Limits on a webhook action can be specified in hello same manner as [HTTP Asynchronous Limits](#asynchronous-limits).</span></span>
  
## <a name="response-action"></a><span data-ttu-id="dba86-484">Akcja odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="dba86-484">Response action</span></span>  

<span data-ttu-id="dba86-485">Ten typ akcji zawiera hello ładunku całej odpowiedzi z żądania HTTP i obejmuje statusCode, treści i nagłówków:</span><span class="sxs-lookup"><span data-stu-id="dba86-485">This action type contains hello entire response payload from an HTTP request and includes a statusCode, body, and headers:</span></span>  
  
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
  
<span data-ttu-id="dba86-486">Akcja odpowiedzi Hello ma specjalne ograniczenia, które nie stosuje określone akcje tooother.</span><span class="sxs-lookup"><span data-stu-id="dba86-486">hello response action has special restrictions that don't apply tooother actions.</span></span> <span data-ttu-id="dba86-487">W szczególności:</span><span class="sxs-lookup"><span data-stu-id="dba86-487">Specifically:</span></span>  
  
-   <span data-ttu-id="dba86-488">Akcje reakcji nie może być równoległe w definicji, ponieważ wymagane jest żądanie przychodzące toohello deterministyczne odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="dba86-488">Response actions cannot be parallel in a definition because a deterministic response toohello incoming request is required.</span></span>  
  
-   <span data-ttu-id="dba86-489">Po osiągnięciu akcji odpowiedzi po otrzymaniu odpowiedzi hello przychodzące żądanie akcji hello jest uznawany za nie powiodło się \(konflikt\), i w związku z tym jest hello Uruchom `Failed`.</span><span class="sxs-lookup"><span data-stu-id="dba86-489">If a response action is reached after hello incoming request has received a response, hello action is considered failed \(conflict\), and as a result, hello run is `Failed`.</span></span>  
  
-   <span data-ttu-id="dba86-490">Przepływ pracy z akcjami odpowiedzi nie może mieć `splitOn` w jego wyzwalacza jedno wywołanie powoduje, że wiele przebiegów.</span><span class="sxs-lookup"><span data-stu-id="dba86-490">A workflow with Response actions cannot have `splitOn` in its trigger because one call causes many runs.</span></span> <span data-ttu-id="dba86-491">W związku z tym to powinny być weryfikowane podczas przepływu hello jest PUT i Przyczyna nieprawidłowe żądanie.</span><span class="sxs-lookup"><span data-stu-id="dba86-491">As a result, this should be validated when hello flow is PUT and cause a Bad Request.</span></span>  
  
## <a name="wait-action"></a><span data-ttu-id="dba86-492">Poczekaj akcji</span><span class="sxs-lookup"><span data-stu-id="dba86-492">Wait action</span></span>  

<span data-ttu-id="dba86-493">Witaj `wait` akcji wstrzymuje wykonywanie przepływu pracy dla hello określonego interwału.</span><span class="sxs-lookup"><span data-stu-id="dba86-493">hello `wait` action suspends workflow execution for hello specified interval.</span></span> <span data-ttu-id="dba86-494">Na przykład toowait 15 minut, można użyć ta Wstawka kodu:</span><span class="sxs-lookup"><span data-stu-id="dba86-494">For example, toowait 15 minutes, you can use this snippet:</span></span>  
  
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
  
<span data-ttu-id="dba86-495">Alternatywnie toowait do określonego momentu w czasie, można użyć w tym przykładzie:</span><span class="sxs-lookup"><span data-stu-id="dba86-495">Alternatively, toowait until a specific moment in time, you can use this example:</span></span>  
  
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
> <span data-ttu-id="dba86-496">czas oczekiwania Hello albo można użyć hello **interwał** obiektu lub hello **do momentu** obiektu, ale nie oba.</span><span class="sxs-lookup"><span data-stu-id="dba86-496">hello wait duration can be either specified using hello **interval** object or hello **until** object, but not both.</span></span>  
  
|<span data-ttu-id="dba86-497">Nazwa</span><span class="sxs-lookup"><span data-stu-id="dba86-497">Name</span></span>|<span data-ttu-id="dba86-498">Wymagane</span><span class="sxs-lookup"><span data-stu-id="dba86-498">Required</span></span>|<span data-ttu-id="dba86-499">Typ</span><span class="sxs-lookup"><span data-stu-id="dba86-499">Type</span></span>|<span data-ttu-id="dba86-500">Opis</span><span class="sxs-lookup"><span data-stu-id="dba86-500">Description</span></span>|  
|--------|------------|--------|---------------|  
|<span data-ttu-id="dba86-501">interval</span><span class="sxs-lookup"><span data-stu-id="dba86-501">interval</span></span>|<span data-ttu-id="dba86-502">Nie</span><span class="sxs-lookup"><span data-stu-id="dba86-502">No</span></span>|<span data-ttu-id="dba86-503">Obiekt</span><span class="sxs-lookup"><span data-stu-id="dba86-503">Object</span></span>|<span data-ttu-id="dba86-504">Witaj poczekaj oparte na czas trwania.</span><span class="sxs-lookup"><span data-stu-id="dba86-504">hello wait duration based on amount of time.</span></span>|  
|<span data-ttu-id="dba86-505">Interwał</span><span class="sxs-lookup"><span data-stu-id="dba86-505">interval unit</span></span>|<span data-ttu-id="dba86-506">Tak</span><span class="sxs-lookup"><span data-stu-id="dba86-506">Yes</span></span>|<span data-ttu-id="dba86-507">Ciąg</span><span class="sxs-lookup"><span data-stu-id="dba86-507">String</span></span>|<span data-ttu-id="dba86-508">Jeden z tych przedziałów: sekundy, minuty, godziny, dnia, tygodnia, miesiąca, roku.</span><span class="sxs-lookup"><span data-stu-id="dba86-508">One of these intervals: second, minute, hour, day, week, month, year.</span></span>|  
|<span data-ttu-id="dba86-509">Liczba interwale</span><span class="sxs-lookup"><span data-stu-id="dba86-509">interval count</span></span>|<span data-ttu-id="dba86-510">Tak</span><span class="sxs-lookup"><span data-stu-id="dba86-510">Yes</span></span>|<span data-ttu-id="dba86-511">Ciąg</span><span class="sxs-lookup"><span data-stu-id="dba86-511">String</span></span>|<span data-ttu-id="dba86-512">Czas trwania oparte na powitania podane wewnętrzny jednostki.</span><span class="sxs-lookup"><span data-stu-id="dba86-512">Duration based on hello given internal unit.</span></span>|  
|<span data-ttu-id="dba86-513">do czasu</span><span class="sxs-lookup"><span data-stu-id="dba86-513">until</span></span>|<span data-ttu-id="dba86-514">Nie</span><span class="sxs-lookup"><span data-stu-id="dba86-514">No</span></span>|<span data-ttu-id="dba86-515">Obiekt</span><span class="sxs-lookup"><span data-stu-id="dba86-515">Object</span></span>|<span data-ttu-id="dba86-516">Witaj poczekaj oparte na punkt w czasie trwania.</span><span class="sxs-lookup"><span data-stu-id="dba86-516">hello wait duration based on a point in time.</span></span>|  
|<span data-ttu-id="dba86-517">do sygnatury czasowej</span><span class="sxs-lookup"><span data-stu-id="dba86-517">until timestamp</span></span>|<span data-ttu-id="dba86-518">Tak</span><span class="sxs-lookup"><span data-stu-id="dba86-518">Yes</span></span>|<span data-ttu-id="dba86-519">Ciąg</span><span class="sxs-lookup"><span data-stu-id="dba86-519">String</span></span>|<span data-ttu-id="dba86-520">Ciąg &#124; hello punktu w czasie w formacie UTC wygaśnięcia hello oczekiwania.</span><span class="sxs-lookup"><span data-stu-id="dba86-520">String&#124;hello point in time in UTC when hello wait expires.</span></span>|  

## <a name="query-action"></a><span data-ttu-id="dba86-521">Akcja kwerendy</span><span class="sxs-lookup"><span data-stu-id="dba86-521">Query action</span></span>

<span data-ttu-id="dba86-522">Witaj `query` akcja umożliwia filtrowanie na podstawie warunku tablicy.</span><span class="sxs-lookup"><span data-stu-id="dba86-522">hello `query` action lets you filter an array based on a condition.</span></span> <span data-ttu-id="dba86-523">Na przykład numery tooselect jest większa niż 2, można:</span><span class="sxs-lookup"><span data-stu-id="dba86-523">For example, tooselect numbers greater than 2, you can use:</span></span>

```json
"FilterNumbers" : {
    "type": "query",
    "inputs": {
        "from": [ 1, 3, 0, 5, 4, 2 ],
        "where": "@greater(item(), 2)"
    }
}
```

<span data-ttu-id="dba86-524">Witaj dane wyjściowe hello `query` tablicę, która ma elementy z tablicy wejściowej hello, które spełniają warunek hello jest akcja.</span><span class="sxs-lookup"><span data-stu-id="dba86-524">hello output from hello `query` action is an array that has elements from hello input array that satisfy hello condition.</span></span>

> [!NOTE]
> <span data-ttu-id="dba86-525">Jeśli wartości nie spełniają hello `where` warunku, hello wyniku jest pusta tablica.</span><span class="sxs-lookup"><span data-stu-id="dba86-525">If no values satisfy hello `where` condition, hello result is an empty array.</span></span>

|<span data-ttu-id="dba86-526">Nazwa</span><span class="sxs-lookup"><span data-stu-id="dba86-526">Name</span></span>|<span data-ttu-id="dba86-527">Wymagane</span><span class="sxs-lookup"><span data-stu-id="dba86-527">Required</span></span>|<span data-ttu-id="dba86-528">Typ</span><span class="sxs-lookup"><span data-stu-id="dba86-528">Type</span></span>|<span data-ttu-id="dba86-529">Opis</span><span class="sxs-lookup"><span data-stu-id="dba86-529">Description</span></span>|
|--------|------------|--------|---------------|
|<span data-ttu-id="dba86-530">Z</span><span class="sxs-lookup"><span data-stu-id="dba86-530">from</span></span>|<span data-ttu-id="dba86-531">Tak</span><span class="sxs-lookup"><span data-stu-id="dba86-531">Yes</span></span>|<span data-ttu-id="dba86-532">Tablica</span><span class="sxs-lookup"><span data-stu-id="dba86-532">Array</span></span>|<span data-ttu-id="dba86-533">Tablica źródłowa Hello.</span><span class="sxs-lookup"><span data-stu-id="dba86-533">hello source array.</span></span>|
|<span data-ttu-id="dba86-534">gdzie</span><span class="sxs-lookup"><span data-stu-id="dba86-534">where</span></span>|<span data-ttu-id="dba86-535">Tak</span><span class="sxs-lookup"><span data-stu-id="dba86-535">Yes</span></span>|<span data-ttu-id="dba86-536">Ciąg</span><span class="sxs-lookup"><span data-stu-id="dba86-536">String</span></span>|<span data-ttu-id="dba86-537">Witaj warunku tooapply tooeach elementu tablicy źródłowej hello.</span><span class="sxs-lookup"><span data-stu-id="dba86-537">hello condition tooapply tooeach element of hello source array.</span></span>|

## <a name="select-action"></a><span data-ttu-id="dba86-538">Wybierz akcję</span><span class="sxs-lookup"><span data-stu-id="dba86-538">Select action</span></span>

<span data-ttu-id="dba86-539">Witaj `select` pozwala projektów każdy element tablicy na nową wartość.</span><span class="sxs-lookup"><span data-stu-id="dba86-539">hello `select` action lets you project each element of an array into a new value.</span></span>
<span data-ttu-id="dba86-540">Na przykład tooconvert jako tablica liczb na tablicę obiektów, można użyć:</span><span class="sxs-lookup"><span data-stu-id="dba86-540">For example, tooconvert an array of numbers into an array of objects, you can use:</span></span>

```json
"SelectNumbers" : {
    "type": "select",
    "inputs": {
        "from": [ 1, 3, 0, 5, 4, 2 ],
        "select": { "number": "@item()" }
    }
}
```

<span data-ttu-id="dba86-541">Witaj dane wyjściowe hello `select` tablicę, która ma hello samą liczność hello tablicy wejściowej z każdym elementem przekształcone jako określone hello jest akcja `select` właściwości.</span><span class="sxs-lookup"><span data-stu-id="dba86-541">hello output of hello `select` action is an array that has hello same cardinality as hello input array, with each element transformed as defined by hello `select` property.</span></span> <span data-ttu-id="dba86-542">Jeśli dane wejściowe hello jest pusta tablica, dane wyjściowe hello jest również pustą tablicę.</span><span class="sxs-lookup"><span data-stu-id="dba86-542">If hello input is an empty array, hello output is also an empty array.</span></span>

|<span data-ttu-id="dba86-543">Nazwa</span><span class="sxs-lookup"><span data-stu-id="dba86-543">Name</span></span>|<span data-ttu-id="dba86-544">Wymagane</span><span class="sxs-lookup"><span data-stu-id="dba86-544">Required</span></span>|<span data-ttu-id="dba86-545">Typ</span><span class="sxs-lookup"><span data-stu-id="dba86-545">Type</span></span>|<span data-ttu-id="dba86-546">Opis</span><span class="sxs-lookup"><span data-stu-id="dba86-546">Description</span></span>|
|--------|------------|--------|---------------|
|<span data-ttu-id="dba86-547">Z</span><span class="sxs-lookup"><span data-stu-id="dba86-547">from</span></span>|<span data-ttu-id="dba86-548">Tak</span><span class="sxs-lookup"><span data-stu-id="dba86-548">Yes</span></span>|<span data-ttu-id="dba86-549">Tablica</span><span class="sxs-lookup"><span data-stu-id="dba86-549">Array</span></span>|<span data-ttu-id="dba86-550">Tablica źródłowa Hello.</span><span class="sxs-lookup"><span data-stu-id="dba86-550">hello source array.</span></span>|
|<span data-ttu-id="dba86-551">Wybierz</span><span class="sxs-lookup"><span data-stu-id="dba86-551">select</span></span>|<span data-ttu-id="dba86-552">Tak</span><span class="sxs-lookup"><span data-stu-id="dba86-552">Yes</span></span>|<span data-ttu-id="dba86-553">Dowolne</span><span class="sxs-lookup"><span data-stu-id="dba86-553">Any</span></span>|<span data-ttu-id="dba86-554">Witaj projekcji tooapply tooeach elementu tablicy źródłowej hello.</span><span class="sxs-lookup"><span data-stu-id="dba86-554">hello projection tooapply tooeach element of hello source array.</span></span>|

## <a name="terminate-action"></a><span data-ttu-id="dba86-555">Zakończenie akcji</span><span class="sxs-lookup"><span data-stu-id="dba86-555">Terminate action</span></span>

<span data-ttu-id="dba86-556">Hello akcji Zakończenie zatrzymuje wykonywanie hello przepływu pracy, przerywanie wszystkie akcje locie i pomija wszystkie pozostałe akcje.</span><span class="sxs-lookup"><span data-stu-id="dba86-556">hello Terminate action stops execution of hello workflow run, aborting any in-flight actions, and skipping any remaining actions.</span></span> <span data-ttu-id="dba86-557">Na przykład tooterminate Uruchom ze stanem ****, można użyć następującego fragmentu hello:</span><span class="sxs-lookup"><span data-stu-id="dba86-557">For example, tooterminate a run with status **Failed**, you can use hello following snippet:</span></span>

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
> <span data-ttu-id="dba86-558">Akcje już ukończone nie dotyczy hello przerwanie działania.</span><span class="sxs-lookup"><span data-stu-id="dba86-558">Actions already completed are not affected by hello terminate action.</span></span>

|<span data-ttu-id="dba86-559">Nazwa</span><span class="sxs-lookup"><span data-stu-id="dba86-559">Name</span></span>|<span data-ttu-id="dba86-560">Wymagane</span><span class="sxs-lookup"><span data-stu-id="dba86-560">Required</span></span>|<span data-ttu-id="dba86-561">Typ</span><span class="sxs-lookup"><span data-stu-id="dba86-561">Type</span></span>|<span data-ttu-id="dba86-562">Opis</span><span class="sxs-lookup"><span data-stu-id="dba86-562">Description</span></span>|
|--------|------------|--------|---------------|
|<span data-ttu-id="dba86-563">runStatus</span><span class="sxs-lookup"><span data-stu-id="dba86-563">runStatus</span></span>|<span data-ttu-id="dba86-564">Tak</span><span class="sxs-lookup"><span data-stu-id="dba86-564">Yes</span></span>|<span data-ttu-id="dba86-565">Ciąg</span><span class="sxs-lookup"><span data-stu-id="dba86-565">String</span></span>|<span data-ttu-id="dba86-566">obiekt docelowy Hello stan uruchomienia.</span><span class="sxs-lookup"><span data-stu-id="dba86-566">hello target run status.</span></span> <span data-ttu-id="dba86-567">Albo **nie powiodło się** lub **anulowane**.</span><span class="sxs-lookup"><span data-stu-id="dba86-567">Either **Failed** or **Cancelled**.</span></span>|
|<span data-ttu-id="dba86-568">runError</span><span class="sxs-lookup"><span data-stu-id="dba86-568">runError</span></span>|<span data-ttu-id="dba86-569">Nie</span><span class="sxs-lookup"><span data-stu-id="dba86-569">No</span></span>|<span data-ttu-id="dba86-570">Obiekt</span><span class="sxs-lookup"><span data-stu-id="dba86-570">Object</span></span>|<span data-ttu-id="dba86-571">Szczegóły błędu Hello.</span><span class="sxs-lookup"><span data-stu-id="dba86-571">hello error details.</span></span> <span data-ttu-id="dba86-572">Tylko obsługiwane w przypadku **runStatus** ustawiono zbyt****.</span><span class="sxs-lookup"><span data-stu-id="dba86-572">Only supported when **runStatus** is set too**Failed**.</span></span>|
|<span data-ttu-id="dba86-573">Kod runError</span><span class="sxs-lookup"><span data-stu-id="dba86-573">runError code</span></span>|<span data-ttu-id="dba86-574">Nie</span><span class="sxs-lookup"><span data-stu-id="dba86-574">No</span></span>|<span data-ttu-id="dba86-575">Ciąg</span><span class="sxs-lookup"><span data-stu-id="dba86-575">String</span></span>|<span data-ttu-id="dba86-576">Witaj, uruchom kod błędu.</span><span class="sxs-lookup"><span data-stu-id="dba86-576">hello run error code.</span></span>|
|<span data-ttu-id="dba86-577">komunikat runError</span><span class="sxs-lookup"><span data-stu-id="dba86-577">runError message</span></span>|<span data-ttu-id="dba86-578">Nie</span><span class="sxs-lookup"><span data-stu-id="dba86-578">No</span></span>|<span data-ttu-id="dba86-579">Ciąg</span><span class="sxs-lookup"><span data-stu-id="dba86-579">String</span></span>|<span data-ttu-id="dba86-580">Witaj, uruchom komunikat o błędzie.</span><span class="sxs-lookup"><span data-stu-id="dba86-580">hello run error message.</span></span>|

## <a name="compose-action"></a><span data-ttu-id="dba86-581">Redagowanie akcji</span><span class="sxs-lookup"><span data-stu-id="dba86-581">Compose action</span></span>

<span data-ttu-id="dba86-582">Witaj akcji tworzenia umożliwia utworzenia dowolnego obiektu.</span><span class="sxs-lookup"><span data-stu-id="dba86-582">hello Compose action lets you construct an arbitrary object.</span></span> <span data-ttu-id="dba86-583">dane wyjściowe Hello hello tworzą akcji jest wynikiem hello oceny jej danych wejściowych.</span><span class="sxs-lookup"><span data-stu-id="dba86-583">hello output of hello compose action is hello result of evaluating its inputs.</span></span> <span data-ttu-id="dba86-584">Na przykład można użyć hello tworzą dane wyjściowe toomerge akcji wiele działań:</span><span class="sxs-lookup"><span data-stu-id="dba86-584">For example, you can use hello compose action toomerge outputs of multiple actions:</span></span>

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
> <span data-ttu-id="dba86-585">Witaj **Redaguj** akcji mogą być używane tooconstruct żadnych danych wyjściowych, w tym obiektów, tablic i innego typu obsługiwane przez logikę aplikacji, takich jak XML i pliku binarnego.</span><span class="sxs-lookup"><span data-stu-id="dba86-585">hello **Compose** action can be used tooconstruct any output, including objects, arrays, and any other type natively supported by logic apps like XML and binary.</span></span>

## <a name="table-action"></a><span data-ttu-id="dba86-586">Akcja tabeli</span><span class="sxs-lookup"><span data-stu-id="dba86-586">Table action</span></span>

<span data-ttu-id="dba86-587">Witaj `table` pozwala tooconvert jako tablicę elementów do **CSV** lub **HTML** tabeli.</span><span class="sxs-lookup"><span data-stu-id="dba86-587">hello `table` allows you tooconvert an array of items into a **CSV** or **HTML** table.</span></span>

<span data-ttu-id="dba86-588">Załóżmy, że @triggerBodyjest)</span><span class="sxs-lookup"><span data-stu-id="dba86-588">Suppose @triggerBody() is</span></span>

```json
[{
  "id": 0,
  "name": "apples"
},{
  "id": 1, 
  "name": "oranges"
}]
```

<span data-ttu-id="dba86-589">Natomiast akcja hello można zdefiniować jako</span><span class="sxs-lookup"><span data-stu-id="dba86-589">And let hello action be defined as</span></span>

```json
"ConvertToTable" : {
    "type": "table",
    "inputs": {
        "from": "@triggerBody()",
        "format": "html"
    }
}
```

<span data-ttu-id="dba86-590">dałby w efekcie Hello powyżej</span><span class="sxs-lookup"><span data-stu-id="dba86-590">hello above would produce</span></span>

<table><thead><tr><th><span data-ttu-id="dba86-591">id</span><span class="sxs-lookup"><span data-stu-id="dba86-591">id</span></span></th><th><span data-ttu-id="dba86-592">name</span><span class="sxs-lookup"><span data-stu-id="dba86-592">name</span></span></th></tr></thead><tbody><tr><td><span data-ttu-id="dba86-593">0</span><span class="sxs-lookup"><span data-stu-id="dba86-593">0</span></span></td><td><span data-ttu-id="dba86-594">jabłek</span><span class="sxs-lookup"><span data-stu-id="dba86-594">apples</span></span></td></tr><tr><td><span data-ttu-id="dba86-595">1</span><span class="sxs-lookup"><span data-stu-id="dba86-595">1</span></span></td><td><span data-ttu-id="dba86-596">Pomarańcze</span><span class="sxs-lookup"><span data-stu-id="dba86-596">oranges</span></span></td></tr></tbody></table><span data-ttu-id="dba86-597">"</span><span class="sxs-lookup"><span data-stu-id="dba86-597">"</span></span>

<span data-ttu-id="dba86-598">W tabeli hello toocustomize kolejności można określić kolumny hello jawnie.</span><span class="sxs-lookup"><span data-stu-id="dba86-598">In order toocustomize hello table, you can specify hello columns explicitly.</span></span> <span data-ttu-id="dba86-599">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="dba86-599">For example:</span></span>

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

<span data-ttu-id="dba86-600">dałby w efekcie Hello powyżej</span><span class="sxs-lookup"><span data-stu-id="dba86-600">hello above would produce</span></span>

<table><thead><tr><th><span data-ttu-id="dba86-601">Tworzy identyfikator</span><span class="sxs-lookup"><span data-stu-id="dba86-601">produce id</span></span></th><th><span data-ttu-id="dba86-602">description</span><span class="sxs-lookup"><span data-stu-id="dba86-602">description</span></span></th></tr></thead><tbody><tr><td><span data-ttu-id="dba86-603">0</span><span class="sxs-lookup"><span data-stu-id="dba86-603">0</span></span></td><td><span data-ttu-id="dba86-604">Nowa jabłek</span><span class="sxs-lookup"><span data-stu-id="dba86-604">fresh apples</span></span></td></tr><tr><td><span data-ttu-id="dba86-605">1</span><span class="sxs-lookup"><span data-stu-id="dba86-605">1</span></span></td><td><span data-ttu-id="dba86-606">świeżych pomarańczy</span><span class="sxs-lookup"><span data-stu-id="dba86-606">fresh oranges</span></span></td></tr></tbody></table><span data-ttu-id="dba86-607">"</span><span class="sxs-lookup"><span data-stu-id="dba86-607">"</span></span>

<span data-ttu-id="dba86-608">Jeśli hello `from` wartość właściwości jest pusta tablica, dane wyjściowe hello jest pusta tabela.</span><span class="sxs-lookup"><span data-stu-id="dba86-608">If hello `from` property value is an empty array, hello output is an empty table.</span></span>

|<span data-ttu-id="dba86-609">Nazwa</span><span class="sxs-lookup"><span data-stu-id="dba86-609">Name</span></span>|<span data-ttu-id="dba86-610">Wymagane</span><span class="sxs-lookup"><span data-stu-id="dba86-610">Required</span></span>|<span data-ttu-id="dba86-611">Typ</span><span class="sxs-lookup"><span data-stu-id="dba86-611">Type</span></span>|<span data-ttu-id="dba86-612">Opis</span><span class="sxs-lookup"><span data-stu-id="dba86-612">Description</span></span>|
|--------|------------|--------|---------------|
|<span data-ttu-id="dba86-613">Z</span><span class="sxs-lookup"><span data-stu-id="dba86-613">from</span></span>|<span data-ttu-id="dba86-614">Tak</span><span class="sxs-lookup"><span data-stu-id="dba86-614">Yes</span></span>|<span data-ttu-id="dba86-615">Tablica</span><span class="sxs-lookup"><span data-stu-id="dba86-615">Array</span></span>|<span data-ttu-id="dba86-616">Tablica źródłowa Hello.</span><span class="sxs-lookup"><span data-stu-id="dba86-616">hello source array.</span></span>|
|<span data-ttu-id="dba86-617">Format</span><span class="sxs-lookup"><span data-stu-id="dba86-617">format</span></span>|<span data-ttu-id="dba86-618">Tak</span><span class="sxs-lookup"><span data-stu-id="dba86-618">Yes</span></span>|<span data-ttu-id="dba86-619">Ciąg</span><span class="sxs-lookup"><span data-stu-id="dba86-619">String</span></span>|<span data-ttu-id="dba86-620">Witaj format, albo **CSV** lub **HTML**.</span><span class="sxs-lookup"><span data-stu-id="dba86-620">hello format, either **CSV** or **HTML**.</span></span>|
|<span data-ttu-id="dba86-621">kolumny</span><span class="sxs-lookup"><span data-stu-id="dba86-621">columns</span></span>|<span data-ttu-id="dba86-622">Nie</span><span class="sxs-lookup"><span data-stu-id="dba86-622">No</span></span>|<span data-ttu-id="dba86-623">Tablica</span><span class="sxs-lookup"><span data-stu-id="dba86-623">Array</span></span>|<span data-ttu-id="dba86-624">Witaj kolumny.</span><span class="sxs-lookup"><span data-stu-id="dba86-624">hello columns.</span></span> <span data-ttu-id="dba86-625">Umożliwia toooverride hello domyślnego kształtu hello tabeli.</span><span class="sxs-lookup"><span data-stu-id="dba86-625">Allows toooverride hello default shape of hello table.</span></span>|
|<span data-ttu-id="dba86-626">Nagłówek kolumny</span><span class="sxs-lookup"><span data-stu-id="dba86-626">column header</span></span>|<span data-ttu-id="dba86-627">Nie</span><span class="sxs-lookup"><span data-stu-id="dba86-627">No</span></span>|<span data-ttu-id="dba86-628">Ciąg</span><span class="sxs-lookup"><span data-stu-id="dba86-628">String</span></span>|<span data-ttu-id="dba86-629">Nagłówek Hello hello kolumny.</span><span class="sxs-lookup"><span data-stu-id="dba86-629">hello header of hello column.</span></span>|
|<span data-ttu-id="dba86-630">wartość w kolumnie</span><span class="sxs-lookup"><span data-stu-id="dba86-630">column value</span></span>|<span data-ttu-id="dba86-631">Tak</span><span class="sxs-lookup"><span data-stu-id="dba86-631">Yes</span></span>|<span data-ttu-id="dba86-632">Ciąg</span><span class="sxs-lookup"><span data-stu-id="dba86-632">String</span></span>|<span data-ttu-id="dba86-633">wartość Hello hello kolumny.</span><span class="sxs-lookup"><span data-stu-id="dba86-633">hello value of hello column.</span></span>|

## <a name="workflow-action"></a><span data-ttu-id="dba86-634">Działania przepływu pracy</span><span class="sxs-lookup"><span data-stu-id="dba86-634">Workflow action</span></span>   

|<span data-ttu-id="dba86-635">Nazwa</span><span class="sxs-lookup"><span data-stu-id="dba86-635">Name</span></span>|<span data-ttu-id="dba86-636">Wymagane</span><span class="sxs-lookup"><span data-stu-id="dba86-636">Required</span></span>|<span data-ttu-id="dba86-637">Typ</span><span class="sxs-lookup"><span data-stu-id="dba86-637">Type</span></span>|<span data-ttu-id="dba86-638">Opis</span><span class="sxs-lookup"><span data-stu-id="dba86-638">Description</span></span>|  
|--------|------------|--------|---------------|  
|<span data-ttu-id="dba86-639">Identyfikator hosta</span><span class="sxs-lookup"><span data-stu-id="dba86-639">host id</span></span>|<span data-ttu-id="dba86-640">Tak</span><span class="sxs-lookup"><span data-stu-id="dba86-640">Yes</span></span>|<span data-ttu-id="dba86-641">Ciąg</span><span class="sxs-lookup"><span data-stu-id="dba86-641">String</span></span>|<span data-ttu-id="dba86-642">Identyfikator zasobu Hello hello przepływu pracy, które mają toocall.</span><span class="sxs-lookup"><span data-stu-id="dba86-642">hello resource ID of hello workflow that you want toocall.</span></span>|  
|<span data-ttu-id="dba86-643">Nazwa_wyzwalacza hosta</span><span class="sxs-lookup"><span data-stu-id="dba86-643">host triggerName</span></span>|<span data-ttu-id="dba86-644">Tak</span><span class="sxs-lookup"><span data-stu-id="dba86-644">Yes</span></span>|<span data-ttu-id="dba86-645">Ciąg</span><span class="sxs-lookup"><span data-stu-id="dba86-645">String</span></span>|<span data-ttu-id="dba86-646">Nazwa Hello hello wyzwalacza, które mają tooinvoke.</span><span class="sxs-lookup"><span data-stu-id="dba86-646">hello name of hello trigger that you want tooinvoke.</span></span>|  
|<span data-ttu-id="dba86-647">— zapytania</span><span class="sxs-lookup"><span data-stu-id="dba86-647">queries</span></span>|<span data-ttu-id="dba86-648">Nie</span><span class="sxs-lookup"><span data-stu-id="dba86-648">No</span></span>|<span data-ttu-id="dba86-649">Obiekt</span><span class="sxs-lookup"><span data-stu-id="dba86-649">Object</span></span>|<span data-ttu-id="dba86-650">Reprezentuje adres URL toohello tooadd hello kwerendy parametrów.</span><span class="sxs-lookup"><span data-stu-id="dba86-650">Represents hello query parameters tooadd toohello URL.</span></span> <span data-ttu-id="dba86-651">Na przykład `"queries" : { "api-version": "2015-02-01" }` dodaje `?api-version=2015-02-01` toohello adresu URL.</span><span class="sxs-lookup"><span data-stu-id="dba86-651">For example, `"queries" : { "api-version": "2015-02-01" }` adds `?api-version=2015-02-01` toohello URL.</span></span>|  
|<span data-ttu-id="dba86-652">Nagłówki</span><span class="sxs-lookup"><span data-stu-id="dba86-652">headers</span></span>|<span data-ttu-id="dba86-653">Nie</span><span class="sxs-lookup"><span data-stu-id="dba86-653">No</span></span>|<span data-ttu-id="dba86-654">Obiekt</span><span class="sxs-lookup"><span data-stu-id="dba86-654">Object</span></span>|<span data-ttu-id="dba86-655">Reprezentuje wszystkich nagłówków hello, które są wysyłane żądania toohello.</span><span class="sxs-lookup"><span data-stu-id="dba86-655">Represents each of hello headers that is sent toohello request.</span></span> <span data-ttu-id="dba86-656">Na przykład tooset hello język i typ żądania:`"headers" : { "Accept-Language": "en-us",  "Content-Type": "application/json" }`</span><span class="sxs-lookup"><span data-stu-id="dba86-656">For example, tooset hello language and type on a request: `"headers" : { "Accept-Language": "en-us",  "Content-Type": "application/json" }`</span></span>|  
|<span data-ttu-id="dba86-657">Treści</span><span class="sxs-lookup"><span data-stu-id="dba86-657">body</span></span>|<span data-ttu-id="dba86-658">Nie</span><span class="sxs-lookup"><span data-stu-id="dba86-658">No</span></span>|<span data-ttu-id="dba86-659">Obiekt</span><span class="sxs-lookup"><span data-stu-id="dba86-659">Object</span></span>|<span data-ttu-id="dba86-660">Reprezentuje ładunek hello wysyłane toohello punktu końcowego.</span><span class="sxs-lookup"><span data-stu-id="dba86-660">Represents hello payload sent toohello endpoint.</span></span>|  
  
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
  
<span data-ttu-id="dba86-661">Sprawdzanie dostępu jest podejmowana hello przepływu pracy \(dokładniej, wyzwalacz hello\), co oznacza muszą uzyskać dostęp toohello przepływu pracy.</span><span class="sxs-lookup"><span data-stu-id="dba86-661">An access check is made on hello workflow \(more specifically, hello trigger\), meaning you need access toohello workflow.</span></span>  
  
<span data-ttu-id="dba86-662">Witaj danych wyjściowych ze hello `workflow` akcji są oparte na zdefiniowane w hello `response` działań w przepływie pracy podrzędny hello.</span><span class="sxs-lookup"><span data-stu-id="dba86-662">hello outputs from hello `workflow` action are based on what you defined in hello `response` action in hello child workflow.</span></span> <span data-ttu-id="dba86-663">Jeśli nie zdefiniowano żadnego `response` akcji, a następnie hello dane wyjściowe są puste.</span><span class="sxs-lookup"><span data-stu-id="dba86-663">If you have not defined any `response` action, then hello outputs are empty.</span></span>  

## <a name="function-action"></a><span data-ttu-id="dba86-664">Akcja — funkcja</span><span class="sxs-lookup"><span data-stu-id="dba86-664">Function action</span></span>   

|<span data-ttu-id="dba86-665">Nazwa</span><span class="sxs-lookup"><span data-stu-id="dba86-665">Name</span></span>|<span data-ttu-id="dba86-666">Wymagane</span><span class="sxs-lookup"><span data-stu-id="dba86-666">Required</span></span>|<span data-ttu-id="dba86-667">Typ</span><span class="sxs-lookup"><span data-stu-id="dba86-667">Type</span></span>|<span data-ttu-id="dba86-668">Opis</span><span class="sxs-lookup"><span data-stu-id="dba86-668">Description</span></span>|  
|--------|------------|--------|---------------|  
|<span data-ttu-id="dba86-669">id — funkcja</span><span class="sxs-lookup"><span data-stu-id="dba86-669">function id</span></span>|<span data-ttu-id="dba86-670">Tak</span><span class="sxs-lookup"><span data-stu-id="dba86-670">Yes</span></span>|<span data-ttu-id="dba86-671">Ciąg</span><span class="sxs-lookup"><span data-stu-id="dba86-671">String</span></span>|<span data-ttu-id="dba86-672">Identyfikator zasobu Hello hello funkcji, które mają tooinvoke.</span><span class="sxs-lookup"><span data-stu-id="dba86-672">hello resource ID of hello function that you want tooinvoke.</span></span>|  
|<span data-ttu-id="dba86-673">— Metoda</span><span class="sxs-lookup"><span data-stu-id="dba86-673">method</span></span>|<span data-ttu-id="dba86-674">Nie</span><span class="sxs-lookup"><span data-stu-id="dba86-674">No</span></span>|<span data-ttu-id="dba86-675">Ciąg</span><span class="sxs-lookup"><span data-stu-id="dba86-675">String</span></span>|<span data-ttu-id="dba86-676">Hello metoda HTTP używana funkcja hello tooinvoke.</span><span class="sxs-lookup"><span data-stu-id="dba86-676">hello HTTP method used tooinvoke hello function.</span></span> <span data-ttu-id="dba86-677">Domyślnie jest `POST` gdy nie został określony.</span><span class="sxs-lookup"><span data-stu-id="dba86-677">By default, it is `POST` when not specified.</span></span>|  
|<span data-ttu-id="dba86-678">— zapytania</span><span class="sxs-lookup"><span data-stu-id="dba86-678">queries</span></span>|<span data-ttu-id="dba86-679">Nie</span><span class="sxs-lookup"><span data-stu-id="dba86-679">No</span></span>|<span data-ttu-id="dba86-680">Obiekt</span><span class="sxs-lookup"><span data-stu-id="dba86-680">Object</span></span>|<span data-ttu-id="dba86-681">Reprezentuje adres URL toohello tooadd hello kwerendy parametrów.</span><span class="sxs-lookup"><span data-stu-id="dba86-681">Represents hello query parameters tooadd toohello URL.</span></span> <span data-ttu-id="dba86-682">Na przykład `"queries" : { "api-version": "2015-02-01" }` dodaje `?api-version=2015-02-01` toohello adresu URL.</span><span class="sxs-lookup"><span data-stu-id="dba86-682">For example, `"queries" : { "api-version": "2015-02-01" }` adds `?api-version=2015-02-01` toohello URL.</span></span>|  
|<span data-ttu-id="dba86-683">Nagłówki</span><span class="sxs-lookup"><span data-stu-id="dba86-683">headers</span></span>|<span data-ttu-id="dba86-684">Nie</span><span class="sxs-lookup"><span data-stu-id="dba86-684">No</span></span>|<span data-ttu-id="dba86-685">Obiekt</span><span class="sxs-lookup"><span data-stu-id="dba86-685">Object</span></span>|<span data-ttu-id="dba86-686">Reprezentuje wszystkich nagłówków hello, które są wysyłane żądania toohello.</span><span class="sxs-lookup"><span data-stu-id="dba86-686">Represents each of hello headers that is sent toohello request.</span></span> <span data-ttu-id="dba86-687">Na przykład tooset hello język i typ na żądanie: `"headers" : { "Accept-Language": "en-us" }`.</span><span class="sxs-lookup"><span data-stu-id="dba86-687">For example, tooset hello language and type on a request: `"headers" : { "Accept-Language": "en-us" }`.</span></span>|  
|<span data-ttu-id="dba86-688">Treści</span><span class="sxs-lookup"><span data-stu-id="dba86-688">body</span></span>|<span data-ttu-id="dba86-689">Nie</span><span class="sxs-lookup"><span data-stu-id="dba86-689">No</span></span>|<span data-ttu-id="dba86-690">Obiekt</span><span class="sxs-lookup"><span data-stu-id="dba86-690">Object</span></span>|<span data-ttu-id="dba86-691">Reprezentuje ładunek hello wysyłane toohello punktu końcowego.</span><span class="sxs-lookup"><span data-stu-id="dba86-691">Represents hello payload sent toohello endpoint.</span></span>|  

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

<span data-ttu-id="dba86-692">Podczas zapisywania aplikacji logiki hello wykonać testy na powitania odwołuje się do funkcji:</span><span class="sxs-lookup"><span data-stu-id="dba86-692">When you save hello logic app, we perform some checks on hello referenced function:</span></span>
-   <span data-ttu-id="dba86-693">Należy toohave dostępu toohello funkcji.</span><span class="sxs-lookup"><span data-stu-id="dba86-693">You need toohave access toohello function.</span></span>
-   <span data-ttu-id="dba86-694">Tylko standardowy wyzwalacza HTTP lub ogólny wyzwalacza elementu webhook JSON jest dozwolone.</span><span class="sxs-lookup"><span data-stu-id="dba86-694">Only standard HTTP trigger or generic JSON webhook trigger is allowed.</span></span>
-   <span data-ttu-id="dba86-695">Nie powinna mieć żadnej trasy zdefiniowane.</span><span class="sxs-lookup"><span data-stu-id="dba86-695">It should not have any route defined.</span></span>
-   <span data-ttu-id="dba86-696">Tylko "funkcji" i "anonymous" autoryzacji na poziomie jest dozwolone.</span><span class="sxs-lookup"><span data-stu-id="dba86-696">Only "function" and "anonymous" authorization level is allowed.</span></span>

<span data-ttu-id="dba86-697">adres URL wyzwalacza Hello jest pobrać, w pamięci podręcznej i używany w czasie wykonywania.</span><span class="sxs-lookup"><span data-stu-id="dba86-697">hello trigger URL is retrieved, cached, and used at runtime.</span></span> <span data-ttu-id="dba86-698">Dlatego jeśli żadnej operacji unieważnia URL hello w pamięci podręcznej, hello akcja zakończy się niepowodzeniem w czasie wykonywania.</span><span class="sxs-lookup"><span data-stu-id="dba86-698">So if any operation invalidates hello cached URL, hello action fails at runtime.</span></span> <span data-ttu-id="dba86-699">toowork wokół, Zapisz hello aplikacji logiki ponownie, co będzie powodować tooretrieve aplikacji logiki i pamięci podręcznej adres URL wyzwalacza hello ponownie.</span><span class="sxs-lookup"><span data-stu-id="dba86-699">toowork around this, save hello logic app again, which will cause logic app tooretrieve and cache hello trigger URL again.</span></span>

## <a name="collection-actions-scopes-and-loops"></a><span data-ttu-id="dba86-700">Akcje kolekcji (zakresy i pętle)</span><span class="sxs-lookup"><span data-stu-id="dba86-700">Collection actions (scopes and loops)</span></span>

<span data-ttu-id="dba86-701">Niektóre typy działań mogą zawierać działania w ramach samodzielnie.</span><span class="sxs-lookup"><span data-stu-id="dba86-701">Some action types can contain actions within themselves.</span></span> <span data-ttu-id="dba86-702">Odwołanie do działań w ramach kolekcji można odwoływać się bezpośrednio poza hello kolekcji.</span><span class="sxs-lookup"><span data-stu-id="dba86-702">Reference actions within a collection can be referenced directly outside of hello collection.</span></span> <span data-ttu-id="dba86-703">Jeśli zdefiniowano `http` w zakresie `@body('http')` jest nadal ważny w dowolnym miejscu w przepływie pracy.</span><span class="sxs-lookup"><span data-stu-id="dba86-703">If you defined `http` in a scope, `@body('http')` is still valid anywhere in a workflow.</span></span> <span data-ttu-id="dba86-704">Akcje w ramach kolekcji można `runAfter` tylko innych działań w ramach hello tej samej kolekcji.</span><span class="sxs-lookup"><span data-stu-id="dba86-704">Actions within a collection can `runAfter` only other actions within hello same collection.</span></span>

## <a name="scope-action"></a><span data-ttu-id="dba86-705">Akcja zakresu</span><span class="sxs-lookup"><span data-stu-id="dba86-705">Scope action</span></span>

<span data-ttu-id="dba86-706">Witaj `scope` pozwala logicznie grupy działań w przepływie pracy.</span><span class="sxs-lookup"><span data-stu-id="dba86-706">hello `scope` action lets you logically group actions in a workflow.</span></span>

|<span data-ttu-id="dba86-707">Nazwa</span><span class="sxs-lookup"><span data-stu-id="dba86-707">Name</span></span>|<span data-ttu-id="dba86-708">Wymagane</span><span class="sxs-lookup"><span data-stu-id="dba86-708">Required</span></span>|<span data-ttu-id="dba86-709">Typ</span><span class="sxs-lookup"><span data-stu-id="dba86-709">Type</span></span>|<span data-ttu-id="dba86-710">Opis</span><span class="sxs-lookup"><span data-stu-id="dba86-710">Description</span></span>|  
|--------|------------|--------|---------------|  
|<span data-ttu-id="dba86-711">Akcje</span><span class="sxs-lookup"><span data-stu-id="dba86-711">actions</span></span>|<span data-ttu-id="dba86-712">Tak</span><span class="sxs-lookup"><span data-stu-id="dba86-712">Yes</span></span>|<span data-ttu-id="dba86-713">Obiekt</span><span class="sxs-lookup"><span data-stu-id="dba86-713">Object</span></span>|<span data-ttu-id="dba86-714">Tooexecute wewnętrzny akcje w zakresie hello</span><span class="sxs-lookup"><span data-stu-id="dba86-714">Inner actions tooexecute within hello scope</span></span>|

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

## <a name="foreach-action"></a><span data-ttu-id="dba86-715">Akcja ForEach</span><span class="sxs-lookup"><span data-stu-id="dba86-715">ForEach action</span></span>

<span data-ttu-id="dba86-716">Ta akcja pętli iteruje tablicy i wykonuje akcje wewnętrzny dla każdego elementu.</span><span class="sxs-lookup"><span data-stu-id="dba86-716">This looping action iterates through an array and performs inner actions for each item.</span></span> <span data-ttu-id="dba86-717">Domyślnie program hello foreach pętla jest wykonywana równolegle (20 wykonaniami równolegle w czasie).</span><span class="sxs-lookup"><span data-stu-id="dba86-717">By default, hello foreach loop executes in parallel (20 executions in parallel at a time).</span></span> <span data-ttu-id="dba86-718">Można ustawić zasady wykonywania przy użyciu hello `operationOptions` parametru.</span><span class="sxs-lookup"><span data-stu-id="dba86-718">You can set execution rules using hello `operationOptions` parameter.</span></span>

|<span data-ttu-id="dba86-719">Nazwa</span><span class="sxs-lookup"><span data-stu-id="dba86-719">Name</span></span>|<span data-ttu-id="dba86-720">Wymagane</span><span class="sxs-lookup"><span data-stu-id="dba86-720">Required</span></span>|<span data-ttu-id="dba86-721">Typ</span><span class="sxs-lookup"><span data-stu-id="dba86-721">Type</span></span>|<span data-ttu-id="dba86-722">Opis</span><span class="sxs-lookup"><span data-stu-id="dba86-722">Description</span></span>|  
|--------|------------|--------|---------------|  
|<span data-ttu-id="dba86-723">Akcje</span><span class="sxs-lookup"><span data-stu-id="dba86-723">actions</span></span>|<span data-ttu-id="dba86-724">Tak</span><span class="sxs-lookup"><span data-stu-id="dba86-724">Yes</span></span>|<span data-ttu-id="dba86-725">Obiekt</span><span class="sxs-lookup"><span data-stu-id="dba86-725">Object</span></span>|<span data-ttu-id="dba86-726">Tooexecute wewnętrzny akcje w ramach hello pętli</span><span class="sxs-lookup"><span data-stu-id="dba86-726">Inner actions tooexecute within hello loop</span></span>|
|<span data-ttu-id="dba86-727">Instrukcja foreach</span><span class="sxs-lookup"><span data-stu-id="dba86-727">foreach</span></span>|<span data-ttu-id="dba86-728">Tak</span><span class="sxs-lookup"><span data-stu-id="dba86-728">Yes</span></span>|<span data-ttu-id="dba86-729">Ciąg</span><span class="sxs-lookup"><span data-stu-id="dba86-729">string</span></span>|<span data-ttu-id="dba86-730">Witaj tooiterate tablicy za pośrednictwem</span><span class="sxs-lookup"><span data-stu-id="dba86-730">hello array tooiterate over</span></span>|
|<span data-ttu-id="dba86-731">operationOptions</span><span class="sxs-lookup"><span data-stu-id="dba86-731">operationOptions</span></span>|<span data-ttu-id="dba86-732">Brak</span><span class="sxs-lookup"><span data-stu-id="dba86-732">no</span></span>|<span data-ttu-id="dba86-733">Ciąg</span><span class="sxs-lookup"><span data-stu-id="dba86-733">string</span></span>|<span data-ttu-id="dba86-734">Wszystkie opcje operacji zachowanie.</span><span class="sxs-lookup"><span data-stu-id="dba86-734">Any operation options for behavior.</span></span> <span data-ttu-id="dba86-735">Aktualnie obsługuje tylko `sequential` iteracji tooexecute sekwencyjnie (domyślne zachowanie to równoległych)</span><span class="sxs-lookup"><span data-stu-id="dba86-735">Currently only supports `sequential` tooexecute iterations sequentially (default behavior is parallel)</span></span>|

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

## <a name="until-action"></a><span data-ttu-id="dba86-736">Do działania</span><span class="sxs-lookup"><span data-stu-id="dba86-736">Until action</span></span>

<span data-ttu-id="dba86-737">Ta akcja pętli wykonuje akcje wewnętrzny dopóki tootrue powoduje warunek.</span><span class="sxs-lookup"><span data-stu-id="dba86-737">This looping action executes inner actions until a condition results tootrue.</span></span>

|<span data-ttu-id="dba86-738">Nazwa</span><span class="sxs-lookup"><span data-stu-id="dba86-738">Name</span></span>|<span data-ttu-id="dba86-739">Wymagane</span><span class="sxs-lookup"><span data-stu-id="dba86-739">Required</span></span>|<span data-ttu-id="dba86-740">Typ</span><span class="sxs-lookup"><span data-stu-id="dba86-740">Type</span></span>|<span data-ttu-id="dba86-741">Opis</span><span class="sxs-lookup"><span data-stu-id="dba86-741">Description</span></span>|  
|--------|------------|--------|---------------|  
|<span data-ttu-id="dba86-742">Akcje</span><span class="sxs-lookup"><span data-stu-id="dba86-742">actions</span></span>|<span data-ttu-id="dba86-743">Tak</span><span class="sxs-lookup"><span data-stu-id="dba86-743">Yes</span></span>|<span data-ttu-id="dba86-744">Obiekt</span><span class="sxs-lookup"><span data-stu-id="dba86-744">Object</span></span>|<span data-ttu-id="dba86-745">Tooexecute wewnętrzny akcje w ramach hello pętli</span><span class="sxs-lookup"><span data-stu-id="dba86-745">Inner actions tooexecute within hello loop</span></span>|
|<span data-ttu-id="dba86-746">wyrażenie</span><span class="sxs-lookup"><span data-stu-id="dba86-746">expression</span></span>|<span data-ttu-id="dba86-747">Tak</span><span class="sxs-lookup"><span data-stu-id="dba86-747">Yes</span></span>|<span data-ttu-id="dba86-748">Ciąg</span><span class="sxs-lookup"><span data-stu-id="dba86-748">string</span></span>|<span data-ttu-id="dba86-749">Witaj tooevaluate wyrażenie po każdej iteracji</span><span class="sxs-lookup"><span data-stu-id="dba86-749">hello expression tooevaluate after each iteration</span></span>|
|<span data-ttu-id="dba86-750">Limit</span><span class="sxs-lookup"><span data-stu-id="dba86-750">limit</span></span>|<span data-ttu-id="dba86-751">Tak</span><span class="sxs-lookup"><span data-stu-id="dba86-751">yes</span></span>|<span data-ttu-id="dba86-752">Obiekt</span><span class="sxs-lookup"><span data-stu-id="dba86-752">Object</span></span>|<span data-ttu-id="dba86-753">limity Hello hello pętli — co najmniej jeden limit musi być zdefiniowana</span><span class="sxs-lookup"><span data-stu-id="dba86-753">hello limits for hello loop - at least one limit must be defined</span></span>|
|<span data-ttu-id="dba86-754">Liczba</span><span class="sxs-lookup"><span data-stu-id="dba86-754">count</span></span>|<span data-ttu-id="dba86-755">Brak</span><span class="sxs-lookup"><span data-stu-id="dba86-755">no</span></span>|<span data-ttu-id="dba86-756">int</span><span class="sxs-lookup"><span data-stu-id="dba86-756">int</span></span>|<span data-ttu-id="dba86-757">Hello limit toohello liczba iteracji, które mogą być wykonywane</span><span class="sxs-lookup"><span data-stu-id="dba86-757">hello limit toohello number of iterations that can be performed</span></span>|
|<span data-ttu-id="dba86-758">timeout</span><span class="sxs-lookup"><span data-stu-id="dba86-758">timeout</span></span>|<span data-ttu-id="dba86-759">Brak</span><span class="sxs-lookup"><span data-stu-id="dba86-759">no</span></span>|<span data-ttu-id="dba86-760">Ciąg</span><span class="sxs-lookup"><span data-stu-id="dba86-760">string</span></span>|<span data-ttu-id="dba86-761">Witaj limitu czasu dla jak długo powinien pętli.</span><span class="sxs-lookup"><span data-stu-id="dba86-761">hello timeout for how long it should loop.</span></span>  <span data-ttu-id="dba86-762">Formacie ISO 8601</span><span class="sxs-lookup"><span data-stu-id="dba86-762">ISO 8601 format</span></span>|


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

## <a name="conditions---if-action"></a><span data-ttu-id="dba86-763">Warunki — Jeśli akcja</span><span class="sxs-lookup"><span data-stu-id="dba86-763">Conditions - If Action</span></span>

<span data-ttu-id="dba86-764">Witaj `If` pozwala ocenić warunku i wykonywanie gałęzi oparte na czy hello wynikiem wyrażenia jest zbyt`true`.</span><span class="sxs-lookup"><span data-stu-id="dba86-764">hello `If` action lets you evaluate a condition and execute a branch based on whether hello expression evaluates too`true`.</span></span>

|<span data-ttu-id="dba86-765">Nazwa</span><span class="sxs-lookup"><span data-stu-id="dba86-765">Name</span></span>|<span data-ttu-id="dba86-766">Wymagane</span><span class="sxs-lookup"><span data-stu-id="dba86-766">Required</span></span>|<span data-ttu-id="dba86-767">Typ</span><span class="sxs-lookup"><span data-stu-id="dba86-767">Type</span></span>|<span data-ttu-id="dba86-768">Opis</span><span class="sxs-lookup"><span data-stu-id="dba86-768">Description</span></span>|  
|--------|------------|--------|---------------|  
|<span data-ttu-id="dba86-769">Akcje</span><span class="sxs-lookup"><span data-stu-id="dba86-769">actions</span></span>|<span data-ttu-id="dba86-770">Tak</span><span class="sxs-lookup"><span data-stu-id="dba86-770">Yes</span></span>|<span data-ttu-id="dba86-771">Obiekt</span><span class="sxs-lookup"><span data-stu-id="dba86-771">Object</span></span>|<span data-ttu-id="dba86-772">Tooexecute wewnętrzny akcje, gdy wyrażenie zbyt`true`</span><span class="sxs-lookup"><span data-stu-id="dba86-772">Inner actions tooexecute when expression evaluates too`true`</span></span>|
|<span data-ttu-id="dba86-773">wyrażenie</span><span class="sxs-lookup"><span data-stu-id="dba86-773">expression</span></span>|<span data-ttu-id="dba86-774">Tak</span><span class="sxs-lookup"><span data-stu-id="dba86-774">Yes</span></span>|<span data-ttu-id="dba86-775">Ciąg</span><span class="sxs-lookup"><span data-stu-id="dba86-775">string</span></span>|<span data-ttu-id="dba86-776">Witaj tooevaluate wyrażenia</span><span class="sxs-lookup"><span data-stu-id="dba86-776">hello expression tooevaluate</span></span>|
|<span data-ttu-id="dba86-777">else</span><span class="sxs-lookup"><span data-stu-id="dba86-777">else</span></span>|<span data-ttu-id="dba86-778">Brak</span><span class="sxs-lookup"><span data-stu-id="dba86-778">no</span></span>|<span data-ttu-id="dba86-779">Obiekt</span><span class="sxs-lookup"><span data-stu-id="dba86-779">Object</span></span>|<span data-ttu-id="dba86-780">Tooexecute wewnętrzny akcje, gdy wyrażenie zbyt`false`</span><span class="sxs-lookup"><span data-stu-id="dba86-780">Inner actions tooexecute when expression evaluates too`false`</span></span>|
  
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
  
<span data-ttu-id="dba86-781">Witaj poniższej tabeli przedstawiono przykłady warunków użycia wyrażeń w akcji:</span><span class="sxs-lookup"><span data-stu-id="dba86-781">hello following table shows examples of how conditions can use expressions in an action:</span></span>  
  
|<span data-ttu-id="dba86-782">Wartość JSON</span><span class="sxs-lookup"><span data-stu-id="dba86-782">JSON value</span></span>|<span data-ttu-id="dba86-783">wynik</span><span class="sxs-lookup"><span data-stu-id="dba86-783">Result</span></span>|  
|--------------|----------|  
|`"expression": "@parameters('hasSpecialAction')"`|<span data-ttu-id="dba86-784">Żadnej wartości, które są używane do oceny tootrue powoduje, że toopass tego warunku.</span><span class="sxs-lookup"><span data-stu-id="dba86-784">Any value that would evaluate tootrue causes this condition toopass.</span></span> <span data-ttu-id="dba86-785">Obsługiwane są tylko wyrażenia logiczne.</span><span class="sxs-lookup"><span data-stu-id="dba86-785">Only Boolean expressions are supported.</span></span> <span data-ttu-id="dba86-786">tooconvert innych typów tooBoolean, użyj funkcji `empty`, `equals`.</span><span class="sxs-lookup"><span data-stu-id="dba86-786">tooconvert other types tooBoolean, use functions `empty`, `equals`.</span></span>|  
|`"expression": "@greater(actions('act1').output.value, parameters('threshold'))"`|<span data-ttu-id="dba86-787">Porównanie funkcji są obsługiwane.</span><span class="sxs-lookup"><span data-stu-id="dba86-787">Comparison functions are supported.</span></span> <span data-ttu-id="dba86-788">Przykładowo hello tutaj hello akcji tylko wykonuje się, gdy dane wyjściowe hello act1 jest większy niż próg hello.</span><span class="sxs-lookup"><span data-stu-id="dba86-788">For hello example here, hello action only executes when hello output of act1 is greater than hello threshold.</span></span>|  
|`"expression": "@or(greater(actions('act1').output.value, parameters('threshold')), less(actions('act1').output.value, 100))"`|<span data-ttu-id="dba86-789">Funkcje logiki są również obsługiwane toocreate zagnieżdżonych wyrażeń logicznych.</span><span class="sxs-lookup"><span data-stu-id="dba86-789">Logic functions are also supported toocreate nested Boolean expressions.</span></span> <span data-ttu-id="dba86-790">W takim przypadku hello operacja zostanie wykonana, gdy dane wyjściowe hello act1 jest powyżej wartości progowej hello lub poniżej 100.</span><span class="sxs-lookup"><span data-stu-id="dba86-790">In this case, hello action executes when hello output of act1 is above hello threshold or below 100.</span></span>|  
|`"expression": "@equals(length(actions('act1').outputs.errors), 0))"`|<span data-ttu-id="dba86-791">Toocheck funkcje tablicy można użyć, jeśli tablicy nie ma żadnych elementów.</span><span class="sxs-lookup"><span data-stu-id="dba86-791">You can use array functions toocheck if an array has any items.</span></span> <span data-ttu-id="dba86-792">W takim przypadku hello operacja zostanie wykonana, gdy hello błędy tablica jest pusta.</span><span class="sxs-lookup"><span data-stu-id="dba86-792">In this case, hello action executes when hello errors array is empty.</span></span>| 
|`"expression": "parameters('hasSpecialAction')"`|<span data-ttu-id="dba86-793">Błąd — nie jest prawidłowym warunku, ponieważ @ jest wymagany dla warunków.</span><span class="sxs-lookup"><span data-stu-id="dba86-793">Error - not a valid condition because @ is required for conditions.</span></span>|  
  
<span data-ttu-id="dba86-794">Jeśli wynikiem warunku jest pomyślnie, warunek hello jest oznaczony jako `Succeeded`.</span><span class="sxs-lookup"><span data-stu-id="dba86-794">If a condition evaluates successfully, hello condition is marked as `Succeeded`.</span></span> <span data-ttu-id="dba86-795">Akcje w ramach jednej hello `actions` lub `else` obiektów ocenić za`Succeeded` po wykonaniu i zakończyło się pomyślnie, `Failed` po wykonaniu i nie powiodło się, lub `Skipped` po gałąź, nie została wykonana.</span><span class="sxs-lookup"><span data-stu-id="dba86-795">Actions within either hello `actions` or `else` objects evaluate too`Succeeded` when executed and succeeded, `Failed` when executed and failed, or `Skipped` when that branch is not executed.</span></span>

## <a name="next-steps"></a><span data-ttu-id="dba86-796">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="dba86-796">Next steps</span></span>

[<span data-ttu-id="dba86-797">Interfejs API REST usługi przepływu pracy</span><span class="sxs-lookup"><span data-stu-id="dba86-797">Workflow Service REST API</span></span>](https://docs.microsoft.com/rest/api/logic/workflows)
