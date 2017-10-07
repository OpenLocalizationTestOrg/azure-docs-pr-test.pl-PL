---
title: "aaaIndexing plików multimedialnych na pliki z usługi Azure Media indeksatora 2 w wersji zapoznawczej | Dokumentacja firmy Microsoft"
description: "Indeksator usługi Azure Media pozwala toomake zawartości z możliwością wyszukiwania plików multimedialnych i toogenerate wykaz pełnotekstowy dla i słów kluczowych. W tym temacie przedstawiono sposób Podgląd toouse indeksatora multimediów 2."
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: 85d25525-a498-44eb-ae3a-2ca5ceb8e53d
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 07/31/2017
ms.author: adsolank;juliako;
ms.openlocfilehash: f83fa0db58b828ffa29933d68ce108b4906dcd78
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="indexing-media-files-with-azure-media-indexer-2-preview"></a>Indeksowanie plików multimedialnych na pliki z podglądem indeksatora 2 multimediów Azure
## <a name="overview"></a>Omówienie
Witaj **Azure Media indeksatora 2 w wersji zapoznawczej** procesor multimediów (MP) pozwala toomake plików multimedialnych i zawartości można wyszukiwać, również generowanie zamkniętego śledzi podpisów. Porównaniu toohello poprzedniej wersji [Azure Media indeksatora](media-services-index-content.md), **Azure Media indeksatora 2 w wersji zapoznawczej** wykonuje indeksowania szybsze i zapewnia szerszy obsługę języka. Obsługiwane języki angielski, hiszpański, francuski, niemiecki, włoski, chiński (mandaryński, uproszczony), portugalski, arabskiego i japoński.

Witaj **Azure Media indeksatora 2 w wersji zapoznawczej** pakiet administracyjny jest obecnie w przeglądzie.

W tym temacie pokazano, jak indeksowania toocreate zadania z **Azure Media indeksatora 2 w wersji zapoznawczej**.

> [!NOTE]
> Zastosuj Hello następujące zagadnienia:
> 
> Indeksator 2 nie jest obsługiwana w chińskiej wersji platformy Azure i Azure dla instytucji rządowych.
> 
> Podczas indeksowania zawartości, upewnij się, że toouse plików multimedialnych, które mają bardzo jasne mowy (bez muzyką w tle, szumu, efekty lub szumów mikrofonu). Oto kilka przykładów odpowiedniej zawartości: rejestrowane spotkań, wykładów lub prezentacji. Witaj następującej zawartości może nie nadawać się do indeksowania: filmy, programy telewizyjne, wszystko z mieszanym audio i efekty, nieprawidłowo zarejestrowana zawartości za pomocą szumu tła (szumów).
> 
> 

Ten temat zawiera szczegółowe informacje o **Azure Media indeksatora 2 w wersji zapoznawczej** i przedstawia sposób toouse go przy użyciu zestawu SDK usługi Media Services dla platformy .NET

## <a name="input-and-output-files"></a>Pliki wejściowe i wyjściowe
### <a name="input-files"></a>Pliki wejściowe
Plików audio i wideo

### <a name="output-files"></a>Pliki wyjściowe
Zadania indeksowania mogą generować pliki napisów w hello następujących formatów:  

* **SAMI**
* **TTML**
* **WebVTT**

Zamkniętych plikach podpis (DW) w tych formatach może być używane toomake audio i wideo pliki dostępny toopeople niepełnosprawne przesłuchanie.

## <a name="task-configuration-preset"></a>Konfiguracja zadania (ustawienia domyślne)
Podczas tworzenia indeksowania zadań z **Azure Media indeksatora 2 w wersji zapoznawczej**, należy określić ustawienia domyślne konfiguracji.

Witaj następujące JSON ustawia dostępne parametry.

    {
      "version":"1.0",
      "Features":
        [
           {
           "Options": {
                "Formats":["WebVtt","ttml"],
                "Language":"enUs",
                "Type":"RecoOptions"
           },
           "Type":"SpReco"
        }]
    }

## <a name="supported-languages"></a>Obsługiwane języki
Wersja zapoznawcza usługi Azure Media indeksatora 2 obsługuje mowy na tekst hello następujących języków (podczas określania nazwy języka hello na powitania zadań konfiguracji, użyj 4-znakowy kod w nawiasach, jak pokazano poniżej):

* Angielski [EnUs]
* Hiszpański [EsEs]
* Chiński (mandaryński, uproszczone) [ZhCn]
* Francuski [FrFr]
* Niemiecki [DeDe]
* Włoski [ItIt]
* Portugalski [PtBr]
* Arabski (egipska) [ArEg]
* Japoński [JaJp]
* Federacja [RuRu]
* Angielski (brytyjski) [EnGb]
* Amerykańską [EsMx] 

## <a name="supported-file-types"></a>Obsługiwane typy plików

Aby uzyskać informacje na temat typów plików obsługiwanych Zobacz hello [obsługiwane formaty/koderów-dekoderów](media-services-media-encoder-standard-formats.md#input-containerfile-formats) sekcji.

## <a name="net-sample-code"></a>.NET przykładowy kod

następujące Hello program pokazuje sposób:

1. Utworzenie elementu zawartości i przesyłanie pliku multimediów do hello zawartości.
2. Utwórz zadanie zadania indeksowania oparty na pliku konfiguracji, który zawiera hello następujące ustawienie wstępne json.
   
        {
          "version":"1.0",
          "Features":
            [
               {
               "Options": {
                    "Formats":["WebVtt","ttml"],
                    "Language":"enUs",
                    "Type":"RecoOptions"
               },
               "Type":"SpReco"
            }]
        }
3. Pobierz pliki wyjściowe hello. 
   
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

    namespace IndexContent
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

                // Run indexing job.
                var asset = RunIndexingJob(@"C:\supportFiles\Indexer\BigBuckBunny.mp4",
                                            @"C:\supportFiles\Indexer\config.json");

                // Download hello job output asset.
                DownloadAsset(asset, @"C:\supportFiles\Indexer\Output");
            }

            static IAsset RunIndexingJob(string inputMediaFilePath, string configurationFile)
            {
                // Create an asset and upload hello input media file toostorage.
                IAsset asset = CreateAssetAndUploadSingleFile(inputMediaFilePath,
                    "My Indexing Input Asset",
                    AssetCreationOptions.None);

                // Declare a new job.
                IJob job = _context.Jobs.Create("My Indexing Job");

                // Get a reference tooAzure Media Indexer 2 Preview.
                string MediaProcessorName = "Azure Media Indexer 2 Preview";

                var processor = GetLatestMediaProcessorByName(MediaProcessorName);

                // Read configuration from hello specified file.
                string configuration = File.ReadAllText(configurationFile);

                // Create a task with hello encoding details, using a string preset.
                ITask task = job.Tasks.AddNew("My Indexing Task",
                    processor,
                    configuration,
                    TaskOptions.None);

                // Specify hello input asset toobe indexed.
                task.InputAssets.Add(asset);

                // Add an output asset toocontain hello results of hello job.
                task.OutputAssets.AddNew("My Indexing Output Asset", AssetCreationOptions.None);

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

## <a name="media-services-learning-paths"></a>Ścieżki szkoleniowe dotyczące usługi Media Services
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Przekazywanie opinii
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="related-links"></a>Powiązane linki
[Przegląd analiz usługi Azure Media Services](media-services-analytics-overview.md)

[W trakcie analizy multimediów Azure](http://azuremedialabs.azurewebsites.net/demos/Analytics.html)

