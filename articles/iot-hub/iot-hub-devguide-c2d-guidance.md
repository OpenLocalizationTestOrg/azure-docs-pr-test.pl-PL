---
title: "Opcje aaaAzure chmury urządzenia IoT Hub | Dokumentacja firmy Microsoft"
description: "Przewodnik dewelopera — wskazówki dotyczące po toouse bezpośrednie metody, właściwości żądaną dwie urządzenia lub wiadomości chmury do urządzenia komunikacji chmury do urządzenia."
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
ms.openlocfilehash: bb95445054fa2711e34fc1d928c3665e0246c81c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="cloud-to-device-communications-guidance"></a>Wskazówki dotyczące komunikacji chmury do urządzenia
Centrum IoT zawiera trzy opcje dla urządzeń aplikacji tooexpose funkcji tooa zaplecza aplikacji:

* [Bezpośrednie metody] [ lnk-methods] komunikacji, które wymagają natychmiastowego potwierdzenie hello wyniku. Bezpośrednie metody są często używane dla sterowania interaktywnego urządzeń, takich jak włączenie wentylatora.
* [Dwie na potrzeby właściwości] [ lnk-twins] dla polecenia długotrwałe, które tooput hello urządzenia do niektórych żądany stan. Na przykład ustawić hello telemetrii wysyłania interwał too30 minut.
* [Komunikaty chmury do urządzenia] [ lnk-c2d] dla aplikacji urządzenia toohello jednokierunkowe powiadomienia.

Oto szczegółowe porównanie hello różnych opcji komunikacji chmury do urządzenia.

|  | Metody bezpośrednie | Dwie na potrzeby właściwości | Komunikaty chmury do urządzenia |
| ---- | ------- | ---------- | ---- |
| Scenariusz | Polecenia, które wymagają natychmiastowego potwierdzenia, jak włączenie wentylatora. | Polecenia długotrwałe przeznaczony tooput hello urządzenia do niektórych żądanego stanu. Na przykład ustawić hello telemetrii wysyłania interwał too30 minut. | Aplikacja urządzenia toohello jednokierunkowe powiadomienia. |
| Przepływ danych | Dwukierunkowe. Hello aplikacji urządzenia mogą odpowiadać metoda toohello od razu. zaplecza rozwiązania Hello odbiera wyniku hello kontekstowej toohello żądania. | Jednokierunkowe. aplikacji urządzenia Hello otrzyma powiadomienie o hello zmiany właściwości. | Jednokierunkowe. Witaj urządzenia aplikacja odbiera wiadomości powitania
| Trwałość | Odłączone urządzenia nie będą wykorzystywane. zaplecza rozwiązania Hello zostanie powiadomiony, że urządzenie hello nie jest podłączony. | Wartości właściwości są zachowywane w Witaj dwie urządzenia. Urządzenie będzie go odczytać w następnym ponowne nawiązanie połączenia. Wartości właściwości są pobieranie z hello [język zapytań Centrum IoT][lnk-query]. | Komunikaty mogą być przechowywane przez Centrum IoT na górę too48 godzin. |
| Obiekty docelowe | Za pomocą jednego urządzenia **deviceId**, lub wielu urządzeń przy użyciu [zadania][lnk-jobs]. | Za pomocą jednego urządzenia **deviceId**, lub wielu urządzeń przy użyciu [zadania][lnk-jobs]. | Pojedyncze urządzenie przez **deviceId**. |
| Rozmiar | Too8KB żądań i odpowiedzi 8KB. | Maksymalna żądany rozmiar właściwości to 8 KB. | Zapasowych too64KB wiadomości. |
| częstotliwość | Wysoki. Aby uzyskać więcej informacji, zobacz [ogranicza Centrum IoT][lnk-quotas]. | Średnia liczba godzin. Aby uzyskać więcej informacji, zobacz [ogranicza Centrum IoT][lnk-quotas]. | Niski. Aby uzyskać więcej informacji, zobacz [ogranicza Centrum IoT][lnk-quotas]. |
| Protokół | Obecnie dostępne tylko w przypadku używania MQTT. | Obecnie dostępne tylko w przypadku używania MQTT. | Dostępna dla wszystkich protokołów. Urządzenie musi wykonać sondowanie przy użyciu protokołu HTTP. |

Dowiedz się, jak toouse bezpośrednie metody, właściwości żądaną i komunikaty chmury do urządzenia w hello następujące samouczki:

* [Użyj metody bezpośredniego][lnk-methods-tutorial], bezpośrednie metod;
* [Używanie urządzeń tooconfigure odpowiednie właściwości][lnk-twin-properties]dla dwie urządzenia na potrzeby właściwości; 
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
