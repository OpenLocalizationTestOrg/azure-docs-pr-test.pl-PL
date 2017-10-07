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
# <a name="read-device-to-cloud-messages-from-hello-built-in-endpoint"></a>Odczytywać wiadomości urządzenia do chmury z wbudowanym punktem końcowym hello

Domyślnie komunikaty są routingiem toohello wbudowanym punktem końcowym usługi połączonej (**wiadomości/zdarzenia**), która jest zgodna z [usługi Event Hubs][lnk-event-hubs]. Ten punkt końcowy jest obecnie dostępne tylko za pomocą hello [AMQP] [ lnk-amqp] protokołu portu 5671. Centrum IoT przedstawia hello następujących właściwości tooenable toocontrol możesz hello wbudowanych obsługi komunikatów punktu końcowego Centrum zdarzeń zgodnych **wiadomości/zdarzenia**.

| Właściwość            | Opis |
| ------------------- | ----------- |
| **Liczba partycji** | Ta właściwość jest ustawiana na tworzenie toodefine hello liczba [partycje] [ lnk-event-hub-partitions] dla wprowadzanie zdarzeń urządzenia do chmury. |
| **Czas przechowywania**  | Ta właściwość określa, jak długo w dniach, komunikaty są zachowywane przez Centrum IoT. Domyślnie Hello jest jeden dzień, ale może być zwiększona tooseven dni. |

Centrum IoT umożliwia także toomanage grupy konsumentów na powitania wbudowane urządzenia do chmury odbierania punktu końcowego.

Domyślnie wszystkie wiadomości, które nie są jawnie zgodne reguły routingu wiadomości są zapisywane toohello wbudowanym punktem końcowym. Jeśli wyłączysz tę trasę rezerwowy wiadomości, które nie są jawnie zgodne żadnych reguł routingu wiadomości są usuwane.

Można zmodyfikować czas przechowywania hello programowo przez hello [interfejsy API REST dostawcy zasobów Centrum IoT][lnk-resource-provider-apis], lub za pomocą hello [portalu Azure] [ lnk-management-portal].

Centrum IoT przedstawia hello **wiadomości/zdarzenia** tooread hello urządzenia do chmury komunikatów odbieranych przez Centrum usługi wbudowanych punktu końcowego sieci wewnętrznej. Ten punkt końcowy jest zdarzeń zgodnych koncentratora, co pozwala toouse żadnego z usługą Event Hubs hello mechanizmów hello obsługuje do odczytywania wiadomości.

## <a name="read-from-hello-built-in-endpoint"></a>Odczyt z wbudowanym punktem końcowym hello

Jeśli używasz hello [Azure Service Bus SDK dla platformy .NET] [ lnk-servicebus-sdk] lub hello [usługi Event Hubs - hosta procesora zdarzeń][lnk-eventprocessorhost], może używać dowolnego połączenia Centrum IoT ciągi o hello odpowiednie uprawnienia. Następnie użyj **wiadomości/zdarzenia** jako hello nazwy Centrum zdarzeń.

Jeśli używasz zestawów SDK (lub integracji produktu) znają z Centrum IoT, należy pobrać punktu końcowego zgodnego Centrum zdarzeń i nazwę Centrum zdarzeń zgodnych z ustawień Centrum IoT hello w hello [portalu Azure] [ lnk-management-portal]:

1. W bloku Centrum IoT hello, kliknij przycisk **punkty końcowe**.
1. W hello **wbudowane punkty końcowe** kliknij **zdarzenia**. Witaj blok zawiera hello następujące wartości: **punktu końcowego Centrum zdarzeń zgodnych**, **nazwę Centrum zdarzeń zgodnych**, **partycje**, **czas przechowywania**, i **grupy konsumentów**.

    ![Ustawienia urządzenia do chmury][img-eventhubcompatible]

Witaj SDK Centrum IoT wymaga hello Nazwa punktu końcowego Centrum IoT, który jest **wiadomości/zdarzenia** pokazane na powitania **punkty końcowe** bloku.

Jeśli hello są przy użyciu zestawu SDK wymaga **Hostname** lub **Namespace** wartość, usunąć schemat hello hello **punktu końcowego Centrum zdarzeń zgodnych**. Na przykład, jeśli jest punktu końcowego Centrum zdarzeń zgodnych **sb://iothub-ns-myiothub-1234.servicebus.windows.net/**, hello **Hostname** będzie  **Centrum iothub-ns-myiothub-1234.servicebus.windows.net**i hello **Namespace** będzie **Centrum iothub-ns-myiothub-1234**.

Można użyć wszystkie zasady dostępu współdzielonego hello **ServiceConnect** toohello tooconnect uprawnienia określone Centrum zdarzeń.

Jeśli potrzebujesz toobuild parametry połączenia Centrum zdarzeń za pomocą hello poprzednich informacji, użyj hello następującego wzorca:

`Endpoint={Event Hub-compatible endpoint};SharedAccessKeyName={iot hub policy name};SharedAccessKey={iot hub policy key}`

Hello zestawy SDK i integracji w korzystające z punktów końcowych zgodnych z Centrum zdarzeń, które udostępnia Centrum IoT zawiera elementy hello w hello następującej listy:

* [Centra zdarzeń w języku Java klienta](https://github.com/hdinsight/eventhubs-client).
* [Apache Storm spout](../hdinsight/hdinsight-storm-develop-csharp-event-hub-topology.md). Możesz wyświetlić hello [spout źródła](https://github.com/apache/storm/tree/master/external/storm-eventhubs) w witrynie GitHub.
* [Platforma Apache Spark integracji](../hdinsight/hdinsight-apache-spark-eventhub-streaming.md).

## <a name="next-steps"></a>Następne kroki

Aby uzyskać więcej informacji na temat punkty końcowe Centrum IoT, zobacz [punkty końcowe Centrum IoT][lnk-endpoints].

Witaj [wprowadzenie] [ lnk-get-started] samouczki wyjaśniają, jak toosend urządzenia do chmury komunikaty z symulowanych urządzeń i odczytywać wiadomości powitania hello wbudowanym punktem końcowym. Aby uzyskać więcej szczegółów, zobacz hello [Centrum IoT procesu wiadomości urządzenia do chmury, za pomocą trasy] [ lnk-d2c-tutorial] samouczka.

Jeśli chcesz, aby tooroute Twojego urządzenia do chmury wiadomości toocustom punktów końcowych, zobacz [urządzenia do chmury wiadomości wysyłanych tras wiadomości i niestandardowe punkty końcowe][lnk-custom].

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
