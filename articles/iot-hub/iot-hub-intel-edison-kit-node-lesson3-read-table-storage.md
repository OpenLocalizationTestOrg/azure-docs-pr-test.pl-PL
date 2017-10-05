---
title: "Nawiązać Edison firmy Intel (węzeł) Azure IoT — lekcji 3: monitorowanie wiadomości | Dokumentacja firmy Microsoft"
description: "Monitorowanie wiadomości urządzenia do chmury, ponieważ są one zapisywane do magazynu tabel Azure."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "dane w chmurze, zbierania danych w chmurze, usługi w chmurze iot, dane iot"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-intel-edison-kit-node-get-started
ms.assetid: fa2c7efe-7e34-4e39-bb70-015c15ac69ed
ms.service: iot-hub
ms.devlang: nodejs
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: c1a59227cd2bf9d2c9bcaa4212dd5127a95e2779
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="read-messages-persisted-in-azure-storage"></a>Odczytywanie wiadomości utrwalane w magazynie Azure
## <a name="what-you-will-do"></a>Będzie wykonywać
Monitorowanie komunikatów urządzenia do chmury, które są wysyłane z Intel Edison do Centrum IoT, jak komunikaty są zapisywane do magazynu tabel Azure. Jeśli masz problemy, poszukaj rozwiązania [Rozwiązywanie problemów z strony][troubleshooting].

## <a name="what-you-will-learn"></a>Co dowiesz się
W tym artykule dowiesz się, jak używać zadań odczytu komunikatu gulp odczytywać komunikaty utrwalone w magazynie tabel Azure.

## <a name="what-you-need"></a>Co jest potrzebne
Przed rozpoczęciem tego procesu, musi pomyślnie ukończył [Uruchom przykładową aplikację Azure migania na Intel Edison][run-the-azure-blink-sample-application-on-intel-edison].

## <a name="read-new-messages-from-your-storage-account"></a>Odczytaj wiadomości z konta magazynu
W poprzednim artykule uruchomiono na Edison przykładowej aplikacji. Komunikaty przykładowej aplikacji wysyłane do Centrum Azure IoT. Komunikaty wysyłane do Centrum IoT są przechowywane w magazynie tabel Azure przy użyciu aplikacji Azure — funkcja. Należy parametry połączenia magazynu Azure do czytania wiadomości z magazynu tabel Azure.

Aby odczytać wiadomości przechowywanych w magazynie tabel Azure, wykonaj następujące kroki:

1. Pobierz ciąg połączenia, uruchamiając następujące polecenia:

   ```bash
   az storage account list -g iot-sample --query [].name
   az storage account show-connection-string -g iot-sample -n {storage name}
   ```

   Pierwsze polecenie pobiera `storage name` używanej w drugiego polecenia można pobrać ciągu połączenia. Użyj `iot-sample` jako wartość `{resource group name}` Jeśli wartości nie można zmienić.
2. Otwórz plik konfiguracji `config-edison.json` w programie Visual Studio Code, uruchamiając następujące polecenie:

   ```bash
   # For Windows command prompt
   code %USERPROFILE%\.iot-hub-getting-started\config-edison.json

   # For MacOS or Ubuntu
   code ~/.iot-hub-getting-started/config-edison.json
   ```
3. Zastąp `[Azure storage connection string]` z parametrami połączenia uzyskano w kroku 1.
4. Zapisz `config-edison.json` pliku.
5. Ponowne wysłanie wiadomości i je odczytać z magazynu tabel Azure, uruchamiając następujące polecenie:

   ```bash
   gulp run --read-storage
   ```

   Logika do odczytu z magazynu tabel Azure znajduje się w `azure-table.js` pliku.

   ![run--gulp odczytu magazynu][gulp run]

## <a name="summary"></a>Podsumowanie
Został pomyślnie połączony Edison Centrum IoT w chmurze i używany migania przykładowej aplikacji do wysyłania wiadomości urządzenia do chmury. Aplikacji Azure — funkcja jest również używane do przechowywania wiadomości przychodzących Centrum IoT do magazynu tabel Azure. Teraz można wysłać wiadomości chmury do urządzenia z Centrum IoT na Edison.

## <a name="next-steps"></a>Następne kroki
[Uruchom przykładową aplikację do odbierania wiadomości chmury do urządzenia][receive-cloud-to-device-messages]
<!-- Images and links -->

[troubleshooting]: iot-hub-intel-edison-kit-node-troubleshooting.md
[run-the-azure-blink-sample-application-on-intel-edison]: iot-hub-intel-edison-kit-node-lesson3-run-azure-blink.md
[gulp run]: media/iot-hub-intel-edison-lessons/lesson3/gulp_read_message.png
[receive-cloud-to-device-messages]: iot-hub-intel-edison-kit-node-lesson4-send-cloud-to-device-messages.md