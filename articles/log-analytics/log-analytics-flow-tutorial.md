---
title: "aaaAutomate Analiza dzienników Azure przetwarza z Flow firmy Microsoft"
description: "Dowiedz się, jak używasz Microsoft Flow tooquickly zautomatyzować powtarzalnych procesów za pomocą łącznika usługi Analiza dzienników Azure hello."
services: log-analytics
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.service: log-analytics
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 08/09/2017
ms.author: bwren
ms.openlocfilehash: 52026df968682842cc9f8d55f6f9875c5f9c10b1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="automate-log-analytics-processes-with-hello-connector-for-microsoft-flow"></a>Zautomatyzować procesy analizy dzienników z łącznikiem hello Flow firmy Microsoft
[Microsoft Flow](https://ms.flow.microsoft.com) pozwala toocreate automatycznego przepływów pracy za pomocą setki akcje do różnych usług. Dane wyjściowe z jedną akcję może służyć jako tooanother wejściowych, umożliwiając integrację toocreate różnych usług.  Łącznik usługi Analiza dzienników Azure powitania dla Microsoft Flow pozwalają toobuild przepływy pracy, które zawierają dane pobierane przez dziennik wyszukiwania analizy dzienników.

Na przykład można użyć danych analizy dzienników toouse Flow firmy Microsoft w wiadomość e-mail z powiadomieniem z usługi Office 365, tworzenie usterki w programie Visual Studio Team Services lub wysłać wiadomość Slack.  Przez harmonogram prosty lub niektóre akcje w podłączonej usługi takie jak po odebraniu wiadomości e-mail lub tweet, może wyzwolić przepływu pracy.  


> [!NOTE]
> Łącznik usługi Analiza dzienników Azure Hello dla Microsoft Flow wymaga obszaru roboczego toobe uaktualnione toohello nowego analizy dzienników zapytania języka. Możesz dowiedzieć się więcej o nowy język hello i uzyskać hello procedury tooupgrade obszaru roboczego na [uaktualnienia wyszukiwania dziennika toonew roboczym usługi Analiza dzienników Azure](log-analytics-log-search-upgrade.md).  

Samouczek Hello w tym artykule przedstawiono, jak toocreate przepływ, który automatycznie wysyła pocztą e-mail, tylko jeden przykład stosowania analizy dzienników w Microsoft Flow hello wyniki wyszukiwania dziennika analizy dzienników. 


## <a name="step-1-create-a-flow"></a>Krok 1: Tworzenie przepływu
1. Zaloguj się za[Microsoft Flow](http://flow.microsoft.com)i wybierz **Moje przepływa**.
2. Kliknij przycisk **+ Utwórz z puste**.

## <a name="step-2-create-a-trigger-for-your-flow"></a>Krok 2: Tworzenie wyzwalacza dla Twojego przepływu
1. Kliknij przycisk **wyszukiwania setki łączników i wyzwalaczy**.
2. Typ **harmonogram** hello pola wyszukiwania.
3. Wybierz **harmonogram**, a następnie wybierz **harmonogram - cyklu**.
4. W hello **częstotliwość** polu Wybierz **dzień** w hello **interwał** wprowadź **1**.<br><br>![Okno dialogowe Microsoft Flow wyzwalacza](media/log-analytics-flow-tutorial/flow01.png)


## <a name="step-3-add-a-log-analytics-action"></a>Krok 3: Dodaj akcję analizy dzienników
1. Kliknij przycisk **+ nowy krok**, a następnie kliknij przycisk **Dodaj akcję**.
2. Wyszukaj **dziennika analizy**.
3. Kliknij przycisk **Azure Log Analytics — uruchomić zapytanie i wizualizacja wyników**.<br><br>![Uruchom okno kwerendy analizy dzienników](media/log-analytics-flow-tutorial/flow02.png)

## <a name="step-4-configure-hello-log-analytics-action"></a>Krok 4: Konfigurowanie hello analizy dzienników akcji

1. Określ szczegóły hello obszaru roboczego, w tym hello subskrypcji identyfikator, grupy zasobów, a nazwa obszaru roboczego.
2. Dodaj powitania po toohello zapytania analizy dzienników **zapytania** okna.  To jest tylko przykładowe zapytanie i możesz zastąpić dowolne inne zwracające dane.
```
    Event
    | where EventLevelName == "Error" 
    | where TimeGenerated > ago(1day)
    | summarize count() by Computer
    | sort by Computerindow. 
```

2. Wybierz **tabeli HTML** dla hello **typ wykresu**.<br><br>![Dziennik akcji analityka](media/log-analytics-flow-tutorial/flow03.png)

## <a name="step-5-configure-hello-flow-toosend-email"></a>Krok 5: Konfigurowanie hello przepływu toosend e-mail

1. Kliknij przycisk **nowy krok**, a następnie kliknij przycisk **+ Dodaj akcję**.
2. Wyszukaj **Outlook pakietu Office 365**.
3. Kliknij przycisk **Office 365 Outlook — Wyślij usługi poczty e-mail**.<br><br>![Okno wyboru Outlook pakietu Office 365](media/log-analytics-flow-tutorial/flow04.png)

4. Określ adres e-mail adresata hello w hello **do** okno i temat wiadomości e-mail hello w **podmiotu**.
5. Kliknij w dowolnym miejscu hello **treści** pole.  A **zawartości dynamicznej** zostanie otwarte okno z wartości z poprzedniej akcji.  
6. Wybierz **treści**.  Jest to hello wyniki zapytania hello w hello analizy dzienników akcji.
6. Kliknij przycisk **Pokaż zaawansowane opcje**.
7. W hello **HTML jest** wybierz opcję **tak**.<br><br>![Okno Konfiguracja poczty e-mail usługi Office 365](media/log-analytics-flow-tutorial/flow05.png)

## <a name="step-6-save-and-test-your-flow"></a>Krok 6: Zapisz i testowania przepływu użytkownika
1. W hello **nazwy przepływu** , Dodaj nazwę użytkownika przepływ, a następnie kliknij przycisk **utworzyć przepływ**.<br><br>![Zapisywanie przepływu](media/log-analytics-flow-tutorial/flow06.png)
2. Hello przepływ został utworzony i zostanie uruchomiony po dniu, czyli hello harmonogramem. 
3. tooimmediately testu hello przepływu, kliknij przycisk **Uruchom teraz** , a następnie **uruchomienia przepływu**.<br><br>![Uruchamianie przepływu](media/log-analytics-flow-tutorial/flow07.png)
3. Po zakończeniu przepływu hello, Sprawdź pocztę hello hello adresata, określony.  Powinna zostać odebrana poczty następujący toohello podobne treści:<br><br>![Przykładowej wiadomości e-mail](media/log-analytics-flow-tutorial/flow08.png)


## <a name="next-steps"></a>Następne kroki

- Dowiedz się więcej o [Zaloguj wyszukiwania analizy dzienników](log-analytics-log-search-new.md).
- Dowiedz się więcej o [Microsoft Flow](https://ms.flow.microsoft.com).



