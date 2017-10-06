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
# <a name="use-logic-apps-features"></a>Korzystanie z funkcji Logic Apps

W [poprzedniego tematu](../logic-apps/logic-apps-create-a-logic-app.md), utworzyć pierwszą aplikację logiki. toocontrol przepływu pracy aplikacji logiki, można określić różne ścieżki dla Twojego toorun aplikacji logiki i jak zbyt przetwarzania danych w macierzy, kolekcji i partie. W przepływie pracy aplikacji logiki można uwzględnić następujące elementy:

* Warunki i [przełącznika instrukcje](../logic-apps/logic-apps-switch-case.md) let aplikację logiki, uruchom różnych akcji w oparciu o Określa, czy zostały spełnione określone warunki.

* [Pętle](../logic-apps/logic-apps-loops-and-scopes.md) let aplikację logiki cyklicznie uruchamiany kroki. Na przykład można powtórzyć akcje dotyczące tablicy korzystając z **For_each** pętli. Lub akcji można powtórzyć, dopóki spełniony jest warunek, korzystając z **do momentu** pętli.

* [Zakresy](../logic-apps/logic-apps-loops-and-scopes.md) let uruchamianym serii akcji, na przykład tooimplement obsługi wyjątków.

* [Debatching](../logic-apps/logic-apps-loops-and-scopes.md) umożliwia aplikację logiki, uruchom oddzielne przepływy pracy dla elementów w tablicy, gdy używasz hello **SplitOn** polecenia.

W tym temacie przedstawiono inne pojęć dotyczących tworzenia aplikacji logiki:

* Kod widoku tooedit istniejących aplikacji logiki
* Opcje uruchamiania przepływu pracy

## <a name="conditions-run-steps-only-after-meeting-a-condition"></a>Warunki: Uruchamianie kroków tylko po spełniających warunek

toohave aplikację logiki, uruchom kroki tylko wtedy, gdy dane spełniają określone kryteria, można dodać warunek, który porównuje dane w przepływie pracy hello względem określonych pól lub wartości.

Na przykład załóżmy, że masz aplikację logiki, która wysyła zbyt dużo żądań wiadomości e-mail Posty na kanału informacyjnego RSS witryny sieci Web. Można dodać warunku, aby aplikację logiki wysyła wiadomości e-mail, tylko wtedy, gdy po hello nowe należy tooa określonej kategorii.

1. W hello [portalu Azure](https://portal.azure.com), znajdowanie i otwieranie aplikacji logiki w Projektancie aplikacji logiki.

2. Dodaj warunek toohello przepływu pracy lokalizacji. 

   warunek hello tooadd między krokami istniejących w przepływie pracy aplikacji logiki hello, przesuń wskaźnik hello na strzałkę hello miejscu tooadd hello warunku. 
   Wybierz hello **znak plus** (**+**), a następnie wybierz **Dodaj warunek**. Na przykład:

   ![Dodaj warunek toologic aplikacji](./media/logic-apps-use-logic-app-features/add-condition.png)

   > [!NOTE]
   > Jeśli chcesz tooadd warunek hello końca bieżącego przepływu pracy, przejdź toohello dołu aplikację logiki i wybierz **+ nowy krok**.

3. Teraz można zdefiniować hello warunku. Określ pola źródłowego hello mają tooevaluate, hello tooperform operację i wartość docelowa hello lub pola. tooadd istniejących pól tooyour warunku, wybierz jedną z hello **listy zawartości dynamicznej Dodaj**.

   Na przykład:

   ![Edytuj warunek w trybie podstawowym](./media/logic-apps-use-logic-app-features/edit-condition-basic-mode.png)

   Oto hello Pełny warunek:

   ![Pełny warunek](./media/logic-apps-use-logic-app-features/edit-condition-basic-mode-2.png)

   > [!TIP]
   > Wybierz warunek hello toodefine w kodzie, **edytowanie w trybie zaawansowanym**. Na przykład:
   > 
   > ![Edytuj warunek w kodzie](./media/logic-apps-use-logic-app-features/edit-condition-advanced-mode.png)

4. W obszarze **tak, jeśli** i **nr IF**, Dodaj tooperform kroki hello według tego, czy jest spełniony warunek hello.

   Na przykład:

   ![Stan tak i ścieżek](./media/logic-apps-use-logic-app-features/condition-yes-no-path.png)

   > [!TIP]
   > Można przeciągnij istniejące działania do hello **tak, jeśli** i **nr IF** ścieżki.

5. Gdy wszystko będzie gotowe, Zapisz aplikację logiki.

Teraz możesz otrzymywać wiadomości e-mail, tylko wtedy, gdy wpisy hello spełniają warunek.

## <a name="repeat-actions-over-a-list-with-foreach"></a>Powtórz akcje listy za pomocą instrukcji forEach

pętli forEach Hello określa toorepeat tablicy akcji za pośrednictwem. Jeśli nie jest tablicą, przepływ hello zakończy się niepowodzeniem. Na przykład jeśli masz action1, który generuje tablicę komunikatów i ma toosend każdy komunikat, we właściwościach hello działań. można uwzględnić tej instrukcji forEach:`forEach : "@action('action1').outputs.messages"`

## <a name="edit-hello-code-definition-for-a-logic-app"></a>Edytuj kod hello definicję aplikacji logiki

Mimo że masz hello projektanta aplikacji logiki można edytować bezpośrednio hello kodu, który definiuje aplikacji logiki.

1. Na pasku poleceń hello, wybierz **widok Kod**.

    Pełna Edytor otwiera się i przedstawiono definicję hello, który można edytować.

    ![Widok kodu](media/logic-apps-use-logic-app-features/codeview.png)

    W edytorze tekstu hello, można skopiować i wkleić dowolną liczbę akcji w obrębie hello tej samej aplikacji logiki lub między aplikacji logiki. 
    Można również łatwo Dodaj lub Usuń całą sekcję od definicji hello i definicji mogą również współużytkować z innymi osobami.

2. Wybierz zmiany, toosave **zapisać**.

## <a name="parameters"></a>Parametry

Niektóre z funkcji Logic Apps są dostępne tylko w widoku kodu, na przykład parametry. Parametry umożliwiają łatwe tooreuse wartości w całej aplikacji logiki. Na przykład jeśli masz adres e-mail, która ma zostać użyta w kilka akcji, należy zdefiniować tego adresu e-mail jako parametr.

Parametry są odpowiednie w ściąganie wartości są prawdopodobnie toochange partii. Są one szczególnie przydatne, gdy będziesz potrzebować toooverride parametrów w różnych środowiskach. Parametry toooverride opartych na środowisku, zobacz temat toolearn [Tworzenie definicji aplikacji logiki](../logic-apps/logic-apps-author-definitions.md) i [dokumentacja interfejsu API REST](https://docs.microsoft.com/rest/api/logic).

W tym przykładzie pokazano sposób tooupdate istniejących aplikacji logiki, aby można używać parametrów dla hello wyszukiwanego terminu.

1. W widoku Kod, Znajdź hello `parameters : {}` obiekt, a następnie dodaj `currentFeedUrl` obiektu:

        "currentFeedUrl" : {
            "type" : "string",
            "defaultValue" : "http://rss.cnn.com/rss/cnn_topstories.rss"
        }

2. Przejdź toohello `When_a_feed-item_is_published` akcji, Znajdź hello `queries` sekcji, a wartość zapytania hello:`"feedUrl": "#@{parameters('currentFeedUrl')}"` 

    toojoin dwa lub więcej ciągów, można również użyć hello `concat` funkcji. 
    Na przykład `"@concat('#',parameters('currentFeedUrl'))"` works hello takie same jak hello powyżej.

3.  Gdy wszystko będzie gotowe, wybierz pozycję **zapisać**. 

    Teraz możesz zmienić witryny hello danych RSS przez przekazanie do innego adresu URL za pośrednictwem hello `currentFeedURL` obiektu.

Dowiedz się więcej o [jak definicjami aplikacji logiki tooauthor](../logic-apps/logic-apps-author-definitions.md).

## <a name="start-logic-app-workflows"></a>Uruchomić przepływy pracy aplikacji logiki

Masz różne opcje uruchamiania przepływu pracy hello zdefiniowanych w aplikacji logiki. Zawsze można uruchomić przepływu pracy na żądanie w hello [portalu Azure].

### <a name="recurrence-triggers"></a>Wyzwalacze cyklu

Uruchamia wyzwalacz cyklu w odstępach czasu, który określisz. Wyzwalacz powitania po logikę warunkową wyzwalacza hello Określa, czy hello przepływu pracy musi toorun. Wyzwalacz wskazuje uruchamiania przepływu pracy hello zwracając `200` kod stanu. Po hello przepływu pracy nie wymaga toorun, wyzwalacz hello zwraca `202` kod stanu.

### <a name="callback-using-rest-apis"></a>Wywołanie zwrotne za pomocą interfejsów API REST

toostart przepływu pracy, usługi mogą wywoływać punkt końcowy aplikacji logiki. Wybierz ten rodzaj logiki aplikacji na żądanie, toostart **Uruchom teraz** na powitania paska poleceń. Zobacz [uruchomić przepływy pracy, wywołując logiki punkty końcowe aplikacji jako wyzwalacze](../logic-apps/logic-apps-http-endpoint.md). 

<!-- Shared links -->
[portalu Azure]: https://portal.azure.com

## <a name="next-steps"></a>Następne kroki

* [Instrukcji Switch](../logic-apps/logic-apps-switch-case.md) 
* [Pętle, zakresy i usuwanie partii](../logic-apps/logic-apps-loops-and-scopes.md)
* [Tworzenie definicji aplikacji logiki](../logic-apps/logic-apps-author-definitions.md)