---
title: "Connect Arduino (C) tooAzure IoT — lekcji 3: uruchamianie przykładowych | Dokumentacja firmy Microsoft"
description: "Wdrażanie i uruchamianie przykładowych aplikacji tooAdafruit piór M0 Wi-Fi, która wysyła Centrum IoT tooyour wiadomości i miganie hello LED."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "usługi w chmurze iot arduino wysyłania toocloud danych"
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
ms.openlocfilehash: ddca015a3655f8a1a9de2a00e718ec0d28a5affb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="run-a-sample-application-toosend-device-to-cloud-messages"></a>Uruchom toosend aplikacji przykładowej wiadomości urządzenia do chmury
## <a name="what-you-will-do"></a>Będzie wykonywać
W tym artykule opisano sposób toodeploy i uruchom przykładową aplikację na Twojej Adafruit piór M0 sieci Wi-Fi Arduino płycie tego Centrum IoT wysyła komunikaty tooyour.

Jeśli masz problemy, poszukaj rozwiązania na powitania [Rozwiązywanie problemów z strony][troubleshooting].

## <a name="what-you-will-learn"></a>Co dowiesz się
Dowiesz się, jak toouse hello system gulp toodeploy narzędzia i uruchomić hello przykładowej aplikacji Arduino na tablicy Arduino.

## <a name="what-you-need"></a>Co jest potrzebne
* Przed rozpoczęciem tego zadania musi pomyślnie ukończył [tworzenie aplikacji funkcji platformy Azure i magazynu konta tooprocess i Magazyn Centrum IoT wiadomości][process-and-store-iot-hub-messages].

## <a name="get-your-iot-hub-and-device-connection-strings"></a>Pobrać parametry połączenia koncentratora i urządzenia IoT
Witaj ciąg połączenia urządzenia jest używane tooconnect Centrum IoT tooyour Arduino tablicy. Parametry połączenia Centrum IoT Hello są używane tooconnect tożsamości IoT hub toohello urządzenia reprezentujący Arduino Twojego płycie w Centrum IoT hello.

* Lista z centra IoT w grupie zasobów, uruchamiając następujące polecenie z wiersza polecenia platformy Azure hello:

```bash
az iot hub list -g iot-sample --query [].name
```

Użyj `iot-sample` jako wartość hello `{resource group name}` Jeśli hello wartość nie zostanie zmieniona.

* Pobierz ciąg połączenia Centrum IoT hello, uruchamiając następujące polecenie z wiersza polecenia platformy Azure hello:

```bash
az iot hub show-connection-string --name {my hub name}
```

`{my hub name}`to nazwa hello określone podczas tworzenia Centrum IoT i zarejestrowana Arduino tablicy.

* Pobierz ciąg połączenia urządzenia hello, uruchamiając następujące polecenie hello:

```bash
az iot device show-connection-string --hub-name {my hub name} --device-id mym0wifi
```

Użyj `mym0wifi` jako wartość hello `{device id}` Jeśli hello wartość nie zostanie zmieniona.
## <a name="configure-hello-device-connection"></a>Skonfiguruj połączenie z urządzeniem hello
tooconfigure hello połączenie z urządzeniem, wykonaj następujące kroki:

1. Uzyskaj hello portu szeregowego hello urządzenia z hello urządzenia odnajdywania interfejsu wiersza polecenia:

   ```bash
   devdisco list --usb
   ```

   Należy wyświetlone informacje podobne następujących toohello i Znajdź hello usb COM port tablicy Arduino:

   ![Odnajdywanie urządzeń][device-discovery]

2. Witaj Otwórz plik `config.json` w hello lekcji folderu i Dodaj wartości hello hello znaleziono numer portu COM:

   ```json
   {
       "device_port" : "COM1"
   }
   ```

   ![Config.JSON][config-json]

   > [!NOTE]
   > Dla portu hello COM, na platformie systemu Windows ma hello format `COM1, COM2, ...`. System macOS lub Ubuntu rozpoczyna się od `/dev/`.

3. Inicjowanie pliku konfiguracji hello, uruchamiając następujące polecenia hello:

   ```bash
   npm install
   gulp init
   gulp install-tools
   ```
4. Plik konfiguracji urządzenia Otwórz hello `config-arduino.json` w programie Visual Studio Code, uruchamiając następujące polecenie hello:

   ```bash
   # For Windows command prompt
   code %USERPROFILE%\.iot-hub-getting-started\config-arduino.json

   # For MacOS or Ubuntu
   code ~/.iot-hub-getting-started/config-arduino.json
   ```

   ![arduino.json konfiguracji][config-arduino-json]

5. Wprowadź następujące elementy zastępcze w hello hello `config-arduino.json` pliku:

   * Zastąp **[SSID sieci Wi-Fi]** o identyfikatorze SSID sieci Wi-Fi, który połączony toohello Internet.
   * Zastąp **[sieci Wi-Fi hasło]** hasła sieci Wi-Fi. Jeśli sieci Wi-Fi nie wymagają hasła, należy usunąć ciąg hello.
   * Zastąp **[parametry połączenia urządzenia IoT]** z hello `device connection string` uzyskaną.
   * Zastąp **[parametry połączenia Centrum IoT]** z hello `iot hub connection string` uzyskaną.

   > [!NOTE]
   > Nie ma potrzeby `azure_storage_connection_string` w tym artykule. Zachować, ponieważ jest.

## <a name="deploy-and-run-hello-sample-application"></a>Wdrażanie i uruchamianie hello przykładowej aplikacji
Wdrażanie i uruchamianie aplikacji przykładowej hello na tablicy Arduino, uruchamiając następujące polecenie hello:

```bash
gulp run
# You can monitor hello serial port by running listen task:
gulp listen

# Or you can combine above two gulp tasks into one:
gulp run --listen
```

> [!NOTE]
> Witaj domyślne gulp zadanie jest uruchamiane `install-tools` i `run` zadania po kolei. Gdy możesz [wdrożonych aplikacji migania hello][deployed-the-blink-app], oddzielnie uruchomiono tych zadań.

## <a name="verify-that-hello-sample-application-works"></a>Sprawdź, czy działa hello przykładowej aplikacji
Powinna zostać wyświetlona hello interfejs GPIO #0 lokalnego LED migający co dwie sekundy. Za każdym razem, gdy hello LED miga, hello przykładowej aplikacji wysyła z Centrum IoT tooyour wiadomości i sprawdza, czy tę wiadomość hello została pomyślnie wysłana tooyour Centrum IoT. Ponadto każdy komunikat odebrany przez Centrum IoT hello jest drukowany w oknie konsoli hello. Witaj przykładowej aplikacji kończy się automatycznie po wysłaniu wiadomości 20.

![Przykładowa aplikacja z wysłanych i odebranych komunikatów][sample-application-with-sent-and-received-messages]

## <a name="summary"></a>Podsumowanie
Zostały wdrożone i uruchom hello nowe migania przykładowej aplikacji w Centrum IoT tooyour Arduino tablicy toosend wiadomości urządzenia do chmury. Jak są one zapisywane na koncie magazynu toohello teraz monitorować wiadomości.

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