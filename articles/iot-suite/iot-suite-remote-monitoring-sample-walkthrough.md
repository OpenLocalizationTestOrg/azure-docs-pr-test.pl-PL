---
title: "Przewodnik po wstępnie skonfigurowanym rozwiązaniu monitorowania zdalnego | Microsoft Docs"
description: "Opis wstępnie skonfigurowanego rozwiązania Azure IoT do monitorowania zdalnego wraz z informacjami dotyczącymi architektury rozwiązania."
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
ms.openlocfilehash: b28105f300723b542fa6d1aebc569439d5c73dc4
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
# <a name="remote-monitoring-preconfigured-solution-walkthrough"></a><span data-ttu-id="c8e80-103">Przewodnik po wstępnie skonfigurowanym rozwiązaniu monitorowania zdalnego</span><span class="sxs-lookup"><span data-stu-id="c8e80-103">Remote monitoring preconfigured solution walkthrough</span></span>

<span data-ttu-id="c8e80-104">[Wstępnie skonfigurowane rozwiązanie][lnk-preconfigured-solutions] do monitorowania zdalnego Pakietu IoT to implementacja kompleksowego rozwiązania do monitorowania wielu maszyn uruchomionych w lokalizacjach zdalnych.</span><span class="sxs-lookup"><span data-stu-id="c8e80-104">The IoT Suite remote monitoring [preconfigured solution][lnk-preconfigured-solutions] is an implementation of an end-to-end monitoring solution for multiple machines running in remote locations.</span></span> <span data-ttu-id="c8e80-105">Rozwiązanie to łączy najważniejsze usługi platformy Azure, aby umożliwić ogólną implementację scenariusza biznesowego.</span><span class="sxs-lookup"><span data-stu-id="c8e80-105">The solution combines key Azure services to provide a generic implementation of the business scenario.</span></span> <span data-ttu-id="c8e80-106">Możesz go użyć jako punktu wyjścia dla Twojej własnej implementacji i je [dostosować][lnk-customize], aby spełniało Twoje własne określone wymagania biznesowe.</span><span class="sxs-lookup"><span data-stu-id="c8e80-106">You can use the solution as a starting point for your own implementation and [customize][lnk-customize] it to meet your own specific business requirements.</span></span>

<span data-ttu-id="c8e80-107">Ten artykuł przeprowadzi Cię przez niektóre kluczowe elementy rozwiązania do monitorowania zdalnego, aby umożliwić Ci zrozumienie jego sposobu działania.</span><span class="sxs-lookup"><span data-stu-id="c8e80-107">This article walks you through some of the key elements of the remote monitoring solution to enable you to understand how it works.</span></span> <span data-ttu-id="c8e80-108">Ta wiedza ułatwi Ci:</span><span class="sxs-lookup"><span data-stu-id="c8e80-108">This knowledge helps you to:</span></span>

* <span data-ttu-id="c8e80-109">Rozwiązywanie problemów w rozwiązaniu.</span><span class="sxs-lookup"><span data-stu-id="c8e80-109">Troubleshoot issues in the solution.</span></span>
* <span data-ttu-id="c8e80-110">Planowanie sposobu dostosowywania rozwiązania, aby spełniało Twoje wymagania.</span><span class="sxs-lookup"><span data-stu-id="c8e80-110">Plan how to customize to the solution to meet your own specific requirements.</span></span> 
* <span data-ttu-id="c8e80-111">Projektowanie własnego rozwiązania IoT korzystającego z usług Azure.</span><span class="sxs-lookup"><span data-stu-id="c8e80-111">Design your own IoT solution that uses Azure services.</span></span>

## <a name="logical-architecture"></a><span data-ttu-id="c8e80-112">Architektura logiczna</span><span class="sxs-lookup"><span data-stu-id="c8e80-112">Logical architecture</span></span>

<span data-ttu-id="c8e80-113">Poniższy diagram przedstawia składniki logiczne wstępnie skonfigurowanego rozwiązania:</span><span class="sxs-lookup"><span data-stu-id="c8e80-113">The following diagram outlines the logical components of the preconfigured solution:</span></span>

![Architektura logiczna](media/iot-suite-remote-monitoring-sample-walkthrough/remote-monitoring-architecture.png)

## <a name="simulated-devices"></a><span data-ttu-id="c8e80-115">Symulowane urządzenia</span><span class="sxs-lookup"><span data-stu-id="c8e80-115">Simulated devices</span></span>

<span data-ttu-id="c8e80-116">W tym wstępnie skonfigurowanym rozwiązaniu symulowane urządzenie odpowiada urządzeniu chłodzącemu (np. klimatyzatorowi lub centrali wentylacyjnej w budynku).</span><span class="sxs-lookup"><span data-stu-id="c8e80-116">In the preconfigured solution, the simulated device represents a cooling device (such as a building air conditioner or facility air handling unit).</span></span> <span data-ttu-id="c8e80-117">Podczas wdrażania wstępnie skonfigurowanego rozwiązania przeprowadzisz też automatyczną aprowizację czterech symulowanych urządzeń działających w zadaniu [WebJob platformy Azure][lnk-webjobs].</span><span class="sxs-lookup"><span data-stu-id="c8e80-117">When you deploy the preconfigured solution, you also automatically provision four simulated devices that run in an [Azure WebJob][lnk-webjobs].</span></span> <span data-ttu-id="c8e80-118">Symulowane urządzenia ułatwiają badanie zachowania rozwiązania bez konieczności wdrażania jakichkolwiek urządzeń fizycznych.</span><span class="sxs-lookup"><span data-stu-id="c8e80-118">The simulated devices make it easy for you to explore the behavior of the solution without the need to deploy any physical devices.</span></span> <span data-ttu-id="c8e80-119">Aby wdrożyć rzeczywiste urządzenie fizyczne, zobacz samouczek [Łączenie urządzenia ze wstępnie skonfigurowanym rozwiązaniem do monitorowania zdalnego][lnk-connect-rm].</span><span class="sxs-lookup"><span data-stu-id="c8e80-119">To deploy a real physical device, see the [Connect your device to the remote monitoring preconfigured solution][lnk-connect-rm] tutorial.</span></span>

### <a name="device-to-cloud-messages"></a><span data-ttu-id="c8e80-120">Komunikaty z urządzenia do chmury</span><span class="sxs-lookup"><span data-stu-id="c8e80-120">Device-to-cloud messages</span></span>

<span data-ttu-id="c8e80-121">Każde symulowane urządzenie może wysyłać do usługi IoT Hub następujące typy wiadomości:</span><span class="sxs-lookup"><span data-stu-id="c8e80-121">Each simulated device can send the following message types to IoT Hub:</span></span>

| <span data-ttu-id="c8e80-122">Komunikat</span><span class="sxs-lookup"><span data-stu-id="c8e80-122">Message</span></span> | <span data-ttu-id="c8e80-123">Opis</span><span class="sxs-lookup"><span data-stu-id="c8e80-123">Description</span></span> |
| --- | --- |
| <span data-ttu-id="c8e80-124">Uruchamianie</span><span class="sxs-lookup"><span data-stu-id="c8e80-124">Startup</span></span> |<span data-ttu-id="c8e80-125">Po uruchomieniu urządzenie wysyła do zaplecza komunikat **device-info** zawierający informacje o tym urządzeniu.</span><span class="sxs-lookup"><span data-stu-id="c8e80-125">When the device starts, it sends a **device-info** message containing information about itself to the back end.</span></span> <span data-ttu-id="c8e80-126">Te dane obejmują identyfikator urządzenia oraz listę poleceń i metod obsługiwanych przez urządzenie.</span><span class="sxs-lookup"><span data-stu-id="c8e80-126">This data includes the device id and a list of the commands and methods the device supports.</span></span> |
| <span data-ttu-id="c8e80-127">Obecność</span><span class="sxs-lookup"><span data-stu-id="c8e80-127">Presence</span></span> |<span data-ttu-id="c8e80-128">Urządzenie okresowo wysyła komunikat **presence** w celu zgłoszenia, czy urządzenie może wykrywać obecność czujnika.</span><span class="sxs-lookup"><span data-stu-id="c8e80-128">A device periodically sends a **presence** message to report whether the device can sense the presence of a sensor.</span></span> |
| <span data-ttu-id="c8e80-129">Telemetria</span><span class="sxs-lookup"><span data-stu-id="c8e80-129">Telemetry</span></span> |<span data-ttu-id="c8e80-130">Urządzenie okresowo wysyła komunikat **telemetry**, który zgłasza symulowane wartości temperatury i wilgotności zebrane z symulowanych czujników urządzenia.</span><span class="sxs-lookup"><span data-stu-id="c8e80-130">A device periodically sends a **telemetry** message that reports simulated values for the temperature and humidity collected from the device's simulated sensors.</span></span> |

> [!NOTE]
> <span data-ttu-id="c8e80-131">Rozwiązanie przechowuje listę poleceń obsługiwanych przez urządzenie w bazie danych Cosmos DB, a nie w bliźniaczej reprezentacji urządzenia.</span><span class="sxs-lookup"><span data-stu-id="c8e80-131">The solution stores the list of commands supported by the device in a Cosmos DB database and not in the device twin.</span></span>

### <a name="properties-and-device-twins"></a><span data-ttu-id="c8e80-132">Właściwości i bliźniacze reprezentacje urządzeń</span><span class="sxs-lookup"><span data-stu-id="c8e80-132">Properties and device twins</span></span>

<span data-ttu-id="c8e80-133">Symulowane urządzenia wysyłają poniższe właściwości urządzenia do [bliźniaczej reprezentacji urządzenia][lnk-device-twins] w usłudze IoT Hub jako *zgłaszane właściwości*.</span><span class="sxs-lookup"><span data-stu-id="c8e80-133">The simulated devices send the following device properties to the [twin][lnk-device-twins] in the IoT hub as *reported properties*.</span></span> <span data-ttu-id="c8e80-134">Urządzenie wysyła zgłaszane właściwości podczas uruchamiania i w odpowiedzi na polecenie lub metodę **zmiany stanu urządzenia**.</span><span class="sxs-lookup"><span data-stu-id="c8e80-134">The device sends reported properties at startup and in response to a **Change Device State** command or method.</span></span>

| <span data-ttu-id="c8e80-135">Właściwość</span><span class="sxs-lookup"><span data-stu-id="c8e80-135">Property</span></span> | <span data-ttu-id="c8e80-136">Przeznaczenie</span><span class="sxs-lookup"><span data-stu-id="c8e80-136">Purpose</span></span> |
| --- | --- |
| <span data-ttu-id="c8e80-137">Config.TelemetryInterval</span><span class="sxs-lookup"><span data-stu-id="c8e80-137">Config.TelemetryInterval</span></span> | <span data-ttu-id="c8e80-138">Częstotliwość (w sekundach) wysłania przez urządzenie danych telemetrycznych</span><span class="sxs-lookup"><span data-stu-id="c8e80-138">Frequency (seconds) the device sends telemetry</span></span> |
| <span data-ttu-id="c8e80-139">Config.TemperatureMeanValue</span><span class="sxs-lookup"><span data-stu-id="c8e80-139">Config.TemperatureMeanValue</span></span> | <span data-ttu-id="c8e80-140">Określa średnią wartość symulowanych danych telemetrycznych dotyczących temperatury</span><span class="sxs-lookup"><span data-stu-id="c8e80-140">Specifies the mean value for the simulated temperature telemetry</span></span> |
| <span data-ttu-id="c8e80-141">Device.DeviceID</span><span class="sxs-lookup"><span data-stu-id="c8e80-141">Device.DeviceID</span></span> |<span data-ttu-id="c8e80-142">Ten identyfikator jest udostępniany lub przypisywany podczas tworzenia urządzenia w rozwiązaniu</span><span class="sxs-lookup"><span data-stu-id="c8e80-142">Id that is either provided or assigned when a device is created in the solution</span></span> |
| <span data-ttu-id="c8e80-143">Device.DeviceState</span><span class="sxs-lookup"><span data-stu-id="c8e80-143">Device.DeviceState</span></span> | <span data-ttu-id="c8e80-144">Stan raportowany przez urządzenie</span><span class="sxs-lookup"><span data-stu-id="c8e80-144">State reported by the device</span></span> |
| <span data-ttu-id="c8e80-145">Device.CreatedTime</span><span class="sxs-lookup"><span data-stu-id="c8e80-145">Device.CreatedTime</span></span> |<span data-ttu-id="c8e80-146">Czas utworzenia urządzenia w rozwiązaniu</span><span class="sxs-lookup"><span data-stu-id="c8e80-146">Time the device was created in the solution</span></span> |
| <span data-ttu-id="c8e80-147">Device.StartupTime</span><span class="sxs-lookup"><span data-stu-id="c8e80-147">Device.StartupTime</span></span> |<span data-ttu-id="c8e80-148">Czas uruchomienia urządzenia</span><span class="sxs-lookup"><span data-stu-id="c8e80-148">Time the device was started</span></span> |
| <span data-ttu-id="c8e80-149">Device.LastDesiredPropertyChange</span><span class="sxs-lookup"><span data-stu-id="c8e80-149">Device.LastDesiredPropertyChange</span></span> |<span data-ttu-id="c8e80-150">Numer wersji ostatniej zmiany żądanej właściwości</span><span class="sxs-lookup"><span data-stu-id="c8e80-150">The version number of the last desired property change</span></span> |
| <span data-ttu-id="c8e80-151">Device.Location.Latitude</span><span class="sxs-lookup"><span data-stu-id="c8e80-151">Device.Location.Latitude</span></span> |<span data-ttu-id="c8e80-152">Współrzędna szerokości geograficznej lokalizacji urządzenia</span><span class="sxs-lookup"><span data-stu-id="c8e80-152">Latitude location of the device</span></span> |
| <span data-ttu-id="c8e80-153">Device.Location.Longitude</span><span class="sxs-lookup"><span data-stu-id="c8e80-153">Device.Location.Longitude</span></span> |<span data-ttu-id="c8e80-154">Współrzędna długości geograficznej lokalizacji urządzenia</span><span class="sxs-lookup"><span data-stu-id="c8e80-154">Longitude location of the device</span></span> |
| <span data-ttu-id="c8e80-155">System.Manufacturer</span><span class="sxs-lookup"><span data-stu-id="c8e80-155">System.Manufacturer</span></span> |<span data-ttu-id="c8e80-156">Producent urządzenia</span><span class="sxs-lookup"><span data-stu-id="c8e80-156">Device manufacturer</span></span> |
| <span data-ttu-id="c8e80-157">System.ModelNumber</span><span class="sxs-lookup"><span data-stu-id="c8e80-157">System.ModelNumber</span></span> |<span data-ttu-id="c8e80-158">Numer modelu urządzenia</span><span class="sxs-lookup"><span data-stu-id="c8e80-158">Model number of the device</span></span> |
| <span data-ttu-id="c8e80-159">System.SerialNumber</span><span class="sxs-lookup"><span data-stu-id="c8e80-159">System.SerialNumber</span></span> |<span data-ttu-id="c8e80-160">Numer seryjny urządzenia</span><span class="sxs-lookup"><span data-stu-id="c8e80-160">Serial number of the device</span></span> |
| <span data-ttu-id="c8e80-161">System.FirmwareVersion</span><span class="sxs-lookup"><span data-stu-id="c8e80-161">System.FirmwareVersion</span></span> |<span data-ttu-id="c8e80-162">Bieżąca wersja oprogramowania układowego na urządzeniu</span><span class="sxs-lookup"><span data-stu-id="c8e80-162">Current version of firmware on the device</span></span> |
| <span data-ttu-id="c8e80-163">System.Platform</span><span class="sxs-lookup"><span data-stu-id="c8e80-163">System.Platform</span></span> |<span data-ttu-id="c8e80-164">Architektura platformy urządzenia</span><span class="sxs-lookup"><span data-stu-id="c8e80-164">Platform architecture of the device</span></span> |
| <span data-ttu-id="c8e80-165">System.Processor</span><span class="sxs-lookup"><span data-stu-id="c8e80-165">System.Processor</span></span> |<span data-ttu-id="c8e80-166">Procesor działający w urządzeniu</span><span class="sxs-lookup"><span data-stu-id="c8e80-166">Processor running the device</span></span> |
| <span data-ttu-id="c8e80-167">System.InstalledRAM</span><span class="sxs-lookup"><span data-stu-id="c8e80-167">System.InstalledRAM</span></span> |<span data-ttu-id="c8e80-168">Ilość pamięci RAM zainstalowanej w urządzeniu</span><span class="sxs-lookup"><span data-stu-id="c8e80-168">Amount of RAM installed on the device</span></span> |

<span data-ttu-id="c8e80-169">W symulowanych urządzeniach te właściwości są wypełniane przykładowymi wartościami.</span><span class="sxs-lookup"><span data-stu-id="c8e80-169">The simulator seeds these properties in simulated devices with sample values.</span></span> <span data-ttu-id="c8e80-170">Za każdym razem, gdy symulator inicjuje symulowane urządzenie, raportuje ono wstępnie zdefiniowane metadane do usługi IoT Hub jako zgłaszane właściwości.</span><span class="sxs-lookup"><span data-stu-id="c8e80-170">Each time the simulator initializes a simulated device, the device reports the pre-defined metadata to IoT Hub as reported properties.</span></span> <span data-ttu-id="c8e80-171">Zgłaszane właściwości mogą być aktualizowane tylko przez urządzenie.</span><span class="sxs-lookup"><span data-stu-id="c8e80-171">Reported properties can only be updated by the device.</span></span> <span data-ttu-id="c8e80-172">Aby zmienić zgłoszoną właściwość, należy ustawić żądaną właściwość w portalu rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="c8e80-172">To change a reported property, you set a desired property in solution portal.</span></span> <span data-ttu-id="c8e80-173">Na urządzeniu są wykonywane następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="c8e80-173">It is the responsibility of the device to:</span></span>

1. <span data-ttu-id="c8e80-174">Okresowe pobieranie żądanych właściwości z usługi IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="c8e80-174">Periodically retrieve desired properties from the IoT hub.</span></span>
2. <span data-ttu-id="c8e80-175">Aktualizowanie swojej konfiguracji wartością żądanej właściwości.</span><span class="sxs-lookup"><span data-stu-id="c8e80-175">Update its configuration with the desired property value.</span></span>
3. <span data-ttu-id="c8e80-176">Wysyłanie nowej wartości z powrotem do usługi IoT Hub jako zgłaszanej właściwości.</span><span class="sxs-lookup"><span data-stu-id="c8e80-176">Send the new value back to the hub as a reported property.</span></span>

<span data-ttu-id="c8e80-177">Z poziomu pulpitu nawigacyjnego rozwiązania możesz używać *żądanych właściwości* do ustawiania właściwości na urządzeniu za pomocą [bliźniaczej reprezentacji urządzenia][lnk-device-twins].</span><span class="sxs-lookup"><span data-stu-id="c8e80-177">From the solution dashboard, you can use *desired properties* to set properties on a device by using the [device twin][lnk-device-twins].</span></span> <span data-ttu-id="c8e80-178">Zwykle urządzenie odczytuje wartość żądanej właściwości z usługi IoT Hub w celu zaktualizowania swojego stanu wewnętrznego i zgłoszenia tej zmiany z powrotem jako zgłaszanej właściwości.</span><span class="sxs-lookup"><span data-stu-id="c8e80-178">Typically, a device reads a desired property value from the hub to update its internal state and report the change back as a reported property.</span></span>

> [!NOTE]
> <span data-ttu-id="c8e80-179">W kodzie na symulowanym urządzeniu są używane wyłącznie żądane właściwości **Desired.Config.TemperatureMeanValue** i **Desired.Config.TelemetryInterval** do aktualizowania zgłaszanych właściwości wysyłanych z powrotem do usługi IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="c8e80-179">The simulated device code only uses the **Desired.Config.TemperatureMeanValue** and **Desired.Config.TelemetryInterval** desired properties to update the reported properties sent back to IoT Hub.</span></span> <span data-ttu-id="c8e80-180">Wszystkie inne żądania zmiany żądanych właściwości są ignorowane na symulowanym urządzeniu.</span><span class="sxs-lookup"><span data-stu-id="c8e80-180">All other desired property change requests are ignored in the simulated device.</span></span>

### <a name="methods"></a><span data-ttu-id="c8e80-181">Metody</span><span class="sxs-lookup"><span data-stu-id="c8e80-181">Methods</span></span>

<span data-ttu-id="c8e80-182">Symulowane urządzenia obsługują następujące metody ([metody bezpośrednie][lnk-direct-methods]) wywoływane z poziomu portalu rozwiązania za pomocą usługi IoT Hub:</span><span class="sxs-lookup"><span data-stu-id="c8e80-182">The simulated devices can handle the following methods ([direct methods][lnk-direct-methods]) invoked from the solution portal through the IoT hub:</span></span>

| <span data-ttu-id="c8e80-183">Metoda</span><span class="sxs-lookup"><span data-stu-id="c8e80-183">Method</span></span> | <span data-ttu-id="c8e80-184">Opis</span><span class="sxs-lookup"><span data-stu-id="c8e80-184">Description</span></span> |
| --- | --- |
| <span data-ttu-id="c8e80-185">InitiateFirmwareUpdate</span><span class="sxs-lookup"><span data-stu-id="c8e80-185">InitiateFirmwareUpdate</span></span> |<span data-ttu-id="c8e80-186">Powoduje, że urządzenie przeprowadza aktualizację oprogramowania układowego</span><span class="sxs-lookup"><span data-stu-id="c8e80-186">Instructs the device to perform a firmware update</span></span> |
| <span data-ttu-id="c8e80-187">Ponowne uruchamianie</span><span class="sxs-lookup"><span data-stu-id="c8e80-187">Reboot</span></span> |<span data-ttu-id="c8e80-188">Powoduje ponowne uruchomienie urządzenia</span><span class="sxs-lookup"><span data-stu-id="c8e80-188">Instructs the device to reboot</span></span> |
| <span data-ttu-id="c8e80-189">FactoryReset</span><span class="sxs-lookup"><span data-stu-id="c8e80-189">FactoryReset</span></span> |<span data-ttu-id="c8e80-190">Powoduje, że na urządzeniu są przywracane ustawienia fabryczne</span><span class="sxs-lookup"><span data-stu-id="c8e80-190">Instructs the device to perform a factory reset</span></span> |

<span data-ttu-id="c8e80-191">Niektóre metody używają zgłaszanych właściwości do raportowania postępu.</span><span class="sxs-lookup"><span data-stu-id="c8e80-191">Some methods use reported properties to report on progress.</span></span> <span data-ttu-id="c8e80-192">Na przykład metoda **InitiateFirmwareUpdate** symuluje asynchroniczne uruchomienie aktualizacji na urządzeniu.</span><span class="sxs-lookup"><span data-stu-id="c8e80-192">For example, the **InitiateFirmwareUpdate** method simulates running the update asynchronously on the device.</span></span> <span data-ttu-id="c8e80-193">Efekty tej metody występują bezpośrednio na urządzeniu, natomiast zadanie asynchroniczne nadal wysyła aktualizacje stanu z powrotem na pulpit nawigacyjny rozwiązania za pomocą zgłaszanych właściwości.</span><span class="sxs-lookup"><span data-stu-id="c8e80-193">The method returns immediately on the device, while the asynchronous task continues to send status updates back to the solution dashboard using reported properties.</span></span>

### <a name="commands"></a><span data-ttu-id="c8e80-194">Polecenia</span><span class="sxs-lookup"><span data-stu-id="c8e80-194">Commands</span></span>

<span data-ttu-id="c8e80-195">Symulowane urządzenia obsługują następujące polecenia (komunikaty z chmury do urządzenia) wysyłane z portalu rozwiązania za pośrednictwem usługi IoT Hub:</span><span class="sxs-lookup"><span data-stu-id="c8e80-195">The simulated devices can handle the following commands (cloud-to-device messages) sent from the solution portal through the IoT hub:</span></span>

| <span data-ttu-id="c8e80-196">Polecenie</span><span class="sxs-lookup"><span data-stu-id="c8e80-196">Command</span></span> | <span data-ttu-id="c8e80-197">Opis</span><span class="sxs-lookup"><span data-stu-id="c8e80-197">Description</span></span> |
| --- | --- |
| <span data-ttu-id="c8e80-198">PingDevice</span><span class="sxs-lookup"><span data-stu-id="c8e80-198">PingDevice</span></span> |<span data-ttu-id="c8e80-199">Sprawdza, czy urządzenie jest aktywne, za pomocą polecenia *ping*.</span><span class="sxs-lookup"><span data-stu-id="c8e80-199">Sends a *ping* to the device to check it is alive</span></span> |
| <span data-ttu-id="c8e80-200">StartTelemetry</span><span class="sxs-lookup"><span data-stu-id="c8e80-200">StartTelemetry</span></span> |<span data-ttu-id="c8e80-201">Włącza przesyłanie danych telemetrycznych przez urządzenie.</span><span class="sxs-lookup"><span data-stu-id="c8e80-201">Starts the device sending telemetry</span></span> |
| <span data-ttu-id="c8e80-202">StopTelemetry</span><span class="sxs-lookup"><span data-stu-id="c8e80-202">StopTelemetry</span></span> |<span data-ttu-id="c8e80-203">Wyłącza przesyłanie danych telemetrycznych przez urządzenie.</span><span class="sxs-lookup"><span data-stu-id="c8e80-203">Stops the device from sending telemetry</span></span> |
| <span data-ttu-id="c8e80-204">ChangeSetPointTemp</span><span class="sxs-lookup"><span data-stu-id="c8e80-204">ChangeSetPointTemp</span></span> |<span data-ttu-id="c8e80-205">Zmienia ustaloną wartość, na podstawie której są generowane dane losowe.</span><span class="sxs-lookup"><span data-stu-id="c8e80-205">Changes the set point value around which the random data is generated</span></span> |
| <span data-ttu-id="c8e80-206">DiagnosticTelemetry</span><span class="sxs-lookup"><span data-stu-id="c8e80-206">DiagnosticTelemetry</span></span> |<span data-ttu-id="c8e80-207">Włącza wysyłanie dodatkowej wartości telemetrycznej (externalTemp — temperatura zewnętrzna) przez symulator urządzenia.</span><span class="sxs-lookup"><span data-stu-id="c8e80-207">Triggers the device simulator to send an additional telemetry value (externalTemp)</span></span> |
| <span data-ttu-id="c8e80-208">ChangeDeviceState</span><span class="sxs-lookup"><span data-stu-id="c8e80-208">ChangeDeviceState</span></span> |<span data-ttu-id="c8e80-209">Zmienia właściwość rozszerzonego stanu urządzenia i wysyła komunikat z informacjami o urządzeniu.</span><span class="sxs-lookup"><span data-stu-id="c8e80-209">Changes an extended state property for the device and sends the device info message from the device</span></span> |

> [!NOTE]
> <span data-ttu-id="c8e80-210">Porównanie tych poleceń (komunikatów wysyłanych z chmury do urządzenia) i metod (metod bezpośrednich) znajduje się w temacie [Wskazówki dotyczące komunikacji z chmury do urządzenia][lnk-c2d-guidance].</span><span class="sxs-lookup"><span data-stu-id="c8e80-210">For a comparison of these commands (cloud-to-device messages) and methods (direct methods), see [Cloud-to-device communications guidance][lnk-c2d-guidance].</span></span>

## <a name="iot-hub"></a><span data-ttu-id="c8e80-211">Usługa IoT Hub</span><span class="sxs-lookup"><span data-stu-id="c8e80-211">IoT Hub</span></span>

<span data-ttu-id="c8e80-212">Usługa [IoT Hub][lnk-iothub] pozyskuje dane wysyłane z urządzeń do chmury i udostępnia je zadaniom usługi Azure Stream Analytics (ASA).</span><span class="sxs-lookup"><span data-stu-id="c8e80-212">The [IoT hub][lnk-iothub] ingests data sent from the devices into the cloud and makes it available to the Azure Stream Analytics (ASA) jobs.</span></span> <span data-ttu-id="c8e80-213">Każde zadanie strumieniowe ASA odczytuje strumień komunikatów z urządzeń przy użyciu osobnej grupy konsumentów usługi IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="c8e80-213">Each stream ASA job uses a separate IoT Hub consumer group to read the stream of messages from your devices.</span></span>

<span data-ttu-id="c8e80-214">Usługa IoT Hub w rozwiązaniu wykonuje ponadto następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="c8e80-214">The IoT hub in the solution also:</span></span>

- <span data-ttu-id="c8e80-215">Obsługuje rejestr tożsamości, w którym są przechowywane identyfikatory i klucze uwierzytelniania wszystkich urządzeń z uprawnieniami do nawiązywania połączeń z portalem.</span><span class="sxs-lookup"><span data-stu-id="c8e80-215">Maintains an identity registry that stores the ids and authentication keys of all the devices permitted to connect to the portal.</span></span> <span data-ttu-id="c8e80-216">Za pomocą rejestru tożsamości możesz włączać i wyłączać urządzenia.</span><span class="sxs-lookup"><span data-stu-id="c8e80-216">You can enable and disable devices through the identity registry.</span></span>
- <span data-ttu-id="c8e80-217">Wysyła polecenia do Twoich urządzeń w imieniu portalu rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="c8e80-217">Sends commands to your devices on behalf of the solution portal.</span></span>
- <span data-ttu-id="c8e80-218">Wywołuje metody na Twoich urządzeniach w imieniu portalu rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="c8e80-218">Invokes methods on your devices on behalf of the solution portal.</span></span>
- <span data-ttu-id="c8e80-219">Obsługuje bliźniacze reprezentacje wszystkich zarejestrowanych urządzeń.</span><span class="sxs-lookup"><span data-stu-id="c8e80-219">Maintains device twins for all registered devices.</span></span> <span data-ttu-id="c8e80-220">W bliźniaczej reprezentacji urządzenia są przechowywane wartości właściwości zgłaszanych przez urządzenie.</span><span class="sxs-lookup"><span data-stu-id="c8e80-220">A device twin stores the property values reported by a device.</span></span> <span data-ttu-id="c8e80-221">W bliźniaczej reprezentacji urządzenia są także przechowywane żądane właściwości ustawione w portalu rozwiązania, które mają zostać pobrane przez urządzanie podczas nawiązywania następnego połączenia.</span><span class="sxs-lookup"><span data-stu-id="c8e80-221">A device twin also stores desired properties, set in the solution portal, for the device to retrieve when it next connects.</span></span>
- <span data-ttu-id="c8e80-222">Planuje zadania ustawiania właściwości dla wielu urządzeń lub wywoływania metod na wielu urządzeniach.</span><span class="sxs-lookup"><span data-stu-id="c8e80-222">Schedules jobs to set properties for multiple devices or invoke methods on multiple devices.</span></span>

## <a name="azure-stream-analytics"></a><span data-ttu-id="c8e80-223">Usługa Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="c8e80-223">Azure Stream Analytics</span></span>

<span data-ttu-id="c8e80-224">W rozwiązaniu do monitorowania zdalnego usługa [Azure Stream Analytics][lnk-asa] (ASA) wysyła komunikaty urządzeń odebrane przez usługę IoT Hub do innych składników zaplecza w celu ich przetwarzania lub magazynowania.</span><span class="sxs-lookup"><span data-stu-id="c8e80-224">In the remote monitoring solution, [Azure Stream Analytics][lnk-asa] (ASA) dispatches device messages received by the IoT hub to other back-end components for processing or storage.</span></span> <span data-ttu-id="c8e80-225">Różne zadania ASA pełnią określone funkcje w zależności od zawartości komunikatów.</span><span class="sxs-lookup"><span data-stu-id="c8e80-225">Different ASA jobs perform specific functions based on the content of the messages.</span></span>

<span data-ttu-id="c8e80-226">**Zadanie 1: Informacje o urządzeniu** odfiltrowuje komunikaty z informacjami o urządzeniu ze strumienia komunikatów przychodzących i wysyła je do punktu końcowego Centrum zdarzeń.</span><span class="sxs-lookup"><span data-stu-id="c8e80-226">**Job 1: Device Info** filters device information messages from the incoming message stream and sends them to an Event Hub endpoint.</span></span> <span data-ttu-id="c8e80-227">Komunikat z informacjami o urządzeniu jest wysyłany podczas uruchamiania urządzenia oraz w odpowiedzi na polecenie **SendDeviceInfo**.</span><span class="sxs-lookup"><span data-stu-id="c8e80-227">A device sends device information messages at startup and in response to a **SendDeviceInfo** command.</span></span> <span data-ttu-id="c8e80-228">To zadanie identyfikuje komunikaty **device-info** przy użyciu następującej definicji zapytania:</span><span class="sxs-lookup"><span data-stu-id="c8e80-228">This job uses the following query definition to identify **device-info** messages:</span></span>

```
SELECT * FROM DeviceDataStream Partition By PartitionId WHERE  ObjectType = 'DeviceInfo'
```

<span data-ttu-id="c8e80-229">To zadanie wysyła dane wyjściowe do centrum zdarzeń w celu dalszego przetwarzania.</span><span class="sxs-lookup"><span data-stu-id="c8e80-229">This job sends its output to an Event Hub for further processing.</span></span>

<span data-ttu-id="c8e80-230">**Zadanie 2: Reguły** porównuje przychodzące dane telemetryczne dotyczące temperatury i wilgotności z wartościami progowymi określonymi dla urządzenia.</span><span class="sxs-lookup"><span data-stu-id="c8e80-230">**Job 2: Rules** evaluates incoming temperature and humidity telemetry values against per-device thresholds.</span></span> <span data-ttu-id="c8e80-231">Wartości progowe są ustawiane za pomocą edytora reguł dostępnego w portalu rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="c8e80-231">Threshold values are set in the rules editor available in the solution portal.</span></span> <span data-ttu-id="c8e80-232">Poszczególne pary urządzenie/wartość są uporządkowane według sygnatur czasowych i przechowywane w obiekcie blob, który jest odczytywany przez usługę Stream Analytics jako **dane referencyjne**.</span><span class="sxs-lookup"><span data-stu-id="c8e80-232">Each device/value pair is stored by timestamp in a blob which Stream Analytics reads in as **Reference Data**.</span></span> <span data-ttu-id="c8e80-233">W ramach zadania wszystkie niepuste wartości są porównywane względem progu ustalonego dla urządzenia.</span><span class="sxs-lookup"><span data-stu-id="c8e80-233">The job compares any non-empty value against the set threshold for the device.</span></span> <span data-ttu-id="c8e80-234">W przypadku przekroczenia warunku „>” zadanie generuje zdarzenie **alarmu** dotyczące przekroczenia wartości progowej, które udostępnia dane o urządzeniu, wartości i sygnaturze czasowej.</span><span class="sxs-lookup"><span data-stu-id="c8e80-234">If it exceeds the '>' condition, the job outputs an **alarm** event that indicates that the threshold is exceeded and provides the device, value, and timestamp values.</span></span> <span data-ttu-id="c8e80-235">To zadanie identyfikuje komunikaty telemetryczne, które powinny wyzwolić alarm, przy użyciu następującej definicji zapytania:</span><span class="sxs-lookup"><span data-stu-id="c8e80-235">This job uses the following query definition to identify telemetry messages that should trigger an alarm:</span></span>

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

<span data-ttu-id="c8e80-236">Zadanie wysyła dane wyjściowe do centrum zdarzeń w celu dalszego przetwarzania i zapisuje szczegóły każdego alertu w magazynie obiektów blob, z którego portal rozwiązania może odczytać informacje o alertach.</span><span class="sxs-lookup"><span data-stu-id="c8e80-236">The job sends its output to an Event Hub for further processing and saves details of each alert to blob storage from where the solution portal can read the alert information.</span></span>

<span data-ttu-id="c8e80-237">**Zadanie 3: Telemetria** przetwarza strumień przychodzących z urządzeń danych telemetrycznych przy użyciu dwóch procedur.</span><span class="sxs-lookup"><span data-stu-id="c8e80-237">**Job 3: Telemetry** operates on the incoming device telemetry stream in two ways.</span></span> <span data-ttu-id="c8e80-238">Pierwsza z nich przesyła wszystkie komunikaty telemetryczne z urządzeń do trwałego magazynu obiektów blob w celu ich długotrwałego przechowywania.</span><span class="sxs-lookup"><span data-stu-id="c8e80-238">The first sends all telemetry messages from the devices to persistent blob storage for long-term storage.</span></span> <span data-ttu-id="c8e80-239">Druga procedura wyznacza średnią, minimalną i maksymalną wartość wilgotności w ramach przesuwającego się okna czasowego o wielkości pięciu minut i wysyła te dane do magazynu obiektów blob.</span><span class="sxs-lookup"><span data-stu-id="c8e80-239">The second computes average, minimum, and maximum humidity values over a five-minute sliding window and sends this data to blob storage.</span></span> <span data-ttu-id="c8e80-240">Portal rozwiązania odczytuje dane telemetryczne z magazynu obiektów blob w celu wypełnienia wykresów.</span><span class="sxs-lookup"><span data-stu-id="c8e80-240">The solution portal reads the telemetry data from blob storage to populate the charts.</span></span> <span data-ttu-id="c8e80-241">W tym zadaniu jest używana następująca definicja zapytania:</span><span class="sxs-lookup"><span data-stu-id="c8e80-241">This job uses the following query definition:</span></span>

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

## <a name="event-hubs"></a><span data-ttu-id="c8e80-242">Usługa Event Hubs</span><span class="sxs-lookup"><span data-stu-id="c8e80-242">Event Hubs</span></span>

<span data-ttu-id="c8e80-243">Zadania ASA **informacje o urządzeniu** i **reguły** przesyłają dane wyjściowe do centrum zdarzeń w celu ich niezawodnego przekazania do **procesora zdarzeń** uruchomionego w zadaniu WebJob.</span><span class="sxs-lookup"><span data-stu-id="c8e80-243">The **device info** and **rules** ASA jobs output their data to Event Hubs to reliably forward on to the **Event Processor** running in the WebJob.</span></span>

## <a name="azure-storage"></a><span data-ttu-id="c8e80-244">Azure Storage</span><span class="sxs-lookup"><span data-stu-id="c8e80-244">Azure storage</span></span>

<span data-ttu-id="c8e80-245">Rozwiązanie korzysta z magazynu obiektów blob platformy Azure, aby utrwalić wszystkie nieprzetworzone i podsumowane dane telemetryczne z urządzeń w rozwiązaniu.</span><span class="sxs-lookup"><span data-stu-id="c8e80-245">The solution uses Azure blob storage to persist all the raw and summarized telemetry data from the devices in the solution.</span></span> <span data-ttu-id="c8e80-246">Portal odczytuje dane telemetryczne z magazynu obiektów blob w celu wypełnienia wykresów.</span><span class="sxs-lookup"><span data-stu-id="c8e80-246">The portal reads the telemetry data from blob storage to populate the charts.</span></span> <span data-ttu-id="c8e80-247">Aby wyświetlić alerty, portal rozwiązania odczytuje dane z magazynu obiektów blob, który rejestruje, kiedy wartości telemetryczne przekraczają skonfigurowane wartości progowe.</span><span class="sxs-lookup"><span data-stu-id="c8e80-247">To display alerts, the solution portal reads the data from blob storage that records when telemetry values exceeded the configured threshold values.</span></span> <span data-ttu-id="c8e80-248">Rozwiązanie używa również magazynu obiektów blob do rejestrowania wartości progowych określonych w portalu rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="c8e80-248">The solution also uses blob storage to record the threshold values you set in the solution portal.</span></span>

## <a name="webjobs"></a><span data-ttu-id="c8e80-249">Zadania WebJob</span><span class="sxs-lookup"><span data-stu-id="c8e80-249">WebJobs</span></span>

<span data-ttu-id="c8e80-250">Oprócz hostowania symulatorów urządzenia zadania WebJob w rozwiązaniu hostują także **procesor zdarzeń** uruchomiony w zadaniu WebJob platformy Azure, które obsługuje odpowiedzi na polecenia.</span><span class="sxs-lookup"><span data-stu-id="c8e80-250">In addition to hosting the device simulators, the WebJobs in the solution also host the **Event Processor** running in an Azure WebJob that handles command responses.</span></span> <span data-ttu-id="c8e80-251">Używa on komunikatów odpowiedzi na polecenia w celu aktualizacji historii poleceń urządzenia (przechowywanej w bazie danych Cosmos DB).</span><span class="sxs-lookup"><span data-stu-id="c8e80-251">It uses command response messages to update the device command history (stored in the Cosmos DB database).</span></span>

## <a name="cosmos-db"></a><span data-ttu-id="c8e80-252">Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="c8e80-252">Cosmos DB</span></span>

<span data-ttu-id="c8e80-253">Rozwiązanie przechowuje informacje o połączonych z nim urządzeniach w bazie danych Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="c8e80-253">The solution uses a Cosmos DB database to store information about the devices connected to the solution.</span></span> <span data-ttu-id="c8e80-254">Te informacje uwzględniają historię poleceń wysłanych do urządzeń z portalu rozwiązania i metod wywołanych z portalu rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="c8e80-254">This information includes the history of commands sent to devices from the solution portal and of methods invoked from the solution portal.</span></span>

## <a name="solution-portal"></a><span data-ttu-id="c8e80-255">Portal rozwiązania</span><span class="sxs-lookup"><span data-stu-id="c8e80-255">Solution portal</span></span>

<span data-ttu-id="c8e80-256">Portal rozwiązania to aplikacja sieci Web wdrożona w ramach wstępnie skonfigurowanego rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="c8e80-256">The solution portal is a web app deployed as part of the preconfigured solution.</span></span> <span data-ttu-id="c8e80-257">Najważniejsze strony w portalu rozwiązania to pulpit nawigacyjny i lista urządzeń.</span><span class="sxs-lookup"><span data-stu-id="c8e80-257">The key pages in the solution portal are the dashboard and the device list.</span></span>

### <a name="dashboard"></a><span data-ttu-id="c8e80-258">Pulpit nawigacyjny</span><span class="sxs-lookup"><span data-stu-id="c8e80-258">Dashboard</span></span>

<span data-ttu-id="c8e80-259">Na tej stronie aplikacji sieci Web są używane kontrolki JavaScript usługi Power BI (zobacz [repozytorium PowerBI-visuals](https://www.github.com/Microsoft/PowerBI-visuals)), które umożliwiają wizualizację danych telemetrycznych z urządzeń.</span><span class="sxs-lookup"><span data-stu-id="c8e80-259">This page in the web app uses PowerBI javascript controls (See [PowerBI-visuals repo](https://www.github.com/Microsoft/PowerBI-visuals)) to visualize the telemetry data from the devices.</span></span> <span data-ttu-id="c8e80-260">Rozwiązanie zapisuje dane telemetryczne w magazynie obiektów blob, używając zadań telemetrii usługi ASA.</span><span class="sxs-lookup"><span data-stu-id="c8e80-260">The solution uses the ASA telemetry job to write the telemetry data to blob storage.</span></span>

### <a name="device-list"></a><span data-ttu-id="c8e80-261">Lista urządzeń</span><span class="sxs-lookup"><span data-stu-id="c8e80-261">Device list</span></span>

<span data-ttu-id="c8e80-262">Na tej stronie w portalu rozwiązania możesz wykonywać następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="c8e80-262">From this page in the solution portal you can:</span></span>

* <span data-ttu-id="c8e80-263">Aprowizacja nowego urządzenia.</span><span class="sxs-lookup"><span data-stu-id="c8e80-263">Provision a new device.</span></span> <span data-ttu-id="c8e80-264">Ta czynność obejmuje określenie unikatowego identyfikatora urządzenia i wygenerowanie klucza uwierzytelniania.</span><span class="sxs-lookup"><span data-stu-id="c8e80-264">This action sets the unique device id and generates the authentication key.</span></span> <span data-ttu-id="c8e80-265">Zapisuje ona informacje o urządzeniu w rejestrze tożsamości usługi IoT Hub oraz w bazie danych Cosmos DB określonego rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="c8e80-265">It writes information about the device to both the IoT Hub identity registry and the solution-specific Cosmos DB database.</span></span>
* <span data-ttu-id="c8e80-266">Zarządzanie właściwościami urządzenia.</span><span class="sxs-lookup"><span data-stu-id="c8e80-266">Manage device properties.</span></span> <span data-ttu-id="c8e80-267">Ta czynność obejmuje wyświetlanie istniejących właściwości i aktualizowanie ich.</span><span class="sxs-lookup"><span data-stu-id="c8e80-267">This action includes viewing existing properties and updating with new properties.</span></span>
* <span data-ttu-id="c8e80-268">Wysyłanie poleceń do urządzenia.</span><span class="sxs-lookup"><span data-stu-id="c8e80-268">Send commands to a device.</span></span>
* <span data-ttu-id="c8e80-269">Wyświetlanie historii poleceń dla urządzenia.</span><span class="sxs-lookup"><span data-stu-id="c8e80-269">View the command history for a device.</span></span>
* <span data-ttu-id="c8e80-270">Włączanie i wyłączanie urządzeń.</span><span class="sxs-lookup"><span data-stu-id="c8e80-270">Enable and disable devices.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c8e80-271">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="c8e80-271">Next steps</span></span>

<span data-ttu-id="c8e80-272">Następujące wpisy na blogu w witrynie TechNet zawierają więcej informacji dotyczących wstępnie skonfigurowanego rozwiązania do monitorowania zdalnego:</span><span class="sxs-lookup"><span data-stu-id="c8e80-272">The following TechNet blog posts provide more detail about the remote monitoring preconfigured solution:</span></span>

* [<span data-ttu-id="c8e80-273">IoT Suite - Under The Hood - Remote Monitoring (Za kulisami pakietu IoT — monitorowanie zdalne)</span><span class="sxs-lookup"><span data-stu-id="c8e80-273">IoT Suite - Under The Hood - Remote Monitoring</span></span>](http://social.technet.microsoft.com/wiki/contents/articles/32941.iot-suite-under-the-hood-remote-monitoring.aspx)
* [<span data-ttu-id="c8e80-274">IoT Suite - Remote Monitoring - Adding Live and Simulated Devices (Pakiet IoT — monitorowanie zdalne — dodawanie rzeczywistych i symulowanych urządzeń)</span><span class="sxs-lookup"><span data-stu-id="c8e80-274">IoT Suite - Remote Monitoring - Adding Live and Simulated Devices</span></span>](http://social.technet.microsoft.com/wiki/contents/articles/32975.iot-suite-remote-monitoring-adding-live-and-simulated-devices.aspx)

<span data-ttu-id="c8e80-275">Możesz kontynuować poznawanie Pakietu IoT, czytając następujące artykuły:</span><span class="sxs-lookup"><span data-stu-id="c8e80-275">You can continue getting started with IoT Suite by reading the following articles:</span></span>

* <span data-ttu-id="c8e80-276">[Łączenie urządzenia ze wstępnie skonfigurowanym rozwiązaniem do monitorowania zdalnego][lnk-connect-rm]</span><span class="sxs-lookup"><span data-stu-id="c8e80-276">[Connect your device to the remote monitoring preconfigured solution][lnk-connect-rm]</span></span>
* <span data-ttu-id="c8e80-277">[Uprawnienia w witrynie azureiotsuite.com][lnk-permissions]</span><span class="sxs-lookup"><span data-stu-id="c8e80-277">[Permissions on the azureiotsuite.com site][lnk-permissions]</span></span>

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
