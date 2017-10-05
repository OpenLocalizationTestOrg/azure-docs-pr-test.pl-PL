---
title: "Zrozumienie twins urządzenia Azure IoT Hub | Dokumentacja firmy Microsoft"
description: "Przewodnik dewelopera - Użyj twins urządzenia do synchronizacji danych stanu i konfiguracji między centrum IoT i urządzeniami"
services: iot-hub
documentationcenter: .net
author: fsautomata
manager: timlt
editor: 
ms.assetid: 8a3da072-a5bf-46e5-8de4-24cdbb2a03fa
ms.service: iot-hub
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/24/2017
ms.author: elioda
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: b316aa419d558547f90a914a22fb29935076de21
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
# <a name="understand-and-use-device-twins-in-iot-hub"></a><span data-ttu-id="e387b-103">W zrozumieniu i użytkowaniu twins urządzenie w Centrum IoT</span><span class="sxs-lookup"><span data-stu-id="e387b-103">Understand and use device twins in IoT Hub</span></span>
## <a name="overview"></a><span data-ttu-id="e387b-104">Omówienie</span><span class="sxs-lookup"><span data-stu-id="e387b-104">Overview</span></span>
<span data-ttu-id="e387b-105">*Urządzenie twins* są dokumentów JSON, w których są przechowywane informacje o stanie urządzenia (metadanych, konfiguracji i warunki).</span><span class="sxs-lookup"><span data-stu-id="e387b-105">*Device twins* are JSON documents that store device state information (metadata, configurations, and conditions).</span></span> <span data-ttu-id="e387b-106">Usługa IoT Hub utrzymuje bliźniaczą reprezentację urządzenia dla każdego urządzenia połączonego z usługą IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="e387b-106">IoT Hub persists a device twin for each device that you connect to IoT Hub.</span></span> <span data-ttu-id="e387b-107">W tym artykule opisano:</span><span class="sxs-lookup"><span data-stu-id="e387b-107">This article describes:</span></span>

* <span data-ttu-id="e387b-108">Struktura dwie urządzenia: *tagi*, *żądany* i *zgłosił właściwości*, i</span><span class="sxs-lookup"><span data-stu-id="e387b-108">The structure of the device twin: *tags*, *desired* and *reported properties*, and</span></span>
* <span data-ttu-id="e387b-109">Operacje, które aplikacje urządzenia i zaplecza, które można wykonywać na twins urządzenia.</span><span class="sxs-lookup"><span data-stu-id="e387b-109">The operations that device apps and back ends can perform on device twins.</span></span>

> [!NOTE]
> <span data-ttu-id="e387b-110">Obecnie twins urządzenia jest dostępny tylko w przypadku urządzeń łączących się za pomocą protokołu MQTT Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="e387b-110">Currently, device twins are accessible only from devices that connect to IoT Hub using the MQTT protocol.</span></span> <span data-ttu-id="e387b-111">Zapoznaj się [Obsługa MQTT] [ lnk-devguide-mqtt] artykułu instrukcje na temat do konwersji istniejącej aplikacji urządzenia do używania MQTT.</span><span class="sxs-lookup"><span data-stu-id="e387b-111">Refer to the [MQTT support][lnk-devguide-mqtt] article for instructions on how to convert existing device app to use MQTT.</span></span>
> 
> 

### <a name="when-to-use"></a><span data-ttu-id="e387b-112">Kiedy stosować</span><span class="sxs-lookup"><span data-stu-id="e387b-112">When to use</span></span>
<span data-ttu-id="e387b-113">Użyj twins urządzenia do:</span><span class="sxs-lookup"><span data-stu-id="e387b-113">Use device twins to:</span></span>

* <span data-ttu-id="e387b-114">Przechowywane metadane dotyczące urządzeń w chmurze.</span><span class="sxs-lookup"><span data-stu-id="e387b-114">Store device-specific metadata in the cloud.</span></span> <span data-ttu-id="e387b-115">Na przykład lokalizacja wdrożenia automaty maszyny.</span><span class="sxs-lookup"><span data-stu-id="e387b-115">For example, the deployment location of a vending machine.</span></span>
* <span data-ttu-id="e387b-116">Bieżący stan informacji w raporcie, takie jak dostępne możliwości i warunków z aplikacją urządzenia.</span><span class="sxs-lookup"><span data-stu-id="e387b-116">Report current state information such as available capabilities and conditions from your device app.</span></span> <span data-ttu-id="e387b-117">Na przykład urządzenie jest podłączone do Centrum IoT over komórkowej lub Wi-Fi.</span><span class="sxs-lookup"><span data-stu-id="e387b-117">For example, a device is connected to your IoT hub over cellular or WiFi.</span></span>
* <span data-ttu-id="e387b-118">Synchronizuj stan przepływów pracy, długotrwałą między aplikacją urządzenia i aplikacji zaplecza.</span><span class="sxs-lookup"><span data-stu-id="e387b-118">Synchronize the state of long-running workflows between device app and back-end app.</span></span> <span data-ttu-id="e387b-119">Na przykład podczas kopii rozwiązania zakończenia określa nowej wersji oprogramowania układowego do zainstalowania i aplikacji urządzenia raporty przez różne etapy procesu aktualizacji.</span><span class="sxs-lookup"><span data-stu-id="e387b-119">For example, when the solution back end specifies the new firmware version to install, and the device app reports the various stages of the update process.</span></span>
* <span data-ttu-id="e387b-120">Zapytanie z metadanych urządzeniami, konfiguracji lub stanu.</span><span class="sxs-lookup"><span data-stu-id="e387b-120">Query your device metadata, configuration, or state.</span></span>

<span data-ttu-id="e387b-121">Zapoznaj się [wskazówki komunikację urządzenia do chmury] [ lnk-d2c-guidance] wskazówki dotyczące przy użyciu właściwości zgłoszone, wiadomości urządzenia do chmury lub przekazywania pliku.</span><span class="sxs-lookup"><span data-stu-id="e387b-121">Refer to [Device-to-cloud communication guidance][lnk-d2c-guidance] for guidance on using reported properties, device-to-cloud messages, or file upload.</span></span>
<span data-ttu-id="e387b-122">Zapoznaj się [wskazówki dotyczące komunikacji chmury do urządzenia] [ lnk-c2d-guidance] wskazówki na temat używania żądanej właściwości, metody bezpośredniego lub komunikaty chmury do urządzenia.</span><span class="sxs-lookup"><span data-stu-id="e387b-122">Refer to [Cloud-to-device communication guidance][lnk-c2d-guidance] for guidance on using desired properties, direct methods, or cloud-to-device messages.</span></span>

## <a name="device-twins"></a><span data-ttu-id="e387b-123">Twins urządzenia</span><span class="sxs-lookup"><span data-stu-id="e387b-123">Device twins</span></span>
<span data-ttu-id="e387b-124">Urządzenia twins przechowywać informacje dotyczące urządzeń który:</span><span class="sxs-lookup"><span data-stu-id="e387b-124">Device twins store device-related information that:</span></span>

* <span data-ttu-id="e387b-125">Urządzenia i z powrotem kończy się służy do synchronizowania urządzenia warunki i konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="e387b-125">Device and back ends can use to synchronize device conditions and configuration.</span></span>
* <span data-ttu-id="e387b-126">Zaplecze rozwiązania służy do zapytań i docelowego długotrwałą operacji.</span><span class="sxs-lookup"><span data-stu-id="e387b-126">The solution back end can use to query and target long-running operations.</span></span>

<span data-ttu-id="e387b-127">Cykl życia dwie urządzenia jest połączony z odpowiadającego [tożsamości urządzenia][lnk-identity].</span><span class="sxs-lookup"><span data-stu-id="e387b-127">The lifecycle of a device twin is linked to the corresponding [device identity][lnk-identity].</span></span> <span data-ttu-id="e387b-128">Urządzenie twins niejawnie są tworzone i usuwane po utworzeniu lub usunięciu w Centrum IoT nowej tożsamości urządzenia.</span><span class="sxs-lookup"><span data-stu-id="e387b-128">Device twins are implicitly created and deleted when a new device identity is created or deleted in IoT Hub.</span></span>

<span data-ttu-id="e387b-129">Dwie urządzenia jest dokumentem JSON, który zawiera:</span><span class="sxs-lookup"><span data-stu-id="e387b-129">A device twin is a JSON document that includes:</span></span>

* <span data-ttu-id="e387b-130">**Tagi**.</span><span class="sxs-lookup"><span data-stu-id="e387b-130">**Tags**.</span></span> <span data-ttu-id="e387b-131">Sekcja zaplecza rozwiązania można odczytywać i zapisywać do dokumentu JSON.</span><span class="sxs-lookup"><span data-stu-id="e387b-131">A section of the JSON document that the solution back end can read from and write to.</span></span> <span data-ttu-id="e387b-132">Tagi nie są widoczne dla aplikacji dla urządzeń.</span><span class="sxs-lookup"><span data-stu-id="e387b-132">Tags are not visible to device apps.</span></span>
* <span data-ttu-id="e387b-133">**Żądany właściwości**.</span><span class="sxs-lookup"><span data-stu-id="e387b-133">**Desired properties**.</span></span> <span data-ttu-id="e387b-134">Używać razem z właściwości zgłoszony do synchronizowania konfiguracji urządzenia lub warunków.</span><span class="sxs-lookup"><span data-stu-id="e387b-134">Used along with reported properties to synchronize device configuration or conditions.</span></span> <span data-ttu-id="e387b-135">Żądane właściwości można ustawić tylko w rozwiązaniu wstecz zakończenia i może zostać odczytany przez aplikacji urządzenia.</span><span class="sxs-lookup"><span data-stu-id="e387b-135">Desired properties can only be set by the solution back end and can be read by the device app.</span></span> <span data-ttu-id="e387b-136">W czasie rzeczywistym o zmianach w odpowiednich właściwościach aplikacji urządzenia też być powiadamiani.</span><span class="sxs-lookup"><span data-stu-id="e387b-136">The device app can also be notified in real time of changes in the desired properties.</span></span>
* <span data-ttu-id="e387b-137">**Zgłoszone właściwości**.</span><span class="sxs-lookup"><span data-stu-id="e387b-137">**Reported properties**.</span></span> <span data-ttu-id="e387b-138">Umożliwia oraz odpowiednie właściwości synchronizacji konfiguracji urządzenia lub warunków.</span><span class="sxs-lookup"><span data-stu-id="e387b-138">Used along with desired properties to synchronize device configuration or conditions.</span></span> <span data-ttu-id="e387b-139">Zgłoszony właściwości można ustawić tylko za pomocą aplikacji urządzenia i można odczytywać i żądanych przez zaplecza rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="e387b-139">Reported properties can only be set by the device app and can be read and queried by the solution back end.</span></span>

<span data-ttu-id="e387b-140">Ponadto głównego dokumentu JSON dwie urządzenia zawiera właściwości tylko do odczytu z odpowiedniego tożsamości urządzenia przechowywany w [rejestru tożsamości][lnk-identity].</span><span class="sxs-lookup"><span data-stu-id="e387b-140">Additionally, the root of the device twin JSON document contains the read-only properties from the corresponding device identity stored in the [identity registry][lnk-identity].</span></span>

![][img-twin]

<span data-ttu-id="e387b-141">W poniższym przykładzie przedstawiono dwie urządzenia dokumentu JSON:</span><span class="sxs-lookup"><span data-stu-id="e387b-141">The following example shows a device twin JSON document:</span></span>

        {
            "deviceId": "devA",
            "generationId": "123",
            "status": "enabled",
            "statusReason": "provisioned",
            "connectionState": "connected",
            "connectionStateUpdatedTime": "2015-02-28T16:24:48.789Z",
            "lastActivityTime": "2015-02-30T16:24:48.789Z",

            "tags": {
                "$etag": "123",
                "deploymentLocation": {
                    "building": "43",
                    "floor": "1"
                }
            },
            "properties": {
                "desired": {
                    "telemetryConfig": {
                        "sendFrequency": "5m"
                    },
                    "$metadata" : {...},
                    "$version": 1
                },
                "reported": {
                    "telemetryConfig": {
                        "sendFrequency": "5m",
                        "status": "success"
                    }
                    "batteryLevel": 55,
                    "$metadata" : {...},
                    "$version": 4
                }
            }
        }

<span data-ttu-id="e387b-142">W obiekcie głównym są właściwości systemu i kontener obiektów na `tags` i oba `reported` i `desired` właściwości.</span><span class="sxs-lookup"><span data-stu-id="e387b-142">In the root object, are the system properties, and container objects for `tags` and both `reported` and `desired` properties.</span></span> <span data-ttu-id="e387b-143">`properties` Kontener zawiera niektóre elementy tylko do odczytu (`$metadata`, `$etag`, i `$version`) opisano w [metadane dwie urządzenia] [ lnk-twin-metadata] i [ Optymistycznej współbieżności] [ lnk-concurrency] sekcje.</span><span class="sxs-lookup"><span data-stu-id="e387b-143">The `properties` container contains some read-only elements (`$metadata`, `$etag`, and `$version`) described in the [Device twin metadata][lnk-twin-metadata] and [Optimistic concurrency][lnk-concurrency] sections.</span></span>

### <a name="reported-property-example"></a><span data-ttu-id="e387b-144">Przykład zgłoszony właściwości</span><span class="sxs-lookup"><span data-stu-id="e387b-144">Reported property example</span></span>
<span data-ttu-id="e387b-145">W poprzednim przykładzie zawiera dwie urządzenia `batteryLevel` właściwość, która jest zgłoszony przez aplikację urządzenia.</span><span class="sxs-lookup"><span data-stu-id="e387b-145">In the previous example, the device twin contains a `batteryLevel` property that is reported by the device app.</span></span> <span data-ttu-id="e387b-146">Ta właściwość umożliwia zapytania i działają na urządzeniach, na podstawie ostatniego poziomu zgłoszone baterii.</span><span class="sxs-lookup"><span data-stu-id="e387b-146">This property makes it possible to query and operate on devices based on the last reported battery level.</span></span> <span data-ttu-id="e387b-147">Przykładami innych możliwości raportowania urządzenia aplikacji urządzenia lub opcji łączności.</span><span class="sxs-lookup"><span data-stu-id="e387b-147">Other examples include the device app reporting device capabilities or connectivity options.</span></span>

> [!NOTE]
> <span data-ttu-id="e387b-148">Właściwości zgłoszone uprościć scenariuszy, w którym zaplecza rozwiązania jest zainteresowana ostatniej znanej wartości właściwości.</span><span class="sxs-lookup"><span data-stu-id="e387b-148">Reported properties simplify scenarios where the solution back end is interested in the last known value of a property.</span></span> <span data-ttu-id="e387b-149">Użyj [wiadomości urządzenia do chmury] [ lnk-d2c] zaplecza rozwiązania musi przetworzyć telemetrii urządzenia w postaci sekwencji zdarzeń oznaczony znacznikiem czasowym, takich jak szeregów czasowych.</span><span class="sxs-lookup"><span data-stu-id="e387b-149">Use [device-to-cloud messages][lnk-d2c] if the solution back end needs to process device telemetry in the form of sequences of timestamped events, such as time series.</span></span>

### <a name="desired-property-example"></a><span data-ttu-id="e387b-150">Przykład żądanej właściwości</span><span class="sxs-lookup"><span data-stu-id="e387b-150">Desired property example</span></span>
<span data-ttu-id="e387b-151">W poprzednim przykładzie `telemetryConfig` potrzebne dwie urządzeń i właściwości zgłoszone są używane przez zaplecza rozwiązania i aplikacji urządzenia zsynchronizować konfiguracji dane telemetryczne dla tego urządzenia.</span><span class="sxs-lookup"><span data-stu-id="e387b-151">In the previous example, the `telemetryConfig` device twin desired and reported properties are used by the solution back end and the device app to synchronize the telemetry configuration for this device.</span></span> <span data-ttu-id="e387b-152">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="e387b-152">For example:</span></span>

1. <span data-ttu-id="e387b-153">Zaplecze rozwiązania ustawia żądanej właściwości na wartość wymaganą konfiguracją.</span><span class="sxs-lookup"><span data-stu-id="e387b-153">The solution back end sets the desired property with the desired configuration value.</span></span> <span data-ttu-id="e387b-154">Poniżej przedstawiono fragment dokumentu przy użyciu zestawu żądanej właściwości:</span><span class="sxs-lookup"><span data-stu-id="e387b-154">Here is the portion of the document with the desired property set:</span></span>
   
        ...
        "desired": {
            "telemetryConfig": {
                "sendFrequency": "5m"
            },
            ...
        },
        ...
2. <span data-ttu-id="e387b-155">Powiadomienie do aplikacji urządzenia zmiany natychmiast, jeśli połączone lub przy pierwszym próba ponownego połączenia.</span><span class="sxs-lookup"><span data-stu-id="e387b-155">The device app is notified of the change immediately if connected, or at the first reconnect.</span></span> <span data-ttu-id="e387b-156">Aplikacji urządzenia następnie raporty zaktualizowanej konfiguracji (lub warunek błędu przy użyciu `status` właściwości).</span><span class="sxs-lookup"><span data-stu-id="e387b-156">The device app then reports the updated configuration (or an error condition using the `status` property).</span></span> <span data-ttu-id="e387b-157">Poniżej przedstawiono część zgłoszonych właściwości:</span><span class="sxs-lookup"><span data-stu-id="e387b-157">Here is the portion of the reported properties:</span></span>
   
        ...
        "reported": {
            "telemetryConfig": {
                "sendFrequency": "5m",
                "status": "success"
            }
            ...
        }
        ...
3. <span data-ttu-id="e387b-158">Zaplecze rozwiązania można śledzić wyniki operacji konfiguracji na wielu urządzeniach przez [badania] [ lnk-query] twins urządzenia.</span><span class="sxs-lookup"><span data-stu-id="e387b-158">The solution back end can track the results of the configuration operation across many devices, by [querying][lnk-query] device twins.</span></span>

> [!NOTE]
> <span data-ttu-id="e387b-159">Poprzedni fragmenty kodu są przykłady, zoptymalizowana pod kątem czytelności, z jednym ze sposobów kodowania Konfiguracja urządzenia i jego stan.</span><span class="sxs-lookup"><span data-stu-id="e387b-159">The preceding snippets are examples, optimized for readability, of one way to encode a device configuration and its status.</span></span> <span data-ttu-id="e387b-160">Centrum IoT nie nakłada określonego schematu dla dwie urządzenia żądanego i podać właściwości w twins urządzenia.</span><span class="sxs-lookup"><span data-stu-id="e387b-160">IoT Hub does not impose a specific schema for the device twin desired and reported properties in the device twins.</span></span>
> 
> 

<span data-ttu-id="e387b-161">Twins służy do synchronizowania długotrwałe operacje, takie jak aktualizacje oprogramowania układowego.</span><span class="sxs-lookup"><span data-stu-id="e387b-161">You can use twins to synchronize long-running operations such as firmware updates.</span></span> <span data-ttu-id="e387b-162">Aby uzyskać więcej informacji na temat sposobu synchronizacji i śledzenia operacją wymagającą dużo czasu na urządzeniach za pomocą właściwości, zobacz [Użyj żądanego właściwości, aby skonfigurować urządzenia][lnk-twin-properties].</span><span class="sxs-lookup"><span data-stu-id="e387b-162">For more information on how to use properties to synchronize and track a long running operation across devices, see [Use desired properties to configure devices][lnk-twin-properties].</span></span>

## <a name="back-end-operations"></a><span data-ttu-id="e387b-163">Operacje zaplecza</span><span class="sxs-lookup"><span data-stu-id="e387b-163">Back-end operations</span></span>
<span data-ttu-id="e387b-164">Zaplecze rozwiązania działa na dwie urządzenia przy użyciu następujących operacji niepodzielnych za pośrednictwem protokołu HTTP:</span><span class="sxs-lookup"><span data-stu-id="e387b-164">The solution back end operates on the device twin using the following atomic operations, exposed through HTTP:</span></span>

1. <span data-ttu-id="e387b-165">**Pobrać dwie urządzenia za pomocą identyfikatora**. Ta operacja zwraca dokument dwie urządzenia, w tym tagów i potrzeby zgłoszone i właściwości systemu.</span><span class="sxs-lookup"><span data-stu-id="e387b-165">**Retrieve device twin by id**. This operation returns the device twin document, including tags and desired, reported, and system properties.</span></span>
2. <span data-ttu-id="e387b-166">**Częściowego zaktualizowania dwie urządzenia**.</span><span class="sxs-lookup"><span data-stu-id="e387b-166">**Partially update device twin**.</span></span> <span data-ttu-id="e387b-167">Ta operacja umożliwia zaplecza rozwiązania celu częściowego zaktualizowania znaczników i odpowiednie właściwości w dwie urządzenia.</span><span class="sxs-lookup"><span data-stu-id="e387b-167">This operation enables the solution back end to partially update the tags or desired properties in a device twin.</span></span> <span data-ttu-id="e387b-168">Częściowej aktualizacji jest wyrażona jako dokument JSON, który dodaje lub aktualizuje dowolną właściwość.</span><span class="sxs-lookup"><span data-stu-id="e387b-168">The partial update is expressed as a JSON document that adds or updates any property.</span></span> <span data-ttu-id="e387b-169">Wartość właściwości `null` zostaną usunięte.</span><span class="sxs-lookup"><span data-stu-id="e387b-169">Properties set to `null` are removed.</span></span> <span data-ttu-id="e387b-170">Poniższy przykład tworzy nową właściwość odpowiednią wartością `{"newProperty": "newValue"}`, spowoduje zastąpienie istniejącej wartości `existingProperty` z `"otherNewValue"`i usuwa `otherOldProperty`.</span><span class="sxs-lookup"><span data-stu-id="e387b-170">The following example creates a new desired property with value `{"newProperty": "newValue"}`, overwrites the existing value of `existingProperty` with `"otherNewValue"`, and removes `otherOldProperty`.</span></span> <span data-ttu-id="e387b-171">Nie zmian do istniejących żądanej właściwości bądź tagi:</span><span class="sxs-lookup"><span data-stu-id="e387b-171">No other changes are made to existing desired properties or tags:</span></span>
   
        {
            "properties": {
                "desired": {
                    "newProperty": {
                        "nestedProperty": "newValue"
                    },
                    "existingProperty": "otherNewValue",
                    "otherOldProperty": null
                }
            }
        }
3. <span data-ttu-id="e387b-172">**Zastąp odpowiednie właściwości**.</span><span class="sxs-lookup"><span data-stu-id="e387b-172">**Replace desired properties**.</span></span> <span data-ttu-id="e387b-173">Ta operacja umożliwia zaplecza rozwiązania całkowicie zastąpić wszystkie istniejące odpowiednie właściwości i Zastąp nowy dokument JSON dla `properties/desired`.</span><span class="sxs-lookup"><span data-stu-id="e387b-173">This operation enables the solution back end to completely overwrite all existing desired properties and substitute a new JSON document for `properties/desired`.</span></span>
4. <span data-ttu-id="e387b-174">**Zastąp znaczniki**.</span><span class="sxs-lookup"><span data-stu-id="e387b-174">**Replace tags**.</span></span> <span data-ttu-id="e387b-175">Ta operacja umożliwia zaplecza rozwiązania całkowicie zastąpić wszystkie istniejące znaczniki i Zastąp nowy dokument JSON dla `tags`.</span><span class="sxs-lookup"><span data-stu-id="e387b-175">This operation enables the solution back end to completely overwrite all existing tags and substitute a new JSON document for `tags`.</span></span>
5. <span data-ttu-id="e387b-176">**Odbieranie powiadomień dwie**.</span><span class="sxs-lookup"><span data-stu-id="e387b-176">**Receive twin notifications**.</span></span> <span data-ttu-id="e387b-177">Ta operacja pozwala zaplecza rozwiązania otrzymać powiadomienie, gdy dwie jest modyfikowany.</span><span class="sxs-lookup"><span data-stu-id="e387b-177">This operation allows the solution back end to be notified when the twin is modified.</span></span> <span data-ttu-id="e387b-178">Aby to zrobić, rozwiązania IoT musi utworzyć trasę i ustaw źródło danych *twinChangeEvents*.</span><span class="sxs-lookup"><span data-stu-id="e387b-178">To do so, your IoT solution needs to create a route and to set the Data Source equal to *twinChangeEvents*.</span></span> <span data-ttu-id="e387b-179">Domyślnie są wysyłane żadne powiadomienia dwie, oznacza to, że istnieje wstępnie ma takie tras.</span><span class="sxs-lookup"><span data-stu-id="e387b-179">By default, no twin notifications are sent, that is, no such routes pre-exist.</span></span> <span data-ttu-id="e387b-180">Jeśli szybkość zmian jest zbyt duża lub z innych powodów, takich jak wewnętrzne błędy Centrum IoT może wysłać tylko jedno powiadomienie, który zawiera wszystkie zmiany.</span><span class="sxs-lookup"><span data-stu-id="e387b-180">If the rate of change is too high, or for other reasons, such as internal failures, the IoT Hub might send only one notification that contains all changes.</span></span> <span data-ttu-id="e387b-181">Tak Jeśli aplikacja wymaga niezawodnej inspekcji i rejestrowania wszystkich stanów pośredniego, następnie nadal zalecane jest używanie D2C wiadomości.</span><span class="sxs-lookup"><span data-stu-id="e387b-181">So, if your application needs reliable auditing and logging of all intermediate states, then it is still recommended that you use D2C messages.</span></span> <span data-ttu-id="e387b-182">Komunikat powiadomienia dwie zawiera właściwości, oraz i treść.</span><span class="sxs-lookup"><span data-stu-id="e387b-182">The twin notification message includes properties, and body.</span></span>

    - <span data-ttu-id="e387b-183">Właściwości</span><span class="sxs-lookup"><span data-stu-id="e387b-183">Properties</span></span>

    | <span data-ttu-id="e387b-184">Nazwa</span><span class="sxs-lookup"><span data-stu-id="e387b-184">Name</span></span> | <span data-ttu-id="e387b-185">Wartość</span><span class="sxs-lookup"><span data-stu-id="e387b-185">Value</span></span> |
    | --- | --- |
    <span data-ttu-id="e387b-186">$content — typ</span><span class="sxs-lookup"><span data-stu-id="e387b-186">$content-type</span></span> | <span data-ttu-id="e387b-187">application/json</span><span class="sxs-lookup"><span data-stu-id="e387b-187">application/json</span></span> |
    <span data-ttu-id="e387b-188">$iothub-enqueuedtime</span><span class="sxs-lookup"><span data-stu-id="e387b-188">$iothub-enqueuedtime</span></span> |  <span data-ttu-id="e387b-189">Czas wysłania powiadomienia</span><span class="sxs-lookup"><span data-stu-id="e387b-189">Time when the notification was sent</span></span> |
    <span data-ttu-id="e387b-190">$iothub-komunikat-źródła</span><span class="sxs-lookup"><span data-stu-id="e387b-190">$iothub-message-source</span></span> | <span data-ttu-id="e387b-191">twinChangeEvents</span><span class="sxs-lookup"><span data-stu-id="e387b-191">twinChangeEvents</span></span> |
    <span data-ttu-id="e387b-192">$content-kodowania</span><span class="sxs-lookup"><span data-stu-id="e387b-192">$content-encoding</span></span> | <span data-ttu-id="e387b-193">UTF-8</span><span class="sxs-lookup"><span data-stu-id="e387b-193">utf-8</span></span> |
    <span data-ttu-id="e387b-194">deviceId</span><span class="sxs-lookup"><span data-stu-id="e387b-194">deviceId</span></span> | <span data-ttu-id="e387b-195">Identyfikator urządzenia</span><span class="sxs-lookup"><span data-stu-id="e387b-195">Id of the device</span></span> |
    <span data-ttu-id="e387b-196">hubName</span><span class="sxs-lookup"><span data-stu-id="e387b-196">hubName</span></span> | <span data-ttu-id="e387b-197">Nazwa centrum IoT</span><span class="sxs-lookup"><span data-stu-id="e387b-197">Name of IoT Hub</span></span> |
    <span data-ttu-id="e387b-198">operationTimestamp</span><span class="sxs-lookup"><span data-stu-id="e387b-198">operationTimestamp</span></span> | <span data-ttu-id="e387b-199">[ISO8601] sygnatury czasowej operacji</span><span class="sxs-lookup"><span data-stu-id="e387b-199">[ISO8601] timestamp of operation</span></span> |
    <span data-ttu-id="e387b-200">Centrum iothub komunikat schemacie</span><span class="sxs-lookup"><span data-stu-id="e387b-200">iothub-message-schema</span></span> | <span data-ttu-id="e387b-201">deviceLifecycleNotification</span><span class="sxs-lookup"><span data-stu-id="e387b-201">deviceLifecycleNotification</span></span> |
    <span data-ttu-id="e387b-202">opType</span><span class="sxs-lookup"><span data-stu-id="e387b-202">opType</span></span> | <span data-ttu-id="e387b-203">"replaceTwin" lub "updateTwin"</span><span class="sxs-lookup"><span data-stu-id="e387b-203">"replaceTwin" or "updateTwin"</span></span> |

    <span data-ttu-id="e387b-204">Właściwości systemu wiadomości są poprzedzane prefiksem `'$'` symbolu.</span><span class="sxs-lookup"><span data-stu-id="e387b-204">Message system properties are prefixed with the `'$'` symbol.</span></span>

    - <span data-ttu-id="e387b-205">Treść</span><span class="sxs-lookup"><span data-stu-id="e387b-205">Body</span></span>
        
    <span data-ttu-id="e387b-206">Ta sekcja zawiera wszystkie zmiany dwie w formacie JSON.</span><span class="sxs-lookup"><span data-stu-id="e387b-206">This section includes all the twin changes in a JSON format.</span></span> <span data-ttu-id="e387b-207">Używa tego samego formatu poprawek, z tą różnicą, że może zawierać wszystkie dwie sekcje: tagi, properties.reported properties.desired i czy zawiera on elementy "$metadata".</span><span class="sxs-lookup"><span data-stu-id="e387b-207">It uses the same format as a patch, with the difference that it can contain all twin sections: tags, properties.reported, properties.desired, and that it contains the “$metadata” elements.</span></span> <span data-ttu-id="e387b-208">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="e387b-208">For example,</span></span>
    ```
    {
        "properties": {
            "desired": {
                "$metadata": {
                    "$lastUpdated": "2016-02-30T16:24:48.789Z"
                },
                "$version": 1
            },
            "reported": {
                "$metadata": {
                    "$lastUpdated": "2016-02-30T16:24:48.789Z"
                },
                "$version": 1
            }
        }
    }
    ``` 

<span data-ttu-id="e387b-209">Obsługuje wszystkie poprzednie operacje [optymistycznej współbieżności] [ lnk-concurrency] i wymagają **ServiceConnect** uprawnienia, zgodnie z definicją w [zabezpieczeń] [ lnk-security] artykułu.</span><span class="sxs-lookup"><span data-stu-id="e387b-209">All the preceding operations support [Optimistic concurrency][lnk-concurrency] and require the **ServiceConnect** permission, as defined in the [Security][lnk-security] article.</span></span>

<span data-ttu-id="e387b-210">Oprócz tych operacji można zaplecza rozwiązania:</span><span class="sxs-lookup"><span data-stu-id="e387b-210">In addition to these operations, the solution back end can:</span></span>

* <span data-ttu-id="e387b-211">Zapytanie twins urządzenia przy użyciu przypominającego SQL [język zapytań Centrum IoT][lnk-query].</span><span class="sxs-lookup"><span data-stu-id="e387b-211">Query the device twins using the SQL-like [IoT Hub query language][lnk-query].</span></span>
* <span data-ttu-id="e387b-212">Wykonywanie operacji na dużych zestawów twins urządzenia przy użyciu [zadania][lnk-jobs].</span><span class="sxs-lookup"><span data-stu-id="e387b-212">Perform operations on large sets of device twins using [jobs][lnk-jobs].</span></span>

## <a name="device-operations"></a><span data-ttu-id="e387b-213">Operacje urządzenia</span><span class="sxs-lookup"><span data-stu-id="e387b-213">Device operations</span></span>
<span data-ttu-id="e387b-214">Aplikacja urządzenie działa na dwie urządzenia przy użyciu operacji niepodzielnych w następujących:</span><span class="sxs-lookup"><span data-stu-id="e387b-214">The device app operates on the device twin using the following atomic operations:</span></span>

1. <span data-ttu-id="e387b-215">**Pobrać dwie urządzenia**.</span><span class="sxs-lookup"><span data-stu-id="e387b-215">**Retrieve device twin**.</span></span> <span data-ttu-id="e387b-216">Ta operacja zwraca dokument dwie urządzenia (łącznie tagów i potrzeby, zgłoszone i właściwości systemu) dla aktualnie podłączonego urządzenia.</span><span class="sxs-lookup"><span data-stu-id="e387b-216">This operation returns the device twin document (including tags and desired, reported and system properties) for the currently connected device.</span></span>
2. <span data-ttu-id="e387b-217">**Częściowego zaktualizowania właściwości zgłoszone**.</span><span class="sxs-lookup"><span data-stu-id="e387b-217">**Partially update reported properties**.</span></span> <span data-ttu-id="e387b-218">Ta operacja umożliwia częściową aktualizację zgłoszone właściwości podłączonego urządzenia.</span><span class="sxs-lookup"><span data-stu-id="e387b-218">This operation enables the partial update of the reported properties of the currently connected device.</span></span> <span data-ttu-id="e387b-219">Ta operacja używa tego samego formatu aktualizacji JSON, że rozwiązanie kopię celu zastosowania częściowej aktualizacji żądanej właściwości.</span><span class="sxs-lookup"><span data-stu-id="e387b-219">This operation uses the same JSON update format that the solution back end uses for a partial update of desired properties.</span></span>
3. <span data-ttu-id="e387b-220">**Sprawdź odpowiednie właściwości**.</span><span class="sxs-lookup"><span data-stu-id="e387b-220">**Observe desired properties**.</span></span> <span data-ttu-id="e387b-221">Aktualnie podłączonego urządzenia można otrzymywać powiadomienia o aktualizacjach do żądanej właściwości, gdy wystąpią.</span><span class="sxs-lookup"><span data-stu-id="e387b-221">The currently connected device can choose to be notified of updates to the desired properties when they happen.</span></span> <span data-ttu-id="e387b-222">Urządzenie odbiera tego samego formularza aktualizacji (pełnych lub wymiana) wykonywane przez zaplecza rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="e387b-222">The device receives the same form of update (partial or full replacement) executed by the solution back end.</span></span>

<span data-ttu-id="e387b-223">Wszystkie poprzednie operacje wymagają **DeviceConnect** uprawnienia, zgodnie z definicją w [zabezpieczeń] [ lnk-security] artykułu.</span><span class="sxs-lookup"><span data-stu-id="e387b-223">All the preceding operations require the **DeviceConnect** permission, as defined in the [Security][lnk-security] article.</span></span>

<span data-ttu-id="e387b-224">[Urządzenia Azure IoT SDK] [ lnk-sdks] ułatwiają używać poprzedniej operacji z wielu języków i platform.</span><span class="sxs-lookup"><span data-stu-id="e387b-224">The [Azure IoT device SDKs][lnk-sdks] make it easy to use the preceding operations from many languages and platforms.</span></span> <span data-ttu-id="e387b-225">Więcej informacji na temat szczegóły Centrum IoT w nim elementów podstawowych synchronizacji odpowiednie właściwości można znaleźć w [przepływu ponowne łączenie urządzenia][lnk-reconnection].</span><span class="sxs-lookup"><span data-stu-id="e387b-225">More information on the details of IoT Hub primitives for desired properties synchronization can be found in [Device reconnection flow][lnk-reconnection].</span></span>

> [!NOTE]
> <span data-ttu-id="e387b-226">Obecnie twins urządzenia jest dostępny tylko w przypadku urządzeń łączących się za pomocą protokołu MQTT Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="e387b-226">Currently, device twins are accessible only from devices that connect to IoT Hub using the MQTT protocol.</span></span>
> 
> 

## <a name="reference-topics"></a><span data-ttu-id="e387b-227">Tematy odwołań:</span><span class="sxs-lookup"><span data-stu-id="e387b-227">Reference topics:</span></span>
<span data-ttu-id="e387b-228">Następujące tematy dokumentacji dostarczają więcej informacji na temat kontrolowania dostępu do Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="e387b-228">The following reference topics provide you with more information about controlling access to your IoT hub.</span></span>

## <a name="tags-and-properties-format"></a><span data-ttu-id="e387b-229">Format znaczników i właściwości</span><span class="sxs-lookup"><span data-stu-id="e387b-229">Tags and properties format</span></span>
<span data-ttu-id="e387b-230">Tagi, żądane i podać właściwości są obiektów JSON z następującymi ograniczeniami:</span><span class="sxs-lookup"><span data-stu-id="e387b-230">Tags, desired, and reported properties are JSON objects with the following restrictions:</span></span>

* <span data-ttu-id="e387b-231">Wszystkie klucze w obiektów JSON jest rozróżniana wielkość liter 64 bajtów ciągów UNICODE UTF-8.</span><span class="sxs-lookup"><span data-stu-id="e387b-231">All keys in JSON objects are case-sensitive 64 bytes UTF-8 UNICODE strings.</span></span> <span data-ttu-id="e387b-232">Dozwolone znaki kontrolne UNICODE (segmenty C0 i C1), Wyklucz znaków i `'.'`, `' '`, i `'$'`.</span><span class="sxs-lookup"><span data-stu-id="e387b-232">Allowed characters exclude UNICODE control characters (segments C0 and C1), and `'.'`, `' '`, and `'$'`.</span></span>
* <span data-ttu-id="e387b-233">Wszystkie wartości w formacie JSON obiekty mogą być następujące typy JSON: wartość logiczna, liczba, ciąg, obiekt.</span><span class="sxs-lookup"><span data-stu-id="e387b-233">All values in JSON objects can be of the following JSON types: boolean, number, string, object.</span></span> <span data-ttu-id="e387b-234">Tablice nie są dozwolone.</span><span class="sxs-lookup"><span data-stu-id="e387b-234">Arrays are not allowed.</span></span>
* <span data-ttu-id="e387b-235">Wszystkie obiekty JSON w tagach, żądane i podać właściwości mogą mieć maksymalną głębokość 5.</span><span class="sxs-lookup"><span data-stu-id="e387b-235">All JSON objects in tags, desired, and reported properties can have a maximum depth of 5.</span></span> <span data-ttu-id="e387b-236">Na przykład następujący obiekt jest prawidłowy:</span><span class="sxs-lookup"><span data-stu-id="e387b-236">For instance, the following object is valid:</span></span>

        {
            ...
            "tags": {
                "one": {
                    "two": {
                        "three": {
                            "four": {
                                "five": {
                                    "property": "value"
                                }
                            }
                        }
                    }
                }
            },
            ...
        }

* <span data-ttu-id="e387b-237">Wszystkie wartości ciągu może mieć maksymalnie 512 bajtów długości.</span><span class="sxs-lookup"><span data-stu-id="e387b-237">All string values can be at most 512 bytes in length.</span></span>

## <a name="device-twin-size"></a><span data-ttu-id="e387b-238">Rozmiar dwie urządzenia</span><span class="sxs-lookup"><span data-stu-id="e387b-238">Device twin size</span></span>
<span data-ttu-id="e387b-239">Centrum IoT wymusza ograniczenia rozmiarze 8KB wartości `tags`, `properties/desired`, i `properties/reported`, z wyjątkiem elementów tylko do odczytu.</span><span class="sxs-lookup"><span data-stu-id="e387b-239">IoT Hub enforces an 8KB size limitation on the values of `tags`, `properties/desired`, and `properties/reported`, excluding read-only elements.</span></span>
<span data-ttu-id="e387b-240">Rozmiar jest obliczany poprzez zliczanie sterowania wszystkie znaki oprócz UNICODE znaków (segmenty C0 i C1) i miejsca `' '` po wyświetleniu poza stałą typu string.</span><span class="sxs-lookup"><span data-stu-id="e387b-240">The size is computed by counting all characters excluding UNICODE control characters (segments C0 and C1) and space `' '` when it appears outside of a string constant.</span></span>
<span data-ttu-id="e387b-241">Centrum IoT z powodu błędu odrzuca wszystkie operacje, które spowoduje zwiększenie rozmiaru tych dokumentów powyżej limitu.</span><span class="sxs-lookup"><span data-stu-id="e387b-241">IoT Hub rejects with an error all operations that would increase the size of those documents above the limit.</span></span>

## <a name="device-twin-metadata"></a><span data-ttu-id="e387b-242">Metadane dwie urządzenia</span><span class="sxs-lookup"><span data-stu-id="e387b-242">Device twin metadata</span></span>
<span data-ttu-id="e387b-243">Centrum IoT przechowuje sygnatura czasowa ostatniej aktualizacji dla każdego obiektu JSON w dwie urządzenia żądanego i podać właściwości.</span><span class="sxs-lookup"><span data-stu-id="e387b-243">IoT Hub maintains the timestamp of the last update for each JSON object in device twin desired and reported properties.</span></span> <span data-ttu-id="e387b-244">Sygnatury czasowe są w UTC i kodowany w [ISO8601] format `YYYY-MM-DDTHH:MM:SS.mmmZ`.</span><span class="sxs-lookup"><span data-stu-id="e387b-244">The timestamps are in UTC and encoded in the [ISO8601] format `YYYY-MM-DDTHH:MM:SS.mmmZ`.</span></span>
<span data-ttu-id="e387b-245">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="e387b-245">For example:</span></span>

        {
            ...
            "properties": {
                "desired": {
                    "telemetryConfig": {
                        "sendFrequency": "5m"
                    },
                    "$metadata": {
                        "telemetryConfig": {
                            "sendFrequency": {
                                "$lastUpdated": "2016-03-30T16:24:48.789Z"
                            },
                            "$lastUpdated": "2016-03-30T16:24:48.789Z"
                        },
                        "$lastUpdated": "2016-03-30T16:24:48.789Z"
                    },
                    "$version": 23
                },
                "reported": {
                    "telemetryConfig": {
                        "sendFrequency": "5m",
                        "status": "success"
                    }
                    "batteryLevel": "55%",
                    "$metadata": {
                        "telemetryConfig": {
                            "sendFrequency": "5m",
                            "status": {
                                "$lastUpdated": "2016-03-31T16:35:48.789Z"
                            },
                            "$lastUpdated": "2016-03-31T16:35:48.789Z"
                        }
                        "batteryLevel": {
                            "$lastUpdated": "2016-04-01T16:35:48.789Z"
                        },
                        "$lastUpdated": "2016-04-01T16:24:48.789Z"
                    },
                    "$version": 123
                }
            }
            ...
        }

<span data-ttu-id="e387b-246">Ta informacja jest przechowywana na każdym poziomie (nie tylko liście strukturze JSON) do zachowania aktualizacji, które usunąć obiekt kluczy.</span><span class="sxs-lookup"><span data-stu-id="e387b-246">This information is kept at every level (not just the leaves of the JSON structure) to preserve updates that remove object keys.</span></span>

## <a name="optimistic-concurrency"></a><span data-ttu-id="e387b-247">Optymistycznej współbieżności</span><span class="sxs-lookup"><span data-stu-id="e387b-247">Optimistic concurrency</span></span>
<span data-ttu-id="e387b-248">Tagi, potrzeby i podać właściwości wszystkich optymistycznej współbieżności pomocy technicznej.</span><span class="sxs-lookup"><span data-stu-id="e387b-248">Tags, desired, and reported properties all support optimistic concurrency.</span></span>
<span data-ttu-id="e387b-249">Tagi przypada tag ETag jako [RFC7232], reprezentujący reprezentacja JSON znacznika.</span><span class="sxs-lookup"><span data-stu-id="e387b-249">Tags have an ETag, as per [RFC7232], that represents the tag's JSON representation.</span></span> <span data-ttu-id="e387b-250">Elementy etag w operacjach aktualizowania warunkowego z zaplecza rozwiązania służy do zapewnienia spójności.</span><span class="sxs-lookup"><span data-stu-id="e387b-250">You can use ETags in conditional update operations from the solution back end to ensure consistency.</span></span>

<span data-ttu-id="e387b-251">Dwie urządzenia żądanego i podać właściwości nie ma elementy etag, ale `$version` wartość, która może być przyrostowe.</span><span class="sxs-lookup"><span data-stu-id="e387b-251">Device twin desired and reported properties do not have ETags, but have a `$version` value that is guaranteed to be incremental.</span></span> <span data-ttu-id="e387b-252">Podobnie do tag ETag wersji mogą być używane przez stronę aktualizacji do wymuszania zgodności aktualizacji.</span><span class="sxs-lookup"><span data-stu-id="e387b-252">Similarly to an ETag, the version can be used by the updating party to enforce consistency of updates.</span></span> <span data-ttu-id="e387b-253">Na przykład aplikacji urządzenia zgłoszonego właściwości lub zaplecza rozwiązania dla żądanej właściwości.</span><span class="sxs-lookup"><span data-stu-id="e387b-253">For example, a device app for a reported property or the solution back end for a desired property.</span></span>

<span data-ttu-id="e387b-254">Wersje są także przydatne, gdy observing agenta (np. aplikacji urządzenia obserwowania odpowiednie właściwości) należy uzgodnić szczepy między wynik operacji pobierania i powiadomienie o aktualizacji.</span><span class="sxs-lookup"><span data-stu-id="e387b-254">Versions are also useful when an observing agent (such as the device app observing the desired properties) must reconcile races between the result of a retrieve operation and an update notification.</span></span> <span data-ttu-id="e387b-255">Sekcja [przepływu ponowne łączenie urządzenia] [ lnk-reconnection] zawiera więcej informacji.</span><span class="sxs-lookup"><span data-stu-id="e387b-255">The section [Device reconnection flow][lnk-reconnection] provides more information.</span></span>

## <a name="device-reconnection-flow"></a><span data-ttu-id="e387b-256">Przepływ ponowne nawiązanie połączenia urządzenia</span><span class="sxs-lookup"><span data-stu-id="e387b-256">Device reconnection flow</span></span>
<span data-ttu-id="e387b-257">Centrum IoT nie zachowa powiadomienia o aktualizacji odpowiednie właściwości dla urządzeń bez połączenia.</span><span class="sxs-lookup"><span data-stu-id="e387b-257">IoT Hub does not preserve desired properties update notifications for disconnected devices.</span></span> <span data-ttu-id="e387b-258">Wynika, że urządzenia, które nawiązuje połączenie musi pobrać pełną odpowiednie właściwości dokumentu, oprócz subskrypcji powiadomienia o aktualizacji.</span><span class="sxs-lookup"><span data-stu-id="e387b-258">It follows that a device that is connecting must retrieve the full desired properties document, in addition to subscribing for update notifications.</span></span> <span data-ttu-id="e387b-259">Możliwość szczepy między powiadomienia o aktualizacji i pobieranie pełnej, należy zapewnić następujący przepływ:</span><span class="sxs-lookup"><span data-stu-id="e387b-259">Given the possibility of races between update notifications and full retrieval, the following flow must be ensured:</span></span>

1. <span data-ttu-id="e387b-260">Łączy się z Centrum IoT z aplikacji urządzenia.</span><span class="sxs-lookup"><span data-stu-id="e387b-260">Device app connects to an IoT hub.</span></span>
2. <span data-ttu-id="e387b-261">Subskrybuje aplikacji urządzenia dla żądanej właściwości powiadomienia o aktualizacji.</span><span class="sxs-lookup"><span data-stu-id="e387b-261">Device app subscribes for desired properties update notifications.</span></span>
3. <span data-ttu-id="e387b-262">Aplikacji urządzenia pobiera pełnego dokumentu dla żądanej właściwości.</span><span class="sxs-lookup"><span data-stu-id="e387b-262">Device app retrieves the full document for desired properties.</span></span>

<span data-ttu-id="e387b-263">Zignorować wszystkie powiadomienia z aplikacji urządzenia `$version` mniejsza lub równa niż wersja pełnego dokumentu pobrane.</span><span class="sxs-lookup"><span data-stu-id="e387b-263">The device app can ignore all notifications with `$version` less or equal than the version of the full retrieved document.</span></span> <span data-ttu-id="e387b-264">Takie podejście jest możliwa, ponieważ gwarantuje Centrum IoT wersje zawsze zwiększyć.</span><span class="sxs-lookup"><span data-stu-id="e387b-264">This approach is possible because IoT Hub guarantees that versions always increment.</span></span>

> [!NOTE]
> <span data-ttu-id="e387b-265">Istotą takiej logiki jest już zaimplementowany w [urządzenia Azure IoT SDK][lnk-sdks].</span><span class="sxs-lookup"><span data-stu-id="e387b-265">This logic is already implemented in the [Azure IoT device SDKs][lnk-sdks].</span></span> <span data-ttu-id="e387b-266">Ten opis jest przydatne tylko w przypadku aplikacji urządzenia nie można użyć dowolnego urządzenia Azure IoT zestawy SDK i należy zaprogramować interfejsu MQTT bezpośrednio.</span><span class="sxs-lookup"><span data-stu-id="e387b-266">This description is useful only if the device app cannot use any of Azure IoT device SDKs and must program the MQTT interface directly.</span></span>
> 
> 

## <a name="additional-reference-material"></a><span data-ttu-id="e387b-267">Odwołanie dodatkowe materiały</span><span class="sxs-lookup"><span data-stu-id="e387b-267">Additional reference material</span></span>
<span data-ttu-id="e387b-268">Inne tematy referencyjne w Podręczniku dewelopera Centrum IoT obejmują:</span><span class="sxs-lookup"><span data-stu-id="e387b-268">Other reference topics in the IoT Hub developer guide include:</span></span>

* <span data-ttu-id="e387b-269">[Punkty końcowe Centrum IoT] [ lnk-endpoints] artykule opisano różne punkty końcowe, które udostępnia każdego centrum IoT dla operacji zarządzania i środowiska wykonawczego.</span><span class="sxs-lookup"><span data-stu-id="e387b-269">The [IoT Hub endpoints][lnk-endpoints] article describes the various endpoints that each IoT hub exposes for run-time and management operations.</span></span>
* <span data-ttu-id="e387b-270">[Ograniczenia przepustowości i przydziały] [ lnk-quotas] artykule przydziałów, które dotyczą usługi IoT Hub i ograniczania przepustowości zachowania można oczekiwać podczas korzystania z usługi.</span><span class="sxs-lookup"><span data-stu-id="e387b-270">The [Throttling and quotas][lnk-quotas] article describes the quotas that apply to the IoT Hub service and the throttling behavior to expect when you use the service.</span></span>
* <span data-ttu-id="e387b-271">[Zestawów SDK urządzeń i usług Azure IoT] [ lnk-sdks] artykule wymieniono języka różnych zestawów SDK, można użyć podczas opracowywania aplikacji usług i urządzeń, które współdziałają z Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="e387b-271">The [Azure IoT device and service SDKs][lnk-sdks] article lists the various language SDKs you can use when you develop both device and service apps that interact with IoT Hub.</span></span>
* <span data-ttu-id="e387b-272">[Centrum IoT zapytania języka twins urządzenia, zadania i rozsyłania wiadomości] [ lnk-query] artykule język zapytań Centrum IoT można pobrać z Centrum IoT informacji o twins urządzenia i zadania.</span><span class="sxs-lookup"><span data-stu-id="e387b-272">The [IoT Hub query language for device twins, jobs, and message routing][lnk-query] article describes the IoT Hub query language you can use to retrieve information from IoT Hub about your device twins and jobs.</span></span>
* <span data-ttu-id="e387b-273">[Obsługa MQTT Centrum IoT] [ lnk-devguide-mqtt] artykuł zawiera więcej informacji na temat obsługi protokołu MQTT Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="e387b-273">The [IoT Hub MQTT support][lnk-devguide-mqtt] article provides more information about IoT Hub support for the MQTT protocol.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e387b-274">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="e387b-274">Next steps</span></span>
<span data-ttu-id="e387b-275">Teraz wiesz już, o twins urządzenie, może Cię zainteresować następujące tematy przewodnik dewelopera Centrum IoT:</span><span class="sxs-lookup"><span data-stu-id="e387b-275">Now you have learned about device twins, you may be interested in the following IoT Hub developer guide topics:</span></span>

* <span data-ttu-id="e387b-276">[Wywoływanie metody bezpośrednio na urządzeniu][lnk-methods]</span><span class="sxs-lookup"><span data-stu-id="e387b-276">[Invoke a direct method on a device][lnk-methods]</span></span>
* <span data-ttu-id="e387b-277">[Planowanie zadań na wielu urządzeniach][lnk-jobs]</span><span class="sxs-lookup"><span data-stu-id="e387b-277">[Schedule jobs on multiple devices][lnk-jobs]</span></span>

<span data-ttu-id="e387b-278">Jeśli chcesz wypróbować niektóre pojęcia opisane w tym artykule, może Cię zainteresować następujące samouczki Centrum IoT:</span><span class="sxs-lookup"><span data-stu-id="e387b-278">If you would like to try out some of the concepts described in this article, you may be interested in the following IoT Hub tutorials:</span></span>

* <span data-ttu-id="e387b-279">[Jak używać dwie urządzenia][lnk-twin-tutorial]</span><span class="sxs-lookup"><span data-stu-id="e387b-279">[How to use the device twin][lnk-twin-tutorial]</span></span>
* <span data-ttu-id="e387b-280">[Sposób użycia właściwości dwie urządzenia][lnk-twin-properties]</span><span class="sxs-lookup"><span data-stu-id="e387b-280">[How to use device twin properties][lnk-twin-properties]</span></span>

<!-- links and images -->

[lnk-endpoints]: iot-hub-devguide-endpoints.md
[lnk-quotas]: iot-hub-devguide-quotas-throttling.md
[lnk-sdks]: iot-hub-devguide-sdks.md
[lnk-query]: iot-hub-devguide-query-language.md
[lnk-jobs]: iot-hub-devguide-jobs.md
[lnk-identity]: iot-hub-devguide-identity-registry.md
[lnk-d2c]: iot-hub-devguide-messages-d2c.md
[lnk-methods]: iot-hub-devguide-direct-methods.md
[lnk-security]: iot-hub-devguide-security.md
[lnk-c2d-guidance]: iot-hub-devguide-c2d-guidance.md
[lnk-d2c-guidance]: iot-hub-devguide-d2c-guidance.md

[ISO8601]: https://en.wikipedia.org/wiki/ISO_8601
[RFC7232]: https://tools.ietf.org/html/rfc7232
[lnk-devguide-mqtt]: iot-hub-mqtt-support.md

[lnk-devguide-directmethods]: iot-hub-devguide-direct-methods.md
[lnk-devguide-jobs]: iot-hub-devguide-jobs.md
[lnk-twin-tutorial]: iot-hub-node-node-twin-getstarted.md
[lnk-twin-properties]: iot-hub-node-node-twin-how-to-configure.md
[lnk-twin-metadata]: iot-hub-devguide-device-twins.md#device-twin-metadata
[lnk-concurrency]: iot-hub-devguide-device-twins.md#optimistic-concurrency
[lnk-reconnection]: iot-hub-devguide-device-twins.md#device-reconnection-flow

[img-twin]: media/iot-hub-devguide-device-twins/twin.png
