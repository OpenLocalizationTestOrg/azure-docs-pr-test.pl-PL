---
title: "Tworzenie niestandardowych obrazów maszyn wirtualnych przy użyciu programu Azure PowerShell | Dokumentacja firmy Microsoft"
description: "Samouczek — Tworzenie niestandardowego obrazu maszyny Wirtualnej przy użyciu programu Azure PowerShell."
services: virtual-machines-windows
documentationcenter: virtual-machines
author: cynthn
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 05/08/2017
ms.author: cynthn
ms.custom: mvc
ms.openlocfilehash: 96be2872a902a7d7063bf1dff7b4ca209a5b67c1
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-custom-image-of-an-azure-vm-using-powershell"></a><span data-ttu-id="72ba9-103">Tworzenie niestandardowego obrazu maszyny Wirtualnej platformy Azure przy użyciu programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="72ba9-103">Create a custom image of an Azure VM using PowerShell</span></span>

<span data-ttu-id="72ba9-104">Niestandardowe obrazy są takie jak obrazy marketplace, ale można je utworzyć samodzielnie.</span><span class="sxs-lookup"><span data-stu-id="72ba9-104">Custom images are like marketplace images, but you create them yourself.</span></span> <span data-ttu-id="72ba9-105">Niestandardowe obrazy może służyć do ładowania początkowego konfiguracje, takie jak wstępnego ładowania aplikacji, konfiguracji aplikacji i inne konfiguracje systemu operacyjnego.</span><span class="sxs-lookup"><span data-stu-id="72ba9-105">Custom images can be used to bootstrap configurations such as preloading applications, application configurations, and other OS configurations.</span></span> <span data-ttu-id="72ba9-106">W tym samouczku utworzysz własnego niestandardowego obrazu maszyny wirtualnej platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="72ba9-106">In this tutorial, you create your own custom image of an Azure virtual machine.</span></span> <span data-ttu-id="72ba9-107">Omawiane kwestie:</span><span class="sxs-lookup"><span data-stu-id="72ba9-107">You learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="72ba9-108">Narzędzie Sysprep i generalize maszyny wirtualne</span><span class="sxs-lookup"><span data-stu-id="72ba9-108">Sysprep and generalize VMs</span></span>
> * <span data-ttu-id="72ba9-109">Tworzenie obrazu niestandardowego</span><span class="sxs-lookup"><span data-stu-id="72ba9-109">Create a custom image</span></span>
> * <span data-ttu-id="72ba9-110">Utwórz maszynę Wirtualną z obrazu niestandardowego</span><span class="sxs-lookup"><span data-stu-id="72ba9-110">Create a VM from a custom image</span></span>
> * <span data-ttu-id="72ba9-111">Wyświetlanie listy wszystkich obrazów w ramach subskrypcji</span><span class="sxs-lookup"><span data-stu-id="72ba9-111">List all the images in your subscription</span></span>
> * <span data-ttu-id="72ba9-112">Usuń obraz</span><span class="sxs-lookup"><span data-stu-id="72ba9-112">Delete an image</span></span>

<span data-ttu-id="72ba9-113">Dla tego samouczka jest wymagany moduł Azure PowerShell w wersji 3.6 lub nowszej.</span><span class="sxs-lookup"><span data-stu-id="72ba9-113">This tutorial requires the Azure PowerShell module version 3.6 or later.</span></span> <span data-ttu-id="72ba9-114">Uruchom polecenie ` Get-Module -ListAvailable AzureRM`, aby dowiedzieć się, jaka wersja jest używana.</span><span class="sxs-lookup"><span data-stu-id="72ba9-114">Run ` Get-Module -ListAvailable AzureRM` to find the version.</span></span> <span data-ttu-id="72ba9-115">Jeśli potrzebujesz do uaktualnienia, zobacz [modułu instalacji programu Azure PowerShell](/powershell/azure/install-azurerm-ps).</span><span class="sxs-lookup"><span data-stu-id="72ba9-115">If you need to upgrade, see [Install Azure PowerShell module](/powershell/azure/install-azurerm-ps).</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="72ba9-116">Przed rozpoczęciem</span><span class="sxs-lookup"><span data-stu-id="72ba9-116">Before you begin</span></span>

<span data-ttu-id="72ba9-117">Poniższe kroki szczegółowo sposób pobrać istniejącej maszyny Wirtualnej i przekształcić ją do ponownego użycia niestandardowego obrazu używanego do utworzenia nowego wystąpienia maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="72ba9-117">The steps below detail how to take an existing VM and turn it into a re-usable custom image that you can use to create new VM instances.</span></span>

<span data-ttu-id="72ba9-118">Aby ukończyć przykład, w tym samouczku, musi mieć istniejącej maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="72ba9-118">To complete the example in this tutorial, you must have an existing virtual machine.</span></span> <span data-ttu-id="72ba9-119">Jeśli to konieczne, to [przykładowym skrypcie](../scripts/virtual-machines-windows-powershell-sample-create-vm.md) można utworzyć.</span><span class="sxs-lookup"><span data-stu-id="72ba9-119">If needed, this [script sample](../scripts/virtual-machines-windows-powershell-sample-create-vm.md) can create one for you.</span></span> <span data-ttu-id="72ba9-120">Podczas pracy nad samouczek, Zastąp maszyny Wirtualnej i grupy zasobów nazwy w razie potrzeby.</span><span class="sxs-lookup"><span data-stu-id="72ba9-120">When working through the tutorial, replace the resource group and VM names where needed.</span></span>

## <a name="prepare-vm"></a><span data-ttu-id="72ba9-121">Przygotowywanie maszyny Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="72ba9-121">Prepare VM</span></span>

<span data-ttu-id="72ba9-122">Aby utworzyć obraz maszyny wirtualnej, należy przygotować maszyny Wirtualnej uogólnianie maszyny Wirtualnej, dealokowanie, a następnie oznaczenie źródłowej maszyny Wirtualnej, ponieważ uogólniony na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="72ba9-122">To create an image of a virtual machine, you need to prepare the VM by generalizing the VM, deallocating, and then marking the source VM as generalized in Azure.</span></span>

### <a name="generalize-the-windows-vm-using-sysprep"></a><span data-ttu-id="72ba9-123">Maszyny Wirtualnej systemu Windows za pomocą programu Sysprep do uogólnienia</span><span class="sxs-lookup"><span data-stu-id="72ba9-123">Generalize the Windows VM using Sysprep</span></span>

<span data-ttu-id="72ba9-124">Program Sysprep usuwa wszystkie informacje osobiste konto, między innymi i przygotowuje komputer do użycia jako obraz.</span><span class="sxs-lookup"><span data-stu-id="72ba9-124">Sysprep removes all your personal account information, among other things, and prepares the machine to be used as an image.</span></span> <span data-ttu-id="72ba9-125">Aby uzyskać więcej informacji o narzędziu Sysprep, zobacz [sposobu użycia programu Sysprep: wprowadzenie](http://technet.microsoft.com/library/bb457073.aspx).</span><span class="sxs-lookup"><span data-stu-id="72ba9-125">For details about Sysprep, see [How to Use Sysprep: An Introduction](http://technet.microsoft.com/library/bb457073.aspx).</span></span>


1. <span data-ttu-id="72ba9-126">Połączenie z maszyną wirtualną.</span><span class="sxs-lookup"><span data-stu-id="72ba9-126">Connect to the virtual machine.</span></span>
2. <span data-ttu-id="72ba9-127">Otwórz okno Wiersz polecenia jako administrator.</span><span class="sxs-lookup"><span data-stu-id="72ba9-127">Open the Command Prompt window as an administrator.</span></span> <span data-ttu-id="72ba9-128">Zmień katalog na *%windir%\system32\sysprep*, a następnie uruchom *sysprep.exe*.</span><span class="sxs-lookup"><span data-stu-id="72ba9-128">Change the directory to *%windir%\system32\sysprep*, and then run *sysprep.exe*.</span></span>
3. <span data-ttu-id="72ba9-129">W **narzędzie przygotowania systemu** okno dialogowe, wybierz opcję *wprowadź systemu Out-of-Box Experience (OOBE)*i upewnij się, że *Generalize* pole wyboru jest zaznaczone.</span><span class="sxs-lookup"><span data-stu-id="72ba9-129">In the **System Preparation Tool** dialog box, select *Enter System Out-of-Box Experience (OOBE)*, and make sure that the *Generalize* check box is selected.</span></span>
4. <span data-ttu-id="72ba9-130">W **opcje zamykania**, wybierz pozycję *zamknięcia* , a następnie kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="72ba9-130">In **Shutdown Options**, select *Shutdown* and then click **OK**.</span></span>
5. <span data-ttu-id="72ba9-131">Po zakończeniu działania programu Sysprep, zamyka maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="72ba9-131">When Sysprep completes, it shuts down the virtual machine.</span></span> <span data-ttu-id="72ba9-132">**Nie uruchamiaj ponownie maszynę Wirtualną**.</span><span class="sxs-lookup"><span data-stu-id="72ba9-132">**Do not restart the VM**.</span></span>

### <a name="deallocate-and-mark-the-vm-as-generalized"></a><span data-ttu-id="72ba9-133">Cofnięcie przydziału i zostać oznaczone jako uogólniona maszyna wirtualna</span><span class="sxs-lookup"><span data-stu-id="72ba9-133">Deallocate and mark the VM as generalized</span></span>

<span data-ttu-id="72ba9-134">Aby utworzyć obraz, maszyna wirtualna musi być alokację oraz oznaczony jako uogólniony na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="72ba9-134">To create an image, the VM needs to be deallocated and marked as generalized in Azure.</span></span>

<span data-ttu-id="72ba9-135">Cofnięcie przydziału maszynę Wirtualną przy użyciu [Stop-AzureRmVM](/powershell/module/azurerm.compute/stop-azurermvm).</span><span class="sxs-lookup"><span data-stu-id="72ba9-135">Deallocated the VM using [Stop-AzureRmVM](/powershell/module/azurerm.compute/stop-azurermvm).</span></span>

```powershell
Stop-AzureRmVM -ResourceGroupName myResourceGroupImages -Name myVM -Force
```

<span data-ttu-id="72ba9-136">Ustaw stan maszyny wirtualnej na `-Generalized` przy użyciu [AzureRmVm zestawu](/powershell/module/azurerm.compute/set-azurermvm).</span><span class="sxs-lookup"><span data-stu-id="72ba9-136">Set the status of the virtual machine to `-Generalized` using [Set-AzureRmVm](/powershell/module/azurerm.compute/set-azurermvm).</span></span> 
   
```powershell
Set-AzureRmVM -ResourceGroupName myResourceGroupImages -Name myVM -Generalized
```


## <a name="create-the-image"></a><span data-ttu-id="72ba9-137">Tworzenie obrazu</span><span class="sxs-lookup"><span data-stu-id="72ba9-137">Create the image</span></span>

<span data-ttu-id="72ba9-138">Teraz można utworzyć obrazu maszyny wirtualnej za pomocą [AzureRmImageConfig nowy](/powershell/module/azurerm.compute/new-azurermimageconfig) i [AzureRmImage nowy](/powershell/module/azurerm.compute/new-azurermimage).</span><span class="sxs-lookup"><span data-stu-id="72ba9-138">Now you can create an image of the VM by using [New-AzureRmImageConfig](/powershell/module/azurerm.compute/new-azurermimageconfig) and [New-AzureRmImage](/powershell/module/azurerm.compute/new-azurermimage).</span></span> <span data-ttu-id="72ba9-139">Poniższy przykład tworzy obraz o nazwie *myImage* z maszyny Wirtualnej o nazwie *myVM*.</span><span class="sxs-lookup"><span data-stu-id="72ba9-139">The following example creates an image named *myImage* from a VM named *myVM*.</span></span>

<span data-ttu-id="72ba9-140">Przełącz maszynę wirtualną.</span><span class="sxs-lookup"><span data-stu-id="72ba9-140">Get the virtual machine.</span></span> 

```powershell
$vm = Get-AzureRmVM -Name myVM -ResourceGroupName myResourceGroupImages
```

<span data-ttu-id="72ba9-141">Utwórz konfigurację obrazu.</span><span class="sxs-lookup"><span data-stu-id="72ba9-141">Create the image configuration.</span></span>

```powershell
$image = New-AzureRmImageConfig -Location EastUS -SourceVirtualMachineId $vm.ID 
```

<span data-ttu-id="72ba9-142">Tworzenie obrazu.</span><span class="sxs-lookup"><span data-stu-id="72ba9-142">Create the image.</span></span>

```powershell
New-AzureRmImage -Image $image -ImageName myImage -ResourceGroupName myResourceGroupImages
``` 

 
## <a name="create-vms-from-the-image"></a><span data-ttu-id="72ba9-143">Tworzenie maszyn wirtualnych z obrazu</span><span class="sxs-lookup"><span data-stu-id="72ba9-143">Create VMs from the image</span></span>

<span data-ttu-id="72ba9-144">Teraz, gdy masz obrazu można utworzyć jeden lub więcej nowych maszyn wirtualnych z obrazu.</span><span class="sxs-lookup"><span data-stu-id="72ba9-144">Now that you have an image, you can create one or more new VMs from the image.</span></span> <span data-ttu-id="72ba9-145">Tworzenie maszyny Wirtualnej z obrazu niestandardowego jest bardzo podobny do tworzenia maszyny Wirtualnej przy użyciu obrazu z witryny Marketplace.</span><span class="sxs-lookup"><span data-stu-id="72ba9-145">Creating a VM from a custom image is very similar to creating a VM using a Marketplace image.</span></span> <span data-ttu-id="72ba9-146">Korzystając z obrazu z witryny Marketplace, trzeba informacji na temat obrazów, dostawcy obrazu, oferty, jednostki SKU i wersji.</span><span class="sxs-lookup"><span data-stu-id="72ba9-146">When you use a Marketplace image, you have to information about the image, image provider, offer, SKU and version.</span></span> <span data-ttu-id="72ba9-147">Z niestandardowego obrazu wystarczy podać identyfikator zasobu obrazu niestandardowego.</span><span class="sxs-lookup"><span data-stu-id="72ba9-147">With a custom image, you just need to provide the ID of the custom image resource.</span></span> 

<span data-ttu-id="72ba9-148">W poniższym skrypcie, możemy utworzyć zmienną *$image* do przechowywania informacji na temat używania niestandardowego obrazu [Get-AzureRmImage](/powershell/module/azurerm.compute/get-azurermimage) , a następnie używamy [AzureRmVMSourceImage zestaw](/powershell/module/azurerm.compute/set-azurermvmsourceimage) i określić za pomocą Identyfikatora *$image* zmiennej właśnie utworzyliśmy.</span><span class="sxs-lookup"><span data-stu-id="72ba9-148">In the following script, we create a variable *$image* to store information about the custom image using [Get-AzureRmImage](/powershell/module/azurerm.compute/get-azurermimage) and then we use [Set-AzureRmVMSourceImage](/powershell/module/azurerm.compute/set-azurermvmsourceimage) and specify the ID using the *$image* variable we just created.</span></span> 

<span data-ttu-id="72ba9-149">Skrypt tworzy Maszynę wirtualną o nazwie *myVMfromImage* z naszych obraz niestandardowy w nowej grupy zasobów o nazwie *myResourceGroupFromImage* w *zachodnie stany USA* lokalizacji.</span><span class="sxs-lookup"><span data-stu-id="72ba9-149">The script creates a VM named *myVMfromImage* from our custom image in a new resource group named *myResourceGroupFromImage* in the *West US* location.</span></span>


```powershell
$cred = Get-Credential -Message "Enter a username and password for the virtual machine."

New-AzureRmResourceGroup -Name myResourceGroupFromImage -Location EastUS

$subnetConfig = New-AzureRmVirtualNetworkSubnetConfig `
    -Name mySubnet `
    -AddressPrefix 192.168.1.0/24

$vnet = New-AzureRmVirtualNetwork `
    -ResourceGroupName myResourceGroupFromImage `
    -Location EastUS `
    -Name MYvNET `
    -AddressPrefix 192.168.0.0/16 `
    -Subnet $subnetConfig

$pip = New-AzureRmPublicIpAddress `
    -ResourceGroupName myResourceGroupFromImage `
    -Location EastUS `
    -Name "mypublicdns$(Get-Random)" `
    -AllocationMethod Static `
    -IdleTimeoutInMinutes 4

  $nsgRuleRDP = New-AzureRmNetworkSecurityRuleConfig `
    -Name myNetworkSecurityGroupRuleRDP `
    -Protocol Tcp `
    -Direction Inbound `
    -Priority 1000 `
    -SourceAddressPrefix * `
    -SourcePortRange * `
    -DestinationAddressPrefix * `
    -DestinationPortRange 3389 `
    -Access Allow

  $nsg = New-AzureRmNetworkSecurityGroup `
    -ResourceGroupName myResourceGroupFromImage `
    -Location EastUS `
    -Name myNetworkSecurityGroup `
    -SecurityRules $nsgRuleRDP

$nic = New-AzureRmNetworkInterface `
    -Name myNic `
    -ResourceGroupName myResourceGroupFromImage `
    -Location EastUS `
    -SubnetId $vnet.Subnets[0].Id `
    -PublicIpAddressId $pip.Id `
    -NetworkSecurityGroupId $nsg.Id

$vmConfig = New-AzureRmVMConfig `
    -VMName myVMfromImage `
    -VMSize Standard_D1 | Set-AzureRmVMOperatingSystem -Windows `
        -ComputerName myComputer `
        -Credential $cred 

# Here is where we create a variable to store information about the image 
$image = Get-AzureRmImage `
    -ImageName myImage `
    -ResourceGroupName myResourceGroupImages

# Here is where we specify that we want to create the VM from and image and provide the image ID
$vmConfig = Set-AzureRmVMSourceImage -VM $vmConfig -Id $image.Id

$vmConfig = Add-AzureRmVMNetworkInterface -VM $vmConfig -Id $nic.Id

New-AzureRmVM `
    -ResourceGroupName myResourceGroupFromImage `
    -Location EastUS `
    -VM $vmConfig
```

## <a name="image-management"></a><span data-ttu-id="72ba9-150">Zarządzanie obrazami</span><span class="sxs-lookup"><span data-stu-id="72ba9-150">Image management</span></span> 

<span data-ttu-id="72ba9-151">Oto kilka przykładów typowych zadań zarządzania dla obrazu i sposobu ich ukończenia przy użyciu programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="72ba9-151">Here are some examples of common management image tasks and how to complete them using PowerShell.</span></span>

<span data-ttu-id="72ba9-152">Wyświetl listę wszystkich obrazów według nazwy.</span><span class="sxs-lookup"><span data-stu-id="72ba9-152">List all images by name.</span></span>

```powershell
$images = Find-AzureRMResource -ResourceType Microsoft.Compute/images 
$images.name
```

<span data-ttu-id="72ba9-153">Usuń obraz.</span><span class="sxs-lookup"><span data-stu-id="72ba9-153">Delete an image.</span></span> <span data-ttu-id="72ba9-154">W tym przykładzie usuwa obraz o nazwie *myOldImage* z *myResourceGroup*.</span><span class="sxs-lookup"><span data-stu-id="72ba9-154">This example deletes the image named *myOldImage* from the *myResourceGroup*.</span></span>

```powershell
Remove-AzureRmImage `
    -ImageName myOldImage `
    -ResourceGroupName myResourceGroup
```

## <a name="next-steps"></a><span data-ttu-id="72ba9-155">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="72ba9-155">Next steps</span></span>

<span data-ttu-id="72ba9-156">W tym samouczku utworzony niestandardowy obraz maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="72ba9-156">In this tutorial, you created a custom VM image.</span></span> <span data-ttu-id="72ba9-157">Możesz przedstawiono sposób do:</span><span class="sxs-lookup"><span data-stu-id="72ba9-157">You learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="72ba9-158">Narzędzie Sysprep i generalize maszyny wirtualne</span><span class="sxs-lookup"><span data-stu-id="72ba9-158">Sysprep and generalize VMs</span></span>
> * <span data-ttu-id="72ba9-159">Tworzenie obrazu niestandardowego</span><span class="sxs-lookup"><span data-stu-id="72ba9-159">Create a custom image</span></span>
> * <span data-ttu-id="72ba9-160">Utwórz maszynę Wirtualną z obrazu niestandardowego</span><span class="sxs-lookup"><span data-stu-id="72ba9-160">Create a VM from a custom image</span></span>
> * <span data-ttu-id="72ba9-161">Wyświetlanie listy wszystkich obrazów w ramach subskrypcji</span><span class="sxs-lookup"><span data-stu-id="72ba9-161">List all the images in your subscription</span></span>
> * <span data-ttu-id="72ba9-162">Usuń obraz</span><span class="sxs-lookup"><span data-stu-id="72ba9-162">Delete an image</span></span>

<span data-ttu-id="72ba9-163">Przejdź do następnego samouczkiem, aby poznać sposób wysokiej dostępności maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="72ba9-163">Advance to the next tutorial to learn about how highly available virtual machines.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="72ba9-164">Tworzenie maszyn wirtualnych o wysokiej dostępności</span><span class="sxs-lookup"><span data-stu-id="72ba9-164">Create highly available VMs</span></span>](tutorial-availability-sets.md)



