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
# <a name="schedule-and-broadcast-jobs-netnodejs"></a><span data-ttu-id="04bb9-104">Zadania harmonogramu i emisji (.NET/Node.js)</span><span class="sxs-lookup"><span data-stu-id="04bb9-104">Schedule and broadcast jobs (.NET/Node.js)</span></span>

[!INCLUDE [iot-hub-selector-schedule-jobs](../../includes/iot-hub-selector-schedule-jobs.md)]

<span data-ttu-id="04bb9-105">Użyj Centrum IoT Azure tooschedule i Śledź zadań aktualizowanych milionów urządzeń.</span><span class="sxs-lookup"><span data-stu-id="04bb9-105">Use Azure IoT Hub tooschedule and track jobs that update millions of devices.</span></span> <span data-ttu-id="04bb9-106">Należy użyć zadania, aby:</span><span class="sxs-lookup"><span data-stu-id="04bb9-106">Use jobs to:</span></span>

* <span data-ttu-id="04bb9-107">Aktualizowanie żądanych właściwości</span><span class="sxs-lookup"><span data-stu-id="04bb9-107">Update desired properties</span></span>
* <span data-ttu-id="04bb9-108">Tagi aktualizacji</span><span class="sxs-lookup"><span data-stu-id="04bb9-108">Update tags</span></span>
* <span data-ttu-id="04bb9-109">Wywołanie metody bezpośredniego</span><span class="sxs-lookup"><span data-stu-id="04bb9-109">Invoke direct methods</span></span>

<span data-ttu-id="04bb9-110">Zadanie opakowuje jedną z następujących czynności i śledzi hello miało zostać wykonane zbiór urządzeń jest definiowana za pomocą zapytania dwie urządzenia.</span><span class="sxs-lookup"><span data-stu-id="04bb9-110">A job wraps one of these actions and tracks hello execution against a set of devices that is defined by a device twin query.</span></span> <span data-ttu-id="04bb9-111">Na przykład aplikacji zaplecza można użyć zadania tooinvoke metoda bezpośrednia na 10 000 urządzeń, które wykonuje ponowny rozruch hello urządzeń.</span><span class="sxs-lookup"><span data-stu-id="04bb9-111">For example, a back-end app can use a job tooinvoke a direct method on 10,000 devices that reboots hello devices.</span></span> <span data-ttu-id="04bb9-112">Określ zestaw hello urządzeń za pomocą kwerendy dwie urządzenia i zaplanować hello toorun zadania w przyszłości.</span><span class="sxs-lookup"><span data-stu-id="04bb9-112">You specify hello set of devices with a device twin query and schedule hello job toorun at a future time.</span></span> <span data-ttu-id="04bb9-113">postęp śledzi zadania Hello jako każdego urządzenia hello odbierania i wykonaj metoda bezpośrednia hello ponowne uruchomienie komputera.</span><span class="sxs-lookup"><span data-stu-id="04bb9-113">hello job tracks progress as each of hello devices receive and execute hello reboot direct method.</span></span>

<span data-ttu-id="04bb9-114">toolearn więcej informacji na temat każdego z tych funkcji, zobacz:</span><span class="sxs-lookup"><span data-stu-id="04bb9-114">toolearn more about each of these capabilities, see:</span></span>

* <span data-ttu-id="04bb9-115">Dwie urządzeń i właściwości: [Rozpoczynanie pracy z urządzenia twins] [ lnk-get-started-twin] i [samouczek: jak urządzenie toouse dwie właściwości][lnk-twin-props]</span><span class="sxs-lookup"><span data-stu-id="04bb9-115">Device twin and properties: [Get started with device twins][lnk-get-started-twin] and [Tutorial: How toouse device twin properties][lnk-twin-props]</span></span>
* <span data-ttu-id="04bb9-116">Bezpośrednie metody: [przewodnik dewelopera Centrum IoT — metody bezpośredniego] [ lnk-dev-methods] i [samouczek: bezpośrednie metody][lnk-c2d-methods]</span><span class="sxs-lookup"><span data-stu-id="04bb9-116">Direct methods: [IoT Hub developer guide - direct methods][lnk-dev-methods] and [Tutorial: Use direct methods][lnk-c2d-methods]</span></span>

<span data-ttu-id="04bb9-117">Ten samouczek przedstawia sposób wykonania następujących czynności:</span><span class="sxs-lookup"><span data-stu-id="04bb9-117">This tutorial shows you how to:</span></span>

* <span data-ttu-id="04bb9-118">Tworzenie aplikacji urządzenia implementujący bezpośredniego metodę o nazwie **lockDoor** który może być wywoływany przez hello zaplecza aplikacji.</span><span class="sxs-lookup"><span data-stu-id="04bb9-118">Create a device app that implements a direct method called **lockDoor** that can be called by hello back-end app.</span></span> <span data-ttu-id="04bb9-119">Aplikacja urządzenia Hello również odbiera zmiany żądanej właściwości z hello zaplecza aplikacji.</span><span class="sxs-lookup"><span data-stu-id="04bb9-119">hello device app also receives desired property changes from hello back-end app.</span></span>
* <span data-ttu-id="04bb9-120">Tworzenie aplikacji zaplecza, która tworzy hello toocall zadania **lockDoor** metoda bezpośrednia na wielu urządzeniach.</span><span class="sxs-lookup"><span data-stu-id="04bb9-120">Create a back-end app that creates a job toocall hello **lockDoor** direct method on multiple devices.</span></span> <span data-ttu-id="04bb9-121">Inne zadanie wysyła żądanej właściwości aktualizuje toomultiple urządzeń.</span><span class="sxs-lookup"><span data-stu-id="04bb9-121">Another job sends desired property updates toomultiple devices.</span></span>

<span data-ttu-id="04bb9-122">Na końcu hello tego samouczka masz aplikację Node.js konsoli urządzenia i zaplecza aplikacji konsoli .NET (C#):</span><span class="sxs-lookup"><span data-stu-id="04bb9-122">At hello end of this tutorial, you have a Node.js console device app and a .NET (C#) console back-end app:</span></span>

<span data-ttu-id="04bb9-123">**simDevice.js** który łączy Centrum IoT tooyour, implementuje hello **lockDoor** bezpośrednie — metoda i uchwytów potrzebne zmiany właściwości.</span><span class="sxs-lookup"><span data-stu-id="04bb9-123">**simDevice.js** that connects tooyour IoT hub, implements hello **lockDoor** direct method, and handles desired property changes.</span></span>

<span data-ttu-id="04bb9-124">**ScheduleJob** używającą hello toocall zadania **lockDoor** właściwości na wielu urządzeniach potrzeby bezpośredniego metoda i aktualizacji dwie hello w urządzeniu.</span><span class="sxs-lookup"><span data-stu-id="04bb9-124">**ScheduleJob** that uses jobs toocall hello **lockDoor** direct method and update hello device twin desired properties on multiple devices.</span></span>

<span data-ttu-id="04bb9-125">toocomplete tego samouczka należy hello następujące:</span><span class="sxs-lookup"><span data-stu-id="04bb9-125">toocomplete this tutorial, you need hello following:</span></span>

* <span data-ttu-id="04bb9-126">Program Visual Studio 2015 lub Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="04bb9-126">Visual Studio 2015 or Visual Studio 2017.</span></span>
* <span data-ttu-id="04bb9-127">Środowisko Node.js w wersji 0.12.x lub nowszej.</span><span class="sxs-lookup"><span data-stu-id="04bb9-127">Node.js version 0.12.x or later.</span></span> <span data-ttu-id="04bb9-128">Artykuł Hello [przygotowywanie środowiska projektowego] [ lnk-dev-setup] w tym artykule opisano sposób tooinstall Node.js, w tym samouczku w systemie Windows lub Linux.</span><span class="sxs-lookup"><span data-stu-id="04bb9-128">hello article [Prepare your development environment][lnk-dev-setup] describes how tooinstall Node.js for this tutorial on either Windows or Linux.</span></span>
* <span data-ttu-id="04bb9-129">Aktywne konto platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="04bb9-129">An active Azure account.</span></span> <span data-ttu-id="04bb9-130">Jeśli go nie masz, możesz utworzyć [bezpłatne konto][lnk-free-trial] w zaledwie kilka minut.</span><span class="sxs-lookup"><span data-stu-id="04bb9-130">If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.</span></span>

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity](../../includes/iot-hub-get-started-create-device-identity.md)]

## <a name="schedule-jobs-for-calling-a-direct-method-and-sending-device-twin-updates"></a><span data-ttu-id="04bb9-131">Planowanie zadań dla wywołania metody bezpośredniego i wysyłania aktualizacji dwie urządzenia</span><span class="sxs-lookup"><span data-stu-id="04bb9-131">Schedule jobs for calling a direct method and sending device twin updates</span></span>

<span data-ttu-id="04bb9-132">W tej sekcji Tworzenie aplikacji konsoli .NET (przy użyciu języka C#) używającej hello toocall zadania **lockDoor** metoda bezpośrednia i wysłać żądanej właściwości aktualizuje toomultiple urządzeń.</span><span class="sxs-lookup"><span data-stu-id="04bb9-132">In this section, you create a .NET console app (using C#) that uses jobs toocall hello **lockDoor** direct method and send desired property updates toomultiple devices.</span></span>

1. <span data-ttu-id="04bb9-133">W programie Visual Studio, należy dodać bieżącego rozwiązania toohello projektu Visual C# pulpitu systemu Windows klasycznego przy użyciu hello **aplikacji konsoli** szablonu projektu.</span><span class="sxs-lookup"><span data-stu-id="04bb9-133">In Visual Studio, add a Visual C# Windows Classic Desktop project toohello current solution by using hello **Console Application** project template.</span></span> <span data-ttu-id="04bb9-134">Nazwa projektu hello **ScheduleJob**.</span><span class="sxs-lookup"><span data-stu-id="04bb9-134">Name hello project **ScheduleJob**.</span></span>

    ![Nowy projekt Visual C# Windows Classic Desktop][img-createapp]

1. <span data-ttu-id="04bb9-136">W Eksploratorze rozwiązań kliknij prawym przyciskiem myszy hello **ScheduleJob** projektu, a następnie kliknij przycisk **Zarządzaj pakietami NuGet...** .</span><span class="sxs-lookup"><span data-stu-id="04bb9-136">In Solution Explorer, right-click hello **ScheduleJob** project, and then click **Manage NuGet Packages...**.</span></span>
1. <span data-ttu-id="04bb9-137">W hello **Menedżera pakietów NuGet** wybierz **Przeglądaj**, wyszukaj **microsoft.azure.devices**, wybierz pozycję **zainstalować** tooinstall Witaj **Microsoft.Azure.Devices** pakietu i zaakceptuj warunki użytkowania hello.</span><span class="sxs-lookup"><span data-stu-id="04bb9-137">In hello **NuGet Package Manager** window, select **Browse**, search for **microsoft.azure.devices**, select **Install** tooinstall hello **Microsoft.Azure.Devices** package, and accept hello terms of use.</span></span> <span data-ttu-id="04bb9-138">Ten krok pliki do pobrania, instaluje i dodaje toohello odwołanie [zestawu SDK usług Azure IoT] [ lnk-nuget-service-sdk] NuGet pakiet i jego zależności.</span><span class="sxs-lookup"><span data-stu-id="04bb9-138">This step downloads, installs, and adds a reference toohello [Azure IoT service SDK][lnk-nuget-service-sdk] NuGet package and its dependencies.</span></span>

    ![Okno Menedżera pakietów NuGet][img-servicenuget]
1. <span data-ttu-id="04bb9-140">Dodaj następujące hello `using` instrukcji u góry hello hello **Program.cs** pliku:</span><span class="sxs-lookup"><span data-stu-id="04bb9-140">Add hello following `using` statements at hello top of hello **Program.cs** file:</span></span>
    
    ```csharp
    using Microsoft.Azure.Devices;
    using Microsoft.Azure.Devices.Shared;
    ```

1. <span data-ttu-id="04bb9-141">Dodaj następujące hello `using` instrukcję, jeśli jeszcze nie istnieje w instrukcjach domyślne hello.</span><span class="sxs-lookup"><span data-stu-id="04bb9-141">Add hello following `using` statement if not already present in hello default statements.</span></span>

    ```csharp
    using System.Threading.Tasks;
    ```

1. <span data-ttu-id="04bb9-142">Dodaj następujące pola toohello hello **Program** klasy.</span><span class="sxs-lookup"><span data-stu-id="04bb9-142">Add hello following fields toohello **Program** class.</span></span> <span data-ttu-id="04bb9-143">Zastąp symbol zastępczy hello hello hello koncentratora, który został utworzony w poprzedniej sekcji hello parametry połączenia Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="04bb9-143">Replace hello placeholder with hello IoT Hub connection string for hello hub that you created in hello previous section.</span></span>

    ```csharp
    static string connString = "{iot hub connection string}";
    static ServiceClient client;
    static JobClient jobClient;
    ```

1. <span data-ttu-id="04bb9-144">Dodaj następujące metody toohello hello **Program** klasy:</span><span class="sxs-lookup"><span data-stu-id="04bb9-144">Add hello following method toohello **Program** class:</span></span>

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

1. <span data-ttu-id="04bb9-145">Dodaj następujące metody toohello hello **Program** klasy:</span><span class="sxs-lookup"><span data-stu-id="04bb9-145">Add hello following method toohello **Program** class:</span></span>

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

1. <span data-ttu-id="04bb9-146">Dodaj następujące metody toohello hello **Program** klasy:</span><span class="sxs-lookup"><span data-stu-id="04bb9-146">Add hello following method toohello **Program** class:</span></span>

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

1. <span data-ttu-id="04bb9-147">Na koniec należy dodać następujące wiersze toohello hello **Main** metody:</span><span class="sxs-lookup"><span data-stu-id="04bb9-147">Finally, add hello following lines toohello **Main** method:</span></span>

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

1. <span data-ttu-id="04bb9-148">W Eksploratorze rozwiązań hello, otwórz hello **projektów startowych ustawić...**  i upewnij się, że hello **akcji** dla **ScheduleJob** projekt jest **Start**.</span><span class="sxs-lookup"><span data-stu-id="04bb9-148">In hello Solution Explorer, open hello **Set StartUp projects...** and make sure hello **Action** for **ScheduleJob** project is **Start**.</span></span> <span data-ttu-id="04bb9-149">Utworzenie rozwiązania hello.</span><span class="sxs-lookup"><span data-stu-id="04bb9-149">Build hello solution.</span></span>

## <a name="create-a-simulated-device-app"></a><span data-ttu-id="04bb9-150">Tworzenie aplikacji symulowanego urządzenia</span><span class="sxs-lookup"><span data-stu-id="04bb9-150">Create a simulated device app</span></span>

<span data-ttu-id="04bb9-151">W tej sekcji utworzysz aplikację konsoli Node.js, która odpowiada tooa metoda bezpośrednia wywoływane przez hello chmury, co jest wyzwalane symulowane urządzenie ponowne uruchomienie komputera i zgłosił hello używa właściwości tooenable urządzeń dwie zapytania tooidentify urządzenia, a podczas ich ostatniego ponownego uruchomienia.</span><span class="sxs-lookup"><span data-stu-id="04bb9-151">In this section, you create a Node.js console app that responds tooa direct method called by hello cloud, which triggers a simulated device reboot and uses hello reported properties tooenable device twin queries tooidentify devices and when they last rebooted.</span></span>

1. <span data-ttu-id="04bb9-152">Utwórz nowy, pusty folder o nazwie **simDevice**.</span><span class="sxs-lookup"><span data-stu-id="04bb9-152">Create a new empty folder called **simDevice**.</span></span>  <span data-ttu-id="04bb9-153">W hello **simDevice** folderu, Utwórz plik package.json za pomocą hello następujące polecenie z wiersza polecenia.</span><span class="sxs-lookup"><span data-stu-id="04bb9-153">In hello **simDevice** folder, create a package.json file using hello following command at your command prompt.</span></span>  <span data-ttu-id="04bb9-154">Zaakceptuj wszystkie domyślne hello:</span><span class="sxs-lookup"><span data-stu-id="04bb9-154">Accept all hello defaults:</span></span>

    ```cmd/sh
    npm init
    ```

1. <span data-ttu-id="04bb9-155">Z wiersza polecenia w hello **simDevice** folderu, uruchom następujące polecenie tooinstall hello hello **azure iot urządzenia** i **azure-iot urządzenie mqtt** pakiety:</span><span class="sxs-lookup"><span data-stu-id="04bb9-155">At your command prompt in hello **simDevice** folder, run hello following command tooinstall hello **azure-iot-device** and **azure-iot-device-mqtt** packages:</span></span>

    ```cmd/sh
    npm install azure-iot-device azure-iot-device-mqtt --save
    ```

1. <span data-ttu-id="04bb9-156">Za pomocą edytora tekstu, Utwórz nową **simDevice.js** pliku w hello **simDevice** folderu.</span><span class="sxs-lookup"><span data-stu-id="04bb9-156">Using a text editor, create a new **simDevice.js** file in hello **simDevice** folder.</span></span>

1. <span data-ttu-id="04bb9-157">Dodaj następujące hello "Wymagaj" instrukcje na początku hello hello **simDevice.js** pliku:</span><span class="sxs-lookup"><span data-stu-id="04bb9-157">Add hello following 'require' statements at hello start of hello **simDevice.js** file:</span></span>

    ```nodejs
    'use strict';
   
    var Client = require('azure-iot-device').Client;
    var Protocol = require('azure-iot-device-mqtt').Mqtt;
    ```

1. <span data-ttu-id="04bb9-158">Dodaj **connectionString** zmiennej i korzystać z niego toocreate **klienta** wystąpienia.</span><span class="sxs-lookup"><span data-stu-id="04bb9-158">Add a **connectionString** variable and use it toocreate a **Client** instance.</span></span> <span data-ttu-id="04bb9-159">Należy symbole zastępcze hello tooreplace się z Instalatorem tooyour odpowiednie wartości.</span><span class="sxs-lookup"><span data-stu-id="04bb9-159">Make sure tooreplace hello placeholders with values appropriate tooyour setup.</span></span>

    ```nodejs
    var connectionString = 'HostName={youriothostname};DeviceId={yourdeviceid};SharedAccessKey={yourdevicekey}';
    var client = Client.fromConnectionString(connectionString, Protocol);
    ```

1. <span data-ttu-id="04bb9-160">Dodaj powitania po hello toohandle funkcja **lockDoor** metody.</span><span class="sxs-lookup"><span data-stu-id="04bb9-160">Add hello following function toohandle hello **lockDoor** method.</span></span>

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

1. <span data-ttu-id="04bb9-161">Dodaj następującego kodu tooregister hello obsługę hello hello **lockDoor** metody.</span><span class="sxs-lookup"><span data-stu-id="04bb9-161">Add hello following code tooregister hello handler for hello **lockDoor** method.</span></span>

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

1. <span data-ttu-id="04bb9-162">Zapisz i zamknij hello **simDevice.js** pliku.</span><span class="sxs-lookup"><span data-stu-id="04bb9-162">Save and close hello **simDevice.js** file.</span></span>

> [!NOTE]
> <span data-ttu-id="04bb9-163">rzeczy tookeep proste, w tym samouczku nie implementuje wszystkie zasady ponawiania.</span><span class="sxs-lookup"><span data-stu-id="04bb9-163">tookeep things simple, this tutorial does not implement any retry policy.</span></span> <span data-ttu-id="04bb9-164">W kodzie produkcyjnym, należy zaimplementować zasady ponawiania (na przykład wykładniczego wycofywania), zgodnie z sugestią podaną w artykuł w witrynie MSDN hello [obsługi błędów przejściowych][lnk-transient-faults].</span><span class="sxs-lookup"><span data-stu-id="04bb9-164">In production code, you should implement retry policies (such as an exponential backoff), as suggested in hello MSDN article [Transient Fault Handling][lnk-transient-faults].</span></span>

## <a name="run-hello-apps"></a><span data-ttu-id="04bb9-165">Uruchamianie aplikacji hello</span><span class="sxs-lookup"><span data-stu-id="04bb9-165">Run hello apps</span></span>

<span data-ttu-id="04bb9-166">Wszystko jest teraz gotowy toorun hello aplikacji.</span><span class="sxs-lookup"><span data-stu-id="04bb9-166">You are now ready toorun hello apps.</span></span>

1. <span data-ttu-id="04bb9-167">W wierszu polecenia hello w hello **simDevice** folderu Uruchom hello następujące polecenia toobegin nasłuchiwanie metoda bezpośrednia hello ponowny rozruch.</span><span class="sxs-lookup"><span data-stu-id="04bb9-167">At hello command prompt in hello **simDevice** folder, run hello following command toobegin listening for hello reboot direct method.</span></span>

    ```cmd/sh
    node simDevice.js
    ```

1. <span data-ttu-id="04bb9-168">Aplikacja konsoli uruchamiania hello C# **ScheduleJob** klikając prawym przyciskiem myszy na powitania **ScheduleJob** projektu, wybierając **debugowania** i **Start nowe wystąpienie**.</span><span class="sxs-lookup"><span data-stu-id="04bb9-168">Run hello C# console app **ScheduleJob** by right-clicking on hello **ScheduleJob** project, then selecting **Debug** and **Start new instance**.</span></span>

1. <span data-ttu-id="04bb9-169">Zostanie wyświetlony hello wyjście z urządzeń i aplikacji zaplecza.</span><span class="sxs-lookup"><span data-stu-id="04bb9-169">You see hello output from both device and back-end apps.</span></span>

    ![Uruchamianie aplikacji hello tooschedule zadań][img-schedulejobs]

## <a name="next-steps"></a><span data-ttu-id="04bb9-171">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="04bb9-171">Next steps</span></span>

<span data-ttu-id="04bb9-172">W tym samouczku użyto zadania tooschedule urządzenia tooa metoda bezpośrednia i aktualizacji hello hello urządzenia dwie właściwości.</span><span class="sxs-lookup"><span data-stu-id="04bb9-172">In this tutorial, you used a job tooschedule a direct method tooa device and hello update of hello device twin's properties.</span></span>

<span data-ttu-id="04bb9-173">wprowadzenie do korzystania z Centrum IoT i urządzeniami wzorców zarządzania, takich jak zdalnego za pośrednictwem aktualizacji oprogramowania układowego lotniczego hello odczytu toocontinue [samouczek: jak toodo oprogramowanie układowe zaktualizować][lnk-fwupdate].</span><span class="sxs-lookup"><span data-stu-id="04bb9-173">toocontinue getting started with IoT Hub and device management patterns such as remote over hello air firmware update, read [Tutorial: How toodo a firmware update][lnk-fwupdate].</span></span>

<span data-ttu-id="04bb9-174">Zobacz toocontinue wprowadzenie do korzystania z Centrum IoT [wprowadzenie krawędzi IoT][lnk-iot-edge].</span><span class="sxs-lookup"><span data-stu-id="04bb9-174">toocontinue getting started with IoT Hub, see [Getting started with IoT Edge][lnk-iot-edge].</span></span>

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
