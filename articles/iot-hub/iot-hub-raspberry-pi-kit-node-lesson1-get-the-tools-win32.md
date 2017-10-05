---
title: "Nawiązać Pi malina (węzeł) Azure IoT — Lekcja 1: Pobierz narzędzia (system Windows) | Dokumentacja firmy Microsoft"
description: "Pobierz i zainstaluj niezbędne narzędzia i oprogramowania dla pierwszej aplikacji przykładowej pi w systemie Windows 7 i nowszych wersjach."
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: "Programowanie iot oprogramowania iot, internet rzeczy oprogramowania, zainstaluj usługę git w systemie windows, system gulp uruchomienia, zainstalowania systemu operacyjnego windows node js, instalowania npm w systemie windows, zainstaluj python w systemie windows"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-raspberry-pi-kit-node-get-started
ms.assetid: b3d88e17-97cc-4f23-85fd-a688fc228eb8
ms.service: iot-hub
ms.devlang: node
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 24c58e006bbef9bbc1fcd626a0f8f6bcac063f05
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="get-the-tools-windows-7-or-later"></a>Pobierz narzędzia (z systemem Windows 7 lub nowszy)

> [!div class="op_single_selector"]
> * [Windows 7 lub nowszy](iot-hub-raspberry-pi-kit-node-lesson1-get-the-tools-win32.md)
> * [Ubuntu 16.04](iot-hub-raspberry-pi-kit-node-lesson1-get-the-tools-ubuntu.md)
> * [System macOS 10.10](iot-hub-raspberry-pi-kit-node-lesson1-get-the-tools-mac.md)


## <a name="what-you-will-do"></a>Będzie wykonywać
Pobierz narzędzia deweloperskie i oprogramowania dla pierwszego Przykładowa aplikacja dla malina Pi 3. Jeśli masz problemy, poszukaj rozwiązania [Rozwiązywanie problemów z strony](iot-hub-raspberry-pi-kit-node-troubleshooting.md).

## <a name="what-you-will-learn"></a>Co dowiesz się
W tym artykule dowiesz się:

* Jak zainstalować usługi Git i Node.js.
  * [Git](https://git-scm.com) jest typu open source rozproszonego systemu kontroli wersji. Przykładowa aplikacja dla tego artykułu znajduje się na Git.
  * [Node.js](https://nodejs.org/en/) jest środowiska wykonawczego języka JavaScript z ekosystemem sformatowanego pakietu.
* Sposób instalowania dodatkowych narzędzi do tworzenia środowiska Node.js za pomocą programu NPM.
  * Minimalne wymagania wersji środowiska node.js jest 4.5 LTS.
  * [NPM](https://www.npmjs.com) jest jednym z wybranych menedżerów pakietu dla środowiska Node.js.

## <a name="what-you-need"></a>Co jest potrzebne
Aby wykonać tę operację, potrzebne będą:

* Połączenie internetowe, aby pobrać oprogramowanie i narzędzia deweloperskie.
* Komputer z systemem Windows.

## <a name="install-git-and-nodejs"></a>Zainstaluj usługi Git i Node.js
Kliknij poniższe łącza, aby pobrać i zainstalować usługi Git i LTS Node.js dla systemu Windows.

* [Pobierz Git dla systemu Windows](https://git-scm.com/download/win/)
* [Pobierz Node.js LTS dla systemu Windows](https://nodejs.org/en/)

## <a name="install-additional-nodejs-development-tools"></a>Instalowania dodatkowych narzędzi do tworzenia środowiska Node.js
Użyj [gulp.js](http://gulpjs.com) do automatyzowania wdrażania przykładowej aplikacji do Pi. Można również użyć [urządzenia odnajdywania cli](https://github.com/Azure/device-discovery-cli) można pobrać informacji o sieci o urządzenia IoT.

Uruchom wiersz polecenia jako administrator. Zainstaluj `gulp` i `device-discovery-cli` , uruchamiając następujące polecenie:

```bash
npm install -g device-discovery-cli gulp
```

Jeśli występują problemy z instalacją środowiska Node.js i te dodatkowe narzędzia programistyczne Node.js na komputerze, zobacz [przewodnik rozwiązywania problemów](iot-hub-raspberry-pi-kit-node-troubleshooting.md) dla rozwiązania typowych problemów.

## <a name="install-visual-studio-code"></a>Zainstaluj kod programu Visual Studio
[Pobierz](https://code.visualstudio.com/docs/setup/windows) i zainstalować Visual Studio Code. Visual Studio Code to lekkie, ale jednocześnie wydajną źródła Edytor kodu dla systemu Windows, Linux i macOS. Umożliwia to edytor później w samouczku Edytuj przykładowy kod.

## <a name="summary"></a>Podsumowanie
Po zainstalowaniu narzędzi do tworzenia wymaganych i oprogramowania dla pierwszej aplikacji przykładowej. Następnym zadaniem jest tworzenie, wdrażanie i uruchom przykładową aplikację na Pi.

## <a name="next-steps"></a>Następne kroki
[Tworzenie i wdrażanie migania przykładowej aplikacji](iot-hub-raspberry-pi-kit-node-lesson1-deploy-blink-app.md)

