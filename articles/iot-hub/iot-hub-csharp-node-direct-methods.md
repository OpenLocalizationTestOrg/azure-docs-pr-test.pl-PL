---
title: "Centrum IoT Azure aaaUse bezpośrednie metod (.NET/węzła) | Dokumentacja firmy Microsoft"
description: "Jak toouse Centrum IoT Azure bezpośrednie metody. Node.js tooimplement aplikacji symulowane urządzenie, która obejmuje metoda bezpośrednia i hello zestawu SDK usług Azure IoT dla tooimplement .NET usługi aplikacji, która wywołuje metodę bezpośredniego hello są używane urządzenia Azure IoT hello zestawu SDK."
services: iot-hub
documentationcenter: 
author: nberdy
manager: timlt
editor: 
ms.assetid: ab035b8e-bff8-4e12-9536-f31d6b6fe425
ms.service: iot-hub
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/10/2017
ms.author: nberdy
ms.openlocfilehash: f566f939be840eb308b00ffa4e05c4e5b3fefb39
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="use-direct-methods-netnode"></a>Użyj metody bezpośredniego (.NET/węzeł)
[!INCLUDE [iot-hub-selector-c2d-methods](../../includes/iot-hub-selector-c2d-methods.md)]

W tym samouczku zamierzamy toodevelop .NET i Node.js aplikację konsoli:

* **CallMethodOnDevice.sln**, aplikacji zaplecza .NET, która wywołuje metodę w aplikacji symulowane urządzenie hello i wyświetla hello odpowiedzi.
* **SimulatedDevice.js**, aplikacji Node.js, która symuluje urządzenie łączące Centrum IoT tooyour z tożsamości urządzenia hello utworzony wcześniej i odpowiada toohello metody wywoływane przez hello chmury.

> [!NOTE]
> Artykuł Hello [Azure IoT SDK] [ lnk-hub-sdks] zawiera informacje o hello Azure IoT SDK, której można toobuild toorun zarówno aplikacje na urządzeniach i z zaplecza rozwiązania.
> 
> 

toocomplete tego samouczka należy:

* Program Visual Studio 2015 lub Visual Studio 2017.
* Środowisko Node.js w wersji 0.10.x lub nowszej.
* Aktywne konto platformy Azure. (Jeśli go nie masz, możesz utworzyć [bezpłatne konto próbne][lnk-free-trial] w zaledwie kilka minut).

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity](../../includes/iot-hub-get-started-create-device-identity.md)]

## <a name="create-a-simulated-device-app"></a>Tworzenie aplikacji symulowanego urządzenia
W tej sekcji utworzysz aplikację konsoli Node.js, która odpowiada tooa metody wywoływane przez rozwiązania hello zakończenia.

1. Utwórz nowy pusty folder o nazwie **simulateddevice**. W hello **simulateddevice** folderu, Utwórz plik package.json za pomocą hello następujące polecenie z wiersza polecenia. Zaakceptuj wszystkie domyślne hello:
   
    ```
    npm init
    ```
2. Z wiersza polecenia w hello **simulateddevice** folderu, uruchom następujące polecenie tooinstall hello hello **azure iot urządzenia** i **azure-iot urządzenie mqtt** pakiety:
   
    ```
        npm install azure-iot-device azure-iot-device-mqtt --save
    ```
3. Za pomocą edytora tekstu, Utwórz plik w hello **simulateddevice** folder i nadaj mu nazwę **SimulatedDevice.js**.
4. Dodaj następujące hello `require` instrukcje na powitania początek hello **SimulatedDevice.js** pliku:
   
    ```
    'use strict';
   
    var Mqtt = require('azure-iot-device-mqtt').Mqtt;
    var DeviceClient = require('azure-iot-device').Client;
    ```
5. Dodaj **connectionString** zmiennej i korzystać z niego toocreate **DeviceClient** wystąpienia. Zastąp **{ciąg połączenia urządzenia}** przy użyciu parametrów połączenia urządzenia hello wygenerowanych w hello *tworzenie tożsamości urządzenia* sekcji:
   
    ```
    var connectionString = '{device connection string}';
    var client = DeviceClient.fromConnectionString(connectionString, Mqtt);
    ```
6. Dodaj następujące metoda bezpośrednia hello tooimplement funkcji na urządzeniu hello hello:
   
    ```
    function onWriteLine(request, response) {
        console.log(request.payload);
   
        response.send(200, 'Input was written toolog.', function(err) {
            if(err) {
                console.error('An error occurred when sending a method response:\n' + err.toString());
            } else {
                console.log('Response toomethod \'' + request.methodName + '\' sent successfully.' );
            }
        });
    }
    ```
7. Otwórz Centrum IoT tooyour połączenia hello i zainicjować odbiornika metody hello:
   
    ```
    client.open(function(err) {
        if (err) {
            console.error('could not open IotHub client');
        }  else {
            console.log('client opened');
            client.onDeviceMethod('writeLine', onWriteLine);
        }
    });
    ```
8. Zapisz i zamknij hello **SimulatedDevice.js** pliku.

> [!NOTE]
> rzeczy tookeep proste, w tym samouczku nie implementuje wszystkie zasady ponawiania. W kodzie produkcyjnym, należy zaimplementować zasady ponawiania (np. Ponów próbę połączenia), zgodnie z sugestią podaną w artykuł w witrynie MSDN hello [obsługi błędów przejściowych][lnk-transient-faults].
> 
> 

## <a name="call-a-direct-method-on-a-device"></a>Wywołanie metody bezpośrednio na urządzeniu
W tej sekcji służy do tworzenia aplikacji konsoli .NET, która wywołuje metodę hello symulowane urządzenie aplikacji, a następnie wyświetla hello odpowiedzi.

1. W programie Visual Studio, należy dodać bieżącego rozwiązania toohello projektu Visual C# pulpitu systemu Windows klasycznego przy użyciu hello **aplikacji konsoli** szablonu projektu. Upewnij się, że wersja platformy .NET hello jest 4.5.1 lub nowszej. Nazwa projektu hello **CallMethodOnDevice**.
   
    ![Nowy projekt Visual C# Windows Classic Desktop][10]
2. W Eksploratorze rozwiązań kliknij prawym przyciskiem myszy hello **CallMethodOnDevice** projektu, a następnie kliknij przycisk **Zarządzaj pakietami NuGet...** .
3. W hello **Menedżera pakietów NuGet** wybierz **Przeglądaj**, wyszukaj **microsoft.azure.devices**, wybierz pozycję **zainstalować** tooinstall Witaj **Microsoft.Azure.Devices** pakietu i zaakceptuj warunki użytkowania hello. Ta procedura pliki do pobrania, instaluje i dodaje toohello odwołanie [zestawu SDK usług Azure IoT] [ lnk-nuget-service-sdk] NuGet pakiet i jego zależności.
   
    ![Okno Menedżera pakietów NuGet][11]

4. Dodaj następujące hello `using` instrukcji u góry hello hello **Program.cs** pliku:
   
        using System.Threading.Tasks;
        using Microsoft.Azure.Devices;
5. Dodaj następujące pola toohello hello **Program** klasy. Zastąp wartość symbolu zastępczego hello hello hello koncentratora, który został utworzony w poprzedniej sekcji hello parametry połączenia Centrum IoT.
   
        static ServiceClient serviceClient;
        static string connectionString = "{iot hub connection string}";
6. Dodaj następujące metody toohello hello **Program** klasy:
   
        private static async Task InvokeMethod()
        {
            var methodInvocation = new CloudToDeviceMethod("writeLine") { ResponseTimeout = TimeSpan.FromSeconds(30) };
            methodInvocation.SetPayloadJson("'a line toobe written'");

            var response = await serviceClient.InvokeDeviceMethodAsync("myDeviceId", methodInvocation);

            Console.WriteLine("Response status: {0}, payload:", response.Status);
            Console.WriteLine(response.GetPayloadAsJson());
        }
   
    Ta metoda wywołuje metodę bezpośredniego o nazwie `writeLine` na powitania `myDeviceId` urządzenia. Następnie zapisuje odpowiedź hello udostępniane przez urządzenie hello na powitania konsoli. Należy zwrócić uwagę, jak to możliwe toospecify wartość limitu czasu dla hello toorespond urządzenia.
7. Na koniec należy dodać następujące wiersze toohello hello **Main** metody:
   
        serviceClient = ServiceClient.CreateFromConnectionString(connectionString);
        InvokeMethod().Wait();
        Console.WriteLine("Press Enter tooexit.");
        Console.ReadLine();

## <a name="run-hello-applications"></a>Uruchamianie aplikacji hello
Wszystko jest teraz gotowy toorun hello aplikacji.

1. W hello Visual Studio Solution Explorer, kliknij prawym przyciskiem myszy rozwiązanie, a następnie kliknij przycisk **Ustaw projekty startowe...** . Wybierz **jednego projektu startowego**, a następnie wybierz hello **CallMethodOnDevice** projektu w menu rozwijanym hello.

2. W wierszu polecenia w hello **simulateddevice** folderu, uruchom następujące polecenia toostart nasłuchiwania dla wywołań metod z Centrum IoT hello:
   
    ```
    node SimulatedDevice.js
    ```
   Poczekaj, aż hello symulowane urządzenie tooopen:![][7]
3. Teraz urządzenia hello jest połączony i Oczekiwanie na wywołania metody, uruchom hello .NET **CallMethodOnDevice** metody hello tooinvoke aplikacji hello symulowane urządzenie aplikacji. Powinna zostać wyświetlona odpowiedź urządzenia hello napisana hello konsoli.
   
    ![][8]
4. urządzenie Hello następnie reaguje metody toohello wydrukowanie tej wiadomości:
   
    ![][9]

## <a name="next-steps"></a>Następne kroki
W tym samouczku został skonfigurowany nowego centrum IoT w portalu Azure hello i w rejestrze tożsamości Centrum IoT hello zostanie utworzona tożsamość urządzenia. Użyto tego urządzenia tożsamości tooenable hello symulowane urządzenie aplikacji tooreact toomethods wywołana przez hello chmury. Utworzono aplikację, która wywołuje metody na urządzeniu hello i wyświetla hello odpowiedzi z hello urządzenia. 

toocontinue wprowadzenie do korzystania z Centrum IoT i tooexplore innych scenariuszach IoT, zobacz:

* [Rozpoczynanie pracy z Centrum IoT]
* [Planowanie zadań na wielu urządzeniach][lnk-devguide-jobs]

toolearn tooextend IoT metody rozwiązania i harmonogram wywołuje na wielu urządzeniach, zobacz hello [emisji zadania i harmonogramu] [ lnk-tutorial-jobs] samouczka.

<!-- Images. -->
[7]: ./media/iot-hub-csharp-node-direct-methods/run-simulated-device.png
[8]: ./media/iot-hub-csharp-node-direct-methods/netserviceapp.png
[9]: ./media/iot-hub-csharp-node-direct-methods/methods-output.png

[10]: ./media/iot-hub-csharp-node-direct-methods/direct-methods-csharp1.png
[11]: ./media/iot-hub-csharp-node-direct-methods/direct-methods-csharp2.png

<!-- Links -->
[lnk-transient-faults]: https://msdn.microsoft.com/library/hh680901(v=pandp.50).aspx

[lnk-dev-setup]: https://github.com/Azure/azure-iot-sdk-node/blob/master/doc/node-devbox-setup.md

[lnk-hub-sdks]: iot-hub-devguide-sdks.md
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[lnk-portal]: https://portal.azure.com/
[lnk-nuget-service-sdk]: https://www.nuget.org/packages/Microsoft.Azure.Devices/

[lnk-devguide-jobs]: iot-hub-devguide-jobs.md
[lnk-tutorial-jobs]: iot-hub-node-node-schedule-jobs.md
[lnk-devguide-methods]: iot-hub-devguide-direct-methods.md
[lnk-devguide-mqtt]: iot-hub-mqtt-support.md

[Send Cloud-to-Device messages with IoT Hub]: iot-hub-csharp-csharp-c2d.md
[Process Device-to-Cloud messages]: iot-hub-csharp-csharp-process-d2c.md
[Rozpoczynanie pracy z Centrum IoT]: iot-hub-node-node-getstarted.md
