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
# <a name="use-device-management-tooinitiate-a-device-firmware-update-netnode"></a><span data-ttu-id="32edc-104">Użyj tooinitiate zarządzania urządzenia aktualizacji oprogramowania układowego urządzenia (.NET/węzeł)</span><span class="sxs-lookup"><span data-stu-id="32edc-104">Use device management tooinitiate a device firmware update (.NET/Node)</span></span>
[!INCLUDE [iot-hub-selector-firmware-update](../../includes/iot-hub-selector-firmware-update.md)]

## <a name="introduction"></a><span data-ttu-id="32edc-105">Wprowadzenie</span><span class="sxs-lookup"><span data-stu-id="32edc-105">Introduction</span></span>
<span data-ttu-id="32edc-106">W hello [wprowadzenie do zarządzania urządzeniami] [ lnk-dm-getstarted] samouczku przedstawiono sposób toouse hello [dwie urządzenia] [ lnk-devtwin] i [bezpośredniego metody] [ lnk-c2dmethod] tooremotely podstawowych ponownego uruchamiania urządzenia.</span><span class="sxs-lookup"><span data-stu-id="32edc-106">In hello [Get started with device management][lnk-dm-getstarted] tutorial, you saw how toouse hello [device twin][lnk-devtwin] and [direct methods][lnk-c2dmethod] primitives tooremotely reboot a device.</span></span> <span data-ttu-id="32edc-107">Ten samouczek używa hello tego samego Centrum IoT elementów podstawowych i pokazuje, jak toodo end-to-end symulowane aktualizacji oprogramowania układowego.</span><span class="sxs-lookup"><span data-stu-id="32edc-107">This tutorial uses hello same IoT Hub primitives and shows you how toodo an end-to-end simulated firmware update.</span></span>  <span data-ttu-id="32edc-108">Ten wzorzec jest używany podczas wdrażania aktualizacji oprogramowania układowego powitania dla hello [Pi malina urządzenia implementacji próbki][lnk-rpi-implementation].</span><span class="sxs-lookup"><span data-stu-id="32edc-108">This pattern is used in hello firmware update implementation for hello [Raspberry Pi device implementation sample][lnk-rpi-implementation].</span></span>

<span data-ttu-id="32edc-109">Ten samouczek przedstawia sposób wykonania następujących czynności:</span><span class="sxs-lookup"><span data-stu-id="32edc-109">This tutorial shows you how to:</span></span>

* <span data-ttu-id="32edc-110">Tworzenie aplikacji konsoli .NET, który wywołuje metodę bezpośredniego firmwareUpdate hello w hello symulowane urządzenie aplikacji za pośrednictwem Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="32edc-110">Create a .NET console app that calls hello firmwareUpdate direct method in hello simulated device app through your IoT hub.</span></span>
* <span data-ttu-id="32edc-111">Tworzenie aplikacji symulowane urządzenie, który implementuje **firmwareUpdate** metoda bezpośrednia.</span><span class="sxs-lookup"><span data-stu-id="32edc-111">Create a simulated device app that implements a **firmwareUpdate** direct method.</span></span> <span data-ttu-id="32edc-112">Ta metoda inicjuje procesem wieloetapowym, która oczekuje toodownload hello oprogramowania układowego obrazu, pobierze obraz oprogramowania układowego hello i finally stosuje hello oprogramowania układowego obrazu.</span><span class="sxs-lookup"><span data-stu-id="32edc-112">This method initiates a multi-stage process that waits toodownload hello firmware image, downloads hello firmware image, and finally applies hello firmware image.</span></span> <span data-ttu-id="32edc-113">Podczas każdego etapu aktualizacji hello hello urządzenie używa hello zgłoszony tooreport właściwości w toku.</span><span class="sxs-lookup"><span data-stu-id="32edc-113">During each stage of hello update, hello device uses hello reported properties tooreport on progress.</span></span>

<span data-ttu-id="32edc-114">Na końcu hello tego samouczka masz aplikację Node.js konsoli urządzenia i zaplecza aplikacji konsoli .NET (C#):</span><span class="sxs-lookup"><span data-stu-id="32edc-114">At hello end of this tutorial, you have a Node.js console device app and a .NET (C#) console back-end app:</span></span>

<span data-ttu-id="32edc-115">**dmpatterns_fwupdate_service.js**, która wywołuje metodę bezpośrednio w aplikacji hello symulowane urządzenie Wyświetla hello odpowiedzi i okresowo (co 500 MS.) hello wyświetla zaktualizowane zgłoszone właściwości.</span><span class="sxs-lookup"><span data-stu-id="32edc-115">**dmpatterns_fwupdate_service.js**, which calls a direct method in hello simulated device app, displays hello response, and periodically (every 500ms) displays hello updated reported properties.</span></span>

<span data-ttu-id="32edc-116">**TriggerFWUpdate**, o tożsamości urządzenia hello utworzony wcześniej, który łączy Centrum IoT tooyour odbiera firmwareUpdate metoda bezpośrednia, jest uruchamiany za pośrednictwem toosimulate wielu stanu procesu aktualizacji oprogramowania układowego łącznie: Oczekiwanie na powitania pobrania obrazu, Trwa pobieranie hello nowy obraz, a na koniec stosowania obrazu hello.</span><span class="sxs-lookup"><span data-stu-id="32edc-116">**TriggerFWUpdate**, which connects tooyour IoT hub with hello device identity created earlier, receives a firmwareUpdate direct method, runs through a multi-state process toosimulate a firmware update including: waiting for hello image download, downloading hello new image, and finally applying hello image.</span></span>

<span data-ttu-id="32edc-117">toocomplete tego samouczka należy hello następujące:</span><span class="sxs-lookup"><span data-stu-id="32edc-117">toocomplete this tutorial, you need hello following:</span></span>

* <span data-ttu-id="32edc-118">Program Visual Studio 2015 lub Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="32edc-118">Visual Studio 2015 or Visual Studio 2017.</span></span>
* <span data-ttu-id="32edc-119">Środowisko node.js w wersji 0.12.x lub nowszym</span><span class="sxs-lookup"><span data-stu-id="32edc-119">Node.js version 0.12.x or later,</span></span> <br/>  <span data-ttu-id="32edc-120">[Przygotowywanie środowiska projektowego] [ lnk-dev-setup] w tym artykule opisano sposób tooinstall Node.js, w tym samouczku w systemie Windows lub Linux.</span><span class="sxs-lookup"><span data-stu-id="32edc-120">[Prepare your development environment][lnk-dev-setup] describes how tooinstall Node.js for this tutorial on either Windows or Linux.</span></span>
* <span data-ttu-id="32edc-121">Aktywne konto platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="32edc-121">An active Azure account.</span></span> <span data-ttu-id="32edc-122">(Jeśli go nie masz, możesz utworzyć [bezpłatne konto próbne][lnk-free-trial] w zaledwie kilka minut).</span><span class="sxs-lookup"><span data-stu-id="32edc-122">(If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.)</span></span>

<span data-ttu-id="32edc-123">Wykonaj hello [wprowadzenie do zarządzania urządzeniami](iot-hub-csharp-node-device-management-get-started.md) artykułu toocreate Centrum IoT i pobrać parametry połączenia Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="32edc-123">Follow hello [Get started with device management](iot-hub-csharp-node-device-management-get-started.md) article toocreate your IoT hub and get your IoT Hub connection string.</span></span>

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity](../../includes/iot-hub-get-started-create-device-identity.md)]

## <a name="trigger-a-remote-firmware-update-on-hello-device-using-a-direct-method"></a><span data-ttu-id="32edc-124">Wyzwalanie aktualizacji oprogramowania układowego zdalnego na urządzeniu hello za pomocą bezpośrednich — metoda</span><span class="sxs-lookup"><span data-stu-id="32edc-124">Trigger a remote firmware update on hello device using a direct method</span></span>
<span data-ttu-id="32edc-125">W tej sekcji służy do tworzenia aplikacji konsoli .NET (przy użyciu języka C#) inicjującym aktualizacji oprogramowania układowego zdalnego na urządzeniu.</span><span class="sxs-lookup"><span data-stu-id="32edc-125">In this section, you create a .NET console app (using C#) that initiates a remote firmware update on a device.</span></span> <span data-ttu-id="32edc-126">Aplikacja Hello korzysta z aktualizacją hello tooinitiate metoda bezpośrednia i używa urządzenia dwie zapytania tooperiodically Pobierz hello stan aktualizacji oprogramowania układowego active hello.</span><span class="sxs-lookup"><span data-stu-id="32edc-126">hello app uses a direct method tooinitiate hello update and uses device twin queries tooperiodically get hello status of hello active firmware update.</span></span>

1. <span data-ttu-id="32edc-127">W programie Visual Studio, należy dodać bieżącego rozwiązania toohello projektu Visual C# pulpitu systemu Windows klasycznego przy użyciu hello **aplikacji konsoli** szablonu projektu.</span><span class="sxs-lookup"><span data-stu-id="32edc-127">In Visual Studio, add a Visual C# Windows Classic Desktop project toohello current solution by using hello **Console Application** project template.</span></span> <span data-ttu-id="32edc-128">Nazwa projektu hello **TriggerFWUpdate**.</span><span class="sxs-lookup"><span data-stu-id="32edc-128">Name hello project **TriggerFWUpdate**.</span></span>

    ![Nowy projekt Visual C# Windows Classic Desktop][img-createapp]

1. <span data-ttu-id="32edc-130">W Eksploratorze rozwiązań kliknij prawym przyciskiem myszy hello **TriggerFWUpdate** projektu, a następnie kliknij przycisk **Zarządzaj pakietami NuGet...** .</span><span class="sxs-lookup"><span data-stu-id="32edc-130">In Solution Explorer, right-click hello **TriggerFWUpdate** project, and then click **Manage NuGet Packages...**.</span></span>
1. <span data-ttu-id="32edc-131">W hello **Menedżera pakietów NuGet** wybierz **Przeglądaj**, wyszukaj **microsoft.azure.devices**, wybierz pozycję **zainstalować** tooinstall Witaj **Microsoft.Azure.Devices** pakietu i zaakceptuj warunki użytkowania hello.</span><span class="sxs-lookup"><span data-stu-id="32edc-131">In hello **NuGet Package Manager** window, select **Browse**, search for **microsoft.azure.devices**, select **Install** tooinstall hello **Microsoft.Azure.Devices** package, and accept hello terms of use.</span></span> <span data-ttu-id="32edc-132">Ta procedura pliki do pobrania, instaluje i dodaje toohello odwołanie [zestawu SDK usług Azure IoT] [ lnk-nuget-service-sdk] NuGet pakiet i jego zależności.</span><span class="sxs-lookup"><span data-stu-id="32edc-132">This procedure downloads, installs, and adds a reference toohello [Azure IoT service SDK][lnk-nuget-service-sdk] NuGet package and its dependencies.</span></span>

    ![Okno Menedżera pakietów NuGet][img-servicenuget]
1. <span data-ttu-id="32edc-134">Dodaj następujące hello `using` instrukcji u góry hello hello **Program.cs** pliku:</span><span class="sxs-lookup"><span data-stu-id="32edc-134">Add hello following `using` statements at hello top of hello **Program.cs** file:</span></span>
   
        using Microsoft.Azure.Devices;
        using Microsoft.Azure.Devices.Shared;
        
1. <span data-ttu-id="32edc-135">Dodaj następujące pola toohello hello **Program** klasy.</span><span class="sxs-lookup"><span data-stu-id="32edc-135">Add hello following fields toohello **Program** class.</span></span> <span data-ttu-id="32edc-136">Zastąp hello wielu symbole zastępcze hello Centrum IoT ciąg połączenia dla koncentratora hello, który został utworzony w poprzedniej sekcji hello i hello identyfikator urządzenia.</span><span class="sxs-lookup"><span data-stu-id="32edc-136">Replace hello multiple placeholder values with hello IoT Hub connection string for hello hub that you created in hello previous section and hello Id of your device.</span></span>
   
        static RegistryManager registryManager;
        static string connString = "{iot hub connection string}";
        static ServiceClient client;
        static JobClient jobClient;
        static string targetDevice = "{deviceIdForTargetDevice}";
        
1. <span data-ttu-id="32edc-137">Dodaj następujące metody toohello hello **Program** klasy:</span><span class="sxs-lookup"><span data-stu-id="32edc-137">Add hello following method toohello **Program** class:</span></span>
   
        public static async Task QueryTwinFWUpdateReported()
        {
            Twin twin = await registryManager.GetTwinAsync(targetDevice);
            Console.WriteLine(twin.Properties.Reported.ToJson());
        }
        
1. <span data-ttu-id="32edc-138">Dodaj następujące metody toohello hello **Program** klasy:</span><span class="sxs-lookup"><span data-stu-id="32edc-138">Add hello following method toohello **Program** class:</span></span>

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

1. <span data-ttu-id="32edc-139">Na koniec należy dodać następujące wiersze toohello hello **Main** metody:</span><span class="sxs-lookup"><span data-stu-id="32edc-139">Finally, add hello following lines toohello **Main** method:</span></span>
   
        registryManager = RegistryManager.CreateFromConnectionString(connString);
        StartFirmwareUpdate().Wait();
        QueryTwinFWUpdateReported().Wait();
        Console.WriteLine("Press ENTER tooexit.");
        Console.ReadLine();
        
1. <span data-ttu-id="32edc-140">W Eksploratorze rozwiązań hello, otwórz hello **projektów startowych ustawić...**  i upewnij się, że hello **akcji** dla **TriggerFWUpdate** projekt jest **Start**.</span><span class="sxs-lookup"><span data-stu-id="32edc-140">In hello Solution Explorer, open hello **Set StartUp projects...** and make sure hello **Action** for **TriggerFWUpdate** project is **Start**.</span></span>

1. <span data-ttu-id="32edc-141">Utworzenie rozwiązania hello.</span><span class="sxs-lookup"><span data-stu-id="32edc-141">Build hello solution.</span></span>

[!INCLUDE [iot-hub-device-firmware-update](../../includes/iot-hub-device-firmware-update.md)]

## <a name="run-hello-apps"></a><span data-ttu-id="32edc-142">Uruchamianie aplikacji hello</span><span class="sxs-lookup"><span data-stu-id="32edc-142">Run hello apps</span></span>
<span data-ttu-id="32edc-143">Wszystko jest teraz gotowy toorun hello aplikacji.</span><span class="sxs-lookup"><span data-stu-id="32edc-143">You are now ready toorun hello apps.</span></span>

1. <span data-ttu-id="32edc-144">W wierszu polecenia hello w hello **manageddevice** folderu Uruchom hello następujące polecenia toobegin nasłuchiwanie metoda bezpośrednia hello ponowny rozruch.</span><span class="sxs-lookup"><span data-stu-id="32edc-144">At hello command prompt in hello **manageddevice** folder, run hello following command toobegin listening for hello reboot direct method.</span></span>
   
    ```
    node dmpatterns_fwupdate_device.js
    ```
2. <span data-ttu-id="32edc-145">W programie Visual Studio, kliknij prawym przyciskiem myszy hello **TriggerFWUpdate** projectRun toohello C# aplikacji konsoli, wybierz opcję **debugowania** i **Start nowe wystąpienie**.</span><span class="sxs-lookup"><span data-stu-id="32edc-145">In Visual Studio, right-click on hello **TriggerFWUpdate** projectRun toohello C# console app, select **Debug** and **Start new instance**.</span></span>

3. <span data-ttu-id="32edc-146">Zostanie wyświetlony hello urządzenia odpowiedzi toohello metoda bezpośrednia hello konsoli.</span><span class="sxs-lookup"><span data-stu-id="32edc-146">You see hello device response toohello direct method in hello console.</span></span>

    ![Pomyślnie zaktualizowano oprogramowania układowego][img-fwupdate]

## <a name="next-steps"></a><span data-ttu-id="32edc-148">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="32edc-148">Next steps</span></span>
<span data-ttu-id="32edc-149">W tym samouczku używana metoda bezpośrednia tootrigger zdalnej aktualizacji oprogramowania układowego na urządzeniach i hello używany zgłaszane postęp hello toofollow właściwości aktualizacji oprogramowania układowego hello.</span><span class="sxs-lookup"><span data-stu-id="32edc-149">In this tutorial, you used a direct method tootrigger a remote firmware update on a device and used hello reported properties toofollow hello progress of hello firmware update.</span></span>

<span data-ttu-id="32edc-150">toolearn tooextend IoT metody rozwiązania i harmonogram wywołuje na wielu urządzeniach, zobacz hello [emisji zadania i harmonogramu] [ lnk-tutorial-jobs] samouczka.</span><span class="sxs-lookup"><span data-stu-id="32edc-150">toolearn how tooextend your IoT solution and schedule method calls on multiple devices, see hello [Schedule and broadcast jobs][lnk-tutorial-jobs] tutorial.</span></span>

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