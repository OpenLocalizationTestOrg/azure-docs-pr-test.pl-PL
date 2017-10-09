---
title: "aaaCreate Maszynę wirtualną z wieloma kartami sieciowymi — 2.0 interfejsu wiersza polecenia platformy Azure | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toocreate maszyny Wirtualnej z wielu kart sieciowych przy użyciu hello Azure CLI 2.0."
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 8e906a4b-8583-4a97-9416-ee34cfa09a98
ms.service: virtual-network
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/02/2016
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: ac0291a978e2c8682c69104915196cc6c4fcf8dd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-vm-with-multiple-nics-using-hello-azure-cli-20"></a>Utwórz maszynę Wirtualną z wieloma kartami sieciowymi przy użyciu hello Azure CLI 2.0

[!INCLUDE [virtual-network-deploy-multinic-arm-selectors-include.md](../../includes/virtual-network-deploy-multinic-arm-selectors-include.md)]

[!INCLUDE [virtual-network-deploy-multinic-intro-include.md](../../includes/virtual-network-deploy-multinic-intro-include.md)]

> [!NOTE]
> Platforma Azure oferuje dwa różne modele wdrażania związane z tworzeniem zasobów i pracą z nimi: [model wdrażania przy użyciu usługi Azure Resource Manager i model klasyczny](../resource-manager-deployment-model.md).  W tym artykule omówiono przy użyciu modelu wdrażania Menedżera zasobów hello, który firma Microsoft zaleca dla większości nowych wdrożeń zamiast hello [klasycznego modelu wdrażania](virtual-network-deploy-multinic-classic-cli.md).
>

## <a name="create"></a>Utwórz hello maszyny Wirtualnej

Można wykonać tego zadania przy użyciu hello Azure CLI 2.0 (w tym artykule) lub hello [Azure CLI 1.0](virtual-network-deploy-multinic-cli-nodejs.md). Witaj wartości "" hello zmiennych w hello czynności, które wykonują Utwórz zasoby przy użyciu ustawień z hello scenariusza. Zmień wartości hello, zgodnie z potrzebami, dla danego środowiska.

1. Zainstaluj hello [Azure CLI 2.0](/cli/azure/install-az-cli2) Jeśli nie masz już zainstalowany.
2. Tworzenie SSH publiczne i prywatne parę kluczy dla maszyn wirtualnych systemu Linux, wykonując kroki hello hello [tworzenie SSH publiczne i prywatne parę kluczy dla maszyn wirtualnych systemu Linux](../virtual-machines/linux/mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-network%2ftoc.json).
3. Z powłoki poleceń, zaloguj się za pomocą polecenia hello `az login`.
4. Wykonywanie skryptu hello, znajdujący się na komputerze z systemem Linux lub Mac, aby utworzyć hello maszyny Wirtualnej. Witaj skrypt tworzy grupę zasobów tooit dołączony jedną sieć wirtualną (VNet) z dwoma podsieciami, dwie karty sieciowe i maszyny Wirtualnej z Witaj dwie karty sieciowe. Jedna z hello kart sieciowych połączonych tooone podsieć i jest przypisany statyczny adres IP publiczne i prywatne. Hello innych kart interfejsu Sieciowego jest połączonych toohello innych podsieci i ma przypisany statycznego prywatnego adresu IP i żadnego publicznego adresu IP. Witaj karty Sieciowej, publiczny adres IP, wirtualnych sieci i zasobów maszyny Wirtualnej muszą istnieć w hello sam lokalizacji i subskrypcji. Chociaż hello zasoby nie wszystkie zawierają tooexist hello tej samej grupie zasobów w hello następującego skryptu, jak.

```bash
#!/bin/sh

RgName="Multi-NIC-VM"
Location="westus"

# Create a resource group.
az group create \
--name $RgName \
--location $Location

# hello address is assigned toohello resource from a pool of IP adresses unique tooeach Azure region. 
# Download and view hello file from https://www.microsoft.com/en-us/download/details.aspx?id=41653 that lists
# hello ranges for each region.

PipName="PIP-WEB"
az network public-ip create \
--name $PipName \
--resource-group $RgName \
--location $Location \
--allocation-method Static

# Create a virtual network with one subnet

VnetName="VNet1"
VnetPrefix="10.0.0.0/16"
VnetSubnet1Name="Front-End"
VnetSubnet1Prefix="10.0.0.0/24"
az network vnet create \
--name $VnetName \
--resource-group $RgName \
--location $Location \
--address-prefix $VnetPrefix \
--subnet-name $VnetSubnet1Name \
--subnet-prefix $VnetSubnet1Prefix

# Create a second subnet within hello VNet

VnetSubnet2Name="Back-end"
VnetSubnet2Prefix="10.0.1.0/24"
az network vnet subnet create \
--vnet-name $VnetName \
--resource-group $RgName \
--name $VnetSubnet2Name \
--address-prefix $VnetSubnet2Prefix

# Create a network interface connected tooone of hello subnets. hello NIC is assigned a single dynamic private and
# public IP address by default, but you can instead, assign static addresses, or no public IP address at all.
# You can also assign multiple private or public IP addresses tooeach NIC. toolearn more about IP addressing
# options for NICs, enter hello az network nic create -h command.

Nic1Name="NIC-FE"
PrivateIpAddress1="10.0.0.5"

az network nic create \
--name $Nic1Name \
--resource-group $RgName \
--location $Location \
--subnet $VnetSubnet1Name \
--vnet-name $VnetName \
--private-ip-address $PrivateIpAddress1 \
--public-ip-address $PipName

# Create a second network interface and connect it toohello other subnet. Though multiple NICs attached toohello same
# VM can be connected toodifferent subnets, hello subnets must all be within hello same VNet. Add additional NICs as necessary.

Nic2Name="NIC-BE"
PrivateIpAddress2="10.0.1.5"

az network nic create \
--name $Nic2Name \
--resource-group $RgName \
--location $Location \
--subnet $VnetSubnet2Name \
--vnet-name $VnetName \
--private-ip-address $PrivateIpAddress2

# Create a VM and attach hello two NICs.

VmName="WEB"

# Replace hello value for hello following **VmSize** variable with a value from the
# https://docs.microsoft.com/azure/virtual-machines/virtual-machines-linux-sizes article. Not all VM sizes support
# more than one NIC, so be sure tooselect a VM size that supports hello number of NICs you want tooattach toohello VM.
# You must create hello VM with at least two NICs if you want tooadd more after VM creation. If you create a VM with
# only one NIC, you can't add additional NICs toohello VM after VM creation, regardless of how many NICs hello VM supports.
# hello VM size specified in hello following variable supports two NICs.

VmSize="Standard_DS2"

# Replace hello value for hello OsImage variable value with a value for *urn* from hello output returned by entering the
# az vm image list command.

OsImage="credativ:Debian:8:latest"

Username="adminuser"

# Replace hello following value with hello path tooyour public key file.

SshKeyValue="~/.ssh/id_rsa.pub"

# Before executing hello following command, add variable names of additional NICs you may have added toohello script that
# you want tooattach toohello VM. If creating a Windows VM, remove hello **ssh-key-value** line and you'll be prompted for
# hello password you want tooconfigure for hello VM.

az vm create \
--name $VmName \
--resource-group $RgName \
--image $OsImage \
--location $Location \
--size $VmSize \
--nics $Nic1Name $Nic2Name \
--admin-username $Username \
--ssh-key-value $SshKeyValue
```

Ponadto toocreating Maszynę wirtualną z dwiema kartami sieciowymi, hello skrypt tworzy:
- Pojedynczy premium zarządzać dysku domyślnie, ale ma inne opcje hello typu dysku, które można utworzyć. Witaj odczytu [Utwórz Maszynę wirtualną systemu Linux przy użyciu hello Azure CLI 2.0](../virtual-machines/linux/quick-create-cli.md?toc=%2fazure%2fvirtual-network%2ftoc.json) artykułu, aby uzyskać szczegółowe informacje.
- Sieć wirtualną z dwiema podsieciami i jeden publiczny adres IP. Alternatywnie można użyć *istniejących* sieci wirtualnej, podsieci, karta sieciowa lub zasobów publicznych adresów IP. toolearn jak toouse istniejących zasobów sieciowych, a nie tworzenia dodatkowych zasobów, wprowadź `az vm create -h`.

## <a name = "validate"></a>Sprawdź poprawność sieciowych i tworzenia maszyny Wirtualnej

1. Wprowadź polecenie hello `az resource list --resouce-group Multi-NIC-VM --output table` toosee listę zasobów hello utworzony przez skrypt hello. Zwrócone dane wyjściowe hello powinna być sześć zasobów: dwie karty sieciowe, jeden dysk, jeden publiczny adres IP, co sieć wirtualna i maszyny wirtualnej.
2. Wprowadź polecenie hello `az network public-ip show --name PIP-WEB --resource-group Multi-NIC-VM --output table`. Hello zwrócone dane wyjściowe, zanotuj wartość hello **IpAddress** i tej wartości hello **PublicIpAllocationMethod** jest *statycznych*.
3. Przed uruchomieniem hello następujące polecenia, należy usunąć hello <>, Zastąp *Username* o nazwie hello używana na potrzeby hello **Username** zmiennej skryptu hello i Zastąp *ipAddress* z hello **ipAddress** hello w poprzednim kroku. Witaj uruchom następujące polecenie toohello tooconnect maszyny Wirtualnej: `ssh -i ~/.ssh/azure_id_rsa <Username>@<ipAddress>`. 
4. Po nawiązaniu połączenia toohello maszyny Wirtualnej, należy uruchomić hello `sudo ifconfig` toosee polecenia *eth0* i *eth1* interfejsów. Poszczególne karty Sieciowe zostały przypisane hello statyczne prywatne adresy IP określone w skrypcie hello przez serwery Azure DHCP hello. Witaj adresów IP i MAC, które są przypisane toohello kart sieciowych nie należy zmieniać dopóki powitalne maszyna wirtualna zostanie usunięta. Firma Microsoft zaleca, aby nie zmieniać adresy IP w ramach systemu operacyjnego, jak można wyłączyć komputer toohello łączności. Publiczne adresy IP nie jest wyświetlana w ramach systemu operacyjnego hello, ponieważ są one tooand translacji adresów sieciowych z hello prywatnego adresu IP przez hello infrastruktury platformy Azure.

## <a name= "clean-up"></a>Usuń hello maszyny Wirtualnej i skojarzonych zasobów

Zalecane jest, aby usunąć zasoby hello utworzone w tym ćwiczeniu, jeśli nie używasz ich w środowisku produkcyjnym. Maszyna wirtualna, publiczny adres IP i zasoby dyskowe spowodować naliczenie opłat, pod warunkiem, że zainicjowano obsługę administracyjną. zasoby hello tooremove utworzone w tym ćwiczeniu pełną hello następujące kroki:
1. tooview hello zasoby w grupie zasobów hello, uruchom hello `az resource list --resource-group Multi-NIC-VM` polecenia.
2. Upewnij się, że nie ma żadnych zasobów w grupie zasobów hello, innego niż zasobów hello utworzony przez skrypt hello w tym artykule. 
3. wszystkie zasoby są tworzone w tym ćwiczeniu Uruchom hello toodelete `az group delete --name Multi-NIC-VM` polecenia. polecenie Hello usuwa hello grupy zasobów i wszystkie zasoby hello, które zawiera.

## <a name="next-steps"></a>Następne kroki

Dowolny ruch sieciowy może przepływać tooand z hello maszyny Wirtualnej utworzone w tym artykule. Można zdefiniować reguły ruchu przychodzącego i wychodzącego w ramach grupy NSG, ograniczające hello ruchu, który może przepływać tooand z każdego interfejsu sieciowego i każdej podsieci. więcej informacji na temat grup NSG, przeczytaj hello toolearn [omówienie NSG](virtual-networks-nsg.md) artykułu.
