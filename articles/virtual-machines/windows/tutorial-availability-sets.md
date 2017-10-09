---
title: aaaAvailability ustawia samouczek dla maszyn wirtualnych systemu Windows na platformie Azure | Dokumentacja firmy Microsoft
description: "Więcej informacji na temat hello dostępności zestawów dla maszyn wirtualnych systemu Windows na platformie Azure."
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
ms.openlocfilehash: 853775c5f126dd815c1933f9d71d2274a75ea661
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-availability-sets"></a><span data-ttu-id="012ba-103">Jak zestawy dostępności toouse</span><span class="sxs-lookup"><span data-stu-id="012ba-103">How toouse availability sets</span></span>

<span data-ttu-id="012ba-104">Z tego samouczka dowiesz się, jak tooincrease hello dostępność i niezawodność rozwiązań maszyny wirtualnej na platformie Azure przy użyciu funkcji o nazwie zestawów dostępności.</span><span class="sxs-lookup"><span data-stu-id="012ba-104">In this tutorial, you will learn how tooincrease hello availability and reliability of your Virtual Machine solutions on Azure using a capability called Availability Sets.</span></span> <span data-ttu-id="012ba-105">Zestawy dostępności upewnij się, tym powitalne wdrażanie na platformie Azure maszyny wirtualne rozproszone na wielu klastrów izolowanego sprzętu.</span><span class="sxs-lookup"><span data-stu-id="012ba-105">Availability sets ensure that hello VMs you deploy on Azure are distributed across multiple isolated hardware clusters.</span></span> <span data-ttu-id="012ba-106">W ten sposób zapewnia, że jeśli awarii sprzętu lub oprogramowania w systemie Azure wykonywany, jest ograniczona tylko do podzbioru maszyny wirtualne i które rozwiązania ogólną pozostanie dostępny i działa z punktu widzenia hello klientów przy użyciu go.</span><span class="sxs-lookup"><span data-stu-id="012ba-106">Doing this ensures that if a hardware or software failure within Azure happens, only a sub-set of your VMs will be impacted and that your overall solution will remain available and operational from hello perspective of your customers using it.</span></span> 

<span data-ttu-id="012ba-107">Ten samouczek zawiera informacje na temat wykonywania następujących czynności:</span><span class="sxs-lookup"><span data-stu-id="012ba-107">In this tutorial, you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="012ba-108">Tworzenie zestawu dostępności</span><span class="sxs-lookup"><span data-stu-id="012ba-108">Create an availability set</span></span>
> * <span data-ttu-id="012ba-109">Tworzenie maszyny Wirtualnej w zestawie dostępności</span><span class="sxs-lookup"><span data-stu-id="012ba-109">Create a VM in an availability set</span></span>
> * <span data-ttu-id="012ba-110">Sprawdź dostępne rozmiary maszyny Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="012ba-110">Check available VM sizes</span></span>

<span data-ttu-id="012ba-111">Ten samouczek wymaga hello Azure PowerShell w wersji modułu 3,6 lub nowszej.</span><span class="sxs-lookup"><span data-stu-id="012ba-111">This tutorial requires hello Azure PowerShell module version 3.6 or later.</span></span> <span data-ttu-id="012ba-112">Uruchom ` Get-Module -ListAvailable AzureRM` toofind hello wersji.</span><span class="sxs-lookup"><span data-stu-id="012ba-112">Run ` Get-Module -ListAvailable AzureRM` toofind hello version.</span></span> <span data-ttu-id="012ba-113">Jeśli potrzebujesz tooupgrade, zobacz [modułu instalacji programu Azure PowerShell](/powershell/azure/install-azurerm-ps).</span><span class="sxs-lookup"><span data-stu-id="012ba-113">If you need tooupgrade, see [Install Azure PowerShell module](/powershell/azure/install-azurerm-ps).</span></span>

## <a name="availability-set-overview"></a><span data-ttu-id="012ba-114">Omówienie zestawu dostępności</span><span class="sxs-lookup"><span data-stu-id="012ba-114">Availability set overview</span></span>

<span data-ttu-id="012ba-115">Zestawu dostępności jest funkcją logicznego grupowania, które można użyć w Azure tooensure hello zasobów maszyny Wirtualnej, który można umieścić w niej są odizolowane od siebie, gdy są wdrożone w centrum danych Azure.</span><span class="sxs-lookup"><span data-stu-id="012ba-115">An Availability Set is a logical grouping capability that you can use in Azure tooensure that hello VM resources you place within it are isolated from each other when they are deployed within an Azure datacenter.</span></span> <span data-ttu-id="012ba-116">Azure zapewnia, że hello maszyn wirtualnych zostanie umieszczony w obrębie zestawu dostępności uruchamiania na wielu serwerach fizycznych, obliczeniowe stojakami jednostek magazynowych i przełączniki sieciowe.</span><span class="sxs-lookup"><span data-stu-id="012ba-116">Azure ensures that hello VMs you place within an Availability Set run across multiple physical servers, compute racks, storage units, and network switches.</span></span> <span data-ttu-id="012ba-117">Dzięki temu w zdarzeniu hello sprzętu lub oprogramowania Azure awarii, jest ograniczona tylko podzestaw maszyn wirtualnych, a pozostanie się i kontynuować klientów dostępne tooyour toobe ogólną aplikacji.</span><span class="sxs-lookup"><span data-stu-id="012ba-117">This ensures that in hello event of a hardware or Azure software failure, only a subset of your VMs will be impacted, and your overall application will stay up and continue toobe available tooyour customers.</span></span> <span data-ttu-id="012ba-118">Przy użyciu zestawów dostępności jest tooleverage podstawowych możliwości, gdy trzeba toobuild niezawodne rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="012ba-118">Using Availability Sets is an essential capability tooleverage when you want toobuild reliable cloud solutions.</span></span>

<span data-ttu-id="012ba-119">Zastanówmy typowe rozwiązania oparte na Maszynach którym może mieć 4 serwery frontonu sieci web i korzystać z 2 maszyny wirtualne zaplecza, które hostują bazy danych.</span><span class="sxs-lookup"><span data-stu-id="012ba-119">Let’s consider a typical VM-based solution where you might have 4 front-end web servers and use 2 back-end VMs that host a database.</span></span> <span data-ttu-id="012ba-120">Przy użyciu platformy Azure, trzeba będzie toodefine dwa zestawy dostępności przed wdrożeniem maszyny wirtualne: zbiór jednej dostępności dla warstwy "web" hello i jeden zbiór dostępności dla warstwy "baza danych" hello.</span><span class="sxs-lookup"><span data-stu-id="012ba-120">With Azure, you’d want toodefine two availability sets before you deploy your VMs: one availability set for hello “web” tier and one availability set for hello “database” tier.</span></span> <span data-ttu-id="012ba-121">Podczas tworzenia nowej maszyny Wirtualnej można określić zestaw jako maszynę wirtualną az toohello parametr Utwórz polecenie, a Azure zostanie automatycznie upewnij się, że hello maszyny wirtualne utworzone w hello dostępne dostępności hello zestawu są izolowane między wieloma zasobami sprzętu fizycznego.</span><span class="sxs-lookup"><span data-stu-id="012ba-121">When you create a new VM you can then specify hello availability set as a parameter toohello az vm create command, and Azure will automatically ensure that hello VMs you create within hello available set are isolated across multiple physical hardware resources.</span></span> <span data-ttu-id="012ba-122">Oznacza to, że jeśli hello sprzętem fizycznym, który działa jeden z serwera sieci Web lub maszyn wirtualnych z serwera bazy danych na ma problem, wiesz, że hello inne wystąpienia serwera sieci Web i bazy danych w maszynach wirtualnych pozostanie uruchomione prawidłowo, ponieważ znajdują się na inny komputer.</span><span class="sxs-lookup"><span data-stu-id="012ba-122">This means that if hello physical hardware that one of your Web Server or Database Server VMs is running on has a problem, you know that hello other instances of your Web Server and Database VMs will remain running fine because they are on different hardware.</span></span>

<span data-ttu-id="012ba-123">Zawsze należy używać zestawów dostępności, jeśli chcesz toodeploy niezawodne rozwiązania na podstawie maszyny Wirtualnej w obrębie platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="012ba-123">You should always use Availability Sets when you want toodeploy reliable VM based solutions within Azure.</span></span>

## <a name="create-an-availability-set"></a><span data-ttu-id="012ba-124">Tworzenie zestawu dostępności</span><span class="sxs-lookup"><span data-stu-id="012ba-124">Create an availability set</span></span>

<span data-ttu-id="012ba-125">Możesz utworzyć zestaw przy użyciu danych o dostępności [AzureRmAvailabilitySet nowy](/powershell/module/azurerm.compute/new-azurermavailabilityset).</span><span class="sxs-lookup"><span data-stu-id="012ba-125">You can create an availability set using [New-AzureRmAvailabilitySet](/powershell/module/azurerm.compute/new-azurermavailabilityset).</span></span> <span data-ttu-id="012ba-126">W tym przykładzie ustawiliśmy na obu hello liczby domen aktualizacji i odporność na *2* dla zestawu o nazwie dostępności hello *myAvailabilitySet* w hello *myResourceGroupAvailability*grupy zasobów.</span><span class="sxs-lookup"><span data-stu-id="012ba-126">In this example, we set both hello number of update and fault domains at *2* for hello availability set named *myAvailabilitySet* in hello *myResourceGroupAvailability* resource group.</span></span>

<span data-ttu-id="012ba-127">Utwórz grupę zasobów.</span><span class="sxs-lookup"><span data-stu-id="012ba-127">Create a resource group.</span></span>

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

## <a name="create-vms-inside-an-availability-set"></a><span data-ttu-id="012ba-128">Tworzenie maszyn wirtualnych w zestawie dostępności</span><span class="sxs-lookup"><span data-stu-id="012ba-128">Create VMs inside an availability set</span></span>

<span data-ttu-id="012ba-129">Maszyny wirtualne muszą toobe utworzone w ramach toomake zestaw dostępności hello się, że poprawnie dystrybuowana ich hello sprzętu.</span><span class="sxs-lookup"><span data-stu-id="012ba-129">VMs need toobe created within hello availability set toomake sure they are correctly distributed across hello hardware.</span></span> <span data-ttu-id="012ba-130">Nie można dodać istniejącej maszyny Wirtualnej tooan zestaw danych o dostępności po jego utworzeniu.</span><span class="sxs-lookup"><span data-stu-id="012ba-130">You can't add an existing VM tooan availability set after it is created.</span></span> 

<span data-ttu-id="012ba-131">sprzętu Hello w lokalizacji jest podzielony na domeny aktualizacji toomultiple i domen błędów.</span><span class="sxs-lookup"><span data-stu-id="012ba-131">hello hardware in a location is divided in toomultiple update domains and fault domains.</span></span> <span data-ttu-id="012ba-132">**Domeny aktualizacji** grupy maszyn wirtualnych i podstawowym sprzętem fizycznym, który może zostać przeprowadzony ponowny rozruch w hello jest tym samym czasie.</span><span class="sxs-lookup"><span data-stu-id="012ba-132">An **update domain** is a group of VMs and underlying physical hardware that can be rebooted at hello same time.</span></span> <span data-ttu-id="012ba-133">Maszyny wirtualne w hello sam **domeny błędów** udostępnianie typowych magazynu, a także wspólnego przełącznik źródła i sieci zasilania.</span><span class="sxs-lookup"><span data-stu-id="012ba-133">VMs in hello same **fault domain** share common storage as well as a common power source and network switch.</span></span> 

<span data-ttu-id="012ba-134">Po utworzeniu maszyny Wirtualnej przy użyciu konfiguracji przy użyciu [AzureRMVMConfig nowy](/powershell/module/azurerm.compute/new-azurermvmconfig) Określ dostępności hello ustawić za pomocą hello `-AvailabilitySetId` identyfikator hello toospecify parametru hello zestawu dostępności.</span><span class="sxs-lookup"><span data-stu-id="012ba-134">When you create a VM using configuration using [New-AzureRMVMConfig](/powershell/module/azurerm.compute/new-azurermvmconfig) you specify hello availability set using hello `-AvailabilitySetId` parameter toospecify hello ID of hello availability set.</span></span>

<span data-ttu-id="012ba-135">Tworzenie 2 maszyn wirtualnych z [AzureRmVM nowy](/powershell/module/azurerm.compute/new-azurermvm) w zestawie dostępności hello.</span><span class="sxs-lookup"><span data-stu-id="012ba-135">Create 2 VMs with [New-AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm) in hello availability set.</span></span>

```powershell
$availabilitySet = Get-AzureRmAvailabilitySet `
    -ResourceGroupName myResourceGroupAvailability `
    -Name myAvailabilitySet

$cred = Get-Credential -Message "Enter a username and password for hello virtual machine."

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

   # Here is where we specify hello availability set
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

<span data-ttu-id="012ba-136">Go zajmuje kilka minut toocreate i skonfiguruj obie maszyny wirtualne.</span><span class="sxs-lookup"><span data-stu-id="012ba-136">It takes a few minutes toocreate and configure both VMs.</span></span> <span data-ttu-id="012ba-137">Po zakończeniu będziesz mieć 2 maszyny wirtualne rozproszone na powitania podstawowy sprzęt.</span><span class="sxs-lookup"><span data-stu-id="012ba-137">When finished, you will have 2 virtual machines distributed across hello underlying hardware.</span></span> 

## <a name="check-for-available-vm-sizes"></a><span data-ttu-id="012ba-138">Sprawdź, czy dostępne rozmiary maszyny Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="012ba-138">Check for available VM sizes</span></span> 

<span data-ttu-id="012ba-139">Możesz dodać więcej maszyn wirtualnych później zestaw dostępności toohello, ale trzeba się tooknow rozmiarów maszyn wirtualnych, które są dostępne na powitania sprzętu.</span><span class="sxs-lookup"><span data-stu-id="012ba-139">You can add more VMs toohello availability set later, but you need tooknow what VM sizes are available on hello hardware.</span></span> <span data-ttu-id="012ba-140">Użyj [Get-AzureRMVMSize](/powershell/module/azurerm.compute/get-azurermvmsize) toolist wszystkie dostępne rozmiary hello na powitania sprzętu klastra hello zestawu dostępności.</span><span class="sxs-lookup"><span data-stu-id="012ba-140">Use [Get-AzureRMVMSize](/powershell/module/azurerm.compute/get-azurermvmsize) toolist all hello available sizes on hello hardware cluster for hello availability set.</span></span>

```powershell
Get-AzureRmVMSize `
   -AvailabilitySetName myAvailabilitySet `
   -ResourceGroupName myResourceGroupAvailability  
```

## <a name="next-steps"></a><span data-ttu-id="012ba-141">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="012ba-141">Next steps</span></span>

<span data-ttu-id="012ba-142">W niniejszym samouczku zawarto informacje na temat wykonywania następujących czynności:</span><span class="sxs-lookup"><span data-stu-id="012ba-142">In this tutorial, you learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="012ba-143">Tworzenie zestawu dostępności</span><span class="sxs-lookup"><span data-stu-id="012ba-143">Create an availability set</span></span>
> * <span data-ttu-id="012ba-144">Tworzenie maszyny Wirtualnej w zestawie dostępności</span><span class="sxs-lookup"><span data-stu-id="012ba-144">Create a VM in an availability set</span></span>
> * <span data-ttu-id="012ba-145">Sprawdź dostępne rozmiary maszyny Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="012ba-145">Check available VM sizes</span></span>

<span data-ttu-id="012ba-146">Przejdź dalej toolearn samouczka toohello o zestawy skalowania maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="012ba-146">Advance toohello next tutorial toolearn about virtual machine scale sets.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="012ba-147">Tworzenie zestawu skalowania maszyn wirtualnych</span><span class="sxs-lookup"><span data-stu-id="012ba-147">Create a VM scale set</span></span>](tutorial-create-vmss.md)


