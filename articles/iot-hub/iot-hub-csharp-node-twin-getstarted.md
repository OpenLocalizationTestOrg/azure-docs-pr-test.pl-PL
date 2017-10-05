---
title: "Rozpoczynanie pracy z Centrum IoT Azure urządzenia twins (.NET/węzła) | Dokumentacja firmy Microsoft"
description: "Jak używać twins urządzenia Azure IoT Hub Dodawanie tagów, a następnie użyć kwerendy Centrum IoT. Przy użyciu urządzenia Azure IoT SDK dla środowiska Node.js usługi Azure IoT SDK dla platformy .NET do implementacji usługi aplikacji, która dodaje znaczniki i uruchamia kwerendy Centrum IoT i aplikacji symulowane urządzenie."
services: iot-hub
documentationcenter: node
author: fsautomata
manager: timlt
editor: 
ms.assetid: f7e23b6e-bfde-4fba-a6ec-dbb0f0e005f4
ms.service: iot-hub
ms.devlang: node
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/29/2017
ms.author: elioda
ms.openlocfilehash: 07797b9159c9b926e9eb47d8864c63048951931a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-device-twins-netnode"></a><span data-ttu-id="41c28-104">Rozpoczynanie pracy z urządzenia twins (.NET/węzeł)</span><span class="sxs-lookup"><span data-stu-id="41c28-104">Get started with device twins (.NET/Node)</span></span>
[!INCLUDE [iot-hub-selector-twin-get-started](../../includes/iot-hub-selector-twin-get-started.md)]

<span data-ttu-id="41c28-105">Na końcu tego samouczka konieczne będzie .NET i Node.js aplikację konsoli:</span><span class="sxs-lookup"><span data-stu-id="41c28-105">At the end of this tutorial, you will have a .NET and a Node.js console app:</span></span>

* <span data-ttu-id="41c28-106">**AddTagsAndQuery.sln**, aplikacji zaplecza .NET, która dodaje znaczniki i zapytanie twins urządzenia.</span><span class="sxs-lookup"><span data-stu-id="41c28-106">**AddTagsAndQuery.sln**, a .NET back-end app, which adds tags and queries device twins.</span></span>
* <span data-ttu-id="41c28-107">**TwinSimulatedDevice.js**, aplikacji Node.js, która symuluje urządzenie, które łączy do Centrum IoT z tożsamości urządzenia utworzony wcześniej, a następnie raportuje stanu łączności.</span><span class="sxs-lookup"><span data-stu-id="41c28-107">**TwinSimulatedDevice.js**, a Node.js app which simulates a device that connects to your IoT hub with the device identity created earlier, and reports its connectivity condition.</span></span>

> [!NOTE]
> <span data-ttu-id="41c28-108">Artykuł [Azure IoT SDK] [ lnk-hub-sdks] informacje na temat zestawów SDK IoT Azure można tworzyć aplikacje zarówno urządzenia, jak i zaplecza.</span><span class="sxs-lookup"><span data-stu-id="41c28-108">The article [Azure IoT SDKs][lnk-hub-sdks] provides information about the Azure IoT SDKs that you can use to build both device and back-end apps.</span></span>
> 
> 

<span data-ttu-id="41c28-109">Do ukończenia tego samouczka należy spełnić następujące warunki:</span><span class="sxs-lookup"><span data-stu-id="41c28-109">To complete this tutorial you need the following:</span></span>

* <span data-ttu-id="41c28-110">Program Visual Studio 2015 lub Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="41c28-110">Visual Studio 2015 or Visual Studio 2017.</span></span>
* <span data-ttu-id="41c28-111">Środowisko Node.js w wersji 0.10.x lub nowszej.</span><span class="sxs-lookup"><span data-stu-id="41c28-111">Node.js version 0.10.x or later.</span></span>
* <span data-ttu-id="41c28-112">Aktywne konto platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="41c28-112">An active Azure account.</span></span> <span data-ttu-id="41c28-113">(Jeśli go nie masz, możesz utworzyć [bezpłatne konto próbne][lnk-free-trial] w zaledwie kilka minut).</span><span class="sxs-lookup"><span data-stu-id="41c28-113">(If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.)</span></span>

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity](../../includes/iot-hub-get-started-create-device-identity.md)]

## <a name="create-the-service-app"></a><span data-ttu-id="41c28-114">Tworzenie aplikacji usługi</span><span class="sxs-lookup"><span data-stu-id="41c28-114">Create the service app</span></span>
<span data-ttu-id="41c28-115">W tej sekcji Tworzenie aplikacji konsoli .NET (przy użyciu języka C#) umożliwiający dodawanie metadanych lokalizacji do dwie urządzeń skojarzonych z **myDeviceId**.</span><span class="sxs-lookup"><span data-stu-id="41c28-115">In this section, you create a .NET console app (using C#) that adds location metadata to the device twin associated with **myDeviceId**.</span></span> <span data-ttu-id="41c28-116">Tworzy następnie kwerendę twins urządzenia przechowywane w Centrum IoT Wybieranie urządzeń znajdujących się w Stanach Zjednoczonych i te, które połączenie transmisji.</span><span class="sxs-lookup"><span data-stu-id="41c28-116">It then queries the device twins stored in the IoT hub selecting the devices located in the US, and then the ones that reported a cellular connection.</span></span>

1. <span data-ttu-id="41c28-117">W programie Visual Studio dodaj projekt Visual C# Windows Classic Desktop do bieżącego rozwiązania przy użyciu szablonu projektu **Aplikacja konsolowa**.</span><span class="sxs-lookup"><span data-stu-id="41c28-117">In Visual Studio, add a Visual C# Windows Classic Desktop project to the current solution by using the **Console Application** project template.</span></span> <span data-ttu-id="41c28-118">Nazwij projekt **AddTagsAndQuery**.</span><span class="sxs-lookup"><span data-stu-id="41c28-118">Name the project **AddTagsAndQuery**.</span></span>
   
    ![Nowy projekt Visual C# Windows Classic Desktop][img-createapp]
1. <span data-ttu-id="41c28-120">W Eksploratorze rozwiązań kliknij prawym przyciskiem myszy **AddTagsAndQuery** projektu, a następnie kliknij przycisk **Zarządzaj pakietami NuGet...** .</span><span class="sxs-lookup"><span data-stu-id="41c28-120">In Solution Explorer, right-click the **AddTagsAndQuery** project, and then click **Manage NuGet Packages...**.</span></span>
1. <span data-ttu-id="41c28-121">W **Menedżera pakietów NuGet** wybierz **Przeglądaj** i wyszukaj **microsoft.azure.devices**.</span><span class="sxs-lookup"><span data-stu-id="41c28-121">In the **NuGet Package Manager** window, select **Browse** and search for **microsoft.azure.devices**.</span></span> <span data-ttu-id="41c28-122">Wybierz **zainstalować** do zainstalowania **Microsoft.Azure.Devices** pakietu, a następnie zaakceptuj warunki użytkowania.</span><span class="sxs-lookup"><span data-stu-id="41c28-122">Select **Install** to install the **Microsoft.Azure.Devices** package, and accept the terms of use.</span></span> <span data-ttu-id="41c28-123">Ta procedura spowoduje pobranie, zainstalowanie i dodanie odwołania do pakietu NuGet [zestawu SDK usługi Azure IoT][lnk-nuget-service-sdk] oraz jego zależności.</span><span class="sxs-lookup"><span data-stu-id="41c28-123">This procedure downloads, installs, and adds a reference to the [Azure IoT service SDK][lnk-nuget-service-sdk] NuGet package and its dependencies.</span></span>
   
    ![Okno Menedżera pakietów NuGet][img-servicenuget]
1. <span data-ttu-id="41c28-125">Dodaj następujące instrukcje `using` w górnej części pliku **Program.cs**:</span><span class="sxs-lookup"><span data-stu-id="41c28-125">Add the following `using` statements at the top of the **Program.cs** file:</span></span>
   
        using Microsoft.Azure.Devices;
1. <span data-ttu-id="41c28-126">Dodaj następujące pola do klasy **Program**:</span><span class="sxs-lookup"><span data-stu-id="41c28-126">Add the following fields to the **Program** class.</span></span> <span data-ttu-id="41c28-127">Zastąp wartość symbolu zastępczego parametrami połączenia usługi IoT Hub dla centrum IoT utworzonego w poprzedniej sekcji.</span><span class="sxs-lookup"><span data-stu-id="41c28-127">Replace the placeholder value with the IoT Hub connection string for the hub that you created in the previous section.</span></span>
   
        static RegistryManager registryManager;
        static string connectionString = "{iot hub connection string}";
1. <span data-ttu-id="41c28-128">Dodaj następującą metodę do klasy **Program**:</span><span class="sxs-lookup"><span data-stu-id="41c28-128">Add the following method to the **Program** class:</span></span>
   
        public static async Task AddTagsAndQuery()
        {
            var twin = await registryManager.GetTwinAsync("myDeviceId");
            var patch =
                @"{
                    tags: {
                        location: {
                            region: 'US',
                            plant: 'Redmond43'
                        }
                    }
                }";
            await registryManager.UpdateTwinAsync(twin.DeviceId, patch, twin.ETag);
   
            var query = registryManager.CreateQuery("SELECT * FROM devices WHERE tags.location.plant = 'Redmond43'", 100);
            var twinsInRedmond43 = await query.GetNextAsTwinAsync();
            Console.WriteLine("Devices in Redmond43: {0}", string.Join(", ", twinsInRedmond43.Select(t => t.DeviceId)));
   
            query = registryManager.CreateQuery("SELECT * FROM devices WHERE tags.location.plant = 'Redmond43' AND properties.reported.connectivity.type = 'cellular'", 100);
            var twinsInRedmond43UsingCellular = await query.GetNextAsTwinAsync();
            Console.WriteLine("Devices in Redmond43 using cellular network: {0}", string.Join(", ", twinsInRedmond43UsingCellular.Select(t => t.DeviceId)));
        }
   
    <span data-ttu-id="41c28-129">**RegistryManager** klasy udostępnia wszystkie metody, które są wymagane do interakcji z twins urządzenia z usługi.</span><span class="sxs-lookup"><span data-stu-id="41c28-129">The **RegistryManager** class exposes all the methods required to interact with device twins from the service.</span></span> <span data-ttu-id="41c28-130">Poprzedni kod najpierw inicjuje **registryManager** obiekt, a następnie pobiera dwie urządzenia dla **myDeviceId**i na koniec aktualizuje jego tagi informacji żądaną lokalizację.</span><span class="sxs-lookup"><span data-stu-id="41c28-130">The previous code first initializes the **registryManager** object, then retrieves the device twin for **myDeviceId**, and finally updates its tags with the desired location information.</span></span>
   
    <span data-ttu-id="41c28-131">Po zaktualizowaniu, wykonuje on dwa zapytania: pierwszy wybiera tylko twins urządzenia urządzeń znajdujących się w **Redmond43** zakładu, a drugi udoskonalanie zapytanie, aby wybrać tylko te urządzenia, które także są połączone za pośrednictwem sieci komórkowej.</span><span class="sxs-lookup"><span data-stu-id="41c28-131">After updating, it executes two queries: the first selects only the device twins of devices located in the **Redmond43** plant, and the second refines the query to select only the devices that are also connected through cellular network.</span></span>
   
    <span data-ttu-id="41c28-132">Należy pamiętać, że poprzedni kod, w którym tworzy **zapytania** obiektów, określa maksymalną liczbę zwracanych dokumentów.</span><span class="sxs-lookup"><span data-stu-id="41c28-132">Note that the previous code, when it creates the **query** object, specifies a maximum number of returned documents.</span></span> <span data-ttu-id="41c28-133">**Zapytania** zawiera obiekt **HasMoreResults** właściwości typu boolean, którego można użyć do wywołania **GetNextAsTwinAsync** metody kilka razy, aby pobrać wszystkie wyniki.</span><span class="sxs-lookup"><span data-stu-id="41c28-133">The **query** object contains a **HasMoreResults** boolean property that you can use to invoke the **GetNextAsTwinAsync** methods multiple times to retrieve all results.</span></span> <span data-ttu-id="41c28-134">Wywołana metoda **GetNextAsJson** jest dostępna dla wyników, które są nie twins urządzenia, na przykład wyniki zapytań agregacji.</span><span class="sxs-lookup"><span data-stu-id="41c28-134">A method called **GetNextAsJson** is available for results that are not device twins, for example, results of aggregation queries.</span></span>
1. <span data-ttu-id="41c28-135">Na koniec dodaj następujące wiersze do metody **Główne**:</span><span class="sxs-lookup"><span data-stu-id="41c28-135">Finally, add the following lines to the **Main** method:</span></span>
   
        registryManager = RegistryManager.CreateFromConnectionString(connectionString);
        AddTagsAndQuery().Wait();
        Console.WriteLine("Press Enter to exit.");
        Console.ReadLine();

1. <span data-ttu-id="41c28-136">W Eksploratorze rozwiązań Otwórz **projektów startowych ustawić...**  i upewnij się, że **akcji** dla **AddTagsAndQuery** projekt jest **Start**.</span><span class="sxs-lookup"><span data-stu-id="41c28-136">In the Solution Explorer, open the **Set StartUp projects...** and make sure the **Action** for **AddTagsAndQuery** project is **Start**.</span></span> <span data-ttu-id="41c28-137">Skompiluj rozwiązanie.</span><span class="sxs-lookup"><span data-stu-id="41c28-137">Build the solution.</span></span>
1. <span data-ttu-id="41c28-138">Uruchomić tę aplikację, klikając prawym przyciskiem myszy **AddTagsAndQuery** projekt i wybierając **debugowania**, a następnie **Start nowe wystąpienie**.</span><span class="sxs-lookup"><span data-stu-id="41c28-138">Run this application by right-clicking on the **AddTagsAndQuery** project and selecting **Debug**, followed by **Start new instance**.</span></span> <span data-ttu-id="41c28-139">Jedno urządzenie w wynikach zadać kwerendy powinna być widoczna dla wszystkich urządzeń znajdujących się w **Redmond43** i Brak dla zapytania, który ogranicza wyniki do urządzenia, które korzystają z sieci komórkowej.</span><span class="sxs-lookup"><span data-stu-id="41c28-139">You should see one device in the results for the query asking for all devices located in **Redmond43** and none for the query that restricts the results to devices that use a cellular network.</span></span>
   
    ![Wyniki zapytania w oknie][img-addtagapp]

<span data-ttu-id="41c28-141">W następnej sekcji utworzysz aplikację urządzenia, która raportuje informacje dotyczące łączności i zmienia się wynik kwerendy w poprzedniej sekcji.</span><span class="sxs-lookup"><span data-stu-id="41c28-141">In the next section, you create a device app that reports the connectivity information and changes the result of the query in the previous section.</span></span>

## <a name="create-the-device-app"></a><span data-ttu-id="41c28-142">Tworzenie aplikacji urządzeń</span><span class="sxs-lookup"><span data-stu-id="41c28-142">Create the device app</span></span>
<span data-ttu-id="41c28-143">W tej sekcji zostanie utworzona aplikacja konsoli Node.js łączący się do Centrum jako **myDeviceId**, a następnie aktualizuje jego zgłoszone właściwości zawierają informacje, że jest połączony za pomocą sieci komórkowej.</span><span class="sxs-lookup"><span data-stu-id="41c28-143">In this section, you create a Node.js console app that connects to your hub as **myDeviceId**, and then updates its reported properties to contain the information that it is connected using a cellular network.</span></span>

1. <span data-ttu-id="41c28-144">Utwórz nowy, pusty folder o nazwie **reportconnectivity**.</span><span class="sxs-lookup"><span data-stu-id="41c28-144">Create a new empty folder called **reportconnectivity**.</span></span> <span data-ttu-id="41c28-145">W **reportconnectivity** folderu, Utwórz nowy plik package.json za pomocą następującego polecenia z wiersza polecenia.</span><span class="sxs-lookup"><span data-stu-id="41c28-145">In the **reportconnectivity** folder, create a new package.json file using the following command at your command prompt.</span></span> <span data-ttu-id="41c28-146">Zaakceptuj wszystkie ustawienia domyślne.</span><span class="sxs-lookup"><span data-stu-id="41c28-146">Accept all the defaults.</span></span>
   
    ```
    npm init
    ```
1. <span data-ttu-id="41c28-147">Z wiersza polecenia w **reportconnectivity** folderu, uruchom następujące polecenie, aby zainstalować **azure iot urządzenia**, i **azure-iot urządzenie mqtt** pakietu:</span><span class="sxs-lookup"><span data-stu-id="41c28-147">At your command prompt in the **reportconnectivity** folder, run the following command to install the **azure-iot-device**, and **azure-iot-device-mqtt** package:</span></span>
   
    ```
    npm install azure-iot-device azure-iot-device-mqtt --save
    ```
1. <span data-ttu-id="41c28-148">Za pomocą edytora tekstu, Utwórz nową **ReportConnectivity.js** w pliku **reportconnectivity** folderu.</span><span class="sxs-lookup"><span data-stu-id="41c28-148">Using a text editor, create a new **ReportConnectivity.js** file in the **reportconnectivity** folder.</span></span>
1. <span data-ttu-id="41c28-149">Dodaj następujący kod do **ReportConnectivity.js** plików i Zastąp symbol zastępczy parametrów połączenia urządzenia z skopiowane podczas tworzenia **myDeviceId** tożsamości urządzenia:</span><span class="sxs-lookup"><span data-stu-id="41c28-149">Add the following code to the **ReportConnectivity.js** file, and substitute the placeholder for device connection string with the one you copied when you created the **myDeviceId** device identity:</span></span>
   
        'use strict';
        var Client = require('azure-iot-device').Client;
        var Protocol = require('azure-iot-device-mqtt').Mqtt;
   
        var connectionString = '{device connection string}';
        var client = Client.fromConnectionString(connectionString, Protocol);
   
        client.open(function(err) {
        if (err) {
            console.error('could not open IotHub client');
        }  else {
            console.log('client opened');
   
            client.getTwin(function(err, twin) {
            if (err) {
                console.error('could not get twin');
            } else {
                var patch = {
                    connectivity: {
                        type: 'cellular'
                    }
                };
   
                twin.properties.reported.update(patch, function(err) {
                    if (err) {
                        console.error('could not update twin');
                    } else {
                        console.log('twin state reported');
                        process.exit();
                    }
                });
            }
            });
        }
        });
   
    <span data-ttu-id="41c28-150">**Klienta** obiekt udostępnia wszystkie metody, które są wymagane do interakcji z twins urządzenia z urządzenia.</span><span class="sxs-lookup"><span data-stu-id="41c28-150">The **Client** object exposes all the methods you require to interact with device twins from the device.</span></span> <span data-ttu-id="41c28-151">Poprzedni kod po jego inicjuje **klienta** obiektów, pobiera dwie urządzenia dla **myDeviceId** i aktualizuje jego właściwość zgłoszone informacje o łączności.</span><span class="sxs-lookup"><span data-stu-id="41c28-151">The previous code, after it initializes the **Client** object, retrieves the device twin for **myDeviceId** and updates its reported property with the connectivity information.</span></span>
1. <span data-ttu-id="41c28-152">Uruchamianie aplikacji urządzeń</span><span class="sxs-lookup"><span data-stu-id="41c28-152">Run the device app</span></span>
   
        node ReportConnectivity.js
   
    <span data-ttu-id="41c28-153">Powinien zostać wyświetlony komunikat `twin state reported`.</span><span class="sxs-lookup"><span data-stu-id="41c28-153">You should see the message `twin state reported`.</span></span>
1. <span data-ttu-id="41c28-154">Teraz, gdy urządzenie zgłosiło jego informacje dotyczące łączności, powinna pojawić się w obu zapytania.</span><span class="sxs-lookup"><span data-stu-id="41c28-154">Now that the device reported its connectivity information, it should appear in both queries.</span></span> <span data-ttu-id="41c28-155">Uruchamianie programu .NET **AddTagsAndQuery** aplikacji, aby ponownie uruchomić zapytania.</span><span class="sxs-lookup"><span data-stu-id="41c28-155">Run the .NET **AddTagsAndQuery** app to run the queries again.</span></span> <span data-ttu-id="41c28-156">Teraz **myDeviceId** powinny być wyświetlane w obu wyników zapytania.</span><span class="sxs-lookup"><span data-stu-id="41c28-156">This time **myDeviceId** should appear in both query results.</span></span>
   
    ![][img-addtagapp2]

## <a name="next-steps"></a><span data-ttu-id="41c28-157">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="41c28-157">Next steps</span></span>
<span data-ttu-id="41c28-158">W tym samouczku opisano konfigurowanie nowego centrum IoT Hub w witrynie Azure Portal, a następnie tworzenie tożsamości urządzenia w rejestrze tożsamości centrum.</span><span class="sxs-lookup"><span data-stu-id="41c28-158">In this tutorial, you configured a new IoT hub in the Azure portal, and then created a device identity in the IoT hub's identity registry.</span></span> <span data-ttu-id="41c28-159">Dodaje metadane urządzenia jako tagi z aplikacji zaplecza i zapisano aplikacji symulowane urządzenie informacji w raporcie urządzenia łączności w dwie urządzenia.</span><span class="sxs-lookup"><span data-stu-id="41c28-159">You added device metadata as tags from a back-end app, and wrote a simulated device app to report device connectivity information in the device twin.</span></span> <span data-ttu-id="41c28-160">Przedstawiono również sposób kwerendy te informacje przy użyciu języka przypominającego SQL Centrum IoT zapytania.</span><span class="sxs-lookup"><span data-stu-id="41c28-160">You also learned how to query this information using the SQL-like IoT Hub query language.</span></span>

<span data-ttu-id="41c28-161">Użyj następujących zasobów, aby dowiedzieć się, jak:</span><span class="sxs-lookup"><span data-stu-id="41c28-161">Use the following resources to learn how to:</span></span>

* <span data-ttu-id="41c28-162">wysyłanie danych telemetrycznych z urządzenia z [Rozpoczynanie pracy z Centrum IoT] [ lnk-iothub-getstarted] samouczka</span><span class="sxs-lookup"><span data-stu-id="41c28-162">send telemetry from devices with the [Get started with IoT Hub][lnk-iothub-getstarted] tutorial,</span></span>
* <span data-ttu-id="41c28-163">Konfigurowanie urządzeń przy użyciu właściwości żądaną dwie urządzenia z [Użyj żądanego właściwości, aby skonfigurować urządzenia] [ lnk-twin-how-to-configure] samouczka</span><span class="sxs-lookup"><span data-stu-id="41c28-163">configure devices using device twin's desired properties with the [Use desired properties to configure devices][lnk-twin-how-to-configure] tutorial,</span></span>
* <span data-ttu-id="41c28-164">kontrolowanie urządzenia interakcyjne (takich jak włączanie wentylator z aplikacji kontrolowane przez użytkownika) z [metody bezpośredniego] [ lnk-methods-tutorial] samouczka.</span><span class="sxs-lookup"><span data-stu-id="41c28-164">control devices interactively (such as turning on a fan from a user-controlled app) with the [Use direct methods][lnk-methods-tutorial] tutorial.</span></span>

<!-- images -->
[img-servicenuget]: media/iot-hub-csharp-node-twin-getstarted/servicesdknuget.png
[img-createapp]: media/iot-hub-csharp-node-twin-getstarted/createnetapp.png
[img-addtagapp]: media/iot-hub-csharp-node-twin-getstarted/addtagapp.png
[img-addtagapp2]: media/iot-hub-csharp-node-twin-getstarted/addtagapp2.png

<!-- links -->
[lnk-hub-sdks]: iot-hub-devguide-sdks.md
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[lnk-nuget-service-sdk]: https://www.nuget.org/packages/Microsoft.Azure.Devices/

[lnk-d2c]: iot-hub-devguide-messaging.md#device-to-cloud-messages
[lnk-methods]: iot-hub-devguide-direct-methods.md
[lnk-twins]: iot-hub-devguide-device-twins.md
[lnk-query]: iot-hub-devguide-query-language.md
[lnk-identity]: iot-hub-devguide-identity-registry.md

[lnk-iothub-getstarted]: iot-hub-node-node-getstarted.md
[lnk-methods-tutorial]: iot-hub-node-node-direct-methods.md
[lnk-twin-how-to-configure]: iot-hub-csharp-node-twin-how-to-configure.md

[lnk-dev-setup]: https://github.com/Azure/azure-iot-sdk-node/blob/master/doc/node-devbox-setup.md

