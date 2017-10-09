---
title: "aaaCreate Maszynę wirtualną systemu Linux na platformie Azure z wieloma kartami sieciowymi | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toocreate Maszynę wirtualną systemu Linux z wieloma kartami sieciowymi dołączony tooit za pomocą szablonów hello Azure CLI lub Menedżera zasobów."
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 05/11/2017
ms.author: iainfou
ms.openlocfilehash: 457dab734ceeeefd35cddaf1ebb9ea0a82f4e207
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-linux-virtual-machine-with-multiple-nics-using-hello-azure-cli-10"></a>Utwórz maszynę wirtualną systemu Linux z wieloma kartami sieciowymi przy użyciu hello Azure CLI w wersji 1.0
Można utworzyć maszynę wirtualną (VM) na platformie Azure, który ma wiele tooit interfejsów (NIC), podłączonych sieci wirtualnej. Typowy scenariusz obejmuje toohave w różnych podsieciach łączności frontonu i zaplecza, lub sieci dedykowanej tooa monitorowania lub tworzenia kopii zapasowych. Ten artykuł zawiera toocreate szybkie polecenia maszyny Wirtualnej z wielu kart sieciowych dołączonych tooit. Aby uzyskać szczegółowe informacje, w tym jak toocreate wiele kart sieciowych w ramach własnego Bash skrypty, przeczytaj więcej na temat [wdrażanie maszyn wirtualnych z wieloma kartami Sieciowymi](../../virtual-network/virtual-network-deploy-multinic-arm-cli.md). Różne [rozmiarów maszyn wirtualnych](sizes.md) obsługuje różną liczbę kart sieciowych, więc odpowiednio rozmiar maszyny Wirtualnej.

> [!WARNING]
> Podczas tworzenia maszyny Wirtualnej — nie można dodać istniejącej maszyny Wirtualnej z hello Azure CLI 1.0 tooan kart sieciowych należy dołączyć wiele kart sieciowych. Możesz [dodać tooan kart sieciowych z istniejącej maszyny Wirtualnej z hello Azure CLI 2.0](multiple-nics.md). Możesz również [Utwórz maszynę Wirtualną, oparte na dyskach wirtualnych oryginalnego hello](copy-vm.md) i utworzyć wiele kart sieciowych, jak wdrożyć hello maszyny Wirtualnej.


## <a name="cli-versions-toocomplete-hello-task"></a>Zadanie hello toocomplete wersje interfejsu wiersza polecenia
Można ukończyć powitalnych zadań przy użyciu jednej z hello następujące wersje interfejsu wiersza polecenia:

- [Azure CLI 1.0](#create-supporting-resources) — nasze interfejsu wiersza polecenia dla hello classic i zasobów zarządzania wdrażania modeli (w tym artykule)
- [Azure CLI 2.0](multiple-nics.md) -naszej nowej generacji interfejsu wiersza polecenia dla modelu wdrażania zarządzania zasobów hello


## <a name="create-supporting-resources"></a>Utwórz dodatkowe zasoby
Upewnij się, że masz hello [interfejsu wiersza polecenia Azure](../../cli-install-nodejs.md) zalogowany i w trybie Menedżera zasobów:

```azurecli
azure config mode arm
```

Poniższe przykłady w hello Zastąp przykładowe nazwy parametrów własne wartości. Przykład nazwy parametrów uwzględnione *myResourceGroup*, *mojekontomagazynu*, i *myVM*.

Najpierw utwórz grupę zasobów. Witaj poniższy przykład tworzy grupę zasobów o nazwie *myResourceGroup* w hello *eastus* lokalizacji:

```azurecli
azure group create myResourceGroup --location eastus
```

Utwórz toohold konta magazynu maszyn wirtualnych. Witaj poniższy przykład tworzy konto magazynu o nazwie *mojekontomagazynu*:

```azurecli
azure storage account create mystorageaccount \
    --resource-group myResourceGroup \
    --location eastus \
    --kind Storage \
    --sku-name PLRS
```

Tworzenie maszyn wirtualnych do tooconnect sieci wirtualnej. Witaj poniższy przykład tworzy sieć wirtualną o nazwie *myVnet* z prefiksem adresu o *192.168.0.0/16*:

```azurecli
azure network vnet create \
    --resource-group myResourceGroup \
    --location eastus \
    --name myVnet \
    --address-prefixes 192.168.0.0/16
```

Utwórz dwie sieci wirtualnej podsieci — po jednej dla ruchu frontonu i jedną dla ruchu zaplecza. Witaj poniższy przykład tworzy dwie podsieci o nazwie *mySubnetFrontEnd* i *mySubnetBackEnd*:

```azurecli
azure network vnet subnet create \
    --resource-group myResourceGroup \
    --location myVnet \
    --name mySubnetFrontEnd \
    --address-prefix 192.168.1.0/24
azure network vnet subnet create \
    --resource-group myResourceGroup \
    --location myVnet \
    --name mySubnetBackEnd \
    --address-prefix 192.168.2.0/24
```

## <a name="create-and-configure-multiple-nics"></a>Tworzenie i konfigurowanie wielu kart sieciowych
Więcej informacji zawiera temat [wdrażania wielu kart sieciowych przy użyciu interfejsu wiersza polecenia Azure hello](../../virtual-network/virtual-network-deploy-multinic-arm-cli.md), tym skrypty proces hello wszystkich kart hello toocreate w pętli.

Witaj poniższy przykład tworzy dwie karty sieciowe, o nazwie *myNic1* i *myNic2*, z jedną kartą Sieciową łączące tooeach podsieci:

```azurecli
azure network nic create \
    --resource-group myResourceGroup \
    --location eastus \
    --name myNic1 \
    --subnet-vnet-name myVnet \
    --subnet-name mySubnetFrontEnd
azure network nic create \
    --resource-group myResourceGroup \
    --location eastus \
    --name myNic2 \
    --subnet-vnet-name myVnet \
    --subnet-name mySubnetBackEnd
```

Zwykle również utworzyć [sieciowej grupy zabezpieczeń](../../virtual-network/virtual-networks-nsg.md) lub [modułu równoważenia obciążenia](../../load-balancer/load-balancer-overview.md) toohelp zarządzania i rozpowszechniają ruch maszyn wirtualnych. Witaj poniższy przykład tworzy sieciową grupę zabezpieczeń o nazwie *myNetworkSecurityGroup*:

```azurecli
azure network nsg create \
    --resource-group myResourceGroup \
    --location eastus \
    --name myNetworkSecurityGroup
```

Powiąż z kart sieciowych toohello grupy zabezpieczeń sieci przy użyciu `azure network nic set`. Witaj poniższy przykład wiąże *myNic1* i *myNic2* z *myNetworkSecurityGroup*:

```azurecli
azure network nic set \
    --resource-group myResourceGroup \
    --name myNic1 \
    --network-security-group-name myNetworkSecurityGroup
azure network nic set \
    --resource-group myResourceGroup \
    --name myNic2 \
    --network-security-group-name myNetworkSecurityGroup
```

## <a name="create-a-vm-and-attach-hello-nics"></a>Utwórz Maszynę wirtualną i Dołącz hello kart sieciowych
Podczas tworzenia hello maszyny Wirtualnej, teraz należy określić wiele kart sieciowych. Zamiast przy użyciu `--nic-name` tooprovide jedną kartę Sieciową, zamiast tego należy użyć `--nic-names` i zawierają rozdzielaną przecinkami listę kart sieciowych. Należy również uwagę tootake po wybraniu hello rozmiar maszyny Wirtualnej. Istnieją ograniczenia hello całkowitą liczbę kart sieciowych, że można dodawać tooa maszyny Wirtualnej. Przeczytaj więcej na temat [rozmiarów maszyn wirtualnych systemu Linux](sizes.md). Witaj poniższy przykład przedstawia sposób toospecify wiele kart sieciowych, a następnie maszyny Wirtualnej rozmiaru obsługującego przy użyciu wielu kart sieciowych (*Standard_DS2_v2*):

```azurecli
azure vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --location eastus \
    --os-type linux \
    --nic-names myNic1,myNic2 \
    --vm-size Standard_DS2_v2 \
    --storage-account-name mystorageaccount \
    --image-urn UbuntuLTS \
    --admin-username azureuser \
    --ssh-publickey-file ~/.ssh/id_rsa.pub
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
Upewnij się, że tooreview [rozmiarów maszyn wirtualnych systemu Linux](sizes.md) podczas próby toocreating Maszynę wirtualną z wieloma kartami sieciowymi. Należy zwrócić uwagę toohello maksymalną liczbę kart sieciowych obsługuje każdego rozmiaru maszyny Wirtualnej. 

Należy pamiętać, że nie można dodać dodatkowe tooan kart sieciowych, istniejącej maszyny Wirtualnej, należy utworzyć wszystkich kart hello podczas wdrażania hello maszyny Wirtualnej. Zachowaj ostrożność podczas planowania Twojej się, że wszystkie wymagane hello połączenia sieciowego z początku hello toomake wdrożeń.

