---
title: "aaaDeploy maszyn wirtualnych systemu Linux w istniejącej sieci Azure CLI 2.0 | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toodeploy maszynę wirtualną systemu Linux do istniejącej sieci wirtualnej przy użyciu hello Azure CLI 2.0"
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
ms.openlocfilehash: 0df44b3437002df050db56f3b3899083fb49d803
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toodeploy-a-linux-virtual-machine-into-an-existing-azure-virtual-network-with-hello-azure-cli"></a>Jak toodeploy maszyny wirtualnej systemu Linux w istniejącej sieci wirtualnej platformy Azure z hello wiersza polecenia platformy Azure

W tym artykule opisano sposób toouse hello Azure CLI 2.0 toodeploy maszynę wirtualną (VM) do istniejącej sieci wirtualnej. wymagania dotyczące Hello są:

- [Konto platformy Azure](https://azure.microsoft.com/pricing/free-trial/)
- [Pliki kluczy publicznych i prywatnych SSH](mac-create-ssh-keys.md)

Można również wykonać te kroki hello [Azure CLI 1.0](deploy-linux-vm-into-existing-vnet-using-cli-nodejs.md).


## <a name="quick-commands"></a>Szybkie polecenia
Jeśli potrzebujesz tooquickly hello zadania, powitania po sekcji Szczegóły poleceń hello potrzebne. Bardziej szczegółowe informacje i kontekst dla każdego kroku można znaleźć hello pozostałej części dokumentu hello [uruchamiania tutaj](#detailed-walkthrough).

toocreate to środowisko niestandardowe, należy hello jest najnowsza wersja [Azure CLI 2.0](/cli/azure/install-az-cli2) zainstalowane i zarejestrowane za pomocą konta Azure tooan [logowania az](/cli/azure/#login).

Poniższe przykłady w hello Zastąp przykładowe nazwy parametrów własne wartości. Przykład nazwy parametru zawierają *myResourceGroup*, *myVnet*, i *myVM*.

**Wymagania wstępne:** grupy zasobów platformy Azure, sieci wirtualnych i podsieci ruchu przychodzącego grupy zabezpieczeń sieci przy użyciu protokołu SSH i karty interfejsu sieci wirtualnej.

### <a name="deploy-hello-vm-into-hello-virtual-network-infrastructure"></a>Wdrażanie hello maszyny Wirtualnej do hello infrastruktury sieci wirtualnej

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

Azure zasoby, takie jak sieci wirtualnych i grup zabezpieczeń sieci musi być statyczny i tam długo zasoby, które rzadko są wdrożone. Po wdrożeniu sieci wirtualnej można użyć ponownie przez nowych wdrożeń bez żadnych infrastruktury toohello niekorzystny wpływ. Pomyśleć o sieci wirtualnej jako przełącznik sieciowy tradycyjnych sprzętu — tooconfigure nowego sprzętu przełącznik z każdego wdrożenia nie jest wymagane. Z sieci wirtualnej prawidłowo skonfigurowany, można kontynuować toodeploy nowych maszyn wirtualnych w tej sieci wirtualnej samodzielnego z kilku, ewentualne zmiany wymagane na okres hello hello sieci wirtualnej.

toocreate to środowisko niestandardowe, należy hello jest najnowsza wersja [Azure CLI 2.0](/cli/azure/install-az-cli2) zainstalowane i zarejestrowane za pomocą konta Azure tooan [logowania az](/cli/azure/#login).

Poniższe przykłady w hello Zastąp przykładowe nazwy parametrów własne wartości. Przykład nazwy parametru zawierają *myResourceGroup*, *myVnet*, i *myVM*.

## <a name="create-hello-resource-group"></a>Utwórz grupę zasobów hello

Najpierw utwórz tooorganize grupy zasobów platformy Azure wszystko, czego możesz utworzyć w tym przewodniku. Więcej informacji na temat grup zasobów znajduje się w temacie [Omówienie usługi Azure Resource Manager](../../azure-resource-manager/resource-group-overview.md). Utwórz grupę zasobów hello z [Tworzenie grupy az](/cli/azure/group#create). Witaj poniższy przykład tworzy grupę zasobów o nazwie *myResourceGroup* w hello *eastus* lokalizacji:

```azurecli
az group create \
    --name myResourceGroup \
    --location eastus
```

## <a name="create-hello-virtual-network"></a>Utwórz sieć wirtualną hello

Umożliwia tworzenie maszyn wirtualnych do hello toolaunch sieci wirtualnej platformy Azure. Aby uzyskać więcej informacji o sieciach wirtualnych, zobacz [utworzyć sieć wirtualną przy użyciu interfejsu wiersza polecenia Azure hello](../../virtual-network/virtual-networks-create-vnet-arm-cli.md). Utwórz sieć wirtualną hello z [tworzenie sieci wirtualnej sieci az](/cli/azure/network/vnet#create). Witaj poniższy przykład tworzy sieć wirtualną o nazwie *myVnet* i podsieć o nazwie *mySubnet*:

```azurecli
az network vnet create \
    --resource-group myResourceGroup \
    --location eastus \
    --name myVnet \
    --address-prefix 10.10.0.0/16 \
    --subnet-name mySubnet \
    --subnet-prefix 10.10.1.0/24
```

## <a name="create-hello-network-security-group"></a>Utwórz grupę zabezpieczeń sieci hello

Grupy zabezpieczeń sieci platformy Azure są równoważne tooa zapory na powitania warstwy sieci. Aby uzyskać więcej informacji dotyczących grup zabezpieczeń sieci, zobacz [jak grupy zabezpieczeń sieci toocreate w hello Azure CLI](../../virtual-network/virtual-networks-create-nsg-arm-cli.md). Utwórz grupę zabezpieczeń sieci hello z [utworzyć nsg sieci az](/cli/azure/network/nsg#create). Witaj poniższy przykład tworzy sieciową grupę zabezpieczeń o nazwie *myNetworkSecurityGroup*:

```azurecli
az network nsg create \
    --resource-group myResourceGroup \
    --location eastus \
    --name myNetworkSecurityGroup
```

## <a name="add-an-inbound-ssh-allow-rule"></a>Dodaj regułę Zezwalaj SSH dla ruchu przychodzącego

Witaj maszyna wirtualna musi mieć dostęp z hello internet, więc regułę zezwalającą na toobe ruch przychodzący port 22 przekazywane hello sieci tooport 22 na powitania maszyny Wirtualnej jest wymagana. Dodaj regułę ruchu przychodzącego dla sieciowej grupy zabezpieczeń z hello [Tworzenie reguły nsg sieci az](/cli/azure/network/nsg/rule#create). Witaj poniższy przykład powoduje utworzenie reguły o nazwie *myNetworkSecurityGroupRuleSSH*:

```azurecli
az network nsg rule create \
    --resource-group myResourceGroup \
    --nsg-name myNetworkSecurityGroup \
    --name myNetworkSecurityGroupRuleSSH \
    --priority 1000 \
    --protocol tcp \
    --destination-port-range 22 \
```

## <a name="attach-hello-subnet-toohello-network-security-group"></a>Dołącz hello podsieci toohello sieciowej grupy zabezpieczeń

reguły grupy zabezpieczeń sieci Hello może być zastosowane tooa podsieci lub interfejs określonej sieci wirtualnej. Umożliwia dołączanie tooour hello podsieci zabezpieczeń grupy. Dołącz grupy zabezpieczeń sieci toohello podsieci z [zaktualizować podsieci sieci wirtualnej sieci az](/cli/azure/network/vnet/subnet#update):

```azurecli
az network vnet subnet update \
    --resource-group myResourceGroup \
    --vnet-name myVnet \
    --name mySubnet \
    --network-security-group myNetworkSecurityGroup
```

## <a name="add-a-virtual-network-interface-card-toohello-subnet"></a>Dodaj podsieć toohello karty interfejsu sieci wirtualnej

Karty interfejsu sieci wirtualnej (VNics) są ważne, ponieważ późniejszego łącząc je toodifferent maszyn wirtualnych. Ta ponownemu pozwala tookeep hello VNic jako zasób statycznych hello maszyny wirtualne mogą być tymczasowe. Utwórz VNic i powiązać ją z podsiecią hello z [tworzenie kart interfejsu sieciowego az](/cli/azure/network/nic#create). Witaj poniższy przykład tworzy VNic, o nazwie *myNic*:

```azurecli
az network nic create \
    --resource-group myResourceGroup \
    --location eastus \
    --name myNic \
    --vnet-name myVnet \
    --subnet mySubnet
```

## <a name="deploy-hello-vm-into-hello-virtual-network-infrastructure"></a>Wdrażanie hello maszyny Wirtualnej do hello infrastruktury sieci wirtualnej

Istnieje już sieć wirtualną i podsieć i podsieć hello tooprotect grupy zabezpieczeń sieci przez blokuje cały ruch przychodzący z wyjątkiem port 22 dla protokołu SSH. Teraz można wdrożyć Hello maszyny Wirtualnej w tym istniejącej infrastruktury sieci.

Tworzenie maszyny Wirtualnej z [tworzenia maszyny wirtualnej az](/cli/azure/vm#create). Aby uzyskać więcej informacji na temat hello flagi toouse z toodeploy hello Azure CLI 2.0 pełną maszyny Wirtualnej, zobacz [tworzyć kompletne środowisko systemu Linux przy użyciu interfejsu wiersza polecenia Azure hello](create-cli-complete.md).

Witaj poniższy przykład tworzy Maszynę wirtualną za pomocą dysków zarządzanych platformy Azure. Te dyski są obsługiwane przez hello platformy Azure i nie wymagają żadnych toostore przygotowania lub lokalizacji je. Aby uzyskać więcej informacji o dyskach zarządzanych, zobacz [Omówienie usługi Azure Managed Disks](../../storage/storage-managed-disks-overview.md). Jeśli chcesz, aby dyski toouse niezarządzanych, zobacz hello dodatkowe Uwaga poniżej.

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --image Debian \
    --admin-username azureuser \
    --generate-ssh-keys \
    --nics myNic
```

Użycie dysków zarządzanych, Pomiń ten krok. Jeśli chcesz, aby dyski toouse niezarządzanych, należy hello tooadd następujące dodatkowe parametry toohello postępowania polecenia toocreate niezarządzanych dysków w hello konto magazynu o nazwie `mystorageaccount`: 

```azurecli
    --use-unmanaged-disk \
    --storage-account mystorageaccount
```

Za pomocą hello interfejsu wiersza polecenia flagi toocall limit istniejących zasobów, poinstruuj hello Azure toodeploy VM wewnątrz hello istniejącej sieci. Po wdrożeniu sieci wirtualnej i podsieci, możesz je zostawić jako statyczne ani stałe zasoby w Twoim regionie Azure. W tym przykładzie nie Utwórz i przypisz publicznego toohello adresu IP wirtualnej karty sieciowej, dlatego ta maszyna wirtualna nie jest dostępny publicznie za pośrednictwem Internetu hello. Aby uzyskać więcej informacji, zobacz [utworzyć Maszynę wirtualną z statycznego publicznego adresu IP za pomocą interfejsu wiersza polecenia Azure hello](../../virtual-network/virtual-network-deploy-static-pip-arm-cli.md).

## <a name="next-steps"></a>Następne kroki
Aby uzyskać więcej informacji o maszynach wirtualnych toocreate sposoby na platformie Azure zobacz następujące zasoby hello:

* [Użyj toocreate szablonu usługi Azure Resource Manager określonego wdrożenia](../windows/cli-deploy-templates.md)
* [Tworzenie niestandardowego środowiska dla maszyny wirtualnej z systemem Linux poprzez bezpośrednie użycie poleceń interfejsu wiersza polecenia platformy Azure](create-cli-complete.md)
* [Utwórz Maszynę wirtualną systemu Linux na platformie Azure za pomocą szablonów](create-ssh-secured-vm-from-template.md)
