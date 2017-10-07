---
title: aaaGetting wprowadzenie do synchronizacji danych SQL Azure (wersja zapoznawcza) | Dokumentacja firmy Microsoft
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
ms.openlocfilehash: 666d09237e42acc23ae3c8c81e60734a413f5949
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="getting-started-with-azure-sql-data-sync-preview"></a><span data-ttu-id="aa1f2-103">Wprowadzenie do synchronizacji danych Azure SQL (wersja zapoznawcza)</span><span class="sxs-lookup"><span data-stu-id="aa1f2-103">Getting Started with Azure SQL Data Sync (Preview)</span></span>
<span data-ttu-id="aa1f2-104">Z tego samouczka dowiesz się, jak tooset się synchronizacja danych SQL Azure, tworząc grupy synchronizacji hybrydowych, który zawiera zarówno usługi Azure SQL Database i programu SQL Server wystąpienia.</span><span class="sxs-lookup"><span data-stu-id="aa1f2-104">In this tutorial, you learn how tooset up Azure SQL Data Sync by creating a hybrid sync group that contains both Azure SQL Database and SQL Server instances.</span></span> <span data-ttu-id="aa1f2-105">Nowa grupa synchronizacji Hello jest w pełni skonfigurowane i synchronizuje zgodnie z harmonogramem hello, które można ustawić.</span><span class="sxs-lookup"><span data-stu-id="aa1f2-105">hello new sync group is fully configured and synchronizes on hello schedule you set.</span></span>

<span data-ttu-id="aa1f2-106">W tym samouczku założono, że co najmniej pewne doświadczenie z bazy danych SQL i programu SQL Server.</span><span class="sxs-lookup"><span data-stu-id="aa1f2-106">This tutorial assumes that you have at least some prior experience with SQL Database and with SQL Server.</span></span> 

<span data-ttu-id="aa1f2-107">Omówienie synchronizacji danych SQL, zobacz [synchronizowanie danych](sql-database-sync-data.md).</span><span class="sxs-lookup"><span data-stu-id="aa1f2-107">For an overview of SQL Data Sync, see [Sync data](sql-database-sync-data.md).</span></span>

<span data-ttu-id="aa1f2-108">Aby uzyskać pełną przykłady z programu PowerShell, które zawierają tooconfigure synchronizacji danych SQL, zobacz temat hello następujące artykuły:</span><span class="sxs-lookup"><span data-stu-id="aa1f2-108">For complete PowerShell examples that show how tooconfigure SQL Data Sync, see hello following articles:</span></span>
-   [<span data-ttu-id="aa1f2-109">Użyj programu PowerShell toosync między wiele baz danych Azure SQL</span><span class="sxs-lookup"><span data-stu-id="aa1f2-109">Use PowerShell toosync between multiple Azure SQL databases</span></span>](scripts/sql-database-sync-data-between-sql-databases.md)
-   [<span data-ttu-id="aa1f2-110">Użyj programu PowerShell toosync między bazą danych SQL Azure i lokalnej bazy danych programu SQL Server</span><span class="sxs-lookup"><span data-stu-id="aa1f2-110">Use PowerShell toosync between an Azure SQL Database and a SQL Server on-premises database</span></span>](scripts/sql-database-sync-data-between-azure-onprem.md)

> [!NOTE]
> <span data-ttu-id="aa1f2-111">Hello pełną dokumentację techniczną dla synchronizacji danych SQL Azure, wcześniej znajdowały się w witrynie MSDN, jest dostępna jako. Dokument PDF.</span><span class="sxs-lookup"><span data-stu-id="aa1f2-111">hello complete technical documentation set for Azure SQL Data Sync, formerly located on MSDN, is available as a .PDF document.</span></span> <span data-ttu-id="aa1f2-112">Pobierz go [tutaj](https://github.com/Microsoft/sql-server-samples/raw/master/samples/features/sql-data-sync/Data_Sync_Preview_full_documentation.pdf?raw=true).</span><span class="sxs-lookup"><span data-stu-id="aa1f2-112">Download it [here](https://github.com/Microsoft/sql-server-samples/raw/master/samples/features/sql-data-sync/Data_Sync_Preview_full_documentation.pdf?raw=true).</span></span>

## <a name="step-1---create-sync-group"></a><span data-ttu-id="aa1f2-113">Krok 1 — Tworzenie grupy synchronizacji</span><span class="sxs-lookup"><span data-stu-id="aa1f2-113">Step 1 - Create sync group</span></span>

### <a name="locate-hello-data-sync-settings"></a><span data-ttu-id="aa1f2-114">Zlokalizuj hello ustawienia synchronizacji danych</span><span class="sxs-lookup"><span data-stu-id="aa1f2-114">Locate hello Data Sync settings</span></span>

1.  <span data-ttu-id="aa1f2-115">W przeglądarce Przejdź toohello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="aa1f2-115">In your browser, navigate toohello Azure portal.</span></span>

2.  <span data-ttu-id="aa1f2-116">W portalu hello zlokalizować bazy danych SQL z pulpitu nawigacyjnego lub ikonę bazy danych SQL hello na powitania narzędzi.</span><span class="sxs-lookup"><span data-stu-id="aa1f2-116">In hello portal, locate your SQL databases from your Dashboard or from hello SQL Databases icon on hello toolbar.</span></span>

    ![Lista baz danych Azure SQL](media/sql-database-get-started-sql-data-sync/datasync-preview-sqldbs.png)

3.  <span data-ttu-id="aa1f2-118">Na powitania **baz danych SQL** bloku, wybierz hello istniejącej bazy danych SQL, które mają toouse jako otwiera hello Centrum bazy danych synchronizacji danych. blok bazy danych SQL o hello.</span><span class="sxs-lookup"><span data-stu-id="aa1f2-118">On hello **SQL databases** blade, select hello existing SQL database that you want toouse as hello hub database for Data Sync. hello SQL database blade opens.</span></span>

4.  <span data-ttu-id="aa1f2-119">W bloku bazy danych SQL hello hello wybranej bazy danych, wybierz **synchronizować bazy danych tooother**.</span><span class="sxs-lookup"><span data-stu-id="aa1f2-119">On hello SQL database blade for hello selected database, select **Sync tooother databases**.</span></span> <span data-ttu-id="aa1f2-120">zostanie otwarty blok synchronizacji danych Hello.</span><span class="sxs-lookup"><span data-stu-id="aa1f2-120">hello Data Sync blade opens.</span></span>

    ![Opcja bazy danych tooother synchronizacji](media/sql-database-get-started-sql-data-sync/datasync-preview-newsyncgroup.png)

### <a name="create-a-new-sync-group"></a><span data-ttu-id="aa1f2-122">Utwórz nową grupę synchronizacji</span><span class="sxs-lookup"><span data-stu-id="aa1f2-122">Create a new Sync Group</span></span>

1.  <span data-ttu-id="aa1f2-123">W bloku synchronizacji danych hello, wybierz **nowej grupy synchronizacji**.</span><span class="sxs-lookup"><span data-stu-id="aa1f2-123">On hello Data Sync blade, select **New Sync Group**.</span></span> <span data-ttu-id="aa1f2-124">Witaj **nowej grupy synchronizacji** z kroku 1, zostanie otwarty blok **Utwórz grupę synchronizacji**, zaznaczony.</span><span class="sxs-lookup"><span data-stu-id="aa1f2-124">hello **New sync group** blade opens with Step 1, **Create sync group**, highlighted.</span></span> <span data-ttu-id="aa1f2-125">Witaj **Tworzenie grupy synchronizacji danych** również zostanie otwarty blok.</span><span class="sxs-lookup"><span data-stu-id="aa1f2-125">hello **Create Data Sync Group** blade also opens.</span></span>

2.  <span data-ttu-id="aa1f2-126">Na powitania **Tworzenie grupy synchronizacji danych** bloku hello następujących czynności:</span><span class="sxs-lookup"><span data-stu-id="aa1f2-126">On hello **Create Data Sync Group** blade, do hello following things:</span></span>

    1.  <span data-ttu-id="aa1f2-127">W hello **nazwy grupy synchronizacji** wprowadź nazwę nowej grupy synchronizacji hello.</span><span class="sxs-lookup"><span data-stu-id="aa1f2-127">In hello **Sync Group Name** field, enter a name for hello new sync group.</span></span>

    2.  <span data-ttu-id="aa1f2-128">W hello **bazy danych usługi synchronizacji metadanych** wybierz, czy toocreate nową bazę danych (zalecane) lub toouse istniejącej bazy danych.</span><span class="sxs-lookup"><span data-stu-id="aa1f2-128">In hello **Sync Metadata Database** section, choose whether toocreate a new database (recommended) or toouse an existing database.</span></span>

        > [!NOTE]
        > <span data-ttu-id="aa1f2-129">Firma Microsoft zaleca utworzenie toouse nową, pustą bazę danych, jak hello synchronizacji bazy danych metadanych.</span><span class="sxs-lookup"><span data-stu-id="aa1f2-129">Microsoft recommends that you create a new, empty database toouse as hello Sync Metadata Database.</span></span> <span data-ttu-id="aa1f2-130">Synchronizacja danych tworzy tabele w tej bazie danych i uruchamia częste obciążenia.</span><span class="sxs-lookup"><span data-stu-id="aa1f2-130">Data Sync creates tables in this database and runs a frequent workload.</span></span> <span data-ttu-id="aa1f2-131">Ta baza danych jest automatycznie udostępniony jako hello synchronizacji bazy danych metadanych dla wszystkich grup synchronizacji w wybranym regionie hello.</span><span class="sxs-lookup"><span data-stu-id="aa1f2-131">This database is automatically shared as hello Sync Metadata Database for all of your Sync groups in hello selected region.</span></span> <span data-ttu-id="aa1f2-132">Nie można zmienić hello bazy danych usługi synchronizacji metadanych, jego nazwa lub jego poziom usługi bez usuwania go.</span><span class="sxs-lookup"><span data-stu-id="aa1f2-132">You can't change hello Sync Metadata Database, its name, or its service level without dropping it.</span></span>

        <span data-ttu-id="aa1f2-133">Jeśli została wybrana opcja **nową bazę danych**, wybierz pozycję **Utwórz nową bazę danych.**</span><span class="sxs-lookup"><span data-stu-id="aa1f2-133">If you chose **New database**, select **Create new database.**</span></span> <span data-ttu-id="aa1f2-134">Witaj **bazy danych SQL** zostanie otwarty blok.</span><span class="sxs-lookup"><span data-stu-id="aa1f2-134">hello **SQL Database** blade opens.</span></span> <span data-ttu-id="aa1f2-135">Na powitania **bazy danych SQL** bloku, nazwy i skonfigurować hello nowej bazy danych.</span><span class="sxs-lookup"><span data-stu-id="aa1f2-135">On hello **SQL Database** blade, name and configure hello new database.</span></span> <span data-ttu-id="aa1f2-136">Następnie wybierz **OK**.</span><span class="sxs-lookup"><span data-stu-id="aa1f2-136">Then select **OK**.</span></span>

        <span data-ttu-id="aa1f2-137">Jeśli została wybrana opcja **Użyj istniejącej bazy danych**, wybierz pozycję hello bazy danych, z listy hello.</span><span class="sxs-lookup"><span data-stu-id="aa1f2-137">If you chose **Use existing database**, select hello database from hello list.</span></span>

    3.  <span data-ttu-id="aa1f2-138">W hello **synchronizacji automatycznej** najpierw wybierz **na** lub **poza**.</span><span class="sxs-lookup"><span data-stu-id="aa1f2-138">In hello **Automatic Sync** section, first select **On** or **Off**.</span></span>

        <span data-ttu-id="aa1f2-139">Jeśli została wybrana opcja **na**, w hello **częstotliwości synchronizacji** , wprowadź liczbę z zakresu a następnie wybierz opcję sekundy, minuty, godziny lub dni.</span><span class="sxs-lookup"><span data-stu-id="aa1f2-139">If you chose **On**, in hello **Sync Frequency** section, enter a number and select Seconds, Minutes, Hours, or Days.</span></span>

        ![Określ częstotliwość synchronizacji](media/sql-database-get-started-sql-data-sync/datasync-preview-syncfreq.png)

    4.  <span data-ttu-id="aa1f2-141">W hello **rozwiązywania konfliktów** wybierz "Centrum wins" lub "Elementu członkowskiego wins".</span><span class="sxs-lookup"><span data-stu-id="aa1f2-141">In hello **Conflict Resolution** section, select "Hub wins" or "Member wins."</span></span>

        ![Określ, jak są rozwiązywane konflikty](media/sql-database-get-started-sql-data-sync/datasync-preview-conflictres.png)

    5.  <span data-ttu-id="aa1f2-143">Wybierz **OK** i poczekaj, aż hello nowe synchronizacji grupy toobe utworzeniu i wdrożeniu.</span><span class="sxs-lookup"><span data-stu-id="aa1f2-143">Select **OK** and wait for hello new sync group toobe created and deployed.</span></span>

## <a name="step-2---add-sync-members"></a><span data-ttu-id="aa1f2-144">Krok 2 — Dodawanie członków synchronizacji</span><span class="sxs-lookup"><span data-stu-id="aa1f2-144">Step 2 - Add sync members</span></span>

<span data-ttu-id="aa1f2-145">Po utworzeniu i wdrożeniu, krok 2 hello nowej grupy synchronizacji **dodawać członków synchronizacji**, zostało wyróżnione hello **nowej grupy synchronizacji** bloku.</span><span class="sxs-lookup"><span data-stu-id="aa1f2-145">After hello new sync group is created and deployed, Step 2, **Add sync members**, is highlighted in hello **New sync group** blade.</span></span>

<span data-ttu-id="aa1f2-146">W hello **bazy danych Centrum** wprowadź hello istniejących poświadczeń dla hello serwera bazy danych SQL, na którym hello znajduje się baza danych Centrum.</span><span class="sxs-lookup"><span data-stu-id="aa1f2-146">In hello **Hub Database** section, enter hello existing credentials for hello SQL Database server on which hello hub database is located.</span></span> <span data-ttu-id="aa1f2-147">Nie wprowadzaj *nowe* poświadczeń w tej sekcji.</span><span class="sxs-lookup"><span data-stu-id="aa1f2-147">Don't enter *new* credentials in this section.</span></span>

![Koncentrator bazy danych został dodany toosync grupy](media/sql-database-get-started-sql-data-sync/datasync-preview-hubadded.png)

## <a name="add-an-azure-sql-database"></a><span data-ttu-id="aa1f2-149">Dodaj bazę danych Azure SQL</span><span class="sxs-lookup"><span data-stu-id="aa1f2-149">Add an Azure SQL Database</span></span>

<span data-ttu-id="aa1f2-150">W hello **bazy danych elementów członkowskich** sekcji i opcjonalnie Dodaj grupy synchronizacji toohello bazy danych SQL Azure, wybierając **dodać bazy danych Azure**.</span><span class="sxs-lookup"><span data-stu-id="aa1f2-150">In hello **Member Database** section, optionally add an Azure SQL Database toohello sync group by selecting **Add an Azure Database**.</span></span> <span data-ttu-id="aa1f2-151">Witaj **Konfigurowanie bazy danych Azure** zostanie otwarty blok.</span><span class="sxs-lookup"><span data-stu-id="aa1f2-151">hello **Configure Azure Database** blade opens.</span></span>

<span data-ttu-id="aa1f2-152">Na powitania **Konfigurowanie bazy danych Azure** bloku hello następujących czynności:</span><span class="sxs-lookup"><span data-stu-id="aa1f2-152">On hello **Configure Azure Database** blade, do hello following things:</span></span>

1.  <span data-ttu-id="aa1f2-153">W hello **nazwa elementu członkowskiego synchronizacji** Podaj nazwę nowego członka synchronizacji hello.</span><span class="sxs-lookup"><span data-stu-id="aa1f2-153">In hello **Sync Member Name** field, provide a name for hello new sync member.</span></span> <span data-ttu-id="aa1f2-154">Ta nazwa różni się od nazwy hello hello bazy danych.</span><span class="sxs-lookup"><span data-stu-id="aa1f2-154">This name is distinct from hello name of hello database itself.</span></span>

2.  <span data-ttu-id="aa1f2-155">W hello **subskrypcji** hello wybierz opcję skojarzona subskrypcja platformy Azure na potrzeby rozliczeń.</span><span class="sxs-lookup"><span data-stu-id="aa1f2-155">In hello **Subscription** field, select hello associated Azure subscription for billing purposes.</span></span>

3.  <span data-ttu-id="aa1f2-156">W hello **Azure SQL Server** hello wybierz opcję istniejącego serwera baz danych SQL.</span><span class="sxs-lookup"><span data-stu-id="aa1f2-156">In hello **Azure SQL Server** field, select hello existing SQL database server.</span></span>

4.  <span data-ttu-id="aa1f2-157">W hello **bazy danych SQL Azure** hello wybierz opcję istniejąca baza danych SQL.</span><span class="sxs-lookup"><span data-stu-id="aa1f2-157">In hello **Azure SQL Database** field, select hello existing SQL database.</span></span>

5.  <span data-ttu-id="aa1f2-158">W hello **kierunki synchronizacji** wybierz synchronizacji dwukierunkowe, toohello koncentratora, lub z hello koncentratora.</span><span class="sxs-lookup"><span data-stu-id="aa1f2-158">In hello **Sync Directions** field, select Bi-directional Sync, toohello Hub, or From hello Hub.</span></span>

    ![Dodawanie nowego elementu członkowskiego synchronizacji bazy danych SQL](media/sql-database-get-started-sql-data-sync/datasync-preview-memberadding.png)

6.  <span data-ttu-id="aa1f2-160">W hello **Username** i **hasło** wprowadź hello istniejących poświadczeń dla hello serwera bazy danych SQL, na które hello znajduje się bazy danych elementów członkowskich.</span><span class="sxs-lookup"><span data-stu-id="aa1f2-160">In hello **Username** and **Password** fields, enter hello existing credentials for hello SQL Database server on which hello member database is located.</span></span> <span data-ttu-id="aa1f2-161">Nie wprowadzaj *nowe* poświadczeń w tej sekcji.</span><span class="sxs-lookup"><span data-stu-id="aa1f2-161">Don't enter *new* credentials in this section.</span></span>

7.  <span data-ttu-id="aa1f2-162">Wybierz **OK** i poczekaj, aż hello nowe synchronizacji członek toobe utworzeniu i wdrożeniu.</span><span class="sxs-lookup"><span data-stu-id="aa1f2-162">Select **OK** and wait for hello new sync member toobe created and deployed.</span></span>

    ![Dodano nowy element członkowski synchronizacji bazy danych SQL](media/sql-database-get-started-sql-data-sync/datasync-preview-memberadded.png)

## <a name="add-an-on-premises-sql-server-database"></a><span data-ttu-id="aa1f2-164">Dodaj lokalną bazą danych programu SQL Server</span><span class="sxs-lookup"><span data-stu-id="aa1f2-164">Add an on-premises SQL Server database</span></span>

<span data-ttu-id="aa1f2-165">W hello **bazy danych elementów członkowskich** sekcji i opcjonalnie Dodaj grupy synchronizacji toohello lokalnego programu SQL Server, wybierając **Dodaj bazę danych z lokalnego**.</span><span class="sxs-lookup"><span data-stu-id="aa1f2-165">In hello **Member Database** section, optionally add an on-premises SQL Server toohello sync group by selecting **Add an On-Premises Database**.</span></span> <span data-ttu-id="aa1f2-166">Witaj **Konfigurowanie lokalnego** zostanie otwarty blok.</span><span class="sxs-lookup"><span data-stu-id="aa1f2-166">hello **Configure On-Premises** blade opens.</span></span>

<span data-ttu-id="aa1f2-167">Na powitania **Konfigurowanie lokalnego** bloku hello następujących czynności:</span><span class="sxs-lookup"><span data-stu-id="aa1f2-167">On hello **Configure On-Premises** blade, do hello following things:</span></span>

1.  <span data-ttu-id="aa1f2-168">Wybierz **hello wybierz bramy agenta synchronizacji**.</span><span class="sxs-lookup"><span data-stu-id="aa1f2-168">Select **Choose hello Sync Agent Gateway**.</span></span> <span data-ttu-id="aa1f2-169">Witaj **Agent synchronizacji wybierz** zostanie otwarty blok.</span><span class="sxs-lookup"><span data-stu-id="aa1f2-169">hello **Select Sync Agent** blade opens.</span></span>

    ![Wybierz bramę agent synchronizacji hello](media/sql-database-get-started-sql-data-sync/datasync-preview-choosegateway.png)

2.  <span data-ttu-id="aa1f2-171">Na powitania **hello wybierz bramy agenta synchronizacji** bloku, wybierz czy toouse istniejącego agenta lub Utwórz nowy agent.</span><span class="sxs-lookup"><span data-stu-id="aa1f2-171">On hello **Choose hello Sync Agent Gateway** blade, choose whether toouse an existing agent or create a new agent.</span></span>

    <span data-ttu-id="aa1f2-172">Jeśli została wybrana opcja **agentów istniejące**, wybierz hello istniejącego agenta z listy hello.</span><span class="sxs-lookup"><span data-stu-id="aa1f2-172">If you chose **Existing agents**, select hello existing agent from hello list.</span></span>

    <span data-ttu-id="aa1f2-173">Jeśli została wybrana opcja **Utwórz nowy agent**, hello następujących czynności:</span><span class="sxs-lookup"><span data-stu-id="aa1f2-173">If you chose **Create a new agent**, do hello following things:</span></span>

    1.  <span data-ttu-id="aa1f2-174">Pobierz oprogramowanie agenta do powitania klienta synchronizacji z łączem hello i zainstaluj go na komputerze hello, w którym znajduje się hello programu SQL Server.</span><span class="sxs-lookup"><span data-stu-id="aa1f2-174">Download hello client sync agent software from hello link provided and install it on hello computer where hello SQL Server is located.</span></span>
 
        > [!IMPORTANT]
        > <span data-ttu-id="aa1f2-175">Masz tooopen wychodzący port TCP 1433 w agenta hello zapory toolet powitania klienta komunikacji z serwerem hello.</span><span class="sxs-lookup"><span data-stu-id="aa1f2-175">You have tooopen outbound TCP port 1433 in hello firewall toolet hello client agent communicate with hello server.</span></span>


    2.  <span data-ttu-id="aa1f2-176">Wprowadź nazwę dla agenta hello.</span><span class="sxs-lookup"><span data-stu-id="aa1f2-176">Enter a name for hello agent.</span></span>

    3.  <span data-ttu-id="aa1f2-177">Wybierz **tworzenie i generowanie klucza**.</span><span class="sxs-lookup"><span data-stu-id="aa1f2-177">Select **Create and Generate Key**.</span></span>

    4.  <span data-ttu-id="aa1f2-178">Kopiuj hello agenta klucza toohello Schowka.</span><span class="sxs-lookup"><span data-stu-id="aa1f2-178">Copy hello agent key toohello clipboard.</span></span>
        
        ![Tworzenie nowego agenta synchronizacji](media/sql-database-get-started-sql-data-sync/datasync-preview-selectsyncagent.png)

    5.  <span data-ttu-id="aa1f2-180">Wybierz **OK** tooclose hello **Agent synchronizacji wybierz** bloku.</span><span class="sxs-lookup"><span data-stu-id="aa1f2-180">Select **OK** tooclose hello **Select Sync Agent** blade.</span></span>

    6.  <span data-ttu-id="aa1f2-181">Na komputerze serwera SQL hello Znajdź i uruchom aplikację klienta synchronizacji agenta hello.</span><span class="sxs-lookup"><span data-stu-id="aa1f2-181">On hello SQL Server computer, locate and run hello Client Sync Agent app.</span></span>

        ![dane Hello synchronizacji aplikacji agenta klienta](media/sql-database-get-started-sql-data-sync/datasync-preview-clientagent.png)

    7.  <span data-ttu-id="aa1f2-183">W aplikacji agenta synchronizacji hello, wybierz **przesłać klucz agenta**.</span><span class="sxs-lookup"><span data-stu-id="aa1f2-183">In hello sync agent app, select **Submit Agent Key**.</span></span> <span data-ttu-id="aa1f2-184">Witaj **synchronizacji metadanych bazy danych konfiguracji** zostanie otwarte okno dialogowe.</span><span class="sxs-lookup"><span data-stu-id="aa1f2-184">hello **Sync Metadata Database Configuration** dialog box opens.</span></span>

    8.  <span data-ttu-id="aa1f2-185">W hello **synchronizacji metadanych bazy danych konfiguracji** okno dialogowe, Wklej hello agenta klucza skopiowany z hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="aa1f2-185">In hello **Sync Metadata Database Configuration** dialog box, paste in hello agent key copied from hello Azure portal.</span></span> <span data-ttu-id="aa1f2-186">Udostępniają hello istniejących poświadczeń dla serwera bazy danych SQL Azure hello, na które hello znajduje się bazy danych metadanych.</span><span class="sxs-lookup"><span data-stu-id="aa1f2-186">Also provide hello existing credentials for hello Azure SQL Database server on which hello metadata database is located.</span></span> <span data-ttu-id="aa1f2-187">(Jeśli została utworzona nowa baza danych metadanych, ta baza danych znajduje się na powitania tym samym serwerze co baza danych Centrum hello.) Wybierz **OK** i poczekaj, aż hello toofinish konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="aa1f2-187">(If you created a new metadata database, this database is on hello same server as hello hub database.) Select **OK** and wait for hello configuration toofinish.</span></span>

        ![Wprowadź poświadczenia agenta hello klucza i serwera](media/sql-database-get-started-sql-data-sync/datasync-preview-agent-enterkey.png)

        >   [!NOTE] 
        >   <span data-ttu-id="aa1f2-189">Jeśli w tym momencie zostanie wyświetlony błąd zapory, należy toocreate reguły zapory na ruch przychodzący Azure tooallow z komputera z programem SQL Server hello.</span><span class="sxs-lookup"><span data-stu-id="aa1f2-189">If you get a firewall error at this point, you have toocreate a firewall rule on Azure tooallow incoming traffic from hello SQL Server computer.</span></span> <span data-ttu-id="aa1f2-190">Witaj regułę można utworzyć ręcznie w portalu hello, ale może być łatwiejsze toocreate go w programu SQL Server Management Studio (SSMS).</span><span class="sxs-lookup"><span data-stu-id="aa1f2-190">You can create hello rule manually in hello portal, but you may find it easier toocreate it in SQL Server Management Studio (SSMS).</span></span> <span data-ttu-id="aa1f2-191">W programie SSMS spróbuj tooconnect toohello centrum danych na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="aa1f2-191">In SSMS, try tooconnect toohello hub database on Azure.</span></span> <span data-ttu-id="aa1f2-192">Wpisz jej nazwę jako \<hub_database_name\>. database.windows.net.</span><span class="sxs-lookup"><span data-stu-id="aa1f2-192">Enter its name as \<hub_database_name\>.database.windows.net.</span></span> <span data-ttu-id="aa1f2-193">Wykonaj kroki hello hello okna dialogowego pole tooconfigure hello Azure reguła.</span><span class="sxs-lookup"><span data-stu-id="aa1f2-193">Follow hello steps in hello dialog box tooconfigure hello Azure firewall rule.</span></span> <span data-ttu-id="aa1f2-194">Następnie wróć toohello aplikacji agenta klienta synchronizacji.</span><span class="sxs-lookup"><span data-stu-id="aa1f2-194">Then return toohello Client Sync Agent app.</span></span>

    9.  <span data-ttu-id="aa1f2-195">W aplikacji agenta klienta synchronizacji powitania kliknij **zarejestrować** tooregister bazy danych programu SQL Server z agentem hello.</span><span class="sxs-lookup"><span data-stu-id="aa1f2-195">In hello Client Sync Agent app, click **Register** tooregister a SQL Server database with hello agent.</span></span> <span data-ttu-id="aa1f2-196">Witaj **konfiguracji serwera SQL** zostanie otwarte okno dialogowe.</span><span class="sxs-lookup"><span data-stu-id="aa1f2-196">hello **SQL Server Configuration** dialog box opens.</span></span>

        ![Dodaj i skonfiguruj bazę danych programu SQL Server](media/sql-database-get-started-sql-data-sync/datasync-preview-agent-adddb.png)

    10. <span data-ttu-id="aa1f2-198">W hello **konfiguracji serwera SQL** oknie dialogowym wybierz czy tooconnect przy użyciu uwierzytelniania programu SQL Server lub uwierzytelniania systemu Windows.</span><span class="sxs-lookup"><span data-stu-id="aa1f2-198">In hello **SQL Server Configuration** dialog box, choose whether tooconnect by using SQL Server authentication or Windows authentication.</span></span> <span data-ttu-id="aa1f2-199">Jeśli wybrano opcję uwierzytelniania programu SQL Server, wprowadź hello istniejących poświadczeń.</span><span class="sxs-lookup"><span data-stu-id="aa1f2-199">If you chose SQL Server authentication, enter hello existing credentials.</span></span> <span data-ttu-id="aa1f2-200">Podaj nazwę programu SQL Server hello oraz nazwę hello hello bazy danych o tym, że chcesz toosync.</span><span class="sxs-lookup"><span data-stu-id="aa1f2-200">Provide hello SQL Server name and hello name of hello database that you want toosync.</span></span> <span data-ttu-id="aa1f2-201">Wybierz **połączenie testowe** tootest ustawień.</span><span class="sxs-lookup"><span data-stu-id="aa1f2-201">Select **Test connection** tootest your settings.</span></span> <span data-ttu-id="aa1f2-202">Następnie wybierz **zapisać**.</span><span class="sxs-lookup"><span data-stu-id="aa1f2-202">Then select **Save**.</span></span> <span data-ttu-id="aa1f2-203">liście hello pojawi się Hello zarejestrowany w bazie danych.</span><span class="sxs-lookup"><span data-stu-id="aa1f2-203">hello registered database appears in hello list.</span></span>

        ![Baza danych SQL Server zostanie zarejestrowany](media/sql-database-get-started-sql-data-sync/datasync-preview-agent-dbadded.png)

    11. <span data-ttu-id="aa1f2-205">Można teraz zamknąć hello aplikacji agenta klienta synchronizacji.</span><span class="sxs-lookup"><span data-stu-id="aa1f2-205">You can now close hello Client Sync Agent app.</span></span>

    12. <span data-ttu-id="aa1f2-206">W portalu hello na powitania **Konfigurowanie lokalnego** bloku, wybierz opcję **wybierz hello bazy danych.**</span><span class="sxs-lookup"><span data-stu-id="aa1f2-206">In hello portal, on hello **Configure On-Premises** blade, select **Select hello Database.**</span></span> <span data-ttu-id="aa1f2-207">Witaj **wybierz bazę danych** zostanie otwarty blok.</span><span class="sxs-lookup"><span data-stu-id="aa1f2-207">hello **Select Database** blade opens.</span></span>

    13. <span data-ttu-id="aa1f2-208">Na powitania **wybierz bazę danych** bloku w hello **nazwa elementu członkowskiego synchronizacji** Podaj nazwę nowego członka synchronizacji hello.</span><span class="sxs-lookup"><span data-stu-id="aa1f2-208">On hello **Select Database** blade, in hello **Sync Member Name** field, provide a name for hello new sync member.</span></span> <span data-ttu-id="aa1f2-209">Ta nazwa różni się od nazwy hello hello bazy danych.</span><span class="sxs-lookup"><span data-stu-id="aa1f2-209">This name is distinct from hello name of hello database itself.</span></span> <span data-ttu-id="aa1f2-210">Wybierz bazę danych hello z listy hello.</span><span class="sxs-lookup"><span data-stu-id="aa1f2-210">Select hello database from hello list.</span></span> <span data-ttu-id="aa1f2-211">W hello **kierunki synchronizacji** wybierz synchronizacji dwukierunkowe, toohello koncentratora, lub z hello koncentratora.</span><span class="sxs-lookup"><span data-stu-id="aa1f2-211">In hello **Sync Directions** field, select Bi-directional Sync, toohello Hub, or From hello Hub.</span></span>

        ![Wybierz hello w lokalnej bazie danych](media/sql-database-get-started-sql-data-sync/datasync-preview-selectdb.png)

    14. <span data-ttu-id="aa1f2-213">Wybierz **OK** tooclose hello **wybierz bazę danych** bloku.</span><span class="sxs-lookup"><span data-stu-id="aa1f2-213">Select **OK** tooclose hello **Select Database** blade.</span></span> <span data-ttu-id="aa1f2-214">Następnie wybierz **OK** tooclose hello **Konfigurowanie lokalnego** bloku i poczekaj hello synchronizacji nowego elementu członkowskiego toobe utworzeniu i wdrożeniu.</span><span class="sxs-lookup"><span data-stu-id="aa1f2-214">Then select **OK** tooclose hello **Configure On-Premises** blade and wait for hello new sync member toobe created and deployed.</span></span> <span data-ttu-id="aa1f2-215">Na koniec kliknij **OK** tooclose hello **Wybierz członków synchronizacji** bloku.</span><span class="sxs-lookup"><span data-stu-id="aa1f2-215">Finally, click **OK** tooclose hello **Select sync members** blade.</span></span>

        ![W lokalnej bazie danych dodano grupę toosync](media/sql-database-get-started-sql-data-sync/datasync-preview-onpremadded.png)

3.  <span data-ttu-id="aa1f2-217">tooSQL tooconnect synchronizacji danych i hello lokalnego agenta, Dodaj toohello nazwa rola `DataSync_Executor`.</span><span class="sxs-lookup"><span data-stu-id="aa1f2-217">tooconnect tooSQL Data Sync and hello local agent, add your user name toohello role `DataSync_Executor`.</span></span> <span data-ttu-id="aa1f2-218">Synchronizacja danych tworzy tę rolę w wystąpieniu programu SQL Server hello.</span><span class="sxs-lookup"><span data-stu-id="aa1f2-218">Data Sync creates this role on hello SQL Server instance.</span></span>

## <a name="step-3---configure-sync-group"></a><span data-ttu-id="aa1f2-219">Krok 3 — Konfigurowanie synchronizacji grupy</span><span class="sxs-lookup"><span data-stu-id="aa1f2-219">Step 3 - Configure sync group</span></span>

<span data-ttu-id="aa1f2-220">Po hello nowych członków grupy synchronizacji są tworzone i wdrażane, krok 3 **Konfigurowanie synchronizacji grupy**, zostało wyróżnione hello **nowej grupy synchronizacji** bloku.</span><span class="sxs-lookup"><span data-stu-id="aa1f2-220">After hello new sync group members are created and deployed, Step 3, **Configure sync group**, is highlighted in hello **New sync group** blade.</span></span>

1.  <span data-ttu-id="aa1f2-221">Na powitania **tabel** bloku, wybierz bazę danych z listy hello synchronizacji członków grupy, a następnie wybierz **schematu odświeżania**.</span><span class="sxs-lookup"><span data-stu-id="aa1f2-221">On hello **Tables** blade, select a database from hello list of sync group members, and then select **Refresh schema**.</span></span>

2.  <span data-ttu-id="aa1f2-222">Zaznacz hello tabel, które mają toosync hello listę dostępnych tabel.</span><span class="sxs-lookup"><span data-stu-id="aa1f2-222">From hello list of available tables, select hello tables that you want toosync.</span></span>

    ![Wybierz tabele toosync](media/sql-database-get-started-sql-data-sync/datasync-preview-tables.png)

3.  <span data-ttu-id="aa1f2-224">Domyślnie wybrane są wszystkie kolumny w tabeli hello.</span><span class="sxs-lookup"><span data-stu-id="aa1f2-224">By default, all columns in hello table are selected.</span></span> <span data-ttu-id="aa1f2-225">Jeśli nie chcesz toosync wszystkie kolumny hello, wyłącz wyboru hello hello kolumn, że nie chcesz toosync.</span><span class="sxs-lookup"><span data-stu-id="aa1f2-225">If you don't want toosync all hello columns, disable hello checkbox for hello columns that you don't want toosync.</span></span> <span data-ttu-id="aa1f2-226">Upewnij się kolumna klucza podstawowego hello tooleave zaznaczone.</span><span class="sxs-lookup"><span data-stu-id="aa1f2-226">Be sure tooleave hello primary key column selected.</span></span>

    ![Wybierz pola toosync](media/sql-database-get-started-sql-data-sync/datasync-preview-tables2.png)

4.  <span data-ttu-id="aa1f2-228">Na koniec wybierz **zapisać**.</span><span class="sxs-lookup"><span data-stu-id="aa1f2-228">Finally, select **Save**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="aa1f2-229">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="aa1f2-229">Next steps</span></span>
<span data-ttu-id="aa1f2-230">Gratulacje.</span><span class="sxs-lookup"><span data-stu-id="aa1f2-230">Congratulations.</span></span> <span data-ttu-id="aa1f2-231">Utworzono grupę synchronizacji, która zawiera zarówno wystąpienie bazy danych SQL, jak i bazy danych programu SQL Server.</span><span class="sxs-lookup"><span data-stu-id="aa1f2-231">You have created a sync group that includes both a SQL Database instance and a SQL Server database.</span></span>

<span data-ttu-id="aa1f2-232">Aby uzyskać więcej informacji na temat bazy danych SQL i synchronizacji danych SQL zobacz:</span><span class="sxs-lookup"><span data-stu-id="aa1f2-232">For more info about SQL Database and SQL Data Sync, see:</span></span>

-   [<span data-ttu-id="aa1f2-233">Pobierz pełną dokumentację techniczną hello synchronizacji danych SQL</span><span class="sxs-lookup"><span data-stu-id="aa1f2-233">Download hello complete SQL Data Sync technical documentation</span></span>](https://github.com/Microsoft/sql-server-samples/raw/master/samples/features/sql-data-sync/Data_Sync_Preview_full_documentation.pdf?raw=true)
-   [<span data-ttu-id="aa1f2-234">Pobierz hello dokumentacji interfejsu API REST synchronizacji danych SQL</span><span class="sxs-lookup"><span data-stu-id="aa1f2-234">Download hello SQL Data Sync REST API documentation</span></span>](https://github.com/Microsoft/sql-server-samples/raw/master/samples/features/sql-data-sync/Data_Sync_Preview_REST_API.pdf?raw=true)
-   [<span data-ttu-id="aa1f2-235">Omówienie bazy danych SQL</span><span class="sxs-lookup"><span data-stu-id="aa1f2-235">SQL Database Overview</span></span>](sql-database-technical-overview.md)
-   [<span data-ttu-id="aa1f2-236">Zarządzanie cyklem życia bazy danych</span><span class="sxs-lookup"><span data-stu-id="aa1f2-236">Database Lifecycle Management</span></span>](https://msdn.microsoft.com/library/jj907294.aspx)
