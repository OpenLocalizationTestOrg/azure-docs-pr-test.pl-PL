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
# <a name="how-to-generate-thumbnails-using-media-encoder-standard-with-net"></a>Generowanie miniatur przy użyciu usługi Media Encoder Standard za pomocą platformy .NET

Umożliwia Media Encoder Standard generowanie miniatur co najmniej jeden z wejściowego pliku wideo w [JPEG](https://en.wikipedia.org/wiki/JPEG), [PNG](https://en.wikipedia.org/wiki/Portable_Network_Graphics), lub [BMP](https://en.wikipedia.org/wiki/BMP_file_format) obrazów w formatach. Można przesłać zadania, które powodują powstanie tylko obrazy, lub można łączyć generowanie miniatur z kodowaniem. Ten temat zawiera kilka przykładowych XML i JSON miniatur ustawienia dla tych scenariuszy. Na końcu tego tematu jest [przykładowy kod](#code_sample) który przedstawia sposób użycia SDK .NET usługi Media Services do wykonania zadania kodowania.

Więcej szczegółów dla elementów, które są używane w predefiniowane próbki, należy przejrzeć [Media Encoder Standard schematu](media-services-mes-schema.md).

Upewnij się przejrzeć [zagadnienia](media-services-dotnet-generate-thumbnail-with-mes.md#considerations) sekcji.

## <a name="example--single-png-file"></a>Przykład — pojedynczy plik PNG

Następujące ustawienia wstępnego JSON i XML może służyć do tworzenia pliku PNG pojedynczym wyjściowym poza pierwszym kilka sekund wejścia wideo, gdzie koder sprawia, że próba optymalnych Znajdowanie ramki "interesujące". Należy pamiętać, że wymiary obrazu wyjściowego zostały ustawione na 100%, co oznacza te będą zgodne wymiary wejściowy plik wideo. Należy też zauważyć, jak ustawienie "Format" w "Dane wyjściowe" jest konieczne dopasowanie użycie "PngLayers" w sekcji "Koderów-dekoderów". 

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

Następujące ustawienie JSON i XML można utworzyć zestaw 10 obrazów w sygnatury czasowe 5% 15%,..., 95% wejściowych osi czasu, gdy określono rozmiar obrazu jest jednym kwartału elementu wejściowego pliku wideo.

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

Następujące ustawienia wstępnego JSON i XML może służyć do tworzenia pojedynczego obrazu JPEG na 30 drugi znacznik wejściowy plik wideo. To ustawienie wstępne oczekuje danych wejściowych w postaci ponad 30 sekund czasu trwania (else zadanie nie powiedzie się).

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

Poniższy przykład kodu wykorzystuje .NET SDK usługi Media Services do wykonywania następujących zadań:

* Utwórz zadania kodowania.
* Pobierz odwołanie do kodera Media Encoder Standard.
* Ładowanie ustawień [XML](media-services-dotnet-generate-thumbnail-with-mes.md#xml) lub [JSON](media-services-dotnet-generate-thumbnail-with-mes.md#json) zawierających ustawienia oraz informacje potrzebne do generowania miniatur kodowania. Można go zapisać [XML](media-services-dotnet-generate-thumbnail-with-mes.md#xml) lub [JSON](media-services-dotnet-generate-thumbnail-with-mes.md#json) w pliku i użyj poniższy kod do załadowania pliku.
  
        // Load the XML (or JSON) from the local file.
        string configuration = File.ReadAllText(fileName);  
* Dodaj pojedynczego zadania kodowania do zadania. 
* Określ wejściowych zasobów do zakodowania.
* Utwórz zasób danych wyjściowych, który będzie zawierać zakodowanym elementem zawartości.
* Dodaj program obsługi zdarzeń, aby sprawdzić postęp zadania.
* Przesłać zadanie.

Zobacz [tworzenia usługi Media Services z platformą .NET](media-services-dotnet-how-to-use.md) tematu dla wskazówki dotyczące sposobu konfigurowania środowiska deweloperów.

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
Następujące kwestie:

* Użycie jawnego sygnatury czasowe początku/krok/zakresu zakłada, że źródło danych wejściowych jest co najmniej 1 minutę.
* Elementy BmpImage-jpg/Png mają Start, krok i zakres string atrybutów — mogą być interpretowane jako:
  
  * Numer ramki, jeśli są one — nieujemne liczby całkowite, np. "Start": "120"
  * Względem źródła czas trwania, jeśli wyrażony jako sufiks %, np. "Start": "15%", lub
  * Sygnatura czasowa Jeśli wyrażonej w postaci hh: mm:... Format. Np. "Start": "00: 01:00"
    
    Można mieszać i dopasowywać notacji jako użytkownik należy.
    
    Ponadto Start obsługuje makra specjalnego: {najlepszych}, który próbuje określić pierwszej ramki "interesujące" notatki zawartości: (krok i zakres są ignorowane, gdy Start ma ustawioną wartość {najlepiej})
  * Wartości domyślne: Start: {najlepsze}
* Format danych wyjściowych muszą zostać jawnie dostarczone dla każdego formatu obrazu: BmpFormat-Jpg/Png. Jeśli jest obecny, rynkowej będzie odpowiadała JpgVideo do JpgFormat i tak dalej. OutputFormat wprowadza nowe określone makro koder-dekoder obrazów: {indeks}, która musi być zawierają (jeden raz i tylko jeden raz) formatów wyjściowych obrazu.

## <a name="next-steps"></a>Następne kroki

Możesz sprawdzić [postępu zadania](media-services-check-job-progress.md) podczas oczekujące zadania kodowania.

## <a name="media-services-learning-paths"></a>Ścieżki szkoleniowe dotyczące usługi Media Services
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Przekazywanie opinii
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="see-also"></a>Zobacz też
[Usługi multimediów kodowania — omówienie](media-services-encode-asset.md)

