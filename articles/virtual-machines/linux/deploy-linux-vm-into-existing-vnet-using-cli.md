---
title: "aaaDeploy maszyn wirtualnych systemu Linux w istniejącej sieci Azure CLI 2.0 | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toodeploy maszynę wirtualną systemu Linux do istniejącej sieci wirtualnej przy użyciu hello Azure CLI 2.0"
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
ms.openlocfilehash: 0df44b3437002df050db56f3b3899083fb49d803
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toodeploy-a-linux-virtual-machine-into-an-existing-azure-virtual-network-with-hello-azure-cli"></a><span data-ttu-id="c6ff5-103">Jak toodeploy maszyny wirtualnej systemu Linux w istniejącej sieci wirtualnej platformy Azure z hello wiersza polecenia platformy Azure</span><span class="sxs-lookup"><span data-stu-id="c6ff5-103">How toodeploy a Linux virtual machine into an existing Azure Virtual Network with hello Azure CLI</span></span>

<span data-ttu-id="c6ff5-104">W tym artykule opisano sposób toouse hello Azure CLI 2.0 toodeploy maszynę wirtualną (VM) do istniejącej sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="c6ff5-104">This article shows you how toouse hello Azure CLI 2.0 toodeploy a virtual machine (VM) into an existing virtual network.</span></span> <span data-ttu-id="c6ff5-105">wymagania dotyczące Hello są:</span><span class="sxs-lookup"><span data-stu-id="c6ff5-105">hello requirements are:</span></span>

- [<span data-ttu-id="c6ff5-106">Konto platformy Azure</span><span class="sxs-lookup"><span data-stu-id="c6ff5-106">an Azure account</span></span>](https://azure.microsoft.com/pricing/free-trial/)
- [<span data-ttu-id="c6ff5-107">Pliki kluczy publicznych i prywatnych SSH</span><span class="sxs-lookup"><span data-stu-id="c6ff5-107">SSH public and private key files</span></span>](mac-create-ssh-keys.md)

<span data-ttu-id="c6ff5-108">Można również wykonać te kroki hello [Azure CLI 1.0](deploy-linux-vm-into-existing-vnet-using-cli-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="c6ff5-108">You can also perform these steps with hello [Azure CLI 1.0](deploy-linux-vm-into-existing-vnet-using-cli-nodejs.md).</span></span>


## <a name="quick-commands"></a><span data-ttu-id="c6ff5-109">Szybkie polecenia</span><span class="sxs-lookup"><span data-stu-id="c6ff5-109">Quick Commands</span></span>
<span data-ttu-id="c6ff5-110">Jeśli potrzebujesz tooquickly hello zadania, powitania po sekcji Szczegóły poleceń hello potrzebne.</span><span class="sxs-lookup"><span data-stu-id="c6ff5-110">If you need tooquickly accomplish hello task, hello following section details hello  commands needed.</span></span> <span data-ttu-id="c6ff5-111">Bardziej szczegółowe informacje i kontekst dla każdego kroku można znaleźć hello pozostałej części dokumentu hello [uruchamiania tutaj](#detailed-walkthrough).</span><span class="sxs-lookup"><span data-stu-id="c6ff5-111">More detailed information and context for each step can be found hello rest of hello document, [starting here](#detailed-walkthrough).</span></span>

<span data-ttu-id="c6ff5-112">toocreate to środowisko niestandardowe, należy hello jest najnowsza wersja [Azure CLI 2.0](/cli/azure/install-az-cli2) zainstalowane i zarejestrowane za pomocą konta Azure tooan [logowania az](/cli/azure/#login).</span><span class="sxs-lookup"><span data-stu-id="c6ff5-112">toocreate this custom environment, you need hello latest [Azure CLI 2.0](/cli/azure/install-az-cli2) installed and logged in tooan Azure account using [az login](/cli/azure/#login).</span></span>

<span data-ttu-id="c6ff5-113">Poniższe przykłady w hello Zastąp przykładowe nazwy parametrów własne wartości.</span><span class="sxs-lookup"><span data-stu-id="c6ff5-113">In hello following examples, replace example parameter names with your own values.</span></span> <span data-ttu-id="c6ff5-114">Przykład nazwy parametru zawierają *myResourceGroup*, *myVnet*, i *myVM*.</span><span class="sxs-lookup"><span data-stu-id="c6ff5-114">Example parameter names include *myResourceGroup*, *myVnet*, and *myVM*.</span></span>

<span data-ttu-id="c6ff5-115">**Wymagania wstępne:** grupy zasobów platformy Azure, sieci wirtualnych i podsieci ruchu przychodzącego grupy zabezpieczeń sieci przy użyciu protokołu SSH i karty interfejsu sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="c6ff5-115">**Pre-requirements:** Azure resource group, virtual network and subnet, network security group with SSH inbound, and a virtual network interface card.</span></span>

### <a name="deploy-hello-vm-into-hello-virtual-network-infrastructure"></a><span data-ttu-id="c6ff5-116">Wdrażanie hello maszyny Wirtualnej do hello infrastruktury sieci wirtualnej</span><span class="sxs-lookup"><span data-stu-id="c6ff5-116">Deploy hello VM into hello virtual network infrastructure</span></span>

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --image Debian \
    --admin-username azureuser \
    --generate-ssh-keys \
    --nics myNic
```

## <a name="detailed-walkthrough"></a><span data-ttu-id="c6ff5-117">Szczegółowy przewodnik</span><span class="sxs-lookup"><span data-stu-id="c6ff5-117">Detailed walkthrough</span></span>

<span data-ttu-id="c6ff5-118">Azure zasoby, takie jak sieci wirtualnych i grup zabezpieczeń sieci musi być statyczny i tam długo zasoby, które rzadko są wdrożone.</span><span class="sxs-lookup"><span data-stu-id="c6ff5-118">Azure assets like virtual networks and network security groups should be static and long lived resources that are rarely deployed.</span></span> <span data-ttu-id="c6ff5-119">Po wdrożeniu sieci wirtualnej można użyć ponownie przez nowych wdrożeń bez żadnych infrastruktury toohello niekorzystny wpływ.</span><span class="sxs-lookup"><span data-stu-id="c6ff5-119">Once a virtual network has been deployed, it can be reused by new deployments without any adverse affects toohello infrastructure.</span></span> <span data-ttu-id="c6ff5-120">Pomyśleć o sieci wirtualnej jako przełącznik sieciowy tradycyjnych sprzętu — tooconfigure nowego sprzętu przełącznik z każdego wdrożenia nie jest wymagane.</span><span class="sxs-lookup"><span data-stu-id="c6ff5-120">Think about a virtual network as being a traditional hardware network switch - you would not need tooconfigure a brand new hardware switch with each deployment.</span></span> <span data-ttu-id="c6ff5-121">Z sieci wirtualnej prawidłowo skonfigurowany, można kontynuować toodeploy nowych maszyn wirtualnych w tej sieci wirtualnej samodzielnego z kilku, ewentualne zmiany wymagane na okres hello hello sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="c6ff5-121">With a correctly configured virtual network, you can continue toodeploy new VMs into that virtual network over and over with few, if any, changes required over hello life of hello virtual network.</span></span>

<span data-ttu-id="c6ff5-122">toocreate to środowisko niestandardowe, należy hello jest najnowsza wersja [Azure CLI 2.0](/cli/azure/install-az-cli2) zainstalowane i zarejestrowane za pomocą konta Azure tooan [logowania az](/cli/azure/#login).</span><span class="sxs-lookup"><span data-stu-id="c6ff5-122">toocreate this custom environment, you need hello latest [Azure CLI 2.0](/cli/azure/install-az-cli2) installed and logged in tooan Azure account using [az login](/cli/azure/#login).</span></span>

<span data-ttu-id="c6ff5-123">Poniższe przykłady w hello Zastąp przykładowe nazwy parametrów własne wartości.</span><span class="sxs-lookup"><span data-stu-id="c6ff5-123">In hello following examples, replace example parameter names with your own values.</span></span> <span data-ttu-id="c6ff5-124">Przykład nazwy parametru zawierają *myResourceGroup*, *myVnet*, i *myVM*.</span><span class="sxs-lookup"><span data-stu-id="c6ff5-124">Example parameter names include *myResourceGroup*, *myVnet*, and *myVM*.</span></span>

## <a name="create-hello-resource-group"></a><span data-ttu-id="c6ff5-125">Utwórz grupę zasobów hello</span><span class="sxs-lookup"><span data-stu-id="c6ff5-125">Create hello resource group</span></span>

<span data-ttu-id="c6ff5-126">Najpierw utwórz tooorganize grupy zasobów platformy Azure wszystko, czego możesz utworzyć w tym przewodniku.</span><span class="sxs-lookup"><span data-stu-id="c6ff5-126">First, create an Azure resource group tooorganize everything you create in this walkthrough.</span></span> <span data-ttu-id="c6ff5-127">Więcej informacji na temat grup zasobów znajduje się w temacie [Omówienie usługi Azure Resource Manager](../../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="c6ff5-127">For more information on resource groups, see [Azure Resource Manager overview](../../azure-resource-manager/resource-group-overview.md).</span></span> <span data-ttu-id="c6ff5-128">Utwórz grupę zasobów hello z [Tworzenie grupy az](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="c6ff5-128">Create hello resource group with [az group create](/cli/azure/group#create).</span></span> <span data-ttu-id="c6ff5-129">Witaj poniższy przykład tworzy grupę zasobów o nazwie *myResourceGroup* w hello *eastus* lokalizacji:</span><span class="sxs-lookup"><span data-stu-id="c6ff5-129">hello following example creates a resource group named *myResourceGroup* in hello *eastus* location:</span></span>

```azurecli
az group create \
    --name myResourceGroup \
    --location eastus
```

## <a name="create-hello-virtual-network"></a><span data-ttu-id="c6ff5-130">Utwórz sieć wirtualną hello</span><span class="sxs-lookup"><span data-stu-id="c6ff5-130">Create hello virtual network</span></span>

<span data-ttu-id="c6ff5-131">Umożliwia tworzenie maszyn wirtualnych do hello toolaunch sieci wirtualnej platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="c6ff5-131">Lets build an Azure virtual network toolaunch hello VMs into.</span></span> <span data-ttu-id="c6ff5-132">Aby uzyskać więcej informacji o sieciach wirtualnych, zobacz [utworzyć sieć wirtualną przy użyciu interfejsu wiersza polecenia Azure hello](../../virtual-network/virtual-networks-create-vnet-arm-cli.md).</span><span class="sxs-lookup"><span data-stu-id="c6ff5-132">For more information on virtual networks, see [Create a virtual network by using hello Azure CLI](../../virtual-network/virtual-networks-create-vnet-arm-cli.md).</span></span> <span data-ttu-id="c6ff5-133">Utwórz sieć wirtualną hello z [tworzenie sieci wirtualnej sieci az](/cli/azure/network/vnet#create).</span><span class="sxs-lookup"><span data-stu-id="c6ff5-133">Create hello virtual network with [az network vnet create](/cli/azure/network/vnet#create).</span></span> <span data-ttu-id="c6ff5-134">Witaj poniższy przykład tworzy sieć wirtualną o nazwie *myVnet* i podsieć o nazwie *mySubnet*:</span><span class="sxs-lookup"><span data-stu-id="c6ff5-134">hello following example creates a virtual network named *myVnet* and subnet named *mySubnet*:</span></span>

```azurecli
az network vnet create \
    --resource-group myResourceGroup \
    --location eastus \
    --name myVnet \
    --address-prefix 10.10.0.0/16 \
    --subnet-name mySubnet \
    --subnet-prefix 10.10.1.0/24
```

## <a name="create-hello-network-security-group"></a><span data-ttu-id="c6ff5-135">Utwórz grupę zabezpieczeń sieci hello</span><span class="sxs-lookup"><span data-stu-id="c6ff5-135">Create hello network security group</span></span>

<span data-ttu-id="c6ff5-136">Grupy zabezpieczeń sieci platformy Azure są równoważne tooa zapory na powitania warstwy sieci.</span><span class="sxs-lookup"><span data-stu-id="c6ff5-136">Azure network security groups are equivalent tooa firewall at hello network layer.</span></span> <span data-ttu-id="c6ff5-137">Aby uzyskać więcej informacji dotyczących grup zabezpieczeń sieci, zobacz [jak grupy zabezpieczeń sieci toocreate w hello Azure CLI](../../virtual-network/virtual-networks-create-nsg-arm-cli.md).</span><span class="sxs-lookup"><span data-stu-id="c6ff5-137">For more information on network security groups, see [How toocreate network security groups in hello Azure CLI](../../virtual-network/virtual-networks-create-nsg-arm-cli.md).</span></span> <span data-ttu-id="c6ff5-138">Utwórz grupę zabezpieczeń sieci hello z [utworzyć nsg sieci az](/cli/azure/network/nsg#create).</span><span class="sxs-lookup"><span data-stu-id="c6ff5-138">Create hello network security group with [az network nsg create](/cli/azure/network/nsg#create).</span></span> <span data-ttu-id="c6ff5-139">Witaj poniższy przykład tworzy sieciową grupę zabezpieczeń o nazwie *myNetworkSecurityGroup*:</span><span class="sxs-lookup"><span data-stu-id="c6ff5-139">hello following example creates a network security group named *myNetworkSecurityGroup*:</span></span>

```azurecli
az network nsg create \
    --resource-group myResourceGroup \
    --location eastus \
    --name myNetworkSecurityGroup
```

## <a name="add-an-inbound-ssh-allow-rule"></a><span data-ttu-id="c6ff5-140">Dodaj regułę Zezwalaj SSH dla ruchu przychodzącego</span><span class="sxs-lookup"><span data-stu-id="c6ff5-140">Add an inbound SSH allow rule</span></span>

<span data-ttu-id="c6ff5-141">Witaj maszyna wirtualna musi mieć dostęp z hello internet, więc regułę zezwalającą na toobe ruch przychodzący port 22 przekazywane hello sieci tooport 22 na powitania maszyny Wirtualnej jest wymagana.</span><span class="sxs-lookup"><span data-stu-id="c6ff5-141">hello VM needs access from hello internet, so a rule allowing inbound port 22 traffic toobe passed through hello network tooport 22 on hello VM is needed.</span></span> <span data-ttu-id="c6ff5-142">Dodaj regułę ruchu przychodzącego dla sieciowej grupy zabezpieczeń z hello [Tworzenie reguły nsg sieci az](/cli/azure/network/nsg/rule#create).</span><span class="sxs-lookup"><span data-stu-id="c6ff5-142">Add an inbound rule for hello network security group with [az network nsg rule create](/cli/azure/network/nsg/rule#create).</span></span> <span data-ttu-id="c6ff5-143">Witaj poniższy przykład powoduje utworzenie reguły o nazwie *myNetworkSecurityGroupRuleSSH*:</span><span class="sxs-lookup"><span data-stu-id="c6ff5-143">hello following example creates a rule named *myNetworkSecurityGroupRuleSSH*:</span></span>

```azurecli
az network nsg rule create \
    --resource-group myResourceGroup \
    --nsg-name myNetworkSecurityGroup \
    --name myNetworkSecurityGroupRuleSSH \
    --priority 1000 \
    --protocol tcp \
    --destination-port-range 22 \
```

## <a name="attach-hello-subnet-toohello-network-security-group"></a><span data-ttu-id="c6ff5-144">Dołącz hello podsieci toohello sieciowej grupy zabezpieczeń</span><span class="sxs-lookup"><span data-stu-id="c6ff5-144">Attach hello subnet toohello network security group</span></span>

<span data-ttu-id="c6ff5-145">reguły grupy zabezpieczeń sieci Hello może być zastosowane tooa podsieci lub interfejs określonej sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="c6ff5-145">hello network security group rules can be applied tooa subnet or a specific virtual network interface.</span></span> <span data-ttu-id="c6ff5-146">Umożliwia dołączanie tooour hello podsieci zabezpieczeń grupy.</span><span class="sxs-lookup"><span data-stu-id="c6ff5-146">Lets attach hello network security group tooour subnet.</span></span> <span data-ttu-id="c6ff5-147">Dołącz grupy zabezpieczeń sieci toohello podsieci z [zaktualizować podsieci sieci wirtualnej sieci az](/cli/azure/network/vnet/subnet#update):</span><span class="sxs-lookup"><span data-stu-id="c6ff5-147">Attach your subnet toohello network security group with [az network vnet subnet update](/cli/azure/network/vnet/subnet#update):</span></span>

```azurecli
az network vnet subnet update \
    --resource-group myResourceGroup \
    --vnet-name myVnet \
    --name mySubnet \
    --network-security-group myNetworkSecurityGroup
```

## <a name="add-a-virtual-network-interface-card-toohello-subnet"></a><span data-ttu-id="c6ff5-148">Dodaj podsieć toohello karty interfejsu sieci wirtualnej</span><span class="sxs-lookup"><span data-stu-id="c6ff5-148">Add a virtual network interface card toohello subnet</span></span>

<span data-ttu-id="c6ff5-149">Karty interfejsu sieci wirtualnej (VNics) są ważne, ponieważ późniejszego łącząc je toodifferent maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="c6ff5-149">Virtual network interface cards (VNics) are important as you can reuse them by connecting them toodifferent VMs.</span></span> <span data-ttu-id="c6ff5-150">Ta ponownemu pozwala tookeep hello VNic jako zasób statycznych hello maszyny wirtualne mogą być tymczasowe.</span><span class="sxs-lookup"><span data-stu-id="c6ff5-150">This reuse allows you tookeep hello VNic as a static resource while hello VMs can be temporary.</span></span> <span data-ttu-id="c6ff5-151">Utwórz VNic i powiązać ją z podsiecią hello z [tworzenie kart interfejsu sieciowego az](/cli/azure/network/nic#create).</span><span class="sxs-lookup"><span data-stu-id="c6ff5-151">Create a VNic and associate it with hello subnet with [az network nic create](/cli/azure/network/nic#create).</span></span> <span data-ttu-id="c6ff5-152">Witaj poniższy przykład tworzy VNic, o nazwie *myNic*:</span><span class="sxs-lookup"><span data-stu-id="c6ff5-152">hello following example creates a VNic named *myNic*:</span></span>

```azurecli
az network nic create \
    --resource-group myResourceGroup \
    --location eastus \
    --name myNic \
    --vnet-name myVnet \
    --subnet mySubnet
```

## <a name="deploy-hello-vm-into-hello-virtual-network-infrastructure"></a><span data-ttu-id="c6ff5-153">Wdrażanie hello maszyny Wirtualnej do hello infrastruktury sieci wirtualnej</span><span class="sxs-lookup"><span data-stu-id="c6ff5-153">Deploy hello VM into hello virtual network infrastructure</span></span>

<span data-ttu-id="c6ff5-154">Istnieje już sieć wirtualną i podsieć i podsieć hello tooprotect grupy zabezpieczeń sieci przez blokuje cały ruch przychodzący z wyjątkiem port 22 dla protokołu SSH.</span><span class="sxs-lookup"><span data-stu-id="c6ff5-154">You now have a virtual network and subnet, and a network security group tooprotect hello subnet by blocking all inbound traffic except port 22 for SSH.</span></span> <span data-ttu-id="c6ff5-155">Teraz można wdrożyć Hello maszyny Wirtualnej w tym istniejącej infrastruktury sieci.</span><span class="sxs-lookup"><span data-stu-id="c6ff5-155">hello VM can now be deployed inside this existing network infrastructure.</span></span>

<span data-ttu-id="c6ff5-156">Tworzenie maszyny Wirtualnej z [tworzenia maszyny wirtualnej az](/cli/azure/vm#create).</span><span class="sxs-lookup"><span data-stu-id="c6ff5-156">Create your VM with [az vm create](/cli/azure/vm#create).</span></span> <span data-ttu-id="c6ff5-157">Aby uzyskać więcej informacji na temat hello flagi toouse z toodeploy hello Azure CLI 2.0 pełną maszyny Wirtualnej, zobacz [tworzyć kompletne środowisko systemu Linux przy użyciu interfejsu wiersza polecenia Azure hello](create-cli-complete.md).</span><span class="sxs-lookup"><span data-stu-id="c6ff5-157">For more information on hello flags toouse with hello Azure CLI 2.0 toodeploy a complete VM, see [Create a complete Linux environment by using hello Azure CLI](create-cli-complete.md).</span></span>

<span data-ttu-id="c6ff5-158">Witaj poniższy przykład tworzy Maszynę wirtualną za pomocą dysków zarządzanych platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="c6ff5-158">hello following example creates a VM using Azure Managed Disks.</span></span> <span data-ttu-id="c6ff5-159">Te dyski są obsługiwane przez hello platformy Azure i nie wymagają żadnych toostore przygotowania lub lokalizacji je.</span><span class="sxs-lookup"><span data-stu-id="c6ff5-159">These disks are handled by hello Azure platform and do not require any preparation or location toostore them.</span></span> <span data-ttu-id="c6ff5-160">Aby uzyskać więcej informacji o dyskach zarządzanych, zobacz [Omówienie usługi Azure Managed Disks](../../storage/storage-managed-disks-overview.md).</span><span class="sxs-lookup"><span data-stu-id="c6ff5-160">For more information about managed disks, see [Azure Managed Disks overview](../../storage/storage-managed-disks-overview.md).</span></span> <span data-ttu-id="c6ff5-161">Jeśli chcesz, aby dyski toouse niezarządzanych, zobacz hello dodatkowe Uwaga poniżej.</span><span class="sxs-lookup"><span data-stu-id="c6ff5-161">If you wish toouse unmanaged disks, see hello additional note below.</span></span>

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --image Debian \
    --admin-username azureuser \
    --generate-ssh-keys \
    --nics myNic
```

<span data-ttu-id="c6ff5-162">Użycie dysków zarządzanych, Pomiń ten krok.</span><span class="sxs-lookup"><span data-stu-id="c6ff5-162">If you use managed disks, skip this step.</span></span> <span data-ttu-id="c6ff5-163">Jeśli chcesz, aby dyski toouse niezarządzanych, należy hello tooadd następujące dodatkowe parametry toohello postępowania polecenia toocreate niezarządzanych dysków w hello konto magazynu o nazwie `mystorageaccount`:</span><span class="sxs-lookup"><span data-stu-id="c6ff5-163">If you wish toouse unmanaged disks, you need tooadd hello following additional parameters toohello proceeding command toocreate unmanaged disks in hello storage account named `mystorageaccount`:</span></span> 

```azurecli
    --use-unmanaged-disk \
    --storage-account mystorageaccount
```

<span data-ttu-id="c6ff5-164">Za pomocą hello interfejsu wiersza polecenia flagi toocall limit istniejących zasobów, poinstruuj hello Azure toodeploy VM wewnątrz hello istniejącej sieci.</span><span class="sxs-lookup"><span data-stu-id="c6ff5-164">By using hello CLI flags toocall out existing resources, you instruct Azure toodeploy hello VM inside hello existing network.</span></span> <span data-ttu-id="c6ff5-165">Po wdrożeniu sieci wirtualnej i podsieci, możesz je zostawić jako statyczne ani stałe zasoby w Twoim regionie Azure.</span><span class="sxs-lookup"><span data-stu-id="c6ff5-165">Once a virtual network and subnet have been deployed, they can be left as static or permanent resources inside your Azure region.</span></span> <span data-ttu-id="c6ff5-166">W tym przykładzie nie Utwórz i przypisz publicznego toohello adresu IP wirtualnej karty sieciowej, dlatego ta maszyna wirtualna nie jest dostępny publicznie za pośrednictwem Internetu hello.</span><span class="sxs-lookup"><span data-stu-id="c6ff5-166">In this example, you did not create and assign a public IP address toohello VNic, so this VM is not publicly accessible over hello Internet.</span></span> <span data-ttu-id="c6ff5-167">Aby uzyskać więcej informacji, zobacz [utworzyć Maszynę wirtualną z statycznego publicznego adresu IP za pomocą interfejsu wiersza polecenia Azure hello](../../virtual-network/virtual-network-deploy-static-pip-arm-cli.md).</span><span class="sxs-lookup"><span data-stu-id="c6ff5-167">For more information, see [Create a VM with a static public IP using hello Azure CLI](../../virtual-network/virtual-network-deploy-static-pip-arm-cli.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="c6ff5-168">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="c6ff5-168">Next steps</span></span>
<span data-ttu-id="c6ff5-169">Aby uzyskać więcej informacji o maszynach wirtualnych toocreate sposoby na platformie Azure zobacz następujące zasoby hello:</span><span class="sxs-lookup"><span data-stu-id="c6ff5-169">For more information about ways toocreate virtual machines in Azure, see hello following resources:</span></span>

* [<span data-ttu-id="c6ff5-170">Użyj toocreate szablonu usługi Azure Resource Manager określonego wdrożenia</span><span class="sxs-lookup"><span data-stu-id="c6ff5-170">Use an Azure Resource Manager template toocreate a specific deployment</span></span>](../windows/cli-deploy-templates.md)
* [<span data-ttu-id="c6ff5-171">Tworzenie niestandardowego środowiska dla maszyny wirtualnej z systemem Linux poprzez bezpośrednie użycie poleceń interfejsu wiersza polecenia platformy Azure</span><span class="sxs-lookup"><span data-stu-id="c6ff5-171">Create your own custom environment for a Linux VM using Azure CLI commands directly</span></span>](create-cli-complete.md)
* [<span data-ttu-id="c6ff5-172">Utwórz Maszynę wirtualną systemu Linux na platformie Azure za pomocą szablonów</span><span class="sxs-lookup"><span data-stu-id="c6ff5-172">Create a Linux VM on Azure using templates</span></span>](create-ssh-secured-vm-from-template.md)
