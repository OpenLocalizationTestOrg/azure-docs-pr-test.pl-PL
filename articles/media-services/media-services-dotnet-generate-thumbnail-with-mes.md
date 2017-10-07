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
# <a name="how-toogenerate-thumbnails-using-media-encoder-standard-with-net"></a>Jak miniatur toogenerate przy użyciu standardu Media Encoder Standard z platformą .NET

Można użyć toogenerate Media Encoder Standard miniatur co najmniej jeden z wejściowego pliku wideo w [JPEG](https://en.wikipedia.org/wiki/JPEG), [PNG](https://en.wikipedia.org/wiki/Portable_Network_Graphics), lub [BMP](https://en.wikipedia.org/wiki/BMP_file_format) obrazów w formatach. Można przesłać zadania, które powodują powstanie tylko obrazy, lub można łączyć generowanie miniatur z kodowaniem. Ten temat zawiera kilka przykładowych XML i JSON miniatur ustawienia dla tych scenariuszy. Na końcu hello hello tematu, istnieje [przykładowy kod](#code_sample) który pokazuje, jak toouse hello .NET SDK usługi Media Services tooaccomplish hello kodowania zadań.

Więcej szczegółów na powitania elementów, które są używane w predefiniowane próbki, należy przejrzeć [Media Encoder Standard schematu](media-services-mes-schema.md).

Upewnij się, że hello tooreview [zagadnienia](media-services-dotnet-generate-thumbnail-with-mes.md#considerations) sekcji.

## <a name="example--single-png-file"></a>Przykład — pojedynczy plik PNG

Witaj następującego formatu JSON i XML ustawienie może być używane tooproduce pojedynczego wyjścia PNG pliku poza hello najpierw kilka sekund wejściowy plik wideo hello, gdzie kodera hello sprawia, że próba optymalnych Znajdowanie ramki "interesujące". Należy pamiętać, że wymiary obrazu wyjściowego hello ustawiono too100%, co oznacza, że odpowiadają one hello wymiary hello wejściowy plik wideo. Należy też zauważyć, jak ustawienie "Format" hello "Dane wyjściowe" jest wymagane użycie hello toomatch "PngLayers" w sekcji "Koderów-dekoderów" hello. 

### <a name="json-preset"></a>Ustawienie wstępne JSON

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
    
### <a name="xml-preset"></a>Ustawienie wstępne XML

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

## <a name="example--a-series-of-jpeg-images"></a>Przykład — szereg obrazy JPEG

Witaj następującego formatu JSON i XML ustawienie może być używane tooproduce zestaw 10 obrazów w sygnatury czasowe 5% 15%,..., 95% wejściowych osi czasu hello, których rozmiar obrazu hello jest określony toobe co kwartał, który hello wejściowych wideo.

### <a name="json-preset"></a>Ustawienie wstępne JSON

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

### <a name="xml-preset"></a>Ustawienie wstępne XML
    
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

## <a name="example--one-image-at-a-specific-timestamp"></a>Przykład — jeden obraz w określonej sygnatury czasowej

Hello następujące ustawienie wstępne JSON i XML może być używane tooproduce jeden obraz JPEG na powitania 30 sekund znak wejściowy plik wideo hello. To ustawienie wstępne oczekuje toobe wejściowych hello ponad 30 sekund czasu trwania (else zadania hello zakończy się niepowodzeniem).

### <a name="json-preset"></a>Ustawienie wstępne JSON

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
    
### <a name="xml-preset"></a>Ustawienie wstępne XML
    
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

## <a id="code_sample"></a>Przykład — kodowanie wideo i generowanie miniatur

Poniższy przykład kodu Hello używa hello tooperform .NET SDK usługi Media Services następujące zadania:

* Utwórz zadania kodowania.
* Pobiera koder Media Encoder Standard toohello odwołania.
* Ustawienia wstępnego ładowania hello [XML](media-services-dotnet-generate-thumbnail-with-mes.md#xml) lub [JSON](media-services-dotnet-generate-thumbnail-with-mes.md#json) zawierających hello kodowanie ustawienia wstępnego również miniatur toogenerate potrzebne informacje. Można go zapisać [XML](media-services-dotnet-generate-thumbnail-with-mes.md#xml) lub [JSON](media-services-dotnet-generate-thumbnail-with-mes.md#json) w pliku i użyj hello, następującego pliku hello tooload kodu.
  
        // Load hello XML (or JSON) from hello local file.
        string configuration = File.ReadAllText(fileName);  
* Dodaj jednego zadania kodowania toohello zadań. 
* Określ dane wejściowe hello zakodowane toobe zasobów.
* Tworzenie zasobu danych wyjściowych, który będzie zawierać hello zakodowane zasobów.
* Dodaj postęp zadania hello toocheck zdarzeń programu obsługi.
* Prześlij zadanie hello.

Zobacz hello [tworzenia usługi Media Services z platformą .NET](media-services-dotnet-how-to-use.md) tematu, aby uzyskać instrukcje na temat tooset Twojego środowiska deweloperów.

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

## <a id="json"></a>Ustawienie JSON miniatur
Aby uzyskać informacje o schemacie, zobacz [to](https://msdn.microsoft.com/library/mt269962.aspx) tematu.

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

## <a id="xml"></a>Ustawienie XML miniatur
Aby uzyskać informacje o schemacie, zobacz [to](https://msdn.microsoft.com/library/mt269962.aspx) tematu.
    
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

## <a name="considerations"></a>Zagadnienia do rozważenia
Zastosuj Hello następujące zagadnienia:

* Hello użycie jawnego znacznika czasu rozpoczęcia/krok/zakresu przyjęto założenie, że źródło danych wejściowych w tym hello jest co najmniej 1 minutę.
* Elementy BmpImage-jpg/Png mają Start, krok i zakres string atrybutów — mogą być interpretowane jako:
  
  * Numer ramki, jeśli są one — nieujemne liczby całkowite, np. "Start": "120"
  * Względna toosource czas trwania, jeśli wyrażony jako sufiks %, np. "Start": "15%", lub
  * Sygnatura czasowa Jeśli wyrażonej w postaci hh: mm:... Format. Np. "Start": "00: 01:00"
    
    Można mieszać i dopasowywać notacji jako użytkownik należy.
    
    Ponadto Start obsługuje makra specjalnego: {najlepszych}, który próbuje hello toodetermine pierwszej ramki "interesujące" hello zawartości Uwaga: (krok i zakres są ignorowane w przypadku rozpoczęcia ustawiono zbyt {najlepsze})
  * Wartości domyślne: Start: {najlepsze}
* Format danych wyjściowych musi toobe jawnie podany dla każdego format obrazu: BmpFormat-Jpg/Png. Jeśli jest obecny, rynkowej będzie odpowiadała JpgVideo tooJpgFormat i tak dalej. OutputFormat wprowadza nowe określone makro koder-dekoder obrazów: {indeks}, która wymaga toobe obecne (jeden raz i tylko jeden raz) dla formatów wyjściowych obrazu.

## <a name="next-steps"></a>Następne kroki

Możesz sprawdzić hello [postępu zadania](media-services-check-job-progress.md) podczas hello oczekuje zadania kodowania.

## <a name="media-services-learning-paths"></a>Ścieżki szkoleniowe dotyczące usługi Media Services
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Przekazywanie opinii
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="see-also"></a>Zobacz też
[Usługi multimediów kodowania — omówienie](media-services-encode-asset.md)

