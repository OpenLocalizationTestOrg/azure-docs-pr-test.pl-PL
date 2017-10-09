---
title: "aaaVM z wielu adresów IP przy użyciu hello Azure CLI 2.0 | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak tooassign wielu adresów IP tooa maszynę wirtualną przy użyciu hello Azure CLI 2.0 | Menedżer zasobów."
services: virtual-network
documentationcenter: na
author: anavinahar
manager: narayan
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 11/17/2016
ms.author: annahar
ms.openlocfilehash: 15efd853cc7c31bacb64ed052dabedd3fe4d3079
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="assign-multiple-ip-addresses-toovirtual-machines-using-hello-azure-cli-20"></a>Przypisz wielu adresów IP maszyn toovirtual za pomocą hello Azure CLI 2.0

[!INCLUDE [virtual-network-multiple-ip-addresses-intro.md](../../includes/virtual-network-multiple-ip-addresses-intro.md)]

W tym artykule opisano, jak toocreate maszynę wirtualną (VM) za pośrednictwem hello Azure Resource Manager deployment model przy użyciu hello Azure CLI 2.0. Wiele adresów IP nie można przypisać tooresources został utworzony za pomocą hello klasycznego modelu wdrażania. więcej informacji na temat modeli wdrażania platformy Azure, przeczytaj hello toolearn [zrozumieć modele wdrażania](../resource-manager-deployment-model.md) artykułu.

[!INCLUDE [virtual-network-multiple-ip-addresses-template-scenario.md](../../includes/virtual-network-multiple-ip-addresses-scenario.md)]

## <a name = "create"></a>Utwórz maszynę Wirtualną z wielu adresów IP

Można wykonać tego zadania przy użyciu hello Azure CLI 2.0 (w tym artykule) lub hello [Azure CLI 1.0](virtual-network-multiple-ip-addresses-cli-nodejs.md). Zmień wartości hello, zgodnie z potrzebami, dla danego środowiska. Hello przestrzeganie objaśniono sposób toocreate przykład maszynę Wirtualną za pomocą wielu IP adresów, zgodnie z opisem w scenariuszu hello. Zmienianie wartości zmiennej "" i typy adresów IP zgodnie z wymaganiami implementacji. 

1. Zainstaluj hello [Azure CLI 2.0](/cli/azure/install-az-cli2) Jeśli nie masz już zainstalowany.
2. Tworzenie SSH publiczne i prywatne parę kluczy dla maszyn wirtualnych systemu Linux, wykonując kroki hello hello [tworzenie SSH publiczne i prywatne parę kluczy dla maszyn wirtualnych systemu Linux](../virtual-machines/linux/mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-network%2ftoc.json).
3. Z powłoki poleceń, zaloguj się za pomocą polecenia hello `az login` i wybierz subskrypcję hello używasz.
4. Wykonywanie skryptu hello, znajdujący się na komputerze z systemem Linux lub Mac, aby utworzyć hello maszyny Wirtualnej. skrypt Hello tworzy grupę zasobów, jedną sieć wirtualną (VNet), jedną kartą Sieciową o trzy konfiguracje adresów IP i maszyny Wirtualnej z Witaj dwie karty sieciowe dołączony tooit. Witaj karty Sieciowej, publiczny adres IP, wirtualnych sieci i zasobów maszyny Wirtualnej muszą istnieć w hello sam lokalizacji i subskrypcji. Chociaż hello zasoby nie wszystkie zawierają tooexist hello tej samej grupie zasobów w hello następującego skryptu, jak.

```bash
    
#!/bin/sh
    
RgName="myResourceGroup"
Location="westcentralus"
az group create --name $RgName --location $Location
    
# Create a public IP address resource with a static IP address using hello `--allocation-method Static` option. If you
# do not specify this option, hello address is allocated dynamically. hello address is assigned toohello resource from a pool
# of IP adresses unique tooeach Azure region. Download and view hello file from
# https://www.microsoft.com/en-us/download/details.aspx?id=41653 that lists hello ranges for each region.

PipName="myPublicIP"

# This name must be unique within an Azure location.
DnsName="myDNSName"

az network public-ip create \
--name $PipName \
--resource-group $RgName \
--location $Location \
--dns-name $DnsName\
--allocation-method Static

# Create a virtual network with one subnet

VnetName="myVnet"
VnetPrefix="10.0.0.0/16"
VnetSubnetName="mySubnet"
VnetSubnetPrefix="10.0.0.0/24"

az network vnet create \
--name $VnetName \
--resource-group $RgName \
--location $Location \
--address-prefix $VnetPrefix \
--subnet-name $VnetSubnetName \
--subnet-prefix $VnetSubnetPrefix

# Create a network interface connected toohello subnet and associate hello public IP address tooit. Azure will create the
# first IP configuration with a static private IP address and will associate hello public IP address resource tooit.

NicName="MyNic1"
az network nic create \
--name $NicName \
--resource-group $RgName \
--location $Location \
--subnet $VnetSubnet1Name \
--private-ip-address 10.0.0.4
--vnet-name $VnetName \
--public-ip-address $PipName
    
# Create a second public IP address, a second IP configuration, and associate it toohello NIC. This configuration has a
# static public IP address and a static private IP address.

az network public-ip create \
--resource-group $RgName \
--location $Location \
--name myPublicIP2 \
--dns-name mypublicdns2 \
--allocation-method Static

az network nic ip-config create \
--resource-group $RgName \
--nic-name $NicName \
--name IPConfig-2 \
--private-ip-address 10.0.0.5 \
--public-ip-name myPublicIP2

# Create a third IP configuration, and associate it toohello NIC. This configuration has  static private IP address and # no public IP address.

azure network nic ip-config create \
--resource-group $RgName \
--nic-name $NicName \
--private-ip-address 10.0.0.6 \
--name IPConfig-3

# Note: Though this article assigns all IP configurations tooa single NIC, you can also assign multiple IP configurations
# tooany NIC in a VM. toolearn how toocreate a VM with multiple NICs, read hello Create a VM with multiple NICs 
# article: https://docs.microsoft.com/azure/virtual-network/virtual-network-deploy-multinic-arm-cli.

# Create a VM and attach hello NIC.

VmName="myVm"

# Replace hello value for hello following **VmSize** variable with a value from the
# https://docs.microsoft.com/azure/virtual-machines/virtual-machines-linux-sizes rticle. hello script fails if hello VM size
# is not supported in hello location you select. Run hello `azure vm sizes --location estcentralus` command tooget a full list
# of VMs in US West Central, for example.

VmSize="Standard_DS1"

# Replace hello value for hello OsImage variable value with a value for *urn* from hello utput returned by entering the
# `az vm image list` command.

OsImage="credativ:Debian:8:latest"

Username="adminuser"

# Replace hello following value with hello path tooyour public key file. If you're creating a Windows VM, remove hello following
# line and you'll be prompted for hello password you want tooconfigure for hello VM.

SshKeyValue="~/.ssh/id_rsa.pub"

az vm create \
--name $VmName \
--resource-group $RgName \
--image $OsImage \
--location $Location \
--size $VmSize \
--nics $NicName \
--admin-username $Username \
--ssh-key-value $SshKeyValue
```

Ponadto toocreating Maszynę wirtualną z jedną kartą Sieciową z 3 konfiguracje adresów IP hello skrypt tworzy:

- Pojedynczy premium zarządzać dysku domyślnie, ale ma inne opcje hello typu dysku, które można utworzyć. Witaj odczytu [Utwórz Maszynę wirtualną systemu Linux przy użyciu hello Azure CLI 2.0](../virtual-machines/linux/quick-create-cli.md?toc=%2fazure%2fvirtual-network%2ftoc.json) artykułu, aby uzyskać szczegółowe informacje.
- Sieć wirtualną z jedną podsiecią i dwa publiczne adresy IP. Alternatywnie można użyć *istniejących* sieci wirtualnej, podsieci, karta sieciowa lub zasobów publicznych adresów IP. toolearn jak toouse istniejących zasobów sieciowych, a nie tworzenia dodatkowych zasobów, wprowadź `az vm create -h`.

Publiczne adresy IP ma nominalnego opłatą. więcej informacji o IP adresów o cenach, toolearn odczytu hello [cennik adres IP](https://azure.microsoft.com/pricing/details/ip-addresses) strony. Brak limitu toohello liczba publicznych adresów IP, których można użyć w ramach subskrypcji. więcej informacji na temat limitów hello, przeczytaj hello toolearn [Azure ogranicza](../azure-subscription-service-limits.md#networking-limits) artykułu.

Po utworzeniu hello maszyny Wirtualnej, wprowadź hello `az network nic show --name MyNic1 --resource-group myResourceGroup` konfigurację karty Sieciowej hello tooview polecenia. Wprowadź hello `az network nic ip-config list --nic-name MyNic1 --resource-group myResourceGroup --output table` tooview listę hello konfiguracje adresów IP skojarzonych toohello karty sieciowej.

Dodaj hello prywatnego adresu IP dotyczy systemu operacyjnego maszyny Wirtualnej toohello, wykonując kroki hello systemu operacyjnego w hello [adresów IP Dodaj system operacyjny maszyny Wirtualnej tooa](#os-config) sekcji tego artykułu.

## <a name="add"></a>Dodaj tooa adresów IP maszyny Wirtualnej

Możesz dodać dodatkowe prywatnych i publicznych IP adresów tooan istniejących kart interfejsu Sieciowego, wykonując kroki hello, które należy wykonać. Przykłady Hello zależą od hello [scenariusza](#Scenario) opisane w tym artykule.

1. Otwórz powłokę poleceń i pełne hello pozostałe kroki opisane w tej sekcji w ramach jednej sesji. Jeśli nie masz jeszcze interfejsu wiersza polecenia Azure zainstalowany i skonfigurowany, pełną hello etapami hello [instalacji Azure CLI 2.0](/cli/azure/install-az-cli2?toc=%2fazure%2fvirtual-network%2ftoc.json) tooyour artykułu i logowania konta platformy Azure z hello `az-login` polecenia.

2. Wykonaj kroki hello w jednym z następujących sekcji, w zależności od wymagań hello:

    **Dodaj prywatnego adresu IP**
    
    tooadd prywatnej tooa adresu IP karty Sieciowej, należy utworzyć konfigurację protokołu IP za pomocą polecenia hello, który jest zgodny. Witaj statyczny adres IP musi zawierać adres nieużywane hello podsieci.

    ```bash
    az network nic ip-config create \
    --resource-group myResourceGroup \
    --nic-name myNic1 \
    --private-ip-address 10.0.0.7 \
    --name IPConfig-4
    ```
    
    Tworzenie konfiguracji tyle, ile potrzebujesz, przy użyciu nazwy konfiguracji unikatowy i prywatnych adresów IP (w przypadku konfiguracji statycznych adresów IP).

    **Dodaj publiczny adres IP**
    
    Publiczny adres IP zostanie dodany przez skojarzenie tooeither nową konfigurację adresu IP lub istniejącej konfiguracji adresu IP. Wykonaj kroki hello w jednym z hello kolejnych sekcjach, ile potrzebujesz.

    Publiczne adresy IP ma nominalnego opłatą. więcej informacji o IP adresów o cenach, toolearn odczytu hello [cennik adres IP](https://azure.microsoft.com/pricing/details/ip-addresses) strony. Brak limitu toohello liczba publicznych adresów IP, których można użyć w ramach subskrypcji. więcej informacji na temat limitów hello, przeczytaj hello toolearn [Azure ogranicza](../azure-subscription-service-limits.md#networking-limits) artykułu.

    - **Skojarz hello zasobów tooa nową konfigurację IP**
    
        Po dodaniu publicznego adresu IP w nowej konfiguracji adresu IP, musisz również dodać prywatnego adresu IP, ponieważ wszystkie konfiguracje adresów IP muszą mieć prywatnego adresu IP. Możesz dodać istniejący zasób publiczny adres IP lub Utwórz nową. toocreate nową, wprowadź następujące polecenie hello:
    
        ```bash
        az network public-ip create \
        --resource-group myResourceGroup \
        --location westcentralus \
        --name myPublicIP3 \
        --dns-name mypublicdns3
        ```

        toocreate nowej konfiguracji IP przy użyciu statycznego prywatnego adresu IP i hello skojarzone *myPublicIP3* publicznego adresu IP adresów zasobów, wpisz następujące polecenie hello:

        ```bash
        az network nic ip-config create \
        --resource-group myResourceGroup \
        --nic-name myNic1 \
        --name IPConfig-5 \
        --private-ip-address 10.0.0.8
        --public-ip-address myPublicIP3
        ```

    - **Skojarz hello zasobów tooan istniejącej konfiguracji IP** zasób publicznego adresu IP może być tylko skojarzone tooan konfiguracji adresów IP, który nie ma jeszcze skojarzone. Można określić, czy konfiguracja IP ma skojarzone publicznego adresu IP, wprowadzając następujące polecenie hello:

        ```bash
        az network nic ip-config list \
        --resource-group myResourceGroup \
        --nic-name myNic1 \
        --query "[?provisioningState=='Succeeded'].{ Name: name, PublicIpAddressId: publicIpAddress.id }" --output table
        ```

        Zwrócone dane wyjściowe:
    
            Name        PublicIpAddressId
            
            ipconfig1   /subscriptions/[Id]/resourceGroups/myResourceGroup/providers/Microsoft.Network/publicIPAddresses/myPublicIP1
            IPConfig-2  /subscriptions/[Id]/resourceGroups/myResourceGroup/providers/Microsoft.Network/publicIPAddresses/myPublicIP2
            IPConfig-3

        Ponieważ hello **PublicIpAddressId** kolumny dla *IpConfig 3* pustym hello wyjściowych zasobu bez publicznego adresu IP jest obecnie skojarzone tooit. Można dodać istniejącego publicznego adresu IP adres zasobów tooIpConfig-3, lub wprowadź powitania po toocreate polecenia, co:

        ```bash
        az network public-ip create \
        --resource-group  myResourceGroup
        --location westcentralus \
        --name myPublicIP3 \
        --dns-name mypublicdns3 \
        --allocation-method Static
        ```
    
        Wprowadź następujące polecenie publicznego adresu IP tooassociate hello adresów zasobów toohello istniejącej konfiguracji IP o nazwie hello *IPConfig 3*:
    
        ```bash
        az network nic ip-config update \
        --resource-group myResourceGroup \
        --nic-name myNic1 \
        --name IPConfig-3 \
        --public-ip myPublicIP3
        ```

3. Widok hello prywatnych adresów IP i hello publicznych adresów IP identyfikatorów zasobów przypisane toohello hello karty Sieciowej, wprowadzając następujące polecenie:

    ```bash
    az network nic ip-config list \
    --resource-group myResourceGroup \
    --nic-name myNic1 \
    --query "[?provisioningState=='Succeeded'].{ Name: name, PrivateIpAddress: privateIpAddress, PrivateIpAllocationMethod: privateIpAllocationMethod, PublicIpAddressId: publicIpAddress.id }" --output table
    ```

    Zwrócone dane wyjściowe: <br>
    
        Name        PrivateIpAddress    PrivateIpAllocationMethod   PublicIpAddressId
        
        ipconfig1   10.0.0.4            Static                      /subscriptions/[Id]/resourceGroups/myResourceGroup/providers/Microsoft.Network/publicIPAddresses/myPublicIP1
        IPConfig-2  10.0.0.5            Static                      /subscriptions/[Id]/resourceGroups/myResourceGroup/providers/Microsoft.Network/publicIPAddresses/myPublicIP2
        IPConfig-3  10.0.0.6            Static                      /subscriptions/[Id]/resourceGroups/myResourceGroup/providers/Microsoft.Network/publicIPAddresses/myPublicIP3
    

4. Dodaj hello prywatnych adresów IP systemu operacyjnego maszyny Wirtualnej toohello kart toohello dodane przez instrukcjami hello w hello [adresów IP Dodaj system operacyjny maszyny Wirtualnej tooa](#os-config) sekcji tego artykułu. Nie należy dodawać hello publicznego adresu IP adresów toohello systemu operacyjnego.

[!INCLUDE [virtual-network-multiple-ip-addresses-os-config.md](../../includes/virtual-network-multiple-ip-addresses-os-config.md)]
