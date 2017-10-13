---
title: "Używać magazynu kolejek Azure monitorować powiadomienia zadania usługi Media Services z platformą .NET | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak używać magazynu kolejek Azure monitorować powiadomienia zadania usługi Media Services. Przykładowy kod jest napisany w języku C# i używa SDK usługi Media Services dla platformy .NET."
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
ms.openlocfilehash: 5ee89d0ae4c3c56d164aff4e321ee99f015ba4fb
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
# <a name="use-azure-queue-storage-to-monitor-media-services-job-notifications-with-net"></a>Użyj magazynu kolejek Azure, aby monitorować powiadomienia zadania usługi Media Services przy użyciu platformy .NET
Po uruchomieniu zadania kodowania, często wymagają sposób, aby śledzić postęp zadania. Można skonfigurować usługi Media Services w celu dostarczenia powiadomienia do [magazynu kolejek Azure](../storage/storage-dotnet-how-to-use-queues.md). Uzyskiwanie powiadomień z magazynu kolejek można monitorować postęp zadania. 

Komunikaty dostarczone do kolejki magazynu można uzyskać z dowolnego miejsca na świecie. Architektura wiadomości kolejki magazynu jest niezawodnych i wysokiej skalowalności. Sondowanie magazynu kolejek wiadomości jest zalecane w przypadku innych metod.

Typowy scenariusz co do nasłuchiwania na powiadomienia usługi Media Services jest Jeśli tworzysz system zarządzania zawartością, które należy wykonać kilka dodatkowych zadań po kodowania zadanie zostało ukończone (na przykład w celu wyzwalania następnego kroku w przepływie pracy, lub do publikowania zawartość).

W tym temacie pokazano, jak pobrać powiadomień wiadomości z kolejki magazynu.  

## <a name="considerations"></a>Zagadnienia do rozważenia
Podczas tworzenia aplikacji usługi Media Services, które używać magazynu kolejek, należy wziąć pod uwagę następujące:

* Magazyn kolejek nie ma gwarancji, najpierw w pierwszym poza dostarczania uporządkowanego (FIFO). Aby uzyskać więcej informacji, zobacz [kolejek Azure i porównać kolejki magistrali usług Azure i Contrasted](https://msdn.microsoft.com/library/azure/hh767287.aspx).
* Magazyn kolejek nie jest usługi wypychania. Trzeba wykonać sondowanie kolejki.
* Może mieć dowolną liczbę kolejek. Aby uzyskać więcej informacji, zobacz [interfejsu API REST usługi kolejki](https://docs.microsoft.com/rest/api/storageservices/Queue-Service-REST-API).
* Magazyn kolejek ma pewnych ograniczeń i charakterystykę pod uwagę. Te ustawienia zostały opisane w [kolejek Azure i porównać kolejki magistrali usług Azure i Contrasted](https://docs.microsoft.com/azure/service-bus-messaging/service-bus-azure-and-service-bus-queues-compared-contrasted).

## <a name="net-code-example"></a>Przykład kodu platformy .NET

Przykład kodu w tej sekcji wykonuje następujące czynności:

1. Definiuje **EncodingJobMessage** klasy, który jest mapowany na format powiadomienia w wiadomości. Kod deserializuje komunikatów odebranych z kolejki, do obiektów **EncodingJobMessage** typu.
2. Ładuje informacje o koncie usługi Media Services i magazynu z pliku app.config. Przykład kodu wykorzystuje te informacje do tworzenia **CloudMediaContext** i **CloudQueue** obiektów.
3. Tworzy kolejkę, która odbiera powiadomienia dotyczące zadania kodowania.
4. Tworzy punktu końcowego powiadomienia, który jest zamapowany do kolejki.
5. Dołącza punktu końcowego powiadomienia do zadania, a następnie przesyła zadania kodowania. Może mieć wiele punktów końcowych powiadomień dołączone do zadania.
6. Przekazuje **NotificationJobState.FinalStatesOnly** do **AddNew** metody. (W tym przykładzie opiszemy tylko Stany końcowego przetwarzania zadania.)

        job.JobNotificationSubscriptions.AddNew(NotificationJobState.FinalStatesOnly, _notificationEndPoint);
7. W przypadku przekazania **NotificationJobState.All**, możesz pobrać wszystkie następujące powiadomienia o zmianie stanu: umieszczonych w kolejce, zaplanowane przetwarzania i gotowe. Jak wspomniano wcześniej, magazyn kolejek gwarantuje jednak uporządkowanego dostarczenia. Kolejność wiadomości, należy użyć **sygnatury czasowej** właściwości (zdefiniowanego w **EncodingJobMessage** typu w poniższym przykładzie). Możliwe są zduplikowane wiadomości. Aby sprawdzić, czy duplikaty, użyj **właściwość ETag** (zdefiniowanego w **EncodingJobMessage** typu). Istnieje również możliwość, że niektóre powiadomienia o zmianie stanu uzyskać pominięte.
8. Oczekuje na zadanie na uzyskanie dostępu do stan zakończenia sprawdzając kolejki co 10 sekund. Usuwa wiadomości po zostały przetworzone.
9. Usuwa kolejkę i punktu końcowego powiadomienia.

> [!NOTE]
> Zalecanym sposobem monitorować stan zadania jest nasłuchiwanie komunikatów powiadomień, jak pokazano w poniższym przykładzie.
>
> Alternatywnie można sprawdzić stanu zadania za pomocą **IJob.State** właściwości.  Komunikat z powiadomieniem o zakończeniu zadania może pojawić się przed stanu na **IJob** ustawiono **Zakończono**. **IJob.State** właściwość odzwierciedla stan dokładne z niewielkie opóźnienie.
>
>

### <a name="create-and-configure-a-visual-studio-project"></a>Tworzenie i konfigurowanie projektu programu Visual Studio

1. Skonfiguruj środowisko projektowe i wypełnij plik app.config przy użyciu informacji dotyczących połączenia, zgodnie z opisem w sekcji [Projektowanie usługi Media Services na platformie .NET](media-services-dotnet-how-to-use.md). 
2. Utwórz nowy folder (może się on znajdować w dowolnym miejscu na dysku lokalnym) i skopiuj plik mp4, który ma zostać zakodowany i przesłany strumieniowo lub pobrany progresywnie. W tym przykładzie ścieżka "C:\Media" jest używana.

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

        // Type of the event. Valid values are
        // JobStateChange and NotificationEndpointRegistration.
        public String EventType { get; set; }

        // ETag is used to help the customer detect if
        // the message is a duplicate of another message previously sent.
        public String ETag { get; set; }

        // Time of occurrence of the event.
        public String TimeStamp { get; set; }

        // Collection of values specific to the event.

        // For the JobStateChange event the values are:
        //     JobId - Id of the Job that triggered the notification.
        //     NewState- The new state of the Job. Valid values are:
        //          Scheduled, Processing, Canceling, Cancelled, Error, Finished
        //     OldState- The old state of the Job. Valid values are:
        //          Scheduled, Processing, Canceling, Cancelled, Error, Finished

        // For the NotificationEndpointRegistration event the values are:
        //     NotificationEndpointId- Id of the NotificationEndpoint
        //          that triggered the notification.
        //     State- The state of the Endpoint.
        //          Valid values are: Registered and Unregistered.

        public IDictionary<string, object> Properties { get; set; }
    }

    class Program
    {

        // Read values from the App.config file.
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

            // Create the context.
            var tokenCredentials = new AzureAdTokenCredentials(_AADTenantDomain, AzureEnvironments.AzureCloudEnvironment);
            var tokenProvider = new AzureAdTokenProvider(tokenCredentials);

            _context = new CloudMediaContext(new Uri(_RESTAPIEndpoint), tokenProvider);

            // Create the queue that will be receiving the notification messages.
            _queue = CreateQueue(_StorageConnectionString, endPointAddress);

            // Create the notification point that is mapped to the queue.
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

            // Create the queue client
            CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();

            // Retrieve a reference to a queue
            CloudQueue queue = queueClient.GetQueueReference(endPointAddress);

            // Create the queue if it doesn't already exist
            queue.CreateIfNotExists();

            return queue;
        }


        public static IJob SubmitEncodingJobWithNotificationEndPoint(string inputMediaFilePath)
        {
            // Declare a new job.
            IJob job = _context.Jobs.Create("My MP4 to Smooth Streaming encoding job");

            //Create an encrypted asset and upload the mp4.
            IAsset asset = CreateAssetAndUploadSingleFile(AssetCreationOptions.StorageEncrypted,
                inputMediaFilePath);

            // Get a media processor reference, and pass to it the name of the
            // processor to use for the specific task.
            IMediaProcessor processor = GetLatestMediaProcessorByName("Media Encoder Standard");

            // Create a task with the conversion details, using a configuration file.
            ITask task = job.Tasks.AddNew("My encoding Task",
                processor,
                "Adaptive Streaming",
                Microsoft.WindowsAzure.MediaServices.Client.TaskOptions.None);

            // Specify the input asset to be encoded.
            task.InputAssets.Add(asset);

            // Add an output asset to contain the results of the job.
            task.OutputAssets.AddNew("Output asset",
                AssetCreationOptions.None);

            // Add a notification point to the job. You can add multiple notification points.  
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
                // Specify how often you want to get messages from the queue.
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

                        // Display the message information.
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
                    // Delete the message after we've read it.
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
Powyższy przykład utworzone następujące dane wyjściowe. Wartości będą się różnić.

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
        JobName: My MP4 to Smooth Streaming encoding job
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
