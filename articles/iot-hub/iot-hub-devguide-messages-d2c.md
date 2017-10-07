---
title: "wiadomości urządzenia do chmury Azure IoT Hub aaaUnderstand | Dokumentacja firmy Microsoft"
description: "Przewodnik dewelopera — jak toouse urządzenia do chmury wiadomości z Centrum IoT. Zawiera informacje na temat wysyłania danych zarówno dane telemetryczne, jak i z systemem innym niż telemtry i przy użyciu routingu toodeliver wiadomości."
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
ms.openlocfilehash: 07dc8a6be747365c7efbc528ab2762b0d9790758
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="send-device-to-cloud-messages-tooiot-hub"></a><span data-ttu-id="ccd8c-104">Wysyłanie wiadomości urządzenia do chmury tooIoT Centrum</span><span class="sxs-lookup"><span data-stu-id="ccd8c-104">Send device-to-cloud messages tooIoT Hub</span></span>

<span data-ttu-id="ccd8c-105">dane telemetryczne szeregów czasowych toosend i alertów z Twojego urządzenia tooyour zaplecza rozwiązania, wysyłać urządzenia do chmury z Centrum IoT tooyour urządzenia.</span><span class="sxs-lookup"><span data-stu-id="ccd8c-105">toosend time-series telemetry and alerts from your devices tooyour solution back end, send device-to-cloud messages from your device tooyour IoT hub.</span></span> <span data-ttu-id="ccd8c-106">Omówienie opcji inne urządzenia do chmury, obsługiwanych przez Centrum IoT można znaleźć [wskazówki komunikację urządzenia do chmury][lnk-d2c-guidance].</span><span class="sxs-lookup"><span data-stu-id="ccd8c-106">For a discussion of other device-to-cloud options supported by IoT Hub, see [Device-to-cloud communications guidance][lnk-d2c-guidance].</span></span>

<span data-ttu-id="ccd8c-107">Wysyłać urządzenia do chmury za pośrednictwem punktu końcowego uwzględniającym urządzenia (**/devices/ {deviceId} / wiadomości/zdarzenia**).</span><span class="sxs-lookup"><span data-stu-id="ccd8c-107">You send device-to-cloud messages through a device-facing endpoint (**/devices/{deviceId}/messages/events**).</span></span> <span data-ttu-id="ccd8c-108">Zasady routingu, a następnie kierować Twojej tooone wiadomości powitania połączonej usługi z punktów końcowych w Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="ccd8c-108">Routing rules then route your messages tooone of hello service-facing endpoints on your IoT hub.</span></span> <span data-ttu-id="ccd8c-109">Użyć reguły routingu hello nagłówki i treści wiadomości powitania od urządzenia do chmury przepływających przez toodetermine Twojego Centrum gdzie tooroute je.</span><span class="sxs-lookup"><span data-stu-id="ccd8c-109">Routing rules use hello headers and body of hello device-to-cloud messages flowing through your hub toodetermine where tooroute them.</span></span> <span data-ttu-id="ccd8c-110">Domyślnie komunikaty są routingiem toohello wbudowanym punktem końcowym usługi połączonej (**wiadomości/zdarzenia**), która jest zgodna z [usługi Event Hubs][lnk-event-hubs].</span><span class="sxs-lookup"><span data-stu-id="ccd8c-110">By default, messages are routed toohello built-in service-facing endpoint (**messages/events**), that is compatible with [Event Hubs][lnk-event-hubs].</span></span> <span data-ttu-id="ccd8c-111">W takim przypadku używane standardowe [integracji usługi Event Hubs i zestawy SDK] [ lnk-compatible-endpoint] tooreceive wiadomości urządzenia do chmury w rozwiązaniu zaplecza.</span><span class="sxs-lookup"><span data-stu-id="ccd8c-111">Therefore, you can use standard [Event Hubs integration and SDKs][lnk-compatible-endpoint] tooreceive device-to-cloud messages in your solution back end.</span></span>

<span data-ttu-id="ccd8c-112">Centrum IoT implementuje wiadomości urządzenia do chmury przy użyciu przesyłania strumieniowego wzorzec przesyłania komunikatów.</span><span class="sxs-lookup"><span data-stu-id="ccd8c-112">IoT Hub implements device-to-cloud messaging using a streaming messaging pattern.</span></span> <span data-ttu-id="ccd8c-113">Przypominają komunikaty urządzenia do chmury Centrum IoT [usługi Event Hubs] [ lnk-event-hubs] *zdarzenia* niż [usługi Service Bus] [ lnk-servicebus] *wiadomości* w tym istnieje duża liczba zdarzeń przekazywanie za pośrednictwem usługi hello, który może zostać odczytany przez wielu czytników.</span><span class="sxs-lookup"><span data-stu-id="ccd8c-113">IoT Hub's device-to-cloud messages are more like [Event Hubs][lnk-event-hubs] *events* than [Service Bus][lnk-servicebus] *messages* in that there is a high volume of events passing through hello service that can be read by multiple readers.</span></span>

<span data-ttu-id="ccd8c-114">Wiadomości z Centrum IoT urządzenia do chmury ma hello następujące cechy:</span><span class="sxs-lookup"><span data-stu-id="ccd8c-114">Device-to-cloud messaging with IoT Hub has hello following characteristics:</span></span>

* <span data-ttu-id="ccd8c-115">Urządzenia do chmury wiadomości są trwałe i zachowanych w Centrum IoT domyślne **wiadomości/zdarzenia** punktu końcowego dla się tooseven dni.</span><span class="sxs-lookup"><span data-stu-id="ccd8c-115">Device-to-cloud messages are durable and retained in an IoT hub's default **messages/events** endpoint for up tooseven days.</span></span>
* <span data-ttu-id="ccd8c-116">Komunikaty urządzenia do chmury może mieć maksymalnie 256 KB i można grupować w partiach, który wysyła toooptimize.</span><span class="sxs-lookup"><span data-stu-id="ccd8c-116">Device-to-cloud messages can be at most 256 KB, and can be grouped in batches toooptimize sends.</span></span> <span data-ttu-id="ccd8c-117">Partie może mieć maksymalnie 256 KB.</span><span class="sxs-lookup"><span data-stu-id="ccd8c-117">Batches can be at most 256 KB.</span></span>
* <span data-ttu-id="ccd8c-118">Zgodnie z objaśnieniem w hello [kontroli dostępu tooIoT Centrum] [ lnk-devguide-security] sekcji Centrum IoT umożliwia na urządzenie uwierzytelniania i kontroli dostępu.</span><span class="sxs-lookup"><span data-stu-id="ccd8c-118">As explained in hello [Control access tooIoT Hub][lnk-devguide-security] section, IoT Hub enables per-device authentication and access control.</span></span>
* <span data-ttu-id="ccd8c-119">Centrum IoT umożliwia toocreate się too10 niestandardowe punkty końcowe.</span><span class="sxs-lookup"><span data-stu-id="ccd8c-119">IoT Hub allows you toocreate up too10 custom endpoints.</span></span> <span data-ttu-id="ccd8c-120">Wiadomości są dostarczane punkty końcowe toohello oparte na trasach skonfigurowany w Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="ccd8c-120">Messages are delivered toohello endpoints based on routes configured on your IoT hub.</span></span> <span data-ttu-id="ccd8c-121">Aby uzyskać więcej informacji, zobacz [reguły routingu](#routing-rules).</span><span class="sxs-lookup"><span data-stu-id="ccd8c-121">For more information, see [Routing rules](#routing-rules).</span></span>
* <span data-ttu-id="ccd8c-122">Centrum IoT umożliwia miliony równocześnie połączonych urządzeń (zobacz [przydziały i ograniczenia przepustowości][lnk-quotas]).</span><span class="sxs-lookup"><span data-stu-id="ccd8c-122">IoT Hub enables millions of simultaneously connected devices (see [Quotas and throttling][lnk-quotas]).</span></span>
* <span data-ttu-id="ccd8c-123">Centrum IoT nie zezwala na dowolne partycjonowania.</span><span class="sxs-lookup"><span data-stu-id="ccd8c-123">IoT Hub does not allow arbitrary partitioning.</span></span> <span data-ttu-id="ccd8c-124">Urządzenia do chmury wiadomości są dzielone na podstawie ich źródłowych **deviceId**.</span><span class="sxs-lookup"><span data-stu-id="ccd8c-124">Device-to-cloud messages are partitioned based on their originating **deviceId**.</span></span>

<span data-ttu-id="ccd8c-125">Aby uzyskać więcej informacji o różnicach hello hello Centrum IoT i usługi Event Hubs, zobacz [porównania Azure IoT Hub i usługi Azure Event Hubs][lnk-comparison].</span><span class="sxs-lookup"><span data-stu-id="ccd8c-125">For more information about hello differences between hello IoT Hub and Event Hubs services, see [Comparison of Azure IoT Hub and Azure Event Hubs][lnk-comparison].</span></span>

## <a name="send-non-telemetry-traffic"></a><span data-ttu-id="ccd8c-126">Wysyłaj ruch z systemem innym niż telemetrii</span><span class="sxs-lookup"><span data-stu-id="ccd8c-126">Send non-telemetry traffic</span></span>

<span data-ttu-id="ccd8c-127">Często oprócz punktów danych tootelemetry, urządzenia wysyłają komunikaty i żądania, które wymagają obsługi w wewnętrznej hello rozwiązania i wykonywania oddzielnych.</span><span class="sxs-lookup"><span data-stu-id="ccd8c-127">Often, in addition tootelemetry data points, devices send messages and requests that require separate execution and handling in hello solution back end.</span></span> <span data-ttu-id="ccd8c-128">Na przykład alerty krytyczne musi wyzwalających określonego działania w hello zaplecza.</span><span class="sxs-lookup"><span data-stu-id="ccd8c-128">For example, critical alerts that must trigger a specific action in hello back end.</span></span> <span data-ttu-id="ccd8c-129">Możesz łatwo zapisywać [reguły routingu] [ lnk-devguide-custom] toosend tootheir przetwarzanie na podstawie nagłówek wiadomości powitania lub wartością w treści wiadomości powitania dedykowanego tych typów punktu końcowego tooan wiadomości.</span><span class="sxs-lookup"><span data-stu-id="ccd8c-129">You can easily write a [routing rule][lnk-devguide-custom] toosend these types of messages tooan endpoint dedicated tootheir processing based on either a header on hello message or a value in hello message body.</span></span>

<span data-ttu-id="ccd8c-130">Aby uzyskać więcej informacji na temat hello najlepsze sposób tooprocess tego rodzaju wiadomości, zobacz hello [samouczek: jak tooprocess Centrum IoT urządzenia do chmury wiadomości] [ lnk-d2c-tutorial] samouczka.</span><span class="sxs-lookup"><span data-stu-id="ccd8c-130">For more information about hello best way tooprocess this kind of message, see hello [Tutorial: How tooprocess IoT Hub device-to-cloud messages][lnk-d2c-tutorial] tutorial.</span></span>

## <a name="route-device-to-cloud-messages"></a><span data-ttu-id="ccd8c-131">Rozsyłanie wiadomości urządzenia do chmury</span><span class="sxs-lookup"><span data-stu-id="ccd8c-131">Route device-to-cloud messages</span></span>

<span data-ttu-id="ccd8c-132">Masz dwie opcje dla routingu wiadomości urządzenia do chmury tooyour zaplecza aplikacji:</span><span class="sxs-lookup"><span data-stu-id="ccd8c-132">You have two options for routing device-to-cloud messages tooyour back-end apps:</span></span>

* <span data-ttu-id="ccd8c-133">Użyj wbudowanego hello [punktu końcowego Centrum zdarzeń zgodnych] [ lnk-compatible-endpoint] tooenable zaplecza aplikacji tooread hello urządzenia do chmury komunikatów odebranych przez hello koncentratora.</span><span class="sxs-lookup"><span data-stu-id="ccd8c-133">Use hello built-in [Event Hub-compatible endpoint][lnk-compatible-endpoint] tooenable back-end apps tooread hello device-to-cloud messages received by hello hub.</span></span> <span data-ttu-id="ccd8c-134">toolearn o hello wbudowanym punktem końcowym zgodnego Centrum zdarzeń, zobacz [odczytywać wiadomości urządzenia do chmury z wbudowanym punktem końcowym hello][lnk-devguide-builtin].</span><span class="sxs-lookup"><span data-stu-id="ccd8c-134">toolearn about hello built-in Event Hub-compatible endpoint, see [Read device-to-cloud messages from hello built-in endpoint][lnk-devguide-builtin].</span></span>
* <span data-ttu-id="ccd8c-135">Użyj routingu reguły toosend wiadomości toocustom punktów końcowych w Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="ccd8c-135">Use routing rules toosend messages toocustom endpoints in your IoT hub.</span></span> <span data-ttu-id="ccd8c-136">Niestandardowe punkty końcowe Włącz wiadomości urządzenia do chmury tooread zaplecza aplikacji za pomocą usługi Event Hubs, kolejek usługi Service Bus lub tematów usługi Service Bus.</span><span class="sxs-lookup"><span data-stu-id="ccd8c-136">Custom endpoints enable your back-end apps tooread device-to-cloud messages using Event Hubs, Service Bus queues, or Service Bus topics.</span></span> <span data-ttu-id="ccd8c-137">Zobacz toolearn o routingu i niestandardowe punkty końcowe [Użyj niestandardowe punkty końcowe i reguły routingu dla komunikatów urządzenia do chmury][lnk-devguide-custom].</span><span class="sxs-lookup"><span data-stu-id="ccd8c-137">toolearn about routing and custom endpoints, see [Use custom endpoints and routing rules for device-to-cloud messages][lnk-devguide-custom].</span></span>

## <a name="anti-spoofing-properties"></a><span data-ttu-id="ccd8c-138">Ochrona przed fałszowaniem właściwości</span><span class="sxs-lookup"><span data-stu-id="ccd8c-138">Anti-spoofing properties</span></span>

<span data-ttu-id="ccd8c-139">urządzenie tooavoid fałszowania w komunikatach urządzenia do chmury, Centrum IoT sygnatury wszystkie komunikaty z hello następujące właściwości:</span><span class="sxs-lookup"><span data-stu-id="ccd8c-139">tooavoid device spoofing in device-to-cloud messages, IoT Hub stamps all messages with hello following properties:</span></span>

* <span data-ttu-id="ccd8c-140">**ConnectionDeviceId**</span><span class="sxs-lookup"><span data-stu-id="ccd8c-140">**ConnectionDeviceId**</span></span>
* <span data-ttu-id="ccd8c-141">**ConnectionDeviceGenerationId**</span><span class="sxs-lookup"><span data-stu-id="ccd8c-141">**ConnectionDeviceGenerationId**</span></span>
* <span data-ttu-id="ccd8c-142">**ConnectionAuthMethod**</span><span class="sxs-lookup"><span data-stu-id="ccd8c-142">**ConnectionAuthMethod**</span></span>

<span data-ttu-id="ccd8c-143">Witaj dwie zawierać hello **deviceId** i **generationId** z hello pochodzące z urządzenia, zgodnie [właściwości tożsamości urządzenia][lnk-device-properties].</span><span class="sxs-lookup"><span data-stu-id="ccd8c-143">hello first two contain hello **deviceId** and **generationId** of hello originating device, as per [Device identity properties][lnk-device-properties].</span></span>

<span data-ttu-id="ccd8c-144">Witaj **ConnectionAuthMethod** właściwość zawiera obiekt Zserializowany do postaci JSON z hello następujące właściwości:</span><span class="sxs-lookup"><span data-stu-id="ccd8c-144">hello **ConnectionAuthMethod** property contains a JSON serialized object, with hello following properties:</span></span>

```json
{
  "scope": "{ hub | device}",
  "type": "{ symkey | sas}",
  "issuer": "iothub"
}
```

## <a name="next-steps"></a><span data-ttu-id="ccd8c-145">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="ccd8c-145">Next steps</span></span>

<span data-ttu-id="ccd8c-146">Informacji o zestawów SDK hello toosend urządzenia do chmury komunikatów, zobacz [Azure IoT SDK][lnk-sdks].</span><span class="sxs-lookup"><span data-stu-id="ccd8c-146">For information about hello SDKs you can use toosend device-to-cloud messages, see [Azure IoT SDKs][lnk-sdks].</span></span>

<span data-ttu-id="ccd8c-147">Witaj [wprowadzenie] [ lnk-get-started] samouczki wyjaśniają, jak komunikaty toosend urządzenia do chmury z zarówno symulowane, jak i fizycznych urządzeń.</span><span class="sxs-lookup"><span data-stu-id="ccd8c-147">hello [Get Started][lnk-get-started] tutorials show you how toosend device-to-cloud messages from both simulated and physical devices.</span></span> <span data-ttu-id="ccd8c-148">Aby uzyskać więcej szczegółów, zobacz hello [Centrum IoT procesu wiadomości urządzenia do chmury, za pomocą trasy] [ lnk-d2c-tutorial] samouczka.</span><span class="sxs-lookup"><span data-stu-id="ccd8c-148">For more detail, see hello [Process IoT Hub device-to-cloud messages using routes][lnk-d2c-tutorial] tutorial.</span></span>

[lnk-devguide-builtin]: iot-hub-devguide-messages-read-builtin.md
[lnk-devguide-custom]: iot-hub-devguide-messages-read-custom.md
[lnk-comparison]: iot-hub-compare-event-hubs.md
[lnk-d2c-guidance]: iot-hub-devguide-d2c-guidance.md
[lnk-get-started]: iot-hub-get-started.md

[lnk-event-hubs]: http://azure.microsoft.com/documentation/services/event-hubs/
[lnk-servicebus]: http://azure.microsoft.com/documentation/services/service-bus/
[lnk-quotas]: iot-hub-devguide-quotas-throttling.md
[lnk-sdks]: iot-hub-devguide-sdks.md
[lnk-compatible-endpoint]: iot-hub-devguide-messages-read-builtin.md
[lnk-device-properties]: iot-hub-devguide-identity-registry.md#device-identity-properties
[lnk-devguide-security]: iot-hub-devguide-security.md
[lnk-d2c-tutorial]: iot-hub-csharp-csharp-process-d2c.md
