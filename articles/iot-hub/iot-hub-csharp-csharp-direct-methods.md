---
title: "Centrum IoT Azure aaaUse bezpośrednie metod (.NET/.NET) | Dokumentacja firmy Microsoft"
description: "Jak toouse Centrum IoT Azure bezpośrednie metody. .NET tooimplement aplikacji symulowane urządzenie, która obejmuje metoda bezpośrednia i hello zestawu SDK usług Azure IoT dla tooimplement .NET usługi aplikacji, która wywołuje metodę bezpośredniego hello są używane urządzenia Azure IoT hello zestawu SDK."
services: iot-hub
documentationcenter: 
author: dsk-2015
manager: timlt
editor: 
ms.assetid: ab035b8e-bff8-4e12-9536-f31d6b6fe425
ms.service: iot-hub
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/18/2017
ms.author: dkshir
ms.openlocfilehash: d4fa093a99558ec6faf294c2583a14a722b9ac03
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="use-direct-methods-netnet"></a>Użyj metody bezpośredniego (.NET/.NET)
[!INCLUDE [iot-hub-selector-c2d-methods](../../includes/iot-hub-selector-c2d-methods.md)]

W tym samouczku są nam będzie toodevelop dwóch aplikacji konsoli .NET:

* **CallMethodOnDevice**, aplikacji wewnętrznych, która wywołuje metodę w aplikacji symulowane urządzenie hello i wyświetla hello odpowiedzi.
* **SimulateDeviceMethods**, aplikacji konsoli, która symuluje urządzenie łączące Centrum IoT tooyour z tożsamości urządzenia hello utworzony wcześniej i odpowiada toohello metody wywoływane przez hello chmury.

> [!NOTE]
> Artykuł Hello [Azure IoT SDK] [ lnk-hub-sdks] zawiera informacje o hello Azure IoT SDK, której można toobuild toorun zarówno aplikacje na urządzeniach i z zaplecza rozwiązania.
> 
> 

toocomplete tego samouczka należy:

* Program Visual Studio 2015 lub Visual Studio 2017.
* Aktywne konto platformy Azure. (Jeśli go nie masz, możesz utworzyć [bezpłatne konto próbne][lnk-free-trial] w zaledwie kilka minut).

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity-portal](../../includes/iot-hub-get-started-create-device-identity-portal.md)]

Chcąc tożsamości urządzenia hello toocreate programowo zamiast tego, przeczytaj hello odpowiedniej sekcji w hello [połączenia Centrum IoT tooyour symulowane urządzenie przy użyciu platformy .NET] [ lnk-device-identity-csharp] artykułu.


## <a name="create-a-simulated-device-app"></a>Tworzenie aplikacji symulowanego urządzenia
W tej sekcji służy do tworzenia aplikacji konsoli .NET, które odpowiada metoda tooa wywoływane przez rozwiązania hello zakończenia.

1. W programie Visual Studio, należy dodać bieżącego rozwiązania toohello projektu Visual C# pulpitu systemu Windows klasycznego przy użyciu hello **aplikacji konsoli** szablonu projektu. Nazwa projektu hello **SimulateDeviceMethods**.
   
    ![Nowa aplikacja Visual C# Windows Classic urządzenia][img-createdeviceapp]
    
1. W Eksploratorze rozwiązań kliknij prawym przyciskiem myszy hello **SimulateDeviceMethods** projektu, a następnie kliknij przycisk **Zarządzaj pakietami NuGet...** .
1. W hello **Menedżera pakietów NuGet** wybierz **Przeglądaj** i wyszukaj **microsoft.azure.devices.client**. Wybierz **zainstalować** tooinstall hello **Microsoft.Azure.Devices.Client** pakietu i zaakceptuj warunki użytkowania hello. Ta procedura pliki do pobrania, instaluje i dodaje toohello odwołanie [urządzenia Azure IoT SDK] [ lnk-nuget-client-sdk] NuGet pakiet i jego zależności.
   
    ![Aplikacja kliencka okna Menedżera pakietów NuGet][img-clientnuget]
1. Dodaj następujące hello `using` instrukcji u góry hello hello **Program.cs** pliku:
   
        using Microsoft.Azure.Devices.Client;
        using Microsoft.Azure.Devices.Shared;

1. Dodaj następujące pola toohello hello **Program** klasy. Zastąp wartość symbolu zastępczego hello ciąg połączenia urządzenia hello zanotowanym w poprzedniej sekcji hello.
   
        static string DeviceConnectionString = "HostName=<yourIotHubName>.azure-devices.net;DeviceId=<yourIotDeviceName>;SharedAccessKey=<yourIotDeviceAccessKey>";
        static DeviceClient Client = null;

1. Dodaj następujące metoda bezpośrednia hello tooimplement na urządzeniu hello hello:

        static Task<MethodResponse> WriteLineToConsole(MethodRequest methodRequest, object userContext)
        {
            Console.WriteLine();
            Console.WriteLine("\t{0}", methodRequest.DataAsJson);
            Console.WriteLine("\nReturning response for method {0}", methodRequest.Name);

            string result = "'Input was written toolog.'";
            return Task.FromResult(new MethodResponse(Encoding.UTF8.GetBytes(result), 200));
        }

1. Na koniec należy dodać hello następującego kodu toohello **Main** — metoda tooopen hello połączenia tooyour IoT hub i zainicjować hello metody odbiornika:
   
        try
        {
            Console.WriteLine("Connecting toohub");
            Client = DeviceClient.CreateFromConnectionString(DeviceConnectionString, TransportType.Mqtt);

            // setup callback for "writeLine" method
            Client.SetMethodHandlerAsync("writeLine", WriteLineToConsole, null).Wait();
            Console.WriteLine("Waiting for direct method call\n Press enter tooexit.");
            Console.ReadLine();

            Console.WriteLine("Exiting...");

            // as a good practice, remove hello "writeLine" handler
            Client.SetMethodHandlerAsync("writeLine", null, null).Wait();
            Client.CloseAsync().Wait();
        }
        catch (Exception ex)
        {
            Console.WriteLine();
            Console.WriteLine("Error in sample: {0}", ex.Message);
        }
        
1. W hello Visual Studio Solution Explorer, kliknij prawym przyciskiem myszy rozwiązanie, a następnie kliknij przycisk **Ustaw projekty startowe...** . Wybierz **jednego projektu startowego**, a następnie wybierz hello **SimulateDeviceMethods** projektu w menu rozwijanym hello.        

> [!NOTE]
> rzeczy tookeep proste, w tym samouczku nie implementuje wszystkie zasady ponawiania. W kodzie produkcyjnym, należy zaimplementować zasady ponawiania (np. Ponów próbę połączenia), zgodnie z sugestią podaną w artykuł w witrynie MSDN hello [obsługi błędów przejściowych][lnk-transient-faults].
> 
> 

## <a name="call-a-direct-method-on-a-device"></a>Wywołanie metody bezpośrednio na urządzeniu
W tej sekcji służy do tworzenia aplikacji konsoli .NET, która wywołuje metodę hello symulowane urządzenie aplikacji, a następnie wyświetla hello odpowiedzi.

1. W programie Visual Studio, należy dodać bieżącego rozwiązania toohello projektu Visual C# pulpitu systemu Windows klasycznego przy użyciu hello **aplikacji konsoli** szablonu projektu. Upewnij się, że wersja platformy .NET hello jest 4.5.1 lub nowszej. Nazwa projektu hello **CallMethodOnDevice**.
   
    ![Nowy projekt Visual C# Windows Classic Desktop][img-createserviceapp]
2. W Eksploratorze rozwiązań kliknij prawym przyciskiem myszy hello **CallMethodOnDevice** projektu, a następnie kliknij przycisk **Zarządzaj pakietami NuGet...** .
3. W hello **Menedżera pakietów NuGet** wybierz **Przeglądaj**, wyszukaj **microsoft.azure.devices**, wybierz pozycję **zainstalować** tooinstall Witaj **Microsoft.Azure.Devices** pakietu i zaakceptuj warunki użytkowania hello. Ta procedura pliki do pobrania, instaluje i dodaje toohello odwołanie [zestawu SDK usług Azure IoT] [ lnk-nuget-service-sdk] NuGet pakiet i jego zależności.
   
    ![Okno Menedżera pakietów NuGet][img-servicenuget]

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

1. W hello Visual Studio Solution Explorer, kliknij prawym przyciskiem myszy rozwiązanie, a następnie kliknij przycisk **Ustaw projekty startowe...** . Wybierz **jednego projektu startowego**, a następnie wybierz hello **CallMethodOnDevice** projektu w menu rozwijanym hello.

## <a name="run-hello-applications"></a>Uruchamianie aplikacji hello
Wszystko jest teraz gotowy toorun hello aplikacji.

1. Uruchamianie aplikacji urządzenia .NET hello **SimulateDeviceMethods**. Należy uruchomić, nasłuchiwania dla wywołań metod z Centrum IoT: 

    ![Uruchom aplikację urządzenia][img-deviceapprun]
1. Teraz urządzenia hello jest połączony i Oczekiwanie na wywołania metody, uruchom hello .NET **CallMethodOnDevice** metody hello tooinvoke aplikacji hello symulowane urządzenie aplikacji. Powinna zostać wyświetlona odpowiedź urządzenia hello napisana hello konsoli.
   
    ![Uruchom aplikację usługi][img-serviceapprun]
1. urządzenie Hello następnie reaguje metody toohello wydrukowanie tej wiadomości:
   
    ![Metoda bezpośrednia wywoływane na urządzeniu hello][img-directmethodinvoked]

## <a name="next-steps"></a>Następne kroki
W tym samouczku został skonfigurowany nowego centrum IoT w portalu Azure hello i w rejestrze tożsamości Centrum IoT hello zostanie utworzona tożsamość urządzenia. Użyto tego urządzenia tożsamości tooenable hello symulowane urządzenie aplikacji tooreact toomethods wywołana przez hello chmury. Utworzono aplikację, która wywołuje metody na urządzeniu hello i wyświetla hello odpowiedzi z hello urządzenia. 

toocontinue wprowadzenie do korzystania z Centrum IoT i tooexplore innych scenariuszach IoT, zobacz:

* [Rozpoczynanie pracy z Centrum IoT]
* [Planowanie zadań na wielu urządzeniach][lnk-devguide-jobs]

toolearn tooextend IoT metody rozwiązania i harmonogram wywołuje na wielu urządzeniach, zobacz hello [emisji zadania i harmonogramu] [ lnk-tutorial-jobs] samouczka.

<!-- Images. -->
[img-createdeviceapp]: ./media/iot-hub-csharp-csharp-direct-methods/create-device-app.png
[img-clientnuget]: ./media/iot-hub-csharp-csharp-direct-methods/device-app-nuget.png
[img-createserviceapp]: ./media/iot-hub-csharp-csharp-direct-methods/create-service-app.png
[img-servicenuget]: ./media/iot-hub-csharp-csharp-direct-methods/service-app-nuget.png
[img-deviceapprun]: ./media/iot-hub-csharp-csharp-direct-methods/run-device-app.png
[img-serviceapprun]: ./media/iot-hub-csharp-csharp-direct-methods/run-service-app.png
[img-directmethodinvoked]: ./media/iot-hub-csharp-csharp-direct-methods/direct-method-invoked.png

<!-- Links -->
[lnk-transient-faults]: https://msdn.microsoft.com/library/hh680901(v=pandp.50).aspx

[lnk-hub-sdks]: iot-hub-devguide-sdks.md
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[lnk-nuget-client-sdk]: https://www.nuget.org/packages/Microsoft.Azure.Devices.Client/
[lnk-nuget-service-sdk]: https://www.nuget.org/packages/Microsoft.Azure.Devices/

[lnk-device-identity-csharp]: iot-hub-csharp-csharp-getstarted.md#DeviceIdentity_csharp

[lnk-devguide-jobs]: iot-hub-devguide-jobs.md
[lnk-tutorial-jobs]: iot-hub-node-node-schedule-jobs.md

[Rozpoczynanie pracy z Centrum IoT]: iot-hub-node-node-getstarted.md
