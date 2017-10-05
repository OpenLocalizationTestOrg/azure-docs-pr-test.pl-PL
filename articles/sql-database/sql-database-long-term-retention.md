---
title: Przechowywanie kopii zapasowych bazy danych SQL Azure przez maksymalnie 10 lat | Dokumentacja firmy Microsoft
description: "Dowiedz się, jak baza danych SQL Azure obsługuje przechowywania kopii zapasowych maksymalnie 10 lat."
keywords: 
services: sql-database
documentationcenter: 
author: anosov1960
manager: jhubbard
editor: 
ms.assetid: 66fdb8b8-5903-4d3a-802e-af08d204566e
ms.service: sql-database
ms.custom: business continuity
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 12/22/2016
ms.author: sashan
ms.openlocfilehash: 25e651203f804fbf32d632b5f83145a3f3f72a7f
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="store-azure-sql-database-backups-for-up-to-10-years"></a><span data-ttu-id="1cdbb-103">Przechowywanie kopii zapasowych bazy danych SQL Azure przez maksymalnie 10 lat</span><span class="sxs-lookup"><span data-stu-id="1cdbb-103">Store Azure SQL Database backups for up to 10 years</span></span>
<span data-ttu-id="1cdbb-104">Wiele aplikacji ma przepisów prawnych, zgodności lub innych firm celów, które wymagają przechowywania kopii zapasowych bazy danych poza 7 35 dni pochodzącymi z bazy danych SQL Azure [automatycznego tworzenia kopii zapasowych](sql-database-automated-backups.md).</span><span class="sxs-lookup"><span data-stu-id="1cdbb-104">Many applications have regulatory, compliance, or other business purposes that require you to retain database backups beyond the 7-35 days provided by Azure SQL Database [automatic backups](sql-database-automated-backups.md).</span></span> <span data-ttu-id="1cdbb-105">Za pomocą funkcji długoterminowego przechowywania kopii zapasowych, można przechowywać kopie zapasowe bazy danych SQL w magazynie usług odzyskiwania Azure przez maksymalnie 10 lat.</span><span class="sxs-lookup"><span data-stu-id="1cdbb-105">By using the long-term backup retention feature, you can store your SQL database backups in an Azure Recovery Services vault for up to 10 years.</span></span> <span data-ttu-id="1cdbb-106">Można przechowywać maksymalnie 1000 baz danych na magazynie.</span><span class="sxs-lookup"><span data-stu-id="1cdbb-106">You can store up to 1,000 databases per vault.</span></span> <span data-ttu-id="1cdbb-107">Następnie można wybrać jakiejkolwiek kopii zapasowej w magazynie, aby przywrócić go jako nową bazę danych.</span><span class="sxs-lookup"><span data-stu-id="1cdbb-107">You then can select any backup in the vault to restore it as a new database.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="1cdbb-108">Długoterminowego przechowywania kopii zapasowych jest obecnie w wersji zapoznawczej i jest dostępna w następujących regionach: Australia Wschodnia, Australia Południowo-Wschodnia, Brazylia Południowa, środkowe stany USA, Azja Wschodnia, wschodnie stany USA, wschodnie stany USA 2, Indie środkowe, Indie Południowe, Japonia Wschodnia, Japonia Zachodnia, północno-środkowe stany, Północna Europa, Południowej środkowe stany USA, Azja południowo-wschodnia, Europa Zachodnia i zachodnie stany USA</span><span class="sxs-lookup"><span data-stu-id="1cdbb-108">Long-term backup retention is currently in preview and available in the following regions: Australia East, Australia Southeast, Brazil South, Central US, East Asia, East US, East US 2, India Central, India South, Japan East, Japan West, North Central US, North Europe, South Central US, Southeast Asia, West Europe, and West US.</span></span>
>

> [!NOTE]
> <span data-ttu-id="1cdbb-109">Maksymalnie 200 baz danych na magazyn można włączyć w 24-godzinnym przedziale czasu.</span><span class="sxs-lookup"><span data-stu-id="1cdbb-109">You can enable up to 200 databases per vault during a 24-hour period.</span></span> <span data-ttu-id="1cdbb-110">Zalecane jest użycie oddzielnych magazynu dla każdego serwera, aby zminimalizować wpływ ten limit.</span><span class="sxs-lookup"><span data-stu-id="1cdbb-110">We recommend that you use a separate vault for each server to minimize the impact of this limit.</span></span> 
> 

## <a name="how-sql-database-long-term-backup-retention-works"></a><span data-ttu-id="1cdbb-111">Jak działa długoterminowego przechowywania kopii zapasowych bazy danych SQL</span><span class="sxs-lookup"><span data-stu-id="1cdbb-111">How SQL Database long-term backup retention works</span></span>

<span data-ttu-id="1cdbb-112">Z długoterminowego przechowywania kopii zapasowych można skojarzyć serwer bazy danych SQL z magazynu usług odzyskiwania Azure.</span><span class="sxs-lookup"><span data-stu-id="1cdbb-112">With long-term backup retention, you can associate a SQL database server with an Azure Recovery Services vault.</span></span> 

* <span data-ttu-id="1cdbb-113">Należy utworzyć magazyn do tej samej subskrypcji platformy Azure, utworzony programu SQL server i w tym samym regionie geograficznym i grupy zasobów.</span><span class="sxs-lookup"><span data-stu-id="1cdbb-113">You must create the vault in the same Azure subscription that created the SQL server and in the same geographic region and resource group.</span></span> 
* <span data-ttu-id="1cdbb-114">Następnie skonfiguruj zasady przechowywania dla dowolnej bazy danych.</span><span class="sxs-lookup"><span data-stu-id="1cdbb-114">You then configure a retention policy for any database.</span></span> <span data-ttu-id="1cdbb-115">Zasad powoduje, że cotygodniowe kopie zapasowe pełnej bazy danych należy skopiować do magazynu usług odzyskiwania i przechowywane przez okres przechowywania określony (maksymalnie 10 lat).</span><span class="sxs-lookup"><span data-stu-id="1cdbb-115">The policy causes the weekly full database backups to be copied to the Recovery Services vault and retained for the specified retention period (up to 10 years).</span></span> 
* <span data-ttu-id="1cdbb-116">Następnie można przywrócić bazy danych z dowolnego z tych kopii zapasowych do nowej bazy danych w dowolnego serwera w ramach subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="1cdbb-116">You can then restore the database from any of these backups to a new database in any server in the subscription.</span></span> <span data-ttu-id="1cdbb-117">Magazynu Azure tworzy kopię na podstawie istniejących kopii zapasowych, a kopia nie ma wpływu wydajności w istniejącej bazie danych.</span><span class="sxs-lookup"><span data-stu-id="1cdbb-117">Azure storage creates a copy from existing backups, and the copy has no performance impact on the existing database.</span></span>

> [!TIP]
> <span data-ttu-id="1cdbb-118">Aby uzyskać przewodnik, zobacz [Konfigurowanie i przywrócenie z długoterminowego przechowywania kopii zapasowych bazy danych SQL Azure](sql-database-long-term-backup-retention-configure.md).</span><span class="sxs-lookup"><span data-stu-id="1cdbb-118">For a how-to guide, see [Configure and restore from Azure SQL Database long-term backup retention](sql-database-long-term-backup-retention-configure.md).</span></span>

## <a name="enable-long-term-backup-retention"></a><span data-ttu-id="1cdbb-119">Włącz długoterminowego przechowywania kopii zapasowych</span><span class="sxs-lookup"><span data-stu-id="1cdbb-119">Enable long-term backup retention</span></span>

<span data-ttu-id="1cdbb-120">Aby skonfigurować długoterminowego przechowywania kopii zapasowych bazy danych:</span><span class="sxs-lookup"><span data-stu-id="1cdbb-120">To configure long-term backup retention for a database:</span></span>

1. <span data-ttu-id="1cdbb-121">Tworzenie magazynu usług odzyskiwania Azure w tym samym regionie, subskrypcji i grupy zasobów jako serwer bazy danych SQL.</span><span class="sxs-lookup"><span data-stu-id="1cdbb-121">Create an Azure Recovery Services vault in the same region, subscription, and resource group as your SQL database server.</span></span> 
2. <span data-ttu-id="1cdbb-122">Zarejestruj serwer w magazynie.</span><span class="sxs-lookup"><span data-stu-id="1cdbb-122">Register the server to the vault.</span></span>
3. <span data-ttu-id="1cdbb-123">Tworzenie zasad ochrony usług odzyskiwania Azure.</span><span class="sxs-lookup"><span data-stu-id="1cdbb-123">Create an Azure Recovery Services protection policy.</span></span>
4. <span data-ttu-id="1cdbb-124">Zastosowanie zasad ochrony do baz danych, które wymagają długoterminowego przechowywania kopii zapasowych.</span><span class="sxs-lookup"><span data-stu-id="1cdbb-124">Apply the protection policy to the databases that require long-term backup retention.</span></span>

<span data-ttu-id="1cdbb-125">Konfigurowanie, zarządzanie i przywracanie bazy danych z długoterminowego przechowywania kopii zapasowych automatycznych kopii zapasowych w magazynie usług odzyskiwania Azure, wykonaj jedną z następujących czynności:</span><span class="sxs-lookup"><span data-stu-id="1cdbb-125">To configure, manage, and restore a database from long-term backup retention of automated backups in an Azure Recovery Services vault, do either of the following:</span></span>

* <span data-ttu-id="1cdbb-126">Przy użyciu portalu Azure: kliknij **długoterminowego przechowywania kopii zapasowych**, wybierz bazę danych, a następnie kliknij przycisk **Konfiguruj**.</span><span class="sxs-lookup"><span data-stu-id="1cdbb-126">Using the Azure portal: Click **Long-term backup retention**, select a database, and then click **Configure**.</span></span> 

   ![Wybierz bazę danych do długoterminowego przechowywania kopii zapasowych](./media/sql-database-get-started-backup-recovery/select-database-for-long-term-backup-retention.png)

* <span data-ttu-id="1cdbb-128">Przy użyciu programu PowerShell: Przejdź do [Konfigurowanie i przywrócenie z długoterminowego przechowywania kopii zapasowych bazy danych SQL Azure](sql-database-long-term-backup-retention-configure.md).</span><span class="sxs-lookup"><span data-stu-id="1cdbb-128">Using PowerShell: Go to [Configure and restore from Azure SQL Database long-term backup retention](sql-database-long-term-backup-retention-configure.md).</span></span>

## <a name="restore-a-database-thats-stored-with-the-long-term-backup-retention-feature"></a><span data-ttu-id="1cdbb-129">Przywracanie bazy danych przechowywanych funkcją długoterminowego przechowywania kopii zapasowych</span><span class="sxs-lookup"><span data-stu-id="1cdbb-129">Restore a database that's stored with the long-term backup retention feature</span></span>

<span data-ttu-id="1cdbb-130">Aby odzyskać z kopii zapasowej długoterminowego przechowywania kopii zapasowych:</span><span class="sxs-lookup"><span data-stu-id="1cdbb-130">To recover from a long-term backup retention backup:</span></span>

1. <span data-ttu-id="1cdbb-131">Wyświetl listę magazynu, w której jest przechowywana kopia zapasowa.</span><span class="sxs-lookup"><span data-stu-id="1cdbb-131">List the vault where the backup is stored.</span></span>
2. <span data-ttu-id="1cdbb-132">Lista kontenera, który jest zamapowany z serwerem logicznym.</span><span class="sxs-lookup"><span data-stu-id="1cdbb-132">List the container that is mapped to your logical server.</span></span>
3. <span data-ttu-id="1cdbb-133">Lista źródła danych w ramach magazynu, który jest mapowany do bazy danych.</span><span class="sxs-lookup"><span data-stu-id="1cdbb-133">List the data source within the vault that is mapped to your database.</span></span>
4. <span data-ttu-id="1cdbb-134">Lista punktów odzyskiwania, które są dostępne do przywrócenia.</span><span class="sxs-lookup"><span data-stu-id="1cdbb-134">List the recovery points that are available to restore.</span></span>
5. <span data-ttu-id="1cdbb-135">Przywracanie bazy danych z punktu odzyskiwania na serwerze docelowym w ramach subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="1cdbb-135">Restore the database from the recovery point to the target server within your subscription.</span></span>

<span data-ttu-id="1cdbb-136">Konfigurowanie, zarządzanie i przywracanie bazy danych z długoterminowego przechowywania kopii zapasowych automatycznych kopii zapasowych w magazynie usług odzyskiwania Azure, wykonaj jedną z następujących czynności:</span><span class="sxs-lookup"><span data-stu-id="1cdbb-136">To configure, manage, and restore a database from long-term backup retention of automated backups in an Azure Recovery Services vault, do either of the following:</span></span>

* <span data-ttu-id="1cdbb-137">Przy użyciu portalu Azure: Przejdź do [Zarządzanie długoterminowego przechowywania kopii zapasowych przy użyciu portalu Azure](sql-database-long-term-backup-retention-configure.md).</span><span class="sxs-lookup"><span data-stu-id="1cdbb-137">Using the Azure portal: Go to [Manage long-term backup retention using the Azure portal](sql-database-long-term-backup-retention-configure.md).</span></span> 

* <span data-ttu-id="1cdbb-138">Przy użyciu programu PowerShell: Przejdź do [Zarządzanie długoterminowego przechowywania kopii zapasowych przy użyciu programu PowerShell](sql-database-long-term-backup-retention-configure.md).</span><span class="sxs-lookup"><span data-stu-id="1cdbb-138">Using PowerShell: Go to [Manage long-term backup retention using PowerShell](sql-database-long-term-backup-retention-configure.md).</span></span>

## <a name="get-pricing-for-long-term-backup-retention"></a><span data-ttu-id="1cdbb-139">Pobierz ceny dla długoterminowego przechowywania kopii zapasowych</span><span class="sxs-lookup"><span data-stu-id="1cdbb-139">Get pricing for long-term backup retention</span></span>

<span data-ttu-id="1cdbb-140">Długoterminowego przechowywania kopii zapasowych bazy danych SQL jest rozliczana zgodnie z [usługi kopii zapasowej Azure cennik stawki](https://azure.microsoft.com/pricing/details/backup/).</span><span class="sxs-lookup"><span data-stu-id="1cdbb-140">Long-term backup retention of a SQL database is charged according to the [Azure backup services pricing rates](https://azure.microsoft.com/pricing/details/backup/).</span></span>

<span data-ttu-id="1cdbb-141">Po zarejestrowaniu serwera bazy danych SQL w magazynie są naliczane opłaty za całkowita ilość miejsca, który jest używany przez cotygodniowe kopie zapasowe przechowywane w magazynie.</span><span class="sxs-lookup"><span data-stu-id="1cdbb-141">After the SQL database server is registered to the vault, you are charged for the total storage that's used by the weekly backups stored in the vault.</span></span>

## <a name="view-available-backups-that-are-stored-in-long-term-backup-retention"></a><span data-ttu-id="1cdbb-142">Wyświetl dostępne kopie zapasowe, które są przechowywane w długoterminowego przechowywania kopii zapasowych</span><span class="sxs-lookup"><span data-stu-id="1cdbb-142">View available backups that are stored in long-term backup retention</span></span>

<span data-ttu-id="1cdbb-143">Konfigurowanie, zarządzanie i przywrócić bazę danych z długoterminowego przechowywania kopii zapasowych automatycznych kopii zapasowych w magazynie usług odzyskiwania Azure przy użyciu portalu Azure, wykonaj jedną z następujących czynności:</span><span class="sxs-lookup"><span data-stu-id="1cdbb-143">To configure, manage, and restore a database from long-term backup retention of automated backups in an Azure Recovery Services vault by using the Azure portal, do either of the following:</span></span>

* <span data-ttu-id="1cdbb-144">Przy użyciu portalu Azure: Przejdź do [Zarządzanie długoterminowego przechowywania kopii zapasowych przy użyciu portalu Azure](sql-database-long-term-backup-retention-configure.md).</span><span class="sxs-lookup"><span data-stu-id="1cdbb-144">Using the Azure portal: Go to [Manage long-term backup retention using the Azure portal](sql-database-long-term-backup-retention-configure.md).</span></span> 

* <span data-ttu-id="1cdbb-145">Przy użyciu programu PowerShell: Przejdź do [Zarządzanie długoterminowego przechowywania kopii zapasowych przy użyciu programu PowerShell](sql-database-long-term-backup-retention-configure.md).</span><span class="sxs-lookup"><span data-stu-id="1cdbb-145">Using PowerShell: Go to [Manage long-term backup retention using PowerShell](sql-database-long-term-backup-retention-configure.md).</span></span>

## <a name="disable-long-term-retention"></a><span data-ttu-id="1cdbb-146">Wyłącz długoterminowego przechowywania</span><span class="sxs-lookup"><span data-stu-id="1cdbb-146">Disable long-term retention</span></span>

<span data-ttu-id="1cdbb-147">Usługi odzyskiwania obsługuje automatycznie Oczyszczanie na podstawie zasad podanych przechowywania kopii zapasowych.</span><span class="sxs-lookup"><span data-stu-id="1cdbb-147">The recovery service automatically handles the cleanup of backups based on the provided retention policy.</span></span> 

<span data-ttu-id="1cdbb-148">Aby zatrzymać wysyłanie kopii zapasowych dla określonej bazy danych do magazynu, należy usunąć zasady przechowywania dla tej bazy danych.</span><span class="sxs-lookup"><span data-stu-id="1cdbb-148">To stop sending the backups for a specific database to the vault, remove the retention policy for that database.</span></span>
  
```
Set-AzureRmSqlDatabaseBackupLongTermRetentionPolicy -ResourceGroupName 'RG1' -ServerName 'Server1' -DatabaseName 'DB1' -State 'Disabled' -ResourceId $policy.Id
```

> [!NOTE]
> <span data-ttu-id="1cdbb-149">Nie dotyczy to kopie zapasowe, które znajdują się już w magazynie.</span><span class="sxs-lookup"><span data-stu-id="1cdbb-149">The backups that are already in the vault are unaffected.</span></span> <span data-ttu-id="1cdbb-150">Zostaną one automatycznie usunięte przez usługi odzyskiwania po wygaśnięciu okresu przechowywania.</span><span class="sxs-lookup"><span data-stu-id="1cdbb-150">They are automatically deleted by the recovery service when their retention period expires.</span></span>

## <a name="long-term-backup-retention-faq"></a><span data-ttu-id="1cdbb-151">Długoterminowego przechowywania kopii zapasowych — często zadawane pytania</span><span class="sxs-lookup"><span data-stu-id="1cdbb-151">Long-term backup retention FAQ</span></span>

<span data-ttu-id="1cdbb-152">**Można ręcznie usunąć z określonych kopii zapasowych w magazynie?**</span><span class="sxs-lookup"><span data-stu-id="1cdbb-152">**Can I manually delete specific backups in the vault?**</span></span>

<span data-ttu-id="1cdbb-153">Nie można obecnie.</span><span class="sxs-lookup"><span data-stu-id="1cdbb-153">Not currently.</span></span> <span data-ttu-id="1cdbb-154">Magazyn automatycznie oczyszcza kopii zapasowych, po zakończeniu okresu przechowywania.</span><span class="sxs-lookup"><span data-stu-id="1cdbb-154">The vault automatically cleans up backups when the retention period has expired.</span></span>

<span data-ttu-id="1cdbb-155">**Można zarejestrować serwer do przechowywania kopii zapasowych do więcej niż jeden Magazyn?**</span><span class="sxs-lookup"><span data-stu-id="1cdbb-155">**Can I register my server to store backups to more than one vault?**</span></span>

<span data-ttu-id="1cdbb-156">Nie, w obecnie można przechowywać kopie zapasowe, aby tylko jeden magazyn, w czasie.</span><span class="sxs-lookup"><span data-stu-id="1cdbb-156">No, you can currently store backups to only one vault at a time.</span></span>

<span data-ttu-id="1cdbb-157">**W ramach różnych subskrypcji może mieć magazyn i serwera?**</span><span class="sxs-lookup"><span data-stu-id="1cdbb-157">**Can I have a vault and server in different subscriptions?**</span></span>

<span data-ttu-id="1cdbb-158">Nie, obecnie magazyn i serwer musi być w tej samej subskrypcji i grupy zasobów.</span><span class="sxs-lookup"><span data-stu-id="1cdbb-158">No, currently the vault and server must be in the same subscription and resource group.</span></span>

<span data-ttu-id="1cdbb-159">**Można użyć magazynu, który został utworzony w regionie, który jest inny niż region Mój serwer?**</span><span class="sxs-lookup"><span data-stu-id="1cdbb-159">**Can I use a vault that I created in a region that's different from my server’s region?**</span></span>

<span data-ttu-id="1cdbb-160">Nie, magazynu i serwer muszą być w tym samym regionie, aby zminimalizować czas kopiowania i zapobiec zmianom ruchu.</span><span class="sxs-lookup"><span data-stu-id="1cdbb-160">No, the vault and server must be in the same region to minimize copy time and avoid traffic charges.</span></span>

<span data-ttu-id="1cdbb-161">**Jak wiele baz danych można przechowywać w jednym magazynie?**</span><span class="sxs-lookup"><span data-stu-id="1cdbb-161">**How many databases can I store in one vault?**</span></span>

<span data-ttu-id="1cdbb-162">Obecnie usługa obsługuje maksymalnie 1000 baz danych na magazynie.</span><span class="sxs-lookup"><span data-stu-id="1cdbb-162">Currently, we support up to 1,000 databases per vault.</span></span> 

<span data-ttu-id="1cdbb-163">**Jak wiele magazynów można utworzyć na subskrypcję?**</span><span class="sxs-lookup"><span data-stu-id="1cdbb-163">**How many vaults can I create per subscription?**</span></span>

<span data-ttu-id="1cdbb-164">Możesz utworzyć maksymalnie 25 magazynów dla subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="1cdbb-164">You can create up to 25 vaults per subscription.</span></span>

<span data-ttu-id="1cdbb-165">**Jak wiele baz danych można skonfigurować na dzień na magazyn?**</span><span class="sxs-lookup"><span data-stu-id="1cdbb-165">**How many databases can I configure per day per vault?**</span></span>

<span data-ttu-id="1cdbb-166">Można skonfigurować 200 bazy danych dziennie na magazynie.</span><span class="sxs-lookup"><span data-stu-id="1cdbb-166">You can set up 200 databases per day per vault.</span></span>

<span data-ttu-id="1cdbb-167">**Długoterminowego przechowywania kopii zapasowych działa z pul elastycznych?**</span><span class="sxs-lookup"><span data-stu-id="1cdbb-167">**Does long-term backup retention work with elastic pools?**</span></span>

<span data-ttu-id="1cdbb-168">Tak.</span><span class="sxs-lookup"><span data-stu-id="1cdbb-168">Yes.</span></span> <span data-ttu-id="1cdbb-169">Wszystkie bazy danych w puli można skonfigurować za pomocą zasad przechowywania.</span><span class="sxs-lookup"><span data-stu-id="1cdbb-169">Any database in the pool can be configured with the retention policy.</span></span>

<span data-ttu-id="1cdbb-170">**Można wybrać czas, o której została utworzona kopia zapasowa?**</span><span class="sxs-lookup"><span data-stu-id="1cdbb-170">**Can I choose the time at which the backup is created?**</span></span>

<span data-ttu-id="1cdbb-171">Nie, baza danych SQL określa harmonogram tworzenia kopii zapasowych, aby zminimalizować wpływ na wydajność w bazach danych.</span><span class="sxs-lookup"><span data-stu-id="1cdbb-171">No, SQL Database controls the backup schedule to minimize the performance impact on your databases.</span></span>

<span data-ttu-id="1cdbb-172">**Masz przezroczystego szyfrowania danych włączone dla bazy danych. Można jej używać w magazynie?**</span><span class="sxs-lookup"><span data-stu-id="1cdbb-172">**I have transparent data encryption enabled for my database. Can I use it with the vault?**</span></span> 

<span data-ttu-id="1cdbb-173">Tak, przezroczystego szyfrowania danych jest obsługiwane.</span><span class="sxs-lookup"><span data-stu-id="1cdbb-173">Yes, transparent data encryption is supported.</span></span> <span data-ttu-id="1cdbb-174">Nawet jeśli oryginalnej bazy danych już nie istnieje, można przywrócić bazy danych z magazynu.</span><span class="sxs-lookup"><span data-stu-id="1cdbb-174">You can restore the database from the vault even if the original database no longer exists.</span></span>

<span data-ttu-id="1cdbb-175">**Co się stanie w przypadku kopii zapasowej w magazynie, jeśli Moja subskrypcja jest zawieszona?**</span><span class="sxs-lookup"><span data-stu-id="1cdbb-175">**What happens with the backups in the vault if my subscription is suspended?**</span></span> 

<span data-ttu-id="1cdbb-176">Jeśli subskrypcja jest zawieszona, możemy zachować istniejące bazy danych i kopii zapasowych.</span><span class="sxs-lookup"><span data-stu-id="1cdbb-176">If your subscription is suspended, we retain the existing databases and backups.</span></span> <span data-ttu-id="1cdbb-177">Nowe kopie zapasowe nie są kopiowane do magazynu.</span><span class="sxs-lookup"><span data-stu-id="1cdbb-177">New backups are not copied to the vault.</span></span> <span data-ttu-id="1cdbb-178">Po aktywowaniu subskrypcji usługi wznawia kopiowania do magazynu kopii zapasowych.</span><span class="sxs-lookup"><span data-stu-id="1cdbb-178">After you reactivate the subscription, the service resumes copying backups to the vault.</span></span> <span data-ttu-id="1cdbb-179">Magazyn staje się dostępny dla operacji przywracania przy użyciu kopii zapasowych, które zostały skopiowane przed subskrypcji zostało zawieszone.</span><span class="sxs-lookup"><span data-stu-id="1cdbb-179">Your vault becomes accessible to the restore operations by using the backups that were copied there before the subscription was suspended.</span></span> 

<span data-ttu-id="1cdbb-180">**Czy można uzyskać dostępu do plików kopii zapasowej bazy danych SQL, można pobrać lub przywrócić je do programu SQL server?**</span><span class="sxs-lookup"><span data-stu-id="1cdbb-180">**Can I get access to the SQL database backup files so I can download or restore them to the SQL server?**</span></span>

<span data-ttu-id="1cdbb-181">Nie, nie jest obecnie.</span><span class="sxs-lookup"><span data-stu-id="1cdbb-181">No, not currently.</span></span>

<span data-ttu-id="1cdbb-182">**Może mieć wielu harmonogramów (codziennie, co tydzień, co miesiąc, co rok) w ramach zasad przechowywania SQL.**</span><span class="sxs-lookup"><span data-stu-id="1cdbb-182">**Is it possible to have multiple schedules (daily, weekly, monthly, yearly) within a SQL retention policy.**</span></span>

<span data-ttu-id="1cdbb-183">Nie, wielu harmonogramów są obecnie dostępne tylko dla kopii zapasowych maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="1cdbb-183">No, multiple schedules are currently available only for virtual machine backups.</span></span>

<span data-ttu-id="1cdbb-184">**Co zrobić, jeśli skonfigurowanie długoterminowego przechowywania kopii zapasowych w bazie danych, która jest aktywna replikacja geograficzna dodatkowej bazy danych dla?**</span><span class="sxs-lookup"><span data-stu-id="1cdbb-184">**What if we set up long-term backup retention on a database that is an active geo-replication secondary database?**</span></span>

<span data-ttu-id="1cdbb-185">Ponieważ firma Microsoft nie wykonuj kopie zapasowe replik, nie ma opcja długoterminowego przechowywania kopii zapasowych z dodatkowej bazy danych.</span><span class="sxs-lookup"><span data-stu-id="1cdbb-185">Because we don't take backups on replicas, there is currently no option for long-term backup retention on secondary databases.</span></span> <span data-ttu-id="1cdbb-186">Jednak ważne jest, aby umożliwić użytkownikom konfigurowanie długoterminowego przechowywania kopii zapasowej w pomocniczej bazie danych aktywna replikacja geograficzna z tego względu:</span><span class="sxs-lookup"><span data-stu-id="1cdbb-186">However, it is important for users to set up long-term backup retention on an active geo-replication secondary database for these reasons:</span></span>
* <span data-ttu-id="1cdbb-187">Po przejściu w tryb failover wykonywany i baza danych będzie podstawowej bazy danych, możemy zająć pełnej kopii zapasowej, który zostanie przekazany do magazynu.</span><span class="sxs-lookup"><span data-stu-id="1cdbb-187">When a failover happens and the database becomes a primary database, we take a full backup, which is uploaded to vault.</span></span>
* <span data-ttu-id="1cdbb-188">Jest nie żadnymi dodatkowymi kosztami klientowi konfigurowania długoterminowego przechowywania kopii zapasowej w pomocniczej bazie danych.</span><span class="sxs-lookup"><span data-stu-id="1cdbb-188">There is no extra cost to the customer for setting up long-term backup retention on a secondary database.</span></span>

## <a name="next-steps"></a><span data-ttu-id="1cdbb-189">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="1cdbb-189">Next steps</span></span>
<span data-ttu-id="1cdbb-190">Ponieważ kopie zapasowe bazy danych ochronę danych przed przypadkowym uszkodzenia lub usunięcia, są one integralną część wszelkie ciągłość prowadzenia działalności biznesowej i strategii odzyskiwania po awarii.</span><span class="sxs-lookup"><span data-stu-id="1cdbb-190">Because database backups protect data from accidental corruption or deletion, they're an essential part of any business continuity and disaster recovery strategy.</span></span> <span data-ttu-id="1cdbb-191">Aby dowiedzieć się więcej o innych rozwiązań ciągłość prowadzenia działalności biznesowej bazy danych SQL, zobacz [omówienie ciągłości działalności biznesowej](sql-database-business-continuity.md).</span><span class="sxs-lookup"><span data-stu-id="1cdbb-191">To learn about the other SQL Database business-continuity solutions, see [Business continuity overview](sql-database-business-continuity.md).</span></span>
