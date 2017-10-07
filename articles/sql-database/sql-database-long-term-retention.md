---
title: kopie zapasowe bazy danych SQL Azure aaaStore dla zapasowej lat too10 | Dokumentacja firmy Microsoft
description: "Dowiedz się, jak baza danych SQL Azure obsługuje przechowywania kopii zapasowych na potrzeby się too10 lata."
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
ms.openlocfilehash: 5825ebd4e3bd66b59b13aea603d377ef814a1df3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="store-azure-sql-database-backups-for-up-too10-years"></a><span data-ttu-id="4829a-103">Przechowywanie kopii zapasowych bazy danych SQL Azure dla się too10 lat.</span><span class="sxs-lookup"><span data-stu-id="4829a-103">Store Azure SQL Database backups for up too10 years</span></span>
<span data-ttu-id="4829a-104">Wiele aplikacji ma przepisów prawnych, zgodności lub innych firm celów, które wymagają kopii zapasowych bazy danych tooretain poza hello 7 35 dni udostępniane przez usługi Azure SQL Database [automatycznego tworzenia kopii zapasowych](sql-database-automated-backups.md).</span><span class="sxs-lookup"><span data-stu-id="4829a-104">Many applications have regulatory, compliance, or other business purposes that require you tooretain database backups beyond hello 7-35 days provided by Azure SQL Database [automatic backups](sql-database-automated-backups.md).</span></span> <span data-ttu-id="4829a-105">Dzięki funkcji hello długoterminowego przechowywania kopii zapasowych, można przechowywać kopie zapasowe bazy danych SQL w magazynie usług odzyskiwania Azure dla zapasowej lat too10.</span><span class="sxs-lookup"><span data-stu-id="4829a-105">By using hello long-term backup retention feature, you can store your SQL database backups in an Azure Recovery Services vault for up too10 years.</span></span> <span data-ttu-id="4829a-106">Można przechowywać się too1, 000 baz danych na magazynie.</span><span class="sxs-lookup"><span data-stu-id="4829a-106">You can store up too1,000 databases per vault.</span></span> <span data-ttu-id="4829a-107">Następnie można wybrać jakiejkolwiek kopii zapasowej w toorestore magazynu hello go jako nową bazę danych.</span><span class="sxs-lookup"><span data-stu-id="4829a-107">You then can select any backup in hello vault toorestore it as a new database.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="4829a-108">Długoterminowego przechowywania kopii zapasowych jest obecnie w wersji zapoznawczej i jest dostępna w następujących regionach hello: Australia Wschodnia, Australia Południowo-Wschodnia, Brazylia Południowa, środkowe stany USA, Azja Wschodnia, wschodnie stany USA, wschodnie stany USA 2, Indie środkowe, Indie Południowe, Japonia Wschodnia, Japonia Zachodnia, północno-środkowe stany, Północna Europa, Południowej środkowe stany USA, Azja południowo-wschodnia, Europa Zachodnia i zachodnie stany USA</span><span class="sxs-lookup"><span data-stu-id="4829a-108">Long-term backup retention is currently in preview and available in hello following regions: Australia East, Australia Southeast, Brazil South, Central US, East Asia, East US, East US 2, India Central, India South, Japan East, Japan West, North Central US, North Europe, South Central US, Southeast Asia, West Europe, and West US.</span></span>
>

> [!NOTE]
> <span data-ttu-id="4829a-109">Można włączyć zapasową baz danych too200 na magazynu w okresie 24-godzinnym.</span><span class="sxs-lookup"><span data-stu-id="4829a-109">You can enable up too200 databases per vault during a 24-hour period.</span></span> <span data-ttu-id="4829a-110">Zalecane jest użycie oddzielnych magazynu dla każdego serwera toominimize hello skutków ten limit.</span><span class="sxs-lookup"><span data-stu-id="4829a-110">We recommend that you use a separate vault for each server toominimize hello impact of this limit.</span></span> 
> 

## <a name="how-sql-database-long-term-backup-retention-works"></a><span data-ttu-id="4829a-111">Jak działa długoterminowego przechowywania kopii zapasowych bazy danych SQL</span><span class="sxs-lookup"><span data-stu-id="4829a-111">How SQL Database long-term backup retention works</span></span>

<span data-ttu-id="4829a-112">Z długoterminowego przechowywania kopii zapasowych można skojarzyć serwer bazy danych SQL z magazynu usług odzyskiwania Azure.</span><span class="sxs-lookup"><span data-stu-id="4829a-112">With long-term backup retention, you can associate a SQL database server with an Azure Recovery Services vault.</span></span> 

* <span data-ttu-id="4829a-113">Należy utworzyć magazyn hello w hello tej samej subskrypcji platformy Azure, utworzony hello programu SQL server i w hello sam geograficzne regionu i grupie zasobów.</span><span class="sxs-lookup"><span data-stu-id="4829a-113">You must create hello vault in hello same Azure subscription that created hello SQL server and in hello same geographic region and resource group.</span></span> 
* <span data-ttu-id="4829a-114">Następnie skonfiguruj zasady przechowywania dla dowolnej bazy danych.</span><span class="sxs-lookup"><span data-stu-id="4829a-114">You then configure a retention policy for any database.</span></span> <span data-ttu-id="4829a-115">Hello zasad powoduje, że hello co tydzień pełną bazy danych kopii zapasowych toobe skopiowane toohello magazyn usług odzyskiwania i przechowywane przez okres przechowywania określony hello (up too10 lat).</span><span class="sxs-lookup"><span data-stu-id="4829a-115">hello policy causes hello weekly full database backups toobe copied toohello Recovery Services vault and retained for hello specified retention period (up too10 years).</span></span> 
* <span data-ttu-id="4829a-116">Następnie można przywrócić hello bazy danych z dowolnego z tych kopii zapasowych tooa nową bazę danych w dowolnego serwera w hello subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="4829a-116">You can then restore hello database from any of these backups tooa new database in any server in hello subscription.</span></span> <span data-ttu-id="4829a-117">Magazyn Azure tworzy kopię z istniejących kopii zapasowych i hello kopiowania nie ma wpływu wydajności na powitania istniejącej bazy danych.</span><span class="sxs-lookup"><span data-stu-id="4829a-117">Azure storage creates a copy from existing backups, and hello copy has no performance impact on hello existing database.</span></span>

> [!TIP]
> <span data-ttu-id="4829a-118">Aby tooguide instrukcje, zobacz [Konfigurowanie i przywrócenie z długoterminowego przechowywania kopii zapasowych bazy danych SQL Azure](sql-database-long-term-backup-retention-configure.md).</span><span class="sxs-lookup"><span data-stu-id="4829a-118">For a how-tooguide, see [Configure and restore from Azure SQL Database long-term backup retention](sql-database-long-term-backup-retention-configure.md).</span></span>

## <a name="enable-long-term-backup-retention"></a><span data-ttu-id="4829a-119">Włącz długoterminowego przechowywania kopii zapasowych</span><span class="sxs-lookup"><span data-stu-id="4829a-119">Enable long-term backup retention</span></span>

<span data-ttu-id="4829a-120">tooconfigure długoterminowego przechowywania kopii zapasowych bazy danych:</span><span class="sxs-lookup"><span data-stu-id="4829a-120">tooconfigure long-term backup retention for a database:</span></span>

1. <span data-ttu-id="4829a-121">Tworzenie magazynu usług odzyskiwania Azure w hello tego samego regionu, subskrypcji i zasobu grupy jako serwer bazy danych SQL.</span><span class="sxs-lookup"><span data-stu-id="4829a-121">Create an Azure Recovery Services vault in hello same region, subscription, and resource group as your SQL database server.</span></span> 
2. <span data-ttu-id="4829a-122">Zarejestruj powitania serwera toohello magazynu.</span><span class="sxs-lookup"><span data-stu-id="4829a-122">Register hello server toohello vault.</span></span>
3. <span data-ttu-id="4829a-123">Tworzenie zasad ochrony usług odzyskiwania Azure.</span><span class="sxs-lookup"><span data-stu-id="4829a-123">Create an Azure Recovery Services protection policy.</span></span>
4. <span data-ttu-id="4829a-124">Zastosuj hello ochrony zasad toohello baz danych, które wymagają długoterminowego przechowywania kopii zapasowych.</span><span class="sxs-lookup"><span data-stu-id="4829a-124">Apply hello protection policy toohello databases that require long-term backup retention.</span></span>

<span data-ttu-id="4829a-125">tooconfigure, zarządzać i Przywróć bazę danych z długoterminowego przechowywania kopii zapasowych automatycznych kopii zapasowych w magazynie usług odzyskiwania Azure, wykonaj jedną z następujących hello:</span><span class="sxs-lookup"><span data-stu-id="4829a-125">tooconfigure, manage, and restore a database from long-term backup retention of automated backups in an Azure Recovery Services vault, do either of hello following:</span></span>

* <span data-ttu-id="4829a-126">Przy użyciu hello portalu Azure: kliknij **długoterminowego przechowywania kopii zapasowych**, wybierz bazę danych, a następnie kliknij przycisk **Konfiguruj**.</span><span class="sxs-lookup"><span data-stu-id="4829a-126">Using hello Azure portal: Click **Long-term backup retention**, select a database, and then click **Configure**.</span></span> 

   ![Wybierz bazę danych do długoterminowego przechowywania kopii zapasowych](./media/sql-database-get-started-backup-recovery/select-database-for-long-term-backup-retention.png)

* <span data-ttu-id="4829a-128">Przy użyciu programu PowerShell: Przejdź zbyt[Konfigurowanie i przywrócenie z długoterminowego przechowywania kopii zapasowych bazy danych SQL Azure](sql-database-long-term-backup-retention-configure.md).</span><span class="sxs-lookup"><span data-stu-id="4829a-128">Using PowerShell: Go too[Configure and restore from Azure SQL Database long-term backup retention](sql-database-long-term-backup-retention-configure.md).</span></span>

## <a name="restore-a-database-thats-stored-with-hello-long-term-backup-retention-feature"></a><span data-ttu-id="4829a-129">Przywracanie bazy danych przechowywanym hello długoterminowego przechowywania kopii zapasowych funkcji</span><span class="sxs-lookup"><span data-stu-id="4829a-129">Restore a database that's stored with hello long-term backup retention feature</span></span>

<span data-ttu-id="4829a-130">toorecover z kopii zapasowej długoterminowego przechowywania kopii zapasowych:</span><span class="sxs-lookup"><span data-stu-id="4829a-130">toorecover from a long-term backup retention backup:</span></span>

1. <span data-ttu-id="4829a-131">Magazyn hello listy przechowywania hello kopii zapasowej.</span><span class="sxs-lookup"><span data-stu-id="4829a-131">List hello vault where hello backup is stored.</span></span>
2. <span data-ttu-id="4829a-132">Kontener hello listy jest mapowanych tooyour serwera logicznego.</span><span class="sxs-lookup"><span data-stu-id="4829a-132">List hello container that is mapped tooyour logical server.</span></span>
3. <span data-ttu-id="4829a-133">Listy hello źródła danych w ramach hello magazynu, który jest mapowanych tooyour bazy danych.</span><span class="sxs-lookup"><span data-stu-id="4829a-133">List hello data source within hello vault that is mapped tooyour database.</span></span>
4. <span data-ttu-id="4829a-134">Punkty odzyskiwania hello listy, które są dostępne toorestore.</span><span class="sxs-lookup"><span data-stu-id="4829a-134">List hello recovery points that are available toorestore.</span></span>
5. <span data-ttu-id="4829a-135">Przywracanie bazy danych hello z serwera docelowego toohello punktu odzyskiwania hello w ramach subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="4829a-135">Restore hello database from hello recovery point toohello target server within your subscription.</span></span>

<span data-ttu-id="4829a-136">tooconfigure, zarządzać i Przywróć bazę danych z długoterminowego przechowywania kopii zapasowych automatycznych kopii zapasowych w magazynie usług odzyskiwania Azure, wykonaj jedną z następujących hello:</span><span class="sxs-lookup"><span data-stu-id="4829a-136">tooconfigure, manage, and restore a database from long-term backup retention of automated backups in an Azure Recovery Services vault, do either of hello following:</span></span>

* <span data-ttu-id="4829a-137">Przy użyciu hello portalu Azure: Przejdź zbyt[Zarządzaj długoterminowego przechowywania kopii zapasowych użyciu hello portalu Azure](sql-database-long-term-backup-retention-configure.md).</span><span class="sxs-lookup"><span data-stu-id="4829a-137">Using hello Azure portal: Go too[Manage long-term backup retention using hello Azure portal](sql-database-long-term-backup-retention-configure.md).</span></span> 

* <span data-ttu-id="4829a-138">Przy użyciu programu PowerShell: Przejdź zbyt[Zarządzanie długoterminowego przechowywania kopii zapasowych przy użyciu programu PowerShell](sql-database-long-term-backup-retention-configure.md).</span><span class="sxs-lookup"><span data-stu-id="4829a-138">Using PowerShell: Go too[Manage long-term backup retention using PowerShell](sql-database-long-term-backup-retention-configure.md).</span></span>

## <a name="get-pricing-for-long-term-backup-retention"></a><span data-ttu-id="4829a-139">Pobierz ceny dla długoterminowego przechowywania kopii zapasowych</span><span class="sxs-lookup"><span data-stu-id="4829a-139">Get pricing for long-term backup retention</span></span>

<span data-ttu-id="4829a-140">Długoterminowego przechowywania kopii zapasowych bazy danych SQL jest rozliczana zgodnie z toohello [usługi kopii zapasowej Azure cennik stawki](https://azure.microsoft.com/pricing/details/backup/).</span><span class="sxs-lookup"><span data-stu-id="4829a-140">Long-term backup retention of a SQL database is charged according toohello [Azure backup services pricing rates](https://azure.microsoft.com/pricing/details/backup/).</span></span>

<span data-ttu-id="4829a-141">Serwer bazy danych SQL powitania po zarejestrowanych toohello magazynu są naliczane opłaty za hello całkowita ilość miejsca, który jest używany przez cotygodniowe kopie zapasowe hello przechowywane w magazynie hello.</span><span class="sxs-lookup"><span data-stu-id="4829a-141">After hello SQL database server is registered toohello vault, you are charged for hello total storage that's used by hello weekly backups stored in hello vault.</span></span>

## <a name="view-available-backups-that-are-stored-in-long-term-backup-retention"></a><span data-ttu-id="4829a-142">Wyświetl dostępne kopie zapasowe, które są przechowywane w długoterminowego przechowywania kopii zapasowych</span><span class="sxs-lookup"><span data-stu-id="4829a-142">View available backups that are stored in long-term backup retention</span></span>

<span data-ttu-id="4829a-143">tooconfigure, zarządzać i Przywróć bazę danych z długoterminowego przechowywania kopii zapasowych automatycznych kopii zapasowych w magazynie usług odzyskiwania Azure przy użyciu hello portalu Azure, wykonaj jedną z następujących hello:</span><span class="sxs-lookup"><span data-stu-id="4829a-143">tooconfigure, manage, and restore a database from long-term backup retention of automated backups in an Azure Recovery Services vault by using hello Azure portal, do either of hello following:</span></span>

* <span data-ttu-id="4829a-144">Przy użyciu hello portalu Azure: Przejdź zbyt[Zarządzaj długoterminowego przechowywania kopii zapasowych użyciu hello portalu Azure](sql-database-long-term-backup-retention-configure.md).</span><span class="sxs-lookup"><span data-stu-id="4829a-144">Using hello Azure portal: Go too[Manage long-term backup retention using hello Azure portal](sql-database-long-term-backup-retention-configure.md).</span></span> 

* <span data-ttu-id="4829a-145">Przy użyciu programu PowerShell: Przejdź zbyt[Zarządzanie długoterminowego przechowywania kopii zapasowych przy użyciu programu PowerShell](sql-database-long-term-backup-retention-configure.md).</span><span class="sxs-lookup"><span data-stu-id="4829a-145">Using PowerShell: Go too[Manage long-term backup retention using PowerShell](sql-database-long-term-backup-retention-configure.md).</span></span>

## <a name="disable-long-term-retention"></a><span data-ttu-id="4829a-146">Wyłącz długoterminowego przechowywania</span><span class="sxs-lookup"><span data-stu-id="4829a-146">Disable long-term retention</span></span>

<span data-ttu-id="4829a-147">usługi odzyskiwania Hello automatycznie obsługuje oczyszczania hello oparte na powitania podane zasady przechowywania kopii zapasowych.</span><span class="sxs-lookup"><span data-stu-id="4829a-147">hello recovery service automatically handles hello cleanup of backups based on hello provided retention policy.</span></span> 

<span data-ttu-id="4829a-148">toostop wysyłania hello kopii zapasowych dla określonej bazy danych magazynu toohello, Usuń hello zasad przechowywania dla tej bazy danych.</span><span class="sxs-lookup"><span data-stu-id="4829a-148">toostop sending hello backups for a specific database toohello vault, remove hello retention policy for that database.</span></span>
  
```
Set-AzureRmSqlDatabaseBackupLongTermRetentionPolicy -ResourceGroupName 'RG1' -ServerName 'Server1' -DatabaseName 'DB1' -State 'Disabled' -ResourceId $policy.Id
```

> [!NOTE]
> <span data-ttu-id="4829a-149">nie dotyczy to Hello kopii zapasowych, które są już w magazynie hello.</span><span class="sxs-lookup"><span data-stu-id="4829a-149">hello backups that are already in hello vault are unaffected.</span></span> <span data-ttu-id="4829a-150">Są one automatycznie usuwane przez hello usługi odzyskiwania po wygaśnięciu okresu przechowywania.</span><span class="sxs-lookup"><span data-stu-id="4829a-150">They are automatically deleted by hello recovery service when their retention period expires.</span></span>

## <a name="long-term-backup-retention-faq"></a><span data-ttu-id="4829a-151">Długoterminowego przechowywania kopii zapasowych — często zadawane pytania</span><span class="sxs-lookup"><span data-stu-id="4829a-151">Long-term backup retention FAQ</span></span>

<span data-ttu-id="4829a-152">**Można ręcznie usunąć z określonych kopii zapasowych w magazynie hello?**</span><span class="sxs-lookup"><span data-stu-id="4829a-152">**Can I manually delete specific backups in hello vault?**</span></span>

<span data-ttu-id="4829a-153">Nie można obecnie.</span><span class="sxs-lookup"><span data-stu-id="4829a-153">Not currently.</span></span> <span data-ttu-id="4829a-154">Magazyn Hello automatycznie oczyszcza kopii zapasowych, po zakończeniu okresu przechowywania hello.</span><span class="sxs-lookup"><span data-stu-id="4829a-154">hello vault automatically cleans up backups when hello retention period has expired.</span></span>

<span data-ttu-id="4829a-155">**Można zarejestrować Mój serwer toostore kopii zapasowych toomore niż jeden Magazyn?**</span><span class="sxs-lookup"><span data-stu-id="4829a-155">**Can I register my server toostore backups toomore than one vault?**</span></span>

<span data-ttu-id="4829a-156">Nie, obecnie można przechowywać kopie zapasowe tooonly jeden magazyn naraz.</span><span class="sxs-lookup"><span data-stu-id="4829a-156">No, you can currently store backups tooonly one vault at a time.</span></span>

<span data-ttu-id="4829a-157">**W ramach różnych subskrypcji może mieć magazyn i serwera?**</span><span class="sxs-lookup"><span data-stu-id="4829a-157">**Can I have a vault and server in different subscriptions?**</span></span>

<span data-ttu-id="4829a-158">Nie, obecnie hello magazynu i serwer muszą być w hello tej samej subskrypcji i grupie zasobów.</span><span class="sxs-lookup"><span data-stu-id="4829a-158">No, currently hello vault and server must be in hello same subscription and resource group.</span></span>

<span data-ttu-id="4829a-159">**Można użyć magazynu, który został utworzony w regionie, który jest inny niż region Mój serwer?**</span><span class="sxs-lookup"><span data-stu-id="4829a-159">**Can I use a vault that I created in a region that's different from my server’s region?**</span></span>

<span data-ttu-id="4829a-160">Nie, hello magazynu i serwer muszą być w hello tego samego regionu toominimize skopiuj czasu i zapobiec zmianom ruchu.</span><span class="sxs-lookup"><span data-stu-id="4829a-160">No, hello vault and server must be in hello same region toominimize copy time and avoid traffic charges.</span></span>

<span data-ttu-id="4829a-161">**Jak wiele baz danych można przechowywać w jednym magazynie?**</span><span class="sxs-lookup"><span data-stu-id="4829a-161">**How many databases can I store in one vault?**</span></span>

<span data-ttu-id="4829a-162">Obecnie firma Microsoft obsługuje konto too1, 000 baz danych na magazynie.</span><span class="sxs-lookup"><span data-stu-id="4829a-162">Currently, we support up too1,000 databases per vault.</span></span> 

<span data-ttu-id="4829a-163">**Jak wiele magazynów można utworzyć na subskrypcję?**</span><span class="sxs-lookup"><span data-stu-id="4829a-163">**How many vaults can I create per subscription?**</span></span>

<span data-ttu-id="4829a-164">Możesz utworzyć zapasową magazynów too25 na subskrypcję.</span><span class="sxs-lookup"><span data-stu-id="4829a-164">You can create up too25 vaults per subscription.</span></span>

<span data-ttu-id="4829a-165">**Jak wiele baz danych można skonfigurować na dzień na magazyn?**</span><span class="sxs-lookup"><span data-stu-id="4829a-165">**How many databases can I configure per day per vault?**</span></span>

<span data-ttu-id="4829a-166">Można skonfigurować 200 bazy danych dziennie na magazynie.</span><span class="sxs-lookup"><span data-stu-id="4829a-166">You can set up 200 databases per day per vault.</span></span>

<span data-ttu-id="4829a-167">**Długoterminowego przechowywania kopii zapasowych działa z pul elastycznych?**</span><span class="sxs-lookup"><span data-stu-id="4829a-167">**Does long-term backup retention work with elastic pools?**</span></span>

<span data-ttu-id="4829a-168">Tak.</span><span class="sxs-lookup"><span data-stu-id="4829a-168">Yes.</span></span> <span data-ttu-id="4829a-169">Wszystkie bazy danych w puli hello można skonfigurować za pomocą zasad przechowywania hello.</span><span class="sxs-lookup"><span data-stu-id="4829a-169">Any database in hello pool can be configured with hello retention policy.</span></span>

<span data-ttu-id="4829a-170">**Można wybrać hello czas, o której została utworzona kopia zapasowa hello?**</span><span class="sxs-lookup"><span data-stu-id="4829a-170">**Can I choose hello time at which hello backup is created?**</span></span>

<span data-ttu-id="4829a-171">Nie, baza danych SQL steruje hello harmonogram tworzenia kopii zapasowych toominimize hello wpływ na wydajność w bazach danych.</span><span class="sxs-lookup"><span data-stu-id="4829a-171">No, SQL Database controls hello backup schedule toominimize hello performance impact on your databases.</span></span>

<span data-ttu-id="4829a-172">**Masz przezroczystego szyfrowania danych włączone dla bazy danych. Można jej używać z magazynem hello?**</span><span class="sxs-lookup"><span data-stu-id="4829a-172">**I have transparent data encryption enabled for my database. Can I use it with hello vault?**</span></span> 

<span data-ttu-id="4829a-173">Tak, przezroczystego szyfrowania danych jest obsługiwane.</span><span class="sxs-lookup"><span data-stu-id="4829a-173">Yes, transparent data encryption is supported.</span></span> <span data-ttu-id="4829a-174">Można przywrócić hello bazy danych z magazynu hello, nawet jeśli hello oryginalnej bazy danych już nie istnieje.</span><span class="sxs-lookup"><span data-stu-id="4829a-174">You can restore hello database from hello vault even if hello original database no longer exists.</span></span>

<span data-ttu-id="4829a-175">**Co się stanie w przypadku kopii zapasowej hello w magazynie hello Jeśli Moja subskrypcja jest zawieszona?**</span><span class="sxs-lookup"><span data-stu-id="4829a-175">**What happens with hello backups in hello vault if my subscription is suspended?**</span></span> 

<span data-ttu-id="4829a-176">Jeśli subskrypcja jest zawieszona, firma Microsoft przechowywała hello istniejących baz danych i tworzenie kopii zapasowych.</span><span class="sxs-lookup"><span data-stu-id="4829a-176">If your subscription is suspended, we retain hello existing databases and backups.</span></span> <span data-ttu-id="4829a-177">Nowe kopie zapasowe nie są toohello skopiowanych magazynu.</span><span class="sxs-lookup"><span data-stu-id="4829a-177">New backups are not copied toohello vault.</span></span> <span data-ttu-id="4829a-178">Po aktywowaniu hello subskrypcji usługi hello wznawia kopiowanie magazynu toohello kopii zapasowych.</span><span class="sxs-lookup"><span data-stu-id="4829a-178">After you reactivate hello subscription, hello service resumes copying backups toohello vault.</span></span> <span data-ttu-id="4829a-179">Magazyn staje się dostępny toohello operacje przywracania przy użyciu kopii zapasowych hello, które zostały skopiowane przed hello subskrypcja została zawieszona.</span><span class="sxs-lookup"><span data-stu-id="4829a-179">Your vault becomes accessible toohello restore operations by using hello backups that were copied there before hello subscription was suspended.</span></span> 

<span data-ttu-id="4829a-180">**Można uzyskać dostępu do plików kopii zapasowej bazy danych SQL toohello, można pobrać lub je przywrócić toohello programu SQL server?**</span><span class="sxs-lookup"><span data-stu-id="4829a-180">**Can I get access toohello SQL database backup files so I can download or restore them toohello SQL server?**</span></span>

<span data-ttu-id="4829a-181">Nie, nie jest obecnie.</span><span class="sxs-lookup"><span data-stu-id="4829a-181">No, not currently.</span></span>

<span data-ttu-id="4829a-182">**Jest to możliwe toohave wielu harmonogramów (codziennie, co tydzień, co miesiąc, co rok) w ramach zasad przechowywania SQL.**</span><span class="sxs-lookup"><span data-stu-id="4829a-182">**Is it possible toohave multiple schedules (daily, weekly, monthly, yearly) within a SQL retention policy.**</span></span>

<span data-ttu-id="4829a-183">Nie, wielu harmonogramów są obecnie dostępne tylko dla kopii zapasowych maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="4829a-183">No, multiple schedules are currently available only for virtual machine backups.</span></span>

<span data-ttu-id="4829a-184">**Co zrobić, jeśli skonfigurowanie długoterminowego przechowywania kopii zapasowych w bazie danych, która jest aktywna replikacja geograficzna dodatkowej bazy danych dla?**</span><span class="sxs-lookup"><span data-stu-id="4829a-184">**What if we set up long-term backup retention on a database that is an active geo-replication secondary database?**</span></span>

<span data-ttu-id="4829a-185">Ponieważ firma Microsoft nie wykonuj kopie zapasowe replik, nie ma opcja długoterminowego przechowywania kopii zapasowych z dodatkowej bazy danych.</span><span class="sxs-lookup"><span data-stu-id="4829a-185">Because we don't take backups on replicas, there is currently no option for long-term backup retention on secondary databases.</span></span> <span data-ttu-id="4829a-186">Jednak ważne jest dla użytkowników tooset się długoterminowego przechowywania kopii zapasowej w pomocniczej bazie danych aktywna replikacja geograficzna tych powodów:</span><span class="sxs-lookup"><span data-stu-id="4829a-186">However, it is important for users tooset up long-term backup retention on an active geo-replication secondary database for these reasons:</span></span>
* <span data-ttu-id="4829a-187">Po przejściu w tryb failover wykonywany i bazy danych hello staje się podstawowej bazy danych, traktujemy pełnej kopii zapasowej, który jest toovault przekazane.</span><span class="sxs-lookup"><span data-stu-id="4829a-187">When a failover happens and hello database becomes a primary database, we take a full backup, which is uploaded toovault.</span></span>
* <span data-ttu-id="4829a-188">Nie istnieje bez dodatkowych kosztów toohello odbiorcy do definiowania długoterminowego przechowywania kopii zapasowej w pomocniczej bazie danych.</span><span class="sxs-lookup"><span data-stu-id="4829a-188">There is no extra cost toohello customer for setting up long-term backup retention on a secondary database.</span></span>

## <a name="next-steps"></a><span data-ttu-id="4829a-189">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="4829a-189">Next steps</span></span>
<span data-ttu-id="4829a-190">Ponieważ kopie zapasowe bazy danych ochronę danych przed przypadkowym uszkodzenia lub usunięcia, są one integralną część wszelkie ciągłość prowadzenia działalności biznesowej i strategii odzyskiwania po awarii.</span><span class="sxs-lookup"><span data-stu-id="4829a-190">Because database backups protect data from accidental corruption or deletion, they're an essential part of any business continuity and disaster recovery strategy.</span></span> <span data-ttu-id="4829a-191">toolearn około hello innych rozwiązań ciągłość prowadzenia działalności biznesowej bazy danych SQL, zobacz [omówienie ciągłości działalności biznesowej](sql-database-business-continuity.md).</span><span class="sxs-lookup"><span data-stu-id="4829a-191">toolearn about hello other SQL Database business-continuity solutions, see [Business continuity overview](sql-database-business-continuity.md).</span></span>
