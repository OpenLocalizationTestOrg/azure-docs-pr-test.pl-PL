---
title: "Wprowadzenie do dostarczania zawartości na żądanie przy użyciu REST | Dokumentacja firmy Microsoft"
description: "Ten samouczek przedstawia kroki wdrażania aplikacji dostarczania zawartości na żądanie przy użyciu interfejsu API REST usługi Azure Media Services."
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
ms.openlocfilehash: f304f7671465862123f64c8b0f9af95a7c828cc2
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
# <a name="get-started-with-delivering-content-on-demand-using-rest"></a><span data-ttu-id="68447-103">Wprowadzenie do dostarczania zawartości na żądanie za pomocą usługi REST</span><span class="sxs-lookup"><span data-stu-id="68447-103">Get started with delivering content on demand using REST</span></span>
[!INCLUDE [media-services-selector-get-started](../../includes/media-services-selector-get-started.md)]

<span data-ttu-id="68447-104">Ta opcja szybkiego startu przeprowadzi Cię przez kroki wdrażania aplikacji do dostarczania zawartości wideo na żądanie (VoD) przy użyciu interfejsów API REST usługi Azure Media Services (AMS).</span><span class="sxs-lookup"><span data-stu-id="68447-104">This quickstart walks you through the steps of implementing a Video-on-Demand (VoD) content delivery application using Azure Media Services (AMS) REST APIs.</span></span>

<span data-ttu-id="68447-105">Samouczek przedstawia podstawowy przepływ pracy usług Media Services oraz najczęściej występujące obiekty i zadania programowania wymagane w celu projektowania usług Media Services.</span><span class="sxs-lookup"><span data-stu-id="68447-105">The tutorial introduces the basic Media Services workflow and the most common programming objects and tasks required for Media Services development.</span></span> <span data-ttu-id="68447-106">Po zakończeniu samouczka będziesz umieć przesłać strumieniowo lub pobrać progresywnie przykładowy plik multimedialny, który został wcześniej przekazany, zakodowany oraz pobrany.</span><span class="sxs-lookup"><span data-stu-id="68447-106">At the completion of the tutorial, you will be able to stream or progressively download a sample media file that you uploaded, encoded, and downloaded.</span></span>

<span data-ttu-id="68447-107">Na poniższym obrazie przedstawiono niektóre z najczęściej używanych obiektów podczas tworzenia aplikacji VoD w modelu Media Services OData.</span><span class="sxs-lookup"><span data-stu-id="68447-107">The following image shows some of the most commonly used objects when developing VoD applications against the Media Services OData model.</span></span>

<span data-ttu-id="68447-108">Kliknij obraz, aby go wyświetlić w pełnym rozmiarze.</span><span class="sxs-lookup"><span data-stu-id="68447-108">Click the image to view it full size.</span></span>  

<a href="./media/media-services-rest-get-started/media-services-overview-object-model.png" target="_blank"><img src="./media/media-services-rest-get-started/media-services-overview-object-model-small.png"></a> 

## <a name="prerequisites"></a><span data-ttu-id="68447-109">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="68447-109">Prerequisites</span></span>
<span data-ttu-id="68447-110">Następujące wymagania wstępne są wymagane do uruchomienia, programowania z użyciem usługi Media Services z interfejsów API REST.</span><span class="sxs-lookup"><span data-stu-id="68447-110">The following prerequisites are required to start developing with Media Services with REST APIs.</span></span>

* <span data-ttu-id="68447-111">Konto platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="68447-111">An Azure account.</span></span> <span data-ttu-id="68447-112">Aby uzyskać szczegółowe informacje, zobacz artykuł [Bezpłatna wersja próbna platformy Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="68447-112">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="68447-113">Konto usługi Media Services.</span><span class="sxs-lookup"><span data-stu-id="68447-113">A Media Services account.</span></span> <span data-ttu-id="68447-114">Aby utworzyć konto usługi Media Services, zobacz temat [Jak utworzyć konto usługi Media Services](media-services-portal-create-account.md).</span><span class="sxs-lookup"><span data-stu-id="68447-114">To create a Media Services account, see [How to Create a Media Services Account](media-services-portal-create-account.md).</span></span>
* <span data-ttu-id="68447-115">Opis sposobu tworzenia z interfejsu API REST usługi multimediów.</span><span class="sxs-lookup"><span data-stu-id="68447-115">Understanding of how to develop with Media Services REST API.</span></span> <span data-ttu-id="68447-116">Aby uzyskać więcej informacji, zobacz [omówienie interfejsu API REST usług Media](media-services-rest-how-to-use.md).</span><span class="sxs-lookup"><span data-stu-id="68447-116">For more information, see [Media Services REST API overview](media-services-rest-how-to-use.md).</span></span>
* <span data-ttu-id="68447-117">Aplikacja, który może wysyłać żądań i odpowiedzi HTTP.</span><span class="sxs-lookup"><span data-stu-id="68447-117">An application of your choice that can send HTTP requests and responses.</span></span> <span data-ttu-id="68447-118">W tym samouczku używana [Fiddler](http://www.telerik.com/download/fiddler).</span><span class="sxs-lookup"><span data-stu-id="68447-118">This tutorial uses [Fiddler](http://www.telerik.com/download/fiddler).</span></span>

<span data-ttu-id="68447-119">Następujące zadania są wyświetlane w tym Szybki Start.</span><span class="sxs-lookup"><span data-stu-id="68447-119">The following tasks are shown in this quickstart.</span></span>

1. <span data-ttu-id="68447-120">Uruchamianie punktów końcowych przesyłania strumieniowego (przy użyciu witryny Azure Portal).</span><span class="sxs-lookup"><span data-stu-id="68447-120">Start streaming endpoint (using the Azure portal).</span></span>
2. <span data-ttu-id="68447-121">Podłącz do konta usługi Media Services z interfejsu API REST.</span><span class="sxs-lookup"><span data-stu-id="68447-121">Connect to the Media Services account with REST API.</span></span>
3. <span data-ttu-id="68447-122">Tworzenie nowego elementu zawartości i przekazywanie pliku wideo z interfejsu API REST.</span><span class="sxs-lookup"><span data-stu-id="68447-122">Create a new asset and upload a video file with REST API.</span></span>
4. <span data-ttu-id="68447-123">Kodowanie pliku źródłowego do zestawu plików MP4 o adaptacyjnej szybkości bitowej z interfejsu API REST.</span><span class="sxs-lookup"><span data-stu-id="68447-123">Encode the source file into a set of adaptive bitrate MP4 files with REST API.</span></span>
5. <span data-ttu-id="68447-124">Publikowanie elementu zawartości i get przesyłania strumieniowego i pobierania progresywnego adresy URL z interfejsu API REST.</span><span class="sxs-lookup"><span data-stu-id="68447-124">Publish the asset and get streaming and progressive download URLs with REST API.</span></span>
6. <span data-ttu-id="68447-125">Odtwarzanie zawartości.</span><span class="sxs-lookup"><span data-stu-id="68447-125">Play your content.</span></span>

>[!NOTE]
><span data-ttu-id="68447-126">Limit różnych zasad usługi AMS wynosi 1 000 000 (na przykład zasad lokalizatorów lub ContentKeyAuthorizationPolicy).</span><span class="sxs-lookup"><span data-stu-id="68447-126">There is a limit of 1,000,000 policies for different AMS policies (for example, for Locator policy or ContentKeyAuthorizationPolicy).</span></span> <span data-ttu-id="68447-127">Należy używać tego samego identyfikatora zasad, jeśli zawsze są używane uprawnienia dotyczące tych samych dni lub tego samego dostępu, na przykład dla lokalizatorów przeznaczonych do długotrwałego stosowania (nieprzekazywanych zasad).</span><span class="sxs-lookup"><span data-stu-id="68447-127">You should use the same policy ID if you are always using the same days / access permissions, for example, policies for locators that are intended to remain in place for a long time (non-upload policies).</span></span> <span data-ttu-id="68447-128">Aby uzyskać więcej informacji, zobacz [ten](media-services-dotnet-manage-entities.md#limit-access-policies) temat.</span><span class="sxs-lookup"><span data-stu-id="68447-128">For more information, see [this](media-services-dotnet-manage-entities.md#limit-access-policies) topic.</span></span>

<span data-ttu-id="68447-129">Aby uzyskać szczegółowe informacje na temat jednostek AMS REST używaną w tym temacie, zobacz [dokumentacja interfejsu API REST usługi Azure Media Services](/rest/api/media/services/azure-media-services-rest-api-reference).</span><span class="sxs-lookup"><span data-stu-id="68447-129">For details about AMS REST entities used in this topic, see [Azure Media Services REST API Reference](/rest/api/media/services/azure-media-services-rest-api-reference).</span></span> <span data-ttu-id="68447-130">Zobacz też [pojęcia dotyczące usługi Azure Media Services](media-services-concepts.md).</span><span class="sxs-lookup"><span data-stu-id="68447-130">Also, see [Azure Media Services concepts](media-services-concepts.md).</span></span>

>[!NOTE]
><span data-ttu-id="68447-131">Podczas uzyskiwania dostępu do obiektów w usłudze Media Services, należy ustawić określonych pól nagłówka i wartości w Twoich żądań HTTP.</span><span class="sxs-lookup"><span data-stu-id="68447-131">When accessing entities in Media Services, you must set specific header fields and values in your HTTP requests.</span></span> <span data-ttu-id="68447-132">Aby uzyskać więcej informacji, zobacz [ustawień dla rozwoju interfejsu API REST usługi Media](media-services-rest-how-to-use.md).</span><span class="sxs-lookup"><span data-stu-id="68447-132">For more information, see [Setup for Media Services REST API Development](media-services-rest-how-to-use.md).</span></span>

## <a name="start-streaming-endpoints-using-the-azure-portal"></a><span data-ttu-id="68447-133">Uruchamianie punktów końcowych przesyłania strumieniowego przy użyciu witryny Azure Portal</span><span class="sxs-lookup"><span data-stu-id="68447-133">Start streaming endpoints using the Azure portal</span></span>

<span data-ttu-id="68447-134">Podczas pracy w usłudze Azure Media Services jednym z najbardziej typowych scenariuszy jest dostarczanie obrazu wideo za pośrednictwem przesyłania strumieniowego z adaptacyjną szybkością transmisji bitów.</span><span class="sxs-lookup"><span data-stu-id="68447-134">When working with Azure Media Services one of the most common scenarios is delivering video via adaptive bitrate streaming.</span></span> <span data-ttu-id="68447-135">Usługa Media Services udostępnia funkcję dynamicznego tworzenia pakietów, która pozwala dostarczać kodowaną zawartość plików MP4 z adaptacyjną szybkością transmisji bitów w formatach przesyłania strumieniowego obsługiwanych przez usługę Media Services (MPEG DASH, HLS, Smooth Streaming) w odpowiednim czasie bez konieczności przechowywania wersji wstępnie utworzonych pakietów poszczególnych formatów przesyłania strumieniowego.</span><span class="sxs-lookup"><span data-stu-id="68447-135">Media Services provides dynamic packaging, which allows you to deliver your adaptive bitrate MP4 encoded content in streaming formats supported by Media Services (MPEG DASH, HLS, Smooth Streaming) just-in-time, without you having to store pre-packaged versions of each of these streaming formats.</span></span>

>[!NOTE]
><span data-ttu-id="68447-136">Po utworzeniu konta usługi AMS zostanie do niego dodany **domyślny** punkt końcowy przesyłania strumieniowego mający stan **Zatrzymany**.</span><span class="sxs-lookup"><span data-stu-id="68447-136">When your AMS account is created a **default** streaming endpoint is added to your account in the **Stopped** state.</span></span> <span data-ttu-id="68447-137">Aby rozpocząć przesyłanie strumieniowe zawartości oraz korzystać z dynamicznego tworzenia pakietów i szyfrowania dynamicznego, punkt końcowy przesyłania strumieniowego, z którego chcesz strumieniowo przesyłać zawartość, musi mieć stan **Uruchomiony**.</span><span class="sxs-lookup"><span data-stu-id="68447-137">To start streaming your content and take advantage of dynamic packaging and dynamic encryption, the streaming endpoint from which you want to stream content has to be in the **Running** state.</span></span>

<span data-ttu-id="68447-138">Aby uruchomić punkt końcowy przesyłania strumieniowego, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="68447-138">To start the streaming endpoint, do the following:</span></span>

1. <span data-ttu-id="68447-139">Zaloguj się w [portalu Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="68447-139">Log in at the [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="68447-140">W oknie Ustawienia kliknij pozycję Punkty końcowe przesyłania strumieniowego.</span><span class="sxs-lookup"><span data-stu-id="68447-140">In the Settings window, click Streaming endpoints.</span></span>
3. <span data-ttu-id="68447-141">Kliknij domyślny punkt końcowy przesyłania strumieniowego.</span><span class="sxs-lookup"><span data-stu-id="68447-141">Click the default streaming endpoint.</span></span>

    <span data-ttu-id="68447-142">Zostanie wyświetlone okno SZCZEGÓŁY DOMYŚLNEGO PUNKTU KOŃCOWEGO PRZESYŁANIA STRUMIENIOWEGO.</span><span class="sxs-lookup"><span data-stu-id="68447-142">The DEFAULT STREAMING ENDPOINT DETAILS window appears.</span></span>

4. <span data-ttu-id="68447-143">Kliknij ikonę Uruchom.</span><span class="sxs-lookup"><span data-stu-id="68447-143">Click the Start icon.</span></span>
5. <span data-ttu-id="68447-144">Kliknij przycisk Zapisz, aby zapisać zmiany.</span><span class="sxs-lookup"><span data-stu-id="68447-144">Click the Save button to save your changes.</span></span>

## <span data-ttu-id="68447-145"><a id="connect"></a>Połącz się kontem usługi Media Services z interfejsu API REST</span><span class="sxs-lookup"><span data-stu-id="68447-145"><a id="connect"></a>Connect to the Media Services account with REST API</span></span>

<span data-ttu-id="68447-146">Aby uzyskać informacje na temat nawiązywania połączenia z interfejsu API usług AMS, zobacz [dostępu Azure Media Services API przy użyciu uwierzytelniania usługi Azure AD](media-services-use-aad-auth-to-access-ams-api.md).</span><span class="sxs-lookup"><span data-stu-id="68447-146">For information on how to connect to the AMS API, see [Access the Azure Media Services API with Azure AD authentication](media-services-use-aad-auth-to-access-ams-api.md).</span></span> 

>[!NOTE]
><span data-ttu-id="68447-147">Po pomyślnym połączeniu się https://media.windows.net, otrzymasz 301 przekierowanie, określając inny identyfikator URI usługi multimediów.</span><span class="sxs-lookup"><span data-stu-id="68447-147">After successfully connecting to https://media.windows.net, you will receive a 301 redirect specifying another Media Services URI.</span></span> <span data-ttu-id="68447-148">Upewnij się kolejne wywołania nowy identyfikator URI.</span><span class="sxs-lookup"><span data-stu-id="68447-148">You must make subsequent calls to the new URI.</span></span>

<span data-ttu-id="68447-149">Na przykład jeśli po próby nawiązania połączenia, masz następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="68447-149">For example, if after trying to connect, you got the following:</span></span>

    HTTP/1.1 301 Moved Permanently
    Location: https://wamsbayclus001rest-hs.cloudapp.net/api/

<span data-ttu-id="68447-150">Należy zadać kolejnych wywołań interfejsu API https://wamsbayclus001rest-hs.cloudapp.net/api/.</span><span class="sxs-lookup"><span data-stu-id="68447-150">You should post your subsequent API calls to https://wamsbayclus001rest-hs.cloudapp.net/api/.</span></span>

## <span data-ttu-id="68447-151"><a id="upload"></a>Tworzenie nowego elementu zawartości i przekazywanie pliku wideo z interfejsu API REST</span><span class="sxs-lookup"><span data-stu-id="68447-151"><a id="upload"></a>Create a new asset and upload a video file with REST API</span></span>

<span data-ttu-id="68447-152">Za pomocą usługi Media Services można przekazać pliki cyfrowe do elementu zawartości.</span><span class="sxs-lookup"><span data-stu-id="68447-152">In Media Services, you upload your digital files into an asset.</span></span> <span data-ttu-id="68447-153">**Zasobów** może zawierać wideo, audio, obrazy, kolekcje miniatur, tekst ścieżek i napisów plików (oraz metadane dotyczące tych plików.)  Po przekazaniu plików do zawartości, zawartość jest bezpiecznie przechowywana w chmurze na potrzeby dalszego przetwarzania i przesyłania strumieniowego.</span><span class="sxs-lookup"><span data-stu-id="68447-153">The **Asset** entity can contain video, audio, images, thumbnail collections, text tracks and closed caption files (and the metadata about these files.)  Once the files are uploaded into the asset, your content is stored securely in the cloud for further processing and streaming.</span></span>

<span data-ttu-id="68447-154">Jedna z wartości, które należy podać podczas tworzenia zasobu jest opcji tworzenia elementów zawartości.</span><span class="sxs-lookup"><span data-stu-id="68447-154">One of the values that you have to provide when creating an asset is asset creation options.</span></span> <span data-ttu-id="68447-155">**Opcje** właściwość jest wartością wyliczenia, które opisano dostępne opcje szyfrowania, które można utworzyć zasobu z.</span><span class="sxs-lookup"><span data-stu-id="68447-155">The **Options** property is an enumeration value that describes the encryption options that an Asset can be created with.</span></span> <span data-ttu-id="68447-156">Nieprawidłowa wartość jest jedną z wartości z listy poniżej, a nie kombinację wartości z tej listy:</span><span class="sxs-lookup"><span data-stu-id="68447-156">A valid value is one of the values from the list below, not a combination of values from this list:</span></span>

* <span data-ttu-id="68447-157">**Brak** = **0** — szyfrowanie nie jest stosowane.</span><span class="sxs-lookup"><span data-stu-id="68447-157">**None** = **0** - No encryption is used.</span></span> <span data-ttu-id="68447-158">Korzystając z tej opcji zawartość nie jest chroniona w trakcie przesyłania lub przechowywania w magazynie.</span><span class="sxs-lookup"><span data-stu-id="68447-158">When using this option your content is not protected in transit or at rest in storage.</span></span>
    <span data-ttu-id="68447-159">Jeśli planujesz dostarczać zawartość w formacie MP4 przy użyciu pobierania progresywnego, użyj tej opcji.</span><span class="sxs-lookup"><span data-stu-id="68447-159">If you plan to deliver an MP4 using progressive download, use this option.</span></span>
* <span data-ttu-id="68447-160">**StorageEncrypted** = **1** — zawartości lokalnie, przy użyciu standardu AES 256-bitowego szyfruje i przekazuje go do magazynu Azure gdzie jest przechowywana szyfrowane, gdy.</span><span class="sxs-lookup"><span data-stu-id="68447-160">**StorageEncrypted** = **1** - Encrypts your clear content locally using AES-256 bit encryption and then uploads it to Azure Storage where it is stored encrypted at rest.</span></span> <span data-ttu-id="68447-161">Elementy zawartości chronione przy użyciu szyfrowania magazynu są automatycznie odszyfrowywane i umieszczane w systemie szyfrowania plików przed kodowaniem, a także opcjonalnie ponownie szyfrowane przed przesłaniem zwrotnym w formie nowego elementu zawartości wyjściowej.</span><span class="sxs-lookup"><span data-stu-id="68447-161">Assets protected with Storage Encryption are automatically unencrypted and placed in an encrypted file system prior to encoding, and optionally re-encrypted prior to uploading back as a new output asset.</span></span> <span data-ttu-id="68447-162">Pierwotnym zastosowaniem szyfrowania magazynu jest zabezpieczenie za pomocą silnego szyfrowania wysokiej jakości multimedialnych plików wejściowych przechowywanych na dysku.</span><span class="sxs-lookup"><span data-stu-id="68447-162">The primary use case for Storage Encryption is when you want to secure your high-quality input media files with strong encryption at rest on disk.</span></span>
* <span data-ttu-id="68447-163">**CommonEncryptionProtected** = **2** — ta opcja umożliwia przekazanie zawartości, który został już szyfrowane i chronione za pomocą wspólnego szyfrowania lub technologii PlayReady DRM (na przykład, Smooth Streaming chronione przy użyciu technologii PlayReady DRM).</span><span class="sxs-lookup"><span data-stu-id="68447-163">**CommonEncryptionProtected** = **2** - Use this option if you are uploading content that has already been encrypted and protected with Common Encryption or PlayReady DRM (for example, Smooth Streaming protected with PlayReady DRM).</span></span>
* <span data-ttu-id="68447-164">**EnvelopeEncryptionProtected** = **4** — Użyj tej opcji, Jeśli przesyłasz HLS zaszyfrowanych z użyciem standardu AES.</span><span class="sxs-lookup"><span data-stu-id="68447-164">**EnvelopeEncryptionProtected** = **4** – Use this option if you are uploading HLS encrypted with AES.</span></span> <span data-ttu-id="68447-165">Należy zakodowane pliki i szyfrowane przez Transform Manager.</span><span class="sxs-lookup"><span data-stu-id="68447-165">The files must have been encoded and encrypted by Transform Manager.</span></span>

### <a name="create-an-asset"></a><span data-ttu-id="68447-166">Utwórz zasób</span><span class="sxs-lookup"><span data-stu-id="68447-166">Create an asset</span></span>
<span data-ttu-id="68447-167">Zasób jest kontenerem dla wielu typów lub zestawów obiektów w usłudze Media Services: wideo, audio, obrazy, kolekcje miniatur, ścieżek tekstu i pliki napisów.</span><span class="sxs-lookup"><span data-stu-id="68447-167">An asset is a container for multiple types or sets of objects in Media Services, including video, audio, images, thumbnail collections, text tracks, and closed caption files.</span></span> <span data-ttu-id="68447-168">W interfejsie API REST tworzenie zasobu wymaga wysłanie żądania POST do usługi Media Services i umieszczenie wszelkie informacje o zawartości w treści żądania.</span><span class="sxs-lookup"><span data-stu-id="68447-168">In the REST API, creating an Asset requires sending POST request to Media Services and placing any property information about your asset in the request body.</span></span>

<span data-ttu-id="68447-169">Poniższy przykład pokazuje, jak utworzyć element zawartości.</span><span class="sxs-lookup"><span data-stu-id="68447-169">The following example shows how to create an asset.</span></span>

<span data-ttu-id="68447-170">**Żądania HTTP**</span><span class="sxs-lookup"><span data-stu-id="68447-170">**HTTP Request**</span></span>

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


<span data-ttu-id="68447-171">**Odpowiedź HTTP**</span><span class="sxs-lookup"><span data-stu-id="68447-171">**HTTP Response**</span></span>

<span data-ttu-id="68447-172">Jeśli to się powiedzie, jest zwracany następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="68447-172">If successful, the following is returned:</span></span>

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

### <a name="create-an-assetfile"></a><span data-ttu-id="68447-173">Utwórz AssetFile</span><span class="sxs-lookup"><span data-stu-id="68447-173">Create an AssetFile</span></span>
<span data-ttu-id="68447-174">[AssetFile](https://docs.microsoft.com/rest/api/media/operations/assetfile) jednostki reprezentuje plik wideo lub audio, który jest przechowywany w kontenerze obiektów blob.</span><span class="sxs-lookup"><span data-stu-id="68447-174">The [AssetFile](https://docs.microsoft.com/rest/api/media/operations/assetfile) entity represents a video or audio file that is stored in a blob container.</span></span> <span data-ttu-id="68447-175">Plik zasobów zawsze jest skojarzony z zasobem i zasobów może zawierać jeden lub wiele AssetFiles.</span><span class="sxs-lookup"><span data-stu-id="68447-175">An asset file is always associated with an asset, and an asset may contain one or many AssetFiles.</span></span> <span data-ttu-id="68447-176">Zadanie Media Encoder usługi nie powiedzie się, jeśli obiekt pliku zasobu nie jest skojarzony z pliku cyfrowego w kontenerze obiektów blob.</span><span class="sxs-lookup"><span data-stu-id="68447-176">The Media Services Encoder task fails if an asset file object is not associated with a digital file in a blob container.</span></span>

<span data-ttu-id="68447-177">Po przekazaniu pliku nośnika cyfrowego do kontenera obiektów blob, użyj **scalania** żądania HTTP, aby zaktualizować informacje o pliku nośnika AssetFile (jak pokazano w dalszej części tematu).</span><span class="sxs-lookup"><span data-stu-id="68447-177">After you upload your digital media file into a blob container, you use the **MERGE** HTTP request to update the AssetFile with information about your media file (as shown later in the topic).</span></span>

<span data-ttu-id="68447-178">**Żądania HTTP**</span><span class="sxs-lookup"><span data-stu-id="68447-178">**HTTP Request**</span></span>

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


<span data-ttu-id="68447-179">**Odpowiedź HTTP**</span><span class="sxs-lookup"><span data-stu-id="68447-179">**HTTP Response**</span></span>

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


### <a name="creating-the-accesspolicy-with-write-permission"></a><span data-ttu-id="68447-180">Tworzenie AccessPolicy z uprawnieniami do zapisu</span><span class="sxs-lookup"><span data-stu-id="68447-180">Creating the AccessPolicy with write permission</span></span>
<span data-ttu-id="68447-181">Przed przekazaniem żadnych plików do magazynu obiektów blob, należy ustawić dostęp zasad prawa do zapisu do elementu zawartości.</span><span class="sxs-lookup"><span data-stu-id="68447-181">Before uploading any files into blob storage, set the access policy rights for writing to an asset.</span></span> <span data-ttu-id="68447-182">W tym celu po żądania HTTP AccessPolicies zestawem jednostek.</span><span class="sxs-lookup"><span data-stu-id="68447-182">To do that, POST an HTTP request to the AccessPolicies entity set.</span></span> <span data-ttu-id="68447-183">Zdefiniuj wartość DurationInMinutes po utworzeniu lub pojawi się komunikat o błędzie 500 wewnętrzny serwer w odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="68447-183">Define a DurationInMinutes value upon creation or you receive a 500 Internal Server error message back in response.</span></span> <span data-ttu-id="68447-184">Aby uzyskać więcej informacji o AccessPolicies, zobacz [AccessPolicy](https://docs.microsoft.com/rest/api/media/operations/accesspolicy).</span><span class="sxs-lookup"><span data-stu-id="68447-184">For more information on AccessPolicies, see [AccessPolicy](https://docs.microsoft.com/rest/api/media/operations/accesspolicy).</span></span>

<span data-ttu-id="68447-185">Poniższy przykład przedstawia sposób tworzenia AccessPolicy:</span><span class="sxs-lookup"><span data-stu-id="68447-185">The following example shows how to create an AccessPolicy:</span></span>

<span data-ttu-id="68447-186">**Żądania HTTP**</span><span class="sxs-lookup"><span data-stu-id="68447-186">**HTTP Request**</span></span>

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

<span data-ttu-id="68447-187">**Odpowiedź HTTP**</span><span class="sxs-lookup"><span data-stu-id="68447-187">**HTTP Response**</span></span>

<span data-ttu-id="68447-188">W przypadku powodzenia następującą odpowiedź jest zwracana:</span><span class="sxs-lookup"><span data-stu-id="68447-188">If successful, the following response is returned:</span></span>

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

### <a name="get-the-upload-url"></a><span data-ttu-id="68447-189">Pobierz adres URL przesyłania</span><span class="sxs-lookup"><span data-stu-id="68447-189">Get the Upload URL</span></span>

<span data-ttu-id="68447-190">Aby uzyskać adres URL przesyłania rzeczywistej, tworzenie lokalizatora SAS.</span><span class="sxs-lookup"><span data-stu-id="68447-190">To receive the actual upload URL, create a SAS Locator.</span></span> <span data-ttu-id="68447-191">Lokalizatory zdefiniuj czas rozpoczęcia i typ punktu końcowego połączenia dla klientów, którzy mają dostęp do plików w zasób.</span><span class="sxs-lookup"><span data-stu-id="68447-191">Locators define the start time and type of connection endpoint for clients that want to access Files in an Asset.</span></span> <span data-ttu-id="68447-192">Możesz utworzyć wiele jednostek lokalizatora dla danego pary AccessPolicy i zasobów do obsługi żądań klientów różnych i potrzeb.</span><span class="sxs-lookup"><span data-stu-id="68447-192">You can create multiple Locator entities for a given AccessPolicy and Asset pair to handle different client requests and needs.</span></span> <span data-ttu-id="68447-193">Wartość StartTime oraz wartość DurationInMinutes AccessPolicy każdego z tych lokalizatorów używa do określenia czasu, można użyć adresu URL.</span><span class="sxs-lookup"><span data-stu-id="68447-193">Each of these Locators uses the StartTime value plus the DurationInMinutes value of the AccessPolicy to determine the length of time a URL can be used.</span></span> <span data-ttu-id="68447-194">Aby uzyskać więcej informacji, zobacz [lokalizatora](https://docs.microsoft.com/rest/api/media/operations/locator).</span><span class="sxs-lookup"><span data-stu-id="68447-194">For more information, see [Locator](https://docs.microsoft.com/rest/api/media/operations/locator).</span></span>

<span data-ttu-id="68447-195">Adres URL SAS ma następujący format:</span><span class="sxs-lookup"><span data-stu-id="68447-195">A SAS URL has the following format:</span></span>

    {https://myaccount.blob.core.windows.net}/{asset name}/{video file name}?{SAS signature}

<span data-ttu-id="68447-196">Zagadnienia do rozważenia:</span><span class="sxs-lookup"><span data-stu-id="68447-196">Some considerations apply:</span></span>

* <span data-ttu-id="68447-197">Nie może mieć więcej niż pięć lokalizatorów unikatowy skojarzone z danym zawartości w tym samym czasie.</span><span class="sxs-lookup"><span data-stu-id="68447-197">You cannot have more than five unique Locators associated with a given Asset at one time.</span></span> <span data-ttu-id="68447-198">Aby uzyskać więcej informacji zobacz lokalizatora.</span><span class="sxs-lookup"><span data-stu-id="68447-198">For more information, see Locator.</span></span>
* <span data-ttu-id="68447-199">Jeśli chcesz przekazać pliki natychmiast, należy ustawić wartość StartTime do pięciu minut przed bieżącym czasem.</span><span class="sxs-lookup"><span data-stu-id="68447-199">If you need to upload your files immediately, you should set your StartTime value to five minutes before the current time.</span></span> <span data-ttu-id="68447-200">Jest to spowodowane mogą istnieć zegara pochylenia między komputer klienta i usługi Media Services.</span><span class="sxs-lookup"><span data-stu-id="68447-200">This is because there may be clock skew between your client machine and Media Services.</span></span> <span data-ttu-id="68447-201">Ponadto wartość StartTime musi być w następującym formacie daty/godziny: RRRR-MM-ddtgg (na przykład "2014-05-23T17:53:50Z").</span><span class="sxs-lookup"><span data-stu-id="68447-201">Also, your StartTime value must be in the following DateTime format: YYYY-MM-DDTHH:mm:ssZ (for example, "2014-05-23T17:53:50Z").</span></span>    
* <span data-ttu-id="68447-202">Może być 30 40 sekund opóźnienia po utworzeniu lokalizatora, gdy jest ona dostępna do użycia.</span><span class="sxs-lookup"><span data-stu-id="68447-202">There may be a 30-40 second delay after a Locator is created to when it is available for use.</span></span> <span data-ttu-id="68447-203">Ten problem dotyczy zarówno adres URL SAS, jak i lokalizatorów pochodzenia.</span><span class="sxs-lookup"><span data-stu-id="68447-203">This issue applies to both SAS URL and Origin Locators.</span></span>

<span data-ttu-id="68447-204">Aby uzyskać więcej informacji na temat sygnatury dostępu Współdzielonego Zobacz lokalizatorów [to](http://southworks.com/blog/2015/05/27/reusing-azure-media-services-locators-to-avoid-facing-the-5-shared-access-policy-limitation/) blogu.</span><span class="sxs-lookup"><span data-stu-id="68447-204">For more information about SAS locators see [this](http://southworks.com/blog/2015/05/27/reusing-azure-media-services-locators-to-avoid-facing-the-5-shared-access-policy-limitation/) blog.</span></span>

<span data-ttu-id="68447-205">Poniższy przykład pokazuje, jak utworzyć Lokalizator adres URL SAS, zgodnie z definicją we właściwości typu w treści żądania ("1" dla lokalizatora SAS) i "2" dla lokalizatora pochodzenia na żądanie.</span><span class="sxs-lookup"><span data-stu-id="68447-205">The following example shows how to create a SAS URL Locator, as defined by the Type property in the request body ("1" for a SAS locator and "2" for an On-Demand origin locator).</span></span> <span data-ttu-id="68447-206">**Ścieżki** właściwości zwróconej zawiera adres URL, który należy użyć, aby przesłać plik.</span><span class="sxs-lookup"><span data-stu-id="68447-206">The **Path** property returned contains the URL that you must use to upload your file.</span></span>

<span data-ttu-id="68447-207">**Żądania HTTP**</span><span class="sxs-lookup"><span data-stu-id="68447-207">**HTTP Request**</span></span>

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


<span data-ttu-id="68447-208">**Odpowiedź HTTP**</span><span class="sxs-lookup"><span data-stu-id="68447-208">**HTTP Response**</span></span>

<span data-ttu-id="68447-209">W przypadku powodzenia następującą odpowiedź jest zwracana:</span><span class="sxs-lookup"><span data-stu-id="68447-209">If successful, the following response is returned:</span></span>

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

### <a name="upload-a-file-into-a-blob-storage-container"></a><span data-ttu-id="68447-210">Przekazywanie pliku do kontenera magazynu obiektów blob</span><span class="sxs-lookup"><span data-stu-id="68447-210">Upload a file into a blob storage container</span></span>
<span data-ttu-id="68447-211">Po utworzeniu AccessPolicy, a także ustawić rzeczywisty plik jest przekazywany do kontenera magazynu obiektów blob platformy Azure przy użyciu interfejsów API REST usługi Magazyn Azure.</span><span class="sxs-lookup"><span data-stu-id="68447-211">Once you have the AccessPolicy and Locator set, the actual file is uploaded to an Azure blob storage container using the Azure Storage REST APIs.</span></span> <span data-ttu-id="68447-212">Należy przekazać pliki jako blokowych obiektów blob.</span><span class="sxs-lookup"><span data-stu-id="68447-212">You must upload the files as block blobs.</span></span> <span data-ttu-id="68447-213">Stronicowe obiekty BLOB nie są obsługiwane przez usługi Azure Media Services.</span><span class="sxs-lookup"><span data-stu-id="68447-213">Page blobs are not supported by Azure Media Services.</span></span>  

> [!NOTE]
> <span data-ttu-id="68447-214">Należy dodać nazwę pliku dla pliku, który chcesz przekazać do Lokalizator **ścieżki** wartość odebrana w poprzedniej sekcji.</span><span class="sxs-lookup"><span data-stu-id="68447-214">You must add the file name for the file you want to upload to the Locator **Path** value received in the previous section.</span></span> <span data-ttu-id="68447-215">Na przykład https://storagetestaccount001.blob.core.windows.net/asset-e7b02da4-5a69-40e7-a8db-e8f4f697aac0/BigBuckBunny.mp4?</span><span class="sxs-lookup"><span data-stu-id="68447-215">For example, https://storagetestaccount001.blob.core.windows.net/asset-e7b02da4-5a69-40e7-a8db-e8f4f697aac0/BigBuckBunny.mp4?</span></span> <span data-ttu-id="68447-216">.</span><span class="sxs-lookup"><span data-stu-id="68447-216">.</span></span> <span data-ttu-id="68447-217">.</span><span class="sxs-lookup"><span data-stu-id="68447-217">.</span></span> <span data-ttu-id="68447-218">.</span><span class="sxs-lookup"><span data-stu-id="68447-218">.</span></span>
>
>

<span data-ttu-id="68447-219">Aby uzyskać więcej informacji na temat pracy z obiektami blob magazynu Azure, zobacz [interfejsu API REST usługi Blob](https://docs.microsoft.com/rest/api/storageservices/Blob-Service-REST-API).</span><span class="sxs-lookup"><span data-stu-id="68447-219">For more information on working with Azure storage blobs, see [Blob Service REST API](https://docs.microsoft.com/rest/api/storageservices/Blob-Service-REST-API).</span></span>

### <a name="update-the-assetfile"></a><span data-ttu-id="68447-220">Aktualizacja AssetFile</span><span class="sxs-lookup"><span data-stu-id="68447-220">Update the AssetFile</span></span>
<span data-ttu-id="68447-221">Teraz, przekazywanego pliku, zaktualizuj informacje FileAsset rozmiarze (i innych).</span><span class="sxs-lookup"><span data-stu-id="68447-221">Now that you've uploaded your file, update the FileAsset size (and other) information.</span></span> <span data-ttu-id="68447-222">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="68447-222">For example:</span></span>

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


<span data-ttu-id="68447-223">**Odpowiedź HTTP**</span><span class="sxs-lookup"><span data-stu-id="68447-223">**HTTP Response**</span></span>

<span data-ttu-id="68447-224">Jeśli to się powiedzie, jest zwracany następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="68447-224">If successful, the following is returned:</span></span>

    HTTP/1.1 204 No Content
    ...

## <a name="delete-the-locator-and-accesspolicy"></a><span data-ttu-id="68447-225">Usuń lokalizator i AccessPolicy</span><span class="sxs-lookup"><span data-stu-id="68447-225">Delete the Locator and AccessPolicy</span></span>
<span data-ttu-id="68447-226">**Żądania HTTP**</span><span class="sxs-lookup"><span data-stu-id="68447-226">**HTTP Request**</span></span>

    DELETE https://wamsbayclus001rest-hs.cloudapp.net/api/Locators('nb%3Alid%3AUUID%3Aaf57bdd8-6751-4e84-b403-f3c140444b54') HTTP/1.1
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amstestaccount001&urn%3aSubscriptionId=z7f09258-2233-4ca2-b1ae-193798e2c9d8&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1421662918&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=utmoXXbm9Q7j4tW1yJuMVA3egRiQy5FPygwadkmPeaY%3d
    x-ms-version: 2.11
    Host: wamsbayclus001rest-hs.cloudapp.net


<span data-ttu-id="68447-227">**Odpowiedź HTTP**</span><span class="sxs-lookup"><span data-stu-id="68447-227">**HTTP Response**</span></span>

<span data-ttu-id="68447-228">Jeśli to się powiedzie, jest zwracany następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="68447-228">If successful, the following is returned:</span></span>

    HTTP/1.1 204 No Content
    ...

<span data-ttu-id="68447-229">**Żądania HTTP**</span><span class="sxs-lookup"><span data-stu-id="68447-229">**HTTP Request**</span></span>

    DELETE https://wamsbayclus001rest-hs.cloudapp.net/api/AccessPolicies('nb%3Apid%3AUUID%3Abe0ac48d-af7d-4877-9d60-1805d68bffae') HTTP/1.1
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amstestaccount001&urn%3aSubscriptionId=z7f09258-2233-4ca2-b1ae-193798e2c9d8&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1421662918&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=utmoXXbm9Q7j4tW1yJuMVA3egRiQy5FPygwadkmPeaY%3d
    x-ms-version: 2.11
    Host: wamsbayclus001rest-hs.cloudapp.net

<span data-ttu-id="68447-230">**Odpowiedź HTTP**</span><span class="sxs-lookup"><span data-stu-id="68447-230">**HTTP Response**</span></span>

<span data-ttu-id="68447-231">Jeśli to się powiedzie, jest zwracany następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="68447-231">If successful, the following is returned:</span></span>

    HTTP/1.1 204 No Content
    ...

## <span data-ttu-id="68447-232"><a id="encode"></a>Kodowanie pliku źródłowego do zestawu plików MP4 z adaptacyjną szybkością transmisji bitów</span><span class="sxs-lookup"><span data-stu-id="68447-232"><a id="encode"></a>Encode the source file into a set of adaptive bitrate MP4 files</span></span>

<span data-ttu-id="68447-233">Po wprowadzania, które mogą być kodowane zasoby w usłudze Media Services nośnika, poddane transmultipleksacji, oznaczone znakiem wodnym i tak dalej przed dostarczeniem do klientów.</span><span class="sxs-lookup"><span data-stu-id="68447-233">After ingesting Assets into Media Services, media can be encoded, transmuxed, watermarked, and so on, before it is delivered to clients.</span></span> <span data-ttu-id="68447-234">Te działania są zaplanowane i uruchamiane w wielu wystąpieniach ról w tle, aby zapewnić wysoką wydajność oraz dostępność.</span><span class="sxs-lookup"><span data-stu-id="68447-234">These activities are scheduled and run against multiple background role instances to ensure high performance and availability.</span></span> <span data-ttu-id="68447-235">Te działania są nazywane zadaniami i każde zadanie składa się z niepodzielnych zadań, które wykonują rzeczywistą pracę w pliku zasobów (Aby uzyskać więcej informacji, zobacz [zadania](/rest/api/media/services/job), [zadań](/rest/api/media/services/task) opisy).</span><span class="sxs-lookup"><span data-stu-id="68447-235">These activities are called Jobs and each Job is composed of atomic Tasks that do the actual work on the Asset file (for more information, see [Job](/rest/api/media/services/job), [Task](/rest/api/media/services/task) descriptions).</span></span>

<span data-ttu-id="68447-236">Jak wspomniano wcześniej, podczas pracy z usługi Azure Media Services jednym z najbardziej typowych scenariuszy jest dostarczanie klientom usługi przesyłania strumieniowego adaptacyjną szybkością transmisji bitów.</span><span class="sxs-lookup"><span data-stu-id="68447-236">As was mentioned earlier, when working with Azure Media Services one of the most common scenarios is delivering adaptive bitrate streaming to your clients.</span></span> <span data-ttu-id="68447-237">Usługi Media Services można dynamicznie pakiet zestawu plików MP4 do jednego z następujących formatów: HTTP Live Streaming (HLS), Smooth Streaming, MPEG DASH.</span><span class="sxs-lookup"><span data-stu-id="68447-237">Media Services can dynamically package a set of adaptive bitrate MP4 files into one of the following formats: HTTP Live Streaming (HLS), Smooth Streaming, MPEG DASH.</span></span>

<span data-ttu-id="68447-238">Poniższej sekcji pokazano, jak utworzyć zadanie, które zawiera jedno zadanie kodowania.</span><span class="sxs-lookup"><span data-stu-id="68447-238">The following section shows how to create a job that contains one encoding task.</span></span> <span data-ttu-id="68447-239">Zadanie określa transkodowanie pliku mezzanine do zestawu z adaptacyjną szybkością transmisji bitów MP4s przy użyciu **Media Encoder Standard**.</span><span class="sxs-lookup"><span data-stu-id="68447-239">The task specifies to transcode the mezzanine file into a set of adaptive bitrate MP4s using **Media Encoder Standard**.</span></span> <span data-ttu-id="68447-240">W sekcji przedstawiono również monitorowanie przetwarzanie postęp zadań.</span><span class="sxs-lookup"><span data-stu-id="68447-240">The section also shows how to monitor the job processing progress.</span></span> <span data-ttu-id="68447-241">Po zakończeniu zadania użytkownik będzie mógł utworzyć lokalizatory, które są niezbędne do uzyskania dostępu do zasobów.</span><span class="sxs-lookup"><span data-stu-id="68447-241">When the job is complete, you would be able to create locators that are needed to get access to your assets.</span></span>

### <a name="get-a-media-processor"></a><span data-ttu-id="68447-242">Pobierz procesor multimediów</span><span class="sxs-lookup"><span data-stu-id="68447-242">Get a media processor</span></span>
<span data-ttu-id="68447-243">W usłudze Media Services procesor multimediów jest składnikiem, który obsługuje przetwarzania specyficznego dla zadania, takie jak kodowanie, Konwersja formatu zawartości multimedialnej szyfrowania lub odszyfrowywania.</span><span class="sxs-lookup"><span data-stu-id="68447-243">In Media Services, a media processor is a component that handles a specific processing task, such as encoding, format conversion, encrypting, or decrypting media content.</span></span> <span data-ttu-id="68447-244">Zadania kodowania przedstawiono w tym samouczku firma Microsoft będzie używany Media Encoder Standard.</span><span class="sxs-lookup"><span data-stu-id="68447-244">For the encoding task shown in this tutorial, we are going to use the Media Encoder Standard.</span></span>

<span data-ttu-id="68447-245">Poniższy kod żądania identyfikator kodera.</span><span class="sxs-lookup"><span data-stu-id="68447-245">The following code requests the encoder's id.</span></span>

<span data-ttu-id="68447-246">**Żądania HTTP**</span><span class="sxs-lookup"><span data-stu-id="68447-246">**HTTP Request**</span></span>

    GET https://wamsbayclus001rest-hs.cloudapp.net/api/MediaProcessors()?$filter=Name%20eq%20'Media%20Encoder%20Standard' HTTP/1.1
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amstestaccount001&urn%3aSubscriptionId=f7f09258-6753-4ca2-b1ae-193798e2c9d8&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1421675491&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=9hUudHYnATpi5hN3cvTfgw%2bL4N3tL0fdsRnQnm6ZYIU%3d
    x-ms-version: 2.11
    Host: wamsbayclus001rest-hs.cloudapp.net


<span data-ttu-id="68447-247">**Odpowiedź HTTP**</span><span class="sxs-lookup"><span data-stu-id="68447-247">**HTTP Response**</span></span>

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

### <a name="create-a-job"></a><span data-ttu-id="68447-248">Tworzenie zadania</span><span class="sxs-lookup"><span data-stu-id="68447-248">Create a job</span></span>
<span data-ttu-id="68447-249">Każde zadanie może mieć jedno lub więcej zadań, w zależności od typu przetwarzania, które chcesz wykonać.</span><span class="sxs-lookup"><span data-stu-id="68447-249">Each Job can have one or more Tasks depending on the type of processing that you want to accomplish.</span></span> <span data-ttu-id="68447-250">Za pomocą interfejsu API REST, można utworzyć zadania i ich zadania pokrewne w jeden z dwóch sposobów: zadania mogą być zdefiniowano w tekście za pośrednictwem właściwości nawigacji zadania na jednostkach zadania, lub przetwarzania wsadowego OData.</span><span class="sxs-lookup"><span data-stu-id="68447-250">Through the REST API, you can create Jobs and their related Tasks in one of two ways: Tasks can be defined inline through the Tasks navigation property on Job entities, or through OData batch processing.</span></span> <span data-ttu-id="68447-251">SDK usługi Media Services używa przetwarzania wsadowego.</span><span class="sxs-lookup"><span data-stu-id="68447-251">The Media Services SDK uses batch processing.</span></span> <span data-ttu-id="68447-252">Aby zwiększyć czytelność, przykładowe kody w tym temacie, zadania są zdefiniowano w tekście.</span><span class="sxs-lookup"><span data-stu-id="68447-252">However, for the readability of the code examples in this topic, tasks are defined inline.</span></span> <span data-ttu-id="68447-253">Informacje dotyczące przetwarzania wsadowego znajdują się w temacie [przetwarzanie wsadowe Open Data Protocol (OData)](http://www.odata.org/documentation/odata-version-3-0/batch-processing/).</span><span class="sxs-lookup"><span data-stu-id="68447-253">For information on batch processing, see [Open Data Protocol (OData) Batch Processing](http://www.odata.org/documentation/odata-version-3-0/batch-processing/).</span></span>

<span data-ttu-id="68447-254">Poniższy przykład przedstawia sposób tworzenia i opublikuj zadanie o zadań zdefiniowana kodowanie wideo w określonej rozdzielczości i jakości.</span><span class="sxs-lookup"><span data-stu-id="68447-254">The following example shows you how to create and post a Job with one Task set to encode a video at a specific resolution and quality.</span></span> <span data-ttu-id="68447-255">W poniższej sekcji dokumentacji zawiera listę wszystkich [zadań predefiniowane](http://msdn.microsoft.com/library/mt269960) obsługiwanych przez procesor Media Encoder Standard.</span><span class="sxs-lookup"><span data-stu-id="68447-255">The following documentation section contains the list of all the [task presets](http://msdn.microsoft.com/library/mt269960) supported by the Media Encoder Standard processor.</span></span>  

<span data-ttu-id="68447-256">**Żądania HTTP**</span><span class="sxs-lookup"><span data-stu-id="68447-256">**HTTP Request**</span></span>

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

<span data-ttu-id="68447-257">**Odpowiedź HTTP**</span><span class="sxs-lookup"><span data-stu-id="68447-257">**HTTP Response**</span></span>

<span data-ttu-id="68447-258">W przypadku powodzenia następującą odpowiedź jest zwracana:</span><span class="sxs-lookup"><span data-stu-id="68447-258">If successful, the following response is returned:</span></span>

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


<span data-ttu-id="68447-259">Istnieje kilka ważnych rzeczy do uwzględnienia w dowolnym żądaniu zadania:</span><span class="sxs-lookup"><span data-stu-id="68447-259">There are a few important things to note in any Job request:</span></span>

* <span data-ttu-id="68447-260">Aby określić ilość danych wejściowych lub wyjściowych zasoby, które są używane przez zadanie taskbody — właściwości należy użyć literału XML.</span><span class="sxs-lookup"><span data-stu-id="68447-260">TaskBody properties MUST use literal XML to define the number of input, or output assets that are used by the Task.</span></span> <span data-ttu-id="68447-261">Temat zadania zawiera definicję schematu XML dla pliku XML.</span><span class="sxs-lookup"><span data-stu-id="68447-261">The Task topic contains the XML Schema Definition for the XML.</span></span>
* <span data-ttu-id="68447-262">W definicji taskbody — wartość każdego wewnętrzny <inputAsset> i <outputAsset> musi być ustawiona jako JobInputAsset(value) lub JobOutputAsset(value).</span><span class="sxs-lookup"><span data-stu-id="68447-262">In the TaskBody definition, each inner value for <inputAsset> and <outputAsset> must be set as JobInputAsset(value) or JobOutputAsset(value).</span></span>
* <span data-ttu-id="68447-263">Zadanie może mieć wielu zasobów danych wyjściowych.</span><span class="sxs-lookup"><span data-stu-id="68447-263">A task can have multiple output assets.</span></span> <span data-ttu-id="68447-264">Jako dane wyjściowe zadania w ramach zadania jeden JobOutputAsset(x) można można użyć tylko raz.</span><span class="sxs-lookup"><span data-stu-id="68447-264">One JobOutputAsset(x) can only be used once as an output of a task in a job.</span></span>
* <span data-ttu-id="68447-265">JobInputAsset lub JobOutputAsset można określić jako zasób wprowadzania zadania.</span><span class="sxs-lookup"><span data-stu-id="68447-265">You can specify JobInputAsset or JobOutputAsset as an input asset of a task.</span></span>
* <span data-ttu-id="68447-266">Zadania musi nie tworzą cyklu.</span><span class="sxs-lookup"><span data-stu-id="68447-266">Tasks must not form a cycle.</span></span>
* <span data-ttu-id="68447-267">Parametru wartości, który jest przekazywany do JobInputAsset lub JobOutputAsset reprezentuje wartość indeksu dla elementu zawartości.</span><span class="sxs-lookup"><span data-stu-id="68447-267">The value parameter that you pass to JobInputAsset or JobOutputAsset represents the index value for an Asset.</span></span> <span data-ttu-id="68447-268">Rzeczywiste zasoby są definiowane w InputMediaAssets i OutputMediaAssets właściwości nawigacji w definicji zadania jednostki.</span><span class="sxs-lookup"><span data-stu-id="68447-268">The actual Assets are defined in the InputMediaAssets and OutputMediaAssets navigation properties on the Job entity definition.</span></span>

> [!NOTE]
> <span data-ttu-id="68447-269">Ponieważ usługi Media Services jest oparty na OData v3, poszczególne zasoby w kolekcji właściwości nawigacji InputMediaAssets i OutputMediaAssets istnieją odwołania za pośrednictwem "__metadata: identyfikator uri" pary nazwa wartość.</span><span class="sxs-lookup"><span data-stu-id="68447-269">Because Media Services is built on OData v3, the individual assets in InputMediaAssets and OutputMediaAssets navigation property collections are referenced through a "__metadata : uri" name-value pair.</span></span>
>
>

* <span data-ttu-id="68447-270">Mapuje InputMediaAssets na jeden lub więcej zasobów, które zostały utworzone w usłudze Media Services.</span><span class="sxs-lookup"><span data-stu-id="68447-270">InputMediaAssets maps to one or more Assets you have created in Media Services.</span></span> <span data-ttu-id="68447-271">OutputMediaAssets są tworzone przez system.</span><span class="sxs-lookup"><span data-stu-id="68447-271">OutputMediaAssets are created by the system.</span></span> <span data-ttu-id="68447-272">Nie odwołują się do istniejącego zasobu.</span><span class="sxs-lookup"><span data-stu-id="68447-272">They do not reference an existing asset.</span></span>
* <span data-ttu-id="68447-273">Może być nazwany OutputMediaAssets za pomocą atrybutu assetName.</span><span class="sxs-lookup"><span data-stu-id="68447-273">OutputMediaAssets can be named using the assetName attribute.</span></span> <span data-ttu-id="68447-274">Jeśli ten atrybut nie jest obecny, a następnie nazwę OutputMediaAsset to niezależnie od tekst wewnętrzny wartość <outputAsset> element jest z sufiksem Nazwa zadania wartość lub wartość identyfikatora zadania (w przypadku, gdy nie jest zdefiniowana właściwość Name).</span><span class="sxs-lookup"><span data-stu-id="68447-274">If this attribute is not present, then the name of the OutputMediaAsset is whatever the inner text value of the <outputAsset> element is with a suffix of either the Job Name value, or the Job Id value (in the case where the Name property isn't defined).</span></span> <span data-ttu-id="68447-275">Na przykład jeśli ustawisz wartość assetName dotyczące nazwy "Test", następnie właściwość OutputMediaAsset Name może być równa "Test".</span><span class="sxs-lookup"><span data-stu-id="68447-275">For example, if you set a value for assetName to "Sample", then the OutputMediaAsset Name property would be set to "Sample".</span></span> <span data-ttu-id="68447-276">Jednak jeśli nie ustawiona wartość assetName, ale ustawiona na nazwę zadania na "NewJob", nazwa OutputMediaAsset będzie "_NewJob JobOutputAsset (wartość)".</span><span class="sxs-lookup"><span data-stu-id="68447-276">However, if you did not set a value for assetName, but did set the job name to "NewJob", then the OutputMediaAsset Name would be "JobOutputAsset(value)_NewJob".</span></span>

    <span data-ttu-id="68447-277">Poniższy przykład przedstawia sposób ustawiania atrybutu assetName:</span><span class="sxs-lookup"><span data-stu-id="68447-277">The following example shows how to set the assetName attribute:</span></span>

        "<?xml version=\"1.0\" encoding=\"utf-8\"?><taskBody><inputAsset>JobInputAsset(0)</inputAsset><outputAsset assetName=\"CustomOutputAssetName\">JobOutputAsset(0)</outputAsset></taskBody>"
* <span data-ttu-id="68447-278">Aby włączyć tworzenie łańcuchów zadań:</span><span class="sxs-lookup"><span data-stu-id="68447-278">To enable task chaining:</span></span>

  * <span data-ttu-id="68447-279">Zadanie musi mieć co najmniej dwa zadania</span><span class="sxs-lookup"><span data-stu-id="68447-279">A job must have at least two tasks</span></span>
  * <span data-ttu-id="68447-280">Musi istnieć co najmniej jedno zadanie, którego dane wejściowe są dane wyjściowe inne zadanie w zadaniu.</span><span class="sxs-lookup"><span data-stu-id="68447-280">There must be at least one task whose input is output of another task in the job.</span></span>

<span data-ttu-id="68447-281">Aby uzyskać więcej informacji, zobacz [Tworzenie zadania kodowania za pomocą interfejsu API REST usług Media](media-services-rest-encode-asset.md).</span><span class="sxs-lookup"><span data-stu-id="68447-281">For more information see, [Creating an Encoding Job with the Media Services REST API](media-services-rest-encode-asset.md).</span></span>

### <a name="monitor-processing-progress"></a><span data-ttu-id="68447-282">Monitor przetwarzania postępu</span><span class="sxs-lookup"><span data-stu-id="68447-282">Monitor Processing Progress</span></span>
<span data-ttu-id="68447-283">Można pobrać stanu zadania za pomocą właściwości stanu, jak pokazano w poniższym przykładzie.</span><span class="sxs-lookup"><span data-stu-id="68447-283">You can retrieve the Job status by using the State property, as shown in the following example.</span></span>

<span data-ttu-id="68447-284">**Żądania HTTP**</span><span class="sxs-lookup"><span data-stu-id="68447-284">**HTTP Request**</span></span>

    GET https://wamsbayclus001rest-hs.net/api/Jobs('nb%3Ajid%3AUUID%3A71d2dd33-efdf-ec43-8ea1-136a110bd42c')/State HTTP/1.1
    Content-Type: application/json;odata=verbose
    Accept: application/json;odata=verbose
    DataServiceVersion: 3.0
    MaxDataServiceVersion: 3.0
    x-ms-version: 2.11
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=youraccountname&urn%3aSubscriptionId=zf84471d-2233-4e75-aa09-010f0fc0cf5b&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1336908022&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=RYXOraO6Z%2f7l9whWZQN%2bypeijgHwIk8XyikA01Kx1%2bk%3d
    Host: wamsbayclus001rest-hs.net
    Content-Length: 0


<span data-ttu-id="68447-285">**Odpowiedź HTTP**</span><span class="sxs-lookup"><span data-stu-id="68447-285">**HTTP Response**</span></span>

<span data-ttu-id="68447-286">W przypadku powodzenia następującą odpowiedź jest zwracana:</span><span class="sxs-lookup"><span data-stu-id="68447-286">If successful, the following response is returned:</span></span>

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


### <a name="cancel-a-job"></a><span data-ttu-id="68447-287">Anulowanie zadania</span><span class="sxs-lookup"><span data-stu-id="68447-287">Cancel a job</span></span>
<span data-ttu-id="68447-288">Usługa Media Services umożliwia anulowanie uruchomionych zadań przy użyciu funkcji CancelJob.</span><span class="sxs-lookup"><span data-stu-id="68447-288">Media Services allows you to cancel running jobs through the CancelJob function.</span></span> <span data-ttu-id="68447-289">To wywołanie zwraca błąd 400 kodu przy próbie anulowania zadania, jeśli jego stan zostanie anulowane, anulowanie, błąd lub zakończona.</span><span class="sxs-lookup"><span data-stu-id="68447-289">This call returns a 400 error code if you try to cancel a Job when its state is canceled, canceling, error, or finished.</span></span>

<span data-ttu-id="68447-290">Poniższy przykład przedstawia sposób wywołania CancelJob.</span><span class="sxs-lookup"><span data-stu-id="68447-290">The following example shows how to call CancelJob.</span></span>

<span data-ttu-id="68447-291">**Żądania HTTP**</span><span class="sxs-lookup"><span data-stu-id="68447-291">**HTTP Request**</span></span>

    GET https://wamsbayclus001rest-hs.net/API/CancelJob?jobid='nb%3ajid%3aUUID%3a71d2dd33-efdf-ec43-8ea1-136a110bd42c' HTTP/1.1
    Content-Type: application/json;odata=verbose
    Accept: application/json;odata=verbose
    DataServiceVersion: 3.0
    MaxDataServiceVersion: 3.0
    x-ms-version: 2.2
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=youraccountname&urn%3aSubscriptionId=2f84471d-b1ae-4e75-aa09-010f0fc0cf5b&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1336908753&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=kolAgnFfbQIeRv4lWxKSFa4USyjWXRm15Kd%2bNd5g8eA%3d
    Host: wamsbayclus001rest-hs.net


<span data-ttu-id="68447-292">W przypadku powodzenia kodu 204 odpowiedź jest zwracana z treści wiadomości.</span><span class="sxs-lookup"><span data-stu-id="68447-292">If successful, a 204 response code is returned with no message body.</span></span>

> [!NOTE]
> <span data-ttu-id="68447-293">Należy zakodować adres URL identyfikatora zadania (zazwyczaj nb:jid:UUID: somevalue) podczas przekazywania go jako parametr do CancelJob.</span><span class="sxs-lookup"><span data-stu-id="68447-293">You must URL-encode the job id (normally nb:jid:UUID: somevalue) when passing it in as a parameter to CancelJob.</span></span>
>
>

### <a name="get-the-output-asset"></a><span data-ttu-id="68447-294">Pobierz elementu zawartości wyjściowej</span><span class="sxs-lookup"><span data-stu-id="68447-294">Get the output asset</span></span>
<span data-ttu-id="68447-295">Poniższy kod przedstawia sposób żądania elementu zawartości wyjściowej identyfikatora.</span><span class="sxs-lookup"><span data-stu-id="68447-295">The following code shows how to request the output asset Id.</span></span>

<span data-ttu-id="68447-296">**Żądania HTTP**</span><span class="sxs-lookup"><span data-stu-id="68447-296">**HTTP Request**</span></span>

    GET https://wamsbayclus001rest-hs.cloudapp.net/api/Jobs('nb%3Ajid%3AUUID%3A71d2dd33-efdf-ec43-8ea1-136a110bd42c')/OutputMediaAssets() HTTP/1.1
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    User-Agent: Microsoft ADO.NET Data Services
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amstestaccount001&urn%3aSubscriptionId=z7f09258-2233-4ca2-b1ae-193798e2c9d8&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1421675491&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=9hUudHYnATpi5hN3cvTfgw%2bL4N3tL0fdsRnQnm6ZYIU%3d
    x-ms-version: 2.11
    Host: wamsbayclus001rest-hs.cloudapp.net


<span data-ttu-id="68447-297">**Odpowiedź HTTP**</span><span class="sxs-lookup"><span data-stu-id="68447-297">**HTTP Response**</span></span>

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



## <span data-ttu-id="68447-298"><a id="publish_get_urls"></a>Publikowanie elementu zawartości i get przesyłania strumieniowego i pobierania progresywnego adresy URL z interfejsu API REST</span><span class="sxs-lookup"><span data-stu-id="68447-298"><a id="publish_get_urls"></a>Publish the asset and get streaming and progressive download URLs with REST API</span></span>

<span data-ttu-id="68447-299">Aby przesłać strumieniowo lub pobrać element zawartości, należy go najpierw opublikować, tworząc lokalizator.</span><span class="sxs-lookup"><span data-stu-id="68447-299">To stream or download an asset, you first need to "publish" it by creating a locator.</span></span> <span data-ttu-id="68447-300">Lokalizatory zapewniają dostęp do plików znajdujących się w elemencie zawartości.</span><span class="sxs-lookup"><span data-stu-id="68447-300">Locators provide access to files contained in the asset.</span></span> <span data-ttu-id="68447-301">Usługa Media Services obsługuje dwa typy lokalizatorów: lokalizatory OnDemandOrigin używane do strumieniowego przesyłania plików multimedialnych (na przykład w formacie MPEG DASH, HLS i Smooth Streaming) oraz lokalizatory sygnatury dostępu współdzielonego (SAS) używane do pobierania plików multimedialnych.</span><span class="sxs-lookup"><span data-stu-id="68447-301">Media Services supports two types of locators: OnDemandOrigin locators, used to stream media (for example, MPEG DASH, HLS, or Smooth Streaming) and Access Signature (SAS) locators, used to download media files.</span></span> <span data-ttu-id="68447-302">Aby uzyskać więcej informacji na temat sygnatury dostępu Współdzielonego Zobacz lokalizatorów [to](http://southworks.com/blog/2015/05/27/reusing-azure-media-services-locators-to-avoid-facing-the-5-shared-access-policy-limitation/) blogu.</span><span class="sxs-lookup"><span data-stu-id="68447-302">For more information about SAS locators see [this](http://southworks.com/blog/2015/05/27/reusing-azure-media-services-locators-to-avoid-facing-the-5-shared-access-policy-limitation/) blog.</span></span>

<span data-ttu-id="68447-303">Po utworzeniu lokalizatorów można tworzyć adresy URL, które są używane do przesyłania strumieniowego lub pobierania plików.</span><span class="sxs-lookup"><span data-stu-id="68447-303">Once you create the locators, you can build the URLs that are used to stream or download your files.</span></span>

>[!NOTE]
><span data-ttu-id="68447-304">Po utworzeniu konta usługi AMS zostanie do niego dodany **domyślny** punkt końcowy przesyłania strumieniowego mający stan **Zatrzymany**.</span><span class="sxs-lookup"><span data-stu-id="68447-304">When your AMS account is created a **default** streaming endpoint is added to your account in the **Stopped** state.</span></span> <span data-ttu-id="68447-305">Aby rozpocząć przesyłanie strumieniowe zawartości oraz korzystać z dynamicznego tworzenia pakietów i szyfrowania dynamicznego, punkt końcowy przesyłania strumieniowego, z którego chcesz strumieniowo przesyłać zawartość, musi mieć stan **Uruchomiony**.</span><span class="sxs-lookup"><span data-stu-id="68447-305">To start streaming your content and take advantage of dynamic packaging and dynamic encryption, the streaming endpoint from which you want to stream content has to be in the **Running** state.</span></span>

<span data-ttu-id="68447-306">Adres URL dla protokołu Smooth Streaming ma następujący format:</span><span class="sxs-lookup"><span data-stu-id="68447-306">A streaming URL for Smooth Streaming has the following format:</span></span>

    {streaming endpoint name-media services account name}.streaming.mediaservices.windows.net/{locator ID}/{filename}.ism/Manifest

<span data-ttu-id="68447-307">Adres URL dla protokołu HLS ma następujący format:</span><span class="sxs-lookup"><span data-stu-id="68447-307">A streaming URL for HLS has the following format:</span></span>

    {streaming endpoint name-media services account name}.streaming.mediaservices.windows.net/{locator ID}/{filename}.ism/Manifest(format=m3u8-aapl)

<span data-ttu-id="68447-308">Adres URL dla protokołu MPEG DASH ma następujący format:</span><span class="sxs-lookup"><span data-stu-id="68447-308">A streaming URL for MPEG DASH has the following format:</span></span>

    {streaming endpoint name-media services account name}.streaming.mediaservices.windows.net/{locator ID}/{filename}.ism/Manifest(format=mpd-time-csf)


<span data-ttu-id="68447-309">Adres URL SAS używany do pobierania plików ma następujący format:</span><span class="sxs-lookup"><span data-stu-id="68447-309">A SAS URL used to download files has the following format:</span></span>

    {blob container name}/{asset name}/{file name}/{SAS signature}

<span data-ttu-id="68447-310">W tej sekcji przedstawiono sposób wykonywania następujących zadań konieczne "Publikuj" zasobów.</span><span class="sxs-lookup"><span data-stu-id="68447-310">This section shows how to perform the following tasks necessary to "publish" your assets.</span></span>  

* <span data-ttu-id="68447-311">Tworzenie AccessPolicy z uprawnieniem do odczytu</span><span class="sxs-lookup"><span data-stu-id="68447-311">Creating the AccessPolicy with read permission</span></span>
* <span data-ttu-id="68447-312">Tworzenie adres URL SAS dla pobierania zawartości</span><span class="sxs-lookup"><span data-stu-id="68447-312">Creating a SAS URL for downloading content</span></span>
* <span data-ttu-id="68447-313">Tworzenie źródłowy adres URL przesyłania strumieniowego zawartości</span><span class="sxs-lookup"><span data-stu-id="68447-313">Creating an origin URL for streaming content</span></span>

### <a name="creating-the-accesspolicy-with-read-permission"></a><span data-ttu-id="68447-314">Tworzenie AccessPolicy z uprawnieniem do odczytu</span><span class="sxs-lookup"><span data-stu-id="68447-314">Creating the AccessPolicy with read permission</span></span>
<span data-ttu-id="68447-315">Przed pobraniem lub przesyłania strumieniowego zawartości nośnika, zdefiniuj AccessPolicy z uprawnienia do odczytu i utworzyć odpowiednie jednostki lokalizatora, która określa typ mechanizm dostarczania, które chcesz włączyć dla klientów.</span><span class="sxs-lookup"><span data-stu-id="68447-315">Before downloading or streaming any media content, first define an AccessPolicy with read permissions and create the appropriate Locator entity that specifies the type of delivery mechanism you want to enable for your clients.</span></span> <span data-ttu-id="68447-316">Aby uzyskać więcej informacji na dostępne właściwości, zobacz [właściwości jednostki AccessPolicy](https://docs.microsoft.com/rest/api/media/operations/accesspolicy#accesspolicy_properties).</span><span class="sxs-lookup"><span data-stu-id="68447-316">For more information on the properties available, see [AccessPolicy Entity Properties](https://docs.microsoft.com/rest/api/media/operations/accesspolicy#accesspolicy_properties).</span></span>

<span data-ttu-id="68447-317">Poniższy przykład przedstawia sposób określania AccessPolicy uzyskać uprawnienia do odczytu dla danego elementu zawartości.</span><span class="sxs-lookup"><span data-stu-id="68447-317">The following example shows how to specify the AccessPolicy for read permissions for a given Asset.</span></span>

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

<span data-ttu-id="68447-318">W przypadku powodzenia zostanie zwrócony kod 201 sukces, opisujący jednostki AccessPolicy, który został utworzony.</span><span class="sxs-lookup"><span data-stu-id="68447-318">If successful, a 201 success code is returned describing the AccessPolicy entity that you created.</span></span> <span data-ttu-id="68447-319">Następnie należy użyć identyfikatora AccessPolicy wraz z identyfikatorem zasobu z zawartości, który zawiera plik, który chcesz dostarczyć (np. zawartości wyjściowej) można utworzyć jednostki lokalizatora.</span><span class="sxs-lookup"><span data-stu-id="68447-319">You then use the AccessPolicy Id along with the Asset Id of the asset that contains the file you want to deliver(such as an output asset) to create the Locator entity.</span></span>

> [!NOTE]
> <span data-ttu-id="68447-320">Ten podstawowy przepływ pracy jest taka sama jak przekazywanie pliku podczas wprowadzania zasobów (zgodnie z opisem został wcześniej w tym temacie).</span><span class="sxs-lookup"><span data-stu-id="68447-320">This basic workflow is the same as uploading a file when ingesting an Asset (as was discussed earlier in this topic).</span></span> <span data-ttu-id="68447-321">Ponadto takich jak przekazywanie plików, jeśli użytkownik (lub klientów) muszą uzyskać dostęp do plików natychmiast, ustaw wartość StartTime pięć minut przed bieżącym czasem.</span><span class="sxs-lookup"><span data-stu-id="68447-321">Also, like uploading files, if you (or your clients) need to access your files immediately, set your StartTime value to five minutes before the current time.</span></span> <span data-ttu-id="68447-322">Ta akcja jest niezbędne, ponieważ może istnieć zegara pochylenia między klientem a Media Services.</span><span class="sxs-lookup"><span data-stu-id="68447-322">This action is necessary because there may be clock skew between the client and Media Services.</span></span> <span data-ttu-id="68447-323">Wartość StartTime musi być w następującym formacie daty/godziny: RRRR-MM-ddtgg (na przykład "2014-05-23T17:53:50Z").</span><span class="sxs-lookup"><span data-stu-id="68447-323">The StartTime value must be in the following DateTime format: YYYY-MM-DDTHH:mm:ssZ (for example, "2014-05-23T17:53:50Z").</span></span>
>
>

### <a name="creating-a-sas-url-for-downloading-content"></a><span data-ttu-id="68447-324">Tworzenie adres URL SAS dla pobierania zawartości</span><span class="sxs-lookup"><span data-stu-id="68447-324">Creating a SAS URL for downloading content</span></span>
<span data-ttu-id="68447-325">Poniższy kod przedstawia sposób uzyskać adres URL, który może służyć do pobrania plik nośnika utworzony i przekazać wcześniej.</span><span class="sxs-lookup"><span data-stu-id="68447-325">The following code shows how to get a URL that can be used to download a media file created and uploaded previously.</span></span> <span data-ttu-id="68447-326">AccessPolicy zapoznał zestaw uprawnień i ścieżka lokalizatora odwołuje się do adresu URL pobierania sygnatury dostępu Współdzielonego.</span><span class="sxs-lookup"><span data-stu-id="68447-326">The AccessPolicy has read permissions set and the Locator path refers to a SAS download URL.</span></span>

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

<span data-ttu-id="68447-327">W przypadku powodzenia następującą odpowiedź jest zwracana:</span><span class="sxs-lookup"><span data-stu-id="68447-327">If successful, the following response is returned:</span></span>

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


<span data-ttu-id="68447-328">Zwrócona **ścieżki** właściwość zawiera adres URL SAS.</span><span class="sxs-lookup"><span data-stu-id="68447-328">The returned **Path** property contains the SAS URL.</span></span>

> [!NOTE]
> <span data-ttu-id="68447-329">Pobrania zawartości szyfrowany w magazynie, musisz ręcznie go odszyfrować przed renderowaniem go lub użyj MediaProcessor odszyfrowywania magazynu w ramach zadania przetwarzania przetworzonych plików w Wyczyść, aby OutputAsset wyjściowych, a następnie pobrać danego.</span><span class="sxs-lookup"><span data-stu-id="68447-329">If you download storage encrypted content, you must manually decrypt it before rendering it, or use the Storage Decryption MediaProcessor in a processing task to output processed files in the clear to an OutputAsset and then download from that Asset.</span></span> <span data-ttu-id="68447-330">Aby uzyskać więcej informacji na temat przetwarzania Zobacz Tworzenie zadania kodowania za pomocą interfejsu API REST usługi multimediów.</span><span class="sxs-lookup"><span data-stu-id="68447-330">For more information on processing, see Creating an Encoding Job with the Media Services REST API.</span></span> <span data-ttu-id="68447-331">Ponadto nie można zaktualizować lokalizatorów adres URL SAS, po ich utworzeniu.</span><span class="sxs-lookup"><span data-stu-id="68447-331">Also, SAS URL Locators cannot be updated after they have been created.</span></span> <span data-ttu-id="68447-332">Na przykład nie można ponownie użyć tego samego lokalizatora z zaktualizowanej wartości StartTime.</span><span class="sxs-lookup"><span data-stu-id="68447-332">For example, you cannot reuse the same Locator with an updated StartTime value.</span></span> <span data-ttu-id="68447-333">Jest to spowodowane sposobu tworzenia adresów URL SAS.</span><span class="sxs-lookup"><span data-stu-id="68447-333">This is because of the way SAS URLs are created.</span></span> <span data-ttu-id="68447-334">Jeśli chcesz uzyskać dostępu do zasobów do pobrania, po upływie lokalizatora musi utworzyć nową z nowej wartości StartTime.</span><span class="sxs-lookup"><span data-stu-id="68447-334">If you want to access an asset for download after a Locator has expired, then you must create a new one with a new StartTime.</span></span>
>
>

### <a name="download-files"></a><span data-ttu-id="68447-335">Pobieranie plików</span><span class="sxs-lookup"><span data-stu-id="68447-335">Download files</span></span>
<span data-ttu-id="68447-336">Po utworzeniu AccessPolicy i ustawić lokalizatora, możesz pobrać plików za pomocą interfejsów API REST usługi Magazyn Azure.</span><span class="sxs-lookup"><span data-stu-id="68447-336">Once you have the AccessPolicy and Locator set, you can download files using the Azure Storage REST APIs.</span></span>  

> [!NOTE]
> <span data-ttu-id="68447-337">Należy dodać nazwę pliku dla pliku, który chcesz pobrać na lokalizatorze **ścieżki** wartość odebrana w poprzedniej sekcji.</span><span class="sxs-lookup"><span data-stu-id="68447-337">You must add the file name for the file you want to download to the Locator **Path** value received in the previous section.</span></span> <span data-ttu-id="68447-338">Na przykład https://storagetestaccount001.blob.core.windows.net/asset-e7b02da4-5a69-40e7-a8db-e8f4f697aac0/BigBuckBunny.mp4?</span><span class="sxs-lookup"><span data-stu-id="68447-338">For example, https://storagetestaccount001.blob.core.windows.net/asset-e7b02da4-5a69-40e7-a8db-e8f4f697aac0/BigBuckBunny.mp4?</span></span> <span data-ttu-id="68447-339">.</span><span class="sxs-lookup"><span data-stu-id="68447-339">.</span></span> <span data-ttu-id="68447-340">.</span><span class="sxs-lookup"><span data-stu-id="68447-340">.</span></span> <span data-ttu-id="68447-341">.</span><span class="sxs-lookup"><span data-stu-id="68447-341">.</span></span>
>
>

<span data-ttu-id="68447-342">Aby uzyskać więcej informacji na temat pracy z obiektami blob magazynu Azure, zobacz [interfejsu API REST usługi Blob](https://docs.microsoft.com/rest/api/storageservices/Blob-Service-REST-API).</span><span class="sxs-lookup"><span data-stu-id="68447-342">For more information on working with Azure storage blobs, see [Blob Service REST API](https://docs.microsoft.com/rest/api/storageservices/Blob-Service-REST-API).</span></span>

<span data-ttu-id="68447-343">W wyniku zadania kodowania wykonano wcześniejszych (kodowanie na zestaw MP4 z adaptacyjną) masz wiele plików MP4, które można pobrać progresywnie.</span><span class="sxs-lookup"><span data-stu-id="68447-343">As a result of the encoding job that you performed earlier (encoding into Adaptive MP4 set), you have multiple MP4 files that you can progressively download.</span></span> <span data-ttu-id="68447-344">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="68447-344">For example:</span></span>    

    https://storagetestaccount001.blob.core.windows.net/asset-38058602-a4b8-4b33-b9f0-6880dc1490ea/BigBuckBunny_H264_650kbps_AAC_und_ch2_96kbps.mp4?sv=2012-02-12&sr=c&si=166d5154-b801-410b-a226-ee2f8eac1929&sig=P2iNZJAvAWpp%2Bj9yV6TQjoz5DIIaj7ve8ARynmEM6Xk%3D&se=2015-02-14T01:13:05Z

    https://storagetestaccount001.blob.core.windows.net/asset-38058602-a4b8-4b33-b9f0-6880dc1490ea/BigBuckBunny_H264_400kbps_AAC_und_ch2_96kbps.mp4?sv=2012-02-12&sr=c&si=166d5154-b801-410b-a226-ee2f8eac1929&sig=P2iNZJAvAWpp%2Bj9yV6TQjoz5DIIaj7ve8ARynmEM6Xk%3D&se=2015-02-14T01:13:05Z

    https://storagetestaccount001.blob.core.windows.net/asset-38058602-a4b8-4b33-b9f0-6880dc1490ea/BigBuckBunny_H264_3400kbps_AAC_und_ch2_96kbps.mp4?sv=2012-02-12&sr=c&si=166d5154-b801-410b-a226-ee2f8eac1929&sig=P2iNZJAvAWpp%2Bj9yV6TQjoz5DIIaj7ve8ARynmEM6Xk%3D&se=2015-02-14T01:13:05Z

    https://storagetestaccount001.blob.core.windows.net/asset-38058602-a4b8-4b33-b9f0-6880dc1490ea/BigBuckBunny_H264_2250kbps_AAC_und_ch2_96kbps.mp4?sv=2012-02-12&sr=c&si=166d5154-b801-410b-a226-ee2f8eac1929&sig=P2iNZJAvAWpp%2Bj9yV6TQjoz5DIIaj7ve8ARynmEM6Xk%3D&se=2015-02-14T01:13:05Z

    https://storagetestaccount001.blob.core.windows.net/asset-38058602-a4b8-4b33-b9f0-6880dc1490ea/BigBuckBunny_H264_1500kbps_AAC_und_ch2_96kbps.mp4?sv=2012-02-12&sr=c&si=166d5154-b801-410b-a226-ee2f8eac1929&sig=P2iNZJAvAWpp%2Bj9yV6TQjoz5DIIaj7ve8ARynmEM6Xk%3D&se=2015-02-14T01:13:05Z

    https://storagetestaccount001.blob.core.windows.net/asset-38058602-a4b8-4b33-b9f0-6880dc1490ea/BigBuckBunny_H264_1000kbps_AAC_und_ch2_96kbps.mp4?sv=2012-02-12&sr=c&si=166d5154-b801-410b-a226-ee2f8eac1929&sig=P2iNZJAvAWpp%2Bj9yV6TQjoz5DIIaj7ve8ARynmEM6Xk%3D&se=2015-02-14T01:13:05Z

    https://storagetestaccount001.blob.core.windows.net/asset-38058602-a4b8-4b33-b9f0-6880dc1490ea/BigBuckBunny_AAC_und_ch2_96kbps.mp4?sv=2012-02-12&sr=c&si=166d5154-b801-410b-a226-ee2f8eac1929&sig=P2iNZJAvAWpp%2Bj9yV6TQjoz5DIIaj7ve8ARynmEM6Xk%3D&se=2015-02-14T01:13:05Z

    https://storagetestaccount001.blob.core.windows.net/asset-38058602-a4b8-4b33-b9f0-6880dc1490ea/BigBuckBunny_AAC_und_ch2_56kbps.mp4?sv=2012-02-12&sr=c&si=166d5154-b801-410b-a226-ee2f8eac1929&sig=P2iNZJAvAWpp%2Bj9yV6TQjoz5DIIaj7ve8ARynmEM6Xk%3D&se=2015-02-14T01:13:05Z


### <a name="creating-a-streaming-url-for-streaming-content"></a><span data-ttu-id="68447-345">Tworzenie adresu URL przesyłania strumieniowego przesyłania strumieniowego zawartości</span><span class="sxs-lookup"><span data-stu-id="68447-345">Creating a streaming URL for streaming content</span></span>
<span data-ttu-id="68447-346">Poniższy kod przedstawia sposób tworzenia Lokalizator przesyłania strumieniowego adresu URL:</span><span class="sxs-lookup"><span data-stu-id="68447-346">The following code shows how to create a streaming URL Locator:</span></span>

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

<span data-ttu-id="68447-347">W przypadku powodzenia następującą odpowiedź jest zwracana:</span><span class="sxs-lookup"><span data-stu-id="68447-347">If successful, the following response is returned:</span></span>

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

<span data-ttu-id="68447-348">Do przesyłania strumieniowego Smooth Streaming źródłowy adres URL w odtwarzaczu multimedialnym przesyłania strumieniowego, można dołączyć ścieżki właściwości o nazwie Smooth Streaming pliku, a następnie manifestu "/ manifest".</span><span class="sxs-lookup"><span data-stu-id="68447-348">To stream a Smooth Streaming origin URL in a streaming media player, you must append the Path property with the name of the Smooth Streaming manifest file, followed by "/manifest".</span></span>

    http://amstestaccount001.streaming.mediaservices.windows.net/ebf733c4-3e2e-4a68-b67b-cc5159d1d7f2/BigBuckBunny.ism/manifest

<span data-ttu-id="68447-349">Aby przesyłać strumieniowo HLS, Dołącz (format = m3u8-aapl) po "/ manifest".</span><span class="sxs-lookup"><span data-stu-id="68447-349">To stream HLS, append (format=m3u8-aapl) after the "/manifest".</span></span>

    http://amstestaccount001.streaming.mediaservices.windows.net/ebf733c4-3e2e-4a68-b67b-cc5159d1d7f2/BigBuckBunny.ism/manifest(format=m3u8-aapl)

<span data-ttu-id="68447-350">Do przesyłania strumieniowego MPEG DASH, Dołącz (format = mpd-time-csf) po "/ manifest".</span><span class="sxs-lookup"><span data-stu-id="68447-350">To stream MPEG DASH, append (format=mpd-time-csf) after the "/manifest".</span></span>

    http://amstestaccount001.streaming.mediaservices.windows.net/ebf733c4-3e2e-4a68-b67b-cc5159d1d7f2/BigBuckBunny.ism/manifest(format=mpd-time-csf)


## <span data-ttu-id="68447-351"><a id="play"></a>Odtwarzanie zawartości</span><span class="sxs-lookup"><span data-stu-id="68447-351"><a id="play"></a>Play your content</span></span>
<span data-ttu-id="68447-352">Do przesyłania strumieniowego zawartości wideo użyj [odtwarzacza usługi Azure Media Services](http://amsplayer.azurewebsites.net/azuremediaplayer.html).</span><span class="sxs-lookup"><span data-stu-id="68447-352">To stream you video, use [Azure Media Services Player](http://amsplayer.azurewebsites.net/azuremediaplayer.html).</span></span>

<span data-ttu-id="68447-353">Aby przetestować pobieranie progresywne, wklej adres URL do przeglądarki (na przykład programu Internet Explorer, Chrome, Safari).</span><span class="sxs-lookup"><span data-stu-id="68447-353">To test progressive download, paste a URL into a browser (for example, IE, Chrome, Safari).</span></span>

## <a name="next-steps-media-services-learning-paths"></a><span data-ttu-id="68447-354">Następne kroki: ścieżki szkoleniowe dotyczące usługi Media Services</span><span class="sxs-lookup"><span data-stu-id="68447-354">Next Steps: Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="68447-355">Przekazywanie opinii</span><span class="sxs-lookup"><span data-stu-id="68447-355">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]
