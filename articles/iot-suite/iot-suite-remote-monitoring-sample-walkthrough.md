---
title: "aaaRemote monitorowanie wstępnie skonfigurowane rozwiązanie wskazówki | Dokumentacja firmy Microsoft"
description: "Opis hello Azure IoT wstępnie skonfigurowane rozwiązanie monitorowania zdalnego i jego architektury."
services: 
suite: iot-suite
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 31fe13af-0482-47be-b4c8-e98e36625855
ms.service: iot-suite
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/24/2017
ms.author: dobett
ms.openlocfilehash: 57a336bd94938c2b9ee5d3456ea8e45446cf3d33
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="remote-monitoring-preconfigured-solution-walkthrough"></a><span data-ttu-id="5a2f5-103">Przewodnik po wstępnie skonfigurowanym rozwiązaniu monitorowania zdalnego</span><span class="sxs-lookup"><span data-stu-id="5a2f5-103">Remote monitoring preconfigured solution walkthrough</span></span>

<span data-ttu-id="5a2f5-104">Witaj, monitorowania zdalnego pakiet IoT [wstępnie skonfigurowane rozwiązanie] [ lnk-preconfigured-solutions] implementacja end-to-end monitoruje rozwiązanie dla wielu komputerów z systemem w lokalizacjach zdalnych.</span><span class="sxs-lookup"><span data-stu-id="5a2f5-104">hello IoT Suite remote monitoring [preconfigured solution][lnk-preconfigured-solutions] is an implementation of an end-to-end monitoring solution for multiple machines running in remote locations.</span></span> <span data-ttu-id="5a2f5-105">rozwiązanie Hello łączy tooprovide klucza usługi Azure ogólną implementację hello scenariusza biznesowego.</span><span class="sxs-lookup"><span data-stu-id="5a2f5-105">hello solution combines key Azure services tooprovide a generic implementation of hello business scenario.</span></span> <span data-ttu-id="5a2f5-106">Za pomocą hello rozwiązania jako punkt początkowy dla własnego implementacji i [dostosować] [ lnk-customize] on toomeet własnych konkretnych potrzeb biznesowych.</span><span class="sxs-lookup"><span data-stu-id="5a2f5-106">You can use hello solution as a starting point for your own implementation and [customize][lnk-customize] it toomeet your own specific business requirements.</span></span>

<span data-ttu-id="5a2f5-107">W tym artykule przedstawiono niektóre z kluczowych elementów tooenable rozwiązanie monitorowania zdalnego hello hello toounderstand jej działania.</span><span class="sxs-lookup"><span data-stu-id="5a2f5-107">This article walks you through some of hello key elements of hello remote monitoring solution tooenable you toounderstand how it works.</span></span> <span data-ttu-id="5a2f5-108">Ta wiedza ułatwi Ci:</span><span class="sxs-lookup"><span data-stu-id="5a2f5-108">This knowledge helps you to:</span></span>

* <span data-ttu-id="5a2f5-109">Rozwiązywanie problemów w rozwiązaniu hello.</span><span class="sxs-lookup"><span data-stu-id="5a2f5-109">Troubleshoot issues in hello solution.</span></span>
* <span data-ttu-id="5a2f5-110">Planowanie sposobu toocustomize toohello rozwiązania toomeet indywidualnymi wymaganiami.</span><span class="sxs-lookup"><span data-stu-id="5a2f5-110">Plan how toocustomize toohello solution toomeet your own specific requirements.</span></span> 
* <span data-ttu-id="5a2f5-111">Projektowanie własnego rozwiązania IoT korzystającego z usług Azure.</span><span class="sxs-lookup"><span data-stu-id="5a2f5-111">Design your own IoT solution that uses Azure services.</span></span>

## <a name="logical-architecture"></a><span data-ttu-id="5a2f5-112">Architektura logiczna</span><span class="sxs-lookup"><span data-stu-id="5a2f5-112">Logical architecture</span></span>

<span data-ttu-id="5a2f5-113">powitania po diagram przedstawia hello logiczne składniki hello wstępnie skonfigurowane rozwiązanie:</span><span class="sxs-lookup"><span data-stu-id="5a2f5-113">hello following diagram outlines hello logical components of hello preconfigured solution:</span></span>

![Architektura logiczna](media/iot-suite-remote-monitoring-sample-walkthrough/remote-monitoring-architecture.png)

## <a name="simulated-devices"></a><span data-ttu-id="5a2f5-115">Symulowane urządzenia</span><span class="sxs-lookup"><span data-stu-id="5a2f5-115">Simulated devices</span></span>

<span data-ttu-id="5a2f5-116">W rozwiązaniu hello wstępnie hello symulowane urządzenie reprezentuje urządzenie chłodzące (na przykład klimatyzator budynku lub jednostki obsługi lotniczego zakładzie).</span><span class="sxs-lookup"><span data-stu-id="5a2f5-116">In hello preconfigured solution, hello simulated device represents a cooling device (such as a building air conditioner or facility air handling unit).</span></span> <span data-ttu-id="5a2f5-117">Podczas wdrażania hello wstępnie skonfigurowane rozwiązanie automatycznie udostępnić cztery symulowanego urządzenia z systemem w [zadań WebJob Azure][lnk-webjobs].</span><span class="sxs-lookup"><span data-stu-id="5a2f5-117">When you deploy hello preconfigured solution, you also automatically provision four simulated devices that run in an [Azure WebJob][lnk-webjobs].</span></span> <span data-ttu-id="5a2f5-118">urządzenia Hello symulowane ułatwiają możesz tooexplore hello zachowanie rozwiązania hello bez toodeploy potrzeby hello żadnych urządzeń fizycznych.</span><span class="sxs-lookup"><span data-stu-id="5a2f5-118">hello simulated devices make it easy for you tooexplore hello behavior of hello solution without hello need toodeploy any physical devices.</span></span> <span data-ttu-id="5a2f5-119">toodeploy rzeczywistym fizyczne urządzenia, zobacz hello [połączyć Twoje toohello urządzenie zdalne monitorowanie wstępnie skonfigurowane rozwiązanie] [ lnk-connect-rm] samouczka.</span><span class="sxs-lookup"><span data-stu-id="5a2f5-119">toodeploy a real physical device, see hello [Connect your device toohello remote monitoring preconfigured solution][lnk-connect-rm] tutorial.</span></span>

### <a name="device-to-cloud-messages"></a><span data-ttu-id="5a2f5-120">Komunikaty z urządzenia do chmury</span><span class="sxs-lookup"><span data-stu-id="5a2f5-120">Device-to-cloud messages</span></span>

<span data-ttu-id="5a2f5-121">Każdy symulowane urządzenie może wysyłać hello następującego komunikatu typy tooIoT Centrum:</span><span class="sxs-lookup"><span data-stu-id="5a2f5-121">Each simulated device can send hello following message types tooIoT Hub:</span></span>

| <span data-ttu-id="5a2f5-122">Komunikat</span><span class="sxs-lookup"><span data-stu-id="5a2f5-122">Message</span></span> | <span data-ttu-id="5a2f5-123">Opis</span><span class="sxs-lookup"><span data-stu-id="5a2f5-123">Description</span></span> |
| --- | --- |
| <span data-ttu-id="5a2f5-124">Uruchamianie</span><span class="sxs-lookup"><span data-stu-id="5a2f5-124">Startup</span></span> |<span data-ttu-id="5a2f5-125">Po uruchomieniu urządzenia hello wysyła **informacje o urządzeniu** komunikat zawierający informacje o sobie toohello zaplecza.</span><span class="sxs-lookup"><span data-stu-id="5a2f5-125">When hello device starts, it sends a **device-info** message containing information about itself toohello back end.</span></span> <span data-ttu-id="5a2f5-126">Te dane obejmują identyfikator urządzenia hello i listę poleceń hello i metod hello obsługuje urządzenia.</span><span class="sxs-lookup"><span data-stu-id="5a2f5-126">This data includes hello device id and a list of hello commands and methods hello device supports.</span></span> |
| <span data-ttu-id="5a2f5-127">Obecność</span><span class="sxs-lookup"><span data-stu-id="5a2f5-127">Presence</span></span> |<span data-ttu-id="5a2f5-128">Urządzenie okresowo wysyła **obecności** komunikatu tooreport czy hello urządzenia można ustawić obecności hello czujnika.</span><span class="sxs-lookup"><span data-stu-id="5a2f5-128">A device periodically sends a **presence** message tooreport whether hello device can sense hello presence of a sensor.</span></span> |
| <span data-ttu-id="5a2f5-129">Telemetria</span><span class="sxs-lookup"><span data-stu-id="5a2f5-129">Telemetry</span></span> |<span data-ttu-id="5a2f5-130">Urządzenie okresowo wysyła **telemetrii** komunikat, który zgłasza symulowane wartości hello temperatury i wilgotności zebrane z urządzeń hello na symulowane czujników.</span><span class="sxs-lookup"><span data-stu-id="5a2f5-130">A device periodically sends a **telemetry** message that reports simulated values for hello temperature and humidity collected from hello device's simulated sensors.</span></span> |

> [!NOTE]
> <span data-ttu-id="5a2f5-131">rozwiązanie Hello przechowywana lista hello polecenia obsługiwane przez urządzenia hello w bazie danych rozwiązania Cosmos bazy danych, a nie w Witaj dwie urządzenia.</span><span class="sxs-lookup"><span data-stu-id="5a2f5-131">hello solution stores hello list of commands supported by hello device in a Cosmos DB database and not in hello device twin.</span></span>

### <a name="properties-and-device-twins"></a><span data-ttu-id="5a2f5-132">Właściwości i bliźniacze reprezentacje urządzeń</span><span class="sxs-lookup"><span data-stu-id="5a2f5-132">Properties and device twins</span></span>

<span data-ttu-id="5a2f5-133">Witaj symulowanego urządzenia wysyłają hello następującego urządzenia właściwości toohello [dwie] [ lnk-device-twins] w Centrum IoT hello jako *zgłosił właściwości*.</span><span class="sxs-lookup"><span data-stu-id="5a2f5-133">hello simulated devices send hello following device properties toohello [twin][lnk-device-twins] in hello IoT hub as *reported properties*.</span></span> <span data-ttu-id="5a2f5-134">Witaj wysyła urządzenia zgłoszone właściwości podczas uruchamiania i w odpowiedzi tooa **zmiany stanu urządzenia** polecenia lub metody.</span><span class="sxs-lookup"><span data-stu-id="5a2f5-134">hello device sends reported properties at startup and in response tooa **Change Device State** command or method.</span></span>

| <span data-ttu-id="5a2f5-135">Właściwość</span><span class="sxs-lookup"><span data-stu-id="5a2f5-135">Property</span></span> | <span data-ttu-id="5a2f5-136">Przeznaczenie</span><span class="sxs-lookup"><span data-stu-id="5a2f5-136">Purpose</span></span> |
| --- | --- |
| <span data-ttu-id="5a2f5-137">Config.TelemetryInterval</span><span class="sxs-lookup"><span data-stu-id="5a2f5-137">Config.TelemetryInterval</span></span> | <span data-ttu-id="5a2f5-138">Częstotliwość (w sekundach) hello urządzenie wysyła dane telemetryczne</span><span class="sxs-lookup"><span data-stu-id="5a2f5-138">Frequency (seconds) hello device sends telemetry</span></span> |
| <span data-ttu-id="5a2f5-139">Config.TemperatureMeanValue</span><span class="sxs-lookup"><span data-stu-id="5a2f5-139">Config.TemperatureMeanValue</span></span> | <span data-ttu-id="5a2f5-140">Określa średnią wartość hello hello symulowane temperatury telemetrii</span><span class="sxs-lookup"><span data-stu-id="5a2f5-140">Specifies hello mean value for hello simulated temperature telemetry</span></span> |
| <span data-ttu-id="5a2f5-141">Device.DeviceID</span><span class="sxs-lookup"><span data-stu-id="5a2f5-141">Device.DeviceID</span></span> |<span data-ttu-id="5a2f5-142">Identyfikator, który jest podany lub przypisywana podczas tworzenia urządzenia w rozwiązaniu hello</span><span class="sxs-lookup"><span data-stu-id="5a2f5-142">Id that is either provided or assigned when a device is created in hello solution</span></span> |
| <span data-ttu-id="5a2f5-143">Device.DeviceState</span><span class="sxs-lookup"><span data-stu-id="5a2f5-143">Device.DeviceState</span></span> | <span data-ttu-id="5a2f5-144">Zgłoszone przez urządzenie hello stanu</span><span class="sxs-lookup"><span data-stu-id="5a2f5-144">State reported by hello device</span></span> |
| <span data-ttu-id="5a2f5-145">Device.CreatedTime</span><span class="sxs-lookup"><span data-stu-id="5a2f5-145">Device.CreatedTime</span></span> |<span data-ttu-id="5a2f5-146">Czas hello urządzenie zostało utworzone w rozwiązaniu hello</span><span class="sxs-lookup"><span data-stu-id="5a2f5-146">Time hello device was created in hello solution</span></span> |
| <span data-ttu-id="5a2f5-147">Device.StartupTime</span><span class="sxs-lookup"><span data-stu-id="5a2f5-147">Device.StartupTime</span></span> |<span data-ttu-id="5a2f5-148">Czas hello urządzenia została uruchomiona.</span><span class="sxs-lookup"><span data-stu-id="5a2f5-148">Time hello device was started</span></span> |
| <span data-ttu-id="5a2f5-149">Device.LastDesiredPropertyChange</span><span class="sxs-lookup"><span data-stu-id="5a2f5-149">Device.LastDesiredPropertyChange</span></span> |<span data-ttu-id="5a2f5-150">Zmień numer wersji Hello hello ostatniego żądanej właściwości</span><span class="sxs-lookup"><span data-stu-id="5a2f5-150">hello version number of hello last desired property change</span></span> |
| <span data-ttu-id="5a2f5-151">Device.Location.Latitude</span><span class="sxs-lookup"><span data-stu-id="5a2f5-151">Device.Location.Latitude</span></span> |<span data-ttu-id="5a2f5-152">Współrzędne lokalizacji hello urządzenia</span><span class="sxs-lookup"><span data-stu-id="5a2f5-152">Latitude location of hello device</span></span> |
| <span data-ttu-id="5a2f5-153">Device.Location.Longitude</span><span class="sxs-lookup"><span data-stu-id="5a2f5-153">Device.Location.Longitude</span></span> |<span data-ttu-id="5a2f5-154">Lokalizacji geograficznej hello urządzenia</span><span class="sxs-lookup"><span data-stu-id="5a2f5-154">Longitude location of hello device</span></span> |
| <span data-ttu-id="5a2f5-155">System.Manufacturer</span><span class="sxs-lookup"><span data-stu-id="5a2f5-155">System.Manufacturer</span></span> |<span data-ttu-id="5a2f5-156">Producent urządzenia</span><span class="sxs-lookup"><span data-stu-id="5a2f5-156">Device manufacturer</span></span> |
| <span data-ttu-id="5a2f5-157">System.ModelNumber</span><span class="sxs-lookup"><span data-stu-id="5a2f5-157">System.ModelNumber</span></span> |<span data-ttu-id="5a2f5-158">Numer modelu urządzenia hello</span><span class="sxs-lookup"><span data-stu-id="5a2f5-158">Model number of hello device</span></span> |
| <span data-ttu-id="5a2f5-159">System.SerialNumber</span><span class="sxs-lookup"><span data-stu-id="5a2f5-159">System.SerialNumber</span></span> |<span data-ttu-id="5a2f5-160">Numer seryjny urządzenia hello</span><span class="sxs-lookup"><span data-stu-id="5a2f5-160">Serial number of hello device</span></span> |
| <span data-ttu-id="5a2f5-161">System.FirmwareVersion</span><span class="sxs-lookup"><span data-stu-id="5a2f5-161">System.FirmwareVersion</span></span> |<span data-ttu-id="5a2f5-162">Bieżąca wersja oprogramowania układowego na urządzeniu hello</span><span class="sxs-lookup"><span data-stu-id="5a2f5-162">Current version of firmware on hello device</span></span> |
| <span data-ttu-id="5a2f5-163">System.Platform</span><span class="sxs-lookup"><span data-stu-id="5a2f5-163">System.Platform</span></span> |<span data-ttu-id="5a2f5-164">Architektura platformy hello urządzenia</span><span class="sxs-lookup"><span data-stu-id="5a2f5-164">Platform architecture of hello device</span></span> |
| <span data-ttu-id="5a2f5-165">System.Processor</span><span class="sxs-lookup"><span data-stu-id="5a2f5-165">System.Processor</span></span> |<span data-ttu-id="5a2f5-166">Urządzenie hello uruchomionych procesora</span><span class="sxs-lookup"><span data-stu-id="5a2f5-166">Processor running hello device</span></span> |
| <span data-ttu-id="5a2f5-167">System.InstalledRAM</span><span class="sxs-lookup"><span data-stu-id="5a2f5-167">System.InstalledRAM</span></span> |<span data-ttu-id="5a2f5-168">Ilość pamięci RAM na urządzeniu hello</span><span class="sxs-lookup"><span data-stu-id="5a2f5-168">Amount of RAM installed on hello device</span></span> |

<span data-ttu-id="5a2f5-169">Symulator Hello nasion tych właściwości w symulowanego urządzenia z wartości przykładowych.</span><span class="sxs-lookup"><span data-stu-id="5a2f5-169">hello simulator seeds these properties in simulated devices with sample values.</span></span> <span data-ttu-id="5a2f5-170">Zawsze symulatora hello inicjuje symulowane urządzenie, urządzenie hello raporty hello tooIoT metadanych wstępnie zdefiniowanego Centrum jako właściwości zgłoszony.</span><span class="sxs-lookup"><span data-stu-id="5a2f5-170">Each time hello simulator initializes a simulated device, hello device reports hello pre-defined metadata tooIoT Hub as reported properties.</span></span> <span data-ttu-id="5a2f5-171">Właściwości zgłoszonego można zaktualizować tylko przez urządzenia hello.</span><span class="sxs-lookup"><span data-stu-id="5a2f5-171">Reported properties can only be updated by hello device.</span></span> <span data-ttu-id="5a2f5-172">toochange zgłoszone właściwości, ustaw właściwość żądaną w portalu rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="5a2f5-172">toochange a reported property, you set a desired property in solution portal.</span></span> <span data-ttu-id="5a2f5-173">Jest odpowiedzialny za hello hello urządzenia:</span><span class="sxs-lookup"><span data-stu-id="5a2f5-173">It is hello responsibility of hello device to:</span></span>

1. <span data-ttu-id="5a2f5-174">Okresowo pobrać żądanej właściwości z Centrum IoT hello.</span><span class="sxs-lookup"><span data-stu-id="5a2f5-174">Periodically retrieve desired properties from hello IoT hub.</span></span>
2. <span data-ttu-id="5a2f5-175">Zaktualizuj jego konfigurację z hello żądaną wartość właściwości.</span><span class="sxs-lookup"><span data-stu-id="5a2f5-175">Update its configuration with hello desired property value.</span></span>
3. <span data-ttu-id="5a2f5-176">Wyślij hello nowe wartości toohello zapasowego Centrum jako właściwość zgłoszony.</span><span class="sxs-lookup"><span data-stu-id="5a2f5-176">Send hello new value back toohello hub as a reported property.</span></span>

<span data-ttu-id="5a2f5-177">Z pulpitu nawigacyjnego rozwiązania hello, możesz użyć *żądanego właściwości* tooset we właściwościach urządzenia za pomocą hello [dwie urządzenia][lnk-device-twins].</span><span class="sxs-lookup"><span data-stu-id="5a2f5-177">From hello solution dashboard, you can use *desired properties* tooset properties on a device by using hello [device twin][lnk-device-twins].</span></span> <span data-ttu-id="5a2f5-178">Zazwyczaj urządzenia odczytuje wartość żądanej właściwości z hello tooupdate koncentratora, jego stan wewnętrzny i hello raportu zmiany jako właściwość zgłoszony.</span><span class="sxs-lookup"><span data-stu-id="5a2f5-178">Typically, a device reads a desired property value from hello hub tooupdate its internal state and report hello change back as a reported property.</span></span>

> [!NOTE]
> <span data-ttu-id="5a2f5-179">Witaj kodu symulowane urządzenie używa tylko hello **Desired.Config.TemperatureMeanValue** i **Desired.Config.TelemetryInterval** odpowiednie właściwości tooupdate hello zgłosił odesłał właściwości tooIoT koncentratora.</span><span class="sxs-lookup"><span data-stu-id="5a2f5-179">hello simulated device code only uses hello **Desired.Config.TemperatureMeanValue** and **Desired.Config.TelemetryInterval** desired properties tooupdate hello reported properties sent back tooIoT Hub.</span></span> <span data-ttu-id="5a2f5-180">Wszystkie inne żądanej właściwości żądania zmiany są ignorowane w hello symulowane urządzenie.</span><span class="sxs-lookup"><span data-stu-id="5a2f5-180">All other desired property change requests are ignored in hello simulated device.</span></span>

### <a name="methods"></a><span data-ttu-id="5a2f5-181">Metody</span><span class="sxs-lookup"><span data-stu-id="5a2f5-181">Methods</span></span>

<span data-ttu-id="5a2f5-182">Witaj symulowanego urządzenia może obsłużyć hello następujące metody ([bezpośrednie metody][lnk-direct-methods]) wywoływane z portalu rozwiązania hello za pośrednictwem Centrum IoT hello:</span><span class="sxs-lookup"><span data-stu-id="5a2f5-182">hello simulated devices can handle hello following methods ([direct methods][lnk-direct-methods]) invoked from hello solution portal through hello IoT hub:</span></span>

| <span data-ttu-id="5a2f5-183">Metoda</span><span class="sxs-lookup"><span data-stu-id="5a2f5-183">Method</span></span> | <span data-ttu-id="5a2f5-184">Opis</span><span class="sxs-lookup"><span data-stu-id="5a2f5-184">Description</span></span> |
| --- | --- |
| <span data-ttu-id="5a2f5-185">InitiateFirmwareUpdate</span><span class="sxs-lookup"><span data-stu-id="5a2f5-185">InitiateFirmwareUpdate</span></span> |<span data-ttu-id="5a2f5-186">Powoduje, że hello tooperform urządzenia aktualizacji oprogramowania układowego</span><span class="sxs-lookup"><span data-stu-id="5a2f5-186">Instructs hello device tooperform a firmware update</span></span> |
| <span data-ttu-id="5a2f5-187">Ponowne uruchamianie</span><span class="sxs-lookup"><span data-stu-id="5a2f5-187">Reboot</span></span> |<span data-ttu-id="5a2f5-188">Powoduje, że hello tooreboot urządzenia</span><span class="sxs-lookup"><span data-stu-id="5a2f5-188">Instructs hello device tooreboot</span></span> |
| <span data-ttu-id="5a2f5-189">FactoryReset</span><span class="sxs-lookup"><span data-stu-id="5a2f5-189">FactoryReset</span></span> |<span data-ttu-id="5a2f5-190">Powoduje, że tooperform urządzenia hello fabrykę resetowania</span><span class="sxs-lookup"><span data-stu-id="5a2f5-190">Instructs hello device tooperform a factory reset</span></span> |

<span data-ttu-id="5a2f5-191">W przypadku niektórych metod Użyj tooreport właściwości zgłoszone w toku.</span><span class="sxs-lookup"><span data-stu-id="5a2f5-191">Some methods use reported properties tooreport on progress.</span></span> <span data-ttu-id="5a2f5-192">Na przykład Witaj **InitiateFirmwareUpdate** metody symuluje uruchomionych aktualizacji hello asynchronicznie na urządzeniu hello.</span><span class="sxs-lookup"><span data-stu-id="5a2f5-192">For example, hello **InitiateFirmwareUpdate** method simulates running hello update asynchronously on hello device.</span></span> <span data-ttu-id="5a2f5-193">Metoda Hello natychmiast zwraca na urządzeniu hello zadanie asynchroniczne hello kontynuuje aktualizacje stanu toosend ponownie przy użyciu pulpitu nawigacyjnego rozwiązania toohello zgłosił właściwości.</span><span class="sxs-lookup"><span data-stu-id="5a2f5-193">hello method returns immediately on hello device, while hello asynchronous task continues toosend status updates back toohello solution dashboard using reported properties.</span></span>

### <a name="commands"></a><span data-ttu-id="5a2f5-194">Polecenia</span><span class="sxs-lookup"><span data-stu-id="5a2f5-194">Commands</span></span>

<span data-ttu-id="5a2f5-195">urządzenia Hello symulowane może obsłużyć hello następującego polecenia (chmury do urządzenia wiadomości) wysyłane z portalu rozwiązania hello za pośrednictwem Centrum IoT hello:</span><span class="sxs-lookup"><span data-stu-id="5a2f5-195">hello simulated devices can handle hello following commands (cloud-to-device messages) sent from hello solution portal through hello IoT hub:</span></span>

| <span data-ttu-id="5a2f5-196">Polecenie</span><span class="sxs-lookup"><span data-stu-id="5a2f5-196">Command</span></span> | <span data-ttu-id="5a2f5-197">Opis</span><span class="sxs-lookup"><span data-stu-id="5a2f5-197">Description</span></span> |
| --- | --- |
| <span data-ttu-id="5a2f5-198">PingDevice</span><span class="sxs-lookup"><span data-stu-id="5a2f5-198">PingDevice</span></span> |<span data-ttu-id="5a2f5-199">Wysyła *ping* toohello toocheck urządzenie jest aktywne</span><span class="sxs-lookup"><span data-stu-id="5a2f5-199">Sends a *ping* toohello device toocheck it is alive</span></span> |
| <span data-ttu-id="5a2f5-200">StartTelemetry</span><span class="sxs-lookup"><span data-stu-id="5a2f5-200">StartTelemetry</span></span> |<span data-ttu-id="5a2f5-201">Urządzenie hello rozpoczyna wysyłanie danych telemetrycznych</span><span class="sxs-lookup"><span data-stu-id="5a2f5-201">Starts hello device sending telemetry</span></span> |
| <span data-ttu-id="5a2f5-202">StopTelemetry</span><span class="sxs-lookup"><span data-stu-id="5a2f5-202">StopTelemetry</span></span> |<span data-ttu-id="5a2f5-203">Zatrzymuje hello urządzenia z wysyłania danych telemetrycznych</span><span class="sxs-lookup"><span data-stu-id="5a2f5-203">Stops hello device from sending telemetry</span></span> |
| <span data-ttu-id="5a2f5-204">ChangeSetPointTemp</span><span class="sxs-lookup"><span data-stu-id="5a2f5-204">ChangeSetPointTemp</span></span> |<span data-ttu-id="5a2f5-205">Ustaw punkt wartość hello zmiany, wokół którego hello jest generowany losowe dane</span><span class="sxs-lookup"><span data-stu-id="5a2f5-205">Changes hello set point value around which hello random data is generated</span></span> |
| <span data-ttu-id="5a2f5-206">DiagnosticTelemetry</span><span class="sxs-lookup"><span data-stu-id="5a2f5-206">DiagnosticTelemetry</span></span> |<span data-ttu-id="5a2f5-207">Wyzwalacze hello toosend symulator urządzeń wartość dodatkowe dane telemetryczne (externalTemp)</span><span class="sxs-lookup"><span data-stu-id="5a2f5-207">Triggers hello device simulator toosend an additional telemetry value (externalTemp)</span></span> |
| <span data-ttu-id="5a2f5-208">ChangeDeviceState</span><span class="sxs-lookup"><span data-stu-id="5a2f5-208">ChangeDeviceState</span></span> |<span data-ttu-id="5a2f5-209">Zmienia właściwość rozszerzona stanu hello urządzenia i wysyła komunikat z informacjami o urządzeniu hello z hello urządzenia</span><span class="sxs-lookup"><span data-stu-id="5a2f5-209">Changes an extended state property for hello device and sends hello device info message from hello device</span></span> |

> [!NOTE]
> <span data-ttu-id="5a2f5-210">Porównanie tych poleceń (komunikatów wysyłanych z chmury do urządzenia) i metod (metod bezpośrednich) znajduje się w temacie [Wskazówki dotyczące komunikacji z chmury do urządzenia][lnk-c2d-guidance].</span><span class="sxs-lookup"><span data-stu-id="5a2f5-210">For a comparison of these commands (cloud-to-device messages) and methods (direct methods), see [Cloud-to-device communications guidance][lnk-c2d-guidance].</span></span>

## <a name="iot-hub"></a><span data-ttu-id="5a2f5-211">Usługa IoT Hub</span><span class="sxs-lookup"><span data-stu-id="5a2f5-211">IoT Hub</span></span>

<span data-ttu-id="5a2f5-212">Witaj [Centrum IoT] [ lnk-iothub] wysyła strumień danych przesyłanych z urządzeń hello w chmurze hello i ułatwia toohello dostępne zadania usługi analiza strumienia Azure (ASA).</span><span class="sxs-lookup"><span data-stu-id="5a2f5-212">hello [IoT hub][lnk-iothub] ingests data sent from hello devices into hello cloud and makes it available toohello Azure Stream Analytics (ASA) jobs.</span></span> <span data-ttu-id="5a2f5-213">Każde zadanie ASA strumienia używa oddzielnych Centrum IoT konsumenta grupy tooread hello strumienia komunikatów z urządzeń.</span><span class="sxs-lookup"><span data-stu-id="5a2f5-213">Each stream ASA job uses a separate IoT Hub consumer group tooread hello stream of messages from your devices.</span></span>

<span data-ttu-id="5a2f5-214">Witaj Centrum IoT w rozwiązaniu hello również:</span><span class="sxs-lookup"><span data-stu-id="5a2f5-214">hello IoT hub in hello solution also:</span></span>

- <span data-ttu-id="5a2f5-215">Przechowuje rejestr tożsamości, który przechowuje identyfikatory hello i klucze uwierzytelniania wszystkich urządzeń hello dozwolone tooconnect toohello portalu.</span><span class="sxs-lookup"><span data-stu-id="5a2f5-215">Maintains an identity registry that stores hello ids and authentication keys of all hello devices permitted tooconnect toohello portal.</span></span> <span data-ttu-id="5a2f5-216">Można włączyć lub wyłączyć urządzeniami za pomocą hello rejestru tożsamości.</span><span class="sxs-lookup"><span data-stu-id="5a2f5-216">You can enable and disable devices through hello identity registry.</span></span>
- <span data-ttu-id="5a2f5-217">Wysyła polecenia urządzeń tooyour imieniu hello rozwiązanie portalu.</span><span class="sxs-lookup"><span data-stu-id="5a2f5-217">Sends commands tooyour devices on behalf of hello solution portal.</span></span>
- <span data-ttu-id="5a2f5-218">Wywołuje metody na urządzeniach w imieniu hello rozwiązanie portalu.</span><span class="sxs-lookup"><span data-stu-id="5a2f5-218">Invokes methods on your devices on behalf of hello solution portal.</span></span>
- <span data-ttu-id="5a2f5-219">Obsługuje bliźniacze reprezentacje wszystkich zarejestrowanych urządzeń.</span><span class="sxs-lookup"><span data-stu-id="5a2f5-219">Maintains device twins for all registered devices.</span></span> <span data-ttu-id="5a2f5-220">Dwie urządzeń są przechowywane wartości właściwości hello zgłoszone przez urządzenie.</span><span class="sxs-lookup"><span data-stu-id="5a2f5-220">A device twin stores hello property values reported by a device.</span></span> <span data-ttu-id="5a2f5-221">Dwie urządzenia przechowuje także żądanej właściwości, w portalu rozwiązania hello, hello tooretrieve urządzenia, gdy obok łączy.</span><span class="sxs-lookup"><span data-stu-id="5a2f5-221">A device twin also stores desired properties, set in hello solution portal, for hello device tooretrieve when it next connects.</span></span>
- <span data-ttu-id="5a2f5-222">Harmonogramy zadań właściwości tooset dla wielu urządzeń lub wywołanie metody na wielu urządzeniach.</span><span class="sxs-lookup"><span data-stu-id="5a2f5-222">Schedules jobs tooset properties for multiple devices or invoke methods on multiple devices.</span></span>

## <a name="azure-stream-analytics"></a><span data-ttu-id="5a2f5-223">Usługa Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="5a2f5-223">Azure Stream Analytics</span></span>

<span data-ttu-id="5a2f5-224">W hello zdalne monitorowanie rozwiązania [Azure Stream Analytics] [ lnk-asa] (ASA) wywołuje urządzenia komunikatów odebranych przez składniki hello IoT hub tooother zaplecza do przetwarzania lub magazynu.</span><span class="sxs-lookup"><span data-stu-id="5a2f5-224">In hello remote monitoring solution, [Azure Stream Analytics][lnk-asa] (ASA) dispatches device messages received by hello IoT hub tooother back-end components for processing or storage.</span></span> <span data-ttu-id="5a2f5-225">Różne zadania ASA wykonywać określonych funkcji, na podstawie zawartości hello wiadomości powitania.</span><span class="sxs-lookup"><span data-stu-id="5a2f5-225">Different ASA jobs perform specific functions based on hello content of hello messages.</span></span>

<span data-ttu-id="5a2f5-226">**Zadanie 1: Informacje o urządzeniu** filtruje komunikaty informacyjne urządzenia ze strumienia przychodzącego wiadomość hello i wysyła je punktu końcowego Centrum zdarzeń tooan.</span><span class="sxs-lookup"><span data-stu-id="5a2f5-226">**Job 1: Device Info** filters device information messages from hello incoming message stream and sends them tooan Event Hub endpoint.</span></span> <span data-ttu-id="5a2f5-227">Urządzenie wysyła komunikaty informacyjne urządzenia podczas uruchamiania i w odpowiedzi tooa **SendDeviceInfo** polecenia.</span><span class="sxs-lookup"><span data-stu-id="5a2f5-227">A device sends device information messages at startup and in response tooa **SendDeviceInfo** command.</span></span> <span data-ttu-id="5a2f5-228">To zadanie używa powitania po tooidentify definicji zapytania **informacje o urządzeniu** wiadomości:</span><span class="sxs-lookup"><span data-stu-id="5a2f5-228">This job uses hello following query definition tooidentify **device-info** messages:</span></span>

```
SELECT * FROM DeviceDataStream Partition By PartitionId WHERE  ObjectType = 'DeviceInfo'
```

<span data-ttu-id="5a2f5-229">To zadanie wysyła tooan jego danych wyjściowych Centrum zdarzeń dla dalszego przetwarzania.</span><span class="sxs-lookup"><span data-stu-id="5a2f5-229">This job sends its output tooan Event Hub for further processing.</span></span>

<span data-ttu-id="5a2f5-230">**Zadanie 2: Reguły** porównuje przychodzące dane telemetryczne dotyczące temperatury i wilgotności z wartościami progowymi określonymi dla urządzenia.</span><span class="sxs-lookup"><span data-stu-id="5a2f5-230">**Job 2: Rules** evaluates incoming temperature and humidity telemetry values against per-device thresholds.</span></span> <span data-ttu-id="5a2f5-231">Próg wartości są ustawiane w edytorze zasad hello dostępne w portalu rozwiązania hello.</span><span class="sxs-lookup"><span data-stu-id="5a2f5-231">Threshold values are set in hello rules editor available in hello solution portal.</span></span> <span data-ttu-id="5a2f5-232">Poszczególne pary urządzenie/wartość są uporządkowane według sygnatur czasowych i przechowywane w obiekcie blob, który jest odczytywany przez usługę Stream Analytics jako **dane referencyjne**.</span><span class="sxs-lookup"><span data-stu-id="5a2f5-232">Each device/value pair is stored by timestamp in a blob which Stream Analytics reads in as **Reference Data**.</span></span> <span data-ttu-id="5a2f5-233">zadanie Hello porównuje wartości niepustym progiem zestaw hello hello urządzenia.</span><span class="sxs-lookup"><span data-stu-id="5a2f5-233">hello job compares any non-empty value against hello set threshold for hello device.</span></span> <span data-ttu-id="5a2f5-234">W przypadku przekroczenia hello ">" warunek, danych wyjściowych zadania hello **alarm** zdarzenie wskazujące ten próg hello przekroczeniu i udostępnia hello urządzenia, wartość oraz wartości sygnatur czasowych.</span><span class="sxs-lookup"><span data-stu-id="5a2f5-234">If it exceeds hello '>' condition, hello job outputs an **alarm** event that indicates that hello threshold is exceeded and provides hello device, value, and timestamp values.</span></span> <span data-ttu-id="5a2f5-235">To zadanie używa następującej kwerendy definicji tooidentify telemetrii wiadomości, które powinny wyzwalać alarm hello:</span><span class="sxs-lookup"><span data-stu-id="5a2f5-235">This job uses hello following query definition tooidentify telemetry messages that should trigger an alarm:</span></span>

```
WITH AlarmsData AS 
(
SELECT
     Stream.IoTHub.ConnectionDeviceId AS DeviceId,
     'Temperature' as ReadingType,
     Stream.Temperature as Reading,
     Ref.Temperature as Threshold,
     Ref.TemperatureRuleOutput as RuleOutput,
     Stream.EventEnqueuedUtcTime AS [Time]
FROM IoTTelemetryStream Stream
JOIN DeviceRulesBlob Ref ON Stream.IoTHub.ConnectionDeviceId = Ref.DeviceID
WHERE
     Ref.Temperature IS NOT null AND Stream.Temperature > Ref.Temperature

UNION ALL

SELECT
     Stream.IoTHub.ConnectionDeviceId AS DeviceId,
     'Humidity' as ReadingType,
     Stream.Humidity as Reading,
     Ref.Humidity as Threshold,
     Ref.HumidityRuleOutput as RuleOutput,
     Stream.EventEnqueuedUtcTime AS [Time]
FROM IoTTelemetryStream Stream
JOIN DeviceRulesBlob Ref ON Stream.IoTHub.ConnectionDeviceId = Ref.DeviceID
WHERE
     Ref.Humidity IS NOT null AND Stream.Humidity > Ref.Humidity
)

SELECT *
INTO DeviceRulesMonitoring
FROM AlarmsData

SELECT *
INTO DeviceRulesHub
FROM AlarmsData
```

<span data-ttu-id="5a2f5-236">Witaj zadanie wysyła tooan jego danych wyjściowych Centrum zdarzeń dla dalszego przetwarzania i zapisuje szczegóły każdego alertu tooblob magazynu, z którym hello rozwiązanie portalu może odczytać informacji o alertach hello.</span><span class="sxs-lookup"><span data-stu-id="5a2f5-236">hello job sends its output tooan Event Hub for further processing and saves details of each alert tooblob storage from where hello solution portal can read hello alert information.</span></span>

<span data-ttu-id="5a2f5-237">**Zadanie 3: Telemetrii** działa na powitania przychodzących urządzenia telemetrii strumienia na dwa sposoby.</span><span class="sxs-lookup"><span data-stu-id="5a2f5-237">**Job 3: Telemetry** operates on hello incoming device telemetry stream in two ways.</span></span> <span data-ttu-id="5a2f5-238">Hello najpierw wysyła komunikaty dane telemetryczne z magazynu obiektów blob toopersistent hello urządzeń do długoterminowego przechowywania.</span><span class="sxs-lookup"><span data-stu-id="5a2f5-238">hello first sends all telemetry messages from hello devices toopersistent blob storage for long-term storage.</span></span> <span data-ttu-id="5a2f5-239">Hello drugi oblicza średnią, minimalną i maksymalną wilgotność wartości na metodzie przesuwanego okna 5 minutową i wysyła ten tooblob pamięci masowej.</span><span class="sxs-lookup"><span data-stu-id="5a2f5-239">hello second computes average, minimum, and maximum humidity values over a five-minute sliding window and sends this data tooblob storage.</span></span> <span data-ttu-id="5a2f5-240">portal rozwiązania Hello odczytuje dane telemetryczne hello z wykresy hello toopopulate magazynu obiektów blob.</span><span class="sxs-lookup"><span data-stu-id="5a2f5-240">hello solution portal reads hello telemetry data from blob storage toopopulate hello charts.</span></span> <span data-ttu-id="5a2f5-241">To zadanie używa powitania po definicji zapytania:</span><span class="sxs-lookup"><span data-stu-id="5a2f5-241">This job uses hello following query definition:</span></span>

```
WITH 
    [StreamData]
AS (
    SELECT
        *
    FROM [IoTHubStream]
    WHERE
        [ObjectType] IS NULL -- Filter out device info and command responses
) 

SELECT
    IoTHub.ConnectionDeviceId AS DeviceId,
    Temperature,
    Humidity,
    ExternalTemperature,
    EventProcessedUtcTime,
    PartitionId,
    EventEnqueuedUtcTime,
    * 
INTO
    [Telemetry]
FROM
    [StreamData]

SELECT
    IoTHub.ConnectionDeviceId AS DeviceId,
    AVG (Humidity) AS [AverageHumidity],
    MIN(Humidity) AS [MinimumHumidity],
    MAX(Humidity) AS [MaxHumidity],
    5.0 AS TimeframeMinutes 
INTO
    [TelemetrySummary]
FROM [StreamData]
WHERE
    [Humidity] IS NOT NULL
GROUP BY
    IoTHub.ConnectionDeviceId,
    SlidingWindow (mi, 5)
```

## <a name="event-hubs"></a><span data-ttu-id="5a2f5-242">Usługa Event Hubs</span><span class="sxs-lookup"><span data-stu-id="5a2f5-242">Event Hubs</span></span>

<span data-ttu-id="5a2f5-243">Witaj **informacje o urządzeniu** i **reguły** ich danych tooEvent koncentratory tooreliably do przodu na toohello dane wyjściowe zadania ASA **procesora zdarzeń** uruchomionych w hello zadania WebJob.</span><span class="sxs-lookup"><span data-stu-id="5a2f5-243">hello **device info** and **rules** ASA jobs output their data tooEvent Hubs tooreliably forward on toohello **Event Processor** running in hello WebJob.</span></span>

## <a name="azure-storage"></a><span data-ttu-id="5a2f5-244">Azure Storage</span><span class="sxs-lookup"><span data-stu-id="5a2f5-244">Azure storage</span></span>

<span data-ttu-id="5a2f5-245">rozwiązanie Hello używa toopersist magazynu obiektów blob platformy Azure wszystkich danych pierwotnych i podsumowują dane telemetryczne hello z hello urządzeń w rozwiązaniu hello.</span><span class="sxs-lookup"><span data-stu-id="5a2f5-245">hello solution uses Azure blob storage toopersist all hello raw and summarized telemetry data from hello devices in hello solution.</span></span> <span data-ttu-id="5a2f5-246">Hello portal odczytuje dane telemetryczne hello z wykresy hello toopopulate magazynu obiektów blob.</span><span class="sxs-lookup"><span data-stu-id="5a2f5-246">hello portal reads hello telemetry data from blob storage toopopulate hello charts.</span></span> <span data-ttu-id="5a2f5-247">alerty toodisplay hello rozwiązanie portalu odczytuje hello dane z magazynu obiektów blob zapisy podczas telemetrii hello wartości przekroczyła skonfigurowany wartości progowe.</span><span class="sxs-lookup"><span data-stu-id="5a2f5-247">toodisplay alerts, hello solution portal reads hello data from blob storage that records when telemetry values exceeded hello configured threshold values.</span></span> <span data-ttu-id="5a2f5-248">rozwiązanie Hello używa również obiektu blob magazynu toorecord hello wartości progowe ustawionych w portalu rozwiązania hello.</span><span class="sxs-lookup"><span data-stu-id="5a2f5-248">hello solution also uses blob storage toorecord hello threshold values you set in hello solution portal.</span></span>

## <a name="webjobs"></a><span data-ttu-id="5a2f5-249">Zadania WebJob</span><span class="sxs-lookup"><span data-stu-id="5a2f5-249">WebJobs</span></span>

<span data-ttu-id="5a2f5-250">Ponadto toohosting hello urządzenia symulatorów, hello zadań Webjob w rozwiązaniu hello również hello hosta **procesora zdarzeń** uruchomionych w zadania WebJob Azure, który obsługuje odpowiedzi polecenia.</span><span class="sxs-lookup"><span data-stu-id="5a2f5-250">In addition toohosting hello device simulators, hello WebJobs in hello solution also host hello **Event Processor** running in an Azure WebJob that handles command responses.</span></span> <span data-ttu-id="5a2f5-251">Używa polecenia odpowiedzi wiadomości tooupdate hello urządzenia historii poleceń (przechowywane w bazie danych DB rozwiązania Cosmos hello).</span><span class="sxs-lookup"><span data-stu-id="5a2f5-251">It uses command response messages tooupdate hello device command history (stored in hello Cosmos DB database).</span></span>

## <a name="cosmos-db"></a><span data-ttu-id="5a2f5-252">Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="5a2f5-252">Cosmos DB</span></span>

<span data-ttu-id="5a2f5-253">rozwiązanie Hello używa informacje toostore bazy danych DB rozwiązania Cosmos hello urządzeń podłączonych toohello rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="5a2f5-253">hello solution uses a Cosmos DB database toostore information about hello devices connected toohello solution.</span></span> <span data-ttu-id="5a2f5-254">Informacje te obejmują hello historii poleceń wysyłane toodevices hello rozwiązanie portalu i metody wywoływane z hello rozwiązanie portalu.</span><span class="sxs-lookup"><span data-stu-id="5a2f5-254">This information includes hello history of commands sent toodevices from hello solution portal and of methods invoked from hello solution portal.</span></span>

## <a name="solution-portal"></a><span data-ttu-id="5a2f5-255">Portal rozwiązania</span><span class="sxs-lookup"><span data-stu-id="5a2f5-255">Solution portal</span></span>

<span data-ttu-id="5a2f5-256">portal rozwiązania Hello jest wdrożony jako część hello wstępnie skonfigurowane rozwiązanie aplikacji sieci web.</span><span class="sxs-lookup"><span data-stu-id="5a2f5-256">hello solution portal is a web app deployed as part of hello preconfigured solution.</span></span> <span data-ttu-id="5a2f5-257">Hello klucza stron w portalu rozwiązania hello są hello pulpitu nawigacyjnego i hello listę urządzeń.</span><span class="sxs-lookup"><span data-stu-id="5a2f5-257">hello key pages in hello solution portal are hello dashboard and hello device list.</span></span>

### <a name="dashboard"></a><span data-ttu-id="5a2f5-258">Pulpit nawigacyjny</span><span class="sxs-lookup"><span data-stu-id="5a2f5-258">Dashboard</span></span>

<span data-ttu-id="5a2f5-259">Formanty javascript usługi Power BI korzysta z tej strony w aplikacji sieci web hello (zobacz [repozytorium elementów wizualnych usługi Power BI](https://www.github.com/Microsoft/PowerBI-visuals)) dane telemetryczne hello toovisualize z hello urządzeń.</span><span class="sxs-lookup"><span data-stu-id="5a2f5-259">This page in hello web app uses PowerBI javascript controls (See [PowerBI-visuals repo](https://www.github.com/Microsoft/PowerBI-visuals)) toovisualize hello telemetry data from hello devices.</span></span> <span data-ttu-id="5a2f5-260">rozwiązanie Hello korzysta z hello ASA telemetrii zadania toowrite hello telemetrii danych tooblob magazynu.</span><span class="sxs-lookup"><span data-stu-id="5a2f5-260">hello solution uses hello ASA telemetry job toowrite hello telemetry data tooblob storage.</span></span>

### <a name="device-list"></a><span data-ttu-id="5a2f5-261">Lista urządzeń</span><span class="sxs-lookup"><span data-stu-id="5a2f5-261">Device list</span></span>

<span data-ttu-id="5a2f5-262">Na tej stronie w portalu rozwiązania hello można:</span><span class="sxs-lookup"><span data-stu-id="5a2f5-262">From this page in hello solution portal you can:</span></span>

* <span data-ttu-id="5a2f5-263">Aprowizacja nowego urządzenia.</span><span class="sxs-lookup"><span data-stu-id="5a2f5-263">Provision a new device.</span></span> <span data-ttu-id="5a2f5-264">Ta akcja określa hello Unikatowy identyfikator urządzenia i generuje klucz uwierzytelniania hello.</span><span class="sxs-lookup"><span data-stu-id="5a2f5-264">This action sets hello unique device id and generates hello authentication key.</span></span> <span data-ttu-id="5a2f5-265">Zapisuje informacje o hello urządzenia tooboth hello rejestru tożsamości Centrum IoT i hello określonego rozwiązania DB rozwiązania Cosmos w bazie danych.</span><span class="sxs-lookup"><span data-stu-id="5a2f5-265">It writes information about hello device tooboth hello IoT Hub identity registry and hello solution-specific Cosmos DB database.</span></span>
* <span data-ttu-id="5a2f5-266">Zarządzanie właściwościami urządzenia.</span><span class="sxs-lookup"><span data-stu-id="5a2f5-266">Manage device properties.</span></span> <span data-ttu-id="5a2f5-267">Ta czynność obejmuje wyświetlanie istniejących właściwości i aktualizowanie ich.</span><span class="sxs-lookup"><span data-stu-id="5a2f5-267">This action includes viewing existing properties and updating with new properties.</span></span>
* <span data-ttu-id="5a2f5-268">Wysyłanie poleceń tooa urządzenia.</span><span class="sxs-lookup"><span data-stu-id="5a2f5-268">Send commands tooa device.</span></span>
* <span data-ttu-id="5a2f5-269">Wyświetl historię poleceń hello urządzenia.</span><span class="sxs-lookup"><span data-stu-id="5a2f5-269">View hello command history for a device.</span></span>
* <span data-ttu-id="5a2f5-270">Włączanie i wyłączanie urządzeń.</span><span class="sxs-lookup"><span data-stu-id="5a2f5-270">Enable and disable devices.</span></span>

## <a name="next-steps"></a><span data-ttu-id="5a2f5-271">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="5a2f5-271">Next steps</span></span>

<span data-ttu-id="5a2f5-272">Witaj następujących wpisach w blogu TechNet zawierają więcej szczegółów na temat zdalnego wstępnie skonfigurowane rozwiązanie monitorujące hello:</span><span class="sxs-lookup"><span data-stu-id="5a2f5-272">hello following TechNet blog posts provide more detail about hello remote monitoring preconfigured solution:</span></span>

* [<span data-ttu-id="5a2f5-273">Monitorowanie zdalne Suite — w obszarze hello maską - IoT</span><span class="sxs-lookup"><span data-stu-id="5a2f5-273">IoT Suite - Under hello Hood - Remote Monitoring</span></span>](http://social.technet.microsoft.com/wiki/contents/articles/32941.iot-suite-under-the-hood-remote-monitoring.aspx)
* [<span data-ttu-id="5a2f5-274">IoT Suite - Remote Monitoring - Adding Live and Simulated Devices (Pakiet IoT — monitorowanie zdalne — dodawanie rzeczywistych i symulowanych urządzeń)</span><span class="sxs-lookup"><span data-stu-id="5a2f5-274">IoT Suite - Remote Monitoring - Adding Live and Simulated Devices</span></span>](http://social.technet.microsoft.com/wiki/contents/articles/32975.iot-suite-remote-monitoring-adding-live-and-simulated-devices.aspx)

<span data-ttu-id="5a2f5-275">Aby kontynuować, wprowadzenie pakiet IoT odczytując hello następujące artykuły:</span><span class="sxs-lookup"><span data-stu-id="5a2f5-275">You can continue getting started with IoT Suite by reading hello following articles:</span></span>

* <span data-ttu-id="5a2f5-276">[Połącz z toohello urządzenie zdalne monitorowanie wstępnie skonfigurowane rozwiązanie][lnk-connect-rm]</span><span class="sxs-lookup"><span data-stu-id="5a2f5-276">[Connect your device toohello remote monitoring preconfigured solution][lnk-connect-rm]</span></span>
* <span data-ttu-id="5a2f5-277">[Uprawnienia w witrynie azureiotsuite.com hello][lnk-permissions]</span><span class="sxs-lookup"><span data-stu-id="5a2f5-277">[Permissions on hello azureiotsuite.com site][lnk-permissions]</span></span>

[lnk-preconfigured-solutions]: iot-suite-what-are-preconfigured-solutions.md
[lnk-customize]: iot-suite-guidance-on-customizing-preconfigured-solutions.md
[lnk-iothub]: https://azure.microsoft.com/documentation/services/iot-hub/
[lnk-asa]: https://azure.microsoft.com/documentation/services/stream-analytics/
[lnk-webjobs]: https://azure.microsoft.com/documentation/articles/websites-webjobs-resources/
[lnk-connect-rm]: iot-suite-connecting-devices.md
[lnk-permissions]: iot-suite-permissions.md
[lnk-c2d-guidance]: ../iot-hub/iot-hub-devguide-c2d-guidance.md
[lnk-device-twins]:  ../iot-hub/iot-hub-devguide-device-twins.md
[lnk-direct-methods]: ../iot-hub/iot-hub-devguide-direct-methods.md
