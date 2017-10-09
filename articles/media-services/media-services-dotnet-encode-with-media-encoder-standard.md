---
title: "element zawartości przy użyciu platformy .NET Media Encoder Standard aaaEncode | Dokumentacja firmy Microsoft"
description: "W tym temacie przedstawiono sposób toouse .NET tooencode zasobów przy użyciu Media Encoder standardowa."
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: 03431b64-5518-478a-a1c2-1de345999274
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/31/2017
ms.author: juliako;anilmur
ms.openlocfilehash: 25e274c3b67168f4afc8b8ab04af2d654c9dd6e4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="encode-an-asset-with-media-encoder-standard-using-net"></a>Kodowanie elementu zawartości z standardu Media Encoder Standard przy użyciu platformy .NET
Zadania kodowania są jednym z najbardziej typowych operacji przetwarzania hello w usłudze Media Services. Utworzysz kodowania plików multimedialnych tooconvert zadań z jednego tooanother kodowania. Podczas kodowania, można użyć hello wbudowanych Media Encoder Media Services. Można również użyć kodera świadczonych przez partnera usługi Media Services; kodery innych firm są dostępne za pośrednictwem hello Azure Marketplace. 

W tym temacie przedstawiono sposób toouse .NET tooencode zasobów z Media Encoder Standard (rynkowej). Media Encoder Standard została skonfigurowana przy użyciu jednego ustawień kodera hello opisane [tutaj](http://go.microsoft.com/fwlink/?linkid=618336&clcid=0x409).

Zaleca się tooalways kodowanie plików źródłowych do adaptacyjnej szybkości bitowej MP4 zestawu, a następnie wykonać konwersję hello zestaw toohello pożądany format przy użyciu hello [dynamicznego tworzenia pakietów](media-services-dynamic-packaging-overview.md). 

Jeśli dane wyjściowe zawartości jest szyfrowany w magazynie, musisz skonfigurować zasady dostarczania elementu zawartości. Aby uzyskać więcej informacji, zobacz [Konfigurowanie zasad dostarczania elementów zawartości](media-services-dotnet-configure-asset-delivery-policy.md).

> [!NOTE]
> Rynkowej i tworzy plik wyjściowy z nazwy, która zawiera hello pierwsze 32 znaki hello nazwa pliku wejściowego. Nazwa Hello jest oparta na co została określona w pliku predefiniowanych hello. Na przykład, "FileName": "{nazwę bazową} _ {Index} {rozszerzenia}". {Nazwę bazową} zastępuje hello pierwsze 32 znaki hello nazwa pliku wejściowego.
> 
> 

### <a name="mes-formats"></a>Formaty rynkowej
[Koderów-dekoderów i formaty](media-services-media-encoder-standard-formats.md)

### <a name="mes-presets"></a>Ustawienia wstępne usługi MES
Media Encoder Standard została skonfigurowana przy użyciu jednego ustawień kodera hello opisane [tutaj](http://go.microsoft.com/fwlink/?linkid=618336&clcid=0x409).

### <a name="input-and-output-metadata"></a>Wejście i wyjście metadanych
Podczas kodowania zasób wejściowy (lub zasoby), za pomocą rynkowej, możesz uzyskać zawartości wyjściowej na powitania ukończenie tego kodowania zadań. zawartości wyjściowej Hello zawiera wideo, audio, miniatur, manifest itp oparte na powitania ustawienie kodowania, które można użyć.

zawartości wyjściowej Hello zawiera także plik o metadane dotyczące zasobu wejściowego hello. Hello nazwę pliku XML metadanych hello ma hello następującego formatu: < asset_id > _metadata.xml (na przykład 41114ad3-eb5e - 4c d 57 8 92-5354e2b7d4a4_metadata.xml), gdzie < asset_id > jest wartością IDśrodkaTrwałego hello hello zasobów wejściowych. Hello schematu wejściowego XML metadanych opisano [tutaj](media-services-input-metadata-schema.md).

zawartości wyjściowej Hello zawiera także plik o metadane dotyczące zawartości wyjściowej hello. Witaj nazwę pliku XML metadanych hello ma hello następującego formatu: < source_file_name > _manifest.xml (na przykład BigBuckBunny_manifest.xml). Schemat Hello opisano XML metadanych dane wyjściowe [tutaj](media-services-output-metadata-schema.md).

Jeśli chcesz tooexamine albo hello dwóch plików metadanych, można tworzyć lokalizatora SAS i Pobierz hello pliku tooyour lokalnego komputera. Przykład sposobu toocreate lokalizatora SAS i pobieranie plików Using hello usługi Media Services można znaleźć rozszerzenia zestawu .NET SDK.

## <a name="download-sample"></a>Pobieranie przykładu
Możesz pobrać i uruchom przykład pokazujący sposób tooencode z rynkowej z [tutaj](https://azure.microsoft.com/documentation/samples/media-services-dotnet-on-demand-encoding-with-media-encoder-standard/).

## <a name="net-sample-code"></a>.NET przykładowy kod

Poniższy przykład kodu Hello używa hello tooperform .NET SDK usługi Media Services następujące zadania:

* Utwórz zadania kodowania.
* Pobiera koder Media Encoder Standard toohello odwołania.
* Określ toouse hello [adaptacyjne przesyłanie strumieniowe](media-services-autogen-bitrate-ladder-with-mes.md) wstępnie zdefiniowane. 
* Dodaj jednego zadania kodowania toohello zadań. 
* Określ dane wejściowe hello zakodowane toobe zasobów.
* Tworzenie zasobu danych wyjściowych, który będzie zawierać hello zakodowane zasobów.
* Dodaj postęp zadania hello toocheck zdarzeń programu obsługi.
* Prześlij zadanie hello.

#### <a name="create-and-configure-a-visual-studio-project"></a>Tworzenie i konfigurowanie projektu programu Visual Studio

Konfigurowanie środowiska projektowego i wypełnić plik app.config hello o informacje dotyczące połączenia, zgodnie z opisem w [tworzenia usługi Media Services z platformą .NET](media-services-dotnet-how-to-use.md). 

#### <a name="example"></a>Przykład 

        using System;
        using System.Linq;
        using System.Configuration;
        using System.IO;
        using System.Threading;
        using Microsoft.WindowsAzure.MediaServices.Client;

        namespace MediaEncoderStandardSample
        {
            class Program
            {
                private static readonly string _AADTenantDomain =
                    ConfigurationManager.AppSettings["AADTenantDomain"];
                private static readonly string _RESTAPIEndpoint =
                    ConfigurationManager.AppSettings["MediaServiceRESTAPIEndpoint"];

                // Field for service context.
                private static CloudMediaContext _context = null;

                private static readonly string _supportFiles =
                    Path.GetFullPath(@"../..\Media");

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

                    // Create a task with hello encoding details, using a string preset.
                    // In this case "Adaptive Streaming" preset is used.
                    ITask task = job.Tasks.AddNew("My encoding task",
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

## <a name="media-services-learning-paths"></a>Ścieżki szkoleniowe dotyczące usługi Media Services
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Przekazywanie opinii
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="next-steps"></a>Następne kroki
[Jak miniatur toogenerate z platformą .NET przy użyciu standardu Media Encoder Standard](media-services-dotnet-generate-thumbnail-with-mes.md)
[usługi Media kodowanie — omówienie](media-services-encode-asset.md)

