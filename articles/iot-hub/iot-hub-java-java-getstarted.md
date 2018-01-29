---
title: "Rozpoczęcie pracy z usługą Azure IoT Hub (Java) | Microsoft Docs"
description: "Dowiedz się, jak wysyłać komunikaty urządzenie-chmura do usługi Azure IoT Hub za pomocą zestawów SDK usługi IoT dla języka Java. Utwórz symulowane aplikacje urządzenia i usługi, aby zarejestrować urządzenie, wysyłać wiadomości i odczytywać wiadomości z usługi IoT Hub."
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
ms.openlocfilehash: 5f41dd62d3f074eebe0c996a9c14bc7811d5b365
ms.sourcegitcommit: e266df9f97d04acfc4a843770fadfd8edf4fa2b7
ms.translationtype: HT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/11/2017
---
# <a name="connect-your-device-to-your-iot-hub-using-java"></a>Podłączanie urządzenia do usługi IoT Hub za pomocą języka Java
[!INCLUDE [iot-hub-selector-get-started](../../includes/iot-hub-selector-get-started.md)]

Na końcu tego samouczka będziesz mieć trzy aplikacje konsolowe Java:

* **create-device-identity** tworzy tożsamość urządzenia i skojarzony klucz zabezpieczeń w celu podłączenia aplikacji urządzenia.
* **read-d2c-messages** powoduje wyświetlenie telemetrii wysyłanej przez aplikację urządzenia.
* **simulated-device** łączy się z centrum IoT Hub przy użyciu utworzonej wcześniej tożsamości urządzenia i wysyła komunikat telemetrii co sekundę przy użyciu protokołu MQTT.

> [!NOTE]
> Artykuł [Azure IoT SDKs][lnk-hub-sdks] (Zestawy SDK Azure IoT) zawiera informacje dotyczące zestawów SDK Azure IoT, których można użyć do utworzenia aplikacji zarówno do uruchamiania na urządzaniach, jak i w zapleczu rozwiązania.

Do wykonania kroków tego samouczka niezbędne są następujące elementy:

* Najnowszy zestaw [Java SE Development Kit 8](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html) 
* [Maven 3](https://maven.apache.org/install.html) 
* Aktywne konto platformy Azure. (Jeśli go nie masz, możesz utworzyć [bezpłatne konto próbne][lnk-free-trial] w zaledwie kilka minut).

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

Na koniec zanotuj wartość **Klucz podstawowy**. Następnie kliknij pozycję **Punkty końcowe** i wbudowany punkt końcowy **Zdarzenia**. W bloku **Właściwości** zanotuj **nazwę zgodną z centrum zdarzeń** oraz adres **punktu końcowego zgodnego z centrum zdarzeń**. Te trzy wartości będą potrzebne podczas tworzenia aplikacji **read-d2c-messages**.

![Blok komunikatów usługi IoT Hub witrynie Azure Portal][6]

Utworzono centrum IoT. Masz nazwę hosta centrum IoT Hub, jego parametry połączenia, klucz podstawowy, nazwę zgodną z centrum zdarzeń i punkt końcowy zgodny z centrum zdarzeń potrzebne do ukończenia tego samouczka.

## <a name="create-a-device-identity"></a>Tworzenie tożsamości urządzenia
W tej sekcji utworzysz aplikację konsolową Java, tworzącą tożsamość urządzenia w rejestrze tożsamości w centrum IoT Hub. Urządzenie nie może połączyć się z centrum IoT, jeśli nie ma wpisu w rejestrze tożsamości. Więcej informacji znajduje się w sekcji **Identity registry** (Rejestr tożsamości) artykułu [IoT Hub developer guide][lnk-devguide-identity] (Usługa IoT Hub — przewodnik dewelopera). Po uruchomieniu ta aplikacja konsoli generuje unikatowy identyfikator urządzenia i klucz, których urządzenie może użyć do zidentyfikowania się podczas wysyłania komunikatów do chmury do usługi IoT Hub.

1. Utwórz pusty folder o nazwie iot-java-get-started. W folderze iot-java-get-started utwórz projekt narzędzia Maven o nazwie **create-device-identity** za pomocą następującego polecenia w wierszu polecenia. Zwróć uwagę, że jest to jedno długie polecenie:

    ```cmd/sh
    mvn archetype:generate -DgroupId=com.mycompany.app -DartifactId=create-device-identity -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false
    ```

2. W wierszu polecenia przejdź do folderu create-device-identity.

3. Za pomocą edytora tekstów otwórz plik pom.xml w folderze create-device-identity i dodaj następującą zależność do węzła **zależności**. Dzięki tej zależności możesz użyć w aplikacji pakietu iot-service-client:

    ```xml
    <dependency>
      <groupId>com.microsoft.azure.sdk.iot</groupId>
      <artifactId>iot-service-client</artifactId>
      <version>1.7.23</version>
    </dependency>
    ```

    > [!NOTE]
    > Możesz sprawdzić dostępność najnowszej wersji pakietu **iot-service-client** za pomocą [funkcji wyszukiwania narzędzia Maven][lnk-maven-service-search].

4. Zapisz i zamknij plik pom.xml.

5. Za pomocą edytora tekstów otwórz plik create-device-identity\src\main\java\com\mycompany\app\App.java.

6. Dodaj do pliku następujące instrukcje **importowania**:

    ```java
    import com.microsoft.azure.sdk.iot.service.exceptions.IotHubException;
    import com.microsoft.azure.sdk.iot.service.Device;
    import com.microsoft.azure.sdk.iot.service.RegistryManager;
   
    import java.io.IOException;
    import java.net.URISyntaxException;
    ```

7. Dodaj następujące zmienne na poziomie klasy do klasy **App**, zastępując ciąg **{yourhubconnectionstring}** zanotowaną wcześniej wartością:

    ```java
    private static final String connectionString = "{yourhubconnectionstring}";
    private static final String deviceId = "myFirstJavaDevice";
    ```
[!INCLUDE [iot-hub-pii-note-naming-device](../../includes/iot-hub-pii-note-naming-device.md)]

8. Zmodyfikuj podpis metody **main**, aby uwzględnić poniższe wyjątki:

    ```java
    public static void main( String[] args ) throws IOException, URISyntaxException, Exception
    ```

9. Dodaj następujący kod jako treść metody **głównej**. Ten kod tworzy urządzenie o nazwie *javadevice* w rejestrze tożsamości usługi IoT Hub, o ile takie już nie istnieje. Następnie wyświetla identyfikator i klucz urządzenia, które będą potrzebne później:

    ```java
    RegistryManager registryManager = RegistryManager.createFromConnectionString(connectionString);

    // Create a device that's enabled by default, 
    // with an autogenerated key.
    Device device = Device.createFromId(deviceId, null, null);
    try {
      device = registryManager.addDevice(device);
    } catch (IotHubException iote) {
      // If the device already exists.
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

10. Zapisz i zamknij plik App.java.

11. Aby utworzyć aplikację **create-device-identity** przy użyciu narzędzia Maven, wykonaj następujące polecenie w wierszu polecenia w folderze create-device-identity:

    ```cmd/sh
    mvn clean package -DskipTests
    ```

12. Aby uruchomić aplikację **create-device-identity** przy użyciu narzędzia Maven, wykonaj następujące polecenie w wierszu polecenia w folderze create-device-identity:

    ```cmd/sh
    mvn exec:java -Dexec.mainClass="com.mycompany.app.App"
    ```

13. Zanotuj **identyfikator urządzenia** i **klucz urządzenia**. Te wartości będą potrzebne później podczas tworzenia aplikacji, która łączy się z usługą IoT Hub jako urządzenie.

> [!NOTE]
> Rejestr tożsamości usługi IoT Hub przechowuje tożsamości urządzenia tylko po to, aby umożliwić bezpieczny dostęp do centrum IoT. Przechowuje identyfikatory i klucze urządzeń, które będą używane jako poświadczenia zabezpieczeń, oraz flagę włączone/wyłączone, która umożliwia wyłączenie dostępu do poszczególnych urządzeń. Jeśli aplikacja wymaga przechowywania innych metadanych dla określonego urządzenia, powinna korzystać z magazynu określonego dla aplikacji. Więcej informacji znajduje się w temacie [IoT Hub developer guide][lnk-devguide-identity] (Usługa IoT Hub — przewodnik dewelopera).

## <a name="receive-device-to-cloud-messages"></a>Odbieranie komunikatów z urządzenia do chmury

W tej sekcji opisano tworzenie aplikacji konsolowej Java, która odczytuje komunikaty z urządzenia do chmury z usługi IoT Hub. Usługa IoT Hub udostępnia punkt końcowy zgodny z [centrum zdarzeń][lnk-event-hubs-overview], aby umożliwić odczytywanie komunikatów z urządzenia do chmury. W celu uproszczenia informacji instrukcje w samouczku dotyczą tworzenia czytnika podstawowego, który nie jest odpowiedni do wdrożenia z użyciem dużej przepustowości. W samouczku [Process device-to-cloud messages (Przetwarzanie komunikatów z urządzenia do chmury)][lnk-process-d2c-tutorial] przedstawiono sposób przetwarzania komunikatów z urządzenia do chmury na dużą skalę. Samouczek [Get Started with Event Hubs (Usługa Event Hubs — wprowadzenie)][lnk-eventhubs-tutorial] zawiera dalsze informacje dotyczące sposobu przetwarzania komunikatów z usługi Event Hubs i dotyczy punktów końcowych usługi IoT Hub zgodnych z centrami zdarzeń.

> [!NOTE]
> Punkt końcowy zgodny z centrum zdarzeń przeznaczony do odczytywania komunikatów z urządzenia do chmury zawsze korzysta z protokołu AMQP.

1. W folderze iot-java-get-started utworzonym w sekcji *Tworzenie tożsamości urządzenia* utwórz projekt narzędzia Maven o nazwie **read-d2c-messages** przy użyciu następującego polecenia w wierszu polecenia. Zwróć uwagę, że jest to jedno długie polecenie:

    ```cmd/sh
    mvn archetype:generate -DgroupId=com.mycompany.app -DartifactId=read-d2c-messages -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false
    ```

2. W wierszu polecenia przejdź do folderu read-d2c-messages.

3. Za pomocą edytora tekstów otwórz plik pom.xml w folderze read-d2c-messages i dodaj następującą zależność do węzła **zależności**. Ta zależność umożliwia użycie pakietu eventhubs-client w aplikacji do odczytywania z punktu końcowego zgodnego z centrum zdarzeń:

    ```xml
    <dependency> 
        <groupId>com.microsoft.azure</groupId> 
        <artifactId>azure-eventhubs</artifactId> 
        <version>0.15.0</version> 
    </dependency>
    ```

4. Zapisz i zamknij plik pom.xml.

5. Za pomocą edytora tekstów otwórz plik read-d2c-messages\src\main\java\com\mycompany\app\App.java.

6. Dodaj do pliku następujące instrukcje **importowania**:

    ```java
    import java.io.IOException;
    import com.microsoft.azure.eventhubs.*;

    import java.nio.charset.Charset;
    import java.time.*;
    import java.util.function.*;
    ```

7. Dodaj następującą zmienną na poziomie klasy do klasy **App**. Zastąp ciągi **{youriothubkey}**, **{youreventhubcompatibleendpoint}** i **{youreventhubcompatiblename}** wartościami zanotowanymi wcześniej:

    ```java
    private static String connStr = "Endpoint={youreventhubcompatibleendpoint};EntityPath={youreventhubcompatiblename};SharedAccessKeyName=iothubowner;SharedAccessKey={youriothubkey}";
    ```

8. Dodaj następującą metodę **receiveMessages** do klasy **App**. Ta metoda tworzy wystąpienie **EventHubClient** do nawiązywania połączenia z punktem końcowym zgodnym z centrum zdarzeń, a następnie tworzy asynchronicznie wystąpienie **PartitionReceiver** do odczytywania z partycji centrum zdarzeń. Działa w sposób ciągły w pętli i drukuje szczegóły komunikatu aż do zakończenia aplikacji.

    ```java
    // Create a receiver on a partition.
    private static EventHubClient receiveMessages(final String partitionId) {
      EventHubClient client = null;
      try {
        client = EventHubClient.createFromConnectionStringSync(connStr);
      } catch (Exception e) {
        System.out.println("Failed to create client: " + e.getMessage());
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
                    System.out.println("Got some events");
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
                System.out.println("Failed to receive messages: " + e.getMessage());
              }
            }
          });
        } catch (Exception e) {
          System.out.println("Failed to create receiver: " + e.getMessage());
      }
      return client;
    }
    ```

   > [!NOTE]
   > Ta metoda używa filtru podczas tworzenia odbiornika, więc odbiornik odczytuje tylko komunikaty wysyłane do usługi IoT Hub po uruchomieniu odbiornika. Ta technika jest przydatna w środowisku testowym, gdyż dzięki niej jest wyświetlany bieżący zestaw komunikatów. W środowisku produkcyjnym kod powinien sprawdzać, czy są przetwarzane wszystkie komunikaty — więcej informacji znajduje się w samouczku [How to process IoT Hub device-to-cloud messages][lnk-process-d2c-tutorial] (Jak przetwarzać komunikaty z urządzenia do chmury w usłudze IoT Hub).

9. Zmodyfikuj podpis metody **main**, aby uwzględnić poniższy wyjątek:

    ```java
    public static void main( String[] args ) throws IOException
    ```

10. Dodaj następujący kod do metody **głównej** w klasie **App**. Ten kod tworzy dwa wystąpienia **EventHubClient** i **PartitionReceiver** wystąpień i umożliwia zamknięcie aplikacji po zakończeniu przetwarzania komunikatów:

    ```java
    // Create receivers for partitions 0 and 1.
    EventHubClient client0 = receiveMessages("0");
    EventHubClient client1 = receiveMessages("1");
    System.out.println("Press ENTER to exit.");
    System.in.read();
    try {
      client0.closeSync();
      client1.closeSync();
      System.exit(0);
    } catch (Exception e) {
      System.exit(1);
    }
    ```

    > [!NOTE]
    > W przypadku tego kodu przyjmuje się założenie, że usługa IoT Hub została utworzona w (bezpłatnej) warstwie F1. Bezpłatne centrum IoT ma dwie partycje o nazwie „0” i „1”.

11. Zapisz i zamknij plik App.java.

12. Aby utworzyć aplikację **read-d2c-messages** przy użyciu narzędzia Maven, wykonaj następujące polecenie w wierszu polecenia w folderze read-d2c-messages:

    ```cmd/sh
    mvn clean package -DskipTests
    ```

## <a name="create-a-device-app"></a>Tworzenie aplikacji urządzenia
Ta sekcja zawiera instrukcje dotyczące tworzenia aplikacji konsolowej Java, która symuluje urządzenie wysyłające komunikaty z urządzenia do chmury do usługi IoT Hub.

1. W folderze iot-java-get-started utworzonym w sekcji *Tworzenie tożsamości urządzenia* utwórz projekt narzędzia Maven o nazwie **simulated-device** przy użyciu następującego polecenia w wierszu polecenia. Zwróć uwagę, że jest to jedno długie polecenie:

    ```cmd/sh
    mvn archetype:generate -DgroupId=com.mycompany.app -DartifactId=simulated-device -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false
    ```

2. W wierszu polecenia przejdź do folderu simulated-device.

3. Za pomocą edytora tekstów otwórz plik pom.xml w folderze simulated-device i dodaj następujące zależności do węzła **zależności**. Ta zależność umożliwia użycie pakietu iothub-java-client w aplikacji do komunikowania się z centrum IoT Hub i serializacji obiektów Java do formatu JSON:

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
    > Możesz sprawdzić dostępność najnowszej wersji pakietu **iot-device-client** za pomocą [funkcji wyszukiwania narzędzia Maven][lnk-maven-device-search].

4. Zapisz i zamknij plik pom.xml.

5. Za pomocą edytora tekstów otwórz plik simulated-device\src\main\java\com\mycompany\app\App.java.

6. Dodaj do pliku następujące instrukcje **importowania**:

    ```java
    import com.microsoft.azure.sdk.iot.device.*;
    import com.google.gson.Gson;

    import java.io.*;
    import java.net.URISyntaxException;
    import java.util.Random;
    import java.util.concurrent.Executors;
    import java.util.concurrent.ExecutorService;
    ```

7. Dodaj następujące zmienne na poziomie klasy do klasy **App**. Zastąp wartość **{youriothubname}** nazwą centrum IoT Hub, a **{yourdevicekey}** wartością klucza urządzenia wygenerowaną w sekcji *Tworzenie tożsamości urządzenia*:

    ```java
    private static String connString = "HostName={youriothubname}.azure-devices.net;DeviceId=myFirstJavaDevice;SharedAccessKey={yourdevicekey}";
    private static IotHubClientProtocol protocol = IotHubClientProtocol.MQTT;
    private static String deviceId = "myFirstJavaDevice";
    private static DeviceClient client;
    ```
   
    Ta przykładowa aplikacja używa zmiennej **protocol** podczas tworzenia wystąpienia obiektu **DeviceClient**. Do komunikacji z usługą IoT Hub możesz użyć protokołu MQTT, AMQP lub HTTPS.

8. Dodaj następującą zagnieżdżoną klasę **TelemetryDataPoint** do wnętrza klasy **App**, aby określić dane telemetryczne wysyłane przez urządzenie do centrum IoT:

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
9. Dodaj następującą zagnieżdżoną klasę **EventCallback** wewnątrz klasy **App**, aby wyświetlić stan potwierdzenia zwracany przez centrum IoT Hub podczas przetwarzania komunikatu z aplikacji urządzenia. Ta metoda powiadamia również wątek główny w aplikacji o przetworzeniu komunikatu:
   
    ```java
    private static class EventCallback implements IotHubEventCallback {
      public void execute(IotHubStatusCode status, Object context) {
        System.out.println("IoT Hub responded to message with status: " + status.name());
   
        if (context != null) {
          synchronized (context) {
            context.notify();
          }
        }
      }
    }
    ```

10. Dodaj następującą zagnieżdżoną klasę **MessageSender** do klasy **App**. Metoda **run** w tej klasie generuje przykładowe dane telemetrii do wysłania do centrum IoT i oczekuje na potwierdzenie przed wysłaniem nowego komunikatu:

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

    Ta metoda wysyła nowy komunikat z urządzenia do chmury sekundę po potwierdzeniu poprzedniego komunikatu przez centrum IoT. Komunikat zawiera obiekt serializacji JSON z identyfikatorem urządzenia i generowanymi losowo numerami do symulacji czujników temperatury i wilgotności.

11. Zastąp metodę **main** następującym kodem, który tworzy wątek do wysyłania komunikatów z urządzenia do chmury do centrum IoT:

    ```java
    public static void main( String[] args ) throws IOException, URISyntaxException {
      client = new DeviceClient(connString, protocol);
      client.open();
    
      MessageSender sender = new MessageSender();
    
      ExecutorService executor = Executors.newFixedThreadPool(1);
      executor.execute(sender);
    
      System.out.println("Press ENTER to exit.");
      System.in.read();
      executor.shutdownNow();
      client.closeNow();
    }
    ```

12. Zapisz i zamknij plik App.java.

13. Aby utworzyć aplikację **simulated-device** przy użyciu narzędzia Maven, wykonaj następujące polecenie w wierszu polecenia w folderze simulated-device:

    ```cmd/sh
    mvn clean package -DskipTests
    ```

> [!NOTE]
> Dla uproszczenia ten samouczek nie zawiera opisu wdrożenia żadnych zasad ponawiania. W kodzie produkcyjnym należy wdrożyć zasady ponawiania (np. wycofywanie wykładnicze) zgodnie z sugestią w artykule z witryny MSDN [Transient Fault Handling][lnk-transient-faults] (Obsługa przejściowych błędów).

## <a name="run-the-apps"></a>Uruchamianie aplikacji

Teraz można przystąpić do uruchomienia aplikacji.

1. Z poziomu wiersza polecenia w folderze read-d2c uruchom następujące polecenie, aby rozpocząć monitorowanie pierwszej partycji centrum IoT:

    ```cmd/sh
    mvn exec:java -Dexec.mainClass="com.mycompany.app.App"
    ```

    ![Aplikacja usługi IoT Hub dla środowiska Java do monitorowania komunikatów wysyłanych z urządzenia do chmury][7]

2. Z poziomu wiersza polecenia w folderze simulated-device uruchom następujące polecenie, aby rozpocząć wysyłanie danych telemetrycznych do centrum IoT:

    ```cmd/sh
    mvn exec:java -Dexec.mainClass="com.mycompany.app.App" 
    ```

    ![Aplikacja urządzenia usługi IoT Hub dla środowiska Java do monitorowania komunikatów wysyłanych z urządzenia do chmury][8]

3. Na kafelku **Użycie** w [witrynie Azure Portal][lnk-portal] wyświetlana jest liczba komunikatów wysłanych do centrum IoT:

    ![Kafelek Użycie witryny Azure Portal przedstawiający liczbę komunikatów wysłanych do usługi IoT Hub][43]

## <a name="next-steps"></a>Następne kroki
W tym samouczku opisano konfigurowanie nowego centrum IoT Hub w witrynie Azure Portal, a następnie tworzenie tożsamości urządzenia w rejestrze tożsamości centrum. Tożsamość urządzenia została użyta, aby włączyć w aplikacji urządzenia funkcję wysyłania komunikatów z urządzenia do chmury do centrum IoT Hub. Utworzono również aplikację, która wyświetla komunikaty odbierane przez centrum IoT Hub.

Aby kontynuować wprowadzenie do usługi IoT Hub i zapoznać się z innymi scenariuszami IoT, zobacz:

* [Łączenie urządzenia][lnk-connect-device]
* [Wprowadzenie do zarządzania urządzeniami][lnk-device-management]
* [Getting started with Azure IoT Edge][lnk-iot-edge] (Rozpoczynanie pracy z usługą Azure IoT Edge)

Aby dowiedzieć się, jak rozszerzyć rozwiązanie IoT i przetwarzać komunikaty z urządzenia do chmury na dużą skalę, zobacz samouczek [Przetwarzanie komunikatów przesyłanych z urządzeń do chmury][lnk-process-d2c-tutorial].
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
[lnk-iot-edge]: ../iot-edge/tutorial-simulate-device-linux.md
[lnk-connect-device]: https://azure.microsoft.com/develop/iot/
[lnk-maven-service-search]: http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22iot-service-client%22%20g%3A%22com.microsoft.azure.sdk.iot%22
[lnk-maven-device-search]: http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22iot-device-client%22%20g%3A%22com.microsoft.azure.sdk.iot%22
[lnk-maven-eventhubs-search]: http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22azure-eventhubs%22
