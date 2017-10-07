---
title: "dynamiczne aaaUsing AES-128 szyfrowania i klucz usługi dostarczania | Dokumentacja firmy Microsoft"
description: "Microsoft Azure Media Services umożliwia toodeliver możesz zawartości zaszyfrowane za pomocą kluczy szyfrowania AES 128-bitowego. Usługa Media Services udostępnia również hello usługi dostarczania klucza, która dostarcza użytkownikom tooauthorized klucze szyfrowania. W tym temacie przedstawiono sposób toodynamically szyfrowania z AES-128 i korzystanie z usługi dostarczania klucza hello."
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: 4d2c10af-9ee0-408f-899b-33fa4c1d89b9
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/25/2017
ms.author: juliako
ms.openlocfilehash: cb1b413ec2ba79f7437464099cf72236ab93f312
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="using-aes-128-dynamic-encryption-and-key-delivery-service"></a><span data-ttu-id="686f0-105">Za pomocą dynamicznego szyfrowania AES-128 i usługi dostarczania klucza</span><span class="sxs-lookup"><span data-stu-id="686f0-105">Using AES-128 dynamic encryption and key delivery service</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="686f0-106">.NET</span><span class="sxs-lookup"><span data-stu-id="686f0-106">.NET</span></span>](media-services-protect-with-aes128.md)
> * [<span data-ttu-id="686f0-107">Java</span><span class="sxs-lookup"><span data-stu-id="686f0-107">Java</span></span>](https://github.com/southworkscom/azure-sdk-for-media-services-java-samples)
> * [<span data-ttu-id="686f0-108">PHP</span><span class="sxs-lookup"><span data-stu-id="686f0-108">PHP</span></span>](https://github.com/Azure/azure-sdk-for-php/tree/master/examples/MediaServices)
> 
> 

## <a name="overview"></a><span data-ttu-id="686f0-109">Omówienie</span><span class="sxs-lookup"><span data-stu-id="686f0-109">Overview</span></span>
> [!NOTE]
> <span data-ttu-id="686f0-110">Zobacz [to](https://channel9.msdn.com/Shows/Azure-Friday/Azure-Media-Services-Protecting-your-Media-Content-with-AES-Encryption) wideo omówienie sposobu tooprotect multimediów zawartości z szyfrowania AES.</span><span class="sxs-lookup"><span data-stu-id="686f0-110">See [this](https://channel9.msdn.com/Shows/Azure-Friday/Azure-Media-Services-Protecting-your-Media-Content-with-AES-Encryption) video for an overview of how tooprotect your Media Content with AES encryption.</span></span>
> 
> 

<span data-ttu-id="686f0-111">Microsoft Azure Media Services umożliwia toodeliver Http-Live-Streaming (HLS) i płynnego przesyłania przesyłane zaszyfrowane z Standard AES (Advanced Encryption) (przy użyciu kluczy szyfrowania 128-bitowe).</span><span class="sxs-lookup"><span data-stu-id="686f0-111">Microsoft Azure Media Services enables you toodeliver Http-Live-Streaming (HLS) and Smooth Streams encrypted with Advanced Encryption Standard (AES) (using 128-bit encryption keys).</span></span> <span data-ttu-id="686f0-112">Usługa Media Services udostępnia również hello usługi dostarczania klucza, która dostarcza użytkownikom tooauthorized klucze szyfrowania.</span><span class="sxs-lookup"><span data-stu-id="686f0-112">Media Services also provides hello Key Delivery service that delivers encryption keys tooauthorized users.</span></span> <span data-ttu-id="686f0-113">Jeśli chcesz dla usługi Media Services tooencrypt zasób, muszą tooassociate klucz szyfrowania z zasobów hello i również skonfigurować zasady autoryzacji klucza hello.</span><span class="sxs-lookup"><span data-stu-id="686f0-113">If you want for Media Services tooencrypt an asset, you need tooassociate an encryption key with hello asset and also configure authorization policies for hello key.</span></span> <span data-ttu-id="686f0-114">Gdy odtwarzacza zażąda strumienia, usługa Media Services używa hello określony toodynamically klucza szyfrowania zawartości przy użyciu szyfrowania AES.</span><span class="sxs-lookup"><span data-stu-id="686f0-114">When a stream is requested by a player, Media Services uses hello specified key toodynamically encrypt your content using AES encryption.</span></span> <span data-ttu-id="686f0-115">toodecrypt hello strumienia, hello odtwarzacza zażąda hello klucza z usługi dostarczania klucza hello.</span><span class="sxs-lookup"><span data-stu-id="686f0-115">toodecrypt hello stream, hello player will request hello key from hello key delivery service.</span></span> <span data-ttu-id="686f0-116">toodecide czy hello użytkownik jest autoryzowany tooget hello klucza, usługi hello ocenia zasady autoryzacji hello określonych hello klucza.</span><span class="sxs-lookup"><span data-stu-id="686f0-116">toodecide whether or not hello user is authorized tooget hello key, hello service evaluates hello authorization policies that you specified for hello key.</span></span>

<span data-ttu-id="686f0-117">Usługa Media Services obsługuje wiele sposobów uwierzytelniania użytkowników, którzy tworzą żądania klucza.</span><span class="sxs-lookup"><span data-stu-id="686f0-117">Media Services supports multiple ways of authenticating users who make key requests.</span></span> <span data-ttu-id="686f0-118">Witaj zasady autoryzacji klucza zawartości może mieć jeden lub więcej ograniczeń: otwarte lub ograniczenie tokenu.</span><span class="sxs-lookup"><span data-stu-id="686f0-118">hello content key authorization policy could have one or more authorization restrictions: open or token restriction.</span></span> <span data-ttu-id="686f0-119">Witaj zasadzie ograniczenia tokenu musi towarzyszyć token wystawiony przez Secure Token Service (STS).</span><span class="sxs-lookup"><span data-stu-id="686f0-119">hello token restricted policy must be accompanied by a token issued by a Secure Token Service (STS).</span></span> <span data-ttu-id="686f0-120">Usługa Media Services obsługuje tokenów w hello [proste tokenów sieci Web](https://msdn.microsoft.com/library/gg185950.aspx#BKMK_2) formatu (SWT) i [JSON Web Token](https://msdn.microsoft.com/library/gg185950.aspx#BKMK_3) formatu (JWT).</span><span class="sxs-lookup"><span data-stu-id="686f0-120">Media Services supports tokens in hello [Simple Web Tokens](https://msdn.microsoft.com/library/gg185950.aspx#BKMK_2) (SWT) format and [JSON Web Token](https://msdn.microsoft.com/library/gg185950.aspx#BKMK_3) (JWT) format.</span></span> <span data-ttu-id="686f0-121">Aby uzyskać więcej informacji, zobacz [Skonfiguruj zasady autoryzacji klucza zawartości hello](media-services-protect-with-aes128.md#configure_key_auth_policy).</span><span class="sxs-lookup"><span data-stu-id="686f0-121">For more information, see [Configure hello content key’s authorization policy](media-services-protect-with-aes128.md#configure_key_auth_policy).</span></span>

<span data-ttu-id="686f0-122">tootake korzystać z szyfrowania dynamicznego, należy toohave element zawartości zawierający zestaw plików MP4 wielokrotnej szybkości transmisji bitów lub pliki źródłowe Smooth Streaming wielokrotnej szybkości transmisji bitów.</span><span class="sxs-lookup"><span data-stu-id="686f0-122">tootake advantage of dynamic encryption, you need toohave an asset that contains a set of multi-bitrate MP4 files or multi-bitrate Smooth Streaming source files.</span></span> <span data-ttu-id="686f0-123">Należy również zasady dostarczania hello tooconfigure dla elementu hello zawartości (opisane w dalszej części tego tematu).</span><span class="sxs-lookup"><span data-stu-id="686f0-123">You also need tooconfigure hello delivery policy for hello asset (described later in this topic).</span></span> <span data-ttu-id="686f0-124">Następnie na podstawie hello formatu określonego w hello URL przesyłania strumieniowego, serwer przesyłania strumieniowego na żądanie hello będzie upewnij się, że strumieniu hello jest dostarczany w protokole hello, wybrana.</span><span class="sxs-lookup"><span data-stu-id="686f0-124">Then, based on hello format specified in hello streaming URL, hello On-Demand Streaming server will ensure that hello stream is delivered in hello protocol you have chosen.</span></span> <span data-ttu-id="686f0-125">W związku z tym konieczne toostore i płatności hello pliki w jednym formacie magazynu, a usługa Media Services skompiluje oraz udostępni właściwą odpowiedź hello na podstawie żądań klienta.</span><span class="sxs-lookup"><span data-stu-id="686f0-125">As a result, you only need toostore and pay for hello files in single storage format and Media Services service will build and serve hello appropriate response based on requests from a client.</span></span>

<span data-ttu-id="686f0-126">Ten temat powinien być przydatny toodevelopers, że działają w przypadku aplikacji dostarczanie multimediów chronionych.</span><span class="sxs-lookup"><span data-stu-id="686f0-126">This topic would be useful toodevelopers that work on applications that deliver protected media.</span></span> <span data-ttu-id="686f0-127">Witaj temacie pokazano, jak tooconfigure hello usługi dostarczania klucza przy użyciu zasad autoryzacji, aby tylko autoryzowani klienci mogli odbierać hello kluczy szyfrowania.</span><span class="sxs-lookup"><span data-stu-id="686f0-127">hello topic shows you how tooconfigure hello key delivery service with authorization policies so that only authorized clients could receive hello encryption keys.</span></span> <span data-ttu-id="686f0-128">Zawiera także sposób toouse szyfrowania dynamicznego.</span><span class="sxs-lookup"><span data-stu-id="686f0-128">It also shows how toouse dynamic encryption.</span></span>


## <a name="aes-128-dynamic-encryption-and-key-delivery-service-workflow"></a><span data-ttu-id="686f0-129">Przepływ pracy usługi dostarczania klucza i dynamicznego szyfrowania AES-128</span><span class="sxs-lookup"><span data-stu-id="686f0-129">AES-128 Dynamic Encryption and Key Delivery Service Workflow</span></span>

<span data-ttu-id="686f0-130">Witaj poniżej przedstawiono ogólne kroki, że będzie potrzebny tooperform podczas szyfrowania zasobów z użyciem standardu AES, za pomocą usługi dostawy klucza usługi Media Services hello, a także korzystanie z szyfrowania dynamicznego.</span><span class="sxs-lookup"><span data-stu-id="686f0-130">hello following are general steps that you would need tooperform when encrypting your assets with AES, using hello Media Services key delivery service, and also using dynamic encryption.</span></span>

1. <span data-ttu-id="686f0-131">[Utworzenie elementu zawartości i przekazywanie plików do zawartości hello](media-services-protect-with-aes128.md#create_asset).</span><span class="sxs-lookup"><span data-stu-id="686f0-131">[Create an asset and upload files into hello asset](media-services-protect-with-aes128.md#create_asset).</span></span>
2. <span data-ttu-id="686f0-132">[Kodowanie zawartości hello zawierającego hello pliku toohello o adaptacyjnej szybkości bitowej MP4 zestawu](media-services-protect-with-aes128.md#encode_asset).</span><span class="sxs-lookup"><span data-stu-id="686f0-132">[Encode hello asset containing hello file toohello adaptive bitrate MP4 set](media-services-protect-with-aes128.md#encode_asset).</span></span>
3. <span data-ttu-id="686f0-133">[Utwórz klucz zawartości i powiązać ją z zasobów hello zakodowane](media-services-protect-with-aes128.md#create_contentkey).</span><span class="sxs-lookup"><span data-stu-id="686f0-133">[Create a content key and associate it with hello encoded asset](media-services-protect-with-aes128.md#create_contentkey).</span></span> <span data-ttu-id="686f0-134">W usłudze Media Services klucz zawartości hello zawiera klucz szyfrowania hello zasobów.</span><span class="sxs-lookup"><span data-stu-id="686f0-134">In Media Services, hello content key contains hello asset’s encryption key.</span></span>
4. <span data-ttu-id="686f0-135">[Skonfiguruj zasady autoryzacji klucza zawartości hello](media-services-protect-with-aes128.md#configure_key_auth_policy).</span><span class="sxs-lookup"><span data-stu-id="686f0-135">[Configure hello content key’s authorization policy](media-services-protect-with-aes128.md#configure_key_auth_policy).</span></span> <span data-ttu-id="686f0-136">zasady autoryzacji klucza zawartości Hello musi być skonfigurowane przez użytkownika i spełnione przez klienta hello w kolejności hello zawartości toobe klucza dostarczonego toohello klienta.</span><span class="sxs-lookup"><span data-stu-id="686f0-136">hello content key authorization policy must be configured by you and met by hello client in order for hello content key toobe delivered toohello client.</span></span>
5. <span data-ttu-id="686f0-137">[Skonfiguruj zasady dostarczania hello zasobu](media-services-protect-with-aes128.md#configure_asset_delivery_policy).</span><span class="sxs-lookup"><span data-stu-id="686f0-137">[Configure hello delivery policy for an asset](media-services-protect-with-aes128.md#configure_asset_delivery_policy).</span></span> <span data-ttu-id="686f0-138">Konfiguracja zasady dostarczania Hello obejmuje: kluczy adres URL pozyskiwania i wektor inicjowania (IV) (AES 128 wymaga hello tego samego toobe IV podane podczas szyfrowania i odszyfrowywania), protokół dostarczania (na przykład MPEG DASH, HLS, Smooth Streaming lub wszystkie), hello typu szyfrowania dynamicznego (na przykład, koperty lub nie szyfrowania dynamicznego).</span><span class="sxs-lookup"><span data-stu-id="686f0-138">hello delivery policy configuration includes: key acquisition URL and Initialization Vector (IV) (AES 128 requires hello same IV toobe supplied when encrypting and decrypting), delivery protocol (for example, MPEG DASH, HLS, Smooth Streaming or all), hello type of dynamic encryption (for example, envelope or no dynamic encryption).</span></span>

    <span data-ttu-id="686f0-139">Protokół tooeach różnych zasad można zastosować na powitania elementu zawartości.</span><span class="sxs-lookup"><span data-stu-id="686f0-139">You could apply different policy tooeach protocol on hello same asset.</span></span> <span data-ttu-id="686f0-140">Na przykład można zastosować szyfrowanie PlayReady tooSmooth/DASH i tooHLS szyfrowanie AES Envelope.</span><span class="sxs-lookup"><span data-stu-id="686f0-140">For example, you could apply PlayReady encryption tooSmooth/DASH and AES Envelope tooHLS.</span></span> <span data-ttu-id="686f0-141">Wszystkie protokoły, które nie są zdefiniowane w zasadzie dostarczania (na przykład dodać jedną zasadę, która tylko określa hello protokół HLS), zostanie zablokowany przesyłania strumieniowego.</span><span class="sxs-lookup"><span data-stu-id="686f0-141">Any protocols that are not defined in a delivery policy (for example, you add a single policy that only specifies HLS as hello protocol) will be blocked from streaming.</span></span> <span data-ttu-id="686f0-142">toothis wyjątek Hello jest, jeśli masz nie zdefiniowano zasad dostarczania elementów zawartości.</span><span class="sxs-lookup"><span data-stu-id="686f0-142">hello exception toothis is if you have no asset delivery policy defined at all.</span></span> <span data-ttu-id="686f0-143">Następnie wszystkie protokoły mogą być przesyłane hello Wyczyść.</span><span class="sxs-lookup"><span data-stu-id="686f0-143">Then, all protocols will be allowed in hello clear.</span></span>

6. <span data-ttu-id="686f0-144">[Utwórz Lokalizator OnDemand](media-services-protect-with-aes128.md#create_locator) w celu tooget adresu URL przesyłania strumieniowego.</span><span class="sxs-lookup"><span data-stu-id="686f0-144">[Create an OnDemand locator](media-services-protect-with-aes128.md#create_locator) in order tooget a streaming URL.</span></span>

<span data-ttu-id="686f0-145">przedstawiono również temat Hello [jak aplikacji klienckiej mogą żądać klucza z usługi dostarczania klucza hello](media-services-protect-with-aes128.md#client_request).</span><span class="sxs-lookup"><span data-stu-id="686f0-145">hello topic also shows [how a client application can request a key from hello key delivery service](media-services-protect-with-aes128.md#client_request).</span></span>

<span data-ttu-id="686f0-146">Dostępne są kompletne .NET [przykład](media-services-protect-with-aes128.md#example) na końcu hello hello tematu.</span><span class="sxs-lookup"><span data-stu-id="686f0-146">You will find a complete .NET [example](media-services-protect-with-aes128.md#example) at hello end of hello topic.</span></span>

<span data-ttu-id="686f0-147">powitania po obraz pokazuje opisany wyżej przepływ pracy hello.</span><span class="sxs-lookup"><span data-stu-id="686f0-147">hello following image demonstrates hello workflow described above.</span></span> <span data-ttu-id="686f0-148">W tym miejscu hello token jest używany do uwierzytelniania.</span><span class="sxs-lookup"><span data-stu-id="686f0-148">Here hello token is used for authentication.</span></span>

![Ochrona z zastosowaniem standardu AES-128](./media/media-services-content-protection-overview/media-services-content-protection-with-aes.png)

<span data-ttu-id="686f0-150">Witaj pozostałej części tego tematu zawiera szczegółowe wyjaśnienia, przykłady kodu i tootopics łącza, które pokazują, jak tooachieve hello zadania opisane powyżej.</span><span class="sxs-lookup"><span data-stu-id="686f0-150">hello rest of this topic provides detailed explanations, code examples, and links tootopics that show you how tooachieve hello tasks described above.</span></span>

## <a name="current-limitations"></a><span data-ttu-id="686f0-151">Bieżące ograniczenia</span><span class="sxs-lookup"><span data-stu-id="686f0-151">Current limitations</span></span>
<span data-ttu-id="686f0-152">W przypadku dodania lub zaktualizowania zasad dostarczania elementów zawartości należy usunąć skojarzony lokalizator (jeśli istnieje) i utworzyć nowy.</span><span class="sxs-lookup"><span data-stu-id="686f0-152">If you add or update your asset’s delivery policy, you must delete an existing locator (if any) and create a new locator.</span></span>

## <span data-ttu-id="686f0-153"><a id="create_asset"></a>Utworzenie elementu zawartości i przekazywanie plików do zawartości hello</span><span class="sxs-lookup"><span data-stu-id="686f0-153"><a id="create_asset"></a>Create an asset and upload files into hello asset</span></span>
<span data-ttu-id="686f0-154">W kolejności toomanage, kodowania i przesyłania strumieniowego filmów, należy najpierw przekazać zawartość do usługi Microsoft Azure Media Services.</span><span class="sxs-lookup"><span data-stu-id="686f0-154">In order toomanage, encode, and stream your videos, you must first upload your content into Microsoft Azure Media Services.</span></span> <span data-ttu-id="686f0-155">Po przekazaniu plików zawartość jest bezpiecznie przechowywana w chmurze powitania dla dalszego przetwarzania i przesyłania strumieniowego.</span><span class="sxs-lookup"><span data-stu-id="686f0-155">Once uploaded, your content is stored securely in hello cloud for further processing and streaming.</span></span> 

<span data-ttu-id="686f0-156">Aby uzyskać szczegółowe informacje, zobacz artykuł [Upload Files into a Media Services account](media-services-dotnet-upload-files.md) (Przekazywanie plików na konto usługi Media Services).</span><span class="sxs-lookup"><span data-stu-id="686f0-156">For detailed information, see [Upload Files into a Media Services account](media-services-dotnet-upload-files.md).</span></span>

## <span data-ttu-id="686f0-157"><a id="encode_asset"></a>Kodowanie hello zasobu zawierającego hello pliku toohello adaptacyjną szybkością transmisji bitów zestaw MP4</span><span class="sxs-lookup"><span data-stu-id="686f0-157"><a id="encode_asset"></a>Encode hello asset containing hello file toohello adaptive bitrate MP4 set</span></span>
<span data-ttu-id="686f0-158">W przypadku szyfrowania dynamicznego wystarczy jest toocreate element zawartości zawierający zestaw plików MP4 wielokrotnej szybkości transmisji bitów lub pliki źródłowe Smooth Streaming wielokrotnej szybkości transmisji bitów.</span><span class="sxs-lookup"><span data-stu-id="686f0-158">With dynamic encryption all you need is toocreate an asset that contains a set of multi-bitrate MP4 files or multi-bitrate Smooth Streaming source files.</span></span> <span data-ttu-id="686f0-159">Następnie na podstawie hello formatu określonego w manifeście hello lub fragmentu żądania, hello Streaming na żądanie serwera zapewni odbierania strumienia hello w protokole hello, wybrana.</span><span class="sxs-lookup"><span data-stu-id="686f0-159">Then, based on hello specified format in hello manifest or fragment request, hello On-Demand Streaming server will ensure that you receive hello stream in hello protocol you have chosen.</span></span> <span data-ttu-id="686f0-160">W związku z tym konieczne toostore i płatności hello pliki w jednym formacie magazynu, a usługa Media Services skompiluje oraz udostępni właściwą odpowiedź hello na podstawie żądań klienta.</span><span class="sxs-lookup"><span data-stu-id="686f0-160">As a result, you only need toostore and pay for hello files in single storage format and Media Services service will build and serve hello appropriate response based on requests from a client.</span></span> <span data-ttu-id="686f0-161">Aby uzyskać więcej informacji, zobacz hello [omówienie tworzenia pakietów dynamicznych](media-services-dynamic-packaging-overview.md) tematu.</span><span class="sxs-lookup"><span data-stu-id="686f0-161">For more information, see hello [Dynamic Packaging Overview](media-services-dynamic-packaging-overview.md) topic.</span></span>

>[!NOTE]
><span data-ttu-id="686f0-162">Po utworzeniu konta usługi AMS **domyślne** punktu końcowego przesyłania strumieniowego w brzmieniu konta tooyour hello **zatrzymane** stanu.</span><span class="sxs-lookup"><span data-stu-id="686f0-162">When your AMS account is created a **default** streaming endpoint is added tooyour account in hello **Stopped** state.</span></span> <span data-ttu-id="686f0-163">przesyłanie strumieniowe zawartości i podejmij korzyści z dynamicznego tworzenia pakietów i dynamicznego szyfrowania toostart hello punktu końcowego przesyłania strumieniowego, z którego mają zostać toostream zawartość ma toobe w hello **systemem** stanu.</span><span class="sxs-lookup"><span data-stu-id="686f0-163">toostart streaming your content and take advantage of dynamic packaging and dynamic encryption, hello streaming endpoint from which you want toostream content has toobe in hello **Running** state.</span></span> 
>
><span data-ttu-id="686f0-164">Ponadto toobe toouse stanie dynamicznego tworzenia pakietów i dynamicznego szyfrowania zawartości musi zawierać zestaw o adaptacyjnej szybkości bitowej MP4s lub pliki Smooth Streaming adaptacyjną szybkością transmisji bitów.</span><span class="sxs-lookup"><span data-stu-id="686f0-164">Also, toobe able toouse dynamic packaging and dynamic encryption your asset must contain a set of adaptive bitrate MP4s or adaptive bitrate Smooth Streaming files.</span></span>

<span data-ttu-id="686f0-165">Aby uzyskać instrukcje dotyczące tooencode, zobacz [jak tooencode zasobów przy użyciu standardu Media Encoder Standard](media-services-dotnet-encode-with-media-encoder-standard.md).</span><span class="sxs-lookup"><span data-stu-id="686f0-165">For instructions on how tooencode, see [How tooencode an asset using Media Encoder Standard](media-services-dotnet-encode-with-media-encoder-standard.md).</span></span>

## <span data-ttu-id="686f0-166"><a id="create_contentkey"></a>Utwórz klucz zawartości i powiązać ją z hello zakodowane zasobów</span><span class="sxs-lookup"><span data-stu-id="686f0-166"><a id="create_contentkey"></a>Create a content key and associate it with hello encoded asset</span></span>
<span data-ttu-id="686f0-167">W usłudze Media Services klucz zawartości hello zawiera klucz hello, które mają tooencrypt zasób z.</span><span class="sxs-lookup"><span data-stu-id="686f0-167">In Media Services, hello content key contains hello key that you want tooencrypt an asset with.</span></span>

<span data-ttu-id="686f0-168">Aby uzyskać szczegółowe informacje, zobacz artykuł [Create content key](media-services-dotnet-create-contentkey.md) (Tworzenie klucza zawartości).</span><span class="sxs-lookup"><span data-stu-id="686f0-168">For detailed information, see [Create content key](media-services-dotnet-create-contentkey.md).</span></span>

## <span data-ttu-id="686f0-169"><a id="configure_key_auth_policy"></a>Skonfiguruj zasady autoryzacji klucza zawartości hello</span><span class="sxs-lookup"><span data-stu-id="686f0-169"><a id="configure_key_auth_policy"></a>Configure hello content key’s authorization policy</span></span>
<span data-ttu-id="686f0-170">Usługa Media Services obsługuje wiele sposobów uwierzytelniania użytkowników, którzy tworzą żądania klucza.</span><span class="sxs-lookup"><span data-stu-id="686f0-170">Media Services supports multiple ways of authenticating users who make key requests.</span></span> <span data-ttu-id="686f0-171">zasady autoryzacji klucza zawartości Hello musi być skonfigurowane przez użytkownika i spełniać powitania klienta (odtwarzacz), aby hello toobe klucza dostarczyć toohello klienta.</span><span class="sxs-lookup"><span data-stu-id="686f0-171">hello content key authorization policy must be configured by you and met by hello client (player) in order for hello key toobe delivered toohello client.</span></span> <span data-ttu-id="686f0-172">Witaj zasady autoryzacji klucza zawartości może mieć jeden lub więcej ograniczeń: Otwórz, token ograniczenia lub ograniczenia adresów IP.</span><span class="sxs-lookup"><span data-stu-id="686f0-172">hello content key authorization policy could have one or more authorization restrictions: open, token restriction, or IP restriction.</span></span>

<span data-ttu-id="686f0-173">Aby uzyskać więcej informacji, zobacz artykuł [Configure Content Key Authorization Policy](media-services-dotnet-configure-content-key-auth-policy.md) (Konfigurowanie zasad autoryzacji klucza zawartości).</span><span class="sxs-lookup"><span data-stu-id="686f0-173">For detailed information, see [Configure Content Key Authorization Policy](media-services-dotnet-configure-content-key-auth-policy.md).</span></span>

## <span data-ttu-id="686f0-174"><a id="configure_asset_delivery_policy"></a>Konfigurowanie zasad dostarczania elementów zawartości</span><span class="sxs-lookup"><span data-stu-id="686f0-174"><a id="configure_asset_delivery_policy"></a>Configure asset delivery policy</span></span>
<span data-ttu-id="686f0-175">Skonfiguruj zasady dostarczania powitania dla zawartości.</span><span class="sxs-lookup"><span data-stu-id="686f0-175">Configure hello delivery policy for your asset.</span></span> <span data-ttu-id="686f0-176">Obejmuje kilka rzeczy, które hello Konfiguracja zasady dostarczania zasobów:</span><span class="sxs-lookup"><span data-stu-id="686f0-176">Some things that hello asset delivery policy configuration includes:</span></span>

* <span data-ttu-id="686f0-177">adres URL pozyskiwania klucza Hello.</span><span class="sxs-lookup"><span data-stu-id="686f0-177">hello Key acquisition URL.</span></span> 
* <span data-ttu-id="686f0-178">Witaj toouse wektor inicjowania (IV) hello koperty szyfrowania.</span><span class="sxs-lookup"><span data-stu-id="686f0-178">hello Initialization Vector (IV) toouse for hello envelope encryption.</span></span> <span data-ttu-id="686f0-179">AES 128 wymaga hello tego samego toobe IV podane podczas szyfrowania i odszyfrowywania.</span><span class="sxs-lookup"><span data-stu-id="686f0-179">AES 128 requires hello same IV toobe supplied when encrypting and decrypting.</span></span> 
* <span data-ttu-id="686f0-180">Witaj Protokół dostarczania elementów zawartości (na przykład MPEG DASH, HLS, Smooth Streaming lub wszystkie).</span><span class="sxs-lookup"><span data-stu-id="686f0-180">hello asset delivery protocol (for example, MPEG DASH, HLS, Smooth Streaming or all).</span></span>
* <span data-ttu-id="686f0-181">Witaj typ szyfrowania dynamicznego (na przykład szyfrowanie AES envelope) lub nie szyfrowania dynamicznego.</span><span class="sxs-lookup"><span data-stu-id="686f0-181">hello type of dynamic encryption (for example, AES envelope) or no dynamic encryption.</span></span> 

<span data-ttu-id="686f0-182">Aby uzyskać szczegółowe informacje, zobacz artykuł [Configure asset delivery policy](media-services-rest-configure-asset-delivery-policy.md) (Konfigurowanie zasad dostarczania elementów zawartości).</span><span class="sxs-lookup"><span data-stu-id="686f0-182">For detailed information, see [Configure asset delivery policy ](media-services-rest-configure-asset-delivery-policy.md).</span></span>

## <span data-ttu-id="686f0-183"><a id="create_locator"></a>Utwórz Lokalizator OnDemand przesyłania strumieniowego w kolejności tooget adresu URL przesyłania strumieniowego</span><span class="sxs-lookup"><span data-stu-id="686f0-183"><a id="create_locator"></a>Create an OnDemand streaming locator in order tooget a streaming URL</span></span>
<span data-ttu-id="686f0-184">Konieczne będzie tooprovide użytkownika z hello przesyłania strumieniowego adres URL dla Smooth, DASH lub HLS.</span><span class="sxs-lookup"><span data-stu-id="686f0-184">You will need tooprovide your user with hello streaming URL for Smooth, DASH or HLS.</span></span>

> [!NOTE]
> <span data-ttu-id="686f0-185">W przypadku dodania lub zaktualizowania zasad dostarczania elementów zawartości należy usunąć skojarzony lokalizator (jeśli istnieje) i utworzyć nowy.</span><span class="sxs-lookup"><span data-stu-id="686f0-185">If you add or update your asset’s delivery policy, you must delete an existing locator (if any) and create a new locator.</span></span>
> 
> 

<span data-ttu-id="686f0-186">Aby uzyskać instrukcje dotyczące sposobu toopublish zasobów i kompilacji adresu URL przesyłania strumieniowego, zobacz [zbudować adresu URL przesyłania strumieniowego](media-services-deliver-streaming-content.md).</span><span class="sxs-lookup"><span data-stu-id="686f0-186">For instructions on how toopublish an asset and build a streaming URL, see [Build a streaming URL](media-services-deliver-streaming-content.md).</span></span>

## <a name="get-a-test-token"></a><span data-ttu-id="686f0-187">Pobieranie tokenu testowego</span><span class="sxs-lookup"><span data-stu-id="686f0-187">Get a test token</span></span>
<span data-ttu-id="686f0-188">Pobierz token testowy, oparte na powitania ograniczenia tokenu użytego do hello zasady autoryzacji klucza.</span><span class="sxs-lookup"><span data-stu-id="686f0-188">Get a test token based on hello token restriction that was used for hello key authorization policy.</span></span>

    // Deserializes a string containing an Xml representation of a TokenRestrictionTemplate
    // back into a TokenRestrictionTemplate class instance.
    TokenRestrictionTemplate tokenTemplate = 
        TokenRestrictionTemplateSerializer.Deserialize(tokenTemplateString);

    // Generate a test token based on hello data in hello given TokenRestrictionTemplate.
    //hello GenerateTestToken method returns hello token without hello word “Bearer” in front
    //so you have tooadd it in front of hello token string. 
    string testToken = TokenRestrictionTemplateSerializer.GenerateTestToken(tokenTemplate);
    Console.WriteLine("hello authorization token is:\nBearer {0}", testToken);

<span data-ttu-id="686f0-189">Można użyć hello [AMS Player](http://amsplayer.azurewebsites.net/azuremediaplayer.html) tootest strumienia.</span><span class="sxs-lookup"><span data-stu-id="686f0-189">You can use hello [AMS Player](http://amsplayer.azurewebsites.net/azuremediaplayer.html) tootest your stream.</span></span>

## <span data-ttu-id="686f0-190"><a id="client_request"></a>Jak klient Zażądaj klucza z usługi dostarczania klucza hello</span><span class="sxs-lookup"><span data-stu-id="686f0-190"><a id="client_request"></a>How can your client request a key from hello key delivery service?</span></span>
<span data-ttu-id="686f0-191">W poprzednim kroku hello należy konstruować hello adres URL, który wskazuje plik manifestu tooa.</span><span class="sxs-lookup"><span data-stu-id="686f0-191">In hello previous step, you constructed hello URL that points tooa manifest file.</span></span> <span data-ttu-id="686f0-192">Klient musi tooextract hello niezbędne informacje z hello przesyłanie strumieniowe plików manifestu w kolejności toomake usługi klucza dostawy toohello żądania.</span><span class="sxs-lookup"><span data-stu-id="686f0-192">Your client needs tooextract hello necessary information from hello streaming manifest files in order toomake a request toohello key delivery service.</span></span>

### <a name="manifest-files"></a><span data-ttu-id="686f0-193">Pliki manifestu</span><span class="sxs-lookup"><span data-stu-id="686f0-193">Manifest files</span></span>
<span data-ttu-id="686f0-194">powitania klienta wymaga adresu URL hello tooextract (zawierającej również identyfikator (Kącik) klucz zawartości) wartość z zakresu od hello pliku manifestu.</span><span class="sxs-lookup"><span data-stu-id="686f0-194">hello client needs tooextract hello URL (that also contains content key Id (kid)) value from hello manifest file.</span></span> <span data-ttu-id="686f0-195">powitania klienta spróbuj klucza szyfrowania hello tooget z usługi dostarczania klucza hello.</span><span class="sxs-lookup"><span data-stu-id="686f0-195">hello client will then try tooget hello encryption key from hello key delivery service.</span></span> <span data-ttu-id="686f0-196">Witaj klienta musi też mieć wartość hello IV tooextract i użyj odszyfrować stream.hello powitania po fragment kodu przedstawia hello <Protection> element hello Smooth Streaming manifestu.</span><span class="sxs-lookup"><span data-stu-id="686f0-196">hello client also needs tooextract hello IV value and use it do decrypt hello stream.hello following snippet shows hello <Protection> element of hello Smooth Streaming manifest.</span></span>

    <Protection>
      <ProtectionHeader SystemID="B47B251A-2409-4B42-958E-08DBAE7B4EE9">
        <ContentProtection xmlns:sea="urn:mpeg:dash:schema:sea:2012" schemeIdUri="urn:mpeg:dash:sea:2012">
          <sea:SegmentEncryption schemeIdUri="urn:mpeg:dash:sea:aes128-cbc:2013"/>
          <sea:KeySystem keySystemUri="urn:mpeg:dash:sea:keysys:http:2013"/>
          <sea:CryptoPeriod IV="0xD7D7D7D7D7D7D7D7D7D7D7D7D7D7D7D7" 
                            keyUriTemplate="https://wamsbayclus001kd-hs.cloudapp.net/HlsHandler.ashx?
                                            kid=da3813af-55e6-48e7-aa9f-a4d6031f7b4d"/>
        </ContentProtection>
      </ProtectionHeader>
    </Protection>

<span data-ttu-id="686f0-197">W przypadku hello HLS hello głównego manifestu jest dzielony na pliki segmentu.</span><span class="sxs-lookup"><span data-stu-id="686f0-197">In hello case of HLS, hello root manifest is broken into segment files.</span></span> 

<span data-ttu-id="686f0-198">Na przykład jest hello głównego manifestu: http://test001.origin.mediaservices.windows.net/8bfe7d6f-34e3-4d1a-b289-3e48a8762490/BigBuckBunny.ism/manifest(format=m3u8-aapl) zawierający listę nazw plików segmentu.</span><span class="sxs-lookup"><span data-stu-id="686f0-198">For example, hello root manifest is: http://test001.origin.mediaservices.windows.net/8bfe7d6f-34e3-4d1a-b289-3e48a8762490/BigBuckBunny.ism/manifest(format=m3u8-aapl) and it contains a list of segment file names.</span></span>

    . . . 
    #EXT-X-STREAM-INF:PROGRAM-ID=1,BANDWIDTH=630133,RESOLUTION=424x240,CODECS="avc1.4d4015,mp4a.40.2",AUDIO="audio"
    QualityLevels(514369)/Manifest(video,format=m3u8-aapl)
    #EXT-X-STREAM-INF:PROGRAM-ID=1,BANDWIDTH=965441,RESOLUTION=636x356,CODECS="avc1.4d401e,mp4a.40.2",AUDIO="audio"
    QualityLevels(842459)/Manifest(video,format=m3u8-aapl)
    …

<span data-ttu-id="686f0-199">Jeśli jeden z plików segmentu hello Otwórz w edytorze tekstu (na przykład http://test001.origin.mediaservices.windows.net/8bfe7d6f-34e3-4d1a-b289-3e48a8762490/BigBuckBunny.ism/QualityLevels(514369)/Manifest(video,format=m3u8-aapl), it should zawiera #EXT-X-klucza, który wskazuje, że ten plik hello jest zaszyfrowany.</span><span class="sxs-lookup"><span data-stu-id="686f0-199">If you open one of hello segment files in text editor (for example, http://test001.origin.mediaservices.windows.net/8bfe7d6f-34e3-4d1a-b289-3e48a8762490/BigBuckBunny.ism/QualityLevels(514369)/Manifest(video,format=m3u8-aapl), it should contain #EXT-X-KEY which indicates that hello file is encrypted.</span></span>

    #EXTM3U
    #EXT-X-VERSION:4
    #EXT-X-ALLOW-CACHE:NO
    #EXT-X-MEDIA-SEQUENCE:0
    #EXT-X-TARGETDURATION:9
    #EXT-X-KEY:METHOD=AES-128,
    URI="https://wamsbayclus001kd-hs.cloudapp.net/HlsHandler.ashx?
         kid=da3813af-55e6-48e7-aa9f-a4d6031f7b4d",
            IV=0XD7D7D7D7D7D7D7D7D7D7D7D7D7D7D7D7
    #EXT-X-PROGRAM-DATE-TIME:1970-01-01T00:00:00.000+00:00
    #EXTINF:8.425708,no-desc
    Fragments(video=0,format=m3u8-aapl)
    #EXT-X-ENDLIST

>[!NOTE] 
><span data-ttu-id="686f0-200">Jeśli planujesz tooplay AES szyfrowane HLS w programie Safari, zobacz [ten blog](https://azure.microsoft.com/blog/how-to-make-token-authorized-aes-encrypted-hls-stream-working-in-safari/).</span><span class="sxs-lookup"><span data-stu-id="686f0-200">If you are planning tooplay an AES encrypted HLS in Safari, see [this blog](https://azure.microsoft.com/blog/how-to-make-token-authorized-aes-encrypted-hls-stream-working-in-safari/).</span></span>

### <a name="request-hello-key-from-hello-key-delivery-service"></a><span data-ttu-id="686f0-201">Żądaj hello klucza z usługi dostarczania klucza hello</span><span class="sxs-lookup"><span data-stu-id="686f0-201">Request hello key from hello key delivery service</span></span>

<span data-ttu-id="686f0-202">Witaj poniższy kod przedstawia sposób toosend toohello żądania usługi Media Services klucz usługi dostarczania przy użyciu klucza dostawy identyfikatora Uri (który został wyodrębniony z manifestu hello) i tokenu (w tym temacie nie opisano sposobu tooget prostego tokeny zabezpieczenia usługi tokenu).</span><span class="sxs-lookup"><span data-stu-id="686f0-202">hello following code shows how toosend a request toohello Media Services key delivery service using a key delivery Uri (that was extracted from hello manifest) and a token (this topic does not talk about how tooget Simple Web Tokens from a Secure Token Service).</span></span>

    private byte[] GetDeliveryKey(Uri keyDeliveryUri, string token)
    {
        HttpWebRequest request = (HttpWebRequest)WebRequest.Create(keyDeliveryUri);

        request.Method = "POST";
        request.ContentType = "text/xml";
        if (!string.IsNullOrEmpty(token))
        {
            request.Headers[AuthorizationHeader] = token;
        }
        request.ContentLength = 0;

        var response = request.GetResponse();

        var stream = response.GetResponseStream();
        if (stream == null)
        {
            throw new NullReferenceException("Response stream is null");
        }

        var buffer = new byte[256];
        var length = 0;
        while (stream.CanRead && length <= buffer.Length)
        {
            var nexByte = stream.ReadByte();
            if (nexByte == -1)
            {
                break;
            }
            buffer[length] = (byte)nexByte;
            length++;
        }
        response.Close();

        // AES keys must be exactly 16 bytes (128 bits).
        var key = new byte[length];
        Array.Copy(buffer, key, length);
        return key;
    }

## <a name="protect-your-content-with-aes-128-using-net"></a><span data-ttu-id="686f0-203">Ochrona zawartości przy użyciu standardu AES-128 przy użyciu platformy .NET</span><span class="sxs-lookup"><span data-stu-id="686f0-203">Protect your content with AES-128 using .NET</span></span>

### <a name="create-and-configure-a-visual-studio-project"></a><span data-ttu-id="686f0-204">Tworzenie i konfigurowanie projektu programu Visual Studio</span><span class="sxs-lookup"><span data-stu-id="686f0-204">Create and configure a Visual Studio project</span></span>

1. <span data-ttu-id="686f0-205">Konfigurowanie środowiska projektowego i wypełnić plik app.config hello o informacje dotyczące połączenia, zgodnie z opisem w [tworzenia usługi Media Services z platformą .NET](media-services-dotnet-how-to-use.md).</span><span class="sxs-lookup"><span data-stu-id="686f0-205">Set up your development environment and populate hello app.config file with connection information, as described in [Media Services development with .NET](media-services-dotnet-how-to-use.md).</span></span> 
2. <span data-ttu-id="686f0-206">Dodaj następujące elementy zbyt hello**appSettings** zdefiniowane w pliku app.config:</span><span class="sxs-lookup"><span data-stu-id="686f0-206">Add hello following elements too**appSettings** defined in your app.config file:</span></span>

        <add key="Issuer" value="http://testacs.com"/>
        <add key="Audience" value="urn:test"/>

### <span data-ttu-id="686f0-207"><a id="example"></a>Przykład</span><span class="sxs-lookup"><span data-stu-id="686f0-207"><a id="example"></a>Example</span></span>

<span data-ttu-id="686f0-208">Zastąp hello kodu w pliku Program.cs kodem hello przedstawionym w tej sekcji.</span><span class="sxs-lookup"><span data-stu-id="686f0-208">Overwrite hello code in your Program.cs file with hello code shown in this section.</span></span>
 
>[!NOTE]
><span data-ttu-id="686f0-209">Limit różnych zasad usługi AMS wynosi 1 000 000 (na przykład zasad lokalizatorów lub ContentKeyAuthorizationPolicy).</span><span class="sxs-lookup"><span data-stu-id="686f0-209">There is a limit of 1,000,000 policies for different AMS policies (for example, for Locator policy or ContentKeyAuthorizationPolicy).</span></span> <span data-ttu-id="686f0-210">Należy używać hello tym samym identyfikatorze zasad, jeśli używasz zawsze hello sam dni / dostęp uprawnień, na przykład zasady dla lokalizatorów, które są przeznaczone tooremain w miejscu przez długi czas (zasady — przekazywanie).</span><span class="sxs-lookup"><span data-stu-id="686f0-210">You should use hello same policy ID if you are always using hello same days / access permissions, for example, policies for locators that are intended tooremain in place for a long time (non-upload policies).</span></span> <span data-ttu-id="686f0-211">Aby uzyskać więcej informacji, zobacz [ten](media-services-dotnet-manage-entities.md#limit-access-policies) temat.</span><span class="sxs-lookup"><span data-stu-id="686f0-211">For more information, see [this](media-services-dotnet-manage-entities.md#limit-access-policies) topic.</span></span>

<span data-ttu-id="686f0-212">Upewnij się, że zmienne tooupdate toopoint toofolders gdzie znajdują się pliki danych wejściowych.</span><span class="sxs-lookup"><span data-stu-id="686f0-212">Make sure tooupdate variables toopoint toofolders where your input files are located.</span></span>

    using System;
    using System.Collections.Generic;
    using System.Configuration;
    using System.IO;
    using System.Linq;
    using System.Security.Cryptography;
    using Microsoft.WindowsAzure.MediaServices.Client;
    using System.Threading;
    using Microsoft.WindowsAzure.MediaServices.Client.ContentKeyAuthorization;
    using Microsoft.WindowsAzure.MediaServices.Client.DynamicEncryption;

    namespace AESDynamicEncryptionAndKeyDeliverySvc
    {
        class Program
        {
        // Read values from hello App.config file.
        private static readonly string _AADTenantDomain =
        ConfigurationManager.AppSettings["AADTenantDomain"];
        private static readonly string _RESTAPIEndpoint =
        ConfigurationManager.AppSettings["MediaServiceRESTAPIEndpoint"];

        // A Uri describing hello issuer of hello token.  
        // Must match hello value in hello token for hello token toobe considered valid.
        private static readonly Uri _sampleIssuer =
            new Uri(ConfigurationManager.AppSettings["Issuer"]);
        // hello Audience or Scope of hello token.  
        // Must match hello value in hello token for hello token toobe considered valid.
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

            IContentKey key = CreateEnvelopeTypeContentKey(encodedAsset);
            Console.WriteLine("Created key {0} for hello asset {1} ", key.Id, encodedAsset.Id);
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

            // Generate a test token based on hello data in hello given TokenRestrictionTemplate.
            // Note, you need toopass hello key id Guid because we specified 
            // TokenClaim.ContentKeyIdentifierClaim in during hello creation of TokenRestrictionTemplate.
            Guid rawkey = EncryptionUtils.GetKeyIdAsGuid(key.Id);

            //hello GenerateTestToken method returns hello token without hello word “Bearer” in front
            //so you have tooadd it in front of hello token string. 
            string testToken = TokenRestrictionTemplateSerializer.GenerateTestToken(tokenTemplate, null, rawkey);
            Console.WriteLine("hello authorization token is:\nBearer {0}", testToken);
            Console.WriteLine();
            }

            // You can use hello bit.ly/aesplayer Flash player tootest hello URL 
            // (with open authorization policy). 
            // Paste hello URL and click hello Update button tooplay hello video. 
            //
            string URL = GetStreamingOriginLocator(encodedAsset);
            Console.WriteLine("Smooth Streaming Url: {0}/manifest", URL);
            Console.WriteLine();
            Console.WriteLine("HLS Url: {0}/manifest(format=m3u8-aapl)", URL);
            Console.WriteLine();

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
            IAsset inputAsset = _context.Assets.Create(assetName, AssetCreationOptions.StorageEncrypted);

            var assetFile = inputAsset.AssetFiles.Create(Path.GetFileName(singleFilePath));

            Console.WriteLine("Created assetFile {0}", assetFile.Name);


            Console.WriteLine("Upload {0}", assetFile.Name);

            assetFile.Upload(singleFilePath);
            Console.WriteLine("Done uploading {0}", assetFile.Name);

            return inputAsset;
        }

        static public IAsset EncodeToAdaptiveBitrateMP4Set(IAsset asset)
        {
            // Declare a new job.
            IJob job = _context.Jobs.Create("Media Encoder Standard Job");
            // Get a media processor reference, and pass tooit hello name of hello 
            // processor toouse for hello specific task.
            IMediaProcessor processor = GetLatestMediaProcessorByName("Media Encoder Standard");

            // Create a task with hello encoding details, using a string preset.
            // In this case "Adaptive Streaming" preset is used.
            ITask task = job.Tasks.AddNew("My encoding task",
            processor,
            "Adaptive Streaming",
            TaskOptions.None);

            // Specify hello input asset toobe encoded.
            task.InputAssets.Add(asset);
            // Add an output asset toocontain hello results of hello job. 
            // This output is specified as AssetCreationOptions.None, which 
            // means hello output asset is not encrypted. 
            task.OutputAssets.AddNew("Output asset",
            AssetCreationOptions.StorageEncrypted);

            job.StateChanged += new EventHandler<JobStateChangedEventArgs>(JobStateChanged);
            job.Submit();
            job.GetExecutionProgressTask(CancellationToken.None).Wait();

            return job.OutputMediaAssets[0];
        }

        private static IMediaProcessor GetLatestMediaProcessorByName(string mediaProcessorName)
        {
            var processor = _context.MediaProcessors.Where(p => p.Name == mediaProcessorName).
            ToList().OrderBy(p => new Version(p.Version)).LastOrDefault();

            if (processor == null)
            throw new ArgumentException(string.Format("Unknown media processor", mediaProcessorName));

            return processor;
        }

        static public IContentKey CreateEnvelopeTypeContentKey(IAsset asset)
        {
            // Create envelope encryption content key
            Guid keyId = Guid.NewGuid();
            byte[] contentKey = GetRandomBuffer(16);

            IContentKey key = _context.ContentKeys.Create(
                keyId,
                contentKey,
                "ContentKey",
                ContentKeyType.EnvelopeEncryption);

            // Associate hello key with hello asset.
            asset.ContentKeys.Add(key);

            return key;
        }

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

        static public void CreateAssetDeliveryPolicy(IAsset asset, IContentKey key)
        {
            Uri keyAcquisitionUri = key.GetKeyDeliveryUrl(ContentKeyDeliveryType.BaselineHttp);

            string envelopeEncryptionIV = Convert.ToBase64String(GetRandomBuffer(16));

            // When configuring delivery policy, you can choose tooassociate it
            // with a key acquisition URL that has a KID appended or
            // or a key acquisition URL that does not have a KID appended  
            // in which case a content key can be reused. 

            // EnvelopeKeyAcquisitionUrl:  contains a key ID in hello key URL.
            // EnvelopeBaseKeyAcquisitionUrl:  hello URL does not contains a key ID

            // hello following policy configuration specifies: 
            // key url that will have KID=<Guid> appended toohello envelope and
            // hello Initialization Vector (IV) toouse for hello envelope encryption.

            Dictionary<AssetDeliveryPolicyConfigurationKey, string> assetDeliveryPolicyConfiguration =
            new Dictionary<AssetDeliveryPolicyConfigurationKey, string>
            {
            {AssetDeliveryPolicyConfigurationKey.EnvelopeKeyAcquisitionUrl, keyAcquisitionUri.ToString()}
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
            Console.WriteLine("Adding Asset Delivery Policy: " +
            assetDeliveryPolicy.AssetDeliveryPolicyType);
        }

        static public string GetStreamingOriginLocator(IAsset asset)
        {

            // Get a reference toohello streaming manifest file from hello  
            // collection of files in hello asset. 

            var assetFile = asset.AssetFiles.Where(f => f.Name.ToLower().
                EndsWith(".ism")).
                FirstOrDefault();

            // Create a 30-day readonly access policy. 
            // You cannot create a streaming locator using an AccessPolicy that includes write or delete permissions.            
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

        static private void JobStateChanged(object sender, JobStateChangedEventArgs e)
        {
            Console.WriteLine(string.Format("{0}\n  State: {1}\n  Time: {2}\n\n",
            ((IJob)sender).Name,
            e.CurrentState,
            DateTime.UtcNow.ToString(@"yyyy_M_d__hh_mm_ss")));
        }

        static private byte[] GetRandomBuffer(int size)
        {
            byte[] randomBytes = new byte[size];
            using (RNGCryptoServiceProvider rng = new RNGCryptoServiceProvider())
            {
            rng.GetBytes(randomBytes);
            }

            return randomBytes;
        }
        }
    }


## <a name="media-services-learning-paths"></a><span data-ttu-id="686f0-213">Ścieżki szkoleniowe dotyczące usługi Media Services</span><span class="sxs-lookup"><span data-stu-id="686f0-213">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="686f0-214">Przekazywanie opinii</span><span class="sxs-lookup"><span data-stu-id="686f0-214">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

