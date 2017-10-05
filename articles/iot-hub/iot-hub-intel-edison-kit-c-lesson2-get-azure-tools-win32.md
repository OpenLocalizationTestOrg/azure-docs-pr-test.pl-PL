---
title: "Connect Intel Edison (C) do Azure IoT — Lekcja 2: narzędzi platformy Azure (system Windows) | Dokumentacja firmy Microsoft"
description: Zainstaluj Python i interfejsu wiersza polecenia platformy Azure (Azure CLI) w systemie Windows 7 i nowszych wersjach.
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "Interfejs wiersza polecenia platformy Azure, usługa w chmurze iot, arduino chmury"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-intel-edison-kit-c-get-started
ms.assetid: 1035760e-cdd1-4d99-8003-067e98b29762
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 90ef113ae84ccc8cb3cbdbe8c245e138320a93c6
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="get-azure-tools-windows-7-and-later"></a>Pobierz narzędzia Azure (z systemem Windows 7 i nowsze)
> [!div class="op_single_selector"]
> * [System Windows 7 lub nowszy][windows]
> * [Ubuntu 16.04][ubuntu]
> * [System macOS 10.10][macos]

## <a name="what-you-will-do"></a>Będzie wykonywać
Zainstaluj Python i interfejsu wiersza polecenia platformy Azure (Azure CLI). Jeśli masz problemy, poszukaj rozwiązania [Rozwiązywanie problemów z strony][troubleshooting].

## <a name="what-you-will-learn"></a>Co dowiesz się
W tym artykule dowiesz się:
* Jak zainstalować Python.
* Jak zainstalować wiersza polecenia platformy Azure.

## <a name="what-you-need"></a>Co jest potrzebne
* Komputer z systemem Windows z połączeniem internetowym.
* Aktywna subskrypcja platformy Azure. Jeśli nie masz konta platformy Azure, Utwórz [bezpłatnego konta wersji próbnej Azure](http://azure.microsoft.com/pricing/free-trial/) za kilka minut.

## <a name="install-python"></a>Instalowanie języka Python
[Instalowanie języka Python](https://www.python.org/downloads/) na komputerze z systemem Windows. Można zainstalować środowisko Python 2.7 3.4 lub 3.5. W tym samouczku jest oparty na języku Python 2.7. Jeśli po zainstalowaniu języka Python, przejdź do następnej sekcji i zainstaluj interfejs wiersza polecenia platformy Azure.

Należy również dodać ścieżkę do folderów, w którym python.exe i pip.exe są zainstalowane w systemie `PATH` zmiennej środowiskowej. Domyślnie python.exe jest zainstalowany w `C:\Python27` i pip.exe jest instalowany w `C:\Python27\Scripts`.

## <a name="install-the-azure-cli"></a>Zainstaluj interfejs wiersza polecenia platformy Azure
Interfejsu wiersza polecenia Azure zapewnia wiele platform wiersza polecenia platformy Azure. Praca bezpośrednio w wierszu polecenia do udostępniania i zarządzania zasobami.

Aby zainstalować interfejs wiersza polecenia Azure, wykonaj następujące kroki:

1. Otwórz okno wiersza polecenia z uprawnieniami administratora.
2. Uruchom następujące polecenia:

   ```cmd
   pip install --upgrade azure-cli
   pip install --upgrade azure-cli-iot
   ```
3. Instalację można zweryfikować, uruchamiając następujące polecenie:

   ```cmd
   az iot -h
   ```

Następujące dane wyjściowe zostanie wyświetlony, jeśli instalacja zakończy się pomyślnie.

![Dane wyjściowe, co oznacza Powodzenie](media/iot-hub-intel-edison-lessons/lesson2/az_iot_help_win.png)

## <a name="summary"></a>Podsumowanie
Po zainstalowaniu interfejsu wiersza polecenia Azure. Następnym zadaniem do tworzenia tożsamości koncentratora i urządzenia Azure IoT przy użyciu wiersza polecenia platformy Azure.

## <a name="next-steps"></a>Następne kroki
[Utworzenie Centrum IoT i zarejestruj Intel Edison][create-your-iot-hub-and-register-intel-edison]
<!-- Images and links -->

[troubleshooting]: iot-hub-intel-edison-kit-c-troubleshooting.md
[create-your-iot-hub-and-register-intel-edison]: iot-hub-intel-edison-kit-c-lesson2-prepare-azure-iot-hub.md
[windows]: iot-hub-intel-edison-kit-c-lesson2-get-azure-tools-win32.md
[ubuntu]: iot-hub-intel-edison-kit-c-lesson2-get-azure-tools-ubuntu.md
[macos]: iot-hub-intel-edison-kit-c-lesson2-get-azure-tools-mac.md
