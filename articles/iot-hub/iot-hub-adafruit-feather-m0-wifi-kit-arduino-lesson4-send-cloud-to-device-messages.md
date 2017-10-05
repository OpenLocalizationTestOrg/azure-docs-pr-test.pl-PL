---
title: "Nawiązać Arduino (C) Azure IoT — lekcji 4: chmury do urządzenia | Dokumentacja firmy Microsoft"
description: "Przykładowa aplikacja działa na komunikaty przychodzące Adafruit piór M0 sieci Wi-Fi i monitorów z Centrum IoT. Nowe zadanie gulp wysyła komunikaty do Adafruit piór M0 sieci Wi-Fi z Centrum IoT miga LED."
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: "Formant arduino doprowadziły z sieci web, kontroli arduino przeprowadzony za pośrednictwem sieci web"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-adafruit-feather-m0-wifi-kit-arduino-get-started
ms.assetid: a0bf53fb-29fb-485f-ba4a-6c715057b1a2
ms.service: iot-hub
ms.devlang: arduino
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: b4f4c1d86b10b64c104ac812d1f650d723322be8
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="run-a-sample-application-to-receive-cloud-to-device-messages"></a>Uruchom przykładową aplikację do odbierania wiadomości chmury do urządzenia
W tym artykule na tablicy Adafruit piór M0 sieci Wi-Fi Arduino wdrażania przykładowej aplikacji.

Przykładowa aplikacja monitoruje komunikaty przychodzące z Centrum IoT. Można również uruchomić zadanie gulp na komputerze do wysyłania komunikatów do tablicy Arduino z Centrum IoT. Gdy przykładowa aplikacja odbiera komunikaty, miga LED. Jeśli masz problemy, poszukaj rozwiązania [Rozwiązywanie problemów z strony][troubleshooting].

## <a name="what-you-will-do"></a>Będzie wykonywać
* Połącz przykładowej aplikacji do Centrum IoT.
* Wdrażanie i uruchamianie przykładowej aplikacji.
* Wysyłanie wiadomości z Centrum IoT do tablicy Arduino miga LED.

## <a name="what-you-will-learn"></a>Co dowiesz się
W tym artykule dowiesz się:
* Jak monitorować komunikaty przychodzące z Centrum IoT.
* Sposób wysyłania komunikatów chmury do urządzenia z Centrum IoT do tablicy Arduino.

## <a name="what-you-need"></a>Co jest potrzebne
* Tablicy Arduino, skonfigurować do używania. Aby dowiedzieć się, jak skonfigurować tablicy Arduino, zobacz [Skonfiguruj urządzenie][configure-your-device].
* Centrum IoT, która jest tworzona w Twojej subskrypcji platformy Azure. Aby dowiedzieć się, jak utworzyć Centrum IoT, zobacz [utworzenie Centrum IoT Azure][create-your-azure-iot-hub].

## <a name="connect-the-sample-application-to-your-iot-hub"></a>Połącz przykładowej aplikacji do Centrum IoT

1. Upewnij się, że jesteś w folderze repozytorium `iot-hub-c-feather-m0-getting-started`.

   Otwórz przykładowej aplikacji w programie Visual Studio Code, uruchamiając następujące polecenia:

   ```bash
   cd Lesson4
   code .
   ```

   Powiadomienie `app.ino` w pliku `app` podfolderu. `app.ino` Plik jest plikiem źródła klucza, który zawiera kod umożliwiający monitorowanie komunikatów przychodzących z Centrum IoT. `blinkLED` LED miga funkcji.

   ![Struktura repozytorium w przykładowej aplikacji][repo-structure]

2. Uzyskaj portu szeregowego urządzenia z odnajdywania urządzenia interfejsu wiersza polecenia:

   ```bash
   devdisco list --usb
   ```

   Należy wyświetlić dane wyjściowe podobne do następujących i Znajdź usb COM port tablicy Arduino:

   ![Odnajdywanie urządzeń][device-discovery]

3. Otwórz plik `config.json` w folderze lekcji i dane wejściowe wartość znaleziony numer portu COM:

   ```json
   {
       "device_port" : "COM1"
   }
   ```

   ![Config.JSON][config-json]

   > [!NOTE]
   > Dla portu COM na platformie systemu Windows ma format `COM1, COM2, ...`. System macOS lub Ubuntu zostanie rozpoczęty z `/dev/`.

4. Inicjowanie pliku konfiguracji, uruchamiając następujące polecenia:

   ```bash
   # For Windows command prompt
   npm install
   gulp init
   gulp install-tools
   ```

5. Wprowadź następujące elementy zastępcze w `config-arduino.json` pliku:

   Jeśli ukończono kroki [Tworzenie funkcji platformy Azure aplikacji i konto magazynu] [ create-an-azure-function-app-and-storage-account] na tym komputerze, wszystkie konfiguracje są dziedziczone, można pominąć krok do zadania, wdrażanie i uruchamianie przykładowej aplikacji. Jeśli ukończono kroki [Tworzenie funkcji platformy Azure aplikacji i konto magazynu] [ create-an-azure-function-app-and-storage-account] na innym komputerze, należy zastąpić symbole zastępcze w `config-arduino.json` pliku. `config-arduino.json` Plik znajduje się w podfolderze folderu macierzystego.

   ![Zawartość pliku konfiguracji arduino.json][config-arduino-json]

   * Zastąp **[SSID sieci Wi-Fi]** o identyfikatorze SSID sieci Wi-Fi, który jest połączony z Internetem.
   * Zastąp **[sieci Wi-Fi hasło]** hasła sieci Wi-Fi. Jeśli sieci Wi-Fi nie wymagają hasła, należy usunąć ciąg.
   * Zastąp **[parametry połączenia urządzenia IoT]** z parametrami połączenia urządzenia, który można uzyskać, uruchamiając `az iot device show-connection-string --hub-name {my hub name} --device-id {device id}` polecenia.
   * Zastąp **[parametry połączenia Centrum IoT]** z parametrami połączenia Centrum IoT, który można uzyskać, uruchamiając `az iot hub show-connection-string --name {my hub name}` polecenia.

## <a name="deploy-and-run-the-sample-application"></a>Wdrażanie i uruchamianie przykładowej aplikacji
Wdrażanie i uruchamianie przykładowej aplikacji na tablicy Arduino, uruchamiając następujące polecenia:

```bash
gulp run
# You can monitor the serial port by running listen task:
gulp listen

# Or you can combine above two gulp tasks into one:
gulp run --listen
```

Polecenie gulp wdraża przykładowej aplikacji do tablicy Arduino. Następnie uruchomi aplikację na tablicy Arduino i oddzielnych zadań na komputerze hosta do wysyłania wiadomości migania 20 do tablicy Arduino z Centrum IoT.

Po uruchomieniu aplikacji przykładowej, rozpoczyna nasłuchiwanie wiadomości z Centrum IoT. W tym samym czasie zadań gulp wysyła komunikaty "blink" z Centrum IoT do tablicy Arduino. Dla każdego komunikatu migania odbierająca tablicy wywołuje przykładowej aplikacji `blinkLED` funkcja miga LED.

Zadanie gulp wyśle 20 komunikatów z Centrum IoT do tablicy Arduino powinna zostać wyświetlona migania LED co dwie sekundy. Komunikat "stop", która kończy działanie aplikacji jest ostatni z nich.

![Przykładowa aplikacja z system gulp polecenia i blink wiadomości][sample-application]

## <a name="summary"></a>Podsumowanie
Na tablicy Arduino miga LED zostało pomyślnie wysłane wiadomości z Centrum IoT. Następne zadanie jest opcjonalne: Zmień włączenia i wyłączenia zachowanie LED.

## <a name="next-steps"></a>Następne kroki
[Zmień włączenia i wyłączenia zachowanie LED][change-the-on-and-off-led-behavior]


<!-- Images and links -->

[troubleshooting]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-troubleshooting.md
[configure-your-device]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson1-configure-your-device.md
[create-your-azure-iot-hub]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson2-prepare-azure-iot-hub.md
[repo-structure]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson4/repo_structure_arduino.png
[device-discovery]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson1/device_discovery.png
[config-json]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson1/vscode-config-mac.png
[create-an-azure-function-app-and-storage-account]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson3-deploy-resource-manager-template.md
[config-arduino-json]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson4/config-arduino.png
[sample-application]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson4/gulp_blink_arduino.png
[change-the-on-and-off-led-behavior]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson4-change-led-behavior.md