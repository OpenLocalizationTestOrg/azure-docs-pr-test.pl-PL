---
title: "aaaAzure przykładowym skrypcie interfejsu wiersza polecenia - kopiowania (przenoszenia) zarządzane toosame dysków lub innej subskrypcji | Dokumentacja firmy Microsoft"
description: "Azure przykładowym skrypcie interfejsu wiersza polecenia - toosame dysków zarządzanych kopiowania (przenoszenia) lub innej subskrypcji"
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
ms.openlocfilehash: 8581169baa0fd0e0eec1c72eab77b657f48b1cfa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="copy-managed-disks-toosame-or-different-subscription-with-cli"></a>Kopiowanie dysków zarządzanych toosame lub innej subskrypcji z interfejsu wiersza polecenia

Ten skrypt kopiuje toosame dysków zarządzanych lub innej subskrypcji, ale w hello sam region. 


[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a>Przykładowy skrypt

[!code-azurecli[main](../../../cli_scripts/storage/copy-managed-disks-to-same-or-different-subscription/copy-managed-disks-to-same-or-different-subscription.sh "Copy managed disk")]


## <a name="script-explanation"></a>Wyjaśnienie skryptu

Ten skrypt używa następujących poleceń toocreate nowy dysk zarządzanych za pomocą subskrypcji docelowej hello hello identyfikator źródła hello zarządzane dysku. Każde polecenie w tabeli hello łączy toocommand szczegółowej dokumentacji.

| Polecenie | Uwagi |
|---|---|
| [Pokaż dysku az](https://docs.microsoft.com/cli/azure/disk#show) | Pobiera wszystkie właściwości hello dysków zarządzanych przy użyciu właściwości hello nazwy i zasobów grupy hello dysku zarządzanego. Identyfikator właściwości jest używane toocopy hello zarządzane dysku toodifferent subskrypcji.  |
| [Tworzenie dysku az](https://docs.microsoft.com/cli/azure/disk#create) | Kopiuje dysków zarządzanych przez utworzenie nowych dysków zarządzanych w innej subskrypcji przy użyciu identyfikatora i nazwy nadrzędnego hello zarządzane dysku.  |

## <a name="next-steps"></a>Następne kroki

[Utwórz maszynę wirtualną z dyskiem zarządzanym](./../../virtual-machines/scripts/virtual-machines-linux-cli-sample-create-vm-from-managed-os-disks.md?toc=%2fpowershell%2fmodule%2ftoc.json)

Aby uzyskać więcej informacji na powitania wiersza polecenia platformy Azure, zobacz [dokumentacji interfejsu wiersza polecenia Azure](https://docs.microsoft.com/cli/azure/overview).

Dodatkowe maszyny wirtualnej i dysków zarządzanych przykłady skryptów interfejsu wiersza polecenia można znaleźć w hello [dokumentacji maszyny Wirtualnej systemu Linux Azure](../../virtual-machines/linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).
