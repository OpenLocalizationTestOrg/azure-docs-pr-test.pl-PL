---
title: "aaaGet wprowadzenie twins urządzenia Azure IoT Hub (Java) | Dokumentacja firmy Microsoft"
description: "Jak tooadd twins urządzenia Azure IoT Hub toouse tagów, a następnie użyj zapytania Centrum IoT. Używasz urządzenia Azure IoT hello zestawu SDK dla języka Java tooimplement hello urządzenia aplikacji i hello Azure IoT usługi SDK dla języka Java tooimplement aplikacji usługi, który dodaje znaczniki hello i uruchamia hello zapytania Centrum IoT."
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
ms.date: 07/04/2017
ms.author: dobett
ms.openlocfilehash: 25f6fc81471d59c62bcdc3766bb5c33f5733c930
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-device-twins-java"></a>Rozpoczynanie pracy z urządzenia twins (Java)

[!INCLUDE [iot-hub-selector-twin-get-started](../../includes/iot-hub-selector-twin-get-started.md)]

W tym samouczku można utworzyć dwie aplikacje konsoli Java:

* **Dodaj tag query**, aplikacji zaplecza Java, która dodaje znaczniki i zapytanie twins urządzenia.
* **Symulowane urządzenie**, że łączące Centrum IoT tooyour i raporty stanu łączności za pomocą właściwości zgłoszone aplikacji Java urządzenia.

> [!NOTE]
> Artykuł Hello [Azure IoT SDK](iot-hub-devguide-sdks.md) informacje na temat hello Azure IoT SDK służy toobuild zarówno urządzenia, jak i zaplecza aplikacji.

toocomplete tego samouczka należy:

* Witaj najnowszych [Java SE Development Kit 8](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)
* [Maven 3](https://maven.apache.org/install.html)
* Aktywne konto platformy Azure. (Jeśli nie masz konta, możesz utworzyć [bezpłatne konto](http://azure.microsoft.com/pricing/free-trial/) w zaledwie kilka minut.)

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity-portal](../../includes/iot-hub-get-started-create-device-identity-portal.md)]

Jeśli wolisz tożsamości urządzenia hello toocreate programowo, przeczytaj hello odpowiedniej sekcji w hello [połączenia przy użyciu języka Java Centrum IoT urządzenia tooyour](iot-hub-java-java-getstarted.md#create-a-device-identity) artykułu.

## <a name="create-hello-service-app"></a>Tworzenie aplikacji usługi hello

W tej sekcji utworzysz aplikację Java dodające metadanych lokalizacji dwie tag toohello urządzenie w Centrum IoT skojarzone z **myDeviceId**. Aplikacja Hello najpierw wysyła zapytanie Centrum IoT dla urządzeń znajdujących się w hello USA, a następnie dla urządzeń, które zgłosiły połączenia sieci komórkowej.

1. Na komputerze deweloperskim, należy utworzyć pusty folder o nazwie `iot-java-twin-getstarted`.

1. W hello `iot-java-twin-getstarted` folderu, Utwórz projekt Maven o nazwie **Dodaj tag query** przy użyciu hello następujące polecenie z wiersza polecenia. Zwróć uwagę, że jest to jedno długie polecenie:

    `mvn archetype:generate -DgroupId=com.mycompany.app -DartifactId=add-tags-query -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false`

1. Wierszu polecenia przejdź toohello `add-tags-query` folderu.

1. Za pomocą edytora tekstu, otwórz hello `pom.xml` pliku w hello `add-tags-query` folderu i dodaj następujące zależności toohello hello **zależności** węzła. Ta zależność umożliwia toouse hello **klienta w przypadku usługi iot** pakiet w Twojej toocommunicate aplikacji z Centrum IoT:

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

1. Za pomocą edytora tekstu, otwórz hello `add-tags-query\src\main\java\com\mycompany\app\App.java` pliku.

1. Dodaj następujące hello **zaimportować** instrukcje toohello pliku:

    ```java
    import com.microsoft.azure.sdk.iot.service.devicetwin.*;
    import com.microsoft.azure.sdk.iot.service.exceptions.IotHubException;

    import java.io.IOException;
    import java.util.HashSet;
    import java.util.Set;
    ```

1. Dodaj następujące zmienne klasy toohello hello **aplikacji** klasy. Zastąp `{youriothubconnectionstring}` z parametrów połączenia Centrum IoT zanotowaną w hello *tworzenia Centrum IoT* sekcji:

    ```java
    public static final String iotHubConnectionString = "{youriothubconnectionstring}";
    public static final String deviceId = "myDeviceId";

    public static final String region = "US";
    public static final String plant = "Redmond43";
    ```

1. Aktualizacja hello **głównego** następujące hello tooinclude podpis metody `throws` klauzuli:

    ```java
    public static void main( String[] args ) throws IOException
    ```

1. Dodaj hello następującego kodu toohello **głównego** hello toocreate — metoda **DeviceTwin** i **DeviceTwinDevice** obiektów. Witaj **DeviceTwin** obiektu obsługuje hello komunikację z Centrum IoT. Witaj **DeviceTwinDevice** obiekt reprezentuje Witaj dwie urządzenia z jego właściwości i tagi:

    ```java
    // Get hello DeviceTwin and DeviceTwinDevice objects
    DeviceTwin twinClient = DeviceTwin.createFromConnectionString(iotHubConnectionString);
    DeviceTwinDevice device = new DeviceTwinDevice(deviceId);
    ```

1. Dodaj następujące hello `try/catch` zablokować toohello **głównego** metody:

    ```java
    try {
      // Code goes here
    } catch (IotHubException e) {
      System.out.println(e.getMessage());
    } catch (IOException e) {
      System.out.println(e.getMessage());
    }
    ```

1. Witaj tooupdate **region** i **roślin** hello następującego kodu w hello Dodaj tagi dwie urządzeń w Twojej dwie urządzenia `try` bloku:

    ```java
    // Get hello device twin from IoT Hub
    System.out.println("Device twin before update:");
    twinClient.getTwin(device);
    System.out.println(device);

    // Update device twin tags if they are different
    // from hello existing values
    String currentTags = device.tagsToString();
    if ((!currentTags.contains("region=" + region) && !currentTags.contains("plant=" + plant))) {
      // Create hello tags and attach them toohello DeviceTwinDevice object
      Set<Pair> tags = new HashSet<Pair>();
      tags.add(new Pair("region", region));
      tags.add(new Pair("plant", plant));
      device.setTags(tags);

      // Update hello device twin in IoT Hub
      System.out.println("Updating device twin");
      twinClient.updateTwin(device);
    }

    // Retrieve hello device twin with hello tag values from IoT Hub
    System.out.println("Device twin after update:");
    twinClient.getTwin(device);
    System.out.println(device);
    ```

1. tooquery hello urządzenia twins w Centrum IoT, Dodaj hello następującego kodu toohello `try` blok po kodzie hello dodanym w poprzednim kroku hello. Kod Hello uruchamia dwa zapytania. Każde zapytanie zwraca maksymalnie 100 urządzeń:

    ```java
    // Query hello device twins in IoT Hub
    System.out.println("Devices in Redmond:");

    // Construct hello query
    SqlQuery sqlQuery = SqlQuery.createSqlQuery("*", SqlQuery.FromType.DEVICES, "tags.plant='Redmond43'", null);

    // Run hello query, returning a maximum of 100 devices
    Query twinQuery = twinClient.queryTwin(sqlQuery.getQuery(), 100);
    while (twinClient.hasNextDeviceTwin(twinQuery)) {
      DeviceTwinDevice d = twinClient.getNextDeviceTwin(twinQuery);
      System.out.println(d.getDeviceId());
    }

    System.out.println("Devices in Redmond using a cellular network:");

    // Construct hello query
    sqlQuery = SqlQuery.createSqlQuery("*", SqlQuery.FromType.DEVICES, "tags.plant='Redmond43' AND properties.reported.connectivityType = 'cellular'", null);

    // Run hello query, returning a maximum of 100 devices
    twinQuery = twinClient.queryTwin(sqlQuery.getQuery(), 3);
    while (twinClient.hasNextDeviceTwin(twinQuery)) {
      DeviceTwinDevice d = twinClient.getNextDeviceTwin(twinQuery);
      System.out.println(d.getDeviceId());
    }
    ```

1. Zapisz i zamknij hello `add-tags-query\src\main\java\com\mycompany\app\App.java` pliku

1. Tworzenie hello **Dodaj tag query** aplikacji i poprawić błędy. Wierszu polecenia przejdź toohello `add-tags-query` folder i hello uruchom następujące polecenie:

    `mvn clean package -DskipTests`

## <a name="create-a-device-app"></a>Tworzenie aplikacji urządzenia

W tej sekcji utworzysz aplikację konsoli języka Java, która ustawia wartości właściwości zgłoszone wysyłany tooIoT Centrum.

1. W hello `iot-java-twin-getstarted` folderu, Utwórz projekt Maven o nazwie **symulowane urządzenie** przy użyciu hello następujące polecenie z wiersza polecenia. Zwróć uwagę, że jest to jedno długie polecenie:

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
    private static String deviceId = "myDeviceId";
    ```

    Ta przykładowa aplikacja używa hello **protokołu** zmiennej podczas tworzenia wystąpień **DeviceClient** obiektu. Obecnie toouse dwie funkcji urządzenia muszą używać protokołu MQTT hello.

1. Dodaj hello następującego kodu toohello **głównego** metodę:
    * Utwórz toocommunicate klienta urządzenia z Centrum IoT.
    * Utwórz **urządzenia** toostore hello urządzenia dwie właściwości obiektu.

    ```java
    DeviceClient client = new DeviceClient(connString, protocol);

    // Create a Device object toostore hello device twin properties
    Device dataCollector = new Device() {
      // Print details when a property value changes
      @Override
      public void PropertyCall(String propertyKey, Object propertyValue, Object context) {
        System.out.println(propertyKey + " changed too" + propertyValue);
      }
    };
    ```

1. Dodaj hello następującego kodu toohello **głównego** toocreate — metoda **connectivityType** zgłosił właściwości, a następnie wysłać je tooIoT Centrum:

    ```java
    try {
      // Open hello DeviceClient and start hello device twin services.
      client.open();
      client.startDeviceTwin(new DeviceTwinStatusCallBack(), null, dataCollector, null);

      // Create a reported property and send it tooyour IoT hub.
      dataCollector.setReportedProp(new Property("connectivityType", "cellular"));
      client.sendReportedProperties(dataCollector.getReportedProp());
    }
    catch (Exception e) {
      System.out.println("On exception, shutting down \n" + " Cause: " + e.getCause() + " \n" + e.getMessage());
      dataCollector.clean();
      client.close();
      System.out.println("Shutting down...");
    }
    ```

1. Dodaj kod zakończenia toohello hello hello **głównego** metody. Oczekiwanie na powitania **Enter** klucz umożliwia czas stanu hello tooreport Centrum IoT hello urządzenia dwie czynności:

    ```java
    System.out.println("Press any key tooexit...");

    Scanner scanner = new Scanner(System.in);
    scanner.nextLine();

    dataCollector.clean();
    client.close();
    ```

1. Zapisz i zamknij hello `simulated-device\src\main\java\com\mycompany\app\App.java` pliku.

1. Tworzenie hello **symulowane urządzenie** aplikacji i poprawić błędy. Wierszu polecenia przejdź toohello `simulated-device` folder i hello uruchom następujące polecenie:

    `mvn clean package -DskipTests`

## <a name="run-hello-apps"></a>Uruchamianie aplikacji hello

Wszystko jest teraz gotowy toorun hello konsoli aplikacji.

1. W wierszu polecenia w hello `add-tags-query` folderu, uruchom następujące polecenie toorun hello hello **Dodaj tag query** usługi aplikacji:

    `mvn exec:java -Dexec.mainClass="com.mycompany.app.App"`

    ![Centrum IoT Java usługi aplikacji tooupdate wartości tagów i uruchamianie zapytań urządzenia](media/iot-hub-java-java-twin-getstarted/service-app-1.png)

    Zostanie wyświetlony hello **roślin** i **region** tagi dodane dwie urządzenia toohello. Hello pierwsza kwerenda zwraca urządzenia, ale hello drugi nie.

1. W wierszu polecenia w hello `simulated-device` folderu, uruchom następujące polecenie tooadd hello hello **connectivityType** zgłosił dwie urządzenia toohello właściwości:

    `mvn exec:java -Dexec.mainClass="com.mycompany.app.App"`

    ![powitania klienta urządzenia dodaje hello ** connectivityType ** zgłosił właściwości](media/iot-hub-java-java-twin-getstarted/device-app-1.png)

1. W wierszu polecenia w hello `add-tags-query` folderu, uruchom następujące polecenie toorun hello hello **Dodaj tag query** usługi aplikacji po raz drugi:

    `mvn exec:java -Dexec.mainClass="com.mycompany.app.App"`

    ![Centrum IoT Java usługi aplikacji tooupdate wartości tagów i uruchamianie zapytań urządzenia](media/iot-hub-java-java-twin-getstarted/service-app-2.png)

    Teraz urządzenia wysłał hello **connectivityType** tooIoT właściwości koncentratora, hello drugiego zapytania zwraca urządzenie.

## <a name="next-steps"></a>Następne kroki

W tym samouczku został skonfigurowany nowego centrum IoT w portalu Azure hello i w rejestrze tożsamości Centrum IoT hello zostanie utworzona tożsamość urządzenia. Dodaje metadane urządzenia jako tagi z aplikacji zaplecza i zapisane urządzenia tooreport urządzenia łączności informacji o aplikacji w Witaj dwie urządzenia. Również wiesz, jak tooquery hello przy użyciu języka zapytań Centrum IoT przypominającego SQL hello dwie informacje o urządzeniu.

Hello Użyj następujących zasobów toolearn jak do:

* Wysłać dane telemetryczne z urządzenia z hello [Rozpoczynanie pracy z Centrum IoT](iot-hub-java-java-getstarted.md) samouczka.
* Kontrolowanie urządzenia interakcyjne (takich jak włączanie wentylator z aplikacji kontrolowane przez użytkownika) z hello [metody bezpośredniego](iot-hub-java-java-direct-methods.md) samouczka.

<!-- Images. -->
[7]: ./media/iot-hub-java-java-twin-getstarted/invoke-method.png
[8]: ./media/iot-hub-java-java-twin-getstarted/device-listen.png
[9]: ./media/iot-hub-java-java-twin-getstarted/device-respond.png

<!-- Links -->
[lnk-hub-sdks]: iot-hub-devguide-sdks.md
