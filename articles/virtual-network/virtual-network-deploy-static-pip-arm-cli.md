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
# <a name="create-a-vm-with-a-static-public-ip-address-using-hello-azure-cli-20"></a><span data-ttu-id="c6ddf-103">Utwórz maszynę Wirtualną z statycznego publicznego adresu IP za pomocą hello Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="c6ddf-103">Create a VM with a static public IP address using hello Azure CLI 2.0</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="c6ddf-104">Witryna Azure Portal</span><span class="sxs-lookup"><span data-stu-id="c6ddf-104">Azure portal</span></span>](virtual-network-deploy-static-pip-arm-portal.md)
> * [<span data-ttu-id="c6ddf-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="c6ddf-105">PowerShell</span></span>](virtual-network-deploy-static-pip-arm-ps.md)
> * [<span data-ttu-id="c6ddf-106">Interfejs wiersza polecenia platformy Azure 2.0</span><span class="sxs-lookup"><span data-stu-id="c6ddf-106">Azure CLI 2.0</span></span>](virtual-network-deploy-static-pip-arm-cli.md)
> * [<span data-ttu-id="c6ddf-107">Interfejs wiersza polecenia platformy Azure 1.0</span><span class="sxs-lookup"><span data-stu-id="c6ddf-107">Azure CLI 1.0</span></span>](virtual-network-deploy-static-pip-cli-nodejs.md)
> * [<span data-ttu-id="c6ddf-108">Szablon</span><span class="sxs-lookup"><span data-stu-id="c6ddf-108">Template</span></span>](virtual-network-deploy-static-pip-arm-template.md)
> * [<span data-ttu-id="c6ddf-109">PowerShell (klasyczny)</span><span class="sxs-lookup"><span data-stu-id="c6ddf-109">PowerShell (Classic)</span></span>](virtual-networks-reserved-public-ip.md)

[!INCLUDE [virtual-network-deploy-static-pip-intro-include.md](../../includes/virtual-network-deploy-static-pip-intro-include.md)]

<span data-ttu-id="c6ddf-110">Platforma Azure ma dwa różne modele wdrażania do tworzenia i pracy z zasobami: [Resource Manager i Model Klasyczny](../resource-manager-deployment-model.md?toc=%2fazure%2fvirtual-network%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="c6ddf-110">Azure has two different deployment models for creating and working with resources: [Resource Manager and classic](../resource-manager-deployment-model.md?toc=%2fazure%2fvirtual-network%2ftoc.json).</span></span> <span data-ttu-id="c6ddf-111">W tym artykule omówiono przy użyciu modelu wdrażania usługi Resource Manager hello, które firma Microsoft zaleca dla większości nowych wdrożeń zamiast hello klasycznego modelu wdrażania.</span><span class="sxs-lookup"><span data-stu-id="c6ddf-111">This article covers using hello Resource Manager deployment model, which Microsoft recommends for most new deployments instead of hello classic deployment model.</span></span>

[!INCLUDE [virtual-network-deploy-static-pip-scenario-include.md](../../includes/virtual-network-deploy-static-pip-scenario-include.md)]

## <span data-ttu-id="c6ddf-112"><a name = "create"></a>Utwórz hello maszyny Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="c6ddf-112"><a name = "create"></a>Create hello VM</span></span>

<span data-ttu-id="c6ddf-113">Można wykonać tego zadania przy użyciu hello Azure CLI 2.0 (w tym artykule) lub hello [Azure CLI 1.0](virtual-network-deploy-static-pip-cli-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="c6ddf-113">You can complete this task using hello Azure CLI 2.0 (this article) or hello [Azure CLI 1.0](virtual-network-deploy-static-pip-cli-nodejs.md).</span></span> <span data-ttu-id="c6ddf-114">Witaj wartości "" hello zmiennych w hello czynności, które wykonują Utwórz zasoby przy użyciu ustawień z hello scenariusza.</span><span class="sxs-lookup"><span data-stu-id="c6ddf-114">hello values in "" for hello variables in hello steps that follow create resources with settings from hello scenario.</span></span> <span data-ttu-id="c6ddf-115">Zmień wartości hello, zgodnie z potrzebami, dla danego środowiska.</span><span class="sxs-lookup"><span data-stu-id="c6ddf-115">Change hello values, as appropriate, for your environment.</span></span>

1. <span data-ttu-id="c6ddf-116">Zainstaluj hello [Azure CLI 2.0](/cli/azure/install-az-cli2) Jeśli nie masz już zainstalowany.</span><span class="sxs-lookup"><span data-stu-id="c6ddf-116">Install hello [Azure CLI 2.0](/cli/azure/install-az-cli2) if you don't already have it installed.</span></span>
2. <span data-ttu-id="c6ddf-117">Tworzenie SSH publiczne i prywatne parę kluczy dla maszyn wirtualnych systemu Linux, wykonując kroki hello hello [tworzenie SSH publiczne i prywatne parę kluczy dla maszyn wirtualnych systemu Linux](../virtual-machines/linux/mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-network%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="c6ddf-117">Create an SSH public and private key pair for Linux VMs by completing hello steps in hello [Create an SSH public and private key pair for Linux VMs](../virtual-machines/linux/mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-network%2ftoc.json).</span></span>
3. <span data-ttu-id="c6ddf-118">Z powłoki poleceń, zaloguj się za pomocą polecenia hello `az login`.</span><span class="sxs-lookup"><span data-stu-id="c6ddf-118">From a command shell, login with hello command `az login`.</span></span>
4. <span data-ttu-id="c6ddf-119">Wykonywanie skryptu hello, znajdujący się na komputerze z systemem Linux lub Mac, aby utworzyć hello maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="c6ddf-119">Create hello VM by executing hello script that follows on a Linux or Mac computer.</span></span> <span data-ttu-id="c6ddf-120">Hello Azure publicznego adresu IP, sieci wirtualnej, interfejsu sieciowego i zasobów maszyny Wirtualnej muszą istnieć w hello sam lokalizacji.</span><span class="sxs-lookup"><span data-stu-id="c6ddf-120">hello Azure public IP address, virtual network, network interface, and VM resources must all exist in hello same location.</span></span> <span data-ttu-id="c6ddf-121">Chociaż hello zasoby nie wszystkie zawierają tooexist hello tej samej grupie zasobów w hello następującego skryptu, jak.</span><span class="sxs-lookup"><span data-stu-id="c6ddf-121">Though hello resources don't all have tooexist in hello same resource group, in hello following script they do.</span></span>

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

<span data-ttu-id="c6ddf-122">Ponadto toocreating Maszynę wirtualną, hello skrypt tworzy:</span><span class="sxs-lookup"><span data-stu-id="c6ddf-122">In addition toocreating a VM, hello script creates:</span></span>
- <span data-ttu-id="c6ddf-123">Pojedynczy premium zarządzać dysku domyślnie, ale ma inne opcje hello typu dysku, które można utworzyć.</span><span class="sxs-lookup"><span data-stu-id="c6ddf-123">A single premium managed disk by default, but you have other options for hello disk type you can create.</span></span> <span data-ttu-id="c6ddf-124">Witaj odczytu [Utwórz Maszynę wirtualną systemu Linux przy użyciu hello Azure CLI 2.0](../virtual-machines/linux/quick-create-cli.md?toc=%2fazure%2fvirtual-network%2ftoc.json) artykułu, aby uzyskać szczegółowe informacje.</span><span class="sxs-lookup"><span data-stu-id="c6ddf-124">Read hello [Create a Linux VM using hello Azure CLI 2.0](../virtual-machines/linux/quick-create-cli.md?toc=%2fazure%2fvirtual-network%2ftoc.json) article for details.</span></span>
- <span data-ttu-id="c6ddf-125">Sieci wirtualnej, podsieci, kart Sieciowych i zasobów publicznych adresów IP.</span><span class="sxs-lookup"><span data-stu-id="c6ddf-125">Virtual network, subnet, NIC, and public IP address resources.</span></span> <span data-ttu-id="c6ddf-126">Alternatywnie można użyć *istniejących* sieci wirtualnej, podsieci, karta sieciowa lub zasobów publicznych adresów IP.</span><span class="sxs-lookup"><span data-stu-id="c6ddf-126">Alternatively, you can use *existing* virtual network, subnet, NIC, or public IP address resources.</span></span> <span data-ttu-id="c6ddf-127">toolearn jak toouse istniejących zasobów sieciowych, a nie tworzenia dodatkowych zasobów, wprowadź `az vm create -h`.</span><span class="sxs-lookup"><span data-stu-id="c6ddf-127">toolearn how toouse existing network resources rather than creating additional resources, enter `az vm create -h`.</span></span>

## <span data-ttu-id="c6ddf-128"><a name = "validate"></a>Sprawdź poprawność tworzenia maszyny Wirtualnej i publiczny adres IP</span><span class="sxs-lookup"><span data-stu-id="c6ddf-128"><a name = "validate"></a>Validate VM creation and public IP address</span></span>

1. <span data-ttu-id="c6ddf-129">Wprowadź polecenie hello `az resource list --resouce-group IaaSStory --output table` toosee listę zasobów hello utworzony przez skrypt hello.</span><span class="sxs-lookup"><span data-stu-id="c6ddf-129">Enter hello command `az resource list --resouce-group IaaSStory --output table` toosee a list of hello resources created by hello script.</span></span> <span data-ttu-id="c6ddf-130">Zwrócone dane wyjściowe hello powinna być pięć zasobów: sieci interfejsu, dysków, publiczny adres IP, sieci wirtualnej i maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="c6ddf-130">There should be five resources in hello returned output: network interface, disk, public IP address, virtual network, and a virtual machine.</span></span>
2. <span data-ttu-id="c6ddf-131">Wprowadź polecenie hello `az network public-ip show --name PIPWEB1 --resource-group IaaSStory --output table`.</span><span class="sxs-lookup"><span data-stu-id="c6ddf-131">Enter hello command `az network public-ip show --name PIPWEB1 --resource-group IaaSStory --output table`.</span></span> <span data-ttu-id="c6ddf-132">Hello zwrócone dane wyjściowe, zanotuj wartość hello **IpAddress** i tej wartości hello **PublicIpAllocationMethod** jest *statycznych*.</span><span class="sxs-lookup"><span data-stu-id="c6ddf-132">In hello returned output, note hello value of **IpAddress** and that hello value of **PublicIpAllocationMethod** is *Static*.</span></span>
3. <span data-ttu-id="c6ddf-133">Przed wykonaniem hello następujące polecenia, należy usunąć hello <>, Zastąp *Username* o nazwie hello używana na potrzeby hello **Username** zmiennej skryptu hello i Zastąp *ipAddress* z hello **ipAddress** hello w poprzednim kroku.</span><span class="sxs-lookup"><span data-stu-id="c6ddf-133">Before executing hello following command, remove hello <>, replace *Username* with hello name you used for hello **Username** variable in hello script, and replace *ipAddress* with hello **ipAddress** from hello previous step.</span></span> <span data-ttu-id="c6ddf-134">Witaj uruchom następujące polecenie toohello tooconnect maszyny Wirtualnej: `ssh -i ~/.ssh/azure_id_rsa <Username>@<ipAddress>`.</span><span class="sxs-lookup"><span data-stu-id="c6ddf-134">Run hello following command tooconnect toohello VM: `ssh -i ~/.ssh/azure_id_rsa <Username>@<ipAddress>`.</span></span> 

## <span data-ttu-id="c6ddf-135"><a name= "clean-up"></a>Usuń hello maszyny Wirtualnej i skojarzonych zasobów</span><span class="sxs-lookup"><span data-stu-id="c6ddf-135"><a name= "clean-up"></a>Remove hello VM and associated resources</span></span>

<span data-ttu-id="c6ddf-136">Zalecane jest, aby usunąć zasoby hello utworzone w tym ćwiczeniu, jeśli nie używasz ich w środowisku produkcyjnym.</span><span class="sxs-lookup"><span data-stu-id="c6ddf-136">It's recommended that you delete hello resources created in this exercise if you won't use them in production.</span></span> <span data-ttu-id="c6ddf-137">Maszyna wirtualna, publiczny adres IP i zasoby dyskowe spowodować naliczenie opłat, pod warunkiem, że zainicjowano obsługę administracyjną.</span><span class="sxs-lookup"><span data-stu-id="c6ddf-137">VM, public IP address, and disk resources incur charges, as long as they're provisioned.</span></span> <span data-ttu-id="c6ddf-138">zasoby hello tooremove utworzone w tym ćwiczeniu pełną hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="c6ddf-138">tooremove hello resources created during this exercise, complete hello following steps:</span></span>

1. <span data-ttu-id="c6ddf-139">tooview hello zasoby w grupie zasobów hello, uruchom hello `az resource list --resource-group IaaSStory` polecenia.</span><span class="sxs-lookup"><span data-stu-id="c6ddf-139">tooview hello resources in hello resource group, run hello `az resource list --resource-group IaaSStory` command.</span></span>
2. <span data-ttu-id="c6ddf-140">Upewnij się, że nie ma żadnych zasobów w grupie zasobów hello, innego niż zasobów hello utworzony przez skrypt hello w tym artykule.</span><span class="sxs-lookup"><span data-stu-id="c6ddf-140">Confirm there are no resources in hello resource group, other than hello resources created by hello script in this article.</span></span> 
3. <span data-ttu-id="c6ddf-141">wszystkie zasoby są tworzone w tym ćwiczeniu Uruchom hello toodelete `az group delete -n IaaSStory` polecenia.</span><span class="sxs-lookup"><span data-stu-id="c6ddf-141">toodelete all resources created in this exercise, run hello `az group delete -n IaaSStory` command.</span></span> <span data-ttu-id="c6ddf-142">polecenie Hello usuwa hello grupy zasobów i wszystkie zasoby hello, które zawiera.</span><span class="sxs-lookup"><span data-stu-id="c6ddf-142">hello command deletes hello resource group and all hello resources it contains.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c6ddf-143">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="c6ddf-143">Next steps</span></span>

<span data-ttu-id="c6ddf-144">Dowolny ruch sieciowy może przepływać tooand z hello maszyny Wirtualnej utworzone w tym artykule.</span><span class="sxs-lookup"><span data-stu-id="c6ddf-144">Any network traffic can flow tooand from hello VM created in this article.</span></span> <span data-ttu-id="c6ddf-145">Można zdefiniować reguły ruchu przychodzącego i wychodzącego w ramach grupy NSG, ograniczające hello ruchu, który może przepływać tooand z interfejsem sieciowym hello i/lub hello podsieci.</span><span class="sxs-lookup"><span data-stu-id="c6ddf-145">You can define inbound and outbound rules within an NSG that limit hello traffic that can flow tooand from hello network interface, hello subnet, or both.</span></span> <span data-ttu-id="c6ddf-146">więcej informacji na temat grup NSG, przeczytaj hello toolearn [omówienie NSG](virtual-networks-nsg.md) artykułu.</span><span class="sxs-lookup"><span data-stu-id="c6ddf-146">toolearn more about NSGs, read hello [NSG overview](virtual-networks-nsg.md) article.</span></span>
