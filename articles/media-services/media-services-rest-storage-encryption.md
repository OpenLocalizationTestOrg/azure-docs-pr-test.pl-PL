---
title: "Szyfrowanie zawartości przy użyciu szyfrowania magazynu przy użyciu interfejsu API REST usług AMS"
description: "Dowiedz się, jak szyfrowanie zawartości przy użyciu szyfrowania magazynu przy użyciu interfejsów API REST usługi AMS."
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: a0a79f3d-76a1-4994-9202-59b91a2230e0
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/10/2017
ms.author: juliako
ms.openlocfilehash: 1979f5bf5e8cab88dab5fba49018afacf24504b3
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
# <a name="encrypting-your-content-with-storage-encryption"></a><span data-ttu-id="38a30-103">Szyfrowanie zawartości przy użyciu szyfrowania magazynu</span><span class="sxs-lookup"><span data-stu-id="38a30-103">Encrypting your content with storage encryption</span></span>

<span data-ttu-id="38a30-104">Zdecydowanie zaleca się do szyfrowania treści lokalnie przy użyciu standardu AES 256-bitowego i przekaż go do magazynu Azure którym będzie przechowywany szyfrowane, gdy.</span><span class="sxs-lookup"><span data-stu-id="38a30-104">It is highly recommended to encrypt your content locally using AES-256 bit encryption and then upload it to Azure Storage where it will be stored encrypted at rest.</span></span>

<span data-ttu-id="38a30-105">Ten artykuł zawiera omówienie usług AMS szyfrowanie magazynu i pokazuje, jak przekazywać zawartość szyfrowany w magazynie:</span><span class="sxs-lookup"><span data-stu-id="38a30-105">This article gives an overview of AMS storage encryption and shows you how to upload the storage encrypted content:</span></span>

* <span data-ttu-id="38a30-106">Utwórz klucz zawartości.</span><span class="sxs-lookup"><span data-stu-id="38a30-106">Create a content key.</span></span>
* <span data-ttu-id="38a30-107">Utwórz zasób.</span><span class="sxs-lookup"><span data-stu-id="38a30-107">Create an Asset.</span></span> <span data-ttu-id="38a30-108">Ustaw AssetCreationOption StorageEncryption podczas tworzenia zasobu.</span><span class="sxs-lookup"><span data-stu-id="38a30-108">Set the AssetCreationOption to StorageEncryption when creating the Asset.</span></span>
  
     <span data-ttu-id="38a30-109">Zaszyfrowane zasoby ma zostać skojarzony z kluczy zawartości.</span><span class="sxs-lookup"><span data-stu-id="38a30-109">Encrypted assets have to be associated with content keys.</span></span>
* <span data-ttu-id="38a30-110">Połącz klucz zawartości do elementu zawartości.</span><span class="sxs-lookup"><span data-stu-id="38a30-110">Link the content key to the asset.</span></span>  
* <span data-ttu-id="38a30-111">Szyfrowanie zestawu parametrów na jednostkach AssetFile dotyczących.</span><span class="sxs-lookup"><span data-stu-id="38a30-111">Set the encryption related parameters on the AssetFile entities.</span></span>

## <a name="considerations"></a><span data-ttu-id="38a30-112">Zagadnienia do rozważenia</span><span class="sxs-lookup"><span data-stu-id="38a30-112">Considerations</span></span> 

<span data-ttu-id="38a30-113">Jeśli chcesz dostarczyć zasób zaszyfrowanych magazynu, należy skonfigurować zasady dostarczania elementu zawartości.</span><span class="sxs-lookup"><span data-stu-id="38a30-113">If you want to deliver a storage encrypted asset, you must configure the asset’s delivery policy.</span></span> <span data-ttu-id="38a30-114">Przed zawartości mogą być przesyłane strumieniowo, serwer przesyłania strumieniowego usuwa szyfrowanie magazynu i strumieni zawartości przy użyciu zasady dostarczania określony.</span><span class="sxs-lookup"><span data-stu-id="38a30-114">Before your asset can be streamed, the streaming server removes the storage encryption and streams your content using the specified delivery policy.</span></span> <span data-ttu-id="38a30-115">Aby uzyskać więcej informacji, zobacz [Konfigurowanie zasad dostarczania zasobów](media-services-rest-configure-asset-delivery-policy.md).</span><span class="sxs-lookup"><span data-stu-id="38a30-115">For more information, see [Configuring Asset Delivery Policies](media-services-rest-configure-asset-delivery-policy.md).</span></span>

<span data-ttu-id="38a30-116">Podczas uzyskiwania dostępu do obiektów w usłudze Media Services, należy ustawić określonych pól nagłówka i wartości w Twoich żądań HTTP.</span><span class="sxs-lookup"><span data-stu-id="38a30-116">When accessing entities in Media Services, you must set specific header fields and values in your HTTP requests.</span></span> <span data-ttu-id="38a30-117">Aby uzyskać więcej informacji, zobacz [ustawień dla rozwoju interfejsu API REST usługi Media](media-services-rest-how-to-use.md).</span><span class="sxs-lookup"><span data-stu-id="38a30-117">For more information, see [Setup for Media Services REST API Development](media-services-rest-how-to-use.md).</span></span> 

## <a name="connect-to-media-services"></a><span data-ttu-id="38a30-118">Łączenie się z usługą Media Services</span><span class="sxs-lookup"><span data-stu-id="38a30-118">Connect to Media Services</span></span>

<span data-ttu-id="38a30-119">Aby uzyskać informacje na temat nawiązywania połączenia z interfejsu API usług AMS, zobacz [dostępu Azure Media Services API przy użyciu uwierzytelniania usługi Azure AD](media-services-use-aad-auth-to-access-ams-api.md).</span><span class="sxs-lookup"><span data-stu-id="38a30-119">For information on how to connect to the AMS API, see [Access the Azure Media Services API with Azure AD authentication](media-services-use-aad-auth-to-access-ams-api.md).</span></span> 

>[!NOTE]
><span data-ttu-id="38a30-120">Po pomyślnym połączeniu się https://media.windows.net, otrzymasz 301 przekierowanie, określając inny identyfikator URI usługi multimediów.</span><span class="sxs-lookup"><span data-stu-id="38a30-120">After successfully connecting to https://media.windows.net, you will receive a 301 redirect specifying another Media Services URI.</span></span> <span data-ttu-id="38a30-121">Upewnij się kolejne wywołania nowy identyfikator URI.</span><span class="sxs-lookup"><span data-stu-id="38a30-121">You must make subsequent calls to the new URI.</span></span>

## <a name="storage-encryption-overview"></a><span data-ttu-id="38a30-122">Omówienie szyfrowania magazynu</span><span class="sxs-lookup"><span data-stu-id="38a30-122">Storage encryption overview</span></span>
<span data-ttu-id="38a30-123">Zastosowanie szyfrowania magazynu AMS **Ewidencyjne AES** tryb szyfrowanie całego pliku.</span><span class="sxs-lookup"><span data-stu-id="38a30-123">The AMS storage encryption applies **AES-CTR** mode encryption to the entire file.</span></span>  <span data-ttu-id="38a30-124">Tryb Ewidencyjne AES jest szyfry blokowe, który można zaszyfrować dane o dowolnej długości bez potrzeby dopełnienia.</span><span class="sxs-lookup"><span data-stu-id="38a30-124">AES-CTR mode is a block cipher that can encrypt arbitrary length data without need for padding.</span></span> <span data-ttu-id="38a30-125">Działa on tak szyfrując z algorytmu AES, a następnie używać XOR dane wyjściowe AES z danymi można zaszyfrować lub odszyfrować bloku licznika.</span><span class="sxs-lookup"><span data-stu-id="38a30-125">It operates by encrypting a counter block with the AES algorithm and then XOR-ing the output of AES with the data to encrypt or decrypt.</span></span>  <span data-ttu-id="38a30-126">Blok licznika używany jest tworzony przez skopiowanie wartości InitializationVector bajtów 0 do 7 wartość licznika i bajtów 8 do 15 wartość licznika jest ustawiana wartość zero.</span><span class="sxs-lookup"><span data-stu-id="38a30-126">The counter block used is constructed by copying the value of the InitializationVector to bytes 0 to 7 of the counter value and bytes 8 to 15 of the counter value are set to zero.</span></span> <span data-ttu-id="38a30-127">16 bajtów bloku licznika bajtów 8 do 15 (tj. najmniej znaczący bajtów) są używane jako proste 64-bitowych unsigned liczba całkowita, która jest zwiększany o jeden dla każdego kolejnych bloków danych przetwarzane i jest przechowywany w kolejności bajtów sieci.</span><span class="sxs-lookup"><span data-stu-id="38a30-127">Of the 16 byte counter block, bytes 8 to 15 (i.e. the least significant bytes) are used as a simple 64 bit unsigned integer that is incremented by one for each subsequent block of data processed and is kept in network byte order.</span></span> <span data-ttu-id="38a30-128">Należy pamiętać, że jeśli ta liczba całkowita osiągnie wartość maksymalna (0xFFFFFFFFFFFFFFFF) zwiększanie go po Resetuje licznik bloku zero (bajtów 8 do 15) bez wpływu na inne 64-bitowy licznika (tj. w bajtach 0-7).</span><span class="sxs-lookup"><span data-stu-id="38a30-128">Note that if this integer reaches the maximum value (0xFFFFFFFFFFFFFFFF) then incrementing it resets the block counter to zero (bytes 8 to 15) without affecting the other 64 bits of the counter (i.e. bytes 0 to 7).</span></span>   <span data-ttu-id="38a30-129">Aby zachować bezpieczeństwo szyfrowania tryb Ewidencyjne AES, wartość InitializationVector danym identyfikatorem klucza dla każdego klucza zawartości jest unikatowy dla każdego pliku i plików jest mniejsza niż wartość 2 ^ 64 bloki o długości.</span><span class="sxs-lookup"><span data-stu-id="38a30-129">In order to maintain the security of the AES-CTR mode encryption, the InitializationVector value for a given Key Identifier for each content key shall be unique for each file and files shall be less than 2^64 blocks in length.</span></span>  <span data-ttu-id="38a30-130">To, aby upewnić się, że wartość licznika nigdy nie jest ponownie z danym kluczem.</span><span class="sxs-lookup"><span data-stu-id="38a30-130">This is to ensure that a counter value is never reused with a given key.</span></span> <span data-ttu-id="38a30-131">Aby uzyskać więcej informacji o trybie kont Zobacz [tej strony typu wiki](https://en.wikipedia.org/wiki/Block_cipher_mode_of_operation#CTR) (Artykuł typu wiki używany jest termin "Nonce" zamiast "InitializationVector").</span><span class="sxs-lookup"><span data-stu-id="38a30-131">For more information about the CTR mode, see [this wiki page](https://en.wikipedia.org/wiki/Block_cipher_mode_of_operation#CTR) (the wiki article uses the term "Nonce" instead of "InitializationVector").</span></span>

<span data-ttu-id="38a30-132">Użyj **szyfrowanie magazynu** do zaszyfrowania zawartości lokalnie przy użyciu standardu AES 256-bitowy szyfrowania i przekaż go do magazynu Azure gdzie jest przechowywana szyfrowane, gdy.</span><span class="sxs-lookup"><span data-stu-id="38a30-132">Use **Storage Encryption** to encrypt your clear content locally using AES-256 bit encryption and then upload it to Azure Storage where it is stored encrypted at rest.</span></span> <span data-ttu-id="38a30-133">Elementy zawartości chronione przy użyciu szyfrowania magazynu są automatycznie odszyfrowywane i umieszczane w systemie szyfrowania plików przed kodowaniem, a następnie opcjonalnie ponownie szyfrowane przed przesłaniem zwrotnym w formie nowego elementu zawartości wyjściowej.</span><span class="sxs-lookup"><span data-stu-id="38a30-133">Assets protected with storage encryption are automatically unencrypted and placed in an encrypted file system prior to encoding, and optionally re-encrypted prior to uploading back as a new output asset.</span></span> <span data-ttu-id="38a30-134">Pierwotnym zastosowaniem szyfrowania magazynu jest, gdy chcesz zabezpieczyć z wysokiej jakości multimedialnych plików wejściowych pomocą silnego szyfrowania przechowywanych na dysku.</span><span class="sxs-lookup"><span data-stu-id="38a30-134">The primary use case for storage encryption is when you want to secure your high quality input media files with strong encryption at rest on disk.</span></span>

<span data-ttu-id="38a30-135">Aby dostarczyć zasób zaszyfrowanych magazynu, należy skonfigurować zasady dostarczania elementu zawartości będzie wówczas traktował Media Services sposób dostarczania zawartości.</span><span class="sxs-lookup"><span data-stu-id="38a30-135">In order to deliver a storage encrypted asset, you must configure the asset’s delivery policy so Media Services knows how you want to deliver your content.</span></span> <span data-ttu-id="38a30-136">Przed zawartości mogą być przesyłane strumieniowo, serwer przesyłania strumieniowego usuwa szyfrowanie magazynu i strumieni zawartości za pomocą zasad określonym dostarczania (na przykład AES, wspólnego szyfrowania lub bez szyfrowania).</span><span class="sxs-lookup"><span data-stu-id="38a30-136">Before your asset can be streamed, the streaming server removes the storage encryption and streams your content using the specified delivery policy (for example, AES, common encryption, or no encryption).</span></span>

## <a name="create-contentkeys-used-for-encryption"></a><span data-ttu-id="38a30-137">Utwórz ContentKeys używany do szyfrowania</span><span class="sxs-lookup"><span data-stu-id="38a30-137">Create ContentKeys used for encryption</span></span>
<span data-ttu-id="38a30-138">Zaszyfrowanych zasoby ma zostać skojarzony z klucz szyfrowania magazynu.</span><span class="sxs-lookup"><span data-stu-id="38a30-138">Encrypted assets have to be associated with Storage Encryption key.</span></span> <span data-ttu-id="38a30-139">Należy utworzyć klucz zawartości do użycia dla szyfrowania przed utworzeniem plików zasobów.</span><span class="sxs-lookup"><span data-stu-id="38a30-139">You must create the content key to be used for encryption before creating the asset files.</span></span> <span data-ttu-id="38a30-140">Ta sekcja zawiera opis sposobu tworzenia klucza zawartości.</span><span class="sxs-lookup"><span data-stu-id="38a30-140">This section describes how to create a content key.</span></span>

<span data-ttu-id="38a30-141">Poniżej przedstawiono ogólne kroki podczas generowania zawartości kluczy, które skojarzysz z zasobów, które mają być szyfrowane.</span><span class="sxs-lookup"><span data-stu-id="38a30-141">The following are general steps for generating content keys that you will associate with assets that you want to be encrypted.</span></span> 

1. <span data-ttu-id="38a30-142">Do szyfrowania magazynu losowego generowania klucza AES 32 bajtów.</span><span class="sxs-lookup"><span data-stu-id="38a30-142">For storage encryption, randomly generate a 32-byte AES key.</span></span> 
   
    <span data-ttu-id="38a30-143">Są to klucz zawartości dla zawartości, co oznacza, że wszystkie pliki skojarzone z tym zasobów będą musieli używać tego samego klucza zawartości podczas odszyfrowywania.</span><span class="sxs-lookup"><span data-stu-id="38a30-143">This will be the content key for your asset, which means all files associated with that asset will need to use the same content key during decryption.</span></span> 
2. <span data-ttu-id="38a30-144">Wywołanie [GetProtectionKeyId](https://docs.microsoft.com/rest/api/media/operations/rest-api-functions#getprotectionkeyid) i [GetProtectionKey](https://msdn.microsoft.com/library/azure/jj683097.aspx#getprotectionkey) metod, aby uzyskać poprawny certyfikat X.509 używany do szyfrowania klucza zawartości.</span><span class="sxs-lookup"><span data-stu-id="38a30-144">Call the [GetProtectionKeyId](https://docs.microsoft.com/rest/api/media/operations/rest-api-functions#getprotectionkeyid) and [GetProtectionKey](https://msdn.microsoft.com/library/azure/jj683097.aspx#getprotectionkey) methods to get the correct X.509 Certificate that must be used to encrypt your content key.</span></span>
3. <span data-ttu-id="38a30-145">Zaszyfrowanie klucza zawartości z kluczem publicznym certyfikatu X.509.</span><span class="sxs-lookup"><span data-stu-id="38a30-145">Encrypt your content key with the public key of the X.509 Certificate.</span></span> 
   
   <span data-ttu-id="38a30-146">.NET SDK usługi Media Services używa algorytmu RSA z OAEP podczas operacji szyfrowania.</span><span class="sxs-lookup"><span data-stu-id="38a30-146">Media Services .NET SDK uses RSA with OAEP when doing the encryption.</span></span>  <span data-ttu-id="38a30-147">Widoczny jest przykład .NET w [funkcja EncryptSymmetricKeyData](https://github.com/Azure/azure-sdk-for-media-services/blob/dev/src/net/Client/Common/Common.FileEncryption/EncryptionUtils.cs).</span><span class="sxs-lookup"><span data-stu-id="38a30-147">You can see a .NET example in the [EncryptSymmetricKeyData function](https://github.com/Azure/azure-sdk-for-media-services/blob/dev/src/net/Client/Common/Common.FileEncryption/EncryptionUtils.cs).</span></span>
4. <span data-ttu-id="38a30-148">Utwórz wartość sumy kontrolnej obliczane przy użyciu klucza identyfikator i klucz zawartości.</span><span class="sxs-lookup"><span data-stu-id="38a30-148">Create a checksum value calculated using the key identifier and content key.</span></span> <span data-ttu-id="38a30-149">W poniższym przykładzie .NET oblicza sumę kontrolną, używając identyfikatora GUID części klucza identyfikator i klucz czyszczenie zawartości.</span><span class="sxs-lookup"><span data-stu-id="38a30-149">The following .NET example calculates the checksum using the GUID part of the key identifier and the clear content key.</span></span>

        public static string CalculateChecksum(byte[] contentKey, Guid keyId)
        {
            const int ChecksumLength = 8;
            const int KeyIdLength = 16;

            byte[] encryptedKeyId = null;

            // Checksum is computed by AES-ECB encrypting the KID
            // with the content key.
            using (AesCryptoServiceProvider rijndael = new AesCryptoServiceProvider())
            {
                rijndael.Mode = CipherMode.ECB;
                rijndael.Key = contentKey;
                rijndael.Padding = PaddingMode.None;

                ICryptoTransform encryptor = rijndael.CreateEncryptor();
                encryptedKeyId = new byte[KeyIdLength];
                encryptor.TransformBlock(keyId.ToByteArray(), 0, KeyIdLength, encryptedKeyId, 0);
            }

            byte[] retVal = new byte[ChecksumLength];
            Array.Copy(encryptedKeyId, retVal, ChecksumLength);

            return Convert.ToBase64String(retVal);
        }

1. <span data-ttu-id="38a30-150">Utwórz klucz zawartości z **EncryptedContentKey** (konwertowana na ciąg kodowany w formacie base64), **ProtectionKeyId**, **ProtectionKeyType**,  **ContentKeyType**, i **sumy kontrolnej** wartości otrzymany w poprzednich krokach.</span><span class="sxs-lookup"><span data-stu-id="38a30-150">Create the Content key with the **EncryptedContentKey** (converted to base64-encoded string), **ProtectionKeyId**, **ProtectionKeyType**, **ContentKeyType**, and **Checksum** values you have received in previous steps.</span></span>

    <span data-ttu-id="38a30-151">Do szyfrowania magazynu powinien znajdować się następujące właściwości, w treści żądania.</span><span class="sxs-lookup"><span data-stu-id="38a30-151">For storage encryption, the following properties should be included in the request body.</span></span>

    <span data-ttu-id="38a30-152">Właściwość treść żądania</span><span class="sxs-lookup"><span data-stu-id="38a30-152">Request body property</span></span>    | <span data-ttu-id="38a30-153">Opis</span><span class="sxs-lookup"><span data-stu-id="38a30-153">Description</span></span>
    ---|---
    <span data-ttu-id="38a30-154">Identyfikator</span><span class="sxs-lookup"><span data-stu-id="38a30-154">Id</span></span> | <span data-ttu-id="38a30-155">Identyfikator ContentKey, który mamy nad Generowanie w następującym formacie, "nb:kid:UUID:<NEW GUID>".</span><span class="sxs-lookup"><span data-stu-id="38a30-155">The ContentKey Id which we generate ourselves using the following format, “nb:kid:UUID:<NEW GUID>”.</span></span>
    <span data-ttu-id="38a30-156">ContentKeyType</span><span class="sxs-lookup"><span data-stu-id="38a30-156">ContentKeyType</span></span> | <span data-ttu-id="38a30-157">Typ klucza zawartości jest liczbą całkowitą dla tego klucza zawartości.</span><span class="sxs-lookup"><span data-stu-id="38a30-157">This is the content key type as an integer for this content key.</span></span> <span data-ttu-id="38a30-158">Wartość 1 dla szyfrowania magazynu jest przekazywana.</span><span class="sxs-lookup"><span data-stu-id="38a30-158">We pass the value 1 for storage encryption.</span></span>
    <span data-ttu-id="38a30-159">EncryptedContentKey</span><span class="sxs-lookup"><span data-stu-id="38a30-159">EncryptedContentKey</span></span> | <span data-ttu-id="38a30-160">Utworzymy nową wartość klucza zawartości, która jest wartością 256-bitowego (32 bajtów).</span><span class="sxs-lookup"><span data-stu-id="38a30-160">We create a new content key value which is a 256-bit (32 byte) value.</span></span> <span data-ttu-id="38a30-161">Klucz jest zaszyfrowany przy użyciu certyfikatu X.509 szyfrowania magazynu, którego możemy pobrać Microsoft Azure Media Services, wykonując żądanie HTTP GET dla GetProtectionKeyId i metod GetProtectionKey.</span><span class="sxs-lookup"><span data-stu-id="38a30-161">The key is encrypted using the storage encryption X.509 certificate which we retrieve from Microsoft Azure Media Services by executing a HTTP GET request for the GetProtectionKeyId and GetProtectionKey Methods.</span></span> <span data-ttu-id="38a30-162">Na przykład zobacz następujący kod .NET: **EncryptSymmetricKeyData** metody zdefiniowanej [tutaj](https://github.com/Azure/azure-sdk-for-media-services/blob/dev/src/net/Client/Common/Common.FileEncryption/EncryptionUtils.cs).</span><span class="sxs-lookup"><span data-stu-id="38a30-162">As an example, see the following .NET code: the  **EncryptSymmetricKeyData** method defined [here](https://github.com/Azure/azure-sdk-for-media-services/blob/dev/src/net/Client/Common/Common.FileEncryption/EncryptionUtils.cs).</span></span>
    <span data-ttu-id="38a30-163">ProtectionKeyId</span><span class="sxs-lookup"><span data-stu-id="38a30-163">ProtectionKeyId</span></span> | <span data-ttu-id="38a30-164">To jest identyfikator klucza ochrony dla magazynu certyfikatu X.509 szyfrowania, który został użyty do zaszyfrowania naszych klucz zawartości.</span><span class="sxs-lookup"><span data-stu-id="38a30-164">This is the protection key id for the storage encryption X.509 certificate that was used to encrypt our content key.</span></span>
    <span data-ttu-id="38a30-165">ProtectionKeyType</span><span class="sxs-lookup"><span data-stu-id="38a30-165">ProtectionKeyType</span></span> | <span data-ttu-id="38a30-166">Jest to typ szyfrowania dla klucza ochrony, który był używany do szyfrowania klucza zawartości.</span><span class="sxs-lookup"><span data-stu-id="38a30-166">This is the encryption type for the protection key that was used to encrypt the content key.</span></span> <span data-ttu-id="38a30-167">Ta wartość jest StorageEncryption(1) w naszym przykładzie.</span><span class="sxs-lookup"><span data-stu-id="38a30-167">This value is StorageEncryption(1) for our example.</span></span>
    <span data-ttu-id="38a30-168">Sumy kontrolnej</span><span class="sxs-lookup"><span data-stu-id="38a30-168">Checksum</span></span> |<span data-ttu-id="38a30-169">Obliczony sumy kontrolnej MD5 dla klucza zawartości.</span><span class="sxs-lookup"><span data-stu-id="38a30-169">The MD5 calculated checksum for the content key.</span></span> <span data-ttu-id="38a30-170">Jest ona obliczana przez szyfrowanie identyfikatora zawartości przy użyciu klucza zawartości.</span><span class="sxs-lookup"><span data-stu-id="38a30-170">It is computed by encrypting the content Id with the content key.</span></span> <span data-ttu-id="38a30-171">Przykład kodu pokazuje, jak można obliczyć sumy kontrolnej.</span><span class="sxs-lookup"><span data-stu-id="38a30-171">The example code demonstrates how to calculate the checksum.</span></span>


### <a name="retrieve-the-protectionkeyid"></a><span data-ttu-id="38a30-172">Pobrać ProtectionKeyId</span><span class="sxs-lookup"><span data-stu-id="38a30-172">Retrieve the ProtectionKeyId</span></span>
<span data-ttu-id="38a30-173">Poniższy przykład pokazuje, jak pobrać ProtectionKeyId, odcisk palca certyfikatu, dla certyfikatu, którego należy użyć w przypadku szyfrowania kluczem zawartości.</span><span class="sxs-lookup"><span data-stu-id="38a30-173">The following example shows how to retrieve the ProtectionKeyId, a certificate thumbprint, for the certificate you must use when encrypting your content key.</span></span> <span data-ttu-id="38a30-174">Wykonaj ten krok, aby się upewnić, że już ma odpowiedniego certyfikatu na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="38a30-174">Do this step to make sure that you already have the appropriate certificate on your machine.</span></span>

<span data-ttu-id="38a30-175">Żądanie:</span><span class="sxs-lookup"><span data-stu-id="38a30-175">Request:</span></span>

    GET https://media.windows.net/api/GetProtectionKeyId?contentKeyType=0 HTTP/1.1
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    User-Agent: Microsoft ADO.NET Data Services
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=juliakoams1&urn%3aSubscriptionId=zbbef702-2233-477b-9f16-bc4d3aa97387&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1423034908&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=7eSLe1GHnxgilr3F2FPCGxdL2%2bwy%2f39XhMPGY9IizfU%3d
    x-ms-version: 2.11
    Host: media.windows.net

<span data-ttu-id="38a30-176">Odpowiedź:</span><span class="sxs-lookup"><span data-stu-id="38a30-176">Response:</span></span>

    HTTP/1.1 200 OK
    Cache-Control: no-cache
    Content-Length: 139
    Content-Type: application/json;odata=minimalmetadata;streaming=true;charset=utf-8
    Server: Microsoft-IIS/8.5
    request-id: 2b6aa7a4-3a09-4b08-b581-26b55667f817
    x-ms-request-id: 2b6aa7a4-3a09-4b08-b581-26b55667f817
    X-Content-Type-Options: nosniff
    DataServiceVersion: 3.0;
    X-Powered-By: ASP.NET
    Strict-Transport-Security: max-age=31536000; includeSubDomains
    Date: Wed, 04 Feb 2015 02:42:52 GMT

    {"odata.metadata":"https://wamsbayclus001rest-hs.cloudapp.net/api/$metadata#Edm.String","value":"7D9BB04D9D0A4A24800CADBFEF232689E048F69C"}

### <a name="retrieve-the-protectionkey-for-the-protectionkeyid"></a><span data-ttu-id="38a30-177">Pobrać ProtectionKey ProtectionKeyId</span><span class="sxs-lookup"><span data-stu-id="38a30-177">Retrieve the ProtectionKey for the ProtectionKeyId</span></span>
<span data-ttu-id="38a30-178">Poniższy przykład pokazuje, jak można pobrać certyfikatu X.509 przy użyciu ProtectionKeyId otrzymanego w poprzednim kroku.</span><span class="sxs-lookup"><span data-stu-id="38a30-178">The following example shows how to retrieve the X.509 certificate using the ProtectionKeyId you received in the previous step.</span></span>

<span data-ttu-id="38a30-179">Żądanie:</span><span class="sxs-lookup"><span data-stu-id="38a30-179">Request:</span></span>

    GET https://media.windows.net/api/GetProtectionKey?ProtectionKeyId='7D9BB04D9D0A4A24800CADBFEF232689E048F69C' HTTP/1.1
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    User-Agent: Microsoft ADO.NET Data Services
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=juliakoams1&urn%3aSubscriptionId=zbbef702-e769-2233-9f16-bc4d3aa97387&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1423141026&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=lDBz5YXKiWe5L7eXOHsLHc9kKEUcUiFJvrNFFSksgkM%3d
    x-ms-version: 2.11
    x-ms-client-request-id: 78d1247a-58d7-40e5-96cc-70ff0dfa7382
    Host: media.windows.net

<span data-ttu-id="38a30-180">Odpowiedź:</span><span class="sxs-lookup"><span data-stu-id="38a30-180">Response:</span></span>

    HTTP/1.1 200 OK
    Cache-Control: no-cache
    Content-Length: 1227
    Content-Type: application/json;odata=minimalmetadata;streaming=true;charset=utf-8
    Server: Microsoft-IIS/8.5
    x-ms-client-request-id: 78d1247a-58d7-40e5-96cc-70ff0dfa7382
    request-id: 1523e8f3-8ed2-40fe-8a9a-5d81eb572cc8
    x-ms-request-id: 1523e8f3-8ed2-40fe-8a9a-5d81eb572cc8
    X-Content-Type-Options: nosniff
    DataServiceVersion: 3.0;
    X-Powered-By: ASP.NET
    Strict-Transport-Security: max-age=31536000; includeSubDomains
    Date: Thu, 05 Feb 2015 07:52:30 GMT

    {"odata.metadata":"https://wamsbayclus001rest-hs.cloudapp.net/api/$metadata#Edm.String",
    "value":"MIIDSTCCAjGgAwIBAgIQqf92wku/HLJGCbMAU8GEnDANBgkqhkiG9w0BAQQFADAuMSwwKgYDVQQDEyN3YW1zYmx1cmVnMDAxZW5jcnlwdGFsbHNlY3JldHMtY2VydDAeFw0xMjA1MjkwNzAwMDBaFw0zMjA1MjkwNzAwMDBaMC4xLDAqBgNVBAMTI3dhbXNibHVyZWcwMDFlbmNyeXB0YWxsc2VjcmV0cy1jZXJ0MIIBIjANBgkqhkiG9w0BAQEFAAOCAQ8AMIIBCgKCAQEAzR0SEbXefvUjb9wCUfkEiKtGQ5Gc328qFPrhMjSo+YHe0AVviZ9YaxPPb0m1AaaRV4dqWpST2+JtDhLOmGpWmmA60tbATJDdmRzKi2eYAyhhE76MgJgL3myCQLP42jDusWXWSMabui3/tMDQs+zfi1sJ4Ch/lm5EvksYsu6o8sCv29VRwxfDLJPBy2NlbV4GbWz5Qxp2tAmHoROnfaRhwp6WIbquk69tEtu2U50CpPN2goLAqx2PpXAqA+prxCZYGTHqfmFJEKtZHhizVBTFPGS3ncfnQC9QIEwFbPw6E5PO5yNaB68radWsp5uvDg33G1i8IT39GstMW6zaaG7cNQIDAQABo2MwYTBfBgNVHQEEWDBWgBCOGT2hPhsvQioZimw8M+jOoTAwLjEsMCoGA1UEAxMjd2Ftc2JsdXJlZzAwMWVuY3J5cHRhbGxzZWNyZXRzLWNlcnSCEKn/dsJLvxyyRgmzAFPBhJwwDQYJKoZIhvcNAQEEBQADggEBABcrQPma2ekNS3Wc5wGXL/aHyQaQRwFGymnUJ+VR8jVUZaC/U/f6lR98eTlwycjVwRL7D15BfClGEHw66QdHejaViJCjbEIJJ3p2c9fzBKhjLhzB3VVNiLIaH6RSI1bMPd2eddSCqhDIn3VBN605GcYXMzhYp+YA6g9+YMNeS1b+LxX3fqixMQIxSHOLFZ1G/H2xfNawv0VikH3djNui3EKT1w/8aRkUv/AAV0b3rYkP/jA1I0CPn0XFk7STYoiJ3gJoKq9EMXhit+Iwfz0sMkfhWG12/XO+TAWqsK1ZxEjuC9OzrY7pFnNxs4Mu4S8iinehduSpY+9mDd3dHynNwT4="}

### <a name="create-the-content-key"></a><span data-ttu-id="38a30-181">Utwórz klucz zawartości</span><span class="sxs-lookup"><span data-stu-id="38a30-181">Create the content key</span></span>
<span data-ttu-id="38a30-182">Po pobrać certyfikat X.509 i używać swojego klucza publicznego do szyfrowania klucza zawartości należy utworzyć **ContentKey** jednostki i ustaw jej właściwość odpowiednio wartości.</span><span class="sxs-lookup"><span data-stu-id="38a30-182">After you have retrieved the X.509 certificate and used its public key to encrypt your content key, create a **ContentKey** entity and set its property values accordingly.</span></span>

<span data-ttu-id="38a30-183">Jedna z wartości, że należy ustawić podczas tworzenia zawartości klucza jest typem.</span><span class="sxs-lookup"><span data-stu-id="38a30-183">One of the values that you must set when create the content key is the type.</span></span> <span data-ttu-id="38a30-184">W przypadku szyfrowania magazynu wartość "1".</span><span class="sxs-lookup"><span data-stu-id="38a30-184">In case of the storage encryption, the value is '1'.</span></span> 

<span data-ttu-id="38a30-185">Poniższy przykład przedstawia sposób tworzenia **ContentKey** z **ContentKeyType** ustawić szyfrowania magazynu ("1") i **ProtectionKeyType** ustawioną wartość "0", aby wskazać, że Klucz ochrony identyfikator jest odcisk palca certyfikatu X.509.</span><span class="sxs-lookup"><span data-stu-id="38a30-185">The following example shows how to create a **ContentKey** with a **ContentKeyType** set for storage encryption ("1") and the **ProtectionKeyType** set to "0" to indicate that the protection key Id is the X.509 certificate thumbprint.</span></span>  

<span data-ttu-id="38a30-186">Żądanie</span><span class="sxs-lookup"><span data-stu-id="38a30-186">Request</span></span>

    POST https://media.windows.net/api/ContentKeys HTTP/1.1
    Content-Type: application/json
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    User-Agent: Microsoft ADO.NET Data Services
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=juliakoams1&urn%3aSubscriptionId=zbbef702-2233-477b-9f16-bc4d3aa97387&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1423034908&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=7eSLe1GHnxgilr3F2FPCGxdL2%2bwy%2f39XhMPGY9IizfU%3d
    x-ms-version: 2.11
    Host: media.windows.net
    {
    "Name":"ContentKey",
    "ProtectionKeyId":"7D9BB04D9D0A4A24800CADBFEF232689E048F69C", 
    "ContentKeyType":"1", 
    "ProtectionKeyType":"0",
    "EncryptedContentKey":"your encrypted content key",
    "Checksum":"calculated checksum"
    }

<span data-ttu-id="38a30-187">Odpowiedź:</span><span class="sxs-lookup"><span data-stu-id="38a30-187">Response:</span></span>

    HTTP/1.1 201 Created
    Cache-Control: no-cache
    Content-Length: 777
    Content-Type: application/json;odata=minimalmetadata;streaming=true;charset=utf-8
    Location: https://media.windows.net/api/ContentKeys('nb%3Akid%3AUUID%3A9c8ea9c6-52bd-4232-8a43-8e43d8564a99')
    Server: Microsoft-IIS/8.5
    request-id: 76e85e0f-5cf1-44cb-b689-b3455888682c
    x-ms-request-id: 76e85e0f-5cf1-44cb-b689-b3455888682c
    X-Content-Type-Options: nosniff
    DataServiceVersion: 3.0;
    X-Powered-By: ASP.NET
    Strict-Transport-Security: max-age=31536000; includeSubDomains
    Date: Wed, 04 Feb 2015 02:37:46 GMT

    {"odata.metadata":"https://wamsbayclus001rest-hs.cloudapp.net/api/$metadata#ContentKeys/@Element",
    "Id":"nb:kid:UUID:9c8ea9c6-52bd-4232-8a43-8e43d8564a99","Created":"2015-02-04T02:37:46.9684379Z",
    "LastModified":"2015-02-04T02:37:46.9684379Z",
    "ContentKeyType":1,
    "EncryptedContentKey":"your encrypted content key",
    "Name":"ContentKey",
    "ProtectionKeyId":"7D9BB04D9D0A4A24800CADBFEF232689E048F69C",
    "ProtectionKeyType":0,
    "Checksum":"calculated checksum"}

## <a name="create-an-asset"></a><span data-ttu-id="38a30-188">Utwórz zasób</span><span class="sxs-lookup"><span data-stu-id="38a30-188">Create an asset</span></span>
<span data-ttu-id="38a30-189">Poniższy przykład pokazuje, jak utworzyć element zawartości.</span><span class="sxs-lookup"><span data-stu-id="38a30-189">The following example shows how to create an asset.</span></span>

<span data-ttu-id="38a30-190">**Żądania HTTP**</span><span class="sxs-lookup"><span data-stu-id="38a30-190">**HTTP Request**</span></span>

    POST https://media.windows.net/api/Assets HTTP/1.1
    Content-Type: application/json
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amstestaccount001&urn%3aSubscriptionId=z7f09258-6753-2233-b1ae-193798e2c9d8&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1421640053&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=vlG%2fPYdFDMS1zKc36qcFVWnaNh07UCkhYj3B71%2fk1YA%3d
    x-ms-version: 2.11
    Host: media.windows.net

    {"Name":"BigBuckBunny" "Options":1}

<span data-ttu-id="38a30-191">**Odpowiedź HTTP**</span><span class="sxs-lookup"><span data-stu-id="38a30-191">**HTTP Response**</span></span>

<span data-ttu-id="38a30-192">Jeśli to się powiedzie, jest zwracany następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="38a30-192">If successful, the following is returned:</span></span>

    HTP/1.1 201 Created
    Cache-Control: no-cache
    Content-Length: 452
    Content-Type: application/json;odata=minimalmetadata;streaming=true;charset=utf-8
    Location: https://wamsbayclus001rest-hs.cloudapp.net/api/Assets('nb%3Acid%3AUUID%3A9bc8ff20-24fb-4fdb-9d7c-b04c7ee573a1')
    Server: Microsoft-IIS/8.5
    x-ms-client-request-id: c59de965-bc89-4295-9a57-75d897e5221e
    request-id: e98be122-ae09-473a-8072-0ccd234a0657
    x-ms-request-id: e98be122-ae09-473a-8072-0ccd234a0657
    X-Content-Type-Options: nosniff
    DataServiceVersion: 3.0;
    Strict-Transport-Security: max-age=31536000; includeSubDomains
    Date: Sun, 18 Jan 2015 22:06:40 GMT
    {  
       "odata.metadata":"https://wamsbayclus001rest-hs.cloudapp.net/api/$metadata#Assets/@Element",
       "Id":"nb:cid:UUID:9bc8ff20-24fb-4fdb-9d7c-b04c7ee573a1",
       "State":0,
       "Created":"2015-01-18T22:06:40.6010903Z",
       "LastModified":"2015-01-18T22:06:40.6010903Z",
       "AlternateId":null,
       "Name":"BigBuckBunny.mp4",
       "Options":1,
       "Uri":"https://storagetestaccount001.blob.core.windows.net/asset-9bc8ff20-24fb-4fdb-9d7c-b04c7ee573a1",
       "StorageAccountName":"storagetestaccount001"
    }

## <a name="associate-the-contentkey-with-an-asset"></a><span data-ttu-id="38a30-193">Skojarz ContentKey z zasobów</span><span class="sxs-lookup"><span data-stu-id="38a30-193">Associate the ContentKey with an Asset</span></span>
<span data-ttu-id="38a30-194">Po utworzeniu ContentKey, skojarzyć ją z zawartości przy użyciu operacji $links, jak pokazano w poniższym przykładzie:</span><span class="sxs-lookup"><span data-stu-id="38a30-194">After creating the ContentKey, associate it with your Asset using the $links operation, as shown in the following example:</span></span>

<span data-ttu-id="38a30-195">Żądanie:</span><span class="sxs-lookup"><span data-stu-id="38a30-195">Request:</span></span>

    POST https://media.windows.net/api/Assets('nb%3Acid%3AUUID%3Afbd7ce05-1087-401b-aaae-29f16383c801')/$links/ContentKeys HTTP/1.1
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    Content-Type: application/json
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=juliakoams1&urn%3aSubscriptionId=zbbef702-2233-477b-9f16-bc4d3aa97387&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1423141026&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=lDBz5YXKiWe5L7eXOHsLHc9kKEUcUiFJvrNFFSksgkM%3d
    x-ms-version: 2.11
    Host: media.windows.net

    {"uri":"https://wamsbayclus001rest-hs.cloudapp.net/api/ContentKeys('nb%3Akid%3AUUID%3A01e6ea36-2285-4562-91f1-82c45736047c')"}

<span data-ttu-id="38a30-196">Odpowiedź:</span><span class="sxs-lookup"><span data-stu-id="38a30-196">Response:</span></span>

    HTTP/1.1 204 No Content 

## <a name="create-an-assetfile"></a><span data-ttu-id="38a30-197">Utwórz AssetFile</span><span class="sxs-lookup"><span data-stu-id="38a30-197">Create an AssetFile</span></span>
<span data-ttu-id="38a30-198">[AssetFile](https://docs.microsoft.com/rest/api/media/operations/assetfile) jednostki reprezentuje plik wideo lub audio, który jest przechowywany w kontenerze obiektów blob.</span><span class="sxs-lookup"><span data-stu-id="38a30-198">The [AssetFile](https://docs.microsoft.com/rest/api/media/operations/assetfile) entity represents a video or audio file that is stored in a blob container.</span></span> <span data-ttu-id="38a30-199">Plik zasobów zawsze jest skojarzony z zasobem i zasobów może zawierać jeden lub wiele plików zasobów.</span><span class="sxs-lookup"><span data-stu-id="38a30-199">An asset file is always associated with an asset, and an asset may contain one or many asset files.</span></span> <span data-ttu-id="38a30-200">Zadanie Media Encoder usługi nie powiedzie się, jeśli obiekt pliku zasobu nie jest skojarzony z pliku cyfrowego w kontenerze obiektów blob.</span><span class="sxs-lookup"><span data-stu-id="38a30-200">The Media Services Encoder task fails if an asset file object is not associated with a digital file in a blob container.</span></span>

<span data-ttu-id="38a30-201">Należy pamiętać, że **AssetFile** wystąpienia oraz plik multimedialna są dwa różne obiekty.</span><span class="sxs-lookup"><span data-stu-id="38a30-201">Note that the **AssetFile** instance and the actual media file are two distinct objects.</span></span> <span data-ttu-id="38a30-202">Wystąpienia AssetFile zawiera metadanych dotyczących pliku nośnika, a plik nośnika zawiera zawartość multimedialna.</span><span class="sxs-lookup"><span data-stu-id="38a30-202">The AssetFile instance contains metadata about the media file, while the media file contains the actual media content.</span></span>

<span data-ttu-id="38a30-203">Po przekazaniu pliku nośnika cyfrowego do kontenera obiektów blob, którego użyjesz **scalania** żądania HTTP w celu zaktualizowania AssetFile informacje o pliku nośnika (niewidoczny w tym temacie).</span><span class="sxs-lookup"><span data-stu-id="38a30-203">After you upload your digital media file into a blob container, you will use the **MERGE** HTTP request to update the AssetFile with information about your media file (not shown in this topic).</span></span> 

<span data-ttu-id="38a30-204">**Żądania HTTP**</span><span class="sxs-lookup"><span data-stu-id="38a30-204">**HTTP Request**</span></span>

    POST https://media.windows.net/api/Files HTTP/1.1
    Content-Type: application/json
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amstestaccount001&urn%3aSubscriptionId=z7f09258-6753-4ca2-2233-193798e2c9d8&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1421640053&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=vlG%2fPYdFDMS1zKc36qcFVWnaNh07UCkhYj3B71%2fk1YA%3d
    x-ms-version: 2.11
    Host: media.windows.net
    Content-Length: 164

    {  
       "IsEncrypted":"true",
       "EncryptionScheme" : "StorageEncryption", 
       "EncryptionVersion" : "1.0",       
       "EncryptionKeyId" : "nb:kid:UUID:32e6efaf-5fba-4538-b115-9d1cefe43510",
       "InitializationVector" : "397304628502661816</d:InitializationVector",
       "Options":0,
       "IsPrimary":"false",
       "MimeType":"video/mp4",
       "Name":"BigBuckBunny.mp4",
       "ParentAssetId":"nb:cid:UUID:9bc8ff20-24fb-4fdb-9d7c-b04c7ee573a1"
    }

<span data-ttu-id="38a30-205">**Odpowiedź HTTP**</span><span class="sxs-lookup"><span data-stu-id="38a30-205">**HTTP Response**</span></span>

    HTTP/1.1 201 Created
    Cache-Control: no-cache
    Content-Length: 535
    Content-Type: application/json;odata=minimalmetadata;streaming=true;charset=utf-8
    Location: https://wamsbayclus001rest-hs.cloudapp.net/api/Files('nb%3Acid%3AUUID%3Af13a0137-0a62-9d4c-b3b9-ca944b5142c5')
    Server: Microsoft-IIS/8.5
    request-id: 98a30e2d-f379-4495-988e-0b79edc9b80e
    x-ms-request-id: 98a30e2d-f379-4495-988e-0b79edc9b80e
    X-Content-Type-Options: nosniff
    DataServiceVersion: 3.0;
    X-Powered-By: ASP.NET
    Strict-Transport-Security: max-age=31536000; includeSubDomains
    Date: Mon, 19 Jan 2015 00:34:07 GMT

    {  
       "odata.metadata":"https://wamsbayclus001rest-hs.cloudapp.net/api/$metadata#Files/@Element",
       "Id":"nb:cid:UUID:f13a0137-0a62-9d4c-b3b9-ca944b5142c5",
       "Name":"BigBuckBunny.mp4",
       "ContentFileSize":"0",
       "ParentAssetId":"nb:cid:UUID:9bc8ff20-24fb-4fdb-9d7c-b04c7ee573a1",
       "EncryptionVersion": "1.0",
       "EncryptionScheme": "StorageEncryption",
       "IsEncrypted":true,
       "EncryptionKeyId":"nb:kid:UUID:32e6efaf-5fba-4538-b115-9d1cefe43510",
       "InitializationVector":"397304628502661816</d:InitializationVector",
       "IsPrimary":false,
       "LastModified":"2015-01-19T00:34:08.1934137Z",
       "Created":"2015-01-19T00:34:08.1934137Z",
       "MimeType":"video/mp4",
       "ContentChecksum":null
    }
