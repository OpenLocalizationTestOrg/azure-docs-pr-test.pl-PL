---
title: "aaaAzure przykładowym skrypcie interfejsu wiersza polecenia - migawki kopiowania (przenoszenia) toosame dysków zarządzanych lub innej subskrypcji z interfejsu wiersza polecenia | Dokumentacja firmy Microsoft"
description: "Azure CLI przykładowym skrypcie - migawki kopiowania (przenoszenia) toosame dysków zarządzanych lub innej subskrypcji z interfejsu wiersza polecenia"
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
ms.openlocfilehash: 4a21fd2435181a033b563100888aba0c5834496d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="copy-snapshot-of-a-managed-disk-toosame-or-different-subscription-with-cli"></a>Kopiowanie migawek dysków zarządzanych w toosame lub innej subskrypcji z interfejsu wiersza polecenia

Ten skrypt kopiuje migawki dysków zarządzanych w toosame lub innej subskrypcji. Użyj tego skryptu toomove subskrypcji toodifferent migawki w hello tego samego regionu hello nadrzędnego migawki.


[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a>Przykładowy skrypt

[!code-azurecli[main](../../../cli_scripts/storage/copy-snapshot-to-same-or-different-subscription/copy-snapshot-to-same-or-different-subscription.sh "Copy snapshot")]


## <a name="script-explanation"></a>Wyjaśnienie skryptu

Ten skrypt używa następujących poleceń toocreate migawki za pomocą subskrypcji docelowej hello hello identyfikator hello źródła migawki. Każde polecenie w tabeli hello łączy toocommand szczegółowej dokumentacji.

| Polecenie | Uwagi |
|---|---|
| [Pokaż migawki az](https://docs.microsoft.com/cli/azure/snapshot#show) | Pobiera wszystkie właściwości hello migawki za pomocą hello nazwy i właściwości grupy zasobów hello migawki. Identyfikator właściwości jest używane toocopy hello migawki toodifferent subskrypcji.  |
| [Tworzenie migawki az](https://docs.microsoft.com/cli/azure/snapshot#create) | Kopie migawki przez tworzenie migawek w innej subskrypcji przy użyciu hello identyfikator i nazwa hello nadrzędnego migawki.  |

## <a name="next-steps"></a>Następne kroki

[Utwórz maszynę wirtualną z migawki](./../../virtual-machines/scripts/virtual-machines-linux-cli-sample-create-vm-from-snapshot.md?toc=%2fpowershell%2fmodule%2ftoc.json)

Aby uzyskać więcej informacji na powitania wiersza polecenia platformy Azure, zobacz [dokumentacji interfejsu wiersza polecenia Azure](https://docs.microsoft.com/cli/azure/overview).

Dodatkowe maszyny wirtualnej i dysków zarządzanych przykłady skryptów interfejsu wiersza polecenia można znaleźć w hello [dokumentacji maszyny Wirtualnej systemu Linux Azure](../../virtual-machines/linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).
