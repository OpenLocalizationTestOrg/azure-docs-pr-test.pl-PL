---
title: "aaaGet pracę z Centrum IoT Azure (węzeł) | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak urządzenia chmury toosend wiadomości tooAzure Centrum IoT przy użyciu IoT zestawy SDK dla środowiska Node.js. Utworzyć symulowane urządzenie i tooregister aplikacji usługi, urządzenia, wysyłania wiadomości i odczytywać wiadomości z Centrum IoT."
services: iot-hub
documentationcenter: nodejs
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 56618522-9a31-42c6-94bf-55e2233b39ac
ms.service: iot-hub
ms.devlang: javascript
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/22/2017
ms.author: dobett
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: d0747895365f2359a9c38ea1e85a5881d6efec0b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="connect-your-simulated-device-tooyour-iot-hub-using-node"></a>Połącz z Centrum IoT tooyour symulowane urządzenie za pomocą węzła
[!INCLUDE [iot-hub-selector-get-started](../../includes/iot-hub-selector-get-started.md)]

Na końcu hello tego samouczka masz trzech aplikacji konsoli Node.js:

* **CreateDeviceIdentity.js**, co powoduje tożsamości urządzenia i skojarzony klucz tooconnect aplikacji symulowane urządzenie.
* **ReadDeviceToCloudMessages.js**, który zawiera dane telemetryczne hello wysyłane przez aplikację symulowane urządzenie.
* **SimulatedDevice.js**, która łączy się tooyour Centrum IoT z tożsamości urządzenia hello utworzony wcześniej i wysyła komunikat telemetrii co drugi przy użyciu hello MQTT protokołu.

> [!NOTE]
> Artykuł Hello [Azure IoT SDK] [ lnk-hub-sdks] zawiera informacje o hello Azure IoT SDK, której można toobuild toorun zarówno aplikacje na urządzeniach i z zaplecza rozwiązania.
> 
> 

toocomplete tego samouczka należy hello następujące:

* Środowisko Node.js w wersji 0.10.x lub nowszej.
* Aktywne konto platformy Azure. (Jeśli go nie masz, możesz utworzyć [bezpłatne konto próbne][lnk-free-trial] w zaledwie kilka minut).

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

Utworzono centrum IoT. Masz hello nazwy hosta Centrum IoT i hello parametry połączenia Centrum IoT należy toocomplete hello pozostałej części tego samouczka.

## <a name="create-a-device-identity"></a>Tworzenie tożsamości urządzenia
W tej sekcji utworzysz aplikację konsoli Node.js, która tworzy tożsamość urządzenia w rejestrze tożsamości hello w Centrum IoT. Urządzenie można połączyć tylko tooIoT koncentratora, jeśli zawiera on wpis w rejestrze tożsamości hello. Aby uzyskać więcej informacji, zobacz hello **rejestru tożsamości** sekcji hello [Centrum IoT — przewodnik dewelopera][lnk-devguide-identity]. Po uruchomieniu tej aplikacji konsoli, generuje on unikatowy identyfikator urządzenia i tooIoT Centrum wiadomości klucz urządzenia można użyć tooidentify się podczas wysyłania urządzenia do chmury.

1. Utwórz nowy pusty folder o nazwie **createdeviceidentity**. W hello **createdeviceidentity** folderu, Utwórz plik package.json za pomocą hello następujące polecenie z wiersza polecenia. Zaakceptuj wszystkie domyślne hello:
   
    ```
    npm init
    ```
2. Z wiersza polecenia w hello **createdeviceidentity** folderu, uruchom następujące polecenie tooinstall hello hello **Centrum iothub azure** pakiet SDK usługi:
   
    ```
    npm install azure-iothub --save
    ```
3. Za pomocą edytora tekstu, Utwórz **CreateDeviceIdentity.js** pliku w hello **createdeviceidentity** folderu.
4. Dodaj następujące hello `require` instrukcji na początku hello hello **CreateDeviceIdentity.js** pliku:
   
    ```
    'use strict';
   
    var iothub = require('azure-iothub');
    ```
5. Dodaj hello następującego kodu toohello **CreateDeviceIdentity.js** plików i Zastąp wartości symbolu zastępczego hello hello Centrum IoT parametry połączenia dla koncentratora hello utworzony w poprzedniej sekcji hello: 
   
    ```
    var connectionString = '{iothub connection string}';
   
    var registry = iothub.Registry.fromConnectionString(connectionString);
    ```
6. Dodaj hello następującego kodu toocreate definicję urządzenia w rejestrze tożsamości hello w Centrum IoT. Ten kod tworzy urządzenia, jeśli identyfikator urządzenia hello nie istnieje w rejestrze tożsamości hello, w przeciwnym razie zwraca wartość klucza hello hello istniejące urządzenia:
   
    ```
    var device = {
      deviceId: 'myFirstNodeDevice'
    }
    registry.create(device, function(err, deviceInfo, res) {
      if (err) {
        registry.get(device.deviceId, printDeviceInfo);
      }
      if (deviceInfo) {
        printDeviceInfo(err, deviceInfo, res)
      }
    });
   
    function printDeviceInfo(err, deviceInfo, res) {
      if (deviceInfo) {
        console.log('Device ID: ' + deviceInfo.deviceId);
        console.log('Device key: ' + deviceInfo.authentication.symmetricKey.primaryKey);
      }
    }
    ```
   [!INCLUDE [iot-hub-pii-note-naming-device](../../includes/iot-hub-pii-note-naming-device.md)]

7. Zapisz i zamknij plik **CreateDeviceIdentity.js**.
8. Witaj toorun **createdeviceidentity** aplikacji, wykonaj następujące polecenie w wierszu polecenia hello w folderze createdeviceidentity hello hello:
   
    ```
    node CreateDeviceIdentity.js 
    ```
9. Zanotuj hello **identyfikator urządzenia** i **klucza urządzenia**. Należy te wartości później podczas tworzenia aplikacji, która łączy tooIoT koncentratora jako urządzenie.

> [!NOTE]
> Witaj w rejestrze tożsamości Centrum IoT przechowuje dane tylko Centrum IoT toohello bezpiecznego dostępu tooenable tożsamości urządzenia. Urządzenie toouse identyfikatorów i klucze są przechowywane jako poświadczeń zabezpieczeń i flagi włączone/wyłączone, której można toodisable dostępu dla poszczególnych urządzeń. Jeśli aplikacja wymaga toostore inne metadane specyficzne dla urządzenia, należy go użyć magazynu specyficzne dla aplikacji. Aby uzyskać więcej informacji, zobacz hello [Centrum IoT — przewodnik dewelopera][lnk-devguide-identity].
> 
> 

<a id="D2C_node"></a>
## <a name="receive-device-to-cloud-messages"></a>Odbieranie komunikatów z urządzenia do chmury
W tej sekcji opisano tworzenie aplikacji konsolowej środowiska Node.js, która odczytuje komunikaty z urządzenia do chmury z usługi IoT Hub. Przedstawia Centrum IoT [usługi Event Hubs][lnk-event-hubs-overview]— tooenable zgodne punktu końcowego można tooread wiadomości urządzenia do chmury. elementy tookeep proste, w tym samouczku tworzy podstawowe reader, który nie jest odpowiedni dla wdrożenia wysokiej przepływności. Witaj [przetwarzania komunikatów urządzenia do chmury] [ lnk-process-d2c-tutorial] samouczek pokazuje, jak urządzenia chmury tooprocess komunikatów na dużą skalę. Witaj [Rozpoczynanie pracy z usługą Event Hubs] [ lnk-eventhubs-tutorial] samouczek zawiera dalsze informacje dotyczące sposobu tooprocess komunikaty z usługi Event Hubs i jest toohello odpowiednich punktów końcowych zgodnych z Centrum IoT Centrum zdarzeń.

> [!NOTE]
> Hello punktu końcowego Centrum zdarzeń zgodnych do odczytywania wiadomości urządzenia do chmury zawsze używa protokołu AMQP hello.
> 
> 

1. Utwórz pusty folder o nazwie **readdevicetocloudmessages**. W hello **readdevicetocloudmessages** folderu, Utwórz plik package.json za pomocą hello następujące polecenie z wiersza polecenia. Zaakceptuj wszystkie domyślne hello:
   
    ```
    npm init
    ```
2. Z wiersza polecenia w hello **readdevicetocloudmessages** folderu, uruchom następujące polecenie tooinstall hello hello **usługi centra zdarzeń azure** pakietu:
   
    ```
    npm install azure-event-hubs --save
    ```
3. Za pomocą edytora tekstu, Utwórz **ReadDeviceToCloudMessages.js** pliku w hello **readdevicetocloudmessages** folderu.
4. Dodaj następujące hello `require` instrukcje na powitania początek hello **ReadDeviceToCloudMessages.js** pliku:
   
    ```
    'use strict';
   
    var EventHubClient = require('azure-event-hubs').Client;
    ```
5. Dodaj powitania po deklaracji zmiennej i zastąp wartość symbolu zastępczego hello hello parametry połączenia Centrum IoT Centrum:
   
    ```
    var connectionString = '{iothub connection string}';
    ```
6. Dodaj następujące dwie funkcje, które dane wyjściowe konsoli toohello drukowaniem hello:
   
    ```
    var printError = function (err) {
      console.log(err.message);
    };
   
    var printMessage = function (message) {
      console.log('Message received: ');
      console.log(JSON.stringify(message.body));
      console.log('');
    };
    ```
7. Dodaj następującego kodu toocreate hello hello **EventHubClient**, otwórz hello tooyour połączenia Centrum IoT i tworzenie odbiornika dla każdej partycji. Ta aplikacja używa filtru podczas tworzenia odbiornika, dzięki czemu hello odbiornika odczytuje jedynie tooIoT wiadomości wysłane koncentratora po odbiornika hello zacznie działać. Ten filtr jest przydatne w środowisku testowym, aby zobaczyć tylko hello bieżący zestaw komunikatów. W środowisku produkcyjnym kodu upewnij się, przetwarza wszystkie wiadomości powitania. Aby uzyskać więcej informacji, zobacz hello [jak tooprocess Centrum IoT urządzenia do chmury wiadomości] [ lnk-process-d2c-tutorial] samouczek:
   
    ```
    var client = EventHubClient.fromConnectionString(connectionString);
    client.open()
        .then(client.getPartitionIds.bind(client))
        .then(function (partitionIds) {
            return partitionIds.map(function (partitionId) {
                return client.createReceiver('$Default', partitionId, { 'startAfterTime' : Date.now()}).then(function(receiver) {
                    console.log('Created partition receiver: ' + partitionId)
                    receiver.on('errorReceived', printError);
                    receiver.on('message', printMessage);
                });
            });
        })
        .catch(printError);
    ```
8. Zapisz i zamknij hello **ReadDeviceToCloudMessages.js** pliku.

## <a name="create-a-simulated-device-app"></a>Tworzenie aplikacji symulowanego urządzenia
W tej sekcji utworzysz aplikację konsoli Node.js, która symuluje urządzenia, które wysyła Centrum IoT tooan wiadomości urządzenia do chmury.

1. Utwórz pusty folder o nazwie **simulateddevice**. W hello **simulateddevice** folderu, Utwórz plik package.json za pomocą hello następujące polecenie z wiersza polecenia. Zaakceptuj wszystkie domyślne hello:
   
    ```
    npm init
    ```
2. Z wiersza polecenia w hello **simulateddevice** folderu, uruchom następujące polecenie tooinstall hello hello **azure iot urządzenia** pakiet SDK urządzenia i **azure-iot urządzenie mqtt**pakietu:
   
    ```
    npm install azure-iot-device azure-iot-device-mqtt --save
    ```
3. Za pomocą edytora tekstu, Utwórz **SimulatedDevice.js** pliku w hello **simulateddevice** folderu.
4. Dodaj następujące hello `require` instrukcje na powitania początek hello **SimulatedDevice.js** pliku:
   
    ```
    'use strict';
   
    var clientFromConnectionString = require('azure-iot-device-mqtt').clientFromConnectionString;
    var Message = require('azure-iot-device').Message;
    ```
5. Dodaj **connectionString** zmiennej i korzystać z niego toocreate **klienta** wystąpienia. Zastąp **{youriothostname}** hello nazwę Centrum IoT hello utworzony hello *tworzenia Centrum IoT* sekcji. Zastąp **{yourdevicekey}** o wartości klucza urządzenia hello wygenerowanych w hello *tworzenie tożsamości urządzenia* sekcji:
   
    ```
    var connectionString = 'HostName={youriothostname};DeviceId=myFirstNodeDevice;SharedAccessKey={yourdevicekey}';
   
    var client = clientFromConnectionString(connectionString);
    ```
6. Dodaj następujące dane wyjściowe toodisplay funkcji z aplikacji hello hello:
   
    ```
    function printResultFor(op) {
      return function printResult(err, res) {
        if (err) console.log(op + ' error: ' + err.toString());
        if (res) console.log(op + ' status: ' + res.constructor.name);
      };
    }
    ```
7. Tworzenie wywołania zwrotnego i użyć hello **setInterval** funkcji co sekundę toosend Centrum IoT tooyour komunikat:
   
    ```
    var connectCallback = function (err) {
      if (err) {
        console.log('Could not connect: ' + err);
      } else {
        console.log('Client connected');
   
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
8. Otwórz tooyour połączenia hello Centrum IoT i Rozpocznij wysyłanie wiadomości:
   
    ```
    client.open(connectCallback);
    ```
9. Zapisz i zamknij hello **SimulatedDevice.js** pliku.

> [!NOTE]
> rzeczy tookeep proste, w tym samouczku nie implementuje wszystkie zasady ponawiania. W kodzie produkcyjnym, należy zaimplementować zasady ponawiania (na przykład wykładniczego wycofywania), zgodnie z sugestią podaną w artykuł w witrynie MSDN hello [obsługi błędów przejściowych][lnk-transient-faults].
> 
> 

## <a name="run-hello-apps"></a>Uruchamianie aplikacji hello
Wszystko jest teraz gotowy toorun hello aplikacji.

1. W wierszu polecenia w hello **readdevicetocloudmessages** folderu Uruchom hello następujące polecenia toobegin monitorowania Centrum IoT:
   
    ```
    node ReadDeviceToCloudMessages.js 
    ```
   
    ![Komunikaty o node.js Centrum IoT usługi aplikacji toomonitor urządzenia do chmury][7]
2. W wierszu polecenia w hello **simulateddevice** folderu Uruchom powitania po toobegin polecenie wysyłania Centrum IoT tooyour danych telemetrii:
   
    ```
    node SimulatedDevice.js
    ```
   
    ![Node.js Centrum IoT urządzenia aplikacji toosend urządzenia do chmury wiadomości][8]
3. Witaj **użycia** kafelka w hello [portalu Azure] [ lnk-portal] pokazuje hello liczbę komunikatów wysłanych toohello Centrum IoT:
   
    ![Azure portalu użycie kafelka pokazujący liczbę komunikatów wysyłanych tooIoT Centrum][43]

## <a name="next-steps"></a>Następne kroki
W tym samouczku został skonfigurowany nowego centrum IoT w portalu Azure hello i w rejestrze tożsamości Centrum IoT hello zostanie utworzona tożsamość urządzenia. Użyto tego urządzenia tożsamości tooenable hello symulowane urządzenie aplikacji toosend wiadomości urządzenia do chmury toohello Centrum IoT. Utworzono aplikację, która wyświetla hello komunikatów odebranych przez Centrum IoT hello. 

toocontinue wprowadzenie do korzystania z Centrum IoT i tooexplore innych scenariuszach IoT, zobacz:

* [Łączenie urządzenia][lnk-connect-device]
* [Wprowadzenie do zarządzania urządzeniami][lnk-device-management]
* [Getting started with Azure IoT Edge][lnk-iot-edge] (Rozpoczynanie pracy z usługą Azure IoT Edge)

toolearn tooextend IoT rozwiązanie i procesu urządzenia do chmury wiadomości na dużą skalę, zobacz temat hello [przetwarzania komunikatów urządzenia do chmury] [ lnk-process-d2c-tutorial] samouczka.
[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]


<!-- Images. -->
[7]: ./media/iot-hub-node-node-getstarted/runapp1.png
[8]: ./media/iot-hub-node-node-getstarted/runapp2.png
[43]: ./media/iot-hub-csharp-csharp-getstarted/usage.png

<!-- Links -->
[lnk-transient-faults]: https://msdn.microsoft.com/library/hh680901(v=pandp.50).aspx

[lnk-eventhubs-tutorial]: ../event-hubs/event-hubs-csharp-ephcs-getstarted.md
[lnk-devguide-identity]: iot-hub-devguide-identity-registry.md
[lnk-event-hubs-overview]: ../event-hubs/event-hubs-overview.md

[lnk-dev-setup]: https://github.com/Azure/azure-iot-sdk-node/tree/master/doc/node-devbox-setup.md
[lnk-process-d2c-tutorial]: iot-hub-csharp-csharp-process-d2c.md

[lnk-hub-sdks]: iot-hub-devguide-sdks.md
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[lnk-portal]: https://portal.azure.com/

[lnk-device-management]: iot-hub-node-node-device-management-get-started.md
[lnk-iot-edge]: iot-hub-linux-iot-edge-get-started.md
[lnk-connect-device]: https://azure.microsoft.com/develop/iot/
