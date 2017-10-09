---
title: "aaaGet wprowadzenie twins urządzenia Azure IoT Hub (.NET/węzła) | Dokumentacja firmy Microsoft"
description: "Jak tooadd twins urządzenia Azure IoT Hub toouse tagów, a następnie użyj zapytania Centrum IoT. Używasz urządzenia Azure IoT hello zestawu SDK dla środowiska Node.js tooimplement hello symulowane urządzenie aplikacji i hello zestawu SDK usług Azure IoT dla .NET tooimplement aplikacji usługi, który dodaje znaczniki hello i uruchamia hello zapytania Centrum IoT."
services: iot-hub
documentationcenter: node
author: fsautomata
manager: timlt
editor: 
ms.assetid: f7e23b6e-bfde-4fba-a6ec-dbb0f0e005f4
ms.service: iot-hub
ms.devlang: node
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/29/2017
ms.author: elioda
ms.openlocfilehash: 1cec082ebddc19c9b87998a5fd0159d32b07acd8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-device-twins-netnode"></a>Rozpoczynanie pracy z urządzenia twins (.NET/węzeł)
[!INCLUDE [iot-hub-selector-twin-get-started](../../includes/iot-hub-selector-twin-get-started.md)]

Na końcu hello tego samouczka konieczne będzie .NET i Node.js aplikację konsoli:

* **AddTagsAndQuery.sln**, aplikacji zaplecza .NET, która dodaje znaczniki i zapytanie twins urządzenia.
* **TwinSimulatedDevice.js**, aplikacji Node.js, która symuluje urządzenie łączące Centrum IoT tooyour o tożsamości urządzenia hello utworzony wcześniej, a następnie raportuje stanu łączności.

> [!NOTE]
> Artykuł Hello [Azure IoT SDK] [ lnk-hub-sdks] informacje na temat hello Azure IoT SDK służy toobuild zarówno urządzenia, jak i zaplecza aplikacji.
> 
> 

toocomplete tego samouczka należy hello poniżej:

* Program Visual Studio 2015 lub Visual Studio 2017.
* Środowisko Node.js w wersji 0.10.x lub nowszej.
* Aktywne konto platformy Azure. (Jeśli go nie masz, możesz utworzyć [bezpłatne konto próbne][lnk-free-trial] w zaledwie kilka minut).

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity](../../includes/iot-hub-get-started-create-device-identity.md)]

## <a name="create-hello-service-app"></a>Tworzenie aplikacji usługi hello
W tej sekcji Tworzenie aplikacji konsoli .NET (przy użyciu języka C#) dodające skojarzone z lokalizacji metadanych toohello urządzenia dwie **myDeviceId**. Następnie zapytania twins urządzenia hello przechowywane w Centrum IoT hello Wybieranie hello urządzeń znajdujących się w hello nam, a następnie hello tych, którzy zgłosili komórkowej połączenia.

1. W programie Visual Studio, należy dodać bieżącego rozwiązania toohello projektu Visual C# pulpitu systemu Windows klasycznego przy użyciu hello **aplikacji konsoli** szablonu projektu. Nazwa projektu hello **AddTagsAndQuery**.
   
    ![Nowy projekt Visual C# Windows Classic Desktop][img-createapp]
1. W Eksploratorze rozwiązań kliknij prawym przyciskiem myszy hello **AddTagsAndQuery** projektu, a następnie kliknij przycisk **Zarządzaj pakietami NuGet...** .
1. W hello **Menedżera pakietów NuGet** wybierz **Przeglądaj** i wyszukaj **microsoft.azure.devices**. Wybierz **zainstalować** tooinstall hello **Microsoft.Azure.Devices** pakietu i zaakceptuj warunki użytkowania hello. Ta procedura pliki do pobrania, instaluje i dodaje toohello odwołanie [zestawu SDK usług Azure IoT] [ lnk-nuget-service-sdk] NuGet pakiet i jego zależności.
   
    ![Okno Menedżera pakietów NuGet][img-servicenuget]
1. Dodaj następujące hello `using` instrukcji u góry hello hello **Program.cs** pliku:
   
        using Microsoft.Azure.Devices;
1. Dodaj następujące pola toohello hello **Program** klasy. Zastąp wartość symbolu zastępczego hello hello hello koncentratora, który został utworzony w poprzedniej sekcji hello parametry połączenia Centrum IoT.
   
        static RegistryManager registryManager;
        static string connectionString = "{iot hub connection string}";
1. Dodaj następujące metody toohello hello **Program** klasy:
   
        public static async Task AddTagsAndQuery()
        {
            var twin = await registryManager.GetTwinAsync("myDeviceId");
            var patch =
                @"{
                    tags: {
                        location: {
                            region: 'US',
                            plant: 'Redmond43'
                        }
                    }
                }";
            await registryManager.UpdateTwinAsync(twin.DeviceId, patch, twin.ETag);
   
            var query = registryManager.CreateQuery("SELECT * FROM devices WHERE tags.location.plant = 'Redmond43'", 100);
            var twinsInRedmond43 = await query.GetNextAsTwinAsync();
            Console.WriteLine("Devices in Redmond43: {0}", string.Join(", ", twinsInRedmond43.Select(t => t.DeviceId)));
   
            query = registryManager.CreateQuery("SELECT * FROM devices WHERE tags.location.plant = 'Redmond43' AND properties.reported.connectivity.type = 'cellular'", 100);
            var twinsInRedmond43UsingCellular = await query.GetNextAsTwinAsync();
            Console.WriteLine("Devices in Redmond43 using cellular network: {0}", string.Join(", ", twinsInRedmond43UsingCellular.Select(t => t.DeviceId)));
        }
   
    Witaj **RegistryManager** klasa przedstawia wszystkie hello metody wymagane toointeract z twins urządzenia z usługi hello. Poprzedni kod Hello najpierw inicjuje hello **registryManager** obiektu, a następnie pobiera Witaj dwie urządzenia dla **myDeviceId**i na koniec aktualizuje jego tagi hello potrzeby informacji o lokalizacji.
   
    Po zaktualizowaniu, wykonuje on dwa zapytania: hello najpierw wybiera tylko twins urządzenia hello urządzeń znajdujących się w hello **Redmond43** roślin i hello drugi refines hello zapytania tooselect tylko hello urządzeń podłączonych do sieci komórkowej.
   
    Należy pamiętać, że poprzedni kod hello, podczas tworzenia hello **zapytania** obiektów, określa maksymalną liczbę zwracanych dokumentów. Hello **zapytania** zawiera obiekt **HasMoreResults** właściwości typu boolean służy tooinvoke hello **GetNextAsTwinAsync** metody wszystkie tooretrieve wiele razy wyniki. Wywołana metoda **GetNextAsJson** jest dostępna dla wyników, które są nie twins urządzenia, na przykład wyniki zapytań agregacji.
1. Na koniec należy dodać następujące wiersze toohello hello **Main** metody:
   
        registryManager = RegistryManager.CreateFromConnectionString(connectionString);
        AddTagsAndQuery().Wait();
        Console.WriteLine("Press Enter tooexit.");
        Console.ReadLine();

1. W Eksploratorze rozwiązań hello, otwórz hello **projektów startowych ustawić...**  i upewnij się, że hello **akcji** dla **AddTagsAndQuery** projekt jest **Start**. Utworzenie rozwiązania hello.
1. Uruchomić tę aplikację, klikając prawym przyciskiem myszy na powitania **AddTagsAndQuery** projekt i wybierając **debugowania**, a następnie **Start nowe wystąpienie**. Powinny pojawić się jedno urządzenie w wynikach hello hello zadać zapytania dla wszystkich urządzeń znajdujących się w **Redmond43** i Brak dla zapytania hello, która ogranicza hello powoduje toodevices używanego przez sieć komórkową.
   
    ![Wyniki zapytania w oknie][img-addtagapp]

W następnej sekcji hello możesz utworzyć aplikację urządzenia, która raportuje informacje o łączności hello i zmiany hello wynik kwerendy hello w poprzedniej sekcji hello.

## <a name="create-hello-device-app"></a>Tworzenie hello urządzenia aplikacji
W tej sekcji zostanie utworzona aplikacja konsoli Node.js łączącego koncentratora tooyour **myDeviceId**, a następnie aktualizuje informacje hello toocontain zgłoszone właściwości jest on podłączony za pomocą sieci komórkowej.

1. Utwórz nowy, pusty folder o nazwie **reportconnectivity**. W hello **reportconnectivity** folderu, Utwórz nowy plik package.json przy użyciu hello następujące polecenie z wiersza polecenia. Zaakceptuj wszystkie domyślne hello.
   
    ```
    npm init
    ```
1. Z wiersza polecenia w hello **reportconnectivity** folderu, uruchom następujące polecenie tooinstall hello hello **azure iot urządzenia**, i **azure-iot urządzenie mqtt** pakietu :
   
    ```
    npm install azure-iot-device azure-iot-device-mqtt --save
    ```
1. Za pomocą edytora tekstu, Utwórz nową **ReportConnectivity.js** pliku w hello **reportconnectivity** folderu.
1. Dodaj hello następującego kodu toohello **ReportConnectivity.js** plików i Zastąp symbol zastępczy parametrów połączenia urządzenia z hello jedną skopiowane podczas tworzenia hello hello **myDeviceId** urządzenia tożsamości:
   
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
1. Uruchamianie hello urządzenia aplikacji
   
        node ReportConnectivity.js
   
    Powinna zostać wyświetlona wiadomość hello `twin state reported`.
1. Teraz, gdy hello Urządzenie zgłosiło jego informacje dotyczące łączności, powinna pojawić się w obu zapytania. Uruchom hello .NET **AddTagsAndQuery** aplikacji hello toorun wysyła zapytanie ponownie. Teraz **myDeviceId** powinny być wyświetlane w obu wyników zapytania.
   
    ![][img-addtagapp2]

## <a name="next-steps"></a>Następne kroki
W tym samouczku został skonfigurowany nowego centrum IoT w portalu Azure hello i w rejestrze tożsamości Centrum IoT hello zostanie utworzona tożsamość urządzenia. Dodaje metadane urządzenia jako tagi z aplikacji zaplecza i zapisane symulowane urządzenie tooreport urządzenia łączności informacji o aplikacji w Witaj dwie urządzenia. Przedstawiono również sposób tooquery te informacje przy użyciu języka kwerend hello Centrum IoT przypominającego SQL.

Hello Użyj następujących zasobów toolearn jak do:

* wysłać dane telemetryczne z urządzenia z hello [Rozpoczynanie pracy z Centrum IoT] [ lnk-iothub-getstarted] samouczka
* Konfigurowanie urządzeń przy użyciu właściwości żądaną dwie urządzenia z hello [Użyj potrzeby urządzeń tooconfigure właściwości] [ lnk-twin-how-to-configure] samouczka
* kontrolowanie urządzenia interakcyjne (takich jak włączanie wentylator z aplikacji kontrolowane przez użytkownika) z hello [metody bezpośredniego] [ lnk-methods-tutorial] samouczka.

<!-- images -->
[img-servicenuget]: media/iot-hub-csharp-node-twin-getstarted/servicesdknuget.png
[img-createapp]: media/iot-hub-csharp-node-twin-getstarted/createnetapp.png
[img-addtagapp]: media/iot-hub-csharp-node-twin-getstarted/addtagapp.png
[img-addtagapp2]: media/iot-hub-csharp-node-twin-getstarted/addtagapp2.png

<!-- links -->
[lnk-hub-sdks]: iot-hub-devguide-sdks.md
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[lnk-nuget-service-sdk]: https://www.nuget.org/packages/Microsoft.Azure.Devices/

[lnk-d2c]: iot-hub-devguide-messaging.md#device-to-cloud-messages
[lnk-methods]: iot-hub-devguide-direct-methods.md
[lnk-twins]: iot-hub-devguide-device-twins.md
[lnk-query]: iot-hub-devguide-query-language.md
[lnk-identity]: iot-hub-devguide-identity-registry.md

[lnk-iothub-getstarted]: iot-hub-node-node-getstarted.md
[lnk-methods-tutorial]: iot-hub-node-node-direct-methods.md
[lnk-twin-how-to-configure]: iot-hub-csharp-node-twin-how-to-configure.md

[lnk-dev-setup]: https://github.com/Azure/azure-iot-sdk-node/blob/master/doc/node-devbox-setup.md

