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
# <a name="use-azure-media-video-thumbnails-toocreate-a-video-summarization"></a>Użyj tooCreate miniatur wideo multimediów Azure podsumowań wideo
## <a name="overview"></a>Omówienie
Witaj **miniatur wideo multimediów Azure** procesor multimediów (MP) umożliwia toocreate podsumowanie wideo jest przydatne toocustomers, która po prostu chcesz toopreview podsumowanie wideo długo. Na przykład klienci mogą też chcieć toosee "krótko wideo" gdy umieść kursor nad miniatury. Przez dostosowywanie parametrów hello **miniatur wideo multimediów Azure** za pomocą ustawienia domyślne konfiguracji, może użyć zaawansowanego wykrywania zrzut hello w pakiecie Administracyjnym i łączenia technologii tooalgorithmically Generowanie subclip opisowy.  

Witaj **miniatur wideo multimediów Azure** pakiet administracyjny jest obecnie w przeglądzie.

Ten temat zawiera szczegółowe informacje o **miniatur wideo multimediów Azure** i przedstawia sposób toouse go przy użyciu zestawu SDK usługi Media Services dla platformy .NET.

## <a name="limitations"></a>Ograniczenia

W niektórych przypadkach Jeśli wideo nie składa się z różnych scen hello dane wyjściowe będą mieć tylko jeden zrzut.

## <a name="video-summary-example"></a>Przykład podsumowanie wideo
Oto kilka przykładów procesor multimediów jakie hello miniatur wideo multimediów Azure można wykonać:

### <a name="original-video"></a>Oryginalnego wideo
[Oryginalnego wideo](http://ampdemo.azureedge.net/azuremediaplayer.html?url=https%3A%2F%2Fnimbuscdn-nimbuspm.streaming.mediaservices.windows.net%2Faed33834-ec2d-4788-88b5-a4505b3d032c%2FMicrosoft%27s%20HoloLens%20Live%20Demonstration.ism%2Fmanifest)

### <a name="video-thumbnail-result"></a>Wynik miniatur wideo
[Wynik miniatur wideo](http://ampdemo.azureedge.net/azuremediaplayer.html?url=http%3A%2F%2Fnimbuscdn-nimbuspm.streaming.mediaservices.windows.net%2Ff5c91052-4232-41d4-b531-062e07b6a9ae%2FHololens%2520Demo_VideoThumbnails_MotionThumbnail.mp4)

## <a name="task-configuration-preset"></a>Konfiguracja zadania (ustawienia domyślne)
Podczas tworzenia zadania miniatur wideo z **miniatur wideo multimediów Azure**, należy określić ustawienia domyślne konfiguracji. Hello powyżej miniatur próbki utworzono za pomocą powitania od podstawowej konfiguracji JSON:

    {"version":"1.0"}

Obecnie można zmienić hello następujące parametry:

| Param | Opis |
| --- | --- |
| outputAudio |Określa, czy wideo wynikowe hello zawiera żadnego dźwięku. <br/>Dozwolone wartości to: True lub False. Domyślna wartość to True. |
| fadeInFadeOut |Określa, czy przejścia zanikania służą między hello oddzielne ruchu miniatur.  <br/>Dozwolone wartości to: True lub False.  Domyślna wartość to True. |
| maxMotionThumbnailDurationInSecs |Liczba całkowita, która określa, jak długo hello całe wideo wynikowe są.  Domyślna zależy od oryginalnego wideo czasu trwania. |

Witaj poniższej tabeli opisano hello domyślny czas trwania, gdy **maxMotionThumbnailInSecs** nie jest używany.

|  |  |  |
| --- | --- | --- | --- | --- |
| Czas trwania wideo |d < 3 min |3 min < d < 15 min |
| Czas trwania miniatur |s 15 (sceny 2 – 3) |30 sekund (3 – 5 sceny) |

Witaj następujące JSON ustawia dostępne parametry.

    {
        "version": "1.0",
        "options": {
            "outputAudio": "true",
            "maxMotionThumbnailDurationInSecs": "10",
            "fadeInFadeOut": "true"
        }
    }

## <a name="net-sample-code"></a>.NET przykładowy kod

następujące Hello program pokazuje sposób:

1. Utworzenie elementu zawartości i przesyłanie pliku multimediów do hello zawartości.
2. Tworzy zadanie z zadaniem miniatur wideo oparty na pliku konfiguracji, który zawiera hello następujące ustawienie wstępne json. 
   
        {                
            "version": "1.0",
            "options": {
                "outputAudio": "true",
                "maxMotionThumbnailDurationInSecs": "30",
                "fadeInFadeOut": "false"
            }
        }
3. Pobiera pliki wyjściowe hello. 

#### <a name="create-and-configure-a-visual-studio-project"></a>Tworzenie i konfigurowanie projektu programu Visual Studio

Konfigurowanie środowiska projektowego i wypełnić plik app.config hello o informacje dotyczące połączenia, zgodnie z opisem w [tworzenia usługi Media Services z platformą .NET](media-services-dotnet-how-to-use.md). 

#### <a name="example"></a>Przykład

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

### <a name="video-thumbnail-output"></a>Wyjście miniatur wideo
[Wyjście miniatur wideo](http://ampdemo.azureedge.net/azuremediaplayer.html?url=http%3A%2F%2Fnimbuscdn-nimbuspm.streaming.mediaservices.windows.net%2Fd06f24dc-bc81-488e-a8d0-348b7dc41b56%2FHololens%2520Demo_VideoThumbnails_MotionThumbnail.mp4)

## <a name="media-services-learning-paths"></a>Ścieżki szkoleniowe dotyczące usługi Media Services
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Przekazywanie opinii
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="related-links"></a>Powiązane linki
[Przegląd analiz usługi Azure Media Services](media-services-analytics-overview.md)

[W trakcie analizy multimediów Azure](http://azuremedialabs.azurewebsites.net/demos/Analytics.html)

