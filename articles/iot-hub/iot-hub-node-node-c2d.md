---
title: "Komunikaty chmury do urządzenia z Centrum IoT Azure (węzeł) | Dokumentacja firmy Microsoft"
description: "Jak wysłać wiadomości chmury do urządzenia na urządzeniu z Centrum Azure IoT przy użyciu zestawów SDK IoT Azure dla środowiska Node.js. Możesz zmodyfikować aplikację symulowane urządzenie, aby odbierać komunikaty z chmury do urządzenia i modyfikowania aplikacji zaplecza, do wysyłania wiadomości chmury do urządzenia."
services: iot-hub
documentationcenter: nodejs
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 3ca8a78f-ade2-46e8-8a49-d5d599cdf1f1
ms.service: iot-hub
ms.devlang: javascript
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/16/2017
ms.author: dobett
ms.openlocfilehash: 4580bda5633f84a7c7af0dc85f3cea4951024836
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="send-cloud-to-device-messages-with-iot-hub-node"></a><span data-ttu-id="82609-104">Wysyłanie komunikatów chmury do urządzenia z Centrum IoT (węzeł)</span><span class="sxs-lookup"><span data-stu-id="82609-104">Send cloud-to-device messages with IoT Hub (Node)</span></span>
[!INCLUDE [iot-hub-selector-c2d](../../includes/iot-hub-selector-c2d.md)]

## <a name="introduction"></a><span data-ttu-id="82609-105">Wprowadzenie</span><span class="sxs-lookup"><span data-stu-id="82609-105">Introduction</span></span>
<span data-ttu-id="82609-106">Centrum IoT Azure jest w pełni zarządzaną usługę, która umożliwia włączanie i niezawodności komunikację dwukierunkową między milionów urządzeń i zaplecze rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="82609-106">Azure IoT Hub is a fully managed service that helps enable reliable and secure bi-directional communications between millions of devices and a solution back end.</span></span> <span data-ttu-id="82609-107">[Rozpoczynanie pracy z Centrum IoT] samouczek przedstawia sposób tworzenia Centrum IoT, udostępnić tożsamość urządzenia w nim i kodem aplikacji symulowane urządzenie, który wysyła wiadomości urządzenia do chmury.</span><span class="sxs-lookup"><span data-stu-id="82609-107">The [Get started with IoT Hub] tutorial shows how to create an IoT hub, provision a device identity in it, and code a simulated device app that sends device-to-cloud messages.</span></span>

<span data-ttu-id="82609-108">W tym samouczku opiera się na [Rozpoczynanie pracy z Centrum IoT].</span><span class="sxs-lookup"><span data-stu-id="82609-108">This tutorial builds on [Get started with IoT Hub].</span></span> <span data-ttu-id="82609-109">Jak przedstawiono na:</span><span class="sxs-lookup"><span data-stu-id="82609-109">It shows you how to:</span></span>

* <span data-ttu-id="82609-110">Z sieci zaplecza rozwiązania wysyłać chmury do urządzenia do jednego urządzenia za pośrednictwem Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="82609-110">From your solution back end, send cloud-to-device messages to a single device through IoT Hub.</span></span>
* <span data-ttu-id="82609-111">Komunikaty chmury do urządzenia na urządzeniu.</span><span class="sxs-lookup"><span data-stu-id="82609-111">Receive cloud-to-device messages on a device.</span></span>
* <span data-ttu-id="82609-112">Z sieci zaplecza rozwiązania, żądania potwierdzenia dostarczenia (*opinii*) dla wiadomości wysyłanych do urządzenia z Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="82609-112">From your solution back end, request delivery acknowledgement (*feedback*) for messages sent to a device from IoT Hub.</span></span>

<span data-ttu-id="82609-113">Można znaleźć więcej informacji na temat wiadomości chmury do urządzenia w [Centrum IoT — przewodnik dewelopera][IoT Hub developer guide - C2D].</span><span class="sxs-lookup"><span data-stu-id="82609-113">You can find more information on cloud-to-device messages in the [IoT Hub developer guide][IoT Hub developer guide - C2D].</span></span>

<span data-ttu-id="82609-114">Na końcu tego samouczka możesz uruchomić dwóch aplikacji konsoli Node.js:</span><span class="sxs-lookup"><span data-stu-id="82609-114">At the end of this tutorial, you run two Node.js console apps:</span></span>

* <span data-ttu-id="82609-115">**SimulatedDevice**, zmodyfikowanej wersji aplikacji utworzonych w [Rozpoczynanie pracy z Centrum IoT], która łączy się z Centrum IoT i odbiera komunikaty chmury do urządzenia.</span><span class="sxs-lookup"><span data-stu-id="82609-115">**SimulatedDevice**, a modified version of the app created in [Get started with IoT Hub], which connects to your IoT hub and receives cloud-to-device messages.</span></span>
* <span data-ttu-id="82609-116">**SendCloudToDeviceMessage**, który wysyła komunikat chmury do urządzenia do aplikacji symulowane urządzenie za pomocą Centrum IoT i następnie odbiera jego potwierdzenie dostarczenia.</span><span class="sxs-lookup"><span data-stu-id="82609-116">**SendCloudToDeviceMessage**, which sends a cloud-to-device message to the simulated device app through IoT Hub, and then receives its delivery acknowledgement.</span></span>

> [!NOTE]
> <span data-ttu-id="82609-117">Centrum IoT obsługuje zestawu SDK dla wielu platform urządzeń i języków (w tym C, Java i Javascript) za pośrednictwem zestawy SDK urządzenia Azure IoT.</span><span class="sxs-lookup"><span data-stu-id="82609-117">IoT Hub has SDK support for many device platforms and languages (including C, Java, and Javascript) through Azure IoT device SDKs.</span></span> <span data-ttu-id="82609-118">Aby uzyskać instrukcje krok po kroku dotyczące sposobu Podłącz urządzenie do kodu w tym samouczku i zwykle z Centrum IoT Azure, zobacz [Azure IoT Developer Center].</span><span class="sxs-lookup"><span data-stu-id="82609-118">For step-by-step instructions on how to connect your device to this tutorial's code, and generally to Azure IoT Hub, see the [Azure IoT Developer Center].</span></span>
> 
> 

<span data-ttu-id="82609-119">Do wykonania kroków tego samouczka niezbędne są następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="82609-119">To complete this tutorial, you need the following:</span></span>

* <span data-ttu-id="82609-120">Środowisko Node.js w wersji 0.10.x lub nowszej.</span><span class="sxs-lookup"><span data-stu-id="82609-120">Node.js version 0.10.x or later.</span></span>
* <span data-ttu-id="82609-121">Aktywne konto platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="82609-121">An active Azure account.</span></span> <span data-ttu-id="82609-122">(Jeśli go nie masz, możesz utworzyć [bezpłatne konto próbne][lnk-free-trial] w zaledwie kilka minut).</span><span class="sxs-lookup"><span data-stu-id="82609-122">(If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.)</span></span>

## <a name="receive-messages-in-the-simulated-device-app"></a><span data-ttu-id="82609-123">Odbieranie komunikatów w aplikacji symulowane urządzenie</span><span class="sxs-lookup"><span data-stu-id="82609-123">Receive messages in the simulated device app</span></span>
<span data-ttu-id="82609-124">W tej sekcji możesz zmodyfikować aplikację symulowane urządzenie, utworzony w [Rozpoczynanie pracy z Centrum IoT] odbierać komunikaty z chmury do urządzenia z Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="82609-124">In this section, you modify the simulated device app you created in [Get started with IoT Hub] to receive cloud-to-device messages from the IoT hub.</span></span>

1. <span data-ttu-id="82609-125">Za pomocą edytora tekstu, otwórz plik SimulatedDevice.js.</span><span class="sxs-lookup"><span data-stu-id="82609-125">Using a text editor, open the SimulatedDevice.js file.</span></span>
2. <span data-ttu-id="82609-126">Modyfikowanie **connectCallback** funkcji obsługi wiadomości wysyłane z Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="82609-126">Modify the **connectCallback** function to handle messages sent from IoT Hub.</span></span> <span data-ttu-id="82609-127">W tym przykładzie zawsze wywołuje urządzenia **pełną** funkcji, aby powiadomić Centrum IoT, że został on przetworzony wiadomości.</span><span class="sxs-lookup"><span data-stu-id="82609-127">In this example, the device always invokes the **complete** function to notify IoT Hub that it has processed the message.</span></span> <span data-ttu-id="82609-128">Nową wersję pakietu **connectCallback** funkcja wygląda następujący fragment kodu:</span><span class="sxs-lookup"><span data-stu-id="82609-128">Your new version of the **connectCallback** function looks like the following snippet:</span></span>
   
    ```javascript
    var connectCallback = function (err) {
      if (err) {
        console.log('Could not connect: ' + err);
      } else {
        console.log('Client connected');
        client.on('message', function (msg) {
          console.log('Id: ' + msg.messageId + ' Body: ' + msg.data);
          client.complete(msg, printResultFor('completed'));
        });
        // Create a message and send it to the IoT Hub every second
        setInterval(function(){
            var temperature = 20 + (Math.random() * 15);
            var humidity = 60 + (Math.random() * 20);            
            var data = JSON.stringify({ deviceId: 'myFirstNodeDevice', temperature: temperature, humidity: humidity });
            var message = new Message(data);
            message.properties.add('temperatureAlert', (temperature > 30) ? 'true' : 'false');
            console.log("Sending message: " + message.getData());
            client.sendEvent(message, printResultFor('send'));
        }, 1000);
      }
    };
    ```
   
   > [!NOTE]
   > <span data-ttu-id="82609-129">Jeśli używasz protokołu HTTP zamiast MQTT lub AMQP do transportu **DeviceClient** wystąpienia sprawdza, czy komunikaty z Centrum IoT rzadko (mniej niż co 25 minut).</span><span class="sxs-lookup"><span data-stu-id="82609-129">If you use HTTP instead of MQTT or AMQP as the transport, the **DeviceClient** instance checks for messages from IoT Hub infrequently (less than every 25 minutes).</span></span> <span data-ttu-id="82609-130">Aby uzyskać więcej informacji na temat różnic między MQTT, AMQP i HTTP pomocy technicznej i ograniczania Centrum IoT, zobacz [Centrum IoT — przewodnik dewelopera][IoT Hub developer guide - C2D].</span><span class="sxs-lookup"><span data-stu-id="82609-130">For more information about the differences between MQTT, AMQP and HTTP support, and IoT Hub throttling, see the [IoT Hub developer guide][IoT Hub developer guide - C2D].</span></span>
   > 
   > 

## <a name="send-a-cloud-to-device-message"></a><span data-ttu-id="82609-131">Wyślij wiadomość chmury do urządzenia</span><span class="sxs-lookup"><span data-stu-id="82609-131">Send a cloud-to-device message</span></span>
<span data-ttu-id="82609-132">W tej sekcji utworzysz aplikację konsoli Node.js, która wysyła komunikaty chmury do urządzenia do aplikacji symulowane urządzenie.</span><span class="sxs-lookup"><span data-stu-id="82609-132">In this section, you create a Node.js console app that sends cloud-to-device messages to the simulated device app.</span></span> <span data-ttu-id="82609-133">Potrzebny jest identyfikator urządzenia urządzenia dodane w [Rozpoczynanie pracy z Centrum IoT] samouczka.</span><span class="sxs-lookup"><span data-stu-id="82609-133">You need the device ID of the device you added in the [Get started with IoT Hub] tutorial.</span></span> <span data-ttu-id="82609-134">Należy również parametry połączenia Centrum IoT, który znajduje się w Centrum [portalu Azure].</span><span class="sxs-lookup"><span data-stu-id="82609-134">You also need the IoT Hub connection string for your hub that you can find in the [Azure portal].</span></span>

1. <span data-ttu-id="82609-135">Utwórz pusty folder o nazwie **sendcloudtodevicemessage**.</span><span class="sxs-lookup"><span data-stu-id="82609-135">Create an empty folder called **sendcloudtodevicemessage**.</span></span> <span data-ttu-id="82609-136">W **sendcloudtodevicemessage** folderu, Utwórz plik package.json za pomocą następującego polecenia z wiersza polecenia.</span><span class="sxs-lookup"><span data-stu-id="82609-136">In the **sendcloudtodevicemessage** folder, create a package.json file using the following command at your command prompt.</span></span> <span data-ttu-id="82609-137">Zaakceptuj wszystkie ustawienia domyślne:</span><span class="sxs-lookup"><span data-stu-id="82609-137">Accept all the defaults:</span></span>
   
    ```shell
    npm init
    ```
2. <span data-ttu-id="82609-138">Z wiersza polecenia w **sendcloudtodevicemessage** folderu, uruchom następujące polecenie, aby zainstalować **Centrum iothub azure** pakietu:</span><span class="sxs-lookup"><span data-stu-id="82609-138">At your command prompt in the **sendcloudtodevicemessage** folder, run the following command to install the **azure-iothub** package:</span></span>
   
    ```shell
    npm install azure-iothub --save
    ```
3. <span data-ttu-id="82609-139">Za pomocą edytora tekstu, Utwórz **SendCloudToDeviceMessage.js** w pliku **sendcloudtodevicemessage** folderu.</span><span class="sxs-lookup"><span data-stu-id="82609-139">Using a text editor, create a **SendCloudToDeviceMessage.js** file in the **sendcloudtodevicemessage** folder.</span></span>
4. <span data-ttu-id="82609-140">Dodaj następujące `require` instrukcje na początku **SendCloudToDeviceMessage.js** pliku:</span><span class="sxs-lookup"><span data-stu-id="82609-140">Add the following `require` statements at the start of the **SendCloudToDeviceMessage.js** file:</span></span>
   
    ```javascript
    'use strict';
   
    var Client = require('azure-iothub').Client;
    var Message = require('azure-iot-common').Message;
    ```
5. <span data-ttu-id="82609-141">Dodaj następujący kod do **SendCloudToDeviceMessage.js** pliku.</span><span class="sxs-lookup"><span data-stu-id="82609-141">Add the following code to **SendCloudToDeviceMessage.js** file.</span></span> <span data-ttu-id="82609-142">Zastąp wartość symbolu zastępczego "{iot hub parametry połączenia}" z Centrum IoT parametry połączenia dla koncentratora utworzony w [Rozpoczynanie pracy z Centrum IoT] samouczka.</span><span class="sxs-lookup"><span data-stu-id="82609-142">Replace the "{iot hub connection string}" placeholder value with the IoT Hub connection string for the hub you created in the [Get started with IoT Hub] tutorial.</span></span> <span data-ttu-id="82609-143">Zastąp symbol zastępczy "{identyfikator urządzenia}" o identyfikatorze urządzenia urządzenie dodane w [Rozpoczynanie pracy z Centrum IoT] samouczek:</span><span class="sxs-lookup"><span data-stu-id="82609-143">Replace the "{device id}" placeholder with the device ID of the device you added in the [Get started with IoT Hub] tutorial:</span></span>
   
    ```javascript
    var connectionString = '{iot hub connection string}';
    var targetDevice = '{device id}';
   
    var serviceClient = Client.fromConnectionString(connectionString);
    ```
6. <span data-ttu-id="82609-144">Dodaj następującą funkcję Drukowanie wyników operacji do konsoli:</span><span class="sxs-lookup"><span data-stu-id="82609-144">Add the following function to print operation results to the console:</span></span>
   
    ```javascript
    function printResultFor(op) {
      return function printResult(err, res) {
        if (err) console.log(op + ' error: ' + err.toString());
        if (res) console.log(op + ' status: ' + res.constructor.name);
      };
    }
    ```
7. <span data-ttu-id="82609-145">Dodaj następującą funkcję drukowania dostarczania komunikatów opinię do konsoli:</span><span class="sxs-lookup"><span data-stu-id="82609-145">Add the following function to print delivery feedback messages to the console:</span></span>
   
    ```javascript
    function receiveFeedback(err, receiver){
      receiver.on('message', function (msg) {
        console.log('Feedback message:')
        console.log(msg.getData().toString('utf-8'));
      });
    }
    ```
8. <span data-ttu-id="82609-146">Dodaj następujący kod, aby wysłać komunikat do Twojego urządzenia i obsłużyć komunikat opinii, gdy urządzenie potwierdza komunikatu chmura urządzenie:</span><span class="sxs-lookup"><span data-stu-id="82609-146">Add the following code to send a message to your device and handle the feedback message when the device acknowledges the cloud-to-device message:</span></span>
   
    ```javascript
    serviceClient.open(function (err) {
      if (err) {
        console.error('Could not connect: ' + err.message);
      } else {
        console.log('Service client connected');
        serviceClient.getFeedbackReceiver(receiveFeedback);
        var message = new Message('Cloud to device message.');
        message.ack = 'full';
        message.messageId = "My Message ID";
        console.log('Sending message: ' + message.getData());
        serviceClient.send(targetDevice, message, printResultFor('send'));
      }
    });
    ```
9. <span data-ttu-id="82609-147">Zapisz i Zamknij **SendCloudToDeviceMessage.js** pliku.</span><span class="sxs-lookup"><span data-stu-id="82609-147">Save and close **SendCloudToDeviceMessage.js** file.</span></span>

## <a name="run-the-applications"></a><span data-ttu-id="82609-148">Uruchamianie aplikacji</span><span class="sxs-lookup"><span data-stu-id="82609-148">Run the applications</span></span>
<span data-ttu-id="82609-149">Teraz można uruchomić aplikacje.</span><span class="sxs-lookup"><span data-stu-id="82609-149">You are now ready to run the applications.</span></span>

1. <span data-ttu-id="82609-150">W wierszu polecenia w **simulateddevice** folderu, uruchom następujące polecenie, aby wysłać dane telemetryczne z Centrum IoT i nasłuchiwać komunikatów chmury do urządzenia:</span><span class="sxs-lookup"><span data-stu-id="82609-150">At the command prompt in the **simulateddevice** folder, run the following command to send telemetry to IoT Hub and to listen for cloud-to-device messages:</span></span>
   
    ```shell
    node SimulatedDevice.js 
    ```
   
    ![Uruchamianie aplikacji symulowane urządzenie][img-simulated-device]
2. <span data-ttu-id="82609-152">W wierszu polecenia **sendcloudtodevicemessage** folderu, uruchom następujące polecenie, aby wysłać wiadomość chmury do urządzenia i poczekaj, aż opinii potwierdzenia:</span><span class="sxs-lookup"><span data-stu-id="82609-152">At a command prompt in the **sendcloudtodevicemessage** folder, run the following command to send a cloud-to-device message and wait for the acknowledgment feedback:</span></span>
   
    ```shell
    node SendCloudToDeviceMessage.js 
    ```
   
    ![Uruchamianie aplikacji, aby wysłać polecenie chmury do urządzenia][img-send-command]
   
   > [!NOTE]
   > <span data-ttu-id="82609-154">Sake na prostotę w tym samouczku nie implementuje wszystkie zasady ponawiania.</span><span class="sxs-lookup"><span data-stu-id="82609-154">For simplicity's sake, this tutorial does not implement any retry policy.</span></span> <span data-ttu-id="82609-155">W kodzie produkcyjnym, należy zaimplementować zasady ponawiania (na przykład wykładniczego wycofywania), zgodnie z sugestią podaną w artykuł w witrynie MSDN [obsługi błędów przejściowych].</span><span class="sxs-lookup"><span data-stu-id="82609-155">In production code, you should implement retry policies (such as exponential backoff), as suggested in the MSDN article [Transient Fault Handling].</span></span>
   > 
   > 

## <a name="next-steps"></a><span data-ttu-id="82609-156">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="82609-156">Next steps</span></span>
<span data-ttu-id="82609-157">W tym samouczku przedstawiono sposób wysyłania i odbierania wiadomości chmury do urządzenia.</span><span class="sxs-lookup"><span data-stu-id="82609-157">In this tutorial, you learned how to send and receive cloud-to-device messages.</span></span> 

<span data-ttu-id="82609-158">Aby zapoznać się przykładem kompletnych rozwiązań end-to-end korzystających z Centrum IoT, zobacz [pakiet IoT Azure].</span><span class="sxs-lookup"><span data-stu-id="82609-158">To see examples of complete end-to-end solutions that use IoT Hub, see [Azure IoT Suite].</span></span>

<span data-ttu-id="82609-159">Aby dowiedzieć się więcej na temat tworzenia rozwiązań z Centrum IoT, zobacz [Centrum IoT — przewodnik dewelopera].</span><span class="sxs-lookup"><span data-stu-id="82609-159">To learn more about developing solutions with IoT Hub, see the [IoT Hub developer guide].</span></span>

<!-- Images -->
[img-simulated-device]: media/iot-hub-node-node-c2d/receivec2d.png
[img-send-command]:  media/iot-hub-node-node-c2d/sendc2d.png

<!-- Links -->

<span data-ttu-id="82609-160">[Rozpoczynanie pracy z Centrum IoT]: iot-hub-node-node-getstarted.md</span><span class="sxs-lookup"><span data-stu-id="82609-160">[Get started with IoT Hub]: iot-hub-node-node-getstarted.md</span></span>
[IoT Hub developer guide - C2D]: iot-hub-devguide-messaging.md
<span data-ttu-id="82609-161">[Centrum IoT — przewodnik dewelopera]: iot-hub-devguide.md</span><span class="sxs-lookup"><span data-stu-id="82609-161">[IoT Hub developer guide]: iot-hub-devguide.md</span></span>
<span data-ttu-id="82609-162">[Azure IoT Developer Center]: http://www.azure.com/develop/iot</span><span class="sxs-lookup"><span data-stu-id="82609-162">[Azure IoT Developer Center]: http://www.azure.com/develop/iot</span></span>
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[lnk-dev-setup]: https://github.com/Azure/azure-iot-sdk-node/tree/master/doc/node-devbox-setup.md
<span data-ttu-id="82609-163">[obsługi błędów przejściowych]: https://msdn.microsoft.com/library/hh680901(v=pandp.50).aspx</span><span class="sxs-lookup"><span data-stu-id="82609-163">[Transient Fault Handling]: https://msdn.microsoft.com/library/hh680901(v=pandp.50).aspx</span></span>
<span data-ttu-id="82609-164">[portalu Azure]: https://portal.azure.com</span><span class="sxs-lookup"><span data-stu-id="82609-164">[Azure portal]: https://portal.azure.com</span></span>
<span data-ttu-id="82609-165">[pakiet IoT Azure]: https://azure.microsoft.com/documentation/suites/iot-suite/</span><span class="sxs-lookup"><span data-stu-id="82609-165">[Azure IoT Suite]: https://azure.microsoft.com/documentation/suites/iot-suite/</span></span>
