---
title: "aaaCreate maszynę Wirtualną za pomocą statycznego publicznego adresu IP - Azure CLI 2.0 | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toocreate maszyny Wirtualnej z statyczny publiczny adres IP przy użyciu hello Azure interfejsu wiersza polecenia (CLI) 2.0."
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 55bc21b0-2a45-4943-a5e7-8d785d0d015c
ms.service: virtual-network
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/15/2016
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 486060463486462dd8336734a7ad23c4a2cba452
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-vm-with-a-static-public-ip-address-using-hello-azure-cli-20"></a>Utwórz maszynę Wirtualną z statycznego publicznego adresu IP za pomocą hello Azure CLI 2.0

> [!div class="op_single_selector"]
> * [Witryna Azure Portal](virtual-network-deploy-static-pip-arm-portal.md)
> * [PowerShell](virtual-network-deploy-static-pip-arm-ps.md)
> * [Interfejs wiersza polecenia platformy Azure 2.0](virtual-network-deploy-static-pip-arm-cli.md)
> * [Interfejs wiersza polecenia platformy Azure 1.0](virtual-network-deploy-static-pip-cli-nodejs.md)
> * [Szablon](virtual-network-deploy-static-pip-arm-template.md)
> * [PowerShell (klasyczny)](virtual-networks-reserved-public-ip.md)

[!INCLUDE [virtual-network-deploy-static-pip-intro-include.md](../../includes/virtual-network-deploy-static-pip-intro-include.md)]

Platforma Azure ma dwa różne modele wdrażania do tworzenia i pracy z zasobami: [Resource Manager i Model Klasyczny](../resource-manager-deployment-model.md?toc=%2fazure%2fvirtual-network%2ftoc.json). W tym artykule omówiono przy użyciu modelu wdrażania usługi Resource Manager hello, które firma Microsoft zaleca dla większości nowych wdrożeń zamiast hello klasycznego modelu wdrażania.

[!INCLUDE [virtual-network-deploy-static-pip-scenario-include.md](../../includes/virtual-network-deploy-static-pip-scenario-include.md)]

## <a name = "create"></a>Utwórz hello maszyny Wirtualnej

Można wykonać tego zadania przy użyciu hello Azure CLI 2.0 (w tym artykule) lub hello [Azure CLI 1.0](virtual-network-deploy-static-pip-cli-nodejs.md). Witaj wartości "" hello zmiennych w hello czynności, które wykonują Utwórz zasoby przy użyciu ustawień z hello scenariusza. Zmień wartości hello, zgodnie z potrzebami, dla danego środowiska.

1. Zainstaluj hello [Azure CLI 2.0](/cli/azure/install-az-cli2) Jeśli nie masz już zainstalowany.
2. Tworzenie SSH publiczne i prywatne parę kluczy dla maszyn wirtualnych systemu Linux, wykonując kroki hello hello [tworzenie SSH publiczne i prywatne parę kluczy dla maszyn wirtualnych systemu Linux](../virtual-machines/linux/mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-network%2ftoc.json).
3. Z powłoki poleceń, zaloguj się za pomocą polecenia hello `az login`.
4. Wykonywanie skryptu hello, znajdujący się na komputerze z systemem Linux lub Mac, aby utworzyć hello maszyny Wirtualnej. Hello Azure publicznego adresu IP, sieci wirtualnej, interfejsu sieciowego i zasobów maszyny Wirtualnej muszą istnieć w hello sam lokalizacji. Chociaż hello zasoby nie wszystkie zawierają tooexist hello tej samej grupie zasobów w hello następującego skryptu, jak.

```bash
RgName="IaaSStory"
Location="westus"

# Create a resource group.

az group create \
--name $RgName \
--location $Location

# Create a public IP address resource with a static IP address using hello --allocation-method Static option.
# If you do not specify this option, hello address is allocated dynamically. hello address is assigned toothe
# resource from a pool of IP adresses unique tooeach Azure region. hello DnsName must be unique within the
# Azure location it's created in. Download and view hello file from https://www.microsoft.com/en-us/download/details.aspx?id=41653#
# that lists hello ranges for each region.

PipName="PIPWEB1"
DnsName="iaasstoryws1"
az network public-ip create \
--name $PipName \
--resource-group $RgName \
--location $Location \
--allocation-method Static \
--dns-name $DnsName

# Create a virtual network with one subnet

VnetName="TestVNet"
VnetPrefix="192.168.0.0/16"
SubnetName="FrontEnd"
SubnetPrefix="192.168.1.0/24"
az network vnet create \
--name $VnetName \
--resource-group $RgName \
--location $Location \
--address-prefix $VnetPrefix \
--subnet-name $SubnetName \
--subnet-prefix $SubnetPrefix

# Create a network interface connected toohello VNet with a static private IP address and associate hello public IP address
# resource toohello NIC.

NicName="NICWEB1"
PrivateIpAddress="192.168.1.101"
az network nic create \
--name $NicName \
--resource-group $RgName \
--location $Location \
--subnet $SubnetName \
--vnet-name $VnetName \
--private-ip-address $PrivateIpAddress \
--public-ip-address $PipName

# Create a new VM with hello NIC

VmName="WEB1"

# Replace hello value for hello VmSize variable with a value from the
# https://docs.microsoft.com/azure/virtual-machines/virtual-machines-linux-sizes article.
VmSize="Standard_DS1"

# Replace hello value for hello OsImage variable with a value for *urn* from hello output returned by entering
# hello `az vm image list` command. 

OsImage="credativ:Debian:8:latest"
Username='adminuser'

# Replace hello following value with hello path tooyour public key file.
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
# If creating a Windows VM, remove hello previous line and you'll be prompted for hello password you want tooconfigure for hello VM.
```

Ponadto toocreating Maszynę wirtualną, hello skrypt tworzy:
- Pojedynczy premium zarządzać dysku domyślnie, ale ma inne opcje hello typu dysku, które można utworzyć. Witaj odczytu [Utwórz Maszynę wirtualną systemu Linux przy użyciu hello Azure CLI 2.0](../virtual-machines/linux/quick-create-cli.md?toc=%2fazure%2fvirtual-network%2ftoc.json) artykułu, aby uzyskać szczegółowe informacje.
- Sieci wirtualnej, podsieci, kart Sieciowych i zasobów publicznych adresów IP. Alternatywnie można użyć *istniejących* sieci wirtualnej, podsieci, karta sieciowa lub zasobów publicznych adresów IP. toolearn jak toouse istniejących zasobów sieciowych, a nie tworzenia dodatkowych zasobów, wprowadź `az vm create -h`.

## <a name = "validate"></a>Sprawdź poprawność tworzenia maszyny Wirtualnej i publiczny adres IP

1. Wprowadź polecenie hello `az resource list --resouce-group IaaSStory --output table` toosee listę zasobów hello utworzony przez skrypt hello. Zwrócone dane wyjściowe hello powinna być pięć zasobów: sieci interfejsu, dysków, publiczny adres IP, sieci wirtualnej i maszyny wirtualnej.
2. Wprowadź polecenie hello `az network public-ip show --name PIPWEB1 --resource-group IaaSStory --output table`. Hello zwrócone dane wyjściowe, zanotuj wartość hello **IpAddress** i tej wartości hello **PublicIpAllocationMethod** jest *statycznych*.
3. Przed wykonaniem hello następujące polecenia, należy usunąć hello <>, Zastąp *Username* o nazwie hello używana na potrzeby hello **Username** zmiennej skryptu hello i Zastąp *ipAddress* z hello **ipAddress** hello w poprzednim kroku. Witaj uruchom następujące polecenie toohello tooconnect maszyny Wirtualnej: `ssh -i ~/.ssh/azure_id_rsa <Username>@<ipAddress>`. 

## <a name= "clean-up"></a>Usuń hello maszyny Wirtualnej i skojarzonych zasobów

Zalecane jest, aby usunąć zasoby hello utworzone w tym ćwiczeniu, jeśli nie używasz ich w środowisku produkcyjnym. Maszyna wirtualna, publiczny adres IP i zasoby dyskowe spowodować naliczenie opłat, pod warunkiem, że zainicjowano obsługę administracyjną. zasoby hello tooremove utworzone w tym ćwiczeniu pełną hello następujące kroki:

1. tooview hello zasoby w grupie zasobów hello, uruchom hello `az resource list --resource-group IaaSStory` polecenia.
2. Upewnij się, że nie ma żadnych zasobów w grupie zasobów hello, innego niż zasobów hello utworzony przez skrypt hello w tym artykule. 
3. wszystkie zasoby są tworzone w tym ćwiczeniu Uruchom hello toodelete `az group delete -n IaaSStory` polecenia. polecenie Hello usuwa hello grupy zasobów i wszystkie zasoby hello, które zawiera.

## <a name="next-steps"></a>Następne kroki

Dowolny ruch sieciowy może przepływać tooand z hello maszyny Wirtualnej utworzone w tym artykule. Można zdefiniować reguły ruchu przychodzącego i wychodzącego w ramach grupy NSG, ograniczające hello ruchu, który może przepływać tooand z interfejsem sieciowym hello i/lub hello podsieci. więcej informacji na temat grup NSG, przeczytaj hello toolearn [omówienie NSG](virtual-networks-nsg.md) artykułu.
