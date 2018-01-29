---
title: "Otrzymywanie powiadomienia w przypadku spełnienia określonego warunku przez wartość metryki | Microsoft Docs"
description: "Przewodnik Szybki start dotyczący tworzenia metryk dla aplikacji logiki"
author: anirudhcavale
manager: orenr
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.service: monitoring-and-diagnostics
ms.topic: quickstart
ms.date: 09/25/2017
ms.author: ancav
ms.custom: mvc
ms.openlocfilehash: 08d63d47a99bdf9480299a74634bc0e9a09e691e
ms.sourcegitcommit: 6699c77dcbd5f8a1a2f21fba3d0a0005ac9ed6b7
ms.translationtype: HT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/11/2017
---
# <a name="receive-a-notification-when-a-metric-value-meets-a-condition"></a>Otrzymywanie powiadomienia w przypadku spełnienia określonego warunku przez wartość metryki

Usługa Azure Monitor udostępnia metryki dla wielu zasobów platformy Azure. Te metryki informują o wydajności i kondycji zasobów. W wielu przypadkach wartości metryk mogą wskazywać problemy z zasobami. Możesz tworzyć alerty dotyczące metryk, aby monitorować zasoby pod kątem nieprawidłowego działania i otrzymywać powiadomienia w przypadku jego wystąpienia. Ten przewodnik Szybki start zawiera instrukcje tworzenia aplikacji logiki, tworzenia zadania oraz wizualizowania metryk tej aplikacji logiki. Następnie opisano proces tworzenia alertu i otrzymywania powiadomienia dotyczącego metryki zasobu aplikacji logiki.

Aby uzyskać więcej informacji na temat metryk i alertów dotyczących metryk, zobacz artykuły [Azure Monitor metrics overview](./monitoring-overview-metrics.md) (Omówienie metryk w usłudze Azure Monitor) i [Azure Monitor alerts overview](./monitoring-overview-alerts.md) (Omówienie alertów w usłudze Azure Monitor). 

Jeśli nie masz subskrypcji platformy Azure, przed rozpoczęciem utwórz [bezpłatne](https://azure.microsoft.com/free/) konto.

## <a name="sign-in-to-the-azure-portal"></a>Logowanie się do witryny Azure Portal

Zaloguj się w witrynie [Azure Portal](https://portal.azure.com/).

## <a name="create-a-logic-app"></a>Tworzenie aplikacji logiki

1. Kliknij przycisk **Nowy** znajdujący się w lewym górnym rogu witryny Azure Portal.

2. Wyszukaj i wybierz pozycję **Aplikacja logiki**. Utwórz nową grupę zasobów o nazwie **myResourceGroup**, używając lokalizacji domyślnej. Kliknij przycisk **Utwórz**.

3. Wprowadź dane aplikacji logiki i zaznacz opcję **Przypnij do pulpitu nawigacyjnego**. Na koniec kliknij pozycję **Utwórz**.

    ![Wprowadzanie podstawowych informacji o aplikacji logiki w portalu](./media/monitoring-quick-resource-metric-alert-portal/create-logic-app-portal.png)  


4. Aplikacja logiki powinna zostać przypięta do pulpitu nawigacyjnego. Kliknij aplikację logiki, aby do niej przejść.

5. Na panelu aplikacji logiki wybierz pozycję **Projektant aplikacji logiki**.

     ![Utworzono wyzwalacz cykliczny w Projektancie aplikacji logiki przy użyciu panelu portalu](./media/monitoring-quick-resource-metric-alert-portal/logic-app-designer.png)  

6. Skonfiguruj wartości zgodnie z poniższym diagramem.

    ![Konfigurowanie wyzwalacza aplikacji logiki przy użyciu panelu portalu](./media/monitoring-quick-resource-metric-alert-portal/create-logic-app-triggers.png). 

7. W projektancie wybierz wyzwalacz **Cykliczny**.

8. Ustaw interwał 20 oraz częstotliwość wyrażaną w sekundach, aby aplikacja logiki była wyzwalana co 20 sekund.

9. Kliknij przycisk **Nowy krok**, a następnie wybierz pozycję **Dodaj akcję**.

10. Wybierz opcję **HTTP**, a następnie **HTTP-HTTP**.

11. Ustaw wartość POST w polu **Metoda** i wybrany adres internetowy w polu **Identyfikator URI**.

12. Kliknij pozycję **Zapisz**.

## <a name="view-metrics-for-your-logic-app"></a>Wyświetlanie metryk aplikacji logiki

1. Kliknij opcję **Monitoruj** w okienku nawigacji po lewej stronie.

2. Wybierz kartę **Metryki** i wprowadź informacje dotyczące aplikacji logiki w polach **Subskrypcja**, **Grupa zasobów**, **Typ zasobu** oraz **Zasób**.

3. Z listy metryk wybierz pozycję **Przebiegi rozpoczęte**.

4. Zmień **Zakres czasu** na wykresie, aby wyświetlić dane z ostatniej godziny.

5. Powinien być teraz widoczny wykres przedstawiający łączną liczbę przebiegów uruchomionych przez aplikację logiki w ciągu ostatniej godziny.

    ![Tworzenie wykresu metryki dla zasobu aplikacji logiki](./media/monitoring-quick-resource-metric-alert-portal/logic-app-metric-chart.png)

## <a name="create-a-metric-alert-for-your-logic-app"></a>Tworzenie alertu dotyczącego metryki aplikacji logiki

1.  W prawym górnym rogu panelu metryk kliknij przycisk **Dodaj alert dotyczący metryki**.

2. Nadaj alertowi dotyczącemu metryki nazwę „myLogicAppAlert” i wprowadź krótki opis.

3. W polu **Warunek** ustaw wartość „Większe niż”, w polu **Próg** — „10”, a w polu **Okres** — „W ciągu 5 ostatnich minut”.

4. Na koniec w polu **Dodatkowe adresy e-mail administratora** wprowadź swój adres e-mail. Dzięki temu alertowi otrzymasz wiadomość e-mail, jeśli w aplikacji logiki w ciągu 5 minut wystąpi 10 nieudanych przebiegów.

    ![Konfigurowanie alertu aplikacji logiki przy użyciu panelu portalu](./media/monitoring-quick-resource-metric-alert-portal/logic-app-metrics-alert-portal.png)

## <a name="receive-metric-alert-notifications-for-your-logic-app"></a>Otrzymywanie powiadomień alertów dotyczących metryki aplikacji logiki
1. Po chwili powinna zostać dostarczona do Ciebie wiadomość e-mail od nadawcy „Microsoft Azure Alerts”, informująca o „aktywowaniu” alertu.

2. Wróć do aplikacji logiki i zmodyfikuj wyzwalacz cykliczny, zmieniając interwał na 1, a częstotliwość na godzinę.

3. Po chwili powinna zostać dostarczona do Ciebie wiadomość e-mail od nadawcy „Microsoft Azure Alerts”, informująca o „rozwiązaniu” alertu.

## <a name="clean-up-resources"></a>Oczyszczanie zasobów

Inne przewodniki Szybki start w tej kolekcji bazują na tym przewodniku. Jeśli planujesz kontynuować pracę z kolejnymi przewodnikami Szybki start lub samouczkami, nie usuwaj zasobów utworzonych w tym przewodniku Szybki start. Jeśli nie planujesz kontynuować pracy, wykonaj następujące czynności, aby usunąć wszystkie zasoby utworzone w witrynie Azure Portal w ramach tego przewodnika Szybki start.

1. W menu po lewej stronie witryny Azure Portal kliknij pozycję **Monitoruj**.

2. Wybierz kartę **Alerty**, znajdź alert utworzony podczas pracy z tym przewodnikiem Szybki start i kliknij go.

3. Na panelu alertu dotyczącego metryki kliknij pozycję **Usuń**.

4. W menu po lewej stronie witryny Azure Portal wyszukaj ciąg **Aplikacje logiki**, a następnie kliknij pozycję **Aplikacje logiki**.

5. W polu tekstowym na panelu kliknij aplikację logiki utworzoną podczas pracy z tym przewodnikiem Szybki start, a następnie kliknij polecenie **Usuń**.

## <a name="next-steps"></a>Następne kroki

Praca z tym przewodnikiem Szybki start pozwoliła Ci nauczyć się, jak utworzyć alert dotyczący metryki dla zasobów. Aby uzyskać więcej informacji na temat alertów dotyczących metryk, kliknij omówienie dotyczące alertów.

> [!div class="nextstepaction"]
> [Azure Monitor subscription action alerts](./monitor-quick-audit-notify-action-in-subscription.md ) (Alerty dotyczące działań związanych z subskrypcją w usłudze Azure Monitor)
