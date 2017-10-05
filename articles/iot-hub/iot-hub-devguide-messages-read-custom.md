---
title: "Zrozumienie niestandardowe punkty końcowe Centrum IoT Azure | Dokumentacja firmy Microsoft"
description: "Przewodnik dewelopera — korzystanie z reguł routingu do kierowania wiadomości urządzenia do chmury do niestandardowe punkty końcowe."
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
ms.openlocfilehash: a21f1c61f344f96e2e03422e41fd8c5f7f841a0c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="use-message-routes-and-custom-endpoints-for-device-to-cloud-messages"></a><span data-ttu-id="b5223-103">Urządzenia do chmury wiadomości wysyłanych tras wiadomości i niestandardowe punkty końcowe</span><span class="sxs-lookup"><span data-stu-id="b5223-103">Use message routes and custom endpoints for device-to-cloud messages</span></span>

<span data-ttu-id="b5223-104">Centrum IoT umożliwia trasy [wiadomości urządzenia do chmury] [ lnk-device-to-cloud] do punktów końcowych usługi połączonej Centrum IoT na podstawie właściwości komunikatu.</span><span class="sxs-lookup"><span data-stu-id="b5223-104">IoT Hub enables you to route [device-to-cloud messages][lnk-device-to-cloud] to IoT Hub service-facing endpoints based on message properties.</span></span> <span data-ttu-id="b5223-105">Reguły routingu zapewniają elastyczność do wysyłania wiadomości, których potrzebują przejścia bez konieczności stosowania dodatkowych usług do przetwarzania komunikatów lub napisać dodatkowy kod.</span><span class="sxs-lookup"><span data-stu-id="b5223-105">Routing rules give you the flexibility to send messages where they need to go without the need for additional services to process messages or to write additional code.</span></span> <span data-ttu-id="b5223-106">Reguł routingu, które można skonfigurować ma następujące właściwości:</span><span class="sxs-lookup"><span data-stu-id="b5223-106">Each routing rule you configure has the following properties:</span></span>

| <span data-ttu-id="b5223-107">Właściwość</span><span class="sxs-lookup"><span data-stu-id="b5223-107">Property</span></span>      | <span data-ttu-id="b5223-108">Opis</span><span class="sxs-lookup"><span data-stu-id="b5223-108">Description</span></span> |
| ------------- | ----------- |
| <span data-ttu-id="b5223-109">**Nazwa**</span><span class="sxs-lookup"><span data-stu-id="b5223-109">**Name**</span></span>      | <span data-ttu-id="b5223-110">Unikatowa nazwa identyfikuje reguły.</span><span class="sxs-lookup"><span data-stu-id="b5223-110">The unique name that identifies the rule.</span></span> |
| <span data-ttu-id="b5223-111">**Źródło**</span><span class="sxs-lookup"><span data-stu-id="b5223-111">**Source**</span></span>    | <span data-ttu-id="b5223-112">Pochodzenie strumień danych, które będą używane.</span><span class="sxs-lookup"><span data-stu-id="b5223-112">The origin of the data stream to be acted upon.</span></span> <span data-ttu-id="b5223-113">Na przykład telemetrii urządzenia.</span><span class="sxs-lookup"><span data-stu-id="b5223-113">For example, device telemetry.</span></span> |
| <span data-ttu-id="b5223-114">**Warunek**</span><span class="sxs-lookup"><span data-stu-id="b5223-114">**Condition**</span></span> | <span data-ttu-id="b5223-115">Wyrażenia zapytania dla reguły routingu, która jest uruchamiana nagłówki i treści wiadomości i używany w celu określenia, czy jest ono dopasowania dla punktu końcowego.</span><span class="sxs-lookup"><span data-stu-id="b5223-115">The query expression for the routing rule that is run against the message's headers and body and used to determine whether it is a match for the endpoint.</span></span> <span data-ttu-id="b5223-116">Aby uzyskać więcej informacji na temat tworzenia warunku trasy, zobacz [odwołanie - zapytania języka twins urządzenia i zadania][lnk-devguide-query-language].</span><span class="sxs-lookup"><span data-stu-id="b5223-116">For more information about constructing a route condition, see the [Reference - query language for device twins and jobs][lnk-devguide-query-language].</span></span> |
| <span data-ttu-id="b5223-117">**Punkt końcowy**</span><span class="sxs-lookup"><span data-stu-id="b5223-117">**Endpoint**</span></span>  | <span data-ttu-id="b5223-118">Nazwa punktu końcowego, w którym Centrum IoT wysyła komunikaty, które są zgodne z warunkiem.</span><span class="sxs-lookup"><span data-stu-id="b5223-118">The name of the endpoint where IoT Hub sends messages that match the condition.</span></span> <span data-ttu-id="b5223-119">Punkty końcowe musi należeć do tego samego regionu Centrum IoT, w przeciwnym razie może być wymagana dla regionu między zapisów.</span><span class="sxs-lookup"><span data-stu-id="b5223-119">Endpoints should be in the same region as the IoT hub, otherwise you may be charged for cross-region writes.</span></span> |

<span data-ttu-id="b5223-120">Pojedynczy komunikat może zgodne z warunkiem na wielu reguł routingu, w których przypadku Centrum IoT dostarcza wiadomość do punktu końcowego skojarzone z każdą regułę dopasowany.</span><span class="sxs-lookup"><span data-stu-id="b5223-120">A single message may match the condition on multiple routing rules, in which case IoT Hub delivers the message to the endpoint associated with each matched rule.</span></span> <span data-ttu-id="b5223-121">Centrum IoT automatycznie deduplicates dostarczanie komunikatów, jeśli komunikat odpowiada wielu reguł mające tego samego miejsca docelowego, jest ona tylko zapisywana do tego miejsca docelowego raz.</span><span class="sxs-lookup"><span data-stu-id="b5223-121">IoT Hub also automatically deduplicates message delivery, so if a message matches multiple rules that all have the same destination, it is only written to that destination once.</span></span>

<span data-ttu-id="b5223-122">Centrum IoT ma wartość domyślną [wbudowanym punktem końcowym][lnk-built-in].</span><span class="sxs-lookup"><span data-stu-id="b5223-122">An IoT hub has a default [built-in endpoint][lnk-built-in].</span></span> <span data-ttu-id="b5223-123">Można tworzyć niestandardowe punkty końcowe do wyznaczania tras wiadomościom przez połączenie innych usług w Twojej subskrypcji do koncentratora.</span><span class="sxs-lookup"><span data-stu-id="b5223-123">You can create custom endpoints to route messages to by linking other services in your subscription to the hub.</span></span> <span data-ttu-id="b5223-124">Centrum IoT obecnie obsługuje centra zdarzeń, kolejki usługi Service Bus i tematów usługi Service Bus jako niestandardowe punkty końcowe.</span><span class="sxs-lookup"><span data-stu-id="b5223-124">IoT Hub currently supports Event Hubs, Service Bus queues, and Service Bus topics as custom endpoints.</span></span>

> [!WARNING]
> <span data-ttu-id="b5223-125">Usługa Service Bus kolejek i tematów z **sesji** lub **wykrywania duplikatów** włączone nie są obsługiwane jako niestandardowe punkty końcowe.</span><span class="sxs-lookup"><span data-stu-id="b5223-125">Service Bus queues and topics with **Sessions** or **Duplicate Detection** enabled are not supported as custom endpoints.</span></span>

<span data-ttu-id="b5223-126">Aby uzyskać więcej informacji na temat tworzenia niestandardowych punktów końcowych w Centrum IoT, zobacz [punkty końcowe Centrum IoT][lnk-devguide-endpoints].</span><span class="sxs-lookup"><span data-stu-id="b5223-126">For more information about creating custom endpoints in IoT Hub, see [IoT Hub endpoints][lnk-devguide-endpoints].</span></span>

<span data-ttu-id="b5223-127">Aby uzyskać więcej informacji na temat odczytu z niestandardowe punkty końcowe zobacz:</span><span class="sxs-lookup"><span data-stu-id="b5223-127">For more information about reading from custom endpoints, see:</span></span>

* <span data-ttu-id="b5223-128">Odczytywanie z [usługi Event Hubs][lnk-getstarted-eh].</span><span class="sxs-lookup"><span data-stu-id="b5223-128">Reading from [Event Hubs][lnk-getstarted-eh].</span></span>
* <span data-ttu-id="b5223-129">Odczytywanie z [kolejek usługi Service Bus][lnk-getstarted-queue].</span><span class="sxs-lookup"><span data-stu-id="b5223-129">Reading from [Service Bus queues][lnk-getstarted-queue].</span></span>
* <span data-ttu-id="b5223-130">Odczytywanie z [tematów usługi Service Bus][lnk-getstarted-topic].</span><span class="sxs-lookup"><span data-stu-id="b5223-130">Reading from [Service Bus topics][lnk-getstarted-topic].</span></span>

### <a name="next-steps"></a><span data-ttu-id="b5223-131">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="b5223-131">Next steps</span></span>

<span data-ttu-id="b5223-132">Aby uzyskać więcej informacji na temat punkty końcowe Centrum IoT, zobacz [punkty końcowe Centrum IoT][lnk-devguide-endpoints].</span><span class="sxs-lookup"><span data-stu-id="b5223-132">For more information about IoT Hub endpoints, see [IoT Hub endpoints][lnk-devguide-endpoints].</span></span>

<span data-ttu-id="b5223-133">Aby uzyskać więcej informacji na temat języka zapytań, służy do definiowania reguł routingu, zobacz [Centrum IoT zapytania języka twins urządzenia, zadania i rozsyłania wiadomości][lnk-devguide-query-language].</span><span class="sxs-lookup"><span data-stu-id="b5223-133">For more information about the query language you use to define routing rules, see [IoT Hub query language for device twins, jobs, and message routing][lnk-devguide-query-language].</span></span>

<span data-ttu-id="b5223-134">[Centrum IoT procesu wiadomości urządzenia do chmury, za pomocą trasy] [ lnk-d2c-tutorial] samouczek pokazuje, jak używać reguł routingu oraz niestandardowe punkty końcowe.</span><span class="sxs-lookup"><span data-stu-id="b5223-134">The [Process IoT Hub device-to-cloud messages using routes][lnk-d2c-tutorial] tutorial shows you how to use routing rules and custom endpoints.</span></span>

[lnk-built-in]: iot-hub-devguide-messages-read-builtin.md
[lnk-device-to-cloud]: iot-hub-devguide-messages-d2c.md
[lnk-devguide-query-language]: iot-hub-devguide-query-language.md
[lnk-devguide-endpoints]: iot-hub-devguide-endpoints.md
[lnk-d2c-tutorial]: iot-hub-csharp-csharp-process-d2c.md
[lnk-getstarted-eh]: ../event-hubs/event-hubs-csharp-ephcs-getstarted.md
[lnk-getstarted-queue]: ../service-bus-messaging/service-bus-dotnet-get-started-with-queues.md
[lnk-getstarted-topic]: ../service-bus-messaging/service-bus-dotnet-how-to-use-topics-subscriptions.md
