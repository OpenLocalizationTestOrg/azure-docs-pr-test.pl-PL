---
title: "aaaCreate aplikacji, które używają usługi Azure Service Bus tematów i subskrypcji | Dokumentacja firmy Microsoft"
description: "Wprowadzenie toohello możliwości publikowania / subskrypcji oferowanych przez usługi Service Bus tematów i subskrypcji."
services: service-bus-messaging
documentationcenter: na
author: sethmanheim
manager: timlt
editor: 
ms.assetid: a48fc9b0-b7b0-464e-8187-a517bf8b4eb4
ms.service: service-bus-messaging
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 04/07/2017
ms.author: sethm
ms.openlocfilehash: f6d7de46ace7bd5b49de612db213ced789308d91
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-applications-that-use-service-bus-topics-and-subscriptions"></a>Tworzenie aplikacji korzystających z usługi Service Bus tematów i subskrypcji
Usługa Azure Service Bus obsługuje zestaw technologii chmurowych, zorientowany oprogramowanie pośredniczące, takich jak usługi kolejkowania komunikatów niezawodnej i trwałe publikowania/subskrybowania komunikatów. W tym artykule opiera się na powitania informacji dostępnych w [tworzenie aplikacji korzystających z kolejek usługi Service Bus](service-bus-create-queues.md) i oferuje wprowadzenie możliwości publikowania/subskrybowania toohello oferowane przez tematów usługi Service Bus.

## <a name="evolving-retail-scenario"></a>Scenariusz sprzedaży detalicznej zmieniające się
W tym artykule nadal używany w scenariuszu sprzedaży detalicznej hello [tworzenie aplikacji korzystających z kolejek usługi Service Bus](service-bus-create-queues.md). Odwołaj się, że danych sprzedaży z poszczególnych terminali w punkcie sprzedaży (POS) musi być kierowany tooan systemu zarządzania spisem, używający tego toodetermine danych giełdowych po toobe uzupełniona. Każdy terminal POS raporty jego danych sprzedaży przez wysłanie wiadomości toohello **DataCollectionQueue** kolejki, gdzie są one nadal aż otrzymuje hello systemu zarządzania spisem, jak pokazano poniżej:

![Usługa Service Bus 1](./media/service-bus-create-topics-subscriptions/IC657161.gif)

tooevolve tego scenariusza, nowe wymaganie został dodany systemu toohello: hello właściciela sklepu chce toobe toomonitor stanie jak hello magazynu działa w czasie rzeczywistym.

tooaddress to wymaganie systemu hello musi "Wybierz" poza hello strumienia danych sprzedaży. Każdy komunikat wysyłany przez toobe Terminale POS hello wysyłane toohello systemu zarządzania spisem jako przed chcemy się nadal, ale chcemy innej kopii każdej wiadomości, że możemy użyć właściciela sklepu toohello widoku pulpitu nawigacyjnego toopresent hello.

W każdej sytuacji, takich jak ta, w której wymagają każdego toobe komunikat używane przez wiele stron, można użyć usługi Service Bus *tematy*. Wzorzec publikowania/subskrypcji, w którym każdy opublikowany komunikat staje się dostępna tooone lub więcej subskrypcji zarejestrowanej temacie hello tematach. Z kolei w przypadku kolejek każdy komunikat jest odbierany przez jednego konsumenta.

Komunikaty są wysyłane tooa tematu w hello sam sposób, jak są one wysyłane tooa kolejki. Jednak nie odbiera wiadomości z tematu hello bezpośrednio; zostały odebrane z subskrypcji. Temat tooa subskrypcji można traktować jako wirtualną kolejkę, która odbiera kopie wiadomości powitania, które są wysyłane toothat tematu. Komunikaty są odbierane z subskrypcji hello sam sposób, jak zostały odebrane z kolejki.

Cofnięcie scenariusz sprzedaży detalicznej toohello kolejki hello zastępuje tematu i subskrypcji zostanie dodany, który składnik systemu hello spisu zarządzania można użyć. Hello system pojawi się teraz w następujący sposób:

![Usługa Service Bus 2](./media/service-bus-create-topics-subscriptions/IC657165.gif)

tutaj konfiguracji Hello tak samo wykonuje toohello poprzedniego kolejki na podstawie projektu. Oznacza to, komunikaty wysyłane toohello tematu są routingiem toohello **spisu** subskrypcji, z których hello **systemu zarządzania spisem** je wykorzystuje.

W kolejności toosupport hello pulpit nawigacyjny zarządzania utworzymy drugi subskrypcji na temat hello, jak pokazano poniżej:

![Usługa Service Bus 3](./media/service-bus-create-topics-subscriptions/IC657166.gif)

W tej konfiguracji każdego komunikatu z terminali hello POS nawiązuje hello dostępne tooboth **pulpitu nawigacyjnego** i **spisu** subskrypcji.

## <a name="show-me-hello-code"></a>Pokaż hello kodu
Artykuł Hello [tworzenie aplikacji korzystających z kolejek usługi Service Bus](service-bus-create-queues.md) w tym artykule opisano sposób toosign Konfigurowanie konta platformy Azure i tworzenia przestrzeni nazw usługi. zależnościami usługi Service Bus tooreference Najprostszym sposobem Hello jest hello tooinstall usługi Service Bus [pakietu Nuget](https://www.nuget.org/packages/WindowsAzure.ServiceBus/). Można również znaleźć hello bibliotek usługi Service Bus jako część hello Azure SDK. Witaj pobierane są dostępne pod adresem hello [strona pobierania zestawu Azure SDK](https://azure.microsoft.com/downloads/).

### <a name="create-hello-topic-and-subscriptions"></a>Utwórz hello tematu i subskrypcji
Operacje zarządzania dla usługi Service Bus jednostek obsługi komunikatów (kolejki i publikowania/subskrypcji tematy) są wykonywane za pośrednictwem hello [NamespaceManager](/dotnet/api/microsoft.servicebus.namespacemanager#microsoft_servicebus_namespacemanager) klasy. Odpowiednie poświadczenia są wymagane w kolejności toocreate **NamespaceManager** wystąpienia określonego obszaru nazw. Usługa Service Bus używa [dostępu sygnatury dostępu Współdzielonego](service-bus-sas.md) na podstawie modelu zabezpieczeń. Witaj [TokenProvider](/dotnet/api/microsoft.servicebus.tokenprovider#microsoft_servicebus_tokenprovider) klasa reprezentuje dostawcę tokenu zabezpieczającego z wbudowanymi metodami factory zwracanie niektórych dobrze znanych dostawców tokenu. Użyjemy [CreateSharedAccessSignatureTokenProvider](/dotnet/api/microsoft.servicebus.tokenprovider#Microsoft_ServiceBus_TokenProvider_CreateSharedAccessSignatureTokenProvider_System_String_) poświadczeń sygnatury dostępu Współdzielonego hello toohold metody. Witaj [NamespaceManager](/dotnet/api/microsoft.servicebus.namespacemanager#microsoft_servicebus_namespacemanager) wystąpienia następnie jest tworzony z hello adresu podstawowego przestrzeni nazw usługi Service Bus hello oraz hello dostawcy tokenu.

Witaj [NamespaceManager](/dotnet/api/microsoft.servicebus.namespacemanager#microsoft_servicebus_namespacemanager) klasa dostarcza metody toocreate, wyliczania i usuwania jednostek obsługi komunikatów. Witaj kod, który jest wyświetlany w tym miejscu przedstawiono sposób hello **NamespaceManager** wystąpienie jest utworzony i używany toocreate hello **DataCollectionTopic** tematu.

```csharp
Uri uri = ServiceBusEnvironment.CreateServiceUri("sb", "test-blog", string.Empty);
string name = "RootManageSharedAccessKey";
string key = "abcdefghijklmopqrstuvwxyz";

TokenProvider tokenProvider = TokenProvider.CreateSharedAccessSignatureTokenProvider(name, key);
NamespaceManager namespaceManager = new NamespaceManager(uri, tokenProvider);

namespaceManager.CreateTopic("DataCollectionTopic");
```

Należy pamiętać, że istnieją przeciążenia metody hello [CreateTopic](/dotnet/api/microsoft.servicebus.namespacemanager#Microsoft_ServiceBus_NamespaceManager_CreateTopic_System_String_) metody umożliwiające właściwości tooset hello tematu. Na przykład można ustawić hello time to live (TTL) wartość domyślna dla wiadomości wysyłanych toohello tematu. Następnie dodaj hello **spisu** i **pulpitu nawigacyjnego** subskrypcji.

```csharp
namespaceManager.CreateSubscription("DataCollectionTopic", "Inventory");
namespaceManager.CreateSubscription("DataCollectionTopic", "Dashboard");
```

### <a name="send-messages-toohello-topic"></a>Wysyłanie wiadomości toohello tematu
Dla czasu wykonywania operacji na jednostek usługi Service Bus; na przykład wysyłanie i odbieranie wiadomości, aplikacja musi najpierw utworzyć [MessagingFactory](/dotnet/api/microsoft.servicebus.messaging.messagingfactory#microsoft_servicebus_messaging_messagingfactory) obiektu. Podobne toohello [NamespaceManager](/dotnet/api/microsoft.servicebus.namespacemanager#microsoft_servicebus_namespacemanager) klasy, hello **MessagingFactory** z adresu podstawowego hello hello przestrzeni nazw usługi i dostawcy tokenów hello jest tworzone wystąpienie.

```
MessagingFactory factory = MessagingFactory.Create(uri, tokenProvider);
```

Tooand wiadomości otrzymanych od tematów usługi Service Bus są wystąpieniami klasy hello [BrokeredMessage](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage) klasy. Ta klasa zawiera zestaw właściwości standardowych (takich jak [etykiety](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage.label?view=azureservicebus-4.0.0#Microsoft_ServiceBus_Messaging_BrokeredMessage_Label) i [TimeToLive](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage.timetolive?view=azureservicebus-4.0.0#Microsoft_ServiceBus_Messaging_BrokeredMessage_TimeToLive)), słownik, który jest używany toohold właściwości aplikacji oraz treść dowolnych danych aplikacji. Aplikacja możne ustawić treść hello przez przekazanie dowolnego obiektu podlegającego serializacji (hello w poniższym przykładzie przekazuje w **SalesData** obiekt, który reprezentuje hello danych sprzedaży z terminalu hello POS), który będzie używany hello [ DataContractSerializer](https://msdn.microsoft.com/library/system.runtime.serialization.datacontractserializer.aspx) tooserialize hello obiektu. Alternatywnie [strumienia](https://msdn.microsoft.com/library/system.io.stream.aspx) można podać obiektu.

```csharp
BrokeredMessage bm = new BrokeredMessage(salesData);
bm.Label = "SalesReport";
bm.Properties["StoreName"] = "Redmond";
bm.Properties["MachineID"] = "POS_1";
```

Witaj najprostszy sposób toosend wiadomości toohello temat jest toouse [CreateMessageSender](/dotnet/api/microsoft.servicebus.messaging.messagingfactory#Microsoft_ServiceBus_Messaging_MessagingFactory_CreateMessageSender_System_String_) toocreate [MessageSender](/dotnet/api/microsoft.servicebus.messaging.messagesender) obiekt bezpośrednio hello [MessagingFactory](/dotnet/api/microsoft.servicebus.messaging.messagingfactory) wystąpienie:

```csharp
MessageSender sender = factory.CreateMessageSender("DataCollectionTopic");
sender.Send(bm);
```

### <a name="receive-messages-from-a-subscription"></a>Odbieranie komunikatów z subskrypcji
Podobne kolejek toousing, tooreceive komunikatów z subskrypcji można użyć [MessageReceiver](/dotnet/api/microsoft.servicebus.messaging.messagereceiver) obiektów, które można tworzyć bezpośrednio z hello [MessagingFactory](/dotnet/api/microsoft.servicebus.messaging.messagingfactory) przy użyciu [ CreateMessageReceiver](/dotnet/api/microsoft.servicebus.messaging.messagingfactory#Microsoft_ServiceBus_Messaging_MessagingFactory_CreateMessageReceiver_System_String_). Można użyć jednej z hello odbierania dwa różne tryby (**ReceiveAndDelete** i **PeekLock**), zgodnie z opisem w [tworzenie aplikacji korzystających z kolejek usługi Service Bus](service-bus-create-queues.md).

Należy pamiętać, że podczas tworzenia **MessageReceiver** subskrypcji, hello *entityPath* parametr ma formę hello `topicPath/subscriptions/subscriptionName`. W związku z tym toocreate **MessageReceiver** dla hello **spisu** subskrypcji hello **DataCollectionTopic** tematu, *entityPath*musi być ustawiona zbyt`DataCollectionTopic/subscriptions/Inventory`. Kod Hello wygląda następująco:

```csharp
MessageReceiver receiver = factory.CreateMessageReceiver("DataCollectionTopic/subscriptions/Inventory");
BrokeredMessage receivedMessage = receiver.Receive();
try
{
    ProcessMessage(receivedMessage);
    receivedMessage.Complete();
}
catch (Exception e)
{
    receivedMessage.Abandon();
}
```

## <a name="subscription-filters"></a>Filtry subskrypcji
Do tej pory w tym scenariuszu wszystkich wiadomości wysłanych toohello tematu są nawiązywane subskrypcje dostępne tooall zarejestrowany. Hello tutaj klucza frazy "udostępniono." Podczas subskrypcje usługi Service Bus, zobacz wszystkich wiadomości wysłanych toohello tematu, możesz skopiować tylko podzbiór tych kolejki subskrypcji wirtualnego toohello wiadomości. To jest wykonywane przy użyciu subskrypcji *filtry*. Podczas tworzenia subskrypcji, możesz podać wyrażenie filtru w postaci hello predykatu styl SQL92 działającą za pośrednictwem właściwości hello wiadomości powitania, zarówno hello właściwości systemu (na przykład [etykiety](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_Label)) i aplikacji hello właściwości, takie jak **StoreName** w poprzednim przykładzie hello.

To rozwijają tooillustrate scenariusza hello, drugi magazynu jest scenariusz sprzedaży detalicznej dodane tooour toobe. Sprzedaży danych ze wszystkich hello POS terminali z obu sklepów jeszcze systemu zarządzania spisem toohello scentralizowane toobe kierowane Menedżera magazynu przy użyciu narzędzia pulpitu nawigacyjnego hello jest jednak tylko zainteresowana hello wydajność tego magazynu. Możesz użyć filtrowania tooachieve to subskrypcji. Należy zauważyć, że terminale hello POS publikowania wiadomości, ich hello **StoreName** właściwości aplikację na wiadomość powitania. Podane dwóch magazynów, na przykład **Redmond** i **Seattle**, hello POS terminali w hello Redmond przechowywania sygnatury komunikatów ich danych sprzedaży z **StoreName** równa zbyt **Redmond**, podczas gdy hello Seattle przechowywania Użyj Terminale POS **StoreName** równa zbyt**Seattle**. Menedżera magazynu Hello hello Redmond przechowywać tylko chce toosee danych z terminali w punkcie sprzedaży. Hello system wygląda następująco:

![Usługa Bus4](./media/service-bus-create-topics-subscriptions/IC657167.gif)

tooset się marszruty, Utwórz hello **pulpitu nawigacyjnego** subskrypcji w następujący sposób:

```csharp
SqlFilter dashboardFilter = new SqlFilter("StoreName = 'Redmond'");
namespaceManager.CreateSubscription("DataCollectionTopic", "Dashboard", dashboardFilter);
```

Z tym [filtr subskrypcji](/dotnet/api/microsoft.servicebus.messaging.sqlfilter), tylko komunikaty, które mają hello **StoreName** właściwość zbyt**Redmond** zostaną skopiowane toohello wirtualnego kolejki hello **Pulpitu nawigacyjnego** subskrypcji. Znacznie więcej toosubscription filtrowania, jednak nie istnieje. Aplikacje mogą mieć wiele reguł filtru na subskrypcję dodanie toohello możliwości toomodify hello właściwości wiadomości, kiedy przechodzi on wirtualnej kolejki subskrypcji tooa.

## <a name="summary"></a>Podsumowanie
Wszystkie usługi kolejkowania toouse powodów hello opisanego w [tworzenie aplikacji korzystających z kolejek usługi Service Bus](service-bus-create-queues.md) mają zastosowanie również tootopics, w szczególności:

* Oddzielenia czasowego — komunikatów, producenci i konsumenci nie mają toobe w trybie online na powitania tym samym czasie.
* Wyrównywanie obciążenia — szczytów obciążenia są wygładzania według tematów hello włączenie odbierającą toobe aplikacje udostępnione średni obciążenia zamiast obciążenia szczytowego.
* Równoważenie obciążenia — podobne tooa kolejka, może mieć wielu konkurujących konsumentów nasłuchiwania na jedną subskrypcją, w każdej wiadomości przekazane tooonly konsumentów hello, w tym samym równoważenia obciążenia.
* Luźne powiązanie — można rozwijać hello wiadomości sieci bez wpływu na istniejące punkty końcowe; na przykład dodawania subskrypcji lub zmiana tooallow tematu tooa filtry dla nowych klientów.

## <a name="next-steps"></a>Następne kroki

Zobacz [tworzenie aplikacji korzystających z kolejek usługi Service Bus](service-bus-create-queues.md) uzyskać informacji na temat sposobu toouse kolejki w scenariuszu detalicznej hello POS.

