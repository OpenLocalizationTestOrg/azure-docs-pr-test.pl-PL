---
title: "aaaReceive zdarzenia z usługi Azure Event Hubs przy użyciu języka Java | Dokumentacja firmy Microsoft"
description: "Rozpocząć odbieranie z usługi Event Hubs przy użyciu języka Java"
services: event-hubs
documentationcenter: 
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 38e3be53-251c-488f-a856-9a500f41b6ca
ms.service: event-hubs
ms.workload: core
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/15/2017
ms.author: sethm
ms.openlocfilehash: 05414a22e6616296752c678bb0af887d6f070c12
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="receive-events-from-azure-event-hubs-using-java"></a><span data-ttu-id="c734b-103">Odbieranie zdarzeń z usługi Azure Event Hubs przy użyciu języka Java</span><span class="sxs-lookup"><span data-stu-id="c734b-103">Receive events from Azure Event Hubs using Java</span></span>


## <a name="introduction"></a><span data-ttu-id="c734b-104">Wprowadzenie</span><span class="sxs-lookup"><span data-stu-id="c734b-104">Introduction</span></span>
<span data-ttu-id="c734b-105">Event Hubs to wysoce skalowalny system przyjmowania może obsługiwać miliony zdarzeń na sekundę, włączanie tooprocess aplikacji i analizowanie olbrzymich ilości danych wytworzonych przez podłączone urządzenia i aplikacje hello.</span><span class="sxs-lookup"><span data-stu-id="c734b-105">Event Hubs is a highly scalable ingestion system that can ingest millions of events per second, enabling an application tooprocess and analyze hello massive amounts of data produced by your connected devices and applications.</span></span> <span data-ttu-id="c734b-106">Po zebraniu danych do usługi Event Hubs można przekształcać dane za pomocą dowolnego dostawcy analiz w czasie rzeczywistym lub przechowywać je przy użyciu klastra magazynu.</span><span class="sxs-lookup"><span data-stu-id="c734b-106">Once collected into Event Hubs, you can transform and store data using any real-time analytics provider or storage cluster.</span></span>

<span data-ttu-id="c734b-107">Aby uzyskać więcej informacji, zobacz hello [Przegląd usługi Event Hubs][Event Hubs overview].</span><span class="sxs-lookup"><span data-stu-id="c734b-107">For more information, see hello [Event Hubs overview][Event Hubs overview].</span></span>

<span data-ttu-id="c734b-108">Ten samouczek pokazuje, jak tooreceive zdarzeń do Centrum zdarzeń za pomocą aplikacji konsoli napisanych w języku Java.</span><span class="sxs-lookup"><span data-stu-id="c734b-108">This tutorial shows how tooreceive events into an event hub using a console application written in Java.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c734b-109">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="c734b-109">Prerequisites</span></span>

<span data-ttu-id="c734b-110">Kolejność toocomplete tego samouczka niezbędne są hello następujące wymagania wstępne:</span><span class="sxs-lookup"><span data-stu-id="c734b-110">In order toocomplete this tutorial, you need hello following prerequisites:</span></span>

* <span data-ttu-id="c734b-111">Środowisko projektowe Java.</span><span class="sxs-lookup"><span data-stu-id="c734b-111">A Java development environment.</span></span> <span data-ttu-id="c734b-112">W tym samouczku przyjęto założenie, [Eclipse](https://www.eclipse.org/).</span><span class="sxs-lookup"><span data-stu-id="c734b-112">For this tutorial, we assume [Eclipse](https://www.eclipse.org/).</span></span>
* <span data-ttu-id="c734b-113">Aktywne konto platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="c734b-113">An active Azure account.</span></span> <br/><span data-ttu-id="c734b-114">Jeśli go nie masz, możesz utworzyć bezpłatne konto próbne w zaledwie kilka minut.</span><span class="sxs-lookup"><span data-stu-id="c734b-114">If you don't have an account, you can create a free account in just a couple of minutes.</span></span> <span data-ttu-id="c734b-115">Aby uzyskać szczegółowe informacje, zobacz artykuł <a href="http://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fdevelop%2Fmobile%2Ftutorials%2Fget-started%2F" target="_blank">Bezpłatna wersja próbna platformy Azure</a>.</span><span class="sxs-lookup"><span data-stu-id="c734b-115">For details, see <a href="http://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fdevelop%2Fmobile%2Ftutorials%2Fget-started%2F" target="_blank">Azure Free Trial</a>.</span></span>

## <a name="receive-messages-with-eventprocessorhost-in-java"></a><span data-ttu-id="c734b-116">Odbieranie komunikatów EventProcessorHost w języku Java</span><span class="sxs-lookup"><span data-stu-id="c734b-116">Receive messages with EventProcessorHost in Java</span></span>

<span data-ttu-id="c734b-117">**EventProcessorHost** jest klasa Java, która upraszcza odbieranie zdarzeń z usługi Event Hubs przez zarządzanie trwałymi punktami kontrolnymi i równoległymi odbiorami z tych usług.</span><span class="sxs-lookup"><span data-stu-id="c734b-117">**EventProcessorHost** is a Java class that simplifies receiving events from Event Hubs by managing persistent checkpoints and parallel receives from those Event Hubs.</span></span> <span data-ttu-id="c734b-118">Za pomocą klasy EventProcessorHost, można podzielić zdarzenia między wieloma odbiornikami, nawet w przypadku hostowania w różnych węzłach.</span><span class="sxs-lookup"><span data-stu-id="c734b-118">Using EventProcessorHost, you can split events across multiple receivers, even when hosted in different nodes.</span></span> <span data-ttu-id="c734b-119">W tym przykładzie pokazano sposób toouse EventProcessorHost dla jednego odbiornika.</span><span class="sxs-lookup"><span data-stu-id="c734b-119">This example shows how toouse EventProcessorHost for a single receiver.</span></span>

### <a name="create-a-storage-account"></a><span data-ttu-id="c734b-120">Tworzenie konta magazynu</span><span class="sxs-lookup"><span data-stu-id="c734b-120">Create a storage account</span></span>
<span data-ttu-id="c734b-121">toouse EventProcessorHost musi mieć [konta magazynu Azure][Azure Storage account]:</span><span class="sxs-lookup"><span data-stu-id="c734b-121">toouse EventProcessorHost, you must have an [Azure Storage account][Azure Storage account]:</span></span>

1. <span data-ttu-id="c734b-122">Zaloguj się na toohello [portalu Azure][Azure portal]i kliknij przycisk **+ nowy** na powitania po lewej stronie ekranu hello.</span><span class="sxs-lookup"><span data-stu-id="c734b-122">Log on toohello [Azure portal][Azure portal], and click **+ New** on hello left-hand side of hello screen.</span></span>
2. <span data-ttu-id="c734b-123">Kliknij pozycję **Magazyn**, a następnie pozycję **Konto magazynu**.</span><span class="sxs-lookup"><span data-stu-id="c734b-123">Click **Storage**, then click **Storage account**.</span></span> <span data-ttu-id="c734b-124">W hello **utworzyć konto magazynu** bloku, wpisz nazwę konta magazynu hello.</span><span class="sxs-lookup"><span data-stu-id="c734b-124">In hello **Create storage account** blade, type a name for hello storage account.</span></span> <span data-ttu-id="c734b-125">Zakończenie rest hello hello pól, wybierz odpowiedni region, a następnie kliknij **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="c734b-125">Complete hello rest of hello fields, select your desired region, and then click **Create**.</span></span>
   
    ![](./media/event-hubs-dotnet-framework-getstarted-receive-eph/create-storage2.png)

3. <span data-ttu-id="c734b-126">Kliknij hello nowo utworzone konto magazynu, a następnie kliknij przycisk **Zarządzaj kluczami dostępu**:</span><span class="sxs-lookup"><span data-stu-id="c734b-126">Click hello newly created storage account, and then click **Manage Access Keys**:</span></span>
   
    ![](./media/event-hubs-dotnet-framework-getstarted-receive-eph/create-storage3.png)

    <span data-ttu-id="c734b-127">Skopiuj hello podstawowego dostępu do klucza tooa tymczasowej lokalizacji, toouse w dalszej części tego samouczka.</span><span class="sxs-lookup"><span data-stu-id="c734b-127">Copy hello primary access key tooa temporary location, toouse later in this tutorial.</span></span>

### <a name="create-a-java-project-using-hello-eventprocessor-host"></a><span data-ttu-id="c734b-128">Tworzenie projektu języka Java przy użyciu hello EventProcessor hosta</span><span class="sxs-lookup"><span data-stu-id="c734b-128">Create a Java project using hello EventProcessor Host</span></span>
<span data-ttu-id="c734b-129">Witaj Java jest biblioteka klienta usługi Event hubs można użyć w przypadku Maven projekty z hello [Maven centralnym repozytorium][Maven Package]i można odwoływać się przy użyciu powitania po deklaracji zależności w sieci Maven pliku projektu:</span><span class="sxs-lookup"><span data-stu-id="c734b-129">hello Java client library for Event Hubs is available for use in Maven projects from hello [Maven Central Repository][Maven Package], and can be referenced using hello following dependency declaration inside your Maven project file:</span></span>    

```xml
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-eventhubs</artifactId>
    <version>{VERSION}</version>
</dependency>
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-eventhubs-eph</artifactId>
    <version>{VERSION}</version>
</dependency>
<dependency>
  <groupId>com.microsoft.azure</groupId>
  <artifactId>azure-eventhubs-eph</artifactId>
  <version>0.14.0</version>
</dependency>
```

<span data-ttu-id="c734b-130">Dla różnych typów środowiska kompilacji, można jawnie uzyskać pliki JAR hello najnowsza wersja wydana hello [Maven centralnym repozytorium] [ Maven Package] lub [hello punktu dystrybucji wersji na GitHub](https://github.com/Azure/azure-event-hubs/releases).</span><span class="sxs-lookup"><span data-stu-id="c734b-130">For different types of build environments, you can explicitly obtain hello latest released JAR files from hello [Maven Central Repository][Maven Package] or from [hello release distribution point on GitHub](https://github.com/Azure/azure-event-hubs/releases).</span></span>  

1. <span data-ttu-id="c734b-131">Dla hello po próbki należy najpierw utworzyć nowy projekt aplikacji konsoli/powłoki Maven w Twoje ulubione środowisko projektowe Java.</span><span class="sxs-lookup"><span data-stu-id="c734b-131">For hello following sample, first create a new Maven project for a console/shell application in your favorite Java development environment.</span></span> <span data-ttu-id="c734b-132">Klasa Hello jest nazywana `ErrorNotificationHandler`.</span><span class="sxs-lookup"><span data-stu-id="c734b-132">hello class is called `ErrorNotificationHandler`.</span></span>     
   
    ```java
    import java.util.function.Consumer;
    import com.microsoft.azure.eventprocessorhost.ExceptionReceivedEventArgs;
   
    public class ErrorNotificationHandler implements Consumer<ExceptionReceivedEventArgs>
    {
        @Override
        public void accept(ExceptionReceivedEventArgs t)
        {
            System.out.println("SAMPLE: Host " + t.getHostname() + " received general error notification during " + t.getAction() + ": " + t.getException().toString());
        }
    }
    ```
2. <span data-ttu-id="c734b-133">Użyj hello poniższy kod toocreate nową klasę o nazwie `EventProcessor`.</span><span class="sxs-lookup"><span data-stu-id="c734b-133">Use hello following code toocreate a new class called `EventProcessor`.</span></span>
   
    ```java
    import com.microsoft.azure.eventhubs.EventData;
    import com.microsoft.azure.eventprocessorhost.CloseReason;
    import com.microsoft.azure.eventprocessorhost.IEventProcessor;
    import com.microsoft.azure.eventprocessorhost.PartitionContext;
   
    public class EventProcessor implements IEventProcessor
    {
        private int checkpointBatchingCount = 0;
   
        @Override
        public void onOpen(PartitionContext context) throws Exception
        {
            System.out.println("SAMPLE: Partition " + context.getPartitionId() + " is opening");
        }
   
        @Override
        public void onClose(PartitionContext context, CloseReason reason) throws Exception
        {
            System.out.println("SAMPLE: Partition " + context.getPartitionId() + " is closing for reason " + reason.toString());
        }
   
        @Override
        public void onError(PartitionContext context, Throwable error)
        {
            System.out.println("SAMPLE: Partition " + context.getPartitionId() + " onError: " + error.toString());
        }
   
        @Override
        public void onEvents(PartitionContext context, Iterable<EventData> messages) throws Exception
        {
            System.out.println("SAMPLE: Partition " + context.getPartitionId() + " got message batch");
            int messageCount = 0;
            for (EventData data : messages)
            {
                System.out.println("SAMPLE (" + context.getPartitionId() + "," + data.getSystemProperties().getOffset() + "," +
                        data.getSystemProperties().getSequenceNumber() + "): " + new String(data.getBody(), "UTF8"));
                messageCount++;
   
                this.checkpointBatchingCount++;
                if ((checkpointBatchingCount % 5) == 0)
                {
                    System.out.println("SAMPLE: Partition " + context.getPartitionId() + " checkpointing at " +
                        data.getSystemProperties().getOffset() + "," + data.getSystemProperties().getSequenceNumber());
                    context.checkpoint(data);
                }
            }
            System.out.println("SAMPLE: Partition " + context.getPartitionId() + " batch size was " + messageCount + " for host " + context.getOwner());
        }
    }
    ```
3. <span data-ttu-id="c734b-134">Utwórz jeden więcej klasy o nazwie `EventProcessorSample`za pomocą hello następujący kod.</span><span class="sxs-lookup"><span data-stu-id="c734b-134">Create one more class called `EventProcessorSample`, using hello following code.</span></span>
   
    ```java
    import com.microsoft.azure.eventprocessorhost.*;
    import com.microsoft.azure.servicebus.ConnectionStringBuilder;
    import com.microsoft.azure.eventhubs.EventData;
   
    public class EventProcessorSample
    {
        public static void main(String args[])
        {
            final String consumerGroupName = "$Default";
            final String namespaceName = "----ServiceBusNamespaceName-----";
            final String eventHubName = "----EventHubName-----";
            final String sasKeyName = "-----SharedAccessSignatureKeyName-----";
            final String sasKey = "---SharedAccessSignatureKey----";
   
            final String storageAccountName = "---StorageAccountName----";
            final String storageAccountKey = "---StorageAccountKey----";
            final String storageConnectionString = "DefaultEndpointsProtocol=https;AccountName=" + storageAccountName + ";AccountKey=" + storageAccountKey;
   
            ConnectionStringBuilder eventHubConnectionString = new ConnectionStringBuilder(namespaceName, eventHubName, sasKeyName, sasKey);
   
            EventProcessorHost host = new EventProcessorHost(eventHubName, consumerGroupName, eventHubConnectionString.toString(), storageConnectionString);
   
            System.out.println("Registering host named " + host.getHostName());
            EventProcessorOptions options = new EventProcessorOptions();
            options.setExceptionNotification(new ErrorNotificationHandler());
            try
            {
                host.registerEventProcessor(EventProcessor.class, options).get();
            }
            catch (Exception e)
            {
                System.out.print("Failure while registering: ");
                if (e instanceof ExecutionException)
                {
                    Throwable inner = e.getCause();
                    System.out.println(inner.toString());
                }
                else
                {
                    System.out.println(e.toString());
                }
            }
   
            System.out.println("Press enter toostop");
            try
            {
                System.in.read();
                host.unregisterEventProcessor();
   
                System.out.println("Calling forceExecutorShutdown");
                EventProcessorHost.forceExecutorShutdown(120);
            }
            catch(Exception e)
            {
                System.out.println(e.toString());
                e.printStackTrace();
            }
   
            System.out.println("End of sample");
        }
    }
    ```
4. <span data-ttu-id="c734b-135">Zastąp hello następujące pola z wartościami hello przy tworzeniu hello zdarzenia koncentratora i konto magazynu.</span><span class="sxs-lookup"><span data-stu-id="c734b-135">Replace hello following fields with hello values used when you created hello event hub and storage account.</span></span>
   
    ```java
    final String namespaceName = "----ServiceBusNamespaceName-----";
    final String eventHubName = "----EventHubName-----";
   
    final String sasKeyName = "-----SharedAccessSignatureKeyName-----";
    final String sasKey = "---SharedAccessSignatureKey----";
   
    final String storageAccountName = "---StorageAccountName----"
    final String storageAccountKey = "---StorageAccountKey----";
    ```

> [!NOTE]
> <span data-ttu-id="c734b-136">Instrukcje w tym samouczku obejmują użycie pojedynczego wystąpienia hosta EventProcessorHost.</span><span class="sxs-lookup"><span data-stu-id="c734b-136">This tutorial uses a single instance of EventProcessorHost.</span></span> <span data-ttu-id="c734b-137">Przepływność tooincrease, zalecane jest uruchomienie wielu wystąpień klasy EventProcessorHost, najlepiej na oddzielnych komputerach.</span><span class="sxs-lookup"><span data-stu-id="c734b-137">tooincrease throughput, it is recommended that you run multiple instances of EventProcessorHost, preferably on separate machines.</span></span>  <span data-ttu-id="c734b-138">Zapewnia to również nadmiarowości.</span><span class="sxs-lookup"><span data-stu-id="c734b-138">This provides redundancy as well.</span></span> <span data-ttu-id="c734b-139">W takich przypadkach różne wystąpienia automatycznie koordynują się ze sobą w kolejności tooload saldo hello powitalne odebranych zdarzeń.</span><span class="sxs-lookup"><span data-stu-id="c734b-139">In those cases, hello various instances automatically coordinate with each other in order tooload balance hello received events.</span></span> <span data-ttu-id="c734b-140">Jeśli chcesz, aby wiele odbiorników tooeach procesu *wszystkie* hello zdarzenia, należy użyć hello **grupy konsumentów** koncepcji.</span><span class="sxs-lookup"><span data-stu-id="c734b-140">If you want multiple receivers tooeach process *all* hello events, you must use hello **ConsumerGroup** concept.</span></span> <span data-ttu-id="c734b-141">Podczas odbierania zdarzeń z różnych komputerów, w których są one wdrażane może być przydatne toospecify nazwy wystąpień klasy EventProcessorHost na podstawie hello maszyny (lub role).</span><span class="sxs-lookup"><span data-stu-id="c734b-141">When receiving events from different machines, it might be useful toospecify names for EventProcessorHost instances based on hello machines (or roles) in which they are deployed.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="c734b-142">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="c734b-142">Next steps</span></span>
<span data-ttu-id="c734b-143">Więcej informacji na temat usługi Event Hubs można poznać, przechodząc na stronę hello następującego łącza:</span><span class="sxs-lookup"><span data-stu-id="c734b-143">You can learn more about Event Hubs by visiting hello following links:</span></span>

* [<span data-ttu-id="c734b-144">Omówienie usługi Event Hubs</span><span class="sxs-lookup"><span data-stu-id="c734b-144">Event Hubs overview</span></span>](event-hubs-what-is-event-hubs.md)
* [<span data-ttu-id="c734b-145">Tworzenie centrum zdarzeń</span><span class="sxs-lookup"><span data-stu-id="c734b-145">Create an Event Hub</span></span>](event-hubs-create.md)
* [<span data-ttu-id="c734b-146">Event Hubs — często zadawane pytania</span><span class="sxs-lookup"><span data-stu-id="c734b-146">Event Hubs FAQ</span></span>](event-hubs-faq.md)

<!-- Links -->
[Event Hubs overview]: event-hubs-what-is-event-hubs.md
[Azure Storage account]: ../storage/common/storage-create-storage-account.md
[Azure portal]: https://portal.azure.com
[Maven Package]: https://search.maven.org/#search%7Cga%7C1%7Ca%3A%22azure-eventhubs-eph%22

<!-- Images -->
[11]: ./media/service-bus-event-hubs-get-started-receive-ephjava/create-eph-csharp2.png
[12]: ./media/service-bus-event-hubs-get-started-receive-ephjava/create-eph-csharp3.png
