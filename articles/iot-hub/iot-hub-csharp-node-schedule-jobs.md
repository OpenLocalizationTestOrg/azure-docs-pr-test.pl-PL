---
title: "zadania aaaSchedule z Centrum IoT Azure (.NET/węzła) | Dokumentacja firmy Microsoft"
description: "Jak tooschedule Centrum IoT Azure zadania tooinvoke metoda bezpośrednia na wielu urządzeniach. Możesz używać urządzenia Azure IoT hello zestawu SDK dla środowiska Node.js tooimplement hello symulowane urządzenie aplikacji i hello Azure IoT usługa zestawu SDK .NET tooimplement zadania hello toorun aplikacji usługi."
services: iot-hub
documentationcenter: .net
author: juanjperez
manager: timlt
editor: 
ms.assetid: 2233356e-b005-4765-ae41-3a4872bda943
ms.service: iot-hub
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/10/2017
ms.author: juanpere
ms.openlocfilehash: f6148b67129dde4580bfe9ccceafd6400fbc5976
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="schedule-and-broadcast-jobs-netnodejs"></a>Zadania harmonogramu i emisji (.NET/Node.js)

[!INCLUDE [iot-hub-selector-schedule-jobs](../../includes/iot-hub-selector-schedule-jobs.md)]

Użyj Centrum IoT Azure tooschedule i Śledź zadań aktualizowanych milionów urządzeń. Należy użyć zadania, aby:

* Aktualizowanie żądanych właściwości
* Tagi aktualizacji
* Wywołanie metody bezpośredniego

Zadanie opakowuje jedną z następujących czynności i śledzi hello miało zostać wykonane zbiór urządzeń jest definiowana za pomocą zapytania dwie urządzenia. Na przykład aplikacji zaplecza można użyć zadania tooinvoke metoda bezpośrednia na 10 000 urządzeń, które wykonuje ponowny rozruch hello urządzeń. Określ zestaw hello urządzeń za pomocą kwerendy dwie urządzenia i zaplanować hello toorun zadania w przyszłości. postęp śledzi zadania Hello jako każdego urządzenia hello odbierania i wykonaj metoda bezpośrednia hello ponowne uruchomienie komputera.

toolearn więcej informacji na temat każdego z tych funkcji, zobacz:

* Dwie urządzeń i właściwości: [Rozpoczynanie pracy z urządzenia twins] [ lnk-get-started-twin] i [samouczek: jak urządzenie toouse dwie właściwości][lnk-twin-props]
* Bezpośrednie metody: [przewodnik dewelopera Centrum IoT — metody bezpośredniego] [ lnk-dev-methods] i [samouczek: bezpośrednie metody][lnk-c2d-methods]

Ten samouczek przedstawia sposób wykonania następujących czynności:

* Tworzenie aplikacji urządzenia implementujący bezpośredniego metodę o nazwie **lockDoor** który może być wywoływany przez hello zaplecza aplikacji. Aplikacja urządzenia Hello również odbiera zmiany żądanej właściwości z hello zaplecza aplikacji.
* Tworzenie aplikacji zaplecza, która tworzy hello toocall zadania **lockDoor** metoda bezpośrednia na wielu urządzeniach. Inne zadanie wysyła żądanej właściwości aktualizuje toomultiple urządzeń.

Na końcu hello tego samouczka masz aplikację Node.js konsoli urządzenia i zaplecza aplikacji konsoli .NET (C#):

**simDevice.js** który łączy Centrum IoT tooyour, implementuje hello **lockDoor** bezpośrednie — metoda i uchwytów potrzebne zmiany właściwości.

**ScheduleJob** używającą hello toocall zadania **lockDoor** właściwości na wielu urządzeniach potrzeby bezpośredniego metoda i aktualizacji dwie hello w urządzeniu.

toocomplete tego samouczka należy hello następujące:

* Program Visual Studio 2015 lub Visual Studio 2017.
* Środowisko Node.js w wersji 0.12.x lub nowszej. Artykuł Hello [przygotowywanie środowiska projektowego] [ lnk-dev-setup] w tym artykule opisano sposób tooinstall Node.js, w tym samouczku w systemie Windows lub Linux.
* Aktywne konto platformy Azure. Jeśli go nie masz, możesz utworzyć [bezpłatne konto][lnk-free-trial] w zaledwie kilka minut.

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity](../../includes/iot-hub-get-started-create-device-identity.md)]

## <a name="schedule-jobs-for-calling-a-direct-method-and-sending-device-twin-updates"></a>Planowanie zadań dla wywołania metody bezpośredniego i wysyłania aktualizacji dwie urządzenia

W tej sekcji Tworzenie aplikacji konsoli .NET (przy użyciu języka C#) używającej hello toocall zadania **lockDoor** metoda bezpośrednia i wysłać żądanej właściwości aktualizuje toomultiple urządzeń.

1. W programie Visual Studio, należy dodać bieżącego rozwiązania toohello projektu Visual C# pulpitu systemu Windows klasycznego przy użyciu hello **aplikacji konsoli** szablonu projektu. Nazwa projektu hello **ScheduleJob**.

    ![Nowy projekt Visual C# Windows Classic Desktop][img-createapp]

1. W Eksploratorze rozwiązań kliknij prawym przyciskiem myszy hello **ScheduleJob** projektu, a następnie kliknij przycisk **Zarządzaj pakietami NuGet...** .
1. W hello **Menedżera pakietów NuGet** wybierz **Przeglądaj**, wyszukaj **microsoft.azure.devices**, wybierz pozycję **zainstalować** tooinstall Witaj **Microsoft.Azure.Devices** pakietu i zaakceptuj warunki użytkowania hello. Ten krok pliki do pobrania, instaluje i dodaje toohello odwołanie [zestawu SDK usług Azure IoT] [ lnk-nuget-service-sdk] NuGet pakiet i jego zależności.

    ![Okno Menedżera pakietów NuGet][img-servicenuget]
1. Dodaj następujące hello `using` instrukcji u góry hello hello **Program.cs** pliku:
    
    ```csharp
    using Microsoft.Azure.Devices;
    using Microsoft.Azure.Devices.Shared;
    ```

1. Dodaj następujące hello `using` instrukcję, jeśli jeszcze nie istnieje w instrukcjach domyślne hello.

    ```csharp
    using System.Threading.Tasks;
    ```

1. Dodaj następujące pola toohello hello **Program** klasy. Zastąp symbol zastępczy hello hello hello koncentratora, który został utworzony w poprzedniej sekcji hello parametry połączenia Centrum IoT.

    ```csharp
    static string connString = "{iot hub connection string}";
    static ServiceClient client;
    static JobClient jobClient;
    ```

1. Dodaj następujące metody toohello hello **Program** klasy:

    ```csharp
    public static async Task MonitorJob(string jobId)
    {
        JobResponse result;
        do
        {
            result = await jobClient.GetJobAsync(jobId);
            Console.WriteLine("Job Status : " + result.Status.ToString());
            Thread.Sleep(2000);
        } while ((result.Status != JobStatus.Completed) && (result.Status != JobStatus.Failed));
    }
    ```

1. Dodaj następujące metody toohello hello **Program** klasy:

    ```csharp
    public static async Task StartMethodJob(string jobId)
    {
        CloudToDeviceMethod directMethod = new CloudToDeviceMethod("lockDoor", TimeSpan.FromSeconds(5), TimeSpan.FromSeconds(5));

        JobResponse result = await jobClient.ScheduleDeviceMethodAsync(jobId,
            "deviceId='myDeviceId'",
            directMethod,
            DateTime.Now,
            10);

        Console.WriteLine("Started Method Job");
    }
    ```

1. Dodaj następujące metody toohello hello **Program** klasy:

    ```csharp
    public static async Task StartTwinUpdateJob(string jobId)
    {
        var twin = new Twin();
        twin.Properties.Desired["Building"] = "43";
        twin.Properties.Desired["Floor"] = "3";
        twin.ETag = "*";

        JobResponse result = await jobClient.ScheduleTwinUpdateAsync(jobId,
            "deviceId='myDeviceId'",
            twin,
            DateTime.Now,
            10);

        Console.WriteLine("Started Twin Update Job");
    }
    ```

1. Na koniec należy dodać następujące wiersze toohello hello **Main** metody:

    ```csharp
    jobClient = JobClient.CreateFromConnectionString(connString);

    string methodJobId = Guid.NewGuid().ToString();

    StartMethodJob(methodJobId);
    MonitorJob(methodJobId).Wait();
    Console.WriteLine("Press ENTER toorun hello next job.");
    Console.ReadLine();

    string twinUpdateJobId = Guid.NewGuid().ToString();

    StartTwinUpdateJob(twinUpdateJobId);
    MonitorJob(twinUpdateJobId).Wait();
    Console.WriteLine("Press ENTER tooexit.");
    Console.ReadLine();
    ```

1. W Eksploratorze rozwiązań hello, otwórz hello **projektów startowych ustawić...**  i upewnij się, że hello **akcji** dla **ScheduleJob** projekt jest **Start**. Utworzenie rozwiązania hello.

## <a name="create-a-simulated-device-app"></a>Tworzenie aplikacji symulowanego urządzenia

W tej sekcji utworzysz aplikację konsoli Node.js, która odpowiada tooa metoda bezpośrednia wywoływane przez hello chmury, co jest wyzwalane symulowane urządzenie ponowne uruchomienie komputera i zgłosił hello używa właściwości tooenable urządzeń dwie zapytania tooidentify urządzenia, a podczas ich ostatniego ponownego uruchomienia.

1. Utwórz nowy, pusty folder o nazwie **simDevice**.  W hello **simDevice** folderu, Utwórz plik package.json za pomocą hello następujące polecenie z wiersza polecenia.  Zaakceptuj wszystkie domyślne hello:

    ```cmd/sh
    npm init
    ```

1. Z wiersza polecenia w hello **simDevice** folderu, uruchom następujące polecenie tooinstall hello hello **azure iot urządzenia** i **azure-iot urządzenie mqtt** pakiety:

    ```cmd/sh
    npm install azure-iot-device azure-iot-device-mqtt --save
    ```

1. Za pomocą edytora tekstu, Utwórz nową **simDevice.js** pliku w hello **simDevice** folderu.

1. Dodaj następujące hello "Wymagaj" instrukcje na początku hello hello **simDevice.js** pliku:

    ```nodejs
    'use strict';
   
    var Client = require('azure-iot-device').Client;
    var Protocol = require('azure-iot-device-mqtt').Mqtt;
    ```

1. Dodaj **connectionString** zmiennej i korzystać z niego toocreate **klienta** wystąpienia. Należy symbole zastępcze hello tooreplace się z Instalatorem tooyour odpowiednie wartości.

    ```nodejs
    var connectionString = 'HostName={youriothostname};DeviceId={yourdeviceid};SharedAccessKey={yourdevicekey}';
    var client = Client.fromConnectionString(connectionString, Protocol);
    ```

1. Dodaj powitania po hello toohandle funkcja **lockDoor** metody.

    ```nodejs
    var onLockDoor = function(request, response) {
   
        // Respond hello cloud app for hello direct method
        response.send(200, function(err) {
            if (!err) {
                console.error('An error occured when sending a method response:\n' + err.toString());
            } else {
                console.log('Response toomethod \'' + request.methodName + '\' sent successfully.');
            }
        });
   
        console.log('Locking Door!');
    };
    ```

1. Dodaj następującego kodu tooregister hello obsługę hello hello **lockDoor** metody.

    ```nodejs
    client.open(function(err) {
        if (err) {
            console.error('Could not connect tooIotHub client.');
        }  else {
            console.log('Client connected tooIoT Hub.  Waiting for lockDoor direct method.');
            client.onDeviceMethod('lockDoor', onLockDoor);
        }
    });
    ```

1. Zapisz i zamknij hello **simDevice.js** pliku.

> [!NOTE]
> rzeczy tookeep proste, w tym samouczku nie implementuje wszystkie zasady ponawiania. W kodzie produkcyjnym, należy zaimplementować zasady ponawiania (na przykład wykładniczego wycofywania), zgodnie z sugestią podaną w artykuł w witrynie MSDN hello [obsługi błędów przejściowych][lnk-transient-faults].

## <a name="run-hello-apps"></a>Uruchamianie aplikacji hello

Wszystko jest teraz gotowy toorun hello aplikacji.

1. W wierszu polecenia hello w hello **simDevice** folderu Uruchom hello następujące polecenia toobegin nasłuchiwanie metoda bezpośrednia hello ponowny rozruch.

    ```cmd/sh
    node simDevice.js
    ```

1. Aplikacja konsoli uruchamiania hello C# **ScheduleJob** klikając prawym przyciskiem myszy na powitania **ScheduleJob** projektu, wybierając **debugowania** i **Start nowe wystąpienie**.

1. Zostanie wyświetlony hello wyjście z urządzeń i aplikacji zaplecza.

    ![Uruchamianie aplikacji hello tooschedule zadań][img-schedulejobs]

## <a name="next-steps"></a>Następne kroki

W tym samouczku użyto zadania tooschedule urządzenia tooa metoda bezpośrednia i aktualizacji hello hello urządzenia dwie właściwości.

wprowadzenie do korzystania z Centrum IoT i urządzeniami wzorców zarządzania, takich jak zdalnego za pośrednictwem aktualizacji oprogramowania układowego lotniczego hello odczytu toocontinue [samouczek: jak toodo oprogramowanie układowe zaktualizować][lnk-fwupdate].

Zobacz toocontinue wprowadzenie do korzystania z Centrum IoT [wprowadzenie krawędzi IoT][lnk-iot-edge].

<!-- images -->
[img-servicenuget]: media/iot-hub-csharp-node-schedule-jobs/servicesdknuget.png
[img-createapp]: media/iot-hub-csharp-node-schedule-jobs/createnetapp.png
[img-schedulejobs]: media/iot-hub-csharp-node-schedule-jobs/schedulejobs.png

[lnk-get-started-twin]: iot-hub-node-node-twin-getstarted.md
[lnk-twin-props]: iot-hub-node-node-twin-how-to-configure.md
[lnk-c2d-methods]: iot-hub-node-node-direct-methods.md
[lnk-dev-methods]: iot-hub-devguide-direct-methods.md
[lnk-fwupdate]: iot-hub-node-node-firmware-update.md
[lnk-iot-edge]: iot-hub-linux-iot-edge-get-started.md
[lnk-dev-setup]: https://github.com/Azure/azure-iot-sdk-node/blob/master/doc/node-devbox-setup.md
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[lnk-transient-faults]: https://msdn.microsoft.com/library/hh680901(v=pandp.50).aspx
[lnk-nuget-service-sdk]: https://www.nuget.org/packages/Microsoft.Azure.Devices/
