---
title: aaaCompare tooAzure Centrum IoT Azure Event Hubs | Dokumentacja firmy Microsoft
description: "Porównanie hello Centrum IoT i wyróżnianie różnice funkcjonalne i przypadki użycia usług Azure centrów zdarzeń. Porównanie Hello zawiera obsługiwanych protokołów, zarządzanie urządzeniami, monitorowania i przekazywania plików."
services: iot-hub
documentationcenter: 
author: fsautomata
manager: timlt
editor: 
ms.assetid: aeddea62-8302-48e2-9aad-c5a0e5f5abe9
ms.service: iot-hub
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/24/2017
ms.author: elioda
ms.openlocfilehash: e5f546b54e29860498d540abfc86a41c4662c0df
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="comparison-of-azure-iot-hub-and-azure-event-hubs"></a>Porównanie Centrum IoT Azure i usługi Azure Event Hubs
Jednym z hello przypadki użycia głównego Centrum IoT jest toogather telemetrię z urządzeń. Z tego powodu Centrum IoT często jest porównywany zbyt[Azure Event Hubs][Azure Event Hubs]. Podobnie jak Centrum IoT Event Hubs to usługa umożliwiająca zdarzeń i danych telemetrycznych przetwarzania zdarzeń toohello chmury w bardzo dużej skali, z małymi opóźnieniami i wysoką niezawodnością.

Jednak usługi hello mają wiele różnice, które są szczegółowo opisane w poniższej tabeli hello:

| Obszar | Usługa IoT Hub | Usługa Event Hubs |
| --- | --- | --- |
| Wzorce komunikacji | Umożliwia [komunikację urządzenia do chmury] [ lnk-d2c-guidance] (wiadomości, plik przekazywania oraz właściwości zgłoszone) i [komunikacji chmury do urządzenia] [ lnk-c2d-guidance] (bezpośrednie metod, odpowiednie właściwości wiadomości). |Tylko umożliwia transfer danych przychodzących zdarzeń (zazwyczaj wzięta pod uwagę scenariusze urządzenia do chmury). |
| Informacje o stanie urządzenia | [Urządzenie twins] [ lnk-twins] można przechowywać i zapytania o informacje o stanie urządzeń. | Mogą być przechowywane żadne informacje o stanie urządzeń. |
| Obsługa protokołu urządzeń |Obsługuje MQTT, MQTT przez protokół WebSockets, AMQP, AMQP za pośrednictwem protokołu WebSockets i HTTP. Ponadto Centrum IoT współpracuje z hello [brama protokołu Azure IoT][lnk-azure-protocol-gateway], można dostosowywać protokołu bramy implementacji toosupport protokoły niestandardowe. |Obsługa protokołu AMQP, AMQP za pośrednictwem protokołu WebSockets i HTTP. |
| Bezpieczeństwo |Miejsce na urządzenie tożsamości i kontroli dostępu odwoływalny. Zobacz hello [zabezpieczeń części hello Centrum IoT — przewodnik dewelopera]. |Udostępnia centra zdarzeń na poziomie [udostępnionych zasady dostępu][Event Hubs - security], z ograniczoną odwołania obsługuje za pośrednictwem [zasad wydawcy][Event Hubs publisher policies]. Rozwiązania IoT są często poświadczenia wymagane tooimplement niestandardowego rozwiązania toosupport na urządzenie i środki ochrony przed fałszowaniem. |
| Monitorowanie operacji |Umożliwia IoT rozwiązań toosubscribe tooa bogaty zestaw urządzenia tożsamości zarządzania i łączność zdarzeń, takich jak błędy uwierzytelniania poszczególnych urządzeń, ograniczania i wyjątków zły format. Zdarzenia te pozwalają tooquickly zidentyfikować problemy z łącznością na poziomie poszczególnych urządzeń hello. |Przedstawia tylko agregacji metryki. |
| Skalowanie |Jest zoptymalizowany toosupport miliony jednocześnie podłączonych urządzeń. |Liczniki hello połączeń zgodnie [przydziały Azure Event Hubs][Azure Event Hubs quotas]. Na hello drugiej strony, usługa Event Hubs umożliwia toospecify hello partycji dla każdej wiadomości wysyłane. |
| Zestawy SDK urządzenia |Udostępnia [urządzenia zestawów SDK] [ Azure IoT SDKs] dla wielu różnych platformach i językach w toodirect dodanie MQTT, AMQP i HTTP interfejsów API. |Jest obsługiwana w .NET, Java i C, dodanie tooAMQP i interfejsy send HTTP. |
| Przekazywanie pliku |Włącza pliki tooupload rozwiązania IoT z chmury toohello urządzeń. Zawiera punkt końcowy powiadomienia pliku integracji przepływu pracy i operacji monitorowania kategorii w celu obsługi debugowania. | Nie jest obsługiwane. |
| Trasy wiadomości toomultiple punkty końcowe | Zapasowej too10 niestandardowe punkty końcowe są obsługiwane. Reguły określają, jak komunikaty są routingiem toocustom punktów końcowych. Aby uzyskać więcej informacji, zobacz [wysyłania i odbierania wiadomości z Centrum IoT][lnk-devguide-messaging]. | Wymaga dodatkowego kodu toobe napisane i hostowanych na potrzeby rozsyłania komunikatów. |

Podsumowując nawet, jeśli przypadek użycia tylko hello jest przychodzący telemetrii urządzenia do chmury Centrum IoT udostępnia usługi, której celem jest łączność urządzenia IoT. Nadal tooexpand hello atrakcyjne oferty w tych scenariuszach z funkcji specyficznych dla IoT. Centra zdarzeń jest przeznaczona dla zdarzeń wejściowych w bardzo dużej skali, zarówno w kontekście hello między centrum danych i centrum danych wewnątrz scenariuszy.

Nie jest rzadko toouse zarówno Centrum IoT i centra zdarzeń w tym samym rozwiązaniu hello. Centrum IoT obsługuje komunikację urządzenia do chmury hello i usługi Event Hubs obsługuje zdarzenia późniejszym etapie ruch przychodzący do aparatami przetwarzania w czasie rzeczywistym.

### <a name="next-steps"></a>Następne kroki
toolearn więcej informacji na temat planowania wdrożenia Centrum IoT, zobacz [skalowanie, wysokiej dostępności i odzyskiwania po awarii][lnk-scaling].

toofurther Poznaj możliwości hello Centrum IoT, zobacz:

* [Przewodnik dewelopera Centrum IoT][lnk-devguide]
* [Symuluje urządzenia IoT krawędzi][lnk-iotedge]

[lnk-twins]: iot-hub-devguide-device-twins.md
[lnk-c2d-guidance]: iot-hub-devguide-c2d-guidance.md
[lnk-d2c-guidance]: iot-hub-devguide-d2c-guidance.md

[Azure Event Hubs]: ../event-hubs/event-hubs-what-is-event-hubs.md
[zabezpieczeń części hello Centrum IoT — przewodnik dewelopera]: iot-hub-devguide-security.md
[Event Hubs - security]: ../event-hubs/event-hubs-authentication-and-security-model-overview.md
[Event Hubs publisher policies]: ../event-hubs/event-hubs-features.md#event-publishers
[Azure Event Hubs quotas]: ../event-hubs/event-hubs-quotas.md
[Azure IoT SDKs]: https://github.com/Azure/azure-iot-sdks
[lnk-azure-protocol-gateway]: iot-hub-protocol-gateway.md

[lnk-scaling]: iot-hub-scaling.md
[lnk-devguide]: iot-hub-devguide.md
[lnk-iotedge]: iot-hub-linux-iot-edge-simulated-device.md
[lnk-devguide-messaging]: iot-hub-devguide-messaging.md
