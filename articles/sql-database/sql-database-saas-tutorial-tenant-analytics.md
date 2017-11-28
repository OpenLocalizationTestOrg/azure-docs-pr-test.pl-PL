---
title: "Uruchamianie analitycznych zapytań w wielu bazach danych Azure SQL | Microsoft Docs"
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
ms.openlocfilehash: 4e32407d5f321198358e07980907c3420aaf56c6
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="extract-data-from-tenant-databases-into-an-analytics-database-for-offline-analysis"></a><span data-ttu-id="a0359-104">Wyodrębniania danych z baz danych dzierżawy do celów analizy offline bazy danych analizy</span><span class="sxs-lookup"><span data-stu-id="a0359-104">Extract data from tenant databases into an analytics database for offline analysis</span></span>

<span data-ttu-id="a0359-105">W tym samouczku elastycznej zadanie służy do wykonywania kwerend do każdej dzierżawy bazy danych.</span><span class="sxs-lookup"><span data-stu-id="a0359-105">In this tutorial, you use an elastic job to run queries against each tenant database.</span></span> <span data-ttu-id="a0359-106">To zadanie umożliwia wyodrębnianie danych sprzedaży biletów i ładuje go do bazy danych analizy (lub magazynu danych) do analizy.</span><span class="sxs-lookup"><span data-stu-id="a0359-106">The job extracts ticket sales data and loads it into an analytics database (or data warehouse) for analysis.</span></span> <span data-ttu-id="a0359-107">Baza danych analizy następnie jest poddawany kwerendzie można wyodrębnić szczegółowych informacji z tego codziennych danych operacyjnych wszystkich dzierżawców.</span><span class="sxs-lookup"><span data-stu-id="a0359-107">The analytics database is then queried to extract insights from this day-to-day operational data of all tenants.</span></span>


<span data-ttu-id="a0359-108">Ten samouczek zawiera informacje na temat wykonywania następujących czynności:</span><span class="sxs-lookup"><span data-stu-id="a0359-108">In this tutorial you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="a0359-109">Tworzenie analitycznej bazy danych dzierżaw</span><span class="sxs-lookup"><span data-stu-id="a0359-109">Create the tenant analytics database</span></span>
> * <span data-ttu-id="a0359-110">Tworzenie zaplanowanego zadania do pobierania danych i wypełniania analitycznej bazy danych</span><span class="sxs-lookup"><span data-stu-id="a0359-110">Create a scheduled job to retrieve data and populate the analytics database</span></span>

<span data-ttu-id="a0359-111">Do wykonania zadań opisanych w tym samouczku niezbędne jest spełnienie następujących wymagań wstępnych:</span><span class="sxs-lookup"><span data-stu-id="a0359-111">To complete this tutorial, make sure the following prerequisites are met:</span></span>

* <span data-ttu-id="a0359-112">Aplikacja Wingtip SaaS jest wdrażana.</span><span class="sxs-lookup"><span data-stu-id="a0359-112">The Wingtip SaaS app is deployed.</span></span> <span data-ttu-id="a0359-113">Aby wdrożyć w mniej niż 5 minut, zobacz [wdrażania i aplikacji Wingtip SaaS](sql-database-saas-tutorial.md)</span><span class="sxs-lookup"><span data-stu-id="a0359-113">To deploy in less than five minutes, see [Deploy and explore the Wingtip SaaS application](sql-database-saas-tutorial.md)</span></span>
* <span data-ttu-id="a0359-114">Zainstalowany jest program Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="a0359-114">Azure PowerShell is installed.</span></span> <span data-ttu-id="a0359-115">Aby uzyskać szczegółowe informacje, zobacz [Rozpoczynanie pracy z programem Azure PowerShell](https://docs.microsoft.com/powershell/azure/get-started-azureps)</span><span class="sxs-lookup"><span data-stu-id="a0359-115">For details, see [Getting started with Azure PowerShell](https://docs.microsoft.com/powershell/azure/get-started-azureps)</span></span>
* <span data-ttu-id="a0359-116">Zainstalowano najnowszą wersję programu SSMS (SQL Server Management Studio).</span><span class="sxs-lookup"><span data-stu-id="a0359-116">The latest version of SQL Server Management Studio (SSMS) is installed.</span></span> [<span data-ttu-id="a0359-117">Pobieranie i instalowanie programu SSMS</span><span class="sxs-lookup"><span data-stu-id="a0359-117">Download and Install SSMS</span></span>](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms)

## <a name="tenant-operational-analytics-pattern"></a><span data-ttu-id="a0359-118">Wzorzec operacyjnej analizy dzierżaw</span><span class="sxs-lookup"><span data-stu-id="a0359-118">Tenant Operational Analytics pattern</span></span>

<span data-ttu-id="a0359-119">Jedną z najważniejszych zalet aplikacji SaaS jest możliwość użycia dużych ilości danych dotyczących dzierżaw, które są przechowywane w chmurze.</span><span class="sxs-lookup"><span data-stu-id="a0359-119">One of the great opportunities with SaaS applications is to use the rich tenant data that is stored in the cloud.</span></span> <span data-ttu-id="a0359-120">Użyj tych danych, aby uzyskać wgląd w działanie i wykorzystanie swojej aplikacji i swoich dzierżaw.</span><span class="sxs-lookup"><span data-stu-id="a0359-120">Use this data to gain insights into the operation and usage of your application, and your tenants.</span></span> <span data-ttu-id="a0359-121">Te dane mogą ukierunkować rozwój funkcji, usprawnienia w zakresie użyteczności oraz inne inwestycje w aplikacje i platformę.</span><span class="sxs-lookup"><span data-stu-id="a0359-121">This data can guide feature development, usability improvements, and other investments in the app and platform.</span></span> <span data-ttu-id="a0359-122">Uzyskiwanie dostępu do tych danych w jednej wielodostępnej bazie danych jest łatwe, ale przestaje być proste, gdy są one znacznie rozproszone, potencjalnie nawet na tysiące baz danych.</span><span class="sxs-lookup"><span data-stu-id="a0359-122">Accessing this data when it's in a single multi-tenant database is easy, but not so easy when distributed at scale across potentially thousands of databases.</span></span> <span data-ttu-id="a0359-123">Jednym z podejść do uzyskiwania dostępu do tych danych jest użycie elastycznych zadań, umożliwiających zwracanie wyników zapytania z wykonywanego zadania i ich przesyłanie do wyjściowej bazy danych i tabeli.</span><span class="sxs-lookup"><span data-stu-id="a0359-123">One approach to accessing this data is to use Elastic jobs, which enable result-returning query results from job execution to be captured in an output database and table.</span></span>

## <a name="get-the-wingtip-application-scripts"></a><span data-ttu-id="a0359-124">Pobieranie skryptów aplikacji Wingtip</span><span class="sxs-lookup"><span data-stu-id="a0359-124">Get the Wingtip application scripts</span></span>

<span data-ttu-id="a0359-125">Wingtip SaaS skrypty i kod źródłowy aplikacji są dostępne w [WingtipSaaS](https://github.com/Microsoft/WingtipSaaS) repozytorium github.</span><span class="sxs-lookup"><span data-stu-id="a0359-125">The Wingtip SaaS scripts and application source code are available in the [WingtipSaaS](https://github.com/Microsoft/WingtipSaaS) github repo.</span></span> <span data-ttu-id="a0359-126">[Kroki, aby pobrać skrypty Wingtip SaaS](sql-database-wtp-overview.md#download-and-unblock-the-wingtip-saas-scripts).</span><span class="sxs-lookup"><span data-stu-id="a0359-126">[Steps to download the Wingtip SaaS scripts](sql-database-wtp-overview.md#download-and-unblock-the-wingtip-saas-scripts).</span></span>

## <a name="deploy-a-database-for-tenant-analytics-results"></a><span data-ttu-id="a0359-127">Wdrażanie bazy danych dla wyników analizy dzierżawy</span><span class="sxs-lookup"><span data-stu-id="a0359-127">Deploy a database for tenant analytics results</span></span>

<span data-ttu-id="a0359-128">Ten samouczek wymaga posiadania bazy danych wdrożonej w celu przechwytywania wyników wykonania zadania skryptów, które zawierają zapytania zwracające wyniki.</span><span class="sxs-lookup"><span data-stu-id="a0359-128">This tutorial requires you to have a database deployed to capture the results from job execution of scripts, which contain results-returning queries.</span></span> <span data-ttu-id="a0359-129">W tym celu utwórzmy bazę danych o nazwie tenantanalytics.</span><span class="sxs-lookup"><span data-stu-id="a0359-129">Let's create a database called tenantanalytics for this purpose.</span></span>

1. <span data-ttu-id="a0359-130">Otwórz plik ...\\Learning Modules\\Operational Analytics\\Tenant Analytics\\*Demo-TenantAnalyticsDB.ps1* w programie *PowerShell ISE* i ustaw następującą wartość:</span><span class="sxs-lookup"><span data-stu-id="a0359-130">Open …\\Learning Modules\\Operational Analytics\\Tenant Analytics\\*Demo-TenantAnalyticsDB.ps1* in the *PowerShell ISE* and set the following value:</span></span>
   * <span data-ttu-id="a0359-131">**$DemoScenario** = **2** *Deploy operational analytics database* (Wdrażanie bazy danych analizy operacyjnej)</span><span class="sxs-lookup"><span data-stu-id="a0359-131">**$DemoScenario** = **2** *Deploy operational analytics database*</span></span>
1. <span data-ttu-id="a0359-132">Naciśnij klawisz **F5**, aby uruchomić skrypt pokazowy (który wywołuje skrypt *Deploy-TenantAnalyticsDB.ps1*) tworzący bazę danych analizy dzierżaw.</span><span class="sxs-lookup"><span data-stu-id="a0359-132">Press **F5** to run the demo script (that calls the *Deploy-TenantAnalyticsDB.ps1* script) which creates the tenant analytics database.</span></span>

## <a name="create-some-data-for-the-demo"></a><span data-ttu-id="a0359-133">Tworzenie danych demonstracyjnych</span><span class="sxs-lookup"><span data-stu-id="a0359-133">Create some data for the demo</span></span>

1. <span data-ttu-id="a0359-134">Otwórz plik ...\\Learning Modules\\Operational Analytics\\Tenant Analytics\\*Demo-TenantAnalyticsDB.ps1* w programie *PowerShell ISE* i ustaw następującą wartość:</span><span class="sxs-lookup"><span data-stu-id="a0359-134">Open …\\Learning Modules\\Operational Analytics\\Tenant Analytics\\*Demo-TenantAnalyticsDB.ps1* in the *PowerShell ISE* and set the following value:</span></span>
   * <span data-ttu-id="a0359-135">**$DemoScenario** = **1** *Purchase tickets for events at all venues* (Zakup biletów dla zdarzeń we wszystkich miejscach)</span><span class="sxs-lookup"><span data-stu-id="a0359-135">**$DemoScenario** = **1** *Purchase tickets for events at all venues*</span></span>
1. <span data-ttu-id="a0359-136">Naciśnij klawisz **F5**, aby uruchomić skrypt i utworzyć historię zakupów biletów.</span><span class="sxs-lookup"><span data-stu-id="a0359-136">Press **F5** to run the script and create ticket purchasing history.</span></span>


## <a name="create-a-scheduled-job-to-retrieve-tenant-analytics-about-ticket-purchases"></a><span data-ttu-id="a0359-137">Tworzenie zaplanowanego zadania do pobierania informacji analitycznych dotyczących zakupów biletów</span><span class="sxs-lookup"><span data-stu-id="a0359-137">Create a scheduled job to retrieve tenant analytics about ticket purchases</span></span>

<span data-ttu-id="a0359-138">Ten skrypt tworzy zadanie do pobierania informacji o zakupie biletów ze wszystkich dzierżaw.</span><span class="sxs-lookup"><span data-stu-id="a0359-138">This script creates a job to retrieve ticket purchase information from all tenants.</span></span> <span data-ttu-id="a0359-139">Po ich zagregowaniu do pojedynczej tabeli można uzyskać szczegółowy wgląd w metryki związane z wzorcami zakupów biletów we wszystkich dzierżawach.</span><span class="sxs-lookup"><span data-stu-id="a0359-139">Once aggregated into a single table, you can gain rich insightful metrics about ticket purchasing patterns across the tenants.</span></span>

1. <span data-ttu-id="a0359-140">Otwórz aplikację SSMS i połącz się z serwerem catalog-&lt;użytkownik&gt;.database.windows.net</span><span class="sxs-lookup"><span data-stu-id="a0359-140">Open SSMS and connect to the catalog-&lt;user&gt;.database.windows.net server</span></span>
1. <span data-ttu-id="a0359-141">Otwórz plik ...\\Learning Modules\\Operational Analytics\\Tenant Analytics\\*TicketPurchasesfromAllTenants.sql*</span><span class="sxs-lookup"><span data-stu-id="a0359-141">Open ...\\Learning Modules\\Operational Analytics\\Tenant Analytics\\*TicketPurchasesfromAllTenants.sql*</span></span>
1. <span data-ttu-id="a0359-142">Modyfikowanie &lt;użytkownika&gt;, należy użyć nazwy użytkownika używane w przypadku wdrażania aplikacji Wingtip SaaS na początku skryptu, **sp\_dodać\_docelowej\_grupy\_elementu członkowskiego** i **sp\_dodać\_etap zadania**</span><span class="sxs-lookup"><span data-stu-id="a0359-142">Modify &lt;User&gt;, use the user name used when you deployed the Wingtip SaaS app at the top of the script, **sp\_add\_target\_group\_member** and **sp\_add\_jobstep**</span></span>
1. <span data-ttu-id="a0359-143">Kliknij prawym przyciskiem myszy, wybierz **połączenia**i połącz się katalogu -&lt;użytkownika&gt;. database.windows.net serwera, jeśli nie został jeszcze połączony</span><span class="sxs-lookup"><span data-stu-id="a0359-143">Right click, select **Connection**, and connect to the catalog-&lt;User&gt;.database.windows.net server, if not already connected</span></span>
1. <span data-ttu-id="a0359-144">Upewnij się, że masz połączenie z bazą danych **jobaccount**, a następnie naciśnij klawisz **F5**, aby uruchomić skrypt.</span><span class="sxs-lookup"><span data-stu-id="a0359-144">Ensure you are connected to the **jobaccount** database and press **F5** to run the script</span></span>

* <span data-ttu-id="a0359-145">**sp\_add\_target\_group** tworzy nazwę grupy docelowej *TenantGroup*, teraz należy dodać docelowe elementy członkowskie.</span><span class="sxs-lookup"><span data-stu-id="a0359-145">**sp\_add\_target\_group** creates the target group name *TenantGroup*, now we need to add target members.</span></span>
* <span data-ttu-id="a0359-146">**SP\_dodać\_docelowej\_grupy\_elementu członkowskiego** dodaje *serwera* docelowy typ elementu członkowskiego, które uzna za wszystkie bazy danych w ramach tego serwera (należy pamiętać, jest to customer1 -&lt;użytkownika&gt; serwer zawierający dzierżawy baz danych) w czasie zadania wykonywania powinny być uwzględnione w zadaniu.</span><span class="sxs-lookup"><span data-stu-id="a0359-146">**sp\_add\_target\_group\_member** adds a *server* target member type, which deems all databases within that server (note this is the customer1-&lt;User&gt; server containing the tenant databases) at time of job execution should be included in the job.</span></span>
* <span data-ttu-id="a0359-147">**sp\_add\_job** tworzy nowe cotygodniowe zaplanowane zadanie o nazwie „Ticket Purchases from all Tenants”</span><span class="sxs-lookup"><span data-stu-id="a0359-147">**sp\_add\_job** creates a new weekly scheduled job called “Ticket Purchases from all Tenants”</span></span>
* <span data-ttu-id="a0359-148">**sp\_add\_jobstep** tworzy krok zadania zawierający tekst polecenia T-SQL służącego do pobierania wszystkich informacji o zakupach biletów ze wszystkich dzierżaw i kopiowania zestawu zwracanych wyników do tabeli o nazwie *AllTicketsPurchasesfromAllTenants*</span><span class="sxs-lookup"><span data-stu-id="a0359-148">**sp\_add\_jobstep** creates the job step containing T-SQL command text to retrieve all the ticket purchase information from all tenants and copy the returning result set into a table called *AllTicketsPurchasesfromAllTenants*</span></span>
* <span data-ttu-id="a0359-149">Pozostałe widoki w skrypcie dotyczą istnienia obiektów i monitorowania wykonania zadań.</span><span class="sxs-lookup"><span data-stu-id="a0359-149">The remaining views in the script display the existence of the objects and monitor job execution.</span></span> <span data-ttu-id="a0359-150">Sprawdź wartość stanu w kolumnie **lifecycle**, aby monitorować stan.</span><span class="sxs-lookup"><span data-stu-id="a0359-150">Review the status value from the **lifecycle** column to monitor the status.</span></span> <span data-ttu-id="a0359-151">Stan Powodzenie będzie oznaczał, że zadanie zostało zakończone pomyślnie dla wszystkich baz danych dzierżaw i dwóch dodatkowych baz danych zawierających tabelę referencyjną.</span><span class="sxs-lookup"><span data-stu-id="a0359-151">Once, Succeeded, the job has successfully finished on all tenant databases and the two additional databases containing the reference table.</span></span>

<span data-ttu-id="a0359-152">Pomyślne uruchomienie skryptu powinno zwrócić wyniki podobne do następujących:</span><span class="sxs-lookup"><span data-stu-id="a0359-152">Successfully running the script should result in similar results:</span></span>

![wyniki](media/sql-database-saas-tutorial-tenant-analytics/ticket-purchases-job.png)

## <a name="create-a-job-to-retrieve-a-summary-count-of-ticket-purchases-from-all-tenants"></a><span data-ttu-id="a0359-154">Tworzenie zadania pobierania łącznej liczby zakupów biletów we wszystkich dzierżawach</span><span class="sxs-lookup"><span data-stu-id="a0359-154">Create a job to retrieve a summary count of ticket purchases from all tenants</span></span>

<span data-ttu-id="a0359-155">Ten skrypt tworzy zadanie pobierania informacji o sumie wszystkich zakupów biletów ze wszystkich dzierżaw.</span><span class="sxs-lookup"><span data-stu-id="a0359-155">This script creates a job to retrieve sum of all ticket purchases from all tenants.</span></span>

1. <span data-ttu-id="a0359-156">Otwórz aplikację SSMS i połącz się z serwerem *catalog-&lt;Użytkownik&gt;.database.windows.net*</span><span class="sxs-lookup"><span data-stu-id="a0359-156">Open SSMS and connect to the *catalog-&lt;User&gt;.database.windows.net* server</span></span>
1. <span data-ttu-id="a0359-157">Otwórz plik …\\Learning Modules\\Provision and Catalog\\Operational Analytics\\Tenant Analytics\\*Results-TicketPurchasesfromAllTenants.sql*</span><span class="sxs-lookup"><span data-stu-id="a0359-157">Open the file …\\Learning Modules\\Provision and Catalog\\Operational Analytics\\Tenant Analytics\\*Results-TicketPurchasesfromAllTenants.sql*</span></span>
1. <span data-ttu-id="a0359-158">Modyfikowanie &lt;użytkownika&gt;, należy użyć nazwy użytkownika używane w przypadku wdrażania aplikacji Wingtip SaaS w skrypcie w **sp\_dodać\_etap zadania** procedury składowanej</span><span class="sxs-lookup"><span data-stu-id="a0359-158">Modify &lt;User&gt;, use the user name used when you deployed the Wingtip SaaS app in the script, in the **sp\_add\_jobstep** stored procedure</span></span>
1. <span data-ttu-id="a0359-159">Kliknij prawym przyciskiem myszy, wybierz **połączenia**i połącz się katalogu -&lt;użytkownika&gt;. database.windows.net serwera, jeśli nie został jeszcze połączony</span><span class="sxs-lookup"><span data-stu-id="a0359-159">Right click, select **Connection**, and connect to the catalog-&lt;User&gt;.database.windows.net server, if not already connected</span></span>
1. <span data-ttu-id="a0359-160">Upewnij się, że masz połączenie z bazą danych **tenantanalytics**, a następnie naciśnij klawisz **F5**, aby uruchomić skrypt</span><span class="sxs-lookup"><span data-stu-id="a0359-160">Ensure you are connected to the **tenantanalytics** database and press **F5** to run the script</span></span>

<span data-ttu-id="a0359-161">Pomyślne uruchomienie skryptu powinno zwrócić wyniki podobne do następujących:</span><span class="sxs-lookup"><span data-stu-id="a0359-161">Successfully running the script should result in similar results:</span></span>

![wyniki](media/sql-database-saas-tutorial-tenant-analytics/total-sales.png)



* <span data-ttu-id="a0359-163">**sp\_add\_job** tworzy nowe cotygodniowe zaplanowane zadanie o nazwie „ResultsTicketsOrders”</span><span class="sxs-lookup"><span data-stu-id="a0359-163">**sp\_add\_job** creates a new weekly scheduled job called “ResultsTicketsOrders”</span></span>

* <span data-ttu-id="a0359-164">**sp\_add\_jobstep** tworzy krok zadania zawierający tekst polecenia T-SQL służącego do pobierania wszystkich informacji o zakupach biletów ze wszystkich dzierżaw i kopiowania zestawu zwracanych wyników do tabeli o nazwie CountofTicketOrders</span><span class="sxs-lookup"><span data-stu-id="a0359-164">**sp\_add\_jobstep** creates the job step containing T-SQL command text to retrieve all the ticket purchase information from all tenants and copy the returning result set into a table called CountofTicketOrders</span></span>

* <span data-ttu-id="a0359-165">Pozostałe widoki w skrypcie dotyczą istnienia obiektów i monitorowania wykonania zadań.</span><span class="sxs-lookup"><span data-stu-id="a0359-165">The remaining views in the script display the existence of the objects and monitor job execution.</span></span> <span data-ttu-id="a0359-166">Sprawdź wartość stanu w kolumnie **lifecycle**, aby monitorować stan.</span><span class="sxs-lookup"><span data-stu-id="a0359-166">Review the status value from the **lifecycle** column to monitor the status.</span></span> <span data-ttu-id="a0359-167">Stan Powodzenie będzie oznaczał, że zadanie zostało zakończone pomyślnie dla wszystkich baz danych dzierżaw i dwóch dodatkowych baz danych zawierających tabelę referencyjną.</span><span class="sxs-lookup"><span data-stu-id="a0359-167">Once, Succeeded, the job has successfully finished on all tenant databases and the two additional databases containing the reference table.</span></span>


## <a name="next-steps"></a><span data-ttu-id="a0359-168">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="a0359-168">Next steps</span></span>

<span data-ttu-id="a0359-169">W tym samouczku zawarto informacje na temat wykonywania następujących czynności:</span><span class="sxs-lookup"><span data-stu-id="a0359-169">In this tutorial you learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="a0359-170">Wdrażanie analitycznej bazy danych dzierżaw</span><span class="sxs-lookup"><span data-stu-id="a0359-170">Deploy a tenant analytics database</span></span>
> * <span data-ttu-id="a0359-171">Tworzenie zaplanowanego zadania do pobierania danych analitycznych z dzierżaw</span><span class="sxs-lookup"><span data-stu-id="a0359-171">Create a scheduled job to retrieve analytical data across tenants</span></span>

<span data-ttu-id="a0359-172">Gratulacje!</span><span class="sxs-lookup"><span data-stu-id="a0359-172">Congratulations!</span></span>

## <a name="additional-resources"></a><span data-ttu-id="a0359-173">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="a0359-173">Additional resources</span></span>

* <span data-ttu-id="a0359-174">Dodatkowe [samouczków, z którymi aplikacji Wingtip SaaS](sql-database-wtp-overview.md#sql-database-wingtip-saas-tutorials)</span><span class="sxs-lookup"><span data-stu-id="a0359-174">Additional [tutorials that build upon the Wingtip SaaS application](sql-database-wtp-overview.md#sql-database-wingtip-saas-tutorials)</span></span>
* [<span data-ttu-id="a0359-175">Zadania elastyczne</span><span class="sxs-lookup"><span data-stu-id="a0359-175">Elastic Jobs</span></span>](sql-database-elastic-jobs-overview.md)
