---
title: "aaaConvert maszyny wirtualnej systemu Linux na platformie Azure z niezarządzanych dyski dysków toomanaged - dysków zarządzanych Azure | Dokumentacja firmy Microsoft"
description: "Jak dyski tooconvert Maszynę wirtualną systemu Linux z toomanaged niezarządzane dysków przy użyciu interfejsu wiersza polecenia Azure w wersji 2.0 w modelu wdrażania usługi Resource Manager hello"
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: azurecli
ms.topic: article
ms.date: 06/23/2017
ms.author: iainfou
ms.openlocfilehash: 1b94da11deab46f344e28ab4491cf220506b6347
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="convert-a-linux-virtual-machine-from-unmanaged-disks-toomanaged-disks"></a>Konwertuj maszyny wirtualnej systemu Linux z dysków toomanaged niezarządzane dysków

Jeśli masz istniejące maszyn wirtualnych systemu Linux (VM) korzystające z niezarządzanego dysków, można konwertować dyski toouse zarządzanych maszyn wirtualnych hello za pośrednictwem hello [dysków zarządzanych Azure](../windows/managed-disks-overview.md) usługi. Ten proces konwersji dyskach hello systemu operacyjnego i wszystkich dysków dołączonych danych.

W tym artykule opisano, jak tooconvert maszyn wirtualnych przy użyciu hello wiersza polecenia platformy Azure. Jeśli konieczne tooinstall lub uaktualnić go, zobacz [zainstalować Azure CLI 2.0](/cli/azure/install-azure-cli). 

## <a name="before-you-begin"></a>Przed rozpoczęciem

[!INCLUDE [virtual-machines-common-convert-disks-considerations](../../../includes/virtual-machines-common-convert-disks-considerations.md)]


## <a name="convert-single-instance-vms"></a>Konwertuj maszyn wirtualnych z jednego wystąpienia
W tej sekcji omówiono sposób tooconvert jednym wystąpieniu maszyny wirtualne platformy Azure z niezarządzanych dyski toomanaged dyski. (W przypadku maszyn wirtualnych w zestawie dostępności, zobacz następną sekcję hello). Można użyć tego procesu tooconvert hello maszyny wirtualne z dysków toopremium zarządzane dysków w warstwie premium (SSD) niezarządzanych lub standard (HDD) niezarządzanych dysków toostandard zarządzanych dysków.

1. Cofnięcie przydziału hello maszyny Wirtualnej za pomocą [deallocate wirtualna az](/cli/azure/vm#deallocate). Witaj poniższy przykład cofa alokację hello maszyny Wirtualnej o nazwie `myVM` hello grupy zasobów o nazwie `myResourceGroup`:

    ```azurecli
    az vm deallocate --resource-group myResourceGroup --name myVM
    ```

2. Skonwertuj dyski toomanaged wirtualna hello przy użyciu [konwersji maszyny wirtualnej az](/cli/azure/vm#convert). Hello następującego procesu konwertuje hello maszyny Wirtualnej o nazwie `myVM`, w tym dysku hello systemu operacyjnego i dysków z danymi:

    ```azurecli
    az vm convert --resource-group myResourceGroup --name myVM
    ```

3. Rozpocznij hello maszyny Wirtualnej po hello konwersji toomanaged dysków za pomocą [uruchomienia maszyny wirtualnej az](/cli/azure/vm#start). Po uruchomieniu przykład Hello hello maszyny Wirtualnej o nazwie `myVM` hello grupy zasobów o nazwie `myResourceGroup`.

    ```azurecli
    az vm start --resource-group myResourceGroup --name myVM
    ```

## <a name="convert-vms-in-an-availability-set"></a>Konwertuj maszyn wirtualnych w zestawie dostępności

Hello maszyn wirtualnych, które mają tooconvert toomanaged dyski znajdują się w zestawie dostępności, należy najpierw tooconvert hello dostępność zestawu tooa zarządzanego zestawu dostępności.

Wszystkie maszyny wirtualne w zestawie dostępności hello musi przydzielenia przed dokonaniem konwersji hello zestawu dostępności. Wszystkie dyski toomanaged maszyn wirtualnych po udostępnieniu hello ustawić siebie tooconvert plan został przekonwertowany tooa zarządzanego zestawu dostępności. Następnie uruchom wszystkie maszyny wirtualne hello i kontynuowania działania jako standardowa.

1. Wyświetl listę wszystkich maszyn wirtualnych w zestawie przy użyciu dostępności [listy zestawu dostępności maszyny wirtualnej az](/cli/azure/vm/availability-set#list). Witaj poniższy przykład zawiera listę wszystkich maszyn wirtualnych w zestawie o nazwie dostępności hello `myAvailabilitySet` hello grupy zasobów o nazwie `myResourceGroup`:

    ```azurecli
    az vm availability-set show \
        --resource-group myResourceGroup \
        --name myAvailabilitySet \
        --query [virtualMachines[*].id] \
        --output table
    ```

2. Cofnięcie przydziału wszystkich hello maszyn wirtualnych za pomocą [deallocate wirtualna az](/cli/azure/vm#deallocate). Witaj poniższy przykład cofa alokację hello maszyny Wirtualnej o nazwie `myVM` hello grupy zasobów o nazwie `myResourceGroup`:

    ```azurecli
    az vm deallocate --resource-group myResourceGroup --name myVM
    ```

3. Konwertuj dostępności hello skonfigurowane za pomocą [przekonwertować zestawu dostępności maszyny wirtualnej az](/cli/azure/vm/availability-set#convert). Witaj poniższy przykład konwertuje zestaw o nazwie dostępności hello `myAvailabilitySet` hello grupy zasobów o nazwie `myResourceGroup`:

    ```azurecli
    az vm availability-set convert \
        --resource-group myResourceGroup \
        --name myAvailabilitySet
    ```

4. Konwertuj wszystkie dyski toomanaged maszyn wirtualnych hello przy użyciu [konwersji maszyny wirtualnej az](/cli/azure/vm#convert). Hello następującego procesu konwertuje hello maszyny Wirtualnej o nazwie `myVM`, w tym dysku hello systemu operacyjnego i dysków z danymi:

    ```azurecli
    az vm convert --resource-group myResourceGroup --name myVM
    ```

5. Uruchomienie wszystkich maszyn wirtualnych powitania po hello konwersji toomanaged dysków za pomocą [uruchomienia maszyny wirtualnej az](/cli/azure/vm#start). Po uruchomieniu przykład Hello hello maszyny Wirtualnej o nazwie `myVM` hello grupy zasobów o nazwie `myResourceGroup`:

    ```azurecli
    az vm start --resource-group myResourceGroup --name myVM
    ```

## <a name="next-steps"></a>Następne kroki
Aby uzyskać więcej informacji na temat opcji magazynu, zobacz [omówienie dysków zarządzanych Azure](../windows/managed-disks-overview.md).
