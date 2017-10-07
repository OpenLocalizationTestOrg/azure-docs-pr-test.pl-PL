---
title: "aaaHyperlapse plików multimedialnych na pliki z usługi Azure Media Hyperlapse | Dokumentacja firmy Microsoft"
description: "Azure Media Hyperlapse tworzy smooth czas, jaki upłynął wideo z pierwszą osobą lub akcji aparatu zawartości. W tym temacie przedstawiono sposób toouse indeksatora nośnika."
services: media-services
documentationcenter: 
author: asolanki
manager: johndeu
editor: 
ms.assetid: 37d54db6-9cf3-4ae9-b3c6-0d29c744e965
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 03/02/2017
ms.author: adsolank
ms.openlocfilehash: 85bb07206d0ca2f5b2fd0767e6ed4904195d3ab6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="hyperlapse-media-files-with-azure-media-hyperlapse"></a>Plikach multimedialnych przyspieszonych ujęć poklatkowych za pomocą usługi Azure Media Hyperlapse
Azure Media Hyperlapse jest nośnik procesora (MP) tworzącą smooth czas, jaki upłynął wideo z pierwszą osobą lub akcji aparatu zawartości.  Witaj równorzędny oparte na chmurze za[desktop Pro przyspieszonych ujęć poklatkowych i opartych na telefon komórkowy przyspieszonych ujęć poklatkowych Microsoft Research](http://aka.ms/hyperlapse), Hyperlapse firmy Microsoft dla usługi Azure Media Services używa hello ogromną skalę hello Azure Media Services nośnika Przetwarzanie toohorizontally platformy skalowanie i parallelize zbiorczego przyspieszonych ujęć poklatkowych przetwarzania.

> [!IMPORTANT]
> Microsoft Hyperlapse jest zaprojektowana toowork najlepiej na pierwszą osobą zawartości za pomocą przenoszenia aparatu.  Mimo że nadal kamery może nadal działać, nie można zagwarantować hello wydajności i jakości hello Azure Media przyspieszonych ujęć poklatkowych nośnika procesora dla innych typów zawartości.  więcej informacji na temat Hyperlapse firmy Microsoft dla usługi Azure Media Services toolearn i wyświetlić niektóre przykładowe filmy, zapoznaj się z hello [wprowadzające wpis w blogu](http://aka.ms/azurehyperlapseblog) z publicznej wersji zapoznawczej hello.
> 
> 

Azure Media Hyperlapse zadania przyjmuje jako dane wejściowe plik MP4, MOV lub WMV zasobów oraz pliku konfiguracji, który określa, które ramki wideo powinny być czas, jaki upłynął i szybkość toowhat (np. pierwszych 10 000 ramek, x 2).  dane wyjściowe Hello jest stabilnych i czas, jaki upłynął dobór hello wejściowy plik wideo.

Najnowsze aktualizacje hello Azure Media Hyperlapse, zobacz [blogi Media Services](https://azure.microsoft.com/blog/topics/media-services/).

## <a name="hyperlapse-an-asset"></a>Przyspieszonych ujęć poklatkowych zasobów
Najpierw należy tooupload Twojego tooAzure żądanego pliku wejściowego usługi Media Services.  więcej informacji o toolearn hello pojęcia związane z przekazywanie i zarządzania zawartością, przeczytaj hello [zarządzania zawartością artykułu](media-services-portal-vod-get-started.md).

### <a id="configuration"></a>Ustawienie konfiguracji dla przyspieszonych ujęć poklatkowych
Gdy zawartość jest na koncie usługi Media Services, należy tooconstruct ustawień konfiguracji.  Witaj w poniższej tabeli opisano hello określone przez użytkownika pola:

| Pole | Opis |
| --- | --- |
| StartFrame |ramki Hello, na które Microsoft Hyperlapse hello powinny one zacząć przetwarzania. |
| NumFrames |Liczba Hello tooprocess ramki |
| Szybkość |współczynnik Hello, z których toospeed się hello wejściowy plik wideo. |

Witaj poniżej przedstawiono przykładowy plik konfiguracji zgodność w pliku XML i JSON:

**Ustawienie wstępne XML:**

    <?xml version="1.0" encoding="utf-16"?>
    <Preset xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:xsd="http://www.w3.org/2001/XMLSchema" Version="1.0" xmlns="http://www.windowsazure.com/media/encoding/Preset/2014/03">
        <Sources>
            <Source StartFrame="0" NumFrames="10000" />
        </Sources>
        <Options>
            <Speed>12</Speed>
        </Options>
    </Preset>

**Ustawienie wstępne JSON:**

    {
        "Version":1.0,
        "Sources": [
            {
                "StartFrame":0,
                "NumFrames":2147483647
            }
        ],
        "Options": {
            "Speed":1,
            "Stabilize":false
        }
    }

### <a id="sample_code"></a>Microsoft Hyperlapse z hello AMS .NET SDK
Witaj następująca metoda przekazuje plik nośnika jako zasób i tworzy zadanie z hello Azure Media przyspieszonych ujęć poklatkowych nośnika procesora.

> [!NOTE]
> CloudMediaContext ma już w zakresie o nazwie hello "context" toowork tego kodu.  więcej informacji na temat tego, odczytu hello toolearn [zarządzania zawartością artykułu](media-services-dotnet-get-started.md).
> 
> [!NOTE]
> argument ciągu Hello "hyperConfig" jest oczekiwany toobe konfiguracji zgodność ustawień w formacie JSON i XML zgodnie z powyższym opisem.
> 
> 

        static bool RunHyperlapseJob(string input, string output, string hyperConfig)
        {
            // create asset with input file
            IAsset asset = context
            .Assets
            .CreateAssetAndUploadSingleFile(input, "My Hyperlapse Input", AssetCreationOptions.None);

            // grab instances of Azure Media Hyperlapse MP
            IMediaProcessor mp = context
            .MediaProcessors
            .GetLatestMediaProcessorByName("Azure Media Hyperlapse");

            // create Job with Hyperlapse task
            IJob job = context
            .Jobs
            .Create(String.Format("Hyperlapse {0}", input));

            if (String.IsNullOrEmpty(hyperConfig))
            {
            // config cannot be empty
            return false;
            }

            hyperConfig = File.ReadAllText(hyperConfig);

            ITask hyperlapseTask = job.Tasks.AddNew("Hyperlapse task",
            mp,
            hyperConfig,
            TaskOptions.None);
            hyperlapseTask.InputAssets.Add(asset);
            hyperlapseTask.OutputAssets.AddNew("Hyperlapse output",
            AssetCreationOptions.None);

            job.Submit();

            // Create progress printing and querying tasks
            Task progressPrintTask = new Task(() =>
            {

            IJob jobQuery = null;
            do
            {
                var progressContext = context;
                jobQuery = progressContext.Jobs
                .Where(j => j.Id == job.Id)
                .First();
                Console.WriteLine(string.Format("{0}\t{1}\t{2}",
                DateTime.Now,
                jobQuery.State,
                jobQuery.Tasks[0].Progress));
                Thread.Sleep(10000);
            }
            while (jobQuery.State != JobState.Finished &&
                                   jobQuery.State != JobState.Error &&
                                   jobQuery.State != JobState.Canceled);
                });
                
            progressPrintTask.Start();

            Task progressJobTask = job.GetExecutionProgressTask(
                                                 CancellationToken.None);
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
                return false;                  
            }

        DownloadAsset(job.OutputMediaAssets.First(), output);
        return true;
    }

    static void DownloadAsset(IAsset asset, string outputDirectory)
    {
        foreach (IAssetFile file in asset.AssetFiles)
        {
            file.Download(Path.Combine(outputDirectory, file.Name));
        }
    }


    static IAsset CreateAssetAndUploadSingleFile(string filePath, string assetName, AssetCreationOptions options)
    {
        IAsset asset = context.Assets.Create(assetName, options);

        var assetFile = asset.AssetFiles.Create(Path.GetFileName(filePath));
        assetFile.Upload(filePath);

        return asset;
    }

    static IMediaProcessor GetLatestMediaProcessorByName(string mediaProcessorName)
    {
        var processor = context.MediaProcessors
        .Where(p => p.Name == mediaProcessorName)
        .ToList()
        .OrderBy(p => new Version(p.Version))
        .LastOrDefault();

        if (processor == null)
            throw new ArgumentException(string.Format("Unknown media processor",
                                                       mediaProcessorName));

        return processor;
    }

### <a id="file_types"></a>Obsługiwane typy plików
* MP4
* MOV
* WMV

## <a name="media-services-learning-paths"></a>Ścieżki szkoleniowe dotyczące usługi Media Services
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Przekazywanie opinii
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="related-links"></a>Powiązane linki
[Przegląd analiz usługi Azure Media Services](media-services-analytics-overview.md)

[W trakcie analizy multimediów Azure](http://azuremedialabs.azurewebsites.net/demos/Analytics.html)

