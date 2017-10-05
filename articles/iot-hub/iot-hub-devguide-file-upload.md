---
title: Zrozumienie przekazania pliku Centrum IoT Azure | Dokumentacja firmy Microsoft
description: "Przewodnik dewelopera — użycie funkcji przekazywania plików z Centrum IoT do zarządzania przekazywania plików z urządzenia do kontenera obiektów blob magazynu Azure."
services: iot-hub
documentationcenter: .net
author: dominicbetts
manager: timlt
editor: 
ms.assetid: a0427925-3e40-4fcd-96c1-2a31d1ddc14b
ms.service: iot-hub
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/08/2017
ms.author: dobett
ms.openlocfilehash: 75a6b9bc3ecfe6d6901bb38e312d62333f38daf1
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/18/2017
---
# <a name="upload-files-with-iot-hub"></a><span data-ttu-id="48a48-103">Przekazywanie plików z Centrum IoT</span><span class="sxs-lookup"><span data-stu-id="48a48-103">Upload files with IoT Hub</span></span>

<span data-ttu-id="48a48-104">Jak wyjaśniono w [punkty końcowe Centrum IoT] [ lnk-endpoints] artykułu, urządzenie może inicjować przekazywania pliku, wysyłając powiadomienia za pośrednictwem punktu końcowego uwzględniającym urządzenia (**/devices/ {deviceId} / pliki**).</span><span class="sxs-lookup"><span data-stu-id="48a48-104">As detailed in the [IoT Hub endpoints][lnk-endpoints] article, a device can initiate a file upload by sending a notification through a device-facing endpoint (**/devices/{deviceId}/files**).</span></span> <span data-ttu-id="48a48-105">Gdy urządzenia IoT Hub powiadamia o zakończeniu przekazywania, Centrum IoT wysyła komunikat z powiadomieniem przekazywania plików za pomocą **/messages/servicebound/filenotifications** połączonej usługi punktu końcowego.</span><span class="sxs-lookup"><span data-stu-id="48a48-105">When a device notifies IoT Hub that an upload is complete, IoT Hub sends a file upload notification message through the **/messages/servicebound/filenotifications** service-facing endpoint.</span></span>

<span data-ttu-id="48a48-106">Zamiast pośrednictwa komunikaty za pośrednictwem Centrum IoT, samej siebie Centrum IoT zamiast tego działa jako dyspozytora skojarzone konto magazynu Azure.</span><span class="sxs-lookup"><span data-stu-id="48a48-106">Instead of brokering messages through IoT Hub itself, IoT Hub instead acts as a dispatcher to an associated Azure Storage account.</span></span> <span data-ttu-id="48a48-107">Urządzenie żądania tokenu magazynu z Centrum IoT, która jest specyficzna dla pliku, który chce przekazać urządzenia.</span><span class="sxs-lookup"><span data-stu-id="48a48-107">A device requests a storage token from IoT Hub that is specific to the file the device wishes to upload.</span></span> <span data-ttu-id="48a48-108">Urządzenie korzysta z identyfikatora URI połączenia SAS można przekazać pliku do magazynu, a po zakończeniu przekazywania urządzenie wysyła powiadomienie z informacją o zakończeniu z Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="48a48-108">The device uses the SAS URI to upload the file to storage, and when the upload is complete the device sends a notification of completion to IoT Hub.</span></span> <span data-ttu-id="48a48-109">Centrum IoT sprawdza przekazywanie pliku zostało ukończone, a następnie dodaje komunikatu powiadomienia przekazywania pliku do punktu końcowego powiadomienia pliku połączonej usługi.</span><span class="sxs-lookup"><span data-stu-id="48a48-109">IoT Hub checks the file upload is complete and then adds a file upload notification message to the service-facing file notification endpoint.</span></span>

<span data-ttu-id="48a48-110">Przed przekazaniem pliku do Centrum IoT z urządzenia, należy skonfigurować Centrum przez [kojarzenie magazynu Azure] [ lnk-associate-storage] konta do niego.</span><span class="sxs-lookup"><span data-stu-id="48a48-110">Before you upload a file to IoT Hub from a device, you must configure your hub by [associating an Azure Storage][lnk-associate-storage] account to it.</span></span>

<span data-ttu-id="48a48-111">Urządzenia można następnie [zainicjować przekazanie] [ lnk-initialize] , a następnie [powiadomienia Centrum IoT] [ lnk-notify] po zakończeniu przekazywania.</span><span class="sxs-lookup"><span data-stu-id="48a48-111">Your device can then [initialize an upload][lnk-initialize] and then [notify IoT hub][lnk-notify] when the upload completes.</span></span> <span data-ttu-id="48a48-112">Opcjonalnie, gdy urządzenie Centrum IoT powiadamia o zakończeniu przekazywania, usługa może wygenerować [komunikatu powiadomienia][lnk-service-notification].</span><span class="sxs-lookup"><span data-stu-id="48a48-112">Optionally, when a device notifies IoT Hub that the upload is complete, the service can generate a [notification message][lnk-service-notification].</span></span>

### <a name="when-to-use"></a><span data-ttu-id="48a48-113">Kiedy stosować</span><span class="sxs-lookup"><span data-stu-id="48a48-113">When to use</span></span>

<span data-ttu-id="48a48-114">Przekazywanie pliku używany do wysyłania plików multimedialnych i partie dużych telemetrii przekazany przez sporadycznie połączonych urządzeń lub skompresowane, aby oszczędzić przepustowość.</span><span class="sxs-lookup"><span data-stu-id="48a48-114">Use file upload to send media files and large telemetry batches uploaded by intermittently connected devices or compressed to save bandwidth.</span></span>

<span data-ttu-id="48a48-115">Zapoznaj się [wskazówki komunikację urządzenia do chmury] [ lnk-d2c-guidance] if wątpliwe między przy użyciu właściwości zgłoszone, wiadomości urządzenia do chmury lub przekazywania pliku.</span><span class="sxs-lookup"><span data-stu-id="48a48-115">Refer to [Device-to-cloud communication guidance][lnk-d2c-guidance] if in doubt between using reported properties, device-to-cloud messages, or file upload.</span></span>

## <a name="associate-an-azure-storage-account-with-iot-hub"></a><span data-ttu-id="48a48-116">Skojarz konta usługi Azure Storage z Centrum IoT</span><span class="sxs-lookup"><span data-stu-id="48a48-116">Associate an Azure Storage account with IoT Hub</span></span>

<span data-ttu-id="48a48-117">Aby korzystać z funkcji przekazywania pliku, możesz połączyć konto usługi Azure Storage w Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="48a48-117">To use the file upload functionality, you must first link an Azure Storage account to the IoT Hub.</span></span> <span data-ttu-id="48a48-118">To zadanie można wykonać za pośrednictwem [portalu Azure][lnk-management-portal], lub programistycznie za pomocą [interfejsy API REST dostawcy zasobów Centrum IoT] [ lnk-resource-provider-apis].</span><span class="sxs-lookup"><span data-stu-id="48a48-118">You can complete this task either through the [Azure portal][lnk-management-portal], or programmatically through the [IoT Hub resource provider REST APIs][lnk-resource-provider-apis].</span></span> <span data-ttu-id="48a48-119">Po powiązaniu konta usługi Azure Storage z Centrum IoT usługi zwraca identyfikator URI sygnatury dostępu Współdzielonego na urządzeniu, jeśli urządzenie inicjuje żądanie przekazywania plików.</span><span class="sxs-lookup"><span data-stu-id="48a48-119">Once you have associated an Azure Storage account with your IoT Hub, the service returns a SAS URI to a device when the device initiates a file upload request.</span></span>

> [!NOTE]
> <span data-ttu-id="48a48-120">[Azure IoT SDK] [ lnk-sdks] obsługiwać automatycznie podczas pobierania identyfikatora URI połączenia SAS, przekazywania pliku i powiadamiania IoT Hub przekazywanie zostało ukończone.</span><span class="sxs-lookup"><span data-stu-id="48a48-120">The [Azure IoT SDKs][lnk-sdks] automatically handle retrieving the SAS URI, uploading the file, and notifying IoT Hub of a completed upload.</span></span>


## <a name="initialize-a-file-upload"></a><span data-ttu-id="48a48-121">Inicjowanie przekazywania pliku</span><span class="sxs-lookup"><span data-stu-id="48a48-121">Initialize a file upload</span></span>
<span data-ttu-id="48a48-122">Centrum IoT ma punkt końcowy specjalnie z myślą o urządzeniom na żądanie identyfikatora URI sygnatury dostępu Współdzielonego dla magazynu do przekazania pliku.</span><span class="sxs-lookup"><span data-stu-id="48a48-122">IoT Hub has an endpoint specifically for devices to request a SAS URI for storage to upload a file.</span></span> <span data-ttu-id="48a48-123">Aby zainicjować proces przekazywania plików, urządzenie wysyła żądanie POST do `{iot hub}.azure-devices.net/devices/{deviceId}/files` o następujących treści JSON:</span><span class="sxs-lookup"><span data-stu-id="48a48-123">To initiate the file upload process, the device sends a POST request to `{iot hub}.azure-devices.net/devices/{deviceId}/files` with the following JSON body:</span></span>

```json
{
    "blobName": "{name of the file for which a SAS URI will be generated}"
}
```

<span data-ttu-id="48a48-124">Centrum IoT zwraca następujące dane urządzenie używa można przekazać pliku:</span><span class="sxs-lookup"><span data-stu-id="48a48-124">IoT Hub returns the following data, which the device uses to upload the file:</span></span>

```json
{
    "correlationId": "somecorrelationid",
    "hostName": "contoso.azure-devices.net",
    "containerName": "testcontainer",
    "blobName": "test-device1/image.jpg",
    "sasToken": "1234asdfSAStoken"
}
```

### <a name="deprecated-initialize-a-file-upload-with-a-get"></a><span data-ttu-id="48a48-125">Przestarzałe: zainicjować pobieranie przekazywania pliku</span><span class="sxs-lookup"><span data-stu-id="48a48-125">Deprecated: initialize a file upload with a GET</span></span>

> [!NOTE]
> <span data-ttu-id="48a48-126">W tej sekcji opisano funkcje uznane za przestarzałe dla jak uzyskać identyfikator URI SAS z Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="48a48-126">This section describes deprecated functionality for how to receive a SAS URI from IoT Hub.</span></span> <span data-ttu-id="48a48-127">Użyj metody POST opisanych powyżej.</span><span class="sxs-lookup"><span data-stu-id="48a48-127">Use the POST method described previously.</span></span>

<span data-ttu-id="48a48-128">Centrum IoT ma dwa punkty końcowe REST do obsługi przekazywania pliku, go w celu uzyskania identyfikatora URI połączenia SAS dla magazynu, a drugą do powiadamiania Centrum IoT z przekazywanie zostało ukończone.</span><span class="sxs-lookup"><span data-stu-id="48a48-128">IoT Hub has two REST endpoints to support file upload, one to get the SAS URI for storage and the other to notify the IoT hub of a completed upload.</span></span> <span data-ttu-id="48a48-129">Urządzenie inicjuje procesu przekazywania pliku, wysyłając GET do Centrum IoT na `{iot hub}.azure-devices.net/devices/{deviceId}/files/{filename}`.</span><span class="sxs-lookup"><span data-stu-id="48a48-129">The device initiates the file upload process by sending a GET to the IoT hub at `{iot hub}.azure-devices.net/devices/{deviceId}/files/{filename}`.</span></span> <span data-ttu-id="48a48-130">Zwraca Centrum IoT:</span><span class="sxs-lookup"><span data-stu-id="48a48-130">The IoT hub returns:</span></span>

* <span data-ttu-id="48a48-131">Identyfikatora URI połączenia SAS określonego pliku do przekazania.</span><span class="sxs-lookup"><span data-stu-id="48a48-131">A SAS URI specific to the file to be uploaded.</span></span>
* <span data-ttu-id="48a48-132">Identyfikator korelacji ma być używany po zakończeniu przekazywania.</span><span class="sxs-lookup"><span data-stu-id="48a48-132">A correlation ID to be used once the upload is completed.</span></span>

## <a name="notify-iot-hub-of-a-completed-file-upload"></a><span data-ttu-id="48a48-133">Powiadom Centrum IoT przekazywania pliku ukończone</span><span class="sxs-lookup"><span data-stu-id="48a48-133">Notify IoT Hub of a completed file upload</span></span>

<span data-ttu-id="48a48-134">Urządzenie jest odpowiedzialny za przekazywania pliku do magazynu przy użyciu zestawów SDK magazynu Azure.</span><span class="sxs-lookup"><span data-stu-id="48a48-134">The device is responsible for uploading the file to storage using the Azure Storage SDKs.</span></span> <span data-ttu-id="48a48-135">Po zakończeniu przekazywania urządzenie wysyła żądanie POST `{iot hub}.azure-devices.net/devices/{deviceId}/files/notifications` o następujących treści JSON:</span><span class="sxs-lookup"><span data-stu-id="48a48-135">When the upload is complete, the device sends a POST request to `{iot hub}.azure-devices.net/devices/{deviceId}/files/notifications` with the following JSON body:</span></span>

```json
{
    "correlationId": "{correlation ID received from the initial request}",
    "isSuccess": bool,
    "statusCode": XXX,
    "statusDescription": "Description of status"
}
```

<span data-ttu-id="48a48-136">Wartość `isSuccess` reprezentująca wartość logiczna, czy plik został załadowany pomyślnie.</span><span class="sxs-lookup"><span data-stu-id="48a48-136">The value of `isSuccess` is a Boolean representing whether the file was uploaded successfully.</span></span> <span data-ttu-id="48a48-137">Kod stanu `statusCode` jest stan przekazywania plików do magazynu i `statusDescription` odpowiada `statusCode`.</span><span class="sxs-lookup"><span data-stu-id="48a48-137">The status code for `statusCode` is the status for the upload of the file to storage, and the `statusDescription` corresponds to the `statusCode`.</span></span>

## <a name="reference-topics"></a><span data-ttu-id="48a48-138">Tematy odwołań:</span><span class="sxs-lookup"><span data-stu-id="48a48-138">Reference topics:</span></span>

<span data-ttu-id="48a48-139">Następujące tematy dokumentacji dostarczają więcej informacji na temat przekazywania plików z urządzenia.</span><span class="sxs-lookup"><span data-stu-id="48a48-139">The following reference topics provide you with more information about uploading files from a device.</span></span>

## <a name="file-upload-notifications"></a><span data-ttu-id="48a48-140">Powiadomienia o przekazywania plików</span><span class="sxs-lookup"><span data-stu-id="48a48-140">File upload notifications</span></span>

<span data-ttu-id="48a48-141">Opcjonalnie urządzenia IoT Hub powiadamia o zakończeniu przekazywania, Centrum IoT może wygenerować komunikat, który zawiera nazwę i magazynu lokalizację pliku.</span><span class="sxs-lookup"><span data-stu-id="48a48-141">Optionally, when a device notifies IoT Hub that an upload is complete, IoT Hub can generate a notification message that contains the name and storage location of the file.</span></span>

<span data-ttu-id="48a48-142">Zgodnie z objaśnieniem w [punkty końcowe][lnk-endpoints], Centrum IoT zapewnia powiadomienia o przekazywania plików za pośrednictwem punktu końcowego usługi połączonej (**/messages/servicebound/fileuploadnotifications**) jako wiadomości.</span><span class="sxs-lookup"><span data-stu-id="48a48-142">As explained in [Endpoints][lnk-endpoints], IoT Hub delivers file upload notifications through a service-facing endpoint (**/messages/servicebound/fileuploadnotifications**) as messages.</span></span> <span data-ttu-id="48a48-143">Semantyka odbierania powiadomień przekazywania plików są takie same jak w przypadku wiadomości chmury do urządzenia i tej samej [cykl życia komunikatów][lnk-lifecycle].</span><span class="sxs-lookup"><span data-stu-id="48a48-143">The receive semantics for file upload notifications are the same as for cloud-to-device messages and have the same [message lifecycle][lnk-lifecycle].</span></span> <span data-ttu-id="48a48-144">Każdy komunikat pobierane z punktu końcowego powiadomienia przekazywania plików jest rekordem JSON z następującymi właściwościami:</span><span class="sxs-lookup"><span data-stu-id="48a48-144">Each message retrieved from the file upload notification endpoint is a JSON record with the following properties:</span></span>

| <span data-ttu-id="48a48-145">Właściwość</span><span class="sxs-lookup"><span data-stu-id="48a48-145">Property</span></span> | <span data-ttu-id="48a48-146">Opis</span><span class="sxs-lookup"><span data-stu-id="48a48-146">Description</span></span> |
| --- | --- |
| <span data-ttu-id="48a48-147">EnqueuedTimeUtc</span><span class="sxs-lookup"><span data-stu-id="48a48-147">EnqueuedTimeUtc</span></span> |<span data-ttu-id="48a48-148">Sygnatura czasowa wskazująca utworzenia powiadomienia.</span><span class="sxs-lookup"><span data-stu-id="48a48-148">Timestamp indicating when the notification was created.</span></span> |
| <span data-ttu-id="48a48-149">Identyfikator urządzenia</span><span class="sxs-lookup"><span data-stu-id="48a48-149">DeviceId</span></span> |<span data-ttu-id="48a48-150">**DeviceId** urządzenia, które przekazać plik.</span><span class="sxs-lookup"><span data-stu-id="48a48-150">**DeviceId** of the device which uploaded the file.</span></span> |
| <span data-ttu-id="48a48-151">BlobUri</span><span class="sxs-lookup"><span data-stu-id="48a48-151">BlobUri</span></span> |<span data-ttu-id="48a48-152">Identyfikator URI przekazanego pliku.</span><span class="sxs-lookup"><span data-stu-id="48a48-152">URI of the uploaded file.</span></span> |
| <span data-ttu-id="48a48-153">Element BlobName</span><span class="sxs-lookup"><span data-stu-id="48a48-153">BlobName</span></span> |<span data-ttu-id="48a48-154">Nazwa przekazanego pliku.</span><span class="sxs-lookup"><span data-stu-id="48a48-154">Name of the uploaded file.</span></span> |
| <span data-ttu-id="48a48-155">LastUpdatedTime</span><span class="sxs-lookup"><span data-stu-id="48a48-155">LastUpdatedTime</span></span> |<span data-ttu-id="48a48-156">Sygnatura czasowa wskazująca, kiedy plik ostatniej aktualizacji.</span><span class="sxs-lookup"><span data-stu-id="48a48-156">Timestamp indicating when the file was last updated.</span></span> |
| <span data-ttu-id="48a48-157">BlobSizeInBytes</span><span class="sxs-lookup"><span data-stu-id="48a48-157">BlobSizeInBytes</span></span> |<span data-ttu-id="48a48-158">Rozmiar przekazanego pliku.</span><span class="sxs-lookup"><span data-stu-id="48a48-158">Size of the uploaded file.</span></span> |

<span data-ttu-id="48a48-159">**Przykład**.</span><span class="sxs-lookup"><span data-stu-id="48a48-159">**Example**.</span></span> <span data-ttu-id="48a48-160">Ten przykład przedstawia treści pliku przekazać komunikat powiadomienia.</span><span class="sxs-lookup"><span data-stu-id="48a48-160">This example shows the body of a file upload notification message.</span></span>

```json
{
    "deviceId":"mydevice",
    "blobUri":"https://{storage account}.blob.core.windows.net/{container name}/mydevice/myfile.jpg",
    "blobName":"mydevice/myfile.jpg",
    "lastUpdatedTime":"2016-06-01T21:22:41+00:00",
    "blobSizeInBytes":1234,
    "enqueuedTimeUtc":"2016-06-01T21:22:43.7996883Z"
}
```

## <a name="file-upload-notification-configuration-options"></a><span data-ttu-id="48a48-161">Opcje konfiguracji powiadomień przekazywania pliku</span><span class="sxs-lookup"><span data-stu-id="48a48-161">File upload notification configuration options</span></span>

<span data-ttu-id="48a48-162">Każdy Centrum IoT udostępnia następujące opcje konfiguracji w pliku przekazywania powiadomień:</span><span class="sxs-lookup"><span data-stu-id="48a48-162">Each IoT hub exposes the following configuration options for file upload notifications:</span></span>

| <span data-ttu-id="48a48-163">Właściwość</span><span class="sxs-lookup"><span data-stu-id="48a48-163">Property</span></span> | <span data-ttu-id="48a48-164">Opis</span><span class="sxs-lookup"><span data-stu-id="48a48-164">Description</span></span> | <span data-ttu-id="48a48-165">Zakres i domyślne</span><span class="sxs-lookup"><span data-stu-id="48a48-165">Range and default</span></span> |
| --- | --- | --- |
| <span data-ttu-id="48a48-166">**enableFileUploadNotifications**</span><span class="sxs-lookup"><span data-stu-id="48a48-166">**enableFileUploadNotifications**</span></span> |<span data-ttu-id="48a48-167">Określa, czy powiadomienia o przekazywania plików są zapisywane w pliku punktu końcowego powiadomienia.</span><span class="sxs-lookup"><span data-stu-id="48a48-167">Controls whether file upload notifications are written to the file notifications endpoint.</span></span> |<span data-ttu-id="48a48-168">Wartość logiczna.</span><span class="sxs-lookup"><span data-stu-id="48a48-168">Bool.</span></span> <span data-ttu-id="48a48-169">Domyślnie: True.</span><span class="sxs-lookup"><span data-stu-id="48a48-169">Default: True.</span></span> |
| <span data-ttu-id="48a48-170">**fileNotifications.ttlAsIso8601**</span><span class="sxs-lookup"><span data-stu-id="48a48-170">**fileNotifications.ttlAsIso8601**</span></span> |<span data-ttu-id="48a48-171">Domyślny czas wygaśnięcia pliku wysyłania powiadomień.</span><span class="sxs-lookup"><span data-stu-id="48a48-171">Default TTL for file upload notifications.</span></span> |<span data-ttu-id="48a48-172">ISO_8601 interwał maksymalnie 48 H (minimalna 1 minuta).</span><span class="sxs-lookup"><span data-stu-id="48a48-172">ISO_8601 interval up to 48H (minimum 1 minute).</span></span> <span data-ttu-id="48a48-173">Wartość domyślna: 1 godzina.</span><span class="sxs-lookup"><span data-stu-id="48a48-173">Default: 1 hour.</span></span> |
| <span data-ttu-id="48a48-174">**fileNotifications.lockDuration**</span><span class="sxs-lookup"><span data-stu-id="48a48-174">**fileNotifications.lockDuration**</span></span> |<span data-ttu-id="48a48-175">Czas trwania blokady do kolejki powiadomień przekazywania plików.</span><span class="sxs-lookup"><span data-stu-id="48a48-175">Lock duration for the file upload notifications queue.</span></span> |<span data-ttu-id="48a48-176">5 a 300 sekund (minimalna 5 sekund).</span><span class="sxs-lookup"><span data-stu-id="48a48-176">5 to 300 seconds (minimum 5 seconds).</span></span> <span data-ttu-id="48a48-177">Domyślnie: 60 sekund.</span><span class="sxs-lookup"><span data-stu-id="48a48-177">Default: 60 seconds.</span></span> |
| <span data-ttu-id="48a48-178">**fileNotifications.maxDeliveryCount**</span><span class="sxs-lookup"><span data-stu-id="48a48-178">**fileNotifications.maxDeliveryCount**</span></span> |<span data-ttu-id="48a48-179">Liczba maksymalna dostarczania dla pliku przekazać kolejka powiadomień.</span><span class="sxs-lookup"><span data-stu-id="48a48-179">Maximum delivery count for the file upload notification queue.</span></span> |<span data-ttu-id="48a48-180">1 do 100.</span><span class="sxs-lookup"><span data-stu-id="48a48-180">1 to 100.</span></span> <span data-ttu-id="48a48-181">Domyślnie: 100.</span><span class="sxs-lookup"><span data-stu-id="48a48-181">Default: 100.</span></span> |

## <a name="additional-reference-material"></a><span data-ttu-id="48a48-182">Odwołanie dodatkowe materiały</span><span class="sxs-lookup"><span data-stu-id="48a48-182">Additional reference material</span></span>

<span data-ttu-id="48a48-183">Inne tematy referencyjne w Podręczniku dewelopera Centrum IoT obejmują:</span><span class="sxs-lookup"><span data-stu-id="48a48-183">Other reference topics in the IoT Hub developer guide include:</span></span>

* <span data-ttu-id="48a48-184">[Punkty końcowe Centrum IoT] [ lnk-endpoints] opisano różne punkty końcowe, które udostępnia każdego centrum IoT dla operacji zarządzania i środowiska wykonawczego.</span><span class="sxs-lookup"><span data-stu-id="48a48-184">[IoT Hub endpoints][lnk-endpoints] describes the various endpoints that each IoT hub exposes for run-time and management operations.</span></span>
* <span data-ttu-id="48a48-185">[Ograniczenia przepustowości i przydziały] [ lnk-quotas] opisano przydziały i ograniczenia przepustowości zachowania, które dotyczą usługi Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="48a48-185">[Throttling and quotas][lnk-quotas] describes the quotas and throttling behaviors that apply to the IoT Hub service.</span></span>
* <span data-ttu-id="48a48-186">[Zestawy Azure IoT urządzenia i usługi SDK] [ lnk-sdks] wymieniono języka różnych zestawów SDK, można użyć podczas opracowywania aplikacji usług i urządzeń, które współdziałają z Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="48a48-186">[Azure IoT device and service SDKs][lnk-sdks] lists the various language SDKs you can use when you develop both device and service apps that interact with IoT Hub.</span></span>
* <span data-ttu-id="48a48-187">[Język zapytań Centrum IoT] [ lnk-query] opisuje język kwerendy można pobrać z Centrum IoT informacji o twins urządzenia i zadania.</span><span class="sxs-lookup"><span data-stu-id="48a48-187">[IoT Hub query language][lnk-query] describes the query language you can use to retrieve information from IoT Hub about your device twins and jobs.</span></span>
* <span data-ttu-id="48a48-188">[Obsługa MQTT Centrum IoT] [ lnk-devguide-mqtt] zapewnia więcej informacji na temat Centrum IoT obsługi protokołu MQTT.</span><span class="sxs-lookup"><span data-stu-id="48a48-188">[IoT Hub MQTT support][lnk-devguide-mqtt] provides more information about IoT Hub support for the MQTT protocol.</span></span>

## <a name="next-steps"></a><span data-ttu-id="48a48-189">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="48a48-189">Next steps</span></span>

<span data-ttu-id="48a48-190">Po zapoznaniu się przekazywania plików z urządzeń przy użyciu Centrum IoT, mogą być zainteresowane w następujących tematach przewodnik dewelopera Centrum IoT:</span><span class="sxs-lookup"><span data-stu-id="48a48-190">Now you have learned how to upload files from devices using IoT Hub, you may be interested in the following IoT Hub developer guide topics:</span></span>

* <span data-ttu-id="48a48-191">[Zarządzanie tożsamościami urządzenie w Centrum IoT][lnk-devguide-identities]</span><span class="sxs-lookup"><span data-stu-id="48a48-191">[Manage device identities in IoT Hub][lnk-devguide-identities]</span></span>
* <span data-ttu-id="48a48-192">[Kontrola dostępu do Centrum IoT][lnk-devguide-security]</span><span class="sxs-lookup"><span data-stu-id="48a48-192">[Control access to IoT Hub][lnk-devguide-security]</span></span>
* <span data-ttu-id="48a48-193">[Użyj twins urządzenia, aby zsynchronizować stanu i konfiguracji][lnk-devguide-device-twins]</span><span class="sxs-lookup"><span data-stu-id="48a48-193">[Use device twins to synchronize state and configurations][lnk-devguide-device-twins]</span></span>
* <span data-ttu-id="48a48-194">[Wywoływanie metody bezpośrednio na urządzeniu][lnk-devguide-directmethods]</span><span class="sxs-lookup"><span data-stu-id="48a48-194">[Invoke a direct method on a device][lnk-devguide-directmethods]</span></span>
* <span data-ttu-id="48a48-195">[Planowanie zadań na wielu urządzeniach][lnk-devguide-jobs]</span><span class="sxs-lookup"><span data-stu-id="48a48-195">[Schedule jobs on multiple devices][lnk-devguide-jobs]</span></span>

<span data-ttu-id="48a48-196">Jeśli chcesz wypróbować niektóre pojęcia opisane w tym artykule, mogą być zainteresowane w następujących instrukcji Centrum IoT:</span><span class="sxs-lookup"><span data-stu-id="48a48-196">If you would like to try out some of the concepts described in this article, you may be interested in the following IoT Hub tutorial:</span></span>

* <span data-ttu-id="48a48-197">[Sposób przekazywania plików z urządzenia do chmury z Centrum IoT][lnk-fileupload-tutorial]</span><span class="sxs-lookup"><span data-stu-id="48a48-197">[How to upload files from devices to the cloud with IoT Hub][lnk-fileupload-tutorial]</span></span>

[lnk-resource-provider-apis]: https://docs.microsoft.com/rest/api/iothub/iothubresource
[lnk-endpoints]: iot-hub-devguide-endpoints.md
[lnk-quotas]: iot-hub-devguide-quotas-throttling.md
[lnk-sdks]: iot-hub-devguide-sdks.md
[lnk-query]: iot-hub-devguide-query-language.md
[lnk-devguide-mqtt]: iot-hub-mqtt-support.md
[lnk-management-portal]: https://portal.azure.com
[lnk-fileupload-tutorial]: iot-hub-csharp-csharp-file-upload.md
[lnk-associate-storage]: iot-hub-devguide-file-upload.md#associate-an-azure-storage-account-with-iot-hub
[lnk-initialize]: iot-hub-devguide-file-upload.md#initialize-a-file-upload
[lnk-notify]: iot-hub-devguide-file-upload.md#notify-iot-hub-of-a-completed-file-upload
[lnk-service-notification]: iot-hub-devguide-file-upload.md#file-upload-notifications
[lnk-lifecycle]: iot-hub-devguide-messages-c2d.md#the-cloud-to-device-message-lifecycle
[lnk-d2c-guidance]: iot-hub-devguide-d2c-guidance.md

[lnk-devguide-identities]: iot-hub-devguide-identity-registry.md
[lnk-devguide-security]: iot-hub-devguide-security.md
[lnk-devguide-device-twins]: iot-hub-devguide-device-twins.md
[lnk-devguide-directmethods]: iot-hub-devguide-direct-methods.md
[lnk-devguide-jobs]: iot-hub-devguide-jobs.md
