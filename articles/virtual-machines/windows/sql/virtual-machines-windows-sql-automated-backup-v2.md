---
title: Automatycznego tworzenia kopii zapasowej w wersji 2 dla programu SQL Server 2016 maszyn wirtualnych platformy Azure | Dokumentacja firmy Microsoft
description: "Zawiera opis funkcji automatycznego tworzenia kopii zapasowej dla programu SQL Server 2016 maszyn wirtualnych działających na platformie Azure. Ten artykuł dotyczy maszyn wirtualnych za pomocą Menedżera zasobów."
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
ms.openlocfilehash: e7e14b0243f82c672392d5ab4bb6aca01156465b
ms.sourcegitcommit: b5c6197f997aa6858f420302d375896360dd7ceb
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/21/2017
---
# <a name="automated-backup-v2-for-sql-server-2016-azure-virtual-machines-resource-manager"></a>Automatycznego tworzenia kopii zapasowej w wersji 2 dla programu SQL Server 2016 maszyn wirtualnych platformy Azure (Resource Manager)

> [!div class="op_single_selector"]
> * [Program SQL Server 2014](virtual-machines-windows-sql-automated-backup.md)
> * [SQL Server 2016](virtual-machines-windows-sql-automated-backup-v2.md)

Automatyczne v2 kopii zapasowej automatycznie konfiguruje [zarządzanej kopii zapasowej Microsoft Azure](https://msdn.microsoft.com/library/dn449496.aspx) dla wszystkich istniejących i nowych baz danych na maszynie Wirtualnej platformy Azure, uruchomione wersje programu SQL Server 2016 Standard, Enterprise lub dewelopera. Dzięki temu można skonfigurować kopie zapasowe zwykłej bazy danych, które korzystać z magazynu trwałego obiektów blob platformy Azure. Automatyczne v2 kopii zapasowej jest zależna od [rozszerzenia agenta programu SQL Server IaaS](virtual-machines-windows-sql-server-agent-extension.md).

[!INCLUDE [learn-about-deployment-models](../../../../includes/learn-about-deployment-models-rm-include.md)]

## <a name="prerequisites"></a>Wymagania wstępne
Aby korzystać z automatycznego tworzenia kopii zapasowej 2, należy przejrzeć następujące wymagania wstępne:

**System operacyjny**:

- Windows Server 2012 R2
- Windows Server 2016

**Wydanie wersji programu SQL Server**:

- SQL Server 2016 Standard
- SQL Server 2016 Enterprise
- SQL Server 2016 Developer

> [!IMPORTANT]
> Automatyczne v2 kopii zapasowej działa z programem SQL Server 2016. Jeśli używasz programu SQL Server 2014, można użyć v1 automatycznego tworzenia kopii zapasowej do tworzenia kopii zapasowych baz danych. Aby uzyskać więcej informacji, zobacz [automatyczna usługa Backup SQL Server 2014 maszyn wirtualnych platformy Azure](virtual-machines-windows-sql-automated-backup.md).

**Baza danych konfiguracji**:

- Docelowej bazy danych muszą używać modelu odzyskiwania pełnego. Aby uzyskać więcej informacji dotyczących wpływu modelu odzyskiwania pełnego na wykonywanie kopii zapasowych, zobacz [kopii zapasowej w obszarze pełny Model odzyskiwania](https://technet.microsoft.com/library/ms190217.aspx).
- Nie masz systemowych baz danych do użycia w modelu odzyskiwania pełnego. Jeśli potrzebujesz kopii zapasowych dziennika mają być pobrane do modelu lub MSDB, musi jednak używać modelu odzyskiwania pełnego.
- Docelowymi bazami danych musi być w domyślnym wystąpieniu programu SQL Server. Rozszerzenie IaaS serwera SQL obsługuje tylko nazwane wystąpienia.

**Model wdrożenia usługi Azure**:

- Resource Manager

> [!NOTE]
> Automatyczne kopie zapasowe polega na **rozszerzenia agenta programu SQL Server IaaS**. Bieżący obrazów Galeria maszyny wirtualnej SQL dodać to rozszerzenie domyślnie. Aby uzyskać więcej informacji, zobacz [rozszerzenia agenta programu SQL Server IaaS](virtual-machines-windows-sql-server-agent-extension.md).

## <a name="settings"></a>Ustawienia
W poniższej tabeli opisano opcje, które można skonfigurować do automatycznego tworzenia kopii zapasowej w wersji 2. Kroki konfiguracji rzeczywisty zależy od przy użyciu portalu Azure lub poleceń programu PowerShell systemu Windows Azure.

### <a name="basic-settings"></a>Ustawienia podstawowe

| Ustawienie | Zakres (ustawienie domyślne) | Opis |
| --- | --- | --- |
| **Automatyczne kopie zapasowe** | Włącza/wyłącza (wyłączone) | Włącza lub wyłącza funkcję automatycznego tworzenia kopii zapasowej dla maszyny Wirtualnej platformy Azure, programem SQL Server 2016 Standard lub Enterprise. |
| **Okres przechowywania** | 1 do 30 dni (30 dni) | Liczba dni przechowywania kopii zapasowych. |
| **Konto magazynu** | Konto magazynu Azure | Konto magazynu Azure do przechowywania plików automatycznego tworzenia kopii zapasowej w magazynie obiektów blob. Kontener jest tworzony w tej lokalizacji, aby zapisać wszystkie pliki kopii zapasowej. Konwencja nazewnictwa pliku kopii zapasowej obejmuje daty, godziny i identyfikator GUID bazy danych. |
| **Szyfrowanie** |Włącza/wyłącza (wyłączone) | Włącza lub wyłącza funkcję szyfrowania. Po włączeniu szyfrowania certyfikatów służących do przywrócenia kopii zapasowej znajdują się na koncie magazynu określonym w tym samym **automaticbackup** kontenera przy użyciu tej samej konwencji nazewnictwa. Zmiana hasła nowego certyfikatu jest generowana za pomocą tego hasła, ale pozostaje stary certyfikat do przywrócenia poprzedniego kopii zapasowych. |
| **Hasło** |Tekst hasła | Hasło dla kluczy szyfrowania. Jest to tylko wymagane, jeśli jest włączone szyfrowanie. Aby przywrócić zaszyfrowanej kopii zapasowej, musi mieć prawidłowe hasło, a powiązany certyfikat, który został użyty w momencie utworzenia kopii zapasowej. |

### <a name="advanced-settings"></a>Ustawienia zaawansowane

| Ustawienie | Zakres (ustawienie domyślne) | Opis |
| --- | --- | --- |
| **Kopie zapasowe bazy danych systemu** | Włącza/wyłącza (wyłączone) | Po włączeniu tej funkcji będzie również wykonać kopię zapasową systemowych baz danych: Master, MSDB i modelu. Sprawdź, czy są w trybie odzyskiwania pełnego Jeśli kopie zapasowe dziennika do wykonania dla bazy danych MSDB i modelu. Kopie zapasowe dziennika nigdy nie są wykonywane dla głównego. A nie kopii zapasowych są wykonywane dla bazy danych TempDB. |
| **Harmonogram tworzenia kopii zapasowych** | Ręczne/automatycznego (automatycznego) | Domyślnie harmonogram tworzenia kopii zapasowych będzie automatycznie ustalana na podstawie przyrostu dziennika. Ręczne harmonogram tworzenia kopii zapasowych umożliwia użytkownikowi określić przedział czasu tworzenia kopii zapasowych. W takim przypadku kopie zapasowe tylko nastąpi z częstotliwością i podczas określone okno czasu danego dnia. |
| **Częstotliwość tworzenia pełnej kopii zapasowej** | Codziennie/co tydzień | Częstotliwość tworzenia pełnych kopii zapasowych. W obu przypadkach pełne kopie zapasowe rozpocznie się podczas następnego okna zaplanowanej godzinie. Po wybraniu co tydzień kopii zapasowych może obejmować wiele dni, dopóki wszystkie bazy danych pomyślnie wykonano kopię zapasową. |
| **Czas rozpoczęcia pełnej kopii zapasowej** | 00:00 – 23:00 (01:00) | Godzina rozpoczęcia dotyczącego danego dnia, w którym pełnych kopii zapasowych może mieć miejsce. |
| **Przedział czasu tworzenia pełnej kopii zapasowej** | 1 – 23 godzin (1 godz.) | Czas trwania przedział czasu danego dnia, w którym pełnych kopii zapasowych może mieć miejsce. |
| **Częstotliwość wykonywania kopii zapasowych dziennika** | 5 – 60 minut (60 minut) | Częstotliwość tworzenia kopii zapasowych dziennika. |

## <a name="understanding-full-backup-frequency"></a>Opis częstotliwość tworzenia pełnej kopii zapasowej
Należy zrozumieć różnicę między codziennie i cotygodniowych pełnych kopii zapasowych. W tym wysiłku opisano dwa przykładowe scenariusze.

### <a name="scenario-1-weekly-backups"></a>Scenariusz 1: Cotygodniowe kopie zapasowe
Masz zawierającą liczbę bardzo dużych baz danych maszyny Wirtualnej serwera SQL.

W poniedziałek możesz włączyć automatyczna usługa Backup v2 z następującymi ustawieniami:

- Harmonogram tworzenia kopii zapasowych: **ręczne**
- Pełnej kopii zapasowej częstotliwości: **co tydzień**
- Czas rozpoczęcia tworzenia kopii zapasowej pełnej: **01:00**
- Przedział czasu tworzenia pełnej kopii zapasowej: **1 godzina**

Oznacza to, że następnym dostępnym oknie kopii zapasowej ma wtorek na 1: 00 1 godziny. W tym czasie automatyczna usługa Backup rozpocznie się wykonywanie kopii zapasowych baz danych jednego naraz. W tym scenariuszu baz danych są wystarczająco duże, że pełne kopie zapasowe ukończy dla pierwszego kilka baz danych. Jednak po godzinie nie wszystkie bazy danych utworzone kopie zapasowe.

W takim przypadku automatyczna usługa Backup rozpocznie się tworzenie kopii zapasowej bazy danych pozostałych następnego dnia, środę o godzinie 1: 00 1 godziny. Jeśli nie wszystkie bazy danych utworzone kopie zapasowe w tym czasie, spróbuje ponownie następnego dnia, w tym samym czasie. Operacja będzie kontynuowana, dopóki wszystkie bazy danych zostały pomyślnie kopii zapasowej.

Gdy osiągnie ona wtorek ponownie, automatyczna usługa Backup rozpocznie się wykonywanie kopii zapasowych wszystkich baz danych ponownie.

W tym scenariuszu pokazano, że automatyczna usługa Backup działa jedynie w określone okno czasu, a każda baza danych zostaną skopiowane nawet, jeden raz w tygodniu. Oznacza to również, że jest to możliwe obejmować wielu dni w przypadku, gdy nie jest możliwe przeprowadzenie wszystkie kopie zapasowe w jednym dniu kopii zapasowych.

### <a name="scenario-2-daily-backups"></a>Scenariusz 2: Codzienne wykonywanie kopii zapasowych
Masz zawierającą liczbę bardzo dużych baz danych maszyny Wirtualnej serwera SQL.

W poniedziałek możesz włączyć automatyczna usługa Backup v2 z następującymi ustawieniami:

- Harmonogram tworzenia kopii zapasowych: ręczne
- Pełnej kopii zapasowej częstotliwości: codziennie
- Czas rozpoczęcia tworzenia kopii zapasowej pełnej: 22:00
- Przedział czasu tworzenia pełnej kopii zapasowej: 6 godzin

Oznacza to, że następnym dostępnym oknie kopii zapasowej ma poniedziałek godzinie 10 przez 6 godzin. W tym czasie automatyczna usługa Backup rozpocznie się wykonywanie kopii zapasowych baz danych jednego naraz.

Następnie wtorek 10 przez 6 godzin, pełne kopie zapasowe wszystkich baz danych zostanie uruchomiony ponownie.

> [!IMPORTANT]
> Podczas planowania codzienne wykonywanie kopii zapasowych, zalecane jest, aby zaplanować okno czasu szerokości do upewnij się, że wszystkie może być kopie zapasowe baz danych w tej chwili. Jest to szczególnie ważne w przypadku, gdy ma dużą ilość danych, aby utworzyć kopię zapasową.

## <a name="configuration-in-the-portal"></a>Konfiguracja w portalu

Azure portal umożliwia konfigurowanie automatycznego tworzenia kopii zapasowej w wersji 2, podczas udostępniania lub dla maszyn wirtualnych istniejącego programu SQL Server 2016.

### <a name="new-vms"></a>Nowe maszyny wirtualne

Użyj portalu Azure, aby skonfigurować v2 automatyczna usługa Backup, podczas tworzenia nowej maszyny wirtualnej 2016 serwera SQL w modelu wdrażania usługi Resource Manager. 

W **ustawienia programu SQL Server** bloku, wybierz opcję **automatyczne kopie zapasowe**. Poniżej przedstawiono zrzut ekranu na portalu Azure **SQL automatyczna usługa Backup** bloku.

![Konfiguracja SQL automatyczna usługa Backup w portalu Azure](./media/virtual-machines-windows-sql-automated-backup-v2/automated-backup-blade.png)

> [!NOTE]
> Automatycznego tworzenia kopii zapasowej v2 jest domyślnie wyłączona.

Dla kontekstu, zobacz temat pełną na [obsługi maszyny wirtualnej programu SQL Server na platformie Azure](virtual-machines-windows-portal-sql-server-provision.md).

### <a name="existing-vms"></a>Istniejące maszyny wirtualne

W przypadku istniejących maszyn wirtualnych programu SQL Server należy wybrać maszyny wirtualnej programu SQL Server. Następnie wybierz **konfigurację programu SQL Server** sekcji **ustawienia** bloku.

![SQL automatyczna usługa Backup dla istniejących maszyn wirtualnych](./media/virtual-machines-windows-sql-automated-backup-v2/sql-server-configuration.png)

W **konfigurację programu SQL Server** bloku, kliknij przycisk **Edytuj** przycisk w sekcji automatycznego tworzenia kopii zapasowej.

![Konfigurowanie kopii zapasowej SQL automatycznego dla istniejących maszyn wirtualnych](./media/virtual-machines-windows-sql-automated-backup-v2/sql-server-configuration-edit.png)

Gdy skończysz, kliknij przycisk **OK** przycisk w dolnej części **konfigurację programu SQL Server** bloku, aby zapisać zmiany.

Jeśli po raz pierwszy włączasz automatyczna usługa Backup, Azure konfiguruje agenta programu SQL Server IaaS w tle. W tym czasie portalu Azure może nie informować, że skonfigurowano automatycznego tworzenia kopii zapasowej. Poczekaj kilka minut dla agenta, który ma zostać zainstalowany, skonfigurowany. Po utworzeniu tego portalu Azure będzie odzwierciedlać nowe ustawienia.

## <a name="configuration-with-powershell"></a>Konfiguracja przy użyciu programu PowerShell

Można skonfigurować v2 automatycznego tworzenia kopii zapasowej za pomocą programu PowerShell. Przed rozpoczęciem należy:

- [Pobierz i zainstaluj najnowsze programu Azure PowerShell](http://aka.ms/webpi-azps).
- Otwórz program Windows PowerShell i skojarzyć go z Twoim kontem. Można to zrobić, wykonując kroki opisane w [skonfiguruj subskrypcję](https://docs.microsoft.com/azure/virtual-machines/windows/sql/virtual-machines-windows-ps-sql-create#configure-your-subscription) tematu inicjowania obsługi administracyjnej.

### <a name="install-the-sql-iaas-extension"></a>Zainstaluj rozszerzenie IaaS SQL
Jeśli aprowizowanej maszyny wirtualnej programu SQL Server w portalu Azure, rozszerzenie IaaS serwera SQL powinno być już zainstalowane. Można określić, czy jest ona instalowana dla maszyny Wirtualnej przez wywołanie metody **Get-AzureRmVM** polecenia i sprawdzeniu **rozszerzenia** właściwości.

```powershell
$vmname = "vmname"
$resourcegroupname = "resourcegroupname"

(Get-AzureRmVM -Name $vmname -ResourceGroupName $resourcegroupname).Extensions 
```

Jeśli zainstalowano rozszerzenia SQL Server IaaS Agent, powinien pojawić się wymienionym "SqlIaaSAgent" lub "SQLIaaSExtension". **ProvisioningState** dla rozszerzenia należy również wyświetlić "Powodzenie". 

Jeśli nie jest zainstalowane lub nie można zainicjować obsługi administracyjnej, należy zainstalować go za pomocą następującego polecenia. Oprócz grupy nazwy i zasobów maszyny Wirtualnej, należy także określić region (**$region**) maszyny Wirtualnej znajdujący się w.

```powershell
$region = “EASTUS2”
Set-AzureRmVMSqlServerExtension -VMName $vmname `
    -ResourceGroupName $resourcegroupname -Name "SQLIaasExtension" `
    -Version "1.2" -Location $region 
```

### <a id="verifysettings"></a>Sprawdź bieżące ustawienia
Jeśli włączono automatyczne kopie zapasowe podczas inicjowania obsługi, można sprawdzić bieżącej konfiguracji za pomocą programu PowerShell. Uruchom **Get-AzureRmVMSqlServerExtension** polecenia i sprawdź, czy **AutoBackupSettings** właściwości:

```powershell
(Get-AzureRmVMSqlServerExtension -VMName $vmname -ResourceGroupName $resourcegroupname).AutoBackupSettings
```

Należy pobrać dane wyjściowe podobne do następujących:

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

Jeśli dane wyjściowe wskazuje, że **włączyć** ma ustawioną wartość **False**, a następnie należy włączyć automatyczne kopie zapasowe. Dobre wieści jest włączone, a następnie skonfiguruj automatyczne kopie zapasowe w taki sam sposób. W następnej sekcji dla tych informacji.

> [!NOTE] 
> Jeśli wybierzesz ustawienia natychmiast po wprowadzeniu zmian jest możliwe, że wystąpi ponownie starych wartości konfiguracji. Poczekaj kilka minut, a następnie sprawdź ustawienia ponownie, aby upewnić się, że zmiany zostały zastosowane.

### <a name="configure-automated-backup-v2"></a>Konfigurowanie automatycznego tworzenia kopii zapasowej v2
Można włączyć automatycznego tworzenia kopii zapasowej oraz aby zmodyfikować jego konfigurację i zachowanie w dowolnej chwili za pomocą programu PowerShell. 

Najpierw wybierz lub Utwórz konto magazynu w przypadku plików kopii zapasowych. Poniższy skrypt wybiera konta magazynu lub jeśli nie istnieje, tworzy go.

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

Następnie użyj **AzureRmVMSqlServerAutoBackupConfig nowy** polecenie, aby włączyć i skonfigurować ustawienia v2 automatycznego tworzenia kopii zapasowej do przechowywania kopii zapasowych w ramach konta magazynu platformy Azure. W tym przykładzie ustawiono kopie zapasowe będą przechowywane w ciągu 10 dni. Kopie zapasowe bazy danych systemu są włączone. Pełne kopie zapasowe są zaplanowane co tydzień w oknie Uruchamianie 20:00 do dwóch godzin. Zaplanowane kopie zapasowe dziennika co 30 minut. Drugie polecenie **AzureRmVMSqlServerExtension zestaw**, aktualizuje określonej maszyny Wirtualnej platformy Azure przy użyciu tych ustawień.

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

Go może potrwać kilka minut, aby zainstalować i skonfigurować agenta programu SQL Server IaaS. 

Aby włączyć szyfrowanie, zmodyfikuj poprzedni skrypt do przekazania **EnableEncryption** parametru wraz z hasła (bezpieczny ciąg) **CertificatePassword** parametru. Poniższy skrypt umożliwia ustawienia automatycznego tworzenia kopii zapasowej w poprzednim przykładzie i dodaje szyfrowania.

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

Aby potwierdzić ustawienia są stosowane, [Sprawdź konfigurację automatycznego tworzenia kopii zapasowej](#verifysettings).

### <a name="disable-automated-backup"></a>Wyłącz automatyczne kopie zapasowe
Aby wyłączyć automatyczna usługa Backup, uruchom ten sam skrypt bez **— Włącz** parametr **AzureRmVMSqlServerAutoBackupConfig nowy** polecenia. Brak **-Włącz** parametru sygnały polecenie, aby wyłączyć funkcję. Podobnie jak w przypadku instalacji, może upłynąć kilka minut, aby wyłączyć automatyczne wykonywanie kopii zapasowych.

```powershell
$autobackupconfig = New-AzureRmVMSqlServerAutoBackupConfig -ResourceGroupName $storage_resourcegroupname

Set-AzureRmVMSqlServerExtension -AutoBackupSettings $autobackupconfig `
    -VMName $vmname -ResourceGroupName $resourcegroupname
```

### <a name="example-script"></a>Przykładowy skrypt
Poniższy skrypt zawiera zestaw zmiennych, które można dostosować, aby włączyć i skonfigurować automatyczna usługa Backup dla maszyny Wirtualnej. W Twoim przypadku może być konieczne dostosowanie skryptu, w zależności od wymagań. Na przykład użytkownik musi wprowadzić zmiany, aby wyłączyć tworzenie kopii zapasowej bazy danych systemu lub włączyć szyfrowanie.

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

# ResourceGroupName is the resource group which is hosting the VM where you are deploying the SQL IaaS Extension 

Set-AzureRmVMSqlServerExtension -VMName $vmname `
    -ResourceGroupName $resourcegroupname -Name "SQLIaasExtension" `
    -Version "1.2" -Location $region

# Creates/use a storage account to store the backups

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

# Apply the Automated Backup settings to the VM

Set-AzureRmVMSqlServerExtension -AutoBackupSettings $autobackupconfig `
    -VMName $vmname -ResourceGroupName $resourcegroupname
```

## <a name="next-steps"></a>Kolejne kroki
Automatyczne v2 kopii zapasowej konfiguruje zarządzanej kopii zapasowej na maszynach wirtualnych Azure. Dlatego ważne jest, aby [zapoznaj się z dokumentacją dla zarządzanej kopii zapasowej](https://msdn.microsoft.com/library/dn449496.aspx) zrozumienie zachowania i skutki.

Można znaleźć dodatkowe kopii zapasowej i przywracanie wskazówki dotyczące programu SQL Server na maszynach wirtualnych Azure w następującym temacie: [kopii zapasowej i przywracania dla programu SQL Server w usłudze Azure Virtual Machines](virtual-machines-windows-sql-backup-recovery.md).

Informacje o innych zadaniach automatyzacji dostępny, zobacz [rozszerzenia agenta programu SQL Server IaaS](virtual-machines-windows-sql-server-agent-extension.md).

Aby uzyskać więcej informacji na temat uruchamiania programu SQL Server na maszynach wirtualnych Azure, zobacz [programu SQL Server na maszynach wirtualnych platformy Azure — omówienie](virtual-machines-windows-sql-server-iaas-overview.md).

