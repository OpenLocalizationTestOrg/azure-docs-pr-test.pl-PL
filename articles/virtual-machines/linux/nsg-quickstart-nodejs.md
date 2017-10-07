---
title: aaaOpen porty tooa maszyny Wirtualnej systemu Linux z interfejsu wiersza polecenia platformy Azure w wersji 1.0 | Dokumentacja firmy Microsoft
description: "Dowiedz się, jak tooopen portu / create tooyour punktu końcowego maszyny Wirtualnej systemu Linux przy użyciu wdrażania Menedżera zasobów Azure hello modelu i hello Azure CLI w wersji 1.0"
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 05/11/2017
ms.author: iainfou
ms.openlocfilehash: 337c37d151f527b43d4852291159b2f70a00accc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="opening-ports-and-endpoints-tooa-linux-vm-in-azure-using-hello-azure-cli-10"></a>Otwieranie portów i punkty końcowe tooa maszyny Wirtualnej systemu Linux platformy Azure przy użyciu hello Azure CLI w wersji 1.0
Otwarcie portu lub tworzenie punktu końcowego tooa maszyny wirtualnej (VM) na platformie Azure przez utworzenie filtru sieci w podsieci lub interfejsu sieciowego maszyny Wirtualnej. Te filtry, które kontrolują ruchu przychodzącego i wychodzącego, należy umieścić na zasób toohello dołączony sieciowej grupy zabezpieczeń, który odbiera ruch hello. Użyjmy typowym przykładem ruchu w sieci web na porcie 80. W tym artykule opisano, jak tooopen portu tooa maszynę Wirtualną przy użyciu hello Azure CLI w wersji 1.0.


## <a name="cli-versions-toocomplete-hello-task"></a>Zadanie hello toocomplete wersje interfejsu wiersza polecenia
Można ukończyć powitalnych zadań przy użyciu jednej z hello następujące wersje interfejsu wiersza polecenia:

- [Azure CLI 1.0](#quick-commands) — nasze interfejsu wiersza polecenia dla hello classic i zasobów zarządzania wdrażania modeli (w tym artykule)
- [Azure CLI 2.0](nsg-quickstart.md) -naszej nowej generacji interfejsu wiersza polecenia dla modelu wdrażania zarządzania zasobów hello


## <a name="quick-commands"></a>Szybkie polecenia
toocreate sieciowej grupy zabezpieczeń i zasad należy [hello Azure CLI 1.0](../../cli-install-nodejs.md) zainstalowanych i użycie tryb usługi Resource Manager:

```azurecli
azure config mode arm
```

Poniższe przykłady w hello Zastąp przykładowe nazwy parametrów własne wartości. Przykład nazwy parametrów uwzględnione *myResourceGroup*, *myNetworkSecurityGroup*, i *myVnet*.

Utwórz swojej grupy zabezpieczeń sieci, odpowiednio wprowadzania własne nazwy i lokalizacji. Witaj poniższy przykład tworzy sieciową grupę zabezpieczeń o nazwie *myNetworkSecurityGroup* w hello *eastus* lokalizacji:

```azurecli
azure network nsg create \
    --resource-group myResourceGroup \
    --location eastus \
    --name myNetworkSecurityGroup
```

Dodaj regułę tooallow HTTP ruchu tooyour serwer sieci Web (lub dostosować własne scenariusz, takich jak SSH łączności dostępu lub bazy danych). Witaj poniższy przykład powoduje utworzenie reguły o nazwie *myNetworkSecurityGroupRule* tooallow TCP, ruch na porcie 80:

```azurecli
azure network nsg rule create \
    --resource-group myResourceGroup \
    --nsg-name myNetworkSecurityGroup \
    --name myNetworkSecurityGroupRule \
    --protocol tcp \
    --direction inbound \
    --priority 1000 \
    --destination-port-range 80 \
    --access allow
```

Skojarz hello sieciową grupę zabezpieczeń z maszyny Wirtualnej interfejsu sieciowego (NIC). Witaj poniższy przykład powoduje skojarzenie istniejącej karty NIC o nazwie *myNic* z hello sieciową grupę zabezpieczeń o nazwie *myNetworkSecurityGroup*:

```azurecli
azure network nic set \
    --resource-group myResourceGroup \
    --network-security-group-name myNetworkSecurityGroup \
    --name myNic
```

Alternatywnie można skojarzyć swojej grupy zabezpieczeń sieci z podsieci sieci wirtualnej, a nie tylko toohello interfejsu sieciowego na jednej maszynie Wirtualnej. Witaj poniższy przykład powoduje skojarzenie istniejącą podsieć o nazwie *mySubnet* w hello *myVnet* sieci wirtualnej z hello sieciową grupę zabezpieczeń o nazwie *myNetworkSecurityGroup*:

```azurecli
azure network vnet subnet set \
    --resource-group myResourceGroup \
    --network-security-group-name myNetworkSecurityGroup \
    --vnet-name myVnet --name mySubnet
```

## <a name="more-information-on-network-security-groups"></a>Więcej informacji na temat grup zabezpieczeń sieci
Witaj w tym miejscu szybkie polecenia pozwalają tooget zapasowych i pracy z tooyour przechodzenia ruchu maszyny Wirtualnej. Grupy zabezpieczeń sieci stanowią wielu funkcje i poziom szczegółowości kontrolowanie dostęp do zasobów tooyour. Możesz przeczytać dodatkowe informacje [Tworzenie grupy zabezpieczeń sieci i listy ACL zasady tutaj](../../virtual-network/virtual-networks-create-nsg-arm-cli.md).

Grupy zabezpieczeń sieci i reguły list kontroli dostępu można zdefiniować jako część szablonów usługi Azure Resource Manager. Przeczytaj więcej na temat [tworzenie grup zabezpieczeń sieci z szablonami](../../virtual-network/virtual-networks-create-nsg-arm-template.md).

Jeśli potrzebujesz toouse przekierowania portów toomap unikatowy portu zewnętrznego portu wewnętrznego tooan na maszynie Wirtualnej, użyj modułu równoważenia obciążenia i reguły translatora adresów sieciowych (NAT). Może na przykład mają tooexpose port TCP 8080 zewnętrznie i mieć ruch skierowany tooTCP port 80 na maszynie Wirtualnej. Informacje na temat [tworzenia modułu równoważenia obciążenia internetowy](../../load-balancer/load-balancer-get-started-internet-arm-cli.md).

## <a name="next-steps"></a>Następne kroki
W tym przykładzie utworzono ruch tooallow HTTP Prosta reguła. Można znaleźć informacje dotyczące tworzenia środowisk bardziej szczegółowe w hello następujące artykuły:

* [Omówienie usługi Azure Resource Manager](../../azure-resource-manager/resource-group-overview.md)
* [Co to jest sieciowa grupa zabezpieczeń?](../../virtual-network/virtual-networks-nsg.md)
* [Omówienie usługi Azure Resource Manager dla usługi równoważenia obciążenia](../../load-balancer/load-balancer-arm.md)

