---
title: "aaaCreate zadanie kodowania usługi Azure Media Services, które generuje fragmentów fMP4 | Dokumentacja firmy Microsoft"
description: "W tym temacie przedstawiono sposób toocreate zadania kodowania, które generuje fMP4 fragmentów. Gdy to zadanie jest używana z hello Media Encoder Standard lub kodera Media Encoder Premium w przepływie pracy, zawartości wyjściowej hello będzie zawierać fragmentów fMP4 zamiast plików ISO MP4."
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: b7029ac5-eadd-4a2f-8111-1fc460828981
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/18/2017
ms.author: juliako
ms.openlocfilehash: 388f3ccb9865b5c4e159af86d5a9ee2f4e3f6120
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
#  <a name="create-an-encoding-task-that-generates-fmp4-chunks"></a><span data-ttu-id="457b5-104">Utwórz zadania kodowania, które generuje fMP4 fragmentów</span><span class="sxs-lookup"><span data-stu-id="457b5-104">Create an encoding task that generates fMP4 chunks</span></span>

## <a name="overview"></a><span data-ttu-id="457b5-105">Omówienie</span><span class="sxs-lookup"><span data-stu-id="457b5-105">Overview</span></span>

<span data-ttu-id="457b5-106">W tym temacie pokazano, jak toocreate zadania kodowania, które generuje pofragmentowany plik MP4 fragmentów (fMP4) zamiast plików ISO MP4.</span><span class="sxs-lookup"><span data-stu-id="457b5-106">This topic shows how toocreate an encoding task that generates fragmented MP4 (fMP4) chunks instead of ISO MP4 files.</span></span> <span data-ttu-id="457b5-107">toogenerate fMP4 fragmentów, użyj hello **Media Encoder Standard** lub **Media Encoder Premium w przepływie pracy** toocreate kodera kodowania zadań, a także określić  **AssetFormatOption.AdaptiveStreaming** opcji, jak pokazano w poniższym przykładzie:</span><span class="sxs-lookup"><span data-stu-id="457b5-107">toogenerate fMP4 chunks, use hello **Media Encoder Standard** or **Media Encoder Premium Workflow** encoder toocreate an encoding task and also specify **AssetFormatOption.AdaptiveStreaming** option, as shown in this code snippet:</span></span>  
    
    task.OutputAssets.AddNew(@"Output Asset containing fMP4 chunks", 
            options: AssetCreationOptions.None, 
            formatOption: AssetFormatOption.AdaptiveStreaming);


## <span data-ttu-id="457b5-108"><a id="encoding_with_dotnet"></a>Kodowanie w usłudze Media Services zestawu .NET SDK</span><span class="sxs-lookup"><span data-stu-id="457b5-108"><a id="encoding_with_dotnet"></a>Encoding with Media Services .NET SDK</span></span>

<span data-ttu-id="457b5-109">Poniższy przykład kodu Hello używa hello tooperform .NET SDK usługi Media Services następujące zadania:</span><span class="sxs-lookup"><span data-stu-id="457b5-109">hello following code example uses Media Services .NET SDK tooperform hello following tasks:</span></span>

- <span data-ttu-id="457b5-110">Utwórz zadania kodowania.</span><span class="sxs-lookup"><span data-stu-id="457b5-110">Create an encoding job.</span></span>
- <span data-ttu-id="457b5-111">Pobierz toohello odwołanie **Media Encoder Standard** kodera.</span><span class="sxs-lookup"><span data-stu-id="457b5-111">Get a reference toohello **Media Encoder Standard** encoder.</span></span>
- <span data-ttu-id="457b5-112">Dodaj zadania kodowania toohello zadań i określ toouse hello **adaptacyjne przesyłanie strumieniowe** wstępnie zdefiniowane.</span><span class="sxs-lookup"><span data-stu-id="457b5-112">Add an encoding task toohello job and specify toouse hello **Adaptive Streaming** preset.</span></span> 
- <span data-ttu-id="457b5-113">Tworzenie zasobu wyjściowego, który będzie zawierać fragmentów fMP4 i plik .ism.</span><span class="sxs-lookup"><span data-stu-id="457b5-113">Create an output asset that will contain fMP4 chunks and an .ism file.</span></span>
- <span data-ttu-id="457b5-114">Dodaj postęp zadania hello toocheck zdarzeń programu obsługi.</span><span class="sxs-lookup"><span data-stu-id="457b5-114">Add an event handler toocheck hello job progress.</span></span>
- <span data-ttu-id="457b5-115">Prześlij zadanie hello.</span><span class="sxs-lookup"><span data-stu-id="457b5-115">Submit hello job.</span></span>

#### <a name="create-and-configure-a-visual-studio-project"></a><span data-ttu-id="457b5-116">Tworzenie i konfigurowanie projektu programu Visual Studio</span><span class="sxs-lookup"><span data-stu-id="457b5-116">Create and configure a Visual Studio project</span></span>

<span data-ttu-id="457b5-117">Konfigurowanie środowiska projektowego i wypełnić plik app.config hello o informacje dotyczące połączenia, zgodnie z opisem w [tworzenia usługi Media Services z platformą .NET](media-services-dotnet-how-to-use.md).</span><span class="sxs-lookup"><span data-stu-id="457b5-117">Set up your development environment and populate hello app.config file with connection information, as described in [Media Services development with .NET](media-services-dotnet-how-to-use.md).</span></span> 

#### <a name="example"></a><span data-ttu-id="457b5-118">Przykład</span><span class="sxs-lookup"><span data-stu-id="457b5-118">Example</span></span>

    using System;
    using System.Configuration;
    using System.Linq;
    using Microsoft.WindowsAzure.MediaServices.Client;
    using System.Threading;

    namespace AdaptiveStreaming
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

            // Get an uploaded asset.
            var asset = _context.Assets.FirstOrDefault();

            // Encode and generate hello output using hello "Adaptive Streaming" preset.
            EncodeToAdaptiveBitrateMP4Set(asset);

            Console.ReadLine();
        }
        static public IAsset EncodeToAdaptiveBitrateMP4Set(IAsset asset)
        {
            // Declare a new job.
            IJob job = _context.Jobs.Create("Media Encoder Standard Job");

            // Get a media processor reference, and pass tooit hello name of hello 
            // processor toouse for hello specific task.
            IMediaProcessor processor = GetLatestMediaProcessorByName("Media Encoder Standard");

            // Create a task
            ITask task = job.Tasks.AddNew("Media Encoder Standard encoding task",
            processor,
            "Adaptive Streaming",
            TaskOptions.None);

            // Specify hello input asset toobe encoded.
            task.InputAssets.Add(asset);

            // Add an output asset toocontain hello results of hello job. 

            // This output is specified as AssetCreationOptions.None, which 
            // means hello output asset is not encrypted. 
            // It is also specified toouse AssetFormatOption.AdaptiveStreaming, 
            // which means hello output asset will contain fMP4 chunks.

            task.OutputAssets.AddNew(@"Output Asset containing fMP4 chunks",
            options: AssetCreationOptions.None,
            formatOption: AssetFormatOption.AdaptiveStreaming);

            job.StateChanged += new EventHandler<JobStateChangedEventArgs>(JobStateChanged);
            job.Submit();
            job.GetExecutionProgressTask(CancellationToken.None).Wait();

            return job.OutputMediaAssets[0];
        }
        private static void JobStateChanged(object sender, JobStateChangedEventArgs e)
        {
            Console.WriteLine("Job state changed event:");
            Console.WriteLine("  Previous state: " + e.PreviousState);
            Console.WriteLine("  Current state: " + e.CurrentState);
            switch (e.CurrentState)
            {
            case JobState.Finished:
                Console.WriteLine();
                Console.WriteLine("Job is finished. Please wait while local tasks or downloads complete...");
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

## <a name="media-services-learning-paths"></a><span data-ttu-id="457b5-119">Ścieżki szkoleniowe dotyczące usługi Media Services</span><span class="sxs-lookup"><span data-stu-id="457b5-119">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="457b5-120">Przekazywanie opinii</span><span class="sxs-lookup"><span data-stu-id="457b5-120">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="see-also"></a><span data-ttu-id="457b5-121">Zobacz też</span><span class="sxs-lookup"><span data-stu-id="457b5-121">See Also</span></span>
[<span data-ttu-id="457b5-122">Usługi multimediów kodowania — omówienie</span><span class="sxs-lookup"><span data-stu-id="457b5-122">Media Services Encoding Overview</span></span>](media-services-encode-asset.md)

