---
title: "Zrozumienie wbudowanych punktu końcowego Centrum IoT Azure | Dokumentacja firmy Microsoft"
description: "Przewodnik dewelopera - informacje dotyczące używania wbudowanych, wiadomości z urządzenia do chmury toread punktu końcowego zgodnego Centrum zdarzeń."
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
ms.openlocfilehash: fcc3743028e369fdc42b71887d49fb41fba2c0dc
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="read-device-to-cloud-messages-from-the-built-in-endpoint"></a><span data-ttu-id="d5beb-103">Przeczytaj komunikaty urządzenia do chmury z wbudowanym punktem końcowym</span><span class="sxs-lookup"><span data-stu-id="d5beb-103">Read device-to-cloud messages from the built-in endpoint</span></span>

<span data-ttu-id="d5beb-104">Domyślnie komunikaty są kierowane do wbudowanym punktem końcowym usługi połączonej (**wiadomości/zdarzenia**), która jest zgodna z [usługi Event Hubs][lnk-event-hubs].</span><span class="sxs-lookup"><span data-stu-id="d5beb-104">By default, messages are routed to the built-in service-facing endpoint (**messages/events**), that is compatible with [Event Hubs][lnk-event-hubs].</span></span> <span data-ttu-id="d5beb-105">Ten punkt końcowy jest obecnie tylko narażonych przy użyciu [AMQP] [ lnk-amqp] protokołu portu 5671.</span><span class="sxs-lookup"><span data-stu-id="d5beb-105">This endpoint is currently only exposed using the [AMQP][lnk-amqp] protocol on port 5671.</span></span> <span data-ttu-id="d5beb-106">Centrum IoT uwidacznia następujące właściwości umożliwiają kontrolowanie wbudowanych zgodnego Centrum zdarzeń obsługi komunikatów punktu końcowego **wiadomości/zdarzenia**.</span><span class="sxs-lookup"><span data-stu-id="d5beb-106">An IoT hub exposes the following properties to enable you to control the built-in Event Hub-compatible messaging endpoint **messages/events**.</span></span>

| <span data-ttu-id="d5beb-107">Właściwość</span><span class="sxs-lookup"><span data-stu-id="d5beb-107">Property</span></span>            | <span data-ttu-id="d5beb-108">Opis</span><span class="sxs-lookup"><span data-stu-id="d5beb-108">Description</span></span> |
| ------------------- | ----------- |
| <span data-ttu-id="d5beb-109">**Liczba partycji**</span><span class="sxs-lookup"><span data-stu-id="d5beb-109">**Partition count**</span></span> | <span data-ttu-id="d5beb-110">Ta właściwość jest ustawiana podczas tworzenia, aby określić liczbę [partycje] [ lnk-event-hub-partitions] dla wprowadzanie zdarzeń urządzenia do chmury.</span><span class="sxs-lookup"><span data-stu-id="d5beb-110">Set this property at creation to define the number of [partitions][lnk-event-hub-partitions] for device-to-cloud event ingestion.</span></span> |
| <span data-ttu-id="d5beb-111">**Czas przechowywania**</span><span class="sxs-lookup"><span data-stu-id="d5beb-111">**Retention time**</span></span>  | <span data-ttu-id="d5beb-112">Ta właściwość określa, jak długo w dniach, komunikaty są zachowywane przez Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="d5beb-112">This property specifies how long in days messages are retained by IoT Hub.</span></span> <span data-ttu-id="d5beb-113">Wartość domyślna to jeden dzień, ale można zwiększyć siedem dni.</span><span class="sxs-lookup"><span data-stu-id="d5beb-113">The default is one day, but it can be increased to seven days.</span></span> |

<span data-ttu-id="d5beb-114">Centrum IoT umożliwia także zarządzanie grupy konsumentów na wbudowanych urządzenia do chmury otrzymają punktu końcowego.</span><span class="sxs-lookup"><span data-stu-id="d5beb-114">IoT Hub also enables you to manage consumer groups on the built-in device-to-cloud receive endpoint.</span></span>

<span data-ttu-id="d5beb-115">Domyślnie wszystkie wiadomości, które nie są jawnie zgodne reguły routingu wiadomości są zapisywane na wbudowanym punktem końcowym.</span><span class="sxs-lookup"><span data-stu-id="d5beb-115">By default, all messages that do not explicitly match a message routing rule are written to the built-in endpoint.</span></span> <span data-ttu-id="d5beb-116">Jeśli wyłączysz tę trasę rezerwowy wiadomości, które nie są jawnie zgodne żadnych reguł routingu wiadomości są usuwane.</span><span class="sxs-lookup"><span data-stu-id="d5beb-116">If you disable this fallback route, messages that do not explicitly match any message routing rules are dropped.</span></span>

<span data-ttu-id="d5beb-117">Czas przechowywania, można zmodyfikować albo programowo za pomocą [interfejsy API REST dostawcy zasobów Centrum IoT][lnk-resource-provider-apis], lub za pomocą [portalu Azure] [ lnk-management-portal].</span><span class="sxs-lookup"><span data-stu-id="d5beb-117">You can modify the retention time, either programmatically through the [IoT Hub resource provider REST APIs][lnk-resource-provider-apis], or by using the [Azure portal][lnk-management-portal].</span></span>

<span data-ttu-id="d5beb-118">Centrum IoT przedstawia **wiadomości/zdarzenia** wbudowanych punktu końcowego usługi zaplecza, aby odczytać odebrane przez Centrum wiadomości urządzenia do chmury.</span><span class="sxs-lookup"><span data-stu-id="d5beb-118">IoT Hub exposes the **messages/events** built-in endpoint for your back-end services to read the device-to-cloud messages received by your hub.</span></span> <span data-ttu-id="d5beb-119">Ten punkt końcowy jest zdarzeń zgodnych koncentratora, dzięki czemu można użyć innych mechanizmów usługę Event Hubs obsługuje do odczytywania wiadomości.</span><span class="sxs-lookup"><span data-stu-id="d5beb-119">This endpoint is Event Hub-compatible, which enables you to use any of the mechanisms the Event Hubs service supports for reading messages.</span></span>

## <a name="read-from-the-built-in-endpoint"></a><span data-ttu-id="d5beb-120">Odczyt z wbudowanym punktem końcowym.</span><span class="sxs-lookup"><span data-stu-id="d5beb-120">Read from the built-in endpoint</span></span>

<span data-ttu-id="d5beb-121">Jeśli używasz [Azure Service Bus SDK dla platformy .NET] [ lnk-servicebus-sdk] lub [usługi Event Hubs - hosta procesora zdarzeń][lnk-eventprocessorhost], może używać dowolnego połączenia Centrum IoT ciągi z odpowiednimi uprawnieniami.</span><span class="sxs-lookup"><span data-stu-id="d5beb-121">When you use the [Azure Service Bus SDK for .NET][lnk-servicebus-sdk] or the [Event Hubs - Event Processor Host][lnk-eventprocessorhost], you can use any IoT Hub connection strings with the correct permissions.</span></span> <span data-ttu-id="d5beb-122">Następnie użyj **wiadomości/zdarzenia** jako nazwy Centrum zdarzeń.</span><span class="sxs-lookup"><span data-stu-id="d5beb-122">Then use **messages/events** as the Event Hub name.</span></span>

<span data-ttu-id="d5beb-123">Jeśli używasz zestawów SDK (lub integracji produktu) znają z Centrum IoT, należy pobrać punktu końcowego zgodnego Centrum zdarzeń i nazwę Centrum zdarzeń zgodnych z ustawień Centrum IoT w [portalu Azure][lnk-management-portal]:</span><span class="sxs-lookup"><span data-stu-id="d5beb-123">When you use SDKs (or product integrations) that are unaware of IoT Hub, you must retrieve an Event Hub-compatible endpoint and Event Hub-compatible name from the IoT Hub settings in the [Azure portal][lnk-management-portal]:</span></span>

1. <span data-ttu-id="d5beb-124">W bloku Centrum IoT kliknij **punkty końcowe**.</span><span class="sxs-lookup"><span data-stu-id="d5beb-124">In the IoT hub blade, click **Endpoints**.</span></span>
1. <span data-ttu-id="d5beb-125">W **wbudowane punkty końcowe** kliknij **zdarzenia**.</span><span class="sxs-lookup"><span data-stu-id="d5beb-125">In the **Built-in endpoints** section, click **Events**.</span></span> <span data-ttu-id="d5beb-126">Blok zawiera następujące wartości: **punktu końcowego Centrum zdarzeń zgodnych**, **nazwę Centrum zdarzeń zgodnych**, **partycje**, **czas przechowywania**, i **grupy konsumentów**.</span><span class="sxs-lookup"><span data-stu-id="d5beb-126">The blade contains the following values: **Event Hub-compatible endpoint**, **Event Hub-compatible name**, **Partitions**, **Retention time**, and **Consumer groups**.</span></span>

    ![Ustawienia urządzenia do chmury][img-eventhubcompatible]

<span data-ttu-id="d5beb-128">Nazwa punktu końcowego Centrum IoT, czyli wymaga zestawu SDK Centrum IoT **wiadomości/zdarzenia** jak pokazano w **punkty końcowe** bloku.</span><span class="sxs-lookup"><span data-stu-id="d5beb-128">The IoT Hub SDK requires the IoT Hub endpoint name, which is **messages/events** as shown in the **Endpoints** blade.</span></span>

<span data-ttu-id="d5beb-129">Jeśli korzystasz z zestawu SDK wymaga **Hostname** lub **Namespace** wartość, Usuń schemat z **punktu końcowego Centrum zdarzeń zgodnych**.</span><span class="sxs-lookup"><span data-stu-id="d5beb-129">If the SDK you are using requires a **Hostname** or **Namespace** value, remove the scheme from the **Event Hub-compatible endpoint**.</span></span> <span data-ttu-id="d5beb-130">Na przykład, jeśli jest punktu końcowego Centrum zdarzeń zgodnych **sb://iothub-ns-myiothub-1234.servicebus.windows.net/**, **Hostname** będzie  **Centrum iothub-ns-myiothub-1234.servicebus.windows.net**i **Namespace** będzie **Centrum iothub-ns-myiothub-1234**.</span><span class="sxs-lookup"><span data-stu-id="d5beb-130">For example, if your Event Hub-compatible endpoint is **sb://iothub-ns-myiothub-1234.servicebus.windows.net/**, the **Hostname** would be **iothub-ns-myiothub-1234.servicebus.windows.net**, and the **Namespace** would be **iothub-ns-myiothub-1234**.</span></span>

<span data-ttu-id="d5beb-131">Następnie można użyć dowolnego zasady dostępu współdzielonego, który ma **ServiceConnect** uprawnień do łączenia się z określonym Centrum zdarzeń.</span><span class="sxs-lookup"><span data-stu-id="d5beb-131">You can then use any shared access policy that has the **ServiceConnect** permissions to connect to the specified Event Hub.</span></span>

<span data-ttu-id="d5beb-132">Jeśli musisz utworzyć parametry połączenia Centrum zdarzeń przy użyciu poprzednich informacji, użyj następującego wzorca:</span><span class="sxs-lookup"><span data-stu-id="d5beb-132">If you need to build an Event Hub connection string by using the previous information, use the following pattern:</span></span>

`Endpoint={Event Hub-compatible endpoint};SharedAccessKeyName={iot hub policy name};SharedAccessKey={iot hub policy key}`

<span data-ttu-id="d5beb-133">Zestawy SDK i integracji w korzystające z punktów końcowych zgodnych z Centrum zdarzeń, które udostępnia Centrum IoT zawiera elementy na liście poniżej:</span><span class="sxs-lookup"><span data-stu-id="d5beb-133">The SDKs and integrations that you can use with Event Hub-compatible endpoints that IoT Hub exposes includes the items in the following list:</span></span>

* <span data-ttu-id="d5beb-134">[Centra zdarzeń w języku Java klienta](https://github.com/hdinsight/eventhubs-client).</span><span class="sxs-lookup"><span data-stu-id="d5beb-134">[Java Event Hubs client](https://github.com/hdinsight/eventhubs-client).</span></span>
* <span data-ttu-id="d5beb-135">[Apache Storm spout](../hdinsight/hdinsight-storm-develop-csharp-event-hub-topology.md).</span><span class="sxs-lookup"><span data-stu-id="d5beb-135">[Apache Storm spout](../hdinsight/hdinsight-storm-develop-csharp-event-hub-topology.md).</span></span> <span data-ttu-id="d5beb-136">Możesz wyświetlić [spout źródła](https://github.com/apache/storm/tree/master/external/storm-eventhubs) w witrynie GitHub.</span><span class="sxs-lookup"><span data-stu-id="d5beb-136">You can view the [spout source](https://github.com/apache/storm/tree/master/external/storm-eventhubs) on GitHub.</span></span>
* <span data-ttu-id="d5beb-137">[Platforma Apache Spark integracji](../hdinsight/hdinsight-apache-spark-eventhub-streaming.md).</span><span class="sxs-lookup"><span data-stu-id="d5beb-137">[Apache Spark integration](../hdinsight/hdinsight-apache-spark-eventhub-streaming.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="d5beb-138">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="d5beb-138">Next steps</span></span>

<span data-ttu-id="d5beb-139">Aby uzyskać więcej informacji na temat punkty końcowe Centrum IoT, zobacz [punkty końcowe Centrum IoT][lnk-endpoints].</span><span class="sxs-lookup"><span data-stu-id="d5beb-139">For more information about IoT Hub endpoints, see [IoT Hub endpoints][lnk-endpoints].</span></span>

<span data-ttu-id="d5beb-140">[Wprowadzenie] [ lnk-get-started] samouczki wyjaśniają, jak wysyłać urządzenia do chmury z symulowanego urządzenia i odczytywać wiadomości z wbudowanym punktem końcowym.</span><span class="sxs-lookup"><span data-stu-id="d5beb-140">The [Get Started][lnk-get-started] tutorials show you how to send device-to-cloud messages from simulated devices and read the messages from the built-in endpoint.</span></span> <span data-ttu-id="d5beb-141">Aby uzyskać więcej szczegółów, zobacz [Centrum IoT procesu wiadomości urządzenia do chmury, za pomocą trasy] [ lnk-d2c-tutorial] samouczka.</span><span class="sxs-lookup"><span data-stu-id="d5beb-141">For more detail, see the [Process IoT Hub device-to-cloud messages using routes][lnk-d2c-tutorial] tutorial.</span></span>

<span data-ttu-id="d5beb-142">Jeśli chcesz rozesłać wiadomości urządzenia do chmury do niestandardowe punkty końcowe, zobacz [urządzenia do chmury wiadomości wysyłanych tras wiadomości i niestandardowe punkty końcowe][lnk-custom].</span><span class="sxs-lookup"><span data-stu-id="d5beb-142">If you want to route your device-to-cloud messages to custom endpoints, see [Use message routes and custom endpoints for device-to-cloud messages][lnk-custom].</span></span>

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
