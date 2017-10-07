---
title: "kolejki utraconych wiadomości magistrali aaaService | Dokumentacja firmy Microsoft"
description: "Omówienie usługi Azure Service Bus kolejki utraconych wiadomości"
services: service-bus-messaging
documentationcenter: .net
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 68b2aa38-dba7-491a-9c26-0289bc15d397
ms.service: service-bus-messaging
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/17/2017
ms.author: clemensv;sethm
ms.openlocfilehash: 1638272085b8a3a59e8814f6f943caee35a2bfdc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="overview-of-service-bus-dead-letter-queues"></a>Omówienie kolejki utraconych wiadomości usługi Service Bus

Kolejki usługi Service Bus i subskrypcje tematu zapewniają podrzędnej kolejki dodatkowej, nazywany *kolejki utraconych wiadomości* (DLQ). kolejki utraconych wiadomości powitania nie jest konieczne toobe jawnie utworzone i nie może być usunięty lub w inny sposób niezależny od zarządzanych hello głównego jednostki.

W tym artykule omówiono kolejki utraconych wiadomości w Azure Service Bus. Większość dyskusji hello jest zilustrowane hello [próbki kolejki utraconych wiadomości](https://github.com/Azure/azure-service-bus/tree/master/samples/DotNet/Microsoft.ServiceBus.Messaging/DeadletterQueue) w witrynie GitHub.
 
## <a name="hello-dead-letter-queue"></a>kolejki utraconych wiadomości powitania

Witaj kolejki utraconych wiadomości powitania służy toohold wiadomości, których nie można dostarczyć odbiornika tooany lub wiadomości, których nie można przetworzyć. Komunikaty można następnie usuwane z hello DLQ i inspekcji. Aplikacji może za pomocą operatora, rozwiązać problemy i ponownie prześlij wiadomość hello, dziennika hello fakt, że wystąpił błąd i podjęcia działań naprawczych. 

Z perspektywy interfejsu API i protokół hello DLQ jest przeważnie podobne tooany innych kolejki z tą różnicą, że komunikaty mogą zostać przesłane tylko za pomocą gestu utraconych wiadomości powitania hello nadrzędnej jednostki. Ponadto, time-to-live nie zostaną spełnione, a nie utraconych komunikatów z DLQ. kolejki utraconych wiadomości powitania w pełni obsługuje operacje transakcyjne i dostarczania peek blokady.

Należy zauważyć, że nie jest Brak automatycznego oczyszczania hello DLQ. Wiadomości pozostaną w hello DLQ, dopóki jawnie je odzyskać z hello DLQ i wywołanie [Complete()](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_CompleteAsync) hello utraconych wiadomości.

## <a name="moving-messages-toohello-dlq"></a>Przenoszenie wiadomości toohello DLQ

Ma kilka działań w usłudze Service Bus, powodujących tooget komunikatów wypchniętych toohello DLQ od w hello aparat się do obsługi komunikatów. Aplikacja również jawnie można przenosić wiadomości toohello DLQ. 

Jako Broker hello pobiera przenieść tej wiadomości powitania, dwie właściwości są dodawane komunikat toohello jako hello broker wywołuje jego wewnętrznego wersja hello [utraconych wiadomości](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_DeadLetter_System_String_System_String_) metody na wiadomość powitania: `DeadLetterReason` i `DeadLetterErrorDescription`.

Aplikacje mogą definiować własne kody hello `DeadLetterReason` właściwości, ale hello zestawów systemu hello następujące wartości.

| Warunek | DeadLetterReason | DeadLetterErrorDescription |
| --- | --- | --- |
| Zawsze |HeaderSizeExceeded |Przekroczono przydział rozmiaru powitania dla tego strumienia. |
| ! TopicDescription.<br />EnableFilteringMessagesBeforePublishing i SubscriptionDescription.<br />EnableDeadLetteringOnFilterEvaluationExceptions |wyjątek. GetType(). Nazwa |wyjątek. Komunikat |
| EnableDeadLetteringOnMessageExpiration |TTLExpiredException |wiadomości powitania wygasła i została martwych lettered. |
| SubscriptionDescription.RequiresSession |Identyfikator sesji ma wartość null. |Jednostki włączone sesji nie pozwala na komunikat, którego identyfikator sesji ma wartość null. |
| ! kolejki utraconych wiadomości |MaxTransferHopCountExceeded |Wartość null |
| Jawne martwych drukiem aplikacji |Określone przez aplikację |Określone przez aplikację |

## <a name="exceeding-maxdeliverycount"></a>Powyżej MaxDeliveryCount
Kolejki, jak i subskrypcje mają [QueueDescription.MaxDeliveryCount](/dotnet/api/microsoft.servicebus.messaging.queuedescription#Microsoft_ServiceBus_Messaging_QueueDescription_MaxDeliveryCount) i [SubscriptionDescription.MaxDeliveryCount](/dotnet/api/microsoft.servicebus.messaging.subscriptiondescription#Microsoft_ServiceBus_Messaging_SubscriptionDescription_MaxDeliveryCount) właściwości odpowiednio; hello wartość domyślna to 10. Zawsze, gdy wiadomość została dostarczona w obszarze blokady ([ReceiveMode.PeekLock](/dotnet/api/microsoft.servicebus.messaging.receivemode)), ale został albo jawnie porzucone lub blokady hello wygasło wiadomości powitania [BrokeredMessage.DeliveryCount](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_DeliveryCount) jest zwiększany. Gdy [DeliveryCount](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_DeliveryCount) przekracza [MaxDeliveryCount](/dotnet/api/microsoft.servicebus.messaging.queuedescription#Microsoft_ServiceBus_Messaging_QueueDescription_MaxDeliveryCount), wiadomość hello jest przeniesionego toohello DLQ, określając hello `MaxDeliveryCountExceeded` kod przyczyny.

Nie można wyłączyć to zachowanie, ale możesz ustawić [MaxDeliveryCount](/dotnet/api/microsoft.servicebus.messaging.queuedescription#Microsoft_ServiceBus_Messaging_QueueDescription_MaxDeliveryCount) tooa bardzo dużą liczbą.

## <a name="exceeding-timetolive"></a>Wartość TimeToLive powyżej
Gdy hello [QueueDescription.EnableDeadLetteringOnMessageExpiration](/dotnet/api/microsoft.servicebus.messaging.queuedescription#Microsoft_ServiceBus_Messaging_QueueDescription_EnableDeadLetteringOnMessageExpiration) lub [SubscriptionDescription.EnableDeadLetteringOnMessageExpiration](/dotnet/api/microsoft.servicebus.messaging.subscriptiondescription#Microsoft_ServiceBus_Messaging_SubscriptionDescription_EnableDeadLetteringOnMessageExpiration) właściwość jest ustawiona zbyt**true** (domyślnie hello **false**), wszystkie komunikaty wygaszenie są przeniesionego toohello DLQ, określając hello `TTLExpiredException` kod przyczyny.

Zauważ, że komunikaty wygasłe są tylko usunięte i w związku z tym przeniesiony toohello DLQ, gdy istnieje co najmniej jeden odbiornik active ściąganie kolejki głównej hello lub subskrypcji; to zachowanie jest celowe.

## <a name="errors-while-processing-subscription-rules"></a>Wystąpiły błędy podczas przetwarzania reguły subskrypcji
Gdy hello [SubscriptionDescription.EnableDeadLetteringOnFilterEvaluationExceptions](/dotnet/api/microsoft.servicebus.messaging.subscriptiondescription#Microsoft_ServiceBus_Messaging_SubscriptionDescription_EnableDeadLetteringOnFilterEvaluationExceptions) właściwości jest włączony dla subskrypcji, wszystkie błędy, które są wykonywane, gdy wykonuje regułę filtru SQL subskrypcji są przechwytywane hello DLQ wraz z naruszeń wiadomość hello.

## <a name="application-level-dead-lettering"></a>Poziom aplikacji obsługa utraconych komunikatów
Dodanie toohello dostarczane przez system Obsługa utraconych komunikatów funkcji aplikacje mogą używać wiadomości powitania od DLQ tooexplicitly Odrzuć nie do przyjęcia. Może to obejmować wiadomości, które nie mogą być przetwarzane prawidłowo powodu sortowania tooany problem systemowy, komunikatów zawierających nieprawidłowo sformułowany ładunek lub wiadomości, które niepowodzenia uwierzytelniania, gdy jest używany schemat niektórych zabezpieczenia na poziomie komunikatu.

## <a name="dead-lettering-in-forwardto-or-sendvia-scenarios"></a>Obsługa utraconych komunikatów w scenariuszach ForwardTo lub SendVia

Wiadomości zostaną wysłane toohello transfer kolejkę z utraconymi komunikatami w obszarze hello następujące warunki:

- Komunikat przechodzi przez więcej niż 3 kolejki i tematy, które są [połączonych ze sobą](service-bus-auto-forwarding.md).
- Kolejka docelowa Hello lub temat zostało wyłączone lub usunięte.
- kolejki docelowej Hello lub temat przekracza rozmiar maksymalny jednostki hello.

tooretrieve te komunikaty lettered wiadomości, można utworzyć odbiornika za pomocą hello [FormatTransferDeadletterPath](/dotnet/api/microsoft.servicebus.messaging.queueclient#Microsoft_ServiceBus_Messaging_QueueClient_FormatTransferDeadLetterPath_System_String_) narzędzie metody.

## <a name="example"></a>Przykład
Witaj następującego fragmentu kodu tworzy odbiorcy wiadomości. W hello pętlę do kolejki głównej hello odbierania, hello kod pobiera wiadomość hello [Receive(TimeSpan.Zero)](/dotnet/api/microsoft.servicebus.messaging.messagereceiver#Microsoft_ServiceBus_Messaging_MessageReceiver_Receive_System_TimeSpan_), z pytaniem, zwracany tooinstantly brokera hello wszystkie dostępne wiadomości lub tooreturn z żadnego wyniku. Jeśli kod hello odbiera wiadomości, jego natychmiast odstępuje, która zwiększa hello `DeliveryCount`. Po hello system przeniesie toohello wiadomość hello DLQ, kolejki głównej hello jest pusty i hello wyjścia z pętli, jako [metody ReceiveAsync](/dotnet/api/microsoft.servicebus.messaging.messagereceiver#Microsoft_ServiceBus_Messaging_MessageReceiver_ReceiveAsync_System_TimeSpan_) zwraca **null**.

```csharp
var receiver = await receiverFactory.CreateMessageReceiverAsync(queueName, ReceiveMode.PeekLock);
while(true)
{
    var msg = await receiver.ReceiveAsync(TimeSpan.Zero);
    if (msg != null)
    {
        Console.WriteLine("Picked up message; DeliveryCount {0}", msg.DeliveryCount);
        await msg.AbandonAsync();
    }
    else
    {
        break;
    }
}
```

## <a name="next-steps"></a>Następne kroki
Zobacz następujące artykuły, aby uzyskać więcej informacji na temat kolejek usługi Service Bus hello:

* [Wprowadzenie do kolejek usługi Service Bus](service-bus-dotnet-get-started-with-queues.md)
* [Azure kolejki i usługi Service Bus w porównaniu kolejek](service-bus-azure-and-service-bus-queues-compared-contrasted.md)

