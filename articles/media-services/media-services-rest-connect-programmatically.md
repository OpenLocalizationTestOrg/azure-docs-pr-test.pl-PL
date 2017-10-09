---
title: "tooMedia aaaConnecting konto usługi za pomocą interfejsu API REST | Dokumentacja firmy Microsoft"
description: "W tym temacie przedstawiono, jak za pomocą usługi tooMedia tooconnect REST API."
services: media-services
documentationcenter: 
author: Juliako
manager: erikre
editor: 
ms.assetid: 79dc64f1-15d8-4a81-b9d9-3d3c44d2e1e8
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 09/26/2016
ms.author: juliako
ms.openlocfilehash: 1d5064a3612dc96f5c5ad910d183d84fb70a3b6a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="connecting-toomedia-services-account-using-media-services-rest-api"></a>Łączenie tooMedia konta usług przy użyciu interfejsu API REST usługi multimediów
> [!div class="op_single_selector"]
> * [.NET](media-services-dotnet-connect-programmatically.md)
> * [REST](media-services-rest-connect-programmatically.md)
> 
> 

W tym temacie opisano, jak tooobtain tooMicrosoft połączenie programowe usługi Azure Media Services są programowania z hello interfejsu API REST usługi multimediów.

Dwie czynności są wymagane podczas uzyskiwania dostępu do usługi Microsoft Azure Media Services: token dostępu udostępniane przez usługi kontroli dostępu (ACS) Azure i hello identyfikator URI usługi Media Services samej siebie. Można użyć dowolnego oznacza, że chcesz podczas tworzenia tych żądań tak długo, jak określić hello nagłówka poprawne wartości i przekaż token dostępu hello poprawnie podczas wywoływania metody do usługi Media Services.

Hello następujące kroki opisano hello najczęściej przepływu pracy, gdy za pomocą tooMedia tooconnect interfejsu API REST usług Media hello usług:

1. Pobieranie tokenu dostępu 
2. Łączenie toohello identyfikator URI usługi multimediów 
   
   > [!NOTE]
   > Po pomyślnym połączeniu toohttps://media.windows.net, otrzymasz 301 przekierowanie, określając inny identyfikator URI usługi multimediów. Należy wykonać kolejne wywołania toohello nowy identyfikator URI.
   > Otrzymasz również odpowiedź HTTP/1.1 200, która zawiera hello opis metadanych interfejsu API ODATA.
   > 
   > 
3. Po kolejnych interfejsu API wywołania toohello nowego adresu URL. 
   
    Na przykład jeśli po wypróbowaniu tooconnect, masz następujące hello:
   
        HTTP/1.1 301 Moved Permanently
        Location: https://wamsbayclus001rest-hs.cloudapp.net/api/
   
    Należy zadać programu późniejsze toohttps://wamsbayclus001rest-hs.cloudapp.net/api/ wywołania interfejsu API.

    >[!NOTE]
    >Limit różnych zasad usługi AMS wynosi 1 000 000 (na przykład zasad lokalizatorów lub ContentKeyAuthorizationPolicy). Należy używać hello tym samym identyfikatorze zasad, jeśli używasz zawsze hello sam dni / dostęp uprawnień, na przykład zasady dla lokalizatorów, które są przeznaczone tooremain w miejscu przez długi czas (zasady — przekazywanie). Aby uzyskać więcej informacji, zobacz [ten](media-services-dotnet-manage-entities.md#limit-access-policies) temat.

## <a name="access-control-address"></a>Adres kontroli dostępu
Adres kontroli dostępu do usługi Media Services jest https://wamsprodglobal001acs.accesscontrol.windows.net, z wyjątkiem Chin Północna regionu, w których jest https://wamsprodglobal001acs.accesscontrol.chinacloudapi.cn.

## <a name="getting-an-access-token"></a>Pobieranie tokenu dostępu
tooaccess Media Services bezpośrednio za pomocą hello interfejsu API REST, pobrać token dostępu z usługi kontroli dostępu i używać go podczas każdego żądania HTTP, wprowadzone do usługi hello. Token ten jest podobny tokenów tooother udostępniane przez usługi ACS na podstawie oświadczeń dostępu podany w nagłówku hello żądania HTTP i przy użyciu protokołu hello OAuth v2. Nie trzeba innych wymagań wstępnych przed bezpośredniego połączenia usługi tooMedia.

Witaj poniższy przykład przedstawia nagłówek żądania HTTP hello i tooretrieve treść, używać tokenu.

**Nagłówek**:

    POST https://wamsprodglobal001acs.accesscontrol.windows.net/v2/OAuth2-13 HTTP/1.1
    Content-Type: application/x-www-form-urlencoded
    Host: wamsprodglobal001acs.accesscontrol.windows.net
    Content-Length: 120
    Expect: 100-continue
    Connection: Keep-Alive
    Accept: application/json


**Treść**:

Należy tooprove wartości client_id i client_secret hello w treści hello tego żądania; client_id i client_secret odpowiadają toohello AccountName i AccountKey wartości, odpowiednio. Te wartości są dostarczane tooyou przez usługę Media Services, po skonfigurowaniu konta. 

Należy pamiętać, że hello AccountKey dla konta usługi Media Services musi być zakodowane w adresie URL (zobacz [kodowanie procent](http://tools.ietf.org/html/rfc3986#section-2.1) w przypadku używania go jako wartość client_secret hello w żądanie tokenu dostępu.

    grant_type=client_credentials&client_id=ams_account_name&client_secret=URL_encoded_ams_account_key&scope=urn%3aWindowsAzureMediaServices


Na przykład: 

    grant_type=client_credentials&client_id=amstestaccount001&client_secret=wUNbKhNj07oqjqU3Ah9R9f4kqTJ9avPpfe6Pk3YZ7ng%3d&scope=urn%3aWindowsAzureMediaServices


Witaj poniższy przykład przedstawia hello odpowiedź HTTP, która zawiera dostępu hello tokenu w treści odpowiedzi hello.

    HTTP/1.1 200 OK
    Cache-Control: no-cache, no-store
    Pragma: no-cache
    Content-Type: application/json; charset=utf-8
    Expires: -1
    request-id: a65150f5-2784-4a01-a4b7-33456187ad83
    X-Content-Type-Options: nosniff
    Strict-Transport-Security: max-age=31536000; includeSubDomains
    Date: Thu, 15 Jan 2015 08:07:20 GMT
    Content-Length: 670

    {  
       "token_type":"http://schemas.xmlsoap.org/ws/2009/11/swt-token-profile-1.0",
       "access_token":"http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amstestaccount001&urn%3aSubscriptionId=z7f19258-2233-4ca2-b1ae-193798e2c9d8&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1421330840&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=uf69n82KlqZmkJDNxhJkOxpyIpA2HDyeGUTtSnq1vlE%3d",
       "expires_in":"21600",
       "scope":"urn:WindowsAzureMediaServices"
    }


> [!NOTE]
> Zalecane jest toocache hello "' access_token '" i "expires_in" wartości tooan magazynu zewnętrznego. później można pobrać z magazynu hello i używać ponownie w wywołaniach interfejsu API REST usługi Media Hello danych tokenu. Jest to szczególnie przydatne w scenariuszach, gdzie hello token można bezpiecznie wymieniać między wiele procesów lub komputery.
> 
> 

Upewnij się, że wartość "expires_in" hello toomonitor dostępu hello tokenu i zaktualizuj wywołaniach interfejsu API REST przy nowe tokeny, zgodnie z potrzebami.

### <a name="connecting-toohello-media-services-uri"></a>Łączenie toohello identyfikator URI usługi multimediów
główny Hello identyfikator URI dla usługi Media Services to https://media.windows.net/. Początkowo należy połączyć toothis identyfikator URI, a można przywrócić 301 przekierowanie odpowiedzi, powinny być toohello wezwań nowy identyfikator URI. Ponadto nie należy używać wszelka logika automatycznego przekierowania/wykonania w Twoich żądań. Zlecenia HTTP i treści żądania nie zostaną przekazane toohello nowy identyfikator URI.

Należy pamiętać, że hello głównego adresu URI do przekazywania i pobierania plików zasobów jest https://yourstorageaccount.blob.core.windows.net/, gdzie nazwa konta magazynu hello jest hello samym kluczem, używane podczas Konfiguracja konta usługi Media Services.

Witaj poniższy przykład przedstawia HTTP żądania toohello Media Services głównego identyfikatora URI (https://media.windows.net/). Żądanie hello pobiera 301 przekierowanie w odpowiedzi. Witaj kolejne żądanie używa hello nowy identyfikator URI (https://wamsbayclus001rest-hs.cloudapp.net/api/).     

**Żądanie HTTP**:

    GET https://media.windows.net/ HTTP/1.1
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amstestaccount001&urn%3aSubscriptionId=z7f19258-6753-4ca2-b1ae-193798e2c9d8&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1421500579&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=ElVWXOnMVggFQl%2ft9vhdcv1qH1n%2fE8l3hRef4zPmrzg%3d
    x-ms-version: 2.11
    Accept: application/json
    Host: media.windows.net


**Odpowiedź HTTP**:

    HTTP/1.1 301 Moved Permanently
    Location: https://wamsbayclus001rest-hs.cloudapp.net/api/
    Server: Microsoft-IIS/8.5
    request-id: 987d7652-497a-44e5-b815-f492e02aef97
    x-ms-request-id: 987d7652-497a-44e5-b815-f492e02aef97
    X-Powered-By: ASP.NET
    Strict-Transport-Security: max-age=31536000; includeSubDomains
    Date: Sat, 17 Jan 2015 07:44:53 GMT
    Content-Length: 164

    <html><head><title>Object moved</title></head><body>
    <h2>Object moved too<a href="https://wamsbayclus001rest-hs.cloudapp.net/api/">here</a>.</h2>
    </body></html>


**Żądanie HTTP** (przy użyciu hello nowy identyfikator URI):

    GET https://wamsbayclus001rest-hs.cloudapp.net/api/ HTTP/1.1
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amstestaccount001&urn%3aSubscriptionId=z7f19258-2233-4ca2-b1ae-193798e2c9d8&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1421500579&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=ElVWXOnMVggFQl%2ft9vhdcv1qH1n%2fE8l3hRef4zPmrzg%3d
    x-ms-version: 2.11
    Accept: application/json
    Host: wamsbayclus001rest-hs.cloudapp.net


**Odpowiedź HTTP**:

    HTTP/1.1 200 OK
    Cache-Control: no-cache
    Content-Length: 1250
    Content-Type: application/json;odata=minimalmetadata;streaming=true;charset=utf-8
    Server: Microsoft-IIS/8.5
    request-id: 5f52ea9d-177e-48fe-9709-24953d19f84a
    x-ms-request-id: 5f52ea9d-177e-48fe-9709-24953d19f84a
    X-Content-Type-Options: nosniff
    DataServiceVersion: 3.0;
    X-Powered-By: ASP.NET
    Strict-Transport-Security: max-age=31536000; includeSubDomains
    Date: Sat, 17 Jan 2015 07:44:52 GMT

    {"odata.metadata":"https://wamsbayclus001rest-hs.cloudapp.net/api/$metadata","value":[{"name":"AccessPolicies","url":"AccessPolicies"},{"name":"Locators","url":"Locators"},{"name":"ContentKeys","url":"ContentKeys"},{"name":"ContentKeyAuthorizationPolicyOptions","url":"ContentKeyAuthorizationPolicyOptions"},{"name":"ContentKeyAuthorizationPolicies","url":"ContentKeyAuthorizationPolicies"},{"name":"Files","url":"Files"},{"name":"Assets","url":"Assets"},{"name":"AssetDeliveryPolicies","url":"AssetDeliveryPolicies"},{"name":"IngestManifestFiles","url":"IngestManifestFiles"},{"name":"IngestManifestAssets","url":"IngestManifestAssets"},{"name":"IngestManifests","url":"IngestManifests"},{"name":"StorageAccounts","url":"StorageAccounts"},{"name":"Tasks","url":"Tasks"},{"name":"NotificationEndPoints","url":"NotificationEndPoints"},{"name":"Jobs","url":"Jobs"},{"name":"TaskTemplates","url":"TaskTemplates"},{"name":"JobTemplates","url":"JobTemplates"},{"name":"MediaProcessors","url":"MediaProcessors"},{"name":"EncodingReservedUnitTypes","url":"EncodingReservedUnitTypes"},{"name":"Operations","url":"Operations"},{"name":"StreamingEndpoints","url":"StreamingEndpoints"},{"name":"Channels","url":"Channels"},{"name":"Programs","url":"Programs"}]}



> [!NOTE]
> Po pobraniu hello nowy identyfikator URI, który jest hello identyfikator URI, który powinien być toocommunicate używane z programem Media Services. 
> 
> 

## <a name="media-services-learning-paths"></a>Ścieżki szkoleniowe dotyczące usługi Media Services
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Przekazywanie opinii
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

