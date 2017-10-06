---
title: "aaaGet wprowadzenie twins urządzenia Azure IoT Hub (węzeł) | Dokumentacja firmy Microsoft"
description: "Jak tooadd twins urządzenia Azure IoT Hub toouse tagów, a następnie użyj zapytania Centrum IoT. Możesz użyć hello Azure IoT SDK dla środowiska Node.js tooimplement hello symulowane urządzenie aplikacji i aplikacji usługi, który dodaje znaczniki hello i uruchamia hello zapytania Centrum IoT."
services: iot-hub
documentationcenter: node
author: fsautomata
manager: timlt
editor: 
ms.assetid: 314c88e4-cce1-441c-b75a-d2e08e39ae7d
ms.service: iot-hub
ms.devlang: node
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/25/2017
ms.author: elioda
ms.openlocfilehash: d60b8c3de85e9285e496b86e27d4ee31a0554a1e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-device-twins-node"></a>Rozpoczynanie pracy z urządzenia twins (węzeł)
[!INCLUDE [iot-hub-selector-twin-get-started](../../includes/iot-hub-selector-twin-get-started.md)]

Na końcu hello tego samouczka masz dwie aplikacje konsoli Node.js:

* **AddTagsAndQuery.js**, aplikacji zaplecza Node.js, która dodaje znaczniki i zapytanie twins urządzenia.
* **TwinSimulatedDevice.js**, aplikacji Node.js, która symuluje urządzenie łączące Centrum IoT tooyour o tożsamości urządzenia hello utworzony wcześniej, a następnie raportuje stanu łączności.

> [!NOTE]
> Artykuł Hello [Azure IoT SDK] [ lnk-hub-sdks] informacje na temat hello Azure IoT SDK służy toobuild zarówno urządzenia, jak i zaplecza aplikacji.
> 
> 

toocomplete tego samouczka należy hello poniżej:

* Środowisko Node.js w wersji 0.10.x lub nowszej.
* Aktywne konto platformy Azure. (Jeśli go nie masz, możesz utworzyć [bezpłatne konto próbne][lnk-free-trial] w zaledwie kilka minut).

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity](../../includes/iot-hub-get-started-create-device-identity.md)]

## <a name="create-hello-service-app"></a>Tworzenie aplikacji usługi hello
W tej sekcji zostanie utworzona aplikacja konsoli Node.js dodające skojarzone z lokalizacji metadanych toohello urządzenia dwie **myDeviceId**. Następnie zapytania twins urządzenia hello przechowywane w Centrum IoT hello Wybieranie hello urządzeń znajdujących się w hello nam, a następnie hello te, które są raportowania komórkowej połączenia.

1. Utwórz nowy, pusty folder o nazwie **addtagsandqueryapp**. W hello **addtagsandqueryapp** folderu, Utwórz nowy plik package.json przy użyciu hello następujące polecenie z wiersza polecenia. Zaakceptuj wszystkie domyślne hello:
   
    ```
    npm init
    ```
2. Z wiersza polecenia w hello **addtagsandqueryapp** folderu, uruchom następujące polecenie tooinstall hello hello **Centrum iothub azure** pakietu:
   
    ```
    npm install azure-iothub --save
    ```
3. Za pomocą edytora tekstu, Utwórz nową **AddTagsAndQuery.js** pliku w hello **addtagsandqueryapp** folderu.
4. Dodaj hello następującego kodu toohello **AddTagsAndQuery.js** plików i Zastąp hello **{parametry połączenia Centrum iot}** symbol zastępczy hello Centrum IoT parametry połączenia skopiowane podczas tworzenia Centrum:
   
        'use strict';
        var iothub = require('azure-iothub');
        var connectionString = '{iot hub connection string}';
        var registry = iothub.Registry.fromConnectionString(connectionString);
   
        registry.getTwin('myDeviceId', function(err, twin){
            if (err) {
                console.error(err.constructor.name + ': ' + err.message);
            } else {
                var patch = {
                    tags: {
                        location: {
                            region: 'US',
                            plant: 'Redmond43'
                      }
                    }
                };
   
                twin.update(patch, function(err) {
                  if (err) {
                    console.error('Could not update twin: ' + err.constructor.name + ': ' + err.message);
                  } else {
                    console.log(twin.deviceId + ' twin updated successfully');
                    queryTwins();
                  }
                });
            }
        });
   
    Witaj **rejestru** obiekt udostępnia wszystkie hello metody wymagane toointeract z twins urządzenia z usługi hello. Poprzedni kod Hello najpierw inicjuje hello **rejestru** obiektu, a następnie pobiera Witaj dwie urządzenia dla **myDeviceId**i na koniec aktualizuje jego tagi hello potrzeby informacji o lokalizacji.
   
    Po hello aktualizowanie hello znaczniki hello wywołania **queryTwins** funkcji.
5. Dodaj następujące kod na końcu hello hello **AddTagsAndQuery.js** tooimplement hello **queryTwins** funkcji:
   
        var queryTwins = function() {
            var query = registry.createQuery("SELECT * FROM devices WHERE tags.location.plant = 'Redmond43'", 100);
            query.nextAsTwin(function(err, results) {
                if (err) {
                    console.error('Failed toofetch hello results: ' + err.message);
                } else {
                    console.log("Devices in Redmond43: " + results.map(function(twin) {return twin.deviceId}).join(','));
                }
            });
   
            query = registry.createQuery("SELECT * FROM devices WHERE tags.location.plant = 'Redmond43' AND properties.reported.connectivity.type = 'cellular'", 100);
            query.nextAsTwin(function(err, results) {
                if (err) {
                    console.error('Failed toofetch hello results: ' + err.message);
                } else {
                    console.log("Devices in Redmond43 using cellular network: " + results.map(function(twin) {return twin.deviceId}).join(','));
                }
            });
        };
   
    Poprzedni kod Hello wykonuje dwa zapytania: hello najpierw wybiera tylko twins urządzenia hello urządzeń znajdujących się w hello **Redmond43** roślin i hello drugi refines hello zapytania tooselect tylko hello urządzeń podłączonych do sieci komórkowej.
   
    Należy pamiętać, że poprzedni kod hello, podczas tworzenia hello **zapytania** obiektów, określa maksymalną liczbę zwracanych dokumentów. Hello **zapytania** zawiera obiekt **hasMoreResults** właściwości typu boolean służy tooinvoke hello **nextAsTwin** metody wielokrotnie tooretrieve wszystkie wyniki. Wywołana metoda **dalej** jest dostępna dla wyników, które nie są urządzenia, na przykład twins wyniki zapytań agregacji.
6. Uruchamianie aplikacji hello:
   
        node AddTagsAndQuery.js
   
    Powinny pojawić się jedno urządzenie w wynikach hello hello zadać zapytania dla wszystkich urządzeń znajdujących się w **Redmond43** i Brak dla zapytania hello, która ogranicza hello powoduje toodevices używanego przez sieć komórkową.
   
    ![][1]

W następnej sekcji hello tworzenia aplikacji urządzenia, która raportuje informacje o łączności hello i zmiany hello wynik kwerendy hello w poprzedniej sekcji hello.

## <a name="create-hello-device-app"></a>Tworzenie hello urządzenia aplikacji
W tej sekcji zostanie utworzona aplikacja konsoli Node.js łączącego koncentratora tooyour **myDeviceId**, a następnie aktualizacje jego dwie urządzenia użytkownika zgłosiła właściwości toocontain hello informacje, że jest połączony za pomocą sieci komórkowej.

> [!NOTE]
> W tej chwili twins urządzenia są dostępne tylko z urządzeń łączących tooIoT Centrum przy użyciu protokołu MQTT hello. Zobacz toohello [Obsługa MQTT] [ lnk-devguide-mqtt] artykuł, aby uzyskać instrukcje dotyczące tooconvert istniejących urządzeń aplikacji toouse MQTT.
> 
> 

1. Utwórz nowy, pusty folder o nazwie **reportconnectivity**. W hello **reportconnectivity** folderu, Utwórz nowy plik package.json przy użyciu hello następujące polecenie z wiersza polecenia. Zaakceptuj wszystkie domyślne hello:
   
    ```
    npm init
    ```
2. Z wiersza polecenia w hello **reportconnectivity** folderu, uruchom następujące polecenie tooinstall hello hello **azure iot urządzenia**, i **azure-iot urządzenie mqtt** pakietu :
   
    ```
    npm install azure-iot-device azure-iot-device-mqtt --save
    ```
3. Za pomocą edytora tekstu, Utwórz nową **ReportConnectivity.js** pliku w hello **reportconnectivity** folderu.
4. Dodaj hello następującego kodu toohello **ReportConnectivity.js** plików i Zastąp hello **{ciąg połączenia urządzenia}** symbol zastępczy parametrów połączenia urządzenia hello skopiowane podczas tworzenia hello **myDeviceId** tożsamości urządzenia:
   
        'use strict';
        var Client = require('azure-iot-device').Client;
        var Protocol = require('azure-iot-device-mqtt').Mqtt;
   
        var connectionString = '{device connection string}';
        var client = Client.fromConnectionString(connectionString, Protocol);
   
        client.open(function(err) {
        if (err) {
            console.error('could not open IotHub client');
        }  else {
            console.log('client opened');
   
            client.getTwin(function(err, twin) {
            if (err) {
                console.error('could not get twin');
            } else {
                var patch = {
                    connectivity: {
                        type: 'cellular'
                    }
                };
   
                twin.properties.reported.update(patch, function(err) {
                    if (err) {
                        console.error('could not update twin');
                    } else {
                        console.log('twin state reported');
                        process.exit();
                    }
                });
            }
            });
        }
        });
   
    Witaj **klienta** obiekt udostępnia wszystkie metody hello wymagają toointeract z twins urządzenia z hello urządzenia. Witaj poprzedni kod po jego inicjuje hello **klienta** obiektu, pobiera Witaj dwie urządzenia dla **myDeviceId** i aktualizuje informacje o łączności hello jego właściwość zgłoszony.
5. Uruchamianie hello urządzenia aplikacji
   
        node ReportConnectivity.js
   
    Powinna zostać wyświetlona wiadomość hello `twin state reported`.
6. Teraz, gdy hello Urządzenie zgłosiło jego informacje dotyczące łączności, powinna pojawić się w obu zapytania. Przejdź wstecz w hello **addtagsandqueryapp** hello folderu i uruchom ponownie zapytanie:
   
        node AddTagsAndQuery.js
   
    Teraz **myDeviceId** powinny być wyświetlane w obu wyników zapytania.
   
    ![][3]

## <a name="next-steps"></a>Następne kroki
W tym samouczku został skonfigurowany nowego centrum IoT w portalu Azure hello i w rejestrze tożsamości Centrum IoT hello zostanie utworzona tożsamość urządzenia. Dodaje metadane urządzenia jako tagi z aplikacji zaplecza i zapisane symulowane urządzenie tooreport urządzenia łączności informacji o aplikacji w Witaj dwie urządzenia. Przedstawiono również sposób tooquery te informacje przy użyciu języka kwerend hello Centrum IoT przypominającego SQL.

Hello Użyj następujących zasobów toolearn jak do:

* wysłać dane telemetryczne z urządzenia z hello [Rozpoczynanie pracy z Centrum IoT] [ lnk-iothub-getstarted] samouczka
* Konfigurowanie urządzeń przy użyciu właściwości żądaną dwie urządzenia z hello [Użyj potrzeby urządzeń tooconfigure właściwości] [ lnk-twin-how-to-configure] samouczka
* sterować urządzenia interakcyjne (takich jak włączanie wentylator z aplikacji kontrolowane przez użytkownika), za pomocą hello [metody bezpośredniego] [ lnk-methods-tutorial] samouczka.

<!-- images -->
[1]: media/iot-hub-node-node-twin-getstarted/service1.png
[3]: media/iot-hub-node-node-twin-getstarted/service2.png

<!-- links -->
[lnk-hub-sdks]: iot-hub-devguide-sdks.md
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/

[lnk-d2c]: iot-hub-devguide-messaging.md#device-to-cloud-messages
[lnk-methods]: iot-hub-devguide-direct-methods.md
[lnk-twins]: iot-hub-devguide-device-twins.md
[lnk-query]: iot-hub-devguide-query-language.md
[lnk-identity]: iot-hub-devguide-identity-registry.md

[lnk-iothub-getstarted]: iot-hub-node-node-getstarted.md
[lnk-device-management]: iot-hub-node-node-device-management-get-started.md
[lnk-iot-edge]: iot-hub-linux-iot-edge-get-started.md
[lnk-connect-device]: https://azure.microsoft.com/develop/iot/

[lnk-twin-how-to-configure]: iot-hub-node-node-twin-how-to-configure.md
[lnk-dev-setup]: https://github.com/Azure/azure-iot-sdk-node/tree/master/doc/node-devbox-setup.md

[lnk-methods-tutorial]: iot-hub-node-node-direct-methods.md
[lnk-devguide-mqtt]: iot-hub-mqtt-support.md
