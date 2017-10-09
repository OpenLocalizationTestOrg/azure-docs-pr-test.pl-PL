---
title: "aaaUse wewnętrzny serwer DNS dla maszyny Wirtualnej do rozpoznawania nazw z hello Azure CLI 2.0 | Dokumentacja firmy Microsoft"
description: "Jak sieci wirtualnej toocreate kartami interfejsu i korzystania z wewnętrznego serwera DNS do rozpoznawania nazw maszyny Wirtualnej na platformie Azure z hello Azure CLI 2.0"
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
ms.openlocfilehash: b3c4bfd3ab698f7b25d763ba9e60dd7984f6269d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-virtual-network-interface-cards-and-use-internal-dns-for-vm-name-resolution-on-azure"></a><span data-ttu-id="e8a55-103">Tworzenie karty interfejsu sieci wirtualnej i korzystania z wewnętrznego serwera DNS do rozpoznawania nazw maszyny Wirtualnej na platformie Azure</span><span class="sxs-lookup"><span data-stu-id="e8a55-103">Create virtual network interface cards and use internal DNS for VM name resolution on Azure</span></span>
<span data-ttu-id="e8a55-104">W tym artykule opisano, jak tooset statyczne wewnętrzne nazwy DNS dla maszyn wirtualnych systemu Linux przy użyciu wirtualnej sieci karty interfejsu (vNics) i nazwy etykiety DNS z hello Azure CLI 2.0.</span><span class="sxs-lookup"><span data-stu-id="e8a55-104">This article shows you how tooset static internal DNS names for Linux VMs using virtual network interface cards (vNics) and DNS label names with hello Azure CLI 2.0.</span></span> <span data-ttu-id="e8a55-105">Można również wykonać te kroki hello [Azure CLI 1.0](static-dns-name-resolution-for-linux-on-azure-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="e8a55-105">You can also perform these steps with hello [Azure CLI 1.0](static-dns-name-resolution-for-linux-on-azure-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> <span data-ttu-id="e8a55-106">Statyczne nazwy DNS są używane dla usług trwałych infrastruktury, takich jak serwer kompilacji Wpięć, który służy do tego dokumentu lub serwer Git.</span><span class="sxs-lookup"><span data-stu-id="e8a55-106">Static DNS names are used for permanent infrastructure services like a Jenkins build server, which is used for this document, or a Git server.</span></span>

<span data-ttu-id="e8a55-107">wymagania dotyczące Hello są:</span><span class="sxs-lookup"><span data-stu-id="e8a55-107">hello requirements are:</span></span>

* [<span data-ttu-id="e8a55-108">Konto platformy Azure</span><span class="sxs-lookup"><span data-stu-id="e8a55-108">an Azure account</span></span>](https://azure.microsoft.com/pricing/free-trial/)
* [<span data-ttu-id="e8a55-109">Pliki kluczy publicznych i prywatnych SSH</span><span class="sxs-lookup"><span data-stu-id="e8a55-109">SSH public and private key files</span></span>](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

## <a name="quick-commands"></a><span data-ttu-id="e8a55-110">Szybkie polecenia</span><span class="sxs-lookup"><span data-stu-id="e8a55-110">Quick commands</span></span>
<span data-ttu-id="e8a55-111">Jeśli potrzebujesz tooquickly hello zadania, powitania po sekcji Szczegóły poleceń hello potrzebne.</span><span class="sxs-lookup"><span data-stu-id="e8a55-111">If you need tooquickly accomplish hello task, hello following section details hello commands needed.</span></span> <span data-ttu-id="e8a55-112">Bardziej szczegółowe informacje i kontekst dla każdego kroku można znaleźć w hello pozostałej części dokumentu hello [uruchamiania tutaj](#detailed-walkthrough).</span><span class="sxs-lookup"><span data-stu-id="e8a55-112">More detailed information and context for each step can be found in hello rest of hello document, [starting here](#detailed-walkthrough).</span></span> <span data-ttu-id="e8a55-113">tooperform tych kroków, należy hello najnowszych [Azure CLI 2.0](/cli/azure/install-az-cli2) zainstalowane i zarejestrowane za pomocą konta Azure tooan [logowania az](/cli/azure/#login).</span><span class="sxs-lookup"><span data-stu-id="e8a55-113">tooperform these steps, you need hello latest [Azure CLI 2.0](/cli/azure/install-az-cli2) installed and logged in tooan Azure account using [az login](/cli/azure/#login).</span></span>

<span data-ttu-id="e8a55-114">Wymagania Wstępne: Grupy zasobów, sieć wirtualną i podsieć, grupy zabezpieczeń sieci przy użyciu protokołu SSH ruchu przychodzącego.</span><span class="sxs-lookup"><span data-stu-id="e8a55-114">Pre-Requirements: Resource Group, virtual network and subnet, Network Security Group with SSH inbound.</span></span>

### <a name="create-a-virtual-network-interface-card-with-a-static-internal-dns-name"></a><span data-ttu-id="e8a55-115">Utwórz karty interfejsu sieci wirtualnej o nazwie DNS wewnętrzny statycznej</span><span class="sxs-lookup"><span data-stu-id="e8a55-115">Create a virtual network interface card with a static internal DNS name</span></span>
<span data-ttu-id="e8a55-116">Utwórz vNic hello z [tworzenie kart interfejsu sieciowego az](/cli/azure/network/nic#create).</span><span class="sxs-lookup"><span data-stu-id="e8a55-116">Create hello vNic with [az network nic create](/cli/azure/network/nic#create).</span></span> <span data-ttu-id="e8a55-117">Witaj `--internal-dns-name` Flaga interfejsu wiersza polecenia jest ustawienie hello DNS etykiety, który zapewnia hello statycznej nazwy DNS dla karty interfejsu sieci wirtualnej hello (vNic).</span><span class="sxs-lookup"><span data-stu-id="e8a55-117">hello `--internal-dns-name` CLI flag is for setting hello DNS label, which provides hello static DNS name for hello virtual network interface card (vNic).</span></span> <span data-ttu-id="e8a55-118">Witaj poniższy przykład tworzy vNic, o nazwie `myNic`, połączony toohello `myVnet` sieci wirtualnej i tworzy wewnętrzny rekordu nazwy DNS nazywanego `jenkins`:</span><span class="sxs-lookup"><span data-stu-id="e8a55-118">hello following example creates a vNic named `myNic`, connects it toohello `myVnet` virtual network, and creates an internal DNS name record called `jenkins`:</span></span>

```azurecli
az network nic create \
    --resource-group myResourceGroup \
    --name myNic \
    --vnet-name myVnet \
    --subnet mySubnet \
    --internal-dns-name jenkins
```

### <a name="deploy-a-vm-and-connect-hello-vnic"></a><span data-ttu-id="e8a55-119">Wdróż Maszynę wirtualną i połączyć hello vNic</span><span class="sxs-lookup"><span data-stu-id="e8a55-119">Deploy a VM and connect hello vNic</span></span>
<span data-ttu-id="e8a55-120">Utwórz maszynę wirtualną za pomocą polecenia [az vm create](/cli/azure/vm#create).</span><span class="sxs-lookup"><span data-stu-id="e8a55-120">Create a VM with [az vm create](/cli/azure/vm#create).</span></span> <span data-ttu-id="e8a55-121">Witaj `--nics` flagi łączy hello vNic toohello maszyny Wirtualnej podczas hello tooAzure wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="e8a55-121">hello `--nics` flag connects hello vNic toohello VM during hello deployment tooAzure.</span></span> <span data-ttu-id="e8a55-122">Witaj poniższy przykład tworzy Maszynę wirtualną o nazwie `myVM` z dyskami zarządzane Azure i dołącza hello vNic o nazwie `myNic` z hello poprzedzających krok:</span><span class="sxs-lookup"><span data-stu-id="e8a55-122">hello following example creates a VM named `myVM` with Azure Managed Disks and attaches hello vNic named `myNic` from hello preceding step:</span></span>

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --nics myNic \
    --image UbuntuLTS \
    --admin-username azureuser \
    --ssh-key-value ~/.ssh/id_rsa.pub
```

## <a name="detailed-walkthrough"></a><span data-ttu-id="e8a55-123">Szczegółowy przewodnik</span><span class="sxs-lookup"><span data-stu-id="e8a55-123">Detailed walkthrough</span></span>

<span data-ttu-id="e8a55-124">Pełne ciągłej integracji i ciągłe wdrażanie (CiCd) infrastruktury na platformie Azure wymaga niektórych toobe statyczne lub długotrwałe serwery.</span><span class="sxs-lookup"><span data-stu-id="e8a55-124">A full continuous integration and continuous deployment (CiCd) infrastructure on Azure requires certain servers toobe static or long-lived servers.</span></span> <span data-ttu-id="e8a55-125">Zaleca się, że Azure zasoby, takie jak hello sieci wirtualnych i sieciowe grupy zabezpieczeń są statyczne i tam długo zasoby, które rzadko są wdrożone.</span><span class="sxs-lookup"><span data-stu-id="e8a55-125">It is recommended that Azure assets like hello virtual networks and Network Security Groups are static and long lived resources that are rarely deployed.</span></span> <span data-ttu-id="e8a55-126">Po wdrożeniu sieci wirtualnej można użyć ponownie przez nowych wdrożeń bez żadnych infrastruktury toohello niekorzystny wpływ.</span><span class="sxs-lookup"><span data-stu-id="e8a55-126">Once a virtual network has been deployed, it can be reused by new deployments without any adverse affects toohello infrastructure.</span></span> <span data-ttu-id="e8a55-127">Później można dodać serwer repozytorium Git lub serwer automatyzacji Wpięć dostarcza CiCd toothis sieci wirtualnej środowiska deweloperskich lub testowania.</span><span class="sxs-lookup"><span data-stu-id="e8a55-127">You can later add a Git repository server or a Jenkins automation server delivers CiCd toothis virtual network for your development or test environments.</span></span>  

<span data-ttu-id="e8a55-128">Wewnętrzny nazw DNS są tylko rozpoznawany w sieci wirtualnej platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="e8a55-128">Internal DNS names are only resolvable inside an Azure virtual network.</span></span> <span data-ttu-id="e8a55-129">Ponieważ nazwy DNS hello są wewnętrzne, nie są one rozpoznawalną toohello poza internet, zapewniając dodatkowe zabezpieczenia toohello infrastruktury.</span><span class="sxs-lookup"><span data-stu-id="e8a55-129">Because hello DNS names are internal, they are not resolvable toohello outside internet, providing additional security toohello infrastructure.</span></span>

<span data-ttu-id="e8a55-130">Poniższe przykłady w hello Zastąp przykładowe nazwy parametrów własne wartości.</span><span class="sxs-lookup"><span data-stu-id="e8a55-130">In hello following examples, replace example parameter names with your own values.</span></span> <span data-ttu-id="e8a55-131">Przykład nazwy parametru zawierają `myResourceGroup`, `myNic`, i `myVM`.</span><span class="sxs-lookup"><span data-stu-id="e8a55-131">Example parameter names include `myResourceGroup`, `myNic`, and `myVM`.</span></span>

## <a name="create-hello-resource-group"></a><span data-ttu-id="e8a55-132">Utwórz grupę zasobów hello</span><span class="sxs-lookup"><span data-stu-id="e8a55-132">Create hello resource group</span></span>
<span data-ttu-id="e8a55-133">Najpierw należy utworzyć grupy zasobów hello z [Tworzenie grupy az](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="e8a55-133">First, create hello resource group with [az group create](/cli/azure/group#create).</span></span> <span data-ttu-id="e8a55-134">Witaj poniższy przykład tworzy grupę zasobów o nazwie `myResourceGroup` w hello `westus` lokalizacji:</span><span class="sxs-lookup"><span data-stu-id="e8a55-134">hello following example creates a resource group named `myResourceGroup` in hello `westus` location:</span></span>

```azurecli
az group create --name myResourceGroup --location westus
```

## <a name="create-hello-virtual-network"></a><span data-ttu-id="e8a55-135">Utwórz sieć wirtualną hello</span><span class="sxs-lookup"><span data-stu-id="e8a55-135">Create hello virtual network</span></span>

<span data-ttu-id="e8a55-136">Witaj następnym krokiem jest toobuild maszyn wirtualnych do hello toolaunch sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="e8a55-136">hello next step is toobuild a virtual network toolaunch hello VMs into.</span></span> <span data-ttu-id="e8a55-137">sieć wirtualna Hello zawiera jedną podsieć w ramach tego przewodnika.</span><span class="sxs-lookup"><span data-stu-id="e8a55-137">hello virtual network contains one subnet for this walkthrough.</span></span> <span data-ttu-id="e8a55-138">Aby uzyskać więcej informacji o sieci wirtualnych platformy Azure, zobacz [utworzyć sieć wirtualną przy użyciu interfejsu wiersza polecenia Azure hello](../../virtual-network/virtual-networks-create-vnet-arm-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="e8a55-138">For more information on Azure virtual networks, see [Create a virtual network by using hello Azure CLI](../../virtual-network/virtual-networks-create-vnet-arm-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> 

<span data-ttu-id="e8a55-139">Utwórz sieć wirtualną hello z [tworzenie sieci wirtualnej sieci az](/cli/azure/network/vnet#create).</span><span class="sxs-lookup"><span data-stu-id="e8a55-139">Create hello virtual network with [az network vnet create](/cli/azure/network/vnet#create).</span></span> <span data-ttu-id="e8a55-140">Witaj poniższy przykład tworzy sieć wirtualną o nazwie `myVnet` i podsieć o nazwie `mySubnet`:</span><span class="sxs-lookup"><span data-stu-id="e8a55-140">hello following example creates a virtual network named `myVnet` and subnet named `mySubnet`:</span></span>

```azurecli
az network vnet create \
    --resource-group myResourceGroup \
    --name myVnet \
    --address-prefix 192.168.0.0/16 \
    --subnet-name mySubnet \
    --subnet-prefix 192.168.1.0/24
```

## <a name="create-hello-network-security-group"></a><span data-ttu-id="e8a55-141">Utwórz hello grupy zabezpieczeń sieci</span><span class="sxs-lookup"><span data-stu-id="e8a55-141">Create hello Network Security Group</span></span>
<span data-ttu-id="e8a55-142">Grupy zabezpieczeń sieci platformy Azure są równoważne tooa zapory na powitania warstwy sieci.</span><span class="sxs-lookup"><span data-stu-id="e8a55-142">Azure Network Security Groups are equivalent tooa firewall at hello network layer.</span></span> <span data-ttu-id="e8a55-143">Aby uzyskać więcej informacji na temat grup zabezpieczeń sieci, zobacz [jak grupy NSG toocreate w hello Azure CLI](../../virtual-network/virtual-networks-create-nsg-arm-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="e8a55-143">For more information about Network Security Groups, see [How toocreate NSGs in hello Azure CLI](../../virtual-network/virtual-networks-create-nsg-arm-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> 

<span data-ttu-id="e8a55-144">Utwórz grupę zabezpieczeń sieci hello z [utworzyć nsg sieci az](/cli/azure/network/nsg#create).</span><span class="sxs-lookup"><span data-stu-id="e8a55-144">Create hello network security group with [az network nsg create](/cli/azure/network/nsg#create).</span></span> <span data-ttu-id="e8a55-145">Witaj poniższy przykład tworzy sieciową grupę zabezpieczeń o nazwie `myNetworkSecurityGroup`:</span><span class="sxs-lookup"><span data-stu-id="e8a55-145">hello following example creates a network security group named `myNetworkSecurityGroup`:</span></span>

```azurecli
az network nsg create \
    --resource-group myResourceGroup \
    --name myNetworkSecurityGroup
```

## <a name="add-an-inbound-rule-tooallow-ssh"></a><span data-ttu-id="e8a55-146">Dodaj regułę ruchu przychodzącego tooallow SSH</span><span class="sxs-lookup"><span data-stu-id="e8a55-146">Add an inbound rule tooallow SSH</span></span>
<span data-ttu-id="e8a55-147">Dodaj regułę ruchu przychodzącego dla sieciowej grupy zabezpieczeń z hello [Tworzenie reguły nsg sieci az](/cli/azure/network/nsg/rule#create).</span><span class="sxs-lookup"><span data-stu-id="e8a55-147">Add an inbound rule for hello network security group with [az network nsg rule create](/cli/azure/network/nsg/rule#create).</span></span> <span data-ttu-id="e8a55-148">Witaj poniższy przykład powoduje utworzenie reguły o nazwie `myRuleAllowSSH`:</span><span class="sxs-lookup"><span data-stu-id="e8a55-148">hello following example creates a rule named `myRuleAllowSSH`:</span></span>

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

## <a name="associate-hello-subnet-with-hello-network-security-group"></a><span data-ttu-id="e8a55-149">Podsieć hello skojarzona z hello grupy zabezpieczeń sieci</span><span class="sxs-lookup"><span data-stu-id="e8a55-149">Associate hello subnet with hello Network Security Group</span></span>
<span data-ttu-id="e8a55-150">podsieć hello tooassociate z hello sieciowej grupy zabezpieczeń, użyj [zaktualizować podsieci sieci wirtualnej sieci az](/cli/azure/network/vnet/subnet#update).</span><span class="sxs-lookup"><span data-stu-id="e8a55-150">tooassociate hello subnet with hello Network Security Group, use [az network vnet subnet update](/cli/azure/network/vnet/subnet#update).</span></span> <span data-ttu-id="e8a55-151">Witaj poniższy przykład powoduje skojarzenie nazwy podsieci hello `mySubnet` z hello sieciową grupę zabezpieczeń o nazwie `myNetworkSecurityGroup`:</span><span class="sxs-lookup"><span data-stu-id="e8a55-151">hello following example associates hello subnet name `mySubnet` with hello Network Security Group named `myNetworkSecurityGroup`:</span></span>

```azurecli
az network vnet subnet update \
    --resource-group myResourceGroup \
    --vnet-name myVnet \
    --name mySubnet \
    --network-security-group myNetworkSecurityGroup
```


## <a name="create-hello-virtual-network-interface-card-and-static-dns-names"></a><span data-ttu-id="e8a55-152">Utwórz statycznej nazwy DNS i hello wirtualnej karty sieciowej</span><span class="sxs-lookup"><span data-stu-id="e8a55-152">Create hello virtual network interface card and static DNS names</span></span>
<span data-ttu-id="e8a55-153">Platforma Azure jest bardzo elastyczne, ale toouse nazwy DNS dla rozpoznawania nazw maszyny Wirtualnej, należy toocreate wirtualne karty sieciowe (vNics) zawierających etykietę DNS.</span><span class="sxs-lookup"><span data-stu-id="e8a55-153">Azure is very flexible, but toouse DNS names for VM name resolution, you need toocreate virtual network interface cards (vNics) that include a DNS label.</span></span> <span data-ttu-id="e8a55-154">vNics są ważne, ponieważ późniejszego przez połączenie ich maszyn wirtualnych toodifferent cyklem hello infrastruktury.</span><span class="sxs-lookup"><span data-stu-id="e8a55-154">vNics are important as you can reuse them by connecting them toodifferent VMs over hello infrastructure lifecycle.</span></span> <span data-ttu-id="e8a55-155">Takie podejście zapewnia hello vNic jako zasób statycznych hello maszyny wirtualne mogą być tymczasowe.</span><span class="sxs-lookup"><span data-stu-id="e8a55-155">This approach keeps hello vNic as a static resource while hello VMs can be temporary.</span></span> <span data-ttu-id="e8a55-156">Przy użyciu systemu DNS etykietowania na karcie vNic hello, możemy rozpoznawania nazw proste stanie tooenable z innych maszyn wirtualnych w hello sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="e8a55-156">By using DNS labeling on hello vNic, we are able tooenable simple name resolution from other VMs in hello VNet.</span></span> <span data-ttu-id="e8a55-157">Przy użyciu nazwy rozpoznawalną umożliwia inny serwer automatyzacji hello tooaccess maszyn wirtualnych na podstawie nazwy DNS hello `Jenkins` lub na serwerze Git hello `gitrepo`.</span><span class="sxs-lookup"><span data-stu-id="e8a55-157">Using resolvable names enables other VMs tooaccess hello automation server by hello DNS name `Jenkins` or hello Git server as `gitrepo`.</span></span>  

<span data-ttu-id="e8a55-158">Utwórz vNic hello z [tworzenie kart interfejsu sieciowego az](/cli/azure/network/nic#create).</span><span class="sxs-lookup"><span data-stu-id="e8a55-158">Create hello vNic with [az network nic create](/cli/azure/network/nic#create).</span></span> <span data-ttu-id="e8a55-159">Witaj poniższy przykład tworzy vNic, o nazwie `myNic`, połączony toohello `myVnet` sieci wirtualnej o nazwie `myVnet`i tworzy wewnętrzny rekordu nazwy DNS nazywanego `jenkins`:</span><span class="sxs-lookup"><span data-stu-id="e8a55-159">hello following example creates a vNic named `myNic`, connects it toohello `myVnet` virtual network named `myVnet`, and creates an internal DNS name record called `jenkins`:</span></span>

```azurecli
az network nic create \
    --resource-group myResourceGroup \
    --name myNic \
    --vnet-name myVnet \
    --subnet mySubnet \
    --internal-dns-name jenkins
```

## <a name="deploy-hello-vm-into-hello-virtual-network-infrastructure"></a><span data-ttu-id="e8a55-160">Wdrażanie hello maszyny Wirtualnej do hello infrastruktury sieci wirtualnej</span><span class="sxs-lookup"><span data-stu-id="e8a55-160">Deploy hello VM into hello virtual network infrastructure</span></span>
<span data-ttu-id="e8a55-161">Mamy teraz sieć wirtualna i podsieć, działając jako tooprotect zapory naszych podsieci blokuje cały ruch przychodzący z wyjątkiem port 22 protokołu SSH i vNic grupa zabezpieczeń sieci.</span><span class="sxs-lookup"><span data-stu-id="e8a55-161">We now have a virtual network and subnet, a Network Security Group acting as a firewall tooprotect our subnet by blocking all inbound traffic except port 22 for SSH, and a vNic.</span></span> <span data-ttu-id="e8a55-162">Teraz można wdrożyć maszyny Wirtualnej w tym istniejącej infrastruktury sieci.</span><span class="sxs-lookup"><span data-stu-id="e8a55-162">You can now deploy a VM inside this existing network infrastructure.</span></span>

<span data-ttu-id="e8a55-163">Utwórz maszynę wirtualną za pomocą polecenia [az vm create](/cli/azure/vm#create).</span><span class="sxs-lookup"><span data-stu-id="e8a55-163">Create a VM with [az vm create](/cli/azure/vm#create).</span></span> <span data-ttu-id="e8a55-164">Witaj poniższy przykład tworzy Maszynę wirtualną o nazwie `myVM` z dyskami zarządzane Azure i dołącza hello vNic o nazwie `myNic` z hello poprzedzających krok:</span><span class="sxs-lookup"><span data-stu-id="e8a55-164">hello following example creates a VM named `myVM` with Azure Managed Disks and attaches hello vNic named `myNic` from hello preceding step:</span></span>

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --nics myNic \
    --image UbuntuLTS \
    --admin-username azureuser \
    --ssh-key-value ~/.ssh/id_rsa.pub
```

<span data-ttu-id="e8a55-165">Za pomocą hello interfejsu wiersza polecenia flagi toocall limit istniejących zasobów, firma Microsoft poinstruować hello Azure toodeploy VM wewnątrz hello istniejącej sieci.</span><span class="sxs-lookup"><span data-stu-id="e8a55-165">By using hello CLI flags toocall out existing resources, we instruct Azure toodeploy hello VM inside hello existing network.</span></span> <span data-ttu-id="e8a55-166">tooreiterate, po wdrożeniu sieci wirtualnej i podsieci, ich może pozostać statyczne ani stałe zasobów w Twoim regionie Azure.</span><span class="sxs-lookup"><span data-stu-id="e8a55-166">tooreiterate, once a VNet and subnet have been deployed, they can be left as static or permanent resources inside your Azure region.</span></span>  

## <a name="next-steps"></a><span data-ttu-id="e8a55-167">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="e8a55-167">Next steps</span></span>
* [<span data-ttu-id="e8a55-168">Tworzenie niestandardowego środowiska dla maszyny wirtualnej z systemem Linux poprzez bezpośrednie użycie poleceń interfejsu wiersza polecenia platformy Azure</span><span class="sxs-lookup"><span data-stu-id="e8a55-168">Create your own custom environment for a Linux VM using Azure CLI commands directly</span></span>](create-cli-complete.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [<span data-ttu-id="e8a55-169">Utwórz Maszynę wirtualną systemu Linux na platformie Azure za pomocą szablonów</span><span class="sxs-lookup"><span data-stu-id="e8a55-169">Create a Linux VM on Azure using templates</span></span>](create-ssh-secured-vm-from-template.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
