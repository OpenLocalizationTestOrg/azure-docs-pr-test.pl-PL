---
title: "aaaOverview wiadomości z kolejki, tematy i subskrypcje usługi Azure Service Bus | Dokumentacja firmy Microsoft"
description: "Przegląd jednostki do obsługi komunikatów usługi Service Bus."
services: service-bus-messaging
documentationcenter: na
author: sethmanheim
manager: timlt
editor: 
ms.assetid: a306ced4-74e9-47c6-990a-d9c47efa31d5
ms.service: service-bus-messaging
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/28/2017
ms.author: sethm
ms.openlocfilehash: 73135d2658e341c14dbb114ab938faed91578ff1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="service-bus-queues-topics-and-subscriptions"></a>Kolejki, tematy i subskrypcje usługi Service Bus

Microsoft Azure Service Bus obsługuje zestaw technologii chmurowych, zorientowany oprogramowanie pośredniczące, takich jak usługi kolejkowania komunikatów niezawodnej i trwałe publikowania/subskrybowania komunikatów. Te możliwości obsługi komunikatów "obsługiwanych przez brokera" można traktować jako rozdzielonymi wiadomości funkcje, które publikacji / subskrypcji, zawierająca dane czasowe oddzielenie i równoważenia obciążenia scenariuszy przy użyciu hello magistrali usług obsługi wiadomości w sieci szkieletowej. Komunikacja oddzielona ma wiele zalet, na przykład klienci i serwery mogą nawiązywać połączenie zgodnie z potrzebami i wykonywać ich operacje w sposób asynchroniczny.

jednostek obsługi komunikatów Hello tworzących hello najważniejsza część hello wiadomości możliwości w usłudze Service Bus są kolejki, tematy i subskrypcje i reguły/akcji.

## <a name="queues"></a>Kolejki

Kolejki oferują *pierwszy na wejściu — pierwszy limit* tooone dostarczania wiadomości (FIFO) lub więcej konkurujących konsumentów. Oznacza to komunikaty są zwykle oczekiwanego toobe odbierane i przetwarzane przez odbiorców hello w kolejności hello, w którym zostały one dodane toohello kolejki, a każdy komunikat jest odbierany i przetwarzany przez tylko jednego odbiorcę komunikatów. Najważniejszą korzyścią z używania kolejek jest tooachieve "oddzielenia czasowego" składników aplikacji. Witaj innymi słowy, producenci (nadawcy) i konsumenci (odbiorcy) nie mają toobe wysyłanie i odbieranie wiadomości na powitania takie same czasu, ponieważ komunikaty są trwale przechowywane w kolejce hello. Ponadto producent hello nie ma toowait na odpowiedź od konsumenta hello w kolejności toocontinue tooprocess i wysyłać wiadomości.

Pokrewną korzyścią jest "obciążenia bilansowanie,", która umożliwia toosend producenci i konsumenci i odbierania wiadomości w różnym tempie. W wielu aplikacjach obciążenie systemu hello różni się wraz z upływem czasu; jednak czas przetwarzania hello wymagany dla każdej jednostki pracy jest zwykle stały. Pośredniczenie producentami a konsumentami komunikatów z kolejki oznacza, że tego hello korzystanie z aplikacji tylko ma średni obciążenia toohandle stanie elastycznie toobe toobe zamiast obciążenia szczytowego. głębokość kolejki hello Hello rośnie i zmniejsza się w zależności od zmian obciążenia przychodzącego hello. To jest zapisywany bezpośrednio pieniędzy z uwzględnieniem toohello ilością obciążenia aplikacji hello wymagane tooservice infrastruktury. Witaj wzrostu obciążenia, więcej procesów roboczych może być dodany tooread z hello kolejki. Każdy komunikat jest przetwarzany przez tylko jeden z procesów roboczych hello. Ponadto to Równoważenie obciążenia oparte na ściąganiu umożliwia optymalne wykorzystanie komputerów roboczych hello nawet wtedy, gdy komputery procesu roboczego hello różnią się z uwzględnieniem tooprocessing zasilania, ponieważ każda będzie ściągać komunikaty własnych maksymalną szybkością. Ten wzorzec jest często nazywany wzorcem "konkurujących konsumentów" hello.

Użycie kolejek toointermediate między producentami a konsumentami komunikatów zapewnia związanego z używaniem luźne powiązanie między składnikami hello. Ponieważ producenci i konsumenci nie są wzajemnie świadomi, można uaktualnić konsumenta bez wpływu na powitania producenta.

Tworzenie kolejki jest procesem wieloetapowych. Możesz wykonywać operacje zarządzania dla usługi Service Bus messaging entities (kolejki i tematy) za pośrednictwem hello [Microsoft.ServiceBus.NamespaceManager](/dotnet/api/microsoft.servicebus.namespacemanager#microsoft_servicebus_namespacemanager) klasy, która jest tworzony, podając adres bazowy hello hello usługi Service Bus przestrzeń nazw i hello poświadczeń użytkownika. [NamespaceManager](/dotnet/api/microsoft.servicebus.namespacemanager#microsoft_servicebus_namespacemanager) zapewnia toocreate metody wyliczania i usuwania jednostek obsługi komunikatów. Po utworzeniu [Microsoft.ServiceBus.TokenProvider](/dotnet/api/microsoft.servicebus.tokenprovider#microsoft_servicebus_tokenprovider) obiektu obiektu z hello SAS nazwy i klucza i zarządzanie przestrzeni nazw usługi, można użyć hello [Microsoft.ServiceBus.NamespaceManager.CreateQueue](/dotnet/api/microsoft.servicebus.namespacemanager#Microsoft_ServiceBus_NamespaceManager_CreateQueue_System_String_) metody toocreate hello kolejki. Na przykład:

```csharp
// Create management credentials
TokenProvider credentials = TokenProvider.CreateSharedAccessSignatureTokenProvider(sasKeyName,sasKeyValue);
// Create namespace client
NamespaceManager namespaceClient = new NamespaceManager(ServiceBusEnvironment.CreateServiceUri("sb", ServiceNamespace, string.Empty), credentials);
```

Następnie można utworzyć obiektu typu kolejka i fabryki obsługi komunikatów z hello identyfikatora URI magistrali usługi jako argument. Na przykład:

```csharp
QueueDescription myQueue;
myQueue = namespaceClient.CreateQueue("TestQueue");
MessagingFactory factory = MessagingFactory.Create(ServiceBusEnvironment.CreateServiceUri("sb", ServiceNamespace, string.Empty), credentials); 
QueueClient myQueueClient = factory.CreateQueueClient("TestQueue");
```

Następnie można wysłać wiadomości toohello kolejki. Na przykład, jeśli masz listę obsługiwanych przez brokera komunikatów o nazwie `MessageList`, kod hello pojawia się poniżej toohello podobne:

```csharp
for (int count = 0; count < 6; count++)
{
    var issue = MessageList[count];
    issue.Label = issue.Properties["IssueTitle"].ToString();
    myQueueClient.Send(issue);
}
```

Następnie komunikaty z kolejki hello w następujący sposób:

```csharp
while ((message = myQueueClient.Receive(new TimeSpan(hours: 0, minutes: 0, seconds: 5))) != null)
    {
        Console.WriteLine(string.Format("Message received: {0}, {1}, {2}", message.SequenceNumber, message.Label, message.MessageId));
        message.Complete();

        Console.WriteLine("Processing message (sleeping...)");
        Thread.Sleep(1000);
    }
```

W hello [ReceiveAndDelete](/dotnet/api/microsoft.servicebus.messaging.receivemode) odbierania hello trybie operacji pojedynczego zrzutu; oznacza to, kiedy usługa Service Bus odbiera żądanie hello, oznacza hello komunikat jako wykorzystany i zwraca go toohello aplikacji. **ReceiveAndDelete** tryb hello najprostszym modelem i działa najlepiej w scenariuszach, w których hello aplikacja może tolerować nieprzetworzenie komunikatu w razie awarii hello. toounderstand, Rozważmy scenariusz w problemy, które konsumenta hello hello mógł odebrać żądanie, a następnie ulega awarii przed jego przetworzeniem. Ponieważ Usługa Service Bus oznacza hello komunikat jako wykorzystany, gdy aplikacja hello ponownego uruchomienia i rozpocznie korzystanie z komunikatów ponownie, pominie utracony komunikat hello, który został wykorzystany przed toohello awarii.

W [PeekLock](/dotnet/api/microsoft.servicebus.messaging.receivemode) odbierania hello trybie operacji będzie dwuetapowa, dzięki czemu możliwe toosupport aplikacji, które nie tolerują brakujących komunikatów. Gdy Usługa Service Bus odbiera żądanie hello, znajduje następny toobe wiadomość hello, używane, blokuje go tooprevent innym klientom odbieranie, a następnie zwrócenie go toohello aplikacji. Kiedy aplikacja hello zakończy przetwarzanie wiadomości powitania (lub niezawodnie zapisze go w celu przyszłego przetwarzania), wykonuje drugi etap hello hello odbierania przez wywołanie metody procesu [Complete](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_Complete) na wiadomość powitania odebrane. Kiedy Usługa Service Bus widzi hello **Complete** wywołania oznacza hello komunikat jako wykorzystany.

Jeśli aplikacja hello nie tooprocess hello komunikat dla jakiegoś powodu, może wywołać hello [Abandon](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_Abandon) metody na wiadomość powitania odebranych (zamiast [Complete](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_Complete)). To umożliwia wiadomość hello toounlock usługi Service Bus i stał się dostępny toobe odbioru, hello przez tego samego użytkownika lub innego konkurujących konsumentów. Po drugie jest skojarzony przekroczenie limitu czasu blokady hello i jeśli aplikacja hello nie powiedzie się tooprocess hello komunikat wygaśnięcia hello limit czasu blokady (na przykład jeśli wystąpiła awaria aplikacji hello), Usługa Service Bus umożliwia odblokowanie wiadomość hello i ułatwia toobe dostępne Odebrano ponownie (zasadniczo wykonywania [Abandon](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_Abandon) operacji domyślnie).

Należy pamiętać, że w hello zdarzenie, które aplikacji hello ulegnie awarii po przetworzeniu wiadomość hello, ale przed jego hello **Complete** żądania, wiadomość hello jest przed przeniesieniem toohello aplikacji po jej ponownym uruchomieniu. Jest to często nazywane *co najmniej raz* przetwarzania; oznacza to, że każdy komunikat jest przetwarzany co najmniej raz. Jednak w niektórych sytuacjach hello sam komunikat może być dostarczony ponownie. Jeśli hello scenariusz nie Toleruje dwukrotnego przetwarzania, a następnie dodatkową logikę jest wymagany w hello duplikaty toodetect aplikacji, które można osiągnąć oparte na powitania **MessageId** właściwości wiadomości powitania, który pozostaje stała między kolejnymi próbami dostarczenia. Jest to nazywane *dokładnie raz* przetwarzania.

## <a name="topics-and-subscriptions"></a>Tematy i subskrypcje
W tooqueues kontrast, w którym każdy komunikat jest przetwarzany przez jednego konsumenta, *tematy* i *subskrypcje* Podaj jeden do wielu formę komunikacji w *publikowania/subskrypcji* wzorca. Przydatne w przypadku skalowania toovery dużą liczbę adresatów, każdy opublikowany komunikat stają się dostępne tooeach subskrypcji zarejestrowanej hello tematu. Komunikaty są wysyłane tooa tematu i dostarczonego tooone lub więcej skojarzone subskrypcje, w zależności od reguły filtrowania, które można ustawić na podstawie na subskrypcję. Subskrypcje Hello można użyć dowolnej tooreceive wiadomości powitania od toorestrict dodatkowe filtry. Komunikaty są wysyłane tooa tematu w hello sam sposób są one wysyłane tooa kolejki, ale nie odbiera wiadomości z tematu hello bezpośrednio. Zamiast tego są odbierane z subskrypcji. Subskrypcja tematu przypomina wirtualną kolejkę otrzymującego wiadomości powitania, które są wysyłane toohello tematu. Komunikaty są odbierane z subskrypcji tak samo sposób toohello zostały odebrane z kolejki.

Porównania hello wysyłanie komunikatu funkcji kolejki mapuje bezpośrednio tooa tematu i subskrypcji tooa mapuje jego funkcjonalność odbieranie komunikatu. Między innymi, oznacza to, czy subskrypcje obsługuje hello tego samego wzorce opisany wcześniej w tej sekcji, z uwzględnieniem tooqueues: konkurujących konsumentów, oddzielenia czasowego wyrównywanie obciążenia i równoważenia obciążenia.

Tworzenie tematu jest podobne toocreating kolejki, jak pokazano w przykładzie hello hello w poprzedniej sekcji. Utwórz identyfikator URI usługi hello, a następnie użyj hello [NamespaceManager](/dotnet/api/microsoft.servicebus.namespacemanager) klasy toocreate hello przestrzeni nazw klienta. Następnie możesz utworzyć temat przy użyciu hello [CreateTopic](/dotnet/api/microsoft.servicebus.namespacemanager#Microsoft_ServiceBus_NamespaceManager_CreateTopic_System_String_) metody. Na przykład:

```csharp
TopicDescription dataCollectionTopic = namespaceClient.CreateTopic("DataCollectionTopic");
```

Następnie dodaj subskrypcji, zgodnie z wymaganiami:

```csharp
SubscriptionDescription myAgentSubscription = namespaceClient.CreateSubscription(myTopic.Path, "Inventory");
SubscriptionDescription myAuditSubscription = namespaceClient.CreateSubscription(myTopic.Path, "Dashboard");
```

Następnie można utworzyć klienta tematu. Na przykład:

```csharp
MessagingFactory factory = MessagingFactory.Create(serviceUri, tokenProvider);
TopicClient myTopicClient = factory.CreateTopicClient(myTopic.Path)
```

Przy użyciu nadawcy wiadomości powitania, można wysyłania i odbierania wiadomości tooand z tematu hello opisane w poprzedniej sekcji hello. Na przykład:

```csharp
foreach (BrokeredMessage message in messageList)
{
    myTopicClient.Send(message);
    Console.WriteLine(
    string.Format("Message sent: Id = {0}, Body = {1}", message.MessageId, message.GetBody<string>()));
}
```

Podobne tooqueues, komunikaty są odbierane z subskrypcją za pomocą [SubscriptionClient](/dotnet/api/microsoft.servicebus.messaging.subscriptionclient) obiekt zamiast [QueueClient](/dotnet/api/microsoft.servicebus.messaging.queueclient) obiektu. Tworzenie klienta subskrypcji hello, przekazywanie nazwa hello hello tematu, nazwa hello hello subskrypcji, uprawnia do (opcjonalnie) hello tryb jako parametry. Na przykład z hello **spisu** subskrypcji:

```csharp
// Create hello subscription client
MessagingFactory factory = MessagingFactory.Create(serviceUri, tokenProvider); 

SubscriptionClient agentSubscriptionClient = factory.CreateSubscriptionClient("IssueTrackingTopic", "Inventory", ReceiveMode.PeekLock);
SubscriptionClient auditSubscriptionClient = factory.CreateSubscriptionClient("IssueTrackingTopic", "Dashboard", ReceiveMode.ReceiveAndDelete); 

while ((message = agentSubscriptionClient.Receive(TimeSpan.FromSeconds(5))) != null)
{
    Console.WriteLine("\nReceiving message from Inventory...");
    Console.WriteLine(string.Format("Message received: Id = {0}, Body = {1}", message.MessageId, message.GetBody<string>()));
    message.Complete();
}          

// Create a receiver using ReceiveAndDelete mode
while ((message = auditSubscriptionClient.Receive(TimeSpan.FromSeconds(5))) != null)
{
    Console.WriteLine("\nReceiving message from Dashboard...");
    Console.WriteLine(string.Format("Message received: Id = {0}, Body = {1}", message.MessageId, message.GetBody<string>()));
}
```

### <a name="rules-and-actions"></a>Reguły i akcje
W wielu scenariuszach wiadomości, które mają określone parametry muszą być przetwarzane na różne sposoby. tooenable, można skonfigurować subskrypcje toofind komunikatów, które ma potrzebne właściwości, a następnie wykonaj pewne zmiany właściwości toothose. Natomiast subskrypcje usługi Service Bus, zobacz wszystkich wiadomości wysłanych toohello tematu, można kopiować tylko podzbiór tych kolejki subskrypcji wirtualnego toohello wiadomości. Jest to realizowane przy użyciu filtrów subskrypcji. Takie zmiany są nazywane *akcje filtru*. Po utworzeniu subskrypcji można podać wyrażenie filtru, który działa na powitania właściwości wiadomości powitania, zarówno hello właściwości systemu (na przykład **etykiety**) i właściwości niestandardowych aplikacji (na przykład **StoreName**.) hello SQL wyrażenie filtru jest opcjonalna w takim przypadku; bez wyrażenie filtru SQL żadnych działań filtru zdefiniowane w przypadku subskrypcji zostaną wykonane dla wszystkich wiadomości powitania dla tej subskrypcji.

Przy użyciu hello poprzedni przykład, komunikaty toofilter pochodzące tylko z **Store1**, należy utworzyć subskrypcję pulpitu nawigacyjnego hello w następujący sposób:

```csharp
namespaceManager.CreateSubscription("IssueTrackingTopic", "Dashboard", new SqlFilter("StoreName = 'Store1'"));
```

Ten filtr subskrypcji w miejscu, tylko komunikaty, które mają hello `StoreName` właściwość zbyt`Store1` są toohello skopiowanego wirtualnego kolejki hello `Dashboard` subskrypcji.

Aby uzyskać więcej informacji o wartości filtru możliwe, zobacz dokumentację hello na powitania [SqlFilter](/dotnet/api/microsoft.servicebus.messaging.sqlfilter) i [SqlRuleAction](/dotnet/api/microsoft.servicebus.messaging.sqlruleaction) klasy. Zobacz też hello [obsługiwanych przez brokera obsługi komunikatów: filtry zaawansowane](http://code.msdn.microsoft.com/Brokered-Messaging-6b0d2749) i [filtry tematu](https://github.com/Azure-Samples/azure-servicebus-messaging-samples/tree/master/TopicFilters) próbek.

## <a name="next-steps"></a>Następne kroki
Zobacz poniższe hello zaawansowane tematy, aby uzyskać więcej informacji i przykłady użycia komunikatów usługi Service Bus.

* [Omówienie obsługi komunikatów w usłudze Service Bus](service-bus-messaging-overview.md)
* [samouczek dotyczący komunikatów obsługiwanych przez brokera w usłudze Service Bus dla platformy .NET](service-bus-brokered-tutorial-dotnet.md)
* [Samouczek dotyczący REST komunikatów obsługiwanych przez brokera usługi Service Bus](service-bus-brokered-tutorial-rest.md)
* [Przykładowe filtry tematu](https://github.com/Azure/azure-service-bus/tree/master/samples/DotNet/Microsoft.ServiceBus.Messaging/TopicFilters)
* [Obsługiwanych przez brokera komunikatów: Przykładowe filtry zaawansowane](http://code.msdn.microsoft.com/Brokered-Messaging-6b0d2749)

