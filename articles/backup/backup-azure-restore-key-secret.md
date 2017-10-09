---
title: "maszyny wirtualne przy użyciu usługi Kopia zapasowa Azure szyfrowania klucza Key Vault aaaRestore i klucz tajny dla | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toorestore klucza magazynu kluczy i klucz tajny w kopii zapasowej Azure przy użyciu programu PowerShell"
services: backup
documentationcenter: 
author: JPallavi
manager: vijayts
editor: 
ms.assetid: 45214083-d5fc-4eb3-a367-0239dc59e0f6
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/28/2017
ms.author: pajosh
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 659b2f647493ffcc9494caee111c8bd584ef9c7f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="restore-key-vault-key-and-secret-for-encrypted-vms-using-azure-backup"></a><span data-ttu-id="5bd18-103">Przywróć klucz magazynu kluczy oraz klucz tajny dla zaszyfrowanych maszyn wirtualnych za pomocą usługi Kopia zapasowa Azure</span><span class="sxs-lookup"><span data-stu-id="5bd18-103">Restore Key Vault key and secret for encrypted VMs using Azure Backup</span></span>
<span data-ttu-id="5bd18-104">Ten artykuł zawiera informacje o przy użyciu kopii zapasowej maszyny Wirtualnej Azure tooperform przywracanie zaszyfrowanych maszynach wirtualnych platformy Azure, jeśli klucz, a klucz tajny nie istnieją w magazynie kluczy hello.</span><span class="sxs-lookup"><span data-stu-id="5bd18-104">This article talks about using Azure VM Backup tooperform restore of encrypted Azure VMs, if your key and secret do not exist in hello key vault.</span></span> <span data-ttu-id="5bd18-105">Te kroki można także toomaintain osobną kopię klucza (klucz szyfrowania klucza) i klucz tajny (klucza szyfrowania funkcją BitLocker) dla hello przywrócić maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="5bd18-105">These steps can also be used if you want toomaintain a separate copy of key (Key Encryption Key) and secret (BitLocker Encryption Key) for hello restored VM.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5bd18-106">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="5bd18-106">Prerequisites</span></span>
* <span data-ttu-id="5bd18-107">**Kopia zapasowa szyfrowane maszyn wirtualnych** — zaszyfrowanych Azure maszyny wirtualne utworzone kopie zapasowe przy użyciu usługi Kopia zapasowa Azure.</span><span class="sxs-lookup"><span data-stu-id="5bd18-107">**Backup encrypted VMs** - Encrypted Azure VMs have been backed up using Azure Backup.</span></span> <span data-ttu-id="5bd18-108">Zobacz artykuł hello [Zarządzanie kopii zapasowej i przywracania maszyn wirtualnych platformy Azure przy użyciu programu PowerShell](backup-azure-vms-automation.md) szczegółowe informacje na temat sposobu toobackup szyfrowane maszynach wirtualnych platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="5bd18-108">Refer hello article [Manage backup and restore of Azure VMs using PowerShell](backup-azure-vms-automation.md) for details about how toobackup encrypted Azure VMs.</span></span>
* <span data-ttu-id="5bd18-109">**Konfigurowanie usługi Azure Key Vault** — upewnij się, że magazyn kluczy toowhich kluczy i kluczy tajnych toobe należy przywrócić jest już obecny.</span><span class="sxs-lookup"><span data-stu-id="5bd18-109">**Configure Azure Key Vault** – Ensure that key vault toowhich keys and secrets need toobe restored is already present.</span></span> <span data-ttu-id="5bd18-110">Zobacz artykuł hello [wprowadzenie do usługi Azure Key Vault](../key-vault/key-vault-get-started.md) szczegółowe informacje na temat zarządzania magazynu kluczy.</span><span class="sxs-lookup"><span data-stu-id="5bd18-110">Refer hello article [Get Started with Azure Key Vault](../key-vault/key-vault-get-started.md) for details about key vault management.</span></span>
* <span data-ttu-id="5bd18-111">**Przywracanie dysku** — upewnij się, że ma wyzwolone zadanie przywracania przywracania dysku zaszyfrowanego maszynę Wirtualną przy użyciu [kroki PowerShell](backup-azure-vms-automation.md#restore-an-azure-vm).</span><span class="sxs-lookup"><span data-stu-id="5bd18-111">**Restore disk** - Ensure that you have triggered restore job for restoring disks for encrypted VM using [PowerShell steps](backup-azure-vms-automation.md#restore-an-azure-vm).</span></span> <span data-ttu-id="5bd18-112">Jest to spowodowane tego zadania generuje plik JSON na koncie magazynu zawierający klucze i klucze tajne dla toobe wirtualna hello szyfrowane przywrócona.</span><span class="sxs-lookup"><span data-stu-id="5bd18-112">This is because this job generates a JSON file in your storage account containing keys and secrets for hello encrypted VM toobe restored.</span></span>

## <a name="get-key-and-secret-from-azure-backup"></a><span data-ttu-id="5bd18-113">Pobierz klucz i klucz tajny usługi Kopia zapasowa Azure</span><span class="sxs-lookup"><span data-stu-id="5bd18-113">Get key and secret from Azure Backup</span></span>

> [!NOTE]
> <span data-ttu-id="5bd18-114">Po przywróceniu dysku dla hello szyfrowane maszyny Wirtualnej, upewnij się, że:</span><span class="sxs-lookup"><span data-stu-id="5bd18-114">Once disk has been restored for hello encrypted VM, ensure that:</span></span>
> 1. <span data-ttu-id="5bd18-115">$details jest wypełniana przywracania dysku szczegóły zadania, jak wspomniano w [programu PowerShell kroki opisane w sekcji dysków hello przywracania](backup-azure-vms-automation.md#restore-an-azure-vm)</span><span class="sxs-lookup"><span data-stu-id="5bd18-115">$details is populated with restore disk job details, as mentioned in [PowerShell steps in Restore hello Disks section](backup-azure-vms-automation.md#restore-an-azure-vm)</span></span>
> 2. <span data-ttu-id="5bd18-116">Należy utworzyć maszyny Wirtualnej z dysków przywróconej tylko **po klucz i klucz tajny jest magazyn przywróconej tookey**.</span><span class="sxs-lookup"><span data-stu-id="5bd18-116">VM should be created from restored disks only **after key and secret is restored tookey vault**.</span></span>
>
>

<span data-ttu-id="5bd18-117">Zapytanie hello przywrócona właściwości dysku hello szczegóły zadania.</span><span class="sxs-lookup"><span data-stu-id="5bd18-117">Query hello restored disk properties for hello job details.</span></span>

```
PS C:\> $properties = $details.properties
PS C:\> $storageAccountName = $properties["Target Storage Account Name"]
PS C:\> $containerName = $properties["Config Blob Container Name"]
PS C:\> $encryptedBlobName = $properties["Encryption Info Blob Name"]
```

<span data-ttu-id="5bd18-118">Ustaw kontekst magazynu Azure hello i przywrócenie pliku konfiguracji JSON zawierający klucz i tajny szczegóły dla zaszyfrowanych maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="5bd18-118">Set hello Azure storage context and restore JSON configuration file containing key and secret details for encrypted VM.</span></span>

```
PS C:\> Set-AzureRmCurrentStorageAccount -Name $storageaccountname -ResourceGroupName '<rg-name>'
PS C:\> $destination_path = 'C:\vmencryption_config.json'
PS C:\> Get-AzureStorageBlobContent -Blob $encryptedBlobName -Container $containerName -Destination $destination_path
PS C:\> $encryptionObject = Get-Content -Path $destination_path  | ConvertFrom-Json
```

## <a name="restore-key"></a><span data-ttu-id="5bd18-119">Przywróć klucz</span><span class="sxs-lookup"><span data-stu-id="5bd18-119">Restore key</span></span>
<span data-ttu-id="5bd18-120">Wygenerowany plik JSON hello w ścieżce docelowej hello wymienione powyżej Generowanie pliku obiektu blob klucza z hello JSON i umieść go toorestore klucza polecenia cmdlet tooput hello klucza (KEK) w magazynie kluczy hello.</span><span class="sxs-lookup"><span data-stu-id="5bd18-120">Once hello JSON file is generated in hello destination path mentioned above, generate key blob file from hello JSON and feed it toorestore key cmdlet tooput hello key (KEK) back in hello key vault.</span></span>

```
PS C:\> $keyDestination = 'C:\keyDetails.blob'
PS C:\> [io.file]::WriteAllBytes($keyDestination, [System.Convert]::FromBase64String($encryptionObject.OsDiskKeyAndSecretDetails.KeyBackupData))
PS C:\> Restore-AzureKeyVaultKey -VaultName '<target_key_vault_name>' -InputFile $keyDestination
```

## <a name="restore-secret"></a><span data-ttu-id="5bd18-121">Przywróć klucz tajny</span><span class="sxs-lookup"><span data-stu-id="5bd18-121">Restore secret</span></span>
<span data-ttu-id="5bd18-122">Użyj pliku JSON hello wygenerowany powyżej tooget tajny nazwą i wartością i umieść go tooset tajny polecenia cmdlet tooput hello tajne (BEK) w magazynie kluczy hello.</span><span class="sxs-lookup"><span data-stu-id="5bd18-122">Use hello JSON file generated above tooget secret name and value and feed it tooset secret cmdlet tooput hello secret (BEK) back in hello key vault.</span></span> <span data-ttu-id="5bd18-123">**Jeśli maszyna wirtualna jest szyfrowana przy użyciu BEK i KEK, należy używać tych poleceń cmdlet.**</span><span class="sxs-lookup"><span data-stu-id="5bd18-123">**Use these cmdlets if your VM is encrypted using BEK and KEK.**</span></span>

```
PS C:\> $secretdata = $encryptionObject.OsDiskKeyAndSecretDetails.SecretData
PS C:\> $Secret = ConvertTo-SecureString -String $secretdata -AsPlainText -Force
PS C:\> $secretname = 'B3284AAA-DAAA-4AAA-B393-60CAA848AAAA'
PS C:\> $Tags = @{'DiskEncryptionKeyEncryptionAlgorithm' = 'RSA-OAEP';'DiskEncryptionKeyFileName' = 'B3284AAA-DAAA-4AAA-B393-60CAA848AAAA.BEK';'DiskEncryptionKeyEncryptionKeyURL' = $encryptionObject.OsDiskKeyAndSecretDetails.KeyUrl;'MachineName' = 'vm-name'}
PS C:\> Set-AzureKeyVaultSecret -VaultName '<target_key_vault_name>' -Name $secretname -SecretValue $Secret -ContentType  'Wrapped BEK' -Tags $Tags
```

<span data-ttu-id="5bd18-124">Jeśli maszyna wirtualna jest **zaszyfrowane za pomocą BEK tylko**, generowanie pliku blob tajnego z hello JSON i umieść go toorestore tajny polecenia cmdlet tooput hello tajne (BEK) w magazynie kluczy hello.</span><span class="sxs-lookup"><span data-stu-id="5bd18-124">If your VM is **encrypted using BEK only**, generate secret blob file from hello JSON and feed it toorestore secret cmdlet tooput hello secret (BEK) back in hello key vault.</span></span>

```
PS C:\> $secretDestination = 'C:\secret.blob'
PS C:\> [io.file]::WriteAllBytes($secretDestination, [System.Convert]::FromBase64String($encryptionObject.OsDiskKeyAndSecretDetails.KeyVaultSecretBackupData))
PS C:\> Restore-AzureKeyVaultSecret -VaultName '<target_key_vault_name>' -InputFile $secretDestination -Verbose
```

> [!NOTE]
> 1. <span data-ttu-id="5bd18-125">Wartość $secretname można uzyskać przez odwołujących się dane wyjściowe toohello $encryptionObject.OsDiskKeyAndSecretDetails.SecretUrl i przy użyciu tekstu po kluczy tajnych / np. adres URL poufne dane wyjściowe jest https://keyvaultname.vault.azure.net/secrets/ Nazwa B3284AAA-DAAA-4AAA-B393-60CAA848AAAA/xx000000xx0849999f3xx30000003163 i tajne jest B3284AAA-DAAA-4AAA-B393-60CAA848AAAA</span><span class="sxs-lookup"><span data-stu-id="5bd18-125">Value for $secretname can be obtained by referring toohello output of $encryptionObject.OsDiskKeyAndSecretDetails.SecretUrl and using text after secrets/ e.g. output secret URL is https://keyvaultname.vault.azure.net/secrets/B3284AAA-DAAA-4AAA-B393-60CAA848AAAA/xx000000xx0849999f3xx30000003163 and secret name is B3284AAA-DAAA-4AAA-B393-60CAA848AAAA</span></span>
> 2. <span data-ttu-id="5bd18-126">Wartość tagu hello DiskEncryptionKeyFileName jest taka sama jak nazwa klucza tajnego.</span><span class="sxs-lookup"><span data-stu-id="5bd18-126">Value of hello tag DiskEncryptionKeyFileName is same as secret name.</span></span>
>
>

## <a name="create-virtual-machine-from-restored-disk"></a><span data-ttu-id="5bd18-127">Tworzenie maszyny wirtualnej z przywróconą dysku</span><span class="sxs-lookup"><span data-stu-id="5bd18-127">Create virtual machine from restored disk</span></span>
<span data-ttu-id="5bd18-128">Jeśli wykonano kopię zapasową zaszyfrowanych maszyny Wirtualnej przy użyciu kopii zapasowej maszyny Wirtualnej Azure, hello poleceń cmdlet programu PowerShell wymienione powyżej pomocy Przywracanie klucza i magazyn kluczy tajnych toohello Wstecz.</span><span class="sxs-lookup"><span data-stu-id="5bd18-128">If you have backed up encrypted VM using Azure VM Backup, hello PowerShell cmdlets mentioned above help you restore key and secret back toohello key vault.</span></span> <span data-ttu-id="5bd18-129">Po przywróceniu je, zobacz artykuł hello [Zarządzanie kopii zapasowej i przywracania maszyn wirtualnych platformy Azure przy użyciu programu PowerShell](backup-azure-vms-automation.md#create-a-vm-from-restored-disks) toocreate szyfrowane maszyn wirtualnych z przywróconą dysku, kluczy i klucz tajny.</span><span class="sxs-lookup"><span data-stu-id="5bd18-129">After restoring them, refer hello article [Manage backup and restore of Azure VMs using PowerShell](backup-azure-vms-automation.md#create-a-vm-from-restored-disks) toocreate encrypted VMs from restored disk, key, and secret.</span></span>

## <a name="legacy-approach"></a><span data-ttu-id="5bd18-130">Podejście starszej wersji</span><span class="sxs-lookup"><span data-stu-id="5bd18-130">Legacy approach</span></span>
<span data-ttu-id="5bd18-131">Witaj wspomnianego powyżej będzie działać we wszystkich punktach odzyskiwania hello.</span><span class="sxs-lookup"><span data-stu-id="5bd18-131">hello approach mentioned above would work for all hello recovery points.</span></span> <span data-ttu-id="5bd18-132">Jednak hello starsze podejście pobierania klucza i tajnych informacji z punktu odzyskiwania, będzie ważny dla punktów odzyskiwania, starsze niż 11 lipca 2017 zaszyfrowane za pomocą BEK i KEK maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="5bd18-132">However, hello older approach of getting key and secret information from recovery point, would be valid for recovery points older than July 11, 2017 for VMs encrypted using BEK and KEK.</span></span> <span data-ttu-id="5bd18-133">Po zakończeniu zadania przywracania dysku dla zaszyfrowanych maszynę Wirtualną przy użyciu [kroki PowerShell](backup-azure-vms-automation.md#restore-an-azure-vm), upewnij się, że $rp jest wypełniane przy użyciu prawidłowej wartości.</span><span class="sxs-lookup"><span data-stu-id="5bd18-133">Once restore disk job is complete for encrypted VM using [PowerShell steps](backup-azure-vms-automation.md#restore-an-azure-vm), ensure that $rp is populated with a valid value.</span></span>

### <a name="restore-key"></a><span data-ttu-id="5bd18-134">Przywróć klucz</span><span class="sxs-lookup"><span data-stu-id="5bd18-134">Restore key</span></span>
<span data-ttu-id="5bd18-135">Użyj hello poniższych poleceń cmdlet tooget klucza (KEK) informacje z punktu odzyskiwania i umieść go w magazynie kluczy hello tooput klucza polecenia cmdlet toorestore.</span><span class="sxs-lookup"><span data-stu-id="5bd18-135">Use hello following cmdlets tooget key (KEK) information from recovery point and feed it toorestore key cmdlet tooput it back in hello key vault.</span></span>

```
PS C:\> $rp1 = Get-AzureRmRecoveryServicesBackupRecoveryPoint -RecoveryPointId $rp[0].RecoveryPointId -Item $backupItem -KeyFileDownloadLocation 'C:\Users\downloads'
PS C:\> Restore-AzureKeyVaultKey -VaultName '<target_key_vault_name>' -InputFile 'C:\Users\downloads'
```

### <a name="restore-secret"></a><span data-ttu-id="5bd18-136">Przywróć klucz tajny</span><span class="sxs-lookup"><span data-stu-id="5bd18-136">Restore secret</span></span>
<span data-ttu-id="5bd18-137">Użyj następujących poleceń cmdlet tooget klucz tajny (BEK) informacji z punktu odzyskiwania hello i umieść go tooput tajny polecenia cmdlet tooset ponownie hello magazynu kluczy.</span><span class="sxs-lookup"><span data-stu-id="5bd18-137">Use hello following cmdlets tooget secret (BEK) information from recovery point and feed it tooset secret cmdlet tooput it back in hello key vault.</span></span>

```
PS C:\> $secretname = 'B3284AAA-DAAA-4AAA-B393-60CAA848AAAA'
PS C:\> $secretdata = $rp1.KeyAndSecretDetails.SecretData
PS C:\> $Secret = ConvertTo-SecureString -String $secretdata -AsPlainText -Force
PS C:\> $Tags = @{'DiskEncryptionKeyEncryptionAlgorithm' = 'RSA-OAEP';'DiskEncryptionKeyFileName' = 'B3284AAA-DAAA-4AAA-B393-60CAA848AAAA.BEK';'DiskEncryptionKeyEncryptionKeyURL' = 'https://mykeyvault.vault.azure.net:443/keys/KeyName/84daaac999949999030bf99aaa5a9f9';'MachineName' = 'vm-name'}
PS C:\> Set-AzureKeyVaultSecret -VaultName '<target_key_vault_name>' -Name $secretname -SecretValue $secret -Tags $Tags -SecretValue $Secret -ContentType  'Wrapped BEK'
```

> [!NOTE]
> 1. <span data-ttu-id="5bd18-138">Wartość $secretname można uzyskać, odnosząc się dane wyjściowe toohello po1 $. KeyAndSecretDetails.SecretUrl i przy użyciu tekstu po kluczy tajnych / np. adres URL poufne dane wyjściowe jest https://keyvaultname.vault.azure.net/secrets/B3284AAA-DAAA-4AAA-B393-60CAA848AAAA/xx000000xx0849999f3xx30000003163 i jest nazwa klucza tajnego B3284AAA-DAAA-4AAA-B393-60CAA848AAAA</span><span class="sxs-lookup"><span data-stu-id="5bd18-138">Value for $secretname can be obtained by referring toohello output of $rp1.KeyAndSecretDetails.SecretUrl and using text after secrets/ e.g. output secret URL is https://keyvaultname.vault.azure.net/secrets/B3284AAA-DAAA-4AAA-B393-60CAA848AAAA/xx000000xx0849999f3xx30000003163 and secret name is B3284AAA-DAAA-4AAA-B393-60CAA848AAAA</span></span>
> 2. <span data-ttu-id="5bd18-139">Wartość tagu hello DiskEncryptionKeyFileName jest taka sama jak nazwa klucza tajnego.</span><span class="sxs-lookup"><span data-stu-id="5bd18-139">Value of hello tag DiskEncryptionKeyFileName is same as secret name.</span></span>
> 3. <span data-ttu-id="5bd18-140">Wartość DiskEncryptionKeyEncryptionKeyURL można uzyskać z magazynu kluczy po Przywracanie kluczy hello powrót i używanie [Get-AzureKeyVaultKey](https://msdn.microsoft.com/library/dn868053.aspx) polecenia cmdlet</span><span class="sxs-lookup"><span data-stu-id="5bd18-140">Value for DiskEncryptionKeyEncryptionKeyURL can be obtained from key vault after restoring hello keys back and using [Get-AzureKeyVaultKey](https://msdn.microsoft.com/library/dn868053.aspx) cmdlet</span></span>
>
>

## <a name="next-steps"></a><span data-ttu-id="5bd18-141">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="5bd18-141">Next steps</span></span>
<span data-ttu-id="5bd18-142">Po przywróceniu klucz i tajny tookey wstecz magazynu, można znaleźć artykuł hello [Zarządzanie kopii zapasowej i przywracania maszyn wirtualnych platformy Azure przy użyciu programu PowerShell](backup-azure-vms-automation.md#create-a-vm-from-restored-disks) toocreate szyfrowane maszyn wirtualnych z przywróconą dysku, kluczy i klucz tajny.</span><span class="sxs-lookup"><span data-stu-id="5bd18-142">After restoring key and secret back tookey vault, refer hello article [Manage backup and restore of Azure VMs using PowerShell](backup-azure-vms-automation.md#create-a-vm-from-restored-disks) toocreate encrypted VMs from restored disk, key and secret.</span></span>
