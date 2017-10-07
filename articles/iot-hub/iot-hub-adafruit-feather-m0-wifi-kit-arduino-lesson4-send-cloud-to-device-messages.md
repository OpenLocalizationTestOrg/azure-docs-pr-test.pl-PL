---
title: "Connect Arduino (C) tooAzure IoT - 4 lekcji: chmury do urządzenia | Dokumentacja firmy Microsoft"
description: "Przykładowa aplikacja działa na komunikaty przychodzące Adafruit piór M0 sieci Wi-Fi i monitorów z Centrum IoT. Nowe zadanie gulp wysyła komunikaty tooAdafruit M0 piór sieci Wi-Fi z Twojej hello tooblink Centrum IoT LED."
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
ms.openlocfilehash: dcddd61ff684f49436103675938d719cb227c409
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="run-a-sample-application-tooreceive-cloud-to-device-messages"></a>Uruchom tooreceive aplikacji przykładowej wiadomości chmury do urządzenia
W tym artykule na tablicy Adafruit piór M0 sieci Wi-Fi Arduino wdrażania przykładowej aplikacji.

aplikacja przykładowa Hello monitoruje komunikaty przychodzące z Centrum IoT. Można również uruchomić zadanie gulp na tooyour wiadomości tablicy Arduino Twojego komputera toosend z Centrum IoT. Gdy hello Przykładowa aplikacja odbiera wiadomości powitania, miga hello LED. Jeśli masz problemy, poszukaj rozwiązania na powitania [Rozwiązywanie problemów z strony][troubleshooting].

## <a name="what-you-will-do"></a>Będzie wykonywać
* Połącz Centrum IoT tooyour hello przykładowej aplikacji.
* Wdrażanie i uruchamianie hello przykładowej aplikacji.
* Wysyłanie wiadomości z Twojej IoT hub tooyour Arduino tablicy tooblink hello LED.

## <a name="what-you-will-learn"></a>Co dowiesz się
W tym artykule dowiesz się:
* Jak komunikaty przychodzące toomonitor z Centrum IoT.
* Jak chmury urządzenia toosend komunikaty z sieci tooyour Centrum IoT Arduino tablicy.

## <a name="what-you-need"></a>Co jest potrzebne
* Tablicy Arduino, skonfigurować do używania. toolearn tooset się tablicy Arduino, zobacz temat [Skonfiguruj urządzenie][configure-your-device].
* Centrum IoT, która jest tworzona w Twojej subskrypcji platformy Azure. toolearn jak toocreate Centrum IoT, zobacz [utworzenie Centrum IoT Azure][create-your-azure-iot-hub].

## <a name="connect-hello-sample-application-tooyour-iot-hub"></a>Połącz z Centrum IoT tooyour hello przykładowej aplikacji

1. Upewnij się, że jesteś w folderze repozytorium hello `iot-hub-c-feather-m0-getting-started`.

   Otwórz hello przykładowej aplikacji w programie Visual Studio Code, uruchamiając następujące polecenia hello:

   ```bash
   cd Lesson4
   code .
   ```

   Powiadomienie hello `app.ino` pliku w hello `app` podfolderu. Witaj `app.ino` plik jest plikiem klucza źródła hello, zawierający hello kodu toomonitor komunikaty przychodzące hello Centrum IoT. Witaj `blinkLED` funkcja miganie hello LED.

   ![Struktura repozytorium w hello przykładowej aplikacji][repo-structure]

2. Uzyskaj hello portu szeregowego hello urządzenia z hello urządzenia odnajdywania interfejsu wiersza polecenia:

   ```bash
   devdisco list --usb
   ```

   Należy wyświetlone informacje podobne następujących toohello i Znajdź hello usb COM port tablicy Arduino:

   ![Odnajdywanie urządzeń][device-discovery]

3. Witaj Otwórz plik `config.json` w folderze lekcji hello i wartości wejściowych hello hello znaleziono numer portu COM:

   ```json
   {
       "device_port" : "COM1"
   }
   ```

   ![Config.JSON][config-json]

   > [!NOTE]
   > Dla portu hello COM, na platformie systemu Windows ma hello format `COM1, COM2, ...`. System macOS lub Ubuntu zostanie rozpoczęty z `/dev/`.

4. Inicjowanie pliku konfiguracji hello, uruchamiając następujące polecenia hello:

   ```bash
   # For Windows command prompt
   npm install
   gulp init
   gulp install-tools
   ```

5. Wprowadź następujące elementy zastępcze w hello hello `config-arduino.json` pliku:

   Jeśli ukończono kroki hello [Tworzenie funkcji platformy Azure aplikacji i konto magazynu] [ create-an-azure-function-app-and-storage-account] na tym komputerze, wszystkie konfiguracje hello są dziedziczone, można pominąć hello krok toohello zadania wdrażania i uruchomiona hello przykładowej aplikacji. Jeśli ukończono kroki hello [Tworzenie funkcji platformy Azure aplikacji i konto magazynu] [ create-an-azure-function-app-and-storage-account] na innym komputerze, należy symbole zastępcze hello tooreplace w hello `config-arduino.json` pliku. Witaj `config-arduino.json` plik znajduje się w podfolderze hello folderu macierzystego.

   ![Zawartość pliku config arduino.json hello][config-arduino-json]

   * Zastąp **[SSID sieci Wi-Fi]** o identyfikatorze SSID sieci Wi-Fi, który połączony toohello Internet.
   * Zastąp **[sieci Wi-Fi hasło]** hasła sieci Wi-Fi. Jeśli sieci Wi-Fi nie wymagają hasła, należy usunąć ciąg hello.
   * Zastąp **[parametry połączenia urządzenia IoT]** z hello parametry połączenia urządzenia, które można uzyskać, uruchamiając hello `az iot device show-connection-string --hub-name {my hub name} --device-id {device id}` polecenia.
   * Zastąp **[parametry połączenia Centrum IoT]** z hello parametry połączenia Centrum IoT, które można uzyskać, uruchamiając hello `az iot hub show-connection-string --name {my hub name}` polecenia.

## <a name="deploy-and-run-hello-sample-application"></a>Wdrażanie i uruchamianie hello przykładowej aplikacji
Wdrażanie i uruchamianie aplikacji przykładowej hello na tablicy Arduino, uruchamiając następujące polecenia hello:

```bash
gulp run
# You can monitor hello serial port by running listen task:
gulp listen

# Or you can combine above two gulp tasks into one:
gulp run --listen
```

polecenie gulp Hello wdraża hello przykładowej aplikacji tooyour Arduino tablicy. Następnie uruchomieniu aplikacji hello na tablicy Arduino i oddzielnych zadań na hoście komputera toosend 20 migania wiadomości tooyour Arduino tablicy z Centrum IoT.

Po uruchomieniu aplikacji przykładowej hello rozpoczyna nasłuchiwanie toomessages z Centrum IoT. W tym samym czasie hello gulp zadań wysyła komunikaty "blink" z Twojej tooyour Centrum IoT Arduino tablicy. Dla każdej wiadomości migania hello tablicy odbiera, hello przykładowej aplikacji wywołuje hello `blinkLED` funkcja tooblink hello LED.

Powinny pojawić się hello LED blink co dwie sekundy zadań gulp hello wyśle 20 komunikatów z Twojej tooyour Centrum IoT Arduino tablicy. Hello ostatnio jedna jest zatrzymuje aplikacji hello komunikat "stop".

![Przykładowa aplikacja z system gulp polecenia i blink wiadomości][sample-application]

## <a name="summary"></a>Podsumowanie
Zostało pomyślnie wysłane wiadomości z Twojej IoT hub tooyour Arduino tablicy tooblink hello LED. następne zadanie Hello jest opcjonalny: Zmień hello włączać i wyłączać zachowanie hello LED.

## <a name="next-steps"></a>Następne kroki
[Zmień hello włączać i wyłączać zachowanie hello LED][change-the-on-and-off-led-behavior]


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