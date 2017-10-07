---
title: aaaOpen porty tooa maszyny Wirtualnej systemu Linux 2.0 interfejsu wiersza polecenia platformy Azure | Dokumentacja firmy Microsoft
description: "Dowiedz się, jak tooopen portu / create tooyour punktu końcowego maszyny Wirtualnej systemu Linux przy użyciu wdrażania Menedżera zasobów Azure hello modelu i hello Azure CLI 2.0"
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
ms.assetid: eef9842b-495a-46cf-99a6-74e49807e74e
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 08/21/2017
ms.author: iainfou
ms.openlocfilehash: c79b31206e97558171609cf033bb3cb3370777c7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="open-ports-and-endpoints-tooa-linux-vm-with-hello-azure-cli"></a>Otwórz porty i punkty końcowe tooa maszyny Wirtualnej systemu Linux z hello wiersza polecenia platformy Azure
Otwarcie portu lub tworzenie punktu końcowego tooa maszyny wirtualnej (VM) na platformie Azure przez utworzenie filtru sieci w podsieci lub interfejsu sieciowego maszyny Wirtualnej. Te filtry, które kontrolują ruchu przychodzącego i wychodzącego, należy umieścić na zasób toohello dołączony sieciowej grupy zabezpieczeń, który odbiera ruch hello. Użyjmy typowym przykładem ruchu w sieci web na porcie 80. W tym artykule opisano sposób tooopen tooa portu maszyny Wirtualnej z hello Azure CLI 2.0. Można również wykonać te kroki hello [Azure CLI 1.0](nsg-quickstart-nodejs.md).


## <a name="quick-commands"></a>Szybkie polecenia
Grupy zabezpieczeń sieci toocreate i potrzebnych reguł hello najnowszych [Azure CLI 2.0](/cli/azure/install-az-cli2) zainstalowane i zarejestrowane za pomocą konta Azure tooan [logowania az](/cli/azure/#login).

Poniższe przykłady w hello Zastąp przykładowe nazwy parametrów własne wartości. Przykład nazwy parametru zawierają *myResourceGroup*, *myNetworkSecurityGroup*, i *myVnet*.

Utwórz grupę zabezpieczeń sieci hello z [utworzyć nsg sieci az](/cli/azure/network/nsg#create). Witaj poniższy przykład tworzy sieciową grupę zabezpieczeń o nazwie *myNetworkSecurityGroup* w hello *eastus* lokalizacji:

```azurecli
az network nsg create \
    --resource-group myResourceGroup \
    --location eastus \
    --name myNetworkSecurityGroup
```

Dodaj regułę z [Tworzenie reguły nsg sieci az](/cli/azure/network/nsg/rule#create) tooallow HTTP ruchu tooyour serwer sieci Web (lub dostosować własne scenariusz, takich jak SSH łączności dostępu lub bazy danych). Witaj poniższy przykład powoduje utworzenie reguły o nazwie *myNetworkSecurityGroupRule* tooallow TCP, ruch na porcie 80:

```azurecli
az network nsg rule create \
    --resource-group myResourceGroup \
    --nsg-name myNetworkSecurityGroup \
    --name myNetworkSecurityGroupRule \
    --protocol tcp \
    --priority 1000 \
    --destination-port-range 80
```

Skojarz hello sieciową grupę zabezpieczeń z maszyny Wirtualnej interfejsu sieciowego (NIC) z [aktualizacji kart sieciowych az](/cli/azure/network/nic#update). Witaj poniższy przykład powoduje skojarzenie istniejącej karty NIC o nazwie *myNic* z hello sieciową grupę zabezpieczeń o nazwie *myNetworkSecurityGroup*:

```azurecli
az network nic update \
    --resource-group myResourceGroup \
    --name myNic \
    --network-security-group myNetworkSecurityGroup
```

Alternatywnie można skojarzyć swojej grupy zabezpieczeń sieci z podsiecią sieci wirtualnej z [zaktualizować podsieci sieci wirtualnej sieci az](/cli/azure/network/vnet/subnet#update) zamiast właśnie toohello interfejsu sieciowego na jednej maszynie Wirtualnej. Witaj poniższy przykład powoduje skojarzenie istniejącą podsieć o nazwie *mySubnet* w hello *myVnet* sieci wirtualnej z hello sieciową grupę zabezpieczeń o nazwie *myNetworkSecurityGroup*:

```azurecli
az network vnet subnet update \
    --resource-group myResourceGroup \
    --vnet-name myVnet \
    --name mySubnet \
    --network-security-group myNetworkSecurityGroup
```

## <a name="more-information-on-network-security-groups"></a>Więcej informacji na temat grup zabezpieczeń sieci
Witaj w tym miejscu szybkie polecenia pozwalają tooget zapasowych i pracy z tooyour przechodzenia ruchu maszyny Wirtualnej. Grupy zabezpieczeń sieci stanowią wielu funkcje i poziom szczegółowości kontrolowanie dostęp do zasobów tooyour. Możesz przeczytać dodatkowe informacje [Tworzenie grupy zabezpieczeń sieci i listy ACL zasady tutaj](tutorial-virtual-network.md#secure-network-traffic).

Dla aplikacji sieci web wysokiej dostępności należy umieszczać maszyny wirtualne za usługą równoważenia obciążenia Azure. Moduł równoważenia obciążenia Hello dystrybuuje tooVMs ruchu, z sieciową grupą zabezpieczeń, który umożliwia filtrowanie ruchu. Aby uzyskać więcej informacji, zobacz [jak maszyn saldo tooload wirtualnych systemu Linux, w Azure toocreate wysokiej dostępności aplikacji](tutorial-load-balancer.md).

## <a name="next-steps"></a>Następne kroki
W tym przykładzie utworzono ruch tooallow HTTP Prosta reguła. Można znaleźć informacje dotyczące tworzenia środowisk bardziej szczegółowe w hello następujące artykuły:

* [Omówienie usługi Azure Resource Manager](../../azure-resource-manager/resource-group-overview.md)
* [Co to jest sieciowa grupa zabezpieczeń?](../../virtual-network/virtual-networks-nsg.md)
