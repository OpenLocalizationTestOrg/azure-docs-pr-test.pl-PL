---
title: "aaaGet wprowadzenie do zarządzania urządzeniami Centrum IoT Azure (Java) | Dokumentacja firmy Microsoft"
description: "Jak tooinitiate zarządzania urządzenia Azure IoT Hub toouse urządzenie zdalne ponowny rozruch. Możesz używać urządzenia Azure IoT hello zestawu SDK dla języka Java tooimplement aplikacji symulowane urządzenie, która obejmuje metoda bezpośrednia i hello Azure IoT usługi SDK dla języka Java tooimplement usługi aplikacji, która wywołuje metodę bezpośredniego hello."
services: iot-hub
documentationcenter: .java
author: dominicbetts
manager: timlt
editor: 
ms.service: iot-hub
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/08/2017
ms.author: dobett
ms.openlocfilehash: 7aaeda9d4ff7002e5c66adfd61e2dfd5bcea964f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-device-management-java"></a>Wprowadzenie do zarządzania urządzeniami (Java)

[!INCLUDE [iot-hub-selector-dm-getstarted](../../includes/iot-hub-selector-dm-getstarted.md)]

Ten samouczek przedstawia sposób wykonania następujących czynności:

* Użyj hello toocreate portalu Azure IoT Hub i Utwórz tożsamość urządzenia w Centrum IoT.
* Utwórz aplikację symulowane urządzenie, która implementuje urządzenie hello tooreboot metoda bezpośrednia. Bezpośrednie metody są wywoływane z hello chmury.
* Utwórz aplikację, która wywołuje metodę hello ponowny rozruch bezpośrednio w aplikacji symulowane urządzenie hello za pośrednictwem Centrum IoT. Tej aplikacji, a następnie hello zgłoszone właściwości z hello toosee urządzeń po zakończeniu operacji ponownego rozruchu hello monitorów.

Na końcu hello tego samouczka znajdują się dwie aplikacje konsoli Java:

**Symulowane urządzenie**. Ta aplikacja:

* Centrum IoT tooyour łączy się z usługą tożsamości urządzenia hello utworzony wcześniej.
* Odbiera wywołanie metody bezpośredniego ponowne uruchomienie komputera.
* Symuluje ponowny rozruch komputera fizycznego.
* Raporty hello czasu ostatniego ponownego uruchomienia hello za pośrednictwem właściwości zgłoszony.

**ponowne uruchomienie wyzwalacza**. Ta aplikacja:

* Wywołuje metodę bezpośrednio w aplikacji symulowane urządzenie hello.
* Wyświetla hello odpowiedzi toohello wywołanie metody bezpośredniego wysyłane przez hello symulowane urządzenie
* Wyświetla hello zaktualizowane zgłosił właściwości.

> [!NOTE]
> Informacje hello zestawów SDK, której można toobuild toorun aplikacji na urządzeniach i z zaplecza rozwiązania, zobacz [Azure IoT SDK][lnk-hub-sdks].

toocomplete tego samouczka należy:

* Java SE 8. <br/> [Przygotowywanie środowiska projektowego] [ lnk-dev-setup] w tym artykule opisano sposób tooinstall Java w tym samouczku w systemie Windows lub Linux.
* Maven 3.  <br/> [Przygotowywanie środowiska projektowego] [ lnk-dev-setup] w tym artykule opisano sposób tooinstall [Maven] [ lnk-maven] ten samouczek dotyczący systemu Windows lub Linux.
* [Środowisko node.js w wersji 0.10.0 lub nowszym](http://nodejs.org).

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity](../../includes/iot-hub-get-started-create-device-identity.md)]

## <a name="trigger-a-remote-reboot-on-hello-device-using-a-direct-method"></a>Wyzwalacz zdalnego ponownego uruchomienia na urządzeniu hello za pomocą bezpośrednich — metoda

W tej sekcji tworzenia aplikacji konsoli Java który:

1. Wywołuje metodę bezpośredniego ponowny rozruch hello w hello symulowane urządzenie aplikacji.
1. Wyświetla hello odpowiedzi.
1. Ankiety hello zgłosił przesyłanych z hello toodetermine urządzeń po zakończeniu ponownego rozruchu hello właściwości.

Ta aplikacja konsoli łączy tooyour Centrum IoT metoda bezpośrednia hello tooinvoke i hello odczytu zgłoszone właściwości.

1. Utwórz pusty folder o nazwie dm-get-started.

1. W folderze dm-get-started hello Utwórz projekt Maven o nazwie **ponowne uruchomienie wyzwalacza** przy użyciu hello następujące polecenie z wiersza polecenia. Oto Hello polecenia jednej, długi:

    `mvn archetype:generate -DgroupId=com.mycompany.app -DartifactId=trigger-reboot -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false`

1. Wierszu polecenia przejdź toohello ponowne uruchomienie wyzwalacza folderu.

1. Za pomocą edytora tekstu, otwórz plik pom.xml hello w folderze ponowne uruchomienie wyzwalacza hello i dodaj następujące zależności toohello hello **zależności** węzła. Ta zależność umożliwia możesz toouse hello iot usługi klienta pakietu w Twojej toocommunicate aplikacji z Centrum IoT:

    ```xml
    <dependency>
      <groupId>com.microsoft.azure.sdk.iot</groupId>
      <artifactId>iot-service-client</artifactId>
      <version>1.7.23</version>
      <type>jar</type>
    </dependency>
    ```

    > [!NOTE]
    > Możesz sprawdzić hello najnowszą wersję **klienta w przypadku usługi iot** przy użyciu [wyszukiwania Maven][lnk-maven-service-search].

1. Dodaj następujące hello **kompilacji** węzła po hello **zależności** węzła. Ta konfiguracja powoduje, że Maven toouse Java 1,8 toobuild hello aplikacji:

    ```xml
    <build>
      <plugins>
        <plugin>
          <groupId>org.apache.maven.plugins</groupId>
          <artifactId>maven-compiler-plugin</artifactId>
          <version>3.3</version>
          <configuration>
            <source>1.8</source>
            <target>1.8</target>
          </configuration>
        </plugin>
      </plugins>
    </build>
    ```

1. Zapisz i zamknij plik pom.xml hello.

1. Za pomocą edytora tekstu, otwórz plik źródłowy trigger-reboot\src\main\java\com\mycompany\app\App.java hello.

1. Dodaj następujące hello **zaimportować** instrukcje toohello pliku:

    ```java
    import com.microsoft.azure.sdk.iot.service.devicetwin.DeviceMethod;
    import com.microsoft.azure.sdk.iot.service.devicetwin.MethodResult;
    import com.microsoft.azure.sdk.iot.service.exceptions.IotHubException;
    import com.microsoft.azure.sdk.iot.service.devicetwin.DeviceTwin;
    import com.microsoft.azure.sdk.iot.service.devicetwin.DeviceTwinDevice;

    import java.io.IOException;
    import java.util.concurrent.TimeUnit;
    import java.util.concurrent.Executors;
    import java.util.concurrent.ExecutorService;
    ```

1. Dodaj następujące zmienne klasy toohello hello **aplikacji** klasy. Zastąp `{youriothubconnectionstring}` z parametrów połączenia Centrum IoT zanotowaną w hello *tworzenia Centrum IoT* sekcji:

    ```java
    public static final String iotHubConnectionString = "{youriothubconnectionstring}";
    public static final String deviceId = "myDeviceId";

    private static final String methodName = "reboot";
    private static final Long responseTimeout = TimeUnit.SECONDS.toSeconds(30);
    private static final Long connectTimeout = TimeUnit.SECONDS.toSeconds(5);
    ```

1. tooimplement wątku, który odczytuje hello zgłosił właściwości z dwie urządzenia hello co 10 sekund, Dodaj hello zagnieżdżona klasa toohello **aplikacji** klasy:

    ```java
    private static class ShowReportedProperties implements Runnable {
      public void run() {
        try {
          DeviceTwin deviceTwins = DeviceTwin.createFromConnectionString(iotHubConnectionString);
          DeviceTwinDevice twinDevice = new DeviceTwinDevice(deviceId);
          while (true) {
            System.out.println("Get reported properties from device twin");
            deviceTwins.getTwin(twinDevice);
            System.out.println(twinDevice.reportedPropertiesToString());
            Thread.sleep(10000);
          }
        } catch (Exception ex) {
          System.out.println("Exception reading reported properties: " + ex.getMessage());
        }
      }
    }
    ```

1. Metoda bezpośrednia ponowny rozruch hello tooinvoke na powitania symulowane urządzenie, Dodaj hello następującego kodu toohello **głównego** metody:

    ```java
    System.out.println("Starting sample...");
    DeviceMethod methodClient = DeviceMethod.createFromConnectionString(iotHubConnectionString);

    try
    {
      System.out.println("Invoke reboot direct method");
      MethodResult result = methodClient.invoke(deviceId, methodName, responseTimeout, connectTimeout, null);

      if(result == null)
      {
        throw new IOException("Invoke direct method reboot returns null");
      }
      System.out.println("Invoked reboot on device");
      System.out.println("Status for device:   " + result.getStatus());
      System.out.println("Message from device: " + result.getPayload());
    }
    catch (IotHubException e)
    {
        System.out.println(e.getMessage());
    }
    ```

1. toostart hello wątku toopoll hello zgłoszone właściwości z hello symulowane urządzenie, należy dodać hello następującego kodu toohello **głównego** metody:

    ```java
    ShowReportedProperties showReportedProperties = new ShowReportedProperties();
    ExecutorService executor = Executors.newFixedThreadPool(1);
    executor.execute(showReportedProperties);
    ```

1. tooenable toostop hello aplikacji, Dodaj hello następującego kodu toohello **głównego** metody:

    ```java
    System.out.println("Press ENTER tooexit.");
    System.in.read();
    executor.shutdownNow();
    System.out.println("Shutting down sample...");
    ```

1. Zapisz i zamknij plik trigger-reboot\src\main\java\com\mycompany\app\App.java hello.

1. Tworzenie hello **ponowne uruchomienie wyzwalacza** aplikacji zaplecza i poprawić błędy. Wierszu polecenia przejdź toohello ponowne uruchomienie wyzwalacza folder i hello uruchom następujące polecenie:

    `mvn clean package -DskipTests`

## <a name="create-a-simulated-device-app"></a>Tworzenie aplikacji symulowanego urządzenia

W tej sekcji utworzysz aplikację konsoli języka Java, która symuluje urządzenia. Aplikacja Hello nasłuchuje wywołanie metody bezpośredniego ponowny rozruch hello z Centrum IoT i natychmiast odpowiada toothat wywołania. Witaj aplikacji, a następnie sen jakiś czas toosimulate hello ponowne uruchomienie procesu przed użyciem hello toonotify zgłoszone właściwości **ponowne uruchomienie wyzwalacza** zaplecza aplikacji hello ponowne uruchomienie zostało ukończone.

1. W folderze dm-get-started hello Utwórz projekt Maven o nazwie **symulowane urządzenie** przy użyciu hello następujące polecenie z wiersza polecenia. następujące Hello jest poleceniem jednej, długi:

    `mvn archetype:generate -DgroupId=com.mycompany.app -DartifactId=simulated-device -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false`

1. Wierszu polecenia przejdź toohello symulowane urządzenie folderu.

1. Za pomocą edytora tekstu, otwórz plik pom.xml hello w folderze symulowane urządzenie hello i dodaj następujące zależności toohello hello **zależności** węzła. Ta zależność umożliwia możesz toouse hello iot usługi klienta pakietu w Twojej toocommunicate aplikacji z Centrum IoT:

    ```xml
    <dependency>
      <groupId>com.microsoft.azure.sdk.iot</groupId>
      <artifactId>iot-device-client</artifactId>
      <version>1.3.32</version>
    </dependency>
    ```

    > [!NOTE]
    > Możesz sprawdzić hello najnowszą wersję **klienta w przypadku urządzenia iot** przy użyciu [wyszukiwania Maven][lnk-maven-device-search].

1. Dodaj następujące hello **kompilacji** węzła po hello **zależności** węzła. Ta konfiguracja powoduje, że Maven toouse Java 1,8 toobuild hello aplikacji:

    ```xml
    <build>
      <plugins>
        <plugin>
          <groupId>org.apache.maven.plugins</groupId>
          <artifactId>maven-compiler-plugin</artifactId>
          <version>3.3</version>
          <configuration>
            <source>1.8</source>
            <target>1.8</target>
          </configuration>
        </plugin>
      </plugins>
    </build>
    ```

1. Zapisz i zamknij plik pom.xml hello.

1. Za pomocą edytora tekstu, otwórz plik źródłowy simulated-device\src\main\java\com\mycompany\app\App.java hello.

1. Dodaj następujące hello **zaimportować** instrukcje toohello pliku:

    ```java
    import com.microsoft.azure.sdk.iot.device.*;
    import com.microsoft.azure.sdk.iot.device.DeviceTwin.*;

    import java.io.IOException;
    import java.net.URISyntaxException;
    import java.time.LocalDateTime;
    import java.util.Scanner;
    import java.util.Set;
    import java.util.HashSet;
    ```

1. Dodaj następujące zmienne klasy toohello hello **aplikacji** klasy. Zastąp `{yourdeviceconnectionstring}` przy użyciu parametrów połączenia urządzenia hello zanotowaną w hello *tworzenie tożsamości urządzenia* sekcji:

    ```java
    private static final int METHOD_SUCCESS = 200;
    private static final int METHOD_NOT_DEFINED = 404;

    private static IotHubClientProtocol protocol = IotHubClientProtocol.MQTT;
    private static String connString = "{yourdeviceconnectionstring}";
    private static DeviceClient client;
    ```

1. tooimplement obsługi wywołania zwrotnego, metoda bezpośrednia zdarzeń stanu, Dodaj następujące hello zagnieżdżona klasa toohello **aplikacji** klasy:

    ```java
    protected static class DirectMethodStatusCallback implements IotHubEventCallback
    {
      public void execute(IotHubStatusCode status, Object context)
      {
        System.out.println("IoT Hub responded toodevice method operation with status " + status.name());
      }
    }
    ```

1. tooimplement obsługi wywołania zwrotnego dla zdarzeń urządzenia dwie stanu, Dodaj następujące hello zagnieżdżona klasa toohello **aplikacji** klasy:

    ```java
    protected static class DeviceTwinStatusCallback implements IotHubEventCallback
    {
        public void execute(IotHubStatusCode status, Object context)
        {
            System.out.println("IoT Hub responded toodevice twin operation with status " + status.name());
        }
    }
    ```

1. tooimplement obsługi wywołania zwrotnego dla właściwości zdarzenia, Dodaj następujące hello zagnieżdżona klasa toohello **aplikacji** klasy:

    ```java
    protected static class PropertyCallback implements PropertyCallBack<String, String>
    {
      public void PropertyCall(String propertyKey, String propertyValue, Object context)
      {
        System.out.println("PropertyKey:     " + propertyKey);
        System.out.println("PropertyKvalue:  " + propertyKey);
      }
    }
    ```

1. tooimplement wątku toosimulate hello urządzenia ponownego uruchomienia komputera, Dodaj następujące hello zagnieżdżona klasa toohello **aplikacji** klasy. Wątek Hello zostanie uśpiony na pięć sekund, a następnie ustawia hello **lastReboot** zgłoszonych właściwości:

    ```java
    protected static class RebootDeviceThread implements Runnable {
      public void run() {
        try {
          System.out.println("Rebooting...");
          Thread.sleep(5000);
          Property property = new Property("lastReboot", LocalDateTime.now());
          Set<Property> properties = new HashSet<Property>();
          properties.add(property);
          client.sendReportedProperties(properties);
          System.out.println("Rebooted");
        }
        catch (Exception ex) {
          System.out.println("Exception in reboot thread: " + ex.getMessage());
        }
      }
    }
    ```

1. Metoda bezpośrednia hello tooimplement na urządzeniu hello, Dodaj następujące hello zagnieżdżona klasa toohello **aplikacji** klasy. Gdy aplikacja symulowane hello odbiera toohello wywołania **ponowny rozruch** metoda bezpośrednia zwraca obiekt wywołujący toohello potwierdzenia i następnie uruchamia hello tooprocess wątku ponownego rozruchu:

    ```java
    protected static class DirectMethodCallback implements com.microsoft.azure.sdk.iot.device.DeviceTwin.DeviceMethodCallback
    {
      @Override
      public DeviceMethodData call(String methodName, Object methodData, Object context)
      {
        DeviceMethodData deviceMethodData;
        switch (methodName)
        {
          case "reboot" :
          {
            int status = METHOD_SUCCESS;
            System.out.println("Received reboot request");
            deviceMethodData = new DeviceMethodData(status, "Started reboot");
            RebootDeviceThread rebootThread = new RebootDeviceThread();
            Thread t = new Thread(rebootThread);
            t.start();
            break;
          }
          default:
          {
            int status = METHOD_NOT_DEFINED;
            deviceMethodData = new DeviceMethodData(status, "Not defined direct method " + methodName);
          }
        }
        return deviceMethodData;
      }
    }
    ```

1. Modyfikowanie hello podpis hello **głównego** hello toothrow metody następujące wyjątki:

    ```java
    public static void main(String[] args) throws IOException, URISyntaxException
    ```

1. tooinstantiate **DeviceClient**, Dodaj hello następującego kodu toohello **głównego** metody:

    ```java
    System.out.println("Starting device client sample...");
    client = new DeviceClient(connString, protocol);
    ```

1. toostart nasłuchiwania dla wywołań metod bezpośrednie dodawanie hello następującego kodu toohello **głównego** metody:

    ```java
    try
    {
      client.open();
      client.subscribeToDeviceMethod(new DirectMethodCallback(), null, new DirectMethodStatusCallback(), null);
      client.startDeviceTwin(new DeviceTwinStatusCallback(), null, new PropertyCallback(), null);
      System.out.println("Subscribed toodirect methods and polling for reported properties. Waiting...");
    }
    catch (Exception e)
    {
      System.out.println("On exception, shutting down \n" + " Cause: " + e.getCause() + " \n" +  e.getMessage());
      client.close();
      System.out.println("Shutting down...");
    }
    ```

1. tooshut dół hello symulator urządzeń, Dodaj hello następującego kodu toohello **głównego** metody:

    ```java
    System.out.println("Press any key tooexit...");
    Scanner scanner = new Scanner(System.in);
    scanner.nextLine();
    scanner.close();
    client.close();
    System.out.println("Shutting down...");
    ```

1. Zapisz i zamknij plik simulated-device\src\main\java\com\mycompany\app\App.java hello.

1. Tworzenie hello **symulowane urządzenie** aplikacji zaplecza i poprawić błędy. Wierszu polecenia przejdź folder symulowane urządzenie toohello i hello uruchom następujące polecenie:

    `mvn clean package -DskipTests`

## <a name="run-hello-apps"></a>Uruchamianie aplikacji hello

Wszystko jest teraz gotowy toorun hello aplikacji.

1. W wierszu polecenia w folderze symulowane urządzenie hello uruchom następujące polecenia toobegin nasłuchiwania dla wywołań metod ponowny rozruch z Centrum IoT hello:

    `mvn exec:java -Dexec.mainClass="com.mycompany.app.App"`

    ![Centrum IoT Java symulowane urządzenie toolisten aplikacji dla wywołań metod bezpośredniego ponowny rozruch][1]

1. W wierszu polecenia w folderze ponowne uruchomienie wyzwalacza hello Uruchom hello, wykonując polecenie toocall hello ponowny rozruch metody na symulowane urządzenie z Centrum IoT:

    `mvn exec:java -Dexec.mainClass="com.mycompany.app.App"`

    ![Centrum IoT Java usługi aplikacji toocall hello ponowny rozruch direct — metoda][2]

1. Symulowane urządzenie Hello odpowiada wywołanie metody bezpośredniego ponowny rozruch toohello:

    ![Wywołanie metody bezpośredniego toohello odpowiada aplikacji symulowane urządzenie Java Centrum IoT][3]

[!INCLUDE [iot-hub-dm-followup](../../includes/iot-hub-dm-followup.md)]

<!-- images and links -->
[1]: ./media/iot-hub-java-java-device-management-getstarted/launchsimulator.png
[2]: ./media/iot-hub-java-java-device-management-getstarted/triggerreboot.png
[3]: ./media/iot-hub-java-java-device-management-getstarted/respondtoreboot.png
<!-- Links -->

[lnk-maven]: https://maven.apache.org/what-is-maven.html

[lnk-dev-setup]: https://github.com/Azure/azure-iot-sdk-java/blob/master/doc/java-devbox-setup.md

[lnk-hub-sdks]: iot-hub-devguide-sdks.md

[lnk-maven-service-search]: http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22iot-service-client%22%20g%3A%22com.microsoft.azure.sdk.iot%22
[lnk-maven-device-search]: http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22iot-device-client%22%20g%3A%22com.microsoft.azure.sdk.iot%22