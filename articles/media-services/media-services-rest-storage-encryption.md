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
# <a name="encrypting-your-content-with-storage-encryption"></a>Szyfrowanie zawartości przy użyciu szyfrowania magazynu

Zdecydowanie zaleca się tooencrypt treści lokalnie przy użyciu standardu AES 256-bitowy szyfrowania, a następnie przekaż tooAzure magazynu, w którym będzie przechowywany szyfrowane, gdy.

Ten artykuł zawiera omówienie usług AMS szyfrowanie magazynu i pokazuje, jak magazynu hello tooupload zaszyfrowana zawartość:

* Utwórz klucz zawartości.
* Utwórz zasób. Ustaw hello AssetCreationOption tooStorageEncryption podczas tworzenia hello zasobów.
  
     Zasoby zaszyfrowanych ma toobe związane z kluczy zawartości.
* Łącze hello toohello klucza zawartości zasobów.  
* Ustawianie parametrów na jednostkach AssetFile hello dotyczących hello szyfrowania.

## <a name="considerations"></a>Zagadnienia do rozważenia 

Chcąc toodeliver zasób zaszyfrowanych magazynu, należy skonfigurować zasady dostarczania zasobów hello. Przed zawartości mogą być przesyłane strumieniowo, hello i przesyłania strumieniowego szyfrowania magazynu hello usuwa strumieni zawartości przy użyciu hello określone zasady dostarczania. Aby uzyskać więcej informacji, zobacz [Konfigurowanie zasad dostarczania zasobów](media-services-rest-configure-asset-delivery-policy.md).

Podczas uzyskiwania dostępu do obiektów w usłudze Media Services, należy ustawić określonych pól nagłówka i wartości w Twoich żądań HTTP. Aby uzyskać więcej informacji, zobacz [ustawień dla rozwoju interfejsu API REST usługi Media](media-services-rest-how-to-use.md). 

## <a name="connect-toomedia-services"></a>Połączenie usług tooMedia

Aby uzyskać informacje dotyczące tooconnect toohello AMS interfejsu API, zobacz temat [hello dostępu do interfejsu API usługi Azure Media Services przy użyciu uwierzytelniania usługi Azure AD](media-services-use-aad-auth-to-access-ams-api.md). 

>[!NOTE]
>Po pomyślnym połączeniu toohttps://media.windows.net, otrzymasz 301 przekierowanie, określając inny identyfikator URI usługi multimediów. Należy wykonać kolejne wywołania toohello nowy identyfikator URI.

## <a name="storage-encryption-overview"></a>Omówienie szyfrowania magazynu
zastosowanie szyfrowania magazynu Hello AMS **Ewidencyjne AES** tryb szyfrowania toohello cały plik.  Tryb Ewidencyjne AES jest szyfry blokowe, który można zaszyfrować dane o dowolnej długości bez potrzeby dopełnienia. Jego działa przez szyfrowanie bloku licznika z hello algorytmu AES, a następnie używać XOR hello dane wyjściowe AES z tooencrypt danych hello lub odszyfrować.  Blok licznika Hello używany jest tworzony przez skopiowanie wartości hello hello InitializationVector toobytes 0 too7 wartości licznika hello i 8 bajtów too15 wartości licznika hello są ustawione toozero. Witaj 16 bajtów licznika bloku, too15 8 bajtów (tj. hello najmniej znaczący w bajtach) są używane jak proste 64-bitowa liczba całkowita bez znaku jest zwiększany o jeden dla każdego kolejnych bloku danych przetwarzanych, który jest przechowywany w sieci kolejności bajtów. Należy pamiętać, że jeśli ta liczba całkowita osiągnie wartość maksymalna hello (0xFFFFFFFFFFFFFFFF) o wartości on następnie resetuje hello bloku licznika toozero (8 bajtów too15) bez wpływu na inne hello 64-bitowy hello licznika (tj. 0 bajtów too7).   W kolejności toomaintain hello zabezpieczeń hello Ewidencyjne AES tryb szyfrowania hello InitializationVector wartość dla podanego identyfikatora klucza do każdego klucz zawartości jest unikatowy dla każdego pliku i plików jest mniejsza niż wartość 2 ^ 64 bloki o długości.  Jest to tooensure, że wartość licznika nigdy nie jest ponownie z danym kluczem. Aby uzyskać więcej informacji o trybie Ewidencyjne hello, zobacz [tej strony typu wiki](https://en.wikipedia.org/wiki/Block_cipher_mode_of_operation#CTR) (Artykuł typu wiki hello używa hello termin "Nonce" zamiast "InitializationVector").

Użyj **szyfrowanie magazynu** tooencrypt zawartości lokalnie przy użyciu standardu AES 256-bitowy szyfrowania, a następnie przekaż tooAzure magazynu, w którym są przechowywane szyfrowane, gdy. Elementy zawartości chronione przy użyciu szyfrowania magazynu są automatycznie bez szyfrowania i umieszczana w poprzednich tooencoding systemu szyfrowania plików i opcjonalnie ponownie szyfrowane przed toouploading zwrotnym w formie nowego elementu zawartości wyjściowej. Witaj pierwotnym zastosowaniem szyfrowania magazynu jest toosecure Twojego wysokiej jakości multimedialnych plików wejściowych pomocą silnego szyfrowania rest na dysku.

W kolejności toodeliver zasób zaszyfrowanych magazynu należy skonfigurować zasady dostarczania zasobów hello będzie wówczas traktował Media Services sposób toodeliver zawartości. Aby mogła być przesłana strumieniowo zawartości, hello i przesyłania strumieniowego szyfrowania magazynu hello usuwa strumieni zawartości przy użyciu hello określone zasady dostarczania (na przykład AES, wspólnego szyfrowania lub bez szyfrowania).

## <a name="create-contentkeys-used-for-encryption"></a>Utwórz ContentKeys używany do szyfrowania
Zasoby zaszyfrowanych ma toobe skojarzone z klucz szyfrowania magazynu. Należy utworzyć hello zawartości toobe klucza szyfrowania przed utworzeniem hello plików zasobów. W tej sekcji opisano sposób toocreate klucz zawartości.

Witaj poniżej przedstawiono ogólne kroki podczas generowania zawartości kluczy, które skojarzysz z zasobów, które mają toobe szyfrowane. 

1. Do szyfrowania magazynu losowego generowania klucza AES 32 bajtów. 
   
    Są to hello klucz zawartości dla zawartości, co oznacza wszystkie pliki skojarzone z tym zawartości będzie konieczne toouse hello tego samego klucza zawartości podczas odszyfrowywania. 
2. Wywołaj hello [GetProtectionKeyId](https://docs.microsoft.com/rest/api/media/operations/rest-api-functions#getprotectionkeyid) i [GetProtectionKey](https://msdn.microsoft.com/library/azure/jj683097.aspx#getprotectionkey) tooget metody hello poprawne certyfikatu X.509, który musi być używane tooencrypt klucz zawartości.
3. Zaszyfrowanie klucza zawartości z klucza publicznego hello hello certyfikatu X.509. 
   
   .NET SDK usługi Media Services używa algorytmu RSA z OAEP podczas szyfrowania hello.  Widoczny jest przykład .NET w hello [funkcja EncryptSymmetricKeyData](https://github.com/Azure/azure-sdk-for-media-services/blob/dev/src/net/Client/Common/Common.FileEncryption/EncryptionUtils.cs).
4. Utwórz wartość sumy kontrolnej obliczane przy użyciu identyfikatora klucza hello i klucz zawartości. Poniższy przykład .NET Hello oblicza sumę kontrolną hello przy użyciu identyfikatora GUID hello część identyfikatora klucza hello i hello wyczyść klucz zawartości.

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

1. Utwórz klucz zawartości hello z hello **EncryptedContentKey** (przekonwertować ciąg kodowany w formacie toobase64), **ProtectionKeyId**, **ProtectionKeyType**,  **ContentKeyType**, i **sumy kontrolnej** wartości otrzymany w poprzednich krokach.

    Do szyfrowania magazynu hello powinny znajdować się następujące właściwości w treści żądania hello.

    Właściwość treść żądania    | Opis
    ---|---
    Identyfikator | Hello ContentKey identyfikator, który mamy Generowanie nad powitania po użyciu formatu, "nb:kid:UUID:<NEW GUID>".
    ContentKeyType | Typ klucza zawartości hello jest jako liczba całkowita dla tego klucza zawartości. Wartość hello 1 szyfrowania magazynu jest przekazywana.
    EncryptedContentKey | Utworzymy nową wartość klucza zawartości, która jest wartością 256-bitowego (32 bajtów). klucz Hello jest szyfrowana przy użyciu certyfikatu X.509 szyfrowania magazynu hello, którego możemy pobrać Microsoft Azure Media Services, wykonując żądanie HTTP GET dla hello GetProtectionKeyId i metod GetProtectionKey. Na przykład zobacz hello następującego kodu platformy .NET: hello **EncryptSymmetricKeyData** metody zdefiniowanej [tutaj](https://github.com/Azure/azure-sdk-for-media-services/blob/dev/src/net/Client/Common/Common.FileEncryption/EncryptionUtils.cs).
    ProtectionKeyId | To jest hello ochrony identyfikator klucza certyfikatu X.509 szyfrowania magazynu hello, który był używany tooencrypt naszych klucz zawartości.
    ProtectionKeyType | Jest to typ szyfrowania hello hello ochrony klucza, który był używany tooencrypt hello zawartości klucz. Ta wartość jest StorageEncryption(1) w naszym przykładzie.
    Sumy kontrolnej |Witaj MD5 obliczeniowej sumy kontrolnej dla hello klucz zawartości. Jest ona obliczana przez szyfrowanie hello identyfikatora zawartości z hello klucz zawartości. Witaj przykładowy kod pokazuje, jak toocalculate hello sumy kontrolnej.


### <a name="retrieve-hello-protectionkeyid"></a>Pobrać hello ProtectionKeyId
Witaj poniższy przykład pokazuje, jak tooretrieve hello ProtectionKeyId, odcisk palca certyfikatu, hello certyfikatu, który należy użyć w przypadku szyfrowania kluczem zawartości. Wykonaj ten krok toomake upewnić się, że już hello odpowiedniego certyfikatu na tym komputerze.

Żądanie:

    GET https://media.windows.net/api/GetProtectionKeyId?contentKeyType=0 HTTP/1.1
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    User-Agent: Microsoft ADO.NET Data Services
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=juliakoams1&urn%3aSubscriptionId=zbbef702-2233-477b-9f16-bc4d3aa97387&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1423034908&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=7eSLe1GHnxgilr3F2FPCGxdL2%2bwy%2f39XhMPGY9IizfU%3d
    x-ms-version: 2.11
    Host: media.windows.net

Odpowiedź:

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

### <a name="retrieve-hello-protectionkey-for-hello-protectionkeyid"></a>Pobrać hello ProtectionKey dla hello ProtectionKeyId
Witaj poniższy przykład przedstawia sposób certyfikatu X.509 hello tooretrieve przy użyciu hello ProtectionKeyId otrzymany hello poprzedniego kroku.

Żądanie:

    GET https://media.windows.net/api/GetProtectionKey?ProtectionKeyId='7D9BB04D9D0A4A24800CADBFEF232689E048F69C' HTTP/1.1
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    User-Agent: Microsoft ADO.NET Data Services
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=juliakoams1&urn%3aSubscriptionId=zbbef702-e769-2233-9f16-bc4d3aa97387&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1423141026&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=lDBz5YXKiWe5L7eXOHsLHc9kKEUcUiFJvrNFFSksgkM%3d
    x-ms-version: 2.11
    x-ms-client-request-id: 78d1247a-58d7-40e5-96cc-70ff0dfa7382
    Host: media.windows.net

Odpowiedź:

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

### <a name="create-hello-content-key"></a>Utwórz klucz zawartości hello
Po pobrać certyfikat X.509 hello i używać jej tooencrypt klucza publicznego klucza zawartości należy utworzyć **ContentKey** jednostki i ustaw jej właściwość odpowiednio wartości.

Jedna z wartości hello, że należy ustawić podczas tworzenia zawartości, że klucz jest typu hello hello. W przypadku szyfrowania magazynu hello wartość hello jest '1'. 

powitania po przykładzie pokazano, jak toocreate **ContentKey** z **ContentKeyType** Konfiguracja do szyfrowania magazynu ("1") i hello **ProtectionKeyType** ustawiona zbyt "0" tooindicate, który hello ochrony klucza identyfikator jest odcisk palca certyfikatu X.509 hello.  

Żądanie

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

Odpowiedź:

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

## <a name="create-an-asset"></a>Utwórz zasób
powitania po przykładzie pokazano, jak toocreate zasób.

**Żądania HTTP**

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

**Odpowiedź HTTP**

W przypadku powodzenia zwrócono hello następujące czynności:

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

## <a name="associate-hello-contentkey-with-an-asset"></a>Skojarz hello ContentKey z zasobów
Po utworzeniu hello ContentKey, skojarzyć ją z zawartości przy użyciu operacji hello $links, jak pokazano w hello poniższy przykład:

Żądanie:

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

Odpowiedź:

    HTTP/1.1 204 No Content 

## <a name="create-an-assetfile"></a>Utwórz AssetFile
Witaj [AssetFile](https://docs.microsoft.com/rest/api/media/operations/assetfile) jednostki reprezentuje plik wideo lub audio, który jest przechowywany w kontenerze obiektów blob. Plik zasobów zawsze jest skojarzony z zasobem i zasobów może zawierać jeden lub wiele plików zasobów. Witaj Media Encoder usług zadanie nie powiedzie się, jeśli obiekt pliku zasobu nie jest skojarzony z pliku cyfrowego w kontenerze obiektów blob.

Należy pamiętać, że hello **AssetFile** wystąpienia oraz plik multimedialna hello są dwa różne obiekty. wystąpienia AssetFile Hello zawiera metadane dotyczące plików multimedialnych hello, a plik multimedialny hello zawiera zawartość multimedialna hello.

Po przekazaniu pliku nośnika cyfrowego do kontenera obiektów blob, użyje hello **scalania** żądania HTTP tooupdate hello AssetFile informacje o pliku nośnika (niewidoczny w tym temacie). 

**Żądania HTTP**

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

**Odpowiedź HTTP**

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
