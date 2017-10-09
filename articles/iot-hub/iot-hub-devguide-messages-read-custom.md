---
title: "niestandardowe punkty końcowe Centrum IoT Azure aaaUnderstand | Dokumentacja firmy Microsoft"
description: "Przewodnik dewelopera — przy użyciu routingu reguł tooroute punktów końcowych z toocustom wiadomości urządzenia do chmury."
services: iot-hub
documentationcenter: .net
author: dominicbetts
manager: timlt
editor: 
ms.service: iot-hub
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/25/2017
ms.author: dobett
ms.openlocfilehash: daa9cfb35d0853e316bbf469b034d4dadbd4e85d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="use-message-routes-and-custom-endpoints-for-device-to-cloud-messages"></a><span data-ttu-id="5aaad-103">Urządzenia do chmury wiadomości wysyłanych tras wiadomości i niestandardowe punkty końcowe</span><span class="sxs-lookup"><span data-stu-id="5aaad-103">Use message routes and custom endpoints for device-to-cloud messages</span></span>

<span data-ttu-id="5aaad-104">Centrum IoT umożliwia tooroute [wiadomości urządzenia do chmury] [ lnk-device-to-cloud] tooIoT Centrum połączonej usługi punktów końcowych na podstawie komunikatu właściwości.</span><span class="sxs-lookup"><span data-stu-id="5aaad-104">IoT Hub enables you tooroute [device-to-cloud messages][lnk-device-to-cloud] tooIoT Hub service-facing endpoints based on message properties.</span></span> <span data-ttu-id="5aaad-105">Routing zapewnia reguły hello toosend elastyczność wiadomości, których potrzebują toogo bez hello muszą wiadomości tooprocess dodatkowych usług lub toowrite dodatkowy kod.</span><span class="sxs-lookup"><span data-stu-id="5aaad-105">Routing rules give you hello flexibility toosend messages where they need toogo without hello need for additional services tooprocess messages or toowrite additional code.</span></span> <span data-ttu-id="5aaad-106">Reguł routingu, które można skonfigurować ma hello następujące właściwości:</span><span class="sxs-lookup"><span data-stu-id="5aaad-106">Each routing rule you configure has hello following properties:</span></span>

| <span data-ttu-id="5aaad-107">Właściwość</span><span class="sxs-lookup"><span data-stu-id="5aaad-107">Property</span></span>      | <span data-ttu-id="5aaad-108">Opis</span><span class="sxs-lookup"><span data-stu-id="5aaad-108">Description</span></span> |
| ------------- | ----------- |
| <span data-ttu-id="5aaad-109">**Nazwa**</span><span class="sxs-lookup"><span data-stu-id="5aaad-109">**Name**</span></span>      | <span data-ttu-id="5aaad-110">Witaj unikatową nazwę identyfikującą hello reguły.</span><span class="sxs-lookup"><span data-stu-id="5aaad-110">hello unique name that identifies hello rule.</span></span> |
| <span data-ttu-id="5aaad-111">**Źródło**</span><span class="sxs-lookup"><span data-stu-id="5aaad-111">**Source**</span></span>    | <span data-ttu-id="5aaad-112">Witaj pochodzenia danych hello strumienia toobe reagować.</span><span class="sxs-lookup"><span data-stu-id="5aaad-112">hello origin of hello data stream toobe acted upon.</span></span> <span data-ttu-id="5aaad-113">Na przykład telemetrii urządzenia.</span><span class="sxs-lookup"><span data-stu-id="5aaad-113">For example, device telemetry.</span></span> |
| <span data-ttu-id="5aaad-114">**Warunek**</span><span class="sxs-lookup"><span data-stu-id="5aaad-114">**Condition**</span></span> | <span data-ttu-id="5aaad-115">wyrażenia zapytania Hello hello reguły routingu, które jest wykonywane na nagłówki i treści wiadomości powitania i czy jest dopasowanie dla punktu końcowego hello są używane toodetermine.</span><span class="sxs-lookup"><span data-stu-id="5aaad-115">hello query expression for hello routing rule that is run against hello message's headers and body and used toodetermine whether it is a match for hello endpoint.</span></span> <span data-ttu-id="5aaad-116">Aby uzyskać więcej informacji na temat tworzenia warunku trasy, zobacz hello [odwołanie - zapytania języka twins urządzenia i zadania][lnk-devguide-query-language].</span><span class="sxs-lookup"><span data-stu-id="5aaad-116">For more information about constructing a route condition, see hello [Reference - query language for device twins and jobs][lnk-devguide-query-language].</span></span> |
| <span data-ttu-id="5aaad-117">**Punkt końcowy**</span><span class="sxs-lookup"><span data-stu-id="5aaad-117">**Endpoint**</span></span>  | <span data-ttu-id="5aaad-118">Nazwa Hello hello punktu końcowego, gdy Centrum IoT wysyła wiadomości spełniających warunek hello.</span><span class="sxs-lookup"><span data-stu-id="5aaad-118">hello name of hello endpoint where IoT Hub sends messages that match hello condition.</span></span> <span data-ttu-id="5aaad-119">Punkty końcowe powinna mieć hello tego samego regionu Centrum IoT hello, w przeciwnym razie może być wymagana dla regionu między zapisuje.</span><span class="sxs-lookup"><span data-stu-id="5aaad-119">Endpoints should be in hello same region as hello IoT hub, otherwise you may be charged for cross-region writes.</span></span> |

<span data-ttu-id="5aaad-120">Pojedynczy komunikat może odpowiadać warunek hello na wielu reguł routingu, w których przypadku Centrum IoT zapewnia endpoint toohello wiadomość hello skojarzone z każdą regułę dopasowany.</span><span class="sxs-lookup"><span data-stu-id="5aaad-120">A single message may match hello condition on multiple routing rules, in which case IoT Hub delivers hello message toohello endpoint associated with each matched rule.</span></span> <span data-ttu-id="5aaad-121">Centrum IoT automatycznie deduplicates dostarczanie komunikatów, jeśli komunikat odpowiada wielu reguł mające hello tego samego miejsca docelowego, jest ona tylko zapisywana docelowego toothat raz.</span><span class="sxs-lookup"><span data-stu-id="5aaad-121">IoT Hub also automatically deduplicates message delivery, so if a message matches multiple rules that all have hello same destination, it is only written toothat destination once.</span></span>

<span data-ttu-id="5aaad-122">Centrum IoT ma wartość domyślną [wbudowanym punktem końcowym][lnk-built-in].</span><span class="sxs-lookup"><span data-stu-id="5aaad-122">An IoT hub has a default [built-in endpoint][lnk-built-in].</span></span> <span data-ttu-id="5aaad-123">Można utworzyć tooby wiadomości tooroute niestandardowe punkty końcowe łączenie innych usług w Centrum toohello subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="5aaad-123">You can create custom endpoints tooroute messages tooby linking other services in your subscription toohello hub.</span></span> <span data-ttu-id="5aaad-124">Centrum IoT obecnie obsługuje centra zdarzeń, kolejki usługi Service Bus i tematów usługi Service Bus jako niestandardowe punkty końcowe.</span><span class="sxs-lookup"><span data-stu-id="5aaad-124">IoT Hub currently supports Event Hubs, Service Bus queues, and Service Bus topics as custom endpoints.</span></span>

> [!WARNING]
> <span data-ttu-id="5aaad-125">Usługa Service Bus kolejek i tematów z **sesji** lub **wykrywania duplikatów** włączone nie są obsługiwane jako niestandardowe punkty końcowe.</span><span class="sxs-lookup"><span data-stu-id="5aaad-125">Service Bus queues and topics with **Sessions** or **Duplicate Detection** enabled are not supported as custom endpoints.</span></span>

<span data-ttu-id="5aaad-126">Aby uzyskać więcej informacji na temat tworzenia niestandardowych punktów końcowych w Centrum IoT, zobacz [punkty końcowe Centrum IoT][lnk-devguide-endpoints].</span><span class="sxs-lookup"><span data-stu-id="5aaad-126">For more information about creating custom endpoints in IoT Hub, see [IoT Hub endpoints][lnk-devguide-endpoints].</span></span>

<span data-ttu-id="5aaad-127">Aby uzyskać więcej informacji na temat odczytu z niestandardowe punkty końcowe zobacz:</span><span class="sxs-lookup"><span data-stu-id="5aaad-127">For more information about reading from custom endpoints, see:</span></span>

* <span data-ttu-id="5aaad-128">Odczytywanie z [usługi Event Hubs][lnk-getstarted-eh].</span><span class="sxs-lookup"><span data-stu-id="5aaad-128">Reading from [Event Hubs][lnk-getstarted-eh].</span></span>
* <span data-ttu-id="5aaad-129">Odczytywanie z [kolejek usługi Service Bus][lnk-getstarted-queue].</span><span class="sxs-lookup"><span data-stu-id="5aaad-129">Reading from [Service Bus queues][lnk-getstarted-queue].</span></span>
* <span data-ttu-id="5aaad-130">Odczytywanie z [tematów usługi Service Bus][lnk-getstarted-topic].</span><span class="sxs-lookup"><span data-stu-id="5aaad-130">Reading from [Service Bus topics][lnk-getstarted-topic].</span></span>

### <a name="next-steps"></a><span data-ttu-id="5aaad-131">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="5aaad-131">Next steps</span></span>

<span data-ttu-id="5aaad-132">Aby uzyskać więcej informacji na temat punkty końcowe Centrum IoT, zobacz [punkty końcowe Centrum IoT][lnk-devguide-endpoints].</span><span class="sxs-lookup"><span data-stu-id="5aaad-132">For more information about IoT Hub endpoints, see [IoT Hub endpoints][lnk-devguide-endpoints].</span></span>

<span data-ttu-id="5aaad-133">Aby uzyskać więcej informacji o język zapytań hello używania toodefine reguły routingu, zobacz [Centrum IoT zapytania języka twins urządzenia, zadania i rozsyłania wiadomości][lnk-devguide-query-language].</span><span class="sxs-lookup"><span data-stu-id="5aaad-133">For more information about hello query language you use toodefine routing rules, see [IoT Hub query language for device twins, jobs, and message routing][lnk-devguide-query-language].</span></span>

<span data-ttu-id="5aaad-134">Witaj [Centrum IoT procesu wiadomości urządzenia do chmury, za pomocą trasy] [ lnk-d2c-tutorial] samouczek pokazuje, jak zasady routingu toouse i niestandardowe punkty końcowe.</span><span class="sxs-lookup"><span data-stu-id="5aaad-134">hello [Process IoT Hub device-to-cloud messages using routes][lnk-d2c-tutorial] tutorial shows you how toouse routing rules and custom endpoints.</span></span>

[lnk-built-in]: iot-hub-devguide-messages-read-builtin.md
[lnk-device-to-cloud]: iot-hub-devguide-messages-d2c.md
[lnk-devguide-query-language]: iot-hub-devguide-query-language.md
[lnk-devguide-endpoints]: iot-hub-devguide-endpoints.md
[lnk-d2c-tutorial]: iot-hub-csharp-csharp-process-d2c.md
[lnk-getstarted-eh]: ../event-hubs/event-hubs-csharp-ephcs-getstarted.md
[lnk-getstarted-queue]: ../service-bus-messaging/service-bus-dotnet-get-started-with-queues.md
[lnk-getstarted-topic]: ../service-bus-messaging/service-bus-dotnet-how-to-use-topics-subscriptions.md
