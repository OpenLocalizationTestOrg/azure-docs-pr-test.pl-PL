---
title: "Skonfiguruj zasady dostarczania zasobów przy użyciu zestawu .NET SDK | Dokumentacja firmy Microsoft"
description: "W tym temacie pokazano, jak skonfigurować zasady dostarczania różnych zasobów z zestawu .NET SDK usługi Azure Media Services."
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
ms.openlocfilehash: 282fd9e24dc147e31613469926128894d48366f4
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
# <a name="configure-asset-delivery-policies-with-net-sdk"></a><span data-ttu-id="7d2a2-103">Skonfiguruj zasady dostarczania zasobów przy użyciu zestawu .NET SDK</span><span class="sxs-lookup"><span data-stu-id="7d2a2-103">Configure asset delivery policies with .NET SDK</span></span>
[!INCLUDE [media-services-selector-asset-delivery-policy](../../includes/media-services-selector-asset-delivery-policy.md)]

## <a name="overview"></a><span data-ttu-id="7d2a2-104">Omówienie</span><span class="sxs-lookup"><span data-stu-id="7d2a2-104">Overview</span></span>
<span data-ttu-id="7d2a2-105">Jeśli planujesz trwałych dostarczania zaszyfrowane, jeden z kroków w przepływie pracy dostarczania zawartości Media Services konfiguruje zasady dostarczania zasobów.</span><span class="sxs-lookup"><span data-stu-id="7d2a2-105">If you plan to delivery encrypted assets, one of the steps in the Media Services content delivery workflow is configuring delivery policies for assets.</span></span> <span data-ttu-id="7d2a2-106">Zasady dostarczania elementu zawartości informuje usługi Media Services sposób dla zawartości dostarczanej: w których przesyłania strumieniowego protokołu powinna zawartości dynamicznie umieszczone (na przykład, MPEG DASH, HLS, Smooth Streaming lub wszystkie), czy ma być dynamicznego szyfrowania zawartości i w jaki sposób (koperty lub szyfrowania common encryption).</span><span class="sxs-lookup"><span data-stu-id="7d2a2-106">The asset delivery policy tells Media Services how you want for your asset to be delivered: into which streaming protocol should your asset be dynamically packaged (for example, MPEG DASH, HLS, Smooth Streaming, or all), whether or not you want to dynamically encrypt your asset and how (envelope or common encryption).</span></span>

<span data-ttu-id="7d2a2-107">W tym temacie omówiono dlaczego i jak utworzyć i skonfigurować zasady dostarczania zasobów.</span><span class="sxs-lookup"><span data-stu-id="7d2a2-107">This topic discusses why and how to create and configure asset delivery policies.</span></span>

>[!NOTE]
><span data-ttu-id="7d2a2-108">Po utworzeniu konta usługi AMS zostanie do niego dodany **domyślny** punkt końcowy przesyłania strumieniowego mający stan **Zatrzymany**.</span><span class="sxs-lookup"><span data-stu-id="7d2a2-108">When your AMS account is created a **default** streaming endpoint is added to your account in the **Stopped** state.</span></span> <span data-ttu-id="7d2a2-109">Aby rozpocząć przesyłanie strumieniowe zawartości oraz korzystać z dynamicznego tworzenia pakietów i szyfrowania dynamicznego, punkt końcowy przesyłania strumieniowego, z którego chcesz strumieniowo przesyłać zawartość, musi mieć stan **Uruchomiony**.</span><span class="sxs-lookup"><span data-stu-id="7d2a2-109">To start streaming your content and take advantage of dynamic packaging and dynamic encryption, the streaming endpoint from which you want to stream content has to be in the **Running** state.</span></span> 
>
><span data-ttu-id="7d2a2-110">Ponadto aby można było korzystać z dynamicznego tworzenia pakietów i dynamicznego szyfrowania zawartości musi zawierać zestaw o adaptacyjnej szybkości bitowej MP4s lub pliki Smooth Streaming adaptacyjną szybkością transmisji bitów.</span><span class="sxs-lookup"><span data-stu-id="7d2a2-110">Also, to be able to use dynamic packaging and dynamic encryption your asset must contain a set of adaptive bitrate MP4s or adaptive bitrate Smooth Streaming files.</span></span>


<span data-ttu-id="7d2a2-111">Różnych zasad można zastosować do tego samego zasobu.</span><span class="sxs-lookup"><span data-stu-id="7d2a2-111">You could apply different policies to the same asset.</span></span> <span data-ttu-id="7d2a2-112">Na przykład można zastosować szyfrowanie PlayReady do szyfrowania Smooth Streaming i szyfrowanie AES Envelope MPEG DASH i HLS.</span><span class="sxs-lookup"><span data-stu-id="7d2a2-112">For example, you could apply PlayReady encryption to Smooth Streaming and AES Envelope encryption to MPEG DASH and HLS.</span></span> <span data-ttu-id="7d2a2-113">Protokoły, które nie są zdefiniowane w zasadzie dostarczania (można na przykład dodać jedną zasadę, która określa tylko protokół HLS), nie mogą korzystać z przesyłania strumieniowego.</span><span class="sxs-lookup"><span data-stu-id="7d2a2-113">Any protocols that are not defined in a delivery policy (for example, you add a single policy that only specifies HLS as the protocol) will be blocked from streaming.</span></span> <span data-ttu-id="7d2a2-114">Wyjątkiem od tej reguły jest przypadek, w którym nie zdefiniowano żadnej zasady dostarczania elementów zawartości.</span><span class="sxs-lookup"><span data-stu-id="7d2a2-114">The exception to this is if you have no asset delivery policy defined at all.</span></span> <span data-ttu-id="7d2a2-115">Wówczas wszystkie protokoły mogą być przesyłane bez zabezpieczeń.</span><span class="sxs-lookup"><span data-stu-id="7d2a2-115">Then, all protocols will be allowed in the clear.</span></span>

<span data-ttu-id="7d2a2-116">Jeśli chcesz dostarczyć zasób zaszyfrowanych magazynu, należy skonfigurować zasady dostarczania elementu zawartości.</span><span class="sxs-lookup"><span data-stu-id="7d2a2-116">If you want to deliver a storage encrypted asset, you must configure the asset’s delivery policy.</span></span> <span data-ttu-id="7d2a2-117">Przed zawartości mogą być przesyłane strumieniowo, serwer przesyłania strumieniowego usuwa szyfrowanie magazynu i strumieni zawartości przy użyciu zasady dostarczania określony.</span><span class="sxs-lookup"><span data-stu-id="7d2a2-117">Before your asset can be streamed, the streaming server removes the storage encryption and streams your content using the specified delivery policy.</span></span> <span data-ttu-id="7d2a2-118">Na przykład aby dostarczania zawartości zaszyfrowane za pomocą klucza szyfrowania koperty Advanced Encryption (Standard AES), Ustaw typ zasad **DynamicEnvelopeEncryption**.</span><span class="sxs-lookup"><span data-stu-id="7d2a2-118">For example, to deliver your asset encrypted with Advanced Encryption Standard (AES) envelope encryption key, set the policy type to **DynamicEnvelopeEncryption**.</span></span> <span data-ttu-id="7d2a2-119">Aby usunąć szyfrowanie magazynu i zasobów niezabezpieczona strumienia, Ustaw typ zasad **NoDynamicEncryption**.</span><span class="sxs-lookup"><span data-stu-id="7d2a2-119">To remove storage encryption and stream the asset in the clear, set the policy type to **NoDynamicEncryption**.</span></span> <span data-ttu-id="7d2a2-120">Wykonaj przykłady, które pokazują, jak skonfigurować te typy zasad.</span><span class="sxs-lookup"><span data-stu-id="7d2a2-120">Examples that show how to configure these policy types follow.</span></span>

<span data-ttu-id="7d2a2-121">W zależności od konfiguracji zasad dostarczania elementów zawartości będzie możliwe dynamicznie pakietu dynamicznie szyfrowania i przesyłania strumieniowego następujących protokołów: Smooth Streaming, HLS i MPEG DASH strumieni.</span><span class="sxs-lookup"><span data-stu-id="7d2a2-121">Depending on how you configure the asset delivery policy you would be able to dynamically package, dynamically encrypt, and stream the following streaming protocols: Smooth Streaming, HLS, and MPEG DASH streams.</span></span>

<span data-ttu-id="7d2a2-122">Na poniższej liście przedstawiono formaty umożliwia strumienia Smooth, HLS i KRESKI.</span><span class="sxs-lookup"><span data-stu-id="7d2a2-122">The following list shows the formats that you use to stream Smooth, HLS, and DASH.</span></span>

<span data-ttu-id="7d2a2-123">Funkcje Smooth Streaming:</span><span class="sxs-lookup"><span data-stu-id="7d2a2-123">Smooth Streaming:</span></span>

<span data-ttu-id="7d2a2-124">{nazwa punktu końcowego przesyłania strumieniowego-nazwa konta usługi Media Services}.streaming.mediaservices.windows.net/{identyfikator lokalizatora}/{nazwa pliku}.ism/Manifest</span><span class="sxs-lookup"><span data-stu-id="7d2a2-124">{streaming endpoint name-media services account name}.streaming.mediaservices.windows.net/{locator ID}/{filename}.ism/Manifest</span></span>

<span data-ttu-id="7d2a2-125">HLS:</span><span class="sxs-lookup"><span data-stu-id="7d2a2-125">HLS:</span></span>

<span data-ttu-id="7d2a2-126">{name}.streaming.mediaservices.windows.net/{locator konta usługi media Nazwa punktu końcowego ID}/{filename}.ism/Manifest(format=m3u8-aapl) przesyłania strumieniowego</span><span class="sxs-lookup"><span data-stu-id="7d2a2-126">{streaming endpoint name-media services account name}.streaming.mediaservices.windows.net/{locator ID}/{filename}.ism/Manifest(format=m3u8-aapl)</span></span>

<span data-ttu-id="7d2a2-127">MPEG DASH</span><span class="sxs-lookup"><span data-stu-id="7d2a2-127">MPEG DASH</span></span>

<span data-ttu-id="7d2a2-128">{name}.streaming.mediaservices.windows.net/{locator konta usługi media Nazwa punktu końcowego ID}/{filename}.ism/Manifest(format=mpd-time-csf) przesyłania strumieniowego</span><span class="sxs-lookup"><span data-stu-id="7d2a2-128">{streaming endpoint name-media services account name}.streaming.mediaservices.windows.net/{locator ID}/{filename}.ism/Manifest(format=mpd-time-csf)</span></span>


## <a name="considerations"></a><span data-ttu-id="7d2a2-129">Zagadnienia do rozważenia</span><span class="sxs-lookup"><span data-stu-id="7d2a2-129">Considerations</span></span>
* <span data-ttu-id="7d2a2-130">Nie można usunąć AssetDeliveryPolicy skojarzone z zasobów, gdy Lokalizator OnDemand (streaming) istnieje dla tego zasobu.</span><span class="sxs-lookup"><span data-stu-id="7d2a2-130">You cannot delete an AssetDeliveryPolicy associated with an asset while an OnDemand (streaming) locator exists for that asset.</span></span> <span data-ttu-id="7d2a2-131">Zalecane jest, aby usunąć zasady z zasobu przed usunięciem zasad.</span><span class="sxs-lookup"><span data-stu-id="7d2a2-131">The recommendation is to remove the policy from the asset before deleting the policy.</span></span>
* <span data-ttu-id="7d2a2-132">Nie można utworzyć Lokalizator przesyłania strumieniowego magazynu trwałego zaszyfrowane, jeśli ustawiono nie zasad dostarczania elementów zawartości.</span><span class="sxs-lookup"><span data-stu-id="7d2a2-132">A streaming locator cannot be created on a storage encrypted asset when no asset delivery policy is set.</span></span>  <span data-ttu-id="7d2a2-133">Jeśli element zawartości nie jest szyfrowany w magazynie, system będzie umożliwiają tworzenie lokalizatora i strumienia zasobów w zwykłym bez zasad dostarczania elementów zawartości.</span><span class="sxs-lookup"><span data-stu-id="7d2a2-133">If the Asset isn’t storage encrypted, the system will let you create a locator and stream the asset in the clear without an asset delivery policy.</span></span>
* <span data-ttu-id="7d2a2-134">Może mieć wiele zasady dostarczania zasobów skojarzonych z pojedynczego zasobu, ale można określić tylko jeden sposób obsługi danego AssetDeliveryProtocol.</span><span class="sxs-lookup"><span data-stu-id="7d2a2-134">You can have multiple asset delivery policies associated with a single asset but you can only specify one way to handle a given AssetDeliveryProtocol.</span></span>  <span data-ttu-id="7d2a2-135">Co oznacza, spróbuj połączyć dwie zasady dostarczania, które określają protokół AssetDeliveryProtocol.SmoothStreaming, który spowoduje błąd, ponieważ system nie może określić, które co ma to zastosowanie, gdy klient przesyła żądanie Smooth Streaming.</span><span class="sxs-lookup"><span data-stu-id="7d2a2-135">Meaning if you try to link two delivery policies that specify the AssetDeliveryProtocol.SmoothStreaming protocol that will result in an error because the system does not know which one you want it to apply when a client makes a Smooth Streaming request.</span></span>
* <span data-ttu-id="7d2a2-136">Jeśli masz zasób z istniejących Lokalizator przesyłania strumieniowego nie może połączyć nowe zasady w zasobie (możesz odłączyć istniejące zasady z zasobu, lub zaktualizowania zasad dostarczania skojarzone z elementu zawartości).</span><span class="sxs-lookup"><span data-stu-id="7d2a2-136">If you have an asset with an existing streaming locator, you cannot link a new policy to the asset (you can either unlink an existing policy from the asset, or update a delivery policy associated with the asset).</span></span>  <span data-ttu-id="7d2a2-137">Należy najpierw usuń Lokalizator przesyłania strumieniowego, Dostosuj zasady, a następnie ponownie utwórz Lokalizator przesyłania strumieniowego.</span><span class="sxs-lookup"><span data-stu-id="7d2a2-137">You first have to remove the streaming locator, adjust the policies, and then re-create the streaming locator.</span></span>  <span data-ttu-id="7d2a2-138">Można użyć tego samego locatorId podczas ponownego tworzenia Lokalizator przesyłania strumieniowego, ale należy upewnić się, że nie będzie powodować problemy dla klientów od zawartości mogą być buforowane źródła lub podrzędne CDN.</span><span class="sxs-lookup"><span data-stu-id="7d2a2-138">You can use the same locatorId when you recreate the streaming locator but you should ensure that won’t cause issues for clients since content can be cached by the origin or a downstream CDN.</span></span>

## <a name="clear-asset-delivery-policy"></a><span data-ttu-id="7d2a2-139">Zasady dostarczania elementu zawartości wyczyść</span><span class="sxs-lookup"><span data-stu-id="7d2a2-139">Clear asset delivery policy</span></span>

<span data-ttu-id="7d2a2-140">Następujące **ConfigureClearAssetDeliveryPolicy** metody określa nie dotyczyć szyfrowania dynamicznego i dostarczać strumienia w jednym z następujących protokołów: MPEG DASH, HLS i Smooth Streaming protokołów.</span><span class="sxs-lookup"><span data-stu-id="7d2a2-140">The following **ConfigureClearAssetDeliveryPolicy** method specifies to not apply dynamic encryption and to deliver the stream in any of the following protocols:  MPEG DASH, HLS, and Smooth Streaming protocols.</span></span> <span data-ttu-id="7d2a2-141">Można stosować te zasady do zasobów magazynu szyfrowane.</span><span class="sxs-lookup"><span data-stu-id="7d2a2-141">You might want to apply this policy to your storage encrypted assets.</span></span>

<span data-ttu-id="7d2a2-142">Aby uzyskać informacje na jakie wartości można określić podczas tworzenia AssetDeliveryPolicy, zobacz [typów używanych podczas definiowania AssetDeliveryPolicy](#types) sekcji.</span><span class="sxs-lookup"><span data-stu-id="7d2a2-142">For information on what values you can specify when creating an AssetDeliveryPolicy, see the [Types used when defining AssetDeliveryPolicy](#types) section.</span></span>

    static public void ConfigureClearAssetDeliveryPolicy(IAsset asset)
    {
        IAssetDeliveryPolicy policy =
        _context.AssetDeliveryPolicies.Create("Clear Policy",
        AssetDeliveryPolicyType.NoDynamicEncryption,
        AssetDeliveryProtocol.HLS | AssetDeliveryProtocol.SmoothStreaming | AssetDeliveryProtocol.Dash, null);
        
        asset.DeliveryPolicies.Add(policy);
    }

## <a name="dynamiccommonencryption-asset-delivery-policy"></a><span data-ttu-id="7d2a2-143">Zasady dostarczania elementu zawartości DynamicCommonEncryption</span><span class="sxs-lookup"><span data-stu-id="7d2a2-143">DynamicCommonEncryption asset delivery policy</span></span>

<span data-ttu-id="7d2a2-144">Następujące **CreateAssetDeliveryPolicy** metoda tworzy **AssetDeliveryPolicy** skonfigurowanego do zastosowania dynamicznego szyfrowania common encryption (**DynamicCommonEncryption**) do sprawnego protokołu przesyłania strumieniowego (inne protokoły będzie blokowany przesyłania strumieniowego).</span><span class="sxs-lookup"><span data-stu-id="7d2a2-144">The following **CreateAssetDeliveryPolicy** method creates the **AssetDeliveryPolicy** that is configured to apply dynamic common encryption (**DynamicCommonEncryption**) to a smooth streaming protocol (other protocols will be blocked from streaming).</span></span> <span data-ttu-id="7d2a2-145">Metoda przyjmuje dwa parametry: **zasobów** (zasobów, do której chcesz zastosować zasady dostarczania) i **IContentKey** (klucz zawartości **CommonEncryption** typu, aby uzyskać więcej informacji, zobacz: [Tworzenie klucza zawartości](media-services-dotnet-create-contentkey.md#common_contentkey)).</span><span class="sxs-lookup"><span data-stu-id="7d2a2-145">The method takes two parameters : **Asset** (the asset to which you want to apply the delivery policy) and **IContentKey** (the content key of the **CommonEncryption** type, for more information, see: [Creating a content key](media-services-dotnet-create-contentkey.md#common_contentkey)).</span></span>

<span data-ttu-id="7d2a2-146">Aby uzyskać informacje na jakie wartości można określić podczas tworzenia AssetDeliveryPolicy, zobacz [typów używanych podczas definiowania AssetDeliveryPolicy](#types) sekcji.</span><span class="sxs-lookup"><span data-stu-id="7d2a2-146">For information on what values you can specify when creating an AssetDeliveryPolicy, see the [Types used when defining AssetDeliveryPolicy](#types) section.</span></span>

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
    
            // Add AssetDelivery Policy to the asset
            asset.DeliveryPolicies.Add(assetDeliveryPolicy);
    
            Console.WriteLine();
            Console.WriteLine("Adding Asset Delivery Policy: " +
                assetDeliveryPolicy.AssetDeliveryPolicyType);
     }

<span data-ttu-id="7d2a2-147">Usługa Azure Media Services umożliwia również dodanie Widevine szyfrowania.</span><span class="sxs-lookup"><span data-stu-id="7d2a2-147">Azure Media Services also enables you to add Widevine encryption.</span></span> <span data-ttu-id="7d2a2-148">W poniższym przykładzie pokazano zarówno PlayReady i Widevine dodawany do zasad dostarczania elementów zawartości.</span><span class="sxs-lookup"><span data-stu-id="7d2a2-148">The following example demonstrates both PlayReady and Widevine being added to the asset delivery policy.</span></span>

    static public void CreateAssetDeliveryPolicy(IAsset asset, IContentKey key)
    {
        // Get the PlayReady license service URL.
        Uri acquisitionUrl = key.GetKeyDeliveryUrl(ContentKeyDeliveryType.PlayReadyLicense);


        // GetKeyDeliveryUrl for Widevine attaches the KID to the URL.
        // For example: https://amsaccount1.keydelivery.mediaservices.windows.net/Widevine/?KID=268a6dcb-18c8-4648-8c95-f46429e4927c.  
        // The WidevineBaseLicenseAcquisitionUrl (used below) also tells Dynamaic Encryption 
        // to append /? KID =< keyId > to the end of the url when creating the manifest.
        // As a result Widevine license acquisition URL will have KID appended twice, 
        // so we need to remove the KID that in the URL when we call GetKeyDeliveryUrl.

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


        // Add AssetDelivery Policy to the asset
        asset.DeliveryPolicies.Add(assetDeliveryPolicy);

    }

> [!NOTE]
> <span data-ttu-id="7d2a2-149">W przypadku szyfrowania przy użyciu metody Widevine, tylko będzie mogła dostarczać przy użyciu kreska.</span><span class="sxs-lookup"><span data-stu-id="7d2a2-149">When encrypting with Widevine, you would only be able to deliver using DASH.</span></span> <span data-ttu-id="7d2a2-150">Upewnij się określić DASH w Protokół dostarczania elementów zawartości.</span><span class="sxs-lookup"><span data-stu-id="7d2a2-150">Make sure to specify DASH in the asset delivery protocol.</span></span>
> 
> 

## <a name="dynamicenvelopeencryption-asset-delivery-policy"></a><span data-ttu-id="7d2a2-151">Zasady dostarczania elementu zawartości DynamicEnvelopeEncryption</span><span class="sxs-lookup"><span data-stu-id="7d2a2-151">DynamicEnvelopeEncryption asset delivery policy</span></span>
<span data-ttu-id="7d2a2-152">Następujące **CreateAssetDeliveryPolicy** metoda tworzy **AssetDeliveryPolicy** skonfigurowanego na zastosowanie szyfrowania dynamicznego koperty (**DynamicEnvelopeEncryption**) do protokołów Smooth Streaming, HLS i KRESKI (Jeśli zdecydujesz nie określać niektóre protokoły, będą blokowani z przesyłania strumieniowego).</span><span class="sxs-lookup"><span data-stu-id="7d2a2-152">The following **CreateAssetDeliveryPolicy** method creates the **AssetDeliveryPolicy** that is configured to apply dynamic envelope encryption (**DynamicEnvelopeEncryption**) to Smooth Streaming, HLS, and DASH protocols (if you decide to not specify some protocols, they will be blocked from streaming).</span></span> <span data-ttu-id="7d2a2-153">Metoda przyjmuje dwa parametry: **zasobów** (zasobów, do której chcesz zastosować zasady dostarczania) i **IContentKey** (klucz zawartości **EnvelopeEncryption** typu, aby uzyskać więcej informacji, zobacz: [Tworzenie klucza zawartości](media-services-dotnet-create-contentkey.md#envelope_contentkey)).</span><span class="sxs-lookup"><span data-stu-id="7d2a2-153">The method takes two parameters : **Asset** (the asset to which you want to apply the delivery policy) and **IContentKey** (the content key of the **EnvelopeEncryption** type, for more information, see: [Creating a content key](media-services-dotnet-create-contentkey.md#envelope_contentkey)).</span></span>

<span data-ttu-id="7d2a2-154">Aby uzyskać informacje na jakie wartości można określić podczas tworzenia AssetDeliveryPolicy, zobacz [typów używanych podczas definiowania AssetDeliveryPolicy](#types) sekcji.</span><span class="sxs-lookup"><span data-stu-id="7d2a2-154">For information on what values you can specify when creating an AssetDeliveryPolicy, see the [Types used when defining AssetDeliveryPolicy](#types) section.</span></span>   

    private static void CreateAssetDeliveryPolicy(IAsset asset, IContentKey key)
    {

        //  Get the Key Delivery Base Url by removing the Query parameter.  The Dynamic Encryption service will
        //  automatically add the correct key identifier to the url when it generates the Envelope encrypted content
        //  manifest.  Omitting the IV will also cause the Dynamice Encryption service to generate a deterministic
        //  IV for the content automatically.  By using the EnvelopeBaseKeyAcquisitionUrl and omitting the IV, this
        //  allows the AssetDelivery policy to be reused by more than one asset.
        //
        Uri keyAcquisitionUri = key.GetKeyDeliveryUrl(ContentKeyDeliveryType.BaselineHttp);
        UriBuilder uriBuilder = new UriBuilder(keyAcquisitionUri);
        uriBuilder.Query = String.Empty;
        keyAcquisitionUri = uriBuilder.Uri;

        // The following policy configuration specifies: 
        //   key url that will have KID=<Guid> appended to the envelope and
        //   the Initialization Vector (IV) to use for the envelope encryption.
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

        // Add AssetDelivery Policy to the asset
        asset.DeliveryPolicies.Add(assetDeliveryPolicy);

        Console.WriteLine();
        Console.WriteLine("Adding Asset Delivery Policy: " + assetDeliveryPolicy.AssetDeliveryPolicyType);
    }


## <span data-ttu-id="7d2a2-155"><a id="types"></a>Typy używane podczas definiowania AssetDeliveryPolicy</span><span class="sxs-lookup"><span data-stu-id="7d2a2-155"><a id="types"></a>Types used when defining AssetDeliveryPolicy</span></span>

### <span data-ttu-id="7d2a2-156"><a id="AssetDeliveryProtocol"></a>AssetDeliveryProtocol</span><span class="sxs-lookup"><span data-stu-id="7d2a2-156"><a id="AssetDeliveryProtocol"></a>AssetDeliveryProtocol</span></span>

<span data-ttu-id="7d2a2-157">Następujące wyliczenia opisano wartości, które można ustawić dla Protokół dostarczania elementów zawartości.</span><span class="sxs-lookup"><span data-stu-id="7d2a2-157">The following enum describes values you can set for the asset delivery protocol.</span></span>

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

### <span data-ttu-id="7d2a2-158"><a id="AssetDeliveryPolicyType"></a>AssetDeliveryPolicyType</span><span class="sxs-lookup"><span data-stu-id="7d2a2-158"><a id="AssetDeliveryPolicyType"></a>AssetDeliveryPolicyType</span></span>

<span data-ttu-id="7d2a2-159">Następujące wyliczenia opisano wartości, które można ustawić dla typu zasady dostarczania elementu zawartości.</span><span class="sxs-lookup"><span data-stu-id="7d2a2-159">The following enum describes values you can set for the asset delivery policy type.</span></span>  

    public enum AssetDeliveryPolicyType
    {
        /// <summary>
        /// Delivery Policy Type not set.  An invalid value.
        /// </summary>
        None,

        /// <summary>
        /// The Asset should not be delivered via this AssetDeliveryProtocol. 
        /// </summary>
        Blocked, 

        /// <summary>
        /// Do not apply dynamic encryption to the asset.
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

### <span data-ttu-id="7d2a2-160"><a id="ContentKeyDeliveryType"></a>ContentKeyDeliveryType</span><span class="sxs-lookup"><span data-stu-id="7d2a2-160"><a id="ContentKeyDeliveryType"></a>ContentKeyDeliveryType</span></span>

<span data-ttu-id="7d2a2-161">Następujące wyliczenia opisano wartości, które służy do konfigurowania metody dostarczania zawartości klucza do klienta.</span><span class="sxs-lookup"><span data-stu-id="7d2a2-161">The following enum describes values you can use to configure the delivery method of the content key to the client.</span></span>
    
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

### <span data-ttu-id="7d2a2-162"><a id="AssetDeliveryPolicyConfigurationKey"></a>AssetDeliveryPolicyConfigurationKey</span><span class="sxs-lookup"><span data-stu-id="7d2a2-162"><a id="AssetDeliveryPolicyConfigurationKey"></a>AssetDeliveryPolicyConfigurationKey</span></span>

<span data-ttu-id="7d2a2-163">Następujące wyliczenia opisano wartości, które można ustawić, aby skonfigurować klucze służące do pobrania konfiguracji określonych dla zasad dostarczania elementów zawartości.</span><span class="sxs-lookup"><span data-stu-id="7d2a2-163">The following enum describes values you can set to configure keys used to get specific configuration for an asset delivery policy.</span></span>

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
        /// The initialization vector to use for envelope encryption in Base64 format.
        /// </summary>
        EnvelopeEncryptionIVAsBase64,

        /// <summary>
        /// The PlayReady License Acquisition Url to use for common encryption.
        /// </summary>
        PlayReadyLicenseAcquisitionUrl,

        /// <summary>
        /// The PlayReady Custom Attributes to add to the PlayReady Content Header
        /// </summary>
        PlayReadyCustomAttributes,

        /// <summary>
        /// The initialization vector to use for envelope encryption.
        /// </summary>
        EnvelopeEncryptionIV,

        /// <summary>
        /// Widevine DRM acquisition url
        /// </summary>
        WidevineLicenseAcquisitionUrl
    }

## <a name="media-services-learning-paths"></a><span data-ttu-id="7d2a2-164">Ścieżki szkoleniowe dotyczące usługi Media Services</span><span class="sxs-lookup"><span data-stu-id="7d2a2-164">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="7d2a2-165">Przekazywanie opinii</span><span class="sxs-lookup"><span data-stu-id="7d2a2-165">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

