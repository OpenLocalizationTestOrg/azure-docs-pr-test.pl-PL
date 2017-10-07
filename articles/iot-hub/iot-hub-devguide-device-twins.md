---
title: "twins urządzenia Azure IoT Hub aaaUnderstand | Dokumentacja firmy Microsoft"
description: "Przewodnik dewelopera - Użyj urządzenia twins toosynchronize stan i dane konfiguracyjne między centrum IoT i urządzeniami"
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
ms.openlocfilehash: 7dade18665108ed352ff3d18e864dc34f451bbf6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="understand-and-use-device-twins-in-iot-hub"></a><span data-ttu-id="40227-103">W zrozumieniu i użytkowaniu twins urządzenie w Centrum IoT</span><span class="sxs-lookup"><span data-stu-id="40227-103">Understand and use device twins in IoT Hub</span></span>
## <a name="overview"></a><span data-ttu-id="40227-104">Omówienie</span><span class="sxs-lookup"><span data-stu-id="40227-104">Overview</span></span>
<span data-ttu-id="40227-105">*Urządzenie twins* są dokumentów JSON, w których są przechowywane informacje o stanie urządzenia (metadanych, konfiguracji i warunki).</span><span class="sxs-lookup"><span data-stu-id="40227-105">*Device twins* are JSON documents that store device state information (metadata, configurations, and conditions).</span></span> <span data-ttu-id="40227-106">Centrum IoT utrzymuje dwie urządzenia, dla każdego urządzenia połączyć z tooIoT koncentratora.</span><span class="sxs-lookup"><span data-stu-id="40227-106">IoT Hub persists a device twin for each device that you connect tooIoT Hub.</span></span> <span data-ttu-id="40227-107">W tym artykule opisano:</span><span class="sxs-lookup"><span data-stu-id="40227-107">This article describes:</span></span>

* <span data-ttu-id="40227-108">Witaj struktury Witaj dwie urządzenia: *tagi*, *żądany* i *zgłosił właściwości*, i</span><span class="sxs-lookup"><span data-stu-id="40227-108">hello structure of hello device twin: *tags*, *desired* and *reported properties*, and</span></span>
* <span data-ttu-id="40227-109">Witaj operacje aplikacji dla urządzeń i zaplecza na twins urządzenia.</span><span class="sxs-lookup"><span data-stu-id="40227-109">hello operations that device apps and back ends can perform on device twins.</span></span>

> [!NOTE]
> <span data-ttu-id="40227-110">Obecnie dostępny tylko w przypadku urządzeń łączących tooIoT Centrum są twins urządzenia przy użyciu protokołu MQTT hello.</span><span class="sxs-lookup"><span data-stu-id="40227-110">Currently, device twins are accessible only from devices that connect tooIoT Hub using hello MQTT protocol.</span></span> <span data-ttu-id="40227-111">Zobacz toohello [Obsługa MQTT] [ lnk-devguide-mqtt] artykuł, aby uzyskać instrukcje dotyczące tooconvert istniejących urządzeń aplikacji toouse MQTT.</span><span class="sxs-lookup"><span data-stu-id="40227-111">Refer toohello [MQTT support][lnk-devguide-mqtt] article for instructions on how tooconvert existing device app toouse MQTT.</span></span>
> 
> 

### <a name="when-toouse"></a><span data-ttu-id="40227-112">Gdy toouse</span><span class="sxs-lookup"><span data-stu-id="40227-112">When toouse</span></span>
<span data-ttu-id="40227-113">Użyj twins urządzenia do:</span><span class="sxs-lookup"><span data-stu-id="40227-113">Use device twins to:</span></span>

* <span data-ttu-id="40227-114">Przechowywania metadanych specyficznych dla urządzeń w chmurze hello.</span><span class="sxs-lookup"><span data-stu-id="40227-114">Store device-specific metadata in hello cloud.</span></span> <span data-ttu-id="40227-115">Na przykład hello lokalizacja wdrożenia automaty maszyny.</span><span class="sxs-lookup"><span data-stu-id="40227-115">For example, hello deployment location of a vending machine.</span></span>
* <span data-ttu-id="40227-116">Bieżący stan informacji w raporcie, takie jak dostępne możliwości i warunków z aplikacją urządzenia.</span><span class="sxs-lookup"><span data-stu-id="40227-116">Report current state information such as available capabilities and conditions from your device app.</span></span> <span data-ttu-id="40227-117">Na przykład urządzenie jest połączone tooyour Centrum IoT over komórkowej lub Wi-Fi.</span><span class="sxs-lookup"><span data-stu-id="40227-117">For example, a device is connected tooyour IoT hub over cellular or WiFi.</span></span>
* <span data-ttu-id="40227-118">Synchronizuj stan hello przepływów pracy, długotrwałą między aplikacją urządzenia i aplikacji zaplecza.</span><span class="sxs-lookup"><span data-stu-id="40227-118">Synchronize hello state of long-running workflows between device app and back-end app.</span></span> <span data-ttu-id="40227-119">Na przykład podczas kopii rozwiązania hello zakończenia określa hello nowe tooinstall wersji oprogramowania układowego i raporty dotyczące aplikacji urządzeń hello hello różne etapy procesu aktualizacji hello.</span><span class="sxs-lookup"><span data-stu-id="40227-119">For example, when hello solution back end specifies hello new firmware version tooinstall, and hello device app reports hello various stages of hello update process.</span></span>
* <span data-ttu-id="40227-120">Zapytanie z metadanych urządzeniami, konfiguracji lub stanu.</span><span class="sxs-lookup"><span data-stu-id="40227-120">Query your device metadata, configuration, or state.</span></span>

<span data-ttu-id="40227-121">Odwołuje się zbyt[wskazówki komunikację urządzenia do chmury] [ lnk-d2c-guidance] wskazówki dotyczące przy użyciu właściwości zgłoszone, wiadomości urządzenia do chmury lub przekazywania pliku.</span><span class="sxs-lookup"><span data-stu-id="40227-121">Refer too[Device-to-cloud communication guidance][lnk-d2c-guidance] for guidance on using reported properties, device-to-cloud messages, or file upload.</span></span>
<span data-ttu-id="40227-122">Odwołuje się zbyt[wskazówki dotyczące komunikacji chmury do urządzenia] [ lnk-c2d-guidance] wskazówki na temat używania żądanej właściwości, metody bezpośredniego lub komunikaty chmury do urządzenia.</span><span class="sxs-lookup"><span data-stu-id="40227-122">Refer too[Cloud-to-device communication guidance][lnk-c2d-guidance] for guidance on using desired properties, direct methods, or cloud-to-device messages.</span></span>

## <a name="device-twins"></a><span data-ttu-id="40227-123">Twins urządzenia</span><span class="sxs-lookup"><span data-stu-id="40227-123">Device twins</span></span>
<span data-ttu-id="40227-124">Urządzenia twins przechowywać informacje dotyczące urządzeń który:</span><span class="sxs-lookup"><span data-stu-id="40227-124">Device twins store device-related information that:</span></span>

* <span data-ttu-id="40227-125">Urządzenia i z powrotem kończy się za pomocą warunków urządzenia toosynchronize i konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="40227-125">Device and back ends can use toosynchronize device conditions and configuration.</span></span>
* <span data-ttu-id="40227-126">za pomocą tooquery zaplecza rozwiązania Hello i docelowa długotrwałej operacji.</span><span class="sxs-lookup"><span data-stu-id="40227-126">hello solution back end can use tooquery and target long-running operations.</span></span>

<span data-ttu-id="40227-127">cykl życia Witaj dwie urządzenie jest połączone odpowiadającego toohello [tożsamości urządzenia][lnk-identity].</span><span class="sxs-lookup"><span data-stu-id="40227-127">hello lifecycle of a device twin is linked toohello corresponding [device identity][lnk-identity].</span></span> <span data-ttu-id="40227-128">Urządzenie twins niejawnie są tworzone i usuwane po utworzeniu lub usunięciu w Centrum IoT nowej tożsamości urządzenia.</span><span class="sxs-lookup"><span data-stu-id="40227-128">Device twins are implicitly created and deleted when a new device identity is created or deleted in IoT Hub.</span></span>

<span data-ttu-id="40227-129">Dwie urządzenia jest dokumentem JSON, który zawiera:</span><span class="sxs-lookup"><span data-stu-id="40227-129">A device twin is a JSON document that includes:</span></span>

* <span data-ttu-id="40227-130">**Tagi**.</span><span class="sxs-lookup"><span data-stu-id="40227-130">**Tags**.</span></span> <span data-ttu-id="40227-131">Sekcja hello dokumentu JSON, który hello zaplecza rozwiązania można z do odczytu i zapisu.</span><span class="sxs-lookup"><span data-stu-id="40227-131">A section of hello JSON document that hello solution back end can read from and write to.</span></span> <span data-ttu-id="40227-132">Tagi nie są widoczne toodevice aplikacji.</span><span class="sxs-lookup"><span data-stu-id="40227-132">Tags are not visible toodevice apps.</span></span>
* <span data-ttu-id="40227-133">**Żądany właściwości**.</span><span class="sxs-lookup"><span data-stu-id="40227-133">**Desired properties**.</span></span> <span data-ttu-id="40227-134">Używać razem z konfiguracji urządzenia zgłoszonego właściwości toosynchronize lub warunków.</span><span class="sxs-lookup"><span data-stu-id="40227-134">Used along with reported properties toosynchronize device configuration or conditions.</span></span> <span data-ttu-id="40227-135">Żądane właściwości można ustawić tylko przez rozwiązania hello zakończenia i może zostać odczytany przez hello aplikacji urządzenia.</span><span class="sxs-lookup"><span data-stu-id="40227-135">Desired properties can only be set by hello solution back end and can be read by hello device app.</span></span> <span data-ttu-id="40227-136">w czasie rzeczywistym zmian właściwości hello potrzeby też być powiadamiani Hello aplikacji urządzenia.</span><span class="sxs-lookup"><span data-stu-id="40227-136">hello device app can also be notified in real time of changes in hello desired properties.</span></span>
* <span data-ttu-id="40227-137">**Zgłoszone właściwości**.</span><span class="sxs-lookup"><span data-stu-id="40227-137">**Reported properties**.</span></span> <span data-ttu-id="40227-138">Używać razem z konfiguracji urządzenia toosynchronize odpowiednie właściwości lub warunków.</span><span class="sxs-lookup"><span data-stu-id="40227-138">Used along with desired properties toosynchronize device configuration or conditions.</span></span> <span data-ttu-id="40227-139">Zgłoszony właściwości można ustawić tylko przez aplikację urządzenia hello i można odczytać i żądanych przez zaplecza rozwiązania hello.</span><span class="sxs-lookup"><span data-stu-id="40227-139">Reported properties can only be set by hello device app and can be read and queried by hello solution back end.</span></span>

<span data-ttu-id="40227-140">Ponadto hello głównego dokumentu JSON dwie urządzenia hello zawiera właściwości tylko do odczytu z hello odpowiedniego tożsamości urządzenia przechowywany w hello hello [rejestru tożsamości][lnk-identity].</span><span class="sxs-lookup"><span data-stu-id="40227-140">Additionally, hello root of hello device twin JSON document contains hello read-only properties from hello corresponding device identity stored in hello [identity registry][lnk-identity].</span></span>

![][img-twin]

<span data-ttu-id="40227-141">Witaj poniższy przykład przedstawia dwie urządzenia dokumentu JSON:</span><span class="sxs-lookup"><span data-stu-id="40227-141">hello following example shows a device twin JSON document:</span></span>

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

<span data-ttu-id="40227-142">W obiekcie głównym hello, są hello właściwości systemu i kontener obiektów na `tags` i oba `reported` i `desired` właściwości.</span><span class="sxs-lookup"><span data-stu-id="40227-142">In hello root object, are hello system properties, and container objects for `tags` and both `reported` and `desired` properties.</span></span> <span data-ttu-id="40227-143">Witaj `properties` kontener zawiera niektóre elementy tylko do odczytu (`$metadata`, `$etag`, i `$version`) opisano w hello [metadane dwie urządzenia] [ lnk-twin-metadata] i [ Optymistycznej współbieżności] [ lnk-concurrency] sekcje.</span><span class="sxs-lookup"><span data-stu-id="40227-143">hello `properties` container contains some read-only elements (`$metadata`, `$etag`, and `$version`) described in hello [Device twin metadata][lnk-twin-metadata] and [Optimistic concurrency][lnk-concurrency] sections.</span></span>

### <a name="reported-property-example"></a><span data-ttu-id="40227-144">Przykład zgłoszony właściwości</span><span class="sxs-lookup"><span data-stu-id="40227-144">Reported property example</span></span>
<span data-ttu-id="40227-145">W poprzednim przykładzie hello zawiera dwie urządzenia hello `batteryLevel` właściwości zgłaszane przez hello aplikacji urządzenia.</span><span class="sxs-lookup"><span data-stu-id="40227-145">In hello previous example, hello device twin contains a `batteryLevel` property that is reported by hello device app.</span></span> <span data-ttu-id="40227-146">Ta właściwość powoduje tooquery możliwe i działanie na urządzeniach, na podstawie ostatniego poziomu zgłoszone baterii hello.</span><span class="sxs-lookup"><span data-stu-id="40227-146">This property makes it possible tooquery and operate on devices based on hello last reported battery level.</span></span> <span data-ttu-id="40227-147">Przykładami innych hello urządzenia aplikacji raportowania możliwości urządzenia lub opcji łączności.</span><span class="sxs-lookup"><span data-stu-id="40227-147">Other examples include hello device app reporting device capabilities or connectivity options.</span></span>

> [!NOTE]
> <span data-ttu-id="40227-148">Właściwości zgłoszone uprościć scenariuszy, w którym zaplecza rozwiązania hello jest zainteresowana hello Ostatnia znana wartość właściwości.</span><span class="sxs-lookup"><span data-stu-id="40227-148">Reported properties simplify scenarios where hello solution back end is interested in hello last known value of a property.</span></span> <span data-ttu-id="40227-149">Użyj [wiadomości urządzenia do chmury] [ lnk-d2c] czy zaplecza rozwiązania hello wymaga tooprocess telemetrii urządzenia w formie hello sekwencji zdarzeń oznaczony znacznikiem czasowym, takich jak szeregów czasowych.</span><span class="sxs-lookup"><span data-stu-id="40227-149">Use [device-to-cloud messages][lnk-d2c] if hello solution back end needs tooprocess device telemetry in hello form of sequences of timestamped events, such as time series.</span></span>

### <a name="desired-property-example"></a><span data-ttu-id="40227-150">Przykład żądanej właściwości</span><span class="sxs-lookup"><span data-stu-id="40227-150">Desired property example</span></span>
<span data-ttu-id="40227-151">W poprzednim przykładzie hello hello `telemetryConfig` potrzebne dwie urządzeń i właściwości zgłoszone są używane przez zaplecza rozwiązania hello i hello urządzenia aplikacji toosynchronize hello telemetrii konfiguracji dla tego urządzenia.</span><span class="sxs-lookup"><span data-stu-id="40227-151">In hello previous example, hello `telemetryConfig` device twin desired and reported properties are used by hello solution back end and hello device app toosynchronize hello telemetry configuration for this device.</span></span> <span data-ttu-id="40227-152">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="40227-152">For example:</span></span>

1. <span data-ttu-id="40227-153">zaplecza rozwiązania Hello ustawia hello wymaganą właściwość z wartością konfiguracji hello potrzebne.</span><span class="sxs-lookup"><span data-stu-id="40227-153">hello solution back end sets hello desired property with hello desired configuration value.</span></span> <span data-ttu-id="40227-154">Poniżej przedstawiono część hello hello dokument z hello żądany zestaw właściwości:</span><span class="sxs-lookup"><span data-stu-id="40227-154">Here is hello portion of hello document with hello desired property set:</span></span>
   
        ...
        "desired": {
            "telemetryConfig": {
                "sendFrequency": "5m"
            },
            ...
        },
        ...
2. <span data-ttu-id="40227-155">aplikacji urządzenia Hello jest powiadamiany o zmiany hello natychmiast, jeśli połączenie lub na powitania najpierw Połącz ponownie.</span><span class="sxs-lookup"><span data-stu-id="40227-155">hello device app is notified of hello change immediately if connected, or at hello first reconnect.</span></span> <span data-ttu-id="40227-156">Witaj aplikacji urządzenia następnie raporty hello aktualizacji konfiguracji (lub warunek błędu przy użyciu hello `status` właściwości).</span><span class="sxs-lookup"><span data-stu-id="40227-156">hello device app then reports hello updated configuration (or an error condition using hello `status` property).</span></span> <span data-ttu-id="40227-157">Oto hello część hello zgłoszonych właściwości:</span><span class="sxs-lookup"><span data-stu-id="40227-157">Here is hello portion of hello reported properties:</span></span>
   
        ...
        "reported": {
            "telemetryConfig": {
                "sendFrequency": "5m",
                "status": "success"
            }
            ...
        }
        ...
3. <span data-ttu-id="40227-158">zaplecza rozwiązania Hello można śledzić hello wyniki operacji konfiguracji hello na wielu urządzeniach przez [badania] [ lnk-query] twins urządzenia.</span><span class="sxs-lookup"><span data-stu-id="40227-158">hello solution back end can track hello results of hello configuration operation across many devices, by [querying][lnk-query] device twins.</span></span>

> [!NOTE]
> <span data-ttu-id="40227-159">Hello poprzedniego fragmenty kodu są przykłady, zoptymalizowana pod kątem czytelności jednokierunkowej tooencode Konfiguracja urządzenia i jego stan.</span><span class="sxs-lookup"><span data-stu-id="40227-159">hello preceding snippets are examples, optimized for readability, of one way tooencode a device configuration and its status.</span></span> <span data-ttu-id="40227-160">Witaj dwie urządzenia żądanego i podać właściwości w twins urządzenia hello Centrum IoT nie nakłada określonego schematu.</span><span class="sxs-lookup"><span data-stu-id="40227-160">IoT Hub does not impose a specific schema for hello device twin desired and reported properties in hello device twins.</span></span>
> 
> 

<span data-ttu-id="40227-161">Możesz użyć twins toosynchronize długotrwałe operacje, takie jak aktualizacje oprogramowania układowego.</span><span class="sxs-lookup"><span data-stu-id="40227-161">You can use twins toosynchronize long-running operations such as firmware updates.</span></span> <span data-ttu-id="40227-162">Aby uzyskać więcej informacji na temat sposobu toosynchronize właściwości toouse i Śledź operacją wymagającą dużo czasu na urządzeniach, zobacz [Użyj potrzeby urządzeń tooconfigure właściwości][lnk-twin-properties].</span><span class="sxs-lookup"><span data-stu-id="40227-162">For more information on how toouse properties toosynchronize and track a long running operation across devices, see [Use desired properties tooconfigure devices][lnk-twin-properties].</span></span>

## <a name="back-end-operations"></a><span data-ttu-id="40227-163">Operacje zaplecza</span><span class="sxs-lookup"><span data-stu-id="40227-163">Back-end operations</span></span>
<span data-ttu-id="40227-164">zaplecza rozwiązania Hello działa na powitania dwie urządzenia przy użyciu powitania po operacjach niepodzielnych za pośrednictwem protokołu HTTP:</span><span class="sxs-lookup"><span data-stu-id="40227-164">hello solution back end operates on hello device twin using hello following atomic operations, exposed through HTTP:</span></span>

1. <span data-ttu-id="40227-165">**Pobrać dwie urządzenia za pomocą identyfikatora**. Ta operacja zwraca hello urządzenia dwie dokumentu, łącznie z tagami i potrzeby zgłoszone i właściwości systemu.</span><span class="sxs-lookup"><span data-stu-id="40227-165">**Retrieve device twin by id**. This operation returns hello device twin document, including tags and desired, reported, and system properties.</span></span>
2. <span data-ttu-id="40227-166">**Częściowego zaktualizowania dwie urządzenia**.</span><span class="sxs-lookup"><span data-stu-id="40227-166">**Partially update device twin**.</span></span> <span data-ttu-id="40227-167">Ta operacja umożliwia hello rozwiązania zaplecza toopartially aktualizacji hello znaczników lub odpowiednie właściwości w dwie urządzenia.</span><span class="sxs-lookup"><span data-stu-id="40227-167">This operation enables hello solution back end toopartially update hello tags or desired properties in a device twin.</span></span> <span data-ttu-id="40227-168">Witaj częściowej aktualizacji jest wyrażona jako dokument JSON, który dodaje lub aktualizuje dowolną właściwość.</span><span class="sxs-lookup"><span data-stu-id="40227-168">hello partial update is expressed as a JSON document that adds or updates any property.</span></span> <span data-ttu-id="40227-169">Właściwości ustawione zbyt`null` zostaną usunięte.</span><span class="sxs-lookup"><span data-stu-id="40227-169">Properties set too`null` are removed.</span></span> <span data-ttu-id="40227-170">Witaj poniższy przykład tworzy nową właściwość żądaną wartością `{"newProperty": "newValue"}`, zastępuje istniejącą wartość hello z `existingProperty` z `"otherNewValue"`i usuwa `otherOldProperty`.</span><span class="sxs-lookup"><span data-stu-id="40227-170">hello following example creates a new desired property with value `{"newProperty": "newValue"}`, overwrites hello existing value of `existingProperty` with `"otherNewValue"`, and removes `otherOldProperty`.</span></span> <span data-ttu-id="40227-171">Nie zmian właściwości tooexisting potrzeby lub tagi:</span><span class="sxs-lookup"><span data-stu-id="40227-171">No other changes are made tooexisting desired properties or tags:</span></span>
   
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
3. <span data-ttu-id="40227-172">**Zastąp odpowiednie właściwości**.</span><span class="sxs-lookup"><span data-stu-id="40227-172">**Replace desired properties**.</span></span> <span data-ttu-id="40227-173">Toocompletely umożliwia zaplecza rozwiązania hello tej operacji zastąpić wszystkie istniejące właściwości żądanego i Zastąp nowy dokument JSON dla `properties/desired`.</span><span class="sxs-lookup"><span data-stu-id="40227-173">This operation enables hello solution back end toocompletely overwrite all existing desired properties and substitute a new JSON document for `properties/desired`.</span></span>
4. <span data-ttu-id="40227-174">**Zastąp znaczniki**.</span><span class="sxs-lookup"><span data-stu-id="40227-174">**Replace tags**.</span></span> <span data-ttu-id="40227-175">Toocompletely umożliwia zaplecza rozwiązania hello tej operacji zastąpić wszystkie istniejące znaczniki i Zastąp nowy dokument JSON dla `tags`.</span><span class="sxs-lookup"><span data-stu-id="40227-175">This operation enables hello solution back end toocompletely overwrite all existing tags and substitute a new JSON document for `tags`.</span></span>
5. <span data-ttu-id="40227-176">**Odbieranie powiadomień dwie**.</span><span class="sxs-lookup"><span data-stu-id="40227-176">**Receive twin notifications**.</span></span> <span data-ttu-id="40227-177">Ta operacja pozwala toobe zaplecza rozwiązania hello powiadomienie, gdy dwie hello jest modyfikowany.</span><span class="sxs-lookup"><span data-stu-id="40227-177">This operation allows hello solution back end toobe notified when hello twin is modified.</span></span> <span data-ttu-id="40227-178">toodo tak, rozwiązania IoT musi toocreate trasy i równości źródła danych hello tooset zbyt*twinChangeEvents*.</span><span class="sxs-lookup"><span data-stu-id="40227-178">toodo so, your IoT solution needs toocreate a route and tooset hello Data Source equal too*twinChangeEvents*.</span></span> <span data-ttu-id="40227-179">Domyślnie są wysyłane żadne powiadomienia dwie, oznacza to, że istnieje wstępnie ma takie tras.</span><span class="sxs-lookup"><span data-stu-id="40227-179">By default, no twin notifications are sent, that is, no such routes pre-exist.</span></span> <span data-ttu-id="40227-180">Jeśli hello szybkość zmian jest zbyt duża lub z innych powodów, takich jak wewnętrzne błędy hello Centrum IoT może wysłać tylko jedno powiadomienie, który zawiera wszystkie zmiany.</span><span class="sxs-lookup"><span data-stu-id="40227-180">If hello rate of change is too high, or for other reasons, such as internal failures, hello IoT Hub might send only one notification that contains all changes.</span></span> <span data-ttu-id="40227-181">Tak Jeśli aplikacja wymaga niezawodnej inspekcji i rejestrowania wszystkich stanów pośredniego, następnie nadal zalecane jest używanie D2C wiadomości.</span><span class="sxs-lookup"><span data-stu-id="40227-181">So, if your application needs reliable auditing and logging of all intermediate states, then it is still recommended that you use D2C messages.</span></span> <span data-ttu-id="40227-182">Witaj dwie powiadomienie zawiera właściwości, oraz i treść.</span><span class="sxs-lookup"><span data-stu-id="40227-182">hello twin notification message includes properties, and body.</span></span>

    - <span data-ttu-id="40227-183">Właściwości</span><span class="sxs-lookup"><span data-stu-id="40227-183">Properties</span></span>

    | <span data-ttu-id="40227-184">Nazwa</span><span class="sxs-lookup"><span data-stu-id="40227-184">Name</span></span> | <span data-ttu-id="40227-185">Wartość</span><span class="sxs-lookup"><span data-stu-id="40227-185">Value</span></span> |
    | --- | --- |
    <span data-ttu-id="40227-186">$content — typ</span><span class="sxs-lookup"><span data-stu-id="40227-186">$content-type</span></span> | <span data-ttu-id="40227-187">application/json</span><span class="sxs-lookup"><span data-stu-id="40227-187">application/json</span></span> |
    <span data-ttu-id="40227-188">$iothub-enqueuedtime</span><span class="sxs-lookup"><span data-stu-id="40227-188">$iothub-enqueuedtime</span></span> |  <span data-ttu-id="40227-189">Czas wysłania powiadomienia hello</span><span class="sxs-lookup"><span data-stu-id="40227-189">Time when hello notification was sent</span></span> |
    <span data-ttu-id="40227-190">$iothub-komunikat-źródła</span><span class="sxs-lookup"><span data-stu-id="40227-190">$iothub-message-source</span></span> | <span data-ttu-id="40227-191">twinChangeEvents</span><span class="sxs-lookup"><span data-stu-id="40227-191">twinChangeEvents</span></span> |
    <span data-ttu-id="40227-192">$content-kodowania</span><span class="sxs-lookup"><span data-stu-id="40227-192">$content-encoding</span></span> | <span data-ttu-id="40227-193">UTF-8</span><span class="sxs-lookup"><span data-stu-id="40227-193">utf-8</span></span> |
    <span data-ttu-id="40227-194">deviceId</span><span class="sxs-lookup"><span data-stu-id="40227-194">deviceId</span></span> | <span data-ttu-id="40227-195">Identyfikator urządzenia hello</span><span class="sxs-lookup"><span data-stu-id="40227-195">Id of hello device</span></span> |
    <span data-ttu-id="40227-196">hubName</span><span class="sxs-lookup"><span data-stu-id="40227-196">hubName</span></span> | <span data-ttu-id="40227-197">Nazwa centrum IoT</span><span class="sxs-lookup"><span data-stu-id="40227-197">Name of IoT Hub</span></span> |
    <span data-ttu-id="40227-198">operationTimestamp</span><span class="sxs-lookup"><span data-stu-id="40227-198">operationTimestamp</span></span> | <span data-ttu-id="40227-199">[ISO8601] sygnatury czasowej operacji</span><span class="sxs-lookup"><span data-stu-id="40227-199">[ISO8601] timestamp of operation</span></span> |
    <span data-ttu-id="40227-200">Centrum iothub komunikat schemacie</span><span class="sxs-lookup"><span data-stu-id="40227-200">iothub-message-schema</span></span> | <span data-ttu-id="40227-201">deviceLifecycleNotification</span><span class="sxs-lookup"><span data-stu-id="40227-201">deviceLifecycleNotification</span></span> |
    <span data-ttu-id="40227-202">opType</span><span class="sxs-lookup"><span data-stu-id="40227-202">opType</span></span> | <span data-ttu-id="40227-203">"replaceTwin" lub "updateTwin"</span><span class="sxs-lookup"><span data-stu-id="40227-203">"replaceTwin" or "updateTwin"</span></span> |

    <span data-ttu-id="40227-204">Właściwości systemu wiadomości są poprzedzane prefiksem hello `'$'` symbolu.</span><span class="sxs-lookup"><span data-stu-id="40227-204">Message system properties are prefixed with hello `'$'` symbol.</span></span>

    - <span data-ttu-id="40227-205">Treść</span><span class="sxs-lookup"><span data-stu-id="40227-205">Body</span></span>
        
    <span data-ttu-id="40227-206">Ta sekcja zawiera wszystkie Witaj dwie zmiany w formacie JSON.</span><span class="sxs-lookup"><span data-stu-id="40227-206">This section includes all hello twin changes in a JSON format.</span></span> <span data-ttu-id="40227-207">Używa takiego samego formatu hello poprawek, z różnicą hello którą może zawierać wszystkie dwie sekcje: tagi, properties.reported properties.desired i czy zawiera on elementy hello "$metadata".</span><span class="sxs-lookup"><span data-stu-id="40227-207">It uses hello same format as a patch, with hello difference that it can contain all twin sections: tags, properties.reported, properties.desired, and that it contains hello “$metadata” elements.</span></span> <span data-ttu-id="40227-208">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="40227-208">For example,</span></span>
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

<span data-ttu-id="40227-209">Wszystkie hello poprzedniej operacji obsługi [optymistycznej współbieżności] [ lnk-concurrency] i wymagają hello **ServiceConnect** uprawnienia, zgodnie z definicją w hello [zabezpieczeń ] [ lnk-security] artykułu.</span><span class="sxs-lookup"><span data-stu-id="40227-209">All hello preceding operations support [Optimistic concurrency][lnk-concurrency] and require hello **ServiceConnect** permission, as defined in hello [Security][lnk-security] article.</span></span>

<span data-ttu-id="40227-210">Ponadto operacji toothese, rozwiązanie hello kopii może zakończenia:</span><span class="sxs-lookup"><span data-stu-id="40227-210">In addition toothese operations, hello solution back end can:</span></span>

* <span data-ttu-id="40227-211">Zapytanie hello twins urządzenia przy użyciu hello przypominającego SQL [język zapytań Centrum IoT][lnk-query].</span><span class="sxs-lookup"><span data-stu-id="40227-211">Query hello device twins using hello SQL-like [IoT Hub query language][lnk-query].</span></span>
* <span data-ttu-id="40227-212">Wykonywanie operacji na dużych zestawów twins urządzenia przy użyciu [zadania][lnk-jobs].</span><span class="sxs-lookup"><span data-stu-id="40227-212">Perform operations on large sets of device twins using [jobs][lnk-jobs].</span></span>

## <a name="device-operations"></a><span data-ttu-id="40227-213">Operacje urządzenia</span><span class="sxs-lookup"><span data-stu-id="40227-213">Device operations</span></span>
<span data-ttu-id="40227-214">Witaj urządzenia aplikacji działa na Witaj dwie urządzenia przy użyciu powitania po operacjach niepodzielnych:</span><span class="sxs-lookup"><span data-stu-id="40227-214">hello device app operates on hello device twin using hello following atomic operations:</span></span>

1. <span data-ttu-id="40227-215">**Pobrać dwie urządzenia**.</span><span class="sxs-lookup"><span data-stu-id="40227-215">**Retrieve device twin**.</span></span> <span data-ttu-id="40227-216">Ta operacja zwraca hello urządzenia dwie dokumentu (łącznie tagów i potrzeby, zgłoszone i właściwości systemu) dla hello aktualnie połączonych urządzeń.</span><span class="sxs-lookup"><span data-stu-id="40227-216">This operation returns hello device twin document (including tags and desired, reported and system properties) for hello currently connected device.</span></span>
2. <span data-ttu-id="40227-217">**Częściowego zaktualizowania właściwości zgłoszone**.</span><span class="sxs-lookup"><span data-stu-id="40227-217">**Partially update reported properties**.</span></span> <span data-ttu-id="40227-218">Ta operacja umożliwia hello częściowego zaktualizowania hello zgłosił właściwości hello podłączonego urządzenia.</span><span class="sxs-lookup"><span data-stu-id="40227-218">This operation enables hello partial update of hello reported properties of hello currently connected device.</span></span> <span data-ttu-id="40227-219">To hello używa operacji aktualizacji JSON tego samego formatu tego hello rozwiązania wstecz celu zastosowania częściowej aktualizacji odpowiednie właściwości.</span><span class="sxs-lookup"><span data-stu-id="40227-219">This operation uses hello same JSON update format that hello solution back end uses for a partial update of desired properties.</span></span>
3. <span data-ttu-id="40227-220">**Sprawdź odpowiednie właściwości**.</span><span class="sxs-lookup"><span data-stu-id="40227-220">**Observe desired properties**.</span></span> <span data-ttu-id="40227-221">Witaj aktualnie podłączonego urządzenia można wybrać toobe powiadomienie właściwości toohello potrzeby aktualizacje, gdy wystąpią.</span><span class="sxs-lookup"><span data-stu-id="40227-221">hello currently connected device can choose toobe notified of updates toohello desired properties when they happen.</span></span> <span data-ttu-id="40227-222">Witaj urządzenie odbiera hello tego samego formularza aktualizacji (pełnych lub wymiana) wykonywane przez zaplecza rozwiązania hello.</span><span class="sxs-lookup"><span data-stu-id="40227-222">hello device receives hello same form of update (partial or full replacement) executed by hello solution back end.</span></span>

<span data-ttu-id="40227-223">Witaj wszystkich poprzednich operacji wymagają hello **DeviceConnect** uprawnienia, zgodnie z definicją w hello [zabezpieczeń] [ lnk-security] artykułu.</span><span class="sxs-lookup"><span data-stu-id="40227-223">All hello preceding operations require hello **DeviceConnect** permission, as defined in hello [Security][lnk-security] article.</span></span>

<span data-ttu-id="40227-224">Witaj [urządzenia Azure IoT SDK] [ lnk-sdks] była hello łatwe toouse poprzedzających operacje z wielu języków i platform.</span><span class="sxs-lookup"><span data-stu-id="40227-224">hello [Azure IoT device SDKs][lnk-sdks] make it easy toouse hello preceding operations from many languages and platforms.</span></span> <span data-ttu-id="40227-225">Więcej informacji na temat hello szczegóły Centrum IoT w nim elementów podstawowych synchronizacji odpowiednie właściwości można znaleźć w [przepływu ponowne łączenie urządzenia][lnk-reconnection].</span><span class="sxs-lookup"><span data-stu-id="40227-225">More information on hello details of IoT Hub primitives for desired properties synchronization can be found in [Device reconnection flow][lnk-reconnection].</span></span>

> [!NOTE]
> <span data-ttu-id="40227-226">Obecnie dostępny tylko w przypadku urządzeń łączących tooIoT Centrum są twins urządzenia przy użyciu protokołu MQTT hello.</span><span class="sxs-lookup"><span data-stu-id="40227-226">Currently, device twins are accessible only from devices that connect tooIoT Hub using hello MQTT protocol.</span></span>
> 
> 

## <a name="reference-topics"></a><span data-ttu-id="40227-227">Tematy odwołań:</span><span class="sxs-lookup"><span data-stu-id="40227-227">Reference topics:</span></span>
<span data-ttu-id="40227-228">Witaj następujące tematy dokumentacji zapewniają więcej informacji na temat kontrolowania dostępu tooyour IoT hub.</span><span class="sxs-lookup"><span data-stu-id="40227-228">hello following reference topics provide you with more information about controlling access tooyour IoT hub.</span></span>

## <a name="tags-and-properties-format"></a><span data-ttu-id="40227-229">Format znaczników i właściwości</span><span class="sxs-lookup"><span data-stu-id="40227-229">Tags and properties format</span></span>
<span data-ttu-id="40227-230">Tagi, żądane i podać właściwości są obiektów JSON z hello następujące ograniczenia:</span><span class="sxs-lookup"><span data-stu-id="40227-230">Tags, desired, and reported properties are JSON objects with hello following restrictions:</span></span>

* <span data-ttu-id="40227-231">Wszystkie klucze w obiektów JSON jest rozróżniana wielkość liter 64 bajtów ciągów UNICODE UTF-8.</span><span class="sxs-lookup"><span data-stu-id="40227-231">All keys in JSON objects are case-sensitive 64 bytes UTF-8 UNICODE strings.</span></span> <span data-ttu-id="40227-232">Dozwolone znaki kontrolne UNICODE (segmenty C0 i C1), Wyklucz znaków i `'.'`, `' '`, i `'$'`.</span><span class="sxs-lookup"><span data-stu-id="40227-232">Allowed characters exclude UNICODE control characters (segments C0 and C1), and `'.'`, `' '`, and `'$'`.</span></span>
* <span data-ttu-id="40227-233">Wszystkie wartości w formacie JSON obiekty mogą być hello następujące typy JSON: wartość logiczna, liczba, ciąg, obiekt.</span><span class="sxs-lookup"><span data-stu-id="40227-233">All values in JSON objects can be of hello following JSON types: boolean, number, string, object.</span></span> <span data-ttu-id="40227-234">Tablice nie są dozwolone.</span><span class="sxs-lookup"><span data-stu-id="40227-234">Arrays are not allowed.</span></span>
* <span data-ttu-id="40227-235">Wszystkie obiekty JSON w tagach, żądane i podać właściwości mogą mieć maksymalną głębokość 5.</span><span class="sxs-lookup"><span data-stu-id="40227-235">All JSON objects in tags, desired, and reported properties can have a maximum depth of 5.</span></span> <span data-ttu-id="40227-236">Na przykład po obiektu hello jest prawidłowy:</span><span class="sxs-lookup"><span data-stu-id="40227-236">For instance, hello following object is valid:</span></span>

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

* <span data-ttu-id="40227-237">Wszystkie wartości ciągu może mieć maksymalnie 512 bajtów długości.</span><span class="sxs-lookup"><span data-stu-id="40227-237">All string values can be at most 512 bytes in length.</span></span>

## <a name="device-twin-size"></a><span data-ttu-id="40227-238">Rozmiar dwie urządzenia</span><span class="sxs-lookup"><span data-stu-id="40227-238">Device twin size</span></span>
<span data-ttu-id="40227-239">Centrum IoT wymusza ograniczenie rozmiaru 8KB na wartościach hello `tags`, `properties/desired`, i `properties/reported`, z wyjątkiem elementów tylko do odczytu.</span><span class="sxs-lookup"><span data-stu-id="40227-239">IoT Hub enforces an 8KB size limitation on hello values of `tags`, `properties/desired`, and `properties/reported`, excluding read-only elements.</span></span>
<span data-ttu-id="40227-240">Hello rozmiar jest obliczany poprzez zliczanie sterowania wszystkie znaki oprócz UNICODE znaków (segmenty C0 i C1) i miejsca `' '` po wyświetleniu poza stałą typu string.</span><span class="sxs-lookup"><span data-stu-id="40227-240">hello size is computed by counting all characters excluding UNICODE control characters (segments C0 and C1) and space `' '` when it appears outside of a string constant.</span></span>
<span data-ttu-id="40227-241">Centrum IoT z powodu błędu odrzuca wszystkie operacje, które spowoduje zwiększenie rozmiaru hello tych dokumentów przekracza hello limit.</span><span class="sxs-lookup"><span data-stu-id="40227-241">IoT Hub rejects with an error all operations that would increase hello size of those documents above hello limit.</span></span>

## <a name="device-twin-metadata"></a><span data-ttu-id="40227-242">Metadane dwie urządzenia</span><span class="sxs-lookup"><span data-stu-id="40227-242">Device twin metadata</span></span>
<span data-ttu-id="40227-243">Centrum IoT przechowuje hello sygnatura czasowa hello ostatniej aktualizacji dla każdego obiektu JSON w dwie urządzenia żądanego i podać właściwości.</span><span class="sxs-lookup"><span data-stu-id="40227-243">IoT Hub maintains hello timestamp of hello last update for each JSON object in device twin desired and reported properties.</span></span> <span data-ttu-id="40227-244">sygnatury czasowe Hello są w UTC i kodowany w hello [ISO8601] format `YYYY-MM-DDTHH:MM:SS.mmmZ`.</span><span class="sxs-lookup"><span data-stu-id="40227-244">hello timestamps are in UTC and encoded in hello [ISO8601] format `YYYY-MM-DDTHH:MM:SS.mmmZ`.</span></span>
<span data-ttu-id="40227-245">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="40227-245">For example:</span></span>

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

<span data-ttu-id="40227-246">Ta informacja jest przechowywana w każdej poziomu aktualizacji toopreserve (nie tylko hello liśćmi hello strukturze JSON), które usunąć klucze obiektu.</span><span class="sxs-lookup"><span data-stu-id="40227-246">This information is kept at every level (not just hello leaves of hello JSON structure) toopreserve updates that remove object keys.</span></span>

## <a name="optimistic-concurrency"></a><span data-ttu-id="40227-247">Optymistycznej współbieżności</span><span class="sxs-lookup"><span data-stu-id="40227-247">Optimistic concurrency</span></span>
<span data-ttu-id="40227-248">Tagi, potrzeby i podać właściwości wszystkich optymistycznej współbieżności pomocy technicznej.</span><span class="sxs-lookup"><span data-stu-id="40227-248">Tags, desired, and reported properties all support optimistic concurrency.</span></span>
<span data-ttu-id="40227-249">Tagi przypada tag ETag jako [RFC7232], reprezentujący reprezentacja JSON hello tagu.</span><span class="sxs-lookup"><span data-stu-id="40227-249">Tags have an ETag, as per [RFC7232], that represents hello tag's JSON representation.</span></span> <span data-ttu-id="40227-250">Elementy etag można użyć w operacjach aktualizowania warunkowego z hello rozwiązania zaplecza tooensure spójności.</span><span class="sxs-lookup"><span data-stu-id="40227-250">You can use ETags in conditional update operations from hello solution back end tooensure consistency.</span></span>

<span data-ttu-id="40227-251">Dwie urządzenia żądanego i podać właściwości nie ma elementy etag, ale `$version` wartość, która jest gwarantowana toobe przyrostowe.</span><span class="sxs-lookup"><span data-stu-id="40227-251">Device twin desired and reported properties do not have ETags, but have a `$version` value that is guaranteed toobe incremental.</span></span> <span data-ttu-id="40227-252">Podobnie tooan ETag, wersja hello mogą być używane przez hello aktualizowanie spójności tooenforce strona aktualizacji.</span><span class="sxs-lookup"><span data-stu-id="40227-252">Similarly tooan ETag, hello version can be used by hello updating party tooenforce consistency of updates.</span></span> <span data-ttu-id="40227-253">Na przykład aplikacji urządzenia dla zgłoszonego właściwości lub hello zaplecza rozwiązania dla żądanej właściwości.</span><span class="sxs-lookup"><span data-stu-id="40227-253">For example, a device app for a reported property or hello solution back end for a desired property.</span></span>

<span data-ttu-id="40227-254">Wersje są także przydatne, gdy observing agenta (np. aplikacji urządzenia hello obserwowania właściwości hello żądanego) należy uzgodnić szczepy między hello wynik operacji pobierania i powiadomienie o aktualizacji.</span><span class="sxs-lookup"><span data-stu-id="40227-254">Versions are also useful when an observing agent (such as hello device app observing hello desired properties) must reconcile races between hello result of a retrieve operation and an update notification.</span></span> <span data-ttu-id="40227-255">Witaj sekcji [przepływu ponowne łączenie urządzenia] [ lnk-reconnection] zawiera więcej informacji.</span><span class="sxs-lookup"><span data-stu-id="40227-255">hello section [Device reconnection flow][lnk-reconnection] provides more information.</span></span>

## <a name="device-reconnection-flow"></a><span data-ttu-id="40227-256">Przepływ ponowne nawiązanie połączenia urządzenia</span><span class="sxs-lookup"><span data-stu-id="40227-256">Device reconnection flow</span></span>
<span data-ttu-id="40227-257">Centrum IoT nie zachowa powiadomienia o aktualizacji odpowiednie właściwości dla urządzeń bez połączenia.</span><span class="sxs-lookup"><span data-stu-id="40227-257">IoT Hub does not preserve desired properties update notifications for disconnected devices.</span></span> <span data-ttu-id="40227-258">Wynika, że urządzenia, które nawiązuje połączenie musi pobrać hello pełne odpowiednie właściwości dokument w toosubscribing dodanie powiadomień aktualizacji.</span><span class="sxs-lookup"><span data-stu-id="40227-258">It follows that a device that is connecting must retrieve hello full desired properties document, in addition toosubscribing for update notifications.</span></span> <span data-ttu-id="40227-259">Biorąc pod uwagę możliwość hello szczepy między powiadomienia o aktualizacji i pobieranie pełnej, należy zapewnić hello następującego przepływu:</span><span class="sxs-lookup"><span data-stu-id="40227-259">Given hello possibility of races between update notifications and full retrieval, hello following flow must be ensured:</span></span>

1. <span data-ttu-id="40227-260">Aplikacji urządzenia łączy tooan Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="40227-260">Device app connects tooan IoT hub.</span></span>
2. <span data-ttu-id="40227-261">Subskrybuje aplikacji urządzenia dla żądanej właściwości powiadomienia o aktualizacji.</span><span class="sxs-lookup"><span data-stu-id="40227-261">Device app subscribes for desired properties update notifications.</span></span>
3. <span data-ttu-id="40227-262">Aplikacji urządzenia pobiera hello pełnego dokumentu dla żądanej właściwości.</span><span class="sxs-lookup"><span data-stu-id="40227-262">Device app retrieves hello full document for desired properties.</span></span>

<span data-ttu-id="40227-263">zignorować wszystkie powiadomienia z aplikacji urządzenia Hello `$version` mniejsza lub równa niż wersja hello hello pełnego dokumentu pobrane.</span><span class="sxs-lookup"><span data-stu-id="40227-263">hello device app can ignore all notifications with `$version` less or equal than hello version of hello full retrieved document.</span></span> <span data-ttu-id="40227-264">Takie podejście jest możliwa, ponieważ gwarantuje Centrum IoT wersje zawsze zwiększyć.</span><span class="sxs-lookup"><span data-stu-id="40227-264">This approach is possible because IoT Hub guarantees that versions always increment.</span></span>

> [!NOTE]
> <span data-ttu-id="40227-265">Istotą takiej logiki jest już zaimplementowany w hello [urządzenia Azure IoT SDK][lnk-sdks].</span><span class="sxs-lookup"><span data-stu-id="40227-265">This logic is already implemented in hello [Azure IoT device SDKs][lnk-sdks].</span></span> <span data-ttu-id="40227-266">Ten opis jest przydatny tylko wtedy, gdy hello aplikacji urządzenia nie można użyć dowolnego urządzenia Azure IoT zestawy SDK i musi program hello MQTT interfejsu bezpośrednio.</span><span class="sxs-lookup"><span data-stu-id="40227-266">This description is useful only if hello device app cannot use any of Azure IoT device SDKs and must program hello MQTT interface directly.</span></span>
> 
> 

## <a name="additional-reference-material"></a><span data-ttu-id="40227-267">Odwołanie dodatkowe materiały</span><span class="sxs-lookup"><span data-stu-id="40227-267">Additional reference material</span></span>
<span data-ttu-id="40227-268">Inne tematy referencyjne w hello Centrum IoT — przewodnik dewelopera obejmują:</span><span class="sxs-lookup"><span data-stu-id="40227-268">Other reference topics in hello IoT Hub developer guide include:</span></span>

* <span data-ttu-id="40227-269">Witaj [punkty końcowe Centrum IoT] [ lnk-endpoints] hello opisano różne punkty końcowe, które udostępnia każdego centrum IoT dla operacji zarządzania i środowiska wykonawczego.</span><span class="sxs-lookup"><span data-stu-id="40227-269">hello [IoT Hub endpoints][lnk-endpoints] article describes hello various endpoints that each IoT hub exposes for run-time and management operations.</span></span>
* <span data-ttu-id="40227-270">Witaj [ograniczenia przepustowości i przydziały] [ lnk-quotas] przydziały hello, stosowane toohello usługi IoT Hub, które hello ograniczania tooexpect zachowanie, gdy używasz usługi hello artykule.</span><span class="sxs-lookup"><span data-stu-id="40227-270">hello [Throttling and quotas][lnk-quotas] article describes hello quotas that apply toohello IoT Hub service and hello throttling behavior tooexpect when you use hello service.</span></span>
* <span data-ttu-id="40227-271">Witaj [zestawów SDK urządzeń i usług Azure IoT] [ lnk-sdks] list artykułu hello różnych SDK języka można używać podczas opracowywania aplikacji usług i urządzeń, które współdziałają z Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="40227-271">hello [Azure IoT device and service SDKs][lnk-sdks] article lists hello various language SDKs you can use when you develop both device and service apps that interact with IoT Hub.</span></span>
* <span data-ttu-id="40227-272">Witaj [Centrum IoT zapytania języka twins urządzenia, zadania i rozsyłania wiadomości] [ lnk-query] artykule hello tooretrieve informacji z Centrum IoT temat zadań i twins urządzenia można używać języka kwerend Centrum IoT .</span><span class="sxs-lookup"><span data-stu-id="40227-272">hello [IoT Hub query language for device twins, jobs, and message routing][lnk-query] article describes hello IoT Hub query language you can use tooretrieve information from IoT Hub about your device twins and jobs.</span></span>
* <span data-ttu-id="40227-273">Witaj [Obsługa MQTT Centrum IoT] [ lnk-devguide-mqtt] artykuł zawiera więcej informacji na temat Centrum IoT obsługę protokołu MQTT hello.</span><span class="sxs-lookup"><span data-stu-id="40227-273">hello [IoT Hub MQTT support][lnk-devguide-mqtt] article provides more information about IoT Hub support for hello MQTT protocol.</span></span>

## <a name="next-steps"></a><span data-ttu-id="40227-274">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="40227-274">Next steps</span></span>
<span data-ttu-id="40227-275">Teraz wiesz już, o twins urządzenia, mogą być zainteresowane hello następujące tematy przewodnik dewelopera Centrum IoT:</span><span class="sxs-lookup"><span data-stu-id="40227-275">Now you have learned about device twins, you may be interested in hello following IoT Hub developer guide topics:</span></span>

* <span data-ttu-id="40227-276">[Wywoływanie metody bezpośrednio na urządzeniu][lnk-methods]</span><span class="sxs-lookup"><span data-stu-id="40227-276">[Invoke a direct method on a device][lnk-methods]</span></span>
* <span data-ttu-id="40227-277">[Planowanie zadań na wielu urządzeniach][lnk-jobs]</span><span class="sxs-lookup"><span data-stu-id="40227-277">[Schedule jobs on multiple devices][lnk-jobs]</span></span>

<span data-ttu-id="40227-278">Jeśli chcesz tootry niektórych hello pojęcia opisane w tym artykule, mogą być zainteresowane hello następujące samouczki Centrum IoT:</span><span class="sxs-lookup"><span data-stu-id="40227-278">If you would like tootry out some of hello concepts described in this article, you may be interested in hello following IoT Hub tutorials:</span></span>

* <span data-ttu-id="40227-279">[Jak toouse Witaj dwie urządzenia][lnk-twin-tutorial]</span><span class="sxs-lookup"><span data-stu-id="40227-279">[How toouse hello device twin][lnk-twin-tutorial]</span></span>
* <span data-ttu-id="40227-280">[Jak urządzenia toouse dwie właściwości][lnk-twin-properties]</span><span class="sxs-lookup"><span data-stu-id="40227-280">[How toouse device twin properties][lnk-twin-properties]</span></span>

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
