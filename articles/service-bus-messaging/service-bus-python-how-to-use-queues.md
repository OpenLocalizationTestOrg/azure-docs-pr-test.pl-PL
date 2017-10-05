---
title: "Jak używać kolejek usługi Azure Service Bus z Python | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak używać kolejek usługi Azure Service Bus w języku Python."
services: service-bus-messaging
documentationcenter: python
author: sethmanheim
manager: timlt
editor: 
ms.assetid: b95ee5cd-3b31-459c-a7f3-cf8bcf77858b
ms.service: service-bus-messaging
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: python
ms.topic: article
ms.date: 08/10/2017
ms.author: sethm;lmazuel
ms.openlocfilehash: e1e81ad1d7b4fe0e044917f090cac59dfd5b6332
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/18/2017
---
# <a name="how-to-use-service-bus-queues-with-python"></a><span data-ttu-id="002dd-103">Jak używać kolejek usługi Service Bus z języka Python</span><span class="sxs-lookup"><span data-stu-id="002dd-103">How to use Service Bus queues with Python</span></span>

[!INCLUDE [service-bus-selector-queues](../../includes/service-bus-selector-queues.md)]

<span data-ttu-id="002dd-104">W tym artykule opisano sposób używania kolejek usługi Service Bus.</span><span class="sxs-lookup"><span data-stu-id="002dd-104">This article describes how to use Service Bus queues.</span></span> <span data-ttu-id="002dd-105">Próbki są napisane w języku Python i użyj [pakiet języka Python Azure Service Bus][Python Azure Service Bus package].</span><span class="sxs-lookup"><span data-stu-id="002dd-105">The samples are written in Python and use the [Python Azure Service Bus package][Python Azure Service Bus package].</span></span> <span data-ttu-id="002dd-106">Omówione scenariusze obejmują **tworzenie kolejek, wysyłanie i odbieranie wiadomości**, i **usuwanie kolejek**.</span><span class="sxs-lookup"><span data-stu-id="002dd-106">The scenarios covered include **creating queues, sending and receiving messages**, and **deleting queues**.</span></span>

[!INCLUDE [howto-service-bus-queues](../../includes/howto-service-bus-queues.md)]

[!INCLUDE [service-bus-create-namespace-portal](../../includes/service-bus-create-namespace-portal.md)]

> [!NOTE]
> <span data-ttu-id="002dd-107">Aby zainstalować Python lub [pakiet języka Python Azure Service Bus][Python Azure Service Bus package], zobacz [Przewodnik instalacji języka Python](../python-how-to-install.md).</span><span class="sxs-lookup"><span data-stu-id="002dd-107">To install Python or the [Python Azure Service Bus package][Python Azure Service Bus package], see the [Python Installation Guide](../python-how-to-install.md).</span></span>
> 
> 

## <a name="create-a-queue"></a><span data-ttu-id="002dd-108">Tworzenie kolejki</span><span class="sxs-lookup"><span data-stu-id="002dd-108">Create a queue</span></span>
<span data-ttu-id="002dd-109">**ServiceBusService** obiektu umożliwia pracę z kolejki.</span><span class="sxs-lookup"><span data-stu-id="002dd-109">The **ServiceBusService** object enables you to work with queues.</span></span> <span data-ttu-id="002dd-110">Dodaj następujący kod u góry każdego pliku Python, w którym chcesz uzyskania programowego dostępu do usługi Service Bus:</span><span class="sxs-lookup"><span data-stu-id="002dd-110">Add the following code near the top of any Python file in which you wish to programmatically access Service Bus:</span></span>

```python
from azure.servicebus import ServiceBusService, Message, Queue
```

<span data-ttu-id="002dd-111">Poniższy kod tworzy **ServiceBusService** obiektu.</span><span class="sxs-lookup"><span data-stu-id="002dd-111">The following code creates a **ServiceBusService** object.</span></span> <span data-ttu-id="002dd-112">Zastąp `mynamespace`, `sharedaccesskeyname`, i `sharedaccesskey` nazwą przestrzeni nazw, nazwę klucza sygnatury dostępu Współdzielonego dostępu współdzielonego i wartość.</span><span class="sxs-lookup"><span data-stu-id="002dd-112">Replace `mynamespace`, `sharedaccesskeyname`, and `sharedaccesskey` with your namespace, shared access signature (SAS) key name, and value.</span></span>

```python
bus_service = ServiceBusService(
    service_namespace='mynamespace',
    shared_access_key_name='sharedaccesskeyname',
    shared_access_key_value='sharedaccesskey')
```

<span data-ttu-id="002dd-113">Wartości dla nazwy klucza sygnatury dostępu Współdzielonego i wartość znajduje się w [portalu Azure] [ Azure portal] informacje dotyczące połączenia, lub w programie Visual Studio **właściwości** okienku, wybierając usługę Przestrzeń nazw magistrali w Eksploratorze serwera (jak pokazano w poprzedniej sekcji).</span><span class="sxs-lookup"><span data-stu-id="002dd-113">The values for the SAS key name and value can be found in the [Azure portal][Azure portal] connection information, or in the Visual Studio **Properties** pane when selecting the Service Bus namespace in Server Explorer (as shown in the previous section).</span></span>

```python
bus_service.create_queue('taskqueue')
```

<span data-ttu-id="002dd-114">`create_queue` Metoda obsługuje również dodatkowe opcje, które umożliwiają zastąpić domyślne ustawienia kolejki, takie jak czas wygaśnięcia (TTL) lub maksymalny rozmiar kolejki wiadomości.</span><span class="sxs-lookup"><span data-stu-id="002dd-114">The `create_queue` method also supports additional options, which enable you to override default queue settings such as message time to live (TTL) or maximum queue size.</span></span> <span data-ttu-id="002dd-115">Poniższy przykład ustawia maksymalny rozmiar kolejki 5 GB i na 1 minutę wartość TTL:</span><span class="sxs-lookup"><span data-stu-id="002dd-115">The following example sets the maximum queue size to 5 GB, and the TTL value to 1 minute:</span></span>

```python
queue_options = Queue()
queue_options.max_size_in_megabytes = '5120'
queue_options.default_message_time_to_live = 'PT1M'

bus_service.create_queue('taskqueue', queue_options)
```

## <a name="send-messages-to-a-queue"></a><span data-ttu-id="002dd-116">Wysyłanie komunikatów do kolejki</span><span class="sxs-lookup"><span data-stu-id="002dd-116">Send messages to a queue</span></span>
<span data-ttu-id="002dd-117">Aby wysłać wiadomość do kolejki usługi Service Bus, wywołania aplikacji `send_queue_message` metoda **ServiceBusService** obiektu.</span><span class="sxs-lookup"><span data-stu-id="002dd-117">To send a message to a Service Bus queue, your application calls the `send_queue_message` method on the **ServiceBusService** object.</span></span>

<span data-ttu-id="002dd-118">W poniższym przykładzie pokazano sposób wysyłania wiadomości testowej do kolejki o nazwie `taskqueue` przy użyciu `send_queue_message`:</span><span class="sxs-lookup"><span data-stu-id="002dd-118">The following example demonstrates how to send a test message to the queue named `taskqueue` using `send_queue_message`:</span></span>

```python
msg = Message(b'Test Message')
bus_service.send_queue_message('taskqueue', msg)
```

<span data-ttu-id="002dd-119">Kolejki usługi Service Bus obsługują maksymalny rozmiar komunikatu 256 KB w [warstwie Standardowa](service-bus-premium-messaging.md) i 1 MB w [warstwie Premium](service-bus-premium-messaging.md).</span><span class="sxs-lookup"><span data-stu-id="002dd-119">Service Bus queues support a maximum message size of 256 KB in the [Standard tier](service-bus-premium-messaging.md) and 1 MB in the [Premium tier](service-bus-premium-messaging.md).</span></span> <span data-ttu-id="002dd-120">Nagłówek, który zawiera standardowe i niestandardowe właściwości aplikacji, może mieć maksymalny rozmiar 64 KB.</span><span class="sxs-lookup"><span data-stu-id="002dd-120">The header, which includes the standard and custom application properties, can have a maximum size of 64 KB.</span></span> <span data-ttu-id="002dd-121">Nie ma żadnego limitu liczby komunikatów w kolejce, ale jest ograniczenie całkowitego rozmiaru komunikatów przechowywanych przez kolejkę.</span><span class="sxs-lookup"><span data-stu-id="002dd-121">There is no limit on the number of messages held in a queue but there is a cap on the total size of the messages held by a queue.</span></span> <span data-ttu-id="002dd-122">Ten rozmiar kolejki jest definiowany w czasie tworzenia, z górnym limitem 5 GB.</span><span class="sxs-lookup"><span data-stu-id="002dd-122">This queue size is defined at creation time, with an upper limit of 5 GB.</span></span> <span data-ttu-id="002dd-123">Aby uzyskać więcej informacji na temat przydziałów, zobacz [przydziały usługi Service Bus][Service Bus quotas].</span><span class="sxs-lookup"><span data-stu-id="002dd-123">For more information about quotas, see [Service Bus quotas][Service Bus quotas].</span></span>

## <a name="receive-messages-from-a-queue"></a><span data-ttu-id="002dd-124">Odbieranie komunikatów z kolejki</span><span class="sxs-lookup"><span data-stu-id="002dd-124">Receive messages from a queue</span></span>
<span data-ttu-id="002dd-125">Odebrane komunikaty z kolejki przy użyciu `receive_queue_message` metoda **ServiceBusService** obiektu:</span><span class="sxs-lookup"><span data-stu-id="002dd-125">Messages are received from a queue using the `receive_queue_message` method on the **ServiceBusService** object:</span></span>

```python
msg = bus_service.receive_queue_message('taskqueue', peek_lock=False)
print(msg.body)
```

<span data-ttu-id="002dd-126">Wiadomości są usuwane z kolejki, ponieważ są one podczas odczytu parametru `peek_lock` ustawiono **False**.</span><span class="sxs-lookup"><span data-stu-id="002dd-126">Messages are deleted from the queue as they are read when the parameter `peek_lock` is set to **False**.</span></span> <span data-ttu-id="002dd-127">Można odczytać (peek) i Zablokuj wiadomość bez jego usuwania z kolejki przez ustawienie dla parametru `peek_lock` do **True**.</span><span class="sxs-lookup"><span data-stu-id="002dd-127">You can read (peek) and lock the message without deleting it from the queue by setting the parameter `peek_lock` to **True**.</span></span>

<span data-ttu-id="002dd-128">Zachowanie odczytywanie i usuwanie wiadomości w ramach operacji receive jest najprostszym modelem i działa najlepiej w scenariuszach, w których aplikacja może tolerować nieprzetworzenie komunikatu w razie awarii.</span><span class="sxs-lookup"><span data-stu-id="002dd-128">The behavior of reading and deleting the message as part of the receive operation is the simplest model, and works best for scenarios in which an application can tolerate not processing a message in the event of a failure.</span></span> <span data-ttu-id="002dd-129">Aby to zrozumieć, rozważmy scenariusz, w którym konsument wystawia żądanie odbioru, a następnie ulega awarii przed jego przetworzeniem.</span><span class="sxs-lookup"><span data-stu-id="002dd-129">To understand this, consider a scenario in which the consumer issues the receive request and then crashes before processing it.</span></span> <span data-ttu-id="002dd-130">Ponieważ Usługa Service Bus zostanie oznaczona komunikat jako wykorzystany, a następnie po uruchomieniu i rozpocznie korzystanie z komunikatów ponownie aplikacji, pominie utracony komunikat, który został wykorzystany przed awarią.</span><span class="sxs-lookup"><span data-stu-id="002dd-130">Because Service Bus will have marked the message as being consumed, then when the application restarts and begins consuming messages again, it will have missed the message that was consumed prior to the crash.</span></span>

<span data-ttu-id="002dd-131">Jeśli `peek_lock` ustawiono parametr **True**, odbieranie staje się operacją dwuetapowy, co umożliwia obsługę aplikacji, które nie tolerują brakujących komunikatów.</span><span class="sxs-lookup"><span data-stu-id="002dd-131">If the `peek_lock` parameter is set to **True**, the receive becomes a two stage operation, which makes it possible to support applications that cannot tolerate missing messages.</span></span> <span data-ttu-id="002dd-132">Gdy usługa Service Bus odbiera żądanie, znajduje następny komunikat do wykorzystania, blokuje go w celu uniemożliwienia innym klientom odebrania go i zwraca go do aplikacji.</span><span class="sxs-lookup"><span data-stu-id="002dd-132">When Service Bus receives a request, it finds the next message to be consumed, locks it to prevent other consumers receiving it, and then returns it to the application.</span></span> <span data-ttu-id="002dd-133">Kiedy aplikacja zakończy przetwarzanie komunikatu (lub niezawodnie zapisze go w celu przyszłego przetwarzania), wykonuje drugi etap procesu odbierania przez wywołanie metody **usunąć** metoda **komunikat** obiekt.</span><span class="sxs-lookup"><span data-stu-id="002dd-133">After the application finishes processing the message (or stores it reliably for future processing), it completes the second stage of the receive process by calling the **delete** method on the **Message** object.</span></span> <span data-ttu-id="002dd-134">**Usunąć** metoda będzie oznaczyć komunikat jako wykorzystany i usunąć go z kolejki.</span><span class="sxs-lookup"><span data-stu-id="002dd-134">The **delete** method will mark the message as being consumed and remove it from the queue.</span></span>

```python
msg = bus_service.receive_queue_message('taskqueue', peek_lock=True)
print(msg.body)

msg.delete()
```

## <a name="how-to-handle-application-crashes-and-unreadable-messages"></a><span data-ttu-id="002dd-135">Sposób obsługi awarii aplikacji i komunikatów niemożliwych do odczytania</span><span class="sxs-lookup"><span data-stu-id="002dd-135">How to handle application crashes and unreadable messages</span></span>
<span data-ttu-id="002dd-136">Usługa Service Bus zapewnia funkcję ułatwiającą bezpieczne odzyskiwanie w razie błędów w aplikacji lub trudności z przetwarzaniem komunikatu.</span><span class="sxs-lookup"><span data-stu-id="002dd-136">Service Bus provides functionality to help you gracefully recover from errors in your application or difficulties processing a message.</span></span> <span data-ttu-id="002dd-137">Jeśli aplikacja odbiorcy nie może przetworzyć komunikatu z jakiegoś powodu, wówczas może wywołać **odblokować** metoda **komunikat** obiektu.</span><span class="sxs-lookup"><span data-stu-id="002dd-137">If a receiver application is unable to process the message for some reason, then it can call the **unlock** method on the **Message** object.</span></span> <span data-ttu-id="002dd-138">Spowoduje to odblokowanie komunikatu w kolejce i udostępnienie go do ponownego odbioru, przez tę samą lub inną odbierającą aplikację usługę Service Bus.</span><span class="sxs-lookup"><span data-stu-id="002dd-138">This will cause Service Bus to unlock the message within the queue and make it available to be received again, either by the same consuming application or by another consuming application.</span></span>

<span data-ttu-id="002dd-139">Istnieje również limit czasu skojarzony z komunikatem zablokowanym w kolejce i jeśli aplikacja nie może przetworzyć komunikatu przed przekroczenie limitu czasu blokady wygaśnięcia (np. Jeśli wystąpiła awaria aplikacji), Usługa Service Bus zostanie automatycznie odblokowanie komunikatu i stał się dostępny do ponownego odbioru.</span><span class="sxs-lookup"><span data-stu-id="002dd-139">There is also a timeout associated with a message locked within the queue, and if the application fails to process the message before the lock timeout expires (e.g., if the application crashes), then Service Bus will unlock the message automatically and make it available to be received again.</span></span>

<span data-ttu-id="002dd-140">W przypadku, gdy aplikacja przestaje działać po przetworzeniu komunikatu, ale przed wysłaniem **usunąć** metoda jest wywoływana, a następnie komunikat zostanie dostarczony do aplikacji po jej ponownym uruchomieniu.</span><span class="sxs-lookup"><span data-stu-id="002dd-140">In the event that the application crashes after processing the message but before the **delete** method is called, then the message will be redelivered to the application when it restarts.</span></span> <span data-ttu-id="002dd-141">Jest to często nazywane **przetwarzaniem co najmniej raz**, oznacza to, że każdy komunikat będzie przetwarzany co najmniej raz, ale w pewnych sytuacjach ten sam komunikat może być dostarczony ponownie.</span><span class="sxs-lookup"><span data-stu-id="002dd-141">This is often called **At Least Once Processing**, that is, each message will be processed at least once but in certain situations the same message may be redelivered.</span></span> <span data-ttu-id="002dd-142">Jeśli scenariusz nie toleruje dwukrotnego przetwarzania, deweloperzy aplikacji powinni dodać dodatkową logikę do swojej aplikacji w celu obsługi dwukrotnego dostarczania komunikatów.</span><span class="sxs-lookup"><span data-stu-id="002dd-142">If the scenario cannot tolerate duplicate processing, then application developers should add additional logic to their application to handle duplicate message delivery.</span></span> <span data-ttu-id="002dd-143">Jest to często osiągane przy użyciu **MessageId** właściwości wiadomości, która pozostaje stała między kolejnymi próbami dostarczenia.</span><span class="sxs-lookup"><span data-stu-id="002dd-143">This is often achieved using the **MessageId** property of the message, which will remain constant across delivery attempts.</span></span>

## <a name="next-steps"></a><span data-ttu-id="002dd-144">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="002dd-144">Next steps</span></span>
<span data-ttu-id="002dd-145">Teraz, kiedy znasz już podstawy kolejek usługi Service Bus, zobacz następujące artykuły, aby dowiedzieć się więcej.</span><span class="sxs-lookup"><span data-stu-id="002dd-145">Now that you have learned the basics of Service Bus queues, see these articles to learn more.</span></span>

* <span data-ttu-id="002dd-146">[Kolejki, tematy i subskrypcje][Queues, topics, and subscriptions]</span><span class="sxs-lookup"><span data-stu-id="002dd-146">[Queues, topics, and subscriptions][Queues, topics, and subscriptions]</span></span>

[Azure portal]: https://portal.azure.com
[Python Azure Service Bus package]: https://pypi.python.org/pypi/azure-servicebus  
[Queues, topics, and subscriptions]: service-bus-queues-topics-subscriptions.md
[Service Bus quotas]: service-bus-quotas.md

