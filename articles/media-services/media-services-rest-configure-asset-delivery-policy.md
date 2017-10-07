---
title: "zasady dostarczania zasobów aaaConfiguring przy użyciu interfejsu API REST usług Media | Dokumentacja firmy Microsoft"
description: "W tym temacie przedstawiono sposób tooconfigure zasady dostarczania dla różnych zasobów przy użyciu interfejsu API REST usługi multimediów."
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: 5cb9d32a-e68b-4585-aa82-58dded0691d0
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/10/2017
ms.author: juliako
ms.openlocfilehash: 8203230d570935e17382c598820dbfe42f83f8d8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="configuring-asset-delivery-policies"></a>Konfigurowanie zasad dostarczania zasobów
[!INCLUDE [media-services-selector-asset-delivery-policy](../../includes/media-services-selector-asset-delivery-policy.md)]

Jeśli planujesz trwałych toodeliver dynamicznie zaszyfrowany, co hello czynnościach w ramach hello zawartości dostarczania przepływu pracy jest konfigurowanie zasad dostarczania dla zasobów usługi Media Services. zasady dostarczania elementu zawartości Hello informuje usługi Media Services sposób dla Twojego toobe zasobów dostarczyć: w przypadku protokołu przesyłania strumieniowego powinno zawartości dynamicznie umieszczone (na przykład, MPEG DASH, HLS, Smooth Streaming lub wszystkie), czy chcesz toodynamically szyfrowanie zawartości i w jaki sposób (koperty lub szyfrowania common encryption).

W tym temacie omówiono dlaczego i w jaki sposób toocreate i skonfigurować zasady dostarczania zasobów.

>[!NOTE]
>Po utworzeniu konta usługi AMS **domyślne** punktu końcowego przesyłania strumieniowego w brzmieniu konta tooyour hello **zatrzymane** stanu. przesyłanie strumieniowe zawartości i podejmij korzyści z dynamicznego tworzenia pakietów i dynamicznego szyfrowania toostart hello punktu końcowego przesyłania strumieniowego, z którego mają zostać toostream zawartość ma toobe w hello **systemem** stanu. 
>
>Ponadto toobe toouse stanie dynamicznego tworzenia pakietów i dynamicznego szyfrowania zawartości musi zawierać zestaw o adaptacyjnej szybkości bitowej MP4s lub pliki Smooth Streaming adaptacyjną szybkością transmisji bitów.

Toohello różnych zasad można zastosować elementu zawartości. Na przykład można zastosować PlayReady szyfrowania tooSmooth przesyłania strumieniowego i szyfrowanie AES Envelope szyfrowania tooMPEG kreska i HLS. Wszystkie protokoły, które nie są zdefiniowane w zasadzie dostarczania (na przykład dodać jedną zasadę, która tylko określa hello protokół HLS), zostanie zablokowany przesyłania strumieniowego. toothis wyjątek Hello jest, jeśli masz nie zdefiniowano zasad dostarczania elementów zawartości. Następnie wszystkie protokoły mogą być przesyłane hello Wyczyść.

Chcąc toodeliver zasób zaszyfrowanych magazynu, należy skonfigurować zasady dostarczania zasobów hello. Przed zawartości mogą być przesyłane strumieniowo, hello i przesyłania strumieniowego szyfrowania magazynu hello usuwa strumieni zawartości przy użyciu hello określone zasady dostarczania. Na przykład toodeliver zawartości zaszyfrowane za pomocą klucza szyfrowania koperty Advanced Encryption (Standard AES), Ustaw typ zasad hello zbyt**DynamicEnvelopeEncryption**. szyfrowanie magazynu tooremove i zasobów hello strumienia w hello Wyczyść, Ustaw typ zasad hello zbyt**NoDynamicEncryption**. Przykłady, które pokazują, jak tooconfigure tych typów zasad należy wykonać.

W zależności od konfiguracji zasad dostarczania elementów zawartości hello czy pakietu toodynamically może być dynamicznie szyfrowania i strumienia powitania po protokołów przesyłania strumieniowego: Smooth Streaming, HLS, strumieni MPEG DASH.

powitania po hello pokazuje listę formatuje użycie toostream Smooth, HLS, DASH.

Funkcje Smooth Streaming:

{nazwa punktu końcowego przesyłania strumieniowego-nazwa konta usługi Media Services}.streaming.mediaservices.windows.net/{identyfikator lokalizatora}/{nazwa pliku}.ism/Manifest

HLS:

{name}.streaming.mediaservices.windows.net/{locator konta usługi media Nazwa punktu końcowego ID}/{filename}.ism/Manifest(format=m3u8-aapl) przesyłania strumieniowego

MPEG DASH

{name}.streaming.mediaservices.windows.net/{locator konta usługi media Nazwa punktu końcowego ID}/{filename}.ism/Manifest(format=mpd-time-csf) przesyłania strumieniowego


Aby uzyskać instrukcje dotyczące sposobu toopublish zasobów i kompilacji adresu URL przesyłania strumieniowego, zobacz [zbudować adresu URL przesyłania strumieniowego](media-services-deliver-streaming-content.md).

## <a name="considerations"></a>Zagadnienia do rozważenia
* Nie można usunąć AssetDeliveryPolicy skojarzone z zasobów, gdy Lokalizator OnDemand (streaming) istnieje dla tego zasobu. zalecenie Hello jest tooremove hello zasady z zasobu hello przed usunięciem hello zasad.
* Nie można utworzyć Lokalizator przesyłania strumieniowego magazynu trwałego zaszyfrowane, jeśli ustawiono nie zasad dostarczania elementów zawartości.  Jeśli hello zasobów nie jest szyfrowany w magazynie, hello system umożliwi utworzyć lokalizator i strumień zasobów hello w hello wyczyść bez zasad dostarczania elementów zawartości.
* Może mieć wiele zasady dostarczania zasobów skojarzonych z pojedynczego zasobu, ale można określić tylko jednokierunkowe toohandle AssetDeliveryProtocol danego.  Co oznacza, Jeśli spróbujesz toolink dwóch dostarczania zasad określających hello AssetDeliveryProtocol.SmoothStreaming protokół, który spowoduje błąd, ponieważ hello system nie może określić, która z nich ma tooapply gdy klient przesyła żądanie Smooth Streaming.
* Jeśli zasób z istniejących Lokalizator przesyłania strumieniowego, nie można połączyć nowych zasobów toohello zasad, Rozłącz istniejące zasady z zasobu hello lub zaktualizowania zasad dostarczania skojarzone z zasobów hello.  Najpierw ma Lokalizator przesyłania strumieniowego hello tooremove, Dostosuj zasady hello i ponownie utwórz hello przesyłania strumieniowego lokalizatora.  Możesz użyć powitalne tego samego locatorId podczas ponownego tworzenia hello przesyłania strumieniowego lokalizatora, ale powinien zapewnić, że nie będzie powodować problemy dla klientów, ponieważ zawartości mogą być buforowane pochodzenia hello lub podrzędne CDN.

>[!NOTE]

>Podczas uzyskiwania dostępu do obiektów w usłudze Media Services, należy ustawić określonych pól nagłówka i wartości w Twoich żądań HTTP. Aby uzyskać więcej informacji, zobacz [ustawień dla rozwoju interfejsu API REST usługi Media](media-services-rest-how-to-use.md).

## <a name="connect-toomedia-services"></a>Połączenie usług tooMedia

Aby uzyskać informacje dotyczące tooconnect toohello AMS interfejsu API, zobacz temat [hello dostępu do interfejsu API usługi Azure Media Services przy użyciu uwierzytelniania usługi Azure AD](media-services-use-aad-auth-to-access-ams-api.md). 

>[!NOTE]
>Po pomyślnym połączeniu toohttps://media.windows.net, otrzymasz 301 przekierowanie, określając inny identyfikator URI usługi multimediów. Należy wykonać kolejne wywołania toohello nowy identyfikator URI.

## <a name="clear-asset-delivery-policy"></a>Zasady dostarczania elementu zawartości wyczyść
### <a id="create_asset_delivery_policy"></a>Tworzenie zasad dostarczania elementów zawartości
Witaj następujące żądania HTTP tworzy zasady dostarczania elementu zawartości, określająca toonot Zastosuj dynamicznego szyfrowania i protokoły toodeliver hello strumienia w jednym z następujących hello: MPEG DASH, HLS i Smooth Streaming protokołów. 

Informacje o jakie wartości można określić podczas tworzenia AssetDeliveryPolicy, zobacz hello [typów używanych podczas definiowania AssetDeliveryPolicy](#types) sekcji.   

Żądanie:

    POST https://media.windows.net/api/AssetDeliveryPolicies HTTP/1.1
    Content-Type: application/json
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amsaccount1&urn%3aSubscriptionId=zbbef702-e769-2233-9f16-bc4d3aa97387&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1423397827&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=Szo6lbJAvL3dyecAeVmyAnzv3mGzfUNClR5shk9Ivbk%3d
    x-ms-version: 2.11
    x-ms-client-request-id: 4651882c-d7ad-4d5e-86ab-f07f47dcb41e
    Host: media.windows.net

    {"Name":"Clear Policy",
    "AssetDeliveryProtocol":7,
    "AssetDeliveryPolicyType":2,
    "AssetDeliveryConfiguration":null}

Odpowiedź:

    HTTP/1.1 201 Created
    Cache-Control: no-cache
    Content-Length: 363
    Content-Type: application/json;odata=minimalmetadata;streaming=true;charset=utf-8
    Location: https://media.windows.net/api/AssetDeliveryPolicies('nb%3Aadpid%3AUUID%3A92b0f6ba-3c9f-49b6-a5fa-2a8703b04ecd')
    Server: Microsoft-IIS/8.5
    x-ms-client-request-id: 4651882c-d7ad-4d5e-86ab-f07f47dcb41e
    request-id: 6aedbf93-4bc2-4586-8845-fd45590136af
    x-ms-request-id: 6aedbf93-4bc2-4586-8845-fd45590136af
    X-Content-Type-Options: nosniff
    DataServiceVersion: 3.0;
    X-Powered-By: ASP.NET
    Strict-Transport-Security: max-age=31536000; includeSubDomains
    Date: Sun, 08 Feb 2015 06:21:27 GMT

    {"odata.metadata":"https://media.windows.net/api/$metadata#AssetDeliveryPolicies/@Element",
    "Id":"nb:adpid:UUID:92b0f6ba-3c9f-49b6-a5fa-2a8703b04ecd",
    "Name":"Clear Policy",
    "AssetDeliveryProtocol":7,
    "AssetDeliveryPolicyType":2,
    "AssetDeliveryConfiguration":null,
    "Created":"2015-02-08T06:21:27.6908329Z",
    "LastModified":"2015-02-08T06:21:27.6908329Z"}

### <a id="link_asset_with_asset_delivery_policy"></a>Łącze zasobów z zasad dostarczania elementów zawartości
powitania po hello łącza żądania HTTP określone zasady dostarczania elementu zawartości toohello zasobów do.

Żądanie:

    POST https://media.windows.net/api/Assets('nb%3Acid%3AUUID%3A86933344-9539-4d0c-be7d-f842458693e0')/$links/DeliveryPolicies HTTP/1.1
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    Content-Type: application/json
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amsaccount1&urn%3aSubscriptionId=zbbef702-e769-3344-9f16-bc4d3aa97387&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1423397827&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=Szo6lbJAvL3dyecAeVmyAnzv3mGzfUNClR5shk9Ivbk%3d
    x-ms-version: 2.11
    x-ms-client-request-id: 56d2763f-6e72-419d-ba3c-685f6db97e81
    Host: media.windows.net

    {"uri":"https://media.windows.net/api/AssetDeliveryPolicies('nb%3Aadpid%3AUUID%3A92b0f6ba-3c9f-49b6-a5fa-2a8703b04ecd')"}

Odpowiedź:

    HTTP/1.1 204 No Content


## <a name="dynamicenvelopeencryption-asset-delivery-policy"></a>Zasady dostarczania elementu zawartości DynamicEnvelopeEncryption
### <a name="create-content-key-of-hello-envelopeencryption-type-and-link-it-toohello-asset"></a>Utwórz klucz zawartości typu EnvelopeEncryption hello i połącz go toohello zasobów
Podczas określania zasad dostarczania DynamicEnvelopeEncryption, należy się toolink toomake klucz zawartości zasobów tooa z hello EnvelopeEncryption typu. Aby uzyskać więcej informacji, zobacz: [Tworzenie klucza zawartości](media-services-rest-create-contentkey.md)).

### <a id="get_delivery_url"></a>Pobieranie adresu URL dostarczania
Get hello dostarczania adres URL hello określona metoda dostarczania hello klucza zawartości utworzony w poprzednim kroku hello. Klient używa hello toorequest adresu URL zwróciła klucza AES lub licencji PlayReady w kolejności tooplayback hello chronionej zawartości.

Określ typ hello hello tooget adres URL w treści żądania HTTP hello hello. W przypadku ochrony zawartości przy użyciu usługi PlayReady, żądanie adresu URL pozyskiwania licencji PlayReady usług nośnika przy użyciu 1 dla hello keyDeliveryType: {"keyDeliveryType": 1}. W przypadku ochrony zawartości przy użyciu szyfrowania koperty hello żądanie adresu URL pozyskiwania kluczy, określając 2 dla keyDeliveryType: {"keyDeliveryType": 2}.

Żądanie:

    POST https://media.windows.net/api/ContentKeys('nb:kid:UUID:dc88f996-2859-4cf7-a279-c52a9d6b2f04')/GetKeyDeliveryUrl HTTP/1.1
    Content-Type: application/json
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amsaccount1&urn%3aSubscriptionId=zbbef702-2233-477b-9f16-bc4d3aa97387&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1423452029&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=IEXV06e3drSIN5naFRBdhJZCbfEqQbFZsGSIGmawhEo%3d
    x-ms-version: 2.11
    x-ms-client-request-id: 569d4b7c-a446-4edc-b77c-9fb686083dd8
    Host: media.windows.net
    Content-Length: 21

    {"keyDeliveryType":2}

Odpowiedź:

    HTTP/1.1 200 OK
    Cache-Control: no-cache
    Content-Length: 198
    Content-Type: application/json;odata=minimalmetadata;streaming=true;charset=utf-8
    Server: Microsoft-IIS/8.5
    x-ms-client-request-id: 569d4b7c-a446-4edc-b77c-9fb686083dd8
    request-id: d26f65d2-fe65-4136-8fcf-31545be68377
    x-ms-request-id: d26f65d2-fe65-4136-8fcf-31545be68377
    X-Content-Type-Options: nosniff
    DataServiceVersion: 3.0;
    Strict-Transport-Security: max-age=31536000; includeSubDomains
    Date: Sun, 08 Feb 2015 21:42:30 GMT

    {"odata.metadata":"media.windows.net/api/$metadata#Edm.String","value":"https://amsaccount1.keydelivery.mediaservices.windows.net/?KID=dc88f996-2859-4cf7-a279-c52a9d6b2f04"}


### <a name="create-asset-delivery-policy"></a>Tworzenie zasad dostarczania elementów zawartości
Witaj następujące żądania HTTP tworzy hello **AssetDeliveryPolicy** będący szyfrowania dynamicznego koperty tooapply skonfigurowany (**DynamicEnvelopeEncryption**) toohello **HLS**protokołu (w tym przykładzie innych protokołów będzie blokowany przesyłania strumieniowego). 

Informacje o jakie wartości można określić podczas tworzenia AssetDeliveryPolicy, zobacz hello [typów używanych podczas definiowania AssetDeliveryPolicy](#types) sekcji.   

Żądanie:

    POST https://media.windows.net/api/AssetDeliveryPolicies HTTP/1.1
    Content-Type: application/json
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    User-Agent: Microsoft ADO.NET Data Services
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amsaccount1&urn%3aSubscriptionId=zbbef702-2233-477b-9f16-bc4d3aa97387&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1423480651&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=T2FG3tIV0e2ETzxQ6RDWxWAsAzuy3ez2ruXPhrBe62Y%3d
    x-ms-version: 2.11
    x-ms-client-request-id: fff319f6-71dd-4f6c-af27-b675c0066fa7
    Host: media.windows.net

    {"Name":"AssetDeliveryPolicy","AssetDeliveryProtocol":4,"AssetDeliveryPolicyType":3,"AssetDeliveryConfiguration":"[{\"Key\":2,\"Value\":\"https:\\/\\/amsaccount1.keydelivery.mediaservices.windows.net\\/\"}]"}


Odpowiedź:

    HTTP/1.1 201 Created
    Cache-Control: no-cache
    Content-Length: 460
    Content-Type: application/json;odata=minimalmetadata;streaming=true;charset=utf-8
    Location: media.windows.net/api/AssetDeliveryPolicies('nb%3Aadpid%3AUUID%3Aec9b994e-672c-4a5b-8490-a464eeb7964b')
    Server: Microsoft-IIS/8.5
    x-ms-client-request-id: fff319f6-71dd-4f6c-af27-b675c0066fa7
    request-id: c2a1ac0e-9644-474f-b38f-b9541c3a7c5f
    x-ms-request-id: c2a1ac0e-9644-474f-b38f-b9541c3a7c5f
    X-Content-Type-Options: nosniff
    DataServiceVersion: 3.0;
    Strict-Transport-Security: max-age=31536000; includeSubDomains
    Date: Mon, 09 Feb 2015 05:24:38 GMT

    {"odata.metadata":"media.windows.net/api/$metadata#AssetDeliveryPolicies/@Element","Id":"nb:adpid:UUID:ec9b994e-672c-4a5b-8490-a464eeb7964b","Name":"AssetDeliveryPolicy","AssetDeliveryProtocol":4,"AssetDeliveryPolicyType":3,"AssetDeliveryConfiguration":"[{\"Key\":2,\"Value\":\"https:\\/\\/amsaccount1.keydelivery.mediaservices.windows.net\\/\"}]","Created":"2015-02-09T05:24:38.9167436Z","LastModified":"2015-02-09T05:24:38.9167436Z"}


### <a name="link-asset-with-asset-delivery-policy"></a>Łącze zasobów z zasad dostarczania elementów zawartości
Zobacz [zasobów łącza z zasad dostarczania elementów zawartości](#link_asset_with_asset_delivery_policy)

## <a name="dynamiccommonencryption-asset-delivery-policy"></a>Zasady dostarczania elementu zawartości DynamicCommonEncryption
### <a name="create-content-key-of-hello-commonencryption-type-and-link-it-toohello-asset"></a>Utwórz klucz zawartości typu CommonEncryption hello i połącz go toohello zasobów
Podczas określania zasad dostarczania DynamicCommonEncryption, należy się toolink toomake klucz zawartości zasobów tooa z hello CommonEncryption typu. Aby uzyskać więcej informacji, zobacz: [Tworzenie klucza zawartości](media-services-rest-create-contentkey.md)).

### <a name="get-delivery-url"></a>Pobieranie adresu URL dostarczania
Pobierz adres URL dostarczania hello metoda dostarczania PlayReady hello hello klucza zawartości utworzony w poprzednim kroku hello. Klient używa hello zwrócił toorequest adres URL licencji PlayReady w kolejności tooplayback hello chronione zawartości. Aby uzyskać więcej informacji, zobacz [uzyskać adres URL dostarczania](#get_delivery_url).

### <a name="create-asset-delivery-policy"></a>Tworzenie zasad dostarczania elementów zawartości
Witaj następujące żądania HTTP tworzy hello **AssetDeliveryPolicy** który jest skonfigurowany tooapply dynamicznego szyfrowania common encryption (**DynamicCommonEncryption**) toohello **Smooth Streaming**  protokołu (w tym przykładzie innych protokołów będzie blokowany przesyłania strumieniowego). 

Informacje o jakie wartości można określić podczas tworzenia AssetDeliveryPolicy, zobacz hello [typów używanych podczas definiowania AssetDeliveryPolicy](#types) sekcji.   

Żądanie:

    POST https://media.windows.net/api/AssetDeliveryPolicies HTTP/1.1
    Content-Type: application/json
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    User-Agent: Microsoft ADO.NET Data Services
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amsaccount1&urn%3aSubscriptionId=zbbef702-2233-477b-9f16-bc4d3aa97387&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1423480651&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=T2FG3tIV0e2ETzxQ6RDWxWAsAzuy3ez2ruXPhrBe62Y%3d
    x-ms-version: 2.11
    x-ms-client-request-id: fff319f6-71dd-4f6c-af27-b675c0066fa7
    Host: media.windows.net

    {"Name":"AssetDeliveryPolicy","AssetDeliveryProtocol":1,"AssetDeliveryPolicyType":4,"AssetDeliveryConfiguration":"[{\"Key\":2,\"Value\":\"https:\\/\\/amsaccount1.keydelivery.mediaservices.windows.net\/PlayReady\/"}]"}


Jeśli chcesz tooprotect zawartości przy użyciu Widevine DRM, zaktualizuj hello AssetDeliveryConfiguration wartości toouse WidevineLicenseAcquisitionUrl (który ma wartość hello 7) i określ hello adres URL usługi dostarczania licencji. Można użyć powitania po dostarczania licencji Widevine toohelp partnerów AMS: [Axinom](http://www.axinom.com/press/ibc-axinom-drm-6/), [EZDRM](http://ezdrm.com/), [castLabs](http://castlabs.com/company/partners/azure/).

Na przykład: 

    {"Name":"AssetDeliveryPolicy","AssetDeliveryProtocol":2,"AssetDeliveryPolicyType":4,"AssetDeliveryConfiguration":"[{\"Key\":7,\"Value\":\"https:\\/\\/example.net\/WidevineLicenseAcquisition\/"}]"}

> [!NOTE]
> W przypadku szyfrowania przy użyciu metody Widevine, tylko będzie możliwe toodeliver przy użyciu kreska. Upewnij się, że Protokół dostarczania elementów zawartości (2) w hello toospecify KRESKI.
> 
> 

### <a name="link-asset-with-asset-delivery-policy"></a>Łącze zasobów z zasad dostarczania elementów zawartości
Zobacz [zasobów łącza z zasad dostarczania elementów zawartości](#link_asset_with_asset_delivery_policy)

## <a id="types"></a>Typy używane podczas definiowania AssetDeliveryPolicy

### <a name="assetdeliveryprotocol"></a>AssetDeliveryProtocol

Witaj następujące wyliczenia opisano wartości ustawione przez protokół dostarczania elementów zawartości hello.

    [Flags]
    public enum AssetDeliveryProtocol
    {
        /// <summary>
        /// No protocols.
        /// </summary>
        None = 0x0,

        /// <summary>
        /// Smooth streaming protocol.
        /// </summary>
        SmoothStreaming = 0x1,

        /// <summary>
        /// MPEG Dynamic Adaptive Streaming over HTTP (DASH)
        /// </summary>
        Dash = 0x2,

        /// <summary>
        /// Apple HTTP Live Streaming protocol.
        /// </summary>
        HLS = 0x4,

        ProgressiveDownload = 0x10, 
 
        /// <summary>
        /// Include all protocols.
        /// </summary>
        All = 0xFFFF
    }

### <a name="assetdeliverypolicytype"></a>AssetDeliveryPolicyType

Witaj następujące wyliczenia opisano wartości, które można ustawić dla typu zasady dostarczania elementu zawartości hello.  

    public enum AssetDeliveryPolicyType
    {
        /// <summary>
        /// Delivery Policy Type not set.  An invalid value.
        /// </summary>
        None,

        /// <summary>
        /// hello Asset should not be delivered via this AssetDeliveryProtocol. 
        /// </summary>
        Blocked, 

        /// <summary>
        /// Do not apply dynamic encryption toohello asset.
        /// </summary>
        /// 
        NoDynamicEncryption,  

        /// <summary>
        /// Apply Dynamic Envelope encryption.
        /// </summary>
        DynamicEnvelopeEncryption,

        /// <summary>
        /// Apply Dynamic Common encryption.
        /// </summary>
        DynamicCommonEncryption
        }

### <a name="contentkeydeliverytype"></a>ContentKeyDeliveryType

Witaj następujące wyliczenia opisano wartości można użyć metody dostarczania hello tooconfigure powitania klienta toohello klucza zawartości.
    
    public enum ContentKeyDeliveryType
    {
        /// <summary>
        /// None.
        ///
        </summary>
        None = 0,

        /// <summary>
        /// Use PlayReady License acquistion protocol
        ///
        </summary>
        PlayReadyLicense = 1,

        /// <summary>
        /// Use MPEG Baseline HTTP key protocol.
        ///
        </summary>
        BaselineHttp = 2,

        /// <summary>
        /// Use Widevine License acquistion protocol
        ///
        </summary>
        Widevine = 3

    }


### <a name="assetdeliverypolicyconfigurationkey"></a>AssetDeliveryPolicyConfigurationKey

powitania po wyliczenia opisano wartości, które można ustawić określonej konfiguracji tooget tooconfigure klucze używane dla zasad dostarczania elementów zawartości.

    public enum AssetDeliveryPolicyConfigurationKey
    {
        /// <summary>
        /// No policies.
        /// </summary>
        None,

        /// <summary>
        /// Exact Envelope key URL.
        /// </summary>
        EnvelopeKeyAcquisitionUrl,

        /// <summary>
        /// Base key url that will have KID=<Guid> appended for Envelope.
        /// </summary>
        EnvelopeBaseKeyAcquisitionUrl,

        /// <summary>
        /// hello initialization vector toouse for envelope encryption in Base64 format.
        /// </summary>
        EnvelopeEncryptionIVAsBase64,

        /// <summary>
        /// hello PlayReady License Acquisition Url toouse for common encryption.
        /// </summary>
        PlayReadyLicenseAcquisitionUrl,

        /// <summary>
        /// hello PlayReady Custom Attributes tooadd toohello PlayReady Content Header
        /// </summary>
        PlayReadyCustomAttributes,

        /// <summary>
        /// hello initialization vector toouse for envelope encryption.
        /// </summary>
        EnvelopeEncryptionIV,

        /// <summary>
        /// Widevine DRM acquisition url
        /// </summary>
        WidevineLicenseAcquisitionUrl
    }

## <a name="media-services-learning-paths"></a>Ścieżki szkoleniowe dotyczące usługi Media Services
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Przekazywanie opinii
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

