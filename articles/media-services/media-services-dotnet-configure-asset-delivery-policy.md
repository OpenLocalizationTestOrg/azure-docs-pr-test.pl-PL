---
title: "zasady dostarczania zasobów aaaConfigure przy użyciu zestawu .NET SDK | Dokumentacja firmy Microsoft"
description: "W tym temacie przedstawiono sposób zasady dostarczania zasobów różnych tooconfigure z zestawu .NET SDK usługi Azure Media Services."
services: media-services
documentationcenter: 
author: Mingfeiy
manager: cfowler
editor: 
ms.assetid: 3ec46f58-6cbb-4d49-bac6-1fd01a5a456b
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 07/13/2017
ms.author: juliako;mingfeiy
ms.openlocfilehash: a6f2644d639cd36d4cdc269b6f01fd4acdf7160b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="configure-asset-delivery-policies-with-net-sdk"></a>Skonfiguruj zasady dostarczania zasobów przy użyciu zestawu .NET SDK
[!INCLUDE [media-services-selector-asset-delivery-policy](../../includes/media-services-selector-asset-delivery-policy.md)]

## <a name="overview"></a>Omówienie
Jeśli planujesz trwałych toodelivery zaszyfrowane, jeden z hello kroków w hello zawartości dostarczania przepływu pracy jest konfigurowanie zasad dostarczania dla zasobów usługi Media Services. zasady dostarczania elementu zawartości Hello informuje usługi Media Services sposób dla Twojego toobe zasobów dostarczyć: w przypadku protokołu przesyłania strumieniowego powinno zawartości dynamicznie umieszczone (na przykład, MPEG DASH, HLS, Smooth Streaming lub wszystkie), czy chcesz toodynamically szyfrowanie zawartości i w jaki sposób (koperty lub szyfrowania common encryption).

W tym temacie omówiono dlaczego i w jaki sposób toocreate i skonfigurować zasady dostarczania zasobów.

>[!NOTE]
>Po utworzeniu konta usługi AMS **domyślne** punktu końcowego przesyłania strumieniowego w brzmieniu konta tooyour hello **zatrzymane** stanu. przesyłanie strumieniowe zawartości i podejmij korzyści z dynamicznego tworzenia pakietów i dynamicznego szyfrowania toostart hello punktu końcowego przesyłania strumieniowego, z którego mają zostać toostream zawartość ma toobe w hello **systemem** stanu. 
>
>Ponadto toobe toouse stanie dynamicznego tworzenia pakietów i dynamicznego szyfrowania zawartości musi zawierać zestaw o adaptacyjnej szybkości bitowej MP4s lub pliki Smooth Streaming adaptacyjną szybkością transmisji bitów.


Toohello różnych zasad można zastosować elementu zawartości. Na przykład można zastosować PlayReady szyfrowania tooSmooth przesyłania strumieniowego i szyfrowanie AES Envelope szyfrowania tooMPEG kreska i HLS. Wszystkie protokoły, które nie są zdefiniowane w zasadzie dostarczania (na przykład dodać jedną zasadę, która tylko określa hello protokół HLS), zostanie zablokowany przesyłania strumieniowego. toothis wyjątek Hello jest, jeśli masz nie zdefiniowano zasad dostarczania elementów zawartości. Następnie wszystkie protokoły mogą być przesyłane hello Wyczyść.

Chcąc toodeliver zasób zaszyfrowanych magazynu, należy skonfigurować zasady dostarczania zasobów hello. Przed zawartości mogą być przesyłane strumieniowo, hello i przesyłania strumieniowego szyfrowania magazynu hello usuwa strumieni zawartości przy użyciu hello określone zasady dostarczania. Na przykład toodeliver zawartości zaszyfrowane za pomocą klucza szyfrowania koperty Advanced Encryption (Standard AES), Ustaw typ zasad hello zbyt**DynamicEnvelopeEncryption**. szyfrowanie magazynu tooremove i zasobów hello strumienia w hello Wyczyść, Ustaw typ zasad hello zbyt**NoDynamicEncryption**. Przykłady, które pokazują, jak tooconfigure tych typów zasad należy wykonać.

W zależności od konfiguracji zasad dostarczania elementów zawartości hello czy pakietu toodynamically może być dynamicznie szyfrowania i strumienia powitania po protokołów przesyłania strumieniowego: Smooth Streaming, HLS i MPEG DASH strumieni.

Witaj Poniższa lista zawiera formaty hello używasz toostream Smooth, HLS i KRESKI.

Funkcje Smooth Streaming:

{nazwa punktu końcowego przesyłania strumieniowego-nazwa konta usługi Media Services}.streaming.mediaservices.windows.net/{identyfikator lokalizatora}/{nazwa pliku}.ism/Manifest

HLS:

{name}.streaming.mediaservices.windows.net/{locator konta usługi media Nazwa punktu końcowego ID}/{filename}.ism/Manifest(format=m3u8-aapl) przesyłania strumieniowego

MPEG DASH

{name}.streaming.mediaservices.windows.net/{locator konta usługi media Nazwa punktu końcowego ID}/{filename}.ism/Manifest(format=mpd-time-csf) przesyłania strumieniowego


## <a name="considerations"></a>Zagadnienia do rozważenia
* Nie można usunąć AssetDeliveryPolicy skojarzone z zasobów, gdy Lokalizator OnDemand (streaming) istnieje dla tego zasobu. zalecenie Hello jest tooremove hello zasady z zasobu hello przed usunięciem hello zasad.
* Nie można utworzyć Lokalizator przesyłania strumieniowego magazynu trwałego zaszyfrowane, jeśli ustawiono nie zasad dostarczania elementów zawartości.  Jeśli hello zasobów nie jest szyfrowany w magazynie, hello system umożliwi utworzyć lokalizator i strumień zasobów hello w hello wyczyść bez zasad dostarczania elementów zawartości.
* Może mieć wiele zasady dostarczania zasobów skojarzonych z pojedynczego zasobu, ale można określić tylko jednokierunkowe toohandle AssetDeliveryProtocol danego.  Co oznacza, Jeśli spróbujesz toolink dwóch dostarczania zasad określających hello AssetDeliveryProtocol.SmoothStreaming protokół, który spowoduje błąd, ponieważ hello system nie może określić, która z nich ma tooapply gdy klient przesyła żądanie Smooth Streaming.
* Jeśli zasób z istniejących Lokalizator przesyłania strumieniowego, nie możesz połączyć nowy trwały toohello zasad (możesz odłączyć istniejące zasady z zasobu hello, lub zaktualizowania zasad dostarczania skojarzone z hello zasobów).  Najpierw ma Lokalizator przesyłania strumieniowego hello tooremove, Dostosuj zasady hello i ponownie utwórz hello przesyłania strumieniowego lokalizatora.  Możesz użyć powitalne tego samego locatorId podczas ponownego tworzenia hello przesyłania strumieniowego lokalizatora, ale powinien zapewnić, że nie będzie powodować problemy dla klientów, ponieważ zawartości mogą być buforowane pochodzenia hello lub podrzędne CDN.

## <a name="clear-asset-delivery-policy"></a>Zasady dostarczania elementu zawartości wyczyść

następujące Hello **ConfigureClearAssetDeliveryPolicy** metody określa toonot zastosowanie szyfrowania dynamicznego i toodeliver hello strumienia w żadnym hello następujące protokoły: MPEG DASH, HLS i Smooth Streaming protokołów. Możesz tooapply zasoby szyfrowany w magazynie tooyour tej zasady.

Informacje o jakie wartości można określić podczas tworzenia AssetDeliveryPolicy, zobacz hello [typów używanych podczas definiowania AssetDeliveryPolicy](#types) sekcji.

    static public void ConfigureClearAssetDeliveryPolicy(IAsset asset)
    {
        IAssetDeliveryPolicy policy =
        _context.AssetDeliveryPolicies.Create("Clear Policy",
        AssetDeliveryPolicyType.NoDynamicEncryption,
        AssetDeliveryProtocol.HLS | AssetDeliveryProtocol.SmoothStreaming | AssetDeliveryProtocol.Dash, null);
        
        asset.DeliveryPolicies.Add(policy);
    }

## <a name="dynamiccommonencryption-asset-delivery-policy"></a>Zasady dostarczania elementu zawartości DynamicCommonEncryption

następujące Hello **CreateAssetDeliveryPolicy** metoda tworzy hello **AssetDeliveryPolicy** który jest skonfigurowany tooapply dynamicznego szyfrowania common encryption (**DynamicCommonEncryption**) tooa smooth streaming protocol (inne protokoły będzie blokowany przesyłania strumieniowego). Metoda Hello przyjmuje dwa parametry: **zasobów** (hello toowhich zasobów ma zasady dostarczania hello tooapply) i **IContentKey** (klucz zawartości hello hello **CommonEncryption**typu, aby uzyskać więcej informacji, zobacz: [Tworzenie klucza zawartości](media-services-dotnet-create-contentkey.md#common_contentkey)).

Informacje o jakie wartości można określić podczas tworzenia AssetDeliveryPolicy, zobacz hello [typów używanych podczas definiowania AssetDeliveryPolicy](#types) sekcji.

    static public void CreateAssetDeliveryPolicy(IAsset asset, IContentKey key)
    {
        Uri acquisitionUrl = key.GetKeyDeliveryUrl(ContentKeyDeliveryType.PlayReadyLicense);
        
        Dictionary<AssetDeliveryPolicyConfigurationKey, string> assetDeliveryPolicyConfiguration =
                new Dictionary<AssetDeliveryPolicyConfigurationKey, string>
            {
                {AssetDeliveryPolicyConfigurationKey.PlayReadyLicenseAcquisitionUrl, acquisitionUrl.ToString()},
            };
    
            var assetDeliveryPolicy = _context.AssetDeliveryPolicies.Create(
                    "AssetDeliveryPolicy",
                AssetDeliveryPolicyType.DynamicCommonEncryption,
                AssetDeliveryProtocol.SmoothStreaming,
                assetDeliveryPolicyConfiguration);
    
            // Add AssetDelivery Policy toohello asset
            asset.DeliveryPolicies.Add(assetDeliveryPolicy);
    
            Console.WriteLine();
            Console.WriteLine("Adding Asset Delivery Policy: " +
                assetDeliveryPolicy.AssetDeliveryPolicyType);
     }

Usługa Azure Media Services umożliwia również tooadd Widevine szyfrowania. Witaj poniższym przykładzie pokazano zarówno PlayReady i Widevine dodawany zasad dostarczania elementów zawartości toohello.

    static public void CreateAssetDeliveryPolicy(IAsset asset, IContentKey key)
    {
        // Get hello PlayReady license service URL.
        Uri acquisitionUrl = key.GetKeyDeliveryUrl(ContentKeyDeliveryType.PlayReadyLicense);


        // GetKeyDeliveryUrl for Widevine attaches hello KID toohello URL.
        // For example: https://amsaccount1.keydelivery.mediaservices.windows.net/Widevine/?KID=268a6dcb-18c8-4648-8c95-f46429e4927c.  
        // hello WidevineBaseLicenseAcquisitionUrl (used below) also tells Dynamaic Encryption 
        // tooappend /? KID =< keyId > toohello end of hello url when creating hello manifest.
        // As a result Widevine license acquisition URL will have KID appended twice, 
        // so we need tooremove hello KID that in hello URL when we call GetKeyDeliveryUrl.

        Uri widevineUrl = key.GetKeyDeliveryUrl(ContentKeyDeliveryType.Widevine);
        UriBuilder uriBuilder = new UriBuilder(widevineUrl);
        uriBuilder.Query = String.Empty;
        widevineUrl = uriBuilder.Uri;

        Dictionary<AssetDeliveryPolicyConfigurationKey, string> assetDeliveryPolicyConfiguration =
            new Dictionary<AssetDeliveryPolicyConfigurationKey, string>
        {
            {AssetDeliveryPolicyConfigurationKey.PlayReadyLicenseAcquisitionUrl, acquisitionUrl.ToString()},
            {AssetDeliveryPolicyConfigurationKey.WidevineLicenseAcquisitionUrl, widevineUrl.ToString()}

        };

        var assetDeliveryPolicy = _context.AssetDeliveryPolicies.Create(
                "AssetDeliveryPolicy",
            AssetDeliveryPolicyType.DynamicCommonEncryption,
            AssetDeliveryProtocol.Dash,
            assetDeliveryPolicyConfiguration);


        // Add AssetDelivery Policy toohello asset
        asset.DeliveryPolicies.Add(assetDeliveryPolicy);

    }

> [!NOTE]
> W przypadku szyfrowania przy użyciu metody Widevine, tylko będzie możliwe toodeliver przy użyciu kreska. Upewnij się, że toospecify DASH w Protokół dostarczania elementów zawartości hello.
> 
> 

## <a name="dynamicenvelopeencryption-asset-delivery-policy"></a>Zasady dostarczania elementu zawartości DynamicEnvelopeEncryption
następujące Hello **CreateAssetDeliveryPolicy** metoda tworzy hello **AssetDeliveryPolicy** będący szyfrowania dynamicznego koperty tooapply skonfigurowany (**DynamicEnvelopeEncryption** ) tooSmooth protokołów przesyłania strumieniowego, HLS i KRESKI (Jeśli zdecydujesz się toonot Określ niektóre protokoły, będzie można korzystać z przesyłania strumieniowego). Metoda Hello przyjmuje dwa parametry: **zasobów** (hello toowhich zasobów ma zasady dostarczania hello tooapply) i **IContentKey** (klucz zawartości hello hello **EnvelopeEncryption**typu, aby uzyskać więcej informacji, zobacz: [Tworzenie klucza zawartości](media-services-dotnet-create-contentkey.md#envelope_contentkey)).

Informacje o jakie wartości można określić podczas tworzenia AssetDeliveryPolicy, zobacz hello [typów używanych podczas definiowania AssetDeliveryPolicy](#types) sekcji.   

    private static void CreateAssetDeliveryPolicy(IAsset asset, IContentKey key)
    {

        //  Get hello Key Delivery Base Url by removing hello Query parameter.  hello Dynamic Encryption service will
        //  automatically add hello correct key identifier toohello url when it generates hello Envelope encrypted content
        //  manifest.  Omitting hello IV will also cause hello Dynamice Encryption service toogenerate a deterministic
        //  IV for hello content automatically.  By using hello EnvelopeBaseKeyAcquisitionUrl and omitting hello IV, this
        //  allows hello AssetDelivery policy toobe reused by more than one asset.
        //
        Uri keyAcquisitionUri = key.GetKeyDeliveryUrl(ContentKeyDeliveryType.BaselineHttp);
        UriBuilder uriBuilder = new UriBuilder(keyAcquisitionUri);
        uriBuilder.Query = String.Empty;
        keyAcquisitionUri = uriBuilder.Uri;

        // hello following policy configuration specifies: 
        //   key url that will have KID=<Guid> appended toohello envelope and
        //   hello Initialization Vector (IV) toouse for hello envelope encryption.
        Dictionary<AssetDeliveryPolicyConfigurationKey, string> assetDeliveryPolicyConfiguration =
            new Dictionary<AssetDeliveryPolicyConfigurationKey, string> 
        {
            {AssetDeliveryPolicyConfigurationKey.EnvelopeBaseKeyAcquisitionUrl, keyAcquisitionUri.ToString()},
        };

        IAssetDeliveryPolicy assetDeliveryPolicy =
            _context.AssetDeliveryPolicies.Create(
                        "AssetDeliveryPolicy",
                        AssetDeliveryPolicyType.DynamicEnvelopeEncryption,
                        AssetDeliveryProtocol.SmoothStreaming | AssetDeliveryProtocol.HLS | AssetDeliveryProtocol.Dash,
                        assetDeliveryPolicyConfiguration);

        // Add AssetDelivery Policy toohello asset
        asset.DeliveryPolicies.Add(assetDeliveryPolicy);

        Console.WriteLine();
        Console.WriteLine("Adding Asset Delivery Policy: " + assetDeliveryPolicy.AssetDeliveryPolicyType);
    }


## <a id="types"></a>Typy używane podczas definiowania AssetDeliveryPolicy

### <a id="AssetDeliveryProtocol"></a>AssetDeliveryProtocol

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

### <a id="AssetDeliveryPolicyType"></a>AssetDeliveryPolicyType

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

### <a id="ContentKeyDeliveryType"></a>ContentKeyDeliveryType

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

### <a id="AssetDeliveryPolicyConfigurationKey"></a>AssetDeliveryPolicyConfigurationKey

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

