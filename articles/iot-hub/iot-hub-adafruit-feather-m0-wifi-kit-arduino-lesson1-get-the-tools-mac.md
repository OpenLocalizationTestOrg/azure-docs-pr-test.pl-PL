---
title: "Nawiązać Arduino Azure IoT — Lekcja 1: Pobierz narzędzia (macOS) | Dokumentacja firmy Microsoft"
description: "Pobierz i zainstaluj niezbędne narzędzia i oprogramowania dla pierwszego przykładowej aplikacji dla sieci Wi-Fi Adafruit piór M0 na macOS."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "Narzędzia deweloperskie arduino, programowanie iot, oprogramowanie iot, internet rzeczy oprogramowanie git instalacji dla komputerów mac, zainstaluj node js mac"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-adafruit-feather-m0-wifi-kit-arduino-get-started
ms.assetid: 0262f3dd-0259-4eb0-962f-9fb534f8359e
ms.service: iot-hub
ms.devlang: arduino
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: a6dc2555367e5fe530b3acde1f1f04ac442fb638
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="get-the-tools-macos-1010"></a>Pobierz narzędzia (macOS 10.10)
> [!div class="op_single_selector"]
> * [Windows 7 lub nowszy][windows]
> * [Ubuntu 16.04][ubuntu]
> * [System macOS 10.10][macos]

## <a name="what-you-will-do"></a>Będzie wykonywać

Pobierz narzędzia deweloperskie i oprogramowania dla pierwszego Przykładowa aplikacja dla tablicy Adafruit piór M0 sieci Wi-Fi Arduino. 

Jeśli masz problemy, poszukaj rozwiązania [Rozwiązywanie problemów z strony][troubleshooting].

> [!NOTE]
> Mimo że język programowania logiki główny Arduino, narzędzia Node.js są używane w wnioski do tworzenia i wdrażania przykładowej aplikacji.

## <a name="what-you-will-learn"></a>Co dowiesz się
W tym artykule dowiesz się:

* Jak zainstalować usługi Git i Node.js.
  * [Git](https://git-scm.com) jest typu open source rozproszonego systemu kontroli wersji. Przykładowa aplikacja dla tego artykułu znajduje się na Git.
  * [Node.js](https://nodejs.org/en/) jest środowiska wykonawczego języka JavaScript z ekosystemem sformatowanego pakietu.
* Sposób instalowania dodatkowych narzędzi do tworzenia środowiska Node.js za pomocą programu NPM.
  * Minimalna wymagana wersja programu Node.js jest 4.5 LTS.
  * [NPM](https://www.npmjs.com) jest jednym z wybranych menedżerów pakietu dla środowiska Node.js.

## <a name="what-you-need"></a>Co jest potrzebne
Aby wykonać tę operację, potrzebne będą:
* Połączenie internetowe, aby pobrać oprogramowanie i narzędzia deweloperskie.
* Mac, na którym działa system macOS Yosemite (10.10) lub nowszym.

## <a name="install-git-and-nodejs"></a>Zainstaluj usługi Git i Node.js
Aby zainstalować usługi Git i Node.js, użyj [Homebrew](http://brew.sh) pakietu narzędzie do zarządzania, wykonując następujące czynności:

1. Instalowanie oprogramowania Homebrew. Jeśli po zainstalowaniu oprogramowania Homebrew, przejdź do kroku 2.

   1. Naciśnij klawisz `Cmd + Space` , a następnie wprowadź `Terminal` otworzyć terminal.
   2. Uruchom następujące polecenie:

      ```bash
      /usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
      ```
2. Zainstaluj usługi Git i Node.js, uruchamiając następujące polecenie:

   ```bash
   brew install node git
   ```

## <a name="install-additional-nodejs-development-tools"></a>Instalowania dodatkowych narzędzi do tworzenia środowiska Node.js
Użyj [gulp.js](http://gulpjs.com) do automatyzowania wdrażania przykładowej aplikacji do tablicy Arduino.

Zainstaluj `gulp`, `device-discovery-cli` , uruchamiając następujące polecenie z poziomu terminala:

```bash
sudo npm install -g gulp device-discovery-cli
```

Jeśli wystąpią problemy z instalacją środowiska Node.js i te narzędzia programistyczne dodatkowe na macOS zobacz [przewodnik rozwiązywania problemów] [ troubleshooting] dla rozwiązania typowych problemów.

## <a name="install-visual-studio-code"></a>Zainstaluj kod programu Visual Studio
[Pobierz](https://code.visualstudio.com/docs/setup/osx) i zainstalować Visual Studio Code. Visual Studio Code to lekkie, ale jednocześnie wydajną źródła Edytor kodu dla systemu Windows, Linux i macOS. Umożliwia to edytor później w samouczku Edytuj przykładowy kod.

## <a name="summary"></a>Podsumowanie
Po zainstalowaniu narzędzi do tworzenia wymaganych i oprogramowania dla pierwszej aplikacji przykładowej. Następnym zadaniem jest tworzenie, wdrażanie i uruchom przykładową aplikację na tablicy Arduino.

## <a name="next-steps"></a>Następne kroki
[Tworzenie i wdrażanie aplikacji migania][create-and-deploy-the-blink-application]
<!-- Images and links -->

[windows]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson1-get-the-tools-win32.md
[ubuntu]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson1-get-the-tools-ubuntu.md
[macos]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson1-get-the-tools-mac.md
[troubleshooting]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-troubleshooting.md
[create-and-deploy-the-blink-application]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson1-deploy-blink-app.md