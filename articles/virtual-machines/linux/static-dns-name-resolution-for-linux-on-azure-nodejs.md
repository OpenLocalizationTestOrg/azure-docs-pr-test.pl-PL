---
title: "aaaUsing wewnętrzny serwer DNS dla maszyny Wirtualnej do rozpoznawania nazw na platformie Azure | Dokumentacja firmy Microsoft"
description: "Przy użyciu wewnętrznego serwera DNS do rozpoznawania nazw maszyny Wirtualnej na platformie Azure."
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
ms.devlang: na
ms.topic: article
ms.date: 12/05/2016
ms.author: v-livech
ms.openlocfilehash: 94fd6577aa51ce5db4dc26649b415ddeeb410eb6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="using-internal-dns-for-vm-name-resolution-on-azure"></a>Przy użyciu wewnętrznego serwera DNS do rozpoznawania nazw maszyny Wirtualnej na platformie Azure

W tym artykule przedstawiono sposób tooset statycznych wewnętrzny serwer DNS nazwy dla maszyn wirtualnych systemu Linux przy użyciu karty wirtualnej karty Sieciowej (VNic) i nazwy etykiety DNS. Statyczne nazwy DNS są używane dla usług trwałych infrastruktury, takich jak serwer kompilacji Wpięć, który służy do tego dokumentu lub serwer Git.

wymagania dotyczące Hello są:

* [Konto platformy Azure](https://azure.microsoft.com/pricing/free-trial/)
* [Pliki kluczy publicznych i prywatnych SSH](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)


## <a name="cli-versions-toocomplete-hello-task"></a>Zadanie hello toocomplete wersje interfejsu wiersza polecenia
Można ukończyć powitalnych zadań przy użyciu jednej z hello następujące wersje interfejsu wiersza polecenia:

- [Azure CLI 1.0](#quick-commands) — nasze interfejsu wiersza polecenia dla hello classic i zasobów zarządzania wdrażania modeli (w tym artykule)
- [Azure CLI 2.0](static-dns-name-resolution-for-linux-on-azure.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) -naszej nowej generacji interfejsu wiersza polecenia dla modelu wdrażania zarządzania zasobów hello


## <a name="quick-commands"></a>Szybkie polecenia

Jeśli potrzebujesz tooquickly hello zadania, powitania po sekcji Szczegóły poleceń hello potrzebne. Bardziej szczegółowe informacje i kontekst dla każdego kroku można znaleźć hello pozostałej części dokumentu hello [uruchamiania tutaj](#detailed-walkthrough).  

Wymagania Wstępne: NSG grupy zasobów, sieciami wirtualnymi, przy użyciu protokołu SSH ruchu przychodzącego, podsieci.

### <a name="create-a-vnic-with-a-static-internal-dns-name"></a>Utworzyć VNic statyczne wewnętrzne nazwy DNS

Witaj `-r` Flaga interfejsu wiersza polecenia jest ustawienie hello DNS etykiety, który zapewnia hello statycznej nazwy DNS dla hello VNic.

```azurecli
azure network nic create jenkinsVNic \
-g myResourceGroup \
-l westus \
-m myVNet \
-k mySubNet \
-r jenkins
```

### <a name="deploy-hello-vm-into-hello-vnet-nsg-and-connect-hello-vnic"></a>Wdrażanie hello maszyny Wirtualnej do hello sieci wirtualnej, NSG i połącz hello VNic

Witaj `-N` łączy hello VNic toohello nowej maszyny Wirtualnej podczas hello tooAzure wdrożenia.

```azurecli
azure vm create jenkins \
-g myResourceGroup \
-l westus \
-y linux \
-Q Debian \
-o myStorageAcct \
-u myAdminUser \
-M ~/.ssh/id_rsa.pub \
-F myVNet \
-j mySubnet \
-N jenkinsVNic
```

## <a name="detailed-walkthrough"></a>Szczegółowy przewodnik

Pełne ciągłej integracji i ciągłe wdrażanie (CiCd) infrastruktury na platformie Azure wymaga niektórych toobe statyczne lub długotrwałe serwery.  Zaleca się, że Azure zasoby, takie jak hello sieci wirtualnych (sieci wirtualne) i grupy zabezpieczeń sieci (NSG), musi być statyczny i tam długo zasoby, które rzadko są wdrożone.  Po wdrożeniu sieci wirtualnej można użyć ponownie przez nowych wdrożeń bez żadnych infrastruktury toohello niekorzystny wpływ.  Dodawanie sieci statycznych toothis Git repozytorium serwera i serwera automatyzacji Wpięć zapewnia CiCd tooyour środowisk deweloperskich lub testowania.  

Wewnętrzny nazw DNS są tylko rozpoznawany w sieci wirtualnej platformy Azure.  Ponieważ nazwy DNS hello są wewnętrzne, nie są one rozpoznawalną toohello poza internet, zapewniając dodatkowe zabezpieczenia toohello infrastruktury.

_Przykładami Zamień własne nazwy._

## <a name="create-hello-resource-group"></a>Utwórz grupę zasobów hello

Grupa zasobów jest wymagane tooorganize wszystko, co mamy utworzyć w tym przewodniku.  Aby uzyskać więcej informacji na temat grup zasobów platformy Azure, zobacz [Omówienie usługi Azure Resource Manager](../../azure-resource-manager/resource-group-overview.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

```azurecli
azure group create myResourceGroup \
--location westus
```

## <a name="create-hello-vnet"></a>Utwórz hello sieci wirtualnej

Witaj pierwszym krokiem jest toobuild maszyn wirtualnych do hello toolaunch sieci wirtualnej.  Witaj sieć wirtualna zawiera jedną podsieć w ramach tego przewodnika.  Aby uzyskać więcej informacji o sieci wirtualnych platformy Azure, zobacz [utworzyć sieć wirtualną przy użyciu hello wiersza polecenia platformy Azure](../../virtual-network/virtual-networks-create-vnet-arm-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

```azurecli
azure network vnet create myVNet \
--resource-group myResourceGroup \
--address-prefixes 10.10.0.0/24 \
--location westus
```

## <a name="create-hello-nsg"></a>Utwórz hello NSG

Witaj podsieci jest oparty za istniejącą sieciową grupę zabezpieczeń, dlatego budujemy hello NSG przed hello podsieci.  Azure grup NSG są równoważne tooa zapory na powitania warstwy sieci.  Aby uzyskać więcej informacji dotyczących grup NSG Azure, zobacz [jak grupy NSG toocreate w hello wiersza polecenia platformy Azure](../../virtual-network/virtual-networks-create-nsg-arm-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

```azurecli
azure network nsg create myNSG \
--resource-group myResourceGroup \
--location westus
```

## <a name="add-an-inbound-ssh-allow-rule"></a>Dodaj regułę Zezwalaj SSH dla ruchu przychodzącego

Witaj maszyny Wirtualnej systemu Linux wymaga dostępu z hello jest wymagana przez internet, regułę zezwalającą na toobe 22 ruch przychodzący port przekazywane hello sieci tooport 22 na powitania maszyny Wirtualnej systemu Linux.

```azurecli
azure network nsg rule create inboundSSH \
--resource-group myResourceGroup \
--nsg-name myNSG \
--access Allow \
--protocol Tcp \
--direction Inbound \
--priority 100 \
--source-address-prefix * \
--source-port-range * \
--destination-address-prefix 10.10.0.0/24 \
--destination-port-range 22
```

## <a name="add-a-subnet-toohello-vnet"></a>Dodaj toohello podsieci sieci wirtualnej

Maszyny wirtualne w ramach hello sieci wirtualnej muszą znajdować się w podsieci.  Każda sieć wirtualna może mieć wiele podsieci.  Utwórz podsieć hello i podsieć hello skojarzona z hello tooadd NSG podsieci toohello zapory.

```azurecli
azure network vnet subnet create mySubNet \
--resource-group myResourceGroup \
--vnet-name myVNet \
--address-prefix 10.10.0.0/26 \
--network-security-group-name myNSG
```

Hello podsieci jest teraz dodawane wewnątrz hello sieci wirtualnej i skojarzonych z hello NSG i reguły NSG hello.

## <a name="creating-static-dns-names"></a>Tworzenie statycznej nazwy DNS

Azure jest bardzo elastyczny, ale toouse nazwy DNS dla rozpoznawania nazw maszyn wirtualnych, należy je jako wirtualnej sieci karty (VNics) przy użyciu systemu DNS etykietowania toocreate.  VNics są ważne, ponieważ użytkownik może korzystać z nich łącząc je toodifferent maszyn wirtualnych, które hello VNic jako zasób statycznych hello maszyny wirtualne mogą być tymczasowe.  Przy użyciu systemu DNS etykietowania na powitania VNic, możemy rozpoznawania nazw proste stanie tooenable z innych maszyn wirtualnych w hello sieci wirtualnej.  Przy użyciu nazwy rozpoznawalną umożliwia inny serwer automatyzacji hello tooaccess maszyn wirtualnych na podstawie nazwy DNS hello `Jenkins` lub na serwerze Git hello `gitrepo`.  Utwórz VNic i powiązać ją z hello utworzone w poprzednim kroku hello podsieci.

```azurecli
azure network nic create jenkinsVNic \
-g myResourceGroup \
-l westus \
-m myVNet \
-k mySubNet \
-r jenkins
```

## <a name="deploy-hello-vm-into-hello-vnet-and-nsg"></a>Wdrażanie hello maszyny Wirtualnej do hello sieci wirtualnej i grupy NSG

Mamy teraz sieci wirtualnej, podsieci w tej sieci wirtualnej, a grupa NSG, działając jako tooprotect zapory naszych podsieci blokuje cały ruch przychodzący z wyjątkiem port 22 SSH.  Teraz można wdrożyć Hello maszyny Wirtualnej w tym istniejącej infrastruktury sieci.

Przy użyciu interfejsu wiersza polecenia Azure hello i hello `azure vm create` polecenia hello maszyny Wirtualnej systemu Linux jest wdrożony toohello istniejącej grupy zasobów platformy Azure, sieci wirtualnej, podsieci i VNic.  Aby uzyskać więcej informacji na temat używania hello CLI toodeploy pełną maszyny Wirtualnej, zobacz [tworzyć kompletne środowisko systemu Linux przy użyciu interfejsu wiersza polecenia Azure hello](create-cli-complete.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

```azurecli
azure vm create jenkins \
--resource-group myResourceGroup myVM \
--location westus \
--os-type linux \
--image-urn Debian \
--storage-account-name mystorageaccount \
--admin-username myAdminUser \
--ssh-publickey-file ~/.ssh/id_rsa.pub \
--vnet-name myVNet \
--vnet-subnet-name mySubnet \
--nic-name jenkinsVNic
```

Za pomocą hello interfejsu wiersza polecenia flagi toocall limit istniejących zasobów, firma Microsoft poinstruować hello Azure toodeploy VM wewnątrz hello istniejącej sieci.  tooreiterate, po wdrożeniu sieci wirtualnej i podsieci, ich może pozostać statyczne ani stałe zasobów w Twoim regionie Azure.  

## <a name="next-steps"></a>Następne kroki
* [Tworzenie niestandardowego środowiska dla maszyny wirtualnej z systemem Linux poprzez bezpośrednie użycie poleceń interfejsu wiersza polecenia platformy Azure](create-cli-complete.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [Utwórz Maszynę wirtualną systemu Linux na platformie Azure za pomocą szablonów](create-ssh-secured-vm-from-template.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
