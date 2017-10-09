---
title: "Połącz Arduino tooAzure IoT — Lekcja 1: Pobierz narzędzia (macOS) | Dokumentacja firmy Microsoft"
description: "Pobierz i zainstaluj na macOS hello niezbędne narzędzia i oprogramowania hello pierwszy przykładowej aplikacji Adafruit piór M0 sieci Wi-Fi."
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
ms.openlocfilehash: 5fd306fecd7259fb8f1e99d76282a1e464c4d4f6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="get-hello-tools-macos-1010"></a>Pobierz narzędzia hello (macOS 10.10)
> [!div class="op_single_selector"]
> * [Windows 7 lub nowszy][windows]
> * [Ubuntu 16.04][ubuntu]
> * [System macOS 10.10][macos]

## <a name="what-you-will-do"></a>Będzie wykonywać

Pobierz oprogramowanie hello hello pierwszy Przykładowa aplikacja dla tablicy Adafruit piór M0 sieci Wi-Fi Arduino i narzędzia deweloperskie hello. 

Jeśli masz problemy, poszukaj rozwiązania na powitania [Rozwiązywanie problemów z strony][troubleshooting].

> [!NOTE]
> Mimo że hello język logiki główny hello programowania Arduino, narzędzia Node.js są używane w toobuild — lekcje hello i wdrażania przykładowej aplikacji.

## <a name="what-you-will-learn"></a>Co dowiesz się
W tym artykule dowiesz się:

* Jak tooinstall Git i Node.js.
  * [Git](https://git-scm.com) jest typu open source rozproszonego systemu kontroli wersji. Witaj Przykładowa aplikacja dla tego artykułu znajduje się na Git.
  * [Node.js](https://nodejs.org/en/) jest środowiska wykonawczego języka JavaScript z ekosystemem sformatowanego pakietu.
* Jak toouse NPM tooinstall dodatkowe Node.js narzędzia deweloperskie.
  * Witaj minimalnej wymaganej wersji środowiska Node.js jest 4.5 LTS.
  * [NPM](https://www.npmjs.com) jest jednym z hello menedżerów pakietu dla środowiska Node.js.

## <a name="what-you-need"></a>Co jest potrzebne
toocomplete tej operacji, należy:
* Toodownload połączenia internetowego hello narzędzia deweloperskie i hello oprogramowania.
* Mac, na którym działa system macOS Yosemite (10.10) lub nowszym.

## <a name="install-git-and-nodejs"></a>Zainstaluj usługi Git i Node.js
tooinstall Git i Node.js, użyj hello [Homebrew](http://brew.sh) pakietu narzędzie do zarządzania, wykonując następujące czynności:

1. Instalowanie oprogramowania Homebrew. Jeśli po zainstalowaniu oprogramowania Homebrew, przejdź toostep 2.

   1. Naciśnij klawisz `Cmd + Space` , a następnie wprowadź `Terminal` tooopen terminalu.
   2. Uruchom następujące polecenie hello:

      ```bash
      /usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
      ```
2. Zainstaluj usługi Git i Node.js, uruchamiając następujące polecenie hello:

   ```bash
   brew install node git
   ```

## <a name="install-additional-nodejs-development-tools"></a>Instalowania dodatkowych narzędzi do tworzenia środowiska Node.js
Użyj [gulp.js](http://gulpjs.com) tooautomate wdrożenie hello hello przykładowej aplikacji tooyour Arduino tablicy.

Zainstaluj `gulp`, `device-discovery-cli` , uruchamiając następujące polecenie w terminalu hello hello:

```bash
sudo npm install -g gulp device-discovery-cli
```

Jeśli wystąpią problemy z instalacją środowiska Node.js i te narzędzia programistyczne dodatkowe na macOS Zobacz hello [przewodnik rozwiązywania problemów] [ troubleshooting] dla rozwiązania toocommon problemów.

## <a name="install-visual-studio-code"></a>Zainstaluj kod programu Visual Studio
[Pobierz](https://code.visualstudio.com/docs/setup/osx) i zainstalować Visual Studio Code. Visual Studio Code to lekkie, ale jednocześnie wydajną źródła Edytor kodu dla systemu Windows, Linux i macOS. Edytor w dalszej części hello samouczek tooedit hello przykładowy kod.

## <a name="summary"></a>Podsumowanie
Po zainstalowaniu oprogramowania hello pierwszy przykładowej aplikacji i narzędzia deweloperskie hello wymagane. następne zadanie Hello jest toocreate, wdrażanie i uruchamianie aplikacji przykładowej hello na tablicy Arduino.

## <a name="next-steps"></a>Następne kroki
[Tworzenie i wdrażanie aplikacji migania hello][create-and-deploy-the-blink-application]
<!-- Images and links -->

[windows]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson1-get-the-tools-win32.md
[ubuntu]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson1-get-the-tools-ubuntu.md
[macos]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson1-get-the-tools-mac.md
[troubleshooting]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-troubleshooting.md
[create-and-deploy-the-blink-application]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson1-deploy-blink-app.md