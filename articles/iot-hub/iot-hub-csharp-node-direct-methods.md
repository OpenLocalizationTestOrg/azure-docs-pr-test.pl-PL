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
# <a name="use-direct-methods-netnode"></a><span data-ttu-id="168d9-104">Użyj metody bezpośredniego (.NET/węzeł)</span><span class="sxs-lookup"><span data-stu-id="168d9-104">Use direct methods (.NET/Node)</span></span>
[!INCLUDE [iot-hub-selector-c2d-methods](../../includes/iot-hub-selector-c2d-methods.md)]

<span data-ttu-id="168d9-105">W tym samouczku zamierzamy toodevelop .NET i Node.js aplikację konsoli:</span><span class="sxs-lookup"><span data-stu-id="168d9-105">In this tutorial, we are going toodevelop a .NET and a Node.js console app:</span></span>

* <span data-ttu-id="168d9-106">**CallMethodOnDevice.sln**, aplikacji zaplecza .NET, która wywołuje metodę w aplikacji symulowane urządzenie hello i wyświetla hello odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="168d9-106">**CallMethodOnDevice.sln**, a .NET back-end app, which calls a method in hello simulated device app and displays hello response.</span></span>
* <span data-ttu-id="168d9-107">**SimulatedDevice.js**, aplikacji Node.js, która symuluje urządzenie łączące Centrum IoT tooyour z tożsamości urządzenia hello utworzony wcześniej i odpowiada toohello metody wywoływane przez hello chmury.</span><span class="sxs-lookup"><span data-stu-id="168d9-107">**SimulatedDevice.js**, a Node.js app, which simulates a device connecting tooyour IoT hub with hello device identity created earlier, and responds toohello method called by hello cloud.</span></span>

> [!NOTE]
> <span data-ttu-id="168d9-108">Artykuł Hello [Azure IoT SDK] [ lnk-hub-sdks] zawiera informacje o hello Azure IoT SDK, której można toobuild toorun zarówno aplikacje na urządzeniach i z zaplecza rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="168d9-108">hello article [Azure IoT SDKs][lnk-hub-sdks] provides information about hello Azure IoT SDKs that you can use toobuild both applications toorun on devices and your solution back end.</span></span>
> 
> 

<span data-ttu-id="168d9-109">toocomplete tego samouczka należy:</span><span class="sxs-lookup"><span data-stu-id="168d9-109">toocomplete this tutorial, you need:</span></span>

* <span data-ttu-id="168d9-110">Program Visual Studio 2015 lub Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="168d9-110">Visual Studio 2015 or Visual Studio 2017.</span></span>
* <span data-ttu-id="168d9-111">Środowisko Node.js w wersji 0.10.x lub nowszej.</span><span class="sxs-lookup"><span data-stu-id="168d9-111">Node.js version 0.10.x or later.</span></span>
* <span data-ttu-id="168d9-112">Aktywne konto platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="168d9-112">An active Azure account.</span></span> <span data-ttu-id="168d9-113">(Jeśli go nie masz, możesz utworzyć [bezpłatne konto próbne][lnk-free-trial] w zaledwie kilka minut).</span><span class="sxs-lookup"><span data-stu-id="168d9-113">(If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.)</span></span>

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity](../../includes/iot-hub-get-started-create-device-identity.md)]

## <a name="create-a-simulated-device-app"></a><span data-ttu-id="168d9-114">Tworzenie aplikacji symulowanego urządzenia</span><span class="sxs-lookup"><span data-stu-id="168d9-114">Create a simulated device app</span></span>
<span data-ttu-id="168d9-115">W tej sekcji utworzysz aplikację konsoli Node.js, która odpowiada tooa metody wywoływane przez rozwiązania hello zakończenia.</span><span class="sxs-lookup"><span data-stu-id="168d9-115">In this section, you create a Node.js console app that responds tooa method called by hello solution back end.</span></span>

1. <span data-ttu-id="168d9-116">Utwórz nowy pusty folder o nazwie **simulateddevice**.</span><span class="sxs-lookup"><span data-stu-id="168d9-116">Create a new empty folder called **simulateddevice**.</span></span> <span data-ttu-id="168d9-117">W hello **simulateddevice** folderu, Utwórz plik package.json za pomocą hello następujące polecenie z wiersza polecenia.</span><span class="sxs-lookup"><span data-stu-id="168d9-117">In hello **simulateddevice** folder, create a package.json file using hello following command at your command prompt.</span></span> <span data-ttu-id="168d9-118">Zaakceptuj wszystkie domyślne hello:</span><span class="sxs-lookup"><span data-stu-id="168d9-118">Accept all hello defaults:</span></span>
   
    ```
    npm init
    ```
2. <span data-ttu-id="168d9-119">Z wiersza polecenia w hello **simulateddevice** folderu, uruchom następujące polecenie tooinstall hello hello **azure iot urządzenia** i **azure-iot urządzenie mqtt** pakiety:</span><span class="sxs-lookup"><span data-stu-id="168d9-119">At your command prompt in hello **simulateddevice** folder, run hello following command tooinstall hello **azure-iot-device** and **azure-iot-device-mqtt** packages:</span></span>
   
    ```
        npm install azure-iot-device azure-iot-device-mqtt --save
    ```
3. <span data-ttu-id="168d9-120">Za pomocą edytora tekstu, Utwórz plik w hello **simulateddevice** folder i nadaj mu nazwę **SimulatedDevice.js**.</span><span class="sxs-lookup"><span data-stu-id="168d9-120">Using a text editor, create a file in hello **simulateddevice** folder and name it **SimulatedDevice.js**.</span></span>
4. <span data-ttu-id="168d9-121">Dodaj następujące hello `require` instrukcje na powitania początek hello **SimulatedDevice.js** pliku:</span><span class="sxs-lookup"><span data-stu-id="168d9-121">Add hello following `require` statements at hello start of hello **SimulatedDevice.js** file:</span></span>
   
    ```
    'use strict';
   
    var Mqtt = require('azure-iot-device-mqtt').Mqtt;
    var DeviceClient = require('azure-iot-device').Client;
    ```
5. <span data-ttu-id="168d9-122">Dodaj **connectionString** zmiennej i korzystać z niego toocreate **DeviceClient** wystąpienia.</span><span class="sxs-lookup"><span data-stu-id="168d9-122">Add a **connectionString** variable and use it toocreate a **DeviceClient** instance.</span></span> <span data-ttu-id="168d9-123">Zastąp **{ciąg połączenia urządzenia}** przy użyciu parametrów połączenia urządzenia hello wygenerowanych w hello *tworzenie tożsamości urządzenia* sekcji:</span><span class="sxs-lookup"><span data-stu-id="168d9-123">Replace **{device connection string}** with hello device connection string you generated in hello *Create a device identity* section:</span></span>
   
    ```
    var connectionString = '{device connection string}';
    var client = DeviceClient.fromConnectionString(connectionString, Mqtt);
    ```
6. <span data-ttu-id="168d9-124">Dodaj następujące metoda bezpośrednia hello tooimplement funkcji na urządzeniu hello hello:</span><span class="sxs-lookup"><span data-stu-id="168d9-124">Add hello following function tooimplement hello direct method on hello device:</span></span>
   
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
7. <span data-ttu-id="168d9-125">Otwórz Centrum IoT tooyour połączenia hello i zainicjować odbiornika metody hello:</span><span class="sxs-lookup"><span data-stu-id="168d9-125">Open hello connection tooyour IoT hub and initialize hello method listener:</span></span>
   
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
8. <span data-ttu-id="168d9-126">Zapisz i zamknij hello **SimulatedDevice.js** pliku.</span><span class="sxs-lookup"><span data-stu-id="168d9-126">Save and close hello **SimulatedDevice.js** file.</span></span>

> [!NOTE]
> <span data-ttu-id="168d9-127">rzeczy tookeep proste, w tym samouczku nie implementuje wszystkie zasady ponawiania.</span><span class="sxs-lookup"><span data-stu-id="168d9-127">tookeep things simple, this tutorial does not implement any retry policy.</span></span> <span data-ttu-id="168d9-128">W kodzie produkcyjnym, należy zaimplementować zasady ponawiania (np. Ponów próbę połączenia), zgodnie z sugestią podaną w artykuł w witrynie MSDN hello [obsługi błędów przejściowych][lnk-transient-faults].</span><span class="sxs-lookup"><span data-stu-id="168d9-128">In production code, you should implement retry policies (such as connection retry), as suggested in hello MSDN article [Transient Fault Handling][lnk-transient-faults].</span></span>
> 
> 

## <a name="call-a-direct-method-on-a-device"></a><span data-ttu-id="168d9-129">Wywołanie metody bezpośrednio na urządzeniu</span><span class="sxs-lookup"><span data-stu-id="168d9-129">Call a direct method on a device</span></span>
<span data-ttu-id="168d9-130">W tej sekcji służy do tworzenia aplikacji konsoli .NET, która wywołuje metodę hello symulowane urządzenie aplikacji, a następnie wyświetla hello odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="168d9-130">In this section, you create a .NET console app that calls a method in hello simulated device app and then displays hello response.</span></span>

1. <span data-ttu-id="168d9-131">W programie Visual Studio, należy dodać bieżącego rozwiązania toohello projektu Visual C# pulpitu systemu Windows klasycznego przy użyciu hello **aplikacji konsoli** szablonu projektu.</span><span class="sxs-lookup"><span data-stu-id="168d9-131">In Visual Studio, add a Visual C# Windows Classic Desktop project toohello current solution by using hello **Console Application** project template.</span></span> <span data-ttu-id="168d9-132">Upewnij się, że wersja platformy .NET hello jest 4.5.1 lub nowszej.</span><span class="sxs-lookup"><span data-stu-id="168d9-132">Make sure hello .NET Framework version is 4.5.1 or later.</span></span> <span data-ttu-id="168d9-133">Nazwa projektu hello **CallMethodOnDevice**.</span><span class="sxs-lookup"><span data-stu-id="168d9-133">Name hello project **CallMethodOnDevice**.</span></span>
   
    ![Nowy projekt Visual C# Windows Classic Desktop][10]
2. <span data-ttu-id="168d9-135">W Eksploratorze rozwiązań kliknij prawym przyciskiem myszy hello **CallMethodOnDevice** projektu, a następnie kliknij przycisk **Zarządzaj pakietami NuGet...** .</span><span class="sxs-lookup"><span data-stu-id="168d9-135">In Solution Explorer, right-click hello **CallMethodOnDevice** project, and then click **Manage NuGet Packages...**.</span></span>
3. <span data-ttu-id="168d9-136">W hello **Menedżera pakietów NuGet** wybierz **Przeglądaj**, wyszukaj **microsoft.azure.devices**, wybierz pozycję **zainstalować** tooinstall Witaj **Microsoft.Azure.Devices** pakietu i zaakceptuj warunki użytkowania hello.</span><span class="sxs-lookup"><span data-stu-id="168d9-136">In hello **NuGet Package Manager** window, select **Browse**, search for **microsoft.azure.devices**, select **Install** tooinstall hello **Microsoft.Azure.Devices** package, and accept hello terms of use.</span></span> <span data-ttu-id="168d9-137">Ta procedura pliki do pobrania, instaluje i dodaje toohello odwołanie [zestawu SDK usług Azure IoT] [ lnk-nuget-service-sdk] NuGet pakiet i jego zależności.</span><span class="sxs-lookup"><span data-stu-id="168d9-137">This procedure downloads, installs, and adds a reference toohello [Azure IoT service SDK][lnk-nuget-service-sdk] NuGet package and its dependencies.</span></span>
   
    ![Okno Menedżera pakietów NuGet][11]

4. <span data-ttu-id="168d9-139">Dodaj następujące hello `using` instrukcji u góry hello hello **Program.cs** pliku:</span><span class="sxs-lookup"><span data-stu-id="168d9-139">Add hello following `using` statements at hello top of hello **Program.cs** file:</span></span>
   
        using System.Threading.Tasks;
        using Microsoft.Azure.Devices;
5. <span data-ttu-id="168d9-140">Dodaj następujące pola toohello hello **Program** klasy.</span><span class="sxs-lookup"><span data-stu-id="168d9-140">Add hello following fields toohello **Program** class.</span></span> <span data-ttu-id="168d9-141">Zastąp wartość symbolu zastępczego hello hello hello koncentratora, który został utworzony w poprzedniej sekcji hello parametry połączenia Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="168d9-141">Replace hello placeholder value with hello IoT Hub connection string for hello hub that you created in hello previous section.</span></span>
   
        static ServiceClient serviceClient;
        static string connectionString = "{iot hub connection string}";
6. <span data-ttu-id="168d9-142">Dodaj następujące metody toohello hello **Program** klasy:</span><span class="sxs-lookup"><span data-stu-id="168d9-142">Add hello following method toohello **Program** class:</span></span>
   
        private static async Task InvokeMethod()
        {
            var methodInvocation = new CloudToDeviceMethod("writeLine") { ResponseTimeout = TimeSpan.FromSeconds(30) };
            methodInvocation.SetPayloadJson("'a line toobe written'");

            var response = await serviceClient.InvokeDeviceMethodAsync("myDeviceId", methodInvocation);

            Console.WriteLine("Response status: {0}, payload:", response.Status);
            Console.WriteLine(response.GetPayloadAsJson());
        }
   
    <span data-ttu-id="168d9-143">Ta metoda wywołuje metodę bezpośredniego o nazwie `writeLine` na powitania `myDeviceId` urządzenia.</span><span class="sxs-lookup"><span data-stu-id="168d9-143">This method invokes a direct method with name `writeLine` on hello `myDeviceId` device.</span></span> <span data-ttu-id="168d9-144">Następnie zapisuje odpowiedź hello udostępniane przez urządzenie hello na powitania konsoli.</span><span class="sxs-lookup"><span data-stu-id="168d9-144">Then, it writes hello response provided by hello device on hello console.</span></span> <span data-ttu-id="168d9-145">Należy zwrócić uwagę, jak to możliwe toospecify wartość limitu czasu dla hello toorespond urządzenia.</span><span class="sxs-lookup"><span data-stu-id="168d9-145">Note how it is possible toospecify a timeout value for hello device toorespond.</span></span>
7. <span data-ttu-id="168d9-146">Na koniec należy dodać następujące wiersze toohello hello **Main** metody:</span><span class="sxs-lookup"><span data-stu-id="168d9-146">Finally, add hello following lines toohello **Main** method:</span></span>
   
        serviceClient = ServiceClient.CreateFromConnectionString(connectionString);
        InvokeMethod().Wait();
        Console.WriteLine("Press Enter tooexit.");
        Console.ReadLine();

## <a name="run-hello-applications"></a><span data-ttu-id="168d9-147">Uruchamianie aplikacji hello</span><span class="sxs-lookup"><span data-stu-id="168d9-147">Run hello applications</span></span>
<span data-ttu-id="168d9-148">Wszystko jest teraz gotowy toorun hello aplikacji.</span><span class="sxs-lookup"><span data-stu-id="168d9-148">You are now ready toorun hello applications.</span></span>

1. <span data-ttu-id="168d9-149">W hello Visual Studio Solution Explorer, kliknij prawym przyciskiem myszy rozwiązanie, a następnie kliknij przycisk **Ustaw projekty startowe...** . Wybierz **jednego projektu startowego**, a następnie wybierz hello **CallMethodOnDevice** projektu w menu rozwijanym hello.</span><span class="sxs-lookup"><span data-stu-id="168d9-149">In hello Visual Studio Solution Explorer, right-click your solution, and then click **Set StartUp Projects...**. Select **Single startup project**, and then select hello **CallMethodOnDevice** project in hello dropdown menu.</span></span>

2. <span data-ttu-id="168d9-150">W wierszu polecenia w hello **simulateddevice** folderu, uruchom następujące polecenia toostart nasłuchiwania dla wywołań metod z Centrum IoT hello:</span><span class="sxs-lookup"><span data-stu-id="168d9-150">At a command prompt in hello **simulateddevice** folder, run hello following command toostart listening for method calls from your IoT Hub:</span></span>
   
    ```
    node SimulatedDevice.js
    ```
   <span data-ttu-id="168d9-151">Poczekaj, aż hello symulowane urządzenie tooopen:![][7]</span><span class="sxs-lookup"><span data-stu-id="168d9-151">Wait for hello simulated device tooopen:  ![][7]</span></span>
3. <span data-ttu-id="168d9-152">Teraz urządzenia hello jest połączony i Oczekiwanie na wywołania metody, uruchom hello .NET **CallMethodOnDevice** metody hello tooinvoke aplikacji hello symulowane urządzenie aplikacji.</span><span class="sxs-lookup"><span data-stu-id="168d9-152">Now that hello device is connected and waiting for method invocations, run hello .NET **CallMethodOnDevice** app tooinvoke hello method in hello simulated device app.</span></span> <span data-ttu-id="168d9-153">Powinna zostać wyświetlona odpowiedź urządzenia hello napisana hello konsoli.</span><span class="sxs-lookup"><span data-stu-id="168d9-153">You should see hello device response written in hello console.</span></span>
   
    ![][8]
4. <span data-ttu-id="168d9-154">urządzenie Hello następnie reaguje metody toohello wydrukowanie tej wiadomości:</span><span class="sxs-lookup"><span data-stu-id="168d9-154">hello device then reacts toohello method by printing this message:</span></span>
   
    ![][9]

## <a name="next-steps"></a><span data-ttu-id="168d9-155">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="168d9-155">Next steps</span></span>
<span data-ttu-id="168d9-156">W tym samouczku został skonfigurowany nowego centrum IoT w portalu Azure hello i w rejestrze tożsamości Centrum IoT hello zostanie utworzona tożsamość urządzenia.</span><span class="sxs-lookup"><span data-stu-id="168d9-156">In this tutorial, you configured a new IoT hub in hello Azure portal, and then created a device identity in hello IoT hub's identity registry.</span></span> <span data-ttu-id="168d9-157">Użyto tego urządzenia tożsamości tooenable hello symulowane urządzenie aplikacji tooreact toomethods wywołana przez hello chmury.</span><span class="sxs-lookup"><span data-stu-id="168d9-157">You used this device identity tooenable hello simulated device app tooreact toomethods invoked by hello cloud.</span></span> <span data-ttu-id="168d9-158">Utworzono aplikację, która wywołuje metody na urządzeniu hello i wyświetla hello odpowiedzi z hello urządzenia.</span><span class="sxs-lookup"><span data-stu-id="168d9-158">You also created an app that invokes methods on hello device and displays hello response from hello device.</span></span> 

<span data-ttu-id="168d9-159">toocontinue wprowadzenie do korzystania z Centrum IoT i tooexplore innych scenariuszach IoT, zobacz:</span><span class="sxs-lookup"><span data-stu-id="168d9-159">toocontinue getting started with IoT Hub and tooexplore other IoT scenarios, see:</span></span>

* <span data-ttu-id="168d9-160">[Rozpoczynanie pracy z Centrum IoT]</span><span class="sxs-lookup"><span data-stu-id="168d9-160">[Get started with IoT Hub]</span></span>
* <span data-ttu-id="168d9-161">[Planowanie zadań na wielu urządzeniach][lnk-devguide-jobs]</span><span class="sxs-lookup"><span data-stu-id="168d9-161">[Schedule jobs on multiple devices][lnk-devguide-jobs]</span></span>

<span data-ttu-id="168d9-162">toolearn tooextend IoT metody rozwiązania i harmonogram wywołuje na wielu urządzeniach, zobacz hello [emisji zadania i harmonogramu] [ lnk-tutorial-jobs] samouczka.</span><span class="sxs-lookup"><span data-stu-id="168d9-162">toolearn how tooextend your IoT solution and schedule method calls on multiple devices, see hello [Schedule and broadcast jobs][lnk-tutorial-jobs] tutorial.</span></span>

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
