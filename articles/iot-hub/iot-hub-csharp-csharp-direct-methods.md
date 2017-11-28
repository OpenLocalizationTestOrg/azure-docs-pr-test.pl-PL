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
# <a name="use-direct-methods-netnet"></a><span data-ttu-id="13b31-104">Użyj metody bezpośredniego (.NET/.NET)</span><span class="sxs-lookup"><span data-stu-id="13b31-104">Use direct methods (.NET/.NET)</span></span>
[!INCLUDE [iot-hub-selector-c2d-methods](../../includes/iot-hub-selector-c2d-methods.md)]

<span data-ttu-id="13b31-105">W tym samouczku są nam będzie toodevelop dwóch aplikacji konsoli .NET:</span><span class="sxs-lookup"><span data-stu-id="13b31-105">In this tutorial, we are going toodevelop two .NET console apps:</span></span>

* <span data-ttu-id="13b31-106">**CallMethodOnDevice**, aplikacji wewnętrznych, która wywołuje metodę w aplikacji symulowane urządzenie hello i wyświetla hello odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="13b31-106">**CallMethodOnDevice**, a back-end app, which calls a method in hello simulated device app and displays hello response.</span></span>
* <span data-ttu-id="13b31-107">**SimulateDeviceMethods**, aplikacji konsoli, która symuluje urządzenie łączące Centrum IoT tooyour z tożsamości urządzenia hello utworzony wcześniej i odpowiada toohello metody wywoływane przez hello chmury.</span><span class="sxs-lookup"><span data-stu-id="13b31-107">**SimulateDeviceMethods**, a console app which simulates a device connecting tooyour IoT hub with hello device identity created earlier, and responds toohello method called by hello cloud.</span></span>

> [!NOTE]
> <span data-ttu-id="13b31-108">Artykuł Hello [Azure IoT SDK] [ lnk-hub-sdks] zawiera informacje o hello Azure IoT SDK, której można toobuild toorun zarówno aplikacje na urządzeniach i z zaplecza rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="13b31-108">hello article [Azure IoT SDKs][lnk-hub-sdks] provides information about hello Azure IoT SDKs that you can use toobuild both applications toorun on devices and your solution back end.</span></span>
> 
> 

<span data-ttu-id="13b31-109">toocomplete tego samouczka należy:</span><span class="sxs-lookup"><span data-stu-id="13b31-109">toocomplete this tutorial, you need:</span></span>

* <span data-ttu-id="13b31-110">Program Visual Studio 2015 lub Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="13b31-110">Visual Studio 2015 or Visual Studio 2017.</span></span>
* <span data-ttu-id="13b31-111">Aktywne konto platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="13b31-111">An active Azure account.</span></span> <span data-ttu-id="13b31-112">(Jeśli go nie masz, możesz utworzyć [bezpłatne konto próbne][lnk-free-trial] w zaledwie kilka minut).</span><span class="sxs-lookup"><span data-stu-id="13b31-112">(If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.)</span></span>

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity-portal](../../includes/iot-hub-get-started-create-device-identity-portal.md)]

<span data-ttu-id="13b31-113">Chcąc tożsamości urządzenia hello toocreate programowo zamiast tego, przeczytaj hello odpowiedniej sekcji w hello [połączenia Centrum IoT tooyour symulowane urządzenie przy użyciu platformy .NET] [ lnk-device-identity-csharp] artykułu.</span><span class="sxs-lookup"><span data-stu-id="13b31-113">If you want toocreate hello device identity programmatically instead, read hello corresponding section in hello [Connect your simulated device tooyour IoT hub using .NET][lnk-device-identity-csharp] article.</span></span>


## <a name="create-a-simulated-device-app"></a><span data-ttu-id="13b31-114">Tworzenie aplikacji symulowanego urządzenia</span><span class="sxs-lookup"><span data-stu-id="13b31-114">Create a simulated device app</span></span>
<span data-ttu-id="13b31-115">W tej sekcji służy do tworzenia aplikacji konsoli .NET, które odpowiada metoda tooa wywoływane przez rozwiązania hello zakończenia.</span><span class="sxs-lookup"><span data-stu-id="13b31-115">In this section, you create a .NET console app that responds tooa method called by hello solution back end.</span></span>

1. <span data-ttu-id="13b31-116">W programie Visual Studio, należy dodać bieżącego rozwiązania toohello projektu Visual C# pulpitu systemu Windows klasycznego przy użyciu hello **aplikacji konsoli** szablonu projektu.</span><span class="sxs-lookup"><span data-stu-id="13b31-116">In Visual Studio, add a Visual C# Windows Classic Desktop project toohello current solution by using hello **Console Application** project template.</span></span> <span data-ttu-id="13b31-117">Nazwa projektu hello **SimulateDeviceMethods**.</span><span class="sxs-lookup"><span data-stu-id="13b31-117">Name hello project **SimulateDeviceMethods**.</span></span>
   
    ![Nowa aplikacja Visual C# Windows Classic urządzenia][img-createdeviceapp]
    
1. <span data-ttu-id="13b31-119">W Eksploratorze rozwiązań kliknij prawym przyciskiem myszy hello **SimulateDeviceMethods** projektu, a następnie kliknij przycisk **Zarządzaj pakietami NuGet...** .</span><span class="sxs-lookup"><span data-stu-id="13b31-119">In Solution Explorer, right-click hello **SimulateDeviceMethods** project, and then click **Manage NuGet Packages...**.</span></span>
1. <span data-ttu-id="13b31-120">W hello **Menedżera pakietów NuGet** wybierz **Przeglądaj** i wyszukaj **microsoft.azure.devices.client**.</span><span class="sxs-lookup"><span data-stu-id="13b31-120">In hello **NuGet Package Manager** window, select **Browse** and search for **microsoft.azure.devices.client**.</span></span> <span data-ttu-id="13b31-121">Wybierz **zainstalować** tooinstall hello **Microsoft.Azure.Devices.Client** pakietu i zaakceptuj warunki użytkowania hello.</span><span class="sxs-lookup"><span data-stu-id="13b31-121">Select **Install** tooinstall hello **Microsoft.Azure.Devices.Client** package, and accept hello terms of use.</span></span> <span data-ttu-id="13b31-122">Ta procedura pliki do pobrania, instaluje i dodaje toohello odwołanie [urządzenia Azure IoT SDK] [ lnk-nuget-client-sdk] NuGet pakiet i jego zależności.</span><span class="sxs-lookup"><span data-stu-id="13b31-122">This procedure downloads, installs, and adds a reference toohello [Azure IoT device SDK][lnk-nuget-client-sdk] NuGet package and its dependencies.</span></span>
   
    ![Aplikacja kliencka okna Menedżera pakietów NuGet][img-clientnuget]
1. <span data-ttu-id="13b31-124">Dodaj następujące hello `using` instrukcji u góry hello hello **Program.cs** pliku:</span><span class="sxs-lookup"><span data-stu-id="13b31-124">Add hello following `using` statements at hello top of hello **Program.cs** file:</span></span>
   
        using Microsoft.Azure.Devices.Client;
        using Microsoft.Azure.Devices.Shared;

1. <span data-ttu-id="13b31-125">Dodaj następujące pola toohello hello **Program** klasy.</span><span class="sxs-lookup"><span data-stu-id="13b31-125">Add hello following fields toohello **Program** class.</span></span> <span data-ttu-id="13b31-126">Zastąp wartość symbolu zastępczego hello ciąg połączenia urządzenia hello zanotowanym w poprzedniej sekcji hello.</span><span class="sxs-lookup"><span data-stu-id="13b31-126">Replace hello placeholder value with hello device connection string that you noted in hello previous section.</span></span>
   
        static string DeviceConnectionString = "HostName=<yourIotHubName>.azure-devices.net;DeviceId=<yourIotDeviceName>;SharedAccessKey=<yourIotDeviceAccessKey>";
        static DeviceClient Client = null;

1. <span data-ttu-id="13b31-127">Dodaj następujące metoda bezpośrednia hello tooimplement na urządzeniu hello hello:</span><span class="sxs-lookup"><span data-stu-id="13b31-127">Add hello following tooimplement hello direct method on hello device:</span></span>

        static Task<MethodResponse> WriteLineToConsole(MethodRequest methodRequest, object userContext)
        {
            Console.WriteLine();
            Console.WriteLine("\t{0}", methodRequest.DataAsJson);
            Console.WriteLine("\nReturning response for method {0}", methodRequest.Name);

            string result = "'Input was written toolog.'";
            return Task.FromResult(new MethodResponse(Encoding.UTF8.GetBytes(result), 200));
        }

1. <span data-ttu-id="13b31-128">Na koniec należy dodać hello następującego kodu toohello **Main** — metoda tooopen hello połączenia tooyour IoT hub i zainicjować hello metody odbiornika:</span><span class="sxs-lookup"><span data-stu-id="13b31-128">Finally, add hello following code toohello **Main** method tooopen hello connection tooyour IoT hub and initialize hello method listener:</span></span>
   
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
        
1. <span data-ttu-id="13b31-129">W hello Visual Studio Solution Explorer, kliknij prawym przyciskiem myszy rozwiązanie, a następnie kliknij przycisk **Ustaw projekty startowe...** . Wybierz **jednego projektu startowego**, a następnie wybierz hello **SimulateDeviceMethods** projektu w menu rozwijanym hello.</span><span class="sxs-lookup"><span data-stu-id="13b31-129">In hello Visual Studio Solution Explorer, right-click your solution, and then click **Set StartUp Projects...**. Select **Single startup project**, and then select hello **SimulateDeviceMethods** project in hello dropdown menu.</span></span>        

> [!NOTE]
> <span data-ttu-id="13b31-130">rzeczy tookeep proste, w tym samouczku nie implementuje wszystkie zasady ponawiania.</span><span class="sxs-lookup"><span data-stu-id="13b31-130">tookeep things simple, this tutorial does not implement any retry policy.</span></span> <span data-ttu-id="13b31-131">W kodzie produkcyjnym, należy zaimplementować zasady ponawiania (np. Ponów próbę połączenia), zgodnie z sugestią podaną w artykuł w witrynie MSDN hello [obsługi błędów przejściowych][lnk-transient-faults].</span><span class="sxs-lookup"><span data-stu-id="13b31-131">In production code, you should implement retry policies (such as connection retry), as suggested in hello MSDN article [Transient Fault Handling][lnk-transient-faults].</span></span>
> 
> 

## <a name="call-a-direct-method-on-a-device"></a><span data-ttu-id="13b31-132">Wywołanie metody bezpośrednio na urządzeniu</span><span class="sxs-lookup"><span data-stu-id="13b31-132">Call a direct method on a device</span></span>
<span data-ttu-id="13b31-133">W tej sekcji służy do tworzenia aplikacji konsoli .NET, która wywołuje metodę hello symulowane urządzenie aplikacji, a następnie wyświetla hello odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="13b31-133">In this section, you create a .NET console app that calls a method in hello simulated device app and then displays hello response.</span></span>

1. <span data-ttu-id="13b31-134">W programie Visual Studio, należy dodać bieżącego rozwiązania toohello projektu Visual C# pulpitu systemu Windows klasycznego przy użyciu hello **aplikacji konsoli** szablonu projektu.</span><span class="sxs-lookup"><span data-stu-id="13b31-134">In Visual Studio, add a Visual C# Windows Classic Desktop project toohello current solution by using hello **Console Application** project template.</span></span> <span data-ttu-id="13b31-135">Upewnij się, że wersja platformy .NET hello jest 4.5.1 lub nowszej.</span><span class="sxs-lookup"><span data-stu-id="13b31-135">Make sure hello .NET Framework version is 4.5.1 or later.</span></span> <span data-ttu-id="13b31-136">Nazwa projektu hello **CallMethodOnDevice**.</span><span class="sxs-lookup"><span data-stu-id="13b31-136">Name hello project **CallMethodOnDevice**.</span></span>
   
    ![Nowy projekt Visual C# Windows Classic Desktop][img-createserviceapp]
2. <span data-ttu-id="13b31-138">W Eksploratorze rozwiązań kliknij prawym przyciskiem myszy hello **CallMethodOnDevice** projektu, a następnie kliknij przycisk **Zarządzaj pakietami NuGet...** .</span><span class="sxs-lookup"><span data-stu-id="13b31-138">In Solution Explorer, right-click hello **CallMethodOnDevice** project, and then click **Manage NuGet Packages...**.</span></span>
3. <span data-ttu-id="13b31-139">W hello **Menedżera pakietów NuGet** wybierz **Przeglądaj**, wyszukaj **microsoft.azure.devices**, wybierz pozycję **zainstalować** tooinstall Witaj **Microsoft.Azure.Devices** pakietu i zaakceptuj warunki użytkowania hello.</span><span class="sxs-lookup"><span data-stu-id="13b31-139">In hello **NuGet Package Manager** window, select **Browse**, search for **microsoft.azure.devices**, select **Install** tooinstall hello **Microsoft.Azure.Devices** package, and accept hello terms of use.</span></span> <span data-ttu-id="13b31-140">Ta procedura pliki do pobrania, instaluje i dodaje toohello odwołanie [zestawu SDK usług Azure IoT] [ lnk-nuget-service-sdk] NuGet pakiet i jego zależności.</span><span class="sxs-lookup"><span data-stu-id="13b31-140">This procedure downloads, installs, and adds a reference toohello [Azure IoT service SDK][lnk-nuget-service-sdk] NuGet package and its dependencies.</span></span>
   
    ![Okno Menedżera pakietów NuGet][img-servicenuget]

4. <span data-ttu-id="13b31-142">Dodaj następujące hello `using` instrukcji u góry hello hello **Program.cs** pliku:</span><span class="sxs-lookup"><span data-stu-id="13b31-142">Add hello following `using` statements at hello top of hello **Program.cs** file:</span></span>
   
        using System.Threading.Tasks;
        using Microsoft.Azure.Devices;
5. <span data-ttu-id="13b31-143">Dodaj następujące pola toohello hello **Program** klasy.</span><span class="sxs-lookup"><span data-stu-id="13b31-143">Add hello following fields toohello **Program** class.</span></span> <span data-ttu-id="13b31-144">Zastąp wartość symbolu zastępczego hello hello hello koncentratora, który został utworzony w poprzedniej sekcji hello parametry połączenia Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="13b31-144">Replace hello placeholder value with hello IoT Hub connection string for hello hub that you created in hello previous section.</span></span>
   
        static ServiceClient serviceClient;
        static string connectionString = "{iot hub connection string}";
6. <span data-ttu-id="13b31-145">Dodaj następujące metody toohello hello **Program** klasy:</span><span class="sxs-lookup"><span data-stu-id="13b31-145">Add hello following method toohello **Program** class:</span></span>
   
        private static async Task InvokeMethod()
        {
            var methodInvocation = new CloudToDeviceMethod("writeLine") { ResponseTimeout = TimeSpan.FromSeconds(30) };
            methodInvocation.SetPayloadJson("'a line toobe written'");

            var response = await serviceClient.InvokeDeviceMethodAsync("myDeviceId", methodInvocation);

            Console.WriteLine("Response status: {0}, payload:", response.Status);
            Console.WriteLine(response.GetPayloadAsJson());
        }
   
    <span data-ttu-id="13b31-146">Ta metoda wywołuje metodę bezpośredniego o nazwie `writeLine` na powitania `myDeviceId` urządzenia.</span><span class="sxs-lookup"><span data-stu-id="13b31-146">This method invokes a direct method with name `writeLine` on hello `myDeviceId` device.</span></span> <span data-ttu-id="13b31-147">Następnie zapisuje odpowiedź hello udostępniane przez urządzenie hello na powitania konsoli.</span><span class="sxs-lookup"><span data-stu-id="13b31-147">Then, it writes hello response provided by hello device on hello console.</span></span> <span data-ttu-id="13b31-148">Należy zwrócić uwagę, jak to możliwe toospecify wartość limitu czasu dla hello toorespond urządzenia.</span><span class="sxs-lookup"><span data-stu-id="13b31-148">Note how it is possible toospecify a timeout value for hello device toorespond.</span></span>
7. <span data-ttu-id="13b31-149">Na koniec należy dodać następujące wiersze toohello hello **Main** metody:</span><span class="sxs-lookup"><span data-stu-id="13b31-149">Finally, add hello following lines toohello **Main** method:</span></span>
   
        serviceClient = ServiceClient.CreateFromConnectionString(connectionString);
        InvokeMethod().Wait();
        Console.WriteLine("Press Enter tooexit.");
        Console.ReadLine();

1. <span data-ttu-id="13b31-150">W hello Visual Studio Solution Explorer, kliknij prawym przyciskiem myszy rozwiązanie, a następnie kliknij przycisk **Ustaw projekty startowe...** . Wybierz **jednego projektu startowego**, a następnie wybierz hello **CallMethodOnDevice** projektu w menu rozwijanym hello.</span><span class="sxs-lookup"><span data-stu-id="13b31-150">In hello Visual Studio Solution Explorer, right-click your solution, and then click **Set StartUp Projects...**. Select **Single startup project**, and then select hello **CallMethodOnDevice** project in hello dropdown menu.</span></span>

## <a name="run-hello-applications"></a><span data-ttu-id="13b31-151">Uruchamianie aplikacji hello</span><span class="sxs-lookup"><span data-stu-id="13b31-151">Run hello applications</span></span>
<span data-ttu-id="13b31-152">Wszystko jest teraz gotowy toorun hello aplikacji.</span><span class="sxs-lookup"><span data-stu-id="13b31-152">You are now ready toorun hello applications.</span></span>

1. <span data-ttu-id="13b31-153">Uruchamianie aplikacji urządzenia .NET hello **SimulateDeviceMethods**.</span><span class="sxs-lookup"><span data-stu-id="13b31-153">Run hello .NET device app **SimulateDeviceMethods**.</span></span> <span data-ttu-id="13b31-154">Należy uruchomić, nasłuchiwania dla wywołań metod z Centrum IoT:</span><span class="sxs-lookup"><span data-stu-id="13b31-154">It should start listening for method calls from your IoT Hub:</span></span> 

    ![Uruchom aplikację urządzenia][img-deviceapprun]
1. <span data-ttu-id="13b31-156">Teraz urządzenia hello jest połączony i Oczekiwanie na wywołania metody, uruchom hello .NET **CallMethodOnDevice** metody hello tooinvoke aplikacji hello symulowane urządzenie aplikacji.</span><span class="sxs-lookup"><span data-stu-id="13b31-156">Now that hello device is connected and waiting for method invocations, run hello .NET **CallMethodOnDevice** app tooinvoke hello method in hello simulated device app.</span></span> <span data-ttu-id="13b31-157">Powinna zostać wyświetlona odpowiedź urządzenia hello napisana hello konsoli.</span><span class="sxs-lookup"><span data-stu-id="13b31-157">You should see hello device response written in hello console.</span></span>
   
    ![Uruchom aplikację usługi][img-serviceapprun]
1. <span data-ttu-id="13b31-159">urządzenie Hello następnie reaguje metody toohello wydrukowanie tej wiadomości:</span><span class="sxs-lookup"><span data-stu-id="13b31-159">hello device then reacts toohello method by printing this message:</span></span>
   
    ![Metoda bezpośrednia wywoływane na urządzeniu hello][img-directmethodinvoked]

## <a name="next-steps"></a><span data-ttu-id="13b31-161">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="13b31-161">Next steps</span></span>
<span data-ttu-id="13b31-162">W tym samouczku został skonfigurowany nowego centrum IoT w portalu Azure hello i w rejestrze tożsamości Centrum IoT hello zostanie utworzona tożsamość urządzenia.</span><span class="sxs-lookup"><span data-stu-id="13b31-162">In this tutorial, you configured a new IoT hub in hello Azure portal, and then created a device identity in hello IoT hub's identity registry.</span></span> <span data-ttu-id="13b31-163">Użyto tego urządzenia tożsamości tooenable hello symulowane urządzenie aplikacji tooreact toomethods wywołana przez hello chmury.</span><span class="sxs-lookup"><span data-stu-id="13b31-163">You used this device identity tooenable hello simulated device app tooreact toomethods invoked by hello cloud.</span></span> <span data-ttu-id="13b31-164">Utworzono aplikację, która wywołuje metody na urządzeniu hello i wyświetla hello odpowiedzi z hello urządzenia.</span><span class="sxs-lookup"><span data-stu-id="13b31-164">You also created an app that invokes methods on hello device and displays hello response from hello device.</span></span> 

<span data-ttu-id="13b31-165">toocontinue wprowadzenie do korzystania z Centrum IoT i tooexplore innych scenariuszach IoT, zobacz:</span><span class="sxs-lookup"><span data-stu-id="13b31-165">toocontinue getting started with IoT Hub and tooexplore other IoT scenarios, see:</span></span>

* <span data-ttu-id="13b31-166">[Rozpoczynanie pracy z Centrum IoT]</span><span class="sxs-lookup"><span data-stu-id="13b31-166">[Get started with IoT Hub]</span></span>
* <span data-ttu-id="13b31-167">[Planowanie zadań na wielu urządzeniach][lnk-devguide-jobs]</span><span class="sxs-lookup"><span data-stu-id="13b31-167">[Schedule jobs on multiple devices][lnk-devguide-jobs]</span></span>

<span data-ttu-id="13b31-168">toolearn tooextend IoT metody rozwiązania i harmonogram wywołuje na wielu urządzeniach, zobacz hello [emisji zadania i harmonogramu] [ lnk-tutorial-jobs] samouczka.</span><span class="sxs-lookup"><span data-stu-id="13b31-168">toolearn how tooextend your IoT solution and schedule method calls on multiple devices, see hello [Schedule and broadcast jobs][lnk-tutorial-jobs] tutorial.</span></span>

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
