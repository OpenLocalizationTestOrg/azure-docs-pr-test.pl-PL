---
title: "Aktualizacja oprogramowania układowego urządzenia z Centrum IoT Azure (.NET/węzła) | Dokumentacja firmy Microsoft"
description: "Jak używać zarządzania urządzeniami w usłudze Azure IoT Hub zainicjować aktualizację oprogramowania układowego urządzenia. Przy użyciu urządzenia Azure IoT SDK dla środowiska Node.js aplikacji symulowane urządzenie i usługa Azure IoT SDK dla platformy .NET do implementacji usługi aplikacji, które wyzwala aktualizacji oprogramowania układowego."
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
ms.openlocfilehash: c2192328a152e955d182c4a07b391c98a5960964
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="use-device-management-to-initiate-a-device-firmware-update-netnode"></a><span data-ttu-id="3aaed-104">Umożliwia zarządzanie urządzeniami zainicjować aktualizację oprogramowania układowego urządzenia (.NET/węzeł)</span><span class="sxs-lookup"><span data-stu-id="3aaed-104">Use device management to initiate a device firmware update (.NET/Node)</span></span>
[!INCLUDE [iot-hub-selector-firmware-update](../../includes/iot-hub-selector-firmware-update.md)]

## <a name="introduction"></a><span data-ttu-id="3aaed-105">Wprowadzenie</span><span class="sxs-lookup"><span data-stu-id="3aaed-105">Introduction</span></span>
<span data-ttu-id="3aaed-106">W [wprowadzenie do zarządzania urządzeniami] [ lnk-dm-getstarted] samouczka przedstawiono sposób użycia [dwie urządzenia] [ lnk-devtwin] i [bezpośrednie metody ] [ lnk-c2dmethod] podstawowych zdalnie ponownego uruchomienia urządzenia.</span><span class="sxs-lookup"><span data-stu-id="3aaed-106">In the [Get started with device management][lnk-dm-getstarted] tutorial, you saw how to use the [device twin][lnk-devtwin] and [direct methods][lnk-c2dmethod] primitives to remotely reboot a device.</span></span> <span data-ttu-id="3aaed-107">Ten samouczek używa tego samego podstawowych Centrum IoT i pokazuje, jak wykonać aktualizację oprogramowania układowego symulowane end-to-end.</span><span class="sxs-lookup"><span data-stu-id="3aaed-107">This tutorial uses the same IoT Hub primitives and shows you how to do an end-to-end simulated firmware update.</span></span>  <span data-ttu-id="3aaed-108">Ten wzorzec jest używany w implementacji aktualizacji oprogramowania układowego dla [Pi malina urządzenia implementacji próbki][lnk-rpi-implementation].</span><span class="sxs-lookup"><span data-stu-id="3aaed-108">This pattern is used in the firmware update implementation for the [Raspberry Pi device implementation sample][lnk-rpi-implementation].</span></span>

<span data-ttu-id="3aaed-109">Ten samouczek przedstawia sposób wykonania następujących czynności:</span><span class="sxs-lookup"><span data-stu-id="3aaed-109">This tutorial shows you how to:</span></span>

* <span data-ttu-id="3aaed-110">Tworzenie aplikacji konsoli .NET, która wywołuje metodę firmwareUpdate bezpośrednio w aplikacji symulowane urządzenie za pomocą Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="3aaed-110">Create a .NET console app that calls the firmwareUpdate direct method in the simulated device app through your IoT hub.</span></span>
* <span data-ttu-id="3aaed-111">Tworzenie aplikacji symulowane urządzenie, który implementuje **firmwareUpdate** metoda bezpośrednia.</span><span class="sxs-lookup"><span data-stu-id="3aaed-111">Create a simulated device app that implements a **firmwareUpdate** direct method.</span></span> <span data-ttu-id="3aaed-112">Ta metoda inicjuje procesem wieloetapowym czeka na pobranie obrazu oprogramowania układowego, pobierze obraz oprogramowania układowego i na koniec dotyczy oprogramowania układowego obrazu.</span><span class="sxs-lookup"><span data-stu-id="3aaed-112">This method initiates a multi-stage process that waits to download the firmware image, downloads the firmware image, and finally applies the firmware image.</span></span> <span data-ttu-id="3aaed-113">Podczas każdego etapu aktualizacji urządzenie korzysta z właściwości zgłoszony do raport dotyczący postępu.</span><span class="sxs-lookup"><span data-stu-id="3aaed-113">During each stage of the update, the device uses the reported properties to report on progress.</span></span>

<span data-ttu-id="3aaed-114">Na końcu tego samouczka masz urządzenie aplikacji konsoli Node.js i zaplecza aplikacji konsoli .NET (C#):</span><span class="sxs-lookup"><span data-stu-id="3aaed-114">At the end of this tutorial, you have a Node.js console device app and a .NET (C#) console back-end app:</span></span>

<span data-ttu-id="3aaed-115">**dmpatterns_fwupdate_service.js**, która wywołuje metodę bezpośrednio w aplikacji symulowane urządzenie Wyświetla odpowiedzi i okresowo (co 500 MS.) Wyświetla zaktualizowanego zgłoszone właściwości.</span><span class="sxs-lookup"><span data-stu-id="3aaed-115">**dmpatterns_fwupdate_service.js**, which calls a direct method in the simulated device app, displays the response, and periodically (every 500ms) displays the updated reported properties.</span></span>

<span data-ttu-id="3aaed-116">**TriggerFWUpdate**, która łączy się z Centrum IoT z tożsamości urządzenia utworzony wcześniej, otrzymuje firmwareUpdate metoda bezpośrednia, uruchamia proces wielu stanu do symulowania, w tym aktualizacji oprogramowania układowego: Oczekiwanie na pobieranie obrazu Pobieranie nowy obraz, a na koniec stosowania obrazu.</span><span class="sxs-lookup"><span data-stu-id="3aaed-116">**TriggerFWUpdate**, which connects to your IoT hub with the device identity created earlier, receives a firmwareUpdate direct method, runs through a multi-state process to simulate a firmware update including: waiting for the image download, downloading the new image, and finally applying the image.</span></span>

<span data-ttu-id="3aaed-117">Do wykonania kroków tego samouczka niezbędne są następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="3aaed-117">To complete this tutorial, you need the following:</span></span>

* <span data-ttu-id="3aaed-118">Program Visual Studio 2015 lub Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="3aaed-118">Visual Studio 2015 or Visual Studio 2017.</span></span>
* <span data-ttu-id="3aaed-119">Środowisko node.js w wersji 0.12.x lub nowszym</span><span class="sxs-lookup"><span data-stu-id="3aaed-119">Node.js version 0.12.x or later,</span></span> <br/>  <span data-ttu-id="3aaed-120">[Przygotowywanie środowiska projektowego] [ lnk-dev-setup] opisuje sposób instalowania programu Node.js w tym samouczku w systemie Windows lub Linux.</span><span class="sxs-lookup"><span data-stu-id="3aaed-120">[Prepare your development environment][lnk-dev-setup] describes how to install Node.js for this tutorial on either Windows or Linux.</span></span>
* <span data-ttu-id="3aaed-121">Aktywne konto platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="3aaed-121">An active Azure account.</span></span> <span data-ttu-id="3aaed-122">(Jeśli go nie masz, możesz utworzyć [bezpłatne konto próbne][lnk-free-trial] w zaledwie kilka minut).</span><span class="sxs-lookup"><span data-stu-id="3aaed-122">(If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.)</span></span>

<span data-ttu-id="3aaed-123">Postępuj zgodnie z [wprowadzenie do zarządzania urządzeniami](iot-hub-csharp-node-device-management-get-started.md) artykuł, aby utworzyć Centrum IoT i pobrać parametry połączenia Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="3aaed-123">Follow the [Get started with device management](iot-hub-csharp-node-device-management-get-started.md) article to create your IoT hub and get your IoT Hub connection string.</span></span>

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity](../../includes/iot-hub-get-started-create-device-identity.md)]

## <a name="trigger-a-remote-firmware-update-on-the-device-using-a-direct-method"></a><span data-ttu-id="3aaed-124">Wyzwalanie aktualizacji oprogramowania układowego zdalnego na urządzeniu, za pomocą bezpośrednich — metoda</span><span class="sxs-lookup"><span data-stu-id="3aaed-124">Trigger a remote firmware update on the device using a direct method</span></span>
<span data-ttu-id="3aaed-125">W tej sekcji służy do tworzenia aplikacji konsoli .NET (przy użyciu języka C#) inicjującym aktualizacji oprogramowania układowego zdalnego na urządzeniu.</span><span class="sxs-lookup"><span data-stu-id="3aaed-125">In this section, you create a .NET console app (using C#) that initiates a remote firmware update on a device.</span></span> <span data-ttu-id="3aaed-126">Aplikacja korzysta metoda bezpośrednia zainicjować aktualizację, a zapytania dwie urządzenia okresowo pobrać stanu aktualizacji oprogramowania układowego active.</span><span class="sxs-lookup"><span data-stu-id="3aaed-126">The app uses a direct method to initiate the update and uses device twin queries to periodically get the status of the active firmware update.</span></span>

1. <span data-ttu-id="3aaed-127">W programie Visual Studio dodaj projekt Visual C# Windows Classic Desktop do bieżącego rozwiązania przy użyciu szablonu projektu **Aplikacja konsolowa**.</span><span class="sxs-lookup"><span data-stu-id="3aaed-127">In Visual Studio, add a Visual C# Windows Classic Desktop project to the current solution by using the **Console Application** project template.</span></span> <span data-ttu-id="3aaed-128">Nazwij projekt **TriggerFWUpdate**.</span><span class="sxs-lookup"><span data-stu-id="3aaed-128">Name the project **TriggerFWUpdate**.</span></span>

    ![Nowy projekt Visual C# Windows Classic Desktop][img-createapp]

1. <span data-ttu-id="3aaed-130">W Eksploratorze rozwiązań kliknij prawym przyciskiem myszy **TriggerFWUpdate** projektu, a następnie kliknij przycisk **Zarządzaj pakietami NuGet...** .</span><span class="sxs-lookup"><span data-stu-id="3aaed-130">In Solution Explorer, right-click the **TriggerFWUpdate** project, and then click **Manage NuGet Packages...**.</span></span>
1. <span data-ttu-id="3aaed-131">W oknie **Menedżer pakietów NuGet** wybierz opcję **Przeglądaj**, wyszukaj pozycję **microsoft.azure.devices**, wybierz opcję **Zainstaluj**, aby zainstalować pakiet **Microsoft.Azure.Devices**, i zaakceptuj warunki użytkowania.</span><span class="sxs-lookup"><span data-stu-id="3aaed-131">In the **NuGet Package Manager** window, select **Browse**, search for **microsoft.azure.devices**, select **Install** to install the **Microsoft.Azure.Devices** package, and accept the terms of use.</span></span> <span data-ttu-id="3aaed-132">Ta procedura spowoduje pobranie, zainstalowanie i dodanie odwołania do pakietu NuGet [zestawu SDK usługi Azure IoT][lnk-nuget-service-sdk] oraz jego zależności.</span><span class="sxs-lookup"><span data-stu-id="3aaed-132">This procedure downloads, installs, and adds a reference to the [Azure IoT service SDK][lnk-nuget-service-sdk] NuGet package and its dependencies.</span></span>

    ![Okno Menedżera pakietów NuGet][img-servicenuget]
1. <span data-ttu-id="3aaed-134">Dodaj następujące instrukcje `using` w górnej części pliku **Program.cs**:</span><span class="sxs-lookup"><span data-stu-id="3aaed-134">Add the following `using` statements at the top of the **Program.cs** file:</span></span>
   
        using Microsoft.Azure.Devices;
        using Microsoft.Azure.Devices.Shared;
        
1. <span data-ttu-id="3aaed-135">Dodaj następujące pola do klasy **Program**:</span><span class="sxs-lookup"><span data-stu-id="3aaed-135">Add the following fields to the **Program** class.</span></span> <span data-ttu-id="3aaed-136">Zastąp symbole zastępcze wielu Centrum IoT ciąg połączenia dla koncentratora, który został utworzony w poprzedniej sekcji oraz identyfikator urządzenia.</span><span class="sxs-lookup"><span data-stu-id="3aaed-136">Replace the multiple placeholder values with the IoT Hub connection string for the hub that you created in the previous section and the Id of your device.</span></span>
   
        static RegistryManager registryManager;
        static string connString = "{iot hub connection string}";
        static ServiceClient client;
        static JobClient jobClient;
        static string targetDevice = "{deviceIdForTargetDevice}";
        
1. <span data-ttu-id="3aaed-137">Dodaj następującą metodę do klasy **Program**:</span><span class="sxs-lookup"><span data-stu-id="3aaed-137">Add the following method to the **Program** class:</span></span>
   
        public static async Task QueryTwinFWUpdateReported()
        {
            Twin twin = await registryManager.GetTwinAsync(targetDevice);
            Console.WriteLine(twin.Properties.Reported.ToJson());
        }
        
1. <span data-ttu-id="3aaed-138">Dodaj następującą metodę do klasy **Program**:</span><span class="sxs-lookup"><span data-stu-id="3aaed-138">Add the following method to the **Program** class:</span></span>

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

1. <span data-ttu-id="3aaed-139">Na koniec dodaj następujące wiersze do metody **Główne**:</span><span class="sxs-lookup"><span data-stu-id="3aaed-139">Finally, add the following lines to the **Main** method:</span></span>
   
        registryManager = RegistryManager.CreateFromConnectionString(connString);
        StartFirmwareUpdate().Wait();
        QueryTwinFWUpdateReported().Wait();
        Console.WriteLine("Press ENTER to exit.");
        Console.ReadLine();
        
1. <span data-ttu-id="3aaed-140">W Eksploratorze rozwiązań Otwórz **projektów startowych ustawić...**  i upewnij się, że **akcji** dla **TriggerFWUpdate** projekt jest **Start**.</span><span class="sxs-lookup"><span data-stu-id="3aaed-140">In the Solution Explorer, open the **Set StartUp projects...** and make sure the **Action** for **TriggerFWUpdate** project is **Start**.</span></span>

1. <span data-ttu-id="3aaed-141">Skompiluj rozwiązanie.</span><span class="sxs-lookup"><span data-stu-id="3aaed-141">Build the solution.</span></span>

[!INCLUDE [iot-hub-device-firmware-update](../../includes/iot-hub-device-firmware-update.md)]

## <a name="run-the-apps"></a><span data-ttu-id="3aaed-142">Uruchamianie aplikacji</span><span class="sxs-lookup"><span data-stu-id="3aaed-142">Run the apps</span></span>
<span data-ttu-id="3aaed-143">Teraz można przystąpić do uruchomienia aplikacji.</span><span class="sxs-lookup"><span data-stu-id="3aaed-143">You are now ready to run the apps.</span></span>

1. <span data-ttu-id="3aaed-144">W wierszu polecenia w **manageddevice** folderu, uruchom następujące polecenie Rozpoczęcie nasłuchiwania metoda bezpośrednia ponowne uruchomienie komputera.</span><span class="sxs-lookup"><span data-stu-id="3aaed-144">At the command prompt in the **manageddevice** folder, run the following command to begin listening for the reboot direct method.</span></span>
   
    ```
    node dmpatterns_fwupdate_device.js
    ```
2. <span data-ttu-id="3aaed-145">W programie Visual Studio, kliknij prawym przyciskiem myszy **TriggerFWUpdate** projectRun w języku C# aplikacji konsoli, wybierz **debugowania** i **Start nowe wystąpienie**.</span><span class="sxs-lookup"><span data-stu-id="3aaed-145">In Visual Studio, right-click on the **TriggerFWUpdate** projectRun to the C# console app, select **Debug** and **Start new instance**.</span></span>

3. <span data-ttu-id="3aaed-146">Zobaczysz odpowiedź urządzenia do metody bezpośrednio w konsoli.</span><span class="sxs-lookup"><span data-stu-id="3aaed-146">You see the device response to the direct method in the console.</span></span>

    ![Pomyślnie zaktualizowano oprogramowania układowego][img-fwupdate]

## <a name="next-steps"></a><span data-ttu-id="3aaed-148">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="3aaed-148">Next steps</span></span>
<span data-ttu-id="3aaed-149">W tym samouczku używana metoda bezpośrednia do wyzwolenia aktualizacji oprogramowania układowego zdalnego na urządzeniu i można śledzić postępy aktualizacji oprogramowania układowego zgłoszone właściwości.</span><span class="sxs-lookup"><span data-stu-id="3aaed-149">In this tutorial, you used a direct method to trigger a remote firmware update on a device and used the reported properties to follow the progress of the firmware update.</span></span>

<span data-ttu-id="3aaed-150">Aby dowiedzieć się, jak rozszerzyć IoT, Twoje rozwiązanie i harmonogram metoda wywołuje na wielu urządzeniach, zobacz [emisji zadania i harmonogramu] [ lnk-tutorial-jobs] samouczka.</span><span class="sxs-lookup"><span data-stu-id="3aaed-150">To learn how to extend your IoT solution and schedule method calls on multiple devices, see the [Schedule and broadcast jobs][lnk-tutorial-jobs] tutorial.</span></span>

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