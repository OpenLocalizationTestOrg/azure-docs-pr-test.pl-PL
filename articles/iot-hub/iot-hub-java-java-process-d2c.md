---
title: "Przetwarzanie wiadomości urządzenia do chmury Azure IoT Hub (Java) | Dokumentacja firmy Microsoft"
description: "Jak komunikaty do przetwarzania komunikatów urządzenia do chmury Centrum IoT przy użyciu reguł routingu oraz niestandardowe punkty końcowe wysłania wiadomości do innych usług zaplecza."
services: iot-hub
documentationcenter: java
author: dominicbetts
manager: timlt
editor: 
ms.assetid: bd9af5f9-a740-4780-a2a6-8c0e2752cf48
ms.service: iot-hub
ms.devlang: java
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/29/2017
ms.author: dobett
ms.openlocfilehash: d1aca8f39e305105d4ec9f63fbe7bee95487e294
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="process-iot-hub-device-to-cloud-messages-java"></a><span data-ttu-id="e040d-103">Przetwarzanie wiadomości urządzenia do chmury Centrum IoT (Java)</span><span class="sxs-lookup"><span data-stu-id="e040d-103">Process IoT Hub device-to-cloud messages (Java)</span></span>

[!INCLUDE [iot-hub-selector-process-d2c](../../includes/iot-hub-selector-process-d2c.md)]

<span data-ttu-id="e040d-104">Centrum IoT Azure jest w pełni zarządzaną usługę, która zapewnia niezawodne i bezpieczną komunikację dwukierunkową między milionów urządzeń i rozwiązanie zaplecza.</span><span class="sxs-lookup"><span data-stu-id="e040d-104">Azure IoT Hub is a fully managed service that enables reliable and secure bi-directional communications between millions of devices and a solution back end.</span></span> <span data-ttu-id="e040d-105">Innych samouczków ([Rozpoczynanie pracy z Centrum IoT] i [wysyłać chmury do urządzenia z Centrum IoT][lnk-c2d]) opisano, jak korzystać z podstawowego urządzenia do chmury i chmury do urządzenia Obsługa wiadomości funkcji Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="e040d-105">Other tutorials ([Get started with IoT Hub] and [Send cloud-to-device messages with IoT Hub][lnk-c2d]) show you how to use the basic device-to-cloud and cloud-to-device messaging functionality of IoT Hub.</span></span>

<span data-ttu-id="e040d-106">W tym samouczku opiera się na kodzie pokazanym w [Rozpoczynanie pracy z Centrum IoT] samouczek oraz przedstawiono sposób do rozsyłania wiadomości przetwarzania komunikatów urządzenia do chmury w sposób skalowalny.</span><span class="sxs-lookup"><span data-stu-id="e040d-106">This tutorial builds on the code shown in the [Get started with IoT Hub] tutorial, and shows you how to use message routing to process device-to-cloud messages in a scalable way.</span></span> <span data-ttu-id="e040d-107">Samouczek przedstawia sposób przetwarzania komunikatów, które wymagają natychmiastowego działania z zaplecza rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="e040d-107">The tutorial illustrates how to process messages that require immediate action from the solution back end.</span></span> <span data-ttu-id="e040d-108">Na przykład urządzenie może wysłać komunikat alarmu, które wyzwala Wstawianie biletu do systemu CRM.</span><span class="sxs-lookup"><span data-stu-id="e040d-108">For example, a device might send an alarm message that triggers inserting a ticket into a CRM system.</span></span> <span data-ttu-id="e040d-109">Z kolei wiadomości punktu danych źródła danych po prostu do aparatu analizy.</span><span class="sxs-lookup"><span data-stu-id="e040d-109">By contrast, data-point messages simply feed into an analytics engine.</span></span> <span data-ttu-id="e040d-110">Na przykład dane telemetryczne temperatury z urządzenia, które mają być przechowywane w celu późniejszej analizy jest komunikat punktu danych.</span><span class="sxs-lookup"><span data-stu-id="e040d-110">For example, temperature telemetry from a device that is to be stored for later analysis is a data-point message.</span></span>

<span data-ttu-id="e040d-111">Na końcu tego samouczka możesz uruchomić trzech aplikacji Java w konsoli:</span><span class="sxs-lookup"><span data-stu-id="e040d-111">At the end of this tutorial, you run three Java console apps:</span></span>

* <span data-ttu-id="e040d-112">**Symulowane urządzenie**, zmodyfikowanej wersji aplikacji utworzonych w [Rozpoczynanie pracy z Centrum IoT] samouczek, wysyła komunikaty urządzenia do chmury punktu danych co sekundę i interaktywne urządzenia do chmury wiadomości co 10 sekund .</span><span class="sxs-lookup"><span data-stu-id="e040d-112">**simulated-device**, a modified version of the app created in the [Get started with IoT Hub] tutorial, sends data-point device-to-cloud messages every second, and interactive device-to-cloud messages every 10 seconds.</span></span> <span data-ttu-id="e040d-113">Ta aplikacja korzysta z protokołu AMQP do komunikowania się z Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="e040d-113">This app uses the AMQP protocol to communicate with IoT Hub.</span></span>
* <span data-ttu-id="e040d-114">**Odczyt — d2c — liczba komunikatów** Wyświetla telemetrii wysyłane przez aplikację na urządzeniu.</span><span class="sxs-lookup"><span data-stu-id="e040d-114">**read-d2c-messages** displays the telemetry sent by your device app.</span></span>
* <span data-ttu-id="e040d-115">**Odczyt krytyczne kolejki** usuwania kolejki krytycznych wiadomości z kolejki usługi Service Bus dołączony do Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="e040d-115">**read-critical-queue** de-queues the critical messages from the Service Bus queue attached to the IoT hub.</span></span>

> [!NOTE]
> <span data-ttu-id="e040d-116">Centrum IoT obsługuje zestawu SDK dla wielu platform urządzeń i języków, w tym C, Java i JavaScript.</span><span class="sxs-lookup"><span data-stu-id="e040d-116">IoT Hub has SDK support for many device platforms and languages, including C, Java, and JavaScript.</span></span> <span data-ttu-id="e040d-117">Aby uzyskać instrukcje dotyczące sposobu Zamień w tym samouczku urządzenie fizyczne urządzenia oraz sposób podłączania urządzeń do Centrum IoT, zobacz [Azure IoT Developer Center].</span><span class="sxs-lookup"><span data-stu-id="e040d-117">For instructions on how to replace the device in this tutorial with a physical device, and how to connect devices to an IoT Hub, see the [Azure IoT Developer Center].</span></span>

<span data-ttu-id="e040d-118">Do wykonania kroków tego samouczka niezbędne są następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="e040d-118">To complete this tutorial, you need the following:</span></span>

* <span data-ttu-id="e040d-119">Pełną wersję pracy [Rozpoczynanie pracy z Centrum IoT] samouczka.</span><span class="sxs-lookup"><span data-stu-id="e040d-119">A complete working version of the [Get started with IoT Hub] tutorial.</span></span>
* <span data-ttu-id="e040d-120">Najnowszy zestaw [Java SE Development Kit 8](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)</span><span class="sxs-lookup"><span data-stu-id="e040d-120">The latest [Java SE Development Kit 8](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)</span></span>
* [<span data-ttu-id="e040d-121">Maven 3</span><span class="sxs-lookup"><span data-stu-id="e040d-121">Maven 3</span></span>](https://maven.apache.org/install.html)
* <span data-ttu-id="e040d-122">Aktywne konto platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="e040d-122">An active Azure account.</span></span> <span data-ttu-id="e040d-123">(Jeśli nie masz konta, możesz utworzyć [bezpłatne konto] [lnk bezpłatnych wersji próbnych] w zaledwie kilka minut.)</span><span class="sxs-lookup"><span data-stu-id="e040d-123">(If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.)</span></span>

<span data-ttu-id="e040d-124">Powinien mieć niektóre podstawową wiedzę na temat [usługi Azure Storage] i [Azure Service Bus].</span><span class="sxs-lookup"><span data-stu-id="e040d-124">You should have some basic knowledge of [Azure Storage] and [Azure Service Bus].</span></span>

## <a name="send-interactive-messages-from-a-device-app"></a><span data-ttu-id="e040d-125">Wysyłanie wiadomości interaktywne z aplikacji przez urządzenia</span><span class="sxs-lookup"><span data-stu-id="e040d-125">Send interactive messages from a device app</span></span>
<span data-ttu-id="e040d-126">W tej sekcji możesz zmodyfikować aplikację urządzenia, utworzony w [Rozpoczynanie pracy z Centrum IoT] samouczek czasami wysłać wiadomości, które wymagają natychmiastowego przetwarzania.</span><span class="sxs-lookup"><span data-stu-id="e040d-126">In this section, you modify the device app you created in the [Get started with IoT Hub] tutorial to occasionally send messages that require immediate processing.</span></span>

1. <span data-ttu-id="e040d-127">Użyj edytora tekstów, aby otworzyć plik simulated-device\src\main\java\com\mycompany\app\App.java.</span><span class="sxs-lookup"><span data-stu-id="e040d-127">Use a text editor to open the simulated-device\src\main\java\com\mycompany\app\App.java file.</span></span> <span data-ttu-id="e040d-128">Ten plik zawiera kod **symulowane urządzenie** aplikacji utworzony w [Rozpoczynanie pracy z Centrum IoT] samouczka.</span><span class="sxs-lookup"><span data-stu-id="e040d-128">This file contains the code for the **simulated-device** app you created in the [Get started with IoT Hub] tutorial.</span></span>

2. <span data-ttu-id="e040d-129">Zastąp **MessageSender** klasy następującym kodem:</span><span class="sxs-lookup"><span data-stu-id="e040d-129">Replace the **MessageSender** class with the following code:</span></span>

    ```java
    private static class MessageSender implements Runnable {

        public void run()  {
            try {
                double minTemperature = 20;
                double minHumidity = 60;
                Random rand = new Random();

                while (true) {
                    String msgStr;
                    Message msg;
                    if (new Random().nextDouble() > 0.7) {
                        msgStr = "This is a critical message.";
                        msg = new Message(msgStr);
                        msg.setProperty("level", "critical");
                    } else {
                        double currentTemperature = minTemperature + rand.nextDouble() * 15;
                        double currentHumidity = minHumidity + rand.nextDouble() * 20; 
                        TelemetryDataPoint telemetryDataPoint = new TelemetryDataPoint();
                        telemetryDataPoint.deviceId = deviceId;
                        telemetryDataPoint.temperature = currentTemperature;
                        telemetryDataPoint.humidity = currentHumidity;

                        msgStr = telemetryDataPoint.serialize();
                        msg = new Message(msgStr);
                    }
                    
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
   
    <span data-ttu-id="e040d-130">Ta metoda losowo dodaje właściwość `"level": "critical"` dla komunikatów wysyłanych przez urządzenia, która symuluje komunikat, który wymaga natychmiastowego działania przez zaplecza aplikacji.</span><span class="sxs-lookup"><span data-stu-id="e040d-130">This method randomly adds the property `"level": "critical"` to messages sent by the device, which simulates a message that requires immediate action by the application back-end.</span></span> <span data-ttu-id="e040d-131">Aplikacji przekazuje informacje we właściwościach komunikatu zamiast, w treści wiadomości, więc tego Centrum IoT może kierować wiadomości do miejsca docelowego właściwy komunikat.</span><span class="sxs-lookup"><span data-stu-id="e040d-131">The application passes this information in the message properties, instead of in the message body, so that IoT Hub can route the message to the proper message destination.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="e040d-132">Można użyć właściwości wiadomości do przesyłania wiadomości dla różnych scenariuszy, w tym chłodni ścieżką podczas przetwarzania, oprócz tu przykładzie aktywnej ścieżki.</span><span class="sxs-lookup"><span data-stu-id="e040d-132">You can use message properties to route messages for various scenarios including cold-path processing, in addition to the hot path example shown here.</span></span>

2. <span data-ttu-id="e040d-133">Zapisz i zamknij plik simulated-device\src\main\java\com\mycompany\app\App.java.</span><span class="sxs-lookup"><span data-stu-id="e040d-133">Save and close the simulated-device\src\main\java\com\mycompany\app\App.java file.</span></span>

    > [!NOTE]
    > <span data-ttu-id="e040d-134">Dla uproszczenia w tym samouczku nie implementuje wszystkie zasady ponawiania.</span><span class="sxs-lookup"><span data-stu-id="e040d-134">For the sake of simplicity, this tutorial does not implement any retry policy.</span></span> <span data-ttu-id="e040d-135">W kodzie produkcyjnym, należy zaimplementować zasady ponawiania wykładniczego wycofywania, zgodnie z sugestią podaną w artykuł w witrynie MSDN np. [obsługi błędów przejściowych].</span><span class="sxs-lookup"><span data-stu-id="e040d-135">In production code, you should implement a retry policy such as exponential backoff, as suggested in the MSDN article [Transient Fault Handling].</span></span>

3. <span data-ttu-id="e040d-136">Aby utworzyć aplikację **simulated-device** przy użyciu narzędzia Maven, wykonaj następujące polecenie w wierszu polecenia w folderze simulated-device:</span><span class="sxs-lookup"><span data-stu-id="e040d-136">To build the **simulated-device** app using Maven, execute the following command at the command prompt in the simulated-device folder:</span></span>

    ```cmd/sh
    mvn clean package -DskipTests
    ```

## <a name="add-a-queue-to-your-iot-hub-and-route-messages-to-it"></a><span data-ttu-id="e040d-137">Dodaj kolejki do IoT hub i tras wiadomości do niego</span><span class="sxs-lookup"><span data-stu-id="e040d-137">Add a queue to your IoT hub and route messages to it</span></span>

<span data-ttu-id="e040d-138">W tej sekcji Tworzenie kolejki usługi Service Bus, połącz go z Centrum IoT i skonfigurować do wysyłania wiadomości do kolejki na podstawie obecności właściwość w komunikacie Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="e040d-138">In this section, you create a Service Bus queue, connect it to your IoT hub, and configure your IoT hub to send messages to the queue based on the presence of a property on the message.</span></span> <span data-ttu-id="e040d-139">Aby uzyskać więcej informacji o sposobie przetwarzania komunikatów z kolejek usługi Service Bus, zobacz [Rozpoczynanie pracy z kolejkami][lnk-sb-queues-java].</span><span class="sxs-lookup"><span data-stu-id="e040d-139">For more information about how to process messages from Service Bus queues, see [Get started with queues][lnk-sb-queues-java].</span></span>

1. <span data-ttu-id="e040d-140">Tworzenie kolejki usługi Service Bus, zgodnie z opisem w [Rozpoczynanie pracy z kolejkami][lnk-sb-queues-java].</span><span class="sxs-lookup"><span data-stu-id="e040d-140">Create a Service Bus queue as described in [Get started with queues][lnk-sb-queues-java].</span></span> <span data-ttu-id="e040d-141">Zanotuj nazwę przestrzeni nazw i kolejki.</span><span class="sxs-lookup"><span data-stu-id="e040d-141">Make a note of the namespace and queue name.</span></span>

2. <span data-ttu-id="e040d-142">W portalu Azure Otwórz Centrum IoT i kliknij przycisk **punkty końcowe**.</span><span class="sxs-lookup"><span data-stu-id="e040d-142">In the Azure portal, open your IoT hub and click **Endpoints**.</span></span>

    ![Punkty końcowe Centrum IoT][30]

3. <span data-ttu-id="e040d-144">W **punkty końcowe** bloku, kliknij przycisk **Dodaj** u góry, aby dodać kolejki do Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="e040d-144">In the **Endpoints** blade, click **Add** at the top to add your queue to your IoT hub.</span></span> <span data-ttu-id="e040d-145">Nazwa punktu końcowego **CriticalQueue** i umożliwia wybranie listach rozwijanych **kolejki usługi Service Bus**, przestrzeń nazw magistrali usług, w której znajduje się kolejki i nazwy kolejki.</span><span class="sxs-lookup"><span data-stu-id="e040d-145">Name the endpoint **CriticalQueue** and use the drop-downs to select **Service Bus queue**, the Service Bus namespace in which your queue resides, and the name of your queue.</span></span> <span data-ttu-id="e040d-146">Gdy wszystko będzie gotowe, kliknij przycisk **zapisać** u dołu.</span><span class="sxs-lookup"><span data-stu-id="e040d-146">When you are done, click **Save** at the bottom.</span></span>

    ![Dodawanie punktu końcowego][31]

4. <span data-ttu-id="e040d-148">Teraz kliknij **tras** w Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="e040d-148">Now click **Routes** in your IoT Hub.</span></span> <span data-ttu-id="e040d-149">Kliknij przycisk **Dodaj** w górnej części bloku, aby utworzyć regułę routingu kieruje komunikaty do kolejki właśnie został dodany.</span><span class="sxs-lookup"><span data-stu-id="e040d-149">Click **Add** at the top of the blade to create a routing rule that routes messages to the queue you just added.</span></span> <span data-ttu-id="e040d-150">Wybierz **DeviceTelemetry** jako źródło danych.</span><span class="sxs-lookup"><span data-stu-id="e040d-150">Select **DeviceTelemetry** as the source of data.</span></span> <span data-ttu-id="e040d-151">Wprowadź `level="critical"` jako warunek i wybierz polecenie kolejki właśnie został dodany jako punkt końcowy niestandardowych jako routingu końcowy reguły.</span><span class="sxs-lookup"><span data-stu-id="e040d-151">Enter `level="critical"` as the condition, and choose the queue you just added as a custom endpoint as the routing rule endpoint.</span></span> <span data-ttu-id="e040d-152">Gdy wszystko będzie gotowe, kliknij przycisk **zapisać** u dołu.</span><span class="sxs-lookup"><span data-stu-id="e040d-152">When you are done, click **Save** at the bottom.</span></span>

    ![Dodawanie trasy][32]

    <span data-ttu-id="e040d-154">Upewnij się, że rezerwowy trasy ma ustawioną wartość **ON**.</span><span class="sxs-lookup"><span data-stu-id="e040d-154">Make sure the fallback route is set to **ON**.</span></span> <span data-ttu-id="e040d-155">To ustawienie jest domyślną konfigurację Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="e040d-155">This setting is the default configuration of an IoT hub.</span></span>

    ![Trasy rezerwowej][33]

## <a name="optional-read-from-the-queue-endpoint"></a><span data-ttu-id="e040d-157">(Opcjonalnie) Odczyt z kolejki punktu końcowego</span><span class="sxs-lookup"><span data-stu-id="e040d-157">(Optional) Read from the queue endpoint</span></span>

<span data-ttu-id="e040d-158">Można opcjonalnie odczytywać wiadomości z kolejki punktu końcowego, postępując zgodnie z instrukcjami w [Rozpoczynanie pracy z kolejkami][lnk-sb-queues-java].</span><span class="sxs-lookup"><span data-stu-id="e040d-158">You can optionally read the messages from the queue endpoint by following the instructions in [Get started with queues][lnk-sb-queues-java].</span></span> <span data-ttu-id="e040d-159">Nazwa aplikacji **odczytu krytycznych kolejki**.</span><span class="sxs-lookup"><span data-stu-id="e040d-159">Name the app **read-critical-queue**.</span></span>

## <a name="run-the-applications"></a><span data-ttu-id="e040d-160">Uruchamianie aplikacji</span><span class="sxs-lookup"><span data-stu-id="e040d-160">Run the applications</span></span>

<span data-ttu-id="e040d-161">Teraz można przystąpić do uruchomienia trzech aplikacji.</span><span class="sxs-lookup"><span data-stu-id="e040d-161">Now you are ready to run the three applications.</span></span>

1. <span data-ttu-id="e040d-162">Aby uruchomić **odczytu — d2c — liczba komunikatów** aplikacji, w wierszu polecenia lub powłoki przejdź do folderu d2c odczytu i uruchom następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="e040d-162">To run the **read-d2c-messages** application, in a command prompt or shell navigate to the read-d2c folder and execute the following command:</span></span>

   ```cmd/sh
   mvn exec:java -Dexec.mainClass="com.mycompany.app.App"
   ```

   ![Uruchom odczytu — d2c — liczba komunikatów][readd2c]

2. <span data-ttu-id="e040d-164">Aby uruchomić **odczytu krytycznych kolejki** aplikacji, w wierszu polecenia lub powłoki przejdź do folderu odczytu krytycznych kolejki i uruchom następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="e040d-164">To run the **read-critical-queue** application, in a command prompt or shell navigate to the read-critical-queue folder and execute the following command:</span></span>

   ```cmd/sh
   mvn exec:java -Dexec.mainClass="com.mycompany.app.App"
   ```
   
   ![Uruchom odczytu — krytyczne — liczba komunikatów][readqueue]

3. <span data-ttu-id="e040d-166">Aby uruchomić **symulowane urządzenie** aplikacji, w wierszu polecenia lub powłoki przejdź do folderu symulowane urządzenie i uruchom następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="e040d-166">To run the **simulated-device** app, in a command prompt or shell navigate to the simulated-device folder and execute the following command:</span></span>

   ```cmd/sh
   mvn exec:java -Dexec.mainClass="com.mycompany.app.App"
   ```
   
   ![Uruchom symulowane urządzenie][simulateddevice]

## <a name="next-steps"></a><span data-ttu-id="e040d-168">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="e040d-168">Next steps</span></span>

<span data-ttu-id="e040d-169">W tym samouczku przedstawiono sposób niezawodny sposób wysyłania wiadomości urządzenia do chmury przy użyciu funkcji routing komunikatów z Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="e040d-169">In this tutorial, you learned how to reliably dispatch device-to-cloud messages by using the message routing functionality of IoT Hub.</span></span>

<span data-ttu-id="e040d-170">[Sposób wysyłania wiadomości chmury do urządzenia z Centrum IoT] [ lnk-c2d] przedstawiono sposób wysyłania komunikatów do urządzeń z Twojej zaplecza rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="e040d-170">The [How to send cloud-to-device messages with IoT Hub][lnk-c2d] shows you how to send messages to your devices from your solution back end.</span></span>

<span data-ttu-id="e040d-171">Aby zapoznać się przykładem kompletnych rozwiązań end-to-end korzystających z Centrum IoT, zobacz [pakiet IoT Azure][lnk-suite].</span><span class="sxs-lookup"><span data-stu-id="e040d-171">To see examples of complete end-to-end solutions that use IoT Hub, see [Azure IoT Suite][lnk-suite].</span></span>

<span data-ttu-id="e040d-172">Aby dowiedzieć się więcej na temat tworzenia rozwiązań z Centrum IoT, zobacz [Centrum IoT — przewodnik dewelopera].</span><span class="sxs-lookup"><span data-stu-id="e040d-172">To learn more about developing solutions with IoT Hub, see the [IoT Hub developer guide].</span></span>

<span data-ttu-id="e040d-173">Aby dowiedzieć się więcej na temat w Centrum IoT rozsyłania wiadomości, zobacz [wysyłania i odbierania wiadomości z Centrum IoT][lnk-devguide-messaging].</span><span class="sxs-lookup"><span data-stu-id="e040d-173">To learn more about message routing in IoT Hub, see [Send and receive messages with IoT Hub][lnk-devguide-messaging].</span></span>

<!-- Images. -->
<!-- TODO: UPDATE PICTURES -->
[simulateddevice]: ./media/iot-hub-java-java-process-d2c/runsimulateddevice.png
[readd2c]: ./media/iot-hub-java-java-process-d2c/runprocessinteractive.png
[readqueue]: ./media/iot-hub-java-java-process-d2c/runprocessd2c.png

[30]: ./media/iot-hub-java-java-process-d2c/click-endpoints.png
[31]: ./media/iot-hub-java-java-process-d2c/endpoint-creation.png
[32]: ./media/iot-hub-java-java-process-d2c/route-creation.png
[33]: ./media/iot-hub-java-java-process-d2c/fallback-route.png

<!-- Links -->

[lnk-sb-queues-java]: ../service-bus-messaging/service-bus-java-how-to-use-queues.md

<span data-ttu-id="e040d-174">[usługi Azure Storage]: https://azure.microsoft.com/documentation/services/storage/</span><span class="sxs-lookup"><span data-stu-id="e040d-174">[Azure Storage]: https://azure.microsoft.com/documentation/services/storage/</span></span>
<span data-ttu-id="e040d-175">[Azure Service Bus]: https://azure.microsoft.com/documentation/services/service-bus/</span><span class="sxs-lookup"><span data-stu-id="e040d-175">[Azure Service Bus]: https://azure.microsoft.com/documentation/services/service-bus/</span></span>

<span data-ttu-id="e040d-176">[Centrum IoT — przewodnik dewelopera]: iot-hub-devguide.md</span><span class="sxs-lookup"><span data-stu-id="e040d-176">[IoT Hub developer guide]: iot-hub-devguide.md</span></span>
[lnk-devguide-messaging]: iot-hub-devguide-messaging.md
<span data-ttu-id="e040d-177">[Rozpoczynanie pracy z Centrum IoT]: iot-hub-java-java-getstarted.md</span><span class="sxs-lookup"><span data-stu-id="e040d-177">[Get started with IoT Hub]: iot-hub-java-java-getstarted.md</span></span>
<span data-ttu-id="e040d-178">[Azure IoT Developer Center]: https://azure.microsoft.com/develop/iot</span><span class="sxs-lookup"><span data-stu-id="e040d-178">[Azure IoT Developer Center]: https://azure.microsoft.com/develop/iot</span></span>
<span data-ttu-id="e040d-179">[obsługi błędów przejściowych]: https://msdn.microsoft.com/library/hh675232.aspx</span><span class="sxs-lookup"><span data-stu-id="e040d-179">[Transient Fault Handling]: https://msdn.microsoft.com/library/hh675232.aspx</span></span>

<!-- Links -->
<span data-ttu-id="e040d-180">[Obsługa błędu przejściowego]: https://msdn.microsoft.com/library/hh680901(v=pandp.50).aspx</span><span class="sxs-lookup"><span data-stu-id="e040d-180">[Transient Fault Handling]: https://msdn.microsoft.com/library/hh680901(v=pandp.50).aspx</span></span>

[lnk-c2d]: iot-hub-java-java-c2d.md
[lnk-suite]: https://azure.microsoft.com/documentation/suites/iot-suite/
