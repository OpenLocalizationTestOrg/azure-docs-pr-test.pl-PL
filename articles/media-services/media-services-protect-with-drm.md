---
title: "Używanie dynamicznego szyfrowania Common Encryption w usługach PlayReady i Widevine | Microsoft Docs"
description: "Usługa Microsoft Azure Media Services umożliwia dostarczanie strumieni MPEG-DASH, Smooth Streaming i HTTP-Live-Streaming (HLS) chronionych przy użyciu usługi Microsoft PlayReady DRM. Możliwe jest również dostarczanie strumienia DASH szyfrowanego przy użyciu usługi Widevine DRM. W tym temacie przedstawiono sposób dynamicznego szyfrowania przy użyciu usług PlayReady i Widevine DRM."
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: 548d1a12-e2cb-45fe-9307-4ec0320567a2
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/18/2017
ms.author: juliako
ms.openlocfilehash: 6cfb7b558b8dce511d517e69c022765feae245fa
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
# <a name="using-playready-andor-widevine-dynamic-common-encryption"></a><span data-ttu-id="1f7ef-105">Używanie dynamicznego szyfrowania Common Encryption w usługach PlayReady i Widevine</span><span class="sxs-lookup"><span data-stu-id="1f7ef-105">Using PlayReady and/or Widevine dynamic common encryption</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="1f7ef-106">.NET</span><span class="sxs-lookup"><span data-stu-id="1f7ef-106">.NET</span></span>](media-services-protect-with-drm.md)
> * [<span data-ttu-id="1f7ef-107">Java</span><span class="sxs-lookup"><span data-stu-id="1f7ef-107">Java</span></span>](https://github.com/southworkscom/azure-sdk-for-media-services-java-samples)
> * [<span data-ttu-id="1f7ef-108">PHP</span><span class="sxs-lookup"><span data-stu-id="1f7ef-108">PHP</span></span>](https://github.com/Azure/azure-sdk-for-php/tree/master/examples/MediaServices)
>
>

<span data-ttu-id="1f7ef-109">Usługa Microsoft Azure Media Services umożliwia dostarczanie strumieni MPEG-DASH, Smooth Streaming i HTTP-Live-Streaming (HLS) chronionych przy użyciu usługi [Microsoft PlayReady DRM](https://www.microsoft.com/playready/overview/).</span><span class="sxs-lookup"><span data-stu-id="1f7ef-109">Microsoft Azure Media Services enables you to deliver MPEG-DASH, Smooth Streaming, and HTTP-Live-Streaming (HLS) streams protected with [Microsoft PlayReady DRM](https://www.microsoft.com/playready/overview/).</span></span> <span data-ttu-id="1f7ef-110">Umożliwia ona także dostarczanie zaszyfrowanych strumienie DASH korzystających z licencji Widevine DRM.</span><span class="sxs-lookup"><span data-stu-id="1f7ef-110">It also enables you to deliver encrypted DASH streams with Widevine DRM licenses.</span></span> <span data-ttu-id="1f7ef-111">Obie usługi, PlayReady i Widevine, szyfrują dane zgodnie ze specyfikacją Common Encryption (ISO/IEC CENC 23001-7).</span><span class="sxs-lookup"><span data-stu-id="1f7ef-111">Both PlayReady and Widevine are encrypted per the Common Encryption (ISO/IEC 23001-7 CENC) specification.</span></span> <span data-ttu-id="1f7ef-112">Aby skorzystać z usługi Widevine, można skonfigurować obiekt AssetDeliveryConfiguration przy użyciu pakietu [AMS .NET SDK](https://www.nuget.org/packages/windowsazure.mediaservices/) (począwszy od wersji 3.5.1) lub interfejsu API REST.</span><span class="sxs-lookup"><span data-stu-id="1f7ef-112">You can use [AMS .NET SDK](https://www.nuget.org/packages/windowsazure.mediaservices/) (starting with the version 3.5.1) or REST API to configure your AssetDeliveryConfiguration to use Widevine.</span></span>

<span data-ttu-id="1f7ef-113">Usługa Media Services udostępnia usługę dostarczania licencji PlayReady i Widevine DRM.</span><span class="sxs-lookup"><span data-stu-id="1f7ef-113">Media Services provides a service for delivering PlayReady and Widevine DRM licenses.</span></span> <span data-ttu-id="1f7ef-114">Usługa Media Services dostarcza również interfejsy API, które umożliwiają skonfigurowanie uprawnień i ograniczeń, które powinny być wymuszane w uruchomionym środowisku PlayReady lub Widevine DRM, gdy użytkownik odtwarza chronioną zawartość.</span><span class="sxs-lookup"><span data-stu-id="1f7ef-114">Media Services also provides APIs that let you configure the rights and restrictions that you want for the PlayReady or Widevine DRM runtime to enforce when a user plays back protected content.</span></span> <span data-ttu-id="1f7ef-115">Gdy użytkownik zażąda zawartości chronionej przy użyciu DRM, aplikacja odtwarzacza zażąda licencji od usługi licencjonowania AMS.</span><span class="sxs-lookup"><span data-stu-id="1f7ef-115">When a user requests a DRM protected content, the player application will request a license from the AMS license service.</span></span> <span data-ttu-id="1f7ef-116">Usługa licencjonowania AMS wystawi licencję dla odtwarzacza, jeśli jest on autoryzowany.</span><span class="sxs-lookup"><span data-stu-id="1f7ef-116">The AMS license service will issue a license to the player if it is authorized.</span></span> <span data-ttu-id="1f7ef-117">Licencja PlayReady lub Widevine zawiera klucz odszyfrowujący, który może zostać użyty przez odtwarzacz klienta do odszyfrowania i strumieniowego przesyłania zawartości.</span><span class="sxs-lookup"><span data-stu-id="1f7ef-117">A PlayReady or Widevine license contains the decryption key that can be used by the client player to decrypt and stream the content.</span></span>

<span data-ttu-id="1f7ef-118">Licencje Widevine są dostępne również u następujących partnerów usługi AMS: [Axinom](http://www.axinom.com/press/ibc-axinom-drm-6/), [EZDRM](http://ezdrm.com/) i [castLabs](http://castlabs.com/company/partners/azure/).</span><span class="sxs-lookup"><span data-stu-id="1f7ef-118">You can also use the following AMS partners to help you deliver Widevine licenses: [Axinom](http://www.axinom.com/press/ibc-axinom-drm-6/), [EZDRM](http://ezdrm.com/), [castLabs](http://castlabs.com/company/partners/azure/).</span></span> <span data-ttu-id="1f7ef-119">Aby uzyskać więcej informacji, zobacz: integracja z [Axinom](media-services-axinom-integration.md) i [castLabs](media-services-castlabs-integration.md).</span><span class="sxs-lookup"><span data-stu-id="1f7ef-119">For more information, see: integration with [Axinom](media-services-axinom-integration.md) and [castLabs](media-services-castlabs-integration.md).</span></span>

<span data-ttu-id="1f7ef-120">Usługa Media Services obsługuje wiele sposobów autoryzacji użytkowników, którzy tworzą żądania klucza.</span><span class="sxs-lookup"><span data-stu-id="1f7ef-120">Media Services supports multiple ways of authorizing users who make key requests.</span></span> <span data-ttu-id="1f7ef-121">Zasady autoryzacji klucza zawartości mogą mieć jedno lub więcej ograniczeń: ograniczenie otwarte lub ograniczenie tokenu.</span><span class="sxs-lookup"><span data-stu-id="1f7ef-121">The content key authorization policy could have one or more authorization restrictions: open or token restriction.</span></span> <span data-ttu-id="1f7ef-122">Zasadzie ograniczenia tokenu musi towarzyszyć token wystawiony przez usługę STS (Secure Token Service).</span><span class="sxs-lookup"><span data-stu-id="1f7ef-122">The token restricted policy must be accompanied by a token issued by a Secure Token Service (STS).</span></span> <span data-ttu-id="1f7ef-123">Usługa Media Services obsługuje następujące formaty tokenów: [SWT (Simple Web Token)](https://msdn.microsoft.com/library/gg185950.aspx#BKMK_2) i [JWT (JSON Web Token)](https://msdn.microsoft.com/library/gg185950.aspx#BKMK_3).</span><span class="sxs-lookup"><span data-stu-id="1f7ef-123">Media Services supports tokens in the [Simple Web Tokens](https://msdn.microsoft.com/library/gg185950.aspx#BKMK_2) (SWT) format and [JSON Web Token](https://msdn.microsoft.com/library/gg185950.aspx#BKMK_3) (JWT) format.</span></span> <span data-ttu-id="1f7ef-124">Aby uzyskać więcej informacji, zobacz Konfigurowanie zasad autoryzacji klucza zawartości.</span><span class="sxs-lookup"><span data-stu-id="1f7ef-124">For more information, see Configure the content key’s authorization policy.</span></span>

<span data-ttu-id="1f7ef-125">Aby móc skorzystać z szyfrowania dynamicznego, należy posiadać element zawartości zawierający zestaw plików MP4 o różnych szybkościach transmisji bitów lub pliki źródłowe Smooth Streaming o różnych szybkościach transmisji bitów.</span><span class="sxs-lookup"><span data-stu-id="1f7ef-125">To take advantage of dynamic encryption, you need to have an asset that contains a set of multi-bitrate MP4 files or multi-bitrate Smooth Streaming source files.</span></span> <span data-ttu-id="1f7ef-126">Należy również skonfigurować zasady dostarczania tego elementu zawartości (opisane w dalszej części niniejszego tematu).</span><span class="sxs-lookup"><span data-stu-id="1f7ef-126">You also need to configure the delivery policies for the asset (described later in this topic).</span></span> <span data-ttu-id="1f7ef-127">Następnie na podstawie formatu określonego w adresie URL przesyłanego strumienia serwer przesyłania strumieniowego na żądanie upewni się, czy strumień jest dostarczany za pomocą wybranego protokołu.</span><span class="sxs-lookup"><span data-stu-id="1f7ef-127">Then, based on the format specified in the streaming URL, the On-Demand Streaming server will ensure that the stream is delivered in the protocol you have chosen.</span></span> <span data-ttu-id="1f7ef-128">Dzięki temu wystarczy przechowywać i opłacać pliki w jednym formacie magazynu, a usługa Media Services utworzy oraz udostępni właściwą odpowiedź HTTP na podstawie żądań klienta.</span><span class="sxs-lookup"><span data-stu-id="1f7ef-128">As a result, you only need to store and pay for the files in a single storage format and Media Services will build and serve the appropriate HTTP response based on each request from a client.</span></span>

<span data-ttu-id="1f7ef-129">Ten temat powinien być przydatny dla deweloperów pracujących nad aplikacjami, które dostarczają zawartość chronioną przy użyciu wielu protokołów DRM, takich jak PlayReady i Widevine.</span><span class="sxs-lookup"><span data-stu-id="1f7ef-129">This topic would be useful to developers that work on applications that deliver media protected with multiple DRMs, such as PlayReady and Widevine.</span></span> <span data-ttu-id="1f7ef-130">W tym temacie opisano sposób konfigurowania usługi dostarczania licencji PlayReady przy użyciu zasad autoryzacji, tak aby tylko autoryzowani klienci mogli odbierać licencje PlayReady lub Widevine.</span><span class="sxs-lookup"><span data-stu-id="1f7ef-130">The topic shows you how to configure the PlayReady license delivery service with authorization policies so that only authorized clients could receive PlayReady or Widevine licenses.</span></span> <span data-ttu-id="1f7ef-131">Przedstawiono także sposób korzystania z szyfrowania przy użyciu usług PlayReady lub Widevine DRM dla strumienia DASH.</span><span class="sxs-lookup"><span data-stu-id="1f7ef-131">It also shows how to use dynamic encryption encryption with PlayReady or Widevine DRM over DASH.</span></span>

>[!NOTE]
><span data-ttu-id="1f7ef-132">Po utworzeniu konta usługi AMS zostanie do niego dodany **domyślny** punkt końcowy przesyłania strumieniowego mający stan **Zatrzymany**.</span><span class="sxs-lookup"><span data-stu-id="1f7ef-132">When your AMS account is created a **default** streaming endpoint is added to your account in the **Stopped** state.</span></span> <span data-ttu-id="1f7ef-133">Aby rozpocząć przesyłanie strumieniowe zawartości oraz korzystać z dynamicznego tworzenia pakietów i szyfrowania dynamicznego, punkt końcowy przesyłania strumieniowego, z którego chcesz strumieniowo przesyłać zawartość, musi mieć stan **Uruchomiony**.</span><span class="sxs-lookup"><span data-stu-id="1f7ef-133">To start streaming your content and take advantage of dynamic packaging and dynamic encryption, the streaming endpoint from which you want to stream content has to be in the **Running** state.</span></span> 

## <a name="download-sample"></a><span data-ttu-id="1f7ef-134">Pobieranie przykładu</span><span class="sxs-lookup"><span data-stu-id="1f7ef-134">Download sample</span></span>
<span data-ttu-id="1f7ef-135">Opisany w tym artykule przykład możesz pobrać [tutaj](https://github.com/Azure-Samples/media-services-dotnet-dynamic-encryption-with-drm).</span><span class="sxs-lookup"><span data-stu-id="1f7ef-135">You can download the sample described in this article from [here](https://github.com/Azure-Samples/media-services-dotnet-dynamic-encryption-with-drm).</span></span>

## <a name="configuring-dynamic-common-encryption-and-drm-license-delivery-services"></a><span data-ttu-id="1f7ef-136">Konfigurowanie dynamicznego szyfrowania Common Encryption i usług dostarczania licencji DRM</span><span class="sxs-lookup"><span data-stu-id="1f7ef-136">Configuring Dynamic Common Encryption and DRM License Delivery Services</span></span>

<span data-ttu-id="1f7ef-137">Poniżej przedstawiono ogólne kroki, które należy wykonać podczas ochrony swoich elementów zawartości przy użyciu usługi PlayReady, usługi dostarczania licencji Media Services, a także za pomocą szyfrowania dynamicznego.</span><span class="sxs-lookup"><span data-stu-id="1f7ef-137">The following are general steps that you would need to perform when protecting your assets with PlayReady, using the Media Services license delivery service, and also using dynamic encryption.</span></span>

1. <span data-ttu-id="1f7ef-138">Utwórz element zawartości i przekaż do niego pliki.</span><span class="sxs-lookup"><span data-stu-id="1f7ef-138">Create an asset and upload files into the asset.</span></span>
2. <span data-ttu-id="1f7ef-139">Przekoduj element zawartości zawierający plik na zestaw o adaptacyjnej szybkości bitowej MP4.</span><span class="sxs-lookup"><span data-stu-id="1f7ef-139">Encode the asset containing the file to the adaptive bitrate MP4 set.</span></span>
3. <span data-ttu-id="1f7ef-140">Utwórz klucz zawartości i skojarz go z zakodowanym elementem zawartości.</span><span class="sxs-lookup"><span data-stu-id="1f7ef-140">Create a content key and associate it with the encoded asset.</span></span> <span data-ttu-id="1f7ef-141">W usłudze Media Services klucz zawartości zawiera klucz szyfrowania elementu zawartości.</span><span class="sxs-lookup"><span data-stu-id="1f7ef-141">In Media Services, the content key contains the asset’s encryption key.</span></span>
4. <span data-ttu-id="1f7ef-142">Skonfiguruj zasady autoryzacji klucza zawartości.</span><span class="sxs-lookup"><span data-stu-id="1f7ef-142">Configure the content key’s authorization policy.</span></span> <span data-ttu-id="1f7ef-143">Zasady autoryzacji klucza zawartości muszą zostać skonfigurowane przez użytkownika i muszą być spełnione przez klienta, aby klucz zawartości został dostarczony do klienta.</span><span class="sxs-lookup"><span data-stu-id="1f7ef-143">The content key authorization policy must be configured by you and met by the client in order for the content key to be delivered to the client.</span></span>

    <span data-ttu-id="1f7ef-144">Podczas tworzenia zasady autoryzacji klucza zawartości należy określić następujące elementy: metodę dostarczania (PlayReady lub Widevine), ograniczenia (otwarte lub tokenu) i informacje specyficzne dla typu klucza dostawy, które definiują sposób dostawy klucza do klienta (szablon licencji [PlayReady](media-services-playready-license-template-overview.md) lub [Widevine](media-services-widevine-license-template-overview.md)).</span><span class="sxs-lookup"><span data-stu-id="1f7ef-144">When creating the content key authorization policy, you need to specify the following: delivery method (PlayReady or Widevine), restrictions (open or token), and information specific to the key delivery type that defines how the key is delivered to the client ([PlayReady](media-services-playready-license-template-overview.md) or [Widevine](media-services-widevine-license-template-overview.md) license template).</span></span>

5. <span data-ttu-id="1f7ef-145">Skonfiguruj zasadę dostarczania elementu zawartości.</span><span class="sxs-lookup"><span data-stu-id="1f7ef-145">Configure the delivery policy for an asset.</span></span> <span data-ttu-id="1f7ef-146">Konfiguracja zasad dostarczania obejmuje: protokół dostarczenia (na przykład MPEG DASH, HLS, Smooth Streaming lub wszystkie z nich), typ szyfrowania dynamicznego (na przykład Common Encryption) oraz adres URL pozyskiwania licencji PlayReady lub Widevine.</span><span class="sxs-lookup"><span data-stu-id="1f7ef-146">The delivery policy configuration includes: delivery protocol (for example, MPEG DASH, HLS, Smooth Streaming or all), the type of dynamic encryption (for example, Common Encryption), PlayReady or Widevine license acquisition URL.</span></span>

    <span data-ttu-id="1f7ef-147">Dla każdego protokołu dotyczącego danego elementu zawartości można stosować inne zasady.</span><span class="sxs-lookup"><span data-stu-id="1f7ef-147">You could apply different policy to each protocol on the same asset.</span></span> <span data-ttu-id="1f7ef-148">Na przykład dla protokołu Smooth/DASH można zastosować szyfrowanie PlayReady, zaś dla protokołu HLS szyfrowanie AES Envelope.</span><span class="sxs-lookup"><span data-stu-id="1f7ef-148">For example, you could apply PlayReady encryption to Smooth/DASH and AES Envelope to HLS.</span></span> <span data-ttu-id="1f7ef-149">Protokoły, które nie są zdefiniowane w zasadzie dostarczania (można na przykład dodać jedną zasadę, która określa tylko protokół HLS), nie mogą korzystać z przesyłania strumieniowego.</span><span class="sxs-lookup"><span data-stu-id="1f7ef-149">Any protocols that are not defined in a delivery policy (for example, you add a single policy that only specifies HLS as the protocol) will be blocked from streaming.</span></span> <span data-ttu-id="1f7ef-150">Wyjątkiem od tej reguły jest przypadek, w którym nie zdefiniowano żadnej zasady dostarczania elementów zawartości.</span><span class="sxs-lookup"><span data-stu-id="1f7ef-150">The exception to this is if you have no asset delivery policy defined at all.</span></span> <span data-ttu-id="1f7ef-151">Wówczas wszystkie protokoły mogą być przesyłane bez zabezpieczeń.</span><span class="sxs-lookup"><span data-stu-id="1f7ef-151">Then, all protocols will be allowed in the clear.</span></span>

6. <span data-ttu-id="1f7ef-152">Utwórz lokalizator OnDemand w celu pobrania adresu URL przesyłania strumieniowego.</span><span class="sxs-lookup"><span data-stu-id="1f7ef-152">Create an OnDemand locator in order to get a streaming URL.</span></span>

<span data-ttu-id="1f7ef-153">Na końcu tego tematu znajduje się pełny przykład dla środowiska .NET.</span><span class="sxs-lookup"><span data-stu-id="1f7ef-153">You will find a complete .NET example at the end of the topic.</span></span>

<span data-ttu-id="1f7ef-154">Poniższa ilustracja pokazuje opisany wyżej przepływ pracy.</span><span class="sxs-lookup"><span data-stu-id="1f7ef-154">The following image demonstrates the workflow described above.</span></span> <span data-ttu-id="1f7ef-155">Token jest tu używany do uwierzytelniania.</span><span class="sxs-lookup"><span data-stu-id="1f7ef-155">Here the token is used for authentication.</span></span>

![Ochrona za pomocą PlayReady](./media/media-services-content-protection-overview/media-services-content-protection-with-drm.png)

<span data-ttu-id="1f7ef-157">Pozostała część tego tematu zawiera szczegółowe wyjaśnienia, przykłady kodu i linki do tematów, w których pokazano, jak wykonać zadania opisane powyżej.</span><span class="sxs-lookup"><span data-stu-id="1f7ef-157">The rest of this topic provides detailed explanations, code examples, and links to topics that show you how to achieve the tasks described above.</span></span>

## <a name="current-limitations"></a><span data-ttu-id="1f7ef-158">Bieżące ograniczenia</span><span class="sxs-lookup"><span data-stu-id="1f7ef-158">Current limitations</span></span>
<span data-ttu-id="1f7ef-159">W przypadku dodania lub zaktualizowania zasad dostarczania elementów zawartości należy usunąć skojarzony lokalizator (jeśli istnieje) i utworzyć nowy.</span><span class="sxs-lookup"><span data-stu-id="1f7ef-159">If you add or update an asset delivery policy, you must delete the associated locator (if any) and create a new locator.</span></span>

<span data-ttu-id="1f7ef-160">Ograniczenie w przypadku szyfrowania przy użyciu metody Widevine dla usługi Azure Media Services: obecnie nie jest obsługiwanych wiele kluczy zawartości.</span><span class="sxs-lookup"><span data-stu-id="1f7ef-160">Limitation when encrypting with Widevine with Azure Media Services: currently, multiple content keys are not supported.</span></span>

## <a name="create-an-asset-and-upload-files-into-the-asset"></a><span data-ttu-id="1f7ef-161">Utworzenie elementu zawartości i przekazanie do niego plików</span><span class="sxs-lookup"><span data-stu-id="1f7ef-161">Create an asset and upload files into the asset</span></span>
<span data-ttu-id="1f7ef-162">W celu kodowania i przesyłania strumieniowego filmów oraz zarządzania nimi należy najpierw przekazać zawartość do usługi Microsoft Azure Media Services.</span><span class="sxs-lookup"><span data-stu-id="1f7ef-162">In order to manage, encode, and stream your videos, you must first upload your content into Microsoft Azure Media Services.</span></span> <span data-ttu-id="1f7ef-163">Po przekazaniu plików ich zawartość jest bezpiecznie przechowywana w chmurze na potrzeby dalszego przetwarzania i przesyłania strumieniowego.</span><span class="sxs-lookup"><span data-stu-id="1f7ef-163">Once uploaded, your content is stored securely in the cloud for further processing and streaming.</span></span>

<span data-ttu-id="1f7ef-164">Aby uzyskać szczegółowe informacje, zobacz artykuł [Upload Files into a Media Services account](media-services-dotnet-upload-files.md) (Przekazywanie plików na konto usługi Media Services).</span><span class="sxs-lookup"><span data-stu-id="1f7ef-164">For detailed information, see [Upload Files into a Media Services account](media-services-dotnet-upload-files.md).</span></span>

## <a name="encode-the-asset-containing-the-file-to-the-adaptive-bitrate-mp4-set"></a><span data-ttu-id="1f7ef-165">Przekodowanie elementu zawartości zawierającego plik na zestaw MP4 o adaptacyjnej szybkości bitowej</span><span class="sxs-lookup"><span data-stu-id="1f7ef-165">Encode the asset containing the file to the adaptive bitrate MP4 set</span></span>
<span data-ttu-id="1f7ef-166">W przypadku szyfrowania dynamicznego wystarczy utworzyć element zawartości zawierający zestaw plików MP4 o różnych szybkościach transmisji bitów lub pliki źródłowe Smooth Streaming o różnych szybkościach transmisji bitów.</span><span class="sxs-lookup"><span data-stu-id="1f7ef-166">With dynamic encryption all you need is to create an asset that contains a set of multi-bitrate MP4 files or multi-bitrate Smooth Streaming source files.</span></span> <span data-ttu-id="1f7ef-167">Następnie na podstawie formatu określonego w manifeście i żądaniu fragmentu serwer przesyłania strumieniowego na żądanie upewni się, czy strumień jest dostarczany za pomocą wybranego protokołu.</span><span class="sxs-lookup"><span data-stu-id="1f7ef-167">Then, based on the specified format in the manifest and fragment request, the On-Demand Streaming server will ensure that you receive the stream in the protocol you have chosen.</span></span> <span data-ttu-id="1f7ef-168">Dzięki temu wystarczy przechowywać i opłacać pliki w jednym formacie magazynu, a usługa Media Services utworzy oraz udostępni właściwą odpowiedź na podstawie żądań klienta.</span><span class="sxs-lookup"><span data-stu-id="1f7ef-168">As a result, you only need to store and pay for the files in single storage format and Media Services service will build and serve the appropriate response based on requests from a client.</span></span> <span data-ttu-id="1f7ef-169">Aby uzyskać więcej informacji, zobacz artykuł [Dynamic Packaging Overview](media-services-dynamic-packaging-overview.md) (Dynamiczne tworzenie pakietów — przegląd).</span><span class="sxs-lookup"><span data-stu-id="1f7ef-169">For more information, see the [Dynamic Packaging Overview](media-services-dynamic-packaging-overview.md) topic.</span></span>

<span data-ttu-id="1f7ef-170">Aby uzyskać instrukcje na temat kodowania, zobacz artykuł [How to encode an asset using Media Encoder Standard](media-services-dotnet-encode-with-media-encoder-standard.md) (Sposób kodowania elementów zawartości przy użyciu standardowego kodera multimediów).</span><span class="sxs-lookup"><span data-stu-id="1f7ef-170">For instructions on how to encode, see [How to encode an asset using Media Encoder Standard](media-services-dotnet-encode-with-media-encoder-standard.md).</span></span>

## <span data-ttu-id="1f7ef-171"><a id="create_contentkey"></a>Tworzenie klucza zawartości i kojarzenie go z zakodowanym elementem zawartości</span><span class="sxs-lookup"><span data-stu-id="1f7ef-171"><a id="create_contentkey"></a>Create a content key and associate it with the encoded asset</span></span>
<span data-ttu-id="1f7ef-172">W usłudze Media Services klucz zawartości zawiera klucz, za pomocą którego chcesz zaszyfrować element zawartości.</span><span class="sxs-lookup"><span data-stu-id="1f7ef-172">In Media Services, the content key contains the key that you want to encrypt an asset with.</span></span>

<span data-ttu-id="1f7ef-173">Aby uzyskać szczegółowe informacje, zobacz artykuł [Create content key](media-services-dotnet-create-contentkey.md) (Tworzenie klucza zawartości).</span><span class="sxs-lookup"><span data-stu-id="1f7ef-173">For detailed information, see [Create content key](media-services-dotnet-create-contentkey.md).</span></span>

## <span data-ttu-id="1f7ef-174"><a id="configure_key_auth_policy"></a>Konfigurowanie zasady autoryzacji klucza zawartości</span><span class="sxs-lookup"><span data-stu-id="1f7ef-174"><a id="configure_key_auth_policy"></a>Configure the content key’s authorization policy</span></span>
<span data-ttu-id="1f7ef-175">Usługa Media Services obsługuje wiele sposobów uwierzytelniania użytkowników, którzy tworzą żądania klucza.</span><span class="sxs-lookup"><span data-stu-id="1f7ef-175">Media Services supports multiple ways of authenticating users who make key requests.</span></span> <span data-ttu-id="1f7ef-176">Zasady autoryzacji klucza zawartości muszą zostać skonfigurowane przez użytkownika i muszą być spełnione przez klienta (odtwarzacz), aby klucz zawartości został dostarczony do klienta.</span><span class="sxs-lookup"><span data-stu-id="1f7ef-176">The content key authorization policy must be configured by you and met by the client (player) in order for the key to be delivered to the client.</span></span> <span data-ttu-id="1f7ef-177">Zasady autoryzacji klucza zawartości mogą mieć jedno lub więcej ograniczeń: ograniczenie otwarte lub ograniczenie tokenu.</span><span class="sxs-lookup"><span data-stu-id="1f7ef-177">The content key authorization policy could have one or more authorization restrictions: open or token restriction.</span></span>

<span data-ttu-id="1f7ef-178">Aby uzyskać więcej informacji, zobacz artykuł [Configure Content Key Authorization Policy](media-services-dotnet-configure-content-key-auth-policy.md#playready-dynamic-encryption) (Konfigurowanie zasad autoryzacji klucza zawartości).</span><span class="sxs-lookup"><span data-stu-id="1f7ef-178">For detailed information, see [Configure Content Key Authorization Policy](media-services-dotnet-configure-content-key-auth-policy.md#playready-dynamic-encryption).</span></span>

## <span data-ttu-id="1f7ef-179"><a id="configure_asset_delivery_policy"></a>Konfigurowanie zasad dostarczania elementów zawartości</span><span class="sxs-lookup"><span data-stu-id="1f7ef-179"><a id="configure_asset_delivery_policy"></a>Configure asset delivery policy</span></span>
<span data-ttu-id="1f7ef-180">Skonfiguruj zasady dostarczania dla swojego elementu zawartości.</span><span class="sxs-lookup"><span data-stu-id="1f7ef-180">Configure the delivery policy for your asset.</span></span> <span data-ttu-id="1f7ef-181">Niektóre elementy objęte konfiguracją zasad dostarczania elementów zawartości:</span><span class="sxs-lookup"><span data-stu-id="1f7ef-181">Some things that the asset delivery policy configuration includes:</span></span>

* <span data-ttu-id="1f7ef-182">Adres URL pozyskiwania licencji DRM.</span><span class="sxs-lookup"><span data-stu-id="1f7ef-182">The DRM license acquisition URL.</span></span>
* <span data-ttu-id="1f7ef-183">Protokół dostarczenia elementów zawartości (na przykład MPEG DASH, HLS, Smooth Streaming lub wszystkie z nich).</span><span class="sxs-lookup"><span data-stu-id="1f7ef-183">The asset delivery protocol (for example, MPEG DASH, HLS, Smooth Streaming or all).</span></span>
* <span data-ttu-id="1f7ef-184">Typ szyfrowania dynamicznego (w tym przypadku jest to Common Encryption).</span><span class="sxs-lookup"><span data-stu-id="1f7ef-184">The type of dynamic encryption (in this case, Common Encryption).</span></span>

<span data-ttu-id="1f7ef-185">Aby uzyskać szczegółowe informacje, zobacz artykuł [Configure asset delivery policy](media-services-rest-configure-asset-delivery-policy.md) (Konfigurowanie zasad dostarczania elementów zawartości).</span><span class="sxs-lookup"><span data-stu-id="1f7ef-185">For detailed information, see [Configure asset delivery policy ](media-services-rest-configure-asset-delivery-policy.md).</span></span>

## <span data-ttu-id="1f7ef-186"><a id="create_locator"></a>Tworzenie lokalizatora OnDemand przesyłania strumieniowego w celu pobrania adresu URL przesyłania strumieniowego</span><span class="sxs-lookup"><span data-stu-id="1f7ef-186"><a id="create_locator"></a>Create an OnDemand streaming locator in order to get a streaming URL</span></span>
<span data-ttu-id="1f7ef-187">W przypadku metod Smooth, DASH lub HLS należy podać użytkownikowi adres URL przesyłania strumieniowego.</span><span class="sxs-lookup"><span data-stu-id="1f7ef-187">You will need to provide your user with the streaming URL for Smooth, DASH or HLS.</span></span>

> [!NOTE]
> <span data-ttu-id="1f7ef-188">W przypadku dodania lub zaktualizowania zasad dostarczania elementów zawartości należy usunąć skojarzony lokalizator (jeśli istnieje) i utworzyć nowy.</span><span class="sxs-lookup"><span data-stu-id="1f7ef-188">If you add or update your asset’s delivery policy, you must delete an existing locator (if any) and create a new locator.</span></span>
>
>

<span data-ttu-id="1f7ef-189">Aby uzyskać instrukcje dotyczące sposobu publikowania elementów zawartości i tworzenia adresu URL przesyłania strumieniowego, zobacz artykuł [Build a streaming URL](media-services-deliver-streaming-content.md) (Tworzenie adresu URL przesyłania strumieniowego).</span><span class="sxs-lookup"><span data-stu-id="1f7ef-189">For instructions on how to publish an asset and build a streaming URL, see [Build a streaming URL](media-services-deliver-streaming-content.md).</span></span>

## <a name="get-a-test-token"></a><span data-ttu-id="1f7ef-190">Pobieranie tokenu testowego</span><span class="sxs-lookup"><span data-stu-id="1f7ef-190">Get a test token</span></span>
<span data-ttu-id="1f7ef-191">Pobierz token testowy, uwzględniając ograniczenia tokenu wybrane w zasadach autoryzacji klucza.</span><span class="sxs-lookup"><span data-stu-id="1f7ef-191">Get a test token based on the token restriction that was used for the key authorization policy.</span></span>

    // Deserializes a string containing an Xml representation of a TokenRestrictionTemplate
    // back into a TokenRestrictionTemplate class instance.
    TokenRestrictionTemplate tokenTemplate =
        TokenRestrictionTemplateSerializer.Deserialize(tokenTemplateString);

    // Generate a test token based on the data in the given TokenRestrictionTemplate.
    //The GenerateTestToken method returns the token without the word “Bearer” in front
    //so you have to add it in front of the token string.
    string testToken = TokenRestrictionTemplateSerializer.GenerateTestToken(tokenTemplate);
    Console.WriteLine("The authorization token is:\nBearer {0}", testToken);


<span data-ttu-id="1f7ef-192">Do przetestowania strumienia można użyć aplikacji [AMS Player](http://amsplayer.azurewebsites.net/azuremediaplayer.html).</span><span class="sxs-lookup"><span data-stu-id="1f7ef-192">You can use the [AMS Player](http://amsplayer.azurewebsites.net/azuremediaplayer.html) to test your stream.</span></span>

## <a name="create-and-configure-a-visual-studio-project"></a><span data-ttu-id="1f7ef-193">Tworzenie i konfigurowanie projektu programu Visual Studio</span><span class="sxs-lookup"><span data-stu-id="1f7ef-193">Create and configure a Visual Studio project</span></span>

1. <span data-ttu-id="1f7ef-194">Skonfiguruj środowisko projektowe i wypełnij plik app.config przy użyciu informacji dotyczących połączenia, zgodnie z opisem w sekcji [Projektowanie usługi Media Services na platformie .NET](media-services-dotnet-how-to-use.md).</span><span class="sxs-lookup"><span data-stu-id="1f7ef-194">Set up your development environment and populate the app.config file with connection information, as described in [Media Services development with .NET](media-services-dotnet-how-to-use.md).</span></span> 
2. <span data-ttu-id="1f7ef-195">Dodaj następujące elementy do węzła **appSettings** zdefiniowanego w pliku app.config:</span><span class="sxs-lookup"><span data-stu-id="1f7ef-195">Add the following elements to **appSettings** defined in your app.config file:</span></span>

        <add key="Issuer" value="http://testacs.com"/>
        <add key="Audience" value="urn:test"/>

## <a name="example"></a><span data-ttu-id="1f7ef-196">Przykład</span><span class="sxs-lookup"><span data-stu-id="1f7ef-196">Example</span></span>

<span data-ttu-id="1f7ef-197">W poniższym przykładzie pokazano funkcje wprowadzone w programie Azure Media Services SDK dla platformy .NET — wersja 3.5.2 (w szczególności jest wykorzystywana możliwość definiowania szablonu licencji Widevine i żądania licencji Widevine przez usługę Azure Media Services).</span><span class="sxs-lookup"><span data-stu-id="1f7ef-197">The following sample demonstrates functionality that was introduced in Azure Media Services SDK for .Net -Version 3.5.2 (specifically, the ability to define a Widevine license template and request a Widevine license from Azure Media Services).</span></span>

<span data-ttu-id="1f7ef-198">Zastąp kod w pliku Program.cs kodem przedstawionym w tej sekcji.</span><span class="sxs-lookup"><span data-stu-id="1f7ef-198">Overwrite the code in your Program.cs file with the code shown in this section.</span></span>

>[!NOTE]
><span data-ttu-id="1f7ef-199">Limit różnych zasad usługi AMS wynosi 1 000 000 (na przykład zasad lokalizatorów lub ContentKeyAuthorizationPolicy).</span><span class="sxs-lookup"><span data-stu-id="1f7ef-199">There is a limit of 1,000,000 policies for different AMS policies (for example, for Locator policy or ContentKeyAuthorizationPolicy).</span></span> <span data-ttu-id="1f7ef-200">Należy używać tego samego identyfikatora zasad, jeśli zawsze są używane uprawnienia dotyczące tych samych dni lub tego samego dostępu, na przykład dla lokalizatorów przeznaczonych do długotrwałego stosowania (nieprzekazywanych zasad).</span><span class="sxs-lookup"><span data-stu-id="1f7ef-200">You should use the same policy ID if you are always using the same days / access permissions, for example, policies for locators that are intended to remain in place for a long time (non-upload policies).</span></span> <span data-ttu-id="1f7ef-201">Aby uzyskać więcej informacji, zobacz [ten](media-services-dotnet-manage-entities.md#limit-access-policies) temat.</span><span class="sxs-lookup"><span data-stu-id="1f7ef-201">For more information, see [this](media-services-dotnet-manage-entities.md#limit-access-policies) topic.</span></span>

<span data-ttu-id="1f7ef-202">Upewnij się, że zaktualizowano zmienne, tak aby wskazywały foldery, w których znajdują się pliki danych wejściowych.</span><span class="sxs-lookup"><span data-stu-id="1f7ef-202">Make sure to update variables to point to folders where your input files are located.</span></span>

    using System;
    using System.Collections.Generic;
    using System.Configuration;
    using System.IO;
    using System.Linq;
    using System.Threading;
    using Microsoft.WindowsAzure.MediaServices.Client;
    using Microsoft.WindowsAzure.MediaServices.Client.ContentKeyAuthorization;
    using Microsoft.WindowsAzure.MediaServices.Client.DynamicEncryption;
    using Microsoft.WindowsAzure.MediaServices.Client.Widevine;
    using Newtonsoft.Json;

    namespace DynamicEncryptionWithDRM
    {
        class Program
        {
        // Read values from the App.config file.
        private static readonly string _AADTenantDomain =
        ConfigurationManager.AppSettings["AADTenantDomain"];
        private static readonly string _RESTAPIEndpoint =
        ConfigurationManager.AppSettings["MediaServiceRESTAPIEndpoint"];

        private static readonly Uri _sampleIssuer =
            new Uri(ConfigurationManager.AppSettings["Issuer"]);
        private static readonly Uri _sampleAudience =
            new Uri(ConfigurationManager.AppSettings["Audience"]);

        // Field for service context.
        private static CloudMediaContext _context = null;

        private static readonly string _mediaFiles =
            Path.GetFullPath(@"../..\Media");

        private static readonly string _singleMP4File =
            Path.Combine(_mediaFiles, @"BigBuckBunny.mp4");

        static void Main(string[] args)
        {
            var tokenCredentials = new AzureAdTokenCredentials(_AADTenantDomain, AzureEnvironments.AzureCloudEnvironment);
            var tokenProvider = new AzureAdTokenProvider(tokenCredentials);

            _context = new CloudMediaContext(new Uri(_RESTAPIEndpoint), tokenProvider);

            bool tokenRestriction = false;
            string tokenTemplateString = null;

            IAsset asset = UploadFileAndCreateAsset(_singleMP4File);
            Console.WriteLine("Uploaded asset: {0}", asset.Id);

            IAsset encodedAsset = EncodeToAdaptiveBitrateMP4Set(asset);
            Console.WriteLine("Encoded asset: {0}", encodedAsset.Id);

            IContentKey key = CreateCommonTypeContentKey(encodedAsset);
            Console.WriteLine("Created key {0} for the asset {1} ", key.Id, encodedAsset.Id);
            Console.WriteLine("PlayReady License Key delivery URL: {0}", key.GetKeyDeliveryUrl(ContentKeyDeliveryType.PlayReadyLicense));
            Console.WriteLine();

            if (tokenRestriction)
            tokenTemplateString = AddTokenRestrictedAuthorizationPolicy(key);
            else
            AddOpenAuthorizationPolicy(key);

            Console.WriteLine("Added authorization policy: {0}", key.AuthorizationPolicyId);
            Console.WriteLine();

            CreateAssetDeliveryPolicy(encodedAsset, key);
            Console.WriteLine("Created asset delivery policy. \n");
            Console.WriteLine();

            if (tokenRestriction && !String.IsNullOrEmpty(tokenTemplateString))
            {
            // Deserializes a string containing an Xml representation of a TokenRestrictionTemplate
            // back into a TokenRestrictionTemplate class instance.
            TokenRestrictionTemplate tokenTemplate =
                TokenRestrictionTemplateSerializer.Deserialize(tokenTemplateString);

            // Generate a test token based on the the data in the given TokenRestrictionTemplate.
            // Note, you need to pass the key id Guid because we specified
            // TokenClaim.ContentKeyIdentifierClaim in during the creation of TokenRestrictionTemplate.
            Guid rawkey = EncryptionUtils.GetKeyIdAsGuid(key.Id);
            string testToken = TokenRestrictionTemplateSerializer.GenerateTestToken(tokenTemplate, null, rawkey,
                                        DateTime.UtcNow.AddDays(365));
            Console.WriteLine("The authorization token is:\nBearer {0}", testToken);
            Console.WriteLine();
            }

            // You can use the http://amsplayer.azurewebsites.net/azuremediaplayer.html player to test streams.
            // Note that DASH works on IE 11 (via PlayReady), Edge (via PlayReady), Chrome (via Widevine).

            string url = GetStreamingOriginLocator(encodedAsset);
            Console.WriteLine("Encrypted DASH URL: {0}/manifest(format=mpd-time-csf)", url);

            Console.ReadLine();
        }

        static public IAsset UploadFileAndCreateAsset(string singleFilePath)
        {
            if (!File.Exists(singleFilePath))
            {
            Console.WriteLine("File does not exist.");
            return null;
            }

            var assetName = Path.GetFileNameWithoutExtension(singleFilePath);
            IAsset inputAsset = _context.Assets.Create(assetName, AssetCreationOptions.None);

            var assetFile = inputAsset.AssetFiles.Create(Path.GetFileName(singleFilePath));

            Console.WriteLine("Created assetFile {0}", assetFile.Name);

            Console.WriteLine("Upload {0}", assetFile.Name);

            assetFile.Upload(singleFilePath);
            Console.WriteLine("Done uploading {0}", assetFile.Name);

            return inputAsset;
        }

        static public IAsset EncodeToAdaptiveBitrateMP4Set(IAsset inputAsset)
        {
            var encodingPreset = "Adaptive Streaming";

            IJob job = _context.Jobs.Create(String.Format("Encoding into Mp4 {0} to {1}",
                        inputAsset.Name,
                        encodingPreset));

            var mediaProcessors =
            _context.MediaProcessors.Where(p => p.Name.Contains("Media Encoder Standard")).ToList();

            var latestMediaProcessor =
            mediaProcessors.OrderBy(mp => new Version(mp.Version)).LastOrDefault();

            ITask encodeTask = job.Tasks.AddNew("Encoding", latestMediaProcessor, encodingPreset, TaskOptions.None);
            encodeTask.InputAssets.Add(inputAsset);
            encodeTask.OutputAssets.AddNew(String.Format("{0} as {1}", inputAsset.Name, encodingPreset), AssetCreationOptions.StorageEncrypted);

            job.StateChanged += new EventHandler<JobStateChangedEventArgs>(JobStateChanged);
            job.Submit();
            job.GetExecutionProgressTask(CancellationToken.None).Wait();

            return job.OutputMediaAssets[0];
        }


        static public IContentKey CreateCommonTypeContentKey(IAsset asset)
        {

            Guid keyId = Guid.NewGuid();
            byte[] contentKey = GetRandomBuffer(16);

            IContentKey key = _context.ContentKeys.Create(
                        keyId,
                        contentKey,
                        "ContentKey",
                        ContentKeyType.CommonEncryption);

            // Associate the key with the asset.
            asset.ContentKeys.Add(key);

            return key;
        }

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

            // Configure PlayReady and Widevine license templates.
            string PlayReadyLicenseTemplate = ConfigurePlayReadyLicenseTemplate();

            string WidevineLicenseTemplate = ConfigureWidevineLicenseTemplate();

            IContentKeyAuthorizationPolicyOption PlayReadyPolicy =
            _context.ContentKeyAuthorizationPolicyOptions.Create("",
                ContentKeyDeliveryType.PlayReadyLicense,
                restrictions, PlayReadyLicenseTemplate);

            IContentKeyAuthorizationPolicyOption WidevinePolicy =
            _context.ContentKeyAuthorizationPolicyOptions.Create("",
                ContentKeyDeliveryType.Widevine,
                restrictions, WidevineLicenseTemplate);

            IContentKeyAuthorizationPolicy contentKeyAuthorizationPolicy = _context.
                ContentKeyAuthorizationPolicies.
                CreateAsync("Deliver Common Content Key with no restrictions").
                Result;


            contentKeyAuthorizationPolicy.Options.Add(PlayReadyPolicy);
            contentKeyAuthorizationPolicy.Options.Add(WidevinePolicy);
            // Associate the content key authorization policy with the content key.
            contentKey.AuthorizationPolicyId = contentKeyAuthorizationPolicy.Id;
            contentKey = contentKey.UpdateAsync().Result;
        }

        public static string AddTokenRestrictedAuthorizationPolicy(IContentKey contentKey)
        {
            string tokenTemplateString = GenerateTokenRequirements();

            List<ContentKeyAuthorizationPolicyRestriction> restrictions = new List<ContentKeyAuthorizationPolicyRestriction>
                {
                new ContentKeyAuthorizationPolicyRestriction
                {
                    Name = "Token Authorization Policy",
                    KeyRestrictionType = (int)ContentKeyRestrictionType.TokenRestricted,
                    Requirements = tokenTemplateString,
                }
                };

            // Configure PlayReady and Widevine license templates.
            string PlayReadyLicenseTemplate = ConfigurePlayReadyLicenseTemplate();

            string WidevineLicenseTemplate = ConfigureWidevineLicenseTemplate();

            IContentKeyAuthorizationPolicyOption PlayReadyPolicy =
            _context.ContentKeyAuthorizationPolicyOptions.Create("Token option",
                ContentKeyDeliveryType.PlayReadyLicense,
                restrictions, PlayReadyLicenseTemplate);

            IContentKeyAuthorizationPolicyOption WidevinePolicy =
            _context.ContentKeyAuthorizationPolicyOptions.Create("Token option",
                ContentKeyDeliveryType.Widevine,
                restrictions, WidevineLicenseTemplate);

            IContentKeyAuthorizationPolicy contentKeyAuthorizationPolicy = _context.
                ContentKeyAuthorizationPolicies.
                CreateAsync("Deliver Common Content Key with token restrictions").
                Result;

            contentKeyAuthorizationPolicy.Options.Add(PlayReadyPolicy);
            contentKeyAuthorizationPolicy.Options.Add(WidevinePolicy);

            // Associate the content key authorization policy with the content key
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
            // The following code configures PlayReady License Template using .NET classes
            // and returns the XML string.

            //The PlayReadyLicenseResponseTemplate class represents the template for the response sent back to the end user.
            //It contains a field for a custom data string between the license server and the application
            //(may be useful for custom app logic) as well as a list of one or more license templates.
            PlayReadyLicenseResponseTemplate responseTemplate = new PlayReadyLicenseResponseTemplate();

            // The PlayReadyLicenseTemplate class represents a license template for creating PlayReady licenses
            // to be returned to the end users.
            //It contains the data on the content key in the license and any rights or restrictions to be
            //enforced by the PlayReady DRM runtime when using the content key.
            PlayReadyLicenseTemplate licenseTemplate = new PlayReadyLicenseTemplate();
            //Configure whether the license is persistent (saved in persistent storage on the client)
            //or non-persistent (only held in memory while the player is using the license).  
            licenseTemplate.LicenseType = PlayReadyLicenseType.Nonpersistent;

            // AllowTestDevices controls whether test devices can use the license or not.  
            // If true, the MinimumSecurityLevel property of the license
            // is set to 150.  If false (the default), the MinimumSecurityLevel property of the license is set to 2000.
            licenseTemplate.AllowTestDevices = true;

            // You can also configure the Play Right in the PlayReady license by using the PlayReadyPlayRight class.
            // It grants the user the ability to playback the content subject to the zero or more restrictions
            // configured in the license and on the PlayRight itself (for playback specific policy).
            // Much of the policy on the PlayRight has to do with output restrictions
            // which control the types of outputs that the content can be played over and
            // any restrictions that must be put in place when using a given output.
            // For example, if the DigitalVideoOnlyContentRestriction is enabled,
            //then the DRM runtime will only allow the video to be displayed over digital outputs
            //(analog video outputs won’t be allowed to pass the content).

            //IMPORTANT: These types of restrictions can be very powerful but can also affect the consumer experience.
            // If the output protections are configured too restrictive,
            // the content might be unplayable on some clients. For more information, see the PlayReady Compliance Rules document.

            // For example:
            //licenseTemplate.PlayRight.AgcAndColorStripeRestriction = new AgcAndColorStripeRestriction(1);

            responseTemplate.LicenseTemplates.Add(licenseTemplate);

            return MediaServicesLicenseTemplateSerializer.Serialize(responseTemplate);
        }

        private static string ConfigureWidevineLicenseTemplate()
        {
            var template = new WidevineMessage
            {
            allowed_track_types = AllowedTrackTypes.SD_HD,
            content_key_specs = new[]
            {
                    new ContentKeySpecs
                    {
                    required_output_protection = new RequiredOutputProtection { hdcp = Hdcp.HDCP_NONE},
                    security_level = 1,
                    track_type = "SD"
                    }
                },
            policy_overrides = new
            {
                can_play = true,
                can_persist = true,
                can_renew = false
            }
            };

            string configuration = JsonConvert.SerializeObject(template);
            return configuration;
        }

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
                    {AssetDeliveryPolicyConfigurationKey.WidevineBaseLicenseAcquisitionUrl, widevineUrl.ToString()}

            };

            // In this case we only specify Dash streaming protocol in the delivery policy,
            // All other protocols will be blocked from streaming.
            var assetDeliveryPolicy = _context.AssetDeliveryPolicies.Create(
                "AssetDeliveryPolicy",
            AssetDeliveryPolicyType.DynamicCommonEncryption,
            AssetDeliveryProtocol.Dash,
            assetDeliveryPolicyConfiguration);


            // Add AssetDelivery Policy to the asset
            asset.DeliveryPolicies.Add(assetDeliveryPolicy);

        }

        /// <summary>
        /// Gets the streaming origin locator.
        /// </summary>
        /// <param name="assets"></param>
        /// <returns></returns>
        static public string GetStreamingOriginLocator(IAsset asset)
        {

            // Get a reference to the streaming manifest file from the  
            // collection of files in the asset.

            var assetFile = asset.AssetFiles.Where(f => f.Name.ToLower().
                         EndsWith(".ism")).
                         FirstOrDefault();

            // Create a 30-day readonly access policy.
            IAccessPolicy policy = _context.AccessPolicies.Create("Streaming policy",
            TimeSpan.FromDays(30),
            AccessPermissions.Read);

            // Create a locator to the streaming content on an origin.
            ILocator originLocator = _context.Locators.CreateLocator(LocatorType.OnDemandOrigin, asset,
            policy,
            DateTime.UtcNow.AddMinutes(-5));

            // Create a URL to the manifest file.
            return originLocator.Path + assetFile.Name;
        }

        static private void JobStateChanged(object sender, JobStateChangedEventArgs e)
        {
            Console.WriteLine(string.Format("{0}\n  State: {1}\n  Time: {2}\n\n",
            ((IJob)sender).Name,
            e.CurrentState,
            DateTime.UtcNow.ToString(@"yyyy_M_d__hh_mm_ss")));
        }

        static private byte[] GetRandomBuffer(int length)
        {
            var returnValue = new byte[length];

            using (var rng =
            new System.Security.Cryptography.RNGCryptoServiceProvider())
            {
            rng.GetBytes(returnValue);
            }

            return returnValue;
        }
        }
    }


## <a name="next-step"></a><span data-ttu-id="1f7ef-203">Następny krok</span><span class="sxs-lookup"><span data-stu-id="1f7ef-203">Next step</span></span>
<span data-ttu-id="1f7ef-204">Przejrzyj ścieżki szkoleniowe dotyczące usługi Media Services.</span><span class="sxs-lookup"><span data-stu-id="1f7ef-204">Review Media Services learning paths.</span></span>

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="1f7ef-205">Przekazywanie opinii</span><span class="sxs-lookup"><span data-stu-id="1f7ef-205">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="see-also"></a><span data-ttu-id="1f7ef-206">Zobacz też</span><span class="sxs-lookup"><span data-stu-id="1f7ef-206">See also</span></span>
[<span data-ttu-id="1f7ef-207">Szyfrowanie CENC przy użyciu technologii Multi-DRM i kontroli dostępu</span><span class="sxs-lookup"><span data-stu-id="1f7ef-207">CENC with Multi-DRM and Access Control</span></span>](media-services-cenc-with-multidrm-access-control.md)

[<span data-ttu-id="1f7ef-208">Konfigurowanie tworzenia pakietów Widevine przy użyciu usługi AMS</span><span class="sxs-lookup"><span data-stu-id="1f7ef-208">Configure Widevine packaging with AMS</span></span>](http://mingfeiy.com/how-to-configure-widevine-packaging-with-azure-media-services)

[<span data-ttu-id="1f7ef-209">Powiadomienie o usługach dostarczania licencji Google Widevine w usłudze Azure Media Services</span><span class="sxs-lookup"><span data-stu-id="1f7ef-209">Announcing Google Widevine license delivery services in Azure Media Services</span></span>](https://azure.microsoft.com/blog/announcing-general-availability-of-google-widevine-license-services/)
