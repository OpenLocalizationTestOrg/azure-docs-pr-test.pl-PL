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
ms.openlocfilehash: 3eb64f104f378dd09ef295c94e03167655883391
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-encrypt-and-decrypt-blobs-in-microsoft-azure-storage-using-azure-key-vault"></a>Samouczek: Szyfrowanie i odszyfrowywanie obiektów blob w magazynie platformy Microsoft Azure przy użyciu usługi Azure Key Vault
## <a name="introduction"></a>Wprowadzenie
W tym samouczku opisano, jak używać toomake szyfrowania magazynu po stronie klienta z usługi Azure Key Vault. Przeprowadzi Cię przez proces tooencrypt i odszyfrowywania obiektu blob w aplikacji konsoli przy użyciu tych technologii.

**Szacowany czas toocomplete:** 20 minut

Aby uzyskać przegląd informacji dotyczących usługi Azure Key Vault, zobacz [co to jest usługa Azure Key Vault?](../key-vault/key-vault-whatis.md).

Aby uzyskać przegląd informacji dotyczących szyfrowania po stronie klienta dla usługi Azure Storage, zobacz [szyfrowania po stronie klienta i usługi Azure Key Vault dla magazynu Microsoft Azure](storage-client-side-encryption.md).

## <a name="prerequisites"></a>Wymagania wstępne
toocomplete tego samouczka, musi mieć następujące hello:

* Konto usługi Azure Storage
* Visual Studio 2013 lub nowszy
* Azure PowerShell

## <a name="overview-of-client-side-encryption"></a>Omówienie szyfrowania po stronie klienta
Omówienie szyfrowania po stronie klienta dla usługi Azure Storage, zobacz [szyfrowania po stronie klienta i usługi Azure Key Vault dla magazynu Microsoft Azure](storage-client-side-encryption.md)

Poniżej przedstawiono krótki opis działania szyfrowania po stronie klienta:

1. powitania klienta usługi Azure Storage SDK generuje klucz szyfrowania zawartości (CEK), jest jeden jednorazowej użycia klucza symetrycznego.
2. Dane klienta są szyfrowane przy użyciu tego CEK.
3. Witaj CEK jest następnie opakowane (zaszyfrowane) przy użyciu hello klucza szyfrowania klucza (KEK). Hello KEK jest identyfikowany przez identyfikator klucza i można parę klucza asymetrycznego lub klucza symetrycznego i może być zarządzane lokalnie lub przechowywane w usłudze Azure Key Vault. Witaj magazynu klienta nigdy nie ma dostępu toohello KEK. Wywołuje po prostu algorytm klucza zawijania hello są udostępniane przez usługi Key Vault. Klienci mogą wybrać toouse niestandardowych dostawców dla zawijania/odkodowywania chcący klucza.
4. Witaj zaszyfrowane dane są następnie przekazywane toohello usługi Magazyn Azure.

## <a name="set-up-your-azure-key-vault"></a>Skonfiguruj magazyn kluczy Azure
W kolejności tooproceed z tego samouczka, należy hello toodo następujące kroki, które zostały opisane w samouczku hello [wprowadzenie do usługi Azure Key Vault](../key-vault/key-vault-get-started.md):

* Tworzenie magazynu kluczy.
* Dodawanie klucza lub magazynu kluczy tajnych toohello.
* Rejestrowanie aplikacji w usłudze Azure Active Directory.
* Autoryzacja hello aplikacji toouse hello klucza lub klucza tajnego.

Upewnij się, należy wziąć pod uwagę hello ClientID i ClientSecret, które zostały wygenerowane podczas rejestrowania aplikacji w usłudze Azure Active Directory.

Utwórz obydwu kluczy w magazynie kluczy hello. Przyjęto założenie, hello pozostałej części samouczka hello użycie hello następujące nazwy: ContosoKeyVault i TestRSAKey1.

## <a name="create-a-console-application-with-packages-and-appsettings"></a>Utwórz aplikację konsoli z pakietów i AppSettings
W programie Visual Studio Utwórz nową aplikację konsoli.

Dodawanie pakietów nuget niezbędne w hello Konsola Menedżera pakietów.

```
Install-Package WindowsAzure.Storage

// This is hello latest stable release for ADAL.
Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory -Version 2.16.204221202

Install-Package Microsoft.Azure.KeyVault
Install-Package Microsoft.Azure.KeyVault.Extensions
```

Dodaj toohello AppSettings pliku App.Config.

```xml
<appSettings>
    <add key="accountName" value="myaccount"/>
    <add key="accountKey" value="theaccountkey"/>
    <add key="clientId" value="theclientid"/>
    <add key="clientSecret" value="theclientsecret"/>
    <add key="container" value="stuff"/>
</appSettings>
```

Dodaj następujące hello `using` instrukcje i upewnij się, że tooadd toohello tooSystem.Configuration odwołania projektu.

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

## <a name="add-a-method-tooget-a-token-tooyour-console-application"></a>Dodaj metodę tooget tooyour tokenu aplikacji konsoli
Witaj następująca metoda jest używana przez klasy magazynu kluczy, które muszą tooauthenticate dla magazynu kluczy tooyour dostępu.

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

## <a name="access-storage-and-key-vault-in-your-program"></a>Dostęp do magazynu i klucza magazynu w programie
W funkcji Main hello Dodaj hello następującego kodu.

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
> Modele obiektów magazynu kluczy
> 
> Jest ważne, czy rzeczywiście dwóch obiektów usługi Key Vault toounderstand modele toobe pamiętać o: jeden jest oparta na powitania interfejsu API REST (KeyVault przestrzeń nazw) i innych hello jest rozszerzeniem szyfrowania po stronie klienta.
> 
> Klucz magazynu klienta Hello współpracuje z hello interfejsu API REST i rozumie JSON Web kluczy i kluczy tajnych dla hello dwa rodzaje rzeczy, które są zawarte w magazynie kluczy.
> 
> Witaj klucza magazynu rozszerzenia są klasy, które wydają się utworzone specjalnie do szyfrowania po stronie klienta w usłudze Azure Storage. Zawierają one interfejs dla kluczy (IKey) i klas opartych na koncepcji hello klucza program rozpoznawania nazw. Istnieją dwa implementacje konieczność tooknow IKey: RSAKey i SymmetricKey. Teraz wystąpią toocoincide z hello rzeczy, które są zawarte w magazynie kluczy, ale w tym momencie są niezależne klasy (aby hello klucza i pobierane przez powitania klienta magazynu klucz tajny nie implementują IKey).
> 
> 

## <a name="encrypt-blob-and-upload"></a>Szyfrowanie obiektów blob i przekaż
Dodaj następujący hello code tooencrypt obiektu blob i przekaż go tooyour kontem magazynu platformy Azure. Witaj **ResolveKeyAsync** IKey zwraca metodę, która jest używana.

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

Poniżej przedstawiono zrzut ekranu hello [klasycznego portalu Azure](https://manage.windowsazure.com) dla obiekt blob, który został zaszyfrowany za pomocą szyfrowania po stronie klienta przy użyciu klucza przechowywane w magazynie kluczy. Witaj **KeyId** właściwość jest hello identyfikatora URI dla klucza hello w magazynie kluczy, który działa jako hello KEK. Witaj **EncryptedKey** hello zaszyfrowana wersja hello CEK zawiera właściwości.

![Zrzut ekranu przedstawiający metadane obiektu Blob, zawierający metadane szyfrowania](./media/storage-encrypt-decrypt-blobs-key-vault/blobmetadata.png)

> [!NOTE]
> Jeśli przyjrzymy się hello BlobEncryptionPolicy konstruktora, pojawi się że można zaakceptować klucza i/lub program rozpoznawania nazw. Należy pamiętać, że w tej chwili nie można użyć program rozpoznawania nazw dla celów szyfrowania, ponieważ tak nie jest obecnie obsługuje domyślny klucz.
> 
> 

## <a name="decrypt-blob-and-download"></a>Odszyfrowywanie obiektów blob i pobierania
Odszyfrowywanie to naprawdę podczas rozpoznawania hello przy użyciu klasy sensu. Identyfikator Hello używany do szyfrowania klucza hello jest skojarzony z obiektu blob hello w metadanych, więc nie ma powodu możesz tooretrieve hello klucza i Zapamiętaj hello skojarzenie obiektu blob i kluczy. Wystarczy toomake się, że klucz hello pozostaje w magazynie kluczy.   

Witaj klucza prywatnego klucza RSA pozostaje w magazynie kluczy, więc dla toooccur odszyfrowywania hello zaszyfrowany klucz z metadane obiektu blob hello zawierający hello wysłania tooKey magazynu do odszyfrowywania CEK.

Dodaj powitania po toodecrypt hello blob, który został przekazany.

```csharp
// In this case, we will not pass a key and only pass hello resolver because
// this policy will only be used for downloading / decrypting.
BlobEncryptionPolicy policy = new BlobEncryptionPolicy(null, cloudResolver);
BlobRequestOptions options = new BlobRequestOptions() { EncryptionPolicy = policy };

using (var np = File.Open(@"C:\data\MyFileDecrypted.txt", FileMode.Create))
    blob.DownloadToStream(np, null, options, null);
```

> [!NOTE]
> Istnieje kilka innych rodzajów zarządzania kluczami toomake rozwiązujący łatwiejsze, w tym: AggregateKeyResolver i CachingKeyResolver.
> 
> 

## <a name="use-key-vault-secrets"></a>Użyj kluczy tajnych magazyn kluczy
toouse sposób Hello hasła przy użyciu szyfrowania po stronie klienta odbywa się za pośrednictwem hello SymmetricKey klasy, ponieważ klucz tajny jest zasadniczo klucza symetrycznego. Jednak jak wspomniano powyżej, klucza tajnego w magazynie kluczy nie jest zmapowany dokładnie tooa SymmetricKey. Istnieje kilka toounderstand rzeczy:

* klucz Hello w SymmetricKey ma toobe o stałej długości: 128, 192, 256, 384 lub 512 bitów.
* klucz Hello w SymmetricKey powinien być kodowany w standardzie Base64.
* Klucz tajny usługi Key Vault, która będzie służyć jako SymmetricKey musi toohave typu zawartości "application/octet-stream" w magazynie kluczy.

Oto przykład w programie PowerShell tworzenia klucza tajnego w magazynie kluczy, który może służyć jako SymmetricKey.
Należy pamiętać, że wartość hello twardych na stałe, $key, jest tylko w celach demonstracyjnych. W swoim własnym kodem należy toogenerate tego klucza.

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

W aplikacji konsoli można użyć hello sam wywołania sprzed tooretrieve tym tajny jako SymmetricKey.

```csharp
SymmetricKey sec = (SymmetricKey) cloudResolver.ResolveKeyAsync(
    "https://contosokeyvault.vault.azure.net/secrets/TestSecret2/",
    CancellationToken.None).GetAwaiter().GetResult();
```
To już wszystko. Owocnej pracy.

## <a name="next-steps"></a>Następne kroki
Aby uzyskać więcej informacji o korzystaniu z usługi Magazyn Microsoft Azure w języku C#, zobacz [Biblioteka klienta usługi Microsoft Azure Storage dla platformy .NET](https://msdn.microsoft.com/library/azure/dn261237.aspx).

Aby uzyskać więcej informacji na temat hello interfejsu API REST obiektów Blob, zobacz [interfejsu API REST usługi Blob](https://msdn.microsoft.com/library/azure/dd135733.aspx).

Aby hello najnowsze informacje dotyczące usługi Magazyn Microsoft Azure, odwiedź toohello [Blog zespołu usługi Magazyn Microsoft Azure](http://blogs.msdn.com/b/windowsazurestorage/).
