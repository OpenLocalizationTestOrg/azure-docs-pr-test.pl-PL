---
title: "Wdrażanie maszyn wirtualnych systemu Linux w istniejącej sieci Azure CLI 2.0 | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak wdrożyć maszynę wirtualną systemu Linux w ramach istniejącej sieci wirtualnej przy użyciu 2.0 interfejsu wiersza polecenia platformy Azure"
services: virtual-machines-linux
documentationcenter: virtual-machines
author: iainfoulds
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.workload: infrastructure
ms.tgt_pltfrm: vm-linux
ms.devlang: azurecli
ms.topic: article
ms.date: 05/11/2017
ms.author: iainfou
ms.openlocfilehash: 932fd74ec83f43b604382346ee2c273f5453fcd0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-deploy-a-linux-virtual-machine-into-an-existing-azure-virtual-network-with-the-azure-cli"></a><span data-ttu-id="5770d-103">Jak wdrożyć maszyny wirtualnej systemu Linux w istniejącej sieci wirtualnej platformy Azure z wiersza polecenia platformy Azure</span><span class="sxs-lookup"><span data-stu-id="5770d-103">How to deploy a Linux virtual machine into an existing Azure Virtual Network with the Azure CLI</span></span>

<span data-ttu-id="5770d-104">W tym artykule przedstawiono sposób użycia 2.0 interfejsu wiersza polecenia Azure, aby wdrożyć maszynę wirtualną (VM) do istniejącej sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="5770d-104">This article shows you how to use the Azure CLI 2.0 to deploy a virtual machine (VM) into an existing virtual network.</span></span> <span data-ttu-id="5770d-105">Wymagania są następujące:</span><span class="sxs-lookup"><span data-stu-id="5770d-105">The requirements are:</span></span>

- [<span data-ttu-id="5770d-106">Konto platformy Azure</span><span class="sxs-lookup"><span data-stu-id="5770d-106">an Azure account</span></span>](https://azure.microsoft.com/pricing/free-trial/)
- [<span data-ttu-id="5770d-107">Pliki kluczy publicznych i prywatnych SSH</span><span class="sxs-lookup"><span data-stu-id="5770d-107">SSH public and private key files</span></span>](mac-create-ssh-keys.md)

<span data-ttu-id="5770d-108">Czynności te można również wykonać przy użyciu [interfejsu wiersza polecenia platformy Azure w wersji 1.0](deploy-linux-vm-into-existing-vnet-using-cli-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="5770d-108">You can also perform these steps with the [Azure CLI 1.0](deploy-linux-vm-into-existing-vnet-using-cli-nodejs.md).</span></span>


## <a name="quick-commands"></a><span data-ttu-id="5770d-109">Szybkie polecenia</span><span class="sxs-lookup"><span data-stu-id="5770d-109">Quick Commands</span></span>
<span data-ttu-id="5770d-110">Jeśli chcesz szybko wykonywać zadania poniższej sekcji Szczegóły poleceń potrzebne.</span><span class="sxs-lookup"><span data-stu-id="5770d-110">If you need to quickly accomplish the task, the following section details the  commands needed.</span></span> <span data-ttu-id="5770d-111">Bardziej szczegółowe informacje i kontekst dla każdego kroku można znaleźć pozostałej części dokumentu, [uruchamiania tutaj](#detailed-walkthrough).</span><span class="sxs-lookup"><span data-stu-id="5770d-111">More detailed information and context for each step can be found the rest of the document, [starting here](#detailed-walkthrough).</span></span>

<span data-ttu-id="5770d-112">Do utworzenia tego środowiska niestandardowe, należy najnowszej [Azure CLI 2.0](/cli/azure/install-az-cli2) zainstalowane i zalogowany do konta platformy Azure przy użyciu [logowania az](/cli/azure/#login).</span><span class="sxs-lookup"><span data-stu-id="5770d-112">To create this custom environment, you need the latest [Azure CLI 2.0](/cli/azure/install-az-cli2) installed and logged in to an Azure account using [az login](/cli/azure/#login).</span></span>

<span data-ttu-id="5770d-113">W poniższych przykładach Zastąp przykładowe nazwy parametrów własne wartości.</span><span class="sxs-lookup"><span data-stu-id="5770d-113">In the following examples, replace example parameter names with your own values.</span></span> <span data-ttu-id="5770d-114">Przykład nazwy parametru zawierają *myResourceGroup*, *myVnet*, i *myVM*.</span><span class="sxs-lookup"><span data-stu-id="5770d-114">Example parameter names include *myResourceGroup*, *myVnet*, and *myVM*.</span></span>

<span data-ttu-id="5770d-115">**Wymagania wstępne:** grupy zasobów platformy Azure, sieci wirtualnych i podsieci ruchu przychodzącego grupy zabezpieczeń sieci przy użyciu protokołu SSH i karty interfejsu sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="5770d-115">**Pre-requirements:** Azure resource group, virtual network and subnet, network security group with SSH inbound, and a virtual network interface card.</span></span>

### <a name="deploy-the-vm-into-the-virtual-network-infrastructure"></a><span data-ttu-id="5770d-116">Wdróż maszynę Wirtualną do infrastruktury sieci wirtualnej</span><span class="sxs-lookup"><span data-stu-id="5770d-116">Deploy the VM into the virtual network infrastructure</span></span>

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --image Debian \
    --admin-username azureuser \
    --generate-ssh-keys \
    --nics myNic
```

## <a name="detailed-walkthrough"></a><span data-ttu-id="5770d-117">Szczegółowy przewodnik</span><span class="sxs-lookup"><span data-stu-id="5770d-117">Detailed walkthrough</span></span>

<span data-ttu-id="5770d-118">Azure zasoby, takie jak sieci wirtualnych i grup zabezpieczeń sieci musi być statyczny i tam długo zasoby, które rzadko są wdrożone.</span><span class="sxs-lookup"><span data-stu-id="5770d-118">Azure assets like virtual networks and network security groups should be static and long lived resources that are rarely deployed.</span></span> <span data-ttu-id="5770d-119">Po wdrożeniu sieci wirtualnej można użyć ponownie przez nowych wdrożeń bez żadnych niekorzystny wpływ infrastruktury.</span><span class="sxs-lookup"><span data-stu-id="5770d-119">Once a virtual network has been deployed, it can be reused by new deployments without any adverse affects to the infrastructure.</span></span> <span data-ttu-id="5770d-120">Pomyśleć o sieci wirtualnej jako przełącznik sieciowy tradycyjnych sprzętu — nie musisz skonfigurować nowy przełącznik sprzętu z każdym wdrożeniu.</span><span class="sxs-lookup"><span data-stu-id="5770d-120">Think about a virtual network as being a traditional hardware network switch - you would not need to configure a brand new hardware switch with each deployment.</span></span> <span data-ttu-id="5770d-121">Z sieci wirtualnej prawidłowo skonfigurowany można wdrożyć nowe maszyny wirtualne w tej sieci wirtualnej samodzielnego z kilku ewentualne zmiany wymagane w całej sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="5770d-121">With a correctly configured virtual network, you can continue to deploy new VMs into that virtual network over and over with few, if any, changes required over the life of the virtual network.</span></span>

<span data-ttu-id="5770d-122">Do utworzenia tego środowiska niestandardowe, należy najnowszej [Azure CLI 2.0](/cli/azure/install-az-cli2) zainstalowane i zalogowany do konta platformy Azure przy użyciu [logowania az](/cli/azure/#login).</span><span class="sxs-lookup"><span data-stu-id="5770d-122">To create this custom environment, you need the latest [Azure CLI 2.0](/cli/azure/install-az-cli2) installed and logged in to an Azure account using [az login](/cli/azure/#login).</span></span>

<span data-ttu-id="5770d-123">W poniższych przykładach Zastąp przykładowe nazwy parametrów własne wartości.</span><span class="sxs-lookup"><span data-stu-id="5770d-123">In the following examples, replace example parameter names with your own values.</span></span> <span data-ttu-id="5770d-124">Przykład nazwy parametru zawierają *myResourceGroup*, *myVnet*, i *myVM*.</span><span class="sxs-lookup"><span data-stu-id="5770d-124">Example parameter names include *myResourceGroup*, *myVnet*, and *myVM*.</span></span>

## <a name="create-the-resource-group"></a><span data-ttu-id="5770d-125">Tworzenie grupy zasobów</span><span class="sxs-lookup"><span data-stu-id="5770d-125">Create the resource group</span></span>

<span data-ttu-id="5770d-126">Najpierw należy utworzyć grupy zasobów platformy Azure do organizowania wszystko, czego możesz utworzyć w tym przewodniku.</span><span class="sxs-lookup"><span data-stu-id="5770d-126">First, create an Azure resource group to organize everything you create in this walkthrough.</span></span> <span data-ttu-id="5770d-127">Więcej informacji na temat grup zasobów znajduje się w temacie [Omówienie usługi Azure Resource Manager](../../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="5770d-127">For more information on resource groups, see [Azure Resource Manager overview](../../azure-resource-manager/resource-group-overview.md).</span></span> <span data-ttu-id="5770d-128">Tworzenie grupy zasobów z [Tworzenie grupy az](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="5770d-128">Create the resource group with [az group create](/cli/azure/group#create).</span></span> <span data-ttu-id="5770d-129">Poniższy przykład tworzy grupę zasobów o nazwie *myResourceGroup* w *eastus* lokalizacji:</span><span class="sxs-lookup"><span data-stu-id="5770d-129">The following example creates a resource group named *myResourceGroup* in the *eastus* location:</span></span>

```azurecli
az group create \
    --name myResourceGroup \
    --location eastus
```

## <a name="create-the-virtual-network"></a><span data-ttu-id="5770d-130">Utwórz sieć wirtualną</span><span class="sxs-lookup"><span data-stu-id="5770d-130">Create the virtual network</span></span>

<span data-ttu-id="5770d-131">Umożliwia tworzenie sieci wirtualnej platformy Azure, można uruchomić na maszynach wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="5770d-131">Lets build an Azure virtual network to launch the VMs into.</span></span> <span data-ttu-id="5770d-132">Aby uzyskać więcej informacji o sieciach wirtualnych, zobacz [utworzyć sieć wirtualną przy użyciu interfejsu wiersza polecenia Azure](../../virtual-network/virtual-networks-create-vnet-arm-cli.md).</span><span class="sxs-lookup"><span data-stu-id="5770d-132">For more information on virtual networks, see [Create a virtual network by using the Azure CLI](../../virtual-network/virtual-networks-create-vnet-arm-cli.md).</span></span> <span data-ttu-id="5770d-133">Utwórz sieć wirtualną z [tworzenie sieci wirtualnej sieci az](/cli/azure/network/vnet#create).</span><span class="sxs-lookup"><span data-stu-id="5770d-133">Create the virtual network with [az network vnet create](/cli/azure/network/vnet#create).</span></span> <span data-ttu-id="5770d-134">Poniższy przykład tworzy sieć wirtualną o nazwie *myVnet* i podsieć o nazwie *mySubnet*:</span><span class="sxs-lookup"><span data-stu-id="5770d-134">The following example creates a virtual network named *myVnet* and subnet named *mySubnet*:</span></span>

```azurecli
az network vnet create \
    --resource-group myResourceGroup \
    --location eastus \
    --name myVnet \
    --address-prefix 10.10.0.0/16 \
    --subnet-name mySubnet \
    --subnet-prefix 10.10.1.0/24
```

## <a name="create-the-network-security-group"></a><span data-ttu-id="5770d-135">Utwórz grupę zabezpieczeń sieci</span><span class="sxs-lookup"><span data-stu-id="5770d-135">Create the network security group</span></span>

<span data-ttu-id="5770d-136">Grupy zabezpieczeń sieci platformy Azure są równoważne zapory w warstwie sieci.</span><span class="sxs-lookup"><span data-stu-id="5770d-136">Azure network security groups are equivalent to a firewall at the network layer.</span></span> <span data-ttu-id="5770d-137">Aby uzyskać więcej informacji dotyczących grup zabezpieczeń sieci, zobacz [sposobu tworzenia grup zabezpieczeń sieci na platformie Azure CLI](../../virtual-network/virtual-networks-create-nsg-arm-cli.md).</span><span class="sxs-lookup"><span data-stu-id="5770d-137">For more information on network security groups, see [How to create network security groups in the Azure CLI](../../virtual-network/virtual-networks-create-nsg-arm-cli.md).</span></span> <span data-ttu-id="5770d-138">Utwórz grupę zabezpieczeń sieci z [utworzyć nsg sieci az](/cli/azure/network/nsg#create).</span><span class="sxs-lookup"><span data-stu-id="5770d-138">Create the network security group with [az network nsg create](/cli/azure/network/nsg#create).</span></span> <span data-ttu-id="5770d-139">Poniższy przykład tworzy sieciową grupę zabezpieczeń o nazwie *myNetworkSecurityGroup*:</span><span class="sxs-lookup"><span data-stu-id="5770d-139">The following example creates a network security group named *myNetworkSecurityGroup*:</span></span>

```azurecli
az network nsg create \
    --resource-group myResourceGroup \
    --location eastus \
    --name myNetworkSecurityGroup
```

## <a name="add-an-inbound-ssh-allow-rule"></a><span data-ttu-id="5770d-140">Dodaj regułę Zezwalaj SSH dla ruchu przychodzącego</span><span class="sxs-lookup"><span data-stu-id="5770d-140">Add an inbound SSH allow rule</span></span>

<span data-ttu-id="5770d-141">Maszyna wirtualna wymaga dostępu z Internetu, więc regułę zezwalającą na ruch przychodzący port 22 mają być przekazywane za pośrednictwem sieci do portu 22 na maszynie Wirtualnej nie jest wymagane.</span><span class="sxs-lookup"><span data-stu-id="5770d-141">The VM needs access from the internet, so a rule allowing inbound port 22 traffic to be passed through the network to port 22 on the VM is needed.</span></span> <span data-ttu-id="5770d-142">Dodaj regułę ruchu przychodzącego dla sieciowej grupy zabezpieczeń z [Tworzenie reguły nsg sieci az](/cli/azure/network/nsg/rule#create).</span><span class="sxs-lookup"><span data-stu-id="5770d-142">Add an inbound rule for the network security group with [az network nsg rule create](/cli/azure/network/nsg/rule#create).</span></span> <span data-ttu-id="5770d-143">Poniższy przykład tworzy reguły o nazwie *myNetworkSecurityGroupRuleSSH*:</span><span class="sxs-lookup"><span data-stu-id="5770d-143">The following example creates a rule named *myNetworkSecurityGroupRuleSSH*:</span></span>

```azurecli
az network nsg rule create \
    --resource-group myResourceGroup \
    --nsg-name myNetworkSecurityGroup \
    --name myNetworkSecurityGroupRuleSSH \
    --priority 1000 \
    --protocol tcp \
    --destination-port-range 22 \
```

## <a name="attach-the-subnet-to-the-network-security-group"></a><span data-ttu-id="5770d-144">Dołącz podsieci do grupy zabezpieczeń sieci</span><span class="sxs-lookup"><span data-stu-id="5770d-144">Attach the subnet to the network security group</span></span>

<span data-ttu-id="5770d-145">Reguły grupy zabezpieczeń sieci może odnosić się do podsieci lub interfejs określonej sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="5770d-145">The network security group rules can be applied to a subnet or a specific virtual network interface.</span></span> <span data-ttu-id="5770d-146">Umożliwia dołączanie sieciowej grupy zabezpieczeń do naszej podsieci.</span><span class="sxs-lookup"><span data-stu-id="5770d-146">Lets attach the network security group to our subnet.</span></span> <span data-ttu-id="5770d-147">Dołącz do sieciowej grupy zabezpieczeń z podsieci [zaktualizować podsieci sieci wirtualnej sieci az](/cli/azure/network/vnet/subnet#update):</span><span class="sxs-lookup"><span data-stu-id="5770d-147">Attach your subnet to the network security group with [az network vnet subnet update](/cli/azure/network/vnet/subnet#update):</span></span>

```azurecli
az network vnet subnet update \
    --resource-group myResourceGroup \
    --vnet-name myVnet \
    --name mySubnet \
    --network-security-group myNetworkSecurityGroup
```

## <a name="add-a-virtual-network-interface-card-to-the-subnet"></a><span data-ttu-id="5770d-148">Dodaj do karty interfejsu sieci wirtualnej do podsieci</span><span class="sxs-lookup"><span data-stu-id="5770d-148">Add a virtual network interface card to the subnet</span></span>

<span data-ttu-id="5770d-149">Karty interfejsu sieci wirtualnej (VNics) są istotne, ponieważ użytkownik może korzystać z nich łącząc je do różnych maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="5770d-149">Virtual network interface cards (VNics) are important as you can reuse them by connecting them to different VMs.</span></span> <span data-ttu-id="5770d-150">Ta ponownemu pozwala na zachowanie VNic jako zasób statycznych, maszyny wirtualne mogą być tymczasowe.</span><span class="sxs-lookup"><span data-stu-id="5770d-150">This reuse allows you to keep the VNic as a static resource while the VMs can be temporary.</span></span> <span data-ttu-id="5770d-151">Utwórz VNic i powiązać ją z podsieci o [tworzenie kart interfejsu sieciowego az](/cli/azure/network/nic#create).</span><span class="sxs-lookup"><span data-stu-id="5770d-151">Create a VNic and associate it with the subnet with [az network nic create](/cli/azure/network/nic#create).</span></span> <span data-ttu-id="5770d-152">Poniższy przykład tworzy VNic, o nazwie *myNic*:</span><span class="sxs-lookup"><span data-stu-id="5770d-152">The following example creates a VNic named *myNic*:</span></span>

```azurecli
az network nic create \
    --resource-group myResourceGroup \
    --location eastus \
    --name myNic \
    --vnet-name myVnet \
    --subnet mySubnet
```

## <a name="deploy-the-vm-into-the-virtual-network-infrastructure"></a><span data-ttu-id="5770d-153">Wdróż maszynę Wirtualną do infrastruktury sieci wirtualnej</span><span class="sxs-lookup"><span data-stu-id="5770d-153">Deploy the VM into the virtual network infrastructure</span></span>

<span data-ttu-id="5770d-154">Istnieje już sieć wirtualną i podsieć i sieciową grupę zabezpieczeń do ochrony przez blokuje cały ruch przychodzący z wyjątkiem port 22 SSH podsieci.</span><span class="sxs-lookup"><span data-stu-id="5770d-154">You now have a virtual network and subnet, and a network security group to protect the subnet by blocking all inbound traffic except port 22 for SSH.</span></span> <span data-ttu-id="5770d-155">Teraz można wdrożyć maszyny Wirtualnej w tym istniejącej infrastruktury sieci.</span><span class="sxs-lookup"><span data-stu-id="5770d-155">The VM can now be deployed inside this existing network infrastructure.</span></span>

<span data-ttu-id="5770d-156">Tworzenie maszyny Wirtualnej z [tworzenia maszyny wirtualnej az](/cli/azure/vm#create).</span><span class="sxs-lookup"><span data-stu-id="5770d-156">Create your VM with [az vm create](/cli/azure/vm#create).</span></span> <span data-ttu-id="5770d-157">Aby uzyskać więcej informacji o flagach do użycia z 2.0 interfejsu wiersza polecenia platformy Azure, aby wdrożyć Maszynę wirtualną pełną, zobacz [tworzyć kompletne środowisko systemu Linux przy użyciu interfejsu wiersza polecenia Azure](create-cli-complete.md).</span><span class="sxs-lookup"><span data-stu-id="5770d-157">For more information on the flags to use with the Azure CLI 2.0 to deploy a complete VM, see [Create a complete Linux environment by using the Azure CLI](create-cli-complete.md).</span></span>

<span data-ttu-id="5770d-158">Poniższy przykład tworzy Maszynę wirtualną za pomocą dysków zarządzanych platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="5770d-158">The following example creates a VM using Azure Managed Disks.</span></span> <span data-ttu-id="5770d-159">Te dyski są obsługiwane przez platformę Azure i nie wymagają wszystkie lub lokalizację do przechowywania ich.</span><span class="sxs-lookup"><span data-stu-id="5770d-159">These disks are handled by the Azure platform and do not require any preparation or location to store them.</span></span> <span data-ttu-id="5770d-160">Aby uzyskać więcej informacji o dyskach zarządzanych, zobacz [Omówienie usługi Azure Managed Disks](../../storage/storage-managed-disks-overview.md).</span><span class="sxs-lookup"><span data-stu-id="5770d-160">For more information about managed disks, see [Azure Managed Disks overview](../../storage/storage-managed-disks-overview.md).</span></span> <span data-ttu-id="5770d-161">Jeśli chcesz używać dysków niezarządzane, zobacz Uwagi dodatkowe poniżej.</span><span class="sxs-lookup"><span data-stu-id="5770d-161">If you wish to use unmanaged disks, see the additional note below.</span></span>

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --image Debian \
    --admin-username azureuser \
    --generate-ssh-keys \
    --nics myNic
```

<span data-ttu-id="5770d-162">Użycie dysków zarządzanych, Pomiń ten krok.</span><span class="sxs-lookup"><span data-stu-id="5770d-162">If you use managed disks, skip this step.</span></span> <span data-ttu-id="5770d-163">Jeśli chcesz używać dysków niezarządzane, należy dodać następujące dodatkowe parametry do polecenia postępowania w celu tworzenia niezarządzanej dysków na koncie magazynu o nazwie `mystorageaccount`:</span><span class="sxs-lookup"><span data-stu-id="5770d-163">If you wish to use unmanaged disks, you need to add the following additional parameters to the proceeding command to create unmanaged disks in the storage account named `mystorageaccount`:</span></span> 

```azurecli
    --use-unmanaged-disk \
    --storage-account mystorageaccount
```

<span data-ttu-id="5770d-164">Za pomocą flag interfejsu wiersza polecenia do wyróżnienia istniejących zasobów, można nakazać Azure, aby wdrożyć maszynę Wirtualną w istniejącej sieci.</span><span class="sxs-lookup"><span data-stu-id="5770d-164">By using the CLI flags to call out existing resources, you instruct Azure to deploy the VM inside the existing network.</span></span> <span data-ttu-id="5770d-165">Po wdrożeniu sieci wirtualnej i podsieci, możesz je zostawić jako statyczne ani stałe zasoby w Twoim regionie Azure.</span><span class="sxs-lookup"><span data-stu-id="5770d-165">Once a virtual network and subnet have been deployed, they can be left as static or permanent resources inside your Azure region.</span></span> <span data-ttu-id="5770d-166">W tym przykładzie jest nie utworzyć i przypisać publicznego adresu IP wirtualnej karty sieciowej, więc ta maszyna wirtualna nie jest dostępny publicznie w Internecie.</span><span class="sxs-lookup"><span data-stu-id="5770d-166">In this example, you did not create and assign a public IP address to the VNic, so this VM is not publicly accessible over the Internet.</span></span> <span data-ttu-id="5770d-167">Aby uzyskać więcej informacji, zobacz [utworzyć Maszynę wirtualną z statycznego publicznego adresu IP za pomocą interfejsu wiersza polecenia Azure](../../virtual-network/virtual-network-deploy-static-pip-arm-cli.md).</span><span class="sxs-lookup"><span data-stu-id="5770d-167">For more information, see [Create a VM with a static public IP using the Azure CLI](../../virtual-network/virtual-network-deploy-static-pip-arm-cli.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="5770d-168">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="5770d-168">Next steps</span></span>
<span data-ttu-id="5770d-169">Aby uzyskać więcej informacji o sposobach tworzenia maszyn wirtualnych na platformie Azure zobacz następujące zasoby:</span><span class="sxs-lookup"><span data-stu-id="5770d-169">For more information about ways to create virtual machines in Azure, see the following resources:</span></span>

* [<span data-ttu-id="5770d-170">Tworzenie konkretnego wdrożenia za pomocą szablonu usługi Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="5770d-170">Use an Azure Resource Manager template to create a specific deployment</span></span>](../windows/cli-deploy-templates.md)
* [<span data-ttu-id="5770d-171">Tworzenie niestandardowego środowiska dla maszyny wirtualnej z systemem Linux poprzez bezpośrednie użycie poleceń interfejsu wiersza polecenia platformy Azure</span><span class="sxs-lookup"><span data-stu-id="5770d-171">Create your own custom environment for a Linux VM using Azure CLI commands directly</span></span>](create-cli-complete.md)
* [<span data-ttu-id="5770d-172">Utwórz Maszynę wirtualną systemu Linux na platformie Azure za pomocą szablonów</span><span class="sxs-lookup"><span data-stu-id="5770d-172">Create a Linux VM on Azure using templates</span></span>](create-ssh-secured-vm-from-template.md)
