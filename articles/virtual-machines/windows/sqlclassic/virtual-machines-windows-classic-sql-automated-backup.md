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
# <a name="automated-backup-for-sql-server-in-azure-virtual-machines-classic"></a><span data-ttu-id="c6cff-103">Automatyczne kopie zapasowe programu SQL Server na maszynach wirtualnych platformy Azure (klasyczne)</span><span class="sxs-lookup"><span data-stu-id="c6cff-103">Automated Backup for SQL Server in Azure Virtual Machines (Classic)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="c6cff-104">Resource Manager</span><span class="sxs-lookup"><span data-stu-id="c6cff-104">Resource Manager</span></span>](../sql/virtual-machines-windows-sql-automated-backup.md)
> * [<span data-ttu-id="c6cff-105">Wdrożenie klasyczne</span><span class="sxs-lookup"><span data-stu-id="c6cff-105">Classic</span></span>](../classic/sql-automated-backup.md)
> 
> 

<span data-ttu-id="c6cff-106">Automatyczne kopie zapasowe automatycznie konfiguruje [tooMicrosoft zarządzanej kopii zapasowej Azure](https://msdn.microsoft.com/library/dn449496.aspx) dla wszystkich istniejących i nowych baz danych na maszynie Wirtualnej platformy Azure, programem SQL Server 2014 Standard lub Enterprise.</span><span class="sxs-lookup"><span data-stu-id="c6cff-106">Automated Backup automatically configures [Managed Backup tooMicrosoft Azure](https://msdn.microsoft.com/library/dn449496.aspx) for all existing and new databases on an Azure VM running SQL Server 2014 Standard or Enterprise.</span></span> <span data-ttu-id="c6cff-107">Dzięki temu tooconfigure kopie zapasowe zwykłej bazy danych, które korzystać z magazynu trwałego obiektów blob platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="c6cff-107">This enables you tooconfigure regular database backups that utilize durable Azure blob storage.</span></span> <span data-ttu-id="c6cff-108">Automatyczne kopie zapasowe zależy od hello [rozszerzenia agenta programu SQL Server IaaS](../classic/sql-server-agent-extension.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="c6cff-108">Automated Backup depends on hello [SQL Server IaaS Agent Extension](../classic/sql-server-agent-extension.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span></span>

> [!IMPORTANT] 
> <span data-ttu-id="c6cff-109">Platforma Azure ma dwa różne modele wdrażania do tworzenia i pracy z zasobami: [Resource Manager i Model Klasyczny](../../../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="c6cff-109">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../azure-resource-manager/resource-manager-deployment-model.md).</span></span> <span data-ttu-id="c6cff-110">W tym artykule omówiono przy użyciu klasycznego modelu wdrożenia hello.</span><span class="sxs-lookup"><span data-stu-id="c6cff-110">This article covers using hello Classic deployment model.</span></span> <span data-ttu-id="c6cff-111">Firma Microsoft zaleca, aby większości nowych wdrożeń korzystać hello modelu Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="c6cff-111">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span> <span data-ttu-id="c6cff-112">wersja Menedżera zasobów hello tooview tego artykułu, zobacz [automatyczna usługa Backup dla programu SQL Server w Menedżerze zasobów maszyn wirtualnych Azure](../sql/virtual-machines-windows-sql-automated-backup.md).</span><span class="sxs-lookup"><span data-stu-id="c6cff-112">tooview hello Resource Manager version of this article, see [Automated Backup for SQL Server in Azure Virtual Machines Resource Manager](../sql/virtual-machines-windows-sql-automated-backup.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c6cff-113">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="c6cff-113">Prerequisites</span></span>
<span data-ttu-id="c6cff-114">toouse automatyczne kopie zapasowe, należy wziąć pod uwagę następujące wymagania wstępne hello:</span><span class="sxs-lookup"><span data-stu-id="c6cff-114">toouse Automated Backup, consider hello following prerequisites:</span></span>

<span data-ttu-id="c6cff-115">**System operacyjny**:</span><span class="sxs-lookup"><span data-stu-id="c6cff-115">**Operating System**:</span></span>

* <span data-ttu-id="c6cff-116">Windows Server 2012</span><span class="sxs-lookup"><span data-stu-id="c6cff-116">Windows Server 2012</span></span>
* <span data-ttu-id="c6cff-117">Windows Server 2012 R2</span><span class="sxs-lookup"><span data-stu-id="c6cff-117">Windows Server 2012 R2</span></span>
* <span data-ttu-id="c6cff-118">Windows Server 2016</span><span class="sxs-lookup"><span data-stu-id="c6cff-118">Windows Server 2016</span></span>

<span data-ttu-id="c6cff-119">**Wydanie wersji programu SQL Server**:</span><span class="sxs-lookup"><span data-stu-id="c6cff-119">**SQL Server version/edition**:</span></span>

* <span data-ttu-id="c6cff-120">SQL Server 2014 Standard</span><span class="sxs-lookup"><span data-stu-id="c6cff-120">SQL Server 2014 Standard</span></span>
* <span data-ttu-id="c6cff-121">SQL Server 2014 Enterprise</span><span class="sxs-lookup"><span data-stu-id="c6cff-121">SQL Server 2014 Enterprise</span></span>

> [!NOTE]
> <span data-ttu-id="c6cff-122">SQL Server 2016 nie jest jeszcze obsługiwana dla automatycznego tworzenia kopii zapasowej.</span><span class="sxs-lookup"><span data-stu-id="c6cff-122">SQL Server 2016 is not yet supported for Automated Backup.</span></span>
> 
> 

<span data-ttu-id="c6cff-123">**Baza danych konfiguracji**:</span><span class="sxs-lookup"><span data-stu-id="c6cff-123">**Database configuration**:</span></span>

* <span data-ttu-id="c6cff-124">Docelowymi bazami danych, należy użyć hello modelu odzyskiwania pełnego.</span><span class="sxs-lookup"><span data-stu-id="c6cff-124">Target databases must use hello full recovery model.</span></span>

<span data-ttu-id="c6cff-125">**Program Azure PowerShell**:</span><span class="sxs-lookup"><span data-stu-id="c6cff-125">**Azure PowerShell**:</span></span>

* <span data-ttu-id="c6cff-126">[Zainstaluj najnowsze poleceń programu Azure PowerShell hello](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="c6cff-126">[Install hello latest Azure PowerShell commands](/powershell/azure/overview).</span></span>

<span data-ttu-id="c6cff-127">**Rozszerzenia programu SQL Server IaaS**:</span><span class="sxs-lookup"><span data-stu-id="c6cff-127">**SQL Server IaaS Extension**:</span></span>

* <span data-ttu-id="c6cff-128">[Zainstaluj hello IaaS rozszerzenie dotyczące programu SQL Server](../classic/sql-server-agent-extension.md).</span><span class="sxs-lookup"><span data-stu-id="c6cff-128">[Install hello SQL Server IaaS Extension](../classic/sql-server-agent-extension.md).</span></span>

## <a name="settings"></a><span data-ttu-id="c6cff-129">Ustawienia</span><span class="sxs-lookup"><span data-stu-id="c6cff-129">Settings</span></span>
<span data-ttu-id="c6cff-130">Witaj poniższej tabeli opisano opcje hello, które można skonfigurować do automatycznego tworzenia kopii zapasowej.</span><span class="sxs-lookup"><span data-stu-id="c6cff-130">hello following table describes hello options that can be configured for Automated Backup.</span></span> <span data-ttu-id="c6cff-131">Klasycznych maszyn wirtualnych należy użyć programu PowerShell tooconfigure te ustawienia.</span><span class="sxs-lookup"><span data-stu-id="c6cff-131">For classic VMs, you must use PowerShell tooconfigure these settings.</span></span>

| <span data-ttu-id="c6cff-132">Ustawienie</span><span class="sxs-lookup"><span data-stu-id="c6cff-132">Setting</span></span> | <span data-ttu-id="c6cff-133">Zakres (ustawienie domyślne)</span><span class="sxs-lookup"><span data-stu-id="c6cff-133">Range (Default)</span></span> | <span data-ttu-id="c6cff-134">Opis</span><span class="sxs-lookup"><span data-stu-id="c6cff-134">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="c6cff-135">**Automatyczne kopie zapasowe**</span><span class="sxs-lookup"><span data-stu-id="c6cff-135">**Automated Backup**</span></span> |<span data-ttu-id="c6cff-136">Włącza/wyłącza (wyłączone)</span><span class="sxs-lookup"><span data-stu-id="c6cff-136">Enable/Disable (Disabled)</span></span> |<span data-ttu-id="c6cff-137">Włącza lub wyłącza funkcję automatycznego tworzenia kopii zapasowej dla maszyny Wirtualnej platformy Azure, programem SQL Server 2014 Standard lub Enterprise.</span><span class="sxs-lookup"><span data-stu-id="c6cff-137">Enables or disables Automated Backup for an Azure VM running SQL Server 2014 Standard or Enterprise.</span></span> |
| <span data-ttu-id="c6cff-138">**Okres przechowywania**</span><span class="sxs-lookup"><span data-stu-id="c6cff-138">**Retention Period**</span></span> |<span data-ttu-id="c6cff-139">1 do 30 dni (30 dni)</span><span class="sxs-lookup"><span data-stu-id="c6cff-139">1-30 days (30 days)</span></span> |<span data-ttu-id="c6cff-140">Witaj liczbę dni tooretain kopii zapasowej.</span><span class="sxs-lookup"><span data-stu-id="c6cff-140">hello number of days tooretain a backup.</span></span> |
| <span data-ttu-id="c6cff-141">**Konto magazynu**</span><span class="sxs-lookup"><span data-stu-id="c6cff-141">**Storage Account**</span></span> |<span data-ttu-id="c6cff-142">Konto magazynu Azure (konto magazynu hello utworzone dla hello określonej maszyny Wirtualnej)</span><span class="sxs-lookup"><span data-stu-id="c6cff-142">Azure storage account (hello storage account created for hello specified VM)</span></span> |<span data-ttu-id="c6cff-143">Toouse konto magazynu Azure do przechowywania plików automatycznego tworzenia kopii zapasowej w magazynie obiektów blob.</span><span class="sxs-lookup"><span data-stu-id="c6cff-143">An Azure storage account toouse for storing Automated Backup files in blob storage.</span></span> <span data-ttu-id="c6cff-144">Kontener jest tworzony w tej lokalizacji toostore wszystkie pliki kopii zapasowej.</span><span class="sxs-lookup"><span data-stu-id="c6cff-144">A container is created at this location toostore all backup files.</span></span> <span data-ttu-id="c6cff-145">Plik kopii zapasowej Hello konwencji nazewnictwa obejmuje hello daty, godziny i nazwy komputera.</span><span class="sxs-lookup"><span data-stu-id="c6cff-145">hello backup file naming convention includes hello date, time, and machine name.</span></span> |
| <span data-ttu-id="c6cff-146">**Szyfrowanie**</span><span class="sxs-lookup"><span data-stu-id="c6cff-146">**Encryption**</span></span> |<span data-ttu-id="c6cff-147">Włącza/wyłącza (wyłączone)</span><span class="sxs-lookup"><span data-stu-id="c6cff-147">Enable/Disable (Disabled)</span></span> |<span data-ttu-id="c6cff-148">Włącza lub wyłącza funkcję szyfrowania.</span><span class="sxs-lookup"><span data-stu-id="c6cff-148">Enables or disables encryption.</span></span> <span data-ttu-id="c6cff-149">Po włączeniu szyfrowania hello certyfikaty używane toorestore hello tworzenia kopii zapasowej znajdują się w hello określono konto magazynu w hello hello tego samego kontenera automaticbackup przy użyciu tej samej konwencji nazewnictwa.</span><span class="sxs-lookup"><span data-stu-id="c6cff-149">When encryption is enabled, hello certificates used toorestore hello backup are located in hello specified storage account in hello same automaticbackup container using hello same naming convention.</span></span> <span data-ttu-id="c6cff-150">Zmiana hasła hello nowego certyfikatu jest generowana za pomocą tego hasła, ale hello stary certyfikat pozostaje toorestore poprzednich kopii zapasowych.</span><span class="sxs-lookup"><span data-stu-id="c6cff-150">If hello password changes, a new certificate is generated with that password, but hello old certificate remains toorestore prior backups.</span></span> |
| <span data-ttu-id="c6cff-151">**Hasło**</span><span class="sxs-lookup"><span data-stu-id="c6cff-151">**Password**</span></span> |<span data-ttu-id="c6cff-152">Tekst hasła, (Brak)</span><span class="sxs-lookup"><span data-stu-id="c6cff-152">Password text (None)</span></span> |<span data-ttu-id="c6cff-153">Hasło dla kluczy szyfrowania.</span><span class="sxs-lookup"><span data-stu-id="c6cff-153">A password for encryption keys.</span></span> <span data-ttu-id="c6cff-154">Jest to tylko wymagane, jeśli jest włączone szyfrowanie.</span><span class="sxs-lookup"><span data-stu-id="c6cff-154">This is only required if encryption is enabled.</span></span> <span data-ttu-id="c6cff-155">W kolejności toorestore zaszyfrowanej kopii zapasowej, trzeba hello prawidłowe hasło i powiązane certyfikatu, który został użyty w czasie hello hello tworzenia kopii zapasowej.</span><span class="sxs-lookup"><span data-stu-id="c6cff-155">In order toorestore an encrypted backup, you must have hello correct password and related certificate that was used at hello time hello backup was taken.</span></span> | <span data-ttu-id="c6cff-156">**Kopia zapasowa systemowych baz danych**</span><span class="sxs-lookup"><span data-stu-id="c6cff-156">**Backup system databases**</span></span> | <span data-ttu-id="c6cff-157">Włącza/wyłącza (wyłączone)</span><span class="sxs-lookup"><span data-stu-id="c6cff-157">Enable/Disable (Disabled)</span></span> | <span data-ttu-id="c6cff-158">Korzystać z pełnej kopii zapasowych Master, Model i MSDB</span><span class="sxs-lookup"><span data-stu-id="c6cff-158">Take full backups of Master, Model, and MSDB</span></span> |
| <span data-ttu-id="c6cff-159">**Skonfiguruj harmonogram tworzenia kopii zapasowych**</span><span class="sxs-lookup"><span data-stu-id="c6cff-159">**Configure backup schedule**</span></span> | <span data-ttu-id="c6cff-160">Ręczne/automatycznego (automatycznego)</span><span class="sxs-lookup"><span data-stu-id="c6cff-160">Manual/Automated (Automated)</span></span> | <span data-ttu-id="c6cff-161">Wybierz **automatycznego** tooautomatically wykonać pełne i kopii zapasowych w oparciu o wzrost dziennika dziennika.</span><span class="sxs-lookup"><span data-stu-id="c6cff-161">Select **Automated** tooautomatically take full and log backups based on log growth.</span></span> <span data-ttu-id="c6cff-162">Wybierz **ręcznego** toospecify hello harmonogram dla pełnej i kopii zapasowych dziennika.</span><span class="sxs-lookup"><span data-stu-id="c6cff-162">Select **Manual** toospecify hello schedule for full and log backups.</span></span> |

## <a name="configuration-with-powershell"></a><span data-ttu-id="c6cff-163">Konfiguracja przy użyciu programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="c6cff-163">Configuration with PowerShell</span></span>
<span data-ttu-id="c6cff-164">W hello poniższy przykład programu PowerShell automatycznego tworzenia kopii zapasowej jest skonfigurowany dla istniejącej maszyny Wirtualnej 2014 r. dla serwera SQL.</span><span class="sxs-lookup"><span data-stu-id="c6cff-164">In hello following PowerShell example, Automated Backup is configured for an existing SQL Server 2014 VM.</span></span> <span data-ttu-id="c6cff-165">Witaj **AzureVMSqlServerAutoBackupConfig nowy** polecenie konfiguruje hello automatyczna usługa Backup ustawienia toostore tworzenia kopii zapasowych na koncie magazynu Azure hello określonej przez zmienną hello $storageaccount.</span><span class="sxs-lookup"><span data-stu-id="c6cff-165">hello **New-AzureVMSqlServerAutoBackupConfig** command configures hello Automated Backup settings toostore backups in hello Azure storage account specified by hello $storageaccount variable.</span></span> <span data-ttu-id="c6cff-166">Te kopie zapasowe będą przechowywane w ciągu 10 dni.</span><span class="sxs-lookup"><span data-stu-id="c6cff-166">These backups will be retained for 10 days.</span></span> <span data-ttu-id="c6cff-167">Witaj **AzureVMSqlServerExtension zestaw** polecenia hello aktualizacji określonej maszyny Wirtualnej platformy Azure przy użyciu tych ustawień.</span><span class="sxs-lookup"><span data-stu-id="c6cff-167">hello **Set-AzureVMSqlServerExtension** command updates hello specified Azure VM with these settings.</span></span>

    $storageaccount = "<storageaccountname>"
    $storageaccountkey = (Get-AzureStorageKey -StorageAccountName $storageaccount).Primary
    $storagecontext = New-AzureStorageContext -StorageAccountName $storageaccount -StorageAccountKey $storageaccountkey
    $autobackupconfig = New-AzureVMSqlServerAutoBackupConfig -StorageContext $storagecontext -Enable -RetentionPeriod 10

    Get-AzureVM -ServiceName <vmservicename> -Name <vmname> | Set-AzureVMSqlServerExtension -AutoBackupSettings $autobackupconfig | Update-AzureVM

<span data-ttu-id="c6cff-168">Go może potrwać kilka minut tooinstall i skonfiguruj hello Agent środowiska IaaS programu SQL Server.</span><span class="sxs-lookup"><span data-stu-id="c6cff-168">It could take several minutes tooinstall and configure hello SQL Server IaaS Agent.</span></span>

<span data-ttu-id="c6cff-169">szyfrowanie tooenable zmodyfikować hello poprzedniej toopass hello EnableEncryption skryptu wraz z hasłem (bezpieczny ciąg) dla parametru CertificatePassword hello.</span><span class="sxs-lookup"><span data-stu-id="c6cff-169">tooenable encryption, modify hello previous script toopass hello EnableEncryption parameter along with a password (secure string) for hello CertificatePassword parameter.</span></span> <span data-ttu-id="c6cff-170">Witaj poniższy skrypt umożliwia hello ustawienia automatycznego tworzenia kopii zapasowej w poprzednim przykładzie hello i dodaje szyfrowania.</span><span class="sxs-lookup"><span data-stu-id="c6cff-170">hello following script enables hello Automated Backup settings in hello previous example and adds encryption.</span></span>

    $storageaccount = "<storageaccountname>"
    $storageaccountkey = (Get-AzureStorageKey -StorageAccountName $storageaccount).Primary
    $storagecontext = New-AzureStorageContext -StorageAccountName $storageaccount -StorageAccountKey $storageaccountkey
    $password = "P@ssw0rd"
    $encryptionpassword = $password | ConvertTo-SecureString -AsPlainText -Force  
    $autobackupconfig = New-AzureVMSqlServerAutoBackupConfig -StorageContext $storagecontext -Enable -RetentionPeriod 10 -EnableEncryption -CertificatePassword $encryptionpassword

    Get-AzureVM -ServiceName <vmservicename> -Name <vmname> | Set-AzureVMSqlServerExtension -AutoBackupSettings $autobackupconfig | Update-AzureVM

<span data-ttu-id="c6cff-171">Automatyczne kopie zapasowe toodisable wykonywania hello sam skrypt bez hello **— włączyć** toohello parametru **AzureVMSqlServerAutoBackupConfig nowy**.</span><span class="sxs-lookup"><span data-stu-id="c6cff-171">toodisable automatic backup, run hello same script without hello **-Enable** parameter toohello **New-AzureVMSqlServerAutoBackupConfig**.</span></span> <span data-ttu-id="c6cff-172">Podobnie jak w przypadku instalacji, może upłynąć kilka minut toodisable automatyczne kopie zapasowe.</span><span class="sxs-lookup"><span data-stu-id="c6cff-172">As with installation, it can take several minutes toodisable Automated Backup.</span></span>

> [!NOTE]
> <span data-ttu-id="c6cff-173">Wyłączanie i odinstalowywania programu SQL Server IaaS Agent hello nie powoduje usunięcia hello wcześniej skonfigurowane ustawienia zarządzanej kopii zapasowej.</span><span class="sxs-lookup"><span data-stu-id="c6cff-173">Disabling and uninstalling hello SQL Server IaaS Agent does not remove hello previously configured Managed Backup settings.</span></span> <span data-ttu-id="c6cff-174">Automatyczna usługa Backup należy wyłączyć przed wyłączeniem lub odinstalowanie hello Agent środowiska IaaS programu SQL Server.</span><span class="sxs-lookup"><span data-stu-id="c6cff-174">You should disable Automated Backup before disabling or uninstalling hello SQL Server IaaS Agent.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="c6cff-175">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="c6cff-175">Next steps</span></span>
<span data-ttu-id="c6cff-176">Automatyczne kopie zapasowe konfiguruje zarządzanej kopii zapasowej na maszynach wirtualnych platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="c6cff-176">Automated Backup configures Managed Backup on Azure VMs.</span></span> <span data-ttu-id="c6cff-177">Dlatego ważne jest zbyt[hello dokumentacji zarządzanej kopii zapasowej](https://msdn.microsoft.com/library/dn449496.aspx) toounderstand hello zachowanie i skutki.</span><span class="sxs-lookup"><span data-stu-id="c6cff-177">So it is important too[review hello documentation for Managed Backup](https://msdn.microsoft.com/library/dn449496.aspx) toounderstand hello behavior and implications.</span></span>

<span data-ttu-id="c6cff-178">Można znaleźć dodatkowe kopii zapasowej i przywracanie wskazówki dotyczące programu SQL Server na maszynach wirtualnych Azure w hello kolejny temat: [kopii zapasowej i przywracania dla programu SQL Server w usłudze Azure Virtual Machines](../sql/virtual-machines-windows-sql-backup-recovery.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fsqlclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="c6cff-178">You can find additional backup and restore guidance for SQL Server on Azure VMs in hello following topic: [Backup and Restore for SQL Server in Azure Virtual Machines](../sql/virtual-machines-windows-sql-backup-recovery.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fsqlclassic%2ftoc.json).</span></span>

<span data-ttu-id="c6cff-179">Informacje o innych zadaniach automatyzacji dostępny, zobacz [rozszerzenia agenta programu SQL Server IaaS](../classic/sql-server-agent-extension.md).</span><span class="sxs-lookup"><span data-stu-id="c6cff-179">For information about other available automation tasks, see [SQL Server IaaS Agent Extension](../classic/sql-server-agent-extension.md).</span></span>

<span data-ttu-id="c6cff-180">Aby uzyskać więcej informacji na temat uruchamiania programu SQL Server na maszynach wirtualnych Azure, zobacz [programu SQL Server na maszynach wirtualnych platformy Azure — omówienie](../sql/virtual-machines-windows-sql-server-iaas-overview.md).</span><span class="sxs-lookup"><span data-stu-id="c6cff-180">For more information about running SQL Server on Azure VMs, see [SQL Server on Azure Virtual Machines overview](../sql/virtual-machines-windows-sql-server-iaas-overview.md).</span></span>

