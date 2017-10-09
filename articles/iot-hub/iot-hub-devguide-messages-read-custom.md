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
# <a name="use-message-routes-and-custom-endpoints-for-device-to-cloud-messages"></a>Urządzenia do chmury wiadomości wysyłanych tras wiadomości i niestandardowe punkty końcowe

Centrum IoT umożliwia tooroute [wiadomości urządzenia do chmury] [ lnk-device-to-cloud] tooIoT Centrum połączonej usługi punktów końcowych na podstawie komunikatu właściwości. Routing zapewnia reguły hello toosend elastyczność wiadomości, których potrzebują toogo bez hello muszą wiadomości tooprocess dodatkowych usług lub toowrite dodatkowy kod. Reguł routingu, które można skonfigurować ma hello następujące właściwości:

| Właściwość      | Opis |
| ------------- | ----------- |
| **Nazwa**      | Witaj unikatową nazwę identyfikującą hello reguły. |
| **Źródło**    | Witaj pochodzenia danych hello strumienia toobe reagować. Na przykład telemetrii urządzenia. |
| **Warunek** | wyrażenia zapytania Hello hello reguły routingu, które jest wykonywane na nagłówki i treści wiadomości powitania i czy jest dopasowanie dla punktu końcowego hello są używane toodetermine. Aby uzyskać więcej informacji na temat tworzenia warunku trasy, zobacz hello [odwołanie - zapytania języka twins urządzenia i zadania][lnk-devguide-query-language]. |
| **Punkt końcowy**  | Nazwa Hello hello punktu końcowego, gdy Centrum IoT wysyła wiadomości spełniających warunek hello. Punkty końcowe powinna mieć hello tego samego regionu Centrum IoT hello, w przeciwnym razie może być wymagana dla regionu między zapisuje. |

Pojedynczy komunikat może odpowiadać warunek hello na wielu reguł routingu, w których przypadku Centrum IoT zapewnia endpoint toohello wiadomość hello skojarzone z każdą regułę dopasowany. Centrum IoT automatycznie deduplicates dostarczanie komunikatów, jeśli komunikat odpowiada wielu reguł mające hello tego samego miejsca docelowego, jest ona tylko zapisywana docelowego toothat raz.

Centrum IoT ma wartość domyślną [wbudowanym punktem końcowym][lnk-built-in]. Można utworzyć tooby wiadomości tooroute niestandardowe punkty końcowe łączenie innych usług w Centrum toohello subskrypcji. Centrum IoT obecnie obsługuje centra zdarzeń, kolejki usługi Service Bus i tematów usługi Service Bus jako niestandardowe punkty końcowe.

> [!WARNING]
> Usługa Service Bus kolejek i tematów z **sesji** lub **wykrywania duplikatów** włączone nie są obsługiwane jako niestandardowe punkty końcowe.

Aby uzyskać więcej informacji na temat tworzenia niestandardowych punktów końcowych w Centrum IoT, zobacz [punkty końcowe Centrum IoT][lnk-devguide-endpoints].

Aby uzyskać więcej informacji na temat odczytu z niestandardowe punkty końcowe zobacz:

* Odczytywanie z [usługi Event Hubs][lnk-getstarted-eh].
* Odczytywanie z [kolejek usługi Service Bus][lnk-getstarted-queue].
* Odczytywanie z [tematów usługi Service Bus][lnk-getstarted-topic].

### <a name="next-steps"></a>Następne kroki

Aby uzyskać więcej informacji na temat punkty końcowe Centrum IoT, zobacz [punkty końcowe Centrum IoT][lnk-devguide-endpoints].

Aby uzyskać więcej informacji o język zapytań hello używania toodefine reguły routingu, zobacz [Centrum IoT zapytania języka twins urządzenia, zadania i rozsyłania wiadomości][lnk-devguide-query-language].

Witaj [Centrum IoT procesu wiadomości urządzenia do chmury, za pomocą trasy] [ lnk-d2c-tutorial] samouczek pokazuje, jak zasady routingu toouse i niestandardowe punkty końcowe.

[lnk-built-in]: iot-hub-devguide-messages-read-builtin.md
[lnk-device-to-cloud]: iot-hub-devguide-messages-d2c.md
[lnk-devguide-query-language]: iot-hub-devguide-query-language.md
[lnk-devguide-endpoints]: iot-hub-devguide-endpoints.md
[lnk-d2c-tutorial]: iot-hub-csharp-csharp-process-d2c.md
[lnk-getstarted-eh]: ../event-hubs/event-hubs-csharp-ephcs-getstarted.md
[lnk-getstarted-queue]: ../service-bus-messaging/service-bus-dotnet-get-started-with-queues.md
[lnk-getstarted-topic]: ../service-bus-messaging/service-bus-dotnet-how-to-use-topics-subscriptions.md
