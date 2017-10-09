---
title: "kolejkuje toouse aaaHow Azure Service Bus z języka Python | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toouse Azure Service Bus kolejek w języku Python."
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
ms.openlocfilehash: bceb84d04ff3445c3087a9c246c583d6630f07af
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-service-bus-queues-with-python"></a><span data-ttu-id="cf8c8-103">Jak kolejki usługi Service Bus toouse języka Python</span><span class="sxs-lookup"><span data-stu-id="cf8c8-103">How toouse Service Bus queues with Python</span></span>

[!INCLUDE [service-bus-selector-queues](../../includes/service-bus-selector-queues.md)]

<span data-ttu-id="cf8c8-104">W tym artykule opisano sposób toouse kolejek usługi Service Bus.</span><span class="sxs-lookup"><span data-stu-id="cf8c8-104">This article describes how toouse Service Bus queues.</span></span> <span data-ttu-id="cf8c8-105">Witaj przykłady są napisane w języku Python i używają hello [pakiet języka Python Azure Service Bus][Python Azure Service Bus package].</span><span class="sxs-lookup"><span data-stu-id="cf8c8-105">hello samples are written in Python and use hello [Python Azure Service Bus package][Python Azure Service Bus package].</span></span> <span data-ttu-id="cf8c8-106">Witaj omówione scenariusze obejmują **tworzenie kolejek, wysyłanie i odbieranie wiadomości**, i **usuwanie kolejek**.</span><span class="sxs-lookup"><span data-stu-id="cf8c8-106">hello scenarios covered include **creating queues, sending and receiving messages**, and **deleting queues**.</span></span>

[!INCLUDE [howto-service-bus-queues](../../includes/howto-service-bus-queues.md)]

[!INCLUDE [service-bus-create-namespace-portal](../../includes/service-bus-create-namespace-portal.md)]

> [!NOTE]
> <span data-ttu-id="cf8c8-107">tooinstall Python lub hello [pakiet języka Python Azure Service Bus][Python Azure Service Bus package], zobacz hello [Przewodnik instalacji języka Python](../python-how-to-install.md).</span><span class="sxs-lookup"><span data-stu-id="cf8c8-107">tooinstall Python or hello [Python Azure Service Bus package][Python Azure Service Bus package], see hello [Python Installation Guide](../python-how-to-install.md).</span></span>
> 
> 

## <a name="create-a-queue"></a><span data-ttu-id="cf8c8-108">Tworzenie kolejki</span><span class="sxs-lookup"><span data-stu-id="cf8c8-108">Create a queue</span></span>
<span data-ttu-id="cf8c8-109">Witaj **ServiceBusService** obiektu umożliwia toowork z kolejki.</span><span class="sxs-lookup"><span data-stu-id="cf8c8-109">hello **ServiceBusService** object enables you toowork with queues.</span></span> <span data-ttu-id="cf8c8-110">Dodaj następującego kodu dla dowolnego pliku Python, w którym chcesz tooprogrammatically dostępu do usługi Service Bus górze hello hello:</span><span class="sxs-lookup"><span data-stu-id="cf8c8-110">Add hello following code near hello top of any Python file in which you wish tooprogrammatically access Service Bus:</span></span>

```python
from azure.servicebus import ServiceBusService, Message, Queue
```

<span data-ttu-id="cf8c8-111">Witaj poniższy kod tworzy **ServiceBusService** obiektu.</span><span class="sxs-lookup"><span data-stu-id="cf8c8-111">hello following code creates a **ServiceBusService** object.</span></span> <span data-ttu-id="cf8c8-112">Zastąp `mynamespace`, `sharedaccesskeyname`, i `sharedaccesskey` nazwą przestrzeni nazw, nazwę klucza sygnatury dostępu Współdzielonego dostępu współdzielonego i wartość.</span><span class="sxs-lookup"><span data-stu-id="cf8c8-112">Replace `mynamespace`, `sharedaccesskeyname`, and `sharedaccesskey` with your namespace, shared access signature (SAS) key name, and value.</span></span>

```python
bus_service = ServiceBusService(
    service_namespace='mynamespace',
    shared_access_key_name='sharedaccesskeyname',
    shared_access_key_value='sharedaccesskey')
```

<span data-ttu-id="cf8c8-113">Hello wartości nazwy klucza SAS hello i wartości można znaleźć w hello [portalu Azure] [ Azure portal] informacje dotyczące połączenia, lub w Visual Studio hello **właściwości** okienku, wybierając Witaj przestrzeń nazw magistrali usług w Eksploratorze serwera (jak pokazano w poprzedniej sekcji hello).</span><span class="sxs-lookup"><span data-stu-id="cf8c8-113">hello values for hello SAS key name and value can be found in hello [Azure portal][Azure portal] connection information, or in hello Visual Studio **Properties** pane when selecting hello Service Bus namespace in Server Explorer (as shown in hello previous section).</span></span>

```python
bus_service.create_queue('taskqueue')
```

<span data-ttu-id="cf8c8-114">Witaj `create_queue` metoda obsługuje również dodatkowe opcje umożliwiające toooverride domyślne kolejki ustawienia, takie jak toolive czasu wiadomości (TTL) lub maksymalny rozmiar kolejki.</span><span class="sxs-lookup"><span data-stu-id="cf8c8-114">hello `create_queue` method also supports additional options, which enable you toooverride default queue settings such as message time toolive (TTL) or maximum queue size.</span></span> <span data-ttu-id="cf8c8-115">Witaj poniższy przykład ustawia hello kolejki maksymalny rozmiar too5 GB i minutę too1 wartość TTL hello:</span><span class="sxs-lookup"><span data-stu-id="cf8c8-115">hello following example sets hello maximum queue size too5 GB, and hello TTL value too1 minute:</span></span>

```python
queue_options = Queue()
queue_options.max_size_in_megabytes = '5120'
queue_options.default_message_time_to_live = 'PT1M'

bus_service.create_queue('taskqueue', queue_options)
```

## <a name="send-messages-tooa-queue"></a><span data-ttu-id="cf8c8-116">Komunikaty tooa kolejki wysyłania</span><span class="sxs-lookup"><span data-stu-id="cf8c8-116">Send messages tooa queue</span></span>
<span data-ttu-id="cf8c8-117">toosend kolejki usługi Service Bus tooa wiadomość hello wywołuje aplikacji `send_queue_message` metody na powitania **ServiceBusService** obiektu.</span><span class="sxs-lookup"><span data-stu-id="cf8c8-117">toosend a message tooa Service Bus queue, your application calls hello `send_queue_message` method on hello **ServiceBusService** object.</span></span>

<span data-ttu-id="cf8c8-118">Witaj poniższym przykładzie pokazano, jak toosend toohello kolejki wiadomości testowej o nazwie `taskqueue` przy użyciu `send_queue_message`:</span><span class="sxs-lookup"><span data-stu-id="cf8c8-118">hello following example demonstrates how toosend a test message toohello queue named `taskqueue` using `send_queue_message`:</span></span>

```python
msg = Message(b'Test Message')
bus_service.send_queue_message('taskqueue', msg)
```

<span data-ttu-id="cf8c8-119">Kolejki usługi Service Bus obsługują maksymalny rozmiar komunikatu 256 KB w hello [warstwy standardowa](service-bus-premium-messaging.md) i 1 MB w hello [warstwy Premium](service-bus-premium-messaging.md).</span><span class="sxs-lookup"><span data-stu-id="cf8c8-119">Service Bus queues support a maximum message size of 256 KB in hello [Standard tier](service-bus-premium-messaging.md) and 1 MB in hello [Premium tier](service-bus-premium-messaging.md).</span></span> <span data-ttu-id="cf8c8-120">Nagłówek Hello, który zawiera standardowy hello i właściwości niestandardowych aplikacji, może mieć maksymalny rozmiar 64 KB.</span><span class="sxs-lookup"><span data-stu-id="cf8c8-120">hello header, which includes hello standard and custom application properties, can have a maximum size of 64 KB.</span></span> <span data-ttu-id="cf8c8-121">Nie ma żadnego limitu liczby hello wiadomości w kolejce, ale jest ograniczenie całkowitego rozmiaru przechowywanych przez kolejkę wiadomości powitania hello.</span><span class="sxs-lookup"><span data-stu-id="cf8c8-121">There is no limit on hello number of messages held in a queue but there is a cap on hello total size of hello messages held by a queue.</span></span> <span data-ttu-id="cf8c8-122">Ten rozmiar kolejki jest definiowany w czasie tworzenia, z górnym limitem 5 GB.</span><span class="sxs-lookup"><span data-stu-id="cf8c8-122">This queue size is defined at creation time, with an upper limit of 5 GB.</span></span> <span data-ttu-id="cf8c8-123">Aby uzyskać więcej informacji na temat przydziałów, zobacz [przydziały usługi Service Bus][Service Bus quotas].</span><span class="sxs-lookup"><span data-stu-id="cf8c8-123">For more information about quotas, see [Service Bus quotas][Service Bus quotas].</span></span>

## <a name="receive-messages-from-a-queue"></a><span data-ttu-id="cf8c8-124">Odbieranie komunikatów z kolejki</span><span class="sxs-lookup"><span data-stu-id="cf8c8-124">Receive messages from a queue</span></span>
<span data-ttu-id="cf8c8-125">Komunikaty są odbierane z kolejki przy użyciu hello `receive_queue_message` metody na powitania **ServiceBusService** obiektu:</span><span class="sxs-lookup"><span data-stu-id="cf8c8-125">Messages are received from a queue using hello `receive_queue_message` method on hello **ServiceBusService** object:</span></span>

```python
msg = bus_service.receive_queue_message('taskqueue', peek_lock=False)
print(msg.body)
```

<span data-ttu-id="cf8c8-126">Wiadomości są usuwane z kolejki hello podczas ich podczas wczytywania hello parametru `peek_lock` ustawiono zbyt**False**.</span><span class="sxs-lookup"><span data-stu-id="cf8c8-126">Messages are deleted from hello queue as they are read when hello parameter `peek_lock` is set too**False**.</span></span> <span data-ttu-id="cf8c8-127">Można odczytać (peek) i Zablokuj wiadomość hello bez jego usuwania z kolejki hello przez ustawienie parametru hello `peek_lock` za**True**.</span><span class="sxs-lookup"><span data-stu-id="cf8c8-127">You can read (peek) and lock hello message without deleting it from hello queue by setting hello parameter `peek_lock` too**True**.</span></span>

<span data-ttu-id="cf8c8-128">Witaj zachowanie odczytu i usuwanie wiadomości powitania jako część hello operacji odbierania jest hello najprostszym modelem i działa najlepiej w scenariuszach, w których aplikacja może tolerować nieprzetworzenie komunikatu w przypadku hello awarii.</span><span class="sxs-lookup"><span data-stu-id="cf8c8-128">hello behavior of reading and deleting hello message as part of hello receive operation is hello simplest model, and works best for scenarios in which an application can tolerate not processing a message in hello event of a failure.</span></span> <span data-ttu-id="cf8c8-129">toounderstand, Rozważmy scenariusz w problemy, które konsumenta hello hello mógł odebrać żądanie, a następnie ulega awarii przed jego przetworzeniem.</span><span class="sxs-lookup"><span data-stu-id="cf8c8-129">toounderstand this, consider a scenario in which hello consumer issues hello receive request and then crashes before processing it.</span></span> <span data-ttu-id="cf8c8-130">Ponieważ usługi Service Bus będzie zostały oznaczone hello komunikat jako wykorzystany, następnie podczas aplikacji hello uruchamia ponownie i rozpoczyna się ponownie korzystanie z komunikatów, pominie utracony wiadomości powitania, który został wykorzystany przed toohello awarii.</span><span class="sxs-lookup"><span data-stu-id="cf8c8-130">Because Service Bus will have marked hello message as being consumed, then when hello application restarts and begins consuming messages again, it will have missed hello message that was consumed prior toohello crash.</span></span>

<span data-ttu-id="cf8c8-131">Jeśli hello `peek_lock` ustawiona jest zbyt**True**, hello odbieranie staje się operacją dwuetapowy, dzięki czemu możliwe toosupport aplikacji, które nie tolerują brakujących komunikatów.</span><span class="sxs-lookup"><span data-stu-id="cf8c8-131">If hello `peek_lock` parameter is set too**True**, hello receive becomes a two stage operation, which makes it possible toosupport applications that cannot tolerate missing messages.</span></span> <span data-ttu-id="cf8c8-132">Usługa Service Bus odbiera żądanie, znajduje się dalej toobe wiadomość hello używane, blokuje go tooprevent innym klientom odebrania go i zwraca go po toohello aplikacji.</span><span class="sxs-lookup"><span data-stu-id="cf8c8-132">When Service Bus receives a request, it finds hello next message toobe consumed, locks it tooprevent other consumers receiving it, and then returns it toohello application.</span></span> <span data-ttu-id="cf8c8-133">Kiedy aplikacja hello zakończy przetwarzanie wiadomości powitania (lub niezawodnie zapisze go w celu przyszłego przetwarzania), wykonuje drugi etap hello hello odbierania przez wywołanie hello procesu **usunąć** metody na powitania **komunikat** obiektu.</span><span class="sxs-lookup"><span data-stu-id="cf8c8-133">After hello application finishes processing hello message (or stores it reliably for future processing), it completes hello second stage of hello receive process by calling hello **delete** method on hello **Message** object.</span></span> <span data-ttu-id="cf8c8-134">Witaj **usunąć** — metoda będzie oznaczyć hello komunikat jako wykorzystany i usunąć go z kolejki hello.</span><span class="sxs-lookup"><span data-stu-id="cf8c8-134">hello **delete** method will mark hello message as being consumed and remove it from hello queue.</span></span>

```python
msg = bus_service.receive_queue_message('taskqueue', peek_lock=True)
print(msg.body)

msg.delete()
```

## <a name="how-toohandle-application-crashes-and-unreadable-messages"></a><span data-ttu-id="cf8c8-135">Jak wystąpiła awaria aplikacji toohandle i nie można go odczytać wiadomości</span><span class="sxs-lookup"><span data-stu-id="cf8c8-135">How toohandle application crashes and unreadable messages</span></span>
<span data-ttu-id="cf8c8-136">Usługa Service Bus udostępnia toohelp funkcji, które bezpieczne odzyskiwanie w razie błędów w aplikacji lub trudności z przetwarzaniem komunikatu.</span><span class="sxs-lookup"><span data-stu-id="cf8c8-136">Service Bus provides functionality toohelp you gracefully recover from errors in your application or difficulties processing a message.</span></span> <span data-ttu-id="cf8c8-137">Jeśli aplikacja odbiorcy nie tooprocess hello komunikat dla jakiegoś powodu, wówczas może wywołać hello **odblokować** metody na powitania **komunikat** obiektu.</span><span class="sxs-lookup"><span data-stu-id="cf8c8-137">If a receiver application is unable tooprocess hello message for some reason, then it can call hello **unlock** method on hello **Message** object.</span></span> <span data-ttu-id="cf8c8-138">Spowoduje to spowodować, że wiadomość hello toounlock usługi Service Bus w kolejce hello i stał się dostępny toobe odbioru, albo hello przez sam korzystanie z aplikacji lub inną odbierającą aplikację.</span><span class="sxs-lookup"><span data-stu-id="cf8c8-138">This will cause Service Bus toounlock hello message within hello queue and make it available toobe received again, either by hello same consuming application or by another consuming application.</span></span>

<span data-ttu-id="cf8c8-139">Istnieje również limit czasu skojarzony z komunikatem zablokowanym w kolejce hello, a jeśli hello hello aplikacji kończy się niepowodzeniem, które tooprocess hello komunikatu przed przekroczenie limitu czasu blokady upływem (np. Jeśli wystąpiła awaria aplikacji hello), Usługa Service Bus spowoduje automatyczne odblokowywanie wiadomość hello i stał się dostępny toobe odbioru.</span><span class="sxs-lookup"><span data-stu-id="cf8c8-139">There is also a timeout associated with a message locked within hello queue, and if hello application fails tooprocess hello message before hello lock timeout expires (e.g., if hello application crashes), then Service Bus will unlock hello message automatically and make it available toobe received again.</span></span>

<span data-ttu-id="cf8c8-140">W hello zdarzenie, które aplikacji hello ulegnie awarii po przetworzeniu wiadomość hello, ale przed hello **usunąć** metoda jest wywoływana, a następnie wiadomość hello jest przed przeniesieniem toohello aplikacji po jej ponownym uruchomieniu.</span><span class="sxs-lookup"><span data-stu-id="cf8c8-140">In hello event that hello application crashes after processing hello message but before hello **delete** method is called, then hello message will be redelivered toohello application when it restarts.</span></span> <span data-ttu-id="cf8c8-141">Jest to często nazywane **przetwarzaniem co najmniej raz**, oznacza to, że każdy komunikat będzie przetwarzany co najmniej raz, ale w niektórych sytuacjach hello sam komunikat może być dostarczony ponownie.</span><span class="sxs-lookup"><span data-stu-id="cf8c8-141">This is often called **At Least Once Processing**, that is, each message will be processed at least once but in certain situations hello same message may be redelivered.</span></span> <span data-ttu-id="cf8c8-142">Jeśli hello scenariusz nie Toleruje dwukrotnego przetwarzania, deweloperzy aplikacji powinni dodać dodatkową logikę tootheir aplikacji toohandle dwukrotnego dostarczania komunikatów.</span><span class="sxs-lookup"><span data-stu-id="cf8c8-142">If hello scenario cannot tolerate duplicate processing, then application developers should add additional logic tootheir application toohandle duplicate message delivery.</span></span> <span data-ttu-id="cf8c8-143">Jest to często osiągane przy użyciu hello **MessageId** właściwości wiadomości powitania, która pozostaje niezmienna między kolejnymi próbami dostarczenia.</span><span class="sxs-lookup"><span data-stu-id="cf8c8-143">This is often achieved using hello **MessageId** property of hello message, which will remain constant across delivery attempts.</span></span>

## <a name="next-steps"></a><span data-ttu-id="cf8c8-144">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="cf8c8-144">Next steps</span></span>
<span data-ttu-id="cf8c8-145">Teraz, kiedy znasz już podstawy hello kolejek usługi Service Bus, zobacz następujące artykuły toolearn więcej.</span><span class="sxs-lookup"><span data-stu-id="cf8c8-145">Now that you have learned hello basics of Service Bus queues, see these articles toolearn more.</span></span>

* <span data-ttu-id="cf8c8-146">[Kolejki, tematy i subskrypcje][Queues, topics, and subscriptions]</span><span class="sxs-lookup"><span data-stu-id="cf8c8-146">[Queues, topics, and subscriptions][Queues, topics, and subscriptions]</span></span>

[Azure portal]: https://portal.azure.com
[Python Azure Service Bus package]: https://pypi.python.org/pypi/azure-servicebus  
[Queues, topics, and subscriptions]: service-bus-queues-topics-subscriptions.md
[Service Bus quotas]: service-bus-quotas.md

