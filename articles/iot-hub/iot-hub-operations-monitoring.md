---
title: Operacje platformy Azure IoT Hub monitorowania | Dokumentacja firmy Microsoft
description: "Jak używać operacji centrum IoT Azure monitorowania do monitorowania stanu operacji w Centrum IoT w czasie rzeczywistym."
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
ms.openlocfilehash: b6de5c5df5f9401a41be152bfa06eb994594e83d
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
# <a name="iot-hub-operations-monitoring"></a><span data-ttu-id="dc012-103">Monitorowanie operacji centrum IoT</span><span class="sxs-lookup"><span data-stu-id="dc012-103">IoT Hub operations monitoring</span></span>

<span data-ttu-id="dc012-104">Monitorowanie operacji centrum IoT umożliwia monitorowanie stanu operacji w Centrum IoT w czasie rzeczywistym.</span><span class="sxs-lookup"><span data-stu-id="dc012-104">IoT Hub operations monitoring enables you to monitor the status of operations on your IoT hub in real time.</span></span> <span data-ttu-id="dc012-105">Centrum IoT śledzi zdarzenia przez różne kategorie działań.</span><span class="sxs-lookup"><span data-stu-id="dc012-105">IoT Hub tracks events across several categories of operations.</span></span> <span data-ttu-id="dc012-106">Można włączyć do wysyłania zdarzeń z co najmniej jednej kategorii do punktu końcowego Centrum IoT do przetwarzania.</span><span class="sxs-lookup"><span data-stu-id="dc012-106">You can opt into sending events from one or more categories to an endpoint of your IoT hub for processing.</span></span> <span data-ttu-id="dc012-107">Możesz monitorować dane błędy lub konfigurowanie bardziej złożonych przetwarzania na podstawie wzorców danych.</span><span class="sxs-lookup"><span data-stu-id="dc012-107">You can monitor the data for errors or set up more complex processing based on data patterns.</span></span>

<span data-ttu-id="dc012-108">Centrum IoT monitoruje sześć kategorii zdarzeń:</span><span class="sxs-lookup"><span data-stu-id="dc012-108">IoT Hub monitors six categories of events:</span></span>

* <span data-ttu-id="dc012-109">Operacje tożsamości urządzenia</span><span class="sxs-lookup"><span data-stu-id="dc012-109">Device identity operations</span></span>
* <span data-ttu-id="dc012-110">Telemetrii urządzenia</span><span class="sxs-lookup"><span data-stu-id="dc012-110">Device telemetry</span></span>
* <span data-ttu-id="dc012-111">Komunikaty chmury do urządzenia</span><span class="sxs-lookup"><span data-stu-id="dc012-111">Cloud-to-device messages</span></span>
* <span data-ttu-id="dc012-112">Połączenia</span><span class="sxs-lookup"><span data-stu-id="dc012-112">Connections</span></span>
* <span data-ttu-id="dc012-113">Przekazywania plików</span><span class="sxs-lookup"><span data-stu-id="dc012-113">File uploads</span></span>
* <span data-ttu-id="dc012-114">Rozsyłanie wiadomości</span><span class="sxs-lookup"><span data-stu-id="dc012-114">Message routing</span></span>

## <a name="how-to-enable-operations-monitoring"></a><span data-ttu-id="dc012-115">Jak włączyć operacje monitorowania</span><span class="sxs-lookup"><span data-stu-id="dc012-115">How to enable operations monitoring</span></span>

1. <span data-ttu-id="dc012-116">Tworzenie Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="dc012-116">Create an IoT hub.</span></span> <span data-ttu-id="dc012-117">Instrukcje można znaleźć na temat sposobu tworzenia Centrum IoT w [wprowadzenie] [ lnk-get-started] przewodnik.</span><span class="sxs-lookup"><span data-stu-id="dc012-117">You can find instructions on how to create an IoT hub in the [Get Started][lnk-get-started] guide.</span></span>

1. <span data-ttu-id="dc012-118">Otwarcie bloku Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="dc012-118">Open the blade of your IoT hub.</span></span> <span data-ttu-id="dc012-119">Z tego miejsca, kliknij przycisk **operacje monitorowania**.</span><span class="sxs-lookup"><span data-stu-id="dc012-119">From there, click **Operations monitoring**.</span></span>

    ![Operacje związane z dostępem monitorowania konfiguracji w portalu][1]

1. <span data-ttu-id="dc012-121">Wybierz kategorie monitorowania, chcesz monitorować, a następnie kliknij przycisk **zapisać**.</span><span class="sxs-lookup"><span data-stu-id="dc012-121">Select the monitoring categories you wish to monitor, and then click **Save**.</span></span> <span data-ttu-id="dc012-122">Zdarzenia są dostępne do odczytu z punktu końcowego Centrum zdarzeń zgodnych na liście **ustawienia monitorowania**.</span><span class="sxs-lookup"><span data-stu-id="dc012-122">The events are available for reading from the Event Hub-compatible endpoint listed in **Monitoring settings**.</span></span> <span data-ttu-id="dc012-123">Nosi nazwę punktu końcowego Centrum IoT `messages/operationsmonitoringevents`.</span><span class="sxs-lookup"><span data-stu-id="dc012-123">The IoT Hub endpoint is called `messages/operationsmonitoringevents`.</span></span>

    ![Skonfiguruj operacje monitorowania na Centrum IoT][2]

> [!NOTE]
> <span data-ttu-id="dc012-125">Wybieranie **pełne** monitorowania **połączeń** category powoduje, że Centrum IoT można wygenerować komunikaty dodatkowych diagnostyczne.</span><span class="sxs-lookup"><span data-stu-id="dc012-125">Selecting **Verbose** monitoring for the **Connections** category causes IoT Hub to generate additional diagnostics messages.</span></span> <span data-ttu-id="dc012-126">Dla wszystkich innych kategoriach **pełne** zawiera zmiany ustawień ilość informacji Centrum IoT w każdy komunikat o błędzie.</span><span class="sxs-lookup"><span data-stu-id="dc012-126">For all other categories, the **Verbose** setting changes the quantity of information IoT Hub includes in each error message.</span></span>

## <a name="event-categories-and-how-to-use-them"></a><span data-ttu-id="dc012-127">Kategorie zdarzeń i sposobu ich użycia</span><span class="sxs-lookup"><span data-stu-id="dc012-127">Event categories and how to use them</span></span>

<span data-ttu-id="dc012-128">Każdy operacje monitorowania śledzi kategorii ma inny typ interakcji z Centrum IoT i każda kategoria monitorowania schematu definiującego struktury zdarzenia w tej kategorii.</span><span class="sxs-lookup"><span data-stu-id="dc012-128">Each operations monitoring category tracks a different type of interaction with IoT Hub, and each monitoring category has a schema that defines how events in that category are structured.</span></span>

### <a name="device-identity-operations"></a><span data-ttu-id="dc012-129">Operacje tożsamości urządzenia</span><span class="sxs-lookup"><span data-stu-id="dc012-129">Device identity operations</span></span>

<span data-ttu-id="dc012-130">Kategoria operacje tożsamości urządzenia śledzi błędów występujących podczas próby utworzenia, zaktualizować lub usunąć wpis w rejestrze tożsamości Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="dc012-130">The device identity operations category tracks errors that occur when you attempt to create, update, or delete an entry in your IoT hub's identity registry.</span></span> <span data-ttu-id="dc012-131">Ta kategoria śledzenia jest przydatne w przypadku inicjowania obsługi scenariuszy.</span><span class="sxs-lookup"><span data-stu-id="dc012-131">Tracking this category is useful for provisioning scenarios.</span></span>

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

### <a name="device-telemetry"></a><span data-ttu-id="dc012-132">Telemetrii urządzenia</span><span class="sxs-lookup"><span data-stu-id="dc012-132">Device telemetry</span></span>

<span data-ttu-id="dc012-133">Kategoria telemetrii urządzenia śledzi błędy występują w Centrum IoT, które są powiązane z potokiem telemetrii.</span><span class="sxs-lookup"><span data-stu-id="dc012-133">The device telemetry category tracks errors that occur at the IoT hub and are related to the telemetry pipeline.</span></span> <span data-ttu-id="dc012-134">Ta kategoria zawiera błędy występujące podczas wysyłania zdarzenia telemetrii (takie jak dławienie) i odbieranie zdarzeń telemetrii (np. czytnik nieautoryzowanych).</span><span class="sxs-lookup"><span data-stu-id="dc012-134">This category includes errors that occur when sending telemetry events (such as throttling) and receiving telemetry events (such as unauthorized reader).</span></span> <span data-ttu-id="dc012-135">Ta kategoria nie może przechwycić błędów spowodowanych przez kod działający na urządzeniu.</span><span class="sxs-lookup"><span data-stu-id="dc012-135">This category cannot catch errors caused by code running on the device itself.</span></span>

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

### <a name="cloud-to-device-commands"></a><span data-ttu-id="dc012-136">Polecenia chmury do urządzenia</span><span class="sxs-lookup"><span data-stu-id="dc012-136">Cloud-to-device commands</span></span>

<span data-ttu-id="dc012-137">Kategoria polecenia chmury do urządzenia śledzi błędy występują w Centrum IoT, które są powiązane z potokiem wiadomości chmury do urządzenia.</span><span class="sxs-lookup"><span data-stu-id="dc012-137">The cloud-to-device commands category tracks errors that occur at the IoT hub and are related to the cloud-to-device message pipeline.</span></span> <span data-ttu-id="dc012-138">Ta kategoria zawiera błędy występujące podczas wysyłania wiadomości chmury do urządzenia (takich jak nieautoryzowanego nadawcę), odbierania wiadomości chmury do urządzenia (takich jak przekroczona liczba dostarczania) i odbieranie komunikatu chmura urządzenie opinii (takie jak opinii wygasł).</span><span class="sxs-lookup"><span data-stu-id="dc012-138">This category includes errors that occur when sending cloud-to-device messages (such as unauthorized sender), receiving cloud-to-device messages (such as delivery count exceeded), and receiving cloud-to-device message feedback (such as feedback expired).</span></span> <span data-ttu-id="dc012-139">Ta kategoria nie przechwytuje błędy z urządzenia, które nieprawidłowo obsługuje komunikat chmury do urządzenia, jeśli komunikatu chmura urządzenie zostało pomyślnie dostarczone.</span><span class="sxs-lookup"><span data-stu-id="dc012-139">This category does not catch errors from a device that improperly handles a cloud-to-device message if the cloud-to-device message was delivered successfully.</span></span>

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

### <a name="connections"></a><span data-ttu-id="dc012-140">Połączenia</span><span class="sxs-lookup"><span data-stu-id="dc012-140">Connections</span></span>

<span data-ttu-id="dc012-141">Kategoria połączenia śledzi błędów występujących podczas urządzeń Połącz lub Rozłącz z Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="dc012-141">The connections category tracks errors that occur when devices connect or disconnect from an IoT hub.</span></span> <span data-ttu-id="dc012-142">Śledzenie tej kategorii jest przydatne do identyfikowania próby nieautoryzowanego połączenia i śledzenia, gdy połączenie zostanie przerwane dla urządzeń w zakresie łączności niska.</span><span class="sxs-lookup"><span data-stu-id="dc012-142">Tracking this category is useful for identifying unauthorized connection attempts and for tracking when a connection is lost for devices in areas of poor connectivity.</span></span>

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

### <a name="file-uploads"></a><span data-ttu-id="dc012-143">Przekazywania plików</span><span class="sxs-lookup"><span data-stu-id="dc012-143">File uploads</span></span>

<span data-ttu-id="dc012-144">Kategoria przekazywania pliku śledzenia błędów, które występują w Centrum IoT i są związane z funkcji przekazywania plików.</span><span class="sxs-lookup"><span data-stu-id="dc012-144">The file upload category tracks errors that occur at the IoT hub and are related to file upload functionality.</span></span> <span data-ttu-id="dc012-145">Ta kategoria zawiera:</span><span class="sxs-lookup"><span data-stu-id="dc012-145">This category includes:</span></span>

* <span data-ttu-id="dc012-146">Błędy, które występują w przypadku identyfikatora URI połączenia SAS, takie jak kiedy wygasa przed urządzenia powiadamia koncentratora przekazywanie zostało ukończone.</span><span class="sxs-lookup"><span data-stu-id="dc012-146">Errors that occur with the SAS URI, such as when it expires before a device notifies the hub of a completed upload.</span></span>
* <span data-ttu-id="dc012-147">Przekazywanie zgłoszonych przez urządzenia nie powiodła się.</span><span class="sxs-lookup"><span data-stu-id="dc012-147">Failed uploads reported by the device.</span></span>
* <span data-ttu-id="dc012-148">Błędy występujące po plik nie zostanie znaleziony w magazynie podczas tworzenia komunikatu powiadomienia Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="dc012-148">Errors that occur when a file is not found in storage during IoT Hub notification message creation.</span></span>

<span data-ttu-id="dc012-149">Ta kategoria nie może przechwycić błędów, które są wykonywane bezpośrednio, gdy urządzenie jest przekazywany do magazynu.</span><span class="sxs-lookup"><span data-stu-id="dc012-149">This category cannot catch errors that directly occur while the device is uploading a file to storage.</span></span>

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

### <a name="message-routing"></a><span data-ttu-id="dc012-150">Rozsyłanie wiadomości</span><span class="sxs-lookup"><span data-stu-id="dc012-150">Message routing</span></span>

<span data-ttu-id="dc012-151">Kategoria routingu wiadomości śledzi błędów występujących podczas oceny trasy wiadomości i punktu końcowego kondycję postrzegane przez Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="dc012-151">The message routing category tracks errors that occur during message route evaluation and endpoint health as perceived by IoT Hub.</span></span> <span data-ttu-id="dc012-152">Ta kategoria zawiera zdarzenia, np. gdy reguła zwraca "undefined", gdy Centrum IoT oznacza punkt końcowy jako wiadomości i innych błędów, odbierane z punktu końcowego.</span><span class="sxs-lookup"><span data-stu-id="dc012-152">This category includes events such as when a rule evaluates to "undefined", when IoT Hub marks an endpoint as dead, and any other errors received from an endpoint.</span></span> <span data-ttu-id="dc012-153">Ta kategoria nie ma określonych błędów o komunikatach się (na przykład urządzenie ograniczania błędy), które zostały zgłoszone w kategorii "telemetrii urządzenia".</span><span class="sxs-lookup"><span data-stu-id="dc012-153">This category does not include specific errors about the messages themselves (such as device throttling errors), which are reported under the "device telemetry" category.</span></span>

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

## <a name="view-events"></a><span data-ttu-id="dc012-154">Wyświetl wydarzenia</span><span class="sxs-lookup"><span data-stu-id="dc012-154">View events</span></span>

<span data-ttu-id="dc012-155">Można użyć *explorer Centrum iothub* narzędzia do testowania szybkie, że Centrum IoT generuje monitorowania zdarzeń.</span><span class="sxs-lookup"><span data-stu-id="dc012-155">You can use the *iothub-explorer* tool to quickly test that your IoT hub is generating monitoring events.</span></span> <span data-ttu-id="dc012-156">Aby zainstalować narzędzie, zobacz instrukcje w [explorer Centrum iothub] [ lnk-iothub-explorer] repozytorium GitHub.</span><span class="sxs-lookup"><span data-stu-id="dc012-156">To install the tool, see the instructions in the [iothub-explorer][lnk-iothub-explorer] GitHub repository.</span></span>

1. <span data-ttu-id="dc012-157">Upewnij się, że **połączeń** monitorowania kategorii ustawiono **pełne** w portalu.</span><span class="sxs-lookup"><span data-stu-id="dc012-157">Make sure the **Connections** monitoring category is set to **Verbose** in the portal.</span></span>

1. <span data-ttu-id="dc012-158">W wierszu polecenia Uruchom następujące polecenie, aby odczytać z punktu końcowego monitorowania:</span><span class="sxs-lookup"><span data-stu-id="dc012-158">At a command-prompt, run the following command to read from the monitoring endpoint:</span></span>

    ```
    iothub-explorer monitor-ops --login {your iothubowner connection string}
    ```

1. <span data-ttu-id="dc012-159">W innego wiersza polecenia Uruchom następujące polecenie, aby symulować urządzenia wysyłania wiadomości urządzenia do chmury:</span><span class="sxs-lookup"><span data-stu-id="dc012-159">In another command-prompt, run the following command to simulate a device sending device-to-cloud messages:</span></span>

    ```
    iothub-explorer simulate-device {your device name} --send "My test message" --login {your iothubowner connection string}
    ```

1. <span data-ttu-id="dc012-160">Pierwszy wiersz polecenia zawiera zdarzenia monitorowania, jak symulowane urządzenie łączy się z Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="dc012-160">The first command-prompt shows the monitoring events as the simulated device connects to your IoT hub.</span></span>

## <a name="connect-to-the-monitoring-endpoint"></a><span data-ttu-id="dc012-161">Połącz z punktem końcowym monitorowania</span><span class="sxs-lookup"><span data-stu-id="dc012-161">Connect to the monitoring endpoint</span></span>

<span data-ttu-id="dc012-162">Punkt końcowy monitorowania w Centrum IoT jest punktem końcowym zgodnego Centrum zdarzeń.</span><span class="sxs-lookup"><span data-stu-id="dc012-162">The monitoring endpoint on your IoT hub is an Event Hub-compatible endpoint.</span></span> <span data-ttu-id="dc012-163">Można użyć dowolnego mechanizm, który współpracuje z usługą Event Hubs można odczytać monitorowania wiadomości z tego punktu końcowego.</span><span class="sxs-lookup"><span data-stu-id="dc012-163">You can use any mechanism that works with Event Hubs to read monitoring messages from this endpoint.</span></span> <span data-ttu-id="dc012-164">W poniższym przykładzie tworzone podstawowe reader, który nie jest odpowiedni dla wdrożenia wysokiej przepływności.</span><span class="sxs-lookup"><span data-stu-id="dc012-164">The following sample creates a basic reader that is not suitable for a high throughput deployment.</span></span> <span data-ttu-id="dc012-165">Więcej informacji na temat przetwarzania komunikatów z usługi Event Hubs znajduje się w samouczku [Rozpoczynanie pracy z usługą Event Hubs][lnk-eventhubs-tutorial].</span><span class="sxs-lookup"><span data-stu-id="dc012-165">For more information about how to process messages from Event Hubs, see the [Get Started with Event Hubs][lnk-eventhubs-tutorial] tutorial.</span></span>

<span data-ttu-id="dc012-166">Aby połączyć się punkt końcowy monitorowania, należy ciąg połączenia i nazwę punktu końcowego.</span><span class="sxs-lookup"><span data-stu-id="dc012-166">To connect to the monitoring endpoint, you need a connection string and the endpoint name.</span></span> <span data-ttu-id="dc012-167">Poniższe kroki pokazują, jak znaleźć niezbędnych wartości w portalu:</span><span class="sxs-lookup"><span data-stu-id="dc012-167">The following steps show you how to find the necessary values in the portal:</span></span>

1. <span data-ttu-id="dc012-168">W portalu przejdź do bloku zasobów z Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="dc012-168">In the portal, navigate to your IoT Hub resource blade.</span></span>

1. <span data-ttu-id="dc012-169">Wybierz **operacje monitorowania**i zanotuj **nazwę Centrum zdarzeń zgodnych** i **punktu końcowego Centrum zdarzeń zgodnych** wartości:</span><span class="sxs-lookup"><span data-stu-id="dc012-169">Choose **Operations monitoring**, and make a note of the **Event Hub-compatible name** and **Event Hub-compatible endpoint** values:</span></span>

    ![Wartości punktu końcowego zgodnych z Centrum zdarzeń][img-endpoints]

1. <span data-ttu-id="dc012-171">Wybierz **zasady dostępu współużytkowanego**, a następnie wybierz **usługi**.</span><span class="sxs-lookup"><span data-stu-id="dc012-171">Choose **Shared access policies**, then choose **service**.</span></span> <span data-ttu-id="dc012-172">Zanotuj **klucz podstawowy** wartość:</span><span class="sxs-lookup"><span data-stu-id="dc012-172">Make a note of the **Primary key** value:</span></span>

    ![Klucz podstawowy zasady dostępu współdzielonego usługi][img-service-key]

<span data-ttu-id="dc012-174">Poniższy przykład kodu C# jest pobierana z programu Visual Studio **Windows Desktop klasycznego** aplikacji konsolowej C#.</span><span class="sxs-lookup"><span data-stu-id="dc012-174">The following C# code sample is taken from a Visual Studio **Windows Classic Desktop** C# console app.</span></span> <span data-ttu-id="dc012-175">Projekt posiada **WindowsAzure.ServiceBus** zainstalowany pakiet NuGet.</span><span class="sxs-lookup"><span data-stu-id="dc012-175">The project has the **WindowsAzure.ServiceBus** NuGet package installed.</span></span>

* <span data-ttu-id="dc012-176">Zastąp symbol zastępczy parametrów połączenia przy użyciu parametrów połączenia, który używa **punktu końcowego Centrum zdarzeń zgodnych** i usługa **klucz podstawowy** wartości zanotowany wcześniej, jak pokazano w poniższym przykładzie:</span><span class="sxs-lookup"><span data-stu-id="dc012-176">Replace the connection string placeholder with a connection string that uses the **Event Hub-compatible endpoint** and service **Primary key** values you noted previously as shown in the following example:</span></span>

    ```cs
    "Endpoint={your Event Hub-compatible endpoint};SharedAccessKeyName=service;SharedAccessKey={your service primary key value}"
    ```

* <span data-ttu-id="dc012-177">Zastąp monitorowania symbol zastępczy Nazwa punktu końcowego z **nazwę Centrum zdarzeń zgodnych** wartość zanotowany wcześniej.</span><span class="sxs-lookup"><span data-stu-id="dc012-177">Replace the monitoring endpoint name placeholder with the **Event Hub-compatible name** value you noted previously.</span></span>

```cs
class Program
{
    static string connectionString = "{your monitoring endpoint connection string}";
    static string monitoringEndpointName = "{your monitoring endpoint name}";
    static EventHubClient eventHubClient;

    static void Main(string[] args)
    {
        Console.WriteLine("Monitoring. Press Enter key to exit.\n");

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

## <a name="next-steps"></a><span data-ttu-id="dc012-178">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="dc012-178">Next steps</span></span>
<span data-ttu-id="dc012-179">Aby dokładniej analizować możliwości Centrum IoT, zobacz:</span><span class="sxs-lookup"><span data-stu-id="dc012-179">To further explore the capabilities of IoT Hub, see:</span></span>

* <span data-ttu-id="dc012-180">[Przewodnik dewelopera Centrum IoT][lnk-devguide]</span><span class="sxs-lookup"><span data-stu-id="dc012-180">[IoT Hub developer guide][lnk-devguide]</span></span>
* <span data-ttu-id="dc012-181">[Symuluje urządzenia Azure IoT krawędzi][lnk-iotedge]</span><span class="sxs-lookup"><span data-stu-id="dc012-181">[Simulating a device with Azure IoT Edge][lnk-iotedge]</span></span>

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