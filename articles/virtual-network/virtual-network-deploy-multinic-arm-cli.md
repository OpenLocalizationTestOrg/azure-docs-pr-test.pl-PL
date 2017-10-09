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
# <a name="create-a-vm-with-multiple-nics-using-hello-azure-cli-20"></a><span data-ttu-id="43eec-103">Utwórz maszynę Wirtualną z wieloma kartami sieciowymi przy użyciu hello Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="43eec-103">Create a VM with multiple NICs using hello Azure CLI 2.0</span></span>

[!INCLUDE [virtual-network-deploy-multinic-arm-selectors-include.md](../../includes/virtual-network-deploy-multinic-arm-selectors-include.md)]

[!INCLUDE [virtual-network-deploy-multinic-intro-include.md](../../includes/virtual-network-deploy-multinic-intro-include.md)]

> [!NOTE]
> <span data-ttu-id="43eec-104">Platforma Azure oferuje dwa różne modele wdrażania związane z tworzeniem zasobów i pracą z nimi: [model wdrażania przy użyciu usługi Azure Resource Manager i model klasyczny](../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="43eec-104">Azure has two different deployment models for creating and working with resources:  [Resource Manager and classic](../resource-manager-deployment-model.md).</span></span>  <span data-ttu-id="43eec-105">W tym artykule omówiono przy użyciu modelu wdrażania Menedżera zasobów hello, który firma Microsoft zaleca dla większości nowych wdrożeń zamiast hello [klasycznego modelu wdrażania](virtual-network-deploy-multinic-classic-cli.md).</span><span class="sxs-lookup"><span data-stu-id="43eec-105">This article covers using hello Resource Manager deployment model, which Microsoft recommends for most new deployments instead of hello [classic deployment model](virtual-network-deploy-multinic-classic-cli.md).</span></span>
>

## <span data-ttu-id="43eec-106"><a name="create"></a>Utwórz hello maszyny Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="43eec-106"><a name="create"></a>Create hello VM</span></span>

<span data-ttu-id="43eec-107">Można wykonać tego zadania przy użyciu hello Azure CLI 2.0 (w tym artykule) lub hello [Azure CLI 1.0](virtual-network-deploy-multinic-cli-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="43eec-107">You can complete this task using hello Azure CLI 2.0 (this article) or hello [Azure CLI 1.0](virtual-network-deploy-multinic-cli-nodejs.md).</span></span> <span data-ttu-id="43eec-108">Witaj wartości "" hello zmiennych w hello czynności, które wykonują Utwórz zasoby przy użyciu ustawień z hello scenariusza.</span><span class="sxs-lookup"><span data-stu-id="43eec-108">hello values in "" for hello variables in hello steps that follow create resources with settings from hello scenario.</span></span> <span data-ttu-id="43eec-109">Zmień wartości hello, zgodnie z potrzebami, dla danego środowiska.</span><span class="sxs-lookup"><span data-stu-id="43eec-109">Change hello values, as appropriate, for your environment.</span></span>

1. <span data-ttu-id="43eec-110">Zainstaluj hello [Azure CLI 2.0](/cli/azure/install-az-cli2) Jeśli nie masz już zainstalowany.</span><span class="sxs-lookup"><span data-stu-id="43eec-110">Install hello [Azure CLI 2.0](/cli/azure/install-az-cli2) if you don't already have it installed.</span></span>
2. <span data-ttu-id="43eec-111">Tworzenie SSH publiczne i prywatne parę kluczy dla maszyn wirtualnych systemu Linux, wykonując kroki hello hello [tworzenie SSH publiczne i prywatne parę kluczy dla maszyn wirtualnych systemu Linux](../virtual-machines/linux/mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-network%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="43eec-111">Create an SSH public and private key pair for Linux VMs by completing hello steps in hello [Create an SSH public and private key pair for Linux VMs](../virtual-machines/linux/mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-network%2ftoc.json).</span></span>
3. <span data-ttu-id="43eec-112">Z powłoki poleceń, zaloguj się za pomocą polecenia hello `az login`.</span><span class="sxs-lookup"><span data-stu-id="43eec-112">From a command shell, login with hello command `az login`.</span></span>
4. <span data-ttu-id="43eec-113">Wykonywanie skryptu hello, znajdujący się na komputerze z systemem Linux lub Mac, aby utworzyć hello maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="43eec-113">Create hello VM by executing hello script that follows on a Linux or Mac computer.</span></span> <span data-ttu-id="43eec-114">Witaj skrypt tworzy grupę zasobów tooit dołączony jedną sieć wirtualną (VNet) z dwoma podsieciami, dwie karty sieciowe i maszyny Wirtualnej z Witaj dwie karty sieciowe.</span><span class="sxs-lookup"><span data-stu-id="43eec-114">hello script creates a resource group, one virtual network (VNet) with two subnets, two NICs, and a VM with hello two NICs attached tooit.</span></span> <span data-ttu-id="43eec-115">Jedna z hello kart sieciowych połączonych tooone podsieć i jest przypisany statyczny adres IP publiczne i prywatne.</span><span class="sxs-lookup"><span data-stu-id="43eec-115">One of hello NICs is connected tooone subnet and is assigned a static public and private IP address.</span></span> <span data-ttu-id="43eec-116">Hello innych kart interfejsu Sieciowego jest połączonych toohello innych podsieci i ma przypisany statycznego prywatnego adresu IP i żadnego publicznego adresu IP.</span><span class="sxs-lookup"><span data-stu-id="43eec-116">hello other NIC is connected toohello other subnet and is assigned a static private IP address and no public IP address.</span></span> <span data-ttu-id="43eec-117">Witaj karty Sieciowej, publiczny adres IP, wirtualnych sieci i zasobów maszyny Wirtualnej muszą istnieć w hello sam lokalizacji i subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="43eec-117">hello NIC, public IP address, virtual network, and VM resources must all exist in hello same location and subscription.</span></span> <span data-ttu-id="43eec-118">Chociaż hello zasoby nie wszystkie zawierają tooexist hello tej samej grupie zasobów w hello następującego skryptu, jak.</span><span class="sxs-lookup"><span data-stu-id="43eec-118">Though hello resources don't all have tooexist in hello same resource group, in hello following script they do.</span></span>

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

<span data-ttu-id="43eec-119">Ponadto toocreating Maszynę wirtualną z dwiema kartami sieciowymi, hello skrypt tworzy:</span><span class="sxs-lookup"><span data-stu-id="43eec-119">In addition toocreating a VM with two NICs, hello script creates:</span></span>
- <span data-ttu-id="43eec-120">Pojedynczy premium zarządzać dysku domyślnie, ale ma inne opcje hello typu dysku, które można utworzyć.</span><span class="sxs-lookup"><span data-stu-id="43eec-120">A single premium managed disk by default, but you have other options for hello disk type you can create.</span></span> <span data-ttu-id="43eec-121">Witaj odczytu [Utwórz Maszynę wirtualną systemu Linux przy użyciu hello Azure CLI 2.0](../virtual-machines/linux/quick-create-cli.md?toc=%2fazure%2fvirtual-network%2ftoc.json) artykułu, aby uzyskać szczegółowe informacje.</span><span class="sxs-lookup"><span data-stu-id="43eec-121">Read hello [Create a Linux VM using hello Azure CLI 2.0](../virtual-machines/linux/quick-create-cli.md?toc=%2fazure%2fvirtual-network%2ftoc.json) article for details.</span></span>
- <span data-ttu-id="43eec-122">Sieć wirtualną z dwiema podsieciami i jeden publiczny adres IP.</span><span class="sxs-lookup"><span data-stu-id="43eec-122">A virtual network with two subnets and a single public IP address.</span></span> <span data-ttu-id="43eec-123">Alternatywnie można użyć *istniejących* sieci wirtualnej, podsieci, karta sieciowa lub zasobów publicznych adresów IP.</span><span class="sxs-lookup"><span data-stu-id="43eec-123">Alternatively, you can use *existing* virtual network, subnet, NIC, or public IP address resources.</span></span> <span data-ttu-id="43eec-124">toolearn jak toouse istniejących zasobów sieciowych, a nie tworzenia dodatkowych zasobów, wprowadź `az vm create -h`.</span><span class="sxs-lookup"><span data-stu-id="43eec-124">toolearn how toouse existing network resources rather than creating additional resources, enter `az vm create -h`.</span></span>

## <span data-ttu-id="43eec-125"><a name = "validate"></a>Sprawdź poprawność sieciowych i tworzenia maszyny Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="43eec-125"><a name = "validate"></a>Validate VM creation and NICs</span></span>

1. <span data-ttu-id="43eec-126">Wprowadź polecenie hello `az resource list --resouce-group Multi-NIC-VM --output table` toosee listę zasobów hello utworzony przez skrypt hello.</span><span class="sxs-lookup"><span data-stu-id="43eec-126">Enter hello command `az resource list --resouce-group Multi-NIC-VM --output table` toosee a list of hello resources created by hello script.</span></span> <span data-ttu-id="43eec-127">Zwrócone dane wyjściowe hello powinna być sześć zasobów: dwie karty sieciowe, jeden dysk, jeden publiczny adres IP, co sieć wirtualna i maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="43eec-127">There should be six resources in hello returned output: Two NICs, one disk, one public IP address, one virtual network, and a virtual machine.</span></span>
2. <span data-ttu-id="43eec-128">Wprowadź polecenie hello `az network public-ip show --name PIP-WEB --resource-group Multi-NIC-VM --output table`.</span><span class="sxs-lookup"><span data-stu-id="43eec-128">Enter hello command `az network public-ip show --name PIP-WEB --resource-group Multi-NIC-VM --output table`.</span></span> <span data-ttu-id="43eec-129">Hello zwrócone dane wyjściowe, zanotuj wartość hello **IpAddress** i tej wartości hello **PublicIpAllocationMethod** jest *statycznych*.</span><span class="sxs-lookup"><span data-stu-id="43eec-129">In hello returned output, note hello value of **IpAddress** and that hello value of **PublicIpAllocationMethod** is *Static*.</span></span>
3. <span data-ttu-id="43eec-130">Przed uruchomieniem hello następujące polecenia, należy usunąć hello <>, Zastąp *Username* o nazwie hello używana na potrzeby hello **Username** zmiennej skryptu hello i Zastąp *ipAddress* z hello **ipAddress** hello w poprzednim kroku.</span><span class="sxs-lookup"><span data-stu-id="43eec-130">Before running hello following command, remove hello <>, replace *Username* with hello name you used for hello **Username** variable in hello script, and replace *ipAddress* with hello **ipAddress** from hello previous step.</span></span> <span data-ttu-id="43eec-131">Witaj uruchom następujące polecenie toohello tooconnect maszyny Wirtualnej: `ssh -i ~/.ssh/azure_id_rsa <Username>@<ipAddress>`.</span><span class="sxs-lookup"><span data-stu-id="43eec-131">Run hello following command tooconnect toohello VM: `ssh -i ~/.ssh/azure_id_rsa <Username>@<ipAddress>`.</span></span> 
4. <span data-ttu-id="43eec-132">Po nawiązaniu połączenia toohello maszyny Wirtualnej, należy uruchomić hello `sudo ifconfig` toosee polecenia *eth0* i *eth1* interfejsów.</span><span class="sxs-lookup"><span data-stu-id="43eec-132">Once connected toohello VM, run hello `sudo ifconfig` command toosee *eth0* and *eth1* interfaces.</span></span> <span data-ttu-id="43eec-133">Poszczególne karty Sieciowe zostały przypisane hello statyczne prywatne adresy IP określone w skrypcie hello przez serwery Azure DHCP hello.</span><span class="sxs-lookup"><span data-stu-id="43eec-133">Each NIC has been assigned hello static private IP addresses specified in hello script by hello Azure DHCP servers.</span></span> <span data-ttu-id="43eec-134">Witaj adresów IP i MAC, które są przypisane toohello kart sieciowych nie należy zmieniać dopóki powitalne maszyna wirtualna zostanie usunięta.</span><span class="sxs-lookup"><span data-stu-id="43eec-134">hello IP and MAC addresses assigned toohello NICs do not change until hello VM is deleted.</span></span> <span data-ttu-id="43eec-135">Firma Microsoft zaleca, aby nie zmieniać adresy IP w ramach systemu operacyjnego, jak można wyłączyć komputer toohello łączności.</span><span class="sxs-lookup"><span data-stu-id="43eec-135">We recommend that you do not change IP addressing within an operating system, as it can disable connectivity toohello computer.</span></span> <span data-ttu-id="43eec-136">Publiczne adresy IP nie jest wyświetlana w ramach systemu operacyjnego hello, ponieważ są one tooand translacji adresów sieciowych z hello prywatnego adresu IP przez hello infrastruktury platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="43eec-136">Public IP addresses do not appear within hello operating system, as they are network address translated tooand from hello private IP address by hello Azure infrastructure.</span></span>

## <span data-ttu-id="43eec-137"><a name= "clean-up"></a>Usuń hello maszyny Wirtualnej i skojarzonych zasobów</span><span class="sxs-lookup"><span data-stu-id="43eec-137"><a name= "clean-up"></a>Remove hello VM and associated resources</span></span>

<span data-ttu-id="43eec-138">Zalecane jest, aby usunąć zasoby hello utworzone w tym ćwiczeniu, jeśli nie używasz ich w środowisku produkcyjnym.</span><span class="sxs-lookup"><span data-stu-id="43eec-138">It's recommended that you delete hello resources created in this exercise if you won't use them in production.</span></span> <span data-ttu-id="43eec-139">Maszyna wirtualna, publiczny adres IP i zasoby dyskowe spowodować naliczenie opłat, pod warunkiem, że zainicjowano obsługę administracyjną.</span><span class="sxs-lookup"><span data-stu-id="43eec-139">VM, public IP address, and disk resources incur charges, as long as they're provisioned.</span></span> <span data-ttu-id="43eec-140">zasoby hello tooremove utworzone w tym ćwiczeniu pełną hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="43eec-140">tooremove hello resources created during this exercise, complete hello following steps:</span></span>
1. <span data-ttu-id="43eec-141">tooview hello zasoby w grupie zasobów hello, uruchom hello `az resource list --resource-group Multi-NIC-VM` polecenia.</span><span class="sxs-lookup"><span data-stu-id="43eec-141">tooview hello resources in hello resource group, run hello `az resource list --resource-group Multi-NIC-VM` command.</span></span>
2. <span data-ttu-id="43eec-142">Upewnij się, że nie ma żadnych zasobów w grupie zasobów hello, innego niż zasobów hello utworzony przez skrypt hello w tym artykule.</span><span class="sxs-lookup"><span data-stu-id="43eec-142">Confirm there are no resources in hello resource group, other than hello resources created by hello script in this article.</span></span> 
3. <span data-ttu-id="43eec-143">wszystkie zasoby są tworzone w tym ćwiczeniu Uruchom hello toodelete `az group delete --name Multi-NIC-VM` polecenia.</span><span class="sxs-lookup"><span data-stu-id="43eec-143">toodelete all resources created in this exercise, run hello `az group delete --name Multi-NIC-VM` command.</span></span> <span data-ttu-id="43eec-144">polecenie Hello usuwa hello grupy zasobów i wszystkie zasoby hello, które zawiera.</span><span class="sxs-lookup"><span data-stu-id="43eec-144">hello command deletes hello resource group and all hello resources it contains.</span></span>

## <a name="next-steps"></a><span data-ttu-id="43eec-145">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="43eec-145">Next steps</span></span>

<span data-ttu-id="43eec-146">Dowolny ruch sieciowy może przepływać tooand z hello maszyny Wirtualnej utworzone w tym artykule.</span><span class="sxs-lookup"><span data-stu-id="43eec-146">Any network traffic can flow tooand from hello VM created in this article.</span></span> <span data-ttu-id="43eec-147">Można zdefiniować reguły ruchu przychodzącego i wychodzącego w ramach grupy NSG, ograniczające hello ruchu, który może przepływać tooand z każdego interfejsu sieciowego i każdej podsieci.</span><span class="sxs-lookup"><span data-stu-id="43eec-147">You can define inbound and outbound rules within an NSG that limit hello traffic that can flow tooand from each network interface, each subnet, or both.</span></span> <span data-ttu-id="43eec-148">więcej informacji na temat grup NSG, przeczytaj hello toolearn [omówienie NSG](virtual-networks-nsg.md) artykułu.</span><span class="sxs-lookup"><span data-stu-id="43eec-148">toolearn more about NSGs, read hello [NSG overview](virtual-networks-nsg.md) article.</span></span>
