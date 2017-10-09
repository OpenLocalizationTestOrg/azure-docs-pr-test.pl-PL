---
title: "aaaCreate kopię maszyny Wirtualnej systemu Linux z hello Azure CLI 1.0 | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toocreate kopia maszyny wirtualnej systemu Linux platformy Azure z hello Azure CLI 1.0 w modelu wdrażania usługi Resource Manager hello"
services: virtual-machines-linux
documentationcenter: 
author: cynthn
manager: timlt
tags: azure-resource-manager
ms.assetid: 770569d2-23c1-4a5b-801e-cddcd1375164
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 03/22/2017
ms.author: cynthn
ms.openlocfilehash: 997a2c8109e7083ececd76fd1013e9ed4d3e6afd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-copy-of-a-linux-virtual-machine-running-on-azure-with-hello-azure-cli-10"></a>Utworzenie kopii maszyny wirtualnej systemu Linux działających na platformie Azure z hello Azure CLI w wersji 1.0
W tym artykule opisano, jak toocreate kopię sieci maszyny wirtualnej platformy Azure (VM) uruchomionego systemu Linux przy użyciu hello modelu wdrażania usługi Resource Manager. Najpierw skopiować hello systemu operacyjnego i dysków tooa nowy kontener danych, a następnie skonfigurowaniu hello zasobów sieciowych i tworzenie nowej maszyny wirtualnej hello.

Możesz również [przekazywanie i tworzenie maszyny Wirtualnej z obrazu niestandardowego dysku](upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

## <a name="cli-versions-toocomplete-hello-task"></a>Zadanie hello toocomplete wersje interfejsu wiersza polecenia
Można ukończyć powitalnych zadań przy użyciu jednej z hello następujące wersje interfejsu wiersza polecenia:

- Azure CLI 1.0 — nasze interfejsu wiersza polecenia dla hello classic i zasobów zarządzania wdrażania modeli (w tym artykule)
- [Azure CLI 2.0](copy-vm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) -naszej nowej generacji interfejsu wiersza polecenia dla modelu wdrażania zarządzania zasobów hello

## <a name="before-you-begin"></a>Przed rozpoczęciem
Upewnij się, czy zostały spełnione następujące wymagania wstępne, przed rozpoczęciem powitalne kroki hello:

* Masz hello [interfejsu wiersza polecenia Azure](../../cli-install-nodejs.md) pobrane i zainstalowane na tym komputerze. 
* Należy również pewne informacje o istniejącej maszyny Wirtualnej systemu Linux platformy Azure:

| Informacje o źródle maszyny Wirtualnej | Gdzie tooget go |
| --- | --- |
| Nazwa maszyny wirtualnej |`azure vm list` |
| Nazwa grupy zasobów |`azure vm list` |
| Lokalizacja |`azure vm list` |
| Nazwa konta magazynu |`azure storage account list -g <resourceGroup>` |
| Nazwa kontenera |`azure storage container list -a <sourcestorageaccountname>` |
| Nazwa pliku wirtualnego dysku twardego maszyny Wirtualnej źródłowego |`azure storage blob list --container <containerName>` |

* Konieczne będzie toomake kilka opcji dotyczących nowej maszyny Wirtualnej:   <br> -Nazwa kontenera   <br> -Nazwa maszyny Wirtualnej   <br> Rozmiar maszyny Wirtualnej —   <br> Nazwa sieci wirtualnej-   <br> -Nazwa podsieci   <br> Nazwa - IP   <br> Nazwa - NIC

## <a name="login-and-set-your-subscription"></a>Logowania i ustaw swoją subskrypcję
1. Toohello logowania interfejsu wiersza polecenia.

    ```azurecli
    azure login
    ```
2. Upewnij się, że jesteś w trybie Menedżera zasobów.

    ```azurecli
    azure config mode arm
    ```
3. Ustaw hello poprawną subskrypcję. Można użyć "Lista konto platformy azure" toosee wszystkich subskrypcji.

    ```azurecli
    azure account set mySubscriptionID
    ```

## <a name="stop-hello-vm"></a>Zatrzymaj hello maszyny Wirtualnej
Zatrzymaj i cofnięcia przydzielenia hello źródłowej maszyny Wirtualnej. Można użyć "Lista maszyna wirtualna platformy azure" tooget listę wszystkich hello maszyn wirtualnych w subskrypcji i ich nazwy grup zasobów.

```azurecli
azure vm stop myResourceGroup myVM
azure vm deallocate myResourceGroup MyVM
```


## <a name="copy-hello-vhd"></a>Skopiuj hello wirtualnego dysku twardego
Możesz skopiować hello wirtualnego dysku twardego z hello źródła toohello miejscem docelowym magazynu przy użyciu hello `azure storage blob copy start`. W tym przykładzie zamierzamy toocopy hello wirtualnego dysku twardego toohello tego samego konta magazynu, ale różnych kontenerów.

kontener tooanother toocopy hello wirtualnego dysku twardego w hello tego samego konta magazynu, wpisz:

```azurecli
azure storage blob copy start \
        https://mystorageaccountname.blob.core.windows.net:8080/mycontainername/myVHD.vhd \
        myNewContainerName
```

## <a name="set-up-hello-virtual-network-for-your-new-vm"></a>Konfigurowanie sieci wirtualnej hello dla nowej maszyny Wirtualnej
Konfigurowanie sieci wirtualnej i karty Sieciowej dla nowej maszyny Wirtualnej. 

```azurecli
azure network vnet create myResourceGroup myVnet -l myLocation

azure network vnet subnet create -a <address.prefix.in.CIDR/format> myResourceGroup myVnet mySubnet

azure network public-ip create myResourceGroup myPublicIP -l myLocation

azure network nic create myResourceGroup myNic -k mySubnet -m myVnet -p myPublicIP -l myLocation
```


## <a name="create-hello-new-vm"></a>Utwórz hello nowej maszyny Wirtualnej
Teraz można utworzyć maszyny Wirtualnej z dysku wirtualnego przekazane [przy użyciu szablonu usługi resource manager](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-from-specialized-vhd) lub za pośrednictwem hello interfejsu wiersza polecenia, określając hello URI tooyour skopiowanych dysku, wpisując:

```azurecli
azure vm create -n myVM -l myLocation -g myResourceGroup -f myNic \
        -z Standard_DS1_v2 -y Linux \
        https://mystorageaccountname.blob.core.windows.net:8080/mycontainername/myVHD.vhd 
```



## <a name="next-steps"></a>Następne kroki
toolearn jak toomanage interfejsu wiersza polecenia Azure toouse nowej maszyny wirtualnej, zobacz [polecenia wiersza polecenia platformy Azure dla usługi Azure Resource Manager hello](../azure-cli-arm-commands.md).

