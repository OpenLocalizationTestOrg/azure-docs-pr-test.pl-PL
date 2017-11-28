---
title: monitorowanie operacji centrum IoT aaaAzure | Dokumentacja firmy Microsoft
description: "Sposób działania Centrum IoT Azure toouse monitorowania toomonitor hello stanu operacji w Centrum IoT w czasie rzeczywistym."
services: iot-hub
documentationcenter: 
author: nberdy
manager: timlt
editor: 
ms.assetid: a299f3a5-b14d-4586-9c3b-44aea14ed013
ms.service: iot-hub
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/25/2017
ms.author: nberdy
ms.openlocfilehash: a0b233ef2d9bd0827e19fa30fdbdd49b2b61b813
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="iot-hub-operations-monitoring"></a><span data-ttu-id="1be73-103">Monitorowanie operacji centrum IoT</span><span class="sxs-lookup"><span data-stu-id="1be73-103">IoT Hub operations monitoring</span></span>

<span data-ttu-id="1be73-104">Monitorowanie operacji centrum IoT umożliwia toomonitor hello stanu operacji w Centrum IoT w czasie rzeczywistym.</span><span class="sxs-lookup"><span data-stu-id="1be73-104">IoT Hub operations monitoring enables you toomonitor hello status of operations on your IoT hub in real time.</span></span> <span data-ttu-id="1be73-105">Centrum IoT śledzi zdarzenia przez różne kategorie działań.</span><span class="sxs-lookup"><span data-stu-id="1be73-105">IoT Hub tracks events across several categories of operations.</span></span> <span data-ttu-id="1be73-106">Można włączyć do wysyłania zdarzeń z jednego lub więcej kategorii tooan punktu końcowego Centrum IoT do przetwarzania.</span><span class="sxs-lookup"><span data-stu-id="1be73-106">You can opt into sending events from one or more categories tooan endpoint of your IoT hub for processing.</span></span> <span data-ttu-id="1be73-107">Możesz monitorować dane hello błędów lub konfigurowanie bardziej złożonych przetwarzania na podstawie wzorców danych.</span><span class="sxs-lookup"><span data-stu-id="1be73-107">You can monitor hello data for errors or set up more complex processing based on data patterns.</span></span>

<span data-ttu-id="1be73-108">Centrum IoT monitoruje sześć kategorii zdarzeń:</span><span class="sxs-lookup"><span data-stu-id="1be73-108">IoT Hub monitors six categories of events:</span></span>

* <span data-ttu-id="1be73-109">Operacje tożsamości urządzenia</span><span class="sxs-lookup"><span data-stu-id="1be73-109">Device identity operations</span></span>
* <span data-ttu-id="1be73-110">Telemetrii urządzenia</span><span class="sxs-lookup"><span data-stu-id="1be73-110">Device telemetry</span></span>
* <span data-ttu-id="1be73-111">Komunikaty chmury do urządzenia</span><span class="sxs-lookup"><span data-stu-id="1be73-111">Cloud-to-device messages</span></span>
* <span data-ttu-id="1be73-112">Połączenia</span><span class="sxs-lookup"><span data-stu-id="1be73-112">Connections</span></span>
* <span data-ttu-id="1be73-113">Przekazywania plików</span><span class="sxs-lookup"><span data-stu-id="1be73-113">File uploads</span></span>
* <span data-ttu-id="1be73-114">Rozsyłanie wiadomości</span><span class="sxs-lookup"><span data-stu-id="1be73-114">Message routing</span></span>

## <a name="how-tooenable-operations-monitoring"></a><span data-ttu-id="1be73-115">Jak operacje tooenable monitorowania</span><span class="sxs-lookup"><span data-stu-id="1be73-115">How tooenable operations monitoring</span></span>

1. <span data-ttu-id="1be73-116">Tworzenie Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="1be73-116">Create an IoT hub.</span></span> <span data-ttu-id="1be73-117">Instrukcje można znaleźć na temat toocreate Centrum IoT w hello [wprowadzenie] [ lnk-get-started] przewodnik.</span><span class="sxs-lookup"><span data-stu-id="1be73-117">You can find instructions on how toocreate an IoT hub in hello [Get Started][lnk-get-started] guide.</span></span>

1. <span data-ttu-id="1be73-118">Otwiera blok hello Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="1be73-118">Open hello blade of your IoT hub.</span></span> <span data-ttu-id="1be73-119">Z tego miejsca, kliknij przycisk **operacje monitorowania**.</span><span class="sxs-lookup"><span data-stu-id="1be73-119">From there, click **Operations monitoring**.</span></span>

    ![Monitorowanie konfiguracji w portalu hello operacje związane z dostępem][1]

1. <span data-ttu-id="1be73-121">Wybierz hello monitorowania kategorii ma toomonitor, a następnie kliknij przycisk **zapisać**.</span><span class="sxs-lookup"><span data-stu-id="1be73-121">Select hello monitoring categories you wish toomonitor, and then click **Save**.</span></span> <span data-ttu-id="1be73-122">Witaj zdarzenia są dostępne do odczytu z punktu końcowego hello zgodnego Centrum zdarzeń na liście **ustawienia monitorowania**.</span><span class="sxs-lookup"><span data-stu-id="1be73-122">hello events are available for reading from hello Event Hub-compatible endpoint listed in **Monitoring settings**.</span></span> <span data-ttu-id="1be73-123">Witaj punktu końcowego Centrum IoT jest nazywany `messages/operationsmonitoringevents`.</span><span class="sxs-lookup"><span data-stu-id="1be73-123">hello IoT Hub endpoint is called `messages/operationsmonitoringevents`.</span></span>

    ![Skonfiguruj operacje monitorowania na Centrum IoT][2]

> [!NOTE]
> <span data-ttu-id="1be73-125">Wybieranie **pełne** monitorowania hello **połączeń** category powoduje, że Centrum IoT toogenerate komunikaty dodatkowych diagnostyczne.</span><span class="sxs-lookup"><span data-stu-id="1be73-125">Selecting **Verbose** monitoring for hello **Connections** category causes IoT Hub toogenerate additional diagnostics messages.</span></span> <span data-ttu-id="1be73-126">Dla wszystkich innych kategoriach hello **pełne** zawiera zmiany ustawień hello ilość informacji Centrum IoT w każdy komunikat o błędzie.</span><span class="sxs-lookup"><span data-stu-id="1be73-126">For all other categories, hello **Verbose** setting changes hello quantity of information IoT Hub includes in each error message.</span></span>

## <a name="event-categories-and-how-toouse-them"></a><span data-ttu-id="1be73-127">Kategorie zdarzeń i w jaki sposób toouse ich</span><span class="sxs-lookup"><span data-stu-id="1be73-127">Event categories and how toouse them</span></span>

<span data-ttu-id="1be73-128">Każdy operacje monitorowania śledzi kategorii ma inny typ interakcji z Centrum IoT i każda kategoria monitorowania schematu definiującego struktury zdarzenia w tej kategorii.</span><span class="sxs-lookup"><span data-stu-id="1be73-128">Each operations monitoring category tracks a different type of interaction with IoT Hub, and each monitoring category has a schema that defines how events in that category are structured.</span></span>

### <a name="device-identity-operations"></a><span data-ttu-id="1be73-129">Operacje tożsamości urządzenia</span><span class="sxs-lookup"><span data-stu-id="1be73-129">Device identity operations</span></span>

<span data-ttu-id="1be73-130">Kategoria operacje tożsamości urządzenia Hello śledzi błędów występujących podczas próby toocreate, zaktualizować lub usunąć wpis w rejestrze tożsamości Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="1be73-130">hello device identity operations category tracks errors that occur when you attempt toocreate, update, or delete an entry in your IoT hub's identity registry.</span></span> <span data-ttu-id="1be73-131">Ta kategoria śledzenia jest przydatne w przypadku inicjowania obsługi scenariuszy.</span><span class="sxs-lookup"><span data-stu-id="1be73-131">Tracking this category is useful for provisioning scenarios.</span></span>

```json
{
    "time": "UTC timestamp",
        "operationName": "create",
        "category": "DeviceIdentityOperations",
        "level": "Error",
        "statusCode": 4XX,
        "statusDescription": "MessageDescription",
        "deviceId": "device-ID",
        "durationMs": 1234,
        "userAgent": "userAgent",
        "sharedAccessPolicy": "accessPolicy"
}
```

### <a name="device-telemetry"></a><span data-ttu-id="1be73-132">Telemetrii urządzenia</span><span class="sxs-lookup"><span data-stu-id="1be73-132">Device telemetry</span></span>

<span data-ttu-id="1be73-133">Kategoria telemetrii urządzenia Hello śledzi błędów, które występują w Centrum IoT hello a są powiązane toohello telemetrii potoku.</span><span class="sxs-lookup"><span data-stu-id="1be73-133">hello device telemetry category tracks errors that occur at hello IoT hub and are related toohello telemetry pipeline.</span></span> <span data-ttu-id="1be73-134">Ta kategoria zawiera błędy występujące podczas wysyłania zdarzenia telemetrii (takie jak dławienie) i odbieranie zdarzeń telemetrii (np. czytnik nieautoryzowanych).</span><span class="sxs-lookup"><span data-stu-id="1be73-134">This category includes errors that occur when sending telemetry events (such as throttling) and receiving telemetry events (such as unauthorized reader).</span></span> <span data-ttu-id="1be73-135">Ta kategoria nie może przechwycić błędów spowodowanych przez kod działający na powitania urządzeniu.</span><span class="sxs-lookup"><span data-stu-id="1be73-135">This category cannot catch errors caused by code running on hello device itself.</span></span>

```json
{
        "messageSizeInBytes": 1234,
        "batching": 0,
        "protocol": "Amqp",
        "authType": "{\"scope\":\"device\",\"type\":\"sas\",\"issuer\":\"iothub\"}",
        "time": "UTC timestamp",
        "operationName": "ingress",
        "category": "DeviceTelemetry",
        "level": "Error",
        "statusCode": 4XX,
        "statusType": 4XX001,
        "statusDescription": "MessageDescription",
        "deviceId": "device-ID",
        "EventProcessedUtcTime": "UTC timestamp",
        "PartitionId": 1,
        "EventEnqueuedUtcTime": "UTC timestamp"
}
```

### <a name="cloud-to-device-commands"></a><span data-ttu-id="1be73-136">Polecenia chmury do urządzenia</span><span class="sxs-lookup"><span data-stu-id="1be73-136">Cloud-to-device commands</span></span>

<span data-ttu-id="1be73-137">Kategoria polecenia chmury do urządzenia Hello śledzi błędów, które występują w Centrum IoT hello a są powiązane toohello komunikatu chmura urządzenie potoku.</span><span class="sxs-lookup"><span data-stu-id="1be73-137">hello cloud-to-device commands category tracks errors that occur at hello IoT hub and are related toohello cloud-to-device message pipeline.</span></span> <span data-ttu-id="1be73-138">Ta kategoria zawiera błędy występujące podczas wysyłania wiadomości chmury do urządzenia (takich jak nieautoryzowanego nadawcę), odbierania wiadomości chmury do urządzenia (takich jak przekroczona liczba dostarczania) i odbieranie komunikatu chmura urządzenie opinii (takie jak opinii wygasł).</span><span class="sxs-lookup"><span data-stu-id="1be73-138">This category includes errors that occur when sending cloud-to-device messages (such as unauthorized sender), receiving cloud-to-device messages (such as delivery count exceeded), and receiving cloud-to-device message feedback (such as feedback expired).</span></span> <span data-ttu-id="1be73-139">Ta kategoria nie przechwytuje błędy z urządzenia, które nieprawidłowo obsługuje komunikatu chmura urządzenie, jeśli został pomyślnie dostarczony wiadomości powitania chmury do urządzenia.</span><span class="sxs-lookup"><span data-stu-id="1be73-139">This category does not catch errors from a device that improperly handles a cloud-to-device message if hello cloud-to-device message was delivered successfully.</span></span>

```json
{
    "messageSizeInBytes": 1234,
    "authType": "{\"scope\":\"hub\",\"type\":\"sas\",\"issuer\":\"iothub\"}",
    "deliveryAcknowledgement": 0,
    "protocol": "Amqp",
    "time": " UTC timestamp",
    "operationName": "ingress",
    "category": "C2DCommands",
    "level": "Error",
    "statusCode": 4XX,
    "statusType": 4XX001,
    "statusDescription": "MessageDescription",
    "deviceId": "device-ID",
    "EventProcessedUtcTime": "UTC timestamp",
    "PartitionId": 1,
    "EventEnqueuedUtcTime": “UTC timestamp"
}
```

### <a name="connections"></a><span data-ttu-id="1be73-140">Połączenia</span><span class="sxs-lookup"><span data-stu-id="1be73-140">Connections</span></span>

<span data-ttu-id="1be73-141">Kategoria połączenia Hello śledzi błędów występujących podczas urządzeń Połącz lub Rozłącz z Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="1be73-141">hello connections category tracks errors that occur when devices connect or disconnect from an IoT hub.</span></span> <span data-ttu-id="1be73-142">Śledzenie tej kategorii jest przydatne do identyfikowania próby nieautoryzowanego połączenia i śledzenia, gdy połączenie zostanie przerwane dla urządzeń w zakresie łączności niska.</span><span class="sxs-lookup"><span data-stu-id="1be73-142">Tracking this category is useful for identifying unauthorized connection attempts and for tracking when a connection is lost for devices in areas of poor connectivity.</span></span>

```json
{
    "durationMs": 1234,
    "authType": "{\"scope\":\"hub\",\"type\":\"sas\",\"issuer\":\"iothub\"}",
    "protocol": "Amqp",
    "time": " UTC timestamp",
    "operationName": "deviceConnect",
    "category": "Connections",
    "level": "Error",
    "statusCode": 4XX,
    "statusType": 4XX001,
    "statusDescription": "MessageDescription",
    "deviceId": "device-ID"
}
```

### <a name="file-uploads"></a><span data-ttu-id="1be73-143">Przekazywania plików</span><span class="sxs-lookup"><span data-stu-id="1be73-143">File uploads</span></span>

<span data-ttu-id="1be73-144">Kategoria przekazywania pliku Hello śledzi błędów, które występują w Centrum IoT hello a są powiązane toofile funkcji przekazywania.</span><span class="sxs-lookup"><span data-stu-id="1be73-144">hello file upload category tracks errors that occur at hello IoT hub and are related toofile upload functionality.</span></span> <span data-ttu-id="1be73-145">Ta kategoria zawiera:</span><span class="sxs-lookup"><span data-stu-id="1be73-145">This category includes:</span></span>

* <span data-ttu-id="1be73-146">Błędy, które występują w przypadku hello identyfikatora URI połączenia SAS, takie jak kiedy wygasa przed urządzenia powiadamia Centrum hello ukończone przekazywania.</span><span class="sxs-lookup"><span data-stu-id="1be73-146">Errors that occur with hello SAS URI, such as when it expires before a device notifies hello hub of a completed upload.</span></span>
* <span data-ttu-id="1be73-147">Zgłoszone przez urządzenie hello przekazywania nie powiodło się.</span><span class="sxs-lookup"><span data-stu-id="1be73-147">Failed uploads reported by hello device.</span></span>
* <span data-ttu-id="1be73-148">Błędy występujące po plik nie zostanie znaleziony w magazynie podczas tworzenia komunikatu powiadomienia Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="1be73-148">Errors that occur when a file is not found in storage during IoT Hub notification message creation.</span></span>

<span data-ttu-id="1be73-149">Ta kategoria nie może przechwycić błędów, które są wykonywane bezpośrednio, gdy urządzenie hello jest przekazywanie toostorage pliku.</span><span class="sxs-lookup"><span data-stu-id="1be73-149">This category cannot catch errors that directly occur while hello device is uploading a file toostorage.</span></span>

```json
{
    "authType": "{\"scope\":\"hub\",\"type\":\"sas\",\"issuer\":\"iothub\"}",
    "protocol": "HTTP",
    "time": " UTC timestamp",
    "operationName": "ingress",
    "category": "fileUpload",
    "level": "Error",
    "statusCode": 4XX,
    "statusType": 4XX001,
    "statusDescription": "MessageDescription",
    "deviceId": "device-ID",
    "blobUri": "http//bloburi.com",
    "durationMs": 1234
}
```

### <a name="message-routing"></a><span data-ttu-id="1be73-150">Rozsyłanie wiadomości</span><span class="sxs-lookup"><span data-stu-id="1be73-150">Message routing</span></span>

<span data-ttu-id="1be73-151">Kategoria routingu wiadomość Hello śledzi błędów występujących podczas oceny trasy wiadomości i punktu końcowego kondycję postrzegane przez Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="1be73-151">hello message routing category tracks errors that occur during message route evaluation and endpoint health as perceived by IoT Hub.</span></span> <span data-ttu-id="1be73-152">Ta kategoria zawiera zdarzenia, np. gdy reguła zwraca zbyt "undefined", gdy Centrum IoT oznacza punkt końcowy jako wiadomości i innych błędów, odbierane z punktu końcowego.</span><span class="sxs-lookup"><span data-stu-id="1be73-152">This category includes events such as when a rule evaluates too"undefined", when IoT Hub marks an endpoint as dead, and any other errors received from an endpoint.</span></span> <span data-ttu-id="1be73-153">Ta kategoria nie ma określonego błędy dotyczące wiadomości powitania się (na przykład urządzenie ograniczania błędy), które zostały zgłoszone w kategorii "telemetrii urządzenia" hello.</span><span class="sxs-lookup"><span data-stu-id="1be73-153">This category does not include specific errors about hello messages themselves (such as device throttling errors), which are reported under hello "device telemetry" category.</span></span>

```json
{
    "messageSizeInBytes": 1234,
    "time": "UTC timestamp",
    "operationName": "ingress",
    "category": "routes",
    "level": "Error",
    "deviceId": "device-ID",
    "messageId": "ID of message",
    "routeName": "myroute",
    "endpointName": "myendpoint",
    "details": "ExternalEndpointDisabled"
}
```

## <a name="view-events"></a><span data-ttu-id="1be73-154">Wyświetl wydarzenia</span><span class="sxs-lookup"><span data-stu-id="1be73-154">View events</span></span>

<span data-ttu-id="1be73-155">Można użyć hello *explorer Centrum iothub* tooquickly narzędzie test, że Centrum IoT generuje monitorowania zdarzeń.</span><span class="sxs-lookup"><span data-stu-id="1be73-155">You can use hello *iothub-explorer* tool tooquickly test that your IoT hub is generating monitoring events.</span></span> <span data-ttu-id="1be73-156">Witaj tooinstall narzędzie, zobacz instrukcje hello hello [explorer Centrum iothub] [ lnk-iothub-explorer] repozytorium GitHub.</span><span class="sxs-lookup"><span data-stu-id="1be73-156">tooinstall hello tool, see hello instructions in hello [iothub-explorer][lnk-iothub-explorer] GitHub repository.</span></span>

1. <span data-ttu-id="1be73-157">Upewnij się, że hello **połączeń** monitorowania kategorii ustawiono zbyt**pełne** w portalu hello.</span><span class="sxs-lookup"><span data-stu-id="1be73-157">Make sure hello **Connections** monitoring category is set too**Verbose** in hello portal.</span></span>

1. <span data-ttu-id="1be73-158">W wierszu polecenia Uruchom hello poniższych poleceń tooread z hello punkt końcowy monitorowania:</span><span class="sxs-lookup"><span data-stu-id="1be73-158">At a command-prompt, run hello following command tooread from hello monitoring endpoint:</span></span>

    ```
    iothub-explorer monitor-ops --login {your iothubowner connection string}
    ```

1. <span data-ttu-id="1be73-159">W innego wiersza polecenia Uruchom następujące polecenie toosimulate hello urządzenia wysyłania wiadomości urządzenia do chmury:</span><span class="sxs-lookup"><span data-stu-id="1be73-159">In another command-prompt, run hello following command toosimulate a device sending device-to-cloud messages:</span></span>

    ```
    iothub-explorer simulate-device {your device name} --send "My test message" --login {your iothubowner connection string}
    ```

1. <span data-ttu-id="1be73-160">pierwszy wiersz polecenia Hello przedstawiono zdarzenia monitorowania hello hello symulowane urządzenie łączy tooyour Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="1be73-160">hello first command-prompt shows hello monitoring events as hello simulated device connects tooyour IoT hub.</span></span>

## <a name="connect-toohello-monitoring-endpoint"></a><span data-ttu-id="1be73-161">Połącz toohello punkt końcowy monitorowania</span><span class="sxs-lookup"><span data-stu-id="1be73-161">Connect toohello monitoring endpoint</span></span>

<span data-ttu-id="1be73-162">Witaj, monitorowanie punktu końcowego w Centrum IoT jest punktem końcowym zgodnego Centrum zdarzeń.</span><span class="sxs-lookup"><span data-stu-id="1be73-162">hello monitoring endpoint on your IoT hub is an Event Hub-compatible endpoint.</span></span> <span data-ttu-id="1be73-163">Można użyć dowolnego mechanizm, który współpracuje z usługi Event Hubs tooread monitorowania wiadomości z tego punktu końcowego.</span><span class="sxs-lookup"><span data-stu-id="1be73-163">You can use any mechanism that works with Event Hubs tooread monitoring messages from this endpoint.</span></span> <span data-ttu-id="1be73-164">Witaj poniższy przykład tworzy podstawowe reader, który nie jest odpowiedni dla wdrożenia wysokiej przepływności.</span><span class="sxs-lookup"><span data-stu-id="1be73-164">hello following sample creates a basic reader that is not suitable for a high throughput deployment.</span></span> <span data-ttu-id="1be73-165">Aby uzyskać więcej informacji dotyczących sposobu tooprocess komunikaty z usługi Event Hubs, zobacz hello [Rozpoczynanie pracy z usługą Event Hubs] [ lnk-eventhubs-tutorial] samouczka.</span><span class="sxs-lookup"><span data-stu-id="1be73-165">For more information about how tooprocess messages from Event Hubs, see hello [Get Started with Event Hubs][lnk-eventhubs-tutorial] tutorial.</span></span>

<span data-ttu-id="1be73-166">tooconnect toohello punkt końcowy monitorowania, należy nazwa punktu końcowego i hello ciąg połączenia.</span><span class="sxs-lookup"><span data-stu-id="1be73-166">tooconnect toohello monitoring endpoint, you need a connection string and hello endpoint name.</span></span> <span data-ttu-id="1be73-167">Hello następujące kroki przedstawiają sposób toofind hello niezbędnych wartości w portalu hello:</span><span class="sxs-lookup"><span data-stu-id="1be73-167">hello following steps show you how toofind hello necessary values in hello portal:</span></span>

1. <span data-ttu-id="1be73-168">W portalu hello Przejdź tooyour bloku zasobów Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="1be73-168">In hello portal, navigate tooyour IoT Hub resource blade.</span></span>

1. <span data-ttu-id="1be73-169">Wybierz **operacje monitorowania**i zanotuj hello **nazwę Centrum zdarzeń zgodnych** i **punktu końcowego Centrum zdarzeń zgodnych** wartości:</span><span class="sxs-lookup"><span data-stu-id="1be73-169">Choose **Operations monitoring**, and make a note of hello **Event Hub-compatible name** and **Event Hub-compatible endpoint** values:</span></span>

    ![Wartości punktu końcowego zgodnych z Centrum zdarzeń][img-endpoints]

1. <span data-ttu-id="1be73-171">Wybierz **zasady dostępu współużytkowanego**, a następnie wybierz **usługi**.</span><span class="sxs-lookup"><span data-stu-id="1be73-171">Choose **Shared access policies**, then choose **service**.</span></span> <span data-ttu-id="1be73-172">Zanotuj hello **klucz podstawowy** wartość:</span><span class="sxs-lookup"><span data-stu-id="1be73-172">Make a note of hello **Primary key** value:</span></span>

    ![Klucz podstawowy zasady dostępu współdzielonego usługi][img-service-key]

<span data-ttu-id="1be73-174">Witaj Poniższy przykładowy kod C# jest pobierana z programu Visual Studio **Windows Desktop klasycznego** aplikacji konsolowej C#.</span><span class="sxs-lookup"><span data-stu-id="1be73-174">hello following C# code sample is taken from a Visual Studio **Windows Classic Desktop** C# console app.</span></span> <span data-ttu-id="1be73-175">Projekt Hello ma hello **WindowsAzure.ServiceBus** zainstalowany pakiet NuGet.</span><span class="sxs-lookup"><span data-stu-id="1be73-175">hello project has hello **WindowsAzure.ServiceBus** NuGet package installed.</span></span>

* <span data-ttu-id="1be73-176">Zastąp symbol zastępczy parametrów połączenia hello ciąg połączenia, który używa hello **punktu końcowego Centrum zdarzeń zgodnych** i usługa **klucz podstawowy** wartości zanotowany wcześniej, jak pokazano poniżej hello przykład:</span><span class="sxs-lookup"><span data-stu-id="1be73-176">Replace hello connection string placeholder with a connection string that uses hello **Event Hub-compatible endpoint** and service **Primary key** values you noted previously as shown in hello following example:</span></span>

    ```cs
    "Endpoint={your Event Hub-compatible endpoint};SharedAccessKeyName=service;SharedAccessKey={your service primary key value}"
    ```

* <span data-ttu-id="1be73-177">Zastąp hello monitorowania symbol zastępczy Nazwa punktu końcowego hello **nazwę Centrum zdarzeń zgodnych** wartość zanotowany wcześniej.</span><span class="sxs-lookup"><span data-stu-id="1be73-177">Replace hello monitoring endpoint name placeholder with hello **Event Hub-compatible name** value you noted previously.</span></span>

```cs
class Program
{
    static string connectionString = "{your monitoring endpoint connection string}";
    static string monitoringEndpointName = "{your monitoring endpoint name}";
    static EventHubClient eventHubClient;

    static void Main(string[] args)
    {
        Console.WriteLine("Monitoring. Press Enter key tooexit.\n");

        eventHubClient = EventHubClient.CreateFromConnectionString(connectionString, monitoringEndpointName);
        var d2cPartitions = eventHubClient.GetRuntimeInformation().PartitionIds;
        CancellationTokenSource cts = new CancellationTokenSource();
        var tasks = new List<Task>();

        foreach (string partition in d2cPartitions)
        {
            tasks.Add(ReceiveMessagesFromDeviceAsync(partition, cts.Token));
        }

        Console.ReadLine();
        Console.WriteLine("Exiting...");
        cts.Cancel();
        Task.WaitAll(tasks.ToArray());
    }

    private static async Task ReceiveMessagesFromDeviceAsync(string partition, CancellationToken ct)
    {
        var eventHubReceiver = eventHubClient.GetDefaultConsumerGroup().CreateReceiver(partition, DateTime.UtcNow);
        while (true)
        {
            if (ct.IsCancellationRequested)
            {
                await eventHubReceiver.CloseAsync();
                break;
            }

            EventData eventData = await eventHubReceiver.ReceiveAsync(new TimeSpan(0,0,10));

            if (eventData != null)
            {
                string data = Encoding.UTF8.GetString(eventData.GetBytes());
                Console.WriteLine("Message received. Partition: {0} Data: '{1}'", partition, data);
            }
        }
    }
}
```

## <a name="next-steps"></a><span data-ttu-id="1be73-178">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="1be73-178">Next steps</span></span>
<span data-ttu-id="1be73-179">toofurther Poznaj możliwości hello Centrum IoT, zobacz:</span><span class="sxs-lookup"><span data-stu-id="1be73-179">toofurther explore hello capabilities of IoT Hub, see:</span></span>

* <span data-ttu-id="1be73-180">[Przewodnik dewelopera Centrum IoT][lnk-devguide]</span><span class="sxs-lookup"><span data-stu-id="1be73-180">[IoT Hub developer guide][lnk-devguide]</span></span>
* <span data-ttu-id="1be73-181">[Symuluje urządzenia Azure IoT krawędzi][lnk-iotedge]</span><span class="sxs-lookup"><span data-stu-id="1be73-181">[Simulating a device with Azure IoT Edge][lnk-iotedge]</span></span>

<!-- Links and images -->
[1]: media/iot-hub-operations-monitoring/enable-OM-1.png
[2]: media/iot-hub-operations-monitoring/enable-OM-2.png
[img-endpoints]: media/iot-hub-operations-monitoring/monitoring-endpoint.png
[img-service-key]: media/iot-hub-operations-monitoring/service-key.png

[lnk-get-started]: iot-hub-csharp-csharp-getstarted.md
[lnk-diagnostic-metrics]: iot-hub-metrics.md
[lnk-scaling]: iot-hub-scaling.md
[lnk-dr]: iot-hub-ha-dr.md

[lnk-devguide]: iot-hub-devguide.md
[lnk-iotedge]: iot-hub-linux-iot-edge-simulated-device.md
[lnk-iothub-explorer]: https://github.com/azure/iothub-explorer
[lnk-eventhubs-tutorial]: ../event-hubs/event-hubs-csharp-ephcs-getstarted.md