---
title: "Samouczek: Szyfrowanie i odszyfrowywanie obiektów blob w usłudze Azure Storage za pomocą usługi Azure Key Vault | Dokumentacja firmy Microsoft"
description: "Jak szyfrowanie i odszyfrowywanie obiektów blob za pomocą szyfrowania po stronie klienta dla usługi Magazyn Microsoft Azure z usługą Azure Key Vault."
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
ms.openlocfilehash: 0c33742a0212e670072a947a2d2ab8304c77b973
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-encrypt-and-decrypt-blobs-in-microsoft-azure-storage-using-azure-key-vault"></a><span data-ttu-id="df46a-103">Samouczek: Szyfrowanie i odszyfrowywanie obiektów blob w magazynie platformy Microsoft Azure przy użyciu usługi Azure Key Vault</span><span class="sxs-lookup"><span data-stu-id="df46a-103">Tutorial: Encrypt and decrypt blobs in Microsoft Azure Storage using Azure Key Vault</span></span>
## <a name="introduction"></a><span data-ttu-id="df46a-104">Wprowadzenie</span><span class="sxs-lookup"><span data-stu-id="df46a-104">Introduction</span></span>
<span data-ttu-id="df46a-105">W tym samouczku opisano sposób należy korzystać z szyfrowania magazynu po stronie klienta z usługi Azure Key Vault.</span><span class="sxs-lookup"><span data-stu-id="df46a-105">This tutorial covers how to make use of client-side storage encryption with Azure Key Vault.</span></span> <span data-ttu-id="df46a-106">Przeprowadza użytkownika przez proces szyfrowania i odszyfrowywania obiektu blob w aplikacji konsoli przy użyciu tych technologii.</span><span class="sxs-lookup"><span data-stu-id="df46a-106">It walks you through how to encrypt and decrypt a blob in a console application using these technologies.</span></span>

<span data-ttu-id="df46a-107">**Szacowany czas trwania:** 20 minut</span><span class="sxs-lookup"><span data-stu-id="df46a-107">**Estimated time to complete:** 20 minutes</span></span>

<span data-ttu-id="df46a-108">Aby uzyskać przegląd informacji dotyczących usługi Azure Key Vault, zobacz [co to jest usługa Azure Key Vault?](../key-vault/key-vault-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="df46a-108">For overview information about Azure Key Vault, see [What is Azure Key Vault?](../key-vault/key-vault-whatis.md).</span></span>

<span data-ttu-id="df46a-109">Aby uzyskać przegląd informacji dotyczących szyfrowania po stronie klienta dla usługi Azure Storage, zobacz [szyfrowania po stronie klienta i usługi Azure Key Vault dla magazynu Microsoft Azure](storage-client-side-encryption.md).</span><span class="sxs-lookup"><span data-stu-id="df46a-109">For overview information about client-side encryption for Azure Storage, see [Client-Side Encryption and Azure Key Vault for Microsoft Azure Storage](storage-client-side-encryption.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="df46a-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="df46a-110">Prerequisites</span></span>
<span data-ttu-id="df46a-111">Do ukończenia tego samouczka niezbędne są następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="df46a-111">To complete this tutorial, you must have the following:</span></span>

* <span data-ttu-id="df46a-112">Konto usługi Azure Storage</span><span class="sxs-lookup"><span data-stu-id="df46a-112">An Azure Storage account</span></span>
* <span data-ttu-id="df46a-113">Visual Studio 2013 lub nowszy</span><span class="sxs-lookup"><span data-stu-id="df46a-113">Visual Studio 2013 or later</span></span>
* <span data-ttu-id="df46a-114">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="df46a-114">Azure PowerShell</span></span>

## <a name="overview-of-client-side-encryption"></a><span data-ttu-id="df46a-115">Omówienie szyfrowania po stronie klienta</span><span class="sxs-lookup"><span data-stu-id="df46a-115">Overview of client-side encryption</span></span>
<span data-ttu-id="df46a-116">Omówienie szyfrowania po stronie klienta dla usługi Azure Storage, zobacz [szyfrowania po stronie klienta i usługi Azure Key Vault dla magazynu Microsoft Azure](storage-client-side-encryption.md)</span><span class="sxs-lookup"><span data-stu-id="df46a-116">For an overview of client-side encryption for Azure Storage, see [Client-Side Encryption and Azure Key Vault for Microsoft Azure Storage](storage-client-side-encryption.md)</span></span>

<span data-ttu-id="df46a-117">Poniżej przedstawiono krótki opis działania szyfrowania po stronie klienta:</span><span class="sxs-lookup"><span data-stu-id="df46a-117">Here is a brief description of how client side encryption works:</span></span>

1. <span data-ttu-id="df46a-118">Zestaw SDK klienta usługi Azure Storage generuje klucz szyfrowania zawartości (CEK), jest jeden jednorazowej użycia klucza symetrycznego.</span><span class="sxs-lookup"><span data-stu-id="df46a-118">The Azure Storage client SDK generates a content encryption key (CEK), which is a one-time-use symmetric key.</span></span>
2. <span data-ttu-id="df46a-119">Dane klienta są szyfrowane przy użyciu tego CEK.</span><span class="sxs-lookup"><span data-stu-id="df46a-119">Customer data is encrypted using this CEK.</span></span>
3. <span data-ttu-id="df46a-120">CEK jest następnie opakowane (zaszyfrowane) przy użyciu klucza szyfrowania klucza (KEK).</span><span class="sxs-lookup"><span data-stu-id="df46a-120">The CEK is then wrapped (encrypted) using the key encryption key (KEK).</span></span> <span data-ttu-id="df46a-121">KEK jest identyfikowany przez identyfikator klucza i można parę klucza asymetrycznego lub klucza symetrycznego i można być zarządzany lokalnie lub przechowywane w usłudze Azure Key Vault.</span><span class="sxs-lookup"><span data-stu-id="df46a-121">The KEK is identified by a key identifier and can be an asymmetric key pair or a symmetric key and can be managed locally or stored in Azure Key Vault.</span></span> <span data-ttu-id="df46a-122">Klienta magazynu nigdy nie ma dostępu do klucza KEK.</span><span class="sxs-lookup"><span data-stu-id="df46a-122">The Storage client itself never has access to the KEK.</span></span> <span data-ttu-id="df46a-123">Wywołuje po prostu algorytm klucza zawijania zapewnianej przez usługi Key Vault.</span><span class="sxs-lookup"><span data-stu-id="df46a-123">It just invokes the key wrapping algorithm that is provided by Key Vault.</span></span> <span data-ttu-id="df46a-124">Klienci mogą wybrać do używania niestandardowych dostawców dla zawijania/odkodowywania chcący klucza.</span><span class="sxs-lookup"><span data-stu-id="df46a-124">Customers can choose to use custom providers for key wrapping/unwrapping if they want.</span></span>
4. <span data-ttu-id="df46a-125">Zaszyfrowane dane są następnie przekazywane do usługi Magazyn Azure.</span><span class="sxs-lookup"><span data-stu-id="df46a-125">The encrypted data is then uploaded to the Azure Storage service.</span></span>

## <a name="set-up-your-azure-key-vault"></a><span data-ttu-id="df46a-126">Skonfiguruj magazyn kluczy Azure</span><span class="sxs-lookup"><span data-stu-id="df46a-126">Set up your Azure Key Vault</span></span>
<span data-ttu-id="df46a-127">Aby kontynuować z tego samouczka, należy wykonać następujące kroki, które zostały opisane w samouczku [wprowadzenie do usługi Azure Key Vault](../key-vault/key-vault-get-started.md):</span><span class="sxs-lookup"><span data-stu-id="df46a-127">In order to proceed with this tutorial, you need to do the following steps, which are outlined in the tutorial  [Get started with Azure Key Vault](../key-vault/key-vault-get-started.md):</span></span>

* <span data-ttu-id="df46a-128">Tworzenie magazynu kluczy.</span><span class="sxs-lookup"><span data-stu-id="df46a-128">Create a key vault.</span></span>
* <span data-ttu-id="df46a-129">Dodawanie klucza lub klucza tajnego do magazynu kluczy.</span><span class="sxs-lookup"><span data-stu-id="df46a-129">Add a key or secret to the key vault.</span></span>
* <span data-ttu-id="df46a-130">Rejestrowanie aplikacji w usłudze Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="df46a-130">Register an application with Azure Active Directory.</span></span>
* <span data-ttu-id="df46a-131">Zezwolić aplikacji na używanie klucza lub klucza tajnego.</span><span class="sxs-lookup"><span data-stu-id="df46a-131">Authorize the application to use the key or secret.</span></span>

<span data-ttu-id="df46a-132">Zanotuj ClientID i ClientSecret, które zostały wygenerowane podczas rejestrowania aplikacji w usłudze Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="df46a-132">Make note of the ClientID and ClientSecret that were generated when registering an application with Azure Active Directory.</span></span>

<span data-ttu-id="df46a-133">Utwórz obydwu kluczy w magazynie kluczy.</span><span class="sxs-lookup"><span data-stu-id="df46a-133">Create both keys in the key vault.</span></span> <span data-ttu-id="df46a-134">W pozostałej części samouczka przyjmujemy, użycie następujących nazw: ContosoKeyVault i TestRSAKey1.</span><span class="sxs-lookup"><span data-stu-id="df46a-134">We assume for the rest of the tutorial that you have used the following names: ContosoKeyVault and TestRSAKey1.</span></span>

## <a name="create-a-console-application-with-packages-and-appsettings"></a><span data-ttu-id="df46a-135">Utwórz aplikację konsoli z pakietów i AppSettings</span><span class="sxs-lookup"><span data-stu-id="df46a-135">Create a console application with packages and AppSettings</span></span>
<span data-ttu-id="df46a-136">W programie Visual Studio Utwórz nową aplikację konsoli.</span><span class="sxs-lookup"><span data-stu-id="df46a-136">In Visual Studio, create a new console application.</span></span>

<span data-ttu-id="df46a-137">Dodawanie pakietów nuget niezbędne w konsoli Menedżera pakietów.</span><span class="sxs-lookup"><span data-stu-id="df46a-137">Add necessary nuget packages in the Package Manager Console.</span></span>

```
Install-Package WindowsAzure.Storage

// This is the latest stable release for ADAL.
Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory -Version 2.16.204221202

Install-Package Microsoft.Azure.KeyVault
Install-Package Microsoft.Azure.KeyVault.Extensions
```

<span data-ttu-id="df46a-138">Dodaj AppSettings do pliku App.Config.</span><span class="sxs-lookup"><span data-stu-id="df46a-138">Add AppSettings to the App.Config.</span></span>

```xml
<appSettings>
    <add key="accountName" value="myaccount"/>
    <add key="accountKey" value="theaccountkey"/>
    <add key="clientId" value="theclientid"/>
    <add key="clientSecret" value="theclientsecret"/>
    <add key="container" value="stuff"/>
</appSettings>
```

<span data-ttu-id="df46a-139">Dodaj następujące `using` instrukcje i upewnij się, że można dodać odwołania do System.Configuration do projektu.</span><span class="sxs-lookup"><span data-stu-id="df46a-139">Add the following `using` statements and make sure to add a reference to System.Configuration to the project.</span></span>

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

## <a name="add-a-method-to-get-a-token-to-your-console-application"></a><span data-ttu-id="df46a-140">Dodaj metodę, aby uzyskać token do aplikacji konsoli</span><span class="sxs-lookup"><span data-stu-id="df46a-140">Add a method to get a token to your console application</span></span>
<span data-ttu-id="df46a-141">Następująca metoda jest używana przez klasy magazynu kluczy, które muszą zostać uwierzytelniony na potrzeby dostępu do magazynu kluczy.</span><span class="sxs-lookup"><span data-stu-id="df46a-141">The following method is used by Key Vault classes that need to authenticate for access to your key vault.</span></span>

```csharp
private async static Task<string> GetToken(string authority, string resource, string scope)
{
    var authContext = new AuthenticationContext(authority);
    ClientCredential clientCred = new ClientCredential(
        ConfigurationManager.AppSettings["clientId"],
        ConfigurationManager.AppSettings["clientSecret"]);
    AuthenticationResult result = await authContext.AcquireTokenAsync(resource, clientCred);

    if (result == null)
        throw new InvalidOperationException("Failed to obtain the JWT token");

    return result.AccessToken;
}
```

## <a name="access-storage-and-key-vault-in-your-program"></a><span data-ttu-id="df46a-142">Dostęp do magazynu i klucza magazynu w programie</span><span class="sxs-lookup"><span data-stu-id="df46a-142">Access Storage and Key Vault in your program</span></span>
<span data-ttu-id="df46a-143">W funkcji Main Dodaj następujący kod.</span><span class="sxs-lookup"><span data-stu-id="df46a-143">In the Main function, add the following code.</span></span>

```csharp
// This is standard code to interact with Blob storage.
StorageCredentials creds = new StorageCredentials(
    ConfigurationManager.AppSettings["accountName"],
       ConfigurationManager.AppSettings["accountKey"]);
CloudStorageAccount account = new CloudStorageAccount(creds, useHttps: true);
CloudBlobClient client = account.CreateCloudBlobClient();
CloudBlobContainer contain = client.GetContainerReference(ConfigurationManager.AppSettings["container"]);
contain.CreateIfNotExists();

// The Resolver object is used to interact with Key Vault for Azure Storage.
// This is where the GetToken method from above is used.
KeyVaultKeyResolver cloudResolver = new KeyVaultKeyResolver(GetToken);
```

> [!NOTE]
> <span data-ttu-id="df46a-144">Modele obiektów magazynu kluczy</span><span class="sxs-lookup"><span data-stu-id="df46a-144">Key Vault Object Models</span></span>
> 
> <span data-ttu-id="df46a-145">Ważne jest, aby dowiedzieć się, że są faktycznie dwie usługi Key Vault modele obiektów należy pamiętać o: jeden jest oparta na interfejsu API REST (przestrzeń nazw KeyVault) i innych to rozszerzenie szyfrowania po stronie klienta.</span><span class="sxs-lookup"><span data-stu-id="df46a-145">It is important to understand that there are actually two Key Vault object models to be aware of: one is based on the REST API (KeyVault namespace) and the other is an extension for client-side encryption.</span></span>
> 
> <span data-ttu-id="df46a-146">Klucz magazynu klienta współdziała z interfejsu API REST i rozumie JSON Web kluczy i kluczy tajnych na dwa rodzaje rzeczy, które są zawarte w magazynie kluczy.</span><span class="sxs-lookup"><span data-stu-id="df46a-146">The Key Vault Client interacts with the REST API and understands JSON Web Keys and secrets for the two kinds of things that are contained in Key Vault.</span></span>
> 
> <span data-ttu-id="df46a-147">Rozszerzenia magazynu kluczy są klasy, które wydają się utworzone specjalnie do szyfrowania po stronie klienta w usłudze Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="df46a-147">The Key Vault Extensions are classes that seem specifically created for client-side encryption in Azure Storage.</span></span> <span data-ttu-id="df46a-148">Zawierają one interfejs dla kluczy (IKey) i oparty na koncepcji rozpoznawania klucz klasy.</span><span class="sxs-lookup"><span data-stu-id="df46a-148">They contain an interface for keys (IKey) and classes based on the concept of a Key Resolver.</span></span> <span data-ttu-id="df46a-149">Istnieją dwa implementacje IKey, które trzeba znać: RSAKey i SymmetricKey.</span><span class="sxs-lookup"><span data-stu-id="df46a-149">There are two implementations of IKey that you need to know: RSAKey and SymmetricKey.</span></span> <span data-ttu-id="df46a-150">Teraz się zdarzyć się z rzeczy, które są zawarte w magazynie kluczy, ale w tym momencie są niezależne klasy (tak, aby klucz i klucz tajny pobierane przez klienta klucza magazynu nie implementują IKey).</span><span class="sxs-lookup"><span data-stu-id="df46a-150">Now they happen to coincide with the things that are contained in a Key Vault, but at this point they are independent classes (so the Key and Secret retrieved by the Key Vault Client do not implement IKey).</span></span>
> 
> 

## <a name="encrypt-blob-and-upload"></a><span data-ttu-id="df46a-151">Szyfrowanie obiektów blob i przekaż</span><span class="sxs-lookup"><span data-stu-id="df46a-151">Encrypt blob and upload</span></span>
<span data-ttu-id="df46a-152">Dodaj następujący kod do szyfrowania obiektu blob i przekaż go do konta magazynu Azure.</span><span class="sxs-lookup"><span data-stu-id="df46a-152">Add the following code to encrypt a blob and upload it to your Azure storage account.</span></span> <span data-ttu-id="df46a-153">**ResolveKeyAsync** IKey zwraca metodę, która jest używana.</span><span class="sxs-lookup"><span data-stu-id="df46a-153">The **ResolveKeyAsync** method that is used returns an IKey.</span></span>

```csharp
// Retrieve the key that you created previously.
// The IKey that is returned here is an RsaKey.
// Remember that we used the names contosokeyvault and testrsakey1.
var rsa = cloudResolver.ResolveKeyAsync("https://contosokeyvault.vault.azure.net/keys/TestRSAKey1", CancellationToken.None).GetAwaiter().GetResult();

// Now you simply use the RSA key to encrypt by setting it in the BlobEncryptionPolicy.
BlobEncryptionPolicy policy = new BlobEncryptionPolicy(rsa, null);
BlobRequestOptions options = new BlobRequestOptions() { EncryptionPolicy = policy };

// Reference a block blob.
CloudBlockBlob blob = contain.GetBlockBlobReference("MyFile.txt");

// Upload using the UploadFromStream method.
using (var stream = System.IO.File.OpenRead(@"C:\data\MyFile.txt"))
    blob.UploadFromStream(stream, stream.Length, null, options, null);
```

<span data-ttu-id="df46a-154">Poniżej przedstawiono zrzut ekranu [klasycznego portalu Azure](https://manage.windowsazure.com) dla obiekt blob, który został zaszyfrowany za pomocą szyfrowania po stronie klienta przy użyciu klucza przechowywane w magazynie kluczy.</span><span class="sxs-lookup"><span data-stu-id="df46a-154">Following is a screenshot from the [Azure Classic Portal](https://manage.windowsazure.com) for a blob that has been encrypted by using client-side encryption with a key stored in Key Vault.</span></span> <span data-ttu-id="df46a-155">**KeyId** właściwości jest identyfikatorem URI dla klucza w magazynie kluczy, który działa jako klucza KEK.</span><span class="sxs-lookup"><span data-stu-id="df46a-155">The **KeyId** property is the URI for the key in Key Vault that acts as the KEK.</span></span> <span data-ttu-id="df46a-156">**EncryptedKey** zaszyfrowana wersja CEK zawiera właściwości.</span><span class="sxs-lookup"><span data-stu-id="df46a-156">The **EncryptedKey** property contains the encrypted version of the CEK.</span></span>

![Zrzut ekranu przedstawiający metadane obiektu Blob, zawierający metadane szyfrowania](./media/storage-encrypt-decrypt-blobs-key-vault/blobmetadata.png)

> [!NOTE]
> <span data-ttu-id="df46a-158">Jeśli przyjrzymy się konstruktora BlobEncryptionPolicy, pojawi się że można zaakceptować klucza i/lub program rozpoznawania nazw.</span><span class="sxs-lookup"><span data-stu-id="df46a-158">If you look at the BlobEncryptionPolicy constructor, you will see that it can accept a key and/or a resolver.</span></span> <span data-ttu-id="df46a-159">Należy pamiętać, że w tej chwili nie można użyć program rozpoznawania nazw dla celów szyfrowania, ponieważ tak nie jest obecnie obsługuje domyślny klucz.</span><span class="sxs-lookup"><span data-stu-id="df46a-159">Be aware that right now you cannot use a resolver for encryption because it does not currently support a default key.</span></span>
> 
> 

## <a name="decrypt-blob-and-download"></a><span data-ttu-id="df46a-160">Odszyfrowywanie obiektów blob i pobierania</span><span class="sxs-lookup"><span data-stu-id="df46a-160">Decrypt blob and download</span></span>
<span data-ttu-id="df46a-161">Odszyfrowywanie jest w rzeczywistości podczas używania klas programu rozpoznawania nazw sensu.</span><span class="sxs-lookup"><span data-stu-id="df46a-161">Decryption is really when using the Resolver classes make sense.</span></span> <span data-ttu-id="df46a-162">Identyfikator używany do szyfrowania klucza jest skojarzony z obiektem blob w metadanych, więc nie ma powodu nie można pobrać klucza i zapamiętać skojarzenie obiektu blob i kluczy.</span><span class="sxs-lookup"><span data-stu-id="df46a-162">The ID of the key used for encryption is associated with the blob in its metadata, so there is no reason for you to retrieve the key and remember the association between key and blob.</span></span> <span data-ttu-id="df46a-163">Masz upewnić się, że klucz pozostanie w magazynie kluczy.</span><span class="sxs-lookup"><span data-stu-id="df46a-163">You just have to make sure that the key remains in Key Vault.</span></span>   

<span data-ttu-id="df46a-164">Klucza prywatnego klucza RSA pozostaje w magazynie kluczy, więc do odszyfrowywania nastąpić, zaszyfrowany klucz z metadane obiektu blob, który zawiera CEK są wysyłane do usługi Key Vault do odszyfrowywania.</span><span class="sxs-lookup"><span data-stu-id="df46a-164">The private key of an RSA Key remains in Key Vault, so for decryption to occur, the Encrypted Key from the blob metadata that contains the CEK is sent to Key Vault for decryption.</span></span>

<span data-ttu-id="df46a-165">Dodaj następujący kod do odszyfrowania obiektu blob, który został przekazany.</span><span class="sxs-lookup"><span data-stu-id="df46a-165">Add the following to decrypt the blob that you just uploaded.</span></span>

```csharp
// In this case, we will not pass a key and only pass the resolver because
// this policy will only be used for downloading / decrypting.
BlobEncryptionPolicy policy = new BlobEncryptionPolicy(null, cloudResolver);
BlobRequestOptions options = new BlobRequestOptions() { EncryptionPolicy = policy };

using (var np = File.Open(@"C:\data\MyFileDecrypted.txt", FileMode.Create))
    blob.DownloadToStream(np, null, options, null);
```

> [!NOTE]
> <span data-ttu-id="df46a-166">Istnieje kilka innych rodzajów rozpoznawania nazw, aby ułatwić zarządzanie kluczami, w tym: AggregateKeyResolver i CachingKeyResolver.</span><span class="sxs-lookup"><span data-stu-id="df46a-166">There are a couple of other kinds of resolvers to make key management easier, including: AggregateKeyResolver and CachingKeyResolver.</span></span>
> 
> 

## <a name="use-key-vault-secrets"></a><span data-ttu-id="df46a-167">Użyj kluczy tajnych magazyn kluczy</span><span class="sxs-lookup"><span data-stu-id="df46a-167">Use Key Vault secrets</span></span>
<span data-ttu-id="df46a-168">Sposób używać hasła przy użyciu szyfrowania po stronie klienta jest za pomocą klasy SymmetricKey, ponieważ klucz tajny jest zasadniczo klucza symetrycznego.</span><span class="sxs-lookup"><span data-stu-id="df46a-168">The way to use a secret with client-side encryption is via the SymmetricKey class because a secret is essentially a symmetric key.</span></span> <span data-ttu-id="df46a-169">Jednak jak wspomniano powyżej, klucza tajnego w magazynie kluczy nie jest zmapowany dokładnie SymmetricKey.</span><span class="sxs-lookup"><span data-stu-id="df46a-169">But, as noted above, a secret in Key Vault does not map exactly to a SymmetricKey.</span></span> <span data-ttu-id="df46a-170">Istnieje kilka rzeczy, aby zrozumieć:</span><span class="sxs-lookup"><span data-stu-id="df46a-170">There are a few things to understand:</span></span>

* <span data-ttu-id="df46a-171">Klucz w SymmetricKey musi być stałą długość: 128, 192, 256, 384 lub 512 bitów.</span><span class="sxs-lookup"><span data-stu-id="df46a-171">The key in a SymmetricKey has to be a fixed length: 128, 192, 256, 384, or 512 bits.</span></span>
* <span data-ttu-id="df46a-172">Klucz w SymmetricKey powinien być kodowany w standardzie Base64.</span><span class="sxs-lookup"><span data-stu-id="df46a-172">The key in a SymmetricKey should be Base64 encoded.</span></span>
* <span data-ttu-id="df46a-173">Klucz tajny usługi Key Vault, która będzie służyć jako SymmetricKey musi mieć typ zawartości "application/octet-stream" w magazynie kluczy.</span><span class="sxs-lookup"><span data-stu-id="df46a-173">A Key Vault secret that will be used as a SymmetricKey needs to have a Content Type of "application/octet-stream" in Key Vault.</span></span>

<span data-ttu-id="df46a-174">Oto przykład w programie PowerShell tworzenia klucza tajnego w magazynie kluczy, który może służyć jako SymmetricKey.</span><span class="sxs-lookup"><span data-stu-id="df46a-174">Here is an example in PowerShell of creating a secret in Key Vault that can be used as a SymmetricKey.</span></span>
<span data-ttu-id="df46a-175">Należy pamiętać, że wartość zakodowany $key, jest tylko w celach demonstracyjnych.</span><span class="sxs-lookup"><span data-stu-id="df46a-175">Please note that the hard coded value, $key, is for demonstration purpose only.</span></span> <span data-ttu-id="df46a-176">W swoim własnym kodem należy do wygenerowania tego klucza.</span><span class="sxs-lookup"><span data-stu-id="df46a-176">In your own code you'll want to generate this key.</span></span>

```csharp
// Here we are making a 128-bit key so we have 16 characters.
//     The characters are in the ASCII range of UTF8 so they are
//    each 1 byte. 16 x 8 = 128.
$key = "qwertyuiopasdfgh"
$b = [System.Text.Encoding]::UTF8.GetBytes($key)
$enc = [System.Convert]::ToBase64String($b)
$secretvalue = ConvertTo-SecureString $enc -AsPlainText -Force

// Substitute the VaultName and Name in this command.
$secret = Set-AzureKeyVaultSecret -VaultName 'ContoseKeyVault' -Name 'TestSecret2' -SecretValue $secretvalue -ContentType "application/octet-stream"
```

<span data-ttu-id="df46a-177">W aplikacji konsoli można użyć to samo wywołanie jako przed pobrać ten klucz tajny jako SymmetricKey.</span><span class="sxs-lookup"><span data-stu-id="df46a-177">In your console application, you can use the same call as before to retrieve this secret as a SymmetricKey.</span></span>

```csharp
SymmetricKey sec = (SymmetricKey) cloudResolver.ResolveKeyAsync(
    "https://contosokeyvault.vault.azure.net/secrets/TestSecret2/",
    CancellationToken.None).GetAwaiter().GetResult();
```
<span data-ttu-id="df46a-178">To już wszystko.</span><span class="sxs-lookup"><span data-stu-id="df46a-178">That's it.</span></span> <span data-ttu-id="df46a-179">Owocnej pracy.</span><span class="sxs-lookup"><span data-stu-id="df46a-179">Enjoy!</span></span>

## <a name="next-steps"></a><span data-ttu-id="df46a-180">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="df46a-180">Next steps</span></span>
<span data-ttu-id="df46a-181">Aby uzyskać więcej informacji o korzystaniu z usługi Magazyn Microsoft Azure w języku C#, zobacz [Biblioteka klienta usługi Microsoft Azure Storage dla platformy .NET](https://msdn.microsoft.com/library/azure/dn261237.aspx).</span><span class="sxs-lookup"><span data-stu-id="df46a-181">For more information about using Microsoft Azure Storage with C#, see [Microsoft Azure Storage Client Library for .NET](https://msdn.microsoft.com/library/azure/dn261237.aspx).</span></span>

<span data-ttu-id="df46a-182">Aby uzyskać więcej informacji na temat interfejsu API REST obiektów Blob, zobacz [interfejsu API REST usługi Blob](https://msdn.microsoft.com/library/azure/dd135733.aspx).</span><span class="sxs-lookup"><span data-stu-id="df46a-182">For more information about the Blob REST API, see [Blob Service REST API](https://msdn.microsoft.com/library/azure/dd135733.aspx).</span></span>

<span data-ttu-id="df46a-183">Aby uzyskać najnowsze informacje dotyczące usługi Magazyn Microsoft Azure, przejdź do [Blog zespołu usługi Magazyn Microsoft Azure](http://blogs.msdn.com/b/windowsazurestorage/).</span><span class="sxs-lookup"><span data-stu-id="df46a-183">For the latest information on Microsoft Azure Storage, go to the [Microsoft Azure Storage Team Blog](http://blogs.msdn.com/b/windowsazurestorage/).</span></span>
