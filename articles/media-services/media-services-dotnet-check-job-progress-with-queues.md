---
title: "aaaUse kolejek Azure magazynu toomonitor Media Services zadania powiadomienia z platformą .NET | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toomonitor magazynu kolejek Azure toouse Media Services zadania powiadomienia. Przykładowy kod Hello jest napisany w języku C# i używa hello SDK usługi Media Services dla platformy .NET."
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: f535d0b5-f86c-465f-81c6-177f4f490987
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 08/14/2017
ms.author: juliako
ms.openlocfilehash: e4068621ada00d763133dc0d01cfc666b53f8b1b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-queue-storage-toomonitor-media-services-job-notifications-with-net"></a>Azure kolejki magazynu toomonitor Media Services zadania powiadomienia za pomocą platformy .NET
Po uruchomieniu zadania kodowania, często wymagają postępu zadania tootrack sposób. Można skonfigurować powiadomienia toodeliver Media Services zbyt[magazynu kolejek Azure](../storage/storage-dotnet-how-to-use-queues.md). Można monitorować postęp zadania pobierania powiadomień z hello magazynu kolejek. 

Komunikaty dostarczone tooQueue magazynu można uzyskać z dowolnego miejsca w hello world. Hello architektura wiadomości kolejki magazynu jest niezawodnych i wysokiej skalowalności. Sondowanie magazynu kolejek wiadomości jest zalecane w przypadku innych metod.

Jednego typowych scenariuszy nasłuchiwania powiadomień usługi tooMedia Jeśli tworzysz system zarządzania zawartością, która musi tooperform ukończeniu (na przykład tootrigger hello następnego kroku w przepływie pracy lub toopublish niektóre dodatkowe zadania po zadania kodowania zawartość).

W tym temacie przedstawiono sposób tooget powiadomień wiadomości z kolejki magazynu.  

## <a name="considerations"></a>Zagadnienia do rozważenia
Podczas tworzenia aplikacji usługi Media Services, które używać magazynu kolejek, należy wziąć pod uwagę następujące hello:

* Magazyn kolejek nie ma gwarancji, najpierw w pierwszym poza dostarczania uporządkowanego (FIFO). Aby uzyskać więcej informacji, zobacz [kolejek Azure i porównać kolejki magistrali usług Azure i Contrasted](https://msdn.microsoft.com/library/azure/hh767287.aspx).
* Magazyn kolejek nie jest usługi wypychania. Masz toopoll hello kolejki.
* Może mieć dowolną liczbę kolejek. Aby uzyskać więcej informacji, zobacz [interfejsu API REST usługi kolejki](https://docs.microsoft.com/rest/api/storageservices/Queue-Service-REST-API).
* Magazyn kolejek ma pewnych ograniczeń i toobe charakterystykę znane. Te ustawienia zostały opisane w [kolejek Azure i porównać kolejki magistrali usług Azure i Contrasted](https://docs.microsoft.com/azure/service-bus-messaging/service-bus-azure-and-service-bus-queues-compared-contrasted).

## <a name="net-code-example"></a>Przykład kodu platformy .NET

przykład Witaj kodu w tej sekcji hello następujące:

1. Definiuje hello **EncodingJobMessage** klasa, która mapuje toohello format powiadomienia w wiadomości. Kod Hello deserializuje komunikatów odebranych z kolejki hello na obiekty hello **EncodingJobMessage** typu.
2. Ładunki hello Media Services oraz informacji o koncie magazynu w pliku app.config hello. Przykładowy kod Hello używa tego hello toocreate informacji **CloudMediaContext** i **CloudQueue** obiektów.
3. Tworzy kolejkę hello, która odbiera powiadomienia dotyczące hello zadania kodowania.
4. Tworzy hello powiadomień, się, że punkt końcowy, który jest mapowany toohello kolejki.
5. Dołącza hello powiadomienia punktu końcowego toohello zadania, a następnie przesyła hello zadania kodowania. Może mieć wiele zadania tooa dołączony punktów końcowych powiadomień.
6. Przekazuje **NotificationJobState.FinalStatesOnly** toohello **AddNew** metody. (W tym przykładzie opiszemy tylko Stany końcowego przetwarzania zadania hello.)

        job.JobNotificationSubscriptions.AddNew(NotificationJobState.FinalStatesOnly, _notificationEndPoint);
7. W przypadku przekazania **NotificationJobState.All**, Pobierz wszystkie następujące powiadomienia o zmianie stanu hello: umieszczonych w kolejce, zaplanowane przetwarzania i gotowe. Jak wspomniano wcześniej, magazyn kolejek gwarantuje jednak uporządkowanego dostarczenia. komunikaty tooorder, należy użyć hello **sygnatury czasowej** właściwości (zdefiniowany na powitania **EncodingJobMessage** typu w poniższym przykładzie hello). Możliwe są zduplikowane wiadomości. toocheck duplikatów, użyj hello **właściwość ETag** (zdefiniowany na powitania **EncodingJobMessage** typu). Istnieje również możliwość, że niektóre powiadomienia o zmianie stanu uzyskać pominięte.
8. Czeka na powitania zadania tooget toohello Zakończono stanu, sprawdzając kolejki hello co 10 sekund. Usuwa wiadomości po zostały przetworzone.
9. Usuwa kolejkę hello i punktu końcowego powiadomienia hello.

> [!NOTE]
> Witaj toomonitor zalecaną metodą, stan zadania to nasłuchiwania toonotification wiadomości, jak pokazano w hello poniższy przykład.
>
> Alternatywnie można sprawdzić stanu zadania za pomocą hello **IJob.State** właściwości.  Komunikat z powiadomieniem o zakończeniu zadania może pojawić się przed stanu hello na **IJob** ustawiono zbyt**Zakończono**. Witaj **IJob.State** właściwość odzwierciedla stan dokładne hello z niewielkie opóźnienie.
>
>

### <a name="create-and-configure-a-visual-studio-project"></a>Tworzenie i konfigurowanie projektu programu Visual Studio

1. Konfigurowanie środowiska projektowego i wypełnić plik app.config hello o informacje dotyczące połączenia, zgodnie z opisem w [tworzenia usługi Media Services z platformą .NET](media-services-dotnet-how-to-use.md). 
2. Utwórz nowy folder (folder może być dowolnym miejscu na dysku lokalnym) i skopiuj plik plik MP4 tooencode i strumienia, lub pobrać progresywnie. W tym przykładzie ścieżki "C:\Media" hello jest używany.

### <a name="code"></a>Kod

```
using System;
using System.Linq;
using System.Configuration;
using System.IO;
using System.Threading;
using System.Collections.Generic;
using Microsoft.WindowsAzure.MediaServices.Client;
using Microsoft.WindowsAzure.Storage;
using Microsoft.WindowsAzure.Storage.Queue;
using System.Runtime.Serialization.Json;

namespace JobNotification
{
    public class EncodingJobMessage
    {
        // MessageVersion is used for version control.
        public String MessageVersion { get; set; }

        // Type of hello event. Valid values are
        // JobStateChange and NotificationEndpointRegistration.
        public String EventType { get; set; }

        // ETag is used toohelp hello customer detect if
        // hello message is a duplicate of another message previously sent.
        public String ETag { get; set; }

        // Time of occurrence of hello event.
        public String TimeStamp { get; set; }

        // Collection of values specific toohello event.

        // For hello JobStateChange event hello values are:
        //     JobId - Id of hello Job that triggered hello notification.
        //     NewState- hello new state of hello Job. Valid values are:
        //          Scheduled, Processing, Canceling, Cancelled, Error, Finished
        //     OldState- hello old state of hello Job. Valid values are:
        //          Scheduled, Processing, Canceling, Cancelled, Error, Finished

        // For hello NotificationEndpointRegistration event hello values are:
        //     NotificationEndpointId- Id of hello NotificationEndpoint
        //          that triggered hello notification.
        //     State- hello state of hello Endpoint.
        //          Valid values are: Registered and Unregistered.

        public IDictionary<string, object> Properties { get; set; }
    }

    class Program
    {

        // Read values from hello App.config file.
        private static readonly string _AADTenantDomain =
            ConfigurationManager.AppSettings["AADTenantDomain"];
        private static readonly string _RESTAPIEndpoint =
            ConfigurationManager.AppSettings["MediaServiceRESTAPIEndpoint"];
        private static readonly string _StorageConnectionString = 
            ConfigurationManager.AppSettings["StorageConnectionString"];

        private static CloudMediaContext _context = null;
        private static CloudQueue _queue = null;
        private static INotificationEndPoint _notificationEndPoint = null;

        private static readonly string _singleInputMp4Path =
            Path.GetFullPath(@"C:\Media\BigBuckBunny.mp4");

        static void Main(string[] args)
        {
            string endPointAddress = Guid.NewGuid().ToString();

            // Create hello context.
            var tokenCredentials = new AzureAdTokenCredentials(_AADTenantDomain, AzureEnvironments.AzureCloudEnvironment);
            var tokenProvider = new AzureAdTokenProvider(tokenCredentials);

            _context = new CloudMediaContext(new Uri(_RESTAPIEndpoint), tokenProvider);

            // Create hello queue that will be receiving hello notification messages.
            _queue = CreateQueue(_StorageConnectionString, endPointAddress);

            // Create hello notification point that is mapped toohello queue.
            _notificationEndPoint =
                    _context.NotificationEndPoints.Create(
                    Guid.NewGuid().ToString(), NotificationEndPointType.AzureQueue, endPointAddress);


            if (_notificationEndPoint != null)
            {
                IJob job = SubmitEncodingJobWithNotificationEndPoint(_singleInputMp4Path);
                WaitForJobToReachedFinishedState(job.Id);
            }

            // Clean up.
            _queue.Delete();
            _notificationEndPoint.Delete();
        }


        static public CloudQueue CreateQueue(string storageAccountConnectionString, string endPointAddress)
        {
            CloudStorageAccount storageAccount = CloudStorageAccount.Parse(storageAccountConnectionString);

            // Create hello queue client
            CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();

            // Retrieve a reference tooa queue
            CloudQueue queue = queueClient.GetQueueReference(endPointAddress);

            // Create hello queue if it doesn't already exist
            queue.CreateIfNotExists();

            return queue;
        }


        public static IJob SubmitEncodingJobWithNotificationEndPoint(string inputMediaFilePath)
        {
            // Declare a new job.
            IJob job = _context.Jobs.Create("My MP4 tooSmooth Streaming encoding job");

            //Create an encrypted asset and upload hello mp4.
            IAsset asset = CreateAssetAndUploadSingleFile(AssetCreationOptions.StorageEncrypted,
                inputMediaFilePath);

            // Get a media processor reference, and pass tooit hello name of the
            // processor toouse for hello specific task.
            IMediaProcessor processor = GetLatestMediaProcessorByName("Media Encoder Standard");

            // Create a task with hello conversion details, using a configuration file.
            ITask task = job.Tasks.AddNew("My encoding Task",
                processor,
                "Adaptive Streaming",
                Microsoft.WindowsAzure.MediaServices.Client.TaskOptions.None);

            // Specify hello input asset toobe encoded.
            task.InputAssets.Add(asset);

            // Add an output asset toocontain hello results of hello job.
            task.OutputAssets.AddNew("Output asset",
                AssetCreationOptions.None);

            // Add a notification point toohello job. You can add multiple notification points.  
            job.JobNotificationSubscriptions.AddNew(NotificationJobState.FinalStatesOnly,
                _notificationEndPoint);

            job.Submit();

            return job;
        }

        public static void WaitForJobToReachedFinishedState(string jobId)
        {
            int expectedState = (int)JobState.Finished;
            int timeOutInSeconds = 600;

            bool jobReachedExpectedState = false;
            DateTime startTime = DateTime.Now;
            int jobState = -1;

            while (!jobReachedExpectedState)
            {
                // Specify how often you want tooget messages from hello queue.
                Thread.Sleep(TimeSpan.FromSeconds(10));

                foreach (var message in _queue.GetMessages(10))
                {
                    using (Stream stream = new MemoryStream(message.AsBytes))
                    {
                        DataContractJsonSerializerSettings settings = new DataContractJsonSerializerSettings();
                        settings.UseSimpleDictionaryFormat = true;
                        DataContractJsonSerializer ser = new DataContractJsonSerializer(typeof(EncodingJobMessage), settings);
                        EncodingJobMessage encodingJobMsg = (EncodingJobMessage)ser.ReadObject(stream);

                        Console.WriteLine();

                        // Display hello message information.
                        Console.WriteLine("EventType: {0}", encodingJobMsg.EventType);
                        Console.WriteLine("MessageVersion: {0}", encodingJobMsg.MessageVersion);
                        Console.WriteLine("ETag: {0}", encodingJobMsg.ETag);
                        Console.WriteLine("TimeStamp: {0}", encodingJobMsg.TimeStamp);
                        foreach (var property in encodingJobMsg.Properties)
                        {
                            Console.WriteLine("    {0}: {1}", property.Key, property.Value);
                        }

                        // We are only interested in messages
                        // where EventType is "JobStateChange".
                        if (encodingJobMsg.EventType == "JobStateChange")
                        {
                            string JobId = (String)encodingJobMsg.Properties.Where(j => j.Key == "JobId").FirstOrDefault().Value;
                            if (JobId == jobId)
                            {
                                string oldJobStateStr = (String)encodingJobMsg.Properties.
                                                            Where(j => j.Key == "OldState").FirstOrDefault().Value;
                                string newJobStateStr = (String)encodingJobMsg.Properties.
                                                            Where(j => j.Key == "NewState").FirstOrDefault().Value;

                                JobState oldJobState = (JobState)Enum.Parse(typeof(JobState), oldJobStateStr);
                                JobState newJobState = (JobState)Enum.Parse(typeof(JobState), newJobStateStr);

                                if (newJobState == (JobState)expectedState)
                                {
                                    Console.WriteLine("job with Id: {0} reached expected state: {1}",
                                        jobId, newJobState);
                                    jobReachedExpectedState = true;
                                    break;
                                }
                            }
                        }
                    }
                    // Delete hello message after we've read it.
                    _queue.DeleteMessage(message);
                }

                // Wait until timeout
                TimeSpan timeDiff = DateTime.Now - startTime;
                bool timedOut = (timeDiff.TotalSeconds > timeOutInSeconds);
                if (timedOut)
                {
                    Console.WriteLine(@"Timeout for checking job notification messages,
                                        latest found state ='{0}', wait time = {1} secs",
                        jobState,
                        timeDiff.TotalSeconds);

                    throw new TimeoutException();
                }
            }
        }

        static private IAsset CreateAssetAndUploadSingleFile(AssetCreationOptions assetCreationOptions, string singleFilePath)
        {
            var asset = _context.Assets.Create("UploadSingleFile_" + DateTime.UtcNow.ToString(),
                assetCreationOptions);

            var fileName = Path.GetFileName(singleFilePath);

            var assetFile = asset.AssetFiles.Create(fileName);

            Console.WriteLine("Created assetFile {0}", assetFile.Name);
            Console.WriteLine("Upload {0}", assetFile.Name);

            assetFile.Upload(singleFilePath);
            Console.WriteLine("Done uploading of {0}", assetFile.Name);

            return asset;
        }

        static private IMediaProcessor GetLatestMediaProcessorByName(string mediaProcessorName)
        {
            var processor = _context.MediaProcessors.Where(p => p.Name == mediaProcessorName).
                ToList().OrderBy(p => new Version(p.Version)).LastOrDefault();

            if (processor == null)
                throw new ArgumentException(string.Format("Unknown media processor", mediaProcessorName));

            return processor;
        }
    }
}
```
Witaj poprzedniego hello przykład utworzone następujące dane wyjściowe. Wartości będą się różnić.

    Created assetFile BigBuckBunny.mp4
    Upload BigBuckBunny.mp4
    Done uploading of BigBuckBunny.mp4

    EventType: NotificationEndPointRegistration
    MessageVersion: 1.0
    ETag: e0238957a9b25bdf3351a88e57978d6a81a84527fad03bc23861dbe28ab293f6
    TimeStamp: 2013-05-14T20:22:37
        NotificationEndPointId: nb:nepid:UUID:d6af9412-2488-45b2-ba1f-6e0ade6dbc27
        State: Registered
        Name: dde957b2-006e-41f2-9869-a978870ac620
        Created: 2013-05-14T20:22:35

    EventType: JobStateChange
    MessageVersion: 1.0
    ETag: 4e381f37c2d844bde06ace650310284d6928b1e50101d82d1b56220cfcb6076c
    TimeStamp: 2013-05-14T20:24:40
        JobId: nb:jid:UUID:526291de-f166-be47-b62a-11ffe6d4be54
        JobName: My MP4 tooSmooth Streaming encoding job
        NewState: Finished
        OldState: Processing
        AccountName: westeuropewamsaccount
    job with Id: nb:jid:UUID:526291de-f166-be47-b62a-11ffe6d4be54 reached expected
    State: Finished


## <a name="next-step"></a>Następny krok
Przejrzyj ścieżki szkoleniowe dotyczące usługi Media Services.

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Przekazywanie opinii
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]
