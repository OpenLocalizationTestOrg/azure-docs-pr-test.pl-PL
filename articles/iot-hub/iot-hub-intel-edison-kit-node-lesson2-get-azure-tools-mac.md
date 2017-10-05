---
title: "Nawiązać Edison firmy Intel (węzeł) Azure IoT — Lekcja 2: narzędzi platformy Azure (macOS) | Dokumentacja firmy Microsoft"
description: "Zainstaluj środowisko Python i interfejsu wiersza polecenia platformy Azure (Azure CLI) na macOS."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "Interfejs wiersza polecenia platformy Azure, usługa w chmurze iot, arduino chmury"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-intel-edison-kit-node-get-started
ms.assetid: 8a2a8031-b1a6-4219-b17d-2825550c35e1
ms.service: iot-hub
ms.devlang: nodejs
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 16705d54e90ee1482822986ca8c581a192e8702f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="get-azure-tools-macos-1010"></a>Pobierz narzędzia Azure (macOS 10.10)
> [!div class="op_single_selector"]
> * [System Windows 7 lub nowszy][windows]
> * [Ubuntu 16.04][ubuntu]
> * [System macOS 10.10][macos]

## <a name="what-you-will-do"></a>Będzie wykonywać
Zainstaluj interfejs wiersza polecenia platformy Azure (Azure CLI). Jeśli masz problemy, poszukaj rozwiązania [Rozwiązywanie problemów z strony][troubleshooting].

## <a name="what-you-will-learn"></a>Co dowiesz się
W tym artykule dowiesz się:
* Jak zainstalować wiersza polecenia platformy Azure.
* Jak dodać podgrupę IoT wiersza polecenia platformy Azure.

## <a name="what-you-need"></a>Co jest potrzebne
* Mac z połączeniem internetowym.
* Aktywna subskrypcja platformy Azure. Jeśli nie masz konta platformy Azure, możesz utworzyć [bezpłatnego konta wersji próbnej Azure](http://azure.microsoft.com/pricing/free-trial/) za kilka minut.

## <a name="install-python"></a>Instalowanie języka Python
Mimo że macOS zawiera Python 2.7 fabrycznej, zaleca się zainstalowanie Python za pomocą oprogramowania Homebrew. Zobacz [instalowanie Python na macOS](http://docs.python-guide.org/en/latest/starting/install/osx/).

Zainstaluj Python oraz narzędzia pip, uruchamiając następujące polecenie:

```bash
brew install python
```

## <a name="install-the-azure-cli"></a>Zainstaluj interfejs wiersza polecenia platformy Azure
Interfejsu wiersza polecenia Azure zapewnia wiele platform wiersza polecenia platformy Azure. Praca bezpośrednio w wierszu polecenia do udostępniania i zarządzania zasobami. 

Aby zainstalować najnowsze wiersza polecenia platformy Azure, wykonaj następujące kroki:

1. Uruchom następujące polecenia w oknie terminalu. Może upłynąć pięć minut na zainstalowanie wiersza polecenia platformy Azure.

   ```bash
   pip install --upgrade azure-cli
   pip install --upgrade azure-cli-iot
   ```
2. Instalację można zweryfikować, uruchamiając następujące polecenie:

   ```bash
   az iot -h
   ```

Następujące dane wyjściowe powinny być widoczne, jeśli instalacja zakończy się pomyślnie.

![Dane wyjściowe, co oznacza Powodzenie](media/iot-hub-intel-edison-lessons/lesson2/az_iot_help_osx.png)

## <a name="summary"></a>Podsumowanie
Po zainstalowaniu interfejsu wiersza polecenia Azure. Następnym zadaniem będzie można utworzyć tożsamości koncentratora i urządzenia Azure IoT przy użyciu wiersza polecenia platformy Azure.

## <a name="next-steps"></a>Następne kroki
[Utworzenie Centrum IoT i zarejestruj Intel Edison][create-your-iot-hub-and-register-intel-edison]
<!-- Images and links -->

[troubleshooting]: iot-hub-intel-edison-kit-node-troubleshooting.md
[create-your-iot-hub-and-register-intel-edison]: iot-hub-intel-edison-kit-node-lesson2-prepare-azure-iot-hub.md
[windows]: iot-hub-intel-edison-kit-node-lesson2-get-azure-tools-win32.md
[ubuntu]: iot-hub-intel-edison-kit-node-lesson2-get-azure-tools-ubuntu.md
[macos]: iot-hub-intel-edison-kit-node-lesson2-get-azure-tools-mac.md
