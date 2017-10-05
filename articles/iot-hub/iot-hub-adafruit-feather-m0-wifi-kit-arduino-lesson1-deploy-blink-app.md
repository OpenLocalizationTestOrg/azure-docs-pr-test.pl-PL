---
title: "Nawiązać Arduino Azure IoT — Lekcja 1: Wdrażanie aplikacji | Dokumentacja firmy Microsoft"
description: "Klonowanie przykładowej aplikacji Arduino z serwisu GitHub, a następnie uruchom gulp, aby wdrożyć tę aplikację z Adafruit piór M0 sieci Wi-Fi. Ta przykładowa aplikacja miganie interfejs GPIO"
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
ms.openlocfilehash: 4431808ac6182d194e841c087c8f89f1a12b1911
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="create-and-deploy-the-blink-application"></a>Tworzenie i wdrażanie aplikacji blink
## <a name="what-you-will-do"></a>Będzie wykonywać
Klonowanie Arduino przykładowej aplikacji z usługi GitHub i wdrażania przykładowej aplikacji do tablicy Adafruit piór M0 sieci Wi-Fi Arduino za pomocą narzędzia gulp. Migania aplikacji przykładowy interfejs GPIO #13 na barod PRZEPROWADZONY co dwie sekundy.

Jeśli masz problemy, poszukaj rozwiązania [Rozwiązywanie problemów z strony][troubleshooting-page].

## <a name="what-you-will-learn"></a>Co dowiesz się
* Jak wdrożyć i uruchomić aplikację przykładową na tablicy Arduino.

## <a name="what-you-need"></a>Co jest potrzebne
Pomyślnie zakończono następujące operacje:

* [Skonfiguruj urządzenie][configure-your-device]
* [Pobierz narzędzia][get-the-tools]

## <a name="open-the-sample-application"></a>Otwórz aplikację przykładową
Aby otworzyć aplikację przykładową, wykonaj następujące kroki:

1. Klonowanie repozytorium przykładowej z serwisu GitHub, uruchamiając następujące polecenie:

   ```bash
   git clone https://github.com/Azure-Samples/iot-hub-c-feather-m0-getting-started.git
   ```
2. Otwórz przykładowej aplikacji w programie Visual Studio Code, uruchamiając następujące polecenia:

   ```bash
   cd iot-hub-c-feather-m0-getting-started
   cd Lesson1
   code .
   ```

   ![Struktura repozytorium][repo-structure]

`app.ino` w pliku `app` podfolder jest plik źródłowy klucza, który zawiera kod służący do kontroli LED.

### <a name="install-application-dependencies"></a>Zainstaluj zależności aplikacji
Zainstaluj biblioteki oraz inne moduły potrzebnych dla aplikacji przykładowej, uruchamiając następujące polecenie:

```bash
npm install
```

## <a name="configure-the-device-connection"></a>Skonfiguruj połączenie z urządzeniem
Aby skonfigurować połączenie z urządzeniem, wykonaj następujące kroki:

1. Uzyskaj portu szeregowego urządzenia z odnajdywania urządzenia interfejsu wiersza polecenia:

   ```bash
   devdisco list --usb
   ```

   Należy wyświetlić dane wyjściowe podobne do następujących i Znajdź usb COM port tablicy Arduino: ![odnajdywania urządzeń][device-discovery]

2. Otwórz plik `config.json` w folderze lekcji i Dodaj wartość znaleziony numer portu COM:

   ```json
   {
       "device_port" : "COM1"
   }
   ```
   ![Config.JSON][config-json]
   > [!NOTE]
   > Dla portu COM na platformie systemu Windows ma format `COM1, COM2, ...`. System macOS lub Ubuntu rozpoczyna się od `/dev/`.

## <a name="deploy-and-run-the-sample-application"></a>Wdrażanie i uruchamianie przykładowej aplikacji
### <a name="install-the-required-tools-for-your-arduino-board"></a>Zainstaluj narzędzia wymagane dla tablicy Arduino

Zainstaluj zestaw SDK Centrum IoT Azure dla tablicy Arduino, uruchamiając następujące polecenie:

```bash
gulp install-tools
```

To zadanie może zająć dużo czasu, w zależności od połączenia sieciowego.

> [!NOTE]
> Zakończ uruchomione wystąpienie Arduino IDE podczas uruchamiania zadania gulp: `install-tools`, `run`.

### <a name="deploy-and-run-the-sample-app"></a>Wdrażanie i uruchamianie przykładowej aplikacji
Wdrażanie i uruchamianie aplikacji przykładowej, uruchamiając następujące polecenie:

```bash
gulp run

# You can monitor the serial port by running listen task:
gulp listen

# Or you can combine above two gulp tasks into one:
gulp run --listen
```

### <a name="verify-the-app-works"></a>Weryfikowanie działania aplikacji
Jeśli nie widzisz migający LED, zobacz [przewodnik rozwiązywania problemów] [ troubleshooting-page] dla rozwiązania typowych problemów.

![Migający LED][led-blinking]

## <a name="summary"></a>Podsumowanie
Zainstalowaniu wymagane narzędzia do pracy z tablicy Arduino i przykładowej aplikacji do tablicy Arduino miga LED wdrożone. Teraz można tworzyć, wdrażać i uruchom inną aplikację przykładową, która łączy tablicy Arduino Centrum IoT Azure do wysyłania i odbierania wiadomości.

## <a name="next-steps"></a>Następne kroki
[Pobierz narzędzia Azure][get-the-azure-tools]

<!-- Images and links -->

[troubleshooting-page]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-troubleshooting.md
[configure-your-device]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson1-configure-your-device.md
[get-the-tools]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson1-get-the-tools-win32.md
[repo-structure]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson1/vscode-blink-arduino-mac.png
[device-discovery]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson1/device_discovery.png
[config-json]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson1/vscode-config-mac.png
[led-blinking]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson1/led_blinking.png
[get-the-azure-tools]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson2-get-azure-tools-win32.md