---
title: aaaRestore pojedynczej tabeli z kopii zapasowej bazy danych SQL Azure | Dokumentacja firmy Microsoft
description: "Dowiedz się, jak toorestore pojedynczej tabeli z kopii zapasowej bazy danych SQL Azure."
services: sql-database
documentationcenter: 
author: dalechen
manager: cshepard
editor: 
ms.assetid: 340b41bd-9df8-47fb-adfc-03216de38a5e
ms.service: sql-database
ms.custom: business continuity
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/13/2017
ms.author: daleche
ms.openlocfilehash: 696d2ac87a70bccdf063bfecb8255723404aa5bd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toorestore-a-single-table-from-an-azure-sql-database-backup"></a><span data-ttu-id="1d953-103">Jak toorestore pojedynczej tabeli z kopii zapasowej bazy danych SQL Azure</span><span class="sxs-lookup"><span data-stu-id="1d953-103">How toorestore a single table from an Azure SQL Database backup</span></span>
<span data-ttu-id="1d953-104">Może wystąpić sytuacja, w którym przypadkowo zmodyfikowano niektóre dane w bazie danych SQL, a teraz ma toorecover hello pojedynczej tabeli dotyczy.</span><span class="sxs-lookup"><span data-stu-id="1d953-104">You may encounter a situation in which you accidentally modified some data in a SQL database and now you want toorecover hello single affected table.</span></span> <span data-ttu-id="1d953-105">W tym artykule opisano, jak toorestore pojedynczej tabeli w bazie danych z jednego z hello bazy danych SQL [automatycznego tworzenia kopii zapasowych](sql-database-automated-backups.md).</span><span class="sxs-lookup"><span data-stu-id="1d953-105">This article describes how toorestore a single table in a database from one of hello SQL Database [automatic backups](sql-database-automated-backups.md).</span></span>

## <a name="preparation-steps-rename-hello-table-and-restore-a-copy-of-hello-database"></a><span data-ttu-id="1d953-106">Czynności przygotowujące: Zmień nazwę tabeli hello i przywrócenie kopii bazy danych hello</span><span class="sxs-lookup"><span data-stu-id="1d953-106">Preparation steps: Rename hello table and restore a copy of hello database</span></span>
1. <span data-ttu-id="1d953-107">Zidentyfikuj hello tabeli, które mają tooreplace hello przywrócić kopię bazy danych Azure SQL.</span><span class="sxs-lookup"><span data-stu-id="1d953-107">Identify hello table in your Azure SQL database that you want tooreplace with hello restored copy.</span></span> <span data-ttu-id="1d953-108">Użyj programu Microsoft SQL Management Studio toorename hello tabeli.</span><span class="sxs-lookup"><span data-stu-id="1d953-108">Use Microsoft SQL Management Studio toorename hello table.</span></span> <span data-ttu-id="1d953-109">Na przykład zmienić nazwę tabeli hello jako &lt;nazwy tabeli&gt;_old.</span><span class="sxs-lookup"><span data-stu-id="1d953-109">For example, rename hello table as &lt;table name&gt;_old.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="1d953-110">tooavoid blokowane, upewnij się, że nic się nie uruchomione na powitania tabeli, która jest zmieniana.</span><span class="sxs-lookup"><span data-stu-id="1d953-110">tooavoid being blocked, make sure that there's no activity running on hello table that you are renaming.</span></span> <span data-ttu-id="1d953-111">Jeśli wystąpią problemy, upewnij się, że wykonać tę procedurę w oknie obsługi.</span><span class="sxs-lookup"><span data-stu-id="1d953-111">If you encounter issues, make sure that perform this procedure during a maintenance window.</span></span>
   >

2. <span data-ttu-id="1d953-112">Przywróć kopię zapasową punktu tooa bazy danych w czasie, które mają toorecover toousing hello [punkt-In_Time przywrócić](sql-database-recovery-using-backups.md#point-in-time-restore) czynności.</span><span class="sxs-lookup"><span data-stu-id="1d953-112">Restore a backup of your database tooa point in time that you want toorecover toousing hello [Point-In_Time Restore](sql-database-recovery-using-backups.md#point-in-time-restore) steps.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="1d953-113">Nazwa Hello hello przywrócona baza danych będzie w hello DBName + format sygnatury czasowej; na przykład **Adventureworks2012_2016-01-01T22-12Z**.</span><span class="sxs-lookup"><span data-stu-id="1d953-113">hello name of hello restored database will be in hello DBName+TimeStamp format; for example, **Adventureworks2012_2016-01-01T22-12Z**.</span></span> <span data-ttu-id="1d953-114">Ten krok nie zastąpienie nazwy istniejącej bazy danych hello na powitania serwera.</span><span class="sxs-lookup"><span data-stu-id="1d953-114">This step doesn't overwrite hello existing database name on hello server.</span></span> <span data-ttu-id="1d953-115">Jest to miara bezpieczeństwa i jest on przeznaczony tooallow tooverify hello przywrócone bazy danych, aby usunąć ich bieżącej bazy danych i Zmień nazwę bazy danych hello przywrócone do użytku produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="1d953-115">This is a safety measure, and it's intended tooallow you tooverify hello restored database before they drop their current database and rename hello restored database for production use.</span></span>
   
## <a name="copying-hello-table-from-hello-restored-database-by-using-hello-sql-database-migration-tool"></a><span data-ttu-id="1d953-116">Kopiowanie tabeli hello z hello przywrócić bazy danych przy użyciu narzędzia do migracji bazy danych SQL hello</span><span class="sxs-lookup"><span data-stu-id="1d953-116">Copying hello table from hello restored database by using hello SQL Database Migration tool</span></span>

1. <span data-ttu-id="1d953-117">Pobierz i zainstaluj hello [Kreatora migracji bazy danych SQL](https://sqlazuremw.codeplex.com).</span><span class="sxs-lookup"><span data-stu-id="1d953-117">Download and install hello [SQL Database Migration Wizard](https://sqlazuremw.codeplex.com).</span></span>
2. <span data-ttu-id="1d953-118">Hello otwórz Kreator migracji bazy danych SQL, na powitania **wybierz proces** wybierz **bazy danych w obszarze Analizuj/migracji**, a następnie kliknij przycisk **dalej**.</span><span class="sxs-lookup"><span data-stu-id="1d953-118">Open hello SQL Database Migration Wizard, on hello **Select Process** page, select **Database under Analyze/Migrate**, and then click **Next**.</span></span>

   ![Kreator migracji bazy danych SQL — wybierz procesu](./media/sql-database-cloud-migrate-restore-single-table-azure-backup/1.png)

3. <span data-ttu-id="1d953-120">W hello **połączyć tooServer** okna dialogowego należy zastosować hello następujące ustawienia:</span><span class="sxs-lookup"><span data-stu-id="1d953-120">In hello **Connect tooServer** dialog box, apply hello following settings:</span></span>

   * <span data-ttu-id="1d953-121">Nazwa serwera: **Your SQL server**</span><span class="sxs-lookup"><span data-stu-id="1d953-121">Server name: **Your SQL server**</span></span>
   * <span data-ttu-id="1d953-122">Uwierzytelnianie: **uwierzytelniania programu SQL Server**</span><span class="sxs-lookup"><span data-stu-id="1d953-122">Authentication: **SQL Server Authentication**</span></span>
   * <span data-ttu-id="1d953-123">Nazwa użytkownika: **logowanie**</span><span class="sxs-lookup"><span data-stu-id="1d953-123">Login: **Your login**</span></span>
   * <span data-ttu-id="1d953-124">Hasło: **hasła**</span><span class="sxs-lookup"><span data-stu-id="1d953-124">Password: **Your password**</span></span>
   * <span data-ttu-id="1d953-125">Baza danych: **bazy danych Master (listę wszystkich baz danych)**</span><span class="sxs-lookup"><span data-stu-id="1d953-125">Database: **Master DB (List all databases)**</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="1d953-126">Domyślnie hello kreator zapisuje informacje logowania.</span><span class="sxs-lookup"><span data-stu-id="1d953-126">By default hello wizard saves your login information.</span></span> <span data-ttu-id="1d953-127">Jeśli nie chcesz jej, wybierz **zapomnij informacje logowania**.</span><span class="sxs-lookup"><span data-stu-id="1d953-127">If you don't want it to, select **Forget Login Information**.</span></span>
   >
   
     ![Migracja bazy danych SQL kreatora — wybierz źródło — krok 1](./media/sql-database-cloud-migrate-restore-single-table-azure-backup/2.png)
4. <span data-ttu-id="1d953-129">W hello **wybierz źródło** okno dialogowe, nazwa bazy danych wybierz hello przywrócone z hello **czynności przygotowujące** sekcji jako źródła, a następnie kliknij przycisk **dalej**.</span><span class="sxs-lookup"><span data-stu-id="1d953-129">In hello **Select Source** dialog box, select hello restored database name from hello **Preparation steps** section as your source, and then click **Next**.</span></span>
   
    ![Migracja bazy danych SQL kreatora — wybierz źródło — krok 2](./media/sql-database-cloud-migrate-restore-single-table-azure-backup/3.png)
5. <span data-ttu-id="1d953-131">W hello **wybierz obiekty** okno dialogowe, wybierz opcję hello **określonych obiektów bazy danych wybierz** opcji, a następnie wybierz table(or tables) hello czy chcesz, aby serwer docelowy toohello toomigrate.</span><span class="sxs-lookup"><span data-stu-id="1d953-131">In hello **Choose Objects** dialog box, select hello **Select specific database objects** option, and then select hello table(or tables) that you want toomigrate toohello target server.</span></span>
   <span data-ttu-id="1d953-132">![Kreator migracji bazy danych SQL — Wybieranie obiektów](./media/sql-database-cloud-migrate-restore-single-table-azure-backup/4.png)</span><span class="sxs-lookup"><span data-stu-id="1d953-132">![SQL Database Migration wizard - Choose Objects](./media/sql-database-cloud-migrate-restore-single-table-azure-backup/4.png)</span></span>
6. <span data-ttu-id="1d953-133">Na powitania **Podsumowanie Kreatora skryptu** kliknij przycisk **tak** monit o czy wszystko jest gotowe toogenerate skryptu SQL.</span><span class="sxs-lookup"><span data-stu-id="1d953-133">On hello **Script Wizard Summary** page, click **Yes** when you’re prompted about whether you’re ready toogenerate a SQL script.</span></span> <span data-ttu-id="1d953-134">Istnieje również opcja hello toosave hello skryptu TSQL do późniejszego użycia.</span><span class="sxs-lookup"><span data-stu-id="1d953-134">You also have hello option toosave hello TSQL Script for later use.</span></span>
   <span data-ttu-id="1d953-135">![Kreator migracji bazy danych SQL — Podsumowanie Kreatora skryptu](./media/sql-database-cloud-migrate-restore-single-table-azure-backup/5.png)</span><span class="sxs-lookup"><span data-stu-id="1d953-135">![SQL Database Migration wizard - Script Wizard Summary](./media/sql-database-cloud-migrate-restore-single-table-azure-backup/5.png)</span></span>
7. <span data-ttu-id="1d953-136">Na powitania **podsumowania wyników** kliknij przycisk **dalej**.</span><span class="sxs-lookup"><span data-stu-id="1d953-136">On hello **Results Summary** page, click **Next**.</span></span>
   <span data-ttu-id="1d953-137">![Kreator migracji bazy danych SQL — podsumowanie wyników](./media/sql-database-cloud-migrate-restore-single-table-azure-backup/6.png)</span><span class="sxs-lookup"><span data-stu-id="1d953-137">![SQL Database Migration wizard - Results Summary](./media/sql-database-cloud-migrate-restore-single-table-azure-backup/6.png)</span></span>
8. <span data-ttu-id="1d953-138">Na powitania **ustawienia połączenia z serwerem docelowym** kliknij przycisk **połączyć tooServer**, a następnie wprowadź szczegóły hello w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="1d953-138">On hello **Setup Target Server Connection** page, click **Connect tooServer**, and then enter hello details as follows:</span></span>
   
   * <span data-ttu-id="1d953-139">**Nazwa serwera**: wystąpienie serwera docelowego</span><span class="sxs-lookup"><span data-stu-id="1d953-139">**Server Name**: Target server instance</span></span>
   * <span data-ttu-id="1d953-140">**Uwierzytelnianie**: **uwierzytelniania programu SQL Server**.</span><span class="sxs-lookup"><span data-stu-id="1d953-140">**Authentication**: **SQL Server authentication**.</span></span> <span data-ttu-id="1d953-141">Wprowadź poświadczenia logowania.</span><span class="sxs-lookup"><span data-stu-id="1d953-141">Enter your login credentials.</span></span>
   * <span data-ttu-id="1d953-142">**Baza danych**: **bazy danych Master (listę wszystkich baz danych)**.</span><span class="sxs-lookup"><span data-stu-id="1d953-142">**Database**: **Master DB (List all databases)**.</span></span> <span data-ttu-id="1d953-143">Ta opcja wyświetla listę wszystkich hello baz danych na serwerze docelowym hello.</span><span class="sxs-lookup"><span data-stu-id="1d953-143">This option lists all hello databases on hello target server.</span></span>
     
     ![Kreator migracji bazy danych SQL — Skonfiguruj połączenie z serwera docelowego](./media/sql-database-cloud-migrate-restore-single-table-azure-backup/7.png)
9. <span data-ttu-id="1d953-145">Kliknij przycisk **Connect**, wybierz docelową bazę danych hello, tabela hello toomove, a następnie kliknij przycisk **dalej**.</span><span class="sxs-lookup"><span data-stu-id="1d953-145">Click **Connect**, select hello target database that you want toomove hello table to, and then click **Next**.</span></span> <span data-ttu-id="1d953-146">To powinno zostać zakończone uruchomienie skryptu hello wcześniej wygenerowany i powinien pojawić się hello nowo przenieść tabeli skopiowanych toohello docelowej bazy danych.</span><span class="sxs-lookup"><span data-stu-id="1d953-146">This should finish running hello previously generated script, and you should see hello newly moved table copied toohello target database.</span></span>

## <a name="verification-step"></a><span data-ttu-id="1d953-147">Krok weryfikacji</span><span class="sxs-lookup"><span data-stu-id="1d953-147">Verification step</span></span>

- <span data-ttu-id="1d953-148">Zapytania i przetestować toomake tabeli hello nowo skopiowany pewność, że dane hello jest prawidłowa.</span><span class="sxs-lookup"><span data-stu-id="1d953-148">Query and test hello newly copied table toomake sure that hello data is intact.</span></span> <span data-ttu-id="1d953-149">Po potwierdzeniu, musisz porzucić hello zmienić nazwy tabeli formularza **czynności przygotowujące** sekcji.</span><span class="sxs-lookup"><span data-stu-id="1d953-149">Upon confirmation, you can drop hello renamed table form **Preparation steps** section.</span></span> <span data-ttu-id="1d953-150">(na przykład &lt;nazwy tabeli&gt;_old).</span><span class="sxs-lookup"><span data-stu-id="1d953-150">(for example, &lt;table name&gt;_old).</span></span>

## <a name="next-steps"></a><span data-ttu-id="1d953-151">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="1d953-151">Next steps</span></span>
[<span data-ttu-id="1d953-152">Automatyczne kopie zapasowe bazy danych SQL</span><span class="sxs-lookup"><span data-stu-id="1d953-152">SQL Database automatic backups</span></span>](sql-database-automated-backups.md)

