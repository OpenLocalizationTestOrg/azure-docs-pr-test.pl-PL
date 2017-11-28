---
title: "Centrum IoT Azure bezpośredniego metody (.NET/węzła) | Dokumentacja firmy Microsoft"
description: "Jak używać bezpośrednich metod Centrum IoT Azure. Przy użyciu urządzenia Azure IoT SDK dla środowiska Node.js aplikacji symulowane urządzenie, która zawiera metoda bezpośrednia i usługę Azure IoT SDK dla platformy .NET zaimplementować aplikację usługi, która wywołuje metodę bezpośredniego."
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
ms.openlocfilehash: ad705789a153381e21b2ccb05d4e0c17f78671fd
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="use-direct-methods-netnode"></a><span data-ttu-id="0a544-104">Użyj metody bezpośredniego (.NET/węzeł)</span><span class="sxs-lookup"><span data-stu-id="0a544-104">Use direct methods (.NET/Node)</span></span>
[!INCLUDE [iot-hub-selector-c2d-methods](../../includes/iot-hub-selector-c2d-methods.md)]

<span data-ttu-id="0a544-105">W tym samouczku zamierzamy opracowanie .NET i Node.js aplikację konsoli:</span><span class="sxs-lookup"><span data-stu-id="0a544-105">In this tutorial, we are going to develop a .NET and a Node.js console app:</span></span>

* <span data-ttu-id="0a544-106">**CallMethodOnDevice.sln**, aplikacji zaplecza .NET, która wywołuje metodę w aplikacji symulowane urządzenie i wyświetla odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="0a544-106">**CallMethodOnDevice.sln**, a .NET back-end app, which calls a method in the simulated device app and displays the response.</span></span>
* <span data-ttu-id="0a544-107">**SimulatedDevice.js**, aplikacji Node.js, która symuluje nawiązywania połączenia z Centrum IoT z tożsamości urządzenia utworzony wcześniej urządzenia i odpowiada metodzie wywołanej przez chmurę.</span><span class="sxs-lookup"><span data-stu-id="0a544-107">**SimulatedDevice.js**, a Node.js app, which simulates a device connecting to your IoT hub with the device identity created earlier, and responds to the method called by the cloud.</span></span>

> [!NOTE]
> <span data-ttu-id="0a544-108">Artykuł [Azure IoT SDKs][lnk-hub-sdks] (Zestawy SDK usług Azure IoT) zawiera informacje dotyczące zestawów SDK usług Azure IoT, przy użyciu których można tworzyć aplikacje zarówno do uruchamiania na urządzaniach, jak i w zapleczu rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="0a544-108">The article [Azure IoT SDKs][lnk-hub-sdks] provides information about the Azure IoT SDKs that you can use to build both applications to run on devices and your solution back end.</span></span>
> 
> 

<span data-ttu-id="0a544-109">Do ukończenia tego samouczka niezbędne są następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="0a544-109">To complete this tutorial, you need:</span></span>

* <span data-ttu-id="0a544-110">Program Visual Studio 2015 lub Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="0a544-110">Visual Studio 2015 or Visual Studio 2017.</span></span>
* <span data-ttu-id="0a544-111">Środowisko Node.js w wersji 0.10.x lub nowszej.</span><span class="sxs-lookup"><span data-stu-id="0a544-111">Node.js version 0.10.x or later.</span></span>
* <span data-ttu-id="0a544-112">Aktywne konto platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="0a544-112">An active Azure account.</span></span> <span data-ttu-id="0a544-113">(Jeśli go nie masz, możesz utworzyć [bezpłatne konto próbne][lnk-free-trial] w zaledwie kilka minut).</span><span class="sxs-lookup"><span data-stu-id="0a544-113">(If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.)</span></span>

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity](../../includes/iot-hub-get-started-create-device-identity.md)]

## <a name="create-a-simulated-device-app"></a><span data-ttu-id="0a544-114">Tworzenie aplikacji symulowanego urządzenia</span><span class="sxs-lookup"><span data-stu-id="0a544-114">Create a simulated device app</span></span>
<span data-ttu-id="0a544-115">W tej sekcji służy do tworzenia aplikacji konsoli Node.js, która odpowiada do metody wywoływane przez rozwiązania zakończenia.</span><span class="sxs-lookup"><span data-stu-id="0a544-115">In this section, you create a Node.js console app that responds to a method called by the solution back end.</span></span>

1. <span data-ttu-id="0a544-116">Utwórz nowy pusty folder o nazwie **simulateddevice**.</span><span class="sxs-lookup"><span data-stu-id="0a544-116">Create a new empty folder called **simulateddevice**.</span></span> <span data-ttu-id="0a544-117">W folderze **simulateddevice** utwórz plik package.json przy użyciu następującego polecenia z poziomu wiersza polecenia.</span><span class="sxs-lookup"><span data-stu-id="0a544-117">In the **simulateddevice** folder, create a package.json file using the following command at your command prompt.</span></span> <span data-ttu-id="0a544-118">Zaakceptuj wszystkie ustawienia domyślne:</span><span class="sxs-lookup"><span data-stu-id="0a544-118">Accept all the defaults:</span></span>
   
    ```
    npm init
    ```
2. <span data-ttu-id="0a544-119">Z wiersza polecenia w **simulateddevice** folderu, uruchom następujące polecenie, aby zainstalować **azure iot urządzenia** i **azure-iot urządzenie mqtt** pakiety:</span><span class="sxs-lookup"><span data-stu-id="0a544-119">At your command prompt in the **simulateddevice** folder, run the following command to install the **azure-iot-device** and **azure-iot-device-mqtt** packages:</span></span>
   
    ```
        npm install azure-iot-device azure-iot-device-mqtt --save
    ```
3. <span data-ttu-id="0a544-120">Za pomocą edytora tekstu, Utwórz plik w **simulateddevice** folder i nadaj mu nazwę **SimulatedDevice.js**.</span><span class="sxs-lookup"><span data-stu-id="0a544-120">Using a text editor, create a file in the **simulateddevice** folder and name it **SimulatedDevice.js**.</span></span>
4. <span data-ttu-id="0a544-121">Dodaj następujące instrukcje `require` na początku pliku **SimulatedDevice.js**:</span><span class="sxs-lookup"><span data-stu-id="0a544-121">Add the following `require` statements at the start of the **SimulatedDevice.js** file:</span></span>
   
    ```
    'use strict';
   
    var Mqtt = require('azure-iot-device-mqtt').Mqtt;
    var DeviceClient = require('azure-iot-device').Client;
    ```
5. <span data-ttu-id="0a544-122">Dodaj **connectionString** zmiennej i użyj go, aby utworzyć **DeviceClient** wystąpienia.</span><span class="sxs-lookup"><span data-stu-id="0a544-122">Add a **connectionString** variable and use it to create a **DeviceClient** instance.</span></span> <span data-ttu-id="0a544-123">Zastąp **{ciąg połączenia urządzenia}** z połączenie z urządzeniem ciągu zostanie wygenerowany w *tworzenie tożsamości urządzenia* sekcji:</span><span class="sxs-lookup"><span data-stu-id="0a544-123">Replace **{device connection string}** with the device connection string you generated in the *Create a device identity* section:</span></span>
   
    ```
    var connectionString = '{device connection string}';
    var client = DeviceClient.fromConnectionString(connectionString, Mqtt);
    ```
6. <span data-ttu-id="0a544-124">Dodaj następującą funkcję do zaimplementowania metoda bezpośrednia na urządzeniu:</span><span class="sxs-lookup"><span data-stu-id="0a544-124">Add the following function to implement the direct method on the device:</span></span>
   
    ```
    function onWriteLine(request, response) {
        console.log(request.payload);
   
        response.send(200, 'Input was written to log.', function(err) {
            if(err) {
                console.error('An error occurred when sending a method response:\n' + err.toString());
            } else {
                console.log('Response to method \'' + request.methodName + '\' sent successfully.' );
            }
        });
    }
    ```
7. <span data-ttu-id="0a544-125">Otwórz połączenie z Centrum IoT i zainicjować odbiornika metody:</span><span class="sxs-lookup"><span data-stu-id="0a544-125">Open the connection to your IoT hub and initialize the method listener:</span></span>
   
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
8. <span data-ttu-id="0a544-126">Zapisz i zamknij plik **SimulatedDevice.js**.</span><span class="sxs-lookup"><span data-stu-id="0a544-126">Save and close the **SimulatedDevice.js** file.</span></span>

> [!NOTE]
> <span data-ttu-id="0a544-127">Dla uproszczenia ten samouczek nie zawiera opisu wdrożenia żadnych zasad ponawiania.</span><span class="sxs-lookup"><span data-stu-id="0a544-127">To keep things simple, this tutorial does not implement any retry policy.</span></span> <span data-ttu-id="0a544-128">W kodzie produkcyjnym, należy zaimplementować zasady ponawiania (np. Ponów próbę połączenia), zgodnie z sugestią podaną w artykuł w witrynie MSDN [obsługi błędów przejściowych][lnk-transient-faults].</span><span class="sxs-lookup"><span data-stu-id="0a544-128">In production code, you should implement retry policies (such as connection retry), as suggested in the MSDN article [Transient Fault Handling][lnk-transient-faults].</span></span>
> 
> 

## <a name="call-a-direct-method-on-a-device"></a><span data-ttu-id="0a544-129">Wywołanie metody bezpośrednio na urządzeniu</span><span class="sxs-lookup"><span data-stu-id="0a544-129">Call a direct method on a device</span></span>
<span data-ttu-id="0a544-130">W tej sekcji służy do tworzenia aplikacji konsoli .NET, która wywołuje metodę w aplikacji symulowane urządzenie, a następnie wyświetla odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="0a544-130">In this section, you create a .NET console app that calls a method in the simulated device app and then displays the response.</span></span>

1. <span data-ttu-id="0a544-131">W programie Visual Studio dodaj projekt Visual C# Windows Classic Desktop do bieżącego rozwiązania przy użyciu szablonu projektu **Aplikacja konsolowa**.</span><span class="sxs-lookup"><span data-stu-id="0a544-131">In Visual Studio, add a Visual C# Windows Classic Desktop project to the current solution by using the **Console Application** project template.</span></span> <span data-ttu-id="0a544-132">Upewnij się, że program .NET Framework jest w wersji 4.5.1 lub nowszej.</span><span class="sxs-lookup"><span data-stu-id="0a544-132">Make sure the .NET Framework version is 4.5.1 or later.</span></span> <span data-ttu-id="0a544-133">Nazwij projekt **CallMethodOnDevice**.</span><span class="sxs-lookup"><span data-stu-id="0a544-133">Name the project **CallMethodOnDevice**.</span></span>
   
    ![Nowy projekt Visual C# Windows Classic Desktop][10]
2. <span data-ttu-id="0a544-135">W Eksploratorze rozwiązań kliknij prawym przyciskiem myszy **CallMethodOnDevice** projektu, a następnie kliknij przycisk **Zarządzaj pakietami NuGet...** .</span><span class="sxs-lookup"><span data-stu-id="0a544-135">In Solution Explorer, right-click the **CallMethodOnDevice** project, and then click **Manage NuGet Packages...**.</span></span>
3. <span data-ttu-id="0a544-136">W oknie **Menedżer pakietów NuGet** wybierz opcję **Przeglądaj**, wyszukaj pozycję **microsoft.azure.devices**, wybierz opcję **Zainstaluj**, aby zainstalować pakiet **Microsoft.Azure.Devices**, i zaakceptuj warunki użytkowania.</span><span class="sxs-lookup"><span data-stu-id="0a544-136">In the **NuGet Package Manager** window, select **Browse**, search for **microsoft.azure.devices**, select **Install** to install the **Microsoft.Azure.Devices** package, and accept the terms of use.</span></span> <span data-ttu-id="0a544-137">Ta procedura spowoduje pobranie, zainstalowanie i dodanie odwołania do pakietu NuGet [zestawu SDK usługi Azure IoT][lnk-nuget-service-sdk] oraz jego zależności.</span><span class="sxs-lookup"><span data-stu-id="0a544-137">This procedure downloads, installs, and adds a reference to the [Azure IoT service SDK][lnk-nuget-service-sdk] NuGet package and its dependencies.</span></span>
   
    ![Okno Menedżera pakietów NuGet][11]

4. <span data-ttu-id="0a544-139">Dodaj następujące instrukcje `using` w górnej części pliku **Program.cs**:</span><span class="sxs-lookup"><span data-stu-id="0a544-139">Add the following `using` statements at the top of the **Program.cs** file:</span></span>
   
        using System.Threading.Tasks;
        using Microsoft.Azure.Devices;
5. <span data-ttu-id="0a544-140">Dodaj następujące pola do klasy **Program**:</span><span class="sxs-lookup"><span data-stu-id="0a544-140">Add the following fields to the **Program** class.</span></span> <span data-ttu-id="0a544-141">Zastąp wartość symbolu zastępczego parametrami połączenia usługi IoT Hub dla centrum IoT utworzonego w poprzedniej sekcji.</span><span class="sxs-lookup"><span data-stu-id="0a544-141">Replace the placeholder value with the IoT Hub connection string for the hub that you created in the previous section.</span></span>
   
        static ServiceClient serviceClient;
        static string connectionString = "{iot hub connection string}";
6. <span data-ttu-id="0a544-142">Dodaj następującą metodę do klasy **Program**:</span><span class="sxs-lookup"><span data-stu-id="0a544-142">Add the following method to the **Program** class:</span></span>
   
        private static async Task InvokeMethod()
        {
            var methodInvocation = new CloudToDeviceMethod("writeLine") { ResponseTimeout = TimeSpan.FromSeconds(30) };
            methodInvocation.SetPayloadJson("'a line to be written'");

            var response = await serviceClient.InvokeDeviceMethodAsync("myDeviceId", methodInvocation);

            Console.WriteLine("Response status: {0}, payload:", response.Status);
            Console.WriteLine(response.GetPayloadAsJson());
        }
   
    <span data-ttu-id="0a544-143">Ta metoda wywołuje metodę bezpośredniego o nazwie `writeLine` na `myDeviceId` urządzenia.</span><span class="sxs-lookup"><span data-stu-id="0a544-143">This method invokes a direct method with name `writeLine` on the `myDeviceId` device.</span></span> <span data-ttu-id="0a544-144">Następnie zapisuje odpowiedź udostępnianym przez urządzenie na konsoli.</span><span class="sxs-lookup"><span data-stu-id="0a544-144">Then, it writes the response provided by the device on the console.</span></span> <span data-ttu-id="0a544-145">Należy pamiętać, jak można określić wartość limitu czasu na odpowiedź urządzenia.</span><span class="sxs-lookup"><span data-stu-id="0a544-145">Note how it is possible to specify a timeout value for the device to respond.</span></span>
7. <span data-ttu-id="0a544-146">Na koniec dodaj następujące wiersze do metody **Główne**:</span><span class="sxs-lookup"><span data-stu-id="0a544-146">Finally, add the following lines to the **Main** method:</span></span>
   
        serviceClient = ServiceClient.CreateFromConnectionString(connectionString);
        InvokeMethod().Wait();
        Console.WriteLine("Press Enter to exit.");
        Console.ReadLine();

## <a name="run-the-applications"></a><span data-ttu-id="0a544-147">Uruchamianie aplikacji</span><span class="sxs-lookup"><span data-stu-id="0a544-147">Run the applications</span></span>
<span data-ttu-id="0a544-148">Teraz można uruchomić aplikacje.</span><span class="sxs-lookup"><span data-stu-id="0a544-148">You are now ready to run the applications.</span></span>

1. <span data-ttu-id="0a544-149">W Eksploratorze rozwiązań programu Visual Studio kliknij rozwiązanie prawym przyciskiem myszy, a następnie kliknij przycisk **Ustaw projekty startowe...** .</span><span class="sxs-lookup"><span data-stu-id="0a544-149">In the Visual Studio Solution Explorer, right-click your solution, and then click **Set StartUp Projects...**.</span></span> <span data-ttu-id="0a544-150">Wybierz **jednego projektu startowego**, a następnie wybierz **CallMethodOnDevice** projektu w menu rozwijanym.</span><span class="sxs-lookup"><span data-stu-id="0a544-150">Select **Single startup project**, and then select the **CallMethodOnDevice** project in the dropdown menu.</span></span>

2. <span data-ttu-id="0a544-151">W wierszu polecenia **simulateddevice** folderu, uruchom następujące polecenie, aby rozpocząć nasłuchiwania dla wywołań metod z Centrum IoT:</span><span class="sxs-lookup"><span data-stu-id="0a544-151">At a command prompt in the **simulateddevice** folder, run the following command to start listening for method calls from your IoT Hub:</span></span>
   
    ```
    node SimulatedDevice.js
    ```
   <span data-ttu-id="0a544-152">Poczekaj, aż symulowane urządzenie otworzyć:![][7]</span><span class="sxs-lookup"><span data-stu-id="0a544-152">Wait for the simulated device to open:  ![][7]</span></span>
3. <span data-ttu-id="0a544-153">Teraz, gdy urządzenie jest podłączone i Oczekiwanie na wywołania metody uruchamiania programu .NET **CallMethodOnDevice** aplikacji można wywołać metody w aplikacji symulowane urządzenie.</span><span class="sxs-lookup"><span data-stu-id="0a544-153">Now that the device is connected and waiting for method invocations, run the .NET **CallMethodOnDevice** app to invoke the method in the simulated device app.</span></span> <span data-ttu-id="0a544-154">Powinna zostać wyświetlona odpowiedź urządzenia zapisywane w konsoli.</span><span class="sxs-lookup"><span data-stu-id="0a544-154">You should see the device response written in the console.</span></span>
   
    ![][8]
4. <span data-ttu-id="0a544-155">Wydrukowanie tej wiadomości urządzenia reaguje do metody:</span><span class="sxs-lookup"><span data-stu-id="0a544-155">The device then reacts to the method by printing this message:</span></span>
   
    ![][9]

## <a name="next-steps"></a><span data-ttu-id="0a544-156">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="0a544-156">Next steps</span></span>
<span data-ttu-id="0a544-157">W tym samouczku opisano konfigurowanie nowego centrum IoT Hub w witrynie Azure Portal, a następnie tworzenie tożsamości urządzenia w rejestrze tożsamości centrum.</span><span class="sxs-lookup"><span data-stu-id="0a544-157">In this tutorial, you configured a new IoT hub in the Azure portal, and then created a device identity in the IoT hub's identity registry.</span></span> <span data-ttu-id="0a544-158">Tej tożsamości urządzenia są używane do włączenia aplikacji symulowane urządzenie zareagować na metody wywoływane przez chmurę.</span><span class="sxs-lookup"><span data-stu-id="0a544-158">You used this device identity to enable the simulated device app to react to methods invoked by the cloud.</span></span> <span data-ttu-id="0a544-159">Utworzono aplikację, która wywołuje metody na urządzeniu i wyświetla odpowiedzi z urządzenia.</span><span class="sxs-lookup"><span data-stu-id="0a544-159">You also created an app that invokes methods on the device and displays the response from the device.</span></span> 

<span data-ttu-id="0a544-160">Aby kontynuować wprowadzenie do usługi IoT Hub i zapoznać się z innymi scenariuszami IoT, zobacz:</span><span class="sxs-lookup"><span data-stu-id="0a544-160">To continue getting started with IoT Hub and to explore other IoT scenarios, see:</span></span>

* <span data-ttu-id="0a544-161">[Rozpoczynanie pracy z Centrum IoT]</span><span class="sxs-lookup"><span data-stu-id="0a544-161">[Get started with IoT Hub]</span></span>
* <span data-ttu-id="0a544-162">[Planowanie zadań na wielu urządzeniach][lnk-devguide-jobs]</span><span class="sxs-lookup"><span data-stu-id="0a544-162">[Schedule jobs on multiple devices][lnk-devguide-jobs]</span></span>

<span data-ttu-id="0a544-163">Aby dowiedzieć się, jak rozszerzyć IoT, Twoje rozwiązanie i harmonogram metoda wywołuje na wielu urządzeniach, zobacz [emisji zadania i harmonogramu] [ lnk-tutorial-jobs] samouczka.</span><span class="sxs-lookup"><span data-stu-id="0a544-163">To learn how to extend your IoT solution and schedule method calls on multiple devices, see the [Schedule and broadcast jobs][lnk-tutorial-jobs] tutorial.</span></span>

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
<span data-ttu-id="0a544-164">[Rozpoczynanie pracy z Centrum IoT]: iot-hub-node-node-getstarted.md</span><span class="sxs-lookup"><span data-stu-id="0a544-164">[Get started with IoT Hub]: iot-hub-node-node-getstarted.md</span></span>
