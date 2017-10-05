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
# <a name="read-device-to-cloud-messages-from-the-built-in-endpoint"></a>Przeczytaj komunikaty urządzenia do chmury z wbudowanym punktem końcowym

Domyślnie komunikaty są kierowane do wbudowanym punktem końcowym usługi połączonej (**wiadomości/zdarzenia**), która jest zgodna z [usługi Event Hubs][lnk-event-hubs]. Ten punkt końcowy jest obecnie tylko narażonych przy użyciu [AMQP] [ lnk-amqp] protokołu portu 5671. Centrum IoT uwidacznia następujące właściwości umożliwiają kontrolowanie wbudowanych zgodnego Centrum zdarzeń obsługi komunikatów punktu końcowego **wiadomości/zdarzenia**.

| Właściwość            | Opis |
| ------------------- | ----------- |
| **Liczba partycji** | Ta właściwość jest ustawiana podczas tworzenia, aby określić liczbę [partycje] [ lnk-event-hub-partitions] dla wprowadzanie zdarzeń urządzenia do chmury. |
| **Czas przechowywania**  | Ta właściwość określa, jak długo w dniach, komunikaty są zachowywane przez Centrum IoT. Wartość domyślna to jeden dzień, ale można zwiększyć siedem dni. |

Centrum IoT umożliwia także zarządzanie grupy konsumentów na wbudowanych urządzenia do chmury otrzymają punktu końcowego.

Domyślnie wszystkie wiadomości, które nie są jawnie zgodne reguły routingu wiadomości są zapisywane na wbudowanym punktem końcowym. Jeśli wyłączysz tę trasę rezerwowy wiadomości, które nie są jawnie zgodne żadnych reguł routingu wiadomości są usuwane.

Czas przechowywania, można zmodyfikować albo programowo za pomocą [interfejsy API REST dostawcy zasobów Centrum IoT][lnk-resource-provider-apis], lub za pomocą [portalu Azure] [ lnk-management-portal].

Centrum IoT przedstawia **wiadomości/zdarzenia** wbudowanych punktu końcowego usługi zaplecza, aby odczytać odebrane przez Centrum wiadomości urządzenia do chmury. Ten punkt końcowy jest zdarzeń zgodnych koncentratora, dzięki czemu można użyć innych mechanizmów usługę Event Hubs obsługuje do odczytywania wiadomości.

## <a name="read-from-the-built-in-endpoint"></a>Odczyt z wbudowanym punktem końcowym.

Jeśli używasz [Azure Service Bus SDK dla platformy .NET] [ lnk-servicebus-sdk] lub [usługi Event Hubs - hosta procesora zdarzeń][lnk-eventprocessorhost], może używać dowolnego połączenia Centrum IoT ciągi z odpowiednimi uprawnieniami. Następnie użyj **wiadomości/zdarzenia** jako nazwy Centrum zdarzeń.

Jeśli używasz zestawów SDK (lub integracji produktu) znają z Centrum IoT, należy pobrać punktu końcowego zgodnego Centrum zdarzeń i nazwę Centrum zdarzeń zgodnych z ustawień Centrum IoT w [portalu Azure][lnk-management-portal]:

1. W bloku Centrum IoT kliknij **punkty końcowe**.
1. W **wbudowane punkty końcowe** kliknij **zdarzenia**. Blok zawiera następujące wartości: **punktu końcowego Centrum zdarzeń zgodnych**, **nazwę Centrum zdarzeń zgodnych**, **partycje**, **czas przechowywania**, i **grupy konsumentów**.

    ![Ustawienia urządzenia do chmury][img-eventhubcompatible]

Nazwa punktu końcowego Centrum IoT, czyli wymaga zestawu SDK Centrum IoT **wiadomości/zdarzenia** jak pokazano w **punkty końcowe** bloku.

Jeśli korzystasz z zestawu SDK wymaga **Hostname** lub **Namespace** wartość, Usuń schemat z **punktu końcowego Centrum zdarzeń zgodnych**. Na przykład, jeśli jest punktu końcowego Centrum zdarzeń zgodnych **sb://iothub-ns-myiothub-1234.servicebus.windows.net/**, **Hostname** będzie  **Centrum iothub-ns-myiothub-1234.servicebus.windows.net**i **Namespace** będzie **Centrum iothub-ns-myiothub-1234**.

Następnie można użyć dowolnego zasady dostępu współdzielonego, który ma **ServiceConnect** uprawnień do łączenia się z określonym Centrum zdarzeń.

Jeśli musisz utworzyć parametry połączenia Centrum zdarzeń przy użyciu poprzednich informacji, użyj następującego wzorca:

`Endpoint={Event Hub-compatible endpoint};SharedAccessKeyName={iot hub policy name};SharedAccessKey={iot hub policy key}`

Zestawy SDK i integracji w korzystające z punktów końcowych zgodnych z Centrum zdarzeń, które udostępnia Centrum IoT zawiera elementy na liście poniżej:

* [Centra zdarzeń w języku Java klienta](https://github.com/hdinsight/eventhubs-client).
* [Apache Storm spout](../hdinsight/hdinsight-storm-develop-csharp-event-hub-topology.md). Możesz wyświetlić [spout źródła](https://github.com/apache/storm/tree/master/external/storm-eventhubs) w witrynie GitHub.
* [Platforma Apache Spark integracji](../hdinsight/hdinsight-apache-spark-eventhub-streaming.md).

## <a name="next-steps"></a>Następne kroki

Aby uzyskać więcej informacji na temat punkty końcowe Centrum IoT, zobacz [punkty końcowe Centrum IoT][lnk-endpoints].

[Wprowadzenie] [ lnk-get-started] samouczki wyjaśniają, jak wysyłać urządzenia do chmury z symulowanego urządzenia i odczytywać wiadomości z wbudowanym punktem końcowym. Aby uzyskać więcej szczegółów, zobacz [Centrum IoT procesu wiadomości urządzenia do chmury, za pomocą trasy] [ lnk-d2c-tutorial] samouczka.

Jeśli chcesz rozesłać wiadomości urządzenia do chmury do niestandardowe punkty końcowe, zobacz [urządzenia do chmury wiadomości wysyłanych tras wiadomości i niestandardowe punkty końcowe][lnk-custom].

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
