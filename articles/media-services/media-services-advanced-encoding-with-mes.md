---
title: "Zaawansowane aaaPerform kodowanie dostosowując ustawienia rynkowej | Dokumentacja firmy Microsoft"
description: "W tym temacie przedstawiono sposób tooperform Zaawansowane kodowanie dostosowując Media Encoder Standard ustawienia zadania."
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: 2a4ade25-e600-4bce-a66e-e29cf4a38369
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/01/2017
ms.author: juliako
ms.openlocfilehash: 9caa68fafacaf51f91f0554c5bafe491928d8c77
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="perform-advanced-encoding-by-customizing-mes-presets"></a>Kodowanie zaawansowane dostosowując rynkowej ustawienia 

## <a name="overview"></a>Omówienie

W tym temacie przedstawiono, jak ustawienia toocustomize Media Encoder Standard. Witaj [kodowanie przy użyciu predefiniowanych Media Encoder Standard](media-services-custom-mes-presets-with-dotnet.md) temacie pokazano, jak toocreate .NET toouse kodowania zadań i zadań, która wykonuje to zadanie. Po dostosowaniu ustawienia domyślne, podaj hello predefiniowanych toohello kodowania zadań. 

>[!NOTE]
>Jeśli za pomocą wstępnie ustawionych XML, upewnij się, że toopreserve hello kolejność elementów, jak pokazano poniżej pokazano XML (na przykład KeyFrameInterval należy poprzedzać SceneChangeDetection).
>

W tym temacie przedstawiono hello predefiniowanych wykonujących hello następujące zadania kodowania.

## <a name="support-for-relative-sizes"></a>Obsługa względnych rozmiarów

Podczas generowania miniatur, nie trzeba tooalways Określ dane wyjściowe szerokość i wysokość w pikselach. Możesz określić je w procentach, w zakresie hello [1%,..., 100%].

### <a name="json-preset"></a>Ustawienie wstępne JSON
    "Width": "100%",
    "Height": "100%"

### <a name="xml-preset"></a>Ustawienie wstępne XML
    <Width>100%</Width>
    <Height>100%</Height>

## <a id="thumbnails"></a>Generowanie miniatur

W tej sekcji przedstawiono sposób toocustomize ustawienie wstępne, które generuje miniatur. Hello ustawienie wstępne określonych poniżej zawiera informacje dotyczące sposobu tooencode pliku również miniatur toogenerate potrzebne informacje. Może mieć jedną z ustawienia rynkowej hello udokumentowane [to](media-services-mes-presets-overview.md) sekcji, a następnie dodaj kod, który generuje miniatur.  

> [!NOTE]
> Witaj **SceneChangeDetection** ustawienie w hello następujące wstępnie zdefiniowane można ustawić tylko tootrue jeśli są kodowanie wideo o pojedynczej szybkości transmisji bitów tooa. Jeśli są kodowanie tooa wielokrotnej szybkości transmisji bitów wideo i ustaw **SceneChangeDetection** tootrue, koder hello zwraca błąd.  
>
>

Aby uzyskać informacje o schemacie, zobacz [to](media-services-mes-schema.md) tematu.

Upewnij się, że hello tooreview [zagadnienia](#considerations) sekcji.

### <a id="json"></a>Ustawienie wstępne JSON
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
              "Width": 640,
              "Height": 360
            }
          ],
          "Start": "{Best}",
          "Type": "JpgImage"
        },
        {
          "PngLayers": [
            {
              "Type": "PngLayer",
              "Width": 640,
              "Height": 360,
            }
          ],
          "Start": "00:00:01",
          "Step": "00:00:10",
          "Range": "00:00:58",
          "Type": "PngImage"
        },
        {
          "BmpLayers": [
            {
              "Type": "BmpLayer",
              "Width": 640,
              "Height": 360
            }
          ],
          "Start": "10%",
          "Step": "10%",
          "Range": "90%",
          "Type": "BmpImage"
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
          "FileName": "{Basename}_{Index}{Extension}",
          "Format": {
            "Type": "PngFormat"
          }
        },
        {
          "FileName": "{Basename}_{Index}{Extension}",
          "Format": {
            "Type": "BmpFormat"
          }
        },
        {
          "FileName": "{Basename}_{Width}x{Height}_{VideoBitrate}.mp4",
          "Format": {
            "Type": "MP4Format"
          }
        }
      ]
    }


### <a id="xml"></a>Ustawienie wstępne XML
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
              <Width>640</Width>
              <Height>360</Height>
              <Quality>90</Quality>
            </JpgLayer>
          </JpgLayers>
        </JpgImage>
        <BmpImage Start="10%" Step="10%" Range="90%">
          <BmpLayers>
            <BmpLayer>
              <Width>640</Width>
              <Height>360</Height>
            </BmpLayer>
          </BmpLayers>
        </BmpImage>
        <PngImage Start="00:00:01" Step="00:00:10" Range="00:00:58">
          <PngLayers>
            <PngLayer>
              <Width>640</Width>
              <Height>360</Height>
            </PngLayer>
          </PngLayers>
        </PngImage>
      </Encoding>
      <Outputs>
        <Output FileName="{Basename}_{Width}x{Height}_{VideoBitrate}.mp4">
          <MP4Format />
        </Output>
        <Output FileName="{Basename}_{Index}{Extension}">
          <JpgFormat />
        </Output>
        <Output FileName="{Basename}_{Index}{Extension}">
          <BmpFormat />
        </Output>
        <Output FileName="{Basename}_{Index}{Extension}">
          <PngFormat />
        </Output>
      </Outputs>
    </Preset>

### <a name="considerations"></a>Zagadnienia do rozważenia

Zastosuj Hello następujące zagadnienia:

* Hello użycie jawnego znacznika czasu rozpoczęcia/krok/zakresu przyjęto założenie, że źródło danych wejściowych w tym hello jest co najmniej 1 minutę.
* Elementy BmpImage-jpg/Png mają Start, krok i należeć do zakresu atrybutów ciąg — mogą być interpretowane jako:

  * Numer ramki, jeśli są one — nieujemne liczby całkowite, na przykład "Start": "120"
  * Względną toosource czas trwania, jeśli wyrażony jako sufiks %, na przykład "Start": "15%", lub
  * Sygnatura czasowa Jeśli wyrażonej w postaci hh: mm:... Format, na przykład "Start": "00: 01:00"

    Można mieszać i dopasowywać notacji jako użytkownik należy.

    Ponadto Start obsługuje makra specjalnego: {najlepszych}, który próbuje hello toodetermine pierwszej ramki "interesujące" hello zawartości Uwaga: (krok i zakres są ignorowane w przypadku rozpoczęcia ustawiono zbyt {najlepsze})
  * Wartości domyślne: Start: {najlepsze}
* Format danych wyjściowych musi toobe jawnie podany dla każdego format obrazu: BmpFormat-Jpg/Png. Jeśli jest obecny, rynkowej odpowiada JpgVideo tooJpgFormat i tak dalej. OutputFormat wprowadza nowe określone makro koder-dekoder obrazów: {indeks}, która wymaga toobe obecne (jeden raz i tylko jeden raz) dla formatów wyjściowych obrazu.

## <a id="trim_video"></a>Przycinanie wideo (wycinka)
Tej sekcji rozmów o modyfikowaniu kodera hello ustawienia tooclip lub trim wejściowy plik wideo hello gdzie wejściowy hello jest tak zwane mezzanine pliku lub plików na żądanie. Witaj kodera można również tooclip używane lub trim zasób, przechwycone lub zarchiwizowane strumienia na żywo — hello tego są one dostępne w [ten blog](https://azure.microsoft.com/blog/sub-clipping-and-live-archive-extraction-with-media-encoder-standard/).

tootrim pliki wideo, można wykonać dowolne ustawienia rynkowej hello udokumentowane [to](media-services-mes-presets-overview.md) sekcji i zmodyfikuj hello **źródeł** elementu (jak pokazano poniżej). wartość StartTime Hello musi toomatch hello bezwzględną znacznikami czasu hello wejściowy plik wideo. Na przykład, jeśli hello pierwszej ramki hello wejściowy plik wideo ma sygnaturę 12:00:10.000, a następnie wartość StartTime powinna być co najmniej 12:00:10.000 lub nowszej. W poniższym przykładzie hello przyjęto założenie, że hello wejściowego pliku wideo ma sygnaturę czasową początkowego o wartości zero. **Źródeł** należy umieścić na początku hello hello ustawienie wstępne.

### <a id="json"></a>Ustawienie wstępne JSON
    {
      "Version": 1.0,
      "Sources": [
        {
          "StartTime": "00:00:04",
          "Duration": "00:00:16"
        }
      ],
      "Codecs": [
        {
          "KeyFrameInterval": "00:00:02",
          "StretchMode": "AutoSize",
          "H264Layers": [
            {
              "Profile": "Auto",
              "Level": "auto",
              "Bitrate": 3400,
              "MaxBitrate": 3400,
              "BufferWindow": "00:00:05",
              "Width": 1280,
              "Height": 720,
              "BFrames": 3,
              "ReferenceFrames": 3,
              "AdaptiveBFrame": true,
              "Type": "H264Layer",
              "FrameRate": "0/1"
            },
            {
              "Profile": "Auto",
              "Level": "auto",
              "Bitrate": 2250,
              "MaxBitrate": 2250,
              "BufferWindow": "00:00:05",
              "Width": 960,
              "Height": 540,
              "BFrames": 3,
              "ReferenceFrames": 3,
              "AdaptiveBFrame": true,
              "Type": "H264Layer",
              "FrameRate": "0/1"
            },
            {
              "Profile": "Auto",
              "Level": "auto",
              "Bitrate": 1500,
              "MaxBitrate": 1500,
              "BufferWindow": "00:00:05",
              "Width": 960,
              "Height": 540,
              "BFrames": 3,
              "ReferenceFrames": 3,
              "AdaptiveBFrame": true,
              "Type": "H264Layer",
              "FrameRate": "0/1"
            },
            {
              "Profile": "Auto",
              "Level": "auto",
              "Bitrate": 1000,
              "MaxBitrate": 1000,
              "BufferWindow": "00:00:05",
              "Width": 640,
              "Height": 360,
              "BFrames": 3,
              "ReferenceFrames": 3,
              "AdaptiveBFrame": true,
              "Type": "H264Layer",
              "FrameRate": "0/1"
            },
            {
              "Profile": "Auto",
              "Level": "auto",
              "Bitrate": 650,
              "MaxBitrate": 650,
              "BufferWindow": "00:00:05",
              "Width": 640,
              "Height": 360,
              "BFrames": 3,
              "ReferenceFrames": 3,
              "AdaptiveBFrame": true,
              "Type": "H264Layer",
              "FrameRate": "0/1"
            },
            {
              "Profile": "Auto",
              "Level": "auto",
              "Bitrate": 400,
              "MaxBitrate": 400,
              "BufferWindow": "00:00:05",
              "Width": 320,
              "Height": 180,
              "BFrames": 3,
              "ReferenceFrames": 3,
              "AdaptiveBFrame": true,
              "Type": "H264Layer",
              "FrameRate": "0/1"
            }
          ],
          "Type": "H264Video"
        },
        {
          "Profile": "AACLC",
          "Channels": 2,
          "SamplingRate": 48000,
          "Bitrate": 128,
          "Type": "AACAudio"
        }
      ],
      "Outputs": [
        {
          "FileName": "{Basename}_{Width}x{Height}_{VideoBitrate}.mp4",
          "Format": {
            "Type": "MP4Format"
          }
        }
      ]
    }

### <a name="xml-preset"></a>Ustawienie wstępne XML
tootrim pliki wideo, można wykonać dowolne ustawienia rynkowej hello udokumentowane [tutaj](media-services-mes-presets-overview.md) i zmodyfikuj hello **źródeł** elementu (jak pokazano poniżej).

    <?xml version="1.0" encoding="utf-16"?>
    <Preset xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" Version="1.0" xmlns="http://www.windowsazure.com/media/encoding/Preset/2014/03">
      <Sources>
        <Source StartTime="PT4S" Duration="PT14S"/>
      </Sources>
      <Encoding>
        <H264Video>
          <KeyFrameInterval>00:00:02</KeyFrameInterval>
          <H264Layers>
            <H264Layer>
              <Bitrate>3400</Bitrate>
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
              <MaxBitrate>3400</MaxBitrate>
            </H264Layer>
            <H264Layer>
              <Bitrate>2250</Bitrate>
              <Width>960</Width>
              <Height>540</Height>
              <FrameRate>0/1</FrameRate>
              <Profile>Auto</Profile>
              <Level>auto</Level>
              <BFrames>3</BFrames>
              <ReferenceFrames>3</ReferenceFrames>
              <Slices>0</Slices>
              <AdaptiveBFrame>true</AdaptiveBFrame>
              <EntropyMode>Cabac</EntropyMode>
              <BufferWindow>00:00:05</BufferWindow>
              <MaxBitrate>2250</MaxBitrate>
            </H264Layer>
            <H264Layer>
              <Bitrate>1500</Bitrate>
              <Width>960</Width>
              <Height>540</Height>
              <FrameRate>0/1</FrameRate>
              <Profile>Auto</Profile>
              <Level>auto</Level>
              <BFrames>3</BFrames>
              <ReferenceFrames>3</ReferenceFrames>
              <Slices>0</Slices>
              <AdaptiveBFrame>true</AdaptiveBFrame>
              <EntropyMode>Cabac</EntropyMode>
              <BufferWindow>00:00:05</BufferWindow>
              <MaxBitrate>1500</MaxBitrate>
            </H264Layer>
            <H264Layer>
              <Bitrate>1000</Bitrate>
              <Width>640</Width>
              <Height>360</Height>
              <FrameRate>0/1</FrameRate>
              <Profile>Auto</Profile>
              <Level>auto</Level>
              <BFrames>3</BFrames>
              <ReferenceFrames>3</ReferenceFrames>
              <Slices>0</Slices>
              <AdaptiveBFrame>true</AdaptiveBFrame>
              <EntropyMode>Cabac</EntropyMode>
              <BufferWindow>00:00:05</BufferWindow>
              <MaxBitrate>1000</MaxBitrate>
            </H264Layer>
            <H264Layer>
              <Bitrate>650</Bitrate>
              <Width>640</Width>
              <Height>360</Height>
              <FrameRate>0/1</FrameRate>
              <Profile>Auto</Profile>
              <Level>auto</Level>
              <BFrames>3</BFrames>
              <ReferenceFrames>3</ReferenceFrames>
              <Slices>0</Slices>
              <AdaptiveBFrame>true</AdaptiveBFrame>
              <EntropyMode>Cabac</EntropyMode>
              <BufferWindow>00:00:05</BufferWindow>
              <MaxBitrate>650</MaxBitrate>
            </H264Layer>
            <H264Layer>
              <Bitrate>400</Bitrate>
              <Width>320</Width>
              <Height>180</Height>
              <FrameRate>0/1</FrameRate>
              <Profile>Auto</Profile>
              <Level>auto</Level>
              <BFrames>3</BFrames>
              <ReferenceFrames>3</ReferenceFrames>
              <Slices>0</Slices>
              <AdaptiveBFrame>true</AdaptiveBFrame>
              <EntropyMode>Cabac</EntropyMode>
              <BufferWindow>00:00:05</BufferWindow>
              <MaxBitrate>400</MaxBitrate>
            </H264Layer>
          </H264Layers>
        </H264Video>
        <AACAudio>
          <Profile>AACLC</Profile>
          <Channels>2</Channels>
          <SamplingRate>48000</SamplingRate>
          <Bitrate>128</Bitrate>
        </AACAudio>
      </Encoding>
      <Outputs>
        <Output FileName="{Basename}_{Width}x{Height}_{VideoBitrate}.mp4">
          <MP4Format />
        </Output>
      </Outputs>
    </Preset>

## <a id="overlay"></a>Utwórz nakładki

Witaj Media Encoder Standard umożliwia toooverlay obrazu na istniejące wideo. Obecnie są obsługiwane następujące formaty hello: png, jpg, gif, bmp, a. Witaj ustawienie wstępne określonych poniżej jest podstawowy przykład nakładka wideo.

Ponadto toodefining istniejących plików, masz również toolet Media Services wiedzieć, plik, który w zasobów hello jest hello nakładki obrazów i plik, który jest hello źródła wideo, na który chcesz toooverlay hello obrazu. Witaj plik wideo ma toobe hello **głównej** pliku.

Jeśli używasz platformy .NET, Dodaj hello następujące dwie funkcje przykład .NET toohello zdefiniowane w [to](media-services-custom-mes-presets-with-dotnet.md#encoding_with_dotnet) tematu. Witaj **UploadMediaFilesFromFolder** funkcja przekazywania plików z folderu (na przykład BigBuckBunny.mp4 i Image001.png) i zestawy hello mp4 toobe hello podstawowy plik w hello zasobów. Witaj **EncodeWithOverlay** funkcja używa hello niestandardowych predefiniowanych plik, który został przekazany tooit (na przykład hello ustawień tego następujące) toocreate hello zadania kodowania.


    static public IAsset UploadMediaFilesFromFolder(string folderPath)
    {
        IAsset asset = _context.Assets.CreateFromFolder(folderPath, AssetCreationOptions.None);
    
        foreach (var af in asset.AssetFiles)
        {
            // hello following code assumes 
            // you have an input folder with one MP4 and one overlay image file.
            if (af.Name.Contains(".mp4"))
                af.IsPrimary = true;
            else
                af.IsPrimary = false;
    
            af.Update();
        }
    
        return asset;
    }

    static public IAsset EncodeWithOverlay(IAsset assetSource, string customPresetFileName)
    {
        // Declare a new job.
        IJob job = _context.Jobs.Create("Media Encoder Standard Job");
        // Get a media processor reference, and pass tooit hello name of hello 
        // processor toouse for hello specific task.
        IMediaProcessor processor = GetLatestMediaProcessorByName("Media Encoder Standard");

        // Load hello XML (or JSON) from hello local file.
        string configuration = File.ReadAllText(customPresetFileName);

        // Create a task
        ITask task = job.Tasks.AddNew("Media Encoder Standard encoding task",
            processor,
            configuration,
            TaskOptions.None);

        // Specify hello input assets toobe encoded.
        // This asset contains a source file and an overlay file.
        task.InputAssets.Add(assetSource);

        // Add an output asset toocontain hello results of hello job. 
        task.OutputAssets.AddNew("Output asset",
            AssetCreationOptions.None);

        job.StateChanged += new EventHandler<JobStateChangedEventArgs>(JobStateChanged);
        job.Submit();
        job.GetExecutionProgressTask(CancellationToken.None).Wait();

        return job.OutputMediaAssets[0];
    }


> [!NOTE]
> Bieżące ograniczenia:
>
> Ustawienie nieprzezroczystość nakładki Hello nie jest obsługiwane.
>
> Źródłowy plik wideo, a plik obrazu nakładki hello ma toobe w hello elementu zawartości i hello zestawu toobe potrzeb plików wideo jako plik podstawowy hello w tym zasobów.
>
>

### <a name="json-preset"></a>Ustawienie wstępne JSON
    {
      "Version": 1.0,
      "Sources": [
        {
          "Streams": [],
          "Filters": {
            "VideoOverlay": {
              "Position": {
                "X": 100,
                "Y": 100,
                "Width": 100,
                "Height": 50
              },
              "AudioGainLevel": 0.0,
              "MediaParams": [
                {
                  "OverlayLoopCount": 1
                },
                {
                  "IsOverlay": true,
                  "OverlayLoopCount": 1,
                  "InputLoop": true
                }
              ],
              "Source": "Image001.png",
              "Clip": {
                "Duration": "00:00:05"
              },
              "FadeInDuration": {
                "Duration": "00:00:01"
              },
              "FadeOutDuration": {
                "StartTime": "00:00:03",
                "Duration": "00:00:04"
              }
            }
          },
          "Pad": true
        }
      ],
      "Codecs": [
        {
          "KeyFrameInterval": "00:00:02",
          "H264Layers": [
            {
              "Profile": "Auto",
              "Level": "auto",
              "Bitrate": 1045,
              "MaxBitrate": 1045,
              "BufferWindow": "00:00:05",
              "ReferenceFrames": 3,
              "EntropyMode": "Cavlc",
              "AdaptiveBFrame": true,
              "Type": "H264Layer",
              "Width": "640",
              "Height": "360",
              "FrameRate": "0/1"
            }
          ],
          "Type": "H264Video"
        },
        {
          "Type": "CopyAudio"
        }
      ],
      "Outputs": [
        {
          "FileName": "{Basename}{Extension}",
          "Format": {
            "Type": "MP4Format"
          }
        }
      ]
    }


### <a name="xml-preset"></a>Ustawienie wstępne XML
    <?xml version="1.0" encoding="utf-16"?>
    <Preset xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" Version="1.0" xmlns="http://www.windowsazure.com/media/encoding/Preset/2014/03">
      <Sources>
        <Source>
          <Streams />
          <Filters>
            <VideoOverlay>
              <Source>Image001.png</Source>
              <Clip Duration="PT5S" />
              <FadeInDuration Duration="PT1S" />
              <FadeOutDuration StartTime="PT3S" Duration="PT4S" />
              <Position X="100" Y="100" Width="100" Height="50" />
              <Opacity>0</Opacity>
              <AudioGainLevel>0</AudioGainLevel>
              <MediaParams>
                <MediaParam>
                  <IsOverlay>false</IsOverlay>
                  <OverlayLoopCount>1</OverlayLoopCount>
                  <InputLoop>false</InputLoop>
                </MediaParam>
                <MediaParam>
                  <IsOverlay>true</IsOverlay>
                  <OverlayLoopCount>1</OverlayLoopCount>
                  <InputLoop>true</InputLoop>
                </MediaParam>
              </MediaParams>
            </VideoOverlay>
          </Filters>
          <Pad>true</Pad>
        </Source>
      </Sources>
      <Encoding>
        <H264Video>
          <KeyFrameInterval>00:00:02</KeyFrameInterval>
          <H264Layers>
            <H264Layer>
              <Bitrate>1045</Bitrate>
              <Width>640</Width>
              <Height>360</Height>
              <FrameRate>0/1</FrameRate>
              <Profile>Auto</Profile>
              <Level>auto</Level>
              <BFrames>0</BFrames>
              <ReferenceFrames>3</ReferenceFrames>
              <Slices>0</Slices>
              <AdaptiveBFrame>true</AdaptiveBFrame>
              <EntropyMode>Cavlc</EntropyMode>
              <BufferWindow>00:00:05</BufferWindow>
              <MaxBitrate>1045</MaxBitrate>
            </H264Layer>
          </H264Layers>
        </H264Video>
        <CopyAudio />
      </Encoding>
      <Outputs>
        <Output FileName="{Basename}{Extension}">
          <MP4Format />
        </Output>
      </Outputs>
    </Preset>


## <a id="silent_audio"></a>Wstawić dyskretnej ścieżki audio, gdy dane wejściowe nie zawierają żadnych audio
Domyślnie w przypadku wysłania koder toohello wejściowego, który zawiera tylko wideo i audio nie następnie zawartości wyjściowej hello zawiera pliki, które zawierają dane tylko wideo. Niektóre odtwarzacze może nie być możliwe toohandle takich danych wyjściowych strumieni. W tym scenariuszu, można użyć tego ustawienia tooforce hello koder tooadd wyjściowego toohello dyskretnej ścieżki audio.

tooforce hello koder tooproduce element zawartości zawierający dyskretnej ścieżki audio, gdy dane wejściowe nie zawierają żadnych audio, określ wartość "InsertSilenceIfNoAudio" hello.

Może mieć jedną z hello predefiniowane rynkowej udokumentowane w [to](media-services-mes-presets-overview.md) sekcji, a następnie wprowadź powitania po dokonaniu zmian:

### <a name="json-preset"></a>Ustawienie wstępne JSON
    {
      "Channels": 2,
      "SamplingRate": 44100,
      "Bitrate": 96,
      "Type": "AACAudio",
      "Condition": "InsertSilenceIfNoAudio"
    }

### <a name="xml-preset"></a>Ustawienie wstępne XML
    <AACAudio Condition="InsertSilenceIfNoAudio">
      <Channels>2</Channels>
      <SamplingRate>44100</SamplingRate>
      <Bitrate>96</Bitrate>
    </AACAudio>

## <a id="deinterlacing"></a>Wyłączanie automatycznego usuwania przeplotu.
Klienci nie muszą toodo niczego, jeśli ich jak hello przeplotu toobe zawartość do naprzemiennych automatycznie. Hello automatycznego usuwania przeplot znajduje się na powitania (ustawienie domyślne), który rynkowej hello automatyczne wykrywanie naprzemiennych ramek, a tylko cofnąć interlaces oznaczony jako naprzemiennych ramki.

Można wyłączyć hello automatycznego usuwania przeplotu. Ta opcja nie jest zalecane.

### <a name="json-preset"></a>Ustawienie wstępne JSON
    "Sources": [
    {
     "Filters": {
        "Deinterlace": {
          "Mode": "Off"
        }
      },
    }
    ]

### <a name="xml-preset"></a>Ustawienie wstępne XML
    <Sources>
    <Source>
      <Filters>
        <Deinterlace>
          <Mode>Off</Mode>
        </Deinterlace>
      </Filters>
    </Source>
    </Sources>


## <a id="audio_only"></a>Ustawienia tylko do audio
W tej sekcji przedstawiono dwie predefiniowane rynkowej tylko dźwięk: AAC Audio i AAC dobrej jakości Audio.

### <a name="aac-audio"></a>AAC Audio
    {
      "Version": 1.0,
      "Codecs": [
        {
          "Profile": "AACLC",
          "Channels": 2,
          "SamplingRate": 48000,
          "Bitrate": 128,
          "Type": "AACAudio"
        }
      ],
      "Outputs": [
        {
          "FileName": "{Basename}_AAC_{AudioBitrate}.mp4",
          "Format": {
            "Type": "MP4Format"
          }
        }
      ]
    }

### <a name="aac-good-quality-audio"></a>AAC dobrej jakości Audio
    {
      "Version": 1.0,
      "Codecs": [
        {
          "Profile": "AACLC",
          "Channels": 2,
          "SamplingRate": 48000,
          "Bitrate": 192,
          "Type": "AACAudio"
        }
      ],
      "Outputs": [
        {
          "FileName": "{Basename}_AAC_{AudioBitrate}.mp4",
          "Format": {
            "Type": "MP4Format"
          }
        }
      ]
    }

## <a id="concatenate"></a>Łączenie dwóch lub więcej plików wideo

Witaj poniższy przykład pokazuje, jak można wygenerować wstępnie zdefiniowane tooconcatenate dwóch lub więcej plików wideo. najbardziej typowym scenariuszem Hello jest tooadd nagłówka lub przyczepy toohello głównego wideo. Witaj przeznaczony jest używany, gdy pliki wideo hello edytowany razem udziału właściwości (rozdzielczości szybkość klatek, liczba ścieżki audio, itp.). Należy zadbać nie toomix wideo różne szybkości odtwarzania, albo z różną liczbą ścieżki audio.

>[!NOTE]
>Witaj bieżący projekt funkcji łączenia hello oczekuje tego hello wejściowych klipy wideo są spójne pod względem rozdzielczości, szybkość klatek itp. 

### <a name="requirements-and-considerations"></a>Wymagania i uwagi

* Wejściowy wideo powinien mieć tylko jedną ścieżkę audio.
* Wejściowy wideo powinien mieć hello tego samego szybkość klatek.
* Należy przekazać pliki wideo do oddzielnych zasobów i ustawić hello wideo jako plik podstawowy hello w poszczególnych zasobów.
* Należy czas trwania hello tooknow plików wideo.
* Hello predefiniowanych poniższe przykłady przyjęto założenie, że wszystkie filmy wejściowych hello rozpocząć z sygnaturą czasową o wartości zero. Należy wartości StartTime hello toomodify Jeśli hello wideo ma inną sygnaturą czasową początkowego, tak jak zwykle hello przypadku archiwa na żywo.
* Hello ustawienie wstępne JSON sprawia, że jawnego odwołania do wartości AssetID toohello hello zasobów wejściowych.
* Witaj przykładowy kod przyjęto założenie, że tego ustawienia wstępnego JSON powitalne został zapisany plik lokalny tooa, takie jak "C:\supportFiles\preset.json". Zakłada się również, czy dwa zasoby zostały utworzone przez dwa pliki wideo i wiedzieć hello wynikowe IDśrodkaTrwałego wartości.
* Witaj fragment kodu i JSON ustawienie wstępne przedstawiono przykład łączenia dwóch plików wideo. Można go rozszerzyć toomore niż dwa pliki wideo przez:

  1. Zadanie telefonicznej. InputAssets.Add() wielokrotnie tooadd więcej filmów w kolejności.
  2. Co odpowiadającego edytuje element toohello "Sources" hello JSON, dodając więcej wpisów w hello tej samej kolejności.

### <a name="net-code"></a>Kodu platformy .NET

    IAsset asset1 = _context.Assets.Where(asset => asset.Id == "nb:cid:UUID:606db602-efd7-4436-97b4-c0b867ba195b").FirstOrDefault();
    IAsset asset2 = _context.Assets.Where(asset => asset.Id == "nb:cid:UUID:a7e2b90f-0565-4a94-87fe-0a9fa07b9c7e").FirstOrDefault();

    // Declare a new job.
    IJob job = _context.Jobs.Create("Media Encoder Standard Job for Concatenating Videos");
    // Get a media processor reference, and pass tooit hello name of the
    // processor toouse for hello specific task.
    IMediaProcessor processor = GetLatestMediaProcessorByName("Media Encoder Standard");

    // Load hello XML (or JSON) from hello local file.
    string configuration = File.ReadAllText(@"c:\supportFiles\preset.json");

    // Create a task
    ITask task = job.Tasks.AddNew("Media Encoder Standard encoding task",
        processor,
        configuration,
        TaskOptions.None);

    // Specify hello input videos toobe concatenated (in order).
    task.InputAssets.Add(asset1);
    task.InputAssets.Add(asset2);
    // Add an output asset toocontain hello results of hello job.
    // This output is specified as AssetCreationOptions.None, which
    // means hello output asset is not encrypted.
    task.OutputAssets.AddNew("Output asset",
        AssetCreationOptions.None);

    job.StateChanged += new EventHandler<JobStateChangedEventArgs>(JobStateChanged);
    job.Submit();
    job.GetExecutionProgressTask(CancellationToken.None).Wait();

### <a name="json-preset"></a>Ustawienie wstępne JSON

Zaktualizuj niestandardowe ustawienia wstępnego z identyfikatorami hello zasoby, które mają tooconcatenate i z segmentem odpowiedni czas hello każdego wideo.

    {
      "Version": 1.0,
      "Sources": [
        {
          "AssetID": "606db602-efd7-4436-97b4-c0b867ba195b",
          "StartTime": "00:00:01",
          "Duration": "00:00:15"
        },
        {
          "AssetID": "a7e2b90f-0565-4a94-87fe-0a9fa07b9c7e",
          "StartTime": "00:00:02",
          "Duration": "00:00:05"
        }
      ],
      "Codecs": [
        {
          "KeyFrameInterval": "00:00:02",
          "SceneChangeDetection": true,
          "H264Layers": [
            {
              "Level": "auto",
              "Bitrate": 1800,
              "MaxBitrate": 1800,
              "BufferWindow": "00:00:05",
              "BFrames": 3,
              "ReferenceFrames": 3,
              "AdaptiveBFrame": true,
              "Type": "H264Layer",
              "Width": "640",
              "Height": "360",
              "FrameRate": "0/1"
            }
          ],
          "Type": "H264Video"
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
          "FileName": "{Basename}_{Width}x{Height}_{VideoBitrate}.mp4",
          "Format": {
            "Type": "MP4Format"
          }
        }
      ]
    }

## <a id="crop"></a>Przytnij wideo przy użyciu Media Encoder Standard
Zobacz hello [Przycinanie wideo z Media Encoder Standard](media-services-crop-video.md) tematu.

## <a id="no_video"></a>Wstaw Ścieżka wideo, gdy dane wejściowe nie ma karty wideo

Domyślnie w przypadku wysłania koder toohello wejściowego, który zawiera tylko audio i wideo nie następnie zawartości wyjściowej hello zawiera pliki, które zawierają dane tylko audio. Niektóre odtwarzacze, łącznie z usługi Azure Media Player (zobacz [to](https://feedback.azure.com/forums/169396-azure-media-services/suggestions/8082468-audio-only-scenarios)) może nie być możliwe toohandle tych strumieni. Można użyć tego ustawienia tooforce hello koder tooadd wyjściowego toohello monochromatyczny Ścieżka wideo w tym scenariuszu.

> [!NOTE]
> Wymuszanie tooinsert kodera hello dane wyjściowe Ścieżka wideo zwiększa hello rozmiar hello output zasobów i tym samym hello kosztów ponoszonych na powitania kodowania zadań. Należy uruchomić testy tooverify to zwiększenie wynikowe ma tylko niewielkie wpływ na Twoje opłaty miesięczne.
>

### <a name="inserting-video-at-only-hello-lowest-bitrate"></a>Wstawianie wideo na wyłącznie hello najniższa szybkość transmisji bitów

Załóżmy, że są przy użyciu wielu kodowania szybkości transmisji bitów ustawień, takich jak ["H264 szybkość transmisji bitów 720p"](media-services-mes-preset-h264-multiple-bitrate-720p.md) tooencode całego wejściowych katalogu do przesyłania strumieniowego, który zawiera pliki wideo i audio — tylko do plików. W tym scenariuszu po hello danych wejściowych nie ma karty wideo, może być tooinsert kodera hello tooforce wideo w skali odcieni szarości śledzenie na właśnie hello najniższa szybkość transmisji bitów, jako min. tooinserting wideo w każdym szybkości transmisji bitów danych wyjściowych. tooachieve, to należy toouse hello **InsertBlackIfNoVideoBottomLayerOnly** flagi.

Może mieć jedną z hello predefiniowane rynkowej udokumentowane w [to](media-services-mes-presets-overview.md) sekcji, a następnie wprowadź powitania po dokonaniu zmian:

#### <a name="json-preset"></a>Ustawienie wstępne JSON
    {
          "KeyFrameInterval": "00:00:02",
          "StretchMode": "AutoSize",
          "Condition": "InsertBlackIfNoVideoBottomLayerOnly",
          "H264Layers": [
          …
          ]
    }

#### <a name="xml-preset"></a>Ustawienie wstępne XML

Za pomocą XML, używaj warunku = "InsertBlackIfNoVideoBottomLayerOnly" jako atrybutu toohello **H264Video** element i stan za = "InsertSilenceIfNoAudio" jako atrybutu**AACAudio**.

```
. . .
<Encoding>
  <H264Video Condition="InsertBlackIfNoVideoBottomLayerOnly">
    <KeyFrameInterval>00:00:02</KeyFrameInterval>
    <SceneChangeDetection>true</SceneChangeDetection>
    <StretchMode>AutoSize</StretchMode>
    <H264Layers>
      <H264Layer>
        . . .
      </H264Layer>
    </H264Layers>
    <Chapters />
  </H264Video>
  <AACAudio Condition="InsertSilenceIfNoAudio">
    <Profile>AACLC</Profile>
    <Channels>2</Channels>
    <SamplingRate>48000</SamplingRate>
    <Bitrate>128</Bitrate>
  </AACAudio>
</Encoding>
. . .
```

### <a name="inserting-video-at-all-output-bitrates"></a>Wstawianie wideo na wszystkich danych wyjściowych szybkości transmisji bitów
Załóżmy, że są przy użyciu wielu kodowania szybkości transmisji bitów ustawień, takich jak ["H264 szybkość transmisji bitów 720p](media-services-mes-preset-H264-Multiple-Bitrate-720p.md) tooencode całego wejściowych katalogu do przesyłania strumieniowego, który zawiera pliki wideo i audio — tylko do plików. W tym scenariuszu po hello danych wejściowych nie ma karty wideo, może być tooinsert kodera hello tooforce monochromatyczny wideo śledzenia na wszystkich hello dane wyjściowe szybkości transmisji bitów. Gwarantuje to, że dane wyjściowe są wszystkie jednorodnego z toonumber względem ścieżki wideo i audio ścieżki. tooachieve, to należy hello toospecify flagi "InsertBlackIfNoVideo".

Może mieć jedną z hello predefiniowane rynkowej udokumentowane w [to](media-services-mes-presets-overview.md) sekcji, a następnie wprowadź powitania po dokonaniu zmian:

#### <a name="json-preset"></a>Ustawienie wstępne JSON
    {
          "KeyFrameInterval": "00:00:02",
          "StretchMode": "AutoSize",
          "Condition": "InsertBlackIfNoVideo",
          "H264Layers": [
          …
          ]
    }

#### <a name="xml-preset"></a>Ustawienie wstępne XML

Za pomocą XML, używaj warunku = "InsertBlackIfNoVideo" jako atrybutu toohello **H264Video** element i stan za = "InsertSilenceIfNoAudio" jako atrybutu**AACAudio**.

```
. . .
<Encoding>
  <H264Video Condition="InsertBlackIfNoVideo">
    <KeyFrameInterval>00:00:02</KeyFrameInterval>
    <SceneChangeDetection>true</SceneChangeDetection>
    <StretchMode>AutoSize</StretchMode>
    <H264Layers>
      <H264Layer>
        . . .
      </H264Layer>
    </H264Layers>
    <Chapters />
  </H264Video>
  <AACAudio Condition="InsertSilenceIfNoAudio">
    <Profile>AACLC</Profile>
    <Channels>2</Channels>
    <SamplingRate>48000</SamplingRate>
    <Bitrate>128</Bitrate>
  </AACAudio>
</Encoding>
. . .  
```

## <a id="rotate_video"></a>Obróć wideo
Witaj [Media Encoder Standard](media-services-dotnet-encode-with-media-encoder-standard.md) obsługuje obrotu kątami 0/90/180/270. Witaj domyślne zachowanie to "Auto", gdy próbuje toodetect hello obrotu metadane w pliku wideo przychodzących hello i kompensacji go. Uwzględnij następujące elementy hello **źródeł** tooone element hello ustawień określonych w [to](media-services-mes-presets-overview.md) sekcji:

### <a name="json-preset"></a>Ustawienie wstępne JSON
    "Sources": [
    {
      "Streams": [],
      "Filters": {
        "Rotation": "90"
      }
    }
    ],
    "Codecs": [

    ...
### <a name="xml-preset"></a>Ustawienie wstępne XML
    <Sources>
           <Source>
          <Streams />
          <Filters>
            <Rotation>90</Rotation>
          </Filters>
        </Source>
    </Sources>

Zobacz też [to](media-services-mes-schema.md#PreserveResolutionAfterRotation) tematu, aby uzyskać więcej informacji na interpretowanie ustawienia szerokości i wysokości hello w hello kodera hello zdefiniowane, po wyzwoleniu kompensacji obrotu.

Za pomocą hello wartość "0" tooindicate toohello koder tooignore obrotu metadanych, jeśli jest obecny w hello wejściowy plik wideo.

## <a name="media-services-learning-paths"></a>Ścieżki szkoleniowe dotyczące usługi Media Services
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Przekazywanie opinii
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="see-also"></a>Zobacz też
[Usługi multimediów kodowania — omówienie](media-services-encode-asset.md)
