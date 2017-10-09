---
title: "aaaCustomizing wstępnie rozwiązania | Dokumentacja firmy Microsoft"
description: "Zawiera wskazówki dotyczące sposobu hello toocustomize pakiet IoT Azure wstępnie rozwiązania."
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
ms.openlocfilehash: 1a8573f5ac6ed944c44459df495446f15174d513
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="customize-a-preconfigured-solution"></a><span data-ttu-id="18980-103">Dostosowanie wstępnie skonfigurowanego rozwiązania</span><span class="sxs-lookup"><span data-stu-id="18980-103">Customize a preconfigured solution</span></span>

<span data-ttu-id="18980-104">rozwiązań Hello wstępnie dostarczonych z hello pakiet IoT Azure przedstawienie usług hello w hello zestawu roboczego razem toodeliver rozwiązania end-to-end.</span><span class="sxs-lookup"><span data-stu-id="18980-104">hello preconfigured solutions provided with hello Azure IoT Suite demonstrate hello services within hello suite working together toodeliver an end-to-end solution.</span></span> <span data-ttu-id="18980-105">Z tego punktu początkowego istnieją różnych miejscach, w których można rozszerzać i dostosować hello w określonych scenariuszach.</span><span class="sxs-lookup"><span data-stu-id="18980-105">From this starting point, there are various places in which you can extend and customize hello solution for specific scenarios.</span></span> <span data-ttu-id="18980-106">Witaj następujące sekcje opisują tych wspólnych punktów dostosowywania.</span><span class="sxs-lookup"><span data-stu-id="18980-106">hello following sections describe these common customization points.</span></span>

## <a name="find-hello-source-code"></a><span data-ttu-id="18980-107">Znajdź hello kodu źródłowego</span><span class="sxs-lookup"><span data-stu-id="18980-107">Find hello source code</span></span>

<span data-ttu-id="18980-108">Hello kodu źródłowego rozwiązania hello wstępnie jest dostępna w witrynie GitHub w powitania po repozytoria:</span><span class="sxs-lookup"><span data-stu-id="18980-108">hello source code for hello preconfigured solutions is available on GitHub in hello following repositories:</span></span>

* <span data-ttu-id="18980-109">Monitorowanie zdalne: [https://www.github.com/Azure/azure-iot-remote-monitoring](https://github.com/Azure/azure-iot-remote-monitoring)</span><span class="sxs-lookup"><span data-stu-id="18980-109">Remote Monitoring: [https://www.github.com/Azure/azure-iot-remote-monitoring](https://github.com/Azure/azure-iot-remote-monitoring)</span></span>
* <span data-ttu-id="18980-110">Konserwacji predykcyjnej: [https://github.com/Azure/azure-iot-predictive-maintenance](https://github.com/Azure/azure-iot-predictive-maintenance)</span><span class="sxs-lookup"><span data-stu-id="18980-110">Predictive Maintenance: [https://github.com/Azure/azure-iot-predictive-maintenance](https://github.com/Azure/azure-iot-predictive-maintenance)</span></span>
* <span data-ttu-id="18980-111">Fabryka połączenia: [https://github.com/Azure/azure-iot-connected-factory](https://github.com/Azure/azure-iot-connected-factory)</span><span class="sxs-lookup"><span data-stu-id="18980-111">Connected factory: [https://github.com/Azure/azure-iot-connected-factory](https://github.com/Azure/azure-iot-connected-factory)</span></span>

<span data-ttu-id="18980-112">Kod źródłowy Hello hello wstępnie rozwiązań jest udostępniane toodemonstrate hello wzorców i rozwiązań używane funkcje end-to-end hello tooimplement rozwiązania IoT przy użyciu pakietu IoT Azure.</span><span class="sxs-lookup"><span data-stu-id="18980-112">hello source code for hello preconfigured solutions is provided toodemonstrate hello patterns and practices used tooimplement hello end-to-end functionality of an IoT solution using Azure IoT Suite.</span></span> <span data-ttu-id="18980-113">Można znaleźć więcej informacji na temat toobuild i wdrażanie rozwiązań hello w hello repozytoriów GitHub.</span><span class="sxs-lookup"><span data-stu-id="18980-113">You can find more information about how toobuild and deploy hello solutions in hello GitHub repositories.</span></span>

## <a name="change-hello-preconfigured-rules"></a><span data-ttu-id="18980-114">Zmień reguły hello wstępnie</span><span class="sxs-lookup"><span data-stu-id="18980-114">Change hello preconfigured rules</span></span>

<span data-ttu-id="18980-115">Witaj rozwiązanie monitorowania zdalnego obejmuje trzy [Azure Stream Analytics](https://azure.microsoft.com/services/stream-analytics/) zadania toohandle informacje o urządzeniu, telemetrii i logiki reguły w rozwiązaniu hello.</span><span class="sxs-lookup"><span data-stu-id="18980-115">hello remote monitoring solution includes three [Azure Stream Analytics](https://azure.microsoft.com/services/stream-analytics/) jobs toohandle device information, telemetry, and rules logic in hello solution.</span></span>

<span data-ttu-id="18980-116">Witaj trzy strumienia zadania usługi analiza i ich składni opisano szczegółowo w hello [monitorowania zdalnego wstępnie skonfigurowane rozwiązanie wskazówki](iot-suite-remote-monitoring-sample-walkthrough.md).</span><span class="sxs-lookup"><span data-stu-id="18980-116">hello three stream analytics jobs and their syntax are described in depth in hello [Remote monitoring preconfigured solution walkthrough](iot-suite-remote-monitoring-sample-walkthrough.md).</span></span> 

<span data-ttu-id="18980-117">Te zadania można edytować bezpośrednio tooalter hello logiki lub Dodawanie logiki tooyour określonego scenariusza.</span><span class="sxs-lookup"><span data-stu-id="18980-117">You can edit these jobs directly tooalter hello logic, or add logic specific tooyour scenario.</span></span> <span data-ttu-id="18980-118">Można znaleźć hello zadania usługi analiza strumienia w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="18980-118">You can find hello Stream Analytics jobs as follows:</span></span>

1. <span data-ttu-id="18980-119">Przejdź za[portalu Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="18980-119">Go too[Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="18980-120">Przejdź toohello grupy zasobów z hello sama nazwa jak rozwiązania IoT.</span><span class="sxs-lookup"><span data-stu-id="18980-120">Navigate toohello resource group with hello same name as your IoT solution.</span></span> 
3. <span data-ttu-id="18980-121">Wybierz zadanie usługi analiza strumienia Azure hello chcesz toomodify.</span><span class="sxs-lookup"><span data-stu-id="18980-121">Select hello Azure Stream Analytics job you'd like toomodify.</span></span> 
4. <span data-ttu-id="18980-122">Zadanie zatrzymania hello wybierając **zatrzymać** hello zestawu poleceń.</span><span class="sxs-lookup"><span data-stu-id="18980-122">Stop hello job by selecting **Stop** in hello set of commands.</span></span> 
5. <span data-ttu-id="18980-123">Edytowanie danych wejściowych hello, zapytań i danych wyjściowych.</span><span class="sxs-lookup"><span data-stu-id="18980-123">Edit hello inputs, query, and outputs.</span></span>
   
    <span data-ttu-id="18980-124">Zapytanie hello toochange dla hello jest prostą modyfikację **reguły** toouse zadania **"<"** zamiast **">"**.</span><span class="sxs-lookup"><span data-stu-id="18980-124">A simple modification is toochange hello query for hello **Rules** job toouse a **"<"** instead of a **">"**.</span></span> <span data-ttu-id="18980-125">portal rozwiązania Hello pozostanie **">"** podczas edycji reguły, ale Zwróć uwagę, jak zachowanie hello jest odwrócony powodu toohello zmianę hello bazowy zadania.</span><span class="sxs-lookup"><span data-stu-id="18980-125">hello solution portal still shows **">"** when you edit a rule, but notice how hello behavior is flipped due toohello change in hello underlying job.</span></span>
6. <span data-ttu-id="18980-126">Uruchom zadanie hello</span><span class="sxs-lookup"><span data-stu-id="18980-126">Start hello job</span></span>

> [!NOTE]
> <span data-ttu-id="18980-127">pulpit nawigacyjny monitorowania zdalnego Hello zależy od określonych danych, zmienianie hello zadania może spowodować hello toofail pulpitu nawigacyjnego.</span><span class="sxs-lookup"><span data-stu-id="18980-127">hello remote monitoring dashboard depends on specific data, so altering hello jobs can cause hello dashboard toofail.</span></span>

## <a name="add-your-own-rules"></a><span data-ttu-id="18980-128">Dodaj własne reguły</span><span class="sxs-lookup"><span data-stu-id="18980-128">Add your own rules</span></span>

<span data-ttu-id="18980-129">Ponadto toochanging hello wstępnie zadania usługi analiza strumienia Azure, możesz użyć hello Azure tooadd portalu nowe zadania lub Dodaj nowe zadania tooexisting zapytania.</span><span class="sxs-lookup"><span data-stu-id="18980-129">In addition toochanging hello preconfigured Azure Stream Analytics jobs, you can use hello Azure portal tooadd new jobs or add new queries tooexisting jobs.</span></span>

## <a name="customize-devices"></a><span data-ttu-id="18980-130">Dostosowywanie urządzeń</span><span class="sxs-lookup"><span data-stu-id="18980-130">Customize devices</span></span>

<span data-ttu-id="18980-131">Jedną z najbardziej typowych działań rozszerzenia hello współpracuje ze scenariuszem tooyour określonych urządzeń.</span><span class="sxs-lookup"><span data-stu-id="18980-131">One of hello most common extension activities is working with devices specific tooyour scenario.</span></span> <span data-ttu-id="18980-132">Istnieje kilka metod do pracy z urządzeń.</span><span class="sxs-lookup"><span data-stu-id="18980-132">There are several methods for working with devices.</span></span> <span data-ttu-id="18980-133">Te metody obejmują zmiany toomatch symulowane urządzenie danego scenariusza lub przy użyciu hello [SDK urządzenia IoT] [ IoT Device SDK] tooconnect rozwiązania toohello urządzenia fizycznego.</span><span class="sxs-lookup"><span data-stu-id="18980-133">These methods include altering a simulated device toomatch your scenario, or using hello [IoT Device SDK][IoT Device SDK] tooconnect your physical device toohello solution.</span></span>

<span data-ttu-id="18980-134">Urządzeń tooadding przewodnik krok po kroku, zobacz hello [urządzenia łączenie pakiet Iot](iot-suite-connecting-devices.md) artykułu i hello [zdalnego monitorowania przykład zestawu SDK C](https://github.com/Azure/azure-iot-sdk-c/tree/master/serializer/samples/remote_monitoring).</span><span class="sxs-lookup"><span data-stu-id="18980-134">For a step-by-step guide tooadding devices, see hello [Iot Suite Connecting Devices](iot-suite-connecting-devices.md) article and hello [remote monitoring C SDK Sample](https://github.com/Azure/azure-iot-sdk-c/tree/master/serializer/samples/remote_monitoring).</span></span> <span data-ttu-id="18980-135">Ten przykład jest zaprojektowana toowork z hello zdalne monitorowanie wstępnie skonfigurowane rozwiązanie.</span><span class="sxs-lookup"><span data-stu-id="18980-135">This sample is designed toowork with hello remote monitoring preconfigured solution.</span></span>

### <a name="create-your-own-simulated-device"></a><span data-ttu-id="18980-136">Utworzyć symulowane urządzenie</span><span class="sxs-lookup"><span data-stu-id="18980-136">Create your own simulated device</span></span>

<span data-ttu-id="18980-137">Uwzględnione w hello [zdalnej kontroli kodu źródłowego rozwiązania](https://github.com/Azure/azure-iot-remote-monitoring), jest symulatora .NET.</span><span class="sxs-lookup"><span data-stu-id="18980-137">Included in hello [remote monitoring solution source code](https://github.com/Azure/azure-iot-remote-monitoring), is a .NET simulator.</span></span> <span data-ttu-id="18980-138">Ta symulator jest hello jedną udostępnione jako część rozwiązania hello i można zmienienia go toosend innych metadanych, telemetrii i odpowiedzi polecenia toodifferent i metod.</span><span class="sxs-lookup"><span data-stu-id="18980-138">This simulator is hello one provisioned as part of hello solution and you can alter it toosend different metadata, telemetry, and respond toodifferent commands and methods.</span></span>

<span data-ttu-id="18980-139">Hello symulatora wstępnie skonfigurowane w hello zdalnego wstępnie skonfigurowane rozwiązanie monitorujące symuluje lodówki urządzenia, który emituje temperatury i wilgotności telemetrii.</span><span class="sxs-lookup"><span data-stu-id="18980-139">hello preconfigured simulator in hello remote monitoring preconfigured solution simulates a cooler device that emits temperature and humidity telemetry.</span></span> <span data-ttu-id="18980-140">Można zmodyfikować symulatora hello w hello [Simulator.WebJob](https://github.com/Azure/azure-iot-remote-monitoring/tree/master/Simulator/Simulator.WebJob) projektu, gdy zostały rozwidlone hello repozytorium GitHub.</span><span class="sxs-lookup"><span data-stu-id="18980-140">You can modify hello simulator in hello [Simulator.WebJob](https://github.com/Azure/azure-iot-remote-monitoring/tree/master/Simulator/Simulator.WebJob) project when you've forked hello GitHub repository.</span></span>

### <a name="available-locations-for-simulated-devices"></a><span data-ttu-id="18980-141">Dostępne lokalizacje symulowanego urządzenia</span><span class="sxs-lookup"><span data-stu-id="18980-141">Available locations for simulated devices</span></span>

<span data-ttu-id="18980-142">jest Hello domyślnego zestawu z lokalizacji w Seattle/Redmond, Washington, USA.</span><span class="sxs-lookup"><span data-stu-id="18980-142">hello default set of locations is in Seattle/Redmond, Washington, United States of America.</span></span> <span data-ttu-id="18980-143">Możesz zmienić te lokalizacje w [SampleDeviceFactory.cs][lnk-sample-device-factory].</span><span class="sxs-lookup"><span data-stu-id="18980-143">You can change these locations in [SampleDeviceFactory.cs][lnk-sample-device-factory].</span></span>

### <a name="add-a-desired-property-update-handler-toohello-simulator"></a><span data-ttu-id="18980-144">Dodaj żądaną właściwość symulatora toohello program obsługi aktualizacji</span><span class="sxs-lookup"><span data-stu-id="18980-144">Add a desired property update handler toohello simulator</span></span>

<span data-ttu-id="18980-145">W portalu rozwiązania hello można ustawić wartość dla żądanej właściwości urządzenia.</span><span class="sxs-lookup"><span data-stu-id="18980-145">You can set a value for a desired property for a device in hello solution portal.</span></span> <span data-ttu-id="18980-146">Kiedy urządzenie hello pobiera wartość właściwości hello potrzebne jest odpowiedzialny za hello żądania zmiany właściwości toohandle hello hello urządzenia.</span><span class="sxs-lookup"><span data-stu-id="18980-146">It is hello responsibility of hello device toohandle hello property change request when hello device retrieves hello desired property value.</span></span> <span data-ttu-id="18980-147">Obsługa tooadd zmiany wartości właściwości za pośrednictwem żądanej właściwości, należy tooadd symulatora toohello obsługi.</span><span class="sxs-lookup"><span data-stu-id="18980-147">tooadd support for a property value change through a desired property, you need tooadd a handler toohello simulator.</span></span>

<span data-ttu-id="18980-148">Symulator Hello zawiera obsługę hello **SetPointTemp** i **TelemetryInterval** aktualizowanych przez ustawienie właściwości żądane wartości w hello rozwiązanie portalu.</span><span class="sxs-lookup"><span data-stu-id="18980-148">hello simulator contains handlers for hello **SetPointTemp** and **TelemetryInterval** properties that you can update by setting desired values in hello solution portal.</span></span>

<span data-ttu-id="18980-149">Witaj poniższy przykład przedstawia hello obsługę hello **SetPointTemp** wymaganą właściwość w hello **CoolerDevice** klasy:</span><span class="sxs-lookup"><span data-stu-id="18980-149">hello following example shows hello handler for hello **SetPointTemp** desired property in hello **CoolerDevice** class:</span></span>

```csharp
protected async Task OnSetPointTempUpdate(object value)
{
    var telemetry = _telemetryController as ITelemetryWithSetPointTemperature;
    telemetry.SetPointTemperature = Convert.ToDouble(value);

    await SetReportedPropertyAsync(SetPointTempPropertyName, telemetry.SetPointTemperature);
}
```

<span data-ttu-id="18980-150">Ta metoda aktualizacji hello telemetrii punktu temperatury, a następnie hello raporty zmienić tooIoT zapasowego Centrum poprzez ustawienie właściwości zgłoszony.</span><span class="sxs-lookup"><span data-stu-id="18980-150">This method updates hello telemetry point temperature and then reports hello change back tooIoT Hub by setting a reported property.</span></span>

<span data-ttu-id="18980-151">Możesz dodać własne programy obsługi dla własnych właściwości przez następujący wzór hello w hello poprzedzających przykład.</span><span class="sxs-lookup"><span data-stu-id="18980-151">You can add your own handlers for your own properties by following hello pattern in hello preceding example.</span></span>

<span data-ttu-id="18980-152">Należy także powiązać hello żądanej właściwości toohello obsługi pokazane na powitania poniższy przykład z hello **CoolerDevice** konstruktora:</span><span class="sxs-lookup"><span data-stu-id="18980-152">You must also bind hello desired property toohello handler as shown in hello following example from hello **CoolerDevice** constructor:</span></span>

```csharp
_desiredPropertyUpdateHandlers.Add(SetPointTempPropertyName, OnSetPointTempUpdate);
```

<span data-ttu-id="18980-153">Należy pamiętać, że **SetPointTempPropertyName** jest stałą zdefiniowany jako "Config.SetPointTemp".</span><span class="sxs-lookup"><span data-stu-id="18980-153">Note that **SetPointTempPropertyName** is a constant defined as "Config.SetPointTemp".</span></span>

### <a name="add-support-for-a-new-method-toohello-simulator"></a><span data-ttu-id="18980-154">Dodaj obsługę nowych symulatora toohello — metoda</span><span class="sxs-lookup"><span data-stu-id="18980-154">Add support for a new method toohello simulator</span></span>

<span data-ttu-id="18980-155">Można dostosować hello symulatora tooadd obsługę nowego [— metoda (metoda bezpośrednia)][lnk-direct-methods].</span><span class="sxs-lookup"><span data-stu-id="18980-155">You can customize hello simulator tooadd support for a new [method (direct method)][lnk-direct-methods].</span></span> <span data-ttu-id="18980-156">Istnieją dwa kluczowe kroki wymagane:</span><span class="sxs-lookup"><span data-stu-id="18980-156">There are two key steps required:</span></span>

- <span data-ttu-id="18980-157">Symulator Hello należy powiadomić hello Centrum IoT w rozwiązaniu hello wstępnie szczegóły hello metody.</span><span class="sxs-lookup"><span data-stu-id="18980-157">hello simulator must notify hello IoT hub in hello preconfigured solution with details of hello method.</span></span>
- <span data-ttu-id="18980-158">Symulator Hello musi zawierać wywołanie metody hello toohandle kod wywoływany z hello **szczegóły urządzenia** panelu w Eksploratorze rozwiązań hello lub za pomocą zadania.</span><span class="sxs-lookup"><span data-stu-id="18980-158">hello simulator must include code toohandle hello method call when you invoke it from hello **Device details** panel in hello solution explorer or through a job.</span></span>

<span data-ttu-id="18980-159">Hello monitorowania zdalnego wstępnie skonfigurowane rozwiązanie używa *zgłosił właściwości* szczegóły toosend obsługiwane metody tooIoT koncentratora.</span><span class="sxs-lookup"><span data-stu-id="18980-159">hello remote monitoring preconfigured solution uses *reported properties* toosend details of supported methods tooIoT hub.</span></span> <span data-ttu-id="18980-160">zaplecza rozwiązania Hello przechowuje listę wszystkich metod hello obsługiwanych przez poszczególne urządzenia oraz Historia wywołań metod.</span><span class="sxs-lookup"><span data-stu-id="18980-160">hello solution back end maintains a list of all hello methods supported by each device along with a history of method invocations.</span></span> <span data-ttu-id="18980-161">Możesz wyświetlić te informacje o urządzeniach i wywołania metod w hello rozwiązanie portalu.</span><span class="sxs-lookup"><span data-stu-id="18980-161">You can view this information about devices and invoke methods in hello solution portal.</span></span>

<span data-ttu-id="18980-162">czy urządzenie obsługuje metodę Centrum IoT hello toonotify, hello urządzenia należy dodać szczegóły toohello metody hello **SupportedMethods** węzła w hello zgłoszonych właściwości:</span><span class="sxs-lookup"><span data-stu-id="18980-162">toonotify hello IoT hub that a device supports a method, hello device must add details of hello method toohello **SupportedMethods** node in hello reported properties:</span></span>

```json
"SupportedMethods": {
  "<method signature>": "<method description>",
  "<method signature>": "<method description>"
}
```

<span data-ttu-id="18980-163">Witaj podpis metody ma hello następującego formatu: `<method name>--<parameter #0 name>-<parameter #1 type>-...-<parameter #n name>-<parameter #n type>`.</span><span class="sxs-lookup"><span data-stu-id="18980-163">hello method signature has hello following format: `<method name>--<parameter #0 name>-<parameter #1 type>-...-<parameter #n name>-<parameter #n type>`.</span></span> <span data-ttu-id="18980-164">Na przykład toospecify hello **InitiateFirmwareUpdate** metoda oczekuje parametru ciągu o nazwie **FwPackageURI**, użyj powitania po podpis metody:</span><span class="sxs-lookup"><span data-stu-id="18980-164">For example, toospecify hello **InitiateFirmwareUpdate** method expects a string parameter named **FwPackageURI**, use hello following method signature:</span></span>

```json
InitiateFirmwareUpate--FwPackageURI-string: "description of method"
```

<span data-ttu-id="18980-165">Dla listy typów obsługiwanych parametrów, zobacz hello **CommandTypes** klasy w projekcie infrastruktury hello.</span><span class="sxs-lookup"><span data-stu-id="18980-165">For a list of supported parameter types, see hello **CommandTypes** class in hello Infrastructure project.</span></span>

<span data-ttu-id="18980-166">toodelete metody, ustawić podpis metody hello także`null` w hello zgłosił właściwości.</span><span class="sxs-lookup"><span data-stu-id="18980-166">toodelete a method, set hello method signature too`null` in hello reported properties.</span></span>

> [!NOTE]
> <span data-ttu-id="18980-167">Witaj zaplecza rozwiązania tylko aktualizuje informacje o obsługiwanych metod po odebraniu *informacje o urządzeniu* wiadomość hello urządzenia.</span><span class="sxs-lookup"><span data-stu-id="18980-167">hello solution back end only updates information about supported methods when it receives a *device information* message from hello device.</span></span>

<span data-ttu-id="18980-168">Witaj następujący przykładowy kod z hello **SampleDeviceFactory** klasy w hello typowe projektu pokazuje, jak tooadd listy toohello — metoda z **SupportedMethods** w hello zgłosił przesyłanych przez hello właściwości urządzenie:</span><span class="sxs-lookup"><span data-stu-id="18980-168">hello following code sample from hello **SampleDeviceFactory** class in hello Common project shows how tooadd a method toohello list of **SupportedMethods** in hello reported properties sent by hello device:</span></span>

```csharp
device.Commands.Add(new Command(
    "InitiateFirmwareUpdate",
    DeliveryType.Method,
    "Updates device Firmware. Use parameter 'FwPackageUri' toospecifiy hello URI of hello firmware file, e.g. https://iotrmassets.blob.core.windows.net/firmwares/FW20.bin",
    new[] { new Parameter("FwPackageUri", "string") }
));
```

<span data-ttu-id="18980-169">Następujący fragment kodu dodaje szczegóły hello **InitiateFirmwareUpdate** metody w tym toodisplay tekstu w portalu rozwiązania hello i szczegóły hello wymagane parametry metody.</span><span class="sxs-lookup"><span data-stu-id="18980-169">This code snippet adds details of hello **InitiateFirmwareUpdate** method including text toodisplay in hello solution portal and details of hello required method parameters.</span></span>

<span data-ttu-id="18980-170">Symulator Hello wysyła zgłoszone właściwości, w tym hello listę obsługiwanych metod tooIoT Centrum podczas uruchamiania symulatora hello.</span><span class="sxs-lookup"><span data-stu-id="18980-170">hello simulator sends reported properties, including hello list of supported methods, tooIoT Hub when hello simulator starts.</span></span>

<span data-ttu-id="18980-171">Dodaj kod obsługi toohello symulatora dla poszczególnych metod obsługiwanych.</span><span class="sxs-lookup"><span data-stu-id="18980-171">Add a handler toohello simulator code for each method it supports.</span></span> <span data-ttu-id="18980-172">Widać hello istniejących programów obsługi w hello **CoolerDevice** klasy w projekcie Simulator.WebJob hello.</span><span class="sxs-lookup"><span data-stu-id="18980-172">You can see hello existing handlers in hello **CoolerDevice** class in hello Simulator.WebJob project.</span></span> <span data-ttu-id="18980-173">Witaj poniższy przykład przedstawia hello obsługę **InitiateFirmwareUpdate** metody:</span><span class="sxs-lookup"><span data-stu-id="18980-173">hello following example shows hello handler for **InitiateFirmwareUpdate** method:</span></span>

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

<span data-ttu-id="18980-174">Nazwy metod obsługi musi rozpoczynać się od `On` następuje nazwa hello hello metody.</span><span class="sxs-lookup"><span data-stu-id="18980-174">Method handler names must start with `On` followed by hello name of hello method.</span></span> <span data-ttu-id="18980-175">Witaj **methodRequest** parametr zawiera parametry przekazywane z zaplecza rozwiązania hello hello wywołania metody.</span><span class="sxs-lookup"><span data-stu-id="18980-175">hello **methodRequest** parameter contains any parameters passed with hello method invocation from hello solution back end.</span></span> <span data-ttu-id="18980-176">Witaj zwracana wartość musi być typu **zadań&lt;MethodResponse&gt;**.</span><span class="sxs-lookup"><span data-stu-id="18980-176">hello return value must be of type **Task&lt;MethodResponse&gt;**.</span></span> <span data-ttu-id="18980-177">Witaj **BuildMethodResponse** narzędzie metody pomaga utworzyć hello zwracanej wartości.</span><span class="sxs-lookup"><span data-stu-id="18980-177">hello **BuildMethodResponse** utility method helps you create hello return value.</span></span>

<span data-ttu-id="18980-178">Wewnątrz hello metody obsługi możesz:</span><span class="sxs-lookup"><span data-stu-id="18980-178">Inside hello method handler, you could:</span></span>

- <span data-ttu-id="18980-179">Uruchom zadanie asynchroniczne.</span><span class="sxs-lookup"><span data-stu-id="18980-179">Start an asynchronous task.</span></span>
- <span data-ttu-id="18980-180">Pobrać żądanej właściwości z hello *dwie urządzenia* w Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="18980-180">Retrieve desired properties from hello *device twin* in IoT Hub.</span></span>
- <span data-ttu-id="18980-181">Zaktualizuj jednej właściwości zgłoszony przy użyciu hello **SetReportedPropertyAsync** metoda hello **CoolerDevice** klasy.</span><span class="sxs-lookup"><span data-stu-id="18980-181">Update a single reported property using hello **SetReportedPropertyAsync** method in hello **CoolerDevice** class.</span></span>
- <span data-ttu-id="18980-182">Zaktualizować wiele właściwości zgłoszonego przez utworzenie **TwinCollection** wystąpienia i wywoływania hello **Transport.UpdateReportedPropertiesAsync** metody.</span><span class="sxs-lookup"><span data-stu-id="18980-182">Update multiple reported properties by creating a **TwinCollection** instance and calling hello **Transport.UpdateReportedPropertiesAsync** method.</span></span>

<span data-ttu-id="18980-183">Witaj poprzednim przykładzie aktualizacji oprogramowania układowego wykonuje hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="18980-183">hello preceding firmware update example performs hello following steps:</span></span>

- <span data-ttu-id="18980-184">Urządzenie hello kontroli jest żądanie aktualizacji oprogramowania układowego hello tooaccept stanie.</span><span class="sxs-lookup"><span data-stu-id="18980-184">Checks hello device is able tooaccept hello firmware update request.</span></span>
- <span data-ttu-id="18980-185">Asynchronicznie inicjuje operacji aktualizacji oprogramowania układowego hello i resetuje hello telemetrii po zakończeniu operacji hello.</span><span class="sxs-lookup"><span data-stu-id="18980-185">Asynchronously initiates hello firmware update operation and resets hello telemetry when hello operation is complete.</span></span>
- <span data-ttu-id="18980-186">Natychmiast zwraca Witaj "FirmwareUpdate zaakceptowane" komunikat tooindicate hello żądanie zostało zaakceptowane przez urządzenie hello.</span><span class="sxs-lookup"><span data-stu-id="18980-186">Immediately returns hello "FirmwareUpdate accepted" message tooindicate hello request was accepted by hello device.</span></span>

### <a name="build-and-use-your-own-physical-device"></a><span data-ttu-id="18980-187">Tworzenie i używanie własnego urządzenia (fizycznych)</span><span class="sxs-lookup"><span data-stu-id="18980-187">Build and use your own (physical) device</span></span>

<span data-ttu-id="18980-188">Witaj [Azure IoT SDK](https://github.com/Azure/azure-iot-sdks) Podaj bibliotek podłączania wiele typów urządzeń (języków i systemów operacyjnych) do rozwiązania IoT.</span><span class="sxs-lookup"><span data-stu-id="18980-188">hello [Azure IoT SDKs](https://github.com/Azure/azure-iot-sdks) provide libraries for connecting numerous device types (languages and operating systems) into IoT solutions.</span></span>

## <a name="modify-dashboard-limits"></a><span data-ttu-id="18980-189">Modyfikowanie limity pulpitu nawigacyjnego</span><span class="sxs-lookup"><span data-stu-id="18980-189">Modify dashboard limits</span></span>

### <a name="number-of-devices-displayed-in-dashboard-dropdown"></a><span data-ttu-id="18980-190">Liczba urządzeń wyświetlane na liście rozwijanej pulpitu nawigacyjnego</span><span class="sxs-lookup"><span data-stu-id="18980-190">Number of devices displayed in dashboard dropdown</span></span>

<span data-ttu-id="18980-191">Witaj domyślna to 200.</span><span class="sxs-lookup"><span data-stu-id="18980-191">hello default is 200.</span></span> <span data-ttu-id="18980-192">Można zmienić tego numeru w [DashboardController.cs][lnk-dashboard-controller].</span><span class="sxs-lookup"><span data-stu-id="18980-192">You can change this number in [DashboardController.cs][lnk-dashboard-controller].</span></span>

### <a name="number-of-pins-toodisplay-in-bing-map-control"></a><span data-ttu-id="18980-193">Numer PIN toodisplay w formancie mapy Bing</span><span class="sxs-lookup"><span data-stu-id="18980-193">Number of pins toodisplay in Bing Map control</span></span>

<span data-ttu-id="18980-194">Witaj domyślna to 200.</span><span class="sxs-lookup"><span data-stu-id="18980-194">hello default is 200.</span></span> <span data-ttu-id="18980-195">Można zmienić tego numeru w [TelemetryApiController.cs][lnk-telemetry-api-controller-01].</span><span class="sxs-lookup"><span data-stu-id="18980-195">You can change this number in [TelemetryApiController.cs][lnk-telemetry-api-controller-01].</span></span>

### <a name="time-period-of-telemetry-graph"></a><span data-ttu-id="18980-196">Okres czasu wykresu telemetrii</span><span class="sxs-lookup"><span data-stu-id="18980-196">Time period of telemetry graph</span></span>

<span data-ttu-id="18980-197">Witaj domyślna to 10 minut.</span><span class="sxs-lookup"><span data-stu-id="18980-197">hello default is 10 minutes.</span></span> <span data-ttu-id="18980-198">Można zmienić tę wartość w [TelmetryApiController.cs][lnk-telemetry-api-controller-02].</span><span class="sxs-lookup"><span data-stu-id="18980-198">You can change this value in [TelmetryApiController.cs][lnk-telemetry-api-controller-02].</span></span>

## <a name="manually-set-up-application-roles"></a><span data-ttu-id="18980-199">Ręczne konfigurowanie ról aplikacji</span><span class="sxs-lookup"><span data-stu-id="18980-199">Manually set up application roles</span></span>

<span data-ttu-id="18980-200">Witaj Poniższa procedura opisuje sposób tooadd **Admin** i **tylko do odczytu** aplikacji ról tooa wstępnie skonfigurowane rozwiązanie.</span><span class="sxs-lookup"><span data-stu-id="18980-200">hello following procedure describes how tooadd **Admin** and **ReadOnly** application roles tooa preconfigured solution.</span></span> <span data-ttu-id="18980-201">Należy zauważyć, że wstępnie skonfigurowanych rozwiązań pobranego z witryny azureiotsuite.com hello już obejmuje hello **Admin** i **tylko do odczytu** ról.</span><span class="sxs-lookup"><span data-stu-id="18980-201">Note that preconfigured solutions provisioned from hello azureiotsuite.com site already include hello **Admin** and **ReadOnly** roles.</span></span>

<span data-ttu-id="18980-202">Elementy członkowskie hello **tylko do odczytu** roli można wyświetlić pulpit nawigacyjny hello i hello listę urządzeń, ale nie są dozwolone tooadd urządzenia, zmiany atrybutów urządzenia lub polecenia send.</span><span class="sxs-lookup"><span data-stu-id="18980-202">Members of hello **ReadOnly** role can see hello dashboard and hello device list, but are not allowed tooadd devices, change device attributes, or send commands.</span></span>  <span data-ttu-id="18980-203">Elementy członkowskie hello **Admin** rola ma pełny dostęp tooall hello funkcjonalność w rozwiązaniu hello.</span><span class="sxs-lookup"><span data-stu-id="18980-203">Members of hello **Admin** role have full access tooall hello functionality in hello solution.</span></span>

1. <span data-ttu-id="18980-204">Przejdź toohello [klasycznego portalu Azure][lnk-classic-portal].</span><span class="sxs-lookup"><span data-stu-id="18980-204">Go toohello [Azure classic portal][lnk-classic-portal].</span></span>
2. <span data-ttu-id="18980-205">Wybierz **usługi Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="18980-205">Select **Active Directory**.</span></span>
3. <span data-ttu-id="18980-206">Kliknij nazwę hello hello dzierżawę usługi AAD, używane podczas przydzielania rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="18980-206">Click hello name of hello AAD tenant you used when you provisioned your solution.</span></span>
4. <span data-ttu-id="18980-207">Kliknij przycisk **aplikacji**.</span><span class="sxs-lookup"><span data-stu-id="18980-207">Click **Applications**.</span></span>
5. <span data-ttu-id="18980-208">Kliknij nazwę hello aplikacji hello, która jest zgodna z nazwą wstępnie skonfigurowane rozwiązanie.</span><span class="sxs-lookup"><span data-stu-id="18980-208">Click hello name of hello application that matches your preconfigured solution name.</span></span> <span data-ttu-id="18980-209">Jeśli nie widzisz aplikacji hello na liście, wybierz **aplikacji Moja firma jest właścicielem** w hello **Pokaż** listy rozwijanej i kliknij znacznik wyboru hello.</span><span class="sxs-lookup"><span data-stu-id="18980-209">If you don't see your application in hello list, select **Applications my company owns** in hello **Show** dropdown and click hello check mark.</span></span>
6. <span data-ttu-id="18980-210">U dołu hello hello strony, kliknij przycisk **Zarządzanie manifestu** , a następnie **Pobierz Manifest**.</span><span class="sxs-lookup"><span data-stu-id="18980-210">At hello bottom of hello page, click **Manage Manifest** and then **Download Manifest**.</span></span>
7. <span data-ttu-id="18980-211">Tej procedury pobiera JSON komputera lokalnego tooyour pliku.</span><span class="sxs-lookup"><span data-stu-id="18980-211">This procedure downloads a .json file tooyour local machine.</span></span> <span data-ttu-id="18980-212">Otwórz ten plik do edycji w wybranym edytorze tekstów.</span><span class="sxs-lookup"><span data-stu-id="18980-212">Open this file for editing in a text editor of your choice.</span></span>
8. <span data-ttu-id="18980-213">Na powitania trzeciego wiersza hello pliku JSON można wyświetlić:</span><span class="sxs-lookup"><span data-stu-id="18980-213">On hello third line of hello .json file, you can see:</span></span>

   ```json
   "appRoles" : [],
   ```
   <span data-ttu-id="18980-214">Zastąp ten wiersz hello następującego kodu:</span><span class="sxs-lookup"><span data-stu-id="18980-214">Replace this line with hello following code:</span></span>

   ```json
   "appRoles": [
   {
   "allowedMemberTypes": [
   "User"
   ],
   "description": "Administrator access toohello application",
   "displayName": "Admin",
   "id": "a400a00b-f67c-42b7-ba9a-f73d8c67e433",
   "isEnabled": true,
   "value": "Admin"
   },
   {
   "allowedMemberTypes": [
   "User"
   ],
   "description": "Read only access toodevice information",
   "displayName": "Read Only",
   "id": "e5bbd0f5-128e-4362-9dd1-8f253c6082d7",
   "isEnabled": true,
   "value": "ReadOnly"
   } ],
   ```

9. <span data-ttu-id="18980-215">Zapisz plik JSON zaktualizowane hello (można zastąpić istniejącego pliku hello).</span><span class="sxs-lookup"><span data-stu-id="18980-215">Save hello updated .json file (you can overwrite hello existing file).</span></span>
10. <span data-ttu-id="18980-216">Hello klasycznego portalu Azure, u dołu strony hello hello wybierz **Zarządzanie manifestu** następnie **przekazać manifestu** plik .json hello tooupload zapisane w poprzednim kroku hello.</span><span class="sxs-lookup"><span data-stu-id="18980-216">In hello Azure classic portal, at hello bottom of hello page, select **Manage Manifest** then **Upload Manifest** tooupload hello .json file you saved in hello previous step.</span></span>
11. <span data-ttu-id="18980-217">Zostały dodane hello **Admin** i **tylko do odczytu** ról tooyour aplikacji.</span><span class="sxs-lookup"><span data-stu-id="18980-217">You have now added hello **Admin** and **ReadOnly** roles tooyour application.</span></span>
12. <span data-ttu-id="18980-218">tooassign jedną z tych ról użytkownika tooa w katalogu, zobacz [uprawnienia w witrynie azureiotsuite.com hello][lnk-permissions].</span><span class="sxs-lookup"><span data-stu-id="18980-218">tooassign one of these roles tooa user in your directory, see [Permissions on hello azureiotsuite.com site][lnk-permissions].</span></span>

## <a name="feedback"></a><span data-ttu-id="18980-219">Opinia</span><span class="sxs-lookup"><span data-stu-id="18980-219">Feedback</span></span>

<span data-ttu-id="18980-220">Masz dostosowanie chcesz toosee omówione w tym dokumencie?</span><span class="sxs-lookup"><span data-stu-id="18980-220">Do you have a customization you'd like toosee covered in this document?</span></span> <span data-ttu-id="18980-221">Dodaj propozycje dotyczące funkcji zbyt[User Voice](https://feedback.azure.com/forums/321918-azure-iot), lub komentarz w tym artykule.</span><span class="sxs-lookup"><span data-stu-id="18980-221">Add feature suggestions too[User Voice](https://feedback.azure.com/forums/321918-azure-iot), or comment on this article.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="18980-222">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="18980-222">Next steps</span></span>

<span data-ttu-id="18980-223">toolearn więcej informacji na temat hello opcje dostosowywania hello wstępnie rozwiązań, zobacz:</span><span class="sxs-lookup"><span data-stu-id="18980-223">toolearn more about hello options for customizing hello preconfigured solutions, see:</span></span>

* <span data-ttu-id="18980-224">[Łączenie aplikacji logiki tooyour Azure IoT pakiet monitorowania zdalnego wstępnie skonfigurowane rozwiązanie][lnk-logicapp]</span><span class="sxs-lookup"><span data-stu-id="18980-224">[Connect Logic App tooyour Azure IoT Suite Remote Monitoring preconfigured solution][lnk-logicapp]</span></span>
* <span data-ttu-id="18980-225">[Dynamiczne telemetrii za pomocą zdalnego wstępnie skonfigurowane rozwiązanie monitorujące hello][lnk-dynamic]</span><span class="sxs-lookup"><span data-stu-id="18980-225">[Use dynamic telemetry with hello remote monitoring preconfigured solution][lnk-dynamic]</span></span>
* <span data-ttu-id="18980-226">[Urządzenie informacji metadanych w hello zdalne monitorowanie wstępnie skonfigurowane rozwiązanie][lnk-devinfo]</span><span class="sxs-lookup"><span data-stu-id="18980-226">[Device information metadata in hello remote monitoring preconfigured solution][lnk-devinfo]</span></span>
* <span data-ttu-id="18980-227">[Dostosuj sposób hello połączenia fabryki rozwiązania wyświetla dane z serwerów OPC UA][lnk-cf-customize]</span><span class="sxs-lookup"><span data-stu-id="18980-227">[Customize how hello connected factory solution displays data from your OPC UA servers][lnk-cf-customize]</span></span>

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