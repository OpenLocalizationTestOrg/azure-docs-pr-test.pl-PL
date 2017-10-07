---
title: "kolejkuje toouse aaaHow Azure Service Bus z językiem Java | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak kolejki toouse usługi Service Bus na platformie Azure. Przykłady kodu napisane w języku Java."
services: service-bus-messaging
documentationcenter: java
author: sethmanheim
manager: timlt
ms.assetid: f701439c-553e-402c-94a7-64400f997d59
ms.service: service-bus-messaging
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: Java
ms.topic: article
ms.date: 08/10/2017
ms.author: sethm
ms.openlocfilehash: f68e941438134090c5eee53459e7667bda13ff3c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-service-bus-queues-with-java"></a><span data-ttu-id="86f77-104">Jak kolejki usługi Service Bus toouse z językiem Java</span><span class="sxs-lookup"><span data-stu-id="86f77-104">How toouse Service Bus queues with Java</span></span>
[!INCLUDE [service-bus-selector-queues](../../includes/service-bus-selector-queues.md)]

<span data-ttu-id="86f77-105">W tym artykule opisano sposób toouse kolejek usługi Service Bus.</span><span class="sxs-lookup"><span data-stu-id="86f77-105">This article describes how toouse Service Bus queues.</span></span> <span data-ttu-id="86f77-106">Hello przykłady są napisane w języku Java i używają hello [zestawu Azure SDK dla języka Java][Azure SDK for Java].</span><span class="sxs-lookup"><span data-stu-id="86f77-106">hello samples are written in Java and use hello [Azure SDK for Java][Azure SDK for Java].</span></span> <span data-ttu-id="86f77-107">Witaj omówione scenariusze obejmują **tworzenie kolejek**, **wysyłania i odbierania wiadomości**, i **usuwanie kolejek**.</span><span class="sxs-lookup"><span data-stu-id="86f77-107">hello scenarios covered include **creating queues**, **sending and receiving messages**, and **deleting queues**.</span></span>

[!INCLUDE [howto-service-bus-queues](../../includes/howto-service-bus-queues.md)]

[!INCLUDE [service-bus-create-namespace-portal](../../includes/service-bus-create-namespace-portal.md)]

## <a name="configure-your-application-toouse-service-bus"></a><span data-ttu-id="86f77-108">Konfigurowanie sieci toouse aplikacji usługi Service Bus</span><span class="sxs-lookup"><span data-stu-id="86f77-108">Configure your application toouse Service Bus</span></span>
<span data-ttu-id="86f77-109">Upewnij się, że zainstalowano hello [zestawu Azure SDK dla języka Java] [ Azure SDK for Java] przed zbudowaniem tego przykładu.</span><span class="sxs-lookup"><span data-stu-id="86f77-109">Make sure you have installed hello [Azure SDK for Java][Azure SDK for Java] before building this sample.</span></span> <span data-ttu-id="86f77-110">Jeśli używasz programu Eclipse, można zainstalować hello [zestawu narzędzi platformy Azure dla programu Eclipse] [ Azure Toolkit for Eclipse] zawierającą hello Azure SDK dla języka Java.</span><span class="sxs-lookup"><span data-stu-id="86f77-110">If you are using Eclipse, you can install hello [Azure Toolkit for Eclipse][Azure Toolkit for Eclipse] that includes hello Azure SDK for Java.</span></span> <span data-ttu-id="86f77-111">Następnie można dodać hello **bibliotek usługi Microsoft Azure dla języka Java** tooyour projektu:</span><span class="sxs-lookup"><span data-stu-id="86f77-111">You can then add hello **Microsoft Azure Libraries for Java** tooyour project:</span></span>

![](./media/service-bus-java-how-to-use-queues/eclipselibs.png)

<span data-ttu-id="86f77-112">Dodaj następujące hello `import` toohello instrukcje na początku pliku Java hello:</span><span class="sxs-lookup"><span data-stu-id="86f77-112">Add hello following `import` statements toohello top of hello Java file:</span></span>

```java
// Include hello following imports toouse Service Bus APIs
import com.microsoft.windowsazure.services.servicebus.*;
import com.microsoft.windowsazure.services.servicebus.models.*;
import com.microsoft.windowsazure.core.*;
import javax.xml.datatype.*;
```

## <a name="create-a-queue"></a><span data-ttu-id="86f77-113">Tworzenie kolejki</span><span class="sxs-lookup"><span data-stu-id="86f77-113">Create a queue</span></span>
<span data-ttu-id="86f77-114">Operacje zarządzania kolejkami usługi Service Bus można wykonywać za pomocą **ServiceBusContract** klasy.</span><span class="sxs-lookup"><span data-stu-id="86f77-114">Management operations for Service Bus queues can be performed via the **ServiceBusContract** class.</span></span> <span data-ttu-id="86f77-115">A **ServiceBusContract** obiekt jest tworzony z odpowiednią konfiguracją, która hermetyzuje tokenu sygnatury dostępu Współdzielonego z uprawnieniami toomanage i hello **ServiceBusContract** klasy jest jedynym punktem hello komunikacji przy użyciu platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="86f77-115">A **ServiceBusContract** object is constructed with an appropriate configuration that encapsulates the SAS token with permissions toomanage it, and hello **ServiceBusContract** class is hello sole point of communication with Azure.</span></span>

<span data-ttu-id="86f77-116">Witaj **ServiceBusService** klasa dostarcza metody toocreate, wyliczania i usuwania kolejek.</span><span class="sxs-lookup"><span data-stu-id="86f77-116">hello **ServiceBusService** class provides methods toocreate, enumerate, and delete queues.</span></span> <span data-ttu-id="86f77-117">Witaj przykład poniżej przedstawiono sposób **ServiceBusService** obiekt może być używane toocreate kolejki o nazwie `TestQueue`, przestrzeń nazw o nazwie `HowToSample`:</span><span class="sxs-lookup"><span data-stu-id="86f77-117">hello example below shows how a **ServiceBusService** object can be used toocreate a queue named `TestQueue`, with a namespace named `HowToSample`:</span></span>

```java
Configuration config =
    ServiceBusConfiguration.configureWithSASAuthentication(
            "HowToSample",
            "RootManageSharedAccessKey",
            "SAS_key_value",
            ".servicebus.windows.net"
            );

ServiceBusContract service = ServiceBusService.create(config);
QueueInfo queueInfo = new QueueInfo("TestQueue");
try
{
    CreateQueueResult result = service.createQueue(queueInfo);
}
catch (ServiceException e)
{
    System.out.print("ServiceException encountered: ");
    System.out.println(e.getMessage());
    System.exit(-1);
}
```

<span data-ttu-id="86f77-118">Dostępne są metody na `QueueInfo` umożliwiające właściwości toobe kolejki hello dopasowane (na przykład: tooset hello domyślny czas wygaśnięcia (TTL) wartość toobe stosowane toomessages wysyłane toohello kolejki).</span><span class="sxs-lookup"><span data-stu-id="86f77-118">There are methods on `QueueInfo` that allow properties of hello queue toobe tuned (for example: tooset hello default time-to-live (TTL) value toobe applied toomessages sent toohello queue).</span></span> <span data-ttu-id="86f77-119">Witaj poniższy przykład przedstawia sposób toocreate kolejki o nazwie `TestQueue` o maksymalnym rozmiarze 5 GB:</span><span class="sxs-lookup"><span data-stu-id="86f77-119">hello following example shows how toocreate a queue named `TestQueue` with a maximum size of 5GB:</span></span>

````java
long maxSizeInMegabytes = 5120;
QueueInfo queueInfo = new QueueInfo("TestQueue");
queueInfo.setMaxSizeInMegabytes(maxSizeInMegabytes);
CreateQueueResult result = service.createQueue(queueInfo);
````

<span data-ttu-id="86f77-120">Należy pamiętać, których można używać hello `listQueues` metoda **ServiceBusContract** obiekty toocheck, jeśli kolejka o określonej nazwie już istnieje w przestrzeni nazw usługi.</span><span class="sxs-lookup"><span data-stu-id="86f77-120">Note that you can use hello `listQueues` method on **ServiceBusContract** objects toocheck if a queue with a specified name already exists within a service namespace.</span></span>

## <a name="send-messages-tooa-queue"></a><span data-ttu-id="86f77-121">Komunikaty tooa kolejki wysyłania</span><span class="sxs-lookup"><span data-stu-id="86f77-121">Send messages tooa queue</span></span>
<span data-ttu-id="86f77-122">uzyskuje aplikacji toosend kolejki komunikatów usługi Service Bus tooa **ServiceBusContract** obiektu.</span><span class="sxs-lookup"><span data-stu-id="86f77-122">toosend a message tooa Service Bus queue, your application obtains a **ServiceBusContract** object.</span></span> <span data-ttu-id="86f77-123">Witaj następującego kodu pokazuje sposób toosend wiadomość hello `TestQueue` kolejki utworzonej wcześniej w hello `HowToSample` przestrzeni nazw:</span><span class="sxs-lookup"><span data-stu-id="86f77-123">hello following code shows how toosend a message for hello `TestQueue` queue previously created in hello `HowToSample` namespace:</span></span>

```java
try
{
    BrokeredMessage message = new BrokeredMessage("MyMessage");
    service.sendQueueMessage("TestQueue", message);
}
catch (ServiceException e)
{
    System.out.print("ServiceException encountered: ");
    System.out.println(e.getMessage());
    System.exit(-1);
}
```

<span data-ttu-id="86f77-124">Komunikaty wysyłane do i odbierane z usługi Service Bus są kolejki wystąpień hello [BrokeredMessage] [ BrokeredMessage] klasy.</span><span class="sxs-lookup"><span data-stu-id="86f77-124">Messages sent to, and received from Service Bus queues are instances of hello [BrokeredMessage][BrokeredMessage] class.</span></span> <span data-ttu-id="86f77-125">[BrokeredMessage] [ BrokeredMessage] obiekty mają zestaw właściwości standardowych (takich jak [etykiety](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage.label#Microsoft_ServiceBus_Messaging_BrokeredMessage_Label) i [TimeToLive](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage.timetolive#Microsoft_ServiceBus_Messaging_BrokeredMessage_TimeToLive)), słownik, który jest używany toohold niestandardowych właściwości specyficzne dla aplikacji oraz treść dowolnych danych aplikacji.</span><span class="sxs-lookup"><span data-stu-id="86f77-125">[BrokeredMessage][BrokeredMessage] objects have a set of standard properties (such as [Label](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage.label#Microsoft_ServiceBus_Messaging_BrokeredMessage_Label) and [TimeToLive](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage.timetolive#Microsoft_ServiceBus_Messaging_BrokeredMessage_TimeToLive)), a dictionary that is used toohold custom application-specific properties, and a body of arbitrary application data.</span></span> <span data-ttu-id="86f77-126">Aplikacja może ustawić hello treści wiadomości powitania przez przekazanie dowolnego obiektu podlegającego serializacji do konstruktora hello hello [BrokeredMessage][BrokeredMessage], a odpowiedni serializator hello jest używany Obiekt hello tooserialize.</span><span class="sxs-lookup"><span data-stu-id="86f77-126">An application can set hello body of hello message by passing any serializable object into hello constructor of hello [BrokeredMessage][BrokeredMessage], and hello appropriate serializer will then be used tooserialize hello object.</span></span> <span data-ttu-id="86f77-127">Alternatywnie można udostępnić **java. WE/WY. InputStream** obiektu.</span><span class="sxs-lookup"><span data-stu-id="86f77-127">Alternatively, you can provide a **java.IO.InputStream** object.</span></span>

<span data-ttu-id="86f77-128">Witaj poniższym przykładzie pokazano, jak testu toosend pięciu komunikatów toothe `TestQueue` **MessageSender** możemy uzyskanych w poprzednich fragment kodu hello:</span><span class="sxs-lookup"><span data-stu-id="86f77-128">hello following example demonstrates how toosend five test messages toothe `TestQueue` **MessageSender** we obtained in hello previous code snippet:</span></span>

```java
for (int i=0; i<5; i++)
{
     // Create message, passing a string message for hello body.
     BrokeredMessage message = new BrokeredMessage("Test message " + i);
     // Set an additional app-specific property.
     message.setProperty("MyProperty", i);
     // Send message toohello queue
     service.sendQueueMessage("TestQueue", message);
}
```

<span data-ttu-id="86f77-129">Kolejki usługi Service Bus obsługują maksymalny rozmiar komunikatu 256 KB w hello [warstwy standardowa](service-bus-premium-messaging.md) i 1 MB w hello [warstwy Premium](service-bus-premium-messaging.md).</span><span class="sxs-lookup"><span data-stu-id="86f77-129">Service Bus queues support a maximum message size of 256 KB in hello [Standard tier](service-bus-premium-messaging.md) and 1 MB in hello [Premium tier](service-bus-premium-messaging.md).</span></span> <span data-ttu-id="86f77-130">Nagłówek Hello, który zawiera standardowy hello i właściwości niestandardowych aplikacji, może mieć maksymalny rozmiar 64 KB.</span><span class="sxs-lookup"><span data-stu-id="86f77-130">hello header, which includes hello standard and custom application properties, can have a maximum size of 64 KB.</span></span> <span data-ttu-id="86f77-131">Nie ma żadnego limitu liczby hello wiadomości w kolejce, ale jest ograniczenie całkowitego rozmiaru przechowywanych przez kolejkę wiadomości powitania hello.</span><span class="sxs-lookup"><span data-stu-id="86f77-131">There is no limit on hello number of messages held in a queue but there is a cap on hello total size of hello messages held by a queue.</span></span> <span data-ttu-id="86f77-132">Ten rozmiar kolejki jest definiowany w czasie tworzenia, z górnym limitem 5 GB.</span><span class="sxs-lookup"><span data-stu-id="86f77-132">This queue size is defined at creation time, with an upper limit of 5 GB.</span></span>

## <a name="receive-messages-from-a-queue"></a><span data-ttu-id="86f77-133">Odbieranie komunikatów z kolejki</span><span class="sxs-lookup"><span data-stu-id="86f77-133">Receive messages from a queue</span></span>
<span data-ttu-id="86f77-134">Witaj podstawowy sposób tooreceive wiadomości z kolejki jest toouse **ServiceBusContract** obiektu.</span><span class="sxs-lookup"><span data-stu-id="86f77-134">hello primary way tooreceive messages from a queue is toouse a **ServiceBusContract** object.</span></span> <span data-ttu-id="86f77-135">Odebrane komunikaty mogą pracować w dwóch różnych trybach: **ReceiveAndDelete** i **PeekLock**.</span><span class="sxs-lookup"><span data-stu-id="86f77-135">Received messages can work in two different modes: **ReceiveAndDelete** and **PeekLock**.</span></span>

<span data-ttu-id="86f77-136">Korzystając z hello **ReceiveAndDelete** trybie odbieranie jest operacją pojedynczego zrzutu - oznacza to, kiedy usługa Service Bus odbiera żądanie odczytu komunikatu w kolejce, oznacza hello komunikat jako wykorzystany i zwraca go toohello aplikacji.</span><span class="sxs-lookup"><span data-stu-id="86f77-136">When using hello **ReceiveAndDelete** mode, receive is a single-shot operation - that is, when Service Bus receives a read request for a message in a queue, it marks hello message as being consumed and returns it toohello application.</span></span> <span data-ttu-id="86f77-137">**ReceiveAndDelete** trybie (który jest trybem domyślnym hello) jest hello najprostszym modelem i działa najlepiej w scenariuszach, w których aplikacja może tolerować nieprzetworzenie komunikatu w przypadku hello awarii.</span><span class="sxs-lookup"><span data-stu-id="86f77-137">**ReceiveAndDelete** mode (which is hello default mode) is hello simplest model and works best for scenarios in which an application can tolerate not processing a message in hello event of a failure.</span></span> <span data-ttu-id="86f77-138">toounderstand, Rozważmy scenariusz w problemy, które konsumenta hello hello mógł odebrać żądanie, a następnie ulega awarii przed jego przetworzeniem.</span><span class="sxs-lookup"><span data-stu-id="86f77-138">toounderstand this, consider a scenario in which hello consumer issues hello receive request and then crashes before processing it.</span></span>
<span data-ttu-id="86f77-139">Ponieważ usługi Service Bus będzie zostały oznaczone hello komunikat jako wykorzystany, następnie podczas aplikacji hello uruchamia ponownie i rozpoczyna się ponownie korzystanie z komunikatów, pominie utracony wiadomości powitania, który został wykorzystany przed toohello awarii.</span><span class="sxs-lookup"><span data-stu-id="86f77-139">Because Service Bus will have marked hello message as being consumed, then when hello application restarts and begins consuming messages again, it will have missed hello message that was consumed prior toohello crash.</span></span>

<span data-ttu-id="86f77-140">W **PeekLock** trybie odbieranie staje się operacją dwuetapowy, dzięki czemu możliwe toosupport aplikacji, które nie tolerują brakujących komunikatów.</span><span class="sxs-lookup"><span data-stu-id="86f77-140">In **PeekLock** mode, receive becomes a two stage operation, which makes it possible toosupport applications that cannot tolerate missing messages.</span></span> <span data-ttu-id="86f77-141">Usługa Service Bus odbiera żądanie, znajduje się dalej toobe wiadomość hello używane, blokuje go tooprevent innym klientom odebrania go i zwraca go po toohello aplikacji.</span><span class="sxs-lookup"><span data-stu-id="86f77-141">When Service Bus receives a request, it finds hello next message toobe consumed, locks it tooprevent other consumers receiving it, and then returns it toohello application.</span></span> <span data-ttu-id="86f77-142">Kiedy aplikacja hello zakończy przetwarzanie wiadomości powitania (lub niezawodnie zapisze go w celu przyszłego przetwarzania), wykonuje drugi etap hello hello odbierania przez wywołanie metody procesu **usunąć** na wiadomość powitania odebrane.</span><span class="sxs-lookup"><span data-stu-id="86f77-142">After hello application finishes processing hello message (or stores it reliably for future processing), it completes hello second stage of hello receive process by calling **Delete** on hello received message.</span></span> <span data-ttu-id="86f77-143">Kiedy Usługa Service Bus widzi hello **usunąć** wywołania spowoduje oznaczenie hello komunikat jako wykorzystany i usunąć go z kolejki hello.</span><span class="sxs-lookup"><span data-stu-id="86f77-143">When Service Bus sees hello **Delete** call, it will mark hello message as being consumed and remove it from hello queue.</span></span>

<span data-ttu-id="86f77-144">Witaj poniższym przykładzie pokazano, jak mogą być odbierane wiadomości i przetworzone przy użyciu **PeekLock** trybu (nie hello tryb domyślny).</span><span class="sxs-lookup"><span data-stu-id="86f77-144">hello following example demonstrates how messages can be received and processed using **PeekLock** mode (not hello default mode).</span></span> <span data-ttu-id="86f77-145">Witaj w poniższym przykładzie nie nieskończoną pętlę i przetwarza wiadomości przychodzących do naszej `TestQueue`:</span><span class="sxs-lookup"><span data-stu-id="86f77-145">hello example below does an infinite loop and processes messages as they arrive into our `TestQueue`:</span></span>

```java
try
{
    ReceiveMessageOptions opts = ReceiveMessageOptions.DEFAULT;
    opts.setReceiveMode(ReceiveMode.PEEK_LOCK);

    while(true)  {
         ReceiveQueueMessageResult resultQM =
                 service.receiveQueueMessage("TestQueue", opts);
        BrokeredMessage message = resultQM.getValue();
        if (message != null && message.getMessageId() != null)
        {
            System.out.println("MessageID: " + message.getMessageId());
            // Display hello queue message.
            System.out.print("From queue: ");
            byte[] b = new byte[200];
            String s = null;
            int numRead = message.getBody().read(b);
            while (-1 != numRead)
            {
                s = new String(b);
                s = s.trim();
                System.out.print(s);
                numRead = message.getBody().read(b);
            }
            System.out.println();
            System.out.println("Custom Property: " +
                message.getProperty("MyProperty"));
            // Remove message from queue.
            System.out.println("Deleting this message.");
            //service.deleteMessage(message);
        }  
        else  
        {
            System.out.println("Finishing up - no more messages.");
            break;
            // Added toohandle no more messages.
            // Could instead wait for more messages toobe added.
        }
    }
}
catch (ServiceException e) {
    System.out.print("ServiceException encountered: ");
    System.out.println(e.getMessage());
    System.exit(-1);
}
catch (Exception e) {
    System.out.print("Generic exception encountered: ");
    System.out.println(e.getMessage());
    System.exit(-1);
}
```

## <a name="how-toohandle-application-crashes-and-unreadable-messages"></a><span data-ttu-id="86f77-146">Jak wystąpiła awaria aplikacji toohandle i nie można go odczytać wiadomości</span><span class="sxs-lookup"><span data-stu-id="86f77-146">How toohandle application crashes and unreadable messages</span></span>
<span data-ttu-id="86f77-147">Usługa Service Bus udostępnia toohelp funkcji, które bezpieczne odzyskiwanie w razie błędów w aplikacji lub trudności z przetwarzaniem komunikatu.</span><span class="sxs-lookup"><span data-stu-id="86f77-147">Service Bus provides functionality toohelp you gracefully recover from errors in your application or difficulties processing a message.</span></span> <span data-ttu-id="86f77-148">Jeśli aplikacja odbiorcy nie tooprocess hello komunikat dla jakiegoś powodu, wówczas może wywołać hello **unlockMessage** metody na wiadomość powitania odebranych (zamiast hello **deleteMessage** metody).</span><span class="sxs-lookup"><span data-stu-id="86f77-148">If a receiver application is unable tooprocess hello message for some reason, then it can call hello **unlockMessage** method on hello received message (instead of hello **deleteMessage** method).</span></span> <span data-ttu-id="86f77-149">Ta powoduje, że usługi Service Bus toounlock hello wiadomości w kolejce hello i stał się dostępny toobe odbioru, albo przez hello sam korzystanie z aplikacji lub inną odbierającą aplikację.</span><span class="sxs-lookup"><span data-stu-id="86f77-149">This causes Service Bus toounlock hello message within hello queue and make it available toobe received again, either by hello same consuming application or by another consuming application.</span></span>

<span data-ttu-id="86f77-150">Istnieje również limit czasu skojarzony z komunikatem zablokowanym w kolejce i jeśli aplikacja hello nie powiedzie się tooprocess hello komunikatu przed upływem limitu czasu blokady (na przykład jeśli wystąpiła awaria aplikacji hello), a następnie usługi Service Bus automatycznie odblokowuje wiadomość hello i Dzięki dostępne toobe odbioru.</span><span class="sxs-lookup"><span data-stu-id="86f77-150">There is also a timeout associated with a message locked within the queue, and if hello application fails tooprocess hello message before the lock timeout expires (for example, if hello application crashes), then Service Bus unlocks hello message automatically and makes it available toobe received again.</span></span>

<span data-ttu-id="86f77-151">W hello zdarzenie, które aplikacji hello ulegnie awarii po przetworzeniu wiadomość hello, ale przed hello **deleteMessage** żądania, a następnie wiadomość hello jest przed przeniesieniem toohello aplikacji po jej ponownym uruchomieniu.</span><span class="sxs-lookup"><span data-stu-id="86f77-151">In hello event that hello application crashes after processing hello message but before hello **deleteMessage** request is issued, then hello message is redelivered toohello application when it restarts.</span></span> <span data-ttu-id="86f77-152">Jest to często nazywane *przetwarzaniem co najmniej raz*; oznacza to, że każdy komunikat jest przetwarzany co najmniej raz, ale w niektórych sytuacjach hello sam komunikat może być dostarczony ponownie.</span><span class="sxs-lookup"><span data-stu-id="86f77-152">This is often called *At Least Once Processing*; that is, each message is processed at least once but in certain situations hello same message may be redelivered.</span></span> <span data-ttu-id="86f77-153">Jeśli hello scenariusz nie Toleruje dwukrotnego przetwarzania, deweloperzy aplikacji powinni dodać dodatkową logikę tootheir aplikacji toohandle dwukrotnego dostarczania komunikatów.</span><span class="sxs-lookup"><span data-stu-id="86f77-153">If hello scenario cannot tolerate duplicate processing, then application developers should add additional logic tootheir application toohandle duplicate message delivery.</span></span> <span data-ttu-id="86f77-154">Jest to często osiągane przy użyciu hello **getMessageId** metody wiadomość hello, która pozostaje stała między kolejnymi próbami dostarczenia.</span><span class="sxs-lookup"><span data-stu-id="86f77-154">This is often achieved using hello **getMessageId** method of hello message, which remains constant across delivery attempts.</span></span>

## <a name="next-steps"></a><span data-ttu-id="86f77-155">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="86f77-155">Next Steps</span></span>
<span data-ttu-id="86f77-156">Teraz, kiedy znasz już podstawy hello kolejek usługi Service Bus, zobacz [kolejki, tematy i subskrypcje] [ Queues, topics, and subscriptions] Aby uzyskać więcej informacji.</span><span class="sxs-lookup"><span data-stu-id="86f77-156">Now that you've learned hello basics of Service Bus queues, see [Queues, topics, and subscriptions][Queues, topics, and subscriptions] for more information.</span></span>

<span data-ttu-id="86f77-157">Aby uzyskać więcej informacji, zobacz hello [Centrum deweloperów języka Java](https://azure.microsoft.com/develop/java/).</span><span class="sxs-lookup"><span data-stu-id="86f77-157">For more information, see hello [Java Developer Center](https://azure.microsoft.com/develop/java/).</span></span>

[Azure SDK for Java]: http://azure.microsoft.com/develop/java/
[Azure Toolkit for Eclipse]: https://msdn.microsoft.com/library/azure/hh694271.aspx
[Queues, topics, and subscriptions]: service-bus-queues-topics-subscriptions.md
[BrokeredMessage]: /dotnet/api/microsoft.servicebus.messaging.brokeredmessage
