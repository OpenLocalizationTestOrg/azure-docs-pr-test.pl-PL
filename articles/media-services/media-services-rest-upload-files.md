---
title: "pliki aaaUpload do konta usługi Media Services za pomocą usługi REST | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak nośnika tooget zawartości do usługi Media Services za tworzenie i przekazywanie zasoby."
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: 41df7cbe-b8e2-48c1-a86c-361ec4e5251f
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/10/2017
ms.author: juliako
ms.openlocfilehash: 2a92cecdc32d747d7a478946f069c15931eb32b9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="upload-files-into-a-media-services-account-using-rest"></a><span data-ttu-id="7b4fa-103">Przekazywanie plików do konta usługi Media Services za pomocą usługi REST</span><span class="sxs-lookup"><span data-stu-id="7b4fa-103">Upload files into a Media Services account using REST</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="7b4fa-104">.NET</span><span class="sxs-lookup"><span data-stu-id="7b4fa-104">.NET</span></span>](media-services-dotnet-upload-files.md)
> * [<span data-ttu-id="7b4fa-105">REST</span><span class="sxs-lookup"><span data-stu-id="7b4fa-105">REST</span></span>](media-services-rest-upload-files.md)
> * [<span data-ttu-id="7b4fa-106">Portal</span><span class="sxs-lookup"><span data-stu-id="7b4fa-106">Portal</span></span>](media-services-portal-upload-files.md)
> 
> 

<span data-ttu-id="7b4fa-107">Za pomocą usługi Media Services można przekazać pliki cyfrowe do elementu zawartości.</span><span class="sxs-lookup"><span data-stu-id="7b4fa-107">In Media Services, you upload your digital files into an asset.</span></span> <span data-ttu-id="7b4fa-108">Witaj [zasobów](https://docs.microsoft.com/rest/api/media/operations/asset) może zawierać wideo, audio, obrazy, kolekcje miniatur, tekst ścieżek i napisów plików (i hello metadane dotyczące tych plików.)  Po hello pliki są przekazywane do hello zawartości, zawartość jest bezpiecznie przechowywana w chmurze powitania dla dalszego przetwarzania i przesyłania strumieniowego.</span><span class="sxs-lookup"><span data-stu-id="7b4fa-108">hello [Asset](https://docs.microsoft.com/rest/api/media/operations/asset) entity can contain video, audio, images, thumbnail collections, text tracks and closed caption files (and hello metadata about these files.)  Once hello files are uploaded into hello asset, your content is stored securely in hello cloud for further processing and streaming.</span></span> 

> [!NOTE]
> <span data-ttu-id="7b4fa-109">Zastosuj Hello następujące zagadnienia:</span><span class="sxs-lookup"><span data-stu-id="7b4fa-109">hello following considerations apply:</span></span>
> 
> * <span data-ttu-id="7b4fa-110">Usługi Media Services używa wartości hello hello właściwość IAssetFile.Name podczas kompilowania adresów URL dla hello przesyłania strumieniowego zawartości (na przykład http://{AMSAccount}.origin.mediaservices.windows.net/{GUID}/{IAssetFile.Name}/streamingParameters.) Z tego powodu kodowania procent jest niedozwolone.</span><span class="sxs-lookup"><span data-stu-id="7b4fa-110">Media Services uses hello value of hello IAssetFile.Name property when building URLs for hello streaming content (for example, http://{AMSAccount}.origin.mediaservices.windows.net/{GUID}/{IAssetFile.Name}/streamingParameters.) For this reason, percent-encoding is not allowed.</span></span> <span data-ttu-id="7b4fa-111">Hello wartość hello **nazwa** właściwość nie może mieć jedną z następujących przyczyn hello [procent kodowanie zarezerwowanych znaków](http://en.wikipedia.org/wiki/Percent-encoding#Percent-encoding_reserved_characters):! * "();: @& = + $, /? [] % #".</span><span class="sxs-lookup"><span data-stu-id="7b4fa-111">hello value of hello **Name** property cannot have any of hello following [percent-encoding-reserved characters](http://en.wikipedia.org/wiki/Percent-encoding#Percent-encoding_reserved_characters): !*'();:@&=+$,/?%#[]".</span></span> <span data-ttu-id="7b4fa-112">Ponadto może istnieć tylko jeden "." hello rozszerzenie.</span><span class="sxs-lookup"><span data-stu-id="7b4fa-112">Also, there can only be one '.' for hello file name extension.</span></span>
> * <span data-ttu-id="7b4fa-113">Długość Hello hello nazwy nie może być większa niż 260 znaków.</span><span class="sxs-lookup"><span data-stu-id="7b4fa-113">hello length of hello name should not be greater than 260 characters.</span></span>
> * <span data-ttu-id="7b4fa-114">Brak limitu toohello maksymalny obsługiwany rozmiar pliku do przetwarzania w usłudze Media Services.</span><span class="sxs-lookup"><span data-stu-id="7b4fa-114">There is a limit toohello maximum file size supported for processing in Media Services.</span></span> <span data-ttu-id="7b4fa-115">Zobacz [to](media-services-quotas-and-limitations.md) tematu, aby uzyskać szczegółowe informacje dotyczące limitu rozmiaru pliku hello.</span><span class="sxs-lookup"><span data-stu-id="7b4fa-115">Please see [this](media-services-quotas-and-limitations.md) topic for details about hello file size limitation.</span></span>
> 

<span data-ttu-id="7b4fa-116">Hello podstawowy przepływ pracy do przekazywania zasobów jest podzielona na następujące sekcje hello:</span><span class="sxs-lookup"><span data-stu-id="7b4fa-116">hello basic workflow for uploading Assets is divided into hello following sections:</span></span>

* <span data-ttu-id="7b4fa-117">Utwórz zasób</span><span class="sxs-lookup"><span data-stu-id="7b4fa-117">Create an Asset</span></span>
* <span data-ttu-id="7b4fa-118">Zaszyfrować element zawartości (opcjonalnie)</span><span class="sxs-lookup"><span data-stu-id="7b4fa-118">Encrypt an Asset (Optional)</span></span>
* <span data-ttu-id="7b4fa-119">Przekaż magazynu tooblob plików</span><span class="sxs-lookup"><span data-stu-id="7b4fa-119">Upload a file tooblob storage</span></span>

<span data-ttu-id="7b4fa-120">AMS umożliwia również zasoby tooupload zbiorczo.</span><span class="sxs-lookup"><span data-stu-id="7b4fa-120">AMS also enables you tooupload assets in bulk.</span></span> <span data-ttu-id="7b4fa-121">Więcej informacji znajduje się w [tej](media-services-rest-upload-files.md#upload_in_bulk) sekcji.</span><span class="sxs-lookup"><span data-stu-id="7b4fa-121">For more information, see [this](media-services-rest-upload-files.md#upload_in_bulk) section.</span></span>

> [!NOTE]
> <span data-ttu-id="7b4fa-122">Podczas uzyskiwania dostępu do obiektów w usłudze Media Services, należy ustawić określonych pól nagłówka i wartości w Twoich żądań HTTP.</span><span class="sxs-lookup"><span data-stu-id="7b4fa-122">When accessing entities in Media Services, you must set specific header fields and values in your HTTP requests.</span></span> <span data-ttu-id="7b4fa-123">Aby uzyskać więcej informacji, zobacz [ustawień dla rozwoju interfejsu API REST usługi Media](media-services-rest-how-to-use.md).</span><span class="sxs-lookup"><span data-stu-id="7b4fa-123">For more information, see [Setup for Media Services REST API Development](media-services-rest-how-to-use.md).</span></span>
> 

## <a name="connect-toomedia-services"></a><span data-ttu-id="7b4fa-124">Połączenie usług tooMedia</span><span class="sxs-lookup"><span data-stu-id="7b4fa-124">Connect tooMedia Services</span></span>

<span data-ttu-id="7b4fa-125">Aby uzyskać informacje dotyczące tooconnect toohello AMS interfejsu API, zobacz temat [hello dostępu do interfejsu API usługi Azure Media Services przy użyciu uwierzytelniania usługi Azure AD](media-services-use-aad-auth-to-access-ams-api.md).</span><span class="sxs-lookup"><span data-stu-id="7b4fa-125">For information on how tooconnect toohello AMS API, see [Access hello Azure Media Services API with Azure AD authentication](media-services-use-aad-auth-to-access-ams-api.md).</span></span> 

>[!NOTE]
><span data-ttu-id="7b4fa-126">Po pomyślnym połączeniu toohttps://media.windows.net, otrzymasz 301 przekierowanie, określając inny identyfikator URI usługi multimediów.</span><span class="sxs-lookup"><span data-stu-id="7b4fa-126">After successfully connecting toohttps://media.windows.net, you will receive a 301 redirect specifying another Media Services URI.</span></span> <span data-ttu-id="7b4fa-127">Należy wykonać kolejne wywołania toohello nowy identyfikator URI.</span><span class="sxs-lookup"><span data-stu-id="7b4fa-127">You must make subsequent calls toohello new URI.</span></span>

## <a name="upload-assets"></a><span data-ttu-id="7b4fa-128">Przekaż zasoby</span><span class="sxs-lookup"><span data-stu-id="7b4fa-128">Upload assets</span></span>

### <a name="create-an-asset"></a><span data-ttu-id="7b4fa-129">Utwórz zasób</span><span class="sxs-lookup"><span data-stu-id="7b4fa-129">Create an asset</span></span>

<span data-ttu-id="7b4fa-130">Zasób jest kontenerem dla wielu typów lub zestawów obiektów w usłudze Media Services: wideo, audio, obrazy, kolekcje miniatur, ścieżek tekstu i pliki napisów.</span><span class="sxs-lookup"><span data-stu-id="7b4fa-130">An asset is a container for multiple types or sets of objects in Media Services, including video, audio, images, thumbnail collections, text tracks, and closed caption files.</span></span> <span data-ttu-id="7b4fa-131">W hello interfejsu API REST, tworzenie zasobu wymaga wysyłania POST wysyłanie żądań usług tooMedia i umieszczenie wszelkie informacje o zawartości w treści żądania hello.</span><span class="sxs-lookup"><span data-stu-id="7b4fa-131">In hello REST API, creating an Asset requires sending POST request tooMedia Services and placing any property information about your asset in hello request body.</span></span>

<span data-ttu-id="7b4fa-132">Jedna z właściwości hello, które można określić podczas tworzenia zasobu jest **opcje**.</span><span class="sxs-lookup"><span data-stu-id="7b4fa-132">One of hello properties that you can specify when creating an asset is **Options**.</span></span> <span data-ttu-id="7b4fa-133">**Opcje** jest wartością wyliczenia, który opisuje opcje szyfrowania hello, które można utworzyć zasobu z.</span><span class="sxs-lookup"><span data-stu-id="7b4fa-133">**Options** is an enumeration value that describes hello encryption options that an Asset can be created with.</span></span> <span data-ttu-id="7b4fa-134">Nieprawidłowa wartość jest jedną z wartości hello z poniższej listy hello nie kombinację wartości.</span><span class="sxs-lookup"><span data-stu-id="7b4fa-134">A valid value is one of hello values from hello list below, not a combination of values.</span></span> 

* <span data-ttu-id="7b4fa-135">**Brak** = **0**: szyfrowanie nie będą używane.</span><span class="sxs-lookup"><span data-stu-id="7b4fa-135">**None** = **0**: No encryption will be used.</span></span> <span data-ttu-id="7b4fa-136">Jest to wartość domyślna hello.</span><span class="sxs-lookup"><span data-stu-id="7b4fa-136">This is hello default value.</span></span> <span data-ttu-id="7b4fa-137">Należy pamiętać, że podczas korzystania z tej opcji zawartość nie jest chroniony w trakcie przesyłania lub przechowywania w magazynie.</span><span class="sxs-lookup"><span data-stu-id="7b4fa-137">Note that when using this option your content is not protected in transit or at rest in storage.</span></span>
    <span data-ttu-id="7b4fa-138">Jeśli planujesz toodeliver MP4 przy użyciu pobierania progresywnego, użyj tej opcji.</span><span class="sxs-lookup"><span data-stu-id="7b4fa-138">If you plan toodeliver an MP4 using progressive download, use this option.</span></span> 
* <span data-ttu-id="7b4fa-139">**StorageEncrypted** = **1**: Określ, czy dla Twojego toobe plików zaszyfrowanych za pomocą szyfrowania bitowego AES 256 w celu przekazywania i magazynu.</span><span class="sxs-lookup"><span data-stu-id="7b4fa-139">**StorageEncrypted** = **1**: Specify if you want for your files toobe encrypted with AES-256 bit encryption for upload and storage.</span></span>
  
    <span data-ttu-id="7b4fa-140">Jeśli element zawartości jest szyfrowany w magazynie, należy skonfigurować zasady dostarczania elementu zawartości.</span><span class="sxs-lookup"><span data-stu-id="7b4fa-140">If your asset is storage encrypted, you must configure asset delivery policy.</span></span> <span data-ttu-id="7b4fa-141">Aby uzyskać więcej informacji, zobacz [Konfigurowanie zasad dostarczania elementów zawartości](media-services-rest-configure-asset-delivery-policy.md).</span><span class="sxs-lookup"><span data-stu-id="7b4fa-141">For more information see [Configuring asset delivery policy](media-services-rest-configure-asset-delivery-policy.md).</span></span>
* <span data-ttu-id="7b4fa-142">**CommonEncryptionProtected** = **2**: Określ, czy przekazujesz pliki chronione przy użyciu wspólnej metody szyfrowania (takich jak PlayReady).</span><span class="sxs-lookup"><span data-stu-id="7b4fa-142">**CommonEncryptionProtected** = **2**: Specify if you are uploading files protected with a common encryption method (such as PlayReady).</span></span> 
* <span data-ttu-id="7b4fa-143">**EnvelopeEncryptionProtected** = **4**: Określ, czy przekazujesz HLS zaszyfrowanych z plikami AES.</span><span class="sxs-lookup"><span data-stu-id="7b4fa-143">**EnvelopeEncryptionProtected** = **4**: Specify if you are uploading HLS encrypted with AES files.</span></span> <span data-ttu-id="7b4fa-144">Należy pamiętać, że pliki hello musi zostały zakodowane i zaszyfrowane przez Transform Manager.</span><span class="sxs-lookup"><span data-stu-id="7b4fa-144">Note that hello files must have been encoded and encrypted by Transform Manager.</span></span>

> [!NOTE]
> <span data-ttu-id="7b4fa-145">Jeśli zawartości będzie korzystać z szyfrowania, należy utworzyć **ContentKey** i połączyć ją tooyour zasobów zgodnie z opisem w hello kolejny temat:[jak toocreate ContentKey](media-services-rest-create-contentkey.md).</span><span class="sxs-lookup"><span data-stu-id="7b4fa-145">If your asset will use encryption, you must create a **ContentKey** and link it tooyour asset as described in hello following topic:[How toocreate a ContentKey](media-services-rest-create-contentkey.md).</span></span> <span data-ttu-id="7b4fa-146">Po przekazaniu plików hello do hello zawartości, należy właściwości szyfrowania hello tooupdate na powitania Uwaga **AssetFile** jednostki o wartości hello uzyskano podczas hello **zasobów** szyfrowania.</span><span class="sxs-lookup"><span data-stu-id="7b4fa-146">Note that after you upload hello files into hello asset, you need tooupdate hello encryption properties on hello **AssetFile** entity with hello values you got during hello **Asset** encryption.</span></span> <span data-ttu-id="7b4fa-147">To zrobić za pomocą hello **scalania** żądania HTTP.</span><span class="sxs-lookup"><span data-stu-id="7b4fa-147">Do it by using hello **MERGE** HTTP request.</span></span> 
> 
> 

<span data-ttu-id="7b4fa-148">powitania po przykładzie pokazano, jak toocreate zasób.</span><span class="sxs-lookup"><span data-stu-id="7b4fa-148">hello following example shows how toocreate an asset.</span></span>

<span data-ttu-id="7b4fa-149">**Żądania HTTP**</span><span class="sxs-lookup"><span data-stu-id="7b4fa-149">**HTTP Request**</span></span>

    POST https://media.windows.net/api/Assets HTTP/1.1
    Content-Type: application/json
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amstestaccount001&urn%3aSubscriptionId=z7f09258-6753-2233-b1ae-193798e2c9d8&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1421640053&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=vlG%2fPYdFDMS1zKc36qcFVWnaNh07UCkhYj3B71%2fk1YA%3d
    x-ms-version: 2.11
    Host: media.windows.net

    {"Name":"BigBuckBunny.mp4"}

<span data-ttu-id="7b4fa-150">**Odpowiedź HTTP**</span><span class="sxs-lookup"><span data-stu-id="7b4fa-150">**HTTP Response**</span></span>

<span data-ttu-id="7b4fa-151">W przypadku powodzenia zwrócono hello następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="7b4fa-151">If successful, hello following is returned:</span></span>

    HTP/1.1 201 Created
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
    Strict-Transport-Security: max-age=31536000; includeSubDomains
    Date: Sun, 18 Jan 2015 22:06:40 GMT
    {  
       "odata.metadata":"https://wamsbayclus001rest-hs.cloudapp.net/api/$metadata#Assets/@Element",
       "Id":"nb:cid:UUID:9bc8ff20-24fb-4fdb-9d7c-b04c7ee573a1",
       "State":0,
       "Created":"2015-01-18T22:06:40.6010903Z",
       "LastModified":"2015-01-18T22:06:40.6010903Z",
       "AlternateId":null,
       "Name":"BigBuckBunny.mp4",
       "Options":0,
       "Uri":"https://storagetestaccount001.blob.core.windows.net/asset-9bc8ff20-24fb-4fdb-9d7c-b04c7ee573a1",
       "StorageAccountName":"storagetestaccount001"
    }

### <a name="create-an-assetfile"></a><span data-ttu-id="7b4fa-152">Utwórz AssetFile</span><span class="sxs-lookup"><span data-stu-id="7b4fa-152">Create an AssetFile</span></span>
<span data-ttu-id="7b4fa-153">Witaj [AssetFile](https://docs.microsoft.com/rest/api/media/operations/assetfile) jednostki reprezentuje plik wideo lub audio, który jest przechowywany w kontenerze obiektów blob.</span><span class="sxs-lookup"><span data-stu-id="7b4fa-153">hello [AssetFile](https://docs.microsoft.com/rest/api/media/operations/assetfile) entity represents a video or audio file that is stored in a blob container.</span></span> <span data-ttu-id="7b4fa-154">Plik zasobów zawsze jest skojarzony z zasobem i zasobów może zawierać jeden lub wiele plików zasobów.</span><span class="sxs-lookup"><span data-stu-id="7b4fa-154">An asset file is always associated with an asset, and an asset may contain one or many asset files.</span></span> <span data-ttu-id="7b4fa-155">Witaj Media Encoder usług zadanie nie powiedzie się, jeśli obiekt pliku zasobu nie jest skojarzony z pliku cyfrowego w kontenerze obiektów blob.</span><span class="sxs-lookup"><span data-stu-id="7b4fa-155">hello Media Services Encoder task fails if an asset file object is not associated with a digital file in a blob container.</span></span>

<span data-ttu-id="7b4fa-156">Należy pamiętać, że hello **AssetFile** wystąpienia oraz plik multimedialna hello są dwa różne obiekty.</span><span class="sxs-lookup"><span data-stu-id="7b4fa-156">Note that hello **AssetFile** instance and hello actual media file are two distinct objects.</span></span> <span data-ttu-id="7b4fa-157">wystąpienia AssetFile Hello zawiera metadane dotyczące plików multimedialnych hello, a plik multimedialny hello zawiera zawartość multimedialna hello.</span><span class="sxs-lookup"><span data-stu-id="7b4fa-157">hello AssetFile instance contains metadata about hello media file, while hello media file contains hello actual media content.</span></span>

<span data-ttu-id="7b4fa-158">Po przekazaniu pliku nośnika cyfrowego do kontenera obiektów blob, użyje hello **scalania** żądania HTTP tooupdate hello AssetFile informacje o pliku nośnika (jak pokazano w dalszej części tematu hello).</span><span class="sxs-lookup"><span data-stu-id="7b4fa-158">After you upload your digital media file into a blob container, you will use hello **MERGE** HTTP request tooupdate hello AssetFile with information about your media file (as shown later in hello topic).</span></span> 

<span data-ttu-id="7b4fa-159">**Żądania HTTP**</span><span class="sxs-lookup"><span data-stu-id="7b4fa-159">**HTTP Request**</span></span>

    POST https://media.windows.net/api/Files HTTP/1.1
    Content-Type: application/json
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amstestaccount001&urn%3aSubscriptionId=z7f09258-6753-4ca2-2233-193798e2c9d8&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1421640053&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=vlG%2fPYdFDMS1zKc36qcFVWnaNh07UCkhYj3B71%2fk1YA%3d
    x-ms-version: 2.11
    Host: media.windows.net
    Content-Length: 164

    {  
       "IsEncrypted":"false",
       "IsPrimary":"false",
       "MimeType":"video/mp4",
       "Name":"BigBuckBunny.mp4",
       "ParentAssetId":"nb:cid:UUID:9bc8ff20-24fb-4fdb-9d7c-b04c7ee573a1"
    }

<span data-ttu-id="7b4fa-160">**Odpowiedź HTTP**</span><span class="sxs-lookup"><span data-stu-id="7b4fa-160">**HTTP Response**</span></span>

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

### <a name="creating-hello-accesspolicy-with-write-permission"></a><span data-ttu-id="7b4fa-161">Tworzenie hello AccessPolicy z uprawnieniami do zapisu.</span><span class="sxs-lookup"><span data-stu-id="7b4fa-161">Creating hello AccessPolicy with write permission.</span></span>

>[!NOTE]
><span data-ttu-id="7b4fa-162">Limit różnych zasad usługi AMS wynosi 1 000 000 (na przykład zasad lokalizatorów lub ContentKeyAuthorizationPolicy).</span><span class="sxs-lookup"><span data-stu-id="7b4fa-162">There is a limit of 1,000,000 policies for different AMS policies (for example, for Locator policy or ContentKeyAuthorizationPolicy).</span></span> <span data-ttu-id="7b4fa-163">Należy używać hello tym samym identyfikatorze zasad, jeśli używasz zawsze hello sam dni / dostęp uprawnień, na przykład zasady dla lokalizatorów, które są przeznaczone tooremain w miejscu przez długi czas (zasady — przekazywanie).</span><span class="sxs-lookup"><span data-stu-id="7b4fa-163">You should use hello same policy ID if you are always using hello same days / access permissions, for example, policies for locators that are intended tooremain in place for a long time (non-upload policies).</span></span> <span data-ttu-id="7b4fa-164">Aby uzyskać więcej informacji, zobacz [ten](media-services-dotnet-manage-entities.md#limit-access-policies) temat.</span><span class="sxs-lookup"><span data-stu-id="7b4fa-164">For more information, see [this](media-services-dotnet-manage-entities.md#limit-access-policies) topic.</span></span>

<span data-ttu-id="7b4fa-165">Przed przekazaniem żadnych plików do magazynu obiektów blob, należy ustawić dostępu hello zasad praw do pisania tooan zasobów.</span><span class="sxs-lookup"><span data-stu-id="7b4fa-165">Before uploading any files into blob storage, set hello access policy rights for writing tooan asset.</span></span> <span data-ttu-id="7b4fa-166">Ustaw toodo, który po toohello żądania HTTP AccessPolicies jednostki.</span><span class="sxs-lookup"><span data-stu-id="7b4fa-166">toodo that, POST an HTTP request toohello AccessPolicies entity set.</span></span> <span data-ttu-id="7b4fa-167">Zdefiniuj wartość DurationInMinutes po utworzeniu lub otrzymasz komunikat o błędzie 500 wewnętrzny serwer w odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="7b4fa-167">Define a DurationInMinutes value upon creation or you will receive a 500 Internal Server error message back in response.</span></span> <span data-ttu-id="7b4fa-168">Aby uzyskać więcej informacji o AccessPolicies, zobacz [AccessPolicy](https://docs.microsoft.com/rest/api/media/operations/accesspolicy).</span><span class="sxs-lookup"><span data-stu-id="7b4fa-168">For more information on AccessPolicies, see [AccessPolicy](https://docs.microsoft.com/rest/api/media/operations/accesspolicy).</span></span>

<span data-ttu-id="7b4fa-169">powitania po przykładzie pokazano, jak toocreate AccessPolicy:</span><span class="sxs-lookup"><span data-stu-id="7b4fa-169">hello following example shows how toocreate an AccessPolicy:</span></span>

<span data-ttu-id="7b4fa-170">**Żądania HTTP**</span><span class="sxs-lookup"><span data-stu-id="7b4fa-170">**HTTP Request**</span></span>

    POST https://media.windows.net/api/AccessPolicies HTTP/1.1
    Content-Type: application/json
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amstestaccount001&urn%3aSubscriptionId=z7f09258-6753-2233-b1ae-193798e2c9d8&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1421640053&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=vlG%2fPYdFDMS1zKc36qcFVWnaNh07UCkhYj3B71%2fk1YA%3d
    x-ms-version: 2.11
    Host: media.windows.net

    {"Name":"NewUploadPolicy", "DurationInMinutes":"440", "Permissions":"2"} 

<span data-ttu-id="7b4fa-171">**Żądania HTTP**</span><span class="sxs-lookup"><span data-stu-id="7b4fa-171">**HTTP Request**</span></span>

    If successful, hello following response is returned:

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

### <a name="get-hello-upload-url"></a><span data-ttu-id="7b4fa-172">Pobierz hello przekazać adres URL</span><span class="sxs-lookup"><span data-stu-id="7b4fa-172">Get hello Upload URL</span></span>
<span data-ttu-id="7b4fa-173">tooreceive hello przekazywania rzeczywisty adres URL, tworzenie lokalizatora SAS.</span><span class="sxs-lookup"><span data-stu-id="7b4fa-173">tooreceive hello actual upload URL, create a SAS Locator.</span></span> <span data-ttu-id="7b4fa-174">Lokalizatory zdefiniuj hello czas rozpoczęcia i typ punktu końcowego połączenia dla klientów, którzy mają tooaccess plików zasobów.</span><span class="sxs-lookup"><span data-stu-id="7b4fa-174">Locators define hello start time and type of connection endpoint for clients that want tooaccess Files in an Asset.</span></span> <span data-ttu-id="7b4fa-175">Można utworzyć wiele jednostek lokalizatora dla danego AccessPolicy i zasobów pary toohandle innego klienta żądań i potrzeb.</span><span class="sxs-lookup"><span data-stu-id="7b4fa-175">You can create multiple Locator entities for a given AccessPolicy and Asset pair toohandle different client requests and needs.</span></span> <span data-ttu-id="7b4fa-176">Każdy z tych lokalizatorów Użyj wartości StartTime hello plus wartość DurationInMinutes hello hello AccessPolicy toodetermine hello długość czasu, można użyć adresu URL.</span><span class="sxs-lookup"><span data-stu-id="7b4fa-176">Each of these Locators use hello StartTime value plus hello DurationInMinutes value of hello AccessPolicy toodetermine hello length of time a URL can be used.</span></span> <span data-ttu-id="7b4fa-177">Aby uzyskać więcej informacji, zobacz [lokalizatora](https://docs.microsoft.com/rest/api/media/operations/locator).</span><span class="sxs-lookup"><span data-stu-id="7b4fa-177">For more information, see [Locator](https://docs.microsoft.com/rest/api/media/operations/locator).</span></span>

<span data-ttu-id="7b4fa-178">Adres URL SAS ma hello następującego formatu:</span><span class="sxs-lookup"><span data-stu-id="7b4fa-178">A SAS URL has hello following format:</span></span>

    {https://myaccount.blob.core.windows.net}/{asset name}/{video file name}?{SAS signature}

<span data-ttu-id="7b4fa-179">Zagadnienia do rozważenia:</span><span class="sxs-lookup"><span data-stu-id="7b4fa-179">Some considerations apply:</span></span>

* <span data-ttu-id="7b4fa-180">Nie może mieć więcej niż pięć lokalizatorów unikatowy skojarzone z danym zawartości w tym samym czasie.</span><span class="sxs-lookup"><span data-stu-id="7b4fa-180">You cannot have more than five unique Locators associated with a given Asset at one time.</span></span> <span data-ttu-id="7b4fa-181">Aby uzyskać więcej informacji zobacz lokalizatora.</span><span class="sxs-lookup"><span data-stu-id="7b4fa-181">For more information, see Locator.</span></span>
* <span data-ttu-id="7b4fa-182">Tooupload plików natychmiast, należy należy ustawić Twojej StartTime wartość toofive minut przed hello bieżącego czasu.</span><span class="sxs-lookup"><span data-stu-id="7b4fa-182">If you need tooupload your files immediately, you should set your StartTime value toofive minutes before hello current time.</span></span> <span data-ttu-id="7b4fa-183">Jest to spowodowane mogą istnieć zegara pochylenia między komputer klienta i usługi Media Services.</span><span class="sxs-lookup"><span data-stu-id="7b4fa-183">This is because there may be clock skew between your client machine and Media Services.</span></span> <span data-ttu-id="7b4fa-184">Ponadto wartość StartTime musi być w powitania po formacie daty/godziny: RRRR-MM-ddtgg (na przykład "2014-05-23T17:53:50Z").</span><span class="sxs-lookup"><span data-stu-id="7b4fa-184">Also, your StartTime value must be in hello following DateTime format: YYYY-MM-DDTHH:mm:ssZ (for example, "2014-05-23T17:53:50Z").</span></span>    
* <span data-ttu-id="7b4fa-185">Może być 30 40 sekund opóźnienia po utworzeniu lokalizatora toowhen nie jest dostępny do użycia.</span><span class="sxs-lookup"><span data-stu-id="7b4fa-185">There may be a 30-40 second delay after a Locator is created toowhen it is available for use.</span></span> <span data-ttu-id="7b4fa-186">Ten problem dotyczy tooboth adres URL SAS oraz Lokalizatory pochodzenia.</span><span class="sxs-lookup"><span data-stu-id="7b4fa-186">This issue applies tooboth SAS URL and Origin Locators.</span></span>

<span data-ttu-id="7b4fa-187">Witaj poniższy przykład pokazuje, jak toocreate lokalizatora adres URL SAS, zgodnie z definicją hello właściwości typu w treści żądania hello ("1" dla lokalizatora SAS) i "2" dla lokalizatora pochodzenia na żądanie.</span><span class="sxs-lookup"><span data-stu-id="7b4fa-187">hello following example shows how toocreate a SAS URL Locator, as defined by hello Type property in hello request body ("1" for a SAS locator and "2" for an On-Demand origin locator).</span></span> <span data-ttu-id="7b4fa-188">Witaj **ścieżki** właściwości zwróconej zawiera adres URL hello, że należy używać tooupload Twojego pliku.</span><span class="sxs-lookup"><span data-stu-id="7b4fa-188">hello **Path** property returned contains hello URL that you must use tooupload your file.</span></span>

<span data-ttu-id="7b4fa-189">**Żądania HTTP**</span><span class="sxs-lookup"><span data-stu-id="7b4fa-189">**HTTP Request**</span></span>

    POST https://media.windows.net/api/Locators HTTP/1.1
    Content-Type: application/json
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amstestaccount001&urn%3aSubscriptionId=z7f09258-6753-4ca2-2233-193798e2c9d8&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1421640053&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=vlG%2fPYdFDMS1zKc36qcFVWnaNh07UCkhYj3B71%2fk1YA%3d
    x-ms-version: 2.11
    Host: media.windows.net
    {  
       "AccessPolicyId":"nb:pid:UUID:be0ac48d-af7d-4877-9d60-1805d68bffae",
       "AssetId":"nb:cid:UUID:9bc8ff20-24fb-4fdb-9d7c-b04c7ee573a1",
       "StartTime":"2015-02-18T16:45:53",
       "Type":1
    }

<span data-ttu-id="7b4fa-190">**Odpowiedź HTTP**</span><span class="sxs-lookup"><span data-stu-id="7b4fa-190">**HTTP Response**</span></span>

<span data-ttu-id="7b4fa-191">W przypadku powodzenia powitania po odpowiedzi jest zwracany:</span><span class="sxs-lookup"><span data-stu-id="7b4fa-191">If successful, hello following response is returned:</span></span>

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

### <a name="upload-a-file-into-a-blob-storage-container"></a><span data-ttu-id="7b4fa-192">Przekazywanie pliku do kontenera magazynu obiektów blob</span><span class="sxs-lookup"><span data-stu-id="7b4fa-192">Upload a file into a blob storage container</span></span>
<span data-ttu-id="7b4fa-193">Po utworzeniu hello AccessPolicy i lokalizatora zestawu hello rzeczywisty plik jest przekazane tooan kontenera magazynu obiektów Blob Azure przy użyciu hello interfejsów API REST magazynu Azure.</span><span class="sxs-lookup"><span data-stu-id="7b4fa-193">Once you have hello AccessPolicy and Locator set, hello actual file is uploaded tooan Azure Blob Storage container using hello Azure Storage REST APIs.</span></span> <span data-ttu-id="7b4fa-194">Należy przekazać pliki hello jako blokowych obiektów blob.</span><span class="sxs-lookup"><span data-stu-id="7b4fa-194">You must upload hello files as block blobs.</span></span> <span data-ttu-id="7b4fa-195">Stronicowe obiekty BLOB nie są obsługiwane przez usługi Azure Media Services.</span><span class="sxs-lookup"><span data-stu-id="7b4fa-195">Page blobs are not supported by Azure Media Services.</span></span>  

> [!NOTE]
> <span data-ttu-id="7b4fa-196">Należy dodać nazwę pliku hello pliku hello ma toohello tooupload lokalizatora **ścieżki** odebrana w poprzedniej sekcji hello wartość.</span><span class="sxs-lookup"><span data-stu-id="7b4fa-196">You must add hello file name for hello file you want tooupload toohello Locator **Path** value received in hello previous section.</span></span> <span data-ttu-id="7b4fa-197">Na przykład https://storagetestaccount001.blob.core.windows.net/asset-e7b02da4-5a69-40e7-a8db-e8f4f697aac0/BigBuckBunny.mp4?</span><span class="sxs-lookup"><span data-stu-id="7b4fa-197">For example, https://storagetestaccount001.blob.core.windows.net/asset-e7b02da4-5a69-40e7-a8db-e8f4f697aac0/BigBuckBunny.mp4?</span></span> <span data-ttu-id="7b4fa-198">.</span><span class="sxs-lookup"><span data-stu-id="7b4fa-198">.</span></span> <span data-ttu-id="7b4fa-199">.</span><span class="sxs-lookup"><span data-stu-id="7b4fa-199">.</span></span> <span data-ttu-id="7b4fa-200">.</span><span class="sxs-lookup"><span data-stu-id="7b4fa-200">.</span></span> 
> 
> 

<span data-ttu-id="7b4fa-201">Aby uzyskać więcej informacji na temat pracy z obiektami blob magazynu Azure, zobacz [interfejsu API REST usługi Blob](https://docs.microsoft.com/rest/api/storageservices/Blob-Service-REST-API).</span><span class="sxs-lookup"><span data-stu-id="7b4fa-201">For more information on working with Azure storage blobs, see [Blob Service REST API](https://docs.microsoft.com/rest/api/storageservices/Blob-Service-REST-API).</span></span>

### <a name="update-hello-assetfile"></a><span data-ttu-id="7b4fa-202">Aktualizacja hello AssetFile</span><span class="sxs-lookup"><span data-stu-id="7b4fa-202">Update hello AssetFile</span></span>
<span data-ttu-id="7b4fa-203">Teraz, przekazywanego pliku, zaktualizuj hello FileAsset rozmiarze (i innych) informacje.</span><span class="sxs-lookup"><span data-stu-id="7b4fa-203">Now that you've uploaded your file, update hello FileAsset size (and other) information.</span></span> <span data-ttu-id="7b4fa-204">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="7b4fa-204">For example:</span></span>

    MERGE https://media.windows.net/api/Files('nb%3Acid%3AUUID%3Af13a0137-0a62-9d4c-b3b9-ca944b5142c5') HTTP/1.1
    Content-Type: application/json
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amstestaccount001&urn%3aSubscriptionId=z7f09258-6753-4ca2-2233-193798e2c9d8&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1421662918&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=utmoXXbm9Q7j4tW1yJuMVA3egRiQy5FPygwadkmPeaY%3d
    x-ms-version: 2.11
    Host: media.windows.net

    {  
       "ContentFileSize":"1186540",
       "Id":"nb:cid:UUID:f13a0137-0a62-9d4c-b3b9-ca944b5142c5",
       "MimeType":"video/mp4",
       "Name":"BigBuckBunny.mp4",
       "ParentAssetId":"nb:cid:UUID:9bc8ff20-24fb-4fdb-9d7c-b04c7ee573a1"
    }


<span data-ttu-id="7b4fa-205">**Odpowiedź HTTP**</span><span class="sxs-lookup"><span data-stu-id="7b4fa-205">**HTTP Response**</span></span>

<span data-ttu-id="7b4fa-206">W przypadku powodzenia poniżej hello jest zwracana: HTTP/1.1 204 nr zawartości</span><span class="sxs-lookup"><span data-stu-id="7b4fa-206">If successful, hello following is returned: HTTP/1.1 204 No Content</span></span>

### <a name="delete-hello-locator-and-accesspolicy"></a><span data-ttu-id="7b4fa-207">Usuń hello lokalizatora i AccessPolicy</span><span class="sxs-lookup"><span data-stu-id="7b4fa-207">Delete hello Locator and AccessPolicy</span></span>
<span data-ttu-id="7b4fa-208">**Żądania HTTP**</span><span class="sxs-lookup"><span data-stu-id="7b4fa-208">**HTTP Request**</span></span>

    DELETE https://media.windows.net/api/Locators('nb%3Alid%3AUUID%3Aaf57bdd8-6751-4e84-b403-f3c140444b54') HTTP/1.1
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amstestaccount001&urn%3aSubscriptionId=z7f09258-6753-2233-b1ae-193798e2c9d8&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1421662918&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=utmoXXbm9Q7j4tW1yJuMVA3egRiQy5FPygwadkmPeaY%3d
    x-ms-version: 2.11
    Host: media.windows.net

<span data-ttu-id="7b4fa-209">**Odpowiedź HTTP**</span><span class="sxs-lookup"><span data-stu-id="7b4fa-209">**HTTP Response**</span></span>

<span data-ttu-id="7b4fa-210">W przypadku powodzenia zwrócono hello następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="7b4fa-210">If successful, hello following is returned:</span></span>

    HTTP/1.1 204 No Content 
    ...

<span data-ttu-id="7b4fa-211">**Żądania HTTP**</span><span class="sxs-lookup"><span data-stu-id="7b4fa-211">**HTTP Request**</span></span>

    DELETE https://media.windows.net/api/AccessPolicies('nb%3Apid%3AUUID%3Abe0ac48d-af7d-4877-9d60-1805d68bffae') HTTP/1.1
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amstestaccount001&urn%3aSubscriptionId=z7f09258-6753-2233-b1ae-193798e2c9d8&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1421662918&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=utmoXXbm9Q7j4tW1yJuMVA3egRiQy5FPygwadkmPeaY%3d
    x-ms-version: 2.11
    Host: media.windows.net

<span data-ttu-id="7b4fa-212">**Odpowiedź HTTP**</span><span class="sxs-lookup"><span data-stu-id="7b4fa-212">**HTTP Response**</span></span>

<span data-ttu-id="7b4fa-213">W przypadku powodzenia zwrócono hello następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="7b4fa-213">If successful, hello following is returned:</span></span>

    HTTP/1.1 204 No Content 
    ...

## <span data-ttu-id="7b4fa-214"><a id="upload_in_bulk"></a>Przekaż zasoby zbiorcze</span><span class="sxs-lookup"><span data-stu-id="7b4fa-214"><a id="upload_in_bulk"></a>Upload assets in bulk</span></span>
### <a name="create-hello-ingestmanifest"></a><span data-ttu-id="7b4fa-215">Utwórz hello IngestManifest</span><span class="sxs-lookup"><span data-stu-id="7b4fa-215">Create hello IngestManifest</span></span>
<span data-ttu-id="7b4fa-216">Witaj IngestManifest to kontener dla zestawu zasobów, pliki zasobów i informacji statystycznych, które mogą być używane toodetermine hello postęp zbiorczego wprowadzania hello zestawu.</span><span class="sxs-lookup"><span data-stu-id="7b4fa-216">hello IngestManifest is a container for a set of assets, asset files, and statistic information that can be used toodetermine hello progress of bulk ingesting for hello set.</span></span>

<span data-ttu-id="7b4fa-217">**Żądania HTTP**</span><span class="sxs-lookup"><span data-stu-id="7b4fa-217">**HTTP Request**</span></span>

    POST https:// media.windows.net/API/IngestManifests HTTP/1.1
    Content-Type: application/json;odata=verbose
    Accept: application/json;odata=verbose
    DataServiceVersion: 3.0
    MaxDataServiceVersion: 3.0
    x-ms-version: 2.11
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=070500D0-F35C-4A5A-9249-485BBF4EC70B&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1334275521&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=GxdBb%2fmEyN7iHdNxbawawHRftLhPFFqxX1JZckuv3hY%3d
    Host: media.windows.net
    Content-Length: 36
    Expect: 100-continue

    { "Name" : "ExampleManifestREST" }

### <a name="create-assets"></a><span data-ttu-id="7b4fa-218">Utwórz zasoby</span><span class="sxs-lookup"><span data-stu-id="7b4fa-218">Create assets</span></span>
<span data-ttu-id="7b4fa-219">Przed utworzeniem hello IngestManifestAsset, należy hello toocreate zawartości, który będzie można wykonać przy użyciu wprowadzania zbiorczego.</span><span class="sxs-lookup"><span data-stu-id="7b4fa-219">Before creating hello IngestManifestAsset, you need toocreate hello Asset that will be completed using bulk ingesting.</span></span> <span data-ttu-id="7b4fa-220">Zasób jest kontenerem dla wielu typów lub zestawów obiektów w usłudze Media Services: wideo, audio, obrazy, kolekcje miniatur, ścieżek tekstu i pliki napisów.</span><span class="sxs-lookup"><span data-stu-id="7b4fa-220">An asset is a container for multiple types or sets of objects in Media Services, including video, audio, images, thumbnail collections, text tracks, and closed caption files.</span></span> <span data-ttu-id="7b4fa-221">W hello interfejsu API REST tworzenie zasobu wymaga wysyłania tooMicrosoft żądania HTTP POST usługi Azure Media Services i umieszczenie wszelkie informacje o zawartości w treści żądania hello. W tym przykładzie hello zasobów jest tworzony przy użyciu opcji StorageEncrption(1) hello dołączonego hello treści żądania.</span><span class="sxs-lookup"><span data-stu-id="7b4fa-221">In hello REST API, creating an Asset requires sending a HTTP POST request tooMicrosoft Azure Media Services and placing any property information about your asset in hello request body.In this example, hello Asset is created using hello StorageEncrption(1) option included with hello request body.</span></span>

<span data-ttu-id="7b4fa-222">**Odpowiedź HTTP**</span><span class="sxs-lookup"><span data-stu-id="7b4fa-222">**HTTP Response**</span></span>

    POST https://media.windows.net/API/Assets HTTP/1.1
    Content-Type: application/json;odata=verbose
    Accept: application/json;odata=verbose
    DataServiceVersion: 3.0
    MaxDataServiceVersion: 3.0
    x-ms-version: 2.11
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=070500D0-F35C-4A5A-9249-485BBF4EC70B&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1334275521&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=GxdBb%2fmEyN7iHdNxbawawHRftLhPFFqxX1JZckuv3hY%3d
    Host: media.windows.net
    Content-Length: 55
    Expect: 100-continue

    { "Name" : "ExampleManifestREST_Asset", "Options" : 1 }

### <a name="create-hello-ingestmanifestassets"></a><span data-ttu-id="7b4fa-223">Utwórz hello IngestManifestAssets</span><span class="sxs-lookup"><span data-stu-id="7b4fa-223">Create hello IngestManifestAssets</span></span>
<span data-ttu-id="7b4fa-224">IngestManifestAssets reprezentują zasobów w ramach IngestManifest, które są używane z wprowadzania zbiorczego.</span><span class="sxs-lookup"><span data-stu-id="7b4fa-224">IngestManifestAssets represent Assets within an IngestManifest that are used with bulk ingesting.</span></span> <span data-ttu-id="7b4fa-225">Witaj zasadniczo łącze hello zasobów toohello manifestu.</span><span class="sxs-lookup"><span data-stu-id="7b4fa-225">hello basically link hello asset toohello manifest.</span></span> <span data-ttu-id="7b4fa-226">Usługa Azure Media Services Obserwujący wewnętrznie przekazywania pliku hello oparte na IngestManifestFiles kolekcję skojarzoną toohello IngestManifestAsset.</span><span class="sxs-lookup"><span data-stu-id="7b4fa-226">Azure Media Services watches internally for hello file upload based on IngestManifestFiles collection associated toohello IngestManifestAsset.</span></span> <span data-ttu-id="7b4fa-227">Po przekazaniu tych plików zasobów hello jest ukończona.</span><span class="sxs-lookup"><span data-stu-id="7b4fa-227">Once these files are uploaded, hello asset is completed.</span></span> <span data-ttu-id="7b4fa-228">Możesz utworzyć nowe IngestManifestAsset z żądaniem HTTP POST.</span><span class="sxs-lookup"><span data-stu-id="7b4fa-228">You can create a new IngestManifestAsset with a HTTP POST request.</span></span> <span data-ttu-id="7b4fa-229">W treści żądania hello obejmują hello identyfikator IngestManifest i hello identyfikator zasobów tego powitalne IngestManifestAsset należy połączyć ze sobą służy do wprowadzania zbiorczego.</span><span class="sxs-lookup"><span data-stu-id="7b4fa-229">In hello request body, include hello IngestManifest Id and hello Asset Id that hello IngestManifestAsset should link together for bulk ingesting.</span></span>

<span data-ttu-id="7b4fa-230">**Odpowiedź HTTP**</span><span class="sxs-lookup"><span data-stu-id="7b4fa-230">**HTTP Response**</span></span>

    POST https://media.windows.net/API/IngestManifestAssets HTTP/1.1
    Content-Type: application/json;odata=verbose
    Accept: application/json;odata=verbose
    DataServiceVersion: 3.0
    MaxDataServiceVersion: 3.0
    x-ms-version: 2.11
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=070500D0-F35C-4A5A-9249-485BBF4EC70B&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1334275521&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=GxdBb%2fmEyN7iHdNxbawawHRftLhPFFqxX1JZckuv3hY%3d
    Host: media.windows.net
    Content-Length: 152
    Expect: 100-continue
    { "ParentIngestManifestId" : "nb:mid:UUID:5c77f186-414f-8b48-8231-17f9264e2048", "Asset" : { "Id" : "nb:cid:UUID:b757929a-5a57-430b-b33e-c05c6cbef02e"}}


### <a name="create-hello-ingestmanifestfiles-for-each-asset"></a><span data-ttu-id="7b4fa-231">Utwórz hello IngestManifestFiles dla każdego zasobu</span><span class="sxs-lookup"><span data-stu-id="7b4fa-231">Create hello IngestManifestFiles for each Asset</span></span>
<span data-ttu-id="7b4fa-232">IngestManifestFile reprezentuje obiekt rzeczywistego obiektu blob wideo lub audio, który zostanie przekazany jako część zbiorczego wprowadzania dla zasobu.</span><span class="sxs-lookup"><span data-stu-id="7b4fa-232">An IngestManifestFile represents an actual video or audio blob object that will be uploaded as part of bulk ingesting for an asset.</span></span> <span data-ttu-id="7b4fa-233">Właściwości nie są wymagane, chyba że zasobów hello jest przy użyciu opcji szyfrowania związanych z szyfrowania.</span><span class="sxs-lookup"><span data-stu-id="7b4fa-233">Encryption related properties are not required unless hello asset is using an encryption option.</span></span> <span data-ttu-id="7b4fa-234">przykład Witaj w tej sekcji przedstawiono tworzenie IngestManifestFile, który używa StorageEncryption hello wcześniej utworzone zasobów.</span><span class="sxs-lookup"><span data-stu-id="7b4fa-234">hello example used in this section demonstrates creating an IngestManifestFile that uses StorageEncryption for hello Asset previously created.</span></span>

<span data-ttu-id="7b4fa-235">**Odpowiedź HTTP**</span><span class="sxs-lookup"><span data-stu-id="7b4fa-235">**HTTP Response**</span></span>

    POST https://media.windows.net/API/IngestManifestFiles HTTP/1.1
    Content-Type: application/json;odata=verbose
    Accept: application/json;odata=verbose
    DataServiceVersion: 3.0
    MaxDataServiceVersion: 3.0
    x-ms-version: 2.11
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=070500D0-F35C-4A5A-9249-485BBF4EC70B&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1334275521&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=GxdBb%2fmEyN7iHdNxbawawHRftLhPFFqxX1JZckuv3hY%3d
    Host: media.windows.net
    Content-Length: 367
    Expect: 100-continue

    { "Name" : "REST_Example_File.wmv", "ParentIngestManifestId" : "nb:mid:UUID:5c77f186-414f-8b48-8231-17f9264e2048", "ParentIngestManifestAssetId" : "nb:maid:UUID:beed8531-9a03-9043-b1d8-6a6d1044cdda", "IsEncrypted" : "true", "EncryptionScheme" : "StorageEncryption", "EncryptionVersion" : "1.0", "EncryptionKeyId" : "nb:kid:UUID:32e6efaf-5fba-4538-b115-9d1cefe43510" }

### <a name="upload-hello-files-tooblob-storage"></a><span data-ttu-id="7b4fa-236">Przekaż hello tooBlob plików magazynu</span><span class="sxs-lookup"><span data-stu-id="7b4fa-236">Upload hello Files tooBlob Storage</span></span>
<span data-ttu-id="7b4fa-237">Możesz użyć dowolnej aplikacji klienckiej szybkich możliwość przekazywania hello zasobów plików toohello kontenera magazynu obiektów blob dostarczonego przez hello BlobStorageUriForUpload właściwość hello IngestManifest identyfikatora Uri.</span><span class="sxs-lookup"><span data-stu-id="7b4fa-237">You can use any high speed client application capable of uploading hello asset files toohello blob storage container Uri provided by hello BlobStorageUriForUpload property of hello IngestManifest.</span></span> <span data-ttu-id="7b4fa-238">Co Usługa przekazywania zauważalne szybkich [Aspera na żądanie dla aplikacji Azure](http://go.microsoft.com/fwlink/?LinkId=272001).</span><span class="sxs-lookup"><span data-stu-id="7b4fa-238">One notable high speed upload service is [Aspera On Demand for Azure Application](http://go.microsoft.com/fwlink/?LinkId=272001).</span></span>

### <a name="monitor-bulk-ingest-progress"></a><span data-ttu-id="7b4fa-239">Monitor zbiorczego pozyskiwania postępu</span><span class="sxs-lookup"><span data-stu-id="7b4fa-239">Monitor Bulk Ingest Progress</span></span>
<span data-ttu-id="7b4fa-240">Można monitorować postęp hello zbiorczego wprowadzania operacje IngestManifest Sondując właściwość statystyki hello hello IngestManifest.</span><span class="sxs-lookup"><span data-stu-id="7b4fa-240">You can monitor hello progress of bulk ingesting operations for an IngestManifest by polling hello Statistics property of hello IngestManifest.</span></span> <span data-ttu-id="7b4fa-241">Czy właściwość jest typem złożonym [IngestManifestStatistics](https://docs.microsoft.com/rest/api/media/operations/ingestmanifeststatistics).</span><span class="sxs-lookup"><span data-stu-id="7b4fa-241">That property is a complex type, [IngestManifestStatistics](https://docs.microsoft.com/rest/api/media/operations/ingestmanifeststatistics).</span></span> <span data-ttu-id="7b4fa-242">toopoll hello właściwości statystyki przesłać żądanie HTTP GET przekazywanie hello IngestManifest identyfikatora.</span><span class="sxs-lookup"><span data-stu-id="7b4fa-242">toopoll hello Statistics property, submit a HTTP GET request passing hello IngestManifest Id.</span></span>

## <a name="create-contentkeys-used-for-encryption"></a><span data-ttu-id="7b4fa-243">Utwórz ContentKeys używany do szyfrowania</span><span class="sxs-lookup"><span data-stu-id="7b4fa-243">Create ContentKeys used for encryption</span></span>
<span data-ttu-id="7b4fa-244">Jeśli zawartości będzie używać szyfrowania, należy utworzyć toobe ContentKey hello używany do szyfrowania przed utworzeniem hello plików zasobów.</span><span class="sxs-lookup"><span data-stu-id="7b4fa-244">If your asset will use encryption, you must create hello ContentKey toobe used for encryption before creating hello asset files.</span></span> <span data-ttu-id="7b4fa-245">Do szyfrowania magazynu hello powinny znajdować się następujące właściwości w treści żądania hello.</span><span class="sxs-lookup"><span data-stu-id="7b4fa-245">For storage encryption, hello following properties should be included in hello request body.</span></span>

| <span data-ttu-id="7b4fa-246">Właściwość treść żądania</span><span class="sxs-lookup"><span data-stu-id="7b4fa-246">Request body property</span></span> | <span data-ttu-id="7b4fa-247">Opis</span><span class="sxs-lookup"><span data-stu-id="7b4fa-247">Description</span></span> |
| --- | --- |
| <span data-ttu-id="7b4fa-248">Identyfikator</span><span class="sxs-lookup"><span data-stu-id="7b4fa-248">Id</span></span> |<span data-ttu-id="7b4fa-249">Hello ContentKey identyfikator, który mamy Generowanie nad powitania po użyciu formatu, "nb:kid:UUID:<NEW GUID>".</span><span class="sxs-lookup"><span data-stu-id="7b4fa-249">hello ContentKey Id which we generate ourselves using hello following format, “nb:kid:UUID:<NEW GUID>”.</span></span> |
| <span data-ttu-id="7b4fa-250">ContentKeyType</span><span class="sxs-lookup"><span data-stu-id="7b4fa-250">ContentKeyType</span></span> |<span data-ttu-id="7b4fa-251">Typ klucza zawartości hello jest jako liczba całkowita dla tego klucza zawartości.</span><span class="sxs-lookup"><span data-stu-id="7b4fa-251">This is hello content key type as an integer for this content key.</span></span> <span data-ttu-id="7b4fa-252">Wartość hello 1 szyfrowania magazynu jest przekazywana.</span><span class="sxs-lookup"><span data-stu-id="7b4fa-252">We pass hello value 1 for storage encryption.</span></span> |
| <span data-ttu-id="7b4fa-253">EncryptedContentKey</span><span class="sxs-lookup"><span data-stu-id="7b4fa-253">EncryptedContentKey</span></span> |<span data-ttu-id="7b4fa-254">Utworzymy nową wartość klucza zawartości, która jest wartością 256-bitowego (32 bajtów).</span><span class="sxs-lookup"><span data-stu-id="7b4fa-254">We create a new content key value which is a 256-bit (32 byte) value.</span></span> <span data-ttu-id="7b4fa-255">klucz Hello jest szyfrowana przy użyciu certyfikatu X.509 szyfrowania magazynu hello, którego możemy pobrać Microsoft Azure Media Services, wykonując żądanie HTTP GET dla hello GetProtectionKeyId i metod GetProtectionKey.</span><span class="sxs-lookup"><span data-stu-id="7b4fa-255">hello key is encrypted using hello storage encryption X.509 certificate which we retrieve from Microsoft Azure Media Services by executing a HTTP GET request for hello GetProtectionKeyId and GetProtectionKey Methods.</span></span> |
| <span data-ttu-id="7b4fa-256">ProtectionKeyId</span><span class="sxs-lookup"><span data-stu-id="7b4fa-256">ProtectionKeyId</span></span> |<span data-ttu-id="7b4fa-257">To jest hello ochrony identyfikator klucza certyfikatu X.509 szyfrowania magazynu hello, który był używany tooencrypt naszych klucz zawartości.</span><span class="sxs-lookup"><span data-stu-id="7b4fa-257">This is hello protection key id for hello storage encryption X.509 certificate that was used tooencrypt our content key.</span></span> |
| <span data-ttu-id="7b4fa-258">ProtectionKeyType</span><span class="sxs-lookup"><span data-stu-id="7b4fa-258">ProtectionKeyType</span></span> |<span data-ttu-id="7b4fa-259">Jest to typ szyfrowania hello hello ochrony klucza, który był używany tooencrypt hello zawartości klucz.</span><span class="sxs-lookup"><span data-stu-id="7b4fa-259">This is hello encryption type for hello protection key that was used tooencrypt hello content key.</span></span> <span data-ttu-id="7b4fa-260">Ta wartość jest StorageEncryption(1) w naszym przykładzie.</span><span class="sxs-lookup"><span data-stu-id="7b4fa-260">This value is StorageEncryption(1) for our example.</span></span> |
| <span data-ttu-id="7b4fa-261">Sumy kontrolnej</span><span class="sxs-lookup"><span data-stu-id="7b4fa-261">Checksum</span></span> |<span data-ttu-id="7b4fa-262">Witaj MD5 obliczeniowej sumy kontrolnej dla hello klucz zawartości.</span><span class="sxs-lookup"><span data-stu-id="7b4fa-262">hello MD5 calculated checksum for hello content key.</span></span> <span data-ttu-id="7b4fa-263">Jest ona obliczana przez szyfrowanie hello identyfikatora zawartości z hello klucz zawartości.</span><span class="sxs-lookup"><span data-stu-id="7b4fa-263">It is computed by encrypting hello content Id with hello content key.</span></span> <span data-ttu-id="7b4fa-264">Witaj przykładowy kod pokazuje, jak toocalculate hello sumy kontrolnej.</span><span class="sxs-lookup"><span data-stu-id="7b4fa-264">hello example code demonstrates how toocalculate hello checksum.</span></span> |

<span data-ttu-id="7b4fa-265">**Odpowiedź HTTP**</span><span class="sxs-lookup"><span data-stu-id="7b4fa-265">**HTTP Response**</span></span>

    POST https://media.windows.net/api/ContentKeys HTTP/1.1
    Content-Type: application/json;odata=verbose
    Accept: application/json;odata=verbose
    DataServiceVersion: 3.0
    MaxDataServiceVersion: 3.0
    x-ms-version: 2.11
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=070500D0-F35C-4A5A-9249-485BBF4EC70B&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1334275521&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=GxdBb%2fmEyN7iHdNxbawawHRftLhPFFqxX1JZckuv3hY%3d
    Host: media.windows.net
    Content-Length: 572
    Expect: 100-continue

    {"Id" : "nb:kid:UUID:316d14d4-b603-4d90-b8db-0fede8aa48f8", "ContentKeyType" : 1, "EncryptedContentKey" : "Y4NPej7heOFa2vsd8ZEOcjjpu/qOq3RJ6GRfxa8CCwtAM83d6J2mKOeQFUmMyVXUSsBCCOdufmieTKi+hOUtNAbyNM4lY4AXI537b9GaY8oSeje0NGU8+QCOuf7jGdRac5B9uIk7WwD76RAJnqyep6U/OdvQV4RLvvZ9w7nO4bY8RHaUaLxC2u4aIRRaZtLu5rm8GKBPy87OzQVXNgnLM01I8s3Z4wJ3i7jXqkknDy4VkIyLBSQvIvUzxYHeNdMVWDmS+jPN9ScVmolUwGzH1A23td8UWFHOjTjXHLjNm5Yq+7MIOoaxeMlKPYXRFKofRY8Qh5o5tqvycSAJ9KUqfg==", "ProtectionKeyId" : "7D9BB04D9D0A4A24800CADBFEF232689E048F69C", "ProtectionKeyType" : 1, "Checksum" : "TfXtjCIlq1Y=" }

### <a name="link-hello-contentkey-toohello-asset"></a><span data-ttu-id="7b4fa-266">Łącze hello toohello ContentKey zasobów</span><span class="sxs-lookup"><span data-stu-id="7b4fa-266">Link hello ContentKey toohello Asset</span></span>
<span data-ttu-id="7b4fa-267">Witaj ContentKey jest skojarzony tooone lub więcej zasobów poprzez wysłanie żądania POST protokołu HTTP.</span><span class="sxs-lookup"><span data-stu-id="7b4fa-267">hello ContentKey is associated tooone or more assets by sending a HTTP POST request.</span></span> <span data-ttu-id="7b4fa-268">Witaj następujące żądania jest przykład toolink hello przykład ContentKey toohello przykład zasób według identyfikatora.</span><span class="sxs-lookup"><span data-stu-id="7b4fa-268">hello following request is an example toolink hello example ContentKey toohello example asset by Id.</span></span>

<span data-ttu-id="7b4fa-269">**Odpowiedź HTTP**</span><span class="sxs-lookup"><span data-stu-id="7b4fa-269">**HTTP Response**</span></span>

    POST https://media.windows.net/API/Assets('nb:cid:UUID:b3023475-09b4-4647-9d6d-6fc242822e68')/$links/ContentKeys HTTP/1.1
    Content-Type: application/json;odata=verbose
    Accept: application/json;odata=verbose
    DataServiceVersion: 3.0
    MaxDataServiceVersion: 3.0
    x-ms-version: 2.11
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=070500D0-F35C-4A5A-9249-485BBF4EC70B&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1334275521&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=GxdBb%2fmEyN7iHdNxbawawHRftLhPFFqxX1JZckuv3hY%3d
    Host: media.windows.net
    Content-Length: 113
    Expect: 100-continue

    { "uri": "https://media.windows.net/api/ContentKeys('nb%3Akid%3AUUID%3A32e6efaf-5fba-4538-b115-9d1cefe43510')"}

<span data-ttu-id="7b4fa-270">**Odpowiedź HTTP**</span><span class="sxs-lookup"><span data-stu-id="7b4fa-270">**HTTP Response**</span></span>

    GET https://media.windows.net/API/IngestManifests('nb:mid:UUID:5c77f186-414f-8b48-8231-17f9264e2048') HTTP/1.1
    Content-Type: application/json;odata=verbose
    Accept: application/json;odata=verbose
    DataServiceVersion: 3.0
    MaxDataServiceVersion: 3.0
    x-ms-version: 2.11
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=070500D0-F35C-4A5A-9249-485BBF4EC70B&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1334275521&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=GxdBb%2fmEyN7iHdNxbawawHRftLhPFFqxX1JZckuv3hY%3d
    Host: media.windows.net

## <a name="next-steps"></a><span data-ttu-id="7b4fa-271">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="7b4fa-271">Next steps</span></span>

<span data-ttu-id="7b4fa-272">Teraz możesz zakodować przekazane elementy zawartości.</span><span class="sxs-lookup"><span data-stu-id="7b4fa-272">You can now encode your uploaded assets.</span></span> <span data-ttu-id="7b4fa-273">Więcej informacji znajduje się na stronie [Kodowanie elementów zawartości](media-services-portal-encode.md).</span><span class="sxs-lookup"><span data-stu-id="7b4fa-273">For more information, see [Encode assets](media-services-portal-encode.md).</span></span>

<span data-ttu-id="7b4fa-274">Umożliwia także tootrigger usługi Azure Functions zadania kodowania, na podstawie pliku odbieranych w kontenerze hello skonfigurowane.</span><span class="sxs-lookup"><span data-stu-id="7b4fa-274">You can also use Azure Functions tootrigger an encoding job based on a file arriving in hello configured container.</span></span> <span data-ttu-id="7b4fa-275">Aby uzyskać więcej informacji, zobacz [ten przykład](https://azure.microsoft.com/resources/samples/media-services-dotnet-functions-integration/ ).</span><span class="sxs-lookup"><span data-stu-id="7b4fa-275">For more information, see [this sample](https://azure.microsoft.com/resources/samples/media-services-dotnet-functions-integration/ ).</span></span>

## <a name="media-services-learning-paths"></a><span data-ttu-id="7b4fa-276">Ścieżki szkoleniowe dotyczące usługi Media Services</span><span class="sxs-lookup"><span data-stu-id="7b4fa-276">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="7b4fa-277">Przekazywanie opinii</span><span class="sxs-lookup"><span data-stu-id="7b4fa-277">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

[How tooGet a Media Processor]: media-services-get-media-processor.md

