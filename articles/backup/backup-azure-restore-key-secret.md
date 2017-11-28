---
title: "Przywróć klucz magazynu kluczy oraz klucz tajny dla zaszyfrowanych maszyn wirtualnych za pomocą usługi Kopia zapasowa Azure | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak można przywrócić klucza magazynu kluczy i klucz tajny w kopii zapasowej Azure przy użyciu programu PowerShell"
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
ms.openlocfilehash: f2db3449187d655248b13198b268841052570626
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
# <a name="restore-key-vault-key-and-secret-for-encrypted-vms-using-azure-backup"></a><span data-ttu-id="e67fb-103">Przywróć klucz magazynu kluczy oraz klucz tajny dla zaszyfrowanych maszyn wirtualnych za pomocą usługi Kopia zapasowa Azure</span><span class="sxs-lookup"><span data-stu-id="e67fb-103">Restore Key Vault key and secret for encrypted VMs using Azure Backup</span></span>
<span data-ttu-id="e67fb-104">Ten artykuł zawiera informacje o przy użyciu kopii zapasowej maszyny Wirtualnej Azure przeprowadzić przywracanie zaszyfrowanych maszynach wirtualnych platformy Azure, jeśli klucz, a klucz tajny nie istnieje w magazynie kluczy.</span><span class="sxs-lookup"><span data-stu-id="e67fb-104">This article talks about using Azure VM Backup to perform restore of encrypted Azure VMs, if your key and secret do not exist in the key vault.</span></span> <span data-ttu-id="e67fb-105">Te kroki można także jeśli chcesz zachować kopię klucza (klucz szyfrowania klucza) i klucz tajny (klucza szyfrowania funkcją BitLocker) przywróconej maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="e67fb-105">These steps can also be used if you want to maintain a separate copy of key (Key Encryption Key) and secret (BitLocker Encryption Key) for the restored VM.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e67fb-106">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="e67fb-106">Prerequisites</span></span>
* <span data-ttu-id="e67fb-107">**Kopia zapasowa szyfrowane maszyn wirtualnych** — zaszyfrowanych Azure maszyny wirtualne utworzone kopie zapasowe przy użyciu usługi Kopia zapasowa Azure.</span><span class="sxs-lookup"><span data-stu-id="e67fb-107">**Backup encrypted VMs** - Encrypted Azure VMs have been backed up using Azure Backup.</span></span> <span data-ttu-id="e67fb-108">Zobacz artykuł [Zarządzanie kopii zapasowej i przywracania maszyn wirtualnych platformy Azure przy użyciu programu PowerShell](backup-azure-vms-automation.md) szczegółowe informacje o sposobie tworzenia kopii zapasowej zaszyfrowanego maszynach wirtualnych platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="e67fb-108">Refer the article [Manage backup and restore of Azure VMs using PowerShell](backup-azure-vms-automation.md) for details about how to backup encrypted Azure VMs.</span></span>
* <span data-ttu-id="e67fb-109">**Konfigurowanie usługi Azure Key Vault** — upewnij się, że magazyn kluczy, do której konieczne jest przywrócenie kluczy i kluczy tajnych znajduje się już.</span><span class="sxs-lookup"><span data-stu-id="e67fb-109">**Configure Azure Key Vault** – Ensure that key vault to which keys and secrets need to be restored is already present.</span></span> <span data-ttu-id="e67fb-110">Zobacz artykuł [wprowadzenie do usługi Azure Key Vault](../key-vault/key-vault-get-started.md) szczegółowe informacje na temat zarządzania magazynu kluczy.</span><span class="sxs-lookup"><span data-stu-id="e67fb-110">Refer the article [Get Started with Azure Key Vault](../key-vault/key-vault-get-started.md) for details about key vault management.</span></span>
* <span data-ttu-id="e67fb-111">**Przywracanie dysku** — upewnij się, że ma wyzwolone zadanie przywracania przywracania dysku zaszyfrowanego maszynę Wirtualną przy użyciu [kroki PowerShell](backup-azure-vms-automation.md#restore-an-azure-vm).</span><span class="sxs-lookup"><span data-stu-id="e67fb-111">**Restore disk** - Ensure that you have triggered restore job for restoring disks for encrypted VM using [PowerShell steps](backup-azure-vms-automation.md#restore-an-azure-vm).</span></span> <span data-ttu-id="e67fb-112">Jest to spowodowane tego zadania generuje plik JSON na koncie magazynu zawierające kluczy i kluczy tajnych zaszyfrowanych maszyny wirtualnej do przywrócenia.</span><span class="sxs-lookup"><span data-stu-id="e67fb-112">This is because this job generates a JSON file in your storage account containing keys and secrets for the encrypted VM to be restored.</span></span>

## <a name="get-key-and-secret-from-azure-backup"></a><span data-ttu-id="e67fb-113">Pobierz klucz i klucz tajny usługi Kopia zapasowa Azure</span><span class="sxs-lookup"><span data-stu-id="e67fb-113">Get key and secret from Azure Backup</span></span>

> [!NOTE]
> <span data-ttu-id="e67fb-114">Po przywróceniu dysku zaszyfrowanego maszyny wirtualnej, upewnij się, że:</span><span class="sxs-lookup"><span data-stu-id="e67fb-114">Once disk has been restored for the encrypted VM, ensure that:</span></span>
> 1. <span data-ttu-id="e67fb-115">$details jest wypełniana przywracania dysku szczegóły zadania, jak wspomniano w [programu PowerShell opisanych w sekcjach przywracania sekcji dysków](backup-azure-vms-automation.md#restore-an-azure-vm)</span><span class="sxs-lookup"><span data-stu-id="e67fb-115">$details is populated with restore disk job details, as mentioned in [PowerShell steps in Restore the Disks section](backup-azure-vms-automation.md#restore-an-azure-vm)</span></span>
> 2. <span data-ttu-id="e67fb-116">Należy utworzyć maszyny Wirtualnej z dysków przywróconej tylko **po klucz i klucz tajny są odzyskiwane do magazynu kluczy**.</span><span class="sxs-lookup"><span data-stu-id="e67fb-116">VM should be created from restored disks only **after key and secret is restored to key vault**.</span></span>
>
>

<span data-ttu-id="e67fb-117">Wyślij zapytanie do właściwości dysku przywróconej szczegóły zadania.</span><span class="sxs-lookup"><span data-stu-id="e67fb-117">Query the restored disk properties for the job details.</span></span>

```
PS C:\> $properties = $details.properties
PS C:\> $storageAccountName = $properties["Target Storage Account Name"]
PS C:\> $containerName = $properties["Config Blob Container Name"]
PS C:\> $encryptedBlobName = $properties["Encryption Info Blob Name"]
```

<span data-ttu-id="e67fb-118">Ustaw kontekst magazynu Azure i przywrócić plik JSON konfiguracji zawierający klucz i tajny szczegóły dla zaszyfrowanych maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="e67fb-118">Set the Azure storage context and restore JSON configuration file containing key and secret details for encrypted VM.</span></span>

```
PS C:\> Set-AzureRmCurrentStorageAccount -Name $storageaccountname -ResourceGroupName '<rg-name>'
PS C:\> $destination_path = 'C:\vmencryption_config.json'
PS C:\> Get-AzureStorageBlobContent -Blob $encryptedBlobName -Container $containerName -Destination $destination_path
PS C:\> $encryptionObject = Get-Content -Path $destination_path  | ConvertFrom-Json
```

## <a name="restore-key"></a><span data-ttu-id="e67fb-119">Przywróć klucz</span><span class="sxs-lookup"><span data-stu-id="e67fb-119">Restore key</span></span>
<span data-ttu-id="e67fb-120">Wygenerowany plik JSON w ścieżce docelowej wymienione powyżej Generowanie pliku obiektu blob klucza w formacie JSON i źródła danych do przywrócenia klucza polecenia cmdlet, aby umieścić klucza (KEK) Wstecz w magazynie kluczy.</span><span class="sxs-lookup"><span data-stu-id="e67fb-120">Once the JSON file is generated in the destination path mentioned above, generate key blob file from the JSON and feed it to restore key cmdlet to put the key (KEK) back in the key vault.</span></span>

```
PS C:\> $keyDestination = 'C:\keyDetails.blob'
PS C:\> [io.file]::WriteAllBytes($keyDestination, [System.Convert]::FromBase64String($encryptionObject.OsDiskKeyAndSecretDetails.KeyBackupData))
PS C:\> Restore-AzureKeyVaultKey -VaultName '<target_key_vault_name>' -InputFile $keyDestination
```

## <a name="restore-secret"></a><span data-ttu-id="e67fb-121">Przywróć klucz tajny</span><span class="sxs-lookup"><span data-stu-id="e67fb-121">Restore secret</span></span>
<span data-ttu-id="e67fb-122">Użyj pliku JSON wygenerowany powyżej uzyskać tajny nazwą i wartością i umieść go, aby ustawić tajny polecenia cmdlet, aby umieścić klucz tajny (BEK) Wstecz w magazynie kluczy.</span><span class="sxs-lookup"><span data-stu-id="e67fb-122">Use the JSON file generated above to get secret name and value and feed it to set secret cmdlet to put the secret (BEK) back in the key vault.</span></span> <span data-ttu-id="e67fb-123">**Jeśli maszyna wirtualna jest szyfrowana przy użyciu BEK i KEK, należy używać tych poleceń cmdlet.**</span><span class="sxs-lookup"><span data-stu-id="e67fb-123">**Use these cmdlets if your VM is encrypted using BEK and KEK.**</span></span>

```
PS C:\> $secretdata = $encryptionObject.OsDiskKeyAndSecretDetails.SecretData
PS C:\> $Secret = ConvertTo-SecureString -String $secretdata -AsPlainText -Force
PS C:\> $secretname = 'B3284AAA-DAAA-4AAA-B393-60CAA848AAAA'
PS C:\> $Tags = @{'DiskEncryptionKeyEncryptionAlgorithm' = 'RSA-OAEP';'DiskEncryptionKeyFileName' = 'B3284AAA-DAAA-4AAA-B393-60CAA848AAAA.BEK';'DiskEncryptionKeyEncryptionKeyURL' = $encryptionObject.OsDiskKeyAndSecretDetails.KeyUrl;'MachineName' = 'vm-name'}
PS C:\> Set-AzureKeyVaultSecret -VaultName '<target_key_vault_name>' -Name $secretname -SecretValue $Secret -ContentType  'Wrapped BEK' -Tags $Tags
```

<span data-ttu-id="e67fb-124">Jeśli maszyna wirtualna jest **zaszyfrowane za pomocą BEK tylko**, generowanie pliku blob tajny w formacie JSON i umieść go przywrócić poufne polecenia cmdlet, aby umieścić klucz tajny (BEK) w magazynie kluczy.</span><span class="sxs-lookup"><span data-stu-id="e67fb-124">If your VM is **encrypted using BEK only**, generate secret blob file from the JSON and feed it to restore secret cmdlet to put the secret (BEK) back in the key vault.</span></span>

```
PS C:\> $secretDestination = 'C:\secret.blob'
PS C:\> [io.file]::WriteAllBytes($secretDestination, [System.Convert]::FromBase64String($encryptionObject.OsDiskKeyAndSecretDetails.KeyVaultSecretBackupData))
PS C:\> Restore-AzureKeyVaultSecret -VaultName '<target_key_vault_name>' -InputFile $secretDestination -Verbose
```

> [!NOTE]
> 1. <span data-ttu-id="e67fb-125">Wartość $secretname można uzyskać przez odwołujących się do danych wyjściowych $encryptionObject.OsDiskKeyAndSecretDetails.SecretUrl i przy użyciu tekstu po kluczy tajnych / np. adres URL poufne dane wyjściowe jest https://keyvaultname.vault.azure.net/secrets/ Nazwa B3284AAA-DAAA-4AAA-B393-60CAA848AAAA/xx000000xx0849999f3xx30000003163 i tajne jest B3284AAA-DAAA-4AAA-B393-60CAA848AAAA</span><span class="sxs-lookup"><span data-stu-id="e67fb-125">Value for $secretname can be obtained by referring to the output of $encryptionObject.OsDiskKeyAndSecretDetails.SecretUrl and using text after secrets/ e.g. output secret URL is https://keyvaultname.vault.azure.net/secrets/B3284AAA-DAAA-4AAA-B393-60CAA848AAAA/xx000000xx0849999f3xx30000003163 and secret name is B3284AAA-DAAA-4AAA-B393-60CAA848AAAA</span></span>
> 2. <span data-ttu-id="e67fb-126">Wartość tagu DiskEncryptionKeyFileName jest taka sama jak nazwa klucza tajnego.</span><span class="sxs-lookup"><span data-stu-id="e67fb-126">Value of the tag DiskEncryptionKeyFileName is same as secret name.</span></span>
>
>

## <a name="create-virtual-machine-from-restored-disk"></a><span data-ttu-id="e67fb-127">Tworzenie maszyny wirtualnej z przywróconą dysku</span><span class="sxs-lookup"><span data-stu-id="e67fb-127">Create virtual machine from restored disk</span></span>
<span data-ttu-id="e67fb-128">Jeśli wykonano kopię zapasową zaszyfrowanych maszyny Wirtualnej przy użyciu kopii zapasowej maszyny Wirtualnej Azure, poleceń cmdlet programu PowerShell wymienione powyżej pomocy Przywracanie klucza i z powrotem tajnego do magazynu kluczy.</span><span class="sxs-lookup"><span data-stu-id="e67fb-128">If you have backed up encrypted VM using Azure VM Backup, the PowerShell cmdlets mentioned above help you restore key and secret back to the key vault.</span></span> <span data-ttu-id="e67fb-129">Po przywróceniu ich, zobacz artykuł [Zarządzanie kopii zapasowej i przywracania maszyn wirtualnych platformy Azure przy użyciu programu PowerShell](backup-azure-vms-automation.md#create-a-vm-from-restored-disks) do tworzenia zaszyfrowanego maszyn wirtualnych z przywróconą dysku, kluczy i klucz tajny.</span><span class="sxs-lookup"><span data-stu-id="e67fb-129">After restoring them, refer the article [Manage backup and restore of Azure VMs using PowerShell](backup-azure-vms-automation.md#create-a-vm-from-restored-disks) to create encrypted VMs from restored disk, key, and secret.</span></span>

## <a name="legacy-approach"></a><span data-ttu-id="e67fb-130">Podejście starszej wersji</span><span class="sxs-lookup"><span data-stu-id="e67fb-130">Legacy approach</span></span>
<span data-ttu-id="e67fb-131">Wspomnianego powyżej będzie działać we wszystkich punktach odzyskiwania.</span><span class="sxs-lookup"><span data-stu-id="e67fb-131">The approach mentioned above would work for all the recovery points.</span></span> <span data-ttu-id="e67fb-132">Jednak starsze podejście pobierania klucza i tajnych informacji z punktu odzyskiwania, będzie ważny dla punktów odzyskiwania, starsze niż 11 lipca 2017 zaszyfrowane za pomocą BEK i KEK maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="e67fb-132">However, the older approach of getting key and secret information from recovery point, would be valid for recovery points older than July 11, 2017 for VMs encrypted using BEK and KEK.</span></span> <span data-ttu-id="e67fb-133">Po zakończeniu zadania przywracania dysku dla zaszyfrowanych maszynę Wirtualną przy użyciu [kroki PowerShell](backup-azure-vms-automation.md#restore-an-azure-vm), upewnij się, że $rp jest wypełniane przy użyciu prawidłowej wartości.</span><span class="sxs-lookup"><span data-stu-id="e67fb-133">Once restore disk job is complete for encrypted VM using [PowerShell steps](backup-azure-vms-automation.md#restore-an-azure-vm), ensure that $rp is populated with a valid value.</span></span>

### <a name="restore-key"></a><span data-ttu-id="e67fb-134">Przywróć klucz</span><span class="sxs-lookup"><span data-stu-id="e67fb-134">Restore key</span></span>
<span data-ttu-id="e67fb-135">Pobieranie informacji klucza (KEK) z punktu odzyskiwania i umieść go do przywrócenia klucza polecenia cmdlet, aby ją ponownie w magazynie kluczy, należy użyć następujących poleceń cmdlet.</span><span class="sxs-lookup"><span data-stu-id="e67fb-135">Use the following cmdlets to get key (KEK) information from recovery point and feed it to restore key cmdlet to put it back in the key vault.</span></span>

```
PS C:\> $rp1 = Get-AzureRmRecoveryServicesBackupRecoveryPoint -RecoveryPointId $rp[0].RecoveryPointId -Item $backupItem -KeyFileDownloadLocation 'C:\Users\downloads'
PS C:\> Restore-AzureKeyVaultKey -VaultName '<target_key_vault_name>' -InputFile 'C:\Users\downloads'
```

### <a name="restore-secret"></a><span data-ttu-id="e67fb-136">Przywróć klucz tajny</span><span class="sxs-lookup"><span data-stu-id="e67fb-136">Restore secret</span></span>
<span data-ttu-id="e67fb-137">Użyj następujących poleceń cmdlet uzyskać tajnych informacji (BEK) z punktu odzyskiwania i umieść go ustawić umieszcza je w magazynie kluczy tajnych polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="e67fb-137">Use the following cmdlets to get secret (BEK) information from recovery point and feed it to set secret cmdlet to put it back in the key vault.</span></span>

```
PS C:\> $secretname = 'B3284AAA-DAAA-4AAA-B393-60CAA848AAAA'
PS C:\> $secretdata = $rp1.KeyAndSecretDetails.SecretData
PS C:\> $Secret = ConvertTo-SecureString -String $secretdata -AsPlainText -Force
PS C:\> $Tags = @{'DiskEncryptionKeyEncryptionAlgorithm' = 'RSA-OAEP';'DiskEncryptionKeyFileName' = 'B3284AAA-DAAA-4AAA-B393-60CAA848AAAA.BEK';'DiskEncryptionKeyEncryptionKeyURL' = 'https://mykeyvault.vault.azure.net:443/keys/KeyName/84daaac999949999030bf99aaa5a9f9';'MachineName' = 'vm-name'}
PS C:\> Set-AzureKeyVaultSecret -VaultName '<target_key_vault_name>' -Name $secretname -SecretValue $secret -Tags $Tags -SecretValue $Secret -ContentType  'Wrapped BEK'
```

> [!NOTE]
> 1. <span data-ttu-id="e67fb-138">Wartość $secretname można uzyskać, odwołując się do danych wyjściowych $po1. KeyAndSecretDetails.SecretUrl i przy użyciu tekstu po kluczy tajnych / np. adres URL poufne dane wyjściowe jest https://keyvaultname.vault.azure.net/secrets/B3284AAA-DAAA-4AAA-B393-60CAA848AAAA/xx000000xx0849999f3xx30000003163 i jest nazwa klucza tajnego B3284AAA-DAAA-4AAA-B393-60CAA848AAAA</span><span class="sxs-lookup"><span data-stu-id="e67fb-138">Value for $secretname can be obtained by referring to the output of $rp1.KeyAndSecretDetails.SecretUrl and using text after secrets/ e.g. output secret URL is https://keyvaultname.vault.azure.net/secrets/B3284AAA-DAAA-4AAA-B393-60CAA848AAAA/xx000000xx0849999f3xx30000003163 and secret name is B3284AAA-DAAA-4AAA-B393-60CAA848AAAA</span></span>
> 2. <span data-ttu-id="e67fb-139">Wartość tagu DiskEncryptionKeyFileName jest taka sama jak nazwa klucza tajnego.</span><span class="sxs-lookup"><span data-stu-id="e67fb-139">Value of the tag DiskEncryptionKeyFileName is same as secret name.</span></span>
> 3. <span data-ttu-id="e67fb-140">Wartość DiskEncryptionKeyEncryptionKeyURL można uzyskać z magazynu kluczy po Przywracanie kluczy powrót i używanie [Get-AzureKeyVaultKey](https://msdn.microsoft.com/library/dn868053.aspx) polecenia cmdlet</span><span class="sxs-lookup"><span data-stu-id="e67fb-140">Value for DiskEncryptionKeyEncryptionKeyURL can be obtained from key vault after restoring the keys back and using [Get-AzureKeyVaultKey](https://msdn.microsoft.com/library/dn868053.aspx) cmdlet</span></span>
>
>

## <a name="next-steps"></a><span data-ttu-id="e67fb-141">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="e67fb-141">Next steps</span></span>
<span data-ttu-id="e67fb-142">Po przywróceniu klucza i z powrotem tajnego do magazynu kluczy, zobacz artykuł [Zarządzanie kopii zapasowej i przywracania maszyn wirtualnych platformy Azure przy użyciu programu PowerShell](backup-azure-vms-automation.md#create-a-vm-from-restored-disks) do tworzenia zaszyfrowanego maszyn wirtualnych z przywróconą dysku, kluczy i klucz tajny.</span><span class="sxs-lookup"><span data-stu-id="e67fb-142">After restoring key and secret back to key vault, refer the article [Manage backup and restore of Azure VMs using PowerShell](backup-azure-vms-automation.md#create-a-vm-from-restored-disks) to create encrypted VMs from restored disk, key and secret.</span></span>
