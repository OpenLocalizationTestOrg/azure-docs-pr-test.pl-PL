---
title: "zasady autoryzacji klucza zawartości aaaConfigure z REST - Azure | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak tooconfigure zasady autoryzacji klucza zawartości przy użyciu interfejsu API REST usługi multimediów."
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: 7af5f9e2-8ed8-43f2-843b-580ce8759fd4
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/31/2017
ms.author: juliako
ms.openlocfilehash: c058b7682bcbfb736faba18ec7fce33f2f2acb49
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="dynamic-encryption-configure-content-key-authorization-policy"></a><span data-ttu-id="01463-103">Szyfrowania dynamicznego: Skonfiguruj zasady autoryzacji klucza zawartości</span><span class="sxs-lookup"><span data-stu-id="01463-103">Dynamic encryption: Configure Content Key Authorization Policy</span></span>
[!INCLUDE [media-services-selector-content-key-auth-policy](../../includes/media-services-selector-content-key-auth-policy.md)]

## <a name="overview"></a><span data-ttu-id="01463-104">Omówienie</span><span class="sxs-lookup"><span data-stu-id="01463-104">Overview</span></span>
<span data-ttu-id="01463-105">Microsoft Azure Media Services umożliwia toodeliver możesz zawartości (dynamicznie) szyfrowany za pomocą Standard AES (Advanced Encryption) (przy użyciu kluczy szyfrowania 128-bitowe) i PlayReady lub Widevine DRM.</span><span class="sxs-lookup"><span data-stu-id="01463-105">Microsoft Azure Media Services enables you toodeliver your content encrypted (dynamically) with Advanced Encryption Standard (AES) (using 128-bit encryption keys) and PlayReady or Widevine DRM.</span></span> <span data-ttu-id="01463-106">Usługi Media Services udostępnia usługę dostarczania kluczy i licencje PlayReady/Widevine tooauthorized klientów.</span><span class="sxs-lookup"><span data-stu-id="01463-106">Media Services also provides a service for delivering keys and PlayReady/Widevine licenses tooauthorized clients.</span></span>

<span data-ttu-id="01463-107">Jeśli chcesz dla usługi Media Services tooencrypt zasób, należy tooassociate klucza szyfrowania (**CommonEncryption** lub **EnvelopeEncryption**) z zasobów hello (zgodnie z opisem [tutaj](media-services-rest-create-contentkey.md)) a także skonfigurować zasady autoryzacji klucza hello (zgodnie z opisem w tym artykule).</span><span class="sxs-lookup"><span data-stu-id="01463-107">If you want for Media Services tooencrypt an asset, you need tooassociate an encryption key (**CommonEncryption** or **EnvelopeEncryption**) with hello asset (as described [here](media-services-rest-create-contentkey.md)) and also configure authorization policies for hello key (as described in this article).</span></span>

<span data-ttu-id="01463-108">Gdy odtwarzacza zażąda strumienia, usługa Media Services używa hello określony toodynamically klucza szyfrowania przy użyciu szyfrowania AES lub PlayReady zawartości.</span><span class="sxs-lookup"><span data-stu-id="01463-108">When a stream is requested by a player, Media Services uses hello specified key toodynamically encrypt your content using AES or PlayReady encryption.</span></span> <span data-ttu-id="01463-109">toodecrypt hello strumienia, hello odtwarzacza zażąda hello klucza z usługi dostarczania klucza hello.</span><span class="sxs-lookup"><span data-stu-id="01463-109">toodecrypt hello stream, hello player will request hello key from hello key delivery service.</span></span> <span data-ttu-id="01463-110">toodecide czy hello użytkownik jest autoryzowany tooget hello klucza, usługi hello ocenia zasady autoryzacji hello określonych hello klucza.</span><span class="sxs-lookup"><span data-stu-id="01463-110">toodecide whether or not hello user is authorized tooget hello key, hello service evaluates hello authorization policies that you specified for hello key.</span></span>

<span data-ttu-id="01463-111">Usługa Media Services obsługuje wiele sposobów uwierzytelniania użytkowników, którzy tworzą żądania klucza.</span><span class="sxs-lookup"><span data-stu-id="01463-111">Media Services supports multiple ways of authenticating users who make key requests.</span></span> <span data-ttu-id="01463-112">Witaj zasady autoryzacji klucza zawartości może mieć jeden lub więcej ograniczeń: **Otwórz** lub **tokenu** ograniczeń.</span><span class="sxs-lookup"><span data-stu-id="01463-112">hello content key authorization policy could have one or more authorization restrictions: **open** or **token** restriction.</span></span> <span data-ttu-id="01463-113">Witaj zasadzie ograniczenia tokenu musi towarzyszyć token wystawiony przez Secure Token Service (STS).</span><span class="sxs-lookup"><span data-stu-id="01463-113">hello token restricted policy must be accompanied by a token issued by a Secure Token Service (STS).</span></span> <span data-ttu-id="01463-114">Usługa Media Services obsługuje tokenów w hello **proste tokenów sieci Web** ([SWT](https://msdn.microsoft.com/library/gg185950.aspx#BKMK_2)) format i ** formatu JSON Web Token **(JWT).</span><span class="sxs-lookup"><span data-stu-id="01463-114">Media Services supports tokens in hello **Simple Web Tokens** ([SWT](https://msdn.microsoft.com/library/gg185950.aspx#BKMK_2)) format and **JSON Web Token **(JWT) format.</span></span>

<span data-ttu-id="01463-115">Usługi Media Services nie zapewnia bezpieczny tokenu usługi.</span><span class="sxs-lookup"><span data-stu-id="01463-115">Media Services does not provide Secure Token Services.</span></span> <span data-ttu-id="01463-116">Można utworzyć niestandardowy STS lub korzystać z usługi Microsoft Azure ACS tooissue tokenów.</span><span class="sxs-lookup"><span data-stu-id="01463-116">You can create a custom STS or leverage Microsoft Azure ACS tooissue tokens.</span></span> <span data-ttu-id="01463-117">Witaj STS musi być skonfigurowany toocreate podpisany token z określonym kluczem hello i wystawiających oświadczenia, określona w konfiguracji ograniczenia tokenu hello (zgodnie z opisem w tym artykule).</span><span class="sxs-lookup"><span data-stu-id="01463-117">hello STS must be configured toocreate a token signed with hello specified key and issue claims that you specified in hello token restriction configuration (as described in this article).</span></span> <span data-ttu-id="01463-118">Witaj usługa Media Services klucza dostawy zwróci klienta toohello klucza szyfrowania hello Jeśli hello token jest prawidłowy i hello oświadczenia w tokenie hello pasują hello klucza zawartości.</span><span class="sxs-lookup"><span data-stu-id="01463-118">hello Media Services key delivery service will return hello encryption key toohello client if hello token is valid and hello claims in hello token match those configured for hello content key.</span></span>

<span data-ttu-id="01463-119">Aby uzyskać więcej informacji, zobacz</span><span class="sxs-lookup"><span data-stu-id="01463-119">For more information, see</span></span>

[<span data-ttu-id="01463-120">Uwierzytelniania tokenu JWT</span><span class="sxs-lookup"><span data-stu-id="01463-120">JWT token authentication</span></span>](http://www.gtrifonov.com/2015/01/03/jwt-token-authentication-in-azure-media-services-and-dynamic-encryption/)

<span data-ttu-id="01463-121">[Integracja aplikacji na podstawie Azure Media Services OWIN MVC z usługi Azure Active Directory i ograniczenie klucza dostarczania zawartości na podstawie oświadczeń JWT](http://www.gtrifonov.com/2015/01/24/mvc-owin-azure-media-services-ad-integration/).</span><span class="sxs-lookup"><span data-stu-id="01463-121">[Integrate Azure Media Services OWIN MVC based app with Azure Active Directory and restrict content key delivery based on JWT claims](http://www.gtrifonov.com/2015/01/24/mvc-owin-azure-media-services-ad-integration/).</span></span>

<span data-ttu-id="01463-122">[Używaj tokenów tooissue Azure ACS](http://mingfeiy.com/acs-with-key-services).</span><span class="sxs-lookup"><span data-stu-id="01463-122">[Use Azure ACS tooissue tokens](http://mingfeiy.com/acs-with-key-services).</span></span>

### <a name="some-considerations-apply"></a><span data-ttu-id="01463-123">Zagadnienia do rozważenia:</span><span class="sxs-lookup"><span data-stu-id="01463-123">Some considerations apply:</span></span>
* <span data-ttu-id="01463-124">toobe toouse stanie dynamicznego tworzenia pakietów i dynamicznego szyfrowania, upewnij się hello punktu końcowego przesyłania strumieniowego z którego mają zostać toostream zawartości jest hello **systemem** stanu.</span><span class="sxs-lookup"><span data-stu-id="01463-124">toobe able toouse dynamic packaging and dynamic encryption, make sure hello streaming endpoint from which you want toostream  your content is in hello **Running** state.</span></span>
* <span data-ttu-id="01463-125">Zawartości musi zawierać zestaw o adaptacyjnej szybkości bitowej MP4s lub pliki Smooth Streaming adaptacyjną szybkością transmisji bitów.</span><span class="sxs-lookup"><span data-stu-id="01463-125">Your asset must contain a set of adaptive bitrate MP4s or  adaptive bitrate Smooth Streaming files.</span></span> <span data-ttu-id="01463-126">Aby uzyskać więcej informacji, zobacz [kodowanie elementu zawartości](media-services-encode-asset.md).</span><span class="sxs-lookup"><span data-stu-id="01463-126">For more information, see [Encode an asset](media-services-encode-asset.md).</span></span>
* <span data-ttu-id="01463-127">Przekazywanie i zasobów przy użyciu kodowania **AssetCreationOptions.StorageEncrypted** opcji.</span><span class="sxs-lookup"><span data-stu-id="01463-127">Upload and encode your assets using **AssetCreationOptions.StorageEncrypted** option.</span></span>
* <span data-ttu-id="01463-128">Jeśli planujesz toohave wiele kluczy zawartości, które wymagają hello sama konfiguracja zasad jest zdecydowanie zalecane toocreate zasad autoryzacji pojedynczego i użyć go ponownie wiele kluczy zawartości.</span><span class="sxs-lookup"><span data-stu-id="01463-128">If you plan toohave multiple content keys that require hello same policy configuration, it is strongly recommended toocreate a single authorization policy and reuse it with multiple content keys.</span></span>
* <span data-ttu-id="01463-129">Hello usługi dostarczania klucza buforuje ContentKeyAuthorizationPolicy i jego obiektów pokrewnych (opcje zasad i ograniczeń) przez 15 minut.</span><span class="sxs-lookup"><span data-stu-id="01463-129">hello Key Delivery service caches ContentKeyAuthorizationPolicy and its related objects (policy options and restrictions) for 15 minutes.</span></span>  <span data-ttu-id="01463-130">Jeśli tworzenie ContentKeyAuthorizationPolicy i określ toouse ograniczenie 'Token', a następnie ją przetestować, a następnie zaktualizuj zasad hello zbyt "Otwórz" ograniczeń, potrwa około 15 minut przed hello przełączniki toohello "Otwórz" Wersja zasad hello zasad.</span><span class="sxs-lookup"><span data-stu-id="01463-130">If you create a ContentKeyAuthorizationPolicy and specify toouse a “Token” restriction, then test it, and then update hello policy too“Open” restriction, it will take roughly 15 minutes before hello policy switches toohello “Open” version of hello policy.</span></span>
* <span data-ttu-id="01463-131">W przypadku dodania lub zaktualizowania zasad dostarczania elementów zawartości należy usunąć skojarzony lokalizator (jeśli istnieje) i utworzyć nowy.</span><span class="sxs-lookup"><span data-stu-id="01463-131">If you add or update your asset’s delivery policy, you must delete an existing locator (if any) and create a new locator.</span></span>
* <span data-ttu-id="01463-132">Obecnie nie można zaszyfrować pobierania progresywnego.</span><span class="sxs-lookup"><span data-stu-id="01463-132">Currently, you cannot encrypt progressive downloads.</span></span>

## <a name="aes-128-dynamic-encryption"></a><span data-ttu-id="01463-133">Dynamicznego szyfrowania AES-128</span><span class="sxs-lookup"><span data-stu-id="01463-133">AES-128 Dynamic Encryption</span></span>
> [!NOTE]
> <span data-ttu-id="01463-134">Witaj pracy z hello interfejsu API REST usługi multimediów, mają zastosowanie następujące zagadnienia:</span><span class="sxs-lookup"><span data-stu-id="01463-134">When working with hello Media Services REST API, hello following considerations apply:</span></span>
> 
> <span data-ttu-id="01463-135">Podczas uzyskiwania dostępu do obiektów w usłudze Media Services, należy ustawić określonych pól nagłówka i wartości w Twoich żądań HTTP.</span><span class="sxs-lookup"><span data-stu-id="01463-135">When accessing entities in Media Services, you must set specific header fields and values in your HTTP requests.</span></span> <span data-ttu-id="01463-136">Aby uzyskać więcej informacji, zobacz [ustawień dla rozwoju interfejsu API REST usługi Media](media-services-rest-how-to-use.md).</span><span class="sxs-lookup"><span data-stu-id="01463-136">For more information, see [Setup for Media Services REST API Development](media-services-rest-how-to-use.md).</span></span>
> 
> <span data-ttu-id="01463-137">Po pomyślnym połączeniu toohttps://media.windows.net, otrzymasz 301 przekierowanie, określając inny identyfikator URI usługi multimediów.</span><span class="sxs-lookup"><span data-stu-id="01463-137">After successfully connecting toohttps://media.windows.net, you will receive a 301 redirect specifying another Media Services URI.</span></span> <span data-ttu-id="01463-138">Należy wykonać kolejne wywołania toohello nowy identyfikator URI.</span><span class="sxs-lookup"><span data-stu-id="01463-138">You must make subsequent calls toohello new URI.</span></span> <span data-ttu-id="01463-139">Aby uzyskać informacje dotyczące tooconnect toohello AMS interfejsu API, zobacz temat [hello dostępu do interfejsu API usługi Azure Media Services przy użyciu uwierzytelniania usługi Azure AD](media-services-use-aad-auth-to-access-ams-api.md).</span><span class="sxs-lookup"><span data-stu-id="01463-139">For information on how tooconnect toohello AMS API, see [Access hello Azure Media Services API with Azure AD authentication](media-services-use-aad-auth-to-access-ams-api.md).</span></span>
> 
> 

### <a name="open-restriction"></a><span data-ttu-id="01463-140">Ograniczenie otwarte</span><span class="sxs-lookup"><span data-stu-id="01463-140">Open Restriction</span></span>
<span data-ttu-id="01463-141">Otwórz ograniczeń oznacza, że hello system będzie dostarczać hello tooanyone klucza, który wysyła żądanie klucza.</span><span class="sxs-lookup"><span data-stu-id="01463-141">Open restriction means hello system will deliver hello key tooanyone who makes a key request.</span></span> <span data-ttu-id="01463-142">To ograniczenie może być przydatna do celów testowych.</span><span class="sxs-lookup"><span data-stu-id="01463-142">This restriction might be useful for testing purposes.</span></span>

<span data-ttu-id="01463-143">Witaj poniższy przykład tworzy zasady autoryzacji otwarte i dodaje go toohello klucz zawartości.</span><span class="sxs-lookup"><span data-stu-id="01463-143">hello following example creates an open authorization policy and adds it toohello content key.</span></span>

#### <span data-ttu-id="01463-144"><a id="ContentKeyAuthorizationPolicies"></a>Utwórz ContentKeyAuthorizationPolicies</span><span class="sxs-lookup"><span data-stu-id="01463-144"><a id="ContentKeyAuthorizationPolicies"></a>Create ContentKeyAuthorizationPolicies</span></span>
<span data-ttu-id="01463-145">Żądanie:</span><span class="sxs-lookup"><span data-stu-id="01463-145">Request:</span></span>

    POST https://wamsbayclus001rest-hs.cloudapp.net/api/ContentKeyAuthorizationPolicies HTTP/1.1
    Content-Type: application/json
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=juliakoams1&urn%3aSubscriptionId=bbbef702-e769-477b-9f16-bc4d3aa97387&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1423578086&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=lZlyQ2%2bvH73qtJsb42%2fH3xF7r7EvQFR3UXyezuDENFU%3d
    x-ms-version: 2.11
    x-ms-client-request-id: d732dbfa-54fc-474c-99d6-9b46a006f389
    Host: wamsbayclus001rest-hs.cloudapp.net
    Content-Length: 36

    {"Name":"Open Authorization Policy"}

<span data-ttu-id="01463-146">Odpowiedź:</span><span class="sxs-lookup"><span data-stu-id="01463-146">Response:</span></span>

    HTTP/1.1 201 Created
    Cache-Control: no-cache
    Content-Length: 211
    Content-Type: application/json;odata=minimalmetadata;streaming=true;charset=utf-8
    Location: https://wamsbayclus001rest-hs.cloudapp.net/api/ContentKeyAuthorizationPolicies('nb%3Ackpid%3AUUID%3Adb4593da-f4d1-4cc5-a92a-d20eacbabee4')
    Server: Microsoft-IIS/8.5
    x-ms-client-request-id: d732dbfa-54fc-474c-99d6-9b46a006f389
    request-id: aabfa731-e884-4bf3-8314-492b04747ac4
    x-ms-request-id: aabfa731-e884-4bf3-8314-492b04747ac4
    X-Content-Type-Options: nosniff
    DataServiceVersion: 3.0;
    X-Powered-By: ASP.NET
    Strict-Transport-Security: max-age=31536000; includeSubDomains
    Date: Tue, 10 Feb 2015 08:25:56 GMT

    {"odata.metadata":"https://wamsbayclus001rest-hs.cloudapp.net/api/$metadata#ContentKeyAuthorizationPolicies/@Element","Id":"nb:ckpid:UUID:db4593da-f4d1-4cc5-a92a-d20eacbabee4","Name":"Open Authorization Policy"}

#### <span data-ttu-id="01463-147"><a id="ContentKeyAuthorizationPolicyOptions"></a>Utwórz ContentKeyAuthorizationPolicyOptions</span><span class="sxs-lookup"><span data-stu-id="01463-147"><a id="ContentKeyAuthorizationPolicyOptions"></a>Create ContentKeyAuthorizationPolicyOptions</span></span>
<span data-ttu-id="01463-148">Żądanie:</span><span class="sxs-lookup"><span data-stu-id="01463-148">Request:</span></span>

    POST https://wamsbayclus001rest-hs.cloudapp.net/api/ContentKeyAuthorizationPolicyOptions HTTP/1.1
    Content-Type: application/json
    DataServiceVersion: 3.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=juliakoams1&urn%3aSubscriptionId=bbbef702-e769-477b-9f16-bc4d3aa97387&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1423580006&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=Ref3EsonGF7fUKCwGwGgiMnZitzIzsDOvvMTeVrVVPg%3d
    x-ms-version: 2.11
    x-ms-client-request-id: d225e357-e60e-4f42-add8-9d93aba1409a
    Host: wamsbayclus001rest-hs.cloudapp.net
    Content-Length: 168

    {"Name":"policy","KeyDeliveryType":2,"KeyDeliveryConfiguration":"","Restrictions":[{"Name":"HLS Open Authorization Policy","KeyRestrictionType":0,"Requirements":null}]}

<span data-ttu-id="01463-149">Odpowiedź:</span><span class="sxs-lookup"><span data-stu-id="01463-149">Response:</span></span>    

    HTTP/1.1 201 Created
    Cache-Control: no-cache
    Content-Length: 349
    Content-Type: application/json;odata=minimalmetadata;streaming=true;charset=utf-8
    Location: https://wamsbayclus001rest-hs.cloudapp.net/api/ContentKeyAuthorizationPolicyOptions('nb%3Ackpoid%3AUUID%3A57829b17-1101-4797-919b-f816f4a007b7')
    Server: Microsoft-IIS/8.5
    x-ms-client-request-id: d225e357-e60e-4f42-add8-9d93aba1409a
    request-id: 81bcad37-295b-431f-972f-b23f2e4172c9
    x-ms-request-id: 81bcad37-295b-431f-972f-b23f2e4172c9
    X-Content-Type-Options: nosniff
    DataServiceVersion: 3.0;
    X-Powered-By: ASP.NET
    Strict-Transport-Security: max-age=31536000; includeSubDomains
    Date: Tue, 10 Feb 2015 08:56:40 GMT

    {"odata.metadata":"https://wamsbayclus001rest-hs.cloudapp.net/api/$metadata#ContentKeyAuthorizationPolicyOptions/@Element","Id":"nb:ckpoid:UUID:57829b17-1101-4797-919b-f816f4a007b7","Name":"policy","KeyDeliveryType":2,"KeyDeliveryConfiguration":"","Restrictions":[{"Name":"HLS Open Authorization Policy","KeyRestrictionType":0,"Requirements":null}]}

#### <span data-ttu-id="01463-150"><a id="LinkContentKeyAuthorizationPoliciesWithOptions"></a>ContentKeyAuthorizationPolicies łącza z opcjami</span><span class="sxs-lookup"><span data-stu-id="01463-150"><a id="LinkContentKeyAuthorizationPoliciesWithOptions"></a>Link ContentKeyAuthorizationPolicies with Options</span></span>
<span data-ttu-id="01463-151">Żądanie:</span><span class="sxs-lookup"><span data-stu-id="01463-151">Request:</span></span>

    POST https://wamsbayclus001rest-hs.cloudapp.net/api/ContentKeyAuthorizationPolicies('nb%3Ackpid%3AUUID%3A0baa438b-8ac2-4c40-a53c-4d4722b78715')/$links/Options HTTP/1.1
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    Content-Type: application/json
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=juliakoams1&urn%3aSubscriptionId=zbbef702-2233-477b-9f16-bc4d3aa97387&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1423580006&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=Ref3EsonGF7fUKCwGwGgiMnZitzIzsDOvvMTeVrVVPg%3d
    x-ms-version: 2.11
    x-ms-client-request-id: 9847f705-f2ca-4e95-a478-8f823dbbaa29
    Host: wamsbayclus001rest-hs.cloudapp.net
    Content-Length: 154

    {"uri":"https://wamsbayclus001rest-hs.cloudapp.net/api/ContentKeyAuthorizationPolicyOptions('nb%3Ackpoid%3AUUID%3A57829b17-1101-4797-919b-f816f4a007b7')"}

<span data-ttu-id="01463-152">Odpowiedź:</span><span class="sxs-lookup"><span data-stu-id="01463-152">Response:</span></span>

    HTTP/1.1 204 No Content

#### <span data-ttu-id="01463-153"><a id="AddAuthorizationPolicyToKey"></a>Dodaj klucz zawartości toohello zasad autoryzacji</span><span class="sxs-lookup"><span data-stu-id="01463-153"><a id="AddAuthorizationPolicyToKey"></a>Add authorization policy toohello content key</span></span>
<span data-ttu-id="01463-154">Żądanie:</span><span class="sxs-lookup"><span data-stu-id="01463-154">Request:</span></span>

    PUT https://wamsbayclus001rest-hs.cloudapp.net/api/ContentKeys('nb%3Akid%3AUUID%3A2e6d36a7-a17c-4e9a-830d-eca23ad1a6f9') HTTP/1.1
    Content-Type: application/json
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=juliakoams1&urn%3aSubscriptionId=zbbef702-2233-477b-9f16-bc4d3aa97387&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1423581565&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=JiNSG3w6r2C0nIyfKvTZj1uPJGjuitD%2b0sbfZ%2b2JDZI%3d
    x-ms-version: 2.11
    x-ms-client-request-id: e613efff-cb6a-41b4-984a-f4f8fb6e76a4
    Host: wamsbayclus001rest-hs.cloudapp.net
    Content-Length: 78

    {"AuthorizationPolicyId":"nb:ckpid:UUID:c06cebb8-c4f0-4d1a-ba00-3273fb2bc3ad"}

<span data-ttu-id="01463-155">Odpowiedź:</span><span class="sxs-lookup"><span data-stu-id="01463-155">Response:</span></span>

    HTTP/1.1 204 No Content

### <a name="token-restriction"></a><span data-ttu-id="01463-156">Ograniczenia tokenu</span><span class="sxs-lookup"><span data-stu-id="01463-156">Token Restriction</span></span>
<span data-ttu-id="01463-157">W tej sekcji opisano, jak toocreate zawartość zasady autoryzacji klucza i powiązać ją z hello klucz zawartości.</span><span class="sxs-lookup"><span data-stu-id="01463-157">This section describes how toocreate a content key authorization policy and associate it with hello content key.</span></span> <span data-ttu-id="01463-158">zasady autoryzacji Hello opisano, jakie wymagania autoryzacji musi być niespełnienia toodetermine, jeśli użytkownik hello jest autoryzowanym tooreceive hello klucza (na przykład, czy listy "klucz weryfikacji" hello zawiera klucz hello hello token została podpisana z).</span><span class="sxs-lookup"><span data-stu-id="01463-158">hello authorization policy describes what authorization requirements must be met toodetermine if hello user is authorized tooreceive hello key (for example, does hello “verification key” list contain hello key that hello token was signed with).</span></span>

<span data-ttu-id="01463-159">Opcja ograniczenia tokenu hello tooconfigure, należy toouse XML tokenu hello toodescribe wymagań autoryzacji.</span><span class="sxs-lookup"><span data-stu-id="01463-159">tooconfigure hello token restriction option, you need toouse an XML toodescribe hello token’s authorization requirements.</span></span> <span data-ttu-id="01463-160">plik XML konfiguracji ograniczenia tokenu Hello muszą być zgodne toohello następującego schematu XML.</span><span class="sxs-lookup"><span data-stu-id="01463-160">hello token restriction configuration XML must conform toohello following XML schema.</span></span>

#### <span data-ttu-id="01463-161"><a id="schema"></a>Ograniczenia tokenu schematu</span><span class="sxs-lookup"><span data-stu-id="01463-161"><a id="schema"></a>Token restriction schema</span></span>
    <?xml version="1.0" encoding="utf-8"?>
    <xs:schema xmlns:tns="http://schemas.microsoft.com/Azure/MediaServices/KeyDelivery/TokenRestrictionTemplate/v1" elementFormDefault="qualified" targetNamespace="http://schemas.microsoft.com/Azure/MediaServices/KeyDelivery/TokenRestrictionTemplate/v1" xmlns:xs="http://www.w3.org/2001/XMLSchema">
      <xs:complexType name="TokenClaim">
        <xs:sequence>
          <xs:element name="ClaimType" nillable="true" type="xs:string" />
          <xs:element minOccurs="0" name="ClaimValue" nillable="true" type="xs:string" />
        </xs:sequence>
      </xs:complexType>
      <xs:element name="TokenClaim" nillable="true" type="tns:TokenClaim" />
      <xs:complexType name="TokenRestrictionTemplate">
        <xs:sequence>
          <xs:element minOccurs="0" name="AlternateVerificationKeys" nillable="true" type="tns:ArrayOfTokenVerificationKey" />
          <xs:element name="Audience" nillable="true" type="xs:anyURI" />
          <xs:element name="Issuer" nillable="true" type="xs:anyURI" />
          <xs:element name="PrimaryVerificationKey" nillable="true" type="tns:TokenVerificationKey" />
          <xs:element minOccurs="0" name="RequiredClaims" nillable="true" type="tns:ArrayOfTokenClaim" />
        </xs:sequence>
      </xs:complexType>
      <xs:element name="TokenRestrictionTemplate" nillable="true" type="tns:TokenRestrictionTemplate" />
      <xs:complexType name="ArrayOfTokenVerificationKey">
        <xs:sequence>
          <xs:element minOccurs="0" maxOccurs="unbounded" name="TokenVerificationKey" nillable="true" type="tns:TokenVerificationKey" />
        </xs:sequence>
      </xs:complexType>
      <xs:element name="ArrayOfTokenVerificationKey" nillable="true" type="tns:ArrayOfTokenVerificationKey" />
      <xs:complexType name="TokenVerificationKey">
        <xs:sequence />
      </xs:complexType>
      <xs:element name="TokenVerificationKey" nillable="true" type="tns:TokenVerificationKey" />
      <xs:complexType name="ArrayOfTokenClaim">
        <xs:sequence>
          <xs:element minOccurs="0" maxOccurs="unbounded" name="TokenClaim" nillable="true" type="tns:TokenClaim" />
        </xs:sequence>
      </xs:complexType>
      <xs:element name="ArrayOfTokenClaim" nillable="true" type="tns:ArrayOfTokenClaim" />
      <xs:complexType name="SymmetricVerificationKey">
        <xs:complexContent mixed="false">
          <xs:extension base="tns:TokenVerificationKey">
            <xs:sequence>
              <xs:element name="KeyValue" nillable="true" type="xs:base64Binary" />
            </xs:sequence>
          </xs:extension>
        </xs:complexContent>
      </xs:complexType>
      <xs:element name="SymmetricVerificationKey" nillable="true" type="tns:SymmetricVerificationKey" />
    </xs:schema>

<span data-ttu-id="01463-162">Podczas konfigurowania hello **tokenu** ograniczone zasad, należy określić hello podstawowy ** weryfikacji klucza **, **wystawcy** i **odbiorców** parametrów.</span><span class="sxs-lookup"><span data-stu-id="01463-162">When configuring hello **token** restricted policy, you must specify hello primary** verification key**, **issuer** and **audience** parameters.</span></span> <span data-ttu-id="01463-163">Witaj ** klucza podstawowego weryfikacji ** zawiera klucz hello hello token został podpisany, **wystawcy** jest usługa bezpiecznego tokenu hello token hello problemy.</span><span class="sxs-lookup"><span data-stu-id="01463-163">hello **primary verification key **contains hello key that hello token was signed with, **issuer** is hello secure token service that issues hello token.</span></span> <span data-ttu-id="01463-164">Witaj **odbiorców** (nazywane **zakresu**) opisuje zamierzone hello hello token lub zasobu hello hello tokenu zezwala na dostęp do.</span><span class="sxs-lookup"><span data-stu-id="01463-164">hello **audience** (sometimes called **scope**) describes hello intent of hello token or hello resource hello token authorizes access to.</span></span> <span data-ttu-id="01463-165">Hello usługa Media Services klucza dostawy weryfikuje, czy te wartości w tokenie hello są takie same wartości hello hello szablonu.</span><span class="sxs-lookup"><span data-stu-id="01463-165">hello Media Services key delivery service validates that these values in hello token match hello values in hello template.</span></span> 

<span data-ttu-id="01463-166">Witaj poniższy przykład tworzy zasady autoryzacji z ograniczenia tokenu.</span><span class="sxs-lookup"><span data-stu-id="01463-166">hello following example creates an authorization policy with a token restriction.</span></span> <span data-ttu-id="01463-167">W tym przykładzie powitania klienta byłyby toopresent token, który zawiera: podpisywanie klucz (VerificationKey), wystawcy tokenów i oświadczeń wymagane.</span><span class="sxs-lookup"><span data-stu-id="01463-167">In this example, hello client would have toopresent a token that contains: signing key (VerificationKey), a token issuer, and required claims.</span></span>

### <a name="create-contentkeyauthorizationpolicies"></a><span data-ttu-id="01463-168">Utwórz ContentKeyAuthorizationPolicies</span><span class="sxs-lookup"><span data-stu-id="01463-168">Create ContentKeyAuthorizationPolicies</span></span>
<span data-ttu-id="01463-169">Utworzyć "Zasady ograniczeń tokenu" hello, jak pokazano [tutaj](#ContentKeyAuthorizationPolicies).</span><span class="sxs-lookup"><span data-stu-id="01463-169">Create hello "Token Restriction Policy" as shown [here](#ContentKeyAuthorizationPolicies).</span></span>

### <a name="create-contentkeyauthorizationpolicyoptions"></a><span data-ttu-id="01463-170">Utwórz ContentKeyAuthorizationPolicyOptions</span><span class="sxs-lookup"><span data-stu-id="01463-170">Create ContentKeyAuthorizationPolicyOptions</span></span>
<span data-ttu-id="01463-171">Żądanie:</span><span class="sxs-lookup"><span data-stu-id="01463-171">Request:</span></span>

    POST https://wamsbayclus001rest-hs.cloudapp.net/api/ContentKeyAuthorizationPolicyOptions HTTP/1.1
    Content-Type: application/json
    DataServiceVersion: 3.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=juliakoams1&urn%3aSubscriptionId=bbbef702-e769-477b-9f16-bc4d3aa97387&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1423580720&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=5LsNu%2b0D4eD3UOP3BviTLDkUjaErdUx0ekJ8402xidQ%3d
    x-ms-version: 2.11
    x-ms-client-request-id: 2643d836-bfe7-438e-9ba2-bc6ff28e4a53
    Host: wamsbayclus001rest-hs.cloudapp.net
    Content-Length: 1079

    {"Name":"Token option for HLS","KeyDeliveryType":2,"KeyDeliveryConfiguration":null,"Restrictions":[{"Name":"Token Authorization Policy","KeyRestrictionType":1,"Requirements":"<TokenRestrictionTemplate xmlns:i=\"http://www.w3.org/2001/XMLSchema-instance\" xmlns=\"http://schemas.microsoft.com/Azure/MediaServices/KeyDelivery/TokenRestrictionTemplate/v1\"><AlternateVerificationKeys><TokenVerificationKey i:type=\"SymmetricVerificationKey\"><KeyValue>BklyAFiPTQsuJNKriQJBZHYaKM2CkCTDQX2bw9sMYuvEC9sjW0W7GUIBygQL/+POEeUqCYPnmEU2g0o1GW2Oqg==</KeyValue></TokenVerificationKey></AlternateVerificationKeys><Audience>urn:test</Audience><Issuer>http://testacs.com/</Issuer><PrimaryVerificationKey i:type=\"SymmetricVerificationKey\"><KeyValue>E5BUHiN4vBdzUzdP0IWaHFMMU3D1uRZgF16TOhSfwwHGSw+Kbf0XqsHzEIYk11M372viB9vbiacsdcQksA0ftw==</KeyValue></PrimaryVerificationKey><RequiredClaims><TokenClaim><ClaimType>urn:microsoft:azure:mediaservices:contentkeyidentifier</ClaimType><ClaimValue i:nil=\"true\" /></TokenClaim></RequiredClaims><TokenType>SWT</TokenType></TokenRestrictionTemplate>"}]}

<span data-ttu-id="01463-172">Odpowiedź:</span><span class="sxs-lookup"><span data-stu-id="01463-172">Response:</span></span>    

    HTTP/1.1 201 Created
    Cache-Control: no-cache
    Content-Length: 1260
    Content-Type: application/json;odata=minimalmetadata;streaming=true;charset=utf-8
    Location: https://wamsbayclus001rest-hs.cloudapp.net/api/ContentKeyAuthorizationPolicyOptions('nb%3Ackpoid%3AUUID%3Ae1ef6145-46e8-4ee6-9756-b1cf96328c23')
    Server: Microsoft-IIS/8.5
    x-ms-client-request-id: 2643d836-bfe7-438e-9ba2-bc6ff28e4a53
    request-id: 2310b716-aeaa-421e-913e-3ce2f6f685ca
    x-ms-request-id: 2310b716-aeaa-421e-913e-3ce2f6f685ca
    X-Content-Type-Options: nosniff
    DataServiceVersion: 3.0;
    X-Powered-By: ASP.NET
    Strict-Transport-Security: max-age=31536000; includeSubDomains
    Date: Tue, 10 Feb 2015 09:10:37 GMT

    {"odata.metadata":"https://wamsbayclus001rest-hs.cloudapp.net/api/$metadata#ContentKeyAuthorizationPolicyOptions/@Element","Id":"nb:ckpoid:UUID:e1ef6145-46e8-4ee6-9756-b1cf96328c23","Name":"Token option for HLS","KeyDeliveryType":2,"KeyDeliveryConfiguration":null,"Restrictions":[{"Name":"Token Authorization Policy","KeyRestrictionType":1,"Requirements":"<TokenRestrictionTemplate xmlns:i=\"http://www.w3.org/2001/XMLSchema-instance\" xmlns=\"http://schemas.microsoft.com/Azure/MediaServices/KeyDelivery/TokenRestrictionTemplate/v1\"><AlternateVerificationKeys><TokenVerificationKey i:type=\"SymmetricVerificationKey\"><KeyValue>BklyAFiPTQsuJNKriQJBZHYaKM2CkCTDQX2bw9sMYuvEC9sjW0W7GUIBygQL/+POEeUqCYPnmEU2g0o1GW2Oqg==</KeyValue></TokenVerificationKey></AlternateVerificationKeys><Audience>urn:test</Audience><Issuer>http://testacs.com/</Issuer><PrimaryVerificationKey i:type=\"SymmetricVerificationKey\"><KeyValue>E5BUHiN4vBdzUzdP0IWaHFMMU3D1uRZgF16TOhSfwwHGSw+Kbf0XqsHzEIYk11M372viB9vbiacsdcQksA0ftw==</KeyValue></PrimaryVerificationKey><RequiredClaims><TokenClaim><ClaimType>urn:microsoft:azure:mediaservices:contentkeyidentifier</ClaimType><ClaimValue i:nil=\"true\" /></TokenClaim></RequiredClaims><TokenType>SWT</TokenType></TokenRestrictionTemplate>"}]}

#### <a name="link-contentkeyauthorizationpolicies-with-options"></a><span data-ttu-id="01463-173">ContentKeyAuthorizationPolicies łącza z opcjami</span><span class="sxs-lookup"><span data-stu-id="01463-173">Link ContentKeyAuthorizationPolicies with Options</span></span>
<span data-ttu-id="01463-174">Łącze ContentKeyAuthorizationPolicies z opcjami, jak pokazano [tutaj](#ContentKeyAuthorizationPolicies).</span><span class="sxs-lookup"><span data-stu-id="01463-174">Link ContentKeyAuthorizationPolicies with Options as shown [here](#ContentKeyAuthorizationPolicies).</span></span>

#### <a name="add-authorization-policy-toohello-content-key"></a><span data-ttu-id="01463-175">Dodaj klucz zawartości toohello zasad autoryzacji</span><span class="sxs-lookup"><span data-stu-id="01463-175">Add authorization policy toohello content key</span></span>
<span data-ttu-id="01463-176">Dodaj AuthorizationPolicy toohello ContentKey, jak pokazano [tutaj](#AddAuthorizationPolicyToKey).</span><span class="sxs-lookup"><span data-stu-id="01463-176">Add AuthorizationPolicy toohello ContentKey as shown [here](#AddAuthorizationPolicyToKey).</span></span>

## <a name="playready-dynamic-encryption"></a><span data-ttu-id="01463-177">Szyfrowanie PlayReady dynamiczne</span><span class="sxs-lookup"><span data-stu-id="01463-177">PlayReady Dynamic Encryption</span></span>
<span data-ttu-id="01463-178">Usługi Media Services umożliwia tooconfigure hello prawa i ograniczenia, które mają dla hello tooenforce środowiska uruchomieniowego PlayReady DRM, gdy użytkownik próbuje się, że tooplay ponownie chronionej zawartości.</span><span class="sxs-lookup"><span data-stu-id="01463-178">Media Services enables you tooconfigure hello rights and restrictions that you want for hello PlayReady DRM runtime tooenforce when a user is trying tooplay back protected content.</span></span> 

<span data-ttu-id="01463-179">W przypadku ochrony zawartości przy użyciu PlayReady, z hello czynności należy toospecify w zasadach autoryzacji jest ciąg XML, który definiuje hello [szablon licencji PlayReady](media-services-playready-license-template-overview.md).</span><span class="sxs-lookup"><span data-stu-id="01463-179">When protecting your content with PlayReady, one of hello things you need toospecify in your authorization policy is an XML string that defines hello [PlayReady license template](media-services-playready-license-template-overview.md).</span></span> 

### <a name="open-restriction"></a><span data-ttu-id="01463-180">Ograniczenie otwarte</span><span class="sxs-lookup"><span data-stu-id="01463-180">Open Restriction</span></span>
<span data-ttu-id="01463-181">Otwórz ograniczeń oznacza, że hello system będzie dostarczać hello tooanyone klucza, który wysyła żądanie klucza.</span><span class="sxs-lookup"><span data-stu-id="01463-181">Open restriction means hello system will deliver hello key tooanyone who makes a key request.</span></span> <span data-ttu-id="01463-182">To ograniczenie może być przydatna do celów testowych.</span><span class="sxs-lookup"><span data-stu-id="01463-182">This restriction might be useful for testing purposes.</span></span>

<span data-ttu-id="01463-183">Witaj poniższy przykład tworzy zasady autoryzacji otwarte i dodaje go toohello klucz zawartości.</span><span class="sxs-lookup"><span data-stu-id="01463-183">hello following example creates an open authorization policy and adds it toohello content key.</span></span>

#### <span data-ttu-id="01463-184"><a id="ContentKeyAuthorizationPolicies2"></a>Utwórz ContentKeyAuthorizationPolicies</span><span class="sxs-lookup"><span data-stu-id="01463-184"><a id="ContentKeyAuthorizationPolicies2"></a>Create ContentKeyAuthorizationPolicies</span></span>
<span data-ttu-id="01463-185">Żądanie:</span><span class="sxs-lookup"><span data-stu-id="01463-185">Request:</span></span>

    POST https://wamsbayclus001rest-hs.cloudapp.net/api/ContentKeyAuthorizationPolicies HTTP/1.1
    Content-Type: application/json
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=juliakoams1&urn%3aSubscriptionId=bbef702-2233-477b-9f16-bc4d3aa97387&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1423581565&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=JiNSG3w6r2C0nIyfKvTZj1uPJGjuitD%2b0sbfZ%2b2JDZI%3d
    x-ms-version: 2.11
    x-ms-client-request-id: 9e7fa407-f84e-43aa-8f05-9790b46e279b
    Host: wamsbayclus001rest-hs.cloudapp.net
    Content-Length: 58

    {"Name":"Deliver Common Content Key"}

<span data-ttu-id="01463-186">Odpowiedź:</span><span class="sxs-lookup"><span data-stu-id="01463-186">Response:</span></span>

    HTTP/1.1 201 Created
    Cache-Control: no-cache
    Content-Length: 233
    Content-Type: application/json;odata=minimalmetadata;streaming=true;charset=utf-8
    Location: https://wamsbayclus001rest-hs.cloudapp.net/api/ContentKeyAuthorizationPolicies('nb%3Ackpid%3AUUID%3Acc3c64a8-e2fc-4e09-bf60-ac954251a387')
    Server: Microsoft-IIS/8.5
    x-ms-client-request-id: 9e7fa407-f84e-43aa-8f05-9790b46e279b
    request-id: b3d33c1b-a9cb-4120-ac0c-18f64846c147
    x-ms-request-id: b3d33c1b-a9cb-4120-ac0c-18f64846c147
    X-Content-Type-Options: nosniff
    DataServiceVersion: 3.0;
    X-Powered-By: ASP.NET
    Strict-Transport-Security: max-age=31536000; includeSubDomains
    Date: Tue, 10 Feb 2015 09:26:00 GMT

    {"odata.metadata":"https://wamsbayclus001rest-hs.cloudapp.net/api/$metadata#ContentKeyAuthorizationPolicies/@Element","Id":"nb:ckpid:UUID:cc3c64a8-e2fc-4e09-bf60-ac954251a387","Name":"Deliver Common Content Key"}


#### <a name="create-contentkeyauthorizationpolicyoptions"></a><span data-ttu-id="01463-187">Utwórz ContentKeyAuthorizationPolicyOptions</span><span class="sxs-lookup"><span data-stu-id="01463-187">Create ContentKeyAuthorizationPolicyOptions</span></span>
<span data-ttu-id="01463-188">Żądanie:</span><span class="sxs-lookup"><span data-stu-id="01463-188">Request:</span></span>

    POST https://wamsbayclus001rest-hs.cloudapp.net/api/ContentKeyAuthorizationPolicyOptions HTTP/1.1
    Content-Type: application/json
    DataServiceVersion: 3.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=juliakoams1&urn%3aSubscriptionId=zbbef702-2233-477b-9f16-bc4d3aa97387&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1423581565&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=JiNSG3w6r2C0nIyfKvTZj1uPJGjuitD%2b0sbfZ%2b2JDZI%3d
    x-ms-version: 2.11
    x-ms-client-request-id: f160ad25-b457-4bc6-8197-315604c5e585
    Host: wamsbayclus001rest-hs.cloudapp.net
    Content-Length: 593

    {"Name":"","KeyDeliveryType":1,"KeyDeliveryConfiguration":"<PlayReadyLicenseResponseTemplate xmlns:i=\"http://www.w3.org/2001/XMLSchema-instance\" xmlns=\"http://schemas.microsoft.com/Azure/MediaServices/KeyDelivery/PlayReadyTemplate/v1\"><LicenseTemplates><PlayReadyLicenseTemplate><AllowTestDevices>false</AllowTestDevices><ContentKey i:type=\"ContentEncryptionKeyFromHeader\" /><LicenseType>Nonpersistent</LicenseType><PlayRight /></PlayReadyLicenseTemplate></LicenseTemplates></PlayReadyLicenseResponseTemplate>","Restrictions":[{"Name":"Open","KeyRestrictionType":0,"Requirements":null}]}

<span data-ttu-id="01463-189">Odpowiedź:</span><span class="sxs-lookup"><span data-stu-id="01463-189">Response:</span></span>

    HTTP/1.1 201 Created
    Cache-Control: no-cache
    Content-Length: 774
    Content-Type: application/json;odata=minimalmetadata;streaming=true;charset=utf-8
    Location: https://wamsbayclus001rest-hs.cloudapp.net/api/ContentKeyAuthorizationPolicyOptions('nb%3Ackpoid%3AUUID%3A1052308c-4df7-4fdb-8d21-4d2141fc2be0')
    Server: Microsoft-IIS/8.5
    x-ms-client-request-id: f160ad25-b457-4bc6-8197-315604c5e585
    request-id: 563f5a42-50a4-4c4a-add8-a833f8364231
    x-ms-request-id: 563f5a42-50a4-4c4a-add8-a833f8364231
    X-Content-Type-Options: nosniff
    DataServiceVersion: 3.0;
    X-Powered-By: ASP.NET
    Strict-Transport-Security: max-age=31536000; includeSubDomains
    Date: Tue, 10 Feb 2015 09:23:24 GMT

    {"odata.metadata":"https://wamsbayclus001rest-hs.cloudapp.net/api/$metadata#ContentKeyAuthorizationPolicyOptions/@Element","Id":"nb:ckpoid:UUID:1052308c-4df7-4fdb-8d21-4d2141fc2be0","Name":"","KeyDeliveryType":1,"KeyDeliveryConfiguration":"<PlayReadyLicenseResponseTemplate xmlns:i=\"http://www.w3.org/2001/XMLSchema-instance\" xmlns=\"http://schemas.microsoft.com/Azure/MediaServices/KeyDelivery/PlayReadyTemplate/v1\"><LicenseTemplates><PlayReadyLicenseTemplate><AllowTestDevices>false</AllowTestDevices><ContentKey i:type=\"ContentEncryptionKeyFromHeader\" /><LicenseType>Nonpersistent</LicenseType><PlayRight /></PlayReadyLicenseTemplate></LicenseTemplates></PlayReadyLicenseResponseTemplate>","Restrictions":[{"Name":"Open","KeyRestrictionType":0,"Requirements":null}]}

#### <a name="link-contentkeyauthorizationpolicies-with-options"></a><span data-ttu-id="01463-190">ContentKeyAuthorizationPolicies łącza z opcjami</span><span class="sxs-lookup"><span data-stu-id="01463-190">Link ContentKeyAuthorizationPolicies with Options</span></span>
<span data-ttu-id="01463-191">Łącze ContentKeyAuthorizationPolicies z opcjami, jak pokazano [tutaj](#ContentKeyAuthorizationPolicies).</span><span class="sxs-lookup"><span data-stu-id="01463-191">Link ContentKeyAuthorizationPolicies with Options as shown [here](#ContentKeyAuthorizationPolicies).</span></span>

#### <a name="add-authorization-policy-toohello-content-key"></a><span data-ttu-id="01463-192">Dodaj klucz zawartości toohello zasad autoryzacji</span><span class="sxs-lookup"><span data-stu-id="01463-192">Add authorization policy toohello content key</span></span>
<span data-ttu-id="01463-193">Dodaj AuthorizationPolicy toohello ContentKey, jak pokazano [tutaj](#AddAuthorizationPolicyToKey).</span><span class="sxs-lookup"><span data-stu-id="01463-193">Add AuthorizationPolicy toohello ContentKey as shown [here](#AddAuthorizationPolicyToKey).</span></span>

### <a name="token-restriction"></a><span data-ttu-id="01463-194">Ograniczenia tokenu</span><span class="sxs-lookup"><span data-stu-id="01463-194">Token Restriction</span></span>
<span data-ttu-id="01463-195">Opcja ograniczenia tokenu hello tooconfigure, należy toouse XML tokenu hello toodescribe wymagań autoryzacji.</span><span class="sxs-lookup"><span data-stu-id="01463-195">tooconfigure hello token restriction option, you need toouse an XML toodescribe hello token’s authorization requirements.</span></span> <span data-ttu-id="01463-196">plik XML konfiguracji ograniczenia tokenu Hello musi być zgodna schematu XML toohello wyświetlany w [to](#schema) sekcji.</span><span class="sxs-lookup"><span data-stu-id="01463-196">hello token restriction configuration XML must conform toohello XML schema shown in [this](#schema) section.</span></span>

#### <a name="create-contentkeyauthorizationpolicies"></a><span data-ttu-id="01463-197">Utwórz ContentKeyAuthorizationPolicies</span><span class="sxs-lookup"><span data-stu-id="01463-197">Create ContentKeyAuthorizationPolicies</span></span>
<span data-ttu-id="01463-198">Utwórz ContentKeyAuthorizationPolicies, jak pokazano [tutaj](#ContentKeyAuthorizationPolicies2).</span><span class="sxs-lookup"><span data-stu-id="01463-198">Create ContentKeyAuthorizationPolicies as shown [here](#ContentKeyAuthorizationPolicies2).</span></span>

#### <a name="create-contentkeyauthorizationpolicyoptions"></a><span data-ttu-id="01463-199">Utwórz ContentKeyAuthorizationPolicyOptions</span><span class="sxs-lookup"><span data-stu-id="01463-199">Create ContentKeyAuthorizationPolicyOptions</span></span>
<span data-ttu-id="01463-200">Żądanie:</span><span class="sxs-lookup"><span data-stu-id="01463-200">Request:</span></span>

    POST https://wamsbayclus001rest-hs.cloudapp.net/api/ContentKeyAuthorizationPolicyOptions HTTP/1.1
    Content-Type: application/json
    DataServiceVersion: 3.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=juliakoams1&urn%3aSubscriptionId=zbbef702-2233-477b-9f16-bc4d3aa97387&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1423583561&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=5eZnkOsSv%2fLLEKmS%2bWObBlsNYyee8BQlp%2bUYbjugcJg%3d
    x-ms-version: 2.11
    x-ms-client-request-id: ab079b0e-2ba9-4cf1-b549-a97bfa6cd2d3
    Host: wamsbayclus001rest-hs.cloudapp.net
    Content-Length: 1525

    {"Name":"Token option","KeyDeliveryType":1,"KeyDeliveryConfiguration":"<PlayReadyLicenseResponseTemplate xmlns:i=\"http://www.w3.org/2001/XMLSchema-instance\" xmlns=\"http://schemas.microsoft.com/Azure/MediaServices/KeyDelivery/PlayReadyTemplate/v1\"><LicenseTemplates><PlayReadyLicenseTemplate><AllowTestDevices>false</AllowTestDevices><ContentKey i:type=\"ContentEncryptionKeyFromHeader\" /><LicenseType>Nonpersistent</LicenseType><PlayRight /></PlayReadyLicenseTemplate></LicenseTemplates></PlayReadyLicenseResponseTemplate>","Restrictions":[{"Name":"Token Authorization Policy","KeyRestrictionType":1,"Requirements":"<TokenRestrictionTemplate xmlns:i=\"http://www.w3.org/2001/XMLSchema-instance\" xmlns=\"http://schemas.microsoft.com/Azure/MediaServices/KeyDelivery/TokenRestrictionTemplate/v1\"><AlternateVerificationKeys><TokenVerificationKey i:type=\"SymmetricVerificationKey\"><KeyValue>w52OyHVqXT8aaupGxuJ3NGt8M6opHDOtx132p4r6q4hLI6ffnLusgEGie1kedUewVoIe1tqDkVE6xsIV7O91KA==</KeyValue></TokenVerificationKey></AlternateVerificationKeys><Audience>urn:test</Audience><Issuer>http://testacs.com/</Issuer><PrimaryVerificationKey i:type=\"SymmetricVerificationKey\"><KeyValue>dYwLKIEMBljLeY9VM7vWdlhps31Fbt0XXhqP5VyjQa33bJXleBtkzQ6dF5AtwI9gDcdM2dV2TvYNhCilBKjMCg==</KeyValue></PrimaryVerificationKey><RequiredClaims><TokenClaim><ClaimType>urn:microsoft:azure:mediaservices:contentkeyidentifier</ClaimType><ClaimValue i:nil=\"true\" /></TokenClaim></RequiredClaims><TokenType>SWT</TokenType></TokenRestrictionTemplate>"}]}

<span data-ttu-id="01463-201">Odpowiedź:</span><span class="sxs-lookup"><span data-stu-id="01463-201">Response:</span></span>

    HTTP/1.1 201 Created
    Cache-Control: no-cache
    Content-Length: 1706
    Content-Type: application/json;odata=minimalmetadata;streaming=true;charset=utf-8
    Location: https://wamsbayclus001rest-hs.cloudapp.net/api/ContentKeyAuthorizationPolicyOptions('nb%3Ackpoid%3AUUID%3Ae42bbeae-de42-4077-90e9-a844f297ef70')
    Server: Microsoft-IIS/8.5
    x-ms-client-request-id: ab079b0e-2ba9-4cf1-b549-a97bfa6cd2d3
    request-id: ccf8a4ba-731e-4124-8192-079592c251cc
    x-ms-request-id: ccf8a4ba-731e-4124-8192-079592c251cc
    X-Content-Type-Options: nosniff
    DataServiceVersion: 3.0;
    X-Powered-By: ASP.NET
    Strict-Transport-Security: max-age=31536000; includeSubDomains
    Date: Tue, 10 Feb 2015 09:58:47 GMT

    {"odata.metadata":"https://wamsbayclus001rest-hs.cloudapp.net/api/$metadata#ContentKeyAuthorizationPolicyOptions/@Element","Id":"nb:ckpoid:UUID:e42bbeae-de42-4077-90e9-a844f297ef70","Name":"Token option","KeyDeliveryType":1,"KeyDeliveryConfiguration":"<PlayReadyLicenseResponseTemplate xmlns:i=\"http://www.w3.org/2001/XMLSchema-instance\" xmlns=\"http://schemas.microsoft.com/Azure/MediaServices/KeyDelivery/PlayReadyTemplate/v1\"><LicenseTemplates><PlayReadyLicenseTemplate><AllowTestDevices>false</AllowTestDevices><ContentKey i:type=\"ContentEncryptionKeyFromHeader\" /><LicenseType>Nonpersistent</LicenseType><PlayRight /></PlayReadyLicenseTemplate></LicenseTemplates></PlayReadyLicenseResponseTemplate>","Restrictions":[{"Name":"Token Authorization Policy","KeyRestrictionType":1,"Requirements":"<TokenRestrictionTemplate xmlns:i=\"http://www.w3.org/2001/XMLSchema-instance\" xmlns=\"http://schemas.microsoft.com/Azure/MediaServices/KeyDelivery/TokenRestrictionTemplate/v1\"><AlternateVerificationKeys><TokenVerificationKey i:type=\"SymmetricVerificationKey\"><KeyValue>w52OyHVqXT8aaupGxuJ3NGt8M6opHDOtx132p4r6q4hLI6ffnLusgEGie1kedUewVoIe1tqDkVE6xsIV7O91KA==</KeyValue></TokenVerificationKey></AlternateVerificationKeys><Audience>urn:test</Audience><Issuer>http://testacs.com/</Issuer><PrimaryVerificationKey i:type=\"SymmetricVerificationKey\"><KeyValue>dYwLKIEMBljLeY9VM7vWdlhps31Fbt0XXhqP5VyjQa33bJXleBtkzQ6dF5AtwI9gDcdM2dV2TvYNhCilBKjMCg==</KeyValue></PrimaryVerificationKey><RequiredClaims><TokenClaim><ClaimType>urn:microsoft:azure:mediaservices:contentkeyidentifier</ClaimType><ClaimValue i:nil=\"true\" /></TokenClaim></RequiredClaims><TokenType>SWT</TokenType></TokenRestrictionTemplate>"}]}

#### <a name="link-contentkeyauthorizationpolicies-with-options"></a><span data-ttu-id="01463-202">ContentKeyAuthorizationPolicies łącza z opcjami</span><span class="sxs-lookup"><span data-stu-id="01463-202">Link ContentKeyAuthorizationPolicies with Options</span></span>
<span data-ttu-id="01463-203">Łącze ContentKeyAuthorizationPolicies z opcjami, jak pokazano [tutaj](#ContentKeyAuthorizationPolicies).</span><span class="sxs-lookup"><span data-stu-id="01463-203">Link ContentKeyAuthorizationPolicies with Options as shown [here](#ContentKeyAuthorizationPolicies).</span></span>

#### <a name="add-authorization-policy-toohello-content-key"></a><span data-ttu-id="01463-204">Dodaj klucz zawartości toohello zasad autoryzacji</span><span class="sxs-lookup"><span data-stu-id="01463-204">Add authorization policy toohello content key</span></span>
<span data-ttu-id="01463-205">Dodaj AuthorizationPolicy toohello ContentKey, jak pokazano [tutaj](#AddAuthorizationPolicyToKey).</span><span class="sxs-lookup"><span data-stu-id="01463-205">Add AuthorizationPolicy toohello ContentKey as shown [here](#AddAuthorizationPolicyToKey).</span></span>

## <span data-ttu-id="01463-206"><a id="types"></a>Typy używane podczas definiowania ContentKeyAuthorizationPolicy</span><span class="sxs-lookup"><span data-stu-id="01463-206"><a id="types"></a>Types used when defining ContentKeyAuthorizationPolicy</span></span>
### <span data-ttu-id="01463-207"><a id="ContentKeyRestrictionType"></a>ContentKeyRestrictionType</span><span class="sxs-lookup"><span data-stu-id="01463-207"><a id="ContentKeyRestrictionType"></a>ContentKeyRestrictionType</span></span>
    public enum ContentKeyRestrictionType
    {
        Open = 0,
        TokenRestricted = 1,
        IPRestricted = 2,
    }

### <span data-ttu-id="01463-208"><a id="ContentKeyDeliveryType"></a>ContentKeyDeliveryType</span><span class="sxs-lookup"><span data-stu-id="01463-208"><a id="ContentKeyDeliveryType"></a>ContentKeyDeliveryType</span></span>
    public enum ContentKeyDeliveryType
    {
        None = 0,
        PlayReadyLicense = 1,
        BaselineHttp = 2,
        Widevine = 3
    }


## <a name="media-services-learning-paths"></a><span data-ttu-id="01463-209">Ścieżki szkoleniowe dotyczące usługi Media Services</span><span class="sxs-lookup"><span data-stu-id="01463-209">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="01463-210">Przekazywanie opinii</span><span class="sxs-lookup"><span data-stu-id="01463-210">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="next-steps"></a><span data-ttu-id="01463-211">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="01463-211">Next Steps</span></span>
<span data-ttu-id="01463-212">Teraz, gdy skonfigurowano zasady autoryzacji klucza zawartości, przejdź toohello [jak zasady dostarczania elementu zawartości tooconfigure](media-services-rest-configure-asset-delivery-policy.md) tematu.</span><span class="sxs-lookup"><span data-stu-id="01463-212">Now that you have configured content key's authorization policy, go toohello [How tooconfigure asset delivery policy](media-services-rest-configure-asset-delivery-policy.md) topic.</span></span>

