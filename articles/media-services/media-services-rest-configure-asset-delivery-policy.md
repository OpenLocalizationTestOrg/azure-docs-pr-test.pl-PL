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
# <a name="configuring-asset-delivery-policies"></a><span data-ttu-id="4d1a8-103">Konfigurowanie zasad dostarczania zasobów</span><span class="sxs-lookup"><span data-stu-id="4d1a8-103">Configuring asset delivery policies</span></span>
[!INCLUDE [media-services-selector-asset-delivery-policy](../../includes/media-services-selector-asset-delivery-policy.md)]

<span data-ttu-id="4d1a8-104">Jeśli planujesz trwałych toodeliver dynamicznie zaszyfrowany, co hello czynnościach w ramach hello zawartości dostarczania przepływu pracy jest konfigurowanie zasad dostarczania dla zasobów usługi Media Services.</span><span class="sxs-lookup"><span data-stu-id="4d1a8-104">If you plan toodeliver dynamically encrypted assets, one of hello steps in hello Media Services content delivery workflow is configuring delivery policies for assets.</span></span> <span data-ttu-id="4d1a8-105">zasady dostarczania elementu zawartości Hello informuje usługi Media Services sposób dla Twojego toobe zasobów dostarczyć: w przypadku protokołu przesyłania strumieniowego powinno zawartości dynamicznie umieszczone (na przykład, MPEG DASH, HLS, Smooth Streaming lub wszystkie), czy chcesz toodynamically szyfrowanie zawartości i w jaki sposób (koperty lub szyfrowania common encryption).</span><span class="sxs-lookup"><span data-stu-id="4d1a8-105">hello asset delivery policy tells Media Services how you want for your asset toobe delivered: into which streaming protocol should your asset be dynamically packaged (for example, MPEG DASH, HLS, Smooth Streaming, or all), whether or not you want toodynamically encrypt your asset and how (envelope or common encryption).</span></span>

<span data-ttu-id="4d1a8-106">W tym temacie omówiono dlaczego i w jaki sposób toocreate i skonfigurować zasady dostarczania zasobów.</span><span class="sxs-lookup"><span data-stu-id="4d1a8-106">This topic discusses why and how toocreate and configure asset delivery policies.</span></span>

>[!NOTE]
><span data-ttu-id="4d1a8-107">Po utworzeniu konta usługi AMS **domyślne** punktu końcowego przesyłania strumieniowego w brzmieniu konta tooyour hello **zatrzymane** stanu.</span><span class="sxs-lookup"><span data-stu-id="4d1a8-107">When your AMS account is created a **default** streaming endpoint is added tooyour account in hello **Stopped** state.</span></span> <span data-ttu-id="4d1a8-108">przesyłanie strumieniowe zawartości i podejmij korzyści z dynamicznego tworzenia pakietów i dynamicznego szyfrowania toostart hello punktu końcowego przesyłania strumieniowego, z którego mają zostać toostream zawartość ma toobe w hello **systemem** stanu.</span><span class="sxs-lookup"><span data-stu-id="4d1a8-108">toostart streaming your content and take advantage of dynamic packaging and dynamic encryption, hello streaming endpoint from which you want toostream content has toobe in hello **Running** state.</span></span> 
>
><span data-ttu-id="4d1a8-109">Ponadto toobe toouse stanie dynamicznego tworzenia pakietów i dynamicznego szyfrowania zawartości musi zawierać zestaw o adaptacyjnej szybkości bitowej MP4s lub pliki Smooth Streaming adaptacyjną szybkością transmisji bitów.</span><span class="sxs-lookup"><span data-stu-id="4d1a8-109">Also, toobe able toouse dynamic packaging and dynamic encryption your asset must contain a set of adaptive bitrate MP4s or adaptive bitrate Smooth Streaming files.</span></span>

<span data-ttu-id="4d1a8-110">Toohello różnych zasad można zastosować elementu zawartości.</span><span class="sxs-lookup"><span data-stu-id="4d1a8-110">You could apply different policies toohello same asset.</span></span> <span data-ttu-id="4d1a8-111">Na przykład można zastosować PlayReady szyfrowania tooSmooth przesyłania strumieniowego i szyfrowanie AES Envelope szyfrowania tooMPEG kreska i HLS.</span><span class="sxs-lookup"><span data-stu-id="4d1a8-111">For example, you could apply PlayReady encryption tooSmooth Streaming and AES Envelope encryption tooMPEG DASH and HLS.</span></span> <span data-ttu-id="4d1a8-112">Wszystkie protokoły, które nie są zdefiniowane w zasadzie dostarczania (na przykład dodać jedną zasadę, która tylko określa hello protokół HLS), zostanie zablokowany przesyłania strumieniowego.</span><span class="sxs-lookup"><span data-stu-id="4d1a8-112">Any protocols that are not defined in a delivery policy (for example, you add a single policy that only specifies HLS as hello protocol) will be blocked from streaming.</span></span> <span data-ttu-id="4d1a8-113">toothis wyjątek Hello jest, jeśli masz nie zdefiniowano zasad dostarczania elementów zawartości.</span><span class="sxs-lookup"><span data-stu-id="4d1a8-113">hello exception toothis is if you have no asset delivery policy defined at all.</span></span> <span data-ttu-id="4d1a8-114">Następnie wszystkie protokoły mogą być przesyłane hello Wyczyść.</span><span class="sxs-lookup"><span data-stu-id="4d1a8-114">Then, all protocols will be allowed in hello clear.</span></span>

<span data-ttu-id="4d1a8-115">Chcąc toodeliver zasób zaszyfrowanych magazynu, należy skonfigurować zasady dostarczania zasobów hello.</span><span class="sxs-lookup"><span data-stu-id="4d1a8-115">If you want toodeliver a storage encrypted asset, you must configure hello asset’s delivery policy.</span></span> <span data-ttu-id="4d1a8-116">Przed zawartości mogą być przesyłane strumieniowo, hello i przesyłania strumieniowego szyfrowania magazynu hello usuwa strumieni zawartości przy użyciu hello określone zasady dostarczania.</span><span class="sxs-lookup"><span data-stu-id="4d1a8-116">Before your asset can be streamed, hello streaming server removes hello storage encryption and streams your content using hello specified delivery policy.</span></span> <span data-ttu-id="4d1a8-117">Na przykład toodeliver zawartości zaszyfrowane za pomocą klucza szyfrowania koperty Advanced Encryption (Standard AES), Ustaw typ zasad hello zbyt**DynamicEnvelopeEncryption**.</span><span class="sxs-lookup"><span data-stu-id="4d1a8-117">For example, toodeliver your asset encrypted with Advanced Encryption Standard (AES) envelope encryption key, set hello policy type too**DynamicEnvelopeEncryption**.</span></span> <span data-ttu-id="4d1a8-118">szyfrowanie magazynu tooremove i zasobów hello strumienia w hello Wyczyść, Ustaw typ zasad hello zbyt**NoDynamicEncryption**.</span><span class="sxs-lookup"><span data-stu-id="4d1a8-118">tooremove storage encryption and stream hello asset in hello clear, set hello policy type too**NoDynamicEncryption**.</span></span> <span data-ttu-id="4d1a8-119">Przykłady, które pokazują, jak tooconfigure tych typów zasad należy wykonać.</span><span class="sxs-lookup"><span data-stu-id="4d1a8-119">Examples that show how tooconfigure these policy types follow.</span></span>

<span data-ttu-id="4d1a8-120">W zależności od konfiguracji zasad dostarczania elementów zawartości hello czy pakietu toodynamically może być dynamicznie szyfrowania i strumienia powitania po protokołów przesyłania strumieniowego: Smooth Streaming, HLS, strumieni MPEG DASH.</span><span class="sxs-lookup"><span data-stu-id="4d1a8-120">Depending on how you configure hello asset delivery policy you would be able toodynamically package, dynamically encrypt, and stream hello following streaming protocols: Smooth Streaming, HLS, MPEG DASH streams.</span></span>

<span data-ttu-id="4d1a8-121">powitania po hello pokazuje listę formatuje użycie toostream Smooth, HLS, DASH.</span><span class="sxs-lookup"><span data-stu-id="4d1a8-121">hello following list shows hello formats that you use toostream Smooth, HLS, DASH.</span></span>

<span data-ttu-id="4d1a8-122">Funkcje Smooth Streaming:</span><span class="sxs-lookup"><span data-stu-id="4d1a8-122">Smooth Streaming:</span></span>

<span data-ttu-id="4d1a8-123">{nazwa punktu końcowego przesyłania strumieniowego-nazwa konta usługi Media Services}.streaming.mediaservices.windows.net/{identyfikator lokalizatora}/{nazwa pliku}.ism/Manifest</span><span class="sxs-lookup"><span data-stu-id="4d1a8-123">{streaming endpoint name-media services account name}.streaming.mediaservices.windows.net/{locator ID}/{filename}.ism/Manifest</span></span>

<span data-ttu-id="4d1a8-124">HLS:</span><span class="sxs-lookup"><span data-stu-id="4d1a8-124">HLS:</span></span>

<span data-ttu-id="4d1a8-125">{name}.streaming.mediaservices.windows.net/{locator konta usługi media Nazwa punktu końcowego ID}/{filename}.ism/Manifest(format=m3u8-aapl) przesyłania strumieniowego</span><span class="sxs-lookup"><span data-stu-id="4d1a8-125">{streaming endpoint name-media services account name}.streaming.mediaservices.windows.net/{locator ID}/{filename}.ism/Manifest(format=m3u8-aapl)</span></span>

<span data-ttu-id="4d1a8-126">MPEG DASH</span><span class="sxs-lookup"><span data-stu-id="4d1a8-126">MPEG DASH</span></span>

<span data-ttu-id="4d1a8-127">{name}.streaming.mediaservices.windows.net/{locator konta usługi media Nazwa punktu końcowego ID}/{filename}.ism/Manifest(format=mpd-time-csf) przesyłania strumieniowego</span><span class="sxs-lookup"><span data-stu-id="4d1a8-127">{streaming endpoint name-media services account name}.streaming.mediaservices.windows.net/{locator ID}/{filename}.ism/Manifest(format=mpd-time-csf)</span></span>


<span data-ttu-id="4d1a8-128">Aby uzyskać instrukcje dotyczące sposobu toopublish zasobów i kompilacji adresu URL przesyłania strumieniowego, zobacz [zbudować adresu URL przesyłania strumieniowego](media-services-deliver-streaming-content.md).</span><span class="sxs-lookup"><span data-stu-id="4d1a8-128">For instructions on how toopublish an asset and build a streaming URL, see [Build a streaming URL](media-services-deliver-streaming-content.md).</span></span>

## <a name="considerations"></a><span data-ttu-id="4d1a8-129">Zagadnienia do rozważenia</span><span class="sxs-lookup"><span data-stu-id="4d1a8-129">Considerations</span></span>
* <span data-ttu-id="4d1a8-130">Nie można usunąć AssetDeliveryPolicy skojarzone z zasobów, gdy Lokalizator OnDemand (streaming) istnieje dla tego zasobu.</span><span class="sxs-lookup"><span data-stu-id="4d1a8-130">You cannot delete an AssetDeliveryPolicy associated with an asset while an OnDemand (streaming) locator exists for that asset.</span></span> <span data-ttu-id="4d1a8-131">zalecenie Hello jest tooremove hello zasady z zasobu hello przed usunięciem hello zasad.</span><span class="sxs-lookup"><span data-stu-id="4d1a8-131">hello recommendation is tooremove hello policy from hello asset before deleting hello policy.</span></span>
* <span data-ttu-id="4d1a8-132">Nie można utworzyć Lokalizator przesyłania strumieniowego magazynu trwałego zaszyfrowane, jeśli ustawiono nie zasad dostarczania elementów zawartości.</span><span class="sxs-lookup"><span data-stu-id="4d1a8-132">A streaming locator cannot be created on a storage encrypted asset when no asset delivery policy is set.</span></span>  <span data-ttu-id="4d1a8-133">Jeśli hello zasobów nie jest szyfrowany w magazynie, hello system umożliwi utworzyć lokalizator i strumień zasobów hello w hello wyczyść bez zasad dostarczania elementów zawartości.</span><span class="sxs-lookup"><span data-stu-id="4d1a8-133">If hello Asset isn’t storage encrypted, hello system will let you create a locator and stream hello asset in hello clear without an asset delivery policy.</span></span>
* <span data-ttu-id="4d1a8-134">Może mieć wiele zasady dostarczania zasobów skojarzonych z pojedynczego zasobu, ale można określić tylko jednokierunkowe toohandle AssetDeliveryProtocol danego.</span><span class="sxs-lookup"><span data-stu-id="4d1a8-134">You can have multiple asset delivery policies associated with a single asset but you can only specify one way toohandle a given AssetDeliveryProtocol.</span></span>  <span data-ttu-id="4d1a8-135">Co oznacza, Jeśli spróbujesz toolink dwóch dostarczania zasad określających hello AssetDeliveryProtocol.SmoothStreaming protokół, który spowoduje błąd, ponieważ hello system nie może określić, która z nich ma tooapply gdy klient przesyła żądanie Smooth Streaming.</span><span class="sxs-lookup"><span data-stu-id="4d1a8-135">Meaning if you try toolink two delivery policies that specify hello AssetDeliveryProtocol.SmoothStreaming protocol that will result in an error because hello system does not know which one you want it tooapply when a client makes a Smooth Streaming request.</span></span>
* <span data-ttu-id="4d1a8-136">Jeśli zasób z istniejących Lokalizator przesyłania strumieniowego, nie można połączyć nowych zasobów toohello zasad, Rozłącz istniejące zasady z zasobu hello lub zaktualizowania zasad dostarczania skojarzone z zasobów hello.</span><span class="sxs-lookup"><span data-stu-id="4d1a8-136">If you have an asset with an existing streaming locator, you cannot link a new policy toohello asset, unlink an existing policy from hello asset, or update a delivery policy associated with hello asset.</span></span>  <span data-ttu-id="4d1a8-137">Najpierw ma Lokalizator przesyłania strumieniowego hello tooremove, Dostosuj zasady hello i ponownie utwórz hello przesyłania strumieniowego lokalizatora.</span><span class="sxs-lookup"><span data-stu-id="4d1a8-137">You first have tooremove hello streaming locator, adjust hello policies, and then re-create hello streaming locator.</span></span>  <span data-ttu-id="4d1a8-138">Możesz użyć powitalne tego samego locatorId podczas ponownego tworzenia hello przesyłania strumieniowego lokalizatora, ale powinien zapewnić, że nie będzie powodować problemy dla klientów, ponieważ zawartości mogą być buforowane pochodzenia hello lub podrzędne CDN.</span><span class="sxs-lookup"><span data-stu-id="4d1a8-138">You can use hello same locatorId when you recreate hello streaming locator but you should ensure that won’t cause issues for clients since content can be cached by hello origin or a downstream CDN.</span></span>

>[!NOTE]

><span data-ttu-id="4d1a8-139">Podczas uzyskiwania dostępu do obiektów w usłudze Media Services, należy ustawić określonych pól nagłówka i wartości w Twoich żądań HTTP.</span><span class="sxs-lookup"><span data-stu-id="4d1a8-139">When accessing entities in Media Services, you must set specific header fields and values in your HTTP requests.</span></span> <span data-ttu-id="4d1a8-140">Aby uzyskać więcej informacji, zobacz [ustawień dla rozwoju interfejsu API REST usługi Media](media-services-rest-how-to-use.md).</span><span class="sxs-lookup"><span data-stu-id="4d1a8-140">For more information, see [Setup for Media Services REST API Development](media-services-rest-how-to-use.md).</span></span>

## <a name="connect-toomedia-services"></a><span data-ttu-id="4d1a8-141">Połączenie usług tooMedia</span><span class="sxs-lookup"><span data-stu-id="4d1a8-141">Connect tooMedia Services</span></span>

<span data-ttu-id="4d1a8-142">Aby uzyskać informacje dotyczące tooconnect toohello AMS interfejsu API, zobacz temat [hello dostępu do interfejsu API usługi Azure Media Services przy użyciu uwierzytelniania usługi Azure AD](media-services-use-aad-auth-to-access-ams-api.md).</span><span class="sxs-lookup"><span data-stu-id="4d1a8-142">For information on how tooconnect toohello AMS API, see [Access hello Azure Media Services API with Azure AD authentication](media-services-use-aad-auth-to-access-ams-api.md).</span></span> 

>[!NOTE]
><span data-ttu-id="4d1a8-143">Po pomyślnym połączeniu toohttps://media.windows.net, otrzymasz 301 przekierowanie, określając inny identyfikator URI usługi multimediów.</span><span class="sxs-lookup"><span data-stu-id="4d1a8-143">After successfully connecting toohttps://media.windows.net, you will receive a 301 redirect specifying another Media Services URI.</span></span> <span data-ttu-id="4d1a8-144">Należy wykonać kolejne wywołania toohello nowy identyfikator URI.</span><span class="sxs-lookup"><span data-stu-id="4d1a8-144">You must make subsequent calls toohello new URI.</span></span>

## <a name="clear-asset-delivery-policy"></a><span data-ttu-id="4d1a8-145">Zasady dostarczania elementu zawartości wyczyść</span><span class="sxs-lookup"><span data-stu-id="4d1a8-145">Clear asset delivery policy</span></span>
### <span data-ttu-id="4d1a8-146"><a id="create_asset_delivery_policy"></a>Tworzenie zasad dostarczania elementów zawartości</span><span class="sxs-lookup"><span data-stu-id="4d1a8-146"><a id="create_asset_delivery_policy"></a>Create asset delivery policy</span></span>
<span data-ttu-id="4d1a8-147">Witaj następujące żądania HTTP tworzy zasady dostarczania elementu zawartości, określająca toonot Zastosuj dynamicznego szyfrowania i protokoły toodeliver hello strumienia w jednym z następujących hello: MPEG DASH, HLS i Smooth Streaming protokołów.</span><span class="sxs-lookup"><span data-stu-id="4d1a8-147">hello following HTTP request creates an asset delivery policy that specifies toonot apply dynamic encryption and toodeliver hello stream in any of hello following protocols:  MPEG DASH, HLS, and Smooth Streaming protocols.</span></span> 

<span data-ttu-id="4d1a8-148">Informacje o jakie wartości można określić podczas tworzenia AssetDeliveryPolicy, zobacz hello [typów używanych podczas definiowania AssetDeliveryPolicy](#types) sekcji.</span><span class="sxs-lookup"><span data-stu-id="4d1a8-148">For information on what values you can specify when creating an AssetDeliveryPolicy, see hello [Types used when defining AssetDeliveryPolicy](#types) section.</span></span>   

<span data-ttu-id="4d1a8-149">Żądanie:</span><span class="sxs-lookup"><span data-stu-id="4d1a8-149">Request:</span></span>

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

<span data-ttu-id="4d1a8-150">Odpowiedź:</span><span class="sxs-lookup"><span data-stu-id="4d1a8-150">Response:</span></span>

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

### <span data-ttu-id="4d1a8-151"><a id="link_asset_with_asset_delivery_policy"></a>Łącze zasobów z zasad dostarczania elementów zawartości</span><span class="sxs-lookup"><span data-stu-id="4d1a8-151"><a id="link_asset_with_asset_delivery_policy"></a>Link asset with asset delivery policy</span></span>
<span data-ttu-id="4d1a8-152">powitania po hello łącza żądania HTTP określone zasady dostarczania elementu zawartości toohello zasobów do.</span><span class="sxs-lookup"><span data-stu-id="4d1a8-152">hello following HTTP request links hello specified asset toohello asset delivery policy to.</span></span>

<span data-ttu-id="4d1a8-153">Żądanie:</span><span class="sxs-lookup"><span data-stu-id="4d1a8-153">Request:</span></span>

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

<span data-ttu-id="4d1a8-154">Odpowiedź:</span><span class="sxs-lookup"><span data-stu-id="4d1a8-154">Response:</span></span>

    HTTP/1.1 204 No Content


## <a name="dynamicenvelopeencryption-asset-delivery-policy"></a><span data-ttu-id="4d1a8-155">Zasady dostarczania elementu zawartości DynamicEnvelopeEncryption</span><span class="sxs-lookup"><span data-stu-id="4d1a8-155">DynamicEnvelopeEncryption asset delivery policy</span></span>
### <a name="create-content-key-of-hello-envelopeencryption-type-and-link-it-toohello-asset"></a><span data-ttu-id="4d1a8-156">Utwórz klucz zawartości typu EnvelopeEncryption hello i połącz go toohello zasobów</span><span class="sxs-lookup"><span data-stu-id="4d1a8-156">Create content key of hello EnvelopeEncryption type and link it toohello asset</span></span>
<span data-ttu-id="4d1a8-157">Podczas określania zasad dostarczania DynamicEnvelopeEncryption, należy się toolink toomake klucz zawartości zasobów tooa z hello EnvelopeEncryption typu.</span><span class="sxs-lookup"><span data-stu-id="4d1a8-157">When specifying DynamicEnvelopeEncryption delivery policy, you need toomake sure toolink your asset tooa content key of hello EnvelopeEncryption type.</span></span> <span data-ttu-id="4d1a8-158">Aby uzyskać więcej informacji, zobacz: [Tworzenie klucza zawartości](media-services-rest-create-contentkey.md)).</span><span class="sxs-lookup"><span data-stu-id="4d1a8-158">For more information, see: [Creating a content key](media-services-rest-create-contentkey.md)).</span></span>

### <span data-ttu-id="4d1a8-159"><a id="get_delivery_url"></a>Pobieranie adresu URL dostarczania</span><span class="sxs-lookup"><span data-stu-id="4d1a8-159"><a id="get_delivery_url"></a>Get delivery URL</span></span>
<span data-ttu-id="4d1a8-160">Get hello dostarczania adres URL hello określona metoda dostarczania hello klucza zawartości utworzony w poprzednim kroku hello.</span><span class="sxs-lookup"><span data-stu-id="4d1a8-160">Get hello delivery URL for hello specified delivery method of hello content key created in hello previous step.</span></span> <span data-ttu-id="4d1a8-161">Klient używa hello toorequest adresu URL zwróciła klucza AES lub licencji PlayReady w kolejności tooplayback hello chronionej zawartości.</span><span class="sxs-lookup"><span data-stu-id="4d1a8-161">A client uses hello returned URL toorequest an AES key or a PlayReady license in order tooplayback hello protected content.</span></span>

<span data-ttu-id="4d1a8-162">Określ typ hello hello tooget adres URL w treści żądania HTTP hello hello.</span><span class="sxs-lookup"><span data-stu-id="4d1a8-162">Specify hello type of hello URL tooget in hello body of hello HTTP request.</span></span> <span data-ttu-id="4d1a8-163">W przypadku ochrony zawartości przy użyciu usługi PlayReady, żądanie adresu URL pozyskiwania licencji PlayReady usług nośnika przy użyciu 1 dla hello keyDeliveryType: {"keyDeliveryType": 1}.</span><span class="sxs-lookup"><span data-stu-id="4d1a8-163">If you are protecting your content with PlayReady, request a Media Services PlayReady license acquisition URL, using 1 for hello keyDeliveryType: {"keyDeliveryType":1}.</span></span> <span data-ttu-id="4d1a8-164">W przypadku ochrony zawartości przy użyciu szyfrowania koperty hello żądanie adresu URL pozyskiwania kluczy, określając 2 dla keyDeliveryType: {"keyDeliveryType": 2}.</span><span class="sxs-lookup"><span data-stu-id="4d1a8-164">If you are protecting your content with hello envelope encryption, request a key acquisition URL by specifying 2 for keyDeliveryType: {"keyDeliveryType":2}.</span></span>

<span data-ttu-id="4d1a8-165">Żądanie:</span><span class="sxs-lookup"><span data-stu-id="4d1a8-165">Request:</span></span>

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

<span data-ttu-id="4d1a8-166">Odpowiedź:</span><span class="sxs-lookup"><span data-stu-id="4d1a8-166">Response:</span></span>

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


### <a name="create-asset-delivery-policy"></a><span data-ttu-id="4d1a8-167">Tworzenie zasad dostarczania elementów zawartości</span><span class="sxs-lookup"><span data-stu-id="4d1a8-167">Create asset delivery policy</span></span>
<span data-ttu-id="4d1a8-168">Witaj następujące żądania HTTP tworzy hello **AssetDeliveryPolicy** będący szyfrowania dynamicznego koperty tooapply skonfigurowany (**DynamicEnvelopeEncryption**) toohello **HLS**protokołu (w tym przykładzie innych protokołów będzie blokowany przesyłania strumieniowego).</span><span class="sxs-lookup"><span data-stu-id="4d1a8-168">hello following HTTP request creates hello **AssetDeliveryPolicy** that is configured tooapply dynamic envelope encryption (**DynamicEnvelopeEncryption**) toohello **HLS** protocol (in this example, other protocols will be blocked from streaming).</span></span> 

<span data-ttu-id="4d1a8-169">Informacje o jakie wartości można określić podczas tworzenia AssetDeliveryPolicy, zobacz hello [typów używanych podczas definiowania AssetDeliveryPolicy](#types) sekcji.</span><span class="sxs-lookup"><span data-stu-id="4d1a8-169">For information on what values you can specify when creating an AssetDeliveryPolicy, see hello [Types used when defining AssetDeliveryPolicy](#types) section.</span></span>   

<span data-ttu-id="4d1a8-170">Żądanie:</span><span class="sxs-lookup"><span data-stu-id="4d1a8-170">Request:</span></span>

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


<span data-ttu-id="4d1a8-171">Odpowiedź:</span><span class="sxs-lookup"><span data-stu-id="4d1a8-171">Response:</span></span>

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


### <a name="link-asset-with-asset-delivery-policy"></a><span data-ttu-id="4d1a8-172">Łącze zasobów z zasad dostarczania elementów zawartości</span><span class="sxs-lookup"><span data-stu-id="4d1a8-172">Link asset with asset delivery policy</span></span>
<span data-ttu-id="4d1a8-173">Zobacz [zasobów łącza z zasad dostarczania elementów zawartości](#link_asset_with_asset_delivery_policy)</span><span class="sxs-lookup"><span data-stu-id="4d1a8-173">See [Link asset with asset delivery policy](#link_asset_with_asset_delivery_policy)</span></span>

## <a name="dynamiccommonencryption-asset-delivery-policy"></a><span data-ttu-id="4d1a8-174">Zasady dostarczania elementu zawartości DynamicCommonEncryption</span><span class="sxs-lookup"><span data-stu-id="4d1a8-174">DynamicCommonEncryption asset delivery policy</span></span>
### <a name="create-content-key-of-hello-commonencryption-type-and-link-it-toohello-asset"></a><span data-ttu-id="4d1a8-175">Utwórz klucz zawartości typu CommonEncryption hello i połącz go toohello zasobów</span><span class="sxs-lookup"><span data-stu-id="4d1a8-175">Create content key of hello CommonEncryption type and link it toohello asset</span></span>
<span data-ttu-id="4d1a8-176">Podczas określania zasad dostarczania DynamicCommonEncryption, należy się toolink toomake klucz zawartości zasobów tooa z hello CommonEncryption typu.</span><span class="sxs-lookup"><span data-stu-id="4d1a8-176">When specifying DynamicCommonEncryption delivery policy, you need toomake sure toolink your asset tooa content key of hello CommonEncryption type.</span></span> <span data-ttu-id="4d1a8-177">Aby uzyskać więcej informacji, zobacz: [Tworzenie klucza zawartości](media-services-rest-create-contentkey.md)).</span><span class="sxs-lookup"><span data-stu-id="4d1a8-177">For more information, see: [Creating a content key](media-services-rest-create-contentkey.md)).</span></span>

### <a name="get-delivery-url"></a><span data-ttu-id="4d1a8-178">Pobieranie adresu URL dostarczania</span><span class="sxs-lookup"><span data-stu-id="4d1a8-178">Get Delivery URL</span></span>
<span data-ttu-id="4d1a8-179">Pobierz adres URL dostarczania hello metoda dostarczania PlayReady hello hello klucza zawartości utworzony w poprzednim kroku hello.</span><span class="sxs-lookup"><span data-stu-id="4d1a8-179">Get hello delivery URL for hello PlayReady delivery method of hello content key created in hello previous step.</span></span> <span data-ttu-id="4d1a8-180">Klient używa hello zwrócił toorequest adres URL licencji PlayReady w kolejności tooplayback hello chronione zawartości.</span><span class="sxs-lookup"><span data-stu-id="4d1a8-180">A client uses hello returned URL toorequest a PlayReady license in order tooplayback hello protected content.</span></span> <span data-ttu-id="4d1a8-181">Aby uzyskać więcej informacji, zobacz [uzyskać adres URL dostarczania](#get_delivery_url).</span><span class="sxs-lookup"><span data-stu-id="4d1a8-181">For more information, see [Get Delivery URL](#get_delivery_url).</span></span>

### <a name="create-asset-delivery-policy"></a><span data-ttu-id="4d1a8-182">Tworzenie zasad dostarczania elementów zawartości</span><span class="sxs-lookup"><span data-stu-id="4d1a8-182">Create asset delivery policy</span></span>
<span data-ttu-id="4d1a8-183">Witaj następujące żądania HTTP tworzy hello **AssetDeliveryPolicy** który jest skonfigurowany tooapply dynamicznego szyfrowania common encryption (**DynamicCommonEncryption**) toohello **Smooth Streaming**  protokołu (w tym przykładzie innych protokołów będzie blokowany przesyłania strumieniowego).</span><span class="sxs-lookup"><span data-stu-id="4d1a8-183">hello following HTTP request creates hello **AssetDeliveryPolicy** that is configured tooapply dynamic common encryption (**DynamicCommonEncryption**) toohello **Smooth Streaming** protocol (in this example, other protocols will be blocked from streaming).</span></span> 

<span data-ttu-id="4d1a8-184">Informacje o jakie wartości można określić podczas tworzenia AssetDeliveryPolicy, zobacz hello [typów używanych podczas definiowania AssetDeliveryPolicy](#types) sekcji.</span><span class="sxs-lookup"><span data-stu-id="4d1a8-184">For information on what values you can specify when creating an AssetDeliveryPolicy, see hello [Types used when defining AssetDeliveryPolicy](#types) section.</span></span>   

<span data-ttu-id="4d1a8-185">Żądanie:</span><span class="sxs-lookup"><span data-stu-id="4d1a8-185">Request:</span></span>

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


<span data-ttu-id="4d1a8-186">Jeśli chcesz tooprotect zawartości przy użyciu Widevine DRM, zaktualizuj hello AssetDeliveryConfiguration wartości toouse WidevineLicenseAcquisitionUrl (który ma wartość hello 7) i określ hello adres URL usługi dostarczania licencji.</span><span class="sxs-lookup"><span data-stu-id="4d1a8-186">If you want tooprotect your content using Widevine DRM, update hello AssetDeliveryConfiguration values toouse WidevineLicenseAcquisitionUrl (which has hello value of 7) and specify hello URL of a license delivery service.</span></span> <span data-ttu-id="4d1a8-187">Można użyć powitania po dostarczania licencji Widevine toohelp partnerów AMS: [Axinom](http://www.axinom.com/press/ibc-axinom-drm-6/), [EZDRM](http://ezdrm.com/), [castLabs](http://castlabs.com/company/partners/azure/).</span><span class="sxs-lookup"><span data-stu-id="4d1a8-187">You can use hello following AMS partners toohelp you deliver Widevine licenses: [Axinom](http://www.axinom.com/press/ibc-axinom-drm-6/), [EZDRM](http://ezdrm.com/), [castLabs](http://castlabs.com/company/partners/azure/).</span></span>

<span data-ttu-id="4d1a8-188">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="4d1a8-188">For example:</span></span> 

    {"Name":"AssetDeliveryPolicy","AssetDeliveryProtocol":2,"AssetDeliveryPolicyType":4,"AssetDeliveryConfiguration":"[{\"Key\":7,\"Value\":\"https:\\/\\/example.net\/WidevineLicenseAcquisition\/"}]"}

> [!NOTE]
> <span data-ttu-id="4d1a8-189">W przypadku szyfrowania przy użyciu metody Widevine, tylko będzie możliwe toodeliver przy użyciu kreska.</span><span class="sxs-lookup"><span data-stu-id="4d1a8-189">When encrypting with Widevine, you would only be able toodeliver using DASH.</span></span> <span data-ttu-id="4d1a8-190">Upewnij się, że Protokół dostarczania elementów zawartości (2) w hello toospecify KRESKI.</span><span class="sxs-lookup"><span data-stu-id="4d1a8-190">Make sure toospecify DASH (2) in hello asset delivery protocol.</span></span>
> 
> 

### <a name="link-asset-with-asset-delivery-policy"></a><span data-ttu-id="4d1a8-191">Łącze zasobów z zasad dostarczania elementów zawartości</span><span class="sxs-lookup"><span data-stu-id="4d1a8-191">Link asset with asset delivery policy</span></span>
<span data-ttu-id="4d1a8-192">Zobacz [zasobów łącza z zasad dostarczania elementów zawartości](#link_asset_with_asset_delivery_policy)</span><span class="sxs-lookup"><span data-stu-id="4d1a8-192">See [Link asset with asset delivery policy](#link_asset_with_asset_delivery_policy)</span></span>

## <span data-ttu-id="4d1a8-193"><a id="types"></a>Typy używane podczas definiowania AssetDeliveryPolicy</span><span class="sxs-lookup"><span data-stu-id="4d1a8-193"><a id="types"></a>Types used when defining AssetDeliveryPolicy</span></span>

### <a name="assetdeliveryprotocol"></a><span data-ttu-id="4d1a8-194">AssetDeliveryProtocol</span><span class="sxs-lookup"><span data-stu-id="4d1a8-194">AssetDeliveryProtocol</span></span>

<span data-ttu-id="4d1a8-195">Witaj następujące wyliczenia opisano wartości ustawione przez protokół dostarczania elementów zawartości hello.</span><span class="sxs-lookup"><span data-stu-id="4d1a8-195">hello following enum describes values you can set for hello asset delivery protocol.</span></span>

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

### <a name="assetdeliverypolicytype"></a><span data-ttu-id="4d1a8-196">AssetDeliveryPolicyType</span><span class="sxs-lookup"><span data-stu-id="4d1a8-196">AssetDeliveryPolicyType</span></span>

<span data-ttu-id="4d1a8-197">Witaj następujące wyliczenia opisano wartości, które można ustawić dla typu zasady dostarczania elementu zawartości hello.</span><span class="sxs-lookup"><span data-stu-id="4d1a8-197">hello following enum describes values you can set for hello asset delivery policy type.</span></span>  

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

### <a name="contentkeydeliverytype"></a><span data-ttu-id="4d1a8-198">ContentKeyDeliveryType</span><span class="sxs-lookup"><span data-stu-id="4d1a8-198">ContentKeyDeliveryType</span></span>

<span data-ttu-id="4d1a8-199">Witaj następujące wyliczenia opisano wartości można użyć metody dostarczania hello tooconfigure powitania klienta toohello klucza zawartości.</span><span class="sxs-lookup"><span data-stu-id="4d1a8-199">hello following enum describes values you can use tooconfigure hello delivery method of hello content key toohello client.</span></span>
    
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


### <a name="assetdeliverypolicyconfigurationkey"></a><span data-ttu-id="4d1a8-200">AssetDeliveryPolicyConfigurationKey</span><span class="sxs-lookup"><span data-stu-id="4d1a8-200">AssetDeliveryPolicyConfigurationKey</span></span>

<span data-ttu-id="4d1a8-201">powitania po wyliczenia opisano wartości, które można ustawić określonej konfiguracji tooget tooconfigure klucze używane dla zasad dostarczania elementów zawartości.</span><span class="sxs-lookup"><span data-stu-id="4d1a8-201">hello following enum describes values you can set tooconfigure keys used tooget specific configuration for an asset delivery policy.</span></span>

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

## <a name="media-services-learning-paths"></a><span data-ttu-id="4d1a8-202">Ścieżki szkoleniowe dotyczące usługi Media Services</span><span class="sxs-lookup"><span data-stu-id="4d1a8-202">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="4d1a8-203">Przekazywanie opinii</span><span class="sxs-lookup"><span data-stu-id="4d1a8-203">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

