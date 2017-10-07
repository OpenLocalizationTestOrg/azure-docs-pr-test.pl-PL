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
# <a name="send-cloud-to-device-messages-with-iot-hub-node"></a>Wysyłanie komunikatów chmury do urządzenia z Centrum IoT (węzeł)
[!INCLUDE [iot-hub-selector-c2d](../../includes/iot-hub-selector-c2d.md)]

## <a name="introduction"></a>Wprowadzenie
Centrum IoT Azure jest w pełni zarządzaną usługę, która umożliwia włączanie i niezawodności komunikację dwukierunkową między milionów urządzeń i zaplecze rozwiązania. Witaj [Rozpoczynanie pracy z Centrum IoT] samouczek pokazuje, jak udostępnić tożsamość urządzenia w nim toocreate Centrum IoT i kodu aplikacji symulowane urządzenie, który wysyła wiadomości urządzenia do chmury.

W tym samouczku opiera się na [Rozpoczynanie pracy z Centrum IoT]. Jak przedstawiono na:

* Z z zaplecza rozwiązania należy wysłać pojedyncze urządzenie tooa wiadomości chmury do urządzenia za pośrednictwem Centrum IoT.
* Komunikaty chmury do urządzenia na urządzeniu.
* Z sieci zaplecza rozwiązania, żądania potwierdzenia dostarczenia (*opinii*) dla wiadomości wysyłane tooa urządzenie z Centrum IoT.

Więcej informacji na temat wiadomości chmury do urządzenia można znaleźć w hello [Centrum IoT — przewodnik dewelopera][IoT Hub developer guide - C2D].

Na końcu hello tego samouczka możesz uruchomić dwóch aplikacji konsoli Node.js:

* **SimulatedDevice**, zmodyfikowanej wersji aplikacji hello utworzone w [Rozpoczynanie pracy z Centrum IoT], która łączy się z Centrum IoT tooyour i odbiera komunikaty chmury do urządzenia.
* **SendCloudToDeviceMessage**, który wysyła aplikacji symulowane urządzenie toohello komunikat chmury do urządzenia, za pośrednictwem Centrum IoT i następnie odbiera jego potwierdzenia dostarczenia.

> [!NOTE]
> Centrum IoT obsługuje zestawu SDK dla wielu platform urządzeń i języków (w tym C, Java i Javascript) za pośrednictwem zestawy SDK urządzenia Azure IoT. Instrukcje krok po kroku dotyczące tooconnect samouczek toothis urządzenia kodu i zazwyczaj tooAzure Centrum IoT, zobacz temat hello [Azure IoT Developer Center].
> 
> 

toocomplete tego samouczka należy hello następujące:

* Środowisko Node.js w wersji 0.10.x lub nowszej.
* Aktywne konto platformy Azure. (Jeśli go nie masz, możesz utworzyć [bezpłatne konto próbne][lnk-free-trial] w zaledwie kilka minut).

## <a name="receive-messages-in-hello-simulated-device-app"></a>Odbieranie komunikatów w aplikacji symulowane urządzenie hello
W tej sekcji możesz zmodyfikować aplikację symulowane urządzenie hello utworzony w [Rozpoczynanie pracy z Centrum IoT] tooreceive komunikaty chmury do urządzenia z Centrum IoT hello.

1. Za pomocą edytora tekstu, otwórz plik SimulatedDevice.js hello.
2. Modyfikowanie hello **connectCallback** funkcji toohandle wiadomości wysyłane z Centrum IoT. W tym przykładzie urządzenia hello zawsze wywołuje hello **pełną** funkcji toonotify został on przetworzony wiadomość hello Centrum IoT. Nową wersję pakietu hello **connectCallback** funkcja wygląda powitania po fragment kodu:
   
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
   > Witaj w przypadku wybrania protokołu HTTP zamiast MQTT lub AMQP jako transportu hello **DeviceClient** wystąpienia sprawdza, czy komunikaty z Centrum IoT rzadko (mniej niż co 25 minut). Aby uzyskać więcej informacji o różnicach hello MQTT, AMQP i HTTP pomocy technicznej i ograniczania Centrum IoT, zobacz hello [Centrum IoT — przewodnik dewelopera][IoT Hub developer guide - C2D].
   > 
   > 

## <a name="send-a-cloud-to-device-message"></a>Wyślij wiadomość chmury do urządzenia
W tej sekcji utworzysz aplikację konsoli Node.js, która wysyła komunikaty chmury do urządzenia toohello symulowane urządzenie aplikacji. Należy hello identyfikator urządzenia urządzenia hello dodane w hello [Rozpoczynanie pracy z Centrum IoT] samouczka. Centrum, które można znaleźć w hello muszą zostać hello parametry połączenia Centrum IoT [portalu Azure].

1. Utwórz pusty folder o nazwie **sendcloudtodevicemessage**. W hello **sendcloudtodevicemessage** folderu, Utwórz plik package.json za pomocą hello następujące polecenie z wiersza polecenia. Zaakceptuj wszystkie domyślne hello:
   
    ```shell
    npm init
    ```
2. Z wiersza polecenia w hello **sendcloudtodevicemessage** folderu, uruchom następujące polecenie tooinstall hello hello **Centrum iothub azure** pakietu:
   
    ```shell
    npm install azure-iothub --save
    ```
3. Za pomocą edytora tekstu, Utwórz **SendCloudToDeviceMessage.js** pliku w hello **sendcloudtodevicemessage** folderu.
4. Dodaj następujące hello `require` instrukcje na powitania początek hello **SendCloudToDeviceMessage.js** pliku:
   
    ```javascript
    'use strict';
   
    var Client = require('azure-iothub').Client;
    var Message = require('azure-iot-common').Message;
    ```
5. Dodaj hello zbyt następującego kodu**SendCloudToDeviceMessage.js** pliku. Zastąp wartość symbolu zastępczego hello "{iot hub parametry połączenia}" hello Centrum IoT parametry połączenia dla koncentratora hello utworzony w hello [Rozpoczynanie pracy z Centrum IoT] samouczka. Zastąp symbol zastępczy hello "{identyfikator urządzenia}" z Identyfikatorem urządzenia hello urządzenia hello dodane w hello [Rozpoczynanie pracy z Centrum IoT] samouczek:
   
    ```javascript
    var connectionString = '{iot hub connection string}';
    var targetDevice = '{device id}';
   
    var serviceClient = Client.fromConnectionString(connectionString);
    ```
6. Dodaj powitania po funkcja tooprint operacji wyniki toohello konsoli:
   
    ```javascript
    function printResultFor(op) {
      return function printResult(err, res) {
        if (err) console.log(op + ' error: ' + err.toString());
        if (res) console.log(op + ' status: ' + res.constructor.name);
      };
    }
    ```
7. Dodaj powitania po funkcja tooprint dostarczania opinii wiadomości toohello konsoli:
   
    ```javascript
    function receiveFeedback(err, receiver){
      receiver.on('message', function (msg) {
        console.log('Feedback message:')
        console.log(msg.getData().toString('utf-8'));
      });
    }
    ```
8. Dodaj następujące hello code toosend urządzenia tooyour wiadomości i obsługi wiadomość hello, gdy urządzenie hello potwierdza wiadomości powitania chmury do urządzenia:
   
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
9. Zapisz i Zamknij **SendCloudToDeviceMessage.js** pliku.

## <a name="run-hello-applications"></a>Uruchamianie aplikacji hello
Wszystko jest teraz gotowy toorun hello aplikacji.

1. W wierszu polecenia hello w hello **simulateddevice** folderu, uruchom następujące hello polecenia toosend telemetrii tooIoT koncentratora i toolisten komunikatów chmury do urządzenia:
   
    ```shell
    node SimulatedDevice.js 
    ```
   
    ![Uruchamianie aplikacji symulowane urządzenie hello][img-simulated-device]
2. W wierszu polecenia w hello **sendcloudtodevicemessage** folderu, uruchom następujące polecenie toosend hello komunikatu chmura urządzenie i poczekaj, aż hello potwierdzenia opinii:
   
    ```shell
    node SendCloudToDeviceMessage.js 
    ```
   
    ![Uruchom polecenie hello toosend hello aplikacji, chmury do urządzenia][img-send-command]
   
   > [!NOTE]
   > Sake na prostotę w tym samouczku nie implementuje wszystkie zasady ponawiania. W kodzie produkcyjnym, należy zaimplementować zasady ponawiania (na przykład wykładniczego wycofywania), zgodnie z sugestią podaną w artykuł w witrynie MSDN hello [obsługi błędów przejściowych].
   > 
   > 

## <a name="next-steps"></a>Następne kroki
W tym samouczku można przedstawiono sposób toosend i odbierania wiadomości chmury do urządzenia. 

Przykłady toosee kompletnych rozwiązań end-to-end korzystających z Centrum IoT, zobacz [pakiet IoT Azure].

toolearn więcej informacji na temat tworzenia rozwiązań z Centrum IoT, zobacz hello [Centrum IoT — przewodnik dewelopera].

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
