---
title: "Connect Raspberry pi (C) tooAzure IoT — Lekcja 2: narzędzi platformy Azure (system Windows) | Dokumentacja firmy Microsoft"
description: Zainstaluj Python i hello interfejsu wiersza polecenia platformy Azure (Azure CLI) w systemie Windows 7 i nowszych wersjach.
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
ms.openlocfilehash: 1819d61fafbee6ac42a1bea5c16437cd8bf43af9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="get-azure-tools-windows-7-and-later"></a>Pobierz narzędzia Azure (z systemem Windows 7 i nowsze)
> [!div class="op_single_selector"]
> * [System Windows 7 lub nowszy](iot-hub-raspberry-pi-kit-c-lesson2-get-azure-tools-win32.md)
> * [Ubuntu 16.04](iot-hub-raspberry-pi-kit-c-lesson2-get-azure-tools-ubuntu.md)
> * [System macOS 10.10](iot-hub-raspberry-pi-kit-c-lesson2-get-azure-tools-mac.md)

## <a name="what-you-will-do"></a>Będzie wykonywać
Zainstaluj Python i hello interfejsu wiersza polecenia platformy Azure (Azure CLI). Jeśli masz problemy, poszukaj rozwiązania na powitania [Rozwiązywanie problemów z strony](iot-hub-raspberry-pi-kit-c-troubleshooting.md).

## <a name="what-you-will-learn"></a>Co dowiesz się
W tym artykule dowiesz się:
* Jak tooinstall języka Python.
* Jak tooinstall hello wiersza polecenia platformy Azure.

## <a name="what-you-need"></a>Co jest potrzebne
* Komputer z systemem Windows z połączeniem internetowym.
* Aktywna subskrypcja platformy Azure. Jeśli nie masz konta platformy Azure, Utwórz [bezpłatnego konta wersji próbnej Azure](http://azure.microsoft.com/pricing/free-trial/) za kilka minut.

## <a name="install-python"></a>Instalowanie języka Python
[Instalowanie języka Python](https://www.python.org/downloads/) na komputerze z systemem Windows. Można zainstalować środowisko Python 2.7 3.4 lub 3.5. W tym samouczku jest oparty na języku Python 2.7. Po zainstalowaniu języka Python, przejdź do następnej sekcji toohello i zainstalować hello wiersza polecenia platformy Azure.

Należy również tooadd hello ścieżki folderów hello skutkującej systemu zainstalowanych toohello python.exe i pip.exe `PATH` zmiennej środowiskowej. Domyślnie python.exe jest zainstalowany w `C:\Python27` i pip.exe jest instalowany w `C:\Python27\Scripts`.

## <a name="install-hello-azure-cli"></a>Zainstaluj hello wiersza polecenia platformy Azure
Witaj interfejsu wiersza polecenia Azure zapewnia wiele platform wiersza polecenia platformy Azure. Praca bezpośrednio z tooprovision z wiersza polecenia i zarządzanie zasobami.

Witaj tooinstall wiersza polecenia platformy Azure, wykonaj następujące kroki:

1. Otwórz okno wiersza polecenia z uprawnieniami administratora.
2. Uruchom następujące polecenia hello:

   ```bash
   pip install --upgrade azure-cli
   pip install --upgrade azure-cli-iot
   ```
3. Sprawdź hello instalacji, uruchamiając następujące polecenie hello:

   ```bash
   az iot -h
   ```

Zobaczysz, że hello następujących danych wyjściowych, jeśli hello Instalacja powiodła się.

![Dane wyjściowe, co oznacza Powodzenie](media/iot-hub-raspberry-pi-lessons/lesson2/az_iot_help_win.png)

## <a name="summary"></a>Podsumowanie
Po zainstalowaniu hello wiersza polecenia platformy Azure. Następnego zadań toocreate tożsamości koncentratora i urządzenia Azure IoT przy użyciu hello wiersza polecenia platformy Azure.

## <a name="next-steps"></a>Następne kroki
[Utworzenie Centrum IoT i zarejestruj malina Pi 3](iot-hub-raspberry-pi-kit-c-lesson2-prepare-azure-iot-hub.md)

