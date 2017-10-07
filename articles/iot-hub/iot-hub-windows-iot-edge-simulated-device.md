---
title: "aaaSimulate urządzenia Azure IoT krawędzi (system Windows) | Dokumentacja firmy Microsoft"
description: "Jak toouse Azure IoT Edge na toocreate Windows symulowane urządzenie wysyłają dane telemetryczne za pośrednictwem Centrum IoT Azure IoT krawędzi tooan bramy."
services: iot-hub
documentationcenter: 
author: chipalost
manager: timlt
editor: 
ms.assetid: 6a2aeda0-696a-4732-90e1-595d2e2fadc6
ms.service: iot-hub
ms.devlang: cpp
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/09/2017
ms.author: andbuc
ms.openlocfilehash: ddbe85eb956e9934e80e2e80e09f77b24cf54856
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-iot-edge-toosend-device-to-cloud-messages-with-a-simulated-device-windows"></a>Azure IoT krawędzi toosend urządzenia do chmury wiadomości za pomocą symulowane urządzenie (system Windows)

[!INCLUDE [iot-hub-iot-edge-simulated-selector](../../includes/iot-hub-iot-edge-simulated-selector.md)]

[!INCLUDE [iot-hub-iot-edge-install-build-windows](../../includes/iot-hub-iot-edge-install-build-windows.md)]

## <a name="how-toorun-hello-sample"></a>Jak toorun hello próbki

Witaj **build.cmd** skrypt generuje dane wyjściowe w hello **kompilacji** folderu w lokalnej kopii hello **krawędzi iot** repozytorium. Te dane wyjściowe obejmują hello czterech krawędzi IoT moduły używane w tym przykładzie.

Witaj miejsca skryptu kompilacji:

* **Logger.dll** w hello **kompilacji\\modułów\\rejestratora\\debugowania** folderu.
* **iothub.dll** w hello **kompilacji\\modułów\\Centrum iothub\\debugowania** folderu.
* **tożsamość\_map.dll** w hello **kompilacji\\modułów\\identitymap\\debugowania** folderu.
* **Symulowane\_device.dll** w hello **kompilacji\\modułów\\symulowane\_urządzenia\\debugowania** folderu.

Użyj tych ścieżek dla hello **ścieżka modułu** wartości, jak pokazano w hello następującego pliku ustawień JSON:

Symulowane Hello\_urządzenia\_chmury\_przekazać\_próbki proces trwa hello pliku konfiguracji JSON tooa ścieżkę jako argument wiersza polecenia. Hello następujący przykładowy plik JSON znajduje się w repozytorium SDK hello na **przykłady\\symulowane\_urządzenia\_chmury\_przekazać\_próbki\\src\\ Symulowane\_urządzenia\_chmury\_przekazać\_próbki\_win.json**. Ta działa plik konfiguracji jest, chyba że zmodyfikujesz hello kompilacji skryptu tooplace hello krawędzi IoT modułów lub przykładowe pliki wykonywalne w lokalizacji innej niż domyślna.

> [!NOTE]
> Witaj modułu ścieżki są względną toohello katalogu, gdzie symulowane hello\_urządzenia\_chmury\_przekazać\_znajduje się sample.exe. Witaj przykładowy plik konfiguracyjny JSON domyślne toowriting too'deviceCloudUploadGatewaylog.log "w bieżącym katalogu roboczym.

W edytorze tekstów otwórz plik hello **przykłady\\symulowane\_urządzenia\_chmury\_przekazać\_próbki\\src\\symulowane\_urządzenia \_chmury\_przekazać\_win.json** w lokalnej kopii hello **krawędzi iot** repozytorium. Ten plik konfiguruje hello krawędzi IoT modułów w hello próbki bramy:

* Witaj **Centrum IoTHub** modułu łączy tooyour Centrum IoT. Możesz ją skonfigurować Centrum IoT tooyour danych toosend. W szczególności zestaw hello **IoTHubName** wartość toohello nazwę Centrum IoT i ustaw hello **IoTHubSuffix** wartość zbyt**azure devices.net**. Zestaw hello **transportu** tooone wartości z: **HTTP**, **AMQP**, lub **MQTT**. Obecnie tylko **HTTP** udostępnia jedno połączenie TCP dla wszystkich wiadomości urządzenia. Jeśli ustawisz wartość hello zbyt**AMQP**, lub **MQTT**, hello bramy przechowuje oddzielnych TCP połączenia tooIoT Centrum dla każdego urządzenia.
* Witaj **mapowania** modułu mapuje adresy MAC hello Twoje nazwy urządzenia IoT Hub tooyour symulowanego urządzenia. Upewnij się, że **deviceId** identyfikatory hello dopasowania wartości hello dwa urządzenia dodane tooyour Centrum IoT i że hello **deviceKey** wartości zawiera klucze Witaj dwie urządzeń.
* Witaj **BLE1** i **BLE2** moduły są urządzeniami hello symulowane. Należy zwrócić uwagę, jak adresy MAC modułu hello zgodne adresy hello hello **mapowania** modułu.
* Witaj **rejestratora** modułu rejestruje pliku tooa działania bramy.
* Hello **ścieżka modułu** toohello względna katalogu gdzie symulowane hello są wartości widoczne w hello poniższy przykład\_urządzenia\_chmury\_przekazać\_znajduje się sample.exe.
* Witaj **łącza** tablicy u dołu hello pliku JSON hello łączy hello **BLE1** i **BLE2** toohello modułów **mapowania** modułu i hello **mapowania** toohello modułu **Centrum IoTHub** modułu. Gwarantuje również, że wszystkie komunikaty są rejestrowane przez hello **rejestratora** modułu.

```json
{
    "modules" :
    [
      {
        "name": "IotHub",
        "loader": {
          "name": "native",
          "entrypoint": {
            "module.path": "..\\..\\..\\modules\\iothub\\Debug\\iothub.dll"
          }
          },
          "args": {
            "IoTHubName": "<<insert here IoTHubName>>",
            "IoTHubSuffix": "<<insert here IoTHubSuffix>>",
            "Transport": "HTTP"
          }
        },
      {
        "name": "mapping",
        "loader": {
          "name": "native",
          "entrypoint": {
            "module.path": "..\\..\\..\\modules\\identitymap\\Debug\\identity_map.dll"
          }
          },
          "args": [
            {
              "macAddress": "01:01:01:01:01:01",
              "deviceId": "<<insert here deviceId>>",
              "deviceKey": "<<insert here deviceKey>>"
            },
            {
              "macAddress": "02:02:02:02:02:02",
              "deviceId": "<<insert here deviceId>>",
              "deviceKey": "<<insert here deviceKey>>"
            }
          ]
        },
      {
        "name": "BLE1",
        "loader": {
          "name": "native",
          "entrypoint": {
            "module.path": "..\\..\\..\\modules\\simulated_device\\Debug\\simulated_device.dll"
          }
          },
          "args": {
            "macAddress": "01:01:01:01:01:01"
          }
        },
      {
        "name": "BLE2",
        "loader": {
          "name": "native",
          "entrypoint": {
            "module.path": "..\\..\\..\\modules\\simulated_device\\Debug\\simulated_device.dll"
          }
          },
          "args": {
            "macAddress": "02:02:02:02:02:02"
          }
        },
      {
        "name": "Logger",
        "loader": {
          "name": "native",
          "entrypoint": {
            "module.path": "..\\..\\..\\modules\\logger\\Debug\\logger.dll"
          }
        },
        "args": {
          "filename": "deviceCloudUploadGatewaylog.log"
        }
      }
    ],
    "links" : [
        { "source" : "*", "sink" : "Logger" },
        { "source" : "BLE1", "sink" : "mapping" },
        { "source" : "BLE2", "sink" : "mapping" },
        { "source" : "mapping", "sink" : "IotHub" }
    ]
}
```

Zapisz zmiany hello wprowadzone toohello pliku konfiguracji.

przykład Witaj toorun:

1. W wierszu polecenia przejdź toohello **kompilacji** folderu w lokalnej kopii hello **krawędzi iot** repozytorium.
2. Uruchom następujące polecenie hello:
   
    ```cmd
    samples\simulated_device_cloud_upload\Debug\simulated_device_cloud_upload_sample.exe ..\samples\simulated_device_cloud_upload\src\simulated_device_cloud_upload_win.json
    ```
3. Można użyć hello [explorer urządzenia] [ lnk-device-explorer] lub [explorer Centrum iothub] [ lnk-iothub-explorer] narzędzia wiadomości powitania toomonitor otrzymywanych z hello Centrum IoT brama. Na przykład za pomocą Eksploratora Centrum iothub można monitorować za pomocą następującego polecenia hello wiadomości urządzenia do chmury:

    ```cmd
    iothub-explorer monitor-events --login "HostName={Your iot hub name}.azure-devices.net;SharedAccessKeyName=iothubowner;SharedAccessKey={Your IoT Hub key}"
    ```

## <a name="next-steps"></a>Następne kroki

toogain dużo większą wiedzę krawędzi IoT i doświadczenia z kilka przykładów kodu, odwiedź stronę hello następujące samouczki deweloperów i zasoby:

* [Wysyłanie wiadomości urządzenia do chmury z fizycznego urządzenia IoT krawędzi][lnk-physical-device]
* [Krawędź IoT Azure][lnk-iot-edge]

toofurther Poznaj możliwości hello Centrum IoT, zobacz:

* [Przewodnik dewelopera Centrum IoT][lnk-devguide]
* [Zabezpieczanie rozwiązania IoT z hello tła w][lnk-securing]

<!-- Links -->
[lnk-iot-edge]: https://github.com/Azure/iot-edge/
[lnk-physical-device]: iot-hub-iot-edge-physical-device.md
[lnk-devguide]: iot-hub-devguide.md
[lnk-securing]: iot-hub-security-ground-up.md
[lnk-device-explorer]: https://github.com/Azure/azure-iot-sdk-csharp/tree/master/tools/DeviceExplorer
[lnk-iothub-explorer]: https://github.com/Azure/iothub-explorer/blob/master/readme.md