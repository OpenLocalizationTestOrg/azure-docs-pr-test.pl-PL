---
title: "Urządzeń Sensor tag & bramy IoT Azure - Lekcja 2: Pobierz narzędzia (Ubuntu) | Dokumentacja firmy Microsoft"
description: "Zainstaluj narzędzia hello i hello oprogramowania na komputerze hosta z systemem Ubuntu, tworzenia Centrum IoT i zarejestrować urządzenie w Centrum IoT hello."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "Programowanie iot, oprogramowania iot iot usługi w chmurze internet rzeczy oprogramowania, azure cli, zainstaluj system git, ubuntu, system gulp uruchomienia, zainstaluj node js ubuntu"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-gateway-kit-c-lesson1-set-up-nuc
ms.assetid: 0bac1412-385b-4255-a33f-9d44c35feb3e
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: c9edca91e791ef914b1920178b66eadd12ae0281
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="get-hello-tools-ubuntu-1604"></a>Pobierz narzędzia hello (Ubuntu 16.04)
> [!div class="op_single_selector"]
> * [Windows 7 lub nowszy](iot-hub-gateway-kit-c-lesson2-get-the-tools-win32.md)
> * [Ubuntu 16.04](iot-hub-gateway-kit-c-lesson2-get-the-tools-ubuntu.md)
> * [System macOS 10.10](iot-hub-gateway-kit-c-lesson2-get-the-tools-mac.md)

## <a name="what-you-will-do"></a>Będzie wykonywać

- Zainstaluj narzędzia Git, Node.js, Gulp, Python.
- Zainstaluj hello interfejsu wiersza polecenia platformy Azure (Azure CLI). 

Jeśli masz problemy, poszukaj rozwiązania na powitania [Rozwiązywanie problemów z strony](iot-hub-gateway-kit-c-troubleshooting.md).
## <a name="what-you-will-learn"></a>Co dowiesz się

W tej lekcji dowiesz się:

- Jak tooinstall Git i Node.js.
  - Git jest typu open source rozproszonego systemu kontroli wersji. Witaj Przykładowa aplikacja dla tej lekcji jest przechowywana na Git.
  - Node.js to środowisko uruchomieniowe JavaScript z ekosystemem sformatowanego pakietu.
- Jak narzędzia deweloperskie toouse NPM tooinstall Node.js.
  - Witaj minimalnej wymaganej wersji środowiska Node.js jest 4.5 LTS.
  - NPM jest jednym z hello menedżerów pakietu dla środowiska Node.js.
- Jak tooinstall Visual Studio Code.
  - Visual Studio Code jest międzyplatformowego Edytor kodu źródłowego lekkie, ale jednocześnie wydajną dla systemu Windows, Linux i macOS. Ma ona doskonałą pomoc techniczną debugowania, osadzonego formantu Git, wyróżniania składni, uzupełniania kodu inteligentnego, wstawki i kod refaktoryzacji również.
- Jak tooinstall hello wiersza polecenia platformy Azure
  - Witaj interfejsu wiersza polecenia Azure zapewnia wiele platform wiersza polecenia platformy Azure. Praca bezpośrednio z tooprovision wiersza polecenia i zarządzanie zasobami.
- Jak toouse hello toocreate interfejsu wiersza polecenia Azure IoT hub.

## <a name="what-you-need"></a>Co jest potrzebne

- Toodownload połączenia internetowego hello i oprogramowania.
- Komputer z systemem Ubuntu 16.04 lub nowszej.

## <a name="install-git-and-nodejs"></a>Zainstaluj usługi Git i Node.js

tooinstall Git i Node.js, wykonaj następujące kroki:

1. Naciśnij klawisz `Ctrl + Alt + T` tooopen terminalu.
2. Uruchom następujące polecenia hello:

   ```bash
   sudo apt-get update
   curl -sL https://deb.nodesource.com/setup_6.x | sudo -E bash -
   sudo apt-get install -y nodejs
   sudo apt-get install git
   ```

## <a name="install-nodejs-development-tools"></a>Instalowania narzędzi do tworzenia środowiska Node.js

Możesz użyć [gulp.js](http://gulpjs.com/) tooautomate wdrożenia i wykonywanie skryptów.

gulp tooinstall, uruchom następujące polecenie w terminalu hello hello:

```bash
sudo npm install -g gulp
```

Jeśli wystąpią problemy z instalacją hello Zobacz hello [przewodnik rozwiązywania problemów](iot-hub-gateway-kit-c-troubleshooting.md) dla rozwiązania toocommon problemów.

> [!Note]
> Węzeł, NPM i Gulp są wymagane toorun skryptów automatyzacji opracowanych w środowisku Node.js.

## <a name="install-hello-azure-cli"></a>Zainstaluj hello wiersza polecenia platformy Azure

Witaj tooinstall wiersza polecenia platformy Azure, wykonaj następujące kroki:

1. Uruchom następujące polecenia w terminalu hello hello:

   ```bash
   sudo apt-get update
   sudo apt-get install -y libssl-dev libffi-dev
   sudo apt-get install -y python-dev
   sudo apt-get install -y build-essential
   sudo apt-get install -y python-pip
   sudo pip install --upgrade azure-cli
   sudo pip install --upgrade azure-cli-iot
   ```

   Witaj, instalacja może zająć 5 minut.

2. Sprawdź hello instalacji, uruchamiając następujące polecenie hello:

   ```bash
   az iot -h
   ```
Powinien pojawić się następujące hello output, jeśli hello Instalacja powiodła się.
![Sprawdzić, czy instalacja wiersza polecenia platformy Azure](media/iot-hub-gateway-kit-lessons/lesson2/az_iot_help_ubuntu.png)

### <a name="install-visual-studio-code"></a>Zainstaluj kod programu Visual Studio

W plikach konfiguracji samouczek tooedit hello można użyć programu Visual Studio Code później.

[Pobierz](https://code.visualstudio.com/docs/setup/linux) i zainstalować Visual Studio Code.

## <a name="summary"></a>Podsumowanie

Po zainstalowaniu wszystkich wymaganych hello i oprogramowania na komputerze hosta. Następnym zadaniem jest toouse hello Azure CLI toocreate Centrum IoT i zarejestrować urządzenie w Centrum IoT.

## <a name="next-steps"></a>Następne kroki
[Create an IoT hub and register your device](iot-hub-gateway-kit-c-lesson2-register-device.md) (Tworzenie centrum IoT Hub i rejestrowanie urządzenia)
