---
title: "Komunikaty chmury do urządzenia z Centrum IoT Azure (Java) | Dokumentacja firmy Microsoft"
description: "Jak wysyłać wiadomości chmury do urządzenia na urządzeniu z Centrum Azure IoT przy użyciu zestawów SDK IoT Azure dla języka Java. Możesz zmodyfikować aplikację symulowane urządzenie, aby odbierać komunikaty z chmury do urządzenia i modyfikowania aplikacji zaplecza, do wysyłania wiadomości chmury do urządzenia."
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
ms.openlocfilehash: f5e3ac46f4d144b12e2ab7fcfb456665ff6cc68f
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/18/2017
---
# <a name="send-cloud-to-device-messages-with-iot-hub-java"></a><span data-ttu-id="b8cab-104">Wysyłanie komunikatów chmury do urządzenia z Centrum IoT (Java)</span><span class="sxs-lookup"><span data-stu-id="b8cab-104">Send cloud-to-device messages with IoT Hub (Java)</span></span>
[!INCLUDE [iot-hub-selector-c2d](../../includes/iot-hub-selector-c2d.md)]

<span data-ttu-id="b8cab-105">Centrum IoT Azure jest w pełni zarządzaną usługę, która umożliwia włączanie i niezawodności komunikację dwukierunkową między milionów urządzeń i zaplecze rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="b8cab-105">Azure IoT Hub is a fully managed service that helps enable reliable and secure bi-directional communications between millions of devices and a solution back end.</span></span> <span data-ttu-id="b8cab-106">[Rozpoczynanie pracy z Centrum IoT] samouczek przedstawia sposób tworzenia Centrum IoT, udostępnić tożsamość urządzenia w nim i kodem aplikacji symulowane urządzenie, który wysyła wiadomości urządzenia do chmury.</span><span class="sxs-lookup"><span data-stu-id="b8cab-106">The [Get started with IoT Hub] tutorial shows how to create an IoT hub, provision a device identity in it, and code a simulated device app that sends device-to-cloud messages.</span></span>

<span data-ttu-id="b8cab-107">W tym samouczku opiera się na [Rozpoczynanie pracy z Centrum IoT].</span><span class="sxs-lookup"><span data-stu-id="b8cab-107">This tutorial builds on [Get started with IoT Hub].</span></span> <span data-ttu-id="b8cab-108">Jak przedstawiono na:</span><span class="sxs-lookup"><span data-stu-id="b8cab-108">It shows you how to:</span></span>

* <span data-ttu-id="b8cab-109">Z sieci zaplecza rozwiązania wysyłać chmury do urządzenia do jednego urządzenia za pośrednictwem Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="b8cab-109">From your solution back end, send cloud-to-device messages to a single device through IoT Hub.</span></span>
* <span data-ttu-id="b8cab-110">Komunikaty chmury do urządzenia na urządzeniu.</span><span class="sxs-lookup"><span data-stu-id="b8cab-110">Receive cloud-to-device messages on a device.</span></span>
* <span data-ttu-id="b8cab-111">Z sieci zaplecza rozwiązania, żądania potwierdzenia dostarczenia (*opinii*) dla wiadomości wysyłanych do urządzenia z Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="b8cab-111">From your solution back end, request delivery acknowledgement (*feedback*) for messages sent to a device from IoT Hub.</span></span>

<span data-ttu-id="b8cab-112">Można znaleźć więcej informacji na temat wiadomości chmury do urządzenia w [Centrum IoT — przewodnik dewelopera][IoT Hub developer guide - C2D].</span><span class="sxs-lookup"><span data-stu-id="b8cab-112">You can find more information on cloud-to-device messages in the [IoT Hub developer guide][IoT Hub developer guide - C2D].</span></span>

<span data-ttu-id="b8cab-113">Na końcu tego samouczka możesz uruchomić dwie aplikacje konsoli Java:</span><span class="sxs-lookup"><span data-stu-id="b8cab-113">At the end of this tutorial, you run two Java console apps:</span></span>

* <span data-ttu-id="b8cab-114">**Symulowane urządzenie**, zmodyfikowanej wersji aplikacji utworzonych w [Rozpoczynanie pracy z Centrum IoT], która łączy się z Centrum IoT i odbiera komunikaty chmury do urządzenia.</span><span class="sxs-lookup"><span data-stu-id="b8cab-114">**simulated-device**, a modified version of the app created in [Get started with IoT Hub], which connects to your IoT hub and receives cloud-to-device messages.</span></span>
* <span data-ttu-id="b8cab-115">**send — c2d — liczba komunikatów**, który wysyła komunikat chmury do urządzenia do aplikacji symulowane urządzenie za pomocą Centrum IoT i następnie odbiera jego potwierdzenie dostarczenia.</span><span class="sxs-lookup"><span data-stu-id="b8cab-115">**send-c2d-messages**, which sends a cloud-to-device message to the simulated device app through IoT Hub, and then receives its delivery acknowledgement.</span></span>

> [!NOTE]
> <span data-ttu-id="b8cab-116">Centrum IoT obsługuje zestawu SDK dla wielu platform urządzeń i języków (w tym C, Java i Javascript) za pośrednictwem zestawy SDK urządzenia Azure IoT.</span><span class="sxs-lookup"><span data-stu-id="b8cab-116">IoT Hub has SDK support for many device platforms and languages (including C, Java, and Javascript) through Azure IoT device SDKs.</span></span> <span data-ttu-id="b8cab-117">Aby uzyskać instrukcje krok po kroku dotyczące sposobu Podłącz urządzenie do kodu w tym samouczku i zwykle z Centrum IoT Azure, zobacz [Azure IoT Developer Center].</span><span class="sxs-lookup"><span data-stu-id="b8cab-117">For step-by-step instructions on how to connect your device to this tutorial's code, and generally to Azure IoT Hub, see the [Azure IoT Developer Center].</span></span>

<span data-ttu-id="b8cab-118">Do wykonania kroków tego samouczka niezbędne są następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="b8cab-118">To complete this tutorial, you need the following:</span></span>

* <span data-ttu-id="b8cab-119">Pełną wersję pracy [Rozpoczynanie pracy z Centrum IoT](iot-hub-java-java-getstarted.md) lub [wiadomości urządzenia do chmury Centrum IoT procesu](iot-hub-java-java-process-d2c.md) samouczka.</span><span class="sxs-lookup"><span data-stu-id="b8cab-119">A complete working version of the [Get started with IoT Hub](iot-hub-java-java-getstarted.md) or [Process IoT Hub device-to-cloud messages](iot-hub-java-java-process-d2c.md) tutorial.</span></span>
* <span data-ttu-id="b8cab-120">Najnowszy zestaw [Java SE Development Kit 8](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)</span><span class="sxs-lookup"><span data-stu-id="b8cab-120">The latest [Java SE Development Kit 8](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)</span></span>
* [<span data-ttu-id="b8cab-121">Maven 3</span><span class="sxs-lookup"><span data-stu-id="b8cab-121">Maven 3</span></span>](https://maven.apache.org/install.html)
* <span data-ttu-id="b8cab-122">Aktywne konto platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="b8cab-122">An active Azure account.</span></span> <span data-ttu-id="b8cab-123">(Jeśli go nie masz, możesz utworzyć [bezpłatne konto próbne][lnk-free-trial] w zaledwie kilka minut).</span><span class="sxs-lookup"><span data-stu-id="b8cab-123">(If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.)</span></span>

## <a name="receive-messages-in-the-simulated-device-app"></a><span data-ttu-id="b8cab-124">Odbieranie komunikatów w aplikacji symulowane urządzenie</span><span class="sxs-lookup"><span data-stu-id="b8cab-124">Receive messages in the simulated device app</span></span>

<span data-ttu-id="b8cab-125">W tej sekcji możesz zmodyfikować aplikację symulowane urządzenie, utworzony w [Rozpoczynanie pracy z Centrum IoT] odbierać komunikaty z chmury do urządzenia z Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="b8cab-125">In this section, you modify the simulated device app you created in [Get started with IoT Hub] to receive cloud-to-device messages from the IoT hub.</span></span>

1. <span data-ttu-id="b8cab-126">Za pomocą edytora tekstów otwórz plik simulated-device\src\main\java\com\mycompany\app\App.java.</span><span class="sxs-lookup"><span data-stu-id="b8cab-126">Using a text editor, open the simulated-device\src\main\java\com\mycompany\app\App.java file.</span></span>

2. <span data-ttu-id="b8cab-127">Dodaj następujące **MessageCallback** jak zagnieżdżone klasa wewnątrz **aplikacji** klasy.</span><span class="sxs-lookup"><span data-stu-id="b8cab-127">Add the following **MessageCallback** class as a nested class inside the **App** class.</span></span> <span data-ttu-id="b8cab-128">**Wykonania** metoda jest wywoływana, gdy urządzenie otrzyma wiadomość z Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="b8cab-128">The **execute** method is invoked when the device receives a message from IoT Hub.</span></span> <span data-ttu-id="b8cab-129">W tym przykładzie urządzenie zawsze powiadamia o Centrum IoT o zakończeniu komunikat:</span><span class="sxs-lookup"><span data-stu-id="b8cab-129">In this example, the device always notifies the IoT hub that it has completed the message:</span></span>

    ```java
    private static class AppMessageCallback implements MessageCallback {
      public IotHubMessageResult execute(Message msg, Object context) {
        System.out.println("Received message from hub: "
          + new String(msg.getBytes(), Message.DEFAULT_IOTHUB_MESSAGE_CHARSET));
    
        return IotHubMessageResult.COMPLETE;
      }
    }
    ```
3. <span data-ttu-id="b8cab-130">Modyfikowanie **głównego** metodę w celu utworzenia **AppMessageCallback** wystąpienia i wywołanie **setMessageCallback** metoda przed jego otwarciem klienta w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="b8cab-130">Modify the **main** method to create an **AppMessageCallback** instance and call the **setMessageCallback** method before it opens the client as follows:</span></span>

    ```java
    client = new DeviceClient(connString, protocol);
   
    MessageCallback callback = new AppMessageCallback();
    client.setMessageCallback(callback, null);
    client.open();
    ```

    > [!NOTE]
    > <span data-ttu-id="b8cab-131">Jeśli używasz protokołu HTTP zamiast MQTT lub AMQP do transportu **DeviceClient** wystąpienia sprawdza, czy komunikaty z Centrum IoT rzadko (mniej niż co 25 minut).</span><span class="sxs-lookup"><span data-stu-id="b8cab-131">If you use HTTP instead of MQTT or AMQP as the transport, the **DeviceClient** instance checks for messages from IoT Hub infrequently (less than every 25 minutes).</span></span> <span data-ttu-id="b8cab-132">Aby uzyskać więcej informacji na temat różnic między MQTT, AMQP i HTTP pomocy technicznej i ograniczania Centrum IoT, zobacz [Centrum IoT — przewodnik dewelopera][IoT Hub developer guide - C2D].</span><span class="sxs-lookup"><span data-stu-id="b8cab-132">For more information about the differences between MQTT, AMQP and HTTP support, and IoT Hub throttling, see the [IoT Hub developer guide][IoT Hub developer guide - C2D].</span></span>

4. <span data-ttu-id="b8cab-133">Aby utworzyć aplikację **simulated-device** przy użyciu narzędzia Maven, wykonaj następujące polecenie w wierszu polecenia w folderze simulated-device:</span><span class="sxs-lookup"><span data-stu-id="b8cab-133">To build the **simulated-device** app using Maven, execute the following command at the command prompt in the simulated-device folder:</span></span>

    ```cmd/sh
    mvn clean package -DskipTests
    ```

## <a name="send-a-cloud-to-device-message"></a><span data-ttu-id="b8cab-134">Wyślij wiadomość chmury do urządzenia</span><span class="sxs-lookup"><span data-stu-id="b8cab-134">Send a cloud-to-device message</span></span>

<span data-ttu-id="b8cab-135">W tej sekcji utworzysz aplikację konsoli języka Java, która wysyła komunikaty chmury do urządzenia do aplikacji symulowane urządzenie.</span><span class="sxs-lookup"><span data-stu-id="b8cab-135">In this section, you create a Java console app that sends cloud-to-device messages to the simulated device app.</span></span> <span data-ttu-id="b8cab-136">Potrzebny jest identyfikator urządzenia urządzenia dodane w [Rozpoczynanie pracy z Centrum IoT] samouczka.</span><span class="sxs-lookup"><span data-stu-id="b8cab-136">You need the device ID of the device you added in the [Get started with IoT Hub] tutorial.</span></span> <span data-ttu-id="b8cab-137">Należy również parametry połączenia Centrum IoT, który znajduje się w Centrum [portalu Azure].</span><span class="sxs-lookup"><span data-stu-id="b8cab-137">You also need the IoT Hub connection string for your hub that you can find in the [Azure portal].</span></span>

1. <span data-ttu-id="b8cab-138">Utwórz projekt Maven o nazwie **wysyłania — c2d — liczba komunikatów** za pomocą następującego polecenia z wiersza polecenia.</span><span class="sxs-lookup"><span data-stu-id="b8cab-138">Create a Maven project called **send-c2d-messages** using the following command at your command prompt.</span></span> <span data-ttu-id="b8cab-139">Należy zauważyć, że to polecenie jest pojedynczą, długie polecenie:</span><span class="sxs-lookup"><span data-stu-id="b8cab-139">Note this command is a single, long command:</span></span>

    ```cmd/sh
    mvn archetype:generate -DgroupId=com.mycompany.app -DartifactId=send-c2d-messages -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false
    ```

2. <span data-ttu-id="b8cab-140">Wierszu polecenia przejdź do nowego folderu wysyłania — c2d — liczba komunikatów.</span><span class="sxs-lookup"><span data-stu-id="b8cab-140">At your command prompt, navigate to the new send-c2d-messages folder.</span></span>

3. <span data-ttu-id="b8cab-141">Za pomocą edytora tekstu, otwórz plik pom.xml w folderze wysyłania — c2d — liczba komunikatów i dodaj następujące zależności do **zależności** węzła.</span><span class="sxs-lookup"><span data-stu-id="b8cab-141">Using a text editor, open the pom.xml file in the send-c2d-messages folder and add the following dependency to the **dependencies** node.</span></span> <span data-ttu-id="b8cab-142">Dodawanie zależności pozwala na użycie **Centrum iothub-java--klient usługi** pakietu aplikacji do komunikowania się z usługą Centrum IoT:</span><span class="sxs-lookup"><span data-stu-id="b8cab-142">Adding the dependency enables you to use the **iothub-java-service-client** package in your application to communicate with your IoT hub service:</span></span>

    ```xml
    <dependency>
      <groupId>com.microsoft.azure.sdk.iot</groupId>
      <artifactId>iot-service-client</artifactId>
      <version>1.7.23</version>
    </dependency>
    ```

    > [!NOTE]
    > <span data-ttu-id="b8cab-143">Możesz sprawdzić dostępność najnowszej wersji pakietu **iot-service-client** za pomocą [funkcji wyszukiwania narzędzia Maven][lnk-maven-service-search].</span><span class="sxs-lookup"><span data-stu-id="b8cab-143">You can check for the latest version of **iot-service-client** using [Maven search][lnk-maven-service-search].</span></span>

4. <span data-ttu-id="b8cab-144">Zapisz i zamknij plik pom.xml.</span><span class="sxs-lookup"><span data-stu-id="b8cab-144">Save and close the pom.xml file.</span></span>

5. <span data-ttu-id="b8cab-145">Za pomocą edytora tekstu, otwórz plik send-c2d-messages\src\main\java\com\mycompany\app\App.java.</span><span class="sxs-lookup"><span data-stu-id="b8cab-145">Using a text editor, open the send-c2d-messages\src\main\java\com\mycompany\app\App.java file.</span></span>

6. <span data-ttu-id="b8cab-146">Dodaj do pliku następujące instrukcje **importowania**:</span><span class="sxs-lookup"><span data-stu-id="b8cab-146">Add the following **import** statements to the file:</span></span>

    ```java
    import com.microsoft.azure.sdk.iot.service.*;
    import java.io.IOException;
    import java.net.URISyntaxException;
    ```

7. <span data-ttu-id="b8cab-147">Dodaj następujące zmienne poziomie klasy do **aplikacji** klasy, zastępując **{yourhubconnectionstring}** i **{yourdeviceid}** z wartościami z dostrzeżone wcześniej:</span><span class="sxs-lookup"><span data-stu-id="b8cab-147">Add the following class-level variables to the **App** class, replacing **{yourhubconnectionstring}** and **{yourdeviceid}** with the values your noted earlier:</span></span>

    ```java
    private static final String connectionString = "{yourhubconnectionstring}";
    private static final String deviceId = "{yourdeviceid}";
    private static final IotHubServiceClientProtocol protocol = IotHubServiceClientProtocol.AMQPS;
    ```

8. <span data-ttu-id="b8cab-148">Zastąp **głównego** metodę z następującym kodem.</span><span class="sxs-lookup"><span data-stu-id="b8cab-148">Replace the **main** method with the following code.</span></span> <span data-ttu-id="b8cab-149">Ten kod łączy się z Centrum IoT, wysyła komunikat do Twojego urządzenia i czeka na potwierdzenie, że urządzenie odbierany i przetwarzany komunikat:</span><span class="sxs-lookup"><span data-stu-id="b8cab-149">This code connects to your IoT hub, sends a message to your device, and then waits for an acknowledgment that the device received and processed the message:</span></span>
   
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
   
        Message messageToSend = new Message("Cloud to device message.");
        messageToSend.setDeliveryAcknowledgement(DeliveryAcknowledgement.Full);
   
        serviceClient.send(deviceId, messageToSend);
        System.out.println("Message sent to device");
   
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
    > <span data-ttu-id="b8cab-150">Sake na prostotę w tym samouczku nie implementuje wszystkie zasady ponawiania.</span><span class="sxs-lookup"><span data-stu-id="b8cab-150">For simplicity's sake, this tutorial does not implement any retry policy.</span></span> <span data-ttu-id="b8cab-151">W kodzie produkcyjnym, należy zaimplementować zasady ponawiania (na przykład wykładniczego wycofywania), zgodnie z sugestią podaną w artykuł w witrynie MSDN [obsługi błędów przejściowych].</span><span class="sxs-lookup"><span data-stu-id="b8cab-151">In production code, you should implement retry policies (such as exponential backoff), as suggested in the MSDN article [Transient Fault Handling].</span></span>


9. <span data-ttu-id="b8cab-152">Aby utworzyć aplikację **simulated-device** przy użyciu narzędzia Maven, wykonaj następujące polecenie w wierszu polecenia w folderze simulated-device:</span><span class="sxs-lookup"><span data-stu-id="b8cab-152">To build the **simulated-device** app using Maven, execute the following command at the command prompt in the simulated-device folder:</span></span>

    ```cmd/sh
    mvn clean package -DskipTests
    ```

## <a name="run-the-applications"></a><span data-ttu-id="b8cab-153">Uruchamianie aplikacji</span><span class="sxs-lookup"><span data-stu-id="b8cab-153">Run the applications</span></span>

<span data-ttu-id="b8cab-154">Teraz można uruchomić aplikacje.</span><span class="sxs-lookup"><span data-stu-id="b8cab-154">You are now ready to run the applications.</span></span>

1. <span data-ttu-id="b8cab-155">W wierszu polecenia w folderze symulowane urządzenie uruchom następujące polecenie, aby rozpocząć wysyłanie danych telemetrycznych do Centrum IoT i nasłuchiwać komunikatów chmury do urządzenia wysyłane z Centrum:</span><span class="sxs-lookup"><span data-stu-id="b8cab-155">At a command prompt in the simulated-device folder, run the following command to begin sending telemetry to your IoT hub and to listen for cloud-to-device messages sent from your hub:</span></span>

    ```cmd/sh
    mvn exec:java -Dexec.mainClass="com.mycompany.app.App" 
    ```

    ![Uruchamianie aplikacji symulowane urządzenie][img-simulated-device]

2. <span data-ttu-id="b8cab-157">W wierszu polecenia w folderze wysyłania — c2d — liczba komunikatów uruchom następujące polecenie, aby wysłać wiadomość chmury do urządzenia i czeka na potwierdzenie opinii:</span><span class="sxs-lookup"><span data-stu-id="b8cab-157">At a command prompt in the send-c2d-messages folder, run the following command to send a cloud-to-device message and wait for a feedback acknowledgment:</span></span>

    ```cmd/sh
    mvn exec:java -Dexec.mainClass="com.mycompany.app.App"
    ```

    ![Uruchom polecenie, aby wysłać wiadomość chmury do urządzenia][img-send-command]

## <a name="next-steps"></a><span data-ttu-id="b8cab-159">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="b8cab-159">Next steps</span></span>

<span data-ttu-id="b8cab-160">W tym samouczku przedstawiono sposób wysyłania i odbierania wiadomości chmury do urządzenia.</span><span class="sxs-lookup"><span data-stu-id="b8cab-160">In this tutorial, you learned how to send and receive cloud-to-device messages.</span></span> 

<span data-ttu-id="b8cab-161">Aby zapoznać się przykładem kompletnych rozwiązań end-to-end korzystających z Centrum IoT, zobacz [pakiet IoT Azure].</span><span class="sxs-lookup"><span data-stu-id="b8cab-161">To see examples of complete end-to-end solutions that use IoT Hub, see [Azure IoT Suite].</span></span>

<span data-ttu-id="b8cab-162">Aby dowiedzieć się więcej na temat tworzenia rozwiązań z Centrum IoT, zobacz [Centrum IoT — przewodnik dewelopera].</span><span class="sxs-lookup"><span data-stu-id="b8cab-162">To learn more about developing solutions with IoT Hub, see the [IoT Hub developer guide].</span></span>

<!-- Images -->
[img-simulated-device]: media/iot-hub-java-java-c2d/receivec2d.png
[img-send-command]:  media/iot-hub-java-java-c2d/sendc2d.png
<!-- Links -->

<span data-ttu-id="b8cab-163">[Rozpoczynanie pracy z Centrum IoT]: iot-hub-java-java-getstarted.md</span><span class="sxs-lookup"><span data-stu-id="b8cab-163">[Get started with IoT Hub]: iot-hub-java-java-getstarted.md</span></span>
[IoT Hub developer guide - C2D]: iot-hub-devguide-messaging.md
<span data-ttu-id="b8cab-164">[Centrum IoT — przewodnik dewelopera]: iot-hub-devguide.md</span><span class="sxs-lookup"><span data-stu-id="b8cab-164">[IoT Hub developer guide]: iot-hub-devguide.md</span></span>
<span data-ttu-id="b8cab-165">[Azure IoT Developer Center]: http://www.azure.com/develop/iot</span><span class="sxs-lookup"><span data-stu-id="b8cab-165">[Azure IoT Developer Center]: http://www.azure.com/develop/iot</span></span>
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[lnk-dev-setup]: https://github.com/Azure/azure-iot-sdk-java
<span data-ttu-id="b8cab-166">[obsługi błędów przejściowych]: https://msdn.microsoft.com/library/hh680901(v=pandp.50).aspx</span><span class="sxs-lookup"><span data-stu-id="b8cab-166">[Transient Fault Handling]: https://msdn.microsoft.com/library/hh680901(v=pandp.50).aspx</span></span>
<span data-ttu-id="b8cab-167">[portalu Azure]: https://portal.azure.com</span><span class="sxs-lookup"><span data-stu-id="b8cab-167">[Azure portal]: https://portal.azure.com</span></span>
<span data-ttu-id="b8cab-168">[pakiet IoT Azure]: https://azure.microsoft.com/documentation/suites/iot-suite/</span><span class="sxs-lookup"><span data-stu-id="b8cab-168">[Azure IoT Suite]: https://azure.microsoft.com/documentation/suites/iot-suite/</span></span>
[lnk-maven-service-search]: http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22iot-service-client%22%20g%3A%22com.microsoft.azure.sdk.iot%22