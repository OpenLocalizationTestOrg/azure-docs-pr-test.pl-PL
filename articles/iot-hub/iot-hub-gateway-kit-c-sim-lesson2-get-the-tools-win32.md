---
title: "Symulowane urządzenie & Azure IoT brama - 2 lekcji: Pobierz narzędzia (system Windows) | Dokumentacja firmy Microsoft"
description: "Zainstaluj narzędzia i oprogramowania na komputerze hosta z systemem Windows, Utwórz Centrum IoT i zarejestrować urządzenie w Centrum IoT."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "Programowanie iot, oprogramowania iot iot usługi w chmurze internet rzeczy oprogramowania, azure cli, zainstaluj oprogramowanie git w systemie windows, system gulp Uruchom, zainstalowania systemu operacyjnego windows node js, instalowania npm w systemie windows, zainstaluj python w systemie windows"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-gateway-kit-c-lesson1-set-up-nuc
ms.assetid: c16eee4c-8756-454b-82bf-3eb0dd51aa5f
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: ecedf5ef89677c73c5d9a3e5250eb9f45f6bad32
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="get-the-tools-windows-7-and-later"></a>Pobierz narzędzia (z systemem Windows 7 i nowsze)
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
- Komputer z systemem Windows.

## <a name="install-git-and-nodejs"></a>Zainstaluj usługi Git i Node.js

Kliknij poniższe łącza, aby pobrać i zainstalować usługi Git i LTS Node.js dla systemu Windows.

- [Pobierz Git dla systemu Windows](https://git-scm.com/download/win/)
- [Pobierz Node.js LTS dla systemu Windows](https://nodejs.org/en/)

## <a name="install-nodejs-development-tools"></a>Instalowania narzędzi do tworzenia środowiska Node.js

Możesz użyć [gulp.js](http://gulpjs.com/) do automatyzowania wdrażania i uruchamiania skryptów.

Naciśnij klawisz `Windows + R`, typ `cmd` i naciśnij klawisz `Enter` aby otworzyć okno wiersza polecenia, a następnie uruchom następujące polecenie:

```cmd
npm install -g gulp
```

Jeśli występują problemy z instalacją, zobacz [przewodnik rozwiązywania problemów](iot-hub-gateway-kit-c-sim-troubleshooting.md) dla rozwiązania typowych problemów.

> [!Note]
> Węzeł, NPM i Gulp są wymagane do uruchamiania skryptów automatyzacji opracowanych w środowisku Node.js.

## <a name="install-python"></a>Instalowanie języka Python

Można wybrać z Python 2.7 3.4 lub 3.5. W tym samouczku używamy Python 2.7. Jeśli po zainstalowaniu języka python, przejdź do następnej sekcji.

[Pobierz języka Python dla systemu Windows](https://www.python.org/downloads/)

Należy również dodać ścieżkę do folderów, w którym Python.exe i pip.exe są zainstalowane w systemie `PATH` zmiennej środowiskowej. Domyślnie python.exe jest zainstalowany w `C:\Python27` i pip.exe jest instalowany w `C:\Python27\Scripts`.

## <a name="install-the-azure-cli"></a>Zainstaluj interfejs wiersza polecenia platformy Azure

Aby zainstalować interfejs wiersza polecenia Azure, wykonaj następujące kroki:

1. Otwórz okno wiersza polecenia z uprawnieniami administratora.

2. Instalowanie interfejsu wiersza polecenia Azure, uruchamiając następujące polecenia:

   ```cmd
   pip install --upgrade azure-cli
   pip install --upgrade azure-cli-iot
   ```

   Instalacja może zająć 5 minut.

3. Instalację można zweryfikować, uruchamiając następujące polecenie:

   ```cmd
   az iot -h
   ```

   Następujące dane wyjściowe powinny być widoczne, jeśli instalacja zakończy się pomyślnie.

   ![Sprawdzić, czy instalacja wiersza polecenia platformy Azure](media/iot-hub-gateway-kit-lessons/lesson2/az_iot_help_win.png)

## <a name="install-visual-studio-code"></a>Zainstaluj kod programu Visual Studio

Używasz programu Visual Studio Code później w samouczku do edycji plików konfiguracji.

[Pobierz](https://code.visualstudio.com/docs/setup/windows) i zainstalować Visual Studio Code.

## <a name="summary"></a>Podsumowanie

Po zainstalowaniu wszystkich wymaganych narzędzi i oprogramowania na komputerze hosta. Następnym zadaniem jest korzystanie z wiersza polecenia platformy Azure w celu tworzenia Centrum IoT i zarejestrować urządzenie w Centrum IoT.

## <a name="next-steps"></a>Następne kroki
[Create an IoT hub and register your device](iot-hub-gateway-kit-c-sim-lesson2-register-device.md) (Tworzenie centrum IoT Hub i rejestrowanie urządzenia)
