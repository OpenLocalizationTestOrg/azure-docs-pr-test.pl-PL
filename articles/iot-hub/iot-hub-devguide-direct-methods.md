---
title: "aaaUnderstand Centrum IoT Azure bezpośrednie metody | Dokumentacja firmy Microsoft"
description: "Przewodnik dewelopera — użyj metody bezpośredniego tooinvoke kodu na urządzeniach z usługi aplikacji."
services: iot-hub
documentationcenter: .net
author: nberdy
manager: timlt
editor: 
ms.assetid: 9f0535f1-02e6-467a-9fc4-c0950702102d
ms.service: iot-hub
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/25/2017
ms.author: nberdy
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 0d15d44a0c3e1d1cda1669c1ed011c2f932e3d92
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="understand-and-invoke-direct-methods-from-iot-hub"></a>Informacje o funkcji i wywołanie metody bezpośrednio z Centrum IoT
## <a name="overview"></a>Omówienie
Centrum IoT umożliwia bezpośrednie metody tooinvoke możliwości na urządzeniach z hello chmury. Bezpośrednie metody reprezentują interakcji żądanie odpowiedź z urządzenia tooan podobne, wywołaj HTTP, w tym ich powodzenie lub niepowodzenie natychmiast (po limitu określonego przez użytkownika). Jest to przydatne w scenariuszach, w którym hello przebiegu natychmiastowego działania różni się w zależności od tego, czy urządzenie hello było możliwe toorespond, takie jak wysyłanie SMS tooa wznawiania urządzenia, jeśli urządzenie jest w trybie offline (SMS są droższe niż wywołania metody).

Każda metoda urządzenia jest przeznaczony dla jednego urządzenia. [Zadania] [ lnk-devguide-jobs] podania tooinvoke sposób bezpośredniego metod na wielu urządzeniach i Zaplanuj wywołania metody odłączone urządzenia.

Każda osoba mająca **usługa połączyć** uprawnień w Centrum IoT mogą wywołać metodę na urządzeniu.

### <a name="when-toouse"></a>Gdy toouse
Bezpośrednie metody wykonaj wzorzec żądań i odpowiedzi i są przeznaczone do komunikacji, które wymagają natychmiastowego potwierdzenia ich wyniku sterowania zwykle interaktywnego hello urządzenia, na przykład tooturn na wentylatora.

Odwołuje się zbyt[wskazówki dotyczące komunikacji chmury do urządzenia] [ lnk-c2d-guidance] w razie wątpliwości między przy użyciu żądanej właściwości, bezpośrednie metod lub komunikaty chmury do urządzenia.

## <a name="method-lifecycle"></a>Cykl życia — metoda
Bezpośrednie metody są wdrożone na urządzeniu hello i może wymagać zero lub więcej danych wejściowych w toocorrectly ładunku metody hello wystąpienia. Wywołaj metodę bezpośrednio za pomocą identyfikatora URI usługi połączonej (`{iot hub}/twins/{device id}/methods/`). Urządzenie odbiera metody bezpośredniego za pośrednictwem tematu MQTT specyficzne dla urządzenia (`$iothub/methods/POST/{method name}/`). Firma Microsoft może obsługiwać bezpośredniego metody na dodatkowych protokołów sieciowych po stronie urządzenia w przyszłości hello.

> [!NOTE]
> Po wywołaniu metody bezpośrednio na urządzeniu, nazwy i wartości właściwości mogą zawierać tylko US-ASCII drukowalnych alfanumeryczne, z wyjątkiem tych w hello następującego zestawu: ``{'$', '(', ')', '<', '>', '@', ',', ';', ':', '\', '"', '/', '[', ']', '?', '=', '{', '}', SP, HT}``.
> 
> 

Bezpośrednie metody są synchroniczne i albo pomyślnie lub niepowodzeniem hello limit czasu, po (domyślne: 30 sekund, można ustawić w górę too3600 sekund). Bezpośrednie metody są przydatne w scenariuszach interakcyjne miejscu tooact urządzenia tylko wtedy, gdy urządzenie hello jest online i odbierania poleceń, jak włączenie światła przez telefon. W tych scenariuszach ma toosee natychmiastowego powodzenie lub niepowodzenie, usługa w chmurze hello może działać na powitania wyniku tak szybko, jak to możliwe. Hello urządzenie może zwrócić niektóre treści wiadomości wyniku metody hello, ale nie jest wymagane dla toodo metody hello tak. Brak żadnej gwarancji, w kolejności lub dowolnego semantyki współbieżności na wywołania metody.

Metoda bezpośrednia są tylko po stronie chmury hello HTTP i MQTT tylko z hello urządzenia strony.

ładunek Hello metod żądań i odpowiedzi jest too8KB dokumentu JSON.

## <a name="reference-topics"></a>Tematy odwołań:
Witaj następujące tematy dokumentacji zapewniają więcej informacji na temat przy użyciu metod bezpośredniego.

## <a name="invoke-a-direct-method-from-a-back-end-app"></a>Wywoływanie metody bezpośrednio z aplikacji zaplecza
### <a name="method-invocation"></a>Wywołanie metody
Bezpośrednie wywołania metod na urządzeniu są połączenia HTTP, które obejmują:

* Witaj *URI* toohello określonego urządzenia (`{iot hub}/twins/{device id}/methods/`)
* Witaj POST *— metoda*
* *Nagłówki* które zawiera hello autoryzacji, żądania Identyfikatora, typu zawartości i kodowania zawartości
* Przezroczysty JSON *treści* w hello następującego formatu:

```
{
    "methodName": "reboot",
    "responseTimeoutInSeconds": 200,
    "payload": {
        "input1": "someInput",
        "input2": "anotherInput"
    }
}
```

Jest limit czasu w sekundach. Jeśli nie ustawiono limit czasu, domyślnie przyjmowana too30 sekund.

### <a name="response"></a>Odpowiedź
Witaj zaplecza aplikacji otrzymuje odpowiedzi, która obejmuje:

* *Kod stanu HTTP*, używany błędy pochodzące z hello Centrum IoT, łącznie z błędem 404 dla urządzeń nie jest obecnie połączony
* *Nagłówki* które zawierają hello ETag, żądania Identyfikatora, typu zawartości i kodowania zawartości
* JSON *treści* w hello następującego formatu:

```
{
    "status" : 201,
    "payload" : {...}
}
```

   Zarówno `status` i `body` są dostarczane przez hello urządzenie i użyć toorespond z kodem stanu dla urządzenia hello i/lub opis.

## <a name="handle-a-direct-method-on-a-device"></a>Dojście metody bezpośrednio na urządzeniu
### <a name="method-invocation"></a>Wywołanie metody
Urządzenia odbierania żądań metoda bezpośrednia na temat MQTT hello:`$iothub/methods/POST/{method name}/?$rid={request id}`

urządzenia, które hello odbiera treści Hello znajduje się w hello następującego formatu:

```
{
    "input1": "someInput",
    "input2": "anotherInput"
}
```

Metoda żądania są QoS 0.

### <a name="response"></a>Odpowiedź
urządzenie Hello wysyła odpowiedzi zbyt`$iothub/methods/res/{status}/?$rid={request id}`, gdzie:

* Witaj `status` właściwość jest hello dostarczone przez urządzenie stan wykonywania metody.
* Witaj `$rid` właściwość jest identyfikator żądania powitania od wywołania metody hello odebranych z Centrum IoT.

Treść Hello jest ustawiana przez urządzenie hello i może być dowolnym stanie.

## <a name="additional-reference-material"></a>Odwołanie dodatkowe materiały
Inne tematy referencyjne w hello Centrum IoT — przewodnik dewelopera obejmują:

* [Punkty końcowe Centrum IoT] [ lnk-endpoints] opisuje hello różnych punktów końcowych, które udostępnia każdego centrum IoT dla operacji zarządzania i środowiska wykonawczego.
* [Ograniczenia przepustowości i przydziały] [ lnk-quotas] opisuje przydziały hello, stosowane toohello usługi IoT Hub, które hello ograniczania tooexpect zachowanie, gdy używasz usługi hello.
* [Zestawy Azure IoT urządzenia i usługi SDK] [ lnk-sdks] list hello języka różnych zestawów SDK, można użyć podczas opracowywania aplikacji usług i urządzeń, które współdziałają z Centrum IoT.
* [Język zapytań Centrum IoT urządzenia twins, zadań i rozsyłania wiadomości] [ lnk-query] opisuje hello tooretrieve informacji z Centrum IoT temat zadań i twins urządzenia można używać języka kwerend Centrum IoT.
* [Obsługa MQTT Centrum IoT] [ lnk-devguide-mqtt] zamieszczono więcej informacji o obsłudze Centrum IoT hello MQTT protokołu.

## <a name="next-steps"></a>Następne kroki
Teraz wiesz już, jak toouse metody bezpośredniego, może Cię zainteresować hello kolejny temat przewodnik dewelopera Centrum IoT:

* [Planowanie zadań na wielu urządzeniach][lnk-devguide-jobs]

Jeśli chcesz tootry niektórych hello pojęcia opisane w tym artykule, mogą być zainteresowane hello samouczka Centrum IoT:

* [Użyj metody bezpośredniego][lnk-methods-tutorial]

<!-- links and images -->

[lnk-endpoints]: iot-hub-devguide-endpoints.md
[lnk-quotas]: iot-hub-devguide-quotas-throttling.md
[lnk-sdks]: iot-hub-devguide-sdks.md
[lnk-query]: iot-hub-devguide-query-language.md
[lnk-devguide-mqtt]: iot-hub-mqtt-support.md

[lnk-devguide-jobs]: iot-hub-devguide-jobs.md
[lnk-methods-tutorial]: iot-hub-node-node-direct-methods.md
[lnk-devguide-messages]: iot-hub-devguide-messaging.md
[lnk-c2d-guidance]: iot-hub-devguide-c2d-guidance.md
