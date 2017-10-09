---
title: "Instrukcja aaaSwitch dla różnych akcji w aplikacjach logiki platformy Azure | Dokumentacja firmy Microsoft"
description: "Wybierz tooperform różne akcje w aplikacjach logiki na podstawie wyrażenia wartości przy użyciu instrukcji switch"
services: logic-apps
keywords: "Switch — instrukcja"
author: derek1ee
manager: anneta
editor: 
documentationcenter: 
ms.assetid: 
ms.service: logic-apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 11/18/2016
ms.author: LADocs; deli
ms.openlocfilehash: 09ed7e4a752003aba157e9156bf4dc89ef86f5ad
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="perform-different-actions-in-logic-apps-with-a-switch-statement"></a><span data-ttu-id="77c89-104">Wykonaj różne akcje w aplikacjach logiki z instrukcji switch</span><span class="sxs-lookup"><span data-stu-id="77c89-104">Perform different actions in logic apps with a switch statement</span></span>

<span data-ttu-id="77c89-105">Podczas tworzenia przepływu pracy, często mają różne akcje tootake na podstawie wartości hello obiektu lub wyrażenie.</span><span class="sxs-lookup"><span data-stu-id="77c89-105">When authoring a workflow, you often have tootake different actions based on hello value of an object or expression.</span></span> <span data-ttu-id="77c89-106">Można na przykład z toobehave aplikacji logiki inaczej w zależności od hello kod stanu HTTP żądania lub opcji wybranej w wiadomości e-mail.</span><span class="sxs-lookup"><span data-stu-id="77c89-106">For example, you might want your logic app toobehave differently based on hello status code of an HTTP request, or an option selected in an email.</span></span>

<span data-ttu-id="77c89-107">Można użyć tych scenariuszy tooimplement instrukcji switch.</span><span class="sxs-lookup"><span data-stu-id="77c89-107">You can use a switch statement tooimplement these scenarios.</span></span> <span data-ttu-id="77c89-108">Aplikację logiki można ocenić tokenu lub wyrażenie i wybierz w przypadku hello hello samą powitalnych tooexecute wartość określone akcje.</span><span class="sxs-lookup"><span data-stu-id="77c89-108">Your logic app can evaluate a token or expression, and choose hello case with hello same value tooexecute hello specified actions.</span></span> <span data-ttu-id="77c89-109">Tylko jeden przypadek powinna odpowiadać hello instrukcji switch.</span><span class="sxs-lookup"><span data-stu-id="77c89-109">Only one case should match hello switch statement.</span></span>

> [!TIP]
> <span data-ttu-id="77c89-110">Podobnie jak wszystkie języki programowania instrukcji switch obsługuje tylko operatory równości.</span><span class="sxs-lookup"><span data-stu-id="77c89-110">Like all programming languages, switch statements support only equality operators.</span></span> <span data-ttu-id="77c89-111">Jeśli potrzebujesz innych operatory relacyjne takich jak "większe niż", użyj instrukcji warunku.</span><span class="sxs-lookup"><span data-stu-id="77c89-111">If you need other relational operators, such as "greater than", use a condition statement.</span></span>
> <span data-ttu-id="77c89-112">sposób wykonywania deterministyczne tooensure, przypadków musi zawierać wartość unikatowa i statyczne zamiast tokeny dynamicznych lub wyrażenie.</span><span class="sxs-lookup"><span data-stu-id="77c89-112">tooensure deterministic execution behavior, cases must contain a unique and static value instead of dynamic tokens or expression.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="77c89-113">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="77c89-113">Prerequisites</span></span>

- <span data-ttu-id="77c89-114">Aktywna subskrypcja platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="77c89-114">An active Azure subscription.</span></span> <span data-ttu-id="77c89-115">Jeśli nie masz aktywnych subskrypcji platformy Azure, [utworzyć bezpłatne konto](https://azure.microsoft.com/free/), lub spróbuj [wolne aplikacje logiki dla](https://tryappservice.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="77c89-115">If you don't have an active Azure subscription, [create a free account](https://azure.microsoft.com/free/), or try [Logic Apps for free](https://tryappservice.azure.com/).</span></span>
- [<span data-ttu-id="77c89-116">Podstawową wiedzę na temat dotyczące aplikacji logiki</span><span class="sxs-lookup"><span data-stu-id="77c89-116">Basic knowledge about logic apps</span></span>](logic-apps-what-are-logic-apps.md)

## <a name="add-a-switch-statement-tooyour-workflow"></a><span data-ttu-id="77c89-117">Dodaj przepływ pracy tooyour instrukcji switch</span><span class="sxs-lookup"><span data-stu-id="77c89-117">Add a switch statement tooyour workflow</span></span>

<span data-ttu-id="77c89-118">tooshow działania instrukcji switch, w tym przykładzie tworzy aplikację logiki, że monitory pliki przekazywane tooDropbox.</span><span class="sxs-lookup"><span data-stu-id="77c89-118">tooshow how a switch statement works, this example creates a logic app that monitors files uploaded tooDropbox.</span></span> <span data-ttu-id="77c89-119">Po przekazaniu hello nowe pliki aplikacji logiki hello wysyła osoba zatwierdzająca tooan poczty e-mail, który wybiera czy tootransfer tooSharePoint tych plików.</span><span class="sxs-lookup"><span data-stu-id="77c89-119">When hello new files are uploaded, hello logic app sends email tooan approver who chooses whether tootransfer those files tooSharePoint.</span></span> <span data-ttu-id="77c89-120">Aplikacja Hello używa instrukcji switch, który wykonuje różne akcje na podstawie wartości hello, które hello wybiera osoby zatwierdzającej.</span><span class="sxs-lookup"><span data-stu-id="77c89-120">hello app uses a switch statement that performs different actions based on hello value that hello approver selects.</span></span>

1. <span data-ttu-id="77c89-121">Tworzenie aplikacji logiki, a następnie wybierz tego wyzwalacza: **Dropbox — po utworzeniu pliku**.</span><span class="sxs-lookup"><span data-stu-id="77c89-121">Create a logic app, and select this trigger: **Dropbox - When a file is created**.</span></span>

   ![Użyj usługi Dropbox — podczas tworzenia pliku wyzwalacza](./media/logic-apps-switch-case/dropbox-trigger.jpg)

2. <span data-ttu-id="77c89-123">W obszarze hello wyzwalacza, Dodaj tę akcję: **Outlook.com — wysyłanie wiadomości e-mail zatwierdzania**</span><span class="sxs-lookup"><span data-stu-id="77c89-123">Under hello trigger, add this action: **Outlook.com - Send approval email**</span></span>

   > [!TIP]
   > <span data-ttu-id="77c89-124">Aplikacje logiki obsługują także wysyłania scenariusze wiadomości e-mail zatwierdzania z konta programu Outlook pakietu Office 365.</span><span class="sxs-lookup"><span data-stu-id="77c89-124">Logic apps also support sending approval email scenarios from an Office 365 Outlook account.</span></span>

   - <span data-ttu-id="77c89-125">Jeśli nie masz istniejące połączenie, zostanie wyświetlony monit toocreate jeden.</span><span class="sxs-lookup"><span data-stu-id="77c89-125">If you don't have an existing connection, you're prompted toocreate one.</span></span>
   - <span data-ttu-id="77c89-126">Wypełnij pola hello wymagane.</span><span class="sxs-lookup"><span data-stu-id="77c89-126">Fill in hello required fields.</span></span> <span data-ttu-id="77c89-127">Na przykład w obszarze **do**, określ hello adres e-mail do wysyłania wiadomości e-mail osoby zatwierdzającej hello.</span><span class="sxs-lookup"><span data-stu-id="77c89-127">For example, under **To**, specify hello email address for sending hello approver email.</span></span>
   - <span data-ttu-id="77c89-128">W obszarze **opcji użytkownika**, wprowadź `Approve, Reject`.</span><span class="sxs-lookup"><span data-stu-id="77c89-128">Under **User Options**, enter `Approve, Reject`.</span></span>

   ![Skonfiguruj połączenie](./media/logic-apps-switch-case/send-approval-email-action.jpg)

3. <span data-ttu-id="77c89-130">Dodawanie instrukcji switch.</span><span class="sxs-lookup"><span data-stu-id="77c89-130">Add a switch statement.</span></span>

   - <span data-ttu-id="77c89-131">Wybierz **+ nowy krok** > **... Więcej** > **dodawanie przypadku przełącznika**.</span><span class="sxs-lookup"><span data-stu-id="77c89-131">Select **+ New step** > **... More** > **Add a switch case**.</span></span> 
   - <span data-ttu-id="77c89-132">Teraz chcemy tooperform akcji hello tooselect oparte na powitania `SelectedOptions` dane wyjściowe z hello *wysyłania wiadomości e-mail zatwierdzania* akcji.</span><span class="sxs-lookup"><span data-stu-id="77c89-132">Now we want tooselect hello action tooperform based on hello `SelectedOptions` output from hello *Send approval email* action.</span></span> 
   <span data-ttu-id="77c89-133">W tym polu można znaleźć w hello **dodać zawartość dynamiczną** selektora.</span><span class="sxs-lookup"><span data-stu-id="77c89-133">You can find this field in hello **Add dynamic content** selector.</span></span>
   - <span data-ttu-id="77c89-134">Użyj *przypadek 1* toohandle po wybraniu osoba zatwierdzająca hello `Approve`.</span><span class="sxs-lookup"><span data-stu-id="77c89-134">Use *Case 1* toohandle when hello approver selects `Approve`.</span></span>
     - <span data-ttu-id="77c89-135">Po zatwierdzeniu skopiować hello oryginalnego pliku tooSharePoint Online z hello [ **usługi SharePoint Online — Utwórz plik** akcji](../connectors/connectors-create-api-sharepointonline.md).</span><span class="sxs-lookup"><span data-stu-id="77c89-135">If approved, copy hello original file tooSharePoint Online with hello [**SharePoint Online - Create file** action](../connectors/connectors-create-api-sharepointonline.md).</span></span>
     - <span data-ttu-id="77c89-136">Dodaj inną akcję w hello toonotify wielkość użytkowników, że nowy plik jest dostępny w programie SharePoint.</span><span class="sxs-lookup"><span data-stu-id="77c89-136">Add another action within hello case toonotify users that a new file is available on SharePoint.</span></span>
   - <span data-ttu-id="77c89-137">Dodaj inną wielkość toohandle po wybraniu użytkownika `Reject`.</span><span class="sxs-lookup"><span data-stu-id="77c89-137">Add another case toohandle when user selects `Reject`.</span></span>
     - <span data-ttu-id="77c89-138">W przypadku odrzucenia, Wyślij wiadomość e-mail z powiadomieniem informowania innych osób zatwierdzających hello pliku zostało odrzucone, a nie są wymagane nie dalsze akcje.</span><span class="sxs-lookup"><span data-stu-id="77c89-138">If rejected, send a notification email informing other approvers that hello file is rejected and no further action is required.</span></span>
   - <span data-ttu-id="77c89-139">`SelectedOptions`udostępnia tylko dwie opcje, aby firma Microsoft może narazić hello **domyślne** przypadku puste.</span><span class="sxs-lookup"><span data-stu-id="77c89-139">`SelectedOptions` provides only two options, so we can leave hello **Default** case empty.</span></span>

   ![Switch — instrukcja](./media/logic-apps-switch-case/switch.jpg)

   > [!NOTE]
   > <span data-ttu-id="77c89-141">Instrukcja switch musi mieć co najmniej jeden przypadek w przypadku domyślnej toohello dodanie.</span><span class="sxs-lookup"><span data-stu-id="77c89-141">A switch statement needs at least one case in addition toohello default case.</span></span>

4. <span data-ttu-id="77c89-142">Po instrukcji switch hello, należy usunąć hello oryginalny plik przekazany tooDropbox przez dodanie tej akcji: **Dropbox - Usuń plik**</span><span class="sxs-lookup"><span data-stu-id="77c89-142">After hello switch statement, delete hello original file uploaded tooDropbox by adding this action: **Dropbox - Delete file**</span></span>

5. <span data-ttu-id="77c89-143">Zapisz aplikację logiki.</span><span class="sxs-lookup"><span data-stu-id="77c89-143">Save your logic app.</span></span> <span data-ttu-id="77c89-144">Testowanie aplikacji, przekazując tooDropbox pliku.</span><span class="sxs-lookup"><span data-stu-id="77c89-144">Test your app by uploading a file tooDropbox.</span></span> <span data-ttu-id="77c89-145">Wkrótce otrzymasz wiadomości e-mail zatwierdzania.</span><span class="sxs-lookup"><span data-stu-id="77c89-145">You should receive an approval email shortly.</span></span> <span data-ttu-id="77c89-146">Wybierz opcję i sprawdź hello zachowanie.</span><span class="sxs-lookup"><span data-stu-id="77c89-146">Select an option, and observe hello behavior.</span></span>

   > [!TIP]
   > <span data-ttu-id="77c89-147">Sprawdź, jak za[Monitoruj aplikacje logiki](logic-apps-monitor-your-logic-apps.md).</span><span class="sxs-lookup"><span data-stu-id="77c89-147">Check out how too[monitor your logic apps](logic-apps-monitor-your-logic-apps.md).</span></span>

## <a name="understand-hello-code-behind-switch-statements"></a><span data-ttu-id="77c89-148">Zrozumienie hello kodzie instrukcji switch</span><span class="sxs-lookup"><span data-stu-id="77c89-148">Understand hello code behind switch statements</span></span>

<span data-ttu-id="77c89-149">Teraz, że pomyślnie utworzono aplikację logiki, za pomocą instrukcji switch, Przyjrzyjmy się definicji kodu hello hello instrukcji switch.</span><span class="sxs-lookup"><span data-stu-id="77c89-149">Now that you successfully created a logic app using a switch statement, let's look at hello code definition behind hello switch statement.</span></span>

```json
"Switch": {
    "type": "Switch",
    "expression": "@body('Send_approval_email')?['SelectedOption']",
    "cases": {
        "Case 1" : {
            "case" : "Approved",
            "actions" : {}
        },
        "Case 2" : {
            "case" : "Rejected",
            "actions" : {}
        }
    },
    "default": {
        "actions": {}
    },
    "runAfter": {
        "Send_approval_email": [
            "Succeeded"
        ]
    }
}
```

* <span data-ttu-id="77c89-150">`"Switch"`to nazwa hello instrukcji switch hello, które można zmienić nazwy dla czytelności.</span><span class="sxs-lookup"><span data-stu-id="77c89-150">`"Switch"` is hello name of hello switch statement, which you can rename for readability.</span></span> 
* <span data-ttu-id="77c89-151">`"type": "Switch"`Wskazuje, że akcja hello jest instrukcji switch.</span><span class="sxs-lookup"><span data-stu-id="77c89-151">`"type": "Switch"` indicates that hello action is a switch statement.</span></span> 
* <span data-ttu-id="77c89-152">`"expression"`jest osoby zatwierdzającej hello wybranej opcji, w tym przykładzie i zostaną ocenione względem każdego przypadku zadeklarowany w dalszej części hello definicji.</span><span class="sxs-lookup"><span data-stu-id="77c89-152">`"expression"` is hello approver's selected option in this example and is evaluated against each case declared later in hello definition.</span></span> 
* <span data-ttu-id="77c89-153">`"cases"`może zawierać dowolną liczbę przypadków.</span><span class="sxs-lookup"><span data-stu-id="77c89-153">`"cases"` can contain any number of cases.</span></span> <span data-ttu-id="77c89-154">W przypadku każdego `"Case *"` jest hello domyślną nazwę przypadku hello, który można zmienić nazwy dla czytelności.</span><span class="sxs-lookup"><span data-stu-id="77c89-154">For each case, `"Case *"` is hello default name of hello case, which you can rename for readability.</span></span> 
<span data-ttu-id="77c89-155">`"case"`Określa etykiety case hello, hello używa wyrażenia switch do porównania, a musi być wartością stałą i unikatowe.</span><span class="sxs-lookup"><span data-stu-id="77c89-155">`"case"` specifies hello case label, which hello switch expression uses for comparison, and must be a constant and unique value.</span></span> <span data-ttu-id="77c89-156">Jeśli żadna z przypadków hello nie zgadza wyrażenie switch hello, akcje w ramach `"default"` są wykonywane.</span><span class="sxs-lookup"><span data-stu-id="77c89-156">If none of hello cases match hello switch expression, actions under `"default"` are executed.</span></span>

## <a name="get-help"></a><span data-ttu-id="77c89-157">Uzyskiwanie pomocy</span><span class="sxs-lookup"><span data-stu-id="77c89-157">Get help</span></span>

<span data-ttu-id="77c89-158">pytania tooask, odpowiadanie na pytania i robią innych użytkowników usługi Azure Logic Apps, zobacz odwiedź hello [forum usługi Azure Logic Apps](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurelogicapps).</span><span class="sxs-lookup"><span data-stu-id="77c89-158">tooask questions, answer questions, and see what other Azure Logic Apps users are doing, visit hello [Azure Logic Apps forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurelogicapps).</span></span>

<span data-ttu-id="77c89-159">toohelp poprawy usługi Azure Logic Apps i łącznikami, Zagłosuj lub Prześlij pomysłów na powitania [witrynę opinii użytkowników usługi Azure Logic Apps](http://aka.ms/logicapps-wish).</span><span class="sxs-lookup"><span data-stu-id="77c89-159">toohelp improve Azure Logic Apps and connectors, vote on or submit ideas at hello [Azure Logic Apps user feedback site](http://aka.ms/logicapps-wish).</span></span>

## <a name="next-steps"></a><span data-ttu-id="77c89-160">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="77c89-160">Next steps</span></span>

- <span data-ttu-id="77c89-161">Dowiedz się, jak za[Dodawanie warunków](logic-apps-use-logic-app-features.md)</span><span class="sxs-lookup"><span data-stu-id="77c89-161">Learn how too[add conditions](logic-apps-use-logic-app-features.md)</span></span>
- <span data-ttu-id="77c89-162">Dowiedz się więcej o [błąd i obsługa wyjątków](logic-apps-exception-handling.md)</span><span class="sxs-lookup"><span data-stu-id="77c89-162">Learn about [error and exception handling](logic-apps-exception-handling.md)</span></span>
- <span data-ttu-id="77c89-163">Poznaj więcej [obsługi language przepływu pracy](logic-apps-author-definitions.md)</span><span class="sxs-lookup"><span data-stu-id="77c89-163">Explore more [workflow language capabilities](logic-apps-author-definitions.md)</span></span>