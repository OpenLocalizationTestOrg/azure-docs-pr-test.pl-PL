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
# <a name="upload-files-from-your-device-toohello-cloud-with-iot-hub"></a><span data-ttu-id="28d44-104">Przekazywanie plików z chmury toohello urządzenie z Centrum IoT</span><span class="sxs-lookup"><span data-stu-id="28d44-104">Upload files from your device toohello cloud with IoT Hub</span></span>

[!INCLUDE [iot-hub-file-upload-language-selector](../../includes/iot-hub-file-upload-language-selector.md)]

<span data-ttu-id="28d44-105">W tym samouczku opiera się na powitania kodu w hello [wysyłać chmury do urządzenia z Centrum IoT](iot-hub-java-java-c2d.md) tooshow samouczka możesz jak toouse hello [pliku możliwości przekazywania Centrum IoT](iot-hub-devguide-file-upload.md) tooupload pliku zbyt[ Magazyn obiektów blob platformy Azure](../storage/index.md).</span><span class="sxs-lookup"><span data-stu-id="28d44-105">This tutorial builds on hello code in hello [Send Cloud-to-Device messages with IoT Hub](iot-hub-java-java-c2d.md) tutorial tooshow you how toouse hello [file upload capabilities of IoT Hub](iot-hub-devguide-file-upload.md) tooupload a file too[Azure blob storage](../storage/index.md).</span></span> <span data-ttu-id="28d44-106">Witaj samouczek pokazuje, jak do:</span><span class="sxs-lookup"><span data-stu-id="28d44-106">hello tutorial shows you how to:</span></span>

- <span data-ttu-id="28d44-107">Bezpieczne udostępnianie urządzenia platformy Azure blob identyfikatora URI pobierania pliku.</span><span class="sxs-lookup"><span data-stu-id="28d44-107">Securely provide a device with an Azure blob URI for uploading a file.</span></span>
- <span data-ttu-id="28d44-108">Użyj hello pliku hello Centrum IoT pliku przekazywania powiadomień tootrigger przetwarzania w sieci wewnętrznej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="28d44-108">Use hello IoT Hub file upload notifications tootrigger processing hello file in your app back end.</span></span>

<span data-ttu-id="28d44-109">Witaj [Rozpoczynanie pracy z Centrum IoT](iot-hub-java-java-getstarted.md) i [wysyłać chmury do urządzenia z Centrum IoT](iot-hub-java-java-c2d.md) samouczki przedstawiają hello podstawowych urządzenia do chmury i chmury do urządzenia obsługi funkcji Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="28d44-109">hello [Get started with IoT Hub](iot-hub-java-java-getstarted.md) and [Send Cloud-to-Device messages with IoT Hub](iot-hub-java-java-c2d.md) tutorials show hello basic device-to-cloud and cloud-to-device messaging functionality of IoT Hub.</span></span> <span data-ttu-id="28d44-110">Witaj [wiadomości procesu urządzenia do chmury](iot-hub-java-java-process-d2c.md) samouczek przedstawia sposób tooreliably magazynu urządzenia do chmury wiadomości w magazynie obiektów blob platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="28d44-110">hello [Process Device-to-Cloud messages](iot-hub-java-java-process-d2c.md) tutorial describes a way tooreliably store device-to-cloud messages in Azure blob storage.</span></span> <span data-ttu-id="28d44-111">Jednak w niektórych scenariuszach nie można łatwo mapować hello dane, które urządzenia wysłać w wiadomości powitania od stosunkowo mały urządzenia do chmury, które akceptuje Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="28d44-111">However, in some scenarios you cannot easily map hello data your devices send into hello relatively small device-to-cloud messages that IoT Hub accepts.</span></span> <span data-ttu-id="28d44-112">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="28d44-112">For example:</span></span>

* <span data-ttu-id="28d44-113">Duże pliki, które zawierają obrazów</span><span class="sxs-lookup"><span data-stu-id="28d44-113">Large files that contain images</span></span>
* <span data-ttu-id="28d44-114">Filmy wideo</span><span class="sxs-lookup"><span data-stu-id="28d44-114">Videos</span></span>
* <span data-ttu-id="28d44-115">Dane wibrację próbkowanych zgodnie o dużej częstotliwości</span><span class="sxs-lookup"><span data-stu-id="28d44-115">Vibration data sampled at high frequency</span></span>
* <span data-ttu-id="28d44-116">Niektóre formularz wstępnie przetworzonych danych.</span><span class="sxs-lookup"><span data-stu-id="28d44-116">Some form of preprocessed data.</span></span>

<span data-ttu-id="28d44-117">Pliki te są zwykle partii przetwarzania w chmurze hello za pomocą narzędzi takich jak [fabryki danych Azure](../data-factory/index.md) lub hello [Hadoop](../hdinsight/index.md) stosu.</span><span class="sxs-lookup"><span data-stu-id="28d44-117">These files are typically batch processed in hello cloud using tools such as [Azure Data Factory](../data-factory/index.md) or hello [Hadoop](../hdinsight/index.md) stack.</span></span> <span data-ttu-id="28d44-118">Jeśli potrzebujesz tooupland pliki z urządzenia, można nadal używać hello bezpieczeństwa i niezawodności Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="28d44-118">When you need tooupland files from a device, you can still use hello security and reliability of IoT Hub.</span></span>

<span data-ttu-id="28d44-119">Na końcu hello tego samouczka możesz uruchomić dwie aplikacje konsoli Java:</span><span class="sxs-lookup"><span data-stu-id="28d44-119">At hello end of this tutorial you run two Java console apps:</span></span>

* <span data-ttu-id="28d44-120">**Symulowane urządzenie**, zmodyfikowanej wersji aplikacji hello utworzonej w samouczku hello [chmury urządzenia wysyłania wiadomości z Centrum IoT].</span><span class="sxs-lookup"><span data-stu-id="28d44-120">**simulated-device**, a modified version of hello app created in hello [Send Cloud-to-Device messages with IoT Hub] tutorial.</span></span> <span data-ttu-id="28d44-121">Ta aplikacja będzie przekazywać toostorage plików, przy użyciu identyfikatora URI połączenia SAS udostępniane przez Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="28d44-121">This app uploads a file toostorage using a SAS URI provided by your IoT hub.</span></span>
* <span data-ttu-id="28d44-122">**Odczyt pliku przekazywania powiadomień**, która odbiera powiadomienia o przekazywania plików z Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="28d44-122">**read-file-upload-notification**, which receives file upload notifications from your IoT hub.</span></span>

> [!NOTE]
> <span data-ttu-id="28d44-123">Centrum IoT obsługuje wiele platform urządzeń i języków (w tym C, .NET i Javascript) za pomocą urządzenia Azure IoT zestawów SDK.</span><span class="sxs-lookup"><span data-stu-id="28d44-123">IoT Hub supports many device platforms and languages (including C, .NET, and Javascript) through Azure IoT device SDKs.</span></span> <span data-ttu-id="28d44-124">Zobacz toohello [Azure IoT Developer Center] instrukcje krok po kroku na temat tooconnect tooAzure Twojego urządzenia IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="28d44-124">Refer toohello [Azure IoT Developer Center] for step-by-step instructions on how tooconnect your device tooAzure IoT Hub.</span></span>

<span data-ttu-id="28d44-125">toocomplete tego samouczka należy hello następujące:</span><span class="sxs-lookup"><span data-stu-id="28d44-125">toocomplete this tutorial, you need hello following:</span></span>

* <span data-ttu-id="28d44-126">Witaj najnowszych [Java SE Development Kit 8](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)</span><span class="sxs-lookup"><span data-stu-id="28d44-126">hello latest [Java SE Development Kit 8](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)</span></span>
* [<span data-ttu-id="28d44-127">Maven 3</span><span class="sxs-lookup"><span data-stu-id="28d44-127">Maven 3</span></span>](https://maven.apache.org/install.html)
* <span data-ttu-id="28d44-128">Aktywne konto platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="28d44-128">An active Azure account.</span></span> <span data-ttu-id="28d44-129">(Jeśli nie masz konta, możesz utworzyć [bezpłatne konto](http://azure.microsoft.com/pricing/free-trial/) w zaledwie kilka minut.)</span><span class="sxs-lookup"><span data-stu-id="28d44-129">(If you don't have an account, you can create a [free account](http://azure.microsoft.com/pricing/free-trial/) in just a couple of minutes.)</span></span>

[!INCLUDE [iot-hub-associate-storage](../../includes/iot-hub-associate-storage.md)]

## <a name="upload-a-file-from-a-device-app"></a><span data-ttu-id="28d44-130">Przekaż plik z aplikacji przez urządzenia</span><span class="sxs-lookup"><span data-stu-id="28d44-130">Upload a file from a device app</span></span>

<span data-ttu-id="28d44-131">W tej sekcji możesz zmodyfikować aplikację urządzenia hello utworzony w [wysyłać chmury do urządzenia z Centrum IoT](iot-hub-java-java-c2d.md) tooupload Centrum tooIoT pliku.</span><span class="sxs-lookup"><span data-stu-id="28d44-131">In this section, you modify hello device app you created in [Send Cloud-to-Device messages with IoT Hub](iot-hub-java-java-c2d.md) tooupload a file tooIoT hub.</span></span>

1. <span data-ttu-id="28d44-132">Kopiowanie obrazu pliku toohello `simulated-device` folder i zmień jego nazwę `myimage.png`.</span><span class="sxs-lookup"><span data-stu-id="28d44-132">Copy an image file toohello `simulated-device` folder and rename it `myimage.png`.</span></span>

1. <span data-ttu-id="28d44-133">Za pomocą edytora tekstu, otwórz hello `simulated-device\src\main\java\com\mycompany\app\App.java` pliku.</span><span class="sxs-lookup"><span data-stu-id="28d44-133">Using a text editor, open hello `simulated-device\src\main\java\com\mycompany\app\App.java` file.</span></span>

1. <span data-ttu-id="28d44-134">Dodaj hello deklaracja zmiennej toohello **aplikacji** klasy:</span><span class="sxs-lookup"><span data-stu-id="28d44-134">Add hello variable declaration toohello **App** class:</span></span>

    ```java
    private static String fileName = "myimage.png";
    ```

1. <span data-ttu-id="28d44-135">tooprocess wywołania zwrotnego komunikatach przekazywania pliku, Dodaj następujące hello zagnieżdżona klasa toohello **aplikacji** klasy:</span><span class="sxs-lookup"><span data-stu-id="28d44-135">tooprocess file upload status callback messages, add hello following nested class toohello **App** class:</span></span>

    ```java
    // Define a callback method tooprint status codes from IoT Hub.
    protected static class FileUploadStatusCallBack implements IotHubEventCallback {
      public void execute(IotHubStatusCode status, Object context) {
        System.out.println("IoT Hub responded toofile upload for " + fileName
            + " operation with status " + status.name());
      }
    }
    ```

1. <span data-ttu-id="28d44-136">tooupload obrazów tooIoT koncentratora, Dodaj hello następujące metody toohello **aplikacji** tooupload klasy obrazy tooIoT Centrum:</span><span class="sxs-lookup"><span data-stu-id="28d44-136">tooupload images tooIoT Hub, add hello following method toohello **App** class tooupload images tooIoT Hub:</span></span>

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

1. <span data-ttu-id="28d44-137">Modyfikowanie hello **głównego** hello toocall — metoda **uploadFile** metody pokazane na powitania po fragment kodu:</span><span class="sxs-lookup"><span data-stu-id="28d44-137">Modify hello **main** method toocall hello **uploadFile** method as shown in hello following snippet:</span></span>

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

1. <span data-ttu-id="28d44-138">Użyj hello następujące polecenie toobuild hello **symulowane urządzenie** aplikacji i sprawdź, czy błędy:</span><span class="sxs-lookup"><span data-stu-id="28d44-138">Use hello following command toobuild hello **simulated-device** app and check for errors:</span></span>

    ```cmd/sh
    mvn clean package -DskipTests
    ```

## <a name="receive-a-file-upload-notification"></a><span data-ttu-id="28d44-139">Otrzymasz powiadomienie przekazywania pliku</span><span class="sxs-lookup"><span data-stu-id="28d44-139">Receive a file upload notification</span></span>

<span data-ttu-id="28d44-140">W tej sekcji utworzysz aplikację konsoli języka Java, która odbiera komunikaty powiadomień dotyczących przekazywania plików z Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="28d44-140">In this section, you create a Java console app that receives file upload notification messages from IoT Hub.</span></span>

<span data-ttu-id="28d44-141">Należy hello **iothubowner** parametrów połączenia dla Twojego toocomplete Centrum IoT w tej sekcji.</span><span class="sxs-lookup"><span data-stu-id="28d44-141">You need hello **iothubowner** connection string for your IoT Hub toocomplete this section.</span></span> <span data-ttu-id="28d44-142">Parametry połączenia hello można znaleźć w hello [portalu Azure](https://portal.azure.com/) na powitania **zasady dostępu współużytkowanego** bloku.</span><span class="sxs-lookup"><span data-stu-id="28d44-142">You can find hello connection string in hello [Azure portal](https://portal.azure.com/) on hello **Shared access policy** blade.</span></span>

1. <span data-ttu-id="28d44-143">Utwórz projekt Maven o nazwie **odczytu pliku przekazywania powiadomień** przy użyciu hello następujące polecenie z wiersza polecenia.</span><span class="sxs-lookup"><span data-stu-id="28d44-143">Create a Maven project called **read-file-upload-notification** using hello following command at your command prompt.</span></span> <span data-ttu-id="28d44-144">Należy zauważyć, że to polecenie jest pojedynczą, długie polecenie:</span><span class="sxs-lookup"><span data-stu-id="28d44-144">Note this command is a single, long command:</span></span>

    ```cmd/sh
    mvn archetype:generate -DgroupId=com.mycompany.app -DartifactId=read-file-upload-notification -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false
    ```

1. <span data-ttu-id="28d44-145">Wierszu polecenia przejdź toohello nowe `read-file-upload-notification` folderu.</span><span class="sxs-lookup"><span data-stu-id="28d44-145">At your command prompt, navigate toohello new `read-file-upload-notification` folder.</span></span>

1. <span data-ttu-id="28d44-146">Za pomocą edytora tekstu, otwórz hello `pom.xml` pliku w hello `read-file-upload-notification` folderu i dodaj następujące zależności toohello hello **zależności** węzła.</span><span class="sxs-lookup"><span data-stu-id="28d44-146">Using a text editor, open hello `pom.xml` file in hello `read-file-upload-notification` folder and add hello following dependency toohello **dependencies** node.</span></span> <span data-ttu-id="28d44-147">Dodawanie zależności hello umożliwia toouse hello **Centrum iothub-java--klient usługi** pakiet w Twojej toocommunicate aplikacji z usługą Centrum IoT:</span><span class="sxs-lookup"><span data-stu-id="28d44-147">Adding hello dependency enables you toouse hello **iothub-java-service-client** package in your application toocommunicate with your IoT hub service:</span></span>

    ```xml
    <dependency>
      <groupId>com.microsoft.azure.sdk.iot</groupId>
      <artifactId>iot-service-client</artifactId>
      <version>1.7.23</version>
    </dependency>
    ```

    > [!NOTE]
    > <span data-ttu-id="28d44-148">Możesz sprawdzić hello najnowszą wersję **klienta w przypadku usługi iot** przy użyciu [wyszukiwania Maven](http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22iot-service-client%22%20g%3A%22com.microsoft.azure.sdk.iot%22).</span><span class="sxs-lookup"><span data-stu-id="28d44-148">You can check for hello latest version of **iot-service-client** using [Maven search](http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22iot-service-client%22%20g%3A%22com.microsoft.azure.sdk.iot%22).</span></span>

1. <span data-ttu-id="28d44-149">Zapisz i zamknij hello `pom.xml` pliku.</span><span class="sxs-lookup"><span data-stu-id="28d44-149">Save and close hello `pom.xml` file.</span></span>

1. <span data-ttu-id="28d44-150">Za pomocą edytora tekstu, otwórz hello `read-file-upload-notification\src\main\java\com\mycompany\app\App.java` pliku.</span><span class="sxs-lookup"><span data-stu-id="28d44-150">Using a text editor, open hello `read-file-upload-notification\src\main\java\com\mycompany\app\App.java` file.</span></span>

1. <span data-ttu-id="28d44-151">Dodaj następujące hello **zaimportować** instrukcje toohello pliku:</span><span class="sxs-lookup"><span data-stu-id="28d44-151">Add hello following **import** statements toohello file:</span></span>

    ```java
    import com.microsoft.azure.sdk.iot.service.*;
    import java.io.IOException;
    import java.net.URISyntaxException;
    import java.util.concurrent.ExecutorService;
    import java.util.concurrent.Executors;
    ```

1. <span data-ttu-id="28d44-152">Dodaj następujące zmienne klasy toohello hello **aplikacji** klasy:</span><span class="sxs-lookup"><span data-stu-id="28d44-152">Add hello following class-level variables toohello **App** class:</span></span>

    ```java
    private static final String connectionString = "{Your IoT Hub connection string}";
    private static final IotHubServiceClientProtocol protocol = IotHubServiceClientProtocol.AMQPS;
    private static FileUploadNotificationReceiver fileUploadNotificationReceiver = null;
    ```

1. <span data-ttu-id="28d44-153">tooprint informacji na temat konsoli toohello przekazywania plików hello, Dodaj następujące hello zagnieżdżona klasa toohello **aplikacji** klasy:</span><span class="sxs-lookup"><span data-stu-id="28d44-153">tooprint information about hello file upload toohello console, add hello following nested class toohello **App** class:</span></span>

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

1. <span data-ttu-id="28d44-154">toostart hello wątku, który odbiera powiadomienia o przekazywania plików, dodawanie hello następującego kodu toohello **głównego** metody:</span><span class="sxs-lookup"><span data-stu-id="28d44-154">toostart hello thread that listens for file upload notifications, add hello following code toohello **main** method:</span></span>

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

1. <span data-ttu-id="28d44-155">Zapisz i zamknij hello `read-file-upload-notification\src\main\java\com\mycompany\app\App.java` pliku.</span><span class="sxs-lookup"><span data-stu-id="28d44-155">Save and close hello `read-file-upload-notification\src\main\java\com\mycompany\app\App.java` file.</span></span>

1. <span data-ttu-id="28d44-156">Użyj hello następujące polecenie toobuild hello **odczytu pliku przekazywania powiadomień** aplikacji i sprawdź, czy błędy:</span><span class="sxs-lookup"><span data-stu-id="28d44-156">Use hello following command toobuild hello **read-file-upload-notification** app and check for errors:</span></span>

    ```cmd/sh
    mvn clean package -DskipTests
    ```

## <a name="run-hello-applications"></a><span data-ttu-id="28d44-157">Uruchamianie aplikacji hello</span><span class="sxs-lookup"><span data-stu-id="28d44-157">Run hello applications</span></span>

<span data-ttu-id="28d44-158">Teraz wszystko jest gotowe toorun hello aplikacji.</span><span class="sxs-lookup"><span data-stu-id="28d44-158">Now you are ready toorun hello applications.</span></span>

<span data-ttu-id="28d44-159">W wierszu polecenia w hello `read-file-upload-notification` folderu, uruchom następujące polecenie hello:</span><span class="sxs-lookup"><span data-stu-id="28d44-159">At a command prompt in hello `read-file-upload-notification` folder, run hello following command:</span></span>

```cmd/sh
mvn exec:java -Dexec.mainClass="com.mycompany.app.App"
```

<span data-ttu-id="28d44-160">W wierszu polecenia w hello `simulated-device` folderu, uruchom następujące polecenie hello:</span><span class="sxs-lookup"><span data-stu-id="28d44-160">At a command prompt in hello `simulated-device` folder, run hello following command:</span></span>

```cmd/sh
mvn exec:java -Dexec.mainClass="com.mycompany.app.App"
```

<span data-ttu-id="28d44-161">Witaj Poniższy zrzut ekranu przedstawia dane wyjściowe hello hello **symulowane urządzenie** aplikacji:</span><span class="sxs-lookup"><span data-stu-id="28d44-161">hello following screenshot shows hello output from hello **simulated-device** app:</span></span>

![Dane wyjściowe z aplikacji symulowane urządzenie](media/iot-hub-java-java-upload/simulated-device.png)

<span data-ttu-id="28d44-163">Witaj Poniższy zrzut ekranu przedstawia dane wyjściowe hello hello **odczytu pliku przekazywania powiadomień** aplikacji:</span><span class="sxs-lookup"><span data-stu-id="28d44-163">hello following screenshot shows hello output from hello **read-file-upload-notification** app:</span></span>

![Dane wyjściowe z aplikacji odczytu pliku przekazywania — powiadomienie](media/iot-hub-java-java-upload/read-file-upload-notification.png)

<span data-ttu-id="28d44-165">Program hello portalu tooview hello przekazany plik w hello kontenera magazynu, które zostały skonfigurowane:</span><span class="sxs-lookup"><span data-stu-id="28d44-165">You can use hello portal tooview hello uploaded file in hello storage container you configured:</span></span>

![Przekazany plik](media/iot-hub-java-java-upload/uploaded-file.png)

## <a name="next-steps"></a><span data-ttu-id="28d44-167">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="28d44-167">Next steps</span></span>

<span data-ttu-id="28d44-168">W tym samouczku przedstawiono, jak plik hello toouse przekazać możliwości przekazywania plików toosimplify z urządzeń Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="28d44-168">In this tutorial, you learned how toouse hello file upload capabilities of IoT Hub toosimplify file uploads from devices.</span></span> <span data-ttu-id="28d44-169">Można kontynuować scenariusze i funkcje Centrum IoT tooexplore hello następujące artykuły:</span><span class="sxs-lookup"><span data-stu-id="28d44-169">You can continue tooexplore IoT hub features and scenarios with hello following articles:</span></span>

* <span data-ttu-id="28d44-170">[Programowo tworzenia Centrum IoT][lnk-create-hub]</span><span class="sxs-lookup"><span data-stu-id="28d44-170">[Create an IoT hub programmatically][lnk-create-hub]</span></span>
* <span data-ttu-id="28d44-171">[Wprowadzenie tooC zestawu SDK][lnk-c-sdk]</span><span class="sxs-lookup"><span data-stu-id="28d44-171">[Introduction tooC SDK][lnk-c-sdk]</span></span>
* <span data-ttu-id="28d44-172">[Zestawy SDK Azure IoT][lnk-sdks]</span><span class="sxs-lookup"><span data-stu-id="28d44-172">[Azure IoT SDKs][lnk-sdks]</span></span>

<span data-ttu-id="28d44-173">toofurther Poznaj możliwości hello Centrum IoT, zobacz:</span><span class="sxs-lookup"><span data-stu-id="28d44-173">toofurther explore hello capabilities of IoT Hub, see:</span></span>

* <span data-ttu-id="28d44-174">[Symuluje urządzenia IoT krawędzi][lnk-iotedge]</span><span class="sxs-lookup"><span data-stu-id="28d44-174">[Simulating a device with IoT Edge][lnk-iotedge]</span></span>

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


