---
title: "Połącz Edison firmy Intel (węzeł) tooAzure IoT — Lekcja 1: Wdrażanie aplikacji | Dokumentacja firmy Microsoft"
description: "Klonowanie hello przykładowej C aplikacji z usługi GitHub i uruchomić gulp toodeploy tej aplikacji tooyour Intel Edison tablicy. Ta przykładowa aplikacja miga tablicy toohello LED połączone hello co dwie sekundy."
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
ms.openlocfilehash: bc03c7e45bd1ba9e9b2c8f2fec70a1be647e96b7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-deploy-hello-blink-application"></a>Tworzenie i wdrażanie aplikacji migania hello
## <a name="what-you-will-do"></a>Będzie wykonywać
Klonowanie hello przykładowej C aplikacji z usługi GitHub i użyj hello gulp narzędzie toodeploy hello przykładowej aplikacji tooIntel Edison. Witaj przykładowej aplikacji miga tablicy toohello LED połączone hello co dwie sekundy. Jeśli masz problemy, poszukaj rozwiązania na powitania [Rozwiązywanie problemów z strony][troubleshooting].

## <a name="what-you-will-learn"></a>Co dowiesz się
* Jak toodeploy i wykonywania hello przykładowej aplikacji na Edison.

## <a name="what-you-need"></a>Co jest potrzebne
Użytkownik pomyślnie ukończona hello następujące operacje:

* [Skonfiguruj urządzenie][configure-your-device]
* [Pobierz narzędzia hello][get-the-tools]

## <a name="open-hello-sample-application"></a>Otwórz hello przykładowej aplikacji
Witaj tooopen przykładowej aplikacji, wykonaj następujące kroki:

1. Klonuj repozytorium przykładowej hello z serwisu GitHub, uruchamiając następujące polecenie hello:

   ```bash
   git clone https://github.com/Azure-Samples/iot-hub-node-edison-getting-started.git
   ```
2. Otwórz hello przykładowej aplikacji w programie Visual Studio Code, uruchamiając następujące polecenia hello:

   ```bash
   cd iot-hub-node-edison-getting-started
   cd Lesson1
   code .
   ```

   ![Struktura repozytorium][repo-structure]

Plik Hello w hello `app` podfolder to plik klucza źródła hello, który zawiera hello kodu toocontrol hello LED.

### <a name="install-application-dependencies"></a>Zainstaluj zależności aplikacji
Zainstaluj hello bibliotek i inne moduły potrzebnych dla aplikacji przykładowej hello, uruchamiając następujące polecenie hello:

```bash
npm install
```

## <a name="configure-hello-device-connection"></a>Skonfiguruj połączenie z urządzeniem hello
tooconfigure hello połączenie z urządzeniem, wykonaj następujące kroki:

1. Generowanie pliku konfiguracji urządzenia hello, uruchamiając następujące polecenie hello:

   ```bash
   gulp init
   ```

   plik konfiguracji Hello `config-edison.json` zawiera poświadczenia użytkownika hello używasz toolog tooEdison. przeciek hello tooavoid poświadczeń użytkownika hello plik konfiguracji jest generowany w podfolderze hello `.iot-hub-getting-started` hello folderu macierzystego na tym komputerze.

2. Otwórz plik konfiguracji urządzenia hello w programie Visual Studio Code, uruchamiając następujące polecenie hello:

   ```bash
   # For Windows command prompt
   code %USERPROFILE%\.iot-hub-getting-started\config-edison.json

   # For MacOS or Ubuntu
   code ~/.iot-hub-getting-started/config-edison.json
   ```

3. Zastąp symbol zastępczy hello `[device hostname or IP address]` i `[device password]` z adresem IP hello i hasło, które są oznaczone w dół w poprzedniej lekcji.

   ![Config.JSON](media/iot-hub-intel-edison-lessons/lesson1/vscode-config-mac.png)

Gratulacje! Witaj pierwszy przykładowej aplikacji Edison została pomyślnie utworzona.

## <a name="deploy-and-run-hello-sample-application"></a>Wdrażanie i uruchamianie hello przykładowej aplikacji

### <a name="deploy-and-run-hello-sample-app"></a>Wdrażanie i uruchamianie hello przykładowej aplikacji
Wdrażanie i uruchamianie aplikacji przykładowej hello, uruchamiając następujące polecenie hello:

```bash
gulp deploy && gulp run
```

### <a name="verify-hello-app-works"></a>Weryfikowanie działania aplikacji hello
Witaj przykładowej aplikacji kończy się automatycznie po hello LED miga do 20 razy. Jeśli nie widzisz migający hello LED, zobacz hello [przewodnik rozwiązywania problemów] [ troubleshooting] dla rozwiązania toocommon problemów.

![Migający LED][led-blinking]

## <a name="summary"></a>Podsumowanie
Zainstalowaniu hello wymagane narzędzia toowork z Edison i przykładowej aplikacji tooEdison tooblink hello LED wdrożone. Można teraz tworzenie, wdrażanie i uruchom inną aplikację przykładową, która łączy tooAzure Edison toosend Centrum IoT i odbierania wiadomości.

## <a name="next-steps"></a>Następne kroki
[Pobierz hello Azure narzędzia][get-the-azure-tools]

<!-- Images and links -->

[troubleshooting]: iot-hub-intel-edison-kit-node-troubleshooting.md
[Configure-your-device]: iot-hub-intel-edison-kit-node-lesson1-configure-your-device.md
[get-the-tools]: iot-hub-intel-edison-kit-node-lesson1-get-the-tools-win32.md
[repo-structure]: media/iot-hub-intel-edison-lessons/lesson1/repo_structure.png
[led-blinking]: media/iot-hub-intel-edison-lessons/lesson1/led_blinking.png
[get-the-azure-tools]: iot-hub-intel-edison-kit-node-lesson2-get-azure-tools-win32.md
