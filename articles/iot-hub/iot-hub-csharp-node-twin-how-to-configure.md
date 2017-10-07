---
title: "właściwości dwie urządzenia Azure IoT Hub aaaUse (.NET/węzła) | Dokumentacja firmy Microsoft"
description: "Jak urządzenia Azure IoT Hub toouse twins tooconfigure urządzeń. Możesz użyć urządzenia Azure IoT hello zestawu SDK dla środowiska Node.js tooimplement aplikacji symulowane urządzenie i hello zestawu SDK usług Azure IoT dla tooimplement .NET usługi aplikacji, które modyfikuje konfigurację urządzenia przy użyciu podwójnego urządzenia."
services: iot-hub
documentationcenter: .net
author: fsautomata
manager: timlt
editor: 
ms.assetid: 3c627476-f982-43c9-bd17-e0698c5d236d
ms.service: iot-hub
ms.devlang: node
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/30/2017
ms.author: elioda
ms.openlocfilehash: 840a1b2e45f4763131299577583aa89015dcdd1d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="use-desired-properties-tooconfigure-devices"></a>Używanie urządzeń tooconfigure odpowiednie właściwości
[!INCLUDE [iot-hub-selector-twin-how-to-configure](../../includes/iot-hub-selector-twin-how-to-configure.md)]

Na końcu hello tego samouczka masz dwie aplikacje konsoli:

* **SimulateDeviceConfiguration.js**, aplikację symulowane urządzenie, która oczekuje na aktualizację wymaganą konfiguracją i hello stanu procesu aktualizacji konfiguracji symulowane.
* **SetDesiredConfigurationAndQuery**, konfiguracja na urządzeniu żądanego aplikacji zaplecza .NET, która ustawia hello i zapytań hello konfiguracji procesu aktualizacji.

> [!NOTE]
> Artykuł Hello [Azure IoT SDK] [ lnk-hub-sdks] informacje na temat hello Azure IoT SDK służy toobuild zarówno urządzenia, jak i zaplecza aplikacji.
> 
> 

toocomplete tego samouczka należy hello poniżej:

* Program Visual Studio 2015 lub Visual Studio 2017.
* Środowisko Node.js w wersji 0.10.x lub nowszej.
* Aktywne konto platformy Azure. Jeśli go nie masz, możesz utworzyć [bezpłatne konto][lnk-free-trial] w zaledwie kilka minut.

Po wykonaniu hello [Rozpoczynanie pracy z urządzenia twins] [ lnk-twin-tutorial] samouczek, masz już Centrum IoT i tożsamość urządzenia o nazwie **myDeviceId**. W takim przypadku można pominąć toohello [Utwórz hello symulowane urządzenie aplikacji] [ lnk-how-to-configure-createapp] sekcji.

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity](../../includes/iot-hub-get-started-create-device-identity.md)]

<a id="#create-the-simulated-device-app"></a>
## <a name="create-hello-simulated-device-app"></a>Tworzenie aplikacji symulowane urządzenie hello
W tej sekcji zostanie utworzona aplikacja konsoli Node.js łączącego koncentratora tooyour **myDeviceId**, czeka na aktualizację wymaganą konfiguracją, a następnie przedstawia aktualizacje na proces aktualizacji konfiguracji hello symulowane.

1. Utwórz nowy, pusty folder o nazwie **simulatedeviceconfiguration**. W hello **simulatedeviceconfiguration** folderu, Utwórz nowy plik package.json przy użyciu hello następujące polecenie z wiersza polecenia. Zaakceptuj wszystkie domyślne hello.
   
    ```
    npm init
    ```
1. Z wiersza polecenia w hello **simulatedeviceconfiguration** folderu, uruchom następujące polecenie tooinstall hello hello **azure iot urządzenia** i **azure-iot urządzenie mqtt**pakiety:
   
    ```
    npm install azure-iot-device azure-iot-device-mqtt --save
    ```
1. Za pomocą edytora tekstu, Utwórz nową **SimulateDeviceConfiguration.js** pliku w hello **simulatedeviceconfiguration** folderu.
1. Dodaj hello następującego kodu toohello **SimulateDeviceConfiguration.js** plików i Zastąp hello **{ciąg połączenia urządzenia}** symbol zastępczy parametrów połączenia urządzenia hello skopiowane podczas możesz utworzony hello **myDeviceId** tożsamości urządzenia:
   
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
   
    Witaj **klienta** obiekt udostępnia wszystkie hello metody wymagane toointeract z twins urządzenia z hello urządzenia. Ten kod inicjuje hello **klienta** obiektu, pobiera Witaj dwie urządzenia dla **myDeviceId**i następnie dołącza program obsługi aktualizacji hello na *żądanego właściwości*. Program Hello obsługi sprawdza, który jest żądanie zmiany konfiguracji rzeczywiste porównując hello configIds, a następnie wywołuje metodę, która rozpoczyna się zmianę konfiguracji hello.
   
    Należy pamiętać, że dla zapewnienia hello prostotę, ten kod używa domyślnego ustalony hello początkową konfigurację. Rzeczywiste aplikacji będzie prawdopodobnie załadować tej konfiguracji z magazynu lokalnego.
   
   > [!IMPORTANT]
   > Zdarzenia zmiany żądanej właściwości zawsze są emitowane raz na połączenie z urządzeniem. Upewnij się, że istnieje rzeczywiste zmiany w hello toocheck żądanego właściwości przed wykonaniem jakiegokolwiek działania.
   > 
   > 
1. Dodaj następujące metody przed hello hello `client.open()` wywołania:
   
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
   
    Hello **initConfigChange** hello aktualizacje — metoda zgłosił zbyt żądania i zestawy stanu hello aktualizacji właściwości w obiekcie dwie urządzenie lokalne powitania z konfiguracją hello**oczekujące**, a następnie hello aktualizacji dwie urządzenia w usłudze hello. Po pomyślnym zaktualizowaniu Witaj dwie urządzenia, jego symuluje długotrwała proces, który kończy w realizacji hello **completeConfigChange**. Ta metoda aktualizuje właściwości zgłoszony z lokalne powitania ustawiania stanu hello zbyt**Powodzenie** i usuwanie hello **pendingConfig** obiektu. Aktualizuje Witaj dwie urządzenia w usłudze hello.
   
    Pamiętaj, że toosave przepustowości, zgłaszany właściwości są aktualizowane, określając modyfikować tylko toobe właściwości hello (o nazwie **poprawki** w hello powyżej kodu), zamiast zastępowanie hello całego dokumentu.
   
   > [!NOTE]
   > W tym samouczku nie zasymulować wszystkie zachowania aktualizacji konfiguracji współbieżnych. Niektóre procesy aktualizacji konfiguracji może być tooaccommodate stanie zmiany konfiguracji docelowej, podczas gdy aktualizacja hello jest uruchomiona, niektóre mogą być tooqueue je, a niektóre można odrzucić warunek błędu. Upewnij się, że tooconsider hello zachowanie procesu określonej konfiguracji, a następnie dodaj odpowiednie logiki hello przed zainicjowaniem hello zmiana konfiguracji.
   > 
   > 
1. Uruchamianie aplikacji urządzenia hello:
   
        node SimulateDeviceConfiguration.js
   
    Powinna zostać wyświetlona wiadomość hello `retrieved device twin`. Zachowaj aplikacji hello uruchomiona.

## <a name="create-hello-service-app"></a>Tworzenie aplikacji usługi hello
W tej sekcji utworzysz aplikacji konsoli .NET hello tej aktualizacji *żądanego właściwości* na powitania dwie urządzeń skojarzonych z **myDeviceId** z obiektem konfiguracji telemetrii. Następnie zapytań przechowywane w Centrum IoT hello twins urządzenia hello i przedstawia hello różnica między hello potrzeby i zgłosił konfiguracje hello urządzenia.

1. W programie Visual Studio, należy dodać bieżącego rozwiązania toohello projektu Visual C# pulpitu systemu Windows klasycznego przy użyciu hello **aplikacji konsoli** szablonu projektu. Nazwa projektu hello **SetDesiredConfigurationAndQuery**.
   
    ![Nowy projekt Visual C# Windows Classic Desktop][img-createapp]
1. W Eksploratorze rozwiązań kliknij prawym przyciskiem myszy hello **SetDesiredConfigurationAndQuery** projektu, a następnie kliknij przycisk **Zarządzaj pakietami NuGet...** .
1. W hello **Menedżera pakietów NuGet** wybierz **Przeglądaj**, wyszukaj **microsoft.azure.devices**, wybierz pozycję **zainstalować** tooinstall Witaj **Microsoft.Azure.Devices** pakietu i zaakceptuj warunki użytkowania hello. Ta procedura pliki do pobrania, instaluje i dodaje toohello odwołanie [zestawu SDK usług Azure IoT] [ lnk-nuget-service-sdk] NuGet pakiet i jego zależności.
   
    ![Okno Menedżera pakietów NuGet][img-servicenuget]
1. Dodaj następujące hello `using` instrukcji u góry hello hello **Program.cs** pliku:
   
        using Microsoft.Azure.Devices;
        using System.Threading;
        using Newtonsoft.Json;
1. Dodaj następujące pola toohello hello **Program** klasy. Zastąp wartość symbolu zastępczego hello hello hello koncentratora, który został utworzony w poprzedniej sekcji hello parametry połączenia Centrum IoT.
   
        static RegistryManager registryManager;
        static string connectionString = "{iot hub connection string}";
1. Dodaj następujące metody toohello hello **Program** klasy:
   
        static private async Task SetDesiredConfigurationAndQuery()
        {
            var twin = await registryManager.GetTwinAsync("myDeviceId");
            var patch = new {
                    properties = new {
                        desired = new {
                            telemetryConfig = new {
                                configId = Guid.NewGuid().ToString(),
                                sendFrequency = "5m"
                            }
                        }
                    }
                };
   
            await registryManager.UpdateTwinAsync(twin.DeviceId, JsonConvert.SerializeObject(patch), twin.ETag);
            Console.WriteLine("Updated desired configuration");
   
            try
            {
                while (true)
                {
                    var query = registryManager.CreateQuery("SELECT * FROM devices WHERE deviceId = 'myDeviceId'");
                    var results = await query.GetNextAsTwinAsync();
                    foreach (var result in results)
                    {
                        Console.WriteLine("Config report for: {0}", result.DeviceId);
                        Console.WriteLine("Desired telemetryConfig: {0}", JsonConvert.SerializeObject(result.Properties.Desired["telemetryConfig"], Formatting.Indented));
                        Console.WriteLine("Reported telemetryConfig: {0}", JsonConvert.SerializeObject(result.Properties.Reported["telemetryConfig"], Formatting.Indented));
                        Console.WriteLine();
                    }
                    Thread.Sleep(10000);
                }
            }
            catch (Exception ex)
            {
                Console.WriteLine($"Exception: {ex.Message}");
            }
        }
   
    Witaj **rejestru** obiekt udostępnia wszystkie hello metody wymagane toointeract z twins urządzenia z usługi hello. Ten kod inicjuje hello **rejestru** obiektu, pobiera Witaj dwie urządzenia dla **myDeviceId**, a następnie aktualizuje jego żądanej właściwości z obiektem konfiguracji telemetrii.
    Po wykonaniu tej wysyła zapytanie twins urządzenia hello przechowywane w Centrum IoT hello co 10 sekund, a hello odbitek potrzeby i zgłosił konfiguracje telemetrii. Zobacz toohello [język zapytań Centrum IoT] [ lnk-query] toolearn jak sformatowanego toogenerate raporty na Twoich urządzeniach.
   
   > [!IMPORTANT]
   > Ta aplikacja kwerendę Centrum IoT co 10 sekund w celach ilustracyjnych. Użyj zapytań toogenerate raporty dla użytkownika na wielu urządzeniach, a nie toodetect zmiany. Jeśli rozwiązanie wymaga powiadomień w czasie rzeczywistym zdarzeń urządzenia, należy użyć [dwie powiadomienia][lnk-twin-notifications].
   > 
   > 
1. Na koniec należy dodać następujące wiersze toohello hello **Main** metody:
   
        registryManager = RegistryManager.CreateFromConnectionString(connectionString);
        SetDesiredConfigurationAndQuery().Wait();
        Console.WriteLine("Press any key tooquit.");
        Console.ReadLine();
1. W Eksploratorze rozwiązań hello, otwórz hello **projektów startowych ustawić...**  i upewnij się, że hello **akcji** dla **SetDesiredConfigurationAndQuery** projekt jest **Start**. Utworzenie rozwiązania hello.
1. Z **SimulateDeviceConfiguration.js** uruchomiona, uruchom aplikację .NET hello z programu Visual Studio za pomocą **F5** i powinna zostać wyświetlona zmiany w konfiguracji zgłoszone hello **Powodzenie** za**oczekujące** za**Powodzenie** ponownie za pomocą nowego aktywny hello wysyłać częstotliwość pięć minut zamiast 24 godziny.

 ![Urządzenie zostało pomyślnie skonfigurowane][img-deviceconfigured]
   
   > [!IMPORTANT]
   > Istnieje opóźnienie zapasowej protokołu tooa między hello urządzenia raport operacji i hello wyniku zapytania. Jest to tooenable hello zapytania infrastruktury toowork na bardzo dużą skalę. Widoki spójne tooretrieve dwie pojedyncze urządzenie, użyj hello **getDeviceTwin** metoda hello **rejestru** klasy.
   > 
   > 

## <a name="next-steps"></a>Następne kroki
W tym samouczku, ustaw żądaną konfiguracją jako *żądanego właściwości* z rozwiązania hello zaplecza i zapisano toodetect aplikacji urządzenia, zmiany i symulować proces aktualizacji wieloetapowych raportowania stanu za pośrednictwem hello zgłosił właściwości.

Hello Użyj następujących zasobów toolearn jak do:

* wysłać dane telemetryczne z urządzenia z hello [Rozpoczynanie pracy z Centrum IoT] [ lnk-iothub-getstarted] samouczka
* harmonogramu lub wykonania operacji na dużych zestawów urządzeń Zobacz hello [emisji zadania i harmonogramu] [ lnk-schedule-jobs] samouczka.
* sterować urządzenia interakcyjne (takich jak włączanie wentylator z aplikacji kontrolowane przez użytkownika), za pomocą hello [metody bezpośredniego] [ lnk-methods-tutorial] samouczka.

<!-- images -->
[img-servicenuget]: media/iot-hub-csharp-node-twin-how-to-configure/servicesdknuget.png
[img-createapp]: media/iot-hub-csharp-node-twin-how-to-configure/createnetapp.png
[img-deviceconfigured]: media/iot-hub-csharp-node-twin-how-to-configure/deviceconfigured.png

<!-- links -->
[lnk-hub-sdks]: iot-hub-devguide-sdks.md
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[lnk-nuget-service-sdk]: https://www.nuget.org/packages/Microsoft.Azure.Devices/1.1.0/

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
[lnk-iothub-getstarted]: iot-hub-node-node-getstarted.md
[lnk-methods-tutorial]: iot-hub-node-node-direct-methods.md

[lnk-guid]: https://en.wikipedia.org/wiki/Globally_unique_identifier

[lnk-how-to-configure-createapp]: iot-hub-csharp-node-twin-how-to-configure.md#create-the-simulated-device-app
