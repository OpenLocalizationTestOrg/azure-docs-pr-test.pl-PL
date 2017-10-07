---
title: "aaaRedact krojów z analizy multimediów Azure | Dokumentacja firmy Microsoft"
description: "W tym temacie przedstawiono sposób tooredact skierowany z analizy multimediów Azure."
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: 5b6d8b8c-5f4d-4fef-b3d6-dc22c6b5a0f5
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 07/31/2017
ms.author: juliako;
ms.openlocfilehash: 1f5688a8c6374151c526a9c702b904d8c3e46164
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="redact-faces-with-azure-media-analytics"></a>Redagowanie krojów z analizy multimediów Azure
## <a name="overview"></a>Omówienie
**Azure Media Redactor** jest [analizy multimediów Azure](media-services-analytics-overview.md) procesor multimediów (MP) oferuje skalowalne krój redakcyjne w chmurze hello. Redakcyjne krój umożliwia możesz toomodify wideo w kolejności tooblur kroje wybrane osoby. Możesz toouse hello krój redakcyjne usługi w publicznych scenariusze bezpieczeństwa i nośnika wiadomości. Kilka minut najmniejszym zawiera wiele kroje może zająć godziny tooredact ręcznie, ale z tej usługi hello powierzchni procesu redakcyjne wymaga kilku prostych krokach. Aby uzyskać więcej informacji, zobacz [to](https://azure.microsoft.com/blog/azure-media-redactor/) blogu.

Ten temat zawiera szczegółowe informacje o **Azure Media Redactor** i przedstawia sposób toouse go przy użyciu zestawu SDK usługi Media Services dla platformy .NET.

Witaj **Azure Media Redactor** pakiet administracyjny jest obecnie w przeglądzie. Jest ona dostępna w wszystkich publicznych regiony platformy Azure, a także centrach danych instytucji rządowych Stanów Zjednoczonych i Chinach. Ta wersja zapoznawcza jest obecnie bezpłatnie. 

## <a name="face-redaction-modes"></a>Tryby redakcyjne krój
Działa twarzy redakcyjne wykrywanie kroje w każdej ramce wideo i śledząc krój hello obiekt, zarówno przodu i do tyłu w czasie, tak aby hello tej samej osoby mogą być rozmyciu z innych kątów również. Witaj redakcyjne zautomatyzowanych procesów jest bardzo skomplikowane i nie zawsze 100% żądanego wyniku, z tego powodu analizy multimediów udostępnia kilka sposobów hello toomodify pliku wyjściowego.

Dodanie tooa pełni automatycznym ma dwa przebiegu przepływu pracy, dzięki czemu hello wyboru/dezaktywuje-selection z znaleziono kroje za pomocą listy identyfikatorów. Toomake dowolnego na ramki dostosowań hello MP używa również, plik metadanych w formacie JSON. Ten przepływ pracy jest podzielony na **Analizuj** i **Redact** trybów. Możesz połączyć ze sobą dwa tryby hello w jednym przebiegu uruchomioną obu zadań w jedno zadanie. Ten tryb jest nazywany **nomenklatury**.

### <a name="combined-mode"></a>Tryb połączone
Spowoduje to utworzenie zredagowanym mp4 automatycznie bez żadnych ręcznego wprowadzania.

| Etap | Nazwa pliku | Uwagi |
| --- | --- | --- |
| Wejściowy zasobów |foo.bar |Wideo w formacie WMV, MOV lub MP4 |
| Dane wejściowe konfiguracji |Zadania konfiguracji ustawień wstępnych. |{"version": "1.0", "Opcje": {'mode': "łączyć"}} |
| Dane wyjściowe zasobów |foo_redacted.mp4 |Wideo z rozmycia stosowane |

#### <a name="input-example"></a>Przykład wejściowych:
[Wyświetl ten film](http://ampdemo.azureedge.net/?url=http%3A%2F%2Freferencestream-samplestream.streaming.mediaservices.windows.net%2Fed99001d-72ee-4f91-9fc0-cd530d0adbbc%2FDancing.mp4)

#### <a name="output-example"></a>Przykład danych wyjściowych:
[Wyświetl ten film](http://ampdemo.azureedge.net/?url=http%3A%2F%2Freferencestream-samplestream.streaming.mediaservices.windows.net%2Fc6608001-e5da-429b-9ec8-d69d8f3bfc79%2Fdance_redacted.mp4)

### <a name="analyze-mode"></a>Analizowanie tryb
Witaj **analizowanie** przebieg przepływu pracy Przekaż dwa hello przyjmuje wejście wideo i tworzy plik JSON krój lokalizacji i obrazów jpg każdego wykryto twarzy na obrazie.

| Etap | Nazwa pliku | Uwagi |
| --- | --- | --- |
| Wejściowy zasobów |foo.bar |Wideo w formacie WMV, MPV lub MP4 |
| Dane wejściowe konfiguracji |Zadania konfiguracji ustawień wstępnych. |{"version": "1.0", "Opcje": {'mode': "analizowanie"}} |
| Dane wyjściowe zasobów |foo_annotations.JSON |Adnotacja danych lokalizacji krój w formacie JSON. To mogą je edytować hello użytkownika toomodify hello rozmycia ograniczenia pola. Zobacz poniższy przykład. |
| Dane wyjściowe zasobów |foo_thumb%06d.jpg [foo_thumb000001.jpg, foo_thumb000002.jpg] |Przycięty jpg każdego wykryto krój, gdzie numer hello wskazuje etykiety hello hello powierzchni |

#### <a name="output-example"></a>Przykład danych wyjściowych:

    {
      "version": 1,
      "timescale": 24000,
      "offset": 0,
      "framerate": 23.976,
      "width": 1280,
      "height": 720,
      "fragments": [
        {
          "start": 0,
          "duration": 48048,
          "interval": 1001,
          "events": [
            [],
            [],
            [],
            [],
            [],
            [],
            [],
            [],
            [],
            [],
            [],
            [],
            [],
            [
              {
                "index": 13,
                "id": 1138,
                "x": 0.29537,
                "y": -0.18987,
                "width": 0.36239,
                "height": 0.80335
              },
              {
                "index": 13,
                "id": 2028,
                "x": 0.60427,
                "y": 0.16098,
                "width": 0.26958,
                "height": 0.57943
              }
            ],

    … truncated

### <a name="redact-mode"></a>Redagowanie tryb
drugi przebieg przepływu pracy hello Hello ma większą liczbę wejść, które muszą być połączone w jeden zasobów.

W tym listę identyfikatorów tooblur hello oryginalnego wideo i adnotacje hello JSON. W tym trybie używa hello adnotacje tooapply rozmycia na powitania wejściowy plik wideo.

Witaj dane wyjściowe z przebiegu Analizuj hello nie obejmuje hello oryginalnego wideo. Witaj wideo musi toobe przekazany do zasobów wejściowych hello hello Redact tryb zadania i wybranych jako plik podstawowy hello.

| Etap | Nazwa pliku | Uwagi |
| --- | --- | --- |
| Wejściowy zasobów |foo.bar |Wideo w formacie WMV, MPV lub MP4. Taka sama jak w kroku 1 wideo. |
| Wejściowy zasobów |foo_annotations.JSON |Plik metadanych adnotacje z fazy, bez modyfikacji opcjonalne. |
| Wejściowy zasobów |foo_IDList.txt (opcjonalnie) |Lista krój tooredact identyfikatorów rozdzielonych opcjonalne nowy wiersz. Jeśli pole pozostanie puste, to rozmywa wszystkich powierzchni. |
| Dane wejściowe konfiguracji |Zadania konfiguracji ustawień wstępnych. |{"version": "1.0", "Opcje": {'mode': "redagowanie"}} |
| Dane wyjściowe zasobów |foo_redacted.mp4 |Wideo z rozmycia stosowane w oparciu adnotacji |

#### <a name="example-output"></a>Przykładowe dane wyjściowe
Jest to hello IDList z jednego Identyfikatora zaznaczone dane wyjściowe.

[Wyświetl ten film](http://ampdemo.azureedge.net/?url=http%3A%2F%2Freferencestream-samplestream.streaming.mediaservices.windows.net%2Fad6e24a2-4f9c-46ee-9fa7-bf05e20d19ac%2Fdance_redacted1.mp4)

Przykład foo_IDList.txt
 
     1
     2
     3

## <a name="blur-types"></a>Rozmywa typów

W hello **nomenklatury** lub **Redact** trybie 5 tryby różnych rozmycia są dostępne za pośrednictwem wejściowych konfiguracji JSON hello: **małej**, **Med**, **Wysokiej**, **debugowania**, i **czarne**. Domyślnie **Med** jest używany.

Można okaże się, że przykłady hello rozmycia typy poniżej.

### <a name="example-json"></a>Przykład JSON:

    {'version':'1.0', 'options': {'Mode': 'Combined', 'BlurType': 'High'}}

#### <a name="low"></a>Niska

![Niska](./media/media-services-face-redaction/blur1.png)
 
#### <a name="med"></a>MED

![MED](./media/media-services-face-redaction/blur2.png)

#### <a name="high"></a>Wysoka

![Wysoka](./media/media-services-face-redaction/blur3.png)

#### <a name="debug"></a>Debugowanie

![Debugowanie](./media/media-services-face-redaction/blur4.png)

#### <a name="black"></a>Czarny

![Czarny](./media/media-services-face-redaction/blur5.png)

## <a name="elements-of-hello-output-json-file"></a>Elementy hello pliku wyjściowego w formacie JSON

Hello redakcyjne pakiet administracyjny zawiera wysokiej precyzji krój lokalizacji wykrywania i śledzenia, która wykrywa się too64 kroje ludzkich w ramce wideo. Kroje czołowego Podaj hello uzyskać jak najlepsze rezultaty, podczas boczne i małych powierzchni (mniej niż lub równa too24x24 pikseli) są trudne.

[!INCLUDE [media-services-analytics-output-json](../../includes/media-services-analytics-output-json.md)]

## <a name="net-sample-code"></a>.NET przykładowy kod

następujące Hello program pokazuje sposób:

1. Utworzenie elementu zawartości i przesyłanie pliku multimediów do hello zawartości.
2. Utwórz zadanie z zadaniem redakcyjne krój oparty na pliku konfiguracji, który zawiera hello następujące ustawienie wstępne json. 
   
        {'version':'1.0', 'options': {'mode':'combined'}}
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

    namespace FaceRedaction
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

            // Run hello FaceRedaction job.
            var asset = RunFaceRedactionJob(@"C:\supportFiles\FaceRedaction\SomeFootage.mp4",
                        @"C:\supportFiles\FaceRedaction\config.json");

            // Download hello job output asset.
            DownloadAsset(asset, @"C:\supportFiles\FaceRedaction\Output");
        }

        static IAsset RunFaceRedactionJob(string inputMediaFilePath, string configurationFile)
        {
            // Create an asset and upload hello input media file toostorage.
            IAsset asset = CreateAssetAndUploadSingleFile(inputMediaFilePath,
            "My Face Redaction Input Asset",
            AssetCreationOptions.None);

            // Declare a new job.
            IJob job = _context.Jobs.Create("My Face Redaction Job");

            // Get a reference tooAzure Media Redactor.
            string MediaProcessorName = "Azure Media Redactor";

            var processor = GetLatestMediaProcessorByName(MediaProcessorName);

            // Read configuration from hello specified file.
            string configuration = File.ReadAllText(configurationFile);

            // Create a task with hello encoding details, using a string preset.
            ITask task = job.Tasks.AddNew("My Face Redaction Task",
            processor,
            configuration,
            TaskOptions.None);

            // Specify hello input asset.
            task.InputAssets.Add(asset);

            // Add an output asset toocontain hello results of hello job.
            task.OutputAssets.AddNew("My Face Redaction Output Asset", AssetCreationOptions.None);

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

## <a name="next-steps"></a>Następne kroki

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Przekazywanie opinii
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="related-links"></a>Powiązane linki
[Przegląd analiz usługi Azure Media Services](media-services-analytics-overview.md)

[W trakcie analizy multimediów Azure](http://azuremedialabs.azurewebsites.net/demos/Analytics.html)

