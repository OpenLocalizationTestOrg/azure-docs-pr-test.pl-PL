---
title: "aaaGet wprowadzenie do zarządzania urządzeniami Centrum IoT Azure (węzeł) | Dokumentacja firmy Microsoft"
description: "Jak toouse tooinitiate zarządzania urządzeniami Centrum IoT urządzenia zdalnego ponowny rozruch. Node.js tooimplement aplikacji symulowane urządzenie, która zawiera metodę bezpośredniego i aplikacji usługi, która wywołuje metodę bezpośredniego hello są używane hello Azure IoT SDK."
services: iot-hub
documentationcenter: .net
author: juanjperez
manager: timlt
editor: 
ms.assetid: e044006d-ffd6-469b-bc63-c182ad066e31
ms.service: iot-hub
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/25/2017
ms.author: juanpere
ms.openlocfilehash: 5dd1878e71231850fb95f4170b823f1e86c3ee83
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-device-management-node"></a>Wprowadzenie do zarządzania urządzeniami (węzeł)

[!INCLUDE [iot-hub-selector-dm-getstarted](../../includes/iot-hub-selector-dm-getstarted.md)]

Ten samouczek przedstawia sposób wykonania następujących czynności:

* Użyj hello toocreate portalu Azure IoT Hub i Utwórz tożsamość urządzenia w Centrum IoT.
* Tworzenie aplikacji symulowane urządzenie zawierającej bezpośredniego metodę, która wykonuje ponowny rozruch tego urządzenia. Bezpośrednie metody są wywoływane z hello chmury.
* Tworzenie aplikacji konsoli Node.js, który wywołuje metodę bezpośredniego ponowny rozruch hello w hello symulowane urządzenie aplikacji za pośrednictwem Centrum IoT.

Na końcu hello tego samouczka znajdują się dwie aplikacje konsoli Node.js:

**dmpatterns_getstarted_device.js**, o tożsamości urządzenia hello utworzony wcześniej, który łączy Centrum IoT tooyour odbiera metoda bezpośrednia ponowny rozruch, symuluje ponowny rozruch komputera fizycznego i raporty hello czasu ostatniego ponownego uruchomienia hello.

**dmpatterns_getstarted_service.js**, która wywołuje metodę bezpośrednio w aplikacji hello symulowane urządzenie Wyświetla odpowiedź hello, i wyświetla hello zaktualizowane raportowane właściwości.

toocomplete tego samouczka należy hello następujące:

* Środowisko node.js w wersji 0.12.x lub nowszym <br/>  [Przygotowywanie środowiska projektowego] [ lnk-dev-setup] w tym artykule opisano sposób tooinstall Node.js, w tym samouczku w systemie Windows lub Linux.
* Aktywne konto platformy Azure. (Jeśli go nie masz, możesz utworzyć [bezpłatne konto próbne][lnk-free-trial] w zaledwie kilka minut).

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity](../../includes/iot-hub-get-started-create-device-identity.md)]

## <a name="create-a-simulated-device-app"></a>Tworzenie aplikacji symulowanego urządzenia
W tej sekcji zostanie

* Tworzenie aplikacji konsoli Node.js, które odpowiada metoda bezpośrednia tooa wywoływane przez hello chmury
* Wyzwalacz symulowane urządzenie ponowny rozruch
* Hello używany zgłaszane właściwości tooenable urządzeń dwie zapytania tooidentify urządzenia, a podczas ich ostatniego ponownego uruchomienia

1. Utwórz pusty folder o nazwie **manageddevice**.  W hello **manageddevice** folderu, Utwórz plik package.json za pomocą hello następujące polecenie z wiersza polecenia.  Zaakceptuj wszystkie domyślne hello:
   
    ```
    npm init
    ```
2. Z wiersza polecenia w hello **manageddevice** folderu, uruchom następujące polecenie tooinstall hello hello **azure iot urządzenia** pakiet SDK urządzenia i **azure-iot urządzenie mqtt**pakietu:
   
    ```
    npm install azure-iot-device azure-iot-device-mqtt --save
    ```
3. Za pomocą edytora tekstu, Utwórz **dmpatterns_getstarted_device.js** pliku w hello **manageddevice** folderu.
4. Dodaj następujące hello "Wymagaj" instrukcje na początku hello hello **dmpatterns_getstarted_device.js** pliku:
   
    ```
    'use strict';
   
    var Client = require('azure-iot-device').Client;
    var Protocol = require('azure-iot-device-mqtt').Mqtt;
    ```
5. Dodaj **connectionString** zmiennej i korzystać z niego toocreate **klienta** wystąpienia.  Zastąp ciąg połączenia hello parametrów połączenia urządzenia.  
   
    ```
    var connectionString = 'HostName={youriothostname};DeviceId=myDeviceId;SharedAccessKey={yourdevicekey}';
    var client = Client.fromConnectionString(connectionString, Protocol);
    ```
6. Dodaj następujące metoda bezpośrednia hello tooimplement funkcji na urządzeniu hello hello
   
    ```
    var onReboot = function(request, response) {
   
        // Respond hello cloud app for hello direct method
        response.send(200, 'Reboot started', function(err) {
            if (!err) {
                console.error('An error occured when sending a method response:\n' + err.toString());
            } else {
                console.log('Response toomethod \'' + request.methodName + '\' sent successfully.');
            }
        });
   
        // Report hello reboot before hello physical restart
        var date = new Date();
        var patch = {
            iothubDM : {
                reboot : {
                    lastReboot : date.toISOString(),
                }
            }
        };
   
        // Get device Twin
        client.getTwin(function(err, twin) {
            if (err) {
                console.error('could not get twin');
            } else {
                console.log('twin acquired');
                twin.properties.reported.update(patch, function(err) {
                    if (err) throw err;
                    console.log('Device reboot twin state reported')
                });  
            }
        });
   
        // Add your device's reboot API for physical restart.
        console.log('Rebooting!');
    };
    ```
7. Otwórz Centrum IoT tooyour połączenia hello i uruchomić odbiornik metoda bezpośrednia hello:
   
    ```
    client.open(function(err) {
        if (err) {
            console.error('Could not open IotHub client');
        }  else {
            console.log('Client opened.  Waiting for reboot method.');
            client.onDeviceMethod('reboot', onReboot);
        }
    });
    ```
8. Zapisz i zamknij hello **dmpatterns_getstarted_device.js** pliku.

> [!NOTE]
> rzeczy tookeep proste, w tym samouczku nie implementuje wszystkie zasady ponawiania. W kodzie produkcyjnym, należy zaimplementować zasady ponawiania (na przykład wykładniczego wycofywania), zgodnie z sugestią podaną w artykuł w witrynie MSDN hello [obsługi błędów przejściowych][lnk-transient-faults].

## <a name="trigger-a-remote-reboot-on-hello-device-using-a-direct-method"></a>Wyzwalacz zdalnego ponownego uruchomienia na urządzeniu hello za pomocą bezpośrednich — metoda
W tej sekcji utworzysz aplikację konsoli Node.js, która inicjuje zdalnego ponownego uruchomienia na urządzeniu przy użyciu metody bezpośredniego. Aplikacja Hello używa urządzenia dwie zapytania toodiscover hello ostatniego ponownego uruchomienia dla tego urządzenia.

1. Utwórz pusty folder o nazwie **triggerrebootondevice**.  W hello **triggerrebootondevice** folderu, Utwórz plik package.json za pomocą hello następujące polecenie z wiersza polecenia.  Zaakceptuj wszystkie domyślne hello:
   
    ```
    npm init
    ```
2. Z wiersza polecenia w hello **triggerrebootondevice** folderu, uruchom następujące polecenie tooinstall hello hello **Centrum iothub azure** pakiet SDK urządzenia i **azure-iot urządzenie mqtt** pakietu:
   
    ```
    npm install azure-iothub --save
    ```
3. Za pomocą edytora tekstu, Utwórz **dmpatterns_getstarted_service.js** pliku w hello **triggerrebootondevice** folderu.
4. Dodaj następujące hello "Wymagaj" instrukcje na początku hello hello **dmpatterns_getstarted_service.js** pliku:
   
    ```
    'use strict';
   
    var Registry = require('azure-iothub').Registry;
    var Client = require('azure-iothub').Client;
    ```
5. Dodaj następujące deklaracje zmiennej hello i zastąp symbole zastępcze hello:
   
    ```
    var connectionString = '{iothubconnectionstring}';
    var registry = Registry.fromConnectionString(connectionString);
    var client = Client.fromConnectionString(connectionString);
    var deviceToReboot = 'myDeviceId';
    ```
6. Dodaj powitania po funkcja tooinvoke hello urządzenia metody tooreboot hello docelowe urządzenie:
   
    ```
    var startRebootDevice = function(twin) {
   
        var methodName = "reboot";
   
        var methodParams = {
            methodName: methodName,
            payload: null,
            timeoutInSeconds: 30
        };
   
        client.invokeDeviceMethod(deviceToReboot, methodParams, function(err, result) {
            if (err) { 
                console.error("Direct method error: "+err.message);
            } else {
                console.log("Successfully invoked hello device tooreboot.");  
            }
        });
    };
    ```
7. Dodaj następujący hello funkcji tooquery hello urządzenia i pobrać powitania od czasu ostatniego ponownego uruchomienia:
   
    ```
    var queryTwinLastReboot = function() {
   
        registry.getTwin(deviceToReboot, function(err, twin){
   
            if (twin.properties.reported.iothubDM != null)
            {
                if (err) {
                    console.error('Could not query twins: ' + err.constructor.name + ': ' + err.message);
                } else {
                    var lastRebootTime = twin.properties.reported.iothubDM.reboot.lastReboot;
                    console.log('Last reboot time: ' + JSON.stringify(lastRebootTime, null, 2));
                }
            } else 
                console.log('Waiting for device tooreport last reboot time.');
        });
    };
    ```
8. Dodaj następujące funkcje hello toocall kodu, które mogą powodować hello hello ponowny rozruch direct — metoda i zapytanie o hello ostatniego ponownego rozruchu czasu:
   
    ```
    startRebootDevice();
    setInterval(queryTwinLastReboot, 2000);
    ```
9. Zapisz i zamknij hello **dmpatterns_getstarted_service.js** pliku.

## <a name="run-hello-apps"></a>Uruchamianie aplikacji hello
Wszystko jest teraz gotowy toorun hello aplikacji.

1. W wierszu polecenia hello w hello **manageddevice** folderu Uruchom hello następujące polecenia toobegin nasłuchiwanie metoda bezpośrednia hello ponowny rozruch.
   
    ```
    node dmpatterns_getstarted_device.js
    ```
2. W wierszu polecenia hello w hello **triggerrebootondevice** folderu, uruchom następujące polecenie tootrigger hello zdalnego hello ponownie i zapytania dla hello urządzenia dwie toofind hello ostatniego ponownego rozruchu czasu.
   
    ```
    node dmpatterns_getstarted_service.js
    ```
3. Zostanie wyświetlony hello urządzenia odpowiedzi toohello metoda bezpośrednia hello konsoli.

[!INCLUDE [iot-hub-dm-followup](../../includes/iot-hub-dm-followup.md)]

<!-- images and links -->
[img-output]: media/iot-hub-get-started-with-dm/image6.png
[img-dm-ui]: media/iot-hub-get-started-with-dm/dmui.png

[lnk-dev-setup]: https://github.com/Azure/azure-iot-sdk-node/tree/master/doc/node-devbox-setup.md

[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[Azure portal]: https://portal.azure.com/
[Using resource groups toomanage your Azure resources]: ../azure-portal/resource-group-portal.md
[lnk-dm-github]: https://github.com/Azure/azure-iot-device-management

[lnk-devtwin]: iot-hub-devguide-device-twins.md
[lnk-c2dmethod]: iot-hub-devguide-direct-methods.md
[lnk-transient-faults]: https://msdn.microsoft.com/library/hh680901(v=pandp.50).aspx
