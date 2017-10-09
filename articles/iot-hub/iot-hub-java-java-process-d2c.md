---
title: "aaaProcess wiadomości urządzenia do chmury Azure IoT Hub (Java) | Dokumentacja firmy Microsoft"
description: "Jak tooprocess Centrum IoT wiadomości urządzenia do chmury przy użyciu reguł routingu oraz niestandardowe punkty końcowe toodispatch komunikatów tooother usług zaplecza."
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
ms.openlocfilehash: 084e84e721ca4297c4d7d6cb06a43b0bed9bce85
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="process-iot-hub-device-to-cloud-messages-java"></a><span data-ttu-id="10b18-103">Przetwarzanie wiadomości urządzenia do chmury Centrum IoT (Java)</span><span class="sxs-lookup"><span data-stu-id="10b18-103">Process IoT Hub device-to-cloud messages (Java)</span></span>

[!INCLUDE [iot-hub-selector-process-d2c](../../includes/iot-hub-selector-process-d2c.md)]

<span data-ttu-id="10b18-104">Centrum IoT Azure jest w pełni zarządzaną usługę, która zapewnia niezawodne i bezpieczną komunikację dwukierunkową między milionów urządzeń i rozwiązanie zaplecza.</span><span class="sxs-lookup"><span data-stu-id="10b18-104">Azure IoT Hub is a fully managed service that enables reliable and secure bi-directional communications between millions of devices and a solution back end.</span></span> <span data-ttu-id="10b18-105">Innych samouczków ([Rozpoczynanie pracy z Centrum IoT] i [wysyłać chmury do urządzenia z Centrum IoT][lnk-c2d]) pokazują, jak toouse hello podstawowe urządzenia do chmury i chmury do urządzenia Obsługa wiadomości funkcji Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="10b18-105">Other tutorials ([Get started with IoT Hub] and [Send cloud-to-device messages with IoT Hub][lnk-c2d]) show you how toouse hello basic device-to-cloud and cloud-to-device messaging functionality of IoT Hub.</span></span>

<span data-ttu-id="10b18-106">W tym samouczku opiera się na powitania kodu pokazano hello [Rozpoczynanie pracy z Centrum IoT] samouczek i pokazuje, jak toouse wiadomości routingu wiadomości urządzenia do chmury tooprocess w sposób skalowalny.</span><span class="sxs-lookup"><span data-stu-id="10b18-106">This tutorial builds on hello code shown in hello [Get started with IoT Hub] tutorial, and shows you how toouse message routing tooprocess device-to-cloud messages in a scalable way.</span></span> <span data-ttu-id="10b18-107">Samouczek Hello przedstawiono, jak komunikaty tooprocess, które wymagają natychmiastowego działania z rozwiązania hello wewnętrzna baza danych.</span><span class="sxs-lookup"><span data-stu-id="10b18-107">hello tutorial illustrates how tooprocess messages that require immediate action from hello solution back end.</span></span> <span data-ttu-id="10b18-108">Na przykład urządzenie może wysłać komunikat alarmu, które wyzwala Wstawianie biletu do systemu CRM.</span><span class="sxs-lookup"><span data-stu-id="10b18-108">For example, a device might send an alarm message that triggers inserting a ticket into a CRM system.</span></span> <span data-ttu-id="10b18-109">Z kolei wiadomości punktu danych źródła danych po prostu do aparatu analizy.</span><span class="sxs-lookup"><span data-stu-id="10b18-109">By contrast, data-point messages simply feed into an analytics engine.</span></span> <span data-ttu-id="10b18-110">Na przykład dane telemetryczne temperatury z urządzenia, które jest przechowywane w celu późniejszej analizy toobe jest komunikat punktu danych.</span><span class="sxs-lookup"><span data-stu-id="10b18-110">For example, temperature telemetry from a device that is toobe stored for later analysis is a data-point message.</span></span>

<span data-ttu-id="10b18-111">Na końcu hello tego samouczka możesz uruchomić trzech aplikacji Java w konsoli:</span><span class="sxs-lookup"><span data-stu-id="10b18-111">At hello end of this tutorial, you run three Java console apps:</span></span>

* <span data-ttu-id="10b18-112">**Symulowane urządzenie**, zmodyfikowanej wersji aplikacji hello utworzone w hello [Rozpoczynanie pracy z Centrum IoT] samouczek, wysyła komunikaty urządzenia do chmury punktu danych co sekundę i interaktywne urządzenia do chmury wiadomości co 10 Liczba sekund.</span><span class="sxs-lookup"><span data-stu-id="10b18-112">**simulated-device**, a modified version of hello app created in hello [Get started with IoT Hub] tutorial, sends data-point device-to-cloud messages every second, and interactive device-to-cloud messages every 10 seconds.</span></span> <span data-ttu-id="10b18-113">Ta aplikacja używa toocommunicate protokołu AMQP hello z Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="10b18-113">This app uses hello AMQP protocol toocommunicate with IoT Hub.</span></span>
* <span data-ttu-id="10b18-114">**Odczyt — d2c — liczba komunikatów** wyświetla dane telemetryczne hello wysyłane przez aplikację na urządzeniu.</span><span class="sxs-lookup"><span data-stu-id="10b18-114">**read-d2c-messages** displays hello telemetry sent by your device app.</span></span>
* <span data-ttu-id="10b18-115">**Odczyt krytyczne kolejki** usuwania kolejki krytycznych wiadomości powitania od toohello dołączony kolejki usługi Service Bus hello Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="10b18-115">**read-critical-queue** de-queues hello critical messages from hello Service Bus queue attached toohello IoT hub.</span></span>

> [!NOTE]
> <span data-ttu-id="10b18-116">Centrum IoT obsługuje zestawu SDK dla wielu platform urządzeń i języków, w tym C, Java i JavaScript.</span><span class="sxs-lookup"><span data-stu-id="10b18-116">IoT Hub has SDK support for many device platforms and languages, including C, Java, and JavaScript.</span></span> <span data-ttu-id="10b18-117">Aby uzyskać instrukcje dotyczące sposobu tooreplace hello urządzenia w ramach tego samouczka z urządzenia fizycznego i tooconnect tooan urządzenia IoT Hub, zobacz temat hello [Azure IoT Developer Center].</span><span class="sxs-lookup"><span data-stu-id="10b18-117">For instructions on how tooreplace hello device in this tutorial with a physical device, and how tooconnect devices tooan IoT Hub, see hello [Azure IoT Developer Center].</span></span>

<span data-ttu-id="10b18-118">toocomplete tego samouczka należy hello następujące:</span><span class="sxs-lookup"><span data-stu-id="10b18-118">toocomplete this tutorial, you need hello following:</span></span>

* <span data-ttu-id="10b18-119">Pełną wersję pracy hello [Rozpoczynanie pracy z Centrum IoT] samouczka.</span><span class="sxs-lookup"><span data-stu-id="10b18-119">A complete working version of hello [Get started with IoT Hub] tutorial.</span></span>
* <span data-ttu-id="10b18-120">Witaj najnowszych [Java SE Development Kit 8](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)</span><span class="sxs-lookup"><span data-stu-id="10b18-120">hello latest [Java SE Development Kit 8](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)</span></span>
* [<span data-ttu-id="10b18-121">Maven 3</span><span class="sxs-lookup"><span data-stu-id="10b18-121">Maven 3</span></span>](https://maven.apache.org/install.html)
* <span data-ttu-id="10b18-122">Aktywne konto platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="10b18-122">An active Azure account.</span></span> <span data-ttu-id="10b18-123">(Jeśli nie masz konta, możesz utworzyć [bezpłatne konto] [lnk bezpłatnych wersji próbnych] w zaledwie kilka minut.)</span><span class="sxs-lookup"><span data-stu-id="10b18-123">(If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.)</span></span>

<span data-ttu-id="10b18-124">Powinien mieć niektóre podstawową wiedzę na temat [usługi Azure Storage] i [Azure Service Bus].</span><span class="sxs-lookup"><span data-stu-id="10b18-124">You should have some basic knowledge of [Azure Storage] and [Azure Service Bus].</span></span>

## <a name="send-interactive-messages-from-a-device-app"></a><span data-ttu-id="10b18-125">Wysyłanie wiadomości interaktywne z aplikacji przez urządzenia</span><span class="sxs-lookup"><span data-stu-id="10b18-125">Send interactive messages from a device app</span></span>
<span data-ttu-id="10b18-126">W tej sekcji możesz zmodyfikować aplikację urządzenia hello utworzony w hello [Rozpoczynanie pracy z Centrum IoT] toooccasionally samouczka Wyślij wiadomości, które wymagają natychmiastowego przetwarzania.</span><span class="sxs-lookup"><span data-stu-id="10b18-126">In this section, you modify hello device app you created in hello [Get started with IoT Hub] tutorial toooccasionally send messages that require immediate processing.</span></span>

1. <span data-ttu-id="10b18-127">Przy użyciu pliku simulated-device\src\main\java\com\mycompany\app\App.java hello tooopen edytora tekstu.</span><span class="sxs-lookup"><span data-stu-id="10b18-127">Use a text editor tooopen hello simulated-device\src\main\java\com\mycompany\app\App.java file.</span></span> <span data-ttu-id="10b18-128">Ten plik zawiera kod hello hello **symulowane urządzenie** aplikacji utworzony w hello [Rozpoczynanie pracy z Centrum IoT] samouczka.</span><span class="sxs-lookup"><span data-stu-id="10b18-128">This file contains hello code for hello **simulated-device** app you created in hello [Get started with IoT Hub] tutorial.</span></span>

2. <span data-ttu-id="10b18-129">Zastąp hello **MessageSender** klasy z hello następującego kodu:</span><span class="sxs-lookup"><span data-stu-id="10b18-129">Replace hello **MessageSender** class with hello following code:</span></span>

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
   
    <span data-ttu-id="10b18-130">Ta metoda losowo dodaje właściwość hello `"level": "critical"` toomessages wysyłane przez urządzenie hello, która symuluje komunikat, który wymaga natychmiastowego działania przez zaplecza aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="10b18-130">This method randomly adds hello property `"level": "critical"` toomessages sent by hello device, which simulates a message that requires immediate action by hello application back-end.</span></span> <span data-ttu-id="10b18-131">Aplikacja Hello przekazuje informacje w oknie dialogowym właściwości wiadomość hello zamiast, w treści wiadomości powitania, dzięki tym Centrum IoT można kierować docelowy prawidłowego komunikatu toohello wiadomość hello.</span><span class="sxs-lookup"><span data-stu-id="10b18-131">hello application passes this information in hello message properties, instead of in hello message body, so that IoT Hub can route hello message toohello proper message destination.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="10b18-132">Można użyć komunikatów właściwości tooroute komunikatów dla różnych scenariuszy, w tym przetwarzanie dodatkowo toohello aktywnej ścieżki przykładzie chłodni path.</span><span class="sxs-lookup"><span data-stu-id="10b18-132">You can use message properties tooroute messages for various scenarios including cold-path processing, in addition toohello hot path example shown here.</span></span>

2. <span data-ttu-id="10b18-133">Zapisz i zamknij plik simulated-device\src\main\java\com\mycompany\app\App.java hello.</span><span class="sxs-lookup"><span data-stu-id="10b18-133">Save and close hello simulated-device\src\main\java\com\mycompany\app\App.java file.</span></span>

    > [!NOTE]
    > <span data-ttu-id="10b18-134">Dla zapewnienia hello prostotę w tym samouczku nie implementuje wszystkie zasady ponawiania.</span><span class="sxs-lookup"><span data-stu-id="10b18-134">For hello sake of simplicity, this tutorial does not implement any retry policy.</span></span> <span data-ttu-id="10b18-135">W kodzie produkcyjnym, należy zaimplementować zasady ponawiania wykładniczego wycofywania, zgodnie z sugestią podaną w artykuł w witrynie MSDN hello np. [obsługi błędów przejściowych].</span><span class="sxs-lookup"><span data-stu-id="10b18-135">In production code, you should implement a retry policy such as exponential backoff, as suggested in hello MSDN article [Transient Fault Handling].</span></span>

3. <span data-ttu-id="10b18-136">Witaj toobuild **symulowane urządzenie** aplikacji za pomocą programu Maven, wykonaj następujące polecenie w wierszu polecenia hello w folderze symulowane urządzenie hello hello:</span><span class="sxs-lookup"><span data-stu-id="10b18-136">toobuild hello **simulated-device** app using Maven, execute hello following command at hello command prompt in hello simulated-device folder:</span></span>

    ```cmd/sh
    mvn clean package -DskipTests
    ```

## <a name="add-a-queue-tooyour-iot-hub-and-route-messages-tooit"></a><span data-ttu-id="10b18-137">Dodaj kolejki tooyour IoT hub i tras wiadomości tooit</span><span class="sxs-lookup"><span data-stu-id="10b18-137">Add a queue tooyour IoT hub and route messages tooit</span></span>

<span data-ttu-id="10b18-138">W tej sekcji Tworzenie kolejki usługi Service Bus, podłącz go tooyour Centrum IoT i skonfigurować IoT Centrum toosend wiadomości toohello kolejki na podstawie obecności hello właściwości na wiadomość powitania.</span><span class="sxs-lookup"><span data-stu-id="10b18-138">In this section, you create a Service Bus queue, connect it tooyour IoT hub, and configure your IoT hub toosend messages toohello queue based on hello presence of a property on hello message.</span></span> <span data-ttu-id="10b18-139">Aby uzyskać więcej informacji o sposobie tooprocess komunikaty z kolejek usługi Service Bus, zobacz [Rozpoczynanie pracy z kolejkami][lnk-sb-queues-java].</span><span class="sxs-lookup"><span data-stu-id="10b18-139">For more information about how tooprocess messages from Service Bus queues, see [Get started with queues][lnk-sb-queues-java].</span></span>

1. <span data-ttu-id="10b18-140">Tworzenie kolejki usługi Service Bus, zgodnie z opisem w [Rozpoczynanie pracy z kolejkami][lnk-sb-queues-java].</span><span class="sxs-lookup"><span data-stu-id="10b18-140">Create a Service Bus queue as described in [Get started with queues][lnk-sb-queues-java].</span></span> <span data-ttu-id="10b18-141">Zanotuj nazwę przestrzeni nazw i kolejki hello.</span><span class="sxs-lookup"><span data-stu-id="10b18-141">Make a note of hello namespace and queue name.</span></span>

2. <span data-ttu-id="10b18-142">Witaj w portalu Azure, Otwórz Centrum IoT i kliknij przycisk **punkty końcowe**.</span><span class="sxs-lookup"><span data-stu-id="10b18-142">In hello Azure portal, open your IoT hub and click **Endpoints**.</span></span>

    ![Punkty końcowe Centrum IoT][30]

3. <span data-ttu-id="10b18-144">W hello **punkty końcowe** bloku, kliknij przycisk **Dodaj** na hello top tooadd Centrum IoT tooyour kolejki.</span><span class="sxs-lookup"><span data-stu-id="10b18-144">In hello **Endpoints** blade, click **Add** at hello top tooadd your queue tooyour IoT hub.</span></span> <span data-ttu-id="10b18-145">Punkt końcowy hello nazwa **CriticalQueue** i użyj hello listach rozwijanych tooselect **kolejki usługi Service Bus**hello przestrzeń nazw magistrali usług, w której znajduje się kolejki i hello nazwę kolejki.</span><span class="sxs-lookup"><span data-stu-id="10b18-145">Name hello endpoint **CriticalQueue** and use hello drop-downs tooselect **Service Bus queue**, hello Service Bus namespace in which your queue resides, and hello name of your queue.</span></span> <span data-ttu-id="10b18-146">Gdy wszystko będzie gotowe, kliknij przycisk **zapisać** u dołu hello.</span><span class="sxs-lookup"><span data-stu-id="10b18-146">When you are done, click **Save** at hello bottom.</span></span>

    ![Dodawanie punktu końcowego][31]

4. <span data-ttu-id="10b18-148">Teraz kliknij **tras** w Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="10b18-148">Now click **Routes** in your IoT Hub.</span></span> <span data-ttu-id="10b18-149">Kliknij przycisk **Dodaj** u góry hello toocreate bloku hello reguły routingu kieruje komunikaty toohello kolejki można tylko dodać.</span><span class="sxs-lookup"><span data-stu-id="10b18-149">Click **Add** at hello top of hello blade toocreate a routing rule that routes messages toohello queue you just added.</span></span> <span data-ttu-id="10b18-150">Wybierz **DeviceTelemetry** hello źródłem danych.</span><span class="sxs-lookup"><span data-stu-id="10b18-150">Select **DeviceTelemetry** as hello source of data.</span></span> <span data-ttu-id="10b18-151">Wprowadź `level="critical"` hello warunkiem i wybierz polecenie kolejki hello właśnie został dodany jako punkt końcowy niestandardowych jako hello punkt końcowy reguły routingu.</span><span class="sxs-lookup"><span data-stu-id="10b18-151">Enter `level="critical"` as hello condition, and choose hello queue you just added as a custom endpoint as hello routing rule endpoint.</span></span> <span data-ttu-id="10b18-152">Gdy wszystko będzie gotowe, kliknij przycisk **zapisać** u dołu hello.</span><span class="sxs-lookup"><span data-stu-id="10b18-152">When you are done, click **Save** at hello bottom.</span></span>

    ![Dodawanie trasy][32]

    <span data-ttu-id="10b18-154">Upewnij się, że trasy rezerwowy hello ustawiono zbyt**ON**.</span><span class="sxs-lookup"><span data-stu-id="10b18-154">Make sure hello fallback route is set too**ON**.</span></span> <span data-ttu-id="10b18-155">To ustawienie jest hello domyślną konfigurację Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="10b18-155">This setting is hello default configuration of an IoT hub.</span></span>

    ![Trasy rezerwowej][33]

## <a name="optional-read-from-hello-queue-endpoint"></a><span data-ttu-id="10b18-157">(Opcjonalnie) Odczyt z hello punkt końcowy z kolejki</span><span class="sxs-lookup"><span data-stu-id="10b18-157">(Optional) Read from hello queue endpoint</span></span>

<span data-ttu-id="10b18-158">Możesz opcjonalnie przeczytać wiadomości powitania z punkt końcowy kolejki hello, wykonując następujące instrukcje hello w [Rozpoczynanie pracy z kolejkami][lnk-sb-queues-java].</span><span class="sxs-lookup"><span data-stu-id="10b18-158">You can optionally read hello messages from hello queue endpoint by following hello instructions in [Get started with queues][lnk-sb-queues-java].</span></span> <span data-ttu-id="10b18-159">Nazwa aplikacji hello **odczytu krytycznych kolejki**.</span><span class="sxs-lookup"><span data-stu-id="10b18-159">Name hello app **read-critical-queue**.</span></span>

## <a name="run-hello-applications"></a><span data-ttu-id="10b18-160">Uruchamianie aplikacji hello</span><span class="sxs-lookup"><span data-stu-id="10b18-160">Run hello applications</span></span>

<span data-ttu-id="10b18-161">Teraz wszystko jest gotowe toorun hello trzech aplikacji.</span><span class="sxs-lookup"><span data-stu-id="10b18-161">Now you are ready toorun hello three applications.</span></span>

1. <span data-ttu-id="10b18-162">Witaj toorun **odczytu — d2c — liczba komunikatów** aplikacji, w wierszu polecenia lub powłoki przejdź do folderu d2c odczytu toohello i wykonywanie hello następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="10b18-162">toorun hello **read-d2c-messages** application, in a command prompt or shell navigate toohello read-d2c folder and execute hello following command:</span></span>

   ```cmd/sh
   mvn exec:java -Dexec.mainClass="com.mycompany.app.App"
   ```

   ![Uruchom odczytu — d2c — liczba komunikatów][readd2c]

2. <span data-ttu-id="10b18-164">Witaj toorun **odczytu krytycznych kolejki** aplikacji, w wierszu polecenia lub powłoki przejdź do folderu odczytu krytycznych kolejki toohello i wykonywanie hello następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="10b18-164">toorun hello **read-critical-queue** application, in a command prompt or shell navigate toohello read-critical-queue folder and execute hello following command:</span></span>

   ```cmd/sh
   mvn exec:java -Dexec.mainClass="com.mycompany.app.App"
   ```
   
   ![Uruchom odczytu — krytyczne — liczba komunikatów][readqueue]

3. <span data-ttu-id="10b18-166">Witaj toorun **symulowane urządzenie** aplikacji, w wierszu polecenia lub powłoki Przejdź toohello folderu symulowane urządzenie i wykonaj hello następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="10b18-166">toorun hello **simulated-device** app, in a command prompt or shell navigate toohello simulated-device folder and execute hello following command:</span></span>

   ```cmd/sh
   mvn exec:java -Dexec.mainClass="com.mycompany.app.App"
   ```
   
   ![Uruchom symulowane urządzenie][simulateddevice]

## <a name="next-steps"></a><span data-ttu-id="10b18-168">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="10b18-168">Next steps</span></span>

<span data-ttu-id="10b18-169">W tym samouczku przedstawiono sposób tooreliably wysyłania wiadomości urządzenia do chmury przy użyciu funkcji routingu wiadomość hello Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="10b18-169">In this tutorial, you learned how tooreliably dispatch device-to-cloud messages by using hello message routing functionality of IoT Hub.</span></span>

<span data-ttu-id="10b18-170">Witaj [jak komunikaty toosend chmury do urządzenia z Centrum IoT] [ lnk-c2d] pokazuje, jak toosend wiadomości tooyour przez urządzenia z zaplecza rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="10b18-170">hello [How toosend cloud-to-device messages with IoT Hub][lnk-c2d] shows you how toosend messages tooyour devices from your solution back end.</span></span>

<span data-ttu-id="10b18-171">Przykłady toosee kompletnych rozwiązań end-to-end korzystających z Centrum IoT, zobacz [pakiet IoT Azure][lnk-suite].</span><span class="sxs-lookup"><span data-stu-id="10b18-171">toosee examples of complete end-to-end solutions that use IoT Hub, see [Azure IoT Suite][lnk-suite].</span></span>

<span data-ttu-id="10b18-172">toolearn więcej informacji na temat tworzenia rozwiązań z Centrum IoT, zobacz hello [Centrum IoT — przewodnik dewelopera].</span><span class="sxs-lookup"><span data-stu-id="10b18-172">toolearn more about developing solutions with IoT Hub, see hello [IoT Hub developer guide].</span></span>

<span data-ttu-id="10b18-173">Zobacz toolearn więcej informacji na temat routing komunikatów w Centrum IoT [wysyłania i odbierania wiadomości z Centrum IoT][lnk-devguide-messaging].</span><span class="sxs-lookup"><span data-stu-id="10b18-173">toolearn more about message routing in IoT Hub, see [Send and receive messages with IoT Hub][lnk-devguide-messaging].</span></span>

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

[usługi Azure Storage]: https://azure.microsoft.com/documentation/services/storage/
[Azure Service Bus]: https://azure.microsoft.com/documentation/services/service-bus/

[Centrum IoT — przewodnik dewelopera]: iot-hub-devguide.md
[lnk-devguide-messaging]: iot-hub-devguide-messaging.md
[Rozpoczynanie pracy z Centrum IoT]: iot-hub-java-java-getstarted.md
[Azure IoT Developer Center]: https://azure.microsoft.com/develop/iot
[obsługi błędów przejściowych]: https://msdn.microsoft.com/library/hh675232.aspx

<!-- Links -->
[Obsługa błędu przejściowego]: https://msdn.microsoft.com/library/hh680901(v=pandp.50).aspx

[lnk-c2d]: iot-hub-java-java-c2d.md
[lnk-suite]: https://azure.microsoft.com/documentation/suites/iot-suite/
