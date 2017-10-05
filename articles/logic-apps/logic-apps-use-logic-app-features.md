---
title: "Dodawanie warunków i uruchomić przepływ pracy - Azure Logic Apps | Dokumentacja firmy Microsoft"
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
ms.openlocfilehash: e632c48ed31e82536db55a9c54438bece0c38fd4
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="use-logic-apps-features"></a><span data-ttu-id="42e29-103">Korzystanie z funkcji Logic Apps</span><span class="sxs-lookup"><span data-stu-id="42e29-103">Use Logic Apps features</span></span>

<span data-ttu-id="42e29-104">W [poprzedniego tematu](../logic-apps/logic-apps-create-a-logic-app.md), utworzyć pierwszą aplikację logiki.</span><span class="sxs-lookup"><span data-stu-id="42e29-104">In a [previous topic](../logic-apps/logic-apps-create-a-logic-app.md), you created your first logic app.</span></span> <span data-ttu-id="42e29-105">Aby kontrolować przepływu pracy aplikacji logiki, można określić różne ścieżki dla aplikacji logiki do uruchomienia i sposobu przetwarzania danych w macierzy, kolekcji i partie.</span><span class="sxs-lookup"><span data-stu-id="42e29-105">To control your logic app's workflow, you can specify different paths for your logic app to run and how to process data in arrays, collections, and batches.</span></span> <span data-ttu-id="42e29-106">W przepływie pracy aplikacji logiki można uwzględnić następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="42e29-106">You can include these elements in your logic app workflow:</span></span>

* <span data-ttu-id="42e29-107">Warunki i [przełącznika instrukcje](../logic-apps/logic-apps-switch-case.md) let aplikację logiki, uruchom różnych akcji w oparciu o Określa, czy zostały spełnione określone warunki.</span><span class="sxs-lookup"><span data-stu-id="42e29-107">Conditions and [switch statements](../logic-apps/logic-apps-switch-case.md) let your logic app run different actions based on whether specific conditions are met.</span></span>

* <span data-ttu-id="42e29-108">[Pętle](../logic-apps/logic-apps-loops-and-scopes.md) let aplikację logiki cyklicznie uruchamiany kroki.</span><span class="sxs-lookup"><span data-stu-id="42e29-108">[Loops](../logic-apps/logic-apps-loops-and-scopes.md) let your logic app run steps repeatedly.</span></span> <span data-ttu-id="42e29-109">Na przykład można powtórzyć akcje dotyczące tablicy korzystając z **For_each** pętli.</span><span class="sxs-lookup"><span data-stu-id="42e29-109">For example, you can repeat actions over an array when you use a **For_each** loop.</span></span> <span data-ttu-id="42e29-110">Lub akcji można powtórzyć, dopóki spełniony jest warunek, korzystając z **do momentu** pętli.</span><span class="sxs-lookup"><span data-stu-id="42e29-110">Or you can repeat actions until a condition is met when you use an **Until** loop.</span></span>

* <span data-ttu-id="42e29-111">[Zakresy](../logic-apps/logic-apps-loops-and-scopes.md) let uruchamianym serii akcji, na przykład, aby zaimplementować obsługi wyjątków.</span><span class="sxs-lookup"><span data-stu-id="42e29-111">[Scopes](../logic-apps/logic-apps-loops-and-scopes.md) let you group series of actions together, for example, to implement exception handling.</span></span>

* <span data-ttu-id="42e29-112">[Debatching](../logic-apps/logic-apps-loops-and-scopes.md) pozwala uruchomić oddzielne przepływy pracy dla elementów w tablicy, korzystając z aplikacji logiki **SplitOn** polecenia.</span><span class="sxs-lookup"><span data-stu-id="42e29-112">[Debatching](../logic-apps/logic-apps-loops-and-scopes.md) lets your logic app start separate workflows for items in an array when you use the **SplitOn** command.</span></span>

<span data-ttu-id="42e29-113">W tym temacie przedstawiono inne pojęć dotyczących tworzenia aplikacji logiki:</span><span class="sxs-lookup"><span data-stu-id="42e29-113">This topic introduces other concepts for building your logic app:</span></span>

* <span data-ttu-id="42e29-114">Kod widoku do edycji istniejących aplikacji logiki</span><span class="sxs-lookup"><span data-stu-id="42e29-114">Code view to edit an existing logic app</span></span>
* <span data-ttu-id="42e29-115">Opcje uruchamiania przepływu pracy</span><span class="sxs-lookup"><span data-stu-id="42e29-115">Options for starting a workflow</span></span>

## <a name="conditions-run-steps-only-after-meeting-a-condition"></a><span data-ttu-id="42e29-116">Warunki: Uruchamianie kroków tylko po spełniających warunek</span><span class="sxs-lookup"><span data-stu-id="42e29-116">Conditions: Run steps only after meeting a condition</span></span>

<span data-ttu-id="42e29-117">Aby aplikację logiki, uruchom kroki tylko wtedy, gdy dane spełniają określone kryteria, można dodać warunek, który porównuje dane w przepływie pracy przed określonych pól lub wartości.</span><span class="sxs-lookup"><span data-stu-id="42e29-117">To have your logic app run steps only when data meets specific criteria, you can add a condition that compares data in the workflow against specific fields or values.</span></span>

<span data-ttu-id="42e29-118">Na przykład załóżmy, że masz aplikację logiki, która wysyła zbyt dużo żądań wiadomości e-mail Posty na kanału informacyjnego RSS witryny sieci Web.</span><span class="sxs-lookup"><span data-stu-id="42e29-118">For example, suppose you have a logic app that sends you too many emails for posts on a website's RSS feed.</span></span> <span data-ttu-id="42e29-119">Tak, aby aplikację logiki wysyła wiadomości e-mail, tylko wtedy, gdy nowy wpis należy do jednej konkretnej kategorii można dodać warunek.</span><span class="sxs-lookup"><span data-stu-id="42e29-119">You can add a condition so that your logic app sends email only when the new post belongs to a specific category.</span></span>

1. <span data-ttu-id="42e29-120">W [portalu Azure](https://portal.azure.com), znajdowanie i otwieranie aplikacji logiki w Projektancie aplikacji logiki.</span><span class="sxs-lookup"><span data-stu-id="42e29-120">In the [Azure portal](https://portal.azure.com), find and open your logic app in Logic App Designer.</span></span>

2. <span data-ttu-id="42e29-121">Dodaj warunek do dowolnej lokalizacji przepływu pracy.</span><span class="sxs-lookup"><span data-stu-id="42e29-121">Add a condition to the workflow location that you want.</span></span> 

   <span data-ttu-id="42e29-122">Aby dodać warunek między krokami istniejących w przepływie pracy aplikacji logiki, wskaźnika na strzałkę której chcesz dodać warunek.</span><span class="sxs-lookup"><span data-stu-id="42e29-122">To add the condition between existing steps in the logic app workflow, move the pointer over the arrow where you want to add the condition.</span></span> 
   <span data-ttu-id="42e29-123">Wybierz **znak plus** (**+**), a następnie wybierz **Dodaj warunek**.</span><span class="sxs-lookup"><span data-stu-id="42e29-123">Choose the **plus sign** (**+**), then choose **Add a condition**.</span></span> <span data-ttu-id="42e29-124">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="42e29-124">For example:</span></span>

   ![Dodaj warunek do aplikacji logiki](./media/logic-apps-use-logic-app-features/add-condition.png)

   > [!NOTE]
   > <span data-ttu-id="42e29-126">Jeśli chcesz dodać warunek na koniec bieżącego przepływu pracy, przejdź do dolnej części aplikacji logiki i wybierz **+ nowy krok**.</span><span class="sxs-lookup"><span data-stu-id="42e29-126">If you want to add a condition at the end of your current workflow, go to the bottom of your logic app, and choose **+ New step**.</span></span>

3. <span data-ttu-id="42e29-127">Teraz można określić warunku.</span><span class="sxs-lookup"><span data-stu-id="42e29-127">Now define the condition.</span></span> <span data-ttu-id="42e29-128">Określ pola źródłowego, który chcesz ocenić, operacji do wykonania i wartość docelowa lub pola.</span><span class="sxs-lookup"><span data-stu-id="42e29-128">Specify the source field that you want to evaluate, the operation to perform, and the target value or field.</span></span> <span data-ttu-id="42e29-129">Aby dodać warunek istniejących pól, wybierz z **listy zawartości dynamicznej Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="42e29-129">To add existing fields to your condition, choose from the **Add dynamic content list**.</span></span>

   <span data-ttu-id="42e29-130">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="42e29-130">For example:</span></span>

   ![Edytuj warunek w trybie podstawowym](./media/logic-apps-use-logic-app-features/edit-condition-basic-mode.png)

   <span data-ttu-id="42e29-132">Oto pełny warunek:</span><span class="sxs-lookup"><span data-stu-id="42e29-132">Here's the complete condition:</span></span>

   ![Pełny warunek](./media/logic-apps-use-logic-app-features/edit-condition-basic-mode-2.png)

   > [!TIP]
   > <span data-ttu-id="42e29-134">Aby zdefiniować warunku w kodzie, wybierz **edytowanie w trybie zaawansowanym**.</span><span class="sxs-lookup"><span data-stu-id="42e29-134">To define the condition in code, choose **Edit in advanced mode**.</span></span> <span data-ttu-id="42e29-135">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="42e29-135">For example:</span></span>
   > 
   > ![Edytuj warunek w kodzie](./media/logic-apps-use-logic-app-features/edit-condition-advanced-mode.png)

4. <span data-ttu-id="42e29-137">W obszarze **tak, jeśli** i **nr IF**, dodaj kroki do wykonania oparte na Określa, czy warunek jest spełniony.</span><span class="sxs-lookup"><span data-stu-id="42e29-137">Under **IF YES** and **IF NO**, add the steps to perform based on whether the condition is met.</span></span>

   <span data-ttu-id="42e29-138">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="42e29-138">For example:</span></span>

   ![Stan tak i ścieżek](./media/logic-apps-use-logic-app-features/condition-yes-no-path.png)

   > [!TIP]
   > <span data-ttu-id="42e29-140">Możesz przeciągnąć istniejących działań do **tak, jeśli** i **nr IF** ścieżki.</span><span class="sxs-lookup"><span data-stu-id="42e29-140">You can drag existing actions into the **IF YES** and **IF NO** paths.</span></span>

5. <span data-ttu-id="42e29-141">Gdy wszystko będzie gotowe, Zapisz aplikację logiki.</span><span class="sxs-lookup"><span data-stu-id="42e29-141">When you're done, save your logic app.</span></span>

<span data-ttu-id="42e29-142">Teraz możesz otrzymywać wiadomości e-mail, tylko wtedy, gdy wpisów spełnienia warunku.</span><span class="sxs-lookup"><span data-stu-id="42e29-142">Now you get emails only when the posts meet your condition.</span></span>

## <a name="repeat-actions-over-a-list-with-foreach"></a><span data-ttu-id="42e29-143">Powtórz akcje listy za pomocą instrukcji forEach</span><span class="sxs-lookup"><span data-stu-id="42e29-143">Repeat actions over a list with forEach</span></span>

<span data-ttu-id="42e29-144">Pętli forEach Określa tablicę powtórzenie akcji za pośrednictwem.</span><span class="sxs-lookup"><span data-stu-id="42e29-144">The forEach loop specifies an array to repeat an action over.</span></span> <span data-ttu-id="42e29-145">Jeśli nie jest tablicą, przepływ zakończy się niepowodzeniem.</span><span class="sxs-lookup"><span data-stu-id="42e29-145">If it is not an array, the flow fails.</span></span> <span data-ttu-id="42e29-146">Na przykład jeśli masz action1, który generuje tablicę komunikatów i chcesz wysłać wiadomości, można uwzględnić tej instrukcji forEach we właściwościach akcji:`forEach : "@action('action1').outputs.messages"`</span><span class="sxs-lookup"><span data-stu-id="42e29-146">For example, if you have action1 that outputs an array of messages, and you want to send each message, you can include this forEach statement in the properties of your action: `forEach : "@action('action1').outputs.messages"`</span></span>

## <a name="edit-the-code-definition-for-a-logic-app"></a><span data-ttu-id="42e29-147">Edytowanie definicji kodu dla aplikacji logiki</span><span class="sxs-lookup"><span data-stu-id="42e29-147">Edit the code definition for a logic app</span></span>

<span data-ttu-id="42e29-148">Mimo że Projektant aplikacji logiki, można bezpośrednio edytować kod, który definiuje aplikacji logiki.</span><span class="sxs-lookup"><span data-stu-id="42e29-148">Although you have the Logic App Designer, you can directly edit the code that defines a logic app.</span></span>

1. <span data-ttu-id="42e29-149">Na pasku poleceń Wybierz **widok Kod**.</span><span class="sxs-lookup"><span data-stu-id="42e29-149">On the command bar, choose **Code view**.</span></span>

    <span data-ttu-id="42e29-150">Pełna Edytor otwiera się i przedstawiono definicję edytowanej.</span><span class="sxs-lookup"><span data-stu-id="42e29-150">A full editor opens and shows the definition you edited.</span></span>

    ![Widok kodu](media/logic-apps-use-logic-app-features/codeview.png)

    <span data-ttu-id="42e29-152">W edytorze tekstu można skopiuj i Wklej dowolną liczbę akcji w obrębie tej samej aplikacji logiki lub między aplikacji logiki.</span><span class="sxs-lookup"><span data-stu-id="42e29-152">In the text editor, you can copy and paste any number of actions within the same logic app or between logic apps.</span></span> 
    <span data-ttu-id="42e29-153">Można również łatwo Dodaj lub Usuń całą sekcję z definicji i definicji mogą również współużytkować z innymi osobami.</span><span class="sxs-lookup"><span data-stu-id="42e29-153">You can also easily add or remove entire sections from the definition, and you can also share definitions with others.</span></span>

2. <span data-ttu-id="42e29-154">Aby zapisać zmiany, wybierz **zapisać**.</span><span class="sxs-lookup"><span data-stu-id="42e29-154">To save your edits, choose **Save**.</span></span>

## <a name="parameters"></a><span data-ttu-id="42e29-155">Parametry</span><span class="sxs-lookup"><span data-stu-id="42e29-155">Parameters</span></span>

<span data-ttu-id="42e29-156">Niektóre z funkcji Logic Apps są dostępne tylko w widoku kodu, na przykład parametry.</span><span class="sxs-lookup"><span data-stu-id="42e29-156">Some Logic Apps capabilities are available only in code view, for example, parameters.</span></span> <span data-ttu-id="42e29-157">Parametry ułatwiają ponowne użycie wartości w całej aplikacji logiki.</span><span class="sxs-lookup"><span data-stu-id="42e29-157">Parameters make it easy to reuse values throughout your logic app.</span></span> <span data-ttu-id="42e29-158">Na przykład jeśli masz adres e-mail, która ma zostać użyta w kilka akcji, należy zdefiniować tego adresu e-mail jako parametr.</span><span class="sxs-lookup"><span data-stu-id="42e29-158">For example, if you have an email address that you want use in several actions, you should define that email address as a parameter.</span></span>

<span data-ttu-id="42e29-159">Parametry są odpowiednie w ściąganie wartości, które mogą znacznie zmieniają.</span><span class="sxs-lookup"><span data-stu-id="42e29-159">Parameters are good for pulling out values that you are likely to change a lot.</span></span> <span data-ttu-id="42e29-160">Są szczególnie przydatne, gdy należy zastąpić parametry w różnych środowiskach.</span><span class="sxs-lookup"><span data-stu-id="42e29-160">They are especially useful when you need to override parameters in different environments.</span></span> <span data-ttu-id="42e29-161">Aby dowiedzieć się, jak zastąpić parametry opartych na środowisku, zobacz [Tworzenie definicji aplikacji logiki](../logic-apps/logic-apps-author-definitions.md) i [dokumentacja interfejsu API REST](https://docs.microsoft.com/rest/api/logic).</span><span class="sxs-lookup"><span data-stu-id="42e29-161">To learn how to override parameters based on environment, see [Author logic app definitions](../logic-apps/logic-apps-author-definitions.md) and [REST API documentation](https://docs.microsoft.com/rest/api/logic).</span></span>

<span data-ttu-id="42e29-162">Ten przykład przedstawia sposób aktualizacji istniejących aplikacji logiki, dzięki czemu można używać parametrów dla wyszukiwanego terminu.</span><span class="sxs-lookup"><span data-stu-id="42e29-162">This example shows how to update your existing logic app so that you can use parameters for the query term.</span></span>

1. <span data-ttu-id="42e29-163">W widoku kodu, Znajdź `parameters : {}` obiekt, a następnie dodaj `currentFeedUrl` obiektu:</span><span class="sxs-lookup"><span data-stu-id="42e29-163">In code view, find the `parameters : {}` object, and add a `currentFeedUrl` object:</span></span>

        "currentFeedUrl" : {
            "type" : "string",
            "defaultValue" : "http://rss.cnn.com/rss/cnn_topstories.rss"
        }

2. <span data-ttu-id="42e29-164">Przejdź do `When_a_feed-item_is_published` akcji, Znajdź `queries` sekcji, a wartość kwerendy:`"feedUrl": "#@{parameters('currentFeedUrl')}"`</span><span class="sxs-lookup"><span data-stu-id="42e29-164">Go to the `When_a_feed-item_is_published` action, find the `queries` section, and replace the query value with : `"feedUrl": "#@{parameters('currentFeedUrl')}"`</span></span> 

    <span data-ttu-id="42e29-165">Aby przyłączyć się co najmniej dwa ciągi, umożliwia także `concat` funkcji.</span><span class="sxs-lookup"><span data-stu-id="42e29-165">To join two or more strings, you can also use the `concat` function.</span></span> 
    <span data-ttu-id="42e29-166">Na przykład `"@concat('#',parameters('currentFeedUrl'))"` działa tak samo jak powyżej.</span><span class="sxs-lookup"><span data-stu-id="42e29-166">For example, `"@concat('#',parameters('currentFeedUrl'))"` works the same as the above.</span></span>

3.  <span data-ttu-id="42e29-167">Gdy wszystko będzie gotowe, wybierz pozycję **zapisać**.</span><span class="sxs-lookup"><span data-stu-id="42e29-167">When you're done, choose **Save**.</span></span> 

    <span data-ttu-id="42e29-168">Teraz możesz zmienić danych RSS witryny sieci Web przez przekazanie do innego adresu URL za pośrednictwem `currentFeedURL` obiektu.</span><span class="sxs-lookup"><span data-stu-id="42e29-168">Now you can change the website's RSS feed by passing a different URL through the `currentFeedURL` object.</span></span>

<span data-ttu-id="42e29-169">Dowiedz się więcej o [sposobu tworzenia definicji aplikacji logiki](../logic-apps/logic-apps-author-definitions.md).</span><span class="sxs-lookup"><span data-stu-id="42e29-169">Learn more about [how to author logic app definitions](../logic-apps/logic-apps-author-definitions.md).</span></span>

## <a name="start-logic-app-workflows"></a><span data-ttu-id="42e29-170">Uruchomić przepływy pracy aplikacji logiki</span><span class="sxs-lookup"><span data-stu-id="42e29-170">Start logic app workflows</span></span>

<span data-ttu-id="42e29-171">Masz różne opcje uruchamiania przepływu pracy zdefiniowanych w aplikacji logiki.</span><span class="sxs-lookup"><span data-stu-id="42e29-171">You have different options for starting the workflow defined in your logic app.</span></span> <span data-ttu-id="42e29-172">Zawsze można uruchomić przepływu pracy na żądanie w [portalu Azure].</span><span class="sxs-lookup"><span data-stu-id="42e29-172">You can always start a workflow on-demand in the [Azure portal].</span></span>

### <a name="recurrence-triggers"></a><span data-ttu-id="42e29-173">Wyzwalacze cyklu</span><span class="sxs-lookup"><span data-stu-id="42e29-173">Recurrence triggers</span></span>

<span data-ttu-id="42e29-174">Uruchamia wyzwalacz cyklu w odstępach czasu, który określisz.</span><span class="sxs-lookup"><span data-stu-id="42e29-174">A recurrence trigger runs at an interval that you specify.</span></span> <span data-ttu-id="42e29-175">Jeśli wyzwalacz logikę warunkową, wyzwalacz Określa, czy przepływ pracy musi być uruchamiane.</span><span class="sxs-lookup"><span data-stu-id="42e29-175">When the trigger has conditional logic, the trigger determines whether the workflow needs to run.</span></span> <span data-ttu-id="42e29-176">Wskazuje wyzwalacz przepływu pracy powinno być ono uruchomione przez zwrócenie `200` kod stanu.</span><span class="sxs-lookup"><span data-stu-id="42e29-176">A trigger indicates the workflow should run by returning a `200` status code.</span></span> <span data-ttu-id="42e29-177">Gdy przepływ pracy nie trzeba uruchamiać, wyzwalacz zwraca `202` kod stanu.</span><span class="sxs-lookup"><span data-stu-id="42e29-177">When the workflow doesn't need to run, the trigger returns a `202` status code.</span></span>

### <a name="callback-using-rest-apis"></a><span data-ttu-id="42e29-178">Wywołanie zwrotne za pomocą interfejsów API REST</span><span class="sxs-lookup"><span data-stu-id="42e29-178">Callback using REST APIs</span></span>

<span data-ttu-id="42e29-179">Aby uruchomić przepływ pracy, usługi mogą wywoływać punkt końcowy aplikacji logiki.</span><span class="sxs-lookup"><span data-stu-id="42e29-179">To start a workflow, services can call a logic app endpoint.</span></span> <span data-ttu-id="42e29-180">Aby uruchomić ten rodzaj logiki aplikacji na żądanie, wybierz **Uruchom teraz** na pasku poleceń.</span><span class="sxs-lookup"><span data-stu-id="42e29-180">To start this kind of logic app on-demand, choose **Run now** on the command bar.</span></span> <span data-ttu-id="42e29-181">Zobacz [uruchomić przepływy pracy, wywołując logiki punkty końcowe aplikacji jako wyzwalacze](../logic-apps/logic-apps-http-endpoint.md).</span><span class="sxs-lookup"><span data-stu-id="42e29-181">See [Start workflows by calling logic app endpoints as triggers](../logic-apps/logic-apps-http-endpoint.md).</span></span> 

<!-- Shared links -->
<span data-ttu-id="42e29-182">[portalu Azure]: https://portal.azure.com</span><span class="sxs-lookup"><span data-stu-id="42e29-182">[Azure portal]: https://portal.azure.com</span></span>

## <a name="next-steps"></a><span data-ttu-id="42e29-183">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="42e29-183">Next steps</span></span>

* [<span data-ttu-id="42e29-184">Instrukcji Switch</span><span class="sxs-lookup"><span data-stu-id="42e29-184">Switch statements</span></span>](../logic-apps/logic-apps-switch-case.md) 
* [<span data-ttu-id="42e29-185">Pętle, zakresy i usuwanie partii</span><span class="sxs-lookup"><span data-stu-id="42e29-185">Loops, scopes, and debatching</span></span>](../logic-apps/logic-apps-loops-and-scopes.md)
* [<span data-ttu-id="42e29-186">Tworzenie definicji aplikacji logiki</span><span class="sxs-lookup"><span data-stu-id="42e29-186">Author logic app definitions</span></span>](../logic-apps/logic-apps-author-definitions.md)