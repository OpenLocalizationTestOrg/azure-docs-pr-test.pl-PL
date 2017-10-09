---
title: "aaaError & obsługi wyjątków — usługi Azure Logic Apps | Dokumentacja firmy Microsoft"
description: "Wzorce dla błędów i obsługa wyjątków w aplikacjach logiki platformy Azure"
services: logic-apps
documentationcenter: .net,nodejs,java
author: jeffhollan
manager: anneta
editor: 
ms.assetid: e50ab2f2-1fdc-4d2a-be40-995a6cc5a0d4
ms.service: logic-apps
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 10/18/2016
ms.author: LADocs; jehollan
ms.openlocfilehash: 326a252310c8dfb154e583f91c9421675e448d1f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="handle-errors-and-exceptions-in-azure-logic-apps"></a><span data-ttu-id="40898-103">Obsługa błędów i wyjątków w aplikacjach logiki platformy Azure</span><span class="sxs-lookup"><span data-stu-id="40898-103">Handle errors and exceptions in Azure Logic Apps</span></span>

<span data-ttu-id="40898-104">Aplikacje logiki platformy Azure udostępnia zaawansowane narzędzia i wzorce toohelp możesz upewnij się, że Twoje integracji są niezawodne i podatne na błędy.</span><span class="sxs-lookup"><span data-stu-id="40898-104">Azure Logic Apps provides rich tools and patterns toohelp you make sure your integrations are robust and resilient against failures.</span></span> <span data-ttu-id="40898-105">Wszelkie architektury integracji stanowi wyzwanie hello dokonywania tooappropriately się, że dojście przestój lub problemów z systemów zależnych.</span><span class="sxs-lookup"><span data-stu-id="40898-105">Any integration architecture poses hello challenge of making sure tooappropriately handle downtime or issues from dependent systems.</span></span> <span data-ttu-id="40898-106">Logic Apps ułatwia obsługi błędów najwyższej jakości środowisko, umożliwiając hello narzędzia potrzebne tooact na wyjątków i błędów w swoich przepływach pracy.</span><span class="sxs-lookup"><span data-stu-id="40898-106">Logic Apps makes handling errors a first-class experience, giving you hello tools you need tooact on exceptions and errors in your workflows.</span></span>

## <a name="retry-policies"></a><span data-ttu-id="40898-107">Spróbuj ponownie zasad</span><span class="sxs-lookup"><span data-stu-id="40898-107">Retry policies</span></span>

<span data-ttu-id="40898-108">Zasady ponawiania jest hello najbardziej podstawowym typem wyjątku i obsługa błędów.</span><span class="sxs-lookup"><span data-stu-id="40898-108">A retry policy is hello most basic type of exception and error handling.</span></span> <span data-ttu-id="40898-109">Jeśli upłynął limit czasu żądania początkowego, lub nie powiodło się (każde żądanie, która powoduje 429 lub odpowiedź 5xx), te zasady określa, czy akcja hello powinna ponowić.</span><span class="sxs-lookup"><span data-stu-id="40898-109">If an initial request timed out or failed (any request that results in a 429 or 5xx response), this policy defines whether hello action should retry.</span></span> <span data-ttu-id="40898-110">Domyślnie wszystkie akcje próbę 4 razy dodatkowe za pośrednictwem 20 sekund.</span><span class="sxs-lookup"><span data-stu-id="40898-110">By default, all actions retry 4 additional times over 20-second intervals.</span></span> <span data-ttu-id="40898-111">Dlatego w przypadku pierwszego żądania hello odbiera `500 Internal Server Error` odpowiedzi, aparatu przepływu pracy hello wstrzymuje 20 sekund i prób hello żądanie ponownie.</span><span class="sxs-lookup"><span data-stu-id="40898-111">So if hello first request receives a `500 Internal Server Error` response, hello workflow engine pauses for 20 seconds, and attempts hello request again.</span></span> <span data-ttu-id="40898-112">Jeśli po wszystkich próbach odpowiedź hello jest nadal wyjątku lub awarii, nadal hello przepływu pracy oraz znaczniki hello stanu akcji jako `Failed`.</span><span class="sxs-lookup"><span data-stu-id="40898-112">If after all retries, hello response is still an exception or failure, hello workflow continues and marks hello action status as `Failed`.</span></span>

<span data-ttu-id="40898-113">Można skonfigurować zasady ponawiania w hello **dane wejściowe** dla określonej akcji.</span><span class="sxs-lookup"><span data-stu-id="40898-113">You can configure retry policies in hello **inputs** for a particular action.</span></span> <span data-ttu-id="40898-114">Na przykład skonfigurować tootry zasady ponawiania maksymalnie 4 czasy przez 1 godzinę.</span><span class="sxs-lookup"><span data-stu-id="40898-114">For example, you can configure a retry policy tootry as many as 4 times over 1-hour intervals.</span></span> <span data-ttu-id="40898-115">Aby uzyskać szczegółowe informacje o właściwościach wejściowego, zobacz [działania przepływu pracy i wyzwalaczy][retryPolicyMSDN].</span><span class="sxs-lookup"><span data-stu-id="40898-115">For full details about input properties, see [Workflow Actions and Triggers][retryPolicyMSDN].</span></span>

```json
"retryPolicy" : {
      "type": "<type-of-retry-policy>",
      "interval": <retry-interval>,
      "count": <number-of-retry-attempts>
    }
```

<span data-ttu-id="40898-116">Jeśli chciał Twojej tooretry akcji HTTP 4 godziny, a następnie odczekaj 10 minut między kolejnymi próbami, należy użyć powitania po definicji:</span><span class="sxs-lookup"><span data-stu-id="40898-116">If you wanted your HTTP action tooretry 4 times and wait 10 minutes between each attempt, you would use hello following definition:</span></span>

```json
"HTTP": 
{
    "inputs": {
        "method": "GET",
        "uri": "http://myAPIendpoint/api/action",
        "retryPolicy" : {
            "type": "fixed",
            "interval": "PT10M",
            "count": 4
        }
    },
    "runAfter": {},
    "type": "Http"
}
```

<span data-ttu-id="40898-117">Aby uzyskać więcej informacji o obsługiwanych składni, zobacz hello [części zasady ponawiania akcji przepływu pracy i wyzwalaczy][retryPolicyMSDN].</span><span class="sxs-lookup"><span data-stu-id="40898-117">For more information on supported syntax, see hello [retry-policy section in Workflow Actions and Triggers][retryPolicyMSDN].</span></span>

## <a name="catch-failures-with-hello-runafter-property"></a><span data-ttu-id="40898-118">Błędy z hello właściwości RunAfter catch</span><span class="sxs-lookup"><span data-stu-id="40898-118">Catch failures with hello RunAfter property</span></span>

<span data-ttu-id="40898-119">Każde działanie aplikacji logiki deklaruje akcje, które muszą zostać zakończone przed uruchomieniem akcji hello, takich jak kolejność kroków hello w przepływie pracy.</span><span class="sxs-lookup"><span data-stu-id="40898-119">Each logic app action declares which actions must finish before hello action starts, like ordering hello steps in your workflow.</span></span> <span data-ttu-id="40898-120">W definicji działania hello, ta kolejność nosi nazwę hello `runAfter` właściwości.</span><span class="sxs-lookup"><span data-stu-id="40898-120">In hello action definition, this ordering is known as hello `runAfter` property.</span></span> <span data-ttu-id="40898-121">Ta właściwość jest obiekt, który opisano, które akcje i stany akcji wykonać hello akcji.</span><span class="sxs-lookup"><span data-stu-id="40898-121">This property is an object that describes which actions and action statuses execute hello action.</span></span> <span data-ttu-id="40898-122">Domyślnie wszystkie akcje dodane za pomocą projektanta aplikacji logiki hello są ustawiane za`runAfter` hello poprzedniego kroku, jeśli hello poprzedniego kroku `Succeeded`.</span><span class="sxs-lookup"><span data-stu-id="40898-122">By default, all actions added through hello Logic App Designer are set too`runAfter` hello previous step if hello previous step `Succeeded`.</span></span> <span data-ttu-id="40898-123">Jednak dostosować ten akcje toofire wartość podczas poprzedniej akcji ma `Failed`, `Skipped`, lub zestaw możliwych tych wartości.</span><span class="sxs-lookup"><span data-stu-id="40898-123">However, you can customize this value toofire actions when previous actions have `Failed`, `Skipped`, or a possible set of these values.</span></span> <span data-ttu-id="40898-124">Jeśli potrzebujesz tooadd tooa elementu wyznaczony tematu usługi Service Bus po określonym działaniu `Insert_Row` kończy się niepowodzeniem, można użyć następującego hello `runAfter` konfiguracji:</span><span class="sxs-lookup"><span data-stu-id="40898-124">If you wanted tooadd an item tooa designated Service Bus topic after a specific action `Insert_Row` fails, you could use hello following `runAfter` configuration:</span></span>

```json
"Send_message": {
    "inputs": {
        "body": {
            "ContentData": "@{encodeBase64(body('Insert_Row'))}",
            "ContentType": "{ \"content-type\" : \"application/json\" }"
        },
        "host": {
            "api": {
                "runtimeUrl": "https://logic-apis-westus.azure-apim.net/apim/servicebus"
            },
            "connection": {
                "name": "@parameters('$connections')['servicebus']['connectionId']"
            }
        },
        "method": "post",
        "path": "/@{encodeURIComponent('failures')}/messages"
    },
    "runAfter": {
        "Insert_Row": [
            "Failed"
        ]
    }
}
```

<span data-ttu-id="40898-125">Powiadomienie hello `runAfter` ustawiono właściwość toofire Jeśli hello `Insert_Row` akcji jest `Failed`.</span><span class="sxs-lookup"><span data-stu-id="40898-125">Notice hello `runAfter` property is set toofire if hello `Insert_Row` action is `Failed`.</span></span> <span data-ttu-id="40898-126">Akcja hello toorun, jeśli jest w stanie akcji hello `Succeeded`, `Failed`, lub `Skipped`, należy użyć następującej składni:</span><span class="sxs-lookup"><span data-stu-id="40898-126">toorun hello action if hello action status is `Succeeded`, `Failed`, or `Skipped`, use this syntax:</span></span>

```json
"runAfter": {
        "Insert_Row": [
            "Failed", "Succeeded", "Skipped"
        ]
    }
```

> [!TIP]
> <span data-ttu-id="40898-127">Akcje, które są uruchomione i pomyślnie zakończone po poprzednim akcja nie powiodła się, są oznaczone jako `Succeeded`.</span><span class="sxs-lookup"><span data-stu-id="40898-127">Actions that run and complete successfully after a preceding action has failed, are marked as `Succeeded`.</span></span> <span data-ttu-id="40898-128">Oznacza to zachowanie, że jeśli możesz pomyślnie catch wszystkich błędów w przepływie pracy, hello uruchamiane samoczynnie jest oznaczone jako `Succeeded`.</span><span class="sxs-lookup"><span data-stu-id="40898-128">This behavior means that if you successfully catch all failures in a workflow, hello run itself is marked as `Succeeded`.</span></span>

## <a name="scopes-and-results-tooevaluate-actions"></a><span data-ttu-id="40898-129">Akcje tooevaluate zakresy i wyniki</span><span class="sxs-lookup"><span data-stu-id="40898-129">Scopes and results tooevaluate actions</span></span>

<span data-ttu-id="40898-130">Podobne toohow można uruchomić po poszczególnych działań, można także pogrupować Akcje wewnątrz [zakres](../logic-apps/logic-apps-loops-and-scopes.md), działających jako logiczne grupowanie akcje.</span><span class="sxs-lookup"><span data-stu-id="40898-130">Similar toohow you can run after individual actions, you can also group actions together inside a [scope](../logic-apps/logic-apps-loops-and-scopes.md), which act as a logical grouping of actions.</span></span> <span data-ttu-id="40898-131">Zakresy są przydatne, zarówno do organizowania akcji aplikacji logiki, jak i do wykonywania agregacji oceny stanu hello zakresu.</span><span class="sxs-lookup"><span data-stu-id="40898-131">Scopes are useful both for organizing your logic app actions, and for performing aggregate evaluations on hello status of a scope.</span></span> <span data-ttu-id="40898-132">zakres Hello, sama przechodzi w stan po ukończeniu wszystkich działań w zakresie.</span><span class="sxs-lookup"><span data-stu-id="40898-132">hello scope itself receives a status after all actions in a scope have finished.</span></span> <span data-ttu-id="40898-133">stan zakresu Hello jest określany hello te same kryteria jak Uruchom.</span><span class="sxs-lookup"><span data-stu-id="40898-133">hello scope status is determined with hello same criteria as a run.</span></span> <span data-ttu-id="40898-134">Jeśli akcja końcowego hello w gałęzi wykonywania jest `Failed` lub `Aborted`, jest w stanie hello `Failed`.</span><span class="sxs-lookup"><span data-stu-id="40898-134">If hello final action in an execution branch is `Failed` or `Aborted`, hello status is `Failed`.</span></span>

<span data-ttu-id="40898-135">toofire określonych akcji dla wszystkich błędów, które wystąpiły w zakresie hello, można użyć `runAfter` z zakresem, który jest oznaczony jako `Failed`.</span><span class="sxs-lookup"><span data-stu-id="40898-135">toofire specific actions for any failures that happened within hello scope, you can use `runAfter` with a scope that is marked `Failed`.</span></span> <span data-ttu-id="40898-136">Jeśli *żadnych* akcje w zakresie hello zakończyć się niepowodzeniem, po zakresu zakończy się niepowodzeniem pozwala utworzyć toocatch jednej akcji błędów.</span><span class="sxs-lookup"><span data-stu-id="40898-136">If *any* actions in hello scope fail, running after a scope fails lets you create a single action toocatch failures.</span></span>

### <a name="getting-hello-context-of-failures-with-results"></a><span data-ttu-id="40898-137">Uzyskanie kontekstu hello niepowodzeń z wynikami</span><span class="sxs-lookup"><span data-stu-id="40898-137">Getting hello context of failures with results</span></span>

<span data-ttu-id="40898-138">Mimo że przechwytywanie błędów z zakresu jest przydatne, można także toohelp kontekstu zrozumieć dokładnie akcje, które nie powiodło się, a jakiekolwiek błędy i kodów stanu, które zostały zwrócone.</span><span class="sxs-lookup"><span data-stu-id="40898-138">Although catching failures from a scope is useful, you might also want context toohelp you understand exactly which actions failed, and any errors or status codes that were returned.</span></span> <span data-ttu-id="40898-139">Witaj `@result()` funkcji przepływu pracy zawierają kontekst o wyniku hello wszystkich działań w zakresie.</span><span class="sxs-lookup"><span data-stu-id="40898-139">hello `@result()` workflow function provides context about hello result of all actions in a scope.</span></span>

<span data-ttu-id="40898-140">`@result()`przyjmuje jeden parametr, nazwa zakresu i zwraca tablicę wszystkich wyników akcji hello z tego zakresu.</span><span class="sxs-lookup"><span data-stu-id="40898-140">`@result()` takes a single parameter, scope name, and returns an array of all hello action results from within that scope.</span></span> <span data-ttu-id="40898-141">Te obiekty działania obejmują takie same atrybuty jako hello hello `@actions()` generuje obiekt, w tym czas rozpoczęcia działania, czas zakończenia działania stanu akcji, dane wejściowe działań, identyfikatorów korelacji działania i akcji.</span><span class="sxs-lookup"><span data-stu-id="40898-141">These action objects include hello same attributes as hello `@actions()` object, including action start time, action end time, action status, action inputs, action correlation IDs, and action outputs.</span></span> <span data-ttu-id="40898-142">kontekst toosend wszystkie akcje, które nie powiodło się w zakresie, można łatwo parowania `@result()` działać z `runAfter`.</span><span class="sxs-lookup"><span data-stu-id="40898-142">toosend context of any actions that failed within a scope, you can easily pair an `@result()` function with a `runAfter`.</span></span>

<span data-ttu-id="40898-143">tooexecute akcji *dla każdego* akcji w zakresie który `Failed`, filtr hello tablicę tooactions wyników zakończonych niepowodzeniem, może łączyć `@result()` z  **[tablicy filtrów](../connectors/connectors-native-query.md)**  akcji i  **[ForEach](../logic-apps/logic-apps-loops-and-scopes.md)**  pętli.</span><span class="sxs-lookup"><span data-stu-id="40898-143">tooexecute an action *for each* action in a scope that `Failed`, filter hello array of results tooactions that failed, you can pair `@result()` with a **[Filter Array](../connectors/connectors-native-query.md)** action and a **[ForEach](../logic-apps/logic-apps-loops-and-scopes.md)** loop.</span></span> <span data-ttu-id="40898-144">Możesz pobrać tablica wynikowa filtrowane hello i wykonania czynności dla każdego błędu przy użyciu hello **ForEach** pętli.</span><span class="sxs-lookup"><span data-stu-id="40898-144">You can take hello filtered result array and perform an action for each failure using hello **ForEach** loop.</span></span> <span data-ttu-id="40898-145">Oto przykład, a następnie szczegółowy opis, który wysyła żądanie HTTP POST z treści odpowiedzi hello wszystkie akcje, które nie powiodło się w zakresie hello `My_Scope`.</span><span class="sxs-lookup"><span data-stu-id="40898-145">Here's an example, followed by a detailed explanation, that sends an HTTP POST request with hello response body of any actions that failed within hello scope `My_Scope`.</span></span>

```json
"Filter_array": {
    "inputs": {
        "from": "@result('My_Scope')",
        "where": "@equals(item()['status'], 'Failed')"
    },
    "runAfter": {
        "My_Scope": [
            "Failed"
        ]
    },
    "type": "Query"
},
"For_each": {
    "actions": {
        "Log_Exception": {
            "inputs": {
                "body": "@item()['outputs']['body']",
                "method": "POST",
                "headers": {
                    "x-failed-action-name": "@item()['name']",
                    "x-failed-tracking-id": "@item()['clientTrackingId']"
                },
                "uri": "http://requestb.in/"
            },
            "runAfter": {},
            "type": "Http"
        }
    },
    "foreach": "@body('Filter_array')",
    "runAfter": {
        "Filter_array": [
            "Succeeded"
        ]
    },
    "type": "Foreach"
}
```

<span data-ttu-id="40898-146">Oto toodescribe szczegółowy przewodnik, co się stanie:</span><span class="sxs-lookup"><span data-stu-id="40898-146">Here's a detailed walkthrough toodescribe what happens:</span></span>

1. <span data-ttu-id="40898-147">wynik hello tooget wszystkich akcji w obrębie `My_Scope`, hello **tablicy filtrów** filtry akcji `@result('My_Scope')`.</span><span class="sxs-lookup"><span data-stu-id="40898-147">tooget hello result of all actions within `My_Scope`, hello **Filter Array** action filters `@result('My_Scope')`.</span></span>

2. <span data-ttu-id="40898-148">Witaj warunek **tablicy filtrów** dowolnego `@result()` element, który ma stan równa zbyt`Failed`.</span><span class="sxs-lookup"><span data-stu-id="40898-148">hello condition for **Filter Array** is any `@result()` item that has status equal too`Failed`.</span></span> <span data-ttu-id="40898-149">Ten warunek filtruje hello tablicy o wszystkich wyników akcji z `My_Scope` tablicy tooan tylko z wyników akcji nie powiodło się.</span><span class="sxs-lookup"><span data-stu-id="40898-149">This condition filters hello array with all action results from `My_Scope` tooan array with only failed action results.</span></span>

3. <span data-ttu-id="40898-150">Wykonaj **dla każdego** akcji na powitania **filtrowane tablicy** danych wyjściowych.</span><span class="sxs-lookup"><span data-stu-id="40898-150">Perform a **For Each** action on hello **Filtered Array** outputs.</span></span> <span data-ttu-id="40898-151">Ten krok wykonuje akcję *dla każdego* nie powiodło się wynik akcji, która wcześniej została przefiltrowana.</span><span class="sxs-lookup"><span data-stu-id="40898-151">This step performs an action *for each* failed action result that was previously filtered.</span></span>

    <span data-ttu-id="40898-152">Jeśli jednej akcji w zakresie hello zakończyło się niepowodzeniem, hello akcje w hello `foreach` uruchomić tylko raz.</span><span class="sxs-lookup"><span data-stu-id="40898-152">If a single action in hello scope failed, hello actions in hello `foreach` run only once.</span></span> 
    <span data-ttu-id="40898-153">Wiele zakończonych niepowodzeniem akcje mogą spowodować jedną akcję na błąd.</span><span class="sxs-lookup"><span data-stu-id="40898-153">Many failed actions cause one action per failure.</span></span>

4. <span data-ttu-id="40898-154">Wyślij HTTP POST na powitania `foreach` elementu treści odpowiedzi lub `@item()['outputs']['body']`.</span><span class="sxs-lookup"><span data-stu-id="40898-154">Send an HTTP POST on hello `foreach` item response body, or `@item()['outputs']['body']`.</span></span> <span data-ttu-id="40898-155">Witaj `@result()` kształt element jest sama hello jako hello `@actions()` kształtu i może być analizowana hello sam sposób.</span><span class="sxs-lookup"><span data-stu-id="40898-155">hello `@result()` item shape is hello same as hello `@actions()` shape, and can be parsed hello same way.</span></span>

5. <span data-ttu-id="40898-156">Obejmują dwa Nagłówki niestandardowe o nazwie nieudanych akcji hello `@item()['name']` i powitania klienta uruchamiania, identyfikator śledzenia nie powiodło się `@item()['clientTrackingId']`.</span><span class="sxs-lookup"><span data-stu-id="40898-156">Include two custom headers with hello failed action name `@item()['name']` and hello failed run client tracking ID `@item()['clientTrackingId']`.</span></span>

<span data-ttu-id="40898-157">Odwołania, Oto przykład jedną `@result()` elementu przedstawiający hello `name`, `body`, i `clientTrackingId` właściwości, które są parsowane w poprzednim przykładzie hello.</span><span class="sxs-lookup"><span data-stu-id="40898-157">For reference, here's an example of a single `@result()` item, showing hello `name`, `body`, and `clientTrackingId` properties that are parsed in hello previous example.</span></span> <span data-ttu-id="40898-158">Poza `foreach`, `@result()` zwraca tablicę tych obiektów.</span><span class="sxs-lookup"><span data-stu-id="40898-158">Outside of a `foreach`, `@result()` returns an array of these objects.</span></span>

```json
{
    "name": "Example_Action_That_Failed",
    "inputs": {
        "uri": "https://myfailedaction.azurewebsites.net",
        "method": "POST"
    },
    "outputs": {
        "statusCode": 404,
        "headers": {
            "Date": "Thu, 11 Aug 2016 03:18:18 GMT",
            "Server": "Microsoft-IIS/8.0",
            "X-Powered-By": "ASP.NET",
            "Content-Length": "68",
            "Content-Type": "application/json"
        },
        "body": {
            "code": "ResourceNotFound",
            "message": "/docs/folder-name/resource-name does not exist"
        }
    },
    "startTime": "2016-08-11T03:18:19.7755341Z",
    "endTime": "2016-08-11T03:18:20.2598835Z",
    "trackingId": "bdd82e28-ba2c-4160-a700-e3a8f1a38e22",
    "clientTrackingId": "08587307213861835591296330354",
    "code": "NotFound",
    "status": "Failed"
}
```

<span data-ttu-id="40898-159">tooperform obsługi wyjątków różne wzorce, można użyć wyrażenia hello przedstawione wcześniej.</span><span class="sxs-lookup"><span data-stu-id="40898-159">tooperform different exception handling patterns, you can use hello expressions shown previously.</span></span> <span data-ttu-id="40898-160">Może wybrać tooexecute pojedynczego wyjątków, Obsługa akcji poza zakres hello, który akceptuje hello całego tablicy filtrowane niepowodzeń i Usuń hello `foreach`.</span><span class="sxs-lookup"><span data-stu-id="40898-160">You might choose tooexecute a single exception handling action outside hello scope that accepts hello entire filtered array of failures, and remove hello `foreach`.</span></span> <span data-ttu-id="40898-161">Możesz również uwzględnić innych przydatnych właściwości hello `@result()` odpowiedzi przedstawione wcześniej.</span><span class="sxs-lookup"><span data-stu-id="40898-161">You can also include other useful properties from hello `@result()` response shown previously.</span></span>

## <a name="azure-diagnostics-and-telemetry"></a><span data-ttu-id="40898-162">Diagnostyka Azure i telemetrii</span><span class="sxs-lookup"><span data-stu-id="40898-162">Azure Diagnostics and telemetry</span></span>

<span data-ttu-id="40898-163">Hello poprzedniej wzorce to doskonały sposób toohandle błędy i wyjątki w Uruchom, ale można również zidentyfikować i odpowiadać tooerrors niezależnie od hello uruchomienia.</span><span class="sxs-lookup"><span data-stu-id="40898-163">hello previous patterns are great way toohandle errors and exceptions within a run, but you can also identify and respond tooerrors independent of hello run itself.</span></span> 
<span data-ttu-id="40898-164">[Diagnostyka Azure](../logic-apps/logic-apps-monitor-your-logic-apps.md) zapewnia toosend prosty sposób wszystkie konta magazynu Azure tooan przepływu pracy zdarzenia (w tym wszystkie stany akcji i uruchom) lub usługi Azure Event Hub.</span><span class="sxs-lookup"><span data-stu-id="40898-164">[Azure Diagnostics](../logic-apps/logic-apps-monitor-your-logic-apps.md) provides a simple way toosend all workflow events (including all run and action statuses) tooan Azure Storage account or an Azure Event Hub.</span></span> <span data-ttu-id="40898-165">tooevaluate Uruchom stany, Monitoruj dzienniki hello i metryki lub publikować je do dowolnego narzędzia monitorowania preferowany.</span><span class="sxs-lookup"><span data-stu-id="40898-165">tooevaluate run statuses, you can monitor hello logs and metrics, or publish them into any monitoring tool you prefer.</span></span> <span data-ttu-id="40898-166">Jedną z opcji potencjalnych jest toostream wszystkie zdarzenia hello za pośrednictwem Centrum zdarzeń Azure do [Stream Analytics](https://azure.microsoft.com/services/stream-analytics/).</span><span class="sxs-lookup"><span data-stu-id="40898-166">One potential option is toostream all hello events through Azure Event Hub into [Stream Analytics](https://azure.microsoft.com/services/stream-analytics/).</span></span> <span data-ttu-id="40898-167">W Stream Analytics można zapisywać zapytania na żywo poza wszelkie nieprawidłowości, średnie lub błędy z hello dzienników diagnostycznych.</span><span class="sxs-lookup"><span data-stu-id="40898-167">In Stream Analytics, you can write live queries off any anomalies, averages, or failures from hello diagnostic logs.</span></span> <span data-ttu-id="40898-168">Analiza strumienia może łatwo output tooother źródeł danych, takich jak kolejki, tematy, SQL, bazy danych rozwiązania Cosmos Azure i usługi Power BI.</span><span class="sxs-lookup"><span data-stu-id="40898-168">Stream Analytics can easily output tooother data sources like queues, topics, SQL, Azure Cosmos DB, and Power BI.</span></span>

## <a name="next-steps"></a><span data-ttu-id="40898-169">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="40898-169">Next Steps</span></span>

* [<span data-ttu-id="40898-170">Zobacz, jak klient tworzy błąd obsługi z usługi Azure Logic Apps</span><span class="sxs-lookup"><span data-stu-id="40898-170">See how a customer builds error handling with Azure Logic Apps</span></span>](../logic-apps/logic-apps-scenario-error-and-exception-handling.md)
* [<span data-ttu-id="40898-171">Znajdź więcej Logic Apps przykłady i scenariusze</span><span class="sxs-lookup"><span data-stu-id="40898-171">Find more Logic Apps examples and scenarios</span></span>](../logic-apps/logic-apps-examples-and-scenarios.md)
* [<span data-ttu-id="40898-172">Dowiedz się, jak toocreate automatycznego wdrożenia dla aplikacji logiki</span><span class="sxs-lookup"><span data-stu-id="40898-172">Learn how toocreate automated deployments for logic apps</span></span>](../logic-apps/logic-apps-create-deploy-template.md)
* [<span data-ttu-id="40898-173">Tworzenie i wdrażanie aplikacji logiki w programie Visual Studio</span><span class="sxs-lookup"><span data-stu-id="40898-173">Build and deploy logic apps with Visual Studio</span></span>](logic-apps-deploy-from-vs.md)

<!-- References -->
[retryPolicyMSDN]: https://docs.microsoft.com/rest/api/logic/actions-and-triggers#Anchor_9
