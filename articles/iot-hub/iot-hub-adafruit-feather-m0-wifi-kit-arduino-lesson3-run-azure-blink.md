---
title: "Connect Arduino (C) do Azure IoT — lekcji 3: uruchamianie przykładowych | Dokumentacja firmy Microsoft"
description: "Wdrażanie i uruchamianie przykładowej aplikacji do Adafruit piór M0 WiFi, który wysyła wiadomości do Centrum IoT i miganie LED."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "usługi w chmurze iot arduino wysyłania danych do chmury"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-adafruit-feather-m0-wifi-kit-arduino-get-started
ms.assetid: 92cce319-2b17-4c9b-889d-deac959e3e7c
ms.service: iot-hub
ms.devlang: arduino
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 0c17fe74dbd78abca955f7789a1674ed6333367f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="run-a-sample-application-to-send-device-to-cloud-messages"></a>Uruchom przykładową aplikację do wysyłania wiadomości urządzenia do chmury
## <a name="what-you-will-do"></a>Będzie wykonywać
W tym artykule opisano sposób wdrażania i uruchom przykładową aplikację na tablicy Adafruit piór M0 sieci Wi-Fi Arduino wysyłania komunikatów do Centrum IoT.

Jeśli masz problemy, poszukaj rozwiązania [Rozwiązywanie problemów z strony][troubleshooting].

## <a name="what-you-will-learn"></a>Co dowiesz się
Zostanie sposób użycia narzędzia gulp do wdrożenia i uruchomienia na tablicy Arduino Arduino przykładowej aplikacji.

## <a name="what-you-need"></a>Co jest potrzebne
* Przed rozpoczęciem tego zadania musi pomyślnie ukończył [tworzenia aplikacji funkcji platformy Azure i konto magazynu do przetwarzania i przechowywania wiadomości Centrum IoT][process-and-store-iot-hub-messages].

## <a name="get-your-iot-hub-and-device-connection-strings"></a>Pobrać parametry połączenia koncentratora i urządzenia IoT
Ciąg połączenia urządzenia jest używany do nawiązania tablicy Arduino Centrum IoT. Parametry połączenia Centrum IoT jest używany do nawiązania połączenia tożsamości tego urządzenia, który reprezentuje tablicy Arduino w Centrum IoT Centrum IoT.

* Lista z centra IoT w grupie zasobów, uruchamiając następujące polecenie z wiersza polecenia platformy Azure:

```bash
az iot hub list -g iot-sample --query [].name
```

Użyj `iot-sample` jako wartość `{resource group name}` Jeśli wartości nie można zmienić.

* Pobierz ciąg połączenia Centrum IoT, uruchamiając następujące polecenie z wiersza polecenia platformy Azure:

```bash
az iot hub show-connection-string --name {my hub name}
```

`{my hub name}`jest to nazwa określonej podczas tworzenia Centrum IoT i zarejestrowana Arduino tablicy.

* Pobierz ciąg połączenia urządzenia, uruchamiając następujące polecenie:

```bash
az iot device show-connection-string --hub-name {my hub name} --device-id mym0wifi
```

Użyj `mym0wifi` jako wartość `{device id}` Jeśli wartości nie można zmienić.
## <a name="configure-the-device-connection"></a>Skonfiguruj połączenie z urządzeniem
Aby skonfigurować połączenie z urządzeniem, wykonaj następujące kroki:

1. Uzyskaj portu szeregowego urządzenia z odnajdywania urządzenia interfejsu wiersza polecenia:

   ```bash
   devdisco list --usb
   ```

   Należy wyświetlić dane wyjściowe podobne do następujących i Znajdź usb COM port tablicy Arduino:

   ![Odnajdywanie urządzeń][device-discovery]

2. Otwórz plik `config.json` w folderze lekcji i Dodaj wartość znaleziony numer portu COM:

   ```json
   {
       "device_port" : "COM1"
   }
   ```

   ![Config.JSON][config-json]

   > [!NOTE]
   > Dla portu COM na platformie systemu Windows ma format `COM1, COM2, ...`. System macOS lub Ubuntu rozpoczyna się od `/dev/`.

3. Inicjowanie pliku konfiguracji, uruchamiając następujące polecenia:

   ```bash
   npm install
   gulp init
   gulp install-tools
   ```
4. Otwórz plik konfiguracji urządzenia `config-arduino.json` w programie Visual Studio Code, uruchamiając następujące polecenie:

   ```bash
   # For Windows command prompt
   code %USERPROFILE%\.iot-hub-getting-started\config-arduino.json

   # For MacOS or Ubuntu
   code ~/.iot-hub-getting-started/config-arduino.json
   ```

   ![arduino.json konfiguracji][config-arduino-json]

5. Wprowadź następujące elementy zastępcze w `config-arduino.json` pliku:

   * Zastąp **[SSID sieci Wi-Fi]** o identyfikatorze SSID sieci Wi-Fi, który jest połączony z Internetem.
   * Zastąp **[sieci Wi-Fi hasło]** hasła sieci Wi-Fi. Jeśli sieci Wi-Fi nie wymagają hasła, należy usunąć ciąg.
   * Zastąp **[parametry połączenia urządzenia IoT]** z `device connection string` uzyskaną.
   * Zastąp **[parametry połączenia Centrum IoT]** z `iot hub connection string` uzyskaną.

   > [!NOTE]
   > Nie ma potrzeby `azure_storage_connection_string` w tym artykule. Zachować, ponieważ jest.

## <a name="deploy-and-run-the-sample-application"></a>Wdrażanie i uruchamianie przykładowej aplikacji
Wdrażanie i uruchamianie przykładowej aplikacji na tablicy Arduino, uruchamiając następujące polecenie:

```bash
gulp run
# You can monitor the serial port by running listen task:
gulp listen

# Or you can combine above two gulp tasks into one:
gulp run --listen
```

> [!NOTE]
> Uruchamia zadanie gulp domyślne `install-tools` i `run` zadania po kolei. Gdy możesz [wdrożonych aplikacji migania][deployed-the-blink-app], oddzielnie uruchomiono tych zadań.

## <a name="verify-that-the-sample-application-works"></a>Sprawdź, czy działa przykładowej aplikacji
Powinien zostać wyświetlony interfejs GPIO #0 lokalnego LED migający przez co dwie sekundy. Za każdym razem, gdy LED miga, przykładowej aplikacji wysyła komunikat do Centrum IoT i sprawdza, czy wiadomość została pomyślnie wysłana do Centrum IoT. Ponadto każdy komunikat odebrany przez Centrum IoT jest drukowany w oknie konsoli. Przykładowa aplikacja kończy się automatycznie po wysłaniu wiadomości 20.

![Przykładowa aplikacja z wysłanych i odebranych komunikatów][sample-application-with-sent-and-received-messages]

## <a name="summary"></a>Podsumowanie
Został wdrożony i Uruchom nowe migania przykładową aplikację na tablicy Arduino do wysyłania wiadomości urządzenia do chmury do Centrum IoT. Wiadomości jest teraz monitorować, ponieważ są one zapisywane na koncie magazynu.

## <a name="next-steps"></a>Następne kroki
[Odczytywanie wiadomości utrwalane w magazynie Azure][read-messages-persisted-in-azure-storage]
<!-- Images and links -->

[troubleshooting]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-troubleshooting.md
[process-and-store-iot-hub-messages]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson3-deploy-resource-manager-template.md
[device-discovery]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson1/device_discovery.png
[config-json]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson1/vscode-config-mac.png
[config-arduino-json]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson3/config-arduino.png
[deployed-the-blink-app]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson1-deploy-blink-app.md
[sample-application-with-sent-and-received-messages]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson3/gulp_run_arduino.png
[read-messages-persisted-in-azure-storage]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson3-read-table-storage.md