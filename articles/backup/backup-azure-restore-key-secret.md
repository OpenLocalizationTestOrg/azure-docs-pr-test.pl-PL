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
# <a name="restore-key-vault-key-and-secret-for-encrypted-vms-using-azure-backup"></a>Przywróć klucz magazynu kluczy oraz klucz tajny dla zaszyfrowanych maszyn wirtualnych za pomocą usługi Kopia zapasowa Azure
Ten artykuł zawiera informacje o przy użyciu kopii zapasowej maszyny Wirtualnej Azure tooperform przywracanie zaszyfrowanych maszynach wirtualnych platformy Azure, jeśli klucz, a klucz tajny nie istnieją w magazynie kluczy hello. Te kroki można także toomaintain osobną kopię klucza (klucz szyfrowania klucza) i klucz tajny (klucza szyfrowania funkcją BitLocker) dla hello przywrócić maszyny Wirtualnej.

## <a name="prerequisites"></a>Wymagania wstępne
* **Kopia zapasowa szyfrowane maszyn wirtualnych** — zaszyfrowanych Azure maszyny wirtualne utworzone kopie zapasowe przy użyciu usługi Kopia zapasowa Azure. Zobacz artykuł hello [Zarządzanie kopii zapasowej i przywracania maszyn wirtualnych platformy Azure przy użyciu programu PowerShell](backup-azure-vms-automation.md) szczegółowe informacje na temat sposobu toobackup szyfrowane maszynach wirtualnych platformy Azure.
* **Konfigurowanie usługi Azure Key Vault** — upewnij się, że magazyn kluczy toowhich kluczy i kluczy tajnych toobe należy przywrócić jest już obecny. Zobacz artykuł hello [wprowadzenie do usługi Azure Key Vault](../key-vault/key-vault-get-started.md) szczegółowe informacje na temat zarządzania magazynu kluczy.
* **Przywracanie dysku** — upewnij się, że ma wyzwolone zadanie przywracania przywracania dysku zaszyfrowanego maszynę Wirtualną przy użyciu [kroki PowerShell](backup-azure-vms-automation.md#restore-an-azure-vm). Jest to spowodowane tego zadania generuje plik JSON na koncie magazynu zawierający klucze i klucze tajne dla toobe wirtualna hello szyfrowane przywrócona.

## <a name="get-key-and-secret-from-azure-backup"></a>Pobierz klucz i klucz tajny usługi Kopia zapasowa Azure

> [!NOTE]
> Po przywróceniu dysku dla hello szyfrowane maszyny Wirtualnej, upewnij się, że:
> 1. $details jest wypełniana przywracania dysku szczegóły zadania, jak wspomniano w [programu PowerShell kroki opisane w sekcji dysków hello przywracania](backup-azure-vms-automation.md#restore-an-azure-vm)
> 2. Należy utworzyć maszyny Wirtualnej z dysków przywróconej tylko **po klucz i klucz tajny jest magazyn przywróconej tookey**.
>
>

Zapytanie hello przywrócona właściwości dysku hello szczegóły zadania.

```
PS C:\> $properties = $details.properties
PS C:\> $storageAccountName = $properties["Target Storage Account Name"]
PS C:\> $containerName = $properties["Config Blob Container Name"]
PS C:\> $encryptedBlobName = $properties["Encryption Info Blob Name"]
```

Ustaw kontekst magazynu Azure hello i przywrócenie pliku konfiguracji JSON zawierający klucz i tajny szczegóły dla zaszyfrowanych maszyny Wirtualnej.

```
PS C:\> Set-AzureRmCurrentStorageAccount -Name $storageaccountname -ResourceGroupName '<rg-name>'
PS C:\> $destination_path = 'C:\vmencryption_config.json'
PS C:\> Get-AzureStorageBlobContent -Blob $encryptedBlobName -Container $containerName -Destination $destination_path
PS C:\> $encryptionObject = Get-Content -Path $destination_path  | ConvertFrom-Json
```

## <a name="restore-key"></a>Przywróć klucz
Wygenerowany plik JSON hello w ścieżce docelowej hello wymienione powyżej Generowanie pliku obiektu blob klucza z hello JSON i umieść go toorestore klucza polecenia cmdlet tooput hello klucza (KEK) w magazynie kluczy hello.

```
PS C:\> $keyDestination = 'C:\keyDetails.blob'
PS C:\> [io.file]::WriteAllBytes($keyDestination, [System.Convert]::FromBase64String($encryptionObject.OsDiskKeyAndSecretDetails.KeyBackupData))
PS C:\> Restore-AzureKeyVaultKey -VaultName '<target_key_vault_name>' -InputFile $keyDestination
```

## <a name="restore-secret"></a>Przywróć klucz tajny
Użyj pliku JSON hello wygenerowany powyżej tooget tajny nazwą i wartością i umieść go tooset tajny polecenia cmdlet tooput hello tajne (BEK) w magazynie kluczy hello. **Jeśli maszyna wirtualna jest szyfrowana przy użyciu BEK i KEK, należy używać tych poleceń cmdlet.**

```
PS C:\> $secretdata = $encryptionObject.OsDiskKeyAndSecretDetails.SecretData
PS C:\> $Secret = ConvertTo-SecureString -String $secretdata -AsPlainText -Force
PS C:\> $secretname = 'B3284AAA-DAAA-4AAA-B393-60CAA848AAAA'
PS C:\> $Tags = @{'DiskEncryptionKeyEncryptionAlgorithm' = 'RSA-OAEP';'DiskEncryptionKeyFileName' = 'B3284AAA-DAAA-4AAA-B393-60CAA848AAAA.BEK';'DiskEncryptionKeyEncryptionKeyURL' = $encryptionObject.OsDiskKeyAndSecretDetails.KeyUrl;'MachineName' = 'vm-name'}
PS C:\> Set-AzureKeyVaultSecret -VaultName '<target_key_vault_name>' -Name $secretname -SecretValue $Secret -ContentType  'Wrapped BEK' -Tags $Tags
```

Jeśli maszyna wirtualna jest **zaszyfrowane za pomocą BEK tylko**, generowanie pliku blob tajnego z hello JSON i umieść go toorestore tajny polecenia cmdlet tooput hello tajne (BEK) w magazynie kluczy hello.

```
PS C:\> $secretDestination = 'C:\secret.blob'
PS C:\> [io.file]::WriteAllBytes($secretDestination, [System.Convert]::FromBase64String($encryptionObject.OsDiskKeyAndSecretDetails.KeyVaultSecretBackupData))
PS C:\> Restore-AzureKeyVaultSecret -VaultName '<target_key_vault_name>' -InputFile $secretDestination -Verbose
```

> [!NOTE]
> 1. Wartość $secretname można uzyskać przez odwołujących się dane wyjściowe toohello $encryptionObject.OsDiskKeyAndSecretDetails.SecretUrl i przy użyciu tekstu po kluczy tajnych / np. adres URL poufne dane wyjściowe jest https://keyvaultname.vault.azure.net/secrets/ Nazwa B3284AAA-DAAA-4AAA-B393-60CAA848AAAA/xx000000xx0849999f3xx30000003163 i tajne jest B3284AAA-DAAA-4AAA-B393-60CAA848AAAA
> 2. Wartość tagu hello DiskEncryptionKeyFileName jest taka sama jak nazwa klucza tajnego.
>
>

## <a name="create-virtual-machine-from-restored-disk"></a>Tworzenie maszyny wirtualnej z przywróconą dysku
Jeśli wykonano kopię zapasową zaszyfrowanych maszyny Wirtualnej przy użyciu kopii zapasowej maszyny Wirtualnej Azure, hello poleceń cmdlet programu PowerShell wymienione powyżej pomocy Przywracanie klucza i magazyn kluczy tajnych toohello Wstecz. Po przywróceniu je, zobacz artykuł hello [Zarządzanie kopii zapasowej i przywracania maszyn wirtualnych platformy Azure przy użyciu programu PowerShell](backup-azure-vms-automation.md#create-a-vm-from-restored-disks) toocreate szyfrowane maszyn wirtualnych z przywróconą dysku, kluczy i klucz tajny.

## <a name="legacy-approach"></a>Podejście starszej wersji
Witaj wspomnianego powyżej będzie działać we wszystkich punktach odzyskiwania hello. Jednak hello starsze podejście pobierania klucza i tajnych informacji z punktu odzyskiwania, będzie ważny dla punktów odzyskiwania, starsze niż 11 lipca 2017 zaszyfrowane za pomocą BEK i KEK maszyn wirtualnych. Po zakończeniu zadania przywracania dysku dla zaszyfrowanych maszynę Wirtualną przy użyciu [kroki PowerShell](backup-azure-vms-automation.md#restore-an-azure-vm), upewnij się, że $rp jest wypełniane przy użyciu prawidłowej wartości.

### <a name="restore-key"></a>Przywróć klucz
Użyj hello poniższych poleceń cmdlet tooget klucza (KEK) informacje z punktu odzyskiwania i umieść go w magazynie kluczy hello tooput klucza polecenia cmdlet toorestore.

```
PS C:\> $rp1 = Get-AzureRmRecoveryServicesBackupRecoveryPoint -RecoveryPointId $rp[0].RecoveryPointId -Item $backupItem -KeyFileDownloadLocation 'C:\Users\downloads'
PS C:\> Restore-AzureKeyVaultKey -VaultName '<target_key_vault_name>' -InputFile 'C:\Users\downloads'
```

### <a name="restore-secret"></a>Przywróć klucz tajny
Użyj następujących poleceń cmdlet tooget klucz tajny (BEK) informacji z punktu odzyskiwania hello i umieść go tooput tajny polecenia cmdlet tooset ponownie hello magazynu kluczy.

```
PS C:\> $secretname = 'B3284AAA-DAAA-4AAA-B393-60CAA848AAAA'
PS C:\> $secretdata = $rp1.KeyAndSecretDetails.SecretData
PS C:\> $Secret = ConvertTo-SecureString -String $secretdata -AsPlainText -Force
PS C:\> $Tags = @{'DiskEncryptionKeyEncryptionAlgorithm' = 'RSA-OAEP';'DiskEncryptionKeyFileName' = 'B3284AAA-DAAA-4AAA-B393-60CAA848AAAA.BEK';'DiskEncryptionKeyEncryptionKeyURL' = 'https://mykeyvault.vault.azure.net:443/keys/KeyName/84daaac999949999030bf99aaa5a9f9';'MachineName' = 'vm-name'}
PS C:\> Set-AzureKeyVaultSecret -VaultName '<target_key_vault_name>' -Name $secretname -SecretValue $secret -Tags $Tags -SecretValue $Secret -ContentType  'Wrapped BEK'
```

> [!NOTE]
> 1. Wartość $secretname można uzyskać, odnosząc się dane wyjściowe toohello po1 $. KeyAndSecretDetails.SecretUrl i przy użyciu tekstu po kluczy tajnych / np. adres URL poufne dane wyjściowe jest https://keyvaultname.vault.azure.net/secrets/B3284AAA-DAAA-4AAA-B393-60CAA848AAAA/xx000000xx0849999f3xx30000003163 i jest nazwa klucza tajnego B3284AAA-DAAA-4AAA-B393-60CAA848AAAA
> 2. Wartość tagu hello DiskEncryptionKeyFileName jest taka sama jak nazwa klucza tajnego.
> 3. Wartość DiskEncryptionKeyEncryptionKeyURL można uzyskać z magazynu kluczy po Przywracanie kluczy hello powrót i używanie [Get-AzureKeyVaultKey](https://msdn.microsoft.com/library/dn868053.aspx) polecenia cmdlet
>
>

## <a name="next-steps"></a>Następne kroki
Po przywróceniu klucz i tajny tookey wstecz magazynu, można znaleźć artykuł hello [Zarządzanie kopii zapasowej i przywracania maszyn wirtualnych platformy Azure przy użyciu programu PowerShell](backup-azure-vms-automation.md#create-a-vm-from-restored-disks) toocreate szyfrowane maszyn wirtualnych z przywróconą dysku, kluczy i klucz tajny.
