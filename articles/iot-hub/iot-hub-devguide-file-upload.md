---
title: Przekazywanie pliku Centrum IoT Azure aaaUnderstand | Dokumentacja firmy Microsoft
description: "Przewodnik dewelopera — funkcja przekazywania plików hello użycia z Centrum IoT toomanage przekazywania plików z kontenera obiektów blob magazynu Azure tooan urządzenia."
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
ms.openlocfilehash: d44f9303ead4fa282dc0baf70887af1b8a03293d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="upload-files-with-iot-hub"></a><span data-ttu-id="e532d-103">Przekazywanie plików z Centrum IoT</span><span class="sxs-lookup"><span data-stu-id="e532d-103">Upload files with IoT Hub</span></span>

<span data-ttu-id="e532d-104">Jak wyjaśniono w hello [punkty końcowe Centrum IoT] [ lnk-endpoints] artykułu, urządzenie może inicjować przekazywania pliku, wysyłając powiadomienia za pośrednictwem punktu końcowego uwzględniającym urządzenia (**/devices/ {deviceId} / pliki**).</span><span class="sxs-lookup"><span data-stu-id="e532d-104">As detailed in hello [IoT Hub endpoints][lnk-endpoints] article, a device can initiate a file upload by sending a notification through a device-facing endpoint (**/devices/{deviceId}/files**).</span></span> <span data-ttu-id="e532d-105">Gdy urządzenia IoT Hub powiadamia o zakończeniu przekazywania, Centrum IoT wysyła komunikat z powiadomieniem przekazywania pliku za pośrednictwem hello **/messages/servicebound/filenotifications** połączonej usługi punktu końcowego.</span><span class="sxs-lookup"><span data-stu-id="e532d-105">When a device notifies IoT Hub that an upload is complete, IoT Hub sends a file upload notification message through hello **/messages/servicebound/filenotifications** service-facing endpoint.</span></span>

<span data-ttu-id="e532d-106">Zamiast utrzymywanie właściwych komunikatów za pośrednictwem Centrum IoT, się, Centrum IoT zamiast tego działa jako tooan dyspozytora skojarzone konto magazynu Azure.</span><span class="sxs-lookup"><span data-stu-id="e532d-106">Instead of brokering messages through IoT Hub itself, IoT Hub instead acts as a dispatcher tooan associated Azure Storage account.</span></span> <span data-ttu-id="e532d-107">Urządzenie żądania tokenu magazynu z Centrum IoT, która jest toohello określonego pliku hello urządzenia żąda tooupload.</span><span class="sxs-lookup"><span data-stu-id="e532d-107">A device requests a storage token from IoT Hub that is specific toohello file hello device wishes tooupload.</span></span> <span data-ttu-id="e532d-108">urządzenie Hello używa hello toostorage pliku hello tooupload identyfikatora URI połączenia SAS, a po zakończeniu przekazywania hello hello urządzenie wysyła powiadomienie z informacją o zakończeniu tooIoT Centrum.</span><span class="sxs-lookup"><span data-stu-id="e532d-108">hello device uses hello SAS URI tooupload hello file toostorage, and when hello upload is complete hello device sends a notification of completion tooIoT Hub.</span></span> <span data-ttu-id="e532d-109">Centrum IoT sprawdza przekazywania pliku hello została zakończona, a następnie dodaje plik przekazywania powiadomień wiadomości toohello połączonej usługi pliku punktu końcowego powiadomienia.</span><span class="sxs-lookup"><span data-stu-id="e532d-109">IoT Hub checks hello file upload is complete and then adds a file upload notification message toohello service-facing file notification endpoint.</span></span>

<span data-ttu-id="e532d-110">Przed przekazaniem tooIoT pliku koncentratora, z urządzenia, należy skonfigurować Centrum przez [kojarzenie magazynu Azure] [ lnk-associate-storage] tooit konta.</span><span class="sxs-lookup"><span data-stu-id="e532d-110">Before you upload a file tooIoT Hub from a device, you must configure your hub by [associating an Azure Storage][lnk-associate-storage] account tooit.</span></span>

<span data-ttu-id="e532d-111">Urządzenia można następnie [zainicjować przekazanie] [ lnk-initialize] , a następnie [powiadomienia Centrum IoT] [ lnk-notify] po zakończeniu przekazywania hello.</span><span class="sxs-lookup"><span data-stu-id="e532d-111">Your device can then [initialize an upload][lnk-initialize] and then [notify IoT hub][lnk-notify] when hello upload completes.</span></span> <span data-ttu-id="e532d-112">Opcjonalnie, gdy urządzenia IoT Hub powiadamia o zakończeniu przekazywania tej hello, usługa hello może wygenerować [komunikatu powiadomienia][lnk-service-notification].</span><span class="sxs-lookup"><span data-stu-id="e532d-112">Optionally, when a device notifies IoT Hub that hello upload is complete, hello service can generate a [notification message][lnk-service-notification].</span></span>

### <a name="when-toouse"></a><span data-ttu-id="e532d-113">Gdy toouse</span><span class="sxs-lookup"><span data-stu-id="e532d-113">When toouse</span></span>

<span data-ttu-id="e532d-114">Użyj plików multimedialnych toosend przekazywania plików i partie dużych telemetrii przekazany przez sporadycznie połączonych urządzeń lub toosave skompresowany przepustowości.</span><span class="sxs-lookup"><span data-stu-id="e532d-114">Use file upload toosend media files and large telemetry batches uploaded by intermittently connected devices or compressed toosave bandwidth.</span></span>

<span data-ttu-id="e532d-115">Odwołuje się zbyt[wskazówki komunikację urządzenia do chmury] [ lnk-d2c-guidance] if wątpliwe między przy użyciu właściwości zgłoszone, wiadomości urządzenia do chmury lub przekazywania pliku.</span><span class="sxs-lookup"><span data-stu-id="e532d-115">Refer too[Device-to-cloud communication guidance][lnk-d2c-guidance] if in doubt between using reported properties, device-to-cloud messages, or file upload.</span></span>

## <a name="associate-an-azure-storage-account-with-iot-hub"></a><span data-ttu-id="e532d-116">Skojarz konta usługi Azure Storage z Centrum IoT</span><span class="sxs-lookup"><span data-stu-id="e532d-116">Associate an Azure Storage account with IoT Hub</span></span>

<span data-ttu-id="e532d-117">toouse hello funkcjonalność przekazywania plików, należy najpierw połączyć toohello konta magazynu Azure IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="e532d-117">toouse hello file upload functionality, you must first link an Azure Storage account toohello IoT Hub.</span></span> <span data-ttu-id="e532d-118">To zadanie można wykonać za pośrednictwem hello [portalu Azure][lnk-management-portal], lub programistycznie za pośrednictwem hello [interfejsy API REST dostawcy zasobów Centrum IoT] [ lnk-resource-provider-apis].</span><span class="sxs-lookup"><span data-stu-id="e532d-118">You can complete this task either through hello [Azure portal][lnk-management-portal], or programmatically through hello [IoT Hub resource provider REST APIs][lnk-resource-provider-apis].</span></span> <span data-ttu-id="e532d-119">Po powiązaniu konta usługi Azure Storage z Centrum IoT hello usługa zwraca identyfikator URI sygnatury dostępu Współdzielonego urządzenia tooa kiedy urządzenie hello inicjuje żądanie przekazywania plików.</span><span class="sxs-lookup"><span data-stu-id="e532d-119">Once you have associated an Azure Storage account with your IoT Hub, hello service returns a SAS URI tooa device when hello device initiates a file upload request.</span></span>

> [!NOTE]
> <span data-ttu-id="e532d-120">Witaj [Azure IoT SDK] [ lnk-sdks] automatycznie podczas pobierania dojścia hello identyfikatora URI połączenia SAS, przekazywanie pliku hello i powiadamianie o tym Centrum IoT z przekazywanie zostało ukończone.</span><span class="sxs-lookup"><span data-stu-id="e532d-120">hello [Azure IoT SDKs][lnk-sdks] automatically handle retrieving hello SAS URI, uploading hello file, and notifying IoT Hub of a completed upload.</span></span>


## <a name="initialize-a-file-upload"></a><span data-ttu-id="e532d-121">Inicjowanie przekazywania pliku</span><span class="sxs-lookup"><span data-stu-id="e532d-121">Initialize a file upload</span></span>
<span data-ttu-id="e532d-122">Centrum IoT ma punkt końcowy specjalnie z myślą o urządzeniach toorequest identyfikator URI sygnatury dostępu Współdzielonego dla magazynu tooupload pliku.</span><span class="sxs-lookup"><span data-stu-id="e532d-122">IoT Hub has an endpoint specifically for devices toorequest a SAS URI for storage tooupload a file.</span></span> <span data-ttu-id="e532d-123">tooinitiate hello procesu przekazywania pliku, hello urządzenie wysyła żądanie POST zbyt`{iot hub}.azure-devices.net/devices/{deviceId}/files` z powitania po treści JSON:</span><span class="sxs-lookup"><span data-stu-id="e532d-123">tooinitiate hello file upload process, hello device sends a POST request too`{iot hub}.azure-devices.net/devices/{deviceId}/files` with hello following JSON body:</span></span>

```json
{
    "blobName": "{name of hello file for which a SAS URI will be generated}"
}
```

<span data-ttu-id="e532d-124">Centrum IoT zwraca następujące dane, które urządzenie hello używa pliku hello tooupload hello:</span><span class="sxs-lookup"><span data-stu-id="e532d-124">IoT Hub returns hello following data, which hello device uses tooupload hello file:</span></span>

```json
{
    "correlationId": "somecorrelationid",
    "hostName": "contoso.azure-devices.net",
    "containerName": "testcontainer",
    "blobName": "test-device1/image.jpg",
    "sasToken": "1234asdfSAStoken"
}
```

### <a name="deprecated-initialize-a-file-upload-with-a-get"></a><span data-ttu-id="e532d-125">Przestarzałe: zainicjować pobieranie przekazywania pliku</span><span class="sxs-lookup"><span data-stu-id="e532d-125">Deprecated: initialize a file upload with a GET</span></span>

> [!NOTE]
> <span data-ttu-id="e532d-126">W tej sekcji opisano funkcje uznane za przestarzałe, przez jaki tooreceive identyfikator URI SAS z Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="e532d-126">This section describes deprecated functionality for how tooreceive a SAS URI from IoT Hub.</span></span> <span data-ttu-id="e532d-127">Użyj metody POST hello opisanych powyżej.</span><span class="sxs-lookup"><span data-stu-id="e532d-127">Use hello POST method described previously.</span></span>

<span data-ttu-id="e532d-128">Centrum IoT ma dwa pozostałe punkty końcowe toosupport plik przekazać jeden hello tooget identyfikatora URI połączenia SAS magazynu i hello innych Centrum IoT hello toonotify przekazywania zakończonych.</span><span class="sxs-lookup"><span data-stu-id="e532d-128">IoT Hub has two REST endpoints toosupport file upload, one tooget hello SAS URI for storage and hello other toonotify hello IoT hub of a completed upload.</span></span> <span data-ttu-id="e532d-129">Witaj urządzenie inicjuje procesu przekazywania pliku hello wysyłając Centrum IoT toohello GET, na `{iot hub}.azure-devices.net/devices/{deviceId}/files/{filename}`.</span><span class="sxs-lookup"><span data-stu-id="e532d-129">hello device initiates hello file upload process by sending a GET toohello IoT hub at `{iot hub}.azure-devices.net/devices/{deviceId}/files/{filename}`.</span></span> <span data-ttu-id="e532d-130">Zwraca Centrum IoT Hello:</span><span class="sxs-lookup"><span data-stu-id="e532d-130">hello IoT hub returns:</span></span>

* <span data-ttu-id="e532d-131">Identyfikator URI sygnatury dostępu Współdzielonego toohello określonego pliku toobe przekazany.</span><span class="sxs-lookup"><span data-stu-id="e532d-131">A SAS URI specific toohello file toobe uploaded.</span></span>
* <span data-ttu-id="e532d-132">Toobe identyfikator korelacji używany po zakończeniu przekazywania hello.</span><span class="sxs-lookup"><span data-stu-id="e532d-132">A correlation ID toobe used once hello upload is completed.</span></span>

## <a name="notify-iot-hub-of-a-completed-file-upload"></a><span data-ttu-id="e532d-133">Powiadom Centrum IoT przekazywania pliku ukończone</span><span class="sxs-lookup"><span data-stu-id="e532d-133">Notify IoT Hub of a completed file upload</span></span>

<span data-ttu-id="e532d-134">urządzenie Hello jest odpowiedzialny za przekazywanie hello toostorage pliku przy użyciu zestawów SDK magazynu Azure hello.</span><span class="sxs-lookup"><span data-stu-id="e532d-134">hello device is responsible for uploading hello file toostorage using hello Azure Storage SDKs.</span></span> <span data-ttu-id="e532d-135">Po zakończeniu przekazywania hello hello urządzenie wysyła żądanie POST zbyt`{iot hub}.azure-devices.net/devices/{deviceId}/files/notifications` z powitania po treści JSON:</span><span class="sxs-lookup"><span data-stu-id="e532d-135">When hello upload is complete, hello device sends a POST request too`{iot hub}.azure-devices.net/devices/{deviceId}/files/notifications` with hello following JSON body:</span></span>

```json
{
    "correlationId": "{correlation ID received from hello initial request}",
    "isSuccess": bool,
    "statusCode": XXX,
    "statusDescription": "Description of status"
}
```

<span data-ttu-id="e532d-136">Witaj wartość `isSuccess` reprezentująca wartość logiczna, czy plik hello został przekazany pomyślnie.</span><span class="sxs-lookup"><span data-stu-id="e532d-136">hello value of `isSuccess` is a Boolean representing whether hello file was uploaded successfully.</span></span> <span data-ttu-id="e532d-137">Witaj kod stanu `statusCode` hello stan przekazywania hello hello toostorage pliku, a hello `statusDescription` odpowiada toohello `statusCode`.</span><span class="sxs-lookup"><span data-stu-id="e532d-137">hello status code for `statusCode` is hello status for hello upload of hello file toostorage, and hello `statusDescription` corresponds toohello `statusCode`.</span></span>

## <a name="reference-topics"></a><span data-ttu-id="e532d-138">Tematy odwołań:</span><span class="sxs-lookup"><span data-stu-id="e532d-138">Reference topics:</span></span>

<span data-ttu-id="e532d-139">Witaj następujące tematy dokumentacji zapewniają więcej informacji na temat przekazywania plików z urządzenia.</span><span class="sxs-lookup"><span data-stu-id="e532d-139">hello following reference topics provide you with more information about uploading files from a device.</span></span>

## <a name="file-upload-notifications"></a><span data-ttu-id="e532d-140">Powiadomienia o przekazywania plików</span><span class="sxs-lookup"><span data-stu-id="e532d-140">File upload notifications</span></span>

<span data-ttu-id="e532d-141">Opcjonalnie urządzenia IoT Hub powiadamia o zakończeniu przekazywania, Centrum IoT może wygenerować komunikat, który zawiera nazwę i magazynu lokalizację hello hello pliku.</span><span class="sxs-lookup"><span data-stu-id="e532d-141">Optionally, when a device notifies IoT Hub that an upload is complete, IoT Hub can generate a notification message that contains hello name and storage location of hello file.</span></span>

<span data-ttu-id="e532d-142">Zgodnie z objaśnieniem w [punkty końcowe][lnk-endpoints], Centrum IoT zapewnia powiadomienia o przekazywania plików za pośrednictwem punktu końcowego usługi połączonej (**/messages/servicebound/fileuploadnotifications**) jako wiadomości.</span><span class="sxs-lookup"><span data-stu-id="e532d-142">As explained in [Endpoints][lnk-endpoints], IoT Hub delivers file upload notifications through a service-facing endpoint (**/messages/servicebound/fileuploadnotifications**) as messages.</span></span> <span data-ttu-id="e532d-143">Hello odbierania semantyki powiadomienia o przekazywania plików są hello takie same jak w przypadku wiadomości chmury do urządzenia oraz mieć takie same hello [cykl życia komunikatów][lnk-lifecycle].</span><span class="sxs-lookup"><span data-stu-id="e532d-143">hello receive semantics for file upload notifications are hello same as for cloud-to-device messages and have hello same [message lifecycle][lnk-lifecycle].</span></span> <span data-ttu-id="e532d-144">Każdy komunikat pobierane z przekazywania hello pliku punkt końcowy jest rekordem JSON z hello następujące właściwości:</span><span class="sxs-lookup"><span data-stu-id="e532d-144">Each message retrieved from hello file upload notification endpoint is a JSON record with hello following properties:</span></span>

| <span data-ttu-id="e532d-145">Właściwość</span><span class="sxs-lookup"><span data-stu-id="e532d-145">Property</span></span> | <span data-ttu-id="e532d-146">Opis</span><span class="sxs-lookup"><span data-stu-id="e532d-146">Description</span></span> |
| --- | --- |
| <span data-ttu-id="e532d-147">EnqueuedTimeUtc</span><span class="sxs-lookup"><span data-stu-id="e532d-147">EnqueuedTimeUtc</span></span> |<span data-ttu-id="e532d-148">Sygnatura czasowa wskazująca utworzenia hello powiadomień.</span><span class="sxs-lookup"><span data-stu-id="e532d-148">Timestamp indicating when hello notification was created.</span></span> |
| <span data-ttu-id="e532d-149">Identyfikator urządzenia</span><span class="sxs-lookup"><span data-stu-id="e532d-149">DeviceId</span></span> |<span data-ttu-id="e532d-150">**DeviceId** hello urządzeń, które przekazany plik hello.</span><span class="sxs-lookup"><span data-stu-id="e532d-150">**DeviceId** of hello device which uploaded hello file.</span></span> |
| <span data-ttu-id="e532d-151">BlobUri</span><span class="sxs-lookup"><span data-stu-id="e532d-151">BlobUri</span></span> |<span data-ttu-id="e532d-152">Identyfikator URI hello przekazać plik.</span><span class="sxs-lookup"><span data-stu-id="e532d-152">URI of hello uploaded file.</span></span> |
| <span data-ttu-id="e532d-153">Element BlobName</span><span class="sxs-lookup"><span data-stu-id="e532d-153">BlobName</span></span> |<span data-ttu-id="e532d-154">Nazwa hello przekazać plik.</span><span class="sxs-lookup"><span data-stu-id="e532d-154">Name of hello uploaded file.</span></span> |
| <span data-ttu-id="e532d-155">LastUpdatedTime</span><span class="sxs-lookup"><span data-stu-id="e532d-155">LastUpdatedTime</span></span> |<span data-ttu-id="e532d-156">Sygnatura czasowa wskazująca, kiedy ostatniej aktualizacji pliku hello.</span><span class="sxs-lookup"><span data-stu-id="e532d-156">Timestamp indicating when hello file was last updated.</span></span> |
| <span data-ttu-id="e532d-157">BlobSizeInBytes</span><span class="sxs-lookup"><span data-stu-id="e532d-157">BlobSizeInBytes</span></span> |<span data-ttu-id="e532d-158">Rozmiar hello przekazać plik.</span><span class="sxs-lookup"><span data-stu-id="e532d-158">Size of hello uploaded file.</span></span> |

<span data-ttu-id="e532d-159">**Przykład**.</span><span class="sxs-lookup"><span data-stu-id="e532d-159">**Example**.</span></span> <span data-ttu-id="e532d-160">Ten przykład przedstawia hello treści pliku przekazać komunikat powiadomienia.</span><span class="sxs-lookup"><span data-stu-id="e532d-160">This example shows hello body of a file upload notification message.</span></span>

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

## <a name="file-upload-notification-configuration-options"></a><span data-ttu-id="e532d-161">Opcje konfiguracji powiadomień przekazywania pliku</span><span class="sxs-lookup"><span data-stu-id="e532d-161">File upload notification configuration options</span></span>

<span data-ttu-id="e532d-162">Każdego centrum IoT udostępnia następujące opcje konfiguracji dla powiadomień przekazywania pliku hello:</span><span class="sxs-lookup"><span data-stu-id="e532d-162">Each IoT hub exposes hello following configuration options for file upload notifications:</span></span>

| <span data-ttu-id="e532d-163">Właściwość</span><span class="sxs-lookup"><span data-stu-id="e532d-163">Property</span></span> | <span data-ttu-id="e532d-164">Opis</span><span class="sxs-lookup"><span data-stu-id="e532d-164">Description</span></span> | <span data-ttu-id="e532d-165">Zakres i domyślne</span><span class="sxs-lookup"><span data-stu-id="e532d-165">Range and default</span></span> |
| --- | --- | --- |
| <span data-ttu-id="e532d-166">**enableFileUploadNotifications**</span><span class="sxs-lookup"><span data-stu-id="e532d-166">**enableFileUploadNotifications**</span></span> |<span data-ttu-id="e532d-167">Określa, czy powiadomienia o przekazywania plików są zapisywane punkt końcowy powiadomienia plików toohello.</span><span class="sxs-lookup"><span data-stu-id="e532d-167">Controls whether file upload notifications are written toohello file notifications endpoint.</span></span> |<span data-ttu-id="e532d-168">Wartość logiczna.</span><span class="sxs-lookup"><span data-stu-id="e532d-168">Bool.</span></span> <span data-ttu-id="e532d-169">Domyślnie: True.</span><span class="sxs-lookup"><span data-stu-id="e532d-169">Default: True.</span></span> |
| <span data-ttu-id="e532d-170">**fileNotifications.ttlAsIso8601**</span><span class="sxs-lookup"><span data-stu-id="e532d-170">**fileNotifications.ttlAsIso8601**</span></span> |<span data-ttu-id="e532d-171">Domyślny czas wygaśnięcia pliku wysyłania powiadomień.</span><span class="sxs-lookup"><span data-stu-id="e532d-171">Default TTL for file upload notifications.</span></span> |<span data-ttu-id="e532d-172">Interwał ISO_8601 się too48H (minimalna 1 minuta).</span><span class="sxs-lookup"><span data-stu-id="e532d-172">ISO_8601 interval up too48H (minimum 1 minute).</span></span> <span data-ttu-id="e532d-173">Wartość domyślna: 1 godzina.</span><span class="sxs-lookup"><span data-stu-id="e532d-173">Default: 1 hour.</span></span> |
| <span data-ttu-id="e532d-174">**fileNotifications.lockDuration**</span><span class="sxs-lookup"><span data-stu-id="e532d-174">**fileNotifications.lockDuration**</span></span> |<span data-ttu-id="e532d-175">Czas trwania blokady do kolejki powiadomień przekazywania plików hello.</span><span class="sxs-lookup"><span data-stu-id="e532d-175">Lock duration for hello file upload notifications queue.</span></span> |<span data-ttu-id="e532d-176">5 sekund too300 (minimalna 5 sekund).</span><span class="sxs-lookup"><span data-stu-id="e532d-176">5 too300 seconds (minimum 5 seconds).</span></span> <span data-ttu-id="e532d-177">Domyślnie: 60 sekund.</span><span class="sxs-lookup"><span data-stu-id="e532d-177">Default: 60 seconds.</span></span> |
| <span data-ttu-id="e532d-178">**fileNotifications.maxDeliveryCount**</span><span class="sxs-lookup"><span data-stu-id="e532d-178">**fileNotifications.maxDeliveryCount**</span></span> |<span data-ttu-id="e532d-179">Liczba maksymalna dostarczania dla pliku hello przekazać kolejka powiadomień.</span><span class="sxs-lookup"><span data-stu-id="e532d-179">Maximum delivery count for hello file upload notification queue.</span></span> |<span data-ttu-id="e532d-180">1 too100.</span><span class="sxs-lookup"><span data-stu-id="e532d-180">1 too100.</span></span> <span data-ttu-id="e532d-181">Domyślnie: 100.</span><span class="sxs-lookup"><span data-stu-id="e532d-181">Default: 100.</span></span> |

## <a name="additional-reference-material"></a><span data-ttu-id="e532d-182">Odwołanie dodatkowe materiały</span><span class="sxs-lookup"><span data-stu-id="e532d-182">Additional reference material</span></span>

<span data-ttu-id="e532d-183">Inne tematy referencyjne w hello Centrum IoT — przewodnik dewelopera obejmują:</span><span class="sxs-lookup"><span data-stu-id="e532d-183">Other reference topics in hello IoT Hub developer guide include:</span></span>

* <span data-ttu-id="e532d-184">[Punkty końcowe Centrum IoT] [ lnk-endpoints] opisuje hello różnych punktów końcowych, które udostępnia każdego centrum IoT dla operacji zarządzania i środowiska wykonawczego.</span><span class="sxs-lookup"><span data-stu-id="e532d-184">[IoT Hub endpoints][lnk-endpoints] describes hello various endpoints that each IoT hub exposes for run-time and management operations.</span></span>
* <span data-ttu-id="e532d-185">[Ograniczenia przepustowości i przydziały] [ lnk-quotas] opisuje przydziały hello i ograniczanie zachowań stosowane toohello usługi IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="e532d-185">[Throttling and quotas][lnk-quotas] describes hello quotas and throttling behaviors that apply toohello IoT Hub service.</span></span>
* <span data-ttu-id="e532d-186">[Zestawy Azure IoT urządzenia i usługi SDK] [ lnk-sdks] list hello języka różnych zestawów SDK, można użyć podczas opracowywania aplikacji usług i urządzeń, które współdziałają z Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="e532d-186">[Azure IoT device and service SDKs][lnk-sdks] lists hello various language SDKs you can use when you develop both device and service apps that interact with IoT Hub.</span></span>
* <span data-ttu-id="e532d-187">[Język zapytań Centrum IoT] [ lnk-query] opisuje tooretrieve informacji z Centrum IoT temat zadań i twins urządzenia można używać języka kwerend hello.</span><span class="sxs-lookup"><span data-stu-id="e532d-187">[IoT Hub query language][lnk-query] describes hello query language you can use tooretrieve information from IoT Hub about your device twins and jobs.</span></span>
* <span data-ttu-id="e532d-188">[Obsługa MQTT Centrum IoT] [ lnk-devguide-mqtt] zamieszczono więcej informacji o obsłudze Centrum IoT hello MQTT protokołu.</span><span class="sxs-lookup"><span data-stu-id="e532d-188">[IoT Hub MQTT support][lnk-devguide-mqtt] provides more information about IoT Hub support for hello MQTT protocol.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e532d-189">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="e532d-189">Next steps</span></span>

<span data-ttu-id="e532d-190">Teraz wiesz już, jak tooupload pliki z urządzeń przy użyciu Centrum IoT, może Cię zainteresować następujące tematy przewodnik dewelopera Centrum IoT hello:</span><span class="sxs-lookup"><span data-stu-id="e532d-190">Now you have learned how tooupload files from devices using IoT Hub, you may be interested in hello following IoT Hub developer guide topics:</span></span>

* <span data-ttu-id="e532d-191">[Zarządzanie tożsamościami urządzenie w Centrum IoT][lnk-devguide-identities]</span><span class="sxs-lookup"><span data-stu-id="e532d-191">[Manage device identities in IoT Hub][lnk-devguide-identities]</span></span>
* <span data-ttu-id="e532d-192">[Kontrola dostępu tooIoT Centrum][lnk-devguide-security]</span><span class="sxs-lookup"><span data-stu-id="e532d-192">[Control access tooIoT Hub][lnk-devguide-security]</span></span>
* <span data-ttu-id="e532d-193">[Urządzenie twins toosynchronize stanu i konfiguracji][lnk-devguide-device-twins]</span><span class="sxs-lookup"><span data-stu-id="e532d-193">[Use device twins toosynchronize state and configurations][lnk-devguide-device-twins]</span></span>
* <span data-ttu-id="e532d-194">[Wywoływanie metody bezpośrednio na urządzeniu][lnk-devguide-directmethods]</span><span class="sxs-lookup"><span data-stu-id="e532d-194">[Invoke a direct method on a device][lnk-devguide-directmethods]</span></span>
* <span data-ttu-id="e532d-195">[Planowanie zadań na wielu urządzeniach][lnk-devguide-jobs]</span><span class="sxs-lookup"><span data-stu-id="e532d-195">[Schedule jobs on multiple devices][lnk-devguide-jobs]</span></span>

<span data-ttu-id="e532d-196">Jeśli chcesz tootry niektórych hello pojęcia opisane w tym artykule, mogą być zainteresowane hello samouczka Centrum IoT:</span><span class="sxs-lookup"><span data-stu-id="e532d-196">If you would like tootry out some of hello concepts described in this article, you may be interested in hello following IoT Hub tutorial:</span></span>

* <span data-ttu-id="e532d-197">[Jak tooupload pliki z urządzeń toohello chmury z Centrum IoT][lnk-fileupload-tutorial]</span><span class="sxs-lookup"><span data-stu-id="e532d-197">[How tooupload files from devices toohello cloud with IoT Hub][lnk-fileupload-tutorial]</span></span>

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
