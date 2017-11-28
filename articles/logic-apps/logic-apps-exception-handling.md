---
title: "Obsługa wyjątków — usługi Azure Logic Apps & błędu | Dokumentacja firmy Microsoft"
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
ms.openlocfilehash: 9af2f71b3d288cc6f4e271d0915545d43a1249bc
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="handle-errors-and-exceptions-in-azure-logic-apps"></a><span data-ttu-id="84788-103">Obsługa błędów i wyjątków w aplikacjach logiki platformy Azure</span><span class="sxs-lookup"><span data-stu-id="84788-103">Handle errors and exceptions in Azure Logic Apps</span></span>

<span data-ttu-id="84788-104">Aplikacje logiki platformy Azure udostępnia zaawansowane narzędzia i wzorce, aby upewnić się, że Twoje integracji są niezawodne i podatne na błędy.</span><span class="sxs-lookup"><span data-stu-id="84788-104">Azure Logic Apps provides rich tools and patterns to help you make sure your integrations are robust and resilient against failures.</span></span> <span data-ttu-id="84788-105">Wszelkie Architektura integracji stanowi wyzwanie, by odpowiednio obsłużyć przestoje lub problemów z systemów zależnych.</span><span class="sxs-lookup"><span data-stu-id="84788-105">Any integration architecture poses the challenge of making sure to appropriately handle downtime or issues from dependent systems.</span></span> <span data-ttu-id="84788-106">Logic Apps sprawia, że obsługa błędów najwyższej jakości środowisko, umożliwiając narzędzi, potrzebnych do działania na wyjątków i błędów w swoich przepływach pracy.</span><span class="sxs-lookup"><span data-stu-id="84788-106">Logic Apps makes handling errors a first-class experience, giving you the tools you need to act on exceptions and errors in your workflows.</span></span>

## <a name="retry-policies"></a><span data-ttu-id="84788-107">Spróbuj ponownie zasad</span><span class="sxs-lookup"><span data-stu-id="84788-107">Retry policies</span></span>

<span data-ttu-id="84788-108">Zasady ponawiania jest najbardziej podstawowy typ wyjątku i obsługa błędów.</span><span class="sxs-lookup"><span data-stu-id="84788-108">A retry policy is the most basic type of exception and error handling.</span></span> <span data-ttu-id="84788-109">Jeśli upłynął limit czasu żądania początkowego, lub nie powiodło się (każde żądanie, która powoduje 429 lub odpowiedź 5xx), ta zasada definiuje, czy akcja powinna ponowić.</span><span class="sxs-lookup"><span data-stu-id="84788-109">If an initial request timed out or failed (any request that results in a 429 or 5xx response), this policy defines whether the action should retry.</span></span> <span data-ttu-id="84788-110">Domyślnie wszystkie akcje próbę 4 razy dodatkowe za pośrednictwem 20 sekund.</span><span class="sxs-lookup"><span data-stu-id="84788-110">By default, all actions retry 4 additional times over 20-second intervals.</span></span> <span data-ttu-id="84788-111">Dlatego w przypadku pierwszego żądania odbiera `500 Internal Server Error` odpowiedzi, aparatu przepływu pracy wstrzymuje 20 sekund i próbuje ponownie żądanie.</span><span class="sxs-lookup"><span data-stu-id="84788-111">So if the first request receives a `500 Internal Server Error` response, the workflow engine pauses for 20 seconds, and attempts the request again.</span></span> <span data-ttu-id="84788-112">Jeśli po wszystkich próbach odpowiedzi jest nadal wyjątku lub błędu, przepływ pracy będzie kontynuowane i oznacza stanu akcji jako `Failed`.</span><span class="sxs-lookup"><span data-stu-id="84788-112">If after all retries, the response is still an exception or failure, the workflow continues and marks the action status as `Failed`.</span></span>

<span data-ttu-id="84788-113">Można skonfigurować zasady ponawiania w **dane wejściowe** dla określonej akcji.</span><span class="sxs-lookup"><span data-stu-id="84788-113">You can configure retry policies in the **inputs** for a particular action.</span></span> <span data-ttu-id="84788-114">Na przykład można skonfigurować zasady ponawiania próby maksymalnie 4 razy na 1 godzinę.</span><span class="sxs-lookup"><span data-stu-id="84788-114">For example, you can configure a retry policy to try as many as 4 times over 1-hour intervals.</span></span> <span data-ttu-id="84788-115">Aby uzyskać szczegółowe informacje o właściwościach wejściowego, zobacz [działania przepływu pracy i wyzwalaczy][retryPolicyMSDN].</span><span class="sxs-lookup"><span data-stu-id="84788-115">For full details about input properties, see [Workflow Actions and Triggers][retryPolicyMSDN].</span></span>

```json
"retryPolicy" : {
      "type": "<type-of-retry-policy>",
      "interval": <retry-interval>,
      "count": <number-of-retry-attempts>
    }
```

<span data-ttu-id="84788-116">Jeśli potrzebujesz Twoja Akcja HTTP, aby ponowić próbę 4 godziny i odczekaj 10 minut między kolejnymi próbami należy użyć następującej definicji:</span><span class="sxs-lookup"><span data-stu-id="84788-116">If you wanted your HTTP action to retry 4 times and wait 10 minutes between each attempt, you would use the following definition:</span></span>

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

<span data-ttu-id="84788-117">Aby uzyskać więcej informacji o obsługiwanych składni, zobacz [części zasady ponawiania akcji przepływu pracy i wyzwalaczy][retryPolicyMSDN].</span><span class="sxs-lookup"><span data-stu-id="84788-117">For more information on supported syntax, see the [retry-policy section in Workflow Actions and Triggers][retryPolicyMSDN].</span></span>

## <a name="catch-failures-with-the-runafter-property"></a><span data-ttu-id="84788-118">Błędy z właściwością RunAfter catch</span><span class="sxs-lookup"><span data-stu-id="84788-118">Catch failures with the RunAfter property</span></span>

<span data-ttu-id="84788-119">Każde działanie aplikacji logiki deklaruje akcje, które muszą zostać zakończone przed uruchomieniem akcji, takich jak kolejności kroków w przepływie pracy.</span><span class="sxs-lookup"><span data-stu-id="84788-119">Each logic app action declares which actions must finish before the action starts, like ordering the steps in your workflow.</span></span> <span data-ttu-id="84788-120">W definicji działania ta kolejność nosi nazwę `runAfter` właściwości.</span><span class="sxs-lookup"><span data-stu-id="84788-120">In the action definition, this ordering is known as the `runAfter` property.</span></span> <span data-ttu-id="84788-121">Ta właściwość jest obiekt, który opisuje, które akcje i Stany Akcja wykonania akcji.</span><span class="sxs-lookup"><span data-stu-id="84788-121">This property is an object that describes which actions and action statuses execute the action.</span></span> <span data-ttu-id="84788-122">Domyślnie wszystkie akcje dodane za pomocą projektanta aplikacji logiki są ustawione na `runAfter` poprzedniego kroku Jeśli poprzedni krok `Succeeded`.</span><span class="sxs-lookup"><span data-stu-id="84788-122">By default, all actions added through the Logic App Designer are set to `runAfter` the previous step if the previous step `Succeeded`.</span></span> <span data-ttu-id="84788-123">Można jednak dostosować tę wartość, aby zostać wywołane akcje podczas poprzedniej akcji ma `Failed`, `Skipped`, lub zestaw możliwych tych wartości.</span><span class="sxs-lookup"><span data-stu-id="84788-123">However, you can customize this value to fire actions when previous actions have `Failed`, `Skipped`, or a possible set of these values.</span></span> <span data-ttu-id="84788-124">Jeśli chcesz dodać element do wyznaczonych tematu usługi Service Bus po określonym działaniu `Insert_Row` nie powiedzie się, można użyć następującego `runAfter` konfiguracji:</span><span class="sxs-lookup"><span data-stu-id="84788-124">If you wanted to add an item to a designated Service Bus topic after a specific action `Insert_Row` fails, you could use the following `runAfter` configuration:</span></span>

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

<span data-ttu-id="84788-125">Powiadomienie `runAfter` wyzwalana, gdy właściwość ma wartość `Insert_Row` akcji jest `Failed`.</span><span class="sxs-lookup"><span data-stu-id="84788-125">Notice the `runAfter` property is set to fire if the `Insert_Row` action is `Failed`.</span></span> <span data-ttu-id="84788-126">Aby uruchomić akcję, gdy stan działania to `Succeeded`, `Failed`, lub `Skipped`, należy użyć następującej składni:</span><span class="sxs-lookup"><span data-stu-id="84788-126">To run the action if the action status is `Succeeded`, `Failed`, or `Skipped`, use this syntax:</span></span>

```json
"runAfter": {
        "Insert_Row": [
            "Failed", "Succeeded", "Skipped"
        ]
    }
```

> [!TIP]
> <span data-ttu-id="84788-127">Akcje, które są uruchomione i pomyślnie zakończone po poprzednim akcja nie powiodła się, są oznaczone jako `Succeeded`.</span><span class="sxs-lookup"><span data-stu-id="84788-127">Actions that run and complete successfully after a preceding action has failed, are marked as `Succeeded`.</span></span> <span data-ttu-id="84788-128">To zachowanie oznacza, że jeśli możesz pomyślnie catch wszystkich błędów w przepływie pracy, uruchom sam jest oznaczony jako `Succeeded`.</span><span class="sxs-lookup"><span data-stu-id="84788-128">This behavior means that if you successfully catch all failures in a workflow, the run itself is marked as `Succeeded`.</span></span>

## <a name="scopes-and-results-to-evaluate-actions"></a><span data-ttu-id="84788-129">Zakresy i wyniki oceny akcje</span><span class="sxs-lookup"><span data-stu-id="84788-129">Scopes and results to evaluate actions</span></span>

<span data-ttu-id="84788-130">Podobnie jak uruchamianie po poszczególnych działań można również pogrupować Akcje wewnątrz [zakres](../logic-apps/logic-apps-loops-and-scopes.md), działających jako logiczne grupowanie akcje.</span><span class="sxs-lookup"><span data-stu-id="84788-130">Similar to how you can run after individual actions, you can also group actions together inside a [scope](../logic-apps/logic-apps-loops-and-scopes.md), which act as a logical grouping of actions.</span></span> <span data-ttu-id="84788-131">Zakresy są przydatne, zarówno do organizowania akcji aplikacji logiki, jak i do wykonywania oceny Łączny stan zakresu.</span><span class="sxs-lookup"><span data-stu-id="84788-131">Scopes are useful both for organizing your logic app actions, and for performing aggregate evaluations on the status of a scope.</span></span> <span data-ttu-id="84788-132">Sam zakres przechodzi w stan po ukończeniu wszystkich działań w zakresie.</span><span class="sxs-lookup"><span data-stu-id="84788-132">The scope itself receives a status after all actions in a scope have finished.</span></span> <span data-ttu-id="84788-133">Stan zakresu jest określana z takich samych kryteriów jako Uruchom.</span><span class="sxs-lookup"><span data-stu-id="84788-133">The scope status is determined with the same criteria as a run.</span></span> <span data-ttu-id="84788-134">Po ostatnim akcji w gałęzi wykonywania `Failed` lub `Aborted`, stan jest `Failed`.</span><span class="sxs-lookup"><span data-stu-id="84788-134">If the final action in an execution branch is `Failed` or `Aborted`, the status is `Failed`.</span></span>

<span data-ttu-id="84788-135">Aby określonych akcji dla wszystkich błędów, które wystąpiły w zakresie, można użyć `runAfter` z zakresem, który jest oznaczony jako `Failed`.</span><span class="sxs-lookup"><span data-stu-id="84788-135">To fire specific actions for any failures that happened within the scope, you can use `runAfter` with a scope that is marked `Failed`.</span></span> <span data-ttu-id="84788-136">Jeśli *żadnych* akcje w zakresie zakończyć się niepowodzeniem, po zakresu zakończy się niepowodzeniem, umożliwia tworzenie jednej akcji, aby wykryć błędów.</span><span class="sxs-lookup"><span data-stu-id="84788-136">If *any* actions in the scope fail, running after a scope fails lets you create a single action to catch failures.</span></span>

### <a name="getting-the-context-of-failures-with-results"></a><span data-ttu-id="84788-137">Uzyskanie kontekstu błędów z wynikami</span><span class="sxs-lookup"><span data-stu-id="84788-137">Getting the context of failures with results</span></span>

<span data-ttu-id="84788-138">Mimo że przechwytywanie błędów z zakresu jest przydatne, będą również chcieli kontekście pomagające zrozumieć dokładnie akcje, które nie powiodło się, a jakiekolwiek błędy i kodów stanu, które zostały zwrócone.</span><span class="sxs-lookup"><span data-stu-id="84788-138">Although catching failures from a scope is useful, you might also want context to help you understand exactly which actions failed, and any errors or status codes that were returned.</span></span> <span data-ttu-id="84788-139">`@result()` Funkcji przepływu pracy zawierają kontekst o wyniku wszystkie akcje w zakresie.</span><span class="sxs-lookup"><span data-stu-id="84788-139">The `@result()` workflow function provides context about the result of all actions in a scope.</span></span>

<span data-ttu-id="84788-140">`@result()`przyjmuje jeden parametr, nazwa zakresu i zwraca tablicę wszystkich akcji wyników w tym zakresie.</span><span class="sxs-lookup"><span data-stu-id="84788-140">`@result()` takes a single parameter, scope name, and returns an array of all the action results from within that scope.</span></span> <span data-ttu-id="84788-141">Te obiekty działania obejmują takie same atrybuty jak `@actions()` generuje obiekt, w tym czas rozpoczęcia działania, czas zakończenia działania stanu akcji, dane wejściowe działań, identyfikatorów korelacji działania i akcji.</span><span class="sxs-lookup"><span data-stu-id="84788-141">These action objects include the same attributes as the `@actions()` object, including action start time, action end time, action status, action inputs, action correlation IDs, and action outputs.</span></span> <span data-ttu-id="84788-142">Aby wysłać kontekstu wszystkie akcje, które nie powiodło się w zakresie, można łatwo skojarzyć `@result()` działać z `runAfter`.</span><span class="sxs-lookup"><span data-stu-id="84788-142">To send context of any actions that failed within a scope, you can easily pair an `@result()` function with a `runAfter`.</span></span>

<span data-ttu-id="84788-143">Do wykonania akcji *dla każdego* akcji w zakresie który `Failed`, filtrować tablicy wyników z akcjami, których nie powiodła się, można skojarzyć `@result()` z  **[tablicy filtrów](../connectors/connectors-native-query.md)**  akcji i  **[ForEach](../logic-apps/logic-apps-loops-and-scopes.md)**  pętli.</span><span class="sxs-lookup"><span data-stu-id="84788-143">To execute an action *for each* action in a scope that `Failed`, filter the array of results to actions that failed, you can pair `@result()` with a **[Filter Array](../connectors/connectors-native-query.md)** action and a **[ForEach](../logic-apps/logic-apps-loops-and-scopes.md)** loop.</span></span> <span data-ttu-id="84788-144">Możesz pobrać tablicy filtrowane wyniki i wykonania czynności dla każdego błędu przy użyciu funkcji **ForEach** pętli.</span><span class="sxs-lookup"><span data-stu-id="84788-144">You can take the filtered result array and perform an action for each failure using the **ForEach** loop.</span></span> <span data-ttu-id="84788-145">Oto przykład, a następnie szczegółowy opis, który wysyła żądanie HTTP POST z treści odpowiedzi żadnych akcji, których nie powiodła się w zakresie `My_Scope`.</span><span class="sxs-lookup"><span data-stu-id="84788-145">Here's an example, followed by a detailed explanation, that sends an HTTP POST request with the response body of any actions that failed within the scope `My_Scope`.</span></span>

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

<span data-ttu-id="84788-146">Poniżej przedstawiono szczegółowy przewodnik opisujący, co się stanie:</span><span class="sxs-lookup"><span data-stu-id="84788-146">Here's a detailed walkthrough to describe what happens:</span></span>

1. <span data-ttu-id="84788-147">Aby uzyskać wynik wszystkich akcji w ramach `My_Scope`, **tablicy filtrów** filtry akcji `@result('My_Scope')`.</span><span class="sxs-lookup"><span data-stu-id="84788-147">To get the result of all actions within `My_Scope`, the **Filter Array** action filters `@result('My_Scope')`.</span></span>

2. <span data-ttu-id="84788-148">Warunek **tablicy filtrów** dowolnego `@result()` elementu, który znajduje się w stanie równa `Failed`.</span><span class="sxs-lookup"><span data-stu-id="84788-148">The condition for **Filter Array** is any `@result()` item that has status equal to `Failed`.</span></span> <span data-ttu-id="84788-149">Ten warunek filtruje tablicy o wszystkich wyników akcji z `My_Scope` do tablicy o tylko nie powiodło się wyniki akcji.</span><span class="sxs-lookup"><span data-stu-id="84788-149">This condition filters the array with all action results from `My_Scope` to an array with only failed action results.</span></span>

3. <span data-ttu-id="84788-150">Wykonaj **dla każdego** akcji **filtrowane tablicy** danych wyjściowych.</span><span class="sxs-lookup"><span data-stu-id="84788-150">Perform a **For Each** action on the **Filtered Array** outputs.</span></span> <span data-ttu-id="84788-151">Ten krok wykonuje akcję *dla każdego* nie powiodło się wynik akcji, która wcześniej została przefiltrowana.</span><span class="sxs-lookup"><span data-stu-id="84788-151">This step performs an action *for each* failed action result that was previously filtered.</span></span>

    <span data-ttu-id="84788-152">Jeśli nie jednej akcji w zakresie, akcje w `foreach` uruchomić tylko raz.</span><span class="sxs-lookup"><span data-stu-id="84788-152">If a single action in the scope failed, the actions in the `foreach` run only once.</span></span> 
    <span data-ttu-id="84788-153">Wiele zakończonych niepowodzeniem akcje mogą spowodować jedną akcję na błąd.</span><span class="sxs-lookup"><span data-stu-id="84788-153">Many failed actions cause one action per failure.</span></span>

4. <span data-ttu-id="84788-154">Wyślij HTTP POST `foreach` elementu treści odpowiedzi lub `@item()['outputs']['body']`.</span><span class="sxs-lookup"><span data-stu-id="84788-154">Send an HTTP POST on the `foreach` item response body, or `@item()['outputs']['body']`.</span></span> <span data-ttu-id="84788-155">`@result()` Kształt element jest taka sama jak `@actions()` kształtu i może być analizowana taki sam sposób.</span><span class="sxs-lookup"><span data-stu-id="84788-155">The `@result()` item shape is the same as the `@actions()` shape, and can be parsed the same way.</span></span>

5. <span data-ttu-id="84788-156">Obejmują dwa Nagłówki niestandardowe o nazwie nieudanych akcji `@item()['name']` i nieudane Uruchom klienta, identyfikator śledzenia `@item()['clientTrackingId']`.</span><span class="sxs-lookup"><span data-stu-id="84788-156">Include two custom headers with the failed action name `@item()['name']` and the failed run client tracking ID `@item()['clientTrackingId']`.</span></span>

<span data-ttu-id="84788-157">Odwołania, Oto przykład jedną `@result()` elementu przedstawiający `name`, `body`, i `clientTrackingId` właściwości, które są parsowane w poprzednim przykładzie.</span><span class="sxs-lookup"><span data-stu-id="84788-157">For reference, here's an example of a single `@result()` item, showing the `name`, `body`, and `clientTrackingId` properties that are parsed in the previous example.</span></span> <span data-ttu-id="84788-158">Poza `foreach`, `@result()` zwraca tablicę tych obiektów.</span><span class="sxs-lookup"><span data-stu-id="84788-158">Outside of a `foreach`, `@result()` returns an array of these objects.</span></span>

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

<span data-ttu-id="84788-159">Do wykonywania różnych wzorców w obsłudze wyjątków, używając wyrażenia przedstawione wcześniej.</span><span class="sxs-lookup"><span data-stu-id="84788-159">To perform different exception handling patterns, you can use the expressions shown previously.</span></span> <span data-ttu-id="84788-160">Może również wykonać pojedynczego wyjątków, Obsługa akcji poza zakres, który akceptuje całą macierz filtrowane awarii, a Usuń `foreach`.</span><span class="sxs-lookup"><span data-stu-id="84788-160">You might choose to execute a single exception handling action outside the scope that accepts the entire filtered array of failures, and remove the `foreach`.</span></span> <span data-ttu-id="84788-161">Możesz również uwzględnić inne przydatne właściwości z `@result()` odpowiedzi przedstawione wcześniej.</span><span class="sxs-lookup"><span data-stu-id="84788-161">You can also include other useful properties from the `@result()` response shown previously.</span></span>

## <a name="azure-diagnostics-and-telemetry"></a><span data-ttu-id="84788-162">Diagnostyka Azure i telemetrii</span><span class="sxs-lookup"><span data-stu-id="84788-162">Azure Diagnostics and telemetry</span></span>

<span data-ttu-id="84788-163">Te wzorce poprzedniej to doskonały sposób na Obsługa błędów i wyjątków w ramach Uruchom, ale można również zidentyfikować i odpowiadać na błędy, niezależnie od samego przebiegu.</span><span class="sxs-lookup"><span data-stu-id="84788-163">The previous patterns are great way to handle errors and exceptions within a run, but you can also identify and respond to errors independent of the run itself.</span></span> 
<span data-ttu-id="84788-164">[Diagnostyka Azure](../logic-apps/logic-apps-monitor-your-logic-apps.md) zapewnia prosty sposób wysyłania wszystkich zdarzeń przepływu pracy (w tym wszystkie stany akcji i uruchom) na konto magazynu Azure lub usługi Azure Event Hub.</span><span class="sxs-lookup"><span data-stu-id="84788-164">[Azure Diagnostics](../logic-apps/logic-apps-monitor-your-logic-apps.md) provides a simple way to send all workflow events (including all run and action statuses) to an Azure Storage account or an Azure Event Hub.</span></span> <span data-ttu-id="84788-165">Aby ocenić stany wykonywania, Monitoruj dzienniki i metryki lub publikować je do dowolnego narzędzia monitorowania preferowany.</span><span class="sxs-lookup"><span data-stu-id="84788-165">To evaluate run statuses, you can monitor the logs and metrics, or publish them into any monitoring tool you prefer.</span></span> <span data-ttu-id="84788-166">Jedną z opcji potencjalnych jest do strumienia wszystkie zdarzenia do Centrum zdarzeń Azure do [Stream Analytics](https://azure.microsoft.com/services/stream-analytics/).</span><span class="sxs-lookup"><span data-stu-id="84788-166">One potential option is to stream all the events through Azure Event Hub into [Stream Analytics](https://azure.microsoft.com/services/stream-analytics/).</span></span> <span data-ttu-id="84788-167">W Stream Analytics można zapisywać zapytania na żywo poza wszelkie nieprawidłowości, średnie lub błędy z dzienników diagnostycznych.</span><span class="sxs-lookup"><span data-stu-id="84788-167">In Stream Analytics, you can write live queries off any anomalies, averages, or failures from the diagnostic logs.</span></span> <span data-ttu-id="84788-168">Analiza strumienia może łatwo dane wyjściowe do innych źródeł danych, takich jak kolejki, tematy, SQL, bazy danych rozwiązania Cosmos Azure i usługi Power BI.</span><span class="sxs-lookup"><span data-stu-id="84788-168">Stream Analytics can easily output to other data sources like queues, topics, SQL, Azure Cosmos DB, and Power BI.</span></span>

## <a name="next-steps"></a><span data-ttu-id="84788-169">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="84788-169">Next Steps</span></span>

* [<span data-ttu-id="84788-170">Zobacz, jak klient tworzy błąd obsługi z usługi Azure Logic Apps</span><span class="sxs-lookup"><span data-stu-id="84788-170">See how a customer builds error handling with Azure Logic Apps</span></span>](../logic-apps/logic-apps-scenario-error-and-exception-handling.md)
* [<span data-ttu-id="84788-171">Znajdź więcej Logic Apps przykłady i scenariusze</span><span class="sxs-lookup"><span data-stu-id="84788-171">Find more Logic Apps examples and scenarios</span></span>](../logic-apps/logic-apps-examples-and-scenarios.md)
* [<span data-ttu-id="84788-172">Dowiedz się, jak utworzyć zautomatyzowanych wdrożeń dla aplikacji logiki</span><span class="sxs-lookup"><span data-stu-id="84788-172">Learn how to create automated deployments for logic apps</span></span>](../logic-apps/logic-apps-create-deploy-template.md)
* [<span data-ttu-id="84788-173">Tworzenie i wdrażanie aplikacji logiki w programie Visual Studio</span><span class="sxs-lookup"><span data-stu-id="84788-173">Build and deploy logic apps with Visual Studio</span></span>](logic-apps-deploy-from-vs.md)

<!-- References -->
[retryPolicyMSDN]: https://docs.microsoft.com/rest/api/logic/actions-and-triggers#Anchor_9
