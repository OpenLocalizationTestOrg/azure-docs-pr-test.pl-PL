---
title: "pliki aaaUpload do konta usługi Media Services przy użyciu platformy .NET | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak nośnika tooget zawartości do usługi Media Services za tworzenie i przekazywanie zasoby."
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: c9c86380-9395-4db8-acea-507c52066f73
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/12/2017
ms.author: juliako
ms.openlocfilehash: 11c8a359b09efe04b54490fd48ac0cd7c366f8b3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="upload-files-into-a-media-services-account-using-net"></a><span data-ttu-id="fb113-103">Przekazywanie plików do konta usługi Media Services przy użyciu platformy .NET</span><span class="sxs-lookup"><span data-stu-id="fb113-103">Upload files into a Media Services account using .NET</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="fb113-104">.NET</span><span class="sxs-lookup"><span data-stu-id="fb113-104">.NET</span></span>](media-services-dotnet-upload-files.md)
> * [<span data-ttu-id="fb113-105">REST</span><span class="sxs-lookup"><span data-stu-id="fb113-105">REST</span></span>](media-services-rest-upload-files.md)
> * [<span data-ttu-id="fb113-106">Portal</span><span class="sxs-lookup"><span data-stu-id="fb113-106">Portal</span></span>](media-services-portal-upload-files.md)
> 
> 

<span data-ttu-id="fb113-107">Za pomocą usługi Media Services można przekazać (lub pozyskać) pliki cyfrowe do elementu zawartości.</span><span class="sxs-lookup"><span data-stu-id="fb113-107">In Media Services, you upload (or ingest) your digital files into an asset.</span></span> <span data-ttu-id="fb113-108">Witaj **zasobów** może zawierać wideo, audio, obrazy, kolekcje miniatur, tekst ścieżek i napisów plików (i hello metadane dotyczące tych plików.)  Po przekazaniu plików hello zawartość jest bezpiecznie przechowywana w chmurze powitania dla dalszego przetwarzania i przesyłania strumieniowego.</span><span class="sxs-lookup"><span data-stu-id="fb113-108">hello **Asset** entity can contain video, audio, images, thumbnail collections, text tracks and closed caption files (and hello metadata about these files.)  Once hello files are uploaded, your content is stored securely in hello cloud for further processing and streaming.</span></span>

<span data-ttu-id="fb113-109">pliki Hello w hello zasobów są nazywane **plików zasobów**.</span><span class="sxs-lookup"><span data-stu-id="fb113-109">hello files in hello asset are called **Asset Files**.</span></span> <span data-ttu-id="fb113-110">Witaj **AssetFile** wystąpienia oraz plik multimedialna hello są dwa różne obiekty.</span><span class="sxs-lookup"><span data-stu-id="fb113-110">hello **AssetFile** instance and hello actual media file are two distinct objects.</span></span> <span data-ttu-id="fb113-111">wystąpienia AssetFile Hello zawiera metadane dotyczące plików multimedialnych hello, a plik multimedialny hello zawiera zawartość multimedialna hello.</span><span class="sxs-lookup"><span data-stu-id="fb113-111">hello AssetFile instance contains metadata about hello media file, while hello media file contains hello actual media content.</span></span>

> [!NOTE]
> <span data-ttu-id="fb113-112">Zastosuj Hello następujące zagadnienia:</span><span class="sxs-lookup"><span data-stu-id="fb113-112">hello following considerations apply:</span></span>
> 
> * <span data-ttu-id="fb113-113">Usługi Media Services używa wartości hello hello właściwość IAssetFile.Name podczas kompilowania adresów URL dla hello przesyłania strumieniowego zawartości (na przykład http://{AMSAccount}.origin.mediaservices.windows.net/{GUID}/{IAssetFile.Name}/streamingParameters.) Z tego powodu kodowania procent jest niedozwolone.</span><span class="sxs-lookup"><span data-stu-id="fb113-113">Media Services uses hello value of hello IAssetFile.Name property when building URLs for hello streaming content (for example, http://{AMSAccount}.origin.mediaservices.windows.net/{GUID}/{IAssetFile.Name}/streamingParameters.) For this reason, percent-encoding is not allowed.</span></span> <span data-ttu-id="fb113-114">Hello wartość hello **nazwa** właściwość nie może mieć jedną z następujących przyczyn hello [procent kodowanie zarezerwowanych znaków](http://en.wikipedia.org/wiki/Percent-encoding#Percent-encoding_reserved_characters):! * "();: @& = + $, /? [] % #".</span><span class="sxs-lookup"><span data-stu-id="fb113-114">hello value of hello **Name** property cannot have any of hello following [percent-encoding-reserved characters](http://en.wikipedia.org/wiki/Percent-encoding#Percent-encoding_reserved_characters): !*'();:@&=+$,/?%#[]".</span></span> <span data-ttu-id="fb113-115">Ponadto może istnieć tylko jeden "." hello rozszerzenie.</span><span class="sxs-lookup"><span data-stu-id="fb113-115">Also, there can only be one '.' for hello file name extension.</span></span>
> * <span data-ttu-id="fb113-116">Długość Hello hello nazwy nie może być większa niż 260 znaków.</span><span class="sxs-lookup"><span data-stu-id="fb113-116">hello length of hello name should not be greater than 260 characters.</span></span>
> * <span data-ttu-id="fb113-117">Brak limitu toohello maksymalny obsługiwany rozmiar pliku do przetwarzania w usłudze Media Services.</span><span class="sxs-lookup"><span data-stu-id="fb113-117">There is a limit toohello maximum file size supported for processing in Media Services.</span></span> <span data-ttu-id="fb113-118">Zobacz [to](media-services-quotas-and-limitations.md) tematu, aby uzyskać szczegółowe informacje dotyczące limitu rozmiaru pliku hello.</span><span class="sxs-lookup"><span data-stu-id="fb113-118">Please see [this](media-services-quotas-and-limitations.md) topic for details about hello file size limitation.</span></span>
> * <span data-ttu-id="fb113-119">Limit różnych zasad usługi AMS wynosi 1 000 000 (na przykład zasad lokalizatorów lub ContentKeyAuthorizationPolicy).</span><span class="sxs-lookup"><span data-stu-id="fb113-119">There is a limit of 1,000,000 policies for different AMS policies (for example, for Locator policy or ContentKeyAuthorizationPolicy).</span></span> <span data-ttu-id="fb113-120">Należy używać hello tym samym identyfikatorze zasad, jeśli używasz zawsze hello sam dni / dostęp uprawnień, na przykład zasady dla lokalizatorów, które są przeznaczone tooremain w miejscu przez długi czas (zasady — przekazywanie).</span><span class="sxs-lookup"><span data-stu-id="fb113-120">You should use hello same policy ID if you are always using hello same days / access permissions, for example, policies for locators that are intended tooremain in place for a long time (non-upload policies).</span></span> <span data-ttu-id="fb113-121">Aby uzyskać więcej informacji, zobacz [ten](media-services-dotnet-manage-entities.md#limit-access-policies) temat.</span><span class="sxs-lookup"><span data-stu-id="fb113-121">For more information, see [this](media-services-dotnet-manage-entities.md#limit-access-policies) topic.</span></span>
> 

<span data-ttu-id="fb113-122">Podczas tworzenia zasobów, można określić hello następujące opcje szyfrowania.</span><span class="sxs-lookup"><span data-stu-id="fb113-122">When you create assets, you can specify hello following encryption options.</span></span> 

* <span data-ttu-id="fb113-123">**None** — szyfrowanie nie jest stosowane.</span><span class="sxs-lookup"><span data-stu-id="fb113-123">**None** - No encryption is used.</span></span> <span data-ttu-id="fb113-124">Jest to wartość domyślna hello.</span><span class="sxs-lookup"><span data-stu-id="fb113-124">This is hello default value.</span></span> <span data-ttu-id="fb113-125">Należy pamiętać, że podczas korzystania z tej opcji zawartość nie jest chroniony w trakcie przesyłania lub przechowywania w magazynie.</span><span class="sxs-lookup"><span data-stu-id="fb113-125">Note that when using this option your content is not protected in transit or at rest in storage.</span></span>
  <span data-ttu-id="fb113-126">Jeśli planujesz toodeliver MP4 przy użyciu pobierania progresywnego, użyj tej opcji.</span><span class="sxs-lookup"><span data-stu-id="fb113-126">If you plan toodeliver an MP4 using progressive download, use this option.</span></span> 
* <span data-ttu-id="fb113-127">**CommonEncryption** — ta opcja umożliwia przekazanie zawartości, który został już szyfrowane i chronione za pomocą wspólnego szyfrowania lub technologii PlayReady DRM (na przykład, Smooth Streaming chronione za pomocą technologii PlayReady DRM).</span><span class="sxs-lookup"><span data-stu-id="fb113-127">**CommonEncryption** - Use this option if you are uploading content that has already been encrypted and protected with Common Encryption or PlayReady DRM (for example, Smooth Streaming protected with PlayReady DRM).</span></span>
* <span data-ttu-id="fb113-128">**EnvelopeEncrypted** — Użyj tej opcji, Jeśli przesyłasz HLS zaszyfrowanych z użyciem standardu AES.</span><span class="sxs-lookup"><span data-stu-id="fb113-128">**EnvelopeEncrypted** – Use this option if you are uploading HLS encrypted with AES.</span></span> <span data-ttu-id="fb113-129">Należy pamiętać, że pliki hello musi zostały zakodowane i zaszyfrowane przez Transform Manager.</span><span class="sxs-lookup"><span data-stu-id="fb113-129">Note that hello files must have been encoded and encrypted by Transform Manager.</span></span>
* <span data-ttu-id="fb113-130">**StorageEncrypted** — szyfruje zawartości lokalnie, przy użyciu standardu AES 256-bitowego, a następnie przekazanie jej tooAzure magazynu, w którym są przechowywane szyfrowane, gdy.</span><span class="sxs-lookup"><span data-stu-id="fb113-130">**StorageEncrypted** - Encrypts your clear content locally using AES-256 bit encryption and then uploads it tooAzure Storage where it is stored encrypted at rest.</span></span> <span data-ttu-id="fb113-131">Elementy zawartości chronione przy użyciu szyfrowania magazynu są automatycznie bez szyfrowania i umieszczana w poprzednich tooencoding systemu szyfrowania plików i opcjonalnie ponownie szyfrowane przed toouploading zwrotnym w formie nowego elementu zawartości wyjściowej.</span><span class="sxs-lookup"><span data-stu-id="fb113-131">Assets protected with Storage Encryption are automatically unencrypted and placed in an encrypted file system prior tooencoding, and optionally re-encrypted prior toouploading back as a new output asset.</span></span> <span data-ttu-id="fb113-132">Witaj pierwotnym zastosowaniem szyfrowania magazynu jest toosecure Twojego wysokiej jakości multimedialnych plików wejściowych pomocą silnego szyfrowania rest na dysku.</span><span class="sxs-lookup"><span data-stu-id="fb113-132">hello primary use case for Storage Encryption is when you want toosecure your high quality input media files with strong encryption at rest on disk.</span></span>
  
    <span data-ttu-id="fb113-133">Usługa Media Services udostępnia szyfrowanie magazynu na dysku dla zasobów, nie w locie podobnie jak Menedżer prawami cyfrowymi (DRM).</span><span class="sxs-lookup"><span data-stu-id="fb113-133">Media Services provides on-disk storage encryption for your assets, not over-the-wire like Digital Rights Manager (DRM).</span></span>
  
    <span data-ttu-id="fb113-134">Jeśli element zawartości jest szyfrowany w magazynie, należy skonfigurować zasady dostarczania elementu zawartości.</span><span class="sxs-lookup"><span data-stu-id="fb113-134">If your asset is storage encrypted, you must configure asset delivery policy.</span></span> <span data-ttu-id="fb113-135">Aby uzyskać więcej informacji, zobacz [Konfigurowanie zasad dostarczania elementów zawartości](media-services-dotnet-configure-asset-delivery-policy.md).</span><span class="sxs-lookup"><span data-stu-id="fb113-135">For more information see [Configuring asset delivery policy](media-services-dotnet-configure-asset-delivery-policy.md).</span></span>

<span data-ttu-id="fb113-136">Jeśli określisz dla Twojego toobe zasobów zaszyfrowane za pomocą **CommonEncrypted** opcji lub **EnvelopeEncypted** opcji, konieczne będzie tooassociate zawartości z **ContentKey**.</span><span class="sxs-lookup"><span data-stu-id="fb113-136">If you specify for your asset toobe encrypted with a **CommonEncrypted** option, or an **EnvelopeEncypted** option, you will need tooassociate your asset with a **ContentKey**.</span></span> <span data-ttu-id="fb113-137">Aby uzyskać więcej informacji, zobacz [jak toocreate ContentKey](media-services-dotnet-create-contentkey.md).</span><span class="sxs-lookup"><span data-stu-id="fb113-137">For more information, see [How toocreate a ContentKey](media-services-dotnet-create-contentkey.md).</span></span> 

<span data-ttu-id="fb113-138">Jeśli określisz dla Twojego toobe zasobów zaszyfrowane za pomocą **StorageEncrypted** hello SDK usługi Media Services dla platformy .NET zostanie utworzona, należy **StorateEncrypted** **ContentKey** dla użytkownika zasobów.</span><span class="sxs-lookup"><span data-stu-id="fb113-138">If you specify for your asset toobe encrypted with a **StorageEncrypted** option, hello Media Services SDK for .NET will create a **StorateEncrypted** **ContentKey** for your asset.</span></span>

<span data-ttu-id="fb113-139">W tym temacie pokazano, jak usługi multimediów toouse .NET SDK, a także pliki tooupload rozszerzenia .NET SDK usługi Media Services do zawartości Media Services.</span><span class="sxs-lookup"><span data-stu-id="fb113-139">This topic shows how toouse Media Services .NET SDK as well as Media Services .NET SDK extensions tooupload files into a Media Services asset.</span></span>

## <a name="upload-a-single-file-with-media-services-net-sdk"></a><span data-ttu-id="fb113-140">Przekaż pojedynczy plik z zestawu .NET SDK usługi multimediów</span><span class="sxs-lookup"><span data-stu-id="fb113-140">Upload a single file with Media Services .NET SDK</span></span>
<span data-ttu-id="fb113-141">Poniższy kod przykładowy Hello korzysta z zestawu .NET SDK tooupload pojedynczy plik.</span><span class="sxs-lookup"><span data-stu-id="fb113-141">hello sample code below uses .NET SDK tooupload a single file.</span></span> <span data-ttu-id="fb113-142">Witaj AccessPolicy i Locator są tworzone i niszczone przez funkcję przekazywania hello.</span><span class="sxs-lookup"><span data-stu-id="fb113-142">hello AccessPolicy and Locator are created and destroyed by hello Upload function.</span></span> 


        static public IAsset CreateAssetAndUploadSingleFile(AssetCreationOptions assetCreationOptions, string singleFilePath)
        {
            if (!File.Exists(singleFilePath))
            {
                Console.WriteLine("File does not exist.");
                return null;
            }

            var assetName = Path.GetFileNameWithoutExtension(singleFilePath);
            IAsset inputAsset = _context.Assets.Create(assetName, assetCreationOptions);

            var assetFile = inputAsset.AssetFiles.Create(Path.GetFileName(singleFilePath));

            Console.WriteLine("Upload {0}", assetFile.Name);

            assetFile.Upload(singleFilePath);
            Console.WriteLine("Done uploading {0}", assetFile.Name);

            return inputAsset;
        }


## <a name="upload-multiple-files-with-media-services-net-sdk"></a><span data-ttu-id="fb113-143">Przekazywania wielu plików z zestawu .NET SDK usługi multimediów</span><span class="sxs-lookup"><span data-stu-id="fb113-143">Upload multiple files with Media Services .NET SDK</span></span>
<span data-ttu-id="fb113-144">Witaj następującego kodu pokazuje sposób toocreate zasobów i przekazywania wielu plików.</span><span class="sxs-lookup"><span data-stu-id="fb113-144">hello following code shows how toocreate an asset and upload multiple files.</span></span>

<span data-ttu-id="fb113-145">Kod Hello hello następujące:</span><span class="sxs-lookup"><span data-stu-id="fb113-145">hello code does hello following:</span></span>

* <span data-ttu-id="fb113-146">Tworzy pusty zasobów przy użyciu metody CreateEmptyAsset hello zdefiniowanej w poprzednim kroku hello.</span><span class="sxs-lookup"><span data-stu-id="fb113-146">Creates an empty asset using hello CreateEmptyAsset method defined in hello previous step.</span></span>
* <span data-ttu-id="fb113-147">Tworzy **AccessPolicy** wystąpienie definiujące hello uprawnienia i czas trwania dostępu toohello zasobów.</span><span class="sxs-lookup"><span data-stu-id="fb113-147">Creates an **AccessPolicy** instance that defines hello permissions and duration of access toohello asset.</span></span>
* <span data-ttu-id="fb113-148">Tworzy **lokalizatora** wystąpienia, która zapewnia dostęp do zasobów toohello.</span><span class="sxs-lookup"><span data-stu-id="fb113-148">Creates a **Locator** instance that provides access toohello asset.</span></span>
* <span data-ttu-id="fb113-149">Tworzy **BlobTransferClient** wystąpienia.</span><span class="sxs-lookup"><span data-stu-id="fb113-149">Creates a **BlobTransferClient** instance.</span></span> <span data-ttu-id="fb113-150">Ten typ przedstawia klienta, który działa na powitalne obiektów blob Azure.</span><span class="sxs-lookup"><span data-stu-id="fb113-150">This type represents a client that operates on hello Azure blobs.</span></span> <span data-ttu-id="fb113-151">W tym przykładzie używamy powitania klienta toomonitor hello przekazywania postępu.</span><span class="sxs-lookup"><span data-stu-id="fb113-151">In this example we use hello client toomonitor hello upload progress.</span></span> 
* <span data-ttu-id="fb113-152">Wylicza pliki w określonym katalogu hello i tworzy **AssetFile** wystąpienia dla każdego pliku.</span><span class="sxs-lookup"><span data-stu-id="fb113-152">Enumerates through files in hello specified directory and creates an **AssetFile** instance for each file.</span></span>
* <span data-ttu-id="fb113-153">Przekazywanie hello plików do usługi Media Services przy użyciu hello **UploadAsync** metody.</span><span class="sxs-lookup"><span data-stu-id="fb113-153">Uploads hello files into Media Services using hello **UploadAsync** method.</span></span> 

> [!NOTE]
> <span data-ttu-id="fb113-154">Użyj hello UploadAsync metody tooensure nie blokują hello wywołań i hello pliki są wysyłane równolegle.</span><span class="sxs-lookup"><span data-stu-id="fb113-154">Use hello UploadAsync method tooensure that hello calls are not blocking and hello files are uploaded in parallel.</span></span>
> 
> 

        static public IAsset CreateAssetAndUploadMultipleFiles(AssetCreationOptions assetCreationOptions, string folderPath)
        {
            var assetName = "UploadMultipleFiles_" + DateTime.UtcNow.ToString();

            IAsset asset = _context.Assets.Create(assetName, assetCreationOptions);

            var accessPolicy = _context.AccessPolicies.Create(assetName, TimeSpan.FromDays(30),
                                                                AccessPermissions.Write | AccessPermissions.List);

            var locator = _context.Locators.CreateLocator(LocatorType.Sas, asset, accessPolicy);

            var blobTransferClient = new BlobTransferClient();
            blobTransferClient.NumberOfConcurrentTransfers = 20;
            blobTransferClient.ParallelTransferThreadCount = 20;

            blobTransferClient.TransferProgressChanged += blobTransferClient_TransferProgressChanged;

            var filePaths = Directory.EnumerateFiles(folderPath);

            Console.WriteLine("There are {0} files in {1}", filePaths.Count(), folderPath);

            if (!filePaths.Any())
            {
                throw new FileNotFoundException(String.Format("No files in directory, check folderPath: {0}", folderPath));
            }

            var uploadTasks = new List<Task>();
            foreach (var filePath in filePaths)
            {
                var assetFile = asset.AssetFiles.Create(Path.GetFileName(filePath));
                Console.WriteLine("Created assetFile {0}", assetFile.Name);

                // It is recommended toovalidate AccestFiles before upload. 
                Console.WriteLine("Start uploading of {0}", assetFile.Name);
                uploadTasks.Add(assetFile.UploadAsync(filePath, blobTransferClient, locator, CancellationToken.None));
            }

            Task.WaitAll(uploadTasks.ToArray());
            Console.WriteLine("Done uploading hello files");

            blobTransferClient.TransferProgressChanged -= blobTransferClient_TransferProgressChanged;

            locator.Delete();
            accessPolicy.Delete();

            return asset;
        }

    static void  blobTransferClient_TransferProgressChanged(object sender, BlobTransferProgressChangedEventArgs e)
    {
        if (e.ProgressPercentage > 4) // Avoid startup jitter, as hello upload tasks are added.
        {
            Console.WriteLine("{0}% upload competed for {1}.", e.ProgressPercentage, e.LocalFile);
        }
    }



<span data-ttu-id="fb113-155">Podczas przekazywania dużej liczby zasobów, należy wziąć pod uwagę następujące hello.</span><span class="sxs-lookup"><span data-stu-id="fb113-155">When uploading a large number of assets, consider hello following.</span></span>

* <span data-ttu-id="fb113-156">Utwórz nową **CloudMediaContext** obiektu na wątek.</span><span class="sxs-lookup"><span data-stu-id="fb113-156">Create a new **CloudMediaContext** object per thread.</span></span> <span data-ttu-id="fb113-157">Witaj **CloudMediaContext** klasa nie jest bezpieczne dla wątków.</span><span class="sxs-lookup"><span data-stu-id="fb113-157">hello **CloudMediaContext** class is not thread safe.</span></span>
* <span data-ttu-id="fb113-158">Zwiększ NumberOfConcurrentTransfers z hello wartość domyślną 2 tooa wyższa wartość 5.</span><span class="sxs-lookup"><span data-stu-id="fb113-158">Increase NumberOfConcurrentTransfers from hello default value of 2 tooa higher value like 5.</span></span> <span data-ttu-id="fb113-159">Ustawienie tej właściwości dotyczy wszystkich wystąpień **CloudMediaContext**.</span><span class="sxs-lookup"><span data-stu-id="fb113-159">Setting this property affects all instances of **CloudMediaContext**.</span></span> 
* <span data-ttu-id="fb113-160">Zachowaj ParallelTransferThreadCount na powitania wartość domyślną równą 10.</span><span class="sxs-lookup"><span data-stu-id="fb113-160">Keep ParallelTransferThreadCount at hello default value of 10.</span></span>

## <span data-ttu-id="fb113-161"><a id="ingest_in_bulk"></a>Pozyskaniu elementów zawartości zbiorczo przy użyciu zestawu .NET SDK usługi multimediów</span><span class="sxs-lookup"><span data-stu-id="fb113-161"><a id="ingest_in_bulk"></a>Ingesting Assets in Bulk using Media Services .NET SDK</span></span>
<span data-ttu-id="fb113-162">Przekazywanie zawartości dużych plików może być wąskie gardło podczas tworzenia zasobu.</span><span class="sxs-lookup"><span data-stu-id="fb113-162">Uploading large asset files can be a bottleneck during asset creation.</span></span> <span data-ttu-id="fb113-163">Pozyskaniu elementów zawartości w zbiorczej lub "Zbiorczego wprowadzania", polega na rozdzieleniu tworzenie zasobów za pomocą hello procesu przekazywania.</span><span class="sxs-lookup"><span data-stu-id="fb113-163">Ingesting Assets in Bulk or “Bulk Ingesting”, involves decoupling asset creation from hello upload process.</span></span> <span data-ttu-id="fb113-164">toouse podejście ingesting zbiorczego tworzenie manifestu (IngestManifest) dotyczące zasobów hello i skojarzone z nią pliki.</span><span class="sxs-lookup"><span data-stu-id="fb113-164">toouse a bulk ingesting approach, create a manifest (IngestManifest) that describes hello asset and its associated files.</span></span> <span data-ttu-id="fb113-165">Następnie należy użyć metody przekazywania hello kontenera obiektów blob z wybranym tooupload hello skojarzone pliki toohello manifestu.</span><span class="sxs-lookup"><span data-stu-id="fb113-165">Then use hello upload method of your choice tooupload hello associated files toohello manifest’s blob container.</span></span> <span data-ttu-id="fb113-166">Microsoft Azure Media Services Obserwujący kontenera obiektów blob hello skojarzonego z hello manifestu.</span><span class="sxs-lookup"><span data-stu-id="fb113-166">Microsoft Azure Media Services watches hello blob container associated with hello manifest.</span></span> <span data-ttu-id="fb113-167">Gdy plik jest przekazany toohello kontenera obiektów blob, Microsoft Azure Media Services kończy tworzenie zasobów hello na podstawie konfiguracji hello hello zasobów w manifeście hello (IngestManifestAsset).</span><span class="sxs-lookup"><span data-stu-id="fb113-167">Once a file is uploaded toohello blob container, Microsoft Azure Media Services completes hello asset creation based on hello configuration of hello asset in hello manifest (IngestManifestAsset).</span></span>

<span data-ttu-id="fb113-168">toocreate nowe IngestManifest wywołać metodę tworzenia hello udostępnianych przez hello kolekcji IngestManifests na powitania CloudMediaContext.</span><span class="sxs-lookup"><span data-stu-id="fb113-168">toocreate a new IngestManifest call hello Create method exposed by hello IngestManifests collection on hello CloudMediaContext.</span></span> <span data-ttu-id="fb113-169">Ta metoda spowoduje utworzenie nowej IngestManifest z hello manifestu o podanej nazwie.</span><span class="sxs-lookup"><span data-stu-id="fb113-169">This method will create a new IngestManifest with hello manifest name you provide.</span></span>

    IIngestManifest manifest = context.IngestManifests.Create(name);

<span data-ttu-id="fb113-170">Utwórz hello zasobów, które będą skojarzone z zbiorczego hello IngestManifest.</span><span class="sxs-lookup"><span data-stu-id="fb113-170">Create hello assets that will be associated with hello bulk IngestManifest.</span></span> <span data-ttu-id="fb113-171">Skonfiguruj opcje szyfrowania hello żądanego na powitania zasobów służy do wprowadzania zbiorczego.</span><span class="sxs-lookup"><span data-stu-id="fb113-171">Configure hello desired encryption options on hello asset for bulk ingesting.</span></span>

    // Create hello assets that will be associated with this bulk ingest manifest
    IAsset destAsset1 = _context.Assets.Create(name + "_asset_1", AssetCreationOptions.None);
    IAsset destAsset2 = _context.Assets.Create(name + "_asset_2", AssetCreationOptions.None);

<span data-ttu-id="fb113-172">IngestManifestAsset kojarzy zasób z zbiorczego IngestManifest służy do wprowadzania zbiorczego.</span><span class="sxs-lookup"><span data-stu-id="fb113-172">An IngestManifestAsset associates an Asset with a bulk IngestManifest for bulk ingesting.</span></span> <span data-ttu-id="fb113-173">Powoduje również skojarzenie hello AssetFiles tworzącej każdego zasobu.</span><span class="sxs-lookup"><span data-stu-id="fb113-173">It also associates hello AssetFiles that will make up each Asset.</span></span> <span data-ttu-id="fb113-174">toocreate IngestManifestAsset, użyj metody tworzenia hello hello kontekstu serwera.</span><span class="sxs-lookup"><span data-stu-id="fb113-174">toocreate an IngestManifestAsset, use hello Create method on hello server context.</span></span>

<span data-ttu-id="fb113-175">Witaj poniższym przykładzie pokazano dodawania dwóch IngestManifestAssets nowe kojarzące hello zasoby dwóch wcześniej utworzony zbiorczego toohello pozyskiwania manifestu.</span><span class="sxs-lookup"><span data-stu-id="fb113-175">hello following example demonstrates adding two new IngestManifestAssets that associate hello two assets previously created toohello bulk ingest manifest.</span></span> <span data-ttu-id="fb113-176">Każdy IngestManifestAsset powoduje również skojarzenie zestaw plików, które zostaną przekazane za każdy zasób podczas wprowadzania zbiorczego.</span><span class="sxs-lookup"><span data-stu-id="fb113-176">Each IngestManifestAsset also associates a set of files that will be uploaded for each asset during bulk ingesting.</span></span>  

    string filename1 = _singleInputMp4Path;
    string filename2 = _primaryFilePath;
    string filename3 = _singleInputFilePath;

    IIngestManifestAsset bulkAsset1 =  manifest.IngestManifestAssets.Create(destAsset1, new[] { filename1 });
    IIngestManifestAsset bulkAsset2 =  manifest.IngestManifestAssets.Create(destAsset2, new[] { filename2, filename3 });

<span data-ttu-id="fb113-177">Można użyć dowolnej aplikacji klienta szybkich możliwość przekazywania hello zasobów plików toohello kontenera magazynu obiektów blob identyfikatora URI podał hello **IIngestManifest.BlobStorageUriForUpload** właściwości hello IngestManifest.</span><span class="sxs-lookup"><span data-stu-id="fb113-177">You can use any high speed client application capable of uploading hello asset files toohello blob storage container URI provided by hello **IIngestManifest.BlobStorageUriForUpload** property of hello IngestManifest.</span></span> <span data-ttu-id="fb113-178">Co Usługa przekazywania zauważalne szybkich [Aspera na żądanie dla aplikacji Azure](https://datamarket.azure.com/application/2cdbc511-cb12-4715-9871-c7e7fbbb82a6).</span><span class="sxs-lookup"><span data-stu-id="fb113-178">One notable high speed upload service is [Aspera On Demand for Azure Application](https://datamarket.azure.com/application/2cdbc511-cb12-4715-9871-c7e7fbbb82a6).</span></span> <span data-ttu-id="fb113-179">Można również napisać kod plików zasobów hello tooupload pokazane na powitania poniższy przykład kodu.</span><span class="sxs-lookup"><span data-stu-id="fb113-179">You can also write code tooupload hello assets files as shown in hello following code example.</span></span>

    static void UploadBlobFile(string destBlobURI, string filename)
    {
        Task copytask = new Task(() =>
        {
            var storageaccount = new CloudStorageAccount(new StorageCredentials(_storageAccountName, _storageAccountKey), true);
            CloudBlobClient blobClient = storageaccount.CreateCloudBlobClient();
            CloudBlobContainer blobContainer = blobClient.GetContainerReference(destBlobURI);

            string[] splitfilename = filename.Split('\\');
            var blob = blobContainer.GetBlockBlobReference(splitfilename[splitfilename.Length - 1]);

            using (var stream = System.IO.File.OpenRead(filename))
                blob.UploadFromStream(stream);

            lock (consoleWriteLock)
            {
                Console.WriteLine("Upload for {0} completed.", filename);
            }
        });

        copytask.Start();
    }

<span data-ttu-id="fb113-180">Kod Hello przekazywania hello plików zasobów dla przykładu hello używane w tym temacie przedstawiono hello poniższy przykład kodu.</span><span class="sxs-lookup"><span data-stu-id="fb113-180">hello code for uploading hello asset files for hello sample used in this topic is shown in hello following code example.</span></span>

    UploadBlobFile(manifest.BlobStorageUriForUpload, filename1);
    UploadBlobFile(manifest.BlobStorageUriForUpload, filename2);
    UploadBlobFile(manifest.BlobStorageUriForUpload, filename3);


<span data-ttu-id="fb113-181">Można określić postęp hello hello zbiorczego wprowadzania dla wszystkich zasobów skojarzonych z **IngestManifest** przez sondowanie właściwość statystyki hello hello **IngestManifest**.</span><span class="sxs-lookup"><span data-stu-id="fb113-181">You can determine hello progress of hello bulk ingesting for all assets associated with an **IngestManifest** by polling hello Statistics property of hello **IngestManifest**.</span></span> <span data-ttu-id="fb113-182">W kolejności informacje o postępie tooupdate, należy użyć nowego **CloudMediaContext** zawsze sondowania hello statystyki właściwości.</span><span class="sxs-lookup"><span data-stu-id="fb113-182">In order tooupdate progress information, you must use a new **CloudMediaContext** each time you poll hello Statistics property.</span></span>

<span data-ttu-id="fb113-183">Witaj poniższym przykładzie pokazano sondowania IngestManifest przez jego **identyfikator**.</span><span class="sxs-lookup"><span data-stu-id="fb113-183">hello following example demonstrates polling an IngestManifest by its **Id**.</span></span>

    static void MonitorBulkManifest(string manifestID)
    {
       bool bContinue = true;
       while (bContinue)
       {
          CloudMediaContext context = GetContext();
          IIngestManifest manifest = context.IngestManifests.Where(m => m.Id == manifestID).FirstOrDefault();

          if (manifest != null)
          {
             lock(consoleWriteLock)
             {
                Console.WriteLine("\nWaiting on all file uploads.");
                Console.WriteLine("PendingFilesCount  : {0}", manifest.Statistics.PendingFilesCount);
                Console.WriteLine("FinishedFilesCount : {0}", manifest.Statistics.FinishedFilesCount);
                Console.WriteLine("{0}% complete.\n", (float)manifest.Statistics.FinishedFilesCount / (float)(manifest.Statistics.FinishedFilesCount + manifest.Statistics.PendingFilesCount) * 100);

                if (manifest.Statistics.PendingFilesCount == 0)
                {
                   Console.WriteLine("Completed\n");
                   bContinue = false;
                }
             }

             if (manifest.Statistics.FinishedFilesCount < manifest.Statistics.PendingFilesCount)
                Thread.Sleep(60000);
          }
          else // Manifest is null
             bContinue = false;
       }
    }



## <a name="upload-files-using-net-sdk-extensions"></a><span data-ttu-id="fb113-184">Przekazywanie plików przy użyciu rozszerzenia zestawu .NET SDK</span><span class="sxs-lookup"><span data-stu-id="fb113-184">Upload files using .NET SDK Extensions</span></span>
<span data-ttu-id="fb113-185">w poniższym przykładzie Hello pokazuje, jak tooupload w jednym pliku przy użyciu rozszerzenia zestawu .NET SDK.</span><span class="sxs-lookup"><span data-stu-id="fb113-185">hello example below shows how tooupload a single file using .NET SDK Extensions.</span></span> <span data-ttu-id="fb113-186">W takim przypadku hello **CreateFromFile** metoda jest używana, ale jest również dostępna wersja asynchroniczne hello (**CreateFromFileAsync**).</span><span class="sxs-lookup"><span data-stu-id="fb113-186">In this case hello **CreateFromFile** method is used, but hello asynchronous version is also available (**CreateFromFileAsync**).</span></span> <span data-ttu-id="fb113-187">Witaj **CreateFromFile** — metoda pozwala na określenie nazwy pliku hello, opcja szyfrowania i wywołanie zwrotne w kolejności tooreport hello postęp pliku hello przekazywania.</span><span class="sxs-lookup"><span data-stu-id="fb113-187">hello **CreateFromFile** method lets you specify hello file name, encryption option, and a callback in order tooreport hello upload progress of hello file.</span></span>

    static public IAsset UploadFile(string fileName, AssetCreationOptions options)
    {
        IAsset inputAsset = _context.Assets.CreateFromFile(
            fileName,
            options,
            (af, p) =>
            {
                Console.WriteLine("Uploading '{0}' - Progress: {1:0.##}%", af.Name, p.Progress);
            });

        Console.WriteLine("Asset {0} created.", inputAsset.Id);

        return inputAsset;
    }

<span data-ttu-id="fb113-188">Witaj poniższy przykład wywołuje funkcję UploadFile i określa szyfrowanie magazynu jako opcję tworzenia zasobów hello.</span><span class="sxs-lookup"><span data-stu-id="fb113-188">hello following example calls UploadFile function and specifies storage encryption as hello asset creation option.</span></span>  

    var asset = UploadFile(@"C:\VideoFiles\BigBuckBunny.mp4", AssetCreationOptions.StorageEncrypted);

## <a name="next-steps"></a><span data-ttu-id="fb113-189">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="fb113-189">Next steps</span></span>

<span data-ttu-id="fb113-190">Teraz możesz zakodować przekazane elementy zawartości.</span><span class="sxs-lookup"><span data-stu-id="fb113-190">You can now encode your uploaded assets.</span></span> <span data-ttu-id="fb113-191">Więcej informacji znajduje się na stronie [Kodowanie elementów zawartości](media-services-portal-encode.md).</span><span class="sxs-lookup"><span data-stu-id="fb113-191">For more information, see [Encode assets](media-services-portal-encode.md).</span></span>

<span data-ttu-id="fb113-192">Umożliwia także tootrigger usługi Azure Functions zadania kodowania, na podstawie pliku odbieranych w kontenerze hello skonfigurowane.</span><span class="sxs-lookup"><span data-stu-id="fb113-192">You can also use Azure Functions tootrigger an encoding job based on a file arriving in hello configured container.</span></span> <span data-ttu-id="fb113-193">Aby uzyskać więcej informacji, zobacz [ten przykład](https://azure.microsoft.com/resources/samples/media-services-dotnet-functions-integration/ ).</span><span class="sxs-lookup"><span data-stu-id="fb113-193">For more information, see [this sample](https://azure.microsoft.com/resources/samples/media-services-dotnet-functions-integration/ ).</span></span>

## <a name="media-services-learning-paths"></a><span data-ttu-id="fb113-194">Ścieżki szkoleniowe dotyczące usługi Media Services</span><span class="sxs-lookup"><span data-stu-id="fb113-194">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="fb113-195">Przekazywanie opinii</span><span class="sxs-lookup"><span data-stu-id="fb113-195">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="next-step"></a><span data-ttu-id="fb113-196">Następny krok</span><span class="sxs-lookup"><span data-stu-id="fb113-196">Next step</span></span>
<span data-ttu-id="fb113-197">Teraz, gdy zostały przekazane zasób usługi tooMedia Przejdź toohello [jak tooGet procesor multimediów] [ How tooGet a Media Processor] tematu.</span><span class="sxs-lookup"><span data-stu-id="fb113-197">Now that you have uploaded an asset tooMedia Services, go toohello [How tooGet a Media Processor][How tooGet a Media Processor] topic.</span></span>

[How tooGet a Media Processor]: media-services-get-media-processor.md

