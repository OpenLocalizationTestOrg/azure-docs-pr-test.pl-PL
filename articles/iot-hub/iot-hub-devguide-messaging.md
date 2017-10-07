---
title: aaaUnderstand Centrum IoT Azure messaging | Dokumentacja firmy Microsoft
description: "Przewodnik dewelopera — urządzenia do chmury i wiadomości z Centrum IoT chmury do urządzenia. Zawiera informacje na temat formaty wiadomości i protokołów komunikacyjnych obsługiwanych."
services: iot-hub
documentationcenter: .net
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 3fc5f1a3-3711-4611-9897-d4db079b4250
ms.service: iot-hub
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/25/2017
ms.author: dobett
ms.openlocfilehash: a610741e23e243f392f1c042f9ab4a00d42f734f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="device-to-cloud-and-cloud-to-device-messaging-with-iot-hub"></a><span data-ttu-id="6880e-104">Urządzenia do chmury i wiadomości z Centrum IoT chmury do urządzenia</span><span class="sxs-lookup"><span data-stu-id="6880e-104">Device-to-cloud and cloud-to-device messaging with IoT Hub</span></span>

<span data-ttu-id="6880e-105">Użyj Centrum IoT messaging toocommunicate z urządzenia przez:</span><span class="sxs-lookup"><span data-stu-id="6880e-105">Use IoT Hub messaging toocommunicate with your devices by:</span></span>

* <span data-ttu-id="6880e-106">Wysyłanie [urządzenia do chmury] [ lnk-d2c] wiadomości z rozwiązania tooyour urządzeń zaplecza.</span><span class="sxs-lookup"><span data-stu-id="6880e-106">Sending [device-to-cloud][lnk-d2c] messages from your devices tooyour solution back end.</span></span>
* <span data-ttu-id="6880e-107">Wysyłanie [chmury do urządzenia] [ lnk-c2d] komunikaty z powrotem rozwiązania hello zakończenie tooyour urządzeń.</span><span class="sxs-lookup"><span data-stu-id="6880e-107">Sending [cloud-to-device][lnk-c2d] messages from hello solution back end tooyour devices.</span></span>

<span data-ttu-id="6880e-108">Właściwości podstawowe Centrum IoT z obsługą wiadomości są hello niezawodność i trwałość wiadomości.</span><span class="sxs-lookup"><span data-stu-id="6880e-108">Core properties of IoT Hub messaging functionality are hello reliability and durability of messages.</span></span> <span data-ttu-id="6880e-109">Te właściwości Włącz odporności toointermittent łączności po stronie urządzenia hello, a tooload wzrósł w przypadku przetwarzania po stronie chmury hello.</span><span class="sxs-lookup"><span data-stu-id="6880e-109">These properties enable resilience toointermittent connectivity on hello device side, and tooload spikes in event processing on hello cloud side.</span></span> <span data-ttu-id="6880e-110">Centrum IoT implementuje *co najmniej raz* gwarantuje dostarczania dla wiadomości zarówno urządzenia do chmury, jak i chmury do urządzenia.</span><span class="sxs-lookup"><span data-stu-id="6880e-110">IoT Hub implements *at least once* delivery guarantees for both device-to-cloud and cloud-to-device messaging.</span></span>

<span data-ttu-id="6880e-111">Wprowadzenie toohello możliwości Centrum IoT, zobacz artykuły hello [Azure i Internet rzeczy] [ lnk-azure-iot] i [omówienie hello usługa Azure IoT Hub] [lnk-iot-hub-overview].</span><span class="sxs-lookup"><span data-stu-id="6880e-111">For an introduction toohello capabilities of IoT Hub, see hello articles [Azure and Internet of Things][lnk-azure-iot] and [Overview of hello Azure IoT Hub service][lnk-iot-hub-overview].</span></span>

## <a name="when-toouse-iot-hub-messaging"></a><span data-ttu-id="6880e-112">Gdy toouse Centrum IoT obsługi wiadomości</span><span class="sxs-lookup"><span data-stu-id="6880e-112">When toouse IoT Hub messaging</span></span>

<span data-ttu-id="6880e-113">Użycie dla aplikacji urządzenia tooyour jednokierunkowe powiadomień wiadomości urządzenia do chmury do wysyłania telemetrii serie czasu i alertów z aplikacją urządzenia i wiadomości chmury do urządzenia.</span><span class="sxs-lookup"><span data-stu-id="6880e-113">Use device-to-cloud messages for sending time series telemetry and alerts from your device app, and cloud-to-device messages for one-way notifications tooyour device app.</span></span>

* <span data-ttu-id="6880e-114">Odwołuje się zbyt[wskazówki komunikację urządzenia do chmury] [ lnk-d2c-guidance] if wątpliwe między przy użyciu wiadomości urządzenia do chmury, zgłoszone właściwości lub przekazywania pliku.</span><span class="sxs-lookup"><span data-stu-id="6880e-114">Refer too[Device-to-cloud communication guidance][lnk-d2c-guidance] if in doubt between using device-to-cloud messages, reported properties, or file upload.</span></span>
* <span data-ttu-id="6880e-115">Odwołuje się zbyt[wskazówki dotyczące komunikacji chmury do urządzenia] [ lnk-c2d-guidance] if wątpliwe między przy użyciu wiadomości chmury do urządzenia, odpowiednie właściwości lub metody bezpośredniego.</span><span class="sxs-lookup"><span data-stu-id="6880e-115">Refer too[Cloud-to-device communication guidance][lnk-c2d-guidance] if in doubt between using cloud-to-device messages, desired properties, or direct methods.</span></span>

## <a name="next-steps"></a><span data-ttu-id="6880e-116">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="6880e-116">Next steps</span></span>

* <span data-ttu-id="6880e-117">Więcej informacji na temat Centrum IoT [urządzenia do chmury do obsługi komunikatów][lnk-d2c].</span><span class="sxs-lookup"><span data-stu-id="6880e-117">Learn about IoT Hub [device-to-cloud messaging][lnk-d2c].</span></span>
* <span data-ttu-id="6880e-118">Więcej informacji na temat Centrum IoT [wiadomości chmury do urządzenia][lnk-c2d].</span><span class="sxs-lookup"><span data-stu-id="6880e-118">Learn about IoT Hub [cloud-to-device messaging][lnk-c2d].</span></span>

[lnk-azure-iot]: iot-hub-what-is-azure-iot.md
[lnk-iot-hub-overview]: iot-hub-what-is-iot-hub.md
[lnk-d2c]: iot-hub-devguide-messages-d2c.md
[lnk-c2d]: iot-hub-devguide-messages-c2d.md
[lnk-c2d-guidance]: iot-hub-devguide-c2d-guidance.md
[lnk-d2c-guidance]: iot-hub-devguide-d2c-guidance.md