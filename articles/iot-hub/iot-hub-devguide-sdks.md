---
title: aaaUnderstand hello Azure IoT SDK | Dokumentacja firmy Microsoft
description: "Przewodnik dewelopera — informacje i linki toohello różnych Azure IoT urządzeń i usług zestawów SDK można toobuild aplikacji dla urządzeń i aplikacji zaplecza."
services: iot-hub
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.assetid: c5c9a497-bb03-4301-be2d-00edfb7d308f
ms.service: iot-hub
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/16/2017
ms.author: dobett
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: e319451ca97876666e1c011ee0e1a73d0a0f1ed1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="understand-and-use-azure-iot-sdks"></a>W zrozumieniu i użytkowaniu zestawów SDK IoT Azure

Istnieją trzy kategorie zestawu SDK do pracy z Centrum IoT:

* **Zestawy SDK urządzenia** pozwalają aplikacji toobuild, które można uruchamiać na urządzeniach IoT. Te aplikacje wysłać dane telemetryczne tooyour IoT hub i opcjonalnie odbierać komunikaty z Centrum IoT.

* **Usługa SDK** włączyć możesz toomanage Centrum IoT i opcjonalnie wysyłać wiadomości tooyour urządzenia IoT.

* **Usługa Azure IoT krawędzi** pozwala toobuild bram tooenable urządzenia nie używający jednego z protokołów hello obsługiwane lub gdy są potrzebne tooprocess wiadomości powitania krawędzi.

Zestawy SDK są udostępniane toosupport wielu języków programowania.

## <a name="azure-iot-device-sdks"></a>Urządzenia IoT Azure SDK

zestawy SDK urządzenia Microsoft Azure IoT Hello zawiera kod, który ułatwia tworzenie urządzenia i aplikacje łączące tooand są zarządzane przez usługi Azure IoT Hub.

Witaj następujące zestawy SDK urządzenia Azure IoT są dostępne toodownload z usługi GitHub:

* [Azure urządzenia IoT zestawu SDK dla języka C] [ lnk-c-device-sdk] napisane w języku C ANSI (C99) dla przenośność i zgodność wielu platform. Istnieją dwie urządzenia klienta biblioteki C, hello niskiego poziomu **iothub_client** i hello **serializator**.
* [Azure urządzenia IoT zestawu SDK dla platformy .NET][lnk-dotnet-device-sdk]
* [Azure urządzenia IoT zestawu SDK dla języka Java][lnk-java-device-sdk]
* [Azure urządzenia IoT zestawu SDK dla środowiska Node.js][lnk-node-device-sdk]
* [Azure urządzenia IoT zestawu SDK dla języka Python][lnk-python-device-sdk]

> [!NOTE]
> Zobacz pliki readme hello w repozytoriów GitHub hello informacji o używaniu języka oraz pliki binarne tooinstall menedżerów specyficzne dla platformy pakietu i zależności na komputerze deweloperskim.
> 
> 

### <a name="os-platform-and-hardware-compatibility"></a>Zgodność platformy, sprzętu i systemu operacyjnego

Aby uzyskać więcej informacji na temat zgodności zestawu SDK z określonego urządzenia, zobacz hello [Azure certyfikowane dla katalogu urządzenia IoT][lnk-certified].

## <a name="azure-iot-service-sdks"></a>Zestawy Azure IoT usługi SDK

Usługa Azure IoT Hello zestawów SDK zawiera kod toofacilitate tworzenia aplikacji, które bezpośrednią interakcję z Centrum IoT toomanage urządzenia i zabezpieczeń.

Witaj następujących zestawów SDK usługi Azure IoT są dostępne toodownload z usługi GitHub:

* [IoT usługi Azure SDK dla platformy .NET][lnk-dotnet-service-sdk]
* [IoT usługi Azure SDK dla środowiska Node.js][lnk-node-service-sdk]
* [IoT usługi Azure SDK dla języka Java][lnk-java-service-sdk]
* [IoT usługi Azure SDK dla języka Python][lnk-python-service-sdk]
* [IoT usługi Azure SDK dla języka C][lnk-c-service-sdk]

> [!NOTE]
> Zobacz pliki readme hello w repozytoriów GitHub hello informacji o używaniu języka oraz pliki binarne tooinstall menedżerów specyficzne dla platformy pakietu i zależności na komputerze deweloperskim.

## <a name="azure-iot-edge"></a>Azure IoT Edge

Azure IoT krawędzi zawiera hello infrastruktury i moduły toocreate bramy rozwiązania IoT. Można rozszerzyć krawędzi IoT toocreate bram dopasowane tooany end-to-end scenariusza.

Możesz pobrać [Azure IoT krawędzi] [ lnk-iot-edge] z usługi GitHub.

## <a name="online-api-reference-documentation"></a>Online dokumentacji interfejsu API

Witaj Poniższa lista zawiera łącza tooonline dokumentacji interfejsu API urządzenia Azure IoT, usługi i bibliotek bramy:

* [Internet rzeczy (IoT) platformy .NET][lnk-dotnet-ref]
* [Centrum IoT REST][lnk-rest-ref]
* [Azure urządzenia IoT zestawu SDK dla języka C][lnk-c-ref]
* [Azure urządzenia IoT zestawu SDK dla języka Java][lnk-java-ref]
* [IoT usługi Azure SDK dla języka Java][lnk-java-service-ref]
* [Azure urządzenia IoT zestawu SDK dla środowiska Node.js][lnk-node-ref]
* [IoT usługi Azure SDK dla środowiska Node.js][lnk-node-service-ref]
* [Krawędź IoT Azure][lnk-gateway-ref]

## <a name="next-steps"></a>Następne kroki

Inne tematy dokumentacji, w tym przewodniku deweloperów Centrum IoT obejmują:

* [Punkty końcowe Centrum IoT][lnk-devguide-endpoints]
* [Język zapytań Centrum IoT urządzenia twins, zadań i rozsyłania wiadomości][lnk-devguide-query]
* [Przydziały i ograniczenia przepustowości][lnk-devguide-quotas]
* [Obsługa MQTT Centrum IoT][lnk-devguide-mqtt]

<!-- Links and images -->

[lnk-c-device-sdk]: https://github.com/Azure/azure-iot-sdk-c
[lnk-c-service-sdk]: https://github.com/Azure/azure-iot-sdk-c/tree/master/iothub_service_client
[lnk-dotnet-device-sdk]: https://github.com/Azure/azure-iot-sdk-csharp/tree/master/device
[lnk-java-device-sdk]: https://github.com/Azure/azure-iot-sdk-java/tree/master/device
[lnk-dotnet-service-sdk]: https://github.com/Azure/azure-iot-sdk-csharp/tree/master/service
[lnk-java-service-sdk]: https://github.com/Azure/azure-iot-sdk-java/tree/master/service
[lnk-node-device-sdk]: https://github.com/Azure/azure-iot-sdk-node/tree/master/device
[lnk-node-service-sdk]: https://github.com/Azure/azure-iot-sdk-node/tree/master/service
[lnk-python-device-sdk]: https://github.com/Azure/azure-iot-sdk-python/tree/master/device
[lnk-python-service-sdk]: https://github.com/Azure/azure-iot-sdk-python/tree/master/service
[lnk-certified]: https://catalog.azureiotsuite.com/
[lnk-iot-edge]: https://github.com/Azure/iot-edge

[lnk-dotnet-ref]: https://docs.microsoft.com/dotnet/api/microsoft.azure.devices
[lnk-c-ref]: https://azure.github.io/azure-iot-sdk-c/index.html
[lnk-java-ref]: https://docs.microsoft.com/java/api/com.microsoft.azure.sdk.iot.device
[lnk-node-ref]: https://azure.github.io/azure-iot-sdk-node/
[lnk-rest-ref]: https://docs.microsoft.com/rest/api/iothub/
[lnk-java-service-ref]: https://docs.microsoft.com/java/api/com.microsoft.azure.sdk.iot.service.auth
[lnk-node-service-ref]: https://azure.github.io/azure-iot-sdk-node/
[lnk-gateway-ref]: http://azure.github.io/iot-edge/api_reference/c/html/

[lnk-devguide-endpoints]: iot-hub-devguide-endpoints.md
[lnk-devguide-quotas]: iot-hub-devguide-quotas-throttling.md
[lnk-devguide-query]: iot-hub-devguide-query-language.md
[lnk-devguide-mqtt]: iot-hub-mqtt-support.md
