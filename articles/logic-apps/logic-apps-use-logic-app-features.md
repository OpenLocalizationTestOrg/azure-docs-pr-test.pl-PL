---
title: "aaaAdd warunki i uruchomić przepływ pracy - Azure Logic Apps | Dokumentacja firmy Microsoft"
description: "Kontroluje sposób uruchamiania przepływów pracy w aplikacjach logiki platformy Azure, dodając logikę warunkową, wyzwalacze, akcje i parametry."
author: stepsic-microsoft-com
manager: anneta
editor: 
services: logic-apps
documentationcenter: 
ms.assetid: e4e24de4-049a-4b3a-a14c-3bf3163287a8
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/28/2017
ms.author: LADocs; stepsic
ms.openlocfilehash: 76d5e44590ffa14cf70d7a93b99a241d286d555b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="use-logic-apps-features"></a><span data-ttu-id="da2fe-103">Korzystanie z funkcji Logic Apps</span><span class="sxs-lookup"><span data-stu-id="da2fe-103">Use Logic Apps features</span></span>

<span data-ttu-id="da2fe-104">W [poprzedniego tematu](../logic-apps/logic-apps-create-a-logic-app.md), utworzyć pierwszą aplikację logiki.</span><span class="sxs-lookup"><span data-stu-id="da2fe-104">In a [previous topic](../logic-apps/logic-apps-create-a-logic-app.md), you created your first logic app.</span></span> <span data-ttu-id="da2fe-105">toocontrol przepływu pracy aplikacji logiki, można określić różne ścieżki dla Twojego toorun aplikacji logiki i jak zbyt przetwarzania danych w macierzy, kolekcji i partie.</span><span class="sxs-lookup"><span data-stu-id="da2fe-105">toocontrol your logic app's workflow, you can specify different paths for your logic app toorun and how too process data in arrays, collections, and batches.</span></span> <span data-ttu-id="da2fe-106">W przepływie pracy aplikacji logiki można uwzględnić następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="da2fe-106">You can include these elements in your logic app workflow:</span></span>

* <span data-ttu-id="da2fe-107">Warunki i [przełącznika instrukcje](../logic-apps/logic-apps-switch-case.md) let aplikację logiki, uruchom różnych akcji w oparciu o Określa, czy zostały spełnione określone warunki.</span><span class="sxs-lookup"><span data-stu-id="da2fe-107">Conditions and [switch statements](../logic-apps/logic-apps-switch-case.md) let your logic app run different actions based on whether specific conditions are met.</span></span>

* <span data-ttu-id="da2fe-108">[Pętle](../logic-apps/logic-apps-loops-and-scopes.md) let aplikację logiki cyklicznie uruchamiany kroki.</span><span class="sxs-lookup"><span data-stu-id="da2fe-108">[Loops](../logic-apps/logic-apps-loops-and-scopes.md) let your logic app run steps repeatedly.</span></span> <span data-ttu-id="da2fe-109">Na przykład można powtórzyć akcje dotyczące tablicy korzystając z **For_each** pętli.</span><span class="sxs-lookup"><span data-stu-id="da2fe-109">For example, you can repeat actions over an array when you use a **For_each** loop.</span></span> <span data-ttu-id="da2fe-110">Lub akcji można powtórzyć, dopóki spełniony jest warunek, korzystając z **do momentu** pętli.</span><span class="sxs-lookup"><span data-stu-id="da2fe-110">Or you can repeat actions until a condition is met when you use an **Until** loop.</span></span>

* <span data-ttu-id="da2fe-111">[Zakresy](../logic-apps/logic-apps-loops-and-scopes.md) let uruchamianym serii akcji, na przykład tooimplement obsługi wyjątków.</span><span class="sxs-lookup"><span data-stu-id="da2fe-111">[Scopes](../logic-apps/logic-apps-loops-and-scopes.md) let you group series of actions together, for example, tooimplement exception handling.</span></span>

* <span data-ttu-id="da2fe-112">[Debatching](../logic-apps/logic-apps-loops-and-scopes.md) umożliwia aplikację logiki, uruchom oddzielne przepływy pracy dla elementów w tablicy, gdy używasz hello **SplitOn** polecenia.</span><span class="sxs-lookup"><span data-stu-id="da2fe-112">[Debatching](../logic-apps/logic-apps-loops-and-scopes.md) lets your logic app start separate workflows for items in an array when you use hello **SplitOn** command.</span></span>

<span data-ttu-id="da2fe-113">W tym temacie przedstawiono inne pojęć dotyczących tworzenia aplikacji logiki:</span><span class="sxs-lookup"><span data-stu-id="da2fe-113">This topic introduces other concepts for building your logic app:</span></span>

* <span data-ttu-id="da2fe-114">Kod widoku tooedit istniejących aplikacji logiki</span><span class="sxs-lookup"><span data-stu-id="da2fe-114">Code view tooedit an existing logic app</span></span>
* <span data-ttu-id="da2fe-115">Opcje uruchamiania przepływu pracy</span><span class="sxs-lookup"><span data-stu-id="da2fe-115">Options for starting a workflow</span></span>

## <a name="conditions-run-steps-only-after-meeting-a-condition"></a><span data-ttu-id="da2fe-116">Warunki: Uruchamianie kroków tylko po spełniających warunek</span><span class="sxs-lookup"><span data-stu-id="da2fe-116">Conditions: Run steps only after meeting a condition</span></span>

<span data-ttu-id="da2fe-117">toohave aplikację logiki, uruchom kroki tylko wtedy, gdy dane spełniają określone kryteria, można dodać warunek, który porównuje dane w przepływie pracy hello względem określonych pól lub wartości.</span><span class="sxs-lookup"><span data-stu-id="da2fe-117">toohave your logic app run steps only when data meets specific criteria, you can add a condition that compares data in hello workflow against specific fields or values.</span></span>

<span data-ttu-id="da2fe-118">Na przykład załóżmy, że masz aplikację logiki, która wysyła zbyt dużo żądań wiadomości e-mail Posty na kanału informacyjnego RSS witryny sieci Web.</span><span class="sxs-lookup"><span data-stu-id="da2fe-118">For example, suppose you have a logic app that sends you too many emails for posts on a website's RSS feed.</span></span> <span data-ttu-id="da2fe-119">Można dodać warunku, aby aplikację logiki wysyła wiadomości e-mail, tylko wtedy, gdy po hello nowe należy tooa określonej kategorii.</span><span class="sxs-lookup"><span data-stu-id="da2fe-119">You can add a condition so that your logic app sends email only when hello new post belongs tooa specific category.</span></span>

1. <span data-ttu-id="da2fe-120">W hello [portalu Azure](https://portal.azure.com), znajdowanie i otwieranie aplikacji logiki w Projektancie aplikacji logiki.</span><span class="sxs-lookup"><span data-stu-id="da2fe-120">In hello [Azure portal](https://portal.azure.com), find and open your logic app in Logic App Designer.</span></span>

2. <span data-ttu-id="da2fe-121">Dodaj warunek toohello przepływu pracy lokalizacji.</span><span class="sxs-lookup"><span data-stu-id="da2fe-121">Add a condition toohello workflow location that you want.</span></span> 

   <span data-ttu-id="da2fe-122">warunek hello tooadd między krokami istniejących w przepływie pracy aplikacji logiki hello, przesuń wskaźnik hello na strzałkę hello miejscu tooadd hello warunku.</span><span class="sxs-lookup"><span data-stu-id="da2fe-122">tooadd hello condition between existing steps in hello logic app workflow, move hello pointer over hello arrow where you want tooadd hello condition.</span></span> 
   <span data-ttu-id="da2fe-123">Wybierz hello **znak plus** (**+**), a następnie wybierz **Dodaj warunek**.</span><span class="sxs-lookup"><span data-stu-id="da2fe-123">Choose hello **plus sign** (**+**), then choose **Add a condition**.</span></span> <span data-ttu-id="da2fe-124">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="da2fe-124">For example:</span></span>

   ![Dodaj warunek toologic aplikacji](./media/logic-apps-use-logic-app-features/add-condition.png)

   > [!NOTE]
   > <span data-ttu-id="da2fe-126">Jeśli chcesz tooadd warunek hello końca bieżącego przepływu pracy, przejdź toohello dołu aplikację logiki i wybierz **+ nowy krok**.</span><span class="sxs-lookup"><span data-stu-id="da2fe-126">If you want tooadd a condition at hello end of your current workflow, go toohello bottom of your logic app, and choose **+ New step**.</span></span>

3. <span data-ttu-id="da2fe-127">Teraz można zdefiniować hello warunku.</span><span class="sxs-lookup"><span data-stu-id="da2fe-127">Now define hello condition.</span></span> <span data-ttu-id="da2fe-128">Określ pola źródłowego hello mają tooevaluate, hello tooperform operację i wartość docelowa hello lub pola.</span><span class="sxs-lookup"><span data-stu-id="da2fe-128">Specify hello source field that you want tooevaluate, hello operation tooperform, and hello target value or field.</span></span> <span data-ttu-id="da2fe-129">tooadd istniejących pól tooyour warunku, wybierz jedną z hello **listy zawartości dynamicznej Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="da2fe-129">tooadd existing fields tooyour condition, choose from hello **Add dynamic content list**.</span></span>

   <span data-ttu-id="da2fe-130">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="da2fe-130">For example:</span></span>

   ![Edytuj warunek w trybie podstawowym](./media/logic-apps-use-logic-app-features/edit-condition-basic-mode.png)

   <span data-ttu-id="da2fe-132">Oto hello Pełny warunek:</span><span class="sxs-lookup"><span data-stu-id="da2fe-132">Here's hello complete condition:</span></span>

   ![Pełny warunek](./media/logic-apps-use-logic-app-features/edit-condition-basic-mode-2.png)

   > [!TIP]
   > <span data-ttu-id="da2fe-134">Wybierz warunek hello toodefine w kodzie, **edytowanie w trybie zaawansowanym**.</span><span class="sxs-lookup"><span data-stu-id="da2fe-134">toodefine hello condition in code, choose **Edit in advanced mode**.</span></span> <span data-ttu-id="da2fe-135">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="da2fe-135">For example:</span></span>
   > 
   > ![Edytuj warunek w kodzie](./media/logic-apps-use-logic-app-features/edit-condition-advanced-mode.png)

4. <span data-ttu-id="da2fe-137">W obszarze **tak, jeśli** i **nr IF**, Dodaj tooperform kroki hello według tego, czy jest spełniony warunek hello.</span><span class="sxs-lookup"><span data-stu-id="da2fe-137">Under **IF YES** and **IF NO**, add hello steps tooperform based on whether hello condition is met.</span></span>

   <span data-ttu-id="da2fe-138">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="da2fe-138">For example:</span></span>

   ![Stan tak i ścieżek](./media/logic-apps-use-logic-app-features/condition-yes-no-path.png)

   > [!TIP]
   > <span data-ttu-id="da2fe-140">Można przeciągnij istniejące działania do hello **tak, jeśli** i **nr IF** ścieżki.</span><span class="sxs-lookup"><span data-stu-id="da2fe-140">You can drag existing actions into hello **IF YES** and **IF NO** paths.</span></span>

5. <span data-ttu-id="da2fe-141">Gdy wszystko będzie gotowe, Zapisz aplikację logiki.</span><span class="sxs-lookup"><span data-stu-id="da2fe-141">When you're done, save your logic app.</span></span>

<span data-ttu-id="da2fe-142">Teraz możesz otrzymywać wiadomości e-mail, tylko wtedy, gdy wpisy hello spełniają warunek.</span><span class="sxs-lookup"><span data-stu-id="da2fe-142">Now you get emails only when hello posts meet your condition.</span></span>

## <a name="repeat-actions-over-a-list-with-foreach"></a><span data-ttu-id="da2fe-143">Powtórz akcje listy za pomocą instrukcji forEach</span><span class="sxs-lookup"><span data-stu-id="da2fe-143">Repeat actions over a list with forEach</span></span>

<span data-ttu-id="da2fe-144">pętli forEach Hello określa toorepeat tablicy akcji za pośrednictwem.</span><span class="sxs-lookup"><span data-stu-id="da2fe-144">hello forEach loop specifies an array toorepeat an action over.</span></span> <span data-ttu-id="da2fe-145">Jeśli nie jest tablicą, przepływ hello zakończy się niepowodzeniem.</span><span class="sxs-lookup"><span data-stu-id="da2fe-145">If it is not an array, hello flow fails.</span></span> <span data-ttu-id="da2fe-146">Na przykład jeśli masz action1, który generuje tablicę komunikatów i ma toosend każdy komunikat, we właściwościach hello działań. można uwzględnić tej instrukcji forEach:`forEach : "@action('action1').outputs.messages"`</span><span class="sxs-lookup"><span data-stu-id="da2fe-146">For example, if you have action1 that outputs an array of messages, and you want toosend each message, you can include this forEach statement in hello properties of your action: `forEach : "@action('action1').outputs.messages"`</span></span>

## <a name="edit-hello-code-definition-for-a-logic-app"></a><span data-ttu-id="da2fe-147">Edytuj kod hello definicję aplikacji logiki</span><span class="sxs-lookup"><span data-stu-id="da2fe-147">Edit hello code definition for a logic app</span></span>

<span data-ttu-id="da2fe-148">Mimo że masz hello projektanta aplikacji logiki można edytować bezpośrednio hello kodu, który definiuje aplikacji logiki.</span><span class="sxs-lookup"><span data-stu-id="da2fe-148">Although you have hello Logic App Designer, you can directly edit hello code that defines a logic app.</span></span>

1. <span data-ttu-id="da2fe-149">Na pasku poleceń hello, wybierz **widok Kod**.</span><span class="sxs-lookup"><span data-stu-id="da2fe-149">On hello command bar, choose **Code view**.</span></span>

    <span data-ttu-id="da2fe-150">Pełna Edytor otwiera się i przedstawiono definicję hello, który można edytować.</span><span class="sxs-lookup"><span data-stu-id="da2fe-150">A full editor opens and shows hello definition you edited.</span></span>

    ![Widok kodu](media/logic-apps-use-logic-app-features/codeview.png)

    <span data-ttu-id="da2fe-152">W edytorze tekstu hello, można skopiować i wkleić dowolną liczbę akcji w obrębie hello tej samej aplikacji logiki lub między aplikacji logiki.</span><span class="sxs-lookup"><span data-stu-id="da2fe-152">In hello text editor, you can copy and paste any number of actions within hello same logic app or between logic apps.</span></span> 
    <span data-ttu-id="da2fe-153">Można również łatwo Dodaj lub Usuń całą sekcję od definicji hello i definicji mogą również współużytkować z innymi osobami.</span><span class="sxs-lookup"><span data-stu-id="da2fe-153">You can also easily add or remove entire sections from hello definition, and you can also share definitions with others.</span></span>

2. <span data-ttu-id="da2fe-154">Wybierz zmiany, toosave **zapisać**.</span><span class="sxs-lookup"><span data-stu-id="da2fe-154">toosave your edits, choose **Save**.</span></span>

## <a name="parameters"></a><span data-ttu-id="da2fe-155">Parametry</span><span class="sxs-lookup"><span data-stu-id="da2fe-155">Parameters</span></span>

<span data-ttu-id="da2fe-156">Niektóre z funkcji Logic Apps są dostępne tylko w widoku kodu, na przykład parametry.</span><span class="sxs-lookup"><span data-stu-id="da2fe-156">Some Logic Apps capabilities are available only in code view, for example, parameters.</span></span> <span data-ttu-id="da2fe-157">Parametry umożliwiają łatwe tooreuse wartości w całej aplikacji logiki.</span><span class="sxs-lookup"><span data-stu-id="da2fe-157">Parameters make it easy tooreuse values throughout your logic app.</span></span> <span data-ttu-id="da2fe-158">Na przykład jeśli masz adres e-mail, która ma zostać użyta w kilka akcji, należy zdefiniować tego adresu e-mail jako parametr.</span><span class="sxs-lookup"><span data-stu-id="da2fe-158">For example, if you have an email address that you want use in several actions, you should define that email address as a parameter.</span></span>

<span data-ttu-id="da2fe-159">Parametry są odpowiednie w ściąganie wartości są prawdopodobnie toochange partii.</span><span class="sxs-lookup"><span data-stu-id="da2fe-159">Parameters are good for pulling out values that you are likely toochange a lot.</span></span> <span data-ttu-id="da2fe-160">Są one szczególnie przydatne, gdy będziesz potrzebować toooverride parametrów w różnych środowiskach.</span><span class="sxs-lookup"><span data-stu-id="da2fe-160">They are especially useful when you need toooverride parameters in different environments.</span></span> <span data-ttu-id="da2fe-161">Parametry toooverride opartych na środowisku, zobacz temat toolearn [Tworzenie definicji aplikacji logiki](../logic-apps/logic-apps-author-definitions.md) i [dokumentacja interfejsu API REST](https://docs.microsoft.com/rest/api/logic).</span><span class="sxs-lookup"><span data-stu-id="da2fe-161">toolearn how toooverride parameters based on environment, see [Author logic app definitions](../logic-apps/logic-apps-author-definitions.md) and [REST API documentation](https://docs.microsoft.com/rest/api/logic).</span></span>

<span data-ttu-id="da2fe-162">W tym przykładzie pokazano sposób tooupdate istniejących aplikacji logiki, aby można używać parametrów dla hello wyszukiwanego terminu.</span><span class="sxs-lookup"><span data-stu-id="da2fe-162">This example shows how tooupdate your existing logic app so that you can use parameters for hello query term.</span></span>

1. <span data-ttu-id="da2fe-163">W widoku Kod, Znajdź hello `parameters : {}` obiekt, a następnie dodaj `currentFeedUrl` obiektu:</span><span class="sxs-lookup"><span data-stu-id="da2fe-163">In code view, find hello `parameters : {}` object, and add a `currentFeedUrl` object:</span></span>

        "currentFeedUrl" : {
            "type" : "string",
            "defaultValue" : "http://rss.cnn.com/rss/cnn_topstories.rss"
        }

2. <span data-ttu-id="da2fe-164">Przejdź toohello `When_a_feed-item_is_published` akcji, Znajdź hello `queries` sekcji, a wartość zapytania hello:`"feedUrl": "#@{parameters('currentFeedUrl')}"`</span><span class="sxs-lookup"><span data-stu-id="da2fe-164">Go toohello `When_a_feed-item_is_published` action, find hello `queries` section, and replace hello query value with : `"feedUrl": "#@{parameters('currentFeedUrl')}"`</span></span> 

    <span data-ttu-id="da2fe-165">toojoin dwa lub więcej ciągów, można również użyć hello `concat` funkcji.</span><span class="sxs-lookup"><span data-stu-id="da2fe-165">toojoin two or more strings, you can also use hello `concat` function.</span></span> 
    <span data-ttu-id="da2fe-166">Na przykład `"@concat('#',parameters('currentFeedUrl'))"` works hello takie same jak hello powyżej.</span><span class="sxs-lookup"><span data-stu-id="da2fe-166">For example, `"@concat('#',parameters('currentFeedUrl'))"` works hello same as hello above.</span></span>

3.  <span data-ttu-id="da2fe-167">Gdy wszystko będzie gotowe, wybierz pozycję **zapisać**.</span><span class="sxs-lookup"><span data-stu-id="da2fe-167">When you're done, choose **Save**.</span></span> 

    <span data-ttu-id="da2fe-168">Teraz możesz zmienić witryny hello danych RSS przez przekazanie do innego adresu URL za pośrednictwem hello `currentFeedURL` obiektu.</span><span class="sxs-lookup"><span data-stu-id="da2fe-168">Now you can change hello website's RSS feed by passing a different URL through hello `currentFeedURL` object.</span></span>

<span data-ttu-id="da2fe-169">Dowiedz się więcej o [jak definicjami aplikacji logiki tooauthor](../logic-apps/logic-apps-author-definitions.md).</span><span class="sxs-lookup"><span data-stu-id="da2fe-169">Learn more about [how tooauthor logic app definitions](../logic-apps/logic-apps-author-definitions.md).</span></span>

## <a name="start-logic-app-workflows"></a><span data-ttu-id="da2fe-170">Uruchomić przepływy pracy aplikacji logiki</span><span class="sxs-lookup"><span data-stu-id="da2fe-170">Start logic app workflows</span></span>

<span data-ttu-id="da2fe-171">Masz różne opcje uruchamiania przepływu pracy hello zdefiniowanych w aplikacji logiki.</span><span class="sxs-lookup"><span data-stu-id="da2fe-171">You have different options for starting hello workflow defined in your logic app.</span></span> <span data-ttu-id="da2fe-172">Zawsze można uruchomić przepływu pracy na żądanie w hello [portalu Azure].</span><span class="sxs-lookup"><span data-stu-id="da2fe-172">You can always start a workflow on-demand in hello [Azure portal].</span></span>

### <a name="recurrence-triggers"></a><span data-ttu-id="da2fe-173">Wyzwalacze cyklu</span><span class="sxs-lookup"><span data-stu-id="da2fe-173">Recurrence triggers</span></span>

<span data-ttu-id="da2fe-174">Uruchamia wyzwalacz cyklu w odstępach czasu, który określisz.</span><span class="sxs-lookup"><span data-stu-id="da2fe-174">A recurrence trigger runs at an interval that you specify.</span></span> <span data-ttu-id="da2fe-175">Wyzwalacz powitania po logikę warunkową wyzwalacza hello Określa, czy hello przepływu pracy musi toorun.</span><span class="sxs-lookup"><span data-stu-id="da2fe-175">When hello trigger has conditional logic, hello trigger determines whether hello workflow needs toorun.</span></span> <span data-ttu-id="da2fe-176">Wyzwalacz wskazuje uruchamiania przepływu pracy hello zwracając `200` kod stanu.</span><span class="sxs-lookup"><span data-stu-id="da2fe-176">A trigger indicates hello workflow should run by returning a `200` status code.</span></span> <span data-ttu-id="da2fe-177">Po hello przepływu pracy nie wymaga toorun, wyzwalacz hello zwraca `202` kod stanu.</span><span class="sxs-lookup"><span data-stu-id="da2fe-177">When hello workflow doesn't need toorun, hello trigger returns a `202` status code.</span></span>

### <a name="callback-using-rest-apis"></a><span data-ttu-id="da2fe-178">Wywołanie zwrotne za pomocą interfejsów API REST</span><span class="sxs-lookup"><span data-stu-id="da2fe-178">Callback using REST APIs</span></span>

<span data-ttu-id="da2fe-179">toostart przepływu pracy, usługi mogą wywoływać punkt końcowy aplikacji logiki.</span><span class="sxs-lookup"><span data-stu-id="da2fe-179">toostart a workflow, services can call a logic app endpoint.</span></span> <span data-ttu-id="da2fe-180">Wybierz ten rodzaj logiki aplikacji na żądanie, toostart **Uruchom teraz** na powitania paska poleceń.</span><span class="sxs-lookup"><span data-stu-id="da2fe-180">toostart this kind of logic app on-demand, choose **Run now** on hello command bar.</span></span> <span data-ttu-id="da2fe-181">Zobacz [uruchomić przepływy pracy, wywołując logiki punkty końcowe aplikacji jako wyzwalacze](../logic-apps/logic-apps-http-endpoint.md).</span><span class="sxs-lookup"><span data-stu-id="da2fe-181">See [Start workflows by calling logic app endpoints as triggers](../logic-apps/logic-apps-http-endpoint.md).</span></span> 

<!-- Shared links -->
[portalu Azure]: https://portal.azure.com

## <a name="next-steps"></a><span data-ttu-id="da2fe-183">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="da2fe-183">Next steps</span></span>

* [<span data-ttu-id="da2fe-184">Instrukcji Switch</span><span class="sxs-lookup"><span data-stu-id="da2fe-184">Switch statements</span></span>](../logic-apps/logic-apps-switch-case.md) 
* [<span data-ttu-id="da2fe-185">Pętle, zakresy i usuwanie partii</span><span class="sxs-lookup"><span data-stu-id="da2fe-185">Loops, scopes, and debatching</span></span>](../logic-apps/logic-apps-loops-and-scopes.md)
* [<span data-ttu-id="da2fe-186">Tworzenie definicji aplikacji logiki</span><span class="sxs-lookup"><span data-stu-id="da2fe-186">Author logic app definitions</span></span>](../logic-apps/logic-apps-author-definitions.md)