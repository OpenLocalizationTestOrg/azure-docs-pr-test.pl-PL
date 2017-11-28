---
title: "Tworzenie zarządzanego obrazu na platformie Azure | Dokumentacja firmy Microsoft"
description: "Tworzenie zarządzanego obrazu maszyny Wirtualnej lub wirtualnego dysku twardego uogólnionego na platformie Azure. Obrazy mogą służyć do tworzenia wiele maszyn wirtualnych, które używają dysków zarządzanych."
services: virtual-machines-windows
documentationcenter: 
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
ms.date: 02/27/2017
ms.author: cynthn
ms.openlocfilehash: f64b81489ab426b50ec89af369e1581ac71848be
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/18/2017
---
# <a name="create-a-managed-image-of-a-generalized-vm-in-azure"></a><span data-ttu-id="2e84f-104">Tworzenie zarządzanego obrazu uogólniony maszyny wirtualnej na platformie Azure</span><span class="sxs-lookup"><span data-stu-id="2e84f-104">Create a managed image of a generalized VM in Azure</span></span>

<span data-ttu-id="2e84f-105">Można utworzyć zasobu zarządzanego obrazu z ogólnych maszyny Wirtualnej, która jest przechowywana jako dysków zarządzanych lub niezarządzanych dysku na koncie magazynu.</span><span class="sxs-lookup"><span data-stu-id="2e84f-105">A managed image resource can be created from a generalized VM that is stored as either a managed disk or an unmanaged disk in a storage account.</span></span> <span data-ttu-id="2e84f-106">Aby utworzyć wiele maszyn wirtualnych można następnie obrazu.</span><span class="sxs-lookup"><span data-stu-id="2e84f-106">The image can then be used to create multiple VMs.</span></span> 


## <a name="generalize-the-windows-vm-using-sysprep"></a><span data-ttu-id="2e84f-107">Maszyny Wirtualnej systemu Windows za pomocą programu Sysprep do uogólnienia</span><span class="sxs-lookup"><span data-stu-id="2e84f-107">Generalize the Windows VM using Sysprep</span></span>

<span data-ttu-id="2e84f-108">Program Sysprep usuwa wszystkie informacje osobiste konto, między innymi i przygotowuje komputer do użycia jako obraz.</span><span class="sxs-lookup"><span data-stu-id="2e84f-108">Sysprep removes all your personal account information, among other things, and prepares the machine to be used as an image.</span></span> <span data-ttu-id="2e84f-109">Aby uzyskać więcej informacji o narzędziu Sysprep, zobacz [sposobu użycia programu Sysprep: wprowadzenie](http://technet.microsoft.com/library/bb457073.aspx).</span><span class="sxs-lookup"><span data-stu-id="2e84f-109">For details about Sysprep, see [How to Use Sysprep: An Introduction](http://technet.microsoft.com/library/bb457073.aspx).</span></span>

<span data-ttu-id="2e84f-110">Upewnij się, że ról serwera uruchomionych na komputerze są obsługiwane przez program Sysprep.</span><span class="sxs-lookup"><span data-stu-id="2e84f-110">Make sure the server roles running on the machine are supported by Sysprep.</span></span> <span data-ttu-id="2e84f-111">Aby uzyskać więcej informacji, zobacz [Obsługa programu Sysprep dla ról serwera](https://msdn.microsoft.com/windows/hardware/commercialize/manufacture/desktop/sysprep-support-for-server-roles)</span><span class="sxs-lookup"><span data-stu-id="2e84f-111">For more information, see [Sysprep Support for Server Roles](https://msdn.microsoft.com/windows/hardware/commercialize/manufacture/desktop/sysprep-support-for-server-roles)</span></span>

> [!IMPORTANT]
> <span data-ttu-id="2e84f-112">Jeśli korzystasz z programu Sysprep przed przekazaniem dysk VHD do platformy Azure po raz pierwszy, upewnij się, masz [przygotować maszyny Wirtualnej](prepare-for-upload-vhd-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) przed uruchomieniem programu Sysprep.</span><span class="sxs-lookup"><span data-stu-id="2e84f-112">If you are running Sysprep before uploading your VHD to Azure for the first time, make sure you have [prepared your VM](prepare-for-upload-vhd-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) before running Sysprep.</span></span> 
> 
> 

1. <span data-ttu-id="2e84f-113">Zaloguj się do maszyny wirtualnej systemu Windows.</span><span class="sxs-lookup"><span data-stu-id="2e84f-113">Sign in to the Windows virtual machine.</span></span>
2. <span data-ttu-id="2e84f-114">Otwórz okno Wiersz polecenia jako administrator.</span><span class="sxs-lookup"><span data-stu-id="2e84f-114">Open the Command Prompt window as an administrator.</span></span> <span data-ttu-id="2e84f-115">Zmień katalog na **%windir%\system32\sysprep**, a następnie uruchom `sysprep.exe`.</span><span class="sxs-lookup"><span data-stu-id="2e84f-115">Change the directory to **%windir%\system32\sysprep**, and then run `sysprep.exe`.</span></span>
3. <span data-ttu-id="2e84f-116">W **narzędzie przygotowania systemu** okno dialogowe, wybierz opcję **wprowadź systemu Out-of-Box Experience (OOBE)**i upewnij się, że **Generalize** pole wyboru jest zaznaczone.</span><span class="sxs-lookup"><span data-stu-id="2e84f-116">In the **System Preparation Tool** dialog box, select **Enter System Out-of-Box Experience (OOBE)**, and make sure that the **Generalize** check box is selected.</span></span>
4. <span data-ttu-id="2e84f-117">W **opcje zamykania**, wybierz pozycję **zamknięcia**.</span><span class="sxs-lookup"><span data-stu-id="2e84f-117">In **Shutdown Options**, select **Shutdown**.</span></span>
5. <span data-ttu-id="2e84f-118">Kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="2e84f-118">Click **OK**.</span></span>
   
    ![Uruchom program Sysprep](./media/upload-generalized-managed/sysprepgeneral.png)
6. <span data-ttu-id="2e84f-120">Po zakończeniu działania programu Sysprep, zamyka maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="2e84f-120">When Sysprep completes, it shuts down the virtual machine.</span></span> <span data-ttu-id="2e84f-121">Nie uruchamiaj ponownie maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="2e84f-121">Do not restart the VM.</span></span>


## <a name="create-a-managed-image-in-the-portal"></a><span data-ttu-id="2e84f-122">Tworzenie zarządzanego obrazu w portalu</span><span class="sxs-lookup"><span data-stu-id="2e84f-122">Create a managed image in the portal</span></span> 

1. <span data-ttu-id="2e84f-123">Otwórz [portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="2e84f-123">Open the [portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="2e84f-124">Kliknij znak plus, aby utworzyć nowy zasób.</span><span class="sxs-lookup"><span data-stu-id="2e84f-124">Click the plus sign to create a new resource.</span></span>
3. <span data-ttu-id="2e84f-125">Filtr wyszukiwania, wpisz **obrazu**.</span><span class="sxs-lookup"><span data-stu-id="2e84f-125">In the filter search, type **Image**.</span></span>
4. <span data-ttu-id="2e84f-126">Wybierz **obrazu** z wyników.</span><span class="sxs-lookup"><span data-stu-id="2e84f-126">Select **Image** from the results.</span></span>
5. <span data-ttu-id="2e84f-127">W **obrazu** bloku, kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="2e84f-127">In the **Image** blade, click **Create**.</span></span>
6. <span data-ttu-id="2e84f-128">W **nazwa**, wpisz nazwę obrazu.</span><span class="sxs-lookup"><span data-stu-id="2e84f-128">In **Name**, type a name for the image.</span></span>
7. <span data-ttu-id="2e84f-129">Jeśli masz więcej niż jedną subskrypcję, wybierz właściwy z **subskrypcji** listy rozwijanej.</span><span class="sxs-lookup"><span data-stu-id="2e84f-129">If you have more than one subscription, select the correct one from the **Subscription** drop-down.</span></span>
7. <span data-ttu-id="2e84f-130">W **grupy zasobów** wybierz opcję **Utwórz nowy** i wpisz nazwę lub wybierz **z istniejących** i wybierz grupę zasobów do użycia z listy rozwijanej.</span><span class="sxs-lookup"><span data-stu-id="2e84f-130">In **Resource Group** either select **Create new** and type in a name, or select **From existing** and select a resource group to use from the drop-down list.</span></span>
8. <span data-ttu-id="2e84f-131">W **lokalizacji**, wybierz lokalizację, w grupie zasobów.</span><span class="sxs-lookup"><span data-stu-id="2e84f-131">In **Location**, choose the location of your resource group.</span></span>
9. <span data-ttu-id="2e84f-132">W **typ systemu operacyjnego** wybierz typ systemu operacyjnego, systemu Windows lub Linux.</span><span class="sxs-lookup"><span data-stu-id="2e84f-132">In **OS type** select the type of operating system, either Windows or Linux.</span></span>
11. <span data-ttu-id="2e84f-133">W **obiektu blob magazynu**, kliknij przycisk **Przeglądaj** do wyszukania dysku VHD w magazynie Azure.</span><span class="sxs-lookup"><span data-stu-id="2e84f-133">In **Storage blob**, click **Browse** to look for the VHD in your Azure storage.</span></span>
12. <span data-ttu-id="2e84f-134">W **typ konta** wybierz Standard_LRS lub Premium_LRS.</span><span class="sxs-lookup"><span data-stu-id="2e84f-134">In **Account type** choose Standard_LRS or Premium_LRS.</span></span> <span data-ttu-id="2e84f-135">Standard korzysta stacje dysków twardych, a Premium dysków SSD.</span><span class="sxs-lookup"><span data-stu-id="2e84f-135">Standard uses hard-disk drives and Premium uses solid-state drives.</span></span> <span data-ttu-id="2e84f-136">Oba rozwiązania używają magazyn lokalnie nadmiarowy.</span><span class="sxs-lookup"><span data-stu-id="2e84f-136">Both use locally-redundant storage.</span></span>
13. <span data-ttu-id="2e84f-137">W **buforowania dysku** wybierz odpowiedni dysk opcję buforowania.</span><span class="sxs-lookup"><span data-stu-id="2e84f-137">In **Disk caching** select the appropriate disk caching option.</span></span> <span data-ttu-id="2e84f-138">Dostępne są następujące opcje **Brak**, **tylko do odczytu** i **odczytem/zapisem**.</span><span class="sxs-lookup"><span data-stu-id="2e84f-138">The options are **None**, **Read-only** and **Read\write**.</span></span>
14. <span data-ttu-id="2e84f-139">Opcjonalnie: Również dodaniem istniejącego dysku danych do obrazu, klikając **+ Dodaj dysk danych**.</span><span class="sxs-lookup"><span data-stu-id="2e84f-139">Optional: You can also add an existing data disk to the image by clicking **+ Add data disk**.</span></span>  
15. <span data-ttu-id="2e84f-140">Po zakończeniu wprowadzania wybrane opcje, kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="2e84f-140">When you are done making your selections, click **Create**.</span></span>
16. <span data-ttu-id="2e84f-141">Po utworzeniu obrazu, zobaczysz go jako **obrazu** zasobu na liście zasobów w grupie zasobów, wybrana.</span><span class="sxs-lookup"><span data-stu-id="2e84f-141">After the image is created, you will see it as an **Image** resource in the list of resources in the resource group you chose.</span></span>



## <a name="create-a-managed-image-of-a-vm-using-powershell"></a><span data-ttu-id="2e84f-142">Tworzenie zarządzanego obrazu maszyny wirtualnej przy użyciu programu Powershell</span><span class="sxs-lookup"><span data-stu-id="2e84f-142">Create a managed image of a VM using Powershell</span></span>

<span data-ttu-id="2e84f-143">Tworzenie obrazu bezpośrednio z maszyny Wirtualnej sprawdza, czy obraz zawiera wszystkie dyski skojarzonych z maszyną Wirtualną, w tym dysku systemu operacyjnego i dysków z danymi.</span><span class="sxs-lookup"><span data-stu-id="2e84f-143">Creating an image directly from the VM ensures that the image includes all of the disks associated with the VM, including the OS Disk and any data disks.</span></span>


<span data-ttu-id="2e84f-144">Przed rozpoczęciem upewnij się, że masz najnowszą wersję modułu programu AzureRM.Compute PowerShell.</span><span class="sxs-lookup"><span data-stu-id="2e84f-144">Before you begin, make sure that you have the latest version of the AzureRM.Compute PowerShell module.</span></span> <span data-ttu-id="2e84f-145">Uruchom następujące polecenie, aby go zainstalować.</span><span class="sxs-lookup"><span data-stu-id="2e84f-145">Run the following command to install it.</span></span>

```powershell
Install-Module AzureRM.Compute -RequiredVersion 2.6.0
```
<span data-ttu-id="2e84f-146">Aby uzyskać więcej informacji, zobacz [przechowywanie wersji programu Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="2e84f-146">For more information, see [Azure PowerShell Versioning](/powershell/azure/overview).</span></span>


1. <span data-ttu-id="2e84f-147">Utwórz niektóre zmienne.</span><span class="sxs-lookup"><span data-stu-id="2e84f-147">Create some variables.</span></span>

    ```powershell
    $vmName = "myVM"
    $rgName = "myResourceGroup"
    $location = "EastUS"
    $imageName = "myImage"
    ```
2. <span data-ttu-id="2e84f-148">Upewnij się, że cofnięciu przydziału maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="2e84f-148">Make sure the VM has been deallocated.</span></span>

    ```powershell
    Stop-AzureRmVM -ResourceGroupName $rgName -Name $vmName -Force
    ```
    
3. <span data-ttu-id="2e84f-149">Ustaw stan maszyny wirtualnej na **Uogólniono**.</span><span class="sxs-lookup"><span data-stu-id="2e84f-149">Set the status of the virtual machine to **Generalized**.</span></span> 
   
    ```powershell
    Set-AzureRmVm -ResourceGroupName $rgName -Name $vmName -Generalized
    ```
    
4. <span data-ttu-id="2e84f-150">Przełącz maszynę wirtualną.</span><span class="sxs-lookup"><span data-stu-id="2e84f-150">Get the virtual machine.</span></span> 

    ```powershell
    $vm = Get-AzureRmVM -Name $vmName -ResourceGroupName $rgName
    ```

5. <span data-ttu-id="2e84f-151">Utwórz konfigurację obrazu.</span><span class="sxs-lookup"><span data-stu-id="2e84f-151">Create the image configuration.</span></span>

    ```powershell
    $image = New-AzureRmImageConfig -Location $location -SourceVirtualMachineId $vm.ID 
    ```
6. <span data-ttu-id="2e84f-152">Tworzenie obrazu.</span><span class="sxs-lookup"><span data-stu-id="2e84f-152">Create the image.</span></span>

    ```powershell
    New-AzureRmImage -Image $image -ImageName $imageName -ResourceGroupName $rgName
    ``` 



## <a name="create-a-managed-image-of-a-vhd-in-powershell"></a><span data-ttu-id="2e84f-153">Tworzenie zarządzanego obrazu dysku VHD w programie PowerShell</span><span class="sxs-lookup"><span data-stu-id="2e84f-153">Create a managed image of a VHD in PowerShell</span></span>

<span data-ttu-id="2e84f-154">Tworzenie obrazu zarządzanych za pomocą programu uogólniony wirtualny dysk twardy systemu operacyjnego.</span><span class="sxs-lookup"><span data-stu-id="2e84f-154">Create a managed image using your generalized OS VHD.</span></span>


1.  <span data-ttu-id="2e84f-155">Najpierw należy ustawić wspólne parametry:</span><span class="sxs-lookup"><span data-stu-id="2e84f-155">First, set the common parameters:</span></span>

    ```powershell
    $rgName = "myResourceGroupName"
    $vmName = "myVM"
    $location = "West Central US" 
    $imageName = "yourImageName"
    $osVhdUri = "https://storageaccount.blob.core.windows.net/vhdcontainer/osdisk.vhd"
    ```
2. <span data-ttu-id="2e84f-156">Step\deallocate maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="2e84f-156">Step\deallocate the VM.</span></span>

    ```powershell
    Stop-AzureRmVM -ResourceGroupName $rgName -Name $vmName -Force
    ```
    
3. <span data-ttu-id="2e84f-157">Maszyna wirtualna zostać oznaczone jako uogólniony.</span><span class="sxs-lookup"><span data-stu-id="2e84f-157">Mark the VM as generalized.</span></span>

    ```powershell
    Set-AzureRmVm -ResourceGroupName $rgName -Name $vmName -Generalized 
    ```
4.  <span data-ttu-id="2e84f-158">Utworzyć obraz przy użyciu programu uogólniony wirtualny dysk twardy systemu operacyjnego.</span><span class="sxs-lookup"><span data-stu-id="2e84f-158">Create the image using your generalized OS VHD.</span></span>

    ```powershell
    $imageConfig = New-AzureRmImageConfig -Location $location
    $imageConfig = Set-AzureRmImageOsDisk -Image $imageConfig -OsType Windows -OsState Generalized -BlobUri $osVhdUri
    $image = New-AzureRmImage -ImageName $imageName -ResourceGroupName $rgName -Image $imageConfig
    ```


## <a name="create-a-managed-image-from-a-snapshot-using-powershell"></a><span data-ttu-id="2e84f-159">Tworzenie zarządzanego obrazu z migawki za pomocą programu Powershell</span><span class="sxs-lookup"><span data-stu-id="2e84f-159">Create a managed image from a snapshot using Powershell</span></span>

<span data-ttu-id="2e84f-160">Można również utworzyć obraz zarządzanego z migawki wirtualnego dysku twardego z ogólnych maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="2e84f-160">You can also create a managed image from a snapshot of the VHD from a generalized VM.</span></span>

    
1. <span data-ttu-id="2e84f-161">Utwórz niektóre zmienne.</span><span class="sxs-lookup"><span data-stu-id="2e84f-161">Create some variables.</span></span> 

    ```powershell
    $rgName = "myResourceGroup"
    $location = "EastUS"
    $snapshotName = "mySnapshot"
    $imageName = "myImage"
    ```

2. <span data-ttu-id="2e84f-162">Pobieranie migawki.</span><span class="sxs-lookup"><span data-stu-id="2e84f-162">Get the snapshot.</span></span>

   ```powershell
   $snapshot = Get-AzureRmSnapshot -ResourceGroupName $rgName -SnapshotName $snapshotName
   ```
   
3. <span data-ttu-id="2e84f-163">Utwórz konfigurację obrazu.</span><span class="sxs-lookup"><span data-stu-id="2e84f-163">Create the image configuration.</span></span>

    ```powershell
    $imageConfig = New-AzureRmImageConfig -Location $location
    $imageConfig = Set-AzureRmImageOsDisk -Image $imageConfig -OsState Generalized -OsType Windows -SnapshotId $snapshot.Id
    ```
4. <span data-ttu-id="2e84f-164">Tworzenie obrazu.</span><span class="sxs-lookup"><span data-stu-id="2e84f-164">Create the image.</span></span>

    ```powershell
    New-AzureRmImage -ImageName $imageName -ResourceGroupName $rgName -Image $imageConfig
    ``` 
    

## <a name="next-steps"></a><span data-ttu-id="2e84f-165">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="2e84f-165">Next steps</span></span>
- <span data-ttu-id="2e84f-166">Teraz możesz [utworzyć Maszynę wirtualną z uogólniony obraz zarządzanych](create-vm-generalized-managed.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="2e84f-166">Now you can [create a VM from the generalized managed image](create-vm-generalized-managed.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>  

