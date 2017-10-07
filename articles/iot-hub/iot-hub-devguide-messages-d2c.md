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
# <a name="send-device-to-cloud-messages-tooiot-hub"></a>Wysyłanie wiadomości urządzenia do chmury tooIoT Centrum

dane telemetryczne szeregów czasowych toosend i alertów z Twojego urządzenia tooyour zaplecza rozwiązania, wysyłać urządzenia do chmury z Centrum IoT tooyour urządzenia. Omówienie opcji inne urządzenia do chmury, obsługiwanych przez Centrum IoT można znaleźć [wskazówki komunikację urządzenia do chmury][lnk-d2c-guidance].

Wysyłać urządzenia do chmury za pośrednictwem punktu końcowego uwzględniającym urządzenia (**/devices/ {deviceId} / wiadomości/zdarzenia**). Zasady routingu, a następnie kierować Twojej tooone wiadomości powitania połączonej usługi z punktów końcowych w Centrum IoT. Użyć reguły routingu hello nagłówki i treści wiadomości powitania od urządzenia do chmury przepływających przez toodetermine Twojego Centrum gdzie tooroute je. Domyślnie komunikaty są routingiem toohello wbudowanym punktem końcowym usługi połączonej (**wiadomości/zdarzenia**), która jest zgodna z [usługi Event Hubs][lnk-event-hubs]. W takim przypadku używane standardowe [integracji usługi Event Hubs i zestawy SDK] [ lnk-compatible-endpoint] tooreceive wiadomości urządzenia do chmury w rozwiązaniu zaplecza.

Centrum IoT implementuje wiadomości urządzenia do chmury przy użyciu przesyłania strumieniowego wzorzec przesyłania komunikatów. Przypominają komunikaty urządzenia do chmury Centrum IoT [usługi Event Hubs] [ lnk-event-hubs] *zdarzenia* niż [usługi Service Bus] [ lnk-servicebus] *wiadomości* w tym istnieje duża liczba zdarzeń przekazywanie za pośrednictwem usługi hello, który może zostać odczytany przez wielu czytników.

Wiadomości z Centrum IoT urządzenia do chmury ma hello następujące cechy:

* Urządzenia do chmury wiadomości są trwałe i zachowanych w Centrum IoT domyślne **wiadomości/zdarzenia** punktu końcowego dla się tooseven dni.
* Komunikaty urządzenia do chmury może mieć maksymalnie 256 KB i można grupować w partiach, który wysyła toooptimize. Partie może mieć maksymalnie 256 KB.
* Zgodnie z objaśnieniem w hello [kontroli dostępu tooIoT Centrum] [ lnk-devguide-security] sekcji Centrum IoT umożliwia na urządzenie uwierzytelniania i kontroli dostępu.
* Centrum IoT umożliwia toocreate się too10 niestandardowe punkty końcowe. Wiadomości są dostarczane punkty końcowe toohello oparte na trasach skonfigurowany w Centrum IoT. Aby uzyskać więcej informacji, zobacz [reguły routingu](#routing-rules).
* Centrum IoT umożliwia miliony równocześnie połączonych urządzeń (zobacz [przydziały i ograniczenia przepustowości][lnk-quotas]).
* Centrum IoT nie zezwala na dowolne partycjonowania. Urządzenia do chmury wiadomości są dzielone na podstawie ich źródłowych **deviceId**.

Aby uzyskać więcej informacji o różnicach hello hello Centrum IoT i usługi Event Hubs, zobacz [porównania Azure IoT Hub i usługi Azure Event Hubs][lnk-comparison].

## <a name="send-non-telemetry-traffic"></a>Wysyłaj ruch z systemem innym niż telemetrii

Często oprócz punktów danych tootelemetry, urządzenia wysyłają komunikaty i żądania, które wymagają obsługi w wewnętrznej hello rozwiązania i wykonywania oddzielnych. Na przykład alerty krytyczne musi wyzwalających określonego działania w hello zaplecza. Możesz łatwo zapisywać [reguły routingu] [ lnk-devguide-custom] toosend tootheir przetwarzanie na podstawie nagłówek wiadomości powitania lub wartością w treści wiadomości powitania dedykowanego tych typów punktu końcowego tooan wiadomości.

Aby uzyskać więcej informacji na temat hello najlepsze sposób tooprocess tego rodzaju wiadomości, zobacz hello [samouczek: jak tooprocess Centrum IoT urządzenia do chmury wiadomości] [ lnk-d2c-tutorial] samouczka.

## <a name="route-device-to-cloud-messages"></a>Rozsyłanie wiadomości urządzenia do chmury

Masz dwie opcje dla routingu wiadomości urządzenia do chmury tooyour zaplecza aplikacji:

* Użyj wbudowanego hello [punktu końcowego Centrum zdarzeń zgodnych] [ lnk-compatible-endpoint] tooenable zaplecza aplikacji tooread hello urządzenia do chmury komunikatów odebranych przez hello koncentratora. toolearn o hello wbudowanym punktem końcowym zgodnego Centrum zdarzeń, zobacz [odczytywać wiadomości urządzenia do chmury z wbudowanym punktem końcowym hello][lnk-devguide-builtin].
* Użyj routingu reguły toosend wiadomości toocustom punktów końcowych w Centrum IoT. Niestandardowe punkty końcowe Włącz wiadomości urządzenia do chmury tooread zaplecza aplikacji za pomocą usługi Event Hubs, kolejek usługi Service Bus lub tematów usługi Service Bus. Zobacz toolearn o routingu i niestandardowe punkty końcowe [Użyj niestandardowe punkty końcowe i reguły routingu dla komunikatów urządzenia do chmury][lnk-devguide-custom].

## <a name="anti-spoofing-properties"></a>Ochrona przed fałszowaniem właściwości

urządzenie tooavoid fałszowania w komunikatach urządzenia do chmury, Centrum IoT sygnatury wszystkie komunikaty z hello następujące właściwości:

* **ConnectionDeviceId**
* **ConnectionDeviceGenerationId**
* **ConnectionAuthMethod**

Witaj dwie zawierać hello **deviceId** i **generationId** z hello pochodzące z urządzenia, zgodnie [właściwości tożsamości urządzenia][lnk-device-properties].

Witaj **ConnectionAuthMethod** właściwość zawiera obiekt Zserializowany do postaci JSON z hello następujące właściwości:

```json
{
  "scope": "{ hub | device}",
  "type": "{ symkey | sas}",
  "issuer": "iothub"
}
```

## <a name="next-steps"></a>Następne kroki

Informacji o zestawów SDK hello toosend urządzenia do chmury komunikatów, zobacz [Azure IoT SDK][lnk-sdks].

Witaj [wprowadzenie] [ lnk-get-started] samouczki wyjaśniają, jak komunikaty toosend urządzenia do chmury z zarówno symulowane, jak i fizycznych urządzeń. Aby uzyskać więcej szczegółów, zobacz hello [Centrum IoT procesu wiadomości urządzenia do chmury, za pomocą trasy] [ lnk-d2c-tutorial] samouczka.

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
