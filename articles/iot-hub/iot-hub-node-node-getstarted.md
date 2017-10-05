---
title: "Rozpoczęcie pracy z usługą Azure IoT Hub (Node) | Microsoft Docs"
description: "Dowiedz się, jak wysyłać komunikaty urządzenie-chmura do usługi Azure IoT Hub za pomocą zestawów SDK usługi IoT dla środowiska Node.js. Utwórz symulowane aplikacje urządzenia i usługi, aby zarejestrować urządzenie, wysyłać wiadomości i odczytywać wiadomości z usługi IoT Hub."
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
ms.openlocfilehash: b27a34c0f1f127628912ad68a002e15cc838b4d0
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
# <a name="connect-your-simulated-device-to-your-iot-hub-using-node"></a><span data-ttu-id="f12fa-104">Podłączanie symulowanego urządzenia do usługi IoT Hub za pomocą środowiska Node</span><span class="sxs-lookup"><span data-stu-id="f12fa-104">Connect your simulated device to your IoT hub using Node</span></span>
[!INCLUDE [iot-hub-selector-get-started](../../includes/iot-hub-selector-get-started.md)]

<span data-ttu-id="f12fa-105">Po ukończeniu tego samouczka będziesz mieć trzy aplikacje konsolowe środowiska Node.js:</span><span class="sxs-lookup"><span data-stu-id="f12fa-105">At the end of this tutorial, you have three Node.js console apps:</span></span>

* <span data-ttu-id="f12fa-106">**CreateDeviceIdentity.js** tworzy tożsamość urządzenia i skojarzony klucz zabezpieczeń w celu podłączenia aplikacji urządzenia symulowanego.</span><span class="sxs-lookup"><span data-stu-id="f12fa-106">**CreateDeviceIdentity.js**, which creates a device identity and associated security key to connect your simulated device app.</span></span>
* <span data-ttu-id="f12fa-107">**ReadDeviceToCloudMessages.js** powoduje wyświetlenie telemetrii wysyłanej przez aplikację urządzenia symulowanego.</span><span class="sxs-lookup"><span data-stu-id="f12fa-107">**ReadDeviceToCloudMessages.js**, which displays the telemetry sent by your simulated device app.</span></span>
* <span data-ttu-id="f12fa-108">**SimulatedDevice.js** łączy się z centrum IoT Hub przy użyciu utworzonej wcześniej tożsamości urządzenia i co sekundę wysyła komunikat telemetrii przy użyciu protokołu MQTT.</span><span class="sxs-lookup"><span data-stu-id="f12fa-108">**SimulatedDevice.js**, which connects to your IoT hub with the device identity created earlier, and sends a telemetry message every second using the MQTT protocol.</span></span>

> [!NOTE]
> <span data-ttu-id="f12fa-109">Artykuł [Azure IoT SDKs][lnk-hub-sdks] (Zestawy SDK usług Azure IoT) zawiera informacje dotyczące zestawów SDK usług Azure IoT, przy użyciu których można tworzyć aplikacje zarówno do uruchamiania na urządzaniach, jak i w zapleczu rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="f12fa-109">The article [Azure IoT SDKs][lnk-hub-sdks] provides information about the Azure IoT SDKs that you can use to build both applications to run on devices and your solution back end.</span></span>
> 
> 

<span data-ttu-id="f12fa-110">Do wykonania kroków tego samouczka niezbędne są następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="f12fa-110">To complete this tutorial, you need the following:</span></span>

* <span data-ttu-id="f12fa-111">Środowisko Node.js w wersji 0.10.x lub nowszej.</span><span class="sxs-lookup"><span data-stu-id="f12fa-111">Node.js version 0.10.x or later.</span></span>
* <span data-ttu-id="f12fa-112">Aktywne konto platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="f12fa-112">An active Azure account.</span></span> <span data-ttu-id="f12fa-113">(Jeśli go nie masz, możesz utworzyć [bezpłatne konto próbne][lnk-free-trial] w zaledwie kilka minut).</span><span class="sxs-lookup"><span data-stu-id="f12fa-113">(If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.)</span></span>

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

<span data-ttu-id="f12fa-114">Utworzono centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="f12fa-114">You have now created your IoT hub.</span></span> <span data-ttu-id="f12fa-115">Istnieje nazwa hosta usługi IoT Hub oraz parametry połączenia usługi IoT Hub potrzebne do ukończenia pozostałej części tego samouczka.</span><span class="sxs-lookup"><span data-stu-id="f12fa-115">You have the IoT Hub host name and the IoT Hub connection string that you need to complete the rest of this tutorial.</span></span>

## <a name="create-a-device-identity"></a><span data-ttu-id="f12fa-116">Tworzenie tożsamości urządzenia</span><span class="sxs-lookup"><span data-stu-id="f12fa-116">Create a device identity</span></span>
<span data-ttu-id="f12fa-117">W tej sekcji utworzysz aplikację konsolową środowiska Node.js, która tworzy tożsamość urządzenia w rejestrze tożsamości w centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="f12fa-117">In this section, you create a Node.js console app that creates a device identity in the identity registry in your IoT hub.</span></span> <span data-ttu-id="f12fa-118">Urządzenie może nawiązać połączenie z centrum IoT tylko wtedy, jeśli ma wpis w rejestrze tożsamości.</span><span class="sxs-lookup"><span data-stu-id="f12fa-118">A device can only connect to IoT hub if it has an entry in the identity registry.</span></span> <span data-ttu-id="f12fa-119">Więcej informacji znajduje się w sekcji **Identity registry** (Rejestr tożsamości) artykułu [IoT Hub developer guide][lnk-devguide-identity] (Usługa IoT Hub — przewodnik dewelopera).</span><span class="sxs-lookup"><span data-stu-id="f12fa-119">For more information, see the **Identity Registry** section of the [IoT Hub developer guide][lnk-devguide-identity].</span></span> <span data-ttu-id="f12fa-120">Po uruchomieniu ta aplikacja konsoli generuje unikatowy identyfikator urządzenia i klucz, których urządzenie może użyć do zidentyfikowania się podczas wysyłania komunikatów do chmury do usługi IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="f12fa-120">When you run this console app, it generates a unique device ID and key that your device can use to identify itself when it sends device-to-cloud messages to IoT Hub.</span></span>

1. <span data-ttu-id="f12fa-121">Utwórz nowy pusty folder o nazwie **createdeviceidentity**.</span><span class="sxs-lookup"><span data-stu-id="f12fa-121">Create a new empty folder called **createdeviceidentity**.</span></span> <span data-ttu-id="f12fa-122">W folderze **createdeviceidentity** utwórz plik package.json przy użyciu następującego polecenia z poziomu wiersza polecenia.</span><span class="sxs-lookup"><span data-stu-id="f12fa-122">In the **createdeviceidentity** folder, create a package.json file using the following command at your command prompt.</span></span> <span data-ttu-id="f12fa-123">Zaakceptuj wszystkie ustawienia domyślne:</span><span class="sxs-lookup"><span data-stu-id="f12fa-123">Accept all the defaults:</span></span>
   
    ```
    npm init
    ```
2. <span data-ttu-id="f12fa-124">Z poziomu wiersza polecenia w folderze **createdeviceidentity** uruchom następujące polecenie, aby zainstalować pakiet zestawu SDK usługi **azure-iothub**:</span><span class="sxs-lookup"><span data-stu-id="f12fa-124">At your command prompt in the **createdeviceidentity** folder, run the following command to install the **azure-iothub** Service SDK package:</span></span>
   
    ```
    npm install azure-iothub --save
    ```
3. <span data-ttu-id="f12fa-125">Za pomocą edytora tekstu utwórz plik **CreateDeviceIdentity.js** w folderze **createdeviceidentity**.</span><span class="sxs-lookup"><span data-stu-id="f12fa-125">Using a text editor, create a **CreateDeviceIdentity.js** file in the **createdeviceidentity** folder.</span></span>
4. <span data-ttu-id="f12fa-126">Dodaj następującą instrukcję `require` na początku pliku **CreateDeviceIdentity.js**:</span><span class="sxs-lookup"><span data-stu-id="f12fa-126">Add the following `require` statement at the start of the **CreateDeviceIdentity.js** file:</span></span>
   
    ```
    'use strict';
   
    var iothub = require('azure-iothub');
    ```
5. <span data-ttu-id="f12fa-127">Dodaj następujący kod do pliku **CreateDeviceIdentity.js** i zastąp wartość symbolu zastępczego parametrami połączenia usługi IoT Hub utworzonego w poprzedniej sekcji:</span><span class="sxs-lookup"><span data-stu-id="f12fa-127">Add the following code to the **CreateDeviceIdentity.js** file and replace the placeholder value with the IoT Hub connection string for the hub you created in the previous section:</span></span> 
   
    ```
    var connectionString = '{iothub connection string}';
   
    var registry = iothub.Registry.fromConnectionString(connectionString);
    ```
6. <span data-ttu-id="f12fa-128">Dodaj następujący kod, aby utworzyć definicję urządzenia w rejestrze tożsamości w centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="f12fa-128">Add the following code to create a device definition in the identity registry in your IoT hub.</span></span> <span data-ttu-id="f12fa-129">Ten kod tworzy urządzenie, jeśli identyfikator urządzenia nie istnieje w rejestrze tożsamości. W przeciwnym razie zwraca klucz istniejącego urządzenia:</span><span class="sxs-lookup"><span data-stu-id="f12fa-129">This code creates a device if the device ID does not exist in the identity registry, otherwise it returns the key of the existing device:</span></span>
   
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

7. <span data-ttu-id="f12fa-130">Zapisz i zamknij plik **CreateDeviceIdentity.js**.</span><span class="sxs-lookup"><span data-stu-id="f12fa-130">Save and close **CreateDeviceIdentity.js** file.</span></span>
8. <span data-ttu-id="f12fa-131">Aby uruchomić aplikację **createdeviceidentity**, wykonaj następujące polecenie w wierszu polecenia w folderze createdeviceidentity:</span><span class="sxs-lookup"><span data-stu-id="f12fa-131">To run the **createdeviceidentity** application, execute the following command at the command prompt in the createdeviceidentity folder:</span></span>
   
    ```
    node CreateDeviceIdentity.js 
    ```
9. <span data-ttu-id="f12fa-132">Zanotuj **identyfikator urządzenia** i **klucz urządzenia**.</span><span class="sxs-lookup"><span data-stu-id="f12fa-132">Make a note of the **Device ID** and **Device key**.</span></span> <span data-ttu-id="f12fa-133">Te wartości będą potrzebne później podczas tworzenia aplikacji, która łączy się z usługą IoT Hub jako urządzenie.</span><span class="sxs-lookup"><span data-stu-id="f12fa-133">You need these values later when you create an application that connects to IoT Hub as a device.</span></span>

> [!NOTE]
> <span data-ttu-id="f12fa-134">Rejestr tożsamości usługi IoT Hub przechowuje tożsamości urządzenia tylko po to, aby umożliwić bezpieczny dostęp do centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="f12fa-134">The IoT Hub identity registry only stores device identities to enable secure access to the IoT hub.</span></span> <span data-ttu-id="f12fa-135">Przechowuje identyfikatory i klucze urządzeń, które będą używane jako poświadczenia zabezpieczeń, oraz flagę włączone/wyłączone, która umożliwia wyłączenie dostępu do poszczególnych urządzeń.</span><span class="sxs-lookup"><span data-stu-id="f12fa-135">It stores device IDs and keys to use as security credentials and an enabled/disabled flag that you can use to disable access for an individual device.</span></span> <span data-ttu-id="f12fa-136">Jeśli aplikacja wymaga przechowywania innych metadanych dla określonego urządzenia, powinna korzystać z magazynu określonego dla aplikacji.</span><span class="sxs-lookup"><span data-stu-id="f12fa-136">If your application needs to store other device-specific metadata, it should use an application-specific store.</span></span> <span data-ttu-id="f12fa-137">Więcej informacji znajduje się w temacie [IoT Hub developer guide][lnk-devguide-identity] (Usługa IoT Hub — przewodnik dewelopera).</span><span class="sxs-lookup"><span data-stu-id="f12fa-137">For more information, see the [IoT Hub developer guide][lnk-devguide-identity].</span></span>
> 
> 

<a id="D2C_node"></a>
## <a name="receive-device-to-cloud-messages"></a><span data-ttu-id="f12fa-138">Odbieranie komunikatów z urządzenia do chmury</span><span class="sxs-lookup"><span data-stu-id="f12fa-138">Receive device-to-cloud messages</span></span>
<span data-ttu-id="f12fa-139">W tej sekcji opisano tworzenie aplikacji konsolowej środowiska Node.js, która odczytuje komunikaty z urządzenia do chmury z usługi IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="f12fa-139">In this section, you create a Node.js console app that reads device-to-cloud messages from IoT Hub.</span></span> <span data-ttu-id="f12fa-140">Usługa IoT Hub udostępnia punkt końcowy zgodny z usługą [Event Hubs][lnk-event-hubs-overview], aby umożliwić odczytywanie komunikatów z urządzenia do chmury.</span><span class="sxs-lookup"><span data-stu-id="f12fa-140">An IoT hub exposes an [Event Hubs][lnk-event-hubs-overview]-compatible endpoint to enable you to read device-to-cloud messages.</span></span> <span data-ttu-id="f12fa-141">W celu uproszczenia informacji instrukcje w samouczku dotyczą tworzenia czytnika podstawowego, który nie jest odpowiedni do wdrożenia z użyciem dużej przepustowości.</span><span class="sxs-lookup"><span data-stu-id="f12fa-141">To keep things simple, this tutorial creates a basic reader that is not suitable for a high throughput deployment.</span></span> <span data-ttu-id="f12fa-142">W samouczku [Process device-to-cloud messages (Przetwarzanie komunikatów z urządzenia do chmury)][lnk-process-d2c-tutorial] przedstawiono sposób przetwarzania komunikatów z urządzenia do chmury na dużą skalę.</span><span class="sxs-lookup"><span data-stu-id="f12fa-142">The [Process device-to-cloud messages][lnk-process-d2c-tutorial] tutorial shows you how to process device-to-cloud messages at scale.</span></span> <span data-ttu-id="f12fa-143">Samouczek [Get Started with Event Hubs (Usługa Event Hubs — wprowadzenie)][lnk-eventhubs-tutorial] zawiera dalsze informacje dotyczące sposobu przetwarzania komunikatów z usługi Event Hubs i dotyczy punktów końcowych usługi IoT Hub zgodnych z centrami zdarzeń.</span><span class="sxs-lookup"><span data-stu-id="f12fa-143">The [Get Started with Event Hubs][lnk-eventhubs-tutorial] tutorial provides further information on how to process messages from Event Hubs and is applicable to the IoT Hub Event Hub-compatible endpoints.</span></span>

> [!NOTE]
> <span data-ttu-id="f12fa-144">Punkt końcowy zgodny z centrum zdarzeń przeznaczony do odczytywania komunikatów z urządzenia do chmury zawsze korzysta z protokołu AMQP.</span><span class="sxs-lookup"><span data-stu-id="f12fa-144">The Event Hub-compatible endpoint for reading device-to-cloud messages always uses the AMQP protocol.</span></span>
> 
> 

1. <span data-ttu-id="f12fa-145">Utwórz pusty folder o nazwie **readdevicetocloudmessages**.</span><span class="sxs-lookup"><span data-stu-id="f12fa-145">Create an empty folder called **readdevicetocloudmessages**.</span></span> <span data-ttu-id="f12fa-146">W folderze **readdevicetocloudmessages** utwórz plik package.json przy użyciu następującego polecenia z poziomu wiersza polecenia.</span><span class="sxs-lookup"><span data-stu-id="f12fa-146">In the **readdevicetocloudmessages** folder, create a package.json file using the following command at your command prompt.</span></span> <span data-ttu-id="f12fa-147">Zaakceptuj wszystkie ustawienia domyślne:</span><span class="sxs-lookup"><span data-stu-id="f12fa-147">Accept all the defaults:</span></span>
   
    ```
    npm init
    ```
2. <span data-ttu-id="f12fa-148">Z poziomu wiersza polecenia w folderze **readdevicetocloudmessages** uruchom następujące polecenie, aby zainstalować pakiet **azure-event-hubs**:</span><span class="sxs-lookup"><span data-stu-id="f12fa-148">At your command prompt in the **readdevicetocloudmessages** folder, run the following command to install the **azure-event-hubs** package:</span></span>
   
    ```
    npm install azure-event-hubs --save
    ```
3. <span data-ttu-id="f12fa-149">Za pomocą edytora tekstu utwórz plik **ReadDeviceToCloudMessages.js** w folderze **readdevicetocloudmessages**.</span><span class="sxs-lookup"><span data-stu-id="f12fa-149">Using a text editor, create a **ReadDeviceToCloudMessages.js** file in the **readdevicetocloudmessages** folder.</span></span>
4. <span data-ttu-id="f12fa-150">Dodaj następujące instrukcję `require` na początku pliku **ReadDeviceToCloudMessages.js**:</span><span class="sxs-lookup"><span data-stu-id="f12fa-150">Add the following `require` statements at the start of the **ReadDeviceToCloudMessages.js** file:</span></span>
   
    ```
    'use strict';
   
    var EventHubClient = require('azure-event-hubs').Client;
    ```
5. <span data-ttu-id="f12fa-151">Dodaj następującą deklarację zmiennej i zastąp wartość symbolu zastępczego parametrami połączenia dla usługi IoT Hub:</span><span class="sxs-lookup"><span data-stu-id="f12fa-151">Add the following variable declaration and replace the placeholder value with the IoT Hub connection string for your hub:</span></span>
   
    ```
    var connectionString = '{iothub connection string}';
    ```
6. <span data-ttu-id="f12fa-152">Dodaj następujące dwie funkcje, które drukują dane wyjściowe do konsoli:</span><span class="sxs-lookup"><span data-stu-id="f12fa-152">Add the following two functions that print output to the console:</span></span>
   
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
7. <span data-ttu-id="f12fa-153">Dodaj następujący kod, aby utworzyć element **EventHubClient**, otwórz połączenie z centrum IoT, a następnie utwórz odbiornik dla każdej partycji.</span><span class="sxs-lookup"><span data-stu-id="f12fa-153">Add the following code to create the **EventHubClient**, open the connection to your IoT Hub, and create a receiver for each partition.</span></span> <span data-ttu-id="f12fa-154">Ta aplikacja używa filtru podczas tworzenia odbiornika, więc odbiornik odczytuje tylko komunikaty wysyłane do usługi Centrum IoT po uruchomieniu odbiornika.</span><span class="sxs-lookup"><span data-stu-id="f12fa-154">This application uses a filter when it creates a receiver so that the receiver only reads messages sent to IoT Hub after the receiver starts running.</span></span> <span data-ttu-id="f12fa-155">Ten filtr jest przydatny w środowisku testowym, gdyż dzięki niemu jest wyświetlany tylko bieżący zestaw komunikatów.</span><span class="sxs-lookup"><span data-stu-id="f12fa-155">This filter is useful in a test environment so you see just the current set of messages.</span></span> <span data-ttu-id="f12fa-156">W środowisku produkcyjnym kod powinien sprawdzać, czy przetwarzane są wszystkie komunikaty.</span><span class="sxs-lookup"><span data-stu-id="f12fa-156">In a production environment, your code should make sure that it processes all the messages.</span></span> <span data-ttu-id="f12fa-157">Więcej informacji znajduje się w samouczku [How to process IoT Hub device-to-cloud messages][lnk-process-d2c-tutorial] (Jak przetwarzać komunikaty z urządzenia do chmury w usłudze IoT Hub):</span><span class="sxs-lookup"><span data-stu-id="f12fa-157">For more information, see the [How to process IoT Hub device-to-cloud messages][lnk-process-d2c-tutorial] tutorial:</span></span>
   
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
8. <span data-ttu-id="f12fa-158">Zapisz i zamknij plik **ReadDeviceToCloudMessages.js**.</span><span class="sxs-lookup"><span data-stu-id="f12fa-158">Save and close the **ReadDeviceToCloudMessages.js** file.</span></span>

## <a name="create-a-simulated-device-app"></a><span data-ttu-id="f12fa-159">Tworzenie aplikacji symulowanego urządzenia</span><span class="sxs-lookup"><span data-stu-id="f12fa-159">Create a simulated device app</span></span>
<span data-ttu-id="f12fa-160">Ta sekcja zawiera instrukcje dotyczące tworzenia aplikacji konsolowej środowiska Node.js, która symuluje urządzenie wysyłające komunikaty z urządzenia do chmury do centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="f12fa-160">In this section, you create a Node.js console app that simulates a device that sends device-to-cloud messages to an IoT hub.</span></span>

1. <span data-ttu-id="f12fa-161">Utwórz pusty folder o nazwie **simulateddevice**.</span><span class="sxs-lookup"><span data-stu-id="f12fa-161">Create an empty folder called **simulateddevice**.</span></span> <span data-ttu-id="f12fa-162">W folderze **simulateddevice** utwórz plik package.json przy użyciu następującego polecenia z poziomu wiersza polecenia.</span><span class="sxs-lookup"><span data-stu-id="f12fa-162">In the **simulateddevice** folder, create a package.json file using the following command at your command prompt.</span></span> <span data-ttu-id="f12fa-163">Zaakceptuj wszystkie ustawienia domyślne:</span><span class="sxs-lookup"><span data-stu-id="f12fa-163">Accept all the defaults:</span></span>
   
    ```
    npm init
    ```
2. <span data-ttu-id="f12fa-164">W wierszu polecenia w folderze **simulateddevice** uruchom następujące polecenie, aby zainstalować pakiet zestawu SDK urządzenia **azure-iot-device** i pakiet **azure-iot-device-mqtt**:</span><span class="sxs-lookup"><span data-stu-id="f12fa-164">At your command prompt in the **simulateddevice** folder, run the following command to install the **azure-iot-device** Device SDK package and **azure-iot-device-mqtt** package:</span></span>
   
    ```
    npm install azure-iot-device azure-iot-device-mqtt --save
    ```
3. <span data-ttu-id="f12fa-165">Za pomocą edytora tekstu utwórz plik **SimulatedDevice.js** w folderze **simulateddevice**.</span><span class="sxs-lookup"><span data-stu-id="f12fa-165">Using a text editor, create a **SimulatedDevice.js** file in the **simulateddevice** folder.</span></span>
4. <span data-ttu-id="f12fa-166">Dodaj następujące instrukcje `require` na początku pliku **SimulatedDevice.js**:</span><span class="sxs-lookup"><span data-stu-id="f12fa-166">Add the following `require` statements at the start of the **SimulatedDevice.js** file:</span></span>
   
    ```
    'use strict';
   
    var clientFromConnectionString = require('azure-iot-device-mqtt').clientFromConnectionString;
    var Message = require('azure-iot-device').Message;
    ```
5. <span data-ttu-id="f12fa-167">Dodaj zmienną **connectionString** i użyj jej do utworzenia wystąpienia **Client**.</span><span class="sxs-lookup"><span data-stu-id="f12fa-167">Add a **connectionString** variable and use it to create a **Client** instance.</span></span> <span data-ttu-id="f12fa-168">Zastąp **{youriothostname}** nazwą centrum IoT utworzonego w sekcji *Tworzenie centrum IoT*.</span><span class="sxs-lookup"><span data-stu-id="f12fa-168">Replace **{youriothostname}** with the name of the IoT hub you created the *Create an IoT Hub* section.</span></span> <span data-ttu-id="f12fa-169">Zastąp **{yourdevicekey}** wartością klucza urządzenia wygenerowanego w sekcji *Tworzenie tożsamości urządzenia*:</span><span class="sxs-lookup"><span data-stu-id="f12fa-169">Replace **{yourdevicekey}** with the device key value you generated in the *Create a device identity* section:</span></span>
   
    ```
    var connectionString = 'HostName={youriothostname};DeviceId=myFirstNodeDevice;SharedAccessKey={yourdevicekey}';
   
    var client = clientFromConnectionString(connectionString);
    ```
6. <span data-ttu-id="f12fa-170">Dodaj następującą funkcję, aby wyświetlić dane wyjściowe z aplikacji:</span><span class="sxs-lookup"><span data-stu-id="f12fa-170">Add the following function to display output from the application:</span></span>
   
    ```
    function printResultFor(op) {
      return function printResult(err, res) {
        if (err) console.log(op + ' error: ' + err.toString());
        if (res) console.log(op + ' status: ' + res.constructor.name);
      };
    }
    ```
7. <span data-ttu-id="f12fa-171">Utwórz wywołanie zwrotne i użyj funkcji **setInterval**, aby co sekundę wysyłać komunikat do centrum IoT Hub:</span><span class="sxs-lookup"><span data-stu-id="f12fa-171">Create a callback and use the **setInterval** function to send a message to your IoT hub every second:</span></span>
   
    ```
    var connectCallback = function (err) {
      if (err) {
        console.log('Could not connect: ' + err);
      } else {
        console.log('Client connected');
   
        // Create a message and send it to the IoT Hub every second
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
8. <span data-ttu-id="f12fa-172">Otwórz połączenie z centrum IoT i rozpocznij wysyłanie komunikatów:</span><span class="sxs-lookup"><span data-stu-id="f12fa-172">Open the connection to your IoT Hub and start sending messages:</span></span>
   
    ```
    client.open(connectCallback);
    ```
9. <span data-ttu-id="f12fa-173">Zapisz i zamknij plik **SimulatedDevice.js**.</span><span class="sxs-lookup"><span data-stu-id="f12fa-173">Save and close the **SimulatedDevice.js** file.</span></span>

> [!NOTE]
> <span data-ttu-id="f12fa-174">Dla uproszczenia ten samouczek nie zawiera opisu wdrożenia żadnych zasad ponawiania.</span><span class="sxs-lookup"><span data-stu-id="f12fa-174">To keep things simple, this tutorial does not implement any retry policy.</span></span> <span data-ttu-id="f12fa-175">W kodzie produkcyjnym należy wdrożyć zasady ponawiania (np. wycofywanie wykładnicze) zgodnie z sugestią w artykule z witryny MSDN [Transient Fault Handling][lnk-transient-faults] (Obsługa przejściowych błędów).</span><span class="sxs-lookup"><span data-stu-id="f12fa-175">In production code, you should implement retry policies (such as an exponential backoff), as suggested in the MSDN article [Transient Fault Handling][lnk-transient-faults].</span></span>
> 
> 

## <a name="run-the-apps"></a><span data-ttu-id="f12fa-176">Uruchamianie aplikacji</span><span class="sxs-lookup"><span data-stu-id="f12fa-176">Run the apps</span></span>
<span data-ttu-id="f12fa-177">Teraz można przystąpić do uruchomienia aplikacji.</span><span class="sxs-lookup"><span data-stu-id="f12fa-177">You are now ready to run the apps.</span></span>

1. <span data-ttu-id="f12fa-178">Z poziomu wiersza polecenia w folderze **readdevicetocloudmessages** uruchom następujące polecenie, aby rozpocząć monitorowanie centrum IoT:</span><span class="sxs-lookup"><span data-stu-id="f12fa-178">At a command prompt in the **readdevicetocloudmessages** folder, run the following command to begin monitoring your IoT hub:</span></span>
   
    ```
    node ReadDeviceToCloudMessages.js 
    ```
   
    ![Aplikacja usługi IoT Hub dla środowiska Node.js do monitorowania komunikatów wysyłanych z urządzenia do chmury][7]
2. <span data-ttu-id="f12fa-180">Z poziomu wiersza polecenia w folderze **simulateddevice** uruchom następujące polecenie, aby rozpocząć wysyłanie danych telemetrycznych do centrum IoT:</span><span class="sxs-lookup"><span data-stu-id="f12fa-180">At a command prompt in the **simulateddevice** folder, run the following command to begin sending telemetry data to your IoT hub:</span></span>
   
    ```
    node SimulatedDevice.js
    ```
   
    ![Aplikacja urządzenia usługi IoT Hub dla środowiska Node.js do monitorowania komunikatów wysyłanych z urządzenia do chmury][8]
3. <span data-ttu-id="f12fa-182">Na kafelku **Użycie** w [witrynie Azure Portal][lnk-portal] wyświetlana jest liczba komunikatów wysłanych do centrum IoT:</span><span class="sxs-lookup"><span data-stu-id="f12fa-182">The **Usage** tile in the [Azure portal][lnk-portal] shows the number of messages sent to the IoT hub:</span></span>
   
    ![Kafelek Użycie witryny Azure Portal przedstawiający liczbę komunikatów wysłanych do usługi IoT Hub][43]

## <a name="next-steps"></a><span data-ttu-id="f12fa-184">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="f12fa-184">Next steps</span></span>
<span data-ttu-id="f12fa-185">W tym samouczku opisano konfigurowanie nowego centrum IoT Hub w witrynie Azure Portal, a następnie tworzenie tożsamości urządzenia w rejestrze tożsamości centrum.</span><span class="sxs-lookup"><span data-stu-id="f12fa-185">In this tutorial, you configured a new IoT hub in the Azure portal, and then created a device identity in the IoT hub's identity registry.</span></span> <span data-ttu-id="f12fa-186">Tożsamość urządzenia została użyta, aby włączyć w aplikacji symulowanego urządzenia funkcję wysyłania komunikatów z urządzenia do chmury do centrum IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="f12fa-186">You used this device identity to enable the simulated device app to send device-to-cloud messages to the IoT hub.</span></span> <span data-ttu-id="f12fa-187">Utworzono również aplikację, która wyświetla komunikaty odbierane przez centrum IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="f12fa-187">You also created an app that displays the messages received by the IoT hub.</span></span> 

<span data-ttu-id="f12fa-188">Aby kontynuować wprowadzenie do usługi IoT Hub i zapoznać się z innymi scenariuszami IoT, zobacz:</span><span class="sxs-lookup"><span data-stu-id="f12fa-188">To continue getting started with IoT Hub and to explore other IoT scenarios, see:</span></span>

* <span data-ttu-id="f12fa-189">[Łączenie urządzenia][lnk-connect-device]</span><span class="sxs-lookup"><span data-stu-id="f12fa-189">[Connecting your device][lnk-connect-device]</span></span>
* <span data-ttu-id="f12fa-190">[Wprowadzenie do zarządzania urządzeniami][lnk-device-management]</span><span class="sxs-lookup"><span data-stu-id="f12fa-190">[Getting started with device management][lnk-device-management]</span></span>
* <span data-ttu-id="f12fa-191">[Getting started with Azure IoT Edge][lnk-iot-edge] (Rozpoczynanie pracy z usługą Azure IoT Edge)</span><span class="sxs-lookup"><span data-stu-id="f12fa-191">[Getting started with Azure IoT Edge][lnk-iot-edge]</span></span>

<span data-ttu-id="f12fa-192">Aby dowiedzieć się, jak rozszerzyć rozwiązanie IoT i przetwarzać komunikaty z urządzenia do chmury na dużą skalę, zobacz samouczek [Przetwarzanie komunikatów przesyłanych z urządzeń do chmury][lnk-process-d2c-tutorial].</span><span class="sxs-lookup"><span data-stu-id="f12fa-192">To learn how to extend your IoT solution and process device-to-cloud messages at scale, see the [Process device-to-cloud messages][lnk-process-d2c-tutorial] tutorial.</span></span>
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
