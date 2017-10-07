---
title: "aaaCreate pierwszy przepływ pracy między aplikacji w chmurze i usługi w chmurze — usługi Azure Logic Apps | Dokumentacja firmy Microsoft"
description: "Automatyzacja procesów biznesowych na potrzeby scenariuszy integracji systemów i usługi Enterprise Application Integration (EAI) przez tworzenie i uruchamianie przepływów pracy w usłudze Azure Logic Apps"
author: jeffhollan
manager: anneta
editor: 
services: logic-apps
keywords: workflow, cloud apps, cloud services, business processes, system integration, enterprise application integration, EAI
documentationcenter: 
ms.assetid: ce3582b5-9c58-4637-9379-75ff99878dcd
ms.service: logic-apps
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 03/31/2017
ms.author: LADocs; jehollan; estfan
ms.openlocfilehash: 17ec589b1c8923b5ad3e6479fc856b6ac81754ab
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-your-first-logic-app-workflow-tooautomate-processes-between-cloud-apps-and-cloud-services"></a>Tworzenie pierwszej aplikacji logiki procesów tooautomate przepływu pracy między aplikacji w chmurze i usługi w chmurze

Procesy biznesowe możesz zautomatyzować bez konieczności pisania kodu łatwiej i szybciej, jeśli utworzysz i uruchomisz przepływy pracy za pomocą usługi [Azure Logic Apps](logic-apps-what-are-logic-apps.md). Pierwszym przykładzie pokazano, jak toocreate przepływu pracy aplikacji logiki podstawowego, który sprawdza RSS źródła danych dla nowej zawartości w witrynie sieci Web. Pojawieniu się nowych elementów w źródle strumieniowym hello witryny, aplikacji logiki hello wysyła wiadomości e-mail z konta programu Outlook lub Gmail.

toocreate i uruchom aplikację logiki, potrzebne są następujące elementy:

* Subskrypcja platformy Azure. Jeśli nie masz subskrypcji, możesz [rozpocząć pracę z bezpłatnym kontem platformy Azure](https://azure.microsoft.com/free/). W przeciwnym razie możesz [skorzystać z subskrypcji z płatnością zgodnie z rzeczywistym użyciem](https://azure.microsoft.com/pricing/purchase-options/).

  Subskrypcja platformy Azure jest używana do rozliczania użycia aplikacji logiki. Dowiedz się, jak działają [pomiary użycia](../logic-apps/logic-apps-pricing.md) i jak wyglądają [ceny](https://azure.microsoft.com/pricing/details/logic-apps) w usłudze Azure Logic Apps.

Przykład wymaga także następujących elementów:

* Konto usługi Outlook.com, Office 365 Outlook lub Gmail

    > [!TIP]
    > Jeśli masz osobiste [konto Microsoft](https://account.microsoft.com/account), masz także konto usługi Outlook.com. W przeciwnym razie, jeśli masz służbowe konto platformy Azure, masz konto usługi **Office 365 Outlook**.

* Tooa łącze witryny sieci Web źródła danych RSS. W tym przykładzie użyto hello [źródło danych RSS dla najważniejszych artykułów z witryny sieci Web hello CNN.com](http://rss.cnn.com/rss/cnn_topstories.rss):`http://rss.cnn.com/rss/cnn_topstories.rss`

## <a name="add-a-trigger-that-starts-your-workflow"></a>Dodawanie wyzwalacza uruchamiającego przepływ pracy

A [ *wyzwalacza* ](./logic-apps-what-are-logic-apps.md#logic-app-concepts) jest zdarzenie, która uruchamia przepływ pracy aplikacji logiki i hello pierwszy element, który wymaga aplikacji logiki.

1. Zaloguj się toohello [portalu Azure](https://portal.azure.com "portalu Azure").

2. Z menu po lewej stronie powitania, wybierz **nowy** > **integracji przedsiębiorstwa** > **aplikacji logiki** w sposób pokazany poniżej:

     ![Azure Portal, Nowy, Integracja w przedsiębiorstwie, Aplikacja logiki](media/logic-apps-create-a-logic-app/azure-portal-create-logic-app.png)

   > [!TIP]
   > Można również wybrać **nowy**, następnie w polu wyszukiwania hello wpisz `logic app`, i naciśnij klawisz Enter. Następnie wybierz kolejno pozycje **Aplikacja logiki** > **Utwórz**.

3. Nadaj nazwę aplikacji logiki i wybierz subskrypcję platformy Azure. Teraz utwórz lub wybierz grupę zasobów platformy Azure, która ułatwi organizowanie powiązanych zasobów platformy Azure i zarządzanie nimi. Na koniec wybierz lokalizację centrum danych hello do hostowania aplikacji logiki. Gdy wszystko jest gotowe, wybierz pozycję **toodashboard numeru Pin** , a następnie **Utwórz**.

     ![Szczegóły aplikacji logiki](media/logic-apps-create-a-logic-app/logic-app-settings.png)

   > [!NOTE]
   > Po wybraniu **toodashboard numeru Pin**, aplikację logiki pojawią się na hello Azure pulpitu nawigacyjnego po wdrożeniu i otwierany automatycznie. Jeśli aplikację logiki nie jest wyświetlane na pulpicie nawigacyjnym hello i na powitania **wszystkie zasoby** kafelka, wybierz **Zobacz więcej**i wybierz aplikację logiki. Lub w menu po lewej stronie powitania, wybierz **więcej usług**. W obszarze **Integracja w przedsiębiorstwie** wybierz pozycję **Aplikacje logiki** i wybierz swoją aplikację logiki.

4. Po otwarciu aplikacji logiki na powitania po raz pierwszy, hello projektanta aplikacji logiki zawiera szablony służy tooget uruchomiona. Na razie wybierz pozycję **Pusta aplikacja logiki**, aby rozpocząć tworzenie aplikacji logiki od podstaw.

    Witaj projektanta aplikacji logiki otwiera i pokazuje dostępnych usług i *wyzwalaczy* używanego w aplikacji logiki.

5. W polu wyszukiwania hello wpisz `RSS`i wybierz wyzwalacz: **RSS — po opublikowaniu element źródła** 

    ![Wyzwalacz kanału informacyjnego RSS](media/logic-apps-create-a-logic-app/rss-trigger.png)

6. Wprowadź hello link do witryny sieci Web hello źródło danych RSS, które mają tootrack. 

     Dodatkowo możesz zmienić **Częstotliwość** i **Interwał**. 
     Te ustawienia umożliwiają określenie, jak często aplikacja logiki ma sprawdzać istnienie nowych elementów i zwracać wszystkie elementy z tego okresu.

     Na przykład załóżmy Sprawdź codziennie dla najważniejszych artykułów zaksięgowany toohello CNN witryny sieci Web.

     ![Konfigurowanie kanału informacyjnego RSS, częstotliwości i interwału dla wyzwalacza](media/logic-apps-create-a-logic-app/rss-trigger-setup.png)

7. Zapisz swoją pracę. (Na pasku poleceń projektanta hello wybierz **zapisać**.)

   ![Zapisywanie aplikacji logiki](media/logic-apps-create-a-logic-app/save-logic-app.png)

   Po zapisaniu, aplikację logiki przechodzi na żywo, ale obecnie aplikację logiki sprawdza tylko dla nowych elementów w hello określone źródło danych RSS. 
   toomake generowane w tym przykładzie bardziej użyteczna, możemy dodać akcję, która wykonuje aplikację logiki po wyzwalacz.

## <a name="add-an-action-that-responds-tooyour-trigger"></a>Dodaj akcję, która odpowiada tooyour wyzwalacza

[*Akcja*](./logic-apps-what-are-logic-apps.md#logic-app-concepts) to zadanie wykonywane przez przepływ pracy aplikacji logiki. Po dodaniu aplikacji logiki wyzwalacza tooyour, można dodać operacji tooperform akcji z danych wygenerowanych przez tego wyzwalacza. W naszym przykładzie mamy teraz dodać akcję, która wysyła wiadomości e-mail, gdy pojawią się nowe elementy w kanału informacyjnego RSS hello witryny.

1. W Projektancie hello, w obszarze wyzwalacz, wybierz **nowy krok** > **Dodaj akcję** w sposób pokazany poniżej:

   ![Dodawanie akcji](media/logic-apps-create-a-logic-app/add-new-action.png)

   Witaj projektanta pokazuje [dostępnych łączników](../connectors/apis-list.md) , w którym można wybrać tooperform akcji po wyzwalacz.

2. W oparciu o Twoje konto e-mail, wykonaj kroki powitania dla programu Outlook lub Gmail.

   * Wprowadź toosend poczty e-mail, z Twojego konta programu Outlook, w polu wyszukiwania hello `outlook`. W obszarze **Usługi** wybierz pozycję **Outlook.com** w przypadku osobistych kont Microsoft lub pozycję **Office 365 Outlook** w przypadku kont służbowych platformy Azure. 
   W obszarze **Akcje** wybierz pozycję **Wyślij wiadomość e-mail**.

       ![Wybieranie akcji programu Outlook „Wyślij wiadomość e-mail”](media/logic-apps-create-a-logic-app/actions.png)

   * Wprowadź toosend poczty e-mail, z Twojego konta usługi Gmail, w polu wyszukiwania hello `gmail`. 
   W obszarze **Akcje** wybierz pozycję **Wyślij wiadomość e-mail**.

       ![Wybieranie pozycji „Gmail — Wyślij wiadomość e-mail”](media/logic-apps-create-a-logic-app/actions-gmail.png)

3. Po wyświetleniu monitu o poświadczenia, zaloguj się hello nazwę użytkownika i hasło dla swojego konta poczty e-mail. 

4. Podaj dane hello dotyczących tej akcji, takich jak hello adresu e-mail i wybierz parametry hello tooinclude danych hello w hello poczty e-mail, na przykład:

   ![Wybierz tooinclude danych w wiadomości e-mail](media/logic-apps-create-a-logic-app/rss-action-setup.png)

    Jeśli wybrano program Outlook, aplikacja logiki może wyglądać jak w tym przykładzie:

    ![Ukończona aplikacja logiki](media/logic-apps-create-a-logic-app/save-run-complete-logic-app.png)

5.  Zapisz zmiany. (Na pasku poleceń projektanta hello wybierz **zapisać**.)

6. Teraz możesz ręcznie uruchomić aplikację logiki na potrzeby testowania. Na pasku poleceń projektanta hello wybierz **Uruchom**. W przeciwnym razie możesz pozwolić, aby aplikację logiki, sprawdź, czy hello określona na podstawie harmonogramu hello, które można skonfigurować źródło danych RSS.

   Jeśli odnalezionej nowej aplikacji logiki aplikacji logiki hello wysyła wiadomości e-mail zawierające wybranych danych. 
   W przypadku znalezienia nowych elementów aplikację logiki pomija hello akcję, która wysyła wiadomość e-mail.

7. toomonitor i Sprawdź aplikację logiki do uruchomienia i wyzwolić historii, w menu aplikacji logiki, wybierz opcję **omówienie**.

   ![Monitorowanie i wyświetlanie historii wyzwalania oraz uruchamiania aplikacji logiki](media/logic-apps-create-a-logic-app/logic-app-run-trigger-history.png)

   > [!TIP]
   > Jeśli nie znajdziesz hello dane, które należy oczekiwać na pasku poleceń hello, spróbuj wybrać **Odśwież**.

   więcej informacji na temat stanu aplikacji logiki toolearn lub uruchamianie i wyzwolić historii lub toodiagnose aplikację logiki, zobacz [rozwiązywania problemów z aplikacją logiki](logic-apps-diagnosing-failures.md).

      > [!NOTE]
      > Aplikacja logiki będzie działać do momentu jej wyłączenia. tooturn poza aplikacji teraz, w menu aplikacji logiki, wybierz **omówienie**. Na pasku poleceń hello, wybierz **wyłączyć**.

Gratulacje, udało Ci się skonfigurować i uruchomić Twoją pierwszą podstawową aplikację logiki. Wiesz już, jak łatwe jest tworzenie przepływów pracy automatyzujących procesy oraz integrowanie aplikacji w chmurze i usług w chmurze — a wszystko to bez konieczności pisania kodu.

## <a name="manage-your-logic-app"></a>Zarządzanie aplikacją logiki

toomanage aplikacji, można wykonać zadania, takie jak sprawdzić stan hello, edytować, wyświetlanie historii, wyłączyć lub usunąć aplikację logiki.

1. Zaloguj się toohello [portalu Azure](https://portal.azure.com "portalu Azure").

2. W menu po lewej stronie powitania, wybierz **więcej usług**. W obszarze **Integracja w przedsiębiorstwie** wybierz pozycję **Logic Apps**. Wybierz aplikację logiki. 

   W menu aplikacji logiki hello można znaleźć w tych zadań zarządzania aplikacji logiki:

   |Zadanie|Kroki| 
   |:---|:---| 
   | Wyświetlenie stanu aplikacji, historii wykonywania i informacji ogólnych| Wybierz pozycję **Przegląd**.| 
   | Edytowanie aplikacji | Wybierz pozycję **Projektant aplikacji logiki**. | 
   | Wyświetlenie definicji kodu JSON przepływu pracy aplikacji | Wybierz pozycję **Widok kodu aplikacji logiki**. | 
   | Wyświetlenie operacji wykonywanych względem aplikacji logiki | Wybierz pozycję **Dziennik aktywności**. | 
   | Wyświetlenie wcześniejszych wersji aplikacji logiki | Wybierz pozycję **Wersje**. | 
   | Tymczasowe wyłączenie aplikacji | Wybierz **omówienie**, następnie na pasku poleceń hello, wybierz pozycję **wyłączyć**. | 
   | Usunięcie aplikacji | Wybierz **omówienie**, następnie na pasku poleceń hello, wybierz pozycję **usunąć**. Wprowadź nazwę aplikacji logiki, a następnie wybierz pozycję **Usuń**. | 

## <a name="get-help"></a>Uzyskiwanie pomocy

pytania tooask odpowiedzi na pytania i Dowiedz się, jakie inne usługi Azure Logic Apps robią użytkownicy, odwiedź stronę hello [forum usługi Azure Logic Apps](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurelogicapps).

toohelp poprawy usługi Azure Logic Apps i łącznikami, Zagłosuj lub Prześlij pomysłów na powitania [witrynę opinii użytkowników usługi Azure Logic Apps](http://aka.ms/logicapps-wish).

## <a name="next-steps"></a>Następne kroki

*  [Dodawanie warunków i uruchamianie przepływów pracy](../logic-apps/logic-apps-use-logic-app-features.md)
*    [Szablony aplikacji logiki](../logic-apps/logic-apps-use-logic-app-templates.md)
*  [Tworzenie aplikacji logiki z szablonów usługi Azure Resource Manager](../logic-apps/logic-apps-arm-provision.md)
