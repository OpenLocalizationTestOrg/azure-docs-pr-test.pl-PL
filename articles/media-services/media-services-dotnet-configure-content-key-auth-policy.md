---
title: "zasady autoryzacji klucza zawartości aaaConfigure przy użyciu zestawu .NET SDK usługi Media | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak tooconfigure zasady autoryzacji klucza zawartości przy użyciu zestawu .NET SDK usługi multimediów."
services: media-services
documentationcenter: 
author: Mingfeiy
manager: cfowler
editor: 
ms.assetid: 1a0aedda-5b87-4436-8193-09fc2f14310c
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/09/2017
ms.author: juliako;mingfeiy
ms.openlocfilehash: cfcbc5da9819bcec8b163fef183988a8beff9ed2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="dynamic-encryption-configure-content-key-authorization-policy"></a><span data-ttu-id="4241b-103">Szyfrowania dynamicznego: Skonfiguruj zasady autoryzacji klucza zawartości</span><span class="sxs-lookup"><span data-stu-id="4241b-103">Dynamic encryption: configure content key authorization policy</span></span>
[!INCLUDE [media-services-selector-content-key-auth-policy](../../includes/media-services-selector-content-key-auth-policy.md)]

## <a name="overview"></a><span data-ttu-id="4241b-104">Omówienie</span><span class="sxs-lookup"><span data-stu-id="4241b-104">Overview</span></span>
<span data-ttu-id="4241b-105">Microsoft Azure Media Services umożliwia toodeliver MPEG-DASH, Smooth Streaming i strumieni HTTP-Live-Streaming (HLS) chronionych przy Standard AES (Advanced Encryption) (przy użyciu kluczy szyfrowania 128-bitowego) lub [Microsoft PlayReady DRM](https://www.microsoft.com/playready/overview/).</span><span class="sxs-lookup"><span data-stu-id="4241b-105">Microsoft Azure Media Services enables you toodeliver MPEG-DASH, Smooth Streaming, and HTTP-Live-Streaming (HLS) streams protected with Advanced Encryption Standard (AES) (using 128-bit encryption keys) or [Microsoft PlayReady DRM](https://www.microsoft.com/playready/overview/).</span></span> <span data-ttu-id="4241b-106">AMS umożliwia również należy toodeliver strumienie DASH korzystających zaszyfrowane za pomocą Widevine DRM.</span><span class="sxs-lookup"><span data-stu-id="4241b-106">AMS also enables you toodeliver DASH streams encrypted with Widevine DRM.</span></span> <span data-ttu-id="4241b-107">Zarówno PlayReady i Widevine są szyfrowane na powitania specyfikacją Common Encryption (ISO/IEC CENC 23001-7).</span><span class="sxs-lookup"><span data-stu-id="4241b-107">Both PlayReady and Widevine are encrypted per hello Common Encryption (ISO/IEC 23001-7 CENC) specification.</span></span>

<span data-ttu-id="4241b-108">Media Services udostępnia również **usługi dostarczania licencji/klucz** z których klienci mogą uzyskać kluczy AES lub tooplay licencji PlayReady/Widevine hello zaszyfrowaną zawartość.</span><span class="sxs-lookup"><span data-stu-id="4241b-108">Media Services also provides a **Key/License Delivery Service** from which clients can obtain AES keys or PlayReady/Widevine licenses tooplay hello encrypted content.</span></span>

<span data-ttu-id="4241b-109">Jeśli chcesz dla usługi Media Services tooencrypt zasób, należy tooassociate klucza szyfrowania (**CommonEncryption** lub **EnvelopeEncryption**) z zasobów hello (zgodnie z opisem [tutaj](media-services-dotnet-create-contentkey.md)) a także skonfigurować zasady autoryzacji klucza hello (zgodnie z opisem w tym artykule).</span><span class="sxs-lookup"><span data-stu-id="4241b-109">If you want for Media Services tooencrypt an asset, you need tooassociate an encryption key (**CommonEncryption** or **EnvelopeEncryption**) with hello asset (as described [here](media-services-dotnet-create-contentkey.md)) and also configure authorization policies for hello key (as described in this article).</span></span>

<span data-ttu-id="4241b-110">Gdy odtwarzacza zażąda strumienia, usługa Media Services używa hello określony toodynamically klucza szyfrowania zawartości przy użyciu szyfrowania AES lub DRM.</span><span class="sxs-lookup"><span data-stu-id="4241b-110">When a stream is requested by a player, Media Services uses hello specified key toodynamically encrypt your content using AES or DRM encryption.</span></span> <span data-ttu-id="4241b-111">toodecrypt hello strumienia, hello odtwarzacza zażąda hello klucza z usługi dostarczania klucza hello.</span><span class="sxs-lookup"><span data-stu-id="4241b-111">toodecrypt hello stream, hello player will request hello key from hello key delivery service.</span></span> <span data-ttu-id="4241b-112">toodecide czy hello użytkownik jest autoryzowany tooget hello klucza, usługi hello ocenia zasady autoryzacji hello określonych hello klucza.</span><span class="sxs-lookup"><span data-stu-id="4241b-112">toodecide whether or not hello user is authorized tooget hello key, hello service evaluates hello authorization policies that you specified for hello key.</span></span>

<span data-ttu-id="4241b-113">Usługa Media Services obsługuje wiele sposobów uwierzytelniania użytkowników, którzy tworzą żądania klucza.</span><span class="sxs-lookup"><span data-stu-id="4241b-113">Media Services supports multiple ways of authenticating users who make key requests.</span></span> <span data-ttu-id="4241b-114">Witaj zasady autoryzacji klucza zawartości może mieć jeden lub więcej ograniczeń: **Otwórz** lub **tokenu** ograniczeń.</span><span class="sxs-lookup"><span data-stu-id="4241b-114">hello content key authorization policy could have one or more authorization restrictions: **open** or **token** restriction.</span></span> <span data-ttu-id="4241b-115">Witaj zasadzie ograniczenia tokenu musi towarzyszyć token wystawiony przez Secure Token Service (STS).</span><span class="sxs-lookup"><span data-stu-id="4241b-115">hello token restricted policy must be accompanied by a token issued by a Secure Token Service (STS).</span></span> <span data-ttu-id="4241b-116">Usługa Media Services obsługuje tokenów w hello **proste tokenów sieci Web** ([SWT](https://msdn.microsoft.com/library/gg185950.aspx#BKMK_2)) format i **JSON Web Token** ([JWT](https://msdn.microsoft.com/library/gg185950.aspx#BKMK_3)) format.</span><span class="sxs-lookup"><span data-stu-id="4241b-116">Media Services supports tokens in hello **Simple Web Tokens** ([SWT](https://msdn.microsoft.com/library/gg185950.aspx#BKMK_2)) format and **JSON Web Token** ([JWT](https://msdn.microsoft.com/library/gg185950.aspx#BKMK_3)) format.</span></span>

<span data-ttu-id="4241b-117">Usługi Media Services nie zapewnia bezpieczny tokenu usługi.</span><span class="sxs-lookup"><span data-stu-id="4241b-117">Media Services does not provide Secure Token Services.</span></span> <span data-ttu-id="4241b-118">Można utworzyć niestandardowy STS lub korzystać z usługi Microsoft Azure ACS tooissue tokenów.</span><span class="sxs-lookup"><span data-stu-id="4241b-118">You can create a custom STS or leverage Microsoft Azure ACS tooissue tokens.</span></span> <span data-ttu-id="4241b-119">Witaj STS musi być skonfigurowany toocreate podpisany token z określonym kluczem hello i wystawiających oświadczenia, określona w konfiguracji ograniczenia tokenu hello (zgodnie z opisem w tym artykule).</span><span class="sxs-lookup"><span data-stu-id="4241b-119">hello STS must be configured toocreate a token signed with hello specified key and issue claims that you specified in hello token restriction configuration (as described in this article).</span></span> <span data-ttu-id="4241b-120">Witaj usługa Media Services klucza dostawy zwróci klienta toohello klucza szyfrowania hello Jeśli hello token jest prawidłowy i hello oświadczenia w tokenie hello pasują hello klucza zawartości.</span><span class="sxs-lookup"><span data-stu-id="4241b-120">hello Media Services key delivery service will return hello encryption key toohello client if hello token is valid and hello claims in hello token match those configured for hello content key.</span></span>

<span data-ttu-id="4241b-121">Aby uzyskać więcej informacji, zobacz</span><span class="sxs-lookup"><span data-stu-id="4241b-121">For more information, see</span></span>

[<span data-ttu-id="4241b-122">Uwierzytelniania tokenu JWT</span><span class="sxs-lookup"><span data-stu-id="4241b-122">JWT token authentication</span></span>](http://www.gtrifonov.com/2015/01/03/jwt-token-authentication-in-azure-media-services-and-dynamic-encryption/)

<span data-ttu-id="4241b-123">[Integracja aplikacji na podstawie Azure Media Services OWIN MVC z usługi Azure Active Directory i ograniczenie klucza dostarczania zawartości na podstawie oświadczeń JWT](http://www.gtrifonov.com/2015/01/24/mvc-owin-azure-media-services-ad-integration/).</span><span class="sxs-lookup"><span data-stu-id="4241b-123">[Integrate Azure Media Services OWIN MVC based app with Azure Active Directory and restrict content key delivery based on JWT claims](http://www.gtrifonov.com/2015/01/24/mvc-owin-azure-media-services-ad-integration/).</span></span>

<span data-ttu-id="4241b-124">[Używaj tokenów tooissue Azure ACS](http://mingfeiy.com/acs-with-key-services).</span><span class="sxs-lookup"><span data-stu-id="4241b-124">[Use Azure ACS tooissue tokens](http://mingfeiy.com/acs-with-key-services).</span></span>

### <a name="some-considerations-apply"></a><span data-ttu-id="4241b-125">Zagadnienia do rozważenia:</span><span class="sxs-lookup"><span data-stu-id="4241b-125">Some considerations apply:</span></span>
* <span data-ttu-id="4241b-126">Po utworzeniu konta usługi AMS **domyślne** punktu końcowego przesyłania strumieniowego w brzmieniu konta tooyour hello **zatrzymane** stanu.</span><span class="sxs-lookup"><span data-stu-id="4241b-126">When your AMS account is created a **default** streaming endpoint is added  tooyour account in hello **Stopped** state.</span></span> <span data-ttu-id="4241b-127">toostart przesyłania strumieniowego zawartości i podejmij korzyści z dynamicznego tworzenia pakietów i dynamicznego szyfrowania, punkt końcowy przesyłania strumieniowego ma toobe w hello **systemem** stanu.</span><span class="sxs-lookup"><span data-stu-id="4241b-127">toostart streaming your content and take advantage of dynamic packaging and dynamic encryption, your streaming endpoint has toobe in hello **Running** state.</span></span> 
* <span data-ttu-id="4241b-128">Zawartości musi zawierać zestaw o adaptacyjnej szybkości bitowej MP4s lub pliki Smooth Streaming adaptacyjną szybkością transmisji bitów.</span><span class="sxs-lookup"><span data-stu-id="4241b-128">Your asset must contain a set of adaptive bitrate MP4s or  adaptive bitrate Smooth Streaming files.</span></span> <span data-ttu-id="4241b-129">Aby uzyskać więcej informacji, zobacz [kodowanie elementu zawartości](media-services-encode-asset.md).</span><span class="sxs-lookup"><span data-stu-id="4241b-129">For more information, see [Encode an asset](media-services-encode-asset.md).</span></span>
* <span data-ttu-id="4241b-130">Przekazywanie i zasobów przy użyciu kodowania **AssetCreationOptions.StorageEncrypted** opcji.</span><span class="sxs-lookup"><span data-stu-id="4241b-130">Upload and encode your assets using **AssetCreationOptions.StorageEncrypted** option.</span></span>
* <span data-ttu-id="4241b-131">Jeśli planujesz toohave wiele kluczy zawartości, które wymagają hello sama konfiguracja zasad jest zdecydowanie zalecane toocreate zasad autoryzacji pojedynczego i użyć go ponownie wiele kluczy zawartości.</span><span class="sxs-lookup"><span data-stu-id="4241b-131">If you plan toohave multiple content keys that require hello same policy configuration, it is strongly recommended toocreate a single authorization policy and reuse it with multiple content keys.</span></span>
* <span data-ttu-id="4241b-132">Hello usługi dostarczania klucza buforuje ContentKeyAuthorizationPolicy i jego obiektów pokrewnych (opcje zasad i ograniczeń) przez 15 minut.</span><span class="sxs-lookup"><span data-stu-id="4241b-132">hello Key Delivery service caches ContentKeyAuthorizationPolicy and its related objects (policy options and restrictions) for 15 minutes.</span></span>  <span data-ttu-id="4241b-133">Jeśli tworzenie ContentKeyAuthorizationPolicy i określ toouse ograniczenie 'Token', a następnie ją przetestować, a następnie zaktualizuj zasad hello zbyt "Otwórz" ograniczeń, potrwa około 15 minut przed hello przełączniki toohello "Otwórz" Wersja zasad hello zasad.</span><span class="sxs-lookup"><span data-stu-id="4241b-133">If you create a ContentKeyAuthorizationPolicy and specify toouse a “Token” restriction, then test it, and then update hello policy too“Open” restriction, it will take roughly 15 minutes before hello policy switches toohello “Open” version of hello policy.</span></span>
* <span data-ttu-id="4241b-134">W przypadku dodania lub zaktualizowania zasad dostarczania elementów zawartości należy usunąć skojarzony lokalizator (jeśli istnieje) i utworzyć nowy.</span><span class="sxs-lookup"><span data-stu-id="4241b-134">If you add or update your asset’s delivery policy, you must delete an existing locator (if any) and create a new locator.</span></span>
* <span data-ttu-id="4241b-135">Obecnie nie można zaszyfrować pobierania progresywnego.</span><span class="sxs-lookup"><span data-stu-id="4241b-135">Currently, you cannot encrypt progressive downloads.</span></span>

## <a name="aes-128-dynamic-encryption"></a><span data-ttu-id="4241b-136">Dynamicznego szyfrowania AES-128</span><span class="sxs-lookup"><span data-stu-id="4241b-136">AES-128 Dynamic Encryption</span></span>
### <a name="open-restriction"></a><span data-ttu-id="4241b-137">Ograniczenie otwarte</span><span class="sxs-lookup"><span data-stu-id="4241b-137">Open Restriction</span></span>
<span data-ttu-id="4241b-138">Otwórz ograniczeń oznacza, że hello system będzie dostarczać hello tooanyone klucza, który wysyła żądanie klucza.</span><span class="sxs-lookup"><span data-stu-id="4241b-138">Open restriction means hello system will deliver hello key tooanyone who makes a key request.</span></span> <span data-ttu-id="4241b-139">To ograniczenie może być przydatna do celów testowych.</span><span class="sxs-lookup"><span data-stu-id="4241b-139">This restriction might be useful for testing purposes.</span></span>

<span data-ttu-id="4241b-140">Witaj poniższy przykład tworzy zasady autoryzacji otwarte i dodaje go toohello klucz zawartości.</span><span class="sxs-lookup"><span data-stu-id="4241b-140">hello following example creates an open authorization policy and adds it toohello content key.</span></span>

    static public void AddOpenAuthorizationPolicy(IContentKey contentKey)
    {
        // Create ContentKeyAuthorizationPolicy with Open restrictions
        // and create authorization policy
        IContentKeyAuthorizationPolicy policy = _context.
        ContentKeyAuthorizationPolicies.
        CreateAsync("Open Authorization Policy").Result;
        
        List<ContentKeyAuthorizationPolicyRestriction> restrictions =
            new List<ContentKeyAuthorizationPolicyRestriction>();

        ContentKeyAuthorizationPolicyRestriction restriction =
            new ContentKeyAuthorizationPolicyRestriction
            {
                Name = "HLS Open Authorization Policy",
                KeyRestrictionType = (int)ContentKeyRestrictionType.Open,
                Requirements = null // no requirements needed for HLS
            };

        restrictions.Add(restriction);

        IContentKeyAuthorizationPolicyOption policyOption =
            _context.ContentKeyAuthorizationPolicyOptions.Create(
            "policy", 
            ContentKeyDeliveryType.BaselineHttp, 
            restrictions, 
            "");

        policy.Options.Add(policyOption);

        // Add ContentKeyAutorizationPolicy tooContentKey
        contentKey.AuthorizationPolicyId = policy.Id;
        IContentKey updatedKey = contentKey.UpdateAsync().Result;
        Console.WriteLine("Adding Key tooAsset: Key ID is " + updatedKey.Id);
    }


### <a name="token-restriction"></a><span data-ttu-id="4241b-141">Ograniczenia tokenu</span><span class="sxs-lookup"><span data-stu-id="4241b-141">Token Restriction</span></span>
<span data-ttu-id="4241b-142">W tej sekcji opisano, jak toocreate zawartość zasady autoryzacji klucza i powiązać ją z hello klucz zawartości.</span><span class="sxs-lookup"><span data-stu-id="4241b-142">This section describes how toocreate a content key authorization policy and associate it with hello content key.</span></span> <span data-ttu-id="4241b-143">zasady autoryzacji Hello opisano, jakie wymagania autoryzacji musi być niespełnienia toodetermine, jeśli użytkownik hello jest autoryzowanym tooreceive hello klucza (na przykład, czy listy "klucz weryfikacji" hello zawiera klucz hello hello token została podpisana z).</span><span class="sxs-lookup"><span data-stu-id="4241b-143">hello authorization policy describes what authorization requirements must be met toodetermine if hello user is authorized tooreceive hello key (for example, does hello “verification key” list contain hello key that hello token was signed with).</span></span>

<span data-ttu-id="4241b-144">Opcja ograniczenia tokenu hello tooconfigure, należy toouse XML tokenu hello toodescribe wymagań autoryzacji.</span><span class="sxs-lookup"><span data-stu-id="4241b-144">tooconfigure hello token restriction option, you need toouse an XML toodescribe hello token’s authorization requirements.</span></span> <span data-ttu-id="4241b-145">plik XML konfiguracji ograniczenia tokenu Hello muszą być zgodne toohello następującego schematu XML.</span><span class="sxs-lookup"><span data-stu-id="4241b-145">hello token restriction configuration XML must conform toohello following XML schema.</span></span>

#### <span data-ttu-id="4241b-146"><a id="schema"></a>Ograniczenia tokenu schematu</span><span class="sxs-lookup"><span data-stu-id="4241b-146"><a id="schema"></a>Token restriction schema</span></span>
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

<span data-ttu-id="4241b-147">Podczas konfigurowania hello **tokenu** ograniczone zasad, należy określić hello podstawowy ** weryfikacji klucza **, **wystawcy** i **odbiorców** parametrów.</span><span class="sxs-lookup"><span data-stu-id="4241b-147">When configuring hello **token** restricted policy, you must specify hello primary** verification key**, **issuer** and **audience** parameters.</span></span> <span data-ttu-id="4241b-148">Witaj ** klucza podstawowego weryfikacji ** zawiera klucz hello hello token został podpisany, **wystawcy** jest usługa bezpiecznego tokenu hello token hello problemy.</span><span class="sxs-lookup"><span data-stu-id="4241b-148">hello **primary verification key **contains hello key that hello token was signed with, **issuer** is hello secure token service that issues hello token.</span></span> <span data-ttu-id="4241b-149">Witaj **odbiorców** (nazywane **zakresu**) opisuje zamierzone hello hello token lub zasobu hello hello tokenu zezwala na dostęp do.</span><span class="sxs-lookup"><span data-stu-id="4241b-149">hello **audience** (sometimes called **scope**) describes hello intent of hello token or hello resource hello token authorizes access to.</span></span> <span data-ttu-id="4241b-150">Hello usługa Media Services klucza dostawy weryfikuje, czy te wartości w tokenie hello są takie same wartości hello hello szablonu.</span><span class="sxs-lookup"><span data-stu-id="4241b-150">hello Media Services key delivery service validates that these values in hello token match hello values in hello template.</span></span> 

<span data-ttu-id="4241b-151">Korzystając z **SDK usługi Media Services dla platformy .NET**, można użyć hello **TokenRestrictionTemplate** klasy toogenerate hello ograniczenie tokenu.</span><span class="sxs-lookup"><span data-stu-id="4241b-151">When using **Media Services SDK for .NET**, you can use hello **TokenRestrictionTemplate** class toogenerate hello restriction token.</span></span>
<span data-ttu-id="4241b-152">Witaj poniższy przykład tworzy zasady autoryzacji z ograniczenia tokenu.</span><span class="sxs-lookup"><span data-stu-id="4241b-152">hello following example creates an authorization policy with a token restriction.</span></span> <span data-ttu-id="4241b-153">W tym przykładzie powitania klienta byłyby toopresent token, który zawiera: podpisywanie klucz (VerificationKey), wystawcy tokenów i oświadczeń wymagane.</span><span class="sxs-lookup"><span data-stu-id="4241b-153">In this example, hello client would have toopresent a token that contains: signing key (VerificationKey), a token issuer, and required claims.</span></span>

    public static string AddTokenRestrictedAuthorizationPolicy(IContentKey contentKey)
    {
        string tokenTemplateString = GenerateTokenRequirements();

        IContentKeyAuthorizationPolicy policy = _context.
                                ContentKeyAuthorizationPolicies.
                                CreateAsync("HLS token restricted authorization policy").Result;

        List<ContentKeyAuthorizationPolicyRestriction> restrictions =
                new List<ContentKeyAuthorizationPolicyRestriction>();

        ContentKeyAuthorizationPolicyRestriction restriction =
                new ContentKeyAuthorizationPolicyRestriction
                {
                    Name = "Token Authorization Policy",
                    KeyRestrictionType = (int)ContentKeyRestrictionType.TokenRestricted,
                    Requirements = tokenTemplateString
                };

        restrictions.Add(restriction);

        //You could have multiple options 
        IContentKeyAuthorizationPolicyOption policyOption =
            _context.ContentKeyAuthorizationPolicyOptions.Create(
                "Token option for HLS",
                ContentKeyDeliveryType.BaselineHttp,
                restrictions,
                null  // no key delivery data is needed for HLS
                );

        policy.Options.Add(policyOption);

        // Add ContentKeyAutorizationPolicy tooContentKey
        contentKey.AuthorizationPolicyId = policy.Id;
        IContentKey updatedKey = contentKey.UpdateAsync().Result;
        Console.WriteLine("Adding Key tooAsset: Key ID is " + updatedKey.Id);

        return tokenTemplateString;
    }

    static private string GenerateTokenRequirements()
    {
        TokenRestrictionTemplate template = new TokenRestrictionTemplate(TokenType.SWT);

        template.PrimaryVerificationKey = new SymmetricVerificationKey();
        template.AlternateVerificationKeys.Add(new SymmetricVerificationKey());
            template.Audience = _sampleAudience.ToString();
            template.Issuer = _sampleIssuer.ToString();

        template.RequiredClaims.Add(TokenClaim.ContentKeyIdentifierClaim);

        return TokenRestrictionTemplateSerializer.Serialize(template);
    }

#### <span data-ttu-id="4241b-154"><a id="test"></a>Test tokenu</span><span class="sxs-lookup"><span data-stu-id="4241b-154"><a id="test"></a>Test token</span></span>
<span data-ttu-id="4241b-155">tooget token testu oparte na powitania ograniczenia tokenu użytego dla zasady autoryzacji klucza hello, hello następujące.</span><span class="sxs-lookup"><span data-stu-id="4241b-155">tooget a test token based on hello token restriction that was used for hello key authorization policy, do hello following.</span></span>

    // Deserializes a string containing an Xml representation of a TokenRestrictionTemplate
    // back into a TokenRestrictionTemplate class instance.
    TokenRestrictionTemplate tokenTemplate =
        TokenRestrictionTemplateSerializer.Deserialize(tokenTemplateString);

    // Generate a test token based on hello hello data in hello given TokenRestrictionTemplate.
    // Note, you need toopass hello key id Guid because we specified 
    // TokenClaim.ContentKeyIdentifierClaim in during hello creation of TokenRestrictionTemplate.
    Guid rawkey = EncryptionUtils.GetKeyIdAsGuid(key.Id);

    //hello GenerateTestToken method returns hello token without hello word “Bearer” in front
    //so you have tooadd it in front of hello token string. 
    string testToken = TokenRestrictionTemplateSerializer.GenerateTestToken(tokenTemplate, null, rawkey);
    Console.WriteLine("hello authorization token is:\nBearer {0}", testToken);
    Console.WriteLine();


## <a name="playready-dynamic-encryption"></a><span data-ttu-id="4241b-156">Szyfrowanie PlayReady dynamiczne</span><span class="sxs-lookup"><span data-stu-id="4241b-156">PlayReady Dynamic Encryption</span></span>
<span data-ttu-id="4241b-157">Usługi Media Services umożliwia tooconfigure hello prawa i ograniczenia, które mają dla hello tooenforce środowiska uruchomieniowego PlayReady DRM, gdy użytkownik próbuje się, że tooplay ponownie chronionej zawartości.</span><span class="sxs-lookup"><span data-stu-id="4241b-157">Media Services enables you tooconfigure hello rights and restrictions that you want for hello PlayReady DRM runtime tooenforce when a user is trying tooplay back protected content.</span></span> 

<span data-ttu-id="4241b-158">W przypadku ochrony zawartości przy użyciu PlayReady, z hello czynności należy toospecify w zasadach autoryzacji jest ciąg XML, który definiuje hello [szablon licencji PlayReady](media-services-playready-license-template-overview.md).</span><span class="sxs-lookup"><span data-stu-id="4241b-158">When protecting your content with PlayReady, one of hello things you need toospecify in your authorization policy is an XML string that defines hello [PlayReady license template](media-services-playready-license-template-overview.md).</span></span> <span data-ttu-id="4241b-159">W zestawie SDK usługi multimediów dla platformy .NET, hello **PlayReadyLicenseResponseTemplate** i **PlayReadyLicenseTemplate** klasy zawierają informacje pomocne podczas definiowania szablonu licencji PlayReady hello.</span><span class="sxs-lookup"><span data-stu-id="4241b-159">In Media Services SDK for .NET, hello **PlayReadyLicenseResponseTemplate** and **PlayReadyLicenseTemplate** classes will help you define hello PlayReady License Template.</span></span>

<span data-ttu-id="4241b-160">[W tym temacie](media-services-protect-with-drm.md) przedstawia sposób tooencrypt zawartości przy użyciu **PlayReady** i **Widevine**.</span><span class="sxs-lookup"><span data-stu-id="4241b-160">[This topic](media-services-protect-with-drm.md) shows how tooencrypt your content with **PlayReady** and **Widevine**.</span></span>

### <a name="open-restriction"></a><span data-ttu-id="4241b-161">Ograniczenie otwarte</span><span class="sxs-lookup"><span data-stu-id="4241b-161">Open Restriction</span></span>
<span data-ttu-id="4241b-162">Otwórz ograniczeń oznacza, że hello system będzie dostarczać hello tooanyone klucza, który wysyła żądanie klucza.</span><span class="sxs-lookup"><span data-stu-id="4241b-162">Open restriction means hello system will deliver hello key tooanyone who makes a key request.</span></span> <span data-ttu-id="4241b-163">To ograniczenie może być przydatna do celów testowych.</span><span class="sxs-lookup"><span data-stu-id="4241b-163">This restriction might be useful for testing purposes.</span></span>

<span data-ttu-id="4241b-164">Witaj poniższy przykład tworzy zasady autoryzacji otwarte i dodaje go toohello klucz zawartości.</span><span class="sxs-lookup"><span data-stu-id="4241b-164">hello following example creates an open authorization policy and adds it toohello content key.</span></span>

    static public void AddOpenAuthorizationPolicy(IContentKey contentKey)
    {

        // Create ContentKeyAuthorizationPolicy with Open restrictions 
        // and create authorization policy          

        List<ContentKeyAuthorizationPolicyRestriction> restrictions = new List<ContentKeyAuthorizationPolicyRestriction>
        {
            new ContentKeyAuthorizationPolicyRestriction 
            { 
                Name = "Open", 
                KeyRestrictionType = (int)ContentKeyRestrictionType.Open, 
                Requirements = null
            }
        };

        // Configure PlayReady license template.
        string newLicenseTemplate = ConfigurePlayReadyLicenseTemplate();

        IContentKeyAuthorizationPolicyOption policyOption =
            _context.ContentKeyAuthorizationPolicyOptions.Create("",
                ContentKeyDeliveryType.PlayReadyLicense,
                    restrictions, newLicenseTemplate);

        IContentKeyAuthorizationPolicy contentKeyAuthorizationPolicy = _context.
                    ContentKeyAuthorizationPolicies.
                    CreateAsync("Deliver Common Content Key with no restrictions").
                    Result;


        contentKeyAuthorizationPolicy.Options.Add(policyOption);

        // Associate hello content key authorization policy with hello content key.
        contentKey.AuthorizationPolicyId = contentKeyAuthorizationPolicy.Id;
        contentKey = contentKey.UpdateAsync().Result;
    }

### <a name="token-restriction"></a><span data-ttu-id="4241b-165">Ograniczenia tokenu</span><span class="sxs-lookup"><span data-stu-id="4241b-165">Token Restriction</span></span>
<span data-ttu-id="4241b-166">Opcja ograniczenia tokenu hello tooconfigure, należy toouse XML tokenu hello toodescribe wymagań autoryzacji.</span><span class="sxs-lookup"><span data-stu-id="4241b-166">tooconfigure hello token restriction option, you need toouse an XML toodescribe hello token’s authorization requirements.</span></span> <span data-ttu-id="4241b-167">plik XML konfiguracji ograniczenia tokenu Hello musi być zgodna schematu XML toohello wyświetlany w [to](#schema) sekcji.</span><span class="sxs-lookup"><span data-stu-id="4241b-167">hello token restriction configuration XML must conform toohello XML schema shown in [this](#schema) section.</span></span>

    public static string AddTokenRestrictedAuthorizationPolicy(IContentKey contentKey)
    {
        string tokenTemplateString = GenerateTokenRequirements();

        IContentKeyAuthorizationPolicy policy = _context.
                                ContentKeyAuthorizationPolicies.
                                CreateAsync("HLS token restricted authorization policy").Result;

        List<ContentKeyAuthorizationPolicyRestriction> restrictions = new List<ContentKeyAuthorizationPolicyRestriction>
        {
            new ContentKeyAuthorizationPolicyRestriction 
            { 
                Name = "Token Authorization Policy", 
                KeyRestrictionType = (int)ContentKeyRestrictionType.TokenRestricted,
                Requirements = tokenTemplateString, 
            }
        };

        // Configure PlayReady license template.
        string newLicenseTemplate = ConfigurePlayReadyLicenseTemplate();

        IContentKeyAuthorizationPolicyOption policyOption =
            _context.ContentKeyAuthorizationPolicyOptions.Create("Token option",
                ContentKeyDeliveryType.PlayReadyLicense,
                    restrictions, newLicenseTemplate);

        IContentKeyAuthorizationPolicy contentKeyAuthorizationPolicy = _context.
                    ContentKeyAuthorizationPolicies.
                    CreateAsync("Deliver Common Content Key with no restrictions").
                    Result;

        policy.Options.Add(policyOption);

        // Add ContentKeyAutorizationPolicy tooContentKey
        contentKeyAuthorizationPolicy.Options.Add(policyOption);

        // Associate hello content key authorization policy with hello content key
        contentKey.AuthorizationPolicyId = contentKeyAuthorizationPolicy.Id;
        contentKey = contentKey.UpdateAsync().Result;

        return tokenTemplateString;
    }

    static private string GenerateTokenRequirements()
    {

        TokenRestrictionTemplate template = new TokenRestrictionTemplate(TokenType.SWT);

        template.PrimaryVerificationKey = new SymmetricVerificationKey();
        template.AlternateVerificationKeys.Add(new SymmetricVerificationKey());
            template.Audience = _sampleAudience.ToString();
            template.Issuer = _sampleIssuer.ToString();


        template.RequiredClaims.Add(TokenClaim.ContentKeyIdentifierClaim);

        return TokenRestrictionTemplateSerializer.Serialize(template);
    } 

    static private string ConfigurePlayReadyLicenseTemplate()
    {
        // hello following code configures PlayReady License Template using .NET classes
        // and returns hello XML string.

        //hello PlayReadyLicenseResponseTemplate class represents hello template for hello response sent back toohello end user. 
        //It contains a field for a custom data string between hello license server and hello application 
        //(may be useful for custom app logic) as well as a list of one or more license templates.
        PlayReadyLicenseResponseTemplate responseTemplate = new PlayReadyLicenseResponseTemplate();

        // hello PlayReadyLicenseTemplate class represents a license template for creating PlayReady licenses
        // toobe returned toohello end users. 
        //It contains hello data on hello content key in hello license and any rights or restrictions toobe 
        //enforced by hello PlayReady DRM runtime when using hello content key.
        PlayReadyLicenseTemplate licenseTemplate = new PlayReadyLicenseTemplate();
        //Configure whether hello license is persistent (saved in persistent storage on hello client) 
        //or non-persistent (only held in memory while hello player is using hello license).  
        licenseTemplate.LicenseType = PlayReadyLicenseType.Nonpersistent;

        // AllowTestDevices controls whether test devices can use hello license or not.  
        // If true, hello MinimumSecurityLevel property of hello license
        // is set too150.  If false (hello default), hello MinimumSecurityLevel property of hello license is set too2000.
        licenseTemplate.AllowTestDevices = true;


        // You can also configure hello Play Right in hello PlayReady license by using hello PlayReadyPlayRight class. 
        // It grants hello user hello ability tooplayback hello content subject toohello zero or more restrictions 
        // configured in hello license and on hello PlayRight itself (for playback specific policy). 
        // Much of hello policy on hello PlayRight has toodo with output restrictions 
        // which control hello types of outputs that hello content can be played over and 
        // any restrictions that must be put in place when using a given output.
        // For example, if hello DigitalVideoOnlyContentRestriction is enabled, 
        //then hello DRM runtime will only allow hello video toobe displayed over digital outputs 
        //(analog video outputs won’t be allowed toopass hello content).

        //IMPORTANT: These types of restrictions can be very powerful but can also affect hello consumer experience. 
        // If hello output protections are configured too restrictive, 
        // hello content might be unplayable on some clients. For more information, see hello PlayReady Compliance Rules document.

        // For example:
        //licenseTemplate.PlayRight.AgcAndColorStripeRestriction = new AgcAndColorStripeRestriction(1);

        responseTemplate.LicenseTemplates.Add(licenseTemplate);

        return MediaServicesLicenseTemplateSerializer.Serialize(responseTemplate);
    }


<span data-ttu-id="4241b-168">test tokenu na hello ograniczenia tokenu, którego użyto do Zobacz zasady autoryzacji klucza hello tooget [to](#test) sekcji.</span><span class="sxs-lookup"><span data-stu-id="4241b-168">tooget a test token based on hello token restriction that was used for hello key authorization policy see [this](#test) section.</span></span> 

## <span data-ttu-id="4241b-169"><a id="types"></a>Typy używane podczas definiowania ContentKeyAuthorizationPolicy</span><span class="sxs-lookup"><span data-stu-id="4241b-169"><a id="types"></a>Types used when defining ContentKeyAuthorizationPolicy</span></span>
### <span data-ttu-id="4241b-170"><a id="ContentKeyRestrictionType"></a>ContentKeyRestrictionType</span><span class="sxs-lookup"><span data-stu-id="4241b-170"><a id="ContentKeyRestrictionType"></a>ContentKeyRestrictionType</span></span>
    public enum ContentKeyRestrictionType
    {
        Open = 0,
        TokenRestricted = 1,
        IPRestricted = 2,
    }

### <span data-ttu-id="4241b-171"><a id="ContentKeyDeliveryType"></a>ContentKeyDeliveryType</span><span class="sxs-lookup"><span data-stu-id="4241b-171"><a id="ContentKeyDeliveryType"></a>ContentKeyDeliveryType</span></span>
    public enum ContentKeyDeliveryType
    {
      None = 0,
      PlayReadyLicense = 1,
      BaselineHttp = 2,
      Widevine = 3
    }

### <span data-ttu-id="4241b-172"><a id="TokenType"></a>TokenType</span><span class="sxs-lookup"><span data-stu-id="4241b-172"><a id="TokenType"></a>TokenType</span></span>
    public enum TokenType
    {
        Undefined = 0,
        SWT = 1,
        JWT = 2,
    }



## <a name="media-services-learning-paths"></a><span data-ttu-id="4241b-173">Ścieżki szkoleniowe dotyczące usługi Media Services</span><span class="sxs-lookup"><span data-stu-id="4241b-173">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="4241b-174">Przekazywanie opinii</span><span class="sxs-lookup"><span data-stu-id="4241b-174">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="next-step"></a><span data-ttu-id="4241b-175">Następny krok</span><span class="sxs-lookup"><span data-stu-id="4241b-175">Next step</span></span>
<span data-ttu-id="4241b-176">Teraz, gdy skonfigurowano zasady autoryzacji klucza zawartości, przejdź toohello [jak zasady dostarczania elementu zawartości tooconfigure](media-services-dotnet-configure-asset-delivery-policy.md) tematu.</span><span class="sxs-lookup"><span data-stu-id="4241b-176">Now that you have configured content key's authorization policy, go toohello [How tooconfigure asset delivery policy](media-services-dotnet-configure-asset-delivery-policy.md) topic.</span></span>

