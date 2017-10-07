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
# <a name="connect-your-device-toohello-remote-monitoring-preconfigured-solution-nodejs"></a><span data-ttu-id="946ad-103">Połącz z toohello urządzenie zdalne monitorowanie wstępnie skonfigurowane rozwiązanie (Node.js)</span><span class="sxs-lookup"><span data-stu-id="946ad-103">Connect your device toohello remote monitoring preconfigured solution (Node.js)</span></span>
[!INCLUDE [iot-suite-selector-connecting](../../includes/iot-suite-selector-connecting.md)]

## <a name="create-a-nodejs-sample-solution"></a><span data-ttu-id="946ad-104">Tworzenie rozwiązania próbki node.js</span><span class="sxs-lookup"><span data-stu-id="946ad-104">Create a node.js sample solution</span></span>

<span data-ttu-id="946ad-105">Upewnij się, tej wersji środowiska Node.js 0.11.5 lub nowszy jest zainstalowany na komputerze deweloperskim.</span><span class="sxs-lookup"><span data-stu-id="946ad-105">Ensure that Node.js version 0.11.5 or later is installed on your development machine.</span></span> <span data-ttu-id="946ad-106">Można uruchomić `node --version` w wersji hello toocheck hello w wierszu polecenia.</span><span class="sxs-lookup"><span data-stu-id="946ad-106">You can run `node --version` at hello command line toocheck hello version.</span></span>

1. <span data-ttu-id="946ad-107">Utwórz folder o nazwie **RemoteMonitoring** na komputerze deweloperskim.</span><span class="sxs-lookup"><span data-stu-id="946ad-107">Create a folder called **RemoteMonitoring** on your development machine.</span></span> <span data-ttu-id="946ad-108">Przejdź toothis folderu w środowisku wiersza polecenia.</span><span class="sxs-lookup"><span data-stu-id="946ad-108">Navigate toothis folder in your command-line environment.</span></span>

1. <span data-ttu-id="946ad-109">Witaj uruchom następujące polecenia toodownload i zainstaluj pakiety hello należy toocomplete hello przykładową aplikację:</span><span class="sxs-lookup"><span data-stu-id="946ad-109">Run hello following commands toodownload and install hello packages you need toocomplete hello sample app:</span></span>

    ```
    npm init
    npm install azure-iot-device azure-iot-device-mqtt --save
    ```

1. <span data-ttu-id="946ad-110">W hello **RemoteMonitoring** folderu, Utwórz plik o nazwie **remote_monitoring.js**.</span><span class="sxs-lookup"><span data-stu-id="946ad-110">In hello **RemoteMonitoring** folder, create a file called **remote_monitoring.js**.</span></span> <span data-ttu-id="946ad-111">Otwórz ten plik w edytorze tekstu.</span><span class="sxs-lookup"><span data-stu-id="946ad-111">Open this file in a text editor.</span></span>

1. <span data-ttu-id="946ad-112">W hello **remote_monitoring.js** plików, Dodaj następujące hello `require` instrukcji:</span><span class="sxs-lookup"><span data-stu-id="946ad-112">In hello **remote_monitoring.js** file, add hello following `require` statements:</span></span>

    ```nodejs
    'use strict';

    var Protocol = require('azure-iot-device-mqtt').Mqtt;
    var Client = require('azure-iot-device').Client;
    var ConnectionString = require('azure-iot-device').ConnectionString;
    var Message = require('azure-iot-device').Message;
    ```

1. <span data-ttu-id="946ad-113">Dodaj następujące deklaracje zmiennej po hello hello `require` instrukcje.</span><span class="sxs-lookup"><span data-stu-id="946ad-113">Add hello following variable declarations after hello `require` statements.</span></span> <span data-ttu-id="946ad-114">Zastąp symbole zastępcze hello [identyfikator urządzenia] i [klucz urządzenia] wartościami zauważyć urządzenia zdalnego rozwiązanie monitorowania powitania w pulpicie nawigacyjnym.</span><span class="sxs-lookup"><span data-stu-id="946ad-114">Replace hello placeholder values [Device Id] and [Device Key] with values you noted for your device in hello remote monitoring solution dashboard.</span></span> <span data-ttu-id="946ad-115">Użyj hello nazwy hosta Centrum IoT z tooreplace pulpitu nawigacyjnego rozwiązania hello [Centrum IoTHub Name].</span><span class="sxs-lookup"><span data-stu-id="946ad-115">Use hello IoT Hub Hostname from hello solution dashboard tooreplace [IoTHub Name].</span></span> <span data-ttu-id="946ad-116">Jeśli na przykład host usługi IoT Hub ma nazwę **contoso.azure-devices.net**, zastąp wartość zastępczą [Nazwa usługi IoTHub] ciągiem **contoso**:</span><span class="sxs-lookup"><span data-stu-id="946ad-116">For example, if your IoT Hub Hostname is **contoso.azure-devices.net**, replace [IoTHub Name] with **contoso**:</span></span>

    ```nodejs
    var connectionString = 'HostName=[IoTHub Name].azure-devices.net;DeviceId=[Device Id];SharedAccessKey=[Device Key]';
    var deviceId = ConnectionString.parse(connectionString).DeviceId;
    ```

1. <span data-ttu-id="946ad-117">Dodaj następujące zmienne toodefine hello niektóre dane telemetryczne podstawowej:</span><span class="sxs-lookup"><span data-stu-id="946ad-117">Add hello following variables toodefine some base telemetry data:</span></span>

    ```nodejs
    var temperature = 50;
    var humidity = 50;
    var externalTemperature = 55;
    ```

1. <span data-ttu-id="946ad-118">Dodaj następujące wyniki operacji tooprint funkcji pomocnika hello:</span><span class="sxs-lookup"><span data-stu-id="946ad-118">Add hello following helper function tooprint operation results:</span></span>

    ```nodejs
    function printErrorFor(op) {
        return function printError(err) {
            if (err) console.log(op + ' error: ' + err.toString());
        };
    }
    ```

1. <span data-ttu-id="946ad-119">Dodaj powitania po pomocnika funkcja toouse toorandomize hello telemetrii wartości:</span><span class="sxs-lookup"><span data-stu-id="946ad-119">Add hello following helper function toouse toorandomize hello telemetry values:</span></span>

    ```nodejs
    function generateRandomIncrement() {
        return ((Math.random() * 2) - 1);
    }
    ```

1. <span data-ttu-id="946ad-120">Dodaj powitania po definicji hello **DeviceInfo** obiektu hello urządzenie wysyła podczas uruchamiania:</span><span class="sxs-lookup"><span data-stu-id="946ad-120">Add hello following definition for hello **DeviceInfo** object hello device sends on startup:</span></span>

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

1. <span data-ttu-id="946ad-121">Dodaj następujące hello definicji Witaj dwie urządzenia zgłoszone wartości.</span><span class="sxs-lookup"><span data-stu-id="946ad-121">Add hello following definition for hello device twin reported values.</span></span> <span data-ttu-id="946ad-122">Ta definicja zawiera opisy metod bezpośredniego hello hello urządzeń obsługiwanych przez:</span><span class="sxs-lookup"><span data-stu-id="946ad-122">This definition includes descriptions of hello direct methods hello device supports:</span></span>

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

1. <span data-ttu-id="946ad-123">Dodaj powitania po hello toohandle funkcja **ponowny rozruch** bezpośrednie wywołanie metody:</span><span class="sxs-lookup"><span data-stu-id="946ad-123">Add hello following function toohandle hello **Reboot** direct method call:</span></span>

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

1. <span data-ttu-id="946ad-124">Dodaj powitania po hello toohandle funkcja **InitiateFirmwareUpdate** bezpośrednie wywołania metody.</span><span class="sxs-lookup"><span data-stu-id="946ad-124">Add hello following function toohandle hello **InitiateFirmwareUpdate** direct method call.</span></span> <span data-ttu-id="946ad-125">Ta metoda bezpośredniego używa parametru lokalizacji hello toospecify toodownload obrazu oprogramowania układowego hello i inicjuje hello aktualizacji oprogramowania układowego na urządzeniu hello asynchronicznie:</span><span class="sxs-lookup"><span data-stu-id="946ad-125">This direct method uses a parameter toospecify hello location of hello firmware image toodownload, and initiates hello firmware update on hello device asynchronously:</span></span>

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

1. <span data-ttu-id="946ad-126">Dodaj hello następującego kodu toocreate wystąpienie klienta:</span><span class="sxs-lookup"><span data-stu-id="946ad-126">Add hello following code toocreate a client instance:</span></span>

    ```nodejs
    var client = Client.fromConnectionString(connectionString, Protocol);
    ```

1. <span data-ttu-id="946ad-127">Dodaj hello następującego kodu:</span><span class="sxs-lookup"><span data-stu-id="946ad-127">Add hello following code to:</span></span>

    * <span data-ttu-id="946ad-128">Otwórz hello połączenia.</span><span class="sxs-lookup"><span data-stu-id="946ad-128">Open hello connection.</span></span>
    * <span data-ttu-id="946ad-129">Wyślij hello **DeviceInfo** obiektu.</span><span class="sxs-lookup"><span data-stu-id="946ad-129">Send hello **DeviceInfo** object.</span></span>
    * <span data-ttu-id="946ad-130">Konfigurowanie obsługi dla żądanej właściwości.</span><span class="sxs-lookup"><span data-stu-id="946ad-130">Set up a handler for desired properties.</span></span>
    * <span data-ttu-id="946ad-131">Wysłać zgłoszonego właściwości.</span><span class="sxs-lookup"><span data-stu-id="946ad-131">Send reported properties.</span></span>
    * <span data-ttu-id="946ad-132">Rejestrowanie procedur obsługi dla metod bezpośredniego hello.</span><span class="sxs-lookup"><span data-stu-id="946ad-132">Register handlers for hello direct methods.</span></span>
    * <span data-ttu-id="946ad-133">Rozpocznij wysyłanie danych telemetrycznych.</span><span class="sxs-lookup"><span data-stu-id="946ad-133">Start sending telemetry.</span></span>

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

1. <span data-ttu-id="946ad-134">Zapisz hello zmiany toohello **remote_monitoring.js** pliku.</span><span class="sxs-lookup"><span data-stu-id="946ad-134">Save hello changes toohello **remote_monitoring.js** file.</span></span>

1. <span data-ttu-id="946ad-135">Uruchom następujące polecenie w wierszu polecenia toolaunch hello przykładowej aplikacji hello:</span><span class="sxs-lookup"><span data-stu-id="946ad-135">Run hello following command at a command prompt toolaunch hello sample application:</span></span>
   
    ```
    node remote_monitoring.js
    ```

[!INCLUDE [iot-suite-visualize-connecting](../../includes/iot-suite-visualize-connecting.md)]

[lnk-github-repo]: https://github.com/azure/azure-iot-sdk-node
[lnk-github-prepare]: https://github.com/Azure/azure-iot-sdk-node/blob/master/doc/node-devbox-setup.md
