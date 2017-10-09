---
title: "Samouczek: Szyfrowanie i odszyfrowywanie obiektów blob w usłudze Azure Storage za pomocą usługi Azure Key Vault | Dokumentacja firmy Microsoft"
description: "Jak tooencrypt i odszyfrować za pomocą szyfrowania po stronie klienta dla usługi Magazyn Microsoft Azure z usługą Azure Key Vault obiektu blob."
services: storage
documentationcenter: 
author: adhurwit
manager: jasonsav
editor: tysonn
ms.assetid: 027e8631-c1bf-48c1-9d9b-f6843e88b583
ms.service: storage
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: required
ms.date: 01/23/2017
ms.author: adhurwit
ms.openlocfilehash: e387dd419a51b5b1df62d10ead97268e8295ff56
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-encrypt-and-decrypt-blobs-in-microsoft-azure-storage-using-azure-key-vault"></a><span data-ttu-id="f135d-103">Samouczek: Szyfrowanie i odszyfrowywanie obiektów blob w magazynie platformy Microsoft Azure przy użyciu usługi Azure Key Vault</span><span class="sxs-lookup"><span data-stu-id="f135d-103">Tutorial: Encrypt and decrypt blobs in Microsoft Azure Storage using Azure Key Vault</span></span>
## <a name="introduction"></a><span data-ttu-id="f135d-104">Wprowadzenie</span><span class="sxs-lookup"><span data-stu-id="f135d-104">Introduction</span></span>
<span data-ttu-id="f135d-105">W tym samouczku opisano, jak używać toomake szyfrowania magazynu po stronie klienta z usługi Azure Key Vault.</span><span class="sxs-lookup"><span data-stu-id="f135d-105">This tutorial covers how toomake use of client-side storage encryption with Azure Key Vault.</span></span> <span data-ttu-id="f135d-106">Przeprowadzi Cię przez proces tooencrypt i odszyfrowywania obiektu blob w aplikacji konsoli przy użyciu tych technologii.</span><span class="sxs-lookup"><span data-stu-id="f135d-106">It walks you through how tooencrypt and decrypt a blob in a console application using these technologies.</span></span>

<span data-ttu-id="f135d-107">**Szacowany czas toocomplete:** 20 minut</span><span class="sxs-lookup"><span data-stu-id="f135d-107">**Estimated time toocomplete:** 20 minutes</span></span>

<span data-ttu-id="f135d-108">Aby uzyskać przegląd informacji dotyczących usługi Azure Key Vault, zobacz [co to jest usługa Azure Key Vault?](../../key-vault/key-vault-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="f135d-108">For overview information about Azure Key Vault, see [What is Azure Key Vault?](../../key-vault/key-vault-whatis.md).</span></span>

<span data-ttu-id="f135d-109">Aby uzyskać przegląd informacji dotyczących szyfrowania po stronie klienta dla usługi Azure Storage, zobacz [szyfrowania po stronie klienta i usługi Azure Key Vault dla magazynu Microsoft Azure](../common/storage-client-side-encryption.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="f135d-109">For overview information about client-side encryption for Azure Storage, see [Client-Side Encryption and Azure Key Vault for Microsoft Azure Storage](../common/storage-client-side-encryption.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f135d-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="f135d-110">Prerequisites</span></span>
<span data-ttu-id="f135d-111">toocomplete tego samouczka, musi mieć następujące hello:</span><span class="sxs-lookup"><span data-stu-id="f135d-111">toocomplete this tutorial, you must have hello following:</span></span>

* <span data-ttu-id="f135d-112">Konto usługi Azure Storage</span><span class="sxs-lookup"><span data-stu-id="f135d-112">An Azure Storage account</span></span>
* <span data-ttu-id="f135d-113">Visual Studio 2013 lub nowszy</span><span class="sxs-lookup"><span data-stu-id="f135d-113">Visual Studio 2013 or later</span></span>
* <span data-ttu-id="f135d-114">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="f135d-114">Azure PowerShell</span></span>

## <a name="overview-of-client-side-encryption"></a><span data-ttu-id="f135d-115">Omówienie szyfrowania po stronie klienta</span><span class="sxs-lookup"><span data-stu-id="f135d-115">Overview of client-side encryption</span></span>
<span data-ttu-id="f135d-116">Omówienie szyfrowania po stronie klienta dla usługi Azure Storage, zobacz [szyfrowania po stronie klienta i usługi Azure Key Vault dla magazynu Microsoft Azure](../common/storage-client-side-encryption.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="f135d-116">For an overview of client-side encryption for Azure Storage, see [Client-Side Encryption and Azure Key Vault for Microsoft Azure Storage](../common/storage-client-side-encryption.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json)</span></span>

<span data-ttu-id="f135d-117">Poniżej przedstawiono krótki opis działania szyfrowania po stronie klienta:</span><span class="sxs-lookup"><span data-stu-id="f135d-117">Here is a brief description of how client side encryption works:</span></span>

1. <span data-ttu-id="f135d-118">powitania klienta usługi Azure Storage SDK generuje klucz szyfrowania zawartości (CEK), jest jeden jednorazowej użycia klucza symetrycznego.</span><span class="sxs-lookup"><span data-stu-id="f135d-118">hello Azure Storage client SDK generates a content encryption key (CEK), which is a one-time-use symmetric key.</span></span>
2. <span data-ttu-id="f135d-119">Dane klienta są szyfrowane przy użyciu tego CEK.</span><span class="sxs-lookup"><span data-stu-id="f135d-119">Customer data is encrypted using this CEK.</span></span>
3. <span data-ttu-id="f135d-120">Witaj CEK jest następnie opakowane (zaszyfrowane) przy użyciu hello klucza szyfrowania klucza (KEK).</span><span class="sxs-lookup"><span data-stu-id="f135d-120">hello CEK is then wrapped (encrypted) using hello key encryption key (KEK).</span></span> <span data-ttu-id="f135d-121">Hello KEK jest identyfikowany przez identyfikator klucza i można parę klucza asymetrycznego lub klucza symetrycznego i może być zarządzane lokalnie lub przechowywane w usłudze Azure Key Vault.</span><span class="sxs-lookup"><span data-stu-id="f135d-121">hello KEK is identified by a key identifier and can be an asymmetric key pair or a symmetric key and can be managed locally or stored in Azure Key Vault.</span></span> <span data-ttu-id="f135d-122">Witaj magazynu klienta nigdy nie ma dostępu toohello KEK.</span><span class="sxs-lookup"><span data-stu-id="f135d-122">hello Storage client itself never has access toohello KEK.</span></span> <span data-ttu-id="f135d-123">Wywołuje po prostu algorytm klucza zawijania hello są udostępniane przez usługi Key Vault.</span><span class="sxs-lookup"><span data-stu-id="f135d-123">It just invokes hello key wrapping algorithm that is provided by Key Vault.</span></span> <span data-ttu-id="f135d-124">Klienci mogą wybrać toouse niestandardowych dostawców dla zawijania/odkodowywania chcący klucza.</span><span class="sxs-lookup"><span data-stu-id="f135d-124">Customers can choose toouse custom providers for key wrapping/unwrapping if they want.</span></span>
4. <span data-ttu-id="f135d-125">Witaj zaszyfrowane dane są następnie przekazywane toohello usługi Magazyn Azure.</span><span class="sxs-lookup"><span data-stu-id="f135d-125">hello encrypted data is then uploaded toohello Azure Storage service.</span></span>

## <a name="set-up-your-azure-key-vault"></a><span data-ttu-id="f135d-126">Skonfiguruj magazyn kluczy Azure</span><span class="sxs-lookup"><span data-stu-id="f135d-126">Set up your Azure Key Vault</span></span>
<span data-ttu-id="f135d-127">W kolejności tooproceed z tego samouczka, należy hello toodo następujące kroki, które zostały opisane w samouczku hello [wprowadzenie do usługi Azure Key Vault](../../key-vault/key-vault-get-started.md):</span><span class="sxs-lookup"><span data-stu-id="f135d-127">In order tooproceed with this tutorial, you need toodo hello following steps, which are outlined in hello tutorial  [Get started with Azure Key Vault](../../key-vault/key-vault-get-started.md):</span></span>

* <span data-ttu-id="f135d-128">Tworzenie magazynu kluczy.</span><span class="sxs-lookup"><span data-stu-id="f135d-128">Create a key vault.</span></span>
* <span data-ttu-id="f135d-129">Dodawanie klucza lub magazynu kluczy tajnych toohello.</span><span class="sxs-lookup"><span data-stu-id="f135d-129">Add a key or secret toohello key vault.</span></span>
* <span data-ttu-id="f135d-130">Rejestrowanie aplikacji w usłudze Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="f135d-130">Register an application with Azure Active Directory.</span></span>
* <span data-ttu-id="f135d-131">Autoryzacja hello aplikacji toouse hello klucza lub klucza tajnego.</span><span class="sxs-lookup"><span data-stu-id="f135d-131">Authorize hello application toouse hello key or secret.</span></span>

<span data-ttu-id="f135d-132">Upewnij się, należy wziąć pod uwagę hello ClientID i ClientSecret, które zostały wygenerowane podczas rejestrowania aplikacji w usłudze Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="f135d-132">Make note of hello ClientID and ClientSecret that were generated when registering an application with Azure Active Directory.</span></span>

<span data-ttu-id="f135d-133">Utwórz obydwu kluczy w magazynie kluczy hello.</span><span class="sxs-lookup"><span data-stu-id="f135d-133">Create both keys in hello key vault.</span></span> <span data-ttu-id="f135d-134">Przyjęto założenie, hello pozostałej części samouczka hello użycie hello następujące nazwy: ContosoKeyVault i TestRSAKey1.</span><span class="sxs-lookup"><span data-stu-id="f135d-134">We assume for hello rest of hello tutorial that you have used hello following names: ContosoKeyVault and TestRSAKey1.</span></span>

## <a name="create-a-console-application-with-packages-and-appsettings"></a><span data-ttu-id="f135d-135">Utwórz aplikację konsoli z pakietów i AppSettings</span><span class="sxs-lookup"><span data-stu-id="f135d-135">Create a console application with packages and AppSettings</span></span>
<span data-ttu-id="f135d-136">W programie Visual Studio Utwórz nową aplikację konsoli.</span><span class="sxs-lookup"><span data-stu-id="f135d-136">In Visual Studio, create a new console application.</span></span>

<span data-ttu-id="f135d-137">Dodawanie pakietów nuget niezbędne w hello Konsola Menedżera pakietów.</span><span class="sxs-lookup"><span data-stu-id="f135d-137">Add necessary nuget packages in hello Package Manager Console.</span></span>

```
Install-Package WindowsAzure.Storage

// This is hello latest stable release for ADAL.
Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory -Version 2.16.204221202

Install-Package Microsoft.Azure.KeyVault
Install-Package Microsoft.Azure.KeyVault.Extensions
```

<span data-ttu-id="f135d-138">Dodaj toohello AppSettings pliku App.Config.</span><span class="sxs-lookup"><span data-stu-id="f135d-138">Add AppSettings toohello App.Config.</span></span>

```xml
<appSettings>
    <add key="accountName" value="myaccount"/>
    <add key="accountKey" value="theaccountkey"/>
    <add key="clientId" value="theclientid"/>
    <add key="clientSecret" value="theclientsecret"/>
    <add key="container" value="stuff"/>
</appSettings>
```

<span data-ttu-id="f135d-139">Dodaj następujące hello `using` instrukcje i upewnij się, że tooadd toohello tooSystem.Configuration odwołania projektu.</span><span class="sxs-lookup"><span data-stu-id="f135d-139">Add hello following `using` statements and make sure tooadd a reference tooSystem.Configuration toohello project.</span></span>

```csharp
using Microsoft.IdentityModel.Clients.ActiveDirectory;
using System.Configuration;
using Microsoft.WindowsAzure.Storage.Auth;
using Microsoft.WindowsAzure.Storage;
using Microsoft.WindowsAzure.Storage.Blob;
using Microsoft.Azure.KeyVault;
using System.Threading;        
using System.IO;
```

## <a name="add-a-method-tooget-a-token-tooyour-console-application"></a><span data-ttu-id="f135d-140">Dodaj metodę tooget tooyour tokenu aplikacji konsoli</span><span class="sxs-lookup"><span data-stu-id="f135d-140">Add a method tooget a token tooyour console application</span></span>
<span data-ttu-id="f135d-141">Witaj następująca metoda jest używana przez klasy magazynu kluczy, które muszą tooauthenticate dla magazynu kluczy tooyour dostępu.</span><span class="sxs-lookup"><span data-stu-id="f135d-141">hello following method is used by Key Vault classes that need tooauthenticate for access tooyour key vault.</span></span>

```csharp
private async static Task<string> GetToken(string authority, string resource, string scope)
{
    var authContext = new AuthenticationContext(authority);
    ClientCredential clientCred = new ClientCredential(
        ConfigurationManager.AppSettings["clientId"],
        ConfigurationManager.AppSettings["clientSecret"]);
    AuthenticationResult result = await authContext.AcquireTokenAsync(resource, clientCred);

    if (result == null)
        throw new InvalidOperationException("Failed tooobtain hello JWT token");

    return result.AccessToken;
}
```

## <a name="access-storage-and-key-vault-in-your-program"></a><span data-ttu-id="f135d-142">Dostęp do magazynu i klucza magazynu w programie</span><span class="sxs-lookup"><span data-stu-id="f135d-142">Access Storage and Key Vault in your program</span></span>
<span data-ttu-id="f135d-143">W funkcji Main hello Dodaj hello następującego kodu.</span><span class="sxs-lookup"><span data-stu-id="f135d-143">In hello Main function, add hello following code.</span></span>

```csharp
// This is standard code toointeract with Blob storage.
StorageCredentials creds = new StorageCredentials(
    ConfigurationManager.AppSettings["accountName"],
       ConfigurationManager.AppSettings["accountKey"]);
CloudStorageAccount account = new CloudStorageAccount(creds, useHttps: true);
CloudBlobClient client = account.CreateCloudBlobClient();
CloudBlobContainer contain = client.GetContainerReference(ConfigurationManager.AppSettings["container"]);
contain.CreateIfNotExists();

// hello Resolver object is used toointeract with Key Vault for Azure Storage.
// This is where hello GetToken method from above is used.
KeyVaultKeyResolver cloudResolver = new KeyVaultKeyResolver(GetToken);
```

> [!NOTE]
> <span data-ttu-id="f135d-144">Modele obiektów magazynu kluczy</span><span class="sxs-lookup"><span data-stu-id="f135d-144">Key Vault Object Models</span></span>
> 
> <span data-ttu-id="f135d-145">Jest ważne, czy rzeczywiście dwóch obiektów usługi Key Vault toounderstand modele toobe pamiętać o: jeden jest oparta na powitania interfejsu API REST (KeyVault przestrzeń nazw) i innych hello jest rozszerzeniem szyfrowania po stronie klienta.</span><span class="sxs-lookup"><span data-stu-id="f135d-145">It is important toounderstand that there are actually two Key Vault object models toobe aware of: one is based on hello REST API (KeyVault namespace) and hello other is an extension for client-side encryption.</span></span>
> 
> <span data-ttu-id="f135d-146">Klucz magazynu klienta Hello współpracuje z hello interfejsu API REST i rozumie JSON Web kluczy i kluczy tajnych dla hello dwa rodzaje rzeczy, które są zawarte w magazynie kluczy.</span><span class="sxs-lookup"><span data-stu-id="f135d-146">hello Key Vault Client interacts with hello REST API and understands JSON Web Keys and secrets for hello two kinds of things that are contained in Key Vault.</span></span>
> 
> <span data-ttu-id="f135d-147">Witaj klucza magazynu rozszerzenia są klasy, które wydają się utworzone specjalnie do szyfrowania po stronie klienta w usłudze Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="f135d-147">hello Key Vault Extensions are classes that seem specifically created for client-side encryption in Azure Storage.</span></span> <span data-ttu-id="f135d-148">Zawierają one interfejs dla kluczy (IKey) i klas opartych na koncepcji hello klucza program rozpoznawania nazw.</span><span class="sxs-lookup"><span data-stu-id="f135d-148">They contain an interface for keys (IKey) and classes based on hello concept of a Key Resolver.</span></span> <span data-ttu-id="f135d-149">Istnieją dwa implementacje konieczność tooknow IKey: RSAKey i SymmetricKey.</span><span class="sxs-lookup"><span data-stu-id="f135d-149">There are two implementations of IKey that you need tooknow: RSAKey and SymmetricKey.</span></span> <span data-ttu-id="f135d-150">Teraz wystąpią toocoincide z hello rzeczy, które są zawarte w magazynie kluczy, ale w tym momencie są niezależne klasy (aby hello klucza i pobierane przez powitania klienta magazynu klucz tajny nie implementują IKey).</span><span class="sxs-lookup"><span data-stu-id="f135d-150">Now they happen toocoincide with hello things that are contained in a Key Vault, but at this point they are independent classes (so hello Key and Secret retrieved by hello Key Vault Client do not implement IKey).</span></span>
> 
> 

## <a name="encrypt-blob-and-upload"></a><span data-ttu-id="f135d-151">Szyfrowanie obiektów blob i przekaż</span><span class="sxs-lookup"><span data-stu-id="f135d-151">Encrypt blob and upload</span></span>
<span data-ttu-id="f135d-152">Dodaj następujący hello code tooencrypt obiektu blob i przekaż go tooyour kontem magazynu platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="f135d-152">Add hello following code tooencrypt a blob and upload it tooyour Azure storage account.</span></span> <span data-ttu-id="f135d-153">Witaj **ResolveKeyAsync** IKey zwraca metodę, która jest używana.</span><span class="sxs-lookup"><span data-stu-id="f135d-153">hello **ResolveKeyAsync** method that is used returns an IKey.</span></span>

```csharp
// Retrieve hello key that you created previously.
// hello IKey that is returned here is an RsaKey.
// Remember that we used hello names contosokeyvault and testrsakey1.
var rsa = cloudResolver.ResolveKeyAsync("https://contosokeyvault.vault.azure.net/keys/TestRSAKey1", CancellationToken.None).GetAwaiter().GetResult();

// Now you simply use hello RSA key tooencrypt by setting it in hello BlobEncryptionPolicy.
BlobEncryptionPolicy policy = new BlobEncryptionPolicy(rsa, null);
BlobRequestOptions options = new BlobRequestOptions() { EncryptionPolicy = policy };

// Reference a block blob.
CloudBlockBlob blob = contain.GetBlockBlobReference("MyFile.txt");

// Upload using hello UploadFromStream method.
using (var stream = System.IO.File.OpenRead(@"C:\data\MyFile.txt"))
    blob.UploadFromStream(stream, stream.Length, null, options, null);
```

<span data-ttu-id="f135d-154">Poniżej przedstawiono zrzut ekranu hello [klasycznego portalu Azure](https://manage.windowsazure.com) dla obiekt blob, który został zaszyfrowany za pomocą szyfrowania po stronie klienta przy użyciu klucza przechowywane w magazynie kluczy.</span><span class="sxs-lookup"><span data-stu-id="f135d-154">Following is a screenshot from hello [Azure Classic Portal](https://manage.windowsazure.com) for a blob that has been encrypted by using client-side encryption with a key stored in Key Vault.</span></span> <span data-ttu-id="f135d-155">Witaj **KeyId** właściwość jest hello identyfikatora URI dla klucza hello w magazynie kluczy, który działa jako hello KEK.</span><span class="sxs-lookup"><span data-stu-id="f135d-155">hello **KeyId** property is hello URI for hello key in Key Vault that acts as hello KEK.</span></span> <span data-ttu-id="f135d-156">Witaj **EncryptedKey** hello zaszyfrowana wersja hello CEK zawiera właściwości.</span><span class="sxs-lookup"><span data-stu-id="f135d-156">hello **EncryptedKey** property contains hello encrypted version of hello CEK.</span></span>

![Zrzut ekranu przedstawiający metadane obiektu Blob, zawierający metadane szyfrowania](./media/storage-encrypt-decrypt-blobs-key-vault/blobmetadata.png)

> [!NOTE]
> <span data-ttu-id="f135d-158">Jeśli przyjrzymy się hello BlobEncryptionPolicy konstruktora, pojawi się że można zaakceptować klucza i/lub program rozpoznawania nazw.</span><span class="sxs-lookup"><span data-stu-id="f135d-158">If you look at hello BlobEncryptionPolicy constructor, you will see that it can accept a key and/or a resolver.</span></span> <span data-ttu-id="f135d-159">Należy pamiętać, że w tej chwili nie można użyć program rozpoznawania nazw dla celów szyfrowania, ponieważ tak nie jest obecnie obsługuje domyślny klucz.</span><span class="sxs-lookup"><span data-stu-id="f135d-159">Be aware that right now you cannot use a resolver for encryption because it does not currently support a default key.</span></span>
> 
> 

## <a name="decrypt-blob-and-download"></a><span data-ttu-id="f135d-160">Odszyfrowywanie obiektów blob i pobierania</span><span class="sxs-lookup"><span data-stu-id="f135d-160">Decrypt blob and download</span></span>
<span data-ttu-id="f135d-161">Odszyfrowywanie to naprawdę podczas rozpoznawania hello przy użyciu klasy sensu.</span><span class="sxs-lookup"><span data-stu-id="f135d-161">Decryption is really when using hello Resolver classes make sense.</span></span> <span data-ttu-id="f135d-162">Identyfikator Hello używany do szyfrowania klucza hello jest skojarzony z obiektu blob hello w metadanych, więc nie ma powodu możesz tooretrieve hello klucza i Zapamiętaj hello skojarzenie obiektu blob i kluczy.</span><span class="sxs-lookup"><span data-stu-id="f135d-162">hello ID of hello key used for encryption is associated with hello blob in its metadata, so there is no reason for you tooretrieve hello key and remember hello association between key and blob.</span></span> <span data-ttu-id="f135d-163">Wystarczy toomake się, że klucz hello pozostaje w magazynie kluczy.</span><span class="sxs-lookup"><span data-stu-id="f135d-163">You just have toomake sure that hello key remains in Key Vault.</span></span>   

<span data-ttu-id="f135d-164">Witaj klucza prywatnego klucza RSA pozostaje w magazynie kluczy, więc dla toooccur odszyfrowywania hello zaszyfrowany klucz z metadane obiektu blob hello zawierający hello wysłania tooKey magazynu do odszyfrowywania CEK.</span><span class="sxs-lookup"><span data-stu-id="f135d-164">hello private key of an RSA Key remains in Key Vault, so for decryption toooccur, hello Encrypted Key from hello blob metadata that contains hello CEK is sent tooKey Vault for decryption.</span></span>

<span data-ttu-id="f135d-165">Dodaj powitania po toodecrypt hello blob, który został przekazany.</span><span class="sxs-lookup"><span data-stu-id="f135d-165">Add hello following toodecrypt hello blob that you just uploaded.</span></span>

```csharp
// In this case, we will not pass a key and only pass hello resolver because
// this policy will only be used for downloading / decrypting.
BlobEncryptionPolicy policy = new BlobEncryptionPolicy(null, cloudResolver);
BlobRequestOptions options = new BlobRequestOptions() { EncryptionPolicy = policy };

using (var np = File.Open(@"C:\data\MyFileDecrypted.txt", FileMode.Create))
    blob.DownloadToStream(np, null, options, null);
```

> [!NOTE]
> <span data-ttu-id="f135d-166">Istnieje kilka innych rodzajów zarządzania kluczami toomake rozwiązujący łatwiejsze, w tym: AggregateKeyResolver i CachingKeyResolver.</span><span class="sxs-lookup"><span data-stu-id="f135d-166">There are a couple of other kinds of resolvers toomake key management easier, including: AggregateKeyResolver and CachingKeyResolver.</span></span>
> 
> 

## <a name="use-key-vault-secrets"></a><span data-ttu-id="f135d-167">Użyj kluczy tajnych magazyn kluczy</span><span class="sxs-lookup"><span data-stu-id="f135d-167">Use Key Vault secrets</span></span>
<span data-ttu-id="f135d-168">toouse sposób Hello hasła przy użyciu szyfrowania po stronie klienta odbywa się za pośrednictwem hello SymmetricKey klasy, ponieważ klucz tajny jest zasadniczo klucza symetrycznego.</span><span class="sxs-lookup"><span data-stu-id="f135d-168">hello way toouse a secret with client-side encryption is via hello SymmetricKey class because a secret is essentially a symmetric key.</span></span> <span data-ttu-id="f135d-169">Jednak jak wspomniano powyżej, klucza tajnego w magazynie kluczy nie jest zmapowany dokładnie tooa SymmetricKey.</span><span class="sxs-lookup"><span data-stu-id="f135d-169">But, as noted above, a secret in Key Vault does not map exactly tooa SymmetricKey.</span></span> <span data-ttu-id="f135d-170">Istnieje kilka toounderstand rzeczy:</span><span class="sxs-lookup"><span data-stu-id="f135d-170">There are a few things toounderstand:</span></span>

* <span data-ttu-id="f135d-171">klucz Hello w SymmetricKey ma toobe o stałej długości: 128, 192, 256, 384 lub 512 bitów.</span><span class="sxs-lookup"><span data-stu-id="f135d-171">hello key in a SymmetricKey has toobe a fixed length: 128, 192, 256, 384, or 512 bits.</span></span>
* <span data-ttu-id="f135d-172">klucz Hello w SymmetricKey powinien być kodowany w standardzie Base64.</span><span class="sxs-lookup"><span data-stu-id="f135d-172">hello key in a SymmetricKey should be Base64 encoded.</span></span>
* <span data-ttu-id="f135d-173">Klucz tajny usługi Key Vault, która będzie służyć jako SymmetricKey musi toohave typu zawartości "application/octet-stream" w magazynie kluczy.</span><span class="sxs-lookup"><span data-stu-id="f135d-173">A Key Vault secret that will be used as a SymmetricKey needs toohave a Content Type of "application/octet-stream" in Key Vault.</span></span>

<span data-ttu-id="f135d-174">Oto przykład w programie PowerShell tworzenia klucza tajnego w magazynie kluczy, który może służyć jako SymmetricKey.</span><span class="sxs-lookup"><span data-stu-id="f135d-174">Here is an example in PowerShell of creating a secret in Key Vault that can be used as a SymmetricKey.</span></span>
<span data-ttu-id="f135d-175">Należy pamiętać, że wartość hello twardych na stałe, $key, jest tylko w celach demonstracyjnych.</span><span class="sxs-lookup"><span data-stu-id="f135d-175">Please note that hello hard coded value, $key, is for demonstration purpose only.</span></span> <span data-ttu-id="f135d-176">W swoim własnym kodem należy toogenerate tego klucza.</span><span class="sxs-lookup"><span data-stu-id="f135d-176">In your own code you'll want toogenerate this key.</span></span>

```csharp
// Here we are making a 128-bit key so we have 16 characters.
//     hello characters are in hello ASCII range of UTF8 so they are
//    each 1 byte. 16 x 8 = 128.
$key = "qwertyuiopasdfgh"
$b = [System.Text.Encoding]::UTF8.GetBytes($key)
$enc = [System.Convert]::ToBase64String($b)
$secretvalue = ConvertTo-SecureString $enc -AsPlainText -Force

// Substitute hello VaultName and Name in this command.
$secret = Set-AzureKeyVaultSecret -VaultName 'ContoseKeyVault' -Name 'TestSecret2' -SecretValue $secretvalue -ContentType "application/octet-stream"
```

<span data-ttu-id="f135d-177">W aplikacji konsoli można użyć hello sam wywołania sprzed tooretrieve tym tajny jako SymmetricKey.</span><span class="sxs-lookup"><span data-stu-id="f135d-177">In your console application, you can use hello same call as before tooretrieve this secret as a SymmetricKey.</span></span>

```csharp
SymmetricKey sec = (SymmetricKey) cloudResolver.ResolveKeyAsync(
    "https://contosokeyvault.vault.azure.net/secrets/TestSecret2/",
    CancellationToken.None).GetAwaiter().GetResult();
```
<span data-ttu-id="f135d-178">To już wszystko.</span><span class="sxs-lookup"><span data-stu-id="f135d-178">That's it.</span></span> <span data-ttu-id="f135d-179">Owocnej pracy.</span><span class="sxs-lookup"><span data-stu-id="f135d-179">Enjoy!</span></span>

## <a name="next-steps"></a><span data-ttu-id="f135d-180">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="f135d-180">Next steps</span></span>
<span data-ttu-id="f135d-181">Aby uzyskać więcej informacji o korzystaniu z usługi Magazyn Microsoft Azure w języku C#, zobacz [Biblioteka klienta usługi Microsoft Azure Storage dla platformy .NET](https://msdn.microsoft.com/library/azure/dn261237.aspx).</span><span class="sxs-lookup"><span data-stu-id="f135d-181">For more information about using Microsoft Azure Storage with C#, see [Microsoft Azure Storage Client Library for .NET](https://msdn.microsoft.com/library/azure/dn261237.aspx).</span></span>

<span data-ttu-id="f135d-182">Aby uzyskać więcej informacji na temat hello interfejsu API REST obiektów Blob, zobacz [interfejsu API REST usługi Blob](https://msdn.microsoft.com/library/azure/dd135733.aspx).</span><span class="sxs-lookup"><span data-stu-id="f135d-182">For more information about hello Blob REST API, see [Blob Service REST API](https://msdn.microsoft.com/library/azure/dd135733.aspx).</span></span>

<span data-ttu-id="f135d-183">Aby hello najnowsze informacje dotyczące usługi Magazyn Microsoft Azure, odwiedź toohello [Blog zespołu usługi Magazyn Microsoft Azure](http://blogs.msdn.com/b/windowsazurestorage/).</span><span class="sxs-lookup"><span data-stu-id="f135d-183">For hello latest information on Microsoft Azure Storage, go toohello [Microsoft Azure Storage Team Blog](http://blogs.msdn.com/b/windowsazurestorage/).</span></span>
