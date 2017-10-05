---
title: "Wdrażanie maszyn wirtualnych systemu Linux w istniejącej sieci Azure CLI 2.0 | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak wdrożyć maszynę wirtualną systemu Linux w ramach istniejącej sieci wirtualnej przy użyciu 2.0 interfejsu wiersza polecenia platformy Azure"
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
ms.devlang: azurecli
ms.topic: article
ms.date: 05/11/2017
ms.author: iainfou
ms.openlocfilehash: 932fd74ec83f43b604382346ee2c273f5453fcd0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-deploy-a-linux-virtual-machine-into-an-existing-azure-virtual-network-with-the-azure-cli"></a>Jak wdrożyć maszyny wirtualnej systemu Linux w istniejącej sieci wirtualnej platformy Azure z wiersza polecenia platformy Azure

W tym artykule przedstawiono sposób użycia 2.0 interfejsu wiersza polecenia Azure, aby wdrożyć maszynę wirtualną (VM) do istniejącej sieci wirtualnej. Wymagania są następujące:

- [Konto platformy Azure](https://azure.microsoft.com/pricing/free-trial/)
- [Pliki kluczy publicznych i prywatnych SSH](mac-create-ssh-keys.md)

Czynności te można również wykonać przy użyciu [interfejsu wiersza polecenia platformy Azure w wersji 1.0](deploy-linux-vm-into-existing-vnet-using-cli-nodejs.md).


## <a name="quick-commands"></a>Szybkie polecenia
Jeśli chcesz szybko wykonywać zadania poniższej sekcji Szczegóły poleceń potrzebne. Bardziej szczegółowe informacje i kontekst dla każdego kroku można znaleźć pozostałej części dokumentu, [uruchamiania tutaj](#detailed-walkthrough).

Do utworzenia tego środowiska niestandardowe, należy najnowszej [Azure CLI 2.0](/cli/azure/install-az-cli2) zainstalowane i zalogowany do konta platformy Azure przy użyciu [logowania az](/cli/azure/#login).

W poniższych przykładach Zastąp przykładowe nazwy parametrów własne wartości. Przykład nazwy parametru zawierają *myResourceGroup*, *myVnet*, i *myVM*.

**Wymagania wstępne:** grupy zasobów platformy Azure, sieci wirtualnych i podsieci ruchu przychodzącego grupy zabezpieczeń sieci przy użyciu protokołu SSH i karty interfejsu sieci wirtualnej.

### <a name="deploy-the-vm-into-the-virtual-network-infrastructure"></a>Wdróż maszynę Wirtualną do infrastruktury sieci wirtualnej

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --image Debian \
    --admin-username azureuser \
    --generate-ssh-keys \
    --nics myNic
```

## <a name="detailed-walkthrough"></a>Szczegółowy przewodnik

Azure zasoby, takie jak sieci wirtualnych i grup zabezpieczeń sieci musi być statyczny i tam długo zasoby, które rzadko są wdrożone. Po wdrożeniu sieci wirtualnej można użyć ponownie przez nowych wdrożeń bez żadnych niekorzystny wpływ infrastruktury. Pomyśleć o sieci wirtualnej jako przełącznik sieciowy tradycyjnych sprzętu — nie musisz skonfigurować nowy przełącznik sprzętu z każdym wdrożeniu. Z sieci wirtualnej prawidłowo skonfigurowany można wdrożyć nowe maszyny wirtualne w tej sieci wirtualnej samodzielnego z kilku ewentualne zmiany wymagane w całej sieci wirtualnej.

Do utworzenia tego środowiska niestandardowe, należy najnowszej [Azure CLI 2.0](/cli/azure/install-az-cli2) zainstalowane i zalogowany do konta platformy Azure przy użyciu [logowania az](/cli/azure/#login).

W poniższych przykładach Zastąp przykładowe nazwy parametrów własne wartości. Przykład nazwy parametru zawierają *myResourceGroup*, *myVnet*, i *myVM*.

## <a name="create-the-resource-group"></a>Tworzenie grupy zasobów

Najpierw należy utworzyć grupy zasobów platformy Azure do organizowania wszystko, czego możesz utworzyć w tym przewodniku. Więcej informacji na temat grup zasobów znajduje się w temacie [Omówienie usługi Azure Resource Manager](../../azure-resource-manager/resource-group-overview.md). Tworzenie grupy zasobów z [Tworzenie grupy az](/cli/azure/group#create). Poniższy przykład tworzy grupę zasobów o nazwie *myResourceGroup* w *eastus* lokalizacji:

```azurecli
az group create \
    --name myResourceGroup \
    --location eastus
```

## <a name="create-the-virtual-network"></a>Utwórz sieć wirtualną

Umożliwia tworzenie sieci wirtualnej platformy Azure, można uruchomić na maszynach wirtualnych. Aby uzyskać więcej informacji o sieciach wirtualnych, zobacz [utworzyć sieć wirtualną przy użyciu interfejsu wiersza polecenia Azure](../../virtual-network/virtual-networks-create-vnet-arm-cli.md). Utwórz sieć wirtualną z [tworzenie sieci wirtualnej sieci az](/cli/azure/network/vnet#create). Poniższy przykład tworzy sieć wirtualną o nazwie *myVnet* i podsieć o nazwie *mySubnet*:

```azurecli
az network vnet create \
    --resource-group myResourceGroup \
    --location eastus \
    --name myVnet \
    --address-prefix 10.10.0.0/16 \
    --subnet-name mySubnet \
    --subnet-prefix 10.10.1.0/24
```

## <a name="create-the-network-security-group"></a>Utwórz grupę zabezpieczeń sieci

Grupy zabezpieczeń sieci platformy Azure są równoważne zapory w warstwie sieci. Aby uzyskać więcej informacji dotyczących grup zabezpieczeń sieci, zobacz [sposobu tworzenia grup zabezpieczeń sieci na platformie Azure CLI](../../virtual-network/virtual-networks-create-nsg-arm-cli.md). Utwórz grupę zabezpieczeń sieci z [utworzyć nsg sieci az](/cli/azure/network/nsg#create). Poniższy przykład tworzy sieciową grupę zabezpieczeń o nazwie *myNetworkSecurityGroup*:

```azurecli
az network nsg create \
    --resource-group myResourceGroup \
    --location eastus \
    --name myNetworkSecurityGroup
```

## <a name="add-an-inbound-ssh-allow-rule"></a>Dodaj regułę Zezwalaj SSH dla ruchu przychodzącego

Maszyna wirtualna wymaga dostępu z Internetu, więc regułę zezwalającą na ruch przychodzący port 22 mają być przekazywane za pośrednictwem sieci do portu 22 na maszynie Wirtualnej nie jest wymagane. Dodaj regułę ruchu przychodzącego dla sieciowej grupy zabezpieczeń z [Tworzenie reguły nsg sieci az](/cli/azure/network/nsg/rule#create). Poniższy przykład tworzy reguły o nazwie *myNetworkSecurityGroupRuleSSH*:

```azurecli
az network nsg rule create \
    --resource-group myResourceGroup \
    --nsg-name myNetworkSecurityGroup \
    --name myNetworkSecurityGroupRuleSSH \
    --priority 1000 \
    --protocol tcp \
    --destination-port-range 22 \
```

## <a name="attach-the-subnet-to-the-network-security-group"></a>Dołącz podsieci do grupy zabezpieczeń sieci

Reguły grupy zabezpieczeń sieci może odnosić się do podsieci lub interfejs określonej sieci wirtualnej. Umożliwia dołączanie sieciowej grupy zabezpieczeń do naszej podsieci. Dołącz do sieciowej grupy zabezpieczeń z podsieci [zaktualizować podsieci sieci wirtualnej sieci az](/cli/azure/network/vnet/subnet#update):

```azurecli
az network vnet subnet update \
    --resource-group myResourceGroup \
    --vnet-name myVnet \
    --name mySubnet \
    --network-security-group myNetworkSecurityGroup
```

## <a name="add-a-virtual-network-interface-card-to-the-subnet"></a>Dodaj do karty interfejsu sieci wirtualnej do podsieci

Karty interfejsu sieci wirtualnej (VNics) są istotne, ponieważ użytkownik może korzystać z nich łącząc je do różnych maszyn wirtualnych. Ta ponownemu pozwala na zachowanie VNic jako zasób statycznych, maszyny wirtualne mogą być tymczasowe. Utwórz VNic i powiązać ją z podsieci o [tworzenie kart interfejsu sieciowego az](/cli/azure/network/nic#create). Poniższy przykład tworzy VNic, o nazwie *myNic*:

```azurecli
az network nic create \
    --resource-group myResourceGroup \
    --location eastus \
    --name myNic \
    --vnet-name myVnet \
    --subnet mySubnet
```

## <a name="deploy-the-vm-into-the-virtual-network-infrastructure"></a>Wdróż maszynę Wirtualną do infrastruktury sieci wirtualnej

Istnieje już sieć wirtualną i podsieć i sieciową grupę zabezpieczeń do ochrony przez blokuje cały ruch przychodzący z wyjątkiem port 22 SSH podsieci. Teraz można wdrożyć maszyny Wirtualnej w tym istniejącej infrastruktury sieci.

Tworzenie maszyny Wirtualnej z [tworzenia maszyny wirtualnej az](/cli/azure/vm#create). Aby uzyskać więcej informacji o flagach do użycia z 2.0 interfejsu wiersza polecenia platformy Azure, aby wdrożyć Maszynę wirtualną pełną, zobacz [tworzyć kompletne środowisko systemu Linux przy użyciu interfejsu wiersza polecenia Azure](create-cli-complete.md).

Poniższy przykład tworzy Maszynę wirtualną za pomocą dysków zarządzanych platformy Azure. Te dyski są obsługiwane przez platformę Azure i nie wymagają wszystkie lub lokalizację do przechowywania ich. Aby uzyskać więcej informacji o dyskach zarządzanych, zobacz [Omówienie usługi Azure Managed Disks](../../storage/storage-managed-disks-overview.md). Jeśli chcesz używać dysków niezarządzane, zobacz Uwagi dodatkowe poniżej.

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --image Debian \
    --admin-username azureuser \
    --generate-ssh-keys \
    --nics myNic
```

Użycie dysków zarządzanych, Pomiń ten krok. Jeśli chcesz używać dysków niezarządzane, należy dodać następujące dodatkowe parametry do polecenia postępowania w celu tworzenia niezarządzanej dysków na koncie magazynu o nazwie `mystorageaccount`: 

```azurecli
    --use-unmanaged-disk \
    --storage-account mystorageaccount
```

Za pomocą flag interfejsu wiersza polecenia do wyróżnienia istniejących zasobów, można nakazać Azure, aby wdrożyć maszynę Wirtualną w istniejącej sieci. Po wdrożeniu sieci wirtualnej i podsieci, możesz je zostawić jako statyczne ani stałe zasoby w Twoim regionie Azure. W tym przykładzie jest nie utworzyć i przypisać publicznego adresu IP wirtualnej karty sieciowej, więc ta maszyna wirtualna nie jest dostępny publicznie w Internecie. Aby uzyskać więcej informacji, zobacz [utworzyć Maszynę wirtualną z statycznego publicznego adresu IP za pomocą interfejsu wiersza polecenia Azure](../../virtual-network/virtual-network-deploy-static-pip-arm-cli.md).

## <a name="next-steps"></a>Następne kroki
Aby uzyskać więcej informacji o sposobach tworzenia maszyn wirtualnych na platformie Azure zobacz następujące zasoby:

* [Tworzenie konkretnego wdrożenia za pomocą szablonu usługi Azure Resource Manager](../windows/cli-deploy-templates.md)
* [Tworzenie niestandardowego środowiska dla maszyny wirtualnej z systemem Linux poprzez bezpośrednie użycie poleceń interfejsu wiersza polecenia platformy Azure](create-cli-complete.md)
* [Utwórz Maszynę wirtualną systemu Linux na platformie Azure za pomocą szablonów](create-ssh-secured-vm-from-template.md)
