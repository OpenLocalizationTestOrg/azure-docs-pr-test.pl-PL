---
title: "Plikach multimedialnych przyspieszonych ujęć poklatkowych za pomocą usługi Azure Media Hyperlapse | Dokumentacja firmy Microsoft"
description: "Azure Media Hyperlapse tworzy smooth czas, jaki upłynął wideo z pierwszą osobą lub akcji aparatu zawartości. W tym temacie pokazano, jak używać nośnika indeksatora."
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
ms.openlocfilehash: 02f634c2af04b6b372642ab0e6a17a5d29f16450
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="hyperlapse-media-files-with-azure-media-hyperlapse"></a><span data-ttu-id="545ee-104">Plikach multimedialnych przyspieszonych ujęć poklatkowych za pomocą usługi Azure Media Hyperlapse</span><span class="sxs-lookup"><span data-stu-id="545ee-104">Hyperlapse Media Files with Azure Media Hyperlapse</span></span>
<span data-ttu-id="545ee-105">Azure Media Hyperlapse jest nośnik procesora (MP) tworzącą smooth czas, jaki upłynął wideo z pierwszą osobą lub akcji aparatu zawartości.</span><span class="sxs-lookup"><span data-stu-id="545ee-105">Azure Media Hyperlapse is a Media Processor (MP) that creates smooth time-lapsed videos from first-person or action-camera content.</span></span>  <span data-ttu-id="545ee-106">Element równorzędny oparte na chmurze do [desktop Pro przyspieszonych ujęć poklatkowych i opartych na telefon komórkowy przyspieszonych ujęć poklatkowych Microsoft Research](http://aka.ms/hyperlapse), Hyperlapse firmy Microsoft dla usługi Azure Media Services używa bardzo dużej skali przetwarzania Media Services multimediów Azure Platforma na poziomie skalowanie i parallelize zbiorcze przyspieszonych ujęć poklatkowych przetwarzania.</span><span class="sxs-lookup"><span data-stu-id="545ee-106">The cloud-based sibling to [Microsoft Research's desktop Hyperlapse Pro and phone-based Hyperlapse Mobile](http://aka.ms/hyperlapse), Microsoft Hyperlapse for Azure Media Services utilizes the massive scale of the Azure Media Services Media Processing platform to horizontally scale and parallelize bulk Hyperlapse processing.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="545ee-107">Microsoft Hyperlapse jest zaprojektowana by najlepiej pracować na pierwszą osobą zawartości za pomocą przenoszenia aparatu.</span><span class="sxs-lookup"><span data-stu-id="545ee-107">Microsoft Hyperlapse is designed to work best on first-person content with a moving camera.</span></span>  <span data-ttu-id="545ee-108">Mimo że nadal kamery może nadal działać, wydajności i jakości procesor multimediów Azure Media przyspieszonych ujęć poklatkowych nie można zagwarantować dla innych typów zawartości.</span><span class="sxs-lookup"><span data-stu-id="545ee-108">Although still-camera footage can still work, the performance and quality of the Azure Media Hyperlapse Media Processor cannot be guaranteed for other types of content.</span></span>  <span data-ttu-id="545ee-109">Aby dowiedzieć się więcej o Hyperlapse firmy Microsoft dla usługi Azure Media Services i wyświetlić niektóre przykładowe filmy, zapoznaj się [wprowadzające wpis w blogu](http://aka.ms/azurehyperlapseblog) z publicznej wersji zapoznawczej.</span><span class="sxs-lookup"><span data-stu-id="545ee-109">To learn more about Microsoft Hyperlapse for Azure Media Services and see some example videos, check out the [introductory blog post](http://aka.ms/azurehyperlapseblog) from the public preview.</span></span>
> 
> 

<span data-ttu-id="545ee-110">Azure Media Hyperlapse zadania przyjmuje jako plik wejściowy elementu MP4, MOV lub WMV zasobów wraz z plikiem konfiguracji, który określa, które ramki wideo powinna być czas, jaki upłynął i jakie szybkości (np. pierwszych 10 000 ramek, x 2).</span><span class="sxs-lookup"><span data-stu-id="545ee-110">An Azure Media Hyperlapse job takes as input an MP4, MOV, or WMV asset file along with a configuration file that specifies which frames of video should be time-lapsed and to what speed (e.g. first 10,000 frames at 2x).</span></span>  <span data-ttu-id="545ee-111">Dane wyjściowe są stabilnych i czas, jaki upłynął dobór wejściowego pliku wideo.</span><span class="sxs-lookup"><span data-stu-id="545ee-111">The output is a stabilized and time-lapsed rendition of the input video.</span></span>

<span data-ttu-id="545ee-112">Najnowsze aktualizacje usługi Azure Media Hyperlapse, zobacz [blogi Media Services](https://azure.microsoft.com/blog/topics/media-services/).</span><span class="sxs-lookup"><span data-stu-id="545ee-112">For the latest Azure Media Hyperlapse updates, see [Media Services blogs](https://azure.microsoft.com/blog/topics/media-services/).</span></span>

## <a name="hyperlapse-an-asset"></a><span data-ttu-id="545ee-113">Przyspieszonych ujęć poklatkowych zasobów</span><span class="sxs-lookup"><span data-stu-id="545ee-113">Hyperlapse an asset</span></span>
<span data-ttu-id="545ee-114">Najpierw należy przesłać żądany plik wejściowy do usługi Azure Media Services.</span><span class="sxs-lookup"><span data-stu-id="545ee-114">First you will need to upload your desired input file to Azure Media Services.</span></span>  <span data-ttu-id="545ee-115">Aby dowiedzieć się więcej na temat pojęć związanych z przekazywanie i zarządzania zawartością, przeczytaj [zarządzania zawartością artykułu](media-services-portal-vod-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="545ee-115">To learn more about the concepts involved with uploading and managing content, read the [content management article](media-services-portal-vod-get-started.md).</span></span>

### <span data-ttu-id="545ee-116"><a id="configuration"></a>Ustawienie konfiguracji dla przyspieszonych ujęć poklatkowych</span><span class="sxs-lookup"><span data-stu-id="545ee-116"><a id="configuration"></a>Configuration Preset for Hyperlapse</span></span>
<span data-ttu-id="545ee-117">Gdy zawartość jest na koncie usługi Media Services, należy utworzyć ustawienia konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="545ee-117">Once your content is in your Media Services account, you will need to construct your configuration preset.</span></span>  <span data-ttu-id="545ee-118">W poniższej tabeli opisano pola określone przez użytkownika:</span><span class="sxs-lookup"><span data-stu-id="545ee-118">The following table explains the user-specified fields:</span></span>

| <span data-ttu-id="545ee-119">Pole</span><span class="sxs-lookup"><span data-stu-id="545ee-119">Field</span></span> | <span data-ttu-id="545ee-120">Opis</span><span class="sxs-lookup"><span data-stu-id="545ee-120">Description</span></span> |
| --- | --- |
| <span data-ttu-id="545ee-121">StartFrame</span><span class="sxs-lookup"><span data-stu-id="545ee-121">StartFrame</span></span> |<span data-ttu-id="545ee-122">Ramka, na którym powinny one zacząć przetwarzania Hyperlapse firmy Microsoft.</span><span class="sxs-lookup"><span data-stu-id="545ee-122">The frame upon which the Microsoft Hyperlapse processing should begin.</span></span> |
| <span data-ttu-id="545ee-123">NumFrames</span><span class="sxs-lookup"><span data-stu-id="545ee-123">NumFrames</span></span> |<span data-ttu-id="545ee-124">Liczba ramek do przetworzenia</span><span class="sxs-lookup"><span data-stu-id="545ee-124">The number of frames to process</span></span> |
| <span data-ttu-id="545ee-125">Szybkość</span><span class="sxs-lookup"><span data-stu-id="545ee-125">Speed</span></span> |<span data-ttu-id="545ee-126">Współczynnik, z którą ma zostać przyspieszenia wejściowy plik wideo.</span><span class="sxs-lookup"><span data-stu-id="545ee-126">The factor with which to speed up the input video.</span></span> |

<span data-ttu-id="545ee-127">Poniżej przedstawiono przykładowy plik konfiguracji zgodność w pliku XML i JSON:</span><span class="sxs-lookup"><span data-stu-id="545ee-127">The following is an example of a conformant configuration file in XML and JSON:</span></span>

<span data-ttu-id="545ee-128">**Ustawienie wstępne XML:**</span><span class="sxs-lookup"><span data-stu-id="545ee-128">**XML preset:**</span></span>

    <?xml version="1.0" encoding="utf-16"?>
    <Preset xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:xsd="http://www.w3.org/2001/XMLSchema" Version="1.0" xmlns="http://www.windowsazure.com/media/encoding/Preset/2014/03">
        <Sources>
            <Source StartFrame="0" NumFrames="10000" />
        </Sources>
        <Options>
            <Speed>12</Speed>
        </Options>
    </Preset>

<span data-ttu-id="545ee-129">**Ustawienie wstępne JSON:**</span><span class="sxs-lookup"><span data-stu-id="545ee-129">**JSON preset:**</span></span>

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

### <span data-ttu-id="545ee-130"><a id="sample_code"></a>Microsoft przyspieszonych ujęć poklatkowych przy użyciu zestawu SDK .NET usługi AMS</span><span class="sxs-lookup"><span data-stu-id="545ee-130"><a id="sample_code"></a> Microsoft Hyperlapse with the AMS .NET SDK</span></span>
<span data-ttu-id="545ee-131">Następująca metoda przekazuje plik nośnika jako zasób i tworzy zadanie z procesora Azure Media przyspieszonych ujęć poklatkowych nośnika.</span><span class="sxs-lookup"><span data-stu-id="545ee-131">The following method uploads a media file as an asset and creates a job with the Azure Media Hyperlapse Media Processor.</span></span>

> [!NOTE]
> <span data-ttu-id="545ee-132">CloudMediaContext ma już w zakresie o nazwie "context" dla tego kodu do pracy.</span><span class="sxs-lookup"><span data-stu-id="545ee-132">You should already have a CloudMediaContext in scope with the name "context" for this code to work.</span></span>  <span data-ttu-id="545ee-133">Aby dowiedzieć się więcej na ten temat, przeczytaj [zarządzania zawartością artykułu](media-services-dotnet-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="545ee-133">To learn more about this, read the [content management article](media-services-dotnet-get-started.md).</span></span>
> 
> [!NOTE]
> <span data-ttu-id="545ee-134">Argument ciągu "hyperConfig" powinien być konfiguracji zgodność ustawień w formacie JSON i XML, zgodnie z powyższym opisem.</span><span class="sxs-lookup"><span data-stu-id="545ee-134">The string argument "hyperConfig" is expected to be a conformant configuration preset in either JSON or XML as described above.</span></span>
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

            // If job state is Error, the event handling
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

### <span data-ttu-id="545ee-135"><a id="file_types"></a>Obsługiwane typy plików</span><span class="sxs-lookup"><span data-stu-id="545ee-135"><a id="file_types"></a>Supported File types</span></span>
* <span data-ttu-id="545ee-136">MP4</span><span class="sxs-lookup"><span data-stu-id="545ee-136">MP4</span></span>
* <span data-ttu-id="545ee-137">MOV</span><span class="sxs-lookup"><span data-stu-id="545ee-137">MOV</span></span>
* <span data-ttu-id="545ee-138">WMV</span><span class="sxs-lookup"><span data-stu-id="545ee-138">WMV</span></span>

## <a name="media-services-learning-paths"></a><span data-ttu-id="545ee-139">Ścieżki szkoleniowe dotyczące usługi Media Services</span><span class="sxs-lookup"><span data-stu-id="545ee-139">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="545ee-140">Przekazywanie opinii</span><span class="sxs-lookup"><span data-stu-id="545ee-140">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="related-links"></a><span data-ttu-id="545ee-141">Powiązane linki</span><span class="sxs-lookup"><span data-stu-id="545ee-141">Related links</span></span>
[<span data-ttu-id="545ee-142">Przegląd analiz usługi Azure Media Services</span><span class="sxs-lookup"><span data-stu-id="545ee-142">Azure Media Services Analytics Overview</span></span>](media-services-analytics-overview.md)

[<span data-ttu-id="545ee-143">W trakcie analizy multimediów Azure</span><span class="sxs-lookup"><span data-stu-id="545ee-143">Azure Media Analytics demos</span></span>](http://azuremedialabs.azurewebsites.net/demos/Analytics.html)

