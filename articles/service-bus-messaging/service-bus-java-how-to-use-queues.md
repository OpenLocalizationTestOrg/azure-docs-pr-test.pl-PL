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
# <a name="how-toouse-service-bus-queues-with-java"></a>Jak kolejki usługi Service Bus toouse z językiem Java
[!INCLUDE [service-bus-selector-queues](../../includes/service-bus-selector-queues.md)]

W tym artykule opisano sposób toouse kolejek usługi Service Bus. Hello przykłady są napisane w języku Java i używają hello [zestawu Azure SDK dla języka Java][Azure SDK for Java]. Witaj omówione scenariusze obejmują **tworzenie kolejek**, **wysyłania i odbierania wiadomości**, i **usuwanie kolejek**.

[!INCLUDE [howto-service-bus-queues](../../includes/howto-service-bus-queues.md)]

[!INCLUDE [service-bus-create-namespace-portal](../../includes/service-bus-create-namespace-portal.md)]

## <a name="configure-your-application-toouse-service-bus"></a>Konfigurowanie sieci toouse aplikacji usługi Service Bus
Upewnij się, że zainstalowano hello [zestawu Azure SDK dla języka Java] [ Azure SDK for Java] przed zbudowaniem tego przykładu. Jeśli używasz programu Eclipse, można zainstalować hello [zestawu narzędzi platformy Azure dla programu Eclipse] [ Azure Toolkit for Eclipse] zawierającą hello Azure SDK dla języka Java. Następnie można dodać hello **bibliotek usługi Microsoft Azure dla języka Java** tooyour projektu:

![](./media/service-bus-java-how-to-use-queues/eclipselibs.png)

Dodaj następujące hello `import` toohello instrukcje na początku pliku Java hello:

```java
// Include hello following imports toouse Service Bus APIs
import com.microsoft.windowsazure.services.servicebus.*;
import com.microsoft.windowsazure.services.servicebus.models.*;
import com.microsoft.windowsazure.core.*;
import javax.xml.datatype.*;
```

## <a name="create-a-queue"></a>Tworzenie kolejki
Operacje zarządzania kolejkami usługi Service Bus można wykonywać za pomocą **ServiceBusContract** klasy. A **ServiceBusContract** obiekt jest tworzony z odpowiednią konfiguracją, która hermetyzuje tokenu sygnatury dostępu Współdzielonego z uprawnieniami toomanage i hello **ServiceBusContract** klasy jest jedynym punktem hello komunikacji przy użyciu platformy Azure.

Witaj **ServiceBusService** klasa dostarcza metody toocreate, wyliczania i usuwania kolejek. Witaj przykład poniżej przedstawiono sposób **ServiceBusService** obiekt może być używane toocreate kolejki o nazwie `TestQueue`, przestrzeń nazw o nazwie `HowToSample`:

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

Dostępne są metody na `QueueInfo` umożliwiające właściwości toobe kolejki hello dopasowane (na przykład: tooset hello domyślny czas wygaśnięcia (TTL) wartość toobe stosowane toomessages wysyłane toohello kolejki). Witaj poniższy przykład przedstawia sposób toocreate kolejki o nazwie `TestQueue` o maksymalnym rozmiarze 5 GB:

````java
long maxSizeInMegabytes = 5120;
QueueInfo queueInfo = new QueueInfo("TestQueue");
queueInfo.setMaxSizeInMegabytes(maxSizeInMegabytes);
CreateQueueResult result = service.createQueue(queueInfo);
````

Należy pamiętać, których można używać hello `listQueues` metoda **ServiceBusContract** obiekty toocheck, jeśli kolejka o określonej nazwie już istnieje w przestrzeni nazw usługi.

## <a name="send-messages-tooa-queue"></a>Komunikaty tooa kolejki wysyłania
uzyskuje aplikacji toosend kolejki komunikatów usługi Service Bus tooa **ServiceBusContract** obiektu. Witaj następującego kodu pokazuje sposób toosend wiadomość hello `TestQueue` kolejki utworzonej wcześniej w hello `HowToSample` przestrzeni nazw:

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

Komunikaty wysyłane do i odbierane z usługi Service Bus są kolejki wystąpień hello [BrokeredMessage] [ BrokeredMessage] klasy. [BrokeredMessage] [ BrokeredMessage] obiekty mają zestaw właściwości standardowych (takich jak [etykiety](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage.label#Microsoft_ServiceBus_Messaging_BrokeredMessage_Label) i [TimeToLive](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage.timetolive#Microsoft_ServiceBus_Messaging_BrokeredMessage_TimeToLive)), słownik, który jest używany toohold niestandardowych właściwości specyficzne dla aplikacji oraz treść dowolnych danych aplikacji. Aplikacja może ustawić hello treści wiadomości powitania przez przekazanie dowolnego obiektu podlegającego serializacji do konstruktora hello hello [BrokeredMessage][BrokeredMessage], a odpowiedni serializator hello jest używany Obiekt hello tooserialize. Alternatywnie można udostępnić **java. WE/WY. InputStream** obiektu.

Witaj poniższym przykładzie pokazano, jak testu toosend pięciu komunikatów toothe `TestQueue` **MessageSender** możemy uzyskanych w poprzednich fragment kodu hello:

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

Kolejki usługi Service Bus obsługują maksymalny rozmiar komunikatu 256 KB w hello [warstwy standardowa](service-bus-premium-messaging.md) i 1 MB w hello [warstwy Premium](service-bus-premium-messaging.md). Nagłówek Hello, który zawiera standardowy hello i właściwości niestandardowych aplikacji, może mieć maksymalny rozmiar 64 KB. Nie ma żadnego limitu liczby hello wiadomości w kolejce, ale jest ograniczenie całkowitego rozmiaru przechowywanych przez kolejkę wiadomości powitania hello. Ten rozmiar kolejki jest definiowany w czasie tworzenia, z górnym limitem 5 GB.

## <a name="receive-messages-from-a-queue"></a>Odbieranie komunikatów z kolejki
Witaj podstawowy sposób tooreceive wiadomości z kolejki jest toouse **ServiceBusContract** obiektu. Odebrane komunikaty mogą pracować w dwóch różnych trybach: **ReceiveAndDelete** i **PeekLock**.

Korzystając z hello **ReceiveAndDelete** trybie odbieranie jest operacją pojedynczego zrzutu - oznacza to, kiedy usługa Service Bus odbiera żądanie odczytu komunikatu w kolejce, oznacza hello komunikat jako wykorzystany i zwraca go toohello aplikacji. **ReceiveAndDelete** trybie (który jest trybem domyślnym hello) jest hello najprostszym modelem i działa najlepiej w scenariuszach, w których aplikacja może tolerować nieprzetworzenie komunikatu w przypadku hello awarii. toounderstand, Rozważmy scenariusz w problemy, które konsumenta hello hello mógł odebrać żądanie, a następnie ulega awarii przed jego przetworzeniem.
Ponieważ usługi Service Bus będzie zostały oznaczone hello komunikat jako wykorzystany, następnie podczas aplikacji hello uruchamia ponownie i rozpoczyna się ponownie korzystanie z komunikatów, pominie utracony wiadomości powitania, który został wykorzystany przed toohello awarii.

W **PeekLock** trybie odbieranie staje się operacją dwuetapowy, dzięki czemu możliwe toosupport aplikacji, które nie tolerują brakujących komunikatów. Usługa Service Bus odbiera żądanie, znajduje się dalej toobe wiadomość hello używane, blokuje go tooprevent innym klientom odebrania go i zwraca go po toohello aplikacji. Kiedy aplikacja hello zakończy przetwarzanie wiadomości powitania (lub niezawodnie zapisze go w celu przyszłego przetwarzania), wykonuje drugi etap hello hello odbierania przez wywołanie metody procesu **usunąć** na wiadomość powitania odebrane. Kiedy Usługa Service Bus widzi hello **usunąć** wywołania spowoduje oznaczenie hello komunikat jako wykorzystany i usunąć go z kolejki hello.

Witaj poniższym przykładzie pokazano, jak mogą być odbierane wiadomości i przetworzone przy użyciu **PeekLock** trybu (nie hello tryb domyślny). Witaj w poniższym przykładzie nie nieskończoną pętlę i przetwarza wiadomości przychodzących do naszej `TestQueue`:

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

## <a name="how-toohandle-application-crashes-and-unreadable-messages"></a>Jak wystąpiła awaria aplikacji toohandle i nie można go odczytać wiadomości
Usługa Service Bus udostępnia toohelp funkcji, które bezpieczne odzyskiwanie w razie błędów w aplikacji lub trudności z przetwarzaniem komunikatu. Jeśli aplikacja odbiorcy nie tooprocess hello komunikat dla jakiegoś powodu, wówczas może wywołać hello **unlockMessage** metody na wiadomość powitania odebranych (zamiast hello **deleteMessage** metody). Ta powoduje, że usługi Service Bus toounlock hello wiadomości w kolejce hello i stał się dostępny toobe odbioru, albo przez hello sam korzystanie z aplikacji lub inną odbierającą aplikację.

Istnieje również limit czasu skojarzony z komunikatem zablokowanym w kolejce i jeśli aplikacja hello nie powiedzie się tooprocess hello komunikatu przed upływem limitu czasu blokady (na przykład jeśli wystąpiła awaria aplikacji hello), a następnie usługi Service Bus automatycznie odblokowuje wiadomość hello i Dzięki dostępne toobe odbioru.

W hello zdarzenie, które aplikacji hello ulegnie awarii po przetworzeniu wiadomość hello, ale przed hello **deleteMessage** żądania, a następnie wiadomość hello jest przed przeniesieniem toohello aplikacji po jej ponownym uruchomieniu. Jest to często nazywane *przetwarzaniem co najmniej raz*; oznacza to, że każdy komunikat jest przetwarzany co najmniej raz, ale w niektórych sytuacjach hello sam komunikat może być dostarczony ponownie. Jeśli hello scenariusz nie Toleruje dwukrotnego przetwarzania, deweloperzy aplikacji powinni dodać dodatkową logikę tootheir aplikacji toohandle dwukrotnego dostarczania komunikatów. Jest to często osiągane przy użyciu hello **getMessageId** metody wiadomość hello, która pozostaje stała między kolejnymi próbami dostarczenia.

## <a name="next-steps"></a>Następne kroki
Teraz, kiedy znasz już podstawy hello kolejek usługi Service Bus, zobacz [kolejki, tematy i subskrypcje] [ Queues, topics, and subscriptions] Aby uzyskać więcej informacji.

Aby uzyskać więcej informacji, zobacz hello [Centrum deweloperów języka Java](https://azure.microsoft.com/develop/java/).

[Azure SDK for Java]: http://azure.microsoft.com/develop/java/
[Azure Toolkit for Eclipse]: https://msdn.microsoft.com/library/azure/hh694271.aspx
[Queues, topics, and subscriptions]: service-bus-queues-topics-subscriptions.md
[BrokeredMessage]: /dotnet/api/microsoft.servicebus.messaging.brokeredmessage
