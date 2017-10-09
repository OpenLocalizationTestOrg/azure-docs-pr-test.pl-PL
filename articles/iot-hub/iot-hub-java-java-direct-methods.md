---
title: "Centrum IoT Azure aaaUse bezpośrednie metod (Java) | Dokumentacja firmy Microsoft"
description: "Jak toouse Centrum IoT Azure bezpośrednie metody. Możesz używać urządzenia Azure IoT hello zestawu SDK dla języka Java tooimplement aplikacji symulowane urządzenie, która obejmuje metoda bezpośrednia i hello Azure IoT usługi SDK dla języka Java tooimplement usługi aplikacji, która wywołuje metodę bezpośredniego hello."
services: iot-hub
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.assetid: ab035b8e-bff8-4e12-9536-f31d6b6fe425
ms.service: iot-hub
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/08/2017
ms.author: dobett
ms.openlocfilehash: b6f2f4a64535ab649a3965cd9c5a19bebaf88eef
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="use-direct-methods-java"></a>Użyj metody bezpośredniego (Java)

[!INCLUDE [iot-hub-selector-c2d-methods](../../includes/iot-hub-selector-c2d-methods.md)]

W tym samouczku można utworzyć dwie aplikacje konsoli Java:

* **wywołania bezpośrednie — metody**, aplikacji zaplecza Java, która wywołuje metodę w aplikacji symulowane urządzenie hello i wyświetla hello odpowiedzi.
* **Symulowane urządzenie**, która symuluje urządzenie łączące Centrum IoT tooyour z tożsamości urządzenia hello tworzenia aplikacji Java. Ta aplikacja odpowiada toohello wywoływany bezpośrednio z zaplecza hello.

> [!NOTE]
> Informacje hello zestawów SDK, której można toobuild toorun aplikacji na urządzeniach i z zaplecza rozwiązania, zobacz [Azure IoT SDK][lnk-hub-sdks].

toocomplete tego samouczka należy:

* Java SE 8. <br/> [Przygotowywanie środowiska projektowego] [ lnk-dev-setup] w tym artykule opisano sposób tooinstall Java w tym samouczku w systemie Windows lub Linux.
* Maven 3.  <br/> [Przygotowywanie środowiska projektowego] [ lnk-dev-setup] w tym artykule opisano sposób tooinstall [Maven] [ lnk-maven] ten samouczek dotyczący systemu Windows lub Linux.
* [Środowisko node.js w wersji 0.10.0 lub nowszym](http://nodejs.org).

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity](../../includes/iot-hub-get-started-create-device-identity.md)]

## <a name="create-a-simulated-device-app"></a>Tworzenie aplikacji symulowanego urządzenia

W tej sekcji utworzysz aplikację konsoli Java, która odpowiada tooa metody wywoływane przez rozwiązania hello zakończenia.

1. Utwórz pusty folder o nazwie iot-java bezpośrednio method.

1. W folderze iot-java bezpośrednio method hello Utwórz projekt Maven o nazwie **symulowane urządzenie** przy użyciu hello następujące polecenie z wiersza polecenia. Hello następujące polecenia jest pojedynczą, długie polecenie:

    `mvn archetype:generate -DgroupId=com.mycompany.app -DartifactId=simulated-device -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false`

1. Wierszu polecenia przejdź toohello symulowane urządzenie folderu.

1. Za pomocą edytora tekstu, otwórz plik pom.xml hello w folderze symulowane urządzenie hello i dodaj następujące zależności toohello hello **zależności** węzła. Ta zależność umożliwia możesz toouse powitania klienta w przypadku urządzenia iot pakiet w toocommunicate Twojego aplikacji z Centrum IoT:

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

1. Za pomocą edytora tekstu, otwórz plik simulated-device\src\main\java\com\mycompany\app\App.java hello.

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
    private static final int METHOD_SUCCESS = 200;
    private static final int METHOD_NOT_DEFINED = 404;
    ```

    Ta przykładowa aplikacja używa hello **protokołu** zmiennej podczas tworzenia wystąpień **DeviceClient** obiektu. Obecnie toouse bezpośrednie metody muszą używać protokołu MQTT hello.

1. tooreturn koncentratora IoT tooyour kod stanu, Dodaj następujące hello zagnieżdżona klasa toohello **aplikacji** klasy:

    ```java
    protected static class DirectMethodStatusCallback implements IotHubEventCallback
    {
      public void execute(IotHubStatusCode status, Object context)
      {
        System.out.println("IoT Hub responded toodevice method operation with status " + status.name());
      }
    }
    ```

1. toohandle hello bezpośrednie wywołania metod z hello rozwiązania wewnętrznego, Dodaj następujące hello zagnieżdżona klasa toohello **aplikacji** klasy:

    ```java
    protected static class DirectMethodCallback implements com.microsoft.azure.sdk.iot.device.DeviceTwin.DeviceMethodCallback
    {
      @Override
      public DeviceMethodData call(String methodName, Object methodData, Object context)
      {
        DeviceMethodData deviceMethodData;
        switch (methodName)
        {
          case "writeLine" :
          {
            int status = METHOD_SUCCESS;
            System.out.println(new String((byte[])methodData));
            deviceMethodData = new DeviceMethodData(status, "Executed direct method " + methodName);
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

1. toocreate **DeviceClient** i nasłuchiwania bezpośrednie wywołania metod, dodać **głównego** toohello metody **aplikacji** klasy:

    ```java
    public static void main(String[] args)
      throws IOException, URISyntaxException
    {
      System.out.println("Starting device sample...");

      DeviceClient client = new DeviceClient(connString, protocol);

      try
      {
        client.open();
        client.subscribeToDeviceMethod(new DirectMethodCallback(), null, new DirectMethodStatusCallback(), null);
        System.out.println("Subscribed toodirect methods. Waiting...");
      }
      catch (Exception e)
      {
        System.out.println("On exception, shutting down \n" + " Cause: " + e.getCause() + " \n" +  e.getMessage());
        client.close();
        System.out.println("Shutting down...");
      }

      System.out.println("Press any key tooexit...");
      Scanner scanner = new Scanner(System.in);
      scanner.nextLine();
      scanner.close();
      client.close();
      System.out.println("Shutting down...");
    }
    ```

1. Zapisz i zamknij plik simulated-device\src\main\java\com\mycompany\app\App.java hello

1. Tworzenie hello **symulowane urządzenie** aplikacji i poprawić błędy. Wierszu polecenia przejdź folder symulowane urządzenie toohello i hello uruchom następujące polecenie:

    `mvn clean package -DskipTests`

## <a name="call-a-direct-method-on-a-device"></a>Wywołanie metody bezpośrednio na urządzeniu

W tej sekcji utworzysz aplikację konsoli języka Java, która wywołuje metodę bezpośredniego, a następnie wyświetla hello odpowiedzi. Ta aplikacja konsoli łączy tooyour metoda bezpośrednia hello tooinvoke Centrum IoT.

1. W folderze iot-java bezpośrednio method hello Utwórz projekt Maven o nazwie **invoke bezpośrednio method** przy użyciu hello następujące polecenie z wiersza polecenia. Hello następujące polecenia jest pojedynczą, długie polecenie:

    `mvn archetype:generate -DgroupId=com.mycompany.app -DartifactId=invoke-direct-method -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false`

1. Wierszu polecenia przejdź toohello invoke bezpośrednio method folderu.

1. Za pomocą edytora tekstu, otwórz plik pom.xml hello w folderze invoke bezpośrednio method hello i dodaj następujące zależności toohello hello **zależności** węzła. Ta zależność umożliwia możesz toouse hello iot usługi klienta pakietu w Twojej toocommunicate aplikacji z Centrum IoT:

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

1. Za pomocą edytora tekstu, otwórz plik invoke-direct-method\src\main\java\com\mycompany\app\App.java hello.

1. Dodaj następujące hello **zaimportować** instrukcje toohello pliku:

    ```java
    import com.microsoft.azure.sdk.iot.service.devicetwin.DeviceMethod;
    import com.microsoft.azure.sdk.iot.service.devicetwin.MethodResult;
    import com.microsoft.azure.sdk.iot.service.exceptions.IotHubException;

    import java.io.IOException;
    import java.util.concurrent.TimeUnit;
    ```

1. Dodaj następujące zmienne klasy toohello hello **aplikacji** klasy. Zastąp `{youriothubconnectionstring}` z parametrów połączenia Centrum IoT zanotowaną w hello *tworzenia Centrum IoT* sekcji:

    ```java
    public static final String iotHubConnectionString = "{youriothubconnectionstring}";
    public static final String deviceId = "myDeviceId";

    public static final String methodName = "writeLine";
    public static final Long responseTimeout = TimeUnit.SECONDS.toSeconds(30);
    public static final Long connectTimeout = TimeUnit.SECONDS.toSeconds(5);
    public static final String payload = "a line toobe written";
    ```

1. Metoda hello tooinvoke na powitania symulowane urządzenie, Dodaj hello następującego kodu toohello **głównego** metody:

    ```java
    System.out.println("Starting sample...");
    DeviceMethod methodClient = DeviceMethod.createFromConnectionString(iotHubConnectionString);

    try
    {
        System.out.println("Invoke direct method");
        MethodResult result = methodClient.invoke(deviceId, methodName, responseTimeout, connectTimeout, payload);

        if(result == null)
        {
            throw new IOException("Direct method invoke returns null");
        }
        System.out.println("Status=" + result.getStatus());
        System.out.println("Payload=" + result.getPayload());
    }
    catch (IotHubException e)
    {
        System.out.println(e.getMessage());
    }

    System.out.println("Shutting down sample...");
    ```

1. Zapisz i zamknij plik invoke-direct-method\src\main\java\com\mycompany\app\App.java hello

1. Tworzenie hello **invoke bezpośrednio method** aplikacji i poprawić błędy. Wierszu polecenia przejdź toohello invoke bezpośrednio method folder i hello uruchom następujące polecenie:

    `mvn clean package -DskipTests`

## <a name="run-hello-apps"></a>Uruchamianie aplikacji hello

Wszystko jest teraz gotowy toorun hello konsoli aplikacji.

1. W wierszu polecenia w folderze symulowane urządzenie hello uruchom następujące polecenia toobegin nasłuchiwania dla wywołań metod z Centrum IoT hello:

    `mvn exec:java -Dexec.mainClass="com.mycompany.app.App"`

    ![Centrum IoT Java symulowane urządzenie toolisten aplikacji dla wywołań metod bezpośredniego][8]

1. W wierszu polecenia w folderze invoke bezpośrednio method hello uruchom następujące polecenie toocall hello metody na symulowane urządzenie z Centrum IoT:

    `mvn exec:java -Dexec.mainClass="com.mycompany.app.App"`

    ![Toocall aplikacji usługi Centrum IoT Java metoda bezpośrednia][7]

1. Symulowane urządzenie Hello odpowiada wywołanie metody bezpośredniego toohello:

    ![Wywołanie metody bezpośredniego toohello odpowiada aplikacji symulowane urządzenie Java Centrum IoT][9]

## <a name="next-steps"></a>Następne kroki

W tym samouczku został skonfigurowany nowego centrum IoT w portalu Azure hello i w rejestrze tożsamości Centrum IoT hello zostanie utworzona tożsamość urządzenia. Użyto tego urządzenia tożsamości tooenable hello symulowane urządzenie aplikacji tooreact toomethods wywołana przez hello chmury. Utworzono aplikację, która wywołuje metody na urządzeniu hello i wyświetla hello odpowiedzi z hello urządzenia.

tooexplore Zobacz inne scenariusze IoT [Planowanie zadań na wielu urządzeniach][lnk-devguide-jobs].

toolearn tooextend IoT metody rozwiązania i harmonogram wywołuje na wielu urządzeniach, zobacz hello [emisji zadania i harmonogramu] [ lnk-tutorial-jobs] samouczka.

<!-- Images. -->
[7]: ./media/iot-hub-java-java-direct-methods/invoke-method.png
[8]: ./media/iot-hub-java-java-direct-methods/device-listen.png
[9]: ./media/iot-hub-java-java-direct-methods/device-respond.png

<!-- Links -->
[lnk-dev-setup]: https://github.com/Azure/azure-iot-sdk-java/blob/master/doc/java-devbox-setup.md
[lnk-maven]: https://maven.apache.org/what-is-maven.html
[lnk-hub-sdks]: iot-hub-devguide-sdks.md

[lnk-devguide-jobs]: iot-hub-devguide-jobs.md
[lnk-tutorial-jobs]: iot-hub-node-node-schedule-jobs.md
[lnk-maven-service-search]: http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22iot-service-client%22%20g%3A%22com.microsoft.azure.sdk.iot%22
[lnk-maven-device-search]: http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22iot-device-client%22%20g%3A%22com.microsoft.azure.sdk.iot%22
