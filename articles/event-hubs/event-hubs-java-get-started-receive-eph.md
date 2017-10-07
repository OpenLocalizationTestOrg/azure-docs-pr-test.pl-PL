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
# <a name="receive-events-from-azure-event-hubs-using-java"></a>Odbieranie zdarzeń z usługi Azure Event Hubs przy użyciu języka Java


## <a name="introduction"></a>Wprowadzenie
Event Hubs to wysoce skalowalny system przyjmowania może obsługiwać miliony zdarzeń na sekundę, włączanie tooprocess aplikacji i analizowanie olbrzymich ilości danych wytworzonych przez podłączone urządzenia i aplikacje hello. Po zebraniu danych do usługi Event Hubs można przekształcać dane za pomocą dowolnego dostawcy analiz w czasie rzeczywistym lub przechowywać je przy użyciu klastra magazynu.

Aby uzyskać więcej informacji, zobacz hello [Przegląd usługi Event Hubs][Event Hubs overview].

Ten samouczek pokazuje, jak tooreceive zdarzeń do Centrum zdarzeń za pomocą aplikacji konsoli napisanych w języku Java.

## <a name="prerequisites"></a>Wymagania wstępne

Kolejność toocomplete tego samouczka niezbędne są hello następujące wymagania wstępne:

* Środowisko projektowe Java. W tym samouczku przyjęto założenie, [Eclipse](https://www.eclipse.org/).
* Aktywne konto platformy Azure. <br/>Jeśli go nie masz, możesz utworzyć bezpłatne konto próbne w zaledwie kilka minut. Aby uzyskać szczegółowe informacje, zobacz artykuł <a href="http://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fdevelop%2Fmobile%2Ftutorials%2Fget-started%2F" target="_blank">Bezpłatna wersja próbna platformy Azure</a>.

## <a name="receive-messages-with-eventprocessorhost-in-java"></a>Odbieranie komunikatów EventProcessorHost w języku Java

**EventProcessorHost** jest klasa Java, która upraszcza odbieranie zdarzeń z usługi Event Hubs przez zarządzanie trwałymi punktami kontrolnymi i równoległymi odbiorami z tych usług. Za pomocą klasy EventProcessorHost, można podzielić zdarzenia między wieloma odbiornikami, nawet w przypadku hostowania w różnych węzłach. W tym przykładzie pokazano sposób toouse EventProcessorHost dla jednego odbiornika.

### <a name="create-a-storage-account"></a>Tworzenie konta magazynu
toouse EventProcessorHost musi mieć [konta magazynu Azure][Azure Storage account]:

1. Zaloguj się na toohello [portalu Azure][Azure portal]i kliknij przycisk **+ nowy** na powitania po lewej stronie ekranu hello.
2. Kliknij pozycję **Magazyn**, a następnie pozycję **Konto magazynu**. W hello **utworzyć konto magazynu** bloku, wpisz nazwę konta magazynu hello. Zakończenie rest hello hello pól, wybierz odpowiedni region, a następnie kliknij **Utwórz**.
   
    ![](./media/event-hubs-dotnet-framework-getstarted-receive-eph/create-storage2.png)

3. Kliknij hello nowo utworzone konto magazynu, a następnie kliknij przycisk **Zarządzaj kluczami dostępu**:
   
    ![](./media/event-hubs-dotnet-framework-getstarted-receive-eph/create-storage3.png)

    Skopiuj hello podstawowego dostępu do klucza tooa tymczasowej lokalizacji, toouse w dalszej części tego samouczka.

### <a name="create-a-java-project-using-hello-eventprocessor-host"></a>Tworzenie projektu języka Java przy użyciu hello EventProcessor hosta
Witaj Java jest biblioteka klienta usługi Event hubs można użyć w przypadku Maven projekty z hello [Maven centralnym repozytorium][Maven Package]i można odwoływać się przy użyciu powitania po deklaracji zależności w sieci Maven pliku projektu:    

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

Dla różnych typów środowiska kompilacji, można jawnie uzyskać pliki JAR hello najnowsza wersja wydana hello [Maven centralnym repozytorium] [ Maven Package] lub [hello punktu dystrybucji wersji na GitHub](https://github.com/Azure/azure-event-hubs/releases).  

1. Dla hello po próbki należy najpierw utworzyć nowy projekt aplikacji konsoli/powłoki Maven w Twoje ulubione środowisko projektowe Java. Klasa Hello jest nazywana `ErrorNotificationHandler`.     
   
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
2. Użyj hello poniższy kod toocreate nową klasę o nazwie `EventProcessor`.
   
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
3. Utwórz jeden więcej klasy o nazwie `EventProcessorSample`za pomocą hello następujący kod.
   
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
4. Zastąp hello następujące pola z wartościami hello przy tworzeniu hello zdarzenia koncentratora i konto magazynu.
   
    ```java
    final String namespaceName = "----ServiceBusNamespaceName-----";
    final String eventHubName = "----EventHubName-----";
   
    final String sasKeyName = "-----SharedAccessSignatureKeyName-----";
    final String sasKey = "---SharedAccessSignatureKey----";
   
    final String storageAccountName = "---StorageAccountName----"
    final String storageAccountKey = "---StorageAccountKey----";
    ```

> [!NOTE]
> Instrukcje w tym samouczku obejmują użycie pojedynczego wystąpienia hosta EventProcessorHost. Przepływność tooincrease, zalecane jest uruchomienie wielu wystąpień klasy EventProcessorHost, najlepiej na oddzielnych komputerach.  Zapewnia to również nadmiarowości. W takich przypadkach różne wystąpienia automatycznie koordynują się ze sobą w kolejności tooload saldo hello powitalne odebranych zdarzeń. Jeśli chcesz, aby wiele odbiorników tooeach procesu *wszystkie* hello zdarzenia, należy użyć hello **grupy konsumentów** koncepcji. Podczas odbierania zdarzeń z różnych komputerów, w których są one wdrażane może być przydatne toospecify nazwy wystąpień klasy EventProcessorHost na podstawie hello maszyny (lub role).
> 
> 

## <a name="next-steps"></a>Następne kroki
Więcej informacji na temat usługi Event Hubs można poznać, przechodząc na stronę hello następującego łącza:

* [Omówienie usługi Event Hubs](event-hubs-what-is-event-hubs.md)
* [Tworzenie centrum zdarzeń](event-hubs-create.md)
* [Event Hubs — często zadawane pytania](event-hubs-faq.md)

<!-- Links -->
[Event Hubs overview]: event-hubs-what-is-event-hubs.md
[Azure Storage account]: ../storage/common/storage-create-storage-account.md
[Azure portal]: https://portal.azure.com
[Maven Package]: https://search.maven.org/#search%7Cga%7C1%7Ca%3A%22azure-eventhubs-eph%22

<!-- Images -->
[11]: ./media/service-bus-event-hubs-get-started-receive-ephjava/create-eph-csharp2.png
[12]: ./media/service-bus-event-hubs-get-started-receive-ephjava/create-eph-csharp3.png
