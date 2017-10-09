---
title: "Connect Arduino (C) tooAzure IoT — lekcji 3: Tabela magazynów | Dokumentacja firmy Microsoft"
description: "Monitorowanie wiadomości powitania od urządzenia do chmury, ponieważ są one zapisywane tooyour magazynu tabel Azure."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "dane w chmurze hello, zbierania danych w chmurze, usługi w chmurze iot, dane iot"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-adafruit-feather-m0-wifi-kit-arduino-get-started
ms.assetid: 386083e0-0dbb-48c0-9ac2-4f8fb4590772
ms.service: iot-hub
ms.devlang: arduino
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 9fef18bc9e780e78d95f0c643a5f193125130a5b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="read-messages-persisted-in-azure-storage"></a>Odczytywanie wiadomości utrwalane w magazynie Azure
## <a name="what-you-will-do"></a>Będzie wykonywać
Monitor hello urządzenia do chmury wiadomości, które są wysyłane z Centrum IoT tooyour tablicy Adafruit piór M0 sieci Wi-Fi Arduino jako wiadomości powitania są zapisywane tooyour magazynu tabel Azure.

Jeśli masz problemy, poszukaj rozwiązania na powitania [Rozwiązywanie problemów z strony][troubleshooting].

## <a name="what-you-will-learn"></a>Co dowiesz się
W tym artykule dowiesz się, jak toouse wiadomości tooread zadanie odczytu wiadomości powitania od gulp utrwalone w magazynem tabel Azure.

## <a name="what-you-need"></a>Co jest potrzebne
Przed rozpoczęciem tego procesu, musi pomyślnie ukończył [Uruchom hello Azure migania przykładowej aplikacji na tablicy Arduino][run-blink-application].

## <a name="read-new-messages-from-your-storage-account"></a>Odczytaj wiadomości z konta magazynu
W poprzednim artykule hello na tablicy Arduino uruchomiono przykładowej aplikacji. aplikacja przykładowa Hello wysyłane Centrum Azure IoT tooyour wiadomości. Centrum IoT tooyour wysłane wiadomości powitania są przechowywane do magazynu tabel Azure za pomocą hello Azure funkcji aplikacji. Należy hello magazynu Azure połączenia ciąg tooread wiadomości z magazynu tabel Azure.

tooread wiadomości przechowywanych w swoim magazynem tabel Azure, wykonaj następujące kroki:

1. Pobierz ciąg połączenia hello, uruchamiając następujące polecenia hello:

   ```bash
   az storage account list -g iot-sample --query [].name
   az storage account show-connection-string -g iot-sample -n {storage name}
   ```

   Witaj pierwsze polecenie pobiera hello `storage name` używanej w hello drugiego polecenia tooget hello parametry połączenia. Użyj `iot-sample` jako wartość hello `{resource group name}` Jeśli hello wartość nie zostanie zmieniona.
2. Plik konfiguracji Otwórz hello `config-arduino.json` w programie Visual Studio Code, uruchamiając następujące polecenie hello:

   ```bash
   # For Windows command prompt
   code %USERPROFILE%\.iot-hub-getting-started\config-arduino.json

   # For MacOS or Ubuntu
   code ~/.iot-hub-getting-started/config-arduino.json
   ```
3. Zastąp `[Azure storage connection string]` przy użyciu parametrów połączenia hello uzyskano w kroku 1.
4. Zapisz hello `config-arduino.json` pliku.
5. Ponowne wysłanie wiadomości i je odczytać z magazynu tabel Azure, uruchamiając następujące polecenie hello:

   ```bash
   gulp run --read-storage

   # You can monitor hello serial port by running listen task:
   gulp listen

   # Or you can combine above two gulp tasks into one:
   gulp run --read-storage --listen
   ```

   Witaj logiki odczytu z magazynu tabel Azure znajduje się w hello `azure-table.js` pliku.

   ![run--gulp odczytu magazynu][gulp-run]

## <a name="summary"></a>Podsumowanie
Pomyślnie zostały połączone z Centrum IoT tooyour Arduino tablicy w chmurze hello i używane wiadomości powitania od migania przykładowej aplikacji toosend urządzenia do chmury. Możesz również hello Azure funkcji aplikacji toostore przychodzące IoT Centrum wiadomości tooyour magazynu tabel Azure. Teraz można wysłać wiadomości chmury do urządzenia z Twojej tooyour Centrum IoT Arduino tablicy.

## <a name="next-steps"></a>Następne kroki
[Wysyłanie komunikatów chmury do urządzenia][send-cloud-to-device-messages]
<!-- Images and links -->

[troubleshooting]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-troubleshooting.md
[run-blink-application]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson3-run-azure-blink.md
[gulp-run]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson3/gulp_read_message_arduino.png
[send-cloud-to-device-messages]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson4-send-cloud-to-device-messages.md