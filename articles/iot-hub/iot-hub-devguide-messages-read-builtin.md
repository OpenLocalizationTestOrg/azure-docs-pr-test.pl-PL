---
title: "wbudowanym punktem końcowym aaaUnderstand hello Azure IoT Hub | Dokumentacja firmy Microsoft"
description: "Przewodnik dewelopera - opisano, jak toouse hello wbudowanych, wiadomości urządzenia do chmury toread punktu końcowego zgodnego Centrum zdarzeń."
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
ms.openlocfilehash: 15484c1b1828151ffcae5f4a1407264374223da1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="read-device-to-cloud-messages-from-hello-built-in-endpoint"></a><span data-ttu-id="d0470-103">Odczytywać wiadomości urządzenia do chmury z wbudowanym punktem końcowym hello</span><span class="sxs-lookup"><span data-stu-id="d0470-103">Read device-to-cloud messages from hello built-in endpoint</span></span>

<span data-ttu-id="d0470-104">Domyślnie komunikaty są routingiem toohello wbudowanym punktem końcowym usługi połączonej (**wiadomości/zdarzenia**), która jest zgodna z [usługi Event Hubs][lnk-event-hubs].</span><span class="sxs-lookup"><span data-stu-id="d0470-104">By default, messages are routed toohello built-in service-facing endpoint (**messages/events**), that is compatible with [Event Hubs][lnk-event-hubs].</span></span> <span data-ttu-id="d0470-105">Ten punkt końcowy jest obecnie dostępne tylko za pomocą hello [AMQP] [ lnk-amqp] protokołu portu 5671.</span><span class="sxs-lookup"><span data-stu-id="d0470-105">This endpoint is currently only exposed using hello [AMQP][lnk-amqp] protocol on port 5671.</span></span> <span data-ttu-id="d0470-106">Centrum IoT przedstawia hello następujących właściwości tooenable toocontrol możesz hello wbudowanych obsługi komunikatów punktu końcowego Centrum zdarzeń zgodnych **wiadomości/zdarzenia**.</span><span class="sxs-lookup"><span data-stu-id="d0470-106">An IoT hub exposes hello following properties tooenable you toocontrol hello built-in Event Hub-compatible messaging endpoint **messages/events**.</span></span>

| <span data-ttu-id="d0470-107">Właściwość</span><span class="sxs-lookup"><span data-stu-id="d0470-107">Property</span></span>            | <span data-ttu-id="d0470-108">Opis</span><span class="sxs-lookup"><span data-stu-id="d0470-108">Description</span></span> |
| ------------------- | ----------- |
| <span data-ttu-id="d0470-109">**Liczba partycji**</span><span class="sxs-lookup"><span data-stu-id="d0470-109">**Partition count**</span></span> | <span data-ttu-id="d0470-110">Ta właściwość jest ustawiana na tworzenie toodefine hello liczba [partycje] [ lnk-event-hub-partitions] dla wprowadzanie zdarzeń urządzenia do chmury.</span><span class="sxs-lookup"><span data-stu-id="d0470-110">Set this property at creation toodefine hello number of [partitions][lnk-event-hub-partitions] for device-to-cloud event ingestion.</span></span> |
| <span data-ttu-id="d0470-111">**Czas przechowywania**</span><span class="sxs-lookup"><span data-stu-id="d0470-111">**Retention time**</span></span>  | <span data-ttu-id="d0470-112">Ta właściwość określa, jak długo w dniach, komunikaty są zachowywane przez Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="d0470-112">This property specifies how long in days messages are retained by IoT Hub.</span></span> <span data-ttu-id="d0470-113">Domyślnie Hello jest jeden dzień, ale może być zwiększona tooseven dni.</span><span class="sxs-lookup"><span data-stu-id="d0470-113">hello default is one day, but it can be increased tooseven days.</span></span> |

<span data-ttu-id="d0470-114">Centrum IoT umożliwia także toomanage grupy konsumentów na powitania wbudowane urządzenia do chmury odbierania punktu końcowego.</span><span class="sxs-lookup"><span data-stu-id="d0470-114">IoT Hub also enables you toomanage consumer groups on hello built-in device-to-cloud receive endpoint.</span></span>

<span data-ttu-id="d0470-115">Domyślnie wszystkie wiadomości, które nie są jawnie zgodne reguły routingu wiadomości są zapisywane toohello wbudowanym punktem końcowym.</span><span class="sxs-lookup"><span data-stu-id="d0470-115">By default, all messages that do not explicitly match a message routing rule are written toohello built-in endpoint.</span></span> <span data-ttu-id="d0470-116">Jeśli wyłączysz tę trasę rezerwowy wiadomości, które nie są jawnie zgodne żadnych reguł routingu wiadomości są usuwane.</span><span class="sxs-lookup"><span data-stu-id="d0470-116">If you disable this fallback route, messages that do not explicitly match any message routing rules are dropped.</span></span>

<span data-ttu-id="d0470-117">Można zmodyfikować czas przechowywania hello programowo przez hello [interfejsy API REST dostawcy zasobów Centrum IoT][lnk-resource-provider-apis], lub za pomocą hello [portalu Azure] [ lnk-management-portal].</span><span class="sxs-lookup"><span data-stu-id="d0470-117">You can modify hello retention time, either programmatically through hello [IoT Hub resource provider REST APIs][lnk-resource-provider-apis], or by using hello [Azure portal][lnk-management-portal].</span></span>

<span data-ttu-id="d0470-118">Centrum IoT przedstawia hello **wiadomości/zdarzenia** tooread hello urządzenia do chmury komunikatów odbieranych przez Centrum usługi wbudowanych punktu końcowego sieci wewnętrznej.</span><span class="sxs-lookup"><span data-stu-id="d0470-118">IoT Hub exposes hello **messages/events** built-in endpoint for your back-end services tooread hello device-to-cloud messages received by your hub.</span></span> <span data-ttu-id="d0470-119">Ten punkt końcowy jest zdarzeń zgodnych koncentratora, co pozwala toouse żadnego z usługą Event Hubs hello mechanizmów hello obsługuje do odczytywania wiadomości.</span><span class="sxs-lookup"><span data-stu-id="d0470-119">This endpoint is Event Hub-compatible, which enables you toouse any of hello mechanisms hello Event Hubs service supports for reading messages.</span></span>

## <a name="read-from-hello-built-in-endpoint"></a><span data-ttu-id="d0470-120">Odczyt z wbudowanym punktem końcowym hello</span><span class="sxs-lookup"><span data-stu-id="d0470-120">Read from hello built-in endpoint</span></span>

<span data-ttu-id="d0470-121">Jeśli używasz hello [Azure Service Bus SDK dla platformy .NET] [ lnk-servicebus-sdk] lub hello [usługi Event Hubs - hosta procesora zdarzeń][lnk-eventprocessorhost], może używać dowolnego połączenia Centrum IoT ciągi o hello odpowiednie uprawnienia.</span><span class="sxs-lookup"><span data-stu-id="d0470-121">When you use hello [Azure Service Bus SDK for .NET][lnk-servicebus-sdk] or hello [Event Hubs - Event Processor Host][lnk-eventprocessorhost], you can use any IoT Hub connection strings with hello correct permissions.</span></span> <span data-ttu-id="d0470-122">Następnie użyj **wiadomości/zdarzenia** jako hello nazwy Centrum zdarzeń.</span><span class="sxs-lookup"><span data-stu-id="d0470-122">Then use **messages/events** as hello Event Hub name.</span></span>

<span data-ttu-id="d0470-123">Jeśli używasz zestawów SDK (lub integracji produktu) znają z Centrum IoT, należy pobrać punktu końcowego zgodnego Centrum zdarzeń i nazwę Centrum zdarzeń zgodnych z ustawień Centrum IoT hello w hello [portalu Azure] [ lnk-management-portal]:</span><span class="sxs-lookup"><span data-stu-id="d0470-123">When you use SDKs (or product integrations) that are unaware of IoT Hub, you must retrieve an Event Hub-compatible endpoint and Event Hub-compatible name from hello IoT Hub settings in hello [Azure portal][lnk-management-portal]:</span></span>

1. <span data-ttu-id="d0470-124">W bloku Centrum IoT hello, kliknij przycisk **punkty końcowe**.</span><span class="sxs-lookup"><span data-stu-id="d0470-124">In hello IoT hub blade, click **Endpoints**.</span></span>
1. <span data-ttu-id="d0470-125">W hello **wbudowane punkty końcowe** kliknij **zdarzenia**.</span><span class="sxs-lookup"><span data-stu-id="d0470-125">In hello **Built-in endpoints** section, click **Events**.</span></span> <span data-ttu-id="d0470-126">Witaj blok zawiera hello następujące wartości: **punktu końcowego Centrum zdarzeń zgodnych**, **nazwę Centrum zdarzeń zgodnych**, **partycje**, **czas przechowywania**, i **grupy konsumentów**.</span><span class="sxs-lookup"><span data-stu-id="d0470-126">hello blade contains hello following values: **Event Hub-compatible endpoint**, **Event Hub-compatible name**, **Partitions**, **Retention time**, and **Consumer groups**.</span></span>

    ![Ustawienia urządzenia do chmury][img-eventhubcompatible]

<span data-ttu-id="d0470-128">Witaj SDK Centrum IoT wymaga hello Nazwa punktu końcowego Centrum IoT, który jest **wiadomości/zdarzenia** pokazane na powitania **punkty końcowe** bloku.</span><span class="sxs-lookup"><span data-stu-id="d0470-128">hello IoT Hub SDK requires hello IoT Hub endpoint name, which is **messages/events** as shown in hello **Endpoints** blade.</span></span>

<span data-ttu-id="d0470-129">Jeśli hello są przy użyciu zestawu SDK wymaga **Hostname** lub **Namespace** wartość, usunąć schemat hello hello **punktu końcowego Centrum zdarzeń zgodnych**.</span><span class="sxs-lookup"><span data-stu-id="d0470-129">If hello SDK you are using requires a **Hostname** or **Namespace** value, remove hello scheme from hello **Event Hub-compatible endpoint**.</span></span> <span data-ttu-id="d0470-130">Na przykład, jeśli jest punktu końcowego Centrum zdarzeń zgodnych **sb://iothub-ns-myiothub-1234.servicebus.windows.net/**, hello **Hostname** będzie  **Centrum iothub-ns-myiothub-1234.servicebus.windows.net**i hello **Namespace** będzie **Centrum iothub-ns-myiothub-1234**.</span><span class="sxs-lookup"><span data-stu-id="d0470-130">For example, if your Event Hub-compatible endpoint is **sb://iothub-ns-myiothub-1234.servicebus.windows.net/**, hello **Hostname** would be **iothub-ns-myiothub-1234.servicebus.windows.net**, and hello **Namespace** would be **iothub-ns-myiothub-1234**.</span></span>

<span data-ttu-id="d0470-131">Można użyć wszystkie zasady dostępu współdzielonego hello **ServiceConnect** toohello tooconnect uprawnienia określone Centrum zdarzeń.</span><span class="sxs-lookup"><span data-stu-id="d0470-131">You can then use any shared access policy that has hello **ServiceConnect** permissions tooconnect toohello specified Event Hub.</span></span>

<span data-ttu-id="d0470-132">Jeśli potrzebujesz toobuild parametry połączenia Centrum zdarzeń za pomocą hello poprzednich informacji, użyj hello następującego wzorca:</span><span class="sxs-lookup"><span data-stu-id="d0470-132">If you need toobuild an Event Hub connection string by using hello previous information, use hello following pattern:</span></span>

`Endpoint={Event Hub-compatible endpoint};SharedAccessKeyName={iot hub policy name};SharedAccessKey={iot hub policy key}`

<span data-ttu-id="d0470-133">Hello zestawy SDK i integracji w korzystające z punktów końcowych zgodnych z Centrum zdarzeń, które udostępnia Centrum IoT zawiera elementy hello w hello następującej listy:</span><span class="sxs-lookup"><span data-stu-id="d0470-133">hello SDKs and integrations that you can use with Event Hub-compatible endpoints that IoT Hub exposes includes hello items in hello following list:</span></span>

* <span data-ttu-id="d0470-134">[Centra zdarzeń w języku Java klienta](https://github.com/hdinsight/eventhubs-client).</span><span class="sxs-lookup"><span data-stu-id="d0470-134">[Java Event Hubs client](https://github.com/hdinsight/eventhubs-client).</span></span>
* <span data-ttu-id="d0470-135">[Apache Storm spout](../hdinsight/hdinsight-storm-develop-csharp-event-hub-topology.md).</span><span class="sxs-lookup"><span data-stu-id="d0470-135">[Apache Storm spout](../hdinsight/hdinsight-storm-develop-csharp-event-hub-topology.md).</span></span> <span data-ttu-id="d0470-136">Możesz wyświetlić hello [spout źródła](https://github.com/apache/storm/tree/master/external/storm-eventhubs) w witrynie GitHub.</span><span class="sxs-lookup"><span data-stu-id="d0470-136">You can view hello [spout source](https://github.com/apache/storm/tree/master/external/storm-eventhubs) on GitHub.</span></span>
* <span data-ttu-id="d0470-137">[Platforma Apache Spark integracji](../hdinsight/hdinsight-apache-spark-eventhub-streaming.md).</span><span class="sxs-lookup"><span data-stu-id="d0470-137">[Apache Spark integration](../hdinsight/hdinsight-apache-spark-eventhub-streaming.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="d0470-138">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="d0470-138">Next steps</span></span>

<span data-ttu-id="d0470-139">Aby uzyskać więcej informacji na temat punkty końcowe Centrum IoT, zobacz [punkty końcowe Centrum IoT][lnk-endpoints].</span><span class="sxs-lookup"><span data-stu-id="d0470-139">For more information about IoT Hub endpoints, see [IoT Hub endpoints][lnk-endpoints].</span></span>

<span data-ttu-id="d0470-140">Witaj [wprowadzenie] [ lnk-get-started] samouczki wyjaśniają, jak toosend urządzenia do chmury komunikaty z symulowanych urządzeń i odczytywać wiadomości powitania hello wbudowanym punktem końcowym.</span><span class="sxs-lookup"><span data-stu-id="d0470-140">hello [Get Started][lnk-get-started] tutorials show you how toosend device-to-cloud messages from simulated devices and read hello messages from hello built-in endpoint.</span></span> <span data-ttu-id="d0470-141">Aby uzyskać więcej szczegółów, zobacz hello [Centrum IoT procesu wiadomości urządzenia do chmury, za pomocą trasy] [ lnk-d2c-tutorial] samouczka.</span><span class="sxs-lookup"><span data-stu-id="d0470-141">For more detail, see hello [Process IoT Hub device-to-cloud messages using routes][lnk-d2c-tutorial] tutorial.</span></span>

<span data-ttu-id="d0470-142">Jeśli chcesz, aby tooroute Twojego urządzenia do chmury wiadomości toocustom punktów końcowych, zobacz [urządzenia do chmury wiadomości wysyłanych tras wiadomości i niestandardowe punkty końcowe][lnk-custom].</span><span class="sxs-lookup"><span data-stu-id="d0470-142">If you want tooroute your device-to-cloud messages toocustom endpoints, see [Use message routes and custom endpoints for device-to-cloud messages][lnk-custom].</span></span>

[img-eventhubcompatible]: ./media/iot-hub-devguide-messages-read-builtin/eventhubcompatible.png

[lnk-custom]: iot-hub-devguide-messages-read-custom.md
[lnk-get-started]: iot-hub-get-started.md
[lnk-endpoints]: iot-hub-devguide-endpoints.md
[lnk-resource-provider-apis]: https://docs.microsoft.com/rest/api/iothub/iothubresource
[lnk-event-hubs]: http://azure.microsoft.com/documentation/services/event-hubs/
[lnk-management-portal]: https://portal.azure.com
[lnk-d2c-tutorial]: iot-hub-csharp-csharp-process-d2c.md
[lnk-event-hub-partitions]: ../event-hubs/event-hubs-features.md#partitions
[lnk-servicebus-sdk]: https://www.nuget.org/packages/WindowsAzure.ServiceBus
[lnk-eventprocessorhost]: http://blogs.msdn.com/b/servicebus/archive/2015/01/16/event-processor-host-best-practices-part-1.aspx
[lnk-amqp]: https://www.amqp.org/
