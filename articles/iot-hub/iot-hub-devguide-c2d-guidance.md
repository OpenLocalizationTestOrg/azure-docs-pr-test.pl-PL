---
title: "Opcje chmury do urządzenia usługi Azure IoT Hub | Dokumentacja firmy Microsoft"
description: "Przewodnik dewelopera — wskazówki dotyczące kiedy należy używać metody bezpośredniego, odpowiednie właściwości urządzenia dwie lub wiadomości chmury do urządzenia komunikacji chmury do urządzenia."
services: iot-hub
documentationcenter: 
author: fsautomata
manager: timlt
editor: 
ms.assetid: 1ac90923-1edf-4134-bbd4-77fee9b68d24
ms.service: iot-hub
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/25/2017
ms.author: elioda
ms.openlocfilehash: e6cd4880c9bfcc670bd116d3dd8e5245d70f85cd
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="cloud-to-device-communications-guidance"></a>Wskazówki dotyczące komunikacji chmury do urządzenia
Centrum IoT zawiera trzy opcje udostępniać funkcje do aplikacji wewnętrznych aplikacji dla urządzeń:

* [Bezpośrednie metody] [ lnk-methods] komunikacji, które wymagają natychmiastowego potwierdzenie wyników. Bezpośrednie metody są często używane dla sterowania interaktywnego urządzeń, takich jak włączenie wentylatora.
* [Dwie na potrzeby właściwości] [ lnk-twins] dla polecenia długotrwałe przeznaczony do poddane urządzenia określony żądany stan. Na przykład ustawić interwał wysyłania danych telemetrycznych do 30 minut.
* [Komunikaty chmury do urządzenia] [ lnk-c2d] jednokierunkowe powiadomień do aplikacji urządzenia.

Oto szczegółowe porównanie różnych opcji komunikacji chmury do urządzenia.

|  | Metody bezpośrednie | Dwie na potrzeby właściwości | Komunikaty chmury do urządzenia |
| ---- | ------- | ---------- | ---- |
| Scenariusz | Polecenia, które wymagają natychmiastowego potwierdzenia, jak włączenie wentylatora. | Przeznaczony do wprowadzone urządzenia do niektórych żądanego stanu polecenia długotrwałe. Na przykład ustawić interwał wysyłania danych telemetrycznych do 30 minut. | Jednokierunkowe powiadomienia do aplikacji urządzenia. |
| Przepływ danych | Dwukierunkowe. Aplikacji urządzenia mogą odpowiadać od razu do metody. Zaplecze rozwiązania odbiera wyniku kontekstowej na żądanie. | Jednokierunkowe. Aplikacja urządzenie odbiera powiadomienie o zmianie właściwości. | Jednokierunkowe. Aplikacja urządzenie odbiera wiadomości
| Trwałość | Odłączone urządzenia nie będą wykorzystywane. Zaplecza rozwiązania jest powiadamiany o to, że urządzenie nie jest połączony. | Wartości właściwości są zachowywane w dwie urządzenia. Urządzenie będzie go odczytać w następnym ponowne nawiązanie połączenia. Wartości właściwości są pobieranie z [język zapytań Centrum IoT][lnk-query]. | Komunikaty mogą być przechowywane przez Centrum IoT do 48 godzin. |
| Obiekty docelowe | Za pomocą jednego urządzenia **deviceId**, lub wielu urządzeń przy użyciu [zadania][lnk-jobs]. | Za pomocą jednego urządzenia **deviceId**, lub wielu urządzeń przy użyciu [zadania][lnk-jobs]. | Pojedyncze urządzenie przez **deviceId**. |
| Rozmiar | Do 8 KB żądań i odpowiedzi 8KB. | Maksymalna żądany rozmiar właściwości to 8 KB. | Komunikaty do 64 KB. |
| częstotliwość | Wysoki. Aby uzyskać więcej informacji, zobacz [ogranicza Centrum IoT][lnk-quotas]. | Średnia liczba godzin. Aby uzyskać więcej informacji, zobacz [ogranicza Centrum IoT][lnk-quotas]. | Niski. Aby uzyskać więcej informacji, zobacz [ogranicza Centrum IoT][lnk-quotas]. |
| Protokół | Obecnie dostępne tylko w przypadku używania MQTT. | Obecnie dostępne tylko w przypadku używania MQTT. | Dostępna dla wszystkich protokołów. Urządzenie musi wykonać sondowanie przy użyciu protokołu HTTP. |

Dowiedz się, jak używać bezpośrednich metod, odpowiednie właściwości i komunikaty chmury do urządzenia w następujące samouczki:

* [Użyj metody bezpośredniego][lnk-methods-tutorial], bezpośrednie metod;
* [Konfigurowanie urządzeń za pomocą właściwości żądanego][lnk-twin-properties]dla dwie urządzenia na potrzeby właściwości; 
* [Wysyłanie komunikatów chmury do urządzenia][lnk-c2d-tutorial], komunikaty chmury do urządzenia.

[lnk-twins]: iot-hub-devguide-device-twins.md
[lnk-quotas]: iot-hub-devguide-quotas-throttling.md
[lnk-query]: iot-hub-devguide-query-language.md
[lnk-jobs]: iot-hub-devguide-jobs.md
[lnk-c2d]: iot-hub-devguide-messages-c2d.md
[lnk-methods]: iot-hub-devguide-direct-methods.md
[lnk-methods-tutorial]: iot-hub-node-node-direct-methods.md
[lnk-twin-properties]: iot-hub-node-node-twin-how-to-configure.md
[lnk-c2d-tutorial]: iot-hub-node-node-c2d.md
