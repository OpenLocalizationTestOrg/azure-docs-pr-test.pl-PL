---
title: "aaaUse miniatur wideo multimediów Azure tooCreate podsumowań wideo | Dokumentacja firmy Microsoft"
description: "Podsumowanie wideo mogą pomóc tworzyć podsumowania długich filmów wideo, wybierając automatycznie interesujące wstawki z hello źródła wideo. Jest to przydatne, należy tooprovide szybki przegląd tooexpect które długie wideo."
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: a245529f-3150-4afc-93ec-e40d8a6b761d
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 07/18/2017
ms.author: milanga;juliako;
ms.openlocfilehash: 0a8f0bba6c12a948b940114fe4937e675688a8c7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-media-video-thumbnails-toocreate-a-video-summarization"></a><span data-ttu-id="da52e-104">Użyj tooCreate miniatur wideo multimediów Azure podsumowań wideo</span><span class="sxs-lookup"><span data-stu-id="da52e-104">Use Azure Media Video Thumbnails tooCreate a Video Summarization</span></span>
## <a name="overview"></a><span data-ttu-id="da52e-105">Omówienie</span><span class="sxs-lookup"><span data-stu-id="da52e-105">Overview</span></span>
<span data-ttu-id="da52e-106">Witaj **miniatur wideo multimediów Azure** procesor multimediów (MP) umożliwia toocreate podsumowanie wideo jest przydatne toocustomers, która po prostu chcesz toopreview podsumowanie wideo długo.</span><span class="sxs-lookup"><span data-stu-id="da52e-106">hello **Azure Media Video Thumbnails** media processor (MP) enables you toocreate a summary of a video that is useful toocustomers who just want toopreview a summary of a long video.</span></span> <span data-ttu-id="da52e-107">Na przykład klienci mogą też chcieć toosee "krótko wideo" gdy umieść kursor nad miniatury.</span><span class="sxs-lookup"><span data-stu-id="da52e-107">For example, customers might want toosee a short "summary video" when they hover over a thumbnail.</span></span> <span data-ttu-id="da52e-108">Przez dostosowywanie parametrów hello **miniatur wideo multimediów Azure** za pomocą ustawienia domyślne konfiguracji, może użyć zaawansowanego wykrywania zrzut hello w pakiecie Administracyjnym i łączenia technologii tooalgorithmically Generowanie subclip opisowy.</span><span class="sxs-lookup"><span data-stu-id="da52e-108">By tweaking hello parameters of **Azure Media Video Thumbnails** through a configuration preset, you can use hello MP's powerful shot detection and concatenation technology tooalgorithmically generate a descriptive subclip.</span></span>  

<span data-ttu-id="da52e-109">Witaj **miniatur wideo multimediów Azure** pakiet administracyjny jest obecnie w przeglądzie.</span><span class="sxs-lookup"><span data-stu-id="da52e-109">hello **Azure Media Video Thumbnail** MP is currently in Preview.</span></span>

<span data-ttu-id="da52e-110">Ten temat zawiera szczegółowe informacje o **miniatur wideo multimediów Azure** i przedstawia sposób toouse go przy użyciu zestawu SDK usługi Media Services dla platformy .NET.</span><span class="sxs-lookup"><span data-stu-id="da52e-110">This topic gives details about  **Azure Media Video Thumbnail** and shows how toouse it with Media Services SDK for .NET.</span></span>

## <a name="limitations"></a><span data-ttu-id="da52e-111">Ograniczenia</span><span class="sxs-lookup"><span data-stu-id="da52e-111">Limitations</span></span>

<span data-ttu-id="da52e-112">W niektórych przypadkach Jeśli wideo nie składa się z różnych scen hello dane wyjściowe będą mieć tylko jeden zrzut.</span><span class="sxs-lookup"><span data-stu-id="da52e-112">In some cases, if your video is not comprised of different scenes, hello output will only be a single shot.</span></span>

## <a name="video-summary-example"></a><span data-ttu-id="da52e-113">Przykład podsumowanie wideo</span><span class="sxs-lookup"><span data-stu-id="da52e-113">Video summary example</span></span>
<span data-ttu-id="da52e-114">Oto kilka przykładów procesor multimediów jakie hello miniatur wideo multimediów Azure można wykonać:</span><span class="sxs-lookup"><span data-stu-id="da52e-114">Here are some examples of what hello Azure Media Video Thumbnails media processor can do:</span></span>

### <a name="original-video"></a><span data-ttu-id="da52e-115">Oryginalnego wideo</span><span class="sxs-lookup"><span data-stu-id="da52e-115">Original video</span></span>
[<span data-ttu-id="da52e-116">Oryginalnego wideo</span><span class="sxs-lookup"><span data-stu-id="da52e-116">Original video</span></span>](http://ampdemo.azureedge.net/azuremediaplayer.html?url=https%3A%2F%2Fnimbuscdn-nimbuspm.streaming.mediaservices.windows.net%2Faed33834-ec2d-4788-88b5-a4505b3d032c%2FMicrosoft%27s%20HoloLens%20Live%20Demonstration.ism%2Fmanifest)

### <a name="video-thumbnail-result"></a><span data-ttu-id="da52e-117">Wynik miniatur wideo</span><span class="sxs-lookup"><span data-stu-id="da52e-117">Video thumbnail result</span></span>
[<span data-ttu-id="da52e-118">Wynik miniatur wideo</span><span class="sxs-lookup"><span data-stu-id="da52e-118">Video thumbnail result</span></span>](http://ampdemo.azureedge.net/azuremediaplayer.html?url=http%3A%2F%2Fnimbuscdn-nimbuspm.streaming.mediaservices.windows.net%2Ff5c91052-4232-41d4-b531-062e07b6a9ae%2FHololens%2520Demo_VideoThumbnails_MotionThumbnail.mp4)

## <a name="task-configuration-preset"></a><span data-ttu-id="da52e-119">Konfiguracja zadania (ustawienia domyślne)</span><span class="sxs-lookup"><span data-stu-id="da52e-119">Task configuration (preset)</span></span>
<span data-ttu-id="da52e-120">Podczas tworzenia zadania miniatur wideo z **miniatur wideo multimediów Azure**, należy określić ustawienia domyślne konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="da52e-120">When creating a video thumbnail task with **Azure Media Video Thumbnails**, you must specify a configuration preset.</span></span> <span data-ttu-id="da52e-121">Hello powyżej miniatur próbki utworzono za pomocą powitania od podstawowej konfiguracji JSON:</span><span class="sxs-lookup"><span data-stu-id="da52e-121">hello above thumbnail sample was created with hello following basic JSON configuration:</span></span>

    {"version":"1.0"}

<span data-ttu-id="da52e-122">Obecnie można zmienić hello następujące parametry:</span><span class="sxs-lookup"><span data-stu-id="da52e-122">Currently, you can change hello following parameters:</span></span>

| <span data-ttu-id="da52e-123">Param</span><span class="sxs-lookup"><span data-stu-id="da52e-123">Param</span></span> | <span data-ttu-id="da52e-124">Opis</span><span class="sxs-lookup"><span data-stu-id="da52e-124">Description</span></span> |
| --- | --- |
| <span data-ttu-id="da52e-125">outputAudio</span><span class="sxs-lookup"><span data-stu-id="da52e-125">outputAudio</span></span> |<span data-ttu-id="da52e-126">Określa, czy wideo wynikowe hello zawiera żadnego dźwięku.</span><span class="sxs-lookup"><span data-stu-id="da52e-126">Specifies whether or not hello resultant video contains any audio.</span></span> <br/><span data-ttu-id="da52e-127">Dozwolone wartości to: True lub False.</span><span class="sxs-lookup"><span data-stu-id="da52e-127">Allowed values are: True or False.</span></span> <span data-ttu-id="da52e-128">Domyślna wartość to True.</span><span class="sxs-lookup"><span data-stu-id="da52e-128">Default is True.</span></span> |
| <span data-ttu-id="da52e-129">fadeInFadeOut</span><span class="sxs-lookup"><span data-stu-id="da52e-129">fadeInFadeOut</span></span> |<span data-ttu-id="da52e-130">Określa, czy przejścia zanikania służą między hello oddzielne ruchu miniatur.</span><span class="sxs-lookup"><span data-stu-id="da52e-130">Specifies whether or not fade transitions are used between hello separate motion thumbnails.</span></span>  <br/><span data-ttu-id="da52e-131">Dozwolone wartości to: True lub False.</span><span class="sxs-lookup"><span data-stu-id="da52e-131">Allowed values are: True or False.</span></span>  <span data-ttu-id="da52e-132">Domyślna wartość to True.</span><span class="sxs-lookup"><span data-stu-id="da52e-132">Default is True.</span></span> |
| <span data-ttu-id="da52e-133">maxMotionThumbnailDurationInSecs</span><span class="sxs-lookup"><span data-stu-id="da52e-133">maxMotionThumbnailDurationInSecs</span></span> |<span data-ttu-id="da52e-134">Liczba całkowita, która określa, jak długo hello całe wideo wynikowe są.</span><span class="sxs-lookup"><span data-stu-id="da52e-134">Integer that specifies how long hello entire resultant video shall be.</span></span>  <span data-ttu-id="da52e-135">Domyślna zależy od oryginalnego wideo czasu trwania.</span><span class="sxs-lookup"><span data-stu-id="da52e-135">Default depends on original video duration.</span></span> |

<span data-ttu-id="da52e-136">Witaj poniższej tabeli opisano hello domyślny czas trwania, gdy **maxMotionThumbnailInSecs** nie jest używany.</span><span class="sxs-lookup"><span data-stu-id="da52e-136">hello following table describes hello default duration, when **maxMotionThumbnailInSecs** is not used.</span></span>

|  |  |  |
| --- | --- | --- | --- | --- |
| <span data-ttu-id="da52e-137">Czas trwania wideo</span><span class="sxs-lookup"><span data-stu-id="da52e-137">Video duration</span></span> |<span data-ttu-id="da52e-138">d < 3 min</span><span class="sxs-lookup"><span data-stu-id="da52e-138">d < 3 min</span></span> |<span data-ttu-id="da52e-139">3 min < d < 15 min</span><span class="sxs-lookup"><span data-stu-id="da52e-139">3 min < d < 15 min</span></span> |
| <span data-ttu-id="da52e-140">Czas trwania miniatur</span><span class="sxs-lookup"><span data-stu-id="da52e-140">Thumbnail duration</span></span> |<span data-ttu-id="da52e-141">s 15 (sceny 2 – 3)</span><span class="sxs-lookup"><span data-stu-id="da52e-141">15 sec (2-3 scenes)</span></span> |<span data-ttu-id="da52e-142">30 sekund (3 – 5 sceny)</span><span class="sxs-lookup"><span data-stu-id="da52e-142">30 sec (3-5 scenes)</span></span> |

<span data-ttu-id="da52e-143">Witaj następujące JSON ustawia dostępne parametry.</span><span class="sxs-lookup"><span data-stu-id="da52e-143">hello following JSON sets available parameters.</span></span>

    {
        "version": "1.0",
        "options": {
            "outputAudio": "true",
            "maxMotionThumbnailDurationInSecs": "10",
            "fadeInFadeOut": "true"
        }
    }

## <a name="net-sample-code"></a><span data-ttu-id="da52e-144">.NET przykładowy kod</span><span class="sxs-lookup"><span data-stu-id="da52e-144">.NET sample code</span></span>

<span data-ttu-id="da52e-145">następujące Hello program pokazuje sposób:</span><span class="sxs-lookup"><span data-stu-id="da52e-145">hello following program shows how to:</span></span>

1. <span data-ttu-id="da52e-146">Utworzenie elementu zawartości i przesyłanie pliku multimediów do hello zawartości.</span><span class="sxs-lookup"><span data-stu-id="da52e-146">Create an asset and upload a media file into hello asset.</span></span>
2. <span data-ttu-id="da52e-147">Tworzy zadanie z zadaniem miniatur wideo oparty na pliku konfiguracji, który zawiera hello następujące ustawienie wstępne json.</span><span class="sxs-lookup"><span data-stu-id="da52e-147">Creates a job with a video thumbnail task based on a configuration file that contains hello following json preset.</span></span> 
   
        {                
            "version": "1.0",
            "options": {
                "outputAudio": "true",
                "maxMotionThumbnailDurationInSecs": "30",
                "fadeInFadeOut": "false"
            }
        }
3. <span data-ttu-id="da52e-148">Pobiera pliki wyjściowe hello.</span><span class="sxs-lookup"><span data-stu-id="da52e-148">Downloads hello output files.</span></span> 

#### <a name="create-and-configure-a-visual-studio-project"></a><span data-ttu-id="da52e-149">Tworzenie i konfigurowanie projektu programu Visual Studio</span><span class="sxs-lookup"><span data-stu-id="da52e-149">Create and configure a Visual Studio project</span></span>

<span data-ttu-id="da52e-150">Konfigurowanie środowiska projektowego i wypełnić plik app.config hello o informacje dotyczące połączenia, zgodnie z opisem w [tworzenia usługi Media Services z platformą .NET](media-services-dotnet-how-to-use.md).</span><span class="sxs-lookup"><span data-stu-id="da52e-150">Set up your development environment and populate hello app.config file with connection information, as described in [Media Services development with .NET](media-services-dotnet-how-to-use.md).</span></span> 

#### <a name="example"></a><span data-ttu-id="da52e-151">Przykład</span><span class="sxs-lookup"><span data-stu-id="da52e-151">Example</span></span>

    using System;
    using System.Configuration;
    using System.IO;
    using System.Linq;
    using Microsoft.WindowsAzure.MediaServices.Client;
    using System.Threading;
    using System.Threading.Tasks;

    namespace VideoSummarization
    {
        class Program
        {
            // Read values from hello App.config file.
            private static readonly string _AADTenantDomain =
                ConfigurationManager.AppSettings["AADTenantDomain"];
            private static readonly string _RESTAPIEndpoint =
                ConfigurationManager.AppSettings["MediaServiceRESTAPIEndpoint"];

            // Field for service context.
            private static CloudMediaContext _context = null;

            static void Main(string[] args)
            {
                var tokenCredentials = new AzureAdTokenCredentials(_AADTenantDomain, AzureEnvironments.AzureCloudEnvironment);
                var tokenProvider = new AzureAdTokenProvider(tokenCredentials);

                _context = new CloudMediaContext(new Uri(_RESTAPIEndpoint), tokenProvider);


                // Run hello thumbnail job.
                var asset = RunVideoThumbnailJob(@"C:\supportFiles\VideoThumbnail\BigBuckBunny.mp4",
                                            @"C:\supportFiles\VideoThumbnail\config.json");

                // Download hello job output asset.
                DownloadAsset(asset, @"C:\supportFiles\VideoThumbnail\Output");
            }

            static IAsset RunVideoThumbnailJob(string inputMediaFilePath, string configurationFile)
            {
                // Create an asset and upload hello input media file toostorage.
                IAsset asset = CreateAssetAndUploadSingleFile(inputMediaFilePath,
                    "My Video Thumbnail Input Asset",
                    AssetCreationOptions.None);

                // Declare a new job.
                IJob job = _context.Jobs.Create("My Video Thumbnail Job");

                // Get a reference tooAzure Media Video Thumbnails.
                string MediaProcessorName = "Azure Media Video Thumbnails";

                var processor = GetLatestMediaProcessorByName(MediaProcessorName);

                // Read configuration from hello specified file.
                string configuration = File.ReadAllText(configurationFile);

                // Create a task with hello encoding details, using a string preset.
                ITask task = job.Tasks.AddNew("My Video Thumbnail Task",
                    processor,
                    configuration,
                    TaskOptions.None);

                // Specify hello input asset.
                task.InputAssets.Add(asset);

                // Add an output asset toocontain hello results of hello job.
                task.OutputAssets.AddNew("My Video Thumbnail Output Asset", AssetCreationOptions.None);

                // Use hello following event handler toocheck job progress.  
                job.StateChanged += new EventHandler<JobStateChangedEventArgs>(StateChanged);

                // Launch hello job.
                job.Submit();

                // Check job execution and wait for job toofinish.
                Task progressJobTask = job.GetExecutionProgressTask(CancellationToken.None);

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
                    return null;
                }

                return job.OutputMediaAssets[0];
            }

            static IAsset CreateAssetAndUploadSingleFile(string filePath, string assetName, AssetCreationOptions options)
            {
                IAsset asset = _context.Assets.Create(assetName, options);

                var assetFile = asset.AssetFiles.Create(Path.GetFileName(filePath));
                assetFile.Upload(filePath);

                return asset;
            }

            static void DownloadAsset(IAsset asset, string outputDirectory)
            {
                foreach (IAssetFile file in asset.AssetFiles)
                {
                    file.Download(Path.Combine(outputDirectory, file.Name));
                }
            }

            static IMediaProcessor GetLatestMediaProcessorByName(string mediaProcessorName)
            {
                var processor = _context.MediaProcessors
                    .Where(p => p.Name == mediaProcessorName)
                    .ToList()
                    .OrderBy(p => new Version(p.Version))
                    .LastOrDefault();

                if (processor == null)
                    throw new ArgumentException(string.Format("Unknown media processor",
                                                               mediaProcessorName));

                return processor;
            }

            static private void StateChanged(object sender, JobStateChangedEventArgs e)
            {
                Console.WriteLine("Job state changed event:");
                Console.WriteLine("  Previous state: " + e.PreviousState);
                Console.WriteLine("  Current state: " + e.CurrentState);

                switch (e.CurrentState)
                {
                    case JobState.Finished:
                        Console.WriteLine();
                        Console.WriteLine("Job is finished.");
                        Console.WriteLine();
                        break;
                    case JobState.Canceling:
                    case JobState.Queued:
                    case JobState.Scheduled:
                    case JobState.Processing:
                        Console.WriteLine("Please wait...\n");
                        break;
                    case JobState.Canceled:
                    case JobState.Error:
                        // Cast sender as a job.
                        IJob job = (IJob)sender;
                        // Display or log error details as needed.
                        // LogJobStop(job.Id);
                        break;
                    default:
                        break;
                }
            }

        }
    }

### <a name="video-thumbnail-output"></a><span data-ttu-id="da52e-152">Wyjście miniatur wideo</span><span class="sxs-lookup"><span data-stu-id="da52e-152">Video thumbnail output</span></span>
[<span data-ttu-id="da52e-153">Wyjście miniatur wideo</span><span class="sxs-lookup"><span data-stu-id="da52e-153">Video thumbnail output</span></span>](http://ampdemo.azureedge.net/azuremediaplayer.html?url=http%3A%2F%2Fnimbuscdn-nimbuspm.streaming.mediaservices.windows.net%2Fd06f24dc-bc81-488e-a8d0-348b7dc41b56%2FHololens%2520Demo_VideoThumbnails_MotionThumbnail.mp4)

## <a name="media-services-learning-paths"></a><span data-ttu-id="da52e-154">Ścieżki szkoleniowe dotyczące usługi Media Services</span><span class="sxs-lookup"><span data-stu-id="da52e-154">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="da52e-155">Przekazywanie opinii</span><span class="sxs-lookup"><span data-stu-id="da52e-155">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="related-links"></a><span data-ttu-id="da52e-156">Powiązane linki</span><span class="sxs-lookup"><span data-stu-id="da52e-156">Related links</span></span>
[<span data-ttu-id="da52e-157">Przegląd analiz usługi Azure Media Services</span><span class="sxs-lookup"><span data-stu-id="da52e-157">Azure Media Services Analytics Overview</span></span>](media-services-analytics-overview.md)

[<span data-ttu-id="da52e-158">W trakcie analizy multimediów Azure</span><span class="sxs-lookup"><span data-stu-id="da52e-158">Azure Media Analytics demos</span></span>](http://azuremedialabs.azurewebsites.net/demos/Analytics.html)

