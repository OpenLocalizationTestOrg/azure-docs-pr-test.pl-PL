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
# <a name="understand-and-use-azure-iot-sdks"></a><span data-ttu-id="18149-103">W zrozumieniu i użytkowaniu zestawów SDK IoT Azure</span><span class="sxs-lookup"><span data-stu-id="18149-103">Understand and use Azure IoT SDKs</span></span>

<span data-ttu-id="18149-104">Istnieją trzy kategorie zestawu SDK do pracy z Centrum IoT:</span><span class="sxs-lookup"><span data-stu-id="18149-104">There are three categories of SDK for working with IoT Hub:</span></span>

* <span data-ttu-id="18149-105">**Zestawy SDK urządzenia** pozwalają aplikacji toobuild, które można uruchamiać na urządzeniach IoT.</span><span class="sxs-lookup"><span data-stu-id="18149-105">**Device SDKs** enable you toobuild apps that run on your IoT devices.</span></span> <span data-ttu-id="18149-106">Te aplikacje wysłać dane telemetryczne tooyour IoT hub i opcjonalnie odbierać komunikaty z Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="18149-106">These apps send telemetry tooyour IoT hub, and optionally receive messages from your IoT hub.</span></span>

* <span data-ttu-id="18149-107">**Usługa SDK** włączyć możesz toomanage Centrum IoT i opcjonalnie wysyłać wiadomości tooyour urządzenia IoT.</span><span class="sxs-lookup"><span data-stu-id="18149-107">**Service SDKs** enable you toomanage your IoT hub, and optionally send messages tooyour IoT devices.</span></span>

* <span data-ttu-id="18149-108">**Usługa Azure IoT krawędzi** pozwala toobuild bram tooenable urządzenia nie używający jednego z protokołów hello obsługiwane lub gdy są potrzebne tooprocess wiadomości powitania krawędzi.</span><span class="sxs-lookup"><span data-stu-id="18149-108">**Azure IoT Edge** enables you toobuild gateways tooenable devices that don't use one of hello supported protocols, or when you need tooprocess messages on hello edge.</span></span>

<span data-ttu-id="18149-109">Zestawy SDK są udostępniane toosupport wielu języków programowania.</span><span class="sxs-lookup"><span data-stu-id="18149-109">SDKs are provided toosupport multiple programming languages.</span></span>

## <a name="azure-iot-device-sdks"></a><span data-ttu-id="18149-110">Urządzenia IoT Azure SDK</span><span class="sxs-lookup"><span data-stu-id="18149-110">Azure IoT device SDKs</span></span>

<span data-ttu-id="18149-111">zestawy SDK urządzenia Microsoft Azure IoT Hello zawiera kod, który ułatwia tworzenie urządzenia i aplikacje łączące tooand są zarządzane przez usługi Azure IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="18149-111">hello Microsoft Azure IoT device SDKs contain code that facilitates building devices and applications that connect tooand are managed by Azure IoT Hub services.</span></span>

<span data-ttu-id="18149-112">Witaj następujące zestawy SDK urządzenia Azure IoT są dostępne toodownload z usługi GitHub:</span><span class="sxs-lookup"><span data-stu-id="18149-112">hello following Azure IoT device SDKs are available toodownload from GitHub:</span></span>

* <span data-ttu-id="18149-113">[Azure urządzenia IoT zestawu SDK dla języka C] [ lnk-c-device-sdk] napisane w języku C ANSI (C99) dla przenośność i zgodność wielu platform.</span><span class="sxs-lookup"><span data-stu-id="18149-113">[Azure IoT device SDK for C][lnk-c-device-sdk] written in ANSI C (C99) for portability and broad platform compatibility.</span></span> <span data-ttu-id="18149-114">Istnieją dwie urządzenia klienta biblioteki C, hello niskiego poziomu **iothub_client** i hello **serializator**.</span><span class="sxs-lookup"><span data-stu-id="18149-114">There are two device client libraries for C, hello low-level **iothub_client** and hello **serializer**.</span></span>
* <span data-ttu-id="18149-115">[Azure urządzenia IoT zestawu SDK dla platformy .NET][lnk-dotnet-device-sdk]</span><span class="sxs-lookup"><span data-stu-id="18149-115">[Azure IoT device SDK for .NET][lnk-dotnet-device-sdk]</span></span>
* <span data-ttu-id="18149-116">[Azure urządzenia IoT zestawu SDK dla języka Java][lnk-java-device-sdk]</span><span class="sxs-lookup"><span data-stu-id="18149-116">[Azure IoT device SDK for Java][lnk-java-device-sdk]</span></span>
* <span data-ttu-id="18149-117">[Azure urządzenia IoT zestawu SDK dla środowiska Node.js][lnk-node-device-sdk]</span><span class="sxs-lookup"><span data-stu-id="18149-117">[Azure IoT device SDK for Node.js][lnk-node-device-sdk]</span></span>
* <span data-ttu-id="18149-118">[Azure urządzenia IoT zestawu SDK dla języka Python][lnk-python-device-sdk]</span><span class="sxs-lookup"><span data-stu-id="18149-118">[Azure IoT device SDK for Python][lnk-python-device-sdk]</span></span>

> [!NOTE]
> <span data-ttu-id="18149-119">Zobacz pliki readme hello w repozytoriów GitHub hello informacji o używaniu języka oraz pliki binarne tooinstall menedżerów specyficzne dla platformy pakietu i zależności na komputerze deweloperskim.</span><span class="sxs-lookup"><span data-stu-id="18149-119">See hello readme files in hello GitHub repositories for information about using language and platform-specific package managers tooinstall binaries and dependencies on your development machine.</span></span>
> 
> 

### <a name="os-platform-and-hardware-compatibility"></a><span data-ttu-id="18149-120">Zgodność platformy, sprzętu i systemu operacyjnego</span><span class="sxs-lookup"><span data-stu-id="18149-120">OS platform and hardware compatibility</span></span>

<span data-ttu-id="18149-121">Aby uzyskać więcej informacji na temat zgodności zestawu SDK z określonego urządzenia, zobacz hello [Azure certyfikowane dla katalogu urządzenia IoT][lnk-certified].</span><span class="sxs-lookup"><span data-stu-id="18149-121">For more information about SDK compatibility with specific hardware devices, see hello [Azure Certified for IoT device catalog][lnk-certified].</span></span>

## <a name="azure-iot-service-sdks"></a><span data-ttu-id="18149-122">Zestawy Azure IoT usługi SDK</span><span class="sxs-lookup"><span data-stu-id="18149-122">Azure IoT service SDKs</span></span>

<span data-ttu-id="18149-123">Usługa Azure IoT Hello zestawów SDK zawiera kod toofacilitate tworzenia aplikacji, które bezpośrednią interakcję z Centrum IoT toomanage urządzenia i zabezpieczeń.</span><span class="sxs-lookup"><span data-stu-id="18149-123">hello Azure IoT service SDKs contain code toofacilitate building applications that interact directly with IoT Hub toomanage devices and security.</span></span>

<span data-ttu-id="18149-124">Witaj następujących zestawów SDK usługi Azure IoT są dostępne toodownload z usługi GitHub:</span><span class="sxs-lookup"><span data-stu-id="18149-124">hello following Azure IoT service SDKs are available toodownload from GitHub:</span></span>

* <span data-ttu-id="18149-125">[IoT usługi Azure SDK dla platformy .NET][lnk-dotnet-service-sdk]</span><span class="sxs-lookup"><span data-stu-id="18149-125">[Azure IoT service SDK for .NET][lnk-dotnet-service-sdk]</span></span>
* <span data-ttu-id="18149-126">[IoT usługi Azure SDK dla środowiska Node.js][lnk-node-service-sdk]</span><span class="sxs-lookup"><span data-stu-id="18149-126">[Azure IoT service SDK for Node.js][lnk-node-service-sdk]</span></span>
* <span data-ttu-id="18149-127">[IoT usługi Azure SDK dla języka Java][lnk-java-service-sdk]</span><span class="sxs-lookup"><span data-stu-id="18149-127">[Azure IoT service SDK for Java][lnk-java-service-sdk]</span></span>
* <span data-ttu-id="18149-128">[IoT usługi Azure SDK dla języka Python][lnk-python-service-sdk]</span><span class="sxs-lookup"><span data-stu-id="18149-128">[Azure IoT service SDK for Python][lnk-python-service-sdk]</span></span>
* <span data-ttu-id="18149-129">[IoT usługi Azure SDK dla języka C][lnk-c-service-sdk]</span><span class="sxs-lookup"><span data-stu-id="18149-129">[Azure IoT service SDK for C][lnk-c-service-sdk]</span></span>

> [!NOTE]
> <span data-ttu-id="18149-130">Zobacz pliki readme hello w repozytoriów GitHub hello informacji o używaniu języka oraz pliki binarne tooinstall menedżerów specyficzne dla platformy pakietu i zależności na komputerze deweloperskim.</span><span class="sxs-lookup"><span data-stu-id="18149-130">See hello readme files in hello GitHub repositories for information about using language and platform-specific package managers tooinstall binaries and dependencies on your development machine.</span></span>

## <a name="azure-iot-edge"></a><span data-ttu-id="18149-131">Azure IoT Edge</span><span class="sxs-lookup"><span data-stu-id="18149-131">Azure IoT Edge</span></span>

<span data-ttu-id="18149-132">Azure IoT krawędzi zawiera hello infrastruktury i moduły toocreate bramy rozwiązania IoT.</span><span class="sxs-lookup"><span data-stu-id="18149-132">Azure IoT Edge contains hello infrastructure and modules toocreate IoT gateway solutions.</span></span> <span data-ttu-id="18149-133">Można rozszerzyć krawędzi IoT toocreate bram dopasowane tooany end-to-end scenariusza.</span><span class="sxs-lookup"><span data-stu-id="18149-133">You can extend IoT Edge toocreate gateways tailored tooany end-to-end scenario.</span></span>

<span data-ttu-id="18149-134">Możesz pobrać [Azure IoT krawędzi] [ lnk-iot-edge] z usługi GitHub.</span><span class="sxs-lookup"><span data-stu-id="18149-134">You can download [Azure IoT Edge][lnk-iot-edge] from GitHub.</span></span>

## <a name="online-api-reference-documentation"></a><span data-ttu-id="18149-135">Online dokumentacji interfejsu API</span><span class="sxs-lookup"><span data-stu-id="18149-135">Online API reference documentation</span></span>

<span data-ttu-id="18149-136">Witaj Poniższa lista zawiera łącza tooonline dokumentacji interfejsu API urządzenia Azure IoT, usługi i bibliotek bramy:</span><span class="sxs-lookup"><span data-stu-id="18149-136">hello following list contains links tooonline API reference documentation for Azure IoT device, service, and gateway libraries:</span></span>

* <span data-ttu-id="18149-137">[Internet rzeczy (IoT) platformy .NET][lnk-dotnet-ref]</span><span class="sxs-lookup"><span data-stu-id="18149-137">[Internet of Things (IoT) .NET][lnk-dotnet-ref]</span></span>
* <span data-ttu-id="18149-138">[Centrum IoT REST][lnk-rest-ref]</span><span class="sxs-lookup"><span data-stu-id="18149-138">[IoT Hub REST][lnk-rest-ref]</span></span>
* <span data-ttu-id="18149-139">[Azure urządzenia IoT zestawu SDK dla języka C][lnk-c-ref]</span><span class="sxs-lookup"><span data-stu-id="18149-139">[Azure IoT device SDK for C][lnk-c-ref]</span></span>
* <span data-ttu-id="18149-140">[Azure urządzenia IoT zestawu SDK dla języka Java][lnk-java-ref]</span><span class="sxs-lookup"><span data-stu-id="18149-140">[Azure IoT device SDK for Java][lnk-java-ref]</span></span>
* <span data-ttu-id="18149-141">[IoT usługi Azure SDK dla języka Java][lnk-java-service-ref]</span><span class="sxs-lookup"><span data-stu-id="18149-141">[Azure IoT service SDK for Java][lnk-java-service-ref]</span></span>
* <span data-ttu-id="18149-142">[Azure urządzenia IoT zestawu SDK dla środowiska Node.js][lnk-node-ref]</span><span class="sxs-lookup"><span data-stu-id="18149-142">[Azure IoT device SDK for Node.js][lnk-node-ref]</span></span>
* <span data-ttu-id="18149-143">[IoT usługi Azure SDK dla środowiska Node.js][lnk-node-service-ref]</span><span class="sxs-lookup"><span data-stu-id="18149-143">[Azure IoT service SDK for Node.js][lnk-node-service-ref]</span></span>
* <span data-ttu-id="18149-144">[Krawędź IoT Azure][lnk-gateway-ref]</span><span class="sxs-lookup"><span data-stu-id="18149-144">[Azure IoT Edge][lnk-gateway-ref]</span></span>

## <a name="next-steps"></a><span data-ttu-id="18149-145">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="18149-145">Next steps</span></span>

<span data-ttu-id="18149-146">Inne tematy dokumentacji, w tym przewodniku deweloperów Centrum IoT obejmują:</span><span class="sxs-lookup"><span data-stu-id="18149-146">Other reference topics in this IoT Hub developer guide include:</span></span>

* <span data-ttu-id="18149-147">[Punkty końcowe Centrum IoT][lnk-devguide-endpoints]</span><span class="sxs-lookup"><span data-stu-id="18149-147">[IoT Hub endpoints][lnk-devguide-endpoints]</span></span>
* <span data-ttu-id="18149-148">[Język zapytań Centrum IoT urządzenia twins, zadań i rozsyłania wiadomości][lnk-devguide-query]</span><span class="sxs-lookup"><span data-stu-id="18149-148">[IoT Hub query language for device twins, jobs, and message routing][lnk-devguide-query]</span></span>
* <span data-ttu-id="18149-149">[Przydziały i ograniczenia przepustowości][lnk-devguide-quotas]</span><span class="sxs-lookup"><span data-stu-id="18149-149">[Quotas and throttling][lnk-devguide-quotas]</span></span>
* <span data-ttu-id="18149-150">[Obsługa MQTT Centrum IoT][lnk-devguide-mqtt]</span><span class="sxs-lookup"><span data-stu-id="18149-150">[IoT Hub MQTT support][lnk-devguide-mqtt]</span></span>

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
