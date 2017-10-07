---
title: "aaaConnect urządzenia przy użyciu środowiska Node.js | Dokumentacja firmy Microsoft"
description: "W tym artykule opisano, jak tooconnect toohello urządzenia pakiet IoT Azure wstępnie zdalnego rozwiązanie monitorowania przy użyciu aplikacji napisanych w Node.js."
services: 
suite: iot-suite
documentationcenter: na
author: dominicbetts
manager: timlt
editor: 
ms.assetid: fc50a33f-9fb9-42d7-b1b8-eb5cff19335e
ms.service: iot-suite
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/24/2017
ms.author: dobett
ms.openlocfilehash: 80bf2b70f15f539bfce4f135d533c46dd2b3f5a7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="connect-your-device-toohello-remote-monitoring-preconfigured-solution-nodejs"></a>Połącz z toohello urządzenie zdalne monitorowanie wstępnie skonfigurowane rozwiązanie (Node.js)
[!INCLUDE [iot-suite-selector-connecting](../../includes/iot-suite-selector-connecting.md)]

## <a name="create-a-nodejs-sample-solution"></a>Tworzenie rozwiązania próbki node.js

Upewnij się, tej wersji środowiska Node.js 0.11.5 lub nowszy jest zainstalowany na komputerze deweloperskim. Można uruchomić `node --version` w wersji hello toocheck hello w wierszu polecenia.

1. Utwórz folder o nazwie **RemoteMonitoring** na komputerze deweloperskim. Przejdź toothis folderu w środowisku wiersza polecenia.

1. Witaj uruchom następujące polecenia toodownload i zainstaluj pakiety hello należy toocomplete hello przykładową aplikację:

    ```
    npm init
    npm install azure-iot-device azure-iot-device-mqtt --save
    ```

1. W hello **RemoteMonitoring** folderu, Utwórz plik o nazwie **remote_monitoring.js**. Otwórz ten plik w edytorze tekstu.

1. W hello **remote_monitoring.js** plików, Dodaj następujące hello `require` instrukcji:

    ```nodejs
    'use strict';

    var Protocol = require('azure-iot-device-mqtt').Mqtt;
    var Client = require('azure-iot-device').Client;
    var ConnectionString = require('azure-iot-device').ConnectionString;
    var Message = require('azure-iot-device').Message;
    ```

1. Dodaj następujące deklaracje zmiennej po hello hello `require` instrukcje. Zastąp symbole zastępcze hello [identyfikator urządzenia] i [klucz urządzenia] wartościami zauważyć urządzenia zdalnego rozwiązanie monitorowania powitania w pulpicie nawigacyjnym. Użyj hello nazwy hosta Centrum IoT z tooreplace pulpitu nawigacyjnego rozwiązania hello [Centrum IoTHub Name]. Jeśli na przykład host usługi IoT Hub ma nazwę **contoso.azure-devices.net**, zastąp wartość zastępczą [Nazwa usługi IoTHub] ciągiem **contoso**:

    ```nodejs
    var connectionString = 'HostName=[IoTHub Name].azure-devices.net;DeviceId=[Device Id];SharedAccessKey=[Device Key]';
    var deviceId = ConnectionString.parse(connectionString).DeviceId;
    ```

1. Dodaj następujące zmienne toodefine hello niektóre dane telemetryczne podstawowej:

    ```nodejs
    var temperature = 50;
    var humidity = 50;
    var externalTemperature = 55;
    ```

1. Dodaj następujące wyniki operacji tooprint funkcji pomocnika hello:

    ```nodejs
    function printErrorFor(op) {
        return function printError(err) {
            if (err) console.log(op + ' error: ' + err.toString());
        };
    }
    ```

1. Dodaj powitania po pomocnika funkcja toouse toorandomize hello telemetrii wartości:

    ```nodejs
    function generateRandomIncrement() {
        return ((Math.random() * 2) - 1);
    }
    ```

1. Dodaj powitania po definicji hello **DeviceInfo** obiektu hello urządzenie wysyła podczas uruchamiania:

    ```nodejs
    var deviceMetaData = {
        'ObjectType': 'DeviceInfo',
        'IsSimulatedDevice': 0,
        'Version': '1.0',
        'DeviceProperties': {
            'DeviceID': deviceId,
            'HubEnabledState': 1
        }
    };
    ```

1. Dodaj następujące hello definicji Witaj dwie urządzenia zgłoszone wartości. Ta definicja zawiera opisy metod bezpośredniego hello hello urządzeń obsługiwanych przez:

    ```nodejs
    var reportedProperties = {
        "Device": {
            "DeviceState": "normal",
            "Location": {
                "Latitude": 47.642877,
                "Longitude": -122.125497
            }
        },
        "Config": {
            "TemperatureMeanValue": 56.7,
            "TelemetryInterval": 45
        },
        "System": {
            "Manufacturer": "Contoso Inc.",
            "FirmwareVersion": "2.22",
            "InstalledRAM": "8 MB",
            "ModelNumber": "DB-14",
            "Platform": "Plat 9.75",
            "Processor": "i3-9",
            "SerialNumber": "SER99"
        },
        "Location": {
            "Latitude": 47.642877,
            "Longitude": -122.125497
        },
        "SupportedMethods": {
            "Reboot": "Reboot hello device",
            "InitiateFirmwareUpdate--FwPackageURI-string": "Updates device Firmware. Use parameter FwPackageURI toospecifiy hello URI of hello firmware file"
        },
    }
    ```

1. Dodaj powitania po hello toohandle funkcja **ponowny rozruch** bezpośrednie wywołanie metody:

    ```nodejs
    function onReboot(request, response) {
        // Implement actual logic here.
        console.log('Simulated reboot...');

        // Complete hello response
        response.send(200, "Rebooting device", function(err) {
            if(!!err) {
                console.error('An error occurred when sending a method response:\n' + err.toString());
            } else {
                console.log('Response toomethod \'' + request.methodName + '\' sent successfully.' );
            }
        });
    }
    ```

1. Dodaj powitania po hello toohandle funkcja **InitiateFirmwareUpdate** bezpośrednie wywołania metody. Ta metoda bezpośredniego używa parametru lokalizacji hello toospecify toodownload obrazu oprogramowania układowego hello i inicjuje hello aktualizacji oprogramowania układowego na urządzeniu hello asynchronicznie:

    ```nodejs
    function onInitiateFirmwareUpdate(request, response) {
        console.log('Simulated firmware update initiated, using: ' + request.payload.FwPackageURI);

        // Complete hello response
        response.send(200, "Firmware update initiated", function(err) {
            if(!!err) {
                console.error('An error occurred when sending a method response:\n' + err.toString());
            } else {
                console.log('Response toomethod \'' + request.methodName + '\' sent successfully.' );
            }
        });

        // Add logic here tooperform hello firmware update asynchronously
    }
    ```

1. Dodaj hello następującego kodu toocreate wystąpienie klienta:

    ```nodejs
    var client = Client.fromConnectionString(connectionString, Protocol);
    ```

1. Dodaj hello następującego kodu:

    * Otwórz hello połączenia.
    * Wyślij hello **DeviceInfo** obiektu.
    * Konfigurowanie obsługi dla żądanej właściwości.
    * Wysłać zgłoszonego właściwości.
    * Rejestrowanie procedur obsługi dla metod bezpośredniego hello.
    * Rozpocznij wysyłanie danych telemetrycznych.

    ```nodejs
    client.open(function (err) {
        if (err) {
            printErrorFor('open')(err);
        } else {
            console.log('Sending device metadata:\n' + JSON.stringify(deviceMetaData));
            client.sendEvent(new Message(JSON.stringify(deviceMetaData)), printErrorFor('send metadata'));

            // Create device twin
            client.getTwin(function(err, twin) {
                if (err) {
                    console.error('Could not get device twin');
                } else {
                    console.log('Device twin created');

                    twin.on('properties.desired', function(delta) {
                        console.log('Received new desired properties:');
                        console.log(JSON.stringify(delta));
                    });

                    // Send reported properties
                    twin.properties.reported.update(reportedProperties, function(err) {
                        if (err) throw err;
                        console.log('twin state reported');
                    });

                    // Register handlers for direct methods
                    client.onDeviceMethod('Reboot', onReboot);
                    client.onDeviceMethod('InitiateFirmwareUpdate', onInitiateFirmwareUpdate);
                }
            });

            // Start sending telemetry
            var sendInterval = setInterval(function () {
                temperature += generateRandomIncrement();
                externalTemperature += generateRandomIncrement();
                humidity += generateRandomIncrement();

                var data = JSON.stringify({
                    'DeviceID': deviceId,
                    'Temperature': temperature,
                    'Humidity': humidity,
                    'ExternalTemperature': externalTemperature
                });

                console.log('Sending device event data:\n' + data);
                client.sendEvent(new Message(data), printErrorFor('send event'));
            }, 5000);

            client.on('error', function (err) {
                printErrorFor('client')(err);
                if (sendInterval) clearInterval(sendInterval);
                client.close(printErrorFor('client.close'));
            });
        }
    });
    ```

1. Zapisz hello zmiany toohello **remote_monitoring.js** pliku.

1. Uruchom następujące polecenie w wierszu polecenia toolaunch hello przykładowej aplikacji hello:
   
    ```
    node remote_monitoring.js
    ```

[!INCLUDE [iot-suite-visualize-connecting](../../includes/iot-suite-visualize-connecting.md)]

[lnk-github-repo]: https://github.com/azure/azure-iot-sdk-node
[lnk-github-prepare]: https://github.com/Azure/azure-iot-sdk-node/blob/master/doc/node-devbox-setup.md
