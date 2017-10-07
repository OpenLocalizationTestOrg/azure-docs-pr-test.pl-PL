---
title: "aaaAzure przykładowym skrypcie programu PowerShell - migawki eksportu/kopiowania co konto magazynu tooa wirtualnego dysku twardego w innym regionie | Dokumentacja firmy Microsoft"
description: "Przykładowy skrypt programu PowerShell Azure - migawki eksportu/kopiowania co konto magazynu tooa wirtualnego dysku twardego w tym samym regionie innym"
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
ms.openlocfilehash: c18ad4fa0bf12033fafe941a807e7b4c8d233a30
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="exportcopy-managed-snapshots-as-vhd-tooa-storage-account-in-different-region-with-powershell"></a>Eksport/kopiowania zarządzane migawki co konto magazynu tooa wirtualnego dysku twardego w innym regionie przy użyciu programu PowerShell

Ten skrypt eksportuje migawki zarządzanego konta magazynu tooa w innym regionie. Najpierw generuje hello identyfikatora URI połączenia SAS hello migawki, a następnie używa go po toocopy go tooa konta magazynu w innym regionie. Użyj tej kopii zapasowej toomaintain skryptu dysków zarządzanych w innym regionie odzyskiwania po awarii.  

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a>Przykładowy skrypt

[!code-powershell[main](../../../powershell_scripts/virtual-machine/copy-snapshot-to-storage-account/copy-snapshot-to-storage-account.ps1 "Copy snapshot")]


## <a name="script-explanation"></a>Wyjaśnienie skryptu

Ten skrypt używa następujących poleceń toogenerate identyfikator URI sygnatury dostępu Współdzielonego dla zarządzanych hello migawki i kopii migawki tooa konto magazynu przy użyciu identyfikatora URI połączenia SAS. Każde polecenie w tabeli hello łączy toocommand szczegółowej dokumentacji.

| Polecenie | Uwagi |
|---|---|
| [Udziel AzureRmSnapshotAccess](/powershell/module/azurerm.compute/New-AzureRmDisk) | Generuje identyfikator URI sygnatury dostępu Współdzielonego dla migawki, która jest używana toocopy on tooa konta magazynu. |
| [Nowe AzureStorageContext](/powershell/module/azure.storage/New-AzureStorageContext) | Tworzy kontekst konta magazynu przy użyciu hello nazwę konta i klucz. Tego kontekstu może być używane tooperform operacji odczytu/zapisu na powitania konta magazynu. |
| [Start AzureStorageBlobCopy](/powershell/module/azure.storage/Start-AzureStorageBlobCopy) | Kopie hello podstawowy dysk VHD konta magazynu tooa migawki |

## <a name="next-steps"></a>Następne kroki

[Tworzenie dysku zarządzanego z wirtualnego dysku twardego](virtual-machines-windows-powershell-sample-create-managed-disk-from-vhd.md?toc=%2fpowershell%2fmodule%2ftoc.json)

[Utwórz maszynę wirtualną z dyskiem zarządzanym](./virtual-machines-windows-powershell-sample-create-vm-from-managed-os-disks.md?toc=%2fpowershell%2fmodule%2ftoc.json)

Aby uzyskać więcej informacji na powitania modułu Azure PowerShell, zobacz [dokumentacji programu Azure PowerShell](/powershell/azure/overview).

Przykłady skryptów PowerShell dodatkowe maszyny wirtualnej znajdują się w hello [dokumentacji maszyny Wirtualnej systemu Windows Azure](../../app-service-web/app-service-powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).
