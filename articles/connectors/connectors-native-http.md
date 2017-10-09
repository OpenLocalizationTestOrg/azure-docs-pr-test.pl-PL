---
title: "aaaCommunicate z dowolnego punktu końcowego za pośrednictwem protokołu HTTP - Azure Logic Apps | Dokumentacja firmy Microsoft"
description: "Tworzenie aplikacji logiki, które mogą się komunikować z dowolnego punktu końcowego za pośrednictwem protokołu HTTP"
services: logic-apps
author: jeffhollan
manager: anneta
editor: 
documentationcenter: 
tags: connectors
ms.assetid: e11c6b4d-65a5-4d2d-8e13-38150db09c0b
ms.service: logic-apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/15/2016
ms.author: jehollan; LADocs
ms.openlocfilehash: 9793601839437a2b880bdb81e15881270cacc963
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-http-action"></a><span data-ttu-id="e041e-103">Rozpoczynanie pracy z hello akcji HTTP</span><span class="sxs-lookup"><span data-stu-id="e041e-103">Get started with hello HTTP action</span></span>

<span data-ttu-id="e041e-104">Hello akcji HTTP możesz rozszerzyć przepływy pracy dla Twojej organizacji i komunikacji tooany punktu końcowego za pośrednictwem protokołu HTTP.</span><span class="sxs-lookup"><span data-stu-id="e041e-104">With hello HTTP action, you can extend workflows for your organization and communicate tooany endpoint over HTTP.</span></span>

<span data-ttu-id="e041e-105">Możesz:</span><span class="sxs-lookup"><span data-stu-id="e041e-105">You can:</span></span>

* <span data-ttu-id="e041e-106">Tworzenie przepływów pracy aplikacji, które aktywować (wyzwalacz) witryny sieci Web, którą zarządzasz systemowi logiki.</span><span class="sxs-lookup"><span data-stu-id="e041e-106">Create logic app workflows that activate (trigger) when a website that you manage goes down.</span></span>
* <span data-ttu-id="e041e-107">Komunikacji tooany punktu końcowego za pośrednictwem protokołu HTTP tooextend przepływy pracy do innych usług.</span><span class="sxs-lookup"><span data-stu-id="e041e-107">Communicate tooany endpoint over HTTP tooextend your workflows into other services.</span></span>

<span data-ttu-id="e041e-108">tooget uruchomiony przy użyciu akcji hello HTTP w aplikacji logiki, zobacz [tworzenie aplikacji logiki](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="e041e-108">tooget started using hello HTTP action in a logic app, see [Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

## <a name="use-hello-http-trigger"></a><span data-ttu-id="e041e-109">Użyj wyzwalacza hello HTTP</span><span class="sxs-lookup"><span data-stu-id="e041e-109">Use hello HTTP trigger</span></span>
<span data-ttu-id="e041e-110">Wyzwalacz jest zdarzenie, które mogą być używane toostart przepływu pracy hello zdefiniowanej w aplikacji logiki.</span><span class="sxs-lookup"><span data-stu-id="e041e-110">A trigger is an event that can be used toostart hello workflow that is defined in a logic app.</span></span> <span data-ttu-id="e041e-111">[Dowiedz się więcej o wyzwalaczy](connectors-overview.md).</span><span class="sxs-lookup"><span data-stu-id="e041e-111">[Learn more about triggers](connectors-overview.md).</span></span>

<span data-ttu-id="e041e-112">Oto przykład sekwencji jak tooset się hello HTTP wyzwalacz w hello projektanta aplikacji logiki.</span><span class="sxs-lookup"><span data-stu-id="e041e-112">Here’s an example sequence of how tooset up hello HTTP trigger in hello Logic App Designer.</span></span>

1. <span data-ttu-id="e041e-113">Dodaj hello wyzwalacza HTTP w aplikacji logiki.</span><span class="sxs-lookup"><span data-stu-id="e041e-113">Add hello HTTP trigger in your logic app.</span></span>
2. <span data-ttu-id="e041e-114">Wypełnij hello parametry dla punktu końcowego hello HTTP, które mają toopoll.</span><span class="sxs-lookup"><span data-stu-id="e041e-114">Fill in hello parameters for hello HTTP endpoint that you want toopoll.</span></span>
3. <span data-ttu-id="e041e-115">Zmodyfikuj interwał cyklu hello na częstotliwości powinna sondowania.</span><span class="sxs-lookup"><span data-stu-id="e041e-115">Modify hello recurrence interval on how frequently it should poll.</span></span>

   <span data-ttu-id="e041e-116">Aplikacja logiki Hello teraz generowane z zawartość, która jest zwracana podczas każdego wyboru.</span><span class="sxs-lookup"><span data-stu-id="e041e-116">hello logic app now fires with any content that is returned during each check.</span></span>

   ![Wyzwalacz HTTP](./media/connectors-native-http/using-trigger.png)

### <a name="how-hello-http-trigger-works"></a><span data-ttu-id="e041e-118">Jak działa hello wyzwalacza HTTP</span><span class="sxs-lookup"><span data-stu-id="e041e-118">How hello HTTP trigger works</span></span>

<span data-ttu-id="e041e-119">wyzwalacza HTTP Hello wysyła punktu końcowego tooHTTP wywołania interwału powtarzania.</span><span class="sxs-lookup"><span data-stu-id="e041e-119">hello HTTP trigger sends a call tooHTTP endpoint on a recurring interval.</span></span> <span data-ttu-id="e041e-120">Domyślnie kodu odpowiedzi HTTP, który jest niższa niż 300 powoduje, że toorun aplikacji logiki.</span><span class="sxs-lookup"><span data-stu-id="e041e-120">By default, any HTTP response code that is lower than 300 causes a logic app toorun.</span></span> <span data-ttu-id="e041e-121">toospecify czy aplikacji logiki hello powinny wyzwalać, można edytować hello aplikacji logiki w widoku kodu i dodać warunek oceniający po hello wywołanie HTTP.</span><span class="sxs-lookup"><span data-stu-id="e041e-121">toospecify whether hello logic app should fire, you can edit hello logic app in code view, and add a condition that evaluates after hello HTTP call.</span></span> <span data-ttu-id="e041e-122">Oto przykład wyzwalacza HTTP, który generowane, gdy hello zwrócił kod stanu jest większa lub równa zbyt`400`.</span><span class="sxs-lookup"><span data-stu-id="e041e-122">Here's an example of an HTTP trigger that fires when hello returned status code is greater than or equal too`400`.</span></span>

```javascript
"Http":
{
    "conditions": [
        {
            "expression": "@greaterOrEquals(triggerOutputs()['statusCode'], 400)"
        }
    ],
    "inputs": {
        "method": "GET",
        "uri": "https://blogs.msdn.microsoft.com/logicapps/",
        "headers": {
            "accept-language": "en"
        }
    },
    "recurrence": {
        "frequency": "Second",
        "interval": 15
    },
    "type": "Http"
}
```

<span data-ttu-id="e041e-123">Szczegółowe informacje o parametrach wyzwalacza hello HTTP są dostępne na [MSDN](https://msdn.microsoft.com/library/azure/mt643939.aspx#HTTP-trigger).</span><span class="sxs-lookup"><span data-stu-id="e041e-123">Full details about hello HTTP trigger parameters are available on [MSDN](https://msdn.microsoft.com/library/azure/mt643939.aspx#HTTP-trigger).</span></span>

## <a name="use-hello-http-action"></a><span data-ttu-id="e041e-124">Za pomocą akcji hello HTTP</span><span class="sxs-lookup"><span data-stu-id="e041e-124">Use hello HTTP action</span></span>

<span data-ttu-id="e041e-125">Akcja jest operacja odbywa się przez hello przepływ pracy, który jest zdefiniowany w aplikacji logiki.</span><span class="sxs-lookup"><span data-stu-id="e041e-125">An action is an operation that is carried out by hello workflow that is defined in a logic app.</span></span> 
<span data-ttu-id="e041e-126">[Dowiedz się więcej o akcjach](connectors-overview.md).</span><span class="sxs-lookup"><span data-stu-id="e041e-126">[Learn more about actions](connectors-overview.md).</span></span>

1. <span data-ttu-id="e041e-127">Wybierz **nowy krok** > **Dodaj akcję**.</span><span class="sxs-lookup"><span data-stu-id="e041e-127">Choose **New Step** > **Add an action**.</span></span>
3. <span data-ttu-id="e041e-128">W polu wyszukiwania akcji hello wpisz **http** toolist hello HTTP akcji.</span><span class="sxs-lookup"><span data-stu-id="e041e-128">In hello action search box, type **http** toolist hello HTTP actions.</span></span>
   
    ![Wybierz akcję hello HTTP](./media/connectors-native-http/using-action-1.png)

4. <span data-ttu-id="e041e-130">Dodaj wszelkie wymagane parametry dla wywołania hello HTTP.</span><span class="sxs-lookup"><span data-stu-id="e041e-130">Add any required parameters for hello HTTP call.</span></span>
   
    ![Witaj pełną Akcja HTTP](./media/connectors-native-http/using-action-2.png)

5. <span data-ttu-id="e041e-132">Na pasku narzędzi Projektanta hello, kliknij przycisk **zapisać**.</span><span class="sxs-lookup"><span data-stu-id="e041e-132">On hello designer toolbar, click **Save**.</span></span> <span data-ttu-id="e041e-133">Aplikację logiki zostaną zapisane i opublikowane (aktywowanego) na powitania tym samym czasie.</span><span class="sxs-lookup"><span data-stu-id="e041e-133">Your logic app is saved and published (activated) at hello same time.</span></span>

## <a name="http-trigger"></a><span data-ttu-id="e041e-134">Wyzwalacz HTTP</span><span class="sxs-lookup"><span data-stu-id="e041e-134">HTTP trigger</span></span>
<span data-ttu-id="e041e-135">Poniżej przedstawiono szczegóły hello hello wyzwalacz, który obsługuje ten łącznik.</span><span class="sxs-lookup"><span data-stu-id="e041e-135">Here are hello details for hello trigger that this connector supports.</span></span> <span data-ttu-id="e041e-136">Łącznik HTTP Hello ma jeden wyzwalacz.</span><span class="sxs-lookup"><span data-stu-id="e041e-136">hello HTTP connector has one trigger.</span></span>

| <span data-ttu-id="e041e-137">Wyzwalacz</span><span class="sxs-lookup"><span data-stu-id="e041e-137">Trigger</span></span> | <span data-ttu-id="e041e-138">Opis</span><span class="sxs-lookup"><span data-stu-id="e041e-138">Description</span></span> |
| --- | --- |
| <span data-ttu-id="e041e-139">HTTP</span><span class="sxs-lookup"><span data-stu-id="e041e-139">HTTP</span></span> |<span data-ttu-id="e041e-140">Wykonuje wywołanie HTTP i zwraca hello zawartości odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="e041e-140">Makes an HTTP call and returns hello response content.</span></span> |

## <a name="http-action"></a><span data-ttu-id="e041e-141">Akcja HTTP</span><span class="sxs-lookup"><span data-stu-id="e041e-141">HTTP action</span></span>
<span data-ttu-id="e041e-142">Poniżej przedstawiono szczegóły hello hello akcję, która obsługuje ten łącznik.</span><span class="sxs-lookup"><span data-stu-id="e041e-142">Here are hello details for hello action that this connector supports.</span></span> <span data-ttu-id="e041e-143">Łącznik HTTP Hello ma jedną akcję możliwe.</span><span class="sxs-lookup"><span data-stu-id="e041e-143">hello HTTP connector has one possible action.</span></span>

| <span data-ttu-id="e041e-144">Akcja</span><span class="sxs-lookup"><span data-stu-id="e041e-144">Action</span></span> | <span data-ttu-id="e041e-145">Opis</span><span class="sxs-lookup"><span data-stu-id="e041e-145">Description</span></span> |
| --- | --- |
| <span data-ttu-id="e041e-146">HTTP</span><span class="sxs-lookup"><span data-stu-id="e041e-146">HTTP</span></span> |<span data-ttu-id="e041e-147">Wykonuje wywołanie HTTP i zwraca hello zawartości odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="e041e-147">Makes an HTTP call and returns hello response content.</span></span> |

## <a name="http-details"></a><span data-ttu-id="e041e-148">Szczegóły HTTP</span><span class="sxs-lookup"><span data-stu-id="e041e-148">HTTP details</span></span>
<span data-ttu-id="e041e-149">Witaj poniższych tabelach opisano hello wymagane i opcjonalne pola wejściowego dla akcji hello i hello odpowiednie dane wyjściowe szczegóły, które są skojarzone z przy użyciu akcji hello.</span><span class="sxs-lookup"><span data-stu-id="e041e-149">hello following tables describe hello required and optional input fields for hello action and hello corresponding output details that are associated with using hello action.</span></span>

#### <a name="http-request"></a><span data-ttu-id="e041e-150">Żądania HTTP</span><span class="sxs-lookup"><span data-stu-id="e041e-150">HTTP request</span></span>
<span data-ttu-id="e041e-151">Oto Hello pól wejściowych dla akcji hello, dzięki czemu żądania wychodzącego HTTP.</span><span class="sxs-lookup"><span data-stu-id="e041e-151">hello following are input fields for hello action, which makes an HTTP outbound request.</span></span>
<span data-ttu-id="e041e-152">A * oznacza, że jest polem wymaganym.</span><span class="sxs-lookup"><span data-stu-id="e041e-152">A * means that it is a required field.</span></span>

| <span data-ttu-id="e041e-153">Nazwa wyświetlana</span><span class="sxs-lookup"><span data-stu-id="e041e-153">Display name</span></span> | <span data-ttu-id="e041e-154">Nazwa właściwości</span><span class="sxs-lookup"><span data-stu-id="e041e-154">Property name</span></span> | <span data-ttu-id="e041e-155">Opis</span><span class="sxs-lookup"><span data-stu-id="e041e-155">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="e041e-156">Metoda *</span><span class="sxs-lookup"><span data-stu-id="e041e-156">Method*</span></span> |<span data-ttu-id="e041e-157">— Metoda</span><span class="sxs-lookup"><span data-stu-id="e041e-157">method</span></span> |<span data-ttu-id="e041e-158">toouse zlecenie Hello HTTP</span><span class="sxs-lookup"><span data-stu-id="e041e-158">hello HTTP verb toouse</span></span> |
| <span data-ttu-id="e041e-159">IDENTYFIKATOR URI *</span><span class="sxs-lookup"><span data-stu-id="e041e-159">URI*</span></span> |<span data-ttu-id="e041e-160">Identyfikator URI</span><span class="sxs-lookup"><span data-stu-id="e041e-160">uri</span></span> |<span data-ttu-id="e041e-161">Witaj identyfikatora URI dla żądania hello HTTP</span><span class="sxs-lookup"><span data-stu-id="e041e-161">hello URI for hello HTTP request</span></span> |
| <span data-ttu-id="e041e-162">Nagłówki</span><span class="sxs-lookup"><span data-stu-id="e041e-162">Headers</span></span> |<span data-ttu-id="e041e-163">Nagłówki</span><span class="sxs-lookup"><span data-stu-id="e041e-163">headers</span></span> |<span data-ttu-id="e041e-164">Obiekt JSON tooinclude nagłówki HTTP</span><span class="sxs-lookup"><span data-stu-id="e041e-164">A JSON object of HTTP headers tooinclude</span></span> |
| <span data-ttu-id="e041e-165">Treść</span><span class="sxs-lookup"><span data-stu-id="e041e-165">Body</span></span> |<span data-ttu-id="e041e-166">Treści</span><span class="sxs-lookup"><span data-stu-id="e041e-166">body</span></span> |<span data-ttu-id="e041e-167">Witaj treści żądania HTTP</span><span class="sxs-lookup"><span data-stu-id="e041e-167">hello HTTP request body</span></span> |
| <span data-ttu-id="e041e-168">Authentication</span><span class="sxs-lookup"><span data-stu-id="e041e-168">Authentication</span></span> |<span data-ttu-id="e041e-169">Uwierzytelnianie</span><span class="sxs-lookup"><span data-stu-id="e041e-169">authentication</span></span> |<span data-ttu-id="e041e-170">Szczegóły w hello [uwierzytelniania](#authentication) sekcji</span><span class="sxs-lookup"><span data-stu-id="e041e-170">Details in hello [Authentication](#authentication) section</span></span> |

<br>

#### <a name="output-details"></a><span data-ttu-id="e041e-171">Szczegóły danych wyjściowych</span><span class="sxs-lookup"><span data-stu-id="e041e-171">Output details</span></span>
<span data-ttu-id="e041e-172">Witaj poniżej przedstawiono szczegóły danych wyjściowych dla hello odpowiedzi HTTP.</span><span class="sxs-lookup"><span data-stu-id="e041e-172">hello following are output details for hello HTTP response.</span></span>

| <span data-ttu-id="e041e-173">Nazwa właściwości</span><span class="sxs-lookup"><span data-stu-id="e041e-173">Property name</span></span> | <span data-ttu-id="e041e-174">Typ danych</span><span class="sxs-lookup"><span data-stu-id="e041e-174">Data type</span></span> | <span data-ttu-id="e041e-175">Opis</span><span class="sxs-lookup"><span data-stu-id="e041e-175">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="e041e-176">Nagłówki</span><span class="sxs-lookup"><span data-stu-id="e041e-176">Headers</span></span> |<span data-ttu-id="e041e-177">Obiekt</span><span class="sxs-lookup"><span data-stu-id="e041e-177">object</span></span> |<span data-ttu-id="e041e-178">Nagłówki odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="e041e-178">Response headers</span></span> |
| <span data-ttu-id="e041e-179">Treść</span><span class="sxs-lookup"><span data-stu-id="e041e-179">Body</span></span> |<span data-ttu-id="e041e-180">Obiekt</span><span class="sxs-lookup"><span data-stu-id="e041e-180">object</span></span> |<span data-ttu-id="e041e-181">Obiekt odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="e041e-181">Response object</span></span> |
| <span data-ttu-id="e041e-182">Kod stanu</span><span class="sxs-lookup"><span data-stu-id="e041e-182">Status Code</span></span> |<span data-ttu-id="e041e-183">int</span><span class="sxs-lookup"><span data-stu-id="e041e-183">int</span></span> |<span data-ttu-id="e041e-184">Kod stanu HTTP</span><span class="sxs-lookup"><span data-stu-id="e041e-184">HTTP status code</span></span> |

## <a name="authentication"></a><span data-ttu-id="e041e-185">Authentication</span><span class="sxs-lookup"><span data-stu-id="e041e-185">Authentication</span></span>
<span data-ttu-id="e041e-186">Funkcja Logic Apps Hello pozwala toouse różnych typów uwierzytelniania względem punktów końcowych HTTP.</span><span class="sxs-lookup"><span data-stu-id="e041e-186">hello Logic Apps feature allows you toouse different types of authentication against HTTP endpoints.</span></span> <span data-ttu-id="e041e-187">Za pomocą tego uwierzytelnienia hello **HTTP**,  **[HTTP + Swagger](connectors-native-http-swagger.md)**, i  **[HTTP elementu Webhook](connectors-native-webhook.md)**  łączniki.</span><span class="sxs-lookup"><span data-stu-id="e041e-187">You can use this authentication with hello **HTTP**, **[HTTP + Swagger](connectors-native-http-swagger.md)**, and **[HTTP Webhook](connectors-native-webhook.md)** connectors.</span></span> <span data-ttu-id="e041e-188">następujące typy uwierzytelniania Hello są konfigurowane:</span><span class="sxs-lookup"><span data-stu-id="e041e-188">hello following types of authentication are configurable:</span></span>

* [<span data-ttu-id="e041e-189">Uwierzytelnianie podstawowe</span><span class="sxs-lookup"><span data-stu-id="e041e-189">Basic authentication</span></span>](#basic-authentication)
* [<span data-ttu-id="e041e-190">Uwierzytelnianie certyfikatu klienta</span><span class="sxs-lookup"><span data-stu-id="e041e-190">Client certificate authentication</span></span>](#client-certificate-authentication)
* [<span data-ttu-id="e041e-191">Azure uwierzytelniania OAuth usługi Active Directory (Azure AD)</span><span class="sxs-lookup"><span data-stu-id="e041e-191">Azure Active Directory (Azure AD) OAuth authentication</span></span>](#azure-active-directory-oauth-authentication)

#### <a name="basic-authentication"></a><span data-ttu-id="e041e-192">Uwierzytelnianie podstawowe</span><span class="sxs-lookup"><span data-stu-id="e041e-192">Basic authentication</span></span>

<span data-ttu-id="e041e-193">powitania po obiekt uwierzytelniania jest wymagany dla uwierzytelniania podstawowego.</span><span class="sxs-lookup"><span data-stu-id="e041e-193">hello following authentication object is needed for basic authentication.</span></span>
<span data-ttu-id="e041e-194">A * oznacza, że jest polem wymaganym.</span><span class="sxs-lookup"><span data-stu-id="e041e-194">A * means that it is a required field.</span></span>

| <span data-ttu-id="e041e-195">Nazwa właściwości</span><span class="sxs-lookup"><span data-stu-id="e041e-195">Property name</span></span> | <span data-ttu-id="e041e-196">Typ danych</span><span class="sxs-lookup"><span data-stu-id="e041e-196">Data type</span></span> | <span data-ttu-id="e041e-197">Opis</span><span class="sxs-lookup"><span data-stu-id="e041e-197">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="e041e-198">Typ *</span><span class="sxs-lookup"><span data-stu-id="e041e-198">Type*</span></span> |<span data-ttu-id="e041e-199">type</span><span class="sxs-lookup"><span data-stu-id="e041e-199">type</span></span> |<span data-ttu-id="e041e-200">Typ uwierzytelniania (musi być `Basic` dla uwierzytelniania podstawowego)</span><span class="sxs-lookup"><span data-stu-id="e041e-200">Type of authentication (must be `Basic` for basic authentication)</span></span> |
| <span data-ttu-id="e041e-201">Nazwa użytkownika *</span><span class="sxs-lookup"><span data-stu-id="e041e-201">Username*</span></span> |<span data-ttu-id="e041e-202">nazwa użytkownika</span><span class="sxs-lookup"><span data-stu-id="e041e-202">username</span></span> |<span data-ttu-id="e041e-203">Tooauthenticate nazwy użytkownika</span><span class="sxs-lookup"><span data-stu-id="e041e-203">User name tooauthenticate</span></span> |
| <span data-ttu-id="e041e-204">Hasło *</span><span class="sxs-lookup"><span data-stu-id="e041e-204">Password*</span></span> |<span data-ttu-id="e041e-205">hasło</span><span class="sxs-lookup"><span data-stu-id="e041e-205">password</span></span> |<span data-ttu-id="e041e-206">Tooauthenticate hasła</span><span class="sxs-lookup"><span data-stu-id="e041e-206">Password tooauthenticate</span></span> |

> [!TIP]
> <span data-ttu-id="e041e-207">Toouse hasła, gdy nie można pobrać z definicji hello, należy użyć `securestring` parametr i hello `@parameters()`  
>  [funkcji definicji przepływu pracy](http://aka.ms/logicappdocs).</span><span class="sxs-lookup"><span data-stu-id="e041e-207">If you want toouse a password that cannot be retrieved from hello definition, use a `securestring` parameter and hello `@parameters()` 
> [workflow definition function](http://aka.ms/logicappdocs).</span></span>

<span data-ttu-id="e041e-208">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="e041e-208">For example:</span></span>

```javascript
{
    "type": "Basic",
    "username": "user",
    "password": "test"
}
```

#### <a name="client-certificate-authentication"></a><span data-ttu-id="e041e-209">Uwierzytelnianie certyfikatów klientów</span><span class="sxs-lookup"><span data-stu-id="e041e-209">Client certificate authentication</span></span>

<span data-ttu-id="e041e-210">Witaj następujący obiekt uwierzytelniania jest potrzebne uwierzytelnianie certyfikatu klienta.</span><span class="sxs-lookup"><span data-stu-id="e041e-210">hello following authentication object is needed for client certificate authentication.</span></span> <span data-ttu-id="e041e-211">A * oznacza, że jest polem wymaganym.</span><span class="sxs-lookup"><span data-stu-id="e041e-211">A * means that it is a required field.</span></span>

| <span data-ttu-id="e041e-212">Nazwa właściwości</span><span class="sxs-lookup"><span data-stu-id="e041e-212">Property name</span></span> | <span data-ttu-id="e041e-213">Typ danych</span><span class="sxs-lookup"><span data-stu-id="e041e-213">Data type</span></span> | <span data-ttu-id="e041e-214">Opis</span><span class="sxs-lookup"><span data-stu-id="e041e-214">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="e041e-215">Typ *</span><span class="sxs-lookup"><span data-stu-id="e041e-215">Type*</span></span> |<span data-ttu-id="e041e-216">type</span><span class="sxs-lookup"><span data-stu-id="e041e-216">type</span></span> |<span data-ttu-id="e041e-217">Witaj typ uwierzytelniania (musi być `ClientCertificate` dla certyfikatów klienta SSL)</span><span class="sxs-lookup"><span data-stu-id="e041e-217">hello type of authentication (must be `ClientCertificate` for SSL client certificates)</span></span> |
| <span data-ttu-id="e041e-218">PFX *</span><span class="sxs-lookup"><span data-stu-id="e041e-218">PFX*</span></span> |<span data-ttu-id="e041e-219">PFX</span><span class="sxs-lookup"><span data-stu-id="e041e-219">pfx</span></span> |<span data-ttu-id="e041e-220">Witaj algorytmem Base64 zawartość pliku wymiany informacji osobistych (PFX) hello</span><span class="sxs-lookup"><span data-stu-id="e041e-220">hello Base64-encoded contents of hello Personal Information Exchange (PFX) file</span></span> |
| <span data-ttu-id="e041e-221">Hasło *</span><span class="sxs-lookup"><span data-stu-id="e041e-221">Password*</span></span> |<span data-ttu-id="e041e-222">hasło</span><span class="sxs-lookup"><span data-stu-id="e041e-222">password</span></span> |<span data-ttu-id="e041e-223">tooaccess hasło Hello hello pliku PFX</span><span class="sxs-lookup"><span data-stu-id="e041e-223">hello password tooaccess hello PFX file</span></span> |

> [!TIP]
> <span data-ttu-id="e041e-224">toouse parametr, który nie będzie można odczytać w definicji powitania po zapisaniu hello logikę aplikacji, można użyć `securestring` parametr i hello `@parameters()`  
>  [funkcji definicji przepływu pracy](http://aka.ms/logicappdocs).</span><span class="sxs-lookup"><span data-stu-id="e041e-224">toouse a parameter that won't be readable in hello definition after saving hello logic app, you can use a `securestring` parameter and hello `@parameters()` 
> [workflow definition function](http://aka.ms/logicappdocs).</span></span>

<span data-ttu-id="e041e-225">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="e041e-225">For example:</span></span>

```javascript
{
    "type": "ClientCertificate",
    "pfx": "aGVsbG8g...d29ybGQ=",
    "password": "@parameters('myPassword')"
}
```

#### <a name="azure-ad-oauth-authentication"></a><span data-ttu-id="e041e-226">Azure uwierzytelniania AD OAuth</span><span class="sxs-lookup"><span data-stu-id="e041e-226">Azure AD OAuth authentication</span></span>
<span data-ttu-id="e041e-227">powitania po obiekt uwierzytelniania jest wymagany dla uwierzytelniania usługi Azure AD OAuth.</span><span class="sxs-lookup"><span data-stu-id="e041e-227">hello following authentication object is needed for Azure AD OAuth authentication.</span></span> <span data-ttu-id="e041e-228">A * oznacza, że jest polem wymaganym.</span><span class="sxs-lookup"><span data-stu-id="e041e-228">A * means that it is a required field.</span></span>

| <span data-ttu-id="e041e-229">Nazwa właściwości</span><span class="sxs-lookup"><span data-stu-id="e041e-229">Property name</span></span> | <span data-ttu-id="e041e-230">Typ danych</span><span class="sxs-lookup"><span data-stu-id="e041e-230">Data type</span></span> | <span data-ttu-id="e041e-231">Opis</span><span class="sxs-lookup"><span data-stu-id="e041e-231">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="e041e-232">Typ *</span><span class="sxs-lookup"><span data-stu-id="e041e-232">Type*</span></span> |<span data-ttu-id="e041e-233">type</span><span class="sxs-lookup"><span data-stu-id="e041e-233">type</span></span> |<span data-ttu-id="e041e-234">Witaj typ uwierzytelniania (musi być `ActiveDirectoryOAuth` dla usługi Azure AD OAuth)</span><span class="sxs-lookup"><span data-stu-id="e041e-234">hello type of authentication (must be `ActiveDirectoryOAuth` for Azure AD OAuth)</span></span> |
| <span data-ttu-id="e041e-235">Dzierżawy *</span><span class="sxs-lookup"><span data-stu-id="e041e-235">Tenant*</span></span> |<span data-ttu-id="e041e-236">Dzierżawy</span><span class="sxs-lookup"><span data-stu-id="e041e-236">tenant</span></span> |<span data-ttu-id="e041e-237">Identyfikator dzierżawy Hello dzierżawy hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="e041e-237">hello tenant identifier for hello Azure AD tenant</span></span> |
| <span data-ttu-id="e041e-238">Grupy odbiorców *</span><span class="sxs-lookup"><span data-stu-id="e041e-238">Audience*</span></span> |<span data-ttu-id="e041e-239">grupy odbiorców</span><span class="sxs-lookup"><span data-stu-id="e041e-239">audience</span></span> |<span data-ttu-id="e041e-240">zasób Hello żądają toouse autoryzacji.</span><span class="sxs-lookup"><span data-stu-id="e041e-240">hello resource you are requesting authorization toouse.</span></span> <span data-ttu-id="e041e-241">Na przykład: `https://management.core.windows.net/`</span><span class="sxs-lookup"><span data-stu-id="e041e-241">For example: `https://management.core.windows.net/`</span></span> |
| <span data-ttu-id="e041e-242">Klient identyfikator *</span><span class="sxs-lookup"><span data-stu-id="e041e-242">Client ID*</span></span> |<span data-ttu-id="e041e-243">clientId</span><span class="sxs-lookup"><span data-stu-id="e041e-243">clientId</span></span> |<span data-ttu-id="e041e-244">Witaj identyfikator klienta aplikacji hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="e041e-244">hello client identifier for hello Azure AD application</span></span> |
| <span data-ttu-id="e041e-245">Klucz tajny *</span><span class="sxs-lookup"><span data-stu-id="e041e-245">Secret*</span></span> |<span data-ttu-id="e041e-246">klucz tajny</span><span class="sxs-lookup"><span data-stu-id="e041e-246">secret</span></span> |<span data-ttu-id="e041e-247">klucz tajny Hello powitania klienta, który żąda hello tokenu</span><span class="sxs-lookup"><span data-stu-id="e041e-247">hello secret of hello client that is requesting hello token</span></span> |

> [!TIP]
> <span data-ttu-id="e041e-248">Można użyć `securestring` parametr i hello `@parameters()` [funkcji definicji przepływu pracy](http://aka.ms/logicappdocs) toouse parametr, który nie będzie można odczytać w definicji powitania po zapisaniu.</span><span class="sxs-lookup"><span data-stu-id="e041e-248">You can use a `securestring` parameter and hello `@parameters()` [workflow definition function](http://aka.ms/logicappdocs) toouse a parameter that won't be readable in hello definition after saving.</span></span>
> 
> 

<span data-ttu-id="e041e-249">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="e041e-249">For example:</span></span>

```javascript
{
    "type": "ActiveDirectoryOAuth",
    "tenant": "72f988bf-86f1-41af-91ab-2d7cd011db47",
    "audience": "https://management.core.windows.net/",
    "clientId": "34750e0b-72d1-4e4f-bbbe-664f6d04d411",
    "secret": "hcqgkYc9ebgNLA5c+GDg7xl9ZJMD88TmTJiJBgZ8dFo="
}
```

## <a name="next-steps"></a><span data-ttu-id="e041e-250">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="e041e-250">Next steps</span></span>
<span data-ttu-id="e041e-251">Teraz, wypróbuj hello platformy i [tworzenie aplikacji logiki](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="e041e-251">Now, try out hello platform and [create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span> <span data-ttu-id="e041e-252">Można eksplorować hello innych dostępnych łączników w aplikacjach logiki analizując naszych [listy interfejsów API](apis-list.md).</span><span class="sxs-lookup"><span data-stu-id="e041e-252">You can explore hello other available connectors in Logic Apps by looking at our [APIs list](apis-list.md).</span></span>

