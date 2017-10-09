---
title: "aaaAzure przykładowy skrypt programu PowerShell — Tworzenie dysku zarządzanego z pliku VHD na koncie magazynu w tym samym lub różnych subskrypcji | Dokumentacja firmy Microsoft"
description: "Skrypt programu PowerShell Azure przykładowe — tworzenie dysków zarządzanych z pliku VHD na koncie magazynu w tym samym lub różnych subskrypcji."
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
ms.openlocfilehash: 93157823eb3b8cddba5e0af455d16bff1d42ce00
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-managed-disk-from-a-vhd-file-in-a-storage-account-in-same-or-different-subscription-with-powershell"></a>Tworzenie dysku zarządzanego z pliku VHD na koncie magazynu w tym samym lub różnych subskrypcji przy użyciu programu PowerShell

Ten skrypt tworzy dysków zarządzanych z pliku VHD na koncie magazynu w tym samym lub różnych subskrypcji. Użyj tego skryptu tooimport specjalne (nie uogólniony/Sysprep) wirtualnego dysku twardego toomanaged OS dysku toocreate maszyny wirtualnej. Należy także użyć go tooimport dysku danych toomanaged dane wirtualnego dysku twardego. 

Nie należy tworzyć wiele identycznych dysków zarządzanych z pliku VHD w krótkim czasie. toocreate zarządzane dysków z pliku vhd migawki obiektu blob hello pliku wirtualnego dysku twardego zostaje utworzony, a następnie jest używany toocreate zarządzanych dysków. W ciągu jednej minuty powodujące błędy tworzenia dysku można utworzyć migawki tylko jeden obiekt blob toothrottling ukończenia. tooavoid tego ograniczenia przepustowości, Utwórz [zarządzanych migawki z pliku vhd hello](./../scripts/storage-windows-powershell-sample-create-snapshot-from-vhd.md?toc=%2fpowershell%2fmodule%2ftoc.json) i następnie użyj hello zarządzane toocreate migawki wiele dysków zarządzanych w krótkim czasie. 

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a>Przykładowy skrypt

[!code-powershell[main](../../../powershell_scripts/storage/create-managed-disks-from-vhd-in-different-subscription/create-managed-disks-from-vhd-in-different-subscription.ps1 "Create managed disk from VHD")]


## <a name="script-explanation"></a>Wyjaśnienie skryptu

Ten skrypt używa następujących poleceń toocreate dysków zarządzanych z dysku VHD w innej subskrypcji. Każde polecenie w tabeli hello łączy toocommand szczegółowej dokumentacji.

| Polecenie | Uwagi |
|---|---|
| [Nowe AzureRmDiskConfig](/powershell/module/azurerm.compute/New-AzureRmDiskConfig) | Tworzy konfiguracji dysku, który jest używany do tworzenia dysku. Zawiera typ magazynu, lokalizacji, identyfikator hello konta magazynu przechowywania hello nadrzędnego dysku VHD, identyfikator URI dysku VHD hello elementu nadrzędnego dysku VHD zasobu. |
| [Nowe AzureRmDisk](/powershell/module/azurerm.compute/New-AzureRmDisk) | Tworzy dysk przy użyciu konfiguracji dysku, nazwa dysku i przekazywane jako parametry nazwę grupy zasobów. |

## <a name="next-steps"></a>Następne kroki

[Utwórz maszynę wirtualną, dołączając dysków zarządzanych jako dysk systemu operacyjnego](./../../virtual-machines/scripts/virtual-machines-windows-powershell-sample-create-vm-from-managed-os-disks.md?toc=%2fpowershell%2fmodule%2ftoc.json)

Aby uzyskać więcej informacji na powitania modułu Azure PowerShell, zobacz [dokumentacji programu Azure PowerShell](/powershell/azure/overview).

Przykłady skryptów PowerShell dodatkowe maszyny wirtualnej znajdują się w hello [dokumentacji maszyny Wirtualnej systemu Windows Azure](../../virtual-machines/windows/powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).
