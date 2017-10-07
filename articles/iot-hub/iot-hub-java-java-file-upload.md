---
title: "pliki aaaUpload z urządzeń tooAzure Centrum IoT z językiem Java | Dokumentacja firmy Microsoft"
description: "Jak tooupload pliki z chmury toohello urządzenia przy użyciu urządzenia Azure IoT SDK dla języka Java. Przekazano pliki są przechowywane w kontenerze obiektu blob magazynu Azure."
services: iot-hub
documentationcenter: java
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 4759d229-f856-4526-abda-414f8b00a56d
ms.service: iot-hub
ms.devlang: java
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/28/2017
ms.author: dobett
ms.openlocfilehash: e305fe61bf7ca0aeb2c092bc2c7efebdc78d4f68
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="upload-files-from-your-device-toohello-cloud-with-iot-hub"></a>Przekazywanie plików z chmury toohello urządzenie z Centrum IoT

[!INCLUDE [iot-hub-file-upload-language-selector](../../includes/iot-hub-file-upload-language-selector.md)]

W tym samouczku opiera się na powitania kodu w hello [wysyłać chmury do urządzenia z Centrum IoT](iot-hub-java-java-c2d.md) tooshow samouczka możesz jak toouse hello [pliku możliwości przekazywania Centrum IoT](iot-hub-devguide-file-upload.md) tooupload pliku zbyt[ Magazyn obiektów blob platformy Azure](../storage/index.md). Witaj samouczek pokazuje, jak do:

- Bezpieczne udostępnianie urządzenia platformy Azure blob identyfikatora URI pobierania pliku.
- Użyj hello pliku hello Centrum IoT pliku przekazywania powiadomień tootrigger przetwarzania w sieci wewnętrznej aplikacji.

Witaj [Rozpoczynanie pracy z Centrum IoT](iot-hub-java-java-getstarted.md) i [wysyłać chmury do urządzenia z Centrum IoT](iot-hub-java-java-c2d.md) samouczki przedstawiają hello podstawowych urządzenia do chmury i chmury do urządzenia obsługi funkcji Centrum IoT. Witaj [wiadomości procesu urządzenia do chmury](iot-hub-java-java-process-d2c.md) samouczek przedstawia sposób tooreliably magazynu urządzenia do chmury wiadomości w magazynie obiektów blob platformy Azure. Jednak w niektórych scenariuszach nie można łatwo mapować hello dane, które urządzenia wysłać w wiadomości powitania od stosunkowo mały urządzenia do chmury, które akceptuje Centrum IoT. Na przykład:

* Duże pliki, które zawierają obrazów
* Filmy wideo
* Dane wibrację próbkowanych zgodnie o dużej częstotliwości
* Niektóre formularz wstępnie przetworzonych danych.

Pliki te są zwykle partii przetwarzania w chmurze hello za pomocą narzędzi takich jak [fabryki danych Azure](../data-factory/index.md) lub hello [Hadoop](../hdinsight/index.md) stosu. Jeśli potrzebujesz tooupland pliki z urządzenia, można nadal używać hello bezpieczeństwa i niezawodności Centrum IoT.

Na końcu hello tego samouczka możesz uruchomić dwie aplikacje konsoli Java:

* **Symulowane urządzenie**, zmodyfikowanej wersji aplikacji hello utworzonej w samouczku hello [chmury urządzenia wysyłania wiadomości z Centrum IoT]. Ta aplikacja będzie przekazywać toostorage plików, przy użyciu identyfikatora URI połączenia SAS udostępniane przez Centrum IoT.
* **Odczyt pliku przekazywania powiadomień**, która odbiera powiadomienia o przekazywania plików z Centrum IoT.

> [!NOTE]
> Centrum IoT obsługuje wiele platform urządzeń i języków (w tym C, .NET i Javascript) za pomocą urządzenia Azure IoT zestawów SDK. Zobacz toohello [Azure IoT Developer Center] instrukcje krok po kroku na temat tooconnect tooAzure Twojego urządzenia IoT Hub.

toocomplete tego samouczka należy hello następujące:

* Witaj najnowszych [Java SE Development Kit 8](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)
* [Maven 3](https://maven.apache.org/install.html)
* Aktywne konto platformy Azure. (Jeśli nie masz konta, możesz utworzyć [bezpłatne konto](http://azure.microsoft.com/pricing/free-trial/) w zaledwie kilka minut.)

[!INCLUDE [iot-hub-associate-storage](../../includes/iot-hub-associate-storage.md)]

## <a name="upload-a-file-from-a-device-app"></a>Przekaż plik z aplikacji przez urządzenia

W tej sekcji możesz zmodyfikować aplikację urządzenia hello utworzony w [wysyłać chmury do urządzenia z Centrum IoT](iot-hub-java-java-c2d.md) tooupload Centrum tooIoT pliku.

1. Kopiowanie obrazu pliku toohello `simulated-device` folder i zmień jego nazwę `myimage.png`.

1. Za pomocą edytora tekstu, otwórz hello `simulated-device\src\main\java\com\mycompany\app\App.java` pliku.

1. Dodaj hello deklaracja zmiennej toohello **aplikacji** klasy:

    ```java
    private static String fileName = "myimage.png";
    ```

1. tooprocess wywołania zwrotnego komunikatach przekazywania pliku, Dodaj następujące hello zagnieżdżona klasa toohello **aplikacji** klasy:

    ```java
    // Define a callback method tooprint status codes from IoT Hub.
    protected static class FileUploadStatusCallBack implements IotHubEventCallback {
      public void execute(IotHubStatusCode status, Object context) {
        System.out.println("IoT Hub responded toofile upload for " + fileName
            + " operation with status " + status.name());
      }
    }
    ```

1. tooupload obrazów tooIoT koncentratora, Dodaj hello następujące metody toohello **aplikacji** tooupload klasy obrazy tooIoT Centrum:

    ```java
    // Use IoT Hub tooupload a file asynchronously tooAzure blob storage.
    private static void uploadFile(String fullFileName) throws FileNotFoundException, IOException
    {
      File file = new File(fullFileName);
      InputStream inputStream = new FileInputStream(file);
      long streamLength = file.length();

      client.uploadToBlobAsync(fileName, inputStream, streamLength, new FileUploadStatusCallBack(), null);
    }
    ```

1. Modyfikowanie hello **głównego** hello toocall — metoda **uploadFile** metody pokazane na powitania po fragment kodu:

    ```java
    client.open();

    try
    {
      // Get hello filename and start hello upload.
      String fullFileName = System.getProperty("user.dir") + File.separator + fileName;
      uploadFile(fullFileName);
      System.out.println("File upload started with success");
    }
    catch (Exception e)
    {
      System.out.println("Exception uploading file: " + e.getCause() + " \nERROR: " + e.getMessage());
    }

    MessageSender sender = new MessageSender();
    ```

1. Użyj hello następujące polecenie toobuild hello **symulowane urządzenie** aplikacji i sprawdź, czy błędy:

    ```cmd/sh
    mvn clean package -DskipTests
    ```

## <a name="receive-a-file-upload-notification"></a>Otrzymasz powiadomienie przekazywania pliku

W tej sekcji utworzysz aplikację konsoli języka Java, która odbiera komunikaty powiadomień dotyczących przekazywania plików z Centrum IoT.

Należy hello **iothubowner** parametrów połączenia dla Twojego toocomplete Centrum IoT w tej sekcji. Parametry połączenia hello można znaleźć w hello [portalu Azure](https://portal.azure.com/) na powitania **zasady dostępu współużytkowanego** bloku.

1. Utwórz projekt Maven o nazwie **odczytu pliku przekazywania powiadomień** przy użyciu hello następujące polecenie z wiersza polecenia. Należy zauważyć, że to polecenie jest pojedynczą, długie polecenie:

    ```cmd/sh
    mvn archetype:generate -DgroupId=com.mycompany.app -DartifactId=read-file-upload-notification -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false
    ```

1. Wierszu polecenia przejdź toohello nowe `read-file-upload-notification` folderu.

1. Za pomocą edytora tekstu, otwórz hello `pom.xml` pliku w hello `read-file-upload-notification` folderu i dodaj następujące zależności toohello hello **zależności** węzła. Dodawanie zależności hello umożliwia toouse hello **Centrum iothub-java--klient usługi** pakiet w Twojej toocommunicate aplikacji z usługą Centrum IoT:

    ```xml
    <dependency>
      <groupId>com.microsoft.azure.sdk.iot</groupId>
      <artifactId>iot-service-client</artifactId>
      <version>1.7.23</version>
    </dependency>
    ```

    > [!NOTE]
    > Możesz sprawdzić hello najnowszą wersję **klienta w przypadku usługi iot** przy użyciu [wyszukiwania Maven](http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22iot-service-client%22%20g%3A%22com.microsoft.azure.sdk.iot%22).

1. Zapisz i zamknij hello `pom.xml` pliku.

1. Za pomocą edytora tekstu, otwórz hello `read-file-upload-notification\src\main\java\com\mycompany\app\App.java` pliku.

1. Dodaj następujące hello **zaimportować** instrukcje toohello pliku:

    ```java
    import com.microsoft.azure.sdk.iot.service.*;
    import java.io.IOException;
    import java.net.URISyntaxException;
    import java.util.concurrent.ExecutorService;
    import java.util.concurrent.Executors;
    ```

1. Dodaj następujące zmienne klasy toohello hello **aplikacji** klasy:

    ```java
    private static final String connectionString = "{Your IoT Hub connection string}";
    private static final IotHubServiceClientProtocol protocol = IotHubServiceClientProtocol.AMQPS;
    private static FileUploadNotificationReceiver fileUploadNotificationReceiver = null;
    ```

1. tooprint informacji na temat konsoli toohello przekazywania plików hello, Dodaj następujące hello zagnieżdżona klasa toohello **aplikacji** klasy:

    ```java
    // Create a thread tooreceive file upload notifications.
    private static class ShowFileUploadNotifications implements Runnable {
      public void run() {
        try {
          while (true) {
            System.out.println("Recieve file upload notifications...");
            FileUploadNotification fileUploadNotification = fileUploadNotificationReceiver.receive();
            if (fileUploadNotification != null) {
              System.out.println("File Upload notification received");
              System.out.println("Device Id : " + fileUploadNotification.getDeviceId());
              System.out.println("Blob Uri: " + fileUploadNotification.getBlobUri());
              System.out.println("Blob Name: " + fileUploadNotification.getBlobName());
              System.out.println("Last Updated : " + fileUploadNotification.getLastUpdatedTimeDate());
              System.out.println("Blob Size (Bytes): " + fileUploadNotification.getBlobSizeInBytes());
              System.out.println("Enqueued Time: " + fileUploadNotification.getEnqueuedTimeUtcDate());
            }
          }
        } catch (Exception ex) {
          System.out.println("Exception reading reported properties: " + ex.getMessage());
        }
      }
    }
    ```

1. toostart hello wątku, który odbiera powiadomienia o przekazywania plików, dodawanie hello następującego kodu toohello **głównego** metody:

    ```java
    public static void main(String[] args) throws IOException, URISyntaxException, Exception {
      ServiceClient serviceClient = ServiceClient.createFromConnectionString(connectionString, protocol);

      if (serviceClient != null) {
        serviceClient.open();

        // Get a file upload notification receiver from hello ServiceClient.
        fileUploadNotificationReceiver = serviceClient.getFileUploadNotificationReceiver();
        fileUploadNotificationReceiver.open();

        // Start hello thread tooreceive file upload notifications.
        ShowFileUploadNotifications showFileUploadNotifications = new ShowFileUploadNotifications();
        ExecutorService executor = Executors.newFixedThreadPool(1);
        executor.execute(showFileUploadNotifications);

        System.out.println("Press ENTER tooexit.");
        System.in.read();
        executor.shutdownNow();
        System.out.println("Shutting down sample...");
        fileUploadNotificationReceiver.close();
        serviceClient.close();
      }
    }
    ```

1. Zapisz i zamknij hello `read-file-upload-notification\src\main\java\com\mycompany\app\App.java` pliku.

1. Użyj hello następujące polecenie toobuild hello **odczytu pliku przekazywania powiadomień** aplikacji i sprawdź, czy błędy:

    ```cmd/sh
    mvn clean package -DskipTests
    ```

## <a name="run-hello-applications"></a>Uruchamianie aplikacji hello

Teraz wszystko jest gotowe toorun hello aplikacji.

W wierszu polecenia w hello `read-file-upload-notification` folderu, uruchom następujące polecenie hello:

```cmd/sh
mvn exec:java -Dexec.mainClass="com.mycompany.app.App"
```

W wierszu polecenia w hello `simulated-device` folderu, uruchom następujące polecenie hello:

```cmd/sh
mvn exec:java -Dexec.mainClass="com.mycompany.app.App"
```

Witaj Poniższy zrzut ekranu przedstawia dane wyjściowe hello hello **symulowane urządzenie** aplikacji:

![Dane wyjściowe z aplikacji symulowane urządzenie](media/iot-hub-java-java-upload/simulated-device.png)

Witaj Poniższy zrzut ekranu przedstawia dane wyjściowe hello hello **odczytu pliku przekazywania powiadomień** aplikacji:

![Dane wyjściowe z aplikacji odczytu pliku przekazywania — powiadomienie](media/iot-hub-java-java-upload/read-file-upload-notification.png)

Program hello portalu tooview hello przekazany plik w hello kontenera magazynu, które zostały skonfigurowane:

![Przekazany plik](media/iot-hub-java-java-upload/uploaded-file.png)

## <a name="next-steps"></a>Następne kroki

W tym samouczku przedstawiono, jak plik hello toouse przekazać możliwości przekazywania plików toosimplify z urządzeń Centrum IoT. Można kontynuować scenariusze i funkcje Centrum IoT tooexplore hello następujące artykuły:

* [Programowo tworzenia Centrum IoT][lnk-create-hub]
* [Wprowadzenie tooC zestawu SDK][lnk-c-sdk]
* [Zestawy SDK Azure IoT][lnk-sdks]

toofurther Poznaj możliwości hello Centrum IoT, zobacz:

* [Symuluje urządzenia IoT krawędzi][lnk-iotedge]

<!-- Images. -->

[50]: ./media/iot-hub-csharp-csharp-file-upload/run-apps1.png
[1]: ./media/iot-hub-csharp-csharp-file-upload/image-properties.png
[2]: ./media/iot-hub-csharp-csharp-file-upload/file-upload-project-csharp1.png
[3]: ./media/iot-hub-csharp-csharp-file-upload/enable-file-notifications.png

<!-- Links -->



[Azure IoT Developer Center]: http://www.azure.com/develop/iot

[Transient Fault Handling]: https://msdn.microsoft.com/library/hh680901(v=pandp.50).aspx
[Azure Storage]:../storage/common/storage-create-storage-account.md#create-a-storage-account
[lnk-configure-upload]: iot-hub-configure-file-upload.md
[Azure IoT service SDK NuGet package]: https://www.nuget.org/packages/Microsoft.Azure.Devices/
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/

[lnk-create-hub]: iot-hub-rm-template-powershell.md
[lnk-c-sdk]: iot-hub-device-sdk-c-intro.md
[lnk-sdks]: iot-hub-devguide-sdks.md

[lnk-iotedge]: iot-hub-windows-iot-edge-simulated-device.md


