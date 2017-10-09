---
title: "wprowadzenie do dostarczania zawartości na żądanie przy użyciu REST aaaGet | Dokumentacja firmy Microsoft"
description: "Ten samouczek przedstawia kroki hello wdrażania aplikacji dostarczania zawartości na żądanie przy użyciu interfejsu API REST usługi Azure Media Services."
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: 88194b59-e479-43ac-b179-af4f295e3780
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/10/2017
ms.author: juliako
ms.openlocfilehash: f270ed59e9ae9745e8403ec6e19d5c3533fc82b7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-delivering-content-on-demand-using-rest"></a>Wprowadzenie do dostarczania zawartości na żądanie za pomocą usługi REST
[!INCLUDE [media-services-selector-get-started](../../includes/media-services-selector-get-started.md)]

Ta opcja szybkiego startu przeprowadzi Cię przez kroki wdrażania aplikacji do dostarczania zawartości wideo na żądanie (VoD) przy użyciu interfejsów API REST usługi Azure Media Services (AMS) hello.

Samouczek Hello wprowadza hello podstawowy przepływ pracy usług Media Services i hello najczęściej obiekty i zadania programowania wymagane do tworzenia usługi Media Services. Po ukończeniu hello samouczka hello będzie toostream może być lub pobrać progresywnie przykładowy plik nośnika, który przekazany, zakodowany i pobierane.

Witaj poniższej ilustracji przedstawiono niektóre obiekty hello najczęściej używane podczas tworzenia aplikacji VoD hello Media Services OData modelu.

Kliknij przycisk tooview obraz powitania pełny jego rozmiar.  

<a href="./media/media-services-rest-get-started/media-services-overview-object-model.png" target="_blank"><img src="./media/media-services-rest-get-started/media-services-overview-object-model-small.png"></a> 

## <a name="prerequisites"></a>Wymagania wstępne
Witaj następujące wymagania wstępne są wymagane toostart programowania z użyciem usługi Media Services z interfejsów API REST.

* Konto platformy Azure. Aby uzyskać szczegółowe informacje, zobacz artykuł [Bezpłatna wersja próbna platformy Azure](https://azure.microsoft.com/pricing/free-trial/).
* Konto usługi Media Services. Zobacz toocreate konto usługi Media Services [jak tooCreate konta usługi Media Services](media-services-portal-create-account.md).
* Opis sposobu toodevelop z interfejsu API REST usługi multimediów. Aby uzyskać więcej informacji, zobacz [omówienie interfejsu API REST usług Media](media-services-rest-how-to-use.md).
* Aplikacja, który może wysyłać żądań i odpowiedzi HTTP. W tym samouczku używana [Fiddler](http://www.telerik.com/download/fiddler).

Witaj następujące zadania są wyświetlane w tego przewodnika Szybki Start.

1. Początek (przy użyciu portalu Azure hello) punktu końcowego przesyłania strumieniowego.
2. Konto usługi Media Services toohello Uzyskuj dostęp do interfejsu API REST.
3. Tworzenie nowego elementu zawartości i przekazywanie pliku wideo z interfejsu API REST.
4. Koduj plik źródłowy hello do zestawu plików MP4 o adaptacyjnej szybkości bitowej z interfejsu API REST.
5. Publikowanie zawartości hello i get przesyłania strumieniowego i pobierania progresywnego adresy URL z interfejsu API REST.
6. Odtwarzanie zawartości.

>[!NOTE]
>Limit różnych zasad usługi AMS wynosi 1 000 000 (na przykład zasad lokalizatorów lub ContentKeyAuthorizationPolicy). Należy używać hello tym samym identyfikatorze zasad, jeśli używasz zawsze hello sam dni / dostęp uprawnień, na przykład zasady dla lokalizatorów, które są przeznaczone tooremain w miejscu przez długi czas (zasady — przekazywanie). Aby uzyskać więcej informacji, zobacz [ten](media-services-dotnet-manage-entities.md#limit-access-policies) temat.

Aby uzyskać szczegółowe informacje na temat jednostek AMS REST używaną w tym temacie, zobacz [dokumentacja interfejsu API REST usługi Azure Media Services](/rest/api/media/services/azure-media-services-rest-api-reference). Zobacz też [pojęcia dotyczące usługi Azure Media Services](media-services-concepts.md).

>[!NOTE]
>Podczas uzyskiwania dostępu do obiektów w usłudze Media Services, należy ustawić określonych pól nagłówka i wartości w Twoich żądań HTTP. Aby uzyskać więcej informacji, zobacz [ustawień dla rozwoju interfejsu API REST usługi Media](media-services-rest-how-to-use.md).

## <a name="start-streaming-endpoints-using-hello-azure-portal"></a>Uruchom przy użyciu portalu Azure hello punkty końcowe przesyłania strumieniowego

Podczas pracy w usłudze Azure Media Services jednym z hello najbardziej typowych scenariuszy jest dostarczanie plików wideo przy użyciu przesyłania strumieniowego adaptacyjną szybkością transmisji bitów. Usługa Media Services udostępnia funkcję dynamicznego tworzenia pakietów, co pozwala toodeliver adaptacyjnej szybkości bitowej MP4 zakodowane zawartości w formatach transmisji strumieniowej obsługiwanych przez usługi Media Services (MPEG DASH, HLS, Smooth Streaming) just-in-time, bez konieczności toostore wstępnie umieszczone wersje każdego z tych formatach.

>[!NOTE]
>Po utworzeniu konta usługi AMS **domyślne** punktu końcowego przesyłania strumieniowego w brzmieniu konta tooyour hello **zatrzymane** stanu. przesyłanie strumieniowe zawartości i podejmij korzyści z dynamicznego tworzenia pakietów i dynamicznego szyfrowania toostart hello punktu końcowego przesyłania strumieniowego, z którego mają zostać toostream zawartość ma toobe w hello **systemem** stanu.

toostart hello punktu końcowego przesyłania strumieniowego, hello następujące:

1. Zaloguj się w hello [portalu Azure](https://portal.azure.com/).
2. W oknie Ustawienia powitania kliknij punkty końcowe przesyłania strumieniowego.
3. Kliknij przycisk domyślny hello punktu końcowego przesyłania strumieniowego.

    zostanie wyświetlone okno Szczegóły punktu KOŃCOWEGO przesyłania STRUMIENIOWEGO domyślne Hello.

4. Kliknij ikonę Start hello.
5. Kliknij przycisk toosave przycisk Zapisz hello zmiany.

## <a id="connect"></a>Konto usługi Media Services toohello Uzyskuj dostęp do interfejsu API REST

Aby uzyskać informacje dotyczące tooconnect toohello AMS interfejsu API, zobacz temat [hello dostępu do interfejsu API usługi Azure Media Services przy użyciu uwierzytelniania usługi Azure AD](media-services-use-aad-auth-to-access-ams-api.md). 

>[!NOTE]
>Po pomyślnym połączeniu toohttps://media.windows.net, otrzymasz 301 przekierowanie, określając inny identyfikator URI usługi multimediów. Należy wykonać kolejne wywołania toohello nowy identyfikator URI.

Na przykład jeśli po wypróbowaniu tooconnect, masz następujące hello:

    HTTP/1.1 301 Moved Permanently
    Location: https://wamsbayclus001rest-hs.cloudapp.net/api/

Należy zadać programu późniejsze toohttps://wamsbayclus001rest-hs.cloudapp.net/api/ wywołania interfejsu API.

## <a id="upload"></a>Tworzenie nowego elementu zawartości i przekazywanie pliku wideo z interfejsu API REST

Za pomocą usługi Media Services można przekazać pliki cyfrowe do elementu zawartości. Witaj **zasobów** może zawierać wideo, audio, obrazy, kolekcje miniatur, tekst ścieżek i napisów plików (i hello metadane dotyczące tych plików.)  Po hello pliki są przekazywane do hello zawartości, zawartość jest bezpiecznie przechowywana w chmurze powitania dla dalszego przetwarzania i przesyłania strumieniowego.

Jedna z wartości hello ma tooprovide, podczas tworzenia zasobu jest opcji tworzenia elementów zawartości. Witaj **opcje** właściwość jest wartością wyliczenia, który opisuje opcje szyfrowania hello, które można utworzyć zasobu z. Nieprawidłowa wartość jest jedną z wartości hello z listy hello poniżej nie kombinację wartości z tej listy:

* **Brak** = **0** — szyfrowanie nie jest stosowane. Korzystając z tej opcji zawartość nie jest chroniona w trakcie przesyłania lub przechowywania w magazynie.
    Jeśli planujesz toodeliver MP4 przy użyciu pobierania progresywnego, użyj tej opcji.
* **StorageEncrypted** = **1** — szyfruje zawartości lokalnie, przy użyciu standardu AES 256-bitowego, a następnie przekazanie jej tooAzure magazynu, w którym są przechowywane szyfrowane, gdy. Elementy zawartości chronione przy użyciu szyfrowania magazynu są automatycznie bez szyfrowania i umieszczana w poprzednich tooencoding systemu szyfrowania plików i opcjonalnie ponownie szyfrowane przed toouploading zwrotnym w formie nowego elementu zawartości wyjściowej. Witaj pierwotnym zastosowaniem szyfrowania magazynu jest toosecure Twojego wysokiej jakości multimedialnych plików wejściowych z silne szyfrowanie przechowywanych na dysku.
* **CommonEncryptionProtected** = **2** — ta opcja umożliwia przekazanie zawartości, który został już szyfrowane i chronione za pomocą wspólnego szyfrowania lub technologii PlayReady DRM (na przykład, Smooth Streaming chronione przy użyciu technologii PlayReady DRM).
* **EnvelopeEncryptionProtected** = **4** — Użyj tej opcji, Jeśli przesyłasz HLS zaszyfrowanych z użyciem standardu AES. pliki Hello musi zostały zakodowane i zaszyfrowane przez Transform Manager.

### <a name="create-an-asset"></a>Utwórz zasób
Zasób jest kontenerem dla wielu typów lub zestawów obiektów w usłudze Media Services: wideo, audio, obrazy, kolekcje miniatur, ścieżek tekstu i pliki napisów. W hello interfejsu API REST, tworzenie zasobu wymaga wysyłania POST wysyłanie żądań usług tooMedia i umieszczenie wszelkie informacje o zawartości w treści żądania hello.

powitania po przykładzie pokazano, jak toocreate zasób.

**Żądania HTTP**

    POST https://wamsbayclus001rest-hs.cloudapp.net/api/Assets HTTP/1.1
    Content-Type: application/json
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amstestaccount001&urn%3aSubscriptionId=z7f09258-2233-4ca2-b1ae-193798e2c9d8&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1421640053&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=vlG%2fPYdFDMS1zKc36qcFVWnaNh07UCkhYj3B71%2fk1YA%3d
    x-ms-version: 2.11
    x-ms-client-request-id: c59de965-bc89-4295-9a57-75d897e5221e
    Host: wamsbayclus001rest-hs.cloudapp.net
    Content-Length: 45

    {"Name":"BigBuckBunny.mp4", "Options":"0"}


**Odpowiedź HTTP**

W przypadku powodzenia zwrócono hello następujące czynności:

    HTTP/1.1 201 Created
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
    X-Powered-By: ASP.NET
    Strict-Transport-Security: max-age=31536000; includeSubDomains
    Date: Sun, 18 Jan 2015 22:06:40 GMT

    {  
       "odata.metadata":"https://wamsbayclus001rest-hs.cloudapp.net/api/$metadata#Assets/@Element",
       "Id":"nb:cid:UUID:9bc8ff20-24fb-4fdb-9d7c-b04c7ee573a1",
       "State":0,
       "Created":"2015-01-18T22:06:40.6010903Z",
       "LastModified":"2015-01-18T22:06:40.6010903Z",
       "AlternateId":null,
       "Name":"BigBuckBunny2.mp4",
       "Options":0,
       "Uri":"https://storagetestaccount001.blob.core.windows.net/asset-9bc8ff20-24fb-4fdb-9d7c-b04c7ee573a1",
       "StorageAccountName":"storagetestaccount001"
    }

### <a name="create-an-assetfile"></a>Utwórz AssetFile
Witaj [AssetFile](https://docs.microsoft.com/rest/api/media/operations/assetfile) jednostki reprezentuje plik wideo lub audio, który jest przechowywany w kontenerze obiektów blob. Plik zasobów zawsze jest skojarzony z zasobem i zasobów może zawierać jeden lub wiele AssetFiles. Witaj Media Encoder usług zadanie nie powiedzie się, jeśli obiekt pliku zasobu nie jest skojarzony z pliku cyfrowego w kontenerze obiektów blob.

Po przekazaniu pliku nośnika cyfrowego do kontenera obiektów blob, użyj hello **scalania** żądania HTTP tooupdate hello AssetFile informacje o pliku nośnika (jak pokazano w dalszej części tematu hello).

**Żądania HTTP**

    POST https://wamsbayclus001rest-hs.cloudapp.net/api/Files HTTP/1.1
    Content-Type: application/json
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amstestaccount001&urn%3aSubscriptionId=z7f09258-2233-4ca2-b1ae-193798e2c9d8&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1421640053&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=vlG%2fPYdFDMS1zKc36qcFVWnaNh07UCkhYj3B71%2fk1YA%3d
    x-ms-version: 2.11
    Host: wamsbayclus001rest-hs.cloudapp.net
    Content-Length: 164

    {  
       "IsEncrypted":"false",
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
       "EncryptionVersion":null,
       "EncryptionScheme":null,
       "IsEncrypted":false,
       "EncryptionKeyId":null,
       "InitializationVector":null,
       "IsPrimary":false,
       "LastModified":"2015-01-19T00:34:08.1934137Z",
       "Created":"2015-01-19T00:34:08.1934137Z",
       "MimeType":"video/mp4",
       "ContentChecksum":null
    }


### <a name="creating-hello-accesspolicy-with-write-permission"></a>Tworzenie hello AccessPolicy z uprawnieniami do zapisu
Przed przekazaniem żadnych plików do magazynu obiektów blob, należy ustawić dostępu hello zasad praw do pisania tooan zasobów. Ustaw toodo, który po toohello żądania HTTP AccessPolicies jednostki. Zdefiniuj wartość DurationInMinutes po utworzeniu lub pojawi się komunikat o błędzie 500 wewnętrzny serwer w odpowiedzi. Aby uzyskać więcej informacji o AccessPolicies, zobacz [AccessPolicy](https://docs.microsoft.com/rest/api/media/operations/accesspolicy).

powitania po przykładzie pokazano, jak toocreate AccessPolicy:

**Żądania HTTP**

    POST https://wamsbayclus001rest-hs.cloudapp.net/api/AccessPolicies HTTP/1.1
    Content-Type: application/json
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amstestaccount001&urn%3aSubscriptionId=z7f09258-2233-4ca2-b1ae-193798e2c9d8&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1421640053&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=vlG%2fPYdFDMS1zKc36qcFVWnaNh07UCkhYj3B71%2fk1YA%3d
    x-ms-version: 2.11
    Host: wamsbayclus001rest-hs.cloudapp.net
    Content-Length: 74

    {"Name":"NewUploadPolicy", "DurationInMinutes":"440", "Permissions":"2"}

**Odpowiedź HTTP**

W przypadku powodzenia powitania po odpowiedzi jest zwracany:

    HTTP/1.1 201 Created
    Cache-Control: no-cache
    Content-Length: 312
    Content-Type: application/json;odata=minimalmetadata;streaming=true;charset=utf-8
    Location: https://wamsbayclus001rest-hs.cloudapp.net/api/AccessPolicies('nb%3Apid%3AUUID%3Abe0ac48d-af7d-4877-9d60-1805d68bffae')
    Server: Microsoft-IIS/8.5
    request-id: 74c74545-7e0a-4cd6-a440-c1c48074a970
    x-ms-request-id: 74c74545-7e0a-4cd6-a440-c1c48074a970
    X-Content-Type-Options: nosniff
    DataServiceVersion: 3.0;
    X-Powered-By: ASP.NET
    Strict-Transport-Security: max-age=31536000; includeSubDomains
    Date: Sun, 18 Jan 2015 22:18:06 GMT

    {  
       "odata.metadata":"https://wamsbayclus001rest-hs.cloudapp.net/api/$metadata#AccessPolicies/@Element",
       "Id":"nb:pid:UUID:be0ac48d-af7d-4877-9d60-1805d68bffae",
       "Created":"2015-01-18T22:18:06.6370575Z",
       "LastModified":"2015-01-18T22:18:06.6370575Z",
       "Name":"NewUploadPolicy",
       "DurationInMinutes":440.0,
       "Permissions":2
    }

### <a name="get-hello-upload-url"></a>Pobierz hello przekazać adres URL

tooreceive hello przekazywania rzeczywisty adres URL, tworzenie lokalizatora SAS. Lokalizatory zdefiniuj hello czas rozpoczęcia i typ punktu końcowego połączenia dla klientów, którzy mają tooaccess plików zasobów. Można utworzyć wiele jednostek lokalizatora dla danego AccessPolicy i zasobów pary toohandle innego klienta żądań i potrzeb. Każda z tych lokalizatorów używa wartości StartTime hello plus wartość DurationInMinutes hello hello AccessPolicy toodetermine hello długość czasu, można użyć adresu URL. Aby uzyskać więcej informacji, zobacz [lokalizatora](https://docs.microsoft.com/rest/api/media/operations/locator).

Adres URL SAS ma hello następującego formatu:

    {https://myaccount.blob.core.windows.net}/{asset name}/{video file name}?{SAS signature}

Zagadnienia do rozważenia:

* Nie może mieć więcej niż pięć lokalizatorów unikatowy skojarzone z danym zawartości w tym samym czasie. Aby uzyskać więcej informacji zobacz lokalizatora.
* Tooupload plików natychmiast, należy należy ustawić Twojej StartTime wartość toofive minut przed hello bieżącego czasu. Jest to spowodowane mogą istnieć zegara pochylenia między komputer klienta i usługi Media Services. Ponadto wartość StartTime musi być w powitania po formacie daty/godziny: RRRR-MM-ddtgg (na przykład "2014-05-23T17:53:50Z").    
* Może być 30 40 sekund opóźnienia po utworzeniu lokalizatora toowhen nie jest dostępny do użycia. Ten problem dotyczy tooboth adres URL SAS oraz Lokalizatory pochodzenia.

Aby uzyskać więcej informacji na temat sygnatury dostępu Współdzielonego Zobacz lokalizatorów [to](http://southworks.com/blog/2015/05/27/reusing-azure-media-services-locators-to-avoid-facing-the-5-shared-access-policy-limitation/) blogu.

Witaj poniższy przykład pokazuje, jak toocreate lokalizatora adres URL SAS, zgodnie z definicją hello właściwości typu w treści żądania hello ("1" dla lokalizatora SAS) i "2" dla lokalizatora pochodzenia na żądanie. Witaj **ścieżki** właściwości zwróconej zawiera adres URL hello, że należy używać tooupload Twojego pliku.

**Żądania HTTP**

    POST https://wamsbayclus001rest-hs.cloudapp.net/api/Locators HTTP/1.1
    Content-Type: application/json
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amstestaccount001&urn%3aSubscriptionId=f7f09258-6753-4ca2-b1ae-193798e2c9d8&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1421640053&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=vlG%2fPYdFDMS1zKc36qcFVWnaNh07UCkhYj3B71%2fk1YA%3d
    x-ms-version: 2.11
    Host: wamsbayclus001rest-hs.cloudapp.net
    Content-Length: 178

    {  
       "AccessPolicyId":"nb:pid:UUID:be0ac48d-af7d-4877-9d60-1805d68bffae",
       "AssetId":"nb:cid:UUID:9bc8ff20-24fb-4fdb-9d7c-b04c7ee573a1",
       "StartTime":"2015-02-18T16:45:53",
       "Type":1
    }


**Odpowiedź HTTP**

W przypadku powodzenia powitania po odpowiedzi jest zwracany:

    HTTP/1.1 201 Created
    Cache-Control: no-cache
    Content-Length: 949
    Content-Type: application/json;odata=minimalmetadata;streaming=true;charset=utf-8
    Location: https://wamsbayclus001rest-hs.cloudapp.net/api/Locators('nb%3Alid%3AUUID%3Aaf57bdd8-6751-4e84-b403-f3c140444b54')
    Server: Microsoft-IIS/8.5
    request-id: 2adeb1f8-89c5-4cc8-aa4f-08cdfef33ae0
    x-ms-request-id: 2adeb1f8-89c5-4cc8-aa4f-08cdfef33ae0
    X-Content-Type-Options: nosniff
    DataServiceVersion: 3.0;
    X-Powered-By: ASP.NET
    Strict-Transport-Security: max-age=31536000; includeSubDomains
    Date: Mon, 19 Jan 2015 03:01:29 GMT

    {  
       "odata.metadata":"https://wamsbayclus001rest-hs.cloudapp.net/api/$metadata#Locators/@Element",
       "Id":"nb:lid:UUID:af57bdd8-6751-4e84-b403-f3c140444b54",
       "ExpirationDateTime":"2015-02-19T00:05:53",
       "Type":1,
       "Path":"https://storagetestaccount001.blob.core.windows.net/asset-f438649c-313c-46e2-8d68-7d2550288247?sv=2012-02-12&sr=c&si=af57bdd8-6751-4e84-b403-f3c140444b54&sig=fE4btwEfZtVQFeC0Wh3Kwks2OFPQfzl5qTMW5YytiuY%3D&st=2015-02-18T16%3A45%3A53Z&se=2015-02-19T00%3A05%3A53Z",
       "BaseUri":"https://storagetestaccount001.blob.core.windows.net/asset-f438649c-313c-46e2-8d68-7d2550288247",
       "ContentAccessComponent":"?sv=2012-02-12&sr=c&si=af57bdd8-6751-4e84-b403-f3c140444b54&sig=fE4btwEfZtVQFeC0Wh3Kwks2OFPQfzl5qTMW5YytiuY%3D&st=2015-02-18T16%3A45%3A53Z&se=2015-02-19T00%3A05%3A53Z",
       "AccessPolicyId":"nb:pid:UUID:be0ac48d-af7d-4877-9d60-1805d68bffae",
       "AssetId":"nb:cid:UUID:9bc8ff20-24fb-4fdb-9d7c-b04c7ee573a1",
       "StartTime":"2015-02-18T16:45:53",
       "Name":null
    }

### <a name="upload-a-file-into-a-blob-storage-container"></a>Przekazywanie pliku do kontenera magazynu obiektów blob
Po utworzeniu hello AccessPolicy i lokalizatora zestawu rzeczywisty plik hello jest kontenera magazynu obiektów blob platformy Azure tooan przekazane za pomocą hello interfejsów API REST magazynu Azure. Należy przekazać pliki hello jako blokowych obiektów blob. Stronicowe obiekty BLOB nie są obsługiwane przez usługi Azure Media Services.  

> [!NOTE]
> Należy dodać nazwę pliku hello pliku hello ma toohello tooupload lokalizatora **ścieżki** odebrana w poprzedniej sekcji hello wartość. Na przykład https://storagetestaccount001.blob.core.windows.net/asset-e7b02da4-5a69-40e7-a8db-e8f4f697aac0/BigBuckBunny.mp4? . . .
>
>

Aby uzyskać więcej informacji na temat pracy z obiektami blob magazynu Azure, zobacz [interfejsu API REST usługi Blob](https://docs.microsoft.com/rest/api/storageservices/Blob-Service-REST-API).

### <a name="update-hello-assetfile"></a>Aktualizacja hello AssetFile
Teraz, przekazywanego pliku, zaktualizuj hello FileAsset rozmiarze (i innych) informacje. Na przykład:

    MERGE https://wamsbayclus001rest-hs.cloudapp.net/api/Files('nb%3Acid%3AUUID%3Af13a0137-0a62-9d4c-b3b9-ca944b5142c5') HTTP/1.1
    Content-Type: application/json
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amstestaccount001&urn%3aSubscriptionId=z7f09258-2233-4ca2-b1ae-193798e2c9d8&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1421662918&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=utmoXXbm9Q7j4tW1yJuMVA3egRiQy5FPygwadkmPeaY%3d
    x-ms-version: 2.11
    Host: wamsbayclus001rest-hs.cloudapp.net

    {  
       "ContentFileSize":"1186540",
       "Id":"nb:cid:UUID:f13a0137-0a62-9d4c-b3b9-ca944b5142c5",
       "MimeType":"video/mp4",
       "Name":"BigBuckBunny.mp4",
       "ParentAssetId":"nb:cid:UUID:9bc8ff20-24fb-4fdb-9d7c-b04c7ee573a1"
    }


**Odpowiedź HTTP**

W przypadku powodzenia zwrócono hello następujące czynności:

    HTTP/1.1 204 No Content
    ...

## <a name="delete-hello-locator-and-accesspolicy"></a>Usuń hello lokalizatora i AccessPolicy
**Żądania HTTP**

    DELETE https://wamsbayclus001rest-hs.cloudapp.net/api/Locators('nb%3Alid%3AUUID%3Aaf57bdd8-6751-4e84-b403-f3c140444b54') HTTP/1.1
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amstestaccount001&urn%3aSubscriptionId=z7f09258-2233-4ca2-b1ae-193798e2c9d8&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1421662918&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=utmoXXbm9Q7j4tW1yJuMVA3egRiQy5FPygwadkmPeaY%3d
    x-ms-version: 2.11
    Host: wamsbayclus001rest-hs.cloudapp.net


**Odpowiedź HTTP**

W przypadku powodzenia zwrócono hello następujące czynności:

    HTTP/1.1 204 No Content
    ...

**Żądania HTTP**

    DELETE https://wamsbayclus001rest-hs.cloudapp.net/api/AccessPolicies('nb%3Apid%3AUUID%3Abe0ac48d-af7d-4877-9d60-1805d68bffae') HTTP/1.1
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amstestaccount001&urn%3aSubscriptionId=z7f09258-2233-4ca2-b1ae-193798e2c9d8&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1421662918&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=utmoXXbm9Q7j4tW1yJuMVA3egRiQy5FPygwadkmPeaY%3d
    x-ms-version: 2.11
    Host: wamsbayclus001rest-hs.cloudapp.net

**Odpowiedź HTTP**

W przypadku powodzenia zwrócono hello następujące czynności:

    HTTP/1.1 204 No Content
    ...

## <a id="encode"></a>Kodowanie pliku źródłowego hello do zestawu plików MP4 z adaptacyjną szybkością transmisji bitów

Po wprowadzania, które mogą być kodowane zasoby w usłudze Media Services nośnika, poddane transmultipleksacji, oznaczone znakiem wodnym i tak dalej przed przekazaniem tooclients. Te działania są zaplanowane i uruchomienia wielu tła roli wystąpień tooensure wysokiej wydajności i dostępności. Te działania są nazywane zadaniami i każde zadanie składa się z niepodzielnych zadań, które hello rzeczywistą pracę w pliku trwałego hello (Aby uzyskać więcej informacji, zobacz [zadania](/rest/api/media/services/job), [zadań](/rest/api/media/services/task) opisy).

Jak wspomniano wcześniej, podczas pracy z Azure Media Services jednym z najbardziej typowych scenariuszy hello jest dostarczanie przesyłania strumieniowego klientów tooyour adaptacyjną szybkością transmisji bitów. Usługi Media Services można dynamicznie pakietu do jednego z następujących formatów hello zestaw plików MP4 z adaptacyjną szybkością transmisji bitów: HTTP Live Streaming (HLS), Smooth Streaming, MPEG DASH.

powitania po sekcji pokazano, jak toocreate zadanie, które zawiera jeden kodowania zadań. Witaj zadanie Określa plik mezzanine hello tootranscode do zestawu z adaptacyjną szybkością transmisji bitów MP4s przy użyciu **Media Encoder Standard**. Hello sekcji przedstawiono również sposób toomonitor hello postęp zadania przetwarzania. Po zakończeniu zadania hello będzie lokalizatorów można toocreate, będącymi aktywami tooyour dostępu tooget potrzebne.

### <a name="get-a-media-processor"></a>Pobierz procesor multimediów
W usłudze Media Services procesor multimediów jest składnikiem, który obsługuje przetwarzania specyficznego dla zadania, takie jak kodowanie, Konwersja formatu zawartości multimedialnej szyfrowania lub odszyfrowywania. Dla hello kodowania zadań przedstawiona w tym samouczku zamierzamy hello toouse Media Encoder Standard.

Witaj poniższy kod identyfikatora żądania hello kodera.

**Żądania HTTP**

    GET https://wamsbayclus001rest-hs.cloudapp.net/api/MediaProcessors()?$filter=Name%20eq%20'Media%20Encoder%20Standard' HTTP/1.1
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amstestaccount001&urn%3aSubscriptionId=f7f09258-6753-4ca2-b1ae-193798e2c9d8&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1421675491&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=9hUudHYnATpi5hN3cvTfgw%2bL4N3tL0fdsRnQnm6ZYIU%3d
    x-ms-version: 2.11
    Host: wamsbayclus001rest-hs.cloudapp.net


**Odpowiedź HTTP**

    HTTP/1.1 200 OK
    Cache-Control: no-cache
    Content-Length: 273
    Content-Type: application/json;odata=minimalmetadata;streaming=true;charset=utf-8
    Server: Microsoft-IIS/8.5
    request-id: 6beb04b4-55a7-480d-8aa8-e5c5d59ffa1f
    x-ms-request-id: 6beb04b4-55a7-480d-8aa8-e5c5d59ffa1f
    X-Content-Type-Options: nosniff
    DataServiceVersion: 3.0;
    X-Powered-By: ASP.NET
    Strict-Transport-Security: max-age=31536000; includeSubDomains
    Date: Mon, 19 Jan 2015 07:54:09 GMT

    {  
       "odata.metadata":"https://wamsbayclus001rest-hs.cloudapp.net/api/$metadata#MediaProcessors",
       "value":[  
          {  
             "Id":"nb:mpid:UUID:ff4df607-d419-42f0-bc17-a481b1331e56",
             "Description":"Media Encoder Standard",
             "Name":"Media Encoder Standard",
             "Sku":"",
             "Vendor":"Microsoft",
             "Version":"1.1"
          }
       ]
    }

### <a name="create-a-job"></a>Tworzenie zadania
Każde zadanie może zawierać jeden lub więcej zadań, w zależności od typu hello przetwarzania, które mają tooaccomplish. Za pośrednictwem interfejsu API REST hello, można tworzyć zadania i ich zadania pokrewne w jeden z dwóch sposobów: zadania mogą być zdefiniowano w tekście za pośrednictwem właściwości nawigacji zadania hello na jednostkach zadania, lub przetwarzania wsadowego OData. Witaj SDK usługi Media Services używa przetwarzania wsadowego. Aby zwiększyć czytelność hello hello przykładów kodu w tym temacie, zadania są zdefiniowano w tekście. Informacje dotyczące przetwarzania wsadowego znajdują się w temacie [przetwarzanie wsadowe Open Data Protocol (OData)](http://www.odata.org/documentation/odata-version-3-0/batch-processing/).

Hello poniższy przykład przedstawia toocreate i post zadania jednego zadania konfiguracji tooencode wideo w określonej rozdzielczości i jakości. powitania po sekcji dokumentacji zawiera listę hello wszystkich hello [zadań predefiniowane](http://msdn.microsoft.com/library/mt269960) obsługiwane przez procesor Media Encoder Standard hello.  

**Żądania HTTP**

    POST https://wamsbayclus001rest-hs.cloudapp.net/api/Jobs HTTP/1.1
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Content-Type: application/json
    Accept: application/json;odata=verbose
    Accept-Charset: UTF-8
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amstestaccount001&urn%3aSubscriptionId=z7f09258-2233-4ca2-b1ae-193798e2c9d8&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1421675491&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=9hUudHYnATpi5hN3cvTfgw%2bL4N3tL0fdsRnQnm6ZYIU%3d
    x-ms-version: 2.11
    Host: wamsbayclus001rest-hs.cloudapp.net
    Content-Length: 482

    {  
       "Name":"NewTestJob",
       "InputMediaAssets":[  
          {  
             "__metadata":{  
                "uri":"https://wamsbayclus001rest-hs.net/api/Assets('nb%3Acid%3AUUID%3A9bc8ff20-24fb-4fdb-9d7c-b04c7ee573a1')"
             }
          }
       ],
       "Tasks":[  
          {  
             "Configuration":"Adaptive Streaming",
             "MediaProcessorId":"nb:mpid:UUID:ff4df607-d419-42f0-bc17-a481b1331e56",
             "TaskBody":"<?xml version=\"1.0\" encoding=\"utf-8\"?><taskBody><inputAsset>JobInputAsset(0)</inputAsset>
                <outputAsset>JobOutputAsset(0)</outputAsset></taskBody>"
          }
       ]
    }

**Odpowiedź HTTP**

W przypadku powodzenia powitania po odpowiedzi jest zwracany:

    HTTP/1.1 201 Created
    Cache-Control: no-cache
    Content-Length: 1215
    Content-Type: application/json;odata=verbose;charset=utf-8
    Location: https://wamsbayclus001rest-hs.cloudapp.net/api/Jobs('nb%3Ajid%3AUUID%3A71d2dd33-efdf-ec43-8ea1-136a110bd42c')
    Server: Microsoft-IIS/8.5
    request-id: 532ac1ec-a475-4dce-b2d5-7c8ce94ac87c
    x-ms-request-id: 532ac1ec-a475-4dce-b2d5-7c8ce94ac87c
    X-Content-Type-Options: nosniff
    DataServiceVersion: 3.0;
    X-Powered-By: ASP.NET
    Strict-Transport-Security: max-age=31536000; includeSubDomains
    Date: Mon, 19 Jan 2015 08:04:35 GMT

    {  
       "d":{  
          "__metadata":{  
             "id":"https://wamsbayclus001rest-hs.cloudapp.net/api/Jobs('nb%3Ajid%3AUUID%3A71d2dd33-efdf-ec43-8ea1-136a110bd42c')",
             "uri":"https://wamsbayclus001rest-hs.cloudapp.net/api/Jobs('nb%3Ajid%3AUUID%3A71d2dd33-efdf-ec43-8ea1-136a110bd42c')",
             "type":"Microsoft.Cloud.Media.Vod.Rest.Data.Models.Job"
          },
          "Tasks":{  
             "__deferred":{  
                "uri":"https://wamsbayclus001rest-hs.cloudapp.net/api/Jobs('nb%3Ajid%3AUUID%3A71d2dd33-efdf-ec43-8ea1-136a110bd42c')/Tasks"
             }
          },
          "OutputMediaAssets":{  
             "__deferred":{  
                "uri":"https://wamsbayclus001rest-hs.cloudapp.net/api/Jobs('nb%3Ajid%3AUUID%3A71d2dd33-efdf-ec43-8ea1-136a110bd42c')/OutputMediaAssets"
             }
          },
          "InputMediaAssets":{  
             "__deferred":{  
                "uri":"https://wamsbayclus001rest-hs.cloudapp.net/api/Jobs('nb%3Ajid%3AUUID%3A9bc8ff20-24fb-4fdb-9d7c-b04c7ee573a1')/InputMediaAssets"
             }
          },
          "Id":"nb:jid:UUID:71d2dd33-efdf-ec43-8ea1-136a110bd42c",
          "Name":"NewTestJob",
          "Created":"2015-01-19T08:04:34.3287057Z",
          "LastModified":"2015-01-19T08:04:34.3287057Z",
          "EndTime":null,
          "Priority":0,
          "RunningDuration":0,
          "StartTime":null,
          "State":0,
          "TemplateId":null,
          "JobNotificationSubscriptions":{  
             "__metadata":{  
                "type":"Collection(Microsoft.Cloud.Media.Vod.Rest.Data.Models.JobNotificationSubscription)"
             },
             "results":[  

             ]
          }
       }
    }


Istnieje kilka ważnych rzeczy toonote w dowolnym żądaniu zadania:

* Taskbody — właściwości należy użyć literału XML toodefine hello liczba danych wejściowych lub zasoby danych wyjściowych, które są używane przez hello zadań. temat zadania Hello zawiera hello definicji schematu XML dla hello XML.
* W definicji taskbody — Witaj, wartość każdego wewnętrzny <inputAsset> i <outputAsset> musi być ustawiona jako JobInputAsset(value) lub JobOutputAsset(value).
* Zadanie może mieć wielu zasobów danych wyjściowych. Jako dane wyjściowe zadania w ramach zadania jeden JobOutputAsset(x) można można użyć tylko raz.
* JobInputAsset lub JobOutputAsset można określić jako zasób wprowadzania zadania.
* Zadania musi nie tworzą cyklu.
* Parametr wartości Hello przekazujesz tooJobInputAsset lub JobOutputAsset reprezentuje hello wartość indeksu dla zasobu. Witaj rzeczywiste zasoby są definiowane w hello InputMediaAssets i OutputMediaAssets właściwości nawigacji na powitania definicji zadania jednostki.

> [!NOTE]
> Ponieważ usługi Media Services jest oparty na OData v3, hello poszczególne zasoby w InputMediaAssets i kolekcje właściwości nawigacji OutputMediaAssets są przywoływane przez "__metadata: identyfikator uri" pary nazwa wartość.
>
>

* InputMediaAssets mapuje tooone lub więcej zasobów, które zostały utworzone w usłudze Media Services. OutputMediaAssets są tworzone przez hello system. Nie odwołują się do istniejącego zasobu.
* Może być nazwany OutputMediaAssets przy użyciu atrybutu assetName hello. Jeśli ten atrybut nie jest obecny, a następnie nazwę hello hello OutputMediaAsset jest niezależnie od wartości tekst wewnętrzny hello hello <outputAsset> element jest z sufiksem hello Nazwa zadania wartość lub wartość identyfikatora zadania hello (w przypadku hello, w których właściwość Name hello nie jest zdefiniowana). Na przykład jeśli zostanie ustawiona wartość assetName zbyt "Test", a następnie hello nazwa OutputMediaAsset można ustawić właściwości zbyt "Sample". Jednak jeśli nie ustawiona wartość assetName, ale ustawiona nazwa zadania hello zbyt "NewJob", a następnie hello nazwa OutputMediaAsset się "_NewJob JobOutputAsset (wartość)".

    Witaj poniższy przykład pokazuje, jak tooset hello assetName atrybutu:

        "<?xml version=\"1.0\" encoding=\"utf-8\"?><taskBody><inputAsset>JobInputAsset(0)</inputAsset><outputAsset assetName=\"CustomOutputAssetName\">JobOutputAsset(0)</outputAsset></taskBody>"
* Tworzenie łańcuchów tooenable zadań:

  * Zadanie musi mieć co najmniej dwa zadania
  * Musi istnieć co najmniej jedno zadanie, którego danych wejściowych jest inne zadanie w zadaniu hello dane wyjściowe.

Aby uzyskać więcej informacji, zobacz [Tworzenie zadania kodowania z hello interfejsu API REST usług Media](media-services-rest-encode-asset.md).

### <a name="monitor-processing-progress"></a>Monitor przetwarzania postępu
Stan zadania hello można pobrać za pomocą właściwości stanu hello, jak pokazano w hello poniższy przykład.

**Żądania HTTP**

    GET https://wamsbayclus001rest-hs.net/api/Jobs('nb%3Ajid%3AUUID%3A71d2dd33-efdf-ec43-8ea1-136a110bd42c')/State HTTP/1.1
    Content-Type: application/json;odata=verbose
    Accept: application/json;odata=verbose
    DataServiceVersion: 3.0
    MaxDataServiceVersion: 3.0
    x-ms-version: 2.11
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=youraccountname&urn%3aSubscriptionId=zf84471d-2233-4e75-aa09-010f0fc0cf5b&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1336908022&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=RYXOraO6Z%2f7l9whWZQN%2bypeijgHwIk8XyikA01Kx1%2bk%3d
    Host: wamsbayclus001rest-hs.net
    Content-Length: 0


**Odpowiedź HTTP**

W przypadku powodzenia powitania po odpowiedzi jest zwracany:

    HTTP/1.1 200 OK
    Cache-Control: no-cache
    Content-Length: 17
    Content-Type: application/json;odata=verbose;charset=utf-8
    Server: Microsoft-IIS/7.5
    x-ms-request-id: 01324d81-18e2-4493-a3e5-c6186209f0c8
    X-Content-Type-Options: nosniff
    DataServiceVersion: 1.0;
    X-AspNet-Version: 4.0.30319
    X-Powered-By: ASP.NET
    Date: Sun, 13 May 2012 05:16:53 GMT

    {"d":{"State":2}}


### <a name="cancel-a-job"></a>Anulowanie zadania
Usługa Media Services umożliwia toocancel uruchomionych zadań za pomocą funkcji CancelJob hello. To wywołanie zwraca kod błędu 400, Jeśli spróbujesz toocancel zadania po anulowaniu jej stan, anulowanie, błąd lub zakończona.

powitania po przykładzie pokazano, jak toocall CancelJob.

**Żądania HTTP**

    GET https://wamsbayclus001rest-hs.net/API/CancelJob?jobid='nb%3ajid%3aUUID%3a71d2dd33-efdf-ec43-8ea1-136a110bd42c' HTTP/1.1
    Content-Type: application/json;odata=verbose
    Accept: application/json;odata=verbose
    DataServiceVersion: 3.0
    MaxDataServiceVersion: 3.0
    x-ms-version: 2.2
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=youraccountname&urn%3aSubscriptionId=2f84471d-b1ae-4e75-aa09-010f0fc0cf5b&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1336908753&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=kolAgnFfbQIeRv4lWxKSFa4USyjWXRm15Kd%2bNd5g8eA%3d
    Host: wamsbayclus001rest-hs.net


W przypadku powodzenia kodu 204 odpowiedź jest zwracana z treści wiadomości.

> [!NOTE]
> Należy zakodować adresu URL hello identyfikator zadania (zazwyczaj nb:jid:UUID: somevalue) podczas przekazywania go jako tooCancelJob parametru.
>
>

### <a name="get-hello-output-asset"></a>Pobierz zawartości wyjściowej hello
Witaj poniższy kod przedstawia sposób toorequest hello output zasobów identyfikatora.

**Żądania HTTP**

    GET https://wamsbayclus001rest-hs.cloudapp.net/api/Jobs('nb%3Ajid%3AUUID%3A71d2dd33-efdf-ec43-8ea1-136a110bd42c')/OutputMediaAssets() HTTP/1.1
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    User-Agent: Microsoft ADO.NET Data Services
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amstestaccount001&urn%3aSubscriptionId=z7f09258-2233-4ca2-b1ae-193798e2c9d8&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1421675491&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=9hUudHYnATpi5hN3cvTfgw%2bL4N3tL0fdsRnQnm6ZYIU%3d
    x-ms-version: 2.11
    Host: wamsbayclus001rest-hs.cloudapp.net


**Odpowiedź HTTP**

    HTTP/1.1 200 OK
    Cache-Control: no-cache
    Content-Length: 445
    Content-Type: application/json;odata=minimalmetadata;streaming=true;charset=utf-8
    Server: Microsoft-IIS/8.5
    request-id: 73cd605d-066a-46f1-8358-f4bd25a9220a
    x-ms-request-id: 73cd605d-066a-46f1-8358-f4bd25a9220a
    X-Content-Type-Options: nosniff
    DataServiceVersion: 3.0;
    X-Powered-By: ASP.NET
    Strict-Transport-Security: max-age=31536000; includeSubDomains
    Date: Mon, 19 Jan 2015 08:28:13 GMT

    {  
       "odata.metadata":"https://wamsbayclus001rest-hs.cloudapp.net/api/$metadata#Assets",
       "value":[  
          {  
             "Id":"nb:cid:UUID:71d2dd33-efdf-ec43-8ea1-136a110bd42c",
             "State":0,
             "Created":"2015-01-19T07:52:15.603",
             "LastModified":"2015-01-19T07:52:15.603",
             "AlternateId":null,
             "Name":"Multibitrate MP4s",
             "Options":0,
             "Uri":"https://storagetestaccount001.blob.core.windows.net/asset-71d2dd33-efdf-ec43-8ea1-136a110bd42c",
             "StorageAccountName":"storagetestaccount001"
          }
       ]
    }



## <a id="publish_get_urls"></a>Publikowanie zawartości hello i get przesyłania strumieniowego i pobierania progresywnego adresy URL z interfejsu API REST

toostream lub pobierania zawartości, należy najpierw należy zbyt opublikować, przez utworzenie lokalizatora. Lokalizatory zapewniają toofiles dostępu do zawartych w hello zasobów. Usługa Media Services obsługuje dwa typy lokalizatorów: OnDemandOrigin lokalizatory nośniki używane toostream (na przykład MPEG DASH, HLS lub Smooth Streaming) i lokalizatorów podpis dostępu (SAS) używane toodownload plików multimedialnych. Aby uzyskać więcej informacji na temat sygnatury dostępu Współdzielonego Zobacz lokalizatorów [to](http://southworks.com/blog/2015/05/27/reusing-azure-media-services-locators-to-avoid-facing-the-5-shared-access-policy-limitation/) blogu.

Po utworzeniu lokalizatorów hello można tworzyć adresy URL hello, które są używane toostream lub pobierania plików.

>[!NOTE]
>Po utworzeniu konta usługi AMS **domyślne** punktu końcowego przesyłania strumieniowego w brzmieniu konta tooyour hello **zatrzymane** stanu. przesyłanie strumieniowe zawartości i podejmij korzyści z dynamicznego tworzenia pakietów i dynamicznego szyfrowania toostart hello punktu końcowego przesyłania strumieniowego, z którego mają zostać toostream zawartość ma toobe w hello **systemem** stanu.

Adres URL dla protokołu Smooth Streaming ma hello następującego formatu:

    {streaming endpoint name-media services account name}.streaming.mediaservices.windows.net/{locator ID}/{filename}.ism/Manifest

Adres URL dla protokołu HLS ma hello następującego formatu:

    {streaming endpoint name-media services account name}.streaming.mediaservices.windows.net/{locator ID}/{filename}.ism/Manifest(format=m3u8-aapl)

Adres URL przesyłania strumieniowego MPEG DASH ma hello następującego formatu:

    {streaming endpoint name-media services account name}.streaming.mediaservices.windows.net/{locator ID}/{filename}.ism/Manifest(format=mpd-time-csf)


Pliki toodownload adres URL SAS używany ma hello następującego formatu:

    {blob container name}/{asset name}/{file name}/{SAS signature}

W tej sekcji przedstawiono, jak tooperform hello następujące zadania niezbędne zbyt "Publikuj" zasobów.  

* Tworzenie hello AccessPolicy z uprawnieniem do odczytu
* Tworzenie adres URL SAS dla pobierania zawartości
* Tworzenie źródłowy adres URL przesyłania strumieniowego zawartości

### <a name="creating-hello-accesspolicy-with-read-permission"></a>Tworzenie hello AccessPolicy z uprawnieniem do odczytu
Przed pobraniem lub przesyłania strumieniowego zawartości nośnika, należy najpierw zdefiniować AccessPolicy z uprawnienia do odczytu i utworzyć hello odpowiednie lokalizatora jednostki, która określa typ hello mechanizm dostarczania ma tooenable dla klientów. Aby uzyskać więcej informacji o dostępnych właściwości hello, zobacz [właściwości jednostki AccessPolicy](https://docs.microsoft.com/rest/api/media/operations/accesspolicy#accesspolicy_properties).

Witaj poniższy przykład pokazuje, jak toospecify hello AccessPolicy dla uprawnień odczytu dla danego elementu zawartości.

    POST https://wamsbayclus001rest-hs.net/API/AccessPolicies HTTP/1.1
    Content-Type: application/json
    Accept: application/json
    DataServiceVersion: 3.0
    MaxDataServiceVersion: 3.0
    x-ms-version: 2.11
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=youraccountname&urn%3aSubscriptionId=2f84471d-b1ae-4e75-aa09-010f0fc0cf5b&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1337067658&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=dithjGvlXR9HlyAf5DE99N5OCYkPAxsHIcsTSjm9%2fVE%3d
    Host: wamsbayclus001rest-hs.net
    Content-Length: 74
    Expect: 100-continue

    {"Name": "DownloadPolicy", "DurationInMinutes" : "300", "Permissions" : 1}

W przypadku powodzenia zostanie zwrócony kod 201 sukces, opisujący hello AccessPolicy jednostki, która zostanie utworzona. Następnie należy użyć hello identyfikator AccessPolicy wraz z hello identyfikator zasobu hello zawartości, który zawiera plik hello ma jednostki lokalizatora hello toocreate toodeliver (na przykład zasób dane wyjściowe).

> [!NOTE]
> Ten podstawowy przepływ pracy jest hello taki sam jak przekazywanie pliku podczas wprowadzania zasobów (zgodnie z opisem został wcześniej w tym temacie). Również takich jak przekazywanie plików, jeśli użytkownik (lub klientów) należy tooaccess plików natychmiast, należy ustawić Twojej StartTime wartość toofive minut przed hello bieżący czas. Ta akcja jest niezbędne, ponieważ może istnieć zegara pochylenia między powitania klienta i usługi Media Services. Hello wartości StartTime musi należeć do powitania po formacie daty/godziny: RRRR-MM-ddtgg (na przykład "2014-05-23T17:53:50Z").
>
>

### <a name="creating-a-sas-url-for-downloading-content"></a>Tworzenie adres URL SAS dla pobierania zawartości
Hello następującego kodu pokazuje sposób tooget adres URL, które mogą być używane toodownload plik nośnika utworzony i przekazać wcześniej. Witaj AccessPolicy zapoznał zestaw uprawnień i hello lokalizatora ścieżki odwołuje się adres URL pobierania SAS tooa.

    POST https://wamsbayclus001rest-hs.net/API/Locators HTTP/1.1
    Content-Type: application/json
    Accept: application/json
    DataServiceVersion: 3.0
    MaxDataServiceVersion: 3.0
    x-ms-version: 2.11
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=youraccountname&urn%3aSubscriptionId=zf84471d-b1ae-2233-aa09-010f0fc0cf5b&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1337067658&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=dithjGvlXR9HlyAf5DE99N5OCYkPAxsHIcsTSjm9%2fVE%3d
    Host: wamsbayclus001rest-hs.net
    Content-Length: 182
    Expect: 100-continue

    {"AccessPolicyId": "nb:pid:UUID:38c71dd0-44c5-4c5f-8418-08bb6fbf7bf8", "AssetId" : "nb:cid:UUID:71d2dd33-efdf-ec43-8ea1-136a110bd42c", "StartTime" : "2014-05-17T16:45:53", "Type":1}

W przypadku powodzenia powitania po odpowiedzi jest zwracany:

    HTTP/1.1 201 Created
    Cache-Control: no-cache
    Content-Length: 1150
    Content-Type: application/json;odata=verbose;charset=utf-8
    Location: https://wamsbayclus001rest-hs.net/api/Locators('nb%3Alid%3AUUID%3A8e5a821d-2194-4d00-8884-adf979856874')
    Server: Microsoft-IIS/7.5
    x-ms-request-id: 8cfd8556-3064-416a-97f2-67d9e35f0911
    X-Content-Type-Options: nosniff
    DataServiceVersion: 1.0;
    X-AspNet-Version: 4.0.30319
    X-Powered-By: ASP.NET
    Date: Mon, 14 May 2012 21:41:32 GMT

    {  
       "d":{  
          "__metadata":{  
             "id":"https://wamsbayclus001rest-hs.net/api/Locators('nb%3Alid%3AUUID%3A8e5a821d-2194-4d00-8884-adf979856874')",
             "uri":"https://wamsbayclus001rest-hs.net/api/Locators('nb%3Alid%3AUUID%3A8e5a821d-2194-4d00-8884-adf979856874')",
             "type":"Microsoft.Cloud.Media.Vod.Rest.Data.Models.Locator"
          },
          "AccessPolicy":{  
             "__deferred":{  
                "uri":"https://wamsbayclus001rest-hs.net/api/Locators('nb%3Alid%3AUUID%3A8e5a821d-2194-4d00-8884-adf979856874')/AccessPolicy"
             }
          },
          "Asset":{  
             "__deferred":{  
                "uri":"https://wamsbayclus001rest-hs.net/api/Locators('nb%3Alid%3AUUID%3A71d2dd33-efdf-ec43-8ea1-136a110bd42c')/Asset"
             }
          },
          "Id":"nb:lid:UUID:8e5a821d-2194-4d00-8884-adf979856874",
          "ExpirationDateTime":"\/Date(1337049393000)\/",
          "Type":1,
          "Path":"https://storagetestaccount001.blob.core.windows.net/asset-71d2dd33-efdf-ec43-8ea1-136a110bd42c?st=2012-05-14T21%3A36%3A33Z&se=2012-05-15T02%3A36%3A33Z&sr=c&si=8e5a821d-2194-4d00-8884-adf979856874&sig=y75dViDpC5V8WutrXM%2B%2FGpR3uOtqmlISiNlHU1YUBOg%3D",
          "AccessPolicyId":"nb:pid:UUID:38c71dd0-44c5-4c5f-8418-08bb6fbf7bf8",
          "AssetId":"nb:cid:UUID:71d2dd33-efdf-ec43-8ea1-136a110bd42c",
          "StartTime":"\/Date(1337031393000)\/"
       }
    }


Witaj zwrócił **ścieżki** właściwość zawiera hello adres URL SAS.

> [!NOTE]
> Czy pobierać zawartość magazynu zaszyfrowane, musisz ręcznie go odszyfrować przed renderowaniem go lub użyj hello MediaProcessor odszyfrowywania magazynu w toooutput zadań przetwarzania przetwarzane pliki w hello wyczyść tooan OutputAsset, a następnie pobrać z tego zasobu. Aby uzyskać więcej informacji na temat przetwarzania Zobacz Tworzenie zadania kodowania z hello interfejsu API REST usług Media. Ponadto nie można zaktualizować lokalizatorów adres URL SAS, po ich utworzeniu. Na przykład nie można ponownie użyć tej samej lokalizacji z zaktualizowanej wartości StartTime hello. Jest to spowodowane hello sposobu tworzenia adresów URL SAS. Chcesz tooaccess zasób do pobrania, po upływie lokalizatora, musi utworzyć nową z nowego czas rozpoczęcia.
>
>

### <a name="download-files"></a>Pobieranie plików
Po utworzeniu hello AccessPolicy i lokalizatora zestawu, możesz pobrać plików za pomocą hello interfejsów API REST magazynu Azure.  

> [!NOTE]
> Należy dodać nazwę pliku hello pliku hello ma toohello toodownload lokalizatora **ścieżki** odebrana w poprzedniej sekcji hello wartość. Na przykład https://storagetestaccount001.blob.core.windows.net/asset-e7b02da4-5a69-40e7-a8db-e8f4f697aac0/BigBuckBunny.mp4? . . .
>
>

Aby uzyskać więcej informacji na temat pracy z obiektami blob magazynu Azure, zobacz [interfejsu API REST usługi Blob](https://docs.microsoft.com/rest/api/storageservices/Blob-Service-REST-API).

W wyniku hello kodowanie zadanie, które wcześniej wykonywanej (kodowanie na zestaw MP4 z adaptacyjną) masz wiele plików MP4, które można pobrać progresywnie. Na przykład:    

    https://storagetestaccount001.blob.core.windows.net/asset-38058602-a4b8-4b33-b9f0-6880dc1490ea/BigBuckBunny_H264_650kbps_AAC_und_ch2_96kbps.mp4?sv=2012-02-12&sr=c&si=166d5154-b801-410b-a226-ee2f8eac1929&sig=P2iNZJAvAWpp%2Bj9yV6TQjoz5DIIaj7ve8ARynmEM6Xk%3D&se=2015-02-14T01:13:05Z

    https://storagetestaccount001.blob.core.windows.net/asset-38058602-a4b8-4b33-b9f0-6880dc1490ea/BigBuckBunny_H264_400kbps_AAC_und_ch2_96kbps.mp4?sv=2012-02-12&sr=c&si=166d5154-b801-410b-a226-ee2f8eac1929&sig=P2iNZJAvAWpp%2Bj9yV6TQjoz5DIIaj7ve8ARynmEM6Xk%3D&se=2015-02-14T01:13:05Z

    https://storagetestaccount001.blob.core.windows.net/asset-38058602-a4b8-4b33-b9f0-6880dc1490ea/BigBuckBunny_H264_3400kbps_AAC_und_ch2_96kbps.mp4?sv=2012-02-12&sr=c&si=166d5154-b801-410b-a226-ee2f8eac1929&sig=P2iNZJAvAWpp%2Bj9yV6TQjoz5DIIaj7ve8ARynmEM6Xk%3D&se=2015-02-14T01:13:05Z

    https://storagetestaccount001.blob.core.windows.net/asset-38058602-a4b8-4b33-b9f0-6880dc1490ea/BigBuckBunny_H264_2250kbps_AAC_und_ch2_96kbps.mp4?sv=2012-02-12&sr=c&si=166d5154-b801-410b-a226-ee2f8eac1929&sig=P2iNZJAvAWpp%2Bj9yV6TQjoz5DIIaj7ve8ARynmEM6Xk%3D&se=2015-02-14T01:13:05Z

    https://storagetestaccount001.blob.core.windows.net/asset-38058602-a4b8-4b33-b9f0-6880dc1490ea/BigBuckBunny_H264_1500kbps_AAC_und_ch2_96kbps.mp4?sv=2012-02-12&sr=c&si=166d5154-b801-410b-a226-ee2f8eac1929&sig=P2iNZJAvAWpp%2Bj9yV6TQjoz5DIIaj7ve8ARynmEM6Xk%3D&se=2015-02-14T01:13:05Z

    https://storagetestaccount001.blob.core.windows.net/asset-38058602-a4b8-4b33-b9f0-6880dc1490ea/BigBuckBunny_H264_1000kbps_AAC_und_ch2_96kbps.mp4?sv=2012-02-12&sr=c&si=166d5154-b801-410b-a226-ee2f8eac1929&sig=P2iNZJAvAWpp%2Bj9yV6TQjoz5DIIaj7ve8ARynmEM6Xk%3D&se=2015-02-14T01:13:05Z

    https://storagetestaccount001.blob.core.windows.net/asset-38058602-a4b8-4b33-b9f0-6880dc1490ea/BigBuckBunny_AAC_und_ch2_96kbps.mp4?sv=2012-02-12&sr=c&si=166d5154-b801-410b-a226-ee2f8eac1929&sig=P2iNZJAvAWpp%2Bj9yV6TQjoz5DIIaj7ve8ARynmEM6Xk%3D&se=2015-02-14T01:13:05Z

    https://storagetestaccount001.blob.core.windows.net/asset-38058602-a4b8-4b33-b9f0-6880dc1490ea/BigBuckBunny_AAC_und_ch2_56kbps.mp4?sv=2012-02-12&sr=c&si=166d5154-b801-410b-a226-ee2f8eac1929&sig=P2iNZJAvAWpp%2Bj9yV6TQjoz5DIIaj7ve8ARynmEM6Xk%3D&se=2015-02-14T01:13:05Z


### <a name="creating-a-streaming-url-for-streaming-content"></a>Tworzenie adresu URL przesyłania strumieniowego przesyłania strumieniowego zawartości
Witaj następującego kodu pokazuje sposób toocreate Lokalizator przesyłania strumieniowego adresu URL:

    POST https://wamsbayclus001rest-hs/API/Locators HTTP/1.1
    Content-Type: application/json
    Accept: application/json
    DataServiceVersion: 3.0
    MaxDataServiceVersion: 3.0
    x-ms-version: 2.11
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=youraccountname&urn%3aSubscriptionId=2f84471d-b1ae-4e75-aa09-010f0fc0cf5b&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1337067658&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=dithjGvlXR9HlyAf5DE99N5OCYkPAxsHIcsTSjm9%2fVE%3d
    Host: wamsbayclus001rest-hs
    Content-Length: 182
    Expect: 100-continue

    {"AccessPolicyId": "nb:pid:UUID:38c71dd0-44c5-4c5f-8418-08bb6fbf7bf8", "AssetId" : "nb:cid:UUID:eb5540a2-116e-4d36-b084-7e9958f7f3c3", "StartTime" : "2014-05-17T16:45:53",, "Type":2}

W przypadku powodzenia powitania po odpowiedzi jest zwracany:

    HTTP/1.1 201 Created
    Cache-Control: no-cache
    Content-Length: 981
    Content-Type: application/json;odata=verbose;charset=utf-8
    Location: https://wamsbayclus001rest-hs.net/api/Locators('nb%3Alid%3AUUID%3A52034bf6-dfae-4d83-aad3-3bd87dcb1a5d')
    Server: Microsoft-IIS/7.5
    x-ms-request-id: 2eac4158-fc78-4fa2-81ee-c9f582dc385f
    X-Content-Type-Options: nosniff
    DataServiceVersion: 1.0;
    X-AspNet-Version: 4.0.30319
    X-Powered-By: ASP.NET
    Date: Mon, 14 May 2012 21:41:39 GMT

    {  
       "d":{  
          "__metadata":{  
             "id":"https://wamsbayclus001rest-hs.net/api/Locators('nb%3Alid%3AUUID%3A52034bf6-dfae-4d83-aad3-3bd87dcb1a5d')",
             "uri":"https://wamsbayclus001rest-hs.net/api/Locators('nb%3Alid%3AUUID%3A52034bf6-dfae-4d83-aad3-3bd87dcb1a5d')",
             "type":"Microsoft.Cloud.Media.Vod.Rest.Data.Models.Locator"
          },
          "AccessPolicy":{  
             "__deferred":{  
                "uri":"https://wamsbayclus001rest-hs.net/api/Locators('nb%3Alid%3AUUID%3A52034bf6-dfae-4d83-aad3-3bd87dcb1a5d')/AccessPolicy"
             }
          },
          "Asset":{  
             "__deferred":{  
                "uri":"https://wamsbayclus001rest-hs.net/api/Locators('nb%3Alid%3AUUID%3A52034bf6-dfae-4d83-aad3-3bd87dcb1a5d')/Asset"
             }
          },
          "Id":"nb:lid:UUID:52034bf6-dfae-4d83-aad3-3bd87dcb1a5d",
          "ExpirationDateTime":"\/Date(1337049395000)\/",
          "Type":2,
          "Path":"http://wamsbayclus001rest-hs.net/52034bf6-dfae-4d83-aad3-3bd87dcb1a5d/",
          "AccessPolicyId":"nb:pid:UUID:38c71dd0-44c5-4c5f-8418-08bb6fbf7bf8",
          "AssetId":"nb:cid:UUID:eb5540a2-116e-4d36-b084-7e9958f7f3c3",
          "StartTime":"\/Date(1337031395000)\/"
       }
    }

toostream adres URL źródła Smooth Streaming w odtwarzaczu multimedialnym przesyłania strumieniowego, można dołączyć hello ścieżki właściwości o nazwie hello hello Smooth Streaming pliku, a następnie manifestu "/ manifest".

    http://amstestaccount001.streaming.mediaservices.windows.net/ebf733c4-3e2e-4a68-b67b-cc5159d1d7f2/BigBuckBunny.ism/manifest

toostream HLS, Dołącz (format = m3u8-aapl) po hello "/ manifest".

    http://amstestaccount001.streaming.mediaservices.windows.net/ebf733c4-3e2e-4a68-b67b-cc5159d1d7f2/BigBuckBunny.ism/manifest(format=m3u8-aapl)

toostream MPEG DASH, Dołącz (format = mpd-time-csf) po hello "/ manifest".

    http://amstestaccount001.streaming.mediaservices.windows.net/ebf733c4-3e2e-4a68-b67b-cc5159d1d7f2/BigBuckBunny.ism/manifest(format=mpd-time-csf)


## <a id="play"></a>Odtwarzanie zawartości
toostream wideo, możesz użyć [Azure Media Services Player](http://amsplayer.azurewebsites.net/azuremediaplayer.html).

tootest progresywnego pobierania, wklej adres URL do przeglądarki (na przykład programu Internet Explorer, Chrome, Safari).

## <a name="next-steps-media-services-learning-paths"></a>Następne kroki: ścieżki szkoleniowe dotyczące usługi Media Services
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Przekazywanie opinii
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]
