---
title: "Azure Media Encoder Standard tooauto aaaUse-Generowanie drabinę szybkości transmisji bitów | Dokumentacja firmy Microsoft"
description: "W tym temacie przedstawiono sposób tooauto Media Encoder Standard (rynkowej) toouse-Generowanie drabinę szybkości transmisji bitów, na podstawie hello rozdzielczość i szybkość transmisji bitów. Hello rozdzielczość i szybkość transmisji bitów nigdy nie zostanie przekroczony. Na przykład jeśli wejściowy hello jest 720p w 3 MB/s, dane wyjściowe będą pozostawać w najlepszym 720p i rozpocznie stawkami niższa niż 3 MB/s."
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: 63ed95da-1b82-44b0-b8ff-eebd535bc5c7
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: juliako
ms.openlocfilehash: 5437f54ac28c42ddd4f9d1986549d6da6261c5da
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
#  <a name="use-azure-media-encoder-standard-tooauto-generate-a-bitrate-ladder"></a>Użyj usługi Azure Media Encoder Standard tooauto-Generowanie drabinę szybkości transmisji bitów

## <a name="overview"></a>Omówienie

W tym temacie przedstawiono sposób tooauto Media Encoder Standard (rynkowej) toouse-Generowanie drabinę szybkości transmisji bitów (pary rozpoznawania szybkości transmisji bitów) na podstawie hello rozdzielczość i szybkość transmisji bitów. Witaj automatycznie generowanej ustawienie wstępne nigdy nie przekroczy hello wejściowych rozdzielczość i szybkość transmisji bitów. Na przykład jeśli wejściowy hello jest 720p w 3 MB/s, dane wyjściowe będą pozostawać w najlepszym 720p i rozpocznie stawkami niższa niż 3 MB/s.

### <a name="encoding-for-streaming-only"></a>Kodowanie tylko przesyłania strumieniowego

Jeśli tooencode zamierzeniu źródła wideo tylko w przypadku przesyłania strumieniowego, możesz powinny używać "Adaptacyjne przesyłanie strumieniowe" hello wstępnie podczas tworzenia zadania kodowania. Korzystając z hello **adaptacyjne przesyłanie strumieniowe** zdefiniowane, hello rynkowej kodera sposób inteligentny będzie cap drabinę szybkości transmisji bitów. Jednak nie będzie możliwe toocontrol hello kodowanie kosztów, ponieważ usługa hello Określa, ile toouse warstwy i jakie rozdzielczości. Zawiera przykłady warstw wyjściowego utworzonego przez rynkowej wyniku kodowania z hello **adaptacyjne przesyłanie strumieniowe** ustawień wstępnych. na końcu hello w tym temacie. Witaj output zasobów będzie zawierać pliki MP4, gdzie audio i wideo nie jest przeplatana.

### <a name="encoding-for-streaming-and-progressive-download"></a>Kodowanie używane do przesyłania strumieniowego i pobierania progresywnego

Jeśli tooencode zamierzeniu źródłowy plik wideo do przesyłania strumieniowego oraz pliki MP4 tooproduce pobierania progresywnego, możesz powinny używać hello "Zawartości adaptacyjną wielu szybkości transmisji bitów MP4" wstępnie podczas tworzenia zadania kodowania. Korzystając z hello **zawartości adaptacyjną wielu MP4 szybkości transmisji bitów** zdefiniowane, koder rynkowej hello zastosuje hello samej logiki kodowania, jak powyżej, ale teraz zawartości wyjściowej hello będzie zawierać MP4 pliki w przypadku, gdy audio i wideo są przeplotem. Można użyć jednego z tych plików MP4 (na przykład hello najwyższej szybkości transmisji bitów wersji) jako plik pobierania progresywnego.

## <a id="encoding_with_dotnet"></a>Kodowanie w usłudze Media Services zestawu .NET SDK

Poniższy przykład kodu Hello używa hello tooperform .NET SDK usługi Media Services następujące zadania:

- Utwórz zadania kodowania.
- Pobiera koder Media Encoder Standard toohello odwołania.
- Dodaj zadania kodowania toohello zadań i określ toouse hello **adaptacyjne przesyłanie strumieniowe** wstępnie zdefiniowane. 
- Tworzenie zasobu danych wyjściowych, który będzie zawierać hello zakodowane zasobów.
- Dodaj postęp zadania hello toocheck zdarzeń programu obsługi.
- Prześlij zadanie hello.

#### <a name="create-and-configure-a-visual-studio-project"></a>Tworzenie i konfigurowanie projektu programu Visual Studio

Konfigurowanie środowiska projektowego i wypełnić plik app.config hello o informacje dotyczące połączenia, zgodnie z opisem w [tworzenia usługi Media Services z platformą .NET](media-services-dotnet-how-to-use.md). 

#### <a name="example"></a>Przykład

    using System;
    using System.Configuration;
    using System.Linq;
    using Microsoft.WindowsAzure.MediaServices.Client;
    using System.Threading;

    namespace AdaptiveStreamingMESPresest
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

            // Create a task
            ITask task = job.Tasks.AddNew("Media Encoder Standard encoding task",
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

## <a id="output"></a>Dane wyjściowe

W tej sekcji przedstawiono trzy przykłady warstw wyjściowego utworzonego przez rynkowej wyniku kodowania z hello **adaptacyjne przesyłanie strumieniowe** wstępnie zdefiniowane. 

### <a name="example-1"></a>Przykład 1
Źródło o wysokość "1080" i "29.970" szybkość klatek tworzy 6 warstwy wideo:

|Warstwy|Wysokość|Szerokość|Bitrate(Kbps)|
|---|---|---|---|
|1|1080|1920|6780|
|2|720|1280|3520|
|3|540|960|2210|
|4|360|640|1150|
|5|270|480|720|
|6|180|320|380|

### <a name="example-2"></a>Przykład 2
Źródło o wysokość "720" i "23.970" szybkość klatek tworzy 5 warstwy wideo:

|Warstwy|Wysokość|Szerokość|Bitrate(Kbps)|
|---|---|---|---|
|1|720|1280|2940|
|2|540|960|1850|
|3|360|640|960|
|4|270|480|600|
|5|180|320|320|

### <a name="example-3"></a>Przykład 3
Źródło o wysokość "360" i "29.970" szybkość klatek tworzy 3 warstwy wideo:

|Warstwy|Wysokość|Szerokość|Bitrate(Kbps)|
|---|---|---|---|
|1|360|640|700|
|2|270|480|440|
|3|180|320|230|
## <a name="media-services-learning-paths"></a>Ścieżki szkoleniowe dotyczące usługi Media Services
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Przekazywanie opinii
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="see-also"></a>Zobacz też
[Usługi multimediów kodowania — omówienie](media-services-encode-asset.md)

