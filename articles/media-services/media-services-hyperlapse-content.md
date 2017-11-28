---
title: "aaaHyperlapse plików multimedialnych na pliki z usługi Azure Media Hyperlapse | Dokumentacja firmy Microsoft"
description: "Azure Media Hyperlapse tworzy smooth czas, jaki upłynął wideo z pierwszą osobą lub akcji aparatu zawartości. W tym temacie przedstawiono sposób toouse indeksatora nośnika."
services: media-services
documentationcenter: 
author: asolanki
manager: johndeu
editor: 
ms.assetid: 37d54db6-9cf3-4ae9-b3c6-0d29c744e965
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 03/02/2017
ms.author: adsolank
ms.openlocfilehash: 85bb07206d0ca2f5b2fd0767e6ed4904195d3ab6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="hyperlapse-media-files-with-azure-media-hyperlapse"></a><span data-ttu-id="36639-104">Plikach multimedialnych przyspieszonych ujęć poklatkowych za pomocą usługi Azure Media Hyperlapse</span><span class="sxs-lookup"><span data-stu-id="36639-104">Hyperlapse Media Files with Azure Media Hyperlapse</span></span>
<span data-ttu-id="36639-105">Azure Media Hyperlapse jest nośnik procesora (MP) tworzącą smooth czas, jaki upłynął wideo z pierwszą osobą lub akcji aparatu zawartości.</span><span class="sxs-lookup"><span data-stu-id="36639-105">Azure Media Hyperlapse is a Media Processor (MP) that creates smooth time-lapsed videos from first-person or action-camera content.</span></span>  <span data-ttu-id="36639-106">Witaj równorzędny oparte na chmurze za[desktop Pro przyspieszonych ujęć poklatkowych i opartych na telefon komórkowy przyspieszonych ujęć poklatkowych Microsoft Research](http://aka.ms/hyperlapse), Hyperlapse firmy Microsoft dla usługi Azure Media Services używa hello ogromną skalę hello Azure Media Services nośnika Przetwarzanie toohorizontally platformy skalowanie i parallelize zbiorczego przyspieszonych ujęć poklatkowych przetwarzania.</span><span class="sxs-lookup"><span data-stu-id="36639-106">hello cloud-based sibling too[Microsoft Research's desktop Hyperlapse Pro and phone-based Hyperlapse Mobile](http://aka.ms/hyperlapse), Microsoft Hyperlapse for Azure Media Services utilizes hello massive scale of hello Azure Media Services Media Processing platform toohorizontally scale and parallelize bulk Hyperlapse processing.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="36639-107">Microsoft Hyperlapse jest zaprojektowana toowork najlepiej na pierwszą osobą zawartości za pomocą przenoszenia aparatu.</span><span class="sxs-lookup"><span data-stu-id="36639-107">Microsoft Hyperlapse is designed toowork best on first-person content with a moving camera.</span></span>  <span data-ttu-id="36639-108">Mimo że nadal kamery może nadal działać, nie można zagwarantować hello wydajności i jakości hello Azure Media przyspieszonych ujęć poklatkowych nośnika procesora dla innych typów zawartości.</span><span class="sxs-lookup"><span data-stu-id="36639-108">Although still-camera footage can still work, hello performance and quality of hello Azure Media Hyperlapse Media Processor cannot be guaranteed for other types of content.</span></span>  <span data-ttu-id="36639-109">więcej informacji na temat Hyperlapse firmy Microsoft dla usługi Azure Media Services toolearn i wyświetlić niektóre przykładowe filmy, zapoznaj się z hello [wprowadzające wpis w blogu](http://aka.ms/azurehyperlapseblog) z publicznej wersji zapoznawczej hello.</span><span class="sxs-lookup"><span data-stu-id="36639-109">toolearn more about Microsoft Hyperlapse for Azure Media Services and see some example videos, check out hello [introductory blog post](http://aka.ms/azurehyperlapseblog) from hello public preview.</span></span>
> 
> 

<span data-ttu-id="36639-110">Azure Media Hyperlapse zadania przyjmuje jako dane wejściowe plik MP4, MOV lub WMV zasobów oraz pliku konfiguracji, który określa, które ramki wideo powinny być czas, jaki upłynął i szybkość toowhat (np. pierwszych 10 000 ramek, x 2).</span><span class="sxs-lookup"><span data-stu-id="36639-110">An Azure Media Hyperlapse job takes as input an MP4, MOV, or WMV asset file along with a configuration file that specifies which frames of video should be time-lapsed and toowhat speed (e.g. first 10,000 frames at 2x).</span></span>  <span data-ttu-id="36639-111">dane wyjściowe Hello jest stabilnych i czas, jaki upłynął dobór hello wejściowy plik wideo.</span><span class="sxs-lookup"><span data-stu-id="36639-111">hello output is a stabilized and time-lapsed rendition of hello input video.</span></span>

<span data-ttu-id="36639-112">Najnowsze aktualizacje hello Azure Media Hyperlapse, zobacz [blogi Media Services](https://azure.microsoft.com/blog/topics/media-services/).</span><span class="sxs-lookup"><span data-stu-id="36639-112">For hello latest Azure Media Hyperlapse updates, see [Media Services blogs](https://azure.microsoft.com/blog/topics/media-services/).</span></span>

## <a name="hyperlapse-an-asset"></a><span data-ttu-id="36639-113">Przyspieszonych ujęć poklatkowych zasobów</span><span class="sxs-lookup"><span data-stu-id="36639-113">Hyperlapse an asset</span></span>
<span data-ttu-id="36639-114">Najpierw należy tooupload Twojego tooAzure żądanego pliku wejściowego usługi Media Services.</span><span class="sxs-lookup"><span data-stu-id="36639-114">First you will need tooupload your desired input file tooAzure Media Services.</span></span>  <span data-ttu-id="36639-115">więcej informacji o toolearn hello pojęcia związane z przekazywanie i zarządzania zawartością, przeczytaj hello [zarządzania zawartością artykułu](media-services-portal-vod-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="36639-115">toolearn more about hello concepts involved with uploading and managing content, read hello [content management article](media-services-portal-vod-get-started.md).</span></span>

### <span data-ttu-id="36639-116"><a id="configuration"></a>Ustawienie konfiguracji dla przyspieszonych ujęć poklatkowych</span><span class="sxs-lookup"><span data-stu-id="36639-116"><a id="configuration"></a>Configuration Preset for Hyperlapse</span></span>
<span data-ttu-id="36639-117">Gdy zawartość jest na koncie usługi Media Services, należy tooconstruct ustawień konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="36639-117">Once your content is in your Media Services account, you will need tooconstruct your configuration preset.</span></span>  <span data-ttu-id="36639-118">Witaj w poniższej tabeli opisano hello określone przez użytkownika pola:</span><span class="sxs-lookup"><span data-stu-id="36639-118">hello following table explains hello user-specified fields:</span></span>

| <span data-ttu-id="36639-119">Pole</span><span class="sxs-lookup"><span data-stu-id="36639-119">Field</span></span> | <span data-ttu-id="36639-120">Opis</span><span class="sxs-lookup"><span data-stu-id="36639-120">Description</span></span> |
| --- | --- |
| <span data-ttu-id="36639-121">StartFrame</span><span class="sxs-lookup"><span data-stu-id="36639-121">StartFrame</span></span> |<span data-ttu-id="36639-122">ramki Hello, na które Microsoft Hyperlapse hello powinny one zacząć przetwarzania.</span><span class="sxs-lookup"><span data-stu-id="36639-122">hello frame upon which hello Microsoft Hyperlapse processing should begin.</span></span> |
| <span data-ttu-id="36639-123">NumFrames</span><span class="sxs-lookup"><span data-stu-id="36639-123">NumFrames</span></span> |<span data-ttu-id="36639-124">Liczba Hello tooprocess ramki</span><span class="sxs-lookup"><span data-stu-id="36639-124">hello number of frames tooprocess</span></span> |
| <span data-ttu-id="36639-125">Szybkość</span><span class="sxs-lookup"><span data-stu-id="36639-125">Speed</span></span> |<span data-ttu-id="36639-126">współczynnik Hello, z których toospeed się hello wejściowy plik wideo.</span><span class="sxs-lookup"><span data-stu-id="36639-126">hello factor with which toospeed up hello input video.</span></span> |

<span data-ttu-id="36639-127">Witaj poniżej przedstawiono przykładowy plik konfiguracji zgodność w pliku XML i JSON:</span><span class="sxs-lookup"><span data-stu-id="36639-127">hello following is an example of a conformant configuration file in XML and JSON:</span></span>

<span data-ttu-id="36639-128">**Ustawienie wstępne XML:**</span><span class="sxs-lookup"><span data-stu-id="36639-128">**XML preset:**</span></span>

    <?xml version="1.0" encoding="utf-16"?>
    <Preset xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:xsd="http://www.w3.org/2001/XMLSchema" Version="1.0" xmlns="http://www.windowsazure.com/media/encoding/Preset/2014/03">
        <Sources>
            <Source StartFrame="0" NumFrames="10000" />
        </Sources>
        <Options>
            <Speed>12</Speed>
        </Options>
    </Preset>

<span data-ttu-id="36639-129">**Ustawienie wstępne JSON:**</span><span class="sxs-lookup"><span data-stu-id="36639-129">**JSON preset:**</span></span>

    {
        "Version":1.0,
        "Sources": [
            {
                "StartFrame":0,
                "NumFrames":2147483647
            }
        ],
        "Options": {
            "Speed":1,
            "Stabilize":false
        }
    }

### <span data-ttu-id="36639-130"><a id="sample_code"></a>Microsoft Hyperlapse z hello AMS .NET SDK</span><span class="sxs-lookup"><span data-stu-id="36639-130"><a id="sample_code"></a> Microsoft Hyperlapse with hello AMS .NET SDK</span></span>
<span data-ttu-id="36639-131">Witaj następująca metoda przekazuje plik nośnika jako zasób i tworzy zadanie z hello Azure Media przyspieszonych ujęć poklatkowych nośnika procesora.</span><span class="sxs-lookup"><span data-stu-id="36639-131">hello following method uploads a media file as an asset and creates a job with hello Azure Media Hyperlapse Media Processor.</span></span>

> [!NOTE]
> <span data-ttu-id="36639-132">CloudMediaContext ma już w zakresie o nazwie hello "context" toowork tego kodu.</span><span class="sxs-lookup"><span data-stu-id="36639-132">You should already have a CloudMediaContext in scope with hello name "context" for this code toowork.</span></span>  <span data-ttu-id="36639-133">więcej informacji na temat tego, odczytu hello toolearn [zarządzania zawartością artykułu](media-services-dotnet-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="36639-133">toolearn more about this, read hello [content management article](media-services-dotnet-get-started.md).</span></span>
> 
> [!NOTE]
> <span data-ttu-id="36639-134">argument ciągu Hello "hyperConfig" jest oczekiwany toobe konfiguracji zgodność ustawień w formacie JSON i XML zgodnie z powyższym opisem.</span><span class="sxs-lookup"><span data-stu-id="36639-134">hello string argument "hyperConfig" is expected toobe a conformant configuration preset in either JSON or XML as described above.</span></span>
> 
> 

        static bool RunHyperlapseJob(string input, string output, string hyperConfig)
        {
            // create asset with input file
            IAsset asset = context
            .Assets
            .CreateAssetAndUploadSingleFile(input, "My Hyperlapse Input", AssetCreationOptions.None);

            // grab instances of Azure Media Hyperlapse MP
            IMediaProcessor mp = context
            .MediaProcessors
            .GetLatestMediaProcessorByName("Azure Media Hyperlapse");

            // create Job with Hyperlapse task
            IJob job = context
            .Jobs
            .Create(String.Format("Hyperlapse {0}", input));

            if (String.IsNullOrEmpty(hyperConfig))
            {
            // config cannot be empty
            return false;
            }

            hyperConfig = File.ReadAllText(hyperConfig);

            ITask hyperlapseTask = job.Tasks.AddNew("Hyperlapse task",
            mp,
            hyperConfig,
            TaskOptions.None);
            hyperlapseTask.InputAssets.Add(asset);
            hyperlapseTask.OutputAssets.AddNew("Hyperlapse output",
            AssetCreationOptions.None);

            job.Submit();

            // Create progress printing and querying tasks
            Task progressPrintTask = new Task(() =>
            {

            IJob jobQuery = null;
            do
            {
                var progressContext = context;
                jobQuery = progressContext.Jobs
                .Where(j => j.Id == job.Id)
                .First();
                Console.WriteLine(string.Format("{0}\t{1}\t{2}",
                DateTime.Now,
                jobQuery.State,
                jobQuery.Tasks[0].Progress));
                Thread.Sleep(10000);
            }
            while (jobQuery.State != JobState.Finished &&
                                   jobQuery.State != JobState.Error &&
                                   jobQuery.State != JobState.Canceled);
                });
                
            progressPrintTask.Start();

            Task progressJobTask = job.GetExecutionProgressTask(
                                                 CancellationToken.None);
            progressJobTask.Wait();

            // If job state is Error, hello event handling
            // method for job progress should log errors.  Here we check
            // for error state and exit if needed.
            if (job.State == JobState.Error)
            {
                ErrorDetail error = job.Tasks.First().ErrorDetails.First();
                Console.WriteLine(string.Format("Error: {0}. {1}",
                                                error.Code,
                                                error.Message));  
                return false;                  
            }

        DownloadAsset(job.OutputMediaAssets.First(), output);
        return true;
    }

    static void DownloadAsset(IAsset asset, string outputDirectory)
    {
        foreach (IAssetFile file in asset.AssetFiles)
        {
            file.Download(Path.Combine(outputDirectory, file.Name));
        }
    }


    static IAsset CreateAssetAndUploadSingleFile(string filePath, string assetName, AssetCreationOptions options)
    {
        IAsset asset = context.Assets.Create(assetName, options);

        var assetFile = asset.AssetFiles.Create(Path.GetFileName(filePath));
        assetFile.Upload(filePath);

        return asset;
    }

    static IMediaProcessor GetLatestMediaProcessorByName(string mediaProcessorName)
    {
        var processor = context.MediaProcessors
        .Where(p => p.Name == mediaProcessorName)
        .ToList()
        .OrderBy(p => new Version(p.Version))
        .LastOrDefault();

        if (processor == null)
            throw new ArgumentException(string.Format("Unknown media processor",
                                                       mediaProcessorName));

        return processor;
    }

### <span data-ttu-id="36639-135"><a id="file_types"></a>Obsługiwane typy plików</span><span class="sxs-lookup"><span data-stu-id="36639-135"><a id="file_types"></a>Supported File types</span></span>
* <span data-ttu-id="36639-136">MP4</span><span class="sxs-lookup"><span data-stu-id="36639-136">MP4</span></span>
* <span data-ttu-id="36639-137">MOV</span><span class="sxs-lookup"><span data-stu-id="36639-137">MOV</span></span>
* <span data-ttu-id="36639-138">WMV</span><span class="sxs-lookup"><span data-stu-id="36639-138">WMV</span></span>

## <a name="media-services-learning-paths"></a><span data-ttu-id="36639-139">Ścieżki szkoleniowe dotyczące usługi Media Services</span><span class="sxs-lookup"><span data-stu-id="36639-139">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="36639-140">Przekazywanie opinii</span><span class="sxs-lookup"><span data-stu-id="36639-140">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="related-links"></a><span data-ttu-id="36639-141">Powiązane linki</span><span class="sxs-lookup"><span data-stu-id="36639-141">Related links</span></span>
[<span data-ttu-id="36639-142">Przegląd analiz usługi Azure Media Services</span><span class="sxs-lookup"><span data-stu-id="36639-142">Azure Media Services Analytics Overview</span></span>](media-services-analytics-overview.md)

[<span data-ttu-id="36639-143">W trakcie analizy multimediów Azure</span><span class="sxs-lookup"><span data-stu-id="36639-143">Azure Media Analytics demos</span></span>](http://azuremedialabs.azurewebsites.net/demos/Analytics.html)

