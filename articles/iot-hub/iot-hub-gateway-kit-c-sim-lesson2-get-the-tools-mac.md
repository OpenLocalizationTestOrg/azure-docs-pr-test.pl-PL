---
title: "Symulowane urządzenie & Azure IoT brama - 2 lekcji: Pobierz narzędzia (macOS) | Dokumentacja firmy Microsoft"
description: "Zainstaluj narzędzia na komputerze Mac, tworzenia Centrum IoT i zarejestrować urządzenie w Centrum IoT."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "Programowanie iot, oprogramowanie iot, iot usługi w chmurze internet rzeczy oprogramowania, interfejsu wiersza polecenia platformy azure, zainstaluj mac python, zainstaluj usługę git dla komputerów mac, gulp, uruchom instalację node js mac"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-gateway-kit-c-lesson1-set-up-nuc
ms.assetid: 42f9d186-e20c-4ef9-98cc-71d39e058b06
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: d86332816130de7a6951a74ceb215c8ce476d5f8
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="get-the-tools-macos"></a>Pobierz narzędzia (macOS)
> [!div class="op_single_selector"]
> * [Windows 7 lub nowszy](iot-hub-gateway-kit-c-sim-lesson2-get-the-tools-win32.md)
> * [Ubuntu 16.04](iot-hub-gateway-kit-c-sim-lesson2-get-the-tools-ubuntu.md)
> * [System macOS 10.10](iot-hub-gateway-kit-c-sim-lesson2-get-the-tools-mac.md)

## <a name="what-you-will-do"></a>Będzie wykonywać

- Zainstaluj narzędzia Git, Node.js, Gulp, Python.
- Zainstaluj interfejs wiersza polecenia platformy Azure (Azure CLI). 

Jeśli masz problemy, poszukaj rozwiązania [Rozwiązywanie problemów z strony](iot-hub-gateway-kit-c-sim-troubleshooting.md).

## <a name="what-you-will-learn"></a>Co dowiesz się

W tej lekcji dowiesz się:

- Jak zainstalować [Git](https://git-scm.com/) i [Node.js](https://nodejs.org/en/).
  - Git jest typu open source rozproszonego systemu kontroli wersji. Przykładowa aplikacja dla tej lekcji jest przechowywana na Git.
  - Node.js to środowisko uruchomieniowe JavaScript z ekosystemem sformatowanego pakietu.
- Jak używać [NPM](https://www.npmjs.com/) do instalowania narzędzi do tworzenia środowiska Node.js.
  - Minimalna wymagana wersja programu Node.js jest 4.5 LTS.
  - NPM jest jednym z wybranych menedżerów pakietu dla środowiska Node.js.
- Jak zainstalować program Visual Studio Code.
  - Visual Studio Code jest międzyplatformowego Edytor kodu źródłowego lekkie, ale jednocześnie wydajną dla systemu Windows, Linux i macOS. Ma ona doskonałą pomoc techniczną debugowania, osadzonego formantu Git, wyróżniania składni, uzupełniania kodu inteligentnego, wstawki i kod refaktoryzacji również.
- Jak zainstalować Python.
  - Python to powszechnie używany język programowania wysokiego poziomu, ogólnego przeznaczenia, interpretowany i dynamicznych.
- Jak zainstalować wiersza polecenia platformy Azure.
  - Interfejsu wiersza polecenia Azure zapewnia wiele platform wiersza polecenia platformy Azure. Praca bezpośrednio z poziomu wiersza polecenia do udostępniania i zarządzania zasobami.
- Sposób użycia interfejsu wiersza polecenia Azure do tworzenia Centrum IoT.

## <a name="what-you-need"></a>Co jest potrzebne

- Połączenia internetowego do pobierania narzędzia i oprogramowania.
- Komputer Mac z systemem OS X Yosemite (10.10) lub nowszym.

## <a name="install-git-and-nodejs"></a>Zainstaluj usługi Git i Node.js

Aby zainstalować usługi Git i Node.js, należy użyć narzędzia zarządzania pakietów oprogramowania Homebrew wykonaj następujące czynności:

1. [Pobierz](http://brew.sh/) i zainstalowania oprogramowania Homebrew. Jeśli po zainstalowaniu oprogramowania Homebrew, przejdź do kroku 2.
   1. Naciśnij klawisz `Cmd + Space` , a następnie wprowadź `Terminal` otworzyć terminal.
   2. Uruchom następujące polecenie:

      ```bash
      /usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
      ```

2. Zainstaluj usługi Git i Node.js, uruchamiając następujące polecenie:

    ```bash
    brew install node git
    ```

## <a name="install-nodejs-development-tools"></a>Instalowania narzędzi do tworzenia środowiska Node.js

Możesz użyć [gulp.js](http://gulpjs.com/) do automatyzowania wdrażania i uruchamiania skryptów.

Aby zainstalować gulp, uruchom następujące polecenie z poziomu terminala:

```bash
npm install -g gulp
```

Jeśli występują problemy z instalacją, zobacz [przewodnik rozwiązywania problemów](iot-hub-gateway-kit-c-sim-troubleshooting.md) dla rozwiązania typowych problemów.

> [!Note]
> Węzeł, NPM i Gulp są wymagane do uruchamiania skryptów automatyzacji opracowanych w środowisku Node.js.

## <a name="install-python"></a>Instalowanie języka Python

Mimo że systemu Mac OS X jest dostarczany z Python 2.7, zaleca się zainstalowanie Python za pomocą oprogramowania Homebrew. Zobacz [instalacji języka Python w systemie Mac OS X](http://docs.python-guide.org/en/latest/starting/install/osx/).

Zainstaluj Python oraz narzędzia pip, uruchamiając następujące polecenie:

```bash
brew install python
```

## <a name="install-the-azure-cli"></a>Zainstaluj interfejs wiersza polecenia platformy Azure

Aby zainstalować interfejs wiersza polecenia Azure, wykonaj następujące kroki:

1. Uruchom następujące polecenia z poziomu terminala:
   ```bash
   pip install --upgrade azure-cli
   pip install --upgrade azure-cli-iot
   ```
   Instalacja może zająć 5 minut.

2. Instalację można zweryfikować, uruchamiając następujące polecenie:
   ```bash
   az iot -h
   ```
   Następujące dane wyjściowe powinny być widoczne, jeśli instalacja zakończy się pomyślnie.

   ![Sprawdzić, czy instalacja wiersza polecenia platformy Azure](media/iot-hub-gateway-kit-lessons/lesson2/az_iot_help_osx.png)

## <a name="install-visual-studio-code"></a>Zainstaluj kod programu Visual Studio

Używasz programu Visual Studio Code później w samouczku do edycji plików konfiguracji.

[Pobierz](https://code.visualstudio.com/docs/setup/osx) i zainstalować Visual Studio Code.

## <a name="summary"></a>Podsumowanie

Na komputerze Mac, że zainstalowano wszystkie wymagane narzędzia i oprogramowania. Następnym zadaniem jest korzystanie z wiersza polecenia platformy Azure w celu tworzenia Centrum IoT i zarejestrować urządzenie w Centrum IoT.

## <a name="next-steps"></a>Następne kroki
[Tworzenie Centrum IoT i rejestrowanie urządzenia](iot-hub-gateway-kit-c-sim-lesson2-register-device.md)
