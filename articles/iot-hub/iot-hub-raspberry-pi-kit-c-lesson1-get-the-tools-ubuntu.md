---
title: "Connect Raspberry pi (C) do Azure IoT — Lekcja 1: Pobierz narzędzia (Ubuntu) | Dokumentacja firmy Microsoft"
description: "Pobierz i zainstaluj niezbędne narzędzia i oprogramowania dla pierwszej aplikacji przykładowej pi na Ubuntu."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: Programowanie iot oprogramowania iot, internet rzeczy oprogramowania, zainstaluj system git, ubuntu, system gulp Uruchom, zainstaluj node js ubuntu
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-raspberry-pi-kit-c-get-started
ms.assetid: 32cfea00-c254-4cef-8f6f-bbf807eca6b6
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 28ebba82e90d91470518cd830c96e6da39d8b9b4
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="get-the-tools-ubuntu-1604"></a>Pobierz narzędzia (Ubuntu 16.04)

> [!div class="op_single_selector"]
> * [Windows 7 lub nowszy](iot-hub-raspberry-pi-kit-c-lesson1-get-the-tools-win32.md)
> * [Ubuntu 16.04](iot-hub-raspberry-pi-kit-c-lesson1-get-the-tools-ubuntu.md)
> * [System macOS 10.10](iot-hub-raspberry-pi-kit-c-lesson1-get-the-tools-mac.md)

## <a name="what-you-will-do"></a>Będzie wykonywać
Pobierz narzędzia deweloperskie i oprogramowania dla pierwszego Przykładowa aplikacja dla programu malina Pi 3. Jeśli masz problemy, poszukaj rozwiązania [Rozwiązywanie problemów z strony](iot-hub-raspberry-pi-kit-c-troubleshooting.md).

> [!NOTE]
> Mimo że logiki główny język programowania C, narzędzia Node.js są używane w wnioski do odnajdywania urządzeń i tworzenia i wdrażania przykładowej aplikacji.

## <a name="what-you-will-learn"></a>Co dowiesz się
W tym artykule dowiesz się:

* Jak zainstalować usługi Git i Node.js
  * [Git](https://git-scm.com) jest typu open source rozproszonego systemu kontroli wersji. Przykładowa aplikacja dla tego artykułu znajduje się na Git.
  * [Node.js](https://nodejs.org/en/) jest środowiska wykonawczego języka JavaScript z ekosystemem sformatowanego pakietu.
* Sposób instalowania dodatkowych narzędzi do tworzenia środowiska Node.js za pomocą programu NPM.
  * Minimalna wymagana wersja programu Node.js jest 4.5 LTS.
  * [NPM](https://www.npmjs.com) jest jednym z wybranych menedżerów pakietu dla środowiska Node.js.

## <a name="what-you-need"></a>Co jest potrzebne
Aby wykonać tę operację, potrzebne będą:

* Połączenie internetowe, aby pobrać oprogramowanie i narzędzia deweloperskie.
* Komputer z systemem Ubuntu 16.04 lub nowszej.

## <a name="install-git-nodejs-and-npm"></a>Zainstaluj narzędzia Git, Node.js i NPM
Użyj skrótu klawiaturowego `Ctrl + Alt + T` Otwórz terminal i uruchom następujące polecenia:

```bash
sudo apt-get update
curl -sL https://deb.nodesource.com/setup_6.x | sudo -E bash -
sudo apt-get install -y nodejs
sudo apt-get install git
```

## <a name="install-additional-nodejs-development-tools"></a>Instalowania dodatkowych narzędzi do tworzenia środowiska Node.js
Użyj [gulp.js](http://gulpjs.com) do automatyzowania wdrażania przykładowej aplikacji do Pi. Użyj [urządzenia odnajdywania cli](https://github.com/Azure/device-discovery-cli) można pobrać informacji o sieci o urządzenia IoT.

Zainstaluj `gulp` i `device-discovery-cli` , uruchamiając następujące polecenie z poziomu terminala:

```bash
sudo npm install -g device-discovery-cli gulp
```

Jeśli występują problemy z instalacją środowiska Node.js i te narzędzia programistyczne dodatkowe na Ubuntu, zobacz [przewodnik rozwiązywania problemów](iot-hub-raspberry-pi-kit-c-troubleshooting.md) dla rozwiązania typowych problemów.

## <a name="install-visual-studio-code"></a>Zainstaluj kod programu Visual Studio
[Pobierz](https://code.visualstudio.com/docs/setup/linux) i zainstalować Visual Studio Code. Visual Studio Code to lekkie, ale jednocześnie wydajną źródła Edytor kodu dla systemu Windows, Linux i macOS. Umożliwia to edytor później w samouczku Edytuj przykładowy kod.

## <a name="summary"></a>Podsumowanie
Po zainstalowaniu narzędzi do tworzenia wymaganych i oprogramowania dla pierwszej aplikacji przykładowej. Następnym zadaniem jest tworzenie, wdrażanie i uruchom przykładową aplikację na Pi.

## <a name="next-steps"></a>Następne kroki
[Tworzenie i wdrażanie aplikacji blink](iot-hub-raspberry-pi-kit-c-lesson1-deploy-blink-app.md)

