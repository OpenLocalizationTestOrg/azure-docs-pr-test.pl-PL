---
title: "aaaDeploy i zarządzanie nimi kopii zapasowych maszyn wirtualnych wdrożonych przez Menedżera zasobów, przy użyciu programu PowerShell | Dokumentacja firmy Microsoft"
description: "Użyj programu PowerShell toodeploy i zarządzanie kopiami zapasowymi w usłudze Azure dla maszyn wirtualnych, wdrożonych przez Menedżera zasobów"
services: backup
documentationcenter: 
author: markgalioto
manager: carmonm
editor: 
ms.assetid: 68606e4f-536d-4eac-9f80-8a198ea94d52
ms.service: backup
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 08/28/2017
ms.author: markgal;trinadhk
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 486fb3ae1902403fe6bf303df57244b76677ab17
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="use-azurermrecoveryservicesbackup-cmdlets-tooback-up-virtual-machines"></a>Użyj tooback poleceń cmdlet AzureRM.RecoveryServices.Backup zapasowych maszyn wirtualnych
> [!div class="op_single_selector"]
> * [Resource Manager](backup-azure-vms-automation.md)
> * [Wdrożenie klasyczne](backup-azure-vms-classic-automation.md)
>
>

W tym artykule opisano, jak magazyn tooback poleceń cmdlet programu Azure PowerShell toouse zapasowej i odzyskiwanie maszyny wirtualnej platformy Azure (VM) z usług odzyskiwania. Magazyn usług odzyskiwania jest zasobów usługi Azure Resource Manager i tooprotect używanych danych i zasobów w usługach zarówno Azure Backup i Azure Site Recovery. Można użyć tooprotect magazyn usług odzyskiwania Azure Service Manager wdrożone maszyny wirtualne i usługi Azure Resource Manager wdrożone maszyny wirtualne.

> [!NOTE]
> Platforma Azure ma dwa modele wdrażania związane z tworzeniem zasobów i pracą z nimi: [Resource Manager i model klasyczny](../azure-resource-manager/resource-manager-deployment-model.md). W tym artykule jest przeznaczona do użytku z maszyn wirtualnych utworzonych przy użyciu hello modelu Resource Manager.
>
>

W tym artykule przedstawiono przy użyciu programu PowerShell tooprotect maszyny Wirtualnej i przywracanie danych z punktu odzyskiwania.

## <a name="concepts"></a>Pojęcia
Jeśli nie masz doświadczenia w obsłudze hello usługi Kopia zapasowa Azure Omówienie usługi hello wyewidencjonować [co to jest kopia zapasowa Azure?](backup-introduction-to-azure-backup.md) Przed rozpoczęciem upewnij się, obejmują essentials hello o toowork wymagania wstępne niezbędne hello w usłudze Kopia zapasowa Azure i hello ograniczenia bieżące rozwiązanie tworzenia kopii zapasowej hello maszyny Wirtualnej.

toouse PowerShell ostatecznie jest konieczne toounderstand hello hierarchii obiektów i z jakiej lokalizacji toostart.

![Hierarchia obiektów usługi odzyskiwania](./media/backup-azure-vms-arm-automation/recovery-services-object-hierarchy.png)

Witaj tooview AzureRm.RecoveryServices.Backup polecenia cmdlet w programie PowerShell, zobacz hello [kopia zapasowa Azure - polecenia cmdlet usług odzyskiwania](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup) w hello Azure biblioteki.

## <a name="setup-and-registration"></a>Instalację i rejestrację
toobegin:

1. [Pobieranie najnowszej wersji programu PowerShell hello](https://docs.microsoft.com/powershell/azure/install-azurerm-ps) (hello minimalna wersja wymagana jest: 1.4.0)
2. Znajdź hello programu PowerShell usługi Azure Backup dostępnych poleceń cmdlet, wpisując następujące polecenie hello:

```
PS C:\> Get-Command *azurermrecoveryservices*

CommandType     Name                                               Version    Source
-----------     ----                                               -------    ------
Cmdlet          Backup-AzureRmRecoveryServicesBackupItem           1.4.0      AzureRM.RecoveryServices.Backup
Cmdlet          Disable-AzureRmRecoveryServicesBackupProtection    1.4.0      AzureRM.RecoveryServices.Backup
Cmdlet          Enable-AzureRmRecoveryServicesBackupProtection     1.4.0      AzureRM.RecoveryServices.Backup
Cmdlet          Get-AzureRmRecoveryServicesBackupContainer         1.4.0      AzureRM.RecoveryServices.Backup
Cmdlet          Get-AzureRmRecoveryServicesBackupItem              1.4.0      AzureRM.RecoveryServices.Backup
Cmdlet          Get-AzureRmRecoveryServicesBackupJob               1.4.0      AzureRM.RecoveryServices.Backup
Cmdlet          Get-AzureRmRecoveryServicesBackupJobDetails        1.4.0      AzureRM.RecoveryServices.Backup
Cmdlet          Get-AzureRmRecoveryServicesBackupManagementServer  1.4.0      AzureRM.RecoveryServices.Backup
Cmdlet          Get-AzureRmRecoveryServicesBackupProperties        1.4.0      AzureRM.RecoveryServices
Cmdlet          Get-AzureRmRecoveryServicesBackupProtectionPolicy  1.4.0      AzureRM.RecoveryServices.Backup
Cmdlet          Get-AzureRMRecoveryServicesBackupRecoveryPoint     1.4.0      AzureRM.RecoveryServices.Backup
Cmdlet          Get-AzureRmRecoveryServicesBackupRetentionPolic... 1.4.0      AzureRM.RecoveryServices.Backup
Cmdlet          Get-AzureRmRecoveryServicesBackupSchedulePolicy... 1.4.0      AzureRM.RecoveryServices.Backup
Cmdlet          Get-AzureRmRecoveryServicesVault                   1.4.0      AzureRM.RecoveryServices
Cmdlet          Get-AzureRmRecoveryServicesVaultSettingsFile       1.4.0      AzureRM.RecoveryServices
Cmdlet          New-AzureRmRecoveryServicesBackupProtectionPolicy  1.4.0      AzureRM.RecoveryServices.Backup
Cmdlet          New-AzureRmRecoveryServicesVault                   1.4.0      AzureRM.RecoveryServices
Cmdlet          Remove-AzureRmRecoveryServicesProtectionPolicy     1.4.0      AzureRM.RecoveryServices.Backup
Cmdlet          Remove-AzureRmRecoveryServicesVault                1.4.0      AzureRM.RecoveryServices
Cmdlet          Restore-AzureRMRecoveryServicesBackupItem          1.4.0      AzureRM.RecoveryServices.Backup
Cmdlet          Set-AzureRmRecoveryServicesBackupProperties        1.4.0      AzureRM.RecoveryServices
Cmdlet          Set-AzureRmRecoveryServicesBackupProtectionPolicy  1.4.0      AzureRM.RecoveryServices.Backup
Cmdlet          Set-AzureRmRecoveryServicesVaultContext            1.4.0      AzureRM.RecoveryServices
Cmdlet          Stop-AzureRmRecoveryServicesBackupJob              1.4.0      AzureRM.RecoveryServices.Backup
Cmdlet          Unregister-AzureRmRecoveryServicesBackupContainer  1.4.0      AzureRM.RecoveryServices.Backup
Cmdlet          Unregister-AzureRmRecoveryServicesBackupManagem... 1.4.0      AzureRM.RecoveryServices.Backup
Cmdlet          Wait-AzureRmRecoveryServicesBackupJob              1.4.0      AzureRM.RecoveryServices.Backup
```


przy użyciu programu PowerShell można zautomatyzować Hello następujące zadania:

* Tworzenie magazynu Usług odzyskiwania
* Tworzenie kopii zapasowych maszyn wirtualnych platformy Azure
* Wyzwalacz zadania tworzenia kopii zapasowej
* Monitor zadania tworzenia kopii zapasowej
* Przywracanie maszyny Wirtualnej platformy Azure

## <a name="create-a-recovery-services-vault"></a>Tworzenie magazynu usługi Recovery Services
następujące kroki Hello przeprowadzi Cię przez tworzenie magazynu usług odzyskiwania. Magazyn usług odzyskiwania są inne niż magazynu kopii zapasowych.

1. Jeśli kopia zapasowa Azure jest używana do powitania po raz pierwszy, należy użyć hello  **[AzureRmResourceProvider rejestru](http://docs.microsoft.com/powershell/module/azurerm.resources/register-azurermresourceprovider)**  polecenia cmdlet tooregister hello Azure odzyskiwania usługodawcy w ramach subskrypcji.

    ```
    PS C:\> Register-AzureRmResourceProvider -ProviderNamespace "Microsoft.RecoveryServices"
    ```
2. Witaj magazyn usług odzyskiwania jest zasobu usługi Resource Manager, więc należy tooplace go w grupie zasobów. Użyj istniejącej grupy zasobów lub Utwórz grupę zasobów o hello  **[New-AzureRmResourceGroup](https://docs.microsoft.com/powershell/module/azurerm.resources/new-azurermresourcegroup)**  polecenia cmdlet. Podczas tworzenia grupy zasobów, należy określić hello nazwę i lokalizację dla grupy zasobów hello.  

    ```
    PS C:\> New-AzureRmResourceGroup –Name "test-rg" –Location "West US"
    ```
3. Użyj hello  **[AzureRmRecoveryServicesVault nowy](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices/new-azurermrecoveryservicesvault)**  hello toocreate polecenia cmdlet magazynu usług odzyskiwania. Pamiętaj, toospecify hello tę samą lokalizację dla magazynu hello, które było używane dla grupy zasobów hello.

    ```
    PS C:\> New-AzureRmRecoveryServicesVault -Name "testvault" -ResourceGroupName " test-rg" -Location "West US"
    ```
4. Określ typ hello toouse nadmiarowość magazynu; można użyć [lokalnie nadmiarowego magazynu (LRS)](../storage/common/storage-redundancy.md#locally-redundant-storage) lub [z magazynu geograficznie nadmiarowego magazynu (GRS)](../storage/common/storage-redundancy.md#geo-redundant-storage). Witaj poniższy przykład przedstawia się, że opcja - BackupStorageRedundancy hello testvault ustawiono tooGeoRedundant.

    ```
    PS C:\> $vault1 = Get-AzureRmRecoveryServicesVault –Name "testvault"
    PS C:\> Set-AzureRmRecoveryServicesBackupProperties  -Vault $vault1 -BackupStorageRedundancy GeoRedundant
    ```

   > [!TIP]
   > Wiele poleceń cmdlet narzędzia Kopia zapasowa Azure wymaga obiektu magazynu usług odzyskiwania hello jako danych wejściowych. Z tego powodu jest wygodne toostore hello usług odzyskiwania kopii zapasowej magazynu obiekt w zmiennej.
   >
   >

## <a name="view-hello-vaults-in-a-subscription"></a>Widok hello magazynów w ramach subskrypcji
Użyj  **[Get-AzureRmRecoveryServicesVault](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices/get-azurermrecoveryservicesvault)**  tooview hello listę wszystkich magazynów w hello bieżącej subskrypcji. Można użyć tego polecenia toocheck, czy utworzono nowy magazyn, lub toosee hello dostępnych magazynów w subskrypcji hello.

Uruchom polecenie hello, Get-AzureRmRecoveryServicesVault tooview wszystkie magazyny hello subskrypcji. Witaj poniższy przykład przedstawia hello informacje wyświetlane dla każdego magazynu.

```
PS C:\> Get-AzureRmRecoveryServicesVault
Name              : Contoso-vault
ID                : /subscriptions/1234
Type              : Microsoft.RecoveryServices/vaults
Location          : WestUS
ResourceGroupName : Contoso-docs-rg
SubscriptionId    : 1234-567f-8910-abc
Properties        : Microsoft.Azure.Commands.RecoveryServices.ARSVaultProperties
```


## <a name="back-up-azure-vms"></a>Tworzenie kopii zapasowych maszyn wirtualnych platformy Azure
Użyj tooprotect magazyn usług odzyskiwania maszyn wirtualnych. Przed zastosowaniem ochrona powitalnych Ustaw kontekst magazynu hello (hello typ danych chronionych w magazynie hello), a następnie sprawdź hello zasad ochrony. zasady ochrony Hello jest harmonogram hello uruchomienie zadania tworzenia kopii zapasowej hello i jak długo są przechowywane każdego migawki kopii zapasowej.

### <a name="set-vault-context"></a>Ustaw kontekst magazynu
Przed ponownym włączeniem ochrony na maszynie Wirtualnej, użyj  **[AzureRmRecoveryServicesVaultContext zestaw](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices/set-azurermrecoveryservicesvaultcontext)**  tooset hello magazynu kontekstu. Po ustawieniu kontekst magazynu hello stosuje tooall kolejne polecenia cmdlet. Witaj poniższy przykład przedstawia hello magazynu kontekst dla magazynu hello *testvault*.

```
PS C:\> Get-AzureRmRecoveryServicesVault -Name "testvault" | Set-AzureRmRecoveryServicesVaultContext
```

### <a name="create-a-protection-policy"></a>Tworzenie zasad ochrony
Podczas tworzenia magazynu usług odzyskiwania jest dostarczany z domyślną ochronę i zasady przechowywania. Witaj domyślne zasady ochrony wyzwala zadanie tworzenia kopii zapasowej każdego dnia o określonej godzinie. zasady przechowywania domyślne Hello zachowuje punkt odzyskiwania codziennie hello przez 30 dni. Można używać domyślnych hello tooquickly zasad ochrony maszyny Wirtualnej i edytować zasady hello później przy użyciu różnych szczegółów.

Użyj  **[Get-AzureRmRecoveryServicesBackupProtectionPolicy](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/get-azurermrecoveryservicesbackupprotectionpolicy)**  tooview zasady ochrony hello w magazynie hello. Tooget tego polecenia cmdlet można użyć określonych zasad lub tooview hello zasady skojarzone z typem obciążenia. Poniższy przykład Hello pobiera zasady dla obciążeń typu AzureVM.

```
PS C:\> Get-AzureRmRecoveryServicesBackupProtectionPolicy -WorkloadType "AzureVM"
Name                 WorkloadType       BackupManagementType BackupTime                DaysOfWeek
----                 ------------       -------------------- ----------                ----------
DefaultPolicy        AzureVM            AzureVM              4/14/2016 5:00:00 PM
```

> [!NOTE]
> Strefa czasowa Hello hello BackupTime pola w programie PowerShell jest czasem UTC. Jednak podczas wykonywania kopii zapasowej hello jest wyświetlany w hello portalu Azure, czas hello jest skorygowaną tooyour lokalną strefę czasową.
>
>

Zasady tworzenia kopii zapasowej ochrony jest skojarzony z co najmniej jedne zasady przechowywania. Zasady przechowywania określają, jak długo punkt odzyskiwania jest przechowywana, przed usunięciem. Użyj  **[Get-AzureRmRecoveryServicesBackupRetentionPolicyObject](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/get-azurermrecoveryservicesbackupretentionpolicyobject)**  tooview hello domyślne zachowanie zasady.  Podobnie można użyć  **[Get-AzureRmRecoveryServicesBackupSchedulePolicyObject](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/get-azurermrecoveryservicesbackupschedulepolicyobject)**  tooobtain hello domyślny harmonogram zasad. Witaj  **[AzureRmRecoveryServicesBackupProtectionPolicy nowy](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/new-azurermrecoveryservicesbackupprotectionpolicy)**  polecenie cmdlet tworzy obiekt programu PowerShell, która przechowuje informacje o zasadach tworzenia kopii zapasowej. Witaj harmonogram i przechowywania obiektów zasady są używane jako danych wejściowych toohello  **[AzureRmRecoveryServicesBackupProtectionPolicy nowy](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/new-azurermrecoveryservicesbackupprotectionpolicy)**  polecenia cmdlet. Witaj poniższy przykład przechowuje hello harmonogram zasad i zasady przechowywania hello w zmiennych. przykład Witaj używa tych zmiennych toodefine hello parametrów podczas tworzenia zasad ochrony, *NewPolicy*.

```
PS C:\> $schPol = Get-AzureRmRecoveryServicesBackupSchedulePolicyObject -WorkloadType "AzureVM"
PS C:\> $retPol = Get-AzureRmRecoveryServicesBackupRetentionPolicyObject -WorkloadType "AzureVM"
PS C:\> New-AzureRmRecoveryServicesBackupProtectionPolicy -Name "NewPolicy" -WorkloadType "AzureVM" -RetentionPolicy $retPol -SchedulePolicy $schPol
Name                 WorkloadType       BackupManagementType BackupTime                DaysOfWeek
----                 ------------       -------------------- ----------                ----------
NewPolicy           AzureVM            AzureVM              4/24/2016 1:30:00 AM
```


### <a name="enable-protection"></a>Włączanie ochrony
Po zdefiniowaniu zasad tworzenia kopii zapasowej ochrony hello nadal należy włączyć hello zasad dla elementu. Użyj  **[AzureRmRecoveryServicesBackupProtection Włącz](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/enable-azurermrecoveryservicesbackupprotection)**  tooenable ochrony. Włączenie ochrony wymaga dwóch obiektów - element hello i hello zasad. Gdy zasady hello został skojarzony z magazynem hello, hello kopii zapasowej przepływ pracy zostanie wyzwolony w czasie hello zdefiniowane w hello harmonogram zasad.

następujące przykładowe umożliwia ochronę hello elementu, V2VM, za pomocą zasad hello, NewPolicy Hello. ochronę hello tooenable niezaszyfrowane maszyn wirtualnych Menedżera zasobów

```
PS C:\> $pol=Get-AzureRmRecoveryServicesBackupProtectionPolicy -Name "NewPolicy"
PS C:\> Enable-AzureRmRecoveryServicesBackupProtection -Policy $pol -Name "V2VM" -ResourceGroupName "RGName1"
```

Ochrona powitalnych tooenable na szyfrowany maszyn wirtualnych (szyfrowane przy użyciu BEK i KEK), toogive hello kopia zapasowa Azure usługa uprawnienia tooread kluczy i kluczy tajnych w magazynie kluczy.

```
PS C:\> Set-AzureRmKeyVaultAccessPolicy -VaultName "KeyVaultName" -ResourceGroupName "RGNameOfKeyVault" -PermissionsToKeys backup,get,list -PermissionsToSecrets get,list -ServicePrincipalName 262044b1-e2ce-469f-a196-69ab7ada62d3
PS C:\> $pol=Get-AzureRmRecoveryServicesBackupProtectionPolicy -Name "NewPolicy"
PS C:\> Enable-AzureRmRecoveryServicesBackupProtection -Policy $pol -Name "V2VM" -ResourceGroupName "RGName1"
```

Ochrona powitalnych tooenable na szyfrowany maszyn wirtualnych (szyfrowane tylko przy użyciu BEK), toogive hello kopia zapasowa Azure usługi uprawnienia tooread kluczy tajnych w magazynie kluczy.

```
PS C:\> Set-AzureRmKeyVaultAccessPolicy -VaultName "KeyVaultName" -ResourceGroupName "RGNameOfKeyVault" -PermissionsToSecrets backup,get,list -ServicePrincipalName 262044b1-e2ce-469f-a196-69ab7ada62d3
PS C:\> $pol=Get-AzureRmRecoveryServicesBackupProtectionPolicy -Name "NewPolicy"
PS C:\> Enable-AzureRmRecoveryServicesBackupProtection -Policy $pol -Name "V2VM" -ResourceGroupName "RGName1"
```

> [!NOTE]
> Jeśli korzystasz z chmury Azure dla instytucji rządowych hello, użyj hello ff281ffe-705c-4f53-9f37-a40e6f2c68f3 wartość dla parametru hello **- ServicePrincipalName** w [Set-AzureRmKeyVaultAccessPolicy](https://docs.microsoft.com/powershell/module/azurerm.keyvault/set-azurermkeyvaultaccesspolicy) polecenia cmdlet .
>
>

Klasycznych maszyn wirtualnych

```
PS C:\> $pol=Get-AzureRmRecoveryServicesBackupProtectionPolicy -Name "NewPolicy"
PS C:\> Enable-AzureRmRecoveryServicesBackupProtection -Policy $pol -Name "V1VM" -ServiceName "ServiceName1"
```

### <a name="modify-a-protection-policy"></a>Modyfikowanie zasad ochrony
zasady ochrony hello toomodify, użyj [AzureRmRecoveryServicesBackupProtectionPolicy zestaw](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/set-azurermrecoveryservicesbackupprotectionpolicy) toomodify hello SchedulePolicy lub RetentionPolicy obiektów.

Witaj poniższy przykład umożliwia zmianę hello odzyskiwania punktu przechowywania too365 dni.

```
PS C:\> $retPol = Get-AzureRmRecoveryServicesBackupRetentionPolicyObject -WorkloadType "AzureVM"
PS C:\> $retPol.DailySchedule.DurationCountInDays = 365
PS C:\> $pol= Get-AzureRmRecoveryServicesBackupProtectionPolicy -Name "NewPolicy"
PS C:\> Set-AzureRmRecoveryServicesBackupProtectionPolicy -Policy $pol  -RetentionPolicy $RetPol
```

## <a name="trigger-a-backup"></a>Wyzwalacz kopią zapasową
Można użyć  **[AzureRmRecoveryServicesBackupItem kopii zapasowej](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/backup-azurermrecoveryservicesbackupitem)**  tootrigger zadania tworzenia kopii zapasowej. Jeśli jest hello początkowa kopia zapasowa jest pełnej kopii zapasowej. Tworzenie kolejnych kopii zapasowych zająć przyrostowej kopii. Należy się toouse  **[AzureRmRecoveryServicesVaultContext zestaw](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices/set-azurermrecoveryservicesvaultcontext)**  kontekst magazynu hello tooset przed wyzwalania hello zadanie tworzenia kopii zapasowej. Poniższy przykład Hello przyjęto założenie, że magazyn kontekst został ustawiony.

```
PS C:\> $namedContainer = Get-AzureRmRecoveryServicesBackupContainer -ContainerType "AzureVM" -Status "Registered" -FriendlyName "V2VM"
PS C:\> $item = Get-AzureRmRecoveryServicesBackupItem -Container $namedContainer -WorkloadType "AzureVM"
PS C:\> $job = Backup-AzureRmRecoveryServicesBackupItem -Item $item
WorkloadName     Operation            Status               StartTime                 EndTime                   JobID
------------     ---------            ------               ---------                 -------                   ----------
V2VM              Backup               InProgress            4/23/2016 5:00:30 PM                       cf4b3ef5-2fac-4c8e-a215-d2eba4124f27
```

> [!NOTE]
> Strefa czasowa Hello hello wartości StartTime i EndTime pól w programie PowerShell jest czasem UTC. Jednak gdy czas hello jest wyświetlana w portalu Azure hello, czas hello jest dostosowaną tooyour lokalną strefę czasową.
>
>

## <a name="monitoring-a-backup-job"></a>Monitorowanie zadania tworzenia kopii zapasowej
Można monitorować długotrwałe operacje, takie jak zadania tworzenia kopii zapasowej bez użycia hello portalu Azure. Stan hello tooget zadania w toku, użyj hello  **[Get-AzureRmRecoveryservicesBackupJob](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/get-azurermrecoveryservicesbackupjob)**  polecenia cmdlet. To polecenie cmdlet pobiera hello zadania tworzenia kopii zapasowej dla określonego magazynu, a tego magazynu jest określona w kontekście magazynu hello. Hello poniższy przykład pobiera hello stan zadania w toku jako tablica i zapisuje stan hello w zmiennej hello $joblist.

```
PS C:\> $joblist = Get-AzureRmRecoveryservicesBackupJob –Status "InProgress"
PS C:\> $joblist[0]
WorkloadName     Operation            Status               StartTime                 EndTime                   JobID
------------     ---------            ------               ---------                 -------                   ----------
V2VM             Backup               InProgress            4/23/2016 5:00:30 PM           cf4b3ef5-2fac-4c8e-a215-d2eba4124f27
```

Zamiast sondowania te zadania na zakończenie — czyli niepotrzebnych dodatkowy kod - Użyj hello  **[AzureRmRecoveryServicesBackupJob oczekiwania](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/wait-azurermrecoveryservicesbackupjob)**  polecenia cmdlet. To polecenie cmdlet wstrzymuje wykonywanie hello dopóki hello określona wartość limitu czasu jest osiągana albo hello zadanie zostało ukończone.

```
PS C:\> Wait-AzureRmRecoveryServicesBackupJob -Job $joblist[0] -Timeout 43200
```

## <a name="restore-an-azure-vm"></a>Przywracanie maszyny Wirtualnej platformy Azure
Ma klucza różnicy między hello przywracanie maszyny Wirtualnej przy użyciu hello portalu Azure i przywracanie maszyny Wirtualnej przy użyciu programu PowerShell. Przy użyciu programu PowerShell operacja przywracania hello została zakończona, po utworzeniu hello dyski i informacje o konfiguracji z hello punkt odzyskiwania.

> [!NOTE]
> Operacja przywracania Hello nie powoduje utworzenia maszyny wirtualnej.
>
>

toocreate maszyny wirtualnej z dysku, zobacz sekcję hello [hello tworzenie maszyny Wirtualnej z przechowywanych dysków](backup-azure-vms-automation.md#create-a-vm-from-stored-disks). Witaj podstawowe kroki toorestore maszyny Wirtualnej platformy Azure są:

* Wybierz hello maszyny Wirtualnej
* Wybierz punkt odzyskiwania
* Przywróć hello dysków
* Utwórz hello maszyny Wirtualnej z przechowywanych dysków

Witaj poniższy rysunek przedstawia hierarchię obiektów hello z hello RecoveryServicesVault toohello BackupRecoveryPoint w dół.

![Hierarchia obiektów usług odzyskiwania przedstawiający BackupContainer](./media/backup-azure-vms-arm-automation/backuprecoverypoint-only.png)

toorestore dane kopii zapasowej, zidentyfikuj hello elementu kopii zapasowej i hello punkt odzyskiwania, która przechowuje dane w momencie hello. Użyj hello  **[AzureRmRecoveryServicesBackupItem przywracania](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/restore-azurermrecoveryservicesbackupitem)**  danych toorestore polecenia cmdlet z hello magazynu toohello odbiorcy.

### <a name="select-hello-vm"></a>Wybierz hello maszyny Wirtualnej
tooget hello środowiska PowerShell obiektu, który identyfikuje hello prawo kopii zapasowej elementu, Rozpocznij od hello kontenera w magazynie hello i przechodzić w dół hierarchii obiektów hello. tooselect hello kontener, który reprezentuje hello maszyny Wirtualnej, użyj hello  **[Get-AzureRmRecoveryServicesBackupContainer](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/get-azurermrecoveryservicesbackupcontainer)**  polecenia cmdlet i przekazać w potoku tego toohello  **[ Get-AzureRmRecoveryServicesBackupItem](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/get-azurermrecoveryservicesbackupitem)**  polecenia cmdlet.

```
PS C:\> $namedContainer = Get-AzureRmRecoveryServicesBackupContainer  -ContainerType "AzureVM" –Status "Registered" -FriendlyName "V2VM"
PS C:\> $backupitem = Get-AzureRmRecoveryServicesBackupItem –Container $namedContainer  –WorkloadType "AzureVM"
```

### <a name="choose-a-recovery-point"></a>Wybierz punkt odzyskiwania
Użyj hello  **[Get-AzureRmRecoveryServicesBackupRecoveryPoint](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/get-azurermrecoveryservicesbackuprecoverypoint)**  wszystkie punkty odzyskiwania dla kopii zapasowej elementu hello toolist polecenia cmdlet. Następnie wybierz pozycję toorestore punktu odzyskiwania hello. Jeśli nie wiesz, które toouse punkt odzyskiwania, jest toochoose dobrym rozwiązaniem hello najnowszych RecoveryPointType = punktu AppConsistent na liście hello.

W hello następującego skryptu, hello zmiennej **$rp**, jest tablica punktów odzyskiwania dla hello wybrany element kopii zapasowej z hello ostatnich siedmiu dni. tablicy Hello jest sortowany w kolejności odwrotnej czasu z najnowszego punktu odzyskiwania hello pod indeksem 0. Użyj standardowych tablicy PowerShell indeksowania punkt odzyskiwania hello toopick. Na przykład Witaj $rp [0] wybiera hello najnowszego punktu odzyskiwania.

```
PS C:\> $startDate = (Get-Date).AddDays(-7)
PS C:\> $endDate = Get-Date
PS C:\> $rp = Get-AzureRmRecoveryServicesBackupRecoveryPoint -Item $backupitem -StartDate $startdate.ToUniversalTime() -EndDate $enddate.ToUniversalTime()
PS C:\> $rp[0]
RecoveryPointAdditionalInfo :
SourceVMStorageType         : NormalStorage
Name                        : 15260861925810
ItemName                    : VM;iaasvmcontainer;RGName1;V2VM
RecoveryPointId             : /subscriptions/XX/resourceGroups/ RGName1/providers/Microsoft.RecoveryServices/vaults/testvault/backupFabrics/Azure/protectionContainers/IaasVMContainer;iaasvmcontainer;RGName1;V2VM/protectedItems/VM;iaasvmcontainer; RGName1;V2VM/recoveryPoints/15260861925810
RecoveryPointType           : AppConsistent
RecoveryPointTime           : 4/23/2016 5:02:04 PM
WorkloadType                : AzureVM
ContainerName               : IaasVMContainer;iaasvmcontainer; RGName1;V2VM
ContainerType               : AzureVM
BackupManagementType        : AzureVM
```



### <a name="restore-hello-disks"></a>Przywróć hello dysków
Użyj hello  **[AzureRmRecoveryServicesBackupItem przywracania](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/restore-azurermrecoveryservicesbackupitem)**  toorestore polecenia cmdlet element kopii zapasowej danych i konfiguracji tooa punktu odzyskiwania. Po zidentyfikowaniu punkt odzyskiwania, używać go jako wartość hello hello **- RecoveryPoint** parametru. W hello poprzedniej przykładowy kod **$rp [0]** został toouse punktu odzyskiwania hello. W powitania po przykładowy kod **$rp [0]** jest toouse punktu odzyskiwania hello przywracania dysku hello.

toorestore hello informacje o dyskach i konfiguracji:

```
PS C:\> $restorejob = Restore-AzureRmRecoveryServicesBackupItem -RecoveryPoint $rp[0] -StorageAccountName "DestAccount" -StorageAccountResourceGroupName "DestRG"
PS C:\> $restorejob
WorkloadName     Operation          Status               StartTime                 EndTime            JobID
------------     ---------          ------               ---------                 -------          ----------
V2VM              Restore           InProgress           4/23/2016 5:00:30 PM                        cf4b3ef5-2fac-4c8e-a215-d2eba4124f27
```

Użyj hello  **[AzureRmRecoveryServicesBackupJob oczekiwania](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/wait-azurermrecoveryservicesbackupjob)**  toowait polecenia cmdlet dla toocomplete zadania przywracania hello.

```
PS C:\> Wait-AzureRmRecoveryServicesBackupJob -Job $restorejob -Timeout 43200
```

Po zakończeniu zadania przywracania hello Użyj hello  **[Get-AzureRmRecoveryServicesBackupJobDetails](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/get-azurermrecoveryservicesbackupjobdetails)**  polecenia cmdlet tooget hello szczegóły hello operację przywracania. Witaj JobDetails właściwości ma hello informacje potrzebne toorebuild hello maszyny Wirtualnej.

```
PS C:\> $restorejob = Get-AzureRmRecoveryServicesBackupJob -Job $restorejob
PS C:\> $details = Get-AzureRmRecoveryServicesBackupJobDetails -Job $restorejob
```

Po przywróceniu dysków hello Przejdź toohello następnej sekcji toocreate hello maszyny Wirtualnej.

## <a name="create-a-vm-from-restored-disks"></a>Utwórz maszynę Wirtualną z przywróconą dysków
Po przywróceniu hello dysków, użyj toocreate te kroki i skonfiguruj hello maszyny wirtualnej z dysku.

> [!NOTE]
> toocreate szyfrowane maszyn wirtualnych z przywróconą dysków, roli użytkownika Azure musi mieć uprawnienie tooperform hello akcji, **Microsoft.KeyVault/vaults/deploy/action**. Jeśli rola użytkownika nie ma to uprawnienie, utworzyć niestandardową rolę za pomocą tej akcji. Aby uzyskać więcej informacji, zobacz [niestandardowych ról w Azure RBAC](../active-directory/role-based-access-control-custom-roles.md).
>
>

1. Zapytanie hello przywrócona właściwości dysku hello szczegóły zadania.

  ```
  PS C:\> $properties = $details.properties
  PS C:\> $storageAccountName = $properties["Target Storage Account Name"]
  PS C:\> $containerName = $properties["Config Blob Container Name"]
  PS C:\> $blobName = $properties["Config Blob Name"]
  ```

2. Ustaw kontekst magazynu Azure hello i przywrócenie pliku konfiguracji JSON hello.

    ```
    PS C:\> Set-AzureRmCurrentStorageAccount -Name $storageaccountname -ResourceGroupName "testvault"
    PS C:\> $destination_path = "C:\vmconfig.json"
    PS C:\> Get-AzureStorageBlobContent -Container $containerName -Blob $blobName -Destination $destination_path
    PS C:\> $obj = ((Get-Content -Path $destination_path -Raw -Encoding Unicode)).TrimEnd([char]0x00) | ConvertFrom-Json
    ```

3. Użyj konfiguracji JSON hello plik konfiguracji maszyny Wirtualnej hello toocreate.

    ```
   PS C:\> $vm = New-AzureRmVMConfig -VMSize $obj.'properties.hardwareProfile'.vmSize -VMName "testrestore"
    ```

4. Dołącz hello dysk systemu operacyjnego i dysków z danymi. W zależności od konfiguracji hello maszyn wirtualnych kliknij na powitania odpowiednie łącze tooview odpowiednich poleceń cmdlet: 
    - [Które nie są zarządzane, niezaszyfrowane maszyny wirtualne](#non-managed-non-encrypted-vms)
    - [Zaszyfrowane, które nie są zarządzane maszyn wirtualnych (tylko BEK)](#non-managed-encrypted-vms-bek-only)
    - [Maszyny wirtualne zaszyfrowane, które nie są zarządzane (BEK i KEK)](#non-managed-encrypted-vms-bek-and-kek)
    - [Zarządzane niezaszyfrowane maszyny wirtualne](#managed-non-encrypted-vms)
    - [Zarządzane, zaszyfrowanych maszyn wirtualnych (BEK i KEK)](#managed-encrypted-vms-bek-and-kek)
    
    #### <a name="non-managed-non-encrypted-vms"></a>Które nie są zarządzane, niezaszyfrowane maszyny wirtualne

    Użyj hello następujące przykładowe niezarządzanych, niezaszyfrowane maszyn wirtualnych.

    ```
    PS C:\> Set-AzureRmVMOSDisk -VM $vm -Name "osdisk" -VhdUri $obj.'properties.StorageProfile'.osDisk.vhd.Uri -CreateOption "Attach"
    PS C:\> $vm.StorageProfile.OsDisk.OsType = $obj.'properties.StorageProfile'.OsDisk.OsType
    PS C:\> foreach($dd in $obj.'properties.StorageProfile'.DataDisks)
    {
    $vm = Add-AzureRmVMDataDisk -VM $vm -Name "datadisk1" -VhdUri $dd.vhd.Uri -DiskSizeInGB 127 -Lun $dd.Lun -CreateOption "Attach"
    }
    ```

    #### <a name="non-managed-encrypted-vms-bek-only"></a>Zaszyfrowane, które nie są zarządzane maszyn wirtualnych (tylko BEK)

    Dla niezarządzanych, zaszyfrowane maszyn wirtualnych (szyfrowane tylko przy użyciu BEK) należy magazynu kluczy tajnych toohello hello toorestore przed dołączeniem dysków. Aby uzyskać więcej informacji, zobacz artykuł hello [przywrócić zaszyfrowanych maszyny wirtualnej z punktu odzyskiwania kopia zapasowa Azure](backup-azure-restore-key-secret.md). następujące przykładowe Hello pokazuje, jak tooattach systemu operacyjnego i dysków z danymi dla szyfrowane maszyn wirtualnych.

    ```
    PS C:\> $dekUrl = "https://ContosoKeyVault.vault.azure.net:443/secrets/ContosoSecret007/xx000000xx0849999f3xx30000003163"
    PS C:\> $keyVaultId = "/subscriptions/abcdedf007-4xyz-1a2b-0000-12a2b345675c/resourceGroups/ContosoRG108/providers/Microsoft.KeyVault/vaults/ContosoKeyVault"
    PS C:\> Set-AzureRmVMOSDisk -VM $vm -Name "osdisk" -VhdUri $obj.'properties.storageProfile'.osDisk.vhd.uri -DiskEncryptionKeyUrl $dekUrl -DiskEncryptionKeyVaultId $keyVaultId -CreateOption "Attach" -Windows
    PS C:\> $vm.StorageProfile.OsDisk.OsType = $obj.'properties.storageProfile'.osDisk.osType
    PS C:\> foreach($dd in $obj.'properties.storageProfile'.dataDisks)
     {
     $vm = Add-AzureRmVMDataDisk -VM $vm -Name "datadisk1" -VhdUri $dd.vhd.Uri -DiskSizeInGB 127 -Lun $dd.Lun -CreateOption "Attach"
     }
    ```

    #### <a name="non-managed-encrypted-vms-bek-and-kek"></a>Maszyny wirtualne zaszyfrowane, które nie są zarządzane (BEK i KEK)

    Dla niezarządzanych, zaszyfrowane maszyn wirtualnych (szyfrowane przy użyciu BEK i KEK) należy toorestore hello klucza i magazyn kluczy tajnych toohello przed dołączeniem dysków. Aby uzyskać więcej informacji, zobacz artykuł hello [przywrócić zaszyfrowanych maszyny wirtualnej z punktu odzyskiwania kopia zapasowa Azure](backup-azure-restore-key-secret.md). następujące przykładowe Hello pokazuje, jak tooattach systemu operacyjnego i dysków z danymi dla szyfrowane maszyn wirtualnych.

    ```
    PS C:\> $dekUrl = "https://ContosoKeyVault.vault.azure.net:443/secrets/ContosoSecret007/xx000000xx0849999f3xx30000003163"
    PS C:\> $kekUrl = "https://ContosoKeyVault.vault.azure.net:443/keys/ContosoKey007/x9xxx00000x0000x9b9949999xx0x006"
    PS C:\> $keyVaultId = "/subscriptions/abcdedf007-4xyz-1a2b-0000-12a2b345675c/resourceGroups/ContosoRG108/providers/Microsoft.KeyVault/vaults/ContosoKeyVault"
    PS C:\> Set-AzureRmVMOSDisk -VM $vm -Name "osdisk" -VhdUri $obj.'properties.storageProfile'.osDisk.vhd.uri -DiskEncryptionKeyUrl $dekUrl -DiskEncryptionKeyVaultId $keyVaultId -KeyEncryptionKeyUrl $kekUrl -KeyEncryptionKeyVaultId $keyVaultId -CreateOption "Attach" -Windows
    PS C:\> $vm.StorageProfile.OsDisk.OsType = $obj.'properties.storageProfile'.osDisk.osType
    PS C:\> foreach($dd in $obj.'properties.storageProfile'.dataDisks)
     {
     $vm = Add-AzureRmVMDataDisk -VM $vm -Name "datadisk1" -VhdUri $dd.vhd.Uri -DiskSizeInGB 127 -Lun $dd.Lun -CreateOption "Attach"
     }
    ```

    #### <a name="managed-non-encrypted-vms"></a>Zarządzane niezaszyfrowane maszyny wirtualne

    Dla zarządzanych maszyn wirtualnych z systemem innym niż zaszyfrowane będzie konieczne toocreate zarządzane dysków z magazynu obiektów blob, a następnie dołącz hello dysków. Aby uzyskać szczegółowe informacje, zobacz artykuł hello [dołączyć tooa dysku danych maszyny Wirtualnej systemu Windows przy użyciu programu PowerShell](../virtual-machines/windows/attach-disk-ps.md). powitania po przykładowy kod pokazuje, jak tooattach hello dysków z danymi dla zarządzanych niezaszyfrowane maszyn wirtualnych.

    ```
    PS C:\> $storageType = "StandardLRS"
    PS C:\> $osDiskName = $vm.Name + "_osdisk"
    PS C:\> $osVhdUri = $obj.'properties.storageProfile'.osDisk.vhd.uri
    PS C:\> $diskConfig = New-AzureRmDiskConfig -AccountType $storageType -Location "West US" -CreateOption Import -SourceUri $osVhdUri
    PS C:\> $osDisk = New-AzureRmDisk -DiskName $osDiskName -Disk $diskConfig -ResourceGroupName "test"
    PS C:\> Set-AzureRmVMOSDisk -VM $vm -ManagedDiskId $osDisk.Id -CreateOption "Attach" -Windows
    PS C:\> foreach($dd in $obj.'properties.storageProfile'.dataDisks)
     {
     $dataDiskName = $vm.Name + $dd.name ;
     $dataVhdUri = $dd.vhd.uri ;
     $dataDiskConfig = New-AzureRmDiskConfig -AccountType $storageType -Location "West US" -CreateOption Import -SourceUri $dataVhdUri ;
     $dataDisk2 = New-AzureRmDisk -DiskName $dataDiskName -Disk $dataDiskConfig -ResourceGroupName "test" ;
     Add-AzureRmVMDataDisk -VM $vm -Name $dataDiskName -ManagedDiskId $dataDisk2.Id -Lun $dd.Lun -CreateOption "Attach"
    }
    ```

    #### <a name="managed-encrypted-vms-bek-and-kek"></a>Zarządzane, zaszyfrowanych maszyn wirtualnych (BEK i KEK)

    Dla zarządzanych zaszyfrowanych maszyn wirtualnych (szyfrowane przy użyciu BEK i KEK) będzie konieczne toocreate zarządzane dysków z magazynu obiektów blob, a następnie dołącz hello dysków. Aby uzyskać szczegółowe informacje, zobacz artykuł hello [dołączyć tooa dysku danych maszyny Wirtualnej systemu Windows przy użyciu programu PowerShell](../virtual-machines/windows/attach-disk-ps.md). Witaj następujący przykładowy kod przedstawia sposób tooattach hello dysków z danymi dla zarządzanych zaszyfrowanych maszyn wirtualnych.

     ```
    PS C:\> $dekUrl = "https://ContosoKeyVault.vault.azure.net:443/secrets/ContosoSecret007/xx000000xx0849999f3xx30000003163"
    PS C:\> $kekUrl = "https://ContosoKeyVault.vault.azure.net:443/keys/ContosoKey007/x9xxx00000x0000x9b9949999xx0x006"
    PS C:\> $keyVaultId = "/subscriptions/abcdedf007-4xyz-1a2b-0000-12a2b345675c/resourceGroups/ContosoRG108/providers/Microsoft.KeyVault/vaults/ContosoKeyVault"
    PS C:\> $storageType = "StandardLRS"
    PS C:\> $osDiskName = $vm.Name + "_osdisk"
    PS C:\> $osVhdUri = $obj.'properties.storageProfile'.osDisk.vhd.uri
    PS C:\> $diskConfig = New-AzureRmDiskConfig -AccountType $storageType -Location "West US" -CreateOption Import -SourceUri $osVhdUri
    PS C:\> $osDisk = New-AzureRmDisk -DiskName $osDiskName -Disk $diskConfig -ResourceGroupName "test"
    PS C:\> Set-AzureRmVMOSDisk -VM $vm -ManagedDiskId $osDisk.Id -DiskEncryptionKeyUrl $dekUrl -DiskEncryptionKeyVaultId $keyVaultId -KeyEncryptionKeyUrl $kekUrl -KeyEncryptionKeyVaultId $keyVaultId -CreateOption "Attach" -Windows
    PS C:\> foreach($dd in $obj.'properties.storageProfile'.dataDisks)
     {
     $dataDiskName = $vm.Name + $dd.name ;
     $dataVhdUri = $dd.vhd.uri ;
     $dataDiskConfig = New-AzureRmDiskConfig -AccountType $storageType -Location "West US" -CreateOption Import -SourceUri $dataVhdUri ;
     $dataDisk2 = New-AzureRmDisk -DiskName $dataDiskName -Disk $dataDiskConfig -ResourceGroupName "test" ;
     Add-AzureRmVMDataDisk -VM $vm -Name $dataDiskName -ManagedDiskId $dataDisk2.Id -Lun $dd.Lun -CreateOption "Attach"
     }
    ```

5. Określ ustawienia sieciowe hello.

    ```
    PS C:\> $nicName="p1234"
    PS C:\> $pip = New-AzureRmPublicIpAddress -Name $nicName -ResourceGroupName "test" -Location "WestUS" -AllocationMethod Dynamic
    PS C:\> $vnet = Get-AzureRmVirtualNetwork -Name "testvNET" -ResourceGroupName "test"
    PS C:\> $nic = New-AzureRmNetworkInterface -Name $nicName -ResourceGroupName "test" -Location "WestUS" -SubnetId $vnet.Subnets[$subnetindex].Id -PublicIpAddressId $pip.Id
    PS C:\> $vm=Add-AzureRmVMNetworkInterface -VM $vm -Id $nic.Id
    ```
6. Utwórz maszynę wirtualną hello.

    ```    
    PS C:\> New-AzureRmVM -ResourceGroupName "test" -Location "WestUS" -VM $vm
    ```

## <a name="next-steps"></a>Następne kroki
Jeśli wolisz toouse tooengage programu PowerShell z zasobów platformy Azure, zobacz artykuł PowerShell hello, [wdrażanie i zarządzanie kopia zapasowa systemu Windows Server](backup-client-automation.md). Jeśli zarządzasz kopii zapasowych programu DPM, zobacz artykuł hello, [wdrażanie i zarządzanie kopii zapasowej programu DPM](backup-dpm-automation.md). Mieć obu tych artykułach wersji dla wdrożenia usługi Resource Manager oraz wdrożenia klasycznego.  
