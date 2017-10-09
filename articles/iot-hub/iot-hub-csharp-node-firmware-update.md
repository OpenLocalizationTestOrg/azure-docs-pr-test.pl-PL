---
title: "Aktualizacja oprogramowania układowego aaaDevice z Centrum IoT Azure (.NET/węzła) | Dokumentacja firmy Microsoft"
description: "Jak zaktualizować toouse zarządzania urządzeniami w usłudze Azure IoT Hub tooinitiate oprogramowanie układowe urządzenia. Możesz użyć urządzenia Azure IoT hello zestawu SDK dla środowiska Node.js tooimplement aplikacji symulowane urządzenie i hello Azure IoT usługi SDK dla platformy .NET tooimplement aplikacji usługi, która wyzwala aktualizacji oprogramowania układowego hello."
services: iot-hub
documentationcenter: .net
author: juanjperez
manager: timlt
editor: 
ms.assetid: 70b84258-bc9f-43b1-b7cf-de1bb715f2cf
ms.service: iot-hub
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/17/2017
ms.author: juanpere
ms.openlocfilehash: d48899651bcd5d67e577c971be0f9453c8f21592
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="use-device-management-tooinitiate-a-device-firmware-update-netnode"></a>Użyj tooinitiate zarządzania urządzenia aktualizacji oprogramowania układowego urządzenia (.NET/węzeł)
[!INCLUDE [iot-hub-selector-firmware-update](../../includes/iot-hub-selector-firmware-update.md)]

## <a name="introduction"></a>Wprowadzenie
W hello [wprowadzenie do zarządzania urządzeniami] [ lnk-dm-getstarted] samouczku przedstawiono sposób toouse hello [dwie urządzenia] [ lnk-devtwin] i [bezpośredniego metody] [ lnk-c2dmethod] tooremotely podstawowych ponownego uruchamiania urządzenia. Ten samouczek używa hello tego samego Centrum IoT elementów podstawowych i pokazuje, jak toodo end-to-end symulowane aktualizacji oprogramowania układowego.  Ten wzorzec jest używany podczas wdrażania aktualizacji oprogramowania układowego powitania dla hello [Pi malina urządzenia implementacji próbki][lnk-rpi-implementation].

Ten samouczek przedstawia sposób wykonania następujących czynności:

* Tworzenie aplikacji konsoli .NET, który wywołuje metodę bezpośredniego firmwareUpdate hello w hello symulowane urządzenie aplikacji za pośrednictwem Centrum IoT.
* Tworzenie aplikacji symulowane urządzenie, który implementuje **firmwareUpdate** metoda bezpośrednia. Ta metoda inicjuje procesem wieloetapowym, która oczekuje toodownload hello oprogramowania układowego obrazu, pobierze obraz oprogramowania układowego hello i finally stosuje hello oprogramowania układowego obrazu. Podczas każdego etapu aktualizacji hello hello urządzenie używa hello zgłoszony tooreport właściwości w toku.

Na końcu hello tego samouczka masz aplikację Node.js konsoli urządzenia i zaplecza aplikacji konsoli .NET (C#):

**dmpatterns_fwupdate_service.js**, która wywołuje metodę bezpośrednio w aplikacji hello symulowane urządzenie Wyświetla hello odpowiedzi i okresowo (co 500 MS.) hello wyświetla zaktualizowane zgłoszone właściwości.

**TriggerFWUpdate**, o tożsamości urządzenia hello utworzony wcześniej, który łączy Centrum IoT tooyour odbiera firmwareUpdate metoda bezpośrednia, jest uruchamiany za pośrednictwem toosimulate wielu stanu procesu aktualizacji oprogramowania układowego łącznie: Oczekiwanie na powitania pobrania obrazu, Trwa pobieranie hello nowy obraz, a na koniec stosowania obrazu hello.

toocomplete tego samouczka należy hello następujące:

* Program Visual Studio 2015 lub Visual Studio 2017.
* Środowisko node.js w wersji 0.12.x lub nowszym <br/>  [Przygotowywanie środowiska projektowego] [ lnk-dev-setup] w tym artykule opisano sposób tooinstall Node.js, w tym samouczku w systemie Windows lub Linux.
* Aktywne konto platformy Azure. (Jeśli go nie masz, możesz utworzyć [bezpłatne konto próbne][lnk-free-trial] w zaledwie kilka minut).

Wykonaj hello [wprowadzenie do zarządzania urządzeniami](iot-hub-csharp-node-device-management-get-started.md) artykułu toocreate Centrum IoT i pobrać parametry połączenia Centrum IoT.

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity](../../includes/iot-hub-get-started-create-device-identity.md)]

## <a name="trigger-a-remote-firmware-update-on-hello-device-using-a-direct-method"></a>Wyzwalanie aktualizacji oprogramowania układowego zdalnego na urządzeniu hello za pomocą bezpośrednich — metoda
W tej sekcji służy do tworzenia aplikacji konsoli .NET (przy użyciu języka C#) inicjującym aktualizacji oprogramowania układowego zdalnego na urządzeniu. Aplikacja Hello korzysta z aktualizacją hello tooinitiate metoda bezpośrednia i używa urządzenia dwie zapytania tooperiodically Pobierz hello stan aktualizacji oprogramowania układowego active hello.

1. W programie Visual Studio, należy dodać bieżącego rozwiązania toohello projektu Visual C# pulpitu systemu Windows klasycznego przy użyciu hello **aplikacji konsoli** szablonu projektu. Nazwa projektu hello **TriggerFWUpdate**.

    ![Nowy projekt Visual C# Windows Classic Desktop][img-createapp]

1. W Eksploratorze rozwiązań kliknij prawym przyciskiem myszy hello **TriggerFWUpdate** projektu, a następnie kliknij przycisk **Zarządzaj pakietami NuGet...** .
1. W hello **Menedżera pakietów NuGet** wybierz **Przeglądaj**, wyszukaj **microsoft.azure.devices**, wybierz pozycję **zainstalować** tooinstall Witaj **Microsoft.Azure.Devices** pakietu i zaakceptuj warunki użytkowania hello. Ta procedura pliki do pobrania, instaluje i dodaje toohello odwołanie [zestawu SDK usług Azure IoT] [ lnk-nuget-service-sdk] NuGet pakiet i jego zależności.

    ![Okno Menedżera pakietów NuGet][img-servicenuget]
1. Dodaj następujące hello `using` instrukcji u góry hello hello **Program.cs** pliku:
   
        using Microsoft.Azure.Devices;
        using Microsoft.Azure.Devices.Shared;
        
1. Dodaj następujące pola toohello hello **Program** klasy. Zastąp hello wielu symbole zastępcze hello Centrum IoT ciąg połączenia dla koncentratora hello, który został utworzony w poprzedniej sekcji hello i hello identyfikator urządzenia.
   
        static RegistryManager registryManager;
        static string connString = "{iot hub connection string}";
        static ServiceClient client;
        static JobClient jobClient;
        static string targetDevice = "{deviceIdForTargetDevice}";
        
1. Dodaj następujące metody toohello hello **Program** klasy:
   
        public static async Task QueryTwinFWUpdateReported()
        {
            Twin twin = await registryManager.GetTwinAsync(targetDevice);
            Console.WriteLine(twin.Properties.Reported.ToJson());
        }
        
1. Dodaj następujące metody toohello hello **Program** klasy:

        public static async Task StartFirmwareUpdate()
        {
            client = ServiceClient.CreateFromConnectionString(connString);
            CloudToDeviceMethod method = new CloudToDeviceMethod("firmwareUpdate");
            method.ResponseTimeout = TimeSpan.FromSeconds(30);
            method.SetPayloadJson(
                @"{
                    fwPackageUri : 'https://someurl'
                }");

            CloudToDeviceMethodResult result = await client.InvokeDeviceMethodAsync(targetDevice, method);

            Console.WriteLine("Invoked firmware update on device.");
        }

1. Na koniec należy dodać następujące wiersze toohello hello **Main** metody:
   
        registryManager = RegistryManager.CreateFromConnectionString(connString);
        StartFirmwareUpdate().Wait();
        QueryTwinFWUpdateReported().Wait();
        Console.WriteLine("Press ENTER tooexit.");
        Console.ReadLine();
        
1. W Eksploratorze rozwiązań hello, otwórz hello **projektów startowych ustawić...**  i upewnij się, że hello **akcji** dla **TriggerFWUpdate** projekt jest **Start**.

1. Utworzenie rozwiązania hello.

[!INCLUDE [iot-hub-device-firmware-update](../../includes/iot-hub-device-firmware-update.md)]

## <a name="run-hello-apps"></a>Uruchamianie aplikacji hello
Wszystko jest teraz gotowy toorun hello aplikacji.

1. W wierszu polecenia hello w hello **manageddevice** folderu Uruchom hello następujące polecenia toobegin nasłuchiwanie metoda bezpośrednia hello ponowny rozruch.
   
    ```
    node dmpatterns_fwupdate_device.js
    ```
2. W programie Visual Studio, kliknij prawym przyciskiem myszy hello **TriggerFWUpdate** projectRun toohello C# aplikacji konsoli, wybierz opcję **debugowania** i **Start nowe wystąpienie**.

3. Zostanie wyświetlony hello urządzenia odpowiedzi toohello metoda bezpośrednia hello konsoli.

    ![Pomyślnie zaktualizowano oprogramowania układowego][img-fwupdate]

## <a name="next-steps"></a>Następne kroki
W tym samouczku używana metoda bezpośrednia tootrigger zdalnej aktualizacji oprogramowania układowego na urządzeniach i hello używany zgłaszane postęp hello toofollow właściwości aktualizacji oprogramowania układowego hello.

toolearn tooextend IoT metody rozwiązania i harmonogram wywołuje na wielu urządzeniach, zobacz hello [emisji zadania i harmonogramu] [ lnk-tutorial-jobs] samouczka.

<!-- images -->
[img-servicenuget]: media/iot-hub-csharp-node-firmware-update/servicesdknuget.png
[img-createapp]: media/iot-hub-csharp-node-firmware-update/createnetapp.png
[img-fwupdate]: media/iot-hub-csharp-node-firmware-update/fwupdated.png

[lnk-devtwin]: iot-hub-devguide-device-twins.md
[lnk-c2dmethod]: iot-hub-devguide-direct-methods.md
[lnk-dm-getstarted]: iot-hub-node-node-device-management-get-started.md
[lnk-tutorial-jobs]: iot-hub-node-node-schedule-jobs.md

[lnk-dev-setup]: https://github.com/Azure/azure-iot-sdk-node/blob/master/doc/node-devbox-setup.md
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[lnk-transient-faults]: https://msdn.microsoft.com/library/hh680901(v=pandp.50).aspx
[lnk-rpi-implementation]: https://github.com/Azure/azure-iot-sdk-c/tree/master/iothub_client/samples/iothub_client_sample_mqtt_dm/pi_device
[lnk-nuget-service-sdk]: https://www.nuget.org/packages/Microsoft.Azure.Devices/