---
title: "tooresize aaaHow Maszynę wirtualną systemu Linux z hello Azure CLI 2.0 | Dokumentacja firmy Microsoft"
description: "Jak tooscale zapasowych lub Zmniejsz maszyny wirtualnej systemu Linux, zmieniając hello rozmiar maszyny Wirtualnej."
services: virtual-machines-linux
documentationcenter: na
author: mikewasson
manager: timlt
editor: 
tags: 
ms.assetid: e163f878-b919-45c5-9f5a-75a64f3b14a0
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/10/2017
ms.author: mwasson
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: e8fba485b5bcc7824f546de5cf3df77624a28008
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="resize-a-linux-virtual-machine-using-cli-20"></a>Zmień rozmiar maszyny wirtualnej systemu Linux przy użyciu interfejsu wiersza polecenia 2.0

Po udostępnić maszynę wirtualną (VM), można skalować hello maszyny Wirtualnej w górę lub w dół, zmieniając hello [rozmiar maszyny Wirtualnej][vm-sizes]. W niektórych przypadkach należy najpierw cofnąć hello maszyny Wirtualnej. W razie potrzeby hello rozmiar nie jest dostępny na hello sprzętu klastra, który jest hostem hello maszyny Wirtualnej należy hello toodeallocate maszyny Wirtualnej. Ten artykuł zawiera szczegóły dotyczące sposobu tooresize a Linux VM z hello Azure CLI 2.0. Można również wykonać te kroki hello [Azure CLI 1.0](change-vm-size-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

## <a name="resize-a-vm"></a>Zmienianie rozmiaru maszyny wirtualnej
tooresize maszyny Wirtualnej, należy hello najnowszych [Azure CLI 2.0](/cli/azure/install-az-cli2) zainstalowane i zarejestrowane za pomocą konta Azure tooan [logowania az](/cli/azure/#login).

1. Wyświetl listę hello maszyny wirtualnej dostępne rozmiary na powitania sprzętu klastra, gdzie jest hostowana hello maszyny Wirtualnej z [az maszyny wirtualnej-vm — zmiany rozmiaru — opcje listy](/cli/azure/vm#list-vm-resize-options). Witaj poniższy przykład zawiera listę rozmiarów maszyn wirtualnych dla maszyny Wirtualnej o nazwie hello `myVM` w grupie zasobów hello `myResourceGroup` regionu:
   
    ```azurecli
    az vm list-vm-resize-options --resource-group myResourceGroup --name myVM --output table
    ```

2. W razie potrzeby hello znajduje się rozmiar maszyny Wirtualnej, należy zmienić rozmiar hello maszyny Wirtualnej z [Zmień rozmiar maszyny wirtualnej az](/cli/azure/vm#resize). powitania po zmienia rozmiar przykład Witaj maszyny Wirtualnej o nazwie `myVM` toohello `Standard_DS3_v2` rozmiar:
   
    ```azurecli
    az vm resize --resource-group myResourceGroup --name myVM --size Standard_DS3_v2
    ```
   
    Witaj maszyny Wirtualnej zostanie uruchomiony ponownie w trakcie tego procesu. Po ponownym uruchomieniu hello są mapowane ponownie z istniejącego systemu operacyjnego i dysków z danymi. Elementy na dysku tymczasowym hello zostaną utracone.

3. W razie potrzeby hello rozmiar maszyny Wirtualnej nie ma na liście należy toofirst deallocate hello maszyny Wirtualnej z [deallocate wirtualna az](/cli/azure/vm#deallocate). Ten proces umożliwia hello toothen maszyny Wirtualnej jest dostępny rozmiar tooany po zmianie rozmiaru, który hello obsługuje region, a następnie uruchomiona. Witaj następujące kroki cofnięcie przydziału, Zmień rozmiar, a następnie uruchom hello maszyny Wirtualnej o nazwie `myVM` hello grupy zasobów o nazwie `myResourceGroup`:
   
    ```azurecli
    az vm deallocate --resource-group myResourceGroup --name myVM
    az vm resize --resource-group myResourceGroup --name myVM --size Standard_DS3_v2
    az vm start --resource-group myResourceGroup --name myVM
    ```
   
   > [!WARNING]
   > Cofanie przydziału hello wirtualna zwalnia również dynamiczne adresy IP przypisane toohello maszyny Wirtualnej. nie dotyczy Hello systemu operacyjnego i dysków z danymi.

## <a name="next-steps"></a>Następne kroki
Dodatkowe możliwości skalowania uruchamianie wielu wystąpień maszyny Wirtualnej i skalowanie w poziomie. Aby uzyskać więcej informacji, zobacz [automatycznie skalować w zestawie skalowania maszyn wirtualnych systemu Linux maszyny][scale-set]. 

<!-- links -->
[boot-diagnostics]: https://azure.microsoft.com/en-us/blog/boot-diagnostics-for-virtual-machines-v2/
[scale-set]: ../../virtual-machine-scale-sets/virtual-machine-scale-sets-linux-autoscale.md 
[vm-sizes]:sizes.md
