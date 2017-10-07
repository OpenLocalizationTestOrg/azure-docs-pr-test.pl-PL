---
title: "aaaGet pracę z Centrum IoT Azure (węzeł) | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak urządzenia chmury toosend wiadomości tooAzure Centrum IoT przy użyciu IoT zestawy SDK dla środowiska Node.js. Utworzyć symulowane urządzenie i tooregister aplikacji usługi, urządzenia, wysyłania wiadomości i odczytywać wiadomości z Centrum IoT."
services: iot-hub
documentationcenter: nodejs
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 56618522-9a31-42c6-94bf-55e2233b39ac
ms.service: iot-hub
ms.devlang: javascript
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/22/2017
ms.author: dobett
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: d0747895365f2359a9c38ea1e85a5881d6efec0b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="connect-your-simulated-device-tooyour-iot-hub-using-node"></a><span data-ttu-id="1eb89-104">Połącz z Centrum IoT tooyour symulowane urządzenie za pomocą węzła</span><span class="sxs-lookup"><span data-stu-id="1eb89-104">Connect your simulated device tooyour IoT hub using Node</span></span>
[!INCLUDE [iot-hub-selector-get-started](../../includes/iot-hub-selector-get-started.md)]

<span data-ttu-id="1eb89-105">Na końcu hello tego samouczka masz trzech aplikacji konsoli Node.js:</span><span class="sxs-lookup"><span data-stu-id="1eb89-105">At hello end of this tutorial, you have three Node.js console apps:</span></span>

* <span data-ttu-id="1eb89-106">**CreateDeviceIdentity.js**, co powoduje tożsamości urządzenia i skojarzony klucz tooconnect aplikacji symulowane urządzenie.</span><span class="sxs-lookup"><span data-stu-id="1eb89-106">**CreateDeviceIdentity.js**, which creates a device identity and associated security key tooconnect your simulated device app.</span></span>
* <span data-ttu-id="1eb89-107">**ReadDeviceToCloudMessages.js**, który zawiera dane telemetryczne hello wysyłane przez aplikację symulowane urządzenie.</span><span class="sxs-lookup"><span data-stu-id="1eb89-107">**ReadDeviceToCloudMessages.js**, which displays hello telemetry sent by your simulated device app.</span></span>
* <span data-ttu-id="1eb89-108">**SimulatedDevice.js**, która łączy się tooyour Centrum IoT z tożsamości urządzenia hello utworzony wcześniej i wysyła komunikat telemetrii co drugi przy użyciu hello MQTT protokołu.</span><span class="sxs-lookup"><span data-stu-id="1eb89-108">**SimulatedDevice.js**, which connects tooyour IoT hub with hello device identity created earlier, and sends a telemetry message every second using hello MQTT protocol.</span></span>

> [!NOTE]
> <span data-ttu-id="1eb89-109">Artykuł Hello [Azure IoT SDK] [ lnk-hub-sdks] zawiera informacje o hello Azure IoT SDK, której można toobuild toorun zarówno aplikacje na urządzeniach i z zaplecza rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="1eb89-109">hello article [Azure IoT SDKs][lnk-hub-sdks] provides information about hello Azure IoT SDKs that you can use toobuild both applications toorun on devices and your solution back end.</span></span>
> 
> 

<span data-ttu-id="1eb89-110">toocomplete tego samouczka należy hello następujące:</span><span class="sxs-lookup"><span data-stu-id="1eb89-110">toocomplete this tutorial, you need hello following:</span></span>

* <span data-ttu-id="1eb89-111">Środowisko Node.js w wersji 0.10.x lub nowszej.</span><span class="sxs-lookup"><span data-stu-id="1eb89-111">Node.js version 0.10.x or later.</span></span>
* <span data-ttu-id="1eb89-112">Aktywne konto platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="1eb89-112">An active Azure account.</span></span> <span data-ttu-id="1eb89-113">(Jeśli go nie masz, możesz utworzyć [bezpłatne konto próbne][lnk-free-trial] w zaledwie kilka minut).</span><span class="sxs-lookup"><span data-stu-id="1eb89-113">(If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.)</span></span>

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

<span data-ttu-id="1eb89-114">Utworzono centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="1eb89-114">You have now created your IoT hub.</span></span> <span data-ttu-id="1eb89-115">Masz hello nazwy hosta Centrum IoT i hello parametry połączenia Centrum IoT należy toocomplete hello pozostałej części tego samouczka.</span><span class="sxs-lookup"><span data-stu-id="1eb89-115">You have hello IoT Hub host name and hello IoT Hub connection string that you need toocomplete hello rest of this tutorial.</span></span>

## <a name="create-a-device-identity"></a><span data-ttu-id="1eb89-116">Tworzenie tożsamości urządzenia</span><span class="sxs-lookup"><span data-stu-id="1eb89-116">Create a device identity</span></span>
<span data-ttu-id="1eb89-117">W tej sekcji utworzysz aplikację konsoli Node.js, która tworzy tożsamość urządzenia w rejestrze tożsamości hello w Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="1eb89-117">In this section, you create a Node.js console app that creates a device identity in hello identity registry in your IoT hub.</span></span> <span data-ttu-id="1eb89-118">Urządzenie można połączyć tylko tooIoT koncentratora, jeśli zawiera on wpis w rejestrze tożsamości hello.</span><span class="sxs-lookup"><span data-stu-id="1eb89-118">A device can only connect tooIoT hub if it has an entry in hello identity registry.</span></span> <span data-ttu-id="1eb89-119">Aby uzyskać więcej informacji, zobacz hello **rejestru tożsamości** sekcji hello [Centrum IoT — przewodnik dewelopera][lnk-devguide-identity].</span><span class="sxs-lookup"><span data-stu-id="1eb89-119">For more information, see hello **Identity Registry** section of hello [IoT Hub developer guide][lnk-devguide-identity].</span></span> <span data-ttu-id="1eb89-120">Po uruchomieniu tej aplikacji konsoli, generuje on unikatowy identyfikator urządzenia i tooIoT Centrum wiadomości klucz urządzenia można użyć tooidentify się podczas wysyłania urządzenia do chmury.</span><span class="sxs-lookup"><span data-stu-id="1eb89-120">When you run this console app, it generates a unique device ID and key that your device can use tooidentify itself when it sends device-to-cloud messages tooIoT Hub.</span></span>

1. <span data-ttu-id="1eb89-121">Utwórz nowy pusty folder o nazwie **createdeviceidentity**.</span><span class="sxs-lookup"><span data-stu-id="1eb89-121">Create a new empty folder called **createdeviceidentity**.</span></span> <span data-ttu-id="1eb89-122">W hello **createdeviceidentity** folderu, Utwórz plik package.json za pomocą hello następujące polecenie z wiersza polecenia.</span><span class="sxs-lookup"><span data-stu-id="1eb89-122">In hello **createdeviceidentity** folder, create a package.json file using hello following command at your command prompt.</span></span> <span data-ttu-id="1eb89-123">Zaakceptuj wszystkie domyślne hello:</span><span class="sxs-lookup"><span data-stu-id="1eb89-123">Accept all hello defaults:</span></span>
   
    ```
    npm init
    ```
2. <span data-ttu-id="1eb89-124">Z wiersza polecenia w hello **createdeviceidentity** folderu, uruchom następujące polecenie tooinstall hello hello **Centrum iothub azure** pakiet SDK usługi:</span><span class="sxs-lookup"><span data-stu-id="1eb89-124">At your command prompt in hello **createdeviceidentity** folder, run hello following command tooinstall hello **azure-iothub** Service SDK package:</span></span>
   
    ```
    npm install azure-iothub --save
    ```
3. <span data-ttu-id="1eb89-125">Za pomocą edytora tekstu, Utwórz **CreateDeviceIdentity.js** pliku w hello **createdeviceidentity** folderu.</span><span class="sxs-lookup"><span data-stu-id="1eb89-125">Using a text editor, create a **CreateDeviceIdentity.js** file in hello **createdeviceidentity** folder.</span></span>
4. <span data-ttu-id="1eb89-126">Dodaj następujące hello `require` instrukcji na początku hello hello **CreateDeviceIdentity.js** pliku:</span><span class="sxs-lookup"><span data-stu-id="1eb89-126">Add hello following `require` statement at hello start of hello **CreateDeviceIdentity.js** file:</span></span>
   
    ```
    'use strict';
   
    var iothub = require('azure-iothub');
    ```
5. <span data-ttu-id="1eb89-127">Dodaj hello następującego kodu toohello **CreateDeviceIdentity.js** plików i Zastąp wartości symbolu zastępczego hello hello Centrum IoT parametry połączenia dla koncentratora hello utworzony w poprzedniej sekcji hello:</span><span class="sxs-lookup"><span data-stu-id="1eb89-127">Add hello following code toohello **CreateDeviceIdentity.js** file and replace hello placeholder value with hello IoT Hub connection string for hello hub you created in hello previous section:</span></span> 
   
    ```
    var connectionString = '{iothub connection string}';
   
    var registry = iothub.Registry.fromConnectionString(connectionString);
    ```
6. <span data-ttu-id="1eb89-128">Dodaj hello następującego kodu toocreate definicję urządzenia w rejestrze tożsamości hello w Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="1eb89-128">Add hello following code toocreate a device definition in hello identity registry in your IoT hub.</span></span> <span data-ttu-id="1eb89-129">Ten kod tworzy urządzenia, jeśli identyfikator urządzenia hello nie istnieje w rejestrze tożsamości hello, w przeciwnym razie zwraca wartość klucza hello hello istniejące urządzenia:</span><span class="sxs-lookup"><span data-stu-id="1eb89-129">This code creates a device if hello device ID does not exist in hello identity registry, otherwise it returns hello key of hello existing device:</span></span>
   
    ```
    var device = {
      deviceId: 'myFirstNodeDevice'
    }
    registry.create(device, function(err, deviceInfo, res) {
      if (err) {
        registry.get(device.deviceId, printDeviceInfo);
      }
      if (deviceInfo) {
        printDeviceInfo(err, deviceInfo, res)
      }
    });
   
    function printDeviceInfo(err, deviceInfo, res) {
      if (deviceInfo) {
        console.log('Device ID: ' + deviceInfo.deviceId);
        console.log('Device key: ' + deviceInfo.authentication.symmetricKey.primaryKey);
      }
    }
    ```
   [!INCLUDE [iot-hub-pii-note-naming-device](../../includes/iot-hub-pii-note-naming-device.md)]

7. <span data-ttu-id="1eb89-130">Zapisz i zamknij plik **CreateDeviceIdentity.js**.</span><span class="sxs-lookup"><span data-stu-id="1eb89-130">Save and close **CreateDeviceIdentity.js** file.</span></span>
8. <span data-ttu-id="1eb89-131">Witaj toorun **createdeviceidentity** aplikacji, wykonaj następujące polecenie w wierszu polecenia hello w folderze createdeviceidentity hello hello:</span><span class="sxs-lookup"><span data-stu-id="1eb89-131">toorun hello **createdeviceidentity** application, execute hello following command at hello command prompt in hello createdeviceidentity folder:</span></span>
   
    ```
    node CreateDeviceIdentity.js 
    ```
9. <span data-ttu-id="1eb89-132">Zanotuj hello **identyfikator urządzenia** i **klucza urządzenia**.</span><span class="sxs-lookup"><span data-stu-id="1eb89-132">Make a note of hello **Device ID** and **Device key**.</span></span> <span data-ttu-id="1eb89-133">Należy te wartości później podczas tworzenia aplikacji, która łączy tooIoT koncentratora jako urządzenie.</span><span class="sxs-lookup"><span data-stu-id="1eb89-133">You need these values later when you create an application that connects tooIoT Hub as a device.</span></span>

> [!NOTE]
> <span data-ttu-id="1eb89-134">Witaj w rejestrze tożsamości Centrum IoT przechowuje dane tylko Centrum IoT toohello bezpiecznego dostępu tooenable tożsamości urządzenia.</span><span class="sxs-lookup"><span data-stu-id="1eb89-134">hello IoT Hub identity registry only stores device identities tooenable secure access toohello IoT hub.</span></span> <span data-ttu-id="1eb89-135">Urządzenie toouse identyfikatorów i klucze są przechowywane jako poświadczeń zabezpieczeń i flagi włączone/wyłączone, której można toodisable dostępu dla poszczególnych urządzeń.</span><span class="sxs-lookup"><span data-stu-id="1eb89-135">It stores device IDs and keys toouse as security credentials and an enabled/disabled flag that you can use toodisable access for an individual device.</span></span> <span data-ttu-id="1eb89-136">Jeśli aplikacja wymaga toostore inne metadane specyficzne dla urządzenia, należy go użyć magazynu specyficzne dla aplikacji.</span><span class="sxs-lookup"><span data-stu-id="1eb89-136">If your application needs toostore other device-specific metadata, it should use an application-specific store.</span></span> <span data-ttu-id="1eb89-137">Aby uzyskać więcej informacji, zobacz hello [Centrum IoT — przewodnik dewelopera][lnk-devguide-identity].</span><span class="sxs-lookup"><span data-stu-id="1eb89-137">For more information, see hello [IoT Hub developer guide][lnk-devguide-identity].</span></span>
> 
> 

<a id="D2C_node"></a>
## <a name="receive-device-to-cloud-messages"></a><span data-ttu-id="1eb89-138">Odbieranie komunikatów z urządzenia do chmury</span><span class="sxs-lookup"><span data-stu-id="1eb89-138">Receive device-to-cloud messages</span></span>
<span data-ttu-id="1eb89-139">W tej sekcji opisano tworzenie aplikacji konsolowej środowiska Node.js, która odczytuje komunikaty z urządzenia do chmury z usługi IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="1eb89-139">In this section, you create a Node.js console app that reads device-to-cloud messages from IoT Hub.</span></span> <span data-ttu-id="1eb89-140">Przedstawia Centrum IoT [usługi Event Hubs][lnk-event-hubs-overview]— tooenable zgodne punktu końcowego można tooread wiadomości urządzenia do chmury.</span><span class="sxs-lookup"><span data-stu-id="1eb89-140">An IoT hub exposes an [Event Hubs][lnk-event-hubs-overview]-compatible endpoint tooenable you tooread device-to-cloud messages.</span></span> <span data-ttu-id="1eb89-141">elementy tookeep proste, w tym samouczku tworzy podstawowe reader, który nie jest odpowiedni dla wdrożenia wysokiej przepływności.</span><span class="sxs-lookup"><span data-stu-id="1eb89-141">tookeep things simple, this tutorial creates a basic reader that is not suitable for a high throughput deployment.</span></span> <span data-ttu-id="1eb89-142">Witaj [przetwarzania komunikatów urządzenia do chmury] [ lnk-process-d2c-tutorial] samouczek pokazuje, jak urządzenia chmury tooprocess komunikatów na dużą skalę.</span><span class="sxs-lookup"><span data-stu-id="1eb89-142">hello [Process device-to-cloud messages][lnk-process-d2c-tutorial] tutorial shows you how tooprocess device-to-cloud messages at scale.</span></span> <span data-ttu-id="1eb89-143">Witaj [Rozpoczynanie pracy z usługą Event Hubs] [ lnk-eventhubs-tutorial] samouczek zawiera dalsze informacje dotyczące sposobu tooprocess komunikaty z usługi Event Hubs i jest toohello odpowiednich punktów końcowych zgodnych z Centrum IoT Centrum zdarzeń.</span><span class="sxs-lookup"><span data-stu-id="1eb89-143">hello [Get Started with Event Hubs][lnk-eventhubs-tutorial] tutorial provides further information on how tooprocess messages from Event Hubs and is applicable toohello IoT Hub Event Hub-compatible endpoints.</span></span>

> [!NOTE]
> <span data-ttu-id="1eb89-144">Hello punktu końcowego Centrum zdarzeń zgodnych do odczytywania wiadomości urządzenia do chmury zawsze używa protokołu AMQP hello.</span><span class="sxs-lookup"><span data-stu-id="1eb89-144">hello Event Hub-compatible endpoint for reading device-to-cloud messages always uses hello AMQP protocol.</span></span>
> 
> 

1. <span data-ttu-id="1eb89-145">Utwórz pusty folder o nazwie **readdevicetocloudmessages**.</span><span class="sxs-lookup"><span data-stu-id="1eb89-145">Create an empty folder called **readdevicetocloudmessages**.</span></span> <span data-ttu-id="1eb89-146">W hello **readdevicetocloudmessages** folderu, Utwórz plik package.json za pomocą hello następujące polecenie z wiersza polecenia.</span><span class="sxs-lookup"><span data-stu-id="1eb89-146">In hello **readdevicetocloudmessages** folder, create a package.json file using hello following command at your command prompt.</span></span> <span data-ttu-id="1eb89-147">Zaakceptuj wszystkie domyślne hello:</span><span class="sxs-lookup"><span data-stu-id="1eb89-147">Accept all hello defaults:</span></span>
   
    ```
    npm init
    ```
2. <span data-ttu-id="1eb89-148">Z wiersza polecenia w hello **readdevicetocloudmessages** folderu, uruchom następujące polecenie tooinstall hello hello **usługi centra zdarzeń azure** pakietu:</span><span class="sxs-lookup"><span data-stu-id="1eb89-148">At your command prompt in hello **readdevicetocloudmessages** folder, run hello following command tooinstall hello **azure-event-hubs** package:</span></span>
   
    ```
    npm install azure-event-hubs --save
    ```
3. <span data-ttu-id="1eb89-149">Za pomocą edytora tekstu, Utwórz **ReadDeviceToCloudMessages.js** pliku w hello **readdevicetocloudmessages** folderu.</span><span class="sxs-lookup"><span data-stu-id="1eb89-149">Using a text editor, create a **ReadDeviceToCloudMessages.js** file in hello **readdevicetocloudmessages** folder.</span></span>
4. <span data-ttu-id="1eb89-150">Dodaj następujące hello `require` instrukcje na powitania początek hello **ReadDeviceToCloudMessages.js** pliku:</span><span class="sxs-lookup"><span data-stu-id="1eb89-150">Add hello following `require` statements at hello start of hello **ReadDeviceToCloudMessages.js** file:</span></span>
   
    ```
    'use strict';
   
    var EventHubClient = require('azure-event-hubs').Client;
    ```
5. <span data-ttu-id="1eb89-151">Dodaj powitania po deklaracji zmiennej i zastąp wartość symbolu zastępczego hello hello parametry połączenia Centrum IoT Centrum:</span><span class="sxs-lookup"><span data-stu-id="1eb89-151">Add hello following variable declaration and replace hello placeholder value with hello IoT Hub connection string for your hub:</span></span>
   
    ```
    var connectionString = '{iothub connection string}';
    ```
6. <span data-ttu-id="1eb89-152">Dodaj następujące dwie funkcje, które dane wyjściowe konsoli toohello drukowaniem hello:</span><span class="sxs-lookup"><span data-stu-id="1eb89-152">Add hello following two functions that print output toohello console:</span></span>
   
    ```
    var printError = function (err) {
      console.log(err.message);
    };
   
    var printMessage = function (message) {
      console.log('Message received: ');
      console.log(JSON.stringify(message.body));
      console.log('');
    };
    ```
7. <span data-ttu-id="1eb89-153">Dodaj następującego kodu toocreate hello hello **EventHubClient**, otwórz hello tooyour połączenia Centrum IoT i tworzenie odbiornika dla każdej partycji.</span><span class="sxs-lookup"><span data-stu-id="1eb89-153">Add hello following code toocreate hello **EventHubClient**, open hello connection tooyour IoT Hub, and create a receiver for each partition.</span></span> <span data-ttu-id="1eb89-154">Ta aplikacja używa filtru podczas tworzenia odbiornika, dzięki czemu hello odbiornika odczytuje jedynie tooIoT wiadomości wysłane koncentratora po odbiornika hello zacznie działać.</span><span class="sxs-lookup"><span data-stu-id="1eb89-154">This application uses a filter when it creates a receiver so that hello receiver only reads messages sent tooIoT Hub after hello receiver starts running.</span></span> <span data-ttu-id="1eb89-155">Ten filtr jest przydatne w środowisku testowym, aby zobaczyć tylko hello bieżący zestaw komunikatów.</span><span class="sxs-lookup"><span data-stu-id="1eb89-155">This filter is useful in a test environment so you see just hello current set of messages.</span></span> <span data-ttu-id="1eb89-156">W środowisku produkcyjnym kodu upewnij się, przetwarza wszystkie wiadomości powitania.</span><span class="sxs-lookup"><span data-stu-id="1eb89-156">In a production environment, your code should make sure that it processes all hello messages.</span></span> <span data-ttu-id="1eb89-157">Aby uzyskać więcej informacji, zobacz hello [jak tooprocess Centrum IoT urządzenia do chmury wiadomości] [ lnk-process-d2c-tutorial] samouczek:</span><span class="sxs-lookup"><span data-stu-id="1eb89-157">For more information, see hello [How tooprocess IoT Hub device-to-cloud messages][lnk-process-d2c-tutorial] tutorial:</span></span>
   
    ```
    var client = EventHubClient.fromConnectionString(connectionString);
    client.open()
        .then(client.getPartitionIds.bind(client))
        .then(function (partitionIds) {
            return partitionIds.map(function (partitionId) {
                return client.createReceiver('$Default', partitionId, { 'startAfterTime' : Date.now()}).then(function(receiver) {
                    console.log('Created partition receiver: ' + partitionId)
                    receiver.on('errorReceived', printError);
                    receiver.on('message', printMessage);
                });
            });
        })
        .catch(printError);
    ```
8. <span data-ttu-id="1eb89-158">Zapisz i zamknij hello **ReadDeviceToCloudMessages.js** pliku.</span><span class="sxs-lookup"><span data-stu-id="1eb89-158">Save and close hello **ReadDeviceToCloudMessages.js** file.</span></span>

## <a name="create-a-simulated-device-app"></a><span data-ttu-id="1eb89-159">Tworzenie aplikacji symulowanego urządzenia</span><span class="sxs-lookup"><span data-stu-id="1eb89-159">Create a simulated device app</span></span>
<span data-ttu-id="1eb89-160">W tej sekcji utworzysz aplikację konsoli Node.js, która symuluje urządzenia, które wysyła Centrum IoT tooan wiadomości urządzenia do chmury.</span><span class="sxs-lookup"><span data-stu-id="1eb89-160">In this section, you create a Node.js console app that simulates a device that sends device-to-cloud messages tooan IoT hub.</span></span>

1. <span data-ttu-id="1eb89-161">Utwórz pusty folder o nazwie **simulateddevice**.</span><span class="sxs-lookup"><span data-stu-id="1eb89-161">Create an empty folder called **simulateddevice**.</span></span> <span data-ttu-id="1eb89-162">W hello **simulateddevice** folderu, Utwórz plik package.json za pomocą hello następujące polecenie z wiersza polecenia.</span><span class="sxs-lookup"><span data-stu-id="1eb89-162">In hello **simulateddevice** folder, create a package.json file using hello following command at your command prompt.</span></span> <span data-ttu-id="1eb89-163">Zaakceptuj wszystkie domyślne hello:</span><span class="sxs-lookup"><span data-stu-id="1eb89-163">Accept all hello defaults:</span></span>
   
    ```
    npm init
    ```
2. <span data-ttu-id="1eb89-164">Z wiersza polecenia w hello **simulateddevice** folderu, uruchom następujące polecenie tooinstall hello hello **azure iot urządzenia** pakiet SDK urządzenia i **azure-iot urządzenie mqtt**pakietu:</span><span class="sxs-lookup"><span data-stu-id="1eb89-164">At your command prompt in hello **simulateddevice** folder, run hello following command tooinstall hello **azure-iot-device** Device SDK package and **azure-iot-device-mqtt** package:</span></span>
   
    ```
    npm install azure-iot-device azure-iot-device-mqtt --save
    ```
3. <span data-ttu-id="1eb89-165">Za pomocą edytora tekstu, Utwórz **SimulatedDevice.js** pliku w hello **simulateddevice** folderu.</span><span class="sxs-lookup"><span data-stu-id="1eb89-165">Using a text editor, create a **SimulatedDevice.js** file in hello **simulateddevice** folder.</span></span>
4. <span data-ttu-id="1eb89-166">Dodaj następujące hello `require` instrukcje na powitania początek hello **SimulatedDevice.js** pliku:</span><span class="sxs-lookup"><span data-stu-id="1eb89-166">Add hello following `require` statements at hello start of hello **SimulatedDevice.js** file:</span></span>
   
    ```
    'use strict';
   
    var clientFromConnectionString = require('azure-iot-device-mqtt').clientFromConnectionString;
    var Message = require('azure-iot-device').Message;
    ```
5. <span data-ttu-id="1eb89-167">Dodaj **connectionString** zmiennej i korzystać z niego toocreate **klienta** wystąpienia.</span><span class="sxs-lookup"><span data-stu-id="1eb89-167">Add a **connectionString** variable and use it toocreate a **Client** instance.</span></span> <span data-ttu-id="1eb89-168">Zastąp **{youriothostname}** hello nazwę Centrum IoT hello utworzony hello *tworzenia Centrum IoT* sekcji.</span><span class="sxs-lookup"><span data-stu-id="1eb89-168">Replace **{youriothostname}** with hello name of hello IoT hub you created hello *Create an IoT Hub* section.</span></span> <span data-ttu-id="1eb89-169">Zastąp **{yourdevicekey}** o wartości klucza urządzenia hello wygenerowanych w hello *tworzenie tożsamości urządzenia* sekcji:</span><span class="sxs-lookup"><span data-stu-id="1eb89-169">Replace **{yourdevicekey}** with hello device key value you generated in hello *Create a device identity* section:</span></span>
   
    ```
    var connectionString = 'HostName={youriothostname};DeviceId=myFirstNodeDevice;SharedAccessKey={yourdevicekey}';
   
    var client = clientFromConnectionString(connectionString);
    ```
6. <span data-ttu-id="1eb89-170">Dodaj następujące dane wyjściowe toodisplay funkcji z aplikacji hello hello:</span><span class="sxs-lookup"><span data-stu-id="1eb89-170">Add hello following function toodisplay output from hello application:</span></span>
   
    ```
    function printResultFor(op) {
      return function printResult(err, res) {
        if (err) console.log(op + ' error: ' + err.toString());
        if (res) console.log(op + ' status: ' + res.constructor.name);
      };
    }
    ```
7. <span data-ttu-id="1eb89-171">Tworzenie wywołania zwrotnego i użyć hello **setInterval** funkcji co sekundę toosend Centrum IoT tooyour komunikat:</span><span class="sxs-lookup"><span data-stu-id="1eb89-171">Create a callback and use hello **setInterval** function toosend a message tooyour IoT hub every second:</span></span>
   
    ```
    var connectCallback = function (err) {
      if (err) {
        console.log('Could not connect: ' + err);
      } else {
        console.log('Client connected');
   
        // Create a message and send it toohello IoT Hub every second
        setInterval(function(){
            var temperature = 20 + (Math.random() * 15);
            var humidity = 60 + (Math.random() * 20);            
            var data = JSON.stringify({ deviceId: 'myFirstNodeDevice', temperature: temperature, humidity: humidity });
            var message = new Message(data);
            message.properties.add('temperatureAlert', (temperature > 30) ? 'true' : 'false');
            console.log("Sending message: " + message.getData());
            client.sendEvent(message, printResultFor('send'));
        }, 1000);
      }
    };
    ```
8. <span data-ttu-id="1eb89-172">Otwórz tooyour połączenia hello Centrum IoT i Rozpocznij wysyłanie wiadomości:</span><span class="sxs-lookup"><span data-stu-id="1eb89-172">Open hello connection tooyour IoT Hub and start sending messages:</span></span>
   
    ```
    client.open(connectCallback);
    ```
9. <span data-ttu-id="1eb89-173">Zapisz i zamknij hello **SimulatedDevice.js** pliku.</span><span class="sxs-lookup"><span data-stu-id="1eb89-173">Save and close hello **SimulatedDevice.js** file.</span></span>

> [!NOTE]
> <span data-ttu-id="1eb89-174">rzeczy tookeep proste, w tym samouczku nie implementuje wszystkie zasady ponawiania.</span><span class="sxs-lookup"><span data-stu-id="1eb89-174">tookeep things simple, this tutorial does not implement any retry policy.</span></span> <span data-ttu-id="1eb89-175">W kodzie produkcyjnym, należy zaimplementować zasady ponawiania (na przykład wykładniczego wycofywania), zgodnie z sugestią podaną w artykuł w witrynie MSDN hello [obsługi błędów przejściowych][lnk-transient-faults].</span><span class="sxs-lookup"><span data-stu-id="1eb89-175">In production code, you should implement retry policies (such as an exponential backoff), as suggested in hello MSDN article [Transient Fault Handling][lnk-transient-faults].</span></span>
> 
> 

## <a name="run-hello-apps"></a><span data-ttu-id="1eb89-176">Uruchamianie aplikacji hello</span><span class="sxs-lookup"><span data-stu-id="1eb89-176">Run hello apps</span></span>
<span data-ttu-id="1eb89-177">Wszystko jest teraz gotowy toorun hello aplikacji.</span><span class="sxs-lookup"><span data-stu-id="1eb89-177">You are now ready toorun hello apps.</span></span>

1. <span data-ttu-id="1eb89-178">W wierszu polecenia w hello **readdevicetocloudmessages** folderu Uruchom hello następujące polecenia toobegin monitorowania Centrum IoT:</span><span class="sxs-lookup"><span data-stu-id="1eb89-178">At a command prompt in hello **readdevicetocloudmessages** folder, run hello following command toobegin monitoring your IoT hub:</span></span>
   
    ```
    node ReadDeviceToCloudMessages.js 
    ```
   
    ![Komunikaty o node.js Centrum IoT usługi aplikacji toomonitor urządzenia do chmury][7]
2. <span data-ttu-id="1eb89-180">W wierszu polecenia w hello **simulateddevice** folderu Uruchom powitania po toobegin polecenie wysyłania Centrum IoT tooyour danych telemetrii:</span><span class="sxs-lookup"><span data-stu-id="1eb89-180">At a command prompt in hello **simulateddevice** folder, run hello following command toobegin sending telemetry data tooyour IoT hub:</span></span>
   
    ```
    node SimulatedDevice.js
    ```
   
    ![Node.js Centrum IoT urządzenia aplikacji toosend urządzenia do chmury wiadomości][8]
3. <span data-ttu-id="1eb89-182">Witaj **użycia** kafelka w hello [portalu Azure] [ lnk-portal] pokazuje hello liczbę komunikatów wysłanych toohello Centrum IoT:</span><span class="sxs-lookup"><span data-stu-id="1eb89-182">hello **Usage** tile in hello [Azure portal][lnk-portal] shows hello number of messages sent toohello IoT hub:</span></span>
   
    ![Azure portalu użycie kafelka pokazujący liczbę komunikatów wysyłanych tooIoT Centrum][43]

## <a name="next-steps"></a><span data-ttu-id="1eb89-184">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="1eb89-184">Next steps</span></span>
<span data-ttu-id="1eb89-185">W tym samouczku został skonfigurowany nowego centrum IoT w portalu Azure hello i w rejestrze tożsamości Centrum IoT hello zostanie utworzona tożsamość urządzenia.</span><span class="sxs-lookup"><span data-stu-id="1eb89-185">In this tutorial, you configured a new IoT hub in hello Azure portal, and then created a device identity in hello IoT hub's identity registry.</span></span> <span data-ttu-id="1eb89-186">Użyto tego urządzenia tożsamości tooenable hello symulowane urządzenie aplikacji toosend wiadomości urządzenia do chmury toohello Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="1eb89-186">You used this device identity tooenable hello simulated device app toosend device-to-cloud messages toohello IoT hub.</span></span> <span data-ttu-id="1eb89-187">Utworzono aplikację, która wyświetla hello komunikatów odebranych przez Centrum IoT hello.</span><span class="sxs-lookup"><span data-stu-id="1eb89-187">You also created an app that displays hello messages received by hello IoT hub.</span></span> 

<span data-ttu-id="1eb89-188">toocontinue wprowadzenie do korzystania z Centrum IoT i tooexplore innych scenariuszach IoT, zobacz:</span><span class="sxs-lookup"><span data-stu-id="1eb89-188">toocontinue getting started with IoT Hub and tooexplore other IoT scenarios, see:</span></span>

* <span data-ttu-id="1eb89-189">[Łączenie urządzenia][lnk-connect-device]</span><span class="sxs-lookup"><span data-stu-id="1eb89-189">[Connecting your device][lnk-connect-device]</span></span>
* <span data-ttu-id="1eb89-190">[Wprowadzenie do zarządzania urządzeniami][lnk-device-management]</span><span class="sxs-lookup"><span data-stu-id="1eb89-190">[Getting started with device management][lnk-device-management]</span></span>
* <span data-ttu-id="1eb89-191">[Getting started with Azure IoT Edge][lnk-iot-edge] (Rozpoczynanie pracy z usługą Azure IoT Edge)</span><span class="sxs-lookup"><span data-stu-id="1eb89-191">[Getting started with Azure IoT Edge][lnk-iot-edge]</span></span>

<span data-ttu-id="1eb89-192">toolearn tooextend IoT rozwiązanie i procesu urządzenia do chmury wiadomości na dużą skalę, zobacz temat hello [przetwarzania komunikatów urządzenia do chmury] [ lnk-process-d2c-tutorial] samouczka.</span><span class="sxs-lookup"><span data-stu-id="1eb89-192">toolearn how tooextend your IoT solution and process device-to-cloud messages at scale, see hello [Process device-to-cloud messages][lnk-process-d2c-tutorial] tutorial.</span></span>
[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]


<!-- Images. -->
[7]: ./media/iot-hub-node-node-getstarted/runapp1.png
[8]: ./media/iot-hub-node-node-getstarted/runapp2.png
[43]: ./media/iot-hub-csharp-csharp-getstarted/usage.png

<!-- Links -->
[lnk-transient-faults]: https://msdn.microsoft.com/library/hh680901(v=pandp.50).aspx

[lnk-eventhubs-tutorial]: ../event-hubs/event-hubs-csharp-ephcs-getstarted.md
[lnk-devguide-identity]: iot-hub-devguide-identity-registry.md
[lnk-event-hubs-overview]: ../event-hubs/event-hubs-overview.md

[lnk-dev-setup]: https://github.com/Azure/azure-iot-sdk-node/tree/master/doc/node-devbox-setup.md
[lnk-process-d2c-tutorial]: iot-hub-csharp-csharp-process-d2c.md

[lnk-hub-sdks]: iot-hub-devguide-sdks.md
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[lnk-portal]: https://portal.azure.com/

[lnk-device-management]: iot-hub-node-node-device-management-get-started.md
[lnk-iot-edge]: iot-hub-linux-iot-edge-get-started.md
[lnk-connect-device]: https://azure.microsoft.com/develop/iot/
