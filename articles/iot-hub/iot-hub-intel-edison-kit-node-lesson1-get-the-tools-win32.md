---
title: "Połącz Edison firmy Intel (węzeł) tooAzure IoT — Lekcja 1: Pobierz narzędzia (system Windows) | Dokumentacja firmy Microsoft"
description: "Pobierz i zainstaluj hello niezbędne narzędzia i oprogramowania hello pierwszy przykładowej aplikacji Edison w systemie Windows 7 i nowszych wersjach."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "Narzędzia deweloperskie arduino, programowanie iot, oprogramowanie iot, internet rzeczy oprogramowanie git instalacji w systemie windows, instalowanie node js systemu windows"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-intel-edison-kit-node-get-started
ms.assetid: 4164b5a1-5a42-4d8a-9ff6-441e79fcc936
ms.service: iot-hub
ms.devlang: nodejs
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 933cc585d1b8b0236d76452f5c449ae9f2f3987b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="get-hello-tools-windows-7-or-later"></a>Pobierz narzędzia hello (z systemem Windows 7 lub nowszy)
> [!div class="op_single_selector"]
> * [Windows 7 lub nowszy][windows]
> * [Ubuntu 16.04][ubuntu]
> * [System macOS 10.10][macos]

## <a name="what-you-will-do"></a>Będzie wykonywać
Pobierz narzędzia deweloperskie hello i oprogramowania hello hello pierwszy przykładowej aplikacji Intel Edison. Jeśli masz problemy, poszukaj rozwiązania na powitania [Rozwiązywanie problemów z strony][troubleshooting].

## <a name="what-you-will-learn"></a>Co dowiesz się
W tym artykule dowiesz się:

* Jak tooinstall Git i Node.js.
  * [Git](https://git-scm.com) jest typu open source rozproszonego systemu kontroli wersji. Witaj Przykładowa aplikacja dla tego artykułu znajduje się na Git.
  * [Node.js](https://nodejs.org/en/) jest środowiska wykonawczego języka JavaScript z ekosystemem sformatowanego pakietu.
* Jak toouse NPM tooinstall dodatkowe Node.js narzędzia deweloperskie.
  * Witaj minimalne wymagania wersji środowiska Node.js jest 4.5 LTS.
  * [NPM](https://www.npmjs.com) jest jednym z hello menedżerów pakietu dla środowiska Node.js.

## <a name="what-you-need"></a>Co jest potrzebne

toocomplete tej operacji, należy:

* Toodownload połączenia internetowego hello narzędzia deweloperskie i hello oprogramowania.
* Komputer z systemem Windows.

## <a name="install-git-and-nodejs"></a>Zainstaluj usługi Git i Node.js

Kliknij łącza hello poniżej toodownload i zainstaluj usługi Git i LTS Node.js dla systemu Windows.

* [Pobierz Git dla systemu Windows](https://git-scm.com/download/win/)
* [Pobierz Node.js LTS dla systemu Windows](https://nodejs.org/en/)

## <a name="install-additional-nodejs-development-tools"></a>Instalowania dodatkowych narzędzi do tworzenia środowiska Node.js

Użyj [gulp.js](http://gulpjs.com) tooautomate wdrożenie hello hello przykładowej aplikacji tooEdison.

Uruchom wiersz polecenia jako administrator. Zainstaluj `gulp` , uruchamiając następujące polecenie hello:

```cmd
npm install -g gulp
```

Jeśli występują problemy z instalacją środowiska Node.js i te dodatkowe narzędzia programistyczne Node.js na komputerze, zobacz hello [przewodnik rozwiązywania problemów] [ troubleshooting] dla rozwiązania toocommon problemów.

## <a name="install-visual-studio-code"></a>Zainstaluj kod programu Visual Studio

[Pobierz](https://code.visualstudio.com/docs/setup/windows) i zainstalować Visual Studio Code. Visual Studio Code to lekkie, ale jednocześnie wydajną źródła Edytor kodu dla systemu Windows, Linux i macOS. Edytor w dalszej części hello samouczek tooedit hello przykładowy kod.

## <a name="summary"></a>Podsumowanie

Po zainstalowaniu oprogramowania hello pierwszy przykładowej aplikacji i narzędzia deweloperskie hello wymagane. następne zadanie Hello jest toocreate, wdrażanie i uruchamianie hello przykładowej aplikacji na Edison.

## <a name="next-steps"></a>Następne kroki

[Tworzenie i wdrażanie aplikacji migania hello][create-and-deploy-the-blink-application]
<!-- Images and links -->

[troubleshooting]: iot-hub-intel-edison-kit-node-troubleshooting.md
[create-and-deploy-the-blink-application]: iot-hub-intel-edison-kit-node-lesson1-deploy-blink-app.md
[windows]: iot-hub-intel-edison-kit-node-lesson1-get-the-tools-win32.md
[ubuntu]: iot-hub-intel-edison-kit-node-lesson1-get-the-tools-ubuntu.md
[macos]: iot-hub-intel-edison-kit-node-lesson1-get-the-tools-mac.md
