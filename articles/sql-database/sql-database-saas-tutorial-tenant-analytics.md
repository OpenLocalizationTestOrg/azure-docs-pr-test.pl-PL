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
# <a name="extract-data-from-tenant-databases-into-an-analytics-database-for-offline-analysis"></a><span data-ttu-id="c177b-104">Wyodrębniania danych z baz danych dzierżawy do celów analizy offline bazy danych analizy</span><span class="sxs-lookup"><span data-stu-id="c177b-104">Extract data from tenant databases into an analytics database for offline analysis</span></span>

<span data-ttu-id="c177b-105">W tym samouczku używamy zapytań toorun zadania elastycznej bazy danych każdej dzierżawy.</span><span class="sxs-lookup"><span data-stu-id="c177b-105">In this tutorial, you use an elastic job toorun queries against each tenant database.</span></span> <span data-ttu-id="c177b-106">zadanie Hello wyodrębnia dane sprzedaży biletów i ładuje go do bazy danych analizy (lub magazynu danych) do analizy.</span><span class="sxs-lookup"><span data-stu-id="c177b-106">hello job extracts ticket sales data and loads it into an analytics database (or data warehouse) for analysis.</span></span> <span data-ttu-id="c177b-107">Witaj analytics baza danych jest następnie zbadać tooextract wgląd w dane dotyczące tej codziennych danych operacyjnych wszystkich dzierżawców.</span><span class="sxs-lookup"><span data-stu-id="c177b-107">hello analytics database is then queried tooextract insights from this day-to-day operational data of all tenants.</span></span>


<span data-ttu-id="c177b-108">Ten samouczek zawiera informacje na temat wykonywania następujących czynności:</span><span class="sxs-lookup"><span data-stu-id="c177b-108">In this tutorial you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="c177b-109">Tworzenie bazy danych analizy dzierżawy hello</span><span class="sxs-lookup"><span data-stu-id="c177b-109">Create hello tenant analytics database</span></span>
> * <span data-ttu-id="c177b-110">Tworzenie danych tooretrieve zaplanowanego zadania i wypełnianie bazy danych analizy hello</span><span class="sxs-lookup"><span data-stu-id="c177b-110">Create a scheduled job tooretrieve data and populate hello analytics database</span></span>

<span data-ttu-id="c177b-111">toocomplete tego samouczka, Utwórz hello się, że następujące wymagania wstępne są spełnione:</span><span class="sxs-lookup"><span data-stu-id="c177b-111">toocomplete this tutorial, make sure hello following prerequisites are met:</span></span>

* <span data-ttu-id="c177b-112">Aplikacja Wingtip SaaS Hello jest wdrażana.</span><span class="sxs-lookup"><span data-stu-id="c177b-112">hello Wingtip SaaS app is deployed.</span></span> <span data-ttu-id="c177b-113">Zobacz toodeploy w mniej niż pięć minut [wdrażania i aplikacji Wingtip SaaS hello](sql-database-saas-tutorial.md)</span><span class="sxs-lookup"><span data-stu-id="c177b-113">toodeploy in less than five minutes, see [Deploy and explore hello Wingtip SaaS application](sql-database-saas-tutorial.md)</span></span>
* <span data-ttu-id="c177b-114">Zainstalowany jest program Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="c177b-114">Azure PowerShell is installed.</span></span> <span data-ttu-id="c177b-115">Aby uzyskać szczegółowe informacje, zobacz [Rozpoczynanie pracy z programem Azure PowerShell](https://docs.microsoft.com/powershell/azure/get-started-azureps)</span><span class="sxs-lookup"><span data-stu-id="c177b-115">For details, see [Getting started with Azure PowerShell](https://docs.microsoft.com/powershell/azure/get-started-azureps)</span></span>
* <span data-ttu-id="c177b-116">zainstalowana jest najnowsza wersja Hello programu SQL Server Management Studio (SSMS).</span><span class="sxs-lookup"><span data-stu-id="c177b-116">hello latest version of SQL Server Management Studio (SSMS) is installed.</span></span> [<span data-ttu-id="c177b-117">Pobieranie i instalowanie programu SSMS</span><span class="sxs-lookup"><span data-stu-id="c177b-117">Download and Install SSMS</span></span>](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms)

## <a name="tenant-operational-analytics-pattern"></a><span data-ttu-id="c177b-118">Wzorzec operacyjnej analizy dzierżaw</span><span class="sxs-lookup"><span data-stu-id="c177b-118">Tenant Operational Analytics pattern</span></span>

<span data-ttu-id="c177b-119">Jedną z możliwości dużą hello z aplikacjami SaaS jest toouse hello sformatowanego dzierżawy danych przechowywanych w chmurze hello.</span><span class="sxs-lookup"><span data-stu-id="c177b-119">One of hello great opportunities with SaaS applications is toouse hello rich tenant data that is stored in hello cloud.</span></span> <span data-ttu-id="c177b-120">Użyj tego danych toogain wgląd w działania hello i użycie aplikacji i dzierżawców.</span><span class="sxs-lookup"><span data-stu-id="c177b-120">Use this data toogain insights into hello operation and usage of your application, and your tenants.</span></span> <span data-ttu-id="c177b-121">Te dane mogą przeprowadzają opracowanie funkcji, ulepszenia użyteczność i innych inwestycji w aplikacji hello i platformie.</span><span class="sxs-lookup"><span data-stu-id="c177b-121">This data can guide feature development, usability improvements, and other investments in hello app and platform.</span></span> <span data-ttu-id="c177b-122">Uzyskiwanie dostępu do tych danych w jednej wielodostępnej bazie danych jest łatwe, ale przestaje być proste, gdy są one znacznie rozproszone, potencjalnie nawet na tysiące baz danych.</span><span class="sxs-lookup"><span data-stu-id="c177b-122">Accessing this data when it's in a single multi-tenant database is easy, but not so easy when distributed at scale across potentially thousands of databases.</span></span> <span data-ttu-id="c177b-123">Jeden tooaccessing podejście te dane są zadania elastyczne toouse, umożliwiające zwracanie wyniku wyników zapytania z toobe wykonanie zadania przechwycone dane wyjściowe bazy danych i tabeli.</span><span class="sxs-lookup"><span data-stu-id="c177b-123">One approach tooaccessing this data is toouse Elastic jobs, which enable result-returning query results from job execution toobe captured in an output database and table.</span></span>

## <a name="get-hello-wingtip-application-scripts"></a><span data-ttu-id="c177b-124">Pobierz skrypty aplikacji hello Wingtip</span><span class="sxs-lookup"><span data-stu-id="c177b-124">Get hello Wingtip application scripts</span></span>

<span data-ttu-id="c177b-125">Witaj Wingtip SaaS skrypty i kod źródłowy aplikacji są dostępne w hello [WingtipSaaS](https://github.com/Microsoft/WingtipSaaS) repozytorium github.</span><span class="sxs-lookup"><span data-stu-id="c177b-125">hello Wingtip SaaS scripts and application source code are available in hello [WingtipSaaS](https://github.com/Microsoft/WingtipSaaS) github repo.</span></span> <span data-ttu-id="c177b-126">[Kroki skrypty Wingtip SaaS hello toodownload](sql-database-wtp-overview.md#download-and-unblock-the-wingtip-saas-scripts).</span><span class="sxs-lookup"><span data-stu-id="c177b-126">[Steps toodownload hello Wingtip SaaS scripts](sql-database-wtp-overview.md#download-and-unblock-the-wingtip-saas-scripts).</span></span>

## <a name="deploy-a-database-for-tenant-analytics-results"></a><span data-ttu-id="c177b-127">Wdrażanie bazy danych dla wyników analizy dzierżawy</span><span class="sxs-lookup"><span data-stu-id="c177b-127">Deploy a database for tenant analytics results</span></span>

<span data-ttu-id="c177b-128">Ten samouczek wymaga toohave hello toocapture wdrożonej bazy danych w wynikach pochodzący z wykonania zadania, skryptów, które zawierają zwracania wyników kwerendy.</span><span class="sxs-lookup"><span data-stu-id="c177b-128">This tutorial requires you toohave a database deployed toocapture hello results from job execution of scripts, which contain results-returning queries.</span></span> <span data-ttu-id="c177b-129">W tym celu utwórzmy bazę danych o nazwie tenantanalytics.</span><span class="sxs-lookup"><span data-stu-id="c177b-129">Let's create a database called tenantanalytics for this purpose.</span></span>

1. <span data-ttu-id="c177b-130">Otwórz... \\Modułów uczenia\\operacyjne Analytics\\Analytics dzierżawy\\*TenantAnalyticsDB.ps1 pokaz* w hello *PowerShell ISE* i ustaw Witaj, następujące wartości:</span><span class="sxs-lookup"><span data-stu-id="c177b-130">Open …\\Learning Modules\\Operational Analytics\\Tenant Analytics\\*Demo-TenantAnalyticsDB.ps1* in hello *PowerShell ISE* and set hello following value:</span></span>
   * <span data-ttu-id="c177b-131">**$DemoScenario** = **2** *Deploy operational analytics database* (Wdrażanie bazy danych analizy operacyjnej)</span><span class="sxs-lookup"><span data-stu-id="c177b-131">**$DemoScenario** = **2** *Deploy operational analytics database*</span></span>
1. <span data-ttu-id="c177b-132">Naciśnij klawisz **F5** toorun hello pokaz skryptu (hello tego wywołania *TenantAnalyticsDB.ps1 Wdróż* skryptu) co powoduje hello dzierżawy analityka w bazie danych.</span><span class="sxs-lookup"><span data-stu-id="c177b-132">Press **F5** toorun hello demo script (that calls hello *Deploy-TenantAnalyticsDB.ps1* script) which creates hello tenant analytics database.</span></span>

## <a name="create-some-data-for-hello-demo"></a><span data-ttu-id="c177b-133">Tworzenie części danych pokaz hello</span><span class="sxs-lookup"><span data-stu-id="c177b-133">Create some data for hello demo</span></span>

1. <span data-ttu-id="c177b-134">Otwórz... \\Modułów uczenia\\operacyjne Analytics\\Analytics dzierżawy\\*TenantAnalyticsDB.ps1 pokaz* w hello *PowerShell ISE* i ustaw Witaj, następujące wartości:</span><span class="sxs-lookup"><span data-stu-id="c177b-134">Open …\\Learning Modules\\Operational Analytics\\Tenant Analytics\\*Demo-TenantAnalyticsDB.ps1* in hello *PowerShell ISE* and set hello following value:</span></span>
   * <span data-ttu-id="c177b-135">**$DemoScenario** = **1** *Purchase tickets for events at all venues* (Zakup biletów dla zdarzeń we wszystkich miejscach)</span><span class="sxs-lookup"><span data-stu-id="c177b-135">**$DemoScenario** = **1** *Purchase tickets for events at all venues*</span></span>
1. <span data-ttu-id="c177b-136">Naciśnij klawisz **F5** toorun hello skryptu i utworzenia biletu zakupu historii.</span><span class="sxs-lookup"><span data-stu-id="c177b-136">Press **F5** toorun hello script and create ticket purchasing history.</span></span>


## <a name="create-a-scheduled-job-tooretrieve-tenant-analytics-about-ticket-purchases"></a><span data-ttu-id="c177b-137">Utwórz zaplanowane zadanie tooretrieve dzierżawy analityczne dotyczące zakupów biletu</span><span class="sxs-lookup"><span data-stu-id="c177b-137">Create a scheduled job tooretrieve tenant analytics about ticket purchases</span></span>

<span data-ttu-id="c177b-138">Ten skrypt tworzy informacji o zakupie biletu tooretrieve zadania na podstawie wszystkich dzierżawców.</span><span class="sxs-lookup"><span data-stu-id="c177b-138">This script creates a job tooretrieve ticket purchase information from all tenants.</span></span> <span data-ttu-id="c177b-139">Po zagregowane w jednej tabeli, można uzyskać sformatowanego interesującego metryk dotyczących struktury zakupów między dzierżawcami hello biletu.</span><span class="sxs-lookup"><span data-stu-id="c177b-139">Once aggregated into a single table, you can gain rich insightful metrics about ticket purchasing patterns across hello tenants.</span></span>

1. <span data-ttu-id="c177b-140">Otwórz program SSMS i połącz toohello katalogu -&lt;użytkownika&gt;. database.windows.net serwera</span><span class="sxs-lookup"><span data-stu-id="c177b-140">Open SSMS and connect toohello catalog-&lt;user&gt;.database.windows.net server</span></span>
1. <span data-ttu-id="c177b-141">Otwórz plik ...\\Learning Modules\\Operational Analytics\\Tenant Analytics\\*TicketPurchasesfromAllTenants.sql*</span><span class="sxs-lookup"><span data-stu-id="c177b-141">Open ...\\Learning Modules\\Operational Analytics\\Tenant Analytics\\*TicketPurchasesfromAllTenants.sql*</span></span>
1. <span data-ttu-id="c177b-142">Modyfikowanie &lt;użytkownika&gt;, nazwa użytkownika hello Użyj używane po wdrożeniu aplikacji Wingtip SaaS hello u góry hello skryptu hello, **sp\_Dodaj\_docelowej\_grupy\_elementuczłonkowskiego** i **sp\_dodać\_etap zadania**</span><span class="sxs-lookup"><span data-stu-id="c177b-142">Modify &lt;User&gt;, use hello user name used when you deployed hello Wingtip SaaS app at hello top of hello script, **sp\_add\_target\_group\_member** and **sp\_add\_jobstep**</span></span>
1. <span data-ttu-id="c177b-143">Kliknij prawym przyciskiem myszy, wybierz **połączenia**i połącz toohello katalogu -&lt;użytkownika&gt;. database.windows.net serwera, jeśli nie został jeszcze połączony</span><span class="sxs-lookup"><span data-stu-id="c177b-143">Right click, select **Connection**, and connect toohello catalog-&lt;User&gt;.database.windows.net server, if not already connected</span></span>
1. <span data-ttu-id="c177b-144">Upewnij się, są połączone toohello **jobaccount** bazy danych i naciśnij klawisz **F5** do uruchamiania skryptu hello</span><span class="sxs-lookup"><span data-stu-id="c177b-144">Ensure you are connected toohello **jobaccount** database and press **F5** to run hello script</span></span>

* <span data-ttu-id="c177b-145">**SP\_dodać\_docelowej\_grupy** tworzy Nazwa grupy docelowej hello *TenantGroup*, teraz potrzebujemy tooadd członków docelowych.</span><span class="sxs-lookup"><span data-stu-id="c177b-145">**sp\_add\_target\_group** creates hello target group name *TenantGroup*, now we need tooadd target members.</span></span>
* <span data-ttu-id="c177b-146">**SP\_dodać\_docelowej\_grupy\_elementu członkowskiego** dodaje *serwera* docelowy typ elementu członkowskiego, które uzna za wszystkie bazy danych w ramach tego serwera (to hello customer1 — adnotacja &lt;Użytkownika&gt; serwer zawierający hello dzierżawcy z bazy danych) w czasie zadania wykonywania powinny być uwzględnione w hello zadania.</span><span class="sxs-lookup"><span data-stu-id="c177b-146">**sp\_add\_target\_group\_member** adds a *server* target member type, which deems all databases within that server (note this is hello customer1-&lt;User&gt; server containing hello tenant databases) at time of job execution should be included in hello job.</span></span>
* <span data-ttu-id="c177b-147">**sp\_add\_job** tworzy nowe cotygodniowe zaplanowane zadanie o nazwie „Ticket Purchases from all Tenants”</span><span class="sxs-lookup"><span data-stu-id="c177b-147">**sp\_add\_job** creates a new weekly scheduled job called “Ticket Purchases from all Tenants”</span></span>
* <span data-ttu-id="c177b-148">**SP\_dodać\_etap zadania** tworzy hello etap zadania zawierające tooretrieve tekst polecenia T-SQL wszystkie informacje zakupu biletu hello ze wszystkich dzierżaw i zwracanie zestawu w tabeli o nazwie wyników hello kopii  *AllTicketsPurchasesfromAllTenants*</span><span class="sxs-lookup"><span data-stu-id="c177b-148">**sp\_add\_jobstep** creates hello job step containing T-SQL command text tooretrieve all hello ticket purchase information from all tenants and copy hello returning result set into a table called *AllTicketsPurchasesfromAllTenants*</span></span>
* <span data-ttu-id="c177b-149">Widoki pozostałych Hello w skrypcie hello wyświetlanie istnienie hello hello obiektów i wykonywania zadania monitorowania.</span><span class="sxs-lookup"><span data-stu-id="c177b-149">hello remaining views in hello script display hello existence of hello objects and monitor job execution.</span></span> <span data-ttu-id="c177b-150">Przejrzyj wartości stanu hello z hello **cyklu życia** stan hello toomonitor kolumny.</span><span class="sxs-lookup"><span data-stu-id="c177b-150">Review hello status value from hello **lifecycle** column toomonitor hello status.</span></span> <span data-ttu-id="c177b-151">Jeden raz zakończyło się pomyślnie, hello zadanie zakończone pomyślnie, do wszystkich baz danych dzierżawy i hello dwóch dodatkowych baz danych zawierających hello odwołuje się tabela.</span><span class="sxs-lookup"><span data-stu-id="c177b-151">Once, Succeeded, hello job has successfully finished on all tenant databases and hello two additional databases containing hello reference table.</span></span>

<span data-ttu-id="c177b-152">Pomyślnie uruchomienie skryptu hello powinno spowodować podobne wyniki:</span><span class="sxs-lookup"><span data-stu-id="c177b-152">Successfully running hello script should result in similar results:</span></span>

![wyniki](media/sql-database-saas-tutorial-tenant-analytics/ticket-purchases-job.png)

## <a name="create-a-job-tooretrieve-a-summary-count-of-ticket-purchases-from-all-tenants"></a><span data-ttu-id="c177b-154">Utwórz tooretrieve zadanie podsumowania liczba biletu zakupy z wszystkich dzierżawców</span><span class="sxs-lookup"><span data-stu-id="c177b-154">Create a job tooretrieve a summary count of ticket purchases from all tenants</span></span>

<span data-ttu-id="c177b-155">Ten skrypt tworzy zadanie tooretrieve sumę wszystkich zakupy biletu z wszystkich dzierżawców.</span><span class="sxs-lookup"><span data-stu-id="c177b-155">This script creates a job tooretrieve sum of all ticket purchases from all tenants.</span></span>

1. <span data-ttu-id="c177b-156">Otwórz program SSMS i połącz toohello *katalogu -&lt;użytkownika&gt;. database.windows.net* serwera</span><span class="sxs-lookup"><span data-stu-id="c177b-156">Open SSMS and connect toohello *catalog-&lt;User&gt;.database.windows.net* server</span></span>
1. <span data-ttu-id="c177b-157">Otwórz hello pliku... \\Modułów szkoleniowych\\udostępniania i wykaz\\operacyjne Analytics\\dzierżawy Analytics\\*TicketPurchasesfromAllTenants.sql wyników*</span><span class="sxs-lookup"><span data-stu-id="c177b-157">Open hello file …\\Learning Modules\\Provision and Catalog\\Operational Analytics\\Tenant Analytics\\*Results-TicketPurchasesfromAllTenants.sql*</span></span>
1. <span data-ttu-id="c177b-158">Modyfikowanie &lt;użytkownika&gt;, nazwa użytkownika hello Użyj używane po wdrożeniu aplikacji Wingtip SaaS hello w skrypcie hello w hello **sp\_dodać\_etap zadania** procedury składowanej</span><span class="sxs-lookup"><span data-stu-id="c177b-158">Modify &lt;User&gt;, use hello user name used when you deployed hello Wingtip SaaS app in hello script, in hello **sp\_add\_jobstep** stored procedure</span></span>
1. <span data-ttu-id="c177b-159">Kliknij prawym przyciskiem myszy, wybierz **połączenia**i połącz toohello katalogu -&lt;użytkownika&gt;. database.windows.net serwera, jeśli nie został jeszcze połączony</span><span class="sxs-lookup"><span data-stu-id="c177b-159">Right click, select **Connection**, and connect toohello catalog-&lt;User&gt;.database.windows.net server, if not already connected</span></span>
1. <span data-ttu-id="c177b-160">Upewnij się, są połączone toohello **tenantanalytics** bazy danych i naciśnij klawisz **F5** do uruchamiania skryptu hello</span><span class="sxs-lookup"><span data-stu-id="c177b-160">Ensure you are connected toohello **tenantanalytics** database and press **F5** to run hello script</span></span>

<span data-ttu-id="c177b-161">Pomyślnie uruchomienie skryptu hello powinno spowodować podobne wyniki:</span><span class="sxs-lookup"><span data-stu-id="c177b-161">Successfully running hello script should result in similar results:</span></span>

![wyniki](media/sql-database-saas-tutorial-tenant-analytics/total-sales.png)



* <span data-ttu-id="c177b-163">**sp\_add\_job** tworzy nowe cotygodniowe zaplanowane zadanie o nazwie „ResultsTicketsOrders”</span><span class="sxs-lookup"><span data-stu-id="c177b-163">**sp\_add\_job** creates a new weekly scheduled job called “ResultsTicketsOrders”</span></span>

* <span data-ttu-id="c177b-164">**SP\_dodać\_etap zadania** tworzy hello etap zadania zawierające tooretrieve tekst polecenia T-SQL wszystkie informacje zakupu biletu hello ze wszystkich dzierżaw i hello kopiowania zwracanie zestawu w tabeli o nazwie CountofTicketOrders wyników</span><span class="sxs-lookup"><span data-stu-id="c177b-164">**sp\_add\_jobstep** creates hello job step containing T-SQL command text tooretrieve all hello ticket purchase information from all tenants and copy hello returning result set into a table called CountofTicketOrders</span></span>

* <span data-ttu-id="c177b-165">Widoki pozostałych Hello w skrypcie hello wyświetlanie istnienie hello hello obiektów i wykonywania zadania monitorowania.</span><span class="sxs-lookup"><span data-stu-id="c177b-165">hello remaining views in hello script display hello existence of hello objects and monitor job execution.</span></span> <span data-ttu-id="c177b-166">Przejrzyj wartości stanu hello z hello **cyklu życia** stan hello toomonitor kolumny.</span><span class="sxs-lookup"><span data-stu-id="c177b-166">Review hello status value from hello **lifecycle** column toomonitor hello status.</span></span> <span data-ttu-id="c177b-167">Jeden raz zakończyło się pomyślnie, hello zadanie zakończone pomyślnie, do wszystkich baz danych dzierżawy i hello dwóch dodatkowych baz danych zawierających hello odwołuje się tabela.</span><span class="sxs-lookup"><span data-stu-id="c177b-167">Once, Succeeded, hello job has successfully finished on all tenant databases and hello two additional databases containing hello reference table.</span></span>


## <a name="next-steps"></a><span data-ttu-id="c177b-168">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="c177b-168">Next steps</span></span>

<span data-ttu-id="c177b-169">W tym samouczku zawarto informacje na temat wykonywania następujących czynności:</span><span class="sxs-lookup"><span data-stu-id="c177b-169">In this tutorial you learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="c177b-170">Wdrażanie analitycznej bazy danych dzierżaw</span><span class="sxs-lookup"><span data-stu-id="c177b-170">Deploy a tenant analytics database</span></span>
> * <span data-ttu-id="c177b-171">Utwórz zaplanowane zadanie danych analitycznych tooretrieve między dzierżawcami</span><span class="sxs-lookup"><span data-stu-id="c177b-171">Create a scheduled job tooretrieve analytical data across tenants</span></span>

<span data-ttu-id="c177b-172">Gratulacje!</span><span class="sxs-lookup"><span data-stu-id="c177b-172">Congratulations!</span></span>

## <a name="additional-resources"></a><span data-ttu-id="c177b-173">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="c177b-173">Additional resources</span></span>

* <span data-ttu-id="c177b-174">Dodatkowe [samouczki, które zależą od hello aplikacji Wingtip SaaS](sql-database-wtp-overview.md#sql-database-wingtip-saas-tutorials)</span><span class="sxs-lookup"><span data-stu-id="c177b-174">Additional [tutorials that build upon hello Wingtip SaaS application](sql-database-wtp-overview.md#sql-database-wingtip-saas-tutorials)</span></span>
* [<span data-ttu-id="c177b-175">Zadania elastyczne</span><span class="sxs-lookup"><span data-stu-id="c177b-175">Elastic Jobs</span></span>](sql-database-elastic-jobs-overview.md)
