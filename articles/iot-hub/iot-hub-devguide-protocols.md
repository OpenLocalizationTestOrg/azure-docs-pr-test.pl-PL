---
title: "aaaAzure komunikacji Centrum IoT protokoły i porty | Dokumentacja firmy Microsoft"
description: "Przewodnik dewelopera — w tym artykule opisano hello obsługiwanych protokołów komunikacyjnych komunikacji urządzenia do chmury i chmury do urządzenia i hello numery portów, które muszą być otwarte."
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
ms.openlocfilehash: 31cb948f1d30edd87edb13ad0dd859c02bcc3239
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# Odwołanie — wybierz protokół komunikacyjny

Centrum IoT umożliwia toouse urządzeń [MQTT][lnk-mqtt], MQTT przez protokół WebSockets, [AMQP][lnk-amqp], protokołów AMQP za pośrednictwem protokołu WebSockets i HTTP dla po stronie urządzenia komunikacji. Informacje, jak te protokoły obsługują określone funkcje Centrum IoT, zobacz [wskazówki komunikację urządzenia do chmury] [ lnk-d2c-guidance] i [wskazówki dotyczące komunikacji chmury do urządzenia][lnk-c2d-guidance].

Witaj Poniższa tabela zawiera hello ogólne zalecenia dotyczące wyboru protokołu:

| Protokół | Kiedy należy wybrać tego protokołu |
| --- | --- |
| MQTT <br> MQTT za pośrednictwem protokołu WebSocket |Użyj na wszystkich urządzeniach, które nie wymagają tooconnect wielu urządzeń (każde z nich własne poświadczenia na urządzenie) za pośrednictwem hello tego samego połączenia TLS. |
| AMQP <br> Protokół AMQP za pośrednictwem protokołu WebSocket |Pole i w chmurze bram tootake zalety połączenia Multipleksowanie między urządzeniami w systemie. |
| HTTP |Zalecany w przypadku urządzeń, które nie obsługują innych protokołów. |

Należy wziąć pod uwagę następujące punkty po wybraniu użytkownika protokołu komunikacji po stronie urządzenia hello:

* **Wzorzec chmury do urządzenia**. HTTP nie ma wypychania serwera tooimplement wydajny sposób. Tak korzystając z protokołu HTTP, urządzenia sondować Centrum IoT wiadomości chmury do urządzenia. Ta metoda jest nieefektywne hello urządzenia i Centrum IoT. W obszarze bieżące wytyczne HTTP każde urządzenie powinno sondowania wiadomości co 25 minut lub więcej. Na hello drugiej strony, MQTT i protokołu AMQP obsługują wypychania serwera podczas odbierania wiadomości chmury do urządzenia. Umożliwiają one natychmiastowego wypchnięć komunikatów z Centrum IoT toohello urządzenia. Jeśli czas oczekiwania na dostarczenie jest istotny, MQTT lub AMQP są hello najlepsze toouse protokołów. Rzadko połączonych urządzeń HTTP działa również.
* **Pole bram**. Korzystając z MQTT i HTTP, nie można połączyć z wieloma urządzeniami (każde z nich własne poświadczenia na urządzenie) przy użyciu hello tego samego połączenia TLS. W związku z tym dla [pola scenariusze bramy][lnk-azure-gateway-guidance], te protokoły są nieoptymalne, ponieważ wymagają one jednego połączenia TLS między bramą pola hello i Centrum IoT dla każdej bramy pola toohello podłączonego urządzenia.
* **Mało zasobów urządzeń**. Witaj MQTT i biblioteki HTTP mają mniejsze zużycie niż hello AMQP biblioteki. Tak, jeśli hello urządzenie ma ograniczone zasoby (na przykład mniejszą niż 1 MB pamięci RAM), te protokoły mogą być hello tylko implementacja protokołu dostępne.
* **Przechodzenie sieci**. Standardowy protokół AMQP Hello korzysta z portu 5671, gdy MQTT nasłuchuje na porcie 8883, co może spowodować problemy w sieciach, które są protokoły HTTP toonon zamknięte. MQTT przez protokół WebSockets, AMQP za pośrednictwem protokołu WebSockets i HTTP są dostępne toobe używaną w tym scenariuszu.
* **Rozmiar ładunku**. MQTT i AMQP są binarne protokołów, które powoduje ładunki mniejszych niż HTTP.

> [!WARNING]
> Przy użyciu protokołu HTTP, każde urządzenie powinien sondowania komunikatów chmury do urządzenia, co 25 minut lub więcej. Jednak podczas tworzenia, jest dopuszczalne toopoll częściej niż co 25 minut.

## Numery portów

Urządzenia mogą komunikować się z Centrum IoT na platformie Azure przy użyciu różnych protokołów. Zazwyczaj wybór hello protokół jest wymuszany przez określone wymagania hello hello rozwiązania. Witaj poniższej tabeli wymieniono hello portów wychodzących, które muszą być otwarte dla urządzenia toobe stanie toouse określonego protokołu:

| Protokół | Port |
| --- | --- |
| MQTT |8883 |
| MQTT przez protokół WebSockets |443 |
| AMQP |5671 |
| Protokół AMQP przez protokół WebSockets |443 |
| HTTP |443 |

Po utworzeniu Centrum IoT w regionie Azure, hello przechowuje Centrum IoT hello tego samego adresu IP dla hello okres istnienia tego Centrum IoT. Jednak toomaintain jakości usług, jeśli przenosi Microsoft hello IoT hub tooa innej skali jednostki, a następnie go jest przypisany nowy adres IP.


## Następne kroki

toolearn więcej informacji na temat sposobu Centrum IoT implementuje protokół MQTT hello, zobacz [komunikacja z Centrum IoT przy użyciu protokołu MQTT hello][lnk-mqtt-support].

[lnk-d2c-guidance]: iot-hub-devguide-d2c-guidance.md
[lnk-c2d-guidance]: iot-hub-devguide-c2d-guidance.md
[lnk-mqtt-support]: iot-hub-mqtt-support.md
[lnk-amqp]: http://docs.oasis-open.org/amqp/core/v1.0/os/amqp-core-complete-v1.0-os.pdf
[lnk-mqtt]: http://docs.oasis-open.org/mqtt/mqtt/v3.1.1/mqtt-v3.1.1.pdf
[lnk-azure-gateway-guidance]: iot-hub-devguide-endpoints.md#field-gateways
