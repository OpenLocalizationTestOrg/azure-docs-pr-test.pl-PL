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
# <a name="assign-multiple-ip-addresses-toovirtual-machines-using-hello-azure-cli-20"></a><span data-ttu-id="ff5ca-103">Przypisz wielu adresów IP maszyn toovirtual za pomocą hello Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="ff5ca-103">Assign multiple IP addresses toovirtual machines using hello Azure CLI 2.0</span></span>

[!INCLUDE [virtual-network-multiple-ip-addresses-intro.md](../../includes/virtual-network-multiple-ip-addresses-intro.md)]

<span data-ttu-id="ff5ca-104">W tym artykule opisano, jak toocreate maszynę wirtualną (VM) za pośrednictwem hello Azure Resource Manager deployment model przy użyciu hello Azure CLI 2.0.</span><span class="sxs-lookup"><span data-stu-id="ff5ca-104">This article explains how toocreate a virtual machine (VM) through hello Azure Resource Manager deployment model using hello Azure CLI 2.0.</span></span> <span data-ttu-id="ff5ca-105">Wiele adresów IP nie można przypisać tooresources został utworzony za pomocą hello klasycznego modelu wdrażania.</span><span class="sxs-lookup"><span data-stu-id="ff5ca-105">Multiple IP addresses cannot be assigned tooresources created through hello classic deployment model.</span></span> <span data-ttu-id="ff5ca-106">więcej informacji na temat modeli wdrażania platformy Azure, przeczytaj hello toolearn [zrozumieć modele wdrażania](../resource-manager-deployment-model.md) artykułu.</span><span class="sxs-lookup"><span data-stu-id="ff5ca-106">toolearn more about Azure deployment models, read hello [Understand deployment models](../resource-manager-deployment-model.md) article.</span></span>

[!INCLUDE [virtual-network-multiple-ip-addresses-template-scenario.md](../../includes/virtual-network-multiple-ip-addresses-scenario.md)]

## <span data-ttu-id="ff5ca-107"><a name = "create"></a>Utwórz maszynę Wirtualną z wielu adresów IP</span><span class="sxs-lookup"><span data-stu-id="ff5ca-107"><a name = "create"></a>Create a VM with multiple IP addresses</span></span>

<span data-ttu-id="ff5ca-108">Można wykonać tego zadania przy użyciu hello Azure CLI 2.0 (w tym artykule) lub hello [Azure CLI 1.0](virtual-network-multiple-ip-addresses-cli-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="ff5ca-108">You can complete this task using hello Azure CLI 2.0 (this article) or hello [Azure CLI 1.0](virtual-network-multiple-ip-addresses-cli-nodejs.md).</span></span> <span data-ttu-id="ff5ca-109">Zmień wartości hello, zgodnie z potrzebami, dla danego środowiska.</span><span class="sxs-lookup"><span data-stu-id="ff5ca-109">Change hello values, as appropriate, for your environment.</span></span> <span data-ttu-id="ff5ca-110">Hello przestrzeganie objaśniono sposób toocreate przykład maszynę Wirtualną za pomocą wielu IP adresów, zgodnie z opisem w scenariuszu hello.</span><span class="sxs-lookup"><span data-stu-id="ff5ca-110">hello steps that follow explain how toocreate an example VM with multiple IP addresses, as described in hello scenario.</span></span> <span data-ttu-id="ff5ca-111">Zmienianie wartości zmiennej "" i typy adresów IP zgodnie z wymaganiami implementacji.</span><span class="sxs-lookup"><span data-stu-id="ff5ca-111">Change variable values in "" and IP address types as required for your implementation.</span></span> 

1. <span data-ttu-id="ff5ca-112">Zainstaluj hello [Azure CLI 2.0](/cli/azure/install-az-cli2) Jeśli nie masz już zainstalowany.</span><span class="sxs-lookup"><span data-stu-id="ff5ca-112">Install hello [Azure CLI 2.0](/cli/azure/install-az-cli2) if you don't already have it installed.</span></span>
2. <span data-ttu-id="ff5ca-113">Tworzenie SSH publiczne i prywatne parę kluczy dla maszyn wirtualnych systemu Linux, wykonując kroki hello hello [tworzenie SSH publiczne i prywatne parę kluczy dla maszyn wirtualnych systemu Linux](../virtual-machines/linux/mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-network%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="ff5ca-113">Create an SSH public and private key pair for Linux VMs by completing hello steps in hello [Create an SSH public and private key pair for Linux VMs](../virtual-machines/linux/mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-network%2ftoc.json).</span></span>
3. <span data-ttu-id="ff5ca-114">Z powłoki poleceń, zaloguj się za pomocą polecenia hello `az login` i wybierz subskrypcję hello używasz.</span><span class="sxs-lookup"><span data-stu-id="ff5ca-114">From a command shell, login with hello command `az login` and select hello subscription you're using.</span></span>
4. <span data-ttu-id="ff5ca-115">Wykonywanie skryptu hello, znajdujący się na komputerze z systemem Linux lub Mac, aby utworzyć hello maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="ff5ca-115">Create hello VM by executing hello script that follows on a Linux or Mac computer.</span></span> <span data-ttu-id="ff5ca-116">skrypt Hello tworzy grupę zasobów, jedną sieć wirtualną (VNet), jedną kartą Sieciową o trzy konfiguracje adresów IP i maszyny Wirtualnej z Witaj dwie karty sieciowe dołączony tooit.</span><span class="sxs-lookup"><span data-stu-id="ff5ca-116">hello script creates a resource group, one virtual network (VNet), one NIC with three IP configurations, and a VM with hello two NICs attached tooit.</span></span> <span data-ttu-id="ff5ca-117">Witaj karty Sieciowej, publiczny adres IP, wirtualnych sieci i zasobów maszyny Wirtualnej muszą istnieć w hello sam lokalizacji i subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="ff5ca-117">hello NIC, public IP address, virtual network, and VM resources must all exist in hello same location and subscription.</span></span> <span data-ttu-id="ff5ca-118">Chociaż hello zasoby nie wszystkie zawierają tooexist hello tej samej grupie zasobów w hello następującego skryptu, jak.</span><span class="sxs-lookup"><span data-stu-id="ff5ca-118">Though hello resources don't all have tooexist in hello same resource group, in hello following script they do.</span></span>

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

<span data-ttu-id="ff5ca-119">Ponadto toocreating Maszynę wirtualną z jedną kartą Sieciową z 3 konfiguracje adresów IP hello skrypt tworzy:</span><span class="sxs-lookup"><span data-stu-id="ff5ca-119">In addition toocreating a VM with a NIC with 3 IP configurations, hello script creates:</span></span>

- <span data-ttu-id="ff5ca-120">Pojedynczy premium zarządzać dysku domyślnie, ale ma inne opcje hello typu dysku, które można utworzyć.</span><span class="sxs-lookup"><span data-stu-id="ff5ca-120">A single premium managed disk by default, but you have other options for hello disk type you can create.</span></span> <span data-ttu-id="ff5ca-121">Witaj odczytu [Utwórz Maszynę wirtualną systemu Linux przy użyciu hello Azure CLI 2.0](../virtual-machines/linux/quick-create-cli.md?toc=%2fazure%2fvirtual-network%2ftoc.json) artykułu, aby uzyskać szczegółowe informacje.</span><span class="sxs-lookup"><span data-stu-id="ff5ca-121">Read hello [Create a Linux VM using hello Azure CLI 2.0](../virtual-machines/linux/quick-create-cli.md?toc=%2fazure%2fvirtual-network%2ftoc.json) article for details.</span></span>
- <span data-ttu-id="ff5ca-122">Sieć wirtualną z jedną podsiecią i dwa publiczne adresy IP.</span><span class="sxs-lookup"><span data-stu-id="ff5ca-122">A virtual network with one subnet and two public IP addresses.</span></span> <span data-ttu-id="ff5ca-123">Alternatywnie można użyć *istniejących* sieci wirtualnej, podsieci, karta sieciowa lub zasobów publicznych adresów IP.</span><span class="sxs-lookup"><span data-stu-id="ff5ca-123">Alternatively, you can use *existing* virtual network, subnet, NIC, or public IP address resources.</span></span> <span data-ttu-id="ff5ca-124">toolearn jak toouse istniejących zasobów sieciowych, a nie tworzenia dodatkowych zasobów, wprowadź `az vm create -h`.</span><span class="sxs-lookup"><span data-stu-id="ff5ca-124">toolearn how toouse existing network resources rather than creating additional resources, enter `az vm create -h`.</span></span>

<span data-ttu-id="ff5ca-125">Publiczne adresy IP ma nominalnego opłatą.</span><span class="sxs-lookup"><span data-stu-id="ff5ca-125">Public IP addresses have a nominal fee.</span></span> <span data-ttu-id="ff5ca-126">więcej informacji o IP adresów o cenach, toolearn odczytu hello [cennik adres IP](https://azure.microsoft.com/pricing/details/ip-addresses) strony.</span><span class="sxs-lookup"><span data-stu-id="ff5ca-126">toolearn more about IP address pricing, read hello [IP address pricing](https://azure.microsoft.com/pricing/details/ip-addresses) page.</span></span> <span data-ttu-id="ff5ca-127">Brak limitu toohello liczba publicznych adresów IP, których można użyć w ramach subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="ff5ca-127">There is a limit toohello number of public IP addresses that can be used in a subscription.</span></span> <span data-ttu-id="ff5ca-128">więcej informacji na temat limitów hello, przeczytaj hello toolearn [Azure ogranicza](../azure-subscription-service-limits.md#networking-limits) artykułu.</span><span class="sxs-lookup"><span data-stu-id="ff5ca-128">toolearn more about hello limits, read hello [Azure limits](../azure-subscription-service-limits.md#networking-limits) article.</span></span>

<span data-ttu-id="ff5ca-129">Po utworzeniu hello maszyny Wirtualnej, wprowadź hello `az network nic show --name MyNic1 --resource-group myResourceGroup` konfigurację karty Sieciowej hello tooview polecenia.</span><span class="sxs-lookup"><span data-stu-id="ff5ca-129">After hello VM is created, enter hello `az network nic show --name MyNic1 --resource-group myResourceGroup` command tooview hello NIC configuration.</span></span> <span data-ttu-id="ff5ca-130">Wprowadź hello `az network nic ip-config list --nic-name MyNic1 --resource-group myResourceGroup --output table` tooview listę hello konfiguracje adresów IP skojarzonych toohello karty sieciowej.</span><span class="sxs-lookup"><span data-stu-id="ff5ca-130">Enter hello `az network nic ip-config list --nic-name MyNic1 --resource-group myResourceGroup --output table` tooview a list of hello IP configurations associated toohello NIC.</span></span>

<span data-ttu-id="ff5ca-131">Dodaj hello prywatnego adresu IP dotyczy systemu operacyjnego maszyny Wirtualnej toohello, wykonując kroki hello systemu operacyjnego w hello [adresów IP Dodaj system operacyjny maszyny Wirtualnej tooa](#os-config) sekcji tego artykułu.</span><span class="sxs-lookup"><span data-stu-id="ff5ca-131">Add hello private IP addresses toohello VM operating system by completing hello steps for your operating system in hello [Add IP addresses tooa VM operating system](#os-config) section of this article.</span></span>

## <span data-ttu-id="ff5ca-132"><a name="add"></a>Dodaj tooa adresów IP maszyny Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="ff5ca-132"><a name="add"></a>Add IP addresses tooa VM</span></span>

<span data-ttu-id="ff5ca-133">Możesz dodać dodatkowe prywatnych i publicznych IP adresów tooan istniejących kart interfejsu Sieciowego, wykonując kroki hello, które należy wykonać.</span><span class="sxs-lookup"><span data-stu-id="ff5ca-133">You can add additional private and public IP addresses tooan existing NIC by completing hello steps that follow.</span></span> <span data-ttu-id="ff5ca-134">Przykłady Hello zależą od hello [scenariusza](#Scenario) opisane w tym artykule.</span><span class="sxs-lookup"><span data-stu-id="ff5ca-134">hello examples build upon hello [scenario](#Scenario) described in this article.</span></span>

1. <span data-ttu-id="ff5ca-135">Otwórz powłokę poleceń i pełne hello pozostałe kroki opisane w tej sekcji w ramach jednej sesji.</span><span class="sxs-lookup"><span data-stu-id="ff5ca-135">Open a command shell and complete hello remaining steps in this section within a single session.</span></span> <span data-ttu-id="ff5ca-136">Jeśli nie masz jeszcze interfejsu wiersza polecenia Azure zainstalowany i skonfigurowany, pełną hello etapami hello [instalacji Azure CLI 2.0](/cli/azure/install-az-cli2?toc=%2fazure%2fvirtual-network%2ftoc.json) tooyour artykułu i logowania konta platformy Azure z hello `az-login` polecenia.</span><span class="sxs-lookup"><span data-stu-id="ff5ca-136">If you don't already have Azure CLI installed and configured, complete hello steps in hello [Azure CLI 2.0 installation](/cli/azure/install-az-cli2?toc=%2fazure%2fvirtual-network%2ftoc.json) article and login tooyour Azure account with hello `az-login` command.</span></span>

2. <span data-ttu-id="ff5ca-137">Wykonaj kroki hello w jednym z następujących sekcji, w zależności od wymagań hello:</span><span class="sxs-lookup"><span data-stu-id="ff5ca-137">Complete hello steps in one of hello following sections, based on your requirements:</span></span>

    <span data-ttu-id="ff5ca-138">**Dodaj prywatnego adresu IP**</span><span class="sxs-lookup"><span data-stu-id="ff5ca-138">**Add a private IP address**</span></span>
    
    <span data-ttu-id="ff5ca-139">tooadd prywatnej tooa adresu IP karty Sieciowej, należy utworzyć konfigurację protokołu IP za pomocą polecenia hello, który jest zgodny.</span><span class="sxs-lookup"><span data-stu-id="ff5ca-139">tooadd a private IP address tooa NIC, you must create an IP configuration using hello command that follows.</span></span> <span data-ttu-id="ff5ca-140">Witaj statyczny adres IP musi zawierać adres nieużywane hello podsieci.</span><span class="sxs-lookup"><span data-stu-id="ff5ca-140">hello static IP address must be an unused address for hello subnet.</span></span>

    ```bash
    az network nic ip-config create \
    --resource-group myResourceGroup \
    --nic-name myNic1 \
    --private-ip-address 10.0.0.7 \
    --name IPConfig-4
    ```
    
    <span data-ttu-id="ff5ca-141">Tworzenie konfiguracji tyle, ile potrzebujesz, przy użyciu nazwy konfiguracji unikatowy i prywatnych adresów IP (w przypadku konfiguracji statycznych adresów IP).</span><span class="sxs-lookup"><span data-stu-id="ff5ca-141">Create as many configurations as you require, using unique configuration names and private IP addresses (for configurations with static IP addresses).</span></span>

    <span data-ttu-id="ff5ca-142">**Dodaj publiczny adres IP**</span><span class="sxs-lookup"><span data-stu-id="ff5ca-142">**Add a public IP address**</span></span>
    
    <span data-ttu-id="ff5ca-143">Publiczny adres IP zostanie dodany przez skojarzenie tooeither nową konfigurację adresu IP lub istniejącej konfiguracji adresu IP.</span><span class="sxs-lookup"><span data-stu-id="ff5ca-143">A public IP address is added by associating it tooeither a new IP configuration or an existing IP configuration.</span></span> <span data-ttu-id="ff5ca-144">Wykonaj kroki hello w jednym z hello kolejnych sekcjach, ile potrzebujesz.</span><span class="sxs-lookup"><span data-stu-id="ff5ca-144">Complete hello steps in one of hello sections that follow, as you require.</span></span>

    <span data-ttu-id="ff5ca-145">Publiczne adresy IP ma nominalnego opłatą.</span><span class="sxs-lookup"><span data-stu-id="ff5ca-145">Public IP addresses have a nominal fee.</span></span> <span data-ttu-id="ff5ca-146">więcej informacji o IP adresów o cenach, toolearn odczytu hello [cennik adres IP](https://azure.microsoft.com/pricing/details/ip-addresses) strony.</span><span class="sxs-lookup"><span data-stu-id="ff5ca-146">toolearn more about IP address pricing, read hello [IP address pricing](https://azure.microsoft.com/pricing/details/ip-addresses) page.</span></span> <span data-ttu-id="ff5ca-147">Brak limitu toohello liczba publicznych adresów IP, których można użyć w ramach subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="ff5ca-147">There is a limit toohello number of public IP addresses that can be used in a subscription.</span></span> <span data-ttu-id="ff5ca-148">więcej informacji na temat limitów hello, przeczytaj hello toolearn [Azure ogranicza](../azure-subscription-service-limits.md#networking-limits) artykułu.</span><span class="sxs-lookup"><span data-stu-id="ff5ca-148">toolearn more about hello limits, read hello [Azure limits](../azure-subscription-service-limits.md#networking-limits) article.</span></span>

    - <span data-ttu-id="ff5ca-149">**Skojarz hello zasobów tooa nową konfigurację IP**</span><span class="sxs-lookup"><span data-stu-id="ff5ca-149">**Associate hello resource tooa new IP configuration**</span></span>
    
        <span data-ttu-id="ff5ca-150">Po dodaniu publicznego adresu IP w nowej konfiguracji adresu IP, musisz również dodać prywatnego adresu IP, ponieważ wszystkie konfiguracje adresów IP muszą mieć prywatnego adresu IP.</span><span class="sxs-lookup"><span data-stu-id="ff5ca-150">Whenever you add a public IP address in a new IP configuration, you must also add a private IP address, because all IP configurations must have a private IP address.</span></span> <span data-ttu-id="ff5ca-151">Możesz dodać istniejący zasób publiczny adres IP lub Utwórz nową.</span><span class="sxs-lookup"><span data-stu-id="ff5ca-151">You can either add an existing public IP address resource, or create a new one.</span></span> <span data-ttu-id="ff5ca-152">toocreate nową, wprowadź następujące polecenie hello:</span><span class="sxs-lookup"><span data-stu-id="ff5ca-152">toocreate a new one, enter hello following command:</span></span>
    
        ```bash
        az network public-ip create \
        --resource-group myResourceGroup \
        --location westcentralus \
        --name myPublicIP3 \
        --dns-name mypublicdns3
        ```

        <span data-ttu-id="ff5ca-153">toocreate nowej konfiguracji IP przy użyciu statycznego prywatnego adresu IP i hello skojarzone *myPublicIP3* publicznego adresu IP adresów zasobów, wpisz następujące polecenie hello:</span><span class="sxs-lookup"><span data-stu-id="ff5ca-153">toocreate a new IP configuration with a static private IP address and hello associated *myPublicIP3* public IP address resource, enter hello following command:</span></span>

        ```bash
        az network nic ip-config create \
        --resource-group myResourceGroup \
        --nic-name myNic1 \
        --name IPConfig-5 \
        --private-ip-address 10.0.0.8
        --public-ip-address myPublicIP3
        ```

    - <span data-ttu-id="ff5ca-154">**Skojarz hello zasobów tooan istniejącej konfiguracji IP** zasób publicznego adresu IP może być tylko skojarzone tooan konfiguracji adresów IP, który nie ma jeszcze skojarzone.</span><span class="sxs-lookup"><span data-stu-id="ff5ca-154">**Associate hello resource tooan existing IP configuration** A public IP address resource can only be associated tooan IP configuration that doesn't already have one associated.</span></span> <span data-ttu-id="ff5ca-155">Można określić, czy konfiguracja IP ma skojarzone publicznego adresu IP, wprowadzając następujące polecenie hello:</span><span class="sxs-lookup"><span data-stu-id="ff5ca-155">You can determine whether an IP configuration has an associated public IP address by entering hello following command:</span></span>

        ```bash
        az network nic ip-config list \
        --resource-group myResourceGroup \
        --nic-name myNic1 \
        --query "[?provisioningState=='Succeeded'].{ Name: name, PublicIpAddressId: publicIpAddress.id }" --output table
        ```

        <span data-ttu-id="ff5ca-156">Zwrócone dane wyjściowe:</span><span class="sxs-lookup"><span data-stu-id="ff5ca-156">Returned output:</span></span>
    
            Name        PublicIpAddressId
            
            ipconfig1   /subscriptions/[Id]/resourceGroups/myResourceGroup/providers/Microsoft.Network/publicIPAddresses/myPublicIP1
            IPConfig-2  /subscriptions/[Id]/resourceGroups/myResourceGroup/providers/Microsoft.Network/publicIPAddresses/myPublicIP2
            IPConfig-3

        <span data-ttu-id="ff5ca-157">Ponieważ hello **PublicIpAddressId** kolumny dla *IpConfig 3* pustym hello wyjściowych zasobu bez publicznego adresu IP jest obecnie skojarzone tooit.</span><span class="sxs-lookup"><span data-stu-id="ff5ca-157">Since hello **PublicIpAddressId** column for *IpConfig-3* is blank in hello output, no public IP address resource is currently associated tooit.</span></span> <span data-ttu-id="ff5ca-158">Można dodać istniejącego publicznego adresu IP adres zasobów tooIpConfig-3, lub wprowadź powitania po toocreate polecenia, co:</span><span class="sxs-lookup"><span data-stu-id="ff5ca-158">You can add an existing public IP address resource tooIpConfig-3, or enter hello following command toocreate one:</span></span>

        ```bash
        az network public-ip create \
        --resource-group  myResourceGroup
        --location westcentralus \
        --name myPublicIP3 \
        --dns-name mypublicdns3 \
        --allocation-method Static
        ```
    
        <span data-ttu-id="ff5ca-159">Wprowadź następujące polecenie publicznego adresu IP tooassociate hello adresów zasobów toohello istniejącej konfiguracji IP o nazwie hello *IPConfig 3*:</span><span class="sxs-lookup"><span data-stu-id="ff5ca-159">Enter hello following command tooassociate hello public IP address resource toohello existing IP configuration named *IPConfig-3*:</span></span>
    
        ```bash
        az network nic ip-config update \
        --resource-group myResourceGroup \
        --nic-name myNic1 \
        --name IPConfig-3 \
        --public-ip myPublicIP3
        ```

3. <span data-ttu-id="ff5ca-160">Widok hello prywatnych adresów IP i hello publicznych adresów IP identyfikatorów zasobów przypisane toohello hello karty Sieciowej, wprowadzając następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="ff5ca-160">View hello private IP addresses and hello public IP address resource Ids assigned toohello NIC by entering hello following command:</span></span>

    ```bash
    az network nic ip-config list \
    --resource-group myResourceGroup \
    --nic-name myNic1 \
    --query "[?provisioningState=='Succeeded'].{ Name: name, PrivateIpAddress: privateIpAddress, PrivateIpAllocationMethod: privateIpAllocationMethod, PublicIpAddressId: publicIpAddress.id }" --output table
    ```

    <span data-ttu-id="ff5ca-161">Zwrócone dane wyjściowe:</span><span class="sxs-lookup"><span data-stu-id="ff5ca-161">Returned output:</span></span> <br>
    
        Name        PrivateIpAddress    PrivateIpAllocationMethod   PublicIpAddressId
        
        ipconfig1   10.0.0.4            Static                      /subscriptions/[Id]/resourceGroups/myResourceGroup/providers/Microsoft.Network/publicIPAddresses/myPublicIP1
        IPConfig-2  10.0.0.5            Static                      /subscriptions/[Id]/resourceGroups/myResourceGroup/providers/Microsoft.Network/publicIPAddresses/myPublicIP2
        IPConfig-3  10.0.0.6            Static                      /subscriptions/[Id]/resourceGroups/myResourceGroup/providers/Microsoft.Network/publicIPAddresses/myPublicIP3
    

4. <span data-ttu-id="ff5ca-162">Dodaj hello prywatnych adresów IP systemu operacyjnego maszyny Wirtualnej toohello kart toohello dodane przez instrukcjami hello w hello [adresów IP Dodaj system operacyjny maszyny Wirtualnej tooa](#os-config) sekcji tego artykułu.</span><span class="sxs-lookup"><span data-stu-id="ff5ca-162">Add hello private IP addresses you added toohello NIC toohello VM operating system by following hello instructions in hello [Add IP addresses tooa VM operating system](#os-config) section of this article.</span></span> <span data-ttu-id="ff5ca-163">Nie należy dodawać hello publicznego adresu IP adresów toohello systemu operacyjnego.</span><span class="sxs-lookup"><span data-stu-id="ff5ca-163">Do not add hello public IP addresses toohello operating system.</span></span>

[!INCLUDE [virtual-network-multiple-ip-addresses-os-config.md](../../includes/virtual-network-multiple-ip-addresses-os-config.md)]
