---
title: "nowe wyszukiwanie dziennika aaaLog Analytics — często zadawane pytania | Dokumentacja firmy Microsoft"
description: "Ten artykuł zawiera często zadawane pytania dotyczące uaktualniania hello analizy dzienników toohello nowego zapytania języka."
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
ms.openlocfilehash: b8664c8329fab0547f270793fa13e8cdd06ba637
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="log-analytics-new-log-search-faq-and-known-issues"></a>Często zadawane pytania dotyczące wyszukiwania i znane problemy dziennika nowe analizy dzienników

Ten artykuł zawiera często zadawane pytania i znane problemy dotyczące uaktualniania hello [toohello analizy dzienników nowego języka zapytań](log-analytics-log-search-upgrade.md).  W tym artykule całego powinien przeczytania przed wprowadzeniem tooupgrade decyzji hello obszaru roboczego.


## <a name="alerts"></a>Alerty

### <a name="question-i-have-a-lot-of-alert-rules-do-i-need-toocreate-them-again-in-hello-new-language-after-i-upgrade"></a>Pytanie: masz wiele reguł alertów. Należy toocreate je ponownie w nowym języku powitania po uaktualnieniu?  
Nie, regułami alertów są automatycznie przekonwertowane toohello nowy język wyszukiwania podczas uaktualniania.  


## <a name="computer-groups"></a>Grupy komputerów

### <a name="question-im-getting-errors-when-trying-toouse-computer-groups--has-their-syntax-changed"></a>Pytanie: błędów występujących podczas próby toouse grupy komputerów.  Zmieniono ich składni?
Tak, składnia hello przy użyciu komputera grupuje zmiany po uaktualnieniu obszaru roboczego.  Zobacz [grup komputerów w analizy dzienników dziennika wyszukiwania](log-analytics-computer-groups.md) szczegółowe informacje.

### <a name="known-issue-groups-imported-from-active-directory"></a>Znany problem: grup importowany z usługi Active Directory
Nie można obecnie utworzyć kwerendę, która używa grupy komputerów importowany z usługi Active Directory.  Jako rozwiązanie alternatywne dopóki ten problem zostanie rozwiązany, utworzyć grupę komputerów przy użyciu hello zaimportowane grupy usługi Active Directory, a następnie użyć tej nowej grupy w zapytaniu.

Przykładowe zapytania toocreate Nowa grupa komputerów, która zawiera grupę usługi Active Directory zaimportowanych wygląda następująco:

    ComputerGroup | where GroupSource == "ActiveDirectory" and Group == "AD Group Name" and TimeGenerated >= ago(24h) | distinct Computer


## <a name="dashboards"></a>Pulpity nawigacyjne

### <a name="question-can-i-still-use-dashboards-in-an-upgraded-workspace"></a>Pytanie: Czy nadal mogę korzystać pulpitów nawigacyjnych w uaktualnionym obszaru roboczego?
Można kontynuować toouse wszystkie Kafelki zbyt dodanych**Mój pulpit nawigacyjny** przed obszaru roboczego został uaktualniony, ale nie można edytować tych kafelków ani dodawać nowe.  Można kontynuować toocreate i edytowania widoków z [Widok projektanta](log-analytics-view-designer.md) , a także tworzyć pulpity nawigacyjne w hello portalu Azure.


## <a name="log-searches"></a>Dziennik wyszukiwania

### <a name="question-i-have-saved-searches-outside-of-my-upgraded-workspace-can-i-convert-them-toohello-new-search-language-automatically"></a>Pytanie: zostały już zapisane wyszukiwanie poza obszar Mój obszar roboczy uaktualniony. Czy mogę przekonwertować je toohello nowy język wyszukiwania automatycznie?
Można użyć narzędzia konwertera języka hello w hello dziennik wyszukiwania strony tooconvert każdej z nich.  Nie ma nie Konwertuj tooautomatically metody wielu Wyszukuje bez uaktualniania hello obszaru roboczego.

### <a name="question-why-are-my-query-results-not-sorted"></a>Pytanie: Dlaczego moja wyników zapytania nie są posortowane?
Wyniki są sortowane nie domyślnie hello nowy język kwerendy.  Użyj hello [operator sortowania](https://go.microsoft.com/fwlink/?linkid=856079) toosort wyników, przez co najmniej jednej właściwości.

### <a name="known-issue-search-results-in-a-list-may-include-properties-with-no-data"></a>Znany problem: wyniki wyszukiwania na liście mogą zawierać właściwości bez danych
Dziennik wyniki wyszukiwania na liście mogą wyświetlać właściwości nie zawiera żadnych danych.  Wcześniejsze tooupgrade te właściwości nie będą dołączone.  Ten problem zostanie rozwiązany, aby nie są wyświetlane właściwości puste.

### <a name="known-issue-selecting-a-value-in-a-chart-doesnt-display-detailed-results"></a>Znany problem: Wybieranie wartość na wykresie nie są wyświetlane szczegółowe wyniki
Wcześniejsze tooupgrade w przypadku wybrania wartość na wykresie go zwróci szczegółową listę rekordy pasujące hello wybrane wartości.  Po uaktualnieniu jest zwracana tylko hello podsumowane jednowierszowego.  Obecnie trwa bada ten problem.

## <a name="log-search-api"></a>Interfejs API wyszukiwania w dzienniku

### <a name="question-does-hello-log-search-api-get-updated-after-i-upgrade"></a>Pytanie: Hello interfejs API dziennika wyszukiwania zostanie zaktualizowana po uaktualnieniu?
Witaj [interfejs API dziennika wyszukiwania](log-analytics-log-search-api.md) nie została jeszcze uaktualniona toohello nowy język wyszukiwania.  Nadal język zapytań starszych hello toouse w tym interfejsie API nawet po uaktualnieniu obszaru roboczego.  Zaktualizowana dokumentacja będzie dostępne dla hello interfejs API dziennika wyszukiwania, gdy jest aktualizowany.


## <a name="portals"></a>Portale

### <a name="question-should-i-use-hello-new-advanced-analytics-portal-or-keep-using-hello-log-search-portal"></a>Pytanie: Należy I użyć nowego portalu analityka zaawansowane hello lub nadal korzystać z portalu wyszukiwania dziennika hello?
Widać porównanie hello dwa portale w [portali tworzenia i edytowania dziennika zapytań w programie Azure Log Analytics](log-analytics-log-search-portals.md).  Każdy ma wiele zalet, można wybrać hello najlepszy dla wymagań.  Jest typowe zapytania toowrite w portalu analityka zaawansowane hello i wklej je do innych miejsc, takich jak Widok projektanta.  Należy się zapoznać [wystawia tooconsider](log-analytics-log-search-portals.md#advanced-analytics-portal) po operacją.


## <a name="power-bi"></a>Power BI

### <a name="question-does-anything-change-with-powerbi-integration"></a>Pytanie: Czy niczego zmienia się z integracją usługi Power BI?
Tak.  Po uaktualnieniu obszaru roboczego hello procesu eksportowania analizy dzienników danych tooPower BI już będzie działać.  Istniejących harmonogramów, które zostały utworzone przed rozpoczęciem uaktualniania zostanie wyłączony.  Po uaktualnieniu, używa usługi Azure Log Analytics hello tej samej platformy jako usługi Application Insights i używać tego samego procesu tooexport analizy dzienników zapytań tooPower BI jako hello [hello tooexport procesu usługi Application Insights odpytuje tooPower BI](../application-insights/app-insights-export-power-bi.md#export-analytics-queries).

### <a name="known-issue-power-bi-request-size-limit"></a>Znany problem: limit rozmiaru żądania usługi Power BI
Obecnie istnieje limit rozmiaru zapytania analizy dzienników, które mogą być wyeksportowane tooPower BI 8 MB.  Wkrótce będzie można zwiększyć ten limit.


##<a name="powershell-cmdlets"></a>Polecenia cmdlet programu PowerShell

### <a name="question-does-hello-log-search-powershell-cmdlet-get-updated-after-i-upgrade"></a>Pytanie: Polecenia cmdlet programu PowerShell wyszukiwania dziennika hello zostanie zaktualizowana po uaktualnieniu?
Witaj [Get-AzureRmOperationalInsightsSearchResults](https://docs.microsoft.com/powershell/module/azurerm.operationalinsights/Get-AzureRmOperationalInsightsSearchResults) nie została jeszcze uaktualniona toohello nowy język wyszukiwania.  Język zapytań starszych hello toouse z tego polecenia cmdlet, należy kontynuować, nawet po uaktualnieniu obszaru roboczego.  Zaktualizowana dokumentacja będzie dostępne dla polecenia cmdlet hello podczas ich aktualizacji.


## <a name="resource-manager-templates"></a>Szablony usługi Resource Manager

### <a name="question-can-i-create-an-upgraded-workspace-with-a-resource-manager-template"></a>Pytanie: Można utworzyć obszar roboczy uaktualniony przy użyciu szablonu usługi Resource Manager?
Tak.  Należy użyć wersji interfejsu API 2017-03-15-preview i obejmują **funkcje** sekcji w szablonie, tak jak hello poniższy przykład.

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

### <a name="question-will-my-solutions-continue-toowork"></a>Pytanie: Moje rozwiązań będzie toowork?
Wszystkie rozwiązania będzie toowork w obszarze roboczym uaktualniony, mimo że ich wydajności poprawi przypadku przekonwertowanego toohello nowy język kwerendy.  Istnieją znane problemy z istniejącego rozwiązania, które zostały opisane w tej sekcji.

### <a name="known-issue-capacity-and-performance-solution"></a>Znany problem: pojemność i wydajność rozwiązania
Niektóre części hello na powitania [pojemność i wydajność](log-analytics-capacity.md) widok może być pusta.  Problem toothis poprawka będzie dostępna wkrótce.

### <a name="known-issue-device-health-solution"></a>Znany problem: rozwiązanie kondycja urządzenia
Witaj [rozwiązania kondycji urządzenia](https://docs.microsoft.com/windows/deployment/update/device-health-monitor) nie będzie zbierał dane w uaktualnionym obszaru roboczego.  Problem toothis poprawka będzie dostępna wkrótce.

### <a name="known-issue-application-insights-connector"></a>Znany problem: łącznika usługi Application Insights
Perspektywy [rozwiązanie Application Insights łącznik](log-analytics-app-insights-connector.md) nie są obecnie obsługiwane w obszarze roboczym uaktualniony.  Problem toothis poprawka jest obecnie w obszarze analizy.

## <a name="upgrade-process"></a>Proces uaktualniania

### <a name="question-i-have-several-workspaces-can-i-upgrade-all-workspaces-at-hello-same-time"></a>Pytanie: masz kilka obszarów roboczych. Można uaktualnić wszystkie obszary robocze na powitania jednocześnie?  
Nie.  Uaktualnienie dotyczy jednego obszaru roboczego tooa zawsze. Obecnie nie istnieje sposób uaktualnienia jednocześnie wiele obszarów roboczych. Należy pamiętać, również wpływ innych użytkowników obszaru roboczego hello uaktualniony.  

### <a name="question-will-existing-log-data-collected-in-my-workspace-be-modified-if-i-upgrade"></a>Pytanie: Zostaną istniejące dane dziennika zebrane w obszarze roboczym zmodyfikowane I uaktualnienia?  
Nie. Hello dziennika danych dostępne tooyour obszaru roboczego wyszukiwania nie ma wpływu na powitania uaktualnienia. Zapisane wyszukiwania, alertów i widoków zostanie przekonwertowana toohello nowy język wyszukiwania automatycznie.  

### <a name="question-what-happens-if-i-dont-upgrade-my-workspace"></a>Pytanie: Co się stanie, jeśli nie można uaktualnić obszar Mój obszar roboczy?  
wyszukiwania dziennika starsze Hello zostaną wycofane w hello przesyłanych miesiące. Obszary robocze, które nie zostały uaktualnione do tego czasu zostanie automatycznie uaktualniona.

### <a name="question-i-didnt-choose-tooupgrade-but-my-workspace-has-been-upgraded-anyway-what-happened"></a>Pytanie: nie wybrać tooupgrade, ale obszar Mój obszar roboczy został uaktualniony mimo wszystko! Co się stało?  
Inny administrator tego obszaru roboczego można uaktualniono hello obszaru roboczego. Należy pamiętać, że wszystkie obszary robocze zostaną automatycznie uaktualnione gdy nowy język hello osiągnie ogólnej dostępności.  

### <a name="question-i-have-upgraded-by-mistake-and-now-need-toocancel-it-and-restore-everything-back-what-should-i-do"></a>Pytanie: uaktualniono przez pomyłkę i teraz należy toocancel go oraz ich przywrócenie wszystkich kopii. Co należy zrobić?  
Nie ma problemu.  Utworzymy migawki obszaru roboczego przed uaktualnieniem, można go przywrócić. Należy pamiętać, która wyszukuje alertów ani widoków, które zapisane po hello uaktualnienia zostaną utracone jeśli.  toorestore środowisku roboczym, wykonaj procedurę hello na [czy można przejść wstecz po uaktualnieniu?](log-analytics-log-search-upgrade.md#can-i-go-back-after-i-upgrade)


## <a name="views"></a>Widoki

### <a name="question-how-do-i-create-a-new-view-with-view-designer"></a>Pytanie: Jak utworzyć nowy widok z projektanta widoków?
Wcześniejsze tooupgrade, można utworzyć nowy widok z projektanta widoków z kafelka na głównym pulpicie nawigacyjnym hello.  Po uaktualnieniu obszaru roboczego tego kafelka zostaną usunięte.  Można utworzyć nowy widok z projektanta widoków w portalu OMS hello, klikając przycisk w menu po lewej stronie powitania + hello zielony.

### <a name="known-issue-see-all-option-for-line-charts-in-views-doesnt-result-in-a-line-chart"></a>Znany problem: Zobacz wszystkich opcji w przypadku wykresów liniowych w widokach nie powoduje wykres liniowy
Po kliknięciu hello *zobaczyć wszystkie* opcji hello dolnej części wykresu wiersza w widoku, jest wyświetlana z tabelą.  Wcześniejsze tooupgrade czy prezentowane z wykres liniowy.  Ten problem jest analizowana potencjalnych modyfikacji.


## <a name="next-steps"></a>Następne kroki

- Dowiedz się więcej o [uaktualniania toohello Twojego obszaru roboczego analizy dzienników nowego języka zapytań](log-analytics-log-search-upgrade.md).
