---
title: "Portów i protokołów komunikacyjnych Centrum IoT Azure | Dokumentacja firmy Microsoft"
description: "Przewodnik dewelopera — w tym artykule opisano protokołów komunikacyjnych obsługiwanych, urządzenia do chmury i chmury do urządzenia komunikację i numery portów, które muszą być otwarte."
services: iot-hub
documentationcenter: .net
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 3fc5f1a3-3711-4611-9897-d4db079b4250
ms.service: iot-hub
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/25/2017
ms.author: dobett
ms.openlocfilehash: 98004a48734e33f85eebf8f6213d9f0751dea843
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# Odwołanie — wybierz protokół komunikacyjny

Centrum IoT umożliwia urządzenia do używania [MQTT][lnk-mqtt], MQTT przez protokół WebSockets, [AMQP][lnk-amqp], protokołów AMQP za pośrednictwem protokołu WebSockets i HTTP do komunikacji po stronie urządzenia. Informacje, jak te protokoły obsługują określone funkcje Centrum IoT, zobacz [wskazówki komunikację urządzenia do chmury] [ lnk-d2c-guidance] i [wskazówki dotyczące komunikacji chmury do urządzenia][lnk-c2d-guidance].

W poniższej tabeli przedstawiono ogólne zalecenia dotyczące wyboru protokołu:

| Protokół | Kiedy należy wybrać tego protokołu |
| --- | --- |
| MQTT <br> MQTT za pośrednictwem protokołu WebSocket |Użyj na wszystkich urządzeniach, które nie wymagają łączyć wielu urządzeń (każde z nich własne poświadczenia na urządzenie) za pośrednictwem tego samego połączenia TLS. |
| AMQP <br> Protokół AMQP za pośrednictwem protokołu WebSocket |Aby móc korzystać z połączenia Multipleksowanie między urządzeniami w systemie bram pola i w chmurze. |
| HTTP |Zalecany w przypadku urządzeń, które nie obsługują innych protokołów. |

Po wybraniu użytkownika protokołu komunikacji po stronie urządzenia, należy wziąć pod uwagę następujące kwestie:

* **Wzorzec chmury do urządzenia**. HTTP nie ma wydajnym sposobem wdrożenia serwera wypychania. Tak korzystając z protokołu HTTP, urządzenia sondować Centrum IoT wiadomości chmury do urządzenia. Ta metoda jest nieefektywne dla Centrum IoT i urządzeniami. W obszarze bieżące wytyczne HTTP każde urządzenie powinno sondowania wiadomości co 25 minut lub więcej. Z drugiej strony MQTT i protokołu AMQP obsługuje wypychania serwera podczas odbierania wiadomości chmury do urządzenia. Umożliwiają one natychmiastowego wypchnięć wiadomości z Centrum IoT na urządzeniu. Jeśli czas oczekiwania na dostarczenie jest istotny, MQTT lub AMQP są protokoły używane. Rzadko połączonych urządzeń HTTP działa również.
* **Pole bram**. Korzystając z MQTT i HTTP, nie można połączyć z wieloma urządzeniami (każde z nich własne poświadczenia na urządzenie) przy użyciu tego samego połączenia TLS. W związku z tym dla [pola scenariusze bramy][lnk-azure-gateway-guidance], te protokoły są nieoptymalne, ponieważ wymagają one jednego połączenia TLS między bramą pola i Centrum IoT dla każdego urządzenia podłączone do bramy pola.
* **Mało zasobów urządzeń**. Biblioteki MQTT i HTTP mają mniejsze zużycie niż bibliotek protokołu AMQP. Tak Jeśli urządzenie ma ograniczone zasoby (na przykład mniejszą niż 1 MB pamięci RAM), te protokoły mogą być dostępne tylko implementacja protokołu.
* **Przechodzenie sieci**. Standardowy protokół AMQP korzysta z portu 5671, podczas gdy MQTT nasłuchuje na porcie 8883, co może spowodować problemy w sieciach, które zostały zamknięte do protokołów innych niż HTTP. MQTT przez protokół WebSockets, AMQP za pośrednictwem protokołu WebSockets i HTTP są dostępne do użycia w tym scenariuszu.
* **Rozmiar ładunku**. MQTT i AMQP są binarne protokołów, które powoduje ładunki mniejszych niż HTTP.

> [!WARNING]
> Przy użyciu protokołu HTTP, każde urządzenie powinien sondowania komunikatów chmury do urządzenia, co 25 minut lub więcej. Jednak podczas tworzenia, dopuszczalne jest do sondowania częściej niż co 25 minut.

## Numery portów

Urządzenia mogą komunikować się z Centrum IoT na platformie Azure przy użyciu różnych protokołów. Zazwyczaj wybór protokół jest wymuszany przez określone wymagania rozwiązania. W poniższej tabeli wymieniono portów wychodzących, które musi być otwarte dla urządzenia można było użyć określonego protokołu:

| Protokół | Port |
| --- | --- |
| MQTT |8883 |
| MQTT przez protokół WebSockets |443 |
| AMQP |5671 |
| Protokół AMQP przez protokół WebSockets |443 |
| HTTP |443 |

Po utworzeniu Centrum IoT w regionie Azure, Centrum IoT przechowuje ten sam adres IP przez czas ich istnienia tego Centrum IoT. Jednak aby obsługa jakości usługi, jeśli Microsoft przenosi Centrum IoT na jednostkę skalowania różnych ona przypisywana jest nowy adres IP.


## Następne kroki

Aby dowiedzieć się więcej na temat sposobu Centrum IoT implementuje ten protokół MQTT, zobacz [komunikacja z Centrum IoT przy użyciu protokołu MQTT][lnk-mqtt-support].

[lnk-d2c-guidance]: iot-hub-devguide-d2c-guidance.md
[lnk-c2d-guidance]: iot-hub-devguide-c2d-guidance.md
[lnk-mqtt-support]: iot-hub-mqtt-support.md
[lnk-amqp]: http://docs.oasis-open.org/amqp/core/v1.0/os/amqp-core-complete-v1.0-os.pdf
[lnk-mqtt]: http://docs.oasis-open.org/mqtt/mqtt/v3.1.1/mqtt-v3.1.1.pdf
[lnk-azure-gateway-guidance]: iot-hub-devguide-endpoints.md#field-gateways
