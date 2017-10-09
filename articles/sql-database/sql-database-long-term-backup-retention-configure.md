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
# <a name="configure-and-restore-from-azure-sql-database-long-term-backup-retention"></a>Konfigurowanie i Przywróć z długoterminowego przechowywania kopii zapasowych bazy danych SQL Azure

Można skonfigurować tworzenia kopii zapasowych bazy danych Azure SQL toostore programu hello usług odzyskiwania Azure magazynu, a następnie Odzyskaj przechowywane za pomocą kopii zapasowej bazy danych za pomocą magazynu hello hello portalu Azure lub programu PowerShell.

## <a name="azure-portal"></a>Azure Portal

następujące sekcje Pokaż jak magazyn toouse hello Azure tooconfigure portalu hello usług odzyskiwania Azure, wyświetlanie kopii zapasowych w magazynie hello i Przywróć z magazynu hello Hello.

### <a name="configure-hello-vault-register-hello-server-and-select-databases"></a>Konfigurowanie magazynu hello, Zarejestruj serwer hello i wybrać bazy danych

Możesz [skonfigurowania kopii zapasowych tooretain automatycznego magazyn usług odzyskiwania Azure](sql-database-long-term-retention.md) przez okres dłuższy niż okres przechowywania hello warstwę usług. 

1. Otwórz hello **programu SQL Server** strony serwera.

   ![Strona serwera SQL](./media/sql-database-get-started-portal/sql-server-blade.png)

2. Kliknij pozycję **Długoterminowe przechowywanie kopii zapasowych**.

   ![link długoterminowego przechowywania kopii zapasowych](./media/sql-database-get-started-backup-recovery/long-term-backup-retention-link.png)

3. Na powitania **długoterminowego przechowywania kopii zapasowych** serwera Przejrzyj i zaakceptuj warunki Podgląd hello (chyba że użytkownik jeszcze - lub ta funkcja nie jest już w wersji zapoznawczej).

   ![Zaakceptuj postanowienia Podgląd hello](./media/sql-database-get-started-backup-recovery/accept-the-preview-terms.png)

4. Wybierz tę bazę danych w siatce hello tooconfigure długoterminowego przechowywania kopii zapasowych, a następnie kliknij przycisk **Konfigurowanie** na powitania narzędzi.

   ![wybieranie bazy danych do długoterminowego przechowywania kopii zapasowych](./media/sql-database-get-started-backup-recovery/select-database-for-long-term-backup-retention.png)

5. Na powitania **Konfiguruj** kliknij przycisk **Skonfiguruj wymagane ustawienia** w obszarze **magazyn usług odzyskiwania**.

   ![konfigurowanie linku do magazynu](./media/sql-database-get-started-backup-recovery/configure-vault-link.png)

6. Na powitania **magazyn usług odzyskiwania** wybierz istniejącego magazynu, jeśli istnieje. W przeciwnym razie jeśli nie znaleziono dla Twojej subskrypcji magazynu usług odzyskiwania, kliknij tooexit hello przepływu i Tworzenie magazynu usług odzyskiwania.

   ![Utwórz łącze do magazynu](./media/sql-database-get-started-backup-recovery/create-new-vault-link.png)

7. Na powitania **Magazyny usług odzyskiwania** kliknij przycisk **Dodaj**.

   ![Dodawanie linku do magazynu](./media/sql-database-get-started-backup-recovery/add-new-vault-link.png)
   
8. Na powitania **magazyn usług odzyskiwania** dla magazyn usług odzyskiwania hello, podaj prawidłową nazwę.

   ![nazwa nowego magazynu](./media/sql-database-get-started-backup-recovery/new-vault-name.png)

9. Wybierz subskrypcji i grupy zasobów, a następnie wybierz lokalizację hello hello magazynu. Gdy skończysz, kliknij pozycję **Utwórz**.

   ![Tworzenie magazynu](./media/sql-database-get-started-backup-recovery/create-new-vault.png)

   > [!IMPORTANT]
   > Magazyn Hello musi znajdować się w hello na tym samym regionie co serwer logiczny Azure SQL hello i musi Użyj hello sam grupie zasobów co powitania serwera logicznego.
   >

10. Po utworzeniu hello nowy magazyn, należy wykonać hello niezbędne kroki tooreturn toohello **magazyn usług odzyskiwania** strony.

11. Na powitania **magazyn usług odzyskiwania** strony, kliknij przycisk hello magazynu, a następnie kliknij przycisk **wybierz**.

   ![wybieranie istniejącego magazynu](./media/sql-database-get-started-backup-recovery/select-existing-vault.png)

12. Na powitania **Konfiguruj** , podaj prawidłową nazwę dla nowych zasad przechowywania hello, zmodyfikuj zasady przechowywania domyślne hello zależnie od potrzeb, a następnie kliknij przycisk **OK**.

   ![definiowanie zasad przechowywania](./media/sql-database-get-started-backup-recovery/define-retention-policy.png)

13. Na powitania **długoterminowego przechowywania kopii zapasowych** stron dla bazy danych, kliknij przycisk **zapisać** , a następnie kliknij przycisk **OK** tooapply hello tooall zasad przechowywania kopii zapasowych, długoterminowe wybrane bazy danych.

   ![definiowanie zasad przechowywania](./media/sql-database-get-started-backup-recovery/save-retention-policy.png)

14. Kliknij przycisk **zapisać** tooenable długoterminowego przechowywania kopii zapasowych za pomocą tego nowego skonfigurowany magazyn usług odzyskiwania Azure toohello zasad.

   ![definiowanie zasad przechowywania](./media/sql-database-get-started-backup-recovery/enable-long-term-retention.png)

> [!IMPORTANT]
> Po skonfigurowaniu kopii zapasowych są wyświetlane w magazynie hello w ciągu najbliższych siedmiu dni. W tym samouczku nie należy kontynuować, aż do tworzenia kopii zapasowych pojawiają się w magazynie hello.
>

### <a name="view-backups-in-long-term-retention-using-azure-portal"></a>Wyświetl kopie zapasowe w przechowywania długoterminowego za pomocą portalu Azure

Wyświetl informacje o kopii zapasowych bazy danych w [długoterminowego przechowywania kopii zapasowych](sql-database-long-term-retention.md). 

1. W portalu Azure Witaj, Otwórz magazyn usług odzyskiwania Azure na kopie zapasowe bazy danych (Przejdź zbyt**wszystkie zasoby** i wybierz ją z listy hello zasobów dla Twojej subskrypcji) tooview hello ilość Magazyn używany przez bazę danych Tworzenie kopii zapasowych w magazynie hello.

   ![wyświetlanie magazynu usługi recovery services z kopiami zapasowymi](./media/sql-database-get-started-backup-recovery/view-recovery-services-vault-with-data.png)

2. Otwórz hello **bazy danych SQL** stron dla bazy danych.

   ![Nowa strona bazy danych przykładowych](./media/sql-database-get-started-portal/new-sample-db-blade.png)

3. Na pasku narzędzi hello, kliknij przycisk **przywrócić**.

   ![pasek narzędzi przywracania](./media/sql-database-get-started-backup-recovery/restore-toolbar.png)

4. Na stronie powitania przywracania kliknij **długoterminowej**.

5. W obszarze kopii zapasowych magazynu Azure, kliknij **Wybierz kopię zapasową** tooview kopii zapasowych bazy danych dostępności hello w długoterminowego przechowywania kopii zapasowych.

   ![kopie zapasowe w magazynie](./media/sql-database-get-started-backup-recovery/view-backups-in-vault.png)

### <a name="restore-a-database-from-a-backup-in-long-term-backup-retention-using-hello-azure-portal"></a>Przywracanie bazy danych z kopii zapasowej w długoterminowego przechowywania kopii zapasowych za pomocą hello portalu Azure

Witaj tooa nowe baza danych jest przywrócenie z kopii zapasowej w powitalne magazyn usług odzyskiwania Azure.

1. Na powitania **kopii zapasowych magazynu Azure** strony, kliknij przycisk hello toorestore kopii zapasowej, a następnie kliknij przycisk **wybierz**.

   ![wybieranie kopii zapasowej w magazynie](./media/sql-database-get-started-backup-recovery/select-backup-in-vault.png)

2. W hello **Nazwa bazy danych** tekst Podaj nazwę hello hello przywrócić bazy danych.

   ![nazwa nowej nazwy danych](./media/sql-database-get-started-backup-recovery/new-database-name.png)

3. Kliknij przycisk **OK** toorestore bazy danych z kopii zapasowej hello hello magazynu toohello nowej bazy danych.

4. Na pasku narzędzi hello kliknij przycisk Stan ikony powiadomień hello hello tooview hello zadania przywracania.

   ![postęp zadania przywracania z magazynu](./media/sql-database-get-started-backup-recovery/restore-job-progress-long-term.png)

5. Po zakończeniu zadania przywracania hello Otwórz hello **baz danych SQL** strony tooview hello nowo przywrócone w bazie danych.

   ![baza danych przywrócona z magazynu](./media/sql-database-get-started-backup-recovery/restored-database-from-vault.png)

> [!NOTE]
> W tym miejscu możesz połączyć toohello przywrócić bazy danych przy użyciu programu SQL Server Management Studio tooperform wymagane zadania, takie jak zbyt[wyodrębniania do istniejącej bazy danych hello lub istniejące hello toodelete hello przywrócić bazy danych toocopy bit danych Nazwa bazy danych bazy danych i Zmień nazwę hello przywrócić bazy danych toohello istniejących](sql-database-recovery-using-backups.md#point-in-time-restore).
>

## <a name="powershell"></a>PowerShell

następujące sekcje Hello Pokaż jak magazyn usług odzyskiwania Azure toouse PowerShell tooconfigure hello, Wyświetl kopii zapasowych w magazynie hello i Przywróć z magazynu hello.

### <a name="create-a-recovery-services-vault"></a>Tworzenie magazynu usługi Recovery Services

Użyj hello [AzureRmRecoveryServicesVault nowy](/powershell/module/azurerm.recoveryservices/new-azurermrecoveryservicesvault) toocreate odzyskiwania usług magazynu.

> [!IMPORTANT]
> Magazyn Hello musi znajdować się w hello na tym samym regionie co serwer logiczny Azure SQL hello i musi Użyj hello sam grupie zasobów co powitania serwera logicznego.

```PowerShell
# Create a recovery services vault

#$resourceGroupName = "{resource-group-name}"
#$serverName = "{server-name}"
$serverLocation = (Get-AzureRmSqlServer -ServerName $serverName -ResourceGroupName $resourceGroupName).Location
$recoveryServiceVaultName = "{new-vault-name}"

$vault = New-AzureRmRecoveryServicesVault -Name $recoveryServiceVaultName -ResourceGroupName $ResourceGroupName -Location $serverLocation 
Set-AzureRmRecoveryServicesBackupProperties -BackupStorageRedundancy LocallyRedundant -Vault $vault
```

### <a name="set-your-server-toouse-hello-recovery-vault-for-its-long-term-retention-backups"></a>Zestawu server toouse hello odzyskiwania magazynu dla jego długoterminowe kopie zapasowe przechowywania

Użyj hello [AzureRmSqlServerBackupLongTermRetentionVault zestaw](/powershell/module/azurerm.sql/set-azurermsqlserverbackuplongtermretentionvault) tooassociate polecenia cmdlet wcześniej utworzony magazyn usług odzyskiwania z określonego serwera Azure SQL.

```PowerShell
# Set your server toouse hello vault toofor long-term backup retention 

Set-AzureRmSqlServerBackupLongTermRetentionVault -ResourceGroupName $resourceGroupName -ServerName $serverName -ResourceId $vault.Id
```

### <a name="create-a-retention-policy"></a>Tworzenie zasad przechowywania

Zasady przechowywania jest, których wartość tookeep czas przechowywania kopii zapasowej bazy danych. Użyj hello [Get-AzureRmRecoveryServicesBackupRetentionPolicyObject](https://docs.microsoft.com/powershell/resourcemanager/azurerm.recoveryservices.backup/v2.3.0/get-azurermrecoveryservicesbackupretentionpolicyobject) polecenia cmdlet tooget hello domyślne przechowywania zasad toouse jako hello szablonu do tworzenia zasad. W tym szablonie okres przechowywania hello jest ustawiona przez 2 lata. Następnie uruchom hello [AzureRmRecoveryServicesBackupProtectionPolicy nowy](/powershell/module/azurerm.recoveryservices.backup/new-azurermrecoveryservicesbackupprotectionpolicy) toofinally tworzenie hello zasad. 

> [!NOTE]
> Niektóre polecenia cmdlet wymaga hello kontekstu magazynem przed uruchomieniem ([AzureRmRecoveryServicesVaultContext zestaw](/powershell/module/azurerm.recoveryservices/set-azurermrecoveryservicesvaultcontext)), zobacz tego polecenia cmdlet w kilku pokrewnych fragmentów. Kontekst hello jest ustawiona, ponieważ zasady hello jest częścią hello magazynu. Można utworzyć wiele zasad przechowywania dla każdego magazynu, a następnie zastosować hello potrzeby zasad toospecific w bazach danych. 


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

### <a name="configure-a-database-toouse-hello-previously-defined-retention-policy"></a>Skonfiguruj zasady przechowywania hello wcześniej zdefiniowany toouse bazy danych

Użyj hello [AzureRmSqlDatabaseBackupLongTermRetentionPolicy zestaw](/powershell/module/azurerm.sql/set-azurermsqldatabasebackuplongtermretentionpolicy) polecenia cmdlet tooapply hello nowej zasady tooa określonej bazy danych.

```PowerShell
# Enable long-term retention for a specific SQL database
$policyState = "enabled"
Set-AzureRmSqlDatabaseBackupLongTermRetentionPolicy -ResourceGroupName $resourceGroupName -ServerName $serverName -DatabaseName $databaseName -State $policyState -ResourceId $policy.Id
```

### <a name="view-backup-info-and-backups-in-long-term-retention"></a>Wyświetlanie informacji o kopiach zapasowych i kopii zapasowych podlegających długoterminowemu przechowywaniu

Wyświetl informacje o kopii zapasowych bazy danych w [długoterminowego przechowywania kopii zapasowych](sql-database-long-term-retention.md). 

Użyj następujących poleceń cmdlet tooview kopii zapasowej informacji hello:

- [Get-AzureRmRecoveryServicesBackupContainer](/powershell/module/azurerm.recoveryservices.backup/get-azurermrecoveryservicesbackupcontainer)
- [Get-AzureRmRecoveryServicesBackupItem](/powershell/module/azurerm.recoveryservices.backup/get-azurermrecoveryservicesbackupitem)
- [Get-AzureRmRecoveryServicesBackupRecoveryPoint](/powershell/module/azurerm.recoveryservices.backup/get-azurermrecoveryservicesbackuprecoverypoint)

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

### <a name="restore-a-database-from-a-backup-in-long-term-backup-retention"></a>Przywracanie bazy danych z kopii zapasowej podlegającej długoterminowemu przechowywaniu kopii zapasowych

Przywracanie z długoterminowego przechowywania kopii zapasowych używa hello [Restore-AzureRmSqlDatabase](/powershell/module/azurerm.sql/restore-azurermsqldatabase) polecenia cmdlet.

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
> W tym miejscu możesz połączyć toohello przywrócić bazę danych za pomocą programu SQL Server Management Studio tooperform wymagane zadania, takie jak tooextract bit danych z hello przywrócić toocopy bazy danych do hello istniejącej bazy danych lub istniejącą bazę danych toodelete hello i Zmień nazwę Witaj przywróconej bazy danych toohello nazwy istniejącej bazy danych. Zobacz [punktu w czasie przywracania](sql-database-recovery-using-backups.md#point-in-time-restore).

## <a name="next-steps"></a>Następne kroki

- toolearn o generowanych przez usługi automatycznego tworzenia kopii zapasowych, zobacz [automatycznego tworzenia kopii zapasowych](sql-database-automated-backups.md)
- toolearn dotyczące długoterminowego przechowywania kopii zapasowych, zobacz [długoterminowego przechowywania kopii zapasowych](sql-database-long-term-retention.md)
- toolearn dotyczące przywracania z kopii zapasowych, zobacz [Przywracanie z kopii zapasowej](sql-database-recovery-using-backups.md)
