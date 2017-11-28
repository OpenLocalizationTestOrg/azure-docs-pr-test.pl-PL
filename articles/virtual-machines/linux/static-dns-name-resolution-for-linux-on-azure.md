---
title: "Używany wewnętrzny serwer DNS do rozpoznawania nazw maszyny Wirtualnej Azure CLI 2.0 | Dokumentacja firmy Microsoft"
description: "Tworzenie sieci wirtualnej kart i korzystania z wewnętrznego serwera DNS do rozpoznawania nazw maszyny Wirtualnej na platformie Azure, Azure CLI 2.0"
services: virtual-machines-linux
documentationcenter: 
author: vlivech
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: azurecli
ms.topic: article
ms.date: 02/16/2017
ms.author: v-livech
ms.openlocfilehash: 992920adb1ae3736d43cc5f0bbb2081a20a1674d
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/18/2017
---
# <a name="create-virtual-network-interface-cards-and-use-internal-dns-for-vm-name-resolution-on-azure"></a><span data-ttu-id="27450-103">Tworzenie karty interfejsu sieci wirtualnej i korzystania z wewnętrznego serwera DNS do rozpoznawania nazw maszyny Wirtualnej na platformie Azure</span><span class="sxs-lookup"><span data-stu-id="27450-103">Create virtual network interface cards and use internal DNS for VM name resolution on Azure</span></span>
<span data-ttu-id="27450-104">W tym artykule przedstawiono sposób ustawić statyczny wewnętrznej nazwy DNS dla maszyn wirtualnych systemu Linux przy użyciu nazwy etykiety DNS i karty interfejsu sieci wirtualnej (vNics) 2.0 interfejsu wiersza polecenia platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="27450-104">This article shows you how to set static internal DNS names for Linux VMs using virtual network interface cards (vNics) and DNS label names with the Azure CLI 2.0.</span></span> <span data-ttu-id="27450-105">Czynności te można również wykonać przy użyciu [interfejsu wiersza polecenia platformy Azure w wersji 1.0](static-dns-name-resolution-for-linux-on-azure-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="27450-105">You can also perform these steps with the [Azure CLI 1.0](static-dns-name-resolution-for-linux-on-azure-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> <span data-ttu-id="27450-106">Statyczne nazwy DNS są używane dla usług trwałych infrastruktury, takich jak serwer kompilacji Wpięć, który służy do tego dokumentu lub serwer Git.</span><span class="sxs-lookup"><span data-stu-id="27450-106">Static DNS names are used for permanent infrastructure services like a Jenkins build server, which is used for this document, or a Git server.</span></span>

<span data-ttu-id="27450-107">Wymagania są następujące:</span><span class="sxs-lookup"><span data-stu-id="27450-107">The requirements are:</span></span>

* [<span data-ttu-id="27450-108">Konto platformy Azure</span><span class="sxs-lookup"><span data-stu-id="27450-108">an Azure account</span></span>](https://azure.microsoft.com/pricing/free-trial/)
* [<span data-ttu-id="27450-109">Pliki kluczy publicznych i prywatnych SSH</span><span class="sxs-lookup"><span data-stu-id="27450-109">SSH public and private key files</span></span>](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

## <a name="quick-commands"></a><span data-ttu-id="27450-110">Szybkie polecenia</span><span class="sxs-lookup"><span data-stu-id="27450-110">Quick commands</span></span>
<span data-ttu-id="27450-111">Jeśli chcesz szybko wykonywać zadania poniższej sekcji Szczegóły poleceń potrzebne.</span><span class="sxs-lookup"><span data-stu-id="27450-111">If you need to quickly accomplish the task, the following section details the commands needed.</span></span> <span data-ttu-id="27450-112">Bardziej szczegółowe informacje i kontekst dla każdego kroku można znaleźć w pozostałej części dokumentu, [uruchamiania tutaj](#detailed-walkthrough).</span><span class="sxs-lookup"><span data-stu-id="27450-112">More detailed information and context for each step can be found in the rest of the document, [starting here](#detailed-walkthrough).</span></span> <span data-ttu-id="27450-113">Aby wykonać te kroki, należy najnowszej [Azure CLI 2.0](/cli/azure/install-az-cli2) zainstalowane i zalogowany do konta platformy Azure przy użyciu [logowania az](/cli/azure/#login).</span><span class="sxs-lookup"><span data-stu-id="27450-113">To perform these steps, you need the latest [Azure CLI 2.0](/cli/azure/install-az-cli2) installed and logged in to an Azure account using [az login](/cli/azure/#login).</span></span>

<span data-ttu-id="27450-114">Wymagania Wstępne: Grupy zasobów, sieć wirtualną i podsieć, grupy zabezpieczeń sieci przy użyciu protokołu SSH ruchu przychodzącego.</span><span class="sxs-lookup"><span data-stu-id="27450-114">Pre-Requirements: Resource Group, virtual network and subnet, Network Security Group with SSH inbound.</span></span>

### <a name="create-a-virtual-network-interface-card-with-a-static-internal-dns-name"></a><span data-ttu-id="27450-115">Utwórz karty interfejsu sieci wirtualnej o nazwie DNS wewnętrzny statycznej</span><span class="sxs-lookup"><span data-stu-id="27450-115">Create a virtual network interface card with a static internal DNS name</span></span>
<span data-ttu-id="27450-116">Utwórz vNic z [tworzenie kart interfejsu sieciowego az](/cli/azure/network/nic#create).</span><span class="sxs-lookup"><span data-stu-id="27450-116">Create the vNic with [az network nic create](/cli/azure/network/nic#create).</span></span> <span data-ttu-id="27450-117">`--internal-dns-name` Flaga interfejsu wiersza polecenia jest do ustawiania etykiety DNS, który zawiera nazwę DNS statycznych dla wirtualnej karty sieciowej (vNic).</span><span class="sxs-lookup"><span data-stu-id="27450-117">The `--internal-dns-name` CLI flag is for setting the DNS label, which provides the static DNS name for the virtual network interface card (vNic).</span></span> <span data-ttu-id="27450-118">Poniższy przykład tworzy vNic, o nazwie `myNic`, łączy się `myVnet` sieci wirtualnej i tworzy wewnętrzny rekordu nazwy DNS nazywanego `jenkins`:</span><span class="sxs-lookup"><span data-stu-id="27450-118">The following example creates a vNic named `myNic`, connects it to the `myVnet` virtual network, and creates an internal DNS name record called `jenkins`:</span></span>

```azurecli
az network nic create \
    --resource-group myResourceGroup \
    --name myNic \
    --vnet-name myVnet \
    --subnet mySubnet \
    --internal-dns-name jenkins
```

### <a name="deploy-a-vm-and-connect-the-vnic"></a><span data-ttu-id="27450-119">Wdróż Maszynę wirtualną i połączyć vNic</span><span class="sxs-lookup"><span data-stu-id="27450-119">Deploy a VM and connect the vNic</span></span>
<span data-ttu-id="27450-120">Utwórz maszynę wirtualną za pomocą polecenia [az vm create](/cli/azure/vm#create).</span><span class="sxs-lookup"><span data-stu-id="27450-120">Create a VM with [az vm create](/cli/azure/vm#create).</span></span> <span data-ttu-id="27450-121">`--nics` Flagi vNic łączy się z maszyny Wirtualnej podczas wdrażania na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="27450-121">The `--nics` flag connects the vNic to the VM during the deployment to Azure.</span></span> <span data-ttu-id="27450-122">Poniższy przykład tworzy Maszynę wirtualną o nazwie `myVM` z dyskami zarządzane Azure i dołącza o nazwie vNic `myNic` w poprzednim kroku:</span><span class="sxs-lookup"><span data-stu-id="27450-122">The following example creates a VM named `myVM` with Azure Managed Disks and attaches the vNic named `myNic` from the preceding step:</span></span>

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --nics myNic \
    --image UbuntuLTS \
    --admin-username azureuser \
    --ssh-key-value ~/.ssh/id_rsa.pub
```

## <a name="detailed-walkthrough"></a><span data-ttu-id="27450-123">Szczegółowy przewodnik</span><span class="sxs-lookup"><span data-stu-id="27450-123">Detailed walkthrough</span></span>

<span data-ttu-id="27450-124">Pełne ciągłej integracji i ciągłe wdrażanie (CiCd) infrastruktury na platformie Azure wymaga niektórych serwerów serwery statyczne lub długotrwałe.</span><span class="sxs-lookup"><span data-stu-id="27450-124">A full continuous integration and continuous deployment (CiCd) infrastructure on Azure requires certain servers to be static or long-lived servers.</span></span> <span data-ttu-id="27450-125">Zaleca się, że Azure zasoby, takie jak sieci wirtualnych i grup zabezpieczeń sieci są statyczne i tam długo zasoby, które rzadko są wdrożone.</span><span class="sxs-lookup"><span data-stu-id="27450-125">It is recommended that Azure assets like the virtual networks and Network Security Groups are static and long lived resources that are rarely deployed.</span></span> <span data-ttu-id="27450-126">Po wdrożeniu sieci wirtualnej można użyć ponownie przez nowych wdrożeń bez żadnych niekorzystny wpływ infrastruktury.</span><span class="sxs-lookup"><span data-stu-id="27450-126">Once a virtual network has been deployed, it can be reused by new deployments without any adverse affects to the infrastructure.</span></span> <span data-ttu-id="27450-127">Później można dodać serwer repozytorium Git lub serwer automatyzacji Wpięć dostarcza CiCd do tej sieci wirtualnej dla rozwoju lub środowisk testowych.</span><span class="sxs-lookup"><span data-stu-id="27450-127">You can later add a Git repository server or a Jenkins automation server delivers CiCd to this virtual network for your development or test environments.</span></span>  

<span data-ttu-id="27450-128">Wewnętrzny nazw DNS są tylko rozpoznawany w sieci wirtualnej platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="27450-128">Internal DNS names are only resolvable inside an Azure virtual network.</span></span> <span data-ttu-id="27450-129">Ponieważ nazwy DNS są wewnętrzne, nie są one rozpoznać poza internet, zapewniając dodatkowe zabezpieczenia infrastruktury.</span><span class="sxs-lookup"><span data-stu-id="27450-129">Because the DNS names are internal, they are not resolvable to the outside internet, providing additional security to the infrastructure.</span></span>

<span data-ttu-id="27450-130">W poniższych przykładach Zastąp przykładowe nazwy parametrów własne wartości.</span><span class="sxs-lookup"><span data-stu-id="27450-130">In the following examples, replace example parameter names with your own values.</span></span> <span data-ttu-id="27450-131">Przykład nazwy parametru zawierają `myResourceGroup`, `myNic`, i `myVM`.</span><span class="sxs-lookup"><span data-stu-id="27450-131">Example parameter names include `myResourceGroup`, `myNic`, and `myVM`.</span></span>

## <a name="create-the-resource-group"></a><span data-ttu-id="27450-132">Tworzenie grupy zasobów</span><span class="sxs-lookup"><span data-stu-id="27450-132">Create the resource group</span></span>
<span data-ttu-id="27450-133">Najpierw należy utworzyć grupy zasobów z [Tworzenie grupy az](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="27450-133">First, create the resource group with [az group create](/cli/azure/group#create).</span></span> <span data-ttu-id="27450-134">Poniższy przykład tworzy grupę zasobów o nazwie `myResourceGroup` w `westus` lokalizacji:</span><span class="sxs-lookup"><span data-stu-id="27450-134">The following example creates a resource group named `myResourceGroup` in the `westus` location:</span></span>

```azurecli
az group create --name myResourceGroup --location westus
```

## <a name="create-the-virtual-network"></a><span data-ttu-id="27450-135">Utwórz sieć wirtualną</span><span class="sxs-lookup"><span data-stu-id="27450-135">Create the virtual network</span></span>

<span data-ttu-id="27450-136">Następnym krokiem jest tworzenie sieci wirtualnej można uruchomić maszyny wirtualne do.</span><span class="sxs-lookup"><span data-stu-id="27450-136">The next step is to build a virtual network to launch the VMs into.</span></span> <span data-ttu-id="27450-137">Sieć wirtualna zawiera jedną podsieć w ramach tego przewodnika.</span><span class="sxs-lookup"><span data-stu-id="27450-137">The virtual network contains one subnet for this walkthrough.</span></span> <span data-ttu-id="27450-138">Aby uzyskać więcej informacji o sieci wirtualnych platformy Azure, zobacz [utworzyć sieć wirtualną przy użyciu interfejsu wiersza polecenia Azure](../../virtual-network/virtual-networks-create-vnet-arm-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="27450-138">For more information on Azure virtual networks, see [Create a virtual network by using the Azure CLI](../../virtual-network/virtual-networks-create-vnet-arm-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> 

<span data-ttu-id="27450-139">Utwórz sieć wirtualną z [tworzenie sieci wirtualnej sieci az](/cli/azure/network/vnet#create).</span><span class="sxs-lookup"><span data-stu-id="27450-139">Create the virtual network with [az network vnet create](/cli/azure/network/vnet#create).</span></span> <span data-ttu-id="27450-140">Poniższy przykład tworzy sieć wirtualną o nazwie `myVnet` i podsieć o nazwie `mySubnet`:</span><span class="sxs-lookup"><span data-stu-id="27450-140">The following example creates a virtual network named `myVnet` and subnet named `mySubnet`:</span></span>

```azurecli
az network vnet create \
    --resource-group myResourceGroup \
    --name myVnet \
    --address-prefix 192.168.0.0/16 \
    --subnet-name mySubnet \
    --subnet-prefix 192.168.1.0/24
```

## <a name="create-the-network-security-group"></a><span data-ttu-id="27450-141">Utwórz grupę zabezpieczeń sieci</span><span class="sxs-lookup"><span data-stu-id="27450-141">Create the Network Security Group</span></span>
<span data-ttu-id="27450-142">Grupy zabezpieczeń sieci platformy Azure są równoważne zapory w warstwie sieci.</span><span class="sxs-lookup"><span data-stu-id="27450-142">Azure Network Security Groups are equivalent to a firewall at the network layer.</span></span> <span data-ttu-id="27450-143">Aby uzyskać więcej informacji na temat grup zabezpieczeń sieci, zobacz [sposób tworzenia grup NSG w interfejsu wiersza polecenia Azure](../../virtual-network/virtual-networks-create-nsg-arm-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="27450-143">For more information about Network Security Groups, see [How to create NSGs in the Azure CLI](../../virtual-network/virtual-networks-create-nsg-arm-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> 

<span data-ttu-id="27450-144">Utwórz grupę zabezpieczeń sieci z [utworzyć nsg sieci az](/cli/azure/network/nsg#create).</span><span class="sxs-lookup"><span data-stu-id="27450-144">Create the network security group with [az network nsg create](/cli/azure/network/nsg#create).</span></span> <span data-ttu-id="27450-145">Poniższy przykład tworzy sieciową grupę zabezpieczeń o nazwie `myNetworkSecurityGroup`:</span><span class="sxs-lookup"><span data-stu-id="27450-145">The following example creates a network security group named `myNetworkSecurityGroup`:</span></span>

```azurecli
az network nsg create \
    --resource-group myResourceGroup \
    --name myNetworkSecurityGroup
```

## <a name="add-an-inbound-rule-to-allow-ssh"></a><span data-ttu-id="27450-146">Dodaj regułę ruchu przychodzącego zezwalająca na SSH</span><span class="sxs-lookup"><span data-stu-id="27450-146">Add an inbound rule to allow SSH</span></span>
<span data-ttu-id="27450-147">Dodaj regułę ruchu przychodzącego dla sieciowej grupy zabezpieczeń z [Tworzenie reguły nsg sieci az](/cli/azure/network/nsg/rule#create).</span><span class="sxs-lookup"><span data-stu-id="27450-147">Add an inbound rule for the network security group with [az network nsg rule create](/cli/azure/network/nsg/rule#create).</span></span> <span data-ttu-id="27450-148">Poniższy przykład tworzy reguły o nazwie `myRuleAllowSSH`:</span><span class="sxs-lookup"><span data-stu-id="27450-148">The following example creates a rule named `myRuleAllowSSH`:</span></span>

```azurecli
az network nsg rule create \
    --resource-group myResourceGroup \
    --nsg-name myNetworkSecurityGroup \
    --name myRuleAllowSSH \
    --protocol tcp \
    --direction inbound \
    --priority 1000 \
    --source-address-prefix '*' \
    --source-port-range '*' \
    --destination-address-prefix '*' \
    --destination-port-range 22 \
    --access allow
```

## <a name="associate-the-subnet-with-the-network-security-group"></a><span data-ttu-id="27450-149">Podsieć jest skojarzona z sieciową grupą zabezpieczeń</span><span class="sxs-lookup"><span data-stu-id="27450-149">Associate the subnet with the Network Security Group</span></span>
<span data-ttu-id="27450-150">Aby skojarzyć podsieci z sieciową grupą zabezpieczeń, użyj [zaktualizować podsieci sieci wirtualnej sieci az](/cli/azure/network/vnet/subnet#update).</span><span class="sxs-lookup"><span data-stu-id="27450-150">To associate the subnet with the Network Security Group, use [az network vnet subnet update](/cli/azure/network/vnet/subnet#update).</span></span> <span data-ttu-id="27450-151">Poniższy przykład powoduje skojarzenie nazwy podsieci `mySubnet` z sieciową grupą zabezpieczeń o nazwie `myNetworkSecurityGroup`:</span><span class="sxs-lookup"><span data-stu-id="27450-151">The following example associates the subnet name `mySubnet` with the Network Security Group named `myNetworkSecurityGroup`:</span></span>

```azurecli
az network vnet subnet update \
    --resource-group myResourceGroup \
    --vnet-name myVnet \
    --name mySubnet \
    --network-security-group myNetworkSecurityGroup
```


## <a name="create-the-virtual-network-interface-card-and-static-dns-names"></a><span data-ttu-id="27450-152">Tworzenie wirtualnej karty sieciowej i statyczne nazwy DNS</span><span class="sxs-lookup"><span data-stu-id="27450-152">Create the virtual network interface card and static DNS names</span></span>
<span data-ttu-id="27450-153">Platforma Azure jest bardzo elastyczne, ale aby użyć nazwy DNS dla rozpoznawania nazw maszyny Wirtualnej, należy utworzyć sieci wirtualnej karty interfejsu (vNics), które obejmują etykietę DNS.</span><span class="sxs-lookup"><span data-stu-id="27450-153">Azure is very flexible, but to use DNS names for VM name resolution, you need to create virtual network interface cards (vNics) that include a DNS label.</span></span> <span data-ttu-id="27450-154">vNics są ważne, ponieważ użytkownik może korzystać z nich łącząc je do różnych maszyn wirtualnych z cyklem infrastruktury.</span><span class="sxs-lookup"><span data-stu-id="27450-154">vNics are important as you can reuse them by connecting them to different VMs over the infrastructure lifecycle.</span></span> <span data-ttu-id="27450-155">Takie podejście zapewnia vNic jako zasób statycznych maszyn wirtualnych mogą być tymczasowe.</span><span class="sxs-lookup"><span data-stu-id="27450-155">This approach keeps the vNic as a static resource while the VMs can be temporary.</span></span> <span data-ttu-id="27450-156">Za pomocą DNS etykietowania na karcie vNic, możemy włączyć rozpoznawanie nazw prostego z innych maszyn wirtualnych w sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="27450-156">By using DNS labeling on the vNic, we are able to enable simple name resolution from other VMs in the VNet.</span></span> <span data-ttu-id="27450-157">Przy użyciu nazwy rozpoznawalną umożliwia innych maszyn wirtualnych na dostęp do serwera automatyzacji za pomocą nazwy DNS `Jenkins` lub na serwerze Git `gitrepo`.</span><span class="sxs-lookup"><span data-stu-id="27450-157">Using resolvable names enables other VMs to access the automation server by the DNS name `Jenkins` or the Git server as `gitrepo`.</span></span>  

<span data-ttu-id="27450-158">Utwórz vNic z [tworzenie kart interfejsu sieciowego az](/cli/azure/network/nic#create).</span><span class="sxs-lookup"><span data-stu-id="27450-158">Create the vNic with [az network nic create](/cli/azure/network/nic#create).</span></span> <span data-ttu-id="27450-159">Poniższy przykład tworzy vNic, o nazwie `myNic`, łączy się `myVnet` sieci wirtualnej o nazwie `myVnet`i tworzy wewnętrzny rekordu nazwy DNS nazywanego `jenkins`:</span><span class="sxs-lookup"><span data-stu-id="27450-159">The following example creates a vNic named `myNic`, connects it to the `myVnet` virtual network named `myVnet`, and creates an internal DNS name record called `jenkins`:</span></span>

```azurecli
az network nic create \
    --resource-group myResourceGroup \
    --name myNic \
    --vnet-name myVnet \
    --subnet mySubnet \
    --internal-dns-name jenkins
```

## <a name="deploy-the-vm-into-the-virtual-network-infrastructure"></a><span data-ttu-id="27450-160">Wdróż maszynę Wirtualną do infrastruktury sieci wirtualnej</span><span class="sxs-lookup"><span data-stu-id="27450-160">Deploy the VM into the virtual network infrastructure</span></span>
<span data-ttu-id="27450-161">Mamy teraz sieć wirtualna i podsieć, grupa zabezpieczeń sieci działający jako zapory do ochrony przez blokuje cały ruch przychodzący z wyjątkiem port 22 protokołu SSH i vNic naszych podsieci.</span><span class="sxs-lookup"><span data-stu-id="27450-161">We now have a virtual network and subnet, a Network Security Group acting as a firewall to protect our subnet by blocking all inbound traffic except port 22 for SSH, and a vNic.</span></span> <span data-ttu-id="27450-162">Teraz można wdrożyć maszyny Wirtualnej w tym istniejącej infrastruktury sieci.</span><span class="sxs-lookup"><span data-stu-id="27450-162">You can now deploy a VM inside this existing network infrastructure.</span></span>

<span data-ttu-id="27450-163">Utwórz maszynę wirtualną za pomocą polecenia [az vm create](/cli/azure/vm#create).</span><span class="sxs-lookup"><span data-stu-id="27450-163">Create a VM with [az vm create](/cli/azure/vm#create).</span></span> <span data-ttu-id="27450-164">Poniższy przykład tworzy Maszynę wirtualną o nazwie `myVM` z dyskami zarządzane Azure i dołącza o nazwie vNic `myNic` w poprzednim kroku:</span><span class="sxs-lookup"><span data-stu-id="27450-164">The following example creates a VM named `myVM` with Azure Managed Disks and attaches the vNic named `myNic` from the preceding step:</span></span>

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --nics myNic \
    --image UbuntuLTS \
    --admin-username azureuser \
    --ssh-key-value ~/.ssh/id_rsa.pub
```

<span data-ttu-id="27450-165">Za pomocą flag interfejsu wiersza polecenia do wyróżnienia istniejących zasobów, poinstruuj firma Microsoft Azure, aby wdrożyć maszynę Wirtualną w istniejącej sieci.</span><span class="sxs-lookup"><span data-stu-id="27450-165">By using the CLI flags to call out existing resources, we instruct Azure to deploy the VM inside the existing network.</span></span> <span data-ttu-id="27450-166">Aby przywołują, po wdrożeniu sieci wirtualnej i podsieci, możesz je zostawić jako statyczne ani stałe zasoby w Twoim regionie Azure.</span><span class="sxs-lookup"><span data-stu-id="27450-166">To reiterate, once a VNet and subnet have been deployed, they can be left as static or permanent resources inside your Azure region.</span></span>  

## <a name="next-steps"></a><span data-ttu-id="27450-167">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="27450-167">Next steps</span></span>
* [<span data-ttu-id="27450-168">Tworzenie niestandardowego środowiska dla maszyny wirtualnej z systemem Linux poprzez bezpośrednie użycie poleceń interfejsu wiersza polecenia platformy Azure</span><span class="sxs-lookup"><span data-stu-id="27450-168">Create your own custom environment for a Linux VM using Azure CLI commands directly</span></span>](create-cli-complete.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [<span data-ttu-id="27450-169">Utwórz Maszynę wirtualną systemu Linux na platformie Azure za pomocą szablonów</span><span class="sxs-lookup"><span data-stu-id="27450-169">Create a Linux VM on Azure using templates</span></span>](create-ssh-secured-vm-from-template.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
