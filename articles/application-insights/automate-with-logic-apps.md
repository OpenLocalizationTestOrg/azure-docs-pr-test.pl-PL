---
title: "aaaAutomate Azure Application Insights przetwarza przy użyciu Logic Apps."
description: "Dowiedz się, jak szybko można zautomatyzować powtarzalnych procesów przez dodanie aplikacji logiki tooyour hello usługi Application Insights łącznika."
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 06/29/2017
ms.author: bwren
ms.openlocfilehash: 8565aadf0644ffb10da8a0964821901907db2e27
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="automate-application-insights-processes-by-using-logic-apps"></a>Zautomatyzować procesy usługi Application Insights przy użyciu aplikacji logiki

Czy zaczniesz wielokrotnie systemem hello tego samego zapytania z toocheck danych telemetrycznych czy usługa działa prawidłowo? Następnie tworzenia własnych przepływów pracy wokół nich i są wyglądającej tooautomate te zapytania do znajdowania trendów i anomalii? Hello łącznika usługi Azure Application Insights (wersja zapoznawcza) dla usługi Logic Apps jest hello właściwych narzędzi, w tym celu.

Dzięki tej integracji można zautomatyzować wiele procesów bez pisania pojedynczy wiersz kodu. Możesz utworzyć aplikację logiki za pomocą usługi Application Insights hello tooquickly łącznika automatyzować każdy proces usługi Application Insights. 

Można dodać również dodatkowe akcje. Funkcja Logic Apps Hello Azure App Service udostępnia setki akcje. Na przykład za pomocą aplikacji logiki, możesz można automatycznie wysłać wiadomość e-mail z powiadomieniem lub tworzenie usterki w programie Visual Studio Team Services. Umożliwia także jedną hello wiele dostępnych [szablony](https://docs.microsoft.com/azure/logic-apps/logic-apps-use-logic-app-templates) toohelp przyspieszenia hello proces tworzenia aplikacji logiki. 

## <a name="create-a-logic-app-for-application-insights"></a>Tworzenie aplikacji logiki do usługi Application Insights

Z tego samouczka dowiesz się, jak toocreate aplikacji logiki, który używa hello Analytics autocluster algorytm toogroup atrybutów w hello danych dla aplikacji sieci web. Przepływ Hello automatycznie wysyła wyników hello za pośrednictwem poczty e-mail, tylko jeden przykład sposobu użycia Application Insights analizy i Logic Apps razem. 

### <a name="step-1-create-a-logic-app"></a>Krok 1: Tworzenie aplikacji logiki
1. Zaloguj się toohello [portalu Azure](https://portal.azure.com).
2. W hello **nowy** okienku wybierz **sieci Web i mobilność**, a następnie wybierz **aplikacji logiki**.

    ![Nowe okno aplikacji logiki](./media/automate-with-logic-apps/logicapp1.png)

### <a name="step-2-create-a-trigger-for-your-logic-app"></a>Krok 2: Tworzenie aplikacji logiki wyzwalacza
1. W hello **projektanta aplikacji logiki** okna, w obszarze **rozpoczynać wyzwalacz wspólnej**, wybierz pozycję **cyklu**.

    ![Okna Projektant aplikacji logiki](./media/automate-with-logic-apps/logicapp2.png)

2. W hello **częstotliwość** wybierz opcję **dzień** , a następnie w hello **interwał** wpisz **1**.

    ![Projektant aplikacji logiki "Cyklu" okna](./media/automate-with-logic-apps/step2b.png)

### <a name="step-3-add-an-application-insights-action"></a>Krok 3: Dodaj akcję usługi Application Insights
1. Kliknij przycisk **nowy krok**, a następnie kliknij przycisk **Dodaj akcję**.

2. W hello **wybierz akcję** pole wyszukiwania, wpisz **Azure Application Insights**.

3. W obszarze **akcje**, kliknij przycisk **Azure Application Insights — wizualizacji analizy zapytania Podgląd**.

    ![Okno "Wybierz akcję" Projektant aplikacji logiki](./media/automate-with-logic-apps/flow2.png)

### <a name="step-4-connect-tooan-application-insights-resource"></a>Krok 4: Łączenie tooan zasobu usługi Application Insights

toocomplete ten krok, potrzebne są identyfikator i klucz interfejsu API dla zasobu. Można je pobrać od hello portalu Azure, jak pokazano w powitania po diagramu:

![Identyfikator aplikacji w portalu Azure hello](./media/automate-with-logic-apps/appid.png) 

Podaj nazwę dla połączenia, identyfikator aplikacji hello i hello klucz interfejsu API.

![Logika Projektant aplikacji przepływu połączenia okna](./media/automate-with-logic-apps/flow3.png)

### <a name="step-5-specify-hello-analytics-query-and-chart-type"></a>Krok 5: Określ hello Analytics zapytania i typ wykresu
W hello poniższy przykład zapytania hello wybiera w hello ostatni dzień żądania hello nie powiodło się i są powiązane z nimi wyjątków, które wystąpiły w ramach operacji hello. Żądania hello nie powiodło się, na podstawie identyfikatora operation_Id hello są powiązane z analizy. Zapytanie Hello następnie segmenty hello wyniki za pomocą algorytmu autocluster hello. 

Podczas tworzenia własnych zapytań, sprawdź, czy działają prawidłowo w module analiz przed dodaniem tooyour przepływu.

1. W hello **zapytania** Dodaj hello następującego zapytania Analytics: 

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

2. W hello **typ wykresu** wybierz opcję **tabeli Html**.

    ![Okno konfiguracji kwerendy analityka](./media/automate-with-logic-apps/flow4.png)

### <a name="step-6-configure-hello-logic-app-toosend-email"></a>Krok 6: Konfigurowanie hello logiki aplikacji toosend w wiadomości e-mail

1. Kliknij przycisk **nowy krok**, a następnie wybierz **Dodaj akcję**.

2. W polu wyszukiwania hello wpisz **Office 365 Outlook**.

3. Kliknij przycisk **Office 365 Outlook — Wyślij usługi poczty e-mail**.

    ![Wybór Outlook pakietu Office 365](./media/automate-with-logic-apps/flow2b.png)

4. W hello **wysłać wiadomość e-mail** oknie hello następujące:

   a. Wpisz adres e-mail adresata hello hello.

   b. Wpisz temat hello poczty e-mail.

   c. Kliknij w dowolnym miejscu hello **treści** polu, a następnie na powitania dynamicznej zawartości wyświetlonym menu na powitania prawo, wybierz **treści**.

   d. Kliknij przycisk **Pokaż zaawansowane opcje**.

      ![Konfiguracja programu Outlook pakietu Office 365](./media/automate-with-logic-apps/flow5.png)

5. W menu hello dynamicznej zawartości hello następujące:

    a. Wybierz **Nazwa załącznika**.

    b. Wybierz **zawartości załącznika**.
    
    c. W hello **HTML jest** wybierz opcję **tak**.

      ![Ekran konfiguracji poczty e-mail usługi Office 365](./media/automate-with-logic-apps/flow7.png)

### <a name="step-7-save-and-test-your-logic-app"></a>Krok 7: Zapisz i przetestuj aplikację logiki
* Kliknij przycisk **zapisać** toosave zmiany.

Możesz poczekać aplikacji logiki hello toorun wyzwalacza hello, lub uruchom aplikację logiki hello natychmiast po wybraniu **Uruchom**.

![Ekran Tworzenie aplikacji logiki](./media/automate-with-logic-apps/step7.png)

Po uruchomieniu aplikacji logiki odbiorcy hello, określone na liście hello wiadomości e-mail będą otrzymywać wiadomości e-mail, która wygląda hello:

![Wiadomość e-mail aplikacji logiki](./media/automate-with-logic-apps/flow9.png)

## <a name="next-steps"></a>Następne kroki

- Dowiedz się więcej o tworzeniu [zapytania analityczne](app-insights-analytics-using.md).
- Dowiedz się więcej o [Logic Apps](https://docs.microsoft.com/azure/logic-apps/logic-apps-what-are-logic-apps).



<!--Link references-->





