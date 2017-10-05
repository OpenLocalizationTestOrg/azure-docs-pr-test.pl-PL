---
title: "Generowanie miniatur przy użyciu usługi Media Encoder Standard za pomocą platformy .NET"
description: "W tym temacie przedstawiono sposób .NET umożliwia kodowanie elementu zawartości oraz generowanie miniatur, w tym samym czasie przy użyciu standardu Media Encoder Standard."
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
ms.openlocfilehash: 89d15cbdf71a140e78f34e07ff208776b7d4cab3
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
# <a name="how-to-generate-thumbnails-using-media-encoder-standard-with-net"></a><span data-ttu-id="d7472-103">Generowanie miniatur przy użyciu usługi Media Encoder Standard za pomocą platformy .NET</span><span class="sxs-lookup"><span data-stu-id="d7472-103">How to generate thumbnails using Media Encoder Standard with .NET</span></span>

<span data-ttu-id="d7472-104">Umożliwia Media Encoder Standard generowanie miniatur co najmniej jeden z wejściowego pliku wideo w [JPEG](https://en.wikipedia.org/wiki/JPEG), [PNG](https://en.wikipedia.org/wiki/Portable_Network_Graphics), lub [BMP](https://en.wikipedia.org/wiki/BMP_file_format) obrazów w formatach.</span><span class="sxs-lookup"><span data-stu-id="d7472-104">You can use Media Encoder Standard to generate one or more thumbnails from your input video in [JPEG](https://en.wikipedia.org/wiki/JPEG), [PNG](https://en.wikipedia.org/wiki/Portable_Network_Graphics), or [BMP](https://en.wikipedia.org/wiki/BMP_file_format) image file formats.</span></span> <span data-ttu-id="d7472-105">Można przesłać zadania, które powodują powstanie tylko obrazy, lub można łączyć generowanie miniatur z kodowaniem.</span><span class="sxs-lookup"><span data-stu-id="d7472-105">You can submit Tasks that produce only images, or you can combine thumbnail generation with encoding.</span></span> <span data-ttu-id="d7472-106">Ten temat zawiera kilka przykładowych XML i JSON miniatur ustawienia dla tych scenariuszy.</span><span class="sxs-lookup"><span data-stu-id="d7472-106">This topic provides a few sample XML and JSON thumbnail presets for such scenarios.</span></span> <span data-ttu-id="d7472-107">Na końcu tego tematu jest [przykładowy kod](#code_sample) który przedstawia sposób użycia SDK .NET usługi Media Services do wykonania zadania kodowania.</span><span class="sxs-lookup"><span data-stu-id="d7472-107">At the end of the topic, there is a [sample code](#code_sample) that shows how to use the Media Services .NET SDK to accomplish the encoding task.</span></span>

<span data-ttu-id="d7472-108">Więcej szczegółów dla elementów, które są używane w predefiniowane próbki, należy przejrzeć [Media Encoder Standard schematu](media-services-mes-schema.md).</span><span class="sxs-lookup"><span data-stu-id="d7472-108">For more details on the elements that are used in sample presets, you should review [Media Encoder Standard schema](media-services-mes-schema.md).</span></span>

<span data-ttu-id="d7472-109">Upewnij się przejrzeć [zagadnienia](media-services-dotnet-generate-thumbnail-with-mes.md#considerations) sekcji.</span><span class="sxs-lookup"><span data-stu-id="d7472-109">Make sure to review the [Considerations](media-services-dotnet-generate-thumbnail-with-mes.md#considerations) section.</span></span>

## <a name="example--single-png-file"></a><span data-ttu-id="d7472-110">Przykład — pojedynczy plik PNG</span><span class="sxs-lookup"><span data-stu-id="d7472-110">Example – single PNG file</span></span>

<span data-ttu-id="d7472-111">Następujące ustawienia wstępnego JSON i XML może służyć do tworzenia pliku PNG pojedynczym wyjściowym poza pierwszym kilka sekund wejścia wideo, gdzie koder sprawia, że próba optymalnych Znajdowanie ramki "interesujące".</span><span class="sxs-lookup"><span data-stu-id="d7472-111">The following JSON and XML preset can be used to produce a single output PNG file out of the first few seconds of the input video, where the encoder makes a best-effort attempt at finding an “interesting” frame.</span></span> <span data-ttu-id="d7472-112">Należy pamiętać, że wymiary obrazu wyjściowego zostały ustawione na 100%, co oznacza te będą zgodne wymiary wejściowy plik wideo.</span><span class="sxs-lookup"><span data-stu-id="d7472-112">Note that the output image dimensions have been set to 100%, meaning these will match the dimensions of the input video.</span></span> <span data-ttu-id="d7472-113">Należy też zauważyć, jak ustawienie "Format" w "Dane wyjściowe" jest konieczne dopasowanie użycie "PngLayers" w sekcji "Koderów-dekoderów".</span><span class="sxs-lookup"><span data-stu-id="d7472-113">Note also how the “Format” setting in “Outputs” is required to match the use of “PngLayers” in the “Codecs” section.</span></span> 

### <a name="json-preset"></a><span data-ttu-id="d7472-114">Ustawienie wstępne JSON</span><span class="sxs-lookup"><span data-stu-id="d7472-114">JSON preset</span></span>

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
    
### <a name="xml-preset"></a><span data-ttu-id="d7472-115">Ustawienie wstępne XML</span><span class="sxs-lookup"><span data-stu-id="d7472-115">XML preset</span></span>

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

## <a name="example--a-series-of-jpeg-images"></a><span data-ttu-id="d7472-116">Przykład — szereg obrazy JPEG</span><span class="sxs-lookup"><span data-stu-id="d7472-116">Example – a series of JPEG images</span></span>

<span data-ttu-id="d7472-117">Następujące ustawienie JSON i XML można utworzyć zestaw 10 obrazów w sygnatury czasowe 5% 15%,..., 95% wejściowych osi czasu, gdy określono rozmiar obrazu jest jednym kwartału elementu wejściowego pliku wideo.</span><span class="sxs-lookup"><span data-stu-id="d7472-117">The following JSON and XML preset can be used to produce a set of 10 images at timestamps of 5%, 15%, …, 95% of the input timeline, where the image size is specified to be one quarter that of the input video.</span></span>

### <a name="json-preset"></a><span data-ttu-id="d7472-118">Ustawienie wstępne JSON</span><span class="sxs-lookup"><span data-stu-id="d7472-118">JSON preset</span></span>

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

### <a name="xml-preset"></a><span data-ttu-id="d7472-119">Ustawienie wstępne XML</span><span class="sxs-lookup"><span data-stu-id="d7472-119">XML preset</span></span>
    
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

## <a name="example--one-image-at-a-specific-timestamp"></a><span data-ttu-id="d7472-120">Przykład — jeden obraz w określonej sygnatury czasowej</span><span class="sxs-lookup"><span data-stu-id="d7472-120">Example – one image at a specific timestamp</span></span>

<span data-ttu-id="d7472-121">Następujące ustawienia wstępnego JSON i XML może służyć do tworzenia pojedynczego obrazu JPEG na 30 drugi znacznik wejściowy plik wideo.</span><span class="sxs-lookup"><span data-stu-id="d7472-121">The following JSON and XML preset can be used to produce a single JPEG image at the 30 second mark of the input video.</span></span> <span data-ttu-id="d7472-122">To ustawienie wstępne oczekuje danych wejściowych w postaci ponad 30 sekund czasu trwania (else zadanie nie powiedzie się).</span><span class="sxs-lookup"><span data-stu-id="d7472-122">This preset expects the input to be more than 30 seconds in duration (else the job will fail).</span></span>

### <a name="json-preset"></a><span data-ttu-id="d7472-123">Ustawienie wstępne JSON</span><span class="sxs-lookup"><span data-stu-id="d7472-123">JSON preset</span></span>

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
    
### <a name="xml-preset"></a><span data-ttu-id="d7472-124">Ustawienie wstępne XML</span><span class="sxs-lookup"><span data-stu-id="d7472-124">XML preset</span></span>
    
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

## <span data-ttu-id="d7472-125"><a id="code_sample"></a>Przykład — kodowanie wideo i generowanie miniatur</span><span class="sxs-lookup"><span data-stu-id="d7472-125"><a id="code_sample"></a>Example – encode video and generate thumbnail</span></span>

<span data-ttu-id="d7472-126">Poniższy przykład kodu wykorzystuje .NET SDK usługi Media Services do wykonywania następujących zadań:</span><span class="sxs-lookup"><span data-stu-id="d7472-126">The following code example uses Media Services .NET SDK to perform the following tasks:</span></span>

* <span data-ttu-id="d7472-127">Utwórz zadania kodowania.</span><span class="sxs-lookup"><span data-stu-id="d7472-127">Create an encoding job.</span></span>
* <span data-ttu-id="d7472-128">Pobierz odwołanie do kodera Media Encoder Standard.</span><span class="sxs-lookup"><span data-stu-id="d7472-128">Get a reference to the Media Encoder Standard encoder.</span></span>
* <span data-ttu-id="d7472-129">Ładowanie ustawień [XML](media-services-dotnet-generate-thumbnail-with-mes.md#xml) lub [JSON](media-services-dotnet-generate-thumbnail-with-mes.md#json) zawierających ustawienia oraz informacje potrzebne do generowania miniatur kodowania.</span><span class="sxs-lookup"><span data-stu-id="d7472-129">Load the preset [XML](media-services-dotnet-generate-thumbnail-with-mes.md#xml) or [JSON](media-services-dotnet-generate-thumbnail-with-mes.md#json) that contain the encoding preset as well as information needed to generate thumbnails.</span></span> <span data-ttu-id="d7472-130">Można go zapisać [XML](media-services-dotnet-generate-thumbnail-with-mes.md#xml) lub [JSON](media-services-dotnet-generate-thumbnail-with-mes.md#json) w pliku i użyj poniższy kod do załadowania pliku.</span><span class="sxs-lookup"><span data-stu-id="d7472-130">You can save this  [XML](media-services-dotnet-generate-thumbnail-with-mes.md#xml) or [JSON](media-services-dotnet-generate-thumbnail-with-mes.md#json) in a file and use the following code to load the file.</span></span>
  
        // Load the XML (or JSON) from the local file.
        string configuration = File.ReadAllText(fileName);  
* <span data-ttu-id="d7472-131">Dodaj pojedynczego zadania kodowania do zadania.</span><span class="sxs-lookup"><span data-stu-id="d7472-131">Add a single encoding task to the job.</span></span> 
* <span data-ttu-id="d7472-132">Określ wejściowych zasobów do zakodowania.</span><span class="sxs-lookup"><span data-stu-id="d7472-132">Specify the input asset to be encoded.</span></span>
* <span data-ttu-id="d7472-133">Utwórz zasób danych wyjściowych, który będzie zawierać zakodowanym elementem zawartości.</span><span class="sxs-lookup"><span data-stu-id="d7472-133">Create an output asset that will contain the encoded asset.</span></span>
* <span data-ttu-id="d7472-134">Dodaj program obsługi zdarzeń, aby sprawdzić postęp zadania.</span><span class="sxs-lookup"><span data-stu-id="d7472-134">Add an event handler to check the job progress.</span></span>
* <span data-ttu-id="d7472-135">Przesłać zadanie.</span><span class="sxs-lookup"><span data-stu-id="d7472-135">Submit the job.</span></span>

<span data-ttu-id="d7472-136">Zobacz [tworzenia usługi Media Services z platformą .NET](media-services-dotnet-how-to-use.md) tematu dla wskazówki dotyczące sposobu konfigurowania środowiska deweloperów.</span><span class="sxs-lookup"><span data-stu-id="d7472-136">See the [Media Services development with .NET](media-services-dotnet-how-to-use.md) topic for directions on how to set up your dev environment.</span></span>

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
            // Read values from the App.config file.
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

            // Encode and generate the thumbnails.
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

            // Load the XML (or JSON) from the local file.
            string configuration = File.ReadAllText("ThumbnailPreset_JSON.json");

            // Create a task
            ITask task = job.Tasks.AddNew("Media Encoder Standard encoding task",
                processor,
                configuration,
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

## <span data-ttu-id="d7472-137"><a id="json"></a>Ustawienie JSON miniatur</span><span class="sxs-lookup"><span data-stu-id="d7472-137"><a id="json"></a>Thumbnail JSON preset</span></span>
<span data-ttu-id="d7472-138">Aby uzyskać informacje o schemacie, zobacz [to](https://msdn.microsoft.com/library/mt269962.aspx) tematu.</span><span class="sxs-lookup"><span data-stu-id="d7472-138">For information about schema, see [this](https://msdn.microsoft.com/library/mt269962.aspx) topic.</span></span>

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

## <span data-ttu-id="d7472-139"><a id="xml"></a>Ustawienie XML miniatur</span><span class="sxs-lookup"><span data-stu-id="d7472-139"><a id="xml"></a>Thumbnail XML preset</span></span>
<span data-ttu-id="d7472-140">Aby uzyskać informacje o schemacie, zobacz [to](https://msdn.microsoft.com/library/mt269962.aspx) tematu.</span><span class="sxs-lookup"><span data-stu-id="d7472-140">For information about schema, see [this](https://msdn.microsoft.com/library/mt269962.aspx) topic.</span></span>
    
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

## <a name="considerations"></a><span data-ttu-id="d7472-141">Zagadnienia do rozważenia</span><span class="sxs-lookup"><span data-stu-id="d7472-141">Considerations</span></span>
<span data-ttu-id="d7472-142">Następujące kwestie:</span><span class="sxs-lookup"><span data-stu-id="d7472-142">The following considerations apply:</span></span>

* <span data-ttu-id="d7472-143">Użycie jawnego sygnatury czasowe początku/krok/zakresu zakłada, że źródło danych wejściowych jest co najmniej 1 minutę.</span><span class="sxs-lookup"><span data-stu-id="d7472-143">The use of explicit timestamps for Start/Step/Range assumes that the input source is at least 1 minute long.</span></span>
* <span data-ttu-id="d7472-144">Elementy BmpImage-jpg/Png mają Start, krok i zakres string atrybutów — mogą być interpretowane jako:</span><span class="sxs-lookup"><span data-stu-id="d7472-144">Jpg/Png/BmpImage elements have Start, Step and Range string attributes – these can be interpreted as:</span></span>
  
  * <span data-ttu-id="d7472-145">Numer ramki, jeśli są one — nieujemne liczby całkowite, np.</span><span class="sxs-lookup"><span data-stu-id="d7472-145">Frame Number if they are non-negative integers, eg.</span></span> <span data-ttu-id="d7472-146">"Start": "120"</span><span class="sxs-lookup"><span data-stu-id="d7472-146">"Start": "120",</span></span>
  * <span data-ttu-id="d7472-147">Względem źródła czas trwania, jeśli wyrażony jako sufiks %, np.</span><span class="sxs-lookup"><span data-stu-id="d7472-147">Relative to source duration if expressed as %-suffixed, eg.</span></span> <span data-ttu-id="d7472-148">"Start": "15%", lub</span><span class="sxs-lookup"><span data-stu-id="d7472-148">"Start": "15%", OR</span></span>
  * <span data-ttu-id="d7472-149">Sygnatura czasowa Jeśli wyrażonej w postaci hh: mm:...</span><span class="sxs-lookup"><span data-stu-id="d7472-149">Timestamp if expressed as HH:MM:SS…</span></span> <span data-ttu-id="d7472-150">Format.</span><span class="sxs-lookup"><span data-stu-id="d7472-150">format.</span></span> <span data-ttu-id="d7472-151">Np.</span><span class="sxs-lookup"><span data-stu-id="d7472-151">Eg.</span></span> <span data-ttu-id="d7472-152">"Start": "00: 01:00"</span><span class="sxs-lookup"><span data-stu-id="d7472-152">"Start" : "00:01:00"</span></span>
    
    <span data-ttu-id="d7472-153">Można mieszać i dopasowywać notacji jako użytkownik należy.</span><span class="sxs-lookup"><span data-stu-id="d7472-153">You can mix and match notations as you please.</span></span>
    
    <span data-ttu-id="d7472-154">Ponadto Start obsługuje makra specjalnego: {najlepszych}, który próbuje określić pierwszej ramki "interesujące" notatki zawartości: (krok i zakres są ignorowane, gdy Start ma ustawioną wartość {najlepiej})</span><span class="sxs-lookup"><span data-stu-id="d7472-154">Additionally, Start also supports a special Macro:{Best}, which attempts to determine the first “interesting” frame of the content NOTE: (Step and Range are ignored when Start is set to {Best})</span></span>
  * <span data-ttu-id="d7472-155">Wartości domyślne: Start: {najlepsze}</span><span class="sxs-lookup"><span data-stu-id="d7472-155">Defaults: Start:{Best}</span></span>
* <span data-ttu-id="d7472-156">Format danych wyjściowych muszą zostać jawnie dostarczone dla każdego formatu obrazu: BmpFormat-Jpg/Png.</span><span class="sxs-lookup"><span data-stu-id="d7472-156">Output format needs to be explicitly provided for each Image format: Jpg/Png/BmpFormat.</span></span> <span data-ttu-id="d7472-157">Jeśli jest obecny, rynkowej będzie odpowiadała JpgVideo do JpgFormat i tak dalej.</span><span class="sxs-lookup"><span data-stu-id="d7472-157">When present, MES will match JpgVideo to JpgFormat and so on.</span></span> <span data-ttu-id="d7472-158">OutputFormat wprowadza nowe określone makro koder-dekoder obrazów: {indeks}, która musi być zawierają (jeden raz i tylko jeden raz) formatów wyjściowych obrazu.</span><span class="sxs-lookup"><span data-stu-id="d7472-158">OutputFormat introduces a new image-codec specific Macro: {Index}, which needs to be present (once and only once) for image output formats.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d7472-159">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="d7472-159">Next steps</span></span>

<span data-ttu-id="d7472-160">Możesz sprawdzić [postępu zadania](media-services-check-job-progress.md) podczas oczekujące zadania kodowania.</span><span class="sxs-lookup"><span data-stu-id="d7472-160">You can check the [job progress](media-services-check-job-progress.md) while the encoding job is pending.</span></span>

## <a name="media-services-learning-paths"></a><span data-ttu-id="d7472-161">Ścieżki szkoleniowe dotyczące usługi Media Services</span><span class="sxs-lookup"><span data-stu-id="d7472-161">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="d7472-162">Przekazywanie opinii</span><span class="sxs-lookup"><span data-stu-id="d7472-162">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="see-also"></a><span data-ttu-id="d7472-163">Zobacz też</span><span class="sxs-lookup"><span data-stu-id="d7472-163">See Also</span></span>
[<span data-ttu-id="d7472-164">Usługi multimediów kodowania — omówienie</span><span class="sxs-lookup"><span data-stu-id="d7472-164">Media Services Encoding Overview</span></span>](media-services-encode-asset.md)

