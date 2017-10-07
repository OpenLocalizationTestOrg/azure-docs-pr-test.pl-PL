---
title: aaaUnderstand Centrum IoT Azure messaging | Dokumentacja firmy Microsoft
description: "Przewodnik dewelopera — urządzenia do chmury i wiadomości z Centrum IoT chmury do urządzenia. Zawiera informacje na temat formaty wiadomości i protokołów komunikacyjnych obsługiwanych."
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
ms.openlocfilehash: a610741e23e243f392f1c042f9ab4a00d42f734f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="device-to-cloud-and-cloud-to-device-messaging-with-iot-hub"></a>Urządzenia do chmury i wiadomości z Centrum IoT chmury do urządzenia

Użyj Centrum IoT messaging toocommunicate z urządzenia przez:

* Wysyłanie [urządzenia do chmury] [ lnk-d2c] wiadomości z rozwiązania tooyour urządzeń zaplecza.
* Wysyłanie [chmury do urządzenia] [ lnk-c2d] komunikaty z powrotem rozwiązania hello zakończenie tooyour urządzeń.

Właściwości podstawowe Centrum IoT z obsługą wiadomości są hello niezawodność i trwałość wiadomości. Te właściwości Włącz odporności toointermittent łączności po stronie urządzenia hello, a tooload wzrósł w przypadku przetwarzania po stronie chmury hello. Centrum IoT implementuje *co najmniej raz* gwarantuje dostarczania dla wiadomości zarówno urządzenia do chmury, jak i chmury do urządzenia.

Wprowadzenie toohello możliwości Centrum IoT, zobacz artykuły hello [Azure i Internet rzeczy] [ lnk-azure-iot] i [omówienie hello usługa Azure IoT Hub] [lnk-iot-hub-overview].

## <a name="when-toouse-iot-hub-messaging"></a>Gdy toouse Centrum IoT obsługi wiadomości

Użycie dla aplikacji urządzenia tooyour jednokierunkowe powiadomień wiadomości urządzenia do chmury do wysyłania telemetrii serie czasu i alertów z aplikacją urządzenia i wiadomości chmury do urządzenia.

* Odwołuje się zbyt[wskazówki komunikację urządzenia do chmury] [ lnk-d2c-guidance] if wątpliwe między przy użyciu wiadomości urządzenia do chmury, zgłoszone właściwości lub przekazywania pliku.
* Odwołuje się zbyt[wskazówki dotyczące komunikacji chmury do urządzenia] [ lnk-c2d-guidance] if wątpliwe między przy użyciu wiadomości chmury do urządzenia, odpowiednie właściwości lub metody bezpośredniego.

## <a name="next-steps"></a>Następne kroki

* Więcej informacji na temat Centrum IoT [urządzenia do chmury do obsługi komunikatów][lnk-d2c].
* Więcej informacji na temat Centrum IoT [wiadomości chmury do urządzenia][lnk-c2d].

[lnk-azure-iot]: iot-hub-what-is-azure-iot.md
[lnk-iot-hub-overview]: iot-hub-what-is-iot-hub.md
[lnk-d2c]: iot-hub-devguide-messages-d2c.md
[lnk-c2d]: iot-hub-devguide-messages-c2d.md
[lnk-c2d-guidance]: iot-hub-devguide-c2d-guidance.md
[lnk-d2c-guidance]: iot-hub-devguide-d2c-guidance.md