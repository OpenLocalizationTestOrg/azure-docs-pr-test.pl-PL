---
title: "Urządzeń Sensor tag & bramy IoT Azure - Lekcja 2: Pobierz narzędzia (system Windows) | Dokumentacja firmy Microsoft"
description: "Zainstaluj narzędzia hello i hello oprogramowania na komputerze hosta z systemem Windows, tworzenia Centrum IoT i zarejestrować urządzenie w Centrum IoT hello."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "Programowanie iot, oprogramowania iot iot usługi w chmurze internet rzeczy oprogramowania, azure cli, zainstaluj oprogramowanie git w systemie windows, system gulp Uruchom, zainstalowania systemu operacyjnego windows node js, instalowania npm w systemie windows, zainstaluj python w systemie windows"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-gateway-kit-c-lesson1-set-up-nuc
ms.assetid: 18ae6ee4-574a-4d5f-9838-ca2a78165628
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 3b30b60a0115413394992061a88dde4cd442ac19
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="get-hello-tools-windows-7-and-later"></a>Pobierz narzędzia hello (z systemem Windows 7 i nowsze)
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
- Komputer z systemem Windows.

## <a name="install-git-and-nodejs"></a>Zainstaluj usługi Git i Node.js

Kliknij następujące łącza toodownload hello i zainstaluj usługi Git i LTS Node.js dla systemu Windows.

- [Pobierz Git dla systemu Windows](https://git-scm.com/download/win/)
- [Pobierz Node.js LTS dla systemu Windows](https://nodejs.org/en/)

## <a name="install-nodejs-development-tools"></a>Instalowania narzędzi do tworzenia środowiska Node.js

Możesz użyć [gulp.js](http://gulpjs.com/) tooautomate wdrożenia i wykonywanie skryptów.

Naciśnij klawisz `Windows + R`, typ `cmd` i naciśnij klawisz `Enter` tooopen okno wiersza polecenia, a następnie hello uruchom następujące polecenie:

```cmd
npm install -g gulp
```

Jeśli wystąpią problemy z instalacją hello Zobacz hello [przewodnik rozwiązywania problemów](iot-hub-gateway-kit-c-troubleshooting.md) dla rozwiązania toocommon problemów.

> [!Note]
> Węzeł, NPM i Gulp są wymagane toorun skryptów automatyzacji opracowanych w środowisku Node.js.

## <a name="install-python"></a>Instalowanie języka Python

Można wybrać z Python 2.7 3.4 lub 3.5. W tym samouczku używamy Python 2.7. Jeśli po zainstalowaniu języka python, przejdź toohello następnej sekcji.

[Pobierz języka Python dla systemu Windows](https://www.python.org/downloads/)

Należy również tooadd hello ścieżki folderów hello skutkującej systemu zainstalowanych toohello Python.exe i pip.exe `PATH` zmiennej środowiskowej. Domyślnie python.exe jest zainstalowany w `C:\Python27` i pip.exe jest instalowany w `C:\Python27\Scripts`.

## <a name="install-hello-azure-cli"></a>Zainstaluj hello wiersza polecenia platformy Azure

Witaj tooinstall wiersza polecenia platformy Azure, wykonaj następujące kroki:

1. Otwórz okno wiersza polecenia z uprawnieniami administratora.

2. Zainstaluj hello Azure CLI, uruchamiając następujące polecenia hello:

   ```cmd
   pip install --upgrade azure-cli
   pip install --upgrade azure-cli-iot
   ```

   Witaj, instalacja może zająć 5 minut.

3. Sprawdź hello instalacji, uruchamiając następujące polecenie hello:

   ```cmd
   az iot -h
   ```

   Powinien pojawić się następujące hello output, jeśli hello Instalacja powiodła się.

   ![Sprawdzić, czy instalacja wiersza polecenia platformy Azure](media/iot-hub-gateway-kit-lessons/lesson2/az_iot_help_win.png)

## <a name="install-visual-studio-code"></a>Zainstaluj kod programu Visual Studio

W plikach konfiguracji samouczek tooedit hello można użyć programu Visual Studio Code później.

[Pobierz](https://code.visualstudio.com/docs/setup/windows) i zainstalować Visual Studio Code.

## <a name="summary"></a>Podsumowanie

Po zainstalowaniu wszystkich wymaganych hello i oprogramowania na komputerze hosta. Następnym zadaniem jest toouse hello Azure CLI toocreate Centrum IoT i zarejestrować urządzenie w Centrum IoT.

## <a name="next-steps"></a>Następne kroki
[Create an IoT hub and register your device](iot-hub-gateway-kit-c-lesson2-register-device.md) (Tworzenie centrum IoT Hub i rejestrowanie urządzenia)
