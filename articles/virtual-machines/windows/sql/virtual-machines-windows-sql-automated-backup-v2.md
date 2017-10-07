---
title: aaaAutomated v2 kopii zapasowej programu SQL Server 2016 maszyn wirtualnych platformy Azure | Dokumentacja firmy Microsoft
description: "Zawiera opis funkcji automatycznego tworzenia kopii zapasowej powitania dla programu SQL Server 2016 maszyn wirtualnych działających na platformie Azure. W tym artykule jest tooVMs określonego za pomocą hello Menedżera zasobów."
services: virtual-machines-windows
documentationcenter: na
author: rothja
manager: jhubbard
editor: 
tags: azure-resource-manager
ms.assetid: ebd23868-821c-475b-b867-06d4a2e310c7
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 04/05/2017
ms.author: jroth
ms.openlocfilehash: a322792fb22c76bfa74fafb711b8b1927a6e2b3a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="automated-backup-v2-for-sql-server-2016-azure-virtual-machines-resource-manager"></a>Automatycznego tworzenia kopii zapasowej w wersji 2 dla programu SQL Server 2016 maszyn wirtualnych platformy Azure (Resource Manager)

> [!div class="op_single_selector"]
> * [Program SQL Server 2014](virtual-machines-windows-sql-automated-backup.md)
> * [SQL Server 2016](virtual-machines-windows-sql-automated-backup-v2.md)

Automatyczne v2 kopii zapasowej automatycznie konfiguruje [tooMicrosoft zarządzanej kopii zapasowej Azure](https://msdn.microsoft.com/library/dn449496.aspx) dla wszystkich istniejących i nowych baz danych na maszynie Wirtualnej platformy Azure, uruchomione wersje programu SQL Server 2016 Standard, Enterprise lub dewelopera. Dzięki temu tooconfigure kopie zapasowe zwykłej bazy danych, które korzystać z magazynu trwałego obiektów blob platformy Azure. Automatyczne v2 kopii zapasowej zależy od hello [rozszerzenia agenta programu SQL Server IaaS](virtual-machines-windows-sql-server-agent-extension.md).

[!INCLUDE [learn-about-deployment-models](../../../../includes/learn-about-deployment-models-rm-include.md)]

## <a name="prerequisites"></a>Wymagania wstępne
toouse v2 automatyczna usługa Backup hello Przejrzyj następujące wymagania wstępne:

**System operacyjny**:

- Windows Server 2012 R2
- Windows Server 2016

**Wydanie wersji programu SQL Server**:

- SQL Server 2016 Standard
- SQL Server 2016 Enterprise
- SQL Server 2016 Developer

> [!IMPORTANT]
> Automatyczne v2 kopii zapasowej działa z programem SQL Server 2016. Jeśli używasz programu SQL Server 2014, można użyć automatycznego tworzenia kopii zapasowej v1 tooback zapasową baz danych. Aby uzyskać więcej informacji, zobacz [automatyczna usługa Backup SQL Server 2014 maszyn wirtualnych platformy Azure](virtual-machines-windows-sql-automated-backup.md).

**Baza danych konfiguracji**:

- Docelowymi bazami danych, należy użyć hello modelu odzyskiwania pełnego. Aby uzyskać więcej informacji dotyczących wpływu hello modelu odzyskiwania pełnego hello na wykonywanie kopii zapasowych, zobacz [hello kopii zapasowych w ramach modelu odzyskiwania pełnego](https://technet.microsoft.com/library/ms190217.aspx).
- Bazy danych systemu nie mają toouse modelu odzyskiwania pełnego. Jeśli potrzebujesz toobe kopii zapasowych dziennika poświęcony Model i MSDB, musi jednak używać modelu odzyskiwania pełnego.
- Docelowymi bazami danych musi znajdować się na powitania domyślnego wystąpienia programu SQL Server. Witaj IaaS rozszerzenie dotyczące programu SQL Server nie obsługuje nazwanych wystąpień.

**Model wdrożenia usługi Azure**:

- Resource Manager

> [!NOTE]
> Automatyczne kopie zapasowe opiera się na powitania **rozszerzenia agenta programu SQL Server IaaS**. Bieżący obrazów Galeria maszyny wirtualnej SQL dodać to rozszerzenie domyślnie. Aby uzyskać więcej informacji, zobacz [rozszerzenia agenta programu SQL Server IaaS](virtual-machines-windows-sql-server-agent-extension.md).

## <a name="settings"></a>Ustawienia
Witaj poniższej tabeli opisano opcje hello, które można skonfigurować do automatycznego tworzenia kopii zapasowej w wersji 2. kroki rzeczywista konfiguracja Hello się różnić w zależności od tego, czy używać hello portalu Azure lub poleceń programu Windows PowerShell dla usługi Azure.

### <a name="basic-settings"></a>Ustawienia podstawowe

| Ustawienie | Zakres (ustawienie domyślne) | Opis |
| --- | --- | --- |
| **Automatyczne kopie zapasowe** | Włącza/wyłącza (wyłączone) | Włącza lub wyłącza funkcję automatycznego tworzenia kopii zapasowej dla maszyny Wirtualnej platformy Azure, programem SQL Server 2016 Standard lub Enterprise. |
| **Okres przechowywania** | 1 do 30 dni (30 dni) | Witaj liczbę kopii zapasowych tooretain dni. |
| **Konto magazynu** | Konto magazynu Azure | Toouse konto magazynu Azure do przechowywania plików automatycznego tworzenia kopii zapasowej w magazynie obiektów blob. Kontener jest tworzony w tej lokalizacji toostore wszystkie pliki kopii zapasowej. Plik kopii zapasowej Hello konwencji nazewnictwa obejmuje hello daty, godziny i identyfikator GUID bazy danych. |
| **Szyfrowanie** |Włącza/wyłącza (wyłączone) | Włącza lub wyłącza funkcję szyfrowania. Po włączeniu szyfrowania hello używane certyfikaty toorestore hello w kopii zapasowej znajdują się w hello określony magazynu konta w hello sam **automaticbackup** przy użyciu kontenera hello tej samej konwencji nazewnictwa. Zmiana hasła hello nowego certyfikatu jest generowana za pomocą tego hasła, ale hello stary certyfikat pozostaje toorestore poprzednich kopii zapasowych. |
| **Hasło** |Tekst hasła | Hasło dla kluczy szyfrowania. Jest to tylko wymagane, jeśli jest włączone szyfrowanie. W kolejności toorestore zaszyfrowanej kopii zapasowej, trzeba hello prawidłowe hasło i powiązane certyfikatu, który został użyty w czasie hello hello tworzenia kopii zapasowej. |

### <a name="advanced-settings"></a>Ustawienia zaawansowane

| Ustawienie | Zakres (ustawienie domyślne) | Opis |
| --- | --- | --- |
| **Kopie zapasowe bazy danych systemu** | Włącza/wyłącza (wyłączone) | Po włączeniu tej funkcji będzie również wykonać kopię zapasową hello systemowych baz danych: Master, MSDB i modelu. Witaj MSDB i baz danych modelu Sprawdź, czy są w trybie odzyskiwania pełnego Jeśli chcesz, aby podjąć toobe kopii zapasowych dziennika. Kopie zapasowe dziennika nigdy nie są wykonywane dla głównego. A nie kopii zapasowych są wykonywane dla bazy danych TempDB. |
| **Harmonogram tworzenia kopii zapasowych** | Ręczne/automatycznego (automatycznego) | Domyślnie hello harmonogram tworzenia kopii zapasowych będzie automatycznie ustalana na podstawie hello wzrostu dziennika. Ręczne harmonogram tworzenia kopii zapasowych umożliwia przedział czasu hello hello użytkownika toospecify kopii zapasowych. W takim przypadku tylko potrwa kopii zapasowych stosowane na powitania określona częstotliwość i podczas hello określony przedział czasu danego dnia. |
| **Częstotliwość tworzenia pełnej kopii zapasowej** | Codziennie/co tydzień | Częstotliwość tworzenia pełnych kopii zapasowych. W obu przypadkach pełne kopie zapasowe rozpocznie się podczas następnego okna zaplanowanej czasie hello. Po wybraniu co tydzień kopii zapasowych może obejmować wiele dni, dopóki wszystkie bazy danych pomyślnie wykonano kopię zapasową. |
| **Czas rozpoczęcia pełnej kopii zapasowej** | 00:00 – 23:00 (01:00) | Godzina rozpoczęcia dotyczącego danego dnia, w którym pełnych kopii zapasowych może mieć miejsce. |
| **Przedział czasu tworzenia pełnej kopii zapasowej** | 1 – 23 godzin (1 godz.) | Czas trwania okna czasu hello danego dnia, w którym pełnych kopii zapasowych może mieć miejsce. |
| **Częstotliwość wykonywania kopii zapasowych dziennika** | 5 – 60 minut (60 minut) | Częstotliwość tworzenia kopii zapasowych dziennika. |

## <a name="understanding-full-backup-frequency"></a>Opis częstotliwość tworzenia pełnej kopii zapasowej
Jest ważne toounderstand hello różnica między codziennie i cotygodniowych pełnych kopii zapasowych. W tym wysiłku opisano dwa przykładowe scenariusze.

### <a name="scenario-1-weekly-backups"></a>Scenariusz 1: Cotygodniowe kopie zapasowe
Masz zawierającą liczbę bardzo dużych baz danych maszyny Wirtualnej serwera SQL.

W poniedziałek możesz włączyć automatyczna usługa Backup v2 z hello następujące ustawienia:

- Harmonogram tworzenia kopii zapasowych: **ręczne**
- Pełnej kopii zapasowej częstotliwości: **co tydzień**
- Czas rozpoczęcia tworzenia kopii zapasowej pełnej: **01:00**
- Przedział czasu tworzenia pełnej kopii zapasowej: **1 godzina**

Oznacza to, że ten hello dalej dostępne okna kopii zapasowej jest wtorek na 1: 00 1 godziny. W tym czasie automatyczna usługa Backup rozpocznie się wykonywanie kopii zapasowych baz danych jednego naraz. W tym scenariuszu baz danych są wystarczająco duże, ukończy pełne kopie zapasowe baz danych hello pierwszy kilku. Jednak po godzinie nie wszystkie bazy danych hello utworzone kopie zapasowe.

W takim przypadku automatyczna usługa Backup rozpocznie się wykonywanie kopii zapasowych hello pozostałych hello baz danych z następnego dnia, środę o godzinie 1: 00 1 godziny. Jeśli nie wszystkie bazy danych utworzone kopie zapasowe w tym czasie, spróbuje następnego dnia o hello ponownie Witaj, sam czas. Operacja będzie kontynuowana, dopóki wszystkie bazy danych zostały pomyślnie kopii zapasowej.

Gdy osiągnie ona wtorek ponownie, automatyczna usługa Backup rozpocznie się wykonywanie kopii zapasowych wszystkich baz danych ponownie.

W tym scenariuszu pokazano, że automatyczna usługa Backup działa jedynie w hello określone okno czasu, a każda baza danych zostaną skopiowane nawet, jeden raz w tygodniu. To także wskazuje, że jest to możliwe dla toospan kopie zapasowe wielu dni w hello przypadek gdy nie jest możliwe toocomplete wszystkie kopie zapasowe w jednym dniu.

### <a name="scenario-2-daily-backups"></a>Scenariusz 2: Codzienne wykonywanie kopii zapasowych
Masz zawierającą liczbę bardzo dużych baz danych maszyny Wirtualnej serwera SQL.

W poniedziałek możesz włączyć automatyczna usługa Backup v2 z hello następujące ustawienia:

- Harmonogram tworzenia kopii zapasowych: ręczne
- Pełnej kopii zapasowej częstotliwości: codziennie
- Czas rozpoczęcia tworzenia kopii zapasowej pełnej: 22:00
- Przedział czasu tworzenia pełnej kopii zapasowej: 6 godzin

Oznacza to, że ten hello dalej dostępne okna kopii zapasowej jest poniedziałek godzinie 10 przez 6 godzin. W tym czasie automatyczna usługa Backup rozpocznie się wykonywanie kopii zapasowych baz danych jednego naraz.

Następnie wtorek 10 przez 6 godzin, pełne kopie zapasowe wszystkich baz danych zostanie uruchomiony ponownie.

> [!IMPORTANT]
> Podczas planowania codzienne wykonywanie kopii zapasowych, zaleca się zaplanowanie tooensure okno czasu szerokości, wszystkie bazy danych można kopii zapasowej, w tym czasie. Jest to szczególnie ważne w przypadku hello, w którym znajduje się duża ilość danych tooback się.

## <a name="configuration-in-hello-portal"></a>Konfiguracja w hello portalu

Możesz użyć hello Azure tooconfigure portalu automatyczna usługa Backup v2 podczas inicjowania obsługi lub dla maszyn wirtualnych istniejącego programu SQL Server 2016.

### <a name="new-vms"></a>Nowe maszyny wirtualne

Podczas tworzenia nowej maszyny wirtualnej 2016 serwera SQL w modelu wdrażania usługi Resource Manager hello, należy użyć hello automatyczna usługa Backup tooconfigure portalu Azure w wersji 2. 

W hello **ustawienia programu SQL Server** bloku, wybierz opcję **automatyczne kopie zapasowe**. Witaj Poniższy zrzut ekranu portalu Azure zawiera hello **SQL automatyczna usługa Backup** bloku.

![Konfiguracja SQL automatyczna usługa Backup w portalu Azure](./media/virtual-machines-windows-sql-automated-backup-v2/automated-backup-blade.png)

> [!NOTE]
> Automatycznego tworzenia kopii zapasowej v2 jest domyślnie wyłączona.

Dla kontekstu, zobacz temat pełną hello na [obsługi maszyny wirtualnej programu SQL Server na platformie Azure](virtual-machines-windows-portal-sql-server-provision.md).

### <a name="existing-vms"></a>Istniejące maszyny wirtualne

W przypadku istniejących maszyn wirtualnych programu SQL Server należy wybrać maszyny wirtualnej programu SQL Server. Następnie wybierz hello **konfigurację programu SQL Server** sekcji hello **ustawienia** bloku.

![SQL automatyczna usługa Backup dla istniejących maszyn wirtualnych](./media/virtual-machines-windows-sql-automated-backup-v2/sql-server-configuration.png)

W hello **konfigurację programu SQL Server** bloku, kliknij hello **Edytuj** przycisku na powitania automatycznego tworzenia kopii zapasowej sekcji.

![Konfigurowanie kopii zapasowej SQL automatycznego dla istniejących maszyn wirtualnych](./media/virtual-machines-windows-sql-automated-backup-v2/sql-server-configuration-edit.png)

Po zakończeniu kliknij przycisk hello **OK** przycisk u dołu hello hello **konfigurację programu SQL Server** toosave bloku zmiany.

Jeśli włączasz automatyczna usługa Backup dla powitania po raz pierwszy, Azure konfiguruje hello Agent środowiska IaaS programu SQL Server w tle hello. W tym czasie hello portalu Azure może nie informować, że skonfigurowano automatycznego tworzenia kopii zapasowej. Poczekaj kilka minut dla hello toobe agent zainstalowany, skonfigurowany. Po tym hello Azure portalu będzie odzwierciedlać hello nowych ustawień.

## <a name="configuration-with-powershell"></a>Konfiguracja przy użyciu programu PowerShell

Można użyć programu PowerShell tooconfigure v2 automatycznego tworzenia kopii zapasowej. Przed rozpoczęciem należy:

- [Pobierz i zainstaluj najnowsze programu Azure PowerShell hello](http://aka.ms/webpi-azps).
- Otwórz program Windows PowerShell i skojarzyć go z Twoim kontem. Aby to zrobić, wykonaj czynności hello w hello [skonfiguruj subskrypcję](https://docs.microsoft.com/azure/virtual-machines/windows/sql/virtual-machines-windows-ps-sql-create#configure-your-subscription) sekcji hello inicjowania obsługi administracyjnej tematu.

### <a name="install-hello-sql-iaas-extension"></a>Zainstaluj hello rozszerzenia IaaS SQL
Jeśli aprowizowanej maszyny wirtualnej programu SQL Server z portalu Azure hello hello rozszerzenie IaaS serwera SQL powinno być już zainstalowane. Można określić, czy jest ona instalowana dla maszyny Wirtualnej przez wywołanie metody **Get-AzureRmVM** polecenia i sprawdzeniu hello **rozszerzenia** właściwości.

```powershell
$vmname = "vmname"
$resourcegroupname = "resourcegroupname"

(Get-AzureRmVM -Name $vmname -ResourceGroupName $resourcegroupname).Extensions 
```

Jeśli zainstalowano hello rozszerzenia SQL Server IaaS Agent, powinien pojawić się wymienionym "SqlIaaSAgent" lub "SQLIaaSExtension". **ProvisioningState** dla rozszerzenia hello również powinny być widoczne "Powodzenie". 

Jeśli nie jest zainstalowany lub nie można zainicjować obsługi administracyjnej toobe, należy zainstalować go z hello następujące polecenia. Dodanie toohello wirtualna Nazwa zasobu grupy i, należy także określić hello region (**$region**) maszyny Wirtualnej znajdujący się w.

```powershell
$region = “EASTUS2”
Set-AzureRmVMSqlServerExtension -VMName $vmname `
    -ResourceGroupName $resourcegroupname -Name "SQLIaasExtension" `
    -Version "1.2" -Location $region 
```

### <a id="verifysettings"></a>Sprawdź bieżące ustawienia
Jeśli włączono automatyczne kopie zapasowe podczas inicjowania obsługi, można użyć programu PowerShell toocheck bieżącej konfiguracji. Uruchom hello **Get-AzureRmVMSqlServerExtension** polecenia i sprawdź, czy hello **AutoBackupSettings** właściwości:

```powershell
(Get-AzureRmVMSqlServerExtension -VMName $vmname -ResourceGroupName $resourcegroupname).AutoBackupSettings
```

Należy pobrać dane wyjściowe podobne toohello poniżej:

```
Enable                      : True
EnableEncryption            : False
RetentionPeriod             : 30
StorageUrl                  : https://test.blob.core.windows.net/
StorageAccessKey            :  
Password                    : 
BackupSystemDbs             : False
BackupScheduleType          : Manual
FullBackupFrequency         : WEEKLY
FullBackupStartTime         : 2
FullBackupWindowHours       : 2
LogBackupFrequency          : 60
```

Jeśli dane wyjściowe wskazuje, że **włączyć** ustawiono zbyt**False**, następnie tooenable automatyczne kopie zapasowe. Witaj szczęście jest włączone, a następnie skonfiguruj automatyczne kopie zapasowe w hello tak samo. Zobacz następną sekcję hello tych informacji.

> [!NOTE] 
> Jeśli natychmiast po wprowadzeniu zmiany można sprawdzić ustawienia hello, istnieje możliwość, że wystąpi ponownie hello starych wartości konfiguracji. Poczekaj kilka minut i sprawdź ustawienia hello ponownie toomake się upewnić, że zmiany zostały zastosowane.

### <a name="configure-automated-backup-v2"></a>Konfigurowanie automatycznego tworzenia kopii zapasowej v2
Umożliwia tooenable PowerShell automatyczne kopie zapasowe, a także toomodify jego konfiguracji i zachowania w dowolnym momencie. 

Najpierw wybierz lub Utwórz konto magazynu dla hello pliki kopii zapasowej. Witaj poniższy skrypt wybiera konto magazynu lub utworzenie go, jeśli nie istnieje.

```powershell
$storage_accountname = “yourstorageaccount”
$storage_resourcegroupname = $resourcegroupname

$storage = Get-AzureRmStorageAccount -ResourceGroupName $resourcegroupname `
    -Name $storage_accountname -ErrorAction SilentlyContinue
If (-Not $storage)
    { $storage = New-AzureRmStorageAccount -ResourceGroupName $storage_resourcegroupname `
    -Name $storage_accountname -SkuName Standard_GRS -Location $region } 
```

> [!NOTE]
> Automatyczne kopie zapasowe nie obsługuje przechowywania kopii zapasowych w magazynie premium, ale może potrwać kopii zapasowych z dysków maszyny Wirtualnej, które używają magazyn w warstwie Premium.

Następnie użyj hello **AzureRmVMSqlServerAutoBackupConfig nowy** polecenia tooenable i skonfigurować kopie zapasowe toostore ustawienia hello v2 automatycznego tworzenia kopii zapasowej w hello kontem magazynu platformy Azure. W tym przykładzie hello kopie zapasowe są ustawiane toobe przechowywane przez 10 dni. Kopie zapasowe bazy danych systemu są włączone. Pełne kopie zapasowe są zaplanowane co tydzień w oknie Uruchamianie 20:00 do dwóch godzin. Zaplanowane kopie zapasowe dziennika co 30 minut. drugie polecenie Hello **AzureRmVMSqlServerExtension zestaw**, hello aktualizacji określonej maszyny Wirtualnej platformy Azure przy użyciu tych ustawień.

```powershell
$autobackupconfig = New-AzureRmVMSqlServerAutoBackupConfig -Enable `
    -RetentionPeriodInDays 10 -StorageContext $storage.Context `
    -ResourceGroupName $storage_resourcegroupname -BackupSystemDbs `
    -BackupScheduleType Manual -FullBackupFrequency Weekly `
    -FullBackupStartHour 20 -FullBackupWindowInHours 2 `
    -LogBackupFrequencyInMinutes 30 

Set-AzureRmVMSqlServerExtension -AutoBackupSettings $autobackupconfig `
    -VMName $vmname -ResourceGroupName $resourcegroupname 
```

Go może potrwać kilka minut tooinstall i skonfiguruj hello Agent środowiska IaaS programu SQL Server. 

szyfrowania tooenable zmodyfikować hello poprzedniej skryptu toopass hello **EnableEncryption** parametru wraz z hasła (bezpieczny ciąg) hello **CertificatePassword** parametru. Witaj poniższy skrypt umożliwia hello ustawienia automatycznego tworzenia kopii zapasowej w poprzednim przykładzie hello i dodaje szyfrowania.

```powershell
$password = "P@ssw0rd"
$encryptionpassword = $password | ConvertTo-SecureString -AsPlainText -Force  

$autobackupconfig = New-AzureRmVMSqlServerAutoBackupConfig -Enable `
    -EnableEncryption -CertificatePassword $encryptionpassword `
    -RetentionPeriodInDays 10 -StorageContext $storage.Context `
    -ResourceGroupName $storage_resourcegroupname -BackupSystemDbs `
    -BackupScheduleType Manual -FullBackupFrequency Weekly `
    -FullBackupStartHour 20 -FullBackupWindowInHours 2 `
    -LogBackupFrequencyInMinutes 30 

Set-AzureRmVMSqlServerExtension -AutoBackupSettings $autobackupconfig `
    -VMName $vmname -ResourceGroupName $resourcegroupname
```

ustawienia są stosowane, tooconfirm [Sprawdź konfigurację automatycznego tworzenia kopii zapasowej hello](#verifysettings).

### <a name="disable-automated-backup"></a>Wyłącz automatyczne kopie zapasowe
toodisable automatyczne kopie zapasowe, uruchom hello sam skrypt bez hello **-Włącz** toohello parametru **AzureRmVMSqlServerAutoBackupConfig nowy** polecenia. Witaj braku hello **-Włącz** parametru sygnały hello polecenia toodisable hello funkcji. Podobnie jak w przypadku instalacji, może upłynąć kilka minut toodisable automatyczne kopie zapasowe.

```powershell
$autobackupconfig = New-AzureRmVMSqlServerAutoBackupConfig -ResourceGroupName $storage_resourcegroupname

Set-AzureRmVMSqlServerExtension -AutoBackupSettings $autobackupconfig `
    -VMName $vmname -ResourceGroupName $resourcegroupname
```

### <a name="example-script"></a>Przykładowy skrypt
Witaj poniższy skrypt zawiera zestaw zmiennych można dostosować tooenable i skonfiguruj automatyczne kopie zapasowe dla maszyny Wirtualnej. W Twoim przypadku może być konieczne skryptu hello toocustomize zgodnie z wymaganiami. Na przykład czy mają toomake zmiany, jeśli potrzebujesz kopii zapasowej hello toodisable systemowych baz danych lub włączyć szyfrowanie.

```powershell
$vmname = "yourvmname"
$resourcegroupname = "vmresourcegroupname"
$region = “Azure region name such as EASTUS2”
$storage_accountname = “storageaccountname”
$storage_resourcegroupname = $resourcegroupname
$retentionperiod = 10
$backupscheduletype = "Manual"
$fullbackupfrequency = "Weekly"
$fullbackupstarthour = "20"
$fullbackupwindow = "2"
$logbackupfrequency = "30"

# ResourceGroupName is hello resource group which is hosting hello VM where you are deploying hello SQL IaaS Extension 

Set-AzureRmVMSqlServerExtension -VMName $vmname `
    -ResourceGroupName $resourcegroupname -Name "SQLIaasExtension" `
    -Version "1.2" -Location $region

# Creates/use a storage account toostore hello backups

$storage = Get-AzureRmStorageAccount -ResourceGroupName $resourcegroupname `
    -Name $storage_accountname -ErrorAction SilentlyContinue
If (-Not $storage)
    { $storage = New-AzureRmStorageAccount -ResourceGroupName $storage_resourcegroupname `
    -Name $storage_accountname -SkuName Standard_GRS -Location $region }

# Configure Automated Backup settings

$autobackupconfig = New-AzureRmVMSqlServerAutoBackupConfig -Enable `
    -RetentionPeriodInDays $retentionperiod -StorageContext $storage.Context `
    -ResourceGroupName $storage_resourcegroupname -BackupSystemDbs `
    -BackupScheduleType $backupscheduletype -FullBackupFrequency $fullbackupfrequency `
    -FullBackupStartHour $fullbackupstarthour -FullBackupWindowInHours $fullbackupwindow `
    -LogBackupFrequencyInMinutes $logbackupfrequency

# Apply hello Automated Backup settings toohello VM

Set-AzureRmVMSqlServerExtension -AutoBackupSettings $autobackupconfig `
    -VMName $vmname -ResourceGroupName $resourcegroupname
```

## <a name="next-steps"></a>Następne kroki
Automatyczne v2 kopii zapasowej konfiguruje zarządzanej kopii zapasowej na maszynach wirtualnych Azure. Dlatego ważne jest zbyt[hello dokumentacji zarządzanej kopii zapasowej](https://msdn.microsoft.com/library/dn449496.aspx) toounderstand hello zachowanie i skutki.

Można znaleźć dodatkowe kopii zapasowej i przywracanie wskazówki dotyczące programu SQL Server na maszynach wirtualnych Azure w hello kolejny temat: [kopii zapasowej i przywracania dla programu SQL Server w usłudze Azure Virtual Machines](virtual-machines-windows-sql-backup-recovery.md).

Informacje o innych zadaniach automatyzacji dostępny, zobacz [rozszerzenia agenta programu SQL Server IaaS](virtual-machines-windows-sql-server-agent-extension.md).

Aby uzyskać więcej informacji na temat uruchamiania programu SQL Server na maszynach wirtualnych Azure, zobacz [programu SQL Server na maszynach wirtualnych platformy Azure — omówienie](virtual-machines-windows-sql-server-iaas-overview.md).

