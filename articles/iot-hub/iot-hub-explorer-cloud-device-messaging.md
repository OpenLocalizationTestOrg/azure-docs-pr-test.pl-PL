---
title: "urządzenie chmury Azure IoT Hub aaaManage wiadomości z Centrum iothub explorer | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toouse hello Centrum iothub explorer interfejsu wiersza polecenia narzędzia toomonitor urządzenia toocloud (D2C) wiadomości i wysyłać chmury toodevice (C2D) w usłudze Azure IoT Hub."
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: "Centrum iothub Eksploratorze chmury urządzenia wiadomości, toodevice chmury Centrum iot, chmury toodevice obsługi wiadomości"
ms.assetid: 04521658-35d3-4503-ae48-51d6ad3c62cc
ms.service: iot-hub
ms.devlang: arduino
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/24/2017
ms.author: xshi
ms.openlocfilehash: 741383b5631714cc2fef3309541fd2117aa7824c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="use-iothub-explorer-toosend-and-receive-messages-between-your-device-and-iot-hub"></a>Użyj Eksploratora Centrum iothub toosend i odbieranie komunikatów między urządzeniem a Centrum IoT

![Diagram end-to-end](media/iot-hub-get-started-e2e-diagram/2.png)

[!INCLUDE [iot-hub-get-started-note](../../includes/iot-hub-get-started-note.md)]

[Centrum iothub explorer](https://github.com/azure/iothub-explorer) ma kilka poleceń, który ułatwia zarządzanie Centrum IoT. Ten samouczek koncentruje się na temat toosend explorer Centrum iothub toouse i odbieranie komunikatów między urządzeniem i Centrum IoT.

## <a name="what-you-will-learn"></a>Co dowiesz się

Dowiesz się, jak toouse explorer Centrum iothub toomonitor urządzenia do chmury wiadomości i toosend wiadomości chmury do urządzenia. Komunikaty urządzenia do chmury można dane czujników, że urządzenie zbiera dane, a następnie wysyła tooyour Centrum IoT. Komunikaty chmury do urządzenia może być poleceń Centrum IoT i wysyła tooblink urządzenia tooyour LED, który jest tooyour podłączonego urządzenia.

## <a name="what-you-will-do"></a>Będzie wykonywać

- Użyj Eksploratora Centrum iothub toomonitor urządzenia do chmury wiadomości.
- Użyj Eksploratora Centrum iothub toosend chmury do urządzenia wiadomości.

## <a name="what-you-need"></a>Co jest potrzebne

- Samouczek [skonfigurować Twoje urządzenie](iot-hub-raspberry-pi-kit-node-get-started.md) ukończone, która obejmuje hello następujące wymagania:
  - Aktywna subskrypcja platformy Azure.
  - Centrum Azure IoT w ramach Twojej subskrypcji.
  - Aplikacja klienta, która wysyła komunikaty tooyour Azure IoT hub.
- Eksplorator Centrum iothub. ([Zainstalować explorer Centrum iothub](https://github.com/azure/iothub-explorer))

## <a name="monitor-device-to-cloud-messages"></a>Monitorowanie wiadomości urządzenia do chmury

toomonitor wiadomości, które są wysyłane z Centrum IoT tooyour urządzenie, wykonaj następujące kroki:

1. Otwórz okno konsoli.
1. Uruchom następujące polecenie hello:

   ```bash
   iothub-explorer monitor-events <device-id> --login "<IoTHubConnectionString>"
   ```

   > [!Note]
   > Pobierz `<device-id>` i `<IoTHubConnectionString>` z Centrum IoT. Upewnij się, że po zakończeniu samouczka poprzedniej hello. Możesz toouse `iothub-explorer monitor-events <device-id> --login "HostName=<my-hub>.azure-devices.net;SharedAccessKeyName=<my-policy>;SharedAccessKey=<my-policy-key>"` Jeśli masz `HostName`, `SharedAccessKeyName` i `SharedAccessKey`.

## <a name="send-cloud-to-device-messages"></a>Wysyłanie komunikatów z chmury do urządzeń

toosend wiadomości z urządzenia tooyour Centrum IoT, wykonaj następujące kroki:

1. Otwórz okno konsoli.
1. Uruchom sesję w Centrum IoT, uruchamiając następujące polecenie hello:

   ```bash
   iothub-explorer login `<IoTHubConnectionString>`
   ```

1. Wyślij komunikat tooyour urządzenia, uruchamiając następujące polecenie hello:

   ```bash
   iothub-explorer send <device-id> <message>
   ```

polecenie Hello miga hello LED tooyour podłączonych urządzeń i wysyła urządzenia tooyour wiadomość hello.

> [!Note]
> Nie istnieje potrzeba dla toosend urządzenia hello Centrum IoT potwierdzenia oddzielne polecenie tooyour wstecz po otrzymaniu wiadomości powitania.

## <a name="next-steps"></a>Następne kroki

Znasz już jak toomonitor urządzenia do chmury wiadomości i wysyłanie komunikatów chmury do urządzenia między urządzenia IoT i Centrum IoT Azure.

[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]
