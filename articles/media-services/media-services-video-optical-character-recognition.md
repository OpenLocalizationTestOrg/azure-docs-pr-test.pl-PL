---
title: "tekst aaaDigitize Rozpoznawania analizy multimediów Azure | Dokumentacja firmy Microsoft"
description: "Azure Media Rozpoznawania Analytics (OCR) umożliwia tooconvert zawartości tekstowej w plikach wideo na tekst cyfrowy można edytować, wyszukiwanie.  Dzięki temu tooautomate wyodrębniania hello łatwy do rozpoznania metadanych z hello sygnału wideo multimediów."
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: 307c196e-3a50-4f4b-b982-51585448ffc6
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 07/31/2017
ms.author: juliako
ms.openlocfilehash: 0476c3ba3942b2c5182a34a429909adbf5c75ac9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-media-analytics-tooconvert-text-content-in-video-files-into-digital-text"></a>Użycie zawartości tekstowej tooconvert analizy multimediów Azure w plikach wideo na cyfrowe tekst
## <a name="overview"></a>Omówienie
Jeśli należy tekst tooextract zawartości od plików wideo i generowanie tekstu cyfrowego można edytować, wyszukiwanie, należy użyć Rozpoznawania analizy multimediów Azure (OCR). Ten procesor multimediów Azure wykrywa zawartości tekstowej w plikach wideo i generuje pliki tekstowe do użycia. Rozpoznawania umożliwia możesz tooautomate hello wyodrębniania łatwy do rozpoznania metadanych z hello sygnału wideo multimediów.

Gdy jest używany w połączeniu z aparatu wyszukiwania, możesz łatwo indeksu multimediów tekst i zwiększyć wykrywalność hello zawartości. Jest to bardzo przydatne w dużej tekstową wideo, takich jak nagrywanie wideo lub Przechwytywanie ekranu prezentacji pokazu slajdów. Procesor multimediów Azure Rozpoznawania Hello jest zoptymalizowana pod kątem cyfrowe tekstu.

Witaj **Azure Media Rozpoznawania** procesor multimediów jest obecnie w przeglądzie.

Ten temat zawiera szczegółowe informacje o **Azure Media Rozpoznawania** i przedstawia sposób toouse go przy użyciu zestawu SDK usługi Media Services dla platformy .NET. Aby uzyskać dodatkowe informacje i przykłady, zobacz [ten blog](https://azure.microsoft.com/blog/announcing-video-ocr-public-preview-new-config/).

## <a name="ocr-input-files"></a>Rozpoznawania plików wejściowych
Pliki wideo. Obecnie są obsługiwane następujące formaty hello: MP4, MOV i WMV.

## <a name="task-configuration"></a>Konfiguracja zadania
Konfiguracja zadania (ustawienia domyślne). Podczas tworzenia zadania z **Azure Media Rozpoznawania**, należy określić ustawienia wstępnego za pomocą formatu JSON i XML konfiguracji. 

>[!NOTE]
>Aparat Rozpoznawania Hello przyjmuje tylko obszar obrazu z minimalną pikseli toomaximum 32000 40 pikseli jako prawidłową wartość wejściową w obu wysokość i szerokość.
>

### <a name="attribute-descriptions"></a>Opisy atrybutów
| Nazwa atrybutu | Opis |
| --- | --- |
|AdvancedOutput| Jeśli ustawisz AdvancedOutput tootrue dane wyjściowe JSON hello zawierają dane pozycyjnych dla każdego pojedynczego wyrazu (w regionach i dodanie toophrases). Jeśli nie chcesz, aby toosee te szczegóły zestawu hello Flaga toofalse. Witaj wartość domyślna to false. Aby uzyskać więcej informacji, zobacz [ten blog](https://azure.microsoft.com/blog/azure-media-ocr-simplified-output/).|
| Język |(opcjonalnie) opisano hello język tekstu, dla których toolook. Jedną z następujących hello: AutoDetect (ustawienie domyślne), arabskiego, ChineseSimplified, ChineseTraditional, czeski, duński, holenderski, angielski, fiński, francuski, niemiecki, grecki, węgierski, włoski, japoński, koreański, norweski, Polski, portugalski, rumuński, rosyjski, SerbianCyrillic, SerbianLatin, słowacki, hiszpański, szwedzki, turecki. |
| TextOrientation |(opcjonalnie) opisano hello orientację tekstu, dla których toolook.  "Po lewej stronie" oznacza, że hello początku wszystkie litery są skierowane hello lewej.  Domyślny tekst (na przykład tych, które można znaleźć w księdze) można wywołać "W górę" orientacji.  Jedną z następujących hello: AutoDetect (ustawienie domyślne), maksymalnie, prawo, w dół, lewo. |
| Parametru TimeInterval |(opcjonalnie) opisano hello próbkowania.  Domyślna to co 1/2 sekundy.<br/>Format JSON — hh: mm:. SSS (00:00:00.500 domyślne)<br/>Format XML — podstawowy czas trwania W3C XSD (domyślnie PT0.5) |
| DetectRegions |(opcjonalnie) Tablica obiektów DetectRegion określenie obszarów w ramce wideo hello w tekst, który toodetect.<br/>Obiekt DetectRegion się następujące cztery wartości całkowite hello:<br/>Po lewej — pikseli z powitania od lewego marginesu<br/>TOP — pikseli z margines górny hello<br/>Szerokość — Szerokość hello regionu w pikselach<br/>Wysokość — wysokość hello regionu w pikselach |

#### <a name="json-preset-example"></a>Przykład predefiniowanych JSON

    {
        "Version":1.0, 
        "Options": 
        {
            "AdvancedOutput":"true",
            "Language":"English", 
            "TimeInterval":"00:00:01.5",
            "TextOrientation":"Up",
            "DetectRegions": [
                    {
                       "Left": 10,
                       "Top": 10,
                       "Width": 100,
                       "Height": 50
                    }
             ]
        }
    }


#### <a name="xml-preset-example"></a>Przykład wstępnie zdefiniowane w pliku XML
    <?xml version=""1.0"" encoding=""utf-16""?>
    <VideoOcrPreset xmlns:xsi=""http://www.w3.org/2001/XMLSchema-instance"" xmlns:xsd=""http://www.w3.org/2001/XMLSchema"" Version=""1.0"" xmlns=""http://www.windowsazure.com/media/encoding/Preset/2014/03"">
      <Options>
         <AdvancedOutput>true</AdvancedOutput>
         <Language>English</Language>
         <TimeInterval>PT1.5S</TimeInterval>
         <DetectRegions>
             <DetectRegion>
                   <Left>10</Left>
                   <Top>10</Top>
                   <Width>100</Width>
                   <Height>50</Height>
            </DetectRegion>
       </DetectRegions>
       <TextOrientation>Up</TextOrientation>
      </Options>
    </VideoOcrPreset>

## <a name="ocr-output-files"></a>Pliki wyjściowe Rozpoznawania
dane wyjściowe Hello procesor multimediów Rozpoznawania hello jest to plik JSON.

### <a name="elements-of-hello-output-json-file"></a>Elementy hello pliku wyjściowego w formacie JSON
Wyjście wideo Rozpoznawania Hello udostępnia dane segmentem czas na powitania znaków wideo.  Można użyć atrybutów, takich jak języka lub orientacji toohone w dokładnie słowa hello wybrane analizowanie. 

dane wyjściowe Hello zawierają hello następujące atrybuty:

| Element | Opis |
| --- | --- |
| skali czasu |"Takty" na sekundę hello wideo |
| Przesunięcie |Czas przesunięcia znaczników czasu. W wersji 1.0 interfejsów API, wideo ta będzie zawsze równa 0. |
| szybkość klatek |Klatek na sekundę hello wideo |
| Szerokość |szerokość hello wideo w pikselach |
| Wysokość |wysokość hello wideo w pikselach |
| fragmenty |Tablica oparte na czasie fragmentów wideo, w których hello jest fragmentaryczne metadanych |
| rozpoczynanie |uruchomienie fragmentu w parametrem "ticks" |
| Czas trwania |Długość fragmentu w parametrem "ticks" |
| interval |Interwał każdego zdarzenia w ciągu danego fragmentu hello |
| zdarzenia |Tablica zawierająca regionów |
| Region |Obiekt reprezentujący wykryto słów ani fraz |
| Język |język tekstu hello wykryte w obrębie regionu |
| Orientacja |orientację tekstu hello wykryte w obrębie regionu |
| wiersze |Tablica wierszy tekstu w regionie |
| Tekst |Witaj tekstu |

### <a name="json-output-example"></a>Przykład danych wyjściowych JSON
Witaj poniższym przykładzie danych wyjściowych zawiera ogólne informacje wideo hello oraz kilka fragmentów wideo. W każdym wideo fragmentu zawiera każdego regionu, który jest wykrywany przez pakiet administracyjny Rozpoznawania z językiem hello i orientacji tekstu. Hello region zawiera także każdy wiersz programu word w tym regionie tekst hello wiersza, pozycja hello wiersza i informacje co word (zawartość programu word, pozycji i zaufania) w tym wierszu. Hello poniżej przedstawiono przykładowy i umieścić niektóre wbudowane komentarze.

    {
        "version": 1, 
        "timescale": 90000, 
        "offset": 0, 
        "framerate": 30, 
        "width": 640, 
        "height": 480,  // general video information
        "fragments": [
            {
                "start": 0, 
                "duration": 180000, 
                "interval": 90000,  // hello time information about this fragment
                "events": [
                    [
                       { 
                            "region": { // hello detected region array in this fragment 
                                "language": "English",  // region language
                                "orientation": "Up",  // text orientation
                                "lines": [  // line information array in this region, including hello text and hello position
                                    {
                                        "text": "One Two", 
                                        "left": 10, 
                                        "top": 10, 
                                        "right": 210, 
                                        "bottom": 110, 
                                        "word": [  // word information array in this line
                                            {
                                                "text": "One", 
                                                "left": 10, 
                                                "top": 10, 
                                                "right": 110, 
                                                "bottom": 110, 
                                                "confidence": 900
                                            }, 
                                            {
                                                "text": "Two", 
                                                "left": 110, 
                                                "top": 10, 
                                                "right": 210, 
                                                "bottom": 110, 
                                                "confidence": 910
                                            }
                                        ]
                                    }
                                ]
                            }
                        }
                    ]
                ]
            }
        ]
    }

## <a name="net-sample-code"></a>.NET przykładowy kod

następujące Hello program pokazuje sposób:

1. Utworzenie elementu zawartości i przesyłanie pliku multimediów do hello zawartości.
2. Utwórz zadanie przy użyciu pliku konfiguracji/ustawienie wstępne Rozpoznawania.
3. Pobierz pliki w formacie JSON dane wyjściowe hello. 
   
#### <a name="create-and-configure-a-visual-studio-project"></a>Tworzenie i konfigurowanie projektu programu Visual Studio

Konfigurowanie środowiska projektowego i wypełnić plik app.config hello o informacje dotyczące połączenia, zgodnie z opisem w [tworzenia usługi Media Services z platformą .NET](media-services-dotnet-how-to-use.md). 

#### <a name="example"></a>Przykład

    using System;
    using System.Configuration;
    using System.IO;
    using System.Linq;
    using Microsoft.WindowsAzure.MediaServices.Client;
    using System.Threading;
    using System.Threading.Tasks;

    namespace OCR
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

                // Run hello OCR job.
                var asset = RunOCRJob(@"C:\supportFiles\OCR\presentation.mp4",
                                            @"C:\supportFiles\OCR\config.json");

                // Download hello job output asset.
                DownloadAsset(asset, @"C:\supportFiles\OCR\Output");
            }

            static IAsset RunOCRJob(string inputMediaFilePath, string configurationFile)
            {
                // Create an asset and upload hello input media file toostorage.
                IAsset asset = CreateAssetAndUploadSingleFile(inputMediaFilePath,
                    "My OCR Input Asset",
                    AssetCreationOptions.None);

                // Declare a new job.
                IJob job = _context.Jobs.Create("My OCR Job");

                // Get a reference tooAzure Media OCR.
                string MediaProcessorName = "Azure Media OCR";

                var processor = GetLatestMediaProcessorByName(MediaProcessorName);

                // Read configuration from hello specified file.
                string configuration = File.ReadAllText(configurationFile);

                // Create a task with hello encoding details, using a string preset.
                ITask task = job.Tasks.AddNew("My OCR Task",
                    processor,
                    configuration,
                    TaskOptions.None);

                // Specify hello input asset.
                task.InputAssets.Add(asset);

                // Add an output asset toocontain hello results of hello job.
                task.OutputAssets.AddNew("My OCR Output Asset", AssetCreationOptions.None);

                // Use hello following event handler toocheck job progress.  
                job.StateChanged += new EventHandler<JobStateChangedEventArgs>(StateChanged);

                // Launch hello job.
                job.Submit();

                // Check job execution and wait for job toofinish.
                Task progressJobTask = job.GetExecutionProgressTask(CancellationToken.None);

                progressJobTask.Wait();

                // If job state is Error, hello event handling
                // method for job progress should log errors.  Here we check
                // for error state and exit if needed.
                if (job.State == JobState.Error)
                {
                    ErrorDetail error = job.Tasks.First().ErrorDetails.First();
                    Console.WriteLine(string.Format("Error: {0}. {1}",
                                                    error.Code,
                                                    error.Message));
                    return null;
                }

                return job.OutputMediaAssets[0];
            }

            static IAsset CreateAssetAndUploadSingleFile(string filePath, string assetName, AssetCreationOptions options)
            {
                IAsset asset = _context.Assets.Create(assetName, options);

                var assetFile = asset.AssetFiles.Create(Path.GetFileName(filePath));
                assetFile.Upload(filePath);

                return asset;
            }

            static void DownloadAsset(IAsset asset, string outputDirectory)
            {
                foreach (IAssetFile file in asset.AssetFiles)
                {
                    file.Download(Path.Combine(outputDirectory, file.Name));
                }
            }

            static IMediaProcessor GetLatestMediaProcessorByName(string mediaProcessorName)
            {
                var processor = _context.MediaProcessors
                    .Where(p => p.Name == mediaProcessorName)
                    .ToList()
                    .OrderBy(p => new Version(p.Version))
                    .LastOrDefault();

                if (processor == null)
                    throw new ArgumentException(string.Format("Unknown media processor",
                                                               mediaProcessorName));

                return processor;
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

        }
    }

## <a name="media-services-learning-paths"></a>Ścieżki szkoleniowe dotyczące usługi Media Services
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Przekazywanie opinii
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="related-links"></a>Powiązane linki
[Przegląd analiz usługi Azure Media Services](media-services-analytics-overview.md)

