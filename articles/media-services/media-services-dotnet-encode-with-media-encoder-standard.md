---
title: "element zawartości przy użyciu platformy .NET Media Encoder Standard aaaEncode | Dokumentacja firmy Microsoft"
description: "W tym temacie przedstawiono sposób toouse .NET tooencode zasobów przy użyciu Media Encoder standardowa."
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: 03431b64-5518-478a-a1c2-1de345999274
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/31/2017
ms.author: juliako;anilmur
ms.openlocfilehash: 25e274c3b67168f4afc8b8ab04af2d654c9dd6e4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="encode-an-asset-with-media-encoder-standard-using-net"></a><span data-ttu-id="105d2-103">Kodowanie elementu zawartości z standardu Media Encoder Standard przy użyciu platformy .NET</span><span class="sxs-lookup"><span data-stu-id="105d2-103">Encode an asset with Media Encoder Standard using .NET</span></span>
<span data-ttu-id="105d2-104">Zadania kodowania są jednym z najbardziej typowych operacji przetwarzania hello w usłudze Media Services.</span><span class="sxs-lookup"><span data-stu-id="105d2-104">Encoding jobs are one of hello most common processing operations in Media Services.</span></span> <span data-ttu-id="105d2-105">Utworzysz kodowania plików multimedialnych tooconvert zadań z jednego tooanother kodowania.</span><span class="sxs-lookup"><span data-stu-id="105d2-105">You create encoding jobs tooconvert media files from one encoding tooanother.</span></span> <span data-ttu-id="105d2-106">Podczas kodowania, można użyć hello wbudowanych Media Encoder Media Services.</span><span class="sxs-lookup"><span data-stu-id="105d2-106">When you encode, you can use hello Media Services built-in Media Encoder.</span></span> <span data-ttu-id="105d2-107">Można również użyć kodera świadczonych przez partnera usługi Media Services; kodery innych firm są dostępne za pośrednictwem hello Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="105d2-107">You can also use an encoder provided by a Media Services partner; third party encoders are available through hello Azure Marketplace.</span></span> 

<span data-ttu-id="105d2-108">W tym temacie przedstawiono sposób toouse .NET tooencode zasobów z Media Encoder Standard (rynkowej).</span><span class="sxs-lookup"><span data-stu-id="105d2-108">This topic shows how toouse .NET tooencode your assets with Media Encoder Standard (MES).</span></span> <span data-ttu-id="105d2-109">Media Encoder Standard została skonfigurowana przy użyciu jednego ustawień kodera hello opisane [tutaj](http://go.microsoft.com/fwlink/?linkid=618336&clcid=0x409).</span><span class="sxs-lookup"><span data-stu-id="105d2-109">Media Encoder Standard is configured using one of hello encoder presets described [here](http://go.microsoft.com/fwlink/?linkid=618336&clcid=0x409).</span></span>

<span data-ttu-id="105d2-110">Zaleca się tooalways kodowanie plików źródłowych do adaptacyjnej szybkości bitowej MP4 zestawu, a następnie wykonać konwersję hello zestaw toohello pożądany format przy użyciu hello [dynamicznego tworzenia pakietów](media-services-dynamic-packaging-overview.md).</span><span class="sxs-lookup"><span data-stu-id="105d2-110">It is recommended tooalways encode your source files into an adaptive bitrate MP4 set and then convert hello set toohello desired format using hello [Dynamic Packaging](media-services-dynamic-packaging-overview.md).</span></span> 

<span data-ttu-id="105d2-111">Jeśli dane wyjściowe zawartości jest szyfrowany w magazynie, musisz skonfigurować zasady dostarczania elementu zawartości.</span><span class="sxs-lookup"><span data-stu-id="105d2-111">If your output asset is storage encrypted, you must configure asset delivery policy.</span></span> <span data-ttu-id="105d2-112">Aby uzyskać więcej informacji, zobacz [Konfigurowanie zasad dostarczania elementów zawartości](media-services-dotnet-configure-asset-delivery-policy.md).</span><span class="sxs-lookup"><span data-stu-id="105d2-112">For more information see [Configuring asset delivery policy](media-services-dotnet-configure-asset-delivery-policy.md).</span></span>

> [!NOTE]
> <span data-ttu-id="105d2-113">Rynkowej i tworzy plik wyjściowy z nazwy, która zawiera hello pierwsze 32 znaki hello nazwa pliku wejściowego.</span><span class="sxs-lookup"><span data-stu-id="105d2-113">MES produces an output file with a name that contains hello first 32 characters of hello input file name.</span></span> <span data-ttu-id="105d2-114">Nazwa Hello jest oparta na co została określona w pliku predefiniowanych hello.</span><span class="sxs-lookup"><span data-stu-id="105d2-114">hello name is based on what is specified in hello preset file.</span></span> <span data-ttu-id="105d2-115">Na przykład, "FileName": "{nazwę bazową} _ {Index} {rozszerzenia}".</span><span class="sxs-lookup"><span data-stu-id="105d2-115">For example, "FileName": "{Basename}_{Index}{Extension}".</span></span> <span data-ttu-id="105d2-116">{Nazwę bazową} zastępuje hello pierwsze 32 znaki hello nazwa pliku wejściowego.</span><span class="sxs-lookup"><span data-stu-id="105d2-116">{Basename} is replaced by hello first 32 characters of hello input file name.</span></span>
> 
> 

### <a name="mes-formats"></a><span data-ttu-id="105d2-117">Formaty rynkowej</span><span class="sxs-lookup"><span data-stu-id="105d2-117">MES Formats</span></span>
[<span data-ttu-id="105d2-118">Koderów-dekoderów i formaty</span><span class="sxs-lookup"><span data-stu-id="105d2-118">Formats and codecs</span></span>](media-services-media-encoder-standard-formats.md)

### <a name="mes-presets"></a><span data-ttu-id="105d2-119">Ustawienia wstępne usługi MES</span><span class="sxs-lookup"><span data-stu-id="105d2-119">MES Presets</span></span>
<span data-ttu-id="105d2-120">Media Encoder Standard została skonfigurowana przy użyciu jednego ustawień kodera hello opisane [tutaj](http://go.microsoft.com/fwlink/?linkid=618336&clcid=0x409).</span><span class="sxs-lookup"><span data-stu-id="105d2-120">Media Encoder Standard is configured using one of hello encoder presets described [here](http://go.microsoft.com/fwlink/?linkid=618336&clcid=0x409).</span></span>

### <a name="input-and-output-metadata"></a><span data-ttu-id="105d2-121">Wejście i wyjście metadanych</span><span class="sxs-lookup"><span data-stu-id="105d2-121">Input and output metadata</span></span>
<span data-ttu-id="105d2-122">Podczas kodowania zasób wejściowy (lub zasoby), za pomocą rynkowej, możesz uzyskać zawartości wyjściowej na powitania ukończenie tego kodowania zadań.</span><span class="sxs-lookup"><span data-stu-id="105d2-122">When you encode an input asset (or assets) using MES, you get an output asset at hello successful completion of that encode task.</span></span> <span data-ttu-id="105d2-123">zawartości wyjściowej Hello zawiera wideo, audio, miniatur, manifest itp oparte na powitania ustawienie kodowania, które można użyć.</span><span class="sxs-lookup"><span data-stu-id="105d2-123">hello output asset contains video, audio, thumbnails, manifest, etc. based on hello encoding preset you use.</span></span>

<span data-ttu-id="105d2-124">zawartości wyjściowej Hello zawiera także plik o metadane dotyczące zasobu wejściowego hello.</span><span class="sxs-lookup"><span data-stu-id="105d2-124">hello output asset also contains a file with metadata about hello input asset.</span></span> <span data-ttu-id="105d2-125">Hello nazwę pliku XML metadanych hello ma hello następującego formatu: < asset_id > _metadata.xml (na przykład 41114ad3-eb5e - 4c d 57 8 92-5354e2b7d4a4_metadata.xml), gdzie < asset_id > jest wartością IDśrodkaTrwałego hello hello zasobów wejściowych.</span><span class="sxs-lookup"><span data-stu-id="105d2-125">hello name of hello metadata XML file has hello following format: <asset_id>_metadata.xml (for example, 41114ad3-eb5e-4c57-8d92-5354e2b7d4a4_metadata.xml), where <asset_id> is hello AssetId value of hello input asset.</span></span> <span data-ttu-id="105d2-126">Hello schematu wejściowego XML metadanych opisano [tutaj](media-services-input-metadata-schema.md).</span><span class="sxs-lookup"><span data-stu-id="105d2-126">hello schema of this input metadata XML is described [here](media-services-input-metadata-schema.md).</span></span>

<span data-ttu-id="105d2-127">zawartości wyjściowej Hello zawiera także plik o metadane dotyczące zawartości wyjściowej hello.</span><span class="sxs-lookup"><span data-stu-id="105d2-127">hello output asset also contains a file with metadata about hello output asset.</span></span> <span data-ttu-id="105d2-128">Witaj nazwę pliku XML metadanych hello ma hello następującego formatu: < source_file_name > _manifest.xml (na przykład BigBuckBunny_manifest.xml).</span><span class="sxs-lookup"><span data-stu-id="105d2-128">hello name of hello metadata XML file has hello following format: <source_file_name>_manifest.xml (for example, BigBuckBunny_manifest.xml).</span></span> <span data-ttu-id="105d2-129">Schemat Hello opisano XML metadanych dane wyjściowe [tutaj](media-services-output-metadata-schema.md).</span><span class="sxs-lookup"><span data-stu-id="105d2-129">hello schema of this output metadata XML is described [here](media-services-output-metadata-schema.md).</span></span>

<span data-ttu-id="105d2-130">Jeśli chcesz tooexamine albo hello dwóch plików metadanych, można tworzyć lokalizatora SAS i Pobierz hello pliku tooyour lokalnego komputera.</span><span class="sxs-lookup"><span data-stu-id="105d2-130">If you want tooexamine either of hello two metadata files, you can create a SAS locator and download hello file tooyour local computer.</span></span> <span data-ttu-id="105d2-131">Przykład sposobu toocreate lokalizatora SAS i pobieranie plików Using hello usługi Media Services można znaleźć rozszerzenia zestawu .NET SDK.</span><span class="sxs-lookup"><span data-stu-id="105d2-131">You can find an example on how toocreate a SAS locator and download a file Using hello Media Services .NET SDK Extensions.</span></span>

## <a name="download-sample"></a><span data-ttu-id="105d2-132">Pobieranie przykładu</span><span class="sxs-lookup"><span data-stu-id="105d2-132">Download sample</span></span>
<span data-ttu-id="105d2-133">Możesz pobrać i uruchom przykład pokazujący sposób tooencode z rynkowej z [tutaj](https://azure.microsoft.com/documentation/samples/media-services-dotnet-on-demand-encoding-with-media-encoder-standard/).</span><span class="sxs-lookup"><span data-stu-id="105d2-133">You can get and run a sample that shows how tooencode with MES from [here](https://azure.microsoft.com/documentation/samples/media-services-dotnet-on-demand-encoding-with-media-encoder-standard/).</span></span>

## <a name="net-sample-code"></a><span data-ttu-id="105d2-134">.NET przykładowy kod</span><span class="sxs-lookup"><span data-stu-id="105d2-134">.NET sample code</span></span>

<span data-ttu-id="105d2-135">Poniższy przykład kodu Hello używa hello tooperform .NET SDK usługi Media Services następujące zadania:</span><span class="sxs-lookup"><span data-stu-id="105d2-135">hello following code example uses Media Services .NET SDK tooperform hello following tasks:</span></span>

* <span data-ttu-id="105d2-136">Utwórz zadania kodowania.</span><span class="sxs-lookup"><span data-stu-id="105d2-136">Create an encoding job.</span></span>
* <span data-ttu-id="105d2-137">Pobiera koder Media Encoder Standard toohello odwołania.</span><span class="sxs-lookup"><span data-stu-id="105d2-137">Get a reference toohello Media Encoder Standard encoder.</span></span>
* <span data-ttu-id="105d2-138">Określ toouse hello [adaptacyjne przesyłanie strumieniowe](media-services-autogen-bitrate-ladder-with-mes.md) wstępnie zdefiniowane.</span><span class="sxs-lookup"><span data-stu-id="105d2-138">Specify toouse hello [Adaptive Streaming](media-services-autogen-bitrate-ladder-with-mes.md) preset.</span></span> 
* <span data-ttu-id="105d2-139">Dodaj jednego zadania kodowania toohello zadań.</span><span class="sxs-lookup"><span data-stu-id="105d2-139">Add a single encoding task toohello job.</span></span> 
* <span data-ttu-id="105d2-140">Określ dane wejściowe hello zakodowane toobe zasobów.</span><span class="sxs-lookup"><span data-stu-id="105d2-140">Specify hello input asset toobe encoded.</span></span>
* <span data-ttu-id="105d2-141">Tworzenie zasobu danych wyjściowych, który będzie zawierać hello zakodowane zasobów.</span><span class="sxs-lookup"><span data-stu-id="105d2-141">Create an output asset that will contain hello encoded asset.</span></span>
* <span data-ttu-id="105d2-142">Dodaj postęp zadania hello toocheck zdarzeń programu obsługi.</span><span class="sxs-lookup"><span data-stu-id="105d2-142">Add an event handler toocheck hello job progress.</span></span>
* <span data-ttu-id="105d2-143">Prześlij zadanie hello.</span><span class="sxs-lookup"><span data-stu-id="105d2-143">Submit hello job.</span></span>

#### <a name="create-and-configure-a-visual-studio-project"></a><span data-ttu-id="105d2-144">Tworzenie i konfigurowanie projektu programu Visual Studio</span><span class="sxs-lookup"><span data-stu-id="105d2-144">Create and configure a Visual Studio project</span></span>

<span data-ttu-id="105d2-145">Konfigurowanie środowiska projektowego i wypełnić plik app.config hello o informacje dotyczące połączenia, zgodnie z opisem w [tworzenia usługi Media Services z platformą .NET](media-services-dotnet-how-to-use.md).</span><span class="sxs-lookup"><span data-stu-id="105d2-145">Set up your development environment and populate hello app.config file with connection information, as described in [Media Services development with .NET](media-services-dotnet-how-to-use.md).</span></span> 

#### <a name="example"></a><span data-ttu-id="105d2-146">Przykład</span><span class="sxs-lookup"><span data-stu-id="105d2-146">Example</span></span> 

        using System;
        using System.Linq;
        using System.Configuration;
        using System.IO;
        using System.Threading;
        using Microsoft.WindowsAzure.MediaServices.Client;

        namespace MediaEncoderStandardSample
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

                    // Create a task with hello encoding details, using a string preset.
                    // In this case "Adaptive Streaming" preset is used.
                    ITask task = job.Tasks.AddNew("My encoding task",
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

## <a name="media-services-learning-paths"></a><span data-ttu-id="105d2-147">Ścieżki szkoleniowe dotyczące usługi Media Services</span><span class="sxs-lookup"><span data-stu-id="105d2-147">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="105d2-148">Przekazywanie opinii</span><span class="sxs-lookup"><span data-stu-id="105d2-148">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="next-steps"></a><span data-ttu-id="105d2-149">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="105d2-149">Next steps</span></span>
<span data-ttu-id="105d2-150">[Jak miniatur toogenerate z platformą .NET przy użyciu standardu Media Encoder Standard](media-services-dotnet-generate-thumbnail-with-mes.md)
[usługi Media kodowanie — omówienie](media-services-encode-asset.md)</span><span class="sxs-lookup"><span data-stu-id="105d2-150">[How toogenerate thumbnail using Media Encoder Standard with .NET](media-services-dotnet-generate-thumbnail-with-mes.md)
[Media Services Encoding Overview](media-services-encode-asset.md)</span></span>

