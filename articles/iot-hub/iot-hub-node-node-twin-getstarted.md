---
title: "aaaGet wprowadzenie twins urządzenia Azure IoT Hub (węzeł) | Dokumentacja firmy Microsoft"
description: "Jak tooadd twins urządzenia Azure IoT Hub toouse tagów, a następnie użyj zapytania Centrum IoT. Możesz użyć hello Azure IoT SDK dla środowiska Node.js tooimplement hello symulowane urządzenie aplikacji i aplikacji usługi, który dodaje znaczniki hello i uruchamia hello zapytania Centrum IoT."
services: iot-hub
documentationcenter: node
author: fsautomata
manager: timlt
editor: 
ms.assetid: 314c88e4-cce1-441c-b75a-d2e08e39ae7d
ms.service: iot-hub
ms.devlang: node
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/25/2017
ms.author: elioda
ms.openlocfilehash: d60b8c3de85e9285e496b86e27d4ee31a0554a1e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-device-twins-node"></a><span data-ttu-id="f31d6-104">Rozpoczynanie pracy z urządzenia twins (węzeł)</span><span class="sxs-lookup"><span data-stu-id="f31d6-104">Get started with device twins (Node)</span></span>
[!INCLUDE [iot-hub-selector-twin-get-started](../../includes/iot-hub-selector-twin-get-started.md)]

<span data-ttu-id="f31d6-105">Na końcu hello tego samouczka masz dwie aplikacje konsoli Node.js:</span><span class="sxs-lookup"><span data-stu-id="f31d6-105">At hello end of this tutorial, you will have two Node.js console apps:</span></span>

* <span data-ttu-id="f31d6-106">**AddTagsAndQuery.js**, aplikacji zaplecza Node.js, która dodaje znaczniki i zapytanie twins urządzenia.</span><span class="sxs-lookup"><span data-stu-id="f31d6-106">**AddTagsAndQuery.js**, a Node.js back-end app, which adds tags and queries device twins.</span></span>
* <span data-ttu-id="f31d6-107">**TwinSimulatedDevice.js**, aplikacji Node.js, która symuluje urządzenie łączące Centrum IoT tooyour o tożsamości urządzenia hello utworzony wcześniej, a następnie raportuje stanu łączności.</span><span class="sxs-lookup"><span data-stu-id="f31d6-107">**TwinSimulatedDevice.js**, a Node.js app which simulates a device that connects tooyour IoT hub with hello device identity created earlier, and reports its connectivity condition.</span></span>

> [!NOTE]
> <span data-ttu-id="f31d6-108">Artykuł Hello [Azure IoT SDK] [ lnk-hub-sdks] informacje na temat hello Azure IoT SDK służy toobuild zarówno urządzenia, jak i zaplecza aplikacji.</span><span class="sxs-lookup"><span data-stu-id="f31d6-108">hello article [Azure IoT SDKs][lnk-hub-sdks] provides information about hello Azure IoT SDKs that you can use toobuild both device and back-end apps.</span></span>
> 
> 

<span data-ttu-id="f31d6-109">toocomplete tego samouczka należy hello poniżej:</span><span class="sxs-lookup"><span data-stu-id="f31d6-109">toocomplete this tutorial you need hello following:</span></span>

* <span data-ttu-id="f31d6-110">Środowisko Node.js w wersji 0.10.x lub nowszej.</span><span class="sxs-lookup"><span data-stu-id="f31d6-110">Node.js version 0.10.x or later.</span></span>
* <span data-ttu-id="f31d6-111">Aktywne konto platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="f31d6-111">An active Azure account.</span></span> <span data-ttu-id="f31d6-112">(Jeśli go nie masz, możesz utworzyć [bezpłatne konto próbne][lnk-free-trial] w zaledwie kilka minut).</span><span class="sxs-lookup"><span data-stu-id="f31d6-112">(If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.)</span></span>

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity](../../includes/iot-hub-get-started-create-device-identity.md)]

## <a name="create-hello-service-app"></a><span data-ttu-id="f31d6-113">Tworzenie aplikacji usługi hello</span><span class="sxs-lookup"><span data-stu-id="f31d6-113">Create hello service app</span></span>
<span data-ttu-id="f31d6-114">W tej sekcji zostanie utworzona aplikacja konsoli Node.js dodające skojarzone z lokalizacji metadanych toohello urządzenia dwie **myDeviceId**.</span><span class="sxs-lookup"><span data-stu-id="f31d6-114">In this section, you create a Node.js console app that adds location metadata toohello device twin associated with **myDeviceId**.</span></span> <span data-ttu-id="f31d6-115">Następnie zapytania twins urządzenia hello przechowywane w Centrum IoT hello Wybieranie hello urządzeń znajdujących się w hello nam, a następnie hello te, które są raportowania komórkowej połączenia.</span><span class="sxs-lookup"><span data-stu-id="f31d6-115">It then queries hello device twins stored in hello IoT hub selecting hello devices located in hello US, and then hello ones that are reporting a cellular connection.</span></span>

1. <span data-ttu-id="f31d6-116">Utwórz nowy, pusty folder o nazwie **addtagsandqueryapp**.</span><span class="sxs-lookup"><span data-stu-id="f31d6-116">Create a new empty folder called **addtagsandqueryapp**.</span></span> <span data-ttu-id="f31d6-117">W hello **addtagsandqueryapp** folderu, Utwórz nowy plik package.json przy użyciu hello następujące polecenie z wiersza polecenia.</span><span class="sxs-lookup"><span data-stu-id="f31d6-117">In hello **addtagsandqueryapp** folder, create a new package.json file using hello following command at your command prompt.</span></span> <span data-ttu-id="f31d6-118">Zaakceptuj wszystkie domyślne hello:</span><span class="sxs-lookup"><span data-stu-id="f31d6-118">Accept all hello defaults:</span></span>
   
    ```
    npm init
    ```
2. <span data-ttu-id="f31d6-119">Z wiersza polecenia w hello **addtagsandqueryapp** folderu, uruchom następujące polecenie tooinstall hello hello **Centrum iothub azure** pakietu:</span><span class="sxs-lookup"><span data-stu-id="f31d6-119">At your command prompt in hello **addtagsandqueryapp** folder, run hello following command tooinstall hello **azure-iothub** package:</span></span>
   
    ```
    npm install azure-iothub --save
    ```
3. <span data-ttu-id="f31d6-120">Za pomocą edytora tekstu, Utwórz nową **AddTagsAndQuery.js** pliku w hello **addtagsandqueryapp** folderu.</span><span class="sxs-lookup"><span data-stu-id="f31d6-120">Using a text editor, create a new **AddTagsAndQuery.js** file in hello **addtagsandqueryapp** folder.</span></span>
4. <span data-ttu-id="f31d6-121">Dodaj hello następującego kodu toohello **AddTagsAndQuery.js** plików i Zastąp hello **{parametry połączenia Centrum iot}** symbol zastępczy hello Centrum IoT parametry połączenia skopiowane podczas tworzenia Centrum:</span><span class="sxs-lookup"><span data-stu-id="f31d6-121">Add hello following code toohello **AddTagsAndQuery.js** file, and substitute hello **{iot hub connection string}** placeholder with hello IoT Hub connection string you copied when you created your hub:</span></span>
   
        'use strict';
        var iothub = require('azure-iothub');
        var connectionString = '{iot hub connection string}';
        var registry = iothub.Registry.fromConnectionString(connectionString);
   
        registry.getTwin('myDeviceId', function(err, twin){
            if (err) {
                console.error(err.constructor.name + ': ' + err.message);
            } else {
                var patch = {
                    tags: {
                        location: {
                            region: 'US',
                            plant: 'Redmond43'
                      }
                    }
                };
   
                twin.update(patch, function(err) {
                  if (err) {
                    console.error('Could not update twin: ' + err.constructor.name + ': ' + err.message);
                  } else {
                    console.log(twin.deviceId + ' twin updated successfully');
                    queryTwins();
                  }
                });
            }
        });
   
    <span data-ttu-id="f31d6-122">Witaj **rejestru** obiekt udostępnia wszystkie hello metody wymagane toointeract z twins urządzenia z usługi hello.</span><span class="sxs-lookup"><span data-stu-id="f31d6-122">hello **Registry** object exposes all hello methods required toointeract with device twins from hello service.</span></span> <span data-ttu-id="f31d6-123">Poprzedni kod Hello najpierw inicjuje hello **rejestru** obiektu, a następnie pobiera Witaj dwie urządzenia dla **myDeviceId**i na koniec aktualizuje jego tagi hello potrzeby informacji o lokalizacji.</span><span class="sxs-lookup"><span data-stu-id="f31d6-123">hello previous code first initializes hello **Registry** object, then retrieves hello device twin for **myDeviceId**, and finally updates its tags with hello desired location information.</span></span>
   
    <span data-ttu-id="f31d6-124">Po hello aktualizowanie hello znaczniki hello wywołania **queryTwins** funkcji.</span><span class="sxs-lookup"><span data-stu-id="f31d6-124">After hello updating hello tags it calls hello **queryTwins** function.</span></span>
5. <span data-ttu-id="f31d6-125">Dodaj następujące kod na końcu hello hello **AddTagsAndQuery.js** tooimplement hello **queryTwins** funkcji:</span><span class="sxs-lookup"><span data-stu-id="f31d6-125">Add hello following code at hello end of  **AddTagsAndQuery.js** tooimplement hello **queryTwins** function:</span></span>
   
        var queryTwins = function() {
            var query = registry.createQuery("SELECT * FROM devices WHERE tags.location.plant = 'Redmond43'", 100);
            query.nextAsTwin(function(err, results) {
                if (err) {
                    console.error('Failed toofetch hello results: ' + err.message);
                } else {
                    console.log("Devices in Redmond43: " + results.map(function(twin) {return twin.deviceId}).join(','));
                }
            });
   
            query = registry.createQuery("SELECT * FROM devices WHERE tags.location.plant = 'Redmond43' AND properties.reported.connectivity.type = 'cellular'", 100);
            query.nextAsTwin(function(err, results) {
                if (err) {
                    console.error('Failed toofetch hello results: ' + err.message);
                } else {
                    console.log("Devices in Redmond43 using cellular network: " + results.map(function(twin) {return twin.deviceId}).join(','));
                }
            });
        };
   
    <span data-ttu-id="f31d6-126">Poprzedni kod Hello wykonuje dwa zapytania: hello najpierw wybiera tylko twins urządzenia hello urządzeń znajdujących się w hello **Redmond43** roślin i hello drugi refines hello zapytania tooselect tylko hello urządzeń podłączonych do sieci komórkowej.</span><span class="sxs-lookup"><span data-stu-id="f31d6-126">hello previous code executes two queries: hello first selects only hello device twins of devices located in hello **Redmond43** plant, and hello second refines hello query tooselect only hello devices that are also connected through cellular network.</span></span>
   
    <span data-ttu-id="f31d6-127">Należy pamiętać, że poprzedni kod hello, podczas tworzenia hello **zapytania** obiektów, określa maksymalną liczbę zwracanych dokumentów.</span><span class="sxs-lookup"><span data-stu-id="f31d6-127">Note that hello previous code, when it creates hello **query** object, specifies a maximum number of returned documents.</span></span> <span data-ttu-id="f31d6-128">Hello **zapytania** zawiera obiekt **hasMoreResults** właściwości typu boolean służy tooinvoke hello **nextAsTwin** metody wielokrotnie tooretrieve wszystkie wyniki.</span><span class="sxs-lookup"><span data-stu-id="f31d6-128">hello **query** object contains a **hasMoreResults** boolean property that you can use tooinvoke hello **nextAsTwin** methods multiple times tooretrieve all results.</span></span> <span data-ttu-id="f31d6-129">Wywołana metoda **dalej** jest dostępna dla wyników, które nie są urządzenia, na przykład twins wyniki zapytań agregacji.</span><span class="sxs-lookup"><span data-stu-id="f31d6-129">A method called **next** is available for results that are not device twins for example, results of aggregation queries.</span></span>
6. <span data-ttu-id="f31d6-130">Uruchamianie aplikacji hello:</span><span class="sxs-lookup"><span data-stu-id="f31d6-130">Run hello application with:</span></span>
   
        node AddTagsAndQuery.js
   
    <span data-ttu-id="f31d6-131">Powinny pojawić się jedno urządzenie w wynikach hello hello zadać zapytania dla wszystkich urządzeń znajdujących się w **Redmond43** i Brak dla zapytania hello, która ogranicza hello powoduje toodevices używanego przez sieć komórkową.</span><span class="sxs-lookup"><span data-stu-id="f31d6-131">You should see one device in hello results for hello query asking for all devices located in **Redmond43** and none for hello query that restricts hello results toodevices that use a cellular network.</span></span>
   
    ![][1]

<span data-ttu-id="f31d6-132">W następnej sekcji hello tworzenia aplikacji urządzenia, która raportuje informacje o łączności hello i zmiany hello wynik kwerendy hello w poprzedniej sekcji hello.</span><span class="sxs-lookup"><span data-stu-id="f31d6-132">In hello next section you create a device app that reports hello connectivity information and changes hello result of hello query in hello previous section.</span></span>

## <a name="create-hello-device-app"></a><span data-ttu-id="f31d6-133">Tworzenie hello urządzenia aplikacji</span><span class="sxs-lookup"><span data-stu-id="f31d6-133">Create hello device app</span></span>
<span data-ttu-id="f31d6-134">W tej sekcji zostanie utworzona aplikacja konsoli Node.js łączącego koncentratora tooyour **myDeviceId**, a następnie aktualizacje jego dwie urządzenia użytkownika zgłosiła właściwości toocontain hello informacje, że jest połączony za pomocą sieci komórkowej.</span><span class="sxs-lookup"><span data-stu-id="f31d6-134">In this section, you create a Node.js console app that connects tooyour hub as **myDeviceId**, and then updates its device twin's reported properties toocontain hello information that it is connected using a cellular network.</span></span>

> [!NOTE]
> <span data-ttu-id="f31d6-135">W tej chwili twins urządzenia są dostępne tylko z urządzeń łączących tooIoT Centrum przy użyciu protokołu MQTT hello.</span><span class="sxs-lookup"><span data-stu-id="f31d6-135">At this time, device twins are accessible only from devices that connect tooIoT Hub using hello MQTT protocol.</span></span> <span data-ttu-id="f31d6-136">Zobacz toohello [Obsługa MQTT] [ lnk-devguide-mqtt] artykuł, aby uzyskać instrukcje dotyczące tooconvert istniejących urządzeń aplikacji toouse MQTT.</span><span class="sxs-lookup"><span data-stu-id="f31d6-136">Please refer toohello [MQTT support][lnk-devguide-mqtt] article for instructions on how tooconvert existing device app toouse MQTT.</span></span>
> 
> 

1. <span data-ttu-id="f31d6-137">Utwórz nowy, pusty folder o nazwie **reportconnectivity**.</span><span class="sxs-lookup"><span data-stu-id="f31d6-137">Create a new empty folder called **reportconnectivity**.</span></span> <span data-ttu-id="f31d6-138">W hello **reportconnectivity** folderu, Utwórz nowy plik package.json przy użyciu hello następujące polecenie z wiersza polecenia.</span><span class="sxs-lookup"><span data-stu-id="f31d6-138">In hello **reportconnectivity** folder, create a new package.json file using hello following command at your command prompt.</span></span> <span data-ttu-id="f31d6-139">Zaakceptuj wszystkie domyślne hello:</span><span class="sxs-lookup"><span data-stu-id="f31d6-139">Accept all hello defaults:</span></span>
   
    ```
    npm init
    ```
2. <span data-ttu-id="f31d6-140">Z wiersza polecenia w hello **reportconnectivity** folderu, uruchom następujące polecenie tooinstall hello hello **azure iot urządzenia**, i **azure-iot urządzenie mqtt** pakietu :</span><span class="sxs-lookup"><span data-stu-id="f31d6-140">At your command prompt in hello **reportconnectivity** folder, run hello following command tooinstall hello **azure-iot-device**, and **azure-iot-device-mqtt** package:</span></span>
   
    ```
    npm install azure-iot-device azure-iot-device-mqtt --save
    ```
3. <span data-ttu-id="f31d6-141">Za pomocą edytora tekstu, Utwórz nową **ReportConnectivity.js** pliku w hello **reportconnectivity** folderu.</span><span class="sxs-lookup"><span data-stu-id="f31d6-141">Using a text editor, create a new **ReportConnectivity.js** file in hello **reportconnectivity** folder.</span></span>
4. <span data-ttu-id="f31d6-142">Dodaj hello następującego kodu toohello **ReportConnectivity.js** plików i Zastąp hello **{ciąg połączenia urządzenia}** symbol zastępczy parametrów połączenia urządzenia hello skopiowane podczas tworzenia hello **myDeviceId** tożsamości urządzenia:</span><span class="sxs-lookup"><span data-stu-id="f31d6-142">Add hello following code toohello **ReportConnectivity.js** file, and substitute hello **{device connection string}** placeholder with hello device connection string you copied when you created hello **myDeviceId** device identity:</span></span>
   
        'use strict';
        var Client = require('azure-iot-device').Client;
        var Protocol = require('azure-iot-device-mqtt').Mqtt;
   
        var connectionString = '{device connection string}';
        var client = Client.fromConnectionString(connectionString, Protocol);
   
        client.open(function(err) {
        if (err) {
            console.error('could not open IotHub client');
        }  else {
            console.log('client opened');
   
            client.getTwin(function(err, twin) {
            if (err) {
                console.error('could not get twin');
            } else {
                var patch = {
                    connectivity: {
                        type: 'cellular'
                    }
                };
   
                twin.properties.reported.update(patch, function(err) {
                    if (err) {
                        console.error('could not update twin');
                    } else {
                        console.log('twin state reported');
                        process.exit();
                    }
                });
            }
            });
        }
        });
   
    <span data-ttu-id="f31d6-143">Witaj **klienta** obiekt udostępnia wszystkie metody hello wymagają toointeract z twins urządzenia z hello urządzenia.</span><span class="sxs-lookup"><span data-stu-id="f31d6-143">hello **Client** object exposes all hello methods you require toointeract with device twins from hello device.</span></span> <span data-ttu-id="f31d6-144">Witaj poprzedni kod po jego inicjuje hello **klienta** obiektu, pobiera Witaj dwie urządzenia dla **myDeviceId** i aktualizuje informacje o łączności hello jego właściwość zgłoszony.</span><span class="sxs-lookup"><span data-stu-id="f31d6-144">hello previous code, after it initializes hello **Client** object, retrieves hello device twin for **myDeviceId** and updates its reported property with hello connectivity information.</span></span>
5. <span data-ttu-id="f31d6-145">Uruchamianie hello urządzenia aplikacji</span><span class="sxs-lookup"><span data-stu-id="f31d6-145">Run hello device app</span></span>
   
        node ReportConnectivity.js
   
    <span data-ttu-id="f31d6-146">Powinna zostać wyświetlona wiadomość hello `twin state reported`.</span><span class="sxs-lookup"><span data-stu-id="f31d6-146">You should see hello message `twin state reported`.</span></span>
6. <span data-ttu-id="f31d6-147">Teraz, gdy hello Urządzenie zgłosiło jego informacje dotyczące łączności, powinna pojawić się w obu zapytania.</span><span class="sxs-lookup"><span data-stu-id="f31d6-147">Now that hello device reported its connectivity information, it should appear in both queries.</span></span> <span data-ttu-id="f31d6-148">Przejdź wstecz w hello **addtagsandqueryapp** hello folderu i uruchom ponownie zapytanie:</span><span class="sxs-lookup"><span data-stu-id="f31d6-148">Go back in hello **addtagsandqueryapp** folder and run hello queries again:</span></span>
   
        node AddTagsAndQuery.js
   
    <span data-ttu-id="f31d6-149">Teraz **myDeviceId** powinny być wyświetlane w obu wyników zapytania.</span><span class="sxs-lookup"><span data-stu-id="f31d6-149">This time **myDeviceId** should appear in both query results.</span></span>
   
    ![][3]

## <a name="next-steps"></a><span data-ttu-id="f31d6-150">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="f31d6-150">Next steps</span></span>
<span data-ttu-id="f31d6-151">W tym samouczku został skonfigurowany nowego centrum IoT w portalu Azure hello i w rejestrze tożsamości Centrum IoT hello zostanie utworzona tożsamość urządzenia.</span><span class="sxs-lookup"><span data-stu-id="f31d6-151">In this tutorial, you configured a new IoT hub in hello Azure portal, and then created a device identity in hello IoT hub's identity registry.</span></span> <span data-ttu-id="f31d6-152">Dodaje metadane urządzenia jako tagi z aplikacji zaplecza i zapisane symulowane urządzenie tooreport urządzenia łączności informacji o aplikacji w Witaj dwie urządzenia.</span><span class="sxs-lookup"><span data-stu-id="f31d6-152">You added device metadata as tags from a back-end app, and wrote a simulated device app tooreport device connectivity information in hello device twin.</span></span> <span data-ttu-id="f31d6-153">Przedstawiono również sposób tooquery te informacje przy użyciu języka kwerend hello Centrum IoT przypominającego SQL.</span><span class="sxs-lookup"><span data-stu-id="f31d6-153">You also learned how tooquery this information using hello SQL-like IoT Hub query language.</span></span>

<span data-ttu-id="f31d6-154">Hello Użyj następujących zasobów toolearn jak do:</span><span class="sxs-lookup"><span data-stu-id="f31d6-154">Use hello following resources toolearn how to:</span></span>

* <span data-ttu-id="f31d6-155">wysłać dane telemetryczne z urządzenia z hello [Rozpoczynanie pracy z Centrum IoT] [ lnk-iothub-getstarted] samouczka</span><span class="sxs-lookup"><span data-stu-id="f31d6-155">send telemetry from devices with hello [Get started with IoT Hub][lnk-iothub-getstarted] tutorial,</span></span>
* <span data-ttu-id="f31d6-156">Konfigurowanie urządzeń przy użyciu właściwości żądaną dwie urządzenia z hello [Użyj potrzeby urządzeń tooconfigure właściwości] [ lnk-twin-how-to-configure] samouczka</span><span class="sxs-lookup"><span data-stu-id="f31d6-156">configure devices using device twin's desired properties with hello [Use desired properties tooconfigure devices][lnk-twin-how-to-configure] tutorial,</span></span>
* <span data-ttu-id="f31d6-157">sterować urządzenia interakcyjne (takich jak włączanie wentylator z aplikacji kontrolowane przez użytkownika), za pomocą hello [metody bezpośredniego] [ lnk-methods-tutorial] samouczka.</span><span class="sxs-lookup"><span data-stu-id="f31d6-157">control devices interactively (such as turning on a fan from a user-controlled app), with hello [Use direct methods][lnk-methods-tutorial] tutorial.</span></span>

<!-- images -->
[1]: media/iot-hub-node-node-twin-getstarted/service1.png
[3]: media/iot-hub-node-node-twin-getstarted/service2.png

<!-- links -->
[lnk-hub-sdks]: iot-hub-devguide-sdks.md
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/

[lnk-d2c]: iot-hub-devguide-messaging.md#device-to-cloud-messages
[lnk-methods]: iot-hub-devguide-direct-methods.md
[lnk-twins]: iot-hub-devguide-device-twins.md
[lnk-query]: iot-hub-devguide-query-language.md
[lnk-identity]: iot-hub-devguide-identity-registry.md

[lnk-iothub-getstarted]: iot-hub-node-node-getstarted.md
[lnk-device-management]: iot-hub-node-node-device-management-get-started.md
[lnk-iot-edge]: iot-hub-linux-iot-edge-get-started.md
[lnk-connect-device]: https://azure.microsoft.com/develop/iot/

[lnk-twin-how-to-configure]: iot-hub-node-node-twin-how-to-configure.md
[lnk-dev-setup]: https://github.com/Azure/azure-iot-sdk-node/tree/master/doc/node-devbox-setup.md

[lnk-methods-tutorial]: iot-hub-node-node-direct-methods.md
[lnk-devguide-mqtt]: iot-hub-mqtt-support.md
