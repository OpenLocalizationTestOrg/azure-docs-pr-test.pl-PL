---
title: "Skonfiguruj długoterminowego przechowywania kopii zapasowych — usługa Azure SQL database | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toostore automatyczne kopie zapasowe w powitalne magazyn usług odzyskiwania Azure i magazyn usług odzyskiwania Azure toorestore z hello"
services: sql-database
documentationcenter: 
author: CarlRabeler
manager: jhubbard
editor: 
ms.assetid: aeb8c4c3-6ae2-45f7-b2c3-fa13e3752eed
ms.service: sql-database
ms.custom: business continuity
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/10/2017
ms.author: carlrab
ms.openlocfilehash: 603f4dd21cee4407d46f749655aba8f9ef3322c0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="configure-and-restore-from-azure-sql-database-long-term-backup-retention"></a><span data-ttu-id="01314-103">Konfigurowanie i Przywróć z długoterminowego przechowywania kopii zapasowych bazy danych SQL Azure</span><span class="sxs-lookup"><span data-stu-id="01314-103">Configure and restore from Azure SQL Database long-term backup retention</span></span>

<span data-ttu-id="01314-104">Można skonfigurować tworzenia kopii zapasowych bazy danych Azure SQL toostore programu hello usług odzyskiwania Azure magazynu, a następnie Odzyskaj przechowywane za pomocą kopii zapasowej bazy danych za pomocą magazynu hello hello portalu Azure lub programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="01314-104">You can configure hello Azure Recovery Services vault toostore Azure SQL database backups and then recover a database using backups retained in hello vault using hello Azure portal or PowerShell.</span></span>

## <a name="azure-portal"></a><span data-ttu-id="01314-105">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="01314-105">Azure portal</span></span>

<span data-ttu-id="01314-106">następujące sekcje Pokaż jak magazyn toouse hello Azure tooconfigure portalu hello usług odzyskiwania Azure, wyświetlanie kopii zapasowych w magazynie hello i Przywróć z magazynu hello Hello.</span><span class="sxs-lookup"><span data-stu-id="01314-106">hello following sections show you how toouse hello Azure portal tooconfigure hello Azure Recovery Services vault, view backups in hello vault, and restore from hello vault.</span></span>

### <a name="configure-hello-vault-register-hello-server-and-select-databases"></a><span data-ttu-id="01314-107">Konfigurowanie magazynu hello, Zarejestruj serwer hello i wybrać bazy danych</span><span class="sxs-lookup"><span data-stu-id="01314-107">Configure hello vault, register hello server, and select databases</span></span>

<span data-ttu-id="01314-108">Możesz [skonfigurowania kopii zapasowych tooretain automatycznego magazyn usług odzyskiwania Azure](sql-database-long-term-retention.md) przez okres dłuższy niż okres przechowywania hello warstwę usług.</span><span class="sxs-lookup"><span data-stu-id="01314-108">You [configure an Azure Recovery Services vault tooretain automated backups](sql-database-long-term-retention.md) for a period longer than hello retention period for your service tier.</span></span> 

1. <span data-ttu-id="01314-109">Otwórz hello **programu SQL Server** strony serwera.</span><span class="sxs-lookup"><span data-stu-id="01314-109">Open hello **SQL Server** page for your server.</span></span>

   ![Strona serwera SQL](./media/sql-database-get-started-portal/sql-server-blade.png)

2. <span data-ttu-id="01314-111">Kliknij pozycję **Długoterminowe przechowywanie kopii zapasowych**.</span><span class="sxs-lookup"><span data-stu-id="01314-111">Click **Long-term backup retention**.</span></span>

   ![link długoterminowego przechowywania kopii zapasowych](./media/sql-database-get-started-backup-recovery/long-term-backup-retention-link.png)

3. <span data-ttu-id="01314-113">Na powitania **długoterminowego przechowywania kopii zapasowych** serwera Przejrzyj i zaakceptuj warunki Podgląd hello (chyba że użytkownik jeszcze - lub ta funkcja nie jest już w wersji zapoznawczej).</span><span class="sxs-lookup"><span data-stu-id="01314-113">On hello **Long-term backup retention** page for your server, review and accept hello preview terms (unless you have already done so - or this feature is no longer in preview).</span></span>

   ![Zaakceptuj postanowienia Podgląd hello](./media/sql-database-get-started-backup-recovery/accept-the-preview-terms.png)

4. <span data-ttu-id="01314-115">Wybierz tę bazę danych w siatce hello tooconfigure długoterminowego przechowywania kopii zapasowych, a następnie kliknij przycisk **Konfigurowanie** na powitania narzędzi.</span><span class="sxs-lookup"><span data-stu-id="01314-115">tooconfigure long-term backup retention, select that database in hello grid and then click **Configure** on hello toolbar.</span></span>

   ![wybieranie bazy danych do długoterminowego przechowywania kopii zapasowych](./media/sql-database-get-started-backup-recovery/select-database-for-long-term-backup-retention.png)

5. <span data-ttu-id="01314-117">Na powitania **Konfiguruj** kliknij przycisk **Skonfiguruj wymagane ustawienia** w obszarze **magazyn usług odzyskiwania**.</span><span class="sxs-lookup"><span data-stu-id="01314-117">On hello **Configure** page, click **Configure required settings** under **Recovery service vault**.</span></span>

   ![konfigurowanie linku do magazynu](./media/sql-database-get-started-backup-recovery/configure-vault-link.png)

6. <span data-ttu-id="01314-119">Na powitania **magazyn usług odzyskiwania** wybierz istniejącego magazynu, jeśli istnieje.</span><span class="sxs-lookup"><span data-stu-id="01314-119">On hello **Recovery services vault** page, select an existing vault, if any.</span></span> <span data-ttu-id="01314-120">W przeciwnym razie jeśli nie znaleziono dla Twojej subskrypcji magazynu usług odzyskiwania, kliknij tooexit hello przepływu i Tworzenie magazynu usług odzyskiwania.</span><span class="sxs-lookup"><span data-stu-id="01314-120">Otherwise, if no recovery services vault found for your subscription, click tooexit hello flow and create a recovery services vault.</span></span>

   ![Utwórz łącze do magazynu](./media/sql-database-get-started-backup-recovery/create-new-vault-link.png)

7. <span data-ttu-id="01314-122">Na powitania **Magazyny usług odzyskiwania** kliknij przycisk **Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="01314-122">On hello **Recovery Services vaults** page, click **Add**.</span></span>

   ![Dodawanie linku do magazynu](./media/sql-database-get-started-backup-recovery/add-new-vault-link.png)
   
8. <span data-ttu-id="01314-124">Na powitania **magazyn usług odzyskiwania** dla magazyn usług odzyskiwania hello, podaj prawidłową nazwę.</span><span class="sxs-lookup"><span data-stu-id="01314-124">On hello **Recovery Services vault** page, provide a valid name for hello Recovery Services vault.</span></span>

   ![nazwa nowego magazynu](./media/sql-database-get-started-backup-recovery/new-vault-name.png)

9. <span data-ttu-id="01314-126">Wybierz subskrypcji i grupy zasobów, a następnie wybierz lokalizację hello hello magazynu.</span><span class="sxs-lookup"><span data-stu-id="01314-126">Select your subscription and resource group, and then select hello location for hello vault.</span></span> <span data-ttu-id="01314-127">Gdy skończysz, kliknij pozycję **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="01314-127">When done, click **Create**.</span></span>

   ![Tworzenie magazynu](./media/sql-database-get-started-backup-recovery/create-new-vault.png)

   > [!IMPORTANT]
   > <span data-ttu-id="01314-129">Magazyn Hello musi znajdować się w hello na tym samym regionie co serwer logiczny Azure SQL hello i musi Użyj hello sam grupie zasobów co powitania serwera logicznego.</span><span class="sxs-lookup"><span data-stu-id="01314-129">hello vault must be located in hello same region as hello Azure SQL logical server, and must use hello same resource group as hello logical server.</span></span>
   >

10. <span data-ttu-id="01314-130">Po utworzeniu hello nowy magazyn, należy wykonać hello niezbędne kroki tooreturn toohello **magazyn usług odzyskiwania** strony.</span><span class="sxs-lookup"><span data-stu-id="01314-130">After hello new vault is created, execute hello necessary steps tooreturn toohello **Recovery services vault** page.</span></span>

11. <span data-ttu-id="01314-131">Na powitania **magazyn usług odzyskiwania** strony, kliknij przycisk hello magazynu, a następnie kliknij przycisk **wybierz**.</span><span class="sxs-lookup"><span data-stu-id="01314-131">On hello **Recovery services vault** page, click hello vault and then click **Select**.</span></span>

   ![wybieranie istniejącego magazynu](./media/sql-database-get-started-backup-recovery/select-existing-vault.png)

12. <span data-ttu-id="01314-133">Na powitania **Konfiguruj** , podaj prawidłową nazwę dla nowych zasad przechowywania hello, zmodyfikuj zasady przechowywania domyślne hello zależnie od potrzeb, a następnie kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="01314-133">On hello **Configure** page, provide a valid name for hello new retention policy, modify hello default retention policy as appropriate, and then click **OK**.</span></span>

   ![definiowanie zasad przechowywania](./media/sql-database-get-started-backup-recovery/define-retention-policy.png)

13. <span data-ttu-id="01314-135">Na powitania **długoterminowego przechowywania kopii zapasowych** stron dla bazy danych, kliknij przycisk **zapisać** , a następnie kliknij przycisk **OK** tooapply hello tooall zasad przechowywania kopii zapasowych, długoterminowe wybrane bazy danych.</span><span class="sxs-lookup"><span data-stu-id="01314-135">On hello **Long-term backup retention** page for your database, click **Save** and then click **OK** tooapply hello long-term backup retention policy tooall selected databases.</span></span>

   ![definiowanie zasad przechowywania](./media/sql-database-get-started-backup-recovery/save-retention-policy.png)

14. <span data-ttu-id="01314-137">Kliknij przycisk **zapisać** tooenable długoterminowego przechowywania kopii zapasowych za pomocą tego nowego skonfigurowany magazyn usług odzyskiwania Azure toohello zasad.</span><span class="sxs-lookup"><span data-stu-id="01314-137">Click **Save** tooenable long-term backup retention using this new policy toohello Azure Recovery Services vault that you configured.</span></span>

   ![definiowanie zasad przechowywania](./media/sql-database-get-started-backup-recovery/enable-long-term-retention.png)

> [!IMPORTANT]
> <span data-ttu-id="01314-139">Po skonfigurowaniu kopii zapasowych są wyświetlane w magazynie hello w ciągu najbliższych siedmiu dni.</span><span class="sxs-lookup"><span data-stu-id="01314-139">Once configured, backups show up in hello vault within next seven days.</span></span> <span data-ttu-id="01314-140">W tym samouczku nie należy kontynuować, aż do tworzenia kopii zapasowych pojawiają się w magazynie hello.</span><span class="sxs-lookup"><span data-stu-id="01314-140">Do not continue this tutorial until backups show up in hello vault.</span></span>
>

### <a name="view-backups-in-long-term-retention-using-azure-portal"></a><span data-ttu-id="01314-141">Wyświetl kopie zapasowe w przechowywania długoterminowego za pomocą portalu Azure</span><span class="sxs-lookup"><span data-stu-id="01314-141">View backups in long-term retention using Azure portal</span></span>

<span data-ttu-id="01314-142">Wyświetl informacje o kopii zapasowych bazy danych w [długoterminowego przechowywania kopii zapasowych](sql-database-long-term-retention.md).</span><span class="sxs-lookup"><span data-stu-id="01314-142">View information about your database backups in [long-term backup retention](sql-database-long-term-retention.md).</span></span> 

1. <span data-ttu-id="01314-143">W portalu Azure Witaj, Otwórz magazyn usług odzyskiwania Azure na kopie zapasowe bazy danych (Przejdź zbyt**wszystkie zasoby** i wybierz ją z listy hello zasobów dla Twojej subskrypcji) tooview hello ilość Magazyn używany przez bazę danych Tworzenie kopii zapasowych w magazynie hello.</span><span class="sxs-lookup"><span data-stu-id="01314-143">In hello Azure portal, open your Azure Recovery Services vault for your database backups (go too**All resources** and select it from hello list of resources for your subscription) tooview hello amount of storage used by your database backups in hello vault.</span></span>

   ![wyświetlanie magazynu usługi recovery services z kopiami zapasowymi](./media/sql-database-get-started-backup-recovery/view-recovery-services-vault-with-data.png)

2. <span data-ttu-id="01314-145">Otwórz hello **bazy danych SQL** stron dla bazy danych.</span><span class="sxs-lookup"><span data-stu-id="01314-145">Open hello **SQL database** page for your database.</span></span>

   ![Nowa strona bazy danych przykładowych](./media/sql-database-get-started-portal/new-sample-db-blade.png)

3. <span data-ttu-id="01314-147">Na pasku narzędzi hello, kliknij przycisk **przywrócić**.</span><span class="sxs-lookup"><span data-stu-id="01314-147">On hello toolbar, click **Restore**.</span></span>

   ![pasek narzędzi przywracania](./media/sql-database-get-started-backup-recovery/restore-toolbar.png)

4. <span data-ttu-id="01314-149">Na stronie powitania przywracania kliknij **długoterminowej**.</span><span class="sxs-lookup"><span data-stu-id="01314-149">On hello Restore page, click **Long-term**.</span></span>

5. <span data-ttu-id="01314-150">W obszarze kopii zapasowych magazynu Azure, kliknij **Wybierz kopię zapasową** tooview kopii zapasowych bazy danych dostępności hello w długoterminowego przechowywania kopii zapasowych.</span><span class="sxs-lookup"><span data-stu-id="01314-150">Under Azure vault backups, click **Select a backup** tooview hello available database backups in long-term backup retention.</span></span>

   ![kopie zapasowe w magazynie](./media/sql-database-get-started-backup-recovery/view-backups-in-vault.png)

### <a name="restore-a-database-from-a-backup-in-long-term-backup-retention-using-hello-azure-portal"></a><span data-ttu-id="01314-152">Przywracanie bazy danych z kopii zapasowej w długoterminowego przechowywania kopii zapasowych za pomocą hello portalu Azure</span><span class="sxs-lookup"><span data-stu-id="01314-152">Restore a database from a backup in long-term backup retention using hello Azure portal</span></span>

<span data-ttu-id="01314-153">Witaj tooa nowe baza danych jest przywrócenie z kopii zapasowej w powitalne magazyn usług odzyskiwania Azure.</span><span class="sxs-lookup"><span data-stu-id="01314-153">You restore hello database tooa new database from a backup in hello Azure Recovery Services vault.</span></span>

1. <span data-ttu-id="01314-154">Na powitania **kopii zapasowych magazynu Azure** strony, kliknij przycisk hello toorestore kopii zapasowej, a następnie kliknij przycisk **wybierz**.</span><span class="sxs-lookup"><span data-stu-id="01314-154">On hello **Azure vault backups** page, click hello backup toorestore and then click **Select**.</span></span>

   ![wybieranie kopii zapasowej w magazynie](./media/sql-database-get-started-backup-recovery/select-backup-in-vault.png)

2. <span data-ttu-id="01314-156">W hello **Nazwa bazy danych** tekst Podaj nazwę hello hello przywrócić bazy danych.</span><span class="sxs-lookup"><span data-stu-id="01314-156">In hello **Database name** text box, provide hello name for hello restored database.</span></span>

   ![nazwa nowej nazwy danych](./media/sql-database-get-started-backup-recovery/new-database-name.png)

3. <span data-ttu-id="01314-158">Kliknij przycisk **OK** toorestore bazy danych z kopii zapasowej hello hello magazynu toohello nowej bazy danych.</span><span class="sxs-lookup"><span data-stu-id="01314-158">Click **OK** toorestore your database from hello backup in hello vault toohello new database.</span></span>

4. <span data-ttu-id="01314-159">Na pasku narzędzi hello kliknij przycisk Stan ikony powiadomień hello hello tooview hello zadania przywracania.</span><span class="sxs-lookup"><span data-stu-id="01314-159">On hello toolbar, click hello notification icon tooview hello status of hello restore job.</span></span>

   ![postęp zadania przywracania z magazynu](./media/sql-database-get-started-backup-recovery/restore-job-progress-long-term.png)

5. <span data-ttu-id="01314-161">Po zakończeniu zadania przywracania hello Otwórz hello **baz danych SQL** strony tooview hello nowo przywrócone w bazie danych.</span><span class="sxs-lookup"><span data-stu-id="01314-161">When hello restore job is completed, open hello **SQL databases** page tooview hello newly restored database.</span></span>

   ![baza danych przywrócona z magazynu](./media/sql-database-get-started-backup-recovery/restored-database-from-vault.png)

> [!NOTE]
> <span data-ttu-id="01314-163">W tym miejscu możesz połączyć toohello przywrócić bazy danych przy użyciu programu SQL Server Management Studio tooperform wymagane zadania, takie jak zbyt[wyodrębniania do istniejącej bazy danych hello lub istniejące hello toodelete hello przywrócić bazy danych toocopy bit danych Nazwa bazy danych bazy danych i Zmień nazwę hello przywrócić bazy danych toohello istniejących](sql-database-recovery-using-backups.md#point-in-time-restore).</span><span class="sxs-lookup"><span data-stu-id="01314-163">From here, you can connect toohello restored database using SQL Server Management Studio tooperform needed tasks, such as too[extract a bit of data from hello restored database toocopy into hello existing database or toodelete hello existing database and rename hello restored database toohello existing database name](sql-database-recovery-using-backups.md#point-in-time-restore).</span></span>
>

## <a name="powershell"></a><span data-ttu-id="01314-164">PowerShell</span><span class="sxs-lookup"><span data-stu-id="01314-164">PowerShell</span></span>

<span data-ttu-id="01314-165">następujące sekcje Hello Pokaż jak magazyn usług odzyskiwania Azure toouse PowerShell tooconfigure hello, Wyświetl kopii zapasowych w magazynie hello i Przywróć z magazynu hello.</span><span class="sxs-lookup"><span data-stu-id="01314-165">hello following sections show you how toouse PowerShell tooconfigure hello Azure Recovery Services vault, view backups in hello vault, and restore from hello vault.</span></span>

### <a name="create-a-recovery-services-vault"></a><span data-ttu-id="01314-166">Tworzenie magazynu usługi Recovery Services</span><span class="sxs-lookup"><span data-stu-id="01314-166">Create a recovery services vault</span></span>

<span data-ttu-id="01314-167">Użyj hello [AzureRmRecoveryServicesVault nowy](/powershell/module/azurerm.recoveryservices/new-azurermrecoveryservicesvault) toocreate odzyskiwania usług magazynu.</span><span class="sxs-lookup"><span data-stu-id="01314-167">Use hello [New-AzureRmRecoveryServicesVault](/powershell/module/azurerm.recoveryservices/new-azurermrecoveryservicesvault) toocreate a recovery services vault.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="01314-168">Magazyn Hello musi znajdować się w hello na tym samym regionie co serwer logiczny Azure SQL hello i musi Użyj hello sam grupie zasobów co powitania serwera logicznego.</span><span class="sxs-lookup"><span data-stu-id="01314-168">hello vault must be located in hello same region as hello Azure SQL logical server, and must use hello same resource group as hello logical server.</span></span>

```PowerShell
# Create a recovery services vault

#$resourceGroupName = "{resource-group-name}"
#$serverName = "{server-name}"
$serverLocation = (Get-AzureRmSqlServer -ServerName $serverName -ResourceGroupName $resourceGroupName).Location
$recoveryServiceVaultName = "{new-vault-name}"

$vault = New-AzureRmRecoveryServicesVault -Name $recoveryServiceVaultName -ResourceGroupName $ResourceGroupName -Location $serverLocation 
Set-AzureRmRecoveryServicesBackupProperties -BackupStorageRedundancy LocallyRedundant -Vault $vault
```

### <a name="set-your-server-toouse-hello-recovery-vault-for-its-long-term-retention-backups"></a><span data-ttu-id="01314-169">Zestawu server toouse hello odzyskiwania magazynu dla jego długoterminowe kopie zapasowe przechowywania</span><span class="sxs-lookup"><span data-stu-id="01314-169">Set your server toouse hello recovery vault for its long-term retention backups</span></span>

<span data-ttu-id="01314-170">Użyj hello [AzureRmSqlServerBackupLongTermRetentionVault zestaw](/powershell/module/azurerm.sql/set-azurermsqlserverbackuplongtermretentionvault) tooassociate polecenia cmdlet wcześniej utworzony magazyn usług odzyskiwania z określonego serwera Azure SQL.</span><span class="sxs-lookup"><span data-stu-id="01314-170">Use hello [Set-AzureRmSqlServerBackupLongTermRetentionVault](/powershell/module/azurerm.sql/set-azurermsqlserverbackuplongtermretentionvault) cmdlet tooassociate a previously created recovery services vault with a specific Azure SQL server.</span></span>

```PowerShell
# Set your server toouse hello vault toofor long-term backup retention 

Set-AzureRmSqlServerBackupLongTermRetentionVault -ResourceGroupName $resourceGroupName -ServerName $serverName -ResourceId $vault.Id
```

### <a name="create-a-retention-policy"></a><span data-ttu-id="01314-171">Tworzenie zasad przechowywania</span><span class="sxs-lookup"><span data-stu-id="01314-171">Create a retention policy</span></span>

<span data-ttu-id="01314-172">Zasady przechowywania jest, których wartość tookeep czas przechowywania kopii zapasowej bazy danych.</span><span class="sxs-lookup"><span data-stu-id="01314-172">A retention policy is where you set how long tookeep a database backup.</span></span> <span data-ttu-id="01314-173">Użyj hello [Get-AzureRmRecoveryServicesBackupRetentionPolicyObject](https://docs.microsoft.com/powershell/resourcemanager/azurerm.recoveryservices.backup/v2.3.0/get-azurermrecoveryservicesbackupretentionpolicyobject) polecenia cmdlet tooget hello domyślne przechowywania zasad toouse jako hello szablonu do tworzenia zasad.</span><span class="sxs-lookup"><span data-stu-id="01314-173">Use hello [Get-AzureRmRecoveryServicesBackupRetentionPolicyObject](https://docs.microsoft.com/powershell/resourcemanager/azurerm.recoveryservices.backup/v2.3.0/get-azurermrecoveryservicesbackupretentionpolicyobject) cmdlet tooget hello default retention policy toouse as hello template for creating policies.</span></span> <span data-ttu-id="01314-174">W tym szablonie okres przechowywania hello jest ustawiona przez 2 lata.</span><span class="sxs-lookup"><span data-stu-id="01314-174">In this template, hello retention period is set for 2 years.</span></span> <span data-ttu-id="01314-175">Następnie uruchom hello [AzureRmRecoveryServicesBackupProtectionPolicy nowy](/powershell/module/azurerm.recoveryservices.backup/new-azurermrecoveryservicesbackupprotectionpolicy) toofinally tworzenie hello zasad.</span><span class="sxs-lookup"><span data-stu-id="01314-175">Next, run hello [New-AzureRmRecoveryServicesBackupProtectionPolicy](/powershell/module/azurerm.recoveryservices.backup/new-azurermrecoveryservicesbackupprotectionpolicy) toofinally create hello policy.</span></span> 

> [!NOTE]
> <span data-ttu-id="01314-176">Niektóre polecenia cmdlet wymaga hello kontekstu magazynem przed uruchomieniem ([AzureRmRecoveryServicesVaultContext zestaw](/powershell/module/azurerm.recoveryservices/set-azurermrecoveryservicesvaultcontext)), zobacz tego polecenia cmdlet w kilku pokrewnych fragmentów.</span><span class="sxs-lookup"><span data-stu-id="01314-176">Some cmdlets require that you set hello vault context before running ([Set-AzureRmRecoveryServicesVaultContext](/powershell/module/azurerm.recoveryservices/set-azurermrecoveryservicesvaultcontext)) so you see this cmdlet in a few related snippets.</span></span> <span data-ttu-id="01314-177">Kontekst hello jest ustawiona, ponieważ zasady hello jest częścią hello magazynu.</span><span class="sxs-lookup"><span data-stu-id="01314-177">You set hello context because hello policy is part of hello vault.</span></span> <span data-ttu-id="01314-178">Można utworzyć wiele zasad przechowywania dla każdego magazynu, a następnie zastosować hello potrzeby zasad toospecific w bazach danych.</span><span class="sxs-lookup"><span data-stu-id="01314-178">You can create multiple retention policies for each vault and then apply hello desired policy toospecific databases.</span></span> 


```PowerShell
# Retrieve hello default retention policy for hello AzureSQLDatabase workload type
$retentionPolicy = Get-AzureRmRecoveryServicesBackupRetentionPolicyObject -WorkloadType AzureSQLDatabase

# Set hello retention value tootwo years (you can set tooany time between 1 week and 10 years)
$retentionPolicy.RetentionDurationType = "Years"
$retentionPolicy.RetentionCount = 2
$retentionPolicyName = "my2YearRetentionPolicy"

# Set hello vault context toohello vault you are creating hello policy for
Set-AzureRmRecoveryServicesVaultContext -Vault $vault

# Create hello new policy
$policy = New-AzureRmRecoveryServicesBackupProtectionPolicy -name $retentionPolicyName -WorkloadType AzureSQLDatabase -retentionPolicy $retentionPolicy
$policy
```

### <a name="configure-a-database-toouse-hello-previously-defined-retention-policy"></a><span data-ttu-id="01314-179">Skonfiguruj zasady przechowywania hello wcześniej zdefiniowany toouse bazy danych</span><span class="sxs-lookup"><span data-stu-id="01314-179">Configure a database toouse hello previously defined retention policy</span></span>

<span data-ttu-id="01314-180">Użyj hello [AzureRmSqlDatabaseBackupLongTermRetentionPolicy zestaw](/powershell/module/azurerm.sql/set-azurermsqldatabasebackuplongtermretentionpolicy) polecenia cmdlet tooapply hello nowej zasady tooa określonej bazy danych.</span><span class="sxs-lookup"><span data-stu-id="01314-180">Use hello [Set-AzureRmSqlDatabaseBackupLongTermRetentionPolicy](/powershell/module/azurerm.sql/set-azurermsqldatabasebackuplongtermretentionpolicy) cmdlet tooapply hello new policy tooa specific database.</span></span>

```PowerShell
# Enable long-term retention for a specific SQL database
$policyState = "enabled"
Set-AzureRmSqlDatabaseBackupLongTermRetentionPolicy -ResourceGroupName $resourceGroupName -ServerName $serverName -DatabaseName $databaseName -State $policyState -ResourceId $policy.Id
```

### <a name="view-backup-info-and-backups-in-long-term-retention"></a><span data-ttu-id="01314-181">Wyświetlanie informacji o kopiach zapasowych i kopii zapasowych podlegających długoterminowemu przechowywaniu</span><span class="sxs-lookup"><span data-stu-id="01314-181">View backup info, and backups in long-term retention</span></span>

<span data-ttu-id="01314-182">Wyświetl informacje o kopii zapasowych bazy danych w [długoterminowego przechowywania kopii zapasowych](sql-database-long-term-retention.md).</span><span class="sxs-lookup"><span data-stu-id="01314-182">View information about your database backups in [long-term backup retention](sql-database-long-term-retention.md).</span></span> 

<span data-ttu-id="01314-183">Użyj następujących poleceń cmdlet tooview kopii zapasowej informacji hello:</span><span class="sxs-lookup"><span data-stu-id="01314-183">Use hello following cmdlets tooview backup information:</span></span>

- [<span data-ttu-id="01314-184">Get-AzureRmRecoveryServicesBackupContainer</span><span class="sxs-lookup"><span data-stu-id="01314-184">Get-AzureRmRecoveryServicesBackupContainer</span></span>](/powershell/module/azurerm.recoveryservices.backup/get-azurermrecoveryservicesbackupcontainer)
- [<span data-ttu-id="01314-185">Get-AzureRmRecoveryServicesBackupItem</span><span class="sxs-lookup"><span data-stu-id="01314-185">Get-AzureRmRecoveryServicesBackupItem</span></span>](/powershell/module/azurerm.recoveryservices.backup/get-azurermrecoveryservicesbackupitem)
- [<span data-ttu-id="01314-186">Get-AzureRmRecoveryServicesBackupRecoveryPoint</span><span class="sxs-lookup"><span data-stu-id="01314-186">Get-AzureRmRecoveryServicesBackupRecoveryPoint</span></span>](/powershell/module/azurerm.recoveryservices.backup/get-azurermrecoveryservicesbackuprecoverypoint)

```PowerShell
#$resourceGroupName = "{resource-group-name}"
#$serverName = "{server-name}"
$databaseNeedingRestore = $databaseName

# Set hello vault context toohello vault we want toorestore from
#$vault = Get-AzureRmRecoveryServicesVault -ResourceGroupName $resourceGroupName
Set-AzureRmRecoveryServicesVaultContext -Vault $vault

# hello following commands find hello container associated with hello server 'myserver' under resource group 'myresourcegroup'
$container = Get-AzureRmRecoveryServicesBackupContainer -ContainerType AzureSQL -FriendlyName $vault.Name

# Get hello long-term retention metadata associated with a specific database
$item = Get-AzureRmRecoveryServicesBackupItem -Container $container -WorkloadType AzureSQLDatabase -Name $databaseNeedingRestore

# Get all available backups for hello previously indicated database
# Optionally, set hello -StartDate and -EndDate parameters tooreturn backups within a specific time period
$availableBackups = Get-AzureRmRecoveryServicesBackupRecoveryPoint -Item $item
$availableBackups
```

### <a name="restore-a-database-from-a-backup-in-long-term-backup-retention"></a><span data-ttu-id="01314-187">Przywracanie bazy danych z kopii zapasowej podlegającej długoterminowemu przechowywaniu kopii zapasowych</span><span class="sxs-lookup"><span data-stu-id="01314-187">Restore a database from a backup in long-term backup retention</span></span>

<span data-ttu-id="01314-188">Przywracanie z długoterminowego przechowywania kopii zapasowych używa hello [Restore-AzureRmSqlDatabase](/powershell/module/azurerm.sql/restore-azurermsqldatabase) polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="01314-188">Restoring from long-term backup retention uses hello [Restore-AzureRmSqlDatabase](/powershell/module/azurerm.sql/restore-azurermsqldatabase) cmdlet.</span></span>

```PowerShell
# Restore hello most recent backup: $availableBackups[0]
#$resourceGroupName = "{resource-group-name}"
#$serverName = "{server-name}"
$restoredDatabaseName = "{new-database-name}"
$edition = "Basic"
$performanceLevel = "Basic"

$restoredDb = Restore-AzureRmSqlDatabase -FromLongTermRetentionBackup -ResourceId $availableBackups[0].Id -ResourceGroupName $resourceGroupName `
 -ServerName $serverName -TargetDatabaseName $restoredDatabaseName -Edition $edition -ServiceObjectiveName $performanceLevel
$restoredDb
```


> [!NOTE]
> <span data-ttu-id="01314-189">W tym miejscu możesz połączyć toohello przywrócić bazę danych za pomocą programu SQL Server Management Studio tooperform wymagane zadania, takie jak tooextract bit danych z hello przywrócić toocopy bazy danych do hello istniejącej bazy danych lub istniejącą bazę danych toodelete hello i Zmień nazwę Witaj przywróconej bazy danych toohello nazwy istniejącej bazy danych.</span><span class="sxs-lookup"><span data-stu-id="01314-189">From here, you can connect toohello restored database using SQL Server Management Studio tooperform needed tasks, such as tooextract a bit of data from hello restored database toocopy into hello existing database or toodelete hello existing database and rename hello restored database toohello existing database name.</span></span> <span data-ttu-id="01314-190">Zobacz [punktu w czasie przywracania](sql-database-recovery-using-backups.md#point-in-time-restore).</span><span class="sxs-lookup"><span data-stu-id="01314-190">See [point in time restore](sql-database-recovery-using-backups.md#point-in-time-restore).</span></span>

## <a name="next-steps"></a><span data-ttu-id="01314-191">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="01314-191">Next steps</span></span>

- <span data-ttu-id="01314-192">toolearn o generowanych przez usługi automatycznego tworzenia kopii zapasowych, zobacz [automatycznego tworzenia kopii zapasowych](sql-database-automated-backups.md)</span><span class="sxs-lookup"><span data-stu-id="01314-192">toolearn about service-generated automatic backups, see [automatic backups](sql-database-automated-backups.md)</span></span>
- <span data-ttu-id="01314-193">toolearn dotyczące długoterminowego przechowywania kopii zapasowych, zobacz [długoterminowego przechowywania kopii zapasowych](sql-database-long-term-retention.md)</span><span class="sxs-lookup"><span data-stu-id="01314-193">toolearn about long-term backup retention, see [long-term backup retention](sql-database-long-term-retention.md)</span></span>
- <span data-ttu-id="01314-194">toolearn dotyczące przywracania z kopii zapasowych, zobacz [Przywracanie z kopii zapasowej](sql-database-recovery-using-backups.md)</span><span class="sxs-lookup"><span data-stu-id="01314-194">toolearn about restoring from backups, see [restore from backup](sql-database-recovery-using-backups.md)</span></span>
