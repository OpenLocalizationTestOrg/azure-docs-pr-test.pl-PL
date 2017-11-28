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
# <a name="azure-key-vault-storage-account-keys"></a><span data-ttu-id="fe461-103">Klucze konta magazynu usługi Azure Key Vault</span><span class="sxs-lookup"><span data-stu-id="fe461-103">Azure Key Vault Storage Account Keys</span></span>

<span data-ttu-id="fe461-104">Przed magazynu kluczy konta Azure klucz magazynu deweloperzy miał toomanage własne klucze konta magazynu Azure (ASA) i Obróć je ręcznie lub za pomocą narzędzie automatyzacji.</span><span class="sxs-lookup"><span data-stu-id="fe461-104">Before Azure Key Vault Storage Account Keys, developers had toomanage their own Azure Storage Account (ASA) keys and rotate them manually or through an external automation.</span></span> <span data-ttu-id="fe461-105">Teraz, klucze konta magazynu kluczy w magazynie są zaimplementowane jako [kluczy tajnych Key Vault](https://docs.microsoft.com/rest/api/keyvault/about-keys--secrets-and-certificates#BKMK_WorkingWithSecrets) do uwierzytelniania przy użyciu konta magazynu Azure.</span><span class="sxs-lookup"><span data-stu-id="fe461-105">Now, Key Vault Storage Account Keys are implemented as [Key Vault secrets](https://docs.microsoft.com/rest/api/keyvault/about-keys--secrets-and-certificates#BKMK_WorkingWithSecrets) for authenticating with an Azure Storage Account.</span></span> 

<span data-ttu-id="fe461-106">Funkcja klucza ASA Hello zarządza tajny obrotu i eliminuje potrzebę hello bezpośredni kontakt z kluczem ASA, oferując dostępu sygnatur dostępu Współdzielonego jako metody.</span><span class="sxs-lookup"><span data-stu-id="fe461-106">hello ASA key feature manages secret rotation for you and removes hello need for your direct contact with an ASA key by offering Shared Access Signatures (SAS) as a method.</span></span> 

<span data-ttu-id="fe461-107">Aby uzyskać więcej ogólnych informacji o kontach magazynu Azure, zobacz [kont magazynu Azure o](https://docs.microsoft.com/azure/storage/storage-create-storage-account).</span><span class="sxs-lookup"><span data-stu-id="fe461-107">For more general information on Azure Storage Accounts, see [About Azure storage accounts](https://docs.microsoft.com/azure/storage/storage-create-storage-account).</span></span>

## <a name="supporting-interfaces"></a><span data-ttu-id="fe461-108">Obsługa interfejsów</span><span class="sxs-lookup"><span data-stu-id="fe461-108">Supporting interfaces</span></span>

<span data-ttu-id="fe461-109">Witaj funkcji klucze konta magazynu Azure jest początkowo dostępna za pośrednictwem hello REST, .NET / interfejsy C# i programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="fe461-109">hello Azure Storage Account keys feature is initially available through hello REST, .NET/C# and PowerShell interfaces.</span></span> <span data-ttu-id="fe461-110">Aby uzyskać więcej informacji, zobacz [z informacjami o kluczach magazynu](https://docs.microsoft.com/azure/key-vault/).</span><span class="sxs-lookup"><span data-stu-id="fe461-110">For more information, see [Key Vault Reference](https://docs.microsoft.com/azure/key-vault/).</span></span>


## <a name="storage-account-keys-behavior"></a><span data-ttu-id="fe461-111">Zachowanie klucze konta magazynu</span><span class="sxs-lookup"><span data-stu-id="fe461-111">Storage account keys behavior</span></span>

### <a name="what-key-vault-manages"></a><span data-ttu-id="fe461-112">Zarządza Magazyn kluczy</span><span class="sxs-lookup"><span data-stu-id="fe461-112">What Key Vault manages</span></span>

<span data-ttu-id="fe461-113">Magazyn kluczy wykonuje wiele funkcji zarządzania wewnętrznego w Twoim imieniu używania kluczy konta magazynu.</span><span class="sxs-lookup"><span data-stu-id="fe461-113">Key Vault performs several internal management functions on your behalf when you use Storage Account Keys.</span></span>

1. <span data-ttu-id="fe461-114">Usługa Azure Key Vault zarządza kluczy dla konta magazynu Azure (ASA).</span><span class="sxs-lookup"><span data-stu-id="fe461-114">Azure Key Vault manages keys of an Azure Storage Account (ASA).</span></span> 
    - <span data-ttu-id="fe461-115">Wewnętrznie usługi Azure Key Vault można wyświetlić listę kluczy (synchronizacja) z kontem magazynu platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="fe461-115">Internally, Azure Key Vault can list (sync) keys with an Azure Storage Account.</span></span>  
    - <span data-ttu-id="fe461-116">Usługa Azure Key Vault generuje (obraca) hello okresowo kluczy.</span><span class="sxs-lookup"><span data-stu-id="fe461-116">Azure Key Vault regenerates (rotates) hello keys periodically.</span></span> 
    - <span data-ttu-id="fe461-117">Wartości klucza nigdy nie są zwracane w toocaller odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="fe461-117">Key values are never returned in response toocaller.</span></span> 
    - <span data-ttu-id="fe461-118">Usługa Azure Key Vault zarządza klucze konta magazynu i klasycznych kont magazynu.</span><span class="sxs-lookup"><span data-stu-id="fe461-118">Azure Key Vault manages keys of both Storage Accounts and Classic Storage Accounts.</span></span> 
2. <span data-ttu-id="fe461-119">Usługa Azure Key Vault umożliwia możesz właściciela magazynu/obiektu hello, toocreate definicje SAS (konta lub sygnatury dostępu Współdzielonego usługi).</span><span class="sxs-lookup"><span data-stu-id="fe461-119">Azure Key Vault allows you, hello vault/object owner, toocreate SAS (account or service SAS) definitions.</span></span> 
    - <span data-ttu-id="fe461-120">Hello wartość SAS, utworzone za pomocą definicji SAS, jest zwracana jako klucza tajnego za pośrednictwem ścieżka identyfikatora URI REST hello.</span><span class="sxs-lookup"><span data-stu-id="fe461-120">hello SAS value, created using SAS definition, is returned as a secret via hello REST URI path.</span></span> <span data-ttu-id="fe461-121">Aby uzyskać więcej informacji, zobacz [operacje konta magazynu usługi Azure Key Vault](https://docs.microsoft.com/rest/api/keyvault/storage-account-key-operations).</span><span class="sxs-lookup"><span data-stu-id="fe461-121">For more information, see [Azure Key Vault storage account operations](https://docs.microsoft.com/rest/api/keyvault/storage-account-key-operations).</span></span>

### <a name="naming-guidance"></a><span data-ttu-id="fe461-122">Wskazówki dotyczące nazewnictwa</span><span class="sxs-lookup"><span data-stu-id="fe461-122">Naming guidance</span></span>

<span data-ttu-id="fe461-123">Nazwy kont usługi Magazyn muszą mieć długość od 3 do 24 znaków i mogą zawierać tylko cyfry i małe litery.</span><span class="sxs-lookup"><span data-stu-id="fe461-123">Storage account names must be between 3 and 24 characters in length and may contain numbers and lowercase letters only.</span></span>  
 
<span data-ttu-id="fe461-124">Nazwa definicji SAS musi być 1 102 znaków długości i zawierać tylko 0-9, a-z, A-Z.</span><span class="sxs-lookup"><span data-stu-id="fe461-124">A SAS definition name must be 1-102 characters in length containing only 0-9, a-z, A-Z.</span></span>

## <a name="developer-experience"></a><span data-ttu-id="fe461-125">Środowisko dewelopera</span><span class="sxs-lookup"><span data-stu-id="fe461-125">Developer experience</span></span> 

### <a name="before-azure-key-vault-storage-keys"></a><span data-ttu-id="fe461-126">Przed usługi Azure Key Vault magazynu kluczy</span><span class="sxs-lookup"><span data-stu-id="fe461-126">Before Azure Key Vault Storage Keys</span></span> 

<span data-ttu-id="fe461-127">Deweloperzy używane hello toodo tooneed wskazówek z magazynu tooAzure dostępu tooget klucza konta magazynu.</span><span class="sxs-lookup"><span data-stu-id="fe461-127">Developers used tooneed toodo hello following practices with a storage account key tooget access tooAzure storage.</span></span> 
 
 ```
//create storage account using connection string containing account name 
// and hello storage key 

var storageAccount = CloudStorageAccount.Parse(CloudConfigurationManager.GetSetting("StorageConnectionString"));
var blobClient = storageAccount.CreateCloudBlobClient();
 ```
 
### <a name="after-azure-key-vault-storage-keys"></a><span data-ttu-id="fe461-128">Po usługi Azure Key Vault magazynu kluczy</span><span class="sxs-lookup"><span data-stu-id="fe461-128">After Azure Key Vault Storage Keys</span></span> 

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
 
 ### <a name="developer-best-practices"></a><span data-ttu-id="fe461-129">Najlepsze praktyki Developer</span><span class="sxs-lookup"><span data-stu-id="fe461-129">Developer best practices</span></span> 

- <span data-ttu-id="fe461-130">Zezwalaj na tylko toomanage Key Vault klucze ASA.</span><span class="sxs-lookup"><span data-stu-id="fe461-130">Only allow Key Vault toomanage your ASA keys.</span></span> <span data-ttu-id="fe461-131">Nie należy podejmować toomanage je samodzielnie, będzie kolidować z procesami magazynu kluczy.</span><span class="sxs-lookup"><span data-stu-id="fe461-131">Do not attempt toomanage them yourself, you will interfere with Key Vault's processes.</span></span> 
- <span data-ttu-id="fe461-132">Nie zezwalaj toobe klucze ASA zarządzane przez więcej niż jeden obiekt magazynu kluczy.</span><span class="sxs-lookup"><span data-stu-id="fe461-132">Do not allow ASA keys toobe managed by more than one Key Vault object.</span></span> 
- <span data-ttu-id="fe461-133">Jeśli potrzebujesz toomanually ponownie wygenerować klucze ASA, zaleca się Generuj je za pomocą usługi Key Vault.</span><span class="sxs-lookup"><span data-stu-id="fe461-133">If you need toomanually regenerate your ASA keys, we recommend that you regenerate them via Key Vault.</span></span> 

## <a name="getting-started"></a><span data-ttu-id="fe461-134">Wprowadzenie</span><span class="sxs-lookup"><span data-stu-id="fe461-134">Getting started</span></span>

### <a name="setup-for-role-based-access-control-rbac-permissions"></a><span data-ttu-id="fe461-135">Ustawienia dla uprawnień kontroli dostępu opartej na rolach</span><span class="sxs-lookup"><span data-stu-id="fe461-135">Setup for role-based access control (RBAC) permissions</span></span>

<span data-ttu-id="fe461-136">Magazyn kluczy wymaga uprawnień zbyt*listy* i *ponownie wygenerować* kluczy dla konta magazynu.</span><span class="sxs-lookup"><span data-stu-id="fe461-136">Key Vault needs permissions too*list* and *regenerate* keys for a storage account.</span></span> <span data-ttu-id="fe461-137">Skonfiguruj te uprawnienia za pomocą hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="fe461-137">Set up these permissions using hello following steps:</span></span>

- <span data-ttu-id="fe461-138">Pobrania ObjectId magazynu kluczy:</span><span class="sxs-lookup"><span data-stu-id="fe461-138">Get ObjectId of Key Vault:</span></span> 

    `Get-AzureRmADServicePrincipal -SearchString "AzureKeyVault"`

- <span data-ttu-id="fe461-139">Przypisz tooAzure roli operatora klucza magazynu klucz magazynu tożsamości:</span><span class="sxs-lookup"><span data-stu-id="fe461-139">Assign Storage Key Operator role tooAzure Key Vault Identity:</span></span> 

    `New-AzureRmRoleAssignment -ObjectId <objectId of AzureKeyVault from previous command> -RoleDefinitionName 'Storage Account Key Operator Service Role' -Scope '<azure resource id of storage account>'`

    >[!NOTE]
    > <span data-ttu-id="fe461-140">Dla typu konta klasycznego, ustaw parametr roli hello zbyt*"Klasycznego magazynu konta klucza usługi roli operatora"*.</span><span class="sxs-lookup"><span data-stu-id="fe461-140">For a classic account type, set hello role parameter too*"Classic Storage Account Key Operator Service Role"*.</span></span>

### <a name="storage-account-onboarding"></a><span data-ttu-id="fe461-141">Dołączanie konta magazynu</span><span class="sxs-lookup"><span data-stu-id="fe461-141">Storage account onboarding</span></span> 

<span data-ttu-id="fe461-142">Przykład: Jako właściciel obiektu magazynu kluczy, Dodaj magazynu konta tooonboard usługi Azure Key Vault tooyour obiektu konta magazynu.</span><span class="sxs-lookup"><span data-stu-id="fe461-142">Example: As a Key Vault object owner you add a storage account object tooyour Azure Key Vault tooonboard a storage account.</span></span>

<span data-ttu-id="fe461-143">Podczas dołączania, Key Vault musi tooverify hello tożsamość konta dołączania hello zbyt ma uprawnienia*listy* i zbyt*ponownie wygenerować* magazynu kluczy.</span><span class="sxs-lookup"><span data-stu-id="fe461-143">During onboarding, Key Vault needs tooverify that hello identity of hello onboarding account has permissions too*list* and too*regenerate* storage keys.</span></span> <span data-ttu-id="fe461-144">W celu tooverify tych uprawnień, Key Vault pobiera OBO (imieniu z) tokenu z usługi uwierzytelniania hello, odbiorców ustawić tooAzure Resource Manager i sprawia, że *listy* klucza usługi Azure Storage toohello wywołania.</span><span class="sxs-lookup"><span data-stu-id="fe461-144">In order tooverify these permissions, Key Vault gets an OBO (On Behalf Of) token from hello authentication service, audience set tooAzure Resource Manager, and makes a *list* key call toohello Azure Storage service.</span></span> <span data-ttu-id="fe461-145">Jeśli hello *listy* wywołać kończy się niepowodzeniem, hello Key Vault Tworzenie obiektu zakończy się niepowodzeniem z kodem stanu HTTP z *zabroniony*.</span><span class="sxs-lookup"><span data-stu-id="fe461-145">If hello *list* call fails, hello Key Vault object creation fails with a HTTP status code of *Forbidden*.</span></span> <span data-ttu-id="fe461-146">klawisze Hello w ten sposób są buforowane z magazynem jednostek magazynu kluczy.</span><span class="sxs-lookup"><span data-stu-id="fe461-146">hello keys listed in this fashion are cached with your key vault entity storage.</span></span> 

<span data-ttu-id="fe461-147">Magazyn kluczy musi sprawdzić, czy tożsamość hello *ponownie wygenerować* uprawnienia przed jego przejąć prawo własności ponowne generowanie kluczy.</span><span class="sxs-lookup"><span data-stu-id="fe461-147">Key Vault must verify that hello identity has *regenerate* permissions before it can take ownership of regenerating your keys.</span></span> <span data-ttu-id="fe461-148">tooverify, który hello tożsamości za pomocą tokenu OBO, a także hello Key Vault pierwszej strony tożsamości ma te uprawnienia:</span><span class="sxs-lookup"><span data-stu-id="fe461-148">tooverify that hello identity, via OBO token, as well as hello Key Vault first party identity has these permissions:</span></span>

- <span data-ttu-id="fe461-149">Magazyn kluczy wymieniono uprawnienia RBAC hello magazynu konta zasobu.</span><span class="sxs-lookup"><span data-stu-id="fe461-149">Key Vault lists RBAC permissions on hello storage account resource.</span></span>
- <span data-ttu-id="fe461-150">Magazyn kluczy weryfikuje hello odpowiedzi przez Dopasowywanie wyrażeń regularnych z systemem innym niż akcji i akcje.</span><span class="sxs-lookup"><span data-stu-id="fe461-150">Key Vault validates hello response via regular expression matching of actions and non-actions.</span></span> 

<span data-ttu-id="fe461-151">Znajdź przykłady obsługi na [magazyn kluczy - zarządzane przykłady klucze konta magazynu](https://github.com/Azure/azure-sdk-for-net/blob/psSdkJson6/src/SDKs/KeyVault/dataPlane/Microsoft.Azure.KeyVault.Samples/samples/HelloKeyVault/Program.cs#L167).</span><span class="sxs-lookup"><span data-stu-id="fe461-151">Find some supporting examples at [Key Vault - Managed Storage Account Keys Samples](https://github.com/Azure/azure-sdk-for-net/blob/psSdkJson6/src/SDKs/KeyVault/dataPlane/Microsoft.Azure.KeyVault.Samples/samples/HelloKeyVault/Program.cs#L167).</span></span>

<span data-ttu-id="fe461-152">Jeśli tożsamość hello nie ma *ponownie wygenerować* uprawnienia lub jeśli nie ma usługi Key Vault pierwszy tożsamości firm *listy* lub *ponownie wygenerować* uprawnienia, a następnie dołączania hello żądanie nie powiedzie się, zwracając kod błędu odpowiednie i komunikatu.</span><span class="sxs-lookup"><span data-stu-id="fe461-152">If hello identity does not have *regenerate* permissions or if Key Vault's first party identity doesn’t have *list* or *regenerate* permission, then hello onboarding request fails returning an appropriate error code and message.</span></span> 

<span data-ttu-id="fe461-153">Hello OBO token działa tylko, gdy używasz firmy, aplikacje klienckie natywnego programu PowerShell lub interfejsu wiersza polecenia.</span><span class="sxs-lookup"><span data-stu-id="fe461-153">hello OBO token will only work when you use first-party, native client applications of either PowerShell or CLI.</span></span>

## <a name="other-applications"></a><span data-ttu-id="fe461-154">Inne aplikacje</span><span class="sxs-lookup"><span data-stu-id="fe461-154">Other applications</span></span>

- <span data-ttu-id="fe461-155">Tokeny sygnatury dostępu Współdzielonego, tworzony przy użyciu kluczy konta magazynu usługi Key Vault, zapewniają większą kontrolą dostępu tooan kontem magazynu platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="fe461-155">SAS tokens, constructed using Key Vault storage account keys, provide even more controlled access tooan Azure storage account.</span></span> <span data-ttu-id="fe461-156">Aby uzyskać więcej informacji, zobacz [używanie sygnatury dostępu współdzielonego](https://docs.microsoft.com/azure/storage/storage-dotnet-shared-access-signature-part-1).</span><span class="sxs-lookup"><span data-stu-id="fe461-156">For more information, see [Using shared access signatures](https://docs.microsoft.com/azure/storage/storage-dotnet-shared-access-signature-part-1).</span></span>

## <a name="see-also"></a><span data-ttu-id="fe461-157">Zobacz też</span><span class="sxs-lookup"><span data-stu-id="fe461-157">See also</span></span>

- [<span data-ttu-id="fe461-158">Informacje o kluczach, wpisach tajnych i certyfikatach</span><span class="sxs-lookup"><span data-stu-id="fe461-158">About keys, secrets, and certificates</span></span>](https://docs.microsoft.com/rest/api/keyvault/)
- [<span data-ttu-id="fe461-159">Blog zespołu magazyn kluczy</span><span class="sxs-lookup"><span data-stu-id="fe461-159">Key Vault Team Blog</span></span>](https://blogs.technet.microsoft.com/kv/)
