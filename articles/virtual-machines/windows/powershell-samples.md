---
title: "Przykłady środowiska PowerShell maszyny wirtualnej aaaAzure | Dokumentacja firmy Microsoft"
description: "Przykłady środowiska PowerShell maszyny wirtualnej platformy Azure"
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
ms.date: 05/05/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: 89fd26aa979687cdcdf9ae4e60be7d0d2eaeae91
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-virtual-machine-powershell-samples"></a>Przykładów dla platformy Azure PowerShell maszyny wirtualnej

Witaj poniższej tabeli przedstawiono przykłady skryptów tooPowerShell łącza, które tworzenia i zarządzania maszynami wirtualnymi systemu Windows.

| | |
|---|---|
|**Tworzenie maszyn wirtualnych**||
| [Utwórz maszynę wirtualną w pełni skonfigurowany](./../scripts/virtual-machines-windows-powershell-sample-create-vm.md?toc=%2fpowershell%2fmodule%2ftoc.json) | Tworzy grupę zasobów, maszyny wirtualnej i wszystkie powiązane zasoby.|
| [Tworzenie maszyn wirtualnych o wysokiej dostępności](./../scripts/virtual-machines-windows-powershell-sample-create-nlb-vm.md?toc=%2fpowershell%2fmodule%2ftoc.json) | Tworzy kilka maszyny wirtualne o wysokiej dostępności i konfiguracji równoważenia obciążenia.|
| [Tworzenie maszyny Wirtualnej, a następnie uruchom skrypt konfiguracji](./../scripts/virtual-machines-windows-powershell-sample-create-vm-iis.md?toc=%2fpowershell%2fmodule%2ftoc.json) | Tworzy maszynę wirtualną i używa hello Azure niestandardowego skryptu rozszerzenia tooinstall usług IIS. |
| [Utwórz maszynę Wirtualną i uruchomić konfiguracji DSC](./../scripts/virtual-machines-windows-powershell-sample-create-iis-using-dsc.md?toc=%2fpowershell%2fmodule%2ftoc.json) | Tworzy maszynę wirtualną i używa hello konfiguracji żądanego stanu Azure (DSC) rozszerzenia tooinstall usług IIS. |
| [Przekazywanie wirtualnego dysku twardego i tworzyć maszyny wirtualne](./../scripts/virtual-machines-windows-powershell-upload-generalized-script.md) | Uplaods lokalnego pliku VHD pliku tooAzure, tworzy obraz z hello wirtualnego dysku twardego i następnie tworzy Maszynę wirtualną z tego obrazu. |
| [Utwórz maszynę Wirtualną z dyskiem zarządzanym systemu operacyjnego](./../scripts/virtual-machines-windows-powershell-sample-create-vm-from-managed-os-disks.md?toc=%2fpowershell%2fmodule%2ftoc.json) | Tworzy maszynę wirtualną, dołączając istniejący dysk zarządzane jako dysk systemu operacyjnego. |
| [Tworzenie maszyny Wirtualnej z migawki](./../scripts/virtual-machines-windows-powershell-sample-create-vm-from-snapshot.md?toc=%2fpowershell%2fmodule%2ftoc.json) | Tworzy maszynę wirtualną z migawki, najpierw tworząc dysków zarządzanych z migawki, a następnie Trwa dołączanie nowego dysku zarządzanego hello jako dysk systemu operacyjnego. |
|**Zarządzanie magazynem**||
| [Tworzenie dysków zarządzanych z dysku VHD w tych samych lub różnych subskrypcji.](../scripts/virtual-machines-windows-powershell-sample-create-managed-disk-from-vhd.md?toc=%2fpowershell%2fmodule%2ftoc.json) | Tworzy dysków zarządzanych z specjalne wirtualny dysk twardy jako dysk systemu operacyjnego lub dane wirtualnego dysku twardego jako dysk danych w tych samych lub różnych subskrypcji.  |
| [Tworzenie dysku zarządzanego z migawki](../scripts/virtual-machines-windows-powershell-sample-create-managed-disk-from-snapshot.md?toc=%2fpowershell%2fmodule%2ftoc.json) | Tworzy dysków zarządzanych z migawki. |
| [Kopiowanie dysków zarządzanych w toosame lub innej subskrypcji](../scripts/virtual-machines-windows-powershell-sample-copy-managed-disks-to-same-or-different-subscription.md?toc=%2fcli%2fmodule%2ftoc.json) | Zarządzane kopii dysku toosame lub innej subskrypcji, ale w hello sam region jako element nadrzędny hello zarządzane dysku. 
| [Eksportowanie migawki co konto magazynu tooa wirtualnego dysku twardego](../scripts/virtual-machines-windows-powershell-sample-copy-snapshot-to-storage-account.md?toc=%2fpowershell%2fmodule%2ftoc.json) | Eksportuje zarządzanych migawki co konto magazynu tooa wirtualnego dysku twardego w innym regionie. |
| [Utwórz migawkę z wirtualnego dysku twardego](../scripts/virtual-machines-windows-powershell-sample-create-snapshot-from-vhd.md?toc=%2fpowershell%2fmodule%2ftoc.json) | Tworzy migawki z toocreate wirtualnego dysku twardego z migawki wiele takich samych dysków zarządzanych w krótkim czasie.  |
| [Kopiowanie migawek toosame lub innej subskrypcji](../scripts/virtual-machines-windows-powershell-sample-copy-snapshot-to-same-or-different-subscription.md?toc=%2fpowershell%2fmodule%2ftoc.json) | Kopie migawki toosame lub innej subskrypcji, ale w hello sam region jako hello nadrzędnego migawki. |
|**Bezpieczne maszyny wirtualne**||
| [Szyfrowanie dysków maszyny Wirtualnej i danych](./../scripts/virtual-machines-windows-powershell-sample-encrypt-vm.md?toc=%2fpowershell%2fazure%2ftoc.json) | Tworzy usługi Azure Key Vault, klucz szyfrowania i nazwy głównej usługi, a następnie szyfruje maszyny Wirtualnej. |
|**Monitorowanie maszyn wirtualnych**||
| [Monitor maszyny Wirtualnej w usłudze Operations Management Suite](./../scripts/virtual-machines-windows-powershell-sample-create-vm-oms.md?toc=%2fpowershell%2fmodule%2ftoc.json) | Tworzy maszynę wirtualną, instaluje agenta Operations Management Suite hello i rejestruje hello maszyny Wirtualnej w obszarze roboczym pakietu OMS.  |
| | |

