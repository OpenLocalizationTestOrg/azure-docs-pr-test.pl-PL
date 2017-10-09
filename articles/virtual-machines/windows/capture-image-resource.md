---
title: "aaaCreate zarządzanego obrazu na platformie Azure | Dokumentacja firmy Microsoft"
description: "Tworzenie zarządzanego obrazu maszyny Wirtualnej lub wirtualnego dysku twardego uogólnionego na platformie Azure. Obrazy mogą być używane toocreate wiele maszyn wirtualnych, które używają dysków zarządzanych."
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
ms.openlocfilehash: d8cd6c2ce8c5d704de2c845abced85139944d682
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-managed-image-of-a-generalized-vm-in-azure"></a><span data-ttu-id="83739-104">Tworzenie zarządzanego obrazu uogólniony maszyny wirtualnej na platformie Azure</span><span class="sxs-lookup"><span data-stu-id="83739-104">Create a managed image of a generalized VM in Azure</span></span>

<span data-ttu-id="83739-105">Można utworzyć zasobu zarządzanego obrazu z ogólnych maszyny Wirtualnej, która jest przechowywana jako dysków zarządzanych lub niezarządzanych dysku na koncie magazynu.</span><span class="sxs-lookup"><span data-stu-id="83739-105">A managed image resource can be created from a generalized VM that is stored as either a managed disk or an unmanaged disk in a storage account.</span></span> <span data-ttu-id="83739-106">Witaj może obrazu, a następnie można toocreate używanych wiele maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="83739-106">hello image can then be used toocreate multiple VMs.</span></span> 


## <a name="generalize-hello-windows-vm-using-sysprep"></a><span data-ttu-id="83739-107">Generalize hello maszyny Wirtualnej systemu Windows za pomocą programu Sysprep</span><span class="sxs-lookup"><span data-stu-id="83739-107">Generalize hello Windows VM using Sysprep</span></span>

<span data-ttu-id="83739-108">Program Sysprep usuwa wszystkie informacje osobiste konto, między innymi i przygotowuje toobe maszyny hello użyty jako obraz.</span><span class="sxs-lookup"><span data-stu-id="83739-108">Sysprep removes all your personal account information, among other things, and prepares hello machine toobe used as an image.</span></span> <span data-ttu-id="83739-109">Aby uzyskać więcej informacji o narzędziu Sysprep, zobacz [jak tooUse Sysprep: wprowadzenie](http://technet.microsoft.com/library/bb457073.aspx).</span><span class="sxs-lookup"><span data-stu-id="83739-109">For details about Sysprep, see [How tooUse Sysprep: An Introduction](http://technet.microsoft.com/library/bb457073.aspx).</span></span>

<span data-ttu-id="83739-110">Upewnij się, że hello ról serwera uruchomionych na maszynie hello są obsługiwane przez program Sysprep.</span><span class="sxs-lookup"><span data-stu-id="83739-110">Make sure hello server roles running on hello machine are supported by Sysprep.</span></span> <span data-ttu-id="83739-111">Aby uzyskać więcej informacji, zobacz [Obsługa programu Sysprep dla ról serwera](https://msdn.microsoft.com/windows/hardware/commercialize/manufacture/desktop/sysprep-support-for-server-roles)</span><span class="sxs-lookup"><span data-stu-id="83739-111">For more information, see [Sysprep Support for Server Roles](https://msdn.microsoft.com/windows/hardware/commercialize/manufacture/desktop/sysprep-support-for-server-roles)</span></span>

> [!IMPORTANT]
> <span data-ttu-id="83739-112">Jeśli korzystasz z programu Sysprep przed przekazaniem tooAzure Twojego dysku VHD na powitania po raz pierwszy, upewnij się, masz [przygotować maszyny Wirtualnej](prepare-for-upload-vhd-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) przed uruchomieniem programu Sysprep.</span><span class="sxs-lookup"><span data-stu-id="83739-112">If you are running Sysprep before uploading your VHD tooAzure for hello first time, make sure you have [prepared your VM](prepare-for-upload-vhd-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) before running Sysprep.</span></span> 
> 
> 

1. <span data-ttu-id="83739-113">Zaloguj się toohello maszyny wirtualnej systemu Windows.</span><span class="sxs-lookup"><span data-stu-id="83739-113">Sign in toohello Windows virtual machine.</span></span>
2. <span data-ttu-id="83739-114">Otwórz okno wiersza polecenia hello jako administrator.</span><span class="sxs-lookup"><span data-stu-id="83739-114">Open hello Command Prompt window as an administrator.</span></span> <span data-ttu-id="83739-115">Zmień katalog hello zbyt**%windir%\system32\sysprep**, a następnie uruchom `sysprep.exe`.</span><span class="sxs-lookup"><span data-stu-id="83739-115">Change hello directory too**%windir%\system32\sysprep**, and then run `sysprep.exe`.</span></span>
3. <span data-ttu-id="83739-116">W hello **narzędzie przygotowania systemu** okno dialogowe, wybierz opcję **wprowadź systemu Out-of-Box Experience (OOBE)**i upewnij się, że hello **Generalize** pole wyboru jest zaznaczone.</span><span class="sxs-lookup"><span data-stu-id="83739-116">In hello **System Preparation Tool** dialog box, select **Enter System Out-of-Box Experience (OOBE)**, and make sure that hello **Generalize** check box is selected.</span></span>
4. <span data-ttu-id="83739-117">W **opcje zamykania**, wybierz pozycję **zamknięcia**.</span><span class="sxs-lookup"><span data-stu-id="83739-117">In **Shutdown Options**, select **Shutdown**.</span></span>
5. <span data-ttu-id="83739-118">Kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="83739-118">Click **OK**.</span></span>
   
    ![Uruchom program Sysprep](./media/upload-generalized-managed/sysprepgeneral.png)
6. <span data-ttu-id="83739-120">Po zakończeniu działania programu Sysprep, zamyka hello maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="83739-120">When Sysprep completes, it shuts down hello virtual machine.</span></span> <span data-ttu-id="83739-121">Nie uruchamiaj ponownie hello maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="83739-121">Do not restart hello VM.</span></span>


## <a name="create-a-managed-image-in-hello-portal"></a><span data-ttu-id="83739-122">Tworzenie zarządzanego obrazu w portalu hello</span><span class="sxs-lookup"><span data-stu-id="83739-122">Create a managed image in hello portal</span></span> 

1. <span data-ttu-id="83739-123">Otwórz hello [portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="83739-123">Open hello [portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="83739-124">Kliknij przycisk hello toocreate znak plus nowy zasób.</span><span class="sxs-lookup"><span data-stu-id="83739-124">Click hello plus sign toocreate a new resource.</span></span>
3. <span data-ttu-id="83739-125">Witaj filtr wyszukiwania, wpisz **obrazu**.</span><span class="sxs-lookup"><span data-stu-id="83739-125">In hello filter search, type **Image**.</span></span>
4. <span data-ttu-id="83739-126">Wybierz **obrazu** z hello wyników.</span><span class="sxs-lookup"><span data-stu-id="83739-126">Select **Image** from hello results.</span></span>
5. <span data-ttu-id="83739-127">W hello **obrazu** bloku, kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="83739-127">In hello **Image** blade, click **Create**.</span></span>
6. <span data-ttu-id="83739-128">W **nazwa**, wpisz nazwę hello obrazu.</span><span class="sxs-lookup"><span data-stu-id="83739-128">In **Name**, type a name for hello image.</span></span>
7. <span data-ttu-id="83739-129">Jeśli masz więcej niż jedną subskrypcję, wybierz hello właściwy z hello **subskrypcji** listy rozwijanej.</span><span class="sxs-lookup"><span data-stu-id="83739-129">If you have more than one subscription, select hello correct one from hello **Subscription** drop-down.</span></span>
7. <span data-ttu-id="83739-130">W **grupy zasobów** wybierz opcję **Utwórz nowy** i wpisz nazwę lub wybierz **z istniejących** i wybierz z listy rozwijanej hello toouse grupy zasobów.</span><span class="sxs-lookup"><span data-stu-id="83739-130">In **Resource Group** either select **Create new** and type in a name, or select **From existing** and select a resource group toouse from hello drop-down list.</span></span>
8. <span data-ttu-id="83739-131">W **lokalizacji**, wybierz lokalizację hello grupy zasobów.</span><span class="sxs-lookup"><span data-stu-id="83739-131">In **Location**, choose hello location of your resource group.</span></span>
9. <span data-ttu-id="83739-132">W **typ systemu operacyjnego** hello typ systemu operacyjnego, systemu Windows lub Linux.</span><span class="sxs-lookup"><span data-stu-id="83739-132">In **OS type** select hello type of operating system, either Windows or Linux.</span></span>
11. <span data-ttu-id="83739-133">W **obiektu blob magazynu**, kliknij przycisk **Przeglądaj** toolook dla hello dysku VHD w magazynie Azure.</span><span class="sxs-lookup"><span data-stu-id="83739-133">In **Storage blob**, click **Browse** toolook for hello VHD in your Azure storage.</span></span>
12. <span data-ttu-id="83739-134">W **typ konta** wybierz Standard_LRS lub Premium_LRS.</span><span class="sxs-lookup"><span data-stu-id="83739-134">In **Account type** choose Standard_LRS or Premium_LRS.</span></span> <span data-ttu-id="83739-135">Standard korzysta stacje dysków twardych, a Premium dysków SSD.</span><span class="sxs-lookup"><span data-stu-id="83739-135">Standard uses hard-disk drives and Premium uses solid-state drives.</span></span> <span data-ttu-id="83739-136">Oba rozwiązania używają magazyn lokalnie nadmiarowy.</span><span class="sxs-lookup"><span data-stu-id="83739-136">Both use locally-redundant storage.</span></span>
13. <span data-ttu-id="83739-137">W **buforowania dysku** wybierz hello odpowiedniego dysku opcję buforowania.</span><span class="sxs-lookup"><span data-stu-id="83739-137">In **Disk caching** select hello appropriate disk caching option.</span></span> <span data-ttu-id="83739-138">Opcje Hello są **Brak**, **tylko do odczytu** i **odczytem/zapisem**.</span><span class="sxs-lookup"><span data-stu-id="83739-138">hello options are **None**, **Read-only** and **Read\write**.</span></span>
14. <span data-ttu-id="83739-139">Opcjonalnie: Można również dodać istniejący obraz toohello dysku danych, klikając **+ Dodaj dysk danych**.</span><span class="sxs-lookup"><span data-stu-id="83739-139">Optional: You can also add an existing data disk toohello image by clicking **+ Add data disk**.</span></span>  
15. <span data-ttu-id="83739-140">Po zakończeniu wprowadzania wybrane opcje, kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="83739-140">When you are done making your selections, click **Create**.</span></span>
16. <span data-ttu-id="83739-141">Po utworzeniu obrazu hello, zobaczysz go jako **obrazu** zasobu w hello listy zasobów w grupie zasobów hello została wybrana opcja.</span><span class="sxs-lookup"><span data-stu-id="83739-141">After hello image is created, you will see it as an **Image** resource in hello list of resources in hello resource group you chose.</span></span>



## <a name="create-a-managed-image-of-a-vm-using-powershell"></a><span data-ttu-id="83739-142">Tworzenie zarządzanego obrazu maszyny wirtualnej przy użyciu programu Powershell</span><span class="sxs-lookup"><span data-stu-id="83739-142">Create a managed image of a VM using Powershell</span></span>

<span data-ttu-id="83739-143">Tworzenie obrazu bezpośrednio z maszyn wirtualnych zapewnia obrazu hello powitalne obejmuje wszystkie dyski hello skojarzone hello maszyny Wirtualnej, w tym hello dysku systemu operacyjnego i dysków z danymi.</span><span class="sxs-lookup"><span data-stu-id="83739-143">Creating an image directly from hello VM ensures that hello image includes all of hello disks associated with hello VM, including hello OS Disk and any data disks.</span></span>


<span data-ttu-id="83739-144">Przed rozpoczęciem upewnij się, że masz najnowszą wersję hello modułu AzureRM.Compute PowerShell hello.</span><span class="sxs-lookup"><span data-stu-id="83739-144">Before you begin, make sure that you have hello latest version of hello AzureRM.Compute PowerShell module.</span></span> <span data-ttu-id="83739-145">Uruchom hello następujących tooinstall polecenia.</span><span class="sxs-lookup"><span data-stu-id="83739-145">Run hello following command tooinstall it.</span></span>

```powershell
Install-Module AzureRM.Compute -RequiredVersion 2.6.0
```
<span data-ttu-id="83739-146">Aby uzyskać więcej informacji, zobacz [przechowywanie wersji programu Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="83739-146">For more information, see [Azure PowerShell Versioning](/powershell/azure/overview).</span></span>


1. <span data-ttu-id="83739-147">Utwórz niektóre zmienne.</span><span class="sxs-lookup"><span data-stu-id="83739-147">Create some variables.</span></span>

    ```powershell
    $vmName = "myVM"
    $rgName = "myResourceGroup"
    $location = "EastUS"
    $imageName = "myImage"
    ```
2. <span data-ttu-id="83739-148">Upewnij się, że powitalne cofnięciu przydziału maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="83739-148">Make sure hello VM has been deallocated.</span></span>

    ```powershell
    Stop-AzureRmVM -ResourceGroupName $rgName -Name $vmName -Force
    ```
    
3. <span data-ttu-id="83739-149">Ustaw stan hello hello maszyny wirtualnej za**Uogólniono**.</span><span class="sxs-lookup"><span data-stu-id="83739-149">Set hello status of hello virtual machine too**Generalized**.</span></span> 
   
    ```powershell
    Set-AzureRmVm -ResourceGroupName $rgName -Name $vmName -Generalized
    ```
    
4. <span data-ttu-id="83739-150">Pobierz hello maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="83739-150">Get hello virtual machine.</span></span> 

    ```powershell
    $vm = Get-AzureRmVM -Name $vmName -ResourceGroupName $rgName
    ```

5. <span data-ttu-id="83739-151">Utwórz konfigurację obraz powitania.</span><span class="sxs-lookup"><span data-stu-id="83739-151">Create hello image configuration.</span></span>

    ```powershell
    $image = New-AzureRmImageConfig -Location $location -SourceVirtualMachineId $vm.ID 
    ```
6. <span data-ttu-id="83739-152">Utwórz obraz powitania.</span><span class="sxs-lookup"><span data-stu-id="83739-152">Create hello image.</span></span>

    ```powershell
    New-AzureRmImage -Image $image -ImageName $imageName -ResourceGroupName $rgName
    ``` 



## <a name="create-a-managed-image-of-a-vhd-in-powershell"></a><span data-ttu-id="83739-153">Tworzenie zarządzanego obrazu dysku VHD w programie PowerShell</span><span class="sxs-lookup"><span data-stu-id="83739-153">Create a managed image of a VHD in PowerShell</span></span>

<span data-ttu-id="83739-154">Tworzenie obrazu zarządzanych za pomocą programu uogólniony wirtualny dysk twardy systemu operacyjnego.</span><span class="sxs-lookup"><span data-stu-id="83739-154">Create a managed image using your generalized OS VHD.</span></span>


1.  <span data-ttu-id="83739-155">Najpierw należy ustawić hello typowe parametry:</span><span class="sxs-lookup"><span data-stu-id="83739-155">First, set hello common parameters:</span></span>

    ```powershell
    $rgName = "myResourceGroupName"
    $vmName = "myVM"
    $location = "West Central US" 
    $imageName = "yourImageName"
    $osVhdUri = "https://storageaccount.blob.core.windows.net/vhdcontainer/osdisk.vhd"
    ```
2. <span data-ttu-id="83739-156">Witaj Step\deallocate maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="83739-156">Step\deallocate hello VM.</span></span>

    ```powershell
    Stop-AzureRmVM -ResourceGroupName $rgName -Name $vmName -Force
    ```
    
3. <span data-ttu-id="83739-157">Oznacz hello maszyny Wirtualnej, ponieważ uogólniony.</span><span class="sxs-lookup"><span data-stu-id="83739-157">Mark hello VM as generalized.</span></span>

    ```powershell
    Set-AzureRmVm -ResourceGroupName $rgName -Name $vmName -Generalized 
    ```
4.  <span data-ttu-id="83739-158">Utwórz obraz powitania przy użyciu Twojej uogólniony wirtualny dysk twardy systemu operacyjnego.</span><span class="sxs-lookup"><span data-stu-id="83739-158">Create hello image using your generalized OS VHD.</span></span>

    ```powershell
    $imageConfig = New-AzureRmImageConfig -Location $location
    $imageConfig = Set-AzureRmImageOsDisk -Image $imageConfig -OsType Windows -OsState Generalized -BlobUri $osVhdUri
    $image = New-AzureRmImage -ImageName $imageName -ResourceGroupName $rgName -Image $imageConfig
    ```


## <a name="create-a-managed-image-from-a-snapshot-using-powershell"></a><span data-ttu-id="83739-159">Tworzenie zarządzanego obrazu z migawki za pomocą programu Powershell</span><span class="sxs-lookup"><span data-stu-id="83739-159">Create a managed image from a snapshot using Powershell</span></span>

<span data-ttu-id="83739-160">Można również utworzyć obraz zarządzanego z migawki hello wirtualnego dysku twardego z ogólnych maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="83739-160">You can also create a managed image from a snapshot of hello VHD from a generalized VM.</span></span>

    
1. <span data-ttu-id="83739-161">Utwórz niektóre zmienne.</span><span class="sxs-lookup"><span data-stu-id="83739-161">Create some variables.</span></span> 

    ```powershell
    $rgName = "myResourceGroup"
    $location = "EastUS"
    $snapshotName = "mySnapshot"
    $imageName = "myImage"
    ```

2. <span data-ttu-id="83739-162">Pobierz hello migawki.</span><span class="sxs-lookup"><span data-stu-id="83739-162">Get hello snapshot.</span></span>

   ```powershell
   $snapshot = Get-AzureRmSnapshot -ResourceGroupName $rgName -SnapshotName $snapshotName
   ```
   
3. <span data-ttu-id="83739-163">Utwórz konfigurację obraz powitania.</span><span class="sxs-lookup"><span data-stu-id="83739-163">Create hello image configuration.</span></span>

    ```powershell
    $imageConfig = New-AzureRmImageConfig -Location $location
    $imageConfig = Set-AzureRmImageOsDisk -Image $imageConfig -OsState Generalized -OsType Windows -SnapshotId $snapshot.Id
    ```
4. <span data-ttu-id="83739-164">Utwórz obraz powitania.</span><span class="sxs-lookup"><span data-stu-id="83739-164">Create hello image.</span></span>

    ```powershell
    New-AzureRmImage -ImageName $imageName -ResourceGroupName $rgName -Image $imageConfig
    ``` 
    

## <a name="next-steps"></a><span data-ttu-id="83739-165">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="83739-165">Next steps</span></span>
- <span data-ttu-id="83739-166">Teraz możesz [utworzyć Maszynę wirtualną z obrazu zarządzanych hello uogólniony](create-vm-generalized-managed.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="83739-166">Now you can [create a VM from hello generalized managed image](create-vm-generalized-managed.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>    

