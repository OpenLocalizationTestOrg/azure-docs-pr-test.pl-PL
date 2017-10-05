---
title: "Edison firmy Intel (węzeł) nawiązania połączenia platformy Azure IoT — Lekcja 1: Wdrażanie aplikacji | Dokumentacja firmy Microsoft"
description: "Klonowanie aplikacji przykładowej C z serwisu GitHub, a następnie uruchom gulp do wdrożenia tej aplikacji do tablicy Intel Edison. Ta przykładowa aplikacja miga LED podłączone do tablicy co dwie sekundy."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "arduino doprowadziły projektów, arduino doprowadziły migania, kod migania arduino doprowadziły, program migania arduino, arduino migania przykład"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-intel-edison-kit-node-get-started
ms.assetid: ed2c21d0-c72c-4ac2-9e70-347e9a0711c0
ms.service: iot-hub
ms.devlang: nodejs
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 8490fbbf14183432c665165412f00955d6323580
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="create-and-deploy-the-blink-application"></a>Tworzenie i wdrażanie aplikacji blink
## <a name="what-you-will-do"></a>Będzie wykonywać
Klonowanie aplikacji przykładowej C z usługi GitHub i wdrażanie przykładowej aplikacji do firmy Intel Edison za pomocą narzędzia gulp. Przykładowa aplikacja miga LED podłączone do tablicy co dwie sekundy. Jeśli masz problemy, poszukaj rozwiązania [Rozwiązywanie problemów z strony][troubleshooting].

## <a name="what-you-will-learn"></a>Co dowiesz się
* Jak wdrożyć i uruchomić aplikację przykładową na Edison.

## <a name="what-you-need"></a>Co jest potrzebne
Pomyślnie zakończono następujące operacje:

* [Skonfiguruj urządzenie][configure-your-device]
* [Pobierz narzędzia][get-the-tools]

## <a name="open-the-sample-application"></a>Otwórz aplikację przykładową
Aby otworzyć aplikację przykładową, wykonaj następujące kroki:

1. Klonowanie repozytorium przykładowej z serwisu GitHub, uruchamiając następujące polecenie:

   ```bash
   git clone https://github.com/Azure-Samples/iot-hub-node-edison-getting-started.git
   ```
2. Otwórz przykładowej aplikacji w programie Visual Studio Code, uruchamiając następujące polecenia:

   ```bash
   cd iot-hub-node-edison-getting-started
   cd Lesson1
   code .
   ```

   ![Struktura repozytorium][repo-structure]

Plik `app` podfolder jest plik źródłowy klucza, który zawiera kod służący do kontroli LED.

### <a name="install-application-dependencies"></a>Zainstaluj zależności aplikacji
Zainstaluj biblioteki oraz inne moduły potrzebnych dla aplikacji przykładowej, uruchamiając następujące polecenie:

```bash
npm install
```

## <a name="configure-the-device-connection"></a>Skonfiguruj połączenie z urządzeniem
Aby skonfigurować połączenie z urządzeniem, wykonaj następujące kroki:

1. Generowanie pliku konfiguracji urządzenia, uruchamiając następujące polecenie:

   ```bash
   gulp init
   ```

   Plik konfiguracji `config-edison.json` zawiera poświadczenia użytkownika używane do logowania się do Edison. W celu uniknięcia wycieku poświadczeń użytkownika, plik konfiguracji jest generowany w podfolderze `.iot-hub-getting-started` folderu macierzystego na tym komputerze.

2. Otwórz plik konfiguracji urządzeń w programie Visual Studio Code, uruchamiając następujące polecenie:

   ```bash
   # For Windows command prompt
   code %USERPROFILE%\.iot-hub-getting-started\config-edison.json

   # For MacOS or Ubuntu
   code ~/.iot-hub-getting-started/config-edison.json
   ```

3. Zastąp symbol zastępczy `[device hostname or IP address]` i `[device password]` przy użyciu adresu IP i hasła, który oznaczony w dół w poprzedniej lekcji.

   ![Config.JSON](media/iot-hub-intel-edison-lessons/lesson1/vscode-config-mac.png)

Gratulacje! Pierwszy Przykładowa aplikacja dla Edison została pomyślnie utworzona.

## <a name="deploy-and-run-the-sample-application"></a>Wdrażanie i uruchamianie przykładowej aplikacji

### <a name="deploy-and-run-the-sample-app"></a>Wdrażanie i uruchamianie przykładowej aplikacji
Wdrażanie i uruchamianie aplikacji przykładowej, uruchamiając następujące polecenie:

```bash
gulp deploy && gulp run
```

### <a name="verify-the-app-works"></a>Weryfikowanie działania aplikacji
Przykładowa aplikacja kończy się automatycznie po LED miga do 20 razy. Jeśli nie widzisz migający LED, zobacz [przewodnik rozwiązywania problemów] [ troubleshooting] dla rozwiązania typowych problemów.

![Migający LED][led-blinking]

## <a name="summary"></a>Podsumowanie
Zainstalowaniu wymagane narzędzia do pracy z Edison i przykładowej aplikacji do Edison miga LED wdrożone. Teraz można tworzyć, wdrażać i uruchom inną aplikację przykładową, która łączy Edison Centrum IoT Azure do wysyłania i odbierania wiadomości.

## <a name="next-steps"></a>Następne kroki
[Pobierz narzędzia Azure][get-the-azure-tools]

<!-- Images and links -->

[troubleshooting]: iot-hub-intel-edison-kit-node-troubleshooting.md
[Configure-your-device]: iot-hub-intel-edison-kit-node-lesson1-configure-your-device.md
[get-the-tools]: iot-hub-intel-edison-kit-node-lesson1-get-the-tools-win32.md
[repo-structure]: media/iot-hub-intel-edison-lessons/lesson1/repo_structure.png
[led-blinking]: media/iot-hub-intel-edison-lessons/lesson1/led_blinking.png
[get-the-azure-tools]: iot-hub-intel-edison-kit-node-lesson2-get-azure-tools-win32.md
