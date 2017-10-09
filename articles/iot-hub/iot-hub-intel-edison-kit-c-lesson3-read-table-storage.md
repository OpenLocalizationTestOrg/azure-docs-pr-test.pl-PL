---
title: "Connect Intel Edison (C) tooAzure IoT — lekcji 3: monitorowanie wiadomości | Dokumentacja firmy Microsoft"
description: "Monitorowanie wiadomości powitania od urządzenia do chmury, ponieważ są one zapisywane tooyour magazynu tabel Azure."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "dane w chmurze hello, zbierania danych w chmurze, usługi w chmurze iot, dane iot"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-intel-edison-kit-c-get-started
ms.assetid: cad545c3-dd88-486c-a663-d587a924ccd4
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 2679b22f2987f77ecd1eea03044ed8ea03bf73f8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="read-messages-persisted-in-azure-storage"></a>Odczytywanie wiadomości utrwalane w magazynie Azure
## <a name="what-you-will-do"></a>Będzie wykonywać
Monitor hello urządzenia do chmury wiadomości, które są wysyłane z Centrum IoT tooyour Intel Edison jako wiadomości powitania są zapisywane tooyour magazynu tabel Azure. Jeśli masz problemy, poszukaj rozwiązania na powitania [Rozwiązywanie problemów z strony][troubleshooting].

## <a name="what-you-will-learn"></a>Co dowiesz się
W tym artykule dowiesz się, jak toouse wiadomości tooread zadanie odczytu wiadomości powitania od gulp utrwalone w magazynem tabel Azure.

## <a name="what-you-need"></a>Co jest potrzebne
Przed rozpoczęciem tego procesu, musi pomyślnie ukończył [Uruchom hello Azure migania przykładowej aplikacji na Intel Edison][run-the-azure-blink-sample-application-on-intel-edison].

## <a name="read-new-messages-from-your-storage-account"></a>Odczytaj wiadomości z konta magazynu
W poprzednim artykule hello na Edison uruchomiono przykładowej aplikacji. aplikacja przykładowa Hello wysyłane Centrum Azure IoT tooyour wiadomości. Centrum IoT tooyour wysłane wiadomości powitania są przechowywane do magazynu tabel Azure za pomocą hello Azure funkcji aplikacji. Należy hello magazynu Azure połączenia ciąg tooread wiadomości z magazynu tabel Azure.

tooread wiadomości przechowywanych w swoim magazynem tabel Azure, wykonaj następujące kroki:

1. Pobierz ciąg połączenia hello, uruchamiając następujące polecenia hello:

   ```bash
   az storage account list -g iot-sample --query [].name
   az storage account show-connection-string -g iot-sample -n {storage name}
   ```

   Witaj pierwsze polecenie pobiera hello `storage name` używanej w hello drugiego polecenia tooget hello parametry połączenia. Użyj `iot-sample` jako wartość hello `{resource group name}` Jeśli hello wartość nie zostanie zmieniona.
2. Plik konfiguracji Otwórz hello `config-edison.json` w programie Visual Studio Code, uruchamiając następujące polecenie hello:

   ```bash
   # For Windows command prompt
   code %USERPROFILE%\.iot-hub-getting-started\config-edison.json

   # For MacOS or Ubuntu
   code ~/.iot-hub-getting-started/config-edison.json
   ```
3. Zastąp `[Azure storage connection string]` przy użyciu parametrów połączenia hello uzyskano w kroku 1.
4. Zapisz hello `config-edison.json` pliku.
5. Ponowne wysłanie wiadomości i je odczytać z magazynu tabel Azure, uruchamiając następujące polecenie hello:

   ```bash
   gulp run --read-storage
   ```

   Witaj logiki odczytu z magazynu tabel Azure znajduje się w hello `azure-table.js` pliku.

   ![run--gulp odczytu magazynu][gulp run]

## <a name="summary"></a>Podsumowanie
Pomyślnie zostały połączone z Centrum IoT tooyour Edison w chmurze hello i używane wiadomości powitania od migania przykładowej aplikacji toosend urządzenia do chmury. Możesz również hello Azure funkcji aplikacji toostore przychodzące IoT Centrum wiadomości tooyour magazynu tabel Azure. Teraz można wysłać wiadomości chmury do urządzenia z Twojej tooEdison Centrum IoT.

## <a name="next-steps"></a>Następne kroki
[Uruchom tooreceive aplikacji przykładowej wiadomości chmury do urządzenia][receive-cloud-to-device-messages]
<!-- Images and links -->

[troubleshooting]: iot-hub-intel-edison-kit-c-troubleshooting.md
[run-the-azure-blink-sample-application-on-intel-edison]: iot-hub-intel-edison-kit-c-lesson3-run-azure-blink.md
[gulp run]: media/iot-hub-intel-edison-lessons/lesson3/gulp_read_message_c.png
[receive-cloud-to-device-messages]: iot-hub-intel-edison-kit-c-lesson4-send-cloud-to-device-messages.md