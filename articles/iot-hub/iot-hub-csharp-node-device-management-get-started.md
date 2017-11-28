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
# <a name="get-started-with-device-management-netnode"></a><span data-ttu-id="cd6a7-104">Wprowadzenie do zarządzania urządzeniami (.NET/węzeł)</span><span class="sxs-lookup"><span data-stu-id="cd6a7-104">Get started with device management (.NET/Node)</span></span>

[!INCLUDE [iot-hub-selector-dm-getstarted](../../includes/iot-hub-selector-dm-getstarted.md)]

<span data-ttu-id="cd6a7-105">Ten samouczek przedstawia sposób wykonania następujących czynności:</span><span class="sxs-lookup"><span data-stu-id="cd6a7-105">This tutorial shows you how to:</span></span>

* <span data-ttu-id="cd6a7-106">Użyj hello toocreate portalu Azure IoT Hub i Utwórz tożsamość urządzenia w Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="cd6a7-106">Use hello Azure portal toocreate an IoT Hub and create a device identity in your IoT hub.</span></span>
* <span data-ttu-id="cd6a7-107">Tworzenie aplikacji symulowane urządzenie zawierającej bezpośredniego metodę, która wykonuje ponowny rozruch tego urządzenia.</span><span class="sxs-lookup"><span data-stu-id="cd6a7-107">Create a simulated device app that contains a direct method that reboots that device.</span></span> <span data-ttu-id="cd6a7-108">Bezpośrednie metody są wywoływane z hello chmury.</span><span class="sxs-lookup"><span data-stu-id="cd6a7-108">Direct methods are invoked from hello cloud.</span></span>
* <span data-ttu-id="cd6a7-109">Tworzenie aplikacji konsoli .NET, który wywołuje metodę bezpośredniego ponowny rozruch hello w hello symulowane urządzenie aplikacji za pośrednictwem Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="cd6a7-109">Create a .NET console app that calls hello reboot direct method in hello simulated device app through your IoT hub.</span></span>

<span data-ttu-id="cd6a7-110">Na końcu hello tego samouczka masz aplikację Node.js konsoli urządzenia i zaplecza aplikacji konsoli .NET (C#):</span><span class="sxs-lookup"><span data-stu-id="cd6a7-110">At hello end of this tutorial, you have a Node.js console device app and a .NET (C#) console back-end app:</span></span>

<span data-ttu-id="cd6a7-111">**dmpatterns_getstarted_device.js**, o tożsamości urządzenia hello utworzony wcześniej, który łączy Centrum IoT tooyour odbiera metoda bezpośrednia ponowny rozruch, symuluje ponowny rozruch komputera fizycznego i raporty hello czasu ostatniego ponownego uruchomienia hello.</span><span class="sxs-lookup"><span data-stu-id="cd6a7-111">**dmpatterns_getstarted_device.js**, which connects tooyour IoT hub with hello device identity created earlier, receives a reboot direct method, simulates a physical reboot, and reports hello time for hello last reboot.</span></span>

<span data-ttu-id="cd6a7-112">**TriggerReboot**, która wywołuje metodę bezpośrednio w aplikacji hello symulowane urządzenie Wyświetla odpowiedź hello, i wyświetla hello zaktualizowane raportowane właściwości.</span><span class="sxs-lookup"><span data-stu-id="cd6a7-112">**TriggerReboot**, which calls a direct method in hello simulated device app, displays hello response, and displays hello updated reported properties.</span></span>

<span data-ttu-id="cd6a7-113">toocomplete tego samouczka należy hello następujące:</span><span class="sxs-lookup"><span data-stu-id="cd6a7-113">toocomplete this tutorial, you need hello following:</span></span>

* <span data-ttu-id="cd6a7-114">Program Visual Studio 2015 lub Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="cd6a7-114">Visual Studio 2015 or Visual Studio 2017.</span></span>
* <span data-ttu-id="cd6a7-115">Środowisko node.js w wersji 0.12.x lub nowszym</span><span class="sxs-lookup"><span data-stu-id="cd6a7-115">Node.js version 0.12.x or later,</span></span> <br/>  <span data-ttu-id="cd6a7-116">[Przygotowywanie środowiska projektowego] [ lnk-dev-setup] w tym artykule opisano sposób tooinstall Node.js, w tym samouczku w systemie Windows lub Linux.</span><span class="sxs-lookup"><span data-stu-id="cd6a7-116">[Prepare your development environment][lnk-dev-setup] describes how tooinstall Node.js for this tutorial on either Windows or Linux.</span></span>
* <span data-ttu-id="cd6a7-117">Aktywne konto platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="cd6a7-117">An active Azure account.</span></span> <span data-ttu-id="cd6a7-118">(Jeśli go nie masz, możesz utworzyć [bezpłatne konto próbne][lnk-free-trial] w zaledwie kilka minut).</span><span class="sxs-lookup"><span data-stu-id="cd6a7-118">(If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.)</span></span>

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity](../../includes/iot-hub-get-started-create-device-identity.md)]

## <a name="trigger-a-remote-reboot-on-hello-device-using-a-direct-method"></a><span data-ttu-id="cd6a7-119">Wyzwalacz zdalnego ponownego uruchomienia na urządzeniu hello za pomocą bezpośrednich — metoda</span><span class="sxs-lookup"><span data-stu-id="cd6a7-119">Trigger a remote reboot on hello device using a direct method</span></span>
<span data-ttu-id="cd6a7-120">W tej sekcji służy do tworzenia aplikacji konsoli .NET (przy użyciu języka C#) inicjującym zdalnego ponownego uruchomienia na urządzeniu przy użyciu metody bezpośredniego.</span><span class="sxs-lookup"><span data-stu-id="cd6a7-120">In this section, you create a .NET console app (using C#) that initiates a remote reboot on a device using a direct method.</span></span> <span data-ttu-id="cd6a7-121">Aplikacja Hello używa urządzenia dwie zapytania toodiscover hello ostatniego ponownego uruchomienia dla tego urządzenia.</span><span class="sxs-lookup"><span data-stu-id="cd6a7-121">hello app uses device twin queries toodiscover hello last reboot time for that device.</span></span>

1. <span data-ttu-id="cd6a7-122">W programie Visual Studio, Dodaj nowe rozwiązanie tooa projektu Visual C# pulpitu systemu Windows klasycznego przy użyciu hello **aplikacji konsoli (.NET Framework)** szablonu projektu.</span><span class="sxs-lookup"><span data-stu-id="cd6a7-122">In Visual Studio, add a Visual C# Windows Classic Desktop project tooa new solution by using hello **Console App (.NET Framework)** project template.</span></span> <span data-ttu-id="cd6a7-123">Upewnij się, że wersja platformy .NET hello jest 4.5.1 lub nowszej.</span><span class="sxs-lookup"><span data-stu-id="cd6a7-123">Make sure hello .NET Framework version is 4.5.1 or later.</span></span> <span data-ttu-id="cd6a7-124">Nazwa projektu hello **TriggerReboot**.</span><span class="sxs-lookup"><span data-stu-id="cd6a7-124">Name hello project **TriggerReboot**.</span></span>

    ![Nowy projekt Visual C# Windows Classic Desktop][img-createapp]

2. <span data-ttu-id="cd6a7-126">W Eksploratorze rozwiązań kliknij prawym przyciskiem myszy hello **TriggerReboot** projektu, a następnie kliknij przycisk **Zarządzaj pakietami NuGet**.</span><span class="sxs-lookup"><span data-stu-id="cd6a7-126">In Solution Explorer, right-click hello **TriggerReboot** project, and then click **Manage NuGet Packages**.</span></span>
3. <span data-ttu-id="cd6a7-127">W hello **Menedżera pakietów NuGet** wybierz **Przeglądaj**, wyszukaj **microsoft.azure.devices**, wybierz pozycję **zainstalować** tooinstall Witaj **Microsoft.Azure.Devices** pakietu i zaakceptuj warunki użytkowania hello.</span><span class="sxs-lookup"><span data-stu-id="cd6a7-127">In hello **NuGet Package Manager** window, select **Browse**, search for **microsoft.azure.devices**, select **Install** tooinstall hello **Microsoft.Azure.Devices** package, and accept hello terms of use.</span></span> <span data-ttu-id="cd6a7-128">Ta procedura pliki do pobrania, instaluje i dodaje toohello odwołanie [zestawu SDK usług Azure IoT] [ lnk-nuget-service-sdk] NuGet pakiet i jego zależności.</span><span class="sxs-lookup"><span data-stu-id="cd6a7-128">This procedure downloads, installs, and adds a reference toohello [Azure IoT service SDK][lnk-nuget-service-sdk] NuGet package and its dependencies.</span></span>

    ![Okno Menedżera pakietów NuGet][img-servicenuget]
4. <span data-ttu-id="cd6a7-130">Dodaj następujące hello `using` instrukcji u góry hello hello **Program.cs** pliku:</span><span class="sxs-lookup"><span data-stu-id="cd6a7-130">Add hello following `using` statements at hello top of hello **Program.cs** file:</span></span>
   
        using Microsoft.Azure.Devices;
        using Microsoft.Azure.Devices.Shared;
        
5. <span data-ttu-id="cd6a7-131">Dodaj następujące pola toohello hello **Program** klasy.</span><span class="sxs-lookup"><span data-stu-id="cd6a7-131">Add hello following fields toohello **Program** class.</span></span> <span data-ttu-id="cd6a7-132">Zastąp wartość symbolu zastępczego hello hello parametry połączenia Centrum IoT hello koncentratora, który został utworzony w poprzedniej sekcji hello i hello urządzenia docelowego.</span><span class="sxs-lookup"><span data-stu-id="cd6a7-132">Replace hello placeholder value with hello IoT Hub connection string for hello hub that you created in hello previous section and hello target device.</span></span>
   
        static RegistryManager registryManager;
        static string connString = "{iot hub connection string}";
        static ServiceClient client;
        static JobClient jobClient;
        static string targetDevice = "{deviceIdForTargetDevice}";
        
6. <span data-ttu-id="cd6a7-133">Dodaj następujące metody toohello hello **Program** klasy.</span><span class="sxs-lookup"><span data-stu-id="cd6a7-133">Add hello following method toohello **Program** class.</span></span>  <span data-ttu-id="cd6a7-134">Ten kod pobiera hello urządzenia dwie do ponownego uruchamiania urządzenia i danych wyjściowych hello hello zgłosił właściwości.</span><span class="sxs-lookup"><span data-stu-id="cd6a7-134">This code gets hello device twin for hello rebooting device and outputs hello reported properties.</span></span>
   
        public static async Task QueryTwinRebootReported()
        {
            Twin twin = await registryManager.GetTwinAsync(targetDevice);
            Console.WriteLine(twin.Properties.Reported.ToJson());
        }
        
7. <span data-ttu-id="cd6a7-135">Dodaj następujące metody toohello hello **Program** klasy.</span><span class="sxs-lookup"><span data-stu-id="cd6a7-135">Add hello following method toohello **Program** class.</span></span>  <span data-ttu-id="cd6a7-136">Ten kod inicjuje hello ponowne uruchomienie komputera, na urządzeniu hello przy użyciu metody bezpośredniego.</span><span class="sxs-lookup"><span data-stu-id="cd6a7-136">This code initiates hello reboot on hello device using a direct method.</span></span>

        public static async Task StartReboot()
        {
            client = ServiceClient.CreateFromConnectionString(connString);
            CloudToDeviceMethod method = new CloudToDeviceMethod("reboot");
            method.ResponseTimeout = TimeSpan.FromSeconds(30);

            CloudToDeviceMethodResult result = await client.InvokeDeviceMethodAsync(targetDevice, method);

            Console.WriteLine("Invoked firmware update on device.");
        }

7. <span data-ttu-id="cd6a7-137">Na koniec należy dodać następujące wiersze toohello hello **Main** metody:</span><span class="sxs-lookup"><span data-stu-id="cd6a7-137">Finally, add hello following lines toohello **Main** method:</span></span>
   
        registryManager = RegistryManager.CreateFromConnectionString(connString);
        StartReboot().Wait();
        QueryTwinRebootReported().Wait();
        Console.WriteLine("Press ENTER tooexit.");
        Console.ReadLine();
        
8. <span data-ttu-id="cd6a7-138">Utworzenie rozwiązania hello.</span><span class="sxs-lookup"><span data-stu-id="cd6a7-138">Build hello solution.</span></span>

## <a name="create-a-simulated-device-app"></a><span data-ttu-id="cd6a7-139">Tworzenie aplikacji symulowanego urządzenia</span><span class="sxs-lookup"><span data-stu-id="cd6a7-139">Create a simulated device app</span></span>
<span data-ttu-id="cd6a7-140">W tej sekcji zostanie</span><span class="sxs-lookup"><span data-stu-id="cd6a7-140">In this section, you will</span></span>

* <span data-ttu-id="cd6a7-141">Tworzenie aplikacji konsoli Node.js, które odpowiada metoda bezpośrednia tooa wywoływane przez hello chmury</span><span class="sxs-lookup"><span data-stu-id="cd6a7-141">Create a Node.js console app that responds tooa direct method called by hello cloud</span></span>
* <span data-ttu-id="cd6a7-142">Wyzwalacz symulowane urządzenie ponowny rozruch</span><span class="sxs-lookup"><span data-stu-id="cd6a7-142">Trigger a simulated device reboot</span></span>
* <span data-ttu-id="cd6a7-143">Hello używany zgłaszane właściwości tooenable urządzeń dwie zapytania tooidentify urządzenia, a podczas ich ostatniego ponownego uruchomienia</span><span class="sxs-lookup"><span data-stu-id="cd6a7-143">Use hello reported properties tooenable device twin queries tooidentify devices and when they last rebooted</span></span>

1. <span data-ttu-id="cd6a7-144">Utwórz nowy, pusty folder o nazwie **manageddevice**.</span><span class="sxs-lookup"><span data-stu-id="cd6a7-144">Create a new empty folder called **manageddevice**.</span></span>  <span data-ttu-id="cd6a7-145">W hello **manageddevice** folderu, Utwórz plik package.json za pomocą hello następujące polecenie z wiersza polecenia.</span><span class="sxs-lookup"><span data-stu-id="cd6a7-145">In hello **manageddevice** folder, create a package.json file using hello following command at your command prompt.</span></span>  <span data-ttu-id="cd6a7-146">Zaakceptuj wszystkie domyślne hello:</span><span class="sxs-lookup"><span data-stu-id="cd6a7-146">Accept all hello defaults:</span></span>
   
    ```
    npm init
    ```
2. <span data-ttu-id="cd6a7-147">Z wiersza polecenia w hello **manageddevice** folderu, uruchom następujące polecenie tooinstall hello hello **azure iot urządzenia** pakiet SDK urządzenia i **azure-iot urządzenie mqtt**pakietu:</span><span class="sxs-lookup"><span data-stu-id="cd6a7-147">At your command prompt in hello **manageddevice** folder, run hello following command tooinstall hello **azure-iot-device** Device SDK package and **azure-iot-device-mqtt** package:</span></span>
   
    ```
    npm install azure-iot-device azure-iot-device-mqtt --save
    ```
3. <span data-ttu-id="cd6a7-148">Za pomocą edytora tekstu, Utwórz nową **dmpatterns_getstarted_device.js** pliku w hello **manageddevice** folderu.</span><span class="sxs-lookup"><span data-stu-id="cd6a7-148">Using a text editor, create a new **dmpatterns_getstarted_device.js** file in hello **manageddevice** folder.</span></span>
4. <span data-ttu-id="cd6a7-149">Dodaj następujące hello "Wymagaj" instrukcje na początku hello hello **dmpatterns_getstarted_device.js** pliku:</span><span class="sxs-lookup"><span data-stu-id="cd6a7-149">Add hello following 'require' statements at hello start of hello **dmpatterns_getstarted_device.js** file:</span></span>
   
    ```
    'use strict';
   
    var Client = require('azure-iot-device').Client;
    var Protocol = require('azure-iot-device-mqtt').Mqtt;
    ```
5. <span data-ttu-id="cd6a7-150">Dodaj **connectionString** zmiennej i korzystać z niego toocreate **klienta** wystąpienia.</span><span class="sxs-lookup"><span data-stu-id="cd6a7-150">Add a **connectionString** variable and use it toocreate a **Client** instance.</span></span>  <span data-ttu-id="cd6a7-151">Zastąp ciąg połączenia hello parametrów połączenia urządzenia.</span><span class="sxs-lookup"><span data-stu-id="cd6a7-151">Replace hello connection string with your device connection string.</span></span>  
   
    ```
    var connectionString = 'HostName={youriothostname};DeviceId=myDeviceId;SharedAccessKey={yourdevicekey}';
    var client = Client.fromConnectionString(connectionString, Protocol);
    ```
6. <span data-ttu-id="cd6a7-152">Dodaj następujące metoda bezpośrednia hello tooimplement funkcji na urządzeniu hello hello</span><span class="sxs-lookup"><span data-stu-id="cd6a7-152">Add hello following function tooimplement hello direct method on hello device</span></span>
   
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
7. <span data-ttu-id="cd6a7-153">Dodaj następujący hello kodu centrum IoT tooyour tooopen hello połączenia i uruchomić odbiornik metoda bezpośrednia hello:</span><span class="sxs-lookup"><span data-stu-id="cd6a7-153">Add hello following code tooopen hello connection tooyour IoT hub and start hello direct method listener:</span></span>
   
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
8. <span data-ttu-id="cd6a7-154">Zapisz i zamknij hello **dmpatterns_getstarted_device.js** pliku.</span><span class="sxs-lookup"><span data-stu-id="cd6a7-154">Save and close hello **dmpatterns_getstarted_device.js** file.</span></span>
   
> [!NOTE]
> <span data-ttu-id="cd6a7-155">rzeczy tookeep proste, w tym samouczku nie implementuje wszystkie zasady ponawiania.</span><span class="sxs-lookup"><span data-stu-id="cd6a7-155">tookeep things simple, this tutorial does not implement any retry policy.</span></span> <span data-ttu-id="cd6a7-156">W kodzie produkcyjnym, należy zaimplementować zasady ponawiania (na przykład wykładniczego wycofywania), zgodnie z sugestią podaną w artykuł w witrynie MSDN hello [obsługi błędów przejściowych][lnk-transient-faults].</span><span class="sxs-lookup"><span data-stu-id="cd6a7-156">In production code, you should implement retry policies (such as an exponential backoff), as suggested in hello MSDN article [Transient Fault Handling][lnk-transient-faults].</span></span>


## <a name="run-hello-apps"></a><span data-ttu-id="cd6a7-157">Uruchamianie aplikacji hello</span><span class="sxs-lookup"><span data-stu-id="cd6a7-157">Run hello apps</span></span>
<span data-ttu-id="cd6a7-158">Wszystko jest teraz gotowy toorun hello aplikacji.</span><span class="sxs-lookup"><span data-stu-id="cd6a7-158">You are now ready toorun hello apps.</span></span>

1. <span data-ttu-id="cd6a7-159">W wierszu polecenia hello w hello **manageddevice** folderu Uruchom hello następujące polecenia toobegin nasłuchiwanie metoda bezpośrednia hello ponowny rozruch.</span><span class="sxs-lookup"><span data-stu-id="cd6a7-159">At hello command prompt in hello **manageddevice** folder, run hello following command toobegin listening for hello reboot direct method.</span></span>
   
    ```
    node dmpatterns_getstarted_device.js
    ```
2. <span data-ttu-id="cd6a7-160">Aplikacja konsoli uruchamiania hello C# **TriggerReboot**.</span><span class="sxs-lookup"><span data-stu-id="cd6a7-160">Run hello C# console app **TriggerReboot**.</span></span> <span data-ttu-id="cd6a7-161">Powitania kliknij prawym przyciskiem myszy **TriggerReboot** projektu, zaznacz **debugowania**, a następnie wybierz **Start nowe wystąpienie**.</span><span class="sxs-lookup"><span data-stu-id="cd6a7-161">Right-click hello **TriggerReboot** project, select **Debug**, and then select **Start new instance**.</span></span>

3. <span data-ttu-id="cd6a7-162">Zostanie wyświetlony hello urządzenia odpowiedzi toohello metoda bezpośrednia hello konsoli.</span><span class="sxs-lookup"><span data-stu-id="cd6a7-162">You see hello device response toohello direct method in hello console.</span></span>

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