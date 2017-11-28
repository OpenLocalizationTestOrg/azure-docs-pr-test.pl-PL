---
title: "aaaEncrypting zawartości przy użyciu szyfrowania magazynu przy użyciu interfejsu API REST usług AMS"
description: "Dowiedz się, jak tooencrypt zawartości przy użyciu szyfrowania magazynu przy użyciu interfejsów API REST usługi AMS."
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
ms.openlocfilehash: d5f8cb8dd1dcded76c9fededccc772d8102ccbad
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="encrypting-your-content-with-storage-encryption"></a><span data-ttu-id="b43dd-103">Szyfrowanie zawartości przy użyciu szyfrowania magazynu</span><span class="sxs-lookup"><span data-stu-id="b43dd-103">Encrypting your content with storage encryption</span></span>

<span data-ttu-id="b43dd-104">Zdecydowanie zaleca się tooencrypt treści lokalnie przy użyciu standardu AES 256-bitowy szyfrowania, a następnie przekaż tooAzure magazynu, w którym będzie przechowywany szyfrowane, gdy.</span><span class="sxs-lookup"><span data-stu-id="b43dd-104">It is highly recommended tooencrypt your content locally using AES-256 bit encryption and then upload it tooAzure Storage where it will be stored encrypted at rest.</span></span>

<span data-ttu-id="b43dd-105">Ten artykuł zawiera omówienie usług AMS szyfrowanie magazynu i pokazuje, jak magazynu hello tooupload zaszyfrowana zawartość:</span><span class="sxs-lookup"><span data-stu-id="b43dd-105">This article gives an overview of AMS storage encryption and shows you how tooupload hello storage encrypted content:</span></span>

* <span data-ttu-id="b43dd-106">Utwórz klucz zawartości.</span><span class="sxs-lookup"><span data-stu-id="b43dd-106">Create a content key.</span></span>
* <span data-ttu-id="b43dd-107">Utwórz zasób.</span><span class="sxs-lookup"><span data-stu-id="b43dd-107">Create an Asset.</span></span> <span data-ttu-id="b43dd-108">Ustaw hello AssetCreationOption tooStorageEncryption podczas tworzenia hello zasobów.</span><span class="sxs-lookup"><span data-stu-id="b43dd-108">Set hello AssetCreationOption tooStorageEncryption when creating hello Asset.</span></span>
  
     <span data-ttu-id="b43dd-109">Zasoby zaszyfrowanych ma toobe związane z kluczy zawartości.</span><span class="sxs-lookup"><span data-stu-id="b43dd-109">Encrypted assets have toobe associated with content keys.</span></span>
* <span data-ttu-id="b43dd-110">Łącze hello toohello klucza zawartości zasobów.</span><span class="sxs-lookup"><span data-stu-id="b43dd-110">Link hello content key toohello asset.</span></span>  
* <span data-ttu-id="b43dd-111">Ustawianie parametrów na jednostkach AssetFile hello dotyczących hello szyfrowania.</span><span class="sxs-lookup"><span data-stu-id="b43dd-111">Set hello encryption related parameters on hello AssetFile entities.</span></span>

## <a name="considerations"></a><span data-ttu-id="b43dd-112">Zagadnienia do rozważenia</span><span class="sxs-lookup"><span data-stu-id="b43dd-112">Considerations</span></span> 

<span data-ttu-id="b43dd-113">Chcąc toodeliver zasób zaszyfrowanych magazynu, należy skonfigurować zasady dostarczania zasobów hello.</span><span class="sxs-lookup"><span data-stu-id="b43dd-113">If you want toodeliver a storage encrypted asset, you must configure hello asset’s delivery policy.</span></span> <span data-ttu-id="b43dd-114">Przed zawartości mogą być przesyłane strumieniowo, hello i przesyłania strumieniowego szyfrowania magazynu hello usuwa strumieni zawartości przy użyciu hello określone zasady dostarczania.</span><span class="sxs-lookup"><span data-stu-id="b43dd-114">Before your asset can be streamed, hello streaming server removes hello storage encryption and streams your content using hello specified delivery policy.</span></span> <span data-ttu-id="b43dd-115">Aby uzyskać więcej informacji, zobacz [Konfigurowanie zasad dostarczania zasobów](media-services-rest-configure-asset-delivery-policy.md).</span><span class="sxs-lookup"><span data-stu-id="b43dd-115">For more information, see [Configuring Asset Delivery Policies](media-services-rest-configure-asset-delivery-policy.md).</span></span>

<span data-ttu-id="b43dd-116">Podczas uzyskiwania dostępu do obiektów w usłudze Media Services, należy ustawić określonych pól nagłówka i wartości w Twoich żądań HTTP.</span><span class="sxs-lookup"><span data-stu-id="b43dd-116">When accessing entities in Media Services, you must set specific header fields and values in your HTTP requests.</span></span> <span data-ttu-id="b43dd-117">Aby uzyskać więcej informacji, zobacz [ustawień dla rozwoju interfejsu API REST usługi Media](media-services-rest-how-to-use.md).</span><span class="sxs-lookup"><span data-stu-id="b43dd-117">For more information, see [Setup for Media Services REST API Development](media-services-rest-how-to-use.md).</span></span> 

## <a name="connect-toomedia-services"></a><span data-ttu-id="b43dd-118">Połączenie usług tooMedia</span><span class="sxs-lookup"><span data-stu-id="b43dd-118">Connect tooMedia Services</span></span>

<span data-ttu-id="b43dd-119">Aby uzyskać informacje dotyczące tooconnect toohello AMS interfejsu API, zobacz temat [hello dostępu do interfejsu API usługi Azure Media Services przy użyciu uwierzytelniania usługi Azure AD](media-services-use-aad-auth-to-access-ams-api.md).</span><span class="sxs-lookup"><span data-stu-id="b43dd-119">For information on how tooconnect toohello AMS API, see [Access hello Azure Media Services API with Azure AD authentication](media-services-use-aad-auth-to-access-ams-api.md).</span></span> 

>[!NOTE]
><span data-ttu-id="b43dd-120">Po pomyślnym połączeniu toohttps://media.windows.net, otrzymasz 301 przekierowanie, określając inny identyfikator URI usługi multimediów.</span><span class="sxs-lookup"><span data-stu-id="b43dd-120">After successfully connecting toohttps://media.windows.net, you will receive a 301 redirect specifying another Media Services URI.</span></span> <span data-ttu-id="b43dd-121">Należy wykonać kolejne wywołania toohello nowy identyfikator URI.</span><span class="sxs-lookup"><span data-stu-id="b43dd-121">You must make subsequent calls toohello new URI.</span></span>

## <a name="storage-encryption-overview"></a><span data-ttu-id="b43dd-122">Omówienie szyfrowania magazynu</span><span class="sxs-lookup"><span data-stu-id="b43dd-122">Storage encryption overview</span></span>
<span data-ttu-id="b43dd-123">zastosowanie szyfrowania magazynu Hello AMS **Ewidencyjne AES** tryb szyfrowania toohello cały plik.</span><span class="sxs-lookup"><span data-stu-id="b43dd-123">hello AMS storage encryption applies **AES-CTR** mode encryption toohello entire file.</span></span>  <span data-ttu-id="b43dd-124">Tryb Ewidencyjne AES jest szyfry blokowe, który można zaszyfrować dane o dowolnej długości bez potrzeby dopełnienia.</span><span class="sxs-lookup"><span data-stu-id="b43dd-124">AES-CTR mode is a block cipher that can encrypt arbitrary length data without need for padding.</span></span> <span data-ttu-id="b43dd-125">Jego działa przez szyfrowanie bloku licznika z hello algorytmu AES, a następnie używać XOR hello dane wyjściowe AES z tooencrypt danych hello lub odszyfrować.</span><span class="sxs-lookup"><span data-stu-id="b43dd-125">It operates by encrypting a counter block with hello AES algorithm and then XOR-ing hello output of AES with hello data tooencrypt or decrypt.</span></span>  <span data-ttu-id="b43dd-126">Blok licznika Hello używany jest tworzony przez skopiowanie wartości hello hello InitializationVector toobytes 0 too7 wartości licznika hello i 8 bajtów too15 wartości licznika hello są ustawione toozero.</span><span class="sxs-lookup"><span data-stu-id="b43dd-126">hello counter block used is constructed by copying hello value of hello InitializationVector toobytes 0 too7 of hello counter value and bytes 8 too15 of hello counter value are set toozero.</span></span> <span data-ttu-id="b43dd-127">Witaj 16 bajtów licznika bloku, too15 8 bajtów (tj. hello najmniej znaczący w bajtach) są używane jak proste 64-bitowa liczba całkowita bez znaku jest zwiększany o jeden dla każdego kolejnych bloku danych przetwarzanych, który jest przechowywany w sieci kolejności bajtów.</span><span class="sxs-lookup"><span data-stu-id="b43dd-127">Of hello 16 byte counter block, bytes 8 too15 (i.e. hello least significant bytes) are used as a simple 64 bit unsigned integer that is incremented by one for each subsequent block of data processed and is kept in network byte order.</span></span> <span data-ttu-id="b43dd-128">Należy pamiętać, że jeśli ta liczba całkowita osiągnie wartość maksymalna hello (0xFFFFFFFFFFFFFFFF) o wartości on następnie resetuje hello bloku licznika toozero (8 bajtów too15) bez wpływu na inne hello 64-bitowy hello licznika (tj. 0 bajtów too7).</span><span class="sxs-lookup"><span data-stu-id="b43dd-128">Note that if this integer reaches hello maximum value (0xFFFFFFFFFFFFFFFF) then incrementing it resets hello block counter toozero (bytes 8 too15) without affecting hello other 64 bits of hello counter (i.e. bytes 0 too7).</span></span>   <span data-ttu-id="b43dd-129">W kolejności toomaintain hello zabezpieczeń hello Ewidencyjne AES tryb szyfrowania hello InitializationVector wartość dla podanego identyfikatora klucza do każdego klucz zawartości jest unikatowy dla każdego pliku i plików jest mniejsza niż wartość 2 ^ 64 bloki o długości.</span><span class="sxs-lookup"><span data-stu-id="b43dd-129">In order toomaintain hello security of hello AES-CTR mode encryption, hello InitializationVector value for a given Key Identifier for each content key shall be unique for each file and files shall be less than 2^64 blocks in length.</span></span>  <span data-ttu-id="b43dd-130">Jest to tooensure, że wartość licznika nigdy nie jest ponownie z danym kluczem.</span><span class="sxs-lookup"><span data-stu-id="b43dd-130">This is tooensure that a counter value is never reused with a given key.</span></span> <span data-ttu-id="b43dd-131">Aby uzyskać więcej informacji o trybie Ewidencyjne hello, zobacz [tej strony typu wiki](https://en.wikipedia.org/wiki/Block_cipher_mode_of_operation#CTR) (Artykuł typu wiki hello używa hello termin "Nonce" zamiast "InitializationVector").</span><span class="sxs-lookup"><span data-stu-id="b43dd-131">For more information about hello CTR mode, see [this wiki page](https://en.wikipedia.org/wiki/Block_cipher_mode_of_operation#CTR) (hello wiki article uses hello term "Nonce" instead of "InitializationVector").</span></span>

<span data-ttu-id="b43dd-132">Użyj **szyfrowanie magazynu** tooencrypt zawartości lokalnie przy użyciu standardu AES 256-bitowy szyfrowania, a następnie przekaż tooAzure magazynu, w którym są przechowywane szyfrowane, gdy.</span><span class="sxs-lookup"><span data-stu-id="b43dd-132">Use **Storage Encryption** tooencrypt your clear content locally using AES-256 bit encryption and then upload it tooAzure Storage where it is stored encrypted at rest.</span></span> <span data-ttu-id="b43dd-133">Elementy zawartości chronione przy użyciu szyfrowania magazynu są automatycznie bez szyfrowania i umieszczana w poprzednich tooencoding systemu szyfrowania plików i opcjonalnie ponownie szyfrowane przed toouploading zwrotnym w formie nowego elementu zawartości wyjściowej.</span><span class="sxs-lookup"><span data-stu-id="b43dd-133">Assets protected with storage encryption are automatically unencrypted and placed in an encrypted file system prior tooencoding, and optionally re-encrypted prior toouploading back as a new output asset.</span></span> <span data-ttu-id="b43dd-134">Witaj pierwotnym zastosowaniem szyfrowania magazynu jest toosecure Twojego wysokiej jakości multimedialnych plików wejściowych pomocą silnego szyfrowania rest na dysku.</span><span class="sxs-lookup"><span data-stu-id="b43dd-134">hello primary use case for storage encryption is when you want toosecure your high quality input media files with strong encryption at rest on disk.</span></span>

<span data-ttu-id="b43dd-135">W kolejności toodeliver zasób zaszyfrowanych magazynu należy skonfigurować zasady dostarczania zasobów hello będzie wówczas traktował Media Services sposób toodeliver zawartości.</span><span class="sxs-lookup"><span data-stu-id="b43dd-135">In order toodeliver a storage encrypted asset, you must configure hello asset’s delivery policy so Media Services knows how you want toodeliver your content.</span></span> <span data-ttu-id="b43dd-136">Aby mogła być przesłana strumieniowo zawartości, hello i przesyłania strumieniowego szyfrowania magazynu hello usuwa strumieni zawartości przy użyciu hello określone zasady dostarczania (na przykład AES, wspólnego szyfrowania lub bez szyfrowania).</span><span class="sxs-lookup"><span data-stu-id="b43dd-136">Before your asset can be streamed, hello streaming server removes hello storage encryption and streams your content using hello specified delivery policy (for example, AES, common encryption, or no encryption).</span></span>

## <a name="create-contentkeys-used-for-encryption"></a><span data-ttu-id="b43dd-137">Utwórz ContentKeys używany do szyfrowania</span><span class="sxs-lookup"><span data-stu-id="b43dd-137">Create ContentKeys used for encryption</span></span>
<span data-ttu-id="b43dd-138">Zasoby zaszyfrowanych ma toobe skojarzone z klucz szyfrowania magazynu.</span><span class="sxs-lookup"><span data-stu-id="b43dd-138">Encrypted assets have toobe associated with Storage Encryption key.</span></span> <span data-ttu-id="b43dd-139">Należy utworzyć hello zawartości toobe klucza szyfrowania przed utworzeniem hello plików zasobów.</span><span class="sxs-lookup"><span data-stu-id="b43dd-139">You must create hello content key toobe used for encryption before creating hello asset files.</span></span> <span data-ttu-id="b43dd-140">W tej sekcji opisano sposób toocreate klucz zawartości.</span><span class="sxs-lookup"><span data-stu-id="b43dd-140">This section describes how toocreate a content key.</span></span>

<span data-ttu-id="b43dd-141">Witaj poniżej przedstawiono ogólne kroki podczas generowania zawartości kluczy, które skojarzysz z zasobów, które mają toobe szyfrowane.</span><span class="sxs-lookup"><span data-stu-id="b43dd-141">hello following are general steps for generating content keys that you will associate with assets that you want toobe encrypted.</span></span> 

1. <span data-ttu-id="b43dd-142">Do szyfrowania magazynu losowego generowania klucza AES 32 bajtów.</span><span class="sxs-lookup"><span data-stu-id="b43dd-142">For storage encryption, randomly generate a 32-byte AES key.</span></span> 
   
    <span data-ttu-id="b43dd-143">Są to hello klucz zawartości dla zawartości, co oznacza wszystkie pliki skojarzone z tym zawartości będzie konieczne toouse hello tego samego klucza zawartości podczas odszyfrowywania.</span><span class="sxs-lookup"><span data-stu-id="b43dd-143">This will be hello content key for your asset, which means all files associated with that asset will need toouse hello same content key during decryption.</span></span> 
2. <span data-ttu-id="b43dd-144">Wywołaj hello [GetProtectionKeyId](https://docs.microsoft.com/rest/api/media/operations/rest-api-functions#getprotectionkeyid) i [GetProtectionKey](https://msdn.microsoft.com/library/azure/jj683097.aspx#getprotectionkey) tooget metody hello poprawne certyfikatu X.509, który musi być używane tooencrypt klucz zawartości.</span><span class="sxs-lookup"><span data-stu-id="b43dd-144">Call hello [GetProtectionKeyId](https://docs.microsoft.com/rest/api/media/operations/rest-api-functions#getprotectionkeyid) and [GetProtectionKey](https://msdn.microsoft.com/library/azure/jj683097.aspx#getprotectionkey) methods tooget hello correct X.509 Certificate that must be used tooencrypt your content key.</span></span>
3. <span data-ttu-id="b43dd-145">Zaszyfrowanie klucza zawartości z klucza publicznego hello hello certyfikatu X.509.</span><span class="sxs-lookup"><span data-stu-id="b43dd-145">Encrypt your content key with hello public key of hello X.509 Certificate.</span></span> 
   
   <span data-ttu-id="b43dd-146">.NET SDK usługi Media Services używa algorytmu RSA z OAEP podczas szyfrowania hello.</span><span class="sxs-lookup"><span data-stu-id="b43dd-146">Media Services .NET SDK uses RSA with OAEP when doing hello encryption.</span></span>  <span data-ttu-id="b43dd-147">Widoczny jest przykład .NET w hello [funkcja EncryptSymmetricKeyData](https://github.com/Azure/azure-sdk-for-media-services/blob/dev/src/net/Client/Common/Common.FileEncryption/EncryptionUtils.cs).</span><span class="sxs-lookup"><span data-stu-id="b43dd-147">You can see a .NET example in hello [EncryptSymmetricKeyData function](https://github.com/Azure/azure-sdk-for-media-services/blob/dev/src/net/Client/Common/Common.FileEncryption/EncryptionUtils.cs).</span></span>
4. <span data-ttu-id="b43dd-148">Utwórz wartość sumy kontrolnej obliczane przy użyciu identyfikatora klucza hello i klucz zawartości.</span><span class="sxs-lookup"><span data-stu-id="b43dd-148">Create a checksum value calculated using hello key identifier and content key.</span></span> <span data-ttu-id="b43dd-149">Poniższy przykład .NET Hello oblicza sumę kontrolną hello przy użyciu identyfikatora GUID hello część identyfikatora klucza hello i hello wyczyść klucz zawartości.</span><span class="sxs-lookup"><span data-stu-id="b43dd-149">hello following .NET example calculates hello checksum using hello GUID part of hello key identifier and hello clear content key.</span></span>

        public static string CalculateChecksum(byte[] contentKey, Guid keyId)
        {
            const int ChecksumLength = 8;
            const int KeyIdLength = 16;

            byte[] encryptedKeyId = null;

            // Checksum is computed by AES-ECB encrypting hello KID
            // with hello content key.
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

1. <span data-ttu-id="b43dd-150">Utwórz klucz zawartości hello z hello **EncryptedContentKey** (przekonwertować ciąg kodowany w formacie toobase64), **ProtectionKeyId**, **ProtectionKeyType**,  **ContentKeyType**, i **sumy kontrolnej** wartości otrzymany w poprzednich krokach.</span><span class="sxs-lookup"><span data-stu-id="b43dd-150">Create hello Content key with hello **EncryptedContentKey** (converted toobase64-encoded string), **ProtectionKeyId**, **ProtectionKeyType**, **ContentKeyType**, and **Checksum** values you have received in previous steps.</span></span>

    <span data-ttu-id="b43dd-151">Do szyfrowania magazynu hello powinny znajdować się następujące właściwości w treści żądania hello.</span><span class="sxs-lookup"><span data-stu-id="b43dd-151">For storage encryption, hello following properties should be included in hello request body.</span></span>

    <span data-ttu-id="b43dd-152">Właściwość treść żądania</span><span class="sxs-lookup"><span data-stu-id="b43dd-152">Request body property</span></span>    | <span data-ttu-id="b43dd-153">Opis</span><span class="sxs-lookup"><span data-stu-id="b43dd-153">Description</span></span>
    ---|---
    <span data-ttu-id="b43dd-154">Identyfikator</span><span class="sxs-lookup"><span data-stu-id="b43dd-154">Id</span></span> | <span data-ttu-id="b43dd-155">Hello ContentKey identyfikator, który mamy Generowanie nad powitania po użyciu formatu, "nb:kid:UUID:<NEW GUID>".</span><span class="sxs-lookup"><span data-stu-id="b43dd-155">hello ContentKey Id which we generate ourselves using hello following format, “nb:kid:UUID:<NEW GUID>”.</span></span>
    <span data-ttu-id="b43dd-156">ContentKeyType</span><span class="sxs-lookup"><span data-stu-id="b43dd-156">ContentKeyType</span></span> | <span data-ttu-id="b43dd-157">Typ klucza zawartości hello jest jako liczba całkowita dla tego klucza zawartości.</span><span class="sxs-lookup"><span data-stu-id="b43dd-157">This is hello content key type as an integer for this content key.</span></span> <span data-ttu-id="b43dd-158">Wartość hello 1 szyfrowania magazynu jest przekazywana.</span><span class="sxs-lookup"><span data-stu-id="b43dd-158">We pass hello value 1 for storage encryption.</span></span>
    <span data-ttu-id="b43dd-159">EncryptedContentKey</span><span class="sxs-lookup"><span data-stu-id="b43dd-159">EncryptedContentKey</span></span> | <span data-ttu-id="b43dd-160">Utworzymy nową wartość klucza zawartości, która jest wartością 256-bitowego (32 bajtów).</span><span class="sxs-lookup"><span data-stu-id="b43dd-160">We create a new content key value which is a 256-bit (32 byte) value.</span></span> <span data-ttu-id="b43dd-161">klucz Hello jest szyfrowana przy użyciu certyfikatu X.509 szyfrowania magazynu hello, którego możemy pobrać Microsoft Azure Media Services, wykonując żądanie HTTP GET dla hello GetProtectionKeyId i metod GetProtectionKey.</span><span class="sxs-lookup"><span data-stu-id="b43dd-161">hello key is encrypted using hello storage encryption X.509 certificate which we retrieve from Microsoft Azure Media Services by executing a HTTP GET request for hello GetProtectionKeyId and GetProtectionKey Methods.</span></span> <span data-ttu-id="b43dd-162">Na przykład zobacz hello następującego kodu platformy .NET: hello **EncryptSymmetricKeyData** metody zdefiniowanej [tutaj](https://github.com/Azure/azure-sdk-for-media-services/blob/dev/src/net/Client/Common/Common.FileEncryption/EncryptionUtils.cs).</span><span class="sxs-lookup"><span data-stu-id="b43dd-162">As an example, see hello following .NET code: hello  **EncryptSymmetricKeyData** method defined [here](https://github.com/Azure/azure-sdk-for-media-services/blob/dev/src/net/Client/Common/Common.FileEncryption/EncryptionUtils.cs).</span></span>
    <span data-ttu-id="b43dd-163">ProtectionKeyId</span><span class="sxs-lookup"><span data-stu-id="b43dd-163">ProtectionKeyId</span></span> | <span data-ttu-id="b43dd-164">To jest hello ochrony identyfikator klucza certyfikatu X.509 szyfrowania magazynu hello, który był używany tooencrypt naszych klucz zawartości.</span><span class="sxs-lookup"><span data-stu-id="b43dd-164">This is hello protection key id for hello storage encryption X.509 certificate that was used tooencrypt our content key.</span></span>
    <span data-ttu-id="b43dd-165">ProtectionKeyType</span><span class="sxs-lookup"><span data-stu-id="b43dd-165">ProtectionKeyType</span></span> | <span data-ttu-id="b43dd-166">Jest to typ szyfrowania hello hello ochrony klucza, który był używany tooencrypt hello zawartości klucz.</span><span class="sxs-lookup"><span data-stu-id="b43dd-166">This is hello encryption type for hello protection key that was used tooencrypt hello content key.</span></span> <span data-ttu-id="b43dd-167">Ta wartość jest StorageEncryption(1) w naszym przykładzie.</span><span class="sxs-lookup"><span data-stu-id="b43dd-167">This value is StorageEncryption(1) for our example.</span></span>
    <span data-ttu-id="b43dd-168">Sumy kontrolnej</span><span class="sxs-lookup"><span data-stu-id="b43dd-168">Checksum</span></span> |<span data-ttu-id="b43dd-169">Witaj MD5 obliczeniowej sumy kontrolnej dla hello klucz zawartości.</span><span class="sxs-lookup"><span data-stu-id="b43dd-169">hello MD5 calculated checksum for hello content key.</span></span> <span data-ttu-id="b43dd-170">Jest ona obliczana przez szyfrowanie hello identyfikatora zawartości z hello klucz zawartości.</span><span class="sxs-lookup"><span data-stu-id="b43dd-170">It is computed by encrypting hello content Id with hello content key.</span></span> <span data-ttu-id="b43dd-171">Witaj przykładowy kod pokazuje, jak toocalculate hello sumy kontrolnej.</span><span class="sxs-lookup"><span data-stu-id="b43dd-171">hello example code demonstrates how toocalculate hello checksum.</span></span>


### <a name="retrieve-hello-protectionkeyid"></a><span data-ttu-id="b43dd-172">Pobrać hello ProtectionKeyId</span><span class="sxs-lookup"><span data-stu-id="b43dd-172">Retrieve hello ProtectionKeyId</span></span>
<span data-ttu-id="b43dd-173">Witaj poniższy przykład pokazuje, jak tooretrieve hello ProtectionKeyId, odcisk palca certyfikatu, hello certyfikatu, który należy użyć w przypadku szyfrowania kluczem zawartości.</span><span class="sxs-lookup"><span data-stu-id="b43dd-173">hello following example shows how tooretrieve hello ProtectionKeyId, a certificate thumbprint, for hello certificate you must use when encrypting your content key.</span></span> <span data-ttu-id="b43dd-174">Wykonaj ten krok toomake upewnić się, że już hello odpowiedniego certyfikatu na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="b43dd-174">Do this step toomake sure that you already have hello appropriate certificate on your machine.</span></span>

<span data-ttu-id="b43dd-175">Żądanie:</span><span class="sxs-lookup"><span data-stu-id="b43dd-175">Request:</span></span>

    GET https://media.windows.net/api/GetProtectionKeyId?contentKeyType=0 HTTP/1.1
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    User-Agent: Microsoft ADO.NET Data Services
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=juliakoams1&urn%3aSubscriptionId=zbbef702-2233-477b-9f16-bc4d3aa97387&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1423034908&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=7eSLe1GHnxgilr3F2FPCGxdL2%2bwy%2f39XhMPGY9IizfU%3d
    x-ms-version: 2.11
    Host: media.windows.net

<span data-ttu-id="b43dd-176">Odpowiedź:</span><span class="sxs-lookup"><span data-stu-id="b43dd-176">Response:</span></span>

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

### <a name="retrieve-hello-protectionkey-for-hello-protectionkeyid"></a><span data-ttu-id="b43dd-177">Pobrać hello ProtectionKey dla hello ProtectionKeyId</span><span class="sxs-lookup"><span data-stu-id="b43dd-177">Retrieve hello ProtectionKey for hello ProtectionKeyId</span></span>
<span data-ttu-id="b43dd-178">Witaj poniższy przykład przedstawia sposób certyfikatu X.509 hello tooretrieve przy użyciu hello ProtectionKeyId otrzymany hello poprzedniego kroku.</span><span class="sxs-lookup"><span data-stu-id="b43dd-178">hello following example shows how tooretrieve hello X.509 certificate using hello ProtectionKeyId you received in hello previous step.</span></span>

<span data-ttu-id="b43dd-179">Żądanie:</span><span class="sxs-lookup"><span data-stu-id="b43dd-179">Request:</span></span>

    GET https://media.windows.net/api/GetProtectionKey?ProtectionKeyId='7D9BB04D9D0A4A24800CADBFEF232689E048F69C' HTTP/1.1
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    User-Agent: Microsoft ADO.NET Data Services
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=juliakoams1&urn%3aSubscriptionId=zbbef702-e769-2233-9f16-bc4d3aa97387&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1423141026&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=lDBz5YXKiWe5L7eXOHsLHc9kKEUcUiFJvrNFFSksgkM%3d
    x-ms-version: 2.11
    x-ms-client-request-id: 78d1247a-58d7-40e5-96cc-70ff0dfa7382
    Host: media.windows.net

<span data-ttu-id="b43dd-180">Odpowiedź:</span><span class="sxs-lookup"><span data-stu-id="b43dd-180">Response:</span></span>

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

### <a name="create-hello-content-key"></a><span data-ttu-id="b43dd-181">Utwórz klucz zawartości hello</span><span class="sxs-lookup"><span data-stu-id="b43dd-181">Create hello content key</span></span>
<span data-ttu-id="b43dd-182">Po pobrać certyfikat X.509 hello i używać jej tooencrypt klucza publicznego klucza zawartości należy utworzyć **ContentKey** jednostki i ustaw jej właściwość odpowiednio wartości.</span><span class="sxs-lookup"><span data-stu-id="b43dd-182">After you have retrieved hello X.509 certificate and used its public key tooencrypt your content key, create a **ContentKey** entity and set its property values accordingly.</span></span>

<span data-ttu-id="b43dd-183">Jedna z wartości hello, że należy ustawić podczas tworzenia zawartości, że klucz jest typu hello hello.</span><span class="sxs-lookup"><span data-stu-id="b43dd-183">One of hello values that you must set when create hello content key is hello type.</span></span> <span data-ttu-id="b43dd-184">W przypadku szyfrowania magazynu hello wartość hello jest '1'.</span><span class="sxs-lookup"><span data-stu-id="b43dd-184">In case of hello storage encryption, hello value is '1'.</span></span> 

<span data-ttu-id="b43dd-185">powitania po przykładzie pokazano, jak toocreate **ContentKey** z **ContentKeyType** Konfiguracja do szyfrowania magazynu ("1") i hello **ProtectionKeyType** ustawiona zbyt "0" tooindicate, który hello ochrony klucza identyfikator jest odcisk palca certyfikatu X.509 hello.</span><span class="sxs-lookup"><span data-stu-id="b43dd-185">hello following example shows how toocreate a **ContentKey** with a **ContentKeyType** set for storage encryption ("1") and hello **ProtectionKeyType** set too"0" tooindicate that hello protection key Id is hello X.509 certificate thumbprint.</span></span>  

<span data-ttu-id="b43dd-186">Żądanie</span><span class="sxs-lookup"><span data-stu-id="b43dd-186">Request</span></span>

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

<span data-ttu-id="b43dd-187">Odpowiedź:</span><span class="sxs-lookup"><span data-stu-id="b43dd-187">Response:</span></span>

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

## <a name="create-an-asset"></a><span data-ttu-id="b43dd-188">Utwórz zasób</span><span class="sxs-lookup"><span data-stu-id="b43dd-188">Create an asset</span></span>
<span data-ttu-id="b43dd-189">powitania po przykładzie pokazano, jak toocreate zasób.</span><span class="sxs-lookup"><span data-stu-id="b43dd-189">hello following example shows how toocreate an asset.</span></span>

<span data-ttu-id="b43dd-190">**Żądania HTTP**</span><span class="sxs-lookup"><span data-stu-id="b43dd-190">**HTTP Request**</span></span>

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

<span data-ttu-id="b43dd-191">**Odpowiedź HTTP**</span><span class="sxs-lookup"><span data-stu-id="b43dd-191">**HTTP Response**</span></span>

<span data-ttu-id="b43dd-192">W przypadku powodzenia zwrócono hello następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="b43dd-192">If successful, hello following is returned:</span></span>

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

## <a name="associate-hello-contentkey-with-an-asset"></a><span data-ttu-id="b43dd-193">Skojarz hello ContentKey z zasobów</span><span class="sxs-lookup"><span data-stu-id="b43dd-193">Associate hello ContentKey with an Asset</span></span>
<span data-ttu-id="b43dd-194">Po utworzeniu hello ContentKey, skojarzyć ją z zawartości przy użyciu operacji hello $links, jak pokazano w hello poniższy przykład:</span><span class="sxs-lookup"><span data-stu-id="b43dd-194">After creating hello ContentKey, associate it with your Asset using hello $links operation, as shown in hello following example:</span></span>

<span data-ttu-id="b43dd-195">Żądanie:</span><span class="sxs-lookup"><span data-stu-id="b43dd-195">Request:</span></span>

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

<span data-ttu-id="b43dd-196">Odpowiedź:</span><span class="sxs-lookup"><span data-stu-id="b43dd-196">Response:</span></span>

    HTTP/1.1 204 No Content 

## <a name="create-an-assetfile"></a><span data-ttu-id="b43dd-197">Utwórz AssetFile</span><span class="sxs-lookup"><span data-stu-id="b43dd-197">Create an AssetFile</span></span>
<span data-ttu-id="b43dd-198">Witaj [AssetFile](https://docs.microsoft.com/rest/api/media/operations/assetfile) jednostki reprezentuje plik wideo lub audio, który jest przechowywany w kontenerze obiektów blob.</span><span class="sxs-lookup"><span data-stu-id="b43dd-198">hello [AssetFile](https://docs.microsoft.com/rest/api/media/operations/assetfile) entity represents a video or audio file that is stored in a blob container.</span></span> <span data-ttu-id="b43dd-199">Plik zasobów zawsze jest skojarzony z zasobem i zasobów może zawierać jeden lub wiele plików zasobów.</span><span class="sxs-lookup"><span data-stu-id="b43dd-199">An asset file is always associated with an asset, and an asset may contain one or many asset files.</span></span> <span data-ttu-id="b43dd-200">Witaj Media Encoder usług zadanie nie powiedzie się, jeśli obiekt pliku zasobu nie jest skojarzony z pliku cyfrowego w kontenerze obiektów blob.</span><span class="sxs-lookup"><span data-stu-id="b43dd-200">hello Media Services Encoder task fails if an asset file object is not associated with a digital file in a blob container.</span></span>

<span data-ttu-id="b43dd-201">Należy pamiętać, że hello **AssetFile** wystąpienia oraz plik multimedialna hello są dwa różne obiekty.</span><span class="sxs-lookup"><span data-stu-id="b43dd-201">Note that hello **AssetFile** instance and hello actual media file are two distinct objects.</span></span> <span data-ttu-id="b43dd-202">wystąpienia AssetFile Hello zawiera metadane dotyczące plików multimedialnych hello, a plik multimedialny hello zawiera zawartość multimedialna hello.</span><span class="sxs-lookup"><span data-stu-id="b43dd-202">hello AssetFile instance contains metadata about hello media file, while hello media file contains hello actual media content.</span></span>

<span data-ttu-id="b43dd-203">Po przekazaniu pliku nośnika cyfrowego do kontenera obiektów blob, użyje hello **scalania** żądania HTTP tooupdate hello AssetFile informacje o pliku nośnika (niewidoczny w tym temacie).</span><span class="sxs-lookup"><span data-stu-id="b43dd-203">After you upload your digital media file into a blob container, you will use hello **MERGE** HTTP request tooupdate hello AssetFile with information about your media file (not shown in this topic).</span></span> 

<span data-ttu-id="b43dd-204">**Żądania HTTP**</span><span class="sxs-lookup"><span data-stu-id="b43dd-204">**HTTP Request**</span></span>

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

<span data-ttu-id="b43dd-205">**Odpowiedź HTTP**</span><span class="sxs-lookup"><span data-stu-id="b43dd-205">**HTTP Response**</span></span>

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
