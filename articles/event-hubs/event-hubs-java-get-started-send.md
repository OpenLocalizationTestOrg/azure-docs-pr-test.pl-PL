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
# <a name="send-events-tooazure-event-hubs-using-java"></a><span data-ttu-id="c4e0c-103">Wysyłanie zdarzeń tooAzure Event Hubs przy użyciu języka Java</span><span class="sxs-lookup"><span data-stu-id="c4e0c-103">Send events tooAzure Event Hubs using Java</span></span>

## <a name="introduction"></a><span data-ttu-id="c4e0c-104">Wprowadzenie</span><span class="sxs-lookup"><span data-stu-id="c4e0c-104">Introduction</span></span>
<span data-ttu-id="c4e0c-105">Event Hubs to wysoce skalowalny system przyjmowania może obsługiwać miliony zdarzeń na sekundę, włączanie tooprocess aplikacji i analizowanie olbrzymich ilości danych wytworzonych przez podłączone urządzenia i aplikacje hello.</span><span class="sxs-lookup"><span data-stu-id="c4e0c-105">Event Hubs is a highly scalable ingestion system that can ingest millions of events per second, enabling an application tooprocess and analyze hello massive amounts of data produced by your connected devices and applications.</span></span> <span data-ttu-id="c4e0c-106">Po zebraniu danych do Centrum zdarzeń, można przekształcić i przechowywanie danych przy użyciu dowolnego dostawcy analiz w czasie rzeczywistym lub magazynu klastra.</span><span class="sxs-lookup"><span data-stu-id="c4e0c-106">Once collected into an event hub, you can transform and store data using any real-time analytics provider or storage cluster.</span></span>

<span data-ttu-id="c4e0c-107">Aby uzyskać więcej informacji, zobacz hello [Przegląd usługi Event Hubs][Event Hubs overview].</span><span class="sxs-lookup"><span data-stu-id="c4e0c-107">For more information, see hello [Event Hubs overview][Event Hubs overview].</span></span>

<span data-ttu-id="c4e0c-108">Ten samouczek pokazuje, jak Centrum zdarzeń tooan toosend zdarzeń za pomocą aplikacji konsoli w języku Java.</span><span class="sxs-lookup"><span data-stu-id="c4e0c-108">This tutorial shows how toosend events tooan event hub by using a console application in Java.</span></span> <span data-ttu-id="c4e0c-109">zdarzenia tooreceive przy użyciu biblioteki hosta procesora zdarzeń Java hello, zobacz [w tym artykule](event-hubs-java-get-started-receive-eph.md), lub kliknij odpowiedni język odbierania hello w tabeli po lewej stronie powitania treści.</span><span class="sxs-lookup"><span data-stu-id="c4e0c-109">tooreceive events using hello Java Event Processor Host library, see [this article](event-hubs-java-get-started-receive-eph.md), or click hello appropriate receiving language in hello left-hand table of contents.</span></span>

<span data-ttu-id="c4e0c-110">W kolejności toocomplete tego samouczka będą potrzebne hello następujące:</span><span class="sxs-lookup"><span data-stu-id="c4e0c-110">In order toocomplete this tutorial, you will need hello following:</span></span>

* <span data-ttu-id="c4e0c-111">Środowisko projektowe Java.</span><span class="sxs-lookup"><span data-stu-id="c4e0c-111">A Java development environment.</span></span> <span data-ttu-id="c4e0c-112">W tym samouczku przyjęto założenie, [Eclipse](https://www.eclipse.org/).</span><span class="sxs-lookup"><span data-stu-id="c4e0c-112">For this tutorial, we assume [Eclipse](https://www.eclipse.org/).</span></span>
* <span data-ttu-id="c4e0c-113">Aktywne konto platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="c4e0c-113">An active Azure account.</span></span> <br/><span data-ttu-id="c4e0c-114">Jeśli go nie masz, możesz utworzyć bezpłatne konto próbne w zaledwie kilka minut.</span><span class="sxs-lookup"><span data-stu-id="c4e0c-114">If you don't have an account, you can create a free account in just a couple of minutes.</span></span> <span data-ttu-id="c4e0c-115">Aby uzyskać szczegółowe informacje, zobacz artykuł <a href="http://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fdevelop%2Fmobile%2Ftutorials%2Fget-started%2F" target="_blank">Bezpłatna wersja próbna platformy Azure</a>.</span><span class="sxs-lookup"><span data-stu-id="c4e0c-115">For details, see <a href="http://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fdevelop%2Fmobile%2Ftutorials%2Fget-started%2F" target="_blank">Azure Free Trial</a>.</span></span>

## <a name="send-messages-tooevent-hubs"></a><span data-ttu-id="c4e0c-116">Wysyłanie komunikatów tooEvent koncentratory</span><span class="sxs-lookup"><span data-stu-id="c4e0c-116">Send messages tooEvent Hubs</span></span>
<span data-ttu-id="c4e0c-117">Witaj Java jest biblioteka klienta usługi Event hubs można użyć w przypadku Maven projekty z hello [Maven centralnym repozytorium](https://search.maven.org/#search%7Cga%7C1%7Ca%3A%22azure-eventhubs%22).</span><span class="sxs-lookup"><span data-stu-id="c4e0c-117">hello Java client library for Event Hubs is available for use in Maven projects from hello [Maven Central Repository](https://search.maven.org/#search%7Cga%7C1%7Ca%3A%22azure-eventhubs%22).</span></span> <span data-ttu-id="c4e0c-118">Możesz odwoływać się do tej biblioteki, przy użyciu powitania po deklaracji zależności w pliku projektu Maven:</span><span class="sxs-lookup"><span data-stu-id="c4e0c-118">You can reference this library using hello following dependency declaration inside your Maven project file:</span></span>    

```xml
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-eventhubs</artifactId>
    <version>{VERSION}</version>
</dependency>
```

<span data-ttu-id="c4e0c-119">Dla różnych typów środowiska kompilacji, można jawnie uzyskać pliki JAR hello najnowsza wersja wydana hello [Maven centralnym repozytorium](https://search.maven.org/#search%7Cga%7C1%7Ca%3A%22azure-eventhubs%22).</span><span class="sxs-lookup"><span data-stu-id="c4e0c-119">For different types of build environments, you can explicitly obtain hello latest released JAR files from hello [Maven Central Repository](https://search.maven.org/#search%7Cga%7C1%7Ca%3A%22azure-eventhubs%22).</span></span>  

<span data-ttu-id="c4e0c-120">Dla wydawcy zdarzenie proste, należy zaimportować hello *com.microsoft.azure.eventhubs* pakiet dla klasy klienta usługi Event Hubs hello i hello *com.microsoft.azure.servicebus* pakietów dla narzędzia klas takich jako wspólne wyjątki, które są udostępniane klienta obsługi wiadomości powitania Azure Service Bus.</span><span class="sxs-lookup"><span data-stu-id="c4e0c-120">For a simple event publisher, import hello *com.microsoft.azure.eventhubs* package for hello Event Hubs client classes and hello *com.microsoft.azure.servicebus* package for utility classes such as common exceptions that are shared with hello Azure Service Bus messaging client.</span></span> 

<span data-ttu-id="c4e0c-121">Dla hello po próbki należy najpierw utworzyć nowy projekt aplikacji konsoli/powłoki Maven w Twoje ulubione środowisko projektowe Java.</span><span class="sxs-lookup"><span data-stu-id="c4e0c-121">For hello following sample, first create a new Maven project for a console/shell application in your favorite Java development environment.</span></span> <span data-ttu-id="c4e0c-122">Nazwa klasy hello `Send`.</span><span class="sxs-lookup"><span data-stu-id="c4e0c-122">Name hello class `Send`.</span></span>     

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

<span data-ttu-id="c4e0c-123">Zastąpić hello przestrzeni nazw i zdarzenia koncentratora hello wartości używane podczas tworzenia Centrum zdarzeń hello.</span><span class="sxs-lookup"><span data-stu-id="c4e0c-123">Replace hello namespace and event hub names with hello values used when you created hello event hub.</span></span>

```java
    final String namespaceName = "----ServiceBusNamespaceName-----";
    final String eventHubName = "----EventHubName-----";
    final String sasKeyName = "-----SharedAccessSignatureKeyName-----";
    final String sasKey = "---SharedAccessSignatureKey----";
    ConnectionStringBuilder connStr = new ConnectionStringBuilder(namespaceName, eventHubName, sasKeyName, sasKey);
```

<span data-ttu-id="c4e0c-124">Następnie utwórz zdarzenie pojedynczej przez przekształcania ciąg w jego kodowania UTF-8 bajtów.</span><span class="sxs-lookup"><span data-stu-id="c4e0c-124">Then, create a singular event by transforming a string into its UTF-8 byte encoding.</span></span> <span data-ttu-id="c4e0c-125">Następnie utwórz nowe wystąpienie klienta usługi Event Hubs z parametrów połączenia hello i wysłać wiadomość hello.</span><span class="sxs-lookup"><span data-stu-id="c4e0c-125">Then, create a new Event Hubs client instance from hello connection string and send hello message.</span></span>   

```java 

    byte[] payloadBytes = "Test AMQP message from JMS".getBytes("UTF-8");
    EventData sendEvent = new EventData(payloadBytes);

    EventHubClient ehClient = EventHubClient.createFromConnectionStringSync(connStr.toString());
    ehClient.sendSync(sendEvent);
    }
}

``` 

## <a name="next-steps"></a><span data-ttu-id="c4e0c-126">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="c4e0c-126">Next steps</span></span>
<span data-ttu-id="c4e0c-127">Więcej informacji na temat usługi Event Hubs można poznać, przechodząc na stronę hello następującego łącza:</span><span class="sxs-lookup"><span data-stu-id="c4e0c-127">You can learn more about Event Hubs by visiting hello following links:</span></span>

* [<span data-ttu-id="c4e0c-128">Zdarzenia są rejestrowane przy użyciu hello EventProcessorHost</span><span class="sxs-lookup"><span data-stu-id="c4e0c-128">Receive events using hello EventProcessorHost</span></span>](event-hubs-java-get-started-receive-eph.md)
* <span data-ttu-id="c4e0c-129">[Przegląd usługi Event Hubs][Event Hubs overview]</span><span class="sxs-lookup"><span data-stu-id="c4e0c-129">[Event Hubs overview][Event Hubs overview]</span></span>
* [<span data-ttu-id="c4e0c-130">Tworzenie centrum zdarzeń</span><span class="sxs-lookup"><span data-stu-id="c4e0c-130">Create an event hub</span></span>](event-hubs-create.md)
* [<span data-ttu-id="c4e0c-131">Event Hubs — często zadawane pytania</span><span class="sxs-lookup"><span data-stu-id="c4e0c-131">Event Hubs FAQ</span></span>](event-hubs-faq.md)

<!-- Links -->
[Event Hubs overview]: event-hubs-overview.md