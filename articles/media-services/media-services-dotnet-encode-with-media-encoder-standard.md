---
title: "Kodowanie elementu zawartości z standardu Media Encoder Standard przy użyciu platformy .NET | Dokumentacja firmy Microsoft"
description: "W tym temacie pokazano, jak używać .NET do zasobów przy użyciu Media Encoder standardowa kodowania."
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
ms.openlocfilehash: 929592368501c54277748bf46b2160c9058db3fb
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
# <a name="encode-an-asset-with-media-encoder-standard-using-net"></a><span data-ttu-id="703a9-103">Kodowanie elementu zawartości z standardu Media Encoder Standard przy użyciu platformy .NET</span><span class="sxs-lookup"><span data-stu-id="703a9-103">Encode an asset with Media Encoder Standard using .NET</span></span>
<span data-ttu-id="703a9-104">Zadania kodowania to jedna z operacji najczęściej przeprowadzanych przy użyciu usługi Media Services.</span><span class="sxs-lookup"><span data-stu-id="703a9-104">Encoding jobs are one of the most common processing operations in Media Services.</span></span> <span data-ttu-id="703a9-105">Zadania kodowania są tworzone w celu konwertowania plików multimediów z jednego formatu kodowania na inny.</span><span class="sxs-lookup"><span data-stu-id="703a9-105">You create encoding jobs to convert media files from one encoding to another.</span></span> <span data-ttu-id="703a9-106">Podczas kodowania, można użyć wbudowanych Media Encoder Media Services.</span><span class="sxs-lookup"><span data-stu-id="703a9-106">When you encode, you can use the Media Services built-in Media Encoder.</span></span> <span data-ttu-id="703a9-107">Można również użyć kodera świadczonych przez partnera usługi Media Services; kodery innych firm są dostępne za pośrednictwem portalu Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="703a9-107">You can also use an encoder provided by a Media Services partner; third party encoders are available through the Azure Marketplace.</span></span> 

<span data-ttu-id="703a9-108">W tym temacie przedstawiono sposób użycia platformy .NET do kodowania zasobów z Media Encoder Standard (rynkowej).</span><span class="sxs-lookup"><span data-stu-id="703a9-108">This topic shows how to use .NET to encode your assets with Media Encoder Standard (MES).</span></span> <span data-ttu-id="703a9-109">Media Encoder Standard została skonfigurowana przy użyciu jednego ustawień kodera opisane [tutaj](http://go.microsoft.com/fwlink/?linkid=618336&clcid=0x409).</span><span class="sxs-lookup"><span data-stu-id="703a9-109">Media Encoder Standard is configured using one of the encoder presets described [here](http://go.microsoft.com/fwlink/?linkid=618336&clcid=0x409).</span></span>

<span data-ttu-id="703a9-110">Zalecane jest zawsze kodowanie plików źródłowych do adaptacyjnej szybkości bitowej MP4 zestawu, a następnie wykonać konwersję zestaw na żądany format za pomocą [dynamicznego tworzenia pakietów](media-services-dynamic-packaging-overview.md).</span><span class="sxs-lookup"><span data-stu-id="703a9-110">It is recommended to always encode your source files into an adaptive bitrate MP4 set and then convert the set to the desired format using the [Dynamic Packaging](media-services-dynamic-packaging-overview.md).</span></span> 

<span data-ttu-id="703a9-111">Jeśli dane wyjściowe zawartości jest szyfrowany w magazynie, musisz skonfigurować zasady dostarczania elementu zawartości.</span><span class="sxs-lookup"><span data-stu-id="703a9-111">If your output asset is storage encrypted, you must configure asset delivery policy.</span></span> <span data-ttu-id="703a9-112">Aby uzyskać więcej informacji, zobacz [Konfigurowanie zasad dostarczania elementów zawartości](media-services-dotnet-configure-asset-delivery-policy.md).</span><span class="sxs-lookup"><span data-stu-id="703a9-112">For more information see [Configuring asset delivery policy](media-services-dotnet-configure-asset-delivery-policy.md).</span></span>

> [!NOTE]
> <span data-ttu-id="703a9-113">Rynkowej tworzy plik wyjściowy z nazwy, która zawiera najpierw 32 znaków nazwy pliku wejściowego.</span><span class="sxs-lookup"><span data-stu-id="703a9-113">MES produces an output file with a name that contains the first 32 characters of the input file name.</span></span> <span data-ttu-id="703a9-114">Nazwa jest oparty na nazwie określonej w istniejących plików.</span><span class="sxs-lookup"><span data-stu-id="703a9-114">The name is based on what is specified in the preset file.</span></span> <span data-ttu-id="703a9-115">Na przykład, "FileName": "{nazwę bazową} _ {Index} {rozszerzenia}".</span><span class="sxs-lookup"><span data-stu-id="703a9-115">For example, "FileName": "{Basename}_{Index}{Extension}".</span></span> <span data-ttu-id="703a9-116">{Nazwę bazową} zostanie zastąpiony przez pierwsze 32 znaków nazwy pliku wejściowego.</span><span class="sxs-lookup"><span data-stu-id="703a9-116">{Basename} is replaced by the first 32 characters of the input file name.</span></span>
> 
> 

### <a name="mes-formats"></a><span data-ttu-id="703a9-117">Formaty rynkowej</span><span class="sxs-lookup"><span data-stu-id="703a9-117">MES Formats</span></span>
[<span data-ttu-id="703a9-118">Koderów-dekoderów i formaty</span><span class="sxs-lookup"><span data-stu-id="703a9-118">Formats and codecs</span></span>](media-services-media-encoder-standard-formats.md)

### <a name="mes-presets"></a><span data-ttu-id="703a9-119">Ustawienia wstępne usługi MES</span><span class="sxs-lookup"><span data-stu-id="703a9-119">MES Presets</span></span>
<span data-ttu-id="703a9-120">Media Encoder Standard została skonfigurowana przy użyciu jednego ustawień kodera opisane [tutaj](http://go.microsoft.com/fwlink/?linkid=618336&clcid=0x409).</span><span class="sxs-lookup"><span data-stu-id="703a9-120">Media Encoder Standard is configured using one of the encoder presets described [here](http://go.microsoft.com/fwlink/?linkid=618336&clcid=0x409).</span></span>

### <a name="input-and-output-metadata"></a><span data-ttu-id="703a9-121">Wejście i wyjście metadanych</span><span class="sxs-lookup"><span data-stu-id="703a9-121">Input and output metadata</span></span>
<span data-ttu-id="703a9-122">Podczas kodowania zasób wejściowy (lub zasoby), za pomocą rynkowej, Pobierz zasób dane wyjściowe po pomyślnym zakończeniu tego kodowania zadań.</span><span class="sxs-lookup"><span data-stu-id="703a9-122">When you encode an input asset (or assets) using MES, you get an output asset at the successful completion of that encode task.</span></span> <span data-ttu-id="703a9-123">Elementu zawartości wyjściowej zawiera wideo, audio, miniatur, manifestu, itp., oparte na ustawienie kodowania, które można użyć.</span><span class="sxs-lookup"><span data-stu-id="703a9-123">The output asset contains video, audio, thumbnails, manifest, etc. based on the encoding preset you use.</span></span>

<span data-ttu-id="703a9-124">Elementu zawartości wyjściowej zawiera także plik o metadane dotyczące zasobu wejściowego.</span><span class="sxs-lookup"><span data-stu-id="703a9-124">The output asset also contains a file with metadata about the input asset.</span></span> <span data-ttu-id="703a9-125">Nazwa pliku XML metadanych ma następujący format: < asset_id > _metadata.xml (na przykład 41114ad3-eb5e - 4c d 57 8 92-5354e2b7d4a4_metadata.xml), gdzie < asset_id > jest wartość IDśrodkaTrwałego zasobów wejściowych.</span><span class="sxs-lookup"><span data-stu-id="703a9-125">The name of the metadata XML file has the following format: <asset_id>_metadata.xml (for example, 41114ad3-eb5e-4c57-8d92-5354e2b7d4a4_metadata.xml), where <asset_id> is the AssetId value of the input asset.</span></span> <span data-ttu-id="703a9-126">Schemat wejściowego XML metadanych jest opisany [tutaj](media-services-input-metadata-schema.md).</span><span class="sxs-lookup"><span data-stu-id="703a9-126">The schema of this input metadata XML is described [here](media-services-input-metadata-schema.md).</span></span>

<span data-ttu-id="703a9-127">Elementu zawartości wyjściowej zawiera także plik o metadane dotyczące zawartości wyjściowej.</span><span class="sxs-lookup"><span data-stu-id="703a9-127">The output asset also contains a file with metadata about the output asset.</span></span> <span data-ttu-id="703a9-128">Nazwa pliku XML metadanych ma następujący format: < source_file_name > _manifest.xml (na przykład BigBuckBunny_manifest.xml).</span><span class="sxs-lookup"><span data-stu-id="703a9-128">The name of the metadata XML file has the following format: <source_file_name>_manifest.xml (for example, BigBuckBunny_manifest.xml).</span></span> <span data-ttu-id="703a9-129">Schemat opisano XML metadanych dane wyjściowe [tutaj](media-services-output-metadata-schema.md).</span><span class="sxs-lookup"><span data-stu-id="703a9-129">The schema of this output metadata XML is described [here](media-services-output-metadata-schema.md).</span></span>

<span data-ttu-id="703a9-130">Jeśli chcesz sprawdzić z jednej z dwóch plików metadanych, można utworzyć lokalizatora SAS i Pobierz plik na komputerze lokalnym.</span><span class="sxs-lookup"><span data-stu-id="703a9-130">If you want to examine either of the two metadata files, you can create a SAS locator and download the file to your local computer.</span></span> <span data-ttu-id="703a9-131">Przykład można znaleźć na tworzenie lokalizatora SAS i Pobierz plik przy użyciu rozszerzenia SDK .NET usługi Media Services.</span><span class="sxs-lookup"><span data-stu-id="703a9-131">You can find an example on how to create a SAS locator and download a file Using the Media Services .NET SDK Extensions.</span></span>

## <a name="download-sample"></a><span data-ttu-id="703a9-132">Pobieranie przykładu</span><span class="sxs-lookup"><span data-stu-id="703a9-132">Download sample</span></span>
<span data-ttu-id="703a9-133">Możesz pobrać i uruchom przykład pokazujący sposób kodowania z rynkowej z [tutaj](https://azure.microsoft.com/documentation/samples/media-services-dotnet-on-demand-encoding-with-media-encoder-standard/).</span><span class="sxs-lookup"><span data-stu-id="703a9-133">You can get and run a sample that shows how to encode with MES from [here](https://azure.microsoft.com/documentation/samples/media-services-dotnet-on-demand-encoding-with-media-encoder-standard/).</span></span>

## <a name="net-sample-code"></a><span data-ttu-id="703a9-134">.NET przykładowy kod</span><span class="sxs-lookup"><span data-stu-id="703a9-134">.NET sample code</span></span>

<span data-ttu-id="703a9-135">Poniższy przykład kodu wykorzystuje .NET SDK usługi Media Services do wykonywania następujących zadań:</span><span class="sxs-lookup"><span data-stu-id="703a9-135">The following code example uses Media Services .NET SDK to perform the following tasks:</span></span>

* <span data-ttu-id="703a9-136">Utwórz zadania kodowania.</span><span class="sxs-lookup"><span data-stu-id="703a9-136">Create an encoding job.</span></span>
* <span data-ttu-id="703a9-137">Pobierz odwołanie do kodera Media Encoder Standard.</span><span class="sxs-lookup"><span data-stu-id="703a9-137">Get a reference to the Media Encoder Standard encoder.</span></span>
* <span data-ttu-id="703a9-138">Określ użycie [adaptacyjne przesyłanie strumieniowe](media-services-autogen-bitrate-ladder-with-mes.md) wstępnie zdefiniowane.</span><span class="sxs-lookup"><span data-stu-id="703a9-138">Specify to use the [Adaptive Streaming](media-services-autogen-bitrate-ladder-with-mes.md) preset.</span></span> 
* <span data-ttu-id="703a9-139">Dodaj pojedynczego zadania kodowania do zadania.</span><span class="sxs-lookup"><span data-stu-id="703a9-139">Add a single encoding task to the job.</span></span> 
* <span data-ttu-id="703a9-140">Określ wejściowych zasobów do zakodowania.</span><span class="sxs-lookup"><span data-stu-id="703a9-140">Specify the input asset to be encoded.</span></span>
* <span data-ttu-id="703a9-141">Utwórz zasób danych wyjściowych, który będzie zawierać zakodowanym elementem zawartości.</span><span class="sxs-lookup"><span data-stu-id="703a9-141">Create an output asset that will contain the encoded asset.</span></span>
* <span data-ttu-id="703a9-142">Dodaj program obsługi zdarzeń, aby sprawdzić postęp zadania.</span><span class="sxs-lookup"><span data-stu-id="703a9-142">Add an event handler to check the job progress.</span></span>
* <span data-ttu-id="703a9-143">Przesłać zadanie.</span><span class="sxs-lookup"><span data-stu-id="703a9-143">Submit the job.</span></span>

#### <a name="create-and-configure-a-visual-studio-project"></a><span data-ttu-id="703a9-144">Tworzenie i konfigurowanie projektu programu Visual Studio</span><span class="sxs-lookup"><span data-stu-id="703a9-144">Create and configure a Visual Studio project</span></span>

<span data-ttu-id="703a9-145">Skonfiguruj środowisko projektowe i wypełnij plik app.config przy użyciu informacji dotyczących połączenia, zgodnie z opisem w sekcji [Projektowanie usługi Media Services na platformie .NET](media-services-dotnet-how-to-use.md).</span><span class="sxs-lookup"><span data-stu-id="703a9-145">Set up your development environment and populate the app.config file with connection information, as described in [Media Services development with .NET](media-services-dotnet-how-to-use.md).</span></span> 

#### <a name="example"></a><span data-ttu-id="703a9-146">Przykład</span><span class="sxs-lookup"><span data-stu-id="703a9-146">Example</span></span> 

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

                    // Encode and generate the output using the "Adaptive Streaming" preset.
                    EncodeToAdaptiveBitrateMP4Set(asset);

                    Console.ReadLine();
                }

                static public IAsset EncodeToAdaptiveBitrateMP4Set(IAsset asset)
                {
                    // Declare a new job.
                    IJob job = _context.Jobs.Create("Media Encoder Standard Job");
                    // Get a media processor reference, and pass to it the name of the 
                    // processor to use for the specific task.
                    IMediaProcessor processor = GetLatestMediaProcessorByName("Media Encoder Standard");

                    // Create a task with the encoding details, using a string preset.
                    // In this case "Adaptive Streaming" preset is used.
                    ITask task = job.Tasks.AddNew("My encoding task",
                        processor,
                        "Adaptive Streaming",
                        TaskOptions.None);

                    // Specify the input asset to be encoded.
                    task.InputAssets.Add(asset);
                    // Add an output asset to contain the results of the job. 
                    // This output is specified as AssetCreationOptions.None, which 
                    // means the output asset is not encrypted. 
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

## <a name="media-services-learning-paths"></a><span data-ttu-id="703a9-147">Ścieżki szkoleniowe dotyczące usługi Media Services</span><span class="sxs-lookup"><span data-stu-id="703a9-147">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="703a9-148">Przekazywanie opinii</span><span class="sxs-lookup"><span data-stu-id="703a9-148">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="next-steps"></a><span data-ttu-id="703a9-149">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="703a9-149">Next steps</span></span>
<span data-ttu-id="703a9-150">[Sposób generowania miniatury z platformą .NET przy użyciu standardu Media Encoder Standard](media-services-dotnet-generate-thumbnail-with-mes.md)
[usługi Media kodowanie — omówienie](media-services-encode-asset.md)</span><span class="sxs-lookup"><span data-stu-id="703a9-150">[How to generate thumbnail using Media Encoder Standard with .NET](media-services-dotnet-generate-thumbnail-with-mes.md)
[Media Services Encoding Overview](media-services-encode-asset.md)</span></span>

