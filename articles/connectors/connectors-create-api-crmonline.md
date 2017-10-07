---
title: "aaaConnect tooDynamics 365 (online) z usługi Azure Logic Apps | Dokumentacja firmy Microsoft"
description: "Tworzenie przepływów pracy aplikacji, które zarządzają Dynamics 365 jednostek (online) za pośrednictwem interfejsu API dostarczonych przez łącznik hello Dynamics 365 hello logiki"
services: logic-apps
cloud: Azure Stack
author: Mattp123
manager: anneta
documentationcenter: 
tags: connectors
ms.assetid: 0dc2abef-7d2c-4a2d-87ca-fad21367d135
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/10/2017
ms.author: matp; LADocs
ms.openlocfilehash: 183d7a6b8e5d2c0eecc70da0da3806e06c382df4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="connect-toodynamics-365-from-logic-app-workflows"></a>Łączenie z tooDynamics 365 z przepływów pracy aplikacji logiki

Z usługą Logic Apps możesz łączyć tooDynamics 365 (online) i tworzyć przepływy przydatne biznesowe, które tworzenie rekordów, aktualizowania elementów lub powrócić do listy rekordów. Łącznik hello Dynamics 365 możesz:

* Tworzenie sieci przepływu biznesowe na podstawie danych hello, uzyskasz od Dynamics 365 (online).
* Użyj akcji, które odpowiedzi, a następnie wprowadź dane wyjściowe hello dostępne dla innych działań. Na przykład po zaktualizowaniu elementu w 365 Dynamics (online), możesz wysłać wiadomość e-mail przy użyciu usługi Office 365.

W tym temacie pokazano, jak toocreate aplikacji logiki tworzącą zadania w Dynamics 365 po każdej zmianie nowego potencjalnego klienta jest tworzony w Dynamics 365.

## <a name="prerequisites"></a>Wymagania wstępne
* Konto platformy Azure.
* Dynamics 365 konta (online).

## <a name="create-a-task-when-a-new-lead-is-created-in-dynamics-365"></a>Utwórz zadania, podczas tworzenia nowego potencjalnego klienta w Dynamics 365

1.  [Zaloguj się tooAzure](https://portal.azure.com).

2.  W usłudze Azure search hello, wpisz `Logic apps`, i naciśnij klawisz ENTER.

      ![Znajdź Logic Apps](./media/connectors-create-api-crmonline/find-logic-apps.png)

3.  W obszarze **Logic apps**, kliknij przycisk **Dodaj**.

      ![Dodaj LogicApp](./media/connectors-create-api-crmonline/add-logic-app.png)

4.  toocreate hello logiki aplikacji hello pełną **nazwa**, **subskrypcji**, **grupy zasobów**, i **lokalizacji** pola, a następnie kliknij przycisk  **Utwórz**.

5.  Wybierz hello nowej aplikacji logiki. Po otrzymaniu hello **Zakończono pomyślnie wdrażanie** powiadomień, kliknij przycisk **Odśwież**.

6.  W obszarze **narzędzi programistycznych**, kliknij przycisk **projektanta aplikacji logiki**. Kliknij na liście szablon hello **pustą aplikację logiki**.

7.  W polu wyszukiwania hello wpisz `Dynamics 365`. Z hello Dynamics 365 wyzwala listy, wybierz **Dynamics 365 — po utworzeniu rekordu**.

8.  Jeśli zostanie wyświetlony monit o toosign w tooDynamics 365, należy to zrobić teraz.

9.  W szczegółach wyzwalacza hello wprowadź hello następujących informacji:

  * **Nazwa organizacji**. Wybierz wystąpienia Dynamics 365 hello, które ma toolisten aplikacji logiki hello do.

  * **Nazwa jednostki**. Wybierz jednostki hello, który ma toolisten do. To zdarzenie działa jako aplikacji logiki hello toostart wyzwalacza. 
  W tym przewodniku **prowadzi** jest zaznaczone.

  * **Jak często mają toocheck dla elementów** Te wartości Ustaw częstotliwość aplikacji logiki hello sprawdza, czy aktualizacje pokrewne toohello wyzwalacza. ustawienie domyślne Hello jest toocheck aktualizacje co trzy minuty.

    * **Częstotliwość**. Wybierz sekundy, minuty, godziny lub dni.

    * **Interwał**. Wprowadź liczbę hello sekundy, minuty, godziny lub dni, które mają toopass przed hello następnego zaewidencjonowania.

      ![Szczegóły wyzwalaczem aplikacji logiki](./media/connectors-create-api-crmonline/trigger-details.png)

10. Kliknij przycisk **nowy krok**, a następnie kliknij przycisk **Dodaj akcję**.

11. W polu wyszukiwania hello wpisz `Dynamics 365`. Wybierz z listy akcji hello **Dynamics 365 — Utwórz nowy rekord**.

12. Wprowadź hello następujących informacji:

    * **Nazwa organizacji**. Wybierz wystąpienie hello Dynamics 365 miejscu hello przepływu toocreate hello rekordu. 
    Powiadomienie, że to wystąpienie nie ma toobe hello sam gdzie hello zdarzenie zostanie wyzwolone z wystąpienia.

    * **Nazwa jednostki**. Wybierz jednostki hello mają toocreate rekordu, po wyzwoleniu hello zdarzenia. 
    W tym przewodniku **zadania** jest zaznaczone.

13. Kliknij hello **podmiotu** pojawi się okno. Z hello dynamicznej zawartości listy możesz wybrać jedną z tych pól:

    * **Nazwisko**. Zaznaczenie tego pola wstawia hello nazwisko potencjalnego powitania klienta do hello pole tematu dla zadania hello, po utworzeniu rekordu zadań hello.
    * **Temat**. Zaznaczenie tego pola pola wstawia hello tematu dla realizacji hello w polu podmiotu hello hello zadania po hello zadań zostaje utworzony rekord. 
    Kliknij przycisk **tematu** tooadd tego toohello **podmiotu** pole.

      ![Logiki aplikacji Utwórz nowe szczegóły rekordu](./media/connectors-create-api-crmonline/create-record-details.png)

14. Na powitania narzędzi Projektanta aplikacji logiki, kliknij przycisk **zapisać**.

    ![Narzędzi Projektanta aplikacji logiki Zapisz](./media/connectors-create-api-crmonline/designer-toolbar-save.png)

15. Witaj toostart aplikacji logiki, kliknij przycisk **Uruchom**.

    ![Narzędzi Projektanta aplikacji logiki Zapisz](./media/connectors-create-api-crmonline/designer-toolbar-run.png)

16. Teraz Utwórz rekord realizacji w 365 Dynamics działu sprzedaży i zobacz Twojej przepływu w akcji!

## <a name="set-advanced-options-for-a-logic-app-step"></a>Ustaw opcje zaawansowane kroku aplikacji logiki

toospecify jak toofilter danych w kroku aplikacji logiki, kliknij przycisk **Pokaż zaawansowane opcje** w tym kroku, następnie dodać filtr lub kolejności przez zapytanie.

Na przykład można użyć filtru kont tylko aktywnych tooget zapytania i kolejność według nazwy konta hello. tooperform to zadanie, wprowadź zapytanie filtru OData hello `statuscode eq 1`i wybierz **nazwa konta** z hello listy zawartości dynamicznej. Więcej informacji: [MSDN: $filter](https://msdn.microsoft.com/library/gg309461.aspx#Anchor_1) i [$orderby](https://msdn.microsoft.com/library/gg309461.aspx#Anchor_2).

![Zaawansowane opcje aplikacji logiki](./media/connectors-create-api-crmonline/advanced-options.png)

### <a name="best-practices-when-using-advanced-options"></a>Najlepsze rozwiązania przy użyciu opcji zaawansowanych

Po dodaniu pola tooa wartości musi odpowiadać typowi pola hello, wpisz wartość lub wybierz wartość z listy hello dynamicznej zawartości.

Typ pola  |Jak toouse  |Gdzie toofind  |Nazwa  |Typ danych  
---------|---------|---------|---------|---------
Pola tekstowe|Pola tekstowe wymagają pojedynczy wiersz tekstu lub zawartość dynamiczną, która jest polem typu tekst. Przykładami pola kategorii i podkategorii hello.|Ustawienia > dostosowania > Dostosuj hello systemu > jednostki > zadań > pól |category |Pojedynczy wiersz tekstu        
Pola Liczba całkowita | Niektóre pola wymagają liczbą całkowitą lub zawartość dynamiczną, która jest typu Integer. Przykładami procent wykonania i czasu trwania. |Ustawienia > dostosowania > Dostosuj hello systemu > jednostki > zadań > pól |ProcentWykonania |Liczby całkowitej         
Pola dat | Niektóre pola wymagają datę wprowadzenia w formacie mm/dd/rrrr lub zawartość dynamiczną, która jest pola typu daty. Przykładami utworzenia, datę rozpoczęcia, Rozpoczęcie rzeczywiste ostatnio na czas przechowywania, rzeczywiste zakończenie i terminu. | Ustawienia > dostosowania > Dostosuj hello systemu > jednostki > zadań > pól |pól createdon |Data i godzina
Typ pola, które wymagają zarówno Identyfikatora rekordu i wyszukiwania |Niektóre pola, które odwołują się do innego rekordu jednostki wymagają zarówno identyfikator rekordu hello i hello typ wyszukiwania. |Ustawienia > dostosowania > Dostosuj hello systemu > jednostki > konto > pól  | AccountID  | Klucz podstawowy

### <a name="more-examples-of-fields-that-require-both-a-record-id-and-lookup-type"></a>Wpisz więcej przykładów dotyczących pola, które wymagają identyfikator rekordu i wyszukiwania
Rozszerzając hello poprzedniej tabeli, Oto przykłady więcej pól, które nie działają z wartościami wybrany z listy zawartości dynamicznej hello. Zamiast tego te pola wymagają zarówno identyfikator i wyszukiwania typ rekordu wprowadzany do pól hello w rozwiązaniu PowerApps.  
* Właściciel i typ właściciela. pole właściciela Hello musi zawierać prawidłowy identyfikator rekordu użytkownika lub zespołu Hello właściciela typu musi być równa albo **systemusers** lub **zespołów**.
* Klienta i typ klienta. powitania klienta pola musi być prawidłowym kontem lub skontaktuj się z identyfikator rekordu. Hello właściciela typu musi być równa albo **kont** lub **kontaktów**.
* Dotyczące oraz dotyczące typu. Witaj dotyczących pola musi być prawidłowy rekord identyfikator, takie jak konto lub skontaktuj się z identyfikator rekordu. Hello dotyczące typ musi być typ wyszukiwania hello hello rekordu, takich jak **kont** lub **kontaktów**.

Witaj poniższy przykład akcji tworzenia zadań dodaje odpowiadający toohello identyfikator rekordu, dodając toohello dotyczących pola hello zadania konta.

![Konto przepływu recordId i typ](./media/connectors-create-api-crmonline/recordid-type-account.png)

W tym przykładzie przypisuje także hello zadań tooa określonego użytkownika na podstawie identyfikatora użytkownika hello rekordu.

![Konto przepływu recordId i typ](./media/connectors-create-api-crmonline/recordid-type-user.png)

toofind rekordu przez identyfikator, zobacz hello następujących sekcji: *Znajdź identyfikator rekordu hello*

## <a name="find-hello-record-id"></a>Znajdź identyfikator rekordu hello

1. Otwórz rekord, takich jak konta.

2. Na pasku narzędzi Akcje hello, kliknij przycisk **Pop limit** ![rekordu podręczne](./media/connectors-create-api-crmonline/popout-record.png).
Alternatywnie na powitania akcje narzędzi toocopy hello pełny adres URL do domyślnego programu poczty e-mail, kliknij **łącze E-mail**.

   Identyfikator rekordu Hello jest wyświetlany Between hello % 7b i %7 d kodowania znaków hello adresu URL.

   ![Konto przepływu recordId i typ](./media/connectors-create-api-crmonline/recordid.png)

## <a name="troubleshooting"></a>Rozwiązywanie problemów
tootroubleshoot krok zakończony niepowodzeniem w aplikacji logiki, Wyświetl szczegóły stanu hello hello zdarzenia.

1. W obszarze **Logic Apps**, wybierz aplikację logiki, a następnie kliknij przycisk **omówienie**. 

   Hello obszar Podsumowanie zawiera stan hello uruchamiania dla aplikacji logiki hello, jest wyświetlany. 

   ![Stan uruchomienia aplikacji logiki](./media/connectors-create-api-crmonline/tshoot1.png)

2. tooview więcej informacji na temat dowolnego przebiegów nie powiodło się, kliknij przycisk hello nie powiodło się zdarzenia. tooexpand krok zakończony niepowodzeniem, kliknij ten krok.

   ![Rozwiń węzeł krok zakończony niepowodzeniem](./media/connectors-create-api-crmonline/tshoot2.png)

   szczegółowe informacje krok Hello wyświetlane i mogą pomóc rozwiązać hello przyczynę błędu na powitania.

   ![Nie można uzyskać szczegółowe informacje krok](./media/connectors-create-api-crmonline/tshoot3.png)

Aby uzyskać więcej informacji na temat rozwiązywania problemów z aplikacji logiki, zobacz [diagnozowanie błędów aplikacji logiki](../logic-apps/logic-apps-diagnosing-failures.md).

## <a name="connector-specific-details"></a>Szczegóły dotyczące łącznika

Wyświetl wszystkie wyzwalacze i akcje zdefiniowane w hello swagger i zobacz też żadnych limitów w hello [szczegóły łącznika](/connectors/crm/). 

## <a name="next-steps"></a>Następne kroki
Eksploruj hello innych dostępnych łączników w aplikacjach logiki w naszym [listy interfejsów API](apis-list.md).
