---
title: "Tworzenie obrazu niezarządzane uogólniony maszyny wirtualnej na platformie Azure | Dokumentacja firmy Microsoft"
description: "Utwórz obraz unmanged uogólniony maszyny Wirtualnej systemu Windows na potrzeby tworzenia wielu kopii maszyny wirtualnej na platformie Azure."
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 05/23/2017
ms.author: cynthn
ms.openlocfilehash: d7f4a9558175835eba9096e6845726f21c7459d3
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/18/2017
---
# <a name="how-to-create-an-unmanaged-vm-image-from-an-azure-vm"></a><span data-ttu-id="d59a3-103">Jak utworzyć niezarządzane obrazu maszyny Wirtualnej z maszyny Wirtualnej platformy Azure</span><span class="sxs-lookup"><span data-stu-id="d59a3-103">How to create an unmanaged VM image from an Azure VM</span></span>

<span data-ttu-id="d59a3-104">W tym artykule omówiono używanie kont magazynu.</span><span class="sxs-lookup"><span data-stu-id="d59a3-104">This article covers using storage accounts.</span></span> <span data-ttu-id="d59a3-105">Zalecane jest użycie dysków zarządzanych i zarządzanych obrazów zamiast konta magazynu.</span><span class="sxs-lookup"><span data-stu-id="d59a3-105">We recommend that you use managed disks and managed images instead of a storage account.</span></span> <span data-ttu-id="d59a3-106">Aby uzyskać więcej informacji, zobacz [Przechwyć obraz zarządzanych uogólniony maszyny wirtualnej na platformie Azure](capture-image-resource.md).</span><span class="sxs-lookup"><span data-stu-id="d59a3-106">For more information, see [Capture a managed image of a generalized VM in Azure](capture-image-resource.md).</span></span>

<span data-ttu-id="d59a3-107">W tym artykule przedstawiono sposób tworzenia obrazu uogólniony maszyny Wirtualnej platformy Azure przy użyciu programu Azure PowerShell przy użyciu konta magazynu.</span><span class="sxs-lookup"><span data-stu-id="d59a3-107">This article shows you how to use Azure PowerShell to create an image of a generalized Azure VM using a storage account.</span></span> <span data-ttu-id="d59a3-108">Obraz można następnie używać do tworzenia inną maszynę Wirtualną.</span><span class="sxs-lookup"><span data-stu-id="d59a3-108">You can then use the image to create another VM.</span></span> <span data-ttu-id="d59a3-109">Obraz zawiera dysk systemu operacyjnego i dysków z danymi, które są dołączone do maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="d59a3-109">The image includes the OS disk and the data disks that are attached to the virtual machine.</span></span> <span data-ttu-id="d59a3-110">Obraz nie zawiera zasobów sieci wirtualnej, więc należy skonfigurować te zasoby, podczas tworzenia nowej maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="d59a3-110">The image doesn't include the virtual network resources, so you need to set up those resources when you create the new VM.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="d59a3-111">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="d59a3-111">Prerequisites</span></span>
<span data-ttu-id="d59a3-112">Musisz mieć wersję programu Azure PowerShell 1.0.x lub nowszej.</span><span class="sxs-lookup"><span data-stu-id="d59a3-112">You need to have Azure PowerShell version 1.0.x or newer installed.</span></span> <span data-ttu-id="d59a3-113">Jeśli jeszcze nie zainstalowano programu PowerShell, przeczytaj [jak instalowanie i konfigurowanie programu Azure PowerShell](/powershell/azure/overview) kroki instalacji.</span><span class="sxs-lookup"><span data-stu-id="d59a3-113">If you haven't already installed PowerShell, read [How to install and configure Azure PowerShell](/powershell/azure/overview) for installation steps.</span></span>

## <a name="generalize-the-vm"></a><span data-ttu-id="d59a3-114">Generalize maszyny Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="d59a3-114">Generalize the VM</span></span> 
<span data-ttu-id="d59a3-115">W tej sekcji przedstawiono sposób generalize maszyny wirtualnej systemu Windows do użycia jako obraz.</span><span class="sxs-lookup"><span data-stu-id="d59a3-115">This section shows you how to generalize your Windows virtual machine for use as an image.</span></span> <span data-ttu-id="d59a3-116">Uogólnianie maszyny Wirtualnej powoduje usunięcie wszystkich informacji osobowych konta, między innymi i przygotowuje komputer do użycia jako obraz.</span><span class="sxs-lookup"><span data-stu-id="d59a3-116">Generalizing a VM removes all your personal account information, among other things, and prepares the machine to be used as an image.</span></span> <span data-ttu-id="d59a3-117">Aby uzyskać więcej informacji o narzędziu Sysprep, zobacz [sposobu użycia programu Sysprep: wprowadzenie](http://technet.microsoft.com/library/bb457073.aspx).</span><span class="sxs-lookup"><span data-stu-id="d59a3-117">For details about Sysprep, see [How to Use Sysprep: An Introduction](http://technet.microsoft.com/library/bb457073.aspx).</span></span>

<span data-ttu-id="d59a3-118">Upewnij się, że ról serwera uruchomionych na komputerze są obsługiwane przez program Sysprep.</span><span class="sxs-lookup"><span data-stu-id="d59a3-118">Make sure the server roles running on the machine are supported by Sysprep.</span></span> <span data-ttu-id="d59a3-119">Aby uzyskać więcej informacji, zobacz [Obsługa programu Sysprep dla ról serwera](https://msdn.microsoft.com/windows/hardware/commercialize/manufacture/desktop/sysprep-support-for-server-roles)</span><span class="sxs-lookup"><span data-stu-id="d59a3-119">For more information, see [Sysprep Support for Server Roles](https://msdn.microsoft.com/windows/hardware/commercialize/manufacture/desktop/sysprep-support-for-server-roles)</span></span>

> [!IMPORTANT]
> <span data-ttu-id="d59a3-120">Podczas przekazywania dysk VHD do platformy Azure po raz pierwszy, upewnij się, że masz [przygotować maszyny Wirtualnej](prepare-for-upload-vhd-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) przed uruchomieniem programu Sysprep.</span><span class="sxs-lookup"><span data-stu-id="d59a3-120">If you are uploading your VHD to Azure for the first time, make sure you have [prepared your VM](prepare-for-upload-vhd-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) before running Sysprep.</span></span> 
> 
> 

<span data-ttu-id="d59a3-121">Można również generalize maszyny Wirtualnej systemu Linux przy użyciu `sudo waagent -deprovision+user` i przechwytywanie maszyny Wirtualnej za pomocą programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="d59a3-121">You can also generalize a Linux VM using `sudo waagent -deprovision+user` and then use PowerShell to capture the VM.</span></span> <span data-ttu-id="d59a3-122">Aby dowiedzieć się, jak przechwycić Maszynę wirtualną za pomocą interfejsu wiersza polecenia, zobacz [generalize i przechwytywanie maszyny wirtualnej systemu Linux przy użyciu interfejsu wiersza polecenia Azure ](../linux/capture-image.md).</span><span class="sxs-lookup"><span data-stu-id="d59a3-122">For information about using the CLI to capture a VM, see [How to generalize and capture a Linux virtual machine using the Azure CLI ](../linux/capture-image.md).</span></span>


1. <span data-ttu-id="d59a3-123">Zaloguj się do maszyny wirtualnej systemu Windows.</span><span class="sxs-lookup"><span data-stu-id="d59a3-123">Sign in to the Windows virtual machine.</span></span>
2. <span data-ttu-id="d59a3-124">Otwórz okno Wiersz polecenia jako administrator.</span><span class="sxs-lookup"><span data-stu-id="d59a3-124">Open the Command Prompt window as an administrator.</span></span> <span data-ttu-id="d59a3-125">Zmień katalog na **%windir%\system32\sysprep**, a następnie uruchom `sysprep.exe`.</span><span class="sxs-lookup"><span data-stu-id="d59a3-125">Change the directory to **%windir%\system32\sysprep**, and then run `sysprep.exe`.</span></span>
3. <span data-ttu-id="d59a3-126">W **narzędzie przygotowania systemu** okno dialogowe, wybierz opcję **wprowadź systemu Out-of-Box Experience (OOBE)**i upewnij się, że **Generalize** pole wyboru jest zaznaczone.</span><span class="sxs-lookup"><span data-stu-id="d59a3-126">In the **System Preparation Tool** dialog box, select **Enter System Out-of-Box Experience (OOBE)**, and make sure that the **Generalize** check box is selected.</span></span>
4. <span data-ttu-id="d59a3-127">W **opcje zamykania**, wybierz pozycję **zamknięcia**.</span><span class="sxs-lookup"><span data-stu-id="d59a3-127">In **Shutdown Options**, select **Shutdown**.</span></span>
5. <span data-ttu-id="d59a3-128">Kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="d59a3-128">Click **OK**.</span></span>
   
    ![Uruchom program Sysprep](./media/upload-generalized-managed/sysprepgeneral.png)
6. <span data-ttu-id="d59a3-130">Po zakończeniu działania programu Sysprep, zamyka maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="d59a3-130">When Sysprep completes, it shuts down the virtual machine.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="d59a3-131">Nie uruchamiaj ponownie maszynę Wirtualną, aż wszystko będzie gotowe, przekazywanie wirtualnego dysku twardego na platformie Azure lub Tworzenie obrazu z maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="d59a3-131">Do not restart the VM until you are done uploading the VHD to Azure or creating an image from the VM.</span></span> <span data-ttu-id="d59a3-132">Gdy maszyna wirtualna przypadkowo pobiera ponownie uruchomione, uruchom program Sysprep do uogólnienia go ponownie.</span><span class="sxs-lookup"><span data-stu-id="d59a3-132">If the VM accidentally gets restarted, run Sysprep to generalize it again.</span></span>
> 
> 

## <a name="log-in-to-azure-powershell"></a><span data-ttu-id="d59a3-133">Zaloguj się do programu Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="d59a3-133">Log in to Azure PowerShell</span></span>
1. <span data-ttu-id="d59a3-134">Otwórz program Azure PowerShell i zaloguj się do konta platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="d59a3-134">Open Azure PowerShell and sign in to your Azure account.</span></span>
   
    ```powershell
    Login-AzureRmAccount
    ```
   
    <span data-ttu-id="d59a3-135">Otwiera okno podręczne wprowadzenie poświadczeń konta platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="d59a3-135">A pop-up window opens for you to enter your Azure account credentials.</span></span>
2. <span data-ttu-id="d59a3-136">Pobierz identyfikatory subskrypcji dla dostępnych subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="d59a3-136">Get the subscription IDs for your available subscriptions.</span></span>
   
    ```powershell
    Get-AzureRmSubscription
    ```
3. <span data-ttu-id="d59a3-137">Ustaw poprawną subskrypcję za pomocą identyfikatora subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="d59a3-137">Set the correct subscription using the subscription ID.</span></span>
   
    ```powershell
    Select-AzureRmSubscription -SubscriptionId "<subscriptionID>"
    ```

## <a name="deallocate-the-vm-and-set-the-state-to-generalized"></a><span data-ttu-id="d59a3-138">Cofnięcie przydziału maszyny Wirtualnej i ustawić stan na uogólniony</span><span class="sxs-lookup"><span data-stu-id="d59a3-138">Deallocate the VM and set the state to generalized</span></span>
1. <span data-ttu-id="d59a3-139">Cofnięcie przydziału zasobów maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="d59a3-139">Deallocate the VM resources.</span></span>
   
    ```powershell
    Stop-AzureRmVM -ResourceGroupName <resourceGroup> -Name <vmName>
    ```
   
    <span data-ttu-id="d59a3-140">*Stan* dla maszyny Wirtualnej na platformie Azure portal zmieni się z **zatrzymane** do **zatrzymane (cofnięciu przydziału)**.</span><span class="sxs-lookup"><span data-stu-id="d59a3-140">The *Status* for the VM in the Azure portal changes from **Stopped** to **Stopped (deallocated)**.</span></span>
2. <span data-ttu-id="d59a3-141">Ustaw stan maszyny wirtualnej na **Uogólniono**.</span><span class="sxs-lookup"><span data-stu-id="d59a3-141">Set the status of the virtual machine to **Generalized**.</span></span> 
   
    ```powershell
    Set-AzureRmVm -ResourceGroupName <resourceGroup> -Name <vmName> -Generalized
    ```
3. <span data-ttu-id="d59a3-142">Sprawdź stan maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="d59a3-142">Check the status of the VM.</span></span> <span data-ttu-id="d59a3-143">**OSState/uogólniony** sekcji dla maszyny Wirtualnej powinny mieć **DisplayStatus** ustawioną **uogólniona maszyna wirtualna**.</span><span class="sxs-lookup"><span data-stu-id="d59a3-143">The **OSState/generalized** section for the VM should have the **DisplayStatus** set to **VM generalized**.</span></span>  
   
    ```powershell
    $vm = Get-AzureRmVM -ResourceGroupName <resourceGroup> -Name <vmName> -Status
    $vm.Statuses
    ```

## <a name="create-the-image"></a><span data-ttu-id="d59a3-144">Tworzenie obrazu</span><span class="sxs-lookup"><span data-stu-id="d59a3-144">Create the image</span></span>

<span data-ttu-id="d59a3-145">Tworzenie obrazu niezarządzane maszyny wirtualnej w docelowy kontener magazynu przy użyciu tego polecenia.</span><span class="sxs-lookup"><span data-stu-id="d59a3-145">Create an unmanaged virtual machine image in the destination storage container using this command.</span></span> <span data-ttu-id="d59a3-146">Obraz jest tworzony w tym samym kontem magazynu oryginalna maszyna wirtualna.</span><span class="sxs-lookup"><span data-stu-id="d59a3-146">The image is created in the same storage account as the original virtual machine.</span></span> <span data-ttu-id="d59a3-147">`-Path` Parametr zapisuje kopię szablonu JSON dla źródłowej maszyny Wirtualnej na komputerze lokalnym.</span><span class="sxs-lookup"><span data-stu-id="d59a3-147">The `-Path` parameter saves a copy of the JSON template for the source VM to your local computer.</span></span> <span data-ttu-id="d59a3-148">`-DestinationContainerName` Parametru jest nazwa kontenera, w którym chcesz przechowywać obrazów.</span><span class="sxs-lookup"><span data-stu-id="d59a3-148">The `-DestinationContainerName` parameter is the name of the container that you want to hold your images.</span></span> <span data-ttu-id="d59a3-149">Jeśli kontener nie istnieje, jest tworzony automatycznie.</span><span class="sxs-lookup"><span data-stu-id="d59a3-149">If the container doesn't exist, it is created for you.</span></span>
   
```powershell
Save-AzureRmVMImage -ResourceGroupName <resourceGroupName> -Name <vmName> `
    -DestinationContainerName <destinationContainerName> -VHDNamePrefix <templateNamePrefix> `
    -Path <C:\local\Filepath\Filename.json>
```
   
<span data-ttu-id="d59a3-150">Możesz uzyskać adres URL obrazu z szablonu pliku JSON.</span><span class="sxs-lookup"><span data-stu-id="d59a3-150">You can get the URL of your image from the JSON file template.</span></span> <span data-ttu-id="d59a3-151">Przejdź do **zasobów** > **storageProfile** > **osDisk** > **obrazu**  >  **uri** sekcji pełną ścieżkę obrazu.</span><span class="sxs-lookup"><span data-stu-id="d59a3-151">Go to the **resources** > **storageProfile** > **osDisk** > **image** > **uri** section for the complete path of your image.</span></span> <span data-ttu-id="d59a3-152">Adres URL obrazu, wygląda następująco: `https://<storageAccountName>.blob.core.windows.net/system/Microsoft.Compute/Images/<imagesContainer>/<templatePrefix-osDisk>.xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx.vhd`.</span><span class="sxs-lookup"><span data-stu-id="d59a3-152">The URL of the image looks like: `https://<storageAccountName>.blob.core.windows.net/system/Microsoft.Compute/Images/<imagesContainer>/<templatePrefix-osDisk>.xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx.vhd`.</span></span>
   
<span data-ttu-id="d59a3-153">Można również sprawdzić identyfikatora URI w portalu.</span><span class="sxs-lookup"><span data-stu-id="d59a3-153">You can also verify the URI in the portal.</span></span> <span data-ttu-id="d59a3-154">Obraz jest kopiowany do kontenera o nazwie **systemu** na koncie magazynu.</span><span class="sxs-lookup"><span data-stu-id="d59a3-154">The image is copied to a container named **system** in your storage account.</span></span> 

## <a name="create-a-vm-from-the-image"></a><span data-ttu-id="d59a3-155">Utwórz maszynę Wirtualną z obrazu</span><span class="sxs-lookup"><span data-stu-id="d59a3-155">Create a VM from the image</span></span>

<span data-ttu-id="d59a3-156">Teraz możesz utworzyć przynajmniej jednej maszyny wirtualnej z obrazu niezarządzane.</span><span class="sxs-lookup"><span data-stu-id="d59a3-156">Now you can create one or more VMs from the unmanaged image.</span></span>

### <a name="set-the-uri-of-the-vhd"></a><span data-ttu-id="d59a3-157">Ustaw identyfikator URI dysku VHD</span><span class="sxs-lookup"><span data-stu-id="d59a3-157">Set the URI of the VHD</span></span>

<span data-ttu-id="d59a3-158">Identyfikator URI dysku VHD do użycia ma format: https://**mojekontomagazynu**.blob.core.windows.net/**mojkontener**/**MyVhdName**VHD.</span><span class="sxs-lookup"><span data-stu-id="d59a3-158">The URI for the VHD to use is in the format: https://**mystorageaccount**.blob.core.windows.net/**mycontainer**/**MyVhdName**.vhd.</span></span> <span data-ttu-id="d59a3-159">W tym przykładzie wirtualnego dysku twardego o nazwie **myVHD** jest na koncie magazynu **mojekontomagazynu** w kontenerze **mojkontener**.</span><span class="sxs-lookup"><span data-stu-id="d59a3-159">In this example the VHD named **myVHD** is in the storage account **mystorageaccount** in the container **mycontainer**.</span></span>

```powershell
$imageURI = "https://mystorageaccount.blob.core.windows.net/mycontainer/myVhd.vhd"
```


### <a name="create-a-virtual-network"></a><span data-ttu-id="d59a3-160">Tworzenie sieci wirtualnej</span><span class="sxs-lookup"><span data-stu-id="d59a3-160">Create a virtual network</span></span>
<span data-ttu-id="d59a3-161">Utwórz sieć wirtualną i podsieć [sieci wirtualnej](../../virtual-network/virtual-networks-overview.md).</span><span class="sxs-lookup"><span data-stu-id="d59a3-161">Create the vNet and subnet of the [virtual network](../../virtual-network/virtual-networks-overview.md).</span></span>

1. <span data-ttu-id="d59a3-162">Utwórz podsieć.</span><span class="sxs-lookup"><span data-stu-id="d59a3-162">Create the subnet.</span></span> <span data-ttu-id="d59a3-163">W poniższym przykładzie tworzone podsieci o nazwie **mySubnet** w grupie zasobów **myResourceGroup** z prefiksem adresu o **10.0.0.0/24**.</span><span class="sxs-lookup"><span data-stu-id="d59a3-163">The following sample creates a subnet named **mySubnet** in the resource group **myResourceGroup** with the address prefix of **10.0.0.0/24**.</span></span>  
   
    ```powershell
    $rgName = "myResourceGroup"
    $subnetName = "mySubnet"
    $singleSubnet = New-AzureRmVirtualNetworkSubnetConfig -Name $subnetName -AddressPrefix 10.0.0.0/24
    ```
2. <span data-ttu-id="d59a3-164">Utwórz sieć wirtualną.</span><span class="sxs-lookup"><span data-stu-id="d59a3-164">Create the virtual network.</span></span> <span data-ttu-id="d59a3-165">Poniższy przykład tworzy sieć wirtualną o nazwie **myVnet** w **zachodnie stany USA** lokalizacji z prefiksem adresu o **10.0.0.0/16**.</span><span class="sxs-lookup"><span data-stu-id="d59a3-165">The following sample creates a virtual network named **myVnet** in the **West US** location with the address prefix of **10.0.0.0/16**.</span></span>  
   
    ```powershell
    $location = "West US"
    $vnetName = "myVnet"
    $vnet = New-AzureRmVirtualNetwork -Name $vnetName -ResourceGroupName $rgName -Location $location `
        -AddressPrefix 10.0.0.0/16 -Subnet $singleSubnet
    ```    

### <a name="create-a-public-ip-address-and-network-interface"></a><span data-ttu-id="d59a3-166">Tworzenie publicznego adresu IP adres i interfejsu sieciowego</span><span class="sxs-lookup"><span data-stu-id="d59a3-166">Create a public IP address and network interface</span></span>
<span data-ttu-id="d59a3-167">Aby umożliwić komunikację z maszyną wirtualną w sieci wirtualnej, potrzebujesz [publicznego adresu IP](../../virtual-network/virtual-network-ip-addresses-overview-arm.md) i interfejsu sieciowego.</span><span class="sxs-lookup"><span data-stu-id="d59a3-167">To enable communication with the virtual machine in the virtual network, you need a [public IP address](../../virtual-network/virtual-network-ip-addresses-overview-arm.md) and a network interface.</span></span>

1. <span data-ttu-id="d59a3-168">Utwórz publiczny adres IP.</span><span class="sxs-lookup"><span data-stu-id="d59a3-168">Create a public IP address.</span></span> <span data-ttu-id="d59a3-169">W tym przykładzie jest tworzony publiczny adres IP o nazwie **myPip**.</span><span class="sxs-lookup"><span data-stu-id="d59a3-169">This example creates a public IP address named **myPip**.</span></span> 
   
    ```powershell
    $ipName = "myPip"
    $pip = New-AzureRmPublicIpAddress -Name $ipName -ResourceGroupName $rgName -Location $location `
        -AllocationMethod Dynamic
    ```       
2. <span data-ttu-id="d59a3-170">Utwórz kartę sieciową.</span><span class="sxs-lookup"><span data-stu-id="d59a3-170">Create the NIC.</span></span> <span data-ttu-id="d59a3-171">W tym przykładzie jest tworzony karty Sieciowej o nazwie **myNic**.</span><span class="sxs-lookup"><span data-stu-id="d59a3-171">This example creates a NIC named **myNic**.</span></span> 
   
    ```powershell
    $nicName = "myNic"
    $nic = New-AzureRmNetworkInterface -Name $nicName -ResourceGroupName $rgName -Location $location `
        -SubnetId $vnet.Subnets[0].Id -PublicIpAddressId $pip.Id
    ```

### <a name="create-the-network-security-group-and-an-rdp-rule"></a><span data-ttu-id="d59a3-172">Tworzenie grupy zabezpieczeń sieci i reguły protokołu RDP</span><span class="sxs-lookup"><span data-stu-id="d59a3-172">Create the network security group and an RDP rule</span></span>
<span data-ttu-id="d59a3-173">Aby móc zalogować się do maszyny Wirtualnej za pomocą protokołu RDP, musisz mieć regułę zabezpieczeń, która udziela dostępu RDP do portu 3389.</span><span class="sxs-lookup"><span data-stu-id="d59a3-173">To be able to log in to your VM using RDP, you need to have a security rule that allows RDP access on port 3389.</span></span> 

<span data-ttu-id="d59a3-174">W tym przykładzie tworzy grupy NSG o nazwie **myNsg** zawierający regułę o nazwie **myRdpRule** za pośrednictwem portu 3389 która zezwala na ruch RDP.</span><span class="sxs-lookup"><span data-stu-id="d59a3-174">This example creates an NSG named **myNsg** that contains a rule called **myRdpRule** that allows RDP traffic over port 3389.</span></span> <span data-ttu-id="d59a3-175">Aby uzyskać więcej informacji na temat grup NSG, zobacz [Otwieranie portów dla maszyny Wirtualnej na platformie Azure przy użyciu programu PowerShell](nsg-quickstart-powershell.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="d59a3-175">For more information about NSGs, see [Opening ports to a VM in Azure using PowerShell](nsg-quickstart-powershell.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

```powershell
$nsgName = "myNsg"

$rdpRule = New-AzureRmNetworkSecurityRuleConfig -Name myRdpRule -Description "Allow RDP" `
    -Access Allow -Protocol Tcp -Direction Inbound -Priority 110 `
    -SourceAddressPrefix Internet -SourcePortRange * `
    -DestinationAddressPrefix * -DestinationPortRange 3389

$nsg = New-AzureRmNetworkSecurityGroup -ResourceGroupName $rgName -Location $location `
    -Name $nsgName -SecurityRules $rdpRule
```


### <a name="create-a-variable-for-the-virtual-network"></a><span data-ttu-id="d59a3-176">Utwórz zmienną dla sieci wirtualnej</span><span class="sxs-lookup"><span data-stu-id="d59a3-176">Create a variable for the virtual network</span></span>
<span data-ttu-id="d59a3-177">Utwórz zmienną dla ukończonych sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="d59a3-177">Create a variable for the completed virtual network.</span></span> 

```powershell
$vnet = Get-AzureRmVirtualNetwork -ResourceGroupName $rgName -Name $vnetName
```

### <a name="create-the-vm"></a><span data-ttu-id="d59a3-178">Tworzenie maszyny wirtualnej</span><span class="sxs-lookup"><span data-stu-id="d59a3-178">Create the VM</span></span>
<span data-ttu-id="d59a3-179">Następujące środowiska PowerShell kończy konfiguracji maszyn wirtualnych i używa niezarządzanej obrazu jako źródło dla nowej instalacji.</span><span class="sxs-lookup"><span data-stu-id="d59a3-179">The following PowerShell completes the virtual machine configurations and uses unmanaged image as the source for the new installation.</span></span>

</br>

```powershell
    # Enter a new user name and password to use as the local administrator account 
    # for remotely accessing the VM.
    $cred = Get-Credential

    # Name of the storage account where the VHD is located. This example sets the 
    # storage account name as "myStorageAccount"
    $storageAccName = "myStorageAccount"

    # Name of the virtual machine. This example sets the VM name as "myVM".
    $vmName = "myVM"

    # Size of the virtual machine. This example creates "Standard_D2_v2" sized VM. 
    # See the VM sizes documentation for more information: 
    # https://azure.microsoft.com/documentation/articles/virtual-machines-windows-sizes/
    $vmSize = "Standard_D2_v2"

    # Computer name for the VM. This examples sets the computer name as "myComputer".
    $computerName = "myComputer"

    # Name of the disk that holds the OS. This example sets the 
    # OS disk name as "myOsDisk"
    $osDiskName = "myOsDisk"

    # Assign a SKU name. This example sets the SKU name as "Standard_LRS"
    # Valid values for -SkuName are: Standard_LRS - locally redundant storage, Standard_ZRS - zone redundant
    # storage, Standard_GRS - geo redundant storage, Standard_RAGRS - read access geo redundant storage,
    # Premium_LRS - premium locally redundant storage. 
    $skuName = "Standard_LRS"

    # Get the storage account where the uploaded image is stored
    $storageAcc = Get-AzureRmStorageAccount -ResourceGroupName $rgName -AccountName $storageAccName

    # Set the VM name and size
    $vmConfig = New-AzureRmVMConfig -VMName $vmName -VMSize $vmSize

    #Set the Windows operating system configuration and add the NIC
    $vm = Set-AzureRmVMOperatingSystem -VM $vmConfig -Windows -ComputerName $computerName `
        -Credential $cred -ProvisionVMAgent -EnableAutoUpdate
    $vm = Add-AzureRmVMNetworkInterface -VM $vm -Id $nic.Id

    # Create the OS disk URI
    $osDiskUri = '{0}vhds/{1}-{2}.vhd' `
        -f $storageAcc.PrimaryEndpoints.Blob.ToString(), $vmName.ToLower(), $osDiskName

    # Configure the OS disk to be created from the existing VHD image (-CreateOption fromImage).
    $vm = Set-AzureRmVMOSDisk -VM $vm -Name $osDiskName -VhdUri $osDiskUri `
        -CreateOption fromImage -SourceImageUri $imageURI -Windows

    # Create the new VM
    New-AzureRmVM -ResourceGroupName $rgName -Location $location -VM $vm
```

### <a name="verify-that-the-vm-was-created"></a><span data-ttu-id="d59a3-180">Sprawdź, czy maszyna wirtualna została utworzona</span><span class="sxs-lookup"><span data-stu-id="d59a3-180">Verify that the VM was created</span></span>
<span data-ttu-id="d59a3-181">Po zakończeniu powinien zostać wyświetlony nowo utworzony maszyny Wirtualnej w ramach [portalu Azure](https://portal.azure.com) w obszarze **Przeglądaj** > **maszyn wirtualnych**, lub za pomocą następujących poleceń programu PowerShell:</span><span class="sxs-lookup"><span data-stu-id="d59a3-181">When complete, you should see the newly created VM in the [Azure portal](https://portal.azure.com) under **Browse** > **Virtual machines**, or by using the following PowerShell commands:</span></span>

```powershell
    $vmList = Get-AzureRmVM -ResourceGroupName $rgName
    $vmList.Name
```

## <a name="next-steps"></a><span data-ttu-id="d59a3-182">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="d59a3-182">Next steps</span></span>
<span data-ttu-id="d59a3-183">Aby zarządzać nową maszynę wirtualną w taki sposób, z programu Azure PowerShell, zobacz [zarządzania maszynami wirtualnymi przy użyciu usługi Azure Resource Manager i programu PowerShell](tutorial-manage-vm.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="d59a3-183">To manage your new virtual machine with Azure PowerShell, see [Manage virtual machines using Azure Resource Manager and PowerShell](tutorial-manage-vm.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>


