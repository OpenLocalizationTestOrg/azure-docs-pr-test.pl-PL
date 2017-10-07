---
title: "Połącz Pi malina (węzeł) tooAzure IoT — Lekcja 1: Pobierz narzędzia (Ubuntu) | Dokumentacja firmy Microsoft"
description: "Pobierz i zainstaluj na Ubuntu hello niezbędne narzędzia i oprogramowania dla pierwszej aplikacji przykładowej hello pi."
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: Programowanie iot oprogramowania iot, internet rzeczy oprogramowania, zainstaluj system git, ubuntu, system gulp Uruchom, zainstaluj node js ubuntu
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-raspberry-pi-kit-node-get-started
ms.assetid: 4d5e45c0-1db9-4662-a039-99ba26333085
ms.service: iot-hub
ms.devlang: node
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: b4f566fa0d1faf8b2321707145f675e3d87f0bef
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="get-hello-tools-ubuntu-1604"></a>Pobierz narzędzia hello (Ubuntu 16.04)

> [!div class="op_single_selector"]
> * [Windows 7 lub nowszy](iot-hub-raspberry-pi-kit-node-lesson1-get-the-tools-win32.md)
> * [Ubuntu 16.04](iot-hub-raspberry-pi-kit-node-lesson1-get-the-tools-ubuntu.md)
> * [System macOS 10.10](iot-hub-raspberry-pi-kit-node-lesson1-get-the-tools-mac.md)


## <a name="what-you-will-do"></a>Będzie wykonywać
Pobierz oprogramowanie hello hello pierwszy przykładowej aplikacji malina Pi 3 i narzędzia deweloperskie hello. Jeśli masz problemy, poszukaj rozwiązania na powitania [Rozwiązywanie problemów z strony](iot-hub-raspberry-pi-kit-node-troubleshooting.md).

## <a name="what-you-will-learn"></a>Co dowiesz się
W tym artykule dowiesz się:

* Jak tooinstall Git i Node.js.
  * [Git](https://git-scm.com) jest typu open source rozproszonego systemu kontroli wersji. Witaj Przykładowa aplikacja dla tego artykułu znajduje się na Git.
  * [Node.js](https://nodejs.org/en/) jest środowiska wykonawczego języka JavaScript z ekosystemem sformatowanego pakietu.
* Jak toouse NPM tooinstall dodatkowe Node.js narzędzia deweloperskie.
  * Witaj minimalnej wymaganej wersji środowiska Node.js jest 4.5 LTS.
  * [NPM](https://www.npmjs.com) jest jednym z hello menedżerów pakietu dla środowiska Node.js.

## <a name="what-do-you-need"></a>Czego potrzebujesz
toocomplete tej operacji, należy:

* Toodownload połączenia internetowego hello narzędzia deweloperskie i hello oprogramowania.
* Komputer z systemem Ubuntu 16.04 lub nowszej.

## <a name="install-git-nodejs-and-npm"></a>Zainstaluj narzędzia Git, Node.js i NPM
Skrót klawiaturowy używany hello `Ctrl + Alt + T` tooopen hello terminalu i uruchom następujące polecenia:

```bash
sudo apt-get update
curl -sL https://deb.nodesource.com/setup_6.x | sudo -E bash -
sudo apt-get install -y nodejs
sudo apt-get install git
```

## <a name="install-additional-nodejs-development-tools"></a>Instalowania dodatkowych narzędzi do tworzenia środowiska Node.js
Możesz użyć [gulp.js](http://gulpjs.com) tooautomate wdrożenie hello hello przykładowej aplikacji tooPi. Możesz również użyć hello [urządzenia odnajdywania cli](https://github.com/Azure/device-discovery-cli) tooretrieve sieci informacje o urządzeniach IoT.

Zainstaluj `gulp` i `device-discovery-cli` , uruchamiając następujące polecenie w terminalu hello hello:

```bash
sudo npm install -g device-discovery-cli gulp
```

Jeśli wystąpią problemy z instalacją środowiska Node.js i te narzędzia programistyczne dodatkowe na Ubuntu Zobacz hello [przewodnik rozwiązywania problemów](iot-hub-raspberry-pi-kit-node-troubleshooting.md) dla rozwiązania toocommon problemów.

## <a name="install-visual-studio-code"></a>Zainstaluj kod programu Visual Studio
[Pobierz](https://code.visualstudio.com/docs/setup/linux) i zainstalować Visual Studio Code. Visual Studio Code to lekkie, ale jednocześnie wydajną źródła Edytor kodu dla systemu Windows, Linux i macOS. Edytor w dalszej części hello samouczek tooedit hello przykładowy kod.

## <a name="summary"></a>Podsumowanie
Po zainstalowaniu oprogramowania hello pierwszy przykładowej aplikacji i narzędzia deweloperskie hello wymagane. następne zadanie Hello jest toocreate, wdrażanie i uruchamianie hello przykładowej aplikacji na Pi.

## <a name="next-steps"></a>Następne kroki
[Tworzenie i wdrażanie hello migania przykładowej aplikacji](iot-hub-raspberry-pi-kit-node-lesson1-deploy-blink-app.md)

