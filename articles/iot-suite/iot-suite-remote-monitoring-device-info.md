---
title: "aaaDevice informacji metadanych w hello zdalne monitorowanie rozwiązania | Dokumentacja firmy Microsoft"
description: "Opis hello Azure IoT wstępnie skonfigurowane rozwiązanie monitorowania zdalnego i jego architektury."
services: 
suite: iot-suite
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 1b334769-103b-4eb0-a293-184f3d1ba9a3
ms.service: iot-suite
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/24/2017
ms.author: dobett
ms.openlocfilehash: 8387b98b8b2ae4934b0c900bc4df37dc17337c60
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="device-information-metadata-in-hello-remote-monitoring-preconfigured-solution"></a><span data-ttu-id="9582a-103">Urządzenie informacji metadanych w hello zdalne monitorowanie wstępnie skonfigurowane rozwiązanie</span><span class="sxs-lookup"><span data-stu-id="9582a-103">Device information metadata in hello remote monitoring preconfigured solution</span></span>

<span data-ttu-id="9582a-104">Hello pakiet Azure IoT zdalnego wstępnie skonfigurowane rozwiązanie monitorujące, przedstawiono podejście do zarządzania urządzeniami metadanych.</span><span class="sxs-lookup"><span data-stu-id="9582a-104">hello Azure IoT Suite remote monitoring preconfigured solution demonstrates an approach for managing device metadata.</span></span> <span data-ttu-id="9582a-105">W tym artykule przedstawiono podejście hello to rozwiązanie ma tooenable toounderstand możesz:</span><span class="sxs-lookup"><span data-stu-id="9582a-105">This article outlines hello approach this solution takes tooenable you toounderstand:</span></span>

* <span data-ttu-id="9582a-106">Jakie rozwiązania hello metadanych urządzeń są przechowywane.</span><span class="sxs-lookup"><span data-stu-id="9582a-106">What device metadata hello solution stores.</span></span>
* <span data-ttu-id="9582a-107">Sposób rozwiązania hello zarządza hello metadane urządzenia.</span><span class="sxs-lookup"><span data-stu-id="9582a-107">How hello solution manages hello device metadata.</span></span>

## <a name="context"></a><span data-ttu-id="9582a-108">Kontekst</span><span class="sxs-lookup"><span data-stu-id="9582a-108">Context</span></span>

<span data-ttu-id="9582a-109">Witaj monitorowania zdalnego wstępnie skonfigurowane rozwiązanie używa [Centrum IoT Azure] [ lnk-iot-hub] tooenable toohello danych toosend Twojego urządzenia w chmurze.</span><span class="sxs-lookup"><span data-stu-id="9582a-109">hello remote monitoring preconfigured solution uses [Azure IoT Hub][lnk-iot-hub] tooenable your devices toosend data toohello cloud.</span></span> <span data-ttu-id="9582a-110">rozwiązanie Hello przechowuje informacje o urządzeniach w trzech różnych miejscach:</span><span class="sxs-lookup"><span data-stu-id="9582a-110">hello solution stores information about devices in three different locations:</span></span>

| <span data-ttu-id="9582a-111">Lokalizacja</span><span class="sxs-lookup"><span data-stu-id="9582a-111">Location</span></span> | <span data-ttu-id="9582a-112">Informacje przechowywane</span><span class="sxs-lookup"><span data-stu-id="9582a-112">Information stored</span></span> | <span data-ttu-id="9582a-113">Wdrażanie</span><span class="sxs-lookup"><span data-stu-id="9582a-113">Implementation</span></span> |
| -------- | ------------------ | -------------- |
| <span data-ttu-id="9582a-114">Tożsamość rejestru</span><span class="sxs-lookup"><span data-stu-id="9582a-114">Identity registry</span></span> | <span data-ttu-id="9582a-115">Identyfikator urządzenia, klucze uwierzytelniania, włączony stan</span><span class="sxs-lookup"><span data-stu-id="9582a-115">Device id, authentication keys, enabled state</span></span> | <span data-ttu-id="9582a-116">Wbudowane tooIoT Centrum</span><span class="sxs-lookup"><span data-stu-id="9582a-116">Built in tooIoT Hub</span></span> |
| <span data-ttu-id="9582a-117">Twins urządzenia</span><span class="sxs-lookup"><span data-stu-id="9582a-117">Device twins</span></span> | <span data-ttu-id="9582a-118">Metadane: właściwości zgłoszone, odpowiednie właściwości, znaczniki</span><span class="sxs-lookup"><span data-stu-id="9582a-118">Metadata: reported properties, desired properties, tags</span></span> | <span data-ttu-id="9582a-119">Wbudowane tooIoT Centrum</span><span class="sxs-lookup"><span data-stu-id="9582a-119">Built in tooIoT Hub</span></span> |
| <span data-ttu-id="9582a-120">Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="9582a-120">Cosmos DB</span></span> | <span data-ttu-id="9582a-121">Historię poleceń i — metoda</span><span class="sxs-lookup"><span data-stu-id="9582a-121">Command and method history</span></span> | <span data-ttu-id="9582a-122">Niestandardowe dla rozwiązania</span><span class="sxs-lookup"><span data-stu-id="9582a-122">Custom for solution</span></span> |

<span data-ttu-id="9582a-123">Centrum IoT obejmuje [rejestrze tożsamości urządzeń] [ lnk-identity-registry] toomanage dostęp do Centrum IoT tooan i używa [twins urządzenia] [ lnk-device-twin] toomanage metadane urządzenia .</span><span class="sxs-lookup"><span data-stu-id="9582a-123">IoT Hub includes a [device identity registry][lnk-identity-registry] toomanage access tooan IoT hub and uses [device twins][lnk-device-twin] toomanage device metadata.</span></span> <span data-ttu-id="9582a-124">Istnieje również zdalnego monitorowania określonego rozwiązania *rejestru urządzenia* który przechowuje historię poleceń i metody.</span><span class="sxs-lookup"><span data-stu-id="9582a-124">There is also a remote monitoring solution-specific *device registry* that stores command and method history.</span></span> <span data-ttu-id="9582a-125">zdalne monitorowanie używa rozwiązania Hello [DB rozwiązania Cosmos] [ lnk-docdb] tooimplement bazy danych magazynu niestandardowego dla historii poleceń i metody.</span><span class="sxs-lookup"><span data-stu-id="9582a-125">hello remote monitoring solution uses a [Cosmos DB][lnk-docdb] database tooimplement a custom store for command and method history.</span></span>

> [!NOTE]
> <span data-ttu-id="9582a-126">Hello zdalnego wstępnie skonfigurowane rozwiązanie monitorujące zachowuje rejestrze tożsamości urządzeń hello zsynchronizowane z hello informacji w bazie danych DB rozwiązania Cosmos hello.</span><span class="sxs-lookup"><span data-stu-id="9582a-126">hello remote monitoring preconfigured solution keeps hello device identity registry in sync with hello information in hello Cosmos DB database.</span></span> <span data-ttu-id="9582a-127">Oba rozwiązania używają hello określenie tej samej toouniquely identyfikator urządzenia każde urządzenie podłączone tooyour Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="9582a-127">Both use hello same device id toouniquely identify each device connected tooyour IoT hub.</span></span>

## <a name="device-metadata"></a><span data-ttu-id="9582a-128">Metadane urządzenia</span><span class="sxs-lookup"><span data-stu-id="9582a-128">Device metadata</span></span>

<span data-ttu-id="9582a-129">Centrum IoT przechowuje [dwie urządzenia] [ lnk-device-twin] dla poszczególnych urządzeń fizycznych i symulowane podłączonej tooa zdalne monitorowanie rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="9582a-129">IoT Hub maintains a [device twin][lnk-device-twin] for each simulated and physical device connected tooa remote monitoring solution.</span></span> <span data-ttu-id="9582a-130">rozwiązanie Hello używa urządzenia twins toomanage hello metadane skojarzone z urządzeń.</span><span class="sxs-lookup"><span data-stu-id="9582a-130">hello solution uses device twins toomanage hello metadata associated with devices.</span></span> <span data-ttu-id="9582a-131">Dwie urządzenia jest dokumentem JSON obsługiwany przez Centrum IoT i rozwiązania hello używa hello toointeract API Centrum IoT z twins urządzenia.</span><span class="sxs-lookup"><span data-stu-id="9582a-131">A device twin is a JSON document maintained by IoT Hub, and hello solution uses hello IoT Hub API toointeract with device twins.</span></span>

<span data-ttu-id="9582a-132">Dwie urządzenia przechowuje trzy rodzaje metadanych:</span><span class="sxs-lookup"><span data-stu-id="9582a-132">A device twin stores three types of metadata:</span></span>

- <span data-ttu-id="9582a-133">*Zgłoszone właściwości* są wysyłane z Centrum IoT tooan przez urządzenie.</span><span class="sxs-lookup"><span data-stu-id="9582a-133">*Reported properties* are sent tooan IoT hub by a device.</span></span> <span data-ttu-id="9582a-134">W hello zdalnego rozwiązanie monitorujące, symulowanego urządzenia wysyłają właściwości zgłoszone podczas rozruchu, a w odpowiedzi zbyt**zmienić stan urządzenia** polecenia i metod.</span><span class="sxs-lookup"><span data-stu-id="9582a-134">In hello remote monitoring solution, simulated devices send reported properties at start-up and in response too**Change device state** commands and methods.</span></span> <span data-ttu-id="9582a-135">Można wyświetlić właściwości zgłoszone w hello **listę urządzeń** i **szczegóły urządzenia** w hello rozwiązanie portalu.</span><span class="sxs-lookup"><span data-stu-id="9582a-135">You can view reported properties in hello **Device list** and **Device details** in hello solution portal.</span></span> <span data-ttu-id="9582a-136">Zgłoszony właściwości są tylko do odczytu.</span><span class="sxs-lookup"><span data-stu-id="9582a-136">Reported properties are read only.</span></span>
- <span data-ttu-id="9582a-137">*Żądany właściwości* są pobierane z Centrum IoT hello przez urządzenia.</span><span class="sxs-lookup"><span data-stu-id="9582a-137">*Desired properties* are retrieved from hello IoT hub by devices.</span></span> <span data-ttu-id="9582a-138">Jest odpowiedzialny za hello toomake urządzenia hello żadnej konfiguracji niezbędne zmiany na urządzeniu hello.</span><span class="sxs-lookup"><span data-stu-id="9582a-138">It is hello responsibility of hello device toomake any necessary configuration change on hello device.</span></span> <span data-ttu-id="9582a-139">Jest również odpowiedzialność hello hello urządzenia tooreport hello zmiany toohello zapasowego Centrum jako właściwość zgłoszony.</span><span class="sxs-lookup"><span data-stu-id="9582a-139">It is also hello responsibility of hello device tooreport hello change back toohello hub as a reported property.</span></span> <span data-ttu-id="9582a-140">Można ustawić wartości właściwości żądaną za pośrednictwem portalu rozwiązania hello.</span><span class="sxs-lookup"><span data-stu-id="9582a-140">You can set a desired property value through hello solution portal.</span></span>
- <span data-ttu-id="9582a-141">*Tagi* istnieje tylko w Witaj dwie urządzenia i nigdy nie są synchronizowane z urządzeniem.</span><span class="sxs-lookup"><span data-stu-id="9582a-141">*Tags* only exist in hello device twin and are never synchronized with a device.</span></span> <span data-ttu-id="9582a-142">Można ustawić wartości tagów w portalu rozwiązania hello i ich używać, aby filtrować listę hello urządzeń.</span><span class="sxs-lookup"><span data-stu-id="9582a-142">You can set tag values in hello solution portal and use them when you filter hello list of devices.</span></span> <span data-ttu-id="9582a-143">rozwiązanie Hello używa również tag tooidentify hello ikona toodisplay dla urządzenia w portalu rozwiązania hello.</span><span class="sxs-lookup"><span data-stu-id="9582a-143">hello solution also uses a tag tooidentify hello icon toodisplay for a device in hello solution portal.</span></span>

<span data-ttu-id="9582a-144">Przykład zgłosił, że właściwości z urządzeń hello symulowane obejmują producenta, numer modelu szerokości geograficznej i długości.</span><span class="sxs-lookup"><span data-stu-id="9582a-144">Example reported properties from hello simulated devices include manufacturer, model number, latitude, and longitude.</span></span> <span data-ttu-id="9582a-145">Symulowane urządzeń również zwrócić hello lista metod obsługiwanych zgłoszone właściwości.</span><span class="sxs-lookup"><span data-stu-id="9582a-145">Simulated devices also return hello list of supported methods as a reported property.</span></span>

> [!NOTE]
> <span data-ttu-id="9582a-146">Witaj kodu symulowane urządzenie używa tylko hello **Desired.Config.TemperatureMeanValue** i **Desired.Config.TelemetryInterval** odpowiednie właściwości tooupdate hello zgłosił odesłał właściwości tooIoT koncentratora.</span><span class="sxs-lookup"><span data-stu-id="9582a-146">hello simulated device code only uses hello **Desired.Config.TemperatureMeanValue** and **Desired.Config.TelemetryInterval** desired properties tooupdate hello reported properties sent back tooIoT Hub.</span></span> <span data-ttu-id="9582a-147">Wszystkie inne żądanej właściwości żądania zmiany są ignorowane.</span><span class="sxs-lookup"><span data-stu-id="9582a-147">All other desired property change requests are ignored.</span></span>

<span data-ttu-id="9582a-148">Urządzenia informacji metadanych dokumentem JSON przechowywane w bazie danych programu hello urządzenia rejestru DB rozwiązania Cosmos ma hello następujące struktury:</span><span class="sxs-lookup"><span data-stu-id="9582a-148">A device information metadata JSON document stored in hello device registry Cosmos DB database has hello following structure:</span></span>

```json
{
  "DeviceProperties": {
    "DeviceID": "deviceid1",
    "HubEnabledState": null,
    "CreatedTime": "2016-04-25T23:54:01.313802Z",
    "DeviceState": "normal",
    "UpdatedTime": null
    },
  "SystemProperties": {
    "ICCID": null
  },
  "Commands": [],
  "CommandHistory": [],
  "IsSimulatedDevice": false,
  "id": "fe81a81c-bcbc-4970-81f4-7f12f2d8bda8"
}
```

> [!NOTE]
> <span data-ttu-id="9582a-149">Informacje o urządzeniu mogą obejmować metadanych toodescribe hello telemetrii hello urządzenie wysyła tooIoT koncentratora.</span><span class="sxs-lookup"><span data-stu-id="9582a-149">Device information can also include metadata toodescribe hello telemetry hello device sends tooIoT Hub.</span></span> <span data-ttu-id="9582a-150">rozwiązanie monitorowania zdalnego Hello używa tego toocustomize metadanych telemetrii sposób wyświetlania pulpitu nawigacyjnego hello [dynamiczne telemetrii][lnk-dynamic-telemetry].</span><span class="sxs-lookup"><span data-stu-id="9582a-150">hello remote monitoring solution uses this telemetry metadata toocustomize how hello dashboard displays [dynamic telemetry][lnk-dynamic-telemetry].</span></span>

## <a name="lifecycle"></a><span data-ttu-id="9582a-151">Cykl życia</span><span class="sxs-lookup"><span data-stu-id="9582a-151">Lifecycle</span></span>

<span data-ttu-id="9582a-152">Po utworzeniu urządzenia w portalu rozwiązania hello, rozwiązanie hello tworzy wpis w hello polecenie toostore bazy danych DB rozwiązania Cosmos i historii — metoda.</span><span class="sxs-lookup"><span data-stu-id="9582a-152">When you first create a device in hello solution portal, hello solution creates an entry in hello Cosmos DB database toostore command and method history.</span></span> <span data-ttu-id="9582a-153">W tym momencie rozwiązanie hello również tworzy wpis dla urządzenia hello w rejestrze tożsamości urządzeń hello, który generuje hello klucze hello urządzenie używa tooauthenticate z Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="9582a-153">At this point, hello solution also creates an entry for hello device in hello device identity registry, which generates hello keys hello device uses tooauthenticate with IoT Hub.</span></span> <span data-ttu-id="9582a-154">Tworzy dwie urządzenia.</span><span class="sxs-lookup"><span data-stu-id="9582a-154">It also creates a device twin.</span></span>

<span data-ttu-id="9582a-155">Kiedy urządzenie łączy się najpierw toohello rozwiązania, wysyła zgłoszone właściwości oraz komunikat z informacjami urządzenia.</span><span class="sxs-lookup"><span data-stu-id="9582a-155">When a device first connects toohello solution, it sends reported properties and a device information message.</span></span> <span data-ttu-id="9582a-156">Witaj zgłosił, że wartości właściwości są automatycznie zapisywane w Witaj dwie urządzenia.</span><span class="sxs-lookup"><span data-stu-id="9582a-156">hello reported property values are automatically saved in hello device twin.</span></span> <span data-ttu-id="9582a-157">Witaj zgłosił, że właściwości zawierają hello producenta urządzenia, numer modelu, numer seryjny i listę obsługiwanych metod.</span><span class="sxs-lookup"><span data-stu-id="9582a-157">hello reported properties include hello device manufacturer, model number, serial number, and a list of supported methods.</span></span> <span data-ttu-id="9582a-158">komunikat z informacjami urządzenia Hello zawiera listę hello hello poleceń, które obsługuje hello urządzenie tym informacje o żadnych parametrów polecenia.</span><span class="sxs-lookup"><span data-stu-id="9582a-158">hello device information message includes hello list of hello commands hello device supports including information about any command parameters.</span></span> <span data-ttu-id="9582a-159">Gdy rozwiązanie hello odbiera ten komunikat, aktualizuje informacje o urządzeniu hello w hello DB rozwiązania Cosmos w bazie danych.</span><span class="sxs-lookup"><span data-stu-id="9582a-159">When hello solution receives this message, it updates hello device information in hello Cosmos DB database.</span></span>

### <a name="view-and-edit-device-information-in-hello-solution-portal"></a><span data-ttu-id="9582a-160">Umożliwia wyświetlanie i edytowanie informacji o urządzeniu w portalu rozwiązania hello</span><span class="sxs-lookup"><span data-stu-id="9582a-160">View and edit device information in hello solution portal</span></span>

<span data-ttu-id="9582a-161">Witaj listy urządzenia w portalu rozwiązania hello wyświetla następujące właściwości urządzenia jako kolumny domyślnie hello: **stan**, **DeviceId**, **producenta**, **Numer modelu**, **numer seryjny**, **oprogramowania układowego**, **platformy**, **procesora**i  **Zainstalowana pamięć RAM**.</span><span class="sxs-lookup"><span data-stu-id="9582a-161">hello device list in hello solution portal displays hello following device properties as columns by default: **Status**, **DeviceId**, **Manufacturer**, **Model Number**, **Serial Number**, **Firmware**, **Platform**, **Processor**, and **Installed RAM**.</span></span> <span data-ttu-id="9582a-162">Można dostosować hello kolumn, klikając **Edytor kolumn**.</span><span class="sxs-lookup"><span data-stu-id="9582a-162">You can customize hello columns by clicking **Column editor**.</span></span> <span data-ttu-id="9582a-163">Witaj właściwości urządzenia **szerokości geograficznej** i **geograficzne** dysków na pulpicie nawigacyjnym hello hello lokalizacji w hello mapy Bing.</span><span class="sxs-lookup"><span data-stu-id="9582a-163">hello device properties **Latitude** and **Longitude** drive hello location in hello Bing Map on hello dashboard.</span></span>

![Edytor kolumn na liście urządzeń][img-device-list]

<span data-ttu-id="9582a-165">W hello **szczegóły urządzenia** okienku w portalu rozwiązania hello, można edytować odpowiednie właściwości i tagi (zgłosić właściwości są tylko do odczytu).</span><span class="sxs-lookup"><span data-stu-id="9582a-165">In hello **Device Details** pane in hello solution portal, you can edit desired properties and tags (reported properties are read only).</span></span>

![W okienku szczegółów urządzenia][img-device-edit]

<span data-ttu-id="9582a-167">Można użyć hello rozwiązanie portalu tooremove urządzenia z rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="9582a-167">You can use hello solution portal tooremove a device from your solution.</span></span> <span data-ttu-id="9582a-168">Po usunięciu urządzenia rozwiązania hello usuwa hello urządzenia wpis w rejestrze tożsamości, a następnie usuwa Witaj dwie urządzenia.</span><span class="sxs-lookup"><span data-stu-id="9582a-168">When you remove a device, hello solution removes hello device entry from identity registry and then deletes hello device twin.</span></span> <span data-ttu-id="9582a-169">Witaj rozwiązania spowoduje również usunięcie urządzenia toohello powiązane informacje z bazy danych DB rozwiązania Cosmos hello.</span><span class="sxs-lookup"><span data-stu-id="9582a-169">hello solution also removes information related toohello device from hello Cosmos DB database.</span></span> <span data-ttu-id="9582a-170">Aby móc usunąć urządzenie, należy ją wyłączyć.</span><span class="sxs-lookup"><span data-stu-id="9582a-170">Before you can remove a device, you must disable it.</span></span>

![Usuwanie urządzenia][img-device-remove]

## <a name="device-information-message-processing"></a><span data-ttu-id="9582a-172">Przetwarzanie komunikatów informacji urządzenia</span><span class="sxs-lookup"><span data-stu-id="9582a-172">Device information message processing</span></span>

<span data-ttu-id="9582a-173">Komunikaty informacyjne urządzenia wysyłane przez urządzenie różnią się od komunikatów telemetrii.</span><span class="sxs-lookup"><span data-stu-id="9582a-173">Device information messages sent by a device are distinct from telemetry messages.</span></span> <span data-ttu-id="9582a-174">Komunikaty informacyjne urządzenia obejmują hello poleceń, które urządzenia mogą odpowiadać na, a cała historia polecenia.</span><span class="sxs-lookup"><span data-stu-id="9582a-174">Device information messages include hello commands a device can respond to, and any command history.</span></span> <span data-ttu-id="9582a-175">Centrum IoT, sama nie ma informacji o metadanych hello komunikat z informacjami urządzenia i procesy hello wiadomości w hello samo przetwarza komunikat dowolnego urządzenia do chmury.</span><span class="sxs-lookup"><span data-stu-id="9582a-175">IoT Hub itself has no knowledge of hello metadata contained in a device information message and processes hello message in hello same way it processes any device-to-cloud message.</span></span> <span data-ttu-id="9582a-176">W hello zdalne monitorowanie rozwiązania [Azure Stream Analytics] [ lnk-stream-analytics] zadania (ASA) odczytuje wiadomości powitania z Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="9582a-176">In hello remote monitoring solution, an [Azure Stream Analytics][lnk-stream-analytics] (ASA) job reads hello messages from IoT Hub.</span></span> <span data-ttu-id="9582a-177">Witaj **DeviceInfo** filtry dla wiadomości, które zawierają zadania stream analytics **"ObjectType": "DeviceInfo"** i przekazuje je toohello **EventProcessorHost** hosta wystąpienie, które uruchamia zadanie sieci web.</span><span class="sxs-lookup"><span data-stu-id="9582a-177">hello **DeviceInfo** stream analytics job filters for messages that contain **"ObjectType": "DeviceInfo"** and forwards them toohello **EventProcessorHost** host instance that runs in a web job.</span></span> <span data-ttu-id="9582a-178">Logikę hello **EventProcessorHost** wystąpienie używa hello urządzenia identyfikator toofind hello DB rozwiązania Cosmos rekordu hello określonych urządzeń i aktualizacji hello rekordu.</span><span class="sxs-lookup"><span data-stu-id="9582a-178">Logic in hello **EventProcessorHost** instance uses hello device id toofind hello Cosmos DB record for hello specific device and update hello record.</span></span>

> [!NOTE]
> <span data-ttu-id="9582a-179">Komunikat z informacjami urządzenia jest standardowy komunikat urządzenia do chmury.</span><span class="sxs-lookup"><span data-stu-id="9582a-179">A device information message is a standard device-to-cloud message.</span></span> <span data-ttu-id="9582a-180">rozwiązanie Hello rozróżnia komunikaty informacyjne urządzenia i dane telemetryczne wiadomości przy użyciu ASA zapytań.</span><span class="sxs-lookup"><span data-stu-id="9582a-180">hello solution distinguishes between device information messages and telemetry messages by using ASA queries.</span></span>

## <a name="next-steps"></a><span data-ttu-id="9582a-181">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="9582a-181">Next steps</span></span>

<span data-ttu-id="9582a-182">Po zakończeniu learning, jak można dostosować hello wstępnie rozwiązania można eksplorować niektóre hello inne funkcje i możliwości rozwiązań pakiet IoT wstępnie hello:</span><span class="sxs-lookup"><span data-stu-id="9582a-182">Now you've finished learning how you can customize hello preconfigured solutions, you can explore some of hello other features and capabilities of hello IoT Suite preconfigured solutions:</span></span>

* <span data-ttu-id="9582a-183">[Omówienie rozwiązania konserwacji predykcyjnej wstępnie][lnk-predictive-overview]</span><span class="sxs-lookup"><span data-stu-id="9582a-183">[Predictive maintenance preconfigured solution overview][lnk-predictive-overview]</span></span>
* <span data-ttu-id="9582a-184">[Często zadawane pytania dotyczące Pakietu IoT][lnk-faq]</span><span class="sxs-lookup"><span data-stu-id="9582a-184">[Frequently asked questions for IoT Suite][lnk-faq]</span></span>
* <span data-ttu-id="9582a-185">[Zabezpieczenia IoT z hello tła w][lnk-security-groundup]</span><span class="sxs-lookup"><span data-stu-id="9582a-185">[IoT security from hello ground up][lnk-security-groundup]</span></span>

<!-- Images and links -->
[img-device-list]: media/iot-suite-remote-monitoring-device-info/image1.png
[img-device-edit]: media/iot-suite-remote-monitoring-device-info/image2.png
[img-device-remove]: media/iot-suite-remote-monitoring-device-info/image3.png

[lnk-iot-hub]: https://azure.microsoft.com/documentation/services/iot-hub/
[lnk-identity-registry]: ../iot-hub/iot-hub-devguide-identity-registry.md
[lnk-device-twin]: ../iot-hub/iot-hub-devguide-device-twins.md
[lnk-docdb]: https://azure.microsoft.com/documentation/services/documentdb/
[lnk-stream-analytics]: https://azure.microsoft.com/documentation/services/stream-analytics/
[lnk-dynamic-telemetry]: iot-suite-dynamic-telemetry.md

[lnk-predictive-overview]: iot-suite-predictive-overview.md
[lnk-faq]: iot-suite-faq.md
[lnk-security-groundup]: securing-iot-ground-up.md
