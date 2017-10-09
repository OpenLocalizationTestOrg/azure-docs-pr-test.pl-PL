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
# <a name="perform-different-actions-in-logic-apps-with-a-switch-statement"></a>Wykonaj różne akcje w aplikacjach logiki z instrukcji switch

Podczas tworzenia przepływu pracy, często mają różne akcje tootake na podstawie wartości hello obiektu lub wyrażenie. Można na przykład z toobehave aplikacji logiki inaczej w zależności od hello kod stanu HTTP żądania lub opcji wybranej w wiadomości e-mail.

Można użyć tych scenariuszy tooimplement instrukcji switch. Aplikację logiki można ocenić tokenu lub wyrażenie i wybierz w przypadku hello hello samą powitalnych tooexecute wartość określone akcje. Tylko jeden przypadek powinna odpowiadać hello instrukcji switch.

> [!TIP]
> Podobnie jak wszystkie języki programowania instrukcji switch obsługuje tylko operatory równości. Jeśli potrzebujesz innych operatory relacyjne takich jak "większe niż", użyj instrukcji warunku.
> sposób wykonywania deterministyczne tooensure, przypadków musi zawierać wartość unikatowa i statyczne zamiast tokeny dynamicznych lub wyrażenie.

## <a name="prerequisites"></a>Wymagania wstępne

- Aktywna subskrypcja platformy Azure. Jeśli nie masz aktywnych subskrypcji platformy Azure, [utworzyć bezpłatne konto](https://azure.microsoft.com/free/), lub spróbuj [wolne aplikacje logiki dla](https://tryappservice.azure.com/).
- [Podstawową wiedzę na temat dotyczące aplikacji logiki](logic-apps-what-are-logic-apps.md)

## <a name="add-a-switch-statement-tooyour-workflow"></a>Dodaj przepływ pracy tooyour instrukcji switch

tooshow działania instrukcji switch, w tym przykładzie tworzy aplikację logiki, że monitory pliki przekazywane tooDropbox. Po przekazaniu hello nowe pliki aplikacji logiki hello wysyła osoba zatwierdzająca tooan poczty e-mail, który wybiera czy tootransfer tooSharePoint tych plików. Aplikacja Hello używa instrukcji switch, który wykonuje różne akcje na podstawie wartości hello, które hello wybiera osoby zatwierdzającej.

1. Tworzenie aplikacji logiki, a następnie wybierz tego wyzwalacza: **Dropbox — po utworzeniu pliku**.

   ![Użyj usługi Dropbox — podczas tworzenia pliku wyzwalacza](./media/logic-apps-switch-case/dropbox-trigger.jpg)

2. W obszarze hello wyzwalacza, Dodaj tę akcję: **Outlook.com — wysyłanie wiadomości e-mail zatwierdzania**

   > [!TIP]
   > Aplikacje logiki obsługują także wysyłania scenariusze wiadomości e-mail zatwierdzania z konta programu Outlook pakietu Office 365.

   - Jeśli nie masz istniejące połączenie, zostanie wyświetlony monit toocreate jeden.
   - Wypełnij pola hello wymagane. Na przykład w obszarze **do**, określ hello adres e-mail do wysyłania wiadomości e-mail osoby zatwierdzającej hello.
   - W obszarze **opcji użytkownika**, wprowadź `Approve, Reject`.

   ![Skonfiguruj połączenie](./media/logic-apps-switch-case/send-approval-email-action.jpg)

3. Dodawanie instrukcji switch.

   - Wybierz **+ nowy krok** > **... Więcej** > **dodawanie przypadku przełącznika**. 
   - Teraz chcemy tooperform akcji hello tooselect oparte na powitania `SelectedOptions` dane wyjściowe z hello *wysyłania wiadomości e-mail zatwierdzania* akcji. 
   W tym polu można znaleźć w hello **dodać zawartość dynamiczną** selektora.
   - Użyj *przypadek 1* toohandle po wybraniu osoba zatwierdzająca hello `Approve`.
     - Po zatwierdzeniu skopiować hello oryginalnego pliku tooSharePoint Online z hello [ **usługi SharePoint Online — Utwórz plik** akcji](../connectors/connectors-create-api-sharepointonline.md).
     - Dodaj inną akcję w hello toonotify wielkość użytkowników, że nowy plik jest dostępny w programie SharePoint.
   - Dodaj inną wielkość toohandle po wybraniu użytkownika `Reject`.
     - W przypadku odrzucenia, Wyślij wiadomość e-mail z powiadomieniem informowania innych osób zatwierdzających hello pliku zostało odrzucone, a nie są wymagane nie dalsze akcje.
   - `SelectedOptions`udostępnia tylko dwie opcje, aby firma Microsoft może narazić hello **domyślne** przypadku puste.

   ![Switch — instrukcja](./media/logic-apps-switch-case/switch.jpg)

   > [!NOTE]
   > Instrukcja switch musi mieć co najmniej jeden przypadek w przypadku domyślnej toohello dodanie.

4. Po instrukcji switch hello, należy usunąć hello oryginalny plik przekazany tooDropbox przez dodanie tej akcji: **Dropbox - Usuń plik**

5. Zapisz aplikację logiki. Testowanie aplikacji, przekazując tooDropbox pliku. Wkrótce otrzymasz wiadomości e-mail zatwierdzania. Wybierz opcję i sprawdź hello zachowanie.

   > [!TIP]
   > Sprawdź, jak za[Monitoruj aplikacje logiki](logic-apps-monitor-your-logic-apps.md).

## <a name="understand-hello-code-behind-switch-statements"></a>Zrozumienie hello kodzie instrukcji switch

Teraz, że pomyślnie utworzono aplikację logiki, za pomocą instrukcji switch, Przyjrzyjmy się definicji kodu hello hello instrukcji switch.

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

* `"Switch"`to nazwa hello instrukcji switch hello, które można zmienić nazwy dla czytelności. 
* `"type": "Switch"`Wskazuje, że akcja hello jest instrukcji switch. 
* `"expression"`jest osoby zatwierdzającej hello wybranej opcji, w tym przykładzie i zostaną ocenione względem każdego przypadku zadeklarowany w dalszej części hello definicji. 
* `"cases"`może zawierać dowolną liczbę przypadków. W przypadku każdego `"Case *"` jest hello domyślną nazwę przypadku hello, który można zmienić nazwy dla czytelności. 
`"case"`Określa etykiety case hello, hello używa wyrażenia switch do porównania, a musi być wartością stałą i unikatowe. Jeśli żadna z przypadków hello nie zgadza wyrażenie switch hello, akcje w ramach `"default"` są wykonywane.

## <a name="get-help"></a>Uzyskiwanie pomocy

pytania tooask, odpowiadanie na pytania i robią innych użytkowników usługi Azure Logic Apps, zobacz odwiedź hello [forum usługi Azure Logic Apps](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurelogicapps).

toohelp poprawy usługi Azure Logic Apps i łącznikami, Zagłosuj lub Prześlij pomysłów na powitania [witrynę opinii użytkowników usługi Azure Logic Apps](http://aka.ms/logicapps-wish).

## <a name="next-steps"></a>Następne kroki

- Dowiedz się, jak za[Dodawanie warunków](logic-apps-use-logic-app-features.md)
- Dowiedz się więcej o [błąd i obsługa wyjątków](logic-apps-exception-handling.md)
- Poznaj więcej [obsługi language przepływu pracy](logic-apps-author-definitions.md)