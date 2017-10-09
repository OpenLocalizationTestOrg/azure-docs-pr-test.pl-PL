---
title: "Przykładowy skrypt programu PowerShell - aaaAzure utworzenia migawki z toocreate wirtualnego dysku twardego wiele takich samych dysków zarządzanych w krótkim czasie | Dokumentacja firmy Microsoft"
description: "Skrypt programu PowerShell Azure przykładowe — Tworzenie migawki z toocreate wirtualnego dysku twardego wiele takich samych dysków zarządzanych w krótkim czasie"
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
ms.date: 06/05/2017
ms.author: ramankum
ms.openlocfilehash: 0a13e399b692f32b3772add39fe5b5c023808c5e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-snapshot-from-a-vhd-toocreate-multiple-identical-managed-disks-in-small-amount-of-time-with-powershell"></a>Utwórz migawkę z toocreate wirtualnego dysku twardego wiele takich samych dysków zarządzanych w krótkim czasie przy użyciu programu PowerShell

Ten skrypt tworzy migawkę z pliku VHD na koncie magazynu w tym samym lub różnych subskrypcji. Użyj tego skryptu tooimport specjalne migawki tooa wirtualnego dysku twardego (nie uogólniony/Sysprep) i użycia toocreate migawki hello wiele takich samych dysków zarządzanych w krótkim czasie. Należy także użyć go tooimport tooa migawki wirtualnego dysku twardego danych a następnie toocreate migawki hello wiele dysków zarządzanych w krótkim czasie. 

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a>Przykładowy skrypt

[!code-powershell[main](../../../powershell_scripts/storage/create-snapshots-from-vhd-in-different-subscription/create-snapshots-from-vhd-in-different-subscription.ps1 "Create snapshot from VHD")]


## <a name="script-explanation"></a>Wyjaśnienie skryptu

Ten skrypt używa następujących poleceń toocreate dysków zarządzanych z dysku VHD w innej subskrypcji. Każde polecenie w tabeli hello łączy toocommand szczegółowej dokumentacji.

| Polecenie | Uwagi |
|---|---|
| [Nowe AzureRmDiskConfig](/powershell/module/azurerm.compute/New-AzureRmDiskConfig) | Tworzy konfiguracji dysku, który jest używany do tworzenia dysku. Zawiera typ magazynu, lokalizacji, identyfikator konta magazynu hello przechowywania hello nadrzędnego dysku VHD zasobu i identyfikator URI dysku VHD hello elementu nadrzędnego dysku VHD. |
| [Nowe AzureRmDisk](/powershell/module/azurerm.compute/New-AzureRmDisk) | Tworzy dysk przy użyciu konfiguracji dysku, nazwa dysku i przekazywane jako parametry nazwę grupy zasobów. |

## <a name="next-steps"></a>Następne kroki

[Tworzenie dysku zarządzanego z migawki](./../../storage/scripts/storage-windows-powershell-sample-create-managed-disk-from-snapshot.md?toc=%2fpowershell%2fmodule%2ftoc.json)


[Utwórz maszynę wirtualną, dołączając dysków zarządzanych jako dysk systemu operacyjnego](./../../virtual-machines/scripts/virtual-machines-windows-powershell-sample-create-vm-from-managed-os-disks.md?toc=%2fpowershell%2fmodule%2ftoc.json)

Aby uzyskać więcej informacji na powitania modułu Azure PowerShell, zobacz [dokumentacji programu Azure PowerShell](/powershell/azure/overview).

Przykłady skryptów PowerShell dodatkowe maszyny wirtualnej znajdują się w hello [dokumentacji maszyny Wirtualnej systemu Windows Azure](../../virtual-machines/windows/powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).
