---
title: aaaAutomated kopii zapasowej programu SQL Server 2014 maszyn wirtualnych platformy Azure | Dokumentacja firmy Microsoft
description: "Zawiera opis funkcji automatycznego tworzenia kopii zapasowej hello programu SQL Server 2014 w maszynach wirtualnych działających na platformie Azure. W tym artykule jest tooVMs określonego za pomocą hello Menedżera zasobów."
services: virtual-machines-windows
documentationcenter: na
author: rothja
manager: jhubbard
editor: 
tags: azure-resource-manager
ms.assetid: bdc63fd1-db49-4e76-87d5-b5c6a890e53c
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 07/05/2017
ms.author: jroth
ms.openlocfilehash: c6803d8ef9f80e44a2f87918d87e099f1b562483
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="automated-backup-for-sql-server-2014-virtual-machines-resource-manager"></a>Automatyczne kopie zapasowe maszyn wirtualnych programu SQL Server 2014 (Resource Manager)

> [!div class="op_single_selector"]
> * [Program SQL Server 2014](virtual-machines-windows-sql-automated-backup.md)
> * [SQL Server 2016](virtual-machines-windows-sql-automated-backup-v2.md)

Automatyczne kopie zapasowe automatycznie konfiguruje [tooMicrosoft zarządzanej kopii zapasowej Azure](https://msdn.microsoft.com/library/dn449496.aspx) dla wszystkich istniejących i nowych baz danych na maszynie Wirtualnej platformy Azure, programem SQL Server 2014 Standard lub Enterprise. Dzięki temu tooconfigure kopie zapasowe zwykłej bazy danych, które korzystać z magazynu trwałego obiektów blob platformy Azure. Automatyczne kopie zapasowe zależy od hello [rozszerzenia agenta programu SQL Server IaaS](virtual-machines-windows-sql-server-agent-extension.md).

[!INCLUDE [learn-about-deployment-models](../../../../includes/learn-about-deployment-models-rm-include.md)]

## <a name="prerequisites"></a>Wymagania wstępne
toouse automatyczne kopie zapasowe, należy wziąć pod uwagę następujące wymagania wstępne hello:

**System operacyjny**:

- Windows Server 2012
- Windows Server 2012 R2
- Windows Server 2016

**Wydanie wersji programu SQL Server**:

- SQL Server 2014 Standard
- SQL Server 2014 Enterprise

> [!IMPORTANT]
> Automatyczne działa kopii zapasowej z programu SQL Server 2014. Jeśli używasz programu SQL Server 2016, można użyć automatycznego tworzenia kopii zapasowej v2 tooback zapasową baz danych. Aby uzyskać więcej informacji, zobacz [v2 automatyczna usługa Backup SQL Server 2016 maszyn wirtualnych platformy Azure](virtual-machines-windows-sql-automated-backup-v2.md).

**Baza danych konfiguracji**:

- Docelowymi bazami danych, należy użyć hello modelu odzyskiwania pełnego. Aby uzyskać więcej informacji dotyczących wpływu hello modelu odzyskiwania pełnego hello na wykonywanie kopii zapasowych, zobacz [hello kopii zapasowych w ramach modelu odzyskiwania pełnego](https://technet.microsoft.com/library/ms190217.aspx).
- Docelowymi bazami danych musi znajdować się na powitania domyślnego wystąpienia programu SQL Server. Witaj IaaS rozszerzenie dotyczące programu SQL Server nie obsługuje nazwanych wystąpień.

**Model wdrożenia usługi Azure**:

- Resource Manager

**Program Azure PowerShell**:

- [Zainstaluj najnowsze poleceń programu Azure PowerShell hello](/powershell/azure/overview) Jeśli planujesz tooconfigure automatyczne kopie zapasowe przy użyciu programu PowerShell.

> [!NOTE]
> Automatyczne kopie zapasowe polega na powitania rozszerzenia agenta programu SQL Server IaaS. Bieżący obrazów Galeria maszyny wirtualnej SQL dodać to rozszerzenie domyślnie. Aby uzyskać więcej informacji, zobacz [rozszerzenia agenta programu SQL Server IaaS](virtual-machines-windows-sql-server-agent-extension.md).

## <a name="settings"></a>Ustawienia

Witaj poniższej tabeli opisano opcje hello, które można skonfigurować do automatycznego tworzenia kopii zapasowej. kroki rzeczywista konfiguracja Hello się różnić w zależności od tego, czy używać hello portalu Azure lub poleceń programu Windows PowerShell dla usługi Azure.

| Ustawienie | Zakres (ustawienie domyślne) | Opis |
| --- | --- | --- |
| **Automatyczne kopie zapasowe** | Włącza/wyłącza (wyłączone) | Włącza lub wyłącza funkcję automatycznego tworzenia kopii zapasowej dla maszyny Wirtualnej platformy Azure, programem SQL Server 2014 Standard lub Enterprise. |
| **Okres przechowywania** | 1 do 30 dni (30 dni) | Witaj liczbę dni tooretain kopii zapasowej. |
| **Konto magazynu** | Konto magazynu Azure | Toouse konto magazynu Azure do przechowywania plików automatycznego tworzenia kopii zapasowej w magazynie obiektów blob. Kontener jest tworzony w tej lokalizacji toostore wszystkie pliki kopii zapasowej. Plik kopii zapasowej Hello konwencji nazewnictwa obejmuje hello daty, godziny i nazwy komputera. |
| **Szyfrowanie** | Włącza/wyłącza (wyłączone) | Włącza lub wyłącza funkcję szyfrowania. Po włączeniu szyfrowania hello używane certyfikaty toorestore hello w kopii zapasowej znajdują się w hello określony magazynu konta w hello sam `automaticbackup` przy użyciu kontenera hello tej samej konwencji nazewnictwa. Zmiana hasła hello nowego certyfikatu jest generowana za pomocą tego hasła, ale hello stary certyfikat pozostaje toorestore poprzednich kopii zapasowych. |
| **Hasło** | Tekst hasła | Hasło dla kluczy szyfrowania. Jest to tylko wymagane, jeśli jest włączone szyfrowanie. W kolejności toorestore zaszyfrowanej kopii zapasowej, trzeba hello prawidłowe hasło i powiązane certyfikatu, który został użyty w czasie hello hello tworzenia kopii zapasowej. |

## <a name="configuration-in-hello-portal"></a>Konfiguracja w hello portalu

Witaj tooconfigure portalu Azure automatyczne kopie zapasowe można użyć podczas inicjowania obsługi lub dla maszyn wirtualnych istniejącego programu SQL Server 2014.

### <a name="new-vms"></a>Nowe maszyny wirtualne

Podczas tworzenia nowej maszyny wirtualnej 2014 serwera SQL w modelu wdrażania usługi Resource Manager hello za pomocą hello Azure tooconfigure portalu automatyczne kopie zapasowe.

W hello **ustawienia programu SQL Server** bloku, wybierz opcję **automatyczne kopie zapasowe**. Witaj Poniższy zrzut ekranu portalu Azure zawiera hello **SQL automatyczna usługa Backup** bloku.

![Konfiguracja SQL automatyczna usługa Backup w portalu Azure](./media/virtual-machines-windows-sql-automated-backup/azure-sql-arm-autobackup.png)

Dla kontekstu, zobacz temat pełną hello na [obsługi maszyny wirtualnej programu SQL Server na platformie Azure](virtual-machines-windows-portal-sql-server-provision.md).

### <a name="existing-vms"></a>Istniejące maszyny wirtualne

W przypadku istniejących maszyn wirtualnych programu SQL Server należy wybrać maszyny wirtualnej programu SQL Server. Następnie wybierz hello **konfigurację programu SQL Server** sekcji hello **ustawienia** bloku.

![SQL automatyczna usługa Backup dla istniejących maszyn wirtualnych](./media/virtual-machines-windows-sql-automated-backup/azure-sql-rm-autobackup-existing-vms.png)

W hello **konfigurację programu SQL Server** bloku, kliknij hello **Edytuj** przycisku na powitania automatycznego tworzenia kopii zapasowej sekcji.

![Konfigurowanie kopii zapasowej SQL automatycznego dla istniejących maszyn wirtualnych](./media/virtual-machines-windows-sql-automated-backup/azure-sql-rm-autobackup-configuration.png)

Po zakończeniu kliknij przycisk hello **OK** przycisk u dołu hello hello **konfigurację programu SQL Server** toosave bloku zmiany.

Jeśli włączasz automatyczna usługa Backup dla powitania po raz pierwszy, Azure konfiguruje hello Agent środowiska IaaS programu SQL Server w tle hello. W tym czasie hello portalu Azure może nie informować, że skonfigurowano automatycznego tworzenia kopii zapasowej. Poczekaj kilka minut dla hello toobe agent zainstalowany, skonfigurowany. Po tym hello Azure portalu będzie odzwierciedlać hello nowych ustawień.

> [!NOTE]
> Istnieje również możliwość skonfigurowania automatycznego tworzenia kopii zapasowej przy użyciu szablonu. Aby uzyskać więcej informacji, zobacz [szablonu Azure szybkiego startu dla automatyczna usługa Backup](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-sql-existing-autobackup-update).

## <a name="configuration-with-powershell"></a>Konfiguracja przy użyciu programu PowerShell

Możesz użyć programu PowerShell tooconfigure automatyczne kopie zapasowe. Przed rozpoczęciem należy:

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
Enable                      : False
EnableEncryption            : False
RetentionPeriod             : -1
StorageUrl                  : NOTSET
StorageAccessKey            : 
Password                    : 
BackupSystemDbs             : False
BackupScheduleType          : 
FullBackupFrequency         : 
FullBackupStartTime         : 
FullBackupWindowHours       : 
LogBackupFrequency          : 
```

Jeśli dane wyjściowe wskazuje, że **włączyć** ustawiono zbyt**False**, następnie tooenable automatyczne kopie zapasowe. Witaj szczęście jest włączone, a następnie skonfiguruj automatyczne kopie zapasowe w hello tak samo. Zobacz następną sekcję hello tych informacji.

> [!NOTE] 
> Jeśli natychmiast po wprowadzeniu zmiany można sprawdzić ustawienia hello, istnieje możliwość, że wystąpi ponownie hello starych wartości konfiguracji. Poczekaj kilka minut i sprawdź ustawienia hello ponownie toomake się upewnić, że zmiany zostały zastosowane.

### <a name="configure-automated-backup"></a>Skonfiguruj automatyczne kopie zapasowe
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

Następnie użyj hello **AzureRmVMSqlServerAutoBackupConfig nowy** polecenia tooenable i skonfigurować hello automatyczna usługa Backup ustawienia toostore tworzenia kopii zapasowych w hello kontem magazynu platformy Azure. W tym przykładzie hello kopie zapasowe są ustawiane toobe przechowywane przez 10 dni. drugie polecenie Hello **AzureRmVMSqlServerExtension zestaw**, hello aktualizacji określonej maszyny Wirtualnej platformy Azure przy użyciu tych ustawień.

```powershell
$autobackupconfig = New-AzureRmVMSqlServerAutoBackupConfig -Enable `
    -RetentionPeriodInDays 10 -StorageContext $storage.Context `
    -ResourceGroupName $storage_resourcegroupname

Set-AzureRmVMSqlServerExtension -AutoBackupSettings $autobackupconfig `
    -VMName $vmname -ResourceGroupName $resourcegroupname
```

Go może potrwać kilka minut tooinstall i skonfiguruj hello Agent środowiska IaaS programu SQL Server.

> [!NOTE]
> Istnieją inne ustawienia **AzureRmVMSqlServerAutoBackupConfig nowy** przeznaczonych tylko tooSQL Server 2016 i v2 automatycznego tworzenia kopii zapasowej. SQL Server 2014 nie obsługuje hello następujące ustawienia: **BackupSystemDbs**, **BackupScheduleType**, **FullBackupFrequency**,  **FullBackupStartHour**, **FullBackupWindowInHours**, i **LogBackupFrequencyInMinutes**. Jeśli próba tooconfigure tych ustawień na maszynę wirtualną programu SQL Server 2014 nie było błędu, ale nie zostać zastosowane ustawienia hello. Jeśli chcesz toouse tych ustawień na maszynę wirtualną programu SQL Server 2016, zobacz [v2 automatyczna usługa Backup SQL Server 2016 maszyn wirtualnych platformy Azure](virtual-machines-windows-sql-automated-backup-v2.md).

szyfrowania tooenable zmodyfikować hello poprzedniej skryptu toopass hello **EnableEncryption** parametru wraz z hasła (bezpieczny ciąg) hello **CertificatePassword** parametru. Witaj poniższy skrypt umożliwia hello ustawienia automatycznego tworzenia kopii zapasowej w poprzednim przykładzie hello i dodaje szyfrowania.

```powershell
$password = "P@ssw0rd"
$encryptionpassword = $password | ConvertTo-SecureString -AsPlainText -Force

$autobackupconfig = New-AzureRmVMSqlServerAutoBackupConfig -Enable `
    -EnableEncryption -CertificatePassword $encryptionpassword `
    -RetentionPeriodInDays 10 -StorageContext $storage.Context `
    -ResourceGroupName $storage_resourcegroupname

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
    -ResourceGroupName $storage_resourcegroupname

# Apply hello Automated Backup settings toohello VM

Set-AzureRmVMSqlServerExtension -AutoBackupSettings $autobackupconfig `
    -VMName $vmname -ResourceGroupName $resourcegroupname
```

## <a name="next-steps"></a>Następne kroki

Automatyczne kopie zapasowe konfiguruje zarządzanej kopii zapasowej na maszynach wirtualnych platformy Azure. Dlatego ważne jest zbyt[hello dokumentacji zarządzanej kopii zapasowej](https://msdn.microsoft.com/library/dn449496.aspx) toounderstand hello zachowanie i skutki.

Można znaleźć dodatkowe kopii zapasowej i przywracanie wskazówki dotyczące programu SQL Server na maszynach wirtualnych Azure w hello kolejny temat: [kopii zapasowej i przywracania dla programu SQL Server w usłudze Azure Virtual Machines](virtual-machines-windows-sql-backup-recovery.md).

Informacje o innych zadaniach automatyzacji dostępny, zobacz [rozszerzenia agenta programu SQL Server IaaS](virtual-machines-windows-sql-server-agent-extension.md).

Aby uzyskać więcej informacji na temat uruchamiania programu SQL Server na maszynach wirtualnych Azure, zobacz [programu SQL Server na maszynach wirtualnych platformy Azure — omówienie](virtual-machines-windows-sql-server-iaas-overview.md).

