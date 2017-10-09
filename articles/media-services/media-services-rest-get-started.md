---
title: "wprowadzenie do dostarczania zawartości na żądanie przy użyciu REST aaaGet | Dokumentacja firmy Microsoft"
description: "Ten samouczek przedstawia kroki hello wdrażania aplikacji dostarczania zawartości na żądanie przy użyciu interfejsu API REST usługi Azure Media Services."
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: 88194b59-e479-43ac-b179-af4f295e3780
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/10/2017
ms.author: juliako
ms.openlocfilehash: f270ed59e9ae9745e8403ec6e19d5c3533fc82b7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-delivering-content-on-demand-using-rest"></a><span data-ttu-id="efd3b-103">Wprowadzenie do dostarczania zawartości na żądanie za pomocą usługi REST</span><span class="sxs-lookup"><span data-stu-id="efd3b-103">Get started with delivering content on demand using REST</span></span>
[!INCLUDE [media-services-selector-get-started](../../includes/media-services-selector-get-started.md)]

<span data-ttu-id="efd3b-104">Ta opcja szybkiego startu przeprowadzi Cię przez kroki wdrażania aplikacji do dostarczania zawartości wideo na żądanie (VoD) przy użyciu interfejsów API REST usługi Azure Media Services (AMS) hello.</span><span class="sxs-lookup"><span data-stu-id="efd3b-104">This quickstart walks you through hello steps of implementing a Video-on-Demand (VoD) content delivery application using Azure Media Services (AMS) REST APIs.</span></span>

<span data-ttu-id="efd3b-105">Samouczek Hello wprowadza hello podstawowy przepływ pracy usług Media Services i hello najczęściej obiekty i zadania programowania wymagane do tworzenia usługi Media Services.</span><span class="sxs-lookup"><span data-stu-id="efd3b-105">hello tutorial introduces hello basic Media Services workflow and hello most common programming objects and tasks required for Media Services development.</span></span> <span data-ttu-id="efd3b-106">Po ukończeniu hello samouczka hello będzie toostream może być lub pobrać progresywnie przykładowy plik nośnika, który przekazany, zakodowany i pobierane.</span><span class="sxs-lookup"><span data-stu-id="efd3b-106">At hello completion of hello tutorial, you will be able toostream or progressively download a sample media file that you uploaded, encoded, and downloaded.</span></span>

<span data-ttu-id="efd3b-107">Witaj poniższej ilustracji przedstawiono niektóre obiekty hello najczęściej używane podczas tworzenia aplikacji VoD hello Media Services OData modelu.</span><span class="sxs-lookup"><span data-stu-id="efd3b-107">hello following image shows some of hello most commonly used objects when developing VoD applications against hello Media Services OData model.</span></span>

<span data-ttu-id="efd3b-108">Kliknij przycisk tooview obraz powitania pełny jego rozmiar.</span><span class="sxs-lookup"><span data-stu-id="efd3b-108">Click hello image tooview it full size.</span></span>  

<a href="./media/media-services-rest-get-started/media-services-overview-object-model.png" target="_blank"><img src="./media/media-services-rest-get-started/media-services-overview-object-model-small.png"></a> 

## <a name="prerequisites"></a><span data-ttu-id="efd3b-109">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="efd3b-109">Prerequisites</span></span>
<span data-ttu-id="efd3b-110">Witaj następujące wymagania wstępne są wymagane toostart programowania z użyciem usługi Media Services z interfejsów API REST.</span><span class="sxs-lookup"><span data-stu-id="efd3b-110">hello following prerequisites are required toostart developing with Media Services with REST APIs.</span></span>

* <span data-ttu-id="efd3b-111">Konto platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="efd3b-111">An Azure account.</span></span> <span data-ttu-id="efd3b-112">Aby uzyskać szczegółowe informacje, zobacz artykuł [Bezpłatna wersja próbna platformy Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="efd3b-112">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="efd3b-113">Konto usługi Media Services.</span><span class="sxs-lookup"><span data-stu-id="efd3b-113">A Media Services account.</span></span> <span data-ttu-id="efd3b-114">Zobacz toocreate konto usługi Media Services [jak tooCreate konta usługi Media Services](media-services-portal-create-account.md).</span><span class="sxs-lookup"><span data-stu-id="efd3b-114">toocreate a Media Services account, see [How tooCreate a Media Services Account](media-services-portal-create-account.md).</span></span>
* <span data-ttu-id="efd3b-115">Opis sposobu toodevelop z interfejsu API REST usługi multimediów.</span><span class="sxs-lookup"><span data-stu-id="efd3b-115">Understanding of how toodevelop with Media Services REST API.</span></span> <span data-ttu-id="efd3b-116">Aby uzyskać więcej informacji, zobacz [omówienie interfejsu API REST usług Media](media-services-rest-how-to-use.md).</span><span class="sxs-lookup"><span data-stu-id="efd3b-116">For more information, see [Media Services REST API overview](media-services-rest-how-to-use.md).</span></span>
* <span data-ttu-id="efd3b-117">Aplikacja, który może wysyłać żądań i odpowiedzi HTTP.</span><span class="sxs-lookup"><span data-stu-id="efd3b-117">An application of your choice that can send HTTP requests and responses.</span></span> <span data-ttu-id="efd3b-118">W tym samouczku używana [Fiddler](http://www.telerik.com/download/fiddler).</span><span class="sxs-lookup"><span data-stu-id="efd3b-118">This tutorial uses [Fiddler](http://www.telerik.com/download/fiddler).</span></span>

<span data-ttu-id="efd3b-119">Witaj następujące zadania są wyświetlane w tego przewodnika Szybki Start.</span><span class="sxs-lookup"><span data-stu-id="efd3b-119">hello following tasks are shown in this quickstart.</span></span>

1. <span data-ttu-id="efd3b-120">Początek (przy użyciu portalu Azure hello) punktu końcowego przesyłania strumieniowego.</span><span class="sxs-lookup"><span data-stu-id="efd3b-120">Start streaming endpoint (using hello Azure portal).</span></span>
2. <span data-ttu-id="efd3b-121">Konto usługi Media Services toohello Uzyskuj dostęp do interfejsu API REST.</span><span class="sxs-lookup"><span data-stu-id="efd3b-121">Connect toohello Media Services account with REST API.</span></span>
3. <span data-ttu-id="efd3b-122">Tworzenie nowego elementu zawartości i przekazywanie pliku wideo z interfejsu API REST.</span><span class="sxs-lookup"><span data-stu-id="efd3b-122">Create a new asset and upload a video file with REST API.</span></span>
4. <span data-ttu-id="efd3b-123">Koduj plik źródłowy hello do zestawu plików MP4 o adaptacyjnej szybkości bitowej z interfejsu API REST.</span><span class="sxs-lookup"><span data-stu-id="efd3b-123">Encode hello source file into a set of adaptive bitrate MP4 files with REST API.</span></span>
5. <span data-ttu-id="efd3b-124">Publikowanie zawartości hello i get przesyłania strumieniowego i pobierania progresywnego adresy URL z interfejsu API REST.</span><span class="sxs-lookup"><span data-stu-id="efd3b-124">Publish hello asset and get streaming and progressive download URLs with REST API.</span></span>
6. <span data-ttu-id="efd3b-125">Odtwarzanie zawartości.</span><span class="sxs-lookup"><span data-stu-id="efd3b-125">Play your content.</span></span>

>[!NOTE]
><span data-ttu-id="efd3b-126">Limit różnych zasad usługi AMS wynosi 1 000 000 (na przykład zasad lokalizatorów lub ContentKeyAuthorizationPolicy).</span><span class="sxs-lookup"><span data-stu-id="efd3b-126">There is a limit of 1,000,000 policies for different AMS policies (for example, for Locator policy or ContentKeyAuthorizationPolicy).</span></span> <span data-ttu-id="efd3b-127">Należy używać hello tym samym identyfikatorze zasad, jeśli używasz zawsze hello sam dni / dostęp uprawnień, na przykład zasady dla lokalizatorów, które są przeznaczone tooremain w miejscu przez długi czas (zasady — przekazywanie).</span><span class="sxs-lookup"><span data-stu-id="efd3b-127">You should use hello same policy ID if you are always using hello same days / access permissions, for example, policies for locators that are intended tooremain in place for a long time (non-upload policies).</span></span> <span data-ttu-id="efd3b-128">Aby uzyskać więcej informacji, zobacz [ten](media-services-dotnet-manage-entities.md#limit-access-policies) temat.</span><span class="sxs-lookup"><span data-stu-id="efd3b-128">For more information, see [this](media-services-dotnet-manage-entities.md#limit-access-policies) topic.</span></span>

<span data-ttu-id="efd3b-129">Aby uzyskać szczegółowe informacje na temat jednostek AMS REST używaną w tym temacie, zobacz [dokumentacja interfejsu API REST usługi Azure Media Services](/rest/api/media/services/azure-media-services-rest-api-reference).</span><span class="sxs-lookup"><span data-stu-id="efd3b-129">For details about AMS REST entities used in this topic, see [Azure Media Services REST API Reference](/rest/api/media/services/azure-media-services-rest-api-reference).</span></span> <span data-ttu-id="efd3b-130">Zobacz też [pojęcia dotyczące usługi Azure Media Services](media-services-concepts.md).</span><span class="sxs-lookup"><span data-stu-id="efd3b-130">Also, see [Azure Media Services concepts](media-services-concepts.md).</span></span>

>[!NOTE]
><span data-ttu-id="efd3b-131">Podczas uzyskiwania dostępu do obiektów w usłudze Media Services, należy ustawić określonych pól nagłówka i wartości w Twoich żądań HTTP.</span><span class="sxs-lookup"><span data-stu-id="efd3b-131">When accessing entities in Media Services, you must set specific header fields and values in your HTTP requests.</span></span> <span data-ttu-id="efd3b-132">Aby uzyskać więcej informacji, zobacz [ustawień dla rozwoju interfejsu API REST usługi Media](media-services-rest-how-to-use.md).</span><span class="sxs-lookup"><span data-stu-id="efd3b-132">For more information, see [Setup for Media Services REST API Development](media-services-rest-how-to-use.md).</span></span>

## <a name="start-streaming-endpoints-using-hello-azure-portal"></a><span data-ttu-id="efd3b-133">Uruchom przy użyciu portalu Azure hello punkty końcowe przesyłania strumieniowego</span><span class="sxs-lookup"><span data-stu-id="efd3b-133">Start streaming endpoints using hello Azure portal</span></span>

<span data-ttu-id="efd3b-134">Podczas pracy w usłudze Azure Media Services jednym z hello najbardziej typowych scenariuszy jest dostarczanie plików wideo przy użyciu przesyłania strumieniowego adaptacyjną szybkością transmisji bitów.</span><span class="sxs-lookup"><span data-stu-id="efd3b-134">When working with Azure Media Services one of hello most common scenarios is delivering video via adaptive bitrate streaming.</span></span> <span data-ttu-id="efd3b-135">Usługa Media Services udostępnia funkcję dynamicznego tworzenia pakietów, co pozwala toodeliver adaptacyjnej szybkości bitowej MP4 zakodowane zawartości w formatach transmisji strumieniowej obsługiwanych przez usługi Media Services (MPEG DASH, HLS, Smooth Streaming) just-in-time, bez konieczności toostore wstępnie umieszczone wersje każdego z tych formatach.</span><span class="sxs-lookup"><span data-stu-id="efd3b-135">Media Services provides dynamic packaging, which allows you toodeliver your adaptive bitrate MP4 encoded content in streaming formats supported by Media Services (MPEG DASH, HLS, Smooth Streaming) just-in-time, without you having toostore pre-packaged versions of each of these streaming formats.</span></span>

>[!NOTE]
><span data-ttu-id="efd3b-136">Po utworzeniu konta usługi AMS **domyślne** punktu końcowego przesyłania strumieniowego w brzmieniu konta tooyour hello **zatrzymane** stanu.</span><span class="sxs-lookup"><span data-stu-id="efd3b-136">When your AMS account is created a **default** streaming endpoint is added tooyour account in hello **Stopped** state.</span></span> <span data-ttu-id="efd3b-137">przesyłanie strumieniowe zawartości i podejmij korzyści z dynamicznego tworzenia pakietów i dynamicznego szyfrowania toostart hello punktu końcowego przesyłania strumieniowego, z którego mają zostać toostream zawartość ma toobe w hello **systemem** stanu.</span><span class="sxs-lookup"><span data-stu-id="efd3b-137">toostart streaming your content and take advantage of dynamic packaging and dynamic encryption, hello streaming endpoint from which you want toostream content has toobe in hello **Running** state.</span></span>

<span data-ttu-id="efd3b-138">toostart hello punktu końcowego przesyłania strumieniowego, hello następujące:</span><span class="sxs-lookup"><span data-stu-id="efd3b-138">toostart hello streaming endpoint, do hello following:</span></span>

1. <span data-ttu-id="efd3b-139">Zaloguj się w hello [portalu Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="efd3b-139">Log in at hello [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="efd3b-140">W oknie Ustawienia powitania kliknij punkty końcowe przesyłania strumieniowego.</span><span class="sxs-lookup"><span data-stu-id="efd3b-140">In hello Settings window, click Streaming endpoints.</span></span>
3. <span data-ttu-id="efd3b-141">Kliknij przycisk domyślny hello punktu końcowego przesyłania strumieniowego.</span><span class="sxs-lookup"><span data-stu-id="efd3b-141">Click hello default streaming endpoint.</span></span>

    <span data-ttu-id="efd3b-142">zostanie wyświetlone okno Szczegóły punktu KOŃCOWEGO przesyłania STRUMIENIOWEGO domyślne Hello.</span><span class="sxs-lookup"><span data-stu-id="efd3b-142">hello DEFAULT STREAMING ENDPOINT DETAILS window appears.</span></span>

4. <span data-ttu-id="efd3b-143">Kliknij ikonę Start hello.</span><span class="sxs-lookup"><span data-stu-id="efd3b-143">Click hello Start icon.</span></span>
5. <span data-ttu-id="efd3b-144">Kliknij przycisk toosave przycisk Zapisz hello zmiany.</span><span class="sxs-lookup"><span data-stu-id="efd3b-144">Click hello Save button toosave your changes.</span></span>

## <span data-ttu-id="efd3b-145"><a id="connect"></a>Konto usługi Media Services toohello Uzyskuj dostęp do interfejsu API REST</span><span class="sxs-lookup"><span data-stu-id="efd3b-145"><a id="connect"></a>Connect toohello Media Services account with REST API</span></span>

<span data-ttu-id="efd3b-146">Aby uzyskać informacje dotyczące tooconnect toohello AMS interfejsu API, zobacz temat [hello dostępu do interfejsu API usługi Azure Media Services przy użyciu uwierzytelniania usługi Azure AD](media-services-use-aad-auth-to-access-ams-api.md).</span><span class="sxs-lookup"><span data-stu-id="efd3b-146">For information on how tooconnect toohello AMS API, see [Access hello Azure Media Services API with Azure AD authentication](media-services-use-aad-auth-to-access-ams-api.md).</span></span> 

>[!NOTE]
><span data-ttu-id="efd3b-147">Po pomyślnym połączeniu toohttps://media.windows.net, otrzymasz 301 przekierowanie, określając inny identyfikator URI usługi multimediów.</span><span class="sxs-lookup"><span data-stu-id="efd3b-147">After successfully connecting toohttps://media.windows.net, you will receive a 301 redirect specifying another Media Services URI.</span></span> <span data-ttu-id="efd3b-148">Należy wykonać kolejne wywołania toohello nowy identyfikator URI.</span><span class="sxs-lookup"><span data-stu-id="efd3b-148">You must make subsequent calls toohello new URI.</span></span>

<span data-ttu-id="efd3b-149">Na przykład jeśli po wypróbowaniu tooconnect, masz następujące hello:</span><span class="sxs-lookup"><span data-stu-id="efd3b-149">For example, if after trying tooconnect, you got hello following:</span></span>

    HTTP/1.1 301 Moved Permanently
    Location: https://wamsbayclus001rest-hs.cloudapp.net/api/

<span data-ttu-id="efd3b-150">Należy zadać programu późniejsze toohttps://wamsbayclus001rest-hs.cloudapp.net/api/ wywołania interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="efd3b-150">You should post your subsequent API calls toohttps://wamsbayclus001rest-hs.cloudapp.net/api/.</span></span>

## <span data-ttu-id="efd3b-151"><a id="upload"></a>Tworzenie nowego elementu zawartości i przekazywanie pliku wideo z interfejsu API REST</span><span class="sxs-lookup"><span data-stu-id="efd3b-151"><a id="upload"></a>Create a new asset and upload a video file with REST API</span></span>

<span data-ttu-id="efd3b-152">Za pomocą usługi Media Services można przekazać pliki cyfrowe do elementu zawartości.</span><span class="sxs-lookup"><span data-stu-id="efd3b-152">In Media Services, you upload your digital files into an asset.</span></span> <span data-ttu-id="efd3b-153">Witaj **zasobów** może zawierać wideo, audio, obrazy, kolekcje miniatur, tekst ścieżek i napisów plików (i hello metadane dotyczące tych plików.)  Po hello pliki są przekazywane do hello zawartości, zawartość jest bezpiecznie przechowywana w chmurze powitania dla dalszego przetwarzania i przesyłania strumieniowego.</span><span class="sxs-lookup"><span data-stu-id="efd3b-153">hello **Asset** entity can contain video, audio, images, thumbnail collections, text tracks and closed caption files (and hello metadata about these files.)  Once hello files are uploaded into hello asset, your content is stored securely in hello cloud for further processing and streaming.</span></span>

<span data-ttu-id="efd3b-154">Jedna z wartości hello ma tooprovide, podczas tworzenia zasobu jest opcji tworzenia elementów zawartości.</span><span class="sxs-lookup"><span data-stu-id="efd3b-154">One of hello values that you have tooprovide when creating an asset is asset creation options.</span></span> <span data-ttu-id="efd3b-155">Witaj **opcje** właściwość jest wartością wyliczenia, który opisuje opcje szyfrowania hello, które można utworzyć zasobu z.</span><span class="sxs-lookup"><span data-stu-id="efd3b-155">hello **Options** property is an enumeration value that describes hello encryption options that an Asset can be created with.</span></span> <span data-ttu-id="efd3b-156">Nieprawidłowa wartość jest jedną z wartości hello z listy hello poniżej nie kombinację wartości z tej listy:</span><span class="sxs-lookup"><span data-stu-id="efd3b-156">A valid value is one of hello values from hello list below, not a combination of values from this list:</span></span>

* <span data-ttu-id="efd3b-157">**Brak** = **0** — szyfrowanie nie jest stosowane.</span><span class="sxs-lookup"><span data-stu-id="efd3b-157">**None** = **0** - No encryption is used.</span></span> <span data-ttu-id="efd3b-158">Korzystając z tej opcji zawartość nie jest chroniona w trakcie przesyłania lub przechowywania w magazynie.</span><span class="sxs-lookup"><span data-stu-id="efd3b-158">When using this option your content is not protected in transit or at rest in storage.</span></span>
    <span data-ttu-id="efd3b-159">Jeśli planujesz toodeliver MP4 przy użyciu pobierania progresywnego, użyj tej opcji.</span><span class="sxs-lookup"><span data-stu-id="efd3b-159">If you plan toodeliver an MP4 using progressive download, use this option.</span></span>
* <span data-ttu-id="efd3b-160">**StorageEncrypted** = **1** — szyfruje zawartości lokalnie, przy użyciu standardu AES 256-bitowego, a następnie przekazanie jej tooAzure magazynu, w którym są przechowywane szyfrowane, gdy.</span><span class="sxs-lookup"><span data-stu-id="efd3b-160">**StorageEncrypted** = **1** - Encrypts your clear content locally using AES-256 bit encryption and then uploads it tooAzure Storage where it is stored encrypted at rest.</span></span> <span data-ttu-id="efd3b-161">Elementy zawartości chronione przy użyciu szyfrowania magazynu są automatycznie bez szyfrowania i umieszczana w poprzednich tooencoding systemu szyfrowania plików i opcjonalnie ponownie szyfrowane przed toouploading zwrotnym w formie nowego elementu zawartości wyjściowej.</span><span class="sxs-lookup"><span data-stu-id="efd3b-161">Assets protected with Storage Encryption are automatically unencrypted and placed in an encrypted file system prior tooencoding, and optionally re-encrypted prior toouploading back as a new output asset.</span></span> <span data-ttu-id="efd3b-162">Witaj pierwotnym zastosowaniem szyfrowania magazynu jest toosecure Twojego wysokiej jakości multimedialnych plików wejściowych z silne szyfrowanie przechowywanych na dysku.</span><span class="sxs-lookup"><span data-stu-id="efd3b-162">hello primary use case for Storage Encryption is when you want toosecure your high-quality input media files with strong encryption at rest on disk.</span></span>
* <span data-ttu-id="efd3b-163">**CommonEncryptionProtected** = **2** — ta opcja umożliwia przekazanie zawartości, który został już szyfrowane i chronione za pomocą wspólnego szyfrowania lub technologii PlayReady DRM (na przykład, Smooth Streaming chronione przy użyciu technologii PlayReady DRM).</span><span class="sxs-lookup"><span data-stu-id="efd3b-163">**CommonEncryptionProtected** = **2** - Use this option if you are uploading content that has already been encrypted and protected with Common Encryption or PlayReady DRM (for example, Smooth Streaming protected with PlayReady DRM).</span></span>
* <span data-ttu-id="efd3b-164">**EnvelopeEncryptionProtected** = **4** — Użyj tej opcji, Jeśli przesyłasz HLS zaszyfrowanych z użyciem standardu AES.</span><span class="sxs-lookup"><span data-stu-id="efd3b-164">**EnvelopeEncryptionProtected** = **4** – Use this option if you are uploading HLS encrypted with AES.</span></span> <span data-ttu-id="efd3b-165">pliki Hello musi zostały zakodowane i zaszyfrowane przez Transform Manager.</span><span class="sxs-lookup"><span data-stu-id="efd3b-165">hello files must have been encoded and encrypted by Transform Manager.</span></span>

### <a name="create-an-asset"></a><span data-ttu-id="efd3b-166">Utwórz zasób</span><span class="sxs-lookup"><span data-stu-id="efd3b-166">Create an asset</span></span>
<span data-ttu-id="efd3b-167">Zasób jest kontenerem dla wielu typów lub zestawów obiektów w usłudze Media Services: wideo, audio, obrazy, kolekcje miniatur, ścieżek tekstu i pliki napisów.</span><span class="sxs-lookup"><span data-stu-id="efd3b-167">An asset is a container for multiple types or sets of objects in Media Services, including video, audio, images, thumbnail collections, text tracks, and closed caption files.</span></span> <span data-ttu-id="efd3b-168">W hello interfejsu API REST, tworzenie zasobu wymaga wysyłania POST wysyłanie żądań usług tooMedia i umieszczenie wszelkie informacje o zawartości w treści żądania hello.</span><span class="sxs-lookup"><span data-stu-id="efd3b-168">In hello REST API, creating an Asset requires sending POST request tooMedia Services and placing any property information about your asset in hello request body.</span></span>

<span data-ttu-id="efd3b-169">powitania po przykładzie pokazano, jak toocreate zasób.</span><span class="sxs-lookup"><span data-stu-id="efd3b-169">hello following example shows how toocreate an asset.</span></span>

<span data-ttu-id="efd3b-170">**Żądania HTTP**</span><span class="sxs-lookup"><span data-stu-id="efd3b-170">**HTTP Request**</span></span>

    POST https://wamsbayclus001rest-hs.cloudapp.net/api/Assets HTTP/1.1
    Content-Type: application/json
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amstestaccount001&urn%3aSubscriptionId=z7f09258-2233-4ca2-b1ae-193798e2c9d8&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1421640053&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=vlG%2fPYdFDMS1zKc36qcFVWnaNh07UCkhYj3B71%2fk1YA%3d
    x-ms-version: 2.11
    x-ms-client-request-id: c59de965-bc89-4295-9a57-75d897e5221e
    Host: wamsbayclus001rest-hs.cloudapp.net
    Content-Length: 45

    {"Name":"BigBuckBunny.mp4", "Options":"0"}


<span data-ttu-id="efd3b-171">**Odpowiedź HTTP**</span><span class="sxs-lookup"><span data-stu-id="efd3b-171">**HTTP Response**</span></span>

<span data-ttu-id="efd3b-172">W przypadku powodzenia zwrócono hello następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="efd3b-172">If successful, hello following is returned:</span></span>

    HTTP/1.1 201 Created
    Cache-Control: no-cache
    Content-Length: 452
    Content-Type: application/json;odata=minimalmetadata;streaming=true;charset=utf-8
    Location: https://wamsbayclus001rest-hs.cloudapp.net/api/Assets('nb%3Acid%3AUUID%3A9bc8ff20-24fb-4fdb-9d7c-b04c7ee573a1')
    Server: Microsoft-IIS/8.5
    x-ms-client-request-id: c59de965-bc89-4295-9a57-75d897e5221e
    request-id: e98be122-ae09-473a-8072-0ccd234a0657
    x-ms-request-id: e98be122-ae09-473a-8072-0ccd234a0657
    X-Content-Type-Options: nosniff
    DataServiceVersion: 3.0;
    X-Powered-By: ASP.NET
    Strict-Transport-Security: max-age=31536000; includeSubDomains
    Date: Sun, 18 Jan 2015 22:06:40 GMT

    {  
       "odata.metadata":"https://wamsbayclus001rest-hs.cloudapp.net/api/$metadata#Assets/@Element",
       "Id":"nb:cid:UUID:9bc8ff20-24fb-4fdb-9d7c-b04c7ee573a1",
       "State":0,
       "Created":"2015-01-18T22:06:40.6010903Z",
       "LastModified":"2015-01-18T22:06:40.6010903Z",
       "AlternateId":null,
       "Name":"BigBuckBunny2.mp4",
       "Options":0,
       "Uri":"https://storagetestaccount001.blob.core.windows.net/asset-9bc8ff20-24fb-4fdb-9d7c-b04c7ee573a1",
       "StorageAccountName":"storagetestaccount001"
    }

### <a name="create-an-assetfile"></a><span data-ttu-id="efd3b-173">Utwórz AssetFile</span><span class="sxs-lookup"><span data-stu-id="efd3b-173">Create an AssetFile</span></span>
<span data-ttu-id="efd3b-174">Witaj [AssetFile](https://docs.microsoft.com/rest/api/media/operations/assetfile) jednostki reprezentuje plik wideo lub audio, który jest przechowywany w kontenerze obiektów blob.</span><span class="sxs-lookup"><span data-stu-id="efd3b-174">hello [AssetFile](https://docs.microsoft.com/rest/api/media/operations/assetfile) entity represents a video or audio file that is stored in a blob container.</span></span> <span data-ttu-id="efd3b-175">Plik zasobów zawsze jest skojarzony z zasobem i zasobów może zawierać jeden lub wiele AssetFiles.</span><span class="sxs-lookup"><span data-stu-id="efd3b-175">An asset file is always associated with an asset, and an asset may contain one or many AssetFiles.</span></span> <span data-ttu-id="efd3b-176">Witaj Media Encoder usług zadanie nie powiedzie się, jeśli obiekt pliku zasobu nie jest skojarzony z pliku cyfrowego w kontenerze obiektów blob.</span><span class="sxs-lookup"><span data-stu-id="efd3b-176">hello Media Services Encoder task fails if an asset file object is not associated with a digital file in a blob container.</span></span>

<span data-ttu-id="efd3b-177">Po przekazaniu pliku nośnika cyfrowego do kontenera obiektów blob, użyj hello **scalania** żądania HTTP tooupdate hello AssetFile informacje o pliku nośnika (jak pokazano w dalszej części tematu hello).</span><span class="sxs-lookup"><span data-stu-id="efd3b-177">After you upload your digital media file into a blob container, you use hello **MERGE** HTTP request tooupdate hello AssetFile with information about your media file (as shown later in hello topic).</span></span>

<span data-ttu-id="efd3b-178">**Żądania HTTP**</span><span class="sxs-lookup"><span data-stu-id="efd3b-178">**HTTP Request**</span></span>

    POST https://wamsbayclus001rest-hs.cloudapp.net/api/Files HTTP/1.1
    Content-Type: application/json
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amstestaccount001&urn%3aSubscriptionId=z7f09258-2233-4ca2-b1ae-193798e2c9d8&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1421640053&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=vlG%2fPYdFDMS1zKc36qcFVWnaNh07UCkhYj3B71%2fk1YA%3d
    x-ms-version: 2.11
    Host: wamsbayclus001rest-hs.cloudapp.net
    Content-Length: 164

    {  
       "IsEncrypted":"false",
       "IsPrimary":"false",
       "MimeType":"video/mp4",
       "Name":"BigBuckBunny.mp4",
       "ParentAssetId":"nb:cid:UUID:9bc8ff20-24fb-4fdb-9d7c-b04c7ee573a1"
    }


<span data-ttu-id="efd3b-179">**Odpowiedź HTTP**</span><span class="sxs-lookup"><span data-stu-id="efd3b-179">**HTTP Response**</span></span>

    HTTP/1.1 201 Created
    Cache-Control: no-cache
    Content-Length: 535
    Content-Type: application/json;odata=minimalmetadata;streaming=true;charset=utf-8
    Location: https://wamsbayclus001rest-hs.cloudapp.net/api/Files('nb%3Acid%3AUUID%3Af13a0137-0a62-9d4c-b3b9-ca944b5142c5')
    Server: Microsoft-IIS/8.5
    request-id: 98a30e2d-f379-4495-988e-0b79edc9b80e
    x-ms-request-id: 98a30e2d-f379-4495-988e-0b79edc9b80e
    X-Content-Type-Options: nosniff
    DataServiceVersion: 3.0;
    X-Powered-By: ASP.NET
    Strict-Transport-Security: max-age=31536000; includeSubDomains
    Date: Mon, 19 Jan 2015 00:34:07 GMT

    {  
       "odata.metadata":"https://wamsbayclus001rest-hs.cloudapp.net/api/$metadata#Files/@Element",
       "Id":"nb:cid:UUID:f13a0137-0a62-9d4c-b3b9-ca944b5142c5",
       "Name":"BigBuckBunny.mp4",
       "ContentFileSize":"0",
       "ParentAssetId":"nb:cid:UUID:9bc8ff20-24fb-4fdb-9d7c-b04c7ee573a1",
       "EncryptionVersion":null,
       "EncryptionScheme":null,
       "IsEncrypted":false,
       "EncryptionKeyId":null,
       "InitializationVector":null,
       "IsPrimary":false,
       "LastModified":"2015-01-19T00:34:08.1934137Z",
       "Created":"2015-01-19T00:34:08.1934137Z",
       "MimeType":"video/mp4",
       "ContentChecksum":null
    }


### <a name="creating-hello-accesspolicy-with-write-permission"></a><span data-ttu-id="efd3b-180">Tworzenie hello AccessPolicy z uprawnieniami do zapisu</span><span class="sxs-lookup"><span data-stu-id="efd3b-180">Creating hello AccessPolicy with write permission</span></span>
<span data-ttu-id="efd3b-181">Przed przekazaniem żadnych plików do magazynu obiektów blob, należy ustawić dostępu hello zasad praw do pisania tooan zasobów.</span><span class="sxs-lookup"><span data-stu-id="efd3b-181">Before uploading any files into blob storage, set hello access policy rights for writing tooan asset.</span></span> <span data-ttu-id="efd3b-182">Ustaw toodo, który po toohello żądania HTTP AccessPolicies jednostki.</span><span class="sxs-lookup"><span data-stu-id="efd3b-182">toodo that, POST an HTTP request toohello AccessPolicies entity set.</span></span> <span data-ttu-id="efd3b-183">Zdefiniuj wartość DurationInMinutes po utworzeniu lub pojawi się komunikat o błędzie 500 wewnętrzny serwer w odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="efd3b-183">Define a DurationInMinutes value upon creation or you receive a 500 Internal Server error message back in response.</span></span> <span data-ttu-id="efd3b-184">Aby uzyskać więcej informacji o AccessPolicies, zobacz [AccessPolicy](https://docs.microsoft.com/rest/api/media/operations/accesspolicy).</span><span class="sxs-lookup"><span data-stu-id="efd3b-184">For more information on AccessPolicies, see [AccessPolicy](https://docs.microsoft.com/rest/api/media/operations/accesspolicy).</span></span>

<span data-ttu-id="efd3b-185">powitania po przykładzie pokazano, jak toocreate AccessPolicy:</span><span class="sxs-lookup"><span data-stu-id="efd3b-185">hello following example shows how toocreate an AccessPolicy:</span></span>

<span data-ttu-id="efd3b-186">**Żądania HTTP**</span><span class="sxs-lookup"><span data-stu-id="efd3b-186">**HTTP Request**</span></span>

    POST https://wamsbayclus001rest-hs.cloudapp.net/api/AccessPolicies HTTP/1.1
    Content-Type: application/json
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amstestaccount001&urn%3aSubscriptionId=z7f09258-2233-4ca2-b1ae-193798e2c9d8&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1421640053&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=vlG%2fPYdFDMS1zKc36qcFVWnaNh07UCkhYj3B71%2fk1YA%3d
    x-ms-version: 2.11
    Host: wamsbayclus001rest-hs.cloudapp.net
    Content-Length: 74

    {"Name":"NewUploadPolicy", "DurationInMinutes":"440", "Permissions":"2"}

<span data-ttu-id="efd3b-187">**Odpowiedź HTTP**</span><span class="sxs-lookup"><span data-stu-id="efd3b-187">**HTTP Response**</span></span>

<span data-ttu-id="efd3b-188">W przypadku powodzenia powitania po odpowiedzi jest zwracany:</span><span class="sxs-lookup"><span data-stu-id="efd3b-188">If successful, hello following response is returned:</span></span>

    HTTP/1.1 201 Created
    Cache-Control: no-cache
    Content-Length: 312
    Content-Type: application/json;odata=minimalmetadata;streaming=true;charset=utf-8
    Location: https://wamsbayclus001rest-hs.cloudapp.net/api/AccessPolicies('nb%3Apid%3AUUID%3Abe0ac48d-af7d-4877-9d60-1805d68bffae')
    Server: Microsoft-IIS/8.5
    request-id: 74c74545-7e0a-4cd6-a440-c1c48074a970
    x-ms-request-id: 74c74545-7e0a-4cd6-a440-c1c48074a970
    X-Content-Type-Options: nosniff
    DataServiceVersion: 3.0;
    X-Powered-By: ASP.NET
    Strict-Transport-Security: max-age=31536000; includeSubDomains
    Date: Sun, 18 Jan 2015 22:18:06 GMT

    {  
       "odata.metadata":"https://wamsbayclus001rest-hs.cloudapp.net/api/$metadata#AccessPolicies/@Element",
       "Id":"nb:pid:UUID:be0ac48d-af7d-4877-9d60-1805d68bffae",
       "Created":"2015-01-18T22:18:06.6370575Z",
       "LastModified":"2015-01-18T22:18:06.6370575Z",
       "Name":"NewUploadPolicy",
       "DurationInMinutes":440.0,
       "Permissions":2
    }

### <a name="get-hello-upload-url"></a><span data-ttu-id="efd3b-189">Pobierz hello przekazać adres URL</span><span class="sxs-lookup"><span data-stu-id="efd3b-189">Get hello Upload URL</span></span>

<span data-ttu-id="efd3b-190">tooreceive hello przekazywania rzeczywisty adres URL, tworzenie lokalizatora SAS.</span><span class="sxs-lookup"><span data-stu-id="efd3b-190">tooreceive hello actual upload URL, create a SAS Locator.</span></span> <span data-ttu-id="efd3b-191">Lokalizatory zdefiniuj hello czas rozpoczęcia i typ punktu końcowego połączenia dla klientów, którzy mają tooaccess plików zasobów.</span><span class="sxs-lookup"><span data-stu-id="efd3b-191">Locators define hello start time and type of connection endpoint for clients that want tooaccess Files in an Asset.</span></span> <span data-ttu-id="efd3b-192">Można utworzyć wiele jednostek lokalizatora dla danego AccessPolicy i zasobów pary toohandle innego klienta żądań i potrzeb.</span><span class="sxs-lookup"><span data-stu-id="efd3b-192">You can create multiple Locator entities for a given AccessPolicy and Asset pair toohandle different client requests and needs.</span></span> <span data-ttu-id="efd3b-193">Każda z tych lokalizatorów używa wartości StartTime hello plus wartość DurationInMinutes hello hello AccessPolicy toodetermine hello długość czasu, można użyć adresu URL.</span><span class="sxs-lookup"><span data-stu-id="efd3b-193">Each of these Locators uses hello StartTime value plus hello DurationInMinutes value of hello AccessPolicy toodetermine hello length of time a URL can be used.</span></span> <span data-ttu-id="efd3b-194">Aby uzyskać więcej informacji, zobacz [lokalizatora](https://docs.microsoft.com/rest/api/media/operations/locator).</span><span class="sxs-lookup"><span data-stu-id="efd3b-194">For more information, see [Locator](https://docs.microsoft.com/rest/api/media/operations/locator).</span></span>

<span data-ttu-id="efd3b-195">Adres URL SAS ma hello następującego formatu:</span><span class="sxs-lookup"><span data-stu-id="efd3b-195">A SAS URL has hello following format:</span></span>

    {https://myaccount.blob.core.windows.net}/{asset name}/{video file name}?{SAS signature}

<span data-ttu-id="efd3b-196">Zagadnienia do rozważenia:</span><span class="sxs-lookup"><span data-stu-id="efd3b-196">Some considerations apply:</span></span>

* <span data-ttu-id="efd3b-197">Nie może mieć więcej niż pięć lokalizatorów unikatowy skojarzone z danym zawartości w tym samym czasie.</span><span class="sxs-lookup"><span data-stu-id="efd3b-197">You cannot have more than five unique Locators associated with a given Asset at one time.</span></span> <span data-ttu-id="efd3b-198">Aby uzyskać więcej informacji zobacz lokalizatora.</span><span class="sxs-lookup"><span data-stu-id="efd3b-198">For more information, see Locator.</span></span>
* <span data-ttu-id="efd3b-199">Tooupload plików natychmiast, należy należy ustawić Twojej StartTime wartość toofive minut przed hello bieżącego czasu.</span><span class="sxs-lookup"><span data-stu-id="efd3b-199">If you need tooupload your files immediately, you should set your StartTime value toofive minutes before hello current time.</span></span> <span data-ttu-id="efd3b-200">Jest to spowodowane mogą istnieć zegara pochylenia między komputer klienta i usługi Media Services.</span><span class="sxs-lookup"><span data-stu-id="efd3b-200">This is because there may be clock skew between your client machine and Media Services.</span></span> <span data-ttu-id="efd3b-201">Ponadto wartość StartTime musi być w powitania po formacie daty/godziny: RRRR-MM-ddtgg (na przykład "2014-05-23T17:53:50Z").</span><span class="sxs-lookup"><span data-stu-id="efd3b-201">Also, your StartTime value must be in hello following DateTime format: YYYY-MM-DDTHH:mm:ssZ (for example, "2014-05-23T17:53:50Z").</span></span>    
* <span data-ttu-id="efd3b-202">Może być 30 40 sekund opóźnienia po utworzeniu lokalizatora toowhen nie jest dostępny do użycia.</span><span class="sxs-lookup"><span data-stu-id="efd3b-202">There may be a 30-40 second delay after a Locator is created toowhen it is available for use.</span></span> <span data-ttu-id="efd3b-203">Ten problem dotyczy tooboth adres URL SAS oraz Lokalizatory pochodzenia.</span><span class="sxs-lookup"><span data-stu-id="efd3b-203">This issue applies tooboth SAS URL and Origin Locators.</span></span>

<span data-ttu-id="efd3b-204">Aby uzyskać więcej informacji na temat sygnatury dostępu Współdzielonego Zobacz lokalizatorów [to](http://southworks.com/blog/2015/05/27/reusing-azure-media-services-locators-to-avoid-facing-the-5-shared-access-policy-limitation/) blogu.</span><span class="sxs-lookup"><span data-stu-id="efd3b-204">For more information about SAS locators see [this](http://southworks.com/blog/2015/05/27/reusing-azure-media-services-locators-to-avoid-facing-the-5-shared-access-policy-limitation/) blog.</span></span>

<span data-ttu-id="efd3b-205">Witaj poniższy przykład pokazuje, jak toocreate lokalizatora adres URL SAS, zgodnie z definicją hello właściwości typu w treści żądania hello ("1" dla lokalizatora SAS) i "2" dla lokalizatora pochodzenia na żądanie.</span><span class="sxs-lookup"><span data-stu-id="efd3b-205">hello following example shows how toocreate a SAS URL Locator, as defined by hello Type property in hello request body ("1" for a SAS locator and "2" for an On-Demand origin locator).</span></span> <span data-ttu-id="efd3b-206">Witaj **ścieżki** właściwości zwróconej zawiera adres URL hello, że należy używać tooupload Twojego pliku.</span><span class="sxs-lookup"><span data-stu-id="efd3b-206">hello **Path** property returned contains hello URL that you must use tooupload your file.</span></span>

<span data-ttu-id="efd3b-207">**Żądania HTTP**</span><span class="sxs-lookup"><span data-stu-id="efd3b-207">**HTTP Request**</span></span>

    POST https://wamsbayclus001rest-hs.cloudapp.net/api/Locators HTTP/1.1
    Content-Type: application/json
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amstestaccount001&urn%3aSubscriptionId=f7f09258-6753-4ca2-b1ae-193798e2c9d8&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1421640053&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=vlG%2fPYdFDMS1zKc36qcFVWnaNh07UCkhYj3B71%2fk1YA%3d
    x-ms-version: 2.11
    Host: wamsbayclus001rest-hs.cloudapp.net
    Content-Length: 178

    {  
       "AccessPolicyId":"nb:pid:UUID:be0ac48d-af7d-4877-9d60-1805d68bffae",
       "AssetId":"nb:cid:UUID:9bc8ff20-24fb-4fdb-9d7c-b04c7ee573a1",
       "StartTime":"2015-02-18T16:45:53",
       "Type":1
    }


<span data-ttu-id="efd3b-208">**Odpowiedź HTTP**</span><span class="sxs-lookup"><span data-stu-id="efd3b-208">**HTTP Response**</span></span>

<span data-ttu-id="efd3b-209">W przypadku powodzenia powitania po odpowiedzi jest zwracany:</span><span class="sxs-lookup"><span data-stu-id="efd3b-209">If successful, hello following response is returned:</span></span>

    HTTP/1.1 201 Created
    Cache-Control: no-cache
    Content-Length: 949
    Content-Type: application/json;odata=minimalmetadata;streaming=true;charset=utf-8
    Location: https://wamsbayclus001rest-hs.cloudapp.net/api/Locators('nb%3Alid%3AUUID%3Aaf57bdd8-6751-4e84-b403-f3c140444b54')
    Server: Microsoft-IIS/8.5
    request-id: 2adeb1f8-89c5-4cc8-aa4f-08cdfef33ae0
    x-ms-request-id: 2adeb1f8-89c5-4cc8-aa4f-08cdfef33ae0
    X-Content-Type-Options: nosniff
    DataServiceVersion: 3.0;
    X-Powered-By: ASP.NET
    Strict-Transport-Security: max-age=31536000; includeSubDomains
    Date: Mon, 19 Jan 2015 03:01:29 GMT

    {  
       "odata.metadata":"https://wamsbayclus001rest-hs.cloudapp.net/api/$metadata#Locators/@Element",
       "Id":"nb:lid:UUID:af57bdd8-6751-4e84-b403-f3c140444b54",
       "ExpirationDateTime":"2015-02-19T00:05:53",
       "Type":1,
       "Path":"https://storagetestaccount001.blob.core.windows.net/asset-f438649c-313c-46e2-8d68-7d2550288247?sv=2012-02-12&sr=c&si=af57bdd8-6751-4e84-b403-f3c140444b54&sig=fE4btwEfZtVQFeC0Wh3Kwks2OFPQfzl5qTMW5YytiuY%3D&st=2015-02-18T16%3A45%3A53Z&se=2015-02-19T00%3A05%3A53Z",
       "BaseUri":"https://storagetestaccount001.blob.core.windows.net/asset-f438649c-313c-46e2-8d68-7d2550288247",
       "ContentAccessComponent":"?sv=2012-02-12&sr=c&si=af57bdd8-6751-4e84-b403-f3c140444b54&sig=fE4btwEfZtVQFeC0Wh3Kwks2OFPQfzl5qTMW5YytiuY%3D&st=2015-02-18T16%3A45%3A53Z&se=2015-02-19T00%3A05%3A53Z",
       "AccessPolicyId":"nb:pid:UUID:be0ac48d-af7d-4877-9d60-1805d68bffae",
       "AssetId":"nb:cid:UUID:9bc8ff20-24fb-4fdb-9d7c-b04c7ee573a1",
       "StartTime":"2015-02-18T16:45:53",
       "Name":null
    }

### <a name="upload-a-file-into-a-blob-storage-container"></a><span data-ttu-id="efd3b-210">Przekazywanie pliku do kontenera magazynu obiektów blob</span><span class="sxs-lookup"><span data-stu-id="efd3b-210">Upload a file into a blob storage container</span></span>
<span data-ttu-id="efd3b-211">Po utworzeniu hello AccessPolicy i lokalizatora zestawu rzeczywisty plik hello jest kontenera magazynu obiektów blob platformy Azure tooan przekazane za pomocą hello interfejsów API REST magazynu Azure.</span><span class="sxs-lookup"><span data-stu-id="efd3b-211">Once you have hello AccessPolicy and Locator set, hello actual file is uploaded tooan Azure blob storage container using hello Azure Storage REST APIs.</span></span> <span data-ttu-id="efd3b-212">Należy przekazać pliki hello jako blokowych obiektów blob.</span><span class="sxs-lookup"><span data-stu-id="efd3b-212">You must upload hello files as block blobs.</span></span> <span data-ttu-id="efd3b-213">Stronicowe obiekty BLOB nie są obsługiwane przez usługi Azure Media Services.</span><span class="sxs-lookup"><span data-stu-id="efd3b-213">Page blobs are not supported by Azure Media Services.</span></span>  

> [!NOTE]
> <span data-ttu-id="efd3b-214">Należy dodać nazwę pliku hello pliku hello ma toohello tooupload lokalizatora **ścieżki** odebrana w poprzedniej sekcji hello wartość.</span><span class="sxs-lookup"><span data-stu-id="efd3b-214">You must add hello file name for hello file you want tooupload toohello Locator **Path** value received in hello previous section.</span></span> <span data-ttu-id="efd3b-215">Na przykład https://storagetestaccount001.blob.core.windows.net/asset-e7b02da4-5a69-40e7-a8db-e8f4f697aac0/BigBuckBunny.mp4?</span><span class="sxs-lookup"><span data-stu-id="efd3b-215">For example, https://storagetestaccount001.blob.core.windows.net/asset-e7b02da4-5a69-40e7-a8db-e8f4f697aac0/BigBuckBunny.mp4?</span></span> <span data-ttu-id="efd3b-216">.</span><span class="sxs-lookup"><span data-stu-id="efd3b-216">.</span></span> <span data-ttu-id="efd3b-217">.</span><span class="sxs-lookup"><span data-stu-id="efd3b-217">.</span></span> <span data-ttu-id="efd3b-218">.</span><span class="sxs-lookup"><span data-stu-id="efd3b-218">.</span></span>
>
>

<span data-ttu-id="efd3b-219">Aby uzyskać więcej informacji na temat pracy z obiektami blob magazynu Azure, zobacz [interfejsu API REST usługi Blob](https://docs.microsoft.com/rest/api/storageservices/Blob-Service-REST-API).</span><span class="sxs-lookup"><span data-stu-id="efd3b-219">For more information on working with Azure storage blobs, see [Blob Service REST API](https://docs.microsoft.com/rest/api/storageservices/Blob-Service-REST-API).</span></span>

### <a name="update-hello-assetfile"></a><span data-ttu-id="efd3b-220">Aktualizacja hello AssetFile</span><span class="sxs-lookup"><span data-stu-id="efd3b-220">Update hello AssetFile</span></span>
<span data-ttu-id="efd3b-221">Teraz, przekazywanego pliku, zaktualizuj hello FileAsset rozmiarze (i innych) informacje.</span><span class="sxs-lookup"><span data-stu-id="efd3b-221">Now that you've uploaded your file, update hello FileAsset size (and other) information.</span></span> <span data-ttu-id="efd3b-222">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="efd3b-222">For example:</span></span>

    MERGE https://wamsbayclus001rest-hs.cloudapp.net/api/Files('nb%3Acid%3AUUID%3Af13a0137-0a62-9d4c-b3b9-ca944b5142c5') HTTP/1.1
    Content-Type: application/json
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amstestaccount001&urn%3aSubscriptionId=z7f09258-2233-4ca2-b1ae-193798e2c9d8&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1421662918&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=utmoXXbm9Q7j4tW1yJuMVA3egRiQy5FPygwadkmPeaY%3d
    x-ms-version: 2.11
    Host: wamsbayclus001rest-hs.cloudapp.net

    {  
       "ContentFileSize":"1186540",
       "Id":"nb:cid:UUID:f13a0137-0a62-9d4c-b3b9-ca944b5142c5",
       "MimeType":"video/mp4",
       "Name":"BigBuckBunny.mp4",
       "ParentAssetId":"nb:cid:UUID:9bc8ff20-24fb-4fdb-9d7c-b04c7ee573a1"
    }


<span data-ttu-id="efd3b-223">**Odpowiedź HTTP**</span><span class="sxs-lookup"><span data-stu-id="efd3b-223">**HTTP Response**</span></span>

<span data-ttu-id="efd3b-224">W przypadku powodzenia zwrócono hello następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="efd3b-224">If successful, hello following is returned:</span></span>

    HTTP/1.1 204 No Content
    ...

## <a name="delete-hello-locator-and-accesspolicy"></a><span data-ttu-id="efd3b-225">Usuń hello lokalizatora i AccessPolicy</span><span class="sxs-lookup"><span data-stu-id="efd3b-225">Delete hello Locator and AccessPolicy</span></span>
<span data-ttu-id="efd3b-226">**Żądania HTTP**</span><span class="sxs-lookup"><span data-stu-id="efd3b-226">**HTTP Request**</span></span>

    DELETE https://wamsbayclus001rest-hs.cloudapp.net/api/Locators('nb%3Alid%3AUUID%3Aaf57bdd8-6751-4e84-b403-f3c140444b54') HTTP/1.1
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amstestaccount001&urn%3aSubscriptionId=z7f09258-2233-4ca2-b1ae-193798e2c9d8&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1421662918&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=utmoXXbm9Q7j4tW1yJuMVA3egRiQy5FPygwadkmPeaY%3d
    x-ms-version: 2.11
    Host: wamsbayclus001rest-hs.cloudapp.net


<span data-ttu-id="efd3b-227">**Odpowiedź HTTP**</span><span class="sxs-lookup"><span data-stu-id="efd3b-227">**HTTP Response**</span></span>

<span data-ttu-id="efd3b-228">W przypadku powodzenia zwrócono hello następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="efd3b-228">If successful, hello following is returned:</span></span>

    HTTP/1.1 204 No Content
    ...

<span data-ttu-id="efd3b-229">**Żądania HTTP**</span><span class="sxs-lookup"><span data-stu-id="efd3b-229">**HTTP Request**</span></span>

    DELETE https://wamsbayclus001rest-hs.cloudapp.net/api/AccessPolicies('nb%3Apid%3AUUID%3Abe0ac48d-af7d-4877-9d60-1805d68bffae') HTTP/1.1
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amstestaccount001&urn%3aSubscriptionId=z7f09258-2233-4ca2-b1ae-193798e2c9d8&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1421662918&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=utmoXXbm9Q7j4tW1yJuMVA3egRiQy5FPygwadkmPeaY%3d
    x-ms-version: 2.11
    Host: wamsbayclus001rest-hs.cloudapp.net

<span data-ttu-id="efd3b-230">**Odpowiedź HTTP**</span><span class="sxs-lookup"><span data-stu-id="efd3b-230">**HTTP Response**</span></span>

<span data-ttu-id="efd3b-231">W przypadku powodzenia zwrócono hello następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="efd3b-231">If successful, hello following is returned:</span></span>

    HTTP/1.1 204 No Content
    ...

## <span data-ttu-id="efd3b-232"><a id="encode"></a>Kodowanie pliku źródłowego hello do zestawu plików MP4 z adaptacyjną szybkością transmisji bitów</span><span class="sxs-lookup"><span data-stu-id="efd3b-232"><a id="encode"></a>Encode hello source file into a set of adaptive bitrate MP4 files</span></span>

<span data-ttu-id="efd3b-233">Po wprowadzania, które mogą być kodowane zasoby w usłudze Media Services nośnika, poddane transmultipleksacji, oznaczone znakiem wodnym i tak dalej przed przekazaniem tooclients.</span><span class="sxs-lookup"><span data-stu-id="efd3b-233">After ingesting Assets into Media Services, media can be encoded, transmuxed, watermarked, and so on, before it is delivered tooclients.</span></span> <span data-ttu-id="efd3b-234">Te działania są zaplanowane i uruchomienia wielu tła roli wystąpień tooensure wysokiej wydajności i dostępności.</span><span class="sxs-lookup"><span data-stu-id="efd3b-234">These activities are scheduled and run against multiple background role instances tooensure high performance and availability.</span></span> <span data-ttu-id="efd3b-235">Te działania są nazywane zadaniami i każde zadanie składa się z niepodzielnych zadań, które hello rzeczywistą pracę w pliku trwałego hello (Aby uzyskać więcej informacji, zobacz [zadania](/rest/api/media/services/job), [zadań](/rest/api/media/services/task) opisy).</span><span class="sxs-lookup"><span data-stu-id="efd3b-235">These activities are called Jobs and each Job is composed of atomic Tasks that do hello actual work on hello Asset file (for more information, see [Job](/rest/api/media/services/job), [Task](/rest/api/media/services/task) descriptions).</span></span>

<span data-ttu-id="efd3b-236">Jak wspomniano wcześniej, podczas pracy z Azure Media Services jednym z najbardziej typowych scenariuszy hello jest dostarczanie przesyłania strumieniowego klientów tooyour adaptacyjną szybkością transmisji bitów.</span><span class="sxs-lookup"><span data-stu-id="efd3b-236">As was mentioned earlier, when working with Azure Media Services one of hello most common scenarios is delivering adaptive bitrate streaming tooyour clients.</span></span> <span data-ttu-id="efd3b-237">Usługi Media Services można dynamicznie pakietu do jednego z następujących formatów hello zestaw plików MP4 z adaptacyjną szybkością transmisji bitów: HTTP Live Streaming (HLS), Smooth Streaming, MPEG DASH.</span><span class="sxs-lookup"><span data-stu-id="efd3b-237">Media Services can dynamically package a set of adaptive bitrate MP4 files into one of hello following formats: HTTP Live Streaming (HLS), Smooth Streaming, MPEG DASH.</span></span>

<span data-ttu-id="efd3b-238">powitania po sekcji pokazano, jak toocreate zadanie, które zawiera jeden kodowania zadań.</span><span class="sxs-lookup"><span data-stu-id="efd3b-238">hello following section shows how toocreate a job that contains one encoding task.</span></span> <span data-ttu-id="efd3b-239">Witaj zadanie Określa plik mezzanine hello tootranscode do zestawu z adaptacyjną szybkością transmisji bitów MP4s przy użyciu **Media Encoder Standard**.</span><span class="sxs-lookup"><span data-stu-id="efd3b-239">hello task specifies tootranscode hello mezzanine file into a set of adaptive bitrate MP4s using **Media Encoder Standard**.</span></span> <span data-ttu-id="efd3b-240">Hello sekcji przedstawiono również sposób toomonitor hello postęp zadania przetwarzania.</span><span class="sxs-lookup"><span data-stu-id="efd3b-240">hello section also shows how toomonitor hello job processing progress.</span></span> <span data-ttu-id="efd3b-241">Po zakończeniu zadania hello będzie lokalizatorów można toocreate, będącymi aktywami tooyour dostępu tooget potrzebne.</span><span class="sxs-lookup"><span data-stu-id="efd3b-241">When hello job is complete, you would be able toocreate locators that are needed tooget access tooyour assets.</span></span>

### <a name="get-a-media-processor"></a><span data-ttu-id="efd3b-242">Pobierz procesor multimediów</span><span class="sxs-lookup"><span data-stu-id="efd3b-242">Get a media processor</span></span>
<span data-ttu-id="efd3b-243">W usłudze Media Services procesor multimediów jest składnikiem, który obsługuje przetwarzania specyficznego dla zadania, takie jak kodowanie, Konwersja formatu zawartości multimedialnej szyfrowania lub odszyfrowywania.</span><span class="sxs-lookup"><span data-stu-id="efd3b-243">In Media Services, a media processor is a component that handles a specific processing task, such as encoding, format conversion, encrypting, or decrypting media content.</span></span> <span data-ttu-id="efd3b-244">Dla hello kodowania zadań przedstawiona w tym samouczku zamierzamy hello toouse Media Encoder Standard.</span><span class="sxs-lookup"><span data-stu-id="efd3b-244">For hello encoding task shown in this tutorial, we are going toouse hello Media Encoder Standard.</span></span>

<span data-ttu-id="efd3b-245">Witaj poniższy kod identyfikatora żądania hello kodera.</span><span class="sxs-lookup"><span data-stu-id="efd3b-245">hello following code requests hello encoder's id.</span></span>

<span data-ttu-id="efd3b-246">**Żądania HTTP**</span><span class="sxs-lookup"><span data-stu-id="efd3b-246">**HTTP Request**</span></span>

    GET https://wamsbayclus001rest-hs.cloudapp.net/api/MediaProcessors()?$filter=Name%20eq%20'Media%20Encoder%20Standard' HTTP/1.1
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amstestaccount001&urn%3aSubscriptionId=f7f09258-6753-4ca2-b1ae-193798e2c9d8&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1421675491&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=9hUudHYnATpi5hN3cvTfgw%2bL4N3tL0fdsRnQnm6ZYIU%3d
    x-ms-version: 2.11
    Host: wamsbayclus001rest-hs.cloudapp.net


<span data-ttu-id="efd3b-247">**Odpowiedź HTTP**</span><span class="sxs-lookup"><span data-stu-id="efd3b-247">**HTTP Response**</span></span>

    HTTP/1.1 200 OK
    Cache-Control: no-cache
    Content-Length: 273
    Content-Type: application/json;odata=minimalmetadata;streaming=true;charset=utf-8
    Server: Microsoft-IIS/8.5
    request-id: 6beb04b4-55a7-480d-8aa8-e5c5d59ffa1f
    x-ms-request-id: 6beb04b4-55a7-480d-8aa8-e5c5d59ffa1f
    X-Content-Type-Options: nosniff
    DataServiceVersion: 3.0;
    X-Powered-By: ASP.NET
    Strict-Transport-Security: max-age=31536000; includeSubDomains
    Date: Mon, 19 Jan 2015 07:54:09 GMT

    {  
       "odata.metadata":"https://wamsbayclus001rest-hs.cloudapp.net/api/$metadata#MediaProcessors",
       "value":[  
          {  
             "Id":"nb:mpid:UUID:ff4df607-d419-42f0-bc17-a481b1331e56",
             "Description":"Media Encoder Standard",
             "Name":"Media Encoder Standard",
             "Sku":"",
             "Vendor":"Microsoft",
             "Version":"1.1"
          }
       ]
    }

### <a name="create-a-job"></a><span data-ttu-id="efd3b-248">Tworzenie zadania</span><span class="sxs-lookup"><span data-stu-id="efd3b-248">Create a job</span></span>
<span data-ttu-id="efd3b-249">Każde zadanie może zawierać jeden lub więcej zadań, w zależności od typu hello przetwarzania, które mają tooaccomplish.</span><span class="sxs-lookup"><span data-stu-id="efd3b-249">Each Job can have one or more Tasks depending on hello type of processing that you want tooaccomplish.</span></span> <span data-ttu-id="efd3b-250">Za pośrednictwem interfejsu API REST hello, można tworzyć zadania i ich zadania pokrewne w jeden z dwóch sposobów: zadania mogą być zdefiniowano w tekście za pośrednictwem właściwości nawigacji zadania hello na jednostkach zadania, lub przetwarzania wsadowego OData.</span><span class="sxs-lookup"><span data-stu-id="efd3b-250">Through hello REST API, you can create Jobs and their related Tasks in one of two ways: Tasks can be defined inline through hello Tasks navigation property on Job entities, or through OData batch processing.</span></span> <span data-ttu-id="efd3b-251">Witaj SDK usługi Media Services używa przetwarzania wsadowego.</span><span class="sxs-lookup"><span data-stu-id="efd3b-251">hello Media Services SDK uses batch processing.</span></span> <span data-ttu-id="efd3b-252">Aby zwiększyć czytelność hello hello przykładów kodu w tym temacie, zadania są zdefiniowano w tekście.</span><span class="sxs-lookup"><span data-stu-id="efd3b-252">However, for hello readability of hello code examples in this topic, tasks are defined inline.</span></span> <span data-ttu-id="efd3b-253">Informacje dotyczące przetwarzania wsadowego znajdują się w temacie [przetwarzanie wsadowe Open Data Protocol (OData)](http://www.odata.org/documentation/odata-version-3-0/batch-processing/).</span><span class="sxs-lookup"><span data-stu-id="efd3b-253">For information on batch processing, see [Open Data Protocol (OData) Batch Processing](http://www.odata.org/documentation/odata-version-3-0/batch-processing/).</span></span>

<span data-ttu-id="efd3b-254">Hello poniższy przykład przedstawia toocreate i post zadania jednego zadania konfiguracji tooencode wideo w określonej rozdzielczości i jakości.</span><span class="sxs-lookup"><span data-stu-id="efd3b-254">hello following example shows you how toocreate and post a Job with one Task set tooencode a video at a specific resolution and quality.</span></span> <span data-ttu-id="efd3b-255">powitania po sekcji dokumentacji zawiera listę hello wszystkich hello [zadań predefiniowane](http://msdn.microsoft.com/library/mt269960) obsługiwane przez procesor Media Encoder Standard hello.</span><span class="sxs-lookup"><span data-stu-id="efd3b-255">hello following documentation section contains hello list of all hello [task presets](http://msdn.microsoft.com/library/mt269960) supported by hello Media Encoder Standard processor.</span></span>  

<span data-ttu-id="efd3b-256">**Żądania HTTP**</span><span class="sxs-lookup"><span data-stu-id="efd3b-256">**HTTP Request**</span></span>

    POST https://wamsbayclus001rest-hs.cloudapp.net/api/Jobs HTTP/1.1
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Content-Type: application/json
    Accept: application/json;odata=verbose
    Accept-Charset: UTF-8
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amstestaccount001&urn%3aSubscriptionId=z7f09258-2233-4ca2-b1ae-193798e2c9d8&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1421675491&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=9hUudHYnATpi5hN3cvTfgw%2bL4N3tL0fdsRnQnm6ZYIU%3d
    x-ms-version: 2.11
    Host: wamsbayclus001rest-hs.cloudapp.net
    Content-Length: 482

    {  
       "Name":"NewTestJob",
       "InputMediaAssets":[  
          {  
             "__metadata":{  
                "uri":"https://wamsbayclus001rest-hs.net/api/Assets('nb%3Acid%3AUUID%3A9bc8ff20-24fb-4fdb-9d7c-b04c7ee573a1')"
             }
          }
       ],
       "Tasks":[  
          {  
             "Configuration":"Adaptive Streaming",
             "MediaProcessorId":"nb:mpid:UUID:ff4df607-d419-42f0-bc17-a481b1331e56",
             "TaskBody":"<?xml version=\"1.0\" encoding=\"utf-8\"?><taskBody><inputAsset>JobInputAsset(0)</inputAsset>
                <outputAsset>JobOutputAsset(0)</outputAsset></taskBody>"
          }
       ]
    }

<span data-ttu-id="efd3b-257">**Odpowiedź HTTP**</span><span class="sxs-lookup"><span data-stu-id="efd3b-257">**HTTP Response**</span></span>

<span data-ttu-id="efd3b-258">W przypadku powodzenia powitania po odpowiedzi jest zwracany:</span><span class="sxs-lookup"><span data-stu-id="efd3b-258">If successful, hello following response is returned:</span></span>

    HTTP/1.1 201 Created
    Cache-Control: no-cache
    Content-Length: 1215
    Content-Type: application/json;odata=verbose;charset=utf-8
    Location: https://wamsbayclus001rest-hs.cloudapp.net/api/Jobs('nb%3Ajid%3AUUID%3A71d2dd33-efdf-ec43-8ea1-136a110bd42c')
    Server: Microsoft-IIS/8.5
    request-id: 532ac1ec-a475-4dce-b2d5-7c8ce94ac87c
    x-ms-request-id: 532ac1ec-a475-4dce-b2d5-7c8ce94ac87c
    X-Content-Type-Options: nosniff
    DataServiceVersion: 3.0;
    X-Powered-By: ASP.NET
    Strict-Transport-Security: max-age=31536000; includeSubDomains
    Date: Mon, 19 Jan 2015 08:04:35 GMT

    {  
       "d":{  
          "__metadata":{  
             "id":"https://wamsbayclus001rest-hs.cloudapp.net/api/Jobs('nb%3Ajid%3AUUID%3A71d2dd33-efdf-ec43-8ea1-136a110bd42c')",
             "uri":"https://wamsbayclus001rest-hs.cloudapp.net/api/Jobs('nb%3Ajid%3AUUID%3A71d2dd33-efdf-ec43-8ea1-136a110bd42c')",
             "type":"Microsoft.Cloud.Media.Vod.Rest.Data.Models.Job"
          },
          "Tasks":{  
             "__deferred":{  
                "uri":"https://wamsbayclus001rest-hs.cloudapp.net/api/Jobs('nb%3Ajid%3AUUID%3A71d2dd33-efdf-ec43-8ea1-136a110bd42c')/Tasks"
             }
          },
          "OutputMediaAssets":{  
             "__deferred":{  
                "uri":"https://wamsbayclus001rest-hs.cloudapp.net/api/Jobs('nb%3Ajid%3AUUID%3A71d2dd33-efdf-ec43-8ea1-136a110bd42c')/OutputMediaAssets"
             }
          },
          "InputMediaAssets":{  
             "__deferred":{  
                "uri":"https://wamsbayclus001rest-hs.cloudapp.net/api/Jobs('nb%3Ajid%3AUUID%3A9bc8ff20-24fb-4fdb-9d7c-b04c7ee573a1')/InputMediaAssets"
             }
          },
          "Id":"nb:jid:UUID:71d2dd33-efdf-ec43-8ea1-136a110bd42c",
          "Name":"NewTestJob",
          "Created":"2015-01-19T08:04:34.3287057Z",
          "LastModified":"2015-01-19T08:04:34.3287057Z",
          "EndTime":null,
          "Priority":0,
          "RunningDuration":0,
          "StartTime":null,
          "State":0,
          "TemplateId":null,
          "JobNotificationSubscriptions":{  
             "__metadata":{  
                "type":"Collection(Microsoft.Cloud.Media.Vod.Rest.Data.Models.JobNotificationSubscription)"
             },
             "results":[  

             ]
          }
       }
    }


<span data-ttu-id="efd3b-259">Istnieje kilka ważnych rzeczy toonote w dowolnym żądaniu zadania:</span><span class="sxs-lookup"><span data-stu-id="efd3b-259">There are a few important things toonote in any Job request:</span></span>

* <span data-ttu-id="efd3b-260">Taskbody — właściwości należy użyć literału XML toodefine hello liczba danych wejściowych lub zasoby danych wyjściowych, które są używane przez hello zadań.</span><span class="sxs-lookup"><span data-stu-id="efd3b-260">TaskBody properties MUST use literal XML toodefine hello number of input, or output assets that are used by hello Task.</span></span> <span data-ttu-id="efd3b-261">temat zadania Hello zawiera hello definicji schematu XML dla hello XML.</span><span class="sxs-lookup"><span data-stu-id="efd3b-261">hello Task topic contains hello XML Schema Definition for hello XML.</span></span>
* <span data-ttu-id="efd3b-262">W definicji taskbody — Witaj, wartość każdego wewnętrzny <inputAsset> i <outputAsset> musi być ustawiona jako JobInputAsset(value) lub JobOutputAsset(value).</span><span class="sxs-lookup"><span data-stu-id="efd3b-262">In hello TaskBody definition, each inner value for <inputAsset> and <outputAsset> must be set as JobInputAsset(value) or JobOutputAsset(value).</span></span>
* <span data-ttu-id="efd3b-263">Zadanie może mieć wielu zasobów danych wyjściowych.</span><span class="sxs-lookup"><span data-stu-id="efd3b-263">A task can have multiple output assets.</span></span> <span data-ttu-id="efd3b-264">Jako dane wyjściowe zadania w ramach zadania jeden JobOutputAsset(x) można można użyć tylko raz.</span><span class="sxs-lookup"><span data-stu-id="efd3b-264">One JobOutputAsset(x) can only be used once as an output of a task in a job.</span></span>
* <span data-ttu-id="efd3b-265">JobInputAsset lub JobOutputAsset można określić jako zasób wprowadzania zadania.</span><span class="sxs-lookup"><span data-stu-id="efd3b-265">You can specify JobInputAsset or JobOutputAsset as an input asset of a task.</span></span>
* <span data-ttu-id="efd3b-266">Zadania musi nie tworzą cyklu.</span><span class="sxs-lookup"><span data-stu-id="efd3b-266">Tasks must not form a cycle.</span></span>
* <span data-ttu-id="efd3b-267">Parametr wartości Hello przekazujesz tooJobInputAsset lub JobOutputAsset reprezentuje hello wartość indeksu dla zasobu.</span><span class="sxs-lookup"><span data-stu-id="efd3b-267">hello value parameter that you pass tooJobInputAsset or JobOutputAsset represents hello index value for an Asset.</span></span> <span data-ttu-id="efd3b-268">Witaj rzeczywiste zasoby są definiowane w hello InputMediaAssets i OutputMediaAssets właściwości nawigacji na powitania definicji zadania jednostki.</span><span class="sxs-lookup"><span data-stu-id="efd3b-268">hello actual Assets are defined in hello InputMediaAssets and OutputMediaAssets navigation properties on hello Job entity definition.</span></span>

> [!NOTE]
> <span data-ttu-id="efd3b-269">Ponieważ usługi Media Services jest oparty na OData v3, hello poszczególne zasoby w InputMediaAssets i kolekcje właściwości nawigacji OutputMediaAssets są przywoływane przez "__metadata: identyfikator uri" pary nazwa wartość.</span><span class="sxs-lookup"><span data-stu-id="efd3b-269">Because Media Services is built on OData v3, hello individual assets in InputMediaAssets and OutputMediaAssets navigation property collections are referenced through a "__metadata : uri" name-value pair.</span></span>
>
>

* <span data-ttu-id="efd3b-270">InputMediaAssets mapuje tooone lub więcej zasobów, które zostały utworzone w usłudze Media Services.</span><span class="sxs-lookup"><span data-stu-id="efd3b-270">InputMediaAssets maps tooone or more Assets you have created in Media Services.</span></span> <span data-ttu-id="efd3b-271">OutputMediaAssets są tworzone przez hello system.</span><span class="sxs-lookup"><span data-stu-id="efd3b-271">OutputMediaAssets are created by hello system.</span></span> <span data-ttu-id="efd3b-272">Nie odwołują się do istniejącego zasobu.</span><span class="sxs-lookup"><span data-stu-id="efd3b-272">They do not reference an existing asset.</span></span>
* <span data-ttu-id="efd3b-273">Może być nazwany OutputMediaAssets przy użyciu atrybutu assetName hello.</span><span class="sxs-lookup"><span data-stu-id="efd3b-273">OutputMediaAssets can be named using hello assetName attribute.</span></span> <span data-ttu-id="efd3b-274">Jeśli ten atrybut nie jest obecny, a następnie nazwę hello hello OutputMediaAsset jest niezależnie od wartości tekst wewnętrzny hello hello <outputAsset> element jest z sufiksem hello Nazwa zadania wartość lub wartość identyfikatora zadania hello (w przypadku hello, w których właściwość Name hello nie jest zdefiniowana).</span><span class="sxs-lookup"><span data-stu-id="efd3b-274">If this attribute is not present, then hello name of hello OutputMediaAsset is whatever hello inner text value of hello <outputAsset> element is with a suffix of either hello Job Name value, or hello Job Id value (in hello case where hello Name property isn't defined).</span></span> <span data-ttu-id="efd3b-275">Na przykład jeśli zostanie ustawiona wartość assetName zbyt "Test", a następnie hello nazwa OutputMediaAsset można ustawić właściwości zbyt "Sample".</span><span class="sxs-lookup"><span data-stu-id="efd3b-275">For example, if you set a value for assetName too"Sample", then hello OutputMediaAsset Name property would be set too"Sample".</span></span> <span data-ttu-id="efd3b-276">Jednak jeśli nie ustawiona wartość assetName, ale ustawiona nazwa zadania hello zbyt "NewJob", a następnie hello nazwa OutputMediaAsset się "_NewJob JobOutputAsset (wartość)".</span><span class="sxs-lookup"><span data-stu-id="efd3b-276">However, if you did not set a value for assetName, but did set hello job name too"NewJob", then hello OutputMediaAsset Name would be "JobOutputAsset(value)_NewJob".</span></span>

    <span data-ttu-id="efd3b-277">Witaj poniższy przykład pokazuje, jak tooset hello assetName atrybutu:</span><span class="sxs-lookup"><span data-stu-id="efd3b-277">hello following example shows how tooset hello assetName attribute:</span></span>

        "<?xml version=\"1.0\" encoding=\"utf-8\"?><taskBody><inputAsset>JobInputAsset(0)</inputAsset><outputAsset assetName=\"CustomOutputAssetName\">JobOutputAsset(0)</outputAsset></taskBody>"
* <span data-ttu-id="efd3b-278">Tworzenie łańcuchów tooenable zadań:</span><span class="sxs-lookup"><span data-stu-id="efd3b-278">tooenable task chaining:</span></span>

  * <span data-ttu-id="efd3b-279">Zadanie musi mieć co najmniej dwa zadania</span><span class="sxs-lookup"><span data-stu-id="efd3b-279">A job must have at least two tasks</span></span>
  * <span data-ttu-id="efd3b-280">Musi istnieć co najmniej jedno zadanie, którego danych wejściowych jest inne zadanie w zadaniu hello dane wyjściowe.</span><span class="sxs-lookup"><span data-stu-id="efd3b-280">There must be at least one task whose input is output of another task in hello job.</span></span>

<span data-ttu-id="efd3b-281">Aby uzyskać więcej informacji, zobacz [Tworzenie zadania kodowania z hello interfejsu API REST usług Media](media-services-rest-encode-asset.md).</span><span class="sxs-lookup"><span data-stu-id="efd3b-281">For more information see, [Creating an Encoding Job with hello Media Services REST API](media-services-rest-encode-asset.md).</span></span>

### <a name="monitor-processing-progress"></a><span data-ttu-id="efd3b-282">Monitor przetwarzania postępu</span><span class="sxs-lookup"><span data-stu-id="efd3b-282">Monitor Processing Progress</span></span>
<span data-ttu-id="efd3b-283">Stan zadania hello można pobrać za pomocą właściwości stanu hello, jak pokazano w hello poniższy przykład.</span><span class="sxs-lookup"><span data-stu-id="efd3b-283">You can retrieve hello Job status by using hello State property, as shown in hello following example.</span></span>

<span data-ttu-id="efd3b-284">**Żądania HTTP**</span><span class="sxs-lookup"><span data-stu-id="efd3b-284">**HTTP Request**</span></span>

    GET https://wamsbayclus001rest-hs.net/api/Jobs('nb%3Ajid%3AUUID%3A71d2dd33-efdf-ec43-8ea1-136a110bd42c')/State HTTP/1.1
    Content-Type: application/json;odata=verbose
    Accept: application/json;odata=verbose
    DataServiceVersion: 3.0
    MaxDataServiceVersion: 3.0
    x-ms-version: 2.11
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=youraccountname&urn%3aSubscriptionId=zf84471d-2233-4e75-aa09-010f0fc0cf5b&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1336908022&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=RYXOraO6Z%2f7l9whWZQN%2bypeijgHwIk8XyikA01Kx1%2bk%3d
    Host: wamsbayclus001rest-hs.net
    Content-Length: 0


<span data-ttu-id="efd3b-285">**Odpowiedź HTTP**</span><span class="sxs-lookup"><span data-stu-id="efd3b-285">**HTTP Response**</span></span>

<span data-ttu-id="efd3b-286">W przypadku powodzenia powitania po odpowiedzi jest zwracany:</span><span class="sxs-lookup"><span data-stu-id="efd3b-286">If successful, hello following response is returned:</span></span>

    HTTP/1.1 200 OK
    Cache-Control: no-cache
    Content-Length: 17
    Content-Type: application/json;odata=verbose;charset=utf-8
    Server: Microsoft-IIS/7.5
    x-ms-request-id: 01324d81-18e2-4493-a3e5-c6186209f0c8
    X-Content-Type-Options: nosniff
    DataServiceVersion: 1.0;
    X-AspNet-Version: 4.0.30319
    X-Powered-By: ASP.NET
    Date: Sun, 13 May 2012 05:16:53 GMT

    {"d":{"State":2}}


### <a name="cancel-a-job"></a><span data-ttu-id="efd3b-287">Anulowanie zadania</span><span class="sxs-lookup"><span data-stu-id="efd3b-287">Cancel a job</span></span>
<span data-ttu-id="efd3b-288">Usługa Media Services umożliwia toocancel uruchomionych zadań za pomocą funkcji CancelJob hello.</span><span class="sxs-lookup"><span data-stu-id="efd3b-288">Media Services allows you toocancel running jobs through hello CancelJob function.</span></span> <span data-ttu-id="efd3b-289">To wywołanie zwraca kod błędu 400, Jeśli spróbujesz toocancel zadania po anulowaniu jej stan, anulowanie, błąd lub zakończona.</span><span class="sxs-lookup"><span data-stu-id="efd3b-289">This call returns a 400 error code if you try toocancel a Job when its state is canceled, canceling, error, or finished.</span></span>

<span data-ttu-id="efd3b-290">powitania po przykładzie pokazano, jak toocall CancelJob.</span><span class="sxs-lookup"><span data-stu-id="efd3b-290">hello following example shows how toocall CancelJob.</span></span>

<span data-ttu-id="efd3b-291">**Żądania HTTP**</span><span class="sxs-lookup"><span data-stu-id="efd3b-291">**HTTP Request**</span></span>

    GET https://wamsbayclus001rest-hs.net/API/CancelJob?jobid='nb%3ajid%3aUUID%3a71d2dd33-efdf-ec43-8ea1-136a110bd42c' HTTP/1.1
    Content-Type: application/json;odata=verbose
    Accept: application/json;odata=verbose
    DataServiceVersion: 3.0
    MaxDataServiceVersion: 3.0
    x-ms-version: 2.2
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=youraccountname&urn%3aSubscriptionId=2f84471d-b1ae-4e75-aa09-010f0fc0cf5b&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1336908753&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=kolAgnFfbQIeRv4lWxKSFa4USyjWXRm15Kd%2bNd5g8eA%3d
    Host: wamsbayclus001rest-hs.net


<span data-ttu-id="efd3b-292">W przypadku powodzenia kodu 204 odpowiedź jest zwracana z treści wiadomości.</span><span class="sxs-lookup"><span data-stu-id="efd3b-292">If successful, a 204 response code is returned with no message body.</span></span>

> [!NOTE]
> <span data-ttu-id="efd3b-293">Należy zakodować adresu URL hello identyfikator zadania (zazwyczaj nb:jid:UUID: somevalue) podczas przekazywania go jako tooCancelJob parametru.</span><span class="sxs-lookup"><span data-stu-id="efd3b-293">You must URL-encode hello job id (normally nb:jid:UUID: somevalue) when passing it in as a parameter tooCancelJob.</span></span>
>
>

### <a name="get-hello-output-asset"></a><span data-ttu-id="efd3b-294">Pobierz zawartości wyjściowej hello</span><span class="sxs-lookup"><span data-stu-id="efd3b-294">Get hello output asset</span></span>
<span data-ttu-id="efd3b-295">Witaj poniższy kod przedstawia sposób toorequest hello output zasobów identyfikatora.</span><span class="sxs-lookup"><span data-stu-id="efd3b-295">hello following code shows how toorequest hello output asset Id.</span></span>

<span data-ttu-id="efd3b-296">**Żądania HTTP**</span><span class="sxs-lookup"><span data-stu-id="efd3b-296">**HTTP Request**</span></span>

    GET https://wamsbayclus001rest-hs.cloudapp.net/api/Jobs('nb%3Ajid%3AUUID%3A71d2dd33-efdf-ec43-8ea1-136a110bd42c')/OutputMediaAssets() HTTP/1.1
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    User-Agent: Microsoft ADO.NET Data Services
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amstestaccount001&urn%3aSubscriptionId=z7f09258-2233-4ca2-b1ae-193798e2c9d8&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1421675491&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=9hUudHYnATpi5hN3cvTfgw%2bL4N3tL0fdsRnQnm6ZYIU%3d
    x-ms-version: 2.11
    Host: wamsbayclus001rest-hs.cloudapp.net


<span data-ttu-id="efd3b-297">**Odpowiedź HTTP**</span><span class="sxs-lookup"><span data-stu-id="efd3b-297">**HTTP Response**</span></span>

    HTTP/1.1 200 OK
    Cache-Control: no-cache
    Content-Length: 445
    Content-Type: application/json;odata=minimalmetadata;streaming=true;charset=utf-8
    Server: Microsoft-IIS/8.5
    request-id: 73cd605d-066a-46f1-8358-f4bd25a9220a
    x-ms-request-id: 73cd605d-066a-46f1-8358-f4bd25a9220a
    X-Content-Type-Options: nosniff
    DataServiceVersion: 3.0;
    X-Powered-By: ASP.NET
    Strict-Transport-Security: max-age=31536000; includeSubDomains
    Date: Mon, 19 Jan 2015 08:28:13 GMT

    {  
       "odata.metadata":"https://wamsbayclus001rest-hs.cloudapp.net/api/$metadata#Assets",
       "value":[  
          {  
             "Id":"nb:cid:UUID:71d2dd33-efdf-ec43-8ea1-136a110bd42c",
             "State":0,
             "Created":"2015-01-19T07:52:15.603",
             "LastModified":"2015-01-19T07:52:15.603",
             "AlternateId":null,
             "Name":"Multibitrate MP4s",
             "Options":0,
             "Uri":"https://storagetestaccount001.blob.core.windows.net/asset-71d2dd33-efdf-ec43-8ea1-136a110bd42c",
             "StorageAccountName":"storagetestaccount001"
          }
       ]
    }



## <span data-ttu-id="efd3b-298"><a id="publish_get_urls"></a>Publikowanie zawartości hello i get przesyłania strumieniowego i pobierania progresywnego adresy URL z interfejsu API REST</span><span class="sxs-lookup"><span data-stu-id="efd3b-298"><a id="publish_get_urls"></a>Publish hello asset and get streaming and progressive download URLs with REST API</span></span>

<span data-ttu-id="efd3b-299">toostream lub pobierania zawartości, należy najpierw należy zbyt opublikować, przez utworzenie lokalizatora.</span><span class="sxs-lookup"><span data-stu-id="efd3b-299">toostream or download an asset, you first need too"publish" it by creating a locator.</span></span> <span data-ttu-id="efd3b-300">Lokalizatory zapewniają toofiles dostępu do zawartych w hello zasobów.</span><span class="sxs-lookup"><span data-stu-id="efd3b-300">Locators provide access toofiles contained in hello asset.</span></span> <span data-ttu-id="efd3b-301">Usługa Media Services obsługuje dwa typy lokalizatorów: OnDemandOrigin lokalizatory nośniki używane toostream (na przykład MPEG DASH, HLS lub Smooth Streaming) i lokalizatorów podpis dostępu (SAS) używane toodownload plików multimedialnych.</span><span class="sxs-lookup"><span data-stu-id="efd3b-301">Media Services supports two types of locators: OnDemandOrigin locators, used toostream media (for example, MPEG DASH, HLS, or Smooth Streaming) and Access Signature (SAS) locators, used toodownload media files.</span></span> <span data-ttu-id="efd3b-302">Aby uzyskać więcej informacji na temat sygnatury dostępu Współdzielonego Zobacz lokalizatorów [to](http://southworks.com/blog/2015/05/27/reusing-azure-media-services-locators-to-avoid-facing-the-5-shared-access-policy-limitation/) blogu.</span><span class="sxs-lookup"><span data-stu-id="efd3b-302">For more information about SAS locators see [this](http://southworks.com/blog/2015/05/27/reusing-azure-media-services-locators-to-avoid-facing-the-5-shared-access-policy-limitation/) blog.</span></span>

<span data-ttu-id="efd3b-303">Po utworzeniu lokalizatorów hello można tworzyć adresy URL hello, które są używane toostream lub pobierania plików.</span><span class="sxs-lookup"><span data-stu-id="efd3b-303">Once you create hello locators, you can build hello URLs that are used toostream or download your files.</span></span>

>[!NOTE]
><span data-ttu-id="efd3b-304">Po utworzeniu konta usługi AMS **domyślne** punktu końcowego przesyłania strumieniowego w brzmieniu konta tooyour hello **zatrzymane** stanu.</span><span class="sxs-lookup"><span data-stu-id="efd3b-304">When your AMS account is created a **default** streaming endpoint is added tooyour account in hello **Stopped** state.</span></span> <span data-ttu-id="efd3b-305">przesyłanie strumieniowe zawartości i podejmij korzyści z dynamicznego tworzenia pakietów i dynamicznego szyfrowania toostart hello punktu końcowego przesyłania strumieniowego, z którego mają zostać toostream zawartość ma toobe w hello **systemem** stanu.</span><span class="sxs-lookup"><span data-stu-id="efd3b-305">toostart streaming your content and take advantage of dynamic packaging and dynamic encryption, hello streaming endpoint from which you want toostream content has toobe in hello **Running** state.</span></span>

<span data-ttu-id="efd3b-306">Adres URL dla protokołu Smooth Streaming ma hello następującego formatu:</span><span class="sxs-lookup"><span data-stu-id="efd3b-306">A streaming URL for Smooth Streaming has hello following format:</span></span>

    {streaming endpoint name-media services account name}.streaming.mediaservices.windows.net/{locator ID}/{filename}.ism/Manifest

<span data-ttu-id="efd3b-307">Adres URL dla protokołu HLS ma hello następującego formatu:</span><span class="sxs-lookup"><span data-stu-id="efd3b-307">A streaming URL for HLS has hello following format:</span></span>

    {streaming endpoint name-media services account name}.streaming.mediaservices.windows.net/{locator ID}/{filename}.ism/Manifest(format=m3u8-aapl)

<span data-ttu-id="efd3b-308">Adres URL przesyłania strumieniowego MPEG DASH ma hello następującego formatu:</span><span class="sxs-lookup"><span data-stu-id="efd3b-308">A streaming URL for MPEG DASH has hello following format:</span></span>

    {streaming endpoint name-media services account name}.streaming.mediaservices.windows.net/{locator ID}/{filename}.ism/Manifest(format=mpd-time-csf)


<span data-ttu-id="efd3b-309">Pliki toodownload adres URL SAS używany ma hello następującego formatu:</span><span class="sxs-lookup"><span data-stu-id="efd3b-309">A SAS URL used toodownload files has hello following format:</span></span>

    {blob container name}/{asset name}/{file name}/{SAS signature}

<span data-ttu-id="efd3b-310">W tej sekcji przedstawiono, jak tooperform hello następujące zadania niezbędne zbyt "Publikuj" zasobów.</span><span class="sxs-lookup"><span data-stu-id="efd3b-310">This section shows how tooperform hello following tasks necessary too"publish" your assets.</span></span>  

* <span data-ttu-id="efd3b-311">Tworzenie hello AccessPolicy z uprawnieniem do odczytu</span><span class="sxs-lookup"><span data-stu-id="efd3b-311">Creating hello AccessPolicy with read permission</span></span>
* <span data-ttu-id="efd3b-312">Tworzenie adres URL SAS dla pobierania zawartości</span><span class="sxs-lookup"><span data-stu-id="efd3b-312">Creating a SAS URL for downloading content</span></span>
* <span data-ttu-id="efd3b-313">Tworzenie źródłowy adres URL przesyłania strumieniowego zawartości</span><span class="sxs-lookup"><span data-stu-id="efd3b-313">Creating an origin URL for streaming content</span></span>

### <a name="creating-hello-accesspolicy-with-read-permission"></a><span data-ttu-id="efd3b-314">Tworzenie hello AccessPolicy z uprawnieniem do odczytu</span><span class="sxs-lookup"><span data-stu-id="efd3b-314">Creating hello AccessPolicy with read permission</span></span>
<span data-ttu-id="efd3b-315">Przed pobraniem lub przesyłania strumieniowego zawartości nośnika, należy najpierw zdefiniować AccessPolicy z uprawnienia do odczytu i utworzyć hello odpowiednie lokalizatora jednostki, która określa typ hello mechanizm dostarczania ma tooenable dla klientów.</span><span class="sxs-lookup"><span data-stu-id="efd3b-315">Before downloading or streaming any media content, first define an AccessPolicy with read permissions and create hello appropriate Locator entity that specifies hello type of delivery mechanism you want tooenable for your clients.</span></span> <span data-ttu-id="efd3b-316">Aby uzyskać więcej informacji o dostępnych właściwości hello, zobacz [właściwości jednostki AccessPolicy](https://docs.microsoft.com/rest/api/media/operations/accesspolicy#accesspolicy_properties).</span><span class="sxs-lookup"><span data-stu-id="efd3b-316">For more information on hello properties available, see [AccessPolicy Entity Properties](https://docs.microsoft.com/rest/api/media/operations/accesspolicy#accesspolicy_properties).</span></span>

<span data-ttu-id="efd3b-317">Witaj poniższy przykład pokazuje, jak toospecify hello AccessPolicy dla uprawnień odczytu dla danego elementu zawartości.</span><span class="sxs-lookup"><span data-stu-id="efd3b-317">hello following example shows how toospecify hello AccessPolicy for read permissions for a given Asset.</span></span>

    POST https://wamsbayclus001rest-hs.net/API/AccessPolicies HTTP/1.1
    Content-Type: application/json
    Accept: application/json
    DataServiceVersion: 3.0
    MaxDataServiceVersion: 3.0
    x-ms-version: 2.11
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=youraccountname&urn%3aSubscriptionId=2f84471d-b1ae-4e75-aa09-010f0fc0cf5b&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1337067658&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=dithjGvlXR9HlyAf5DE99N5OCYkPAxsHIcsTSjm9%2fVE%3d
    Host: wamsbayclus001rest-hs.net
    Content-Length: 74
    Expect: 100-continue

    {"Name": "DownloadPolicy", "DurationInMinutes" : "300", "Permissions" : 1}

<span data-ttu-id="efd3b-318">W przypadku powodzenia zostanie zwrócony kod 201 sukces, opisujący hello AccessPolicy jednostki, która zostanie utworzona.</span><span class="sxs-lookup"><span data-stu-id="efd3b-318">If successful, a 201 success code is returned describing hello AccessPolicy entity that you created.</span></span> <span data-ttu-id="efd3b-319">Następnie należy użyć hello identyfikator AccessPolicy wraz z hello identyfikator zasobu hello zawartości, który zawiera plik hello ma jednostki lokalizatora hello toocreate toodeliver (na przykład zasób dane wyjściowe).</span><span class="sxs-lookup"><span data-stu-id="efd3b-319">You then use hello AccessPolicy Id along with hello Asset Id of hello asset that contains hello file you want toodeliver(such as an output asset) toocreate hello Locator entity.</span></span>

> [!NOTE]
> <span data-ttu-id="efd3b-320">Ten podstawowy przepływ pracy jest hello taki sam jak przekazywanie pliku podczas wprowadzania zasobów (zgodnie z opisem został wcześniej w tym temacie).</span><span class="sxs-lookup"><span data-stu-id="efd3b-320">This basic workflow is hello same as uploading a file when ingesting an Asset (as was discussed earlier in this topic).</span></span> <span data-ttu-id="efd3b-321">Również takich jak przekazywanie plików, jeśli użytkownik (lub klientów) należy tooaccess plików natychmiast, należy ustawić Twojej StartTime wartość toofive minut przed hello bieżący czas.</span><span class="sxs-lookup"><span data-stu-id="efd3b-321">Also, like uploading files, if you (or your clients) need tooaccess your files immediately, set your StartTime value toofive minutes before hello current time.</span></span> <span data-ttu-id="efd3b-322">Ta akcja jest niezbędne, ponieważ może istnieć zegara pochylenia między powitania klienta i usługi Media Services.</span><span class="sxs-lookup"><span data-stu-id="efd3b-322">This action is necessary because there may be clock skew between hello client and Media Services.</span></span> <span data-ttu-id="efd3b-323">Hello wartości StartTime musi należeć do powitania po formacie daty/godziny: RRRR-MM-ddtgg (na przykład "2014-05-23T17:53:50Z").</span><span class="sxs-lookup"><span data-stu-id="efd3b-323">hello StartTime value must be in hello following DateTime format: YYYY-MM-DDTHH:mm:ssZ (for example, "2014-05-23T17:53:50Z").</span></span>
>
>

### <a name="creating-a-sas-url-for-downloading-content"></a><span data-ttu-id="efd3b-324">Tworzenie adres URL SAS dla pobierania zawartości</span><span class="sxs-lookup"><span data-stu-id="efd3b-324">Creating a SAS URL for downloading content</span></span>
<span data-ttu-id="efd3b-325">Hello następującego kodu pokazuje sposób tooget adres URL, które mogą być używane toodownload plik nośnika utworzony i przekazać wcześniej.</span><span class="sxs-lookup"><span data-stu-id="efd3b-325">hello following code shows how tooget a URL that can be used toodownload a media file created and uploaded previously.</span></span> <span data-ttu-id="efd3b-326">Witaj AccessPolicy zapoznał zestaw uprawnień i hello lokalizatora ścieżki odwołuje się adres URL pobierania SAS tooa.</span><span class="sxs-lookup"><span data-stu-id="efd3b-326">hello AccessPolicy has read permissions set and hello Locator path refers tooa SAS download URL.</span></span>

    POST https://wamsbayclus001rest-hs.net/API/Locators HTTP/1.1
    Content-Type: application/json
    Accept: application/json
    DataServiceVersion: 3.0
    MaxDataServiceVersion: 3.0
    x-ms-version: 2.11
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=youraccountname&urn%3aSubscriptionId=zf84471d-b1ae-2233-aa09-010f0fc0cf5b&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1337067658&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=dithjGvlXR9HlyAf5DE99N5OCYkPAxsHIcsTSjm9%2fVE%3d
    Host: wamsbayclus001rest-hs.net
    Content-Length: 182
    Expect: 100-continue

    {"AccessPolicyId": "nb:pid:UUID:38c71dd0-44c5-4c5f-8418-08bb6fbf7bf8", "AssetId" : "nb:cid:UUID:71d2dd33-efdf-ec43-8ea1-136a110bd42c", "StartTime" : "2014-05-17T16:45:53", "Type":1}

<span data-ttu-id="efd3b-327">W przypadku powodzenia powitania po odpowiedzi jest zwracany:</span><span class="sxs-lookup"><span data-stu-id="efd3b-327">If successful, hello following response is returned:</span></span>

    HTTP/1.1 201 Created
    Cache-Control: no-cache
    Content-Length: 1150
    Content-Type: application/json;odata=verbose;charset=utf-8
    Location: https://wamsbayclus001rest-hs.net/api/Locators('nb%3Alid%3AUUID%3A8e5a821d-2194-4d00-8884-adf979856874')
    Server: Microsoft-IIS/7.5
    x-ms-request-id: 8cfd8556-3064-416a-97f2-67d9e35f0911
    X-Content-Type-Options: nosniff
    DataServiceVersion: 1.0;
    X-AspNet-Version: 4.0.30319
    X-Powered-By: ASP.NET
    Date: Mon, 14 May 2012 21:41:32 GMT

    {  
       "d":{  
          "__metadata":{  
             "id":"https://wamsbayclus001rest-hs.net/api/Locators('nb%3Alid%3AUUID%3A8e5a821d-2194-4d00-8884-adf979856874')",
             "uri":"https://wamsbayclus001rest-hs.net/api/Locators('nb%3Alid%3AUUID%3A8e5a821d-2194-4d00-8884-adf979856874')",
             "type":"Microsoft.Cloud.Media.Vod.Rest.Data.Models.Locator"
          },
          "AccessPolicy":{  
             "__deferred":{  
                "uri":"https://wamsbayclus001rest-hs.net/api/Locators('nb%3Alid%3AUUID%3A8e5a821d-2194-4d00-8884-adf979856874')/AccessPolicy"
             }
          },
          "Asset":{  
             "__deferred":{  
                "uri":"https://wamsbayclus001rest-hs.net/api/Locators('nb%3Alid%3AUUID%3A71d2dd33-efdf-ec43-8ea1-136a110bd42c')/Asset"
             }
          },
          "Id":"nb:lid:UUID:8e5a821d-2194-4d00-8884-adf979856874",
          "ExpirationDateTime":"\/Date(1337049393000)\/",
          "Type":1,
          "Path":"https://storagetestaccount001.blob.core.windows.net/asset-71d2dd33-efdf-ec43-8ea1-136a110bd42c?st=2012-05-14T21%3A36%3A33Z&se=2012-05-15T02%3A36%3A33Z&sr=c&si=8e5a821d-2194-4d00-8884-adf979856874&sig=y75dViDpC5V8WutrXM%2B%2FGpR3uOtqmlISiNlHU1YUBOg%3D",
          "AccessPolicyId":"nb:pid:UUID:38c71dd0-44c5-4c5f-8418-08bb6fbf7bf8",
          "AssetId":"nb:cid:UUID:71d2dd33-efdf-ec43-8ea1-136a110bd42c",
          "StartTime":"\/Date(1337031393000)\/"
       }
    }


<span data-ttu-id="efd3b-328">Witaj zwrócił **ścieżki** właściwość zawiera hello adres URL SAS.</span><span class="sxs-lookup"><span data-stu-id="efd3b-328">hello returned **Path** property contains hello SAS URL.</span></span>

> [!NOTE]
> <span data-ttu-id="efd3b-329">Czy pobierać zawartość magazynu zaszyfrowane, musisz ręcznie go odszyfrować przed renderowaniem go lub użyj hello MediaProcessor odszyfrowywania magazynu w toooutput zadań przetwarzania przetwarzane pliki w hello wyczyść tooan OutputAsset, a następnie pobrać z tego zasobu.</span><span class="sxs-lookup"><span data-stu-id="efd3b-329">If you download storage encrypted content, you must manually decrypt it before rendering it, or use hello Storage Decryption MediaProcessor in a processing task toooutput processed files in hello clear tooan OutputAsset and then download from that Asset.</span></span> <span data-ttu-id="efd3b-330">Aby uzyskać więcej informacji na temat przetwarzania Zobacz Tworzenie zadania kodowania z hello interfejsu API REST usług Media.</span><span class="sxs-lookup"><span data-stu-id="efd3b-330">For more information on processing, see Creating an Encoding Job with hello Media Services REST API.</span></span> <span data-ttu-id="efd3b-331">Ponadto nie można zaktualizować lokalizatorów adres URL SAS, po ich utworzeniu.</span><span class="sxs-lookup"><span data-stu-id="efd3b-331">Also, SAS URL Locators cannot be updated after they have been created.</span></span> <span data-ttu-id="efd3b-332">Na przykład nie można ponownie użyć tej samej lokalizacji z zaktualizowanej wartości StartTime hello.</span><span class="sxs-lookup"><span data-stu-id="efd3b-332">For example, you cannot reuse hello same Locator with an updated StartTime value.</span></span> <span data-ttu-id="efd3b-333">Jest to spowodowane hello sposobu tworzenia adresów URL SAS.</span><span class="sxs-lookup"><span data-stu-id="efd3b-333">This is because of hello way SAS URLs are created.</span></span> <span data-ttu-id="efd3b-334">Chcesz tooaccess zasób do pobrania, po upływie lokalizatora, musi utworzyć nową z nowego czas rozpoczęcia.</span><span class="sxs-lookup"><span data-stu-id="efd3b-334">If you want tooaccess an asset for download after a Locator has expired, then you must create a new one with a new StartTime.</span></span>
>
>

### <a name="download-files"></a><span data-ttu-id="efd3b-335">Pobieranie plików</span><span class="sxs-lookup"><span data-stu-id="efd3b-335">Download files</span></span>
<span data-ttu-id="efd3b-336">Po utworzeniu hello AccessPolicy i lokalizatora zestawu, możesz pobrać plików za pomocą hello interfejsów API REST magazynu Azure.</span><span class="sxs-lookup"><span data-stu-id="efd3b-336">Once you have hello AccessPolicy and Locator set, you can download files using hello Azure Storage REST APIs.</span></span>  

> [!NOTE]
> <span data-ttu-id="efd3b-337">Należy dodać nazwę pliku hello pliku hello ma toohello toodownload lokalizatora **ścieżki** odebrana w poprzedniej sekcji hello wartość.</span><span class="sxs-lookup"><span data-stu-id="efd3b-337">You must add hello file name for hello file you want toodownload toohello Locator **Path** value received in hello previous section.</span></span> <span data-ttu-id="efd3b-338">Na przykład https://storagetestaccount001.blob.core.windows.net/asset-e7b02da4-5a69-40e7-a8db-e8f4f697aac0/BigBuckBunny.mp4?</span><span class="sxs-lookup"><span data-stu-id="efd3b-338">For example, https://storagetestaccount001.blob.core.windows.net/asset-e7b02da4-5a69-40e7-a8db-e8f4f697aac0/BigBuckBunny.mp4?</span></span> <span data-ttu-id="efd3b-339">.</span><span class="sxs-lookup"><span data-stu-id="efd3b-339">.</span></span> <span data-ttu-id="efd3b-340">.</span><span class="sxs-lookup"><span data-stu-id="efd3b-340">.</span></span> <span data-ttu-id="efd3b-341">.</span><span class="sxs-lookup"><span data-stu-id="efd3b-341">.</span></span>
>
>

<span data-ttu-id="efd3b-342">Aby uzyskać więcej informacji na temat pracy z obiektami blob magazynu Azure, zobacz [interfejsu API REST usługi Blob](https://docs.microsoft.com/rest/api/storageservices/Blob-Service-REST-API).</span><span class="sxs-lookup"><span data-stu-id="efd3b-342">For more information on working with Azure storage blobs, see [Blob Service REST API](https://docs.microsoft.com/rest/api/storageservices/Blob-Service-REST-API).</span></span>

<span data-ttu-id="efd3b-343">W wyniku hello kodowanie zadanie, które wcześniej wykonywanej (kodowanie na zestaw MP4 z adaptacyjną) masz wiele plików MP4, które można pobrać progresywnie.</span><span class="sxs-lookup"><span data-stu-id="efd3b-343">As a result of hello encoding job that you performed earlier (encoding into Adaptive MP4 set), you have multiple MP4 files that you can progressively download.</span></span> <span data-ttu-id="efd3b-344">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="efd3b-344">For example:</span></span>    

    https://storagetestaccount001.blob.core.windows.net/asset-38058602-a4b8-4b33-b9f0-6880dc1490ea/BigBuckBunny_H264_650kbps_AAC_und_ch2_96kbps.mp4?sv=2012-02-12&sr=c&si=166d5154-b801-410b-a226-ee2f8eac1929&sig=P2iNZJAvAWpp%2Bj9yV6TQjoz5DIIaj7ve8ARynmEM6Xk%3D&se=2015-02-14T01:13:05Z

    https://storagetestaccount001.blob.core.windows.net/asset-38058602-a4b8-4b33-b9f0-6880dc1490ea/BigBuckBunny_H264_400kbps_AAC_und_ch2_96kbps.mp4?sv=2012-02-12&sr=c&si=166d5154-b801-410b-a226-ee2f8eac1929&sig=P2iNZJAvAWpp%2Bj9yV6TQjoz5DIIaj7ve8ARynmEM6Xk%3D&se=2015-02-14T01:13:05Z

    https://storagetestaccount001.blob.core.windows.net/asset-38058602-a4b8-4b33-b9f0-6880dc1490ea/BigBuckBunny_H264_3400kbps_AAC_und_ch2_96kbps.mp4?sv=2012-02-12&sr=c&si=166d5154-b801-410b-a226-ee2f8eac1929&sig=P2iNZJAvAWpp%2Bj9yV6TQjoz5DIIaj7ve8ARynmEM6Xk%3D&se=2015-02-14T01:13:05Z

    https://storagetestaccount001.blob.core.windows.net/asset-38058602-a4b8-4b33-b9f0-6880dc1490ea/BigBuckBunny_H264_2250kbps_AAC_und_ch2_96kbps.mp4?sv=2012-02-12&sr=c&si=166d5154-b801-410b-a226-ee2f8eac1929&sig=P2iNZJAvAWpp%2Bj9yV6TQjoz5DIIaj7ve8ARynmEM6Xk%3D&se=2015-02-14T01:13:05Z

    https://storagetestaccount001.blob.core.windows.net/asset-38058602-a4b8-4b33-b9f0-6880dc1490ea/BigBuckBunny_H264_1500kbps_AAC_und_ch2_96kbps.mp4?sv=2012-02-12&sr=c&si=166d5154-b801-410b-a226-ee2f8eac1929&sig=P2iNZJAvAWpp%2Bj9yV6TQjoz5DIIaj7ve8ARynmEM6Xk%3D&se=2015-02-14T01:13:05Z

    https://storagetestaccount001.blob.core.windows.net/asset-38058602-a4b8-4b33-b9f0-6880dc1490ea/BigBuckBunny_H264_1000kbps_AAC_und_ch2_96kbps.mp4?sv=2012-02-12&sr=c&si=166d5154-b801-410b-a226-ee2f8eac1929&sig=P2iNZJAvAWpp%2Bj9yV6TQjoz5DIIaj7ve8ARynmEM6Xk%3D&se=2015-02-14T01:13:05Z

    https://storagetestaccount001.blob.core.windows.net/asset-38058602-a4b8-4b33-b9f0-6880dc1490ea/BigBuckBunny_AAC_und_ch2_96kbps.mp4?sv=2012-02-12&sr=c&si=166d5154-b801-410b-a226-ee2f8eac1929&sig=P2iNZJAvAWpp%2Bj9yV6TQjoz5DIIaj7ve8ARynmEM6Xk%3D&se=2015-02-14T01:13:05Z

    https://storagetestaccount001.blob.core.windows.net/asset-38058602-a4b8-4b33-b9f0-6880dc1490ea/BigBuckBunny_AAC_und_ch2_56kbps.mp4?sv=2012-02-12&sr=c&si=166d5154-b801-410b-a226-ee2f8eac1929&sig=P2iNZJAvAWpp%2Bj9yV6TQjoz5DIIaj7ve8ARynmEM6Xk%3D&se=2015-02-14T01:13:05Z


### <a name="creating-a-streaming-url-for-streaming-content"></a><span data-ttu-id="efd3b-345">Tworzenie adresu URL przesyłania strumieniowego przesyłania strumieniowego zawartości</span><span class="sxs-lookup"><span data-stu-id="efd3b-345">Creating a streaming URL for streaming content</span></span>
<span data-ttu-id="efd3b-346">Witaj następującego kodu pokazuje sposób toocreate Lokalizator przesyłania strumieniowego adresu URL:</span><span class="sxs-lookup"><span data-stu-id="efd3b-346">hello following code shows how toocreate a streaming URL Locator:</span></span>

    POST https://wamsbayclus001rest-hs/API/Locators HTTP/1.1
    Content-Type: application/json
    Accept: application/json
    DataServiceVersion: 3.0
    MaxDataServiceVersion: 3.0
    x-ms-version: 2.11
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=youraccountname&urn%3aSubscriptionId=2f84471d-b1ae-4e75-aa09-010f0fc0cf5b&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1337067658&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=dithjGvlXR9HlyAf5DE99N5OCYkPAxsHIcsTSjm9%2fVE%3d
    Host: wamsbayclus001rest-hs
    Content-Length: 182
    Expect: 100-continue

    {"AccessPolicyId": "nb:pid:UUID:38c71dd0-44c5-4c5f-8418-08bb6fbf7bf8", "AssetId" : "nb:cid:UUID:eb5540a2-116e-4d36-b084-7e9958f7f3c3", "StartTime" : "2014-05-17T16:45:53",, "Type":2}

<span data-ttu-id="efd3b-347">W przypadku powodzenia powitania po odpowiedzi jest zwracany:</span><span class="sxs-lookup"><span data-stu-id="efd3b-347">If successful, hello following response is returned:</span></span>

    HTTP/1.1 201 Created
    Cache-Control: no-cache
    Content-Length: 981
    Content-Type: application/json;odata=verbose;charset=utf-8
    Location: https://wamsbayclus001rest-hs.net/api/Locators('nb%3Alid%3AUUID%3A52034bf6-dfae-4d83-aad3-3bd87dcb1a5d')
    Server: Microsoft-IIS/7.5
    x-ms-request-id: 2eac4158-fc78-4fa2-81ee-c9f582dc385f
    X-Content-Type-Options: nosniff
    DataServiceVersion: 1.0;
    X-AspNet-Version: 4.0.30319
    X-Powered-By: ASP.NET
    Date: Mon, 14 May 2012 21:41:39 GMT

    {  
       "d":{  
          "__metadata":{  
             "id":"https://wamsbayclus001rest-hs.net/api/Locators('nb%3Alid%3AUUID%3A52034bf6-dfae-4d83-aad3-3bd87dcb1a5d')",
             "uri":"https://wamsbayclus001rest-hs.net/api/Locators('nb%3Alid%3AUUID%3A52034bf6-dfae-4d83-aad3-3bd87dcb1a5d')",
             "type":"Microsoft.Cloud.Media.Vod.Rest.Data.Models.Locator"
          },
          "AccessPolicy":{  
             "__deferred":{  
                "uri":"https://wamsbayclus001rest-hs.net/api/Locators('nb%3Alid%3AUUID%3A52034bf6-dfae-4d83-aad3-3bd87dcb1a5d')/AccessPolicy"
             }
          },
          "Asset":{  
             "__deferred":{  
                "uri":"https://wamsbayclus001rest-hs.net/api/Locators('nb%3Alid%3AUUID%3A52034bf6-dfae-4d83-aad3-3bd87dcb1a5d')/Asset"
             }
          },
          "Id":"nb:lid:UUID:52034bf6-dfae-4d83-aad3-3bd87dcb1a5d",
          "ExpirationDateTime":"\/Date(1337049395000)\/",
          "Type":2,
          "Path":"http://wamsbayclus001rest-hs.net/52034bf6-dfae-4d83-aad3-3bd87dcb1a5d/",
          "AccessPolicyId":"nb:pid:UUID:38c71dd0-44c5-4c5f-8418-08bb6fbf7bf8",
          "AssetId":"nb:cid:UUID:eb5540a2-116e-4d36-b084-7e9958f7f3c3",
          "StartTime":"\/Date(1337031395000)\/"
       }
    }

<span data-ttu-id="efd3b-348">toostream adres URL źródła Smooth Streaming w odtwarzaczu multimedialnym przesyłania strumieniowego, można dołączyć hello ścieżki właściwości o nazwie hello hello Smooth Streaming pliku, a następnie manifestu "/ manifest".</span><span class="sxs-lookup"><span data-stu-id="efd3b-348">toostream a Smooth Streaming origin URL in a streaming media player, you must append hello Path property with hello name of hello Smooth Streaming manifest file, followed by "/manifest".</span></span>

    http://amstestaccount001.streaming.mediaservices.windows.net/ebf733c4-3e2e-4a68-b67b-cc5159d1d7f2/BigBuckBunny.ism/manifest

<span data-ttu-id="efd3b-349">toostream HLS, Dołącz (format = m3u8-aapl) po hello "/ manifest".</span><span class="sxs-lookup"><span data-stu-id="efd3b-349">toostream HLS, append (format=m3u8-aapl) after hello "/manifest".</span></span>

    http://amstestaccount001.streaming.mediaservices.windows.net/ebf733c4-3e2e-4a68-b67b-cc5159d1d7f2/BigBuckBunny.ism/manifest(format=m3u8-aapl)

<span data-ttu-id="efd3b-350">toostream MPEG DASH, Dołącz (format = mpd-time-csf) po hello "/ manifest".</span><span class="sxs-lookup"><span data-stu-id="efd3b-350">toostream MPEG DASH, append (format=mpd-time-csf) after hello "/manifest".</span></span>

    http://amstestaccount001.streaming.mediaservices.windows.net/ebf733c4-3e2e-4a68-b67b-cc5159d1d7f2/BigBuckBunny.ism/manifest(format=mpd-time-csf)


## <span data-ttu-id="efd3b-351"><a id="play"></a>Odtwarzanie zawartości</span><span class="sxs-lookup"><span data-stu-id="efd3b-351"><a id="play"></a>Play your content</span></span>
<span data-ttu-id="efd3b-352">toostream wideo, możesz użyć [Azure Media Services Player](http://amsplayer.azurewebsites.net/azuremediaplayer.html).</span><span class="sxs-lookup"><span data-stu-id="efd3b-352">toostream you video, use [Azure Media Services Player](http://amsplayer.azurewebsites.net/azuremediaplayer.html).</span></span>

<span data-ttu-id="efd3b-353">tootest progresywnego pobierania, wklej adres URL do przeglądarki (na przykład programu Internet Explorer, Chrome, Safari).</span><span class="sxs-lookup"><span data-stu-id="efd3b-353">tootest progressive download, paste a URL into a browser (for example, IE, Chrome, Safari).</span></span>

## <a name="next-steps-media-services-learning-paths"></a><span data-ttu-id="efd3b-354">Następne kroki: ścieżki szkoleniowe dotyczące usługi Media Services</span><span class="sxs-lookup"><span data-stu-id="efd3b-354">Next Steps: Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="efd3b-355">Przekazywanie opinii</span><span class="sxs-lookup"><span data-stu-id="efd3b-355">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]
