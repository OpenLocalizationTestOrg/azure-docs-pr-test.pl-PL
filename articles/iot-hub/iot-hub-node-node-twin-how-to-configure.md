---
title: "właściwości dwie urządzenia Azure IoT Hub aaaUse (węzeł) | Dokumentacja firmy Microsoft"
description: "Jak urządzenia Azure IoT Hub toouse twins tooconfigure urządzeń. Używasz hello Azure IoT SDK dla środowiska Node.js tooimplement aplikacji symulowane urządzenie i aplikacji usługi, który modyfikuje konfigurację urządzenia przy użyciu podwójnego urządzenia."
services: iot-hub
documentationcenter: .net
author: fsautomata
manager: timlt
editor: 
ms.assetid: d0bcec50-26e6-40f0-8096-733b2f3071ec
ms.service: iot-hub
ms.devlang: node
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 09/13/2016
ms.author: elioda
ms.openlocfilehash: 7ebfe2dfa0876bf04fdbaceae55db76456523e8a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="use-desired-properties-tooconfigure-devices-node"></a>Żądany właściwości tooconfigure urządzeń (węzeł)
[!INCLUDE [iot-hub-selector-twin-how-to-configure](../../includes/iot-hub-selector-twin-how-to-configure.md)]

Na końcu hello tego samouczka masz dwie aplikacje konsoli Node.js:

* **SimulateDeviceConfiguration.js**, aplikację symulowane urządzenie, która oczekuje na aktualizację wymaganą konfiguracją i hello stanu procesu aktualizacji konfiguracji symulowane.
* **SetDesiredConfigurationAndQuery.js**, konfiguracja na urządzeniu żądanego aplikacji zaplecza Node.js, która ustawia hello i zapytań hello konfiguracji procesu aktualizacji.

> [!NOTE]
> Artykuł Hello [Azure IoT SDK] [ lnk-hub-sdks] informacje na temat hello Azure IoT SDK służy toobuild zarówno urządzenia, jak i zaplecza aplikacji.
> 
> 

toocomplete tego samouczka należy hello poniżej:

* Środowisko Node.js w wersji 0.10.x lub nowszej.
* Aktywne konto platformy Azure. (Jeśli go nie masz, możesz utworzyć [bezpłatne konto próbne][lnk-free-trial] w zaledwie kilka minut).

Po wykonaniu hello [Rozpoczynanie pracy z urządzenia twins] [ lnk-twin-tutorial] samouczek, masz już Centrum IoT i tożsamość urządzenia o nazwie **myDeviceId**; i można pominąć toohello [ Tworzenie aplikacji symulowane urządzenie hello] [ lnk-how-to-configure-createapp] sekcji.

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity](../../includes/iot-hub-get-started-create-device-identity.md)]

## <a name="create-hello-simulated-device-app"></a>Tworzenie aplikacji symulowane urządzenie hello
W tej sekcji zostanie utworzona aplikacja konsoli Node.js łączącego koncentratora tooyour **myDeviceId**, czeka na aktualizację wymaganą konfiguracją, a następnie przedstawia aktualizacje na proces aktualizacji konfiguracji hello symulowane.

1. Utwórz nowy, pusty folder o nazwie **simulatedeviceconfiguration**. W hello **simulatedeviceconfiguration** folderu, Utwórz nowy plik package.json przy użyciu hello następujące polecenie z wiersza polecenia. Zaakceptuj wszystkie domyślne hello:
   
    ```
    npm init
    ```
2. Z wiersza polecenia w hello **simulatedeviceconfiguration** folderu, uruchom następujące polecenie tooinstall hello hello **azure iot urządzenia**, i **azure-iot urządzenie mqtt**pakietu:
   
    ```
    npm install azure-iot-device azure-iot-device-mqtt --save
    ```
3. Za pomocą edytora tekstu, Utwórz nową **SimulateDeviceConfiguration.js** pliku w hello **simulatedeviceconfiguration** folderu.
4. Dodaj hello następującego kodu toohello **SimulateDeviceConfiguration.js** plików i Zastąp hello **{ciąg połączenia urządzenia}** symbol zastępczy parametrów połączenia urządzenia hello skopiowane podczas możesz utworzony hello **myDeviceId** tożsamości urządzenia:
   
        'use strict';
        var Client = require('azure-iot-device').Client;
        var Protocol = require('azure-iot-device-mqtt').Mqtt;
   
        var connectionString = '{device connection string}';
        var client = Client.fromConnectionString(connectionString, Protocol);
   
        client.open(function(err) {
            if (err) {
                console.error('could not open IotHub client');
            } else {
                client.getTwin(function(err, twin) {
                    if (err) {
                        console.error('could not get twin');
                    } else {
                        console.log('retrieved device twin');
                        twin.properties.reported.telemetryConfig = {
                            configId: "0",
                            sendFrequency: "24h"
                        }
                        twin.on('properties.desired', function(desiredChange) {
                            console.log("received change: "+JSON.stringify(desiredChange));
                            var currentTelemetryConfig = twin.properties.reported.telemetryConfig;
                            if (desiredChange.telemetryConfig &&desiredChange.telemetryConfig.configId !== currentTelemetryConfig.configId) {
                                initConfigChange(twin);
                            }
                        });
                    }
                });
            }
        });
   
    Witaj **klienta** obiekt udostępnia wszystkie hello metody wymagane toointeract z twins urządzenia z hello urządzenia. Witaj poprzedni kod po jego inicjuje hello **klienta** obiektu, pobiera Witaj dwie urządzenia dla **myDeviceId**i dołącza program obsługi aktualizacji hello żądanej właściwości. Program Hello obsługi sprawdza, który jest żądanie zmiany konfiguracji rzeczywiste porównując hello configIds, a następnie wywołuje metodę, która rozpoczyna się zmianę konfiguracji hello.
   
    Należy zwrócić uwagę, że dla zapewnienia hello prostotę, hello poprzedni kod używa domyślnego ustalony hello początkową konfigurację. Rzeczywiste aplikacji będzie prawdopodobnie załadować tej konfiguracji z magazynu lokalnego.
   
   > [!IMPORTANT]
   > Zdarzenia zmiany żądanej właściwości zawsze są emitowane raz na połączenie z urządzeniem, upewnij się, że istnieje rzeczywiste zmiany w hello toocheck żądanego właściwości przed wykonaniem jakiegokolwiek działania.
   > 
   > 
5. Dodaj następujące metody przed hello hello `client.open()` wywołania:
   
        var initConfigChange = function(twin) {
            var currentTelemetryConfig = twin.properties.reported.telemetryConfig;
            currentTelemetryConfig.pendingConfig = twin.properties.desired.telemetryConfig;
            currentTelemetryConfig.status = "Pending";
   
            var patch = {
            telemetryConfig: currentTelemetryConfig
            };
            twin.properties.reported.update(patch, function(err) {
                if (err) {
                    console.log('Could not report properties');
                } else {
                    console.log('Reported pending config change: ' + JSON.stringify(patch));
                    setTimeout(function() {completeConfigChange(twin);}, 60000);
                }
            });
        }
   
        var completeConfigChange =  function(twin) {
            var currentTelemetryConfig = twin.properties.reported.telemetryConfig;
            currentTelemetryConfig.configId = currentTelemetryConfig.pendingConfig.configId;
            currentTelemetryConfig.sendFrequency = currentTelemetryConfig.pendingConfig.sendFrequency;
            currentTelemetryConfig.status = "Success";
            delete currentTelemetryConfig.pendingConfig;
   
            var patch = {
                telemetryConfig: currentTelemetryConfig
            };
            patch.telemetryConfig.pendingConfig = null;
   
            twin.properties.reported.update(patch, function(err) {
                if (err) {
                    console.error('Error reporting properties: ' + err);
                } else {
                    console.log('Reported completed config change: ' + JSON.stringify(patch));
                }
            });
        };
   
    Hello **initConfigChange** metody aktualizacji zgłaszane właściwości dla obiektu dwie urządzenie lokalne powitania o żądanie aktualizacji konfiguracji hello i ustawia stan hello zbyt**oczekujące**, następnie aktualizacje hello urządzenia dwie na powitania usługi. Po pomyślnym zaktualizowaniu Witaj dwie urządzenia, jego symuluje długotrwała proces, który kończy w realizacji hello **completeConfigChange**. Tej metody aktualizacji hello urządzenia lokalnego dwie obiektu zgłosił właściwości ustawiania stanu hello zbyt**Powodzenie** i usuwanie hello **pendingConfig** obiektu. Aktualizuje Witaj dwie urządzenia w usłudze hello.
   
    Pamiętaj, że toosave przepustowości, zgłaszany właściwości są aktualizowane, określając modyfikować tylko toobe właściwości hello (o nazwie **poprawki** w hello powyżej kodu), zamiast zastępowanie hello całego dokumentu.
   
   > [!NOTE]
   > W tym samouczku nie zasymulować wszystkie zachowania aktualizacji konfiguracji współbieżnych. Niektóre procesy aktualizacji konfiguracji może być tooaccommodate stanie zmiany konfiguracji docelowej, podczas gdy aktualizacja hello jest uruchomiona, inne osoby mogą mieć tooqueue je, a inne można odrzucić warunek błędu. Upewnij się, że tooconsider hello zachowanie procesu określonej konfiguracji, a następnie dodaj odpowiednie logiki hello przed zainicjowaniem hello zmiana konfiguracji.
   > 
   > 
6. Uruchamianie aplikacji urządzenia hello:
   
        node SimulateDeviceConfiguration.js
   
    Powinna zostać wyświetlona wiadomość hello `retrieved device twin`. Zachowaj aplikacji hello uruchomiona.

## <a name="create-hello-service-app"></a>Tworzenie aplikacji usługi hello
W tej sekcji utworzysz aplikację konsoli Node.js hello tej aktualizacji *żądanego właściwości* na powitania dwie urządzeń skojarzonych z **myDeviceId** z obiektem konfiguracji telemetrii. Następnie zapytań przechowywane w Centrum IoT hello twins urządzenia hello i przedstawia hello różnica między hello potrzeby i zgłosił konfiguracje hello urządzenia.

1. Utwórz nowy, pusty folder o nazwie **setdesiredandqueryapp**. W hello **setdesiredandqueryapp** folderu, Utwórz nowy plik package.json przy użyciu hello następujące polecenie z wiersza polecenia. Zaakceptuj wszystkie domyślne hello:
   
    ```
    npm init
    ```
2. Z wiersza polecenia w hello **setdesiredandqueryapp** folderu, uruchom następujące polecenie tooinstall hello hello **Centrum iothub azure** pakietu:
   
    ```
    npm install azure-iothub node-uuid --save
    ```
3. Za pomocą edytora tekstu, Utwórz nową **SetDesiredAndQuery.js** pliku w hello **addtagsandqueryapp** folderu.
4. Dodaj hello następującego kodu toohello **SetDesiredAndQuery.js** plików i Zastąp hello **{parametry połączenia Centrum iot}** symbol zastępczy hello Centrum IoT parametry połączenia skopiowane podczas tworzenia Centrum :
   
        'use strict';
        var iothub = require('azure-iothub');
        var uuid = require('node-uuid');
        var connectionString = '{iot hub connection string}';
        var registry = iothub.Registry.fromConnectionString(connectionString);
   
        registry.getTwin('myDeviceId', function(err, twin){
            if (err) {
                console.error(err.constructor.name + ': ' + err.message);
            } else {
                var newConfigId = uuid.v4();
                var newFrequency = process.argv[2] || "5m";
                var patch = {
                    properties: {
                        desired: {
                            telemetryConfig: {
                                configId: newConfigId,
                                sendFrequency: newFrequency
                            }
                        }
                    }
                }
                twin.update(patch, function(err) {
                    if (err) {
                        console.error('Could not update twin: ' + err.constructor.name + ': ' + err.message);
                    } else {
                        console.log(twin.deviceId + ' twin updated successfully');
                    }
                });
                setInterval(queryTwins, 10000);
            }
        });

    Witaj **rejestru** obiekt udostępnia wszystkie hello metody wymagane toointeract z twins urządzenia z usługi hello. Witaj poprzedni kod po jego inicjuje hello **rejestru** obiektu, pobiera Witaj dwie urządzenia dla **myDeviceId**i aktualizuje jego właściwości żądany nowy obiekt konfiguracji telemetrii. Po wykonaniu tej wywołuje hello **queryTwins** funkcji zdarzeń 10 sekund.

    > [!IMPORTANT]
    > Ta aplikacja kwerendę Centrum IoT co 10 sekund w celach ilustracyjnych. Użyj zapytań toogenerate raporty dla użytkownika na wielu urządzeniach, a nie toodetect zmiany. Jeśli rozwiązanie wymaga powiadomień w czasie rzeczywistym zdarzeń urządzenia, należy użyć [dwie powiadomienia][lnk-twin-notifications].
    > 
    >.

1. Dodaj powitania po prawej kodu przed hello `registry.getDeviceTwin()` hello tooimplement wywołania **queryTwins** funkcji:
   
        var queryTwins = function() {
            var query = registry.createQuery("SELECT * FROM devices WHERE deviceId = 'myDeviceId'", 100);
            query.nextAsTwin(function(err, results) {
                if (err) {
                    console.error('Failed toofetch hello results: ' + err.message);
                } else {
                    console.log();
                    results.forEach(function(twin) {
                        var desiredConfig = twin.properties.desired.telemetryConfig;
                        var reportedConfig = twin.properties.reported.telemetryConfig;
                        console.log("Config report for: " + twin.deviceId);
                        console.log("Desired: ");
                        console.log(JSON.stringify(desiredConfig, null, 2));
                        console.log("Reported: ");
                        console.log(JSON.stringify(reportedConfig, null, 2));
                    });
                }
            });
        };
   
    Hello poprzednich zapytań kodu hello przechowywane w Centrum IoT hello twins urządzenia i hello odbitek potrzeby i konfiguracje dane telemetryczne zgłoszone. Zobacz toohello [język zapytań Centrum IoT] [ lnk-query] toolearn jak sformatowanego toogenerate raporty na Twoich urządzeniach.
2. Z **SimulateDeviceConfiguration.js** uruchomiona, uruchom aplikacji hello:
   
        node SetDesiredAndQuery.js 5m
   
    Powinny pojawić się zmiany w konfiguracji zgłoszone hello **Powodzenie** za**oczekujące** za**Powodzenie** ponownie za pomocą nowego aktywny hello wysyłać częstotliwość pięć minut zamiast 24 godziny.
   
   > [!IMPORTANT]
   > Istnieje opóźnienie zapasowej protokołu tooa między hello urządzenia raport operacji i hello wyniku zapytania. Jest to tooenable hello zapytania infrastruktury toowork na bardzo dużą skalę. Widoki spójne tooretrieve dwie pojedyncze urządzenie, użyj hello **getDeviceTwin** metoda hello **rejestru** klasy.
   > 
   > 

## <a name="next-steps"></a>Następne kroki
W tym samouczku, ustaw żądaną konfiguracją jako *żądanego właściwości* z poziomu aplikacji zaplecza i zapisano toodetect aplikacji symulowane urządzenie, zmienianie i symulować proces aktualizacji wieloetapowych raportowania stanu jako  *zgłoszone właściwości* toohello dwie urządzenia.

Hello Użyj następujących zasobów toolearn jak do:

* wysłać dane telemetryczne z urządzenia z hello [Rozpoczynanie pracy z Centrum IoT] [ lnk-iothub-getstarted] samouczka
* harmonogramu lub wykonania operacji na dużych zestawów urządzeń Zobacz hello [emisji zadania i harmonogramu] [ lnk-schedule-jobs] samouczka.
* sterować urządzenia interakcyjne (takich jak włączanie wentylator z aplikacji kontrolowane przez użytkownika), za pomocą hello [metody bezpośredniego] [ lnk-methods-tutorial] samouczka.

<!-- links -->
[lnk-hub-sdks]: iot-hub-devguide-sdks.md
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/

[lnk-devguide-jobs]: iot-hub-devguide-jobs.md
[lnk-query]: iot-hub-devguide-query-language.md
[lnk-twin-notifications]: iot-hub-devguide-device-twins.md#back-end-operations
[lnk-methods]: iot-hub-devguide-direct-methods.md
[lnk-dm-overview]: iot-hub-device-management-overview.md
[lnk-twin-tutorial]: iot-hub-node-node-twin-getstarted.md
[lnk-schedule-jobs]: iot-hub-node-node-schedule-jobs.md
[lnk-dev-setup]: https://github.com/Azure/azure-iot-sdk-node/blob/master/doc/node-devbox-setup.md
[lnk-connect-device]: https://azure.microsoft.com/develop/iot/
[lnk-device-management]: iot-hub-node-node-device-management-get-started.md
[lnk-iot-edge]: iot-hub-linux-iot-edge-get-started.md
[lnk-iothub-getstarted]: iot-hub-node-node-getstarted.md
[lnk-methods-tutorial]: iot-hub-node-node-direct-methods.md

[lnk-guid]: https://en.wikipedia.org/wiki/Globally_unique_identifier

[lnk-how-to-configure-createapp]: iot-hub-node-node-twin-how-to-configure.md#create-the-simulated-device-app
