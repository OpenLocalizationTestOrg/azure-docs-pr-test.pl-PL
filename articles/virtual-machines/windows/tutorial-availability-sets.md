---
title: "Samouczek zestawy dostępności dla maszyn wirtualnych systemu Windows na platformie Azure | Dokumentacja firmy Microsoft"
description: "Informacje na temat zestawów dostępności dla maszyn wirtualnych systemu Windows na platformie Azure."
documentationcenter: 
services: virtual-machines-windows
author: cynthn
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 05/08/2017
ms.author: cynthn
ms.custom: mvc
ms.openlocfilehash: d918362106ef93cf47620e0018d363cd510884b0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-use-availability-sets"></a><span data-ttu-id="439d7-103">Jak używać zestawów dostępności</span><span class="sxs-lookup"><span data-stu-id="439d7-103">How to use availability sets</span></span>

<span data-ttu-id="439d7-104">Z tego samouczka dowiesz się, jak zwiększyć dostępność i niezawodność rozwiązań maszyny wirtualnej na platformie Azure przy użyciu funkcji o nazwie zestawów dostępności.</span><span class="sxs-lookup"><span data-stu-id="439d7-104">In this tutorial, you will learn how to increase the availability and reliability of your Virtual Machine solutions on Azure using a capability called Availability Sets.</span></span> <span data-ttu-id="439d7-105">Zestawy dostępności upewnij się, czy maszyn wirtualnych, należy wdrożyć na platformie Azure są rozproszone na wielu klastrów izolowanego sprzętu.</span><span class="sxs-lookup"><span data-stu-id="439d7-105">Availability sets ensure that the VMs you deploy on Azure are distributed across multiple isolated hardware clusters.</span></span> <span data-ttu-id="439d7-106">W ten sposób zapewnia, że jeśli awarii sprzętu lub oprogramowania w systemie Azure wykonywany, jest ograniczona tylko do podzbioru maszyny wirtualne i które rozwiązania ogólną pozostanie dostępny i działa z perspektywy klientów przy użyciu go.</span><span class="sxs-lookup"><span data-stu-id="439d7-106">Doing this ensures that if a hardware or software failure within Azure happens, only a sub-set of your VMs will be impacted and that your overall solution will remain available and operational from the perspective of your customers using it.</span></span> 

<span data-ttu-id="439d7-107">Ten samouczek zawiera informacje na temat wykonywania następujących czynności:</span><span class="sxs-lookup"><span data-stu-id="439d7-107">In this tutorial, you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="439d7-108">Tworzenie zestawu dostępności</span><span class="sxs-lookup"><span data-stu-id="439d7-108">Create an availability set</span></span>
> * <span data-ttu-id="439d7-109">Tworzenie maszyny Wirtualnej w zestawie dostępności</span><span class="sxs-lookup"><span data-stu-id="439d7-109">Create a VM in an availability set</span></span>
> * <span data-ttu-id="439d7-110">Sprawdź dostępne rozmiary maszyny Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="439d7-110">Check available VM sizes</span></span>

<span data-ttu-id="439d7-111">Dla tego samouczka jest wymagany moduł Azure PowerShell w wersji 3.6 lub nowszej.</span><span class="sxs-lookup"><span data-stu-id="439d7-111">This tutorial requires the Azure PowerShell module version 3.6 or later.</span></span> <span data-ttu-id="439d7-112">Uruchom polecenie ` Get-Module -ListAvailable AzureRM`, aby dowiedzieć się, jaka wersja jest używana.</span><span class="sxs-lookup"><span data-stu-id="439d7-112">Run ` Get-Module -ListAvailable AzureRM` to find the version.</span></span> <span data-ttu-id="439d7-113">Jeśli potrzebujesz do uaktualnienia, zobacz [modułu instalacji programu Azure PowerShell](/powershell/azure/install-azurerm-ps).</span><span class="sxs-lookup"><span data-stu-id="439d7-113">If you need to upgrade, see [Install Azure PowerShell module](/powershell/azure/install-azurerm-ps).</span></span>

## <a name="availability-set-overview"></a><span data-ttu-id="439d7-114">Omówienie zestawu dostępności</span><span class="sxs-lookup"><span data-stu-id="439d7-114">Availability set overview</span></span>

<span data-ttu-id="439d7-115">Zestawu dostępności jest możliwość grupę logiczną, która na platformie Azure umożliwia Sprawdź, czy zasobów maszyny Wirtualnej, który można umieścić w nim są odizolowane od siebie, gdy są wdrożone w centrum danych Azure.</span><span class="sxs-lookup"><span data-stu-id="439d7-115">An Availability Set is a logical grouping capability that you can use in Azure to ensure that the VM resources you place within it are isolated from each other when they are deployed within an Azure datacenter.</span></span> <span data-ttu-id="439d7-116">Azure zapewnia, że maszyny wirtualne, umieść w ramach zestawu dostępności uruchamiania na wielu serwerach fizycznych, obliczeniowe stojakami jednostek magazynowych i przełączniki sieciowe.</span><span class="sxs-lookup"><span data-stu-id="439d7-116">Azure ensures that the VMs you place within an Availability Set run across multiple physical servers, compute racks, storage units, and network switches.</span></span> <span data-ttu-id="439d7-117">Dzięki temu w przypadku awarii sprzętu lub oprogramowania Azure awarii, jest ograniczona tylko podzestaw maszyn wirtualnych, a aplikacja ogólna pozostanie w górę i nadal dostępne dla klientów.</span><span class="sxs-lookup"><span data-stu-id="439d7-117">This ensures that in the event of a hardware or Azure software failure, only a subset of your VMs will be impacted, and your overall application will stay up and continue to be available to your customers.</span></span> <span data-ttu-id="439d7-118">Przy użyciu zestawów dostępności jest podstawowych możliwości wykorzystać umożliwia tworzenia rozwiązań chmur wiarygodne.</span><span class="sxs-lookup"><span data-stu-id="439d7-118">Using Availability Sets is an essential capability to leverage when you want to build reliable cloud solutions.</span></span>

<span data-ttu-id="439d7-119">Zastanówmy typowe rozwiązania oparte na Maszynach którym może mieć 4 serwery frontonu sieci web i korzystać z 2 maszyny wirtualne zaplecza, które hostują bazy danych.</span><span class="sxs-lookup"><span data-stu-id="439d7-119">Let’s consider a typical VM-based solution where you might have 4 front-end web servers and use 2 back-end VMs that host a database.</span></span> <span data-ttu-id="439d7-120">Przy użyciu platformy Azure, należy zdefiniować dwa zestawy dostępności, przed wdrożeniem maszyn wirtualnych: jeden zbiór dostępności dla warstwy "web" i jeden zbiór dostępności dla warstwy "baza danych".</span><span class="sxs-lookup"><span data-stu-id="439d7-120">With Azure, you’d want to define two availability sets before you deploy your VMs: one availability set for the “web” tier and one availability set for the “database” tier.</span></span> <span data-ttu-id="439d7-121">Podczas tworzenia nowej maszyny Wirtualnej można określić zestaw dostępności jako parametr do maszyny wirtualnej az utworzyć polecenie, a Azure zostanie automatycznie upewnij się, że maszyny wirtualne utworzone w zestawie dostępne są izolowane między wieloma zasobami sprzętu fizycznego.</span><span class="sxs-lookup"><span data-stu-id="439d7-121">When you create a new VM you can then specify the availability set as a parameter to the az vm create command, and Azure will automatically ensure that the VMs you create within the available set are isolated across multiple physical hardware resources.</span></span> <span data-ttu-id="439d7-122">Oznacza to, że jeśli sprzęt fizyczny wykorzystywany do jednego serwera sieci Web lub maszyn wirtualnych z serwera bazy danych jest uruchomiona na ma problem, wiesz, że inne wystąpienia serwera sieci Web i bazy danych w maszynach wirtualnych pozostaną uruchomione prawidłowo ponieważ są one na inny komputer.</span><span class="sxs-lookup"><span data-stu-id="439d7-122">This means that if the physical hardware that one of your Web Server or Database Server VMs is running on has a problem, you know that the other instances of your Web Server and Database VMs will remain running fine because they are on different hardware.</span></span>

<span data-ttu-id="439d7-123">Zawsze należy używać zestawów dostępności, jeśli chcesz wdrożyć niezawodne rozwiązania na podstawie maszyny Wirtualnej w obrębie platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="439d7-123">You should always use Availability Sets when you want to deploy reliable VM based solutions within Azure.</span></span>

## <a name="create-an-availability-set"></a><span data-ttu-id="439d7-124">Tworzenie zestawu dostępności</span><span class="sxs-lookup"><span data-stu-id="439d7-124">Create an availability set</span></span>

<span data-ttu-id="439d7-125">Możesz utworzyć zestaw przy użyciu danych o dostępności [AzureRmAvailabilitySet nowy](/powershell/module/azurerm.compute/new-azurermavailabilityset).</span><span class="sxs-lookup"><span data-stu-id="439d7-125">You can create an availability set using [New-AzureRmAvailabilitySet](/powershell/module/azurerm.compute/new-azurermavailabilityset).</span></span> <span data-ttu-id="439d7-126">W tym przykładzie umieszczania liczba domen aktualizacji i odporność na *2* dla zestawu o nazwie dostępności *myAvailabilitySet* w *myResourceGroupAvailability* grupy zasobów.</span><span class="sxs-lookup"><span data-stu-id="439d7-126">In this example, we set both the number of update and fault domains at *2* for the availability set named *myAvailabilitySet* in the *myResourceGroupAvailability* resource group.</span></span>

<span data-ttu-id="439d7-127">Utwórz grupę zasobów.</span><span class="sxs-lookup"><span data-stu-id="439d7-127">Create a resource group.</span></span>

```powershell
New-AzureRmResourceGroup -Name myResourceGroupAvailability -Location EastUS
```


```powershell
New-AzureRmAvailabilitySet `
   -Location EastUS `
   -Name myAvailabilitySet `
   -ResourceGroupName myResourceGroupAvailability `
   -Managed `
   -PlatformFaultDomainCount 2 `
   -PlatformUpdateDomainCount 2
```

## <a name="create-vms-inside-an-availability-set"></a><span data-ttu-id="439d7-128">Tworzenie maszyn wirtualnych w zestawie dostępności</span><span class="sxs-lookup"><span data-stu-id="439d7-128">Create VMs inside an availability set</span></span>

<span data-ttu-id="439d7-129">Maszyny wirtualne muszą można utworzyć dostępność ustawioną upewnij się, że są one poprawnie dystrybuowana sprzętu.</span><span class="sxs-lookup"><span data-stu-id="439d7-129">VMs need to be created within the availability set to make sure they are correctly distributed across the hardware.</span></span> <span data-ttu-id="439d7-130">Nie można dodać istniejącej maszyny Wirtualnej do dostępności po jego utworzeniu.</span><span class="sxs-lookup"><span data-stu-id="439d7-130">You can't add an existing VM to an availability set after it is created.</span></span> 

<span data-ttu-id="439d7-131">Sprzęt w lokalizacji jest podzielony na wiele domen aktualizacji i domen błędów.</span><span class="sxs-lookup"><span data-stu-id="439d7-131">The hardware in a location is divided in to multiple update domains and fault domains.</span></span> <span data-ttu-id="439d7-132">**Domeny aktualizacji** jest grupą maszyn wirtualnych i podstawowym sprzętem fizycznym, który może zostać uruchomiony ponownie w tym samym czasie.</span><span class="sxs-lookup"><span data-stu-id="439d7-132">An **update domain** is a group of VMs and underlying physical hardware that can be rebooted at the same time.</span></span> <span data-ttu-id="439d7-133">Maszyny wirtualne w tej samej **domeny błędów** udostępnianie typowych magazynu, a także wspólnego przełącznik źródła i sieci zasilania.</span><span class="sxs-lookup"><span data-stu-id="439d7-133">VMs in the same **fault domain** share common storage as well as a common power source and network switch.</span></span> 

<span data-ttu-id="439d7-134">Po utworzeniu maszyny Wirtualnej przy użyciu konfiguracji przy użyciu [AzureRMVMConfig nowy](/powershell/module/azurerm.compute/new-azurermvmconfig) określ zestaw, za pomocą dostępności `-AvailabilitySetId` parametr, aby określić identyfikator zestawu dostępności.</span><span class="sxs-lookup"><span data-stu-id="439d7-134">When you create a VM using configuration using [New-AzureRMVMConfig](/powershell/module/azurerm.compute/new-azurermvmconfig) you specify the availability set using the `-AvailabilitySetId` parameter to specify the ID of the availability set.</span></span>

<span data-ttu-id="439d7-135">Tworzenie 2 maszyn wirtualnych z [AzureRmVM nowy](/powershell/module/azurerm.compute/new-azurermvm) w zestawie dostępności.</span><span class="sxs-lookup"><span data-stu-id="439d7-135">Create 2 VMs with [New-AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm) in the availability set.</span></span>

```powershell
$availabilitySet = Get-AzureRmAvailabilitySet `
    -ResourceGroupName myResourceGroupAvailability `
    -Name myAvailabilitySet

$cred = Get-Credential -Message "Enter a username and password for the virtual machine."

$subnetConfig = New-AzureRmVirtualNetworkSubnetConfig `
    -Name mySubnet `
    -AddressPrefix 192.168.1.0/24
$vnet = New-AzureRmVirtualNetwork `
    -ResourceGroupName myResourceGroupAvailability `
    -Location EastUS `
    -Name MYvNET `
    -AddressPrefix 192.168.0.0/16 `
    -Subnet $subnetConfig

for ($i=1; $i -le 2; $i++)
{
   $pip = New-AzureRmPublicIpAddress `
        -ResourceGroupName myResourceGroupAvailability `
        -Location EastUS `
        -Name "mypublicdns$(Get-Random)" `
        -AllocationMethod Static `
        -IdleTimeoutInMinutes 4

   $nsgRuleRDP = New-AzureRmNetworkSecurityRuleConfig `
        -Name myNetworkSecurityGroupRuleRDP$i `
        -Protocol Tcp `
        -Direction Inbound `
        -Priority 1000 `
        -SourceAddressPrefix * `
        -SourcePortRange * `
        -DestinationAddressPrefix * `
        -DestinationPortRange 3389 `
        -Access Allow

   $nsg = New-AzureRmNetworkSecurityGroup `
        -ResourceGroupName myResourceGroupAvailability `
        -Location EastUS `
        -Name myNetworkSecurityGroup$i `
        -SecurityRules $nsgRuleRDP

   $nic = New-AzureRmNetworkInterface `
        -Name myNic$i `
        -ResourceGroupName myResourceGroupAvailability `
        -Location EastUS `
        -SubnetId $vnet.Subnets[0].Id `
        -PublicIpAddressId $pip.Id `
        -NetworkSecurityGroupId $nsg.Id

   # Here is where we specify the availability set
   $vm = New-AzureRmVMConfig `
        -VMName myVM$i `
        -VMSize Standard_D1 `
        -AvailabilitySetId $availabilitySet.Id

   $vm = Set-AzureRmVMOperatingSystem `
        -VM $vm `
        -Windows -ComputerName myVM$i `   
        -Credential $cred `
        -ProvisionVMAgent `
        -EnableAutoUpdate
   $vm = Set-AzureRmVMSourceImage `
        -VM $vm `
        -PublisherName MicrosoftWindowsServer `
        -Offer WindowsServer `
        -Skus 2016-Datacenter `
        -Version latest
   $vm = Set-AzureRmVMOSDisk `
        -VM $vm `
        -Name myOsDisk$i `
        -DiskSizeInGB 128 `
        -CreateOption FromImage `
        -Caching ReadWrite
   $vm = Add-AzureRmVMNetworkInterface -VM $vm -Id $nic.Id
   New-AzureRmVM `
        -ResourceGroupName myResourceGroupAvailability `
        -Location EastUS `
        -VM $vm
}

```

<span data-ttu-id="439d7-136">Trwa kilka minut, aby utworzyć i skonfigurować obie maszyny wirtualne.</span><span class="sxs-lookup"><span data-stu-id="439d7-136">It takes a few minutes to create and configure both VMs.</span></span> <span data-ttu-id="439d7-137">Po zakończeniu będziesz mieć 2 maszyny wirtualne rozproszone na używanego sprzętu.</span><span class="sxs-lookup"><span data-stu-id="439d7-137">When finished, you will have 2 virtual machines distributed across the underlying hardware.</span></span> 

## <a name="check-for-available-vm-sizes"></a><span data-ttu-id="439d7-138">Sprawdź, czy dostępne rozmiary maszyny Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="439d7-138">Check for available VM sizes</span></span> 

<span data-ttu-id="439d7-139">Możesz dodać więcej maszyn wirtualnych do później zestaw dostępności, ale musisz wiedzieć, jaki rozmiarów maszyn wirtualnych są dostępne na sprzęcie.</span><span class="sxs-lookup"><span data-stu-id="439d7-139">You can add more VMs to the availability set later, but you need to know what VM sizes are available on the hardware.</span></span> <span data-ttu-id="439d7-140">Użyj [Get AzureRMVMSize](/powershell/module/azurerm.compute/get-azurermvmsize) Aby wyświetlić listę wszystkich dostępnych rozmiarów na sprzęcie klastra dla zestawu dostępności.</span><span class="sxs-lookup"><span data-stu-id="439d7-140">Use [Get-AzureRMVMSize](/powershell/module/azurerm.compute/get-azurermvmsize) to list all the available sizes on the hardware cluster for the availability set.</span></span>

```powershell
Get-AzureRmVMSize `
   -AvailabilitySetName myAvailabilitySet `
   -ResourceGroupName myResourceGroupAvailability  
```

## <a name="next-steps"></a><span data-ttu-id="439d7-141">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="439d7-141">Next steps</span></span>

<span data-ttu-id="439d7-142">W niniejszym samouczku zawarto informacje na temat wykonywania następujących czynności:</span><span class="sxs-lookup"><span data-stu-id="439d7-142">In this tutorial, you learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="439d7-143">Tworzenie zestawu dostępności</span><span class="sxs-lookup"><span data-stu-id="439d7-143">Create an availability set</span></span>
> * <span data-ttu-id="439d7-144">Tworzenie maszyny Wirtualnej w zestawie dostępności</span><span class="sxs-lookup"><span data-stu-id="439d7-144">Create a VM in an availability set</span></span>
> * <span data-ttu-id="439d7-145">Sprawdź dostępne rozmiary maszyny Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="439d7-145">Check available VM sizes</span></span>

<span data-ttu-id="439d7-146">Przejdź do następnego samouczkiem, aby poznać zestawy skalowania maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="439d7-146">Advance to the next tutorial to learn about virtual machine scale sets.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="439d7-147">Tworzenie zestawu skalowania maszyn wirtualnych</span><span class="sxs-lookup"><span data-stu-id="439d7-147">Create a VM scale set</span></span>](tutorial-create-vmss.md)


