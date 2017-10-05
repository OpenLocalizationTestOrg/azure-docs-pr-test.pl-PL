---
title: "Tworzenie aplikacji korzystających z tematów i subskrypcji Azure Service Bus | Dokumentacja firmy Microsoft"
description: "Wprowadzenie do publikacji-subskrypcji możliwości oferowane przez usługi Service Bus tematów i subskrypcji."
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
ms.openlocfilehash: eb01120ce9578f716e5381c107faa93f0b36e358
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/18/2017
---
# <a name="create-applications-that-use-service-bus-topics-and-subscriptions"></a>Tworzenie aplikacji korzystających z usługi Service Bus tematów i subskrypcji
Usługa Azure Service Bus obsługuje zestaw technologii chmurowych, zorientowany oprogramowanie pośredniczące, takich jak usługi kolejkowania komunikatów niezawodnej i trwałe publikowania/subskrybowania komunikatów. W tym artykule opiera się na informacji dostępnych w [tworzenie aplikacji korzystających z kolejek usługi Service Bus](service-bus-create-queues.md) i oferuje wprowadzenie do publikowania/subskrypcji możliwości oferowane przez tematów usługi Service Bus.

## <a name="evolving-retail-scenario"></a>Scenariusz sprzedaży detalicznej zmieniające się
W tym artykule nadal scenariusz sprzedaży detalicznej używane w [tworzenie aplikacji korzystających z kolejek usługi Service Bus](service-bus-create-queues.md). Odwołaj danych sprzedaży z poszczególnych punktu z sprzedaży (POS) terminale muszą być kierowane do systemu zarządzania spisem, który używa tych danych do określania, kiedy ma być uzupełniona zasobów. Każdy terminal POS raporty jego danych sprzedaży przez wysyłanie komunikatów do **DataCollectionQueue** kolejki, gdy są one nadal dopóki nie zostaną odebrane z magazynu systemu zarządzania, jak pokazano poniżej:

![Usługa Service Bus 1](./media/service-bus-create-topics-subscriptions/IC657161.gif)

Podlegać ewolucji w tym scenariuszu, do systemu dodano nowe wymaganie: właściciela sklepu chce mieć możliwość monitorowania, jak magazyn działa w czasie rzeczywistym.

W celu rozwiązania tego wymagania, system musi "naciśnij przycisk" Wyłącz strumienia danych sprzedaży. Każdy komunikat wysyłany przez Terminale POS do wysłania do systemu zarządzania spisu jako przed chcemy się nadal, ale chcemy innej kopii każdej wiadomości, które firma Microsoft służy do prezentowania widoku pulpitu nawigacyjnego do właściciela sklepu.

W każdej sytuacji, takich jak ta, w której wymagają każdy komunikat jest używane przez wiele stron, można użyć usługi Service Bus *tematy*. Tematy zawierają wzorzec publikowania/subskrypcji, w którym każdy opublikowany komunikat jest udostępniony dla przynajmniej jednej subskrypcji zarejestrowanej w temacie. Z kolei w przypadku kolejek każdy komunikat jest odbierany przez jednego konsumenta.

Komunikaty są wysyłane do tematu w taki sam sposób jak te są wysyłane do kolejki. Jednak nie odbiera wiadomości z tematu bezpośrednio; zostały odebrane z subskrypcji. Można potraktować subskrypcję tematu jako wirtualną kolejkę, która odbiera kopie komunikatów, które są wysyłane do tego tematu. Komunikaty są odbierane z subskrypcji samo są odbierane z kolejki.

Po powrocie do scenariusza sieci sprzedaży, kolejki zastępuje tematu i subskrypcji zostanie dodany, którego można użyć składnika systemu zarządzania spisu. System pojawi się teraz w następujący sposób:

![Usługa Service Bus 2](./media/service-bus-create-topics-subscriptions/IC657165.gif)

Konfiguracji przeprowadza się tak samo do poprzedniego projekt na podstawie kolejki. Oznacza to, że komunikaty wysłane do tematu są kierowane do **spisu** subskrypcji, z którego **systemu zarządzania spisem** je wykorzystuje.

Aby zapewnić obsługę pulpit nawigacyjny zarządzania, utworzymy drugi subskrypcję tematu, jak pokazano poniżej:

![Usługa Service Bus 3](./media/service-bus-create-topics-subscriptions/IC657166.gif)

W tej konfiguracji, ma zostać udostępnione zarówno każdy komunikat z Terminale POS **pulpitu nawigacyjnego** i **spisu** subskrypcji.

## <a name="show-me-the-code"></a>Pokaż kod
Artykuł [tworzenie aplikacji korzystających z kolejek usługi Service Bus](service-bus-create-queues.md) opisano, jak utworzyć konta platformy Azure i tworzenia przestrzeni nazw usługi. Najprostszym sposobem odwołania zależnościami usługi Service Bus jest zainstalowanie usługi Service Bus [pakietu Nuget](https://www.nuget.org/packages/WindowsAzure.ServiceBus/). Można również znaleźć bibliotek usługi Service Bus jako część zestawu Azure SDK. Dane pobierane są dostępne pod adresem [strona pobierania zestawu Azure SDK](https://azure.microsoft.com/downloads/).

### <a name="create-the-topic-and-subscriptions"></a>Tworzenie tematu i subskrypcji
Operacje zarządzania jednostek obsługi komunikatów (kolejki i publikowania/subskrypcji tematy) są wykonywane za pośrednictwem usługi Service Bus [NamespaceManager](/dotnet/api/microsoft.servicebus.namespacemanager#microsoft_servicebus_namespacemanager) klasy. Odpowiednie poświadczenia są wymagane w celu utworzenia **NamespaceManager** wystąpienia określonego obszaru nazw. Usługa Service Bus używa [dostępu sygnatury dostępu Współdzielonego](service-bus-sas.md) na podstawie modelu zabezpieczeń. [TokenProvider](/dotnet/api/microsoft.servicebus.tokenprovider#microsoft_servicebus_tokenprovider) klasa reprezentuje dostawcę tokenu zabezpieczającego z wbudowanymi metodami factory zwracanie niektórych dobrze znanych dostawców tokenu. Użyjemy [CreateSharedAccessSignatureTokenProvider](/dotnet/api/microsoft.servicebus.tokenprovider#Microsoft_ServiceBus_TokenProvider_CreateSharedAccessSignatureTokenProvider_System_String_) metody do przechowywania poświadczeń sygnatury dostępu Współdzielonego. [NamespaceManager](/dotnet/api/microsoft.servicebus.namespacemanager#microsoft_servicebus_namespacemanager) wystąpienia następnie jest tworzony z adresu podstawowego przestrzeni nazw usługi Service Bus oraz dostawcy tokenu.

[NamespaceManager](/dotnet/api/microsoft.servicebus.namespacemanager#microsoft_servicebus_namespacemanager) klasa dostarcza metody do tworzenia, wyliczania i usuwania jednostek obsługi komunikatów. Kod, który jest wyświetlany w tym miejscu przedstawiono sposób **NamespaceManager** wystąpienia są tworzone i używane do tworzenia **DataCollectionTopic** tematu.

```csharp
Uri uri = ServiceBusEnvironment.CreateServiceUri("sb", "test-blog", string.Empty);
string name = "RootManageSharedAccessKey";
string key = "abcdefghijklmopqrstuvwxyz";

TokenProvider tokenProvider = TokenProvider.CreateSharedAccessSignatureTokenProvider(name, key);
NamespaceManager namespaceManager = new NamespaceManager(uri, tokenProvider);

namespaceManager.CreateTopic("DataCollectionTopic");
```

Należy pamiętać, że istnieją overloads z [CreateTopic](/dotnet/api/microsoft.servicebus.namespacemanager#Microsoft_ServiceBus_NamespaceManager_CreateTopic_System_String_) metody umożliwiające ustawienie właściwości tematu. Na przykład można ustawić czas wygaśnięcia (TTL) wartością domyślną dla komunikatów wysyłanych do tematu. Następnie dodaj **spisu** i **pulpitu nawigacyjnego** subskrypcji.

```csharp
namespaceManager.CreateSubscription("DataCollectionTopic", "Inventory");
namespaceManager.CreateSubscription("DataCollectionTopic", "Dashboard");
```

### <a name="send-messages-to-the-topic"></a>Wysyłanie komunikatów do tematu
Dla czasu wykonywania operacji na jednostek usługi Service Bus; na przykład wysyłanie i odbieranie wiadomości, aplikacja musi najpierw utworzyć [MessagingFactory](/dotnet/api/microsoft.servicebus.messaging.messagingfactory#microsoft_servicebus_messaging_messagingfactory) obiektu. Podobnie jak [NamespaceManager](/dotnet/api/microsoft.servicebus.namespacemanager#microsoft_servicebus_namespacemanager) klasy **MessagingFactory** wystąpienia jest tworzona na podstawie adresu podstawowego przestrzeni nazw usługi i dostawcy tokenu.

```
MessagingFactory factory = MessagingFactory.Create(uri, tokenProvider);
```

Komunikaty wysyłane do i odebrane od tematów usługi Service Bus są wystąpieniami klasy [BrokeredMessage](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage) klasy. Ta klasa zawiera zestaw właściwości standardowych (takich jak [etykiety](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage.label?view=azureservicebus-4.0.0#Microsoft_ServiceBus_Messaging_BrokeredMessage_Label) i [TimeToLive](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage.timetolive?view=azureservicebus-4.0.0#Microsoft_ServiceBus_Messaging_BrokeredMessage_TimeToLive)), słownik, który jest używany do przechowywania aplikacji właściwości oraz treść dowolnych danych aplikacji. Aplikacja możne ustawić treść przez przekazanie dowolnego obiektu podlegającego serializacji (poniższy przykład przekazuje w **SalesData** obiekt, który reprezentuje dane o sprzedaży z POS terminal), co oznacza użycie [DataContractSerializer](https://msdn.microsoft.com/library/system.runtime.serialization.datacontractserializer.aspx) do serializacji obiektu. Alternatywnie [strumienia](https://msdn.microsoft.com/library/system.io.stream.aspx) można podać obiektu.

```csharp
BrokeredMessage bm = new BrokeredMessage(salesData);
bm.Label = "SalesReport";
bm.Properties["StoreName"] = "Redmond";
bm.Properties["MachineID"] = "POS_1";
```

Najprostszym sposobem wysyłania komunikatów do tematu jest użycie [CreateMessageSender](/dotnet/api/microsoft.servicebus.messaging.messagingfactory#Microsoft_ServiceBus_Messaging_MessagingFactory_CreateMessageSender_System_String_) utworzyć [MessageSender](/dotnet/api/microsoft.servicebus.messaging.messagesender) obiekt bezpośrednio z [MessagingFactory](/dotnet/api/microsoft.servicebus.messaging.messagingfactory) wystąpienie:

```csharp
MessageSender sender = factory.CreateMessageSender("DataCollectionTopic");
sender.Send(bm);
```

### <a name="receive-messages-from-a-subscription"></a>Odbieranie komunikatów z subskrypcji
Podobnie jak przy użyciu kolejki, do odbierania wiadomości z subskrypcji, można użyć [MessageReceiver](/dotnet/api/microsoft.servicebus.messaging.messagereceiver) obiektów, które można tworzyć bezpośrednio z [MessagingFactory](/dotnet/api/microsoft.servicebus.messaging.messagingfactory) przy użyciu [CreateMessageReceiver](/dotnet/api/microsoft.servicebus.messaging.messagingfactory#Microsoft_ServiceBus_Messaging_MessagingFactory_CreateMessageReceiver_System_String_). Można użyć jednej z dwóch różnych trybów odbierać (**ReceiveAndDelete** i **PeekLock**), zgodnie z opisem w [tworzenie aplikacji korzystających z kolejek usługi Service Bus](service-bus-create-queues.md).

Należy pamiętać, że podczas tworzenia **MessageReceiver** subskrypcji, *entityPath* parametr ma postać `topicPath/subscriptions/subscriptionName`. W związku z tym aby utworzyć **MessageReceiver** dla **spisu** subskrypcji **DataCollectionTopic** tematu, *entityPath* musi mieć ustawioną `DataCollectionTopic/subscriptions/Inventory`. Kod wygląda następująco:

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
Do tej pory w tym scenariuszu wszystkich wiadomości wysłanych do tematu są udostępniane dla wszystkich zarejestrowanych subskrypcji. Tutaj klucza frazy "udostępniono." Natomiast subskrypcje usługi Service Bus, zobacz wszystkich wiadomości wysłanych do tematu, możesz skopiować tylko podzbiór tych wiadomości do kolejki subskrypcji wirtualnego. To jest wykonywane przy użyciu subskrypcji *filtry*. Podczas tworzenia subskrypcji, możesz podać wyrażenie filtru w formularzu predykatu styl SQL92 działającą za pośrednictwem właściwości wiadomości, właściwości systemu (na przykład [etykiety](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_Label)) i właściwości aplikacji, takich jak **StoreName** w poprzednim przykładzie.

Rozwijają scenariusza ilustrację, drugi magazynu jest mają zostać dodane do naszych scenariusz sprzedaży detalicznej. Jeszcze przesłana do systemu zarządzania spisem scentralizowane sprzedaży danych ze wszystkich terminali w punkcie sprzedaży z obu sklepów, ale Menedżera magazynu przy użyciu narzędzia Pulpit nawigacyjny jest tylko zainteresowane w wykonywaniu tego magazynu. Możesz użyć filtrowania można to osiągnąć subskrypcji. Należy pamiętać, że Terminale POS publikowania wiadomości, ustawione **StoreName** właściwości aplikacji w komunikacie. Podane dwóch magazynów, na przykład **Redmond** i **Seattle**, Terminale POS w magazynie Redmond oznaczania ich wiadomości danych sprzedaży z **StoreName** równa **Redmond**, podczas gdy Seattle przechowywania Użyj Terminale POS **StoreName** równa **Seattle**. Menedżer magazynu magazynu Redmond tylko chce wyświetlać dane z terminali w punkcie sprzedaży. System wygląda następująco:

![Usługa Bus4](./media/service-bus-create-topics-subscriptions/IC657167.gif)

Aby skonfigurować ten routingu, należy utworzyć **pulpitu nawigacyjnego** subskrypcji w następujący sposób:

```csharp
SqlFilter dashboardFilter = new SqlFilter("StoreName = 'Redmond'");
namespaceManager.CreateSubscription("DataCollectionTopic", "Dashboard", dashboardFilter);
```

Z tym [filtr subskrypcji](/dotnet/api/microsoft.servicebus.messaging.sqlfilter), tylko komunikaty, które mają **StoreName** ustawioną właściwość **Redmond** zostaną skopiowane do wirtualnej kolejki w celu **pulpitu nawigacyjnego** subskrypcji. Istnieje wiele więcej filtrowanie subskrypcji, jednak. Aplikacje mogą mieć wiele reguł filtrowania dla subskrypcji Oprócz uprawnienia do modyfikowania właściwości komunikatu zgodnie z przekazaniem do wirtualnej kolejki subskrypcji.

## <a name="summary"></a>Podsumowanie
Wszystkie powody do korzystania z usługi kolejkowania wiadomości opisanego w [tworzenie aplikacji korzystających z kolejek usługi Service Bus](service-bus-create-queues.md) mają zastosowanie również do tematów, w szczególności:

* Oddzielenia czasowego — komunikatów, producenci i konsumenci nie trzeba być w trybie online w tym samym czasie.
* Wyrównywanie obciążenia — szczytów obciążenia są wygładzania w temacie Włączanie aplikacji odbiorczych może udostępnić średni obciążenia zamiast obciążenia szczytowego.
* Równoważenie obciążenia — podobnie jak kolejka, może mieć na wielu konkurujących konsumentów nasłuchiwania na jedną subskrypcją, w każdej wiadomości przekazane do tylko jednej konsumentów, a tym samym równoważenia obciążenia.
* Luźne powiązanie — komunikacji sieciowej można rozwijać, bez wywierania wpływu na istniejące punkty końcowe; na przykład dodawania subskrypcji lub zmiana filtrów do tematu, aby umożliwić nowych klientów.

## <a name="next-steps"></a>Następne kroki

Zobacz [tworzenie aplikacji korzystających z kolejek usługi Service Bus](service-bus-create-queues.md) informacji o tym, jak używać kolejek w scenariuszu retail POS.

