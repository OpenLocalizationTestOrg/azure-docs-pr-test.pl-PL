---
title: aaaAutomate Azure Application Insights przetwarza z Flow firmy Microsoft
description: "Dowiedz się, jak używasz Microsoft Flow tooquickly zautomatyzować powtarzalnych procesów za pomocą łącznika usługi Application Insights hello."
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 06/25/2017
ms.author: bwren
ms.openlocfilehash: b34488a6b8b8b0a6add960a67f1426cbbbc13552
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="automate-azure-application-insights-processes-with-hello-connector-for-microsoft-flow"></a>Zautomatyzować procesy Azure Application Insights z łącznikiem hello Flow firmy Microsoft

Czy zaczniesz wielokrotnie systemem hello tego samego zapytania z toocheck danych telemetrii, że usługa działa prawidłowo? Następnie tworzenia własnych przepływów pracy wokół nich i są wyglądającej tooautomate te zapytania do znajdowania trendów i anomalii? Hello łącznika Azure Application Insights (wersja zapoznawcza) dla programu Microsoft Flow jest hello właściwych narzędzi dla tych celów.

Dzięki tej integracji teraz można zautomatyzować wiele procesów bez pisania pojedynczy wiersz kodu. Po utworzeniu przepływu za pomocą usługi Application Insights akcji przepływu hello automatycznie uruchamia kwerendy analizy Insights aplikacji. 

Można dodać również dodatkowe akcje. Microsoft Flow udostępnia setki akcje. Na przykład można użyć Microsoft Flow tooautomatically Wyślij wiadomość e-mail z powiadomieniem lub tworzenie usterki w programie Visual Studio Team Services. Umożliwia także jedną hello wiele [szablony](https://ms.flow.microsoft.com/en-us/connectors/shared_applicationinsights/?slug=azure-application-insights) dostępnych dla łącznika powitania dla Flow firmy Microsoft. Te szablony przyspieszyć proces hello tworzenia przepływu. 

<!--hello Application Insights connector also works with [Azure Power Apps](https://powerapps.microsoft.com/en-us/) and [Azure Logic Apps](https://azure.microsoft.com/services/logic-apps/?v=17.23h). --> 

## <a name="create-a-flow-for-application-insights"></a>Utwórz strumień dla usługi Application Insights

Z tego samouczka dowiesz się, jak toocreate przepływ, który używa hello Analytics klastra automatycznie algorytmu toogroup atrybutów w hello danych dla aplikacji sieci web. Przepływ Hello automatycznie wysyła wyników hello za pośrednictwem poczty e-mail, tylko jeden przykład sposobu użycia Flow firmy Microsoft i analizy aplikacji Insights ze sobą. 

### <a name="step-1-create-a-flow"></a>Krok 1: Tworzenie przepływu
1. Zaloguj się za[Microsoft Flow](http://flow.microsoft.com), a następnie wybierz **Moje przepływa**.
2. Kliknij przycisk **Utwórz przepływem na podstawie puste**.

### <a name="step-2-create-a-trigger-for-your-flow"></a>Krok 2: Tworzenie wyzwalacza dla Twojego przepływu
1. Wybierz **harmonogram**, a następnie wybierz **harmonogram - cyklu**.
2. W hello **częstotliwość** wybierz opcję **dzień**i w hello **interwał** wprowadź **1**.

    ![Okno dialogowe Microsoft Flow wyzwalacza](./media/app-insights-automate-with-flow/flow1.png)


### <a name="step-3-add-an-application-insights-action"></a>Krok 3: Dodaj akcję usługi Application Insights
1. Kliknij przycisk **nowy krok**, a następnie kliknij przycisk **Dodaj akcję**.
2. Wyszukaj **Azure Application Insights**.
3. Kliknij przycisk **Azure Application Insights — wizualizacji analizy zapytania Podgląd**.

    ![Uruchom okno kwerendy analityka](./media/app-insights-automate-with-flow/flow2.png)

### <a name="step-4-connect-tooan-application-insights-resource"></a>Krok 4: Łączenie tooan zasobu usługi Application Insights

toocomplete ten krok, potrzebne są identyfikator i klucz interfejsu API dla zasobu. Można je pobrać od hello portalu Azure, jak pokazano w powitania po diagramu:

![Identyfikator aplikacji w portalu Azure hello](./media/app-insights-automate-with-flow/appid.png) 

- Podaj nazwę dla połączenia, wraz z hello aplikacji identyfikator i klucz API.

    ![Okno połączenia Flow firmy Microsoft](./media/app-insights-automate-with-flow/flow3.png)

### <a name="step-5-specify-hello-analytics-query-and-chart-type"></a>Krok 5: Określ hello Analytics zapytania i typ wykresu
To przykładowe zapytanie wybiera w hello ostatni dzień żądania hello nie powiodło się i są powiązane z nimi wyjątków, które wystąpiły w ramach operacji hello. Analiza są powiązane z nimi na podstawie identyfikatora operation_Id hello. Zapytanie Hello następnie segmenty hello wyniki za pomocą algorytmu autocluster hello. 

Podczas tworzenia własnych zapytań, sprawdź, czy działają prawidłowo w module analiz przed dodaniem tooyour przepływu.

- Dodaj hello następującego zapytania Analytics, a następnie wybierz typ wykresu tabeli HTML hello. 

    ```
    requests
    | where timestamp > ago(1d)
    | where success == "False"
    | project name, operation_Id
    | join ( exceptions
        | project problemId, outerMessage, operation_Id
    ) on operation_Id
    | evaluate autocluster()
    ```
    
    ![Okno konfiguracji kwerendy analityka](./media/app-insights-automate-with-flow/flow4.png)

### <a name="step-6-configure-hello-flow-toosend-email"></a>Krok 6: Konfigurowanie hello przepływu toosend e-mail

1. Kliknij przycisk **nowy krok**, a następnie kliknij przycisk **Dodaj akcję**.
2. Wyszukaj **Outlook pakietu Office 365**.
3. Kliknij przycisk **Office 365 Outlook — Wyślij usługi poczty e-mail**.

    ![Okno wyboru Outlook pakietu Office 365](./media/app-insights-automate-with-flow/flow2b.png)

4. W hello **wysłać wiadomość e-mail** oknie hello następujące:

   a. Wpisz adres e-mail adresata hello hello.

   b. Wpisz temat hello poczty e-mail.

   c. Kliknij w dowolnym miejscu hello **treści** polu, a następnie na powitania dynamicznej zawartości wyświetlonym menu na powitania prawo, wybierz **treści**.

   d. Kliknij przycisk **Pokaż zaawansowane opcje**.

    ![Konfiguracja programu Outlook pakietu Office 365](./media/app-insights-automate-with-flow/flow5.png)

5. W menu hello dynamicznej zawartości hello następujące:

    a. Wybierz **Nazwa załącznika**.

    b. Wybierz **zawartości załącznika**.
    
    c. W hello **HTML jest** wybierz opcję **tak**.

    ![Okno Konfiguracja poczty e-mail usługi Office 365](./media/app-insights-automate-with-flow/flow7.png)

### <a name="step-7-save-and-test-your-flow"></a>Krok 7: Zapisz i testowania przepływu użytkownika
- W hello **nazwy przepływu** , Dodaj nazwę użytkownika przepływ, a następnie kliknij przycisk **utworzyć przepływ**.

    ![Tworzenie przepływu okna](./media/app-insights-automate-with-flow/flow8.png)

Możesz poczekać na powitania wyzwalacza toorun tej akcji, lub uruchomić przepływ hello natychmiast przez [uruchomionych wyzwalacza hello na żądanie](https://flow.microsoft.com/blog/run-now-and-six-more-services/).

Po uruchomieniu przepływu hello hello adresatów, określone na liście e-mail hello otrzymywać wiadomości e-mail, która wygląda hello:

![Przykładowej wiadomości e-mail](./media/app-insights-automate-with-flow/flow9.png)


## <a name="next-steps"></a>Następne kroki

- Dowiedz się więcej o tworzeniu [zapytania analityczne](app-insights-analytics-using.md).
- Dowiedz się więcej o [Microsoft Flow](https://ms.flow.microsoft.com).



<!--Link references-->





