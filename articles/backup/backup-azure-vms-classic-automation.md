---
title: "aaaDeploy i zarządzanie kopiami zapasowymi dla maszyn wirtualnych platformy Azure przy użyciu programu PowerShell | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toodeploy i zarządzać nimi za pomocą programu PowerShell usługi Kopia zapasowa Azure."
services: backup
documentationcenter: 
author: markgalioto
manager: carmonm
editor: 
ms.assetid: 2e24b1d9-4375-4049-a28d-e3bc01152f32
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 8/2/2017
ms.author: markgal;trinadhk;jimpark
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: f3ecd3f94c5e3e8fc8018e8786302edd4847744b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="use-azurermbackup-cmdlets-tooback-up-virtual-machines"></a>Użyj tooback poleceń cmdlet AzureRM.Backup zapasowych maszyn wirtualnych
> [!div class="op_single_selector"]
> * [Resource Manager](backup-azure-vms-automation.md)
> * [Wdrożenie klasyczne](backup-azure-vms-classic-automation.md)
>
>

W tym artykule opisano sposób toouse programu Azure PowerShell kopii zapasowych i odzyskiwania maszyn wirtualnych platformy Azure. Platforma Azure oferuje dwa różne modele wdrażania związane z tworzeniem zasobów i pracą z nimi: model wdrażania przy użyciu usługi Resource Manager i model klasyczny. W tym artykule omówiono przy użyciu hello Classic wdrażania modelu tooback zapasowej magazyn kopii zapasowych tooa danych. Jeśli nie utworzono magazyn kopii zapasowych w ramach subskrypcji, zobacz hello wersja Menedżera zasobów tego artykułu, [AzureRM.RecoveryServices.Backup użyj polecenia cmdlet tooback zapasowe](backup-azure-vms-automation.md). Firma Microsoft zaleca, aby większości nowych wdrożeń korzystać hello modelu Resource Manager.

> [!IMPORTANT]
> Teraz można uaktualnić Twoje Magazyny usług tooRecovery magazynów kopii zapasowych. Aby uzyskać więcej informacji, zobacz artykuł hello [uaktualnienia tooa magazynu kopii zapasowej, Magazyn usług odzyskiwania i](backup-azure-upgrade-backup-to-recovery-services.md). Firma Microsoft zachęca tooupgrade Magazyny usług tooRecovery magazyny kopii zapasowych.<br/> Po 15 października 2017 nie można użyć magazyny kopii zapasowych toocreate środowiska PowerShell. **Do 1 listopada 2017 r.**:
>- Wszystkie pozostałe magazyny kopii zapasowych zostanie automatycznie uaktualniony tooRecovery Magazyny usług.
>- Użytkownik nie będzie możliwe tooaccess danych kopii zapasowych w portalu klasycznym hello. Zamiast tego użyj hello Azure tooaccess portalu tej kopii zapasowej w Magazyny usług odzyskiwania.
>

## <a name="concepts"></a>Pojęcia
Ten artykuł zawiera informacje o określonym toohello poleceń cmdlet programu PowerShell używanych tooback zapasowych maszyn wirtualnych. Aby uzyskać informacje wprowadzające dotyczące ochrony maszyn wirtualnych platformy Azure, zobacz [Zaplanuj infrastrukturę kopii zapasowej maszyny Wirtualnej na platformie Azure](backup-azure-vms-introduction.md).

> [!NOTE]
> Przed rozpoczęciem przeczytaj hello [wymagania wstępne](backup-azure-vms-prepare.md) wymagane toowork z usługi Kopia zapasowa Azure i hello [ograniczenia](backup-azure-vms-prepare.md#limitations-when-backing-up-and-restoring-a-vm) bieżącego rozwiązania kopii zapasowej hello maszyny Wirtualnej.
>
>

toouse PowerShell efektywnie zająć chwilę toounderstand hello hierarchię obiektów i z jakiej lokalizacji toostart.

![Hierarchia obiektów](./media/backup-azure-vms-classic-automation/object-hierarchy.png)

Witaj dwóch przepływów najważniejszych są włączania ochrony dla maszyny Wirtualnej i przywrócić dane z punktu odzyskiwania. Witaj ten artykuł koncentruje się toohelp staje się doświadczenie w pracy z tooenable poleceń cmdlet programu PowerShell hello tych dwóch scenariuszy.

## <a name="setup-and-registration"></a>Instalację i rejestrację
toobegin:

1. [Pobierz najnowsze PowerShell](https://github.com/Azure/azure-powershell/releases) (minimalna wersja wymagana jest: 1.0.0)
2. Znajdź hello programu PowerShell usługi Azure Backup dostępnych poleceń cmdlet, wpisując następujące polecenie hello:

```
PS C:\> Get-Command *azurermbackup*

CommandType     Name                                               Version    Source
-----------     ----                                               -------    ------
Cmdlet          Backup-AzureRmBackupItem                           1.0.1      AzureRM.Backup
Cmdlet          Disable-AzureRmBackupProtection                    1.0.1      AzureRM.Backup
Cmdlet          Enable-AzureRmBackupContainerReregistration        1.0.1      AzureRM.Backup
Cmdlet          Enable-AzureRmBackupProtection                     1.0.1      AzureRM.Backup
Cmdlet          Get-AzureRmBackupContainer                         1.0.1      AzureRM.Backup
Cmdlet          Get-AzureRmBackupItem                              1.0.1      AzureRM.Backup
Cmdlet          Get-AzureRmBackupJob                               1.0.1      AzureRM.Backup
Cmdlet          Get-AzureRmBackupJobDetails                        1.0.1      AzureRM.Backup
Cmdlet          Get-AzureRmBackupProtectionPolicy                  1.0.1      AzureRM.Backup
Cmdlet          Get-AzureRmBackupRecoveryPoint                     1.0.1      AzureRM.Backup
Cmdlet          Get-AzureRmBackupVault                             1.0.1      AzureRM.Backup
Cmdlet          Get-AzureRmBackupVaultCredentials                  1.0.1      AzureRM.Backup
Cmdlet          New-AzureRmBackupProtectionPolicy                  1.0.1      AzureRM.Backup
Cmdlet          New-AzureRmBackupRetentionPolicyObject             1.0.1      AzureRM.Backup
Cmdlet          New-AzureRmBackupVault                             1.0.1      AzureRM.Backup
Cmdlet          Register-AzureRmBackupContainer                    1.0.1      AzureRM.Backup
Cmdlet          Remove-AzureRmBackupProtectionPolicy               1.0.1      AzureRM.Backup
Cmdlet          Remove-AzureRmBackupVault                          1.0.1      AzureRM.Backup
Cmdlet          Restore-AzureRmBackupItem                          1.0.1      AzureRM.Backup
Cmdlet          Set-AzureRmBackupProtectionPolicy                  1.0.1      AzureRM.Backup
Cmdlet          Set-AzureRmBackupVault                             1.0.1      AzureRM.Backup
Cmdlet          Stop-AzureRmBackupJob                              1.0.1      AzureRM.Backup
Cmdlet          Unregister-AzureRmBackupContainer                  1.0.1      AzureRM.Backup
Cmdlet          Wait-AzureRmBackupJob                              1.0.1      AzureRM.Backup
```

Witaj następujące ustawienia i zadania rejestracji można zautomatyzować przy użyciu programu PowerShell:

* Tworzenie magazynu kopii zapasowych
* Rejestrowanie hello maszyn wirtualnych z hello usługi Kopia zapasowa Azure

### <a name="create-a-backup-vault"></a>Tworzenie magazynu kopii zapasowych
> [!WARNING]
> W przypadku klientów przy kopia zapasowa Azure powitania po raz pierwszy należy tooregister hello kopia zapasowa Azure dostawcy toobe używane w ramach subskrypcji. Można to zrobić, uruchamiając następujące polecenie hello: Register-AzureRmResourceProvider - ProviderNamespace "Microsoft.Backup"
>
>

Można utworzyć nowy magazyn kopii zapasowych za pomocą hello **AzureRmBackupVault nowy** polecenia cmdlet. Hello magazynu kopii zapasowych jest zasobem ARM, więc należy tooplace go w grupie zasobów. W konsoli programu Azure PowerShell z podwyższonym poziomem uprawnień uruchom następujące polecenia hello:

```
PS C:\> New-AzureRmResourceGroup –Name “test-rg” –Location “West US”
PS C:\> $backupvault = New-AzureRmBackupVault –ResourceGroupName “test-rg” –Name “test-vault” –Region “West US” –Storage GeoRedundant
```

Można uzyskać listę wszystkich magazynów kopii zapasowych hello w ramach danej subskrypcji przy użyciu hello **Get-AzureRmBackupVault** polecenia cmdlet.

> [!NOTE]
> Jest wygodną toostore hello magazynu kopii zapasowych obiekt w zmiennej. Obiekt magazynu Hello jest potrzebny jako dane wejściowe dla wielu poleceń cmdlet narzędzia Kopia zapasowa Azure.
>
>

### <a name="registering-hello-vms"></a>Rejestrowanie hello maszyny wirtualne
pierwszy krok Hello w kierunku Konfigurowanie tworzenia kopii zapasowych w usłudze Kopia zapasowa Azure jest tooregister Twojego komputera lub maszyny Wirtualnej w magazynie usługi Kopia zapasowa Azure. Witaj **AzureRmBackupContainer rejestru** polecenie cmdlet pobiera dane wejściowe hello maszyny wirtualne Azure IaaS i rejestruje go wraz hello określonego magazynu. Operacja rejestracji Hello kojarzy hello Azure maszyny wirtualnej z magazynu kopii zapasowych hello i śledzi hello maszyny Wirtualnej za pośrednictwem hello cyklu tworzenia kopii zapasowej.

Rejestrowanie maszyny Wirtualnej z hello usługi Azure Backup tworzy obiekt kontenerem najwyższego poziomu. Kontener zwykle zawiera wiele elementów, które można utworzyć kopię zapasową, ale w przypadku hello maszyn wirtualnych będzie tylko jeden element kopii zapasowej hello kontenera.

```
PS C:\> $registerjob = Register-AzureRmBackupContainer -Vault $backupvault -Name "testvm" -ServiceName "testvm"
```

## <a name="backup-azure-vms"></a>Tworzenie kopii zapasowych maszyn wirtualnych platformy Azure
### <a name="create-a-protection-policy"></a>Tworzenie zasad ochrony
Nie jest obowiązkowe toocreate nową ochrony zasad toostart kopię zapasową maszyn wirtualnych. Magazyn Hello jest dostarczany z "Domyślne zasady" mogą być używane tooquickly Włączanie ochrony, a następnie edytować później za pomocą hello szczegółów prawym. Listę dostępnych w magazynie hello zasad hello można uzyskać za pomocą hello **Get-AzureRmBackupProtectionPolicy** polecenia cmdlet:

```
PS C:\> Get-AzureRmBackupProtectionPolicy -Vault $backupvault

Name                      Type               ScheduleType       BackupTime
----                      ----               ------------       ----------
DefaultPolicy             AzureVM            Daily              26-Aug-15 12:30:00 AM
```

> [!NOTE]
> Strefa czasowa Hello hello BackupTime pola w programie PowerShell jest czasem UTC. Jednak podczas wykonywania kopii zapasowej hello jest wyświetlany w hello portalu Azure, strefy czasowej hello jest wyrównany tooyour systemu lokalnego, wraz z przesunięciem hello UTC.
>
>

Zasady tworzenia kopii zapasowej jest skojarzony z co najmniej jedne zasady przechowywania. zasady przechowywania Hello określają, jak długo punkt odzyskiwania jest przechowywany z usługi Kopia zapasowa Azure. Witaj **AzureRmBackupRetentionPolicy nowy** polecenie cmdlet tworzy obiekty programu PowerShell, zawierających informacje o zasadach przechowywania. Te obiekty zasad przechowywania są używane jako danych wejściowych toohello *AzureRmBackupProtectionPolicy nowy* polecenia cmdlet, lub bezpośrednio z hello *AzureRmBackupProtection Włącz* polecenia cmdlet.

Zasady tworzenia kopii zapasowej definiuje kiedy i jak często hello kopii zapasowej elementu odbywa się. Witaj **AzureRmBackupProtectionPolicy nowy** polecenie cmdlet tworzy obiekt programu PowerShell, która przechowuje informacje o zasadach tworzenia kopii zapasowej. Witaj zasad tworzenia kopii zapasowej jest używany jako wejściowych toohello *AzureRmBackupProtection Włącz* polecenia cmdlet.

```
PS C:\> $Daily = New-AzureRmBackupRetentionPolicyObject -DailyRetention -Retention 30
PS C:\> $newpolicy = New-AzureRmBackupProtectionPolicy -Name DailyBackup01 -Type AzureVM -Daily -BackupTime ([datetime]"3:30 PM") -RetentionPolicy $Daily -Vault $backupvault

Name                      Type               ScheduleType       BackupTime
----                      ----               ------------       ----------
DailyBackup01             AzureVM            Daily              01-Sep-15 3:30:00 PM
```

### <a name="enable-protection"></a>Włączanie ochrony
Włączanie ochrony obejmuje dwa obiekty — Witaj elementu i hello zasad, a oba toohello toobelong potrzeby sam magazyn. Po hello zasady został skojarzony z elementem hello, przepływ pracy tworzenia kopii zapasowej hello będzie zaczną działać na powitania zdefiniowanym harmonogramem.

```
PS C:\> Get-AzureRmBackupContainer -Type AzureVM -Status Registered -Vault $backupvault | Get-AzureRmBackupItem | Enable-AzureRmBackupProtection -Policy $newpolicy
```

### <a name="initial-backup"></a>Początkowa kopia zapasowa
harmonogram tworzenia kopii zapasowych Hello zajmie się czynności hello wstępny pełny kopii dla elementu hello i hello przyrostowej kopii hello kolejnych kopii zapasowych. Jednak jeśli chcesz tooforce hello początkowej kopii zapasowej toohappen w określonym czasie, lub nawet natychmiast Użyj hello **AzureRmBackupItem kopii zapasowej** polecenia cmdlet:

```
PS C:\> $container = Get-AzureRmBackupContainer -Vault $backupvault -Type AzureVM -Name "testvm"
PS C:\> $backupjob = Get-AzureRmBackupItem -Container $container | Backup-AzureRmBackupItem
PS C:\> $backupjob

WorkloadName    Operation       Status          StartTime              EndTime
------------    ---------       ------          ---------              -------
testvm          Backup          InProgress      01-Sep-15 12:24:01 PM  01-Jan-01 12:00:00 AM
```

> [!NOTE]
> Witaj strefę czasową hello wartości StartTime i EndTime pól w programie PowerShell jest UTC. Jednak podczas hello podobne informacje są wyświetlane w portalu Azure hello, strefa czasowa hello jest wyrównany tooyour zegara systemu lokalnego.
>
>

### <a name="monitoring-a-backup-job"></a>Monitorowanie zadania tworzenia kopii zapasowej
Większość długotrwałej operacji w usłudze Kopia zapasowa Azure są sporządzony według wzoru jako zadanie. Dzięki temu postępu łatwe tootrack bez konieczności hello tookeep Otwieranie portalu Azure przez cały czas.

tooget hello najnowszy stan zadania w toku, użyj hello **Get-AzureRmBackupJob** polecenia cmdlet.

```
PS C:\> $joblist = Get-AzureRmBackupJob -Vault $backupvault -Status InProgress
PS C:\> $joblist[0]

WorkloadName    Operation       Status          StartTime              EndTime
------------    ---------       ------          ---------              -------
testvm          Backup          InProgress      01-Sep-15 12:24:01 PM  01-Jan-01 12:00:00 AM
```

Zamiast sondowania te zadania na zakończenie — czyli kod niepotrzebne, dodatkowe — jest prostsze hello toouse **AzureRmBackupJob oczekiwania** polecenia cmdlet. Używanego w skrypcie, polecenia cmdlet hello wstrzyma wykonywania hello dopóki hello określona wartość limitu czasu jest osiągana albo hello zadanie zostało ukończone.

```
PS C:\> Wait-AzureRmBackupJob -Job $joblist[0] -Timeout 43200
```


## <a name="restore-an-azure-vm"></a>Przywracanie maszyny Wirtualnej platformy Azure
W kolejności toorestore dane kopii zapasowej należy tooidentify hello kopii zapasowej elementu i hello punkt odzyskiwania, który zawiera dane w momencie hello. Te informacje są podane toohello AzureRmBackupItem przywracania polecenia cmdlet tooinitiate przywracania danych z konta klienta hello magazynu toohello.

### <a name="select-hello-vm"></a>Wybierz hello maszyny Wirtualnej
obiekt programu PowerShell hello tooget, który identyfikuje hello elementu prawo kopii zapasowej, należy toostart z hello kontenera w magazynie hello i przechodzić w dół hierarchii obiektów. tooselect hello kontener, który reprezentuje hello maszyny Wirtualnej, użyj hello **Get-AzureRmBackupContainer** polecenia cmdlet i przekazać w potoku tego toohello **Get-AzureRmBackupItem** polecenia cmdlet.

```
PS C:\> $backupitem = Get-AzureRmBackupContainer -Vault $backupvault -Type AzureVM -name "testvm" | Get-AzureRmBackupItem
```

### <a name="choose-a-recovery-point"></a>Wybierz punkt odzyskiwania
Można teraz wyświetlić listę wszystkich punktów odzyskiwania hello hello elementu kopii zapasowej za pomocą hello **Get-AzureRmBackupRecoveryPoint** polecenia cmdlet i wybierz polecenie toorestore punktu odzyskiwania hello. Zazwyczaj użytkowników pobranie najnowszych hello *AppConsistent* punktu hello na liście.

```
PS C:\> $rp =  Get-AzureRmBackupRecoveryPoint -Item $backupitem
PS C:\> $rp

RecoveryPointId    RecoveryPointType  RecoveryPointTime      ContainerName
---------------    -----------------  -----------------      -------------
15273496567119     AppConsistent      01-Sep-15 12:27:38 PM  iaasvmcontainer;testvm;testv...
```

Zmienna Hello ```$rp``` jest tablicą punkty odzyskiwania dla hello zaznaczony element kopii zapasowej, posortowane w kolejności odwrotnej czas — Witaj najnowszy punkt odzyskiwania znajduje się pod indeksem 0. Użyj standardowych tablicy PowerShell indeksowania punkt odzyskiwania hello toopick. Na przykład: ```$rp[0]``` wybierze hello najnowszego punktu odzyskiwania.

### <a name="restoring-disks"></a>Przywracanie dysków
Brak klucza różnica między operacje przywracania hello wykonywane za pośrednictwem hello portalu Azure i przy użyciu programu Azure PowerShell. Przy użyciu programu PowerShell operacji przywracania hello zatrzymuje przy przywracaniu dysków hello i informacje o konfiguracji z hello punktu odzyskiwania. Nie tworzy maszynę wirtualną.

> [!WARNING]
> Witaj AzureRmBackupItem przywracania nie powoduje utworzenia maszyny Wirtualnej. Przywraca jedynie dyski hello toohello określono konto magazynu. Nie jest to hello takie samo zachowanie, które wystąpią w hello portalu Azure.
>
>

```
PS C:\> $restorejob = Restore-AzureRmBackupItem -StorageAccountName "DestAccount" -RecoveryPoint $rp[0]
PS C:\> $restorejob

WorkloadName    Operation       Status          StartTime              EndTime
------------    ---------       ------          ---------              -------
testvm          Restore         InProgress      01-Sep-15 1:14:01 PM   01-Jan-01 12:00:00 AM
```

Można uzyskać szczegółów hello hello operacji przywracania, używając hello **Get-AzureRmBackupJobDetails** polecenia cmdlet, po zakończeniu zadania przywracania hello. Witaj *szczegóły błędu* właściwość będzie mieć informacji hello potrzebne toorebuild hello maszyny Wirtualnej.

```
PS C:\> $restorejob = Get-AzureRmBackupJob -Job $restorejob
PS C:\> $details = Get-AzureRmBackupJobDetails -Job $restorejob
```

### <a name="build-hello-vm"></a>Tworzenie hello maszyny Wirtualnej
Hello tworzenia maszyny Wirtualnej poza hello przywrócić dysków jest możliwe za pomocą hello starszych poleceń cmdlet programu PowerShell do zarządzania usługi Azure, hello nowych szablonów usługi Azure Resource Manager lub nawet hello portalu Azure. W szybkim przykładzie pokazano, jak tooget miejsca przy użyciu poleceń cmdlet usługi Azure Service Management hello.

```
$properties  = $details.Properties

$storageAccountName = $properties["Target Storage Account Name"]
$containerName = $properties["Config Blob Container Name"]
$blobName = $properties["Config Blob Name"]

$keys = Get-AzureStorageKey -StorageAccountName $storageAccountName
$storageAccountKey = $keys.Primary
$storageContext = New-AzureStorageContext -StorageAccountName $storageAccountName -StorageAccountKey $storageAccountKey


$destination_path = "C:\Users\admin\Desktop\vmconfig.xml"
Get-AzureStorageBlobContent -Container $containerName -Blob $blobName -Destination $destination_path -Context $storageContext


$obj = [xml](((Get-Content -Path $destination_path -Encoding UniCode)).TrimEnd([char]0x00))
$pvr = $obj.PersistentVMRole
$os = $pvr.OSVirtualHardDisk
$dds = $pvr.DataVirtualHardDisks
$osDisk = Add-AzureDisk -MediaLocation $os.MediaLink -OS $os.OS -DiskName "panbhaosdisk"
$vm = New-AzureVMConfig -Name $pvr.RoleName -InstanceSize $pvr.RoleSize -DiskName $osDisk.DiskName

if (!($dds -eq $null))
{
    foreach($d in $dds.DataVirtualHardDisk)
    {
        $lun = 0
        if(!($d.Lun -eq $null))
        {
            $lun = $d.Lun
        }
        $name = "panbhadataDisk" + $lun
        Add-AzureDisk -DiskName $name -MediaLocation $d.MediaLink
        $vm | Add-AzureDataDisk -Import -DiskName $name -LUN $lun
    }
}

New-AzureVM -ServiceName "panbhasample" -Location "SouthEast Asia" -VM $vm
```

Aby uzyskać więcej informacji na temat toobuild Maszynę wirtualną z dysków hello przywrócone, przeczytaj o hello następującego polecenia cmdlet:

* [Dodaj AzureDisk](https://msdn.microsoft.com/library/azure/dn495252.aspx)
* [Nowe AzureVMConfig](https://msdn.microsoft.com/library/azure/dn495159.aspx)
* [Nowe AzureVM](https://msdn.microsoft.com/library/azure/dn495254.aspx)

## <a name="code-samples"></a>Przykłady kodu
### <a name="1-get-hello-completion-status-of-job-sub-tasks"></a>1. Pobierz stan ukończenia hello zadania podrzędne zadania
Stan ukończenia hello tootrack poszczególnych zadań podrzędnych, można użyć hello **Get-AzureRmBackupJobDetails** polecenia cmdlet:

```
PS C:\> $details = Get-AzureRmBackupJobDetails -JobId $backupjob.InstanceId -Vault $backupvault
PS C:\> $details.SubTasks

Name                                                        Status
----                                                        ------
Take Snapshot                                               Completed
Transfer data tooBackup vault                               InProgress
```

### <a name="2-create-a-dailyweekly-report-of-backup-jobs"></a>2. Tworzenie raportu codziennie/cotygodniowych zadań tworzenia kopii zapasowej
Administratorzy mają zwykle tooknow jakie zadania tworzenia kopii zapasowej został uruchomiony w hello ostatnich 24 godzinach, stan hello tych zadań tworzenia kopii zapasowej. Ponadto hello ilość danych przesyłanych zapewnia administratorom tooestimate sposób ich miesięcznego użycia danych. Poniższy skrypt Hello pobiera hello nieprzetworzone dane z hello usługi Kopia zapasowa Azure i wyświetla informacje hello w konsoli programu PowerShell hello.

```
param(  [Parameter(Mandatory=$True,Position=1)]
        [string]$backupvaultname,

        [Parameter(Mandatory=$False,Position=2)]
        [int]$numberofdays = 7)


#Initialize variables
$DAILYBACKUPSTATS = @()
$backupvault = Get-AzureRmBackupVault -Name $backupvaultname
$enddate = ([datetime]::Today).AddDays(1)
$startdate = ([datetime]::Today)

for( $i = 1; $i -le $numberofdays; $i++ )
{
    # We query one day at a time because pulling 7 days of data might be too much
    $dailyjoblist = Get-AzureRmBackupJob -Vault $backupvault -From $startdate -too$enddate -Type AzureVM -Operation Backup
    Write-Progress -Activity "Getting job information for hello last $numberofdays days" -Status "Day -$i" -PercentComplete ([int]([decimal]$i*100/$numberofdays))

    foreach( $job in $dailyjoblist )
    {
        #Extract hello information for hello reports
        $newstatsobj = New-Object System.Object
        $newstatsobj | Add-Member -Type NoteProperty -Name Date -Value $startdate
        $newstatsobj | Add-Member -Type NoteProperty -Name VMName -Value $job.WorkloadName
        $newstatsobj | Add-Member -Type NoteProperty -Name Duration -Value $job.Duration
        $newstatsobj | Add-Member -Type NoteProperty -Name Status -Value $job.Status

        $details = Get-AzureRmBackupJobDetails -Job $job
        $newstatsobj | Add-Member -Type NoteProperty -Name BackupSize -Value $details.Properties["Backup Size"]
        $DAILYBACKUPSTATS += $newstatsobj
    }

    $enddate = $enddate.AddDays(-1)
    $startdate = $startdate.AddDays(-1)
}

$DAILYBACKUPSTATS | Out-GridView
```

Jeśli chcesz tooadd wykresów dane wyjściowe raportu toothis możliwości nauki TechNet hello wpis w blogu [wykresów przy użyciu programu PowerShell](http://blogs.technet.com/b/richard_macdonald/archive/2009/04/28/3231887.aspx)

## <a name="next-steps"></a>Następne kroki
Jeśli wolisz przy użyciu programu PowerShell tooengage z zasobów platformy Azure, zapoznaj się artykuł PowerShell hello ochrony systemu Windows Server, [wdrażanie i zarządzanie kopia zapasowa systemu Windows Server](backup-client-automation-classic.md). Jest również artykuł programu PowerShell do zarządzania kopii zapasowych programu DPM, [wdrażanie i zarządzanie kopii zapasowej programu DPM](backup-dpm-automation-classic.md). Mieć obu tych artykułach wersji dla wdrożenia usługi Resource Manager oraz wdrożenia klasycznego.
