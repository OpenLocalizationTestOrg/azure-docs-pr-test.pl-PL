---
title: "przekazywanie aaaAuto jednostki do obsługi komunikatów usługi Azure Service Bus | Dokumentacja firmy Microsoft"
description: "Jak toochain usługi Service Bus kolejki lub kolejka tooanother subskrypcji lub temat."
services: service-bus-messaging
documentationcenter: na
author: sethmanheim
manager: timlt
editor: 
ms.assetid: f7060778-3421-402c-97c7-735dbf6a61e8
ms.service: service-bus-messaging
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/07/2017
ms.author: sethm
ms.openlocfilehash: af18273e4e2f81c5363eb830c7decf313afd8307
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="chaining-service-bus-entities-with-auto-forwarding"></a><span data-ttu-id="f19e0-103">Tworzenie łańcuchów jednostek usługi Service Bus z automatyczne przekazywanie</span><span class="sxs-lookup"><span data-stu-id="f19e0-103">Chaining Service Bus entities with auto-forwarding</span></span>

<span data-ttu-id="f19e0-104">Witaj usługi Service Bus *automatyczne przekazywanie* pozwala toochain kolejkę lub kolejki tooanother subskrypcji lub temat, który jest częścią hello tego samego obszaru nazw.</span><span class="sxs-lookup"><span data-stu-id="f19e0-104">hello Service Bus *auto-forwarding* feature enables you toochain a queue or subscription tooanother queue or topic that is part of hello same namespace.</span></span> <span data-ttu-id="f19e0-105">Gdy włączone jest automatyczne przekazywanie, usługi Service Bus automatycznie usuwa wiadomości, które są umieszczane w pierwszej kolejki hello lub subskrypcji (źródło) i umieszcza je w hello drugi kolejka lub temat (docelowy).</span><span class="sxs-lookup"><span data-stu-id="f19e0-105">When auto-forwarding is enabled, Service Bus automatically removes messages that are placed in hello first queue or subscription (source) and puts them in hello second queue or topic (destination).</span></span> <span data-ttu-id="f19e0-106">Należy pamiętać, że nadal możliwe toosend do jednostki docelowej toohello komunikat bezpośrednio.</span><span class="sxs-lookup"><span data-stu-id="f19e0-106">Note that it is still possible toosend a message toohello destination entity directly.</span></span> <span data-ttu-id="f19e0-107">Ponadto nie jest możliwe toochain podkolejki, takich jak kolejki utraconych wiadomości, tooanother kolejka lub temat.</span><span class="sxs-lookup"><span data-stu-id="f19e0-107">Also, it is not possible toochain a subqueue, such as a deadletter queue, tooanother queue or topic.</span></span>

## <a name="using-auto-forwarding"></a><span data-ttu-id="f19e0-108">Przy użyciu automatycznego przekazywania</span><span class="sxs-lookup"><span data-stu-id="f19e0-108">Using auto-forwarding</span></span>
<span data-ttu-id="f19e0-109">Możesz włączyć automatyczne przekazywanie przez ustawienie hello [QueueDescription.ForwardTo] [ QueueDescription.ForwardTo] lub [SubscriptionDescription.ForwardTo] [ SubscriptionDescription.ForwardTo] właściwości na powitania [QueueDescription] [ QueueDescription] lub [SubscriptionDescription] [ SubscriptionDescription] obiekty źródła hello, tak jak hello Poniższy przykład.</span><span class="sxs-lookup"><span data-stu-id="f19e0-109">You can enable auto-forwarding by setting hello [QueueDescription.ForwardTo][QueueDescription.ForwardTo] or [SubscriptionDescription.ForwardTo][SubscriptionDescription.ForwardTo] properties on hello [QueueDescription][QueueDescription] or [SubscriptionDescription][SubscriptionDescription] objects for hello source, as in hello following example.</span></span>

```csharp
SubscriptionDescription srcSubscription = new SubscriptionDescription (srcTopic, srcSubscriptionName);
srcSubscription.ForwardTo = destTopic;
namespaceManager.CreateSubscription(srcSubscription));
```

<span data-ttu-id="f19e0-110">Witaj jednostki docelowej musi istnieć w czasie hello jednostki źródłowej hello jest tworzony.</span><span class="sxs-lookup"><span data-stu-id="f19e0-110">hello destination entity must exist at hello time hello source entity is created.</span></span> <span data-ttu-id="f19e0-111">Jeśli hello jednostki docelowej nie istnieje, usługi Service Bus zwraca wyjątek podczas zadawane toocreate hello jednostki źródłowej.</span><span class="sxs-lookup"><span data-stu-id="f19e0-111">If hello destination entity does not exist, Service Bus returns an exception when asked toocreate hello source entity.</span></span>

<span data-ttu-id="f19e0-112">Umożliwia automatyczne przekazywanie tooscale limit poszczególne tematy.</span><span class="sxs-lookup"><span data-stu-id="f19e0-112">You can use auto-forwarding tooscale out an individual topic.</span></span> <span data-ttu-id="f19e0-113">Usługi Service Bus limity hello [liczba subskrypcji danego tematu](service-bus-quotas.md) too2, 000.</span><span class="sxs-lookup"><span data-stu-id="f19e0-113">Service Bus limits hello [number of subscriptions on a given topic](service-bus-quotas.md) too2,000.</span></span> <span data-ttu-id="f19e0-114">Może obsłużyć dodatkowe subskrypcji, tworząc tematy drugiego poziomu.</span><span class="sxs-lookup"><span data-stu-id="f19e0-114">You can accommodate additional subscriptions by creating second-level topics.</span></span> <span data-ttu-id="f19e0-115">Należy pamiętać, że nawet jeśli nie są powiązane przez hello usługi Service Bus ograniczenia hello liczbę subskrypcji, dodawanie drugiego poziomu tematów można zwiększyć hello ogólną przepustowość tematu.</span><span class="sxs-lookup"><span data-stu-id="f19e0-115">Note that even if you are not bound by hello Service Bus limitation on hello number of subscriptions, adding a second level of topics can improve hello overall throughput of your topic.</span></span>

![Automatyczne przekazywanie scenariusza][0]

<span data-ttu-id="f19e0-117">Umożliwia także automatyczne przekazywanie nadawcy wiadomości toodecouple z odbiorcy.</span><span class="sxs-lookup"><span data-stu-id="f19e0-117">You can also use auto-forwarding toodecouple message senders from receivers.</span></span> <span data-ttu-id="f19e0-118">Rozważmy na przykład system ERP, który składa się z trzech modułów: kolejność przetwarzania, Zarządzanie zapasami i zarządzania relacjami z klientami.</span><span class="sxs-lookup"><span data-stu-id="f19e0-118">For example, consider an ERP system that consists of three modules: order processing, inventory management, and customer relations management.</span></span> <span data-ttu-id="f19e0-119">Każdy z tych modułów generuje wiadomości, które są umieszczonych w kolejce do odpowiedniego tematu.</span><span class="sxs-lookup"><span data-stu-id="f19e0-119">Each of these modules generates messages that are enqueued into a corresponding topic.</span></span> <span data-ttu-id="f19e0-120">Alicja i Robert są przedstawicieli handlowych, którzy chcą wszystkie komunikaty dotyczące tootheir klientów.</span><span class="sxs-lookup"><span data-stu-id="f19e0-120">Alice and Bob are sales representatives that are interested in all messages that relate tootheir customers.</span></span> <span data-ttu-id="f19e0-121">tooreceive tych wiadomości, Alicja, jak i Robert Utwórz kolejkę osobistych i subskrypcji na każdym hello ERP tematów, które automatycznie przekazywać wszystkie kolejki tootheir wiadomości.</span><span class="sxs-lookup"><span data-stu-id="f19e0-121">tooreceive those messages, Alice and Bob each create a personal queue and a subscription on each of hello ERP topics that automatically forward all messages tootheir queue.</span></span>

![Automatyczne przekazywanie scenariusza][1]

<span data-ttu-id="f19e0-123">Jeśli Alicja odbędzie się na urlop, swoje osobiste kolejki, a nie hello ERP tematu, wypełnia.</span><span class="sxs-lookup"><span data-stu-id="f19e0-123">If Alice goes on vacation, her personal queue, rather than hello ERP topic, fills up.</span></span> <span data-ttu-id="f19e0-124">W tym scenariuszu ponieważ przedstawiciel handlowy nie odebrał żadnych wiadomości Brak tematów ERP hello kiedykolwiek łączność przydziału.</span><span class="sxs-lookup"><span data-stu-id="f19e0-124">In this scenario, because a sales representative has not received any messages, none of hello ERP topics ever reach quota.</span></span>

## <a name="auto-forwarding-considerations"></a><span data-ttu-id="f19e0-125">Zagadnienia dotyczące automatyczne przekazywanie</span><span class="sxs-lookup"><span data-stu-id="f19e0-125">Auto-forwarding considerations</span></span>

<span data-ttu-id="f19e0-126">Jeśli jednostki docelowej hello akumuluje zbyt wiele komunikatów i przekracza przydział hello lub hello jednostki docelowej jest wyłączona, jednostki źródłowej hello dodaje tooits wiadomości powitania [kolejki utraconych wiadomości](service-bus-dead-letter-queues.md) do momentu w docelowym hello jest miejsca lub hello jednostki zostanie ponownie włączony.</span><span class="sxs-lookup"><span data-stu-id="f19e0-126">If hello destination entity accumulates too many messages and exceeds hello quota, or hello destination entity is disabled, hello source entity adds hello messages tooits [dead-letter queue](service-bus-dead-letter-queues.md) until there is space in hello destination (or hello entity is re-enabled).</span></span> <span data-ttu-id="f19e0-127">Te komunikaty będą nadal toolive kolejki utraconych wiadomości powitania, musisz jawnie odbierania i ich przetwarzania z kolejki utraconych wiadomości powitania.</span><span class="sxs-lookup"><span data-stu-id="f19e0-127">Those messages will continue toolive in hello dead-letter queue, so you must explicitly receive and process them from hello dead-letter queue.</span></span>

<span data-ttu-id="f19e0-128">Podczas łączenia ze sobą tooobtain tematy złożonego temat o wielu subskrypcji, zaleca się, że masz umiarkowanej liczbie subskrypcje tematu pierwszego stopnia hello i wiele subskrypcji na powitania tematy drugiego poziomu.</span><span class="sxs-lookup"><span data-stu-id="f19e0-128">When chaining together individual topics tooobtain a composite topic with many subscriptions, it is recommended that you have a moderate number of subscriptions on hello first-level topic and many subscriptions on hello second-level topics.</span></span> <span data-ttu-id="f19e0-129">Na przykład pierwszego stopnia tematu z subskrypcjami 20, każdego z nich łańcuchowej tooa drugiego poziomu tematu z subskrypcjami 200 umożliwia wyższej przepustowości niż tematu pierwszego stopnia z subskrypcjami 200 każdego łańcuchowej tooa drugiego poziomu tematu z subskrypcjami 20 .</span><span class="sxs-lookup"><span data-stu-id="f19e0-129">For example, a first-level topic with 20 subscriptions, each of them chained tooa second-level topic with 200 subscriptions, allows for higher throughput than a first-level topic with 200 subscriptions, each chained tooa second-level topic with 20 subscriptions.</span></span>

<span data-ttu-id="f19e0-130">Usługa Service Bus rachunków jedna operacja dla każdej przekazany dalej komunikat.</span><span class="sxs-lookup"><span data-stu-id="f19e0-130">Service Bus bills one operation for each forwarded message.</span></span> <span data-ttu-id="f19e0-131">Na przykład wysyłanie temat tooa wiadomość z subskrypcjami 20, każde z nich skonfigurowany komunikatów do przodu tooauto tooanother kolejka lub temat, jest użyta jako 21 operacje, jeśli wszystkie subskrypcje pierwszego stopnia otrzymać kopię wiadomości powitania.</span><span class="sxs-lookup"><span data-stu-id="f19e0-131">For example, sending a message tooa topic with 20 subscriptions, each of them configured tooauto-forward messages tooanother queue or topic, is billed as 21 operations if all first-level subscriptions receive a copy of hello message.</span></span>

<span data-ttu-id="f19e0-132">toocreate subskrypcji, która jest tooanother łańcuchowa kolejka lub temat hello twórca subskrypcji hello musi mieć **Zarządzaj** uprawnienia na powitania źródła i hello jednostki docelowej.</span><span class="sxs-lookup"><span data-stu-id="f19e0-132">toocreate a subscription that is chained tooanother queue or topic, hello creator of hello subscription must have **Manage** permissions on both hello source and hello destination entity.</span></span> <span data-ttu-id="f19e0-133">Wysyłanie wiadomości toohello źródła tematu wymaga tylko **wysyłania** uprawnienia na powitania źródła tematu.</span><span class="sxs-lookup"><span data-stu-id="f19e0-133">Sending messages toohello source topic only requires **Send** permissions on hello source topic.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f19e0-134">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="f19e0-134">Next steps</span></span>

<span data-ttu-id="f19e0-135">Szczegółowe informacje dotyczące automatycznego przekazywania zobacz następujące tematy dokumentacji hello:</span><span class="sxs-lookup"><span data-stu-id="f19e0-135">For detailed information about auto-forwarding, see hello following reference topics:</span></span>

* <span data-ttu-id="f19e0-136">[ForwardTo][QueueDescription.ForwardTo]</span><span class="sxs-lookup"><span data-stu-id="f19e0-136">[ForwardTo][QueueDescription.ForwardTo]</span></span>
* <span data-ttu-id="f19e0-137">[QueueDescription][QueueDescription]</span><span class="sxs-lookup"><span data-stu-id="f19e0-137">[QueueDescription][QueueDescription]</span></span>
* <span data-ttu-id="f19e0-138">[SubscriptionDescription][SubscriptionDescription]</span><span class="sxs-lookup"><span data-stu-id="f19e0-138">[SubscriptionDescription][SubscriptionDescription]</span></span>

<span data-ttu-id="f19e0-139">toolearn więcej informacji na temat ulepszenia wydajności usługi Service Bus, zobacz</span><span class="sxs-lookup"><span data-stu-id="f19e0-139">toolearn more about Service Bus performance improvements, see</span></span> 

* [<span data-ttu-id="f19e0-140">Najlepsze rozwiązania dotyczące poprawy wydajności przy użyciu usługi magistrali komunikatów</span><span class="sxs-lookup"><span data-stu-id="f19e0-140">Best Practices for performance improvements using Service Bus Messaging</span></span>](service-bus-performance-improvements.md)
* <span data-ttu-id="f19e0-141">[Partycjonowane jednostki do obsługi komunikatów][Partitioned messaging entities].</span><span class="sxs-lookup"><span data-stu-id="f19e0-141">[Partitioned messaging entities][Partitioned messaging entities].</span></span>

[QueueDescription.ForwardTo]: /dotnet/api/microsoft.servicebus.messaging.queuedescription.forwardto#Microsoft_ServiceBus_Messaging_QueueDescription_ForwardTo
[SubscriptionDescription.ForwardTo]: /dotnet/api/microsoft.servicebus.messaging.subscriptiondescription.forwardto#Microsoft_ServiceBus_Messaging_SubscriptionDescription_ForwardTo
[QueueDescription]: /dotnet/api/microsoft.servicebus.messaging.queuedescription
[SubscriptionDescription]: /dotnet/api/microsoft.servicebus.messaging.queuedescription
[0]: ./media/service-bus-auto-forwarding/IC628631.gif
[1]: ./media/service-bus-auto-forwarding/IC628632.gif
[Partitioned messaging entities]: service-bus-partitioning.md
