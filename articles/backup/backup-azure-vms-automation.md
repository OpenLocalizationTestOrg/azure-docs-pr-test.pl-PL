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
# <a name="use-azurermrecoveryservicesbackup-cmdlets-tooback-up-virtual-machines"></a><span data-ttu-id="ac974-103">Użyj tooback poleceń cmdlet AzureRM.RecoveryServices.Backup zapasowych maszyn wirtualnych</span><span class="sxs-lookup"><span data-stu-id="ac974-103">Use AzureRM.RecoveryServices.Backup cmdlets tooback up virtual machines</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="ac974-104">Resource Manager</span><span class="sxs-lookup"><span data-stu-id="ac974-104">Resource Manager</span></span>](backup-azure-vms-automation.md)
> * [<span data-ttu-id="ac974-105">Wdrożenie klasyczne</span><span class="sxs-lookup"><span data-stu-id="ac974-105">Classic</span></span>](backup-azure-vms-classic-automation.md)
>
>

<span data-ttu-id="ac974-106">W tym artykule opisano, jak magazyn tooback poleceń cmdlet programu Azure PowerShell toouse zapasowej i odzyskiwanie maszyny wirtualnej platformy Azure (VM) z usług odzyskiwania.</span><span class="sxs-lookup"><span data-stu-id="ac974-106">This article shows you how toouse Azure PowerShell cmdlets tooback up and recover an Azure virtual machine (VM) from a Recovery Services vault.</span></span> <span data-ttu-id="ac974-107">Magazyn usług odzyskiwania jest zasobów usługi Azure Resource Manager i tooprotect używanych danych i zasobów w usługach zarówno Azure Backup i Azure Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="ac974-107">A Recovery Services vault is an Azure Resource Manager resource and is used tooprotect data and assets in both Azure Backup and Azure Site Recovery services.</span></span> <span data-ttu-id="ac974-108">Można użyć tooprotect magazyn usług odzyskiwania Azure Service Manager wdrożone maszyny wirtualne i usługi Azure Resource Manager wdrożone maszyny wirtualne.</span><span class="sxs-lookup"><span data-stu-id="ac974-108">You can use a Recovery Services vault tooprotect Azure Service Manager-deployed VMs, and Azure Resource Manager-deployed VMs.</span></span>

> [!NOTE]
> <span data-ttu-id="ac974-109">Platforma Azure ma dwa modele wdrażania związane z tworzeniem zasobów i pracą z nimi: [Resource Manager i model klasyczny](../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="ac974-109">Azure has two deployment models for creating and working with resources: [Resource Manager and Classic](../azure-resource-manager/resource-manager-deployment-model.md).</span></span> <span data-ttu-id="ac974-110">W tym artykule jest przeznaczona do użytku z maszyn wirtualnych utworzonych przy użyciu hello modelu Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="ac974-110">This article is for use with VMs created using hello Resource Manager model.</span></span>
>
>

<span data-ttu-id="ac974-111">W tym artykule przedstawiono przy użyciu programu PowerShell tooprotect maszyny Wirtualnej i przywracanie danych z punktu odzyskiwania.</span><span class="sxs-lookup"><span data-stu-id="ac974-111">This article walks you through using PowerShell tooprotect a VM, and restore data from a recovery point.</span></span>

## <a name="concepts"></a><span data-ttu-id="ac974-112">Pojęcia</span><span class="sxs-lookup"><span data-stu-id="ac974-112">Concepts</span></span>
<span data-ttu-id="ac974-113">Jeśli nie masz doświadczenia w obsłudze hello usługi Kopia zapasowa Azure Omówienie usługi hello wyewidencjonować [co to jest kopia zapasowa Azure?](backup-introduction-to-azure-backup.md)</span><span class="sxs-lookup"><span data-stu-id="ac974-113">If you are not familiar with hello Azure Backup service, for an overview of hello service, check out [What is Azure Backup?](backup-introduction-to-azure-backup.md)</span></span> <span data-ttu-id="ac974-114">Przed rozpoczęciem upewnij się, obejmują essentials hello o toowork wymagania wstępne niezbędne hello w usłudze Kopia zapasowa Azure i hello ograniczenia bieżące rozwiązanie tworzenia kopii zapasowej hello maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="ac974-114">Before you start, ensure that you cover hello essentials about hello prerequisites needed toowork with Azure Backup, and hello limitations of hello current VM backup solution.</span></span>

<span data-ttu-id="ac974-115">toouse PowerShell ostatecznie jest konieczne toounderstand hello hierarchii obiektów i z jakiej lokalizacji toostart.</span><span class="sxs-lookup"><span data-stu-id="ac974-115">toouse PowerShell effectively, it is necessary toounderstand hello hierarchy of objects and from where toostart.</span></span>

![Hierarchia obiektów usługi odzyskiwania](./media/backup-azure-vms-arm-automation/recovery-services-object-hierarchy.png)

<span data-ttu-id="ac974-117">Witaj tooview AzureRm.RecoveryServices.Backup polecenia cmdlet w programie PowerShell, zobacz hello [kopia zapasowa Azure - polecenia cmdlet usług odzyskiwania](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup) w hello Azure biblioteki.</span><span class="sxs-lookup"><span data-stu-id="ac974-117">tooview hello AzureRm.RecoveryServices.Backup PowerShell cmdlet reference, see hello [Azure Backup - Recovery Services Cmdlets](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup) in hello Azure library.</span></span>

## <a name="setup-and-registration"></a><span data-ttu-id="ac974-118">Instalację i rejestrację</span><span class="sxs-lookup"><span data-stu-id="ac974-118">Setup and Registration</span></span>
<span data-ttu-id="ac974-119">toobegin:</span><span class="sxs-lookup"><span data-stu-id="ac974-119">toobegin:</span></span>

1. <span data-ttu-id="ac974-120">[Pobieranie najnowszej wersji programu PowerShell hello](https://docs.microsoft.com/powershell/azure/install-azurerm-ps) (hello minimalna wersja wymagana jest: 1.4.0)</span><span class="sxs-lookup"><span data-stu-id="ac974-120">[Download hello latest version of PowerShell](https://docs.microsoft.com/powershell/azure/install-azurerm-ps) (hello minimum version required is: 1.4.0)</span></span>
2. <span data-ttu-id="ac974-121">Znajdź hello programu PowerShell usługi Azure Backup dostępnych poleceń cmdlet, wpisując następujące polecenie hello:</span><span class="sxs-lookup"><span data-stu-id="ac974-121">Find hello Azure Backup PowerShell cmdlets available by typing hello following command:</span></span>

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


<span data-ttu-id="ac974-122">przy użyciu programu PowerShell można zautomatyzować Hello następujące zadania:</span><span class="sxs-lookup"><span data-stu-id="ac974-122">hello following tasks can be automated with PowerShell:</span></span>

* <span data-ttu-id="ac974-123">Tworzenie magazynu Usług odzyskiwania</span><span class="sxs-lookup"><span data-stu-id="ac974-123">Create a Recovery Services vault</span></span>
* <span data-ttu-id="ac974-124">Tworzenie kopii zapasowych maszyn wirtualnych platformy Azure</span><span class="sxs-lookup"><span data-stu-id="ac974-124">Back up Azure VMs</span></span>
* <span data-ttu-id="ac974-125">Wyzwalacz zadania tworzenia kopii zapasowej</span><span class="sxs-lookup"><span data-stu-id="ac974-125">Trigger a backup job</span></span>
* <span data-ttu-id="ac974-126">Monitor zadania tworzenia kopii zapasowej</span><span class="sxs-lookup"><span data-stu-id="ac974-126">Monitor a backup job</span></span>
* <span data-ttu-id="ac974-127">Przywracanie maszyny Wirtualnej platformy Azure</span><span class="sxs-lookup"><span data-stu-id="ac974-127">Restore an Azure VM</span></span>

## <a name="create-a-recovery-services-vault"></a><span data-ttu-id="ac974-128">Tworzenie magazynu usługi Recovery Services</span><span class="sxs-lookup"><span data-stu-id="ac974-128">Create a recovery services vault</span></span>
<span data-ttu-id="ac974-129">następujące kroki Hello przeprowadzi Cię przez tworzenie magazynu usług odzyskiwania.</span><span class="sxs-lookup"><span data-stu-id="ac974-129">hello following steps lead you through creating a Recovery Services vault.</span></span> <span data-ttu-id="ac974-130">Magazyn usług odzyskiwania są inne niż magazynu kopii zapasowych.</span><span class="sxs-lookup"><span data-stu-id="ac974-130">A Recovery Services vault is different than a Backup vault.</span></span>

1. <span data-ttu-id="ac974-131">Jeśli kopia zapasowa Azure jest używana do powitania po raz pierwszy, należy użyć hello  **[AzureRmResourceProvider rejestru](http://docs.microsoft.com/powershell/module/azurerm.resources/register-azurermresourceprovider)**  polecenia cmdlet tooregister hello Azure odzyskiwania usługodawcy w ramach subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="ac974-131">If you are using Azure Backup for hello first time, you must use hello **[Register-AzureRmResourceProvider](http://docs.microsoft.com/powershell/module/azurerm.resources/register-azurermresourceprovider)** cmdlet tooregister hello Azure Recovery Service provider with your subscription.</span></span>

    ```
    PS C:\> Register-AzureRmResourceProvider -ProviderNamespace "Microsoft.RecoveryServices"
    ```
2. <span data-ttu-id="ac974-132">Witaj magazyn usług odzyskiwania jest zasobu usługi Resource Manager, więc należy tooplace go w grupie zasobów.</span><span class="sxs-lookup"><span data-stu-id="ac974-132">hello Recovery Services vault is a Resource Manager resource, so you need tooplace it within a resource group.</span></span> <span data-ttu-id="ac974-133">Użyj istniejącej grupy zasobów lub Utwórz grupę zasobów o hello  **[New-AzureRmResourceGroup](https://docs.microsoft.com/powershell/module/azurerm.resources/new-azurermresourcegroup)**  polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="ac974-133">You can use an existing resource group, or create a resource group with hello **[New-AzureRmResourceGroup](https://docs.microsoft.com/powershell/module/azurerm.resources/new-azurermresourcegroup)** cmdlet.</span></span> <span data-ttu-id="ac974-134">Podczas tworzenia grupy zasobów, należy określić hello nazwę i lokalizację dla grupy zasobów hello.</span><span class="sxs-lookup"><span data-stu-id="ac974-134">When creating a resource group, specify hello name and location for hello resource group.</span></span>  

    ```
    PS C:\> New-AzureRmResourceGroup –Name "test-rg" –Location "West US"
    ```
3. <span data-ttu-id="ac974-135">Użyj hello  **[AzureRmRecoveryServicesVault nowy](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices/new-azurermrecoveryservicesvault)**  hello toocreate polecenia cmdlet magazynu usług odzyskiwania.</span><span class="sxs-lookup"><span data-stu-id="ac974-135">Use hello **[New-AzureRmRecoveryServicesVault](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices/new-azurermrecoveryservicesvault)** cmdlet toocreate hello Recovery Services vault.</span></span> <span data-ttu-id="ac974-136">Pamiętaj, toospecify hello tę samą lokalizację dla magazynu hello, które było używane dla grupy zasobów hello.</span><span class="sxs-lookup"><span data-stu-id="ac974-136">Be sure toospecify hello same location for hello vault as was used for hello resource group.</span></span>

    ```
    PS C:\> New-AzureRmRecoveryServicesVault -Name "testvault" -ResourceGroupName " test-rg" -Location "West US"
    ```
4. <span data-ttu-id="ac974-137">Określ typ hello toouse nadmiarowość magazynu; można użyć [lokalnie nadmiarowego magazynu (LRS)](../storage/common/storage-redundancy.md#locally-redundant-storage) lub [z magazynu geograficznie nadmiarowego magazynu (GRS)](../storage/common/storage-redundancy.md#geo-redundant-storage).</span><span class="sxs-lookup"><span data-stu-id="ac974-137">Specify hello type of storage redundancy toouse; you can use [Locally Redundant Storage (LRS)](../storage/common/storage-redundancy.md#locally-redundant-storage) or [Geo Redundant Storage (GRS)](../storage/common/storage-redundancy.md#geo-redundant-storage).</span></span> <span data-ttu-id="ac974-138">Witaj poniższy przykład przedstawia się, że opcja - BackupStorageRedundancy hello testvault ustawiono tooGeoRedundant.</span><span class="sxs-lookup"><span data-stu-id="ac974-138">hello following example shows hello -BackupStorageRedundancy option for testvault is set tooGeoRedundant.</span></span>

    ```
    PS C:\> $vault1 = Get-AzureRmRecoveryServicesVault –Name "testvault"
    PS C:\> Set-AzureRmRecoveryServicesBackupProperties  -Vault $vault1 -BackupStorageRedundancy GeoRedundant
    ```

   > [!TIP]
   > <span data-ttu-id="ac974-139">Wiele poleceń cmdlet narzędzia Kopia zapasowa Azure wymaga obiektu magazynu usług odzyskiwania hello jako danych wejściowych.</span><span class="sxs-lookup"><span data-stu-id="ac974-139">Many Azure Backup cmdlets require hello Recovery Services vault object as an input.</span></span> <span data-ttu-id="ac974-140">Z tego powodu jest wygodne toostore hello usług odzyskiwania kopii zapasowej magazynu obiekt w zmiennej.</span><span class="sxs-lookup"><span data-stu-id="ac974-140">For this reason, it is convenient toostore hello Backup Recovery Services vault object in a variable.</span></span>
   >
   >

## <a name="view-hello-vaults-in-a-subscription"></a><span data-ttu-id="ac974-141">Widok hello magazynów w ramach subskrypcji</span><span class="sxs-lookup"><span data-stu-id="ac974-141">View hello vaults in a subscription</span></span>
<span data-ttu-id="ac974-142">Użyj  **[Get-AzureRmRecoveryServicesVault](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices/get-azurermrecoveryservicesvault)**  tooview hello listę wszystkich magazynów w hello bieżącej subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="ac974-142">Use **[Get-AzureRmRecoveryServicesVault](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices/get-azurermrecoveryservicesvault)** tooview hello list of all vaults in hello current subscription.</span></span> <span data-ttu-id="ac974-143">Można użyć tego polecenia toocheck, czy utworzono nowy magazyn, lub toosee hello dostępnych magazynów w subskrypcji hello.</span><span class="sxs-lookup"><span data-stu-id="ac974-143">You can use this command toocheck that a new vault was created, or toosee hello available vaults in hello subscription.</span></span>

<span data-ttu-id="ac974-144">Uruchom polecenie hello, Get-AzureRmRecoveryServicesVault tooview wszystkie magazyny hello subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="ac974-144">Run hello command, Get-AzureRmRecoveryServicesVault, tooview all vaults in hello subscription.</span></span> <span data-ttu-id="ac974-145">Witaj poniższy przykład przedstawia hello informacje wyświetlane dla każdego magazynu.</span><span class="sxs-lookup"><span data-stu-id="ac974-145">hello following example shows hello information displayed for each vault.</span></span>

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


## <a name="back-up-azure-vms"></a><span data-ttu-id="ac974-146">Tworzenie kopii zapasowych maszyn wirtualnych platformy Azure</span><span class="sxs-lookup"><span data-stu-id="ac974-146">Back up Azure VMs</span></span>
<span data-ttu-id="ac974-147">Użyj tooprotect magazyn usług odzyskiwania maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="ac974-147">Use a Recovery Services vault tooprotect your virtual machines.</span></span> <span data-ttu-id="ac974-148">Przed zastosowaniem ochrona powitalnych Ustaw kontekst magazynu hello (hello typ danych chronionych w magazynie hello), a następnie sprawdź hello zasad ochrony.</span><span class="sxs-lookup"><span data-stu-id="ac974-148">Before you apply hello protection, set hello vault context (hello type of data protected in hello vault), and verify hello protection policy.</span></span> <span data-ttu-id="ac974-149">zasady ochrony Hello jest harmonogram hello uruchomienie zadania tworzenia kopii zapasowej hello i jak długo są przechowywane każdego migawki kopii zapasowej.</span><span class="sxs-lookup"><span data-stu-id="ac974-149">hello protection policy is hello schedule when hello backup jobs run, and how long each backup snapshot is retained.</span></span>

### <a name="set-vault-context"></a><span data-ttu-id="ac974-150">Ustaw kontekst magazynu</span><span class="sxs-lookup"><span data-stu-id="ac974-150">Set vault context</span></span>
<span data-ttu-id="ac974-151">Przed ponownym włączeniem ochrony na maszynie Wirtualnej, użyj  **[AzureRmRecoveryServicesVaultContext zestaw](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices/set-azurermrecoveryservicesvaultcontext)**  tooset hello magazynu kontekstu.</span><span class="sxs-lookup"><span data-stu-id="ac974-151">Before enabling protection on a VM, use **[Set-AzureRmRecoveryServicesVaultContext](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices/set-azurermrecoveryservicesvaultcontext)** tooset hello vault context.</span></span> <span data-ttu-id="ac974-152">Po ustawieniu kontekst magazynu hello stosuje tooall kolejne polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="ac974-152">Once hello vault context is set, it applies tooall subsequent cmdlets.</span></span> <span data-ttu-id="ac974-153">Witaj poniższy przykład przedstawia hello magazynu kontekst dla magazynu hello *testvault*.</span><span class="sxs-lookup"><span data-stu-id="ac974-153">hello following example sets hello vault context for hello vault, *testvault*.</span></span>

```
PS C:\> Get-AzureRmRecoveryServicesVault -Name "testvault" | Set-AzureRmRecoveryServicesVaultContext
```

### <a name="create-a-protection-policy"></a><span data-ttu-id="ac974-154">Tworzenie zasad ochrony</span><span class="sxs-lookup"><span data-stu-id="ac974-154">Create a protection policy</span></span>
<span data-ttu-id="ac974-155">Podczas tworzenia magazynu usług odzyskiwania jest dostarczany z domyślną ochronę i zasady przechowywania.</span><span class="sxs-lookup"><span data-stu-id="ac974-155">When you create a Recovery Services vault, it comes with default protection and retention policies.</span></span> <span data-ttu-id="ac974-156">Witaj domyślne zasady ochrony wyzwala zadanie tworzenia kopii zapasowej każdego dnia o określonej godzinie.</span><span class="sxs-lookup"><span data-stu-id="ac974-156">hello default protection policy triggers a backup job each day at a specified time.</span></span> <span data-ttu-id="ac974-157">zasady przechowywania domyślne Hello zachowuje punkt odzyskiwania codziennie hello przez 30 dni.</span><span class="sxs-lookup"><span data-stu-id="ac974-157">hello default retention policy retains hello daily recovery point for 30 days.</span></span> <span data-ttu-id="ac974-158">Można używać domyślnych hello tooquickly zasad ochrony maszyny Wirtualnej i edytować zasady hello później przy użyciu różnych szczegółów.</span><span class="sxs-lookup"><span data-stu-id="ac974-158">You can use hello default policy tooquickly protect your VM and edit hello policy later with different details.</span></span>

<span data-ttu-id="ac974-159">Użyj  **[Get-AzureRmRecoveryServicesBackupProtectionPolicy](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/get-azurermrecoveryservicesbackupprotectionpolicy)**  tooview zasady ochrony hello w magazynie hello.</span><span class="sxs-lookup"><span data-stu-id="ac974-159">Use **[Get-AzureRmRecoveryServicesBackupProtectionPolicy](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/get-azurermrecoveryservicesbackupprotectionpolicy)** tooview hello protection policies in hello vault.</span></span> <span data-ttu-id="ac974-160">Tooget tego polecenia cmdlet można użyć określonych zasad lub tooview hello zasady skojarzone z typem obciążenia.</span><span class="sxs-lookup"><span data-stu-id="ac974-160">You can use this cmdlet tooget a specific policy, or tooview hello policies associated with a workload type.</span></span> <span data-ttu-id="ac974-161">Poniższy przykład Hello pobiera zasady dla obciążeń typu AzureVM.</span><span class="sxs-lookup"><span data-stu-id="ac974-161">hello following example gets policies for workload type, AzureVM.</span></span>

```
PS C:\> Get-AzureRmRecoveryServicesBackupProtectionPolicy -WorkloadType "AzureVM"
Name                 WorkloadType       BackupManagementType BackupTime                DaysOfWeek
----                 ------------       -------------------- ----------                ----------
DefaultPolicy        AzureVM            AzureVM              4/14/2016 5:00:00 PM
```

> [!NOTE]
> <span data-ttu-id="ac974-162">Strefa czasowa Hello hello BackupTime pola w programie PowerShell jest czasem UTC.</span><span class="sxs-lookup"><span data-stu-id="ac974-162">hello timezone of hello BackupTime field in PowerShell is UTC.</span></span> <span data-ttu-id="ac974-163">Jednak podczas wykonywania kopii zapasowej hello jest wyświetlany w hello portalu Azure, czas hello jest skorygowaną tooyour lokalną strefę czasową.</span><span class="sxs-lookup"><span data-stu-id="ac974-163">However, when hello backup time is shown in hello Azure portal, hello time is adjusted tooyour local timezone.</span></span>
>
>

<span data-ttu-id="ac974-164">Zasady tworzenia kopii zapasowej ochrony jest skojarzony z co najmniej jedne zasady przechowywania.</span><span class="sxs-lookup"><span data-stu-id="ac974-164">A backup protection policy is associated with at least one retention policy.</span></span> <span data-ttu-id="ac974-165">Zasady przechowywania określają, jak długo punkt odzyskiwania jest przechowywana, przed usunięciem.</span><span class="sxs-lookup"><span data-stu-id="ac974-165">Retention policy defines how long a recovery point is kept before it is deleted.</span></span> <span data-ttu-id="ac974-166">Użyj  **[Get-AzureRmRecoveryServicesBackupRetentionPolicyObject](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/get-azurermrecoveryservicesbackupretentionpolicyobject)**  tooview hello domyślne zachowanie zasady.</span><span class="sxs-lookup"><span data-stu-id="ac974-166">Use **[Get-AzureRmRecoveryServicesBackupRetentionPolicyObject](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/get-azurermrecoveryservicesbackupretentionpolicyobject)** tooview hello default retention policy.</span></span>  <span data-ttu-id="ac974-167">Podobnie można użyć  **[Get-AzureRmRecoveryServicesBackupSchedulePolicyObject](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/get-azurermrecoveryservicesbackupschedulepolicyobject)**  tooobtain hello domyślny harmonogram zasad.</span><span class="sxs-lookup"><span data-stu-id="ac974-167">Similarly you can use **[Get-AzureRmRecoveryServicesBackupSchedulePolicyObject](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/get-azurermrecoveryservicesbackupschedulepolicyobject)** tooobtain hello default schedule policy.</span></span> <span data-ttu-id="ac974-168">Witaj  **[AzureRmRecoveryServicesBackupProtectionPolicy nowy](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/new-azurermrecoveryservicesbackupprotectionpolicy)**  polecenie cmdlet tworzy obiekt programu PowerShell, która przechowuje informacje o zasadach tworzenia kopii zapasowej.</span><span class="sxs-lookup"><span data-stu-id="ac974-168">hello **[New-AzureRmRecoveryServicesBackupProtectionPolicy](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/new-azurermrecoveryservicesbackupprotectionpolicy)** cmdlet creates a PowerShell object that holds backup policy information.</span></span> <span data-ttu-id="ac974-169">Witaj harmonogram i przechowywania obiektów zasady są używane jako danych wejściowych toohello  **[AzureRmRecoveryServicesBackupProtectionPolicy nowy](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/new-azurermrecoveryservicesbackupprotectionpolicy)**  polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="ac974-169">hello schedule and retention policy objects are used as inputs toohello **[New-AzureRmRecoveryServicesBackupProtectionPolicy](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/new-azurermrecoveryservicesbackupprotectionpolicy)** cmdlet.</span></span> <span data-ttu-id="ac974-170">Witaj poniższy przykład przechowuje hello harmonogram zasad i zasady przechowywania hello w zmiennych.</span><span class="sxs-lookup"><span data-stu-id="ac974-170">hello following example stores hello schedule policy and hello retention policy in variables.</span></span> <span data-ttu-id="ac974-171">przykład Witaj używa tych zmiennych toodefine hello parametrów podczas tworzenia zasad ochrony, *NewPolicy*.</span><span class="sxs-lookup"><span data-stu-id="ac974-171">hello example uses those variables toodefine hello parameters when creating a protection policy, *NewPolicy*.</span></span>

```
PS C:\> $schPol = Get-AzureRmRecoveryServicesBackupSchedulePolicyObject -WorkloadType "AzureVM"
PS C:\> $retPol = Get-AzureRmRecoveryServicesBackupRetentionPolicyObject -WorkloadType "AzureVM"
PS C:\> New-AzureRmRecoveryServicesBackupProtectionPolicy -Name "NewPolicy" -WorkloadType "AzureVM" -RetentionPolicy $retPol -SchedulePolicy $schPol
Name                 WorkloadType       BackupManagementType BackupTime                DaysOfWeek
----                 ------------       -------------------- ----------                ----------
NewPolicy           AzureVM            AzureVM              4/24/2016 1:30:00 AM
```


### <a name="enable-protection"></a><span data-ttu-id="ac974-172">Włączanie ochrony</span><span class="sxs-lookup"><span data-stu-id="ac974-172">Enable protection</span></span>
<span data-ttu-id="ac974-173">Po zdefiniowaniu zasad tworzenia kopii zapasowej ochrony hello nadal należy włączyć hello zasad dla elementu.</span><span class="sxs-lookup"><span data-stu-id="ac974-173">Once you have defined hello backup protection policy, you still must enable hello policy for an item.</span></span> <span data-ttu-id="ac974-174">Użyj  **[AzureRmRecoveryServicesBackupProtection Włącz](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/enable-azurermrecoveryservicesbackupprotection)**  tooenable ochrony.</span><span class="sxs-lookup"><span data-stu-id="ac974-174">Use **[Enable-AzureRmRecoveryServicesBackupProtection](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/enable-azurermrecoveryservicesbackupprotection)** tooenable protection.</span></span> <span data-ttu-id="ac974-175">Włączenie ochrony wymaga dwóch obiektów - element hello i hello zasad.</span><span class="sxs-lookup"><span data-stu-id="ac974-175">Enabling protection requires two objects - hello item and hello policy.</span></span> <span data-ttu-id="ac974-176">Gdy zasady hello został skojarzony z magazynem hello, hello kopii zapasowej przepływ pracy zostanie wyzwolony w czasie hello zdefiniowane w hello harmonogram zasad.</span><span class="sxs-lookup"><span data-stu-id="ac974-176">Once hello policy has been associated with hello vault, hello backup workflow is triggered at hello time defined in hello policy schedule.</span></span>

<span data-ttu-id="ac974-177">następujące przykładowe umożliwia ochronę hello elementu, V2VM, za pomocą zasad hello, NewPolicy Hello.</span><span class="sxs-lookup"><span data-stu-id="ac974-177">hello following example enables protection for hello item, V2VM, using hello policy, NewPolicy.</span></span> <span data-ttu-id="ac974-178">ochronę hello tooenable niezaszyfrowane maszyn wirtualnych Menedżera zasobów</span><span class="sxs-lookup"><span data-stu-id="ac974-178">tooenable hello protection on non-encrypted Resource Manager VMs</span></span>

```
PS C:\> $pol=Get-AzureRmRecoveryServicesBackupProtectionPolicy -Name "NewPolicy"
PS C:\> Enable-AzureRmRecoveryServicesBackupProtection -Policy $pol -Name "V2VM" -ResourceGroupName "RGName1"
```

<span data-ttu-id="ac974-179">Ochrona powitalnych tooenable na szyfrowany maszyn wirtualnych (szyfrowane przy użyciu BEK i KEK), toogive hello kopia zapasowa Azure usługa uprawnienia tooread kluczy i kluczy tajnych w magazynie kluczy.</span><span class="sxs-lookup"><span data-stu-id="ac974-179">tooenable hello protection on encrypted VMs (encrypted using BEK and KEK), you need toogive hello Azure Backup service permission tooread keys and secrets from key vault.</span></span>

```
PS C:\> Set-AzureRmKeyVaultAccessPolicy -VaultName "KeyVaultName" -ResourceGroupName "RGNameOfKeyVault" -PermissionsToKeys backup,get,list -PermissionsToSecrets get,list -ServicePrincipalName 262044b1-e2ce-469f-a196-69ab7ada62d3
PS C:\> $pol=Get-AzureRmRecoveryServicesBackupProtectionPolicy -Name "NewPolicy"
PS C:\> Enable-AzureRmRecoveryServicesBackupProtection -Policy $pol -Name "V2VM" -ResourceGroupName "RGName1"
```

<span data-ttu-id="ac974-180">Ochrona powitalnych tooenable na szyfrowany maszyn wirtualnych (szyfrowane tylko przy użyciu BEK), toogive hello kopia zapasowa Azure usługi uprawnienia tooread kluczy tajnych w magazynie kluczy.</span><span class="sxs-lookup"><span data-stu-id="ac974-180">tooenable hello protection on encrypted VMs (encrypted using BEK only), you need toogive hello Azure Backup service permission tooread secrets from key vault.</span></span>

```
PS C:\> Set-AzureRmKeyVaultAccessPolicy -VaultName "KeyVaultName" -ResourceGroupName "RGNameOfKeyVault" -PermissionsToSecrets backup,get,list -ServicePrincipalName 262044b1-e2ce-469f-a196-69ab7ada62d3
PS C:\> $pol=Get-AzureRmRecoveryServicesBackupProtectionPolicy -Name "NewPolicy"
PS C:\> Enable-AzureRmRecoveryServicesBackupProtection -Policy $pol -Name "V2VM" -ResourceGroupName "RGName1"
```

> [!NOTE]
> <span data-ttu-id="ac974-181">Jeśli korzystasz z chmury Azure dla instytucji rządowych hello, użyj hello ff281ffe-705c-4f53-9f37-a40e6f2c68f3 wartość dla parametru hello **- ServicePrincipalName** w [Set-AzureRmKeyVaultAccessPolicy](https://docs.microsoft.com/powershell/module/azurerm.keyvault/set-azurermkeyvaultaccesspolicy) polecenia cmdlet .</span><span class="sxs-lookup"><span data-stu-id="ac974-181">If you are using hello Azure Government cloud, then use hello value ff281ffe-705c-4f53-9f37-a40e6f2c68f3 for hello parameter **-ServicePrincipalName** in [Set-AzureRmKeyVaultAccessPolicy](https://docs.microsoft.com/powershell/module/azurerm.keyvault/set-azurermkeyvaultaccesspolicy) cmdlet.</span></span>
>
>

<span data-ttu-id="ac974-182">Klasycznych maszyn wirtualnych</span><span class="sxs-lookup"><span data-stu-id="ac974-182">For classic VMs</span></span>

```
PS C:\> $pol=Get-AzureRmRecoveryServicesBackupProtectionPolicy -Name "NewPolicy"
PS C:\> Enable-AzureRmRecoveryServicesBackupProtection -Policy $pol -Name "V1VM" -ServiceName "ServiceName1"
```

### <a name="modify-a-protection-policy"></a><span data-ttu-id="ac974-183">Modyfikowanie zasad ochrony</span><span class="sxs-lookup"><span data-stu-id="ac974-183">Modify a protection policy</span></span>
<span data-ttu-id="ac974-184">zasady ochrony hello toomodify, użyj [AzureRmRecoveryServicesBackupProtectionPolicy zestaw](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/set-azurermrecoveryservicesbackupprotectionpolicy) toomodify hello SchedulePolicy lub RetentionPolicy obiektów.</span><span class="sxs-lookup"><span data-stu-id="ac974-184">toomodify hello protection policy, use [Set-AzureRmRecoveryServicesBackupProtectionPolicy](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/set-azurermrecoveryservicesbackupprotectionpolicy) toomodify hello SchedulePolicy or RetentionPolicy objects.</span></span>

<span data-ttu-id="ac974-185">Witaj poniższy przykład umożliwia zmianę hello odzyskiwania punktu przechowywania too365 dni.</span><span class="sxs-lookup"><span data-stu-id="ac974-185">hello following example changes hello recovery point retention too365 days.</span></span>

```
PS C:\> $retPol = Get-AzureRmRecoveryServicesBackupRetentionPolicyObject -WorkloadType "AzureVM"
PS C:\> $retPol.DailySchedule.DurationCountInDays = 365
PS C:\> $pol= Get-AzureRmRecoveryServicesBackupProtectionPolicy -Name "NewPolicy"
PS C:\> Set-AzureRmRecoveryServicesBackupProtectionPolicy -Policy $pol  -RetentionPolicy $RetPol
```

## <a name="trigger-a-backup"></a><span data-ttu-id="ac974-186">Wyzwalacz kopią zapasową</span><span class="sxs-lookup"><span data-stu-id="ac974-186">Trigger a backup</span></span>
<span data-ttu-id="ac974-187">Można użyć  **[AzureRmRecoveryServicesBackupItem kopii zapasowej](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/backup-azurermrecoveryservicesbackupitem)**  tootrigger zadania tworzenia kopii zapasowej.</span><span class="sxs-lookup"><span data-stu-id="ac974-187">You can use **[Backup-AzureRmRecoveryServicesBackupItem](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/backup-azurermrecoveryservicesbackupitem)** tootrigger a backup job.</span></span> <span data-ttu-id="ac974-188">Jeśli jest hello początkowa kopia zapasowa jest pełnej kopii zapasowej.</span><span class="sxs-lookup"><span data-stu-id="ac974-188">If it is hello initial backup, it is a full backup.</span></span> <span data-ttu-id="ac974-189">Tworzenie kolejnych kopii zapasowych zająć przyrostowej kopii.</span><span class="sxs-lookup"><span data-stu-id="ac974-189">Subsequent backups take an incremental copy.</span></span> <span data-ttu-id="ac974-190">Należy się toouse  **[AzureRmRecoveryServicesVaultContext zestaw](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices/set-azurermrecoveryservicesvaultcontext)**  kontekst magazynu hello tooset przed wyzwalania hello zadanie tworzenia kopii zapasowej.</span><span class="sxs-lookup"><span data-stu-id="ac974-190">Be sure toouse **[Set-AzureRmRecoveryServicesVaultContext](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices/set-azurermrecoveryservicesvaultcontext)** tooset hello vault context before triggering hello backup job.</span></span> <span data-ttu-id="ac974-191">Poniższy przykład Hello przyjęto założenie, że magazyn kontekst został ustawiony.</span><span class="sxs-lookup"><span data-stu-id="ac974-191">hello following example assumes vault context was set.</span></span>

```
PS C:\> $namedContainer = Get-AzureRmRecoveryServicesBackupContainer -ContainerType "AzureVM" -Status "Registered" -FriendlyName "V2VM"
PS C:\> $item = Get-AzureRmRecoveryServicesBackupItem -Container $namedContainer -WorkloadType "AzureVM"
PS C:\> $job = Backup-AzureRmRecoveryServicesBackupItem -Item $item
WorkloadName     Operation            Status               StartTime                 EndTime                   JobID
------------     ---------            ------               ---------                 -------                   ----------
V2VM              Backup               InProgress            4/23/2016 5:00:30 PM                       cf4b3ef5-2fac-4c8e-a215-d2eba4124f27
```

> [!NOTE]
> <span data-ttu-id="ac974-192">Strefa czasowa Hello hello wartości StartTime i EndTime pól w programie PowerShell jest czasem UTC.</span><span class="sxs-lookup"><span data-stu-id="ac974-192">hello timezone of hello StartTime and EndTime fields in PowerShell is UTC.</span></span> <span data-ttu-id="ac974-193">Jednak gdy czas hello jest wyświetlana w portalu Azure hello, czas hello jest dostosowaną tooyour lokalną strefę czasową.</span><span class="sxs-lookup"><span data-stu-id="ac974-193">However, when hello time is shown in hello Azure portal, hello time is adjusted tooyour local timezone.</span></span>
>
>

## <a name="monitoring-a-backup-job"></a><span data-ttu-id="ac974-194">Monitorowanie zadania tworzenia kopii zapasowej</span><span class="sxs-lookup"><span data-stu-id="ac974-194">Monitoring a backup job</span></span>
<span data-ttu-id="ac974-195">Można monitorować długotrwałe operacje, takie jak zadania tworzenia kopii zapasowej bez użycia hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="ac974-195">You can monitor long-running operations, such as backup jobs, without using hello Azure portal.</span></span> <span data-ttu-id="ac974-196">Stan hello tooget zadania w toku, użyj hello  **[Get-AzureRmRecoveryservicesBackupJob](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/get-azurermrecoveryservicesbackupjob)**  polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="ac974-196">tooget hello status of an in-progress job, use hello **[Get-AzureRmRecoveryservicesBackupJob](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/get-azurermrecoveryservicesbackupjob)** cmdlet.</span></span> <span data-ttu-id="ac974-197">To polecenie cmdlet pobiera hello zadania tworzenia kopii zapasowej dla określonego magazynu, a tego magazynu jest określona w kontekście magazynu hello.</span><span class="sxs-lookup"><span data-stu-id="ac974-197">This cmdlet gets hello backup jobs for a specific vault, and that vault is specified in hello vault context.</span></span> <span data-ttu-id="ac974-198">Hello poniższy przykład pobiera hello stan zadania w toku jako tablica i zapisuje stan hello w zmiennej hello $joblist.</span><span class="sxs-lookup"><span data-stu-id="ac974-198">hello following example gets hello status of an in-progress job as an array, and stores hello status in hello $joblist variable.</span></span>

```
PS C:\> $joblist = Get-AzureRmRecoveryservicesBackupJob –Status "InProgress"
PS C:\> $joblist[0]
WorkloadName     Operation            Status               StartTime                 EndTime                   JobID
------------     ---------            ------               ---------                 -------                   ----------
V2VM             Backup               InProgress            4/23/2016 5:00:30 PM           cf4b3ef5-2fac-4c8e-a215-d2eba4124f27
```

<span data-ttu-id="ac974-199">Zamiast sondowania te zadania na zakończenie — czyli niepotrzebnych dodatkowy kod - Użyj hello  **[AzureRmRecoveryServicesBackupJob oczekiwania](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/wait-azurermrecoveryservicesbackupjob)**  polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="ac974-199">Instead of polling these jobs for completion - which is unnecessary additional code - use hello **[Wait-AzureRmRecoveryServicesBackupJob](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/wait-azurermrecoveryservicesbackupjob)** cmdlet.</span></span> <span data-ttu-id="ac974-200">To polecenie cmdlet wstrzymuje wykonywanie hello dopóki hello określona wartość limitu czasu jest osiągana albo hello zadanie zostało ukończone.</span><span class="sxs-lookup"><span data-stu-id="ac974-200">This cmdlet pauses hello execution until either hello job completes or hello specified timeout value is reached.</span></span>

```
PS C:\> Wait-AzureRmRecoveryServicesBackupJob -Job $joblist[0] -Timeout 43200
```

## <a name="restore-an-azure-vm"></a><span data-ttu-id="ac974-201">Przywracanie maszyny Wirtualnej platformy Azure</span><span class="sxs-lookup"><span data-stu-id="ac974-201">Restore an Azure VM</span></span>
<span data-ttu-id="ac974-202">Ma klucza różnicy między hello przywracanie maszyny Wirtualnej przy użyciu hello portalu Azure i przywracanie maszyny Wirtualnej przy użyciu programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="ac974-202">There is a key difference between hello restoring a VM using hello Azure portal and restoring a VM using PowerShell.</span></span> <span data-ttu-id="ac974-203">Przy użyciu programu PowerShell operacja przywracania hello została zakończona, po utworzeniu hello dyski i informacje o konfiguracji z hello punkt odzyskiwania.</span><span class="sxs-lookup"><span data-stu-id="ac974-203">With PowerShell, hello restore operation is complete once hello disks and configuration information from hello recovery point are created.</span></span>

> [!NOTE]
> <span data-ttu-id="ac974-204">Operacja przywracania Hello nie powoduje utworzenia maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="ac974-204">hello restore operation does not create a virtual machine.</span></span>
>
>

<span data-ttu-id="ac974-205">toocreate maszyny wirtualnej z dysku, zobacz sekcję hello [hello tworzenie maszyny Wirtualnej z przechowywanych dysków](backup-azure-vms-automation.md#create-a-vm-from-stored-disks).</span><span class="sxs-lookup"><span data-stu-id="ac974-205">toocreate a virtual machine from disk, see hello section, [Create hello VM from stored disks](backup-azure-vms-automation.md#create-a-vm-from-stored-disks).</span></span> <span data-ttu-id="ac974-206">Witaj podstawowe kroki toorestore maszyny Wirtualnej platformy Azure są:</span><span class="sxs-lookup"><span data-stu-id="ac974-206">hello basic steps toorestore an Azure VM are:</span></span>

* <span data-ttu-id="ac974-207">Wybierz hello maszyny Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="ac974-207">Select hello VM</span></span>
* <span data-ttu-id="ac974-208">Wybierz punkt odzyskiwania</span><span class="sxs-lookup"><span data-stu-id="ac974-208">Choose a recovery point</span></span>
* <span data-ttu-id="ac974-209">Przywróć hello dysków</span><span class="sxs-lookup"><span data-stu-id="ac974-209">Restore hello disks</span></span>
* <span data-ttu-id="ac974-210">Utwórz hello maszyny Wirtualnej z przechowywanych dysków</span><span class="sxs-lookup"><span data-stu-id="ac974-210">Create hello VM from stored disks</span></span>

<span data-ttu-id="ac974-211">Witaj poniższy rysunek przedstawia hierarchię obiektów hello z hello RecoveryServicesVault toohello BackupRecoveryPoint w dół.</span><span class="sxs-lookup"><span data-stu-id="ac974-211">hello following graphic shows hello object hierarchy from hello RecoveryServicesVault down toohello BackupRecoveryPoint.</span></span>

![Hierarchia obiektów usług odzyskiwania przedstawiający BackupContainer](./media/backup-azure-vms-arm-automation/backuprecoverypoint-only.png)

<span data-ttu-id="ac974-213">toorestore dane kopii zapasowej, zidentyfikuj hello elementu kopii zapasowej i hello punkt odzyskiwania, która przechowuje dane w momencie hello.</span><span class="sxs-lookup"><span data-stu-id="ac974-213">toorestore backup data, identify hello backed-up item and hello recovery point that holds hello point-in-time data.</span></span> <span data-ttu-id="ac974-214">Użyj hello  **[AzureRmRecoveryServicesBackupItem przywracania](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/restore-azurermrecoveryservicesbackupitem)**  danych toorestore polecenia cmdlet z hello magazynu toohello odbiorcy.</span><span class="sxs-lookup"><span data-stu-id="ac974-214">Use hello **[Restore-AzureRmRecoveryServicesBackupItem](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/restore-azurermrecoveryservicesbackupitem)** cmdlet toorestore data from hello vault toohello customer's account.</span></span>

### <a name="select-hello-vm"></a><span data-ttu-id="ac974-215">Wybierz hello maszyny Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="ac974-215">Select hello VM</span></span>
<span data-ttu-id="ac974-216">tooget hello środowiska PowerShell obiektu, który identyfikuje hello prawo kopii zapasowej elementu, Rozpocznij od hello kontenera w magazynie hello i przechodzić w dół hierarchii obiektów hello.</span><span class="sxs-lookup"><span data-stu-id="ac974-216">tooget hello PowerShell object that identifies hello right backup item, start from hello container in hello vault, and work your way down hello object hierarchy.</span></span> <span data-ttu-id="ac974-217">tooselect hello kontener, który reprezentuje hello maszyny Wirtualnej, użyj hello  **[Get-AzureRmRecoveryServicesBackupContainer](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/get-azurermrecoveryservicesbackupcontainer)**  polecenia cmdlet i przekazać w potoku tego toohello  **[ Get-AzureRmRecoveryServicesBackupItem](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/get-azurermrecoveryservicesbackupitem)**  polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="ac974-217">tooselect hello container that represents hello VM, use hello **[Get-AzureRmRecoveryServicesBackupContainer](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/get-azurermrecoveryservicesbackupcontainer)** cmdlet and pipe that toohello **[Get-AzureRmRecoveryServicesBackupItem](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/get-azurermrecoveryservicesbackupitem)** cmdlet.</span></span>

```
PS C:\> $namedContainer = Get-AzureRmRecoveryServicesBackupContainer  -ContainerType "AzureVM" –Status "Registered" -FriendlyName "V2VM"
PS C:\> $backupitem = Get-AzureRmRecoveryServicesBackupItem –Container $namedContainer  –WorkloadType "AzureVM"
```

### <a name="choose-a-recovery-point"></a><span data-ttu-id="ac974-218">Wybierz punkt odzyskiwania</span><span class="sxs-lookup"><span data-stu-id="ac974-218">Choose a recovery point</span></span>
<span data-ttu-id="ac974-219">Użyj hello  **[Get-AzureRmRecoveryServicesBackupRecoveryPoint](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/get-azurermrecoveryservicesbackuprecoverypoint)**  wszystkie punkty odzyskiwania dla kopii zapasowej elementu hello toolist polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="ac974-219">Use hello **[Get-AzureRmRecoveryServicesBackupRecoveryPoint](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/get-azurermrecoveryservicesbackuprecoverypoint)** cmdlet toolist all recovery points for hello backup item.</span></span> <span data-ttu-id="ac974-220">Następnie wybierz pozycję toorestore punktu odzyskiwania hello.</span><span class="sxs-lookup"><span data-stu-id="ac974-220">Then choose hello recovery point toorestore.</span></span> <span data-ttu-id="ac974-221">Jeśli nie wiesz, które toouse punkt odzyskiwania, jest toochoose dobrym rozwiązaniem hello najnowszych RecoveryPointType = punktu AppConsistent na liście hello.</span><span class="sxs-lookup"><span data-stu-id="ac974-221">If you are unsure which recovery point toouse, it is a good practice toochoose hello most recent RecoveryPointType = AppConsistent point in hello list.</span></span>

<span data-ttu-id="ac974-222">W hello następującego skryptu, hello zmiennej **$rp**, jest tablica punktów odzyskiwania dla hello wybrany element kopii zapasowej z hello ostatnich siedmiu dni.</span><span class="sxs-lookup"><span data-stu-id="ac974-222">In hello following script, hello variable, **$rp**, is an array of recovery points for hello selected backup item, from hello past seven days.</span></span> <span data-ttu-id="ac974-223">tablicy Hello jest sortowany w kolejności odwrotnej czasu z najnowszego punktu odzyskiwania hello pod indeksem 0.</span><span class="sxs-lookup"><span data-stu-id="ac974-223">hello array is sorted in reverse order of time with hello latest recovery point at index 0.</span></span> <span data-ttu-id="ac974-224">Użyj standardowych tablicy PowerShell indeksowania punkt odzyskiwania hello toopick.</span><span class="sxs-lookup"><span data-stu-id="ac974-224">Use standard PowerShell array indexing toopick hello recovery point.</span></span> <span data-ttu-id="ac974-225">Na przykład Witaj $rp [0] wybiera hello najnowszego punktu odzyskiwania.</span><span class="sxs-lookup"><span data-stu-id="ac974-225">In hello example, $rp[0] selects hello latest recovery point.</span></span>

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



### <a name="restore-hello-disks"></a><span data-ttu-id="ac974-226">Przywróć hello dysków</span><span class="sxs-lookup"><span data-stu-id="ac974-226">Restore hello disks</span></span>
<span data-ttu-id="ac974-227">Użyj hello  **[AzureRmRecoveryServicesBackupItem przywracania](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/restore-azurermrecoveryservicesbackupitem)**  toorestore polecenia cmdlet element kopii zapasowej danych i konfiguracji tooa punktu odzyskiwania.</span><span class="sxs-lookup"><span data-stu-id="ac974-227">Use hello **[Restore-AzureRmRecoveryServicesBackupItem](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/restore-azurermrecoveryservicesbackupitem)** cmdlet toorestore a backup item's data and configuration tooa recovery point.</span></span> <span data-ttu-id="ac974-228">Po zidentyfikowaniu punkt odzyskiwania, używać go jako wartość hello hello **- RecoveryPoint** parametru.</span><span class="sxs-lookup"><span data-stu-id="ac974-228">Once you have identified a recovery point, use it as hello value for hello **-RecoveryPoint** parameter.</span></span> <span data-ttu-id="ac974-229">W hello poprzedniej przykładowy kod **$rp [0]** został toouse punktu odzyskiwania hello.</span><span class="sxs-lookup"><span data-stu-id="ac974-229">In hello previous sample code, **$rp[0]** was hello recovery point toouse.</span></span> <span data-ttu-id="ac974-230">W powitania po przykładowy kod **$rp [0]** jest toouse punktu odzyskiwania hello przywracania dysku hello.</span><span class="sxs-lookup"><span data-stu-id="ac974-230">In hello following sample code, **$rp[0]** is hello recovery point toouse for restoring hello disk.</span></span>

<span data-ttu-id="ac974-231">toorestore hello informacje o dyskach i konfiguracji:</span><span class="sxs-lookup"><span data-stu-id="ac974-231">toorestore hello disks and configuration information:</span></span>

```
PS C:\> $restorejob = Restore-AzureRmRecoveryServicesBackupItem -RecoveryPoint $rp[0] -StorageAccountName "DestAccount" -StorageAccountResourceGroupName "DestRG"
PS C:\> $restorejob
WorkloadName     Operation          Status               StartTime                 EndTime            JobID
------------     ---------          ------               ---------                 -------          ----------
V2VM              Restore           InProgress           4/23/2016 5:00:30 PM                        cf4b3ef5-2fac-4c8e-a215-d2eba4124f27
```

<span data-ttu-id="ac974-232">Użyj hello  **[AzureRmRecoveryServicesBackupJob oczekiwania](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/wait-azurermrecoveryservicesbackupjob)**  toowait polecenia cmdlet dla toocomplete zadania przywracania hello.</span><span class="sxs-lookup"><span data-stu-id="ac974-232">Use hello **[Wait-AzureRmRecoveryServicesBackupJob](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/wait-azurermrecoveryservicesbackupjob)** cmdlet toowait for hello Restore job toocomplete.</span></span>

```
PS C:\> Wait-AzureRmRecoveryServicesBackupJob -Job $restorejob -Timeout 43200
```

<span data-ttu-id="ac974-233">Po zakończeniu zadania przywracania hello Użyj hello  **[Get-AzureRmRecoveryServicesBackupJobDetails](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/get-azurermrecoveryservicesbackupjobdetails)**  polecenia cmdlet tooget hello szczegóły hello operację przywracania.</span><span class="sxs-lookup"><span data-stu-id="ac974-233">Once hello Restore job has completed, use hello **[Get-AzureRmRecoveryServicesBackupJobDetails](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/get-azurermrecoveryservicesbackupjobdetails)** cmdlet tooget hello details of hello restore operation.</span></span> <span data-ttu-id="ac974-234">Witaj JobDetails właściwości ma hello informacje potrzebne toorebuild hello maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="ac974-234">hello JobDetails property has hello information needed toorebuild hello VM.</span></span>

```
PS C:\> $restorejob = Get-AzureRmRecoveryServicesBackupJob -Job $restorejob
PS C:\> $details = Get-AzureRmRecoveryServicesBackupJobDetails -Job $restorejob
```

<span data-ttu-id="ac974-235">Po przywróceniu dysków hello Przejdź toohello następnej sekcji toocreate hello maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="ac974-235">Once you restore hello disks, go toohello next section toocreate hello VM.</span></span>

## <a name="create-a-vm-from-restored-disks"></a><span data-ttu-id="ac974-236">Utwórz maszynę Wirtualną z przywróconą dysków</span><span class="sxs-lookup"><span data-stu-id="ac974-236">Create a VM from restored disks</span></span>
<span data-ttu-id="ac974-237">Po przywróceniu hello dysków, użyj toocreate te kroki i skonfiguruj hello maszyny wirtualnej z dysku.</span><span class="sxs-lookup"><span data-stu-id="ac974-237">After you have restored hello disks, use these steps toocreate and configure hello virtual machine from disk.</span></span>

> [!NOTE]
> <span data-ttu-id="ac974-238">toocreate szyfrowane maszyn wirtualnych z przywróconą dysków, roli użytkownika Azure musi mieć uprawnienie tooperform hello akcji, **Microsoft.KeyVault/vaults/deploy/action**.</span><span class="sxs-lookup"><span data-stu-id="ac974-238">toocreate encrypted VMs from restored disks, your Azure role must have permission tooperform hello action, **Microsoft.KeyVault/vaults/deploy/action**.</span></span> <span data-ttu-id="ac974-239">Jeśli rola użytkownika nie ma to uprawnienie, utworzyć niestandardową rolę za pomocą tej akcji.</span><span class="sxs-lookup"><span data-stu-id="ac974-239">If your role does not have this permission, create a custom role with this action.</span></span> <span data-ttu-id="ac974-240">Aby uzyskać więcej informacji, zobacz [niestandardowych ról w Azure RBAC](../active-directory/role-based-access-control-custom-roles.md).</span><span class="sxs-lookup"><span data-stu-id="ac974-240">For more information, see [Custom Roles in Azure RBAC](../active-directory/role-based-access-control-custom-roles.md).</span></span>
>
>

1. <span data-ttu-id="ac974-241">Zapytanie hello przywrócona właściwości dysku hello szczegóły zadania.</span><span class="sxs-lookup"><span data-stu-id="ac974-241">Query hello restored disk properties for hello job details.</span></span>

  ```
  PS C:\> $properties = $details.properties
  PS C:\> $storageAccountName = $properties["Target Storage Account Name"]
  PS C:\> $containerName = $properties["Config Blob Container Name"]
  PS C:\> $blobName = $properties["Config Blob Name"]
  ```

2. <span data-ttu-id="ac974-242">Ustaw kontekst magazynu Azure hello i przywrócenie pliku konfiguracji JSON hello.</span><span class="sxs-lookup"><span data-stu-id="ac974-242">Set hello Azure storage context and restore hello JSON configuration file.</span></span>

    ```
    PS C:\> Set-AzureRmCurrentStorageAccount -Name $storageaccountname -ResourceGroupName "testvault"
    PS C:\> $destination_path = "C:\vmconfig.json"
    PS C:\> Get-AzureStorageBlobContent -Container $containerName -Blob $blobName -Destination $destination_path
    PS C:\> $obj = ((Get-Content -Path $destination_path -Raw -Encoding Unicode)).TrimEnd([char]0x00) | ConvertFrom-Json
    ```

3. <span data-ttu-id="ac974-243">Użyj konfiguracji JSON hello plik konfiguracji maszyny Wirtualnej hello toocreate.</span><span class="sxs-lookup"><span data-stu-id="ac974-243">Use hello JSON configuration file toocreate hello VM configuration.</span></span>

    ```
   PS C:\> $vm = New-AzureRmVMConfig -VMSize $obj.'properties.hardwareProfile'.vmSize -VMName "testrestore"
    ```

4. <span data-ttu-id="ac974-244">Dołącz hello dysk systemu operacyjnego i dysków z danymi.</span><span class="sxs-lookup"><span data-stu-id="ac974-244">Attach hello OS disk and data disks.</span></span> <span data-ttu-id="ac974-245">W zależności od konfiguracji hello maszyn wirtualnych kliknij na powitania odpowiednie łącze tooview odpowiednich poleceń cmdlet:</span><span class="sxs-lookup"><span data-stu-id="ac974-245">Depending on hello configuration of your VMs, click on hello relevant link tooview respective cmdlets:</span></span> 
    - [<span data-ttu-id="ac974-246">Które nie są zarządzane, niezaszyfrowane maszyny wirtualne</span><span class="sxs-lookup"><span data-stu-id="ac974-246">Non-managed, non-encrypted VMs</span></span>](#non-managed-non-encrypted-vms)
    - [<span data-ttu-id="ac974-247">Zaszyfrowane, które nie są zarządzane maszyn wirtualnych (tylko BEK)</span><span class="sxs-lookup"><span data-stu-id="ac974-247">Non-managed, encrypted VMs (BEK only)</span></span>](#non-managed-encrypted-vms-bek-only)
    - [<span data-ttu-id="ac974-248">Maszyny wirtualne zaszyfrowane, które nie są zarządzane (BEK i KEK)</span><span class="sxs-lookup"><span data-stu-id="ac974-248">Non-managed, encrypted VMs (BEK and KEK)</span></span>](#non-managed-encrypted-vms-bek-and-kek)
    - [<span data-ttu-id="ac974-249">Zarządzane niezaszyfrowane maszyny wirtualne</span><span class="sxs-lookup"><span data-stu-id="ac974-249">Managed, non-encrypted VMs</span></span>](#managed-non-encrypted-vms)
    - [<span data-ttu-id="ac974-250">Zarządzane, zaszyfrowanych maszyn wirtualnych (BEK i KEK)</span><span class="sxs-lookup"><span data-stu-id="ac974-250">Managed, encrypted VMs (BEK and KEK)</span></span>](#managed-encrypted-vms-bek-and-kek)
    
    #### <a name="non-managed-non-encrypted-vms"></a><span data-ttu-id="ac974-251">Które nie są zarządzane, niezaszyfrowane maszyny wirtualne</span><span class="sxs-lookup"><span data-stu-id="ac974-251">Non-managed, non-encrypted VMs</span></span>

    <span data-ttu-id="ac974-252">Użyj hello następujące przykładowe niezarządzanych, niezaszyfrowane maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="ac974-252">Use hello following sample for non-managed, non-encrypted VMs.</span></span>

    ```
    PS C:\> Set-AzureRmVMOSDisk -VM $vm -Name "osdisk" -VhdUri $obj.'properties.StorageProfile'.osDisk.vhd.Uri -CreateOption "Attach"
    PS C:\> $vm.StorageProfile.OsDisk.OsType = $obj.'properties.StorageProfile'.OsDisk.OsType
    PS C:\> foreach($dd in $obj.'properties.StorageProfile'.DataDisks)
    {
    $vm = Add-AzureRmVMDataDisk -VM $vm -Name "datadisk1" -VhdUri $dd.vhd.Uri -DiskSizeInGB 127 -Lun $dd.Lun -CreateOption "Attach"
    }
    ```

    #### <a name="non-managed-encrypted-vms-bek-only"></a><span data-ttu-id="ac974-253">Zaszyfrowane, które nie są zarządzane maszyn wirtualnych (tylko BEK)</span><span class="sxs-lookup"><span data-stu-id="ac974-253">Non-managed, encrypted VMs (BEK only)</span></span>

    <span data-ttu-id="ac974-254">Dla niezarządzanych, zaszyfrowane maszyn wirtualnych (szyfrowane tylko przy użyciu BEK) należy magazynu kluczy tajnych toohello hello toorestore przed dołączeniem dysków.</span><span class="sxs-lookup"><span data-stu-id="ac974-254">For non-managed, encrypted VMs (encrypted using BEK only), you need toorestore hello secret toohello key vault before you can attach disks.</span></span> <span data-ttu-id="ac974-255">Aby uzyskać więcej informacji, zobacz artykuł hello [przywrócić zaszyfrowanych maszyny wirtualnej z punktu odzyskiwania kopia zapasowa Azure](backup-azure-restore-key-secret.md).</span><span class="sxs-lookup"><span data-stu-id="ac974-255">For more information, please see hello article, [Restore an encrypted virtual machine from an Azure Backup recovery point](backup-azure-restore-key-secret.md).</span></span> <span data-ttu-id="ac974-256">następujące przykładowe Hello pokazuje, jak tooattach systemu operacyjnego i dysków z danymi dla szyfrowane maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="ac974-256">hello following sample shows how tooattach OS and data disks for encrypted VMs.</span></span>

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

    #### <a name="non-managed-encrypted-vms-bek-and-kek"></a><span data-ttu-id="ac974-257">Maszyny wirtualne zaszyfrowane, które nie są zarządzane (BEK i KEK)</span><span class="sxs-lookup"><span data-stu-id="ac974-257">Non-managed, encrypted VMs (BEK and KEK)</span></span>

    <span data-ttu-id="ac974-258">Dla niezarządzanych, zaszyfrowane maszyn wirtualnych (szyfrowane przy użyciu BEK i KEK) należy toorestore hello klucza i magazyn kluczy tajnych toohello przed dołączeniem dysków.</span><span class="sxs-lookup"><span data-stu-id="ac974-258">For non-managed, encrypted VMs (encrypted using BEK and KEK), you need toorestore hello key and secret toohello key vault before you can attach disks.</span></span> <span data-ttu-id="ac974-259">Aby uzyskać więcej informacji, zobacz artykuł hello [przywrócić zaszyfrowanych maszyny wirtualnej z punktu odzyskiwania kopia zapasowa Azure](backup-azure-restore-key-secret.md).</span><span class="sxs-lookup"><span data-stu-id="ac974-259">For more information, please see hello article, [Restore an encrypted virtual machine from an Azure Backup recovery point](backup-azure-restore-key-secret.md).</span></span> <span data-ttu-id="ac974-260">następujące przykładowe Hello pokazuje, jak tooattach systemu operacyjnego i dysków z danymi dla szyfrowane maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="ac974-260">hello following sample shows how tooattach OS and data disks for encrypted VMs.</span></span>

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

    #### <a name="managed-non-encrypted-vms"></a><span data-ttu-id="ac974-261">Zarządzane niezaszyfrowane maszyny wirtualne</span><span class="sxs-lookup"><span data-stu-id="ac974-261">Managed, non-encrypted VMs</span></span>

    <span data-ttu-id="ac974-262">Dla zarządzanych maszyn wirtualnych z systemem innym niż zaszyfrowane będzie konieczne toocreate zarządzane dysków z magazynu obiektów blob, a następnie dołącz hello dysków.</span><span class="sxs-lookup"><span data-stu-id="ac974-262">For managed non-encrypted VMs, you'll need toocreate managed disks from blob storage, and then attach hello disks.</span></span> <span data-ttu-id="ac974-263">Aby uzyskać szczegółowe informacje, zobacz artykuł hello [dołączyć tooa dysku danych maszyny Wirtualnej systemu Windows przy użyciu programu PowerShell](../virtual-machines/windows/attach-disk-ps.md).</span><span class="sxs-lookup"><span data-stu-id="ac974-263">For in-depth information, see hello article, [Attach a data disk tooa Windows VM using PowerShell](../virtual-machines/windows/attach-disk-ps.md).</span></span> <span data-ttu-id="ac974-264">powitania po przykładowy kod pokazuje, jak tooattach hello dysków z danymi dla zarządzanych niezaszyfrowane maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="ac974-264">hello following sample code shows how tooattach hello data disks for managed non-encrypted VMs.</span></span>

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

    #### <a name="managed-encrypted-vms-bek-and-kek"></a><span data-ttu-id="ac974-265">Zarządzane, zaszyfrowanych maszyn wirtualnych (BEK i KEK)</span><span class="sxs-lookup"><span data-stu-id="ac974-265">Managed, encrypted VMs (BEK and KEK)</span></span>

    <span data-ttu-id="ac974-266">Dla zarządzanych zaszyfrowanych maszyn wirtualnych (szyfrowane przy użyciu BEK i KEK) będzie konieczne toocreate zarządzane dysków z magazynu obiektów blob, a następnie dołącz hello dysków.</span><span class="sxs-lookup"><span data-stu-id="ac974-266">For managed encrypted VMs (encrypted using BEK and KEK), you'll need toocreate managed disks from blob storage, and then attach hello disks.</span></span> <span data-ttu-id="ac974-267">Aby uzyskać szczegółowe informacje, zobacz artykuł hello [dołączyć tooa dysku danych maszyny Wirtualnej systemu Windows przy użyciu programu PowerShell](../virtual-machines/windows/attach-disk-ps.md).</span><span class="sxs-lookup"><span data-stu-id="ac974-267">For in-depth information, see hello article, [Attach a data disk tooa Windows VM using PowerShell](../virtual-machines/windows/attach-disk-ps.md).</span></span> <span data-ttu-id="ac974-268">Witaj następujący przykładowy kod przedstawia sposób tooattach hello dysków z danymi dla zarządzanych zaszyfrowanych maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="ac974-268">hello following sample code shows how tooattach hello data disks for managed encrypted VMs.</span></span>

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

5. <span data-ttu-id="ac974-269">Określ ustawienia sieciowe hello.</span><span class="sxs-lookup"><span data-stu-id="ac974-269">Set hello Network settings.</span></span>

    ```
    PS C:\> $nicName="p1234"
    PS C:\> $pip = New-AzureRmPublicIpAddress -Name $nicName -ResourceGroupName "test" -Location "WestUS" -AllocationMethod Dynamic
    PS C:\> $vnet = Get-AzureRmVirtualNetwork -Name "testvNET" -ResourceGroupName "test"
    PS C:\> $nic = New-AzureRmNetworkInterface -Name $nicName -ResourceGroupName "test" -Location "WestUS" -SubnetId $vnet.Subnets[$subnetindex].Id -PublicIpAddressId $pip.Id
    PS C:\> $vm=Add-AzureRmVMNetworkInterface -VM $vm -Id $nic.Id
    ```
6. <span data-ttu-id="ac974-270">Utwórz maszynę wirtualną hello.</span><span class="sxs-lookup"><span data-stu-id="ac974-270">Create hello virtual machine.</span></span>

    ```    
    PS C:\> New-AzureRmVM -ResourceGroupName "test" -Location "WestUS" -VM $vm
    ```

## <a name="next-steps"></a><span data-ttu-id="ac974-271">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="ac974-271">Next steps</span></span>
<span data-ttu-id="ac974-272">Jeśli wolisz toouse tooengage programu PowerShell z zasobów platformy Azure, zobacz artykuł PowerShell hello, [wdrażanie i zarządzanie kopia zapasowa systemu Windows Server](backup-client-automation.md).</span><span class="sxs-lookup"><span data-stu-id="ac974-272">If you prefer toouse PowerShell tooengage with your Azure resources, see hello PowerShell article, [Deploy and Manage Backup for Windows Server](backup-client-automation.md).</span></span> <span data-ttu-id="ac974-273">Jeśli zarządzasz kopii zapasowych programu DPM, zobacz artykuł hello, [wdrażanie i zarządzanie kopii zapasowej programu DPM](backup-dpm-automation.md).</span><span class="sxs-lookup"><span data-stu-id="ac974-273">If you manage DPM backups, see hello article, [Deploy and Manage Backup for DPM](backup-dpm-automation.md).</span></span> <span data-ttu-id="ac974-274">Mieć obu tych artykułach wersji dla wdrożenia usługi Resource Manager oraz wdrożenia klasycznego.</span><span class="sxs-lookup"><span data-stu-id="ac974-274">Both of these articles have a version for Resource Manager deployments and Classic deployments.</span></span>  
