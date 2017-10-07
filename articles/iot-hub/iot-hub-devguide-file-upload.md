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
# <a name="upload-files-with-iot-hub"></a>Przekazywanie plików z Centrum IoT

Jak wyjaśniono w hello [punkty końcowe Centrum IoT] [ lnk-endpoints] artykułu, urządzenie może inicjować przekazywania pliku, wysyłając powiadomienia za pośrednictwem punktu końcowego uwzględniającym urządzenia (**/devices/ {deviceId} / pliki**). Gdy urządzenia IoT Hub powiadamia o zakończeniu przekazywania, Centrum IoT wysyła komunikat z powiadomieniem przekazywania pliku za pośrednictwem hello **/messages/servicebound/filenotifications** połączonej usługi punktu końcowego.

Zamiast utrzymywanie właściwych komunikatów za pośrednictwem Centrum IoT, się, Centrum IoT zamiast tego działa jako tooan dyspozytora skojarzone konto magazynu Azure. Urządzenie żądania tokenu magazynu z Centrum IoT, która jest toohello określonego pliku hello urządzenia żąda tooupload. urządzenie Hello używa hello toostorage pliku hello tooupload identyfikatora URI połączenia SAS, a po zakończeniu przekazywania hello hello urządzenie wysyła powiadomienie z informacją o zakończeniu tooIoT Centrum. Centrum IoT sprawdza przekazywania pliku hello została zakończona, a następnie dodaje plik przekazywania powiadomień wiadomości toohello połączonej usługi pliku punktu końcowego powiadomienia.

Przed przekazaniem tooIoT pliku koncentratora, z urządzenia, należy skonfigurować Centrum przez [kojarzenie magazynu Azure] [ lnk-associate-storage] tooit konta.

Urządzenia można następnie [zainicjować przekazanie] [ lnk-initialize] , a następnie [powiadomienia Centrum IoT] [ lnk-notify] po zakończeniu przekazywania hello. Opcjonalnie, gdy urządzenia IoT Hub powiadamia o zakończeniu przekazywania tej hello, usługa hello może wygenerować [komunikatu powiadomienia][lnk-service-notification].

### <a name="when-toouse"></a>Gdy toouse

Użyj plików multimedialnych toosend przekazywania plików i partie dużych telemetrii przekazany przez sporadycznie połączonych urządzeń lub toosave skompresowany przepustowości.

Odwołuje się zbyt[wskazówki komunikację urządzenia do chmury] [ lnk-d2c-guidance] if wątpliwe między przy użyciu właściwości zgłoszone, wiadomości urządzenia do chmury lub przekazywania pliku.

## <a name="associate-an-azure-storage-account-with-iot-hub"></a>Skojarz konta usługi Azure Storage z Centrum IoT

toouse hello funkcjonalność przekazywania plików, należy najpierw połączyć toohello konta magazynu Azure IoT Hub. To zadanie można wykonać za pośrednictwem hello [portalu Azure][lnk-management-portal], lub programistycznie za pośrednictwem hello [interfejsy API REST dostawcy zasobów Centrum IoT] [ lnk-resource-provider-apis]. Po powiązaniu konta usługi Azure Storage z Centrum IoT hello usługa zwraca identyfikator URI sygnatury dostępu Współdzielonego urządzenia tooa kiedy urządzenie hello inicjuje żądanie przekazywania plików.

> [!NOTE]
> Witaj [Azure IoT SDK] [ lnk-sdks] automatycznie podczas pobierania dojścia hello identyfikatora URI połączenia SAS, przekazywanie pliku hello i powiadamianie o tym Centrum IoT z przekazywanie zostało ukończone.


## <a name="initialize-a-file-upload"></a>Inicjowanie przekazywania pliku
Centrum IoT ma punkt końcowy specjalnie z myślą o urządzeniach toorequest identyfikator URI sygnatury dostępu Współdzielonego dla magazynu tooupload pliku. tooinitiate hello procesu przekazywania pliku, hello urządzenie wysyła żądanie POST zbyt`{iot hub}.azure-devices.net/devices/{deviceId}/files` z powitania po treści JSON:

```json
{
    "blobName": "{name of hello file for which a SAS URI will be generated}"
}
```

Centrum IoT zwraca następujące dane, które urządzenie hello używa pliku hello tooupload hello:

```json
{
    "correlationId": "somecorrelationid",
    "hostName": "contoso.azure-devices.net",
    "containerName": "testcontainer",
    "blobName": "test-device1/image.jpg",
    "sasToken": "1234asdfSAStoken"
}
```

### <a name="deprecated-initialize-a-file-upload-with-a-get"></a>Przestarzałe: zainicjować pobieranie przekazywania pliku

> [!NOTE]
> W tej sekcji opisano funkcje uznane za przestarzałe, przez jaki tooreceive identyfikator URI SAS z Centrum IoT. Użyj metody POST hello opisanych powyżej.

Centrum IoT ma dwa pozostałe punkty końcowe toosupport plik przekazać jeden hello tooget identyfikatora URI połączenia SAS magazynu i hello innych Centrum IoT hello toonotify przekazywania zakończonych. Witaj urządzenie inicjuje procesu przekazywania pliku hello wysyłając Centrum IoT toohello GET, na `{iot hub}.azure-devices.net/devices/{deviceId}/files/{filename}`. Zwraca Centrum IoT Hello:

* Identyfikator URI sygnatury dostępu Współdzielonego toohello określonego pliku toobe przekazany.
* Toobe identyfikator korelacji używany po zakończeniu przekazywania hello.

## <a name="notify-iot-hub-of-a-completed-file-upload"></a>Powiadom Centrum IoT przekazywania pliku ukończone

urządzenie Hello jest odpowiedzialny za przekazywanie hello toostorage pliku przy użyciu zestawów SDK magazynu Azure hello. Po zakończeniu przekazywania hello hello urządzenie wysyła żądanie POST zbyt`{iot hub}.azure-devices.net/devices/{deviceId}/files/notifications` z powitania po treści JSON:

```json
{
    "correlationId": "{correlation ID received from hello initial request}",
    "isSuccess": bool,
    "statusCode": XXX,
    "statusDescription": "Description of status"
}
```

Witaj wartość `isSuccess` reprezentująca wartość logiczna, czy plik hello został przekazany pomyślnie. Witaj kod stanu `statusCode` hello stan przekazywania hello hello toostorage pliku, a hello `statusDescription` odpowiada toohello `statusCode`.

## <a name="reference-topics"></a>Tematy odwołań:

Witaj następujące tematy dokumentacji zapewniają więcej informacji na temat przekazywania plików z urządzenia.

## <a name="file-upload-notifications"></a>Powiadomienia o przekazywania plików

Opcjonalnie urządzenia IoT Hub powiadamia o zakończeniu przekazywania, Centrum IoT może wygenerować komunikat, który zawiera nazwę i magazynu lokalizację hello hello pliku.

Zgodnie z objaśnieniem w [punkty końcowe][lnk-endpoints], Centrum IoT zapewnia powiadomienia o przekazywania plików za pośrednictwem punktu końcowego usługi połączonej (**/messages/servicebound/fileuploadnotifications**) jako wiadomości. Hello odbierania semantyki powiadomienia o przekazywania plików są hello takie same jak w przypadku wiadomości chmury do urządzenia oraz mieć takie same hello [cykl życia komunikatów][lnk-lifecycle]. Każdy komunikat pobierane z przekazywania hello pliku punkt końcowy jest rekordem JSON z hello następujące właściwości:

| Właściwość | Opis |
| --- | --- |
| EnqueuedTimeUtc |Sygnatura czasowa wskazująca utworzenia hello powiadomień. |
| Identyfikator urządzenia |**DeviceId** hello urządzeń, które przekazany plik hello. |
| BlobUri |Identyfikator URI hello przekazać plik. |
| Element BlobName |Nazwa hello przekazać plik. |
| LastUpdatedTime |Sygnatura czasowa wskazująca, kiedy ostatniej aktualizacji pliku hello. |
| BlobSizeInBytes |Rozmiar hello przekazać plik. |

**Przykład**. Ten przykład przedstawia hello treści pliku przekazać komunikat powiadomienia.

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

## <a name="file-upload-notification-configuration-options"></a>Opcje konfiguracji powiadomień przekazywania pliku

Każdego centrum IoT udostępnia następujące opcje konfiguracji dla powiadomień przekazywania pliku hello:

| Właściwość | Opis | Zakres i domyślne |
| --- | --- | --- |
| **enableFileUploadNotifications** |Określa, czy powiadomienia o przekazywania plików są zapisywane punkt końcowy powiadomienia plików toohello. |Wartość logiczna. Domyślnie: True. |
| **fileNotifications.ttlAsIso8601** |Domyślny czas wygaśnięcia pliku wysyłania powiadomień. |Interwał ISO_8601 się too48H (minimalna 1 minuta). Wartość domyślna: 1 godzina. |
| **fileNotifications.lockDuration** |Czas trwania blokady do kolejki powiadomień przekazywania plików hello. |5 sekund too300 (minimalna 5 sekund). Domyślnie: 60 sekund. |
| **fileNotifications.maxDeliveryCount** |Liczba maksymalna dostarczania dla pliku hello przekazać kolejka powiadomień. |1 too100. Domyślnie: 100. |

## <a name="additional-reference-material"></a>Odwołanie dodatkowe materiały

Inne tematy referencyjne w hello Centrum IoT — przewodnik dewelopera obejmują:

* [Punkty końcowe Centrum IoT] [ lnk-endpoints] opisuje hello różnych punktów końcowych, które udostępnia każdego centrum IoT dla operacji zarządzania i środowiska wykonawczego.
* [Ograniczenia przepustowości i przydziały] [ lnk-quotas] opisuje przydziały hello i ograniczanie zachowań stosowane toohello usługi IoT Hub.
* [Zestawy Azure IoT urządzenia i usługi SDK] [ lnk-sdks] list hello języka różnych zestawów SDK, można użyć podczas opracowywania aplikacji usług i urządzeń, które współdziałają z Centrum IoT.
* [Język zapytań Centrum IoT] [ lnk-query] opisuje tooretrieve informacji z Centrum IoT temat zadań i twins urządzenia można używać języka kwerend hello.
* [Obsługa MQTT Centrum IoT] [ lnk-devguide-mqtt] zamieszczono więcej informacji o obsłudze Centrum IoT hello MQTT protokołu.

## <a name="next-steps"></a>Następne kroki

Teraz wiesz już, jak tooupload pliki z urządzeń przy użyciu Centrum IoT, może Cię zainteresować następujące tematy przewodnik dewelopera Centrum IoT hello:

* [Zarządzanie tożsamościami urządzenie w Centrum IoT][lnk-devguide-identities]
* [Kontrola dostępu tooIoT Centrum][lnk-devguide-security]
* [Urządzenie twins toosynchronize stanu i konfiguracji][lnk-devguide-device-twins]
* [Wywoływanie metody bezpośrednio na urządzeniu][lnk-devguide-directmethods]
* [Planowanie zadań na wielu urządzeniach][lnk-devguide-jobs]

Jeśli chcesz tootry niektórych hello pojęcia opisane w tym artykule, mogą być zainteresowane hello samouczka Centrum IoT:

* [Jak tooupload pliki z urządzeń toohello chmury z Centrum IoT][lnk-fileupload-tutorial]

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
