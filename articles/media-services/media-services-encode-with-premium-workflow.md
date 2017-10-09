---
title: "kodowanie aaaAdvanced z przepływem pracy Premium kodera multimediów | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak tooencode z przepływem pracy Premium kodera multimediów. Przykłady kodu są napisane w języku C# i używają hello SDK usługi Media Services dla platformy .NET."
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: 0f4c87ac-810a-4d42-8df8-923dff2016c6
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/18/2017
ms.author: juliako
ms.openlocfilehash: 5a1c3d019a5c8fbf9bda2da751a7eff4c4907d97
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="advanced-encoding-with-media-encoder-premium-workflow"></a>Zaawansowane encoding w usłudze Media Encoder Premium w przepływie pracy
> [!NOTE]
> Procesor multimediów Media Encoder Premium w przepływie pracy omówione w tym temacie nie jest dostępna w Chinach.
>
>

Odpowiedzi na pytania koder premium poczty e-mail mepd z witryny Microsoft.com.

## <a name="overview"></a>Omówienie
Microsoft Azure Media Services wprowadzają hello **Media Encoder Premium w przepływie pracy** procesor multimediów. To kodowanie możliwości przepływy pracy na żądanie premium wcześniejszym oferty procesora.

Witaj poniższych tematach przedstawiono szczegółowe informacje dotyczące zbyt**Media Encoder Premium w przepływie pracy**:

* [Formatuje obsługiwane przez hello Media Encoder Premium w przepływie pracy](media-services-premium-workflow-encoder-formats.md) — w tym artykule omówiono hello formaty plików i kodery-dekodery obsługiwane przez **Media Encoder Premium w przepływie pracy**.
* [Omówienie i porównanie Azure na żądanie nośnika koderów](media-services-encode-asset.md) porównuje hello kodowania możliwości **Media Encoder Premium w przepływie pracy** i **Media Encoder Standard**.

W tym temacie przedstawiono sposób tooencode z **Media Encoder Premium w przepływie pracy** przy użyciu platformy .NET.

Kodowanie zadania hello **Media Encoder Premium w przepływie pracy** wymagają osobną konfiguracją pliku o nazwie pliku przepływu pracy. Te pliki mają rozszerzenie .workflow i są tworzone przy użyciu hello [projektanta przepływów pracy](media-services-workflow-designer.md) narzędzia.

Można także uzyskać hello domyślne pliki przepływu pracy [tutaj](https://github.com/Azure/azure-media-services-samples/tree/master/Encoding%20Presets/VoD/MediaEncoderPremiumWorkfows). Hello folder zawiera również opis hello tych plików.

pliki przepływu pracy Hello wymagają konta usługi Media Services tooyour toobe przekazany jako zasób, a ten zasób powinien zostać przekazany w toohello kodowania zadań.

## <a name="create-and-configure-a-visual-studio-project"></a>Tworzenie i konfigurowanie projektu programu Visual Studio

Konfigurowanie środowiska projektowego i wypełnić plik app.config hello o informacje dotyczące połączenia, zgodnie z opisem w [tworzenia usługi Media Services z platformą .NET](media-services-dotnet-how-to-use.md). 

## <a name="encoding-example"></a>Przykład kodowania

Witaj poniższym przykładzie pokazano, jak tooencode z **Media Encoder Premium w przepływie pracy**.

wykonywane są Hello następujące kroki:

1. Utworzenie elementu zawartości i przekazywanie pliku przepływu pracy.
2. Utworzenie elementu zawartości i przekazywanie pliku nośnika źródłowego.
3. Pobierz procesor multimediów hello "Media Encoder Premium przepływu pracy".
4. Utwórz zadania i zadania.

    W większości przypadków ciągu konfiguracji hello hello zadania jest pusty (takich jak hello poniższy przykład). Niektórych zaawansowanych scenariuszy (które wymagają właściwości środowisko uruchomieniowe tootooset dynamicznie) w takim przypadku zapewni toohello ciągu XML dla zadania kodowania. Przykłady takich scenariuszy: tworzenie nakładki, równoległe i sekwencyjne nośnika łączenia, napisy.
5. Dodaj dwa zadania toohello zasobów wejściowych.

    1. 1 — Witaj zasobów przepływu pracy.
    2. 2 — Witaj zawartości wideo.

    >[!NOTE]
    >Hello zasobów przepływu pracy należy dodać zadanie toohello przed hello nośnika zasobów.
   Witaj ciągu konfiguracji tego zadania może być pusta.
   
6. Przedstawia hello zadania kodowania.

        using System;
        using System.Linq;
        using System.Configuration;
        using System.IO;
        using System.Threading;
        using System.Threading.Tasks;
        using Microsoft.WindowsAzure.MediaServices.Client;

        namespace MediaEncoderPremiumWorkflowSample
        {
            class Program
            {
                private static readonly string _AADTenantDomain =
                    ConfigurationManager.AppSettings["AADTenantDomain"];
                private static readonly string _RESTAPIEndpoint =
                    ConfigurationManager.AppSettings["MediaServiceRESTAPIEndpoint"];

                // Field for service context.
                private static CloudMediaContext _context = null;

                private static readonly string _supportFiles =
                    Path.GetFullPath(@"../..\Media");

                private static readonly string _workflowFilePath =
                    Path.GetFullPath(_supportFiles + @"\H264 Progressive Download MP4.workflow");

                private static readonly string _singleMP4InputFilePath =
                    Path.GetFullPath(_supportFiles + @"\BigBuckBunny.mp4");

                static void Main(string[] args)
                {
                    var tokenCredentials = new AzureAdTokenCredentials(_AADTenantDomain, AzureEnvironments.AzureCloudEnvironment);
                    var tokenProvider = new AzureAdTokenProvider(tokenCredentials);

                    _context = new CloudMediaContext(new Uri(_RESTAPIEndpoint), tokenProvider);

                    var workflowAsset = CreateAssetAndUploadSingleFile(_workflowFilePath);
                    var videoAsset = CreateAssetAndUploadSingleFile(_singleMP4InputFilePath);
                    IAsset outputAsset = CreateEncodingJob(workflowAsset, videoAsset);

                }

                static public IAsset CreateAssetAndUploadSingleFile(string singleFilePath)
                {
                    var assetName = "UploadSingleFile_" + DateTime.UtcNow.ToString();
                    var asset = _context.Assets.Create(assetName, AssetCreationOptions.None);

                    var fileName = Path.GetFileName(singleFilePath);

                    var assetFile = asset.AssetFiles.Create(fileName);

                    Console.WriteLine("Created assetFile {0}", assetFile.Name);

                    Console.WriteLine("Upload {0}", assetFile.Name);

                    assetFile.Upload(singleFilePath);
                    Console.WriteLine("Done uploading {0}", assetFile.Name);

                    return asset;
                }

                static public IAsset CreateEncodingJob(IAsset workflow, IAsset video)
                {
                    // Declare a new job.
                    IJob job = _context.Jobs.Create("Premium Workflow encoding job");
                    // Get a media processor reference, and pass tooit hello name of the
                    // processor toouse for hello specific task.
                    IMediaProcessor processor = GetLatestMediaProcessorByName("Media Encoder Premium Workflow");

                    // Create a task with hello encoding details, using a string preset.
                    ITask task = job.Tasks.AddNew("Premium Workflow encoding task",
                        processor,
                        "",
                        TaskOptions.None);

                    // Specify hello input asset toobe encoded.
                    task.InputAssets.Add(workflow);
                    task.InputAssets.Add(video); // we add one asset
                                                 // Add an output asset toocontain hello results of hello job.
                                                 // This output is specified as AssetCreationOptions.None, which
                                                 // means hello output asset is not encrypted.
                    task.OutputAssets.AddNew("Output asset",
                        AssetCreationOptions.None);

                    // Use hello following event handler toocheck job progress.  
                    job.StateChanged += new
                            EventHandler<JobStateChangedEventArgs>(StateChanged);

                    // Launch hello job.
                    job.Submit();

                    // Check job execution and wait for job toofinish.
                    Task progressJobTask = job.GetExecutionProgressTask(CancellationToken.None);
                    progressJobTask.Wait();

                    // If job state is Error hello event handling
                    // method for job progress should log errors.  Here we check
                    // for error state and exit if needed.
                    if (job.State == JobState.Error)
                    {
                        throw new Exception("\nExiting method due toojob error.");
                    }

                    return job.OutputMediaAssets[0];
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
                private static IMediaProcessor GetLatestMediaProcessorByName(string mediaProcessorName)
                {
                    var processor = _context.MediaProcessors.Where(p => p.Name == mediaProcessorName).
                    ToList().OrderBy(p => new Version(p.Version)).LastOrDefault();

                    if (processor == null)
                        throw new ArgumentException(string.Format("Unknown media processor", mediaProcessorName));

                    return processor;
                }
            }
        }

Odpowiedzi na pytania koder premium poczty e-mail mepd z witryny Microsoft.com.

## <a name="media-services-learning-paths"></a>Ścieżki szkoleniowe dotyczące usługi Media Services
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Przekazywanie opinii
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]
