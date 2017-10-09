---
title: zapytania analityczne aaaRun wielu baz danych Azure SQL | Dokumentacja firmy Microsoft
description: "Wyodrębniania danych z baz danych dzierżawy do celów analizy offline bazy danych analizy"
keywords: "samouczek usługi sql database"
services: sql-database
documentationcenter: 
author: stevestein
manager: jhubbard
editor: 
ms.assetid: 
ms.service: sql-database
ms.custom: scale out apps
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/16/2017
ms.author: billgib; sstein
ms.openlocfilehash: f2664e4aafd2fecc98d20d229342bca19b0b08c1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="extract-data-from-tenant-databases-into-an-analytics-database-for-offline-analysis"></a>Wyodrębniania danych z baz danych dzierżawy do celów analizy offline bazy danych analizy

W tym samouczku używamy zapytań toorun zadania elastycznej bazy danych każdej dzierżawy. zadanie Hello wyodrębnia dane sprzedaży biletów i ładuje go do bazy danych analizy (lub magazynu danych) do analizy. Witaj analytics baza danych jest następnie zbadać tooextract wgląd w dane dotyczące tej codziennych danych operacyjnych wszystkich dzierżawców.


Ten samouczek zawiera informacje na temat wykonywania następujących czynności:

> [!div class="checklist"]
> * Tworzenie bazy danych analizy dzierżawy hello
> * Tworzenie danych tooretrieve zaplanowanego zadania i wypełnianie bazy danych analizy hello

toocomplete tego samouczka, Utwórz hello się, że następujące wymagania wstępne są spełnione:

* Aplikacja Wingtip SaaS Hello jest wdrażana. Zobacz toodeploy w mniej niż pięć minut [wdrażania i aplikacji Wingtip SaaS hello](sql-database-saas-tutorial.md)
* Zainstalowany jest program Azure PowerShell. Aby uzyskać szczegółowe informacje, zobacz [Rozpoczynanie pracy z programem Azure PowerShell](https://docs.microsoft.com/powershell/azure/get-started-azureps)
* zainstalowana jest najnowsza wersja Hello programu SQL Server Management Studio (SSMS). [Pobieranie i instalowanie programu SSMS](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms)

## <a name="tenant-operational-analytics-pattern"></a>Wzorzec operacyjnej analizy dzierżaw

Jedną z możliwości dużą hello z aplikacjami SaaS jest toouse hello sformatowanego dzierżawy danych przechowywanych w chmurze hello. Użyj tego danych toogain wgląd w działania hello i użycie aplikacji i dzierżawców. Te dane mogą przeprowadzają opracowanie funkcji, ulepszenia użyteczność i innych inwestycji w aplikacji hello i platformie. Uzyskiwanie dostępu do tych danych w jednej wielodostępnej bazie danych jest łatwe, ale przestaje być proste, gdy są one znacznie rozproszone, potencjalnie nawet na tysiące baz danych. Jeden tooaccessing podejście te dane są zadania elastyczne toouse, umożliwiające zwracanie wyniku wyników zapytania z toobe wykonanie zadania przechwycone dane wyjściowe bazy danych i tabeli.

## <a name="get-hello-wingtip-application-scripts"></a>Pobierz skrypty aplikacji hello Wingtip

Witaj Wingtip SaaS skrypty i kod źródłowy aplikacji są dostępne w hello [WingtipSaaS](https://github.com/Microsoft/WingtipSaaS) repozytorium github. [Kroki skrypty Wingtip SaaS hello toodownload](sql-database-wtp-overview.md#download-and-unblock-the-wingtip-saas-scripts).

## <a name="deploy-a-database-for-tenant-analytics-results"></a>Wdrażanie bazy danych dla wyników analizy dzierżawy

Ten samouczek wymaga toohave hello toocapture wdrożonej bazy danych w wynikach pochodzący z wykonania zadania, skryptów, które zawierają zwracania wyników kwerendy. W tym celu utwórzmy bazę danych o nazwie tenantanalytics.

1. Otwórz... \\Modułów uczenia\\operacyjne Analytics\\Analytics dzierżawy\\*TenantAnalyticsDB.ps1 pokaz* w hello *PowerShell ISE* i ustaw Witaj, następujące wartości:
   * **$DemoScenario** = **2** *Deploy operational analytics database* (Wdrażanie bazy danych analizy operacyjnej)
1. Naciśnij klawisz **F5** toorun hello pokaz skryptu (hello tego wywołania *TenantAnalyticsDB.ps1 Wdróż* skryptu) co powoduje hello dzierżawy analityka w bazie danych.

## <a name="create-some-data-for-hello-demo"></a>Tworzenie części danych pokaz hello

1. Otwórz... \\Modułów uczenia\\operacyjne Analytics\\Analytics dzierżawy\\*TenantAnalyticsDB.ps1 pokaz* w hello *PowerShell ISE* i ustaw Witaj, następujące wartości:
   * **$DemoScenario** = **1** *Purchase tickets for events at all venues* (Zakup biletów dla zdarzeń we wszystkich miejscach)
1. Naciśnij klawisz **F5** toorun hello skryptu i utworzenia biletu zakupu historii.


## <a name="create-a-scheduled-job-tooretrieve-tenant-analytics-about-ticket-purchases"></a>Utwórz zaplanowane zadanie tooretrieve dzierżawy analityczne dotyczące zakupów biletu

Ten skrypt tworzy informacji o zakupie biletu tooretrieve zadania na podstawie wszystkich dzierżawców. Po zagregowane w jednej tabeli, można uzyskać sformatowanego interesującego metryk dotyczących struktury zakupów między dzierżawcami hello biletu.

1. Otwórz program SSMS i połącz toohello katalogu -&lt;użytkownika&gt;. database.windows.net serwera
1. Otwórz plik ...\\Learning Modules\\Operational Analytics\\Tenant Analytics\\*TicketPurchasesfromAllTenants.sql*
1. Modyfikowanie &lt;użytkownika&gt;, nazwa użytkownika hello Użyj używane po wdrożeniu aplikacji Wingtip SaaS hello u góry hello skryptu hello, **sp\_Dodaj\_docelowej\_grupy\_elementuczłonkowskiego** i **sp\_dodać\_etap zadania**
1. Kliknij prawym przyciskiem myszy, wybierz **połączenia**i połącz toohello katalogu -&lt;użytkownika&gt;. database.windows.net serwera, jeśli nie został jeszcze połączony
1. Upewnij się, są połączone toohello **jobaccount** bazy danych i naciśnij klawisz **F5** do uruchamiania skryptu hello

* **SP\_dodać\_docelowej\_grupy** tworzy Nazwa grupy docelowej hello *TenantGroup*, teraz potrzebujemy tooadd członków docelowych.
* **SP\_dodać\_docelowej\_grupy\_elementu członkowskiego** dodaje *serwera* docelowy typ elementu członkowskiego, które uzna za wszystkie bazy danych w ramach tego serwera (to hello customer1 — adnotacja &lt;Użytkownika&gt; serwer zawierający hello dzierżawcy z bazy danych) w czasie zadania wykonywania powinny być uwzględnione w hello zadania.
* **sp\_add\_job** tworzy nowe cotygodniowe zaplanowane zadanie o nazwie „Ticket Purchases from all Tenants”
* **SP\_dodać\_etap zadania** tworzy hello etap zadania zawierające tooretrieve tekst polecenia T-SQL wszystkie informacje zakupu biletu hello ze wszystkich dzierżaw i zwracanie zestawu w tabeli o nazwie wyników hello kopii  *AllTicketsPurchasesfromAllTenants*
* Widoki pozostałych Hello w skrypcie hello wyświetlanie istnienie hello hello obiektów i wykonywania zadania monitorowania. Przejrzyj wartości stanu hello z hello **cyklu życia** stan hello toomonitor kolumny. Jeden raz zakończyło się pomyślnie, hello zadanie zakończone pomyślnie, do wszystkich baz danych dzierżawy i hello dwóch dodatkowych baz danych zawierających hello odwołuje się tabela.

Pomyślnie uruchomienie skryptu hello powinno spowodować podobne wyniki:

![wyniki](media/sql-database-saas-tutorial-tenant-analytics/ticket-purchases-job.png)

## <a name="create-a-job-tooretrieve-a-summary-count-of-ticket-purchases-from-all-tenants"></a>Utwórz tooretrieve zadanie podsumowania liczba biletu zakupy z wszystkich dzierżawców

Ten skrypt tworzy zadanie tooretrieve sumę wszystkich zakupy biletu z wszystkich dzierżawców.

1. Otwórz program SSMS i połącz toohello *katalogu -&lt;użytkownika&gt;. database.windows.net* serwera
1. Otwórz hello pliku... \\Modułów szkoleniowych\\udostępniania i wykaz\\operacyjne Analytics\\dzierżawy Analytics\\*TicketPurchasesfromAllTenants.sql wyników*
1. Modyfikowanie &lt;użytkownika&gt;, nazwa użytkownika hello Użyj używane po wdrożeniu aplikacji Wingtip SaaS hello w skrypcie hello w hello **sp\_dodać\_etap zadania** procedury składowanej
1. Kliknij prawym przyciskiem myszy, wybierz **połączenia**i połącz toohello katalogu -&lt;użytkownika&gt;. database.windows.net serwera, jeśli nie został jeszcze połączony
1. Upewnij się, są połączone toohello **tenantanalytics** bazy danych i naciśnij klawisz **F5** do uruchamiania skryptu hello

Pomyślnie uruchomienie skryptu hello powinno spowodować podobne wyniki:

![wyniki](media/sql-database-saas-tutorial-tenant-analytics/total-sales.png)



* **sp\_add\_job** tworzy nowe cotygodniowe zaplanowane zadanie o nazwie „ResultsTicketsOrders”

* **SP\_dodać\_etap zadania** tworzy hello etap zadania zawierające tooretrieve tekst polecenia T-SQL wszystkie informacje zakupu biletu hello ze wszystkich dzierżaw i hello kopiowania zwracanie zestawu w tabeli o nazwie CountofTicketOrders wyników

* Widoki pozostałych Hello w skrypcie hello wyświetlanie istnienie hello hello obiektów i wykonywania zadania monitorowania. Przejrzyj wartości stanu hello z hello **cyklu życia** stan hello toomonitor kolumny. Jeden raz zakończyło się pomyślnie, hello zadanie zakończone pomyślnie, do wszystkich baz danych dzierżawy i hello dwóch dodatkowych baz danych zawierających hello odwołuje się tabela.


## <a name="next-steps"></a>Następne kroki

W tym samouczku zawarto informacje na temat wykonywania następujących czynności:

> [!div class="checklist"]
> * Wdrażanie analitycznej bazy danych dzierżaw
> * Utwórz zaplanowane zadanie danych analitycznych tooretrieve między dzierżawcami

Gratulacje!

## <a name="additional-resources"></a>Dodatkowe zasoby

* Dodatkowe [samouczki, które zależą od hello aplikacji Wingtip SaaS](sql-database-wtp-overview.md#sql-database-wingtip-saas-tutorials)
* [Zadania elastyczne](sql-database-elastic-jobs-overview.md)
