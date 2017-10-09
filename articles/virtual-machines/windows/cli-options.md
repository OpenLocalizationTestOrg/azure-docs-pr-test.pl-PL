---
title: Witaj aaaUsing wiersza polecenia platformy Azure w systemie Windows | Dokumentacja firmy Microsoft
description: "Przy użyciu interfejsu wiersza polecenia Azure hello w systemie Windows"
services: virtual-machines-windows
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: 
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 02/14/2017
ms.author: nepeters
ms.openlocfilehash: edca4a2701a7dfc0fc54df5649e8a5e7afc95490
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="using-hello-azure-cli-on-windows"></a>Przy użyciu interfejsu wiersza polecenia Azure hello w systemie Windows

Hello Azure interfejsu wiersza polecenia (CLI) oferuje wiersza polecenia i skryptów środowiska do tworzenia i zarządzania zasobami platformy Azure. Hello wiersza polecenia platformy Azure jest dostępna dla macOS, Linux i systemów operacyjnych Windows. W tych systemach operacyjnych hello polecenia interfejsu wiersza polecenia są identyczne, jednak może się różnić składni skryptów systemu operacyjnego.

Tej metody hello szczegóły dokumentu hello wiersza polecenia platformy Azure można zainstalować i uruchomić na zagadnienia syntaktycznych systemu Windows i szczegóły dla każdego. Aby uzyskać szczegółowe interfejsu wiersza polecenia Azure dokumentacji, zobacz [dokumentacji interfejsu wiersza polecenia Azure]( https://docs.microsoft.com/en-us/cli/azure/overview).

## <a name="windows-subsystem-for-linux"></a>Podsystem systemu Windows dla systemu Linux

Witaj podsystemu systemu Windows dla systemu Linux (WSL) udostępnia środowisko Ubuntu Linux na system Windows 10 Anniversary i późniejszych wersjach. Po włączeniu WSL zapewnia natywnym środowiskiem Bash, która może służyć do tworzenia i uruchamiania skryptów wiersza polecenia platformy Azure. Ponieważ WSL zapewnia natywnym środowiskiem Bash, skryptów wiersza polecenia platformy Azure może być współużytkowana macOS, Linux i Windows bez żadnych modyfikacji.

Witaj toouse wiersza polecenia platformy Azure w WSL, wykonaj następujące czynności hello.

|Zadanie | Instrukcje |
|---|---|
| Włącz WSL | [Zainstaluj WSL dokumentacji](https://msdn.microsoft.com/en-us/commandline/wsl/install_guide) |
| Zainstaluj hello wiersza polecenia platformy Azure |[Zainstaluj na WSL/Ubuntu 14.04 hello interfejsu wiersza polecenia](https://docs.microsoft.com/en-us/cli/azure/install-az-cli2#ubuntu)|

## <a name="powershell"></a>PowerShell

Witaj wiersza polecenia platformy Azure może działać natywnie w systemie Windows. W tej konfiguracji hello Azure CLI pakiet jest zainstalowany w systemie operacyjnym Windows hello, a polecenia można uruchomić z programu PowerShell. W tej konfiguracji interfejsu wiersza polecenia Azure poleceń i skryptów może działać w dowolnej obsługiwanej wersji systemu Windows, jednak platforma składni skryptów jest wymagane. W związku z tym skrypty nie zawsze mogą współużytkować system macOS, Linux i Windows bez żadnych modyfikacji.

Witaj toouse wiersza polecenia platformy Azure w systemie Windows, zainstaluj pakiet hello za pomocą tych instrukcji [hello instalowanie interfejsu wiersza polecenia w systemie Windows](https://docs.microsoft.com/en-us/cli/azure/install-az-cli2#windows).

## <a name="docker-image"></a>Obraz docker

Korzystając z Docker dla systemu Windows, obrazu Docker można uruchomić zawierającą hello wiersza polecenia platformy Azure. Ten obraz jest oparte na systemie Linux i zawiera natywnym środowiskiem Bash.  Korzystając z Docker dla systemu Windows i hello Azure CLI obrazu, toobe skrypty współużytkowane przez system macOS, Linux i Windows. 

toouse hello Azure CLI na Docker dla systemu Windows, upewnij się, że Docker dla systemu Windows działa i uruchom następujące polecenie hello.

```bash
docker run -it azuresdk/azure-cli-python:latest bash
```

Po ukończeniu Bash, czyli rozpoczęcia sesji wstępnie ładowane hello narzędzia wiersza polecenia platformy Azure.

## <a name="next-steps"></a>Następne kroki

[Przykładowy interfejs wiersza polecenia dla maszyn wirtualnych platformy Azure](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

[Przykłady interfejsu wiersza polecenia dla aplikacji sieci Web Azure](../../app-service-web/app-service-cli-samples.md)

[Przykłady interfejsu wiersza polecenia dla bazy danych SQL Azure](../../sql-database/sql-database-cli-samples.md)
