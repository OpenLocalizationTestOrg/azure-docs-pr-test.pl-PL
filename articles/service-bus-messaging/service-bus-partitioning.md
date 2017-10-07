---
title: "aaaCreate podzielona na partycje, tematów i kolejek usługi Azure Service Bus | Dokumentacja firmy Microsoft"
description: "W tym artykule opisano, jak tematy dotyczące przy użyciu wielu wiadomości i kolejek usługi Service Bus toopartition przekazuje informacje dotyczące."
services: service-bus-messaging
documentationcenter: na
author: sethmanheim
manager: timlt
editor: 
ms.assetid: a0c7d5a2-4876-42cb-8344-a1fc988746e7
ms.service: service-bus-messaging
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/07/2017
ms.author: sethm;hillaryc
ms.openlocfilehash: 6d42556a0714d6a012dc319f662521c8b0bb958b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="partitioned-queues-and-topics"></a>Partycjonowane kolejki i tematy
Usługa Azure Service Bus jest stosowana w wielu komunikatów brokerzy tooprocess komunikatów i wielu komunikatów przechowuje komunikaty toostore. Konwencjonalne kolejka lub temat są obsługiwane przez brokera pojedynczej wiadomości i przechowywane w jeden Magazyn obsługi komunikatów. Usługa Service Bus *partycje* włączyć kolejek i tematów, lub *jednostki do obsługi komunikatów*, toobe podzielonym na partycje w wielu brokerzy wiadomości i magazyny obsługi komunikatów. Oznacza to, że hello ogólną przepustowość partycjonowane jednostki nie jest już ograniczone przez wydajności hello brokera komunikatów pojedynczego lub magazynie obsługi komunikatów. Ponadto tymczasowego awaria magazynie obsługi komunikatów nie renderować partycjonowanej kolejka lub temat niedostępny. Partycjonowane kolejek i tematów może zawierać wszystkich zaawansowanych funkcji usługi Service Bus, takie jak obsługa transakcji i sesje.

Informacje o wewnętrzne usługi Service Bus, zobacz hello [Architektura usługi Service Bus] [ Service Bus architecture] artykułu.

Partycjonowanie jest włączone domyślnie podczas tworzenia jednostki dla wszystkich kolejek i tematów w wersjach Standard i Premium messaging. Można utworzyć Standard warstwy jednostki do obsługi komunikatów bez podziału na partycje, ale kolejek i tematów w przestrzeni nazw Premium zawsze są podzielone na partycje; Nie można wyłączyć tę opcję. 

Nie jest możliwe toochange hello partycje opcji dla istniejącej kolejki lub tematu w warstwy standardowa lub Premium, można ustawić tylko opcja hello podczas tworzenia jednostki hello.

## <a name="how-it-works"></a>Jak to działa

Każdy partycjonowanej kolejka lub temat składa się z wielu fragmentów. Każdy fragment jest przechowywane w różnych magazynie obsługi komunikatów i obsługiwane przez brokera inny komunikat. Po wysłaniu wiadomości tooa partycjonowanej kolejka lub temat usługi Service Bus przypisuje tooone wiadomość hello hello fragmentów. Wybór Hello odbywa się losowo przez magistralę usług lub można określić za pomocą klucza partycji, który hello nadawcy.

Gdy klient chce tooreceive wiadomości z kolejki podzielonym na partycje, lub z tematu partycjonowanej tooa subskrypcji, usługi Service Bus kwerendy, wszystkie fragmenty wiadomości, zwraca pierwszą wiadomość hello, uzyskany z dowolnego z magazynów toohello odbiorcy wiadomości powitania. Pamięci podręczne usługi Service Bus hello inne komunikaty i zwraca je po odebraniu dodatkowe odbierania żądań. Odbieranie klienta nie został powiadomiony o hello partycjonowanie; Witaj partycjonowanej kolejka lub temat zachowanie po stronie klienta (na przykład Odczyt, ukończenia, odroczenie utraconych wiadomości, Odczyt z wyprzedzeniem) jest identyczne toohello zachowanie regularne jednostki.

Nie ma żadnych dodatkowych kosztów przy wysyłaniu wiadomości lub odbierania wiadomości z kolejki podzielonym na partycje lub temat.

## <a name="enable-partitioning"></a>Włącz partycjonowania

toouse podzielona na partycje kolejek i tematów z usługi Azure Service Bus, użyj hello Azure SDK w wersji 2,2 lub nowszej, lub określ `api-version=2013-10` w HTTP żądania.

### <a name="standard"></a>Standardowa

W warstwie standardowej obsługi wiadomości powitania można utworzyć kolejki usługi Service Bus i tematów w rozmiarze 1, 2, 3, 4 lub 5 GB (domyślnie hello jest 1 GB). Z partycjonowania włączone, usługi Service Bus tworzy 16 kopie (16 partycji) hello jednostki dla każdego Gigabajta określisz. Tak, można utworzyć kolejkę o rozmiarze 5 GB, z 16 partycji hello maksymalny rozmiar kolejki staje się (5 \* 16) = 80 GB. Widać hello maksymalny rozmiar kolejki podzielonym na partycje lub tematu, analizując jego wpis na powitania [portalu Azure][Azure portal], w hello **omówienie** bloku dla tej jednostki.

### <a name="premium"></a>Premium

W przypadku przestrzeni nazw warstwy Premium można utworzyć kolejki usługi Service Bus i tematów w rozmiarze 1, 2, 3, 4, 5, 10, 20, 40 lub 80 GB (domyślnie hello jest 1 GB). W partycji, domyślnie włączona, usługi Service Bus tworzy dwie partycje nieobsługujące jednostki. Widać hello maksymalny rozmiar kolejki podzielonym na partycje lub tematu, analizując jego wpis na powitania [portalu Azure][Azure portal], w hello **omówienie** bloku dla tej jednostki.

Aby uzyskać więcej informacji na temat partycjonowania w warstwie obsługi wiadomości powitania Premium, zobacz [usługi Service Bus w warstwie Premium i standardowa komunikatami w warstwie](service-bus-premium-messaging.md). 

### <a name="create-a-partitioned-entity"></a>Utwórz jednostkę podzielonym na partycje

Istnieje kilka sposobów toocreate kolejki podzielonym na partycje lub temat. Podczas tworzenia kolejki hello lub tematu z aplikacji, można włączyć podział hello kolejka lub temat przez odpowiednio ustawienia hello [QueueDescription.EnablePartitioning] [ QueueDescription.EnablePartitioning] lub [TopicDescription.EnablePartitioning] [ TopicDescription.EnablePartitioning] właściwości zbyt**true**. Te właściwości musi być ustawiony na powitania czas hello kolejki lub tematu jest tworzony. Jak wspomniano wcześniej, to nie jest możliwe toochange tych właściwości na istniejącej kolejki lub temat. Na przykład:

```csharp
// Create partitioned topic
NamespaceManager ns = NamespaceManager.CreateFromConnectionString(myConnectionString);
TopicDescription td = new TopicDescription(TopicName);
td.EnablePartitioning = true;
ns.CreateTopic(td);
```

Alternatywnie możesz utworzyć partycjonowanej kolejka lub temat w hello [portalu Azure] [ Azure portal] lub w programie Visual Studio. Po utworzeniu kolejka lub temat w portalu hello hello **włączyć partycjonowania** opcję hello kolejka lub temat **Utwórz** bloku jest domyślnie zaznaczone. Tylko można wyłączyć tę opcję w jednostce warstwy standardowa; w hello partycjonowania warstwy Premium jest zawsze włączone. W programie Visual Studio, kliknij przycisk hello **włączyć partycjonowania** checkbox w hello **nową kolejkę** lub **nowy temat** okno dialogowe.

## <a name="use-of-partition-keys"></a>Użycie kluczy partycji
Gdy komunikat jest dodawanych do kolejki w podzielonym na partycje kolejka lub temat, usługi Service Bus sprawdza obecność hello klucza partycji. Jeśli zostanie znaleziony, wybiera fragmentu hello na podstawie tego klucza. Jeśli nie znajdzie klucza partycji, wybiera fragmentu hello na podstawie wewnętrznego algorytmu.

### <a name="using-a-partition-key"></a>Użycie klucza partycji
Niektóre scenariusze, takie jak sesji lub transakcji, wymagają toobe wiadomości przechowywane w określonych fragmentu. Te scenariusze wymagają hello użycie klucza partycji. Wszystkie komunikaty o tym hello Użyj tego samego klucza partycji są przypisane toohello sam fragmentu. Jeśli fragmentu hello jest tymczasowo niedostępny, usługi Service Bus zwraca błąd.

W zależności od scenariusza hello inny komunikat właściwości są używane jako klucza partycji:

**Identyfikator sesji**: Jeśli wiadomość hello [BrokeredMessage.SessionId] [ BrokeredMessage.SessionId] ustaw właściwość, a następnie usługi Service Bus używa tej właściwości jako klucza partycji hello. W ten sposób, wszystkie komunikaty, które należy toohello tej samej sesji są obsługiwane przez hello sam brokera komunikatów. Dzięki temu usługi Service Bus tooguarantee komunikat porządkowanie oraz hello spójności stanów sesji.

**PartitionKey**: Jeśli wiadomość hello [BrokeredMessage.PartitionKey] [ BrokeredMessage.PartitionKey] właściwość, ale nie hello [BrokeredMessage.SessionId] [ BrokeredMessage.SessionId] ustaw właściwość, a następnie Usługa Service Bus używa hello [PartitionKey] [ PartitionKey] właściwość jako klucza partycji hello. Jeśli wiadomość hello ma zarówno hello [SessionId] [ SessionId] i hello [PartitionKey] [ PartitionKey] zestaw właściwości obie właściwości muszą być takie same. Jeśli hello [PartitionKey] [ PartitionKey] ustawiono właściwość tooa wartość inną niż hello [SessionId] [ SessionId] właściwość, usługi Service Bus zwraca jest nieprawidłowa wyjątek operacji. Witaj [PartitionKey] [ PartitionKey] właściwości należy używać, gdy nadawca wysyła wiadomości transakcyjne pamiętać-session. Witaj klucza partycji gwarantuje, że wszystkie komunikaty, które są wysyłane w ramach transakcji są obsługiwane przez hello sam brokera obsługi komunikatów.

**Identyfikator komunikatu**: Jeśli hello kolejka lub temat ma hello [QueueDescription.RequiresDuplicateDetection] [ QueueDescription.RequiresDuplicateDetection] właściwość zbyt**true** i hello [BrokeredMessage.SessionId] [ BrokeredMessage.SessionId] lub [BrokeredMessage.PartitionKey] [ BrokeredMessage.PartitionKey] właściwości nie są ustawione, a następnie hello [BrokeredMessage.MessageId] [ BrokeredMessage.MessageId] właściwość służy jako klucza partycji hello. (Należy pamiętać, że biblioteki Microsoft .NET i protokołu AMQP hello automatycznie przypisywać identyfikator komunikatu, jeśli aplikacja wysyłająca hello nie). W takim przypadku wszystkie kopie obsługi przez tę samą wiadomość hello hello tego samego brokera komunikatów. To umożliwia toodetect usługi Service Bus i wyeliminowania zduplikowanych wiadomości. Jeśli hello [QueueDescription.RequiresDuplicateDetection] [ QueueDescription.RequiresDuplicateDetection] nie ustawiono właściwości zbyt**true**, magistrali usług nie należy wziąć pod uwagę hello [MessageId] [ MessageId] właściwość jako klucza partycji.

### <a name="not-using-a-partition-key"></a>Nie używa klucza partycji
W przypadku braku hello klucza partycji usługi Service Bus dystrybuuje wiadomości w okrężne tooall hello fragmentów hello partycjonowanej kolejka lub temat. Jeśli wybrany hello fragmentu nie jest dostępna, usługi Service Bus przypisuje fragmentu różnych tooa wiadomość hello. W ten sposób operacji wysyłania hello powiedzie się niezależnie od hello tymczasowej niedostępności magazynie obsługi komunikatów. Nie będzie jednak osiągnąć hello gwarancji, porządkowanie, że klucz partycji zawiera.

Aby uzyskać bardziej szczegółowym omówieniem hello zależności między dostępności (nie klucza partycji) i spójności (przy użyciu klucza partycji), zobacz [w tym artykule](../event-hubs/event-hubs-availability-and-consistency.md). Te informacje dotyczą jednakowo toopartitioned jednostek usługi Service Bus i usługi Event Hubs partycji.

toogive usługi magistrali wiadomości powitania tooenqueue wystarczająco dużo czasu do fragmentu różnych hello [MessagingFactorySettings.OperationTimeout] [ MessagingFactorySettings.OperationTimeout] wartość określoną przez powitania klienta, który wysyła wiadomości powitania musi być większa niż 15 sekund. Zalecane jest, aby ustawić hello [OperationTimeout] [ OperationTimeout] właściwości toohello domyślną wartość 60 sekund.

Należy pamiętać, że klucz partycji "PIN" fragmentu określonych tooa komunikatu. Jeśli hello magazynie obsługi komunikatów, który zawiera ten fragment jest niedostępny, usługi Service Bus zwraca błąd. W przypadku braku hello klucza partycji usługi Service Bus można wybrać różne fragmentu i hello operacja zakończy się powodzeniem. Dlatego zaleca się, że nie zostanie podany klucz partycji, chyba że jest to wymagane.

## <a name="advanced-topics-use-transactions-with-partitioned-entities"></a>Tematy zaawansowane: transakcji za pomocą partycjonowane jednostki
Komunikaty, które są wysyłane jako część transakcji muszą określać klucz partycji. Może to być jeden z następujących właściwościach hello: [BrokeredMessage.SessionId][BrokeredMessage.SessionId], [BrokeredMessage.PartitionKey][BrokeredMessage.PartitionKey], lub [ BrokeredMessage.MessageId][BrokeredMessage.MessageId]. Wszystkie komunikaty, które są wysyłane jako część hello musi określać tej samej transakcji hello tego samego klucza partycji. Jeśli podjęto toosend wiadomość bez klucza partycji w obrębie transakcji usługi Service Bus zwraca wyjątek Nieprawidłowa operacja. Jeśli próba toosend wiele komunikatów w ramach hello tej samej transakcji, które mają różne klucze partycji, usługi Service Bus zwraca wyjątek Nieprawidłowa operacja. Na przykład:

```csharp
CommittableTransaction committableTransaction = new CommittableTransaction();
using (TransactionScope ts = new TransactionScope(committableTransaction))
{
    BrokeredMessage msg = new BrokeredMessage("This is a message");
    msg.PartitionKey = "myPartitionKey";
    messageSender.Send(msg); 
    ts.Complete();
}
committableTransaction.Commit();
```

Jeśli ustawiono hello właściwości, które służą jako klucza partycji, numerów PIN usługi Service Bus hello fragmentu określonych tooa komunikatu. Dzieje się tak, czy transakcja jest używany. Zaleca się, że nie określisz klucza partycji, jeśli nie jest konieczne.

## <a name="using-sessions-with-partitioned-entities"></a>Korzystanie z sesji z partycjonowane jednostki
temat wiadomości transakcyjnych obsługujący sesji tooa toosend lub kolejki wiadomości powitania musi mieć hello [BrokeredMessage.SessionId] [ BrokeredMessage.SessionId] zestawu właściwości. Jeśli hello [BrokeredMessage.PartitionKey] [ BrokeredMessage.PartitionKey] także określona właściwość, musi ona być identyczne toohello [SessionId] [ SessionId] właściwości. Jeśli będą się różnić, usługi Service Bus zwraca wyjątek Nieprawidłowa operacja.

W odróżnieniu od regularne (niepartycjonowany) kolejki i tematy nie jest możliwe toouse toosend jednej transakcji wiele sesji toodifferent wiadomości. Jeśli podjęto, usługi Service Bus zwraca wyjątek Nieprawidłowa operacja. Na przykład:

```csharp
CommittableTransaction committableTransaction = new CommittableTransaction();
using (TransactionScope ts = new TransactionScope(committableTransaction))
{
    BrokeredMessage msg = new BrokeredMessage("This is a message");
    msg.SessionId = "mySession";
    messageSender.Send(msg); 
    ts.Complete();
}
committableTransaction.Commit();
```

## <a name="automatic-message-forwarding-with-partitioned-entities"></a>Przekazywanie komunikatów automatyczne z partycjonowane jednostki
Usługa Service Bus obsługuje komunikat automatycznego przesyłania dalej z, aby lub między partycjonowane jednostki. tooenable komunikat automatycznego przekazywania, ustaw hello [QueueDescription.ForwardTo] [ QueueDescription.ForwardTo] właściwości kolejki źródłowej hello lub subskrypcji. Jeśli wiadomość hello Określa klucz partycji ([SessionId][SessionId], [PartitionKey][PartitionKey], lub [MessageId] [ MessageId]), ten klucz partycji służy do jednostki docelowej hello.

## <a name="considerations-and-guidelines"></a>Zagadnienia i wskazówki
* **Funkcje wysokiej spójności**: Jeśli jednostki korzysta z funkcji, takich jak sesje, wykrywania duplikatów lub jawne kontrolę nad kluczem partycjonowania, a następnie operacje obsługi wiadomości powitania są zawsze routingiem toospecific fragmenty. Jeśli środowisko wszelkie fragmenty hello dużego natężenia ruchu sieciowego lub odpowiedni magazyn hello jest zła, te operacje kończą się niepowodzeniem i zmniejsza dostępności. Generalnie spójności hello jest nadal znacznie wyższa niż niepartycjonowany jednostki; tylko podzestaw ruchu wystąpiły problemy, jako min. tooall hello ruchu. Aby uzyskać więcej informacji, zobacz [Omówienie dostępności i spójności](../event-hubs/event-hubs-availability-and-consistency.md).
* **Zarządzanie**: operacje takie jak tworzenie, Update i Delete musi zostać wykonana na wszystkie fragmenty hello hello jednostki. Jeśli wszystkie fragment jest zła może spowodować błędy do tych operacji. Dla operacji Get hello informacje takie jak liczba wiadomości musi być agregowana z wszystkie fragmenty. Jeśli wszystkie fragment jest zła, stan dostępności jednostki hello został zgłoszony jako ograniczone.
* **Niska scenariuszy komunikat**: dla takich scenariuszy, szczególnie w przypadku, gdy używany jest protokół hello HTTP, może być tooperform wielu operacji pobrania w kolejności tooobtain wszystkie wiadomości powitania. Dla żądania odbierania hello frontonu wykonuje receive na wszystkie fragmenty hello i buforuje wszystkich hello odpowiedzi. Żądania odbierania kolejnych na powitania tego samego połączenia będzie korzystać z tej pamięci podręcznej i odbierania opóźnienia będzie niższa. Jednak jeśli masz wiele połączeń lub za pomocą protokołu HTTP, który ustanawia nowego połączenia dla każdego żądania. W efekcie nie ma żadnej gwarancji, że będzie on trafić na powitania tym samym węźle. Jeśli wszystkie istniejące wiadomości są zablokowane i są przechowywane w innej frontonu hello wyświetlony zwraca operacji **null**. Po pewnym czasie wygaśnięcia wiadomości i może odbierać je ponownie. Utrzymanie aktywności HTTP jest zalecane.
* **Przeglądaj/Peek wiadomości**: [PeekBatch](/dotnet/api/microsoft.servicebus.messaging.queueclient#Microsoft_ServiceBus_Messaging_QueueClient_PeekBatch_System_Int32_) nie zawsze zwraca hello liczbę wiadomości określona w hello [MessageCount](/dotnet/api/microsoft.servicebus.messaging.queuedescription#Microsoft_ServiceBus_Messaging_QueueDescription_MessageCount) właściwości. Istnieją dwie typowe powody to. Jedną z przyczyn jest tym hello zagregowany rozmiar wiadomości powitania kolekcji przekracza maksymalny rozmiar hello 256 KB. Inną przyczyną jest to, że jeśli hello kolejka lub temat ma hello [właściwości parametr EnablePartitioning](/dotnet/api/microsoft.servicebus.messaging.queuedescription#Microsoft_ServiceBus_Messaging_QueueDescription_EnablePartitioning) ustawić także**wartość true,**, partycji może nie mieć wystarczającej liczby wiadomości powitania toocomplete żądana liczba komunikatów. Ogólnie rzecz biorąc, jeśli aplikacja potrzebuje tooreceive określoną liczbę wiadomości, powinna wywołać [PeekBatch](/dotnet/api/microsoft.servicebus.messaging.queueclient#Microsoft_ServiceBus_Messaging_QueueClient_PeekBatch_System_Int32_) aż pobiera tej liczby wiadomości, lub nie ma żadnych toopeek więcej wiadomości. Aby uzyskać więcej informacji, przykłady kodu, w tym temacie [QueueClient.PeekBatch](/dotnet/api/microsoft.servicebus.messaging.queueclient#Microsoft_ServiceBus_Messaging_QueueClient_PeekBatch_System_Int32_) lub [SubscriptionClient.PeekBatch](/dotnet/api/microsoft.servicebus.messaging.subscriptionclient#Microsoft_ServiceBus_Messaging_SubscriptionClient_PeekBatch_System_Int32_).

## <a name="latest-added-features"></a>Najnowsze funkcje dodane
* Dodawanie lub usuwanie reguł jest teraz obsługiwana przez partycjonowane jednostki. Inne niż niepartycjonowany jednostki, te operacje nie są obsługiwane w transakcji. 
* Protokół AMQP jest teraz obsługiwana do wysyłania i odbierania wiadomości tooand z partycjonowane jednostki.
* AMQP jest teraz obsługiwana przez hello następujące operacje: [wysyłania partii](/dotnet/api/microsoft.servicebus.messaging.queueclient#Microsoft_ServiceBus_Messaging_QueueClient_SendBatch_System_Collections_Generic_IEnumerable_Microsoft_ServiceBus_Messaging_BrokeredMessage__), [odbierania partii](/dotnet/api/microsoft.servicebus.messaging.queueclient#Microsoft_ServiceBus_Messaging_QueueClient_ReceiveBatch_System_Int32_), [Receive numer porządkowy](/dotnet/api/microsoft.servicebus.messaging.queueclient#Microsoft_ServiceBus_Messaging_QueueClient_Receive_System_Int64_), [wgląd](/dotnet/api/microsoft.servicebus.messaging.queueclient#Microsoft_ServiceBus_Messaging_QueueClient_Peek), [ Odnów blokady](/dotnet/api/microsoft.servicebus.messaging.queueclient#Microsoft_ServiceBus_Messaging_QueueClient_RenewMessageLock_System_Guid_), [zaplanować komunikat](/dotnet/api/microsoft.servicebus.messaging.queueclient#Microsoft_ServiceBus_Messaging_QueueClient_ScheduleMessageAsync_Microsoft_ServiceBus_Messaging_BrokeredMessage_System_DateTimeOffset_), [Anuluj zaplanowane wiadomość](/dotnet/api/microsoft.servicebus.messaging.queueclient#Microsoft_ServiceBus_Messaging_QueueClient_CancelScheduledMessageAsync_System_Int64_), [Dodaj regułę](/dotnet/api/microsoft.servicebus.messaging.ruledescription), [Usuń regułę](/dotnet/api/microsoft.servicebus.messaging.ruledescription), [Sesji odnawiania blokady](/dotnet/api/microsoft.servicebus.messaging.messagesession#Microsoft_ServiceBus_Messaging_MessageSession_RenewLock), [stanu sesji zestaw](/dotnet/api/microsoft.servicebus.messaging.messagesession#Microsoft_ServiceBus_Messaging_MessageSession_SetState_System_IO_Stream_), [stanu sesji Get](/dotnet/api/microsoft.servicebus.messaging.messagesession#Microsoft_ServiceBus_Messaging_MessageSession_GetState), i [wyliczyć sesji](/dotnet/api/microsoft.servicebus.messaging.queueclient#Microsoft_ServiceBus_Messaging_QueueClient_GetMessageSessionsAsync).

## <a name="partitioned-entities-limitations"></a>Ograniczenia partycjonowane jednostki
Obecnie usługi Service Bus nakłada następujące ograniczenia w podzielonym na partycje kolejek i tematów hello:

* Partycjonowane kolejek i tematów nie obsługują wysyłanie wiadomości, które należą toodifferent sesji w ramach jednej transakcji.
* Usługi Service Bus umożliwia obecnie kolejek too100 podzielona na partycje lub tematy na przestrzeni nazw. Każdy partycjonowanej kolejka lub temat, liczy się przydziału hello 10 000 jednostek na przestrzeń nazw (nie dotyczy to warstwy tooPremium).

## <a name="next-steps"></a>Następne kroki
Zobacz Omówienie hello [obsługi protokołu AMQP 1.0 dla usługi Service Bus podzielona na partycje, kolejek i tematów] [ AMQP 1.0 support for Service Bus partitioned queues and topics] toolearn więcej informacji na temat partycjonowania jednostek obsługi komunikatów. 

[Service Bus architecture]: service-bus-architecture.md
[Azure portal]: https://portal.azure.com
[QueueDescription.EnablePartitioning]: /dotnet/api/microsoft.servicebus.messaging.queuedescription#Microsoft_ServiceBus_Messaging_QueueDescription_EnablePartitioning
[TopicDescription.EnablePartitioning]: /dotnet/api/microsoft.servicebus.messaging.topicdescription#Microsoft_ServiceBus_Messaging_TopicDescription_EnablePartitioning
[BrokeredMessage.SessionId]: /dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_SessionId
[BrokeredMessage.PartitionKey]: /dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_PartitionKey
[SessionId]: /dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_SessionId
[PartitionKey]: /dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_PartitionKey
[QueueDescription.RequiresDuplicateDetection]: /dotnet/api/microsoft.servicebus.messaging.queuedescription#Microsoft_ServiceBus_Messaging_QueueDescription_RequiresDuplicateDetection
[BrokeredMessage.MessageId]: /dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_MessageId
[MessageId]: /dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_MessageId
[MessagingFactorySettings.OperationTimeout]: /dotnet/api/microsoft.servicebus.messaging.messagingfactorysettings#Microsoft_ServiceBus_Messaging_MessagingFactorySettings_OperationTimeout
[OperationTimeout]: /dotnet/api/microsoft.servicebus.messaging.messagingfactorysettings#Microsoft_ServiceBus_Messaging_MessagingFactorySettings_OperationTimeout
[QueueDescription.ForwardTo]: /dotnet/api/microsoft.servicebus.messaging.queuedescription#Microsoft_ServiceBus_Messaging_QueueDescription_ForwardTo
[AMQP 1.0 support for Service Bus partitioned queues and topics]: service-bus-partitioned-queues-and-topics-amqp-overview.md
