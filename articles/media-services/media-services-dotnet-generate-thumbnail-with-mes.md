---
title: "miniatury toogenerate aaaHow przy użyciu standardu Media Encoder Standard z platformą .NET"
description: "W tym temacie przedstawiono sposób toouse .NET tooencode zasobów oraz generowanie miniatur na powitania tym samym czasie przy użyciu standardu Media Encoder Standard."
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: b8dab73a-1d91-4b6d-9741-a92ad39fc3f7
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/14/2017
ms.author: juliako
ms.openlocfilehash: 23d3e4d9bf64a688d45499c045f19d2792167990
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toogenerate-thumbnails-using-media-encoder-standard-with-net"></a><span data-ttu-id="ff847-103">Jak miniatur toogenerate przy użyciu standardu Media Encoder Standard z platformą .NET</span><span class="sxs-lookup"><span data-stu-id="ff847-103">How toogenerate thumbnails using Media Encoder Standard with .NET</span></span>

<span data-ttu-id="ff847-104">Można użyć toogenerate Media Encoder Standard miniatur co najmniej jeden z wejściowego pliku wideo w [JPEG](https://en.wikipedia.org/wiki/JPEG), [PNG](https://en.wikipedia.org/wiki/Portable_Network_Graphics), lub [BMP](https://en.wikipedia.org/wiki/BMP_file_format) obrazów w formatach.</span><span class="sxs-lookup"><span data-stu-id="ff847-104">You can use Media Encoder Standard toogenerate one or more thumbnails from your input video in [JPEG](https://en.wikipedia.org/wiki/JPEG), [PNG](https://en.wikipedia.org/wiki/Portable_Network_Graphics), or [BMP](https://en.wikipedia.org/wiki/BMP_file_format) image file formats.</span></span> <span data-ttu-id="ff847-105">Można przesłać zadania, które powodują powstanie tylko obrazy, lub można łączyć generowanie miniatur z kodowaniem.</span><span class="sxs-lookup"><span data-stu-id="ff847-105">You can submit Tasks that produce only images, or you can combine thumbnail generation with encoding.</span></span> <span data-ttu-id="ff847-106">Ten temat zawiera kilka przykładowych XML i JSON miniatur ustawienia dla tych scenariuszy.</span><span class="sxs-lookup"><span data-stu-id="ff847-106">This topic provides a few sample XML and JSON thumbnail presets for such scenarios.</span></span> <span data-ttu-id="ff847-107">Na końcu hello hello tematu, istnieje [przykładowy kod](#code_sample) który pokazuje, jak toouse hello .NET SDK usługi Media Services tooaccomplish hello kodowania zadań.</span><span class="sxs-lookup"><span data-stu-id="ff847-107">At hello end of hello topic, there is a [sample code](#code_sample) that shows how toouse hello Media Services .NET SDK tooaccomplish hello encoding task.</span></span>

<span data-ttu-id="ff847-108">Więcej szczegółów na powitania elementów, które są używane w predefiniowane próbki, należy przejrzeć [Media Encoder Standard schematu](media-services-mes-schema.md).</span><span class="sxs-lookup"><span data-stu-id="ff847-108">For more details on hello elements that are used in sample presets, you should review [Media Encoder Standard schema](media-services-mes-schema.md).</span></span>

<span data-ttu-id="ff847-109">Upewnij się, że hello tooreview [zagadnienia](media-services-dotnet-generate-thumbnail-with-mes.md#considerations) sekcji.</span><span class="sxs-lookup"><span data-stu-id="ff847-109">Make sure tooreview hello [Considerations](media-services-dotnet-generate-thumbnail-with-mes.md#considerations) section.</span></span>

## <a name="example--single-png-file"></a><span data-ttu-id="ff847-110">Przykład — pojedynczy plik PNG</span><span class="sxs-lookup"><span data-stu-id="ff847-110">Example – single PNG file</span></span>

<span data-ttu-id="ff847-111">Witaj następującego formatu JSON i XML ustawienie może być używane tooproduce pojedynczego wyjścia PNG pliku poza hello najpierw kilka sekund wejściowy plik wideo hello, gdzie kodera hello sprawia, że próba optymalnych Znajdowanie ramki "interesujące".</span><span class="sxs-lookup"><span data-stu-id="ff847-111">hello following JSON and XML preset can be used tooproduce a single output PNG file out of hello first few seconds of hello input video, where hello encoder makes a best-effort attempt at finding an “interesting” frame.</span></span> <span data-ttu-id="ff847-112">Należy pamiętać, że wymiary obrazu wyjściowego hello ustawiono too100%, co oznacza, że odpowiadają one hello wymiary hello wejściowy plik wideo.</span><span class="sxs-lookup"><span data-stu-id="ff847-112">Note that hello output image dimensions have been set too100%, meaning these will match hello dimensions of hello input video.</span></span> <span data-ttu-id="ff847-113">Należy też zauważyć, jak ustawienie "Format" hello "Dane wyjściowe" jest wymagane użycie hello toomatch "PngLayers" w sekcji "Koderów-dekoderów" hello.</span><span class="sxs-lookup"><span data-stu-id="ff847-113">Note also how hello “Format” setting in “Outputs” is required toomatch hello use of “PngLayers” in hello “Codecs” section.</span></span> 

### <a name="json-preset"></a><span data-ttu-id="ff847-114">Ustawienie wstępne JSON</span><span class="sxs-lookup"><span data-stu-id="ff847-114">JSON preset</span></span>

    {
      "Version": 1.0,
      "Codecs": [
        {
          "PngLayers": [
            {
              "Type": "PngLayer",
              "Width": "100%",
              "Height": "100%"
            }
          ],
          "Start": "{Best}",
          "Type": "PngImage"
        }
      ],
      "Outputs": [
        {
          "FileName": "{Basename}_{Index}{Extension}",
          "Format": {
            "Type": "PngFormat"
          }
        }
      ]
    }
    
### <a name="xml-preset"></a><span data-ttu-id="ff847-115">Ustawienie wstępne XML</span><span class="sxs-lookup"><span data-stu-id="ff847-115">XML preset</span></span>

    <?xml version="1.0" encoding="utf-16"?>
    <Preset xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" Version="1.0" xmlns="http://www.windowsazure.com/media/encoding/Preset/2014/03">
      <Encoding>
        <PngImage Start="{Best}">
          <PngLayers>
            <PngLayer>
              <Width>100%</Width>
              <Height>100%</Height>
            </PngLayer>
          </PngLayers>
        </PngImage>
      </Encoding>
      <Outputs>
        <Output FileName="{Basename}_{Index}{Extension}">
          <PngFormat />
        </Output>
      </Outputs>
    </Preset>

## <a name="example--a-series-of-jpeg-images"></a><span data-ttu-id="ff847-116">Przykład — szereg obrazy JPEG</span><span class="sxs-lookup"><span data-stu-id="ff847-116">Example – a series of JPEG images</span></span>

<span data-ttu-id="ff847-117">Witaj następującego formatu JSON i XML ustawienie może być używane tooproduce zestaw 10 obrazów w sygnatury czasowe 5% 15%,..., 95% wejściowych osi czasu hello, których rozmiar obrazu hello jest określony toobe co kwartał, który hello wejściowych wideo.</span><span class="sxs-lookup"><span data-stu-id="ff847-117">hello following JSON and XML preset can be used tooproduce a set of 10 images at timestamps of 5%, 15%, …, 95% of hello input timeline, where hello image size is specified toobe one quarter that of hello input video.</span></span>

### <a name="json-preset"></a><span data-ttu-id="ff847-118">Ustawienie wstępne JSON</span><span class="sxs-lookup"><span data-stu-id="ff847-118">JSON preset</span></span>

    {
      "Version": 1.0,
      "Codecs": [
        {
          "JpgLayers": [
            {
              "Quality": 90,
              "Type": "JpgLayer",
              "Width": "25%",
              "Height": "25%"
            }
          ],
          "Start": "5%",
          "Step": "1",
          "Range": "1",
          "Type": "JpgImage"
        }
      ],
      "Outputs": [
        {
          "FileName": "{Basename}_{Index}{Extension}",
          "Format": {
            "Type": "JpgFormat"
          }
        }
      ]
    }

### <a name="xml-preset"></a><span data-ttu-id="ff847-119">Ustawienie wstępne XML</span><span class="sxs-lookup"><span data-stu-id="ff847-119">XML preset</span></span>
    
    <?xml version="1.0" encoding="utf-16"?>
    <Preset xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" Version="1.0" xmlns="http://www.windowsazure.com/media/encoding/Preset/2014/03">
      <Encoding>
        <JpgImage Start="5%" Step="10%" Range="96%">
          <JpgLayers>
            <JpgLayer>
              <Width>25%</Width>
              <Height>25%</Height>
              <Quality>90</Quality>
            </JpgLayer>
          </JpgLayers>
        </JpgImage>
      </Encoding>
      <Outputs>
        <Output FileName="{Basename}_{Index}{Extension}">
          <JpgFormat />
        </Output>
      </Outputs>
    </Preset>

## <a name="example--one-image-at-a-specific-timestamp"></a><span data-ttu-id="ff847-120">Przykład — jeden obraz w określonej sygnatury czasowej</span><span class="sxs-lookup"><span data-stu-id="ff847-120">Example – one image at a specific timestamp</span></span>

<span data-ttu-id="ff847-121">Hello następujące ustawienie wstępne JSON i XML może być używane tooproduce jeden obraz JPEG na powitania 30 sekund znak wejściowy plik wideo hello.</span><span class="sxs-lookup"><span data-stu-id="ff847-121">hello following JSON and XML preset can be used tooproduce a single JPEG image at hello 30 second mark of hello input video.</span></span> <span data-ttu-id="ff847-122">To ustawienie wstępne oczekuje toobe wejściowych hello ponad 30 sekund czasu trwania (else zadania hello zakończy się niepowodzeniem).</span><span class="sxs-lookup"><span data-stu-id="ff847-122">This preset expects hello input toobe more than 30 seconds in duration (else hello job will fail).</span></span>

### <a name="json-preset"></a><span data-ttu-id="ff847-123">Ustawienie wstępne JSON</span><span class="sxs-lookup"><span data-stu-id="ff847-123">JSON preset</span></span>

    {
      "Version": 1.0,
      "Codecs": [
        {
          "JpgLayers": [
            {
              "Quality": 90,
              "Type": "JpgLayer",
              "Width": "25%",
              "Height": "25%"
            }
          ],
          "Start": "00:00:30",
          "Step": "1",
          "Range": "1",
          "Type": "JpgImage"
        }
      ],
      "Outputs": [
        {
          "FileName": "{Basename}_{Index}{Extension}",
          "Format": {
            "Type": "JpgFormat"
          }
        }
      ]
    }
    
### <a name="xml-preset"></a><span data-ttu-id="ff847-124">Ustawienie wstępne XML</span><span class="sxs-lookup"><span data-stu-id="ff847-124">XML preset</span></span>
    
    <?xml version="1.0" encoding="utf-16"?>
    <Preset xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" Version="1.0" xmlns="http://www.windowsazure.com/media/encoding/Preset/2014/03">
      <Encoding>
        <JpgImage Start="00:00:30" Step="00:00:02" Range="00:00:01">
          <JpgLayers>
            <JpgLayer>
              <Width>25%</Width>
              <Height>25%</Height>
              <Quality>90</Quality>
            </JpgLayer>
          </JpgLayers>
        </JpgImage>
      </Encoding>
      <Outputs>
        <Output FileName="{Basename}_{Index}{Extension}">
          <JpgFormat />
        </Output>
      </Outputs>
    </Preset>

## <span data-ttu-id="ff847-125"><a id="code_sample"></a>Przykład — kodowanie wideo i generowanie miniatur</span><span class="sxs-lookup"><span data-stu-id="ff847-125"><a id="code_sample"></a>Example – encode video and generate thumbnail</span></span>

<span data-ttu-id="ff847-126">Poniższy przykład kodu Hello używa hello tooperform .NET SDK usługi Media Services następujące zadania:</span><span class="sxs-lookup"><span data-stu-id="ff847-126">hello following code example uses Media Services .NET SDK tooperform hello following tasks:</span></span>

* <span data-ttu-id="ff847-127">Utwórz zadania kodowania.</span><span class="sxs-lookup"><span data-stu-id="ff847-127">Create an encoding job.</span></span>
* <span data-ttu-id="ff847-128">Pobiera koder Media Encoder Standard toohello odwołania.</span><span class="sxs-lookup"><span data-stu-id="ff847-128">Get a reference toohello Media Encoder Standard encoder.</span></span>
* <span data-ttu-id="ff847-129">Ustawienia wstępnego ładowania hello [XML](media-services-dotnet-generate-thumbnail-with-mes.md#xml) lub [JSON](media-services-dotnet-generate-thumbnail-with-mes.md#json) zawierających hello kodowanie ustawienia wstępnego również miniatur toogenerate potrzebne informacje.</span><span class="sxs-lookup"><span data-stu-id="ff847-129">Load hello preset [XML](media-services-dotnet-generate-thumbnail-with-mes.md#xml) or [JSON](media-services-dotnet-generate-thumbnail-with-mes.md#json) that contain hello encoding preset as well as information needed toogenerate thumbnails.</span></span> <span data-ttu-id="ff847-130">Można go zapisać [XML](media-services-dotnet-generate-thumbnail-with-mes.md#xml) lub [JSON](media-services-dotnet-generate-thumbnail-with-mes.md#json) w pliku i użyj hello, następującego pliku hello tooload kodu.</span><span class="sxs-lookup"><span data-stu-id="ff847-130">You can save this  [XML](media-services-dotnet-generate-thumbnail-with-mes.md#xml) or [JSON](media-services-dotnet-generate-thumbnail-with-mes.md#json) in a file and use hello following code tooload hello file.</span></span>
  
        // Load hello XML (or JSON) from hello local file.
        string configuration = File.ReadAllText(fileName);  
* <span data-ttu-id="ff847-131">Dodaj jednego zadania kodowania toohello zadań.</span><span class="sxs-lookup"><span data-stu-id="ff847-131">Add a single encoding task toohello job.</span></span> 
* <span data-ttu-id="ff847-132">Określ dane wejściowe hello zakodowane toobe zasobów.</span><span class="sxs-lookup"><span data-stu-id="ff847-132">Specify hello input asset toobe encoded.</span></span>
* <span data-ttu-id="ff847-133">Tworzenie zasobu danych wyjściowych, który będzie zawierać hello zakodowane zasobów.</span><span class="sxs-lookup"><span data-stu-id="ff847-133">Create an output asset that will contain hello encoded asset.</span></span>
* <span data-ttu-id="ff847-134">Dodaj postęp zadania hello toocheck zdarzeń programu obsługi.</span><span class="sxs-lookup"><span data-stu-id="ff847-134">Add an event handler toocheck hello job progress.</span></span>
* <span data-ttu-id="ff847-135">Prześlij zadanie hello.</span><span class="sxs-lookup"><span data-stu-id="ff847-135">Submit hello job.</span></span>

<span data-ttu-id="ff847-136">Zobacz hello [tworzenia usługi Media Services z platformą .NET](media-services-dotnet-how-to-use.md) tematu, aby uzyskać instrukcje na temat tooset Twojego środowiska deweloperów.</span><span class="sxs-lookup"><span data-stu-id="ff847-136">See hello [Media Services development with .NET](media-services-dotnet-how-to-use.md) topic for directions on how tooset up your dev environment.</span></span>

        using System;
        using System.Configuration;
        using System.IO;
        using System.Linq;
        using Microsoft.WindowsAzure.MediaServices.Client;
        using System.Threading;

        namespace EncodeAndGenerateThumbnails
        {
        class Program
        {
            // Read values from hello App.config file.
            private static readonly string _AADTenantDomain =
            ConfigurationManager.AppSettings["AADTenantDomain"];
            private static readonly string _RESTAPIEndpoint =
            ConfigurationManager.AppSettings["MediaServiceRESTAPIEndpoint"];

            private static CloudMediaContext _context = null;

            private static readonly string _mediaFiles =
            Path.GetFullPath(@"../..\Media");

            private static readonly string _singleMP4File =
            Path.Combine(_mediaFiles, @"BigBuckBunny.mp4");

            static void Main(string[] args)
            {
            var tokenCredentials = new AzureAdTokenCredentials(_AADTenantDomain, AzureEnvironments.AzureCloudEnvironment);
            var tokenProvider = new AzureAdTokenProvider(tokenCredentials);

            _context = new CloudMediaContext(new Uri(_RESTAPIEndpoint), tokenProvider);

            // Get an uploaded asset.
            var asset = _context.Assets.FirstOrDefault();

            // Encode and generate hello thumbnails.
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

            // Load hello XML (or JSON) from hello local file.
            string configuration = File.ReadAllText("ThumbnailPreset_JSON.json");

            // Create a task
            ITask task = job.Tasks.AddNew("Media Encoder Standard encoding task",
                processor,
                configuration,
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

## <span data-ttu-id="ff847-137"><a id="json"></a>Ustawienie JSON miniatur</span><span class="sxs-lookup"><span data-stu-id="ff847-137"><a id="json"></a>Thumbnail JSON preset</span></span>
<span data-ttu-id="ff847-138">Aby uzyskać informacje o schemacie, zobacz [to](https://msdn.microsoft.com/library/mt269962.aspx) tematu.</span><span class="sxs-lookup"><span data-stu-id="ff847-138">For information about schema, see [this](https://msdn.microsoft.com/library/mt269962.aspx) topic.</span></span>

    {
      "Version": 1.0,
      "Codecs": [
        {
          "KeyFrameInterval": "00:00:02",
          "SceneChangeDetection": "true",
          "H264Layers": [
            {
              "Profile": "Auto",
              "Level": "auto",
              "Bitrate": 4500,
              "MaxBitrate": 4500,
              "BufferWindow": "00:00:05",
              "Width": 1280,
              "Height": 720,
              "ReferenceFrames": 3,
              "EntropyMode": "Cabac",
              "AdaptiveBFrame": true,
              "Type": "H264Layer",
              "FrameRate": "0/1"
    
            }
          ],
          "Type": "H264Video"
        },
        {
          "JpgLayers": [
            {
              "Quality": 90,
              "Type": "JpgLayer",
              "Width": "100%",
              "Height": "100%"
            }
          ],
          "Start": "{Best}",
          "Type": "JpgImage"
        },
        {
          "Channels": 2,
          "SamplingRate": 48000,
          "Bitrate": 128,
          "Type": "AACAudio"
        }
      ],
      "Outputs": [
        {
          "FileName": "{Basename}_{Index}{Extension}",
          "Format": {
            "Type": "JpgFormat"
          }
        },
        {
          "FileName": "{Basename}_{Resolution}_{VideoBitrate}.mp4",
          "Format": {
            "Type": "MP4Format"
          }
        }
      ]
    }

## <span data-ttu-id="ff847-139"><a id="xml"></a>Ustawienie XML miniatur</span><span class="sxs-lookup"><span data-stu-id="ff847-139"><a id="xml"></a>Thumbnail XML preset</span></span>
<span data-ttu-id="ff847-140">Aby uzyskać informacje o schemacie, zobacz [to](https://msdn.microsoft.com/library/mt269962.aspx) tematu.</span><span class="sxs-lookup"><span data-stu-id="ff847-140">For information about schema, see [this](https://msdn.microsoft.com/library/mt269962.aspx) topic.</span></span>
    
    <?xml version="1.0" encoding="utf-16"?>
    <Preset xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" Version="1.0" xmlns="http://www.windowsazure.com/media/encoding/Preset/2014/03">
      <Encoding>
        <H264Video>
          <KeyFrameInterval>00:00:02</KeyFrameInterval>
          <SceneChangeDetection>true</SceneChangeDetection>
          <H264Layers>
            <H264Layer>
              <Bitrate>4500</Bitrate>
              <Width>1280</Width>
              <Height>720</Height>
              <FrameRate>0/1</FrameRate>
              <Profile>Auto</Profile>
              <Level>auto</Level>
              <BFrames>3</BFrames>
              <ReferenceFrames>3</ReferenceFrames>
              <Slices>0</Slices>
              <AdaptiveBFrame>true</AdaptiveBFrame>
              <EntropyMode>Cabac</EntropyMode>
              <BufferWindow>00:00:05</BufferWindow>
              <MaxBitrate>4500</MaxBitrate>
            </H264Layer>
          </H264Layers>
        </H264Video>
        <AACAudio>
          <Profile>AACLC</Profile>
          <Channels>2</Channels>
          <SamplingRate>48000</SamplingRate>
          <Bitrate>128</Bitrate>
        </AACAudio>
        <JpgImage Start="{Best}">
          <JpgLayers>
            <JpgLayer>
              <Width>100%</Width>
              <Height>100%/Height>
              <Quality>90</Quality>
            </JpgLayer>
          </JpgLayers>
        </JpgImage>
      </Encoding>
      <Outputs>
        <Output FileName="{Basename}_{Resolution}_{VideoBitrate}.mp4">
          <MP4Format />
        </Output>
        <Output FileName="{Basename}_{Index}{Extension}">
          <JpgFormat />
        </Output>
      </Outputs>
    </Preset>

## <a name="considerations"></a><span data-ttu-id="ff847-141">Zagadnienia do rozważenia</span><span class="sxs-lookup"><span data-stu-id="ff847-141">Considerations</span></span>
<span data-ttu-id="ff847-142">Zastosuj Hello następujące zagadnienia:</span><span class="sxs-lookup"><span data-stu-id="ff847-142">hello following considerations apply:</span></span>

* <span data-ttu-id="ff847-143">Hello użycie jawnego znacznika czasu rozpoczęcia/krok/zakresu przyjęto założenie, że źródło danych wejściowych w tym hello jest co najmniej 1 minutę.</span><span class="sxs-lookup"><span data-stu-id="ff847-143">hello use of explicit timestamps for Start/Step/Range assumes that hello input source is at least 1 minute long.</span></span>
* <span data-ttu-id="ff847-144">Elementy BmpImage-jpg/Png mają Start, krok i zakres string atrybutów — mogą być interpretowane jako:</span><span class="sxs-lookup"><span data-stu-id="ff847-144">Jpg/Png/BmpImage elements have Start, Step and Range string attributes – these can be interpreted as:</span></span>
  
  * <span data-ttu-id="ff847-145">Numer ramki, jeśli są one — nieujemne liczby całkowite, np.</span><span class="sxs-lookup"><span data-stu-id="ff847-145">Frame Number if they are non-negative integers, eg.</span></span> <span data-ttu-id="ff847-146">"Start": "120"</span><span class="sxs-lookup"><span data-stu-id="ff847-146">"Start": "120",</span></span>
  * <span data-ttu-id="ff847-147">Względna toosource czas trwania, jeśli wyrażony jako sufiks %, np.</span><span class="sxs-lookup"><span data-stu-id="ff847-147">Relative toosource duration if expressed as %-suffixed, eg.</span></span> <span data-ttu-id="ff847-148">"Start": "15%", lub</span><span class="sxs-lookup"><span data-stu-id="ff847-148">"Start": "15%", OR</span></span>
  * <span data-ttu-id="ff847-149">Sygnatura czasowa Jeśli wyrażonej w postaci hh: mm:...</span><span class="sxs-lookup"><span data-stu-id="ff847-149">Timestamp if expressed as HH:MM:SS…</span></span> <span data-ttu-id="ff847-150">Format.</span><span class="sxs-lookup"><span data-stu-id="ff847-150">format.</span></span> <span data-ttu-id="ff847-151">Np.</span><span class="sxs-lookup"><span data-stu-id="ff847-151">Eg.</span></span> <span data-ttu-id="ff847-152">"Start": "00: 01:00"</span><span class="sxs-lookup"><span data-stu-id="ff847-152">"Start" : "00:01:00"</span></span>
    
    <span data-ttu-id="ff847-153">Można mieszać i dopasowywać notacji jako użytkownik należy.</span><span class="sxs-lookup"><span data-stu-id="ff847-153">You can mix and match notations as you please.</span></span>
    
    <span data-ttu-id="ff847-154">Ponadto Start obsługuje makra specjalnego: {najlepszych}, który próbuje hello toodetermine pierwszej ramki "interesujące" hello zawartości Uwaga: (krok i zakres są ignorowane w przypadku rozpoczęcia ustawiono zbyt {najlepsze})</span><span class="sxs-lookup"><span data-stu-id="ff847-154">Additionally, Start also supports a special Macro:{Best}, which attempts toodetermine hello first “interesting” frame of hello content NOTE: (Step and Range are ignored when Start is set too{Best})</span></span>
  * <span data-ttu-id="ff847-155">Wartości domyślne: Start: {najlepsze}</span><span class="sxs-lookup"><span data-stu-id="ff847-155">Defaults: Start:{Best}</span></span>
* <span data-ttu-id="ff847-156">Format danych wyjściowych musi toobe jawnie podany dla każdego format obrazu: BmpFormat-Jpg/Png.</span><span class="sxs-lookup"><span data-stu-id="ff847-156">Output format needs toobe explicitly provided for each Image format: Jpg/Png/BmpFormat.</span></span> <span data-ttu-id="ff847-157">Jeśli jest obecny, rynkowej będzie odpowiadała JpgVideo tooJpgFormat i tak dalej.</span><span class="sxs-lookup"><span data-stu-id="ff847-157">When present, MES will match JpgVideo tooJpgFormat and so on.</span></span> <span data-ttu-id="ff847-158">OutputFormat wprowadza nowe określone makro koder-dekoder obrazów: {indeks}, która wymaga toobe obecne (jeden raz i tylko jeden raz) dla formatów wyjściowych obrazu.</span><span class="sxs-lookup"><span data-stu-id="ff847-158">OutputFormat introduces a new image-codec specific Macro: {Index}, which needs toobe present (once and only once) for image output formats.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ff847-159">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="ff847-159">Next steps</span></span>

<span data-ttu-id="ff847-160">Możesz sprawdzić hello [postępu zadania](media-services-check-job-progress.md) podczas hello oczekuje zadania kodowania.</span><span class="sxs-lookup"><span data-stu-id="ff847-160">You can check hello [job progress](media-services-check-job-progress.md) while hello encoding job is pending.</span></span>

## <a name="media-services-learning-paths"></a><span data-ttu-id="ff847-161">Ścieżki szkoleniowe dotyczące usługi Media Services</span><span class="sxs-lookup"><span data-stu-id="ff847-161">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="ff847-162">Przekazywanie opinii</span><span class="sxs-lookup"><span data-stu-id="ff847-162">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="see-also"></a><span data-ttu-id="ff847-163">Zobacz też</span><span class="sxs-lookup"><span data-stu-id="ff847-163">See Also</span></span>
[<span data-ttu-id="ff847-164">Usługi multimediów kodowania — omówienie</span><span class="sxs-lookup"><span data-stu-id="ff847-164">Media Services Encoding Overview</span></span>](media-services-encode-asset.md)

