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
# <a name="enterprise-push-architectural-guidance"></a>Wskazówki dotyczące architektury powiadomień wypychanych w przedsiębiorstwie
Dzisiaj przedsiębiorstwa są stopniowo przenoszenie do tworzenia aplikacji dla urządzeń przenośnych dla dowolnego użytkownikom końcowym (zewnętrzne) lub dla pracowników hello (wewnętrzny). Mają one istniejącymi systemami wewnętrznej bazy danych w miejscu, można go Komputery mainframe firmy lub niektóre aplikacje LoB, które muszą zostać włączone do hello architektury aplikacji mobilnej. W tym przewodniku zostaną omówione toodo najlepszego integracja rekomendowania możliwe rozwiązanie toocommon scenariuszy.

Jest wymagane częste do wysyłania powiadomień toohello użytkowników za pomocą ich aplikacji mobilnej wypychania po wystąpieniu zdarzenia zainteresowania w systemach zaplecza hello. Na przykład Klient bank, który jest aplikacja bankowa hello bank na swoim telefonie iPhone chce toobe powiadomienie, gdy debetowa staje się powyżej pewnego swoje konto lub scenariusz sieci intranet, gdzie pracowników z działu finansowego mającego aplikacji zatwierdzenia budżetu na jego Windows Phone, który chce toobe powiadomienie, gdy uzyskuje on żądanie zatwierdzenia.

konta bankowego Hello lub przetwarzania zatwierdzenia jest prawdopodobnie toobe wykonywane w niektórych systemie wewnętrznej bazy danych, w którym konieczne jest zainicjowanie użytkownika toohello wypychania. Może istnieć wiele takich zaplecza systemów, które muszą wszystkie kompilacji hello sam rodzaj logiki tooimplement wypychania, gdy zdarzenie jest wyzwalane powiadomienie. złożoność Hello tutaj znajduje się w integrowania kilka systemów wewnętrznej bazy danych wraz z systemu pojedynczego wypychania, gdzie hello użytkownikom końcowym masz subskrypcję powiadomień toodifferent i może nawet być wiele aplikacji mobilnych, np. w przypadku hello aplikacji mobilnych w sieci intranet gdzie jednej aplikacji mobilnej można tooreceive powiadomienia z wielu takich systemów zaplecza. systemy zaplecza Hello nie znasz lub muszą mieć tooknow wypychania semantyki/technologii umożliwiające rozwiązanie typowych tutaj tradycyjnie była toointroduce składnika, który sonduje systemów zaplecza hello wszystkie zdarzenia odsetek i jest odpowiedzialny za wysyłanie wiadomości wypychanych powitania toohello klienta.
W tym polu, zostaną omawianiu nawet lepszym rozwiązaniem przy użyciu usługi Azure Service Bus - modelu tematu/subskrypcji, który zostanie zredukowana złożoność hello jednocześnie skalowalne rozwiązanie hello.

Oto hello ogólne architektury rozwiązania hello (uogólniony z wielu aplikacji mobilnych ale również mają zastosowanie, gdy istnieje tylko jeden aplikacji mobilnej)

## <a name="architecture"></a>Architektura
![][1]

część klucza Hello na tym diagramie architektury jest Azure Service Bus, która zapewnia model programowania tematy/subskrypcji (więcej informacji na temat go w [programowania magistrali usługi Pub/Sub]). odbiornik Hello, w tym przypadku jest hello zaplecza aplikacji mobilnych (zazwyczaj [usługi mobilnej Azure], inicjuje wypychanych aplikacji mobilnych toohello) nie odbierać komunikaty bezpośrednio z systemów zaplecza hello, ale zamiast tego mamy warstwy abstrakcji pośredniego dostarczonych przez [Azure Service Bus] co pozwala komunikaty tooreceive zaplecza aplikacji mobilnych z jednego lub kilku systemów zaplecza. Temat magistrali usług musi toobe tworzone dla poszczególnych systemów hello zaplecza np. konta, HR, finansowych, które są po prostu "tematów", który będzie inicjował toobe wiadomości wysyłane jako powiadomienie wypychane. systemy zaplecza Hello wyśle komunikaty toothese tematów. Zaplecza Mobile można zasubskrybować tooone lub więcej takich tematy podczas tworzenia subskrypcji usługi Service Bus. Spowoduje to uprawniają hello zaplecze aplikacji mobilnej tooreceive powiadomienie z hello odpowiedniej wewnętrznej bazy danych systemu. Zaplecze aplikacji mobilnej nadal toolisten wiadomości na ich subskrypcji i zaraz po odebraniu komunikatu Przechodzi wstecz i wysyła je jako centrum powiadomień tooits powiadomień. Następnie usługi Notification hubs zapewnia ostatecznie aplikacji mobilnej toohello wiadomość hello. Dlatego toosummarize hello najważniejsze składniki mamy:

1. Systemy zaplecza (LoB/starsze systemy)
   * Tworzy temat magistrali usług
   * Wysyła komunikat
2. Zaplecze mobilne
   * Tworzy subskrypcji usługi
   * Odbiera komunikat (z wewnętrznej bazy danych systemu)
   * Wysyła powiadomienia tooclients (za pośrednictwem Centrum powiadomień Azure)
3. Aplikacji mobilnej
   * Odbiera i wyświetlania powiadomień

### <a name="benefits"></a>Korzyści:
1. rozdzielenie Hello hello odbiornika (aplikacji/usługi mobilnej za pośrednictwem Centrum powiadomień) i nadawcy (systemy zaplecza) umożliwia systemów dodatkowe wewnętrznej bazy danych jest zintegrowany z minimalnym zmiany.
2. Ułatwia to też hello scenariusz wiele aplikacji mobilnych, jest w stanie tooreceive zdarzeń z jednego lub kilku systemów zaplecza.  

## <a name="sample"></a>Przykład:
### <a name="prerequisites"></a>Wymagania wstępne
Należy wykonać hello następujące samouczki toofamiliarize z założenia hello, a także typowe kroki tworzenia i konfiguracji:

1. [programowania magistrali usługi Pub/Sub] — w tej sekcji wyjaśniono hello szczegółowe informacje dotyczące pracy z tematów magistrali usługi/subskrypcji, jak toocreate przestrzeni nazw toocontain tematy/subskrypcji, jak toosend & odbierać komunikaty z nich.
2. [Notification Hubs — samouczek aplikacji uniwersalnych systemu Windows] — w tej sekcji wyjaśniono, jak tooset Konfigurowanie aplikacji ze Sklepu Windows i używać usługi Notification Hubs tooregister i będzie otrzymywać powiadomienia.

### <a name="sample-code"></a>Przykładowy kod
Kod pełny przykład Hello jest dostępny w [przykłady Centrum powiadomień]. Są one podzielone na trzy składniki:

1. **EnterprisePushBackendSystem**
   
    a. Ten projekt używa hello *WindowsAzure.ServiceBus* pakietu Nuget i jest oparty na [programowania magistrali usługi Pub/Sub].
   
    b. Jest to prosty C# console aplikacji toosimulate systemu LoB, która inicjuje toobe wiadomość hello dostarczyć toohello aplikacji mobilnej.
   
        static void Main(string[] args)
        {
            string connectionString =
                CloudConfigurationManager.GetSetting("Microsoft.ServiceBus.ConnectionString");
   
            // Create hello topic where we will send notifications
            CreateTopic(connectionString);
   
            // Send message
            SendMessage(connectionString);
        }
   
    c. `CreateTopic`jest tematu usługi Service Bus hello toocreate używany gdzie możemy wysłać wiadomości.
   
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
   
    d. `SendMessage`jest toothis wiadomości powitania toosend używanych tematów magistrali usługi. Firma Microsoft tutaj po prostu wysyłania zestaw tematu toohello losowe wiadomości okresowo w celu hello hello próbki. Zwykle będzie systemu wewnętrznej bazy danych, która będzie wysyłać wiadomości, gdy wystąpi zdarzenie.
   
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
2. **ReceiveAndSendNotification**
   
    a. Ten projekt używa hello *WindowsAzure.ServiceBus* i *Microsoft.Web.WebJobs.Publish* Nuget pakietów i jest oparty na [programowania magistrali usługi Pub/Sub].
   
    b. Jest to inny C# console aplikacji, która zostanie uruchomiony jako [zadań WebJob Azure] ponieważ stale ma toorun toolisten dla komunikatów z systemów LoB/zaplecza hello. Są to część z zaplecza aplikacji mobilnych.
   
        static void Main(string[] args)
        {
            string connectionString =
                     CloudConfigurationManager.GetSetting("Microsoft.ServiceBus.ConnectionString");
   
            // Create hello subscription which will receive messages
            CreateSubscription(connectionString);
   
            // Receive message
            ReceiveMessageAndSendNotification(connectionString);
        }
   
    c. `CreateSubscription`jest używana toocreate subskrypcji usługi Service Bus dla tematu hello gdzie hello wewnętrznej bazy danych systemu będzie wysyłać wiadomości. W zależności od scenariusza biznesowego hello ten składnik utworzy jedną lub więcej subskrypcji tematy toocorresponding (np. niektóre może odbierać komunikaty z systemu HR, niektóre z systemu finansowego i tak dalej)
   
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
   
    d. Wiadomości powitania tooread używanych z tematu hello przy użyciu jej subskrypcja jest ReceiveMessageAndSendNotification i w przypadku pomyślnego nawiązania hello odczytu jednostki przenośnych toohello toobe wysyłane powiadomienia (w przykładowym scenariuszu hello natywnego wyskakujących powiadomień systemu Windows) Aplikacja korzystająca z usługi Azure Notification Hubs.
   
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
   
    e. Do publikowania jako **zadania WebJob**, kliknij prawym przyciskiem myszy rozwiązanie hello w programie Visual Studio i wybierz **Publikuj jako zadanie WebJob**
   
    ![][2]
   
    f. Wybierz profil publikowania i tworzenia nowej witryny sieci Web platformy Azure, jeśli nie istnieje już który będzie hostem tego zadania WebJob i po utworzeniu witryny sieci Web hello następnie **publikowania**.
   
    ![][3]
   
    g. Skonfiguruj hello zadanie "Uruchom stale" toobe, dzięki czemu podczas logowania w toohello [klasycznego portalu Azure] powinien zostać wyświetlony ekran podobny do następujących hello:
   
    ![][4]
3. **EnterprisePushMobileApp**
   
    a. To jest aplikacją ze Sklepu Windows, który będzie otrzymywać wyskakujące powiadomienia hello zadania WebJob uruchomiony jako część programu zaplecza aplikacji mobilnych i wyświetl ją. To jest oparta na [Notification Hubs — samouczek aplikacji uniwersalnych systemu Windows].  
   
    b. Upewnij się, że aplikacja jest włączone tooreceive wyskakujące powiadomienia.
   
    c. Upewnij się, że hello następującego kodu rejestracji usługi Notification Hubs jest wywoływana po uruchomieniu aplikacji hello (po zastąpieniu hello *HubName* i *DefaultListenSharedAccessSignature*:
   
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

### <a name="running-sample"></a>Uruchamianie przykładowych:
1. Upewnij się, że WebJob działa prawidłowo i zaplanowane zbyt "Uruchamiaj stale".
2. Uruchom hello **EnterprisePushMobileApp** rozpocząć aplikacji ze Sklepu Windows hello.
3. Uruchom hello **EnterprisePushBackendSystem** aplikacji konsoli, która będzie symulować hello LoB wewnętrznej bazy danych i rozpocznie się wysyłanie wiadomości i powinna zostać wyświetlona wyskakujące powiadomienia znajdujących się podobnie następującej hello:
   
    ![][5]
4. wiadomości powitania pierwotnie zostały wysłane tooService magistrali tematy, które monitorowanym przez subskrypcje usługi Service Bus w zadanie sieci Web. Po Odebrano komunikat powiadomienia została tworzonych i wysyłanych toohello aplikacji mobilnej. Można sprawdzić za pomocą hello zadania WebJob dzienniki tooconfirm hello przetwarzania po przejściu toohello dzienniki łącze w [klasycznego portalu Azure] dla zadania sieci Web:
   
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
