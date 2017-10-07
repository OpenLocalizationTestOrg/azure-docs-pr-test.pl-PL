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
# <a name="configure-asset-delivery-policies-with-net-sdk"></a><span data-ttu-id="d6cf3-103">Skonfiguruj zasady dostarczania zasobów przy użyciu zestawu .NET SDK</span><span class="sxs-lookup"><span data-stu-id="d6cf3-103">Configure asset delivery policies with .NET SDK</span></span>
[!INCLUDE [media-services-selector-asset-delivery-policy](../../includes/media-services-selector-asset-delivery-policy.md)]

## <a name="overview"></a><span data-ttu-id="d6cf3-104">Omówienie</span><span class="sxs-lookup"><span data-stu-id="d6cf3-104">Overview</span></span>
<span data-ttu-id="d6cf3-105">Jeśli planujesz trwałych toodelivery zaszyfrowane, jeden z hello kroków w hello zawartości dostarczania przepływu pracy jest konfigurowanie zasad dostarczania dla zasobów usługi Media Services.</span><span class="sxs-lookup"><span data-stu-id="d6cf3-105">If you plan toodelivery encrypted assets, one of hello steps in hello Media Services content delivery workflow is configuring delivery policies for assets.</span></span> <span data-ttu-id="d6cf3-106">zasady dostarczania elementu zawartości Hello informuje usługi Media Services sposób dla Twojego toobe zasobów dostarczyć: w przypadku protokołu przesyłania strumieniowego powinno zawartości dynamicznie umieszczone (na przykład, MPEG DASH, HLS, Smooth Streaming lub wszystkie), czy chcesz toodynamically szyfrowanie zawartości i w jaki sposób (koperty lub szyfrowania common encryption).</span><span class="sxs-lookup"><span data-stu-id="d6cf3-106">hello asset delivery policy tells Media Services how you want for your asset toobe delivered: into which streaming protocol should your asset be dynamically packaged (for example, MPEG DASH, HLS, Smooth Streaming, or all), whether or not you want toodynamically encrypt your asset and how (envelope or common encryption).</span></span>

<span data-ttu-id="d6cf3-107">W tym temacie omówiono dlaczego i w jaki sposób toocreate i skonfigurować zasady dostarczania zasobów.</span><span class="sxs-lookup"><span data-stu-id="d6cf3-107">This topic discusses why and how toocreate and configure asset delivery policies.</span></span>

>[!NOTE]
><span data-ttu-id="d6cf3-108">Po utworzeniu konta usługi AMS **domyślne** punktu końcowego przesyłania strumieniowego w brzmieniu konta tooyour hello **zatrzymane** stanu.</span><span class="sxs-lookup"><span data-stu-id="d6cf3-108">When your AMS account is created a **default** streaming endpoint is added tooyour account in hello **Stopped** state.</span></span> <span data-ttu-id="d6cf3-109">przesyłanie strumieniowe zawartości i podejmij korzyści z dynamicznego tworzenia pakietów i dynamicznego szyfrowania toostart hello punktu końcowego przesyłania strumieniowego, z którego mają zostać toostream zawartość ma toobe w hello **systemem** stanu.</span><span class="sxs-lookup"><span data-stu-id="d6cf3-109">toostart streaming your content and take advantage of dynamic packaging and dynamic encryption, hello streaming endpoint from which you want toostream content has toobe in hello **Running** state.</span></span> 
>
><span data-ttu-id="d6cf3-110">Ponadto toobe toouse stanie dynamicznego tworzenia pakietów i dynamicznego szyfrowania zawartości musi zawierać zestaw o adaptacyjnej szybkości bitowej MP4s lub pliki Smooth Streaming adaptacyjną szybkością transmisji bitów.</span><span class="sxs-lookup"><span data-stu-id="d6cf3-110">Also, toobe able toouse dynamic packaging and dynamic encryption your asset must contain a set of adaptive bitrate MP4s or adaptive bitrate Smooth Streaming files.</span></span>


<span data-ttu-id="d6cf3-111">Toohello różnych zasad można zastosować elementu zawartości.</span><span class="sxs-lookup"><span data-stu-id="d6cf3-111">You could apply different policies toohello same asset.</span></span> <span data-ttu-id="d6cf3-112">Na przykład można zastosować PlayReady szyfrowania tooSmooth przesyłania strumieniowego i szyfrowanie AES Envelope szyfrowania tooMPEG kreska i HLS.</span><span class="sxs-lookup"><span data-stu-id="d6cf3-112">For example, you could apply PlayReady encryption tooSmooth Streaming and AES Envelope encryption tooMPEG DASH and HLS.</span></span> <span data-ttu-id="d6cf3-113">Wszystkie protokoły, które nie są zdefiniowane w zasadzie dostarczania (na przykład dodać jedną zasadę, która tylko określa hello protokół HLS), zostanie zablokowany przesyłania strumieniowego.</span><span class="sxs-lookup"><span data-stu-id="d6cf3-113">Any protocols that are not defined in a delivery policy (for example, you add a single policy that only specifies HLS as hello protocol) will be blocked from streaming.</span></span> <span data-ttu-id="d6cf3-114">toothis wyjątek Hello jest, jeśli masz nie zdefiniowano zasad dostarczania elementów zawartości.</span><span class="sxs-lookup"><span data-stu-id="d6cf3-114">hello exception toothis is if you have no asset delivery policy defined at all.</span></span> <span data-ttu-id="d6cf3-115">Następnie wszystkie protokoły mogą być przesyłane hello Wyczyść.</span><span class="sxs-lookup"><span data-stu-id="d6cf3-115">Then, all protocols will be allowed in hello clear.</span></span>

<span data-ttu-id="d6cf3-116">Chcąc toodeliver zasób zaszyfrowanych magazynu, należy skonfigurować zasady dostarczania zasobów hello.</span><span class="sxs-lookup"><span data-stu-id="d6cf3-116">If you want toodeliver a storage encrypted asset, you must configure hello asset’s delivery policy.</span></span> <span data-ttu-id="d6cf3-117">Przed zawartości mogą być przesyłane strumieniowo, hello i przesyłania strumieniowego szyfrowania magazynu hello usuwa strumieni zawartości przy użyciu hello określone zasady dostarczania.</span><span class="sxs-lookup"><span data-stu-id="d6cf3-117">Before your asset can be streamed, hello streaming server removes hello storage encryption and streams your content using hello specified delivery policy.</span></span> <span data-ttu-id="d6cf3-118">Na przykład toodeliver zawartości zaszyfrowane za pomocą klucza szyfrowania koperty Advanced Encryption (Standard AES), Ustaw typ zasad hello zbyt**DynamicEnvelopeEncryption**.</span><span class="sxs-lookup"><span data-stu-id="d6cf3-118">For example, toodeliver your asset encrypted with Advanced Encryption Standard (AES) envelope encryption key, set hello policy type too**DynamicEnvelopeEncryption**.</span></span> <span data-ttu-id="d6cf3-119">szyfrowanie magazynu tooremove i zasobów hello strumienia w hello Wyczyść, Ustaw typ zasad hello zbyt**NoDynamicEncryption**.</span><span class="sxs-lookup"><span data-stu-id="d6cf3-119">tooremove storage encryption and stream hello asset in hello clear, set hello policy type too**NoDynamicEncryption**.</span></span> <span data-ttu-id="d6cf3-120">Przykłady, które pokazują, jak tooconfigure tych typów zasad należy wykonać.</span><span class="sxs-lookup"><span data-stu-id="d6cf3-120">Examples that show how tooconfigure these policy types follow.</span></span>

<span data-ttu-id="d6cf3-121">W zależności od konfiguracji zasad dostarczania elementów zawartości hello czy pakietu toodynamically może być dynamicznie szyfrowania i strumienia powitania po protokołów przesyłania strumieniowego: Smooth Streaming, HLS i MPEG DASH strumieni.</span><span class="sxs-lookup"><span data-stu-id="d6cf3-121">Depending on how you configure hello asset delivery policy you would be able toodynamically package, dynamically encrypt, and stream hello following streaming protocols: Smooth Streaming, HLS, and MPEG DASH streams.</span></span>

<span data-ttu-id="d6cf3-122">Witaj Poniższa lista zawiera formaty hello używasz toostream Smooth, HLS i KRESKI.</span><span class="sxs-lookup"><span data-stu-id="d6cf3-122">hello following list shows hello formats that you use toostream Smooth, HLS, and DASH.</span></span>

<span data-ttu-id="d6cf3-123">Funkcje Smooth Streaming:</span><span class="sxs-lookup"><span data-stu-id="d6cf3-123">Smooth Streaming:</span></span>

<span data-ttu-id="d6cf3-124">{nazwa punktu końcowego przesyłania strumieniowego-nazwa konta usługi Media Services}.streaming.mediaservices.windows.net/{identyfikator lokalizatora}/{nazwa pliku}.ism/Manifest</span><span class="sxs-lookup"><span data-stu-id="d6cf3-124">{streaming endpoint name-media services account name}.streaming.mediaservices.windows.net/{locator ID}/{filename}.ism/Manifest</span></span>

<span data-ttu-id="d6cf3-125">HLS:</span><span class="sxs-lookup"><span data-stu-id="d6cf3-125">HLS:</span></span>

<span data-ttu-id="d6cf3-126">{name}.streaming.mediaservices.windows.net/{locator konta usługi media Nazwa punktu końcowego ID}/{filename}.ism/Manifest(format=m3u8-aapl) przesyłania strumieniowego</span><span class="sxs-lookup"><span data-stu-id="d6cf3-126">{streaming endpoint name-media services account name}.streaming.mediaservices.windows.net/{locator ID}/{filename}.ism/Manifest(format=m3u8-aapl)</span></span>

<span data-ttu-id="d6cf3-127">MPEG DASH</span><span class="sxs-lookup"><span data-stu-id="d6cf3-127">MPEG DASH</span></span>

<span data-ttu-id="d6cf3-128">{name}.streaming.mediaservices.windows.net/{locator konta usługi media Nazwa punktu końcowego ID}/{filename}.ism/Manifest(format=mpd-time-csf) przesyłania strumieniowego</span><span class="sxs-lookup"><span data-stu-id="d6cf3-128">{streaming endpoint name-media services account name}.streaming.mediaservices.windows.net/{locator ID}/{filename}.ism/Manifest(format=mpd-time-csf)</span></span>


## <a name="considerations"></a><span data-ttu-id="d6cf3-129">Zagadnienia do rozważenia</span><span class="sxs-lookup"><span data-stu-id="d6cf3-129">Considerations</span></span>
* <span data-ttu-id="d6cf3-130">Nie można usunąć AssetDeliveryPolicy skojarzone z zasobów, gdy Lokalizator OnDemand (streaming) istnieje dla tego zasobu.</span><span class="sxs-lookup"><span data-stu-id="d6cf3-130">You cannot delete an AssetDeliveryPolicy associated with an asset while an OnDemand (streaming) locator exists for that asset.</span></span> <span data-ttu-id="d6cf3-131">zalecenie Hello jest tooremove hello zasady z zasobu hello przed usunięciem hello zasad.</span><span class="sxs-lookup"><span data-stu-id="d6cf3-131">hello recommendation is tooremove hello policy from hello asset before deleting hello policy.</span></span>
* <span data-ttu-id="d6cf3-132">Nie można utworzyć Lokalizator przesyłania strumieniowego magazynu trwałego zaszyfrowane, jeśli ustawiono nie zasad dostarczania elementów zawartości.</span><span class="sxs-lookup"><span data-stu-id="d6cf3-132">A streaming locator cannot be created on a storage encrypted asset when no asset delivery policy is set.</span></span>  <span data-ttu-id="d6cf3-133">Jeśli hello zasobów nie jest szyfrowany w magazynie, hello system umożliwi utworzyć lokalizator i strumień zasobów hello w hello wyczyść bez zasad dostarczania elementów zawartości.</span><span class="sxs-lookup"><span data-stu-id="d6cf3-133">If hello Asset isn’t storage encrypted, hello system will let you create a locator and stream hello asset in hello clear without an asset delivery policy.</span></span>
* <span data-ttu-id="d6cf3-134">Może mieć wiele zasady dostarczania zasobów skojarzonych z pojedynczego zasobu, ale można określić tylko jednokierunkowe toohandle AssetDeliveryProtocol danego.</span><span class="sxs-lookup"><span data-stu-id="d6cf3-134">You can have multiple asset delivery policies associated with a single asset but you can only specify one way toohandle a given AssetDeliveryProtocol.</span></span>  <span data-ttu-id="d6cf3-135">Co oznacza, Jeśli spróbujesz toolink dwóch dostarczania zasad określających hello AssetDeliveryProtocol.SmoothStreaming protokół, który spowoduje błąd, ponieważ hello system nie może określić, która z nich ma tooapply gdy klient przesyła żądanie Smooth Streaming.</span><span class="sxs-lookup"><span data-stu-id="d6cf3-135">Meaning if you try toolink two delivery policies that specify hello AssetDeliveryProtocol.SmoothStreaming protocol that will result in an error because hello system does not know which one you want it tooapply when a client makes a Smooth Streaming request.</span></span>
* <span data-ttu-id="d6cf3-136">Jeśli zasób z istniejących Lokalizator przesyłania strumieniowego, nie możesz połączyć nowy trwały toohello zasad (możesz odłączyć istniejące zasady z zasobu hello, lub zaktualizowania zasad dostarczania skojarzone z hello zasobów).</span><span class="sxs-lookup"><span data-stu-id="d6cf3-136">If you have an asset with an existing streaming locator, you cannot link a new policy toohello asset (you can either unlink an existing policy from hello asset, or update a delivery policy associated with hello asset).</span></span>  <span data-ttu-id="d6cf3-137">Najpierw ma Lokalizator przesyłania strumieniowego hello tooremove, Dostosuj zasady hello i ponownie utwórz hello przesyłania strumieniowego lokalizatora.</span><span class="sxs-lookup"><span data-stu-id="d6cf3-137">You first have tooremove hello streaming locator, adjust hello policies, and then re-create hello streaming locator.</span></span>  <span data-ttu-id="d6cf3-138">Możesz użyć powitalne tego samego locatorId podczas ponownego tworzenia hello przesyłania strumieniowego lokalizatora, ale powinien zapewnić, że nie będzie powodować problemy dla klientów, ponieważ zawartości mogą być buforowane pochodzenia hello lub podrzędne CDN.</span><span class="sxs-lookup"><span data-stu-id="d6cf3-138">You can use hello same locatorId when you recreate hello streaming locator but you should ensure that won’t cause issues for clients since content can be cached by hello origin or a downstream CDN.</span></span>

## <a name="clear-asset-delivery-policy"></a><span data-ttu-id="d6cf3-139">Zasady dostarczania elementu zawartości wyczyść</span><span class="sxs-lookup"><span data-stu-id="d6cf3-139">Clear asset delivery policy</span></span>

<span data-ttu-id="d6cf3-140">następujące Hello **ConfigureClearAssetDeliveryPolicy** metody określa toonot zastosowanie szyfrowania dynamicznego i toodeliver hello strumienia w żadnym hello następujące protokoły: MPEG DASH, HLS i Smooth Streaming protokołów.</span><span class="sxs-lookup"><span data-stu-id="d6cf3-140">hello following **ConfigureClearAssetDeliveryPolicy** method specifies toonot apply dynamic encryption and toodeliver hello stream in any of hello following protocols:  MPEG DASH, HLS, and Smooth Streaming protocols.</span></span> <span data-ttu-id="d6cf3-141">Możesz tooapply zasoby szyfrowany w magazynie tooyour tej zasady.</span><span class="sxs-lookup"><span data-stu-id="d6cf3-141">You might want tooapply this policy tooyour storage encrypted assets.</span></span>

<span data-ttu-id="d6cf3-142">Informacje o jakie wartości można określić podczas tworzenia AssetDeliveryPolicy, zobacz hello [typów używanych podczas definiowania AssetDeliveryPolicy](#types) sekcji.</span><span class="sxs-lookup"><span data-stu-id="d6cf3-142">For information on what values you can specify when creating an AssetDeliveryPolicy, see hello [Types used when defining AssetDeliveryPolicy](#types) section.</span></span>

    static public void ConfigureClearAssetDeliveryPolicy(IAsset asset)
    {
        IAssetDeliveryPolicy policy =
        _context.AssetDeliveryPolicies.Create("Clear Policy",
        AssetDeliveryPolicyType.NoDynamicEncryption,
        AssetDeliveryProtocol.HLS | AssetDeliveryProtocol.SmoothStreaming | AssetDeliveryProtocol.Dash, null);
        
        asset.DeliveryPolicies.Add(policy);
    }

## <a name="dynamiccommonencryption-asset-delivery-policy"></a><span data-ttu-id="d6cf3-143">Zasady dostarczania elementu zawartości DynamicCommonEncryption</span><span class="sxs-lookup"><span data-stu-id="d6cf3-143">DynamicCommonEncryption asset delivery policy</span></span>

<span data-ttu-id="d6cf3-144">następujące Hello **CreateAssetDeliveryPolicy** metoda tworzy hello **AssetDeliveryPolicy** który jest skonfigurowany tooapply dynamicznego szyfrowania common encryption (**DynamicCommonEncryption**) tooa smooth streaming protocol (inne protokoły będzie blokowany przesyłania strumieniowego).</span><span class="sxs-lookup"><span data-stu-id="d6cf3-144">hello following **CreateAssetDeliveryPolicy** method creates hello **AssetDeliveryPolicy** that is configured tooapply dynamic common encryption (**DynamicCommonEncryption**) tooa smooth streaming protocol (other protocols will be blocked from streaming).</span></span> <span data-ttu-id="d6cf3-145">Metoda Hello przyjmuje dwa parametry: **zasobów** (hello toowhich zasobów ma zasady dostarczania hello tooapply) i **IContentKey** (klucz zawartości hello hello **CommonEncryption**typu, aby uzyskać więcej informacji, zobacz: [Tworzenie klucza zawartości](media-services-dotnet-create-contentkey.md#common_contentkey)).</span><span class="sxs-lookup"><span data-stu-id="d6cf3-145">hello method takes two parameters : **Asset** (hello asset toowhich you want tooapply hello delivery policy) and **IContentKey** (hello content key of hello **CommonEncryption** type, for more information, see: [Creating a content key](media-services-dotnet-create-contentkey.md#common_contentkey)).</span></span>

<span data-ttu-id="d6cf3-146">Informacje o jakie wartości można określić podczas tworzenia AssetDeliveryPolicy, zobacz hello [typów używanych podczas definiowania AssetDeliveryPolicy](#types) sekcji.</span><span class="sxs-lookup"><span data-stu-id="d6cf3-146">For information on what values you can specify when creating an AssetDeliveryPolicy, see hello [Types used when defining AssetDeliveryPolicy](#types) section.</span></span>

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

<span data-ttu-id="d6cf3-147">Usługa Azure Media Services umożliwia również tooadd Widevine szyfrowania.</span><span class="sxs-lookup"><span data-stu-id="d6cf3-147">Azure Media Services also enables you tooadd Widevine encryption.</span></span> <span data-ttu-id="d6cf3-148">Witaj poniższym przykładzie pokazano zarówno PlayReady i Widevine dodawany zasad dostarczania elementów zawartości toohello.</span><span class="sxs-lookup"><span data-stu-id="d6cf3-148">hello following example demonstrates both PlayReady and Widevine being added toohello asset delivery policy.</span></span>

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
> <span data-ttu-id="d6cf3-149">W przypadku szyfrowania przy użyciu metody Widevine, tylko będzie możliwe toodeliver przy użyciu kreska.</span><span class="sxs-lookup"><span data-stu-id="d6cf3-149">When encrypting with Widevine, you would only be able toodeliver using DASH.</span></span> <span data-ttu-id="d6cf3-150">Upewnij się, że toospecify DASH w Protokół dostarczania elementów zawartości hello.</span><span class="sxs-lookup"><span data-stu-id="d6cf3-150">Make sure toospecify DASH in hello asset delivery protocol.</span></span>
> 
> 

## <a name="dynamicenvelopeencryption-asset-delivery-policy"></a><span data-ttu-id="d6cf3-151">Zasady dostarczania elementu zawartości DynamicEnvelopeEncryption</span><span class="sxs-lookup"><span data-stu-id="d6cf3-151">DynamicEnvelopeEncryption asset delivery policy</span></span>
<span data-ttu-id="d6cf3-152">następujące Hello **CreateAssetDeliveryPolicy** metoda tworzy hello **AssetDeliveryPolicy** będący szyfrowania dynamicznego koperty tooapply skonfigurowany (**DynamicEnvelopeEncryption** ) tooSmooth protokołów przesyłania strumieniowego, HLS i KRESKI (Jeśli zdecydujesz się toonot Określ niektóre protokoły, będzie można korzystać z przesyłania strumieniowego).</span><span class="sxs-lookup"><span data-stu-id="d6cf3-152">hello following **CreateAssetDeliveryPolicy** method creates hello **AssetDeliveryPolicy** that is configured tooapply dynamic envelope encryption (**DynamicEnvelopeEncryption**) tooSmooth Streaming, HLS, and DASH protocols (if you decide toonot specify some protocols, they will be blocked from streaming).</span></span> <span data-ttu-id="d6cf3-153">Metoda Hello przyjmuje dwa parametry: **zasobów** (hello toowhich zasobów ma zasady dostarczania hello tooapply) i **IContentKey** (klucz zawartości hello hello **EnvelopeEncryption**typu, aby uzyskać więcej informacji, zobacz: [Tworzenie klucza zawartości](media-services-dotnet-create-contentkey.md#envelope_contentkey)).</span><span class="sxs-lookup"><span data-stu-id="d6cf3-153">hello method takes two parameters : **Asset** (hello asset toowhich you want tooapply hello delivery policy) and **IContentKey** (hello content key of hello **EnvelopeEncryption** type, for more information, see: [Creating a content key](media-services-dotnet-create-contentkey.md#envelope_contentkey)).</span></span>

<span data-ttu-id="d6cf3-154">Informacje o jakie wartości można określić podczas tworzenia AssetDeliveryPolicy, zobacz hello [typów używanych podczas definiowania AssetDeliveryPolicy](#types) sekcji.</span><span class="sxs-lookup"><span data-stu-id="d6cf3-154">For information on what values you can specify when creating an AssetDeliveryPolicy, see hello [Types used when defining AssetDeliveryPolicy](#types) section.</span></span>   

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


## <span data-ttu-id="d6cf3-155"><a id="types"></a>Typy używane podczas definiowania AssetDeliveryPolicy</span><span class="sxs-lookup"><span data-stu-id="d6cf3-155"><a id="types"></a>Types used when defining AssetDeliveryPolicy</span></span>

### <span data-ttu-id="d6cf3-156"><a id="AssetDeliveryProtocol"></a>AssetDeliveryProtocol</span><span class="sxs-lookup"><span data-stu-id="d6cf3-156"><a id="AssetDeliveryProtocol"></a>AssetDeliveryProtocol</span></span>

<span data-ttu-id="d6cf3-157">Witaj następujące wyliczenia opisano wartości ustawione przez protokół dostarczania elementów zawartości hello.</span><span class="sxs-lookup"><span data-stu-id="d6cf3-157">hello following enum describes values you can set for hello asset delivery protocol.</span></span>

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

### <span data-ttu-id="d6cf3-158"><a id="AssetDeliveryPolicyType"></a>AssetDeliveryPolicyType</span><span class="sxs-lookup"><span data-stu-id="d6cf3-158"><a id="AssetDeliveryPolicyType"></a>AssetDeliveryPolicyType</span></span>

<span data-ttu-id="d6cf3-159">Witaj następujące wyliczenia opisano wartości, które można ustawić dla typu zasady dostarczania elementu zawartości hello.</span><span class="sxs-lookup"><span data-stu-id="d6cf3-159">hello following enum describes values you can set for hello asset delivery policy type.</span></span>  

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

### <span data-ttu-id="d6cf3-160"><a id="ContentKeyDeliveryType"></a>ContentKeyDeliveryType</span><span class="sxs-lookup"><span data-stu-id="d6cf3-160"><a id="ContentKeyDeliveryType"></a>ContentKeyDeliveryType</span></span>

<span data-ttu-id="d6cf3-161">Witaj następujące wyliczenia opisano wartości można użyć metody dostarczania hello tooconfigure powitania klienta toohello klucza zawartości.</span><span class="sxs-lookup"><span data-stu-id="d6cf3-161">hello following enum describes values you can use tooconfigure hello delivery method of hello content key toohello client.</span></span>
    
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

### <span data-ttu-id="d6cf3-162"><a id="AssetDeliveryPolicyConfigurationKey"></a>AssetDeliveryPolicyConfigurationKey</span><span class="sxs-lookup"><span data-stu-id="d6cf3-162"><a id="AssetDeliveryPolicyConfigurationKey"></a>AssetDeliveryPolicyConfigurationKey</span></span>

<span data-ttu-id="d6cf3-163">powitania po wyliczenia opisano wartości, które można ustawić określonej konfiguracji tooget tooconfigure klucze używane dla zasad dostarczania elementów zawartości.</span><span class="sxs-lookup"><span data-stu-id="d6cf3-163">hello following enum describes values you can set tooconfigure keys used tooget specific configuration for an asset delivery policy.</span></span>

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

## <a name="media-services-learning-paths"></a><span data-ttu-id="d6cf3-164">Ścieżki szkoleniowe dotyczące usługi Media Services</span><span class="sxs-lookup"><span data-stu-id="d6cf3-164">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="d6cf3-165">Przekazywanie opinii</span><span class="sxs-lookup"><span data-stu-id="d6cf3-165">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

