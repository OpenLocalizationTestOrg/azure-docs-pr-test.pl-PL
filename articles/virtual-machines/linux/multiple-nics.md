---
title: "aaaCreate Maszynę wirtualną systemu Linux na platformie Azure z wieloma kartami sieciowymi | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toocreate Maszynę wirtualną systemu Linux z wieloma kartami sieciowymi dołączony tooit za pomocą szablonów hello Azure CLI w wersji 2.0 lub Menedżera zasobów."
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
ms.assetid: 5d2d04d0-fc62-45fa-88b1-61808a2bc691
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 05/11/2017
ms.author: iainfou
ms.openlocfilehash: 2723405914777a5dce4354d4f5d8413e357f58e7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocreate-a-linux-virtual-machine-in-azure-with-multiple-network-interface-cards"></a>Jak kartami interfejsu toocreate maszyny wirtualnej systemu Linux na platformie Azure z wielu sieci
Można utworzyć maszynę wirtualną (VM) na platformie Azure, który ma wiele tooit interfejsów (NIC), podłączonych sieci wirtualnej. Typowy scenariusz obejmuje toohave w różnych podsieciach łączności frontonu i zaplecza, lub sieci dedykowanej tooa monitorowania lub tworzenia kopii zapasowych. W tym artykule szczegółowo jak tooit dołączony toocreate Maszynę wirtualną z wieloma kartami sieciowymi i jak tooadd lub usuń karty sieciowe z istniejącej maszyny Wirtualnej. Aby uzyskać szczegółowe informacje, w tym jak toocreate wiele kart sieciowych w ramach własnego Bash skrypty, przeczytaj więcej na temat [wdrażanie maszyn wirtualnych z wieloma kartami Sieciowymi](../../virtual-network/virtual-network-deploy-multinic-arm-cli.md). Różne [rozmiarów maszyn wirtualnych](sizes.md) obsługuje różną liczbę kart sieciowych, więc odpowiednio rozmiar maszyny Wirtualnej.

Ten artykuł zawiera szczegóły dotyczące sposobu toocreate a maszyn wirtualnych z wieloma kartami sieciowymi z hello Azure CLI 2.0. Można również wykonać te kroki hello [Azure CLI 1.0](multiple-nics-nodejs.md).


## <a name="create-supporting-resources"></a>Utwórz dodatkowe zasoby
Najnowsza wersja hello instalacji [Azure CLI 2.0](/cli/azure/install-az-cli2) i zaloguj się za pomocą konta Azure tooan [logowania az](/cli/azure/#login).

Poniższe przykłady w hello Zastąp przykładowe nazwy parametrów własne wartości. Przykład nazwy parametrów uwzględnione *myResourceGroup*, *mojekontomagazynu*, i *myVM*.

Najpierw utwórz nową grupę zasobów o [Tworzenie grupy az](/cli/azure/group#create). Witaj poniższy przykład tworzy grupę zasobów o nazwie *myResourceGroup* w hello *eastus* lokalizacji:

```azurecli
az group create --name myResourceGroup --location eastus
```

Utwórz sieć wirtualną hello z [tworzenie sieci wirtualnej sieci az](/cli/azure/network/vnet#create). Witaj poniższy przykład tworzy sieć wirtualną o nazwie *myVnet* i podsieć o nazwie *mySubnetFrontEnd*:

```azurecli
az network vnet create \
    --resource-group myResourceGroup \
    --name myVnet \
    --address-prefix 192.168.0.0/16 \
    --subnet-name mySubnetFrontEnd \
    --subnet-prefix 192.168.1.0/24
```

Utwórz podsieć dla ruchu zaplecza hello z [Utwórz podsieć sieci wirtualnej sieci az](/cli/azure/network/vnet/subnet#create). Witaj poniższy przykład tworzy podsieć o nazwie *mySubnetBackEnd*:

```azurecli
az network vnet subnet create \
    --resource-group myResourceGroup \
    --vnet-name myVnet \
    --name mySubnetBackEnd \
    --address-prefix 192.168.2.0/24
```

Utwórz grupę zabezpieczeń sieci z [utworzyć nsg sieci az](/cli/azure/network/nsg#create). Witaj poniższy przykład tworzy sieciową grupę zabezpieczeń o nazwie *myNetworkSecurityGroup*:

```azurecli
az network nsg create \
    --resource-group myResourceGroup \
    --name myNetworkSecurityGroup
```

## <a name="create-and-configure-multiple-nics"></a>Tworzenie i konfigurowanie wielu kart sieciowych
Utwórz dwie karty sieciowe z [tworzenie kart interfejsu sieciowego az](/cli/azure/network/nic#create). Witaj poniższy przykład tworzy dwie karty sieciowe, o nazwie *myNic1* i *myNic2*, połączonych hello grupy zabezpieczeń sieci, z jedną kartą Sieciową łączące tooeach podsieci:

```azurecli
az network nic create \
    --resource-group myResourceGroup \
    --name myNic1 \
    --vnet-name myVnet \
    --subnet mySubnetFrontEnd \
    --network-security-group myNetworkSecurityGroup
az network nic create \
    --resource-group myResourceGroup \
    --name myNic2 \
    --vnet-name myVnet \
    --subnet mySubnetBackEnd \
    --network-security-group myNetworkSecurityGroup
```

## <a name="create-a-vm-and-attach-hello-nics"></a>Utwórz Maszynę wirtualną i Dołącz hello kart sieciowych
Podczas tworzenia hello maszyny Wirtualnej, określ hello karty sieciowe zostały utworzone z `--nics`. Należy również uwagę tootake po wybraniu hello rozmiar maszyny Wirtualnej. Istnieją ograniczenia hello całkowitą liczbę kart sieciowych, że można dodawać tooa maszyny Wirtualnej. Przeczytaj więcej na temat [rozmiarów maszyn wirtualnych systemu Linux](sizes.md). 

Utwórz maszynę wirtualną za pomocą polecenia [az vm create](/cli/azure/vm#create). Witaj poniższy przykład tworzy Maszynę wirtualną o nazwie *myVM*:

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --image UbuntuLTS \
    --size Standard_DS3_v2 \
    --admin-username azureuser \
    --generate-ssh-keys \
    --nics myNic1 myNic2
```

## <a name="add-a-nic-tooa-vm"></a>Dodaj tooa karty Sieciowej maszyny Wirtualnej
poprzednie kroki Hello utworzyć Maszynę wirtualną z wieloma kartami sieciowymi. Można również dodać istniejące maszyny Wirtualnej z hello Azure CLI 2.0 tooan kart sieciowych. 

Utwórz inną kartą Sieciową o [tworzenie kart interfejsu sieciowego az](/cli/azure/network/nic#create). Witaj poniższy przykład tworzy karty Sieciowej o nazwie *myNic3* podłączone podsieci wewnętrznej toohello i grupy zabezpieczeń sieci utworzone w poprzednich krokach hello:

```azurecli
az network nic create \
    --resource-group myResourceGroup \
    --name myNic3 \
    --vnet-name myVnet \
    --subnet mySubnetBackEnd \
    --network-security-group myNetworkSecurityGroup
```

tooadd tooan kart istniejącej maszyny Wirtualnej, najpierw cofnąć hello maszyny Wirtualnej z [deallocate wirtualna az](/cli/azure/vm#deallocate). Witaj poniższy przykład cofa alokację hello maszyny Wirtualnej o nazwie *myVM*:

```azurecli
az vm deallocate --resource-group myResourceGroup --name myVM
```

Dodaj hello kartą Sieciową o [Dodaj kartę sieciową maszyny wirtualnej az](/cli/azure/vm/nic#add). Witaj poniższy przykład umożliwia dodanie *myNic3* za*myVM*:

```azurecli
az vm nic add \
    --resource-group myResourceGroup \
    --vm-name myVM \
    --nics myNic3
```

Uruchom hello maszyny Wirtualnej z [uruchomienia maszyny wirtualnej az](/cli/azure/vm#start):

```azurecli
az vm start --resource-group myResourceGroup --name myVM
```

## <a name="remove-a-nic-from-a-vm"></a>Usuń kartę Sieciową z maszyny Wirtualnej
tooremove karty Sieciowej z istniejącej maszyny Wirtualnej, najpierw cofnąć hello maszyny Wirtualnej z [deallocate wirtualna az](/cli/azure/vm#deallocate). Witaj poniższy przykład cofa alokację hello maszyny Wirtualnej o nazwie *myVM*:

```azurecli
az vm deallocate --resource-group myResourceGroup --name myVM
```

Usuń hello kartą Sieciową o [Usuń kartę sieciową maszyny wirtualnej az](/cli/azure/vm/nic#remove). Witaj poniższy przykład umożliwia usunięcie *myNic3* z *myVM*:

```azurecli
az vm nic remove \
    --resource-group myResourceGroup \
    --vm-name myVM 
    --nics myNic3
```

Uruchom hello maszyny Wirtualnej z [uruchomienia maszyny wirtualnej az](/cli/azure/vm#start):

```azurecli
az vm start --resource-group myResourceGroup --name myVM
```


## <a name="create-multiple-nics-using-resource-manager-templates"></a>Tworzenie wielu kart sieciowych przy użyciu szablonów usługi Resource Manager
Szablony usługi Azure Resource Manager Użyj deklaratywne toodefine pliki JSON środowiska. Możesz przeczytać [Omówienie usługi Azure Resource Manager](../../azure-resource-manager/resource-group-overview.md). Szablony Menedżera zasobów zapewniają toocreate sposób wielu wystąpień zasobu podczas wdrażania, takich jak tworzenie wielu kart sieciowych. Możesz użyć *kopiowania* toospecify hello liczbę wystąpień toocreate:

```json
"copy": {
    "name": "multiplenics"
    "count": "[parameters('count')]"
}
```

Przeczytaj więcej na temat [tworzenia wielu wystąpień przy użyciu *kopiowania*](../../resource-group-create-multiple.md). 

Można również użyć `copyIndex()` toothen append numer Nazwa zasobu tooa, dzięki czemu można toocreate `myNic1`, `myNic2`, itp. hello poniżej pokazano przykład dołączanie wartość indeksu hello:

```json
"name": "[concat('myNic', copyIndex())]", 
```

Pełny przykład można znaleźć [tworzenia wielu kart sieciowych przy użyciu szablonów usługi Resource Manager](../../virtual-network/virtual-network-deploy-multinic-arm-template.md).

## <a name="next-steps"></a>Następne kroki
Przegląd [rozmiarów maszyn wirtualnych systemu Linux](sizes.md) podczas próby toocreating Maszynę wirtualną z wieloma kartami sieciowymi. Należy zwrócić uwagę toohello maksymalną liczbę kart sieciowych obsługuje każdego rozmiaru maszyny Wirtualnej. 
