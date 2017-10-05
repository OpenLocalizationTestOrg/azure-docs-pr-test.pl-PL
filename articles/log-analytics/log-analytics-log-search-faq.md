---
title: "Nowe wyszukiwanie dziennika analizy dziennika często zadawane pytania | Dokumentacja firmy Microsoft"
description: "Ten artykuł zawiera często zadawane pytania dotyczące uaktualniania analizy dzienników dla nowego języka zapytań."
services: log-analytics
documentationcenter: 
author: bwren
manager: carmonm
editor: 
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/27/2017
ms.author: bwren
ms.openlocfilehash: d7bd0d780c265cc15ad09a73ede8c5a886005e37
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
# <a name="log-analytics-new-log-search-faq-and-known-issues"></a>Często zadawane pytania dotyczące wyszukiwania i znane problemy dziennika nowe analizy dzienników

Ten artykuł zawiera często zadawane pytania i znane problemy dotyczące uaktualniania [analizy dzienników dla nowego języka zapytań](log-analytics-log-search-upgrade.md).  W tym artykule całego powinien przeczytania przed podjęciem decyzji o uaktualnienie obszaru roboczego.


## <a name="alerts"></a>Alerty

### <a name="question-i-have-a-lot-of-alert-rules-do-i-need-to-create-them-again-in-the-new-language-after-i-upgrade"></a>Pytanie: masz wiele reguł alertów. Należy utworzyć je ponownie w nowym języku po uaktualnieniu?  
Nie, regułami alertów są konwertowane na nowy język wyszukiwania podczas uaktualniania.  


## <a name="computer-groups"></a>Grupy komputerów

### <a name="question-im-getting-errors-when-trying-to-use-computer-groups--has-their-syntax-changed"></a>Pytanie: błędów występujących podczas próby użycia grupy komputerów.  Zmieniono ich składni?
Tak, przy użyciu komputera składnia grupuje zmiany po uaktualnieniu obszaru roboczego.  Zobacz [grup komputerów w analizy dzienników dziennika wyszukiwania](log-analytics-computer-groups.md) szczegółowe informacje.

### <a name="known-issue-groups-imported-from-active-directory"></a>Znany problem: grup importowany z usługi Active Directory
Nie można obecnie utworzyć kwerendę, która używa grupy komputerów importowany z usługi Active Directory.  Jako rozwiązanie alternatywne dopóki ten problem zostanie rozwiązany, utworzyć grupę komputerów za pomocą zaimportowanych grupy usługi Active Directory, a następnie użyć tej nowej grupy w zapytaniu.

Przykładowe zapytanie, aby utworzyć nową grupę komputera, która zawiera grupę usługi Active Directory zaimportowanych wygląda następująco:

    ComputerGroup | where GroupSource == "ActiveDirectory" and Group == "AD Group Name" and TimeGenerated >= ago(24h) | distinct Computer


## <a name="dashboards"></a>Pulpity nawigacyjne

### <a name="question-can-i-still-use-dashboards-in-an-upgraded-workspace"></a>Pytanie: Czy nadal mogę korzystać pulpitów nawigacyjnych w uaktualnionym obszaru roboczego?
Można nadal korzystać z żadnych kafelków, które zostały dodane do **Mój pulpit nawigacyjny** przed obszaru roboczego został uaktualniony, ale nie można edytować tych kafelków ani dodawać nowe.  Możesz nadal tworzyć i edytować widoków z [Widok projektanta](log-analytics-view-designer.md) , a także tworzenia pulpitów nawigacyjnych w portalu Azure.


## <a name="log-searches"></a>Dziennik wyszukiwania

### <a name="question-i-have-saved-searches-outside-of-my-upgraded-workspace-can-i-convert-them-to-the-new-search-language-automatically"></a>Pytanie: zostały już zapisane wyszukiwanie poza obszar Mój obszar roboczy uaktualniony. Można przekonwertować je na nowy język wyszukiwania automatycznie?
Narzędzia konwertera języka na stronie dziennik wyszukiwania umożliwia konwertowanie każdej z nich.  Nie istnieje metoda aby dokonać automatycznej konwersji wielu wyszukiwania bez uaktualniania obszaru roboczego.

### <a name="question-why-are-my-query-results-not-sorted"></a>Pytanie: Dlaczego moja wyników zapytania nie są posortowane?
Wyniki są sortowane nie domyślnie w nowym języku zapytania.  Użyj [operator sortowania](https://go.microsoft.com/fwlink/?linkid=856079) Aby posortować wyników według co najmniej jednej właściwości.

### <a name="known-issue-search-results-in-a-list-may-include-properties-with-no-data"></a>Znany problem: wyniki wyszukiwania na liście mogą zawierać właściwości bez danych
Dziennik wyniki wyszukiwania na liście mogą wyświetlać właściwości nie zawiera żadnych danych.  Przed uaktualnieniem te właściwości nie będą dołączone.  Ten problem zostanie rozwiązany, aby nie są wyświetlane właściwości puste.

### <a name="known-issue-selecting-a-value-in-a-chart-doesnt-display-detailed-results"></a>Znany problem: Wybieranie wartość na wykresie nie są wyświetlane szczegółowe wyniki
Przed uaktualnieniem gdy wybrana wartość na wykresie go zwróci szczegółową listę rekordy pasujące do wybranej wartości.  Po uaktualnieniu jest zwracana tylko pojedynczy wiersz podsumowania.  Obecnie trwa bada ten problem.

## <a name="log-search-api"></a>Interfejs API wyszukiwania w dzienniku

### <a name="question-does-the-log-search-api-get-updated-after-i-upgrade"></a>Pytanie: Interfejs API wyszukiwania dziennika zostanie zaktualizowana po uaktualnieniu?
[Interfejs API dziennika wyszukiwania](log-analytics-log-search-api.md) nie została jeszcze uaktualniona w nowym języku wyszukiwania.  Nadal używać języka kwerend starszej wersji w tym interfejsie API nawet po uaktualnieniu obszaru roboczego.  Zaktualizowana dokumentacja staną się dostępne interfejsu API wyszukiwania dziennika podczas jej aktualizowania.


## <a name="portals"></a>Portale

### <a name="question-should-i-use-the-new-advanced-analytics-portal-or-keep-using-the-log-search-portal"></a>Pytanie: Należy I użyć nowego portalu analityka zaawansowane lub nadal korzystać z portalu wyszukiwania dziennika?
Widać porównanie dwa portale w [portali tworzenia i edytowania dziennika zapytań w programie Azure Log Analytics](log-analytics-log-search-portals.md).  Każdy ma wiele zalet, można wybrać najlepszy do wymagań.  Jest często stosowanym rozwiązaniem pisać zapytania w portalu analityka zaawansowane i wklej je do innych miejsc, takich jak Widok projektanta.  Należy się zapoznać [zagadnień do uwzględnienia](log-analytics-log-search-portals.md#advanced-analytics-portal) po operacją.


## <a name="power-bi"></a>Power BI

### <a name="question-does-anything-change-with-powerbi-integration"></a>Pytanie: Czy niczego zmienia się z integracją usługi Power BI?
Tak.  Po uaktualnieniu obszaru roboczego procesu eksportowania analizy dzienników danych do usługi Power BI nie będzie działać.  Istniejących harmonogramów, które zostały utworzone przed rozpoczęciem uaktualniania zostanie wyłączony.  Po uaktualnieniu, analiza dzienników Azure używa tej samej platformy jako usługi Application Insights i używać tego samego procesu eksportowania analizy dzienników zapytań do usługi Power BI jako [procesu eksportowania zapytań usługi Application Insights do usługi Power BI](../application-insights/app-insights-export-power-bi.md#export-analytics-queries).

### <a name="known-issue-power-bi-request-size-limit"></a>Znany problem: limit rozmiaru żądania usługi Power BI
Obecnie jest ograniczenie do 8 MB dla zapytania analizy dzienników, które mogą być eksportowane do usługi Power BI.  Wkrótce będzie można zwiększyć ten limit.


##<a name="powershell-cmdlets"></a>Polecenia cmdlet programu PowerShell

### <a name="question-does-the-log-search-powershell-cmdlet-get-updated-after-i-upgrade"></a>Pytanie: Polecenie cmdlet programu PowerShell wyszukiwania dziennika zostanie zaktualizowana po uaktualnieniu?
[Get-AzureRmOperationalInsightsSearchResults](https://docs.microsoft.com/powershell/module/azurerm.operationalinsights/Get-AzureRmOperationalInsightsSearchResults) nie została jeszcze uaktualniona w nowym języku wyszukiwania.  Nadal używać języka kwerend starszej wersji tego polecenia cmdlet, nawet po uaktualnieniu obszaru roboczego.  Zaktualizowana dokumentacja będzie dostępne polecenia cmdlet, gdy jest on aktualizowany.


## <a name="resource-manager-templates"></a>Szablony usługi Resource Manager

### <a name="question-can-i-create-an-upgraded-workspace-with-a-resource-manager-template"></a>Pytanie: Można utworzyć obszar roboczy uaktualniony przy użyciu szablonu usługi Resource Manager?
Tak.  Należy użyć wersji interfejsu API 2017-03-15-preview i obejmują **funkcje** sekcji w szablonie, jak w poniższym przykładzie.

    "resources": [
        {
            "type": "Microsoft.OperationalInsights/workspaces",
            "apiVersion": "2017-03-15-preview",
            "name": "[parameters('workspaceName')]",
            "location": "[parameters('workspaceRegion')]",
            "properties": {
                "sku": {
                    "name": "Free"
                },
                "features": {
                    "legacy": 0,
                    "searchVersion": 1
                }
            }
        }
    ],



## <a name="solutions"></a>Rozwiązania

### <a name="question-will-my-solutions-continue-to-work"></a>Pytanie: Moje rozwiązań będzie działać?
Wszystkie rozwiązania będą nadal działać w obszarze roboczym uaktualniony, mimo że ich wydajności zwiększy wtedy są konwertowane na nowy język kwerendy.  Istnieją znane problemy z istniejącego rozwiązania, które zostały opisane w tej sekcji.

### <a name="known-issue-capacity-and-performance-solution"></a>Znany problem: pojemność i wydajność rozwiązania
Niektóre elementy w [pojemność i wydajność](log-analytics-capacity.md) widok może być pusta.  Rozwiązano ten problem będzie dostępna wkrótce.

### <a name="known-issue-device-health-solution"></a>Znany problem: rozwiązanie kondycja urządzenia
[Rozwiązania kondycji urządzenia](https://docs.microsoft.com/windows/deployment/update/device-health-monitor) nie będzie zbierał dane w uaktualnionym obszaru roboczego.  Rozwiązano ten problem będzie dostępna wkrótce.

### <a name="known-issue-application-insights-connector"></a>Znany problem: łącznika usługi Application Insights
Perspektywy [rozwiązanie Application Insights łącznik](log-analytics-app-insights-connector.md) nie są obecnie obsługiwane w obszarze roboczym uaktualniony.  Rozwiązania tego problemu jest obecnie w obszarze analizy.

## <a name="upgrade-process"></a>Proces uaktualniania

### <a name="question-i-have-several-workspaces-can-i-upgrade-all-workspaces-at-the-same-time"></a>Pytanie: masz kilka obszarów roboczych. W tym samym czasie można uaktualnić wszystkie obszary robocze?  
Nie.  Uaktualnienie dotyczy jednego obszaru roboczego zawsze. Obecnie nie istnieje sposób uaktualnienia jednocześnie wiele obszarów roboczych. Należy pamiętać, również wpływ innym użytkownikom uaktualniony obszaru roboczego.  

### <a name="question-will-existing-log-data-collected-in-my-workspace-be-modified-if-i-upgrade"></a>Pytanie: Zostaną istniejące dane dziennika zebrane w obszarze roboczym zmodyfikowane I uaktualnienia?  
Nie. Dostępne do wyszukiwania obszaru roboczego danych dziennika nie ma wpływu na uaktualnienie. Zapisane wyszukiwania, alertów i widoków zostaną przekonwertowane na nowy język wyszukiwania automatycznie.  

### <a name="question-what-happens-if-i-dont-upgrade-my-workspace"></a>Pytanie: Co się stanie, jeśli nie można uaktualnić obszar Mój obszar roboczy?  
Wyszukiwanie starszych dziennika zostaną wycofane w najbliższych miesiącach. Obszary robocze, które nie zostały uaktualnione do tego czasu zostanie automatycznie uaktualniona.

### <a name="question-i-didnt-choose-to-upgrade-but-my-workspace-has-been-upgraded-anyway-what-happened"></a>Pytanie: czy nie zdecydować się na uaktualnienie, ale obszar Mój obszar roboczy został uaktualniony mimo wszystko! Co się stało?  
Inny administrator tego obszaru roboczego można uaktualniono obszaru roboczego. Należy pamiętać, że wszystkie obszary robocze zostaną automatycznie uaktualnione po udostępnieniu wersji ogólnodostępnej nowego języka.  

### <a name="question-i-have-upgraded-by-mistake-and-now-need-to-cancel-it-and-restore-everything-back-what-should-i-do"></a>Pytanie: uaktualniono przez pomyłkę i teraz musisz anulować go i przywrócić wszystkie ponownie. Co należy zrobić?  
Nie ma problemu.  Utworzymy migawki obszaru roboczego przed uaktualnieniem, można go przywrócić. Należy pamiętać, która wyszukuje alertów ani widoków, które jest zapisywane po uaktualnieniu zostaną utracone jeśli.  Aby przywrócić środowisku roboczym, wykonaj tę procedurę na [czy można przejść wstecz po uaktualnieniu?](log-analytics-log-search-upgrade.md#can-i-go-back-after-i-upgrade)


## <a name="views"></a>Widoki

### <a name="question-how-do-i-create-a-new-view-with-view-designer"></a>Pytanie: Jak utworzyć nowy widok z projektanta widoków?
Przed uaktualnieniem można utworzyć nowy widok z projektanta widoków z kafelka na głównym pulpicie nawigacyjnym.  Po uaktualnieniu obszaru roboczego tego kafelka zostaną usunięte.  Można utworzyć nowy widok z projektanta widoków w portalu OMS, klikając przycisk w lewym menu + zielony.

### <a name="known-issue-see-all-option-for-line-charts-in-views-doesnt-result-in-a-line-chart"></a>Znany problem: Zobacz wszystkich opcji w przypadku wykresów liniowych w widokach nie powoduje wykres liniowy
Po kliknięciu *zobaczyć wszystkie* opcji w dolnej części wykresu wiersza w widoku jest wyświetlana z tabelą.  Przed uaktualnieniem będą przedstawiane z wykres liniowy.  Ten problem jest analizowana potencjalnych modyfikacji.


## <a name="next-steps"></a>Następne kroki

- Dowiedz się więcej o [uaktualnianie obszaru roboczego do nowego języka zapytań usługi Analiza dzienników](log-analytics-log-search-upgrade.md).
