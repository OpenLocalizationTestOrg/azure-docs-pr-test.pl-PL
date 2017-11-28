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
# <a name="use-azurermbackup-cmdlets-tooback-up-virtual-machines"></a><span data-ttu-id="ef374-103">Użyj tooback poleceń cmdlet AzureRM.Backup zapasowych maszyn wirtualnych</span><span class="sxs-lookup"><span data-stu-id="ef374-103">Use AzureRM.Backup cmdlets tooback up virtual machines</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="ef374-104">Resource Manager</span><span class="sxs-lookup"><span data-stu-id="ef374-104">Resource Manager</span></span>](backup-azure-vms-automation.md)
> * [<span data-ttu-id="ef374-105">Wdrożenie klasyczne</span><span class="sxs-lookup"><span data-stu-id="ef374-105">Classic</span></span>](backup-azure-vms-classic-automation.md)
>
>

<span data-ttu-id="ef374-106">W tym artykule opisano sposób toouse programu Azure PowerShell kopii zapasowych i odzyskiwania maszyn wirtualnych platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="ef374-106">This article shows you how toouse Azure PowerShell for backup and recovery of Azure VMs.</span></span> <span data-ttu-id="ef374-107">Platforma Azure oferuje dwa różne modele wdrażania związane z tworzeniem zasobów i pracą z nimi: model wdrażania przy użyciu usługi Resource Manager i model klasyczny.</span><span class="sxs-lookup"><span data-stu-id="ef374-107">Azure has two different deployment models for creating and working with resources: Resource Manager and Classic.</span></span> <span data-ttu-id="ef374-108">W tym artykule omówiono przy użyciu hello Classic wdrażania modelu tooback zapasowej magazyn kopii zapasowych tooa danych.</span><span class="sxs-lookup"><span data-stu-id="ef374-108">This article covers using hello Classic deployment model tooback up data tooa Backup vault.</span></span> <span data-ttu-id="ef374-109">Jeśli nie utworzono magazyn kopii zapasowych w ramach subskrypcji, zobacz hello wersja Menedżera zasobów tego artykułu, [AzureRM.RecoveryServices.Backup użyj polecenia cmdlet tooback zapasowe](backup-azure-vms-automation.md).</span><span class="sxs-lookup"><span data-stu-id="ef374-109">If you have not created a Backup vault in your subscription, see hello Resource Manager version of this article, [Use AzureRM.RecoveryServices.Backup cmdlets tooback up virtual machines](backup-azure-vms-automation.md).</span></span> <span data-ttu-id="ef374-110">Firma Microsoft zaleca, aby większości nowych wdrożeń korzystać hello modelu Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="ef374-110">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="ef374-111">Teraz można uaktualnić Twoje Magazyny usług tooRecovery magazynów kopii zapasowych.</span><span class="sxs-lookup"><span data-stu-id="ef374-111">You can now upgrade your Backup vaults tooRecovery Services vaults.</span></span> <span data-ttu-id="ef374-112">Aby uzyskać więcej informacji, zobacz artykuł hello [uaktualnienia tooa magazynu kopii zapasowej, Magazyn usług odzyskiwania i](backup-azure-upgrade-backup-to-recovery-services.md).</span><span class="sxs-lookup"><span data-stu-id="ef374-112">For details, see hello article [Upgrade a Backup vault tooa Recovery Services vault](backup-azure-upgrade-backup-to-recovery-services.md).</span></span> <span data-ttu-id="ef374-113">Firma Microsoft zachęca tooupgrade Magazyny usług tooRecovery magazyny kopii zapasowych.</span><span class="sxs-lookup"><span data-stu-id="ef374-113">Microsoft encourages you tooupgrade your Backup vaults tooRecovery Services vaults.</span></span><br/> <span data-ttu-id="ef374-114">Po 15 października 2017 nie można użyć magazyny kopii zapasowych toocreate środowiska PowerShell.</span><span class="sxs-lookup"><span data-stu-id="ef374-114">After October 15, 2017, you can’t use PowerShell toocreate Backup vaults.</span></span> <span data-ttu-id="ef374-115">**Do 1 listopada 2017 r.**:</span><span class="sxs-lookup"><span data-stu-id="ef374-115">**By November 1, 2017**:</span></span>
>- <span data-ttu-id="ef374-116">Wszystkie pozostałe magazyny kopii zapasowych zostanie automatycznie uaktualniony tooRecovery Magazyny usług.</span><span class="sxs-lookup"><span data-stu-id="ef374-116">All remaining Backup vaults will be automatically upgraded tooRecovery Services vaults.</span></span>
>- <span data-ttu-id="ef374-117">Użytkownik nie będzie możliwe tooaccess danych kopii zapasowych w portalu klasycznym hello.</span><span class="sxs-lookup"><span data-stu-id="ef374-117">You won't be able tooaccess your backup data in hello classic portal.</span></span> <span data-ttu-id="ef374-118">Zamiast tego użyj hello Azure tooaccess portalu tej kopii zapasowej w Magazyny usług odzyskiwania.</span><span class="sxs-lookup"><span data-stu-id="ef374-118">Instead, use hello Azure portal tooaccess your backup data in Recovery Services vaults.</span></span>
>

## <a name="concepts"></a><span data-ttu-id="ef374-119">Pojęcia</span><span class="sxs-lookup"><span data-stu-id="ef374-119">Concepts</span></span>
<span data-ttu-id="ef374-120">Ten artykuł zawiera informacje o określonym toohello poleceń cmdlet programu PowerShell używanych tooback zapasowych maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="ef374-120">This article provides information specific toohello PowerShell cmdlets used tooback up virtual machines.</span></span> <span data-ttu-id="ef374-121">Aby uzyskać informacje wprowadzające dotyczące ochrony maszyn wirtualnych platformy Azure, zobacz [Zaplanuj infrastrukturę kopii zapasowej maszyny Wirtualnej na platformie Azure](backup-azure-vms-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="ef374-121">For introductory information about protecting Azure VMs, please see [Plan your VM backup infrastructure in Azure](backup-azure-vms-introduction.md).</span></span>

> [!NOTE]
> <span data-ttu-id="ef374-122">Przed rozpoczęciem przeczytaj hello [wymagania wstępne](backup-azure-vms-prepare.md) wymagane toowork z usługi Kopia zapasowa Azure i hello [ograniczenia](backup-azure-vms-prepare.md#limitations-when-backing-up-and-restoring-a-vm) bieżącego rozwiązania kopii zapasowej hello maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="ef374-122">Before you start, read hello [prerequisites](backup-azure-vms-prepare.md) required toowork with Azure Backup, and hello [limitations](backup-azure-vms-prepare.md#limitations-when-backing-up-and-restoring-a-vm) of hello current VM backup solution.</span></span>
>
>

<span data-ttu-id="ef374-123">toouse PowerShell efektywnie zająć chwilę toounderstand hello hierarchię obiektów i z jakiej lokalizacji toostart.</span><span class="sxs-lookup"><span data-stu-id="ef374-123">toouse PowerShell effectively, take a moment toounderstand hello hierarchy of objects and from where toostart.</span></span>

![Hierarchia obiektów](./media/backup-azure-vms-classic-automation/object-hierarchy.png)

<span data-ttu-id="ef374-125">Witaj dwóch przepływów najważniejszych są włączania ochrony dla maszyny Wirtualnej i przywrócić dane z punktu odzyskiwania.</span><span class="sxs-lookup"><span data-stu-id="ef374-125">hello two most important flows are enabling protection for a VM, and restoring data from a recovery point.</span></span> <span data-ttu-id="ef374-126">Witaj ten artykuł koncentruje się toohelp staje się doświadczenie w pracy z tooenable poleceń cmdlet programu PowerShell hello tych dwóch scenariuszy.</span><span class="sxs-lookup"><span data-stu-id="ef374-126">hello focus of this article is toohelp you become adept at working with hello PowerShell cmdlets tooenable these two scenarios.</span></span>

## <a name="setup-and-registration"></a><span data-ttu-id="ef374-127">Instalację i rejestrację</span><span class="sxs-lookup"><span data-stu-id="ef374-127">Setup and Registration</span></span>
<span data-ttu-id="ef374-128">toobegin:</span><span class="sxs-lookup"><span data-stu-id="ef374-128">toobegin:</span></span>

1. <span data-ttu-id="ef374-129">[Pobierz najnowsze PowerShell](https://github.com/Azure/azure-powershell/releases) (minimalna wersja wymagana jest: 1.0.0)</span><span class="sxs-lookup"><span data-stu-id="ef374-129">[Download latest PowerShell](https://github.com/Azure/azure-powershell/releases) (minimum version required is : 1.0.0)</span></span>
2. <span data-ttu-id="ef374-130">Znajdź hello programu PowerShell usługi Azure Backup dostępnych poleceń cmdlet, wpisując następujące polecenie hello:</span><span class="sxs-lookup"><span data-stu-id="ef374-130">Find hello Azure Backup PowerShell cmdlets available by typing hello following command:</span></span>

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

<span data-ttu-id="ef374-131">Witaj następujące ustawienia i zadania rejestracji można zautomatyzować przy użyciu programu PowerShell:</span><span class="sxs-lookup"><span data-stu-id="ef374-131">hello following setup and registration tasks can be automated with PowerShell:</span></span>

* <span data-ttu-id="ef374-132">Tworzenie magazynu kopii zapasowych</span><span class="sxs-lookup"><span data-stu-id="ef374-132">Create a backup vault</span></span>
* <span data-ttu-id="ef374-133">Rejestrowanie hello maszyn wirtualnych z hello usługi Kopia zapasowa Azure</span><span class="sxs-lookup"><span data-stu-id="ef374-133">Registering hello VMs with hello Azure Backup service</span></span>

### <a name="create-a-backup-vault"></a><span data-ttu-id="ef374-134">Tworzenie magazynu kopii zapasowych</span><span class="sxs-lookup"><span data-stu-id="ef374-134">Create a backup vault</span></span>
> [!WARNING]
> <span data-ttu-id="ef374-135">W przypadku klientów przy kopia zapasowa Azure powitania po raz pierwszy należy tooregister hello kopia zapasowa Azure dostawcy toobe używane w ramach subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="ef374-135">For customers using Azure Backup for hello first time, you need tooregister hello Azure Backup provider toobe used with your subscription.</span></span> <span data-ttu-id="ef374-136">Można to zrobić, uruchamiając następujące polecenie hello: Register-AzureRmResourceProvider - ProviderNamespace "Microsoft.Backup"</span><span class="sxs-lookup"><span data-stu-id="ef374-136">This can be done by running hello following command: Register-AzureRmResourceProvider -ProviderNamespace "Microsoft.Backup"</span></span>
>
>

<span data-ttu-id="ef374-137">Można utworzyć nowy magazyn kopii zapasowych za pomocą hello **AzureRmBackupVault nowy** polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="ef374-137">You can create a new backup vault using hello **New-AzureRmBackupVault** cmdlet.</span></span> <span data-ttu-id="ef374-138">Hello magazynu kopii zapasowych jest zasobem ARM, więc należy tooplace go w grupie zasobów.</span><span class="sxs-lookup"><span data-stu-id="ef374-138">hello backup vault is an ARM resource, so you need tooplace it within a Resource Group.</span></span> <span data-ttu-id="ef374-139">W konsoli programu Azure PowerShell z podwyższonym poziomem uprawnień uruchom następujące polecenia hello:</span><span class="sxs-lookup"><span data-stu-id="ef374-139">In an elevated Azure PowerShell console, run hello following commands:</span></span>

```
PS C:\> New-AzureRmResourceGroup –Name “test-rg” –Location “West US”
PS C:\> $backupvault = New-AzureRmBackupVault –ResourceGroupName “test-rg” –Name “test-vault” –Region “West US” –Storage GeoRedundant
```

<span data-ttu-id="ef374-140">Można uzyskać listę wszystkich magazynów kopii zapasowych hello w ramach danej subskrypcji przy użyciu hello **Get-AzureRmBackupVault** polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="ef374-140">You can get a list of all hello backup vaults in a given subscription using hello **Get-AzureRmBackupVault** cmdlet.</span></span>

> [!NOTE]
> <span data-ttu-id="ef374-141">Jest wygodną toostore hello magazynu kopii zapasowych obiekt w zmiennej.</span><span class="sxs-lookup"><span data-stu-id="ef374-141">It is convenient toostore hello backup vault object into a variable.</span></span> <span data-ttu-id="ef374-142">Obiekt magazynu Hello jest potrzebny jako dane wejściowe dla wielu poleceń cmdlet narzędzia Kopia zapasowa Azure.</span><span class="sxs-lookup"><span data-stu-id="ef374-142">hello vault object is needed as an input for many Azure Backup cmdlets.</span></span>
>
>

### <a name="registering-hello-vms"></a><span data-ttu-id="ef374-143">Rejestrowanie hello maszyny wirtualne</span><span class="sxs-lookup"><span data-stu-id="ef374-143">Registering hello VMs</span></span>
<span data-ttu-id="ef374-144">pierwszy krok Hello w kierunku Konfigurowanie tworzenia kopii zapasowych w usłudze Kopia zapasowa Azure jest tooregister Twojego komputera lub maszyny Wirtualnej w magazynie usługi Kopia zapasowa Azure.</span><span class="sxs-lookup"><span data-stu-id="ef374-144">hello first step towards configuring backup with Azure Backup is tooregister your machine or VM with an Azure Backup vault.</span></span> <span data-ttu-id="ef374-145">Witaj **AzureRmBackupContainer rejestru** polecenie cmdlet pobiera dane wejściowe hello maszyny wirtualne Azure IaaS i rejestruje go wraz hello określonego magazynu.</span><span class="sxs-lookup"><span data-stu-id="ef374-145">hello **Register-AzureRmBackupContainer** cmdlet takes hello input information of an Azure IaaS virtual machine and registers it with hello specified vault.</span></span> <span data-ttu-id="ef374-146">Operacja rejestracji Hello kojarzy hello Azure maszyny wirtualnej z magazynu kopii zapasowych hello i śledzi hello maszyny Wirtualnej za pośrednictwem hello cyklu tworzenia kopii zapasowej.</span><span class="sxs-lookup"><span data-stu-id="ef374-146">hello register operation associates hello Azure virtual machine with hello backup vault and tracks hello VM through hello backup lifecycle.</span></span>

<span data-ttu-id="ef374-147">Rejestrowanie maszyny Wirtualnej z hello usługi Azure Backup tworzy obiekt kontenerem najwyższego poziomu.</span><span class="sxs-lookup"><span data-stu-id="ef374-147">Registering your VM with hello Azure Backup service creates a top-level container object.</span></span> <span data-ttu-id="ef374-148">Kontener zwykle zawiera wiele elementów, które można utworzyć kopię zapasową, ale w przypadku hello maszyn wirtualnych będzie tylko jeden element kopii zapasowej hello kontenera.</span><span class="sxs-lookup"><span data-stu-id="ef374-148">A container typically contains multiple items that can be backed up, but in hello case of VMs there will be only one backup item for hello container.</span></span>

```
PS C:\> $registerjob = Register-AzureRmBackupContainer -Vault $backupvault -Name "testvm" -ServiceName "testvm"
```

## <a name="backup-azure-vms"></a><span data-ttu-id="ef374-149">Tworzenie kopii zapasowych maszyn wirtualnych platformy Azure</span><span class="sxs-lookup"><span data-stu-id="ef374-149">Backup Azure VMs</span></span>
### <a name="create-a-protection-policy"></a><span data-ttu-id="ef374-150">Tworzenie zasad ochrony</span><span class="sxs-lookup"><span data-stu-id="ef374-150">Create a protection policy</span></span>
<span data-ttu-id="ef374-151">Nie jest obowiązkowe toocreate nową ochrony zasad toostart kopię zapasową maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="ef374-151">It is not mandatory toocreate a new protection policy toostart backup of your VMs.</span></span> <span data-ttu-id="ef374-152">Magazyn Hello jest dostarczany z "Domyślne zasady" mogą być używane tooquickly Włączanie ochrony, a następnie edytować później za pomocą hello szczegółów prawym.</span><span class="sxs-lookup"><span data-stu-id="ef374-152">hello vault comes with a 'Default Policy' that can be used tooquickly enable protection, and then edited later with hello right details.</span></span> <span data-ttu-id="ef374-153">Listę dostępnych w magazynie hello zasad hello można uzyskać za pomocą hello **Get-AzureRmBackupProtectionPolicy** polecenia cmdlet:</span><span class="sxs-lookup"><span data-stu-id="ef374-153">You can get a list of hello policies available in hello vault by using hello **Get-AzureRmBackupProtectionPolicy** cmdlet:</span></span>

```
PS C:\> Get-AzureRmBackupProtectionPolicy -Vault $backupvault

Name                      Type               ScheduleType       BackupTime
----                      ----               ------------       ----------
DefaultPolicy             AzureVM            Daily              26-Aug-15 12:30:00 AM
```

> [!NOTE]
> <span data-ttu-id="ef374-154">Strefa czasowa Hello hello BackupTime pola w programie PowerShell jest czasem UTC.</span><span class="sxs-lookup"><span data-stu-id="ef374-154">hello timezone of hello BackupTime field in PowerShell is UTC.</span></span> <span data-ttu-id="ef374-155">Jednak podczas wykonywania kopii zapasowej hello jest wyświetlany w hello portalu Azure, strefy czasowej hello jest wyrównany tooyour systemu lokalnego, wraz z przesunięciem hello UTC.</span><span class="sxs-lookup"><span data-stu-id="ef374-155">However, when hello backup time is shown in hello Azure portal, hello timezone is aligned tooyour local system along with hello UTC offset.</span></span>
>
>

<span data-ttu-id="ef374-156">Zasady tworzenia kopii zapasowej jest skojarzony z co najmniej jedne zasady przechowywania.</span><span class="sxs-lookup"><span data-stu-id="ef374-156">A backup policy is associated with at least one retention policy.</span></span> <span data-ttu-id="ef374-157">zasady przechowywania Hello określają, jak długo punkt odzyskiwania jest przechowywany z usługi Kopia zapasowa Azure.</span><span class="sxs-lookup"><span data-stu-id="ef374-157">hello retention policy defines how long a recovery point is kept with Azure Backup.</span></span> <span data-ttu-id="ef374-158">Witaj **AzureRmBackupRetentionPolicy nowy** polecenie cmdlet tworzy obiekty programu PowerShell, zawierających informacje o zasadach przechowywania.</span><span class="sxs-lookup"><span data-stu-id="ef374-158">hello **New-AzureRmBackupRetentionPolicy** cmdlet creates PowerShell objects that hold retention policy information.</span></span> <span data-ttu-id="ef374-159">Te obiekty zasad przechowywania są używane jako danych wejściowych toohello *AzureRmBackupProtectionPolicy nowy* polecenia cmdlet, lub bezpośrednio z hello *AzureRmBackupProtection Włącz* polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="ef374-159">These retention policy objects are used as inputs toohello *New-AzureRmBackupProtectionPolicy* cmdlet, or directly with hello *Enable-AzureRmBackupProtection* cmdlet.</span></span>

<span data-ttu-id="ef374-160">Zasady tworzenia kopii zapasowej definiuje kiedy i jak często hello kopii zapasowej elementu odbywa się.</span><span class="sxs-lookup"><span data-stu-id="ef374-160">A backup policy defines when and how often hello backup of an item is done.</span></span> <span data-ttu-id="ef374-161">Witaj **AzureRmBackupProtectionPolicy nowy** polecenie cmdlet tworzy obiekt programu PowerShell, która przechowuje informacje o zasadach tworzenia kopii zapasowej.</span><span class="sxs-lookup"><span data-stu-id="ef374-161">hello **New-AzureRmBackupProtectionPolicy** cmdlet creates a PowerShell object that holds backup policy information.</span></span> <span data-ttu-id="ef374-162">Witaj zasad tworzenia kopii zapasowej jest używany jako wejściowych toohello *AzureRmBackupProtection Włącz* polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="ef374-162">hello backup policy is used as an input toohello *Enable-AzureRmBackupProtection* cmdlet.</span></span>

```
PS C:\> $Daily = New-AzureRmBackupRetentionPolicyObject -DailyRetention -Retention 30
PS C:\> $newpolicy = New-AzureRmBackupProtectionPolicy -Name DailyBackup01 -Type AzureVM -Daily -BackupTime ([datetime]"3:30 PM") -RetentionPolicy $Daily -Vault $backupvault

Name                      Type               ScheduleType       BackupTime
----                      ----               ------------       ----------
DailyBackup01             AzureVM            Daily              01-Sep-15 3:30:00 PM
```

### <a name="enable-protection"></a><span data-ttu-id="ef374-163">Włączanie ochrony</span><span class="sxs-lookup"><span data-stu-id="ef374-163">Enable protection</span></span>
<span data-ttu-id="ef374-164">Włączanie ochrony obejmuje dwa obiekty — Witaj elementu i hello zasad, a oba toohello toobelong potrzeby sam magazyn.</span><span class="sxs-lookup"><span data-stu-id="ef374-164">Enabling protection involves two objects - hello Item and hello Policy, and both need toobelong toohello same vault.</span></span> <span data-ttu-id="ef374-165">Po hello zasady został skojarzony z elementem hello, przepływ pracy tworzenia kopii zapasowej hello będzie zaczną działać na powitania zdefiniowanym harmonogramem.</span><span class="sxs-lookup"><span data-stu-id="ef374-165">Once hello policy has been associated with hello item, hello backup workflow will kick in at hello defined schedule.</span></span>

```
PS C:\> Get-AzureRmBackupContainer -Type AzureVM -Status Registered -Vault $backupvault | Get-AzureRmBackupItem | Enable-AzureRmBackupProtection -Policy $newpolicy
```

### <a name="initial-backup"></a><span data-ttu-id="ef374-166">Początkowa kopia zapasowa</span><span class="sxs-lookup"><span data-stu-id="ef374-166">Initial backup</span></span>
<span data-ttu-id="ef374-167">harmonogram tworzenia kopii zapasowych Hello zajmie się czynności hello wstępny pełny kopii dla elementu hello i hello przyrostowej kopii hello kolejnych kopii zapasowych.</span><span class="sxs-lookup"><span data-stu-id="ef374-167">hello backup schedule will take care of doing hello full initial copy for hello item and hello incremental copy for hello subsequent backups.</span></span> <span data-ttu-id="ef374-168">Jednak jeśli chcesz tooforce hello początkowej kopii zapasowej toohappen w określonym czasie, lub nawet natychmiast Użyj hello **AzureRmBackupItem kopii zapasowej** polecenia cmdlet:</span><span class="sxs-lookup"><span data-stu-id="ef374-168">However, if you want tooforce hello initial backup toohappen at a certain time or even immediately then use hello **Backup-AzureRmBackupItem** cmdlet:</span></span>

```
PS C:\> $container = Get-AzureRmBackupContainer -Vault $backupvault -Type AzureVM -Name "testvm"
PS C:\> $backupjob = Get-AzureRmBackupItem -Container $container | Backup-AzureRmBackupItem
PS C:\> $backupjob

WorkloadName    Operation       Status          StartTime              EndTime
------------    ---------       ------          ---------              -------
testvm          Backup          InProgress      01-Sep-15 12:24:01 PM  01-Jan-01 12:00:00 AM
```

> [!NOTE]
> <span data-ttu-id="ef374-169">Witaj strefę czasową hello wartości StartTime i EndTime pól w programie PowerShell jest UTC.</span><span class="sxs-lookup"><span data-stu-id="ef374-169">hello timezone of hello StartTime and EndTime fields shown in PowerShell is UTC.</span></span> <span data-ttu-id="ef374-170">Jednak podczas hello podobne informacje są wyświetlane w portalu Azure hello, strefa czasowa hello jest wyrównany tooyour zegara systemu lokalnego.</span><span class="sxs-lookup"><span data-stu-id="ef374-170">However, when hello similar information is shown in hello Azure portal, hello timezone is aligned tooyour local system clock.</span></span>
>
>

### <a name="monitoring-a-backup-job"></a><span data-ttu-id="ef374-171">Monitorowanie zadania tworzenia kopii zapasowej</span><span class="sxs-lookup"><span data-stu-id="ef374-171">Monitoring a backup job</span></span>
<span data-ttu-id="ef374-172">Większość długotrwałej operacji w usłudze Kopia zapasowa Azure są sporządzony według wzoru jako zadanie.</span><span class="sxs-lookup"><span data-stu-id="ef374-172">Most long-running operations in Azure Backup are modelled as a job.</span></span> <span data-ttu-id="ef374-173">Dzięki temu postępu łatwe tootrack bez konieczności hello tookeep Otwieranie portalu Azure przez cały czas.</span><span class="sxs-lookup"><span data-stu-id="ef374-173">This makes it easy tootrack progress without having tookeep hello Azure portal open at all times.</span></span>

<span data-ttu-id="ef374-174">tooget hello najnowszy stan zadania w toku, użyj hello **Get-AzureRmBackupJob** polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="ef374-174">tooget hello latest status of an in-progress job, use hello **Get-AzureRmBackupJob** cmdlet.</span></span>

```
PS C:\> $joblist = Get-AzureRmBackupJob -Vault $backupvault -Status InProgress
PS C:\> $joblist[0]

WorkloadName    Operation       Status          StartTime              EndTime
------------    ---------       ------          ---------              -------
testvm          Backup          InProgress      01-Sep-15 12:24:01 PM  01-Jan-01 12:00:00 AM
```

<span data-ttu-id="ef374-175">Zamiast sondowania te zadania na zakończenie — czyli kod niepotrzebne, dodatkowe — jest prostsze hello toouse **AzureRmBackupJob oczekiwania** polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="ef374-175">Instead of polling these jobs for completion - which is unnecessary, additional code - it is simpler toouse hello **Wait-AzureRmBackupJob** cmdlet.</span></span> <span data-ttu-id="ef374-176">Używanego w skrypcie, polecenia cmdlet hello wstrzyma wykonywania hello dopóki hello określona wartość limitu czasu jest osiągana albo hello zadanie zostało ukończone.</span><span class="sxs-lookup"><span data-stu-id="ef374-176">When used in a script, hello cmdlet will pause hello execution until either hello job completes or hello specified timeout value is reached.</span></span>

```
PS C:\> Wait-AzureRmBackupJob -Job $joblist[0] -Timeout 43200
```


## <a name="restore-an-azure-vm"></a><span data-ttu-id="ef374-177">Przywracanie maszyny Wirtualnej platformy Azure</span><span class="sxs-lookup"><span data-stu-id="ef374-177">Restore an Azure VM</span></span>
<span data-ttu-id="ef374-178">W kolejności toorestore dane kopii zapasowej należy tooidentify hello kopii zapasowej elementu i hello punkt odzyskiwania, który zawiera dane w momencie hello.</span><span class="sxs-lookup"><span data-stu-id="ef374-178">In order toorestore backup data, you need tooidentify hello backed-up Item and hello Recovery Point that holds hello point-in-time data.</span></span> <span data-ttu-id="ef374-179">Te informacje są podane toohello AzureRmBackupItem przywracania polecenia cmdlet tooinitiate przywracania danych z konta klienta hello magazynu toohello.</span><span class="sxs-lookup"><span data-stu-id="ef374-179">This information is supplied toohello Restore-AzureRmBackupItem cmdlet tooinitiate a restore of data from hello vault toohello customer's account.</span></span>

### <a name="select-hello-vm"></a><span data-ttu-id="ef374-180">Wybierz hello maszyny Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="ef374-180">Select hello VM</span></span>
<span data-ttu-id="ef374-181">obiekt programu PowerShell hello tooget, który identyfikuje hello elementu prawo kopii zapasowej, należy toostart z hello kontenera w magazynie hello i przechodzić w dół hierarchii obiektów.</span><span class="sxs-lookup"><span data-stu-id="ef374-181">tooget hello PowerShell object that identifies hello right backup Item, you need toostart from hello Container in hello vault, and work your way down object hierarchy.</span></span> <span data-ttu-id="ef374-182">tooselect hello kontener, który reprezentuje hello maszyny Wirtualnej, użyj hello **Get-AzureRmBackupContainer** polecenia cmdlet i przekazać w potoku tego toohello **Get-AzureRmBackupItem** polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="ef374-182">tooselect hello container that represents hello VM, use hello **Get-AzureRmBackupContainer** cmdlet and pipe that toohello **Get-AzureRmBackupItem** cmdlet.</span></span>

```
PS C:\> $backupitem = Get-AzureRmBackupContainer -Vault $backupvault -Type AzureVM -name "testvm" | Get-AzureRmBackupItem
```

### <a name="choose-a-recovery-point"></a><span data-ttu-id="ef374-183">Wybierz punkt odzyskiwania</span><span class="sxs-lookup"><span data-stu-id="ef374-183">Choose a recovery point</span></span>
<span data-ttu-id="ef374-184">Można teraz wyświetlić listę wszystkich punktów odzyskiwania hello hello elementu kopii zapasowej za pomocą hello **Get-AzureRmBackupRecoveryPoint** polecenia cmdlet i wybierz polecenie toorestore punktu odzyskiwania hello.</span><span class="sxs-lookup"><span data-stu-id="ef374-184">You can now list all hello recovery points for hello backup item using hello **Get-AzureRmBackupRecoveryPoint** cmdlet, and choose hello recovery point toorestore.</span></span> <span data-ttu-id="ef374-185">Zazwyczaj użytkowników pobranie najnowszych hello *AppConsistent* punktu hello na liście.</span><span class="sxs-lookup"><span data-stu-id="ef374-185">Typically users pick hello most recent *AppConsistent* point in hello list.</span></span>

```
PS C:\> $rp =  Get-AzureRmBackupRecoveryPoint -Item $backupitem
PS C:\> $rp

RecoveryPointId    RecoveryPointType  RecoveryPointTime      ContainerName
---------------    -----------------  -----------------      -------------
15273496567119     AppConsistent      01-Sep-15 12:27:38 PM  iaasvmcontainer;testvm;testv...
```

<span data-ttu-id="ef374-186">Zmienna Hello ```$rp``` jest tablicą punkty odzyskiwania dla hello zaznaczony element kopii zapasowej, posortowane w kolejności odwrotnej czas — Witaj najnowszy punkt odzyskiwania znajduje się pod indeksem 0.</span><span class="sxs-lookup"><span data-stu-id="ef374-186">hello variable ```$rp``` is an array of recovery points for hello selected backup item, sorted in reverse order of time - hello latest recovery point is at index 0.</span></span> <span data-ttu-id="ef374-187">Użyj standardowych tablicy PowerShell indeksowania punkt odzyskiwania hello toopick.</span><span class="sxs-lookup"><span data-stu-id="ef374-187">Use standard PowerShell array indexing toopick hello recovery point.</span></span> <span data-ttu-id="ef374-188">Na przykład: ```$rp[0]``` wybierze hello najnowszego punktu odzyskiwania.</span><span class="sxs-lookup"><span data-stu-id="ef374-188">For example: ```$rp[0]``` will select hello latest recovery point.</span></span>

### <a name="restoring-disks"></a><span data-ttu-id="ef374-189">Przywracanie dysków</span><span class="sxs-lookup"><span data-stu-id="ef374-189">Restoring disks</span></span>
<span data-ttu-id="ef374-190">Brak klucza różnica między operacje przywracania hello wykonywane za pośrednictwem hello portalu Azure i przy użyciu programu Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="ef374-190">There is a key difference between hello restore operations done through hello Azure portal and through Azure PowerShell.</span></span> <span data-ttu-id="ef374-191">Przy użyciu programu PowerShell operacji przywracania hello zatrzymuje przy przywracaniu dysków hello i informacje o konfiguracji z hello punktu odzyskiwania.</span><span class="sxs-lookup"><span data-stu-id="ef374-191">With PowerShell, hello restore operation stops at restoring hello disks and config information from hello recovery point.</span></span> <span data-ttu-id="ef374-192">Nie tworzy maszynę wirtualną.</span><span class="sxs-lookup"><span data-stu-id="ef374-192">It does not create a virtual machine.</span></span>

> [!WARNING]
> <span data-ttu-id="ef374-193">Witaj AzureRmBackupItem przywracania nie powoduje utworzenia maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="ef374-193">hello Restore-AzureRmBackupItem does not create a VM.</span></span> <span data-ttu-id="ef374-194">Przywraca jedynie dyski hello toohello określono konto magazynu.</span><span class="sxs-lookup"><span data-stu-id="ef374-194">It only restores hello disks toohello specified storage account.</span></span> <span data-ttu-id="ef374-195">Nie jest to hello takie samo zachowanie, które wystąpią w hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="ef374-195">This is not hello same behavior you will experience in hello Azure portal.</span></span>
>
>

```
PS C:\> $restorejob = Restore-AzureRmBackupItem -StorageAccountName "DestAccount" -RecoveryPoint $rp[0]
PS C:\> $restorejob

WorkloadName    Operation       Status          StartTime              EndTime
------------    ---------       ------          ---------              -------
testvm          Restore         InProgress      01-Sep-15 1:14:01 PM   01-Jan-01 12:00:00 AM
```

<span data-ttu-id="ef374-196">Można uzyskać szczegółów hello hello operacji przywracania, używając hello **Get-AzureRmBackupJobDetails** polecenia cmdlet, po zakończeniu zadania przywracania hello.</span><span class="sxs-lookup"><span data-stu-id="ef374-196">You can get hello details of hello restore operation using hello **Get-AzureRmBackupJobDetails** cmdlet once hello Restore job has completed.</span></span> <span data-ttu-id="ef374-197">Witaj *szczegóły błędu* właściwość będzie mieć informacji hello potrzebne toorebuild hello maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="ef374-197">hello *ErrorDetails* property will have hello information needed toorebuild hello VM.</span></span>

```
PS C:\> $restorejob = Get-AzureRmBackupJob -Job $restorejob
PS C:\> $details = Get-AzureRmBackupJobDetails -Job $restorejob
```

### <a name="build-hello-vm"></a><span data-ttu-id="ef374-198">Tworzenie hello maszyny Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="ef374-198">Build hello VM</span></span>
<span data-ttu-id="ef374-199">Hello tworzenia maszyny Wirtualnej poza hello przywrócić dysków jest możliwe za pomocą hello starszych poleceń cmdlet programu PowerShell do zarządzania usługi Azure, hello nowych szablonów usługi Azure Resource Manager lub nawet hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="ef374-199">Building hello VM out of hello restored disks can be done using hello older Azure Service Management PowerShell cmdlets, hello new Azure Resource Manager templates, or even using hello Azure portal.</span></span> <span data-ttu-id="ef374-200">W szybkim przykładzie pokazano, jak tooget miejsca przy użyciu poleceń cmdlet usługi Azure Service Management hello.</span><span class="sxs-lookup"><span data-stu-id="ef374-200">In a quick example, we will show how tooget there using hello Azure Service Management cmdlets.</span></span>

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

<span data-ttu-id="ef374-201">Aby uzyskać więcej informacji na temat toobuild Maszynę wirtualną z dysków hello przywrócone, przeczytaj o hello następującego polecenia cmdlet:</span><span class="sxs-lookup"><span data-stu-id="ef374-201">For more information on how toobuild a VM from hello restored disks, read about hello following cmdlets:</span></span>

* [<span data-ttu-id="ef374-202">Dodaj AzureDisk</span><span class="sxs-lookup"><span data-stu-id="ef374-202">Add-AzureDisk</span></span>](https://msdn.microsoft.com/library/azure/dn495252.aspx)
* [<span data-ttu-id="ef374-203">Nowe AzureVMConfig</span><span class="sxs-lookup"><span data-stu-id="ef374-203">New-AzureVMConfig</span></span>](https://msdn.microsoft.com/library/azure/dn495159.aspx)
* [<span data-ttu-id="ef374-204">Nowe AzureVM</span><span class="sxs-lookup"><span data-stu-id="ef374-204">New-AzureVM</span></span>](https://msdn.microsoft.com/library/azure/dn495254.aspx)

## <a name="code-samples"></a><span data-ttu-id="ef374-205">Przykłady kodu</span><span class="sxs-lookup"><span data-stu-id="ef374-205">Code samples</span></span>
### <a name="1-get-hello-completion-status-of-job-sub-tasks"></a><span data-ttu-id="ef374-206">1. Pobierz stan ukończenia hello zadania podrzędne zadania</span><span class="sxs-lookup"><span data-stu-id="ef374-206">1. Get hello completion status of job sub-tasks</span></span>
<span data-ttu-id="ef374-207">Stan ukończenia hello tootrack poszczególnych zadań podrzędnych, można użyć hello **Get-AzureRmBackupJobDetails** polecenia cmdlet:</span><span class="sxs-lookup"><span data-stu-id="ef374-207">tootrack hello completion status of individual sub-tasks, you can use hello **Get-AzureRmBackupJobDetails** cmdlet:</span></span>

```
PS C:\> $details = Get-AzureRmBackupJobDetails -JobId $backupjob.InstanceId -Vault $backupvault
PS C:\> $details.SubTasks

Name                                                        Status
----                                                        ------
Take Snapshot                                               Completed
Transfer data tooBackup vault                               InProgress
```

### <a name="2-create-a-dailyweekly-report-of-backup-jobs"></a><span data-ttu-id="ef374-208">2. Tworzenie raportu codziennie/cotygodniowych zadań tworzenia kopii zapasowej</span><span class="sxs-lookup"><span data-stu-id="ef374-208">2. Create a daily/weekly report of backup jobs</span></span>
<span data-ttu-id="ef374-209">Administratorzy mają zwykle tooknow jakie zadania tworzenia kopii zapasowej został uruchomiony w hello ostatnich 24 godzinach, stan hello tych zadań tworzenia kopii zapasowej.</span><span class="sxs-lookup"><span data-stu-id="ef374-209">Administrators typically want tooknow what backup jobs ran in hello last 24 hours, hello status of those backup jobs.</span></span> <span data-ttu-id="ef374-210">Ponadto hello ilość danych przesyłanych zapewnia administratorom tooestimate sposób ich miesięcznego użycia danych.</span><span class="sxs-lookup"><span data-stu-id="ef374-210">Additionally, hello amount of data transferred gives administrators a way tooestimate their monthly data usage.</span></span> <span data-ttu-id="ef374-211">Poniższy skrypt Hello pobiera hello nieprzetworzone dane z hello usługi Kopia zapasowa Azure i wyświetla informacje hello w konsoli programu PowerShell hello.</span><span class="sxs-lookup"><span data-stu-id="ef374-211">hello script below pulls hello raw data from hello Azure Backup service and displays hello information in hello PowerShell console.</span></span>

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

<span data-ttu-id="ef374-212">Jeśli chcesz tooadd wykresów dane wyjściowe raportu toothis możliwości nauki TechNet hello wpis w blogu [wykresów przy użyciu programu PowerShell](http://blogs.technet.com/b/richard_macdonald/archive/2009/04/28/3231887.aspx)</span><span class="sxs-lookup"><span data-stu-id="ef374-212">If you want tooadd charting capabilities toothis report output, learn from hello TechNet blog post [Charting with PowerShell](http://blogs.technet.com/b/richard_macdonald/archive/2009/04/28/3231887.aspx)</span></span>

## <a name="next-steps"></a><span data-ttu-id="ef374-213">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="ef374-213">Next steps</span></span>
<span data-ttu-id="ef374-214">Jeśli wolisz przy użyciu programu PowerShell tooengage z zasobów platformy Azure, zapoznaj się artykuł PowerShell hello ochrony systemu Windows Server, [wdrażanie i zarządzanie kopia zapasowa systemu Windows Server](backup-client-automation-classic.md).</span><span class="sxs-lookup"><span data-stu-id="ef374-214">If you prefer using PowerShell tooengage with your Azure resources, check out hello PowerShell article for protecting Windows Server, [Deploy and Manage Backup for Windows Server](backup-client-automation-classic.md).</span></span> <span data-ttu-id="ef374-215">Jest również artykuł programu PowerShell do zarządzania kopii zapasowych programu DPM, [wdrażanie i zarządzanie kopii zapasowej programu DPM](backup-dpm-automation-classic.md).</span><span class="sxs-lookup"><span data-stu-id="ef374-215">There is also a PowerShell article for managing DPM backups, [Deploy and Manage Backup for DPM](backup-dpm-automation-classic.md).</span></span> <span data-ttu-id="ef374-216">Mieć obu tych artykułach wersji dla wdrożenia usługi Resource Manager oraz wdrożenia klasycznego.</span><span class="sxs-lookup"><span data-stu-id="ef374-216">Both of these articles have a version for Resource Manager deployments as well as Classic deployments.</span></span>
