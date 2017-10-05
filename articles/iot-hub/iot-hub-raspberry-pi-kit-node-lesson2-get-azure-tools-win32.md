---
title: "Nawiązać Pi malina (węzeł) Azure IoT — Lekcja 2: Pobierz narzędzia (system Windows) | Dokumentacja firmy Microsoft"
description: Zainstaluj Python i interfejsu wiersza polecenia platformy Azure (Azure CLI) w systemie Windows 7 i nowszych wersjach.
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: "iot chmury usługi azure cli"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-raspberry-pi-kit-node-get-started
ms.assetid: acfa13e3-6d2c-4e68-9a77-1cbc2cf3f9c1
ms.service: iot-hub
ms.devlang: node
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: c7b927997b738f7a80b71c06d4dff2278dc7c64e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="get-azure-tools-windows-7-and-later"></a>Pobierz narzędzia Azure (z systemem Windows 7 i nowsze)
> [!div class="op_single_selector"]
> * [System Windows 7 lub nowszy](iot-hub-raspberry-pi-kit-node-lesson2-get-azure-tools-win32.md)
> * [Ubuntu 16.04](iot-hub-raspberry-pi-kit-node-lesson2-get-azure-tools-ubuntu.md)
> * [System macOS 10.10](iot-hub-raspberry-pi-kit-node-lesson2-get-azure-tools-mac.md)

## <a name="what-you-will-do"></a>Będzie wykonywać
Zainstaluj Python i interfejsu wiersza polecenia platformy Azure (Azure CLI). Jeśli masz problemy, poszukaj rozwiązania [Rozwiązywanie problemów z strony](iot-hub-raspberry-pi-kit-node-troubleshooting.md).

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
Interfejsu wiersza polecenia Azure zapewnia wiele platform wiersza polecenia platformy Azure. Możesz pracować bezpośrednio z z wiersza polecenia do obsługi administracyjnej zasobów i zarządzanie nimi.

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
[Utworzenie Centrum IoT i zarejestruj malina Pi 3](iot-hub-raspberry-pi-kit-node-lesson2-prepare-azure-iot-hub.md)

