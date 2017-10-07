---
title: "zmiany maszyny wirtualnej aaaMonitor - & siatki zdarzeń Azure Logic Apps | Dokumentacja firmy Microsoft"
description: "Sprawdź zmiany konfiguracji w maszynach wirtualnych (VM) przy użyciu siatki zdarzeń platformy Azure i Logic Apps"
keywords: "aplikacje logiki, siatki zdarzeń, w przypadku maszyny wirtualnej maszyny Wirtualnej"
services: logic-apps
author: ecfan
manager: anneta
ms.assetid: 
ms.workload: logic-apps
ms.service: logic-apps
ms.topic: article
ms.date: 08/16/2017
ms.author: LADocs; estfan
ms.openlocfilehash: f0633e598be6e7880a310e6f8e64f6738cc692b3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-virtual-machine-changes-with-azure-event-grid-and-logic-apps"></a>Monitoruj zmiany maszyny wirtualnej Azure zdarzeń siatki i Logic Apps

Można uruchomić zautomatyzowanych [przepływu pracy aplikacji logiki](../logic-apps/logic-apps-what-are-logic-apps.md) po określonych zdarzeń w zasobów platformy Azure lub innych zasobów. Te zasoby można opublikować te zdarzenia tooan [siatki usługi Azure event](../event-grid/overview.md). Z kolei siatki zdarzeń hello wypchnięcia toosubscribers tych zdarzeń, których kolejek, elementów webhook, lub [usługi event hubs](../event-hubs/event-hubs-what-is-event-hubs.md) jako punktów końcowych. Jako aplikację logiki może oczekiwać przed uruchomieniem zadania tooperform — automatycznych przepływów pracy bez pisania żadnego kodu tych zdarzeń z hello zdarzeń siatki.

Na przykład poniżej przedstawiono niektóre zdarzenia wysłać toosubscribers za pośrednictwem usługi Azure Event siatki hello wydawcy:

* Tworzenia, odczytu, zaktualizować lub usunąć zasób. Na przykład można monitorować zmian, które mogą spowodować naliczenie opłat w ramach subskrypcji platformy Azure i mają wpływ na rachunku. 
* Dodaj lub Usuń osoby z subskrypcją platformy Azure.
* Aplikacja wykonuje określonej akcji.
* Wyświetleniu nowego komunikatu z kolejki.

W tym samouczku tworzy aplikację logiki, który monitoruje maszyny wirtualnej tooa zmiany i wysyła powiadomienia dotyczące tych zmian. Podczas tworzenia aplikacji logiki z subskrypcji zdarzeń dla zasobów platformy Azure, zdarzenia będą przepływać z tego zasobu za pośrednictwem aplikacji logiki toohello zdarzeń siatki. Witaj samouczek przedstawia tworzenie aplikacji logiki:

![Przegląd — monitor maszyny wirtualnej z aplikacji logiki i siatki zdarzeń](./media/monitor-virtual-machine-changes-event-grid-logic-app/monitor-virtual-machine-event-grid-logic-app-overview.png)

Ten samouczek zawiera informacje na temat wykonywania następujących czynności:

> [!div class="checklist"]
> * Tworzenie aplikacji logiki, który monitoruje zdarzenia z siatki zdarzeń.
> * Dodaj warunek, które w szczególności sprawdza zmiany maszyny wirtualnej.
> * Wyślij wiadomość e-mail, gdy zmienia się na komputerze wirtualnym.

## <a name="prerequisites"></a>Wymagania wstępne

* Konto e-mail z [każdego dostawcy poczty e-mail obsługiwane przez usługi Azure Logic Apps](../connectors/apis-list.md), takie jak program Outlook pakietu Office 365, Outlook.com lub Gmail wysyłania powiadomień. W tym samouczku korzysta z programu Outlook pakietu Office 365.

* A [maszyny wirtualnej](https://azure.microsoft.com/services/virtual-machines). Jeśli jeszcze tego nie zrobiono, utwórz maszynę wirtualną za pośrednictwem [utworzyć samouczek wirtualna](https://docs.microsoft.com/azure/virtual-machines/). Maszyna wirtualna hello toomake publikowanie zdarzeń, możesz [nie ma potrzeby toodo cokolwiek innego](../event-grid/overview.md).

## <a name="create-a-logic-app-that-monitors-events-from-an-event-grid"></a>Tworzenie aplikacji logiki, który monitoruje zdarzenia z siatki zdarzeń

Najpierw należy utworzyć aplikację logiki i dodać wyzwalacz siatki zdarzeń, który monitoruje hello grupy zasobów dla maszyny wirtualnej. 

1. Zaloguj się toohello [portalu Azure](https://portal.azure.com). 

2. Z hello lewego górnego rogu hello głównego menu Azure, wybierz **nowy** > **integracji przedsiębiorstwa** > **aplikacji logiki**.

   ![Tworzenie aplikacji logiki](./media/monitor-virtual-machine-changes-event-grid-logic-app/azure-portal-create-logic-app.png)

3. Utwórz aplikację logiki z ustawieniami hello hello w poniższej tabeli:

   ![Podaj szczegóły aplikacji logiki](./media/monitor-virtual-machine-changes-event-grid-logic-app/create-logic-app-for-event-grid.png)

   | Ustawienie | Sugerowana wartość | Opis | 
   | ------- | --------------- | ----------- | 
   | **Nazwa** | *{your logiki app-name}* | Podaj nazwę aplikacji logiki unikatowy. | 
   | **Subskrypcja** | *{subskrypcji your Azure}* | Wybierz hello tej samej subskrypcji platformy Azure dla wszystkich usług w tym samouczku. | 
   | **Grupa zasobów** | *{your-Azure grupa zasobów}* | Wybierz hello tej samej grupy zasobów platformy Azure dla wszystkich usług, w tym samouczku. | 
   | **Lokalizacja** | *{your Azure region}* | Wybierz hello tego samego regionu dla wszystkich usług, w tym samouczku. | 
   | | | 

4. Jeśli wszystko jest gotowe, wybierz **toodashboard numeru Pin**i wybierz polecenie **Utwórz**.

   Teraz utworzona zasobów platformy Azure dla aplikacji logiki. 
   Po Azure wdraża aplikację logiki, hello projektanta aplikacji logiki pokazuje szablonów dla typowe wzorce, można rozpocząć szybciej.

   > [!NOTE] 
   > Po wybraniu **toodashboard numeru Pin**, aplikację logiki automatycznie otwiera w Projektancie aplikacji logiki. W przeciwnym razie ręcznie znaleźć i otworzyć aplikację logiki.

5. Teraz można wybrać szablon aplikacji logiki. W obszarze **szablony**, wybierz **pustą aplikację logiki** , można utworzyć aplikację logiki od początku.

   ![Wybierz szablon aplikacji logiki](./media/monitor-virtual-machine-changes-event-grid-logic-app/choose-logic-app-template.png)

   teraz pokazuje Hello projektanta aplikacji logiki [ *łączniki* ](../connectors/apis-list.md) i [ *wyzwalaczy* ](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts) można użyć toostart aplikacji logiki i również akcje Czy można dodać po zadania tooperform wyzwalacza. Wyzwalacz jest zdarzenie, które tworzy wystąpienie aplikacji logiki i uruchamia przepływ pracy aplikacji logiki. 
   Aplikację logiki musi wyzwalacz jako pierwszy element hello.

6. W polu wyszukiwania hello wprowadź "zdarzeń siatki" jako filtr. Wybierz ten wyzwalacz: **siatki zdarzeń Azure — w przypadku zdarzeń zasobów**

   ![Wybierz ten wyzwalacz: "Azure zdarzeń Siatka — na zdarzenie typu zasobu"](./media/monitor-virtual-machine-changes-event-grid-logic-app/logic-app-event-grid-trigger.png)

7. Po wyświetleniu monitu zaloguj się tooAzure siatki zdarzeń przy użyciu poświadczeń platformy Azure.

   ![Zaloguj się przy użyciu poświadczeń platformy Azure](./media/monitor-virtual-machine-changes-event-grid-logic-app/sign-in-event-grid.png)

   > [!NOTE]
   > Jeśli logujesz się za pomocą osobistego konta Microsoft, takich jak @outlook.com lub @hotmail.com, wyzwalacz zdarzenia siatki hello może nie być wyświetlana poprawnie. Jako obejście, wybierz [Połącz z główną usługi](/azure-resource-manager/resource-group-create-service-principal-portal.md), lub Uwierzytelnij się jako członek hello Azure Active Directory, skojarzone z subskrypcją platformy Azure, na przykład *nazwy użytkownika* @emailoutlook.onmicrosoft.com.

8. Teraz subskrypcji zdarzeń toopublisher aplikacji logiki. Podaj szczegóły powitania dla Twojej subskrypcji zdarzeń, jak określono w hello w poniższej tabeli:

   ![Podaj szczegóły subskrypcji zdarzeń](./media/monitor-virtual-machine-changes-event-grid-logic-app/logic-app-event-grid-trigger-details-generic.png)

   | Ustawienie | Sugerowana wartość | Opis | 
   | ------- | --------------- | ----------- | 
   | **Subskrypcja** | *{wirtualnego machine subskrypcji platformy Azure —}* | Wybierz wydawca zdarzeń hello subskrypcji platformy Azure. W tym samouczku wybierz hello subskrypcji platformy Azure dla maszyny wirtualnej. | 
   | **Typ zasobu** | Microsoft.Resources.resourceGroups | Wybierz typ zasobu wydawca zdarzeń hello. W tym samouczku wybierz hello określonej wartości, więc aplikację logiki monitoruje tylko grupy zasobów. | 
   | **Nazwa zasobu** | *{wirtualnego machine-— Nazwa grupy zasobów —}* | Wybierz nazwę zasobu hello wydawcy. W tym samouczku wybierz nazwę hello hello grupy zasobów dla maszyny wirtualnej. | 
   | Wybierz opcjonalne ustawienia **Pokaż zaawansowane opcje**. | *{zobacz opisy}* | * **Prefiks filtru**: W tym samouczku, pozostaw to ustawienie puste. zachowanie domyślne Hello dopasowuje wszystkie wartości. Jednak można określić ciąg prefiksu jako filtru, na przykład ścieżkę i parametr dla określonego zasobu. <p>* **Sufiks filtru**: W tym samouczku, pozostaw to ustawienie puste. zachowanie domyślne Hello dopasowuje wszystkie wartości. Jednak można określić ciąg sufiksu jako filtru, na przykład rozszerzenie nazwy pliku, jeśli chcesz tylko określonych typów plików.<p>* **Nazwa subskrypcji**: Podaj unikatową nazwę dla Twojej subskrypcji zdarzeń. |
   | | | 

   Gdy wszystko będzie gotowe, wyzwalacz siatki zdarzeń może wyglądać w tym przykładzie:
   
   ![Przykład zdarzeń wyzwalacza siatki](./media/monitor-virtual-machine-changes-event-grid-logic-app/logic-app-event-grid-trigger-details.png)

9. Zapisz aplikację logiki. Na pasku narzędzi Projektanta hello, wybierz **zapisać**. toocollapse i Ukryj szczegóły akcji w aplikacji logiki, wybierz pasek tytułu hello akcji.

   ![Zapisywanie aplikacji logiki](./media/monitor-virtual-machine-changes-event-grid-logic-app/logic-app-event-grid-save.png)

   Przy zapisywaniu aplikację logiki wyzwalacza siatki zdarzeń, Azure automatycznie tworzy subskrypcji zdarzeń dla zasobu tooyour wybrane aplikacji logiki. Dlatego podczas zasobów hello publikuje zdarzeń toohello zdarzeń siatki, tej siatki zdarzeń automatycznie wypycha hello zdarzeń tooyour logiki aplikacji. To zdarzenie wyzwala aplikację logiki, a następnie tworzy i uruchomione jest wystąpienie przepływu pracy hello, zdefiniowanego w tych kroków.

Aplikację logiki jest teraz na żywo i nasłuchuje tooevents z hello zdarzeń siatki, ale nic nie robi do momentu dodania toohello działań w przepływie pracy. 

## <a name="add-a-condition-that-checks-for-virtual-machine-changes"></a>Dodaj warunek, który sprawdza, czy zmiany maszyny wirtualnej

toorun przepływu aplikacji logiki tylko wtedy, gdy występuje określonego zdarzenia, Dodaj warunek, który sprawdza dla maszyny wirtualnej "" operacji zapisu. Jeśli ten warunek jest spełniony, aplikację logiki wysyła wiadomości e-mail ze szczegółami hello zaktualizować maszyny wirtualnej.

1. W Projektancie aplikacji logiki, w obszarze hello wyzwalacza siatki zdarzenia, wybierz **nowy krok** > **Dodaj warunek**.

   ![Dodaj warunek tooyour aplikacji logiki](./media/monitor-virtual-machine-changes-event-grid-logic-app/logic-app-event-grid-add-condition-step.png)

   Witaj projektanta aplikacji logiki dodaje pusty warunku tooyour przepływu pracy, zawierającą toofollow ścieżki akcji na podstawie czy hello warunku jest PRAWDA lub FAŁSZ.

   ![Pusty warunku](./media/monitor-virtual-machine-changes-event-grid-logic-app/logic-app-add-empty-condition.png)

2. W hello **warunku** wybierz **edytowanie w trybie zaawansowanym**.
Wprowadź wyrażenie:

   `@equals(triggerBody()?['data']['operationName'], 'Microsoft.Compute/virtualMachines/write')`

   Warunek teraz wygląda następująco:

   ![Pusty warunku](./media/monitor-virtual-machine-changes-event-grid-logic-app/logic-app-condition-expression.png)

   To wyrażenie sprawdza zdarzeń hello `body` dla `data` obiektów, których hello `operationName` właściwość jest hello `Microsoft.Compute/virtualMachines/write` operacji. 
   Dowiedz się więcej o [schematu zdarzeń siatki zdarzeń](../event-grid/event-schema.md).

3. Opis warunku hello tooprovide wybierz hello **wielokropek** (**...** ) znajdującego się na powitania kształt warunku, a następnie wybierz pozycję **zmienić**.

   > [!NOTE] 
   > Witaj nowsze przykłady w tym samouczku również zawierają opisy kroków w przepływie pracy aplikacji logiki hello.

4. Teraz wybierz **edytowania w trybie podstawowe** tak, aby wyrażenie hello automatycznie rozwiązuje, jak pokazano:

   ![Stan aplikacji logiki](./media/monitor-virtual-machine-changes-event-grid-logic-app/logic-app-condition-1.png)

5. Zapisz aplikację logiki.

## <a name="send-email-when-your-virtual-machine-changes"></a>Wyślij wiadomość e-mail, gdy zmienia się na komputerze wirtualnym

Teraz Dodaj [ *akcji* ](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts) tak, aby pobrać wiadomość e-mail, gdy hello określony warunek jest spełniony.

1. W warunku hello **w przypadku wartości PRAWDA** wybierz **Dodaj akcję**.

   ![Dodaj akcję dla gdy warunek ma wartość true](./media/monitor-virtual-machine-changes-event-grid-logic-app/logic-app-condition-2.png)

2. W polu wyszukiwania hello wprowadź "e-mail" jako filtr. W oparciu o dostawcę poczty e-mail, Znajdź i zaznacz pozycję hello pasującego łącznika. Następnie wybierz akcję "Wyślij wiadomość e-mail" hello, dla Twojego łącznika. Na przykład: 

   * Platformy Azure konto służbowe, wybierz hello łącznika programu Outlook pakietu Office 365. 
   * W przypadku osobistego konta Microsoft należy wybrać hello Outlook.com łącznika. 
   * W przypadku kont usługi Gmail wybierz łącznik usługi Gmail hello. 

   Chcemy toocontinue hello łącznik programu Outlook pakietu Office 365. 
   Użycie innego dostawcy, powitalne kroki hello takie same, ale interfejsu użytkownika może wyglądać inaczej. 

   ![Wybierz akcję "Wyślij wiadomość e-mail"](./media/monitor-virtual-machine-changes-event-grid-logic-app/logic-app-send-email.png)

3. Jeśli masz już połączenia dla dostawcy usługi poczty e-mail, zaloguj się na koncie e-mail tooyour, pytanie uwierzytelniania.

4. Podaj szczegóły hello poczty e-mail, jak określono w hello w poniższej tabeli:

   ![Akcja pusty poczty e-mail](./media/monitor-virtual-machine-changes-event-grid-logic-app/logic-app-empty-email-action.png)

   > [!TIP]
   > tooselect z pola dostępne w przepływie pracy, kliknij w polu edycji tak że hello **zawartości dynamicznej** liście otwiera lub wybierz **dodać zawartość dynamiczną**. Więcej pól, wybierz **zobaczyć więcej** dla każdej sekcji hello na liście. Witaj tooclose **zawartości dynamicznej** wybierz **dodać zawartość dynamiczną**.

   | Ustawienie | Sugerowana wartość | Opis | 
   | ------- | --------------- | ----------- | 
   | **Aby** | *{odbiorcy — adres e-mail}* |Wprowadź adres e-mail adresata hello. Do celów testowych, można użyć adresu e-mail. | 
   | **Temat** | Zasób zaktualizowane: **podmiotu**| Wprowadź wiadomość hello e-mail temat hello zawartości. W tym samouczku, wprowadź hello sugerowane tekstu i wybierz hello zdarzeń **podmiotu** pola. W tym miejscu temat wiadomości e-mail zawiera hello nazwy zasobu hello zaktualizowane (maszyny wirtualnej). | 
   | **Treści** | Grupa zasobów: **tematu** <p>Typ zdarzenia: **typ zdarzenia**<p>Identyfikator zdarzenia: **ID**<p>Czas: **czas trwania zdarzenia** | Wprowadź treść wiadomości powitania e-mail hello zawartości. W tym samouczku, wprowadź hello sugerowane tekstu i wybierz hello zdarzeń **tematu**, **typ zdarzenia**, **identyfikator**, i **czas trwania zdarzenia** pola, aby adres e-mail zawiera nazwa grupy zasobów hello, typu zdarzenia, sygnatura czasowa zdarzenia i identyfikator zdarzenia hello aktualizacji. <p>tooadd puste wiersze w zawartości, naciśnij klawisze Shift + Enter. | 
   | | | 

   > [!NOTE] 
   > Po zaznaczeniu pola, które reprezentuje tablicę, Projektant hello automatycznie dodaje **dla każdego** wokół hello akcję, która odwołuje się do tablicy hello pętlę. W ten sposób aplikację logiki wykonuje tego działania na każdy element tablicy.

   Twoja Akcja poczty e-mail może wyglądać tak jak w tym przykładzie:

   ![Wybierz tooinclude dane wyjściowe w wiadomości e-mail](./media/monitor-virtual-machine-changes-event-grid-logic-app/logic-app-send-email-details.png)

   I aplikację logiki Zakończono może wyglądać następująco:

   ![Zakończono logiki aplikacji](./media/monitor-virtual-machine-changes-event-grid-logic-app/logic-app-completed.png)

5. Zapisz aplikację logiki. toocollapse i Ukryj szczegóły każdej akcji w aplikacji logiki, wybierz pasek tytułu hello akcji.

   ![Zapisywanie aplikacji logiki](./media/monitor-virtual-machine-changes-event-grid-logic-app/logic-app-event-grid-save-completed.png)

   Aplikację logiki jest teraz na żywo, ale oczekuje na maszynie wirtualnej tooyour zmiany przed wykonaniem jakichkolwiek. 
   tootest aplikację logiki, kontynuowana toohello następnej sekcji.

## <a name="test-your-logic-app-workflow"></a>Testowanie przepływu pracy aplikacji logiki

1. czy aplikacji logiki będzie niedługo hello toocheck określone zdarzenia, zaktualizuj maszynę wirtualną. 

   Na przykład można zmienić rozmiar maszyny wirtualnej w portalu Azure hello lub [Zmień rozmiar maszyny Wirtualnej przy użyciu programu Azure PowerShell](../virtual-machines/windows/resize-vm.md). 

   Po kilku chwilach otrzymasz wiadomość e-mail. Na przykład:

   ![Wyślij wiadomość e-mail o aktualizacji maszyny wirtualnej](./media/monitor-virtual-machine-changes-event-grid-logic-app/email.png)

2. Uruchamia tooreview hello i historię wyzwalacza aplikacji logiki, w menu aplikacji logiki, wybierz **omówienie**. tooview więcej szczegółów na temat wykonywania, wybierz wiersz hello do uruchomienia.

   ![Historia uruchomieniu aplikacji logiki](./media/monitor-virtual-machine-changes-event-grid-logic-app/logic-app-run-history.png)

3. tooview hello wejścia i wyjścia dla każdego kroku rozwiń krok hello, które mają tooreview. Te informacje ułatwiają diagnozowanie i debugowania problemów w aplikacji logiki.
 
   ![Szczegóły historii uruchomienia aplikacji logiki](./media/monitor-virtual-machine-changes-event-grid-logic-app/logic-app-run-history-details.png)

Gratulacje, utworzeniu i uruchom aplikację logiki, który monitoruje zdarzenia zasobów za pomocą siatki zdarzeń i wiadomości e-mail możesz przypadku tych zdarzeń. Również wiesz, jak łatwo mogą tworzyć przepływy pracy, które automatyzację procesów i integrować systemy oraz usług w chmurze.

## <a name="clean-up-resources"></a>Oczyszczanie zasobów

Ten samouczek używa zasobów i wykonuje akcje, które naliczenie opłat w ramach subskrypcji platformy Azure. Dlatego po zakończeniu korzystania z samouczka hello i testowania, upewnij się, zostanie wyłączone lub usunięcie wszystkich zasobów, których nie chcesz tooincur opłat.

Można zatrzymać aplikację logiki z systemem i wysyłania wiadomości e-mail bez usuwania aplikacji hello. W menu aplikacji logiki, wybierz **omówienie**. Na pasku narzędzi hello, wybierz **wyłączyć**.

![Wyłącz aplikację logiki](./media/monitor-virtual-machine-changes-event-grid-logic-app/turn-off-disable-logic-app.png)

## <a name="faq"></a>Często zadawane pytania

**Q**: jakie inne maszyny wirtualnej, monitorowanie zadań można wykonywać z użyciem siatki zdarzeń i logic apps? </br>
**A**: można monitorować inne zmiany w konfiguracji, na przykład:

* Maszyna wirtualna uzyskuje dostęp opartej na rolach prawa kontroli (RBAC).
* Zmiany zostały wprowadzone tooa sieciowej grupy zabezpieczeń (NSG) dla interfejsu sieciowego (NIC).
* Dysków dla maszyny wirtualnej są dodawane lub usuwane.
* Publiczny adres IP jest przypisany tooa maszyny wirtualnej karty sieciowej.

## <a name="next-steps"></a>Następne kroki

* [Przegląd zdarzeń siatki](../event-grid/overview.md)
* [Pojęcia dotyczące siatki zdarzeń](../event-grid/concepts.md)
* [Szybki Start: Tworzenie i trasy zdarzeń niestandardowych zdarzeń siatki](../event-grid/custom-event-quickstart.md)
* [Schematu zdarzeń siatki zdarzeń](../event-grid/event-schema.md)
* [Azure Logic Apps](../logic-apps/logic-apps-what-are-logic-apps.md)
* [Tworzenie przepływów pracy aplikacji logiki z wstępnie zdefiniowanych szablonów](../logic-apps/logic-apps-use-logic-app-templates.md)