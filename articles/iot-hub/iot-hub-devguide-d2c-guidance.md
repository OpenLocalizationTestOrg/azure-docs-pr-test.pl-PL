---
title: "Opcje urządzenia do chmury systemu Azure IoT Hub | Dokumentacja firmy Microsoft"
description: "Przewodnik dewelopera — wskazówki dotyczące użycie wiadomości urządzenia do chmury, zgłoszone właściwości lub przekazywania pliku do komunikacji z chmury do urządzenia."
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
ms.openlocfilehash: a36283053939ccd53856a394cd9efb66285271ae
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="device-to-cloud-communications-guidance"></a>Wskazówki dotyczące komunikacji urządzenia do chmury
Podczas wysyłania informacji z aplikacji urządzenia zaplecza rozwiązania, Centrum IoT udostępnia trzy opcje:

* [Urządzenia do chmury wiadomości] [ lnk-d2c] telemetrii serie czasu i alerty.
* [Zgłoszone właściwości] [ lnk-twins] raportowania urządzenia stan informacje takie jak dostępne możliwości, warunków lub stan długotrwałe przepływów pracy. Na przykład konfiguracji i aktualizacji oprogramowania.
* [Przekazywanie pliku] [ lnk-fileupload] nośnika pliki i partie dużych telemetrii przekazany przez sporadycznie połączonych urządzeń lub skompresowane, aby oszczędzić przepustowość.

Oto szczegółowe porównanie różnych opcji komunikacji urządzenia do chmury.

|  | Komunikaty z urządzenia do chmury | Zgłoszony właściwości | Przekazywania plików |
| ---- | ------- | ---------- | ---- |
| Scenariusz | Dane telemetryczne szeregów czasowych i alerty. Na przykład partii danych czujnika 256 KB wysyłane co 5 minut. | Dostępne możliwości i warunki. Na przykład bieżącego urządzenia tryb łączności przykład sieci komórkowej lub Wi-Fi. Synchronizowanie długotrwałe przepływów pracy, takich jak aktualizacje oprogramowania i konfiguracji oprogramowania. | Pliki multimedialne. Partie dużych telemetrii (zazwyczaj skompresowane). |
| Przechowywanie i pobieranie | Tymczasowo przechowywane przez Centrum IoT maksymalnie 7 dni. Tylko sekwencyjnego odczytu. | Przechowywane przez Centrum IoT w dwie urządzenia. Pobieranie przy użyciu [język zapytań Centrum IoT][lnk-query]. | Przechowywane na koncie usługi Magazyn Azure dostarczane przez użytkownika. |
| Rozmiar | Maksymalnie 256 KB wiadomości. | Rozmiar maksymalny zgłoszone właściwości jest 8 KB. | Maksymalny rozmiar obsługiwany przez magazyn obiektów Blob Azure. |
| częstotliwość | Wysoki. Aby uzyskać więcej informacji, zobacz [ogranicza Centrum IoT][lnk-quotas]. | Średnia liczba godzin. Aby uzyskać więcej informacji, zobacz [ogranicza Centrum IoT][lnk-quotas]. | Niski. Aby uzyskać więcej informacji, zobacz [ogranicza Centrum IoT][lnk-quotas]. |
| Protokół | Dostępna dla wszystkich protokołów. | Obecnie dostępne tylko w przypadku używania MQTT. | Dostępne w przypadku korzystania z protokołów, ale wymaga HTTP na urządzeniu. |

Istnieje możliwość, że aplikacja wymaga aby zarówno wysyłać informacje jako szeregów czasowych telemetrii lub alert, a także aby udostępnić ją w dwie urządzenia. W tym scenariuszu można wybrać jedną z następujących opcji:

* Aplikacja urządzenie wysyła komunikat urządzenia do chmury i raporty zmiany właściwości.
* Zaplecze rozwiązania może przechowywać informacje w znacznikach dwie urządzenia po odebraniu wiadomości.

Ponieważ urządzenia do chmury wiadomości włączyć znacznie wyższą przepływność niż aktualizacji dwie urządzenia, czasami jest pożądane, aby uniknąć aktualizowanie dwie urządzenia dla każdej wiadomości urządzenia do chmury.


[lnk-twins]: iot-hub-devguide-device-twins.md
[lnk-fileupload]: iot-hub-devguide-file-upload.md
[lnk-quotas]: iot-hub-devguide-quotas-throttling.md
[lnk-query]: iot-hub-devguide-query-language.md
[lnk-d2c]: iot-hub-devguide-messages-d2c.md
