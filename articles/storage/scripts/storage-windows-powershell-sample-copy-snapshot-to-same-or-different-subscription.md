---
title: "Przykładowy skrypt programu PowerShell — migawki kopiowania (przenoszenia) toosame dysków zarządzanych lub innej subskrypcji aaaAzure | Dokumentacja firmy Microsoft"
description: "Przykładowy skrypt programu PowerShell Azure - migawki kopiowania (przenoszenia) toosame dysków zarządzanych lub innej subskrypcji"
services: virtual-machines-windows
documentationcenter: storage
author: ramankumarlive
manager: kavithag
editor: tysonn
tags: azure-service-management
ms.assetid: 
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: sample
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 06/06/2017
ms.author: ramankum
ms.openlocfilehash: 7a3565356f13cb93759dec7ef9d0357e04c3410b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="copy-snapshot-of-a-managed-disk-in-same-subscription-or-different-subscription-with-powershell"></a>Kopiowanie migawek dysków zarządzanych w tej samej subskrypcji lub różnych subskrypcji przy użyciu programu PowerShell

Ten skrypt tworzy kopię migawkę w hello tej samej subskrypcji tej samej lub innej subskrypcji. Użyj tego skryptu toomove subskrypcji toodifferent migawki dla przechowywania danych. Zapisywanie migawek w innej subskrypcji Chroń przed przypadkowym usunięciem migawek w ramach subskrypcji głównego. 

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a>Przykładowy skrypt

[!code-powershell[main](../../../powershell_scripts/storage/copy-snapshot-to-same-or-different-subscription/copy-snapshot-to-same-or-different-subscription.ps1 "Copy snapshot")]


## <a name="script-explanation"></a>Wyjaśnienie skryptu

Ten skrypt używa następujących poleceń toocreate migawki za pomocą subskrypcji docelowej hello hello identyfikator hello źródła migawki. Każde polecenie w tabeli hello łączy toocommand szczegółowej dokumentacji.

| Polecenie | Uwagi |
|---|---|
| [Nowe AzureRmSnapshotConfig](/powershell/module/azurerm.compute/New-AzureRmSnapshotConfig) | Tworzy konfigurację migawki, która służy do tworzenia migawek. Obejmuje on zasobów hello identyfikator migawki nadrzędnego hello i lokalizacji, która jest taka sama jak hello nadrzędnego migawki.  |
| [Nowe AzureRmSnapshot](/powershell/module/azurerm.compute/New-AzureRmDisk) | Tworzy migawkę przy użyciu konfiguracji migawki, nazwę migawki i przekazywane jako parametry nazwę grupy zasobów. |


## <a name="next-steps"></a>Następne kroki

[Utwórz maszynę wirtualną z migawki](./../../virtual-machines/scripts/virtual-machines-windows-powershell-sample-create-vm-from-snapshot.md?toc=%2fpowershell%2fmodule%2ftoc.json)

Aby uzyskać więcej informacji na powitania modułu Azure PowerShell, zobacz [dokumentacji programu Azure PowerShell](/powershell/azure/overview).

Przykłady skryptów PowerShell dodatkowe maszyny wirtualnej znajdują się w hello [dokumentacji maszyny Wirtualnej systemu Windows Azure](../../virtual-machines/windows/powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).
