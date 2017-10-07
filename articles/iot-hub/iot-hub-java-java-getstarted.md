---
title: "aaaGet pracę z Centrum IoT Azure (Java) | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak urządzenia chmury toosend wiadomości tooAzure Centrum IoT przy użyciu IoT zestawy SDK dla języka Java. Utworzyć symulowane urządzenie i tooregister aplikacji usługi, urządzenia, wysyłania wiadomości i odczytywać wiadomości z Centrum IoT."
services: iot-hub
documentationcenter: java
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 70dae4a8-0e98-4c53-b5a5-9d6963abb245
ms.service: iot-hub
ms.devlang: java
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/29/2017
ms.author: dobett
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: ac954f0522b46ed2a5b4a819bc611c13be0b9a9e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="connect-your-device-tooyour-iot-hub-using-java"></a>Połącz przy użyciu języka Java Centrum IoT tooyour urządzenia
[!INCLUDE [iot-hub-selector-get-started](../../includes/iot-hub-selector-get-started.md)]

Na końcu hello tego samouczka masz trzech aplikacji Java w konsoli:

* **Utwórz urządzenie tożsamości**, co powoduje tożsamości urządzenia i skojarzony klucz tooconnect aplikacją urządzenia.
* **Odczyt — d2c — liczba komunikatów**, który zawiera dane telemetryczne hello wysyłane przez aplikację na urządzeniu.
* **Symulowane urządzenie**, która łączy się tooyour Centrum IoT z tożsamości urządzenia hello utworzony wcześniej i wysyła komunikat telemetrii co drugi przy użyciu hello MQTT protokołu.

> [!NOTE]
> Artykuł Hello [Azure IoT SDK] [ lnk-hub-sdks] zawiera informacje o hello Azure IoT SDK, której można toobuild toorun zarówno aplikacje na urządzeniach i z zaplecza rozwiązania.

toocomplete tego samouczka należy hello następujące:

* Witaj najnowszych [Java SE Development Kit 8](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html) 
* [Maven 3](https://maven.apache.org/install.html) 
* Aktywne konto platformy Azure. (Jeśli go nie masz, możesz utworzyć [bezpłatne konto próbne][lnk-free-trial] w zaledwie kilka minut).

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

Jako ostatni krok, zanotuj hello **klucz podstawowy** wartość. Następnie kliknij przycisk **punkty końcowe** i hello **zdarzenia** wbudowanym punktem końcowym. Na powitania **właściwości** bloku, zanotuj hello **nazwę Centrum zdarzeń zgodnych** i hello **punktu końcowego Centrum zdarzeń zgodnych** adres. Te trzy wartości będą potrzebne podczas tworzenia aplikacji **read-d2c-messages**.

![Blok komunikatów usługi IoT Hub witrynie Azure Portal][6]

Utworzono centrum IoT. Masz hello nazwy hosta Centrum IoT, parametry połączenia Centrum IoT, klucz podstawowy Centrum IoT, nazwa zgodnego Centrum zdarzeń i punktu końcowego zgodnego Centrum zdarzeń należy toocomplete w tym samouczku.

## <a name="create-a-device-identity"></a>Tworzenie tożsamości urządzenia
W tej sekcji utworzysz aplikację konsoli języka Java, która tworzy tożsamość urządzenia w rejestrze tożsamości hello w Centrum IoT. Urządzenie nie może połączyć tooIoT koncentratora, chyba że jego wpis w rejestrze tożsamości hello. Aby uzyskać więcej informacji, zobacz hello **rejestru tożsamości** sekcji hello [Centrum IoT — przewodnik dewelopera][lnk-devguide-identity]. Po uruchomieniu tej aplikacji konsoli, generuje on unikatowy identyfikator urządzenia i tooIoT Centrum wiadomości klucz urządzenia można użyć tooidentify się podczas wysyłania urządzenia do chmury.

1. Utwórz pusty folder o nazwie iot-java-get-started. W folderze iot-java-get-started hello Utwórz projekt Maven o nazwie **utworzyć urządzenie identity** przy użyciu hello następujące polecenie z wiersza polecenia. Zwróć uwagę, że jest to jedno długie polecenie:

    ```cmd/sh
    mvn archetype:generate -DgroupId=com.mycompany.app -DartifactId=create-device-identity -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false
    ```

2. Wierszu polecenia przejdź toohello folderu utworzyć--tożsamości urządzenia.

3. Za pomocą edytora tekstu, otwórz plik pom.xml hello w folderze utwórz urządzenie tożsamości hello i dodaj następujące zależności toohello hello **zależności** węzła. Ta zależność umożliwia możesz toouse powitania klienta w przypadku usługi iot pakietu w aplikacji:

    ```xml
    <dependency>
      <groupId>com.microsoft.azure.sdk.iot</groupId>
      <artifactId>iot-service-client</artifactId>
      <version>1.7.23</version>
    </dependency>
    ```

    > [!NOTE]
    > Możesz sprawdzić hello najnowszą wersję **klienta w przypadku usługi iot** przy użyciu [wyszukiwania Maven][lnk-maven-service-search].

4. Zapisz i zamknij plik pom.xml hello.

5. Za pomocą edytora tekstu, otwórz plik create-device-identity\src\main\java\com\mycompany\app\App.java hello.

6. Dodaj następujące hello **zaimportować** instrukcje toohello pliku:

    ```java
    import com.microsoft.azure.sdk.iot.service.exceptions.IotHubException;
    import com.microsoft.azure.sdk.iot.service.Device;
    import com.microsoft.azure.sdk.iot.service.RegistryManager;
   
    import java.io.IOException;
    import java.net.URISyntaxException;
    ```

7. Dodaj następujące zmienne klasy toohello hello **aplikacji** klasy, zastępując **{yourhubconnectionstring}** z hello wartość Twojej dostrzeżone wcześniej:

    ```java
    private static final String connectionString = "{yourhubconnectionstring}";
    private static final String deviceId = "myFirstJavaDevice";
    ```
[!INCLUDE [iot-hub-pii-note-naming-device](../../includes/iot-hub-pii-note-naming-device.md)]

8. Modyfikowanie hello podpis hello **głównego** tooinclude metody hello wyjątków w następujący sposób:

    ```java
    public static void main( String[] args ) throws IOException, URISyntaxException, Exception
    ```

9. Dodaj następującego kodu jako treść hello hello hello **głównego** metody. Ten kod tworzy urządzenie o nazwie *javadevice* w rejestrze tożsamości usługi IoT Hub, o ile takie już nie istnieje. Następnie wyświetla hello urządzenia identyfikator i klucz, które są potrzebne później:

    ```java
    RegistryManager registryManager = RegistryManager.createFromConnectionString(connectionString);
RegistryManager registryManager = RegistryManager.createFromConnectionString(connectionString);

    // Create a device that's enabled by default, 
    // with an autogenerated key.
    Device device = Device.createFromId(deviceId, null, null);
    try {
      device = registryManager.addDevice(device);
    } catch (IotHubException iote) {
      // If hello device already exists.
      try {
        device = registryManager.getDevice(deviceId);
      } catch (IotHubException iotf) {
        iotf.printStackTrace();
      }
    }

    // Display information about the
    // device you created.
    System.out.println("Device Id: " + device.getDeviceId());
    System.out.println("Device key: " + device.getPrimaryKey());
    // Create a device that's enabled by default, 
    // with an autogenerated key.
    Device device = Device.createFromId(deviceId, null, null);
    try {
      device = registryManager.addDevice(device);
    } catch (IotHubException iote) {
      // If hello device already exists.
      try {
        device = registryManager.getDevice(deviceId);
      } catch (IotHubException iotf) {
        iotf.printStackTrace();
      }
    }

    // Display information about the
    // device you created.
    System.out.println("Device Id: " + device.getDeviceId());
    System.out.println("Device key: " + device.getPrimaryKey());
    ```

10. Zapisz i zamknij plik App.java hello.

11. Witaj toobuild **utworzyć--tożsamości urządzenia** aplikacji za pomocą programu Maven, wykonaj następujące polecenie w wierszu polecenia hello w folderze utwórz urządzenie tożsamości hello hello:

    ```cmd/sh
    mvn clean package -DskipTests
    ```

12. Witaj toorun **utworzyć--tożsamości urządzenia** aplikacji za pomocą programu Maven, wykonaj następujące polecenie w wierszu polecenia hello w folderze utwórz urządzenie tożsamości hello hello:

    ```cmd/sh
    mvn exec:java -Dexec.mainClass="com.mycompany.app.App"
    ```

13. Zanotuj hello **identyfikator urządzenia** i **klucza urządzenia**. Należy te wartości później podczas tworzenia aplikacji, która łączy tooIoT koncentratora jako urządzenie.

> [!NOTE]
> Witaj w rejestrze tożsamości Centrum IoT przechowuje dane tylko Centrum IoT toohello bezpiecznego dostępu tooenable tożsamości urządzenia. Urządzenie toouse identyfikatorów i klucze są przechowywane jako poświadczeń zabezpieczeń i flagi włączone/wyłączone, której można toodisable dostępu dla poszczególnych urządzeń. Jeśli Twoja aplikacja powinna toostore inne metadane specyficzne dla urządzenia, należy go użyć magazynu specyficzny dla aplikacji. Aby uzyskać więcej informacji, zobacz hello [Centrum IoT — przewodnik dewelopera][lnk-devguide-identity].

## <a name="receive-device-to-cloud-messages"></a>Odbieranie komunikatów z urządzenia do chmury

W tej sekcji opisano tworzenie aplikacji konsolowej Java, która odczytuje komunikaty z urządzenia do chmury z usługi IoT Hub. Przedstawia Centrum IoT [Centrum zdarzeń][lnk-event-hubs-overview]-tooenable zgodne punktu końcowego można tooread wiadomości urządzenia do chmury. elementy tookeep proste, w tym samouczku tworzy podstawowe reader, który nie jest odpowiedni dla wdrożenia wysokiej przepływności. Witaj [przetwarzania komunikatów urządzenia do chmury] [ lnk-process-d2c-tutorial] samouczek pokazuje, jak urządzenia chmury tooprocess komunikatów na dużą skalę. Witaj [Rozpoczynanie pracy z usługą Event Hubs] [ lnk-eventhubs-tutorial] samouczek zawiera dalsze informacje dotyczące sposobu tooprocess komunikaty z usługi Event Hubs i jest toohello odpowiednich punktów końcowych zgodnych z Centrum IoT Centrum zdarzeń.

> [!NOTE]
> Hello punktu końcowego Centrum zdarzeń zgodnych do odczytywania wiadomości urządzenia do chmury zawsze używa protokołu AMQP hello.

1. W folderze iot-java-get-started hello utworzonego w hello *tworzenie tożsamości urządzenia* sekcji, Utwórz projekt Maven o nazwie **odczytu — d2c — liczba komunikatów** przy użyciu hello następujące polecenie z wiersza polecenia. Zwróć uwagę, że jest to jedno długie polecenie:

    ```cmd/sh
    mvn archetype:generate -DgroupId=com.mycompany.app -DartifactId=read-d2c-messages -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false
    ```

2. Wierszu polecenia przejdź toohello odczytu — d2c — liczba komunikatów folderu.

3. Za pomocą edytora tekstu, otwórz plik pom.xml hello na odczyt d2c-wiadomości powitania w folderze i dodaj następujące zależności toohello hello **zależności** węzła. Ta zależność umożliwia toouse powitania klienta eventhubs pakietu w Twojej aplikacji tooread z punktu końcowego Centrum zdarzeń zgodnych hello:

    ```xml
    <dependency> 
        <groupId>com.microsoft.azure</groupId> 
        <artifactId>azure-eventhubs</artifactId> 
        <version>0.13.0</version> 
    </dependency>
    ```

4. Zapisz i zamknij plik pom.xml hello.

5. Za pomocą edytora tekstu, otwórz plik read-d2c-messages\src\main\java\com\mycompany\app\App.java hello.

6. Dodaj następujące hello **zaimportować** instrukcje toohello pliku:

    ```java
    import java.io.IOException;
    import com.microsoft.azure.eventhubs.*;
    import com.microsoft.azure.servicebus.*;

    import java.nio.charset.Charset;
    import java.time.*;
    import java.util.function.*;
    ```

7. Dodaj powitania po toohello zmiennej poziomie klasy **aplikacji** klasy. Zastąp **{youriothubkey}**, **{youreventhubcompatibleendpoint}**, i **{youreventhubcompatiblename}** wartościami hello zanotowany wcześniej:

    ```java
    private static String connStr = "Endpoint={youreventhubcompatibleendpoint};EntityPath={youreventhubcompatiblename};SharedAccessKeyName=iothubowner;SharedAccessKey={youriothubkey}";
    ```

8. Dodaj następujące hello **receiveMessages** toohello metody **aplikacji** klasy. Ta metoda tworzy **EventHubClient** wystąpienia tooconnect toohello zgodnego Centrum zdarzeń z punktu końcowego, a następnie asynchronicznie tworzy **PartitionReceiver** tooread wystąpienia z Centrum zdarzeń partycja. Wykonuje pętlę w sposób ciągły, a drukuje wiadomość hello — szczegóły, aż do zakończenia aplikacji hello.

    ```java
    // Create a receiver on a partition.
    private static EventHubClient receiveMessages(final String partitionId) {
      EventHubClient client = null;
      try {
        client = EventHubClient.createFromConnectionStringSync(connStr);
      } catch (Exception e) {
        System.out.println("Failed toocreate client: " + e.getMessage());
        System.exit(1);
      }
      try {
        // Create a receiver using the
        // default Event Hubs consumer group
        // that listens for messages from now on.
        client.createReceiver(EventHubClient.DEFAULT_CONSUMER_GROUP_NAME, partitionId, Instant.now())
          .thenAccept(new Consumer<PartitionReceiver>() {
            public void accept(PartitionReceiver receiver) {
              System.out.println("** Created receiver on partition " + partitionId);
              try {
                while (true) {
                  Iterable<EventData> receivedEvents = receiver.receive(100).get();
                  int batchSize = 0;
                  if (receivedEvents != null) {
                    System.out.println("Got some evenst");
                    for (EventData receivedEvent : receivedEvents) {
                      System.out.println(String.format("Offset: %s, SeqNo: %s, EnqueueTime: %s",
                        receivedEvent.getSystemProperties().getOffset(),
                        receivedEvent.getSystemProperties().getSequenceNumber(),
                        receivedEvent.getSystemProperties().getEnqueuedTime()));
                      System.out.println(String.format("| Device ID: %s",
                        receivedEvent.getSystemProperties().get("iothub-connection-device-id")));
                      System.out.println(String.format("| Message Payload: %s",
                        new String(receivedEvent.getBytes(), Charset.defaultCharset())));
                      batchSize++;
                    }
                  }
                  System.out.println(String.format("Partition: %s, ReceivedBatch Size: %s", partitionId, batchSize));
                }
              } catch (Exception e) {
                System.out.println("Failed tooreceive messages: " + e.getMessage());
              }
            }
          });
        } catch (Exception e) {
          System.out.println("Failed toocreate receiver: " + e.getMessage());
      }
      return client;
    }
    ```

   > [!NOTE]
   > Ta metoda używa filtru podczas tworzenia odbiornika hello tak, aby hello odbiornika odczytuje jedynie tooIoT wiadomości wysłane koncentratora po odbiornika hello zacznie działać. Ta technika jest przydatne w środowisku testowym, dzięki czemu bieżącego zestawu wiadomości powitania. W środowisku produkcyjnym kod powinien upewnij się, że przetwarza wszystkie wiadomości powitania — Aby uzyskać więcej informacji, zobacz hello [jak tooprocess Centrum IoT urządzenia do chmury wiadomości] [ lnk-process-d2c-tutorial] samouczka.

9. Modyfikowanie hello podpis hello **głównego** tooinclude metody hello wyjątek w następujący sposób:

    ```java
    public static void main( String[] args ) throws IOException
    ```

10. Dodaj hello następującego kodu toohello **głównego** metoda hello **aplikacji** klasy. Ten kod tworzy dwa hello **EventHubClient** i **PartitionReceiver** wystąpień i umożliwia aplikacji hello tooclose po zakończeniu przetwarzania komunikatów:

    ```java
    // Create receivers for partitions 0 and 1.
    EventHubClient client0 = receiveMessages("0");
    EventHubClient client1 = receiveMessages("1");
    System.out.println("Press ENTER tooexit.");
    System.in.read();
    try {
      client0.closeSync();
      client1.closeSync();
      System.exit(0);
    } catch (ServiceBusException sbe) {
      System.exit(1);
    }
    ```

    > [!NOTE]
    > Ten kod przyjęto założenie, że utworzono Centrum IoT w warstwie (bezpłatnie) hello F1. Bezpłatne centrum IoT ma dwie partycje o nazwie „0” i „1”.

11. Zapisz i zamknij plik App.java hello.

12. Witaj toobuild **odczytu — d2c — liczba komunikatów** aplikacji za pomocą programu Maven, wykonaj następujące polecenie w wierszu polecenia hello na odczyt d2c-wiadomości powitania w folderze hello:

    ```cmd/sh
    mvn clean package -DskipTests
    ```

## <a name="create-a-device-app"></a>Tworzenie aplikacji urządzenia
W tej sekcji utworzysz aplikację konsoli języka Java, która symuluje urządzenia, które wysyła Centrum IoT tooan wiadomości urządzenia do chmury.

1. W folderze iot-java-get-started hello utworzonego w hello *tworzenie tożsamości urządzenia* sekcji, Utwórz projekt Maven o nazwie **symulowane urządzenie** przy użyciu hello następujące polecenie z wiersza polecenia. Zwróć uwagę, że jest to jedno długie polecenie:

    ```cmd/sh
    mvn archetype:generate -DgroupId=com.mycompany.app -DartifactId=simulated-device -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false
    ```

2. Wierszu polecenia przejdź toohello symulowane urządzenie folderu.

3. Za pomocą edytora tekstu, otwórz plik pom.xml hello w folderze symulowane urządzenie hello i dodaj następujące zależności toohello hello **zależności** węzła. Ta zależność umożliwia możesz toouse hello Centrum iothub-java-pakietu klienta w Twojej toocommunicate aplikacji z Centrum IoT i tooserialize tooJSON obiektów języka Java:

    ```xml
    <dependency>
      <groupId>com.microsoft.azure.sdk.iot</groupId>
      <artifactId>iot-device-client</artifactId>
      <version>1.3.32</version>
    </dependency>
    <dependency>
      <groupId>com.google.code.gson</groupId>
      <artifactId>gson</artifactId>
      <version>2.3.1</version>
    </dependency>
    ```

    > [!NOTE]
    > Możesz sprawdzić hello najnowszą wersję **klienta w przypadku urządzenia iot** przy użyciu [wyszukiwania Maven][lnk-maven-device-search].

4. Zapisz i zamknij plik pom.xml hello.

5. Za pomocą edytora tekstu, otwórz plik simulated-device\src\main\java\com\mycompany\app\App.java hello.

6. Dodaj następujące hello **zaimportować** instrukcje toohello pliku:

    ```java
    import com.microsoft.azure.sdk.iot.device.*;
    import com.google.gson.Gson;

    import java.io.*;
    import java.net.URISyntaxException;
    import java.util.Random;
    import java.util.concurrent.Executors;
    import java.util.concurrent.ExecutorService;
    ```

7. Dodaj następujące zmienne klasy toohello hello **aplikacji** klasy. Zastępowanie **{youriothubname}** z nazwę Centrum IoT i **{yourdevicekey}** o wartości klucza urządzenia hello wygenerowanych w hello *tworzenie tożsamości urządzenia* sekcji:

    ```java
    private static String connString = "HostName={youriothubname}.azure-devices.net;DeviceId=myFirstJavaDevice;SharedAccessKey={yourdevicekey}";
    private static IotHubClientProtocol protocol = IotHubClientProtocol.MQTT;
    private static String deviceId = "myFirstJavaDevice";
    private static DeviceClient client;
    ```
   
    Ta przykładowa aplikacja używa hello **protokołu** zmiennej podczas tworzenia wystąpień **DeviceClient** obiektu. Można użyć albo toocommunicate protokołu hello, jak MQTT AMQP i HTTP z Centrum IoT.

8. Dodaj następujące hello zagnieżdżone **TelemetryDataPoint** klasy wewnątrz hello **aplikacji** klasy danych telemetrycznych hello toospecify urządzenie wysyła tooyour Centrum IoT:

    ```java
    private static class TelemetryDataPoint {
      public String deviceId;
      public double temperature;
      public double humidity;
   
      public String serialize() {
        Gson gson = new Gson();
        return gson.toJson(this);
      }
    }
    ```
9. Dodaj następujące hello zagnieżdżone **EventCallback** klasy wewnątrz hello **aplikacji** klasy toodisplay hello potwierdzenia stan hello Centrum IoT zwraca podczas przetwarzania wiadomości powitania urządzenia aplikacji. Ta metoda również powiadamia hello wątku głównego w aplikacji hello po przetworzeniu wiadomość hello:
   
    ```java
    private static class EventCallback implements IotHubEventCallback {
      public void execute(IotHubStatusCode status, Object context) {
        System.out.println("IoT Hub responded toomessage with status: " + status.name());
   
        if (context != null) {
          synchronized (context) {
            context.notify();
          }
        }
      }
    }
    ```

10. Dodaj następujące hello zagnieżdżone **MessageSender** klasy wewnątrz hello **aplikacji** klasy. Witaj **Uruchom** metoda w klasie generuje Centrum IoT tooyour toosend danych przykładowych danych telemetrycznych i czeka na potwierdzenie przed wysłaniem hello następny komunikat:

    ```java
    private static class MessageSender implements Runnable {
      public void run()  {
        try {
          double minTemperature = 20;
          double minHumidity = 60;
          Random rand = new Random();
    
          while (true) {
            double currentTemperature = minTemperature + rand.nextDouble() * 15;
            double currentHumidity = minHumidity + rand.nextDouble() * 20;
            TelemetryDataPoint telemetryDataPoint = new TelemetryDataPoint();
            telemetryDataPoint.deviceId = deviceId;
            telemetryDataPoint.temperature = currentTemperature;
            telemetryDataPoint.humidity = currentHumidity;
    
            String msgStr = telemetryDataPoint.serialize();
            Message msg = new Message(msgStr);
            msg.setProperty("temperatureAlert", (currentTemperature > 30) ? "true" : "false");
            msg.setMessageId(java.util.UUID.randomUUID().toString()); 
            System.out.println("Sending: " + msgStr);
    
            Object lockobj = new Object();
            EventCallback callback = new EventCallback();
            client.sendEventAsync(msg, callback, lockobj);
    
            synchronized (lockobj) {
              lockobj.wait();
            }
            Thread.sleep(1000);
          }
        } catch (InterruptedException e) {
          System.out.println("Finished.");
        }
      }
    }
    ```

    Ta metoda wysyła nowy komunikat urządzenia do chmury jednej sekundy po poprzedniej wiadomości powitania potwierdzeniu hello Centrum IoT. wiadomości powitania zawiera obiekt serializacji JSON z hello deviceId i losowo wygenerowane numery toosimulate czujnik temperatury i wilgotności czujnika.

11. Zastąp hello **głównego** metody za pomocą następującego kodu, która tworzy Centrum IoT wątku toosend wiadomości urządzenia do chmury tooyour hello:

    ```java
    public static void main( String[] args ) throws IOException, URISyntaxException {
      client = new DeviceClient(connString, protocol);
      client.open();
    
      MessageSender sender = new MessageSender();
    
      ExecutorService executor = Executors.newFixedThreadPool(1);
      executor.execute(sender);
    
      System.out.println("Press ENTER tooexit.");
      System.in.read();
      executor.shutdownNow();
      client.closeNow();
    }
    ```

12. Zapisz i zamknij plik App.java hello.

13. Witaj toobuild **symulowane urządzenie** aplikacji za pomocą programu Maven, wykonaj następujące polecenie w wierszu polecenia hello w folderze symulowane urządzenie hello hello:

    ```cmd/sh
    mvn clean package -DskipTests
    ```

> [!NOTE]
> rzeczy tookeep proste, w tym samouczku nie implementuje wszystkie zasady ponawiania. W kodzie produkcyjnym, należy zaimplementować zasady ponawiania (na przykład wykładniczego wycofywania), zgodnie z sugestią podaną w artykuł w witrynie MSDN hello [obsługi błędów przejściowych][lnk-transient-faults].

## <a name="run-hello-apps"></a>Uruchamianie aplikacji hello

Wszystko jest teraz gotowy toorun hello aplikacji.

1. W wierszu polecenia w folderze d2c odczytu hello uruchom następujące polecenie toobegin monitorowania hello pierwszej partycji w Centrum IoT hello:

    ```cmd/sh
    mvn exec:java -Dexec.mainClass="com.mycompany.app.App"
    ```

    ![Centrum IoT Java usługi aplikacji toomonitor urządzenia do chmury wiadomości][7]

2. W wierszu polecenia w folderze symulowane urządzenie hello Uruchom powitania po toobegin polecenie wysyłania Centrum IoT tooyour danych telemetrii:

    ```cmd/sh
    mvn exec:java -Dexec.mainClass="com.mycompany.app.App" 
    ```

    ![Centrum IoT Java urządzenia aplikacji toosend urządzenia do chmury wiadomości][8]

3. Witaj **użycia** kafelka w hello [portalu Azure] [ lnk-portal] pokazuje hello liczbę komunikatów wysłanych toohello Centrum IoT:

    ![Azure portalu użycie kafelka pokazujący liczbę komunikatów wysyłanych tooIoT Centrum][43]

## <a name="next-steps"></a>Następne kroki
W tym samouczku został skonfigurowany nowego centrum IoT w portalu Azure hello i w rejestrze tożsamości Centrum IoT hello zostanie utworzona tożsamość urządzenia. Użyto tego urządzenia tożsamości tooenable hello urządzenia aplikacji toosend wiadomości urządzenia do chmury toohello Centrum IoT. Utworzono aplikację, która wyświetla hello komunikatów odebranych przez Centrum IoT hello.

toocontinue wprowadzenie do korzystania z Centrum IoT i tooexplore innych scenariuszach IoT, zobacz:

* [Łączenie urządzenia][lnk-connect-device]
* [Wprowadzenie do zarządzania urządzeniami][lnk-device-management]
* [Getting started with Azure IoT Edge][lnk-iot-edge] (Rozpoczynanie pracy z usługą Azure IoT Edge)

toolearn tooextend IoT rozwiązanie i procesu urządzenia do chmury wiadomości na dużą skalę, zobacz temat hello [przetwarzania komunikatów urządzenia do chmury] [ lnk-process-d2c-tutorial] samouczka.
[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]

<!-- Images. -->
[6]: ./media/iot-hub-java-java-getstarted/create-iot-hub6.png
[7]: ./media/iot-hub-java-java-getstarted/runapp1.png
[8]: ./media/iot-hub-java-java-getstarted/runapp2.png
[43]: ./media/iot-hub-java-java-getstarted/usage.png

<!-- Links -->
[lnk-transient-faults]: https://msdn.microsoft.com/library/hh680901(v=pandp.50).aspx

[lnk-eventhubs-tutorial]: ../event-hubs/event-hubs-csharp-ephcs-getstarted.md
[lnk-devguide-identity]: iot-hub-devguide-identity-registry.md
[lnk-event-hubs-overview]: ../event-hubs/event-hubs-overview.md
[lnk-process-d2c-tutorial]: iot-hub-csharp-csharp-process-d2c.md

[lnk-hub-sdks]: iot-hub-devguide-sdks.md
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[lnk-portal]: https://portal.azure.com/

[lnk-device-management]: iot-hub-node-node-device-management-get-started.md
[lnk-iot-edge]: iot-hub-linux-iot-edge-get-started.md
[lnk-connect-device]: https://azure.microsoft.com/develop/iot/
[lnk-maven-service-search]: http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22iot-service-client%22%20g%3A%22com.microsoft.azure.sdk.iot%22
[lnk-maven-device-search]: http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22iot-device-client%22%20g%3A%22com.microsoft.azure.sdk.iot%22
[lnk-maven-eventhubs-search]: http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22azure-eventhubs%22
