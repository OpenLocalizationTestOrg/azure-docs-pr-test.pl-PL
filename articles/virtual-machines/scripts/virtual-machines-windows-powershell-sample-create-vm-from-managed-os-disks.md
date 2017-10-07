---
title: "aaaAzure przykładowy skrypt programu PowerShell — Utwórz maszynę Wirtualną, dołączając dysków zarządzanych jako dysk systemu operacyjnego | Dokumentacja firmy Microsoft"
description: "Skrypt programu PowerShell Azure przykładowe — Utwórz maszynę Wirtualną, dołączając dysków zarządzanych jako dysk systemu operacyjnego"
services: virtual-machines-windows
documentationcenter: virtual-machines
author: ramankum
manager: kavithag
editor: ramankum
tags: azure-service-management
ms.assetid: 
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: sample
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 05/10/2017
ms.author: ramankum
ms.custom: mvc
ms.openlocfilehash: 8ae5b14df3977a4af91b92692cb925199cfb8058
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-virtual-machine-using-an-existing-managed-os-disk-with-powershell"></a>Utwórz maszynę wirtualną przy użyciu istniejącego dysku systemu operacyjnego zarządzane przy użyciu programu PowerShell

Ten skrypt tworzy maszynę wirtualną, dołączając istniejący dysk zarządzane jako dysk systemu operacyjnego. Użyj tego skryptu w poprzednich scenariuszach:
* Tworzenie maszyny Wirtualnej z istniejącego zarządzanych dysk systemu operacyjnego, który został skopiowany z dysków zarządzanych w innej subskrypcji
* Tworzenie maszyny Wirtualnej z istniejącego dysku zarządzanego utworzony na podstawie specjalne pliku wirtualnego dysku twardego 
* Tworzenie maszyny Wirtualnej z istniejącego zarządzanych dysk systemu operacyjnego, który został utworzony na podstawie migawki 

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install-no-ssh.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a>Przykładowy skrypt

[!code-powershell[main](../../../powershell_scripts/virtual-machine/create-vm-from-snapshot/create-vm-from-snapshot.ps1 "Create VM from snapshot")]

## <a name="clean-up-deployment"></a>Czyszczenie wdrożenia 

Hello uruchom następujące polecenie, grupy zasobów hello tooremove, maszyny Wirtualnej i wszystkich powiązanych zasobów.

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup
```

## <a name="script-explanation"></a>Wyjaśnienie skryptu

Ten skrypt używa hello następujące właściwości dysku tooget zarządzane poleceń, Dołącz tooa dysków zarządzanych w nowej maszyny Wirtualnej i tworzenie maszyny Wirtualnej. Każdy element w tabeli hello łączy toocommand szczegółowej dokumentacji.

| Polecenie | Uwagi |
|---|---|
| [Get-AzureRmDisk](/powershell/module/azurerm.compute/Get-AzureRmDisk) | Pobiera obiekt na podstawie nazwy hello i grupy zasobów hello dysku. Identyfikator właściwości hello zwrócony obiekt tooa dysku hello tooattach używane nowej maszyny Wirtualnej |
| [Nowe AzureRmVMConfig](/powershell/module/azurerm.compute/new-azurermvmconfig) | Tworzy konfiguracji maszyny Wirtualnej. Ta konfiguracja zawiera informacje, takie jak nazwa maszyny Wirtualnej, system operacyjny i poświadczenia administracyjne. Konfiguracja Hello jest używany podczas tworzenia maszyny Wirtualnej. |
| [Zestaw AzureRmVMOSDisk](/powershell/module/azurerm.compute/set-azurermvmosdisk) | Dołącza dysk zarządzane przy użyciu właściwości identyfikatora hello hello dysku jako systemu operacyjnego dysku tooa nowej maszyny wirtualnej |
| [Nowe AzureRmPublicIpAddress](/powershell/module/azurerm.network/new-azurermpublicipaddress) | Tworzy publiczny adres IP. |
| [Nowe AzureRmNetworkInterface](/powershell/module/azurerm.network/new-azurermnetworkinterface) | Tworzy interfejs sieciowy. |
| [Nowe AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm) | Utwórz maszynę wirtualną. |
|[Remove-AzureRmResourceGroup](/powershell/module/azurerm.resources/remove-azurermresourcegroup) | Usuwa grupę zasobów i wszystkie zasoby zawarte w ciągu. |

## <a name="next-steps"></a>Następne kroki

Aby uzyskać więcej informacji na powitania modułu Azure PowerShell, zobacz [dokumentacji programu Azure PowerShell](/powershell/azure/overview).

Przykłady skryptów PowerShell dodatkowe maszyny wirtualnej znajdują się w hello [dokumentacji maszyny Wirtualnej systemu Windows Azure](../windows/powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).
