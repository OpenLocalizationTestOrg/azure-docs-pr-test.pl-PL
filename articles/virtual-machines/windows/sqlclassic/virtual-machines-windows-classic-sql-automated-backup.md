---
title: aaaAutomated kopii zapasowej dla programu SQL Server maszyn wirtualnych (klasyczne) | Dokumentacja firmy Microsoft
description: "Zawiera opis funkcji automatycznego tworzenia kopii zapasowej hello na serwerze SQL działa w maszynach wirtualnych platformy Azure za pomocą Menedżera zasobów. "
services: virtual-machines-windows
documentationcenter: na
author: rothja
manager: jhubbard
editor: 
tags: azure-service-management
ms.assetid: 3333e830-8a60-42f5-9f44-8e02e9868d7b
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 07/05/2017
ms.author: jroth
ms.openlocfilehash: 5d8f0412578c2d86edc6e54093a5da4891d3847e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="automated-backup-for-sql-server-in-azure-virtual-machines-classic"></a>Automatyczne kopie zapasowe programu SQL Server na maszynach wirtualnych platformy Azure (klasyczne)
> [!div class="op_single_selector"]
> * [Resource Manager](../sql/virtual-machines-windows-sql-automated-backup.md)
> * [Wdrożenie klasyczne](../classic/sql-automated-backup.md)
> 
> 

Automatyczne kopie zapasowe automatycznie konfiguruje [tooMicrosoft zarządzanej kopii zapasowej Azure](https://msdn.microsoft.com/library/dn449496.aspx) dla wszystkich istniejących i nowych baz danych na maszynie Wirtualnej platformy Azure, programem SQL Server 2014 Standard lub Enterprise. Dzięki temu tooconfigure kopie zapasowe zwykłej bazy danych, które korzystać z magazynu trwałego obiektów blob platformy Azure. Automatyczne kopie zapasowe zależy od hello [rozszerzenia agenta programu SQL Server IaaS](../classic/sql-server-agent-extension.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).

> [!IMPORTANT] 
> Platforma Azure ma dwa różne modele wdrażania do tworzenia i pracy z zasobami: [Resource Manager i Model Klasyczny](../../../azure-resource-manager/resource-manager-deployment-model.md). W tym artykule omówiono przy użyciu klasycznego modelu wdrożenia hello. Firma Microsoft zaleca, aby większości nowych wdrożeń korzystać hello modelu Resource Manager. wersja Menedżera zasobów hello tooview tego artykułu, zobacz [automatyczna usługa Backup dla programu SQL Server w Menedżerze zasobów maszyn wirtualnych Azure](../sql/virtual-machines-windows-sql-automated-backup.md).

## <a name="prerequisites"></a>Wymagania wstępne
toouse automatyczne kopie zapasowe, należy wziąć pod uwagę następujące wymagania wstępne hello:

**System operacyjny**:

* Windows Server 2012
* Windows Server 2012 R2
* Windows Server 2016

**Wydanie wersji programu SQL Server**:

* SQL Server 2014 Standard
* SQL Server 2014 Enterprise

> [!NOTE]
> SQL Server 2016 nie jest jeszcze obsługiwana dla automatycznego tworzenia kopii zapasowej.
> 
> 

**Baza danych konfiguracji**:

* Docelowymi bazami danych, należy użyć hello modelu odzyskiwania pełnego.

**Program Azure PowerShell**:

* [Zainstaluj najnowsze poleceń programu Azure PowerShell hello](/powershell/azure/overview).

**Rozszerzenia programu SQL Server IaaS**:

* [Zainstaluj hello IaaS rozszerzenie dotyczące programu SQL Server](../classic/sql-server-agent-extension.md).

## <a name="settings"></a>Ustawienia
Witaj poniższej tabeli opisano opcje hello, które można skonfigurować do automatycznego tworzenia kopii zapasowej. Klasycznych maszyn wirtualnych należy użyć programu PowerShell tooconfigure te ustawienia.

| Ustawienie | Zakres (ustawienie domyślne) | Opis |
| --- | --- | --- |
| **Automatyczne kopie zapasowe** |Włącza/wyłącza (wyłączone) |Włącza lub wyłącza funkcję automatycznego tworzenia kopii zapasowej dla maszyny Wirtualnej platformy Azure, programem SQL Server 2014 Standard lub Enterprise. |
| **Okres przechowywania** |1 do 30 dni (30 dni) |Witaj liczbę dni tooretain kopii zapasowej. |
| **Konto magazynu** |Konto magazynu Azure (konto magazynu hello utworzone dla hello określonej maszyny Wirtualnej) |Toouse konto magazynu Azure do przechowywania plików automatycznego tworzenia kopii zapasowej w magazynie obiektów blob. Kontener jest tworzony w tej lokalizacji toostore wszystkie pliki kopii zapasowej. Plik kopii zapasowej Hello konwencji nazewnictwa obejmuje hello daty, godziny i nazwy komputera. |
| **Szyfrowanie** |Włącza/wyłącza (wyłączone) |Włącza lub wyłącza funkcję szyfrowania. Po włączeniu szyfrowania hello certyfikaty używane toorestore hello tworzenia kopii zapasowej znajdują się w hello określono konto magazynu w hello hello tego samego kontenera automaticbackup przy użyciu tej samej konwencji nazewnictwa. Zmiana hasła hello nowego certyfikatu jest generowana za pomocą tego hasła, ale hello stary certyfikat pozostaje toorestore poprzednich kopii zapasowych. |
| **Hasło** |Tekst hasła, (Brak) |Hasło dla kluczy szyfrowania. Jest to tylko wymagane, jeśli jest włączone szyfrowanie. W kolejności toorestore zaszyfrowanej kopii zapasowej, trzeba hello prawidłowe hasło i powiązane certyfikatu, który został użyty w czasie hello hello tworzenia kopii zapasowej. | **Kopia zapasowa systemowych baz danych** | Włącza/wyłącza (wyłączone) | Korzystać z pełnej kopii zapasowych Master, Model i MSDB |
| **Skonfiguruj harmonogram tworzenia kopii zapasowych** | Ręczne/automatycznego (automatycznego) | Wybierz **automatycznego** tooautomatically wykonać pełne i kopii zapasowych w oparciu o wzrost dziennika dziennika. Wybierz **ręcznego** toospecify hello harmonogram dla pełnej i kopii zapasowych dziennika. |

## <a name="configuration-with-powershell"></a>Konfiguracja przy użyciu programu PowerShell
W hello poniższy przykład programu PowerShell automatycznego tworzenia kopii zapasowej jest skonfigurowany dla istniejącej maszyny Wirtualnej 2014 r. dla serwera SQL. Witaj **AzureVMSqlServerAutoBackupConfig nowy** polecenie konfiguruje hello automatyczna usługa Backup ustawienia toostore tworzenia kopii zapasowych na koncie magazynu Azure hello określonej przez zmienną hello $storageaccount. Te kopie zapasowe będą przechowywane w ciągu 10 dni. Witaj **AzureVMSqlServerExtension zestaw** polecenia hello aktualizacji określonej maszyny Wirtualnej platformy Azure przy użyciu tych ustawień.

    $storageaccount = "<storageaccountname>"
    $storageaccountkey = (Get-AzureStorageKey -StorageAccountName $storageaccount).Primary
    $storagecontext = New-AzureStorageContext -StorageAccountName $storageaccount -StorageAccountKey $storageaccountkey
    $autobackupconfig = New-AzureVMSqlServerAutoBackupConfig -StorageContext $storagecontext -Enable -RetentionPeriod 10

    Get-AzureVM -ServiceName <vmservicename> -Name <vmname> | Set-AzureVMSqlServerExtension -AutoBackupSettings $autobackupconfig | Update-AzureVM

Go może potrwać kilka minut tooinstall i skonfiguruj hello Agent środowiska IaaS programu SQL Server.

szyfrowanie tooenable zmodyfikować hello poprzedniej toopass hello EnableEncryption skryptu wraz z hasłem (bezpieczny ciąg) dla parametru CertificatePassword hello. Witaj poniższy skrypt umożliwia hello ustawienia automatycznego tworzenia kopii zapasowej w poprzednim przykładzie hello i dodaje szyfrowania.

    $storageaccount = "<storageaccountname>"
    $storageaccountkey = (Get-AzureStorageKey -StorageAccountName $storageaccount).Primary
    $storagecontext = New-AzureStorageContext -StorageAccountName $storageaccount -StorageAccountKey $storageaccountkey
    $password = "P@ssw0rd"
    $encryptionpassword = $password | ConvertTo-SecureString -AsPlainText -Force  
    $autobackupconfig = New-AzureVMSqlServerAutoBackupConfig -StorageContext $storagecontext -Enable -RetentionPeriod 10 -EnableEncryption -CertificatePassword $encryptionpassword

    Get-AzureVM -ServiceName <vmservicename> -Name <vmname> | Set-AzureVMSqlServerExtension -AutoBackupSettings $autobackupconfig | Update-AzureVM

Automatyczne kopie zapasowe toodisable wykonywania hello sam skrypt bez hello **— włączyć** toohello parametru **AzureVMSqlServerAutoBackupConfig nowy**. Podobnie jak w przypadku instalacji, może upłynąć kilka minut toodisable automatyczne kopie zapasowe.

> [!NOTE]
> Wyłączanie i odinstalowywania programu SQL Server IaaS Agent hello nie powoduje usunięcia hello wcześniej skonfigurowane ustawienia zarządzanej kopii zapasowej. Automatyczna usługa Backup należy wyłączyć przed wyłączeniem lub odinstalowanie hello Agent środowiska IaaS programu SQL Server.
> 
> 

## <a name="next-steps"></a>Następne kroki
Automatyczne kopie zapasowe konfiguruje zarządzanej kopii zapasowej na maszynach wirtualnych platformy Azure. Dlatego ważne jest zbyt[hello dokumentacji zarządzanej kopii zapasowej](https://msdn.microsoft.com/library/dn449496.aspx) toounderstand hello zachowanie i skutki.

Można znaleźć dodatkowe kopii zapasowej i przywracanie wskazówki dotyczące programu SQL Server na maszynach wirtualnych Azure w hello kolejny temat: [kopii zapasowej i przywracania dla programu SQL Server w usłudze Azure Virtual Machines](../sql/virtual-machines-windows-sql-backup-recovery.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fsqlclassic%2ftoc.json).

Informacje o innych zadaniach automatyzacji dostępny, zobacz [rozszerzenia agenta programu SQL Server IaaS](../classic/sql-server-agent-extension.md).

Aby uzyskać więcej informacji na temat uruchamiania programu SQL Server na maszynach wirtualnych Azure, zobacz [programu SQL Server na maszynach wirtualnych platformy Azure — omówienie](../sql/virtual-machines-windows-sql-server-iaas-overview.md).

