---
title: "aaaGet wprowadzenie twins urządzenia Azure IoT Hub (.NET/.NET) | Dokumentacja firmy Microsoft"
description: "Jak tooadd twins urządzenia Azure IoT Hub toouse tagów, a następnie użyj zapytania Centrum IoT. Używasz urządzenia Azure IoT hello zestawu SDK .NET tooimplement hello symulowane urządzenie aplikacji i hello zestawu SDK usług Azure IoT dla .NET tooimplement aplikacji usługi, który dodaje znaczniki hello i uruchamia hello zapytania Centrum IoT."
services: iot-hub
documentationcenter: node
author: dsk-2015
manager: timlt
editor: 
ms.assetid: f7e23b6e-bfde-4fba-a6ec-dbb0f0e005f4
ms.service: iot-hub
ms.devlang: node
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/15/2017
ms.author: dkshir
ms.openlocfilehash: 7fa73ac896c44e79c6522d252cd1515bd6e7bb2b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-device-twins-netnet"></a><span data-ttu-id="a5b4e-104">Rozpoczynanie pracy z urządzenia twins (.NET/.NET)</span><span class="sxs-lookup"><span data-stu-id="a5b4e-104">Get started with device twins (.NET/.NET)</span></span>
[!INCLUDE [iot-hub-selector-twin-get-started](../../includes/iot-hub-selector-twin-get-started.md)]

<span data-ttu-id="a5b4e-105">Na końcu hello tego samouczka konieczne będzie tych aplikacji konsoli .NET:</span><span class="sxs-lookup"><span data-stu-id="a5b4e-105">At hello end of this tutorial, you will have these .NET console apps:</span></span>

* <span data-ttu-id="a5b4e-106">**CreateDeviceIdentity**, aplikacji .NET, która tworzy tożsamości urządzenia i skojarzony klucz tooconnect aplikacji symulowane urządzenie.</span><span class="sxs-lookup"><span data-stu-id="a5b4e-106">**CreateDeviceIdentity**, a .NET app which creates a device identity and associated security key tooconnect your simulated device app.</span></span>
* <span data-ttu-id="a5b4e-107">**AddTagsAndQuery**, aplikacji zaplecza .NET, która dodaje znaczniki i zapytanie twins urządzenia.</span><span class="sxs-lookup"><span data-stu-id="a5b4e-107">**AddTagsAndQuery**, a .NET back-end app which adds tags and queries device twins.</span></span>
* <span data-ttu-id="a5b4e-108">**ReportConnectivity**, aplikacji urządzenia .NET, która symuluje urządzenie łączące Centrum IoT tooyour o tożsamości urządzenia hello utworzony wcześniej, a następnie raportuje stanu łączności.</span><span class="sxs-lookup"><span data-stu-id="a5b4e-108">**ReportConnectivity**, a .NET device app which simulates a device that connects tooyour IoT hub with hello device identity created earlier, and reports its connectivity condition.</span></span>

> [!NOTE]
> <span data-ttu-id="a5b4e-109">Artykuł Hello [Azure IoT SDK] [ lnk-hub-sdks] informacje na temat hello Azure IoT SDK służy toobuild zarówno urządzenia, jak i zaplecza aplikacji.</span><span class="sxs-lookup"><span data-stu-id="a5b4e-109">hello article [Azure IoT SDKs][lnk-hub-sdks] provides information about hello Azure IoT SDKs that you can use toobuild both device and back-end apps.</span></span>
> 
> 

<span data-ttu-id="a5b4e-110">toocomplete tego samouczka należy hello poniżej:</span><span class="sxs-lookup"><span data-stu-id="a5b4e-110">toocomplete this tutorial you need hello following:</span></span>

* <span data-ttu-id="a5b4e-111">Program Visual Studio 2015 lub Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="a5b4e-111">Visual Studio 2015 or Visual Studio 2017.</span></span>
* <span data-ttu-id="a5b4e-112">Aktywne konto platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="a5b4e-112">An active Azure account.</span></span> <span data-ttu-id="a5b4e-113">(Jeśli go nie masz, możesz utworzyć [bezpłatne konto próbne][lnk-free-trial] w zaledwie kilka minut).</span><span class="sxs-lookup"><span data-stu-id="a5b4e-113">(If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.)</span></span>

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity-portal](../../includes/iot-hub-get-started-create-device-identity-portal.md)]

<span data-ttu-id="a5b4e-114">Chcąc tożsamości urządzenia hello toocreate programowo zamiast tego, przeczytaj hello odpowiedniej sekcji w hello [połączenia Centrum IoT tooyour symulowane urządzenie przy użyciu platformy .NET] [ lnk-device-identity-csharp] artykułu.</span><span class="sxs-lookup"><span data-stu-id="a5b4e-114">If you want toocreate hello device identity programmatically instead, read hello corresponding section in hello [Connect your simulated device tooyour IoT hub using .NET][lnk-device-identity-csharp] article.</span></span>

## <a name="create-hello-service-app"></a><span data-ttu-id="a5b4e-115">Tworzenie aplikacji usługi hello</span><span class="sxs-lookup"><span data-stu-id="a5b4e-115">Create hello service app</span></span>
<span data-ttu-id="a5b4e-116">W tej sekcji Tworzenie aplikacji konsoli .NET (przy użyciu języka C#) dodające skojarzone z lokalizacji metadanych toohello urządzenia dwie **myDeviceId**.</span><span class="sxs-lookup"><span data-stu-id="a5b4e-116">In this section, you create a .NET console app (using C#) that adds location metadata toohello device twin associated with **myDeviceId**.</span></span> <span data-ttu-id="a5b4e-117">Następnie zapytania twins urządzenia hello przechowywane w Centrum IoT hello Wybieranie hello urządzeń znajdujących się w hello nam, a następnie hello tych, którzy zgłosili komórkowej połączenia.</span><span class="sxs-lookup"><span data-stu-id="a5b4e-117">It then queries hello device twins stored in hello IoT hub selecting hello devices located in hello US, and then hello ones that reported a cellular connection.</span></span>

1. <span data-ttu-id="a5b4e-118">W programie Visual Studio, należy dodać bieżącego rozwiązania toohello projektu Visual C# pulpitu systemu Windows klasycznego przy użyciu hello **aplikacji konsoli** szablonu projektu.</span><span class="sxs-lookup"><span data-stu-id="a5b4e-118">In Visual Studio, add a Visual C# Windows Classic Desktop project toohello current solution by using hello **Console Application** project template.</span></span> <span data-ttu-id="a5b4e-119">Nazwa projektu hello **AddTagsAndQuery**.</span><span class="sxs-lookup"><span data-stu-id="a5b4e-119">Name hello project **AddTagsAndQuery**.</span></span>
   
    ![Nowy projekt Visual C# Windows Classic Desktop][img-createapp]
1. <span data-ttu-id="a5b4e-121">W Eksploratorze rozwiązań kliknij prawym przyciskiem myszy hello **AddTagsAndQuery** projektu, a następnie kliknij przycisk **Zarządzaj pakietami NuGet...** .</span><span class="sxs-lookup"><span data-stu-id="a5b4e-121">In Solution Explorer, right-click hello **AddTagsAndQuery** project, and then click **Manage NuGet Packages...**.</span></span>
1. <span data-ttu-id="a5b4e-122">W hello **Menedżera pakietów NuGet** wybierz **Przeglądaj** i wyszukaj **microsoft.azure.devices**.</span><span class="sxs-lookup"><span data-stu-id="a5b4e-122">In hello **NuGet Package Manager** window, select **Browse** and search for **microsoft.azure.devices**.</span></span> <span data-ttu-id="a5b4e-123">Wybierz **zainstalować** tooinstall hello **Microsoft.Azure.Devices** pakietu i zaakceptuj warunki użytkowania hello.</span><span class="sxs-lookup"><span data-stu-id="a5b4e-123">Select **Install** tooinstall hello **Microsoft.Azure.Devices** package, and accept hello terms of use.</span></span> <span data-ttu-id="a5b4e-124">Ta procedura pliki do pobrania, instaluje i dodaje toohello odwołanie [zestawu SDK usług Azure IoT] [ lnk-nuget-service-sdk] NuGet pakiet i jego zależności.</span><span class="sxs-lookup"><span data-stu-id="a5b4e-124">This procedure downloads, installs, and adds a reference toohello [Azure IoT service SDK][lnk-nuget-service-sdk] NuGet package and its dependencies.</span></span>
   
    ![Okno Menedżera pakietów NuGet][img-servicenuget]
1. <span data-ttu-id="a5b4e-126">Dodaj następujące hello `using` instrukcji u góry hello hello **Program.cs** pliku:</span><span class="sxs-lookup"><span data-stu-id="a5b4e-126">Add hello following `using` statements at hello top of hello **Program.cs** file:</span></span>
   
        using Microsoft.Azure.Devices;
1. <span data-ttu-id="a5b4e-127">Dodaj następujące pola toohello hello **Program** klasy.</span><span class="sxs-lookup"><span data-stu-id="a5b4e-127">Add hello following fields toohello **Program** class.</span></span> <span data-ttu-id="a5b4e-128">Zastąp wartość symbolu zastępczego hello hello hello koncentratora, który został utworzony w poprzedniej sekcji hello parametry połączenia Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="a5b4e-128">Replace hello placeholder value with hello IoT Hub connection string for hello hub that you created in hello previous section.</span></span>
   
        static RegistryManager registryManager;
        static string connectionString = "{iot hub connection string}";
1. <span data-ttu-id="a5b4e-129">Dodaj następujące metody toohello hello **Program** klasy:</span><span class="sxs-lookup"><span data-stu-id="a5b4e-129">Add hello following method toohello **Program** class:</span></span>
   
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
   
    <span data-ttu-id="a5b4e-130">Witaj **RegistryManager** klasa przedstawia wszystkie hello metody wymagane toointeract z twins urządzenia z usługi hello.</span><span class="sxs-lookup"><span data-stu-id="a5b4e-130">hello **RegistryManager** class exposes all hello methods required toointeract with device twins from hello service.</span></span> <span data-ttu-id="a5b4e-131">Poprzedni kod Hello najpierw inicjuje hello **registryManager** obiektu, a następnie pobiera Witaj dwie urządzenia dla **myDeviceId**i na koniec aktualizuje jego tagi hello potrzeby informacji o lokalizacji.</span><span class="sxs-lookup"><span data-stu-id="a5b4e-131">hello previous code first initializes hello **registryManager** object, then retrieves hello device twin for **myDeviceId**, and finally updates its tags with hello desired location information.</span></span>
   
    <span data-ttu-id="a5b4e-132">Po zaktualizowaniu, wykonuje on dwa zapytania: hello najpierw wybiera tylko twins urządzenia hello urządzeń znajdujących się w hello **Redmond43** roślin i hello drugi refines hello zapytania tooselect tylko hello urządzeń podłączonych do sieci komórkowej.</span><span class="sxs-lookup"><span data-stu-id="a5b4e-132">After updating, it executes two queries: hello first selects only hello device twins of devices located in hello **Redmond43** plant, and hello second refines hello query tooselect only hello devices that are also connected through cellular network.</span></span>
   
    <span data-ttu-id="a5b4e-133">Należy pamiętać, że poprzedni kod hello, podczas tworzenia hello **zapytania** obiektów, określa maksymalną liczbę zwracanych dokumentów.</span><span class="sxs-lookup"><span data-stu-id="a5b4e-133">Note that hello previous code, when it creates hello **query** object, specifies a maximum number of returned documents.</span></span> <span data-ttu-id="a5b4e-134">Hello **zapytania** zawiera obiekt **HasMoreResults** właściwości typu boolean służy tooinvoke hello **GetNextAsTwinAsync** metody wszystkie tooretrieve wiele razy wyniki.</span><span class="sxs-lookup"><span data-stu-id="a5b4e-134">hello **query** object contains a **HasMoreResults** boolean property that you can use tooinvoke hello **GetNextAsTwinAsync** methods multiple times tooretrieve all results.</span></span> <span data-ttu-id="a5b4e-135">Wywołana metoda **GetNextAsJson** jest dostępna dla wyników, które są nie twins urządzenia, na przykład wyniki zapytań agregacji.</span><span class="sxs-lookup"><span data-stu-id="a5b4e-135">A method called **GetNextAsJson** is available for results that are not device twins, for example, results of aggregation queries.</span></span>
1. <span data-ttu-id="a5b4e-136">Na koniec należy dodać następujące wiersze toohello hello **Main** metody:</span><span class="sxs-lookup"><span data-stu-id="a5b4e-136">Finally, add hello following lines toohello **Main** method:</span></span>
   
        registryManager = RegistryManager.CreateFromConnectionString(connectionString);
        AddTagsAndQuery().Wait();
        Console.WriteLine("Press Enter tooexit.");
        Console.ReadLine();

1. <span data-ttu-id="a5b4e-137">W Eksploratorze rozwiązań hello, otwórz hello **projektów startowych ustawić...**  i upewnij się, że hello **akcji** dla **AddTagsAndQuery** projekt jest **Start**.</span><span class="sxs-lookup"><span data-stu-id="a5b4e-137">In hello Solution Explorer, open hello **Set StartUp projects...** and make sure hello **Action** for **AddTagsAndQuery** project is **Start**.</span></span> <span data-ttu-id="a5b4e-138">Utworzenie rozwiązania hello.</span><span class="sxs-lookup"><span data-stu-id="a5b4e-138">Build hello solution.</span></span>
1. <span data-ttu-id="a5b4e-139">Uruchomić tę aplikację, klikając prawym przyciskiem myszy na powitania **AddTagsAndQuery** projekt i wybierając **debugowania**, a następnie **Start nowe wystąpienie**.</span><span class="sxs-lookup"><span data-stu-id="a5b4e-139">Run this application by right-clicking on hello **AddTagsAndQuery** project and selecting **Debug**, followed by **Start new instance**.</span></span> <span data-ttu-id="a5b4e-140">Powinny pojawić się jedno urządzenie w wynikach hello hello zadać zapytania dla wszystkich urządzeń znajdujących się w **Redmond43** i Brak dla zapytania hello, która ogranicza hello powoduje toodevices używanego przez sieć komórkową.</span><span class="sxs-lookup"><span data-stu-id="a5b4e-140">You should see one device in hello results for hello query asking for all devices located in **Redmond43** and none for hello query that restricts hello results toodevices that use a cellular network.</span></span>
   
    ![Wyniki zapytania w oknie][img-addtagapp]

<span data-ttu-id="a5b4e-142">W następnej sekcji hello możesz utworzyć aplikację urządzenia, która raportuje informacje o łączności hello i zmiany hello wynik kwerendy hello w poprzedniej sekcji hello.</span><span class="sxs-lookup"><span data-stu-id="a5b4e-142">In hello next section, you create a device app that reports hello connectivity information and changes hello result of hello query in hello previous section.</span></span>

## <a name="create-hello-device-app"></a><span data-ttu-id="a5b4e-143">Tworzenie hello urządzenia aplikacji</span><span class="sxs-lookup"><span data-stu-id="a5b4e-143">Create hello device app</span></span>
<span data-ttu-id="a5b4e-144">W tej sekcji Tworzenie aplikacji konsoli .NET łączącego Centrum tooyour jako **myDeviceId**, a następnie aktualizuje informacje hello toocontain zgłoszone właściwości jest on podłączony za pomocą sieci komórkowej.</span><span class="sxs-lookup"><span data-stu-id="a5b4e-144">In this section, you create a .NET console app that connects tooyour hub as **myDeviceId**, and then updates its reported properties toocontain hello information that it is connected using a cellular network.</span></span>

1. <span data-ttu-id="a5b4e-145">W programie Visual Studio, należy dodać bieżącego rozwiązania toohello projektu Visual C# pulpitu systemu Windows klasycznego przy użyciu hello **aplikacji konsoli** szablonu projektu.</span><span class="sxs-lookup"><span data-stu-id="a5b4e-145">In Visual Studio, add a Visual C# Windows Classic Desktop project toohello current solution by using hello **Console Application** project template.</span></span> <span data-ttu-id="a5b4e-146">Nazwa projektu hello **ReportConnectivity**.</span><span class="sxs-lookup"><span data-stu-id="a5b4e-146">Name hello project **ReportConnectivity**.</span></span>
   
    ![Nowa aplikacja Visual C# Windows Classic urządzenia][img-createdeviceapp]
    
1. <span data-ttu-id="a5b4e-148">W Eksploratorze rozwiązań kliknij prawym przyciskiem myszy hello **ReportConnectivity** projektu, a następnie kliknij przycisk **Zarządzaj pakietami NuGet...** .</span><span class="sxs-lookup"><span data-stu-id="a5b4e-148">In Solution Explorer, right-click hello **ReportConnectivity** project, and then click **Manage NuGet Packages...**.</span></span>
1. <span data-ttu-id="a5b4e-149">W hello **Menedżera pakietów NuGet** wybierz **Przeglądaj** i wyszukaj **microsoft.azure.devices.client**.</span><span class="sxs-lookup"><span data-stu-id="a5b4e-149">In hello **NuGet Package Manager** window, select **Browse** and search for **microsoft.azure.devices.client**.</span></span> <span data-ttu-id="a5b4e-150">Wybierz **zainstalować** tooinstall hello **Microsoft.Azure.Devices.Client** pakietu i zaakceptuj warunki użytkowania hello.</span><span class="sxs-lookup"><span data-stu-id="a5b4e-150">Select **Install** tooinstall hello **Microsoft.Azure.Devices.Client** package, and accept hello terms of use.</span></span> <span data-ttu-id="a5b4e-151">Ta procedura pliki do pobrania, instaluje i dodaje toohello odwołanie [urządzenia Azure IoT SDK] [ lnk-nuget-client-sdk] NuGet pakiet i jego zależności.</span><span class="sxs-lookup"><span data-stu-id="a5b4e-151">This procedure downloads, installs, and adds a reference toohello [Azure IoT device SDK][lnk-nuget-client-sdk] NuGet package and its dependencies.</span></span>
   
    ![Aplikacja kliencka okna Menedżera pakietów NuGet][img-clientnuget]
1. <span data-ttu-id="a5b4e-153">Dodaj następujące hello `using` instrukcji u góry hello hello **Program.cs** pliku:</span><span class="sxs-lookup"><span data-stu-id="a5b4e-153">Add hello following `using` statements at hello top of hello **Program.cs** file:</span></span>
   
        using Microsoft.Azure.Devices.Client;
        using Microsoft.Azure.Devices.Shared;
        using Newtonsoft.Json;

1. <span data-ttu-id="a5b4e-154">Dodaj następujące pola toohello hello **Program** klasy.</span><span class="sxs-lookup"><span data-stu-id="a5b4e-154">Add hello following fields toohello **Program** class.</span></span> <span data-ttu-id="a5b4e-155">Zastąp wartość symbolu zastępczego hello ciąg połączenia urządzenia hello zanotowanym w poprzedniej sekcji hello.</span><span class="sxs-lookup"><span data-stu-id="a5b4e-155">Replace hello placeholder value with hello device connection string that you noted in hello previous section.</span></span>
   
        static string DeviceConnectionString = "HostName=<yourIotHubName>.azure-devices.net;DeviceId=<yourIotDeviceName>;SharedAccessKey=<yourIotDeviceAccessKey>";
        static DeviceClient Client = null;

1. <span data-ttu-id="a5b4e-156">Dodaj następujące metody toohello hello **Program** klasy:</span><span class="sxs-lookup"><span data-stu-id="a5b4e-156">Add hello following method toohello **Program** class:</span></span>

       public static async void InitClient()
        {
            try
            {
                Console.WriteLine("Connecting toohub");
                Client = DeviceClient.CreateFromConnectionString(DeviceConnectionString, TransportType.Mqtt);
                Console.WriteLine("Retrieving twin");
                await Client.GetTwinAsync();
            }
            catch (Exception ex)
            {
                Console.WriteLine();
                Console.WriteLine("Error in sample: {0}", ex.Message);
            }
        }

    <span data-ttu-id="a5b4e-157">Witaj **klienta** obiekt udostępnia wszystkie metody hello wymagają toointeract z twins urządzenia z hello urządzenia.</span><span class="sxs-lookup"><span data-stu-id="a5b4e-157">hello **Client** object exposes all hello methods you require toointeract with device twins from hello device.</span></span> <span data-ttu-id="a5b4e-158">Witaj kodzie pokazanym powyżej, hello inicjuje **klienta** obiektu, a następnie pobiera hello urządzenia dwie dla **myDeviceId**.</span><span class="sxs-lookup"><span data-stu-id="a5b4e-158">hello code shown above, initializes hello **Client** object, and then retrieves hello device twin for **myDeviceId**.</span></span>

1. <span data-ttu-id="a5b4e-159">Dodaj następujące metody toohello hello **Program** klasy:</span><span class="sxs-lookup"><span data-stu-id="a5b4e-159">Add hello following method toohello **Program** class:</span></span>
   
        public static async void ReportConnectivity()
        {
            try
            {
                Console.WriteLine("Sending connectivity data as reported property");
                
                TwinCollection reportedProperties, connectivity;
                reportedProperties = new TwinCollection();
                connectivity = new TwinCollection();
                connectivity["type"] = "cellular";
                reportedProperties["connectivity"] = connectivity;
                await Client.UpdateReportedPropertiesAsync(reportedProperties);
            }
            catch (Exception ex)
            {
                Console.WriteLine();
                Console.WriteLine("Error in sample: {0}", ex.Message);
            }
        }

   <span data-ttu-id="a5b4e-160">Witaj kodu powyżej aktualizacje **myDeviceId**obiektu podać właściwość o informacje dotyczące łączności hello.</span><span class="sxs-lookup"><span data-stu-id="a5b4e-160">hello code above updates **myDeviceId**'s reported property with hello connectivity information.</span></span>

1. <span data-ttu-id="a5b4e-161">Na koniec należy dodać następujące wiersze toohello hello **Main** metody:</span><span class="sxs-lookup"><span data-stu-id="a5b4e-161">Finally, add hello following lines toohello **Main** method:</span></span>
   
       try
       {
            InitClient();
            ReportConnectivity();
       }
       catch (Exception ex)
       {
            Console.WriteLine();
            Console.WriteLine("Error in sample: {0}", ex.Message);
       }
       Console.WriteLine("Press Enter tooexit.");
       Console.ReadLine();

1. <span data-ttu-id="a5b4e-162">W Eksploratorze rozwiązań hello, otwórz hello **projektów startowych ustawić...**  i upewnij się, że hello **akcji** dla **ReportConnectivity** projekt jest **Start**.</span><span class="sxs-lookup"><span data-stu-id="a5b4e-162">In hello Solution Explorer, open hello **Set StartUp projects...** and make sure hello **Action** for **ReportConnectivity** project is **Start**.</span></span> <span data-ttu-id="a5b4e-163">Utworzenie rozwiązania hello.</span><span class="sxs-lookup"><span data-stu-id="a5b4e-163">Build hello solution.</span></span>
1. <span data-ttu-id="a5b4e-164">Uruchomić tę aplikację, klikając prawym przyciskiem myszy na powitania **ReportConnectivity** projekt i wybierając **debugowania**, a następnie **Start nowe wystąpienie**.</span><span class="sxs-lookup"><span data-stu-id="a5b4e-164">Run this application by right-clicking on hello **ReportConnectivity** project and selecting **Debug**, followed by **Start new instance**.</span></span> <span data-ttu-id="a5b4e-165">Powinny pojawić się ona pobieranie Witaj dwie informacje, a następnie wysyłając łączność *podać właściwość*.</span><span class="sxs-lookup"><span data-stu-id="a5b4e-165">You should see it getting hello twin information, and then sending connectivity as a *reported property*.</span></span>
   
    ![Uruchom urządzenia aplikacji tooreport łączności][img-rundeviceapp]
    
    
1. <span data-ttu-id="a5b4e-167">Teraz, gdy hello Urządzenie zgłosiło jego informacje dotyczące łączności, powinna pojawić się w obu zapytania.</span><span class="sxs-lookup"><span data-stu-id="a5b4e-167">Now that hello device reported its connectivity information, it should appear in both queries.</span></span> <span data-ttu-id="a5b4e-168">Uruchom hello .NET **AddTagsAndQuery** aplikacji hello toorun wysyła zapytanie ponownie.</span><span class="sxs-lookup"><span data-stu-id="a5b4e-168">Run hello .NET **AddTagsAndQuery** app toorun hello queries again.</span></span> <span data-ttu-id="a5b4e-169">Teraz **myDeviceId** powinny być wyświetlane w obu wyników zapytania.</span><span class="sxs-lookup"><span data-stu-id="a5b4e-169">This time **myDeviceId** should appear in both query results.</span></span>
   
    ![Łączność urządzeń zgłoszonych pomyślnie][img-tagappsuccess]

## <a name="next-steps"></a><span data-ttu-id="a5b4e-171">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="a5b4e-171">Next steps</span></span>
<span data-ttu-id="a5b4e-172">W tym samouczku został skonfigurowany nowego centrum IoT w portalu Azure hello i w rejestrze tożsamości Centrum IoT hello zostanie utworzona tożsamość urządzenia.</span><span class="sxs-lookup"><span data-stu-id="a5b4e-172">In this tutorial, you configured a new IoT hub in hello Azure portal, and then created a device identity in hello IoT hub's identity registry.</span></span> <span data-ttu-id="a5b4e-173">Dodaje metadane urządzenia jako tagi z aplikacji zaplecza i zapisane symulowane urządzenie tooreport urządzenia łączności informacji o aplikacji w Witaj dwie urządzenia.</span><span class="sxs-lookup"><span data-stu-id="a5b4e-173">You added device metadata as tags from a back-end app, and wrote a simulated device app tooreport device connectivity information in hello device twin.</span></span> <span data-ttu-id="a5b4e-174">Przedstawiono również sposób tooquery te informacje przy użyciu języka kwerend hello Centrum IoT przypominającego SQL.</span><span class="sxs-lookup"><span data-stu-id="a5b4e-174">You also learned how tooquery this information using hello SQL-like IoT Hub query language.</span></span>

<span data-ttu-id="a5b4e-175">Hello Użyj następujących zasobów toolearn jak do:</span><span class="sxs-lookup"><span data-stu-id="a5b4e-175">Use hello following resources toolearn how to:</span></span>

* <span data-ttu-id="a5b4e-176">wysłać dane telemetryczne z urządzenia z hello [Rozpoczynanie pracy z Centrum IoT] [ lnk-iothub-getstarted] samouczka</span><span class="sxs-lookup"><span data-stu-id="a5b4e-176">send telemetry from devices with hello [Get started with IoT Hub][lnk-iothub-getstarted] tutorial,</span></span>
* <span data-ttu-id="a5b4e-177">Konfigurowanie urządzeń przy użyciu właściwości żądaną dwie urządzenia z hello [Użyj potrzeby urządzeń tooconfigure właściwości] [ lnk-twin-how-to-configure] samouczka</span><span class="sxs-lookup"><span data-stu-id="a5b4e-177">configure devices using device twin's desired properties with hello [Use desired properties tooconfigure devices][lnk-twin-how-to-configure] tutorial,</span></span>
* <span data-ttu-id="a5b4e-178">kontrolowanie urządzenia interakcyjne (takich jak włączanie wentylator z aplikacji kontrolowane przez użytkownika) z hello [metody bezpośredniego] [ lnk-methods-tutorial] samouczka.</span><span class="sxs-lookup"><span data-stu-id="a5b4e-178">control devices interactively (such as turning on a fan from a user-controlled app) with hello [Use direct methods][lnk-methods-tutorial] tutorial.</span></span>

<!-- images -->
[img-servicenuget]: media/iot-hub-csharp-csharp-twin-getstarted/servicesdknuget.png
[img-createapp]: media/iot-hub-csharp-csharp-twin-getstarted/createnetapp.png
[img-addtagapp]: media/iot-hub-csharp-csharp-twin-getstarted/addtagapp.png
[img-createdeviceapp]: media/iot-hub-csharp-csharp-twin-getstarted/createdeviceapp.png
[img-clientnuget]: media/iot-hub-csharp-csharp-twin-getstarted/clientsdknuget.png
[img-rundeviceapp]: media/iot-hub-csharp-csharp-twin-getstarted/rundeviceapp.png
[img-tagappsuccess]: media/iot-hub-csharp-csharp-twin-getstarted/tagappsuccess.png

<!-- links -->
[lnk-hub-sdks]: iot-hub-devguide-sdks.md
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[lnk-nuget-service-sdk]: https://www.nuget.org/packages/Microsoft.Azure.Devices/
[lnk-nuget-client-sdk]: https://www.nuget.org/packages/Microsoft.Azure.Devices.Client/

[lnk-device-identity-csharp]: iot-hub-csharp-csharp-getstarted.md#DeviceIdentity_csharp
[lnk-d2c]: iot-hub-devguide-messaging.md#device-to-cloud-messages
[lnk-methods]: iot-hub-devguide-direct-methods.md
[lnk-twins]: iot-hub-devguide-device-twins.md
[lnk-query]: iot-hub-devguide-query-language.md
[lnk-identity]: iot-hub-devguide-identity-registry.md

[lnk-iothub-getstarted]: iot-hub-csharp-csharp-getstarted.md
[lnk-methods-tutorial]: iot-hub-node-node-direct-methods.md
[lnk-twin-how-to-configure]: iot-hub-csharp-node-twin-how-to-configure.md

[lnk-dev-setup]: https://github.com/Azure/azure-iot-sdk-node/blob/master/doc/node-devbox-setup.md

