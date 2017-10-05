---
title: "Connect Raspberry pi (C) do Azure IoT — Lekcja 2: narzędzi platformy Azure (system Windows) | Dokumentacja firmy Microsoft"
description: Zainstaluj Python i interfejsu wiersza polecenia platformy Azure (Azure CLI) w systemie Windows 7 i nowszych wersjach.
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "iot chmury usługi azure cli"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-raspberry-pi-kit-c-get-started
ms.assetid: a3c083b5-0d76-46af-bc77-2ad7d8aadc1e
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: aa96000cb676c088a90f2b3d45c159913185a2e1
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="get-azure-tools-windows-7-and-later"></a>Pobierz narzędzia Azure (z systemem Windows 7 i nowsze)
> [!div class="op_single_selector"]
> * [System Windows 7 lub nowszy](iot-hub-raspberry-pi-kit-c-lesson2-get-azure-tools-win32.md)
> * [Ubuntu 16.04](iot-hub-raspberry-pi-kit-c-lesson2-get-azure-tools-ubuntu.md)
> * [System macOS 10.10](iot-hub-raspberry-pi-kit-c-lesson2-get-azure-tools-mac.md)

## <a name="what-you-will-do"></a>Będzie wykonywać
Zainstaluj Python i interfejsu wiersza polecenia platformy Azure (Azure CLI). Jeśli masz problemy, poszukaj rozwiązania [Rozwiązywanie problemów z strony](iot-hub-raspberry-pi-kit-c-troubleshooting.md).

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

   ```bash
   pip install --upgrade azure-cli
   pip install --upgrade azure-cli-iot
   ```
3. Instalację można zweryfikować, uruchamiając następujące polecenie:

   ```bash
   az iot -h
   ```

Następujące dane wyjściowe zostanie wyświetlony, jeśli instalacja zakończy się pomyślnie.

![Dane wyjściowe, co oznacza Powodzenie](media/iot-hub-raspberry-pi-lessons/lesson2/az_iot_help_win.png)

## <a name="summary"></a>Podsumowanie
Po zainstalowaniu interfejsu wiersza polecenia Azure. Następnym zadaniem do tworzenia tożsamości koncentratora i urządzenia Azure IoT przy użyciu wiersza polecenia platformy Azure.

## <a name="next-steps"></a>Następne kroki
[Utworzenie Centrum IoT i zarejestruj malina Pi 3](iot-hub-raspberry-pi-kit-c-lesson2-prepare-azure-iot-hub.md)

