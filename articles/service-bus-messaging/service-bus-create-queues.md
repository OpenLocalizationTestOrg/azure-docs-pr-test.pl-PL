---
title: "aaaWrite aplikacji, które używają kolejek usługi Azure Service Bus | Dokumentacja firmy Microsoft"
description: "Jak toowrite prostą aplikację na podstawie kolejki, która używa usługi Azure Service Bus."
services: service-bus-messaging
documentationcenter: na
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 754d91b3-1426-405e-84b4-fd36d65b114a
ms.service: service-bus-messaging
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/07/2017
ms.author: sethm
ms.openlocfilehash: 93b75902a06becd6e33e05298e09f5669d0e2aef
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-applications-that-use-service-bus-queues"></a>Tworzenie aplikacji korzystających z kolejek usługi Service Bus
W tym temacie opisano kolejek usługi Service Bus oraz przedstawiono sposób toowrite prostą aplikację na podstawie kolejki, która używa usługi Service Bus.

Rozważmy scenariusz z Witaj świecie sprzedaży detalicznej, w którym dane o sprzedaży z poszczególnych Point-of-Sale (POS) musi być terminale kierowane tooan systemu zarządzania spisem, używany hello toodetermine danych w magazynie ma toobe uzupełniane. To rozwiązanie wymaga komunikatów usługi Service Bus hello komunikacji między terminale hello i hello systemu zarządzania spisem, jak pokazano na następującej ilustracji hello:

![Obraz kolejek usługi Service Bus 1](./media/service-bus-create-queues/IC657161.gif)

Każdy terminal POS raporty jego danych sprzedaży przez wysłanie wiadomości toohello **DataCollectionQueue**. Komunikaty te pozostają w tej kolejki do momentu pobrania przez system zarządzania hello spisu. Ten wzorzec jest często nazywany *asynchroniczną obsługę wiadomości*, ponieważ hello POS terminali nie ma toowait na odpowiedź od przetwarzania toocontinue hello spisu zarządzania systemu.

## <a name="why-queuing"></a>Dlaczego kolejkowania?
Zanim przyjrzymy hello kodu, który jest wymagany tooset się tej aplikacji, należy rozważyć zalety hello przy użyciu kolejki w tym scenariuszu zamiast terminale hello POS komunikować się bezpośrednio (synchronicznie) toohello spisu systemu zarządzania.

### <a name="temporal-decoupling"></a>Oddzielenia czasowego
Z hello asynchroniczny wzorzec przesyłania komunikatów, producenci i konsumenci nie mają toobe w trybie online na powitania tym samym czasie. infrastruktury obsługi wiadomości powitania niezawodny sposób przechowuje komunikaty do momentu hello odbierająca jest gotowa tooreceive je. Oznacza to, że hello składniki aplikacji rozproszonej hello mogą być rozłączone zarówno dobrowolnie; na przykład w celu przeprowadzenia konserwacji lub powodu tooa awarii składników, bez wywierania wpływu na powitania całego systemu. Ponadto korzystanie z aplikacji hello może mieć tylko toobe online pewnych porach dnia hello. Na przykład w tym scenariuszu handlowej systemu zarządzania spisem hello może mieć tylko toocome online po zakończeniu hello hello dnia roboczego.

### <a name="load-leveling"></a>Wyrównywanie obciążenia
W wielu aplikacjach obciążenie systemu różni się wraz z upływem czasu, podczas gdy czas przetwarzania hello wymagany dla każdej jednostki pracy jest zwykle stały. Pośredniczenie komunikatów, producenci i konsumenci środki kolejki, które hello aplikacja odbierająca komunikaty (proces roboczy hello) zawiera jedynie toobe zainicjowana tooservice średnią załadować zamiast obciążenia szczytowego. wzrośnie Hello głębokość kolejki hello i kontraktu jako hello przychodzące obciążenia zmienia się. To jest zapisywany bezpośrednio pieniędzy z uwzględnieniem toohello ilością obciążenia aplikacji hello wymagane tooservice infrastruktury.

![Kolejki usługi Service Bus obraz 2](./media/service-bus-create-queues/IC657162.gif)

### <a name="load-balancing"></a>Równoważenie obciążenia
Witaj wzrostu obciążenia, więcej procesów roboczych może być dodany tooread z hello kolejki procesu roboczego. Każdy komunikat jest przetwarzany przez tylko jeden z procesów roboczych hello. Ponadto tego równoważenie obciążenia oparte na ściąganiu umożliwia optymalne użycie komputerów roboczych hello nawet wtedy, gdy komputery procesu roboczego hello różnią się z uwzględnieniem tooprocessing zasilania, ponieważ każda będzie ściągać komunikaty własnych maksymalną szybkością. Ten wzorzec jest często nazywany hello konkurujących konsumentów wzorca.

![Obraz kolejek usługi Service Bus 3](./media/service-bus-create-queues/IC657163.gif)

### <a name="loose-coupling"></a>Luźne powiązanie
Przy użyciu toointermediate kolejkowania wiadomości między producentami a konsumentami komunikatów zawiera wewnętrzne luźne powiązanie między składnikami hello. Ponieważ producenci i konsumenci nie są wzajemnie świadomi, można uaktualnić konsumenta bez wpływu na powitania producenta. Ponadto można rozwijać hello wiadomości topologii, bez wpływu na istniejące punkty końcowe hello. Omówiono to bardziej przy omawianiu publikowania/subskrypcji.

## <a name="show-me-hello-code"></a>Pokaż hello kodu
Witaj w następującej sekcji przedstawiono sposób toobuild usługi Service Bus toouse tej aplikacji.

### <a name="sign-up-for-an-azure-account"></a>Załóż konto platformy Azure
Konieczne będzie konto platformy Azure w kolejności toostart pracy z usługą Service Bus. Jeśli nie masz już jeden, można utworzysz bezpłatne konto [tutaj](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A85619ABF).

### <a name="create-a-namespace"></a>Tworzenie przestrzeni nazw
Po utworzeniu subskrypcji można [tworzenie przestrzeni nazw usługi](service-bus-create-namespace-portal.md). Każdy obszar nazw działa jako kontener zakresu dla zestawu jednostek usługi Service Bus. Nadaj unikatową nazwę nowego obszaru nazw, wszystkich kont usługi Service Bus. 

### <a name="install-hello-nuget-package"></a>Zainstaluj pakiet NuGet hello
toouse hello nazw usługi Service Bus, aplikacja musi odwoływać się hello zestawu usługi Service Bus, w szczególności Microsoft.ServiceBus.dll. Możesz znaleźć tego zestawu jako część hello Microsoft Azure SDK i pobierania hello jest dostępna na powitania [strona pobierania zestawu Azure SDK](https://azure.microsoft.com/downloads/). Jednak hello [pakietu NuGet usługi Service Bus](https://www.nuget.org/packages/WindowsAzure.ServiceBus) jest hello Najprostszym sposobem tooget hello interfejsu API usługi Service Bus i tooconfigure aplikacji ze wszystkimi zależnościami usługi Service Bus hello.

### <a name="create-hello-queue"></a>Utwórz kolejkę hello
Operacje zarządzania dla usługi Service Bus jednostek obsługi komunikatów (kolejki i publikowania/subskrypcji tematy) są wykonywane za pośrednictwem hello [NamespaceManager](/dotnet/api/microsoft.servicebus.namespacemanager) klasy. Usługa Service Bus używa [dostępu sygnatury dostępu Współdzielonego](service-bus-sas.md) na podstawie modelu zabezpieczeń. Witaj [TokenProvider](/dotnet/api/microsoft.servicebus.tokenprovider) klasa reprezentuje dostawcę tokenu zabezpieczającego z wbudowanymi metodami factory zwracanie niektórych dobrze znanych dostawców tokenu. Użyjemy [CreateSharedAccessSignatureTokenProvider](/dotnet/api/microsoft.servicebus.tokenprovider#Microsoft_ServiceBus_TokenProvider_CreateSharedAccessSignatureTokenProvider_System_String_) poświadczeń sygnatury dostępu Współdzielonego hello toohold metody. Witaj [NamespaceManager](/dotnet/api/microsoft.servicebus.namespacemanager) wystąpienia następnie jest tworzony z hello adresu podstawowego przestrzeni nazw usługi Service Bus hello oraz hello dostawcy tokenu.

Witaj [NamespaceManager](/dotnet/api/microsoft.servicebus.namespacemanager) klasa dostarcza metody toocreate, wyliczania i usuwania jednostek obsługi komunikatów. Witaj kod, który jest wyświetlany w tym miejscu przedstawiono sposób hello [NamespaceManager](/dotnet/api/microsoft.servicebus.namespacemanager) wystąpienie jest utworzony i używany toocreate hello **DataCollectionQueue** kolejki.

```csharp
Uri uri = ServiceBusEnvironment.CreateServiceUri("sb", 
                "test-blog", string.Empty);
string name = "RootManageSharedAccessKey";
string key = "abcdefghijklmopqrstuvwxyz";

TokenProvider tokenProvider = 
    TokenProvider.CreateSharedAccessSignatureTokenProvider(name, key);
NamespaceManager namespaceManager = 
    new NamespaceManager(uri, tokenProvider);
namespaceManager.CreateQueue("DataCollectionQueue");
```

Należy pamiętać, że istnieją przeciążenia metody hello [CreateQueue](/dotnet/api/microsoft.servicebus.namespacemanager#Microsoft_ServiceBus_NamespaceManager_CreateQueue_System_String_) metodę, która włączyć właściwości toobe kolejki hello dostosowana. Na przykład można ustawić hello time to live (TTL) wartość domyślna dla wiadomości wysyłanych toohello kolejki.

### <a name="send-messages-toohello-queue"></a>Komunikaty toohello kolejki wysyłania
Dla czasu wykonywania operacji na jednostek usługi Service Bus; na przykład wysyłanie i odbieranie wiadomości, aplikacja musi najpierw utworzyć [MessagingFactory](/dotnet/api/microsoft.servicebus.messaging.messagingfactory) obiektu. Podobne toohello [NamespaceManager](/dotnet/api/microsoft.servicebus.namespacemanager) klasy, hello [MessagingFactory](/dotnet/api/microsoft.servicebus.messaging.messagingfactory) z adresu podstawowego hello hello przestrzeni nazw usługi i dostawcy tokenów hello jest tworzone wystąpienie.

```csharp
 BrokeredMessage bm = new BrokeredMessage(salesData);
 bm.Label = "SalesReport";
 bm.Properties["StoreName"] = "Redmond";
 bm.Properties["MachineID"] = "POS_1";
```

Komunikaty wysyłane do i odbierane z usługi Service Bus są kolejki wystąpień hello [BrokeredMessage](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage) klasy. Ta klasa zawiera zestaw właściwości standardowych (takich jak [etykiety](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_Label) i [TimeToLive](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_TimeToLive)), słownik, który jest używany toohold właściwości aplikacji oraz treść dowolnych danych aplikacji. Aplikacja możne ustawić treść hello przez przekazanie dowolnego obiektu podlegającego serializacji (hello w poniższym przykładzie przekazuje w **SalesData** obiekt, który reprezentuje hello danych sprzedaży z terminalu hello POS), który będzie używany hello [ DataContractSerializer](https://msdn.microsoft.com/library/system.runtime.serialization.datacontractserializer.aspx) tooserialize hello obiektu. Alternatywnie [strumienia](https://msdn.microsoft.com/library/system.io.stream.aspx) można podać obiektu.

Witaj najprostszym tooa sposób toosend wiadomości, podane kolejki w naszym wielkość hello **DataCollectionQueue**, jest toouse [CreateMessageSender](/dotnet/api/microsoft.servicebus.messaging.messagingfactory#Microsoft_ServiceBus_Messaging_MessagingFactory_CreateMessageSender_System_String_) toocreate [MessageSender](/dotnet/api/microsoft.servicebus.messaging.messagesender) obiektu bezpośrednio z hello [MessagingFactory](/dotnet/api/microsoft.servicebus.messaging.messagingfactory) wystąpienia.

```csharp
MessageSender sender = factory.CreateMessageSender("DataCollectionQueue");
sender.Send(bm);
```

### <a name="receiving-messages-from-hello-queue"></a>Odbieranie komunikatów z kolejki hello
tooreceive wiadomości z kolejki hello, można użyć [MessageReceiver](/dotnet/api/microsoft.servicebus.messaging.messagereceiver) obiektów, które można tworzyć bezpośrednio z hello [MessagingFactory](/dotnet/api/microsoft.servicebus.messaging.messagingfactory) przy użyciu [CreateMessageReceiver](/dotnet/api/microsoft.servicebus.messaging.messagingfactory#Microsoft_ServiceBus_Messaging_MessagingFactory_CreateMessageReceiver_System_String_). Odbiorcy wiadomości mogą pracować w dwóch różnych trybach: **ReceiveAndDelete** i **PeekLock**. Witaj [ReceiveMode](/dotnet/api/microsoft.servicebus.messaging.receivemode) jest ustawiana po utworzeniu odbiornika wiadomość hello jako toohello parametru [CreateMessageReceiver](/dotnet/api/microsoft.servicebus.messaging.messagingfactory?redirectedfrom=MSDN#Microsoft_ServiceBus_Messaging_MessagingFactory_CreateMessageReceiver_System_String_Microsoft_ServiceBus_Messaging_ReceiveMode_) wywołania.

Korzystając z hello **ReceiveAndDelete** trybie hello odbieranie jest operacją pojedynczego zrzutu; oznacza to, kiedy usługa Service Bus odbiera żądanie hello, oznacza hello komunikat jako wykorzystany i zwraca go toohello aplikacji. **ReceiveAndDelete** tryb jest hello najprostszym modelem i działa najlepiej w scenariuszach, w których hello aplikacji może tolerować nieprzetworzenie komunikatu toooccur gdyby awarii. toounderstand, Rozważmy scenariusz w problemy, które konsumenta hello hello mógł odebrać żądanie, a następnie ulega awarii przed jego przetworzeniem. Ponieważ Usługa Service Bus oznaczony hello komunikat jako wykorzystany, podczas ponownego uruchamiania aplikacji hello i uruchamia ponownie, korzystanie z komunikatów pominie utracony wiadomość hello, który został wykorzystany przed hello awarii.

W **PeekLock** trybie hello odbieranie staje się operacją dwuetapową, dzięki czemu możliwe toosupport aplikacji, które nie tolerują brakujących komunikatów. Usługa Service Bus odbiera żądanie hello, znajduje się dalej toobe wiadomość hello używane, blokuje go tooprevent innym klientom odebrania go i zwraca go po toohello aplikacji. Kiedy aplikacja hello zakończy przetwarzanie wiadomości powitania (lub niezawodnie zapisze go w celu przyszłego przetwarzania), wykonuje drugi etap hello hello odbierania przez wywołanie metody procesu [Complete](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_Complete) na wiadomość powitania odebrane. Kiedy Usługa Service Bus widzi hello [Complete](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_Complete) wywołania oznacza hello komunikat jako wykorzystany.

Możliwe są dwa inne wyniki. Po pierwsze, jeśli aplikacja hello nie tooprocess hello komunikat dla jakiegoś powodu, może wywołać [Abandon](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_Abandon) na wiadomość powitania odebranych (zamiast [Complete](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_Complete)). To spowoduje, że wiadomość hello toounlock usługi Service Bus i stał się dostępny toobe odbioru, hello przez tego samego użytkownika lub innego Kończenie konsumenta. Po drugie istnieje limit czasu skojarzony z blokadą hello i jeśli aplikacja hello nie można przetworzyć wiadomości powitania przed hello upływem limitu czasu blokady (na przykład jeśli wystąpiła awaria aplikacji hello), a następnie odblokowaniem usługi Service Bus wiadomość hello i stał się dostępny toobe Odebrano ponownie (zasadniczo wykonywania [Abandon](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_Abandon) operacji domyślnie).

Należy pamiętać, że jeśli hello aplikacja przestaje działać po przetwarza wiadomości powitania, ale przed jego hello [Complete](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_Complete) żądanie zostało wydane, wiadomość hello jest przed przeniesieniem toohello aplikacji po jej ponownym uruchomieniu. To jest często nazywany * co najmniej raz * przetwarzania. Oznacza to, że każdy komunikat będzie przetwarzany co najmniej raz, ale w niektórych sytuacjach hello sam komunikat może być dostarczony ponownie. Jeśli hello scenariusz nie Toleruje dwukrotnego przetwarzania, w duplikaty toodetect aplikacji hello jest wymagane dodatkowe logiki. Można to osiągnąć oparte na powitania [MessageId](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_MessageId) właściwości wiadomości powitania. wartość tej właściwości Hello pozostaje stała między kolejnymi próbami dostarczenia. Jest to określane jako *dokładnie raz* przetwarzania.

Witaj kod, który jest wyświetlany w tym miejscu odbiera i przetwarza wiadomości przy użyciu hello **PeekLock** tryb, który jest domyślnym hello, jeśli nie [ReceiveMode](/dotnet/api/microsoft.servicebus.messaging.receivemode) wartość nie zostanie podany wprost.

```csharp
MessageReceiver receiver = factory.CreateMessageReceiver("DataCollectionQueue");
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

### <a name="use-hello-queue-client"></a>Użyj powitania klienta kolejki
Witaj przykłady we wcześniejszej części tej sekcji utworzony [MessageSender](/dotnet/api/microsoft.servicebus.messaging.messagesender) i [MessageReceiver](/dotnet/api/microsoft.servicebus.messaging.messagereceiver) obiektów bezpośrednio z hello [MessagingFactory](/dotnet/api/microsoft.servicebus.messaging.messagingfactory) toosend i odbierania wiadomości z kolejki hello odpowiednio. Informacje o innym podejściu jest toouse [QueueClient](/dotnet/api/microsoft.servicebus.messaging.queueclient) obiektu, który obsługuje zarówno operacji wysyłania i odbierania w toomore dodanie zaawansowane funkcje, takie jak sesji.

```csharp
QueueClient queueClient = factory.CreateQueueClient("DataCollectionQueue");
queueClient.Send(bm);

BrokeredMessage message = queueClient.Receive();

try
{
    ProcessMessage(message);
    message.Complete();
}
catch (Exception e)
{
    message.Abandon();
} 
```

## <a name="next-steps"></a>Następne kroki
Teraz, kiedy znasz już podstawy hello kolejek, zobacz [tworzenie aplikacji korzystających z usługi Service Bus tematy i subskrypcje](service-bus-create-topics-subscriptions.md) toocontinue rozważania przy użyciu możliwości publikowania/subskrybowania hello tematów usługi Service Bus i Subskrypcje.

