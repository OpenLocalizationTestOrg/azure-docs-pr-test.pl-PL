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
# <a name="dynamic-encryption-configure-content-key-authorization-policy"></a>Szyfrowania dynamicznego: Skonfiguruj zasady autoryzacji klucza zawartości
[!INCLUDE [media-services-selector-content-key-auth-policy](../../includes/media-services-selector-content-key-auth-policy.md)]

## <a name="overview"></a>Omówienie
Microsoft Azure Media Services umożliwia toodeliver MPEG-DASH, Smooth Streaming i strumieni HTTP-Live-Streaming (HLS) chronionych przy Standard AES (Advanced Encryption) (przy użyciu kluczy szyfrowania 128-bitowego) lub [Microsoft PlayReady DRM](https://www.microsoft.com/playready/overview/). AMS umożliwia również należy toodeliver strumienie DASH korzystających zaszyfrowane za pomocą Widevine DRM. Zarówno PlayReady i Widevine są szyfrowane na powitania specyfikacją Common Encryption (ISO/IEC CENC 23001-7).

Media Services udostępnia również **usługi dostarczania licencji/klucz** z których klienci mogą uzyskać kluczy AES lub tooplay licencji PlayReady/Widevine hello zaszyfrowaną zawartość.

Jeśli chcesz dla usługi Media Services tooencrypt zasób, należy tooassociate klucza szyfrowania (**CommonEncryption** lub **EnvelopeEncryption**) z zasobów hello (zgodnie z opisem [tutaj](media-services-dotnet-create-contentkey.md)) a także skonfigurować zasady autoryzacji klucza hello (zgodnie z opisem w tym artykule).

Gdy odtwarzacza zażąda strumienia, usługa Media Services używa hello określony toodynamically klucza szyfrowania zawartości przy użyciu szyfrowania AES lub DRM. toodecrypt hello strumienia, hello odtwarzacza zażąda hello klucza z usługi dostarczania klucza hello. toodecide czy hello użytkownik jest autoryzowany tooget hello klucza, usługi hello ocenia zasady autoryzacji hello określonych hello klucza.

Usługa Media Services obsługuje wiele sposobów uwierzytelniania użytkowników, którzy tworzą żądania klucza. Witaj zasady autoryzacji klucza zawartości może mieć jeden lub więcej ograniczeń: **Otwórz** lub **tokenu** ograniczeń. Witaj zasadzie ograniczenia tokenu musi towarzyszyć token wystawiony przez Secure Token Service (STS). Usługa Media Services obsługuje tokenów w hello **proste tokenów sieci Web** ([SWT](https://msdn.microsoft.com/library/gg185950.aspx#BKMK_2)) format i **JSON Web Token** ([JWT](https://msdn.microsoft.com/library/gg185950.aspx#BKMK_3)) format.

Usługi Media Services nie zapewnia bezpieczny tokenu usługi. Można utworzyć niestandardowy STS lub korzystać z usługi Microsoft Azure ACS tooissue tokenów. Witaj STS musi być skonfigurowany toocreate podpisany token z określonym kluczem hello i wystawiających oświadczenia, określona w konfiguracji ograniczenia tokenu hello (zgodnie z opisem w tym artykule). Witaj usługa Media Services klucza dostawy zwróci klienta toohello klucza szyfrowania hello Jeśli hello token jest prawidłowy i hello oświadczenia w tokenie hello pasują hello klucza zawartości.

Aby uzyskać więcej informacji, zobacz

[Uwierzytelniania tokenu JWT](http://www.gtrifonov.com/2015/01/03/jwt-token-authentication-in-azure-media-services-and-dynamic-encryption/)

[Integracja aplikacji na podstawie Azure Media Services OWIN MVC z usługi Azure Active Directory i ograniczenie klucza dostarczania zawartości na podstawie oświadczeń JWT](http://www.gtrifonov.com/2015/01/24/mvc-owin-azure-media-services-ad-integration/).

[Używaj tokenów tooissue Azure ACS](http://mingfeiy.com/acs-with-key-services).

### <a name="some-considerations-apply"></a>Zagadnienia do rozważenia:
* Po utworzeniu konta usługi AMS **domyślne** punktu końcowego przesyłania strumieniowego w brzmieniu konta tooyour hello **zatrzymane** stanu. toostart przesyłania strumieniowego zawartości i podejmij korzyści z dynamicznego tworzenia pakietów i dynamicznego szyfrowania, punkt końcowy przesyłania strumieniowego ma toobe w hello **systemem** stanu. 
* Zawartości musi zawierać zestaw o adaptacyjnej szybkości bitowej MP4s lub pliki Smooth Streaming adaptacyjną szybkością transmisji bitów. Aby uzyskać więcej informacji, zobacz [kodowanie elementu zawartości](media-services-encode-asset.md).
* Przekazywanie i zasobów przy użyciu kodowania **AssetCreationOptions.StorageEncrypted** opcji.
* Jeśli planujesz toohave wiele kluczy zawartości, które wymagają hello sama konfiguracja zasad jest zdecydowanie zalecane toocreate zasad autoryzacji pojedynczego i użyć go ponownie wiele kluczy zawartości.
* Hello usługi dostarczania klucza buforuje ContentKeyAuthorizationPolicy i jego obiektów pokrewnych (opcje zasad i ograniczeń) przez 15 minut.  Jeśli tworzenie ContentKeyAuthorizationPolicy i określ toouse ograniczenie 'Token', a następnie ją przetestować, a następnie zaktualizuj zasad hello zbyt "Otwórz" ograniczeń, potrwa około 15 minut przed hello przełączniki toohello "Otwórz" Wersja zasad hello zasad.
* W przypadku dodania lub zaktualizowania zasad dostarczania elementów zawartości należy usunąć skojarzony lokalizator (jeśli istnieje) i utworzyć nowy.
* Obecnie nie można zaszyfrować pobierania progresywnego.

## <a name="aes-128-dynamic-encryption"></a>Dynamicznego szyfrowania AES-128
### <a name="open-restriction"></a>Ograniczenie otwarte
Otwórz ograniczeń oznacza, że hello system będzie dostarczać hello tooanyone klucza, który wysyła żądanie klucza. To ograniczenie może być przydatna do celów testowych.

Witaj poniższy przykład tworzy zasady autoryzacji otwarte i dodaje go toohello klucz zawartości.

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


### <a name="token-restriction"></a>Ograniczenia tokenu
W tej sekcji opisano, jak toocreate zawartość zasady autoryzacji klucza i powiązać ją z hello klucz zawartości. zasady autoryzacji Hello opisano, jakie wymagania autoryzacji musi być niespełnienia toodetermine, jeśli użytkownik hello jest autoryzowanym tooreceive hello klucza (na przykład, czy listy "klucz weryfikacji" hello zawiera klucz hello hello token została podpisana z).

Opcja ograniczenia tokenu hello tooconfigure, należy toouse XML tokenu hello toodescribe wymagań autoryzacji. plik XML konfiguracji ograniczenia tokenu Hello muszą być zgodne toohello następującego schematu XML.

#### <a id="schema"></a>Ograniczenia tokenu schematu
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

Podczas konfigurowania hello **tokenu** ograniczone zasad, należy określić hello podstawowy ** weryfikacji klucza **, **wystawcy** i **odbiorców** parametrów. Witaj ** klucza podstawowego weryfikacji ** zawiera klucz hello hello token został podpisany, **wystawcy** jest usługa bezpiecznego tokenu hello token hello problemy. Witaj **odbiorców** (nazywane **zakresu**) opisuje zamierzone hello hello token lub zasobu hello hello tokenu zezwala na dostęp do. Hello usługa Media Services klucza dostawy weryfikuje, czy te wartości w tokenie hello są takie same wartości hello hello szablonu. 

Korzystając z **SDK usługi Media Services dla platformy .NET**, można użyć hello **TokenRestrictionTemplate** klasy toogenerate hello ograniczenie tokenu.
Witaj poniższy przykład tworzy zasady autoryzacji z ograniczenia tokenu. W tym przykładzie powitania klienta byłyby toopresent token, który zawiera: podpisywanie klucz (VerificationKey), wystawcy tokenów i oświadczeń wymagane.

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

#### <a id="test"></a>Test tokenu
tooget token testu oparte na powitania ograniczenia tokenu użytego dla zasady autoryzacji klucza hello, hello następujące.

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


## <a name="playready-dynamic-encryption"></a>Szyfrowanie PlayReady dynamiczne
Usługi Media Services umożliwia tooconfigure hello prawa i ograniczenia, które mają dla hello tooenforce środowiska uruchomieniowego PlayReady DRM, gdy użytkownik próbuje się, że tooplay ponownie chronionej zawartości. 

W przypadku ochrony zawartości przy użyciu PlayReady, z hello czynności należy toospecify w zasadach autoryzacji jest ciąg XML, który definiuje hello [szablon licencji PlayReady](media-services-playready-license-template-overview.md). W zestawie SDK usługi multimediów dla platformy .NET, hello **PlayReadyLicenseResponseTemplate** i **PlayReadyLicenseTemplate** klasy zawierają informacje pomocne podczas definiowania szablonu licencji PlayReady hello.

[W tym temacie](media-services-protect-with-drm.md) przedstawia sposób tooencrypt zawartości przy użyciu **PlayReady** i **Widevine**.

### <a name="open-restriction"></a>Ograniczenie otwarte
Otwórz ograniczeń oznacza, że hello system będzie dostarczać hello tooanyone klucza, który wysyła żądanie klucza. To ograniczenie może być przydatna do celów testowych.

Witaj poniższy przykład tworzy zasady autoryzacji otwarte i dodaje go toohello klucz zawartości.

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

### <a name="token-restriction"></a>Ograniczenia tokenu
Opcja ograniczenia tokenu hello tooconfigure, należy toouse XML tokenu hello toodescribe wymagań autoryzacji. plik XML konfiguracji ograniczenia tokenu Hello musi być zgodna schematu XML toohello wyświetlany w [to](#schema) sekcji.

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


test tokenu na hello ograniczenia tokenu, którego użyto do Zobacz zasady autoryzacji klucza hello tooget [to](#test) sekcji. 

## <a id="types"></a>Typy używane podczas definiowania ContentKeyAuthorizationPolicy
### <a id="ContentKeyRestrictionType"></a>ContentKeyRestrictionType
    public enum ContentKeyRestrictionType
    {
        Open = 0,
        TokenRestricted = 1,
        IPRestricted = 2,
    }

### <a id="ContentKeyDeliveryType"></a>ContentKeyDeliveryType
    public enum ContentKeyDeliveryType
    {
      None = 0,
      PlayReadyLicense = 1,
      BaselineHttp = 2,
      Widevine = 3
    }

### <a id="TokenType"></a>TokenType
    public enum TokenType
    {
        Undefined = 0,
        SWT = 1,
        JWT = 2,
    }



## <a name="media-services-learning-paths"></a>Ścieżki szkoleniowe dotyczące usługi Media Services
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Przekazywanie opinii
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="next-step"></a>Następny krok
Teraz, gdy skonfigurowano zasady autoryzacji klucza zawartości, przejdź toohello [jak zasady dostarczania elementu zawartości tooconfigure](media-services-dotnet-configure-asset-delivery-policy.md) tematu.

