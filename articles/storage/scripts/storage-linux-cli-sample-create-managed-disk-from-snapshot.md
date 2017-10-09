---
title: "aaaAzure przykładowym skrypcie interfejsu wiersza polecenia — Tworzenie dysku zarządzanego z migawki | Dokumentacja firmy Microsoft"
description: "Azure CLI skrypt przykładowy — tworzenie dysków zarządzanych z migawki"
services: virtual-machines-linux
documentationcenter: storage
author: ramankumarlive
manager: kavithag
editor: tysonn
tags: azure-service-management
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 05/19/2017
ms.author: ramankum
ms.openlocfilehash: f92059353bfb739cff05213a9d206bfde2829a98
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-managed-disk-from-a-snapshot-with-cli"></a>Tworzenie dysku zarządzanego z migawki z interfejsu wiersza polecenia

Ten skrypt tworzy dysków zarządzanych z migawki. Użyj toorestore maszynę wirtualną z migawek systemu operacyjnego i dysków z danymi. Utwórz systemu operacyjnego i danych zarządzanych dysków z odpowiednich migawki, a następnie utwórz nową maszynę wirtualną dołączając dysków zarządzanych. Można także przywrócić dysków z danymi z istniejącej maszyny Wirtualnej, dołączając dyski danych utworzone na podstawie migawki.


[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a>Przykładowy skrypt

[!code-azurecli[main](../../../cli_scripts/storage/create-managed-disks-from-snapshot/create-managed-disks-from-snapshot.sh "Create managed disk from snapshot")]


## <a name="script-explanation"></a>Wyjaśnienie skryptu

Ten skrypt używa następujących poleceń toocreate dysków zarządzanych z migawki. Każde polecenie w tabeli hello łączy toocommand szczegółowej dokumentacji.

| Polecenie | Uwagi |
|---|---|
| [Pokaż migawki az](https://docs.microsoft.com/cli/azure/snapshot#show) | Pobiera wszystkie właściwości hello migawki za pomocą hello nazwy i właściwości grupy zasobów hello migawki. Identyfikator właściwości jest używane toocreate dysków zarządzanych.  |
| [Tworzenie dysku az](https://docs.microsoft.com/cli/azure/disk#create) | Tworzy zarządzanego przy użyciu dysku migawki identyfikator migawki zarządzanych |

## <a name="next-steps"></a>Następne kroki

[Utwórz maszynę wirtualną, dołączając dysków zarządzanych jako dysk systemu operacyjnego](./../../virtual-machines/scripts/virtual-machines-linux-cli-sample-create-vm-from-managed-os-disks.md?toc=%2fcli%2fmodule%2ftoc.json)

Aby uzyskać więcej informacji na powitania wiersza polecenia platformy Azure, zobacz [dokumentacji interfejsu wiersza polecenia Azure](https://docs.microsoft.com/cli/azure/overview).

Dodatkowe maszyny wirtualnej i dysków zarządzanych przykłady skryptów interfejsu wiersza polecenia można znaleźć w hello [dokumentacji maszyny Wirtualnej systemu Linux Azure](../../virtual-machines/linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).
