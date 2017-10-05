---
title: "Nawiązać Pi malina (węzeł) Azure IoT — Lekcja 2: Pobierz narzędzia (Ubuntu) | Dokumentacja firmy Microsoft"
description: "Zainstaluj środowisko Python i interfejsu wiersza polecenia platformy Azure (Azure CLI) na Ubuntu."
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: "iot chmury usługi azure cli"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-raspberry-pi-kit-node-get-started
ms.assetid: 2f98923a-5274-4220-87d4-77ac8beb4d0f
ms.service: iot-hub
ms.devlang: node
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 3933ccea992c62da1dd402f651d5b5b4ad43713d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="get-azure-tools-ubuntu-1604"></a>Pobierz narzędzia Azure (Ubuntu 16.04)
> [!div class="op_single_selector"]
> * [System Windows 7 lub nowszy](iot-hub-raspberry-pi-kit-node-lesson2-get-azure-tools-win32.md)
> * [Ubuntu 16.04](iot-hub-raspberry-pi-kit-node-lesson2-get-azure-tools-ubuntu.md)
> * [System macOS 10.10](iot-hub-raspberry-pi-kit-node-lesson2-get-azure-tools-mac.md)

## <a name="what-you-will-do"></a>Będzie wykonywać
Zainstaluj interfejs wiersza polecenia platformy Azure (Azure CLI). Jeśli masz problemy, poszukaj rozwiązania [Rozwiązywanie problemów z strony](iot-hub-raspberry-pi-kit-node-troubleshooting.md).

## <a name="what-you-will-learn"></a>Co dowiesz się
W tym artykule dowiesz się:
* Jak zainstalować wiersza polecenia platformy Azure.
* Jak dodać podgrupę IoT wiersza polecenia platformy Azure.

## <a name="what-you-need"></a>Co jest potrzebne
* Ubuntu komputera z połączeniem internetowym.
* Aktywna subskrypcja platformy Azure. Jeśli nie masz konta, możesz utworzyć [bezpłatnego konta wersji próbnej](http://azure.microsoft.com/pricing/free-trial/) za kilka minut.

## <a name="install-the-azure-cli"></a>Zainstaluj interfejs wiersza polecenia platformy Azure
Interfejsu wiersza polecenia Azure zapewnia wiele platform wiersza polecenia platformy Azure, dzięki któremu można pracować bezpośrednio z wiersza polecenia do udostępniania zasobów i zarządzanie nimi.

Aby zainstalować najnowsze wiersza polecenia platformy Azure, wykonaj następujące kroki:

1. Uruchom następujące polecenia w oknie terminalu. Może upłynąć pięć minut na zainstalowanie wiersza polecenia platformy Azure.

   ```bash
   sudo apt-get update
   sudo apt-get install -y libssl-dev libffi-dev
   sudo apt-get install -y python-dev
   sudo apt-get install -y build-essential
   sudo apt-get install -y python-pip
   sudo pip install --upgrade azure-cli
   sudo pip install --upgrade azure-cli-iot
   ```
2. Instalację można zweryfikować, uruchamiając następujące polecenie:

   ```bash
   az iot -h
   ```

Następujące dane wyjściowe powinny być widoczne, jeśli instalacja zakończy się pomyślnie.

![Dane wyjściowe, co oznacza Powodzenie](media/iot-hub-raspberry-pi-lessons/lesson2/az_iot_help_ubuntu.png)

## <a name="summary"></a>Podsumowanie
Po zainstalowaniu interfejsu wiersza polecenia Azure. Następnym zadaniem będzie można utworzyć tożsamości koncentratora i urządzenia Azure IoT przy użyciu wiersza polecenia platformy Azure.

## <a name="next-steps"></a>Następne kroki
[Utworzenie Centrum IoT i zarejestruj malina Pi 3](iot-hub-raspberry-pi-kit-node-lesson2-prepare-azure-iot-hub.md)

