---
title: "Switch — instrukcja dla różnych akcji w aplikacjach logiki platformy Azure | Dokumentacja firmy Microsoft"
description: "Wybierz różne akcje do wykonania w aplikacjach logiki na podstawie wyrażenia wartości przy użyciu instrukcji switch"
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
ms.openlocfilehash: 338b6a5b549d7bf81186550295608438ac4aee32
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="perform-different-actions-in-logic-apps-with-a-switch-statement"></a><span data-ttu-id="3583e-104">Wykonaj różne akcje w aplikacjach logiki z instrukcji switch</span><span class="sxs-lookup"><span data-stu-id="3583e-104">Perform different actions in logic apps with a switch statement</span></span>

<span data-ttu-id="3583e-105">Podczas tworzenia przepływu pracy, często trzeba wykonywać różne akcje na podstawie wartości obiektu lub wyrażenie.</span><span class="sxs-lookup"><span data-stu-id="3583e-105">When authoring a workflow, you often have to take different actions based on the value of an object or expression.</span></span> <span data-ttu-id="3583e-106">Na przykład można aplikację logiki zachowuje się inaczej w zależności od kodu stanu żądania HTTP lub opcji wybranej w wiadomości e-mail.</span><span class="sxs-lookup"><span data-stu-id="3583e-106">For example, you might want your logic app to behave differently based on the status code of an HTTP request, or an option selected in an email.</span></span>

<span data-ttu-id="3583e-107">Instrukcja switch służy do wdrożenia tych scenariuszy.</span><span class="sxs-lookup"><span data-stu-id="3583e-107">You can use a switch statement to implement these scenarios.</span></span> <span data-ttu-id="3583e-108">Aplikację logiki można ocenić tokenu lub wyrażenie i wybrać sprawę z taką samą wartość do wykonywania określonych akcji.</span><span class="sxs-lookup"><span data-stu-id="3583e-108">Your logic app can evaluate a token or expression, and choose the case with the same value to execute the specified actions.</span></span> <span data-ttu-id="3583e-109">Tylko jeden przypadek powinna odpowiadać instrukcji switch.</span><span class="sxs-lookup"><span data-stu-id="3583e-109">Only one case should match the switch statement.</span></span>

> [!TIP]
> <span data-ttu-id="3583e-110">Podobnie jak wszystkie języki programowania instrukcji switch obsługuje tylko operatory równości.</span><span class="sxs-lookup"><span data-stu-id="3583e-110">Like all programming languages, switch statements support only equality operators.</span></span> <span data-ttu-id="3583e-111">Jeśli potrzebujesz innych operatory relacyjne takich jak "większe niż", użyj instrukcji warunku.</span><span class="sxs-lookup"><span data-stu-id="3583e-111">If you need other relational operators, such as "greater than", use a condition statement.</span></span>
> <span data-ttu-id="3583e-112">W celu zapewnienia sposób wykonywania deterministyczna, przypadków musi zawierać wartość unikatowa i statyczne zamiast tokeny dynamicznych lub wyrażenie.</span><span class="sxs-lookup"><span data-stu-id="3583e-112">To ensure deterministic execution behavior, cases must contain a unique and static value instead of dynamic tokens or expression.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="3583e-113">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="3583e-113">Prerequisites</span></span>

- <span data-ttu-id="3583e-114">Aktywna subskrypcja platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="3583e-114">An active Azure subscription.</span></span> <span data-ttu-id="3583e-115">Jeśli nie masz aktywnych subskrypcji platformy Azure, [utworzyć bezpłatne konto](https://azure.microsoft.com/free/), lub spróbuj [wolne aplikacje logiki dla](https://tryappservice.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="3583e-115">If you don't have an active Azure subscription, [create a free account](https://azure.microsoft.com/free/), or try [Logic Apps for free](https://tryappservice.azure.com/).</span></span>
- [<span data-ttu-id="3583e-116">Podstawową wiedzę na temat dotyczące aplikacji logiki</span><span class="sxs-lookup"><span data-stu-id="3583e-116">Basic knowledge about logic apps</span></span>](logic-apps-what-are-logic-apps.md)

## <a name="add-a-switch-statement-to-your-workflow"></a><span data-ttu-id="3583e-117">Dodawanie instrukcji switch do przepływu pracy</span><span class="sxs-lookup"><span data-stu-id="3583e-117">Add a switch statement to your workflow</span></span>

<span data-ttu-id="3583e-118">Aby pokazać, jak działa instrukcji switch, w tym przykładzie jest tworzony aplikacji logiki, który monitoruje plików przekazanych do skrzynki.</span><span class="sxs-lookup"><span data-stu-id="3583e-118">To show how a switch statement works, this example creates a logic app that monitors files uploaded to Dropbox.</span></span> <span data-ttu-id="3583e-119">Po przekazaniu nowe pliki aplikacji logiki wysyła wiadomości e-mail do osoby zatwierdzającej, który wybiera, czy do przesyłania tych plików w programie SharePoint.</span><span class="sxs-lookup"><span data-stu-id="3583e-119">When the new files are uploaded, the logic app sends email to an approver who chooses whether to transfer those files to SharePoint.</span></span> <span data-ttu-id="3583e-120">Aplikacja używa instrukcji switch, który wykonuje różne akcje na podstawie wartości, który wybiera osoby zatwierdzającej.</span><span class="sxs-lookup"><span data-stu-id="3583e-120">The app uses a switch statement that performs different actions based on the value that the approver selects.</span></span>

1. <span data-ttu-id="3583e-121">Tworzenie aplikacji logiki, a następnie wybierz tego wyzwalacza: **Dropbox — po utworzeniu pliku**.</span><span class="sxs-lookup"><span data-stu-id="3583e-121">Create a logic app, and select this trigger: **Dropbox - When a file is created**.</span></span>

   ![Użyj usługi Dropbox — podczas tworzenia pliku wyzwalacza](./media/logic-apps-switch-case/dropbox-trigger.jpg)

2. <span data-ttu-id="3583e-123">W obszarze wyzwalacza, Dodaj tę akcję: **Outlook.com — wysyłanie wiadomości e-mail zatwierdzania**</span><span class="sxs-lookup"><span data-stu-id="3583e-123">Under the trigger, add this action: **Outlook.com - Send approval email**</span></span>

   > [!TIP]
   > <span data-ttu-id="3583e-124">Aplikacje logiki obsługują także wysyłania scenariusze wiadomości e-mail zatwierdzania z konta programu Outlook pakietu Office 365.</span><span class="sxs-lookup"><span data-stu-id="3583e-124">Logic apps also support sending approval email scenarios from an Office 365 Outlook account.</span></span>

   - <span data-ttu-id="3583e-125">Jeśli nie masz istniejące połączenie, zostanie wyświetlony monit o utworzenie.</span><span class="sxs-lookup"><span data-stu-id="3583e-125">If you don't have an existing connection, you're prompted to create one.</span></span>
   - <span data-ttu-id="3583e-126">Wypełnij wymagane pola.</span><span class="sxs-lookup"><span data-stu-id="3583e-126">Fill in the required fields.</span></span> <span data-ttu-id="3583e-127">Na przykład w obszarze **do**, określ adres e-mail do wysyłania wiadomości e-mail osoby zatwierdzającej.</span><span class="sxs-lookup"><span data-stu-id="3583e-127">For example, under **To**, specify the email address for sending the approver email.</span></span>
   - <span data-ttu-id="3583e-128">W obszarze **opcji użytkownika**, wprowadź `Approve, Reject`.</span><span class="sxs-lookup"><span data-stu-id="3583e-128">Under **User Options**, enter `Approve, Reject`.</span></span>

   ![Skonfiguruj połączenie](./media/logic-apps-switch-case/send-approval-email-action.jpg)

3. <span data-ttu-id="3583e-130">Dodawanie instrukcji switch.</span><span class="sxs-lookup"><span data-stu-id="3583e-130">Add a switch statement.</span></span>

   - <span data-ttu-id="3583e-131">Wybierz **+ nowy krok** > **... Więcej** > **dodawanie przypadku przełącznika**.</span><span class="sxs-lookup"><span data-stu-id="3583e-131">Select **+ New step** > **... More** > **Add a switch case**.</span></span> 
   - <span data-ttu-id="3583e-132">Na podstawie teraz chcemy wybrać akcję do wykonania `SelectedOptions` dane wyjściowe z *wysyłania wiadomości e-mail zatwierdzania* akcji.</span><span class="sxs-lookup"><span data-stu-id="3583e-132">Now we want to select the action to perform based on the `SelectedOptions` output from the *Send approval email* action.</span></span> 
   <span data-ttu-id="3583e-133">Możesz znaleźć tego pola w **dodać zawartość dynamiczną** selektora.</span><span class="sxs-lookup"><span data-stu-id="3583e-133">You can find this field in the **Add dynamic content** selector.</span></span>
   - <span data-ttu-id="3583e-134">Użyj *przypadek 1* do obsługi po wybraniu osoby zatwierdzającej `Approve`.</span><span class="sxs-lookup"><span data-stu-id="3583e-134">Use *Case 1* to handle when the approver selects `Approve`.</span></span>
     - <span data-ttu-id="3583e-135">Po zatwierdzeniu skopiować oryginalnego pliku do usługi SharePoint Online z [ **usługi SharePoint Online — Utwórz plik** akcji](../connectors/connectors-create-api-sharepointonline.md).</span><span class="sxs-lookup"><span data-stu-id="3583e-135">If approved, copy the original file to SharePoint Online with the [**SharePoint Online - Create file** action](../connectors/connectors-create-api-sharepointonline.md).</span></span>
     - <span data-ttu-id="3583e-136">Dodaj inną akcję w przypadku aby powiadomić użytkowników, że nowy plik jest dostępny w programie SharePoint.</span><span class="sxs-lookup"><span data-stu-id="3583e-136">Add another action within the case to notify users that a new file is available on SharePoint.</span></span>
   - <span data-ttu-id="3583e-137">Dodaj inny przypadek do obsługi, gdy użytkownik wybierze `Reject`.</span><span class="sxs-lookup"><span data-stu-id="3583e-137">Add another case to handle when user selects `Reject`.</span></span>
     - <span data-ttu-id="3583e-138">W przypadku odrzucenia, Wyślij wiadomość e-mail z powiadomieniem innych osób zatwierdzających dowie się, że plik został odrzucony, a nie są wymagane nie dalsze akcje.</span><span class="sxs-lookup"><span data-stu-id="3583e-138">If rejected, send a notification email informing other approvers that the file is rejected and no further action is required.</span></span>
   - <span data-ttu-id="3583e-139">`SelectedOptions`udostępnia tylko dwie opcje, aby firma Microsoft może narazić **domyślne** przypadku puste.</span><span class="sxs-lookup"><span data-stu-id="3583e-139">`SelectedOptions` provides only two options, so we can leave the **Default** case empty.</span></span>

   ![Switch — instrukcja](./media/logic-apps-switch-case/switch.jpg)

   > [!NOTE]
   > <span data-ttu-id="3583e-141">Instrukcja switch musi mieć co najmniej jeden przypadek oprócz przypadek domyślny.</span><span class="sxs-lookup"><span data-stu-id="3583e-141">A switch statement needs at least one case in addition to the default case.</span></span>

4. <span data-ttu-id="3583e-142">Po instrukcji switch usunąć oryginalny plik przekazany do skrzynki przez dodanie tej akcji: **Dropbox - Usuń plik**</span><span class="sxs-lookup"><span data-stu-id="3583e-142">After the switch statement, delete the original file uploaded to Dropbox by adding this action: **Dropbox - Delete file**</span></span>

5. <span data-ttu-id="3583e-143">Zapisz aplikację logiki.</span><span class="sxs-lookup"><span data-stu-id="3583e-143">Save your logic app.</span></span> <span data-ttu-id="3583e-144">Testowanie aplikacji, przekazując plik do skrzynki.</span><span class="sxs-lookup"><span data-stu-id="3583e-144">Test your app by uploading a file to Dropbox.</span></span> <span data-ttu-id="3583e-145">Wkrótce otrzymasz wiadomości e-mail zatwierdzania.</span><span class="sxs-lookup"><span data-stu-id="3583e-145">You should receive an approval email shortly.</span></span> <span data-ttu-id="3583e-146">Wybierz opcję, a przyjrzeć się zachowaniu.</span><span class="sxs-lookup"><span data-stu-id="3583e-146">Select an option, and observe the behavior.</span></span>

   > [!TIP]
   > <span data-ttu-id="3583e-147">Sprawdź informacje dotyczące sposobu [Monitoruj aplikacje logiki](logic-apps-monitor-your-logic-apps.md).</span><span class="sxs-lookup"><span data-stu-id="3583e-147">Check out how to [monitor your logic apps](logic-apps-monitor-your-logic-apps.md).</span></span>

## <a name="understand-the-code-behind-switch-statements"></a><span data-ttu-id="3583e-148">Zrozumienie kodzie instrukcji switch</span><span class="sxs-lookup"><span data-stu-id="3583e-148">Understand the code behind switch statements</span></span>

<span data-ttu-id="3583e-149">Teraz, że pomyślnie utworzono aplikację logiki, za pomocą instrukcji switch, Przyjrzyjmy się definicji kodu za instrukcji switch.</span><span class="sxs-lookup"><span data-stu-id="3583e-149">Now that you successfully created a logic app using a switch statement, let's look at the code definition behind the switch statement.</span></span>

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

* <span data-ttu-id="3583e-150">`"Switch"`to nazwa instrukcji switch, które można zmienić nazwy dla czytelności.</span><span class="sxs-lookup"><span data-stu-id="3583e-150">`"Switch"` is the name of the switch statement, which you can rename for readability.</span></span> 
* <span data-ttu-id="3583e-151">`"type": "Switch"`Wskazuje, czy akcja jest instrukcji switch.</span><span class="sxs-lookup"><span data-stu-id="3583e-151">`"type": "Switch"` indicates that the action is a switch statement.</span></span> 
* <span data-ttu-id="3583e-152">`"expression"`jest osoby zatwierdzającej w tym przykładzie wybrano opcję i zostaną ocenione względem każdego przypadku zadeklarowany później w definicji.</span><span class="sxs-lookup"><span data-stu-id="3583e-152">`"expression"` is the approver's selected option in this example and is evaluated against each case declared later in the definition.</span></span> 
* <span data-ttu-id="3583e-153">`"cases"`może zawierać dowolną liczbę przypadków.</span><span class="sxs-lookup"><span data-stu-id="3583e-153">`"cases"` can contain any number of cases.</span></span> <span data-ttu-id="3583e-154">W przypadku każdego `"Case *"` to domyślna nazwa przypadek, który można zmienić nazwy dla czytelności.</span><span class="sxs-lookup"><span data-stu-id="3583e-154">For each case, `"Case *"` is the default name of the case, which you can rename for readability.</span></span> 
<span data-ttu-id="3583e-155">`"case"`Określa etykiety case, która używa wyrażenie switch do porównania, i musi być wartością stałą i unikatowe.</span><span class="sxs-lookup"><span data-stu-id="3583e-155">`"case"` specifies the case label, which the switch expression uses for comparison, and must be a constant and unique value.</span></span> <span data-ttu-id="3583e-156">Jeśli żaden z przypadków zgodne wyrażenie switch akcje w ramach `"default"` są wykonywane.</span><span class="sxs-lookup"><span data-stu-id="3583e-156">If none of the cases match the switch expression, actions under `"default"` are executed.</span></span>

## <a name="get-help"></a><span data-ttu-id="3583e-157">Uzyskiwanie pomocy</span><span class="sxs-lookup"><span data-stu-id="3583e-157">Get help</span></span>

<span data-ttu-id="3583e-158">Aby zadawać pytania, odpowiadać na nie i patrzeć, co robią inni użytkownicy usługi Azure Logic Apps, odwiedź [forum usługi Logic Apps](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurelogicapps).</span><span class="sxs-lookup"><span data-stu-id="3583e-158">To ask questions, answer questions, and see what other Azure Logic Apps users are doing, visit the [Azure Logic Apps forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurelogicapps).</span></span>

<span data-ttu-id="3583e-159">Aby pomóc w ulepszaniu usługi Azure Logic Apps, przesyłaj pomysły lub głosuj na nie w [witrynie opinii użytkowników usługi Azure Logic Apps](http://aka.ms/logicapps-wish).</span><span class="sxs-lookup"><span data-stu-id="3583e-159">To help improve Azure Logic Apps and connectors, vote on or submit ideas at the [Azure Logic Apps user feedback site](http://aka.ms/logicapps-wish).</span></span>

## <a name="next-steps"></a><span data-ttu-id="3583e-160">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="3583e-160">Next steps</span></span>

- <span data-ttu-id="3583e-161">Dowiedz się, jak [Dodawanie warunków](logic-apps-use-logic-app-features.md)</span><span class="sxs-lookup"><span data-stu-id="3583e-161">Learn how to [add conditions](logic-apps-use-logic-app-features.md)</span></span>
- <span data-ttu-id="3583e-162">Dowiedz się więcej o [błąd i obsługa wyjątków](logic-apps-exception-handling.md)</span><span class="sxs-lookup"><span data-stu-id="3583e-162">Learn about [error and exception handling](logic-apps-exception-handling.md)</span></span>
- <span data-ttu-id="3583e-163">Poznaj więcej [obsługi language przepływu pracy](logic-apps-author-definitions.md)</span><span class="sxs-lookup"><span data-stu-id="3583e-163">Explore more [workflow language capabilities](logic-apps-author-definitions.md)</span></span>