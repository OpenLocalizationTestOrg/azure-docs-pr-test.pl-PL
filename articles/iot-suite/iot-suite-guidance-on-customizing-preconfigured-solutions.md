---
title: "Dostosowywanie wstępnie rozwiązania | Dokumentacja firmy Microsoft"
description: "Zawiera wskazówki dotyczące sposobu dostosowywania rozwiązań wstępnie pakiet IoT Azure."
services: 
suite: iot-suite
documentationcenter: .net
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 4653ae53-4110-4a10-bd6c-7dc034c293a8
ms.service: iot-suite
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/15/2017
ms.author: corywink
ms.openlocfilehash: bdf4cd89d5ad0392337dfe761108608d506adf18
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="customize-a-preconfigured-solution"></a><span data-ttu-id="2c678-103">Dostosowanie wstępnie skonfigurowanego rozwiązania</span><span class="sxs-lookup"><span data-stu-id="2c678-103">Customize a preconfigured solution</span></span>

<span data-ttu-id="2c678-104">Wstępnie skonfigurowanych rozwiązań wyposażone w pakiet IoT Azure przedstawienie usług w obrębie zestawu, które współpracują, aby dostarczać rozwiązanie end-to-end.</span><span class="sxs-lookup"><span data-stu-id="2c678-104">The preconfigured solutions provided with the Azure IoT Suite demonstrate the services within the suite working together to deliver an end-to-end solution.</span></span> <span data-ttu-id="2c678-105">Z tego punktu początkowego istnieją różnych miejscach, w których można rozszerzać i dostosować rozwiązania dla konkretnych scenariuszy.</span><span class="sxs-lookup"><span data-stu-id="2c678-105">From this starting point, there are various places in which you can extend and customize the solution for specific scenarios.</span></span> <span data-ttu-id="2c678-106">W poniższych sekcjach opisano typowe punkty dostosowania.</span><span class="sxs-lookup"><span data-stu-id="2c678-106">The following sections describe these common customization points.</span></span>

## <a name="find-the-source-code"></a><span data-ttu-id="2c678-107">Znaleźć kodu źródłowego</span><span class="sxs-lookup"><span data-stu-id="2c678-107">Find the source code</span></span>

<span data-ttu-id="2c678-108">Kod źródłowy dla wstępnie skonfigurowanych rozwiązań jest dostępna w witrynie GitHub w następujących repozytoria:</span><span class="sxs-lookup"><span data-stu-id="2c678-108">The source code for the preconfigured solutions is available on GitHub in the following repositories:</span></span>

* <span data-ttu-id="2c678-109">Monitorowanie zdalne: [https://www.github.com/Azure/azure-iot-remote-monitoring](https://github.com/Azure/azure-iot-remote-monitoring)</span><span class="sxs-lookup"><span data-stu-id="2c678-109">Remote Monitoring: [https://www.github.com/Azure/azure-iot-remote-monitoring](https://github.com/Azure/azure-iot-remote-monitoring)</span></span>
* <span data-ttu-id="2c678-110">Konserwacji predykcyjnej: [https://github.com/Azure/azure-iot-predictive-maintenance](https://github.com/Azure/azure-iot-predictive-maintenance)</span><span class="sxs-lookup"><span data-stu-id="2c678-110">Predictive Maintenance: [https://github.com/Azure/azure-iot-predictive-maintenance](https://github.com/Azure/azure-iot-predictive-maintenance)</span></span>
* <span data-ttu-id="2c678-111">Fabryka połączenia: [https://github.com/Azure/azure-iot-connected-factory](https://github.com/Azure/azure-iot-connected-factory)</span><span class="sxs-lookup"><span data-stu-id="2c678-111">Connected factory: [https://github.com/Azure/azure-iot-connected-factory](https://github.com/Azure/azure-iot-connected-factory)</span></span>

<span data-ttu-id="2c678-112">Aby zademonstrować wzorców i procedur wykorzystywanych do implementowania end-to-end rozwiązania IoT przy użyciu pakietu IoT Azure znajduje się kod źródłowy dla wstępnie skonfigurowanych rozwiązań.</span><span class="sxs-lookup"><span data-stu-id="2c678-112">The source code for the preconfigured solutions is provided to demonstrate the patterns and practices used to implement the end-to-end functionality of an IoT solution using Azure IoT Suite.</span></span> <span data-ttu-id="2c678-113">Można znaleźć więcej informacji na temat sposobu tworzenia i wdrażania rozwiązań w repozytoriów GitHub.</span><span class="sxs-lookup"><span data-stu-id="2c678-113">You can find more information about how to build and deploy the solutions in the GitHub repositories.</span></span>

## <a name="change-the-preconfigured-rules"></a><span data-ttu-id="2c678-114">Zmień wstępnie skonfigurowanych reguł</span><span class="sxs-lookup"><span data-stu-id="2c678-114">Change the preconfigured rules</span></span>

<span data-ttu-id="2c678-115">Rozwiązanie monitorowania zdalnego obejmuje trzy [Azure Stream Analytics](https://azure.microsoft.com/services/stream-analytics/) zadania obsługi informacji o urządzeniu, telemetrii i logiki reguły w rozwiązaniu.</span><span class="sxs-lookup"><span data-stu-id="2c678-115">The remote monitoring solution includes three [Azure Stream Analytics](https://azure.microsoft.com/services/stream-analytics/) jobs to handle device information, telemetry, and rules logic in the solution.</span></span>

<span data-ttu-id="2c678-116">Trzy strumienia zadania usługi analiza i ich składni opisano szczegółowo w [monitorowania zdalnego wstępnie skonfigurowane rozwiązanie wskazówki](iot-suite-remote-monitoring-sample-walkthrough.md).</span><span class="sxs-lookup"><span data-stu-id="2c678-116">The three stream analytics jobs and their syntax are described in depth in the [Remote monitoring preconfigured solution walkthrough](iot-suite-remote-monitoring-sample-walkthrough.md).</span></span> 

<span data-ttu-id="2c678-117">Edytowanie tych zadań bezpośrednio do alter logiki lub dodać logikę określonych do danego scenariusza.</span><span class="sxs-lookup"><span data-stu-id="2c678-117">You can edit these jobs directly to alter the logic, or add logic specific to your scenario.</span></span> <span data-ttu-id="2c678-118">Zadania usługi analiza strumienia można znaleźć w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="2c678-118">You can find the Stream Analytics jobs as follows:</span></span>

1. <span data-ttu-id="2c678-119">Przejdź do [portalu Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="2c678-119">Go to [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="2c678-120">Przejdź do grupy zasobów o nazwie identycznej z nazwą rozwiązania IoT.</span><span class="sxs-lookup"><span data-stu-id="2c678-120">Navigate to the resource group with the same name as your IoT solution.</span></span> 
3. <span data-ttu-id="2c678-121">Wybierz zadanie usługi analiza strumienia Azure, którą chcesz zmodyfikować.</span><span class="sxs-lookup"><span data-stu-id="2c678-121">Select the Azure Stream Analytics job you'd like to modify.</span></span> 
4. <span data-ttu-id="2c678-122">Zatrzymaj zadanie, wybierając **zatrzymać** zestawu poleceń.</span><span class="sxs-lookup"><span data-stu-id="2c678-122">Stop the job by selecting **Stop** in the set of commands.</span></span> 
5. <span data-ttu-id="2c678-123">Edytowanie danych wejściowych, zapytań i danych wyjściowych.</span><span class="sxs-lookup"><span data-stu-id="2c678-123">Edit the inputs, query, and outputs.</span></span>
   
    <span data-ttu-id="2c678-124">Prostą modyfikację jest zmiana kwerendy dotyczącej **reguły** zadanie, aby użyć **"<"** zamiast **">"**.</span><span class="sxs-lookup"><span data-stu-id="2c678-124">A simple modification is to change the query for the **Rules** job to use a **"<"** instead of a **">"**.</span></span> <span data-ttu-id="2c678-125">Portal rozwiązania pozostanie **">"** podczas edycji reguły, ale Zwróć uwagę, jak zachowanie jest odwrócony z powodu zmiany w podstawowym zadania.</span><span class="sxs-lookup"><span data-stu-id="2c678-125">The solution portal still shows **">"** when you edit a rule, but notice how the behavior is flipped due to the change in the underlying job.</span></span>
6. <span data-ttu-id="2c678-126">Uruchom zadanie</span><span class="sxs-lookup"><span data-stu-id="2c678-126">Start the job</span></span>

> [!NOTE]
> <span data-ttu-id="2c678-127">Zdalnego pulpitu nawigacyjnego monitorowania zależy od określonych danych, więc zmiany zadania może spowodować niepowodzenie pulpitu nawigacyjnego.</span><span class="sxs-lookup"><span data-stu-id="2c678-127">The remote monitoring dashboard depends on specific data, so altering the jobs can cause the dashboard to fail.</span></span>

## <a name="add-your-own-rules"></a><span data-ttu-id="2c678-128">Dodaj własne reguły</span><span class="sxs-lookup"><span data-stu-id="2c678-128">Add your own rules</span></span>

<span data-ttu-id="2c678-129">Oprócz zmiana wstępnie skonfigurowane zadania usługi analiza strumienia Azure, można użyć portalu Azure, aby dodać nowe zadania, lub dodawanie nowych zapytań do istniejącego zadania.</span><span class="sxs-lookup"><span data-stu-id="2c678-129">In addition to changing the preconfigured Azure Stream Analytics jobs, you can use the Azure portal to add new jobs or add new queries to existing jobs.</span></span>

## <a name="customize-devices"></a><span data-ttu-id="2c678-130">Dostosowywanie urządzeń</span><span class="sxs-lookup"><span data-stu-id="2c678-130">Customize devices</span></span>

<span data-ttu-id="2c678-131">Jedną z najbardziej typowych działań rozszerzenia jest praca z urządzeniami, które są specyficzne dla danego scenariusza.</span><span class="sxs-lookup"><span data-stu-id="2c678-131">One of the most common extension activities is working with devices specific to your scenario.</span></span> <span data-ttu-id="2c678-132">Istnieje kilka metod do pracy z urządzeń.</span><span class="sxs-lookup"><span data-stu-id="2c678-132">There are several methods for working with devices.</span></span> <span data-ttu-id="2c678-133">Te metody obejmują zmiany symulowane urządzenie, aby dopasować danego scenariusza lub przy użyciu [SDK urządzenia IoT] [ IoT Device SDK] Podłącz urządzenie fizyczne do rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="2c678-133">These methods include altering a simulated device to match your scenario, or using the [IoT Device SDK][IoT Device SDK] to connect your physical device to the solution.</span></span>

<span data-ttu-id="2c678-134">Przewodnik krok po kroku dotyczący dodawania urządzeń, zobacz [urządzenia łączenie pakiet Iot](iot-suite-connecting-devices.md) artykułu i [zdalnego monitorowania przykład zestawu SDK C](https://github.com/Azure/azure-iot-sdk-c/tree/master/serializer/samples/remote_monitoring).</span><span class="sxs-lookup"><span data-stu-id="2c678-134">For a step-by-step guide to adding devices, see the [Iot Suite Connecting Devices](iot-suite-connecting-devices.md) article and the [remote monitoring C SDK Sample](https://github.com/Azure/azure-iot-sdk-c/tree/master/serializer/samples/remote_monitoring).</span></span> <span data-ttu-id="2c678-135">Ten przykład jest przeznaczona do pracy z zdalnego wstępnie skonfigurowane rozwiązanie monitorowania.</span><span class="sxs-lookup"><span data-stu-id="2c678-135">This sample is designed to work with the remote monitoring preconfigured solution.</span></span>

### <a name="create-your-own-simulated-device"></a><span data-ttu-id="2c678-136">Utworzyć symulowane urządzenie</span><span class="sxs-lookup"><span data-stu-id="2c678-136">Create your own simulated device</span></span>

<span data-ttu-id="2c678-137">Uwzględnione w [zdalnej kontroli kodu źródłowego rozwiązania](https://github.com/Azure/azure-iot-remote-monitoring), jest symulatora .NET.</span><span class="sxs-lookup"><span data-stu-id="2c678-137">Included in the [remote monitoring solution source code](https://github.com/Azure/azure-iot-remote-monitoring), is a .NET simulator.</span></span> <span data-ttu-id="2c678-138">Ta symulator jest udostępniane w ramach rozwiązania i można zmienić go wysłać innych metadanych, telemetrii, i reagowanie na inne polecenia i metody.</span><span class="sxs-lookup"><span data-stu-id="2c678-138">This simulator is the one provisioned as part of the solution and you can alter it to send different metadata, telemetry, and respond to different commands and methods.</span></span>

<span data-ttu-id="2c678-139">Symulator wstępnie skonfigurowane w zdalnym wstępnie skonfigurowane rozwiązanie monitorowania symuluje lodówki urządzenia, który emituje temperatury i wilgotności telemetrii.</span><span class="sxs-lookup"><span data-stu-id="2c678-139">The preconfigured simulator in the remote monitoring preconfigured solution simulates a cooler device that emits temperature and humidity telemetry.</span></span> <span data-ttu-id="2c678-140">Można zmodyfikować w symulatorze [Simulator.WebJob](https://github.com/Azure/azure-iot-remote-monitoring/tree/master/Simulator/Simulator.WebJob) projektu, gdy zostały rozwidlone repozytorium GitHub.</span><span class="sxs-lookup"><span data-stu-id="2c678-140">You can modify the simulator in the [Simulator.WebJob](https://github.com/Azure/azure-iot-remote-monitoring/tree/master/Simulator/Simulator.WebJob) project when you've forked the GitHub repository.</span></span>

### <a name="available-locations-for-simulated-devices"></a><span data-ttu-id="2c678-141">Dostępne lokalizacje symulowanego urządzenia</span><span class="sxs-lookup"><span data-stu-id="2c678-141">Available locations for simulated devices</span></span>

<span data-ttu-id="2c678-142">Domyślny zbiór lokalizacji jest w Seattle/Redmond, Washington, USA.</span><span class="sxs-lookup"><span data-stu-id="2c678-142">The default set of locations is in Seattle/Redmond, Washington, United States of America.</span></span> <span data-ttu-id="2c678-143">Możesz zmienić te lokalizacje w [SampleDeviceFactory.cs][lnk-sample-device-factory].</span><span class="sxs-lookup"><span data-stu-id="2c678-143">You can change these locations in [SampleDeviceFactory.cs][lnk-sample-device-factory].</span></span>

### <a name="add-a-desired-property-update-handler-to-the-simulator"></a><span data-ttu-id="2c678-144">Dodaj program obsługi aktualizacji żądanej właściwości do symulatora</span><span class="sxs-lookup"><span data-stu-id="2c678-144">Add a desired property update handler to the simulator</span></span>

<span data-ttu-id="2c678-145">Można ustawić wartości dla żądanej właściwości dla urządzenia w portalu rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="2c678-145">You can set a value for a desired property for a device in the solution portal.</span></span> <span data-ttu-id="2c678-146">Jest obowiązkiem urządzenia do obsługi właściwości żądania zmiany, gdy urządzenie pobiera wartość żądanej właściwości.</span><span class="sxs-lookup"><span data-stu-id="2c678-146">It is the responsibility of the device to handle the property change request when the device retrieves the desired property value.</span></span> <span data-ttu-id="2c678-147">Aby dodać obsługę zmiany wartości właściwości w ramach żądanej właściwości, należy dodać program obsługi do symulatora.</span><span class="sxs-lookup"><span data-stu-id="2c678-147">To add support for a property value change through a desired property, you need to add a handler to the simulator.</span></span>

<span data-ttu-id="2c678-148">Symulator zawiera obsługę **SetPointTemp** i **TelemetryInterval** aktualizowanych przez ustawienie właściwości żądane wartości w portalu rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="2c678-148">The simulator contains handlers for the **SetPointTemp** and **TelemetryInterval** properties that you can update by setting desired values in the solution portal.</span></span>

<span data-ttu-id="2c678-149">W poniższym przykładzie pokazano programu obsługi **SetPointTemp** wymaganą właściwość w **CoolerDevice** klasy:</span><span class="sxs-lookup"><span data-stu-id="2c678-149">The following example shows the handler for the **SetPointTemp** desired property in the **CoolerDevice** class:</span></span>

```csharp
protected async Task OnSetPointTempUpdate(object value)
{
    var telemetry = _telemetryController as ITelemetryWithSetPointTemperature;
    telemetry.SetPointTemperature = Convert.ToDouble(value);

    await SetReportedPropertyAsync(SetPointTempPropertyName, telemetry.SetPointTemperature);
}
```

<span data-ttu-id="2c678-150">Ta metoda aktualizacji temperatury punktu danych telemetrycznych i następnie raportuje zmiany ją do Centrum IoT przez ustawienie właściwości zgłoszone.</span><span class="sxs-lookup"><span data-stu-id="2c678-150">This method updates the telemetry point temperature and then reports the change back to IoT Hub by setting a reported property.</span></span>

<span data-ttu-id="2c678-151">Wykonując wzorca w poprzednim przykładzie, można dodać własne programy obsługi dla własnych właściwości.</span><span class="sxs-lookup"><span data-stu-id="2c678-151">You can add your own handlers for your own properties by following the pattern in the preceding example.</span></span>

<span data-ttu-id="2c678-152">Należy także powiązać żądanej właściwości do programu obsługi, jak pokazano w poniższym przykładzie z **CoolerDevice** konstruktora:</span><span class="sxs-lookup"><span data-stu-id="2c678-152">You must also bind the desired property to the handler as shown in the following example from the **CoolerDevice** constructor:</span></span>

```csharp
_desiredPropertyUpdateHandlers.Add(SetPointTempPropertyName, OnSetPointTempUpdate);
```

<span data-ttu-id="2c678-153">Należy pamiętać, że **SetPointTempPropertyName** jest stałą zdefiniowany jako "Config.SetPointTemp".</span><span class="sxs-lookup"><span data-stu-id="2c678-153">Note that **SetPointTempPropertyName** is a constant defined as "Config.SetPointTemp".</span></span>

### <a name="add-support-for-a-new-method-to-the-simulator"></a><span data-ttu-id="2c678-154">Dodaj obsługę nowej metody do symulatora</span><span class="sxs-lookup"><span data-stu-id="2c678-154">Add support for a new method to the simulator</span></span>

<span data-ttu-id="2c678-155">Symulator, aby dodać nową obsługę można dostosować [— metoda (metoda bezpośrednia)][lnk-direct-methods].</span><span class="sxs-lookup"><span data-stu-id="2c678-155">You can customize the simulator to add support for a new [method (direct method)][lnk-direct-methods].</span></span> <span data-ttu-id="2c678-156">Istnieją dwa kluczowe kroki wymagane:</span><span class="sxs-lookup"><span data-stu-id="2c678-156">There are two key steps required:</span></span>

- <span data-ttu-id="2c678-157">Symulator należy powiadomić Centrum IoT w wstępnie skonfigurowane rozwiązanie szczegółowe informacje o metodzie.</span><span class="sxs-lookup"><span data-stu-id="2c678-157">The simulator must notify the IoT hub in the preconfigured solution with details of the method.</span></span>
- <span data-ttu-id="2c678-158">Symulator musi zawierać kod obsługi wywołania metody, uruchamiając go z **szczegóły urządzenia** panelu w Eksploratorze rozwiązań i za pomocą zadania.</span><span class="sxs-lookup"><span data-stu-id="2c678-158">The simulator must include code to handle the method call when you invoke it from the **Device details** panel in the solution explorer or through a job.</span></span>

<span data-ttu-id="2c678-159">Zdalne monitorowanie wstępnie skonfigurowane rozwiązanie używa *zgłosił właściwości* wysłać szczegóły obsługiwane metody do Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="2c678-159">The remote monitoring preconfigured solution uses *reported properties* to send details of supported methods to IoT hub.</span></span> <span data-ttu-id="2c678-160">Zaplecze rozwiązania przechowuje listę wszystkich metod obsługiwanych przez poszczególne urządzenia oraz Historia wywołań metod.</span><span class="sxs-lookup"><span data-stu-id="2c678-160">The solution back end maintains a list of all the methods supported by each device along with a history of method invocations.</span></span> <span data-ttu-id="2c678-161">Możesz wyświetlić te informacje o urządzeniach i wywołania metod w portalu rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="2c678-161">You can view this information about devices and invoke methods in the solution portal.</span></span>

<span data-ttu-id="2c678-162">Aby powiadomić Centrum IoT, czy urządzenie obsługuje metodę, urządzenia, należy dodać szczegóły metody **SupportedMethods** węzła we właściwościach zgłoszone:</span><span class="sxs-lookup"><span data-stu-id="2c678-162">To notify the IoT hub that a device supports a method, the device must add details of the method to the **SupportedMethods** node in the reported properties:</span></span>

```json
"SupportedMethods": {
  "<method signature>": "<method description>",
  "<method signature>": "<method description>"
}
```

<span data-ttu-id="2c678-163">Podpis metody ma następujący format: `<method name>--<parameter #0 name>-<parameter #1 type>-...-<parameter #n name>-<parameter #n type>`.</span><span class="sxs-lookup"><span data-stu-id="2c678-163">The method signature has the following format: `<method name>--<parameter #0 name>-<parameter #1 type>-...-<parameter #n name>-<parameter #n type>`.</span></span> <span data-ttu-id="2c678-164">Na przykład, aby określić **InitiateFirmwareUpdate** metoda oczekuje parametru ciągu o nazwie **FwPackageURI**, użyj następujących podpis metody:</span><span class="sxs-lookup"><span data-stu-id="2c678-164">For example, to specify the **InitiateFirmwareUpdate** method expects a string parameter named **FwPackageURI**, use the following method signature:</span></span>

```json
InitiateFirmwareUpate--FwPackageURI-string: "description of method"
```

<span data-ttu-id="2c678-165">Dla listy typów obsługiwanych parametrów, zobacz **CommandTypes** klasy w projekcie infrastruktury.</span><span class="sxs-lookup"><span data-stu-id="2c678-165">For a list of supported parameter types, see the **CommandTypes** class in the Infrastructure project.</span></span>

<span data-ttu-id="2c678-166">Aby usunąć metody, należy ustawić podpis metody `null` we właściwościach zgłoszony.</span><span class="sxs-lookup"><span data-stu-id="2c678-166">To delete a method, set the method signature to `null` in the reported properties.</span></span>

> [!NOTE]
> <span data-ttu-id="2c678-167">Po odebraniu zaplecza rozwiązania tylko aktualizuje informacje o obsługiwanych metod *informacje o urządzeniu* wiadomości z urządzenia.</span><span class="sxs-lookup"><span data-stu-id="2c678-167">The solution back end only updates information about supported methods when it receives a *device information* message from the device.</span></span>

<span data-ttu-id="2c678-168">Poniższy przykładowy kod z **SampleDeviceFactory** klasy w projekcie wspólnej pokazano, jak dodać metodę do listy **SupportedMethods** we właściwościach zgłoszone wysyłane przez urządzenie:</span><span class="sxs-lookup"><span data-stu-id="2c678-168">The following code sample from the **SampleDeviceFactory** class in the Common project shows how to add a method to the list of **SupportedMethods** in the reported properties sent by the device:</span></span>

```csharp
device.Commands.Add(new Command(
    "InitiateFirmwareUpdate",
    DeliveryType.Method,
    "Updates device Firmware. Use parameter 'FwPackageUri' to specifiy the URI of the firmware file, e.g. https://iotrmassets.blob.core.windows.net/firmwares/FW20.bin",
    new[] { new Parameter("FwPackageUri", "string") }
));
```

<span data-ttu-id="2c678-169">Następujący fragment kodu dodaje szczegóły **InitiateFirmwareUpdate** metody, łącznie z tekstem, które mają być wyświetlane w portalu rozwiązania i szczegółowe informacje o parametrach wymaganej metody.</span><span class="sxs-lookup"><span data-stu-id="2c678-169">This code snippet adds details of the **InitiateFirmwareUpdate** method including text to display in the solution portal and details of the required method parameters.</span></span>

<span data-ttu-id="2c678-170">Symulator wysyła właściwości zgłoszone, łącznie z listą obsługiwanych metod, aby Centrum IoT podczas uruchamiania symulatora.</span><span class="sxs-lookup"><span data-stu-id="2c678-170">The simulator sends reported properties, including the list of supported methods, to IoT Hub when the simulator starts.</span></span>

<span data-ttu-id="2c678-171">Dodaj program obsługi do kodu symulatora dla poszczególnych metod obsługiwanych.</span><span class="sxs-lookup"><span data-stu-id="2c678-171">Add a handler to the simulator code for each method it supports.</span></span> <span data-ttu-id="2c678-172">Widać istniejących programów obsługi w **CoolerDevice** klasy w projekcie Simulator.WebJob.</span><span class="sxs-lookup"><span data-stu-id="2c678-172">You can see the existing handlers in the **CoolerDevice** class in the Simulator.WebJob project.</span></span> <span data-ttu-id="2c678-173">W poniższym przykładzie pokazano programu obsługi **InitiateFirmwareUpdate** metody:</span><span class="sxs-lookup"><span data-stu-id="2c678-173">The following example shows the handler for **InitiateFirmwareUpdate** method:</span></span>

```csharp
public async Task<MethodResponse> OnInitiateFirmwareUpdate(MethodRequest methodRequest, object userContext)
{
    if (_deviceManagementTask != null && !_deviceManagementTask.IsCompleted)
    {
        return await Task.FromResult(BuildMethodRespose(new
        {
            Message = "Device is busy"
        }, 409));
    }

    try
    {
        var operation = new FirmwareUpdate(methodRequest);
        _deviceManagementTask = operation.Run(Transport).ContinueWith(async task =>
        {
            // after firmware completed, we reset telemetry
            var telemetry = _telemetryController as ITelemetryWithTemperatureMeanValue;
            if (telemetry != null)
            {
                telemetry.TemperatureMeanValue = 34.5;
            }

            await UpdateReportedTemperatureMeanValue();
        });

        return await Task.FromResult(BuildMethodRespose(new
        {
            Message = "FirmwareUpdate accepted",
            Uri = operation.Uri
        }));
    }
    catch (Exception ex)
    {
        return await Task.FromResult(BuildMethodRespose(new
        {
            Message = ex.Message
        }, 400));
    }
}
```

<span data-ttu-id="2c678-174">Nazwy metod obsługi musi rozpoczynać się od `On` następuje nazwa metody.</span><span class="sxs-lookup"><span data-stu-id="2c678-174">Method handler names must start with `On` followed by the name of the method.</span></span> <span data-ttu-id="2c678-175">**MethodRequest** parametr zawiera parametry przekazywane wywołania metody z zaplecza rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="2c678-175">The **methodRequest** parameter contains any parameters passed with the method invocation from the solution back end.</span></span> <span data-ttu-id="2c678-176">Zwracana wartość musi być typu **zadań&lt;MethodResponse&gt;**.</span><span class="sxs-lookup"><span data-stu-id="2c678-176">The return value must be of type **Task&lt;MethodResponse&gt;**.</span></span> <span data-ttu-id="2c678-177">**BuildMethodResponse** narzędzie metody pomaga utworzyć wartość zwracaną.</span><span class="sxs-lookup"><span data-stu-id="2c678-177">The **BuildMethodResponse** utility method helps you create the return value.</span></span>

<span data-ttu-id="2c678-178">Wewnątrz metody obsługi możesz:</span><span class="sxs-lookup"><span data-stu-id="2c678-178">Inside the method handler, you could:</span></span>

- <span data-ttu-id="2c678-179">Uruchom zadanie asynchroniczne.</span><span class="sxs-lookup"><span data-stu-id="2c678-179">Start an asynchronous task.</span></span>
- <span data-ttu-id="2c678-180">Pobrać żądanej właściwości z *dwie urządzenia* w Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="2c678-180">Retrieve desired properties from the *device twin* in IoT Hub.</span></span>
- <span data-ttu-id="2c678-181">Aktualizuj przy użyciu jednej właściwości zgłoszone **SetReportedPropertyAsync** metody w **CoolerDevice** klasy.</span><span class="sxs-lookup"><span data-stu-id="2c678-181">Update a single reported property using the **SetReportedPropertyAsync** method in the **CoolerDevice** class.</span></span>
- <span data-ttu-id="2c678-182">Zaktualizować wiele właściwości zgłoszonego przez utworzenie **TwinCollection** wystąpienia i wywoływania **Transport.UpdateReportedPropertiesAsync** metody.</span><span class="sxs-lookup"><span data-stu-id="2c678-182">Update multiple reported properties by creating a **TwinCollection** instance and calling the **Transport.UpdateReportedPropertiesAsync** method.</span></span>

<span data-ttu-id="2c678-183">W poprzednim przykładzie aktualizacji oprogramowania układowego wykonuje następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="2c678-183">The preceding firmware update example performs the following steps:</span></span>

- <span data-ttu-id="2c678-184">Sprawdza, czy urządzenie jest w stanie zaakceptować żądania aktualizacji oprogramowania układowego.</span><span class="sxs-lookup"><span data-stu-id="2c678-184">Checks the device is able to accept the firmware update request.</span></span>
- <span data-ttu-id="2c678-185">Asynchronicznie inicjuje operację aktualizacji oprogramowania układowego i przywraca dane telemetryczne po zakończeniu operacji.</span><span class="sxs-lookup"><span data-stu-id="2c678-185">Asynchronously initiates the firmware update operation and resets the telemetry when the operation is complete.</span></span>
- <span data-ttu-id="2c678-186">Natychmiast zwraca komunikat "FirmwareUpdate zaakceptowane", aby wskazać, że żądanie zostało zaakceptowane przez urządzenie.</span><span class="sxs-lookup"><span data-stu-id="2c678-186">Immediately returns the "FirmwareUpdate accepted" message to indicate the request was accepted by the device.</span></span>

### <a name="build-and-use-your-own-physical-device"></a><span data-ttu-id="2c678-187">Tworzenie i używanie własnego urządzenia (fizycznych)</span><span class="sxs-lookup"><span data-stu-id="2c678-187">Build and use your own (physical) device</span></span>

<span data-ttu-id="2c678-188">[Azure IoT SDK](https://github.com/Azure/azure-iot-sdks) Podaj bibliotek podłączania wiele typów urządzeń (języków i systemów operacyjnych) do rozwiązania IoT.</span><span class="sxs-lookup"><span data-stu-id="2c678-188">The [Azure IoT SDKs](https://github.com/Azure/azure-iot-sdks) provide libraries for connecting numerous device types (languages and operating systems) into IoT solutions.</span></span>

## <a name="modify-dashboard-limits"></a><span data-ttu-id="2c678-189">Modyfikowanie limity pulpitu nawigacyjnego</span><span class="sxs-lookup"><span data-stu-id="2c678-189">Modify dashboard limits</span></span>

### <a name="number-of-devices-displayed-in-dashboard-dropdown"></a><span data-ttu-id="2c678-190">Liczba urządzeń wyświetlane na liście rozwijanej pulpitu nawigacyjnego</span><span class="sxs-lookup"><span data-stu-id="2c678-190">Number of devices displayed in dashboard dropdown</span></span>

<span data-ttu-id="2c678-191">Wartość domyślna to 200.</span><span class="sxs-lookup"><span data-stu-id="2c678-191">The default is 200.</span></span> <span data-ttu-id="2c678-192">Można zmienić tego numeru w [DashboardController.cs][lnk-dashboard-controller].</span><span class="sxs-lookup"><span data-stu-id="2c678-192">You can change this number in [DashboardController.cs][lnk-dashboard-controller].</span></span>

### <a name="number-of-pins-to-display-in-bing-map-control"></a><span data-ttu-id="2c678-193">Numer PIN do wyświetlenia w formancie mapy Bing</span><span class="sxs-lookup"><span data-stu-id="2c678-193">Number of pins to display in Bing Map control</span></span>

<span data-ttu-id="2c678-194">Wartość domyślna to 200.</span><span class="sxs-lookup"><span data-stu-id="2c678-194">The default is 200.</span></span> <span data-ttu-id="2c678-195">Można zmienić tego numeru w [TelemetryApiController.cs][lnk-telemetry-api-controller-01].</span><span class="sxs-lookup"><span data-stu-id="2c678-195">You can change this number in [TelemetryApiController.cs][lnk-telemetry-api-controller-01].</span></span>

### <a name="time-period-of-telemetry-graph"></a><span data-ttu-id="2c678-196">Okres czasu wykresu telemetrii</span><span class="sxs-lookup"><span data-stu-id="2c678-196">Time period of telemetry graph</span></span>

<span data-ttu-id="2c678-197">Wartość domyślna to 10 minut.</span><span class="sxs-lookup"><span data-stu-id="2c678-197">The default is 10 minutes.</span></span> <span data-ttu-id="2c678-198">Można zmienić tę wartość w [TelmetryApiController.cs][lnk-telemetry-api-controller-02].</span><span class="sxs-lookup"><span data-stu-id="2c678-198">You can change this value in [TelmetryApiController.cs][lnk-telemetry-api-controller-02].</span></span>

## <a name="manually-set-up-application-roles"></a><span data-ttu-id="2c678-199">Ręczne konfigurowanie ról aplikacji</span><span class="sxs-lookup"><span data-stu-id="2c678-199">Manually set up application roles</span></span>

<span data-ttu-id="2c678-200">W poniższej procedurze opisano sposób dodawania **Admin** i **tylko do odczytu** ról aplikacji do wstępnie skonfigurowanego rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="2c678-200">The following procedure describes how to add **Admin** and **ReadOnly** application roles to a preconfigured solution.</span></span> <span data-ttu-id="2c678-201">Należy zauważyć, że obejmuje wstępnie skonfigurowanych rozwiązań pobranego z witryny azureiotsuite.com już **Admin** i **tylko do odczytu** ról.</span><span class="sxs-lookup"><span data-stu-id="2c678-201">Note that preconfigured solutions provisioned from the azureiotsuite.com site already include the **Admin** and **ReadOnly** roles.</span></span>

<span data-ttu-id="2c678-202">Elementy członkowskie **tylko do odczytu** roli można wyświetlić pulpit nawigacyjny i listę urządzeń, ale nie mogą dodać urządzenia, zmiany atrybutów urządzenia lub wysyłać polecenia.</span><span class="sxs-lookup"><span data-stu-id="2c678-202">Members of the **ReadOnly** role can see the dashboard and the device list, but are not allowed to add devices, change device attributes, or send commands.</span></span>  <span data-ttu-id="2c678-203">Elementy członkowskie **Admin** rola ma pełny dostęp do wszystkich funkcji w rozwiązaniu.</span><span class="sxs-lookup"><span data-stu-id="2c678-203">Members of the **Admin** role have full access to all the functionality in the solution.</span></span>

1. <span data-ttu-id="2c678-204">Przejdź do [klasycznego portalu Azure][lnk-classic-portal].</span><span class="sxs-lookup"><span data-stu-id="2c678-204">Go to the [Azure classic portal][lnk-classic-portal].</span></span>
2. <span data-ttu-id="2c678-205">Wybierz **usługi Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="2c678-205">Select **Active Directory**.</span></span>
3. <span data-ttu-id="2c678-206">Kliknij nazwę dzierżawę usługi AAD, używane podczas przydzielania rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="2c678-206">Click the name of the AAD tenant you used when you provisioned your solution.</span></span>
4. <span data-ttu-id="2c678-207">Kliknij przycisk **aplikacji**.</span><span class="sxs-lookup"><span data-stu-id="2c678-207">Click **Applications**.</span></span>
5. <span data-ttu-id="2c678-208">Kliknij nazwę aplikacji, która jest zgodna z nazwą wstępnie skonfigurowane rozwiązanie.</span><span class="sxs-lookup"><span data-stu-id="2c678-208">Click the name of the application that matches your preconfigured solution name.</span></span> <span data-ttu-id="2c678-209">Jeśli nie widzisz aplikacji na liście, wybierz **aplikacji Moja firma jest właścicielem** w **Pokaż** listy rozwijanej i kliknij znacznik wyboru.</span><span class="sxs-lookup"><span data-stu-id="2c678-209">If you don't see your application in the list, select **Applications my company owns** in the **Show** dropdown and click the check mark.</span></span>
6. <span data-ttu-id="2c678-210">W dolnej części strony kliknij **Zarządzanie manifestu** , a następnie **Pobierz Manifest**.</span><span class="sxs-lookup"><span data-stu-id="2c678-210">At the bottom of the page, click **Manage Manifest** and then **Download Manifest**.</span></span>
7. <span data-ttu-id="2c678-211">Tej procedury pobiera plik JSON na komputerze lokalnym.</span><span class="sxs-lookup"><span data-stu-id="2c678-211">This procedure downloads a .json file to your local machine.</span></span> <span data-ttu-id="2c678-212">Otwórz ten plik do edycji w wybranym edytorze tekstów.</span><span class="sxs-lookup"><span data-stu-id="2c678-212">Open this file for editing in a text editor of your choice.</span></span>
8. <span data-ttu-id="2c678-213">Na trzeci wiersz pliku JSON można wyświetlić:</span><span class="sxs-lookup"><span data-stu-id="2c678-213">On the third line of the .json file, you can see:</span></span>

   ```json
   "appRoles" : [],
   ```
   <span data-ttu-id="2c678-214">Zastąp ten wiersz z następującym kodem:</span><span class="sxs-lookup"><span data-stu-id="2c678-214">Replace this line with the following code:</span></span>

   ```json
   "appRoles": [
   {
   "allowedMemberTypes": [
   "User"
   ],
   "description": "Administrator access to the application",
   "displayName": "Admin",
   "id": "a400a00b-f67c-42b7-ba9a-f73d8c67e433",
   "isEnabled": true,
   "value": "Admin"
   },
   {
   "allowedMemberTypes": [
   "User"
   ],
   "description": "Read only access to device information",
   "displayName": "Read Only",
   "id": "e5bbd0f5-128e-4362-9dd1-8f253c6082d7",
   "isEnabled": true,
   "value": "ReadOnly"
   } ],
   ```

9. <span data-ttu-id="2c678-215">Zapisz plik JSON zaktualizowane (można zastąpić istniejącego pliku).</span><span class="sxs-lookup"><span data-stu-id="2c678-215">Save the updated .json file (you can overwrite the existing file).</span></span>
10. <span data-ttu-id="2c678-216">W klasycznym portalu Azure, w dolnej części strony, wybierz **Zarządzanie manifestu** następnie **przekazać manifestu** można przekazać pliku JSON zapisane w poprzednim kroku.</span><span class="sxs-lookup"><span data-stu-id="2c678-216">In the Azure classic portal, at the bottom of the page, select **Manage Manifest** then **Upload Manifest** to upload the .json file you saved in the previous step.</span></span>
11. <span data-ttu-id="2c678-217">Zostały dodane **Admin** i **tylko do odczytu** role w aplikacji.</span><span class="sxs-lookup"><span data-stu-id="2c678-217">You have now added the **Admin** and **ReadOnly** roles to your application.</span></span>
12. <span data-ttu-id="2c678-218">Aby przypisać jedną z tych ról użytkownika w katalogu, zobacz [uprawnienia w witrynie azureiotsuite.com][lnk-permissions].</span><span class="sxs-lookup"><span data-stu-id="2c678-218">To assign one of these roles to a user in your directory, see [Permissions on the azureiotsuite.com site][lnk-permissions].</span></span>

## <a name="feedback"></a><span data-ttu-id="2c678-219">Opinia</span><span class="sxs-lookup"><span data-stu-id="2c678-219">Feedback</span></span>

<span data-ttu-id="2c678-220">Masz dostosowanie chcesz wyświetlić w tym dokumencie?</span><span class="sxs-lookup"><span data-stu-id="2c678-220">Do you have a customization you'd like to see covered in this document?</span></span> <span data-ttu-id="2c678-221">Dodaj sugestii funkcji [User Voice](https://feedback.azure.com/forums/321918-azure-iot), lub komentarz w tym artykule.</span><span class="sxs-lookup"><span data-stu-id="2c678-221">Add feature suggestions to [User Voice](https://feedback.azure.com/forums/321918-azure-iot), or comment on this article.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="2c678-222">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="2c678-222">Next steps</span></span>

<span data-ttu-id="2c678-223">Aby dowiedzieć się więcej na temat opcji dostosowywania wstępnie skonfigurowanych rozwiązań, zobacz:</span><span class="sxs-lookup"><span data-stu-id="2c678-223">To learn more about the options for customizing the preconfigured solutions, see:</span></span>

* <span data-ttu-id="2c678-224">[Łączenie aplikacji logiki do rozwiązania Azure IoT pakiet monitorowania zdalnego wstępnie][lnk-logicapp]</span><span class="sxs-lookup"><span data-stu-id="2c678-224">[Connect Logic App to your Azure IoT Suite Remote Monitoring preconfigured solution][lnk-logicapp]</span></span>
* <span data-ttu-id="2c678-225">[Dynamiczne telemetrii za pomocą zdalnego wstępnie skonfigurowane rozwiązanie monitorowania][lnk-dynamic]</span><span class="sxs-lookup"><span data-stu-id="2c678-225">[Use dynamic telemetry with the remote monitoring preconfigured solution][lnk-dynamic]</span></span>
* <span data-ttu-id="2c678-226">[Urządzenie informacji metadanych w zdalnym wstępnie skonfigurowane rozwiązanie monitorowania][lnk-devinfo]</span><span class="sxs-lookup"><span data-stu-id="2c678-226">[Device information metadata in the remote monitoring preconfigured solution][lnk-devinfo]</span></span>
* <span data-ttu-id="2c678-227">[Dostosuj sposób rozwiązania połączonych fabryki wyświetlania danych z serwerów OPC UA][lnk-cf-customize]</span><span class="sxs-lookup"><span data-stu-id="2c678-227">[Customize how the connected factory solution displays data from your OPC UA servers][lnk-cf-customize]</span></span>

[lnk-logicapp]: iot-suite-logic-apps-tutorial.md
[lnk-dynamic]: iot-suite-dynamic-telemetry.md
[lnk-devinfo]: iot-suite-remote-monitoring-device-info.md

[IoT Device SDK]: https://azure.microsoft.com/documentation/articles/iot-hub-sdks-summary/
[lnk-permissions]: iot-suite-permissions.md
[lnk-dashboard-controller]: https://github.com/Azure/azure-iot-remote-monitoring/blob/3fd43b8a9f7e0f2774d73f3569439063705cebe4/DeviceAdministration/Web/Controllers/DashboardController.cs#L27
[lnk-telemetry-api-controller-01]: https://github.com/Azure/azure-iot-remote-monitoring/blob/3fd43b8a9f7e0f2774d73f3569439063705cebe4/DeviceAdministration/Web/WebApiControllers/TelemetryApiController.cs#L27
[lnk-telemetry-api-controller-02]: https://github.com/Azure/azure-iot-remote-monitoring/blob/e7003339f73e21d3930f71ceba1e74fb5c0d9ea0/DeviceAdministration/Web/WebApiControllers/TelemetryApiController.cs#L25 
[lnk-sample-device-factory]: https://github.com/Azure/azure-iot-remote-monitoring/blob/master/Common/Factory/SampleDeviceFactory.cs#L40
[lnk-classic-portal]: https://manage.windowsazure.com
[lnk-direct-methods]: ../iot-hub/iot-hub-devguide-direct-methods.md
[lnk-cf-customize]: iot-suite-connected-factory-customize.md