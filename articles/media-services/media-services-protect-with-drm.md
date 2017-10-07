---
title: aaaUsing PlayReady i Widevine dynamicznego szyfrowania common encryption | Dokumentacja firmy Microsoft
description: "Microsoft Azure Media Services umożliwia możesz toodeliver MPEG-DASH, Smooth Streaming i Http-Live-Streaming (HLS) strumieni chronionych z Microsoft PlayReady DRM. Można również toodelivery strumienia DASH szyfrowanego przy Widevine DRM. W tym temacie przedstawiono sposób toodynamically szyfrowanie PlayReady i Widevine DRM."
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
ms.openlocfilehash: 0475e6ec80dcf39eb4e5c4ad4d17f821502951bd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="using-playready-andor-widevine-dynamic-common-encryption"></a><span data-ttu-id="5120d-105">Używanie dynamicznego szyfrowania Common Encryption w usługach PlayReady i Widevine</span><span class="sxs-lookup"><span data-stu-id="5120d-105">Using PlayReady and/or Widevine dynamic common encryption</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="5120d-106">.NET</span><span class="sxs-lookup"><span data-stu-id="5120d-106">.NET</span></span>](media-services-protect-with-drm.md)
> * [<span data-ttu-id="5120d-107">Java</span><span class="sxs-lookup"><span data-stu-id="5120d-107">Java</span></span>](https://github.com/southworkscom/azure-sdk-for-media-services-java-samples)
> * [<span data-ttu-id="5120d-108">PHP</span><span class="sxs-lookup"><span data-stu-id="5120d-108">PHP</span></span>](https://github.com/Azure/azure-sdk-for-php/tree/master/examples/MediaServices)
>
>

<span data-ttu-id="5120d-109">Microsoft Azure Media Services umożliwia toodeliver MPEG-DASH, Smooth Streaming i strumieni HTTP-Live-Streaming (HLS) chronionych przy [Microsoft PlayReady DRM](https://www.microsoft.com/playready/overview/).</span><span class="sxs-lookup"><span data-stu-id="5120d-109">Microsoft Azure Media Services enables you toodeliver MPEG-DASH, Smooth Streaming, and HTTP-Live-Streaming (HLS) streams protected with [Microsoft PlayReady DRM](https://www.microsoft.com/playready/overview/).</span></span> <span data-ttu-id="5120d-110">Można również toodeliver zaszyfrowanych strumienie DASH korzystających z licencji Widevine DRM.</span><span class="sxs-lookup"><span data-stu-id="5120d-110">It also enables you toodeliver encrypted DASH streams with Widevine DRM licenses.</span></span> <span data-ttu-id="5120d-111">Zarówno PlayReady i Widevine są szyfrowane na powitania specyfikacją Common Encryption (ISO/IEC CENC 23001-7).</span><span class="sxs-lookup"><span data-stu-id="5120d-111">Both PlayReady and Widevine are encrypted per hello Common Encryption (ISO/IEC 23001-7 CENC) specification.</span></span> <span data-ttu-id="5120d-112">Można użyć [AMS .NET SDK](https://www.nuget.org/packages/windowsazure.mediaservices/) (począwszy od wersji hello 3.5.1) lub REST API tooconfigure Twojego toouse AssetDeliveryConfiguration Widevine.</span><span class="sxs-lookup"><span data-stu-id="5120d-112">You can use [AMS .NET SDK](https://www.nuget.org/packages/windowsazure.mediaservices/) (starting with hello version 3.5.1) or REST API tooconfigure your AssetDeliveryConfiguration toouse Widevine.</span></span>

<span data-ttu-id="5120d-113">Usługa Media Services udostępnia usługę dostarczania licencji PlayReady i Widevine DRM.</span><span class="sxs-lookup"><span data-stu-id="5120d-113">Media Services provides a service for delivering PlayReady and Widevine DRM licenses.</span></span> <span data-ttu-id="5120d-114">Media Services dostarcza również interfejsy API, które umożliwiają skonfigurowanie hello prawa i ograniczenia, które mają hello PlayReady lub Widevine DRM środowiska uruchomieniowego tooenforce, gdy użytkownik odtwarza chronioną zawartość.</span><span class="sxs-lookup"><span data-stu-id="5120d-114">Media Services also provides APIs that let you configure hello rights and restrictions that you want for hello PlayReady or Widevine DRM runtime tooenforce when a user plays back protected content.</span></span> <span data-ttu-id="5120d-115">Gdy użytkownik zażąda zawartości chronione DRM, hello aplikacja odtwarzacza zażąda licencji z hello AMS licencji usługi.</span><span class="sxs-lookup"><span data-stu-id="5120d-115">When a user requests a DRM protected content, hello player application will request a license from hello AMS license service.</span></span> <span data-ttu-id="5120d-116">Usługa licencjonowania AMS Hello będzie wystawiać player toohello licencji, jeśli jest on autoryzowany.</span><span class="sxs-lookup"><span data-stu-id="5120d-116">hello AMS license service will issue a license toohello player if it is authorized.</span></span> <span data-ttu-id="5120d-117">Licencja PlayReady lub Widevine zawiera klucz odszyfrowujący hello używanego przez powitania klienta player toodecrypt i strumienia hello zawartości.</span><span class="sxs-lookup"><span data-stu-id="5120d-117">A PlayReady or Widevine license contains hello decryption key that can be used by hello client player toodecrypt and stream hello content.</span></span>

<span data-ttu-id="5120d-118">Można również użyć powitania po dostarczania licencji Widevine toohelp partnerów AMS: [Axinom](http://www.axinom.com/press/ibc-axinom-drm-6/), [EZDRM](http://ezdrm.com/), [castLabs](http://castlabs.com/company/partners/azure/).</span><span class="sxs-lookup"><span data-stu-id="5120d-118">You can also use hello following AMS partners toohelp you deliver Widevine licenses: [Axinom](http://www.axinom.com/press/ibc-axinom-drm-6/), [EZDRM](http://ezdrm.com/), [castLabs](http://castlabs.com/company/partners/azure/).</span></span> <span data-ttu-id="5120d-119">Aby uzyskać więcej informacji, zobacz: integracja z [Axinom](media-services-axinom-integration.md) i [castLabs](media-services-castlabs-integration.md).</span><span class="sxs-lookup"><span data-stu-id="5120d-119">For more information, see: integration with [Axinom](media-services-axinom-integration.md) and [castLabs](media-services-castlabs-integration.md).</span></span>

<span data-ttu-id="5120d-120">Usługa Media Services obsługuje wiele sposobów autoryzacji użytkowników, którzy tworzą żądania klucza.</span><span class="sxs-lookup"><span data-stu-id="5120d-120">Media Services supports multiple ways of authorizing users who make key requests.</span></span> <span data-ttu-id="5120d-121">Witaj zasady autoryzacji klucza zawartości może mieć jeden lub więcej ograniczeń: otwarte lub ograniczenie tokenu.</span><span class="sxs-lookup"><span data-stu-id="5120d-121">hello content key authorization policy could have one or more authorization restrictions: open or token restriction.</span></span> <span data-ttu-id="5120d-122">Witaj zasadzie ograniczenia tokenu musi towarzyszyć token wystawiony przez Secure Token Service (STS).</span><span class="sxs-lookup"><span data-stu-id="5120d-122">hello token restricted policy must be accompanied by a token issued by a Secure Token Service (STS).</span></span> <span data-ttu-id="5120d-123">Usługa Media Services obsługuje tokenów w hello [proste tokenów sieci Web](https://msdn.microsoft.com/library/gg185950.aspx#BKMK_2) formatu (SWT) i [JSON Web Token](https://msdn.microsoft.com/library/gg185950.aspx#BKMK_3) formatu (JWT).</span><span class="sxs-lookup"><span data-stu-id="5120d-123">Media Services supports tokens in hello [Simple Web Tokens](https://msdn.microsoft.com/library/gg185950.aspx#BKMK_2) (SWT) format and [JSON Web Token](https://msdn.microsoft.com/library/gg185950.aspx#BKMK_3) (JWT) format.</span></span> <span data-ttu-id="5120d-124">Aby uzyskać więcej informacji zobacz Konfigurowanie hello zawartości zasady autoryzacji klucza.</span><span class="sxs-lookup"><span data-stu-id="5120d-124">For more information, see Configure hello content key’s authorization policy.</span></span>

<span data-ttu-id="5120d-125">tootake korzystać z szyfrowania dynamicznego, należy toohave element zawartości zawierający zestaw plików MP4 wielokrotnej szybkości transmisji bitów lub pliki źródłowe Smooth Streaming wielokrotnej szybkości transmisji bitów.</span><span class="sxs-lookup"><span data-stu-id="5120d-125">tootake advantage of dynamic encryption, you need toohave an asset that contains a set of multi-bitrate MP4 files or multi-bitrate Smooth Streaming source files.</span></span> <span data-ttu-id="5120d-126">Należy również zasady dostarczania hello tooconfigure dla elementu hello zawartości (opisane w dalszej części tego tematu).</span><span class="sxs-lookup"><span data-stu-id="5120d-126">You also need tooconfigure hello delivery policies for hello asset (described later in this topic).</span></span> <span data-ttu-id="5120d-127">Następnie na podstawie hello formatu określonego w hello URL przesyłania strumieniowego, serwer przesyłania strumieniowego na żądanie hello będzie upewnij się, że strumieniu hello jest dostarczany w protokole hello, wybrana.</span><span class="sxs-lookup"><span data-stu-id="5120d-127">Then, based on hello format specified in hello streaming URL, hello On-Demand Streaming server will ensure that hello stream is delivered in hello protocol you have chosen.</span></span> <span data-ttu-id="5120d-128">W związku z tym konieczne toostore i płatności hello pliki w jednym formacie magazynu, a usługa Media Services skompiluje oraz udostępni właściwą odpowiedź HTTP hello, na podstawie żądań klienta.</span><span class="sxs-lookup"><span data-stu-id="5120d-128">As a result, you only need toostore and pay for hello files in a single storage format and Media Services will build and serve hello appropriate HTTP response based on each request from a client.</span></span>

<span data-ttu-id="5120d-129">Ten temat powinien być przydatny toodevelopers, które działają w przypadku aplikacji, które dostarczają zawartość chronioną przy użyciu wielu protokołów DRM, takich jak PlayReady i Widevine.</span><span class="sxs-lookup"><span data-stu-id="5120d-129">This topic would be useful toodevelopers that work on applications that deliver media protected with multiple DRMs, such as PlayReady and Widevine.</span></span> <span data-ttu-id="5120d-130">Witaj temacie pokazano, jak tooconfigure hello usługi dostarczania licencji PlayReady przy użyciu zasad autoryzacji, tak aby tylko autoryzowani klienci mogli odbierać licencje PlayReady lub Widevine.</span><span class="sxs-lookup"><span data-stu-id="5120d-130">hello topic shows you how tooconfigure hello PlayReady license delivery service with authorization policies so that only authorized clients could receive PlayReady or Widevine licenses.</span></span> <span data-ttu-id="5120d-131">Zawiera także sposób toouse szyfrowania PlayReady lub Widevine DRM strumienia DASH.</span><span class="sxs-lookup"><span data-stu-id="5120d-131">It also shows how toouse dynamic encryption encryption with PlayReady or Widevine DRM over DASH.</span></span>

>[!NOTE]
><span data-ttu-id="5120d-132">Po utworzeniu konta usługi AMS **domyślne** punktu końcowego przesyłania strumieniowego w brzmieniu konta tooyour hello **zatrzymane** stanu.</span><span class="sxs-lookup"><span data-stu-id="5120d-132">When your AMS account is created a **default** streaming endpoint is added tooyour account in hello **Stopped** state.</span></span> <span data-ttu-id="5120d-133">przesyłanie strumieniowe zawartości i podejmij korzyści z dynamicznego tworzenia pakietów i dynamicznego szyfrowania toostart hello punktu końcowego przesyłania strumieniowego, z którego mają zostać toostream zawartość ma toobe w hello **systemem** stanu.</span><span class="sxs-lookup"><span data-stu-id="5120d-133">toostart streaming your content and take advantage of dynamic packaging and dynamic encryption, hello streaming endpoint from which you want toostream content has toobe in hello **Running** state.</span></span> 

## <a name="download-sample"></a><span data-ttu-id="5120d-134">Pobieranie przykładu</span><span class="sxs-lookup"><span data-stu-id="5120d-134">Download sample</span></span>
<span data-ttu-id="5120d-135">Możesz pobrać przykładowy hello opisane w tym artykule [tutaj](https://github.com/Azure-Samples/media-services-dotnet-dynamic-encryption-with-drm).</span><span class="sxs-lookup"><span data-stu-id="5120d-135">You can download hello sample described in this article from [here](https://github.com/Azure-Samples/media-services-dotnet-dynamic-encryption-with-drm).</span></span>

## <a name="configuring-dynamic-common-encryption-and-drm-license-delivery-services"></a><span data-ttu-id="5120d-136">Konfigurowanie dynamicznego szyfrowania Common Encryption i usług dostarczania licencji DRM</span><span class="sxs-lookup"><span data-stu-id="5120d-136">Configuring Dynamic Common Encryption and DRM License Delivery Services</span></span>

<span data-ttu-id="5120d-137">Witaj poniżej przedstawiono ogólne kroki, że będzie potrzebny tooperform podczas ochrony swoich elementów zawartości za pomocą PlayReady, za pomocą usługi dostarczania licencji Media Services hello, a także za pomocą szyfrowania dynamicznego.</span><span class="sxs-lookup"><span data-stu-id="5120d-137">hello following are general steps that you would need tooperform when protecting your assets with PlayReady, using hello Media Services license delivery service, and also using dynamic encryption.</span></span>

1. <span data-ttu-id="5120d-138">Utworzenie elementu zawartości i przekazywanie plików do zawartości hello.</span><span class="sxs-lookup"><span data-stu-id="5120d-138">Create an asset and upload files into hello asset.</span></span>
2. <span data-ttu-id="5120d-139">Kodowanie hello zasobu zawierającego hello pliku toohello adaptacyjną szybkością transmisji bitów zestaw MP4.</span><span class="sxs-lookup"><span data-stu-id="5120d-139">Encode hello asset containing hello file toohello adaptive bitrate MP4 set.</span></span>
3. <span data-ttu-id="5120d-140">Utwórz klucz zawartości i skojarz go z algorytmem hello zawartości.</span><span class="sxs-lookup"><span data-stu-id="5120d-140">Create a content key and associate it with hello encoded asset.</span></span> <span data-ttu-id="5120d-141">W usłudze Media Services klucz zawartości hello zawiera klucz szyfrowania hello zasobów.</span><span class="sxs-lookup"><span data-stu-id="5120d-141">In Media Services, hello content key contains hello asset’s encryption key.</span></span>
4. <span data-ttu-id="5120d-142">Skonfiguruj zasady autoryzacji klucza zawartości hello.</span><span class="sxs-lookup"><span data-stu-id="5120d-142">Configure hello content key’s authorization policy.</span></span> <span data-ttu-id="5120d-143">zasady autoryzacji klucza zawartości Hello musi być skonfigurowane przez użytkownika i spełnione przez klienta hello w kolejności hello zawartości toobe klucza dostarczonego toohello klienta.</span><span class="sxs-lookup"><span data-stu-id="5120d-143">hello content key authorization policy must be configured by you and met by hello client in order for hello content key toobe delivered toohello client.</span></span>

    <span data-ttu-id="5120d-144">Podczas tworzenia zasady autoryzacji klucza zawartości hello, potrzebujesz następujących hello toospecify: dostarczania — metoda (PlayReady lub Widevine), ograniczenia (otwarte lub tokenu) i typu klucza dostawy toohello określonych informacji, który definiuje sposób dostawy klucza hello Klient toohello ([PlayReady](media-services-playready-license-template-overview.md) lub [Widevine](media-services-widevine-license-template-overview.md) szablon licencji).</span><span class="sxs-lookup"><span data-stu-id="5120d-144">When creating hello content key authorization policy, you need toospecify hello following: delivery method (PlayReady or Widevine), restrictions (open or token), and information specific toohello key delivery type that defines how hello key is delivered toohello client ([PlayReady](media-services-playready-license-template-overview.md) or [Widevine](media-services-widevine-license-template-overview.md) license template).</span></span>

5. <span data-ttu-id="5120d-145">Skonfiguruj zasady dostarczania hello zasobu.</span><span class="sxs-lookup"><span data-stu-id="5120d-145">Configure hello delivery policy for an asset.</span></span> <span data-ttu-id="5120d-146">Konfiguracja zasady dostarczania Hello obejmuje: Protokół dostarczania (na przykład MPEG DASH, HLS, Smooth Streaming lub wszystkie), hello typ szyfrowania dynamicznego (na przykład Common Encryption) PlayReady lub Widevine adres URL pozyskiwania licencji.</span><span class="sxs-lookup"><span data-stu-id="5120d-146">hello delivery policy configuration includes: delivery protocol (for example, MPEG DASH, HLS, Smooth Streaming or all), hello type of dynamic encryption (for example, Common Encryption), PlayReady or Widevine license acquisition URL.</span></span>

    <span data-ttu-id="5120d-147">Protokół tooeach różnych zasad można zastosować na powitania elementu zawartości.</span><span class="sxs-lookup"><span data-stu-id="5120d-147">You could apply different policy tooeach protocol on hello same asset.</span></span> <span data-ttu-id="5120d-148">Na przykład można zastosować szyfrowanie PlayReady tooSmooth/DASH i tooHLS szyfrowanie AES Envelope.</span><span class="sxs-lookup"><span data-stu-id="5120d-148">For example, you could apply PlayReady encryption tooSmooth/DASH and AES Envelope tooHLS.</span></span> <span data-ttu-id="5120d-149">Wszystkie protokoły, które nie są zdefiniowane w zasadzie dostarczania (na przykład dodać jedną zasadę, która tylko określa hello protokół HLS), zostanie zablokowany przesyłania strumieniowego.</span><span class="sxs-lookup"><span data-stu-id="5120d-149">Any protocols that are not defined in a delivery policy (for example, you add a single policy that only specifies HLS as hello protocol) will be blocked from streaming.</span></span> <span data-ttu-id="5120d-150">toothis wyjątek Hello jest, jeśli masz nie zdefiniowano zasad dostarczania elementów zawartości.</span><span class="sxs-lookup"><span data-stu-id="5120d-150">hello exception toothis is if you have no asset delivery policy defined at all.</span></span> <span data-ttu-id="5120d-151">Następnie wszystkie protokoły mogą być przesyłane hello Wyczyść.</span><span class="sxs-lookup"><span data-stu-id="5120d-151">Then, all protocols will be allowed in hello clear.</span></span>

6. <span data-ttu-id="5120d-152">Utwórz Lokalizator OnDemand w kolejności tooget adresu URL przesyłania strumieniowego.</span><span class="sxs-lookup"><span data-stu-id="5120d-152">Create an OnDemand locator in order tooget a streaming URL.</span></span>

<span data-ttu-id="5120d-153">Znajduje się pełny przykład .NET na końcu hello hello tematu.</span><span class="sxs-lookup"><span data-stu-id="5120d-153">You will find a complete .NET example at hello end of hello topic.</span></span>

<span data-ttu-id="5120d-154">powitania po obraz pokazuje opisany wyżej przepływ pracy hello.</span><span class="sxs-lookup"><span data-stu-id="5120d-154">hello following image demonstrates hello workflow described above.</span></span> <span data-ttu-id="5120d-155">W tym miejscu hello token jest używany do uwierzytelniania.</span><span class="sxs-lookup"><span data-stu-id="5120d-155">Here hello token is used for authentication.</span></span>

![Ochrona za pomocą PlayReady](./media/media-services-content-protection-overview/media-services-content-protection-with-drm.png)

<span data-ttu-id="5120d-157">Witaj pozostałej części tego tematu zawiera szczegółowe wyjaśnienia, przykłady kodu i tootopics łącza, które pokazują, jak tooachieve hello zadania opisane powyżej.</span><span class="sxs-lookup"><span data-stu-id="5120d-157">hello rest of this topic provides detailed explanations, code examples, and links tootopics that show you how tooachieve hello tasks described above.</span></span>

## <a name="current-limitations"></a><span data-ttu-id="5120d-158">Bieżące ograniczenia</span><span class="sxs-lookup"><span data-stu-id="5120d-158">Current limitations</span></span>
<span data-ttu-id="5120d-159">Jeśli w przypadku dodania lub zaktualizowania zasad dostarczania elementów zawartości, należy usunąć hello skojarzony Lokalizator (jeśli istnieje) i utworzyć nowy.</span><span class="sxs-lookup"><span data-stu-id="5120d-159">If you add or update an asset delivery policy, you must delete hello associated locator (if any) and create a new locator.</span></span>

<span data-ttu-id="5120d-160">Ograniczenie w przypadku szyfrowania przy użyciu metody Widevine dla usługi Azure Media Services: obecnie nie jest obsługiwanych wiele kluczy zawartości.</span><span class="sxs-lookup"><span data-stu-id="5120d-160">Limitation when encrypting with Widevine with Azure Media Services: currently, multiple content keys are not supported.</span></span>

## <a name="create-an-asset-and-upload-files-into-hello-asset"></a><span data-ttu-id="5120d-161">Utworzenie elementu zawartości i przekazywanie plików do zawartości hello</span><span class="sxs-lookup"><span data-stu-id="5120d-161">Create an asset and upload files into hello asset</span></span>
<span data-ttu-id="5120d-162">W kolejności toomanage, kodowania i przesyłania strumieniowego filmów, należy najpierw przekazać zawartość do usługi Microsoft Azure Media Services.</span><span class="sxs-lookup"><span data-stu-id="5120d-162">In order toomanage, encode, and stream your videos, you must first upload your content into Microsoft Azure Media Services.</span></span> <span data-ttu-id="5120d-163">Po przekazaniu plików zawartość jest bezpiecznie przechowywana w chmurze powitania dla dalszego przetwarzania i przesyłania strumieniowego.</span><span class="sxs-lookup"><span data-stu-id="5120d-163">Once uploaded, your content is stored securely in hello cloud for further processing and streaming.</span></span>

<span data-ttu-id="5120d-164">Aby uzyskać szczegółowe informacje, zobacz artykuł [Upload Files into a Media Services account](media-services-dotnet-upload-files.md) (Przekazywanie plików na konto usługi Media Services).</span><span class="sxs-lookup"><span data-stu-id="5120d-164">For detailed information, see [Upload Files into a Media Services account](media-services-dotnet-upload-files.md).</span></span>

## <a name="encode-hello-asset-containing-hello-file-toohello-adaptive-bitrate-mp4-set"></a><span data-ttu-id="5120d-165">Kodowanie hello zasobu zawierającego hello pliku toohello adaptacyjną szybkością transmisji bitów zestaw MP4</span><span class="sxs-lookup"><span data-stu-id="5120d-165">Encode hello asset containing hello file toohello adaptive bitrate MP4 set</span></span>
<span data-ttu-id="5120d-166">W przypadku szyfrowania dynamicznego wystarczy jest toocreate element zawartości zawierający zestaw plików MP4 wielokrotnej szybkości transmisji bitów lub pliki źródłowe Smooth Streaming wielokrotnej szybkości transmisji bitów.</span><span class="sxs-lookup"><span data-stu-id="5120d-166">With dynamic encryption all you need is toocreate an asset that contains a set of multi-bitrate MP4 files or multi-bitrate Smooth Streaming source files.</span></span> <span data-ttu-id="5120d-167">Następnie na podstawie hello formatu określonego w manifeście hello fragmentu żądania, hello Streaming na żądanie serwera zapewni odbierania strumienia hello w protokole hello, wybrana.</span><span class="sxs-lookup"><span data-stu-id="5120d-167">Then, based on hello specified format in hello manifest and fragment request, hello On-Demand Streaming server will ensure that you receive hello stream in hello protocol you have chosen.</span></span> <span data-ttu-id="5120d-168">W związku z tym konieczne toostore i płatności hello pliki w jednym formacie magazynu, a usługa Media Services skompiluje oraz udostępni właściwą odpowiedź hello na podstawie żądań klienta.</span><span class="sxs-lookup"><span data-stu-id="5120d-168">As a result, you only need toostore and pay for hello files in single storage format and Media Services service will build and serve hello appropriate response based on requests from a client.</span></span> <span data-ttu-id="5120d-169">Aby uzyskać więcej informacji, zobacz hello [omówienie tworzenia pakietów dynamicznych](media-services-dynamic-packaging-overview.md) tematu.</span><span class="sxs-lookup"><span data-stu-id="5120d-169">For more information, see hello [Dynamic Packaging Overview](media-services-dynamic-packaging-overview.md) topic.</span></span>

<span data-ttu-id="5120d-170">Aby uzyskać instrukcje dotyczące tooencode, zobacz [jak tooencode zasobów przy użyciu standardu Media Encoder Standard](media-services-dotnet-encode-with-media-encoder-standard.md).</span><span class="sxs-lookup"><span data-stu-id="5120d-170">For instructions on how tooencode, see [How tooencode an asset using Media Encoder Standard](media-services-dotnet-encode-with-media-encoder-standard.md).</span></span>

## <span data-ttu-id="5120d-171"><a id="create_contentkey"></a>Utwórz klucz zawartości i powiązać ją z hello zakodowane zasobów</span><span class="sxs-lookup"><span data-stu-id="5120d-171"><a id="create_contentkey"></a>Create a content key and associate it with hello encoded asset</span></span>
<span data-ttu-id="5120d-172">W usłudze Media Services klucz zawartości hello zawiera klucz hello, które mają tooencrypt zasób z.</span><span class="sxs-lookup"><span data-stu-id="5120d-172">In Media Services, hello content key contains hello key that you want tooencrypt an asset with.</span></span>

<span data-ttu-id="5120d-173">Aby uzyskać szczegółowe informacje, zobacz artykuł [Create content key](media-services-dotnet-create-contentkey.md) (Tworzenie klucza zawartości).</span><span class="sxs-lookup"><span data-stu-id="5120d-173">For detailed information, see [Create content key](media-services-dotnet-create-contentkey.md).</span></span>

## <span data-ttu-id="5120d-174"><a id="configure_key_auth_policy"></a>Skonfiguruj zasady autoryzacji klucza zawartości hello</span><span class="sxs-lookup"><span data-stu-id="5120d-174"><a id="configure_key_auth_policy"></a>Configure hello content key’s authorization policy</span></span>
<span data-ttu-id="5120d-175">Usługa Media Services obsługuje wiele sposobów uwierzytelniania użytkowników, którzy tworzą żądania klucza.</span><span class="sxs-lookup"><span data-stu-id="5120d-175">Media Services supports multiple ways of authenticating users who make key requests.</span></span> <span data-ttu-id="5120d-176">zasady autoryzacji klucza zawartości Hello musi być skonfigurowane przez użytkownika i spełniać powitania klienta (odtwarzacz), aby hello toobe klucza dostarczyć toohello klienta.</span><span class="sxs-lookup"><span data-stu-id="5120d-176">hello content key authorization policy must be configured by you and met by hello client (player) in order for hello key toobe delivered toohello client.</span></span> <span data-ttu-id="5120d-177">Witaj zasady autoryzacji klucza zawartości może mieć jeden lub więcej ograniczeń: otwarte lub ograniczenie tokenu.</span><span class="sxs-lookup"><span data-stu-id="5120d-177">hello content key authorization policy could have one or more authorization restrictions: open or token restriction.</span></span>

<span data-ttu-id="5120d-178">Aby uzyskać więcej informacji, zobacz artykuł [Configure Content Key Authorization Policy](media-services-dotnet-configure-content-key-auth-policy.md#playready-dynamic-encryption) (Konfigurowanie zasad autoryzacji klucza zawartości).</span><span class="sxs-lookup"><span data-stu-id="5120d-178">For detailed information, see [Configure Content Key Authorization Policy](media-services-dotnet-configure-content-key-auth-policy.md#playready-dynamic-encryption).</span></span>

## <span data-ttu-id="5120d-179"><a id="configure_asset_delivery_policy"></a>Konfigurowanie zasad dostarczania elementów zawartości</span><span class="sxs-lookup"><span data-stu-id="5120d-179"><a id="configure_asset_delivery_policy"></a>Configure asset delivery policy</span></span>
<span data-ttu-id="5120d-180">Skonfiguruj zasady dostarczania powitania dla zawartości.</span><span class="sxs-lookup"><span data-stu-id="5120d-180">Configure hello delivery policy for your asset.</span></span> <span data-ttu-id="5120d-181">Obejmuje kilka rzeczy, które hello Konfiguracja zasady dostarczania zasobów:</span><span class="sxs-lookup"><span data-stu-id="5120d-181">Some things that hello asset delivery policy configuration includes:</span></span>

* <span data-ttu-id="5120d-182">Witaj URL pozyskiwania licencji DRM.</span><span class="sxs-lookup"><span data-stu-id="5120d-182">hello DRM license acquisition URL.</span></span>
* <span data-ttu-id="5120d-183">Witaj Protokół dostarczania elementów zawartości (na przykład MPEG DASH, HLS, Smooth Streaming lub wszystkie).</span><span class="sxs-lookup"><span data-stu-id="5120d-183">hello asset delivery protocol (for example, MPEG DASH, HLS, Smooth Streaming or all).</span></span>
* <span data-ttu-id="5120d-184">Witaj typ szyfrowania dynamicznego (w tym przypadku Common Encryption).</span><span class="sxs-lookup"><span data-stu-id="5120d-184">hello type of dynamic encryption (in this case, Common Encryption).</span></span>

<span data-ttu-id="5120d-185">Aby uzyskać szczegółowe informacje, zobacz artykuł [Configure asset delivery policy](media-services-rest-configure-asset-delivery-policy.md) (Konfigurowanie zasad dostarczania elementów zawartości).</span><span class="sxs-lookup"><span data-stu-id="5120d-185">For detailed information, see [Configure asset delivery policy ](media-services-rest-configure-asset-delivery-policy.md).</span></span>

## <span data-ttu-id="5120d-186"><a id="create_locator"></a>Utwórz Lokalizator OnDemand przesyłania strumieniowego w kolejności tooget adresu URL przesyłania strumieniowego</span><span class="sxs-lookup"><span data-stu-id="5120d-186"><a id="create_locator"></a>Create an OnDemand streaming locator in order tooget a streaming URL</span></span>
<span data-ttu-id="5120d-187">Konieczne będzie tooprovide użytkownika z hello przesyłania strumieniowego adres URL dla Smooth, DASH lub HLS.</span><span class="sxs-lookup"><span data-stu-id="5120d-187">You will need tooprovide your user with hello streaming URL for Smooth, DASH or HLS.</span></span>

> [!NOTE]
> <span data-ttu-id="5120d-188">W przypadku dodania lub zaktualizowania zasad dostarczania elementów zawartości należy usunąć skojarzony lokalizator (jeśli istnieje) i utworzyć nowy.</span><span class="sxs-lookup"><span data-stu-id="5120d-188">If you add or update your asset’s delivery policy, you must delete an existing locator (if any) and create a new locator.</span></span>
>
>

<span data-ttu-id="5120d-189">Aby uzyskać instrukcje dotyczące sposobu toopublish zasobów i kompilacji adresu URL przesyłania strumieniowego, zobacz [zbudować adresu URL przesyłania strumieniowego](media-services-deliver-streaming-content.md).</span><span class="sxs-lookup"><span data-stu-id="5120d-189">For instructions on how toopublish an asset and build a streaming URL, see [Build a streaming URL](media-services-deliver-streaming-content.md).</span></span>

## <a name="get-a-test-token"></a><span data-ttu-id="5120d-190">Pobieranie tokenu testowego</span><span class="sxs-lookup"><span data-stu-id="5120d-190">Get a test token</span></span>
<span data-ttu-id="5120d-191">Pobierz token testowy, oparte na powitania ograniczenia tokenu użytego do hello zasady autoryzacji klucza.</span><span class="sxs-lookup"><span data-stu-id="5120d-191">Get a test token based on hello token restriction that was used for hello key authorization policy.</span></span>

    // Deserializes a string containing an Xml representation of a TokenRestrictionTemplate
    // back into a TokenRestrictionTemplate class instance.
    TokenRestrictionTemplate tokenTemplate =
        TokenRestrictionTemplateSerializer.Deserialize(tokenTemplateString);

    // Generate a test token based on hello data in hello given TokenRestrictionTemplate.
    //hello GenerateTestToken method returns hello token without hello word “Bearer” in front
    //so you have tooadd it in front of hello token string.
    string testToken = TokenRestrictionTemplateSerializer.GenerateTestToken(tokenTemplate);
    Console.WriteLine("hello authorization token is:\nBearer {0}", testToken);


<span data-ttu-id="5120d-192">Można użyć hello [AMS Player](http://amsplayer.azurewebsites.net/azuremediaplayer.html) tootest strumienia.</span><span class="sxs-lookup"><span data-stu-id="5120d-192">You can use hello [AMS Player](http://amsplayer.azurewebsites.net/azuremediaplayer.html) tootest your stream.</span></span>

## <a name="create-and-configure-a-visual-studio-project"></a><span data-ttu-id="5120d-193">Tworzenie i konfigurowanie projektu programu Visual Studio</span><span class="sxs-lookup"><span data-stu-id="5120d-193">Create and configure a Visual Studio project</span></span>

1. <span data-ttu-id="5120d-194">Konfigurowanie środowiska projektowego i wypełnić plik app.config hello o informacje dotyczące połączenia, zgodnie z opisem w [tworzenia usługi Media Services z platformą .NET](media-services-dotnet-how-to-use.md).</span><span class="sxs-lookup"><span data-stu-id="5120d-194">Set up your development environment and populate hello app.config file with connection information, as described in [Media Services development with .NET](media-services-dotnet-how-to-use.md).</span></span> 
2. <span data-ttu-id="5120d-195">Dodaj następujące elementy zbyt hello**appSettings** zdefiniowane w pliku app.config:</span><span class="sxs-lookup"><span data-stu-id="5120d-195">Add hello following elements too**appSettings** defined in your app.config file:</span></span>

        <add key="Issuer" value="http://testacs.com"/>
        <add key="Audience" value="urn:test"/>

## <a name="example"></a><span data-ttu-id="5120d-196">Przykład</span><span class="sxs-lookup"><span data-stu-id="5120d-196">Example</span></span>

<span data-ttu-id="5120d-197">Witaj poniższym przykładzie pokazano funkcje wprowadzone w programie Azure Media Services SDK dla platformy .net — wersja 3.5.2 (w szczególności hello możliwości toodefine Widevine licencji szablonu i żądania licencji Widevine z usługi Azure Media Services).</span><span class="sxs-lookup"><span data-stu-id="5120d-197">hello following sample demonstrates functionality that was introduced in Azure Media Services SDK for .Net -Version 3.5.2 (specifically, hello ability toodefine a Widevine license template and request a Widevine license from Azure Media Services).</span></span>

<span data-ttu-id="5120d-198">Zastąp hello kodu w pliku Program.cs kodem hello przedstawionym w tej sekcji.</span><span class="sxs-lookup"><span data-stu-id="5120d-198">Overwrite hello code in your Program.cs file with hello code shown in this section.</span></span>

>[!NOTE]
><span data-ttu-id="5120d-199">Limit różnych zasad usługi AMS wynosi 1 000 000 (na przykład zasad lokalizatorów lub ContentKeyAuthorizationPolicy).</span><span class="sxs-lookup"><span data-stu-id="5120d-199">There is a limit of 1,000,000 policies for different AMS policies (for example, for Locator policy or ContentKeyAuthorizationPolicy).</span></span> <span data-ttu-id="5120d-200">Należy używać hello tym samym identyfikatorze zasad, jeśli używasz zawsze hello sam dni / dostęp uprawnień, na przykład zasady dla lokalizatorów, które są przeznaczone tooremain w miejscu przez długi czas (zasady — przekazywanie).</span><span class="sxs-lookup"><span data-stu-id="5120d-200">You should use hello same policy ID if you are always using hello same days / access permissions, for example, policies for locators that are intended tooremain in place for a long time (non-upload policies).</span></span> <span data-ttu-id="5120d-201">Aby uzyskać więcej informacji, zobacz [ten](media-services-dotnet-manage-entities.md#limit-access-policies) temat.</span><span class="sxs-lookup"><span data-stu-id="5120d-201">For more information, see [this](media-services-dotnet-manage-entities.md#limit-access-policies) topic.</span></span>

<span data-ttu-id="5120d-202">Upewnij się, że zmienne tooupdate toopoint toofolders gdzie znajdują się pliki danych wejściowych.</span><span class="sxs-lookup"><span data-stu-id="5120d-202">Make sure tooupdate variables toopoint toofolders where your input files are located.</span></span>

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
        // Read values from hello App.config file.
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
            Console.WriteLine("Created key {0} for hello asset {1} ", key.Id, encodedAsset.Id);
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

            // Generate a test token based on hello hello data in hello given TokenRestrictionTemplate.
            // Note, you need toopass hello key id Guid because we specified
            // TokenClaim.ContentKeyIdentifierClaim in during hello creation of TokenRestrictionTemplate.
            Guid rawkey = EncryptionUtils.GetKeyIdAsGuid(key.Id);
            string testToken = TokenRestrictionTemplateSerializer.GenerateTestToken(tokenTemplate, null, rawkey,
                                        DateTime.UtcNow.AddDays(365));
            Console.WriteLine("hello authorization token is:\nBearer {0}", testToken);
            Console.WriteLine();
            }

            // You can use hello http://amsplayer.azurewebsites.net/azuremediaplayer.html player tootest streams.
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

            IJob job = _context.Jobs.Create(String.Format("Encoding into Mp4 {0} too{1}",
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

            // Associate hello key with hello asset.
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
            // Associate hello content key authorization policy with hello content key.
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
                    {AssetDeliveryPolicyConfigurationKey.WidevineBaseLicenseAcquisitionUrl, widevineUrl.ToString()}

            };

            // In this case we only specify Dash streaming protocol in hello delivery policy,
            // All other protocols will be blocked from streaming.
            var assetDeliveryPolicy = _context.AssetDeliveryPolicies.Create(
                "AssetDeliveryPolicy",
            AssetDeliveryPolicyType.DynamicCommonEncryption,
            AssetDeliveryProtocol.Dash,
            assetDeliveryPolicyConfiguration);


            // Add AssetDelivery Policy toohello asset
            asset.DeliveryPolicies.Add(assetDeliveryPolicy);

        }

        /// <summary>
        /// Gets hello streaming origin locator.
        /// </summary>
        /// <param name="assets"></param>
        /// <returns></returns>
        static public string GetStreamingOriginLocator(IAsset asset)
        {

            // Get a reference toohello streaming manifest file from hello  
            // collection of files in hello asset.

            var assetFile = asset.AssetFiles.Where(f => f.Name.ToLower().
                         EndsWith(".ism")).
                         FirstOrDefault();

            // Create a 30-day readonly access policy.
            IAccessPolicy policy = _context.AccessPolicies.Create("Streaming policy",
            TimeSpan.FromDays(30),
            AccessPermissions.Read);

            // Create a locator toohello streaming content on an origin.
            ILocator originLocator = _context.Locators.CreateLocator(LocatorType.OnDemandOrigin, asset,
            policy,
            DateTime.UtcNow.AddMinutes(-5));

            // Create a URL toohello manifest file.
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


## <a name="next-step"></a><span data-ttu-id="5120d-203">Następny krok</span><span class="sxs-lookup"><span data-stu-id="5120d-203">Next step</span></span>
<span data-ttu-id="5120d-204">Przejrzyj ścieżki szkoleniowe dotyczące usługi Media Services.</span><span class="sxs-lookup"><span data-stu-id="5120d-204">Review Media Services learning paths.</span></span>

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="5120d-205">Przekazywanie opinii</span><span class="sxs-lookup"><span data-stu-id="5120d-205">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="see-also"></a><span data-ttu-id="5120d-206">Zobacz też</span><span class="sxs-lookup"><span data-stu-id="5120d-206">See also</span></span>
[<span data-ttu-id="5120d-207">Szyfrowanie CENC przy użyciu technologii Multi-DRM i kontroli dostępu</span><span class="sxs-lookup"><span data-stu-id="5120d-207">CENC with Multi-DRM and Access Control</span></span>](media-services-cenc-with-multidrm-access-control.md)

[<span data-ttu-id="5120d-208">Konfigurowanie tworzenia pakietów Widevine przy użyciu usługi AMS</span><span class="sxs-lookup"><span data-stu-id="5120d-208">Configure Widevine packaging with AMS</span></span>](http://mingfeiy.com/how-to-configure-widevine-packaging-with-azure-media-services)

[<span data-ttu-id="5120d-209">Powiadomienie o usługach dostarczania licencji Google Widevine w usłudze Azure Media Services</span><span class="sxs-lookup"><span data-stu-id="5120d-209">Announcing Google Widevine license delivery services in Azure Media Services</span></span>](https://azure.microsoft.com/blog/announcing-general-availability-of-google-widevine-license-services/)
