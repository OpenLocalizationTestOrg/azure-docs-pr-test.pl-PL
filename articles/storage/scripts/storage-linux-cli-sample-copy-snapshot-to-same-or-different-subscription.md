---
title: "Azure CLI przykładowym skrypcie - migawki kopiowania (przenoszenia) dysków zarządzanych do tych samych lub różnych subskrypcji z interfejsu wiersza polecenia | Dokumentacja firmy Microsoft"
description: "Azure CLI przykładowym skrypcie - migawki kopiowania (przenoszenia) dysków zarządzanych do tych samych lub różnych subskrypcji z interfejsu wiersza polecenia"
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
ms.openlocfilehash: 0127e342bd0c3afbe9de775399f5510814bff499
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="copy-snapshot-of-a-managed-disk-to-same-or-different-subscription-with-cli"></a>Kopiowanie migawek dysków zarządzanych do tych samych lub różnych subskrypcji z interfejsu wiersza polecenia

Ten skrypt powoduje skopiowanie migawki dysków zarządzanych tych samych lub różnych subskrypcji. Użyj tego skryptu można przenieść do innej subskrypcji w tym samym regionie co migawki nadrzędnego migawki.


[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a>Przykładowy skrypt

[!code-azurecli[główne](../../../cli_scripts/storage/copy-snapshot-to-same-or-different-subscription/copy-snapshot-to-same-or-different-subscription.sh "migawki kopiowania")]


## <a name="script-explanation"></a>Wyjaśnienie skryptu

Ten skrypt używa następujących poleceń do tworzenia migawek w subskrypcji docelowej przy użyciu identyfikatora migawki źródła. Każde polecenie w tabeli łącza do dokumentacji określonego polecenia.

| Polecenie | Uwagi |
|---|---|
| [Pokaż migawki az](https://docs.microsoft.com/cli/azure/snapshot#show) | Pobiera właściwości migawki przy użyciu nazwy i właściwości grupy zasobów migawki. Identyfikator jest używana do skopiowania migawki do innej subskrypcji.  |
| [Tworzenie migawki az](https://docs.microsoft.com/cli/azure/snapshot#create) | Kopiuje migawki przez tworzenie migawek w innej subskrypcji przy użyciu identyfikatora i nazwy migawki nadrzędnej.  |

## <a name="next-steps"></a>Następne kroki

[Utwórz maszynę wirtualną z migawki](./../../virtual-machines/scripts/virtual-machines-linux-cli-sample-create-vm-from-snapshot.md?toc=%2fpowershell%2fmodule%2ftoc.json)

Aby uzyskać więcej informacji dotyczących interfejsu wiersza polecenia Azure, zobacz [dokumentacji interfejsu wiersza polecenia Azure](https://docs.microsoft.com/cli/azure/overview).

Dodatkowe maszyny wirtualnej i dysków zarządzanych przykłady skryptów interfejsu wiersza polecenia można znaleźć w [dokumentacji maszyny Wirtualnej systemu Linux Azure](../../virtual-machines/linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).
