---
title: "Urządzeń Sensor tag & bramy IoT Azure - Lekcja 2: Pobierz narzędzia (macOS) | Dokumentacja firmy Microsoft"
description: "Zainstaluj narzędzia na komputerze Mac, tworzenia Centrum IoT i zarejestrować urządzenie w Centrum IoT hello."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "Programowanie iot, oprogramowanie iot, iot usługi w chmurze internet rzeczy oprogramowania, interfejsu wiersza polecenia platformy azure, zainstaluj mac python, zainstaluj usługę git dla komputerów mac, gulp, uruchom instalację node js mac"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-gateway-kit-c-lesson1-set-up-nuc
ms.assetid: 94e538ef-9857-4023-9c3c-e92a0be7c395
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 44bce452690e18e6c803df564fdafcdda7f41c8c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="get-hello-tools-macos"></a>Pobierz narzędzia hello (MacOS)
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

- Jak tooinstall [Git](https://git-scm.com/) i [Node.js](https://nodejs.org/en/).
  - Git jest typu open source rozproszonego systemu kontroli wersji. Witaj Przykładowa aplikacja dla tej lekcji jest przechowywana na Git.
  - Node.js to środowisko uruchomieniowe JavaScript z ekosystemem sformatowanego pakietu.
- Jak toouse [NPM](https://www.npmjs.com/) tooinstall narzędzi do tworzenia środowiska Node.js.
  - Witaj minimalnej wymaganej wersji środowiska Node.js jest 4.5 LTS.
  - NPM jest jednym z hello menedżerów pakietu dla środowiska Node.js.
- Jak tooinstall Visual Studio Code.
  - Visual Studio Code jest międzyplatformowego Edytor kodu źródłowego lekkie, ale jednocześnie wydajną dla systemu Windows, Linux i macOS. Ma ona doskonałą pomoc techniczną debugowania, osadzonego formantu Git, wyróżniania składni, uzupełniania kodu inteligentnego, wstawki i kod refaktoryzacji również.
- Jak tooinstall języka Python.
  - Python to powszechnie używany język programowania wysokiego poziomu, ogólnego przeznaczenia, interpretowany i dynamicznych.
- Jak tooinstall hello wiersza polecenia platformy Azure.
  - Witaj interfejsu wiersza polecenia Azure zapewnia wiele platform wiersza polecenia platformy Azure. Praca bezpośrednio z tooprovision wiersza polecenia i zarządzanie zasobami.
- Jak toouse hello toocreate interfejsu wiersza polecenia Azure IoT hub.

## <a name="what-you-need"></a>Co jest potrzebne

- Toodownload połączenia internetowego hello i oprogramowania.
- Komputer Mac z systemem OS X Yosemite (10.10) lub nowszym.

## <a name="install-git-and-nodejs"></a>Zainstaluj usługi Git i Node.js

tooinstall Git i Node.js, należy użyć narzędzia zarządzania pakietów oprogramowania Homebrew hello, wykonaj następujące czynności:

1. [Pobierz](http://brew.sh/) i zainstalowania oprogramowania Homebrew. Jeśli po zainstalowaniu oprogramowania Homebrew, przejdź toostep 2.
   1. Naciśnij klawisz `Cmd + Space` , a następnie wprowadź `Terminal` tooopen terminalu.
   2. Uruchom następujące polecenie hello:

      ```bash
      /usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
      ```

2. Zainstaluj usługi Git i Node.js, uruchamiając następujące polecenie hello:

    ```bash
    brew install node git
    ```

## <a name="install-nodejs-development-tools"></a>Instalowania narzędzi do tworzenia środowiska Node.js

Możesz użyć [gulp.js](http://gulpjs.com/) tooautomate wdrożenia i wykonywanie skryptów.

gulp tooinstall, uruchom następujące polecenie w terminalu hello hello:

```bash
npm install -g gulp
```

Jeśli wystąpią problemy z instalacją hello Zobacz hello [przewodnik rozwiązywania problemów](iot-hub-gateway-kit-c-troubleshooting.md) dla rozwiązania toocommon problemów.

> [!Note]
> Węzeł, NPM i Gulp są wymagane toorun skryptów automatyzacji opracowanych w środowisku Node.js.

## <a name="install-python"></a>Instalowanie języka Python

Mimo że systemu Mac OS X jest dostarczany z Python 2.7, zaleca się zainstalowanie Python za pomocą oprogramowania Homebrew. Zobacz [instalacji języka Python w systemie Mac OS X](http://docs.python-guide.org/en/latest/starting/install/osx/).

Zainstaluj Python oraz narzędzia pip, uruchamiając następujące polecenie hello:

```bash
brew install python
```

## <a name="install-hello-azure-cli"></a>Zainstaluj hello wiersza polecenia platformy Azure

Witaj tooinstall wiersza polecenia platformy Azure, wykonaj następujące kroki:

1. Uruchom następujące polecenia w terminalu hello hello:
   ```bash
   pip install --upgrade azure-cli
   pip install --upgrade azure-cli-iot
   ```
   Witaj, instalacja może zająć 5 minut.

2. Sprawdź hello instalacji, uruchamiając następujące polecenie hello:
   ```bash
   az iot -h
   ```
   Powinien pojawić się następujące hello output, jeśli hello Instalacja powiodła się.

   ![Sprawdzić, czy instalacja wiersza polecenia platformy Azure](media/iot-hub-gateway-kit-lessons/lesson2/az_iot_help_osx.png)

## <a name="install-visual-studio-code"></a>Zainstaluj kod programu Visual Studio

W plikach konfiguracji samouczek tooedit hello można użyć programu Visual Studio Code później.

[Pobierz](https://code.visualstudio.com/docs/setup/osx) i zainstalować Visual Studio Code.

## <a name="summary"></a>Podsumowanie

Na komputerze Mac, że zainstalowano wszystkie wymagane hello i oprogramowania. Następnym zadaniem jest toouse hello Azure CLI toocreate Centrum IoT i zarejestrować urządzenie w Centrum IoT.

## <a name="next-steps"></a>Następne kroki
[Tworzenie Centrum IoT i rejestrowanie urządzenia](iot-hub-gateway-kit-c-lesson2-register-device.md)
