---
title: "aaaCreate niestandardowych obrazów maszyn wirtualnych z hello Azure PowerShell | Dokumentacja firmy Microsoft"
description: "Samouczek — Tworzenie niestandardowego obrazu maszyny Wirtualnej przy użyciu hello Azure PowerShell."
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
ms.openlocfilehash: 3a759fe1b7e7b72f531399b0f4a99e341713c6a4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-custom-image-of-an-azure-vm-using-powershell"></a><span data-ttu-id="adcd2-103">Tworzenie niestandardowego obrazu maszyny Wirtualnej platformy Azure przy użyciu programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="adcd2-103">Create a custom image of an Azure VM using PowerShell</span></span>

<span data-ttu-id="adcd2-104">Niestandardowe obrazy są takie jak obrazy marketplace, ale można je utworzyć samodzielnie.</span><span class="sxs-lookup"><span data-stu-id="adcd2-104">Custom images are like marketplace images, but you create them yourself.</span></span> <span data-ttu-id="adcd2-105">Niestandardowe obrazy mogą być używane toobootstrap konfiguracje, takie jak wstępnego ładowania aplikacji, konfiguracji aplikacji i inne konfiguracje systemu operacyjnego.</span><span class="sxs-lookup"><span data-stu-id="adcd2-105">Custom images can be used toobootstrap configurations such as preloading applications, application configurations, and other OS configurations.</span></span> <span data-ttu-id="adcd2-106">W tym samouczku utworzysz własnego niestandardowego obrazu maszyny wirtualnej platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="adcd2-106">In this tutorial, you create your own custom image of an Azure virtual machine.</span></span> <span data-ttu-id="adcd2-107">Omawiane kwestie:</span><span class="sxs-lookup"><span data-stu-id="adcd2-107">You learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="adcd2-108">Narzędzie Sysprep i generalize maszyny wirtualne</span><span class="sxs-lookup"><span data-stu-id="adcd2-108">Sysprep and generalize VMs</span></span>
> * <span data-ttu-id="adcd2-109">Tworzenie obrazu niestandardowego</span><span class="sxs-lookup"><span data-stu-id="adcd2-109">Create a custom image</span></span>
> * <span data-ttu-id="adcd2-110">Utwórz maszynę Wirtualną z obrazu niestandardowego</span><span class="sxs-lookup"><span data-stu-id="adcd2-110">Create a VM from a custom image</span></span>
> * <span data-ttu-id="adcd2-111">Wyświetlanie listy wszystkich obrazów hello w ramach subskrypcji</span><span class="sxs-lookup"><span data-stu-id="adcd2-111">List all hello images in your subscription</span></span>
> * <span data-ttu-id="adcd2-112">Usuń obraz</span><span class="sxs-lookup"><span data-stu-id="adcd2-112">Delete an image</span></span>

<span data-ttu-id="adcd2-113">Ten samouczek wymaga hello Azure PowerShell w wersji modułu 3,6 lub nowszej.</span><span class="sxs-lookup"><span data-stu-id="adcd2-113">This tutorial requires hello Azure PowerShell module version 3.6 or later.</span></span> <span data-ttu-id="adcd2-114">Uruchom ` Get-Module -ListAvailable AzureRM` toofind hello wersji.</span><span class="sxs-lookup"><span data-stu-id="adcd2-114">Run ` Get-Module -ListAvailable AzureRM` toofind hello version.</span></span> <span data-ttu-id="adcd2-115">Jeśli potrzebujesz tooupgrade, zobacz [modułu instalacji programu Azure PowerShell](/powershell/azure/install-azurerm-ps).</span><span class="sxs-lookup"><span data-stu-id="adcd2-115">If you need tooupgrade, see [Install Azure PowerShell module](/powershell/azure/install-azurerm-ps).</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="adcd2-116">Przed rozpoczęciem</span><span class="sxs-lookup"><span data-stu-id="adcd2-116">Before you begin</span></span>

<span data-ttu-id="adcd2-117">Poniższe kroki Hello szczegółowo tootake istniejącej maszyny Wirtualnej i włącz go do wielokrotnego użytku niestandardowego obrazu, który służy toocreate nowych wystąpień maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="adcd2-117">hello steps below detail how tootake an existing VM and turn it into a re-usable custom image that you can use toocreate new VM instances.</span></span>

<span data-ttu-id="adcd2-118">przykład Witaj toocomplete w tym samouczku, musi mieć istniejącej maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="adcd2-118">toocomplete hello example in this tutorial, you must have an existing virtual machine.</span></span> <span data-ttu-id="adcd2-119">Jeśli to konieczne, to [przykładowym skrypcie](../scripts/virtual-machines-windows-powershell-sample-create-vm.md) można utworzyć.</span><span class="sxs-lookup"><span data-stu-id="adcd2-119">If needed, this [script sample](../scripts/virtual-machines-windows-powershell-sample-create-vm.md) can create one for you.</span></span> <span data-ttu-id="adcd2-120">Podczas pracy nad hello samouczek, Zastąp maszyny Wirtualnej i grupy zasobów hello nazwy w razie potrzeby.</span><span class="sxs-lookup"><span data-stu-id="adcd2-120">When working through hello tutorial, replace hello resource group and VM names where needed.</span></span>

## <a name="prepare-vm"></a><span data-ttu-id="adcd2-121">Przygotowywanie maszyny Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="adcd2-121">Prepare VM</span></span>

<span data-ttu-id="adcd2-122">toocreate obrazu maszyny wirtualnej, należy tooprepare hello maszyny Wirtualnej przez uogólnianie hello maszyny Wirtualnej, dealokowanie, a następnie oznaczenie hello źródłowej maszyny Wirtualnej, ponieważ uogólniony na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="adcd2-122">toocreate an image of a virtual machine, you need tooprepare hello VM by generalizing hello VM, deallocating, and then marking hello source VM as generalized in Azure.</span></span>

### <a name="generalize-hello-windows-vm-using-sysprep"></a><span data-ttu-id="adcd2-123">Generalize hello maszyny Wirtualnej systemu Windows za pomocą programu Sysprep</span><span class="sxs-lookup"><span data-stu-id="adcd2-123">Generalize hello Windows VM using Sysprep</span></span>

<span data-ttu-id="adcd2-124">Program Sysprep usuwa wszystkie informacje osobiste konto, między innymi i przygotowuje toobe maszyny hello użyty jako obraz.</span><span class="sxs-lookup"><span data-stu-id="adcd2-124">Sysprep removes all your personal account information, among other things, and prepares hello machine toobe used as an image.</span></span> <span data-ttu-id="adcd2-125">Aby uzyskać więcej informacji o narzędziu Sysprep, zobacz [jak tooUse Sysprep: wprowadzenie](http://technet.microsoft.com/library/bb457073.aspx).</span><span class="sxs-lookup"><span data-stu-id="adcd2-125">For details about Sysprep, see [How tooUse Sysprep: An Introduction](http://technet.microsoft.com/library/bb457073.aspx).</span></span>


1. <span data-ttu-id="adcd2-126">Połącz toohello maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="adcd2-126">Connect toohello virtual machine.</span></span>
2. <span data-ttu-id="adcd2-127">Otwórz okno wiersza polecenia hello jako administrator.</span><span class="sxs-lookup"><span data-stu-id="adcd2-127">Open hello Command Prompt window as an administrator.</span></span> <span data-ttu-id="adcd2-128">Zmień katalog hello zbyt*%windir%\system32\sysprep*, a następnie uruchom *sysprep.exe*.</span><span class="sxs-lookup"><span data-stu-id="adcd2-128">Change hello directory too*%windir%\system32\sysprep*, and then run *sysprep.exe*.</span></span>
3. <span data-ttu-id="adcd2-129">W hello **narzędzie przygotowania systemu** okno dialogowe, wybierz opcję *wprowadź systemu Out-of-Box Experience (OOBE)*i upewnij się, że hello *Generalize* pole wyboru jest zaznaczone.</span><span class="sxs-lookup"><span data-stu-id="adcd2-129">In hello **System Preparation Tool** dialog box, select *Enter System Out-of-Box Experience (OOBE)*, and make sure that hello *Generalize* check box is selected.</span></span>
4. <span data-ttu-id="adcd2-130">W **opcje zamykania**, wybierz pozycję *zamknięcia* , a następnie kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="adcd2-130">In **Shutdown Options**, select *Shutdown* and then click **OK**.</span></span>
5. <span data-ttu-id="adcd2-131">Po zakończeniu działania programu Sysprep, zamyka hello maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="adcd2-131">When Sysprep completes, it shuts down hello virtual machine.</span></span> <span data-ttu-id="adcd2-132">**Nie uruchamiaj ponownie hello wirtualna**.</span><span class="sxs-lookup"><span data-stu-id="adcd2-132">**Do not restart hello VM**.</span></span>

### <a name="deallocate-and-mark-hello-vm-as-generalized"></a><span data-ttu-id="adcd2-133">Cofnięcie przydziału i oznacz hello maszyny Wirtualnej, ponieważ uogólniony</span><span class="sxs-lookup"><span data-stu-id="adcd2-133">Deallocate and mark hello VM as generalized</span></span>

<span data-ttu-id="adcd2-134">toocreate obraz powitania maszyny Wirtualnej musi toobe alokację i oznaczone jako uogólniony na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="adcd2-134">toocreate an image, hello VM needs toobe deallocated and marked as generalized in Azure.</span></span>

<span data-ttu-id="adcd2-135">Deallocated hello maszynę Wirtualną przy użyciu [Stop-AzureRmVM](/powershell/module/azurerm.compute/stop-azurermvm).</span><span class="sxs-lookup"><span data-stu-id="adcd2-135">Deallocated hello VM using [Stop-AzureRmVM](/powershell/module/azurerm.compute/stop-azurermvm).</span></span>

```powershell
Stop-AzureRmVM -ResourceGroupName myResourceGroupImages -Name myVM -Force
```

<span data-ttu-id="adcd2-136">Ustaw stan hello hello maszyny wirtualnej za`-Generalized` przy użyciu [AzureRmVm zestawu](/powershell/module/azurerm.compute/set-azurermvm).</span><span class="sxs-lookup"><span data-stu-id="adcd2-136">Set hello status of hello virtual machine too`-Generalized` using [Set-AzureRmVm](/powershell/module/azurerm.compute/set-azurermvm).</span></span> 
   
```powershell
Set-AzureRmVM -ResourceGroupName myResourceGroupImages -Name myVM -Generalized
```


## <a name="create-hello-image"></a><span data-ttu-id="adcd2-137">Utworzyć obraz powitania</span><span class="sxs-lookup"><span data-stu-id="adcd2-137">Create hello image</span></span>

<span data-ttu-id="adcd2-138">Teraz można utworzyć obraz powitania maszyny Wirtualnej za pomocą [AzureRmImageConfig nowy](/powershell/module/azurerm.compute/new-azurermimageconfig) i [AzureRmImage nowy](/powershell/module/azurerm.compute/new-azurermimage).</span><span class="sxs-lookup"><span data-stu-id="adcd2-138">Now you can create an image of hello VM by using [New-AzureRmImageConfig](/powershell/module/azurerm.compute/new-azurermimageconfig) and [New-AzureRmImage](/powershell/module/azurerm.compute/new-azurermimage).</span></span> <span data-ttu-id="adcd2-139">Witaj poniższy przykład tworzy obraz o nazwie *myImage* z maszyny Wirtualnej o nazwie *myVM*.</span><span class="sxs-lookup"><span data-stu-id="adcd2-139">hello following example creates an image named *myImage* from a VM named *myVM*.</span></span>

<span data-ttu-id="adcd2-140">Pobierz hello maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="adcd2-140">Get hello virtual machine.</span></span> 

```powershell
$vm = Get-AzureRmVM -Name myVM -ResourceGroupName myResourceGroupImages
```

<span data-ttu-id="adcd2-141">Utwórz konfigurację obraz powitania.</span><span class="sxs-lookup"><span data-stu-id="adcd2-141">Create hello image configuration.</span></span>

```powershell
$image = New-AzureRmImageConfig -Location EastUS -SourceVirtualMachineId $vm.ID 
```

<span data-ttu-id="adcd2-142">Utwórz obraz powitania.</span><span class="sxs-lookup"><span data-stu-id="adcd2-142">Create hello image.</span></span>

```powershell
New-AzureRmImage -Image $image -ImageName myImage -ResourceGroupName myResourceGroupImages
``` 

 
## <a name="create-vms-from-hello-image"></a><span data-ttu-id="adcd2-143">Tworzenie maszyn wirtualnych z hello obrazu</span><span class="sxs-lookup"><span data-stu-id="adcd2-143">Create VMs from hello image</span></span>

<span data-ttu-id="adcd2-144">Teraz, gdy masz obrazu można utworzyć jeden lub więcej nowych maszyn wirtualnych z hello obrazu.</span><span class="sxs-lookup"><span data-stu-id="adcd2-144">Now that you have an image, you can create one or more new VMs from hello image.</span></span> <span data-ttu-id="adcd2-145">Tworzenie maszyny Wirtualnej z obrazu niestandardowego jest bardzo podobne toocreating Maszynę wirtualną przy użyciu obrazu z witryny Marketplace.</span><span class="sxs-lookup"><span data-stu-id="adcd2-145">Creating a VM from a custom image is very similar toocreating a VM using a Marketplace image.</span></span> <span data-ttu-id="adcd2-146">Korzystając z obrazu z witryny Marketplace, masz tooinformation o obraz powitania, dostawca obrazu, oferty, jednostki SKU i wersji.</span><span class="sxs-lookup"><span data-stu-id="adcd2-146">When you use a Marketplace image, you have tooinformation about hello image, image provider, offer, SKU and version.</span></span> <span data-ttu-id="adcd2-147">Z niestandardowego obrazu wystarczy tooprovide hello identyfikator zasobu obrazu niestandardowego hello.</span><span class="sxs-lookup"><span data-stu-id="adcd2-147">With a custom image, you just need tooprovide hello ID of hello custom image resource.</span></span> 

<span data-ttu-id="adcd2-148">W hello następującego skryptu, możemy utworzyć zmienną *$image* toostore informacji o korzystaniu z hello niestandardowego obrazu [Get-AzureRmImage](/powershell/module/azurerm.compute/get-azurermimage) , a następnie używamy [Set-AzureRmVMSourceImage](/powershell/module/azurerm.compute/set-azurermvmsourceimage)i podaj identyfikator hello przy użyciu hello *$image* zmiennej właśnie utworzyliśmy.</span><span class="sxs-lookup"><span data-stu-id="adcd2-148">In hello following script, we create a variable *$image* toostore information about hello custom image using [Get-AzureRmImage](/powershell/module/azurerm.compute/get-azurermimage) and then we use [Set-AzureRmVMSourceImage](/powershell/module/azurerm.compute/set-azurermvmsourceimage) and specify hello ID using hello *$image* variable we just created.</span></span> 

<span data-ttu-id="adcd2-149">Witaj skrypt tworzy Maszynę wirtualną o nazwie *myVMfromImage* z naszych obraz niestandardowy w nowej grupy zasobów o nazwie *myResourceGroupFromImage* w hello *zachodnie stany USA* lokalizacji.</span><span class="sxs-lookup"><span data-stu-id="adcd2-149">hello script creates a VM named *myVMfromImage* from our custom image in a new resource group named *myResourceGroupFromImage* in hello *West US* location.</span></span>


```powershell
$cred = Get-Credential -Message "Enter a username and password for hello virtual machine."

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

# Here is where we create a variable toostore information about hello image 
$image = Get-AzureRmImage `
    -ImageName myImage `
    -ResourceGroupName myResourceGroupImages

# Here is where we specify that we want toocreate hello VM from and image and provide hello image ID
$vmConfig = Set-AzureRmVMSourceImage -VM $vmConfig -Id $image.Id

$vmConfig = Add-AzureRmVMNetworkInterface -VM $vmConfig -Id $nic.Id

New-AzureRmVM `
    -ResourceGroupName myResourceGroupFromImage `
    -Location EastUS `
    -VM $vmConfig
```

## <a name="image-management"></a><span data-ttu-id="adcd2-150">Zarządzanie obrazami</span><span class="sxs-lookup"><span data-stu-id="adcd2-150">Image management</span></span> 

<span data-ttu-id="adcd2-151">Oto kilka przykładów typowych zadań zarządzania dla obrazu i w jaki sposób toocomplete ich przy użyciu programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="adcd2-151">Here are some examples of common management image tasks and how toocomplete them using PowerShell.</span></span>

<span data-ttu-id="adcd2-152">Wyświetl listę wszystkich obrazów według nazwy.</span><span class="sxs-lookup"><span data-stu-id="adcd2-152">List all images by name.</span></span>

```powershell
$images = Find-AzureRMResource -ResourceType Microsoft.Compute/images 
$images.name
```

<span data-ttu-id="adcd2-153">Usuń obraz.</span><span class="sxs-lookup"><span data-stu-id="adcd2-153">Delete an image.</span></span> <span data-ttu-id="adcd2-154">W tym przykładzie usuwa hello obrazu o nazwie *myOldImage* z hello *myResourceGroup*.</span><span class="sxs-lookup"><span data-stu-id="adcd2-154">This example deletes hello image named *myOldImage* from hello *myResourceGroup*.</span></span>

```powershell
Remove-AzureRmImage `
    -ImageName myOldImage `
    -ResourceGroupName myResourceGroup
```

## <a name="next-steps"></a><span data-ttu-id="adcd2-155">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="adcd2-155">Next steps</span></span>

<span data-ttu-id="adcd2-156">W tym samouczku utworzony niestandardowy obraz maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="adcd2-156">In this tutorial, you created a custom VM image.</span></span> <span data-ttu-id="adcd2-157">W tym samouczku omówiono:</span><span class="sxs-lookup"><span data-stu-id="adcd2-157">You learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="adcd2-158">Narzędzie Sysprep i generalize maszyny wirtualne</span><span class="sxs-lookup"><span data-stu-id="adcd2-158">Sysprep and generalize VMs</span></span>
> * <span data-ttu-id="adcd2-159">Tworzenie obrazu niestandardowego</span><span class="sxs-lookup"><span data-stu-id="adcd2-159">Create a custom image</span></span>
> * <span data-ttu-id="adcd2-160">Utwórz maszynę Wirtualną z obrazu niestandardowego</span><span class="sxs-lookup"><span data-stu-id="adcd2-160">Create a VM from a custom image</span></span>
> * <span data-ttu-id="adcd2-161">Wyświetlanie listy wszystkich obrazów hello w ramach subskrypcji</span><span class="sxs-lookup"><span data-stu-id="adcd2-161">List all hello images in your subscription</span></span>
> * <span data-ttu-id="adcd2-162">Usuń obraz</span><span class="sxs-lookup"><span data-stu-id="adcd2-162">Delete an image</span></span>

<span data-ttu-id="adcd2-163">Przejdź dalej toolearn samouczka toohello o jak wysokiej dostępności maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="adcd2-163">Advance toohello next tutorial toolearn about how highly available virtual machines.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="adcd2-164">Tworzenie maszyn wirtualnych o wysokiej dostępności</span><span class="sxs-lookup"><span data-stu-id="adcd2-164">Create highly available VMs</span></span>](tutorial-availability-sets.md)



