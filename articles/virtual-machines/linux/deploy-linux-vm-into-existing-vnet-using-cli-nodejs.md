---
title: "aaaDeploy maszyn wirtualnych systemu Linux w istniejącej sieci z interfejsu wiersza polecenia platformy Azure w wersji 1.0 | Dokumentacja firmy Microsoft"
description: "Jak toodeploy Maszynę wirtualną systemu Linux w istniejącej sieci wirtualnej przy użyciu hello Azure CLI w wersji 1.0"
services: virtual-machines-linux
documentationcenter: virtual-machines
author: iainfoulds
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.workload: infrastructure
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 05/11/2017
ms.author: iainfou
ms.openlocfilehash: e660f1563d386efc7788bd236f8b067145ea09bb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toodeploy-a-linux-virtual-machine-into-an-existing-azure-virtual-network-with-hello-azure-cli-10"></a>Jak toodeploy maszyny wirtualnej systemu Linux w istniejącej sieci wirtualnej platformy Azure z hello Azure CLI w wersji 1.0

W tym artykule opisano sposób toodeploy toouse Azure CLI 1.0 maszynę wirtualną (VM) do istniejącej sieci wirtualnej (VNet). wymagania dotyczące Hello są:

- [Konto platformy Azure](https://azure.microsoft.com/pricing/free-trial/)
- [Pliki kluczy publicznych i prywatnych SSH](mac-create-ssh-keys.md)


## <a name="cli-versions-toocomplete-hello-task"></a>Zadanie hello toocomplete wersje interfejsu wiersza polecenia
Można ukończyć powitalnych zadań przy użyciu jednej z hello następujące wersje interfejsu wiersza polecenia:

- [Azure CLI 1.0](#quick-commands) — nasze interfejsu wiersza polecenia dla hello classic i zasobów zarządzania wdrażania modeli (w tym artykule)
- [Azure CLI 2.0](deploy-linux-vm-into-existing-vnet-using-cli.md) -naszej nowej generacji interfejsu wiersza polecenia dla modelu wdrażania zarządzania zasobów hello


## <a name="quick-commands"></a>Szybkie polecenia

Jeśli potrzebujesz tooquickly hello zadania, powitania po sekcji Szczegóły poleceń hello potrzebne. Bardziej szczegółowe informacje i kontekst dla każdego kroku można znaleźć hello pozostałej części dokumentu hello [uruchamiania tutaj](deploy-linux-vm-into-existing-vnet-using-cli.md#detailed-walkthrough).

Wymagania Wstępne: NSG grupy zasobów, sieciami wirtualnymi, przy użyciu protokołu SSH ruchu przychodzącego, podsieci. Przykładami należy zastąpić własnymi ustawieniami.

### <a name="deploy-hello-vm-into-hello-virtual-network-infrastructure"></a>Wdrażanie hello maszyny Wirtualnej do hello infrastruktury sieci wirtualnej

```azurecli
azure vm create myVM \
    -g myResourceGroup \
    -l eastus \
    -y linux \
    -Q Debian \
    -o mystorageaccount \
    -u myAdminUser \
    -M ~/.ssh/id_rsa.pub \
    -n myVM \
    -F myVNet \
    -j mySubnet \
    -N myVNic
```

## <a name="detailed-walkthrough"></a>Szczegółowy przewodnik

Zasoby platformy Azure, takich jak hello sieci wirtualnych i grup zabezpieczeń sieci musi być statyczny i tam długo zasoby, które rzadko są wdrożone. Po wdrożeniu sieci wirtualnej można użyć ponownie przez nowych wdrożeń bez żadnych infrastruktury toohello niekorzystny wpływ. Traktować jako przełącznik sieciowy sprzętu tradycyjnych sieci wirtualnej. Nie trzeba tooconfigure nowego sprzętu przełącznik z każdym wdrożeniu. Z poprawnie skonfigurowana sieć wirtualną możesz kontynuować toodeploy nowych serwerów do tej sieci wirtualnej samodzielnego kilka, zmian wymaganych przez czas życia hello hello sieci wirtualnej.

## <a name="create-hello-resource-group"></a>Utwórz grupę zasobów hello

Najpierw utwórz tooorganize grupy zasobów wszystko, czego możesz utworzyć w tym przewodniku. Aby uzyskać więcej informacji na temat grup zasobów, zobacz [Omówienie usługi Azure Resource Manager](../../azure-resource-manager/resource-group-overview.md)

```azurecli
azure group create myResourceGroup --location eastus
```

## <a name="create-hello-vnet"></a>Utwórz hello sieci wirtualnej

Witaj pierwszym krokiem jest toobuild maszyn wirtualnych do hello toolaunch sieci wirtualnej. Witaj sieć wirtualna zawiera jedną podsieć w ramach tego przewodnika. Aby uzyskać więcej informacji o sieci wirtualnych platformy Azure, zobacz [utworzyć sieć wirtualną przy użyciu hello wiersza polecenia platformy Azure](../../virtual-network/virtual-networks-create-vnet-arm-cli.md)

```azurecli
azure network vnet create myVNet \
    --resource-group myResourceGroup \
    --address-prefixes 10.10.0.0/24 \
    --location eastus
```

## <a name="create-hello-network-security-group"></a>Utwórz grupę zabezpieczeń sieci hello

podsieci Hello jest wbudowana za istniejącej grupy zabezpieczeń sieci tak kompilacji hello sieciowej grupy zabezpieczeń przed hello podsieci. Grupy zabezpieczeń sieci platformy Azure są równoważne tooa zapory na powitania warstwy sieci. Aby uzyskać więcej informacji dotyczących grup zabezpieczeń sieci platformy Azure, zobacz [jak grupy zabezpieczeń sieci toocreate w hello wiersza polecenia platformy Azure](../../virtual-network/virtual-networks-create-nsg-arm-cli.md)

```azurecli
azure network nsg create myNetworkSecurityGroup \
    --resource-group myResourceGroup \
    --location eastus
```

## <a name="add-an-inbound-ssh-allow-rule"></a>Dodaj regułę Zezwalaj SSH dla ruchu przychodzącego

Witaj maszyna wirtualna musi mieć dostęp z hello internet, regułę zezwalającą na toobe ruch przychodzący port 22 przekazywane hello sieci tooport 22 na powitania maszyny Wirtualnej jest wymagana.

```azurecli
azure network nsg rule create inboundSSH \
    --resource-group myResourceGroup \
    --nsg-name myNSG \
    --access Allow \
    --protocol Tcp \
    --direction Inbound \
    --priority 100 \
    --source-address-prefix Internet \
    --source-port-range 22 \
    --destination-address-prefix 10.10.0.0/24 \
    --destination-port-range 22
```

## <a name="add-a-subnet-toohello-vnet"></a>Dodaj toohello podsieci sieci wirtualnej

Maszyny wirtualne w ramach hello sieci wirtualnej muszą znajdować się w podsieci. Każda sieć wirtualna może mieć wiele podsieci. Utwórz podsieć hello i skojarz z hello sieciowej grupy zabezpieczeń.

```azurecli
azure network vnet subnet create mySubNet \
    --resource-group myResourceGroup \
    --vnet-name myVNet \
    --address-prefix 10.10.0.0/26 \
    --network-security-group-name myNetworkSecurityGroup
```

Hello podsieci jest teraz dodawane wewnątrz hello sieci wirtualnej i skojarzonych z hello sieciowej grupy zabezpieczeń i reguły.


## <a name="add-a-vnic-toohello-subnet"></a>Dodaj podsieć toohello VNic

Wirtualne karty sieciowe (VNics) są ważne, ponieważ późniejszego łącząc je toodifferent maszyn wirtualnych. Takie podejście zapewnia hello VNic jako zasób statycznych hello maszyny wirtualne mogą być tymczasowe. Utwórz VNic i skojarzyć go z podsiecią hello utworzony w poprzednim kroku hello.

```azurecli
azure network nic create myVNic \
    --resource-group myResourceGroup \
    --location eastus \
    ---subnet-vnet-name myVNet \
    --subnet-name mySubNet
```

## <a name="deploy-hello-vm-into-hello-vnet-and-nsg"></a>Wdrażanie hello maszyny Wirtualnej do hello sieci wirtualnej i grupy NSG

Istnieje już sieć wirtualną i podsieci w tej sieci wirtualnej i sieciową grupę zabezpieczeń, stanowiąc podsieci hello tooprotect blokuje cały ruch przychodzący z wyjątkiem port 22 dla protokołu SSH. Teraz można wdrożyć Hello maszyny Wirtualnej w tym istniejącej infrastruktury sieci.

Przy użyciu interfejsu wiersza polecenia Azure hello i hello `azure vm create` polecenia hello maszyny Wirtualnej systemu Linux jest wdrożony toohello istniejącej grupy zasobów platformy Azure, sieci wirtualnej, podsieci i VNic. Aby uzyskać więcej informacji na temat używania hello CLI toodeploy pełną maszyny Wirtualnej, zobacz [tworzyć kompletne środowisko systemu Linux przy użyciu interfejsu wiersza polecenia Azure hello](create-cli-complete.md)

```azurecli
azure vm create myVM \
    --resource-group myResourceGroup \
    --location eastus \
    --os-type linux \
    --image-urn Debian \
    --storage-account-name mystorageaccount \
    --admin-username myAdminUser \
    --ssh-publickey-file ~/.ssh/id_rsa.pub \
    --vnet-name myVNet \
    --vnet-subnet-name mySubnet \
    --nic-name myVNic
```

Za pomocą hello interfejsu wiersza polecenia flagi toocall limit istniejących zasobów, poinstruuj hello Azure toodeploy VM wewnątrz hello istniejącej sieci. Po wdrożeniu sieci wirtualnej i podsieci, możesz je zostawić jako statyczne ani stałe zasoby w Twoim regionie Azure.  

## <a name="next-steps"></a>Następne kroki

* [Użyj toocreate szablonu usługi Azure Resource Manager określonego wdrożenia](../windows/cli-deploy-templates.md)
* [Tworzenie niestandardowego środowiska dla maszyny wirtualnej z systemem Linux poprzez bezpośrednie użycie poleceń interfejsu wiersza polecenia platformy Azure](create-cli-complete.md)
* [Utwórz Maszynę wirtualną systemu Linux na platformie Azure za pomocą szablonów](create-ssh-secured-vm-from-template.md)
