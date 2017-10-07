---
title: "Opcje aaaAzure Centrum IoT urządzenia do chmury | Dokumentacja firmy Microsoft"
description: "Przewodnik dewelopera — wskazówki dotyczące po toouse wiadomości urządzenia do chmury, zgłoszone właściwości lub plik przekazać do komunikacji z chmury do urządzenia."
services: iot-hub
documentationcenter: .net
author: fsautomata
manager: timlt
editor: 
ms.assetid: 979136db-c92d-4288-870c-f305e8777bdd
ms.service: iot-hub
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/25/2017
ms.author: elioda
ms.openlocfilehash: 2caefc4f59e16ad28b0d8cf4b3bb627b4cba803b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="device-to-cloud-communications-guidance"></a>Wskazówki dotyczące komunikacji urządzenia do chmury
Podczas wysyłania informacji z hello urządzenia aplikacji toohello zaplecza rozwiązania, Centrum IoT udostępnia trzy opcje:

* [Urządzenia do chmury wiadomości] [ lnk-d2c] telemetrii serie czasu i alerty.
* [Zgłoszone właściwości] [ lnk-twins] raportowania urządzenia stan informacje takie jak dostępne możliwości, warunków lub stan hello długotrwałe przepływów pracy. Na przykład konfiguracji i aktualizacji oprogramowania.
* [Przekazywanie pliku] [ lnk-fileupload] nośnika pliki i partie dużych telemetrii przekazany przez sporadycznie połączonych urządzeń lub skompresowany przepustowości toosave.

Oto szczegółowe porównanie hello różnych opcji komunikacji urządzenia do chmury.

|  | Komunikaty z urządzenia do chmury | Zgłoszony właściwości | Przekazywania plików |
| ---- | ------- | ---------- | ---- |
| Scenariusz | Dane telemetryczne szeregów czasowych i alerty. Na przykład partii danych czujnika 256 KB wysyłane co 5 minut. | Dostępne możliwości i warunki. Na przykład hello bieżącego urządzenia tryb łączności przykład sieci komórkowej lub Wi-Fi. Synchronizowanie długotrwałe przepływów pracy, takich jak aktualizacje oprogramowania i konfiguracji oprogramowania. | Pliki multimedialne. Partie dużych telemetrii (zazwyczaj skompresowane). |
| Przechowywanie i pobieranie | Tymczasowo przechowywane przez Centrum IoT się too7 dni. Tylko sekwencyjnego odczytu. | Przechowywane przez Centrum IoT w Witaj dwie urządzenia. Pobieranie, przy użyciu hello [język zapytań Centrum IoT][lnk-query]. | Przechowywane na koncie usługi Magazyn Azure dostarczane przez użytkownika. |
| Rozmiar | Się komunikaty too256 KB. | Rozmiar maksymalny zgłoszone właściwości jest 8 KB. | Maksymalny rozmiar obsługiwany przez magazyn obiektów Blob Azure. |
| częstotliwość | Wysoki. Aby uzyskać więcej informacji, zobacz [ogranicza Centrum IoT][lnk-quotas]. | Średnia liczba godzin. Aby uzyskać więcej informacji, zobacz [ogranicza Centrum IoT][lnk-quotas]. | Niski. Aby uzyskać więcej informacji, zobacz [ogranicza Centrum IoT][lnk-quotas]. |
| Protokół | Dostępna dla wszystkich protokołów. | Obecnie dostępne tylko w przypadku używania MQTT. | Dostępne, gdy przy użyciu protokołów, ale wymaga HTTP na urządzeniu hello. |

Istnieje możliwość, że aplikacja wymaga tooboth wysyłania informacji dotyczących telemetrii szeregów czasowych lub alert, a także toomake ich w Witaj dwie urządzenia. W tym scenariuszu można wybrać hello następujące opcje:

* aplikacji urządzenia Hello wysyła komunikat urządzenia do chmury i raporty zmiany właściwości.
* zaplecza rozwiązania Hello można przechowywać informacje hello w znacznikach dwie urządzenia hello po odebraniu wiadomości powitania.

Ponieważ urządzenia do chmury wiadomości włączyć znacznie wyższą przepływność niż aktualizacji dwie urządzenia, czasami jest pożądane tooavoid aktualizowania hello urządzenia dwie dla każdego komunikatu urządzenia do chmury.


[lnk-twins]: iot-hub-devguide-device-twins.md
[lnk-fileupload]: iot-hub-devguide-file-upload.md
[lnk-quotas]: iot-hub-devguide-quotas-throttling.md
[lnk-query]: iot-hub-devguide-query-language.md
[lnk-d2c]: iot-hub-devguide-messages-d2c.md
