---
title: "aaaCreate kompletne środowisko Linux z hello Azure CLI 1.0 | Dokumentacja firmy Microsoft"
description: "Tworzenie magazynu, Maszynę wirtualną systemu Linux, sieci wirtualnej i podsieci, usługi równoważenia obciążenia, karty Sieciowej, publicznego adresu IP i sieciową grupę zabezpieczeń, z hello tła przy użyciu hello Azure CLI w wersji 1.0."
services: virtual-machines-linux
documentationcenter: virtual-machines
author: iainfoulds
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 4ba4060b-ce95-4747-a735-1d7c68597a1a
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 02/09/2017
ms.author: iainfou
ms.openlocfilehash: 7fe00e138704fe9c9a1c9b87a7dd1afd6174e527
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-complete-linux-environment-with-hello-azure-cli-10"></a>Utwórz pełną środowiska Linux z hello Azure CLI w wersji 1.0
W tym artykule budujemy prosta sieć z modułem równoważenia obciążenia i para maszyn wirtualnych, które są przydatne w przypadku tworzenia i przetwarzania proste. Firma Microsoft przeprowadzenie procesu hello przez polecenie, dopóki nie uzyskasz dwóch pracy zabezpieczeń toowhich maszyn wirtualnych systemu Linux, które można połączyć z dowolnego miejsca w hello Internet. Następnie można przenieść na toomore złożone sieci i środowiskach.

Wzdłuż sposób hello zapoznanie się hello zależności hierarchii modelu wdrażania usługi Resource Manager hello umożliwia, czy o ile zawiera. Po jak hello system jest wbudowana, można go znacznie szybciej odtworzyć za pomocą [szablonów usługi Azure Resource Manager](../../resource-group-authoring-templates.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json). Ponadto po dowiesz się, jak hello części środowiska dopasowania, tworzenie szablonów tooautomate ich staje się łatwiejsze.

środowisko Hello zawiera:

* Dwie maszyny wirtualne w zestawie dostępności.
* Usługi równoważenia obciążenia z regułą równoważenia obciążenia na porcie 80.
* Grupy zabezpieczeń sieci (NSG) zasady tooprotect maszyny Wirtualnej z niepożądanego ruchu.

toocreate to środowisko niestandardowe, należy hello najnowszych [Azure CLI 1.0](../../cli-install-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) w trybie Menedżera zasobów (`azure config mode arm`). Należy również JSON, narzędzie do analizy. W tym przykładzie użyto [jq](https://stedolan.github.io/jq/).


## <a name="cli-versions-toocomplete-hello-task"></a>Zadanie hello toocomplete wersje interfejsu wiersza polecenia
Można ukończyć powitalnych zadań przy użyciu jednej z hello następujące wersje interfejsu wiersza polecenia:

- [Azure CLI 1.0](#quick-commands) — nasze interfejsu wiersza polecenia dla hello classic i zasobów zarządzania wdrażania modeli (w tym artykule)
- [Azure CLI 2.0](create-cli-complete.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) -naszej nowej generacji interfejsu wiersza polecenia dla modelu wdrażania zarządzania zasobów hello


## <a name="quick-commands"></a>Szybkie polecenia
Jeśli potrzebujesz tooquickly hello zadania, powitania po sekcji Szczegóły hello podstawowych poleceń tooupload tooAzure maszyny Wirtualnej. Bardziej szczegółowe informacje i kontekst dla każdego kroku można znaleźć w rest hello hello dokumentu, początkowa [tutaj](#detailed-walkthrough).

Upewnij się, że masz [hello Azure CLI 1.0](../../cli-install-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) zalogowany i w trybie Menedżera zasobów:

```azurecli
azure config mode arm
```

Poniższe przykłady w hello Zastąp przykładowe nazwy parametrów własne wartości. Przykład nazwy parametru zawierają `myResourceGroup`, `mystorageaccount`, i `myVM`.

Utwórz grupę zasobów hello. Witaj poniższy przykład tworzy grupę zasobów o nazwie `myResourceGroup` w hello `westeurope` lokalizacji:

```azurecli
azure group create -n myResourceGroup -l westeurope
```

Sprawdź hello grupy zasobów, przy użyciu analizatora składni JSON hello:

```azurecli
azure group show myResourceGroup --json | jq '.'
```

Tworzenie konta magazynu hello. Witaj poniższy przykład tworzy konto magazynu o nazwie `mystorageaccount`. (nazwa konta magazynu hello musi być unikatowa, aby podać własną unikatową nazwę.)

```azurecli
azure storage account create -g myResourceGroup -l westeurope \
  --kind Storage --sku-name GRS mystorageaccount
```

Sprawdź konto magazynu hello przy użyciu analizatora składni JSON hello:

```azurecli
azure storage account show -g myResourceGroup mystorageaccount --json | jq '.'
```

Utwórz sieć wirtualną hello. Witaj poniższy przykład tworzy sieć wirtualną o nazwie `myVnet`:

```azurecli
azure network vnet create -g myResourceGroup -l westeurope\
  -n myVnet -a 192.168.0.0/16
```

Utwórz podsieć. Witaj poniższy przykład tworzy podsieć o nazwie `mySubnet`:

```azurecli
azure network vnet subnet create -g myResourceGroup \
  -e myVnet -n mySubnet -a 192.168.1.0/24
```

Sprawdź hello sieci wirtualnej i podsieci przy użyciu analizatora składni JSON hello:

```azurecli
azure network vnet show myResourceGroup myVnet --json | jq '.'
```

Tworzenie publicznego adresu IP. Witaj poniższy przykład tworzy publicznego adresu IP o nazwie `myPublicIP` o nazwie DNS hello `mypublicdns`. (nazwa DNS hello musi być unikatowa, aby podać własną unikatową nazwę.)

```azurecli
azure network public-ip create -g myResourceGroup -l westeurope \
  -n myPublicIP  -d mypublicdns -a static -i 4
```

Utwórz hello modułu równoważenia obciążenia. Witaj poniższy przykład tworzy moduł równoważenia obciążenia o nazwie `myLoadBalancer`:

```azurecli
azure network lb create -g myResourceGroup -l westeurope -n myLoadBalancer
```

Utwórz pulę IP frontonu dla usługi równoważenia obciążenia hello i skojarz hello publicznego adresu IP. Witaj poniższy przykład tworzy frontonu pula IP o nazwie `mySubnetPool`:

```azurecli
azure network lb frontend-ip create -g myResourceGroup -l myLoadBalancer \
  -i myPublicIP -n myFrontEndPool
```

Tworzenie puli adresów IP zaplecza powitania dla usługi równoważenia obciążenia hello. Witaj poniższy przykład tworzy pula IP zaplecza, o nazwie `myBackEndPool`:

```azurecli
azure network lb address-pool create -g myResourceGroup -l myLoadBalancer \
  -n myBackEndPool
```

Tworzenie sieci dla ruchu przychodzącego protokołu SSH reguł translacji adresów adres hello modułu równoważenia obciążenia. Witaj poniższy przykład tworzy dwie reguły modułu równoważenia obciążenia, `myLoadBalancerRuleSSH1` i `myLoadBalancerRuleSSH2`:

```azurecli
azure network lb inbound-nat-rule create -g myResourceGroup -l myLoadBalancer \
  -n myLoadBalancerRuleSSH1 -p tcp -f 4222 -b 22
azure network lb inbound-nat-rule create -g myResourceGroup -l myLoadBalancer \
  -n myLoadBalancerRuleSSH2 -p tcp -f 4223 -b 22
```

Tworzenie sieci web hello reguły NAT ruchu przychodzącego dla hello modułu równoważenia obciążenia. Witaj poniższy przykład tworzy regułę równoważenia obciążenia o nazwie `myLoadBalancerRuleWeb`:

```azurecli
azure network lb rule create -g myResourceGroup -l myLoadBalancer \
  -n myLoadBalancerRuleWeb -p tcp -f 80 -b 80 \
  -t myFrontEndPool -o myBackEndPool
```

Utwórz sondy kondycji modułu równoważenia obciążenia hello. Witaj poniższy przykład tworzy sondowaniem TCP o nazwie `myHealthProbe`:

```azurecli
azure network lb probe create -g myResourceGroup -l myLoadBalancer \
  -n myHealthProbe -p "tcp" -i 15 -c 4
```

Sprawdź hello modułu równoważenia obciążenia, pule adresów IP i reguł NAT, za pomocą analizatora składni JSON hello:

```azurecli
azure network lb show -g myResourceGroup -n myLoadBalancer --json | jq '.'
```

Utwórz hello pierwszy karta sieciowa (NIC). Zastąp hello `#####-###-###` sekcje z identyfikatorem subskrypcji platformy Azure Identyfikator jest odnotowany w danych wyjściowych hello subskrypcji **jq** podczas badania zasobów hello tworzenia. Można również wyświetlić identyfikator subskrypcji z `azure account list`.

Witaj poniższy przykład tworzy karty Sieciowej o nazwie `myNic1`:

```azurecli
azure network nic create -g myResourceGroup -l westeurope \
  -n myNic1 -m myVnet -k mySubnet \
  -d "/subscriptions/########-####-####-####-############/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/backendAddressPools/myBackEndPool" \
  -e "/subscriptions/########-####-####-####-############/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/inboundNatRules/myLoadBalancerRuleSSH1"
```

Utwórz hello drugiej karty sieciowej. Witaj poniższy przykład tworzy karty Sieciowej o nazwie `myNic2`:

```azurecli
azure network nic create -g myResourceGroup -l westeurope \
  -n myNic2 -m myVnet -k mySubnet \
  -d "/subscriptions/########-####-####-####-############/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/backendAddressPools/myBackEndPool" \
  -e "/subscriptions/########-####-####-####-############/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/inboundNatRules/myLoadBalancerRuleSSH2"
```

Sprawdź Witaj dwie karty sieciowe za pomocą analizatora składni JSON hello:

```azurecli
azure network nic show myResourceGroup myNic1 --json | jq '.'
azure network nic show myResourceGroup myNic2 --json | jq '.'
```

Utwórz grupę zabezpieczeń sieci hello. Witaj poniższy przykład tworzy sieciową grupę zabezpieczeń o nazwie `myNetworkSecurityGroup`:

```azurecli
azure network nsg create -g myResourceGroup -l westeurope \
  -n myNetworkSecurityGroup
```

Dodaj dwie reguły ruchu przychodzącego hello sieciowej grupy zabezpieczeń. Witaj poniższy przykład tworzy dwie reguły `myNetworkSecurityGroupRuleSSH` i `myNetworkSecurityGroupRuleHTTP`:

```azurecli
azure network nsg rule create -p tcp -r inbound -y 1000 -u 22 -c allow \
  -g myResourceGroup -a myNetworkSecurityGroup -n myNetworkSecurityGroupRuleSSH
azure network nsg rule create -p tcp -r inbound -y 1001 -u 80 -c allow \
  -g myResourceGroup -a myNetworkSecurityGroup -n myNetworkSecurityGroupRuleHTTP
```

Sprawdź hello sieciowej grupy zabezpieczeń i reguł ruchu przychodzącego przy użyciu analizatora składni JSON hello:

```azurecli
azure network nsg show -g myResourceGroup -n myNetworkSecurityGroup --json | jq '.'
```

Powiązania zabezpieczeń sieciowych hello grupy toohello dwie karty sieciowe:

```azurecli
azure network nic set -g myResourceGroup -o myNetworkSecurityGroup -n myNic1
azure network nic set -g myResourceGroup -o myNetworkSecurityGroup -n myNic2
```

Utwórz hello zestawu dostępności. Witaj poniższy przykład tworzy zbiór nazwanego dostępności `myAvailabilitySet`:

```azurecli
azure availset create -g myResourceGroup -l westeurope -n myAvailabilitySet
```

Tworzenie pierwszej maszyny Wirtualnej systemu Linux hello. Witaj poniższy przykład tworzy Maszynę wirtualną o nazwie `myVM1`:

```azurecli
azure vm create \
    --resource-group myResourceGroup \
    --name myVM1 \
    --location westeurope \
    --os-type linux \
    --availset-name myAvailabilitySet \
    --nic-name myNic1 \
    --vnet-name myVnet \
    --vnet-subnet-name mySubnet \
    --storage-account-name mystorageaccount \
    --image-urn canonical:UbuntuServer:16.04.0-LTS:latest \
    --ssh-publickey-file ~/.ssh/id_rsa.pub \
    --admin-username azureuser
```

Utwórz hello drugie maszyny Wirtualnej systemu Linux. Witaj poniższy przykład tworzy Maszynę wirtualną o nazwie `myVM2`:

```azurecli
azure vm create \
    --resource-group myResourceGroup \
    --name myVM2 \
    --location westeurope \
    --os-type linux \
    --availset-name myAvailabilitySet \
    --nic-name myNic2 \
    --vnet-name myVnet \
    --vnet-subnet-name mySubnet \
    --storage-account-name mystorageaccount \
    --image-urn canonical:UbuntuServer:16.04.0-LTS:latest \
    --ssh-publickey-file ~/.ssh/id_rsa.pub \
    --admin-username azureuser
```

Użyj tooverify analizatora składni JSON hello, że wszystko, który został utworzony:

```azurecli
azure vm show -g myResourceGroup -n myVM1 --json | jq '.'
azure vm show -g myResourceGroup -n myVM2 --json | jq '.'
```

Eksportowanie z nowego środowiska tooa szablonu tooquickly ponownie utworzyć nowych wystąpień:

```azurecli
azure group export myResourceGroup
```

## <a name="detailed-walkthrough"></a>Szczegółowy przewodnik
Witaj szczegółowy opis kroków, które należy wykonać wyjaśnić, każdego polecenia czynności podczas tworzenia Twoje środowisko. Te pojęcia są przydatne podczas tworzenia własnego niestandardowego środowiska dla rozwoju lub produkcji.

Upewnij się, że masz [hello Azure CLI 1.0](../../cli-install-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) zalogowany i w trybie Menedżera zasobów:

```azurecli
azure config mode arm
```

Poniższe przykłady w hello Zastąp przykładowe nazwy parametrów własne wartości. Przykład nazwy parametru zawierają `myResourceGroup`, `mystorageaccount`, i `myVM`.

## <a name="create-resource-groups-and-choose-deployment-locations"></a>Tworzenie grupy zasobów, a następnie wybierz pozycję lokalizacji wdrożenia
Grupy zasobów platformy Azure są jednostki logicznej wdrożenia, które zawiera informacje i metadanych tooenable hello logiczny zarządzania konfiguracją wdrożeń zasobów. Witaj poniższy przykład tworzy grupę zasobów o nazwie `myResourceGroup` w hello `westeurope` lokalizacji:

```azurecli
azure group create --name myResourceGroup --location westeurope
```

Dane wyjściowe:

```azurecli                        
info:    Executing command group create
+ Getting resource group myResourceGroup
+ Creating resource group myResourceGroup
info:    Created resource group myResourceGroup
data:    Id:                  /subscriptions/guid/resourceGroups/myResourceGroup
data:    Name:                myResourceGroup
data:    Location:            westeurope
data:    Provisioning State:  Succeeded
data:    Tags: null
data:
info:    group create command OK
```

## <a name="create-a-storage-account"></a>Tworzenie konta magazynu
Potrzebujesz konta usługi storage dla dysków maszyny Wirtualnej i dla dowolnego dodatkowego dysku z danymi, które mają tooadd. Możesz utworzyć konta magazynu prawie natychmiast po utworzeniu grup zasobów.

W tym miejscu użyjemy hello `azure storage account create` polecenia przekazywanie hello Lokalizacja konta hello, hello grupy zasobów, która kontroluje, a typ hello obsługi magazynu ma. Witaj poniższy przykład tworzy konto magazynu o nazwie `mystorageaccount`:

```azurecli
azure storage account create \  
  --location westeurope \
  --resource-group myResourceGroup \
  --kind Storage --sku-name GRS \
  mystorageaccount
```

Dane wyjściowe:

```azurecli
info:    Executing command storage account create
+ Creating storage account
info:    storage account create command OK
```

tooexamine zasobów naszej grupy za pomocą hello `azure group show` polecenia, można użyć hello [jq](https://stedolan.github.io/jq/) narzędzia wraz z hello `--json` opcji wiersza polecenia platformy Azure. (Można użyć **jsawk** lub żadnej biblioteki języka wolisz tooparse hello JSON.)

```azurecli
azure group show myResourceGroup --json | jq '.'
```

Dane wyjściowe:

```json
{
  "tags": {},
  "id": "/subscriptions/guid/resourceGroups/myResourceGroup",
  "name": "myResourceGroup",
  "provisioningState": "Succeeded",
  "location": "westeurope",
  "properties": {
    "provisioningState": "Succeeded"
  },
  "resources": [
    {
      "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Storage/storageAccounts/mystorageaccount",
      "name": "mystorageaccount",
      "type": "storageAccounts",
      "location": "westeurope",
      "tags": null
    }
  ],
  "permissions": [
    {
      "actions": [
        "*"
      ],
      "notActions": []
    }
  ]
}
```

tooinvestigate hello konta magazynu przy użyciu interfejsu wiersza polecenia hello, musisz najpierw nazwy kont hello tooset i kluczy. Zastąp hello nazwy konta magazynu hello w hello poniższy przykład o nazwie, wybrane:

```bash
export AZURE_STORAGE_CONNECTION_STRING="$(azure storage account connectionstring show mystorageaccount --resource-group myResourceGroup --json | jq -r '.string')"
```

Następnie można wyświetlić informacje o pamięci masowej łatwo:

```azurecli
azure storage container list
```

Dane wyjściowe:

```azurecli
info:    Executing command storage container list
+ Getting storage containers
data:    Name  Public-Access  Last-Modified
data:    ----  -------------  -----------------------------
data:    vhds  Off            Sun, 27 Sep 2015 19:03:54 GMT
info:    storage container list command OK
```

## <a name="create-a-virtual-network-and-subnet"></a>Tworzenie sieci wirtualnej i podsieci
Następnie będzie tooneed toocreate sieci wirtualnej z systemem Azure i podsieć, w którym można utworzyć maszyny wirtualne. Witaj poniższy przykład tworzy sieć wirtualną o nazwie `myVnet` z hello `192.168.0.0/16` prefiks adresu:

```azurecli
azure network vnet create --resource-group myResourceGroup --location westeurope \
  --name myVnet --address-prefixes 192.168.0.0/16
```

Dane wyjściowe:

```azurecli
info:    Executing command network vnet create
+ Looking up virtual network "myVnet"
+ Creating virtual network "myVnet"
+ Loading virtual network state
data:    Id                              : /subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/virtualNetworks/myVnet
data:    Name                            : myVnet
data:    Type                            : Microsoft.Network/virtualNetworks
data:    Location                        : westeurope
data:    ProvisioningState               : Succeeded
data:    Address prefixes:
data:      192.168.0.0/16
info:    network vnet create command OK
```

Użyjmy ponownie, opcja--json hello `azure group show` i `jq` toosee jak tworzymy naszych zasobów. Teraz `storageAccounts` zasobów i `virtualNetworks` zasobów.  

```azurecli
azure group show myResourceGroup --json | jq '.'
```

Dane wyjściowe:

```json
{
  "tags": {},
  "id": "/subscriptions/guid/resourceGroups/myResourceGroup",
  "name": "myResourceGroup",
  "provisioningState": "Succeeded",
  "location": "westeurope",
  "properties": {
    "provisioningState": "Succeeded"
  },
  "resources": [
    {
      "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/virtualNetworks/myVnet",
      "name": "myVnet",
      "type": "virtualNetworks",
      "location": "westeurope",
      "tags": null
    },
    {
      "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Storage/storageAccounts/mystorageaccount",
      "name": "mystorageaccount",
      "type": "storageAccounts",
      "location": "westeurope",
      "tags": null
    }
  ],
  "permissions": [
    {
      "actions": [
        "*"
      ],
      "notActions": []
    }
  ]
}
```

Teraz Utwórzmy podsieci w hello `myVnet` sieci wirtualnej, w których hello wdrożonych maszyn wirtualnych. Używamy hello `azure network vnet subnet create` polecenia wraz z zasobów hello już utworzyliśmy: hello `myResourceGroup` grupy zasobów i hello `myVnet` sieci wirtualnej. W hello poniższy przykład, możemy dodać hello podsieci o nazwie `mySubnet` z prefiksu adresu podsieci hello `192.168.1.0/24`:

```azurecli
azure network vnet subnet create --resource-group myResourceGroup \
  --vnet-name myVnet --name mySubnet --address-prefix 192.168.1.0/24
```

Dane wyjściowe:

```azurecli
info:    Executing command network vnet subnet create
+ Looking up hello subnet "mySubnet"
+ Creating subnet "mySubnet"
+ Looking up hello subnet "mySubnet"
data:    Id                              : /subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/virtualNetworks/myVnet/subnets/mySubnet
data:    Type                            : Microsoft.Network/virtualNetworks/subnets
data:    ProvisioningState               : Succeeded
data:    Name                            : mySubnet
data:    Address prefix                  : 192.168.1.0/24
data:
info:    network vnet subnet create command OK
```

Ponieważ podsieci hello logicznie znajduje się w sieci wirtualnej hello, możemy znaleźć hello podsieci za pomocą polecenia nieco inne. polecenie Hello używamy jest `azure network vnet show`, ale nadal dane wyjściowe JSON hello tooexamine przy użyciu `jq`.

```azurecli
azure network vnet show myResourceGroup myVnet --json | jq '.'
```

Dane wyjściowe:

```json
{
  "subnets": [
    {
      "ipConfigurations": [],
      "addressPrefix": "192.168.1.0/24",
      "provisioningState": "Succeeded",
      "name": "mySubnet",
      "etag": "W/\"974f3e2c-028e-4b35-832b-a4b16ad25eb6\"",
      "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/virtualNetworks/myVnet/subnets/mySubnet"
    }
  ],
  "tags": {},
  "addressSpace": {
    "addressPrefixes": [
      "192.168.0.0/16"
    ]
  },
  "dhcpOptions": {
    "dnsServers": []
  },
  "provisioningState": "Succeeded",
  "etag": "W/\"974f3e2c-028e-4b35-832b-a4b16ad25eb6\"",
  "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/virtualNetworks/myVnet",
  "name": "myVnet",
  "location": "westeurope"
}
```

## <a name="create-a-public-ip-address"></a>Tworzenie publicznego adresu IP
Teraz Utwórzmy hello publicznego adresu IP (PIP) czy możemy przypisać tooyour modułu równoważenia obciążenia. Włącza tooconnect tooyour maszyn wirtualnych z hello Internet przy użyciu hello `azure network public-ip create` polecenia. Ponieważ hello domyślnym adresem jest dynamiczny, utworzymy nazwany wpis DNS w hello **cloudapp.azure.com** domeny przy użyciu hello `--domain-name-label` opcji. Witaj poniższy przykład tworzy publicznego adresu IP o nazwie `myPublicIP` o nazwie DNS hello `mypublicdns`. Nazwa DNS hello musi być unikatowa, należy dostarczyć własną unikatową nazwę DNS:

```azurecli
azure network public-ip create --resource-group myResourceGroup \
  --location westeurope --name myPublicIP --domain-name-label mypublicdns
```

Dane wyjściowe:

```azurecli
info:    Executing command network public-ip create
+ Looking up hello public ip "myPublicIP"
+ Creating public ip address "myPublicIP"
+ Looking up hello public ip "myPublicIP"
data:    Id                              : /subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/publicIPAddresses/myPublicIP
data:    Name                            : myPublicIP
data:    Type                            : Microsoft.Network/publicIPAddresses
data:    Location                        : westeurope
data:    Provisioning state              : Succeeded
data:    Allocation method               : Dynamic
data:    Idle timeout                    : 4
data:    Domain name label               : mypublicdns
data:    FQDN                            : mypublicdns.westeurope.cloudapp.azure.com
info:    network public-ip create command OK
```

Hello publiczny adres IP jest również zasobem najwyższego poziomu, tak aby było widać, z `azure group show`.

```azurecli
azure group show myResourceGroup --json | jq '.'
```

Dane wyjściowe:

```json
{
"tags": {},
"id": "/subscriptions/guid/resourceGroups/myResourceGroup",
"name": "myResourceGroup",
"provisioningState": "Succeeded",
"location": "westeurope",
"properties": {
    "provisioningState": "Succeeded"
},
"resources": [
    {
    "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/publicIPAddresses/myPublicIP",
    "name": "myPublicIP",
    "type": "publicIPAddresses",
    "location": "westeurope",
    "tags": null
    },
    {
    "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/virtualNetworks/myVnet",
    "name": "myVnet",
    "type": "virtualNetworks",
    "location": "westeurope",
    "tags": null
    },
    {
    "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Storage/storageAccounts/mystorageaccount",
    "name": "mystorageaccount",
    "type": "storageAccounts",
    "location": "westeurope",
    "tags": null
    }
],
"permissions": [
    {
    "actions": [
        "*"
    ],
    "notActions": []
    }
]
}
```

Więcej szczegółów zasobów, w tym hello pełną nazwę domeny (FQDN) domeny podrzędnej hello, za pomocą hello pełną można zbadać `azure network public-ip show` polecenia. została przydzielona logicznie Hello zasobu publicznego adresu IP, ale nie został jeszcze przypisany określony adres. tooobtain adresu IP, który ma tooneed modułu równoważenia obciążenia, które firma Microsoft nie został jeszcze utworzony.

```azurecli
azure network public-ip show myResourceGroup myPublicIP --json | jq '.'
```

Dane wyjściowe:

```json
{
"tags": {},
"publicIpAllocationMethod": "Dynamic",
"dnsSettings": {
    "domainNameLabel": "mypublicdns",
    "fqdn": "mypublicdns.westeurope.cloudapp.azure.com"
},
"idleTimeoutInMinutes": 4,
"provisioningState": "Succeeded",
"etag": "W/\"c63154b3-1130-49b9-a887-877d74d5ebc5\"",
"id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/publicIPAddresses/myPublicIP",
"name": "myPublicIP",
"location": "westeurope"
}
```

## <a name="create-a-load-balancer-and-ip-pools"></a>Tworzenie modułu równoważenia obciążenia i pule adresów IP
Podczas tworzenia modułu równoważenia obciążenia, umożliwia toodistribute ruchu między wieloma maszynami wirtualnymi. Udostępnia również nadmiarowość tooyour aplikacji, uruchamiając wiele maszyn wirtualnych, które odpowiadać toouser żądań w zdarzeniu hello konserwacji lub dużym obciążeniem. Witaj poniższy przykład tworzy moduł równoważenia obciążenia o nazwie `myLoadBalancer`:

```azurecli
azure network lb create --resource-group myResourceGroup --location westeurope \
  --name myLoadBalancer
```

Dane wyjściowe:

```azurecli
info:    Executing command network lb create
+ Looking up hello load balancer "myLoadBalancer"
+ Creating load balancer "myLoadBalancer"
data:    Id                              : /subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer
data:    Name                            : myLoadBalancer
data:    Type                            : Microsoft.Network/loadBalancers
data:    Location                        : westeurope
data:    Provisioning state              : Succeeded
info:    network lb create command OK
```

Naszej usługi równoważenia obciążenia jest dość pusty, więc warto utworzyć niektóre pule adresów IP. Chcemy toocreate dwa pule adresów IP dla naszej usługi równoważenia obciążenia, jedno dla hello frontonu i jeden dla hello zaplecza. puli adresów IP frontonu Hello jest publicznie widoczna. Możliwe jest również hello toowhich lokalizacji, które możemy przypisać hello PIP utworzonej wcześniej. Następnie używamy puli zaplecza hello jako lokalizacji dla naszej tooconnect maszyn wirtualnych do. W ten sposób hello ruch mógł przepływać przez toohello usługi równoważenia obciążenia hello maszyn wirtualnych.

Najpierw utwórz naszych frontonu puli adresów IP. Witaj poniższy przykład tworzy puli frontonu o nazwie `myFrontEndPool`:

```azurecli
azure network lb frontend-ip create --resource-group myResourceGroup \
  --lb-name myLoadBalancer --public-ip-name myPublicIP \
  --name myFrontEndPool
```

Dane wyjściowe:

```azurecli
info:    Executing command network lb frontend-ip create
+ Looking up hello load balancer "myLoadBalancer"
+ Looking up hello public ip "myPublicIP"
+ Updating load balancer "myLoadBalancer"
data:    Name                            : myFrontEndPool
data:    Provisioning state              : Succeeded
data:    Private IP allocation method    : Dynamic
data:    Public IP address id            : /subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/publicIPAddresses/myPublicIP
info:    network lb mySubnet-ip create command OK
```

Należy zwrócić uwagę, jak użyliśmy hello `--public-ip-name` przełącznika toopass w hello `myPublicIP` utworzonej wcześniej. Przypisywanie hello publicznego adresu IP usługi równoważenia obciążenia toohello adres pozwala tooreach maszyn wirtualnych między hello Internet.

Następnie Utwórzmy naszych drugi pula IP teraz naszych ruchu zaplecza. Witaj poniższy przykład tworzy puli zaplecza, o nazwie `myBackEndPool`:

```azurecli
azure network lb address-pool create --resource-group myResourceGroup \
  --lb-name myLoadBalancer --name myBackEndPool
```

Dane wyjściowe:

```azurecli
info:    Executing command network lb address-pool create
+ Looking up hello load balancer "myLoadBalancer"
+ Updating load balancer "myLoadBalancer"
data:    Name                            : myBackEndPool
data:    Provisioning state              : Succeeded
info:    network lb address-pool create command OK
```

Zobaczysz, jak robi naszej usługi równoważenia obciążenia przez wyszukiwanie z `azure network lb show` i badanie danych wyjściowych JSON hello:

```azurecli
azure network lb show myResourceGroup myLoadBalancer --json | jq '.'
```

Dane wyjściowe:

```json
{
  "etag": "W/\"29c38649-77d6-43ff-ab8f-977536b0047c\"",
  "provisioningState": "Succeeded",
  "resourceGuid": "f1446acb-09ba-44d9-b8b6-849d9983dc09",
  "outboundNatRules": [],
  "inboundNatPools": [],
  "inboundNatRules": [],
  "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer",
  "name": "myLoadBalancer",
  "type": "Microsoft.Network/loadBalancers",
  "location": "westeurope",
  "mySubnetIPConfigurations": [
    {
      "etag": "W/\"29c38649-77d6-43ff-ab8f-977536b0047c\"",
      "name": "myFrontEndPool",
      "provisioningState": "Succeeded",
      "publicIPAddress": {
        "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/publicIPAddresses/myPublicIP"
      },
      "privateIPAllocationMethod": "Dynamic",
      "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/mySubnetIPConfigurations/myFrontEndPool"
    }
  ],
  "backendAddressPools": [
    {
      "etag": "W/\"29c38649-77d6-43ff-ab8f-977536b0047c\"",
      "name": "myBackEndPool",
      "provisioningState": "Succeeded",
      "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/backendAddressPools/myBackEndPool"
    }
  ],
  "loadBalancingRules": [],
  "probes": []
}
```

## <a name="create-load-balancer-nat-rules"></a>Tworzenie reguł NAT modułu równoważenia obciążenia
ruch tooget przepływających przez naszych modułu równoważenia obciążenia, potrzebujemy toocreate sieci adresu translacji adresów reguł określających działania ruchu przychodzącego lub wychodzącego. Należy określić hello toouse protokołu, a następnie mapują porty toointernal portów zewnętrznych zgodnie z potrzebami. W naszym środowisku Utwórzmy niektórych reguł, które umożliwiają SSH za pośrednictwem naszego tooour usługi równoważenia obciążenia maszyn wirtualnych. Port TCP portów 4222 i 4223 toodirect tooTCP 22 skonfigurowanie na naszych maszyn wirtualnych (które możemy utworzyć później). Witaj poniższy przykład powoduje utworzenie reguły o nazwie `myLoadBalancerRuleSSH1` toomap TCP port 4222 tooport 22:

```azurecli
azure network lb inbound-nat-rule create --resource-group myResourceGroup \
  --lb-name myLoadBalancer --name myLoadBalancerRuleSSH1 \
  --protocol tcp --frontend-port 4222 --backend-port 22
```

Dane wyjściowe:

```azurecli
info:    Executing command network lb inbound-nat-rule create
+ Looking up hello load balancer "myLoadBalancer"
warn:    Using default enable floating ip: false
warn:    Using default idle timeout: 4
warn:    Using default mySubnet IP configuration "myFrontEndPool"
+ Updating load balancer "myLoadBalancer"
data:    Name                            : myLoadBalancerRuleSSH1
data:    Provisioning state              : Succeeded
data:    Protocol                        : Tcp
data:    mySubnet port                   : 4222
data:    Backend port                    : 22
data:    Enable floating IP              : false
data:    Idle timeout in minutes         : 4
data:    mySubnet IP configuration id    : /subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/mySubnetIPConfigurations/myFrontEndPool
info:    network lb inbound-nat-rule create command OK
```

Powtórz procedurę hello drugi reguły NAT dla SSH. Witaj poniższy przykład powoduje utworzenie reguły o nazwie `myLoadBalancerRuleSSH2` toomap TCP port 4223 tooport 22:

```azurecli
azure network lb inbound-nat-rule create --resource-group myResourceGroup \
  --lb-name myLoadBalancer --name myLoadBalancerRuleSSH2 --protocol tcp \
  --frontend-port 4223 --backend-port 22
```

Umożliwia również Przejdź dalej i utworzyć regułę NAT dla portu TCP 80 dla ruchu w sieci web, Podłączanie reguły hello tooour pule adresów IP. Jeśli firma Microsoft dołączenie tooan reguły hello puli IP, a Podłączanie hello reguły tooour maszyny wirtualne pojedynczo, firma Microsoft można dodawać i usuwać maszyn wirtualnych z hello puli adresów IP. Moduł równoważenia obciążenia Hello automatycznie dostosowuje hello przepływu ruchu. Witaj poniższy przykład powoduje utworzenie reguły o nazwie `myLoadBalancerRuleWeb` toomap TCP port 80 tooport 80:

```azurecli
azure network lb rule create --resource-group myResourceGroup \
  --lb-name myLoadBalancer --name myLoadBalancerRuleWeb --protocol tcp \
  --frontend-port 80 --backend-port 80 --frontend-ip-name myFrontEndPool \
  --backend-address-pool-name myBackEndPool
```

Dane wyjściowe:

```azurecli
info:    Executing command network lb rule create
+ Looking up hello load balancer "myLoadBalancer"
warn:    Using default idle timeout: 4
warn:    Using default enable floating ip: false
warn:    Using default load distribution: Default
+ Updating load balancer "myLoadBalancer"
data:    Name                            : myLoadBalancerRuleWeb
data:    Provisioning state              : Succeeded
data:    Protocol                        : Tcp
data:    mySubnet port                   : 80
data:    Backend port                    : 80
data:    Enable floating IP              : false
data:    Load distribution               : Default
data:    Idle timeout in minutes         : 4
data:    mySubnet IP configuration id    : /subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/mySubnetIPConfigurations/myFrontEndPool
data:    Backend address pool id         : /subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/backendAddressPools/myBackEndPool
info:    network lb rule create command OK
```

## <a name="create-a-load-balancer-health-probe"></a>Utwórz kondycji sondę modułu równoważenia obciążenia
Kondycję okresowo badania kontroli hello maszyn wirtualnych, które znajdują się za naszych się, że ich działania i odpowiada toorequests zgodnie z definicją toomake usługi równoważenia obciążenia. Jeśli nie są usuwane z tooensure operacji, które użytkownicy nie są kierowane toothem. Można zdefiniować niestandardowe sprawdza, czy hello sondy kondycji, oraz odstępach czasu i wartości limitu czasu. Aby uzyskać więcej informacji na temat sondy kondycji, zobacz [sondy modułu równoważenia obciążenia](../../load-balancer/load-balancer-custom-probe-overview.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json). Witaj poniższy przykład tworzy TCP kondycji sondowany o nazwie `myHealthProbe`:

```azurecli
azure network lb probe create --resource-group myResourceGroup \
  --lb-name myLoadBalancer --name myHealthProbe --protocol "tcp" \
  --interval 15 --count 4
```

Dane wyjściowe:

```azurecli
info:    Executing command network lb probe create
warn:    Using default probe port: 80
+ Looking up hello load balancer "myLoadBalancer"
+ Updating load balancer "myLoadBalancer"
data:    Name                            : myHealthProbe
data:    Provisioning state              : Succeeded
data:    Protocol                        : Tcp
data:    Port                            : 80
data:    Interval in seconds             : 15
data:    Number of probes                : 4
info:    network lb probe create command OK
```

W tym miejscu możemy określony interwał 15 sekund dla naszych kontroli kondycji. Firma Microsoft może pominąć maksymalnie cztery sond (jedną minutę), zanim hello modułu równoważenia obciążenia uzna, że nie działa na tym hoście hello.

## <a name="verify-hello-load-balancer"></a>Sprawdź hello modułu równoważenia obciążenia
Po zakończeniu konfiguracji usługi równoważenia obciążenia hello. Poniżej przedstawiono kroki hello, wykonane:

1. Utworzono usługę równoważenia obciążenia.
2. Utworzyć pulę IP frontonu i przypisane publicznego tooit IP.
3. Została utworzona pula adresów IP zaplecza, która maszyny wirtualne mogą nawiązać połączenie.
4. Utworzono reguł NAT, zezwalających na maszynach wirtualnych toohello SSH do zarządzania, oraz regułę zezwalającą port TCP 80 dla aplikacji sieci web.
5. Po dodaniu kondycji sondowania tooperiodically wyboru hello maszyn wirtualnych. Tej sondy kondycji gwarantuje, że użytkownicy nie próbują tooaccess maszynę Wirtualną, która jest już nie działa lub obsługę zawartości.

Umożliwia przeglądanie jak teraz wygląda przez moduł równoważenia obciążenia:

```azurecli
azure network lb show --resource-group myResourceGroup \
  --name myLoadBalancer --json | jq '.'
```

Dane wyjściowe:

```json
{
  "etag": "W/\"62a7c8e7-859c-48d3-8e76-5e078c5e4a02\"",
  "provisioningState": "Succeeded",
  "resourceGuid": "f1446acb-09ba-44d9-b8b6-849d9983dc09",
  "outboundNatRules": [],
  "inboundNatPools": [],
  "inboundNatRules": [
    {
      "etag": "W/\"62a7c8e7-859c-48d3-8e76-5e078c5e4a02\"",
      "name": "myLoadBalancerRuleSSH1",
      "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/inboundNatRules/myLoadBalancerRuleSSH1",
      "mySubnetIPConfiguration": {
        "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/mySubnetIPConfigurations/myFrontEndPool"
      },
      "protocol": "Tcp",
      "mySubnetPort": 4222,
      "backendPort": 22,
      "idleTimeoutInMinutes": 4,
      "enableFloatingIP": false,
      "provisioningState": "Succeeded"
    },
    {
      "etag": "W/\"62a7c8e7-859c-48d3-8e76-5e078c5e4a02\"",
      "name": "myLoadBalancerRuleSSH2",
      "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/inboundNatRules/myLoadBalancerRuleSSH2",
      "mySubnetIPConfiguration": {
        "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/mySubnetIPConfigurations/myFrontEndPool"
      },
      "protocol": "Tcp",
      "mySubnetPort": 4223,
      "backendPort": 22,
      "idleTimeoutInMinutes": 4,
      "enableFloatingIP": false,
      "provisioningState": "Succeeded"
    }
  ],
  "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer",
  "name": "myLoadBalancer",
  "type": "Microsoft.Network/loadBalancers",
  "location": "westeurope",
  "mySubnetIPConfigurations": [
    {
      "etag": "W/\"62a7c8e7-859c-48d3-8e76-5e078c5e4a02\"",
      "name": "myFrontEndPool",
      "provisioningState": "Succeeded",
      "publicIPAddress": {
        "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/publicIPAddresses/myPublicIP"
      },
      "privateIPAllocationMethod": "Dynamic",
      "loadBalancingRules": [
        {
          "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/loadBalancingRules/myLoadBalancerRuleWeb"
        }
      ],
      "inboundNatRules": [
        {
          "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/inboundNatRules/myLoadBalancerRuleSSH1"
        },
        {
          "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/inboundNatRules/myLoadBalancerRuleSSH2"
        }
      ],
      "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/mySubnetIPConfigurations/myFrontEndPool"
    }
  ],
  "backendAddressPools": [
    {
      "etag": "W/\"62a7c8e7-859c-48d3-8e76-5e078c5e4a02\"",
      "name": "myBackEndPool",
      "provisioningState": "Succeeded",
      "loadBalancingRules": [
        {
          "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/loadBalancingRules/myLoadBalancerRuleWeb"
        }
      ],
      "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/backendAddressPools/myBackEndPool"
    }
  ],
  "loadBalancingRules": [
    {
      "etag": "W/\"62a7c8e7-859c-48d3-8e76-5e078c5e4a02\"",
      "name": "myLoadBalancerRuleWeb",
      "provisioningState": "Succeeded",
      "enableFloatingIP": false,
      "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/loadBalancingRules/myLoadBalancerRuleWeb",
      "mySubnetIPConfiguration": {
        "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/mySubnetIPConfigurations/myFrontEndPool"
      },
      "backendAddressPool": {
        "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/backendAddressPools/myBackEndPool"
      },
      "protocol": "Tcp",
      "loadDistribution": "Default",
      "mySubnetPort": 80,
      "backendPort": 80,
      "idleTimeoutInMinutes": 4
    }
  ],
  "probes": [
    {
      "etag": "W/\"62a7c8e7-859c-48d3-8e76-5e078c5e4a02\"",
      "name": "myHealthProbe",
      "provisioningState": "Succeeded",
      "numberOfProbes": 4,
      "intervalInSeconds": 15,
      "port": 80,
      "protocol": "Tcp",
      "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/probes/myHealthProbe"
    }
  ]
}
```

## <a name="create-an-nic-toouse-with-hello-linux-vm"></a>Utwórz toouse karty Sieciowej z hello maszyny Wirtualnej systemu Linux
Karty sieciowe są programowo dostępne, ponieważ możesz zastosować zasady tootheir użycia. Może także zawierać więcej niż jeden. W następujących hello `azure network nic create` polecenia Podłączanie hello kart toohello obciążenia zaplecza puli adresów IP i powiązać ją z hello ruchu SSH toopermit reguły NAT.

Zastąp hello `#####-###-###` sekcje z identyfikatorem subskrypcji platformy Azure Identyfikator jest odnotowany w danych wyjściowych hello subskrypcji `jq` podczas badania zasobów hello tworzenia. Można również wyświetlić identyfikator subskrypcji z `azure account list`.

Witaj poniższy przykład tworzy karty Sieciowej o nazwie `myNic1`:

```azurecli
azure network nic create --resource-group myResourceGroup --location westeurope \
  --subnet-vnet-name myVnet --subnet-name mySubnet --name myNic1 \
  --lb-address-pool-ids /subscriptions/########-####-####-####-############/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/backendAddressPools/myBackEndPool \
  --lb-inbound-nat-rule-ids /subscriptions/########-####-####-####-############/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/inboundNatRules/myLoadBalancerRuleSSH1
```

Dane wyjściowe:

```azurecli
info:    Executing command network nic create
+ Looking up hello subnet "mySubnet"
+ Looking up hello network interface "myNic1"
+ Creating network interface "myNic1"
data:    Id                              : /subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/networkInterfaces/myNic1
data:    Name                            : myNic1
data:    Type                            : Microsoft.Network/networkInterfaces
data:    Location                        : westeurope
data:    Provisioning state              : Succeeded
data:    Enable IP forwarding            : false
data:    IP configurations:
data:      Name                          : Nic-IP-config
data:      Provisioning state            : Succeeded
data:      Private IP address            : 192.168.1.4
data:      Private IP allocation method  : Dynamic
data:      Subnet                        : /subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/virtualNetworks/myVnet/subnets/mySubnet
data:      Load balancer backend address pools:
data:        Id                          : /subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/backendAddressPools/myBackEndPool
data:      Load balancer inbound NAT rules:
data:        Id                          : /subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/inboundNatRules/myLoadBalancerRuleSSH1
data:
info:    network nic create command OK
```

Można wyświetlić szczegóły hello, sprawdzając zasobów hello bezpośrednio. Należy zbadać hello zasobów za pomocą hello `azure network nic show` polecenia:

```azurecli
azure network nic show myResourceGroup myNic1 --json | jq '.'
```

Dane wyjściowe:

```json
{
  "etag": "W/\"fc1eaaa1-ee55-45bd-b847-5a08c7f4264a\"",
  "provisioningState": "Succeeded",
  "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/networkInterfaces/myNic1",
  "name": "myNic1",
  "type": "Microsoft.Network/networkInterfaces",
  "location": "westeurope",
  "ipConfigurations": [
    {
      "etag": "W/\"fc1eaaa1-ee55-45bd-b847-5a08c7f4264a\"",
      "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/networkInterfaces/myNic1/ipConfigurations/Nic-IP-config",
      "loadBalancerBackendAddressPools": [
        {
          "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/backendAddressPools/myBackEndPool"
        }
      ],
      "loadBalancerInboundNatRules": [
        {
          "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/inboundNatRules/myLoadBalancerRuleSSH1"
        }
      ],
      "privateIPAddress": "192.168.1.4",
      "privateIPAllocationMethod": "Dynamic",
      "subnet": {
        "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/virtualNetworks/myVnet/subnets/mySubnet"
      },
      "provisioningState": "Succeeded",
      "name": "Nic-IP-config"
    }
  ],
  "dnsSettings": {
    "appliedDnsServers": [],
    "dnsServers": []
  },
  "enableIPForwarding": false,
  "resourceGuid": "a20258b8-6361-45f6-b1b4-27ffed28798c"
}
```

Teraz utworzymy hello drugiej karty Sieciowej, przechwytywanie w puli adresów IP zaplecza tooour ponownie. Ta druga reguły NAT czasu hello zezwala na ruch protokołu SSH. Witaj poniższy przykład tworzy karty Sieciowej o nazwie `myNic2`:

```azurecli
azure network nic create --resource-group myResourceGroup --location westeurope \
  --subnet-vnet-name myVnet --subnet-name mySubnet --name myNic2 \
  --lb-address-pool-ids  /subscriptions/########-####-####-####-############/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/backendAddressPools/myBackEndPool \
  --lb-inbound-nat-rule-ids /subscriptions/########-####-####-####-############/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/inboundNatRules/myLoadBalancerRuleSSH2
```

## <a name="create-a-network-security-group-and-rules"></a>Utwórz grupę zabezpieczeń sieci i reguł
Po wprowadzeniu Utwórz grupę zabezpieczeń sieci i hello reguły ruchu przychodzącego, które kontrolują dostęp toohello karty sieciowej. Grupa zabezpieczeń sieci może być zastosowane tooa karty Sieciowej lub podsieci. Należy zdefiniować reguły toocontrol hello przepływu ruchu do i z maszyn wirtualnych. Witaj poniższy przykład tworzy sieciową grupę zabezpieczeń o nazwie `myNetworkSecurityGroup`:

```azurecli
azure network nsg create --resource-group myResourceGroup --location westeurope \
  --name myNetworkSecurityGroup
```

Dodajmy hello regułę ruchu przychodzącego dla hello NSG tooallow przychodzących połączeń na porcie 22 (toosupport SSH). Witaj poniższy przykład powoduje utworzenie reguły o nazwie `myNetworkSecurityGroupRuleSSH` tooallow ruch TCP na porcie 22:

```azurecli
azure network nsg rule create --resource-group myResourceGroup \
  --nsg-name myNetworkSecurityGroup --protocol tcp --direction inbound \
  --priority 1000 --destination-port-range 22 --access allow \
  --name myNetworkSecurityGroupRuleSSH
```

Teraz Dodajmy hello regułę ruchu przychodzącego dla hello NSG tooallow przychodzących połączeń na porcie 80 (toosupport ruchu w sieci web). Witaj poniższy przykład powoduje utworzenie reguły o nazwie `myNetworkSecurityGroupRuleHTTP` tooallow ruch TCP na porcie 80:

```azurecli
azure network nsg rule create --resource-group myResourceGroup \
  --nsg-name myNetworkSecurityGroup --protocol tcp --direction inbound \
  --priority 1001 --destination-port-range 80 --access allow \
  --name myNetworkSecurityGroupRuleHTTP
```

> [!NOTE]
> reguły dla ruchu przychodzącego Hello jest filtrem dla połączeń sieciowych dla ruchu przychodzącego. W tym przykładzie mamy powiązać hello NSG toohello maszyn wirtualnych wirtualnej karty Sieciowej, co oznacza, że wszystkie żądania tooport 22 jest przekazywana toohello karty Sieciowej na naszych maszyny Wirtualnej. Tę regułę dla ruchu przychodzącego jest o połączenie sieciowe, a nie o punkt końcowy, który jest co byłoby o we wdrożeniach klasycznych. tooopen port musi pozostać hello `--source-port-range` ustawić także "\*" tooaccept (wartość domyślna hello) ruchu przychodzącego żądania od **żadnych** żąda portu. Porty są zwykle dynamiczne.
>
>

## <a name="bind-toohello-nic"></a>Powiąż toohello karty Sieciowej
Powiąż hello NSG toohello kart sieciowych. Potrzebujemy tooconnect naszych kart sieciowych z naszej grupy zabezpieczeń sieci. Uruchom zarówno polecenia toohook się naszego kart sieciowych:

```azurecli
azure network nic set --resource-group myResourceGroup --name myNic1 \
  --network-security-group-name myNetworkSecurityGroup
```

```azurecli
azure network nic set --resource-group myResourceGroup --name myNic2 \
  --network-security-group-name myNetworkSecurityGroup
```

## <a name="create-an-availability-set"></a>Tworzenie zestawu dostępności
Zestawy dostępności rozpowszechniania pomocy maszyn wirtualnych w domenach awarii i domen uaktualnienia. Utwórz zbiór dostępności dla maszyn wirtualnych. Witaj poniższy przykład tworzy zbiór nazwanego dostępności `myAvailabilitySet`:

```azurecli
azure availset create --resource-group myResourceGroup --location westeurope
  --name myAvailabilitySet
```

Domen błędów Definiowanie grup maszyn wirtualnych, które współużytkują wspólne przełącznik źródła i sieci zasilania. Domyślnie program hello maszyn wirtualnych, które są skonfigurowane w zestawie dostępności są rozdzielone przez się toothree domen błędów. pomysł Hello jest problemem sprzętowym w jednym z tych domen błędów nie wpływa na każdej maszynie Wirtualnej, która jest uruchomiona aplikacja. Azure automatycznie dystrybuuje maszyn wirtualnych w domenach awarii hello podczas umieszczania ich w zestawie dostępności.

Domen uaktualnienia wskazują grupy maszyn wirtualnych i podstawowym sprzętem fizycznym, który może zostać uruchomiony ponownie na powitania tym samym czasie. kolejność Hello, w którym są ponownie uruchamiane domen uaktualnienia może nie być sekwencyjnych podczas zaplanowanej konserwacji, ale tylko jedno uaktualnienie ponownego uruchomienia w czasie. Ponownie Azure automatycznie dystrybuuje maszyn wirtualnych między domenami uaktualnienia podczas umieszczania ich w witrynie dostępności.

Przeczytaj więcej na temat [Zarządzanie hello dostępność maszyn wirtualnych](manage-availability.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

## <a name="create-hello-linux-vms"></a>Tworzenie maszyn wirtualnych systemu Linux hello
Po utworzeniu hello zasobów magazynu i sieci maszyn wirtualnych toosupport dostępny z Internetu. Teraz załóżmy tworzenie tych maszyn wirtualnych i zabezpieczenia przy użyciu klucza SSH, który nie ma hasła. W takim przypadku zamierzamy toocreate maszyny Wirtualnej systemu Ubuntu oparte na powitania najnowszych LTS. Możemy zlokalizować informacji obrazu przy użyciu `azure vm image list`, zgodnie z opisem w [znajdowanie obrazów maszyn wirtualnych Azure](../windows/cli-ps-findimage.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

Wybraliśmy obrazu za pomocą polecenia hello `azure vm image list westeurope canonical | grep LTS`. W takim przypadku stosujemy `canonical:UbuntuServer:16.04.0-LTS:16.04.201608150`. Dla ostatniego pola hello jest przekazywana `latest` tak, aby w przyszłości hello zawsze uzyskujemy hello ostatniej kompilacji. (ciąg hello używamy jest `canonical:UbuntuServer:16.04.0-LTS:16.04.201608150`).

Ten krok dalej jest znane tooanyone, który został już utworzony ssh publicznego i prywatnego klucza rsa pary w systemie Linux lub Mac za pomocą **ssh-keygen - t rsa -b 2048**. Jeśli nie masz żadnych certyfikatów pary kluczy Twojej `~/.ssh` katalogu, można je utworzyć:

* Automatycznie, przy użyciu hello `azure vm create --generate-ssh-keys` opcji.
* Ręcznie, używając [toocreate instrukcje hello je samodzielnie](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

Alternatywnie można użyć hello `--admin-password` tooauthenticate metody połączenia SSH po hello maszyny Wirtualnej jest tworzona. Ta metoda jest zazwyczaj mniej bezpieczna.

Utworzymy hello wirtualna przełączając naszych zasobów i informacji wraz z hello `azure vm create` polecenia:

```azurecli
azure vm create \
  --resource-group myResourceGroup \
  --name myVM1 \
  --location westeurope \
  --os-type linux \
  --availset-name myAvailabilitySet \
  --nic-name myNic1 \
  --vnet-name myVnet \
  --vnet-subnet-name mySubnet \
  --storage-account-name mystorageaccount \
  --image-urn canonical:UbuntuServer:16.04.0-LTS:latest \
  --ssh-publickey-file ~/.ssh/id_rsa.pub \
  --admin-username azureuser
```

Dane wyjściowe:

```azurecli
info:    Executing command vm create
+ Looking up hello VM "myVM1"
info:    Verifying hello public key SSH file: /home/ahmet/.ssh/id_rsa.pub
info:    Using hello VM Size "Standard_DS1"
info:    hello [OS, Data] Disk or image configuration requires storage account
+ Looking up hello storage account mystorageaccount
+ Looking up hello availability set "myAvailabilitySet"
info:    Found an Availability set "myAvailabilitySet"
+ Looking up hello NIC "myNic1"
info:    Found an existing NIC "myNic1"
info:    Found an IP configuration with virtual network subnet id "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/virtualNetworks/myVnet/subnets/mySubnet" in hello NIC "myNic1"
info:    This is an NIC without publicIP configured
info:    hello storage URI 'https://mystorageaccount.blob.core.windows.net/' will be used for boot diagnostics settings, and it can be overwritten by hello parameter input of '--boot-diagnostics-storage-uri'.
info:    vm create command OK
```

Możesz połączyć natychmiast tooyour maszyny Wirtualnej przy użyciu kluczy SSH domyślne. Upewnij się, określ odpowiedni port hello, ponieważ firma Microsoft jest przekazanie za pośrednictwem usługi równoważenia obciążenia hello. (Dla naszych pierwsza maszyna wirtualna, możemy skonfigurować hello NAT reguły tooforward portu 4222 tooour maszyny Wirtualnej).

```bash
ssh ops@mypublicdns.westeurope.cloudapp.azure.com -p 4222
```

Dane wyjściowe:

```bash
hello authenticity of host '[mypublicdns.westeurope.cloudapp.azure.com]:4222 ([xx.xx.xx.xx]:4222)' can't be established.
ECDSA key fingerprint is 94:2d:d0:ce:6b:fb:7f:ad:5b:3c:78:93:75:82:12:f9.
Are you sure you want toocontinue connecting (yes/no)? yes
Warning: Permanently added '[mypublicdns.westeurope.cloudapp.azure.com]:4222,[xx.xx.xx.xx]:4222' (ECDSA) toohello list of known hosts.
Welcome tooUbuntu 16.04.1 LTS (GNU/Linux 4.4.0-34-generic x86_64)

 * Documentation:  https://help.ubuntu.com
 * Management:     https://landscape.canonical.com
 * Support:        https://ubuntu.com/advantage

  Get cloud support with Ubuntu Advantage Cloud Guest:
    http://www.ubuntu.com/business/services/cloud

0 packages can be updated.
0 updates are security updates.

ops@myVM1:~$
```

Przejdź dalej i utworzyć drugi maszyny Wirtualnej w hello tak samo jak:

```azurecli
azure vm create \
  --resource-group myResourceGroup \
  --name myVM2 \
  --location westeurope \
  --os-type linux \
  --availset-name myAvailabilitySet \
  --nic-name myNic2 \
  --vnet-name myVnet \
  --vnet-subnet-name mySubnet \
  --storage-account-name mystorageaccount \
  --image-urn canonical:UbuntuServer:16.04.0-LTS:latest \
  --ssh-publickey-file ~/.ssh/id_rsa.pub \
  --admin-username azureuser
```

I można teraz używać hello `azure vm show myResourceGroup myVM1` polecenia tooexamine został utworzony. W tym momencie używasz Ubuntu maszyn wirtualnych za modułem równoważenia obciążenia w Azure, który użytkownik może zalogować się do tylko z Twojej pary kluczy SSH (ponieważ haseł są wyłączone). Można zainstalować nginx lub host z wieloma adresami, wdrażanie aplikacji sieci web i widoczny ruch hello przepływ przez tooboth usługi równoważenia obciążenia hello hello maszyn wirtualnych.

```azurecli
azure vm show --resource-group myResourceGroup --name myVM1
```

Dane wyjściowe:

```azurecli
info:    Executing command vm show
+ Looking up hello VM "TestVM1"
+ Looking up hello NIC "myNic1"
data:    Id                              :/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Compute/virtualMachines/myVM1
data:    ProvisioningState               :Succeeded
data:    Name                            :myVM1
data:    Location                        :westeurope
data:    Type                            :Microsoft.Compute/virtualMachines
data:
data:    Hardware Profile:
data:      Size                          :Standard_DS1
data:
data:    Storage Profile:
data:      Image reference:
data:        Publisher                   :canonical
data:        Offer                       :UbuntuServer
data:        Sku                         :16.04.0-LTS
data:        Version                     :latest
data:
data:      OS Disk:
data:        OSType                      :Linux
data:        Name                        :clib45a8b650f4428a1-os-1471973896525
data:        Caching                     :ReadWrite
data:        CreateOption                :FromImage
data:        Vhd:
data:          Uri                       :https://mystorageaccount.blob.core.windows.net/vhds/clib45a8b650f4428a1-os-1471973896525.vhd
data:
data:    OS Profile:
data:      Computer Name                 :myVM1
data:      User Name                     :ops
data:      Linux Configuration:
data:        Disable Password Auth       :true
data:
data:    Network Profile:
data:      Network Interfaces:
data:        Network Interface #1:
data:          Primary                   :true
data:          MAC Address               :00-0D-3A-24-D4-AA
data:          Provisioning State        :Succeeded
data:          Name                      :LmyNic1
data:          Location                  :westeurope
data:
data:    AvailabilitySet:
data:      Id                            :/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Compute/availabilitySets/myAvailabilitySet
data:
data:    Diagnostics Profile:
data:      BootDiagnostics Enabled       :true
data:      BootDiagnostics StorageUri    :https://mystorageaccount.blob.core.windows.net/
data:
data:      Diagnostics Instance View:
info:    vm show command OK

```


## <a name="export-hello-environment-as-a-template"></a>Eksportuj środowiska hello jako szablon
Teraz, to środowisko, co zrobić, jeśli chcesz toocreate mają wbudowane dodatkowe środowiska hello takie same parametry lub w środowisku produkcyjnym, odpowiadający jej? Menedżer zasobów używa szablony JSON, definiują wszystkie parametry hello w danym środowisku. Limit całego środowiska kompilacji, umieszczając odwołanie do tego szablonu JSON. Możesz [ręcznie utworzyć szablony JSON](../../resource-group-authoring-templates.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) lub wyeksportować istniejącego środowiska toocreate hello JSON szablonu dla Ciebie:

```azurecli
azure group export --name myResourceGroup
```

To polecenie tworzy hello `myResourceGroup.json` plik w bieżącym katalogu roboczym. Podczas tworzenia środowiska z tego szablonu, wyświetlany jest monit dla wszystkich nazw zasobów hello, w tym nazwy hello hello modułu równoważenia obciążenia, interfejsów sieciowych lub maszyn wirtualnych. Można go wypełnić te nazwy w pliku szablonu, dodając hello `-p` lub `--includeParameterDefaultValue` toohello parametru `azure group export` polecenia, która została przedstawiona wcześniej. Edytowanie nazwy JSON szablonu toospecify hello zasobów lub [Tworzenie pliku parameters.JSON następującym kodem](../../resource-group-authoring-templates.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) określający hello nazw zasobów.

toocreate środowisko z szablonu:

```azurecli
azure group deployment create --resource-group myNewResourceGroup \
  --template-file myResourceGroup.json
```

Może być tooread [więcej informacji na temat toodeploy z szablonów](../../resource-group-template-deploy-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json). Więcej informacji na temat jak tooincrementally środowisk aktualizacji, użyj pliku parametrów hello i uzyskiwać dostęp do szablonów z lokalizacji magazynu jednego.

## <a name="next-steps"></a>Następne kroki
Teraz wszystko jest gotowe toobegin Praca z wielu składników sieciowych i maszyn wirtualnych. Za pomocą hello podstawowe składniki wprowadzone w tym miejscu, można użyć tej próbki toobuild środowiska limit aplikacji.
