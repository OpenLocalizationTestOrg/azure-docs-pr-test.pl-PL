---
title: "aaaUse wewnętrzny serwer DNS dla maszyny Wirtualnej do rozpoznawania nazw z hello Azure CLI 2.0 | Dokumentacja firmy Microsoft"
description: "Jak sieci wirtualnej toocreate kartami interfejsu i korzystania z wewnętrznego serwera DNS do rozpoznawania nazw maszyny Wirtualnej na platformie Azure z hello Azure CLI 2.0"
services: virtual-machines-linux
documentationcenter: 
author: vlivech
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: azurecli
ms.topic: article
ms.date: 02/16/2017
ms.author: v-livech
ms.openlocfilehash: b3c4bfd3ab698f7b25d763ba9e60dd7984f6269d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-virtual-network-interface-cards-and-use-internal-dns-for-vm-name-resolution-on-azure"></a>Tworzenie karty interfejsu sieci wirtualnej i korzystania z wewnętrznego serwera DNS do rozpoznawania nazw maszyny Wirtualnej na platformie Azure
W tym artykule opisano, jak tooset statyczne wewnętrzne nazwy DNS dla maszyn wirtualnych systemu Linux przy użyciu wirtualnej sieci karty interfejsu (vNics) i nazwy etykiety DNS z hello Azure CLI 2.0. Można również wykonać te kroki hello [Azure CLI 1.0](static-dns-name-resolution-for-linux-on-azure-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json). Statyczne nazwy DNS są używane dla usług trwałych infrastruktury, takich jak serwer kompilacji Wpięć, który służy do tego dokumentu lub serwer Git.

wymagania dotyczące Hello są:

* [Konto platformy Azure](https://azure.microsoft.com/pricing/free-trial/)
* [Pliki kluczy publicznych i prywatnych SSH](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

## <a name="quick-commands"></a>Szybkie polecenia
Jeśli potrzebujesz tooquickly hello zadania, powitania po sekcji Szczegóły poleceń hello potrzebne. Bardziej szczegółowe informacje i kontekst dla każdego kroku można znaleźć w hello pozostałej części dokumentu hello [uruchamiania tutaj](#detailed-walkthrough). tooperform tych kroków, należy hello najnowszych [Azure CLI 2.0](/cli/azure/install-az-cli2) zainstalowane i zarejestrowane za pomocą konta Azure tooan [logowania az](/cli/azure/#login).

Wymagania Wstępne: Grupy zasobów, sieć wirtualną i podsieć, grupy zabezpieczeń sieci przy użyciu protokołu SSH ruchu przychodzącego.

### <a name="create-a-virtual-network-interface-card-with-a-static-internal-dns-name"></a>Utwórz karty interfejsu sieci wirtualnej o nazwie DNS wewnętrzny statycznej
Utwórz vNic hello z [tworzenie kart interfejsu sieciowego az](/cli/azure/network/nic#create). Witaj `--internal-dns-name` Flaga interfejsu wiersza polecenia jest ustawienie hello DNS etykiety, który zapewnia hello statycznej nazwy DNS dla karty interfejsu sieci wirtualnej hello (vNic). Witaj poniższy przykład tworzy vNic, o nazwie `myNic`, połączony toohello `myVnet` sieci wirtualnej i tworzy wewnętrzny rekordu nazwy DNS nazywanego `jenkins`:

```azurecli
az network nic create \
    --resource-group myResourceGroup \
    --name myNic \
    --vnet-name myVnet \
    --subnet mySubnet \
    --internal-dns-name jenkins
```

### <a name="deploy-a-vm-and-connect-hello-vnic"></a>Wdróż Maszynę wirtualną i połączyć hello vNic
Utwórz maszynę wirtualną za pomocą polecenia [az vm create](/cli/azure/vm#create). Witaj `--nics` flagi łączy hello vNic toohello maszyny Wirtualnej podczas hello tooAzure wdrożenia. Witaj poniższy przykład tworzy Maszynę wirtualną o nazwie `myVM` z dyskami zarządzane Azure i dołącza hello vNic o nazwie `myNic` z hello poprzedzających krok:

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --nics myNic \
    --image UbuntuLTS \
    --admin-username azureuser \
    --ssh-key-value ~/.ssh/id_rsa.pub
```

## <a name="detailed-walkthrough"></a>Szczegółowy przewodnik

Pełne ciągłej integracji i ciągłe wdrażanie (CiCd) infrastruktury na platformie Azure wymaga niektórych toobe statyczne lub długotrwałe serwery. Zaleca się, że Azure zasoby, takie jak hello sieci wirtualnych i sieciowe grupy zabezpieczeń są statyczne i tam długo zasoby, które rzadko są wdrożone. Po wdrożeniu sieci wirtualnej można użyć ponownie przez nowych wdrożeń bez żadnych infrastruktury toohello niekorzystny wpływ. Później można dodać serwer repozytorium Git lub serwer automatyzacji Wpięć dostarcza CiCd toothis sieci wirtualnej środowiska deweloperskich lub testowania.  

Wewnętrzny nazw DNS są tylko rozpoznawany w sieci wirtualnej platformy Azure. Ponieważ nazwy DNS hello są wewnętrzne, nie są one rozpoznawalną toohello poza internet, zapewniając dodatkowe zabezpieczenia toohello infrastruktury.

Poniższe przykłady w hello Zastąp przykładowe nazwy parametrów własne wartości. Przykład nazwy parametru zawierają `myResourceGroup`, `myNic`, i `myVM`.

## <a name="create-hello-resource-group"></a>Utwórz grupę zasobów hello
Najpierw należy utworzyć grupy zasobów hello z [Tworzenie grupy az](/cli/azure/group#create). Witaj poniższy przykład tworzy grupę zasobów o nazwie `myResourceGroup` w hello `westus` lokalizacji:

```azurecli
az group create --name myResourceGroup --location westus
```

## <a name="create-hello-virtual-network"></a>Utwórz sieć wirtualną hello

Witaj następnym krokiem jest toobuild maszyn wirtualnych do hello toolaunch sieci wirtualnej. sieć wirtualna Hello zawiera jedną podsieć w ramach tego przewodnika. Aby uzyskać więcej informacji o sieci wirtualnych platformy Azure, zobacz [utworzyć sieć wirtualną przy użyciu interfejsu wiersza polecenia Azure hello](../../virtual-network/virtual-networks-create-vnet-arm-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json). 

Utwórz sieć wirtualną hello z [tworzenie sieci wirtualnej sieci az](/cli/azure/network/vnet#create). Witaj poniższy przykład tworzy sieć wirtualną o nazwie `myVnet` i podsieć o nazwie `mySubnet`:

```azurecli
az network vnet create \
    --resource-group myResourceGroup \
    --name myVnet \
    --address-prefix 192.168.0.0/16 \
    --subnet-name mySubnet \
    --subnet-prefix 192.168.1.0/24
```

## <a name="create-hello-network-security-group"></a>Utwórz hello grupy zabezpieczeń sieci
Grupy zabezpieczeń sieci platformy Azure są równoważne tooa zapory na powitania warstwy sieci. Aby uzyskać więcej informacji na temat grup zabezpieczeń sieci, zobacz [jak grupy NSG toocreate w hello Azure CLI](../../virtual-network/virtual-networks-create-nsg-arm-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json). 

Utwórz grupę zabezpieczeń sieci hello z [utworzyć nsg sieci az](/cli/azure/network/nsg#create). Witaj poniższy przykład tworzy sieciową grupę zabezpieczeń o nazwie `myNetworkSecurityGroup`:

```azurecli
az network nsg create \
    --resource-group myResourceGroup \
    --name myNetworkSecurityGroup
```

## <a name="add-an-inbound-rule-tooallow-ssh"></a>Dodaj regułę ruchu przychodzącego tooallow SSH
Dodaj regułę ruchu przychodzącego dla sieciowej grupy zabezpieczeń z hello [Tworzenie reguły nsg sieci az](/cli/azure/network/nsg/rule#create). Witaj poniższy przykład powoduje utworzenie reguły o nazwie `myRuleAllowSSH`:

```azurecli
az network nsg rule create \
    --resource-group myResourceGroup \
    --nsg-name myNetworkSecurityGroup \
    --name myRuleAllowSSH \
    --protocol tcp \
    --direction inbound \
    --priority 1000 \
    --source-address-prefix '*' \
    --source-port-range '*' \
    --destination-address-prefix '*' \
    --destination-port-range 22 \
    --access allow
```

## <a name="associate-hello-subnet-with-hello-network-security-group"></a>Podsieć hello skojarzona z hello grupy zabezpieczeń sieci
podsieć hello tooassociate z hello sieciowej grupy zabezpieczeń, użyj [zaktualizować podsieci sieci wirtualnej sieci az](/cli/azure/network/vnet/subnet#update). Witaj poniższy przykład powoduje skojarzenie nazwy podsieci hello `mySubnet` z hello sieciową grupę zabezpieczeń o nazwie `myNetworkSecurityGroup`:

```azurecli
az network vnet subnet update \
    --resource-group myResourceGroup \
    --vnet-name myVnet \
    --name mySubnet \
    --network-security-group myNetworkSecurityGroup
```


## <a name="create-hello-virtual-network-interface-card-and-static-dns-names"></a>Utwórz statycznej nazwy DNS i hello wirtualnej karty sieciowej
Platforma Azure jest bardzo elastyczne, ale toouse nazwy DNS dla rozpoznawania nazw maszyny Wirtualnej, należy toocreate wirtualne karty sieciowe (vNics) zawierających etykietę DNS. vNics są ważne, ponieważ późniejszego przez połączenie ich maszyn wirtualnych toodifferent cyklem hello infrastruktury. Takie podejście zapewnia hello vNic jako zasób statycznych hello maszyny wirtualne mogą być tymczasowe. Przy użyciu systemu DNS etykietowania na karcie vNic hello, możemy rozpoznawania nazw proste stanie tooenable z innych maszyn wirtualnych w hello sieci wirtualnej. Przy użyciu nazwy rozpoznawalną umożliwia inny serwer automatyzacji hello tooaccess maszyn wirtualnych na podstawie nazwy DNS hello `Jenkins` lub na serwerze Git hello `gitrepo`.  

Utwórz vNic hello z [tworzenie kart interfejsu sieciowego az](/cli/azure/network/nic#create). Witaj poniższy przykład tworzy vNic, o nazwie `myNic`, połączony toohello `myVnet` sieci wirtualnej o nazwie `myVnet`i tworzy wewnętrzny rekordu nazwy DNS nazywanego `jenkins`:

```azurecli
az network nic create \
    --resource-group myResourceGroup \
    --name myNic \
    --vnet-name myVnet \
    --subnet mySubnet \
    --internal-dns-name jenkins
```

## <a name="deploy-hello-vm-into-hello-virtual-network-infrastructure"></a>Wdrażanie hello maszyny Wirtualnej do hello infrastruktury sieci wirtualnej
Mamy teraz sieć wirtualna i podsieć, działając jako tooprotect zapory naszych podsieci blokuje cały ruch przychodzący z wyjątkiem port 22 protokołu SSH i vNic grupa zabezpieczeń sieci. Teraz można wdrożyć maszyny Wirtualnej w tym istniejącej infrastruktury sieci.

Utwórz maszynę wirtualną za pomocą polecenia [az vm create](/cli/azure/vm#create). Witaj poniższy przykład tworzy Maszynę wirtualną o nazwie `myVM` z dyskami zarządzane Azure i dołącza hello vNic o nazwie `myNic` z hello poprzedzających krok:

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --nics myNic \
    --image UbuntuLTS \
    --admin-username azureuser \
    --ssh-key-value ~/.ssh/id_rsa.pub
```

Za pomocą hello interfejsu wiersza polecenia flagi toocall limit istniejących zasobów, firma Microsoft poinstruować hello Azure toodeploy VM wewnątrz hello istniejącej sieci. tooreiterate, po wdrożeniu sieci wirtualnej i podsieci, ich może pozostać statyczne ani stałe zasobów w Twoim regionie Azure.  

## <a name="next-steps"></a>Następne kroki
* [Tworzenie niestandardowego środowiska dla maszyny wirtualnej z systemem Linux poprzez bezpośrednie użycie poleceń interfejsu wiersza polecenia platformy Azure](create-cli-complete.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [Utwórz Maszynę wirtualną systemu Linux na platformie Azure za pomocą szablonów](create-ssh-secured-vm-from-template.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
