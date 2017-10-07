---
title: "Ruchy aaaDetect z analizy multimediów Azure | Dokumentacja firmy Microsoft"
description: "Witaj umożliwia procesora (MP) nośnika czujnik ruchu Azure Media tooefficiently można zidentyfikować sekcje zawierają informacje przydatne w wideo w innym przypadku długich i procesu."
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: d144f813-1a55-442f-a895-5c4cb6d0aeae
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 07/31/2017
ms.author: milanga;juliako;
ms.openlocfilehash: cb431375c92222053ed2239dd4e45767524dab68
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="detect-motions-with-azure-media-analytics"></a>Wykrywanie ruchów z analizy multimediów Azure
## <a name="overview"></a>Omówienie
Witaj **czujnik ruchu Azure Media** nośnika procesora (MP) umożliwia tooefficiently można zidentyfikować sekcje zawierają informacje przydatne w wideo w innym przypadku długich i procesu. Wykrywanie ruchu może służyć na statycznych aparatu materiał tooidentify sekcje wideo hello gdzie występuje ruchu. Generuje plik JSON zawierający metadane z sygnatury czasowe i hello ograniczenia regionu, w którym wystąpiło zdarzenie hello.

Docelowe do źródła wideo zabezpieczeń, ta technologia jest możliwe toocategorize ruchu na odpowiednie zdarzenia i fałszywych alarmów, takie jak cieni i zmian oświetlenia. Dzięki temu można toogenerate alertów zabezpieczeń z aparatu fotograficznego źródła danych bez otrzymywania wiadomości-śmieci nieskończone zdarzenia nie ma znaczenia, będąc chwil stanie tooextract płynących z bardzo długi nadzoru wideo.

Witaj **czujnik ruchu Azure Media** pakiet administracyjny jest obecnie w przeglądzie.

Ten temat zawiera szczegółowe informacje o **czujnik ruchu Azure Media** i przedstawia sposób toouse go przy użyciu zestawu SDK usługi Media Services dla platformy .NET

## <a name="motion-detector-input-files"></a>Pliki wejściowe wykrywanie ruchu
Pliki wideo. Obecnie są obsługiwane następujące formaty hello: MP4, MOV i WMV.

## <a name="task-configuration-preset"></a>Konfiguracja zadania (ustawienia domyślne)
Podczas tworzenia zadania z **czujnik ruchu Azure Media**, należy określić ustawienia domyślne konfiguracji. 

### <a name="parameters"></a>Parametry
Program hello następujące parametry:

| Nazwa | Opcje | Opis | Domyślne |
| --- | --- | --- | --- |
| sensitivityLevel |Ciąg: "Niski", "medium',"Wysoki" |Ustawia poziom czułości hello na ruchy, która jest raportowana. Dostosuj tooadjust ilość fałszywych alarmów. |"Średni" |
| frameSamplingValue |Dodatnia liczba całkowita |Ustawia częstotliwość hello, w której działa algorytmu. Każdy ramki jest równa 1, 2 oznacza, że każdy ramki 2 i tak dalej. |1 |
| detectLightChange |Wartość logiczna: "prawda", "fałsz" |Określa, czy zmiany światła są podane w wynikach hello |"Fałsz" |
| mergeTimeThreshold |Czas xs: Hh: mm:<br/>Przykład: 00:00:03 |Określa hello przedział czasu między zdarzeniami ruchu, gdzie łączyć i zgłaszane jako 1 2 zdarzenia. |00:00:00 |
| detectionZones |Tablica wykrywania stref:<br/>-Wykrywania strefy jest tablicą 3 lub więcej punktów<br/>— Punkt jest x i y Współrzędna z 0 too1. |W tym artykule opisano hello lista wykrywania wielobocznych stref toobe używane.<br/>Wyniki będą raportowane ze strefami hello jako identyfikator z hello pierwszy z nich jest 'id': 0 |Jednej strefie, która obejmuje całą ramkę hello. |

### <a name="json-example"></a>Przykład JSON
    {
      "version": "1.0",
      "options": {
        "sensitivityLevel": "medium",
        "frameSamplingValue": 1,
        "detectLightChange": "False",
        "mergeTimeThreshold":
        "00:00:02",
        "detectionZones": [
          [
            {"x": 0, "y": 0},
            {"x": 0.5, "y": 0},
            {"x": 0, "y": 1}
           ],
          [
            {"x": 0.3, "y": 0.3},
            {"x": 0.55, "y": 0.3},
            {"x": 0.8, "y": 0.3},
            {"x": 0.8, "y": 0.55},
            {"x": 0.8, "y": 0.8},
            {"x": 0.55, "y": 0.8},
            {"x": 0.3, "y": 0.8},
            {"x": 0.3, "y": 0.55}
          ]
        ]
      }
    }


## <a name="motion-detector-output-files"></a>Pliki wyjściowe wykrywanie ruchu
Zadanie wykrywania ruchu zwróci pliku JSON w zawartości wyjściowej hello opisującą hello ruchu alertów i ich w kategorie hello wideo. Witaj plik będzie zawierać informacje o hello czas i czas trwania ruchu wykryte w hello wideo.

Hello API wykrywanie ruchu zawiera wskaźniki po ruchu w stałej tło w formie wideo (np. nadzoru, wideo) są obiekty. Hello czujnik ruchu jest fałszywe alarmy przeszkolone tooreduce, takie jak oświetlenia i zmiany w tle. Bieżące ograniczenia hello algorytmy obejmują nocy wizji wideo, półprzezroczyste obiektów i małych obiektów.

### <a id="output_elements"></a>Elementy hello pliku wyjściowego w formacie JSON
> [!NOTE]
> W najnowszej wersji hello formacie JSON dane wyjściowe hello została zmieniona, może reprezentować istotne zmiany w przypadku niektórych klientów.
> 
> 

Witaj poniższej tabeli opisano elementy hello pliku wyjściowego w formacie JSON.

| Element | Opis |
| --- | --- |
| Wersja |Odnosi się wersja toohello hello wideo interfejsu API. Witaj bieżąca wersja to 2. |
| skali czasu |"Impulsów" na sekundę hello wideo. |
| Przesunięcie |Przesunięcie czasu Hello sygnatur czasowych w parametrem "ticks". W wersji 1.0 interfejsów API, wideo ta będzie zawsze równa 0. W przyszłości scenariusze, które firma Microsoft obsługuje, ta wartość może zmienić. |
| szybkość klatek |Klatek na sekundę hello wideo. |
| Szerokość, wysokość |Odwołuje się toohello szerokość i wysokość hello wideo w pikselach. |
| Uruchamianie |Witaj start sygnaturą czasową w parametrem "ticks". |
| Czas trwania |Długość Hello zdarzenia hello w parametrem "ticks". |
| Interwał |Interwał powitania każdego wpisu w przypadku hello w parametrem "ticks". |
| Zdarzenia |Każdy fragment zdarzenia zawiera ruchu hello wykryty w tym czas trwania. |
| Typ |W bieżącej wersji hello jest to zawsze "2" dla ogólnego ruchu. Etykieta udostępnia interfejsy API wideo hello elastyczność toocategorize ruchu w przyszłych wersjach. |
| RegionID |Zgodnie z powyższymi wskazówkami, ta będzie zawsze równa 0 w tej wersji. Etykieta daje API wideo hello elastyczność toofind ruchu w różnych regionach w przyszłych wersjach. |
| Regiony |Odwołuje się toohello obszar wideo gdzie interesujących ruchu. <br/><br/>-"id" reprezentuje obszar region hello — w tej wersji jest tylko jeden, identyfikator: 0. <br/>-"type" reprezentuje hello kształt obszaru hello interesujących dla ruchu. "Prostokąt" i "wielokąta" są obecnie obsługiwane.<br/> Jeśli określono "prostokąt" hello region ma wymiarów w X, Y, szerokość i wysokość. Witaj X i Y współrzędne reprezentują współrzędnych XY lewy górny hello hello regionu w skali znormalizowane 0.0 too1.0. Hello szerokości i wysokości reprezentuje rozmiar hello hello regionu w skali znormalizowane 0.0 too1.0. W bieżącej wersji hello X, Y, szerokość i wysokość jest zawsze ustalone na 0, 0 i 1, 1. <br/>Jeśli określono "wielokąta" hello region ma wymiarów w punktach. <br/> |
| fragmenty |metadane Hello jest fragmentaryczne się w różnych segmentach fragmenty. Każdy fragmentu zawiera rozpoczęcia, czas trwania, liczba interwałów i zdarzenia. Fragment ze zdarzeniami nie oznacza, że ruch nie został wykryty podczas tej godziny rozpoczęcia i czas trwania. |
| Nawiasy kwadratowe] |Każdy nawiasu reprezentuje jeden interwał w zdarzeniu hello. Puste nawiasy dla tego przedziału oznacza, że ruch nie została wykryta. |
| Lokalizacje |Ten nowy wpis w polu zdarzenia wymieniono hello lokalizacji, gdzie wystąpił hello ruchu. Jest to bardziej szczegółowy niż hello wykrywania strefy. |

Witaj poniżej przedstawiono przykładowe dane wyjściowe JSON

    {
      "version": 2,
      "timescale": 23976,
      "offset": 0,
      "framerate": 24,
      "width": 1280,
      "height": 720,
      "regions": [
        {
          "id": 0,
          "type": "polygon",
          "points": [{'x': 0, 'y': 0},
            {'x': 0.5, 'y': 0},
            {'x': 0, 'y': 1}]
        }
      ],
      "fragments": [
        {
          "start": 0,
          "duration": 226765
        },
        {
          "start": 226765,
          "duration": 47952,
          "interval": 999,
          "events": [
            [
              {
                "type": 2,
                "typeName": "motion",
                "locations": [
                  {
                    "x": 0.004184,
                    "y": 0.007463,
                    "width": 0.991667,
                    "height": 0.985185
                  }
                ],
                "regionId": 0
              }
            ],

    …
## <a name="limitations"></a>Ograniczenia
* formatów wejściowych wideo Hello obsługiwane obejmują MP4, MOV i WMV.
* Wykrywanie ruchu jest zoptymalizowana pod kątem wideo nieruchomy tła. Algorytm Hello koncentruje się na zmniejszenie fałszywe alarmy, takie jak zmiany oświetlenia i cieni.
* Niektóre ruchu mogą nie być wykrywane powodu wyzwania tootechnical; np. nocy wizji wideo, półprzezroczyste obiektów i małych obiektów.

## <a name="net-sample-code"></a>.NET przykładowy kod

następujące Hello program pokazuje sposób:

1. Utworzenie elementu zawartości i przesyłanie pliku multimediów do hello zawartości.
2. Utwórz zadanie z zadania wykrywania ruchu na obrazie wideo w zależności od pliku konfiguracji, który zawiera hello następujące ustawienie wstępne json. 
   
        {
          "Version": "1.0",
          "Options": {
            "SensitivityLevel": "medium",
            "FrameSamplingValue": 1,
            "DetectLightChange": "False",
            "MergeTimeThreshold":
            "00:00:02",
            "DetectionZones": [
              [
                {"x": 0, "y": 0},
                {"x": 0.5, "y": 0},
                {"x": 0, "y": 1}
               ],
              [
                {"x": 0.3, "y": 0.3},
                {"x": 0.55, "y": 0.3},
                {"x": 0.8, "y": 0.3},
                {"x": 0.8, "y": 0.55},
                {"x": 0.8, "y": 0.8},
                {"x": 0.55, "y": 0.8},
                {"x": 0.3, "y": 0.8},
                {"x": 0.3, "y": 0.55}
              ]
            ]
          }
        }
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

    namespace VideoMotionDetection
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

                // Run hello VideoMotionDetection job.
                var asset = RunVideoMotionDetectionJob(@"C:\supportFiles\VideoMotionDetection\BigBuckBunny.mp4",
                                            @"C:\supportFiles\VideoMotionDetection\config.json");

                // Download hello job output asset.
                DownloadAsset(asset, @"C:\supportFiles\VideoMotionDetection\Output");
            }

            static IAsset RunVideoMotionDetectionJob(string inputMediaFilePath, string configurationFile)
            {
                // Create an asset and upload hello input media file toostorage.
                IAsset asset = CreateAssetAndUploadSingleFile(inputMediaFilePath,
                    "My Video Motion Detection Input Asset",
                    AssetCreationOptions.None);

                // Declare a new job.
                IJob job = _context.Jobs.Create("My Video Motion Detection Job");

                // Get a reference tooAzure Media Motion Detector.
                string MediaProcessorName = "Azure Media Motion Detector";

                var processor = GetLatestMediaProcessorByName(MediaProcessorName);

                // Read configuration from hello specified file.
                string configuration = File.ReadAllText(configurationFile);

                // Create a task with hello encoding details, using a string preset.
                ITask task = job.Tasks.AddNew("My Video Motion Detection Task",
                    processor,
                    configuration,
                    TaskOptions.None);

                // Specify hello input asset.
                task.InputAssets.Add(asset);

                // Add an output asset toocontain hello results of hello job.
                task.OutputAssets.AddNew("My Video Motion Detectoion Output Asset", AssetCreationOptions.None);

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
[Blog Azure Media Services ruchu detektora](https://azure.microsoft.com/blog/motion-detector-update/)

[Przegląd analiz usługi Azure Media Services](media-services-analytics-overview.md)

[W trakcie analizy multimediów Azure](http://azuremedialabs.azurewebsites.net/demos/Analytics.html)

