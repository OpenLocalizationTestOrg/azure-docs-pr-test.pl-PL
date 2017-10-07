---
title: "aaaUnderstand chmury urządzenia Centrum IoT Azure messaging | Dokumentacja firmy Microsoft"
description: "Przewodnik dewelopera — jak toouse chmury do urządzenia z Centrum IoT do obsługi komunikatów. Zawiera informacje na temat cyklu życia wiadomość hello i opcje konfiguracji."
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
ms.openlocfilehash: 5c747b50163873d823556a8baa769c4b8f7f8c44
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="send-cloud-to-device-messages-from-iot-hub"></a>Wysyłanie wiadomości chmury do urządzenia z Centrum IoT

toosend jednokierunkowe powiadomienia toohello urządzenia aplikacji z Twojej zaplecza rozwiązania, wysyłania wiadomości chmury do urządzenia z urządzenia tooyour Centrum IoT. Omówienie innych opcji chmury do urządzeń obsługiwanych przez Centrum IoT można znaleźć [wskazówki dotyczące komunikacji chmury do urządzenia][lnk-c2d-guidance].

Wysyłanie wiadomości chmury do urządzenia za pośrednictwem punktu końcowego usługi połączonej (**/wiadomości/devicebound**). Urządzenie otrzyma wiadomości powitania za pośrednictwem punktu końcowego specyficzne dla urządzenia (**/devices/ {deviceId} / wiadomości/devicebound**).

Każdy komunikat chmury do urządzenia jest wskazywane na jednym urządzeniu przez ustawienie hello **do** właściwości zbyt**/devices/ {deviceId} / wiadomości/devicebound**.

Każda kolejka urządzenia zawiera maksymalnie 50 wiadomości chmury do urządzenia. Więcej wiadomości toohello toosend w trakcie tego samego urządzenia powoduje błąd.

## <a name="hello-cloud-to-device-message-lifecycle"></a>Witaj cykl życia komunikatów chmury do urządzenia

dostarczanie komunikatów w najmniej jednokrotne tooguarantee, Centrum IoT utrzymuje chmury do urządzenia komunikatów w kolejkach na urządzenie. Urządzenia musi jawnie potwierdzić *zakończenia* dla Centrum IoT tooremove hello je z kolejki. Ta metoda gwarantuje odporność na błędy urządzenia i łączności.

Witaj Poniższy diagram przedstawia wykres stanu cyklu życia hello komunikatu chmura urządzenie w Centrum IoT.

![Cykl życia komunikatów chmury do urządzenia][img-lifecycle]

Gdy hello usługi IoT Hub wysyła komunikat tooa urządzenia, usługa hello ustawia stan wiadomość hello zbyt**umieszczonych w kolejce**. Gdy urządzenie potrzebuje zbyt*odbierania* komunikat Centrum IoT *blokad* wiadomość hello (przez ustawienie stanu hello zbyt**niewidoczne**), co pozwala na powitania urządzenia toostart inne wątki odbieranie inne komunikaty. Po zakończeniu przetwarzania wiadomość hello wątku urządzenia powiadomi Centrum IoT przez *Kończenie* wiadomość hello. Centrum IoT następnie ustawia stan hello zbyt**Ukończono**.

Urządzenia można także wybrać opcję:

* *Odrzuć* wiadomość hello, co powoduje, że Centrum IoT tooset on toohello **Deadlettered** stanu. Urządzeń łączących się za pośrednictwem protokołu MQTT hello nie można odrzucić wiadomości chmury do urządzenia.
* *Porzuć* wiadomość hello, co powoduje, że Centrum IoT wiadomość hello tooput w kolejce hello ze stanem hello ustawić także**umieszczonych w kolejce**.

Wątek może funkcjonować w trybie tooprocess wiadomość bez powiadamiania Centrum IoT. W takim przypadku komunikaty automatycznie przejście od hello **niewidoczne** toohello wstecz stanu **umieszczonych w kolejce** stanu po *limitu czasu widoczności (lub blokowania)*. Wartość domyślna Hello tego limitu czasu jest jedna minuta.

Komunikat może przejść między hello **umieszczonych w kolejce** i **niewidoczne** stanów, co najwyżej hello liczba powtórzeń w hello **maksymalna liczba dostarczania** właściwość Centrum IoT. Po liczby przejść, Centrum IoT ustawia stan hello wiadomość hello zbyt**Deadlettered**. Podobnie, Centrum IoT ustawia stan wiadomość hello zbyt**Deadlettered** po godzinie wygaśnięcia (zobacz [czasu toolive][lnk-ttl]).

Witaj [jak komunikaty toosend chmury do urządzenia z Centrum IoT] [ lnk-c2d-tutorial] pokazano, jak toosend chmury do urządzenia wiadomości powitania w chmurze oraz ich odbierania na urządzeniu.

Zazwyczaj urządzenia wypełnia komunikat chmury do urządzenia, gdy hello wiadomości powitania nie wpływa na powitania logiki aplikacji. Na przykład jeśli urządzenia hello utrwalił zawartość wiadomość hello lokalnie lub została pomyślnie wykonana operacja. wiadomość Hello może również zawierać informacje przejściowy, w których utraty nie będzie wpływ na funkcje hello aplikacji hello. Czasami długotrwałych zadań, możesz ukończyć wiadomości powitania chmury do urządzenia po trwałym hello opis zadania w magazynie lokalnym. Następnie na różnych etapach postęp zadania hello można powiadomić hello zaplecza rozwiązania z jednego lub więcej komunikatów urządzenia do chmury.

## <a name="message-expiration-time-toolive"></a>Wygaśnięcia wiadomości (czas toolive)

Każdy komunikat chmury do urządzenia ma czasu wygaśnięcia. Ten czas jest ustawiony przez hello usługi (w hello **ExpiryTimeUtc** właściwości), lub przez Centrum IoT przy użyciu domyślnego hello *czasu toolive* określony jako właściwość Centrum IoT. Zobacz [opcje konfiguracji chmury do urządzenia][lnk-c2d-configuration].

Typowe sposób tootake zaletą komunikatu wygaśnięcia i unikanie wysyłania wiadomości toodisconnected urządzeń, jest tooset wartości toolive krótki czas. Takie podejście osiąga hello spowodować takie same jako zachowanie stanu połączenia urządzenia hello, będąc bardziej wydajne. W przypadku żądania potwierdzeń wiadomości, Centrum IoT powiadamia, urządzeń, które są komunikaty o stanie tooreceive i urządzeń, które nie są w trybie online lub nie powiodło się.

## <a name="message-feedback"></a>Komunikat opinii

Po wysłaniu komunikatu chmura urządzenie hello usługi mogą żądać hello dostarczania wiadomości informacji dotyczących stanu końcowego hello tej wiadomości.

| Właściwość ACK. | Zachowanie |
| ------------ | -------- |
| **dodatnią** | Centrum IoT generuje komunikat opinii w przypadku i tylko wtedy, gdy hello chmury do urządzenia wiadomość dotarła hello **Ukończono** stanu. |
| **ujemna** | Centrum IoT generuje komunikat opinii, tylko wtedy, gdy, wiadomości powitania chmury do urządzenia osiągnie hello **Deadlettered** stanu. |
| **Pełna**     | Centrum IoT generuje komunikat opinii w każdym przypadku. |

Jeśli **potwierdzenia** jest **pełne**i nie zostanie wyświetlony komunikat opinii, oznacza to, tym wiadomość hello wygasł. Usługa Hello nie wiadomo, jakie wystąpiły toohello oryginalnej wiadomości. W praktyce usługi powinien upewnić, że opinii hello może przetworzyć przed jej wygaśnięciem. czas wygaśnięcia maksymalną Hello jest dwa dni, który zapewnia dużo czasu tooget hello uruchomiona ponownie, jeśli wystąpi błąd.

Zgodnie z objaśnieniem w [punkty końcowe][lnk-endpoints], Centrum IoT zapewnia informacje zwrotne przez punkt końcowy usługi połączonej (**/messages/servicebound/feedback**) jako wiadomości. Hello semantyki wysyłania opinii dla są hello takie same jak w przypadku wiadomości chmury do urządzenia i mieć takie same hello [cykl życia komunikatów][lnk-lifecycle]. Jeśli to możliwe, opinii komunikat jest przetwarzany wsadowo w pojedynczym komunikacie z hello następującego formatu:

| Właściwość     | Opis |
| ------------ | ----------- |
| EnqueuedTime | Sygnatura czasowa wskazująca, kiedy wiadomość hello została utworzona. |
| Nazwa użytkownika       | `{iot hub name}` |
| Typ zawartości  | `application/vnd.microsoft.iothub.feedback.json` |

Treść Hello jest serializacji JSON tablicą rekordów, każde z nich hello następujące właściwości:

| Właściwość           | Opis |
| ------------------ | ----------- |
| EnqueuedTimeUtc    | Sygnatura czasowa wskazująca, kiedy wystąpił hello wyniku wiadomość hello. Na przykład Witaj urządzenia zakończone lub wiadomość hello wygasł. |
| originalMessageId  | **Identyfikator komunikatu** toowhich chmury do urządzenia wiadomość hello dotyczy tej opinii. |
| statusCode         | Wymagany ciąg. Używane w opinii komunikaty generowane przez Centrum IoT. <br/> 'Success' <br/> "Wygasł" <br/> "DeliveryCountExceeded" <br/> "Odrzucone" <br/> "Usunięte" |
| Opis        | Ciąg wartości **StatusCode**. |
| Identyfikator urządzenia           | **DeviceId** z urządzeniem docelowym hello toowhich chmury do urządzenia wiadomość hello odnosi się ten element opinii. |
| DeviceGenerationId | **DeviceGenerationId** z urządzeniem docelowym hello toowhich chmury do urządzenia wiadomość hello odnosi się ten element opinii. |

należy określić Hello usługi **MessageId** dla hello chmury do urządzenia komunikatów toocorrelate stanie toobe jego opinii z oryginalnej wiadomości powitania.

Witaj poniższy przykład przedstawia wiadomość hello treści.

```json
[
  {
    "OriginalMessageId": "0987654321",
    "EnqueuedTimeUtc": "2015-07-28T16:24:48.789Z",
    "StatusCode": 0,
    "Description": "Success",
    "DeviceId": "123",
    "DeviceGenerationId": "abcdefghijklmnopqrstuvwxyz"
  },
  {
    ...
  },
  ...
]
```

## <a name="cloud-to-device-configuration-options"></a>Opcje konfiguracji chmury do urządzenia

Każdy Centrum IoT udostępnia następujące opcje konfiguracji chmury do urządzenia wiadomości powitania:

| Właściwość                  | Opis | Zakres i domyślne |
| ------------------------- | ----------- | ----------------- |
| defaultTtlAsIso8601       | Domyślny czas wygaśnięcia wiadomości chmury do urządzenia. | Interwał ISO_8601 się too2D (minimalna 1 minuta). Wartość domyślna: 1 godzina. |
| maxDeliveryCount          | Liczba maksymalna dostarczania dla kolejek chmury do urządzenia na urządzeniu. | 1 too100. Domyślny: 10. |
| feedback.ttlAsIso8601     | Przechowywanie komunikatów usługi powiązane z opinii. | Interwał ISO_8601 się too2D (minimalna 1 minuta). Wartość domyślna: 1 godzina. |
| feedback.maxDeliveryCount |Liczba maksymalna dostarczania dla kolejki opinii. | 1 too100. Domyślnie: 100. |

Aby uzyskać więcej informacji na temat tooset tych opcji konfiguracji, zobacz temat [centra IoT utworzyć][lnk-portal].

## <a name="next-steps"></a>Następne kroki

Informacje o hello zestawów SDK tooreceive komunikatów chmury do urządzenia, zobacz [Azure IoT SDK][lnk-sdks].

tootry limit odbieranie komunikatów z chmury do urządzenia, zobacz hello [wysyłania chmury do urządzenia] [ lnk-c2d-tutorial] samouczka.

[img-lifecycle]: ./media/iot-hub-devguide-messages-c2d/lifecycle.png

[lnk-portal]: iot-hub-create-through-portal.md
[lnk-c2d-guidance]: iot-hub-devguide-c2d-guidance.md
[lnk-endpoints]: iot-hub-devguide-endpoints.md
[lnk-sdks]: iot-hub-devguide-sdks.md
[lnk-ttl]: #message-expiration-time-to-live
[lnk-c2d-configuration]: #cloud-to-device-configuration-options
[lnk-lifecycle]: #message-lifecycle
[lnk-c2d-tutorial]: iot-hub-csharp-csharp-c2d.md
