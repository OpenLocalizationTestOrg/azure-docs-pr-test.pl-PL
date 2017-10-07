---
title: "aaaUse analizy dzienników z aplikacją wielodostępne bazy danych SQL | Dokumentacja firmy Microsoft"
description: "Konfiguracja i analiza dzienników (OMS) za pomocą aplikacji Wingtip SaaS przykładowej bazy danych SQL Azure hello"
keywords: "samouczek usługi sql database"
services: sql-database
documentationcenter: 
author: stevestein
manager: craigg
editor: 
ms.assetid: 
ms.service: sql-database
ms.custom: scale out apps
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/26/2017
ms.author: billgib; sstein
ms.openlocfilehash: fa9085ce3462939e66853faa2a3cd71e0f6c2581
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="setup-and-use-log-analytics-oms-with-hello-wingtip-saas-app"></a>Konfiguracja i analiza dzienników (OMS) za pomocą aplikacji Wingtip SaaS hello

W tym samouczku, konfigurowania i używania *analizy dzienników ([OMS](https://www.microsoft.com/cloud-platform/operations-management-suite))* monitorowania pule elastyczne i baz danych. Opiera się na powitania [Samouczek zarządzania i monitorowania wydajności](sql-database-saas-tutorial-performance-monitoring.md)i pokazuje sposób toouse *analizy dzienników* tooaugment hello monitorowania oraz alertów zawarte w hello portalu Azure. Program Log Analytics jest szczególnie przydatny w przypadku monitorowania i alertów na dużą skalę, ponieważ obsługuje setki pul i setki tysięcy baz danych. Udostępnia również jedno rozwiązanie do monitorowania, w którym można zintegrować monitorowanie różnych aplikacji i usług Azure w wielu subskrypcjach Azure.

Ten samouczek zawiera informacje na temat wykonywania następujących czynności:

> [!div class="checklist"]
> * Instalowanie i konfigurowanie programu Log Analytics (OMS)
> * Użyj analizy dzienników toomonitor pul i baz danych

toocomplete ukończenia tego samouczka, Utwórz hello się, że następujące wymagania wstępne:

* Aplikacja Wingtip SaaS Hello jest wdrażana. Zobacz toodeploy w mniej niż pięć minut [wdrażania i aplikacji Wingtip SaaS hello](sql-database-saas-tutorial.md)
* Zainstalowany jest program Azure PowerShell. Aby uzyskać szczegółowe informacje, zobacz [Rozpoczynanie pracy z programem Azure PowerShell](https://docs.microsoft.com/powershell/azure/get-started-azureps)

Zobacz hello [Samouczek zarządzania i monitorowania wydajności](sql-database-saas-tutorial-performance-monitoring.md) omówienie scenariuszy SaaS hello, wzorców i ich wpływ na wymagania hello na rozwiązanie monitorowania.

## <a name="monitoring-and-managing-performance-with-log-analytics-oms"></a>Monitorowanie i zarządzanie wydajnością za pomocą programu Log Analytics (usługi OMS)

W usłudze SQL Database funkcje monitorowania i zgłaszania alertów są dostępne na poziomie baz danych i pul. Ten wbudowany, monitorowanie i alerty określonych zasobów i wygodną metodą małej liczby zasobów, ale jest mniej dobrze nadają się toomonitoring duże instalacje lub zapewniające ujednoliconego podglądu między różnymi zasobami i subskrypcje.

Programu Log Analytics można używać w scenariuszach dotyczących dużych ilości danych. Jest oddzielne usługa Azure, która zapewnia analityka za pośrednictwem emitowany dzienniki diagnostyczne i dane telemetryczne zebrane w obszaru roboczego analizy dziennika, które można zbierać dane telemetryczne z wielu usług i tooquery używane i Ustaw alerty. Program Log Analytics udostępnia wbudowany język zapytań oraz narzędzia do wizualizacji danych, umożliwiając analizę danych operacyjnych oraz ich wizualizację. Hello rozwiązania analizy SQL zawiera kilka wstępnie zdefiniowanych puli elastycznej i bazy danych monitorowania oraz alertów, widoków i kwerend i umożliwia dodawanie zapytań ad hoc i zapisać je w razie potrzeby. Usługa OMS udostępnia także projektanta widoków niestandardowych.

Rozwiązań obszarów roboczych i analiza analizy dziennika można otworzyć hello portalu Azure oraz OMS. Witaj portalu Azure jest hello nowszej punktu dostępu, ale może być za portalu OMS hello w niektórych obszarach.

### <a name="start-hello-load-generator-toocreate-data-tooanalyze"></a>Uruchom hello obciążenia generator toocreate danych tooanalyze

1. Otwórz **PerformanceMonitoringAndManagement.ps1 pokaz** w hello **PowerShell ISE**. Nie zamykaj tego skryptu jako może być toorun kilka scenariuszy generowania obciążenia hello w tym samouczku.
1. Jeśli masz mniej niż pięć dzierżawcy, Zapewnij partii tooprovide dzierżaw bardziej interesującego kontekstu monitorowania:
   1. Ustaw zmienną **$DemoScenario = 1,** **Provision a batch of tenants** (Aprowizacja partii dzierżaw).
   1. Naciśnij klawisz **F5** toorun hello skryptu.

1. Ustaw zmienną **$DemoScenario** = 2, **Generate normal intensity load (approx 40 DTU)** (Generowanie obciążenia o normalnym natężeniu (ok. 40 jednostek DTU)).
1. Naciśnij klawisz **F5** toorun hello skryptu.

## <a name="get-hello-wingtip-application-scripts"></a>Pobierz skrypty aplikacji hello Wingtip

Witaj biletów Wingtip skrypty i kod źródłowy aplikacji są dostępne w hello [WingtipSaaS](https://github.com/Microsoft/WingtipSaaS) repozytorium github. Pliki skryptów znajdują się w hello [folderu modułów uczenia](https://github.com/Microsoft/WingtipSaaS/tree/master/Learning%20Modules). Pobierz hello **modułów uczenia** komputer lokalny tooyour folderu, zachowaniu jego struktury folderów.

## <a name="installing-and-configuring-log-analytics-and-hello-azure-sql-analytics-solution"></a>Instalowanie i konfigurowanie analizy dzienników i hello rozwiązania analizy SQL Azure

Analiza dzienników jest oddzielne usługa, która ma toobe skonfigurowany. Program Log Analytics gromadzi dane dziennika oraz dane telemetryczne i metryki w obszarze roboczym. Obszar roboczy jest zasobem, podobnie jak inne zasoby na platformie Azure, i musi zostać utworzony. Gdy obszar roboczy hello nie wymaga toobe utworzone w hello tej samej grupy zasobów jako aplikacji hello monitoruje, to często sens hello większości. W przypadku hello aplikacji Wingtip SaaS hello dzięki temu toobe obszaru roboczego hello łatwo usunąć z aplikacji hello przez usunięcie grupy zasobów hello.

1. Otwórz... \\Modułów uczenia\\zarządzania i monitorowania wydajności\\analizy dzienników\\*LogAnalytics.ps1 pokaz* w hello **PowerShell ISE**.
1. Naciśnij klawisz **F5** toorun hello skryptu.

W tym momencie należy stanie otwarte Log Analytics w portalu Azure hello (lub portalu OMS hello). Potrwa kilka minut, aż toobe dane telemetryczne zbierane w obszarze roboczym analizy dzienników hello i toobecome widoczne. będzie Hello pozostanie system hello zbierania się, że dane hello bardziej interesującego środowisko hello dłużej. Teraz jest odpowiedni moment toograb napój — po prostu upewnij się, że generator obciążenia hello jest nadal uruchomiona!


## <a name="use-log-analytics-and-hello-sql-analytics-solution-toomonitor-pools-and-databases"></a>Użyj analizy dzienników i hello pul toomonitor rozwiązania analizy SQL i baz danych


W tym ćwiczeniu Otwórz analizy dzienników i toolook portalu OMS hello na powitania telemetrii zbierana hello baz danych i pul.

1. Przeglądaj toohello [portalu Azure](https://portal.azure.com) i otwórz analizy dzienników, klikając przycisk więcej usług, a następnie wyszukaj analizy dzienników:

   ![otwieranie programu log analytics](media/sql-database-saas-tutorial-log-analytics/log-analytics-open.png)

1. Wybierz obszar roboczy hello o nazwie *wtploganalytics -&lt;użytkownika&gt;*.

1. Wybierz **omówienie** hello tooopen rozwiązania hello portalu Azure Log Analytics.
   ![overview-link](media/sql-database-saas-tutorial-log-analytics/click-overview.png)

    **WAŻNE**: może potrwać kilka minut, zanim rozwiązanie hello jest aktywny. Zachowaj cierpliwość.

1. Kliknij na powitania tooopen kafelka analiza SQL Azure go.

    ![overview](media/sql-database-saas-tutorial-log-analytics/overview.png)

    ![analiza](media/sql-database-saas-tutorial-log-analytics/analytics.png)

1. Witaj widoku w bok, Przewija bloku rozwiązania hello z własnego paska przewijania u dołu hello (odświeżania hello bloku w razie potrzeby).

1. Eksploruj hello różne widoki, klikając na nich lub na poszczególnych zasobów tooopen explorer przechodzenia, których można użyć suwak czasu hello w hello góry po lewej lub kliknij na pionowym pasku toofocus w na mniejszą niż przedział czasu. Z tego widoku można wybrać poszczególnych baz danych lub pul toofocus na określonych zasobów:

    ![wykres](media/sql-database-saas-tutorial-log-analytics/chart.png)

1. Do bloku rozwiązania hello Jeśli przewiń toohello prawej zostanie wyświetlony niektóre zapisane kwerendy kliknij tooopen i Eksploruj. Możesz poeksperymentować, zmieniając je i zapisując wszystkie utworzone przez siebie interesujące zapytania, które następnie będzie można otworzyć i użyć z innymi zasobami.

1. W bloku obszaru roboczego analizy dzienników hello wybierz istnieje rozwiązanie hello tooopen portalu OMS.

    ![oms](media/sql-database-saas-tutorial-log-analytics/oms.png)

1. W portalu OMS hello można skonfigurować alerty. Polecenie hello alertu część hello jednostek dtu w warstwie widoku bazy danych.

1. W hello wyszukiwania dziennika widoku, który zostanie wyświetlony użytkownik zostanie wyświetlona wykres słupkowy metryk hello reprezentowanego.

    ![przeszukiwanie dzienników](media/sql-database-saas-tutorial-log-analytics/log-search.png)

1. Kliknięcie alertu w hello narzędzi będzie konfiguracji alertu hello stanie toosee i można go zmienić.

    ![dodawanie reguły alertu](media/sql-database-saas-tutorial-log-analytics/add-alert.png)

Witaj, monitorowanie i alerty analizy dzienników i OMS na podstawie kwerend nad danymi hello w obszarze roboczym hello, w odróżnieniu od hello alerty na każdego bloku zasobów, która jest specyficzna dla zasobu. W związku z tym można zdefiniować alert sprawdzający wszystkie bazy danych, zamiast definiować po jednym alercie dla każdej bazy danych. Można również napisać alert, który używa złożonego zapytania dla wielu typów zasobów. Zapytania są ograniczone tylko hello danych dostępne w obszarze roboczym hello.

Analiza dzienników bazy danych SQL jest obciążony oparte na powitania ilość danych w obszarze roboczym hello. W tym samouczku utworzono wolnego obszaru roboczego, który jest ograniczona too500MB na dzień. Po osiągnięciu tego limitu danych jest już dodany toohello obszaru roboczego.


## <a name="next-steps"></a>Następne kroki

W tym samouczku zawarto informacje na temat wykonywania następujących czynności:

> [!div class="checklist"]
> * Instalowanie i konfigurowanie programu Log Analytics (OMS)
> * Użyj analizy dzienników toomonitor pul i baz danych

[Samouczek analiz dzierżaw](sql-database-saas-tutorial-tenant-analytics.md)

## <a name="additional-resources"></a>Dodatkowe zasoby

* [Dodatkowe samouczki, które zależą od pierwszego wdrożenia aplikacji Wingtip SaaS hello](sql-database-wtp-overview.md#sql-database-wingtip-saas-tutorials)
* [Program Azure Log Analytics](../log-analytics/log-analytics-azure-sql.md)
* [OMS](https://blogs.technet.microsoft.com/msoms/2017/02/21/azure-sql-analytics-solution-public-preview/)
