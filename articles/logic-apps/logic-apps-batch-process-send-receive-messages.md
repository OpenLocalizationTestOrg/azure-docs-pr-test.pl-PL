---
title: "aaaBatch przetwarzania komunikatów przez grupę lub kolekcji — usługi Azure Logic Apps | Dokumentacja firmy Microsoft"
description: "Wysyłanie i odbieranie wiadomości dla przetwarzania wsadowego w aplikacji logiki"
keywords: partii, przetwarzanie wsadowe
author: jonfancey
manager: anneta
editor: 
services: logic-apps
documentationcenter: 
ms.assetid: 
ms.service: logic-apps
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/7/2017
ms.author: LADocs; estfan; jonfan
ms.openlocfilehash: 2603db71ee0659d5b6bf5ce3d32f1b0d13c34194
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="send-receive-and-batch-process-messages-in-logic-apps"></a>Wyślij, odbierania i partii przetwarzania komunikatów w aplikacji logiki

komunikaty tooprocess razem w grupach, możesz wysłać tooa danych zapasów lub komunikatów, *partii*, a następnie przetwarzania tych elementów jako plik wsadowy. Takie rozwiązanie jest przydatne, jeśli chcesz toomake się, że elementy danych są grupowane w szczególny sposób i wspólnego przetwarzania. 

Można tworzyć aplikacje logiki, które odbierają elementów jako plik wsadowy przy użyciu hello **partii** wyzwalacza. Umożliwia tworzenie aplikacji logiki, które wysyłania partii tooa elementów przy użyciu hello **partii** akcji.

W tym temacie pokazano, jak można tworzyć przetwarzanie wsadowe rozwiązanie, wykonując następujące zadania: 

* [Tworzenie aplikacji logiki, która odbiera i zbiera elementów jako plik wsadowy](#batch-receiver). Ta aplikacja logiki "partii odbiorcy" Określa hello partii nazwa i wersja kryteria toomeet przed aplikacji logiki odbiornika hello zwalnia i przetwarza elementy. 

* [Tworzenie aplikacji logiki wysyłanej partii tooa elementów](#batch-sender). Ta aplikacja logiki "partii sender" Określa, gdzie toosend elementów, które muszą być istniejących aplikacji logiki odbiornika partii. Można również określić unikatowy klucz, takich jak numer klienta, za "partycji" lub dzielenia partii docelowy hello na podzbiory na podstawie tego klucza. W ten sposób wszystkie elementy z tego klucza są zbierane i przetwarzane razem. 

## <a name="requirements"></a>Wymagania

toofollow w tym przykładzie potrzebne następujące elementy:

* Subskrypcja platformy Azure. Jeśli nie masz subskrypcji, możesz [rozpocząć pracę z bezpłatnym kontem platformy Azure](https://azure.microsoft.com/free/). W przeciwnym razie możesz [skorzystać z subskrypcji z płatnością zgodnie z rzeczywistym użyciem](https://azure.microsoft.com/pricing/purchase-options/).

* Podstawową wiedzę na temat o [jak toocreate logic apps](../logic-apps/logic-apps-create-a-logic-app.md) 

* Konto e-mail ze wszystkimi [dostawcy poczty e-mail obsługiwane przez usługi Azure Logic Apps](../connectors/apis-list.md)

<a name="batch-receiver"></a>

## <a name="create-logic-apps-that-receive-messages-as-a-batch"></a>Tworzenie aplikacji logiki, który odbiera komunikaty jako partii

Przed wysłaniem wiadomości tooa partii, należy najpierw utworzyć aplikację logiki "partii odbiornika" z hello **partii** wyzwalacza. W ten sposób można wybrać tę aplikację logiki odbiornika podczas tworzenia aplikacji logiki hello nadawcy. Dla odbiornika hello należy określić nazwę usługi partia zadań hello, kryteriów wersji i inne ustawienia. 

Aplikacje logiki nadawcy musi wiedzieć, gdzie elementów toosend, podczas gdy aplikacje logiki odbiorcy nie muszą tooknow cokolwiek o nadawcy hello.

1. W hello [portalu Azure](https://portal.azure.com), tworzenie aplikacji logiki o tej nazwie: "BatchReceiver" 

2. W Projektancie aplikacji logiki, Dodaj hello **partii** wyzwalacza, która uruchamia przepływ pracy aplikacji logiki. W polu wyszukiwania hello wprowadź "partii" jako filtr. Wybierz ten wyzwalacz: **partii — komunikaty wsadowe**

   ![Dodaj wyzwalacza partii](./media/logic-apps-batch-process-send-receive-messages/add-batch-receiver-trigger.png)

3. Podaj nazwę dla partii hello i określ kryteria za zwolnienie hello partii, na przykład:

   * **Nazwa partii**: hello nazwę używaną tooidentify hello partii, czyli "TestBatch" w tym przykładzie.
   * **Liczba komunikatów**: hello liczbę wiadomości toohold jako partii przed zwolnieniem do przetwarzania, czyli "5" w tym przykładzie.

   ![Podaj szczegóły wyzwalacza partii](./media/logic-apps-batch-process-send-receive-messages/receive-batch-trigger-details.png)

4. Dodaj inną akcję, która wysyła wiadomość e-mail, gdy hello partii wyzwalacz. Każdej z partii hello czasu ma pięć elementów, aplikację logiki hello wysyła wiadomość e-mail.

   1. W obszarze hello partii wyzwalacza, wybierz **+ nowy krok** > **Dodaj akcję**.

   2. W polu wyszukiwania hello wprowadź "e-mail" jako filtr.
   W oparciu o dostawcę poczty e-mail, wybierz łącznik poczty e-mail.
   
      Na przykład jeśli masz konto służbowe, wybierz hello łącznika programu Outlook pakietu Office 365. 
      Jeśli masz konto usługi Gmail, wybierz łącznik usługi Gmail hello.

   3. Wybierz tę akcję dla Twojego łącznika:  **{*dostawcy e-mail*} — Wyślij e-mail **

      Na przykład:

      ![Wybierz akcję "Wyślij wiadomość e-mail" dla dostawcy usługi poczty e-mail](./media/logic-apps-batch-process-send-receive-messages/add-send-email-action.png)

5. Jeśli wcześniej nie utworzono połączenia dla dostawcy usługi poczty e-mail, wprowadź swoje poświadczenia poczty e-mail dla uwierzytelniania po wyświetleniu monitu. Dowiedz się więcej o [uwierzytelniania poświadczeń e-mail](../logic-apps/logic-apps-create-a-logic-app.md).

6. Ustaw właściwości hello akcji hello, który właśnie został dodany.

   * W hello **do** wprowadź adres e-mail adresata hello. 
   Do celów testowych, można użyć adresu e-mail.

   * W hello **podmiotu** polu, gdy hello **zawartości dynamicznej** zostanie wyświetlona lista, wybierz hello **nazwa partycji** pola.

     ![Z listy "Zawartość dynamiczna" hello wybierz "Nazwa partycji"](./media/logic-apps-batch-process-send-receive-messages/send-email-action-details.png)

     W dalszej części artykułu można określić klucz partycji unikatowy czy bez reszty hello partii docelowych do logicznego ustawia toowhere można wysyłać wiadomości. 
     Każdy zestaw ma unikatowy numer, który jest generowany przez aplikację logiki hello nadawcy. 
     Ta funkcja umożliwia pojedyncza partia za pomocą wielu podzestawy i zdefiniować każdy podzbiór o nazwie hello, podane.

   * W hello **treści** polu, gdy hello **zawartości dynamicznej** zostanie wyświetlona lista, wybierz hello **identyfikator komunikatu** pola.

     !["Identyfikator komunikatu" Wybierz "Treść"](./media/logic-apps-batch-process-send-receive-messages/send-email-action-details-for-each.png)

     Ponieważ dane wejściowe hello hello wysyłania wiadomości e-mail akcji jest tablicą, Projektant hello automatycznie dodaje **dla każdego** pętlę wokół hello **wysłać wiadomość e-mail** akcji. 
     Ta pętla wykonuje akcję wewnętrzny hello każdego elementu w partii hello. 
     Tak z zestawu elementów toofive hello wsadowych wyzwalacza, otrzymasz pięć wiadomości e-mail, które każdy czas hello wyzwalacza.

7.  Teraz, gdy utworzono aplikacji logiki odbiornika partii, Zapisz aplikację logiki.

    ![Zapisywanie aplikacji logiki](./media/logic-apps-batch-process-send-receive-messages/save-batch-receiver-logic-app.png)

<a name="batch-sender"></a>

## <a name="create-logic-apps-that-send-messages-tooa-batch"></a>Tworzenie aplikacji logiki, wysyłających komunikaty tooa partii

Teraz należy utworzyć co najmniej jedną aplikację logiki, wysyłających partii toohello elementy zdefiniowane przez aplikację logiki hello odbiornika. Dla hello nadawcy należy określić aplikację logiki odbiornika hello i nazwa usługi partia zadań, zawartość komunikatu i inne ustawienia. Opcjonalnie można podać partii partycji unikatowy kluczy toodivide hello na podzestawy toocollect elementy z tego klucza.

Aplikacje logiki nadawcy musi wiedzieć, gdzie elementów toosend, podczas gdy aplikacje logiki odbiorcy nie muszą tooknow cokolwiek o nadawcy hello.

1. Tworzenie aplikacji logiki innej o tej nazwie: "BatchSender"

   1. W polu wyszukiwania hello wprowadź "cyklu" jako filtr. 
   Wybierz ten wyzwalacz: **harmonogram - cyklu**

      ![Dodaj wyzwalacza hello "Harmonogram cyklu"](./media/logic-apps-batch-process-send-receive-messages/add-schedule-trigger-batch-receiver.png)

   2. Ustaw częstotliwość hello i aplikacji logiki nadawcy hello toorun interwał co minutę.

      ![Ustaw częstotliwość i interwał cyklu wyzwalacza](./media/logic-apps-batch-process-send-receive-messages/recurrence-trigger-batch-receiver-details.png)

2. Dodaj nowy krok do wysyłania wiadomości tooa partii.

   1. W obszarze hello cyklu wyzwalacza, wybierz **+ nowy krok** > **Dodaj akcję**.

   2. W polu wyszukiwania hello wprowadź "partii" jako filtr. 

   3. Wybierz tę akcję: **wysyłania wiadomości toobatch — wybierz przepływ pracy aplikacji logiki z wyzwalaczem partii**

      ![Zaznacz pole wyboru "Wyślij wiadomości toobatch"](./media/logic-apps-batch-process-send-receive-messages/send-messages-batch-action.png)

   4. Teraz wybierz "BatchReceiver" aplikację logiki utworzony wcześniej, która jest teraz wyświetlany jako akcja.

      ![Wybierz aplikację logiki "partii odbiornika"](./media/logic-apps-batch-process-send-receive-messages/send-batch-select-batch-receiver.png)

      > [!NOTE]
      > Lista Hello zawiera również wszystkie inne aplikacje logiki mających wyzwalaczy partii.

3. Ustaw właściwości partii hello.

   * **Nazwa partii**: Nazwa instancji hello zdefiniowane przez aplikację logiki odbiornika Witaj, "TestBatch" w tym przykładzie i sprawdzania poprawności w czasie wykonywania.

     > [!IMPORTANT]
     > Upewnij się, nie zmieniać hello partii nazwy, która musi odpowiadać nazwie partii hello, określonym przez aplikację logiki hello odbiornika.
     > Zmiana nazwy partii hello powoduje, że nadawca hello toofail aplikacji logiki.

   * **Zawartość komunikatu**: hello treści wiadomości, które mają toosend. 
   Na przykład dodać to wyrażenie, że wstawia hello bieżącą datę i godzinę do zawartości, że wysyłania partii toohello wiadomość hello:

     1. Gdy hello **zawartości dynamicznej** zostanie wyświetlona lista, wybierz **wyrażenia**. 
     2. Wprowadź wyrażenie hello **utcnow()**i wybierz polecenie **OK**. 

        ![W "Zawartość komunikatu" Wybierz opcję "Wyrażenie". Wprowadź "utcnow()".](./media/logic-apps-batch-process-send-receive-messages/send-batch-receiver-details.png)

4. Teraz należy skonfigurować partycji dla partii hello. Akcja "BatchReceiver" hello, wybierz **Pokaż zaawansowane opcje**.

   * **Nazwa partycji**: toouse klucza partycji unikatowy opcjonalne rozdzielania hello docelowy partii. Na przykład Dodaj wyrażenie, które generuje losową liczbę między jeden a pięć.
   
     1. Gdy hello **zawartości dynamicznej** zostanie wyświetlona lista, wybierz **wyrażenia**.
     2. Wprowadź wyrażenie: **rand(1,6)**

        ![Konfigurowanie partycji dla partii użytkownika docelowego](./media/logic-apps-batch-process-send-receive-messages/send-batch-receiver-partition-advanced-options.png)

        To **rand** funkcja generuje do zakresu od jednej do pięciu. 
        Dlatego są podzielenie tej partii na pięć numerowane partycje, które dynamicznie ustawia tego wyrażenia.

   * **Identyfikator wiadomości**: identyfikator komunikatu opcjonalne i jest generowanym identyfikatorze GUID, gdy parametr jest pusty. 
   W tym przykładzie pozostaw to pole puste.

5. Zapisz aplikację logiki. Aplikację logiki nadawcy wyglądają teraz podobny przykład toothis:

   ![Zapisz aplikację logiki nadawcy](./media/logic-apps-batch-process-send-receive-messages/send-batch-receiver-details-finished.png)

## <a name="test-your-logic-apps"></a>Testowanie aplikacji logiki

tootest Twojego przetwarzanie wsadowe rozwiązania, pozostaw aplikacje logiki uruchomione kilka minut. Po chwili uruchamiania uzyskiwania wiadomości e-mail w grupach pięć, wszystkie z hello partycji sam klucz.

Aplikację logiki BatchSender co minutę, generuje losową liczbę między jeden a pięć, korzysta to generowany numer jako klucza partycji hello partii docelowy hello wysyłania wiadomości. Zawsze partii hello zawiera pięć elementy z hello tym samym kluczem partycji aplikacji logiki BatchReceiver generowane i wysyła poczty dla każdego komunikatu.

> [!IMPORTANT]
> Po zakończeniu testowania, sprawdź, czy wyłączyć wysyłanie wiadomości powitania BatchSender logiki aplikacji toostop i nie przeciążać skrzynki odbiorczej.

## <a name="next-steps"></a>Następne kroki

* [Tworzenie w definicji aplikacji logiki za pomocą formatu JSON](../logic-apps/logic-apps-author-definitions.md)
* [Tworzenie aplikacji bez serwera w programie Visual Studio z usługi Azure Logic Apps i funkcje](../logic-apps/logic-apps-serverless-get-started-vs.md)
* [Obsługa wyjątków i rejestrowania błędów dla usługi logic apps](../logic-apps/logic-apps-scenario-error-and-exception-handling.md)
