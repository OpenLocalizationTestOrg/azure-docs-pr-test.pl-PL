---
title: "Zaawansowane kodowania w przepływie pracy Premium kodera multimediów | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak do zakodowania w przepływie pracy Premium kodera multimediów. Przykłady kodu są napisane w języku C# i używają SDK usługi Media Services dla platformy .NET."
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
ms.openlocfilehash: 2b03853bf07e05c07fd730d5e8a8563963887921
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
# <a name="advanced-encoding-with-media-encoder-premium-workflow"></a><span data-ttu-id="9d231-104">Zaawansowane encoding w usłudze Media Encoder Premium w przepływie pracy</span><span class="sxs-lookup"><span data-stu-id="9d231-104">Advanced encoding with Media Encoder Premium Workflow</span></span>
> [!NOTE]
> <span data-ttu-id="9d231-105">Procesor multimediów Media Encoder Premium w przepływie pracy omówione w tym temacie nie jest dostępna w Chinach.</span><span class="sxs-lookup"><span data-stu-id="9d231-105">Media Encoder Premium Workflow media processor discussed in this topic is not available in China.</span></span>
>
>

<span data-ttu-id="9d231-106">Odpowiedzi na pytania koder premium poczty e-mail mepd z witryny Microsoft.com.</span><span class="sxs-lookup"><span data-stu-id="9d231-106">For premium encoder questions, email mepd at Microsoft.com.</span></span>

## <a name="overview"></a><span data-ttu-id="9d231-107">Omówienie</span><span class="sxs-lookup"><span data-stu-id="9d231-107">Overview</span></span>
<span data-ttu-id="9d231-108">Wprowadzenie do usługi Microsoft Azure Media Services **Media Encoder Premium w przepływie pracy** procesor multimediów.</span><span class="sxs-lookup"><span data-stu-id="9d231-108">Microsoft Azure Media Services is introducing the **Media Encoder Premium Workflow** media processor.</span></span> <span data-ttu-id="9d231-109">To kodowanie możliwości przepływy pracy na żądanie premium wcześniejszym oferty procesora.</span><span class="sxs-lookup"><span data-stu-id="9d231-109">This processor offers advance encoding capabilities for your premium on-demand workflows.</span></span>

<span data-ttu-id="9d231-110">W poniższych tematach przedstawiono szczegółowe informacje dotyczące **Media Encoder Premium w przepływie pracy**:</span><span class="sxs-lookup"><span data-stu-id="9d231-110">The following topics outline details related to **Media Encoder Premium Workflow**:</span></span>

* <span data-ttu-id="9d231-111">[Formatuje obsługiwane przez przepływ pracy Media Encoder Premium](media-services-premium-workflow-encoder-formats.md) — Discusses pliku formatuje i kodery-dekodery obsługiwane przez **Media Encoder Premium w przepływie pracy**.</span><span class="sxs-lookup"><span data-stu-id="9d231-111">[Formats Supported by the Media Encoder Premium Workflow](media-services-premium-workflow-encoder-formats.md) – Discusses the file formats and codecs supported by **Media Encoder Premium Workflow**.</span></span>
* <span data-ttu-id="9d231-112">[Omówienie i porównanie Azure na żądanie nośnika koderów](media-services-encode-asset.md) porównuje kodowania możliwości **Media Encoder Premium w przepływie pracy** i **Media Encoder Standard**.</span><span class="sxs-lookup"><span data-stu-id="9d231-112">[Overview and comparison of Azure on demand media encoders](media-services-encode-asset.md) compares the encoding capabilities of **Media Encoder Premium Workflow** and **Media Encoder Standard**.</span></span>

<span data-ttu-id="9d231-113">W tym temacie przedstawiono sposób kodowania z **Media Encoder Premium w przepływie pracy** przy użyciu platformy .NET.</span><span class="sxs-lookup"><span data-stu-id="9d231-113">This topic demonstrates how to encode with **Media Encoder Premium Workflow** using .NET.</span></span>

<span data-ttu-id="9d231-114">Kodowanie zadania **Media Encoder Premium w przepływie pracy** wymagają osobną konfiguracją pliku o nazwie pliku przepływu pracy.</span><span class="sxs-lookup"><span data-stu-id="9d231-114">Encoding tasks for the **Media Encoder Premium Workflow** require a separate configuration file, called a Workflow file.</span></span> <span data-ttu-id="9d231-115">Te pliki mają rozszerzenie .workflow i są tworzone przy użyciu [projektanta przepływów pracy](media-services-workflow-designer.md) narzędzia.</span><span class="sxs-lookup"><span data-stu-id="9d231-115">These files have a .workflow extension and are created using the [Workflow Designer](media-services-workflow-designer.md) tool.</span></span>

<span data-ttu-id="9d231-116">Można także uzyskać domyślne pliki przepływu pracy [tutaj](https://github.com/Azure/azure-media-services-samples/tree/master/Encoding%20Presets/VoD/MediaEncoderPremiumWorkfows).</span><span class="sxs-lookup"><span data-stu-id="9d231-116">You can also get the default workflow files [here](https://github.com/Azure/azure-media-services-samples/tree/master/Encoding%20Presets/VoD/MediaEncoderPremiumWorkfows).</span></span> <span data-ttu-id="9d231-117">Folder zawiera również opis tych plików.</span><span class="sxs-lookup"><span data-stu-id="9d231-117">The folder also contains the description of these files.</span></span>

<span data-ttu-id="9d231-118">Pliki przepływu pracy muszą zostać przekazana do konta usługi Media Services jako zasób, a ten zasób należy przekazać do kodowania zadań.</span><span class="sxs-lookup"><span data-stu-id="9d231-118">The workflow files need to be uploaded to your Media Services account as an Asset, and this Asset should be passed in to the encoding Task.</span></span>

## <a name="create-and-configure-a-visual-studio-project"></a><span data-ttu-id="9d231-119">Tworzenie i konfigurowanie projektu programu Visual Studio</span><span class="sxs-lookup"><span data-stu-id="9d231-119">Create and configure a Visual Studio project</span></span>

<span data-ttu-id="9d231-120">Skonfiguruj środowisko projektowe i wypełnij plik app.config przy użyciu informacji dotyczących połączenia, zgodnie z opisem w sekcji [Projektowanie usługi Media Services na platformie .NET](media-services-dotnet-how-to-use.md).</span><span class="sxs-lookup"><span data-stu-id="9d231-120">Set up your development environment and populate the app.config file with connection information, as described in [Media Services development with .NET](media-services-dotnet-how-to-use.md).</span></span> 

## <a name="encoding-example"></a><span data-ttu-id="9d231-121">Przykład kodowania</span><span class="sxs-lookup"><span data-stu-id="9d231-121">Encoding example</span></span>

<span data-ttu-id="9d231-122">W poniższym przykładzie pokazano sposób kodowania z **Media Encoder Premium w przepływie pracy**.</span><span class="sxs-lookup"><span data-stu-id="9d231-122">The following example demonstrates how to encode with **Media Encoder Premium Workflow**.</span></span>

<span data-ttu-id="9d231-123">Są wykonywane następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="9d231-123">The following steps are performed:</span></span>

1. <span data-ttu-id="9d231-124">Utworzenie elementu zawartości i przekazywanie pliku przepływu pracy.</span><span class="sxs-lookup"><span data-stu-id="9d231-124">Create an asset and upload a workflow file.</span></span>
2. <span data-ttu-id="9d231-125">Utworzenie elementu zawartości i przekazywanie pliku nośnika źródłowego.</span><span class="sxs-lookup"><span data-stu-id="9d231-125">Create an asset and upload a source media file.</span></span>
3. <span data-ttu-id="9d231-126">Pobierz nośnika procesor "Media Encoder Premium przepływu pracy".</span><span class="sxs-lookup"><span data-stu-id="9d231-126">Get the "Media Encoder Premium Workflow" media processor.</span></span>
4. <span data-ttu-id="9d231-127">Utwórz zadania i zadania.</span><span class="sxs-lookup"><span data-stu-id="9d231-127">Create a job and a task.</span></span>

    <span data-ttu-id="9d231-128">W większości przypadków ciągu konfiguracji zadania jest pusty (takich jak w poniższym przykładzie).</span><span class="sxs-lookup"><span data-stu-id="9d231-128">In most cases, the configuration string for the task is empty (like in the following example).</span></span> <span data-ttu-id="9d231-129">Niektórych zaawansowanych scenariuszy (które wymagają dynamicznego ustawiania właściwości środowisko uruchomieniowe) w takim przypadku zapewni ciągu XML do kodowania zadań.</span><span class="sxs-lookup"><span data-stu-id="9d231-129">There are some advanced scenarios (that require you to to set runtime properties dynamically) in which case you would provide an XML string to the encoding task.</span></span> <span data-ttu-id="9d231-130">Przykłady takich scenariuszy: tworzenie nakładki, równoległe i sekwencyjne nośnika łączenia, napisy.</span><span class="sxs-lookup"><span data-stu-id="9d231-130">Examples of such scenarios are: creating an overlay, parallel or sequential media stitching, subtitling.</span></span>
5. <span data-ttu-id="9d231-131">Dodaj dwa zasoby wejściowych do zadania.</span><span class="sxs-lookup"><span data-stu-id="9d231-131">Add two input assets to the task.</span></span>

    1. <span data-ttu-id="9d231-132">1 — zasobów przepływu pracy.</span><span class="sxs-lookup"><span data-stu-id="9d231-132">1st – the workflow asset.</span></span>
    2. <span data-ttu-id="9d231-133">2 — zawartości wideo.</span><span class="sxs-lookup"><span data-stu-id="9d231-133">2nd – the video asset.</span></span>

    >[!NOTE]
    ><span data-ttu-id="9d231-134">Zasobów przepływu pracy musi zostać dodany do zadań przed zasobu multimediów.</span><span class="sxs-lookup"><span data-stu-id="9d231-134">The workflow asset must be added to the task before the media asset.</span></span>
   <span data-ttu-id="9d231-135">Ciąg konfiguracji tego zadania powinna być pusta.</span><span class="sxs-lookup"><span data-stu-id="9d231-135">The configuration string for this task should be empty.</span></span>
   
6. <span data-ttu-id="9d231-136">Przesyłania zadania kodowania.</span><span class="sxs-lookup"><span data-stu-id="9d231-136">Submit the encoding job.</span></span>

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
                    // Get a media processor reference, and pass to it the name of the
                    // processor to use for the specific task.
                    IMediaProcessor processor = GetLatestMediaProcessorByName("Media Encoder Premium Workflow");

                    // Create a task with the encoding details, using a string preset.
                    ITask task = job.Tasks.AddNew("Premium Workflow encoding task",
                        processor,
                        "",
                        TaskOptions.None);

                    // Specify the input asset to be encoded.
                    task.InputAssets.Add(workflow);
                    task.InputAssets.Add(video); // we add one asset
                                                 // Add an output asset to contain the results of the job.
                                                 // This output is specified as AssetCreationOptions.None, which
                                                 // means the output asset is not encrypted.
                    task.OutputAssets.AddNew("Output asset",
                        AssetCreationOptions.None);

                    // Use the following event handler to check job progress.  
                    job.StateChanged += new
                            EventHandler<JobStateChangedEventArgs>(StateChanged);

                    // Launch the job.
                    job.Submit();

                    // Check job execution and wait for job to finish.
                    Task progressJobTask = job.GetExecutionProgressTask(CancellationToken.None);
                    progressJobTask.Wait();

                    // If job state is Error the event handling
                    // method for job progress should log errors.  Here we check
                    // for error state and exit if needed.
                    if (job.State == JobState.Error)
                    {
                        throw new Exception("\nExiting method due to job error.");
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

<span data-ttu-id="9d231-137">Odpowiedzi na pytania koder premium poczty e-mail mepd z witryny Microsoft.com.</span><span class="sxs-lookup"><span data-stu-id="9d231-137">For premium encoder questions, email mepd at Microsoft.com.</span></span>

## <a name="media-services-learning-paths"></a><span data-ttu-id="9d231-138">Ścieżki szkoleniowe dotyczące usługi Media Services</span><span class="sxs-lookup"><span data-stu-id="9d231-138">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="9d231-139">Przekazywanie opinii</span><span class="sxs-lookup"><span data-stu-id="9d231-139">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]
