---
ms.assetid: 
title: "Klucze konta magazynu usługi Azure Key Vault"
description: "Klucze konta magazynu przedstawić seemless integrację usługi Azure Key Vault i klucza dostępu na podstawie konta magazynu Azure."
ms.topic: article
services: key-vault
ms.service: key-vault
author: BrucePerlerMS
ms.author: bruceper
manager: mbaldwin
ms.date: 07/25/2017
ms.openlocfilehash: 3148088c88236c64e089fd25c98eb8ac7cdcbfea
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
# <a name="azure-key-vault-storage-account-keys"></a>Klucze konta magazynu usługi Azure Key Vault

Przed magazynu kluczy konta Azure klucz magazynu deweloperzy mają zarządzać własne klucze konta magazynu Azure (ASA) i Obróć je ręcznie lub za pomocą narzędzie automatyzacji. Teraz, klucze konta magazynu kluczy w magazynie są zaimplementowane jako [kluczy tajnych Key Vault](https://docs.microsoft.com/rest/api/keyvault/about-keys--secrets-and-certificates#BKMK_WorkingWithSecrets) do uwierzytelniania przy użyciu konta magazynu Azure. 

Funkcja klucza ASA zarządza tajny obrotu i eliminuje to potrzebę bezpośredniego kontaktu z kluczem ASA oferując dostępu sygnatur dostępu Współdzielonego jako metody. 

Aby uzyskać więcej ogólnych informacji o kontach magazynu Azure, zobacz [kont magazynu Azure o](https://docs.microsoft.com/azure/storage/storage-create-storage-account).

## <a name="supporting-interfaces"></a>Obsługa interfejsów

Funkcja klucze konta magazynu Azure jest początkowo dostępna za pośrednictwem pozostałe .NET / interfejsy C# i programu PowerShell. Aby uzyskać więcej informacji, zobacz [z informacjami o kluczach magazynu](https://docs.microsoft.com/azure/key-vault/).


## <a name="storage-account-keys-behavior"></a>Zachowanie klucze konta magazynu

### <a name="what-key-vault-manages"></a>Zarządza Magazyn kluczy

Magazyn kluczy wykonuje wiele funkcji zarządzania wewnętrznego w Twoim imieniu używania kluczy konta magazynu.

1. Usługa Azure Key Vault zarządza kluczy dla konta magazynu Azure (ASA). 
    - Wewnętrznie usługi Azure Key Vault można wyświetlić listę kluczy (synchronizacja) z kontem magazynu platformy Azure.  
    - Usługa Azure Key Vault generuje (obraca) okresowo kluczy. 
    - Wartości klucza nigdy nie są zwracane w odpowiedzi do wywołującego. 
    - Usługa Azure Key Vault zarządza klucze konta magazynu i klasycznych kont magazynu. 
2. Usługa Azure Key Vault pozwala, właściciel magazynu/obiektu, do tworzenia definicji SAS (konta lub sygnatury dostępu Współdzielonego usługi). 
    - Wartość SAS, utworzone za pomocą definicji SAS, jest zwracana jako klucza tajnego za pośrednictwem ścieżka identyfikatora URI REST. Aby uzyskać więcej informacji, zobacz [operacje konta magazynu usługi Azure Key Vault](https://docs.microsoft.com/rest/api/keyvault/storage-account-key-operations).

### <a name="naming-guidance"></a>Wskazówki dotyczące nazewnictwa

Nazwy kont usługi Magazyn muszą mieć długość od 3 do 24 znaków i mogą zawierać tylko cyfry i małe litery.  
 
Nazwa definicji SAS musi być 1 102 znaków długości i zawierać tylko 0-9, a-z, A-Z.

## <a name="developer-experience"></a>Środowisko dewelopera 

### <a name="before-azure-key-vault-storage-keys"></a>Przed usługi Azure Key Vault magazynu kluczy 

Deweloperzy umożliwia należy wykonać następujące rozwiązania kluczem konta magazynu można uzyskać dostępu do magazynu Azure. 
 
 ```
//create storage account using connection string containing account name 
// and the storage key 

var storageAccount = CloudStorageAccount.Parse(CloudConfigurationManager.GetSetting("StorageConnectionString"));
var blobClient = storageAccount.CreateCloudBlobClient();
 ```
 
### <a name="after-azure-key-vault-storage-keys"></a>Po usługi Azure Key Vault magazynu kluczy 

```
//Please make sure to set storage permissions appropriately on your key vault
Set-AzureRmKeyVaultAccessPolicy -VaultName 'yourVault' -ObjectId yourObjectId -PermissionsToStorage all

//Use PowerShell command to get Secret URI 

Set-AzureKeyVaultManagedStorageSasDefinition -Service Blob -ResourceType Container,Service -VaultName yourKV  
-AccountName msak01 -Name blobsas1 -Protocol HttpsOnly -ValidityPeriod ([System.Timespan]::FromDays(1)) -Permission Read,List

//Get SAS token from Key Vault

var secret = await kv.GetSecretAsync("SecretUri");

// Create new storage credentials using the SAS token. 

var accountSasCredential = new StorageCredentials(secret.Value); 

// Use credentials and the Blob storage endpoint to create a new Blob service client. 

var accountWithSas = new CloudStorageAccount(accountSasCredential, new Uri ("https://myaccount.blob.core.windows.net/"), null, null, null); 

var blobClientWithSas = accountWithSas.CreateCloudBlobClient(); 
 
// If SAS token is about to expire then Get sasToken again from Key Vault and update it.

accountSasCredential.UpdateSASToken(sasToken);

  ```
 
 ### <a name="developer-best-practices"></a>Najlepsze praktyki Developer 

- Zezwalaj tylko na Key Vault w celu zarządzanie kluczami ASA. Nie należy próbować Zarządzanie samodzielnie, będzie zakłócać procesów magazynu kluczy. 
- Nie zezwalaj ASA klucze mają być zarządzane przez więcej niż jeden obiekt magazynu kluczy. 
- Jeśli musisz ręcznie wygenerować ponownie klucze ASA, zaleca się Generuj je za pomocą usługi Key Vault. 

## <a name="getting-started"></a>Wprowadzenie

### <a name="setup-for-role-based-access-control-rbac-permissions"></a>Ustawienia dla uprawnień kontroli dostępu opartej na rolach

Magazyn kluczy wymaga uprawnień do *listy* i *ponownie wygenerować* kluczy dla konta magazynu. Skonfiguruj te uprawnienia, wykonując następujące czynności:

- Pobrania ObjectId magazynu kluczy: 

    `Get-AzureRmADServicePrincipal -SearchString "AzureKeyVault"`

- Przypisz roli operatora klucza magazynu Azure klucza magazynu tożsamości: 

    `New-AzureRmRoleAssignment -ObjectId <objectId of AzureKeyVault from previous command> -RoleDefinitionName 'Storage Account Key Operator Service Role' -Scope '<azure resource id of storage account>'`

    >[!NOTE]
    > Dla typu konta klasycznego, ustaw dla parametru roli *"Klasycznego magazynu konta klucza usługi roli operatora"*.

### <a name="storage-account-onboarding"></a>Dołączanie konta magazynu 

Przykład: jako właściciel obiektu usługi Key Vault dodawany obiekt konta magazynu do użytkownika usługa Azure Key Vault dołączeniu konto magazynu.

Podczas dołączania, Key Vault musi sprawdzić, czy tożsamość konta dołączania ma uprawnienia do *listy* i *ponownie wygenerować* magazynu kluczy. Aby można było zweryfikować te uprawnienia, Key Vault pobiera OBO (imieniu z) tokenu z usługi uwierzytelniania, odbiorców, ustaw do usługi Azure Resource Manager i sprawia, że *listy* klucza wywołanie usługi Magazyn Azure. Jeśli *listy* wywołanie zakończy się niepowodzeniem, Key Vault Tworzenie obiektu zakończy się niepowodzeniem z kodem stanu HTTP z *zabroniony*. Klucze wymienione w ten sposób są buforowane z magazynem jednostek magazynu kluczy. 

Magazyn kluczy należy sprawdzić, czy tożsamość *ponownie wygenerować* uprawnienia przed jego przejąć prawo własności ponowne generowanie kluczy. Aby sprawdzić, czy tożsamość, za pomocą tokenu OBO, jak również tożsamości firm pierwszej usługi Key Vault ma tych uprawnień:

- Magazyn kluczy wymieniono uprawnienia RBAC zasobu konta magazynu.
- Magazyn kluczy sprawdza poprawność odpowiedzi, używając wyrażenia regularnego dopasowanie działania i z systemem innym niż działania. 

Znajdź przykłady obsługi na [magazyn kluczy - zarządzane przykłady klucze konta magazynu](https://github.com/Azure/azure-sdk-for-net/blob/psSdkJson6/src/SDKs/KeyVault/dataPlane/Microsoft.Azure.KeyVault.Samples/samples/HelloKeyVault/Program.cs#L167).

Jeśli nie ma tożsamość *ponownie wygenerować* uprawnienia lub jeśli nie ma usługi Key Vault pierwszej strony tożsamości *listy* lub *ponownie wygenerować* uprawnienia, a następnie procesu dołączania żądanie nie powiedzie się, zwracając kod błędu odpowiednie i wiadomości. 

OBO token działa tylko, gdy używasz firmy, aplikacje klienckie natywnego programu PowerShell lub interfejsu wiersza polecenia.

## <a name="other-applications"></a>Inne aplikacje

- Tokeny sygnatury dostępu Współdzielonego, tworzony przy użyciu kluczy konta magazynu usługi Key Vault, zapewniają bardziej kontroli dostępu do konta magazynu platformy Azure. Aby uzyskać więcej informacji, zobacz [używanie sygnatury dostępu współdzielonego](https://docs.microsoft.com/azure/storage/storage-dotnet-shared-access-signature-part-1).

## <a name="see-also"></a>Zobacz też

- [Informacje o kluczach, wpisach tajnych i certyfikatach](https://docs.microsoft.com/rest/api/keyvault/)
- [Blog zespołu magazyn kluczy](https://blogs.technet.microsoft.com/kv/)
