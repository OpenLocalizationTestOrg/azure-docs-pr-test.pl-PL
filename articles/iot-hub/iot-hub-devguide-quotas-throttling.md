---
title: "przydziały Centrum IoT Azure aaaUnderstand i ograniczania przepustowości | Dokumentacja firmy Microsoft"
description: "Przewodnik dewelopera — opis przydziały hello, stosowane tooIoT koncentratora i hello ograniczania przepustowości zachowanie jest oczekiwane."
services: iot-hub
documentationcenter: .net
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 425e1b08-8789-4377-85f7-c13131fae4ce
ms.service: iot-hub
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/16/2017
ms.author: dobett
ms.openlocfilehash: 023fa29bfbfb1de35708d6d121a1c56b50adfed9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="reference---iot-hub-quotas-and-throttling"></a>Odwołanie - Centrum IoT przydziały i ograniczenia przepustowości

## <a name="quotas-and-throttling"></a>Limity przydziału i ograniczanie wydajności
Każdej subskrypcji platformy Azure może mieć maksymalnie 10 centra IoT i maksymalnie 1 wolnego koncentratora.

Każdy Centrum IoT jest udostępniane z określonej liczby jednostek w określonej jednostki SKU (Aby uzyskać więcej informacji, zobacz [cennik usługi Azure IoT Hub][lnk-pricing]). Witaj jednostki SKU i liczbę jednostek określają hello maksymalny dzienny limit przydziału wiadomości, które można wysyłać.

Witaj SKU określa również hello ograniczenie, które egzekwuje Centrum IoT na wszystkie operacje.

## <a name="operation-throttles"></a>Limity operacji
Limity operacji są ograniczenia szybkości, które są stosowane w zakresach minuty hello i są przeznaczone nadużycie tooavoid. Centrum IoT próbuje tooavoid zwraca błędy, jeśli to możliwe, ale rozpoczyna zwracania wyjątków, jeśli naruszenia ograniczenia hello zbyt długo.

Witaj w następującej tabeli przedstawiono hello wymuszane limity. Wartości można znaleźć tooan poszczególnych koncentratora.

| Ograniczenie | Bezpłatne i koncentratory S1 | Koncentratory s2 | Koncentratory S3 | 
| -------- | ------- | ------- | ------- |
| Operacje rejestru tożsamości (Tworzenie, pobieranie, listy, aktualizowanie i usuwanie) | 1.67/sec/Unit (jednostka/100/min) | 1.67/sec/Unit (jednostka/100/min) | 83.33/sec/Unit (jednostka-5000/min) |
| Połączenia urządzenia | Maksymalną 100 na sekundę lub jednostki-12/s <br/> Na przykład dwie jednostki S1 są 2\*12 = 24/s, ale mają co najmniej 100 na sekundę przez jednostek. W przypadku dziewięć S1, masz 108 na sekundę (9\*12) między jednostek. | Jednostka-120/s | Jednostka-6000/s |
| Liczba elementów wysłanych z urządzenia do chmury | Maksymalną 100 na sekundę lub jednostki-12/s <br/> Na przykład dwie jednostki S1 są 2\*12 = 24/s, ale mają co najmniej 100 na sekundę przez jednostek. W przypadku dziewięć S1, masz 108 na sekundę (9\*12) między jednostek. | Jednostka-120/s | Jednostka-6000/s |
| Liczba elementów wysłanych z chmury do urządzenia | 1.67/sec/Unit (jednostka/100/min) | 1.67/sec/Unit (jednostka/100/min) | 83.33/sec/Unit (jednostka-5000/min) |
| Liczba odebranych elementów wysłanych z chmury do urządzenia <br/> (tylko gdy urządzenie korzysta z protokołu HTTP)| 16.67/sec/Unit (jednostka-1000/min) | 16.67/sec/Unit (jednostka-1000/min) | 833.33/sec/Unit (jednostka-50000/min) |
| Przekazywanie pliku | 1.67 pliku przekazywania powiadomień na sekundę/jednostkę (jednostka/100/min) | 1.67 pliku przekazywania powiadomień na sekundę/jednostkę (jednostka/100/min) | 83.33 pliku przekazywania powiadomień/s/jednostek (jednostka-5000/min) |
| Metody bezpośrednie | Jednostka-20/s | Jednostka-60/s | Jednostka-3000/s | 
| Liczba odczytów bliźniaczej reprezentacji urządzenia | 10 na sekundę | Maksymalnie 10 na sekundę lub jednostki-1/s | Jednostka-50/s |
| Liczba aktualizacji bliźniaczej reprezentacji urządzenia | 10 na sekundę | Maksymalnie 10 na sekundę lub jednostki-1/s | Jednostka-50/s |
| Operacje zadań <br/> (tworzenie, aktualizowanie, wyświetlanie, usuwanie) | 1.67/sec/Unit (jednostka/100/min) | 1.67/sec/Unit (jednostka/100/min) | 83.33/sec/Unit (jednostka-5000/min) |
| Przepływność operacji zadań poszczególnych urządzeń | 10 na sekundę | Maksymalnie 10 na sekundę lub jednostki-1/s | Jednostka-50/s |

Jest ważne tooclarify, który hello *połączenia urządzenia* ograniczania kontroluje częstotliwość hello jaką nawiązywanie nowych połączeń urządzenia z Centrum IoT. Witaj *połączenia urządzenia* przepustnicy nie kontroluje hello maksymalna liczba równocześnie połączonych urządzeń. Przepustnica Hello zależy od hello liczbę jednostek, które są udostępniane dla Centrum IoT hello.

Na przykład jeśli kupisz pojedynczą jednostkę S1 get przepustnicy połączenia o szybkości 100 na sekundę. W związku z tym tooconnect 100000 urządzeniami potrzebny co najmniej 1 000 sekund (około 16 minut). Jednak może mieć dowolną liczbę równocześnie połączonych urządzeń zgodnie z urządzeń zarejestrowanych w rejestrze tożsamości.

Szczegółowe omówienie Centrum IoT ograniczania zachowania, zobacz hello blogu [Centrum IoT ograniczania przepustowości i][lnk-throttle-blog].

> [!NOTE]
> W dowolnym momencie, jest możliwe tooincrease przydziałów lub ograniczyć limity przez odpowiednie zwiększenie liczby hello elastycznie jednostki w Centrum IoT.
> 
> [!IMPORTANT]
> Operacje rejestru tożsamości są przeznaczone dla środowiska wykonawczego używanych do zarządzania urządzeniami i inicjowania obsługi scenariuszy. Odczytu lub aktualizacji dużej liczby urządzeń tożsamości jest obsługiwany za pośrednictwem [importowanie i eksportowanie zadań][lnk-importexport].
> 
> 

## <a name="other-limits"></a>Inne ograniczenia.

Centrum IoT wymusza inne ograniczenia operacyjne:

| Operacja | Limit |
| --------- | ----- |
| Przekazywanie pliku identyfikatorów URI | 10000 URI SAS może być limit dla konta magazynu w tym samym czasie. <br/> Jednocześnie może istnieć 10 identyfikatorów URI sygnatury dostępu współdzielonego. |
| Zadania | Historia zadań są przechowywane w górę too30 dni <br/> Maksymalna współbieżnych zadań ma wartość 1 (w przypadku wolnego i S1, 5 (w przypadku S2), 10 (na potrzeby S3). |
| Dodatkowe punkty końcowe | Płatnej SKU koncentratory może być 10 dodatkowe punkty końcowe. Bezpłatne koncentratory SKU może mieć jeden dodatkowy punkt końcowy. |
| Reguły routingu wiadomości | Płatnej SKU koncentratory mogą mieć 100 reguły routingu. Bezpłatne koncentratory SKU może mieć pięć reguły routingu. |
| Urządzenia do chmury do obsługi komunikatów | Rozmiar maksymalny komunikatu 256 KB |
| Obsługa wiadomości chmury do urządzenia | Komunikat maksymalny rozmiar 64 KB |
| Obsługa wiadomości chmury do urządzenia | Maksymalna liczba oczekujących komunikatów w celu dostarczania to 50 |

> [!NOTE]
> Obecnie hello maksymalną liczbę urządzeń, możesz połączyć pojedynczy Centrum IoT tooa jest 500 000. Jeśli chcesz tooincrease ten limit, skontaktuj się z [Microsoft Support](https://azure.microsoft.com/support/options/).

## <a name="latency"></a>Opóźnienie
Centrum IoT dokłada starań, małe opóźnienia tooprovide dla wszystkich operacji. Jednak ze względu na warunki toonetwork i inne czynniki nieprzewidywalne go nie może zagwarantować maksymalnego czasu oczekiwania. Podczas projektowania rozwiązania, wykonaj następujące czynności:

* Należy unikać wprowadzania żadnych założeń dotyczących hello maksymalnego czasu oczekiwania żadnej operacji centrum IoT.
* Udostępnić Centrum IoT w najbliższej urządzeń tooyour hello region platformy Azure.
* Należy rozważyć użycie Azure IoT krawędzi tooperform wrażliwy na opóźnienia operacji na urządzeniu hello lub na urządzeniu toohello Zamknij bramy.

Wiele jednostek Centrum IoT wpłynąć na ograniczenia przepustowości, jak opisano wcześniej, ale nie udostępniają wszystkie korzyści dodatkowe opóźnienia lub gwarancji.
Jeśli widzisz zwiększa nieoczekiwane opóźnienia operacji, skontaktuj się z [Microsoft Support](https://azure.microsoft.com/support/options/).

## <a name="next-steps"></a>Następne kroki
Inne tematy dokumentacji, w tym przewodniku deweloperów Centrum IoT obejmują:

* [Punkty końcowe Centrum IoT][lnk-devguide-endpoints]
* [Język zapytań Centrum IoT urządzenia twins, zadań i rozsyłania wiadomości][lnk-devguide-query]
* [Obsługa MQTT Centrum IoT][lnk-devguide-mqtt]

[lnk-pricing]: https://azure.microsoft.com/pricing/details/iot-hub
[lnk-throttle-blog]: https://azure.microsoft.com/blog/iot-hub-throttling-and-you/
[lnk-importexport]: iot-hub-devguide-identity-registry.md#import-and-export-device-identities

[lnk-devguide-endpoints]: iot-hub-devguide-endpoints.md
[lnk-devguide-query]: iot-hub-devguide-query-language.md
[lnk-devguide-mqtt]: iot-hub-mqtt-support.md
