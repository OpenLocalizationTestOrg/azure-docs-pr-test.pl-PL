---
title: "aaaCopy Maszynę wirtualną systemu Linux przy użyciu interfejsu wiersza polecenia platformy Azure w wersji 2.0 | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toocreate kopię maszyny Wirtualnej systemu Linux platformy Azure przy użyciu interfejsu wiersza polecenia platformy Azure w wersji 2.0 i dysków zarządzanych."
services: virtual-machines-linux
documentationcenter: 
author: cynthn
manager: timlt
tags: azure-resource-manager
ms.assetid: 770569d2-23c1-4a5b-801e-cddcd1375164
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: azurecli
ms.topic: article
ms.date: 03/10/2017
ms.author: cynthn
ms.openlocfilehash: ee34a4259dd0c1e7bf49312fe3fe3ba809bf69e5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-copy-of-a-linux-vm-by-using-azure-cli-20-and-managed-disks"></a>Utworzenie kopii maszyny wirtualnej systemu Linux przy użyciu interfejsu wiersza polecenia platformy Azure w wersji 2.0 i dysków zarządzanych


W tym artykule opisano, jak toocreate kopię Azure maszyny wirtualnej (VM) systemem Linux przy użyciu hello Azure CLI w wersji 2.0 i modelu wdrażania usługi Azure Resource Manager hello. Można również wykonać te kroki hello [Azure CLI 1.0](copy-vm-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

Możesz również [przekazywanie i tworzenie maszyny Wirtualnej z dysku VHD](upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

## <a name="prerequisites"></a>Wymagania wstępne


-   Zainstaluj [Azure CLI 2.0](/cli/azure/install-az-cli2)

-   Zaloguj się tooan konto platformy Azure z [logowania az](/cli/azure/#login).

-   Ma toouse maszyny Wirtualnej platformy Azure jako hello źródła dla tej kopii.

## <a name="step-1-stop-hello-source-vm"></a>Krok 1: Zatrzymaj hello źródłowej maszyny Wirtualnej


Cofnięcie przydziału hello źródłowej maszyny Wirtualnej za pomocą [deallocate wirtualna az](/cli/azure/vm#deallocate).
Witaj poniższy przykład cofa alokację hello maszyny Wirtualnej o nazwie **myVM** w grupie zasobów hello **myResourceGroup**:

```azurecli
az vm deallocate --resource-group myResourceGroup --name myVM
```

## <a name="step-2-copy-hello-source-vm"></a>Krok 2: Kopiowanie hello źródłowej maszyny Wirtualnej


toocopy Maszynę wirtualną, Utwórz kopię hello podstawowych dysków wirtualnych. Ten proces tworzy specjalne wirtualnego dysku twardego jako zarządzane dysk zawierający hello tej samej konfiguracji i ustawień, jak hello źródłowej maszyny Wirtualnej.

Aby uzyskać więcej informacji o dyskach Azure Managed Disks, zobacz [Omówienie usługi Azure Managed Disks](../windows/managed-disks-overview.md). 

1.  Każda nazwa maszyny Wirtualnej i hello jej dysk systemu operacyjnego z [listy wirtualna az](/cli/azure/vm#list). Witaj poniższy przykład zawiera listę wszystkich maszyn wirtualnych w grupie zasobów o nazwie **myResourceGroup**:
    
    ```azurecli
    az vm list -g myTestRG --query '[].{Name:name,DiskName:storageProfile.osDisk.name}' --output table
    ```

    Witaj danych wyjściowych jest toohello podobnie poniższy przykład:

    ```azurecli
    Name    DiskName
    ------  --------
    myVM    myDisk
    ```

1.  Kopiuj hello dysk, tworząc nowe zarządzane przy użyciu dysku [Tworzenie dysku az](/cli/azure/disk#create). Witaj poniższy przykład tworzy dysk o nazwie **myCopiedDisk** z hello zarządzane dysku o nazwie **myDisk**:

    ```azurecli
    az disk create --resource-group myResourceGroup --name myCopiedDisk --source myDisk
    ``` 

1.  Sprawdź hello zarządzane dysków w grupie zasobów za pomocą [Lista dysków az](/cli/azure/disk#list). Hello poniższy przykład zawiera listę dysków hello zarządzane w hello grupy zasobów o nazwie **myResourceGroup**:

    ```azurecli
    az disk list --resource-group myResourceGroup --output table
    ```

1.  Pomiń zbyt["krok 3: Konfigurowanie sieci wirtualnej"](#step-3-set-up-a-virtual-network).


## <a name="step-3-set-up-a-virtual-network"></a>Krok 3: Konfigurowanie sieci wirtualnej


Witaj następujące opcjonalne kroki tworzenia nowej sieci wirtualnej, podsieci, publiczny adres IP i sieć wirtualna karta sieciowa (NIC).

Jeśli kopiujesz Maszynę wirtualną do rozwiązywania problemów z celów lub dodatkowe wdrożenia, nie może być toouse maszyny Wirtualnej w ramach istniejącej sieci wirtualnej.

Jeśli chcesz toocreate infrastruktury sieci wirtualnej dla maszyn wirtualnych skopiowanych wykonaj hello obok kilku kroków. Jeśli nie chcesz toocreate sieci wirtualnej, Pomiń zbyt[krok 4: tworzenie maszyny Wirtualnej](#step-4-create-a-vm).

1.  Utwórz sieć wirtualną hello przy użyciu [tworzenie sieci wirtualnej sieci az](/cli/azure/network/vnet#create). Witaj poniższy przykład tworzy sieć wirtualną o nazwie **myVnet** i podsieć o nazwie **mySubnet**:

    ```azurecli
    az network vnet create --resource-group myResourceGroup --location westus --name myVnet \
        --address-prefix 192.168.0.0/16 --subnet-name mySubnet --subnet-prefix 192.168.1.0/24
    ```

1.  Tworzenie publicznego adresu IP za pomocą [utworzyć az sieci publicznej ip](/cli/azure/network/public-ip#create). Witaj poniższy przykład tworzy publicznego adresu IP o nazwie **myPublicIP** o nazwie DNS hello **mypublicdns**. (nazwa DNS hello musi być unikatowa, więc Podaj unikatową nazwę.)

    ```azurecli
    az network public-ip create --resource-group myResourceGroup --location westus \
        --name myPublicIP --dns-name mypublicdns --allocation-method static --idle-timeout 4
    ```

1.  Tworzenie przy użyciu kart hello [tworzenie kart interfejsu sieciowego az](/cli/azure/network/nic#create).
    Witaj poniższy przykład tworzy karty Sieciowej o nazwie **myNic** to jest dołączona toothe **mySubnet** podsieci:

    ```azurecli
    az network nic create --resource-group myResourceGroup --location westus --name myNic \
        --vnet-name myVnet --subnet mySubnet --public-ip-address myPublicIP
    ```

## <a name="step-4-create-a-vm"></a>Krok 4: Tworzenie maszyny Wirtualnej

Można teraz utworzyć Maszynę wirtualną za pomocą [tworzenia maszyny wirtualnej az](/cli/azure/vm#create).

Określ hello skopiowane toouse dysków zarządzanych jako dysk systemu operacyjnego hello (--attach-os-disk) w następujący sposób:

```azurecli
az vm create --resource-group myResourceGroup --name myCopiedVM \
    --admin-username azureuser --ssh-key-value ~/.ssh/id_rsa.pub \
    --nics myNic --size Standard_DS1_v2 --os-type Linux \
    --attach-os-disk myCopiedDisk
```

## <a name="next-steps"></a>Następne kroki

toolearn jak toomanage interfejsu wiersza polecenia Azure toouse nowej maszyny Wirtualnej, zobacz [polecenia wiersza polecenia platformy Azure dla usługi Azure Resource Manager hello](../azure-cli-arm-commands.md).
