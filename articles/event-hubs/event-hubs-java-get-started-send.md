---
title: "aaaSend tooAzure zdarzeń usługi Event Hubs przy użyciu języka Java | Dokumentacja firmy Microsoft"
description: "Rozpoczynanie pracy wysyłania koncentratory tooEvent używany język Java"
services: event-hubs
documentationcenter: 
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 
ms.service: event-hubs
ms.workload: core
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/15/2017
ms.author: sethm
ms.openlocfilehash: ec537b8849a0cb49855e76c0c0ef4093108fe83c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="send-events-tooazure-event-hubs-using-java"></a>Wysyłanie zdarzeń tooAzure Event Hubs przy użyciu języka Java

## <a name="introduction"></a>Wprowadzenie
Event Hubs to wysoce skalowalny system przyjmowania może obsługiwać miliony zdarzeń na sekundę, włączanie tooprocess aplikacji i analizowanie olbrzymich ilości danych wytworzonych przez podłączone urządzenia i aplikacje hello. Po zebraniu danych do Centrum zdarzeń, można przekształcić i przechowywanie danych przy użyciu dowolnego dostawcy analiz w czasie rzeczywistym lub magazynu klastra.

Aby uzyskać więcej informacji, zobacz hello [Przegląd usługi Event Hubs][Event Hubs overview].

Ten samouczek pokazuje, jak Centrum zdarzeń tooan toosend zdarzeń za pomocą aplikacji konsoli w języku Java. zdarzenia tooreceive przy użyciu biblioteki hosta procesora zdarzeń Java hello, zobacz [w tym artykule](event-hubs-java-get-started-receive-eph.md), lub kliknij odpowiedni język odbierania hello w tabeli po lewej stronie powitania treści.

W kolejności toocomplete tego samouczka będą potrzebne hello następujące:

* Środowisko projektowe Java. W tym samouczku przyjęto założenie, [Eclipse](https://www.eclipse.org/).
* Aktywne konto platformy Azure. <br/>Jeśli go nie masz, możesz utworzyć bezpłatne konto próbne w zaledwie kilka minut. Aby uzyskać szczegółowe informacje, zobacz artykuł <a href="http://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fdevelop%2Fmobile%2Ftutorials%2Fget-started%2F" target="_blank">Bezpłatna wersja próbna platformy Azure</a>.

## <a name="send-messages-tooevent-hubs"></a>Wysyłanie komunikatów tooEvent koncentratory
Witaj Java jest biblioteka klienta usługi Event hubs można użyć w przypadku Maven projekty z hello [Maven centralnym repozytorium](https://search.maven.org/#search%7Cga%7C1%7Ca%3A%22azure-eventhubs%22). Możesz odwoływać się do tej biblioteki, przy użyciu powitania po deklaracji zależności w pliku projektu Maven:    

```xml
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-eventhubs</artifactId>
    <version>{VERSION}</version>
</dependency>
```

Dla różnych typów środowiska kompilacji, można jawnie uzyskać pliki JAR hello najnowsza wersja wydana hello [Maven centralnym repozytorium](https://search.maven.org/#search%7Cga%7C1%7Ca%3A%22azure-eventhubs%22).  

Dla wydawcy zdarzenie proste, należy zaimportować hello *com.microsoft.azure.eventhubs* pakiet dla klasy klienta usługi Event Hubs hello i hello *com.microsoft.azure.servicebus* pakietów dla narzędzia klas takich jako wspólne wyjątki, które są udostępniane klienta obsługi wiadomości powitania Azure Service Bus. 

Dla hello po próbki należy najpierw utworzyć nowy projekt aplikacji konsoli/powłoki Maven w Twoje ulubione środowisko projektowe Java. Nazwa klasy hello `Send`.     

```java
import java.io.IOException;
import java.nio.charset.*;
import java.util.*;
import java.util.concurrent.ExecutionException;

import com.microsoft.azure.eventhubs.*;
import com.microsoft.azure.servicebus.*;

public class Send
{
    public static void main(String[] args) 
            throws ServiceBusException, ExecutionException, InterruptedException, IOException
    {
```

Zastąpić hello przestrzeni nazw i zdarzenia koncentratora hello wartości używane podczas tworzenia Centrum zdarzeń hello.

```java
    final String namespaceName = "----ServiceBusNamespaceName-----";
    final String eventHubName = "----EventHubName-----";
    final String sasKeyName = "-----SharedAccessSignatureKeyName-----";
    final String sasKey = "---SharedAccessSignatureKey----";
    ConnectionStringBuilder connStr = new ConnectionStringBuilder(namespaceName, eventHubName, sasKeyName, sasKey);
```

Następnie utwórz zdarzenie pojedynczej przez przekształcania ciąg w jego kodowania UTF-8 bajtów. Następnie utwórz nowe wystąpienie klienta usługi Event Hubs z parametrów połączenia hello i wysłać wiadomość hello.   

```java 

    byte[] payloadBytes = "Test AMQP message from JMS".getBytes("UTF-8");
    EventData sendEvent = new EventData(payloadBytes);

    EventHubClient ehClient = EventHubClient.createFromConnectionStringSync(connStr.toString());
    ehClient.sendSync(sendEvent);
    }
}

``` 

## <a name="next-steps"></a>Następne kroki
Więcej informacji na temat usługi Event Hubs można poznać, przechodząc na stronę hello następującego łącza:

* [Zdarzenia są rejestrowane przy użyciu hello EventProcessorHost](event-hubs-java-get-started-receive-eph.md)
* [Przegląd usługi Event Hubs][Event Hubs overview]
* [Tworzenie centrum zdarzeń](event-hubs-create.md)
* [Event Hubs — często zadawane pytania](event-hubs-faq.md)

<!-- Links -->
[Event Hubs overview]: event-hubs-overview.md