---
title: "aaaGet rozpoczęcia pracy z monitorem Azure | Dokumentacja firmy Microsoft"
description: "Rozpocząć korzystanie z monitora Azure toogain wgląd w działania hello zasobów i podejmij działania oparte na danych."
author: johnkemnetz
manager: orenr
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: ce2930aa-fc41-4b81-b0cb-e7ea922467e1
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/19/2016
ms.author: johnkem
ms.openlocfilehash: 49e7105621a9e60c9fa14c4911c4fe45e0d197a6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-monitor"></a>Rozpoczynanie pracy z usługą Azure Monitor
Azure Monitor to usługa platformy hello, która zapewnia jednego źródła do monitorowania zasobów platformy Azure. Z monitorem Azure można zwizualizować, zapytania, trasy, archiwizacji i podejmij akcję na powitania metryki i dzienników pochodzących z zasobami na platformie Azure. Możesz pracować z tych danych za pomocą bloku portalu Monitor hello, [poleceń cmdlet programu PowerShell Monitor](insights-powershell-samples.md), [interfejsu wiersza polecenia i Platform](insights-cli-samples.md), lub [interfejsów API REST Monitor Azure](https://msdn.microsoft.com/library/dn931943.aspx). W tym artykule firma Microsoft przeprowadzenie kilka kluczowych składników hello Azure monitora, za pomocą portalu hello do pokazania.

1. W portalu hello Przejdź zbyt**więcej usług** i Znajdź hello **Monitor** opcji. Kliknij przycisk tooadd ikonę gwiazdki hello listy ulubionych tooyour tej opcji, aby zawsze jest łatwo dostępna z hello na pasku nawigacyjnym po lewej stronie.
   
    ![Monitorowanie na liście usług hello](./media/monitoring-get-started/monitor-more-services.png)
2. Kliknij hello **Monitor** tooopen opcji zapasowej hello **Monitor** bloku. Ten blok gromadzi wszystkie ustawienia monitorowania i dane użytkownika w jednym skonsolidowanym widoku. Pierwszym otwarciu toohello **dziennik aktywności** sekcji.
   
    ![Nawigacja w bloku Monitor](./media/monitoring-get-started/monitor-blade-nav.png)
   
    Azure Monitor ma trzy podstawowe kategorie danych monitorowania: hello **dziennik aktywności**, **metryki**, i **dzienników diagnostycznych**.
3. Kliknij przycisk **dziennik aktywności** tooensure, który hello sekcji dziennika aktywności jest wyświetlany.
   
    ![Blok dziennika aktywności](./media/monitoring-get-started/monitor-act-log-blade.png)
   
    Witaj [ **dziennik aktywności** ](monitoring-overview-activity-logs.md) opisano wszystkie operacje wykonywane na zasobów w ramach subskrypcji. Przy użyciu hello dziennik aktywności, można określić hello ", co, kto i kiedy" dla dowolnego tworzenia, aktualizowania lub usuwania operacje na zasobach w ramach subskrypcji. Na przykład hello dziennik aktywności informuje, kiedy aplikacji sieci web została zatrzymana i który zatrzymania. Działania zdarzenia dziennika są przechowywane w hello platformy i tooquery dostępne przez 90 dni.
   
    Możesz utworzyć i zapisać zapytania dotyczące typowych filtrów, a następnie numeru pin hello najważniejszych zapytań tooa pulpitu nawigacyjnego portalu, aby zawsze będzie wiadomo, czy wystąpiły zdarzenia, które spełniają kryteria.
4. Filtrowanie hello widoku tooa wybranej grupy zasobów w ostatnim tygodniu hello, a następnie kliknij przycisk hello **zapisać** przycisku.
   
    ![Zapisywanie zapytania dotyczącego dziennika aktywności](./media/monitoring-get-started/monitor-act-log-save.png)
5. Teraz, kliknij przycisk hello **numeru Pin** przycisku.
   
    ![Kliknięcie opcji Przypnij dla dziennika aktywności](./media/monitoring-get-started/monitor-act-log-pin.png)
   
    Większość hello widoków, w tym przewodniku można przypiętych tooa pulpitu nawigacyjnego. Pozwala to utworzyć pojedyncze źródło informacji dotyczących danych operacyjnych Twoich usług. 
6. Zwraca tooyour pulpitu nawigacyjnego. Możesz teraz przeglądać czy kwerendy hello (i liczbę wyników) są wyświetlane na pulpicie nawigacyjnym. Jest to przydatne, jeśli chcesz znaleźć tooquickly wszystkie akcje wysokiej jakości, które wystąpiły ostatnio w ramach subskrypcji, np. przypisanie nowej roli lub usunięcie maszyny wirtualnej.
   
    ![Toodashboard przypięty dziennika aktywności](./media/monitoring-get-started/monitor-act-log-db.png)
7. Zwraca toohello **Monitor** Kafelek, a następnie kliknij przycisk hello **metryki** sekcji. Należy najpierw tooselect zasobu filtrowania, a następnie wybierając polecenie za pomocą hello listy rozwijanej Opcje u góry bloku hello hello.
   
    ![Filtrowanie zasobu pod kątem metryk](./media/monitoring-get-started/monitor-met-filter.png)
   
    Wszystkie zasoby platformy Azure tworzą [**metryki**](monitoring-overview-metrics.md). Ten widok gromadzi wszystkie metryki na jednym ekranie, dzięki czemu można łatwo prześledzić działanie zasobów.
8. Po wybraniu zasobu na powitania po lewej stronie bloku hello są wyświetlane wszystkie dostępne metryki. Można jednocześnie wykresu wiele metryk, wybierając metryki i modyfikować hello wykres typu i zakres czasu. Możesz również wyświetlić wszystkie alerty metryki ustawione dla danego zasobu.
   
    ![Blok metryki](./media/monitoring-get-started/monitor-metric-blade.png)
   
   > [!NOTE]
   > Niektóre metryki są dostępne tylko po włączeniu dla zasobu usługi [Application Insights](../application-insights/app-insights-overview.md) i/lub Diagnostyki Azure dla systemu Windows bądź Linux.
   > 
   > 
9. Jeśli są zadowalające z wykresu, możesz użyć hello **numeru Pin** toopin przycisk go tooyour pulpitu nawigacyjnego.
10. Zwraca toohello **Monitor** bloku i kliknij przycisk **dzienniki diagnostyczne**.
    
    ![Blok dzienników diagnostycznych](./media/monitoring-get-started/monitor-diaglogs-blade.png)
    
    [**Dzienniki diagnostyczne** ](monitoring-overview-of-diagnostic-logs.md) są dzienniki wysyłanego *przez* z zasobem, który zawierają dane dotyczące działania hello tego zasobu. Na przykład typami dzienników diagnostycznych są liczniki reguł grup zabezpieczeń sieci oraz dzienniki przepływu pracy aplikacji logiki. Te dzienniki mogą być przechowywane na koncie magazynu, przesyłanej strumieniowo tooan Centrum zdarzeń i/lub wysłany[analizy dzienników](../log-analytics/log-analytics-overview.md). Usługa Log Analytics jest produktem firmy Microsoft służącym do analizy operacyjnej, który umożliwia zaawansowane wyszukiwanie oraz generowanie alertów.
    
    W portalu hello można przeglądać i Filtruj listę wszystkich zasobów w Twojej subskrypcji tooidentify, gdy mają włączone dzienników diagnostycznych.
11. Kliknij zasób w bloku dzienników diagnostycznych hello. Jeśli dzienniki diagnostyczne są przechowywane na koncie magazynu, zostanie wyświetlona lista tworzonych co godzinę dzienników, które można bezpośrednio pobrać.
    
    ![Dzienniki diagnostyczne dla jednego zasobu](./media/monitoring-get-started/monitor-diaglogs-detail.png)
    
    Możesz również kliknąć **ustawień diagnostycznych**, która umożliwia tooset się lub zmodyfikować ustawienia dla konta magazynu tooa archiwizacji, przesyłanie strumieniowe koncentratory tooEvent lub wysyłanie tooa obszaru roboczego analizy dzienników.
    
    ![Włączanie dzienników diagnostycznych](./media/monitoring-get-started/monitor-diaglogs-enable.png)
    
    Jeśli zdefiniowano tooLog dzienników diagnostycznych Analytics, możesz wyszukiwać ich w hello **wyszukiwania dziennika** sekcji hello portalu.
12. Przejdź toohello **alerty** sekcji hello Monitor bloku.
    
    ![publiczny blok alertów](./media/monitoring-get-started/monitor-alerts-nopp.png)
    
    W tym miejscu można zarządzać wszystkimi [**alertami**](monitoring-overview-alerts.md) dotyczącymi zasobów platformy Azure. Dotyczy to również alerty dotyczące metryk, zdarzenia dziennika aktywności testów sieci web usługi Application Insights (lokalizacja) i proaktywna Diagnostyka usługi Application Insights. Alerty można wyzwolić toobe wiadomości e-mail wysyłane lub adres URL elementu webhook tooa HTTP POST.
13. Kliknij przycisk **Dodaj alert metryki** toocreate alertu.
    
    ![dodawanie alertu dotyczącego metryki](./media/monitoring-get-started/monitor-alerts-add.png)
    
    Mogą być następnie numeru pin alertu tooyour tooeasily pulpitu nawigacyjnego zobacz jego stanu w dowolnym momencie.
14. zbyt Hello sekcji Monitor łączy zawiera również[usługi Application Insights](../application-insights/app-insights-overview.md) aplikacji i [analizy dzienników](../log-analytics/log-analytics-overview.md) rozwiązania do zarządzania. Te produkty firmy Microsoft są silnie zintegrowane z usługą Azure Monitor.
15. Jeśli nie korzystasz z usług Application Insights ani Log Analytics, możliwe jest, że usługa Azure Monitor współpracuje z aktualnie używanymi przez Ciebie produktami do monitorowania, rejestrowania i tworzenia alertów. Zobacz nasze [strony partnerów](monitoring-partners.md) pełną listę i instrukcje toointegrate.

Poniższe kroki i przypinanie wszystkich pulpitu nawigacyjnego tooa odpowiednich fragmentów, można tworzyć kompleksowe widoki aplikacji i infrastruktury, takich jak ta:

![Pulpit nawigacyjny usługi Azure Monitor](./media/monitoring-get-started/monitor-final-dash.png)

## <a name="next-steps"></a>Następne kroki
* Witaj odczytu [Monitor Omówienie usługi Azure](monitoring-overview.md)

