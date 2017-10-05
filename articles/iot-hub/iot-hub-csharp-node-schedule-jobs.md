---
title: "Planowanie zadań z Centrum IoT Azure (.NET/węzła) | Dokumentacja firmy Microsoft"
description: "Sposób tworzenia harmonogramu zadań Centrum IoT Azure do wywołania metody bezpośrednio na wielu urządzeniach. Urządzenia Azure IoT SDK dla środowiska Node.js umożliwia wdrożenie symulowane urządzenie aplikacje i usługi Azure IoT SDK dla platformy .NET do implementacji usługi aplikacji, aby uruchomić to zadanie."
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
ms.openlocfilehash: a8f4f34aa99c4a9966957cac213ec9170de80a46
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="schedule-and-broadcast-jobs-netnodejs"></a><span data-ttu-id="cd48a-104">Zadania harmonogramu i emisji (.NET/Node.js)</span><span class="sxs-lookup"><span data-stu-id="cd48a-104">Schedule and broadcast jobs (.NET/Node.js)</span></span>

[!INCLUDE [iot-hub-selector-schedule-jobs](../../includes/iot-hub-selector-schedule-jobs.md)]

<span data-ttu-id="cd48a-105">Użyj Centrum IoT Azure do planowania i śledzenia zadań, które aktualizują milionów urządzeń.</span><span class="sxs-lookup"><span data-stu-id="cd48a-105">Use Azure IoT Hub to schedule and track jobs that update millions of devices.</span></span> <span data-ttu-id="cd48a-106">Należy użyć zadania, aby:</span><span class="sxs-lookup"><span data-stu-id="cd48a-106">Use jobs to:</span></span>

* <span data-ttu-id="cd48a-107">Aktualizowanie żądanych właściwości</span><span class="sxs-lookup"><span data-stu-id="cd48a-107">Update desired properties</span></span>
* <span data-ttu-id="cd48a-108">Tagi aktualizacji</span><span class="sxs-lookup"><span data-stu-id="cd48a-108">Update tags</span></span>
* <span data-ttu-id="cd48a-109">Wywołanie metody bezpośredniego</span><span class="sxs-lookup"><span data-stu-id="cd48a-109">Invoke direct methods</span></span>

<span data-ttu-id="cd48a-110">Zadanie opakowuje jedną z następujących czynności i śledzi wykonanie względem zbiór urządzeń jest definiowana za pomocą zapytania dwie urządzenia.</span><span class="sxs-lookup"><span data-stu-id="cd48a-110">A job wraps one of these actions and tracks the execution against a set of devices that is defined by a device twin query.</span></span> <span data-ttu-id="cd48a-111">Na przykład aplikacji zaplecza zadanie służy do wywołania metody bezpośrednie na 10 000 urządzeń, które ponownym uruchomieniu urządzenia.</span><span class="sxs-lookup"><span data-stu-id="cd48a-111">For example, a back-end app can use a job to invoke a direct method on 10,000 devices that reboots the devices.</span></span> <span data-ttu-id="cd48a-112">Określ zbiór urządzeń za pomocą kwerendy dwie urządzenia i zaplanować zadania do uruchomienia w przyszłości.</span><span class="sxs-lookup"><span data-stu-id="cd48a-112">You specify the set of devices with a device twin query and schedule the job to run at a future time.</span></span> <span data-ttu-id="cd48a-113">Śledzi postęp zadania jako każdego urządzenia odbierają i wykonać metoda bezpośrednia ponowny rozruch.</span><span class="sxs-lookup"><span data-stu-id="cd48a-113">The job tracks progress as each of the devices receive and execute the reboot direct method.</span></span>

<span data-ttu-id="cd48a-114">Aby dowiedzieć się więcej na temat każdego z tych funkcji, zobacz:</span><span class="sxs-lookup"><span data-stu-id="cd48a-114">To learn more about each of these capabilities, see:</span></span>

* <span data-ttu-id="cd48a-115">Dwie urządzeń i właściwości: [Rozpoczynanie pracy z urządzenia twins] [ lnk-get-started-twin] i [samouczek: sposób użycia właściwości dwie urządzenia][lnk-twin-props]</span><span class="sxs-lookup"><span data-stu-id="cd48a-115">Device twin and properties: [Get started with device twins][lnk-get-started-twin] and [Tutorial: How to use device twin properties][lnk-twin-props]</span></span>
* <span data-ttu-id="cd48a-116">Bezpośrednie metody: [przewodnik dewelopera Centrum IoT — metody bezpośredniego] [ lnk-dev-methods] i [samouczek: bezpośrednie metody][lnk-c2d-methods]</span><span class="sxs-lookup"><span data-stu-id="cd48a-116">Direct methods: [IoT Hub developer guide - direct methods][lnk-dev-methods] and [Tutorial: Use direct methods][lnk-c2d-methods]</span></span>

<span data-ttu-id="cd48a-117">Ten samouczek przedstawia sposób wykonania następujących czynności:</span><span class="sxs-lookup"><span data-stu-id="cd48a-117">This tutorial shows you how to:</span></span>

* <span data-ttu-id="cd48a-118">Tworzenie aplikacji urządzenia implementujący bezpośredniego metodę o nazwie **lockDoor** który można wywołać za pomocą aplikacji zaplecza.</span><span class="sxs-lookup"><span data-stu-id="cd48a-118">Create a device app that implements a direct method called **lockDoor** that can be called by the back-end app.</span></span> <span data-ttu-id="cd48a-119">Aplikacji urządzenia Ponadto otrzymuje żądanej właściwości zmiany z poziomu aplikacji zaplecza.</span><span class="sxs-lookup"><span data-stu-id="cd48a-119">The device app also receives desired property changes from the back-end app.</span></span>
* <span data-ttu-id="cd48a-120">Tworzenie aplikacji zaplecza, która tworzy zadanie, aby wywołać **lockDoor** metoda bezpośrednia na wielu urządzeniach.</span><span class="sxs-lookup"><span data-stu-id="cd48a-120">Create a back-end app that creates a job to call the **lockDoor** direct method on multiple devices.</span></span> <span data-ttu-id="cd48a-121">Inne zadanie po zaakceptowaniu żądanej właściwości na wielu urządzeniach.</span><span class="sxs-lookup"><span data-stu-id="cd48a-121">Another job sends desired property updates to multiple devices.</span></span>

<span data-ttu-id="cd48a-122">Na końcu tego samouczka masz urządzenie aplikacji konsoli Node.js i zaplecza aplikacji konsoli .NET (C#):</span><span class="sxs-lookup"><span data-stu-id="cd48a-122">At the end of this tutorial, you have a Node.js console device app and a .NET (C#) console back-end app:</span></span>

<span data-ttu-id="cd48a-123">**simDevice.js** które nawiązuje połączenie z Centrum IoT, implementuje **lockDoor** bezpośrednie — metoda i uchwytów potrzebne zmiany właściwości.</span><span class="sxs-lookup"><span data-stu-id="cd48a-123">**simDevice.js** that connects to your IoT hub, implements the **lockDoor** direct method, and handles desired property changes.</span></span>

<span data-ttu-id="cd48a-124">**ScheduleJob** używającą zadania do wywołania **lockDoor** metoda bezpośrednia i zaktualizuj właściwości dwie żądanego urządzenia na wielu urządzeniach.</span><span class="sxs-lookup"><span data-stu-id="cd48a-124">**ScheduleJob** that uses jobs to call the **lockDoor** direct method and update the device twin desired properties on multiple devices.</span></span>

<span data-ttu-id="cd48a-125">Do wykonania kroków tego samouczka niezbędne są następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="cd48a-125">To complete this tutorial, you need the following:</span></span>

* <span data-ttu-id="cd48a-126">Program Visual Studio 2015 lub Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="cd48a-126">Visual Studio 2015 or Visual Studio 2017.</span></span>
* <span data-ttu-id="cd48a-127">Środowisko Node.js w wersji 0.12.x lub nowszej.</span><span class="sxs-lookup"><span data-stu-id="cd48a-127">Node.js version 0.12.x or later.</span></span> <span data-ttu-id="cd48a-128">Artykuł [przygotowywanie środowiska projektowego] [ lnk-dev-setup] opisuje sposób instalowania programu Node.js w tym samouczku w systemie Windows lub Linux.</span><span class="sxs-lookup"><span data-stu-id="cd48a-128">The article [Prepare your development environment][lnk-dev-setup] describes how to install Node.js for this tutorial on either Windows or Linux.</span></span>
* <span data-ttu-id="cd48a-129">Aktywne konto platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="cd48a-129">An active Azure account.</span></span> <span data-ttu-id="cd48a-130">Jeśli go nie masz, możesz utworzyć [bezpłatne konto][lnk-free-trial] w zaledwie kilka minut.</span><span class="sxs-lookup"><span data-stu-id="cd48a-130">If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.</span></span>

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity](../../includes/iot-hub-get-started-create-device-identity.md)]

## <a name="schedule-jobs-for-calling-a-direct-method-and-sending-device-twin-updates"></a><span data-ttu-id="cd48a-131">Planowanie zadań dla wywołania metody bezpośredniego i wysyłania aktualizacji dwie urządzenia</span><span class="sxs-lookup"><span data-stu-id="cd48a-131">Schedule jobs for calling a direct method and sending device twin updates</span></span>

<span data-ttu-id="cd48a-132">W tej sekcji Tworzenie aplikacji konsoli .NET (przy użyciu języka C#) korzystającą z zadań w celu wywołania **lockDoor** metoda bezpośrednia i wysyłać aktualizacje żądanej właściwości na wielu urządzeniach.</span><span class="sxs-lookup"><span data-stu-id="cd48a-132">In this section, you create a .NET console app (using C#) that uses jobs to call the **lockDoor** direct method and send desired property updates to multiple devices.</span></span>

1. <span data-ttu-id="cd48a-133">W programie Visual Studio dodaj projekt Visual C# Windows Classic Desktop do bieżącego rozwiązania przy użyciu szablonu projektu **Aplikacja konsolowa**.</span><span class="sxs-lookup"><span data-stu-id="cd48a-133">In Visual Studio, add a Visual C# Windows Classic Desktop project to the current solution by using the **Console Application** project template.</span></span> <span data-ttu-id="cd48a-134">Nazwij projekt **ScheduleJob**.</span><span class="sxs-lookup"><span data-stu-id="cd48a-134">Name the project **ScheduleJob**.</span></span>

    ![Nowy projekt Visual C# Windows Classic Desktop][img-createapp]

1. <span data-ttu-id="cd48a-136">W Eksploratorze rozwiązań kliknij prawym przyciskiem myszy **ScheduleJob** projektu, a następnie kliknij przycisk **Zarządzaj pakietami NuGet...** .</span><span class="sxs-lookup"><span data-stu-id="cd48a-136">In Solution Explorer, right-click the **ScheduleJob** project, and then click **Manage NuGet Packages...**.</span></span>
1. <span data-ttu-id="cd48a-137">W oknie **Menedżer pakietów NuGet** wybierz opcję **Przeglądaj**, wyszukaj pozycję **microsoft.azure.devices**, wybierz opcję **Zainstaluj**, aby zainstalować pakiet **Microsoft.Azure.Devices**, i zaakceptuj warunki użytkowania.</span><span class="sxs-lookup"><span data-stu-id="cd48a-137">In the **NuGet Package Manager** window, select **Browse**, search for **microsoft.azure.devices**, select **Install** to install the **Microsoft.Azure.Devices** package, and accept the terms of use.</span></span> <span data-ttu-id="cd48a-138">Ten krok pliki do pobrania, instaluje i dodaje odwołanie do [zestawu SDK usług Azure IoT] [ lnk-nuget-service-sdk] NuGet pakiet i jego zależności.</span><span class="sxs-lookup"><span data-stu-id="cd48a-138">This step downloads, installs, and adds a reference to the [Azure IoT service SDK][lnk-nuget-service-sdk] NuGet package and its dependencies.</span></span>

    ![Okno Menedżera pakietów NuGet][img-servicenuget]
1. <span data-ttu-id="cd48a-140">Dodaj następujące instrukcje `using` w górnej części pliku **Program.cs**:</span><span class="sxs-lookup"><span data-stu-id="cd48a-140">Add the following `using` statements at the top of the **Program.cs** file:</span></span>
    
    ```csharp
    using Microsoft.Azure.Devices;
    using Microsoft.Azure.Devices.Shared;
    ```

1. <span data-ttu-id="cd48a-141">Dodaj następujące `using` instrukcję, jeśli jeszcze nie istnieje w instrukcjach domyślne.</span><span class="sxs-lookup"><span data-stu-id="cd48a-141">Add the following `using` statement if not already present in the default statements.</span></span>

    ```csharp
    using System.Threading.Tasks;
    ```

1. <span data-ttu-id="cd48a-142">Dodaj następujące pola do klasy **Program**:</span><span class="sxs-lookup"><span data-stu-id="cd48a-142">Add the following fields to the **Program** class.</span></span> <span data-ttu-id="cd48a-143">Zastąp symbol zastępczy parametrów połączenia Centrum IoT dla koncentratora, który został utworzony w poprzedniej sekcji.</span><span class="sxs-lookup"><span data-stu-id="cd48a-143">Replace the placeholder with the IoT Hub connection string for the hub that you created in the previous section.</span></span>

    ```csharp
    static string connString = "{iot hub connection string}";
    static ServiceClient client;
    static JobClient jobClient;
    ```

1. <span data-ttu-id="cd48a-144">Dodaj następującą metodę do klasy **Program**:</span><span class="sxs-lookup"><span data-stu-id="cd48a-144">Add the following method to the **Program** class:</span></span>

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

1. <span data-ttu-id="cd48a-145">Dodaj następującą metodę do klasy **Program**:</span><span class="sxs-lookup"><span data-stu-id="cd48a-145">Add the following method to the **Program** class:</span></span>

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

1. <span data-ttu-id="cd48a-146">Dodaj następującą metodę do klasy **Program**:</span><span class="sxs-lookup"><span data-stu-id="cd48a-146">Add the following method to the **Program** class:</span></span>

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

1. <span data-ttu-id="cd48a-147">Na koniec dodaj następujące wiersze do metody **Główne**:</span><span class="sxs-lookup"><span data-stu-id="cd48a-147">Finally, add the following lines to the **Main** method:</span></span>

    ```csharp
    jobClient = JobClient.CreateFromConnectionString(connString);

    string methodJobId = Guid.NewGuid().ToString();

    StartMethodJob(methodJobId);
    MonitorJob(methodJobId).Wait();
    Console.WriteLine("Press ENTER to run the next job.");
    Console.ReadLine();

    string twinUpdateJobId = Guid.NewGuid().ToString();

    StartTwinUpdateJob(twinUpdateJobId);
    MonitorJob(twinUpdateJobId).Wait();
    Console.WriteLine("Press ENTER to exit.");
    Console.ReadLine();
    ```

1. <span data-ttu-id="cd48a-148">W Eksploratorze rozwiązań Otwórz **projektów startowych ustawić...**  i upewnij się, że **akcji** dla **ScheduleJob** projekt jest **Start**.</span><span class="sxs-lookup"><span data-stu-id="cd48a-148">In the Solution Explorer, open the **Set StartUp projects...** and make sure the **Action** for **ScheduleJob** project is **Start**.</span></span> <span data-ttu-id="cd48a-149">Skompiluj rozwiązanie.</span><span class="sxs-lookup"><span data-stu-id="cd48a-149">Build the solution.</span></span>

## <a name="create-a-simulated-device-app"></a><span data-ttu-id="cd48a-150">Tworzenie aplikacji symulowanego urządzenia</span><span class="sxs-lookup"><span data-stu-id="cd48a-150">Create a simulated device app</span></span>

<span data-ttu-id="cd48a-151">W tej sekcji utworzysz aplikację konsoli Node.js, która odpowiada na bezpośrednie metody wywoływane przez chmury, które wyzwala ponowne uruchomienie symulowane urządzenie i używa właściwości zgłoszone, aby umożliwić zapytania dwie urządzenia w celu identyfikowania urządzeń, a podczas ich ostatniego ponownego uruchomienia.</span><span class="sxs-lookup"><span data-stu-id="cd48a-151">In this section, you create a Node.js console app that responds to a direct method called by the cloud, which triggers a simulated device reboot and uses the reported properties to enable device twin queries to identify devices and when they last rebooted.</span></span>

1. <span data-ttu-id="cd48a-152">Utwórz nowy, pusty folder o nazwie **simDevice**.</span><span class="sxs-lookup"><span data-stu-id="cd48a-152">Create a new empty folder called **simDevice**.</span></span>  <span data-ttu-id="cd48a-153">W **simDevice** folderu, Utwórz plik package.json za pomocą następującego polecenia z wiersza polecenia.</span><span class="sxs-lookup"><span data-stu-id="cd48a-153">In the **simDevice** folder, create a package.json file using the following command at your command prompt.</span></span>  <span data-ttu-id="cd48a-154">Zaakceptuj wszystkie ustawienia domyślne:</span><span class="sxs-lookup"><span data-stu-id="cd48a-154">Accept all the defaults:</span></span>

    ```cmd/sh
    npm init
    ```

1. <span data-ttu-id="cd48a-155">Z wiersza polecenia w **simDevice** folderu, uruchom następujące polecenie, aby zainstalować **azure iot urządzenia** i **azure-iot urządzenie mqtt** pakiety:</span><span class="sxs-lookup"><span data-stu-id="cd48a-155">At your command prompt in the **simDevice** folder, run the following command to install the **azure-iot-device** and **azure-iot-device-mqtt** packages:</span></span>

    ```cmd/sh
    npm install azure-iot-device azure-iot-device-mqtt --save
    ```

1. <span data-ttu-id="cd48a-156">Za pomocą edytora tekstu, Utwórz nową **simDevice.js** w pliku **simDevice** folderu.</span><span class="sxs-lookup"><span data-stu-id="cd48a-156">Using a text editor, create a new **simDevice.js** file in the **simDevice** folder.</span></span>

1. <span data-ttu-id="cd48a-157">Dodaj następujące "wymagane" instrukcje na początku **simDevice.js** pliku:</span><span class="sxs-lookup"><span data-stu-id="cd48a-157">Add the following 'require' statements at the start of the **simDevice.js** file:</span></span>

    ```nodejs
    'use strict';
   
    var Client = require('azure-iot-device').Client;
    var Protocol = require('azure-iot-device-mqtt').Mqtt;
    ```

1. <span data-ttu-id="cd48a-158">Dodaj zmienną **connectionString** i użyj jej do utworzenia wystąpienia **Client**.</span><span class="sxs-lookup"><span data-stu-id="cd48a-158">Add a **connectionString** variable and use it to create a **Client** instance.</span></span> <span data-ttu-id="cd48a-159">Upewnij się zastąpić symbole zastępcze wartości ustawień.</span><span class="sxs-lookup"><span data-stu-id="cd48a-159">Make sure to replace the placeholders with values appropriate to your setup.</span></span>

    ```nodejs
    var connectionString = 'HostName={youriothostname};DeviceId={yourdeviceid};SharedAccessKey={yourdevicekey}';
    var client = Client.fromConnectionString(connectionString, Protocol);
    ```

1. <span data-ttu-id="cd48a-160">Dodaj następującą funkcję obsługi **lockDoor** metody.</span><span class="sxs-lookup"><span data-stu-id="cd48a-160">Add the following function to handle the **lockDoor** method.</span></span>

    ```nodejs
    var onLockDoor = function(request, response) {
   
        // Respond the cloud app for the direct method
        response.send(200, function(err) {
            if (!err) {
                console.error('An error occured when sending a method response:\n' + err.toString());
            } else {
                console.log('Response to method \'' + request.methodName + '\' sent successfully.');
            }
        });
   
        console.log('Locking Door!');
    };
    ```

1. <span data-ttu-id="cd48a-161">Dodaj następujący kod, aby zarejestrować obsługi dla **lockDoor** metody.</span><span class="sxs-lookup"><span data-stu-id="cd48a-161">Add the following code to register the handler for the **lockDoor** method.</span></span>

    ```nodejs
    client.open(function(err) {
        if (err) {
            console.error('Could not connect to IotHub client.');
        }  else {
            console.log('Client connected to IoT Hub.  Waiting for lockDoor direct method.');
            client.onDeviceMethod('lockDoor', onLockDoor);
        }
    });
    ```

1. <span data-ttu-id="cd48a-162">Zapisz i Zamknij **simDevice.js** pliku.</span><span class="sxs-lookup"><span data-stu-id="cd48a-162">Save and close the **simDevice.js** file.</span></span>

> [!NOTE]
> <span data-ttu-id="cd48a-163">Dla uproszczenia ten samouczek nie zawiera opisu wdrożenia żadnych zasad ponawiania.</span><span class="sxs-lookup"><span data-stu-id="cd48a-163">To keep things simple, this tutorial does not implement any retry policy.</span></span> <span data-ttu-id="cd48a-164">W kodzie produkcyjnym należy wdrożyć zasady ponawiania (np. wycofywanie wykładnicze) zgodnie z sugestią w artykule z witryny MSDN [Transient Fault Handling][lnk-transient-faults] (Obsługa przejściowych błędów).</span><span class="sxs-lookup"><span data-stu-id="cd48a-164">In production code, you should implement retry policies (such as an exponential backoff), as suggested in the MSDN article [Transient Fault Handling][lnk-transient-faults].</span></span>

## <a name="run-the-apps"></a><span data-ttu-id="cd48a-165">Uruchamianie aplikacji</span><span class="sxs-lookup"><span data-stu-id="cd48a-165">Run the apps</span></span>

<span data-ttu-id="cd48a-166">Teraz można przystąpić do uruchomienia aplikacji.</span><span class="sxs-lookup"><span data-stu-id="cd48a-166">You are now ready to run the apps.</span></span>

1. <span data-ttu-id="cd48a-167">W wierszu polecenia w **simDevice** folderu, uruchom następujące polecenie Rozpoczęcie nasłuchiwania metoda bezpośrednia ponowne uruchomienie komputera.</span><span class="sxs-lookup"><span data-stu-id="cd48a-167">At the command prompt in the **simDevice** folder, run the following command to begin listening for the reboot direct method.</span></span>

    ```cmd/sh
    node simDevice.js
    ```

1. <span data-ttu-id="cd48a-168">Uruchom aplikację konsoli języka C# **ScheduleJob** przez kliknięcie prawym przyciskiem myszy **ScheduleJob** projektu, wybierając **debugowania** i **Start nowe wystąpienie**.</span><span class="sxs-lookup"><span data-stu-id="cd48a-168">Run the C# console app **ScheduleJob** by right-clicking on the **ScheduleJob** project, then selecting **Debug** and **Start new instance**.</span></span>

1. <span data-ttu-id="cd48a-169">Możesz wyświetlić dane wyjściowe z urządzeń i aplikacji zaplecza.</span><span class="sxs-lookup"><span data-stu-id="cd48a-169">You see the output from both device and back-end apps.</span></span>

    ![Uruchamianie aplikacji do planowania zadań][img-schedulejobs]

## <a name="next-steps"></a><span data-ttu-id="cd48a-171">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="cd48a-171">Next steps</span></span>

<span data-ttu-id="cd48a-172">W tym samouczku użyto zadanie można zaplanować metoda bezpośrednia urządzenia i aktualizacji właściwości dwie urządzenia.</span><span class="sxs-lookup"><span data-stu-id="cd48a-172">In this tutorial, you used a job to schedule a direct method to a device and the update of the device twin's properties.</span></span>

<span data-ttu-id="cd48a-173">Aby kontynuować, wprowadzenie do korzystania z Centrum IoT i urządzenia zarządzania wzorców, takich jak zdalnego za pośrednictwem aktualizacji oprogramowania układowego lotniczego, przeczytaj [samouczek: sposób wykonywania aktualizacji oprogramowania układowego][lnk-fwupdate].</span><span class="sxs-lookup"><span data-stu-id="cd48a-173">To continue getting started with IoT Hub and device management patterns such as remote over the air firmware update, read [Tutorial: How to do a firmware update][lnk-fwupdate].</span></span>

<span data-ttu-id="cd48a-174">Aby kontynuować, wprowadzenie do korzystania z Centrum IoT, zobacz [wprowadzenie krawędzi IoT][lnk-iot-edge].</span><span class="sxs-lookup"><span data-stu-id="cd48a-174">To continue getting started with IoT Hub, see [Getting started with IoT Edge][lnk-iot-edge].</span></span>

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
