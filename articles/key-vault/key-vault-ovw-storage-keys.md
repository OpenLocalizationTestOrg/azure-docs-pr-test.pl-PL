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
# <a name="azure-key-vault-storage-account-keys"></a><span data-ttu-id="3e090-103">Klucze konta magazynu usługi Azure Key Vault</span><span class="sxs-lookup"><span data-stu-id="3e090-103">Azure Key Vault Storage Account Keys</span></span>

<span data-ttu-id="3e090-104">Przed magazynu kluczy konta Azure klucz magazynu deweloperzy mają zarządzać własne klucze konta magazynu Azure (ASA) i Obróć je ręcznie lub za pomocą narzędzie automatyzacji.</span><span class="sxs-lookup"><span data-stu-id="3e090-104">Before Azure Key Vault Storage Account Keys, developers had to manage their own Azure Storage Account (ASA) keys and rotate them manually or through an external automation.</span></span> <span data-ttu-id="3e090-105">Teraz, klucze konta magazynu kluczy w magazynie są zaimplementowane jako [kluczy tajnych Key Vault](https://docs.microsoft.com/rest/api/keyvault/about-keys--secrets-and-certificates#BKMK_WorkingWithSecrets) do uwierzytelniania przy użyciu konta magazynu Azure.</span><span class="sxs-lookup"><span data-stu-id="3e090-105">Now, Key Vault Storage Account Keys are implemented as [Key Vault secrets](https://docs.microsoft.com/rest/api/keyvault/about-keys--secrets-and-certificates#BKMK_WorkingWithSecrets) for authenticating with an Azure Storage Account.</span></span> 

<span data-ttu-id="3e090-106">Funkcja klucza ASA zarządza tajny obrotu i eliminuje to potrzebę bezpośredniego kontaktu z kluczem ASA oferując dostępu sygnatur dostępu Współdzielonego jako metody.</span><span class="sxs-lookup"><span data-stu-id="3e090-106">The ASA key feature manages secret rotation for you and removes the need for your direct contact with an ASA key by offering Shared Access Signatures (SAS) as a method.</span></span> 

<span data-ttu-id="3e090-107">Aby uzyskać więcej ogólnych informacji o kontach magazynu Azure, zobacz [kont magazynu Azure o](https://docs.microsoft.com/azure/storage/storage-create-storage-account).</span><span class="sxs-lookup"><span data-stu-id="3e090-107">For more general information on Azure Storage Accounts, see [About Azure storage accounts](https://docs.microsoft.com/azure/storage/storage-create-storage-account).</span></span>

## <a name="supporting-interfaces"></a><span data-ttu-id="3e090-108">Obsługa interfejsów</span><span class="sxs-lookup"><span data-stu-id="3e090-108">Supporting interfaces</span></span>

<span data-ttu-id="3e090-109">Funkcja klucze konta magazynu Azure jest początkowo dostępna za pośrednictwem pozostałe .NET / interfejsy C# i programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="3e090-109">The Azure Storage Account keys feature is initially available through the REST, .NET/C# and PowerShell interfaces.</span></span> <span data-ttu-id="3e090-110">Aby uzyskać więcej informacji, zobacz [z informacjami o kluczach magazynu](https://docs.microsoft.com/azure/key-vault/).</span><span class="sxs-lookup"><span data-stu-id="3e090-110">For more information, see [Key Vault Reference](https://docs.microsoft.com/azure/key-vault/).</span></span>


## <a name="storage-account-keys-behavior"></a><span data-ttu-id="3e090-111">Zachowanie klucze konta magazynu</span><span class="sxs-lookup"><span data-stu-id="3e090-111">Storage account keys behavior</span></span>

### <a name="what-key-vault-manages"></a><span data-ttu-id="3e090-112">Zarządza Magazyn kluczy</span><span class="sxs-lookup"><span data-stu-id="3e090-112">What Key Vault manages</span></span>

<span data-ttu-id="3e090-113">Magazyn kluczy wykonuje wiele funkcji zarządzania wewnętrznego w Twoim imieniu używania kluczy konta magazynu.</span><span class="sxs-lookup"><span data-stu-id="3e090-113">Key Vault performs several internal management functions on your behalf when you use Storage Account Keys.</span></span>

1. <span data-ttu-id="3e090-114">Usługa Azure Key Vault zarządza kluczy dla konta magazynu Azure (ASA).</span><span class="sxs-lookup"><span data-stu-id="3e090-114">Azure Key Vault manages keys of an Azure Storage Account (ASA).</span></span> 
    - <span data-ttu-id="3e090-115">Wewnętrznie usługi Azure Key Vault można wyświetlić listę kluczy (synchronizacja) z kontem magazynu platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="3e090-115">Internally, Azure Key Vault can list (sync) keys with an Azure Storage Account.</span></span>  
    - <span data-ttu-id="3e090-116">Usługa Azure Key Vault generuje (obraca) okresowo kluczy.</span><span class="sxs-lookup"><span data-stu-id="3e090-116">Azure Key Vault regenerates (rotates) the keys periodically.</span></span> 
    - <span data-ttu-id="3e090-117">Wartości klucza nigdy nie są zwracane w odpowiedzi do wywołującego.</span><span class="sxs-lookup"><span data-stu-id="3e090-117">Key values are never returned in response to caller.</span></span> 
    - <span data-ttu-id="3e090-118">Usługa Azure Key Vault zarządza klucze konta magazynu i klasycznych kont magazynu.</span><span class="sxs-lookup"><span data-stu-id="3e090-118">Azure Key Vault manages keys of both Storage Accounts and Classic Storage Accounts.</span></span> 
2. <span data-ttu-id="3e090-119">Usługa Azure Key Vault pozwala, właściciel magazynu/obiektu, do tworzenia definicji SAS (konta lub sygnatury dostępu Współdzielonego usługi).</span><span class="sxs-lookup"><span data-stu-id="3e090-119">Azure Key Vault allows you, the vault/object owner, to create SAS (account or service SAS) definitions.</span></span> 
    - <span data-ttu-id="3e090-120">Wartość SAS, utworzone za pomocą definicji SAS, jest zwracana jako klucza tajnego za pośrednictwem ścieżka identyfikatora URI REST.</span><span class="sxs-lookup"><span data-stu-id="3e090-120">The SAS value, created using SAS definition, is returned as a secret via the REST URI path.</span></span> <span data-ttu-id="3e090-121">Aby uzyskać więcej informacji, zobacz [operacje konta magazynu usługi Azure Key Vault](https://docs.microsoft.com/rest/api/keyvault/storage-account-key-operations).</span><span class="sxs-lookup"><span data-stu-id="3e090-121">For more information, see [Azure Key Vault storage account operations](https://docs.microsoft.com/rest/api/keyvault/storage-account-key-operations).</span></span>

### <a name="naming-guidance"></a><span data-ttu-id="3e090-122">Wskazówki dotyczące nazewnictwa</span><span class="sxs-lookup"><span data-stu-id="3e090-122">Naming guidance</span></span>

<span data-ttu-id="3e090-123">Nazwy kont usługi Magazyn muszą mieć długość od 3 do 24 znaków i mogą zawierać tylko cyfry i małe litery.</span><span class="sxs-lookup"><span data-stu-id="3e090-123">Storage account names must be between 3 and 24 characters in length and may contain numbers and lowercase letters only.</span></span>  
 
<span data-ttu-id="3e090-124">Nazwa definicji SAS musi być 1 102 znaków długości i zawierać tylko 0-9, a-z, A-Z.</span><span class="sxs-lookup"><span data-stu-id="3e090-124">A SAS definition name must be 1-102 characters in length containing only 0-9, a-z, A-Z.</span></span>

## <a name="developer-experience"></a><span data-ttu-id="3e090-125">Środowisko dewelopera</span><span class="sxs-lookup"><span data-stu-id="3e090-125">Developer experience</span></span> 

### <a name="before-azure-key-vault-storage-keys"></a><span data-ttu-id="3e090-126">Przed usługi Azure Key Vault magazynu kluczy</span><span class="sxs-lookup"><span data-stu-id="3e090-126">Before Azure Key Vault Storage Keys</span></span> 

<span data-ttu-id="3e090-127">Deweloperzy umożliwia należy wykonać następujące rozwiązania kluczem konta magazynu można uzyskać dostępu do magazynu Azure.</span><span class="sxs-lookup"><span data-stu-id="3e090-127">Developers used to need to do the following practices with a storage account key to get access to Azure storage.</span></span> 
 
 ```
//create storage account using connection string containing account name 
// and the storage key 

var storageAccount = CloudStorageAccount.Parse(CloudConfigurationManager.GetSetting("StorageConnectionString"));
var blobClient = storageAccount.CreateCloudBlobClient();
 ```
 
### <a name="after-azure-key-vault-storage-keys"></a><span data-ttu-id="3e090-128">Po usługi Azure Key Vault magazynu kluczy</span><span class="sxs-lookup"><span data-stu-id="3e090-128">After Azure Key Vault Storage Keys</span></span> 

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
 
 ### <a name="developer-best-practices"></a><span data-ttu-id="3e090-129">Najlepsze praktyki Developer</span><span class="sxs-lookup"><span data-stu-id="3e090-129">Developer best practices</span></span> 

- <span data-ttu-id="3e090-130">Zezwalaj tylko na Key Vault w celu zarządzanie kluczami ASA.</span><span class="sxs-lookup"><span data-stu-id="3e090-130">Only allow Key Vault to manage your ASA keys.</span></span> <span data-ttu-id="3e090-131">Nie należy próbować Zarządzanie samodzielnie, będzie zakłócać procesów magazynu kluczy.</span><span class="sxs-lookup"><span data-stu-id="3e090-131">Do not attempt to manage them yourself, you will interfere with Key Vault's processes.</span></span> 
- <span data-ttu-id="3e090-132">Nie zezwalaj ASA klucze mają być zarządzane przez więcej niż jeden obiekt magazynu kluczy.</span><span class="sxs-lookup"><span data-stu-id="3e090-132">Do not allow ASA keys to be managed by more than one Key Vault object.</span></span> 
- <span data-ttu-id="3e090-133">Jeśli musisz ręcznie wygenerować ponownie klucze ASA, zaleca się Generuj je za pomocą usługi Key Vault.</span><span class="sxs-lookup"><span data-stu-id="3e090-133">If you need to manually regenerate your ASA keys, we recommend that you regenerate them via Key Vault.</span></span> 

## <a name="getting-started"></a><span data-ttu-id="3e090-134">Wprowadzenie</span><span class="sxs-lookup"><span data-stu-id="3e090-134">Getting started</span></span>

### <a name="setup-for-role-based-access-control-rbac-permissions"></a><span data-ttu-id="3e090-135">Ustawienia dla uprawnień kontroli dostępu opartej na rolach</span><span class="sxs-lookup"><span data-stu-id="3e090-135">Setup for role-based access control (RBAC) permissions</span></span>

<span data-ttu-id="3e090-136">Magazyn kluczy wymaga uprawnień do *listy* i *ponownie wygenerować* kluczy dla konta magazynu.</span><span class="sxs-lookup"><span data-stu-id="3e090-136">Key Vault needs permissions to *list* and *regenerate* keys for a storage account.</span></span> <span data-ttu-id="3e090-137">Skonfiguruj te uprawnienia, wykonując następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="3e090-137">Set up these permissions using the following steps:</span></span>

- <span data-ttu-id="3e090-138">Pobrania ObjectId magazynu kluczy:</span><span class="sxs-lookup"><span data-stu-id="3e090-138">Get ObjectId of Key Vault:</span></span> 

    `Get-AzureRmADServicePrincipal -SearchString "AzureKeyVault"`

- <span data-ttu-id="3e090-139">Przypisz roli operatora klucza magazynu Azure klucza magazynu tożsamości:</span><span class="sxs-lookup"><span data-stu-id="3e090-139">Assign Storage Key Operator role to Azure Key Vault Identity:</span></span> 

    `New-AzureRmRoleAssignment -ObjectId <objectId of AzureKeyVault from previous command> -RoleDefinitionName 'Storage Account Key Operator Service Role' -Scope '<azure resource id of storage account>'`

    >[!NOTE]
    > <span data-ttu-id="3e090-140">Dla typu konta klasycznego, ustaw dla parametru roli *"Klasycznego magazynu konta klucza usługi roli operatora"*.</span><span class="sxs-lookup"><span data-stu-id="3e090-140">For a classic account type, set the role parameter to *"Classic Storage Account Key Operator Service Role"*.</span></span>

### <a name="storage-account-onboarding"></a><span data-ttu-id="3e090-141">Dołączanie konta magazynu</span><span class="sxs-lookup"><span data-stu-id="3e090-141">Storage account onboarding</span></span> 

<span data-ttu-id="3e090-142">Przykład: jako właściciel obiektu usługi Key Vault dodawany obiekt konta magazynu do użytkownika usługa Azure Key Vault dołączeniu konto magazynu.</span><span class="sxs-lookup"><span data-stu-id="3e090-142">Example: As a Key Vault object owner you add a storage account object to your Azure Key Vault to onboard a storage account.</span></span>

<span data-ttu-id="3e090-143">Podczas dołączania, Key Vault musi sprawdzić, czy tożsamość konta dołączania ma uprawnienia do *listy* i *ponownie wygenerować* magazynu kluczy.</span><span class="sxs-lookup"><span data-stu-id="3e090-143">During onboarding, Key Vault needs to verify that the identity of the onboarding account has permissions to *list* and to *regenerate* storage keys.</span></span> <span data-ttu-id="3e090-144">Aby można było zweryfikować te uprawnienia, Key Vault pobiera OBO (imieniu z) tokenu z usługi uwierzytelniania, odbiorców, ustaw do usługi Azure Resource Manager i sprawia, że *listy* klucza wywołanie usługi Magazyn Azure.</span><span class="sxs-lookup"><span data-stu-id="3e090-144">In order to verify these permissions, Key Vault gets an OBO (On Behalf Of) token from the authentication service, audience set to Azure Resource Manager, and makes a *list* key call to the Azure Storage service.</span></span> <span data-ttu-id="3e090-145">Jeśli *listy* wywołanie zakończy się niepowodzeniem, Key Vault Tworzenie obiektu zakończy się niepowodzeniem z kodem stanu HTTP z *zabroniony*.</span><span class="sxs-lookup"><span data-stu-id="3e090-145">If the *list* call fails, the Key Vault object creation fails with a HTTP status code of *Forbidden*.</span></span> <span data-ttu-id="3e090-146">Klucze wymienione w ten sposób są buforowane z magazynem jednostek magazynu kluczy.</span><span class="sxs-lookup"><span data-stu-id="3e090-146">The keys listed in this fashion are cached with your key vault entity storage.</span></span> 

<span data-ttu-id="3e090-147">Magazyn kluczy należy sprawdzić, czy tożsamość *ponownie wygenerować* uprawnienia przed jego przejąć prawo własności ponowne generowanie kluczy.</span><span class="sxs-lookup"><span data-stu-id="3e090-147">Key Vault must verify that the identity has *regenerate* permissions before it can take ownership of regenerating your keys.</span></span> <span data-ttu-id="3e090-148">Aby sprawdzić, czy tożsamość, za pomocą tokenu OBO, jak również tożsamości firm pierwszej usługi Key Vault ma tych uprawnień:</span><span class="sxs-lookup"><span data-stu-id="3e090-148">To verify that the identity, via OBO token, as well as the Key Vault first party identity has these permissions:</span></span>

- <span data-ttu-id="3e090-149">Magazyn kluczy wymieniono uprawnienia RBAC zasobu konta magazynu.</span><span class="sxs-lookup"><span data-stu-id="3e090-149">Key Vault lists RBAC permissions on the storage account resource.</span></span>
- <span data-ttu-id="3e090-150">Magazyn kluczy sprawdza poprawność odpowiedzi, używając wyrażenia regularnego dopasowanie działania i z systemem innym niż działania.</span><span class="sxs-lookup"><span data-stu-id="3e090-150">Key Vault validates the response via regular expression matching of actions and non-actions.</span></span> 

<span data-ttu-id="3e090-151">Znajdź przykłady obsługi na [magazyn kluczy - zarządzane przykłady klucze konta magazynu](https://github.com/Azure/azure-sdk-for-net/blob/psSdkJson6/src/SDKs/KeyVault/dataPlane/Microsoft.Azure.KeyVault.Samples/samples/HelloKeyVault/Program.cs#L167).</span><span class="sxs-lookup"><span data-stu-id="3e090-151">Find some supporting examples at [Key Vault - Managed Storage Account Keys Samples](https://github.com/Azure/azure-sdk-for-net/blob/psSdkJson6/src/SDKs/KeyVault/dataPlane/Microsoft.Azure.KeyVault.Samples/samples/HelloKeyVault/Program.cs#L167).</span></span>

<span data-ttu-id="3e090-152">Jeśli nie ma tożsamość *ponownie wygenerować* uprawnienia lub jeśli nie ma usługi Key Vault pierwszej strony tożsamości *listy* lub *ponownie wygenerować* uprawnienia, a następnie procesu dołączania żądanie nie powiedzie się, zwracając kod błędu odpowiednie i wiadomości.</span><span class="sxs-lookup"><span data-stu-id="3e090-152">If the identity does not have *regenerate* permissions or if Key Vault's first party identity doesn’t have *list* or *regenerate* permission, then the onboarding request fails returning an appropriate error code and message.</span></span> 

<span data-ttu-id="3e090-153">OBO token działa tylko, gdy używasz firmy, aplikacje klienckie natywnego programu PowerShell lub interfejsu wiersza polecenia.</span><span class="sxs-lookup"><span data-stu-id="3e090-153">The OBO token will only work when you use first-party, native client applications of either PowerShell or CLI.</span></span>

## <a name="other-applications"></a><span data-ttu-id="3e090-154">Inne aplikacje</span><span class="sxs-lookup"><span data-stu-id="3e090-154">Other applications</span></span>

- <span data-ttu-id="3e090-155">Tokeny sygnatury dostępu Współdzielonego, tworzony przy użyciu kluczy konta magazynu usługi Key Vault, zapewniają bardziej kontroli dostępu do konta magazynu platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="3e090-155">SAS tokens, constructed using Key Vault storage account keys, provide even more controlled access to an Azure storage account.</span></span> <span data-ttu-id="3e090-156">Aby uzyskać więcej informacji, zobacz [używanie sygnatury dostępu współdzielonego](https://docs.microsoft.com/azure/storage/storage-dotnet-shared-access-signature-part-1).</span><span class="sxs-lookup"><span data-stu-id="3e090-156">For more information, see [Using shared access signatures](https://docs.microsoft.com/azure/storage/storage-dotnet-shared-access-signature-part-1).</span></span>

## <a name="see-also"></a><span data-ttu-id="3e090-157">Zobacz też</span><span class="sxs-lookup"><span data-stu-id="3e090-157">See also</span></span>

- [<span data-ttu-id="3e090-158">Informacje o kluczach, wpisach tajnych i certyfikatach</span><span class="sxs-lookup"><span data-stu-id="3e090-158">About keys, secrets, and certificates</span></span>](https://docs.microsoft.com/rest/api/keyvault/)
- [<span data-ttu-id="3e090-159">Blog zespołu magazyn kluczy</span><span class="sxs-lookup"><span data-stu-id="3e090-159">Key Vault Team Blog</span></span>](https://blogs.technet.microsoft.com/kv/)
