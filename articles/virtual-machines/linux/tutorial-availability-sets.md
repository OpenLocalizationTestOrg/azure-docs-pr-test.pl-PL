---
title: aaaAvailability ustawia samouczek dla maszyn wirtualnych systemu Linux na platformie Azure | Dokumentacja firmy Microsoft
description: "Dowiedz się więcej o hello zestawów dostępności dla maszyn wirtualnych systemu Linux na platformie Azure."
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
ms.openlocfilehash: 2a91e4a6057180035ec51410d9fffccaca343758
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-availability-sets"></a><span data-ttu-id="6eb9b-103">Jak zestawy dostępności toouse</span><span class="sxs-lookup"><span data-stu-id="6eb9b-103">How toouse availability sets</span></span>


<span data-ttu-id="6eb9b-104">Z tego samouczka dowiesz się, jak tooincrease hello dostępność i niezawodność rozwiązań maszyny wirtualnej na platformie Azure przy użyciu funkcji o nazwie zestawów dostępności.</span><span class="sxs-lookup"><span data-stu-id="6eb9b-104">In this tutorial, you will learn how tooincrease hello availability and reliability of your Virtual Machine solutions on Azure using a capability called Availability Sets.</span></span> <span data-ttu-id="6eb9b-105">Zestawy dostępności upewnij się, tym powitalne wdrażanie na platformie Azure maszyny wirtualne rozproszone na wielu klastrów izolowanego sprzętu.</span><span class="sxs-lookup"><span data-stu-id="6eb9b-105">Availability sets ensure that hello VMs you deploy on Azure are distributed across multiple isolated hardware clusters.</span></span> <span data-ttu-id="6eb9b-106">W ten sposób zapewnia, że jeśli awarii sprzętu lub oprogramowania w systemie Azure wykonywany, jest ograniczona tylko do podzbioru maszyny wirtualne i które rozwiązania ogólną pozostanie dostępny i działa z punktu widzenia hello klientów przy użyciu go.</span><span class="sxs-lookup"><span data-stu-id="6eb9b-106">Doing this ensures that if a hardware or software failure within Azure happens, only a sub-set of your VMs will be impacted and that your overall solution will remain available and operational from hello perspective of your customers using it.</span></span>

<span data-ttu-id="6eb9b-107">Ten samouczek zawiera informacje na temat wykonywania następujących czynności:</span><span class="sxs-lookup"><span data-stu-id="6eb9b-107">In this tutorial, you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="6eb9b-108">Tworzenie zestawu dostępności</span><span class="sxs-lookup"><span data-stu-id="6eb9b-108">Create an availability set</span></span>
> * <span data-ttu-id="6eb9b-109">Tworzenie maszyny Wirtualnej w zestawie dostępności</span><span class="sxs-lookup"><span data-stu-id="6eb9b-109">Create a VM in an availability set</span></span>
> * <span data-ttu-id="6eb9b-110">Sprawdź dostępne rozmiary maszyny Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="6eb9b-110">Check available VM sizes</span></span>


[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="6eb9b-111">Jeśli wybierz tooinstall i użyj interfejsu wiersza polecenia hello lokalnie, w tym samouczku wymaga działają hello Azure CLI w wersji 2.0.4 lub nowszej.</span><span class="sxs-lookup"><span data-stu-id="6eb9b-111">If you choose tooinstall and use hello CLI locally, this tutorial requires that you are running hello Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="6eb9b-112">Uruchom `az --version` toofind hello wersji.</span><span class="sxs-lookup"><span data-stu-id="6eb9b-112">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="6eb9b-113">Jeśli potrzebujesz tooinstall lub uaktualniania, zobacz [zainstalować Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="6eb9b-113">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="availability-set-overview"></a><span data-ttu-id="6eb9b-114">Omówienie zestawu dostępności</span><span class="sxs-lookup"><span data-stu-id="6eb9b-114">Availability set overview</span></span>

<span data-ttu-id="6eb9b-115">Zestawu dostępności jest funkcją logicznego grupowania, które można użyć w Azure tooensure hello zasobów maszyny Wirtualnej, który można umieścić w niej są odizolowane od siebie, gdy są wdrożone w centrum danych Azure.</span><span class="sxs-lookup"><span data-stu-id="6eb9b-115">An Availability Set is a logical grouping capability that you can use in Azure tooensure that hello VM resources you place within it are isolated from each other when they are deployed within an Azure datacenter.</span></span> <span data-ttu-id="6eb9b-116">Azure zapewnia, że hello maszyn wirtualnych zostanie umieszczony w obrębie zestawu dostępności uruchamiania na wielu serwerach fizycznych, obliczeniowe stojakami jednostek magazynowych i przełączniki sieciowe.</span><span class="sxs-lookup"><span data-stu-id="6eb9b-116">Azure ensures that hello VMs you place within an Availability Set run across multiple physical servers, compute racks, storage units, and network switches.</span></span> <span data-ttu-id="6eb9b-117">Dzięki temu w zdarzeniu hello sprzętu lub oprogramowania Azure awarii, jest ograniczona tylko podzestaw maszyn wirtualnych, a pozostanie się i kontynuować klientów dostępne tooyour toobe ogólną aplikacji.</span><span class="sxs-lookup"><span data-stu-id="6eb9b-117">This ensures that in hello event of a hardware or Azure software failure, only a subset of your VMs will be impacted, and your overall application will stay up and continue toobe available tooyour customers.</span></span> <span data-ttu-id="6eb9b-118">Przy użyciu zestawów dostępności jest tooleverage podstawowych możliwości, gdy trzeba toobuild niezawodne rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="6eb9b-118">Using Availability Sets is an essential capability tooleverage when you want toobuild reliable cloud solutions.</span></span>

<span data-ttu-id="6eb9b-119">Zastanówmy typowe rozwiązania oparte na Maszynach którym może mieć 4 serwery frontonu sieci web i korzystać z 2 maszyny wirtualne zaplecza, które hostują bazy danych.</span><span class="sxs-lookup"><span data-stu-id="6eb9b-119">Let’s consider a typical VM-based solution where you might have 4 front-end web servers and use 2 back-end VMs that host a database.</span></span> <span data-ttu-id="6eb9b-120">Przy użyciu platformy Azure, trzeba będzie toodefine dwa zestawy dostępności przed wdrożeniem maszyny wirtualne: zbiór jednej dostępności dla warstwy "web" hello i jeden zbiór dostępności dla warstwy "baza danych" hello.</span><span class="sxs-lookup"><span data-stu-id="6eb9b-120">With Azure, you’d want toodefine two availability sets before you deploy your VMs: one availability set for hello “web” tier and one availability set for hello “database” tier.</span></span> <span data-ttu-id="6eb9b-121">Podczas tworzenia nowej maszyny Wirtualnej można określić zestaw jako maszynę wirtualną az toohello parametr Utwórz polecenie, a Azure zostanie automatycznie upewnij się, że hello maszyny wirtualne utworzone w hello dostępne dostępności hello zestawu są izolowane między wieloma zasobami sprzętu fizycznego.</span><span class="sxs-lookup"><span data-stu-id="6eb9b-121">When you create a new VM you can then specify hello availability set as a parameter toohello az vm create command, and Azure will automatically ensure that hello VMs you create within hello available set are isolated across multiple physical hardware resources.</span></span> <span data-ttu-id="6eb9b-122">Oznacza to, że jeśli hello sprzętem fizycznym, który działa jeden z serwera sieci Web lub maszyn wirtualnych z serwera bazy danych na ma problem, wiesz, że hello inne wystąpienia serwera sieci Web i bazy danych w maszynach wirtualnych pozostanie uruchomione prawidłowo, ponieważ znajdują się na inny komputer.</span><span class="sxs-lookup"><span data-stu-id="6eb9b-122">This means that if hello physical hardware that one of your Web Server or Database Server VMs is running on has a problem, you know that hello other instances of your Web Server and Database VMs will remain running fine because they are on different hardware.</span></span>

<span data-ttu-id="6eb9b-123">Zawsze należy używać zestawów dostępności, jeśli chcesz toodeploy niezawodnej wirtualna rozwiązań opartych na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="6eb9b-123">You should always use Availability Sets when you want toodeploy reliable VM-based solutions within Azure.</span></span>


## <a name="create-an-availability-set"></a><span data-ttu-id="6eb9b-124">Tworzenie zestawu dostępności</span><span class="sxs-lookup"><span data-stu-id="6eb9b-124">Create an availability set</span></span>

<span data-ttu-id="6eb9b-125">Możesz utworzyć zestaw przy użyciu danych o dostępności [tworzenia maszyny wirtualnej az zestawu dostępności](/cli/azure/vm/availability-set#create).</span><span class="sxs-lookup"><span data-stu-id="6eb9b-125">You can create an availability set using [az vm availability-set create](/cli/azure/vm/availability-set#create).</span></span> <span data-ttu-id="6eb9b-126">W tym przykładzie ustawiliśmy na obu hello liczby domen aktualizacji i odporność na *2* dla zestawu o nazwie dostępności hello *myAvailabilitySet* w hello *myResourceGroupAvailability*grupy zasobów.</span><span class="sxs-lookup"><span data-stu-id="6eb9b-126">In this example, we set both hello number of update and fault domains at *2* for hello availability set named *myAvailabilitySet* in hello *myResourceGroupAvailability* resource group.</span></span>

<span data-ttu-id="6eb9b-127">Utwórz grupę zasobów.</span><span class="sxs-lookup"><span data-stu-id="6eb9b-127">Create a resource group.</span></span>

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

<span data-ttu-id="6eb9b-128">Zestawy dostępności pozwalają tooisolate zasobów między "domen błędów" i "Aktualizuj domeny".</span><span class="sxs-lookup"><span data-stu-id="6eb9b-128">Availability Sets allow you tooisolate resources across "fault domains" and "update domains".</span></span> <span data-ttu-id="6eb9b-129">A **domeny błędów** reprezentuje kolekcję izolowanego server + sieć i Magazyn zasobów.</span><span class="sxs-lookup"><span data-stu-id="6eb9b-129">A **fault domain** represents an isolated collection of server + network + storage resources.</span></span> <span data-ttu-id="6eb9b-130">W hello poprzedzających przykład możemy wskazać chcemy zestawu dostępności naszych toobe dystrybuowana do co najmniej dwóch domen błędów po naszej maszyny wirtualne są wdrażane.</span><span class="sxs-lookup"><span data-stu-id="6eb9b-130">In hello preceding example, we indicate that we want our availability set toobe distributed across at least two fault domains when our VMs are deployed.</span></span> <span data-ttu-id="6eb9b-131">Również wskazywać czy chcemy naszego zestawu rozproszonych w dwóch dostępności **zaktualizować domen**.</span><span class="sxs-lookup"><span data-stu-id="6eb9b-131">We also indicate that we want our availability set distributed across two **update domains**.</span></span>  <span data-ttu-id="6eb9b-132">Dwie domeny aktualizacji Sprawdź, czy gdy platforma Azure stosuje aktualizacje oprogramowania naszych zasobów maszyny Wirtualnej są izolowane uniemożliwia całe oprogramowanie hello systemem poniżej naszych maszyny Wirtualnej z aktualizacji na powitania tym samym czasie.</span><span class="sxs-lookup"><span data-stu-id="6eb9b-132">Two update domains ensure that when Azure performs software updates our VM resources are isolated, preventing all hello software running underneath our VM from being updated at hello same time.</span></span>

## <a name="configure-virtual-network"></a><span data-ttu-id="6eb9b-133">Konfigurowanie sieci wirtualnej</span><span class="sxs-lookup"><span data-stu-id="6eb9b-133">Configure virtual network</span></span>
<span data-ttu-id="6eb9b-134">Przed wdrożeniem niektórych maszyn wirtualnych i przetestować z usługi równoważenia, Utwórz hello obsługi zasobów sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="6eb9b-134">Before you deploy some VMs and can test your balancer, create hello supporting virtual network resources.</span></span> <span data-ttu-id="6eb9b-135">Aby uzyskać więcej informacji o sieciach wirtualnych, zobacz hello [Zarządzanie sieciami wirtualnymi Azure](tutorial-virtual-network.md) samouczka.</span><span class="sxs-lookup"><span data-stu-id="6eb9b-135">For more information about virtual networks, see hello [Manage Azure Virtual Networks](tutorial-virtual-network.md) tutorial.</span></span>

### <a name="create-network-resources"></a><span data-ttu-id="6eb9b-136">Utwórz zasoby sieciowe</span><span class="sxs-lookup"><span data-stu-id="6eb9b-136">Create network resources</span></span>
<span data-ttu-id="6eb9b-137">Tworzenie sieci wirtualnej z [tworzenie sieci wirtualnej sieci az](/cli/azure/network/vnet#create).</span><span class="sxs-lookup"><span data-stu-id="6eb9b-137">Create a virtual network with [az network vnet create](/cli/azure/network/vnet#create).</span></span> <span data-ttu-id="6eb9b-138">Witaj poniższy przykład tworzy sieć wirtualną o nazwie *myVnet* z podsiecią o nazwie *mySubnet*:</span><span class="sxs-lookup"><span data-stu-id="6eb9b-138">hello following example creates a virtual network named *myVnet* with a subnet named *mySubnet*:</span></span>

```azurecli-interactive 
az network vnet create \
    --resource-group myResourceGroupAvailability \
    --name myVnet \
    --subnet-name mySubnet
```
<span data-ttu-id="6eb9b-139">Wirtualne karty sieciowe są tworzone za pomocą [tworzenie kart interfejsu sieciowego az](/cli/azure/network/nic#create).</span><span class="sxs-lookup"><span data-stu-id="6eb9b-139">Virtual NICs are created with [az network nic create](/cli/azure/network/nic#create).</span></span> <span data-ttu-id="6eb9b-140">Witaj poniższy przykład tworzy trzy wirtualne karty sieciowe.</span><span class="sxs-lookup"><span data-stu-id="6eb9b-140">hello following example creates three virtual NICs.</span></span> <span data-ttu-id="6eb9b-141">(Jedną wirtualną kartę Sieciową dla każdej maszyny Wirtualnej można utworzyć dla aplikacji w hello następujące kroki).</span><span class="sxs-lookup"><span data-stu-id="6eb9b-141">(One virtual NIC for each VM you create for your app in hello following steps).</span></span> <span data-ttu-id="6eb9b-142">Można tworzyć dodatkowe wirtualne karty sieciowe i maszyn wirtualnych w dowolnym momencie i dodać je toohello usługi równoważenia obciążenia:</span><span class="sxs-lookup"><span data-stu-id="6eb9b-142">You can create additional virtual NICs and VMs at any time and add them toohello load balancer:</span></span>

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

## <a name="create-vms-inside-an-availability-set"></a><span data-ttu-id="6eb9b-143">Tworzenie maszyn wirtualnych w zestawie dostępności</span><span class="sxs-lookup"><span data-stu-id="6eb9b-143">Create VMs inside an availability set</span></span>

<span data-ttu-id="6eb9b-144">Maszyny wirtualne, musi zostać utworzony w toomake zestaw dostępności hello się, że poprawnie dystrybuowana ich hello sprzętu.</span><span class="sxs-lookup"><span data-stu-id="6eb9b-144">VMs must be created within hello availability set toomake sure they are correctly distributed across hello hardware.</span></span> <span data-ttu-id="6eb9b-145">Nie można dodać istniejącej maszyny Wirtualnej tooan zestaw danych o dostępności po jego utworzeniu.</span><span class="sxs-lookup"><span data-stu-id="6eb9b-145">You can't add an existing VM tooan availability set after it is created.</span></span> 

<span data-ttu-id="6eb9b-146">Po utworzeniu maszyny Wirtualnej przy użyciu [tworzenia maszyny wirtualnej az](/cli/azure/vm#create) Określ dostępności hello ustawić za pomocą hello `--availability-set` parametru toospecify hello nazwa zbioru dostępności hello.</span><span class="sxs-lookup"><span data-stu-id="6eb9b-146">When you create a VM using [az vm create](/cli/azure/vm#create) you specify hello availability set using hello `--availability-set` parameter toospecify hello name of hello availability set.</span></span>

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

<span data-ttu-id="6eb9b-147">Mamy teraz dwie maszyny wirtualne w naszym zestawie dostępności nowo utworzony.</span><span class="sxs-lookup"><span data-stu-id="6eb9b-147">We now have two virtual machines within our newly created availability set.</span></span> <span data-ttu-id="6eb9b-148">Ponieważ są one takie same hello zestawu dostępności Azure zapewnia tego hello maszyn wirtualnych i wszystkich ich zasobów (w tym dysków z danymi) są rozproszone na izolowanego sprzętu fizycznego.</span><span class="sxs-lookup"><span data-stu-id="6eb9b-148">Because they are in hello same availability set, Azure will ensure that hello VMs and all their resources (including data disks) are distributed across isolated physical hardware.</span></span> <span data-ttu-id="6eb9b-149">Tej dystrybucji zapewnia znacznie wyższą dostępność naszych ogólnego rozwiązania maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="6eb9b-149">This distribution helps ensure much higher availability of our overall VM solution.</span></span>

<span data-ttu-id="6eb9b-150">Jedyną operacją, której można napotkać podczas dodawania maszyn wirtualnych jest, że dla określonego rozmiaru maszyny Wirtualnej nie jest już dostępne toouse w zestawie dostępności.</span><span class="sxs-lookup"><span data-stu-id="6eb9b-150">One thing you may encounter as you add VMs is that a particular VM size is no longer available toouse within your availability set.</span></span> <span data-ttu-id="6eb9b-151">Ten problem może się zdarzyć, jeśli nie ma wystarczającej liczby tooadd pojemności, które przy zachowaniu zestawu dostępności hello zasady izolacji hello wymusza.</span><span class="sxs-lookup"><span data-stu-id="6eb9b-151">This issue can happen if there is no longer enough capacity tooadd it while preserving hello isolation rules hello availability set enforces.</span></span> <span data-ttu-id="6eb9b-152">Możesz sprawdzić toosee rozmiarów maszyn wirtualnych, które są dostępne toouse istniejących dostępność ustawić za pomocą hello `--availability-set list-sizes` parametru.</span><span class="sxs-lookup"><span data-stu-id="6eb9b-152">You can check toosee what VM sizes are available toouse within an existing availability set using hello `--availability-set list-sizes` parameter.</span></span>

## <a name="check-for-available-vm-sizes"></a><span data-ttu-id="6eb9b-153">Sprawdź, czy dostępne rozmiary maszyny Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="6eb9b-153">Check for available VM sizes</span></span> 

<span data-ttu-id="6eb9b-154">Możesz dodać więcej maszyn wirtualnych później zestaw dostępności toohello, ale trzeba się tooknow rozmiarów maszyn wirtualnych, które są dostępne na powitania sprzętu.</span><span class="sxs-lookup"><span data-stu-id="6eb9b-154">You can add more VMs toohello availability set later, but you need tooknow what VM sizes are available on hello hardware.</span></span> <span data-ttu-id="6eb9b-155">Użyj [az listy rozmiarów maszyn wirtualnych zestawu dostępności](/cli/azure/availability-set#list-sizes) toolist wszystkie dostępne rozmiary hello na powitania sprzętu klastra hello zestawu dostępności.</span><span class="sxs-lookup"><span data-stu-id="6eb9b-155">Use [az vm availability-set list-sizes](/cli/azure/availability-set#list-sizes) toolist all hello available sizes on hello hardware cluster for hello availability set.</span></span>

```azurecli-interactive 
az vm availability-set list-sizes \
     --resource-group myResourceGroupAvailability \
     --name myAvailabilitySet \
     --output table  
```

## <a name="next-steps"></a><span data-ttu-id="6eb9b-156">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="6eb9b-156">Next steps</span></span>

<span data-ttu-id="6eb9b-157">W niniejszym samouczku zawarto informacje na temat wykonywania następujących czynności:</span><span class="sxs-lookup"><span data-stu-id="6eb9b-157">In this tutorial, you learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="6eb9b-158">Tworzenie zestawu dostępności</span><span class="sxs-lookup"><span data-stu-id="6eb9b-158">Create an availability set</span></span>
> * <span data-ttu-id="6eb9b-159">Tworzenie maszyny Wirtualnej w zestawie dostępności</span><span class="sxs-lookup"><span data-stu-id="6eb9b-159">Create a VM in an availability set</span></span>
> * <span data-ttu-id="6eb9b-160">Sprawdź dostępne rozmiary maszyny Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="6eb9b-160">Check available VM sizes</span></span>

<span data-ttu-id="6eb9b-161">Przejdź dalej toolearn samouczka toohello o zestawy skalowania maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="6eb9b-161">Advance toohello next tutorial toolearn about virtual machine scale sets.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="6eb9b-162">Tworzenie zestawu skalowania maszyn wirtualnych</span><span class="sxs-lookup"><span data-stu-id="6eb9b-162">Create a VM scale set</span></span>](tutorial-create-vmss.md)

