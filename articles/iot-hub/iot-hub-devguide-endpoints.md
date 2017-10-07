---
title: "punkty końcowe Centrum IoT Azure aaaUnderstand | Dokumentacja firmy Microsoft"
description: "Przewodnik dewelopera — informacje na temat Centrum IoT punkty końcowe skierowane do urządzenia i połączonej usługi."
services: iot-hub
documentationcenter: .net
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 57ba52ae-19c6-43e4-bc6c-d8a5c2476e95
ms.service: iot-hub
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/08/2017
ms.author: dobett
ms.openlocfilehash: 8647f15d2f2a050ad5799ea82f4d2d46db0dbec1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="reference---iot-hub-endpoints"></a>Odwołanie — punkty końcowe Centrum IoT

## <a name="iot-hub-names"></a>Nazwy Centrum IoT

Można znaleźć hello nazwę Centrum IoT hello obsługującego punktów końcowych w portalu hello na powitania **omówienie** bloku. Domyślnie nazwa DNS hello Centrum IoT wygląda następująco: `{your iot hub name}.azure-devices.net`.

Możesz użyć usługi Azure DNS toocreate niestandardową nazwę DNS Centrum IoT. Aby uzyskać więcej informacji, zobacz [ustawienia domeny niestandardowej tooprovide użycia usługi Azure DNS dla usługi Azure](../dns/dns-custom-domain.md#azure-iot).

## <a name="list-of-built-in-iot-hub-endpoints"></a>Lista wbudowanych punkty końcowe Centrum IoT

Centrum IoT Azure to usługa wielodostępne, która przedstawia podmiotów toovarious jego funkcjonalność. Witaj Poniższy diagram przedstawia hello różnych punktów końcowych, które udostępnia Centrum IoT.

![Punkty końcowe centrum IoT Hub][img-endpoints]

następujące listy Hello opisano hello punktów końcowych:

* **Dostawca zasobów**. Witaj Centrum IoT dostawca zasobów udostępnia [usługi Azure Resource Manager] [ lnk-arm] interfejsu. Ten interfejs umożliwia toocreate właściciele subskrypcji platformy Azure i usuwanie centra IoT i właściwości Centrum IoT tooupdate. Centrum IoT właściwości regulują [zasad zabezpieczeń na poziomie koncentratora][lnk-accesscontrol], w przeciwieństwie do kontroli dostępu na poziomie toodevice i funkcjonalności opcji chmury do urządzenia i urządzenia do chmury do obsługi komunikatów. Witaj dostawcy zasobów Centrum IoT można również zbyt[wyeksportować tożsamości urządzenia][lnk-importexport].
* **Zarządzanie tożsamościami urządzenia**. Każdy Centrum IoT udostępnia zestaw tożsamości urządzenia toomanage punkty końcowe REST protokołu HTTP (Tworzenie, pobieranie, aktualizowanie i usuwanie). [Tożsamości urządzenia] [ lnk-device-identities] służą do urządzenia uwierzytelniania i kontroli dostępu.
* **Zarządzanie urządzeniami dwie**. Każdy Centrum IoT udostępnia zestaw tooquery punkt końcowy REST protokołu HTTP i aktualizacji usługi połączonej [twins urządzenia] [ lnk-twins] (aktualizacja znaczniki i właściwości).
* **Zadania zarządzania**. Każdy Centrum IoT udostępnia zestaw tooquery punkt końcowy REST protokołu HTTP skierowane do usługi i zarządzanie nimi [zadania][lnk-jobs].
* **Punkty końcowe urządzenia**. Dla każdego urządzenia w rejestrze tożsamości hello Centrum IoT udostępnia zestaw punktów końcowych:

  * *Wysyłanie komunikatów urządzenia do chmury*. Urządzenie korzysta z tego punktu końcowego za[wysyłać urządzenia do chmury][lnk-d2c].
  * *Komunikaty chmury do urządzenia*. Urządzenie korzysta z tego tooreceive punktu końcowego docelowe [wiadomości chmury do urządzenia][lnk-c2d].
  * *Zainicjuj przekazywania plików*. Urządzenie korzysta z tego punktu końcowego tooreceive Azure magazynu identyfikatora URI połączenia SAS z Centrum IoT zbyt[przekazać plik][lnk-upload].
  * *Pobierania i aktualizowania urządzenia dwie właściwości*. Urządzenie korzysta z tego punktu końcowego tooaccess jego [dwie urządzenia][lnk-twins]jego właściwości.
  * *Odbierania żądań metoda bezpośrednia*. Urządzenie korzysta z tego punktu końcowego toolisten dla [metoda bezpośrednia][lnk-methods]tego żądania.

    Te punkty końcowe są udostępniane za pomocą [MQTT v3.1.1][lnk-mqtt], protokołu HTTP 1.1 i [protokołu AMQP 1.0] [ lnk-amqp] protokołów. Jest również dostępny za pośrednictwem protokołu AMQP [Websocket] [ lnk-websockets] na porcie 443.

    Witaj urządzenia twins i metody punkty końcowe są dostępne tylko wtedy, gdy używasz hello [MQTT v3.1.1] [ lnk-mqtt] protokołu.

* **Punkty końcowe usługi**. Każdy Centrum IoT udostępnia zestaw punktów końcowych dla sieci toocommunicate zaplecza rozwiązania dotyczące urządzeń z systemem. Z jednym wyjątkiem te punkty końcowe są dostępne tylko za pomocą hello [AMQP] [ lnk-amqp] protokołu. punkt końcowy wywołania metody Hello jest uwidaczniany za pośrednictwem hello protokołu HTTP.
  
  * *Komunikaty urządzenia do chmury*. Ten punkt końcowy jest zgodny z [Azure Event Hubs][lnk-event-hubs]. Usługi zaplecza może być używany tooread hello [wiadomości urządzenia do chmury] [ lnk-d2c] wysyłanych przez urządzenia. Możesz utworzyć niestandardowe punkty końcowe w Centrum IoT w dodanie toothis wbudowanym punktem końcowym.
  * *Chmury do urządzenia wysyłać i odbierać potwierdzeń dostarczenia*. Te punkty końcowe włączyć Twojej niezawodne rozwiązanie zaplecza toosend [wiadomości chmury do urządzenia][lnk-c2d], i tooreceive hello odpowiedniego potwierdzeń dostarczenia lub wygaśnięcia.
  * *Odbieranie powiadomień pliku*. Tego obsługi komunikatów punktu końcowego umożliwia tooreceive powiadomienia o urządzeniach udało się przekazać pliku. 
  * *Bezpośrednie wywołania metody*. Ten punkt końcowy pozwala tooinvoke usługi zaplecza [metoda bezpośrednia] [ lnk-methods] na urządzeniu.
  * *Monitorowanie zdarzeń operacji odbioru*. Ten punkt końcowy pozwala operacji tooreceive monitorowanie zdarzeń skonfigurowanie tooemit Twojego IoT koncentrator został je. Aby uzyskać więcej informacji, zobacz [operacji centrum IoT monitorowania][lnk-operations-mon].

Witaj [Azure IoT SDK] [ lnk-sdks] artykule hello różne sposoby tooaccess tymi punktami końcowymi.

Wszystkie punkty końcowe Centrum IoT Użyj hello [TLS] [ lnk-tls] protokołu i żaden punkt końcowy kiedykolwiek jest uwidaczniana w postaci niezaszyfrowanej niezabezpieczone kanałach.

## <a name="custom-endpoints"></a>Niestandardowe punkty końcowe

Możesz połączyć istniejące usługi platformy Azure w Twojej subskrypcji tooyour IoT hub tooact jako punktów końcowych do rozsyłania wiadomości. Te punkty końcowe działać jako punkty końcowe usługi i są używane jako wychwytywanie tras wiadomości. Urządzenia nie można zapisać bezpośrednio toohello dodatkowe punkty końcowe. toolearn więcej informacji na temat tras wiadomości, zobacz wpis przewodnik dewelopera hello na [wysyłanie i odbieranie komunikatów z Centrum IoT][lnk-devguide-messaging].

Centrum IoT obsługuje obecnie następujących usług platformy Azure jako dodatkowe punkty końcowe hello:

* Usługa Event Hubs
* Kolejki usługi Service Bus
* Tematy dotyczące usługi Service Bus

Centrum IoT potrzebuje punktów końcowych usługi toothese zapisu komunikatu toowork routingu. Skonfiguruj punkty końcowe za pośrednictwem portalu Azure hello, hello niezbędne uprawnienia zostaną dodane automatycznie. Upewnij się, że należy skonfigurować przepływności hello oczekiwano toosupport Twojego usług. Podczas pierwszej konfiguracji rozwiązania IoT, mogą muszą toomonitor dodatkowych punktów końcowych i wprowadź wymagane zmiany hello rzeczywistego obciążenia.

Jeśli wiele tras, że wszystkie punktu toohello dopasuje komunikat o stanie tego samego punktu końcowego Centrum IoT zapewnia końcowy toothat komunikatu tylko raz. W związku z tym czynności nie potrzeba tooconfigure deduplikacji na kolejki usługi Service Bus lub tematu. W kolejkach podzielonym na partycje koligacji partycji gwarantuje porządkowania wiadomości.

> [!NOTE]
> Tematy dotyczące używany jako punkty końcowe Centrum IoT nie może mieć i kolejek usługi Service Bus **sesji** lub **wykrywania duplikatów** włączone. Jeśli dowolna z tych opcji są włączone, hello punkt końcowy jest wyświetlany jako **informujący** w hello portalu Azure.

Witaj limitów liczby hello punkty końcowe można dodać, zobacz [przydziały i ograniczenia przepustowości][lnk-devguide-quotas].

## <a name="field-gateways"></a>Pole bram

Rozwiązania IoT *bramy pola* znajduje się między urządzeniami a punktami końcowymi Centrum IoT. Jest zwykle tooyour Zamknij urządzeń. Urządzenia bezpośredniego komunikowania się z hello pola bramy przy użyciu protokołu obsługiwanego przez hello urządzenia. Brama pola Hello łączy tooan punktu końcowego Centrum IoT przy użyciu protokołu, który jest obsługiwany przez Centrum IoT. Brama pole może być dedykowanym urządzeniem sprzętowym lub niskiego poboru energii komputer z oprogramowaniem bram.

Można użyć [Azure IoT krawędzi] [ lnk-iot-edge] tooimplement bramy pola. Krawędź IoT oferuje funkcje, takie jak Multipleksowanie komunikację z wielu urządzeń na powitania tego samego połączenia Centrum IoT.

## <a name="next-steps"></a>Następne kroki

Inne tematy dokumentacji, w tym przewodniku deweloperów Centrum IoT obejmują:

* [Język zapytań Centrum IoT urządzenia twins, zadań i rozsyłania wiadomości][lnk-devguide-query]
* [Przydziały i ograniczenia przepustowości][lnk-devguide-quotas]
* [Obsługa MQTT Centrum IoT][lnk-devguide-mqtt]

[lnk-iot-edge]: https://github.com/Azure/iot-edge

[img-endpoints]: ./media/iot-hub-devguide-endpoints/endpoints.png
[lnk-amqp]: https://www.amqp.org/
[lnk-mqtt]: http://mqtt.org/
[lnk-websockets]: https://tools.ietf.org/html/rfc6455
[lnk-arm]: ../azure-resource-manager/resource-group-overview.md
[lnk-event-hubs]: http://azure.microsoft.com/documentation/services/event-hubs/

[lnk-tls]: https://tools.ietf.org/html/rfc5246


[lnk-sdks]: iot-hub-devguide-sdks.md
[lnk-accesscontrol]: iot-hub-devguide-security.md#access-control-and-permissions
[lnk-importexport]: iot-hub-devguide-identity-registry.md#import-and-export-device-identities
[lnk-d2c]: iot-hub-devguide-messages-d2c.md
[lnk-device-identities]: iot-hub-devguide-identity-registry.md
[lnk-upload]: iot-hub-devguide-file-upload.md
[lnk-c2d]: iot-hub-devguide-messages-c2d.md
[lnk-methods]: iot-hub-devguide-direct-methods.md
[lnk-twins]: iot-hub-devguide-device-twins.md
[lnk-query]: iot-hub-devguide-query-language.md
[lnk-jobs]: iot-hub-devguide-jobs.md

[lnk-devguide-quotas]: iot-hub-devguide-quotas-throttling.md
[lnk-devguide-query]: iot-hub-devguide-query-language.md
[lnk-devguide-mqtt]: iot-hub-mqtt-support.md
[lnk-devguide-messaging]: iot-hub-devguide-messaging.md
[lnk-operations-mon]: iot-hub-operations-monitoring.md
