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
# <a name="overview-of-service-bus-transaction-processing"></a><span data-ttu-id="2c631-103">Omówienie przetwarzanie transakcji usługi Service Bus</span><span class="sxs-lookup"><span data-stu-id="2c631-103">Overview of Service Bus transaction processing</span></span>
<span data-ttu-id="2c631-104">W tym artykule omówiono możliwości transakcji hello Azure Service Bus.</span><span class="sxs-lookup"><span data-stu-id="2c631-104">This article discusses hello transaction capabilities of Azure Service Bus.</span></span> <span data-ttu-id="2c631-105">Większość dyskusji hello jest zilustrowane hello [Atomic transakcji z usługi Service Bus próbki](https://github.com/Azure/azure-service-bus/tree/master/samples/DotNet/Microsoft.ServiceBus.Messaging/AtomicTransactions).</span><span class="sxs-lookup"><span data-stu-id="2c631-105">Much of hello discussion is illustrated by hello [Atomic Transactions with Service Bus sample](https://github.com/Azure/azure-service-bus/tree/master/samples/DotNet/Microsoft.ServiceBus.Messaging/AtomicTransactions).</span></span> <span data-ttu-id="2c631-106">Ten artykuł zawiera omówienie tooan ograniczone przetwarzanie transakcji i hello *wyśle* funkcji w usłudze Service Bus, podczas przykład Atomic transakcji hello jest bardziej rozbudowaną i bardziej złożonej w zakresie.</span><span class="sxs-lookup"><span data-stu-id="2c631-106">This article is limited tooan overview of transaction processing and hello *send via* feature in Service Bus, while hello Atomic Transactions sample is broader and more complex in scope.</span></span>

## <a name="transactions-in-service-bus"></a><span data-ttu-id="2c631-107">Transakcje w usłudze Service Bus</span><span class="sxs-lookup"><span data-stu-id="2c631-107">Transactions in Service Bus</span></span>
<span data-ttu-id="2c631-108">A [transakcji](https://github.com/Azure/azure-service-bus/tree/master/samples/DotNet/Microsoft.ServiceBus.Messaging/AtomicTransactions#what-are-transactions) grupowanie dwóch lub więcej operacji w *zakresu wykonywania*.</span><span class="sxs-lookup"><span data-stu-id="2c631-108">A [transaction](https://github.com/Azure/azure-service-bus/tree/master/samples/DotNet/Microsoft.ServiceBus.Messaging/AtomicTransactions#what-are-transactions) groups two or more operations together into an *execution scope*.</span></span> <span data-ttu-id="2c631-109">Natury takich transakcji musi upewnij się, że wszystkie operacje należących do danej grupy działań tooa powiedzie się lub wspólnie zakończyć się niepowodzeniem.</span><span class="sxs-lookup"><span data-stu-id="2c631-109">By nature, such a transaction must ensure that all operations belonging tooa given group of operations either succeed or fail jointly.</span></span> <span data-ttu-id="2c631-110">W związku z tym transakcji pełnić jedną jednostkę, która jest często tooas określonego *niepodzielność*.</span><span class="sxs-lookup"><span data-stu-id="2c631-110">In this respect transactions act as one unit, which is often referred tooas *atomicity*.</span></span> 

<span data-ttu-id="2c631-111">Usługa Service Bus jest brokera wiadomości transakcyjnych i zapewnia integralność transakcyjne dla wszystkich operacji wewnętrznych przed jego magazyny wiadomości.</span><span class="sxs-lookup"><span data-stu-id="2c631-111">Service Bus is a transactional message broker and ensures transactional integrity for all internal operations against its message stores.</span></span> <span data-ttu-id="2c631-112">Wszystkie operacje transferu komunikatów wewnątrz usługi Service Bus, takich jak przenoszenie wiadomości tooa [kolejki utraconych wiadomości](service-bus-dead-letter-queues.md) lub [automatyczne przekazywanie](service-bus-auto-forwarding.md) komunikatów między jednostkami, są transakcyjnych.</span><span class="sxs-lookup"><span data-stu-id="2c631-112">All transfers of messages inside of Service Bus, such as moving messages tooa [dead-letter queue](service-bus-dead-letter-queues.md) or [automatic forwarding](service-bus-auto-forwarding.md) of messages between entities, are transactional.</span></span> <span data-ttu-id="2c631-113">Tak Jeśli usługi Service Bus akceptuje wiadomości, już został przechowywane i z liczbą sekwencji.</span><span class="sxs-lookup"><span data-stu-id="2c631-113">As such, if Service Bus accepts a message, it has already been stored and labeled with a sequence number.</span></span> <span data-ttu-id="2c631-114">Następnie wszelkich transferów komunikatów w ramach usługi Service Bus są skoordynowanej operacji w ramach jednostkami i nie będzie prowadzić tooloss (źródła zakończy się pomyślnie i docelowa kończy się niepowodzeniem) lub tooduplication (źródłowego nie powiedzie się i docelowego zakończy się powodzeniem) wiadomości powitania.</span><span class="sxs-lookup"><span data-stu-id="2c631-114">From then on, any message transfers within Service Bus are coordinated operations across entities, and will neither lead tooloss (source succeeds and target fails) or tooduplication (source fails and target succeeds) of hello message.</span></span>

<span data-ttu-id="2c631-115">Usługa Service Bus obsługuje operacje grupowania względem jednej jednostki obsługi komunikatów (kolejki, tematu, subskrypcji) w zakresie hello transakcji.</span><span class="sxs-lookup"><span data-stu-id="2c631-115">Service Bus supports grouping operations against a single messaging entity (queue, topic, subscription) within hello scope of a transaction.</span></span> <span data-ttu-id="2c631-116">Na przykład kilka kolejki tooone wiadomości z może wysyłać w zakresie transakcji, a wiadomości powitania będą tylko zatwierdzone toohello kolejki dziennika po pomyślnym zakończeniu hello transakcji.</span><span class="sxs-lookup"><span data-stu-id="2c631-116">For example, you can send several messages tooone queue from within a transaction scope, and hello messages will only be committed toohello queue's log when hello transaction successfully completes.</span></span>

## <a name="operations-within-a-transaction-scope"></a><span data-ttu-id="2c631-117">Operacje w zakresie transakcji</span><span class="sxs-lookup"><span data-stu-id="2c631-117">Operations within a transaction scope</span></span>
<span data-ttu-id="2c631-118">dostępne są następujące operacje Hello, które mogą być wykonywane w zakresie transakcji:</span><span class="sxs-lookup"><span data-stu-id="2c631-118">hello operations that can be performed within a transaction scope are as follows:</span></span>

* <span data-ttu-id="2c631-119">**[QueueClient](/dotnet/api/microsoft.servicebus.messaging.queueclient), [MessageSender](/dotnet/api/microsoft.servicebus.messaging.messagesender), [TopicClient](/dotnet/api/microsoft.servicebus.messaging.topicclient)**: wysyłanie SendAsync, SendBatch, SendBatchAsync</span><span class="sxs-lookup"><span data-stu-id="2c631-119">**[QueueClient](/dotnet/api/microsoft.servicebus.messaging.queueclient), [MessageSender](/dotnet/api/microsoft.servicebus.messaging.messagesender), [TopicClient](/dotnet/api/microsoft.servicebus.messaging.topicclient)**: Send, SendAsync, SendBatch, SendBatchAsync</span></span> 
* <span data-ttu-id="2c631-120">**[BrokeredMessage](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage)**: zakończeniu CompleteAsync, porzucenia, AbandonAsync, utraconych wiadomości, DeadletterAsync, wstrzymuje, DeferAsync, RenewLock, RenewLockAsync</span><span class="sxs-lookup"><span data-stu-id="2c631-120">**[BrokeredMessage](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage)**: Complete, CompleteAsync, Abandon, AbandonAsync, Deadletter, DeadletterAsync, Defer, DeferAsync, RenewLock, RenewLockAsync</span></span> 

<span data-ttu-id="2c631-121">Odbieranie operacje nie są uwzględnione, ponieważ zakłada się, że aplikacja hello nabywa komunikaty przy użyciu hello [ReceiveMode.PeekLock](/dotnet/api/microsoft.servicebus.messaging.receivemode) tryb, w niektórych pętlę odbierania lub [OnMessage](/dotnet/api/microsoft.servicebus.messaging.messagereceiver#Microsoft_ServiceBus_Messaging_MessageReceiver_OnMessage_System_Action_Microsoft_ServiceBus_Messaging_BrokeredMessage__Microsoft_ServiceBus_Messaging_OnMessageOptions_) wywołania zwrotnego, i zakres tylko następnie otwiera transakcji wiadomość hello przetwarzania.</span><span class="sxs-lookup"><span data-stu-id="2c631-121">Receive operations are not included, because it is assumed that hello application acquires messages using hello [ReceiveMode.PeekLock](/dotnet/api/microsoft.servicebus.messaging.receivemode) mode, inside some receive loop or with an [OnMessage](/dotnet/api/microsoft.servicebus.messaging.messagereceiver#Microsoft_ServiceBus_Messaging_MessageReceiver_OnMessage_System_Action_Microsoft_ServiceBus_Messaging_BrokeredMessage__Microsoft_ServiceBus_Messaging_OnMessageOptions_) callback, and only then opens a transaction scope for processing hello message.</span></span>

<span data-ttu-id="2c631-122">Hello dyspozycji wiadomość hello (zakończeniu porzucenia, wiadomości utraconych odroczyć) następnie odbywa się w zakresie hello, w zależności od, hello ogólną wyniku hello transakcji.</span><span class="sxs-lookup"><span data-stu-id="2c631-122">hello disposition of hello message (complete, abandon, dead-letter, defer) then occurs within hello scope of, and dependent on, hello overall outcome of hello transaction.</span></span>

## <a name="transfers-and-send-via"></a><span data-ttu-id="2c631-123">Transfery i "Wyślij za pośrednictwem"</span><span class="sxs-lookup"><span data-stu-id="2c631-123">Transfers and "send via"</span></span>
<span data-ttu-id="2c631-124">tooenable transakcyjnych przekazania danych z kolejki tooa procesora, a następnie tooanother kolejki, Usługa Service Bus obsługuje *transferów*.</span><span class="sxs-lookup"><span data-stu-id="2c631-124">tooenable transactional handover of data from a queue tooa processor, and then tooanother queue, Service Bus supports *transfers*.</span></span> <span data-ttu-id="2c631-125">W operacji przeniesienia nadawcy najpierw wysyła tooa komunikat "kolejce transferu" i kolejce transferu hello natychmiast przenosi toohello wiadomość hello mającą przy użyciu hello sam niezawodne transfer implementację, która opiera się możliwość automatycznego przekazywania hello kolejki docelowej na serwerze.</span><span class="sxs-lookup"><span data-stu-id="2c631-125">In a transfer operation, a sender first sends a message tooa "transfer queue" and hello transfer queue immediately moves hello message toohello intended destination queue using hello same robust transfer implementation that hello auto-forward capability relies on.</span></span> <span data-ttu-id="2c631-126">wiadomości powitania nigdy nie jest dziennika kolejce transferu toohello zadeklarowanej w taki sposób, że stają się one widoczne dla użytkowników w kolejce transferu hello.</span><span class="sxs-lookup"><span data-stu-id="2c631-126">hello message is never committed toohello transfer queue's log in a way that it becomes visible for hello transfer queue's consumers.</span></span>

<span data-ttu-id="2c631-127">power Hello tej możliwości transakcyjnych stała się oczywista, gdy samej kolejki transfer hello jest źródłem hello komunikaty wejściowe hello nadawcy.</span><span class="sxs-lookup"><span data-stu-id="2c631-127">hello power of this transactional capability becomes apparent when hello transfer queue itself is hello source of hello sender's input messages.</span></span> <span data-ttu-id="2c631-128">Innymi słowy, usługi Service Bus można przetransferować kolejki docelowej toohello wiadomość hello "przez" hello kolejce transferu, podczas wykonywania pełnego (lub mają być odroczone, lub utraconych) operacji na powitania komunikat wejściowy wszystko w jednym niepodzielną operację.</span><span class="sxs-lookup"><span data-stu-id="2c631-128">In other words, Service Bus can transfer hello message toohello destination queue "via" hello transfer queue, while performing a complete (or defer, or dead-letter) operation on hello input message, all in one atomic operation.</span></span> 

### <a name="see-it-in-code"></a><span data-ttu-id="2c631-129">Zobacz go w kodzie</span><span class="sxs-lookup"><span data-stu-id="2c631-129">See it in code</span></span>
<span data-ttu-id="2c631-130">tooset się przeniesienie, możesz utworzyć przeznaczonego dla kolejki docelowej hello za pośrednictwem kolejki transfer hello nadawcy wiadomości.</span><span class="sxs-lookup"><span data-stu-id="2c631-130">tooset up such transfers, you create a message sender that targets hello destination queue via hello transfer queue.</span></span> <span data-ttu-id="2c631-131">Konieczne będzie również odbiornik, który pobiera komunikaty z tej samej kolejki.</span><span class="sxs-lookup"><span data-stu-id="2c631-131">You will also have a receiver that pulls messages from that same queue.</span></span> <span data-ttu-id="2c631-132">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="2c631-132">For example:</span></span>

```csharp
var sender = this.messagingFactory.CreateMessageSender(destinationQueue, myQueueName);
var receiver = this.messagingFactory.CreateMessageReceiver(myQueueName);
```

<span data-ttu-id="2c631-133">Następnie proste transakcji korzysta z tych elementów, jak hello poniższy przykład:</span><span class="sxs-lookup"><span data-stu-id="2c631-133">A simple transaction then uses these elements, as in hello following example:</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="2c631-134">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="2c631-134">Next steps</span></span>

<span data-ttu-id="2c631-135">Zobacz następujące artykuły, aby uzyskać więcej informacji na temat kolejek usługi Service Bus hello:</span><span class="sxs-lookup"><span data-stu-id="2c631-135">See hello following articles for more information about Service Bus queues:</span></span>

* [<span data-ttu-id="2c631-136">Tworzenie łańcuchów jednostek usługi Service Bus z automatyczne przekazywanie</span><span class="sxs-lookup"><span data-stu-id="2c631-136">Chaining Service Bus entities with auto-forwarding</span></span>](service-bus-auto-forwarding.md)
* [<span data-ttu-id="2c631-137">Przykładowe do przodu automatycznie</span><span class="sxs-lookup"><span data-stu-id="2c631-137">Auto-forward sample</span></span>](https://github.com/Azure/azure-service-bus/tree/master/samples/DotNet/Microsoft.ServiceBus.Messaging/AutoForward)
* [<span data-ttu-id="2c631-138">Niepodzielne transakcji z usługi Service Bus próbki</span><span class="sxs-lookup"><span data-stu-id="2c631-138">Atomic Transactions with Service Bus sample</span></span>](https://github.com/Azure/azure-service-bus/tree/master/samples/DotNet/Microsoft.ServiceBus.Messaging/AtomicTransactions)
* [<span data-ttu-id="2c631-139">Azure kolejki i usługi Service Bus w porównaniu kolejek</span><span class="sxs-lookup"><span data-stu-id="2c631-139">Azure Queues and Service Bus queues compared</span></span>](service-bus-azure-and-service-bus-queues-compared-contrasted.md)
* [<span data-ttu-id="2c631-140">Jak toouse kolejek usługi Service Bus</span><span class="sxs-lookup"><span data-stu-id="2c631-140">How toouse Service Bus queues</span></span>](service-bus-dotnet-get-started-with-queues.md)

