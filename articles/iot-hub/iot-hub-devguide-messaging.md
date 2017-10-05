---
title: Zrozumienie Centrum IoT Azure messaging | Dokumentacja firmy Microsoft
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
ms.openlocfilehash: f54398d7ac46bf178d2bb603669b399d25370736
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="device-to-cloud-and-cloud-to-device-messaging-with-iot-hub"></a><span data-ttu-id="f7c1c-104">Urządzenia do chmury i wiadomości z Centrum IoT chmury do urządzenia</span><span class="sxs-lookup"><span data-stu-id="f7c1c-104">Device-to-cloud and cloud-to-device messaging with IoT Hub</span></span>

<span data-ttu-id="f7c1c-105">Użyj Centrum IoT wiadomości do komunikowania się z urządzeniami przez:</span><span class="sxs-lookup"><span data-stu-id="f7c1c-105">Use IoT Hub messaging to communicate with your devices by:</span></span>

* <span data-ttu-id="f7c1c-106">Wysyłanie [urządzenia do chmury] [ lnk-d2c] zaplecza wiadomości z urządzeń do rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="f7c1c-106">Sending [device-to-cloud][lnk-d2c] messages from your devices to your solution back end.</span></span>
* <span data-ttu-id="f7c1c-107">Wysyłanie [chmury do urządzenia] [ lnk-c2d] wiadomości z rozwiązania zaplecza na urządzeniach.</span><span class="sxs-lookup"><span data-stu-id="f7c1c-107">Sending [cloud-to-device][lnk-c2d] messages from the solution back end to your devices.</span></span>

<span data-ttu-id="f7c1c-108">Właściwości podstawowe Centrum IoT z obsługą wiadomości są niezawodność i trwałość wiadomości.</span><span class="sxs-lookup"><span data-stu-id="f7c1c-108">Core properties of IoT Hub messaging functionality are the reliability and durability of messages.</span></span> <span data-ttu-id="f7c1c-109">Te właściwości Włącz odporności na niestabilne połączenie po stronie urządzenia i załadować wzrostów w przypadku przetwarzania po stronie chmury.</span><span class="sxs-lookup"><span data-stu-id="f7c1c-109">These properties enable resilience to intermittent connectivity on the device side, and to load spikes in event processing on the cloud side.</span></span> <span data-ttu-id="f7c1c-110">Centrum IoT implementuje *co najmniej raz* gwarantuje dostarczania dla wiadomości zarówno urządzenia do chmury, jak i chmury do urządzenia.</span><span class="sxs-lookup"><span data-stu-id="f7c1c-110">IoT Hub implements *at least once* delivery guarantees for both device-to-cloud and cloud-to-device messaging.</span></span>

<span data-ttu-id="f7c1c-111">Aby obejrzeć wprowadzenie do funkcji Centrum IoT, zobacz artykuły [Azure i Internet rzeczy] [ lnk-azure-iot] i [Omówienie usługi Azure IoT Hub][lnk-iot-hub-overview].</span><span class="sxs-lookup"><span data-stu-id="f7c1c-111">For an introduction to the capabilities of IoT Hub, see the articles [Azure and Internet of Things][lnk-azure-iot] and [Overview of the Azure IoT Hub service][lnk-iot-hub-overview].</span></span>

## <a name="when-to-use-iot-hub-messaging"></a><span data-ttu-id="f7c1c-112">Kiedy należy używać Centrum IoT obsługi wiadomości</span><span class="sxs-lookup"><span data-stu-id="f7c1c-112">When to use IoT Hub messaging</span></span>

<span data-ttu-id="f7c1c-113">Jednokierunkowe powiadomień do aplikacji urządzenia, należy użyć urządzenia do chmury wiadomości do wysyłania telemetrii serie czasu i alertów z aplikacją urządzenia i wiadomości chmury do urządzenia.</span><span class="sxs-lookup"><span data-stu-id="f7c1c-113">Use device-to-cloud messages for sending time series telemetry and alerts from your device app, and cloud-to-device messages for one-way notifications to your device app.</span></span>

* <span data-ttu-id="f7c1c-114">Zapoznaj się [wskazówki komunikację urządzenia do chmury] [ lnk-d2c-guidance] if wątpliwe między przy użyciu wiadomości urządzenia do chmury, zgłoszone właściwości lub przekazywania pliku.</span><span class="sxs-lookup"><span data-stu-id="f7c1c-114">Refer to [Device-to-cloud communication guidance][lnk-d2c-guidance] if in doubt between using device-to-cloud messages, reported properties, or file upload.</span></span>
* <span data-ttu-id="f7c1c-115">Zapoznaj się [wskazówki dotyczące komunikacji chmury do urządzenia] [ lnk-c2d-guidance] if wątpliwe między przy użyciu wiadomości chmury do urządzenia, odpowiednie właściwości lub metody bezpośredniego.</span><span class="sxs-lookup"><span data-stu-id="f7c1c-115">Refer to [Cloud-to-device communication guidance][lnk-c2d-guidance] if in doubt between using cloud-to-device messages, desired properties, or direct methods.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f7c1c-116">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="f7c1c-116">Next steps</span></span>

* <span data-ttu-id="f7c1c-117">Więcej informacji na temat Centrum IoT [urządzenia do chmury do obsługi komunikatów][lnk-d2c].</span><span class="sxs-lookup"><span data-stu-id="f7c1c-117">Learn about IoT Hub [device-to-cloud messaging][lnk-d2c].</span></span>
* <span data-ttu-id="f7c1c-118">Więcej informacji na temat Centrum IoT [wiadomości chmury do urządzenia][lnk-c2d].</span><span class="sxs-lookup"><span data-stu-id="f7c1c-118">Learn about IoT Hub [cloud-to-device messaging][lnk-c2d].</span></span>

[lnk-azure-iot]: iot-hub-what-is-azure-iot.md
[lnk-iot-hub-overview]: iot-hub-what-is-iot-hub.md
[lnk-d2c]: iot-hub-devguide-messages-d2c.md
[lnk-c2d]: iot-hub-devguide-messages-c2d.md
[lnk-c2d-guidance]: iot-hub-devguide-c2d-guidance.md
[lnk-d2c-guidance]: iot-hub-devguide-d2c-guidance.md