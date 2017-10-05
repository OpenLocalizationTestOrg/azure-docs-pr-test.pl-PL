---
title: Wprowadzenie do synchronizacji danych SQL Azure (wersja zapoznawcza) | Dokumentacja firmy Microsoft
description: "Ten samouczek ułatwia szybkie wprowadzenie do synchronizacji danych SQL Azure (wersja zapoznawcza)."
services: sql-database
documentationcenter: 
author: douglaslms
manager: craigg
editor: 
ms.assetid: a295a768-7ff2-4a86-a253-0090281c8efa
ms.service: sql-database
ms.custom: load & move data
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/08/2017
ms.author: douglasl
ms.openlocfilehash: 2d0f9d7f32ad79f49d58165d734b9df4af862835
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/18/2017
---
# <a name="getting-started-with-azure-sql-data-sync-preview"></a><span data-ttu-id="dbaef-103">Wprowadzenie do synchronizacji danych Azure SQL (wersja zapoznawcza)</span><span class="sxs-lookup"><span data-stu-id="dbaef-103">Getting Started with Azure SQL Data Sync (Preview)</span></span>
<span data-ttu-id="dbaef-104">Z tego samouczka dowiesz się sposobu konfigurowania synchronizacji danych SQL Azure, tworząc grupy synchronizacji hybrydowych, zawierającej wystąpienia zarówno usługi Azure SQL Database i programu SQL Server.</span><span class="sxs-lookup"><span data-stu-id="dbaef-104">In this tutorial, you learn how to set up Azure SQL Data Sync by creating a hybrid sync group that contains both Azure SQL Database and SQL Server instances.</span></span> <span data-ttu-id="dbaef-105">Nowa grupa synchronizacji jest w pełni skonfigurowane i synchronizuje się zgodnie z harmonogramem, które można ustawić.</span><span class="sxs-lookup"><span data-stu-id="dbaef-105">The new sync group is fully configured and synchronizes on the schedule you set.</span></span>

<span data-ttu-id="dbaef-106">W tym samouczku założono, że co najmniej pewne doświadczenie z bazy danych SQL i programu SQL Server.</span><span class="sxs-lookup"><span data-stu-id="dbaef-106">This tutorial assumes that you have at least some prior experience with SQL Database and with SQL Server.</span></span> 

<span data-ttu-id="dbaef-107">Omówienie synchronizacji danych SQL, zobacz [synchronizowanie danych](sql-database-sync-data.md).</span><span class="sxs-lookup"><span data-stu-id="dbaef-107">For an overview of SQL Data Sync, see [Sync data](sql-database-sync-data.md).</span></span>

<span data-ttu-id="dbaef-108">Aby uzyskać pełną przykładów programu PowerShell, które przedstawiają sposób konfigurowania synchronizacji danych SQL, zobacz następujące artykuły:</span><span class="sxs-lookup"><span data-stu-id="dbaef-108">For complete PowerShell examples that show how to configure SQL Data Sync, see the following articles:</span></span>
-   [<span data-ttu-id="dbaef-109">Synchronizacja między wiele baz danych Azure SQL przy użyciu programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="dbaef-109">Use PowerShell to sync between multiple Azure SQL databases</span></span>](scripts/sql-database-sync-data-between-sql-databases.md)
-   [<span data-ttu-id="dbaef-110">Synchronizacja między bazą danych SQL Azure i lokalnej bazy danych programu SQL Server przy użyciu programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="dbaef-110">Use PowerShell to sync between an Azure SQL Database and a SQL Server on-premises database</span></span>](scripts/sql-database-sync-data-between-azure-onprem.md)

> [!NOTE]
> <span data-ttu-id="dbaef-111">Pełną dokumentację techniczną dla synchronizacji danych SQL Azure, wcześniej znajdowały się w witrynie MSDN, jest dostępna jako. Dokument PDF.</span><span class="sxs-lookup"><span data-stu-id="dbaef-111">The complete technical documentation set for Azure SQL Data Sync, formerly located on MSDN, is available as a .PDF document.</span></span> <span data-ttu-id="dbaef-112">Pobierz go [tutaj](https://github.com/Microsoft/sql-server-samples/raw/master/samples/features/sql-data-sync/Data_Sync_Preview_full_documentation.pdf?raw=true).</span><span class="sxs-lookup"><span data-stu-id="dbaef-112">Download it [here](https://github.com/Microsoft/sql-server-samples/raw/master/samples/features/sql-data-sync/Data_Sync_Preview_full_documentation.pdf?raw=true).</span></span>

## <a name="step-1---create-sync-group"></a><span data-ttu-id="dbaef-113">Krok 1 — Tworzenie grupy synchronizacji</span><span class="sxs-lookup"><span data-stu-id="dbaef-113">Step 1 - Create sync group</span></span>

### <a name="locate-the-data-sync-settings"></a><span data-ttu-id="dbaef-114">Zlokalizuj ustawienia synchronizacji danych</span><span class="sxs-lookup"><span data-stu-id="dbaef-114">Locate the Data Sync settings</span></span>

1.  <span data-ttu-id="dbaef-115">W przeglądarce przejdź do portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="dbaef-115">In your browser, navigate to the Azure portal.</span></span>

2.  <span data-ttu-id="dbaef-116">W portalu Znajdź bazy danych SQL z pulpitu nawigacyjnego lub ikonę baz danych na pasku narzędzi.</span><span class="sxs-lookup"><span data-stu-id="dbaef-116">In the portal, locate your SQL databases from your Dashboard or from the SQL Databases icon on the toolbar.</span></span>

    ![Lista baz danych Azure SQL](media/sql-database-get-started-sql-data-sync/datasync-preview-sqldbs.png)

3.  <span data-ttu-id="dbaef-118">Na **baz danych SQL** bloku, wybierz istniejącej bazy danych SQL, który ma być używany jako baza danych Centrum synchronizacji danych. Zostanie otwarty blok bazy danych SQL.</span><span class="sxs-lookup"><span data-stu-id="dbaef-118">On the **SQL databases** blade, select the existing SQL database that you want to use as the hub database for Data Sync. The SQL database blade opens.</span></span>

4.  <span data-ttu-id="dbaef-119">W bloku bazy danych SQL dla wybranej bazy danych, wybierz **synchronizacji do innych baz danych**.</span><span class="sxs-lookup"><span data-stu-id="dbaef-119">On the SQL database blade for the selected database, select **Sync to other databases**.</span></span> <span data-ttu-id="dbaef-120">Zostanie otwarty blok synchronizacji danych.</span><span class="sxs-lookup"><span data-stu-id="dbaef-120">The Data Sync blade opens.</span></span>

    ![Synchronizowanie innych opcji bazy danych](media/sql-database-get-started-sql-data-sync/datasync-preview-newsyncgroup.png)

### <a name="create-a-new-sync-group"></a><span data-ttu-id="dbaef-122">Utwórz nową grupę synchronizacji</span><span class="sxs-lookup"><span data-stu-id="dbaef-122">Create a new Sync Group</span></span>

1.  <span data-ttu-id="dbaef-123">W bloku danych synchronizacji wybierz **nowej grupy synchronizacji**.</span><span class="sxs-lookup"><span data-stu-id="dbaef-123">On the Data Sync blade, select **New Sync Group**.</span></span> <span data-ttu-id="dbaef-124">**Nowej grupy synchronizacji** z kroku 1, zostanie otwarty blok **Utwórz grupę synchronizacji**, zaznaczony.</span><span class="sxs-lookup"><span data-stu-id="dbaef-124">The **New sync group** blade opens with Step 1, **Create sync group**, highlighted.</span></span> <span data-ttu-id="dbaef-125">**Tworzenie grupy synchronizacji danych** również zostanie otwarty blok.</span><span class="sxs-lookup"><span data-stu-id="dbaef-125">The **Create Data Sync Group** blade also opens.</span></span>

2.  <span data-ttu-id="dbaef-126">Na **Tworzenie grupy synchronizacji danych** blok, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="dbaef-126">On the **Create Data Sync Group** blade, do the following things:</span></span>

    1.  <span data-ttu-id="dbaef-127">W **nazwy grupy synchronizacji** wprowadź nazwę nowej grupy synchronizacji.</span><span class="sxs-lookup"><span data-stu-id="dbaef-127">In the **Sync Group Name** field, enter a name for the new sync group.</span></span>

    2.  <span data-ttu-id="dbaef-128">W **bazy danych usługi synchronizacji metadanych** sekcji wybierz, czy można utworzyć nową bazę danych (zalecane) lub użyj istniejącej bazy danych.</span><span class="sxs-lookup"><span data-stu-id="dbaef-128">In the **Sync Metadata Database** section, choose whether to create a new database (recommended) or to use an existing database.</span></span>

        > [!NOTE]
        > <span data-ttu-id="dbaef-129">Firma Microsoft zaleca, aby utworzyć nową, pustą bazę danych do użycia jako bazy danych usługi synchronizacji metadanych.</span><span class="sxs-lookup"><span data-stu-id="dbaef-129">Microsoft recommends that you create a new, empty database to use as the Sync Metadata Database.</span></span> <span data-ttu-id="dbaef-130">Synchronizacja danych tworzy tabele w tej bazie danych i uruchamia częste obciążenia.</span><span class="sxs-lookup"><span data-stu-id="dbaef-130">Data Sync creates tables in this database and runs a frequent workload.</span></span> <span data-ttu-id="dbaef-131">Ta baza danych jest automatycznie udostępniony jako bazy danych usługi synchronizacji metadanych dla wszystkich grup synchronizacji w wybranym regionie.</span><span class="sxs-lookup"><span data-stu-id="dbaef-131">This database is automatically shared as the Sync Metadata Database for all of your Sync groups in the selected region.</span></span> <span data-ttu-id="dbaef-132">Nie można zmienić metadanych bazy danych usługi synchronizacji, jego nazwa lub jego poziom usługi bez porzuceniem jej.</span><span class="sxs-lookup"><span data-stu-id="dbaef-132">You can't change the Sync Metadata Database, its name, or its service level without dropping it.</span></span>

        <span data-ttu-id="dbaef-133">Jeśli została wybrana opcja **nową bazę danych**, wybierz pozycję **Utwórz nową bazę danych.**</span><span class="sxs-lookup"><span data-stu-id="dbaef-133">If you chose **New database**, select **Create new database.**</span></span> <span data-ttu-id="dbaef-134">**Bazy danych SQL** zostanie otwarty blok.</span><span class="sxs-lookup"><span data-stu-id="dbaef-134">The **SQL Database** blade opens.</span></span> <span data-ttu-id="dbaef-135">Na **bazy danych SQL** bloku, nazwy i skonfiguruj nową bazę danych.</span><span class="sxs-lookup"><span data-stu-id="dbaef-135">On the **SQL Database** blade, name and configure the new database.</span></span> <span data-ttu-id="dbaef-136">Następnie wybierz **OK**.</span><span class="sxs-lookup"><span data-stu-id="dbaef-136">Then select **OK**.</span></span>

        <span data-ttu-id="dbaef-137">Jeśli została wybrana opcja **Użyj istniejącej bazy danych**, wybierz bazę danych z listy.</span><span class="sxs-lookup"><span data-stu-id="dbaef-137">If you chose **Use existing database**, select the database from the list.</span></span>

    3.  <span data-ttu-id="dbaef-138">W **synchronizacji automatycznej** najpierw wybierz **na** lub **poza**.</span><span class="sxs-lookup"><span data-stu-id="dbaef-138">In the **Automatic Sync** section, first select **On** or **Off**.</span></span>

        <span data-ttu-id="dbaef-139">Jeśli została wybrana opcja **na**w **częstotliwości synchronizacji** , wprowadź liczbę z zakresu a następnie wybierz opcję sekundy, minuty, godziny lub dni.</span><span class="sxs-lookup"><span data-stu-id="dbaef-139">If you chose **On**, in the **Sync Frequency** section, enter a number and select Seconds, Minutes, Hours, or Days.</span></span>

        ![Określ częstotliwość synchronizacji](media/sql-database-get-started-sql-data-sync/datasync-preview-syncfreq.png)

    4.  <span data-ttu-id="dbaef-141">W **rozwiązywania konfliktów** wybierz "Centrum wins" lub "Elementu członkowskiego wins".</span><span class="sxs-lookup"><span data-stu-id="dbaef-141">In the **Conflict Resolution** section, select "Hub wins" or "Member wins."</span></span>

        ![Określ, jak są rozwiązywane konflikty](media/sql-database-get-started-sql-data-sync/datasync-preview-conflictres.png)

    5.  <span data-ttu-id="dbaef-143">Wybierz **OK** i poczekaj, aż nową grupę synchronizacji, aby utworzyć i wdrożyć.</span><span class="sxs-lookup"><span data-stu-id="dbaef-143">Select **OK** and wait for the new sync group to be created and deployed.</span></span>

## <a name="step-2---add-sync-members"></a><span data-ttu-id="dbaef-144">Krok 2 — Dodawanie członków synchronizacji</span><span class="sxs-lookup"><span data-stu-id="dbaef-144">Step 2 - Add sync members</span></span>

<span data-ttu-id="dbaef-145">Po utworzeniu i wdrożeniu, krok 2 nowej grupy synchronizacji **dodawać członków synchronizacji**, zostanie wyróżniona w **nowej grupy synchronizacji** bloku.</span><span class="sxs-lookup"><span data-stu-id="dbaef-145">After the new sync group is created and deployed, Step 2, **Add sync members**, is highlighted in the **New sync group** blade.</span></span>

<span data-ttu-id="dbaef-146">W **bazy danych Centrum** wprowadź istniejących poświadczeń dla serwera bazy danych SQL, na którym znajduje się baza danych Centrum.</span><span class="sxs-lookup"><span data-stu-id="dbaef-146">In the **Hub Database** section, enter the existing credentials for the SQL Database server on which the hub database is located.</span></span> <span data-ttu-id="dbaef-147">Nie wprowadzaj *nowe* poświadczeń w tej sekcji.</span><span class="sxs-lookup"><span data-stu-id="dbaef-147">Don't enter *new* credentials in this section.</span></span>

![Koncentrator bazy danych został dodany do grupy synchronizacji](media/sql-database-get-started-sql-data-sync/datasync-preview-hubadded.png)

## <a name="add-an-azure-sql-database"></a><span data-ttu-id="dbaef-149">Dodaj bazę danych Azure SQL</span><span class="sxs-lookup"><span data-stu-id="dbaef-149">Add an Azure SQL Database</span></span>

<span data-ttu-id="dbaef-150">W **bazy danych elementów członkowskich** sekcji i opcjonalnie Dodaj do grupy synchronizacji bazy danych SQL Azure, wybierając **dodać bazy danych Azure**.</span><span class="sxs-lookup"><span data-stu-id="dbaef-150">In the **Member Database** section, optionally add an Azure SQL Database to the sync group by selecting **Add an Azure Database**.</span></span> <span data-ttu-id="dbaef-151">**Konfigurowanie bazy danych Azure** zostanie otwarty blok.</span><span class="sxs-lookup"><span data-stu-id="dbaef-151">The **Configure Azure Database** blade opens.</span></span>

<span data-ttu-id="dbaef-152">Na **Konfigurowanie bazy danych Azure** blok, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="dbaef-152">On the **Configure Azure Database** blade, do the following things:</span></span>

1.  <span data-ttu-id="dbaef-153">W **nazwa elementu członkowskiego synchronizacji** Podaj nazwę nowego elementu synchronizacji.</span><span class="sxs-lookup"><span data-stu-id="dbaef-153">In the **Sync Member Name** field, provide a name for the new sync member.</span></span> <span data-ttu-id="dbaef-154">Ta nazwa różni się od nazwy bazy danych.</span><span class="sxs-lookup"><span data-stu-id="dbaef-154">This name is distinct from the name of the database itself.</span></span>

2.  <span data-ttu-id="dbaef-155">W **subskrypcji** wybierz skojarzona subskrypcja platformy Azure na potrzeby rozliczeń.</span><span class="sxs-lookup"><span data-stu-id="dbaef-155">In the **Subscription** field, select the associated Azure subscription for billing purposes.</span></span>

3.  <span data-ttu-id="dbaef-156">W **Azure SQL Server** wybierz istniejącego serwera baz danych SQL.</span><span class="sxs-lookup"><span data-stu-id="dbaef-156">In the **Azure SQL Server** field, select the existing SQL database server.</span></span>

4.  <span data-ttu-id="dbaef-157">W **bazy danych SQL Azure** wybierz istniejącą bazę danych SQL.</span><span class="sxs-lookup"><span data-stu-id="dbaef-157">In the **Azure SQL Database** field, select the existing SQL database.</span></span>

5.  <span data-ttu-id="dbaef-158">W **kierunki synchronizacji** pola, wybierz opcję synchronizacji dwukierunkowe, do koncentratora lub z Centrum.</span><span class="sxs-lookup"><span data-stu-id="dbaef-158">In the **Sync Directions** field, select Bi-directional Sync, To the Hub, or From the Hub.</span></span>

    ![Dodawanie nowego elementu członkowskiego synchronizacji bazy danych SQL](media/sql-database-get-started-sql-data-sync/datasync-preview-memberadding.png)

6.  <span data-ttu-id="dbaef-160">W **Username** i **hasło** wprowadź istniejących poświadczeń dla serwera bazy danych SQL, na którym znajduje się bazy danych elementów członkowskich.</span><span class="sxs-lookup"><span data-stu-id="dbaef-160">In the **Username** and **Password** fields, enter the existing credentials for the SQL Database server on which the member database is located.</span></span> <span data-ttu-id="dbaef-161">Nie wprowadzaj *nowe* poświadczeń w tej sekcji.</span><span class="sxs-lookup"><span data-stu-id="dbaef-161">Don't enter *new* credentials in this section.</span></span>

7.  <span data-ttu-id="dbaef-162">Wybierz **OK** i poczekaj, aż nowy element członkowski synchronizacji utworzyć i wdrożyć.</span><span class="sxs-lookup"><span data-stu-id="dbaef-162">Select **OK** and wait for the new sync member to be created and deployed.</span></span>

    ![Dodano nowy element członkowski synchronizacji bazy danych SQL](media/sql-database-get-started-sql-data-sync/datasync-preview-memberadded.png)

## <a name="add-an-on-premises-sql-server-database"></a><span data-ttu-id="dbaef-164">Dodaj lokalną bazą danych programu SQL Server</span><span class="sxs-lookup"><span data-stu-id="dbaef-164">Add an on-premises SQL Server database</span></span>

<span data-ttu-id="dbaef-165">W **bazy danych elementów członkowskich** sekcji i opcjonalnie Dodaj lokalny serwer SQL do grupy synchronizacji, wybierając **Dodaj bazę danych z lokalnego**.</span><span class="sxs-lookup"><span data-stu-id="dbaef-165">In the **Member Database** section, optionally add an on-premises SQL Server to the sync group by selecting **Add an On-Premises Database**.</span></span> <span data-ttu-id="dbaef-166">**Konfigurowanie lokalnego** zostanie otwarty blok.</span><span class="sxs-lookup"><span data-stu-id="dbaef-166">The **Configure On-Premises** blade opens.</span></span>

<span data-ttu-id="dbaef-167">Na **Konfigurowanie lokalnego** blok, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="dbaef-167">On the **Configure On-Premises** blade, do the following things:</span></span>

1.  <span data-ttu-id="dbaef-168">Wybierz **wybierz bramę Agent synchronizacji**.</span><span class="sxs-lookup"><span data-stu-id="dbaef-168">Select **Choose the Sync Agent Gateway**.</span></span> <span data-ttu-id="dbaef-169">**Agent synchronizacji wybierz** zostanie otwarty blok.</span><span class="sxs-lookup"><span data-stu-id="dbaef-169">The **Select Sync Agent** blade opens.</span></span>

    ![Wybierz bramę agent synchronizacji](media/sql-database-get-started-sql-data-sync/datasync-preview-choosegateway.png)

2.  <span data-ttu-id="dbaef-171">Na **wybierz bramę Agent synchronizacji** bloku, wybierz, czy chcesz użyć istniejącego agenta lub Utwórz nowy agent.</span><span class="sxs-lookup"><span data-stu-id="dbaef-171">On the **Choose the Sync Agent Gateway** blade, choose whether to use an existing agent or create a new agent.</span></span>

    <span data-ttu-id="dbaef-172">Jeśli została wybrana opcja **agentów istniejące**, wybierz z listy istniejącego agenta.</span><span class="sxs-lookup"><span data-stu-id="dbaef-172">If you chose **Existing agents**, select the existing agent from the list.</span></span>

    <span data-ttu-id="dbaef-173">Jeśli została wybrana opcja **Utwórz nowy agent**, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="dbaef-173">If you chose **Create a new agent**, do the following things:</span></span>

    1.  <span data-ttu-id="dbaef-174">Pobierz oprogramowanie klienckie synchronizacji agenta z linku podanego i zainstaluj go na komputerze, na którym znajduje się serwer SQL.</span><span class="sxs-lookup"><span data-stu-id="dbaef-174">Download the client sync agent software from the link provided and install it on the computer where the SQL Server is located.</span></span>
 
        > [!IMPORTANT]
        > <span data-ttu-id="dbaef-175">Należy otworzyć w zaporze, aby umożliwić agenta klienta komunikacji z serwerem wychodzący port TCP 1433.</span><span class="sxs-lookup"><span data-stu-id="dbaef-175">You have to open outbound TCP port 1433 in the firewall to let the client agent communicate with the server.</span></span>


    2.  <span data-ttu-id="dbaef-176">Wprowadź nazwę dla agenta.</span><span class="sxs-lookup"><span data-stu-id="dbaef-176">Enter a name for the agent.</span></span>

    3.  <span data-ttu-id="dbaef-177">Wybierz **tworzenie i generowanie klucza**.</span><span class="sxs-lookup"><span data-stu-id="dbaef-177">Select **Create and Generate Key**.</span></span>

    4.  <span data-ttu-id="dbaef-178">Klucz agenta należy skopiować do Schowka.</span><span class="sxs-lookup"><span data-stu-id="dbaef-178">Copy the agent key to the clipboard.</span></span>
        
        ![Tworzenie nowego agenta synchronizacji](media/sql-database-get-started-sql-data-sync/datasync-preview-selectsyncagent.png)

    5.  <span data-ttu-id="dbaef-180">Wybierz **OK** zamknąć **Agent synchronizacji wybierz** bloku.</span><span class="sxs-lookup"><span data-stu-id="dbaef-180">Select **OK** to close the **Select Sync Agent** blade.</span></span>

    6.  <span data-ttu-id="dbaef-181">Na komputerze serwera SQL Znajdź i uruchom aplikację klienta synchronizacji agenta.</span><span class="sxs-lookup"><span data-stu-id="dbaef-181">On the SQL Server computer, locate and run the Client Sync Agent app.</span></span>

        ![Aplikacja kliencka agenta synchronizacji danych](media/sql-database-get-started-sql-data-sync/datasync-preview-clientagent.png)

    7.  <span data-ttu-id="dbaef-183">W aplikacji agenta synchronizacji, wybierz **przesłać klucz agenta**.</span><span class="sxs-lookup"><span data-stu-id="dbaef-183">In the sync agent app, select **Submit Agent Key**.</span></span> <span data-ttu-id="dbaef-184">**Synchronizacji metadanych bazy danych konfiguracji** zostanie otwarte okno dialogowe.</span><span class="sxs-lookup"><span data-stu-id="dbaef-184">The **Sync Metadata Database Configuration** dialog box opens.</span></span>

    8.  <span data-ttu-id="dbaef-185">W **synchronizacji metadanych bazy danych konfiguracji** okno dialogowe, Wklej klucz agenta skopiowany z portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="dbaef-185">In the **Sync Metadata Database Configuration** dialog box, paste in the agent key copied from the Azure portal.</span></span> <span data-ttu-id="dbaef-186">Udostępniają istniejących poświadczeń dla serwera bazy danych SQL Azure, na którym znajduje się baza danych metadanych.</span><span class="sxs-lookup"><span data-stu-id="dbaef-186">Also provide the existing credentials for the Azure SQL Database server on which the metadata database is located.</span></span> <span data-ttu-id="dbaef-187">(Jeśli została utworzona nowa baza danych metadanych, ta baza danych jest na tym samym serwerze co baza danych Centrum). Wybierz **OK** i poczekaj, aż do zakończenia konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="dbaef-187">(If you created a new metadata database, this database is on the same server as the hub database.) Select **OK** and wait for the configuration to finish.</span></span>

        ![Wprowadź poświadczenia agenta klucza i serwera](media/sql-database-get-started-sql-data-sync/datasync-preview-agent-enterkey.png)

        >   [!NOTE] 
        >   <span data-ttu-id="dbaef-189">Jeśli w tym momencie zostanie wyświetlony błąd zapory, należy utworzyć regułę zapory na platformie Azure, aby zezwolić na ruch przychodzący z komputera programu SQL Server.</span><span class="sxs-lookup"><span data-stu-id="dbaef-189">If you get a firewall error at this point, you have to create a firewall rule on Azure to allow incoming traffic from the SQL Server computer.</span></span> <span data-ttu-id="dbaef-190">Regułę można utworzyć ręcznie w portalu, ale użytkownik może ułatwić ją utworzyć w programu SQL Server Management Studio (SSMS).</span><span class="sxs-lookup"><span data-stu-id="dbaef-190">You can create the rule manually in the portal, but you may find it easier to create it in SQL Server Management Studio (SSMS).</span></span> <span data-ttu-id="dbaef-191">W programie SSMS próby nawiązania połączenia z bazą danych Centrum na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="dbaef-191">In SSMS, try to connect to the hub database on Azure.</span></span> <span data-ttu-id="dbaef-192">Wpisz jej nazwę jako \<hub_database_name\>. database.windows.net.</span><span class="sxs-lookup"><span data-stu-id="dbaef-192">Enter its name as \<hub_database_name\>.database.windows.net.</span></span> <span data-ttu-id="dbaef-193">Wykonaj kroki opisane w oknie dialogowym, aby skonfigurować regułę zapory platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="dbaef-193">Follow the steps in the dialog box to configure the Azure firewall rule.</span></span> <span data-ttu-id="dbaef-194">Następnie wróć do aplikacji agenta klienta synchronizacji.</span><span class="sxs-lookup"><span data-stu-id="dbaef-194">Then return to the Client Sync Agent app.</span></span>

    9.  <span data-ttu-id="dbaef-195">W aplikacji klienta synchronizacji agenta, kliknij przycisk **zarejestrować** zarejestrować bazy danych programu SQL Server z agentem.</span><span class="sxs-lookup"><span data-stu-id="dbaef-195">In the Client Sync Agent app, click **Register** to register a SQL Server database with the agent.</span></span> <span data-ttu-id="dbaef-196">**Konfiguracji serwera SQL** zostanie otwarte okno dialogowe.</span><span class="sxs-lookup"><span data-stu-id="dbaef-196">The **SQL Server Configuration** dialog box opens.</span></span>

        ![Dodaj i skonfiguruj bazę danych programu SQL Server](media/sql-database-get-started-sql-data-sync/datasync-preview-agent-adddb.png)

    10. <span data-ttu-id="dbaef-198">W **konfiguracji serwera SQL** oknie dialogowym Wybierz, czy nawiązać połączenie przy użyciu uwierzytelniania programu SQL Server lub uwierzytelniania systemu Windows.</span><span class="sxs-lookup"><span data-stu-id="dbaef-198">In the **SQL Server Configuration** dialog box, choose whether to connect by using SQL Server authentication or Windows authentication.</span></span> <span data-ttu-id="dbaef-199">Jeśli wybrano opcję uwierzytelniania programu SQL Server, wprowadź istniejących poświadczeń.</span><span class="sxs-lookup"><span data-stu-id="dbaef-199">If you chose SQL Server authentication, enter the existing credentials.</span></span> <span data-ttu-id="dbaef-200">Podaj nazwę serwera SQL i nazwę bazy danych, które mają być synchronizowane. Wybierz **połączenie testowe** Aby przetestować ustawienia.</span><span class="sxs-lookup"><span data-stu-id="dbaef-200">Provide the SQL Server name and the name of the database that you want to sync. Select **Test connection** to test your settings.</span></span> <span data-ttu-id="dbaef-201">Następnie wybierz **zapisać**.</span><span class="sxs-lookup"><span data-stu-id="dbaef-201">Then select **Save**.</span></span> <span data-ttu-id="dbaef-202">Zarejestrowane bazy danych zostanie wyświetlony na liście.</span><span class="sxs-lookup"><span data-stu-id="dbaef-202">The registered database appears in the list.</span></span>

        ![Baza danych SQL Server zostanie zarejestrowany](media/sql-database-get-started-sql-data-sync/datasync-preview-agent-dbadded.png)

    11. <span data-ttu-id="dbaef-204">Można teraz zamknąć aplikacji agenta klienta synchronizacji.</span><span class="sxs-lookup"><span data-stu-id="dbaef-204">You can now close the Client Sync Agent app.</span></span>

    12. <span data-ttu-id="dbaef-205">W portalu na **Konfigurowanie lokalnego** bloku, wybierz opcję **wybierz bazę danych.**</span><span class="sxs-lookup"><span data-stu-id="dbaef-205">In the portal, on the **Configure On-Premises** blade, select **Select the Database.**</span></span> <span data-ttu-id="dbaef-206">**Wybierz bazę danych** zostanie otwarty blok.</span><span class="sxs-lookup"><span data-stu-id="dbaef-206">The **Select Database** blade opens.</span></span>

    13. <span data-ttu-id="dbaef-207">Na **wybierz bazę danych** bloku, w **nazwa elementu członkowskiego synchronizacji** Podaj nazwę nowego elementu synchronizacji.</span><span class="sxs-lookup"><span data-stu-id="dbaef-207">On the **Select Database** blade, in the **Sync Member Name** field, provide a name for the new sync member.</span></span> <span data-ttu-id="dbaef-208">Ta nazwa różni się od nazwy bazy danych.</span><span class="sxs-lookup"><span data-stu-id="dbaef-208">This name is distinct from the name of the database itself.</span></span> <span data-ttu-id="dbaef-209">Wybierz bazę danych z listy.</span><span class="sxs-lookup"><span data-stu-id="dbaef-209">Select the database from the list.</span></span> <span data-ttu-id="dbaef-210">W **kierunki synchronizacji** pola, wybierz opcję synchronizacji dwukierunkowe, do koncentratora lub z Centrum.</span><span class="sxs-lookup"><span data-stu-id="dbaef-210">In the **Sync Directions** field, select Bi-directional Sync, To the Hub, or From the Hub.</span></span>

        ![Wybierz bazę danych na lokalnym](media/sql-database-get-started-sql-data-sync/datasync-preview-selectdb.png)

    14. <span data-ttu-id="dbaef-212">Wybierz **OK** zamknąć **wybierz bazę danych** bloku.</span><span class="sxs-lookup"><span data-stu-id="dbaef-212">Select **OK** to close the **Select Database** blade.</span></span> <span data-ttu-id="dbaef-213">Następnie wybierz **OK** zamknąć **Konfigurowanie lokalnego** bloku i oczekiwania dla nowego elementu synchronizacji, aby utworzyć i wdrożyć.</span><span class="sxs-lookup"><span data-stu-id="dbaef-213">Then select **OK** to close the **Configure On-Premises** blade and wait for the new sync member to be created and deployed.</span></span> <span data-ttu-id="dbaef-214">Na koniec kliknij **OK** zamknąć **Wybierz członków synchronizacji** bloku.</span><span class="sxs-lookup"><span data-stu-id="dbaef-214">Finally, click **OK** to close the **Select sync members** blade.</span></span>

        ![W lokalnej bazie danych dodane do grupy synchronizacji](media/sql-database-get-started-sql-data-sync/datasync-preview-onpremadded.png)

3.  <span data-ttu-id="dbaef-216">Aby połączyć się synchronizacja danych SQL i agent lokalny, Dodaj nazwę użytkownika do roli `DataSync_Executor`.</span><span class="sxs-lookup"><span data-stu-id="dbaef-216">To connect to SQL Data Sync and the local agent, add your user name to the role `DataSync_Executor`.</span></span> <span data-ttu-id="dbaef-217">Synchronizacja danych tworzy tę rolę w wystąpieniu programu SQL Server.</span><span class="sxs-lookup"><span data-stu-id="dbaef-217">Data Sync creates this role on the SQL Server instance.</span></span>

## <a name="step-3---configure-sync-group"></a><span data-ttu-id="dbaef-218">Krok 3 — Konfigurowanie synchronizacji grupy</span><span class="sxs-lookup"><span data-stu-id="dbaef-218">Step 3 - Configure sync group</span></span>

<span data-ttu-id="dbaef-219">Po nowych członków grupy synchronizacji są tworzone i wdrażane, krok 3 **Konfigurowanie synchronizacji grupy**, zostanie wyróżniona w **nowej grupy synchronizacji** bloku.</span><span class="sxs-lookup"><span data-stu-id="dbaef-219">After the new sync group members are created and deployed, Step 3, **Configure sync group**, is highlighted in the **New sync group** blade.</span></span>

1.  <span data-ttu-id="dbaef-220">Na **tabel** bloku, wybierz bazę danych z listy synchronizacji członków grupy, a następnie wybierz **schematu odświeżania**.</span><span class="sxs-lookup"><span data-stu-id="dbaef-220">On the **Tables** blade, select a database from the list of sync group members, and then select **Refresh schema**.</span></span>

2.  <span data-ttu-id="dbaef-221">Z listy dostępnych tabel wybierz tabele, które mają być synchronizowane.</span><span class="sxs-lookup"><span data-stu-id="dbaef-221">From the list of available tables, select the tables that you want to sync.</span></span>

    ![Wybierz tabele do synchronizacji](media/sql-database-get-started-sql-data-sync/datasync-preview-tables.png)

3.  <span data-ttu-id="dbaef-223">Domyślnie wybrane są wszystkie kolumny w tabeli.</span><span class="sxs-lookup"><span data-stu-id="dbaef-223">By default, all columns in the table are selected.</span></span> <span data-ttu-id="dbaef-224">Jeśli nie chcesz zsynchronizować wszystkie kolumny, wyłącz pole wyboru dla kolumn, które nie mają być synchronizowane. Pamiętaj pozostawić wybrana kolumna klucza podstawowego.</span><span class="sxs-lookup"><span data-stu-id="dbaef-224">If you don't want to sync all the columns, disable the checkbox for the columns that you don't want to sync. Be sure to leave the primary key column selected.</span></span>

    ![Wybierz pola do synchronizacji](media/sql-database-get-started-sql-data-sync/datasync-preview-tables2.png)

4.  <span data-ttu-id="dbaef-226">Na koniec wybierz **zapisać**.</span><span class="sxs-lookup"><span data-stu-id="dbaef-226">Finally, select **Save**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="dbaef-227">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="dbaef-227">Next steps</span></span>
<span data-ttu-id="dbaef-228">Gratulacje.</span><span class="sxs-lookup"><span data-stu-id="dbaef-228">Congratulations.</span></span> <span data-ttu-id="dbaef-229">Utworzono grupę synchronizacji, która zawiera zarówno wystąpienie bazy danych SQL, jak i bazy danych programu SQL Server.</span><span class="sxs-lookup"><span data-stu-id="dbaef-229">You have created a sync group that includes both a SQL Database instance and a SQL Server database.</span></span>

<span data-ttu-id="dbaef-230">Aby uzyskać więcej informacji na temat bazy danych SQL i synchronizacji danych SQL zobacz:</span><span class="sxs-lookup"><span data-stu-id="dbaef-230">For more info about SQL Database and SQL Data Sync, see:</span></span>

-   [<span data-ttu-id="dbaef-231">Pobierz pełną dokumentację techniczną synchronizacji danych SQL</span><span class="sxs-lookup"><span data-stu-id="dbaef-231">Download the complete SQL Data Sync technical documentation</span></span>](https://github.com/Microsoft/sql-server-samples/raw/master/samples/features/sql-data-sync/Data_Sync_Preview_full_documentation.pdf?raw=true)
-   [<span data-ttu-id="dbaef-232">Pobrać dokumentację interfejsu API REST synchronizacji danych SQL</span><span class="sxs-lookup"><span data-stu-id="dbaef-232">Download the SQL Data Sync REST API documentation</span></span>](https://github.com/Microsoft/sql-server-samples/raw/master/samples/features/sql-data-sync/Data_Sync_Preview_REST_API.pdf?raw=true)
-   [<span data-ttu-id="dbaef-233">Omówienie bazy danych SQL</span><span class="sxs-lookup"><span data-stu-id="dbaef-233">SQL Database Overview</span></span>](sql-database-technical-overview.md)
-   [<span data-ttu-id="dbaef-234">Zarządzanie cyklem życia bazy danych</span><span class="sxs-lookup"><span data-stu-id="dbaef-234">Database Lifecycle Management</span></span>](https://msdn.microsoft.com/library/jj907294.aspx)
