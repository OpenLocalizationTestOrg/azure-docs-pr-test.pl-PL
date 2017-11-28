---
title: "Azure Media Encoder Standard tooauto aaaUse-Generowanie drabinę szybkości transmisji bitów | Dokumentacja firmy Microsoft"
description: "W tym temacie przedstawiono sposób tooauto Media Encoder Standard (rynkowej) toouse-Generowanie drabinę szybkości transmisji bitów, na podstawie hello rozdzielczość i szybkość transmisji bitów. Hello rozdzielczość i szybkość transmisji bitów nigdy nie zostanie przekroczony. Na przykład jeśli wejściowy hello jest 720p w 3 MB/s, dane wyjściowe będą pozostawać w najlepszym 720p i rozpocznie stawkami niższa niż 3 MB/s."
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: 63ed95da-1b82-44b0-b8ff-eebd535bc5c7
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: juliako
ms.openlocfilehash: 5437f54ac28c42ddd4f9d1986549d6da6261c5da
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
#  <a name="use-azure-media-encoder-standard-tooauto-generate-a-bitrate-ladder"></a><span data-ttu-id="e1be6-105">Użyj usługi Azure Media Encoder Standard tooauto-Generowanie drabinę szybkości transmisji bitów</span><span class="sxs-lookup"><span data-stu-id="e1be6-105">Use Azure Media Encoder Standard tooauto-generate a bitrate ladder</span></span>

## <a name="overview"></a><span data-ttu-id="e1be6-106">Omówienie</span><span class="sxs-lookup"><span data-stu-id="e1be6-106">Overview</span></span>

<span data-ttu-id="e1be6-107">W tym temacie przedstawiono sposób tooauto Media Encoder Standard (rynkowej) toouse-Generowanie drabinę szybkości transmisji bitów (pary rozpoznawania szybkości transmisji bitów) na podstawie hello rozdzielczość i szybkość transmisji bitów.</span><span class="sxs-lookup"><span data-stu-id="e1be6-107">This topic shows how toouse Media Encoder Standard (MES) tooauto-generate a bitrate ladder (bitrate-resolution pairs) based on hello input resolution and bitrate.</span></span> <span data-ttu-id="e1be6-108">Witaj automatycznie generowanej ustawienie wstępne nigdy nie przekroczy hello wejściowych rozdzielczość i szybkość transmisji bitów.</span><span class="sxs-lookup"><span data-stu-id="e1be6-108">hello auto-generated preset will never exceed hello input resolution and bitrate.</span></span> <span data-ttu-id="e1be6-109">Na przykład jeśli wejściowy hello jest 720p w 3 MB/s, dane wyjściowe będą pozostawać w najlepszym 720p i rozpocznie stawkami niższa niż 3 MB/s.</span><span class="sxs-lookup"><span data-stu-id="e1be6-109">For example, if hello input is 720p at 3Mbps, output will remain 720p at best, and will start at rates lower than 3Mbps.</span></span>

### <a name="encoding-for-streaming-only"></a><span data-ttu-id="e1be6-110">Kodowanie tylko przesyłania strumieniowego</span><span class="sxs-lookup"><span data-stu-id="e1be6-110">Encoding for Streaming Only</span></span>

<span data-ttu-id="e1be6-111">Jeśli tooencode zamierzeniu źródła wideo tylko w przypadku przesyłania strumieniowego, możesz powinny używać "Adaptacyjne przesyłanie strumieniowe" hello wstępnie podczas tworzenia zadania kodowania.</span><span class="sxs-lookup"><span data-stu-id="e1be6-111">If your intent is tooencode your source video only for streaming, then you shoud use hello "Adaptive Streaming" preset when creating an encoding task.</span></span> <span data-ttu-id="e1be6-112">Korzystając z hello **adaptacyjne przesyłanie strumieniowe** zdefiniowane, hello rynkowej kodera sposób inteligentny będzie cap drabinę szybkości transmisji bitów.</span><span class="sxs-lookup"><span data-stu-id="e1be6-112">When using hello **Adaptive Streaming** preset, hello MES encoder will intelligently cap a bitrate ladder.</span></span> <span data-ttu-id="e1be6-113">Jednak nie będzie możliwe toocontrol hello kodowanie kosztów, ponieważ usługa hello Określa, ile toouse warstwy i jakie rozdzielczości.</span><span class="sxs-lookup"><span data-stu-id="e1be6-113">However, you will not be able toocontrol hello encoding costs, since hello service determines how many layers toouse and at what resolution.</span></span> <span data-ttu-id="e1be6-114">Zawiera przykłady warstw wyjściowego utworzonego przez rynkowej wyniku kodowania z hello **adaptacyjne przesyłanie strumieniowe** ustawień wstępnych. na końcu hello w tym temacie.</span><span class="sxs-lookup"><span data-stu-id="e1be6-114">You can see examples of output layers produced by MES as a result of encoding with hello **Adaptive Streaming** preset at hello end of this topic.</span></span> <span data-ttu-id="e1be6-115">Witaj output zasobów będzie zawierać pliki MP4, gdzie audio i wideo nie jest przeplatana.</span><span class="sxs-lookup"><span data-stu-id="e1be6-115">hello output Asset will contain MP4 files where audio and video are not interleaved.</span></span>

### <a name="encoding-for-streaming-and-progressive-download"></a><span data-ttu-id="e1be6-116">Kodowanie używane do przesyłania strumieniowego i pobierania progresywnego</span><span class="sxs-lookup"><span data-stu-id="e1be6-116">Encoding for Streaming and Progressive Download</span></span>

<span data-ttu-id="e1be6-117">Jeśli tooencode zamierzeniu źródłowy plik wideo do przesyłania strumieniowego oraz pliki MP4 tooproduce pobierania progresywnego, możesz powinny używać hello "Zawartości adaptacyjną wielu szybkości transmisji bitów MP4" wstępnie podczas tworzenia zadania kodowania.</span><span class="sxs-lookup"><span data-stu-id="e1be6-117">If your intent is tooencode your source video for streaming as well as tooproduce MP4 files for progressive download, then you shoud use hello "Content Adaptive Multiple Bitrate MP4" preset when creating an encoding task.</span></span> <span data-ttu-id="e1be6-118">Korzystając z hello **zawartości adaptacyjną wielu MP4 szybkości transmisji bitów** zdefiniowane, koder rynkowej hello zastosuje hello samej logiki kodowania, jak powyżej, ale teraz zawartości wyjściowej hello będzie zawierać MP4 pliki w przypadku, gdy audio i wideo są przeplotem.</span><span class="sxs-lookup"><span data-stu-id="e1be6-118">When using hello **Content Adaptive Multiple Bitrate MP4** preset, hello MES encoder will apply hello same encoding logic as above, but now hello output asset will contain MP4 files where audio and video are interleaved.</span></span> <span data-ttu-id="e1be6-119">Można użyć jednego z tych plików MP4 (na przykład hello najwyższej szybkości transmisji bitów wersji) jako plik pobierania progresywnego.</span><span class="sxs-lookup"><span data-stu-id="e1be6-119">You can use one of these MP4 files (for example, hello highest bitrate version) as a progressive download file.</span></span>

## <span data-ttu-id="e1be6-120"><a id="encoding_with_dotnet"></a>Kodowanie w usłudze Media Services zestawu .NET SDK</span><span class="sxs-lookup"><span data-stu-id="e1be6-120"><a id="encoding_with_dotnet"></a>Encoding with Media Services .NET SDK</span></span>

<span data-ttu-id="e1be6-121">Poniższy przykład kodu Hello używa hello tooperform .NET SDK usługi Media Services następujące zadania:</span><span class="sxs-lookup"><span data-stu-id="e1be6-121">hello following code example uses Media Services .NET SDK tooperform hello following tasks:</span></span>

- <span data-ttu-id="e1be6-122">Utwórz zadania kodowania.</span><span class="sxs-lookup"><span data-stu-id="e1be6-122">Create an encoding job.</span></span>
- <span data-ttu-id="e1be6-123">Pobiera koder Media Encoder Standard toohello odwołania.</span><span class="sxs-lookup"><span data-stu-id="e1be6-123">Get a reference toohello Media Encoder Standard encoder.</span></span>
- <span data-ttu-id="e1be6-124">Dodaj zadania kodowania toohello zadań i określ toouse hello **adaptacyjne przesyłanie strumieniowe** wstępnie zdefiniowane.</span><span class="sxs-lookup"><span data-stu-id="e1be6-124">Add an encoding task toohello job and specify toouse hello **Adaptive Streaming** preset.</span></span> 
- <span data-ttu-id="e1be6-125">Tworzenie zasobu danych wyjściowych, który będzie zawierać hello zakodowane zasobów.</span><span class="sxs-lookup"><span data-stu-id="e1be6-125">Create an output asset that will contain hello encoded asset.</span></span>
- <span data-ttu-id="e1be6-126">Dodaj postęp zadania hello toocheck zdarzeń programu obsługi.</span><span class="sxs-lookup"><span data-stu-id="e1be6-126">Add an event handler toocheck hello job progress.</span></span>
- <span data-ttu-id="e1be6-127">Prześlij zadanie hello.</span><span class="sxs-lookup"><span data-stu-id="e1be6-127">Submit hello job.</span></span>

#### <a name="create-and-configure-a-visual-studio-project"></a><span data-ttu-id="e1be6-128">Tworzenie i konfigurowanie projektu programu Visual Studio</span><span class="sxs-lookup"><span data-stu-id="e1be6-128">Create and configure a Visual Studio project</span></span>

<span data-ttu-id="e1be6-129">Konfigurowanie środowiska projektowego i wypełnić plik app.config hello o informacje dotyczące połączenia, zgodnie z opisem w [tworzenia usługi Media Services z platformą .NET](media-services-dotnet-how-to-use.md).</span><span class="sxs-lookup"><span data-stu-id="e1be6-129">Set up your development environment and populate hello app.config file with connection information, as described in [Media Services development with .NET](media-services-dotnet-how-to-use.md).</span></span> 

#### <a name="example"></a><span data-ttu-id="e1be6-130">Przykład</span><span class="sxs-lookup"><span data-stu-id="e1be6-130">Example</span></span>

    using System;
    using System.Configuration;
    using System.Linq;
    using Microsoft.WindowsAzure.MediaServices.Client;
    using System.Threading;

    namespace AdaptiveStreamingMESPresest
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
            task.OutputAssets.AddNew("Output asset",
            AssetCreationOptions.None);

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

## <span data-ttu-id="e1be6-131"><a id="output"></a>Dane wyjściowe</span><span class="sxs-lookup"><span data-stu-id="e1be6-131"><a id="output"></a>Output</span></span>

<span data-ttu-id="e1be6-132">W tej sekcji przedstawiono trzy przykłady warstw wyjściowego utworzonego przez rynkowej wyniku kodowania z hello **adaptacyjne przesyłanie strumieniowe** wstępnie zdefiniowane.</span><span class="sxs-lookup"><span data-stu-id="e1be6-132">This section shows three examples of output layers produced by MES as a result of encoding with hello **Adaptive Streaming** preset.</span></span> 

### <a name="example-1"></a><span data-ttu-id="e1be6-133">Przykład 1</span><span class="sxs-lookup"><span data-stu-id="e1be6-133">Example 1</span></span>
<span data-ttu-id="e1be6-134">Źródło o wysokość "1080" i "29.970" szybkość klatek tworzy 6 warstwy wideo:</span><span class="sxs-lookup"><span data-stu-id="e1be6-134">Source with height "1080" and framerate "29.970" produces 6 video layers:</span></span>

|<span data-ttu-id="e1be6-135">Warstwy</span><span class="sxs-lookup"><span data-stu-id="e1be6-135">Layer</span></span>|<span data-ttu-id="e1be6-136">Wysokość</span><span class="sxs-lookup"><span data-stu-id="e1be6-136">Height</span></span>|<span data-ttu-id="e1be6-137">Szerokość</span><span class="sxs-lookup"><span data-stu-id="e1be6-137">Width</span></span>|<span data-ttu-id="e1be6-138">Bitrate(Kbps)</span><span class="sxs-lookup"><span data-stu-id="e1be6-138">Bitrate(kbps)</span></span>|
|---|---|---|---|
|<span data-ttu-id="e1be6-139">1</span><span class="sxs-lookup"><span data-stu-id="e1be6-139">1</span></span>|<span data-ttu-id="e1be6-140">1080</span><span class="sxs-lookup"><span data-stu-id="e1be6-140">1080</span></span>|<span data-ttu-id="e1be6-141">1920</span><span class="sxs-lookup"><span data-stu-id="e1be6-141">1920</span></span>|<span data-ttu-id="e1be6-142">6780</span><span class="sxs-lookup"><span data-stu-id="e1be6-142">6780</span></span>|
|<span data-ttu-id="e1be6-143">2</span><span class="sxs-lookup"><span data-stu-id="e1be6-143">2</span></span>|<span data-ttu-id="e1be6-144">720</span><span class="sxs-lookup"><span data-stu-id="e1be6-144">720</span></span>|<span data-ttu-id="e1be6-145">1280</span><span class="sxs-lookup"><span data-stu-id="e1be6-145">1280</span></span>|<span data-ttu-id="e1be6-146">3520</span><span class="sxs-lookup"><span data-stu-id="e1be6-146">3520</span></span>|
|<span data-ttu-id="e1be6-147">3</span><span class="sxs-lookup"><span data-stu-id="e1be6-147">3</span></span>|<span data-ttu-id="e1be6-148">540</span><span class="sxs-lookup"><span data-stu-id="e1be6-148">540</span></span>|<span data-ttu-id="e1be6-149">960</span><span class="sxs-lookup"><span data-stu-id="e1be6-149">960</span></span>|<span data-ttu-id="e1be6-150">2210</span><span class="sxs-lookup"><span data-stu-id="e1be6-150">2210</span></span>|
|<span data-ttu-id="e1be6-151">4</span><span class="sxs-lookup"><span data-stu-id="e1be6-151">4</span></span>|<span data-ttu-id="e1be6-152">360</span><span class="sxs-lookup"><span data-stu-id="e1be6-152">360</span></span>|<span data-ttu-id="e1be6-153">640</span><span class="sxs-lookup"><span data-stu-id="e1be6-153">640</span></span>|<span data-ttu-id="e1be6-154">1150</span><span class="sxs-lookup"><span data-stu-id="e1be6-154">1150</span></span>|
|<span data-ttu-id="e1be6-155">5</span><span class="sxs-lookup"><span data-stu-id="e1be6-155">5</span></span>|<span data-ttu-id="e1be6-156">270</span><span class="sxs-lookup"><span data-stu-id="e1be6-156">270</span></span>|<span data-ttu-id="e1be6-157">480</span><span class="sxs-lookup"><span data-stu-id="e1be6-157">480</span></span>|<span data-ttu-id="e1be6-158">720</span><span class="sxs-lookup"><span data-stu-id="e1be6-158">720</span></span>|
|<span data-ttu-id="e1be6-159">6</span><span class="sxs-lookup"><span data-stu-id="e1be6-159">6</span></span>|<span data-ttu-id="e1be6-160">180</span><span class="sxs-lookup"><span data-stu-id="e1be6-160">180</span></span>|<span data-ttu-id="e1be6-161">320</span><span class="sxs-lookup"><span data-stu-id="e1be6-161">320</span></span>|<span data-ttu-id="e1be6-162">380</span><span class="sxs-lookup"><span data-stu-id="e1be6-162">380</span></span>|

### <a name="example-2"></a><span data-ttu-id="e1be6-163">Przykład 2</span><span class="sxs-lookup"><span data-stu-id="e1be6-163">Example 2</span></span>
<span data-ttu-id="e1be6-164">Źródło o wysokość "720" i "23.970" szybkość klatek tworzy 5 warstwy wideo:</span><span class="sxs-lookup"><span data-stu-id="e1be6-164">Source with height "720" and framerate "23.970" produces 5 video layers:</span></span>

|<span data-ttu-id="e1be6-165">Warstwy</span><span class="sxs-lookup"><span data-stu-id="e1be6-165">Layer</span></span>|<span data-ttu-id="e1be6-166">Wysokość</span><span class="sxs-lookup"><span data-stu-id="e1be6-166">Height</span></span>|<span data-ttu-id="e1be6-167">Szerokość</span><span class="sxs-lookup"><span data-stu-id="e1be6-167">Width</span></span>|<span data-ttu-id="e1be6-168">Bitrate(Kbps)</span><span class="sxs-lookup"><span data-stu-id="e1be6-168">Bitrate(kbps)</span></span>|
|---|---|---|---|
|<span data-ttu-id="e1be6-169">1</span><span class="sxs-lookup"><span data-stu-id="e1be6-169">1</span></span>|<span data-ttu-id="e1be6-170">720</span><span class="sxs-lookup"><span data-stu-id="e1be6-170">720</span></span>|<span data-ttu-id="e1be6-171">1280</span><span class="sxs-lookup"><span data-stu-id="e1be6-171">1280</span></span>|<span data-ttu-id="e1be6-172">2940</span><span class="sxs-lookup"><span data-stu-id="e1be6-172">2940</span></span>|
|<span data-ttu-id="e1be6-173">2</span><span class="sxs-lookup"><span data-stu-id="e1be6-173">2</span></span>|<span data-ttu-id="e1be6-174">540</span><span class="sxs-lookup"><span data-stu-id="e1be6-174">540</span></span>|<span data-ttu-id="e1be6-175">960</span><span class="sxs-lookup"><span data-stu-id="e1be6-175">960</span></span>|<span data-ttu-id="e1be6-176">1850</span><span class="sxs-lookup"><span data-stu-id="e1be6-176">1850</span></span>|
|<span data-ttu-id="e1be6-177">3</span><span class="sxs-lookup"><span data-stu-id="e1be6-177">3</span></span>|<span data-ttu-id="e1be6-178">360</span><span class="sxs-lookup"><span data-stu-id="e1be6-178">360</span></span>|<span data-ttu-id="e1be6-179">640</span><span class="sxs-lookup"><span data-stu-id="e1be6-179">640</span></span>|<span data-ttu-id="e1be6-180">960</span><span class="sxs-lookup"><span data-stu-id="e1be6-180">960</span></span>|
|<span data-ttu-id="e1be6-181">4</span><span class="sxs-lookup"><span data-stu-id="e1be6-181">4</span></span>|<span data-ttu-id="e1be6-182">270</span><span class="sxs-lookup"><span data-stu-id="e1be6-182">270</span></span>|<span data-ttu-id="e1be6-183">480</span><span class="sxs-lookup"><span data-stu-id="e1be6-183">480</span></span>|<span data-ttu-id="e1be6-184">600</span><span class="sxs-lookup"><span data-stu-id="e1be6-184">600</span></span>|
|<span data-ttu-id="e1be6-185">5</span><span class="sxs-lookup"><span data-stu-id="e1be6-185">5</span></span>|<span data-ttu-id="e1be6-186">180</span><span class="sxs-lookup"><span data-stu-id="e1be6-186">180</span></span>|<span data-ttu-id="e1be6-187">320</span><span class="sxs-lookup"><span data-stu-id="e1be6-187">320</span></span>|<span data-ttu-id="e1be6-188">320</span><span class="sxs-lookup"><span data-stu-id="e1be6-188">320</span></span>|

### <a name="example-3"></a><span data-ttu-id="e1be6-189">Przykład 3</span><span class="sxs-lookup"><span data-stu-id="e1be6-189">Example 3</span></span>
<span data-ttu-id="e1be6-190">Źródło o wysokość "360" i "29.970" szybkość klatek tworzy 3 warstwy wideo:</span><span class="sxs-lookup"><span data-stu-id="e1be6-190">Source with height "360" and framerate "29.970" produces 3 video layers:</span></span>

|<span data-ttu-id="e1be6-191">Warstwy</span><span class="sxs-lookup"><span data-stu-id="e1be6-191">Layer</span></span>|<span data-ttu-id="e1be6-192">Wysokość</span><span class="sxs-lookup"><span data-stu-id="e1be6-192">Height</span></span>|<span data-ttu-id="e1be6-193">Szerokość</span><span class="sxs-lookup"><span data-stu-id="e1be6-193">Width</span></span>|<span data-ttu-id="e1be6-194">Bitrate(Kbps)</span><span class="sxs-lookup"><span data-stu-id="e1be6-194">Bitrate(kbps)</span></span>|
|---|---|---|---|
|<span data-ttu-id="e1be6-195">1</span><span class="sxs-lookup"><span data-stu-id="e1be6-195">1</span></span>|<span data-ttu-id="e1be6-196">360</span><span class="sxs-lookup"><span data-stu-id="e1be6-196">360</span></span>|<span data-ttu-id="e1be6-197">640</span><span class="sxs-lookup"><span data-stu-id="e1be6-197">640</span></span>|<span data-ttu-id="e1be6-198">700</span><span class="sxs-lookup"><span data-stu-id="e1be6-198">700</span></span>|
|<span data-ttu-id="e1be6-199">2</span><span class="sxs-lookup"><span data-stu-id="e1be6-199">2</span></span>|<span data-ttu-id="e1be6-200">270</span><span class="sxs-lookup"><span data-stu-id="e1be6-200">270</span></span>|<span data-ttu-id="e1be6-201">480</span><span class="sxs-lookup"><span data-stu-id="e1be6-201">480</span></span>|<span data-ttu-id="e1be6-202">440</span><span class="sxs-lookup"><span data-stu-id="e1be6-202">440</span></span>|
|<span data-ttu-id="e1be6-203">3</span><span class="sxs-lookup"><span data-stu-id="e1be6-203">3</span></span>|<span data-ttu-id="e1be6-204">180</span><span class="sxs-lookup"><span data-stu-id="e1be6-204">180</span></span>|<span data-ttu-id="e1be6-205">320</span><span class="sxs-lookup"><span data-stu-id="e1be6-205">320</span></span>|<span data-ttu-id="e1be6-206">230</span><span class="sxs-lookup"><span data-stu-id="e1be6-206">230</span></span>|
## <a name="media-services-learning-paths"></a><span data-ttu-id="e1be6-207">Ścieżki szkoleniowe dotyczące usługi Media Services</span><span class="sxs-lookup"><span data-stu-id="e1be6-207">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="e1be6-208">Przekazywanie opinii</span><span class="sxs-lookup"><span data-stu-id="e1be6-208">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="see-also"></a><span data-ttu-id="e1be6-209">Zobacz też</span><span class="sxs-lookup"><span data-stu-id="e1be6-209">See Also</span></span>
[<span data-ttu-id="e1be6-210">Usługi multimediów kodowania — omówienie</span><span class="sxs-lookup"><span data-stu-id="e1be6-210">Media Services Encoding Overview</span></span>](media-services-encode-asset.md)

