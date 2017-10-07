---
title: "aaaGet wprowadzenie do zarządzania urządzeniami Centrum IoT Azure (.NET/węzła) | Dokumentacja firmy Microsoft"
description: "Jak tooinitiate zarządzania urządzenia Azure IoT Hub toouse urządzenie zdalne ponowny rozruch. Node.js tooimplement aplikacji symulowane urządzenie, która obejmuje metoda bezpośrednia i hello zestawu SDK usług Azure IoT dla tooimplement .NET usługi aplikacji, która wywołuje metodę bezpośredniego hello są używane urządzenia Azure IoT hello zestawu SDK."
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
ms.date: 11/17/2016
ms.author: juanpere
ms.openlocfilehash: ea6d50dfac1c222d7836e3bf5503c6c9b8c89dfa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-device-management-netnode"></a>Wprowadzenie do zarządzania urządzeniami (.NET/węzeł)

[!INCLUDE [iot-hub-selector-dm-getstarted](../../includes/iot-hub-selector-dm-getstarted.md)]

Ten samouczek przedstawia sposób wykonania następujących czynności:

* Użyj hello toocreate portalu Azure IoT Hub i Utwórz tożsamość urządzenia w Centrum IoT.
* Tworzenie aplikacji symulowane urządzenie zawierającej bezpośredniego metodę, która wykonuje ponowny rozruch tego urządzenia. Bezpośrednie metody są wywoływane z hello chmury.
* Tworzenie aplikacji konsoli .NET, który wywołuje metodę bezpośredniego ponowny rozruch hello w hello symulowane urządzenie aplikacji za pośrednictwem Centrum IoT.

Na końcu hello tego samouczka masz aplikację Node.js konsoli urządzenia i zaplecza aplikacji konsoli .NET (C#):

**dmpatterns_getstarted_device.js**, o tożsamości urządzenia hello utworzony wcześniej, który łączy Centrum IoT tooyour odbiera metoda bezpośrednia ponowny rozruch, symuluje ponowny rozruch komputera fizycznego i raporty hello czasu ostatniego ponownego uruchomienia hello.

**TriggerReboot**, która wywołuje metodę bezpośrednio w aplikacji hello symulowane urządzenie Wyświetla odpowiedź hello, i wyświetla hello zaktualizowane raportowane właściwości.

toocomplete tego samouczka należy hello następujące:

* Program Visual Studio 2015 lub Visual Studio 2017.
* Środowisko node.js w wersji 0.12.x lub nowszym <br/>  [Przygotowywanie środowiska projektowego] [ lnk-dev-setup] w tym artykule opisano sposób tooinstall Node.js, w tym samouczku w systemie Windows lub Linux.
* Aktywne konto platformy Azure. (Jeśli go nie masz, możesz utworzyć [bezpłatne konto próbne][lnk-free-trial] w zaledwie kilka minut).

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity](../../includes/iot-hub-get-started-create-device-identity.md)]

## <a name="trigger-a-remote-reboot-on-hello-device-using-a-direct-method"></a>Wyzwalacz zdalnego ponownego uruchomienia na urządzeniu hello za pomocą bezpośrednich — metoda
W tej sekcji służy do tworzenia aplikacji konsoli .NET (przy użyciu języka C#) inicjującym zdalnego ponownego uruchomienia na urządzeniu przy użyciu metody bezpośredniego. Aplikacja Hello używa urządzenia dwie zapytania toodiscover hello ostatniego ponownego uruchomienia dla tego urządzenia.

1. W programie Visual Studio, Dodaj nowe rozwiązanie tooa projektu Visual C# pulpitu systemu Windows klasycznego przy użyciu hello **aplikacji konsoli (.NET Framework)** szablonu projektu. Upewnij się, że wersja platformy .NET hello jest 4.5.1 lub nowszej. Nazwa projektu hello **TriggerReboot**.

    ![Nowy projekt Visual C# Windows Classic Desktop][img-createapp]

2. W Eksploratorze rozwiązań kliknij prawym przyciskiem myszy hello **TriggerReboot** projektu, a następnie kliknij przycisk **Zarządzaj pakietami NuGet**.
3. W hello **Menedżera pakietów NuGet** wybierz **Przeglądaj**, wyszukaj **microsoft.azure.devices**, wybierz pozycję **zainstalować** tooinstall Witaj **Microsoft.Azure.Devices** pakietu i zaakceptuj warunki użytkowania hello. Ta procedura pliki do pobrania, instaluje i dodaje toohello odwołanie [zestawu SDK usług Azure IoT] [ lnk-nuget-service-sdk] NuGet pakiet i jego zależności.

    ![Okno Menedżera pakietów NuGet][img-servicenuget]
4. Dodaj następujące hello `using` instrukcji u góry hello hello **Program.cs** pliku:
   
        using Microsoft.Azure.Devices;
        using Microsoft.Azure.Devices.Shared;
        
5. Dodaj następujące pola toohello hello **Program** klasy. Zastąp wartość symbolu zastępczego hello hello parametry połączenia Centrum IoT hello koncentratora, który został utworzony w poprzedniej sekcji hello i hello urządzenia docelowego.
   
        static RegistryManager registryManager;
        static string connString = "{iot hub connection string}";
        static ServiceClient client;
        static JobClient jobClient;
        static string targetDevice = "{deviceIdForTargetDevice}";
        
6. Dodaj następujące metody toohello hello **Program** klasy.  Ten kod pobiera hello urządzenia dwie do ponownego uruchamiania urządzenia i danych wyjściowych hello hello zgłosił właściwości.
   
        public static async Task QueryTwinRebootReported()
        {
            Twin twin = await registryManager.GetTwinAsync(targetDevice);
            Console.WriteLine(twin.Properties.Reported.ToJson());
        }
        
7. Dodaj następujące metody toohello hello **Program** klasy.  Ten kod inicjuje hello ponowne uruchomienie komputera, na urządzeniu hello przy użyciu metody bezpośredniego.

        public static async Task StartReboot()
        {
            client = ServiceClient.CreateFromConnectionString(connString);
            CloudToDeviceMethod method = new CloudToDeviceMethod("reboot");
            method.ResponseTimeout = TimeSpan.FromSeconds(30);

            CloudToDeviceMethodResult result = await client.InvokeDeviceMethodAsync(targetDevice, method);

            Console.WriteLine("Invoked firmware update on device.");
        }

7. Na koniec należy dodać następujące wiersze toohello hello **Main** metody:
   
        registryManager = RegistryManager.CreateFromConnectionString(connString);
        StartReboot().Wait();
        QueryTwinRebootReported().Wait();
        Console.WriteLine("Press ENTER tooexit.");
        Console.ReadLine();
        
8. Utworzenie rozwiązania hello.

## <a name="create-a-simulated-device-app"></a>Tworzenie aplikacji symulowanego urządzenia
W tej sekcji zostanie

* Tworzenie aplikacji konsoli Node.js, które odpowiada metoda bezpośrednia tooa wywoływane przez hello chmury
* Wyzwalacz symulowane urządzenie ponowny rozruch
* Hello używany zgłaszane właściwości tooenable urządzeń dwie zapytania tooidentify urządzenia, a podczas ich ostatniego ponownego uruchomienia

1. Utwórz nowy, pusty folder o nazwie **manageddevice**.  W hello **manageddevice** folderu, Utwórz plik package.json za pomocą hello następujące polecenie z wiersza polecenia.  Zaakceptuj wszystkie domyślne hello:
   
    ```
    npm init
    ```
2. Z wiersza polecenia w hello **manageddevice** folderu, uruchom następujące polecenie tooinstall hello hello **azure iot urządzenia** pakiet SDK urządzenia i **azure-iot urządzenie mqtt**pakietu:
   
    ```
    npm install azure-iot-device azure-iot-device-mqtt --save
    ```
3. Za pomocą edytora tekstu, Utwórz nową **dmpatterns_getstarted_device.js** pliku w hello **manageddevice** folderu.
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
7. Dodaj następujący hello kodu centrum IoT tooyour tooopen hello połączenia i uruchomić odbiornik metoda bezpośrednia hello:
   
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


## <a name="run-hello-apps"></a>Uruchamianie aplikacji hello
Wszystko jest teraz gotowy toorun hello aplikacji.

1. W wierszu polecenia hello w hello **manageddevice** folderu Uruchom hello następujące polecenia toobegin nasłuchiwanie metoda bezpośrednia hello ponowny rozruch.
   
    ```
    node dmpatterns_getstarted_device.js
    ```
2. Aplikacja konsoli uruchamiania hello C# **TriggerReboot**. Powitania kliknij prawym przyciskiem myszy **TriggerReboot** projektu, zaznacz **debugowania**, a następnie wybierz **Start nowe wystąpienie**.

3. Zostanie wyświetlony hello urządzenia odpowiedzi toohello metoda bezpośrednia hello konsoli.

[!INCLUDE [iot-hub-dm-followup](../../includes/iot-hub-dm-followup.md)]

<!-- images and links -->
[img-output]: media/iot-hub-get-started-with-dm/image6.png
[img-dm-ui]: media/iot-hub-get-started-with-dm/dmui.png
[img-servicenuget]: media/iot-hub-csharp-node-device-management-get-started/servicesdknuget.png
[img-createapp]: media/iot-hub-csharp-node-device-management-get-started/createnetapp.png

[lnk-dev-setup]: https://github.com/Azure/azure-iot-sdk-node/blob/master/doc/node-devbox-setup.md

[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[Azure portal]: https://portal.azure.com/
[Using resource groups toomanage your Azure resources]: ../azure-portal/resource-group-portal.md
[lnk-dm-github]: https://github.com/Azure/azure-iot-device-management

[lnk-devtwin]: iot-hub-devguide-device-twins.md
[lnk-c2dmethod]: iot-hub-devguide-direct-methods.md
[lnk-transient-faults]: https://msdn.microsoft.com/library/hh680901(v=pandp.50).aspx
[lnk-nuget-service-sdk]: https://www.nuget.org/packages/Microsoft.Azure.Devices/