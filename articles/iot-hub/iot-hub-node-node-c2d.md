---
title: "komunikaty aaaCloud do urządzenia z Centrum IoT Azure (węzeł) | Dokumentacja firmy Microsoft"
description: "Jak chmury urządzenia toosend komunikatów tooa urządzenia z Centrum Azure IoT przy użyciu hello Azure IoT SDK dla środowiska Node.js. Modyfikowanie komunikatów chmury do urządzenia symulowane urządzenie aplikacji tooreceive i modyfikowanie aplikacji zaplecza toosend hello chmury do urządzenia komunikatów."
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
ms.openlocfilehash: 1ccae0cada52193c2abb91504c086cac226e93da
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="send-cloud-to-device-messages-with-iot-hub-node"></a><span data-ttu-id="f7792-104">Wysyłanie komunikatów chmury do urządzenia z Centrum IoT (węzeł)</span><span class="sxs-lookup"><span data-stu-id="f7792-104">Send cloud-to-device messages with IoT Hub (Node)</span></span>
[!INCLUDE [iot-hub-selector-c2d](../../includes/iot-hub-selector-c2d.md)]

## <a name="introduction"></a><span data-ttu-id="f7792-105">Wprowadzenie</span><span class="sxs-lookup"><span data-stu-id="f7792-105">Introduction</span></span>
<span data-ttu-id="f7792-106">Centrum IoT Azure jest w pełni zarządzaną usługę, która umożliwia włączanie i niezawodności komunikację dwukierunkową między milionów urządzeń i zaplecze rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="f7792-106">Azure IoT Hub is a fully managed service that helps enable reliable and secure bi-directional communications between millions of devices and a solution back end.</span></span> <span data-ttu-id="f7792-107">Witaj [Rozpoczynanie pracy z Centrum IoT] samouczek pokazuje, jak udostępnić tożsamość urządzenia w nim toocreate Centrum IoT i kodu aplikacji symulowane urządzenie, który wysyła wiadomości urządzenia do chmury.</span><span class="sxs-lookup"><span data-stu-id="f7792-107">hello [Get started with IoT Hub] tutorial shows how toocreate an IoT hub, provision a device identity in it, and code a simulated device app that sends device-to-cloud messages.</span></span>

<span data-ttu-id="f7792-108">W tym samouczku opiera się na [Rozpoczynanie pracy z Centrum IoT].</span><span class="sxs-lookup"><span data-stu-id="f7792-108">This tutorial builds on [Get started with IoT Hub].</span></span> <span data-ttu-id="f7792-109">Jak przedstawiono na:</span><span class="sxs-lookup"><span data-stu-id="f7792-109">It shows you how to:</span></span>

* <span data-ttu-id="f7792-110">Z z zaplecza rozwiązania należy wysłać pojedyncze urządzenie tooa wiadomości chmury do urządzenia za pośrednictwem Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="f7792-110">From your solution back end, send cloud-to-device messages tooa single device through IoT Hub.</span></span>
* <span data-ttu-id="f7792-111">Komunikaty chmury do urządzenia na urządzeniu.</span><span class="sxs-lookup"><span data-stu-id="f7792-111">Receive cloud-to-device messages on a device.</span></span>
* <span data-ttu-id="f7792-112">Z sieci zaplecza rozwiązania, żądania potwierdzenia dostarczenia (*opinii*) dla wiadomości wysyłane tooa urządzenie z Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="f7792-112">From your solution back end, request delivery acknowledgement (*feedback*) for messages sent tooa device from IoT Hub.</span></span>

<span data-ttu-id="f7792-113">Więcej informacji na temat wiadomości chmury do urządzenia można znaleźć w hello [Centrum IoT — przewodnik dewelopera][IoT Hub developer guide - C2D].</span><span class="sxs-lookup"><span data-stu-id="f7792-113">You can find more information on cloud-to-device messages in hello [IoT Hub developer guide][IoT Hub developer guide - C2D].</span></span>

<span data-ttu-id="f7792-114">Na końcu hello tego samouczka możesz uruchomić dwóch aplikacji konsoli Node.js:</span><span class="sxs-lookup"><span data-stu-id="f7792-114">At hello end of this tutorial, you run two Node.js console apps:</span></span>

* <span data-ttu-id="f7792-115">**SimulatedDevice**, zmodyfikowanej wersji aplikacji hello utworzone w [Rozpoczynanie pracy z Centrum IoT], która łączy się z Centrum IoT tooyour i odbiera komunikaty chmury do urządzenia.</span><span class="sxs-lookup"><span data-stu-id="f7792-115">**SimulatedDevice**, a modified version of hello app created in [Get started with IoT Hub], which connects tooyour IoT hub and receives cloud-to-device messages.</span></span>
* <span data-ttu-id="f7792-116">**SendCloudToDeviceMessage**, który wysyła aplikacji symulowane urządzenie toohello komunikat chmury do urządzenia, za pośrednictwem Centrum IoT i następnie odbiera jego potwierdzenia dostarczenia.</span><span class="sxs-lookup"><span data-stu-id="f7792-116">**SendCloudToDeviceMessage**, which sends a cloud-to-device message toohello simulated device app through IoT Hub, and then receives its delivery acknowledgement.</span></span>

> [!NOTE]
> <span data-ttu-id="f7792-117">Centrum IoT obsługuje zestawu SDK dla wielu platform urządzeń i języków (w tym C, Java i Javascript) za pośrednictwem zestawy SDK urządzenia Azure IoT.</span><span class="sxs-lookup"><span data-stu-id="f7792-117">IoT Hub has SDK support for many device platforms and languages (including C, Java, and Javascript) through Azure IoT device SDKs.</span></span> <span data-ttu-id="f7792-118">Instrukcje krok po kroku dotyczące tooconnect samouczek toothis urządzenia kodu i zazwyczaj tooAzure Centrum IoT, zobacz temat hello [Azure IoT Developer Center].</span><span class="sxs-lookup"><span data-stu-id="f7792-118">For step-by-step instructions on how tooconnect your device toothis tutorial's code, and generally tooAzure IoT Hub, see hello [Azure IoT Developer Center].</span></span>
> 
> 

<span data-ttu-id="f7792-119">toocomplete tego samouczka należy hello następujące:</span><span class="sxs-lookup"><span data-stu-id="f7792-119">toocomplete this tutorial, you need hello following:</span></span>

* <span data-ttu-id="f7792-120">Środowisko Node.js w wersji 0.10.x lub nowszej.</span><span class="sxs-lookup"><span data-stu-id="f7792-120">Node.js version 0.10.x or later.</span></span>
* <span data-ttu-id="f7792-121">Aktywne konto platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="f7792-121">An active Azure account.</span></span> <span data-ttu-id="f7792-122">(Jeśli go nie masz, możesz utworzyć [bezpłatne konto próbne][lnk-free-trial] w zaledwie kilka minut).</span><span class="sxs-lookup"><span data-stu-id="f7792-122">(If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.)</span></span>

## <a name="receive-messages-in-hello-simulated-device-app"></a><span data-ttu-id="f7792-123">Odbieranie komunikatów w aplikacji symulowane urządzenie hello</span><span class="sxs-lookup"><span data-stu-id="f7792-123">Receive messages in hello simulated device app</span></span>
<span data-ttu-id="f7792-124">W tej sekcji możesz zmodyfikować aplikację symulowane urządzenie hello utworzony w [Rozpoczynanie pracy z Centrum IoT] tooreceive komunikaty chmury do urządzenia z Centrum IoT hello.</span><span class="sxs-lookup"><span data-stu-id="f7792-124">In this section, you modify hello simulated device app you created in [Get started with IoT Hub] tooreceive cloud-to-device messages from hello IoT hub.</span></span>

1. <span data-ttu-id="f7792-125">Za pomocą edytora tekstu, otwórz plik SimulatedDevice.js hello.</span><span class="sxs-lookup"><span data-stu-id="f7792-125">Using a text editor, open hello SimulatedDevice.js file.</span></span>
2. <span data-ttu-id="f7792-126">Modyfikowanie hello **connectCallback** funkcji toohandle wiadomości wysyłane z Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="f7792-126">Modify hello **connectCallback** function toohandle messages sent from IoT Hub.</span></span> <span data-ttu-id="f7792-127">W tym przykładzie urządzenia hello zawsze wywołuje hello **pełną** funkcji toonotify został on przetworzony wiadomość hello Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="f7792-127">In this example, hello device always invokes hello **complete** function toonotify IoT Hub that it has processed hello message.</span></span> <span data-ttu-id="f7792-128">Nową wersję pakietu hello **connectCallback** funkcja wygląda powitania po fragment kodu:</span><span class="sxs-lookup"><span data-stu-id="f7792-128">Your new version of hello **connectCallback** function looks like hello following snippet:</span></span>
   
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
        // Create a message and send it toohello IoT Hub every second
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
   > <span data-ttu-id="f7792-129">Witaj w przypadku wybrania protokołu HTTP zamiast MQTT lub AMQP jako transportu hello **DeviceClient** wystąpienia sprawdza, czy komunikaty z Centrum IoT rzadko (mniej niż co 25 minut).</span><span class="sxs-lookup"><span data-stu-id="f7792-129">If you use HTTP instead of MQTT or AMQP as hello transport, hello **DeviceClient** instance checks for messages from IoT Hub infrequently (less than every 25 minutes).</span></span> <span data-ttu-id="f7792-130">Aby uzyskać więcej informacji o różnicach hello MQTT, AMQP i HTTP pomocy technicznej i ograniczania Centrum IoT, zobacz hello [Centrum IoT — przewodnik dewelopera][IoT Hub developer guide - C2D].</span><span class="sxs-lookup"><span data-stu-id="f7792-130">For more information about hello differences between MQTT, AMQP and HTTP support, and IoT Hub throttling, see hello [IoT Hub developer guide][IoT Hub developer guide - C2D].</span></span>
   > 
   > 

## <a name="send-a-cloud-to-device-message"></a><span data-ttu-id="f7792-131">Wyślij wiadomość chmury do urządzenia</span><span class="sxs-lookup"><span data-stu-id="f7792-131">Send a cloud-to-device message</span></span>
<span data-ttu-id="f7792-132">W tej sekcji utworzysz aplikację konsoli Node.js, która wysyła komunikaty chmury do urządzenia toohello symulowane urządzenie aplikacji.</span><span class="sxs-lookup"><span data-stu-id="f7792-132">In this section, you create a Node.js console app that sends cloud-to-device messages toohello simulated device app.</span></span> <span data-ttu-id="f7792-133">Należy hello identyfikator urządzenia urządzenia hello dodane w hello [Rozpoczynanie pracy z Centrum IoT] samouczka.</span><span class="sxs-lookup"><span data-stu-id="f7792-133">You need hello device ID of hello device you added in hello [Get started with IoT Hub] tutorial.</span></span> <span data-ttu-id="f7792-134">Centrum, które można znaleźć w hello muszą zostać hello parametry połączenia Centrum IoT [portalu Azure].</span><span class="sxs-lookup"><span data-stu-id="f7792-134">You also need hello IoT Hub connection string for your hub that you can find in hello [Azure portal].</span></span>

1. <span data-ttu-id="f7792-135">Utwórz pusty folder o nazwie **sendcloudtodevicemessage**.</span><span class="sxs-lookup"><span data-stu-id="f7792-135">Create an empty folder called **sendcloudtodevicemessage**.</span></span> <span data-ttu-id="f7792-136">W hello **sendcloudtodevicemessage** folderu, Utwórz plik package.json za pomocą hello następujące polecenie z wiersza polecenia.</span><span class="sxs-lookup"><span data-stu-id="f7792-136">In hello **sendcloudtodevicemessage** folder, create a package.json file using hello following command at your command prompt.</span></span> <span data-ttu-id="f7792-137">Zaakceptuj wszystkie domyślne hello:</span><span class="sxs-lookup"><span data-stu-id="f7792-137">Accept all hello defaults:</span></span>
   
    ```shell
    npm init
    ```
2. <span data-ttu-id="f7792-138">Z wiersza polecenia w hello **sendcloudtodevicemessage** folderu, uruchom następujące polecenie tooinstall hello hello **Centrum iothub azure** pakietu:</span><span class="sxs-lookup"><span data-stu-id="f7792-138">At your command prompt in hello **sendcloudtodevicemessage** folder, run hello following command tooinstall hello **azure-iothub** package:</span></span>
   
    ```shell
    npm install azure-iothub --save
    ```
3. <span data-ttu-id="f7792-139">Za pomocą edytora tekstu, Utwórz **SendCloudToDeviceMessage.js** pliku w hello **sendcloudtodevicemessage** folderu.</span><span class="sxs-lookup"><span data-stu-id="f7792-139">Using a text editor, create a **SendCloudToDeviceMessage.js** file in hello **sendcloudtodevicemessage** folder.</span></span>
4. <span data-ttu-id="f7792-140">Dodaj następujące hello `require` instrukcje na powitania początek hello **SendCloudToDeviceMessage.js** pliku:</span><span class="sxs-lookup"><span data-stu-id="f7792-140">Add hello following `require` statements at hello start of hello **SendCloudToDeviceMessage.js** file:</span></span>
   
    ```javascript
    'use strict';
   
    var Client = require('azure-iothub').Client;
    var Message = require('azure-iot-common').Message;
    ```
5. <span data-ttu-id="f7792-141">Dodaj hello zbyt następującego kodu**SendCloudToDeviceMessage.js** pliku.</span><span class="sxs-lookup"><span data-stu-id="f7792-141">Add hello following code too**SendCloudToDeviceMessage.js** file.</span></span> <span data-ttu-id="f7792-142">Zastąp wartość symbolu zastępczego hello "{iot hub parametry połączenia}" hello Centrum IoT parametry połączenia dla koncentratora hello utworzony w hello [Rozpoczynanie pracy z Centrum IoT] samouczka.</span><span class="sxs-lookup"><span data-stu-id="f7792-142">Replace hello "{iot hub connection string}" placeholder value with hello IoT Hub connection string for hello hub you created in hello [Get started with IoT Hub] tutorial.</span></span> <span data-ttu-id="f7792-143">Zastąp symbol zastępczy hello "{identyfikator urządzenia}" z Identyfikatorem urządzenia hello urządzenia hello dodane w hello [Rozpoczynanie pracy z Centrum IoT] samouczek:</span><span class="sxs-lookup"><span data-stu-id="f7792-143">Replace hello "{device id}" placeholder with hello device ID of hello device you added in hello [Get started with IoT Hub] tutorial:</span></span>
   
    ```javascript
    var connectionString = '{iot hub connection string}';
    var targetDevice = '{device id}';
   
    var serviceClient = Client.fromConnectionString(connectionString);
    ```
6. <span data-ttu-id="f7792-144">Dodaj powitania po funkcja tooprint operacji wyniki toohello konsoli:</span><span class="sxs-lookup"><span data-stu-id="f7792-144">Add hello following function tooprint operation results toohello console:</span></span>
   
    ```javascript
    function printResultFor(op) {
      return function printResult(err, res) {
        if (err) console.log(op + ' error: ' + err.toString());
        if (res) console.log(op + ' status: ' + res.constructor.name);
      };
    }
    ```
7. <span data-ttu-id="f7792-145">Dodaj powitania po funkcja tooprint dostarczania opinii wiadomości toohello konsoli:</span><span class="sxs-lookup"><span data-stu-id="f7792-145">Add hello following function tooprint delivery feedback messages toohello console:</span></span>
   
    ```javascript
    function receiveFeedback(err, receiver){
      receiver.on('message', function (msg) {
        console.log('Feedback message:')
        console.log(msg.getData().toString('utf-8'));
      });
    }
    ```
8. <span data-ttu-id="f7792-146">Dodaj następujące hello code toosend urządzenia tooyour wiadomości i obsługi wiadomość hello, gdy urządzenie hello potwierdza wiadomości powitania chmury do urządzenia:</span><span class="sxs-lookup"><span data-stu-id="f7792-146">Add hello following code toosend a message tooyour device and handle hello feedback message when hello device acknowledges hello cloud-to-device message:</span></span>
   
    ```javascript
    serviceClient.open(function (err) {
      if (err) {
        console.error('Could not connect: ' + err.message);
      } else {
        console.log('Service client connected');
        serviceClient.getFeedbackReceiver(receiveFeedback);
        var message = new Message('Cloud toodevice message.');
        message.ack = 'full';
        message.messageId = "My Message ID";
        console.log('Sending message: ' + message.getData());
        serviceClient.send(targetDevice, message, printResultFor('send'));
      }
    });
    ```
9. <span data-ttu-id="f7792-147">Zapisz i Zamknij **SendCloudToDeviceMessage.js** pliku.</span><span class="sxs-lookup"><span data-stu-id="f7792-147">Save and close **SendCloudToDeviceMessage.js** file.</span></span>

## <a name="run-hello-applications"></a><span data-ttu-id="f7792-148">Uruchamianie aplikacji hello</span><span class="sxs-lookup"><span data-stu-id="f7792-148">Run hello applications</span></span>
<span data-ttu-id="f7792-149">Wszystko jest teraz gotowy toorun hello aplikacji.</span><span class="sxs-lookup"><span data-stu-id="f7792-149">You are now ready toorun hello applications.</span></span>

1. <span data-ttu-id="f7792-150">W wierszu polecenia hello w hello **simulateddevice** folderu, uruchom następujące hello polecenia toosend telemetrii tooIoT koncentratora i toolisten komunikatów chmury do urządzenia:</span><span class="sxs-lookup"><span data-stu-id="f7792-150">At hello command prompt in hello **simulateddevice** folder, run hello following command toosend telemetry tooIoT Hub and toolisten for cloud-to-device messages:</span></span>
   
    ```shell
    node SimulatedDevice.js 
    ```
   
    ![Uruchamianie aplikacji symulowane urządzenie hello][img-simulated-device]
2. <span data-ttu-id="f7792-152">W wierszu polecenia w hello **sendcloudtodevicemessage** folderu, uruchom następujące polecenie toosend hello komunikatu chmura urządzenie i poczekaj, aż hello potwierdzenia opinii:</span><span class="sxs-lookup"><span data-stu-id="f7792-152">At a command prompt in hello **sendcloudtodevicemessage** folder, run hello following command toosend a cloud-to-device message and wait for hello acknowledgment feedback:</span></span>
   
    ```shell
    node SendCloudToDeviceMessage.js 
    ```
   
    ![Uruchom polecenie hello toosend hello aplikacji, chmury do urządzenia][img-send-command]
   
   > [!NOTE]
   > <span data-ttu-id="f7792-154">Sake na prostotę w tym samouczku nie implementuje wszystkie zasady ponawiania.</span><span class="sxs-lookup"><span data-stu-id="f7792-154">For simplicity's sake, this tutorial does not implement any retry policy.</span></span> <span data-ttu-id="f7792-155">W kodzie produkcyjnym, należy zaimplementować zasady ponawiania (na przykład wykładniczego wycofywania), zgodnie z sugestią podaną w artykuł w witrynie MSDN hello [obsługi błędów przejściowych].</span><span class="sxs-lookup"><span data-stu-id="f7792-155">In production code, you should implement retry policies (such as exponential backoff), as suggested in hello MSDN article [Transient Fault Handling].</span></span>
   > 
   > 

## <a name="next-steps"></a><span data-ttu-id="f7792-156">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="f7792-156">Next steps</span></span>
<span data-ttu-id="f7792-157">W tym samouczku można przedstawiono sposób toosend i odbierania wiadomości chmury do urządzenia.</span><span class="sxs-lookup"><span data-stu-id="f7792-157">In this tutorial, you learned how toosend and receive cloud-to-device messages.</span></span> 

<span data-ttu-id="f7792-158">Przykłady toosee kompletnych rozwiązań end-to-end korzystających z Centrum IoT, zobacz [pakiet IoT Azure].</span><span class="sxs-lookup"><span data-stu-id="f7792-158">toosee examples of complete end-to-end solutions that use IoT Hub, see [Azure IoT Suite].</span></span>

<span data-ttu-id="f7792-159">toolearn więcej informacji na temat tworzenia rozwiązań z Centrum IoT, zobacz hello [Centrum IoT — przewodnik dewelopera].</span><span class="sxs-lookup"><span data-stu-id="f7792-159">toolearn more about developing solutions with IoT Hub, see hello [IoT Hub developer guide].</span></span>

<!-- Images -->
[img-simulated-device]: media/iot-hub-node-node-c2d/receivec2d.png
[img-send-command]:  media/iot-hub-node-node-c2d/sendc2d.png

<!-- Links -->

[Rozpoczynanie pracy z Centrum IoT]: iot-hub-node-node-getstarted.md
[IoT Hub developer guide - C2D]: iot-hub-devguide-messaging.md
[Centrum IoT — przewodnik dewelopera]: iot-hub-devguide.md
[Azure IoT Developer Center]: http://www.azure.com/develop/iot
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[lnk-dev-setup]: https://github.com/Azure/azure-iot-sdk-node/tree/master/doc/node-devbox-setup.md
[obsługi błędów przejściowych]: https://msdn.microsoft.com/library/hh680901(v=pandp.50).aspx
[portalu Azure]: https://portal.azure.com
[pakiet IoT Azure]: https://azure.microsoft.com/documentation/suites/iot-suite/
