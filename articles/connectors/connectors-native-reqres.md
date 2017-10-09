---
title: "Akcje żądań i odpowiedzi aaaUse | Dokumentacja firmy Microsoft"
description: "Omówienie hello żądań i odpowiedzi trigger i action w aplikacji logiki platformy Azure"
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
ms.openlocfilehash: 24c378cc12d5f3f65116d5e59278236186a99662
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-request-and-response-components"></a><span data-ttu-id="b1969-103">Rozpoczęcie pracy ze składnikami hello żądań i odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="b1969-103">Get started with hello request and response components</span></span>
<span data-ttu-id="b1969-104">Składnikom hello żądań i odpowiedzi w aplikacji logiki może odpowiedzieć w czasie rzeczywistym tooevents.</span><span class="sxs-lookup"><span data-stu-id="b1969-104">With hello request and response components in a logic app, you can respond in real time tooevents.</span></span>

<span data-ttu-id="b1969-105">Można na przykład:</span><span class="sxs-lookup"><span data-stu-id="b1969-105">For example, you can:</span></span>

* <span data-ttu-id="b1969-106">Odpowiedz tooan żądania HTTP z danymi z lokalną bazą danych za pośrednictwem aplikacji logiki.</span><span class="sxs-lookup"><span data-stu-id="b1969-106">Respond tooan HTTP request with data from an on-premises database through a logic app.</span></span>
* <span data-ttu-id="b1969-107">Uruchomienie aplikacji logiki z zdarzenie zewnętrznego elementu webhook.</span><span class="sxs-lookup"><span data-stu-id="b1969-107">Trigger a logic app from an external webhook event.</span></span>
* <span data-ttu-id="b1969-108">Wywołania z akcją żądań i odpowiedzi z poziomu innej aplikacji logiki aplikacji logiki.</span><span class="sxs-lookup"><span data-stu-id="b1969-108">Call a logic app with a request and response action from within another logic app.</span></span>

<span data-ttu-id="b1969-109">tooget uruchomiony przy użyciu akcji hello żądań i odpowiedzi w aplikacji logiki, zobacz [tworzenie aplikacji logiki](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="b1969-109">tooget started using hello request and response actions in a logic app, see [Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

## <a name="use-hello-http-request-trigger"></a><span data-ttu-id="b1969-110">Użyj hello wyzwalacza żądania HTTP</span><span class="sxs-lookup"><span data-stu-id="b1969-110">Use hello HTTP Request trigger</span></span>
<span data-ttu-id="b1969-111">Wyzwalacz jest zdarzenie, które mogą być używane toostart przepływu pracy hello zdefiniowanej w aplikacji logiki.</span><span class="sxs-lookup"><span data-stu-id="b1969-111">A trigger is an event that can be used toostart hello workflow that is defined in a logic app.</span></span> <span data-ttu-id="b1969-112">[Dowiedz się więcej o wyzwalaczy](connectors-overview.md).</span><span class="sxs-lookup"><span data-stu-id="b1969-112">[Learn more about triggers](connectors-overview.md).</span></span>

<span data-ttu-id="b1969-113">Oto przykład sekwencji jak tooset się HTTP żądania w hello projektanta aplikacji logiki.</span><span class="sxs-lookup"><span data-stu-id="b1969-113">Here’s an example sequence of how tooset up an HTTP request in hello Logic App Designer.</span></span>

1. <span data-ttu-id="b1969-114">Dodaj wyzwalacza hello **żądania - zostanie odebrane żądanie HTTP podczas** w aplikacji logiki.</span><span class="sxs-lookup"><span data-stu-id="b1969-114">Add hello trigger **Request - When an HTTP request is received** in your logic app.</span></span> <span data-ttu-id="b1969-115">Opcjonalnie można podać schematu JSON (przy użyciu narzędzia, takiego jak [JSONSchema.net](http://jsonschema.net)) dla hello treści żądania.</span><span class="sxs-lookup"><span data-stu-id="b1969-115">You can optionally provide a JSON schema (by using a tool like [JSONSchema.net](http://jsonschema.net)) for hello request body.</span></span> <span data-ttu-id="b1969-116">Dzięki temu hello projektanta toogenerate tokeny dla właściwości w żądaniu hello HTTP.</span><span class="sxs-lookup"><span data-stu-id="b1969-116">This allows hello designer toogenerate tokens for properties in hello HTTP request.</span></span>
2. <span data-ttu-id="b1969-117">Dodaj inną akcję, dzięki czemu można zapisać hello aplikacji logiki.</span><span class="sxs-lookup"><span data-stu-id="b1969-117">Add another action so that you can save hello logic app.</span></span>
3. <span data-ttu-id="b1969-118">Po zapisaniu hello aplikacji logiki, może uzyskać adres URL żądania hello HTTP z hello żądania karty.</span><span class="sxs-lookup"><span data-stu-id="b1969-118">After saving hello logic app, you can get hello HTTP request URL from hello request card.</span></span>
4. <span data-ttu-id="b1969-119">HTTP POST (można użyć narzędzia, takiego jak [Postman](https://www.getpostman.com/)) toohello adres URL wyzwalaczy hello aplikacji logiki.</span><span class="sxs-lookup"><span data-stu-id="b1969-119">An HTTP POST (you can use a tool like [Postman](https://www.getpostman.com/)) toohello URL triggers hello logic app.</span></span>

> [!NOTE]
> <span data-ttu-id="b1969-120">Jeśli nie zdefiniowano akcję odpowiedzi `202 ACCEPTED` odpowiedzi jest zwracany natychmiast toohello wywołującego.</span><span class="sxs-lookup"><span data-stu-id="b1969-120">If you don't define a response action, a `202 ACCEPTED` response is immediately returned toohello caller.</span></span> <span data-ttu-id="b1969-121">Możesz użyć toocustomize akcji odpowiedzi hello odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="b1969-121">You can use hello response action toocustomize a response.</span></span>
> 
> 

![Wyzwalacz odpowiedzi](./media/connectors-native-reqres/using-trigger.png)

## <a name="use-hello-http-response-action"></a><span data-ttu-id="b1969-123">Użyj hello akcji odpowiedzi HTTP</span><span class="sxs-lookup"><span data-stu-id="b1969-123">Use hello HTTP Response action</span></span>
<span data-ttu-id="b1969-124">Hello akcji odpowiedzi HTTP jest prawidłowa tylko w przypadku, gdy jest używany w przepływie pracy, który jest wyzwalana przez żądanie HTTP.</span><span class="sxs-lookup"><span data-stu-id="b1969-124">hello HTTP Response action is only valid when you use it in a workflow that is triggered by an HTTP request.</span></span> <span data-ttu-id="b1969-125">Jeśli nie zdefiniowano akcję odpowiedzi `202 ACCEPTED` odpowiedzi jest zwracany natychmiast toohello wywołującego.</span><span class="sxs-lookup"><span data-stu-id="b1969-125">If you don't define a response action, a `202 ACCEPTED` response is immediately returned toohello caller.</span></span>  <span data-ttu-id="b1969-126">Można dodać akcję odpowiedzi na dowolnym etapie w przepływie pracy hello.</span><span class="sxs-lookup"><span data-stu-id="b1969-126">You can add a response action at any step within hello workflow.</span></span> <span data-ttu-id="b1969-127">aplikacji logiki Hello przechowuje tylko przychodzące żądanie hello otwarte przez jedną minutę na odpowiedź.</span><span class="sxs-lookup"><span data-stu-id="b1969-127">hello logic app only keeps hello incoming request open for one minute for a response.</span></span>  <span data-ttu-id="b1969-128">Po minucie, jeśli odpowiedź nie została wysłana z hello przepływu pracy (i istnieje akcja odpowiedzi w definicji hello) `504 GATEWAY TIMEOUT` jest zwracany toohello wywołującego.</span><span class="sxs-lookup"><span data-stu-id="b1969-128">After one minute, if no response was sent from hello workflow (and a response action exists in hello definition), a `504 GATEWAY TIMEOUT` is returned toohello caller.</span></span>

<span data-ttu-id="b1969-129">Oto jak tooadd akcji odpowiedzi HTTP:</span><span class="sxs-lookup"><span data-stu-id="b1969-129">Here's how tooadd an HTTP Response action:</span></span>

1. <span data-ttu-id="b1969-130">Wybierz hello **nowy krok** przycisku.</span><span class="sxs-lookup"><span data-stu-id="b1969-130">Select hello **New Step** button.</span></span>
2. <span data-ttu-id="b1969-131">Wybierz **Dodaj akcję**.</span><span class="sxs-lookup"><span data-stu-id="b1969-131">Choose **Add an action**.</span></span>
3. <span data-ttu-id="b1969-132">W polu wyszukiwania akcji hello wpisz **odpowiedzi** hello toolist akcji odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="b1969-132">In hello action search box, type **response** toolist hello Response action.</span></span>
   
    ![Wybierz akcję odpowiedzi hello](./media/connectors-native-reqres/using-action-1.png)
4. <span data-ttu-id="b1969-134">Dodaj w żadnych parametrów, które są wymagane dla komunikatu odpowiedzi HTTP hello.</span><span class="sxs-lookup"><span data-stu-id="b1969-134">Add in any parameters that are required for hello HTTP response message.</span></span>
   
    ![Zakończenie hello akcji odpowiedzi](./media/connectors-native-reqres/using-action-2.png)
5. <span data-ttu-id="b1969-136">Kliknij przycisk hello lewego górnego rogu hello toosave narzędzi i Twoje logiki aplikacji zapisze zarówno i publikowanie (Aktywuj).</span><span class="sxs-lookup"><span data-stu-id="b1969-136">Click hello upper-left corner of hello toolbar toosave, and your logic app will both save and publish (activate).</span></span>

## <a name="request-trigger"></a><span data-ttu-id="b1969-137">Wyzwalacz żądania</span><span class="sxs-lookup"><span data-stu-id="b1969-137">Request trigger</span></span>
<span data-ttu-id="b1969-138">Poniżej przedstawiono szczegóły hello hello wyzwalacz, który obsługuje ten łącznik.</span><span class="sxs-lookup"><span data-stu-id="b1969-138">Here are hello details for hello trigger that this connector supports.</span></span> <span data-ttu-id="b1969-139">Brak wyzwalacz pojedyncze żądanie.</span><span class="sxs-lookup"><span data-stu-id="b1969-139">There is a single request trigger.</span></span>

| <span data-ttu-id="b1969-140">Wyzwalacz</span><span class="sxs-lookup"><span data-stu-id="b1969-140">Trigger</span></span> | <span data-ttu-id="b1969-141">Opis</span><span class="sxs-lookup"><span data-stu-id="b1969-141">Description</span></span> |
| --- | --- |
| <span data-ttu-id="b1969-142">Żądanie</span><span class="sxs-lookup"><span data-stu-id="b1969-142">Request</span></span> |<span data-ttu-id="b1969-143">Występuje, gdy zostanie odebrane żądanie HTTP</span><span class="sxs-lookup"><span data-stu-id="b1969-143">Occurs when an HTTP request is received</span></span> |

## <a name="response-action"></a><span data-ttu-id="b1969-144">Akcja odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="b1969-144">Response action</span></span>
<span data-ttu-id="b1969-145">Poniżej przedstawiono szczegóły hello hello akcję, która obsługuje ten łącznik.</span><span class="sxs-lookup"><span data-stu-id="b1969-145">Here are hello details for hello action that this connector supports.</span></span> <span data-ttu-id="b1969-146">Brak akcji pojedynczą odpowiedź, który można użyć tylko, gdy towarzyszy wyzwalacz żądania.</span><span class="sxs-lookup"><span data-stu-id="b1969-146">There is a single response action that can only be used when it is accompanied by a request trigger.</span></span>

| <span data-ttu-id="b1969-147">Akcja</span><span class="sxs-lookup"><span data-stu-id="b1969-147">Action</span></span> | <span data-ttu-id="b1969-148">Opis</span><span class="sxs-lookup"><span data-stu-id="b1969-148">Description</span></span> |
| --- | --- |
| <span data-ttu-id="b1969-149">Odpowiedź</span><span class="sxs-lookup"><span data-stu-id="b1969-149">Response</span></span> |<span data-ttu-id="b1969-150">Zwraca toohello odpowiedzi skorelowane żądanie HTTP</span><span class="sxs-lookup"><span data-stu-id="b1969-150">Returns a response toohello correlated HTTP request</span></span> |

### <a name="trigger-and-action-details"></a><span data-ttu-id="b1969-151">Szczegóły TRIGGER i action</span><span class="sxs-lookup"><span data-stu-id="b1969-151">Trigger and action details</span></span>
<span data-ttu-id="b1969-152">Hello poniższych tabelach opisano hello pól wejściowych dla hello trigger i action i hello szczegóły danych wyjściowych.</span><span class="sxs-lookup"><span data-stu-id="b1969-152">hello following tables describe hello input fields for hello trigger and action, and hello corresponding output details.</span></span>

#### <a name="request-trigger"></a><span data-ttu-id="b1969-153">Wyzwalacz żądania</span><span class="sxs-lookup"><span data-stu-id="b1969-153">Request trigger</span></span>
<span data-ttu-id="b1969-154">Witaj poniżej znajduje się pole wejściowe dla wyzwalacza hello z przychodzącego żądania HTTP.</span><span class="sxs-lookup"><span data-stu-id="b1969-154">hello following is an input field for hello trigger from an incoming HTTP request.</span></span>

| <span data-ttu-id="b1969-155">Nazwa wyświetlana</span><span class="sxs-lookup"><span data-stu-id="b1969-155">Display name</span></span> | <span data-ttu-id="b1969-156">Nazwa właściwości</span><span class="sxs-lookup"><span data-stu-id="b1969-156">Property name</span></span> | <span data-ttu-id="b1969-157">Opis</span><span class="sxs-lookup"><span data-stu-id="b1969-157">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="b1969-158">Schematu JSON</span><span class="sxs-lookup"><span data-stu-id="b1969-158">JSON Schema</span></span> |<span data-ttu-id="b1969-159">Schemat</span><span class="sxs-lookup"><span data-stu-id="b1969-159">schema</span></span> |<span data-ttu-id="b1969-160">Witaj schematu JSON w treści żądania HTTP hello</span><span class="sxs-lookup"><span data-stu-id="b1969-160">hello JSON schema of hello HTTP request body</span></span> |

<br>

<span data-ttu-id="b1969-161">**Szczegóły danych wyjściowych**</span><span class="sxs-lookup"><span data-stu-id="b1969-161">**Output details**</span></span>

<span data-ttu-id="b1969-162">Witaj poniżej przedstawiono szczegóły danych wyjściowych hello żądania.</span><span class="sxs-lookup"><span data-stu-id="b1969-162">hello following are output details for hello request.</span></span>

| <span data-ttu-id="b1969-163">Nazwa właściwości</span><span class="sxs-lookup"><span data-stu-id="b1969-163">Property name</span></span> | <span data-ttu-id="b1969-164">Typ danych</span><span class="sxs-lookup"><span data-stu-id="b1969-164">Data type</span></span> | <span data-ttu-id="b1969-165">Opis</span><span class="sxs-lookup"><span data-stu-id="b1969-165">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="b1969-166">Nagłówki</span><span class="sxs-lookup"><span data-stu-id="b1969-166">Headers</span></span> |<span data-ttu-id="b1969-167">Obiekt</span><span class="sxs-lookup"><span data-stu-id="b1969-167">object</span></span> |<span data-ttu-id="b1969-168">Nagłówki żądania</span><span class="sxs-lookup"><span data-stu-id="b1969-168">Request headers</span></span> |
| <span data-ttu-id="b1969-169">Treść</span><span class="sxs-lookup"><span data-stu-id="b1969-169">Body</span></span> |<span data-ttu-id="b1969-170">Obiekt</span><span class="sxs-lookup"><span data-stu-id="b1969-170">object</span></span> |<span data-ttu-id="b1969-171">Obiekt żądania</span><span class="sxs-lookup"><span data-stu-id="b1969-171">Request object</span></span> |

#### <a name="response-action"></a><span data-ttu-id="b1969-172">Akcja odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="b1969-172">Response action</span></span>
<span data-ttu-id="b1969-173">Oto Hello pól wejściowych dla hello akcji odpowiedzi HTTP.</span><span class="sxs-lookup"><span data-stu-id="b1969-173">hello following are input fields for hello HTTP Response action.</span></span> <span data-ttu-id="b1969-174">A * oznacza, że jest polem wymaganym.</span><span class="sxs-lookup"><span data-stu-id="b1969-174">A * means that it is a required field.</span></span>

| <span data-ttu-id="b1969-175">Nazwa wyświetlana</span><span class="sxs-lookup"><span data-stu-id="b1969-175">Display name</span></span> | <span data-ttu-id="b1969-176">Nazwa właściwości</span><span class="sxs-lookup"><span data-stu-id="b1969-176">Property name</span></span> | <span data-ttu-id="b1969-177">Opis</span><span class="sxs-lookup"><span data-stu-id="b1969-177">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="b1969-178">Kod stanu *</span><span class="sxs-lookup"><span data-stu-id="b1969-178">Status Code*</span></span> |<span data-ttu-id="b1969-179">statusCode</span><span class="sxs-lookup"><span data-stu-id="b1969-179">statusCode</span></span> |<span data-ttu-id="b1969-180">Witaj kod stanu HTTP</span><span class="sxs-lookup"><span data-stu-id="b1969-180">hello HTTP status code</span></span> |
| <span data-ttu-id="b1969-181">Nagłówki</span><span class="sxs-lookup"><span data-stu-id="b1969-181">Headers</span></span> |<span data-ttu-id="b1969-182">Nagłówki</span><span class="sxs-lookup"><span data-stu-id="b1969-182">headers</span></span> |<span data-ttu-id="b1969-183">Obiekt JSON w dowolnym tooinclude nagłówki odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="b1969-183">A JSON object of any response headers tooinclude</span></span> |
| <span data-ttu-id="b1969-184">Treść</span><span class="sxs-lookup"><span data-stu-id="b1969-184">Body</span></span> |<span data-ttu-id="b1969-185">Treści</span><span class="sxs-lookup"><span data-stu-id="b1969-185">body</span></span> |<span data-ttu-id="b1969-186">treść odpowiedzi Hello</span><span class="sxs-lookup"><span data-stu-id="b1969-186">hello response body</span></span> |

## <a name="next-steps"></a><span data-ttu-id="b1969-187">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="b1969-187">Next steps</span></span>
<span data-ttu-id="b1969-188">Teraz, wypróbuj hello platformy i [tworzenie aplikacji logiki](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="b1969-188">Now, try out hello platform and [create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span> <span data-ttu-id="b1969-189">Można eksplorować hello innych dostępnych łączników w aplikacjach logiki analizując naszych [listy interfejsów API](apis-list.md).</span><span class="sxs-lookup"><span data-stu-id="b1969-189">You can explore hello other available connectors in logic apps by looking at our [APIs list](apis-list.md).</span></span>

