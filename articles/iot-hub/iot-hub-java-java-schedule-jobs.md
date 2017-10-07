---
title: zadania aaaSchedule z Centrum IoT Azure (Java) | Dokumentacja firmy Microsoft
description: "Jak tooschedule Centrum IoT Azure zadania tooinvoke metoda bezpośrednia i ustaw odpowiednie właściwości na wielu urządzeniach. Możesz używać urządzenia Azure IoT hello zestawu SDK dla języka Java tooimplement hello symulowane urządzenie aplikacji i hello Azure IoT usługa zestawu SDK dla języka Java tooimplement zadania hello toorun aplikacji usługi."
services: iot-hub
documentationcenter: java
author: dominicbetts
manager: timlt
editor: 
ms.service: iot-hub
ms.devlang: java
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/10/2017
ms.author: dobett
ms.openlocfilehash: b1b05fa56c3ce96af0b33d4cca0dd54da0f4e927
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="schedule-and-broadcast-jobs-java"></a>Zadania harmonogramu i emisji (Java)

[!INCLUDE [iot-hub-selector-schedule-jobs](../../includes/iot-hub-selector-schedule-jobs.md)]

Użyj Centrum IoT Azure tooschedule i Śledź zadań aktualizowanych milionów urządzeń. Należy użyć zadania, aby:

* Aktualizowanie żądanych właściwości
* Tagi aktualizacji
* Wywołanie metody bezpośredniego

Zadanie opakowuje jedną z następujących czynności i śledzi hello wykonywania z zestawem urządzeń. Zapytanie dwie urządzenia definiuje hello zbiór urządzeń, które wykonuje zadanie hello przed. Na przykład aplikacji zaplecza można użyć zadania tooinvoke metoda bezpośrednia na 10 000 urządzeń, które wykonuje ponowny rozruch hello urządzeń. Określ zestaw hello urządzeń za pomocą kwerendy dwie urządzenia i zaplanować hello toorun zadania w przyszłości. postęp śledzi zadania Hello jako każdego urządzenia hello odbierania i wykonaj metoda bezpośrednia hello ponowne uruchomienie komputera.

toolearn więcej informacji na temat każdego z tych funkcji, zobacz:

* Dwie urządzeń i właściwości: [wprowadzenie twins urządzenia](iot-hub-java-java-twin-getstarted.md)
* Bezpośrednie metody: [przewodnik dewelopera Centrum IoT — metody bezpośredniego](iot-hub-devguide-direct-methods.md) i [samouczek: bezpośrednie metody](iot-hub-java-java-direct-methods.md)

Ten samouczek przedstawia sposób wykonania następujących czynności:

* Tworzenie aplikacji urządzenia implementujący bezpośredniego metodę o nazwie **lockDoor**. Aplikacja urządzenia Hello również odbiera zmiany żądanej właściwości z hello zaplecza aplikacji.
* Tworzenie aplikacji zaplecza, która tworzy hello toocall zadania **lockDoor** metoda bezpośrednia na wielu urządzeniach. Inne zadanie wysyła żądanej właściwości aktualizuje toomultiple urządzeń.

Na końcu hello tego samouczka masz urządzenie aplikację konsoli języka java i zaplecza aplikacji konsoli java:

**Symulowane urządzenie** który łączy Centrum IoT tooyour, implementuje hello **lockDoor** bezpośrednie — metoda i uchwytów potrzebne zmiany właściwości.

**Harmonogram zadań** wykorzystujące hello toocall zadania **lockDoor** właściwości na wielu urządzeniach potrzeby bezpośredniego metoda i aktualizacji dwie hello w urządzeniu.

> [!NOTE]
> Artykuł Hello [Azure IoT SDK](iot-hub-devguide-sdks.md) informacje na temat hello Azure IoT SDK służy toobuild zarówno urządzenia, jak i zaplecza aplikacji.

## <a name="prerequisites"></a>Wymagania wstępne

toocomplete tego samouczka należy:

* Witaj najnowszych [Java SE Development Kit 8](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)
* [Maven 3](https://maven.apache.org/install.html)
* Aktywne konto platformy Azure. (Jeśli nie masz konta, możesz utworzyć [bezpłatne konto](http://azure.microsoft.com/pricing/free-trial/) w zaledwie kilka minut.)

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity-portal](../../includes/iot-hub-get-started-create-device-identity-portal.md)]

Jeśli wolisz tożsamości urządzenia hello toocreate programowo, przeczytaj hello odpowiedniej sekcji w hello [połączenia przy użyciu języka Java Centrum IoT urządzenia tooyour](iot-hub-java-java-getstarted.md#create-a-device-identity) artykułu. Można również użyć hello [explorer Centrum iothub](https://github.com/Azure/iothub-explorer) tooadd narzędzia Centrum IoT tooyour urządzenia.

## <a name="create-hello-service-app"></a>Tworzenie aplikacji usługi hello

W tej sekcji służy do tworzenia aplikacji konsoli Java, który używa zadań:

* Wywołaj hello **lockDoor** metoda bezpośrednia na wielu urządzeniach.
* Wyślij odpowiednie właściwości toomultiple urządzeń.

Aplikacja hello toocreate:

1. Na komputerze deweloperskim, należy utworzyć pusty folder o nazwie `iot-java-schedule-jobs`.

1. W hello `iot-java-schedule-jobs` folderu, Utwórz projekt Maven o nazwie **harmonogram zadań** przy użyciu hello następujące polecenie z wiersza polecenia. Zwróć uwagę, że jest to jedno długie polecenie:

    `mvn archetype:generate -DgroupId=com.mycompany.app -DartifactId=schedule-jobs -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false`

1. Wierszu polecenia przejdź toohello `schedule-jobs` folderu.

1. Za pomocą edytora tekstu, otwórz hello `pom.xml` pliku w hello `schedule-jobs` folderu i dodaj następujące zależności toohello hello **zależności** węzła. Ta zależność umożliwia toouse hello **klienta w przypadku usługi iot** pakiet w Twojej toocommunicate aplikacji z Centrum IoT:

    ```xml
    <dependency>
      <groupId>com.microsoft.azure.sdk.iot</groupId>
      <artifactId>iot-service-client</artifactId>
      <version>1.7.23</version>
      <type>jar</type>
    </dependency>
    ```

    > [!NOTE]
    > Możesz sprawdzić hello najnowszą wersję **klienta w przypadku usługi iot** przy użyciu [wyszukiwania Maven](http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22iot-service-client%22%20g%3A%22com.microsoft.azure.sdk.iot%22).

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

1. Zapisz i zamknij hello `pom.xml` pliku.

1. Za pomocą edytora tekstu, otwórz hello `schedule-jobs\src\main\java\com\mycompany\app\App.java` pliku.

1. Dodaj następujące hello **zaimportować** instrukcje toohello pliku:

    ```java
    import com.microsoft.azure.sdk.iot.service.devicetwin.DeviceTwinDevice;
    import com.microsoft.azure.sdk.iot.service.devicetwin.Pair;
    import com.microsoft.azure.sdk.iot.service.devicetwin.Query;
    import com.microsoft.azure.sdk.iot.service.devicetwin.SqlQuery;
    import com.microsoft.azure.sdk.iot.service.jobs.JobClient;
    import com.microsoft.azure.sdk.iot.service.jobs.JobResult;
    import com.microsoft.azure.sdk.iot.service.jobs.JobStatus;

    import java.util.Date;
    import java.time.Instant;
    import java.util.HashSet;
    import java.util.Set;
    import java.util.UUID;
    ```

1. Dodaj następujące zmienne klasy toohello hello **aplikacji** klasy. Zastąp `{youriothubconnectionstring}` z parametrów połączenia Centrum IoT zanotowaną w hello *tworzenia Centrum IoT* sekcji:

    ```java
    public static final String iotHubConnectionString = "{youriothubconnectionstring}";
    public static final String deviceId = "myDeviceId";

    // How long hello job is permitted toorun without
    // completing its work on hello set of devices
    private static final long maxExecutionTimeInSeconds = 30;
    ```

1. Dodaj następujące metody toohello hello **aplikacji** tooschedule klasy hello tooupdate zadania **budynku** i **Floor** żądanego właściwości w Witaj dwie urządzenia:

    ```java
    private static JobResult scheduleJobSetDesiredProperties(JobClient jobClient, String jobId) {
      DeviceTwinDevice twin = new DeviceTwinDevice(deviceId);
      Set<Pair> desiredProperties = new HashSet<Pair>();
      desiredProperties.add(new Pair("Building", 43));
      desiredProperties.add(new Pair("Floor", 3));
      twin.setDesiredProperties(desiredProperties);
      // Optimistic concurrency control
      twin.setETag("*");

      // Schedule hello update twin job toorun now
      // against a single device
      System.out.println("Schedule job " + jobId + " for device " + deviceId);
      try {
        JobResult jobResult = jobClient.scheduleUpdateTwin(jobId, 
          "deviceId='" + deviceId + "'",
          twin,
          new Date(),
          maxExecutionTimeInSeconds);
        return jobResult;
      } catch (Exception e) {
        System.out.println("Exception scheduling desired properties job: " + jobId);
        System.out.println(e.getMessage());
        return null;
      }
    }
    ```

1. tooschedule hello toocall zadania **lockDoor** metody, Dodaj następujące metody toohello hello **aplikacji** klasy:

    ```java
    private static JobResult scheduleJobCallDirectMethod(JobClient jobClient, String jobId) {
      // Schedule a job now toocall hello lockDoor direct method
      // against a single device. Response and connection
      // timeouts are set too5 seconds.
      System.out.println("Schedule job " + jobId + " for device " + deviceId);
      try {
        JobResult jobResult = jobClient.scheduleDeviceMethod(jobId,
          "deviceId='" + deviceId + "'",
          "lockDoor",
          5L, 5L, null,
          new Date(),
          maxExecutionTimeInSeconds);
        return jobResult;
      } catch (Exception e) {
        System.out.println("Exception scheduling direct method job: " + jobId);
        System.out.println(e.getMessage());
        return null;
      }
    };
    ```

1. toomonitor zadania, Dodaj następujące metody toohello hello **aplikacji** klasy:

    ```java
    private static void monitorJob(JobClient jobClient, String jobId) {
      try {
        JobResult jobResult = jobClient.getJob(jobId);
        if(jobResult == null)
        {
          System.out.println("No JobResult for: " + jobId);
          return;
        }
        // Check hello job result until it's completed
        while(jobResult.getJobStatus() != JobStatus.completed)
        {
          Thread.sleep(100);
          jobResult = jobClient.getJob(jobId);
          System.out.println("Status " + jobResult.getJobStatus() + " for job " + jobId);
        }
        System.out.println("Final status " + jobResult.getJobStatus() + " for job " + jobId);
      } catch (Exception e) {
        System.out.println("Exception monitoring job: " + jobId);
        System.out.println(e.getMessage());
        return;
      }
    }
    ```

1. tooquery hello informacji o zadaniach hello uruchomienia, Dodaj hello następujące metody:

    ```java
    private static void queryDeviceJobs(JobClient jobClient, String start) throws Exception {
      System.out.println("\nQuery device jobs since " + start);

      // Create a jobs query using hello time hello jobs started
      Query deviceJobQuery = jobClient
          .queryDeviceJob(SqlQuery.createSqlQuery("*", SqlQuery.FromType.JOBS, "devices.jobs.startTimeUtc > '" + start + "'", null).getQuery());

      // Iterate over hello list of jobs and print hello details
      while (jobClient.hasNextJob(deviceJobQuery)) {
        System.out.println(jobClient.getNextJob(deviceJobQuery));
      }
    }
    ```

1. Aktualizacja hello **głównego** następujące hello tooinclude podpis metody `throws` klauzuli:

    ```java
    public static void main( String[] args ) throws Exception
    ```

1. monitor i toorun dwa zadania sekwencyjnie, Dodaj hello następującego kodu toohello **głównego** metody:

    ```java
    // Record hello start time
    String start = Instant.now().toString();

    // Create JobClient
    JobClient jobClient = JobClient.createFromConnectionString(iotHubConnectionString);
    System.out.println("JobClient created with success");

    // Schedule twin job desired properties
    // Maximum concurrent jobs is 1 for Free and S1 tiers
    String desiredPropertiesJobId = "DPCMD" + UUID.randomUUID();
    scheduleJobSetDesiredProperties(jobClient, desiredPropertiesJobId);
    monitorJob(jobClient, desiredPropertiesJobId);

    // Schedule twin job direct method
    String directMethodJobId = "DMCMD" + UUID.randomUUID();
    scheduleJobCallDirectMethod(jobClient, directMethodJobId);
    monitorJob(jobClient, directMethodJobId);

    // Run a query tooshow hello job detail
    queryDeviceJobs(jobClient, start);

    System.out.println("Shutting down schedule-jobs app");
    ```

1. Zapisz i zamknij hello `schedule-jobs\src\main\java\com\mycompany\app\App.java` pliku

1. Tworzenie hello **harmonogram zadań** aplikacji i poprawić błędy. Wierszu polecenia przejdź toohello `schedule-jobs` folder i hello uruchom następujące polecenie:

    `mvn clean package -DskipTests`

## <a name="create-a-device-app"></a>Tworzenie aplikacji urządzenia

W tej sekcji utworzysz aplikację konsoli języka Java, która uchwytów hello żądanej właściwości wysyłane z Centrum IoT i implementuje wywołanie metody bezpośredniego hello.

1. W hello `iot-java-schedule-jobs` folderu, Utwórz projekt Maven o nazwie **symulowane urządzenie** przy użyciu hello następujące polecenie z wiersza polecenia. Zwróć uwagę, że jest to jedno długie polecenie:

    `mvn archetype:generate -DgroupId=com.mycompany.app -DartifactId=simulated-device -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false`

1. Wierszu polecenia przejdź toohello `simulated-device` folderu.

1. Za pomocą edytora tekstu, otwórz hello `pom.xml` pliku w hello `simulated-device` folderu i dodaj następujące zależności toohello hello **zależności** węzła. Ta zależność umożliwia toouse hello **klienta w przypadku urządzenia iot** pakiet w Twojej toocommunicate aplikacji z Centrum IoT:

    ```xml
    <dependency>
      <groupId>com.microsoft.azure.sdk.iot</groupId>
      <artifactId>iot-device-client</artifactId>
      <version>1.3.32</version>
    </dependency>
    ```

    > [!NOTE]
    > Możesz sprawdzić hello najnowszą wersję **klienta w przypadku urządzenia iot** przy użyciu [wyszukiwania Maven](http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22iot-device-client%22%20g%3A%22com.microsoft.azure.sdk.iot%22).

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

1. Zapisz i zamknij hello `pom.xml` pliku.

1. Za pomocą edytora tekstu, otwórz hello `simulated-device\src\main\java\com\mycompany\app\App.java` pliku.

1. Dodaj następujące hello **zaimportować** instrukcje toohello pliku:

    ```java
    import com.microsoft.azure.sdk.iot.device.*;
    import com.microsoft.azure.sdk.iot.device.DeviceTwin.*;

    import java.io.IOException;
    import java.net.URISyntaxException;
    import java.util.Scanner;
    ```

1. Dodaj następujące zmienne klasy toohello hello **aplikacji** klasy. Zastępowanie `{youriothubname}` z nazwę Centrum IoT i `{yourdevicekey}` o wartości klucza urządzenia hello wygenerowanych w hello *tworzenie tożsamości urządzenia* sekcji:

    ```java
    private static String connString = "HostName={youriothubname}.azure-devices.net;DeviceId=myDeviceID;SharedAccessKey={yourdevicekey}";
    private static IotHubClientProtocol protocol = IotHubClientProtocol.MQTT;
    private static final int METHOD_SUCCESS = 200;
    private static final int METHOD_NOT_DEFINED = 404;
    ```

    Ta przykładowa aplikacja używa hello **protokołu** zmiennej podczas tworzenia wystąpień **DeviceClient** obiektu. Obecnie toouse dwie funkcji urządzenia muszą używać protokołu MQTT hello.

1. tooprint urządzenia dwie powiadomienia toohello konsoli, należy dodać następujące hello zagnieżdżona klasa toohello **aplikacji** klasy:

    ```java
    // Handler for device twin operation notifications from IoT Hub
    protected static class DeviceTwinStatusCallBack implements IotHubEventCallback {
      public void execute(IotHubStatusCode status, Object context) {
        System.out.println("IoT Hub responded toodevice twin operation with status " + status.name());
      }
    }
    ```

1. tooprint bezpośrednie toohello powiadomienia metody konsoli, należy dodać następujące hello zagnieżdżona klasa toohello **aplikacji** klasy:

    ```java
    // Handler for direct method notifications from IoT Hub
    protected static class DirectMethodStatusCallback implements IotHubEventCallback {
      public void execute(IotHubStatusCode status, Object context) {
        System.out.println("IoT Hub responded toodirect method operation with status " + status.name());
      }
    }
    ```

1. toohandle wywołania metody bezpośrednio z Centrum IoT, Dodaj następujące hello zagnieżdżona klasa toohello **aplikacji** klasy:

    ```java
    // Handler for direct method calls from IoT Hub
    protected static class DirectMethodCallback
        implements DeviceMethodCallback {
      @Override
      public DeviceMethodData call(String methodName, Object methodData, Object context) {
        DeviceMethodData deviceMethodData;
        switch (methodName) {
          case "lockDoor": {
            System.out.println("Executing direct method: " + methodName);
            deviceMethodData = new DeviceMethodData(METHOD_SUCCESS, "Executed direct method " + methodName);
            break;
          }
          default: {
            deviceMethodData = new DeviceMethodData(METHOD_NOT_DEFINED, "Not defined direct method " + methodName);
          }
        }
        // Notify IoT Hub of result
        return deviceMethodData;
      }
    }
    ```

1. Aktualizacja hello **głównego** następujące hello tooinclude podpis metody `throws` klauzuli:

    ```java
    public static void main( String[] args ) throws IOException, URISyntaxException
    ```

1. Dodaj hello następującego kodu toohello **głównego** metodę:
    * Utwórz toocommunicate klienta urządzenia z Centrum IoT.
    * Utwórz **urządzenia** toostore hello urządzenia dwie właściwości obiektu.

    ```java
    // Create a device client
    DeviceClient client = new DeviceClient(connString, protocol);

    // An object toomanage device twin desired and reported properties
    Device dataCollector = new Device() {
      @Override
      public void PropertyCall(String propertyKey, Object propertyValue, Object context)
      {
        System.out.println("Received desired property change: " + propertyKey + " " + propertyValue);
      }
    };
    ```

1. toostart hello urządzenia klienta usługi, dodać hello następującego kodu toohello **głównego** metody:

    ```java
    try {
      // Open hello DeviceClient
      // Start hello device twin services
      // Subscribe toodirect method calls
      client.open();
      client.startDeviceTwin(new DeviceTwinStatusCallBack(), null, dataCollector, null);
      client.subscribeToDeviceMethod(new DirectMethodCallback(), null, new DirectMethodStatusCallback(), null);
    } catch (Exception e) {
      System.out.println("Exception, shutting down \n" + " Cause: " + e.getCause() + " \n" + e.getMessage());
      dataCollector.clean();
      client.closeNow();
      System.out.println("Shutting down...");
    }
    ```

1. toowait dla hello użytkownika toopress hello **Enter** klucza przed zamknięciem, należy dodać kodu zakończenia toohello hello hello **głównego** metody:

    ```java
    // Close hello app
    System.out.println("Press any key tooexit...");
    Scanner scanner = new Scanner(System.in);
    scanner.nextLine();
    dataCollector.clean();
    client.closeNow();
    scanner.close();
    ```

1. Zapisz i zamknij hello `simulated-device\src\main\java\com\mycompany\app\App.java` pliku.

1. Tworzenie hello **symulowane urządzenie** aplikacji i poprawić błędy. Wierszu polecenia przejdź toohello `simulated-device` folder i hello uruchom następujące polecenie:

    `mvn clean package -DskipTests`

## <a name="run-hello-apps"></a>Uruchamianie aplikacji hello

Wszystko jest teraz gotowy toorun hello konsoli aplikacji.

1. W wierszu polecenia w hello `simulated-device` folderu, uruchom następujące polecenie toostart hello aplikacji urządzenia nasłuchiwanie zmian żądanej właściwości i wywołania metody bezpośredniego hello:

    `mvn exec:java -Dexec.mainClass="com.mycompany.app.App"`

    ![Uruchamia powitania klienta urządzenia](media/iot-hub-java-java-schedule-jobs/device-app-1.png)

1. W wierszu polecenia w hello `schedule-jobs` folderu, uruchom następujące polecenie toorun hello hello **harmonogram zadań** usługi aplikacji toorun dwa zadania. Hello najpierw ustawia wartości właściwości hello potrzebne, wywołania drugiej hello hello metoda bezpośrednia:

    `mvn exec:java -Dexec.mainClass="com.mycompany.app.App"`

    ![Centrum IoT Java usługi aplikacji tworzy dwa zadania](media/iot-hub-java-java-schedule-jobs/service-app-1.png)

1. aplikacji urządzenia Hello obsługuje hello potrzebne zmiany właściwości i wywołanie metody bezpośredniego hello:

    ![zmiany toohello odpowiada powitania klienta urządzenia](media/iot-hub-java-java-schedule-jobs/device-app-2.png)

## <a name="next-steps"></a>Następne kroki

W tym samouczku został skonfigurowany nowego centrum IoT w portalu Azure hello i w rejestrze tożsamości Centrum IoT hello zostanie utworzona tożsamość urządzenia. Utworzono aplikacji zaplecza toorun dwa zadania. Hello pierwszego zadania ustawić wartości żądanej właściwości, a zadanie drugi hello wywołana metoda bezpośrednia.

Hello Użyj następujących zasobów toolearn jak do:

* Wysłać dane telemetryczne z urządzenia z hello [Rozpoczynanie pracy z Centrum IoT](iot-hub-java-java-getstarted.md) samouczka.
* Kontrolowanie urządzenia interakcyjne (takich jak włączanie wentylator z aplikacji kontrolowane przez użytkownika) z hello [metody bezpośredniego](iot-hub-java-java-direct-methods.md) samouczka.
