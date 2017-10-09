---
title: "aaaWhat jest analiza dzienników w Operations Management Suite (OMS)? | Microsoft Docs"
description: "Log Analytics to usługa należąca do pakietu Operations Management Suite (OMS) ułatwiająca zbieranie i analizę danych operacyjnych generowanych przez zasoby w środowisku chmurowym i lokalnym.  Ten artykuł zawiera krótki przegląd różnych składników hello analizy dzienników i linki toodetailed zawartości."
services: log-analytics
documentationcenter: 
author: bwren
manager: jwhit
editor: tysonn
ms.assetid: bd90b460-bacf-4345-ae31-26e155beac0e
ms.service: log-analytics
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 06/12/2017
ms.author: bwren
ms.openlocfilehash: b35da77e3782f7c1fe54cc34142f8cd9f2eb57d7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="what-is-log-analytics"></a>Co to jest usługa Log Analytics?
Log Analytics jest usługą [Operations Management Suite \(OMS\) ](../operations-management-suite/operations-management-suite-overview.md) Twojego toomaintain środowisk chmury i lokalnych który monitoruje ich dostępności i wydajności.  Zbiera dane generowane przez zasobów w swoich środowiskach w chmurze i lokalnie i z innych monitorowania analizy tooprovide narzędzi w wielu źródeł.  Ten artykuł zawiera krótkie omówienie wartość hello czy analizy dzienników omówiono, jak działa, i toomore łącza szczegółowych zawartości, więc można wyświetlić w dalszych.

## <a name="is-log-analytics-for-you"></a>Czy usługa Log Analytics jest przeznaczona dla Ciebie?
Jeśli obecnie środowisko platformy Azure nie jest monitorowane, warto rozpocząć od pracy z usługą [Azure Monitor](../monitoring-and-diagnostics/monitoring-overview.md), która zbiera i analizuje dane monitorowania zasobów platformy Azure.  Analizy dzienników można [zbierania danych z monitora Azure](log-analytics-azure-storage.md) toocorrelate go z innymi danymi i udostępnia dodatkowe analizy.

Jeśli masz istniejące monitorowanie za pomocą usług, takich jak Azure Monitor lub System Center Operations Manager ma toomonitor w lokalnym środowisku, Log Analytics można dodać wartość.  Może ona zbierać dane bezpośrednio od agentów oraz innych narzędzi w obrębie pojedynczego repozytorium.  Narzędzia analityczne w usłudze Log Analytics, takie jak operacje wyszukiwania w dziennikach, widoki i rozwiązania, działają na wszystkich zebranych danych i oferują scentralizowaną analizę całego środowiska.


## <a name="using-log-analytics"></a>Korzystanie z usługi Log Analytics
Analiza dzienników dostępne za pośrednictwem portalu OMS hello lub hello portalu Azure, która uruchomić w dowolnej przeglądarce i podaj możesz z ustawieniami tooconfiguration dostępu i wielu tooanalyze narzędzia i korzystania z zebranych danych.  Z portalu hello można wykorzystać [dziennika wyszukiwania](log-analytics-log-searches.md) w przypadku, gdy tworzenia zapytań tooanalyze zebranych danych, [pulpity nawigacyjne](log-analytics-dashboards.md) , który można dostosować za pomocą graficznego widoków wyszukiwań najbardziej przydatna, i [rozwiązań](log-analytics-add-solutions.md) które zapewniają dodatkowe narzędzia funkcjonalność i analizy.

Obraz powitania poniżej pochodzi z portalu OMS hello które pulpit nawigacyjny hello pokazuje, który wyświetla informacje podsumowania hello [rozwiązań](#add-functionality-with-management-solutions) są instalowane w obszarze roboczym hello.  Możesz kliknąć żadnych dalszych kafelka toodrill na powitania dane dla tego rozwiązania.

![Portal pakietu OMS](media/log-analytics-overview/portal.png)

Analiza dzienników zawiera pobrać tooquickly języka zapytań i Konsolidowanie danych w repozytorium hello.  Można utworzyć i zapisać [dziennik wyszukiwania](log-analytics-log-searches.md) toodirectly analizowanie danych w portalu hello lub dziennik wyszukiwania uruchomiono automatycznie toocreate alert Jeśli hello wynikach zapytania hello warunek ważne.

![Wyszukiwanie w dzienniku](media/log-analytics-overview/log-search.png)

tooget szybki przegląd graficznego hello kondycji ogólnej środowiska, możesz dodać wizualizacji dla dziennika zapisanych wyszukiwań tooyour [pulpitu nawigacyjnego](log-analytics-dashboards.md).   

![Pulpit nawigacyjny](media/log-analytics-overview/dashboard.png)

W danych tooanalyze poza analizy dzienników, można wyeksportować danych hello z repozytorium OMS hello do narzędzi takich jak [usługi Power BI](log-analytics-powerbi.md) lub programu Excel.  Można również wykorzystać hello [interfejs API dziennika wyszukiwania](log-analytics-log-search-api.md) toobuild niestandardowych rozwiązań korzystających z danych analizy dzienników lub toointegrate z innymi systemami.

## <a name="add-functionality-with-management-solutions"></a>Dodawanie funkcjonalności dzięki rozwiązaniom do zarządzania
[Rozwiązania do zarządzania](log-analytics-add-solutions.md) Dodaj funkcje tooOMS, zapewniając dodatkowe dane i tooLog narzędzia analizy Analytics.  Mogą również określić nowe toobe typy rekordów zbierane umożliwia analizowanie wyszukiwania dziennika lub przy użyciu interfejsu użytkownika dodatkowe podane przez rozwiązanie hello na pulpicie nawigacyjnym hello.  Witaj przykład obraz poniżej przedstawia hello [rozwiązaniu do śledzenia zmian](log-analytics-change-tracking.md)

![Rozwiązanie do śledzenia zmian](media/log-analytics-overview/change-tracking.png)

Dostępne są już rozwiązania związane z różnorodnymi funkcjami i cały czas dodajemy kolejne rozwiązania.  Możesz łatwo przeglądać dostępne rozwiązania i [je dodać obszar roboczy OMS tooyour](log-analytics-add-solutions.md) z galerii rozwiązań hello lub portalu Azure Marketplace.  Wiele rozwiązań zostanie automatycznie wdrożonych i od razu zacznie działać, ale w przypadku innych może być konieczne wykonanie umiarkowanie złożonych czynności konfiguracyjnych.

![Galeria rozwiązań](media/log-analytics-overview/solution-gallery.png)

## <a name="log-analytics-components"></a>Składniki usługi Log Analytics
Na powitania center analizy dzienników jest hello OMS repozytorium, która jest hostowana w hello chmury Azure.  Dane są zbierane w repozytorium hello z połączonych źródeł Konfigurowanie źródeł danych i dodawania subskrypcji tooyour rozwiązania.  Źródła danych i rozwiązania spowoduje utworzenie różnych typów rekordów własnych zbiór właściwości, które mogą być analizowane razem w repozytorium toohello zapytania.  Dzięki temu hello toouse tego samego narzędzia i metody toowork z różnych rodzajów danych zbieranych przez różnych źródeł.

![Repozytorium pakietu OMS](media/log-analytics-overview/overview.png)

Połączone źródła są hello komputery i inne zasoby, które generują dane zebrane przez analizy dzienników.  Może to obejmować agentów zainstalowanych na komputerach z systemem [Windows](log-analytics-windows-agents.md) i [Linux](log-analytics-linux-agents.md) nawiązujących połączenie bezpośrednio lub agentów w [podłączonej grupie zarządzania programu System Center Operations Manager](log-analytics-om-agents.md).  W przypadku zasobów platformy Azure usługa Log Analytics zbiera dane z usług [Azure Monitor i Azure Diagnostics](log-analytics-azure-storage.md).

[Źródła danych](log-analytics-data-sources.md) są hello różnych rodzajów zebrane podczas każdego połączenia źródła danych.  Obejmuje to [zdarzenia](log-analytics-data-sources-windows-events.md) i [dane dotyczące wydajności](log-analytics-data-sources-performance-counters.md) z [Windows](log-analytics-data-sources-windows-events.md) i agentów systemu Linux w toosources dodanie, takich jak [dzienniki programu IIS](log-analytics-data-sources-iis-logs.md)i [dzienniki tekstowe niestandardowych](log-analytics-data-sources-custom-logs.md).  Możesz skonfigurować dla każdego źródła danych ma toocollect, czy konfiguracja hello jest automatycznie dostarczonego tooeach połączone źródła.

Jeśli masz własne wymagania, a następnie użyć hello [interfejsu API modułów zbierających dane HTTP](log-analytics-data-collector-api.md) toowrite repozytorium toohello danych z klienta interfejsu API REST.

## <a name="log-analytics-architecture"></a>Architektura usługi Log Analytics
wymagania wdrożenia Hello analizy dzienników są minimalne, ponieważ składników centralnej hello znajdują się w hello chmury Azure.  Dotyczy to repozytorium hello dodanie toohello usług, które pozwalają toocorrelate i analizowanie zebranych danych.  Hello portal są dostępne z dowolnej przeglądarki, nie jest wymagane dla oprogramowania klienckiego.

Konieczne jest zainstalowanie agentów na komputerach z systemem [Windows](log-analytics-windows-agents.md) i [Linux](log-analytics-linux-agents.md), ale dla komputerów, które są już elementami członkowskimi [podłączonej grupy zarządzania SCOM](log-analytics-om-agents.md), nie są wymagani żadni dodatkowi agenci.  Agenci SCOM będzie toocommunicate z serwerami zarządzania, które przekazuje ich tooLog danych analizy.  Mimo że niektóre rozwiązania będzie wymagać toocommunicate agentów bezpośrednio z analizy dzienników.  Hello dokumentacji dla poszczególnych rozwiązań będzie określać jego wymagania komunikacji.

Po [utworzeniu konta usługi Log Analytics](log-analytics-get-started.md) zostanie utworzony obszar roboczy pakietu OMS.  Obszar roboczy hello można traktować jako unikatowy środowisko analizy dzienników z własnych danych repozytorium, źródła danych i rozwiązania. Może utworzyć wiele obszarów roboczych w Twojej subskrypcji toosupport wielu środowiskach, takich jak produkcyjnych i testowych.

![Architektura usługi Log Analytics](media/log-analytics-overview/architecture.png)

## <a name="next-steps"></a>Następne kroki
* [Załóż bezpłatne konto analizy dzienników](log-analytics-get-started.md) tootest we własnym środowisku.
* Widok hello różnych [źródeł danych](log-analytics-data-sources.md) toocollect dostępnych danych do repozytorium OMS hello.
* [Przeglądaj dostępne rozwiązania hello w galerii rozwiązań hello](log-analytics-add-solutions.md) tooadd funkcji tooLog Analytics.

