---
title: "Connect Raspberry pi (C) tooAzure IoT — Lekcja 2: narzędzi platformy Azure (Ubuntu) | Dokumentacja firmy Microsoft"
description: "Zainstaluj środowisko Python i interfejsu wiersza polecenia platformy Azure (Azure CLI) na Ubuntu."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "iot chmury usługi azure cli"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-raspberry-pi-kit-c-get-started
ms.assetid: a03512f2-fabe-40c5-8505-b93eef8e5bec
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 1af4848f9fe0508e362c15b36eec8a35aea9ac5b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="get-azure-tools-ubuntu-1604"></a>Pobierz narzędzia Azure (Ubuntu 16.04)
> [!div class="op_single_selector"]
> * [System Windows 7 lub nowszy](iot-hub-raspberry-pi-kit-c-lesson2-get-azure-tools-win32.md)
> * [Ubuntu 16.04](iot-hub-raspberry-pi-kit-c-lesson2-get-azure-tools-ubuntu.md)
> * [System macOS 10.10](iot-hub-raspberry-pi-kit-c-lesson2-get-azure-tools-mac.md)

## <a name="what-you-will-do"></a>Będzie wykonywać
Zainstaluj hello interfejsu wiersza polecenia platformy Azure (Azure CLI). Jeśli masz problemy, poszukaj rozwiązania na powitania [Rozwiązywanie problemów z strony](iot-hub-raspberry-pi-kit-c-troubleshooting.md).

## <a name="what-you-will-learn"></a>Co dowiesz się
W tym artykule dowiesz się:
* Jak tooinstall hello wiersza polecenia platformy Azure.
* Jak tooadd podgrupę IoT hello wiersza polecenia platformy Azure.

## <a name="what-you-need"></a>Co jest potrzebne
* Ubuntu komputera z połączeniem internetowym.
* Aktywna subskrypcja platformy Azure. Jeśli nie masz konta, możesz utworzyć [bezpłatnego konta wersji próbnej](http://azure.microsoft.com/pricing/free-trial/) za kilka minut.

## <a name="install-hello-azure-cli"></a>Zainstaluj hello wiersza polecenia platformy Azure
Hello interfejsu wiersza polecenia Azure zapewnia wiele platform wiersza polecenia platformy Azure, umożliwiając toowork bezpośrednio z tooprovision z wiersza polecenia i zarządzanie zasobami.

tooinstall hello najnowsze wiersza polecenia platformy Azure, wykonaj następujące kroki:

1. Uruchom następujące polecenia w oknie terminalu hello. Może upłynąć hello tooinstall pięć minut wiersza polecenia platformy Azure.

   ```bash
   sudo apt-get update
   sudo apt-get install -y libssl-dev libffi-dev
   sudo apt-get install -y python-dev
   sudo apt-get install -y build-essential
   sudo apt-get install -y python-pip
   sudo pip install --upgrade azure-cli
   sudo pip install --upgrade azure-cli-iot
   ```
2. Sprawdź hello instalacji, uruchamiając następujące polecenie hello:

   ```bash
   az iot -h
   ```

Powinien pojawić się następujące hello output, jeśli hello Instalacja powiodła się.

![Dane wyjściowe, co oznacza Powodzenie](media/iot-hub-raspberry-pi-lessons/lesson2/az_iot_help_ubuntu.png)

## <a name="summary"></a>Podsumowanie
Po zainstalowaniu hello wiersza polecenia platformy Azure. Następnym zadaniem jest toocreate Centrum Azure IoT i urządzeniami przy użyciu tożsamości hello wiersza polecenia platformy Azure.

## <a name="next-steps"></a>Następne kroki
[Utworzenie Centrum IoT i zarejestruj malina Pi 3](iot-hub-raspberry-pi-kit-c-lesson2-prepare-azure-iot-hub.md)

