---
title: "Połącz Arduino tooAzure IoT — Lekcja 1: Wdrażanie aplikacji | Dokumentacja firmy Microsoft"
description: "Klonowanie hello przykładowej Arduino aplikacji z usługi GitHub i uruchomić gulp toodeploy tooyour tej aplikacji Adafruit piór M0 sieci Wi-Fi. Miga, to przykładowa aplikacja hello interfejs GPIO"
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "arduino doprowadziły projektów, arduino doprowadziły migania, kod migania arduino doprowadziły, program migania arduino, arduino migania przykład"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-adafruit-feather-m0-wifi-kit-arduino-get-started
ms.assetid: b0a7d076-d580-4686-9f7d-c0712750b615
ms.service: iot-hub
ms.devlang: arduino
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 5bf8e4ae88e070aeacf34bfc43b8d2daeeb1a2fa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-deploy-hello-blink-application"></a>Tworzenie i wdrażanie aplikacji migania hello
## <a name="what-you-will-do"></a>Będzie wykonywać
Klonowanie hello przykładowej Arduino aplikacji z usługi GitHub i użyj hello gulp narzędzie toodeploy hello przykładowej aplikacji tooyour Adafruit piór M0 sieci Wi-Fi Arduino tablicy. Witaj przykładowej aplikacji migania Witaj interfejs GPIO #13 na barod PRZEPROWADZONY co dwie sekundy.

Jeśli masz problemy, poszukaj rozwiązania na powitania [Rozwiązywanie problemów z strony][troubleshooting-page].

## <a name="what-you-will-learn"></a>Co dowiesz się
* Jak toodeploy i wykonywania hello przykładowej aplikacji na tablicy Arduino.

## <a name="what-you-need"></a>Co jest potrzebne
Użytkownik pomyślnie ukończona hello następujące operacje:

* [Skonfiguruj urządzenie][configure-your-device]
* [Pobierz narzędzia hello][get-the-tools]

## <a name="open-hello-sample-application"></a>Otwórz hello przykładowej aplikacji
Witaj tooopen przykładowej aplikacji, wykonaj następujące kroki:

1. Klonuj repozytorium przykładowej hello z serwisu GitHub, uruchamiając następujące polecenie hello:

   ```bash
   git clone https://github.com/Azure-Samples/iot-hub-c-feather-m0-getting-started.git
   ```
2. Otwórz hello przykładowej aplikacji w programie Visual Studio Code, uruchamiając następujące polecenia hello:

   ```bash
   cd iot-hub-c-feather-m0-getting-started
   cd Lesson1
   code .
   ```

   ![Struktura repozytorium][repo-structure]

Witaj `app.ino` pliku w hello `app` podfolder to plik klucza źródła hello, który zawiera hello kodu toocontrol hello LED.

### <a name="install-application-dependencies"></a>Zainstaluj zależności aplikacji
Zainstaluj hello bibliotek i inne moduły potrzebnych dla aplikacji przykładowej hello, uruchamiając następujące polecenie hello:

```bash
npm install
```

## <a name="configure-hello-device-connection"></a>Skonfiguruj połączenie z urządzeniem hello
tooconfigure hello połączenie z urządzeniem, wykonaj następujące kroki:

1. Uzyskaj hello portu szeregowego hello urządzenia z hello urządzenia odnajdywania interfejsu wiersza polecenia:

   ```bash
   devdisco list --usb
   ```

   Należy wyświetlone informacje podobne następujących toohello i Znajdź hello usb COM port tablicy Arduino: ![odnajdywania urządzeń][device-discovery]

2. Witaj Otwórz plik `config.json` w hello lekcji folderu i Dodaj wartości hello hello znaleziono numer portu COM:

   ```json
   {
       "device_port" : "COM1"
   }
   ```
   ![Config.JSON][config-json]
   > [!NOTE]
   > Dla portu hello COM, na platformie systemu Windows ma hello format `COM1, COM2, ...`. System macOS lub Ubuntu rozpoczyna się od `/dev/`.

## <a name="deploy-and-run-hello-sample-application"></a>Wdrażanie i uruchamianie hello przykładowej aplikacji
### <a name="install-hello-required-tools-for-your-arduino-board"></a>Zainstaluj narzędzia hello wymagane dla tablicy Arduino

Zainstaluj hello Azure IoT Hub SDK dla tablicy Arduino, uruchamiając następujące polecenie hello:

```bash
gulp install-tools
```

To zadanie może potrwać długo toocomplete, w zależności od połączenia sieciowego.

> [!NOTE]
> Zakończ hello uruchomione wystąpienie Arduino IDE, podczas uruchamiania zadania gulp: `install-tools`, `run`.

### <a name="deploy-and-run-hello-sample-app"></a>Wdrażanie i uruchamianie hello przykładowej aplikacji
Wdrażanie i uruchamianie aplikacji przykładowej hello, uruchamiając następujące polecenie hello:

```bash
gulp run

# You can monitor hello serial port by running listen task:
gulp listen

# Or you can combine above two gulp tasks into one:
gulp run --listen
```

### <a name="verify-hello-app-works"></a>Weryfikowanie działania aplikacji hello
Jeśli nie widzisz migający hello LED, zobacz hello [przewodnik rozwiązywania problemów] [ troubleshooting-page] dla rozwiązania toocommon problemów.

![Migający LED][led-blinking]

## <a name="summary"></a>Podsumowanie
Zainstalowaniu hello wymagane narzędzia toowork z tablicy Arduino i przykładowej aplikacji tooyour Arduino tablicy tooblink hello LED wdrożone. Można teraz tworzenie, wdrażanie i uruchom inną aplikację przykładową, która łączy się z tooAzure tablicy Arduino toosend Centrum IoT i odbierania wiadomości.

## <a name="next-steps"></a>Następne kroki
[Pobierz hello Azure narzędzia][get-the-azure-tools]

<!-- Images and links -->

[troubleshooting-page]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-troubleshooting.md
[configure-your-device]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson1-configure-your-device.md
[get-the-tools]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson1-get-the-tools-win32.md
[repo-structure]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson1/vscode-blink-arduino-mac.png
[device-discovery]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson1/device_discovery.png
[config-json]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson1/vscode-config-mac.png
[led-blinking]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson1/led_blinking.png
[get-the-azure-tools]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson2-get-azure-tools-win32.md