---
ms.assetid: 
title: aaaAzure klucze konta magazynu kluczy w magazynie
description: "Klucze konta magazynu Podaj seemless integrację usługi Azure Key Vault tooAzure klucza dostępu na podstawie konta magazynu."
ms.topic: article
services: key-vault
ms.service: key-vault
author: BrucePerlerMS
ms.author: bruceper
manager: mbaldwin
ms.date: 07/25/2017
ms.openlocfilehash: becdf97798a08164c48d3a7a14aea6ca54085c9a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-key-vault-storage-account-keys"></a>Klucze konta magazynu usługi Azure Key Vault

Przed magazynu kluczy konta Azure klucz magazynu deweloperzy miał toomanage własne klucze konta magazynu Azure (ASA) i Obróć je ręcznie lub za pomocą narzędzie automatyzacji. Teraz, klucze konta magazynu kluczy w magazynie są zaimplementowane jako [kluczy tajnych Key Vault](https://docs.microsoft.com/rest/api/keyvault/about-keys--secrets-and-certificates#BKMK_WorkingWithSecrets) do uwierzytelniania przy użyciu konta magazynu Azure. 

Funkcja klucza ASA Hello zarządza tajny obrotu i eliminuje potrzebę hello bezpośredni kontakt z kluczem ASA, oferując dostępu sygnatur dostępu Współdzielonego jako metody. 

Aby uzyskać więcej ogólnych informacji o kontach magazynu Azure, zobacz [kont magazynu Azure o](https://docs.microsoft.com/azure/storage/storage-create-storage-account).

## <a name="supporting-interfaces"></a>Obsługa interfejsów

Witaj funkcji klucze konta magazynu Azure jest początkowo dostępna za pośrednictwem hello REST, .NET / interfejsy C# i programu PowerShell. Aby uzyskać więcej informacji, zobacz [z informacjami o kluczach magazynu](https://docs.microsoft.com/azure/key-vault/).


## <a name="storage-account-keys-behavior"></a>Zachowanie klucze konta magazynu

### <a name="what-key-vault-manages"></a>Zarządza Magazyn kluczy

Magazyn kluczy wykonuje wiele funkcji zarządzania wewnętrznego w Twoim imieniu używania kluczy konta magazynu.

1. Usługa Azure Key Vault zarządza kluczy dla konta magazynu Azure (ASA). 
    - Wewnętrznie usługi Azure Key Vault można wyświetlić listę kluczy (synchronizacja) z kontem magazynu platformy Azure.  
    - Usługa Azure Key Vault generuje (obraca) hello okresowo kluczy. 
    - Wartości klucza nigdy nie są zwracane w toocaller odpowiedzi. 
    - Usługa Azure Key Vault zarządza klucze konta magazynu i klasycznych kont magazynu. 
2. Usługa Azure Key Vault umożliwia możesz właściciela magazynu/obiektu hello, toocreate definicje SAS (konta lub sygnatury dostępu Współdzielonego usługi). 
    - Hello wartość SAS, utworzone za pomocą definicji SAS, jest zwracana jako klucza tajnego za pośrednictwem ścieżka identyfikatora URI REST hello. Aby uzyskać więcej informacji, zobacz [operacje konta magazynu usługi Azure Key Vault](https://docs.microsoft.com/rest/api/keyvault/storage-account-key-operations).

### <a name="naming-guidance"></a>Wskazówki dotyczące nazewnictwa

Nazwy kont usługi Magazyn muszą mieć długość od 3 do 24 znaków i mogą zawierać tylko cyfry i małe litery.  
 
Nazwa definicji SAS musi być 1 102 znaków długości i zawierać tylko 0-9, a-z, A-Z.

## <a name="developer-experience"></a>Środowisko dewelopera 

### <a name="before-azure-key-vault-storage-keys"></a>Przed usługi Azure Key Vault magazynu kluczy 

Deweloperzy używane hello toodo tooneed wskazówek z magazynu tooAzure dostępu tooget klucza konta magazynu. 
 
 ```
//create storage account using connection string containing account name 
// and hello storage key 

var storageAccount = CloudStorageAccount.Parse(CloudConfigurationManager.GetSetting("StorageConnectionString"));
var blobClient = storageAccount.CreateCloudBlobClient();
 ```
 
### <a name="after-azure-key-vault-storage-keys"></a>Po usługi Azure Key Vault magazynu kluczy 

```
//Please make sure tooset storage permissions appropriately on your key vault
Set-AzureRmKeyVaultAccessPolicy -VaultName 'yourVault' -ObjectId yourObjectId -PermissionsToStorage all

//Use PowerShell command tooget Secret URI 

Set-AzureKeyVaultManagedStorageSasDefinition -Service Blob -ResourceType Container,Service -VaultName yourKV  
-AccountName msak01 -Name blobsas1 -Protocol HttpsOnly -ValidityPeriod ([System.Timespan]::FromDays(1)) -Permission Read,List

//Get SAS token from Key Vault

var secret = await kv.GetSecretAsync("SecretUri");

// Create new storage credentials using hello SAS token. 

var accountSasCredential = new StorageCredentials(secret.Value); 

// Use credentials and hello Blob storage endpoint toocreate a new Blob service client. 

var accountWithSas = new CloudStorageAccount(accountSasCredential, new Uri ("https://myaccount.blob.core.windows.net/"), null, null, null); 

var blobClientWithSas = accountWithSas.CreateCloudBlobClient(); 
 
// If SAS token is about tooexpire then Get sasToken again from Key Vault and update it.

accountSasCredential.UpdateSASToken(sasToken);

  ```
 
 ### <a name="developer-best-practices"></a>Najlepsze praktyki Developer 

- Zezwalaj na tylko toomanage Key Vault klucze ASA. Nie należy podejmować toomanage je samodzielnie, będzie kolidować z procesami magazynu kluczy. 
- Nie zezwalaj toobe klucze ASA zarządzane przez więcej niż jeden obiekt magazynu kluczy. 
- Jeśli potrzebujesz toomanually ponownie wygenerować klucze ASA, zaleca się Generuj je za pomocą usługi Key Vault. 

## <a name="getting-started"></a>Wprowadzenie

### <a name="setup-for-role-based-access-control-rbac-permissions"></a>Ustawienia dla uprawnień kontroli dostępu opartej na rolach

Magazyn kluczy wymaga uprawnień zbyt*listy* i *ponownie wygenerować* kluczy dla konta magazynu. Skonfiguruj te uprawnienia za pomocą hello następujące kroki:

- Pobrania ObjectId magazynu kluczy: 

    `Get-AzureRmADServicePrincipal -SearchString "AzureKeyVault"`

- Przypisz tooAzure roli operatora klucza magazynu klucz magazynu tożsamości: 

    `New-AzureRmRoleAssignment -ObjectId <objectId of AzureKeyVault from previous command> -RoleDefinitionName 'Storage Account Key Operator Service Role' -Scope '<azure resource id of storage account>'`

    >[!NOTE]
    > Dla typu konta klasycznego, ustaw parametr roli hello zbyt*"Klasycznego magazynu konta klucza usługi roli operatora"*.

### <a name="storage-account-onboarding"></a>Dołączanie konta magazynu 

Przykład: Jako właściciel obiektu magazynu kluczy, Dodaj magazynu konta tooonboard usługi Azure Key Vault tooyour obiektu konta magazynu.

Podczas dołączania, Key Vault musi tooverify hello tożsamość konta dołączania hello zbyt ma uprawnienia*listy* i zbyt*ponownie wygenerować* magazynu kluczy. W celu tooverify tych uprawnień, Key Vault pobiera OBO (imieniu z) tokenu z usługi uwierzytelniania hello, odbiorców ustawić tooAzure Resource Manager i sprawia, że *listy* klucza usługi Azure Storage toohello wywołania. Jeśli hello *listy* wywołać kończy się niepowodzeniem, hello Key Vault Tworzenie obiektu zakończy się niepowodzeniem z kodem stanu HTTP z *zabroniony*. klawisze Hello w ten sposób są buforowane z magazynem jednostek magazynu kluczy. 

Magazyn kluczy musi sprawdzić, czy tożsamość hello *ponownie wygenerować* uprawnienia przed jego przejąć prawo własności ponowne generowanie kluczy. tooverify, który hello tożsamości za pomocą tokenu OBO, a także hello Key Vault pierwszej strony tożsamości ma te uprawnienia:

- Magazyn kluczy wymieniono uprawnienia RBAC hello magazynu konta zasobu.
- Magazyn kluczy weryfikuje hello odpowiedzi przez Dopasowywanie wyrażeń regularnych z systemem innym niż akcji i akcje. 

Znajdź przykłady obsługi na [magazyn kluczy - zarządzane przykłady klucze konta magazynu](https://github.com/Azure/azure-sdk-for-net/blob/psSdkJson6/src/SDKs/KeyVault/dataPlane/Microsoft.Azure.KeyVault.Samples/samples/HelloKeyVault/Program.cs#L167).

Jeśli tożsamość hello nie ma *ponownie wygenerować* uprawnienia lub jeśli nie ma usługi Key Vault pierwszy tożsamości firm *listy* lub *ponownie wygenerować* uprawnienia, a następnie dołączania hello żądanie nie powiedzie się, zwracając kod błędu odpowiednie i komunikatu. 

Hello OBO token działa tylko, gdy używasz firmy, aplikacje klienckie natywnego programu PowerShell lub interfejsu wiersza polecenia.

## <a name="other-applications"></a>Inne aplikacje

- Tokeny sygnatury dostępu Współdzielonego, tworzony przy użyciu kluczy konta magazynu usługi Key Vault, zapewniają większą kontrolą dostępu tooan kontem magazynu platformy Azure. Aby uzyskać więcej informacji, zobacz [używanie sygnatury dostępu współdzielonego](https://docs.microsoft.com/azure/storage/storage-dotnet-shared-access-signature-part-1).

## <a name="see-also"></a>Zobacz też

- [Informacje o kluczach, wpisach tajnych i certyfikatach](https://docs.microsoft.com/rest/api/keyvault/)
- [Blog zespołu magazyn kluczy](https://blogs.technet.microsoft.com/kv/)
