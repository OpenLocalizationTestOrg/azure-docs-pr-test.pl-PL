---
title: "Akcje żądań i odpowiedzi | Dokumentacja firmy Microsoft"
description: "Omówienie wyzwalacza żądań i odpowiedzi i akcji w aplikacji logiki platformy Azure"
services: 
documentationcenter: 
author: jeffhollan
manager: erikre
editor: 
tags: connectors
ms.assetid: 566924a4-0988-4d86-9ecd-ad22507858c0
ms.service: logic-apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/18/2016
ms.author: jehollan
ms.openlocfilehash: e45b07d709927af64cfba28dfb0d8ee9cb8893b3
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-the-request-and-response-components"></a><span data-ttu-id="201ab-103">Rozpoczęcie pracy ze składnikami żądań i odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="201ab-103">Get started with the request and response components</span></span>
<span data-ttu-id="201ab-104">Ze składnikami żądań i odpowiedzi w aplikacji logiki możesz odpowiedzieć w czasie rzeczywistym na zdarzenia.</span><span class="sxs-lookup"><span data-stu-id="201ab-104">With the request and response components in a logic app, you can respond in real time to events.</span></span>

<span data-ttu-id="201ab-105">Można na przykład:</span><span class="sxs-lookup"><span data-stu-id="201ab-105">For example, you can:</span></span>

* <span data-ttu-id="201ab-106">Odpowiada na żądania HTTP z danymi z lokalną bazą danych za pośrednictwem aplikacji logiki.</span><span class="sxs-lookup"><span data-stu-id="201ab-106">Respond to an HTTP request with data from an on-premises database through a logic app.</span></span>
* <span data-ttu-id="201ab-107">Uruchomienie aplikacji logiki z zdarzenie zewnętrznego elementu webhook.</span><span class="sxs-lookup"><span data-stu-id="201ab-107">Trigger a logic app from an external webhook event.</span></span>
* <span data-ttu-id="201ab-108">Wywołania z akcją żądań i odpowiedzi z poziomu innej aplikacji logiki aplikacji logiki.</span><span class="sxs-lookup"><span data-stu-id="201ab-108">Call a logic app with a request and response action from within another logic app.</span></span>

<span data-ttu-id="201ab-109">Aby rozpocząć korzystanie z akcji żądań i odpowiedzi w aplikacji logiki, zobacz [tworzenie aplikacji logiki](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="201ab-109">To get started using the request and response actions in a logic app, see [Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

## <a name="use-the-http-request-trigger"></a><span data-ttu-id="201ab-110">Użyj wyzwalacza żądania HTTP</span><span class="sxs-lookup"><span data-stu-id="201ab-110">Use the HTTP Request trigger</span></span>
<span data-ttu-id="201ab-111">Wyzwalacz to zdarzenie służy do uruchomienia przepływu pracy, który jest zdefiniowany w aplikacji logiki.</span><span class="sxs-lookup"><span data-stu-id="201ab-111">A trigger is an event that can be used to start the workflow that is defined in a logic app.</span></span> <span data-ttu-id="201ab-112">[Dowiedz się więcej o wyzwalaczy](connectors-overview.md).</span><span class="sxs-lookup"><span data-stu-id="201ab-112">[Learn more about triggers](connectors-overview.md).</span></span>

<span data-ttu-id="201ab-113">Oto przykład sekwencji sposobu konfigurowania żądania HTTP w Projektancie aplikacji logiki.</span><span class="sxs-lookup"><span data-stu-id="201ab-113">Here’s an example sequence of how to set up an HTTP request in the Logic App Designer.</span></span>

1. <span data-ttu-id="201ab-114">Dodaj wyzwalacza **żądania - zostanie odebrane żądanie HTTP podczas** w aplikacji logiki.</span><span class="sxs-lookup"><span data-stu-id="201ab-114">Add the trigger **Request - When an HTTP request is received** in your logic app.</span></span> <span data-ttu-id="201ab-115">Opcjonalnie można podać schematu JSON (przy użyciu narzędzia, takiego jak [JSONSchema.net](http://jsonschema.net)) dla treści żądania.</span><span class="sxs-lookup"><span data-stu-id="201ab-115">You can optionally provide a JSON schema (by using a tool like [JSONSchema.net](http://jsonschema.net)) for the request body.</span></span> <span data-ttu-id="201ab-116">Dzięki temu projektanta, aby generować tokeny dla właściwości w żądaniu HTTP.</span><span class="sxs-lookup"><span data-stu-id="201ab-116">This allows the designer to generate tokens for properties in the HTTP request.</span></span>
2. <span data-ttu-id="201ab-117">Dodaj inną akcję, aby zapisać aplikacji logiki.</span><span class="sxs-lookup"><span data-stu-id="201ab-117">Add another action so that you can save the logic app.</span></span>
3. <span data-ttu-id="201ab-118">Po zapisaniu aplikację logiki, może uzyskać adres URL żądania HTTP z karty żądania.</span><span class="sxs-lookup"><span data-stu-id="201ab-118">After saving the logic app, you can get the HTTP request URL from the request card.</span></span>
4. <span data-ttu-id="201ab-119">HTTP POST (można użyć narzędzia, takiego jak [Postman](https://www.getpostman.com/)) do adresu URL wyzwala aplikacji logiki.</span><span class="sxs-lookup"><span data-stu-id="201ab-119">An HTTP POST (you can use a tool like [Postman](https://www.getpostman.com/)) to the URL triggers the logic app.</span></span>

> [!NOTE]
> <span data-ttu-id="201ab-120">Jeśli nie zdefiniowano akcję odpowiedzi `202 ACCEPTED` natychmiast zwrócił odpowiedź do obiektu wywołującego.</span><span class="sxs-lookup"><span data-stu-id="201ab-120">If you don't define a response action, a `202 ACCEPTED` response is immediately returned to the caller.</span></span> <span data-ttu-id="201ab-121">Akcja odpowiedzi służy do dostosowywania odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="201ab-121">You can use the response action to customize a response.</span></span>
> 
> 

![Wyzwalacz odpowiedzi](./media/connectors-native-reqres/using-trigger.png)

## <a name="use-the-http-response-action"></a><span data-ttu-id="201ab-123">Za pomocą akcji odpowiedzi HTTP</span><span class="sxs-lookup"><span data-stu-id="201ab-123">Use the HTTP Response action</span></span>
<span data-ttu-id="201ab-124">Akcja odpowiedzi HTTP jest prawidłowa tylko w przypadku, gdy jest używany w przepływie pracy, który jest wyzwalana przez żądanie HTTP.</span><span class="sxs-lookup"><span data-stu-id="201ab-124">The HTTP Response action is only valid when you use it in a workflow that is triggered by an HTTP request.</span></span> <span data-ttu-id="201ab-125">Jeśli nie zdefiniowano akcję odpowiedzi `202 ACCEPTED` natychmiast zwrócił odpowiedź do obiektu wywołującego.</span><span class="sxs-lookup"><span data-stu-id="201ab-125">If you don't define a response action, a `202 ACCEPTED` response is immediately returned to the caller.</span></span>  <span data-ttu-id="201ab-126">Można dodać akcję odpowiedzi na dowolnym etapie w przepływie pracy.</span><span class="sxs-lookup"><span data-stu-id="201ab-126">You can add a response action at any step within the workflow.</span></span> <span data-ttu-id="201ab-127">Aplikację logiki przechowuje tylko przychodzące żądanie otwarte przez jedną minutę na odpowiedź.</span><span class="sxs-lookup"><span data-stu-id="201ab-127">The logic app only keeps the incoming request open for one minute for a response.</span></span>  <span data-ttu-id="201ab-128">Po minucie, jeśli odpowiedź nie został wysłany z przepływu pracy (i istnieje akcja odpowiedzi w definicji) `504 GATEWAY TIMEOUT` jest zwracany do obiektu wywołującego.</span><span class="sxs-lookup"><span data-stu-id="201ab-128">After one minute, if no response was sent from the workflow (and a response action exists in the definition), a `504 GATEWAY TIMEOUT` is returned to the caller.</span></span>

<span data-ttu-id="201ab-129">Poniżej przedstawiono sposób dodawania akcji odpowiedzi HTTP:</span><span class="sxs-lookup"><span data-stu-id="201ab-129">Here's how to add an HTTP Response action:</span></span>

1. <span data-ttu-id="201ab-130">Wybierz **nowy krok** przycisku.</span><span class="sxs-lookup"><span data-stu-id="201ab-130">Select the **New Step** button.</span></span>
2. <span data-ttu-id="201ab-131">Wybierz **Dodaj akcję**.</span><span class="sxs-lookup"><span data-stu-id="201ab-131">Choose **Add an action**.</span></span>
3. <span data-ttu-id="201ab-132">W polu wyszukiwania akcji wpisz **odpowiedzi** Aby wyświetlić listę akcji odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="201ab-132">In the action search box, type **response** to list the Response action.</span></span>
   
    ![Wybierz akcję odpowiedzi](./media/connectors-native-reqres/using-action-1.png)
4. <span data-ttu-id="201ab-134">Dodaj w żadnych parametrów, które są wymagane dla komunikatu odpowiedzi HTTP.</span><span class="sxs-lookup"><span data-stu-id="201ab-134">Add in any parameters that are required for the HTTP response message.</span></span>
   
    ![Zakończenie akcji odpowiedzi](./media/connectors-native-reqres/using-action-2.png)
5. <span data-ttu-id="201ab-136">Kliknij w lewym górnym rogu paska narzędzi, aby zapisać i aplikacji logiki będzie Zapisz i opublikuj (Aktywuj).</span><span class="sxs-lookup"><span data-stu-id="201ab-136">Click the upper-left corner of the toolbar to save, and your logic app will both save and publish (activate).</span></span>

## <a name="request-trigger"></a><span data-ttu-id="201ab-137">Wyzwalacz żądania</span><span class="sxs-lookup"><span data-stu-id="201ab-137">Request trigger</span></span>
<span data-ttu-id="201ab-138">Poniżej przedstawiono szczegóły wyzwalacz, który obsługuje ten łącznik.</span><span class="sxs-lookup"><span data-stu-id="201ab-138">Here are the details for the trigger that this connector supports.</span></span> <span data-ttu-id="201ab-139">Brak wyzwalacz pojedyncze żądanie.</span><span class="sxs-lookup"><span data-stu-id="201ab-139">There is a single request trigger.</span></span>

| <span data-ttu-id="201ab-140">Wyzwalacz</span><span class="sxs-lookup"><span data-stu-id="201ab-140">Trigger</span></span> | <span data-ttu-id="201ab-141">Opis</span><span class="sxs-lookup"><span data-stu-id="201ab-141">Description</span></span> |
| --- | --- |
| <span data-ttu-id="201ab-142">Żądanie</span><span class="sxs-lookup"><span data-stu-id="201ab-142">Request</span></span> |<span data-ttu-id="201ab-143">Występuje, gdy zostanie odebrane żądanie HTTP</span><span class="sxs-lookup"><span data-stu-id="201ab-143">Occurs when an HTTP request is received</span></span> |

## <a name="response-action"></a><span data-ttu-id="201ab-144">Akcja odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="201ab-144">Response action</span></span>
<span data-ttu-id="201ab-145">Poniżej przedstawiono szczegóły akcję, która obsługuje ten łącznik.</span><span class="sxs-lookup"><span data-stu-id="201ab-145">Here are the details for the action that this connector supports.</span></span> <span data-ttu-id="201ab-146">Brak akcji pojedynczą odpowiedź, który można użyć tylko, gdy towarzyszy wyzwalacz żądania.</span><span class="sxs-lookup"><span data-stu-id="201ab-146">There is a single response action that can only be used when it is accompanied by a request trigger.</span></span>

| <span data-ttu-id="201ab-147">Akcja</span><span class="sxs-lookup"><span data-stu-id="201ab-147">Action</span></span> | <span data-ttu-id="201ab-148">Opis</span><span class="sxs-lookup"><span data-stu-id="201ab-148">Description</span></span> |
| --- | --- |
| <span data-ttu-id="201ab-149">Odpowiedź</span><span class="sxs-lookup"><span data-stu-id="201ab-149">Response</span></span> |<span data-ttu-id="201ab-150">Zwraca odpowiedź skorelowane żądanie HTTP</span><span class="sxs-lookup"><span data-stu-id="201ab-150">Returns a response to the correlated HTTP request</span></span> |

### <a name="trigger-and-action-details"></a><span data-ttu-id="201ab-151">Szczegóły TRIGGER i action</span><span class="sxs-lookup"><span data-stu-id="201ab-151">Trigger and action details</span></span>
<span data-ttu-id="201ab-152">W poniższych tabelach opisano pole wejściowe dla wyzwalacza i akcji, a odpowiednie szczegóły danych wyjściowych.</span><span class="sxs-lookup"><span data-stu-id="201ab-152">The following tables describe the input fields for the trigger and action, and the corresponding output details.</span></span>

#### <a name="request-trigger"></a><span data-ttu-id="201ab-153">Wyzwalacz żądania</span><span class="sxs-lookup"><span data-stu-id="201ab-153">Request trigger</span></span>
<span data-ttu-id="201ab-154">Poniżej znajduje się pole wejściowe dla wyzwalacza z przychodzącego żądania HTTP.</span><span class="sxs-lookup"><span data-stu-id="201ab-154">The following is an input field for the trigger from an incoming HTTP request.</span></span>

| <span data-ttu-id="201ab-155">Nazwa wyświetlana</span><span class="sxs-lookup"><span data-stu-id="201ab-155">Display name</span></span> | <span data-ttu-id="201ab-156">Nazwa właściwości</span><span class="sxs-lookup"><span data-stu-id="201ab-156">Property name</span></span> | <span data-ttu-id="201ab-157">Opis</span><span class="sxs-lookup"><span data-stu-id="201ab-157">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="201ab-158">Schematu JSON</span><span class="sxs-lookup"><span data-stu-id="201ab-158">JSON Schema</span></span> |<span data-ttu-id="201ab-159">Schemat</span><span class="sxs-lookup"><span data-stu-id="201ab-159">schema</span></span> |<span data-ttu-id="201ab-160">Schematu JSON w treści żądania HTTP</span><span class="sxs-lookup"><span data-stu-id="201ab-160">The JSON schema of the HTTP request body</span></span> |

<br>

<span data-ttu-id="201ab-161">**Szczegóły danych wyjściowych**</span><span class="sxs-lookup"><span data-stu-id="201ab-161">**Output details**</span></span>

<span data-ttu-id="201ab-162">Poniżej przedstawiono szczegóły danych wyjściowych dla żądania.</span><span class="sxs-lookup"><span data-stu-id="201ab-162">The following are output details for the request.</span></span>

| <span data-ttu-id="201ab-163">Nazwa właściwości</span><span class="sxs-lookup"><span data-stu-id="201ab-163">Property name</span></span> | <span data-ttu-id="201ab-164">Typ danych</span><span class="sxs-lookup"><span data-stu-id="201ab-164">Data type</span></span> | <span data-ttu-id="201ab-165">Opis</span><span class="sxs-lookup"><span data-stu-id="201ab-165">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="201ab-166">Nagłówki</span><span class="sxs-lookup"><span data-stu-id="201ab-166">Headers</span></span> |<span data-ttu-id="201ab-167">Obiekt</span><span class="sxs-lookup"><span data-stu-id="201ab-167">object</span></span> |<span data-ttu-id="201ab-168">Nagłówki żądania</span><span class="sxs-lookup"><span data-stu-id="201ab-168">Request headers</span></span> |
| <span data-ttu-id="201ab-169">Treść</span><span class="sxs-lookup"><span data-stu-id="201ab-169">Body</span></span> |<span data-ttu-id="201ab-170">Obiekt</span><span class="sxs-lookup"><span data-stu-id="201ab-170">object</span></span> |<span data-ttu-id="201ab-171">Obiekt żądania</span><span class="sxs-lookup"><span data-stu-id="201ab-171">Request object</span></span> |

#### <a name="response-action"></a><span data-ttu-id="201ab-172">Akcja odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="201ab-172">Response action</span></span>
<span data-ttu-id="201ab-173">Poniżej przedstawiono pól wejściowych dla akcji odpowiedzi HTTP.</span><span class="sxs-lookup"><span data-stu-id="201ab-173">The following are input fields for the HTTP Response action.</span></span> <span data-ttu-id="201ab-174">A * oznacza, że jest polem wymaganym.</span><span class="sxs-lookup"><span data-stu-id="201ab-174">A * means that it is a required field.</span></span>

| <span data-ttu-id="201ab-175">Nazwa wyświetlana</span><span class="sxs-lookup"><span data-stu-id="201ab-175">Display name</span></span> | <span data-ttu-id="201ab-176">Nazwa właściwości</span><span class="sxs-lookup"><span data-stu-id="201ab-176">Property name</span></span> | <span data-ttu-id="201ab-177">Opis</span><span class="sxs-lookup"><span data-stu-id="201ab-177">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="201ab-178">Kod stanu *</span><span class="sxs-lookup"><span data-stu-id="201ab-178">Status Code*</span></span> |<span data-ttu-id="201ab-179">statusCode</span><span class="sxs-lookup"><span data-stu-id="201ab-179">statusCode</span></span> |<span data-ttu-id="201ab-180">Kod stanu HTTP</span><span class="sxs-lookup"><span data-stu-id="201ab-180">The HTTP status code</span></span> |
| <span data-ttu-id="201ab-181">Nagłówki</span><span class="sxs-lookup"><span data-stu-id="201ab-181">Headers</span></span> |<span data-ttu-id="201ab-182">Nagłówki</span><span class="sxs-lookup"><span data-stu-id="201ab-182">headers</span></span> |<span data-ttu-id="201ab-183">Obiekt JSON nagłówków odpowiedzi do uwzględnienia</span><span class="sxs-lookup"><span data-stu-id="201ab-183">A JSON object of any response headers to include</span></span> |
| <span data-ttu-id="201ab-184">Treść</span><span class="sxs-lookup"><span data-stu-id="201ab-184">Body</span></span> |<span data-ttu-id="201ab-185">Treści</span><span class="sxs-lookup"><span data-stu-id="201ab-185">body</span></span> |<span data-ttu-id="201ab-186">Treść odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="201ab-186">The response body</span></span> |

## <a name="next-steps"></a><span data-ttu-id="201ab-187">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="201ab-187">Next steps</span></span>
<span data-ttu-id="201ab-188">Teraz, wypróbuj platformy i [tworzenie aplikacji logiki](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="201ab-188">Now, try out the platform and [create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span> <span data-ttu-id="201ab-189">Dostępne łączniki w aplikacjach logiki można eksplorować analizując naszych [listy interfejsów API](apis-list.md).</span><span class="sxs-lookup"><span data-stu-id="201ab-189">You can explore the other available connectors in logic apps by looking at our [APIs list](apis-list.md).</span></span>

