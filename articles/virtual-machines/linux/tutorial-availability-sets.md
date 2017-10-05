---
title: "Samouczek zestawy dostępności dla maszyn wirtualnych systemu Linux na platformie Azure | Dokumentacja firmy Microsoft"
description: "Informacje na temat zestawów dostępności dla maszyn wirtualnych systemu Linux na platformie Azure."
documentationcenter: 
services: virtual-machines-linux
author: cynthn
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 05/22/2017
ms.author: cynthn
ms.custom: mvc
ms.openlocfilehash: 63fe3f165864f06228604cac56d06cc061ab25f5
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
# <a name="how-to-use-availability-sets"></a><span data-ttu-id="409a3-103">Jak używać zestawów dostępności</span><span class="sxs-lookup"><span data-stu-id="409a3-103">How to use availability sets</span></span>


<span data-ttu-id="409a3-104">Z tego samouczka dowiesz się, jak zwiększyć dostępność i niezawodność rozwiązań maszyny wirtualnej na platformie Azure przy użyciu funkcji o nazwie zestawów dostępności.</span><span class="sxs-lookup"><span data-stu-id="409a3-104">In this tutorial, you will learn how to increase the availability and reliability of your Virtual Machine solutions on Azure using a capability called Availability Sets.</span></span> <span data-ttu-id="409a3-105">Zestawy dostępności upewnij się, czy maszyn wirtualnych, należy wdrożyć na platformie Azure są rozproszone na wielu klastrów izolowanego sprzętu.</span><span class="sxs-lookup"><span data-stu-id="409a3-105">Availability sets ensure that the VMs you deploy on Azure are distributed across multiple isolated hardware clusters.</span></span> <span data-ttu-id="409a3-106">W ten sposób zapewnia, że jeśli awarii sprzętu lub oprogramowania w systemie Azure wykonywany, jest ograniczona tylko do podzbioru maszyny wirtualne i które rozwiązania ogólną pozostanie dostępny i działa z perspektywy klientów przy użyciu go.</span><span class="sxs-lookup"><span data-stu-id="409a3-106">Doing this ensures that if a hardware or software failure within Azure happens, only a sub-set of your VMs will be impacted and that your overall solution will remain available and operational from the perspective of your customers using it.</span></span>

<span data-ttu-id="409a3-107">Ten samouczek zawiera informacje na temat wykonywania następujących czynności:</span><span class="sxs-lookup"><span data-stu-id="409a3-107">In this tutorial, you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="409a3-108">Tworzenie zestawu dostępności</span><span class="sxs-lookup"><span data-stu-id="409a3-108">Create an availability set</span></span>
> * <span data-ttu-id="409a3-109">Tworzenie maszyny Wirtualnej w zestawie dostępności</span><span class="sxs-lookup"><span data-stu-id="409a3-109">Create a VM in an availability set</span></span>
> * <span data-ttu-id="409a3-110">Sprawdź dostępne rozmiary maszyny Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="409a3-110">Check available VM sizes</span></span>


[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="409a3-111">Jeśli wybierzesz do zainstalowania i używania interfejsu wiersza polecenia lokalnie, w tym samouczku wymaga używasz interfejsu wiersza polecenia Azure w wersji 2.0.4 lub nowszej.</span><span class="sxs-lookup"><span data-stu-id="409a3-111">If you choose to install and use the CLI locally, this tutorial requires that you are running the Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="409a3-112">Uruchom polecenie `az --version`, aby dowiedzieć się, jaka wersja jest używana.</span><span class="sxs-lookup"><span data-stu-id="409a3-112">Run `az --version` to find the version.</span></span> <span data-ttu-id="409a3-113">Jeśli konieczna będzie instalacja lub uaktualnienie, zobacz [Instalowanie interfejsu wiersza polecenia platformy Azure 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="409a3-113">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="availability-set-overview"></a><span data-ttu-id="409a3-114">Omówienie zestawu dostępności</span><span class="sxs-lookup"><span data-stu-id="409a3-114">Availability set overview</span></span>

<span data-ttu-id="409a3-115">Zestawu dostępności jest możliwość grupę logiczną, która na platformie Azure umożliwia Sprawdź, czy zasobów maszyny Wirtualnej, który można umieścić w nim są odizolowane od siebie, gdy są wdrożone w centrum danych Azure.</span><span class="sxs-lookup"><span data-stu-id="409a3-115">An Availability Set is a logical grouping capability that you can use in Azure to ensure that the VM resources you place within it are isolated from each other when they are deployed within an Azure datacenter.</span></span> <span data-ttu-id="409a3-116">Azure zapewnia, że maszyny wirtualne, umieść w ramach zestawu dostępności uruchamiania na wielu serwerach fizycznych, obliczeniowe stojakami jednostek magazynowych i przełączniki sieciowe.</span><span class="sxs-lookup"><span data-stu-id="409a3-116">Azure ensures that the VMs you place within an Availability Set run across multiple physical servers, compute racks, storage units, and network switches.</span></span> <span data-ttu-id="409a3-117">Dzięki temu w przypadku awarii sprzętu lub oprogramowania Azure awarii, jest ograniczona tylko podzestaw maszyn wirtualnych, a aplikacja ogólna pozostanie w górę i nadal dostępne dla klientów.</span><span class="sxs-lookup"><span data-stu-id="409a3-117">This ensures that in the event of a hardware or Azure software failure, only a subset of your VMs will be impacted, and your overall application will stay up and continue to be available to your customers.</span></span> <span data-ttu-id="409a3-118">Przy użyciu zestawów dostępności jest podstawowych możliwości wykorzystać umożliwia tworzenia rozwiązań chmur wiarygodne.</span><span class="sxs-lookup"><span data-stu-id="409a3-118">Using Availability Sets is an essential capability to leverage when you want to build reliable cloud solutions.</span></span>

<span data-ttu-id="409a3-119">Zastanówmy typowe rozwiązania oparte na Maszynach którym może mieć 4 serwery frontonu sieci web i korzystać z 2 maszyny wirtualne zaplecza, które hostują bazy danych.</span><span class="sxs-lookup"><span data-stu-id="409a3-119">Let’s consider a typical VM-based solution where you might have 4 front-end web servers and use 2 back-end VMs that host a database.</span></span> <span data-ttu-id="409a3-120">Przy użyciu platformy Azure, należy zdefiniować dwa zestawy dostępności, przed wdrożeniem maszyn wirtualnych: jeden zbiór dostępności dla warstwy "web" i jeden zbiór dostępności dla warstwy "baza danych".</span><span class="sxs-lookup"><span data-stu-id="409a3-120">With Azure, you’d want to define two availability sets before you deploy your VMs: one availability set for the “web” tier and one availability set for the “database” tier.</span></span> <span data-ttu-id="409a3-121">Podczas tworzenia nowej maszyny Wirtualnej można określić zestaw dostępności jako parametr do maszyny wirtualnej az utworzyć polecenie, a Azure zostanie automatycznie upewnij się, że maszyny wirtualne utworzone w zestawie dostępne są izolowane między wieloma zasobami sprzętu fizycznego.</span><span class="sxs-lookup"><span data-stu-id="409a3-121">When you create a new VM you can then specify the availability set as a parameter to the az vm create command, and Azure will automatically ensure that the VMs you create within the available set are isolated across multiple physical hardware resources.</span></span> <span data-ttu-id="409a3-122">Oznacza to, że jeśli sprzęt fizyczny wykorzystywany do jednego serwera sieci Web lub maszyn wirtualnych z serwera bazy danych jest uruchomiona na ma problem, wiesz, że inne wystąpienia serwera sieci Web i bazy danych w maszynach wirtualnych pozostaną uruchomione prawidłowo ponieważ są one na inny komputer.</span><span class="sxs-lookup"><span data-stu-id="409a3-122">This means that if the physical hardware that one of your Web Server or Database Server VMs is running on has a problem, you know that the other instances of your Web Server and Database VMs will remain running fine because they are on different hardware.</span></span>

<span data-ttu-id="409a3-123">Zawsze należy używać zestawów dostępności, jeśli chcesz wdrożyć niezawodne rozwiązania na podstawie maszyny Wirtualnej w systemie Azure.</span><span class="sxs-lookup"><span data-stu-id="409a3-123">You should always use Availability Sets when you want to deploy reliable VM-based solutions within Azure.</span></span>


## <a name="create-an-availability-set"></a><span data-ttu-id="409a3-124">Tworzenie zestawu dostępności</span><span class="sxs-lookup"><span data-stu-id="409a3-124">Create an availability set</span></span>

<span data-ttu-id="409a3-125">Możesz utworzyć zestaw przy użyciu danych o dostępności [tworzenia maszyny wirtualnej az zestawu dostępności](/cli/azure/vm/availability-set#create).</span><span class="sxs-lookup"><span data-stu-id="409a3-125">You can create an availability set using [az vm availability-set create](/cli/azure/vm/availability-set#create).</span></span> <span data-ttu-id="409a3-126">W tym przykładzie umieszczania liczba domen aktualizacji i odporność na *2* dla zestawu o nazwie dostępności *myAvailabilitySet* w *myResourceGroupAvailability* grupy zasobów.</span><span class="sxs-lookup"><span data-stu-id="409a3-126">In this example, we set both the number of update and fault domains at *2* for the availability set named *myAvailabilitySet* in the *myResourceGroupAvailability* resource group.</span></span>

<span data-ttu-id="409a3-127">Utwórz grupę zasobów.</span><span class="sxs-lookup"><span data-stu-id="409a3-127">Create a resource group.</span></span>

```azurecli-interactive 
az group create --name myResourceGroupAvailability --location eastus
```


```azurecli-interactive 
az vm availability-set create \
    --resource-group myResourceGroupAvailability \
    --name myAvailabilitySet \
    --platform-fault-domain-count 2 \
    --platform-update-domain-count 2
```

<span data-ttu-id="409a3-128">Zestawy dostępności umożliwiają izolować zasobów między "domen błędów" i "Aktualizuj domeny".</span><span class="sxs-lookup"><span data-stu-id="409a3-128">Availability Sets allow you to isolate resources across "fault domains" and "update domains".</span></span> <span data-ttu-id="409a3-129">A **domeny błędów** reprezentuje kolekcję izolowanego server + sieć i Magazyn zasobów.</span><span class="sxs-lookup"><span data-stu-id="409a3-129">A **fault domain** represents an isolated collection of server + network + storage resources.</span></span> <span data-ttu-id="409a3-130">W powyższym przykładzie mamy wskazać, że firma Microsoft ma naszych dostępności ustawioną być rozproszone na co najmniej dwóch domen błędów, gdy naszych maszyny wirtualne są wdrażane.</span><span class="sxs-lookup"><span data-stu-id="409a3-130">In the preceding example, we indicate that we want our availability set to be distributed across at least two fault domains when our VMs are deployed.</span></span> <span data-ttu-id="409a3-131">Również wskazywać czy chcemy naszego zestawu rozproszonych w dwóch dostępności **zaktualizować domen**.</span><span class="sxs-lookup"><span data-stu-id="409a3-131">We also indicate that we want our availability set distributed across two **update domains**.</span></span>  <span data-ttu-id="409a3-132">Dwie domeny aktualizacji Sprawdź, czy w gdy platforma Azure stosuje aktualizacje oprogramowania naszych zasobów maszyny Wirtualnej są izolowane, co uniemożliwia całe oprogramowanie uruchomione poniżej naszych maszyny Wirtualnej z aktualizacji w tym samym czasie.</span><span class="sxs-lookup"><span data-stu-id="409a3-132">Two update domains ensure that when Azure performs software updates our VM resources are isolated, preventing all the software running underneath our VM from being updated at the same time.</span></span>

## <a name="configure-virtual-network"></a><span data-ttu-id="409a3-133">Skonfiguruj sieć wirtualną</span><span class="sxs-lookup"><span data-stu-id="409a3-133">Configure virtual network</span></span>
<span data-ttu-id="409a3-134">Przed wdrożeniem niektórych maszyn wirtualnych i przetestować z usługi równoważenia, Utwórz pomocnicze zasoby sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="409a3-134">Before you deploy some VMs and can test your balancer, create the supporting virtual network resources.</span></span> <span data-ttu-id="409a3-135">Aby uzyskać więcej informacji o sieciach wirtualnych, zobacz [Zarządzanie sieciami wirtualnymi Azure](tutorial-virtual-network.md) samouczka.</span><span class="sxs-lookup"><span data-stu-id="409a3-135">For more information about virtual networks, see the [Manage Azure Virtual Networks](tutorial-virtual-network.md) tutorial.</span></span>

### <a name="create-network-resources"></a><span data-ttu-id="409a3-136">Utwórz zasoby sieciowe</span><span class="sxs-lookup"><span data-stu-id="409a3-136">Create network resources</span></span>
<span data-ttu-id="409a3-137">Tworzenie sieci wirtualnej z [tworzenie sieci wirtualnej sieci az](/cli/azure/network/vnet#create).</span><span class="sxs-lookup"><span data-stu-id="409a3-137">Create a virtual network with [az network vnet create](/cli/azure/network/vnet#create).</span></span> <span data-ttu-id="409a3-138">Poniższy przykład tworzy sieć wirtualną o nazwie *myVnet* z podsiecią o nazwie *mySubnet*:</span><span class="sxs-lookup"><span data-stu-id="409a3-138">The following example creates a virtual network named *myVnet* with a subnet named *mySubnet*:</span></span>

```azurecli-interactive 
az network vnet create \
    --resource-group myResourceGroupAvailability \
    --name myVnet \
    --subnet-name mySubnet
```
<span data-ttu-id="409a3-139">Wirtualne karty sieciowe są tworzone za pomocą [tworzenie kart interfejsu sieciowego az](/cli/azure/network/nic#create).</span><span class="sxs-lookup"><span data-stu-id="409a3-139">Virtual NICs are created with [az network nic create](/cli/azure/network/nic#create).</span></span> <span data-ttu-id="409a3-140">Poniższy przykład tworzy trzy wirtualne karty sieciowe.</span><span class="sxs-lookup"><span data-stu-id="409a3-140">The following example creates three virtual NICs.</span></span> <span data-ttu-id="409a3-141">(Jedną wirtualną kartę Sieciową dla każdej maszyny Wirtualnej można utworzyć dla aplikacji w poniższych krokach).</span><span class="sxs-lookup"><span data-stu-id="409a3-141">(One virtual NIC for each VM you create for your app in the following steps).</span></span> <span data-ttu-id="409a3-142">Można utworzyć dodatkowe wirtualne karty sieciowe i maszyn wirtualnych w dowolnym momencie i dodaj je do usługi równoważenia obciążenia:</span><span class="sxs-lookup"><span data-stu-id="409a3-142">You can create additional virtual NICs and VMs at any time and add them to the load balancer:</span></span>

```bash
for i in `seq 1 3`; do
    az network nic create \
        --resource-group myResourceGroupAvailability \
        --name myNic$i \
        --vnet-name myVnet \
        --subnet mySubnet \
        --lb-name myLoadBalancer \
        --lb-address-pools myBackEndPool
done
```

## <a name="create-vms-inside-an-availability-set"></a><span data-ttu-id="409a3-143">Tworzenie maszyn wirtualnych w zestawie dostępności</span><span class="sxs-lookup"><span data-stu-id="409a3-143">Create VMs inside an availability set</span></span>

<span data-ttu-id="409a3-144">Maszyny wirtualne muszą być tworzone dostępność ustawioną upewnij się, że są one poprawnie dystrybuowana sprzętu.</span><span class="sxs-lookup"><span data-stu-id="409a3-144">VMs must be created within the availability set to make sure they are correctly distributed across the hardware.</span></span> <span data-ttu-id="409a3-145">Nie można dodać istniejącej maszyny Wirtualnej do dostępności po jego utworzeniu.</span><span class="sxs-lookup"><span data-stu-id="409a3-145">You can't add an existing VM to an availability set after it is created.</span></span> 

<span data-ttu-id="409a3-146">Po utworzeniu maszyny Wirtualnej przy użyciu [tworzenia maszyny wirtualnej az](/cli/azure/vm#create) określ zestaw, za pomocą dostępności `--availability-set` parametr, aby określić nazwę zestawu dostępności.</span><span class="sxs-lookup"><span data-stu-id="409a3-146">When you create a VM using [az vm create](/cli/azure/vm#create) you specify the availability set using the `--availability-set` parameter to specify the name of the availability set.</span></span>

```azurecli-interactive 
for i in `seq 1 2`; do
   az vm create \
     --resource-group myResourceGroupAvailability \
     --name myVM$i \
     --availability-set myAvailabilitySet \
     --nics myNic$i \
     --size Standard_DS1_v2  \
     --image Canonical:UbuntuServer:14.04.4-LTS:latest \
     --admin-username azureuser \
     --generate-ssh-keys \
     --no-wait
done 
```

<span data-ttu-id="409a3-147">Mamy teraz dwie maszyny wirtualne w naszym zestawie dostępności nowo utworzony.</span><span class="sxs-lookup"><span data-stu-id="409a3-147">We now have two virtual machines within our newly created availability set.</span></span> <span data-ttu-id="409a3-148">Ponieważ są one w tym samym zestawie dostępności, Azure zapewni, że maszyn wirtualnych i ich zasobów (w tym dysków z danymi) są rozmieszczane izolowanego sprzętu fizycznego.</span><span class="sxs-lookup"><span data-stu-id="409a3-148">Because they are in the same availability set, Azure will ensure that the VMs and all their resources (including data disks) are distributed across isolated physical hardware.</span></span> <span data-ttu-id="409a3-149">Tej dystrybucji zapewnia znacznie wyższą dostępność naszych ogólnego rozwiązania maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="409a3-149">This distribution helps ensure much higher availability of our overall VM solution.</span></span>

<span data-ttu-id="409a3-150">Jedyną operacją, której można napotkać podczas dodawania maszyn wirtualnych jest, że określonego rozmiaru maszyny Wirtualnej nie jest już dostępny do użycia w zestawie dostępności.</span><span class="sxs-lookup"><span data-stu-id="409a3-150">One thing you may encounter as you add VMs is that a particular VM size is no longer available to use within your availability set.</span></span> <span data-ttu-id="409a3-151">Ten problem może się zdarzyć, jeśli nie jest dostępna wystarczająca pojemność dodać ją przy zachowaniu zasady izolacji wymusza zestawu dostępności.</span><span class="sxs-lookup"><span data-stu-id="409a3-151">This issue can happen if there is no longer enough capacity to add it while preserving the isolation rules the availability set enforces.</span></span> <span data-ttu-id="409a3-152">Można sprawdzić, jakie rozmiarów maszyn wirtualnych są dostępne do użycia w istniejących dostępności ustawić za pomocą `--availability-set list-sizes` parametru.</span><span class="sxs-lookup"><span data-stu-id="409a3-152">You can check to see what VM sizes are available to use within an existing availability set using the `--availability-set list-sizes` parameter.</span></span>

## <a name="check-for-available-vm-sizes"></a><span data-ttu-id="409a3-153">Sprawdź, czy dostępne rozmiary maszyny Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="409a3-153">Check for available VM sizes</span></span> 

<span data-ttu-id="409a3-154">Możesz dodać więcej maszyn wirtualnych do później zestaw dostępności, ale musisz wiedzieć, jaki rozmiarów maszyn wirtualnych są dostępne na sprzęcie.</span><span class="sxs-lookup"><span data-stu-id="409a3-154">You can add more VMs to the availability set later, but you need to know what VM sizes are available on the hardware.</span></span> <span data-ttu-id="409a3-155">Użyj [az listy rozmiarów maszyn wirtualnych zestawu dostępności](/cli/azure/availability-set#list-sizes) Aby wyświetlić listę wszystkich dostępnych rozmiarów na sprzęcie klastra dla zestawu dostępności.</span><span class="sxs-lookup"><span data-stu-id="409a3-155">Use [az vm availability-set list-sizes](/cli/azure/availability-set#list-sizes) to list all the available sizes on the hardware cluster for the availability set.</span></span>

```azurecli-interactive 
az vm availability-set list-sizes \
     --resource-group myResourceGroupAvailability \
     --name myAvailabilitySet \
     --output table  
```

## <a name="next-steps"></a><span data-ttu-id="409a3-156">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="409a3-156">Next steps</span></span>

<span data-ttu-id="409a3-157">W niniejszym samouczku zawarto informacje na temat wykonywania następujących czynności:</span><span class="sxs-lookup"><span data-stu-id="409a3-157">In this tutorial, you learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="409a3-158">Tworzenie zestawu dostępności</span><span class="sxs-lookup"><span data-stu-id="409a3-158">Create an availability set</span></span>
> * <span data-ttu-id="409a3-159">Tworzenie maszyny Wirtualnej w zestawie dostępności</span><span class="sxs-lookup"><span data-stu-id="409a3-159">Create a VM in an availability set</span></span>
> * <span data-ttu-id="409a3-160">Sprawdź dostępne rozmiary maszyny Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="409a3-160">Check available VM sizes</span></span>

<span data-ttu-id="409a3-161">Przejdź do następnego samouczkiem, aby poznać zestawy skalowania maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="409a3-161">Advance to the next tutorial to learn about virtual machine scale sets.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="409a3-162">Tworzenie zestawu skalowania maszyn wirtualnych</span><span class="sxs-lookup"><span data-stu-id="409a3-162">Create a VM scale set</span></span>](tutorial-create-vmss.md)

