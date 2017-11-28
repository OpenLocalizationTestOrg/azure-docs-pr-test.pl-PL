---
title: "aaaCall, wyzwalacza lub zagnieździć przepływy pracy z punktów końcowych HTTP - Azure Logic Apps | Dokumentacja firmy Microsoft"
description: "Konfigurowanie toocall punktów końcowych HTTP, wyzwalacza lub zagnieżdżania przepływy pracy dla usługi Azure Logic Apps"
services: logic-apps
keywords: "przepływy pracy, punktów końcowych HTTP"
author: jeffhollan
manager: anneta
editor: 
documentationcenter: 
ms.assetid: 73ba2a70-03e9-4982-bfc8-ebfaad798bc2
ms.service: logic-apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.custom: H1Hack27Feb2017
ms.date: 03/31/2017
ms.author: LADocs; jehollan
ms.openlocfilehash: 072a314c3bff75ab7696f86bb063bb7c03c4ae89
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="call-trigger-or-nest-workflows-with-http-endpoints-in-logic-apps"></a><span data-ttu-id="162ce-104">Wywołaj wyzwalacz, lub zagnieżdżania przepływy pracy z punktów końcowych HTTP w aplikacji logiki</span><span class="sxs-lookup"><span data-stu-id="162ce-104">Call, trigger, or nest workflows with HTTP endpoints in logic apps</span></span>

<span data-ttu-id="162ce-105">Natywnie mogą uwidaczniać synchroniczne końcowych HTTP jako Wyzwalacze w aplikacji logiki, aby można wyzwolić lub wywołać aplikacje logiki przy użyciu adresu URL.</span><span class="sxs-lookup"><span data-stu-id="162ce-105">You can natively expose synchronous HTTP endpoints as triggers on logic apps so that you can trigger or call your logic apps through a URL.</span></span> <span data-ttu-id="162ce-106">Można zagnieżdżać przepływów pracy w aplikacjach logiki za pomocą wzorca można wywołać punktów końcowych.</span><span class="sxs-lookup"><span data-stu-id="162ce-106">You can also nest workflows in your logic apps by using a pattern of callable endpoints.</span></span>

<span data-ttu-id="162ce-107">punkty końcowe HTTP toocreate, można dodać te wyzwalacze, dzięki czemu aplikacje logiki może odbierać przychodzące żądania:</span><span class="sxs-lookup"><span data-stu-id="162ce-107">toocreate HTTP endpoints, you can add these triggers so that your logic apps can receive incoming requests:</span></span>

* [<span data-ttu-id="162ce-108">Żądanie</span><span class="sxs-lookup"><span data-stu-id="162ce-108">Request</span></span>](../connectors/connectors-native-reqres.md)

* [<span data-ttu-id="162ce-109">Element Webhook połączenia interfejsu API</span><span class="sxs-lookup"><span data-stu-id="162ce-109">API Connection Webhook</span></span>](logic-apps-workflow-actions-triggers.md#api-connection-trigger)

* [<span data-ttu-id="162ce-110">Element webhook protokołu HTTP</span><span class="sxs-lookup"><span data-stu-id="162ce-110">HTTP Webhook</span></span>](../connectors/connectors-native-webhook.md)

   > [!NOTE]
   > <span data-ttu-id="162ce-111">Mimo że nasze przykłady użycia hello **żądania** wyzwalacza, będzie można użyć dowolnego z hello na liście wyzwalaczy HTTP, a wszystkie zasady tak samo zastosować toohello inne typy wyzwalacza.</span><span class="sxs-lookup"><span data-stu-id="162ce-111">Although our examples use hello **Request** trigger, you can use any of hello listed HTTP triggers, and all principles identically apply toohello other trigger types.</span></span>

## <a name="set-up-an-http-endpoint-for-your-logic-app"></a><span data-ttu-id="162ce-112">Konfigurowanie punktu końcowego HTTP dla aplikacji logiki</span><span class="sxs-lookup"><span data-stu-id="162ce-112">Set up an HTTP endpoint for your logic app</span></span>

<span data-ttu-id="162ce-113">punkt końcowy HTTP toocreate dodać wyzwalacz, który może odbierać przychodzące żądania.</span><span class="sxs-lookup"><span data-stu-id="162ce-113">toocreate an HTTP endpoint, add a trigger that can receive incoming requests.</span></span>

1. <span data-ttu-id="162ce-114">Zaloguj się toohello [portalu Azure](https://portal.azure.com "portalu Azure").</span><span class="sxs-lookup"><span data-stu-id="162ce-114">Sign in toohello [Azure portal](https://portal.azure.com "Azure portal").</span></span> <span data-ttu-id="162ce-115">Przejdź do aplikacji logiki tooyour i otwórz projektanta aplikacji logiki.</span><span class="sxs-lookup"><span data-stu-id="162ce-115">Go tooyour logic app, and open Logic App Designer.</span></span>

2. <span data-ttu-id="162ce-116">Dodaj wyzwalacz, który umożliwia aplikacji logiki odbierania żądań przychodzących.</span><span class="sxs-lookup"><span data-stu-id="162ce-116">Add a trigger that lets your logic app receive incoming requests.</span></span> <span data-ttu-id="162ce-117">Na przykład dodać hello **żądania** aplikacji logiki tooyour wyzwalacza.</span><span class="sxs-lookup"><span data-stu-id="162ce-117">For example, add hello **Request** trigger tooyour logic app.</span></span>

3.  <span data-ttu-id="162ce-118">W obszarze **żądania schematu JSON treści**, można opcjonalnie wprowadzić schematu JSON dla ładunku hello (dane) spodziewać się hello tooreceive wyzwalacza.</span><span class="sxs-lookup"><span data-stu-id="162ce-118">Under **Request Body JSON Schema**, you can optionally enter a JSON schema for hello payload (data) that you expect hello trigger tooreceive.</span></span>

    <span data-ttu-id="162ce-119">Projektant Hello używa tego schematu do generowania tokenów, że aplikację logiki można użyć tooconsume, analizy i przekazywania danych z wyzwalacza hello przez przepływ pracy.</span><span class="sxs-lookup"><span data-stu-id="162ce-119">hello designer uses this schema for generating tokens that your logic app can use tooconsume, parse, and pass data from hello trigger through your workflow.</span></span> 
    <span data-ttu-id="162ce-120">Więcej informacji o [tokeny generowane na podstawie schematów JSON](#generated-tokens).</span><span class="sxs-lookup"><span data-stu-id="162ce-120">More about [tokens generated from JSON schemas](#generated-tokens).</span></span>

    <span data-ttu-id="162ce-121">Na przykład wprowadź schematu hello wyświetlany w Projektancie hello:</span><span class="sxs-lookup"><span data-stu-id="162ce-121">For this example, enter hello schema shown in hello designer:</span></span>

    ```json
    {
      "type": "object",
      "properties": {
        "address": {
          "type": "string"
        }
      },
      "required": [
        "address"
      ]
    }
    ```

    ![Dodaj akcję żądania hello][1]

    > [!TIP]
    > 
    > <span data-ttu-id="162ce-123">Schemat przykładowy ładunek JSON można generować za pomocą narzędzia, takie jak [jsonschema.net](http://jsonschema.net/), lub w hello **żądania** wyzwalacza, wybierając **Użyj przykładowy ładunek toogenerate schematu**.</span><span class="sxs-lookup"><span data-stu-id="162ce-123">You can generate a schema for a sample JSON payload from a tool like [jsonschema.net](http://jsonschema.net/), or in hello **Request** trigger by choosing **Use sample payload toogenerate schema**.</span></span> 
    > <span data-ttu-id="162ce-124">Wprowadź przykładowy ładunek, a następnie wybierz pozycję **gotowe**.</span><span class="sxs-lookup"><span data-stu-id="162ce-124">Enter your sample payload, and choose **Done**.</span></span>

    <span data-ttu-id="162ce-125">Na przykład ten przykładowy ładunek:</span><span class="sxs-lookup"><span data-stu-id="162ce-125">For example, this sample payload:</span></span>

    ```json
    {
       "address": "21 2nd Street, New York, New York"
    }
    ```

    <span data-ttu-id="162ce-126">generuje ten schemat:</span><span class="sxs-lookup"><span data-stu-id="162ce-126">generates this schema:</span></span>

    ```json
    }
       "type": "object",
       "properties": {
          "address": {
             "type": "string" 
          }
       }
    }
    ```

4.  <span data-ttu-id="162ce-127">Zapisz aplikację logiki.</span><span class="sxs-lookup"><span data-stu-id="162ce-127">Save your logic app.</span></span> <span data-ttu-id="162ce-128">W obszarze **HTTP POST toothis URL**, powinna być teraz widoczna wygenerowanego wywołania zwrotnego adresu URL, tak jak ten przykład:</span><span class="sxs-lookup"><span data-stu-id="162ce-128">Under **HTTP POST toothis URL**, you should now find a generated callback URL, like this example:</span></span>

    ![Wywołanie zwrotne wygenerowany adres URL punktu końcowego](./media/logic-apps-http-endpoint/generated-endpoint-url.png)

    <span data-ttu-id="162ce-130">Ten adres URL zawiera klucz dostępu sygnatury dostępu Współdzielonego w hello parametry zapytania, które są używane do uwierzytelniania.</span><span class="sxs-lookup"><span data-stu-id="162ce-130">This URL contains a Shared Access Signature (SAS) key in hello query parameters that are used for authentication.</span></span> 
    <span data-ttu-id="162ce-131">Można również uzyskać adres URL punktu końcowego HTTP hello z Twojej Omówienie aplikacji logiki w hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="162ce-131">You can also get hello HTTP endpoint URL from your logic app overview in hello Azure portal.</span></span> <span data-ttu-id="162ce-132">W obszarze **historii wyzwalacza**, wybierz wyzwalacz:</span><span class="sxs-lookup"><span data-stu-id="162ce-132">Under **Trigger History**, select your trigger:</span></span>

    ![Adres URL punktu końcowego HTTP GET z portalu Azure][2]

    <span data-ttu-id="162ce-134">Można także uzyskać adres URL hello za sprawą tego wywołania:</span><span class="sxs-lookup"><span data-stu-id="162ce-134">Or you can get hello URL by making this call:</span></span>

    ```
    POST https://management.azure.com/{logic-app-resourceID}/triggers/{myendpointtrigger}/listCallbackURL?api-version=2016-06-01
    ```

## <a name="change-hello-http-method-for-your-trigger"></a><span data-ttu-id="162ce-135">Zmień metodę HTTP hello wyzwalacza</span><span class="sxs-lookup"><span data-stu-id="162ce-135">Change hello HTTP method for your trigger</span></span>

<span data-ttu-id="162ce-136">Domyślnie program hello **żądania** wyzwalacza oczekuje żądania HTTP POST, ale można użyć innej metody HTTP.</span><span class="sxs-lookup"><span data-stu-id="162ce-136">By default, hello **Request** trigger expects an HTTP POST request, but you can use a different HTTP method.</span></span> 

> [!NOTE]
> <span data-ttu-id="162ce-137">Można określić tylko jedną metodę typu.</span><span class="sxs-lookup"><span data-stu-id="162ce-137">You can specify only one method type.</span></span>

1. <span data-ttu-id="162ce-138">W Twojej **żądania** wyzwalania, wybierz **Pokaż zaawansowane opcje**.</span><span class="sxs-lookup"><span data-stu-id="162ce-138">On your **Request** trigger, choose **Show advanced options**.</span></span>

2. <span data-ttu-id="162ce-139">Otwórz hello **metody** listy.</span><span class="sxs-lookup"><span data-stu-id="162ce-139">Open hello **Method** list.</span></span> <span data-ttu-id="162ce-140">Na przykład wybierz **UZYSKAĆ** tak, aby można było testować punkt końcowy HTTP URL później.</span><span class="sxs-lookup"><span data-stu-id="162ce-140">For this example, select **GET** so that you can test your HTTP endpoint's URL later.</span></span>

    > [!NOTE]
    > <span data-ttu-id="162ce-141">Wybierz inne metody HTTP lub określić metodę niestandardowych aplikacji logiki.</span><span class="sxs-lookup"><span data-stu-id="162ce-141">You can select any other HTTP method, or specify a custom method for your own logic app.</span></span>

    ![Zmień metodę HTTP](./media/logic-apps-http-endpoint/change-method.png)

## <a name="accept-parameters-through-your-http-endpoint-url"></a><span data-ttu-id="162ce-143">Akceptować parametry przez adres URL punktu końcowego HTTP</span><span class="sxs-lookup"><span data-stu-id="162ce-143">Accept parameters through your HTTP endpoint URL</span></span>

<span data-ttu-id="162ce-144">Parametry tooaccept adres URL punktu końcowego HTTP, należy dostosować ścieżkę względną do tego wyzwalacza.</span><span class="sxs-lookup"><span data-stu-id="162ce-144">When you want your HTTP endpoint URL tooaccept parameters, customize your trigger's relative path.</span></span>

1. <span data-ttu-id="162ce-145">W Twojej **żądania** wyzwalania, wybierz **Pokaż zaawansowane opcje**.</span><span class="sxs-lookup"><span data-stu-id="162ce-145">On your **Request** trigger, choose **Show advanced options**.</span></span> 

2. <span data-ttu-id="162ce-146">W obszarze **metody**, określ metodę hello HTTP, które mają toouse Twojego żądania.</span><span class="sxs-lookup"><span data-stu-id="162ce-146">Under **Method**, specify hello HTTP method that you want your request toouse.</span></span> <span data-ttu-id="162ce-147">Na przykład wybierz hello **UZYSKAĆ** metody, jeśli nie jest jeszcze, dzięki czemu można sprawdzić adres URL punkt końcowy HTTP.</span><span class="sxs-lookup"><span data-stu-id="162ce-147">For this example, select hello **GET** method, if you haven't already, so that you can test your HTTP endpoint's URL.</span></span>

      > [!NOTE]
      > <span data-ttu-id="162ce-148">Po określeniu ścieżki względnej wyzwalacza metody HTTP należy również jawnie określić wyzwalacza.</span><span class="sxs-lookup"><span data-stu-id="162ce-148">When you specify a relative path for your trigger, you must also explicitly specify an HTTP method for your trigger.</span></span>

3. <span data-ttu-id="162ce-149">W obszarze **ścieżki względnej**, określ ścieżkę względną hello parametru hello adres URL powinien akceptują, na przykład `customers/{customerID}`.</span><span class="sxs-lookup"><span data-stu-id="162ce-149">Under **Relative path**, specify hello relative path for hello parameter that your URL should accept, for example, `customers/{customerID}`.</span></span>

    ![Określ metodę HTTP hello i ścieżka względna dla parametru](./media/logic-apps-http-endpoint/relativeurl.png)

4. <span data-ttu-id="162ce-151">toouse hello parametr, Dodaj **odpowiedzi** aplikacji logiki tooyour akcji.</span><span class="sxs-lookup"><span data-stu-id="162ce-151">toouse hello parameter, add a **Response** action tooyour logic app.</span></span> <span data-ttu-id="162ce-152">(W obszarze wyzwalacz, wybierz **nowy krok** > **Dodaj akcję** > **odpowiedzi**)</span><span class="sxs-lookup"><span data-stu-id="162ce-152">(Under your trigger, choose **New step** > **Add an action** > **Response**)</span></span> 

5. <span data-ttu-id="162ce-153">Do odpowiedzi **treści**, obejmuje hello tokenu dla parametru hello, określonej ścieżki względnej do tego wyzwalacza.</span><span class="sxs-lookup"><span data-stu-id="162ce-153">In your response's **Body**, include hello token for hello parameter that you specified in your trigger's relative path.</span></span>

    <span data-ttu-id="162ce-154">Na przykład tooreturn `Hello {customerID}`, aktualizacja do odpowiedzi **treści** z `Hello {customerID token}`.</span><span class="sxs-lookup"><span data-stu-id="162ce-154">For example, tooreturn `Hello {customerID}`, update your response's **Body** with `Hello {customerID token}`.</span></span> 
    <span data-ttu-id="162ce-155">listy zawartości dynamicznej Hello powinna występować i Pokaż hello `customerID` tokenu dla tooselect użytkownik.</span><span class="sxs-lookup"><span data-stu-id="162ce-155">hello dynamic content list should appear and show hello `customerID` token for you tooselect.</span></span>

    ![Dodaj parametr tooresponse treści](./media/logic-apps-http-endpoint/relativeurlresponse.png)

    <span data-ttu-id="162ce-157">Twoje **treści** powinna wyglądać następująco:</span><span class="sxs-lookup"><span data-stu-id="162ce-157">Your **Body** should look like this example:</span></span>

    ![Treść odpowiedzi z parametrem](./media/logic-apps-http-endpoint/relative-url-with-parameter.png)

6. <span data-ttu-id="162ce-159">Zapisz aplikację logiki.</span><span class="sxs-lookup"><span data-stu-id="162ce-159">Save your logic app.</span></span> 

    <span data-ttu-id="162ce-160">Adres URL punktu końcowego HTTP zawiera teraz hello ścieżki względnej, na przykład:</span><span class="sxs-lookup"><span data-stu-id="162ce-160">Your HTTP endpoint URL now includes hello relative path, for example:</span></span> 

    <span data-ttu-id="162ce-161">HTTPS & # 58;//prod-00.southcentralus.logic.azure.com/workflows/f90cb66c52ea4e9cabe0abf4e197deff/triggers/manual/paths/invoke/customers/{customerID}...</span><span class="sxs-lookup"><span data-stu-id="162ce-161">https&#58;//prod-00.southcentralus.logic.azure.com/workflows/f90cb66c52ea4e9cabe0abf4e197deff/triggers/manual/paths/invoke/customers/{customerID}...</span></span>

7. <span data-ttu-id="162ce-162">tootest Twojego punkt końcowy HTTP, kopiowania i wklejania hello zaktualizowane adres URL w innym oknie przeglądarki, ale zastępuje `{customerID}` z `123456`, i naciśnij klawisz Enter.</span><span class="sxs-lookup"><span data-stu-id="162ce-162">tootest your HTTP endpoint, copy and paste hello updated URL into another browser window, but replace `{customerID}` with `123456`, and press Enter.</span></span>

    <span data-ttu-id="162ce-163">Ten tekst powinien być wyświetlony w przeglądarce:</span><span class="sxs-lookup"><span data-stu-id="162ce-163">Your browser should show this text:</span></span> 

    `Hello 123456`

<a name="generated-tokens"></a>
### <a name="tokens-generated-from-json-schemas-for-your-logic-app"></a><span data-ttu-id="162ce-164">Tokeny generowane na podstawie schematów JSON aplikacji logiki</span><span class="sxs-lookup"><span data-stu-id="162ce-164">Tokens generated from JSON schemas for your logic app</span></span>

<span data-ttu-id="162ce-165">Jeśli podasz schematu JSON w Twojej **żądania** Wyzwól program hello projektanta aplikacji logiki generuje tokeny na potrzeby właściwości w tym schemacie.</span><span class="sxs-lookup"><span data-stu-id="162ce-165">When you provide a JSON schema in your **Request** trigger, hello Logic App Designer generates tokens for properties in that schema.</span></span> <span data-ttu-id="162ce-166">Można następnie użyć tych tokenów przekazywania danych za pomocą przepływu pracy aplikacji logiki.</span><span class="sxs-lookup"><span data-stu-id="162ce-166">You can then use those tokens for passing data through your logic app workflow.</span></span>

<span data-ttu-id="162ce-167">Na przykład, jeśli dodasz hello `title` i `name` właściwości tooyour schematu JSON, tokenów są teraz dostępne toouse w kolejnych krokach przepływu pracy.</span><span class="sxs-lookup"><span data-stu-id="162ce-167">For this example, if you add hello `title` and `name` properties tooyour JSON schema, their tokens are now available toouse in later workflow steps.</span></span> 

<span data-ttu-id="162ce-168">Oto hello pełną schematu JSON:</span><span class="sxs-lookup"><span data-stu-id="162ce-168">Here is hello complete JSON schema:</span></span>

```json
{
   "type": "object",
   "properties": {
      "address": {
         "type": "string"
      },
      "title": {
         "type": "string"
      },
      "name": {
         "type": "string"
      }
   },
   "required": [
      "address",
      "title",
      "name"
   ]
}
```

## <a name="create-nested-workflows-for-logic-apps"></a><span data-ttu-id="162ce-169">Utwórz zagnieżdżone przepływy pracy dla usługi logic apps</span><span class="sxs-lookup"><span data-stu-id="162ce-169">Create nested workflows for logic apps</span></span>

<span data-ttu-id="162ce-170">Przepływy pracy można zagnieździć w aplikacji logiki przez dodanie innych aplikacji logiki, które mogą odbierać żądań.</span><span class="sxs-lookup"><span data-stu-id="162ce-170">You can nest workflows in your logic app by adding other logic apps that can receive requests.</span></span> <span data-ttu-id="162ce-171">tooinclude tych aplikacji logiki, Dodaj hello **Azure Logic Apps — wybierz przepływ pracy aplikacji logiki** akcji tooyour wyzwalacza.</span><span class="sxs-lookup"><span data-stu-id="162ce-171">tooinclude these logic apps, add hello **Azure Logic Apps - Choose a Logic Apps workflow** action tooyour trigger.</span></span> <span data-ttu-id="162ce-172">Następnie możesz wybrać z kwalifikujących się logiki aplikacji.</span><span class="sxs-lookup"><span data-stu-id="162ce-172">You can then select from eligible logic apps.</span></span>

![Dodaj inną aplikację logiki](./media/logic-apps-http-endpoint/choose-logic-apps-workflow.png)

## <a name="call-or-trigger-logic-apps-through-http-endpoints"></a><span data-ttu-id="162ce-174">Wyzwalacza logiki aplikacji za pomocą punktów końcowych HTTP lub wywołać</span><span class="sxs-lookup"><span data-stu-id="162ce-174">Call or trigger logic apps through HTTP endpoints</span></span>

<span data-ttu-id="162ce-175">Po utworzeniu punktu końcowego HTTP, możesz wyzwolić aplikację logiki za pośrednictwem `POST` metody toohello pełny adres URL.</span><span class="sxs-lookup"><span data-stu-id="162ce-175">After you create your HTTP endpoint, you can trigger your logic app through a `POST` method toohello full URL.</span></span> <span data-ttu-id="162ce-176">Aplikacje logiki mają wbudowaną obsługę dostęp bezpośredni punktów końcowych.</span><span class="sxs-lookup"><span data-stu-id="162ce-176">Logic apps have built-in support for direct-access endpoints.</span></span>

## <a name="reference-content-from-an-incoming-request"></a><span data-ttu-id="162ce-177">Odwołanie do zawartości z przychodzącego żądania</span><span class="sxs-lookup"><span data-stu-id="162ce-177">Reference content from an incoming request</span></span>

<span data-ttu-id="162ce-178">Jeśli typ zawartości hello jest `application/json`, możesz odwoływać właściwości z żądania przychodzącego hello.</span><span class="sxs-lookup"><span data-stu-id="162ce-178">If hello content's type is `application/json`, you can reference properties from hello incoming request.</span></span> <span data-ttu-id="162ce-179">W przeciwnym razie zawartość jest traktowany jako pojedyncza jednostka binarne przekazywanej tooother interfejsów API.</span><span class="sxs-lookup"><span data-stu-id="162ce-179">Otherwise, content is treated as a single binary unit that you can pass tooother APIs.</span></span> <span data-ttu-id="162ce-180">Ta zawartość wewnątrz przepływu pracy hello tooreference, należy przekonwertować tej zawartości.</span><span class="sxs-lookup"><span data-stu-id="162ce-180">tooreference this content inside hello workflow, you must convert that content.</span></span> <span data-ttu-id="162ce-181">Na przykład w przypadku przekazania `application/xml` zawartości, można użyć `@xpath()` do wyodrębnienia XPath lub `@json()` do konwertowania XML tooJSON.</span><span class="sxs-lookup"><span data-stu-id="162ce-181">For example, if you pass `application/xml` content, you can use `@xpath()` for an XPath extraction, or `@json()` for converting XML tooJSON.</span></span> <span data-ttu-id="162ce-182">Dowiedz się więcej o [Praca z typami zawartości](../logic-apps/logic-apps-content-type.md).</span><span class="sxs-lookup"><span data-stu-id="162ce-182">Learn about [working with content types](../logic-apps/logic-apps-content-type.md).</span></span>

<span data-ttu-id="162ce-183">Witaj tooget dane wyjściowe z żądania przychodzącego, można użyć hello `@triggerOutputs()` funkcji.</span><span class="sxs-lookup"><span data-stu-id="162ce-183">tooget hello output from an incoming request, you can use hello `@triggerOutputs()` function.</span></span> <span data-ttu-id="162ce-184">dane wyjściowe Hello może wyglądać w tym przykładzie:</span><span class="sxs-lookup"><span data-stu-id="162ce-184">hello output might look like this example:</span></span>

```json
{
    "headers": {
        "content-type" : "application/json"
    },
    "body": {
        "myProperty" : "property value"
    }
}
```

<span data-ttu-id="162ce-185">Witaj tooaccess `body` właściwości w szczególności służy hello `@triggerBody()` skrótów.</span><span class="sxs-lookup"><span data-stu-id="162ce-185">tooaccess hello `body` property specifically, you can use hello `@triggerBody()` shortcut.</span></span> 

## <a name="respond-toorequests"></a><span data-ttu-id="162ce-186">Odpowiedź toorequests</span><span class="sxs-lookup"><span data-stu-id="162ce-186">Respond toorequests</span></span>

<span data-ttu-id="162ce-187">Możesz toorespond toocertain żądań, które uruchamiają aplikację logiki, zwracając obiekt wywołujący toohello zawartości.</span><span class="sxs-lookup"><span data-stu-id="162ce-187">You might want toorespond toocertain requests that start a logic app by returning content toohello caller.</span></span> <span data-ttu-id="162ce-188">Kod stanu hello tooconstruct, nagłówek i treść odpowiedzi można użyć hello **odpowiedzi** akcji.</span><span class="sxs-lookup"><span data-stu-id="162ce-188">tooconstruct hello status code, header, and body for your response, you can use hello **Response** action.</span></span> <span data-ttu-id="162ce-189">Ta akcja może występować w dowolnym miejscu w aplikacji logiki, nie tylko na końcu hello przepływ pracy.</span><span class="sxs-lookup"><span data-stu-id="162ce-189">This action can appear anywhere in your logic app, not just at hello end of your workflow.</span></span>

> [!NOTE] 
> <span data-ttu-id="162ce-190">Jeśli nie zawiera aplikacji logiki **odpowiedzi**, odpowiada punkt końcowy hello HTTP *natychmiast* z **202 zaakceptowane** stanu.</span><span class="sxs-lookup"><span data-stu-id="162ce-190">If your logic app doesn't include a **Response**, hello HTTP endpoint responds *immediately* with a **202 Accepted** status.</span></span> <span data-ttu-id="162ce-191">Ponadto dla oryginalnego żądania tooget hello odpowiedź hello, wszystkich kroków wymaganych do odpowiedzi hello musi zakończyć się w obrębie hello [limit czasu żądania](./logic-apps-limits-and-config.md) chyba, że wywołanie przepływu pracy hello jako aplikację logiki zagnieżdżonych.</span><span class="sxs-lookup"><span data-stu-id="162ce-191">Also, for hello original request tooget hello response, all steps required for hello response must finish within hello [request timeout limit](./logic-apps-limits-and-config.md) unless you call hello workflow as a nested logic app.</span></span> <span data-ttu-id="162ce-192">Jeśli się nie dzieje nie otrzymano odpowiedzi w ramach tego limitu, hello przychodzące żądanie upłynie limit czasu i odbiera odpowiedź hello HTTP **408 Limit czasu klienta**.</span><span class="sxs-lookup"><span data-stu-id="162ce-192">If no response happens within this limit, hello incoming request times out and receives hello HTTP response **408 Client timeout**.</span></span> <span data-ttu-id="162ce-193">Dla aplikacji logiki zagnieżdżonych aplikacji logiki nadrzędnego hello nadal toowait dla odpowiedzi do czasu ukończenia, niezależnie od tego, ile czasu jest wymagana.</span><span class="sxs-lookup"><span data-stu-id="162ce-193">For nested logic apps, hello parent logic app continues toowait for a response until completed, regardless of how much time is required.</span></span>

### <a name="construct-hello-response"></a><span data-ttu-id="162ce-194">Konstrukcja hello odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="162ce-194">Construct hello response</span></span>

<span data-ttu-id="162ce-195">W treści odpowiedzi hello może zawierać więcej niż jeden nagłówek i dowolnego typu zawartości.</span><span class="sxs-lookup"><span data-stu-id="162ce-195">You can include more than one header and any type of content in hello response body.</span></span> <span data-ttu-id="162ce-196">W naszym przykładzie odpowiedzi, nagłówek hello Określa, czy odpowiedź hello ma typ zawartości `application/json`.</span><span class="sxs-lookup"><span data-stu-id="162ce-196">In our example response, hello header specifies that hello response has content type `application/json`.</span></span> <span data-ttu-id="162ce-197">i zawiera treść hello `title` i `name`, oparte na wcześniej dodano hello schematu JSON hello **żądania** wyzwalacza.</span><span class="sxs-lookup"><span data-stu-id="162ce-197">and hello body contains `title` and `name`, based on hello JSON schema updated previously for hello **Request** trigger.</span></span>

![Akcja odpowiedzi HTTP][3]

<span data-ttu-id="162ce-199">Odpowiedzi ma następujące właściwości:</span><span class="sxs-lookup"><span data-stu-id="162ce-199">Responses have these properties:</span></span>

| <span data-ttu-id="162ce-200">Właściwość</span><span class="sxs-lookup"><span data-stu-id="162ce-200">Property</span></span> | <span data-ttu-id="162ce-201">Opis</span><span class="sxs-lookup"><span data-stu-id="162ce-201">Description</span></span> |
| --- | --- |
| <span data-ttu-id="162ce-202">statusCode</span><span class="sxs-lookup"><span data-stu-id="162ce-202">statusCode</span></span> |<span data-ttu-id="162ce-203">Określa kod stanu hello HTTP odpowiada toohello żądania przychodzącego.</span><span class="sxs-lookup"><span data-stu-id="162ce-203">Specifies hello HTTP status code for responding toohello incoming request.</span></span> <span data-ttu-id="162ce-204">Ten kod może być prawidłowym stanem kodu, który rozpoczyna się od 2xx, 4xx lub 5xx.</span><span class="sxs-lookup"><span data-stu-id="162ce-204">This code can be any valid status code that starts with 2xx, 4xx, or 5xx.</span></span> <span data-ttu-id="162ce-205">Kody stanu 3xx nie są dozwolone.</span><span class="sxs-lookup"><span data-stu-id="162ce-205">However, 3xx status codes are not permitted.</span></span> |
| <span data-ttu-id="162ce-206">Nagłówki</span><span class="sxs-lookup"><span data-stu-id="162ce-206">headers</span></span> |<span data-ttu-id="162ce-207">Definiuje dowolną liczbę tooinclude nagłówki odpowiedzi hello.</span><span class="sxs-lookup"><span data-stu-id="162ce-207">Defines any number of headers tooinclude in hello response.</span></span> |
| <span data-ttu-id="162ce-208">Treści</span><span class="sxs-lookup"><span data-stu-id="162ce-208">body</span></span> |<span data-ttu-id="162ce-209">Określa obiekt treści, która może być ciągiem, obiekt JSON lub nawet binarny zawartości przywoływanej z poprzedniego kroku.</span><span class="sxs-lookup"><span data-stu-id="162ce-209">Specifies a body object that can be a string, a JSON object, or even binary content referenced from a previous step.</span></span> |

<span data-ttu-id="162ce-210">Oto, jakie schematu JSON hello prawdopodobnie teraz dla hello **odpowiedzi** akcji:</span><span class="sxs-lookup"><span data-stu-id="162ce-210">Here's what hello JSON schema looks like now for hello **Response** action:</span></span>

``` json
"Response": {
   "inputs": {
      "body": {
         "title": "@{triggerBody()?['title']}",
         "name": "@{triggerBody()?['name']}"
      },
      "headers": {
           "content-type": "application/json"
      },
      "statusCode": 200
   },
   "runAfter": {},
   "type": "Response"
}
```

> [!TIP]
> <span data-ttu-id="162ce-211">Wybierz tooview hello pełnej JSON definicji aplikacji logiki, na powitania projektanta aplikacji logiki, **widok Kod**.</span><span class="sxs-lookup"><span data-stu-id="162ce-211">tooview hello complete JSON definition for your logic app, on hello Logic App Designer, choose **Code view**.</span></span>

## <a name="q--a"></a><span data-ttu-id="162ce-212">Pytania i odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="162ce-212">Q & A</span></span>

#### <a name="q-what-about-url-security"></a><span data-ttu-id="162ce-213">Pytanie: jak adres URL zabezpieczeń?</span><span class="sxs-lookup"><span data-stu-id="162ce-213">Q: What about URL security?</span></span>

<span data-ttu-id="162ce-214">A: azure generuje bezpieczne logiki wywołania zwrotnego adresy URL aplikacji przy użyciu udostępnionych podpis dostępu (SAS).</span><span class="sxs-lookup"><span data-stu-id="162ce-214">A: Azure securely generates logic app callback URLs using a Shared Access Signature (SAS).</span></span> <span data-ttu-id="162ce-215">Ta sygnatura przekazuje jako parametr zapytania i musi zostać zweryfikowany przed mogą wyzwalać aplikację logiki.</span><span class="sxs-lookup"><span data-stu-id="162ce-215">This signature passes through as a query parameter and must be validated before your logic app can fire.</span></span> <span data-ttu-id="162ce-216">Platforma Azure generuje podpisu hello przy użyciu unikatowej kombinacji wartości klucza tajnego dla każdej aplikacji logiki, nazwa wyzwalacza hello i hello operacja, która jest wykonywana.</span><span class="sxs-lookup"><span data-stu-id="162ce-216">Azure generates hello signature using a unique combination of a secret key per logic app, hello trigger name, and hello operation that's performed.</span></span> <span data-ttu-id="162ce-217">Dlatego jeśli ktoś ma klucz aplikacji logiki tajny toohello dostępu, nie można wygenerować prawidłowego podpisu.</span><span class="sxs-lookup"><span data-stu-id="162ce-217">So unless someone has access toohello secret logic app key, they cannot generate a valid signature.</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="162ce-218">Produkcyjnego i systemów zabezpieczeń zaleca przed wywołaniem bezpośrednio z przeglądarki hello aplikację logiki, ponieważ:</span><span class="sxs-lookup"><span data-stu-id="162ce-218">For production and secure systems, we strongly recommend against calling your logic app directly from hello browser because:</span></span>
   > 
   > * <span data-ttu-id="162ce-219">w adresie URL hello pojawi się Hello udostępniony klucz dostępu.</span><span class="sxs-lookup"><span data-stu-id="162ce-219">hello shared access key appears in hello URL.</span></span>
   > * <span data-ttu-id="162ce-220">Nie można zarządzać bezpieczna zasady zawartości powodu domen tooshared wielu odbiorców aplikacji logiki.</span><span class="sxs-lookup"><span data-stu-id="162ce-220">You can't manage secure content policies due tooshared domains across Logic App customers.</span></span>

#### <a name="q-can-i-configure-http-endpoints-further"></a><span data-ttu-id="162ce-221">Pytanie: czy można skonfigurować dodatkowe punkty końcowe HTTP?</span><span class="sxs-lookup"><span data-stu-id="162ce-221">Q: Can I configure HTTP endpoints further?</span></span>

<span data-ttu-id="162ce-222">Odpowiedź: tak punktów końcowych HTTP obsługuje bardziej zaawansowanych konfiguracji za pomocą [ **zarządzanie interfejsami API**](../api-management/api-management-key-concepts.md).</span><span class="sxs-lookup"><span data-stu-id="162ce-222">A: Yes, HTTP endpoints support more advanced configuration through [**API Management**](../api-management/api-management-key-concepts.md).</span></span> <span data-ttu-id="162ce-223">Ta usługa również oferuje możliwości hello tooconsistently możesz zarządzać wszystkie swoje interfejsy API, łącznie z aplikacji logiki, konfigurowanie niestandardowych nazw domen, użyj więcej metod uwierzytelniania i inne, na przykład:</span><span class="sxs-lookup"><span data-stu-id="162ce-223">This service also offers hello capability for you tooconsistently manage all your APIs, including logic apps, set up custom domain names, use more authentication methods, and more, for example:</span></span>

* [<span data-ttu-id="162ce-224">Metoda żądania zmiany hello</span><span class="sxs-lookup"><span data-stu-id="162ce-224">Change hello request method</span></span>](https://docs.microsoft.com/azure/api-management/api-management-advanced-policies#SetRequestMethod)
* [<span data-ttu-id="162ce-225">Segmenty adresu URL hello hello żądania zmiany</span><span class="sxs-lookup"><span data-stu-id="162ce-225">Change hello URL segments of hello request</span></span>](https://docs.microsoft.com/azure/api-management/api-management-transformation-policies#RewriteURL)
* <span data-ttu-id="162ce-226">Konfigurowanie domeny zarządzanie interfejsami API w hello [portalu Azure](https://portal.azure.com/ "portalu Azure")</span><span class="sxs-lookup"><span data-stu-id="162ce-226">Set up your API Management domains in hello [Azure portal](https://portal.azure.com/ "Azure portal")</span></span>
* <span data-ttu-id="162ce-227">Konfigurowanie zasad toocheck dla uwierzytelniania podstawowego</span><span class="sxs-lookup"><span data-stu-id="162ce-227">Set up policy toocheck for Basic authentication</span></span>

#### <a name="q-what-changed-when-hello-schema-migrated-from-hello-december-1-2014-preview"></a><span data-ttu-id="162ce-228">Pytanie: jakie zmieniony podczas migracji hello schematu w hello 1 grudnia 2014 r. w wersji zapoznawczej?</span><span class="sxs-lookup"><span data-stu-id="162ce-228">Q: What changed when hello schema migrated from hello December 1, 2014 preview?</span></span>

<span data-ttu-id="162ce-229">Odpowiedź: w tym miejscu znajduje się podsumowanie dotyczące tych zmian:</span><span class="sxs-lookup"><span data-stu-id="162ce-229">A: Here's a summary about these changes:</span></span>

| <span data-ttu-id="162ce-230">Wersja zapoznawcza 1 grudnia 2014 r.</span><span class="sxs-lookup"><span data-stu-id="162ce-230">December 1, 2014 preview</span></span> | <span data-ttu-id="162ce-231">1 czerwca 2016 r.</span><span class="sxs-lookup"><span data-stu-id="162ce-231">June 1, 2016</span></span> |
| --- | --- |
| <span data-ttu-id="162ce-232">Kliknij przycisk **odbiornik HTTP** aplikacji interfejsu API</span><span class="sxs-lookup"><span data-stu-id="162ce-232">Click **HTTP Listener** API App</span></span> |<span data-ttu-id="162ce-233">Kliknij przycisk **ręczne wyzwalacza** (wymagane dla żadnej aplikacji interfejsu API)</span><span class="sxs-lookup"><span data-stu-id="162ce-233">Click **Manual trigger** (no API App required)</span></span> |
| <span data-ttu-id="162ce-234">Ustawienia odbiornika HTTP "*automatycznie wysyła odpowiedź*"</span><span class="sxs-lookup"><span data-stu-id="162ce-234">HTTP Listener setting "*Sends response automatically*"</span></span> |<span data-ttu-id="162ce-235">Zawierają **odpowiedzi** akcji lub nie znajduje się w hello definicji przepływu pracy</span><span class="sxs-lookup"><span data-stu-id="162ce-235">Either include a **Response** action or not in hello workflow definition</span></span> |
| <span data-ttu-id="162ce-236">Skonfiguruj uwierzytelnianie podstawowe lub OAuth</span><span class="sxs-lookup"><span data-stu-id="162ce-236">Configure Basic or OAuth authentication</span></span> |<span data-ttu-id="162ce-237">za pomocą interfejsu API zarządzania</span><span class="sxs-lookup"><span data-stu-id="162ce-237">via API Management</span></span> |
| <span data-ttu-id="162ce-238">Skonfiguruj HTTP — metoda</span><span class="sxs-lookup"><span data-stu-id="162ce-238">Configure HTTP method</span></span> |<span data-ttu-id="162ce-239">W obszarze **Pokaż zaawansowane opcje**, wybierz metodę HTTP</span><span class="sxs-lookup"><span data-stu-id="162ce-239">Under **Show advanced options**, choose an HTTP method</span></span> |
| <span data-ttu-id="162ce-240">Konfigurowanie ścieżki względnej</span><span class="sxs-lookup"><span data-stu-id="162ce-240">Configure relative path</span></span> |<span data-ttu-id="162ce-241">W obszarze **Pokaż zaawansowane opcje**, Dodaj ścieżkę względną</span><span class="sxs-lookup"><span data-stu-id="162ce-241">Under **Show advanced options**, add a relative path</span></span> |
| <span data-ttu-id="162ce-242">Odwołanie hello treści przychodzące za pośrednictwem`@triggerOutputs().body.Content`</span><span class="sxs-lookup"><span data-stu-id="162ce-242">Reference hello incoming body through `@triggerOutputs().body.Content`</span></span> |<span data-ttu-id="162ce-243">Odwołanie za pośrednictwem`@triggerOutputs().body`</span><span class="sxs-lookup"><span data-stu-id="162ce-243">Reference through `@triggerOutputs().body`</span></span> |
| <span data-ttu-id="162ce-244">**Wyślij odpowiedź HTTP** akcji na powitania odbiornika HTTP</span><span class="sxs-lookup"><span data-stu-id="162ce-244">**Send HTTP response** action on hello HTTP Listener</span></span> |<span data-ttu-id="162ce-245">Kliknij przycisk **żądania tooHTTP odpowiedź** (wymagane dla żadnej aplikacji interfejsu API)</span><span class="sxs-lookup"><span data-stu-id="162ce-245">Click **Respond tooHTTP request** (no API App required)</span></span> |

## <a name="get-help"></a><span data-ttu-id="162ce-246">Uzyskiwanie pomocy</span><span class="sxs-lookup"><span data-stu-id="162ce-246">Get help</span></span>

<span data-ttu-id="162ce-247">pytania tooask odpowiedzi na pytania i Dowiedz się, jakie inne usługi Azure Logic Apps robią użytkownicy, odwiedź stronę hello [forum usługi Azure Logic Apps](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurelogicapps).</span><span class="sxs-lookup"><span data-stu-id="162ce-247">tooask questions, answer questions, and learn what other Azure Logic Apps users are doing, visit hello [Azure Logic Apps forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurelogicapps).</span></span>

<span data-ttu-id="162ce-248">toohelp poprawy usługi Azure Logic Apps i łącznikami, Zagłosuj lub Prześlij pomysłów na powitania [witrynę opinii użytkowników usługi Azure Logic Apps](http://aka.ms/logicapps-wish).</span><span class="sxs-lookup"><span data-stu-id="162ce-248">toohelp improve Azure Logic Apps and connectors, vote on or submit ideas at hello [Azure Logic Apps user feedback site](http://aka.ms/logicapps-wish).</span></span>

## <a name="next-steps"></a><span data-ttu-id="162ce-249">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="162ce-249">Next steps</span></span>

* [<span data-ttu-id="162ce-250">Tworzenie definicji aplikacji logiki</span><span class="sxs-lookup"><span data-stu-id="162ce-250">Author logic app definitions</span></span>](./logic-apps-author-definitions.md)
* [<span data-ttu-id="162ce-251">Obsługa błędów i wyjątków</span><span class="sxs-lookup"><span data-stu-id="162ce-251">Handle errors and exceptions</span></span>](./logic-apps-exception-handling.md)

[1]: ./media/logic-apps-http-endpoint/manualtrigger.png
[2]: ./media/logic-apps-http-endpoint/manualtriggerurl.png
[3]: ./media/logic-apps-http-endpoint/response.png
