---
title: "Wdrażanie maszyn wirtualnych systemu Linux w istniejącej sieci z interfejsu wiersza polecenia platformy Azure w wersji 1.0 | Dokumentacja firmy Microsoft"
description: "Jak wdrożyć Maszynę wirtualną systemu Linux w ramach istniejącej sieci wirtualnej przy użyciu 1.0 interfejsu wiersza polecenia platformy Azure"
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
ms.openlocfilehash: 767a3f7cadba6b1e71e5a8f5995a9db090e419dd
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-deploy-a-linux-virtual-machine-into-an-existing-azure-virtual-network-with-the-azure-cli-10"></a>Jak wdrożyć maszyny wirtualnej systemu Linux w istniejącej sieci wirtualnej platformy Azure z interfejsu wiersza polecenia platformy Azure w wersji 1.0

W tym artykule przedstawiono sposób użycia interfejsu wiersza polecenia platformy Azure w wersji 1.0, aby wdrożyć maszynę wirtualną (VM) do istniejącej sieci wirtualnej (VNet). Wymagania są następujące:

- [Konto platformy Azure](https://azure.microsoft.com/pricing/free-trial/)
- [Pliki kluczy publicznych i prywatnych SSH](mac-create-ssh-keys.md)


## <a name="cli-versions-to-complete-the-task"></a>Wersje interfejsu wiersza polecenia umożliwiające wykonanie zadania
Zadanie można wykonać przy użyciu jednej z następujących wersji interfejsu wiersza polecenia:

- [Azure CLI 1.0](#quick-commands) — nasze interfejsu wiersza polecenia dla klasycznego i zasobów zarządzania wdrażania modeli (w tym artykule)
- [Interfejs wiersza polecenia platformy Azure w wersji 2.0](deploy-linux-vm-into-existing-vnet-using-cli.md) — nasz interfejs wiersza polecenia nowej generacji dla modelu wdrażania na potrzeby zarządzania zasobami


## <a name="quick-commands"></a>Szybkie polecenia

Jeśli chcesz szybko wykonywać zadania poniższej sekcji Szczegóły poleceń potrzebne. Bardziej szczegółowe informacje i kontekst dla każdego kroku można znaleźć pozostałej części dokumentu, [uruchamiania tutaj](deploy-linux-vm-into-existing-vnet-using-cli.md#detailed-walkthrough).

Wymagania Wstępne: NSG grupy zasobów, sieciami wirtualnymi, przy użyciu protokołu SSH ruchu przychodzącego, podsieci. Przykładami należy zastąpić własnymi ustawieniami.

### <a name="deploy-the-vm-into-the-virtual-network-infrastructure"></a>Wdróż maszynę Wirtualną do infrastruktury sieci wirtualnej

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

Zasoby platformy Azure, takich jak sieci wirtualnych i grup zabezpieczeń sieci musi być statyczny i tam długo zasoby, które rzadko są wdrożone. Po wdrożeniu sieci wirtualnej można użyć ponownie przez nowych wdrożeń bez żadnych niekorzystny wpływ infrastruktury. Traktować jako przełącznik sieciowy sprzętu tradycyjnych sieci wirtualnej. Nie musisz skonfigurować nowy przełącznik sprzętu z każdym wdrożeniu. Z poprawnie skonfigurowana sieć wirtualną możesz kontynuować wdrażanie nowych serwerów w tej sieci wirtualnej samodzielnego z kilku ewentualne zmiany wymagane w całej sieci wirtualnej.

## <a name="create-the-resource-group"></a>Tworzenie grupy zasobów

Najpierw utwórz grupę zasobów do organizowania wszystko, czego możesz utworzyć w tym przewodniku. Aby uzyskać więcej informacji na temat grup zasobów, zobacz [Omówienie usługi Azure Resource Manager](../../azure-resource-manager/resource-group-overview.md)

```azurecli
azure group create myResourceGroup --location eastus
```

## <a name="create-the-vnet"></a>Tworzenie sieci wirtualnej

Pierwszym krokiem jest kompilacji do uruchamiania maszyn wirtualnych do sieci wirtualnej. Sieć wirtualna zawiera jedną podsieć w ramach tego przewodnika. Aby uzyskać więcej informacji o sieci wirtualnych platformy Azure, zobacz [utworzyć sieć wirtualną przy użyciu wiersza polecenia platformy Azure](../../virtual-network/virtual-networks-create-vnet-arm-cli.md)

```azurecli
azure network vnet create myVNet \
    --resource-group myResourceGroup \
    --address-prefixes 10.10.0.0/24 \
    --location eastus
```

## <a name="create-the-network-security-group"></a>Utwórz grupę zabezpieczeń sieci

Podsieć jest wbudowana za istniejącej sieci grupy zabezpieczeń tak Tworzenie grupy zabezpieczeń sieci przed podsieci. Grupy zabezpieczeń sieci platformy Azure są równoważne zapory w warstwie sieci. Aby uzyskać więcej informacji dotyczących grup zabezpieczeń sieci platformy Azure, zobacz [sposobu tworzenia grup zabezpieczeń sieci na platformie Azure CLI](../../virtual-network/virtual-networks-create-nsg-arm-cli.md)

```azurecli
azure network nsg create myNetworkSecurityGroup \
    --resource-group myResourceGroup \
    --location eastus
```

## <a name="add-an-inbound-ssh-allow-rule"></a>Dodaj regułę Zezwalaj SSH dla ruchu przychodzącego

Maszyna wirtualna wymaga dostępu z Internetu, więc regułę zezwalającą na ruch przychodzący port 22 mają być przekazywane za pośrednictwem sieci do portu 22 na maszynie Wirtualnej nie jest wymagane.

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

## <a name="add-a-subnet-to-the-vnet"></a>Dodaj podsieć do sieci wirtualnej

Maszyny wirtualne w ramach sieci wirtualnej muszą znajdować się w podsieci. Każda sieć wirtualna może mieć wiele podsieci. Utwórz podsieć i skojarzyć z sieciową grupą zabezpieczeń.

```azurecli
azure network vnet subnet create mySubNet \
    --resource-group myResourceGroup \
    --vnet-name myVNet \
    --address-prefix 10.10.0.0/26 \
    --network-security-group-name myNetworkSecurityGroup
```

Podsieć jest teraz dodany wewnątrz sieci wirtualnej i skojarzonych z grupy zabezpieczeń sieci i reguły.


## <a name="add-a-vnic-to-the-subnet"></a>Dodaj VNic do podsieci

Wirtualne karty sieciowe (VNics) są istotne, ponieważ użytkownik może korzystać z nich łącząc je do różnych maszyn wirtualnych. Takie podejście zapewnia VNic jako zasób statycznych maszyn wirtualnych mogą być tymczasowe. Utwórz VNic i skojarzyć go z podsiecią utworzony w poprzednim kroku.

```azurecli
azure network nic create myVNic \
    --resource-group myResourceGroup \
    --location eastus \
    ---subnet-vnet-name myVNet \
    --subnet-name mySubNet
```

## <a name="deploy-the-vm-into-the-vnet-and-nsg"></a>Wdróż maszynę Wirtualną do sieci wirtualnej i grupy NSG

Istnieje już sieć wirtualną i podsieci w tej sieci wirtualnej, a grupa zabezpieczeń sieci w celu ochrony podsieci blokuje cały ruch przychodzący z wyjątkiem port 22 dla protokołu SSH. Teraz można wdrożyć maszyny Wirtualnej w tym istniejącej infrastruktury sieci.

Przy użyciu interfejsu wiersza polecenia Azure i `azure vm create` polecenia do istniejącej grupy zasobów platformy Azure, sieci wirtualnej, podsieci i VNic wdrożeniu maszyny Wirtualnej systemu Linux. Aby uzyskać więcej informacji na instalację pełną maszyny Wirtualnej za pomocą interfejsu wiersza polecenia, zobacz [tworzyć kompletne środowisko systemu Linux przy użyciu wiersza polecenia platformy Azure](create-cli-complete.md)

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

Za pomocą flag interfejsu wiersza polecenia do wyróżnienia istniejących zasobów, można nakazać Azure, aby wdrożyć maszynę Wirtualną w istniejącej sieci. Po wdrożeniu sieci wirtualnej i podsieci, możesz je zostawić jako statyczne ani stałe zasoby w Twoim regionie Azure.  

## <a name="next-steps"></a>Następne kroki

* [Tworzenie konkretnego wdrożenia za pomocą szablonu usługi Azure Resource Manager](../windows/cli-deploy-templates.md)
* [Tworzenie niestandardowego środowiska dla maszyny wirtualnej z systemem Linux poprzez bezpośrednie użycie poleceń interfejsu wiersza polecenia platformy Azure](create-cli-complete.md)
* [Utwórz Maszynę wirtualną systemu Linux na platformie Azure za pomocą szablonów](create-ssh-secured-vm-from-template.md)
