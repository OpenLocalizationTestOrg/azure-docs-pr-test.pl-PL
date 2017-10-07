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
# <a name="use-azure-queue-storage-toomonitor-media-services-job-notifications-with-net"></a><span data-ttu-id="3a990-104">Azure kolejki magazynu toomonitor Media Services zadania powiadomienia za pomocą platformy .NET</span><span class="sxs-lookup"><span data-stu-id="3a990-104">Use Azure Queue storage toomonitor Media Services job notifications with .NET</span></span>
<span data-ttu-id="3a990-105">Po uruchomieniu zadania kodowania, często wymagają postępu zadania tootrack sposób.</span><span class="sxs-lookup"><span data-stu-id="3a990-105">When you run encoding jobs, you often require a way tootrack job progress.</span></span> <span data-ttu-id="3a990-106">Można skonfigurować powiadomienia toodeliver Media Services zbyt[magazynu kolejek Azure](../storage/storage-dotnet-how-to-use-queues.md).</span><span class="sxs-lookup"><span data-stu-id="3a990-106">You can configure Media Services toodeliver notifications too[Azure Queue storage](../storage/storage-dotnet-how-to-use-queues.md).</span></span> <span data-ttu-id="3a990-107">Można monitorować postęp zadania pobierania powiadomień z hello magazynu kolejek.</span><span class="sxs-lookup"><span data-stu-id="3a990-107">You can monitor job progress by getting notifications from hello Queue storage.</span></span> 

<span data-ttu-id="3a990-108">Komunikaty dostarczone tooQueue magazynu można uzyskać z dowolnego miejsca w hello world.</span><span class="sxs-lookup"><span data-stu-id="3a990-108">Messages delivered tooQueue storage can be accessed from anywhere in hello world.</span></span> <span data-ttu-id="3a990-109">Hello architektura wiadomości kolejki magazynu jest niezawodnych i wysokiej skalowalności.</span><span class="sxs-lookup"><span data-stu-id="3a990-109">hello Queue storage messaging architecture is reliable and highly scalable.</span></span> <span data-ttu-id="3a990-110">Sondowanie magazynu kolejek wiadomości jest zalecane w przypadku innych metod.</span><span class="sxs-lookup"><span data-stu-id="3a990-110">Polling Queue storage for messages is recommended over using other methods.</span></span>

<span data-ttu-id="3a990-111">Jednego typowych scenariuszy nasłuchiwania powiadomień usługi tooMedia Jeśli tworzysz system zarządzania zawartością, która musi tooperform ukończeniu (na przykład tootrigger hello następnego kroku w przepływie pracy lub toopublish niektóre dodatkowe zadania po zadania kodowania zawartość).</span><span class="sxs-lookup"><span data-stu-id="3a990-111">One common scenario for listening tooMedia Services notifications is if you are developing a content management system that needs tooperform some additional task after an encoding job completes (for example, tootrigger hello next step in a workflow, or toopublish content).</span></span>

<span data-ttu-id="3a990-112">W tym temacie przedstawiono sposób tooget powiadomień wiadomości z kolejki magazynu.</span><span class="sxs-lookup"><span data-stu-id="3a990-112">This topic shows how tooget notification messages from Queue storage.</span></span>  

## <a name="considerations"></a><span data-ttu-id="3a990-113">Zagadnienia do rozważenia</span><span class="sxs-lookup"><span data-stu-id="3a990-113">Considerations</span></span>
<span data-ttu-id="3a990-114">Podczas tworzenia aplikacji usługi Media Services, które używać magazynu kolejek, należy wziąć pod uwagę następujące hello:</span><span class="sxs-lookup"><span data-stu-id="3a990-114">Consider hello following when developing Media Services applications that use Queue storage:</span></span>

* <span data-ttu-id="3a990-115">Magazyn kolejek nie ma gwarancji, najpierw w pierwszym poza dostarczania uporządkowanego (FIFO).</span><span class="sxs-lookup"><span data-stu-id="3a990-115">Queue storage does not provide a guarantee of first-in-first-out (FIFO) ordered delivery.</span></span> <span data-ttu-id="3a990-116">Aby uzyskać więcej informacji, zobacz [kolejek Azure i porównać kolejki magistrali usług Azure i Contrasted](https://msdn.microsoft.com/library/azure/hh767287.aspx).</span><span class="sxs-lookup"><span data-stu-id="3a990-116">For more information, see [Azure Queues and Azure Service Bus Queues Compared and Contrasted](https://msdn.microsoft.com/library/azure/hh767287.aspx).</span></span>
* <span data-ttu-id="3a990-117">Magazyn kolejek nie jest usługi wypychania.</span><span class="sxs-lookup"><span data-stu-id="3a990-117">Queue storage is not a push service.</span></span> <span data-ttu-id="3a990-118">Masz toopoll hello kolejki.</span><span class="sxs-lookup"><span data-stu-id="3a990-118">You have toopoll hello queue.</span></span>
* <span data-ttu-id="3a990-119">Może mieć dowolną liczbę kolejek.</span><span class="sxs-lookup"><span data-stu-id="3a990-119">You can have any number of queues.</span></span> <span data-ttu-id="3a990-120">Aby uzyskać więcej informacji, zobacz [interfejsu API REST usługi kolejki](https://docs.microsoft.com/rest/api/storageservices/Queue-Service-REST-API).</span><span class="sxs-lookup"><span data-stu-id="3a990-120">For more information, see [Queue Service REST API](https://docs.microsoft.com/rest/api/storageservices/Queue-Service-REST-API).</span></span>
* <span data-ttu-id="3a990-121">Magazyn kolejek ma pewnych ograniczeń i toobe charakterystykę znane.</span><span class="sxs-lookup"><span data-stu-id="3a990-121">Queue storage has some limitations and specifics toobe aware of.</span></span> <span data-ttu-id="3a990-122">Te ustawienia zostały opisane w [kolejek Azure i porównać kolejki magistrali usług Azure i Contrasted](https://docs.microsoft.com/azure/service-bus-messaging/service-bus-azure-and-service-bus-queues-compared-contrasted).</span><span class="sxs-lookup"><span data-stu-id="3a990-122">These are described in [Azure Queues and Azure Service Bus Queues Compared and Contrasted](https://docs.microsoft.com/azure/service-bus-messaging/service-bus-azure-and-service-bus-queues-compared-contrasted).</span></span>

## <a name="net-code-example"></a><span data-ttu-id="3a990-123">Przykład kodu platformy .NET</span><span class="sxs-lookup"><span data-stu-id="3a990-123">.NET code example</span></span>

<span data-ttu-id="3a990-124">przykład Witaj kodu w tej sekcji hello następujące:</span><span class="sxs-lookup"><span data-stu-id="3a990-124">hello code example in this section does hello following:</span></span>

1. <span data-ttu-id="3a990-125">Definiuje hello **EncodingJobMessage** klasa, która mapuje toohello format powiadomienia w wiadomości.</span><span class="sxs-lookup"><span data-stu-id="3a990-125">Defines hello **EncodingJobMessage** class that maps toohello notification message format.</span></span> <span data-ttu-id="3a990-126">Kod Hello deserializuje komunikatów odebranych z kolejki hello na obiekty hello **EncodingJobMessage** typu.</span><span class="sxs-lookup"><span data-stu-id="3a990-126">hello code deserializes messages received from hello queue into objects of hello **EncodingJobMessage** type.</span></span>
2. <span data-ttu-id="3a990-127">Ładunki hello Media Services oraz informacji o koncie magazynu w pliku app.config hello.</span><span class="sxs-lookup"><span data-stu-id="3a990-127">Loads hello Media Services and Storage account information from hello app.config file.</span></span> <span data-ttu-id="3a990-128">Przykładowy kod Hello używa tego hello toocreate informacji **CloudMediaContext** i **CloudQueue** obiektów.</span><span class="sxs-lookup"><span data-stu-id="3a990-128">hello code example uses this information toocreate hello **CloudMediaContext** and **CloudQueue** objects.</span></span>
3. <span data-ttu-id="3a990-129">Tworzy kolejkę hello, która odbiera powiadomienia dotyczące hello zadania kodowania.</span><span class="sxs-lookup"><span data-stu-id="3a990-129">Creates hello queue that receives notification messages about hello encoding job.</span></span>
4. <span data-ttu-id="3a990-130">Tworzy hello powiadomień, się, że punkt końcowy, który jest mapowany toohello kolejki.</span><span class="sxs-lookup"><span data-stu-id="3a990-130">Creates hello notification end point that is mapped toohello queue.</span></span>
5. <span data-ttu-id="3a990-131">Dołącza hello powiadomienia punktu końcowego toohello zadania, a następnie przesyła hello zadania kodowania.</span><span class="sxs-lookup"><span data-stu-id="3a990-131">Attaches hello notification end point toohello job and submits hello encoding job.</span></span> <span data-ttu-id="3a990-132">Może mieć wiele zadania tooa dołączony punktów końcowych powiadomień.</span><span class="sxs-lookup"><span data-stu-id="3a990-132">You can have multiple notification end points attached tooa job.</span></span>
6. <span data-ttu-id="3a990-133">Przekazuje **NotificationJobState.FinalStatesOnly** toohello **AddNew** metody.</span><span class="sxs-lookup"><span data-stu-id="3a990-133">Passes **NotificationJobState.FinalStatesOnly** toohello **AddNew** method.</span></span> <span data-ttu-id="3a990-134">(W tym przykładzie opiszemy tylko Stany końcowego przetwarzania zadania hello.)</span><span class="sxs-lookup"><span data-stu-id="3a990-134">(In this example, we are only interested in final states of hello job processing.)</span></span>

        job.JobNotificationSubscriptions.AddNew(NotificationJobState.FinalStatesOnly, _notificationEndPoint);
7. <span data-ttu-id="3a990-135">W przypadku przekazania **NotificationJobState.All**, Pobierz wszystkie następujące powiadomienia o zmianie stanu hello: umieszczonych w kolejce, zaplanowane przetwarzania i gotowe.</span><span class="sxs-lookup"><span data-stu-id="3a990-135">If you pass **NotificationJobState.All**, you get all of hello following state change notifications: queued, scheduled, processing, and finished.</span></span> <span data-ttu-id="3a990-136">Jak wspomniano wcześniej, magazyn kolejek gwarantuje jednak uporządkowanego dostarczenia.</span><span class="sxs-lookup"><span data-stu-id="3a990-136">However, as noted earlier, Queue storage does not guarantee ordered delivery.</span></span> <span data-ttu-id="3a990-137">komunikaty tooorder, należy użyć hello **sygnatury czasowej** właściwości (zdefiniowany na powitania **EncodingJobMessage** typu w poniższym przykładzie hello).</span><span class="sxs-lookup"><span data-stu-id="3a990-137">tooorder messages, use hello **Timestamp** property (defined on hello **EncodingJobMessage** type in hello example below).</span></span> <span data-ttu-id="3a990-138">Możliwe są zduplikowane wiadomości.</span><span class="sxs-lookup"><span data-stu-id="3a990-138">Duplicate messages are possible.</span></span> <span data-ttu-id="3a990-139">toocheck duplikatów, użyj hello **właściwość ETag** (zdefiniowany na powitania **EncodingJobMessage** typu).</span><span class="sxs-lookup"><span data-stu-id="3a990-139">toocheck for duplicates, use hello **ETag property** (defined on hello **EncodingJobMessage** type).</span></span> <span data-ttu-id="3a990-140">Istnieje również możliwość, że niektóre powiadomienia o zmianie stanu uzyskać pominięte.</span><span class="sxs-lookup"><span data-stu-id="3a990-140">It is also possible that some state change notifications get skipped.</span></span>
8. <span data-ttu-id="3a990-141">Czeka na powitania zadania tooget toohello Zakończono stanu, sprawdzając kolejki hello co 10 sekund.</span><span class="sxs-lookup"><span data-stu-id="3a990-141">Waits for hello job tooget toohello finished state by checking hello queue every 10 seconds.</span></span> <span data-ttu-id="3a990-142">Usuwa wiadomości po zostały przetworzone.</span><span class="sxs-lookup"><span data-stu-id="3a990-142">Deletes messages after they have been processed.</span></span>
9. <span data-ttu-id="3a990-143">Usuwa kolejkę hello i punktu końcowego powiadomienia hello.</span><span class="sxs-lookup"><span data-stu-id="3a990-143">Deletes hello queue and hello notification end point.</span></span>

> [!NOTE]
> <span data-ttu-id="3a990-144">Witaj toomonitor zalecaną metodą, stan zadania to nasłuchiwania toonotification wiadomości, jak pokazano w hello poniższy przykład.</span><span class="sxs-lookup"><span data-stu-id="3a990-144">hello recommended way toomonitor a job’s state is by listening toonotification messages, as shown in hello following example.</span></span>
>
> <span data-ttu-id="3a990-145">Alternatywnie można sprawdzić stanu zadania za pomocą hello **IJob.State** właściwości.</span><span class="sxs-lookup"><span data-stu-id="3a990-145">Alternatively, you could check on a job’s state by using hello **IJob.State** property.</span></span>  <span data-ttu-id="3a990-146">Komunikat z powiadomieniem o zakończeniu zadania może pojawić się przed stanu hello na **IJob** ustawiono zbyt**Zakończono**.</span><span class="sxs-lookup"><span data-stu-id="3a990-146">A notification message about a job’s completion may arrive before hello state on **IJob** is set too**Finished**.</span></span> <span data-ttu-id="3a990-147">Witaj **IJob.State** właściwość odzwierciedla stan dokładne hello z niewielkie opóźnienie.</span><span class="sxs-lookup"><span data-stu-id="3a990-147">hello **IJob.State**  property reflects hello accurate state with a slight delay.</span></span>
>
>

### <a name="create-and-configure-a-visual-studio-project"></a><span data-ttu-id="3a990-148">Tworzenie i konfigurowanie projektu programu Visual Studio</span><span class="sxs-lookup"><span data-stu-id="3a990-148">Create and configure a Visual Studio project</span></span>

1. <span data-ttu-id="3a990-149">Konfigurowanie środowiska projektowego i wypełnić plik app.config hello o informacje dotyczące połączenia, zgodnie z opisem w [tworzenia usługi Media Services z platformą .NET](media-services-dotnet-how-to-use.md).</span><span class="sxs-lookup"><span data-stu-id="3a990-149">Set up your development environment and populate hello app.config file with connection information, as described in [Media Services development with .NET](media-services-dotnet-how-to-use.md).</span></span> 
2. <span data-ttu-id="3a990-150">Utwórz nowy folder (folder może być dowolnym miejscu na dysku lokalnym) i skopiuj plik plik MP4 tooencode i strumienia, lub pobrać progresywnie.</span><span class="sxs-lookup"><span data-stu-id="3a990-150">Create a new folder (folder can be anywhere on your local drive) and copy an .mp4 file that you want tooencode and stream or progressively download.</span></span> <span data-ttu-id="3a990-151">W tym przykładzie ścieżki "C:\Media" hello jest używany.</span><span class="sxs-lookup"><span data-stu-id="3a990-151">In this example, hello "C:\Media" path is used.</span></span>

### <a name="code"></a><span data-ttu-id="3a990-152">Kod</span><span class="sxs-lookup"><span data-stu-id="3a990-152">Code</span></span>

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
<span data-ttu-id="3a990-153">Witaj poprzedniego hello przykład utworzone następujące dane wyjściowe.</span><span class="sxs-lookup"><span data-stu-id="3a990-153">hello preceding example produced hello following output.</span></span> <span data-ttu-id="3a990-154">Wartości będą się różnić.</span><span class="sxs-lookup"><span data-stu-id="3a990-154">Your values will vary.</span></span>

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


## <a name="next-step"></a><span data-ttu-id="3a990-155">Następny krok</span><span class="sxs-lookup"><span data-stu-id="3a990-155">Next step</span></span>
<span data-ttu-id="3a990-156">Przejrzyj ścieżki szkoleniowe dotyczące usługi Media Services.</span><span class="sxs-lookup"><span data-stu-id="3a990-156">Review Media Services learning paths.</span></span>

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="3a990-157">Przekazywanie opinii</span><span class="sxs-lookup"><span data-stu-id="3a990-157">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]
