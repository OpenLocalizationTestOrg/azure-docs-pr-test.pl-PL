---
title: "aaaNotification koncentratory — architektura Push Enterprise"
description: "Wskazówki dotyczące używania usługi Azure Notification Hubs w środowisku przedsiębiorstwa"
services: notification-hubs
documentationcenter: 
author: ysxu
manager: erikre
editor: 
ms.assetid: 903023e9-9347-442a-924b-663af85e05c6
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: mobile-windows
ms.devlang: dotnet
ms.topic: article
ms.date: 06/29/2016
ms.author: yuaxu
ms.openlocfilehash: c3afb83de1ba0882bf99e10f38cca40cb42d07a5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="enterprise-push-architectural-guidance"></a><span data-ttu-id="f16c8-103">Wskazówki dotyczące architektury powiadomień wypychanych w przedsiębiorstwie</span><span class="sxs-lookup"><span data-stu-id="f16c8-103">Enterprise push architectural guidance</span></span>
<span data-ttu-id="f16c8-104">Dzisiaj przedsiębiorstwa są stopniowo przenoszenie do tworzenia aplikacji dla urządzeń przenośnych dla dowolnego użytkownikom końcowym (zewnętrzne) lub dla pracowników hello (wewnętrzny).</span><span class="sxs-lookup"><span data-stu-id="f16c8-104">Enterprises today are gradually moving towards creating mobile applications for either their end users (external) or for hello employees (internal).</span></span> <span data-ttu-id="f16c8-105">Mają one istniejącymi systemami wewnętrznej bazy danych w miejscu, można go Komputery mainframe firmy lub niektóre aplikacje LoB, które muszą zostać włączone do hello architektury aplikacji mobilnej.</span><span class="sxs-lookup"><span data-stu-id="f16c8-105">They have existing backend systems in place be it mainframes or some LoB applications which must be integrated into hello mobile application architecture.</span></span> <span data-ttu-id="f16c8-106">W tym przewodniku zostaną omówione toodo najlepszego integracja rekomendowania możliwe rozwiązanie toocommon scenariuszy.</span><span class="sxs-lookup"><span data-stu-id="f16c8-106">This guide will talk about how best toodo this integration recommending possible solution toocommon scenarios.</span></span>

<span data-ttu-id="f16c8-107">Jest wymagane częste do wysyłania powiadomień toohello użytkowników za pomocą ich aplikacji mobilnej wypychania po wystąpieniu zdarzenia zainteresowania w systemach zaplecza hello.</span><span class="sxs-lookup"><span data-stu-id="f16c8-107">A frequent requirement is for sending push notification toohello users through their mobile application when an event of interest occurs in hello backend systems.</span></span> <span data-ttu-id="f16c8-108">Na przykład</span><span class="sxs-lookup"><span data-stu-id="f16c8-108">E.g.</span></span> <span data-ttu-id="f16c8-109">Klient bank, który jest aplikacja bankowa hello bank na swoim telefonie iPhone chce toobe powiadomienie, gdy debetowa staje się powyżej pewnego swoje konto lub scenariusz sieci intranet, gdzie pracowników z działu finansowego mającego aplikacji zatwierdzenia budżetu na jego Windows Phone, który chce toobe powiadomienie, gdy uzyskuje on żądanie zatwierdzenia.</span><span class="sxs-lookup"><span data-stu-id="f16c8-109">a bank customer who has hello bank's banking app on her iPhone wants toobe notified when a debit is made above a certain amount from her account or an intranet scenario where an employee from finance department who has a budget approval app on his Windows Phone wants toobe notified when he gets an approval request.</span></span>

<span data-ttu-id="f16c8-110">konta bankowego Hello lub przetwarzania zatwierdzenia jest prawdopodobnie toobe wykonywane w niektórych systemie wewnętrznej bazy danych, w którym konieczne jest zainicjowanie użytkownika toohello wypychania.</span><span class="sxs-lookup"><span data-stu-id="f16c8-110">hello bank account or approval processing is likely toobe done in some backend system which must initiate a push toohello user.</span></span> <span data-ttu-id="f16c8-111">Może istnieć wiele takich zaplecza systemów, które muszą wszystkie kompilacji hello sam rodzaj logiki tooimplement wypychania, gdy zdarzenie jest wyzwalane powiadomienie.</span><span class="sxs-lookup"><span data-stu-id="f16c8-111">There may be multiple such backend systems which must all build hello same kind of logic tooimplement push when an event triggers a notification.</span></span> <span data-ttu-id="f16c8-112">złożoność Hello tutaj znajduje się w integrowania kilka systemów wewnętrznej bazy danych wraz z systemu pojedynczego wypychania, gdzie hello użytkownikom końcowym masz subskrypcję powiadomień toodifferent i może nawet być wiele aplikacji mobilnych, np. w przypadku hello aplikacji mobilnych w sieci intranet gdzie jednej aplikacji mobilnej można tooreceive powiadomienia z wielu takich systemów zaplecza.</span><span class="sxs-lookup"><span data-stu-id="f16c8-112">hello complexity here lies in integrating several backend systems together with a single push system where hello end users may have subscribed toodifferent notifications and there may even be multiple mobile applications e.g. in hello case of intranet mobile apps where one mobile application may want tooreceive notifications from multiple such backend systems.</span></span> <span data-ttu-id="f16c8-113">systemy zaplecza Hello nie znasz lub muszą mieć tooknow wypychania semantyki/technologii umożliwiające rozwiązanie typowych tutaj tradycyjnie była toointroduce składnika, który sonduje systemów zaplecza hello wszystkie zdarzenia odsetek i jest odpowiedzialny za wysyłanie wiadomości wypychanych powitania toohello klienta.</span><span class="sxs-lookup"><span data-stu-id="f16c8-113">hello backend systems do not know or need tooknow of push semantics/technology so a common solution here traditionally has been toointroduce a component which polls hello backend systems for any events of interest and is responsible for sending hello push messages toohello client.</span></span>
<span data-ttu-id="f16c8-114">W tym polu, zostaną omawianiu nawet lepszym rozwiązaniem przy użyciu usługi Azure Service Bus - modelu tematu/subskrypcji, który zostanie zredukowana złożoność hello jednocześnie skalowalne rozwiązanie hello.</span><span class="sxs-lookup"><span data-stu-id="f16c8-114">Here we will talk about an even better solution using Azure Service Bus - Topic/Subscription model which will reduce hello complexity while making hello solution scalable.</span></span>

<span data-ttu-id="f16c8-115">Oto hello ogólne architektury rozwiązania hello (uogólniony z wielu aplikacji mobilnych ale również mają zastosowanie, gdy istnieje tylko jeden aplikacji mobilnej)</span><span class="sxs-lookup"><span data-stu-id="f16c8-115">Here is hello general architecture of hello solution (generalized with multiple mobile apps but equally applicable when there is only one mobile app)</span></span>

## <a name="architecture"></a><span data-ttu-id="f16c8-116">Architektura</span><span class="sxs-lookup"><span data-stu-id="f16c8-116">Architecture</span></span>
![][1]

<span data-ttu-id="f16c8-117">część klucza Hello na tym diagramie architektury jest Azure Service Bus, która zapewnia model programowania tematy/subskrypcji (więcej informacji na temat go w [programowania magistrali usługi Pub/Sub]).</span><span class="sxs-lookup"><span data-stu-id="f16c8-117">hello key piece in this architectural diagram is Azure Service Bus which provides a topics/subscriptions programming model (more on it at [Service Bus Pub/Sub programming]).</span></span> <span data-ttu-id="f16c8-118">odbiornik Hello, w tym przypadku jest hello zaplecza aplikacji mobilnych (zazwyczaj [usługi mobilnej Azure], inicjuje wypychanych aplikacji mobilnych toohello) nie odbierać komunikaty bezpośrednio z systemów zaplecza hello, ale zamiast tego mamy warstwy abstrakcji pośredniego dostarczonych przez [Azure Service Bus] co pozwala komunikaty tooreceive zaplecza aplikacji mobilnych z jednego lub kilku systemów zaplecza.</span><span class="sxs-lookup"><span data-stu-id="f16c8-118">hello receiver, which in this case, is hello Mobile backend (typically [Azure Mobile Service], which will initiate a push toohello mobile apps) does not receive messages directly from hello backend systems but instead we have an intermediate abstraction layer provided by [Azure Service Bus] which enables mobile backend tooreceive messages from one or more backend systems.</span></span> <span data-ttu-id="f16c8-119">Temat magistrali usług musi toobe tworzone dla poszczególnych systemów hello zaplecza np. konta, HR, finansowych, które są po prostu "tematów", który będzie inicjował toobe wiadomości wysyłane jako powiadomienie wypychane.</span><span class="sxs-lookup"><span data-stu-id="f16c8-119">A Service Bus Topic needs toobe created for each of hello backend systems e.g. Account, HR, Finance which are basically "topics" of interest which will initiate messages toobe sent as push notification.</span></span> <span data-ttu-id="f16c8-120">systemy zaplecza Hello wyśle komunikaty toothese tematów.</span><span class="sxs-lookup"><span data-stu-id="f16c8-120">hello backend systems will send messages toothese topics.</span></span> <span data-ttu-id="f16c8-121">Zaplecza Mobile można zasubskrybować tooone lub więcej takich tematy podczas tworzenia subskrypcji usługi Service Bus.</span><span class="sxs-lookup"><span data-stu-id="f16c8-121">A Mobile Backend can subscribe tooone or more such topics by creating a Service Bus subscription.</span></span> <span data-ttu-id="f16c8-122">Spowoduje to uprawniają hello zaplecze aplikacji mobilnej tooreceive powiadomienie z hello odpowiedniej wewnętrznej bazy danych systemu.</span><span class="sxs-lookup"><span data-stu-id="f16c8-122">This will entitle hello mobile backend tooreceive a notification from hello corresponding backend system.</span></span> <span data-ttu-id="f16c8-123">Zaplecze aplikacji mobilnej nadal toolisten wiadomości na ich subskrypcji i zaraz po odebraniu komunikatu Przechodzi wstecz i wysyła je jako centrum powiadomień tooits powiadomień.</span><span class="sxs-lookup"><span data-stu-id="f16c8-123">Mobile backend continues toolisten for messages on their subscriptions and as soon as a message arrives, it turns back and sends it as notification tooits notification hub.</span></span> <span data-ttu-id="f16c8-124">Następnie usługi Notification hubs zapewnia ostatecznie aplikacji mobilnej toohello wiadomość hello.</span><span class="sxs-lookup"><span data-stu-id="f16c8-124">Notification hubs then eventually delivers hello message toohello mobile app.</span></span> <span data-ttu-id="f16c8-125">Dlatego toosummarize hello najważniejsze składniki mamy:</span><span class="sxs-lookup"><span data-stu-id="f16c8-125">So toosummarize hello key components, we have:</span></span>

1. <span data-ttu-id="f16c8-126">Systemy zaplecza (LoB/starsze systemy)</span><span class="sxs-lookup"><span data-stu-id="f16c8-126">Backend systems (LoB/Legacy systems)</span></span>
   * <span data-ttu-id="f16c8-127">Tworzy temat magistrali usług</span><span class="sxs-lookup"><span data-stu-id="f16c8-127">Creates Service Bus Topic</span></span>
   * <span data-ttu-id="f16c8-128">Wysyła komunikat</span><span class="sxs-lookup"><span data-stu-id="f16c8-128">Sends Message</span></span>
2. <span data-ttu-id="f16c8-129">Zaplecze mobilne</span><span class="sxs-lookup"><span data-stu-id="f16c8-129">Mobile backend</span></span>
   * <span data-ttu-id="f16c8-130">Tworzy subskrypcji usługi</span><span class="sxs-lookup"><span data-stu-id="f16c8-130">Creates Service Subscription</span></span>
   * <span data-ttu-id="f16c8-131">Odbiera komunikat (z wewnętrznej bazy danych systemu)</span><span class="sxs-lookup"><span data-stu-id="f16c8-131">Receives Message (from Backend system)</span></span>
   * <span data-ttu-id="f16c8-132">Wysyła powiadomienia tooclients (za pośrednictwem Centrum powiadomień Azure)</span><span class="sxs-lookup"><span data-stu-id="f16c8-132">Sends notification tooclients (via Azure Notification Hub)</span></span>
3. <span data-ttu-id="f16c8-133">Aplikacji mobilnej</span><span class="sxs-lookup"><span data-stu-id="f16c8-133">Mobile Application</span></span>
   * <span data-ttu-id="f16c8-134">Odbiera i wyświetlania powiadomień</span><span class="sxs-lookup"><span data-stu-id="f16c8-134">Receives and display notification</span></span>

### <a name="benefits"></a><span data-ttu-id="f16c8-135">Korzyści:</span><span class="sxs-lookup"><span data-stu-id="f16c8-135">Benefits:</span></span>
1. <span data-ttu-id="f16c8-136">rozdzielenie Hello hello odbiornika (aplikacji/usługi mobilnej za pośrednictwem Centrum powiadomień) i nadawcy (systemy zaplecza) umożliwia systemów dodatkowe wewnętrznej bazy danych jest zintegrowany z minimalnym zmiany.</span><span class="sxs-lookup"><span data-stu-id="f16c8-136">hello decoupling between hello receiver (mobile app/service via Notification Hub) and sender (backend systems) enables additional backend systems being integrated with minimal change.</span></span>
2. <span data-ttu-id="f16c8-137">Ułatwia to też hello scenariusz wiele aplikacji mobilnych, jest w stanie tooreceive zdarzeń z jednego lub kilku systemów zaplecza.</span><span class="sxs-lookup"><span data-stu-id="f16c8-137">This also makes hello scenario of multiple mobile apps being able tooreceive events from one or more backend systems.</span></span>  

## <a name="sample"></a><span data-ttu-id="f16c8-138">Przykład:</span><span class="sxs-lookup"><span data-stu-id="f16c8-138">Sample:</span></span>
### <a name="prerequisites"></a><span data-ttu-id="f16c8-139">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="f16c8-139">Prerequisites</span></span>
<span data-ttu-id="f16c8-140">Należy wykonać hello następujące samouczki toofamiliarize z założenia hello, a także typowe kroki tworzenia i konfiguracji:</span><span class="sxs-lookup"><span data-stu-id="f16c8-140">You should complete hello following tutorials toofamiliarize with hello concepts as well as common creation & configuration steps:</span></span>

1. <span data-ttu-id="f16c8-141">[programowania magistrali usługi Pub/Sub] — w tej sekcji wyjaśniono hello szczegółowe informacje dotyczące pracy z tematów magistrali usługi/subskrypcji, jak toocreate przestrzeni nazw toocontain tematy/subskrypcji, jak toosend & odbierać komunikaty z nich.</span><span class="sxs-lookup"><span data-stu-id="f16c8-141">[Service Bus Pub/Sub programming] - This explains hello details of working with Service Bus Topics/Subscriptions, how toocreate a namespace toocontain topics/subscriptions, how toosend & receive messages from them.</span></span>
2. <span data-ttu-id="f16c8-142">[Notification Hubs — samouczek aplikacji uniwersalnych systemu Windows] — w tej sekcji wyjaśniono, jak tooset Konfigurowanie aplikacji ze Sklepu Windows i używać usługi Notification Hubs tooregister i będzie otrzymywać powiadomienia.</span><span class="sxs-lookup"><span data-stu-id="f16c8-142">[Notification Hubs - Windows Universal tutorial] - This explains how tooset up a Windows Store app and use Notification Hubs tooregister and then receive notifications.</span></span>

### <a name="sample-code"></a><span data-ttu-id="f16c8-143">Przykładowy kod</span><span class="sxs-lookup"><span data-stu-id="f16c8-143">Sample code</span></span>
<span data-ttu-id="f16c8-144">Kod pełny przykład Hello jest dostępny w [przykłady Centrum powiadomień].</span><span class="sxs-lookup"><span data-stu-id="f16c8-144">hello full sample code is available at [Notification Hub Samples].</span></span> <span data-ttu-id="f16c8-145">Są one podzielone na trzy składniki:</span><span class="sxs-lookup"><span data-stu-id="f16c8-145">It is split into three components:</span></span>

1. <span data-ttu-id="f16c8-146">**EnterprisePushBackendSystem**</span><span class="sxs-lookup"><span data-stu-id="f16c8-146">**EnterprisePushBackendSystem**</span></span>
   
    <span data-ttu-id="f16c8-147">a.</span><span class="sxs-lookup"><span data-stu-id="f16c8-147">a.</span></span> <span data-ttu-id="f16c8-148">Ten projekt używa hello *WindowsAzure.ServiceBus* pakietu Nuget i jest oparty na [programowania magistrali usługi Pub/Sub].</span><span class="sxs-lookup"><span data-stu-id="f16c8-148">This project uses hello *WindowsAzure.ServiceBus* Nuget package and is  based on [Service Bus Pub/Sub programming].</span></span>
   
    <span data-ttu-id="f16c8-149">b.</span><span class="sxs-lookup"><span data-stu-id="f16c8-149">b.</span></span> <span data-ttu-id="f16c8-150">Jest to prosty C# console aplikacji toosimulate systemu LoB, która inicjuje toobe wiadomość hello dostarczyć toohello aplikacji mobilnej.</span><span class="sxs-lookup"><span data-stu-id="f16c8-150">This is a simple C# console app toosimulate an LoB system which initiates hello message toobe delivered toohello mobile app.</span></span>
   
        static void Main(string[] args)
        {
            string connectionString =
                CloudConfigurationManager.GetSetting("Microsoft.ServiceBus.ConnectionString");
   
            // Create hello topic where we will send notifications
            CreateTopic(connectionString);
   
            // Send message
            SendMessage(connectionString);
        }
   
    <span data-ttu-id="f16c8-151">c.</span><span class="sxs-lookup"><span data-stu-id="f16c8-151">c.</span></span> <span data-ttu-id="f16c8-152">`CreateTopic`jest tematu usługi Service Bus hello toocreate używany gdzie możemy wysłać wiadomości.</span><span class="sxs-lookup"><span data-stu-id="f16c8-152">`CreateTopic` is used toocreate hello Service Bus topic where we will send messages.</span></span>
   
        public static void CreateTopic(string connectionString)
        {
            // Create hello topic if it does not exist already
   
            var namespaceManager =
                NamespaceManager.CreateFromConnectionString(connectionString);
   
            if (!namespaceManager.TopicExists(sampleTopic))
            {
                namespaceManager.CreateTopic(sampleTopic);
            }
        }
   
    <span data-ttu-id="f16c8-153">d.</span><span class="sxs-lookup"><span data-stu-id="f16c8-153">d.</span></span> <span data-ttu-id="f16c8-154">`SendMessage`jest toothis wiadomości powitania toosend używanych tematów magistrali usługi.</span><span class="sxs-lookup"><span data-stu-id="f16c8-154">`SendMessage` is used toosend hello messages toothis Service Bus Topic.</span></span> <span data-ttu-id="f16c8-155">Firma Microsoft tutaj po prostu wysyłania zestaw tematu toohello losowe wiadomości okresowo w celu hello hello próbki.</span><span class="sxs-lookup"><span data-stu-id="f16c8-155">Here we are simply sending a set of random messages toohello topic periodically for hello purpose of hello sample.</span></span> <span data-ttu-id="f16c8-156">Zwykle będzie systemu wewnętrznej bazy danych, która będzie wysyłać wiadomości, gdy wystąpi zdarzenie.</span><span class="sxs-lookup"><span data-stu-id="f16c8-156">Normally there will be a backend system which will send messages when an event occurs.</span></span>
   
        public static void SendMessage(string connectionString)
        {
            TopicClient client =
                TopicClient.CreateFromConnectionString(connectionString, sampleTopic);
   
            // Sends random messages every 10 seconds toohello topic
            string[] messages =
            {
                "Employee Id '{0}' has joined.",
                "Employee Id '{0}' has left.",
                "Employee Id '{0}' has switched tooa different team."
            };
   
            while (true)
            {
                Random rnd = new Random();
                string employeeId = rnd.Next(10000, 99999).ToString();
                string notification = String.Format(messages[rnd.Next(0,messages.Length)], employeeId);
   
                // Send Notification
                BrokeredMessage message = new BrokeredMessage(notification);
                client.Send(message);
   
                Console.WriteLine("{0} Message sent - '{1}'", DateTime.Now, notification);
   
                System.Threading.Thread.Sleep(new TimeSpan(0, 0, 10));
            }
        }
2. <span data-ttu-id="f16c8-157">**ReceiveAndSendNotification**</span><span class="sxs-lookup"><span data-stu-id="f16c8-157">**ReceiveAndSendNotification**</span></span>
   
    <span data-ttu-id="f16c8-158">a.</span><span class="sxs-lookup"><span data-stu-id="f16c8-158">a.</span></span> <span data-ttu-id="f16c8-159">Ten projekt używa hello *WindowsAzure.ServiceBus* i *Microsoft.Web.WebJobs.Publish* Nuget pakietów i jest oparty na [programowania magistrali usługi Pub/Sub].</span><span class="sxs-lookup"><span data-stu-id="f16c8-159">This project uses hello *WindowsAzure.ServiceBus* and *Microsoft.Web.WebJobs.Publish* Nuget packages and is based on [Service Bus Pub/Sub programming].</span></span>
   
    <span data-ttu-id="f16c8-160">b.</span><span class="sxs-lookup"><span data-stu-id="f16c8-160">b.</span></span> <span data-ttu-id="f16c8-161">Jest to inny C# console aplikacji, która zostanie uruchomiony jako [zadań WebJob Azure] ponieważ stale ma toorun toolisten dla komunikatów z systemów LoB/zaplecza hello.</span><span class="sxs-lookup"><span data-stu-id="f16c8-161">This is another C# console app which we will run as an [Azure WebJob] since it has toorun continuously toolisten for messages from hello LoB/backend systems.</span></span> <span data-ttu-id="f16c8-162">Są to część z zaplecza aplikacji mobilnych.</span><span class="sxs-lookup"><span data-stu-id="f16c8-162">This will be part of your Mobile backend.</span></span>
   
        static void Main(string[] args)
        {
            string connectionString =
                     CloudConfigurationManager.GetSetting("Microsoft.ServiceBus.ConnectionString");
   
            // Create hello subscription which will receive messages
            CreateSubscription(connectionString);
   
            // Receive message
            ReceiveMessageAndSendNotification(connectionString);
        }
   
    <span data-ttu-id="f16c8-163">c.</span><span class="sxs-lookup"><span data-stu-id="f16c8-163">c.</span></span> <span data-ttu-id="f16c8-164">`CreateSubscription`jest używana toocreate subskrypcji usługi Service Bus dla tematu hello gdzie hello wewnętrznej bazy danych systemu będzie wysyłać wiadomości.</span><span class="sxs-lookup"><span data-stu-id="f16c8-164">`CreateSubscription` is used toocreate a Service Bus subscription for hello topic where hello backend system will send messages.</span></span> <span data-ttu-id="f16c8-165">W zależności od scenariusza biznesowego hello ten składnik utworzy jedną lub więcej subskrypcji tematy toocorresponding (np. niektóre może odbierać komunikaty z systemu HR, niektóre z systemu finansowego i tak dalej)</span><span class="sxs-lookup"><span data-stu-id="f16c8-165">Depending on hello business scenario, this component will create one or more subscriptions toocorresponding topics (e.g. some may be receiving messages from HR system, some from Finance system, and so on)</span></span>
   
        static void CreateSubscription(string connectionString)
        {
            // Create hello subscription if it does not exist already
            var namespaceManager =
                NamespaceManager.CreateFromConnectionString(connectionString);
   
            if (!namespaceManager.SubscriptionExists(sampleTopic, sampleSubscription))
            {
                namespaceManager.CreateSubscription(sampleTopic, sampleSubscription);
            }
        }
   
    <span data-ttu-id="f16c8-166">d.</span><span class="sxs-lookup"><span data-stu-id="f16c8-166">d.</span></span> <span data-ttu-id="f16c8-167">Wiadomości powitania tooread używanych z tematu hello przy użyciu jej subskrypcja jest ReceiveMessageAndSendNotification i w przypadku pomyślnego nawiązania hello odczytu jednostki przenośnych toohello toobe wysyłane powiadomienia (w przykładowym scenariuszu hello natywnego wyskakujących powiadomień systemu Windows) Aplikacja korzystająca z usługi Azure Notification Hubs.</span><span class="sxs-lookup"><span data-stu-id="f16c8-167">ReceiveMessageAndSendNotification is used tooread hello message from hello topic using its subscription and if hello read is successful then craft a notification (in hello sample scenario a Windows native toast notification) toobe sent toohello mobile application using Azure Notification Hubs.</span></span>
   
        static void ReceiveMessageAndSendNotification(string connectionString)
        {
            // Initialize hello Notification Hub
            string hubConnectionString = CloudConfigurationManager.GetSetting
                    ("Microsoft.NotificationHub.ConnectionString");
            hub = NotificationHubClient.CreateClientFromConnectionString
                    (hubConnectionString, "enterprisepushservicehub");
   
            SubscriptionClient Client =
                SubscriptionClient.CreateFromConnectionString
                        (connectionString, sampleTopic, sampleSubscription);
   
            Client.Receive();
   
            // Continuously process messages received from hello subscription
            while (true)
            {
                BrokeredMessage message = Client.Receive();
                var toastMessage = @"<toast><visual><binding template=""ToastText01""><text id=""1"">{messagepayload}</text></binding></visual></toast>";
   
                if (message != null)
                {
                    try
                    {
                        Console.WriteLine(message.MessageId);
                        Console.WriteLine(message.SequenceNumber);
                        string messageBody = message.GetBody<string>();
                        Console.WriteLine("Body: " + messageBody + "\n");
   
                        toastMessage = toastMessage.Replace("{messagepayload}", messageBody);
                        SendNotificationAsync(toastMessage);
   
                        // Remove message from subscription
                        message.Complete();
                    }
                    catch (Exception)
                    {
                        // Indicate a problem, unlock message in subscription
                        message.Abandon();
                    }
                }
            }
        }
        static async void SendNotificationAsync(string message)
        {
            await hub.SendWindowsNativeNotificationAsync(message);
        }
   
    <span data-ttu-id="f16c8-168">e.</span><span class="sxs-lookup"><span data-stu-id="f16c8-168">e.</span></span> <span data-ttu-id="f16c8-169">Do publikowania jako **zadania WebJob**, kliknij prawym przyciskiem myszy rozwiązanie hello w programie Visual Studio i wybierz **Publikuj jako zadanie WebJob**</span><span class="sxs-lookup"><span data-stu-id="f16c8-169">For publishing this as a **WebJob**, right click on hello solution in Visual Studio and select **Publish as WebJob**</span></span>
   
    ![][2]
   
    <span data-ttu-id="f16c8-170">f.</span><span class="sxs-lookup"><span data-stu-id="f16c8-170">f.</span></span> <span data-ttu-id="f16c8-171">Wybierz profil publikowania i tworzenia nowej witryny sieci Web platformy Azure, jeśli nie istnieje już który będzie hostem tego zadania WebJob i po utworzeniu witryny sieci Web hello następnie **publikowania**.</span><span class="sxs-lookup"><span data-stu-id="f16c8-171">Select your publishing profile and create a new Azure WebSite if it doesnt exist already which will host this WebJob and once you have hello WebSite then **Publish**.</span></span>
   
    ![][3]
   
    <span data-ttu-id="f16c8-172">g.</span><span class="sxs-lookup"><span data-stu-id="f16c8-172">g.</span></span> <span data-ttu-id="f16c8-173">Skonfiguruj hello zadanie "Uruchom stale" toobe, dzięki czemu podczas logowania w toohello [klasycznego portalu Azure] powinien zostać wyświetlony ekran podobny do następujących hello:</span><span class="sxs-lookup"><span data-stu-id="f16c8-173">Configure hello job toobe "Run Continuously" so that when you log in toohello [Azure Classic Portal] you should see something like hello following:</span></span>
   
    ![][4]
3. <span data-ttu-id="f16c8-174">**EnterprisePushMobileApp**</span><span class="sxs-lookup"><span data-stu-id="f16c8-174">**EnterprisePushMobileApp**</span></span>
   
    <span data-ttu-id="f16c8-175">a.</span><span class="sxs-lookup"><span data-stu-id="f16c8-175">a.</span></span> <span data-ttu-id="f16c8-176">To jest aplikacją ze Sklepu Windows, który będzie otrzymywać wyskakujące powiadomienia hello zadania WebJob uruchomiony jako część programu zaplecza aplikacji mobilnych i wyświetl ją.</span><span class="sxs-lookup"><span data-stu-id="f16c8-176">This is a Windows Store application which will receive toast notifications from hello WebJob running as part of your Mobile backend and display it.</span></span> <span data-ttu-id="f16c8-177">To jest oparta na [Notification Hubs — samouczek aplikacji uniwersalnych systemu Windows].</span><span class="sxs-lookup"><span data-stu-id="f16c8-177">This is based on [Notification Hubs - Windows Universal tutorial].</span></span>  
   
    <span data-ttu-id="f16c8-178">b.</span><span class="sxs-lookup"><span data-stu-id="f16c8-178">b.</span></span> <span data-ttu-id="f16c8-179">Upewnij się, że aplikacja jest włączone tooreceive wyskakujące powiadomienia.</span><span class="sxs-lookup"><span data-stu-id="f16c8-179">Ensure that your application is enabled tooreceive toast notifications.</span></span>
   
    <span data-ttu-id="f16c8-180">c.</span><span class="sxs-lookup"><span data-stu-id="f16c8-180">c.</span></span> <span data-ttu-id="f16c8-181">Upewnij się, że hello następującego kodu rejestracji usługi Notification Hubs jest wywoływana po uruchomieniu aplikacji hello (po zastąpieniu hello *HubName* i *DefaultListenSharedAccessSignature*:</span><span class="sxs-lookup"><span data-stu-id="f16c8-181">Ensure that hello following Notification Hubs registration code is being called at hello App start up (after replacing hello *HubName* and *DefaultListenSharedAccessSignature*:</span></span>
   
        private async void InitNotificationsAsync()
        {
            var channel = await PushNotificationChannelManager.CreatePushNotificationChannelForApplicationAsync();
   
            var hub = new NotificationHub("[HubName]", "[DefaultListenSharedAccessSignature]");
            var result = await hub.RegisterNativeAsync(channel.Uri);
   
            // Displays hello registration ID so you know it was successful
            if (result.RegistrationId != null)
            {
                var dialog = new MessageDialog("Registration successful: " + result.RegistrationId);
                dialog.Commands.Add(new UICommand("OK"));
                await dialog.ShowAsync();
            }
        }

### <a name="running-sample"></a><span data-ttu-id="f16c8-182">Uruchamianie przykładowych:</span><span class="sxs-lookup"><span data-stu-id="f16c8-182">Running sample:</span></span>
1. <span data-ttu-id="f16c8-183">Upewnij się, że WebJob działa prawidłowo i zaplanowane zbyt "Uruchamiaj stale".</span><span class="sxs-lookup"><span data-stu-id="f16c8-183">Ensure that your WebJob is running successfully and scheduled too"Run Continuously".</span></span>
2. <span data-ttu-id="f16c8-184">Uruchom hello **EnterprisePushMobileApp** rozpocząć aplikacji ze Sklepu Windows hello.</span><span class="sxs-lookup"><span data-stu-id="f16c8-184">Run hello **EnterprisePushMobileApp** which will start hello Windows Store app.</span></span>
3. <span data-ttu-id="f16c8-185">Uruchom hello **EnterprisePushBackendSystem** aplikacji konsoli, która będzie symulować hello LoB wewnętrznej bazy danych i rozpocznie się wysyłanie wiadomości i powinna zostać wyświetlona wyskakujące powiadomienia znajdujących się podobnie następującej hello:</span><span class="sxs-lookup"><span data-stu-id="f16c8-185">Run hello **EnterprisePushBackendSystem** console application which will simulate hello LoB backend and will start sending messages and you should see toast notifications appearing like hello following:</span></span>
   
    ![][5]
4. <span data-ttu-id="f16c8-186">wiadomości powitania pierwotnie zostały wysłane tooService magistrali tematy, które monitorowanym przez subskrypcje usługi Service Bus w zadanie sieci Web.</span><span class="sxs-lookup"><span data-stu-id="f16c8-186">hello messages were originally sent tooService Bus topics which was being monitored by Service Bus subscriptions in your Web Job.</span></span> <span data-ttu-id="f16c8-187">Po Odebrano komunikat powiadomienia została tworzonych i wysyłanych toohello aplikacji mobilnej.</span><span class="sxs-lookup"><span data-stu-id="f16c8-187">Once a message was received, a notification was created and sent toohello mobile app.</span></span> <span data-ttu-id="f16c8-188">Można sprawdzić za pomocą hello zadania WebJob dzienniki tooconfirm hello przetwarzania po przejściu toohello dzienniki łącze w [klasycznego portalu Azure] dla zadania sieci Web:</span><span class="sxs-lookup"><span data-stu-id="f16c8-188">You can look through hello WebJob logs tooconfirm hello processing when you go toohello Logs link in [Azure Classic Portal] for your Web Job:</span></span>
   
    ![][6]

<!-- Images -->
[1]: ./media/notification-hubs-enterprise-push-architecture/architecture.png
[2]: ./media/notification-hubs-enterprise-push-architecture/WebJobsContextMenu.png
[3]: ./media/notification-hubs-enterprise-push-architecture/PublishAsWebJob.png
[4]: ./media/notification-hubs-enterprise-push-architecture/WebJob.png
[5]: ./media/notification-hubs-enterprise-push-architecture/Notifications.png
[6]: ./media/notification-hubs-enterprise-push-architecture/WebJobsLog.png

<!-- Links -->
[przykłady Centrum powiadomień]: https://github.com/Azure/azure-notificationhubs-samples
[usługi mobilnej Azure]: http://azure.microsoft.com/documentation/services/mobile-services/
[Azure Service Bus]: http://azure.microsoft.com/documentation/articles/fundamentals-service-bus-hybrid-solutions/
[programowania magistrali usługi Pub/Sub]: http://azure.microsoft.com/documentation/articles/service-bus-dotnet-how-to-use-topics-subscriptions/
[zadań WebJob Azure]: http://azure.microsoft.com/documentation/articles/web-sites-create-web-jobs/
[Notification Hubs — samouczek aplikacji uniwersalnych systemu Windows]: http://azure.microsoft.com/documentation/articles/notification-hubs-windows-store-dotnet-get-started/
[klasycznego portalu Azure]: https://manage.windowsazure.com/
