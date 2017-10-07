---
title: "Centrum IoT aaaAzure bezpośrednie metod (węzeł) | Dokumentacja firmy Microsoft"
description: "Jak toouse Centrum IoT Azure bezpośrednie metody. Node.js tooimplement aplikacji symulowane urządzenie, która zawiera metodę bezpośredniego i aplikacji usługi, która wywołuje metodę bezpośredniego hello są używane hello Azure IoT SDK."
services: iot-hub
documentationcenter: 
author: nberdy
manager: timlt
editor: 
ms.assetid: ea9c73ca-7778-4e38-a8f1-0bee9d142f04
ms.service: iot-hub
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/25/2017
ms.author: nberdy
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 12300ba451816fec1f80163b633f6b6e411d9e5c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="use-direct-methods-on-your-iot-device-with-nodejs"></a>Użyj metody bezpośrednio na urządzeniu IoT z Node.js
[!INCLUDE [iot-hub-selector-c2d-methods](../../includes/iot-hub-selector-c2d-methods.md)]

Na końcu hello tego samouczka znajdują się dwie aplikacje konsoli Node.js:

* **CallMethodOnDevice.js**, która wywołuje metodę w aplikacji symulowane urządzenie hello i wyświetla hello odpowiedzi.
* **SimulatedDevice.js**, która łączy się tooyour Centrum IoT z tożsamości urządzenia hello utworzony wcześniej i odpowiada toohello metody wywoływane przez hello chmury.

> [!NOTE]
> Artykuł Hello [Azure IoT SDK] [ lnk-hub-sdks] zawiera informacje o hello Azure IoT SDK, której można toobuild toorun zarówno aplikacje na urządzeniach i z zaplecza rozwiązania.
> 
> 

toocomplete tego samouczka należy hello następujące:

* Środowisko Node.js w wersji 0.10.x lub nowszej.
* Aktywne konto platformy Azure. (Jeśli go nie masz, możesz utworzyć [bezpłatne konto próbne][lnk-free-trial] w zaledwie kilka minut).

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity](../../includes/iot-hub-get-started-create-device-identity.md)]

## <a name="create-a-simulated-device-app"></a>Tworzenie aplikacji symulowanego urządzenia
W tej sekcji utworzysz aplikację konsoli Node.js, która odpowiada tooa metody wywoływane przez hello chmury.

1. Utwórz nowy pusty folder o nazwie **simulateddevice**. W hello **simulateddevice** folderu, Utwórz plik package.json za pomocą hello następujące polecenie z wiersza polecenia. Zaakceptuj wszystkie domyślne hello:
   
    ```
    npm init
    ```
2. Z wiersza polecenia w hello **simulateddevice** folderu, uruchom następujące polecenie tooinstall hello hello **azure iot urządzenia** pakiet SDK urządzenia i **azure-iot urządzenie mqtt**pakietu:
   
    ```
    npm install azure-iot-device azure-iot-device-mqtt --save
    ```
3. Za pomocą edytora tekstu, Utwórz nową **SimulatedDevice.js** pliku w hello **simulateddevice** folderu.
4. Dodaj następujące hello `require` instrukcje na powitania początek hello **SimulatedDevice.js** pliku:
   
    ```
    'use strict';
   
    var Mqtt = require('azure-iot-device-mqtt').Mqtt;
    var DeviceClient = require('azure-iot-device').Client;
    ```
5. Dodaj **connectionString** zmiennej i korzystać z niego toocreate **DeviceClient** wystąpienia. Zastąp **{ciąg połączenia urządzenia}** przy użyciu parametrów połączenia urządzenia hello wygenerowanych w hello *tworzenie tożsamości urządzenia* sekcji:
   
    ```
    var connectionString = '{device connection string}';
    var client = DeviceClient.fromConnectionString(connectionString, Mqtt);
    ```
6. Dodaj następujące metody hello tooimplement funkcji na urządzeniu hello hello:
   
    ```
    function onWriteLine(request, response) {
        console.log(request.payload);
   
        response.send(200, 'Input was written toolog.', function(err) {
            if(err) {
                console.error('An error ocurred when sending a method response:\n' + err.toString());
            } else {
                console.log('Response toomethod \'' + request.methodName + '\' sent successfully.' );
            }
        });
    }
    ```
7. Otwórz Centrum IoT tooyour połączenia hello i uruchomić odbiornik metody hello zainicjować:
   
    ```
    client.open(function(err) {
        if (err) {
            console.error('could not open IotHub client');
        }  else {
            console.log('client opened');
            client.onDeviceMethod('writeLine', onWriteLine);
        }
    });
    ```
8. Zapisz i zamknij hello **SimulatedDevice.js** pliku.

> [!NOTE]
> rzeczy tookeep proste, w tym samouczku nie implementuje wszystkie zasady ponawiania. W kodzie produkcyjnym, należy zaimplementować zasady ponawiania (np. Ponów próbę połączenia), zgodnie z sugestią podaną w artykuł w witrynie MSDN hello [obsługi błędów przejściowych][lnk-transient-faults].
> 
> 

## <a name="call-a-method-on-a-device"></a>Wywołanie metody na urządzeniu
W tej sekcji utworzysz aplikację konsoli Node.js, która wywołuje metodę hello symulowane urządzenie aplikacji, a następnie wyświetla hello odpowiedzi.

1. Utwórz nowy, pusty folder o nazwie **callmethodondevice**. W hello **callmethodondevice** folderu, Utwórz plik package.json za pomocą hello następujące polecenie z wiersza polecenia. Zaakceptuj wszystkie domyślne hello:
   
    ```
    npm init
    ```
2. Z wiersza polecenia w hello **callmethodondevice** folderu, uruchom następujące polecenie tooinstall hello hello **Centrum iothub azure** pakietu:
   
    ```
    npm install azure-iothub --save
    ```
3. Za pomocą edytora tekstu, Utwórz **CallMethodOnDevice.js** pliku w hello **callmethodondevice** folderu.
4. Dodaj następujące hello `require` instrukcje na powitania początek hello **CallMethodOnDevice.js** pliku:
   
    ```
    'use strict';
   
    var Client = require('azure-iothub').Client;
    ```
5. Dodaj powitania po deklaracji zmiennej i zastąp wartość symbolu zastępczego hello hello parametry połączenia Centrum IoT Centrum:
   
    ```
    var connectionString = '{iothub connection string}';
    var methodName = 'writeLine';
    var deviceId = 'myDeviceId';
    ```
6. Tworzenie Centrum IoT tooyour powitania klienta tooopen hello połączenia.
   
    ```
    var client = Client.fromConnectionString(connectionString);
    ```
7. Dodaj hello funkcja tooinvoke hello urządzenia metody drukowania hello urządzenia odpowiedzi toohello konsoli i po:
   
    ```
    var methodParams = {
        methodName: methodName,
        payload: 'hello world',
        timeoutInSeconds: 30
    };
   
    client.invokeDeviceMethod(deviceId, methodParams, function (err, result) {
        if (err) {
            console.error('Failed tooinvoke method \'' + methodName + '\': ' + err.message);
        } else {
            console.log(methodName + ' on ' + deviceId + ':');
            console.log(JSON.stringify(result, null, 2));
        }
    });
    ```
8. Zapisz i zamknij hello **CallMethodOnDevice.js** pliku.

## <a name="run-hello-apps"></a>Uruchamianie aplikacji hello
Wszystko jest teraz gotowy toorun hello aplikacji.

1. W wierszu polecenia w hello **simulateddevice** folderu, uruchom następujące polecenia toostart nasłuchiwania dla wywołań metod z Centrum IoT hello:
   
    ```
    node SimulatedDevice.js
    ```
   
    ![][7]
2. W wierszu polecenia w hello **callmethodondevice** folderu Uruchom hello następujące polecenia toobegin monitorowania Centrum IoT:
   
    ```
    node CallMethodOnDevice.js 
    ```
   
    ![][8]
3. Zostaną wyświetlone urządzenia hello zareagowania metody toohello przez drukowanie wiadomość hello i aplikacji hello, nazywane hello metoda wyświetlania hello odpowiedzi z urządzenia hello:
   
    ![][9]

## <a name="next-steps"></a>Następne kroki
W tym samouczku został skonfigurowany nowego centrum IoT w portalu Azure hello i w rejestrze tożsamości Centrum IoT hello zostanie utworzona tożsamość urządzenia. Użyto tego urządzenia tożsamości tooenable hello symulowane urządzenie aplikacji tooreact toomethods wywołana przez hello chmury. Utworzono aplikację, która wywołuje metody na urządzeniu hello i wyświetla hello odpowiedzi z hello urządzenia. 

toocontinue wprowadzenie do korzystania z Centrum IoT i tooexplore innych scenariuszach IoT, zobacz:

* [Rozpoczynanie pracy z Centrum IoT]
* [Planowanie zadań na wielu urządzeniach][lnk-devguide-jobs]

toolearn tooextend IoT metody rozwiązania i harmonogram wywołuje na wielu urządzeniach, zobacz hello [emisji zadania i harmonogramu] [ lnk-tutorial-jobs] samouczka.

<!-- Images. -->
[7]: ./media/iot-hub-node-node-direct-methods/run-simulated-device.png
[8]: ./media/iot-hub-node-node-direct-methods/run-callmethodondevice.png
[9]: ./media/iot-hub-node-node-direct-methods/methods-output.png

<!-- Links -->
[lnk-transient-faults]: https://msdn.microsoft.com/library/hh680901(v=pandp.50).aspx

[lnk-dev-setup]: https://github.com/Azure/azure-iot-sdk-node/tree/master/doc/node-devbox-setup.md

[lnk-hub-sdks]: iot-hub-devguide-sdks.md
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[lnk-portal]: https://portal.azure.com/

[lnk-devguide-jobs]: iot-hub-devguide-jobs.md
[lnk-tutorial-jobs]: iot-hub-node-node-schedule-jobs.md
[lnk-devguide-methods]: iot-hub-devguide-direct-methods.md
[lnk-devguide-mqtt]: iot-hub-mqtt-support.md

[Send Cloud-to-Device messages with IoT Hub]: iot-hub-csharp-csharp-c2d.md
[Process Device-to-Cloud messages]: iot-hub-csharp-csharp-process-d2c.md
[Rozpoczynanie pracy z Centrum IoT]: iot-hub-node-node-getstarted.md
