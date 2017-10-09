---
title: "aaaSimulate urządzenia Azure IoT krawędzi (Linux) | Dokumentacja firmy Microsoft"
description: "Jak toouse krawędzi IoT Azure w systemie Linux toocreate symulowane urządzenie wysyłają dane telemetryczne za pośrednictwem krawędzi IoT Centrum IoT tooan bramy."
services: iot-hub
documentationcenter: 
author: chipalost
manager: timlt
editor: 
ms.assetid: 11e7bf28-ee3d-48d6-a386-eb506c7a31cf
ms.service: iot-hub
ms.devlang: cpp
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/09/2017
ms.author: andbuc
ms.openlocfilehash: 168fb8eda8671d02c63073bdf36dfcd88b397fe2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-iot-edge-toosend-device-to-cloud-messages-with-a-simulated-device-linux"></a>Azure IoT krawędzi toosend urządzenia do chmury wiadomości za pomocą symulowane urządzenie (Linux)

[!INCLUDE [iot-hub-iot-edge-simulated-selector](../../includes/iot-hub-iot-edge-simulated-selector.md)]

[!INCLUDE [iot-hub-iot-edge-install-build-linux](../../includes/iot-hub-iot-edge-install-build-linux.md)]

## <a name="how-toorun-hello-sample"></a>Jak toorun hello próbki

Witaj **build.sh** skrypt generuje dane wyjściowe w hello **kompilacji** folderu w lokalnej kopii hello **krawędzi iot** repozytorium. Te dane wyjściowe obejmują hello czterech krawędzi IoT moduły używane w tym przykładzie.

Witaj miejsca skryptu kompilacji:

* **liblogger.so** w hello **kompilacji/moduły/rejestratora** folderu.
* **libiothub.so** w hello **kompilacji/moduły/Centrum iothub** folderu.
* **lib\_tożsamości\_map.so** w hello **kompilacji/moduły/identitymap** folderu.
* **libsimulated\_device.so** w hello **kompilacji/moduły/symulowane\_urządzenia** folderu.

Użyj tych ścieżek dla hello **ścieżka modułu** wartości, jak pokazano w hello następującego pliku ustawień JSON:

Symulowane Hello\_urządzenia\_chmury\_przekazać\_próbki proces trwa hello pliku konfiguracji JSON tooa ścieżkę jako argument wiersza polecenia. Hello następujący przykładowy plik JSON znajduje się w repozytorium SDK hello na **przykłady\\symulowane\_urządzenia\_chmury\_przekazać\_próbki\\src\\ Symulowane\_urządzenia\_chmury\_przekazać\_próbki\_lin.json**. Ta działa plik konfiguracji jest, chyba że zmodyfikujesz hello kompilacji skryptu tooplace hello krawędzi IoT modułów lub przykładowe pliki wykonywalne w lokalizacji innej niż domyślna.

> [!NOTE]
> ścieżki modułu Hello są względną toohello katalogu, z którego jest uruchamiany hello symulowane\_urządzenia\_chmury\_przekazać\_przykładowy plik wykonywalny, nie hello katalog w którym znajduje się plik wykonywalny hello. Witaj przykładowy plik konfiguracyjny JSON domyślne toowriting too'deviceCloudUploadGatewaylog.log "w bieżącym katalogu roboczym.

W edytorze tekstów otwórz plik hello **przykłady/symulowane\_urządzenia\_chmury\_przekazać\_próbki/src/symulowane\_urządzenia\_chmury\_przekazać\_lin.json** w lokalnej kopii hello **krawędzi iot** repozytorium. Ten plik konfiguruje hello krawędzi IoT modułów w hello próbki bramy:

* Witaj **Centrum IoTHub** modułu łączy tooyour Centrum IoT. Możesz ją skonfigurować Centrum IoT tooyour danych toosend. W szczególności zestaw hello **IoTHubName** wartość toohello nazwę Centrum IoT i ustaw hello **IoTHubSuffix** wartość zbyt**azure devices.net**. Zestaw hello **transportu** tooone wartości z: **HTTP**, **AMQP**, lub **MQTT**. Obecnie tylko **HTTP** udostępnia jedno połączenie TCP dla wszystkich wiadomości urządzenia. Jeśli ustawisz wartość hello zbyt**AMQP**, lub **MQTT**, hello bramy przechowuje oddzielnych TCP połączenia tooIoT Centrum dla każdego urządzenia.
* Witaj **mapowania** modułu mapuje adresy MAC hello Twoje nazwy urządzenia IoT Hub tooyour symulowanego urządzenia. Upewnij się, że **deviceId** identyfikatory hello dopasowania wartości hello dwa urządzenia dodane tooyour Centrum IoT i że hello **deviceKey** wartości zawiera klucze Witaj dwie urządzeń.
* Witaj **BLE1** i **BLE2** moduły są urządzeniami hello symulowane. Należy zwrócić uwagę, jak ich MAC dotyczy dopasowania hello adresy hello **mapowania** modułu.
* Witaj **rejestratora** modułu rejestruje pliku tooa działania bramy.
* Witaj **ścieżka modułu** wartości pokazano w przykładzie hello założono Uruchom przykładowe hello z hello **kompilacji** folderu w lokalnej kopii hello **krawędzi iot** repozytorium.
* Witaj **łącza** tablicy u dołu hello pliku JSON hello łączy hello **BLE1** i **BLE2** toohello modułów **mapowania** modułu i hello **mapowania** toohello modułu **Centrum IoTHub** modułu. Gwarantuje również, że wszystkie komunikaty są rejestrowane przez hello **rejestratora** modułu.

```json
{
    "modules": [
        {
            "name": "IotHub",
          "loader": {
            "name": "native",
            "entrypoint": {
              "module.path": "./modules/iothub/libiothub.so"
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
              "module.path": "./modules/identitymap/libidentity_map.so"
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
              "module.path": "./modules/simulated_device/libsimulated_device.so"
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
              "module.path": "./modules/simulated_device/libsimulated_device.so"
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
              "module.path": "./modules/logger/liblogger.so"
            }
            },
            "args": {
              "filename": "deviceCloudUploadGatewaylog.log"
            }
          }
    ],
    "links": [
        {
            "source": "*",
            "sink": "Logger"
        },
        {
            "source": "BLE1",
            "sink": "mapping"
        },
        {
            "source": "BLE2",
            "sink": "mapping"
        },
        {
            "source": "mapping",
            "sink": "IotHub"
        }
    ]
}
```

Zapisz zmiany hello wprowadzone toohello pliku konfiguracji.

przykład Witaj toorun:

1. W powłoki, przejdź toohello **iot krawędzi/kompilacji** folderu.
2. Uruchom następujące polecenie hello:
   
    ```sh
    ./samples/simulated_device_cloud_upload/simulated_device_cloud_upload_sample ../samples/simulated_device_cloud_upload/src/simulated_device_cloud_upload_lin.json
    ```
3. Można użyć hello [explorer urządzenia] [ lnk-device-explorer] lub [explorer Centrum iothub] [ lnk-iothub-explorer] narzędzia wiadomości powitania toomonitor otrzymywanych z hello Centrum IoT brama. Na przykład za pomocą Eksploratora Centrum iothub można monitorować za pomocą następującego polecenia hello wiadomości urządzenia do chmury:

    ```sh
    iothub-explorer monitor-events --login "HostName={Your iot hub name}.azure-devices.net;SharedAccessKeyName=iothubowner;SharedAccessKey={Your IoT Hub key}"
    ```

## <a name="next-steps"></a>Następne kroki

toogain dużo większą wiedzę Azure IoT Edge i doświadczenia z kilka przykładów kodu, odwiedź stronę hello następujące samouczki deweloperów i zasoby:

* [Wysyłać urządzenia do chmury z fizycznego urządzenia z krawędzią IoT Azure][lnk-physical-device]
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
