---
title: aaaOverview transakcji przetwarzania w Azure Service Bus | Dokumentacja firmy Microsoft
description: "Omówienie usługi Azure Service Bus atomic transakcji i za pośrednictwem"
services: service-bus-messaging
documentationcenter: .net
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 64449247-1026-44ba-b15a-9610f9385ed8
ms.service: service-bus-messaging
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/17/2017
ms.author: clemensv;sethm
ms.openlocfilehash: 5ed4d1fd3a089b8ebcd69a568f4ac863e753aecd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="overview-of-service-bus-transaction-processing"></a>Omówienie przetwarzanie transakcji usługi Service Bus
W tym artykule omówiono możliwości transakcji hello Azure Service Bus. Większość dyskusji hello jest zilustrowane hello [Atomic transakcji z usługi Service Bus próbki](https://github.com/Azure/azure-service-bus/tree/master/samples/DotNet/Microsoft.ServiceBus.Messaging/AtomicTransactions). Ten artykuł zawiera omówienie tooan ograniczone przetwarzanie transakcji i hello *wyśle* funkcji w usłudze Service Bus, podczas przykład Atomic transakcji hello jest bardziej rozbudowaną i bardziej złożonej w zakresie.

## <a name="transactions-in-service-bus"></a>Transakcje w usłudze Service Bus
A [transakcji](https://github.com/Azure/azure-service-bus/tree/master/samples/DotNet/Microsoft.ServiceBus.Messaging/AtomicTransactions#what-are-transactions) grupowanie dwóch lub więcej operacji w *zakresu wykonywania*. Natury takich transakcji musi upewnij się, że wszystkie operacje należących do danej grupy działań tooa powiedzie się lub wspólnie zakończyć się niepowodzeniem. W związku z tym transakcji pełnić jedną jednostkę, która jest często tooas określonego *niepodzielność*. 

Usługa Service Bus jest brokera wiadomości transakcyjnych i zapewnia integralność transakcyjne dla wszystkich operacji wewnętrznych przed jego magazyny wiadomości. Wszystkie operacje transferu komunikatów wewnątrz usługi Service Bus, takich jak przenoszenie wiadomości tooa [kolejki utraconych wiadomości](service-bus-dead-letter-queues.md) lub [automatyczne przekazywanie](service-bus-auto-forwarding.md) komunikatów między jednostkami, są transakcyjnych. Tak Jeśli usługi Service Bus akceptuje wiadomości, już został przechowywane i z liczbą sekwencji. Następnie wszelkich transferów komunikatów w ramach usługi Service Bus są skoordynowanej operacji w ramach jednostkami i nie będzie prowadzić tooloss (źródła zakończy się pomyślnie i docelowa kończy się niepowodzeniem) lub tooduplication (źródłowego nie powiedzie się i docelowego zakończy się powodzeniem) wiadomości powitania.

Usługa Service Bus obsługuje operacje grupowania względem jednej jednostki obsługi komunikatów (kolejki, tematu, subskrypcji) w zakresie hello transakcji. Na przykład kilka kolejki tooone wiadomości z może wysyłać w zakresie transakcji, a wiadomości powitania będą tylko zatwierdzone toohello kolejki dziennika po pomyślnym zakończeniu hello transakcji.

## <a name="operations-within-a-transaction-scope"></a>Operacje w zakresie transakcji
dostępne są następujące operacje Hello, które mogą być wykonywane w zakresie transakcji:

* **[QueueClient](/dotnet/api/microsoft.servicebus.messaging.queueclient), [MessageSender](/dotnet/api/microsoft.servicebus.messaging.messagesender), [TopicClient](/dotnet/api/microsoft.servicebus.messaging.topicclient)**: wysyłanie SendAsync, SendBatch, SendBatchAsync 
* **[BrokeredMessage](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage)**: zakończeniu CompleteAsync, porzucenia, AbandonAsync, utraconych wiadomości, DeadletterAsync, wstrzymuje, DeferAsync, RenewLock, RenewLockAsync 

Odbieranie operacje nie są uwzględnione, ponieważ zakłada się, że aplikacja hello nabywa komunikaty przy użyciu hello [ReceiveMode.PeekLock](/dotnet/api/microsoft.servicebus.messaging.receivemode) tryb, w niektórych pętlę odbierania lub [OnMessage](/dotnet/api/microsoft.servicebus.messaging.messagereceiver#Microsoft_ServiceBus_Messaging_MessageReceiver_OnMessage_System_Action_Microsoft_ServiceBus_Messaging_BrokeredMessage__Microsoft_ServiceBus_Messaging_OnMessageOptions_) wywołania zwrotnego, i zakres tylko następnie otwiera transakcji wiadomość hello przetwarzania.

Hello dyspozycji wiadomość hello (zakończeniu porzucenia, wiadomości utraconych odroczyć) następnie odbywa się w zakresie hello, w zależności od, hello ogólną wyniku hello transakcji.

## <a name="transfers-and-send-via"></a>Transfery i "Wyślij za pośrednictwem"
tooenable transakcyjnych przekazania danych z kolejki tooa procesora, a następnie tooanother kolejki, Usługa Service Bus obsługuje *transferów*. W operacji przeniesienia nadawcy najpierw wysyła tooa komunikat "kolejce transferu" i kolejce transferu hello natychmiast przenosi toohello wiadomość hello mającą przy użyciu hello sam niezawodne transfer implementację, która opiera się możliwość automatycznego przekazywania hello kolejki docelowej na serwerze. wiadomości powitania nigdy nie jest dziennika kolejce transferu toohello zadeklarowanej w taki sposób, że stają się one widoczne dla użytkowników w kolejce transferu hello.

power Hello tej możliwości transakcyjnych stała się oczywista, gdy samej kolejki transfer hello jest źródłem hello komunikaty wejściowe hello nadawcy. Innymi słowy, usługi Service Bus można przetransferować kolejki docelowej toohello wiadomość hello "przez" hello kolejce transferu, podczas wykonywania pełnego (lub mają być odroczone, lub utraconych) operacji na powitania komunikat wejściowy wszystko w jednym niepodzielną operację. 

### <a name="see-it-in-code"></a>Zobacz go w kodzie
tooset się przeniesienie, możesz utworzyć przeznaczonego dla kolejki docelowej hello za pośrednictwem kolejki transfer hello nadawcy wiadomości. Konieczne będzie również odbiornik, który pobiera komunikaty z tej samej kolejki. Na przykład:

```csharp
var sender = this.messagingFactory.CreateMessageSender(destinationQueue, myQueueName);
var receiver = this.messagingFactory.CreateMessageReceiver(myQueueName);
```

Następnie proste transakcji korzysta z tych elementów, jak hello poniższy przykład:

```csharp
var msg = receiver.Receive();

using (scope = new TransactionScope())
{
    // Do whatever work is required 

    var newmsg = ... // package hello result 

    msg.Complete(); // mark hello message as done
    sender.Send(newmsg); // forward hello result

    scope.Complete(); // declare hello transaction done
} 
```

## <a name="next-steps"></a>Następne kroki

Zobacz następujące artykuły, aby uzyskać więcej informacji na temat kolejek usługi Service Bus hello:

* [Tworzenie łańcuchów jednostek usługi Service Bus z automatyczne przekazywanie](service-bus-auto-forwarding.md)
* [Przykładowe do przodu automatycznie](https://github.com/Azure/azure-service-bus/tree/master/samples/DotNet/Microsoft.ServiceBus.Messaging/AutoForward)
* [Niepodzielne transakcji z usługi Service Bus próbki](https://github.com/Azure/azure-service-bus/tree/master/samples/DotNet/Microsoft.ServiceBus.Messaging/AtomicTransactions)
* [Azure kolejki i usługi Service Bus w porównaniu kolejek](service-bus-azure-and-service-bus-queues-compared-contrasted.md)
* [Jak toouse kolejek usługi Service Bus](service-bus-dotnet-get-started-with-queues.md)

