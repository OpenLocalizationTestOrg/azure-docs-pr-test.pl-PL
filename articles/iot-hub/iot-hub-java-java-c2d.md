---
title: "komunikaty aaaCloud do urządzenia z Centrum IoT Azure (Java) | Dokumentacja firmy Microsoft"
description: "Jak chmury urządzenia toosend komunikatów tooa urządzenia z Centrum Azure IoT przy użyciu hello Azure IoT SDK dla języka Java. Modyfikowanie komunikatów chmury do urządzenia symulowane urządzenie aplikacji tooreceive i modyfikowanie aplikacji zaplecza toosend hello chmury do urządzenia komunikatów."
services: iot-hub
documentationcenter: java
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 7f785ea8-e7c2-40c5-87ef-96525e9b9e1e
ms.service: iot-hub
ms.devlang: java
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/28/2017
ms.author: dobett
ms.openlocfilehash: 8721f18428c849ed9a04aa2e45c65605c3e38101
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="send-cloud-to-device-messages-with-iot-hub-java"></a><span data-ttu-id="c2b6e-104">Wysyłanie komunikatów chmury do urządzenia z Centrum IoT (Java)</span><span class="sxs-lookup"><span data-stu-id="c2b6e-104">Send cloud-to-device messages with IoT Hub (Java)</span></span>
[!INCLUDE [iot-hub-selector-c2d](../../includes/iot-hub-selector-c2d.md)]

<span data-ttu-id="c2b6e-105">Centrum IoT Azure jest w pełni zarządzaną usługę, która umożliwia włączanie i niezawodności komunikację dwukierunkową między milionów urządzeń i zaplecze rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="c2b6e-105">Azure IoT Hub is a fully managed service that helps enable reliable and secure bi-directional communications between millions of devices and a solution back end.</span></span> <span data-ttu-id="c2b6e-106">Witaj [Rozpoczynanie pracy z Centrum IoT] samouczek pokazuje, jak udostępnić tożsamość urządzenia w nim toocreate Centrum IoT i kodu aplikacji symulowane urządzenie, który wysyła wiadomości urządzenia do chmury.</span><span class="sxs-lookup"><span data-stu-id="c2b6e-106">hello [Get started with IoT Hub] tutorial shows how toocreate an IoT hub, provision a device identity in it, and code a simulated device app that sends device-to-cloud messages.</span></span>

<span data-ttu-id="c2b6e-107">W tym samouczku opiera się na [Rozpoczynanie pracy z Centrum IoT].</span><span class="sxs-lookup"><span data-stu-id="c2b6e-107">This tutorial builds on [Get started with IoT Hub].</span></span> <span data-ttu-id="c2b6e-108">Jak przedstawiono na:</span><span class="sxs-lookup"><span data-stu-id="c2b6e-108">It shows you how to:</span></span>

* <span data-ttu-id="c2b6e-109">Z z zaplecza rozwiązania należy wysłać pojedyncze urządzenie tooa wiadomości chmury do urządzenia za pośrednictwem Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="c2b6e-109">From your solution back end, send cloud-to-device messages tooa single device through IoT Hub.</span></span>
* <span data-ttu-id="c2b6e-110">Komunikaty chmury do urządzenia na urządzeniu.</span><span class="sxs-lookup"><span data-stu-id="c2b6e-110">Receive cloud-to-device messages on a device.</span></span>
* <span data-ttu-id="c2b6e-111">Z sieci zaplecza rozwiązania, żądania potwierdzenia dostarczenia (*opinii*) dla wiadomości wysyłane tooa urządzenie z Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="c2b6e-111">From your solution back end, request delivery acknowledgement (*feedback*) for messages sent tooa device from IoT Hub.</span></span>

<span data-ttu-id="c2b6e-112">Więcej informacji na temat wiadomości chmury do urządzenia można znaleźć w hello [Centrum IoT — przewodnik dewelopera][IoT Hub developer guide - C2D].</span><span class="sxs-lookup"><span data-stu-id="c2b6e-112">You can find more information on cloud-to-device messages in hello [IoT Hub developer guide][IoT Hub developer guide - C2D].</span></span>

<span data-ttu-id="c2b6e-113">Na końcu hello tego samouczka możesz uruchomić dwie aplikacje konsoli Java:</span><span class="sxs-lookup"><span data-stu-id="c2b6e-113">At hello end of this tutorial, you run two Java console apps:</span></span>

* <span data-ttu-id="c2b6e-114">**Symulowane urządzenie**, zmodyfikowanej wersji aplikacji hello utworzone w [Rozpoczynanie pracy z Centrum IoT], która łączy się z Centrum IoT tooyour i odbiera komunikaty chmury do urządzenia.</span><span class="sxs-lookup"><span data-stu-id="c2b6e-114">**simulated-device**, a modified version of hello app created in [Get started with IoT Hub], which connects tooyour IoT hub and receives cloud-to-device messages.</span></span>
* <span data-ttu-id="c2b6e-115">**send — c2d — liczba komunikatów**, który wysyła aplikacji symulowane urządzenie toohello komunikat chmury do urządzenia, za pośrednictwem Centrum IoT i następnie odbiera jego potwierdzenia dostarczenia.</span><span class="sxs-lookup"><span data-stu-id="c2b6e-115">**send-c2d-messages**, which sends a cloud-to-device message toohello simulated device app through IoT Hub, and then receives its delivery acknowledgement.</span></span>

> [!NOTE]
> <span data-ttu-id="c2b6e-116">Centrum IoT obsługuje zestawu SDK dla wielu platform urządzeń i języków (w tym C, Java i Javascript) za pośrednictwem zestawy SDK urządzenia Azure IoT.</span><span class="sxs-lookup"><span data-stu-id="c2b6e-116">IoT Hub has SDK support for many device platforms and languages (including C, Java, and Javascript) through Azure IoT device SDKs.</span></span> <span data-ttu-id="c2b6e-117">Instrukcje krok po kroku dotyczące tooconnect samouczek toothis urządzenia kodu i zazwyczaj tooAzure Centrum IoT, zobacz temat hello [Azure IoT Developer Center].</span><span class="sxs-lookup"><span data-stu-id="c2b6e-117">For step-by-step instructions on how tooconnect your device toothis tutorial's code, and generally tooAzure IoT Hub, see hello [Azure IoT Developer Center].</span></span>

<span data-ttu-id="c2b6e-118">toocomplete tego samouczka należy hello następujące:</span><span class="sxs-lookup"><span data-stu-id="c2b6e-118">toocomplete this tutorial, you need hello following:</span></span>

* <span data-ttu-id="c2b6e-119">Pełną wersję pracy hello [Rozpoczynanie pracy z Centrum IoT](iot-hub-java-java-getstarted.md) lub [wiadomości urządzenia do chmury Centrum IoT procesu](iot-hub-java-java-process-d2c.md) samouczka.</span><span class="sxs-lookup"><span data-stu-id="c2b6e-119">A complete working version of hello [Get started with IoT Hub](iot-hub-java-java-getstarted.md) or [Process IoT Hub device-to-cloud messages](iot-hub-java-java-process-d2c.md) tutorial.</span></span>
* <span data-ttu-id="c2b6e-120">Witaj najnowszych [Java SE Development Kit 8](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)</span><span class="sxs-lookup"><span data-stu-id="c2b6e-120">hello latest [Java SE Development Kit 8](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)</span></span>
* [<span data-ttu-id="c2b6e-121">Maven 3</span><span class="sxs-lookup"><span data-stu-id="c2b6e-121">Maven 3</span></span>](https://maven.apache.org/install.html)
* <span data-ttu-id="c2b6e-122">Aktywne konto platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="c2b6e-122">An active Azure account.</span></span> <span data-ttu-id="c2b6e-123">(Jeśli go nie masz, możesz utworzyć [bezpłatne konto próbne][lnk-free-trial] w zaledwie kilka minut).</span><span class="sxs-lookup"><span data-stu-id="c2b6e-123">(If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.)</span></span>

## <a name="receive-messages-in-hello-simulated-device-app"></a><span data-ttu-id="c2b6e-124">Odbieranie komunikatów w aplikacji symulowane urządzenie hello</span><span class="sxs-lookup"><span data-stu-id="c2b6e-124">Receive messages in hello simulated device app</span></span>

<span data-ttu-id="c2b6e-125">W tej sekcji możesz zmodyfikować aplikację symulowane urządzenie hello utworzony w [Rozpoczynanie pracy z Centrum IoT] tooreceive komunikaty chmury do urządzenia z Centrum IoT hello.</span><span class="sxs-lookup"><span data-stu-id="c2b6e-125">In this section, you modify hello simulated device app you created in [Get started with IoT Hub] tooreceive cloud-to-device messages from hello IoT hub.</span></span>

1. <span data-ttu-id="c2b6e-126">Za pomocą edytora tekstu, otwórz plik simulated-device\src\main\java\com\mycompany\app\App.java hello.</span><span class="sxs-lookup"><span data-stu-id="c2b6e-126">Using a text editor, open hello simulated-device\src\main\java\com\mycompany\app\App.java file.</span></span>

2. <span data-ttu-id="c2b6e-127">Dodaj następujące hello **MessageCallback** jak zagnieżdżone klasa wewnątrz hello **aplikacji** klasy.</span><span class="sxs-lookup"><span data-stu-id="c2b6e-127">Add hello following **MessageCallback** class as a nested class inside hello **App** class.</span></span> <span data-ttu-id="c2b6e-128">Witaj **wykonania** metoda jest wywoływana, gdy urządzenie hello otrzyma komunikat z Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="c2b6e-128">hello **execute** method is invoked when hello device receives a message from IoT Hub.</span></span> <span data-ttu-id="c2b6e-129">W tym przykładzie urządzenia hello zawsze powiadamia o Centrum IoT hello o zakończeniu wiadomość hello:</span><span class="sxs-lookup"><span data-stu-id="c2b6e-129">In this example, hello device always notifies hello IoT hub that it has completed hello message:</span></span>

    ```java
    private static class AppMessageCallback implements MessageCallback {
      public IotHubMessageResult execute(Message msg, Object context) {
        System.out.println("Received message from hub: "
          + new String(msg.getBytes(), Message.DEFAULT_IOTHUB_MESSAGE_CHARSET));
    
        return IotHubMessageResult.COMPLETE;
      }
    }
    ```
3. <span data-ttu-id="c2b6e-130">Modyfikowanie hello **głównego** toocreate — metoda **AppMessageCallback** hello wystąpienia i wywołanie **setMessageCallback** metoda przed jego otwarciem powitania klienta w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="c2b6e-130">Modify hello **main** method toocreate an **AppMessageCallback** instance and call hello **setMessageCallback** method before it opens hello client as follows:</span></span>

    ```java
    client = new DeviceClient(connString, protocol);
   
    MessageCallback callback = new AppMessageCallback();
    client.setMessageCallback(callback, null);
    client.open();
    ```

    > [!NOTE]
    > <span data-ttu-id="c2b6e-131">Witaj w przypadku wybrania protokołu HTTP zamiast MQTT lub AMQP jako transportu hello **DeviceClient** wystąpienia sprawdza, czy komunikaty z Centrum IoT rzadko (mniej niż co 25 minut).</span><span class="sxs-lookup"><span data-stu-id="c2b6e-131">If you use HTTP instead of MQTT or AMQP as hello transport, hello **DeviceClient** instance checks for messages from IoT Hub infrequently (less than every 25 minutes).</span></span> <span data-ttu-id="c2b6e-132">Aby uzyskać więcej informacji o różnicach hello MQTT, AMQP i HTTP pomocy technicznej i ograniczania Centrum IoT, zobacz hello [Centrum IoT — przewodnik dewelopera][IoT Hub developer guide - C2D].</span><span class="sxs-lookup"><span data-stu-id="c2b6e-132">For more information about hello differences between MQTT, AMQP and HTTP support, and IoT Hub throttling, see hello [IoT Hub developer guide][IoT Hub developer guide - C2D].</span></span>

4. <span data-ttu-id="c2b6e-133">Witaj toobuild **symulowane urządzenie** aplikacji za pomocą programu Maven, wykonaj następujące polecenie w wierszu polecenia hello w folderze symulowane urządzenie hello hello:</span><span class="sxs-lookup"><span data-stu-id="c2b6e-133">toobuild hello **simulated-device** app using Maven, execute hello following command at hello command prompt in hello simulated-device folder:</span></span>

    ```cmd/sh
    mvn clean package -DskipTests
    ```

## <a name="send-a-cloud-to-device-message"></a><span data-ttu-id="c2b6e-134">Wyślij wiadomość chmury do urządzenia</span><span class="sxs-lookup"><span data-stu-id="c2b6e-134">Send a cloud-to-device message</span></span>

<span data-ttu-id="c2b6e-135">W tej sekcji utworzysz aplikację konsoli języka Java, która wysyła komunikaty chmury do urządzenia toohello symulowane urządzenie aplikacji.</span><span class="sxs-lookup"><span data-stu-id="c2b6e-135">In this section, you create a Java console app that sends cloud-to-device messages toohello simulated device app.</span></span> <span data-ttu-id="c2b6e-136">Należy hello identyfikator urządzenia urządzenia hello dodane w hello [Rozpoczynanie pracy z Centrum IoT] samouczka.</span><span class="sxs-lookup"><span data-stu-id="c2b6e-136">You need hello device ID of hello device you added in hello [Get started with IoT Hub] tutorial.</span></span> <span data-ttu-id="c2b6e-137">Centrum, które można znaleźć w hello muszą zostać hello parametry połączenia Centrum IoT [portalu Azure].</span><span class="sxs-lookup"><span data-stu-id="c2b6e-137">You also need hello IoT Hub connection string for your hub that you can find in hello [Azure portal].</span></span>

1. <span data-ttu-id="c2b6e-138">Utwórz projekt Maven o nazwie **wysyłania — c2d — liczba komunikatów** przy użyciu hello następujące polecenie z wiersza polecenia.</span><span class="sxs-lookup"><span data-stu-id="c2b6e-138">Create a Maven project called **send-c2d-messages** using hello following command at your command prompt.</span></span> <span data-ttu-id="c2b6e-139">Należy zauważyć, że to polecenie jest pojedynczą, długie polecenie:</span><span class="sxs-lookup"><span data-stu-id="c2b6e-139">Note this command is a single, long command:</span></span>

    ```cmd/sh
    mvn archetype:generate -DgroupId=com.mycompany.app -DartifactId=send-c2d-messages -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false
    ```

2. <span data-ttu-id="c2b6e-140">Wierszu polecenia przejdź toohello nowy folder wysyłania — c2d — liczba komunikatów.</span><span class="sxs-lookup"><span data-stu-id="c2b6e-140">At your command prompt, navigate toohello new send-c2d-messages folder.</span></span>

3. <span data-ttu-id="c2b6e-141">Za pomocą edytora tekstu, otwórz plik pom.xml hello w folderze wysyłać c2d-wiadomości powitania i dodaj następujące zależności toohello hello **zależności** węzła.</span><span class="sxs-lookup"><span data-stu-id="c2b6e-141">Using a text editor, open hello pom.xml file in hello send-c2d-messages folder and add hello following dependency toohello **dependencies** node.</span></span> <span data-ttu-id="c2b6e-142">Dodawanie zależności hello umożliwia toouse hello **Centrum iothub-java--klient usługi** pakiet w Twojej toocommunicate aplikacji z usługą Centrum IoT:</span><span class="sxs-lookup"><span data-stu-id="c2b6e-142">Adding hello dependency enables you toouse hello **iothub-java-service-client** package in your application toocommunicate with your IoT hub service:</span></span>

    ```xml
    <dependency>
      <groupId>com.microsoft.azure.sdk.iot</groupId>
      <artifactId>iot-service-client</artifactId>
      <version>1.7.23</version>
    </dependency>
    ```

    > [!NOTE]
    > <span data-ttu-id="c2b6e-143">Możesz sprawdzić hello najnowszą wersję **klienta w przypadku usługi iot** przy użyciu [wyszukiwania Maven][lnk-maven-service-search].</span><span class="sxs-lookup"><span data-stu-id="c2b6e-143">You can check for hello latest version of **iot-service-client** using [Maven search][lnk-maven-service-search].</span></span>

4. <span data-ttu-id="c2b6e-144">Zapisz i zamknij plik pom.xml hello.</span><span class="sxs-lookup"><span data-stu-id="c2b6e-144">Save and close hello pom.xml file.</span></span>

5. <span data-ttu-id="c2b6e-145">Za pomocą edytora tekstu, otwórz plik send-c2d-messages\src\main\java\com\mycompany\app\App.java hello.</span><span class="sxs-lookup"><span data-stu-id="c2b6e-145">Using a text editor, open hello send-c2d-messages\src\main\java\com\mycompany\app\App.java file.</span></span>

6. <span data-ttu-id="c2b6e-146">Dodaj następujące hello **zaimportować** instrukcje toohello pliku:</span><span class="sxs-lookup"><span data-stu-id="c2b6e-146">Add hello following **import** statements toohello file:</span></span>

    ```java
    import com.microsoft.azure.sdk.iot.service.*;
    import java.io.IOException;
    import java.net.URISyntaxException;
    ```

7. <span data-ttu-id="c2b6e-147">Dodaj następujące zmienne klasy toohello hello **aplikacji** klasy, zastępując **{yourhubconnectionstring}** i **{yourdeviceid}** hello wartości z dostrzeżone wcześniej:</span><span class="sxs-lookup"><span data-stu-id="c2b6e-147">Add hello following class-level variables toohello **App** class, replacing **{yourhubconnectionstring}** and **{yourdeviceid}** with hello values your noted earlier:</span></span>

    ```java
    private static final String connectionString = "{yourhubconnectionstring}";
    private static final String deviceId = "{yourdeviceid}";
    private static final IotHubServiceClientProtocol protocol = IotHubServiceClientProtocol.AMQPS;
    ```

8. <span data-ttu-id="c2b6e-148">Zastąp hello **głównego** metody z hello następującego kodu.</span><span class="sxs-lookup"><span data-stu-id="c2b6e-148">Replace hello **main** method with hello following code.</span></span> <span data-ttu-id="c2b6e-149">Ten kod łączy z Centrum IoT tooyour, wysyła komunikat tooyour urządzenia i czeka na potwierdzenie tę wiadomość hello odebrane i przetwarzanie urządzenia hello:</span><span class="sxs-lookup"><span data-stu-id="c2b6e-149">This code connects tooyour IoT hub, sends a message tooyour device, and then waits for an acknowledgment that hello device received and processed hello message:</span></span>
   
    ```java
    public static void main(String[] args) throws IOException,
        URISyntaxException, Exception {
      ServiceClient serviceClient = ServiceClient.createFromConnectionString(
        connectionString, protocol);
   
      if (serviceClient != null) {
        serviceClient.open();
        FeedbackReceiver feedbackReceiver = serviceClient
          .getFeedbackReceiver();
        if (feedbackReceiver != null) feedbackReceiver.open();
   
        Message messageToSend = new Message("Cloud toodevice message.");
        messageToSend.setDeliveryAcknowledgement(DeliveryAcknowledgement.Full);
   
        serviceClient.send(deviceId, messageToSend);
        System.out.println("Message sent toodevice");
   
        FeedbackBatch feedbackBatch = feedbackReceiver.receive(10000);
        if (feedbackBatch != null) {
          System.out.println("Message feedback received, feedback time: "
            + feedbackBatch.getEnqueuedTimeUtc().toString());
        }
   
        if (feedbackReceiver != null) feedbackReceiver.close();
        serviceClient.close();
      }
    }
    ```

    > [!NOTE]
    > <span data-ttu-id="c2b6e-150">Sake na prostotę w tym samouczku nie implementuje wszystkie zasady ponawiania.</span><span class="sxs-lookup"><span data-stu-id="c2b6e-150">For simplicity's sake, this tutorial does not implement any retry policy.</span></span> <span data-ttu-id="c2b6e-151">W kodzie produkcyjnym, należy zaimplementować zasady ponawiania (na przykład wykładniczego wycofywania), zgodnie z sugestią podaną w artykuł w witrynie MSDN hello [obsługi błędów przejściowych].</span><span class="sxs-lookup"><span data-stu-id="c2b6e-151">In production code, you should implement retry policies (such as exponential backoff), as suggested in hello MSDN article [Transient Fault Handling].</span></span>


9. <span data-ttu-id="c2b6e-152">Witaj toobuild **symulowane urządzenie** aplikacji za pomocą programu Maven, wykonaj następujące polecenie w wierszu polecenia hello w folderze symulowane urządzenie hello hello:</span><span class="sxs-lookup"><span data-stu-id="c2b6e-152">toobuild hello **simulated-device** app using Maven, execute hello following command at hello command prompt in hello simulated-device folder:</span></span>

    ```cmd/sh
    mvn clean package -DskipTests
    ```

## <a name="run-hello-applications"></a><span data-ttu-id="c2b6e-153">Uruchamianie aplikacji hello</span><span class="sxs-lookup"><span data-stu-id="c2b6e-153">Run hello applications</span></span>

<span data-ttu-id="c2b6e-154">Wszystko jest teraz gotowy toorun hello aplikacji.</span><span class="sxs-lookup"><span data-stu-id="c2b6e-154">You are now ready toorun hello applications.</span></span>

1. <span data-ttu-id="c2b6e-155">W wierszu polecenia w folderze symulowane urządzenie hello Uruchom powitania po toobegin polecenie wysyłania danych telemetrycznych tooyour IoT hub i toolisten komunikatów chmury do urządzenia wysyłane z Centrum:</span><span class="sxs-lookup"><span data-stu-id="c2b6e-155">At a command prompt in hello simulated-device folder, run hello following command toobegin sending telemetry tooyour IoT hub and toolisten for cloud-to-device messages sent from your hub:</span></span>

    ```cmd/sh
    mvn exec:java -Dexec.mainClass="com.mycompany.app.App" 
    ```

    ![Uruchamianie aplikacji symulowane urządzenie hello][img-simulated-device]

2. <span data-ttu-id="c2b6e-157">W wierszu polecenia w folderze wysyłać c2d-wiadomości powitania uruchom następujące polecenie toosend hello komunikatu chmura urządzenie i oczekiwania na potwierdzenie opinii:</span><span class="sxs-lookup"><span data-stu-id="c2b6e-157">At a command prompt in hello send-c2d-messages folder, run hello following command toosend a cloud-to-device message and wait for a feedback acknowledgment:</span></span>

    ```cmd/sh
    mvn exec:java -Dexec.mainClass="com.mycompany.app.App"
    ```

    ![Uruchom wiadomość hello polecenia toosend powitania chmury do urządzenia][img-send-command]

## <a name="next-steps"></a><span data-ttu-id="c2b6e-159">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="c2b6e-159">Next steps</span></span>

<span data-ttu-id="c2b6e-160">W tym samouczku można przedstawiono sposób toosend i odbierania wiadomości chmury do urządzenia.</span><span class="sxs-lookup"><span data-stu-id="c2b6e-160">In this tutorial, you learned how toosend and receive cloud-to-device messages.</span></span> 

<span data-ttu-id="c2b6e-161">Przykłady toosee kompletnych rozwiązań end-to-end korzystających z Centrum IoT, zobacz [pakiet IoT Azure].</span><span class="sxs-lookup"><span data-stu-id="c2b6e-161">toosee examples of complete end-to-end solutions that use IoT Hub, see [Azure IoT Suite].</span></span>

<span data-ttu-id="c2b6e-162">toolearn więcej informacji na temat tworzenia rozwiązań z Centrum IoT, zobacz hello [Centrum IoT — przewodnik dewelopera].</span><span class="sxs-lookup"><span data-stu-id="c2b6e-162">toolearn more about developing solutions with IoT Hub, see hello [IoT Hub developer guide].</span></span>

<!-- Images -->
[img-simulated-device]: media/iot-hub-java-java-c2d/receivec2d.png
[img-send-command]:  media/iot-hub-java-java-c2d/sendc2d.png
<!-- Links -->

[Rozpoczynanie pracy z Centrum IoT]: iot-hub-java-java-getstarted.md
[IoT Hub developer guide - C2D]: iot-hub-devguide-messaging.md
[Centrum IoT — przewodnik dewelopera]: iot-hub-devguide.md
[Azure IoT Developer Center]: http://www.azure.com/develop/iot
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[lnk-dev-setup]: https://github.com/Azure/azure-iot-sdk-java
[obsługi błędów przejściowych]: https://msdn.microsoft.com/library/hh680901(v=pandp.50).aspx
[portalu Azure]: https://portal.azure.com
[pakiet IoT Azure]: https://azure.microsoft.com/documentation/suites/iot-suite/
[lnk-maven-service-search]: http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22iot-service-client%22%20g%3A%22com.microsoft.azure.sdk.iot%22