---
title: "aaaCreate niezarządzane obraz uogólniony maszyny wirtualnej na platformie Azure | Dokumentacja firmy Microsoft"
description: "Utwórz obraz unmanged uogólniony toocreate toouse maszyny Wirtualnej systemu Windows wiele kopii maszyny wirtualnej na platformie Azure."
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
ms.openlocfilehash: b8a044d20313efa6dd9b9757e61154f922134476
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocreate-an-unmanaged-vm-image-from-an-azure-vm"></a><span data-ttu-id="3e42f-103">Jak obraz toocreate niezarządzane maszyny Wirtualnej z maszyny Wirtualnej platformy Azure</span><span class="sxs-lookup"><span data-stu-id="3e42f-103">How toocreate an unmanaged VM image from an Azure VM</span></span>

<span data-ttu-id="3e42f-104">W tym artykule omówiono używanie kont magazynu.</span><span class="sxs-lookup"><span data-stu-id="3e42f-104">This article covers using storage accounts.</span></span> <span data-ttu-id="3e42f-105">Zalecane jest użycie dysków zarządzanych i zarządzanych obrazów zamiast konta magazynu.</span><span class="sxs-lookup"><span data-stu-id="3e42f-105">We recommend that you use managed disks and managed images instead of a storage account.</span></span> <span data-ttu-id="3e42f-106">Aby uzyskać więcej informacji, zobacz [Przechwyć obraz zarządzanych uogólniony maszyny wirtualnej na platformie Azure](capture-image-resource.md).</span><span class="sxs-lookup"><span data-stu-id="3e42f-106">For more information, see [Capture a managed image of a generalized VM in Azure](capture-image-resource.md).</span></span>

<span data-ttu-id="3e42f-107">W tym artykule opisano sposób toouse programu Azure PowerShell toocreate obraz uogólniony maszyny Wirtualnej platformy Azure przy użyciu konta magazynu.</span><span class="sxs-lookup"><span data-stu-id="3e42f-107">This article shows you how toouse Azure PowerShell toocreate an image of a generalized Azure VM using a storage account.</span></span> <span data-ttu-id="3e42f-108">Następnie można toocreate obraz powitania inną maszynę Wirtualną.</span><span class="sxs-lookup"><span data-stu-id="3e42f-108">You can then use hello image toocreate another VM.</span></span> <span data-ttu-id="3e42f-109">Obraz powitania obejmuje hello dysk systemu operacyjnego i dysków danych hello, które są dołączone toohello maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="3e42f-109">hello image includes hello OS disk and hello data disks that are attached toohello virtual machine.</span></span> <span data-ttu-id="3e42f-110">Obraz powitania nie zawiera zasobów sieci wirtualnej hello, więc należy tooset tych zasobów, podczas tworzenia nowej maszyny Wirtualnej hello.</span><span class="sxs-lookup"><span data-stu-id="3e42f-110">hello image doesn't include hello virtual network resources, so you need tooset up those resources when you create hello new VM.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="3e42f-111">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="3e42f-111">Prerequisites</span></span>
<span data-ttu-id="3e42f-112">Wymagana wersja programu Azure PowerShell toohave 1.0.x lub nowszej.</span><span class="sxs-lookup"><span data-stu-id="3e42f-112">You need toohave Azure PowerShell version 1.0.x or newer installed.</span></span> <span data-ttu-id="3e42f-113">Jeśli jeszcze nie zainstalowano programu PowerShell, przeczytaj [jak tooinstall i konfigurowanie programu Azure PowerShell](/powershell/azure/overview) kroki instalacji.</span><span class="sxs-lookup"><span data-stu-id="3e42f-113">If you haven't already installed PowerShell, read [How tooinstall and configure Azure PowerShell](/powershell/azure/overview) for installation steps.</span></span>

## <a name="generalize-hello-vm"></a><span data-ttu-id="3e42f-114">Generalize hello maszyny Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="3e42f-114">Generalize hello VM</span></span> 
<span data-ttu-id="3e42f-115">W tej sekcji opisano sposób toogeneralize maszyny wirtualnej systemu Windows do użycia jako obraz.</span><span class="sxs-lookup"><span data-stu-id="3e42f-115">This section shows you how toogeneralize your Windows virtual machine for use as an image.</span></span> <span data-ttu-id="3e42f-116">Uogólnianie maszyny Wirtualnej powoduje usunięcie wszystkich informacji osobowych konta, między innymi i przygotowuje toobe maszyny hello użyty jako obraz.</span><span class="sxs-lookup"><span data-stu-id="3e42f-116">Generalizing a VM removes all your personal account information, among other things, and prepares hello machine toobe used as an image.</span></span> <span data-ttu-id="3e42f-117">Aby uzyskać więcej informacji o narzędziu Sysprep, zobacz [jak tooUse Sysprep: wprowadzenie](http://technet.microsoft.com/library/bb457073.aspx).</span><span class="sxs-lookup"><span data-stu-id="3e42f-117">For details about Sysprep, see [How tooUse Sysprep: An Introduction](http://technet.microsoft.com/library/bb457073.aspx).</span></span>

<span data-ttu-id="3e42f-118">Upewnij się, że hello ról serwera uruchomionych na maszynie hello są obsługiwane przez program Sysprep.</span><span class="sxs-lookup"><span data-stu-id="3e42f-118">Make sure hello server roles running on hello machine are supported by Sysprep.</span></span> <span data-ttu-id="3e42f-119">Aby uzyskać więcej informacji, zobacz [Obsługa programu Sysprep dla ról serwera](https://msdn.microsoft.com/windows/hardware/commercialize/manufacture/desktop/sysprep-support-for-server-roles)</span><span class="sxs-lookup"><span data-stu-id="3e42f-119">For more information, see [Sysprep Support for Server Roles](https://msdn.microsoft.com/windows/hardware/commercialize/manufacture/desktop/sysprep-support-for-server-roles)</span></span>

> [!IMPORTANT]
> <span data-ttu-id="3e42f-120">Podczas przekazywania tooAzure Twojego dysku VHD na powitania po raz pierwszy, upewnij się, masz [przygotować maszyny Wirtualnej](prepare-for-upload-vhd-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) przed uruchomieniem programu Sysprep.</span><span class="sxs-lookup"><span data-stu-id="3e42f-120">If you are uploading your VHD tooAzure for hello first time, make sure you have [prepared your VM](prepare-for-upload-vhd-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) before running Sysprep.</span></span> 
> 
> 

<span data-ttu-id="3e42f-121">Można również generalize maszyny Wirtualnej systemu Linux przy użyciu `sudo waagent -deprovision+user` , a następnie użyj programu PowerShell toocapture hello maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="3e42f-121">You can also generalize a Linux VM using `sudo waagent -deprovision+user` and then use PowerShell toocapture hello VM.</span></span> <span data-ttu-id="3e42f-122">Aby dowiedzieć się, jak przy użyciu hello CLI toocapture maszyny Wirtualnej, zobacz [jak toogeneralize i przechwycenia maszyny wirtualnej systemu Linux przy użyciu interfejsu wiersza polecenia Azure hello ](../linux/capture-image.md).</span><span class="sxs-lookup"><span data-stu-id="3e42f-122">For information about using hello CLI toocapture a VM, see [How toogeneralize and capture a Linux virtual machine using hello Azure CLI ](../linux/capture-image.md).</span></span>


1. <span data-ttu-id="3e42f-123">Zaloguj się toohello maszyny wirtualnej systemu Windows.</span><span class="sxs-lookup"><span data-stu-id="3e42f-123">Sign in toohello Windows virtual machine.</span></span>
2. <span data-ttu-id="3e42f-124">Otwórz okno wiersza polecenia hello jako administrator.</span><span class="sxs-lookup"><span data-stu-id="3e42f-124">Open hello Command Prompt window as an administrator.</span></span> <span data-ttu-id="3e42f-125">Zmień katalog hello zbyt**%windir%\system32\sysprep**, a następnie uruchom `sysprep.exe`.</span><span class="sxs-lookup"><span data-stu-id="3e42f-125">Change hello directory too**%windir%\system32\sysprep**, and then run `sysprep.exe`.</span></span>
3. <span data-ttu-id="3e42f-126">W hello **narzędzie przygotowania systemu** okno dialogowe, wybierz opcję **wprowadź systemu Out-of-Box Experience (OOBE)**i upewnij się, że hello **Generalize** pole wyboru jest zaznaczone.</span><span class="sxs-lookup"><span data-stu-id="3e42f-126">In hello **System Preparation Tool** dialog box, select **Enter System Out-of-Box Experience (OOBE)**, and make sure that hello **Generalize** check box is selected.</span></span>
4. <span data-ttu-id="3e42f-127">W **opcje zamykania**, wybierz pozycję **zamknięcia**.</span><span class="sxs-lookup"><span data-stu-id="3e42f-127">In **Shutdown Options**, select **Shutdown**.</span></span>
5. <span data-ttu-id="3e42f-128">Kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="3e42f-128">Click **OK**.</span></span>
   
    ![Uruchom program Sysprep](./media/upload-generalized-managed/sysprepgeneral.png)
6. <span data-ttu-id="3e42f-130">Po zakończeniu działania programu Sysprep, zamyka hello maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="3e42f-130">When Sysprep completes, it shuts down hello virtual machine.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="3e42f-131">Nie uruchamiaj ponownie hello maszyny Wirtualnej, dopóki nie są gotowe, przesyłania tooAzure wirtualnego dysku twardego hello lub Tworzenie obrazu z hello maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="3e42f-131">Do not restart hello VM until you are done uploading hello VHD tooAzure or creating an image from hello VM.</span></span> <span data-ttu-id="3e42f-132">Jeśli hello wirtualna przypadkowo pobiera ponownie uruchomione, uruchom Sysprep toogeneralize go ponownie.</span><span class="sxs-lookup"><span data-stu-id="3e42f-132">If hello VM accidentally gets restarted, run Sysprep toogeneralize it again.</span></span>
> 
> 

## <a name="log-in-tooazure-powershell"></a><span data-ttu-id="3e42f-133">Zaloguj się za tooAzure programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="3e42f-133">Log in tooAzure PowerShell</span></span>
1. <span data-ttu-id="3e42f-134">Otwórz program Azure PowerShell i zaloguj się na tooyour konto platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="3e42f-134">Open Azure PowerShell and sign in tooyour Azure account.</span></span>
   
    ```powershell
    Login-AzureRmAccount
    ```
   
    <span data-ttu-id="3e42f-135">Zostanie otwarte okno podręczne dla tooenter możesz poświadczenia konta Azure.</span><span class="sxs-lookup"><span data-stu-id="3e42f-135">A pop-up window opens for you tooenter your Azure account credentials.</span></span>
2. <span data-ttu-id="3e42f-136">Uzyskanie subskrypcji hello identyfikatorów subskrypcji dostępne.</span><span class="sxs-lookup"><span data-stu-id="3e42f-136">Get hello subscription IDs for your available subscriptions.</span></span>
   
    ```powershell
    Get-AzureRmSubscription
    ```
3. <span data-ttu-id="3e42f-137">Ustaw poprawną subskrypcję hello przy użyciu identyfikatora hello subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="3e42f-137">Set hello correct subscription using hello subscription ID.</span></span>
   
    ```powershell
    Select-AzureRmSubscription -SubscriptionId "<subscriptionID>"
    ```

## <a name="deallocate-hello-vm-and-set-hello-state-toogeneralized"></a><span data-ttu-id="3e42f-138">Cofnięcie przydziału hello maszyny Wirtualnej i ustaw hello toogeneralized stanu</span><span class="sxs-lookup"><span data-stu-id="3e42f-138">Deallocate hello VM and set hello state toogeneralized</span></span>
1. <span data-ttu-id="3e42f-139">Cofnięcie przydziału hello zasobów maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="3e42f-139">Deallocate hello VM resources.</span></span>
   
    ```powershell
    Stop-AzureRmVM -ResourceGroupName <resourceGroup> -Name <vmName>
    ```
   
    <span data-ttu-id="3e42f-140">Witaj *stan* dla hello maszyny Wirtualnej w hello Azure portal zmieni się z **zatrzymane** za**zatrzymane (cofnięciu przydziału)**.</span><span class="sxs-lookup"><span data-stu-id="3e42f-140">hello *Status* for hello VM in hello Azure portal changes from **Stopped** too**Stopped (deallocated)**.</span></span>
2. <span data-ttu-id="3e42f-141">Ustaw stan hello hello maszyny wirtualnej za**Uogólniono**.</span><span class="sxs-lookup"><span data-stu-id="3e42f-141">Set hello status of hello virtual machine too**Generalized**.</span></span> 
   
    ```powershell
    Set-AzureRmVm -ResourceGroupName <resourceGroup> -Name <vmName> -Generalized
    ```
3. <span data-ttu-id="3e42f-142">Sprawdź stan hello hello maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="3e42f-142">Check hello status of hello VM.</span></span> <span data-ttu-id="3e42f-143">Witaj **OSState/uogólniony** sekcji hello maszyny Wirtualnej powinny mieć hello **DisplayStatus** ustawić także**uogólniona maszyna wirtualna**.</span><span class="sxs-lookup"><span data-stu-id="3e42f-143">hello **OSState/generalized** section for hello VM should have hello **DisplayStatus** set too**VM generalized**.</span></span>  
   
    ```powershell
    $vm = Get-AzureRmVM -ResourceGroupName <resourceGroup> -Name <vmName> -Status
    $vm.Statuses
    ```

## <a name="create-hello-image"></a><span data-ttu-id="3e42f-144">Utworzyć obraz powitania</span><span class="sxs-lookup"><span data-stu-id="3e42f-144">Create hello image</span></span>

<span data-ttu-id="3e42f-145">Tworzenie obrazu niezarządzane maszyny wirtualnej w hello docelowy kontener magazynu przy użyciu tego polecenia.</span><span class="sxs-lookup"><span data-stu-id="3e42f-145">Create an unmanaged virtual machine image in hello destination storage container using this command.</span></span> <span data-ttu-id="3e42f-146">Witaj obrazu jest tworzony w hello same konta magazynu, ponieważ hello oryginalna maszyna wirtualna.</span><span class="sxs-lookup"><span data-stu-id="3e42f-146">hello image is created in hello same storage account as hello original virtual machine.</span></span> <span data-ttu-id="3e42f-147">Witaj `-Path` parametr zapisuje kopię szablonu JSON hello na komputerze lokalnym tooyour hello źródłowej maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="3e42f-147">hello `-Path` parameter saves a copy of hello JSON template for hello source VM tooyour local computer.</span></span> <span data-ttu-id="3e42f-148">Witaj `-DestinationContainerName` parametru jest nazwa hello kontenera hello mają toohold obrazów.</span><span class="sxs-lookup"><span data-stu-id="3e42f-148">hello `-DestinationContainerName` parameter is hello name of hello container that you want toohold your images.</span></span> <span data-ttu-id="3e42f-149">Jeśli hello kontener nie istnieje, jest tworzony automatycznie.</span><span class="sxs-lookup"><span data-stu-id="3e42f-149">If hello container doesn't exist, it is created for you.</span></span>
   
```powershell
Save-AzureRmVMImage -ResourceGroupName <resourceGroupName> -Name <vmName> `
    -DestinationContainerName <destinationContainerName> -VHDNamePrefix <templateNamePrefix> `
    -Path <C:\local\Filepath\Filename.json>
```
   
<span data-ttu-id="3e42f-150">Możesz pobrać ze strony szablonu pliku JSON hello hello adres URL obrazu.</span><span class="sxs-lookup"><span data-stu-id="3e42f-150">You can get hello URL of your image from hello JSON file template.</span></span> <span data-ttu-id="3e42f-151">Przejdź toohello **zasobów** > **storageProfile** > **osDisk** > **obrazu**  >  **uri** sekcji hello pełną ścieżkę obrazu.</span><span class="sxs-lookup"><span data-stu-id="3e42f-151">Go toohello **resources** > **storageProfile** > **osDisk** > **image** > **uri** section for hello complete path of your image.</span></span> <span data-ttu-id="3e42f-152">adres URL obrazu, hello Hello wygląda następująco: `https://<storageAccountName>.blob.core.windows.net/system/Microsoft.Compute/Images/<imagesContainer>/<templatePrefix-osDisk>.xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx.vhd`.</span><span class="sxs-lookup"><span data-stu-id="3e42f-152">hello URL of hello image looks like: `https://<storageAccountName>.blob.core.windows.net/system/Microsoft.Compute/Images/<imagesContainer>/<templatePrefix-osDisk>.xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx.vhd`.</span></span>
   
<span data-ttu-id="3e42f-153">Można również sprawdzić hello identyfikatora URI w portalu hello.</span><span class="sxs-lookup"><span data-stu-id="3e42f-153">You can also verify hello URI in hello portal.</span></span> <span data-ttu-id="3e42f-154">Obraz powitania jest skopiowany tooa kontener o nazwie **systemu** na koncie magazynu.</span><span class="sxs-lookup"><span data-stu-id="3e42f-154">hello image is copied tooa container named **system** in your storage account.</span></span> 

## <a name="create-a-vm-from-hello-image"></a><span data-ttu-id="3e42f-155">Utwórz maszynę Wirtualną z obrazu hello</span><span class="sxs-lookup"><span data-stu-id="3e42f-155">Create a VM from hello image</span></span>

<span data-ttu-id="3e42f-156">Teraz możesz utworzyć przynajmniej jednej maszyny wirtualnej z obrazu niezarządzane hello.</span><span class="sxs-lookup"><span data-stu-id="3e42f-156">Now you can create one or more VMs from hello unmanaged image.</span></span>

### <a name="set-hello-uri-of-hello-vhd"></a><span data-ttu-id="3e42f-157">Ustaw hello URI hello wirtualnego dysku twardego</span><span class="sxs-lookup"><span data-stu-id="3e42f-157">Set hello URI of hello VHD</span></span>

<span data-ttu-id="3e42f-158">Hello identyfikatora URI dla toouse wirtualnego dysku twardego hello jest w formacie hello: https://**mojekontomagazynu**.blob.core.windows.net/**mojkontener**/**MyVhdName**VHD.</span><span class="sxs-lookup"><span data-stu-id="3e42f-158">hello URI for hello VHD toouse is in hello format: https://**mystorageaccount**.blob.core.windows.net/**mycontainer**/**MyVhdName**.vhd.</span></span> <span data-ttu-id="3e42f-159">W tym przykładzie hello wirtualnego dysku twardego o nazwie **myVHD** jest na koncie magazynu hello **mojekontomagazynu** w kontenerze hello **mojkontener**.</span><span class="sxs-lookup"><span data-stu-id="3e42f-159">In this example hello VHD named **myVHD** is in hello storage account **mystorageaccount** in hello container **mycontainer**.</span></span>

```powershell
$imageURI = "https://mystorageaccount.blob.core.windows.net/mycontainer/myVhd.vhd"
```


### <a name="create-a-virtual-network"></a><span data-ttu-id="3e42f-160">Tworzenie sieci wirtualnej</span><span class="sxs-lookup"><span data-stu-id="3e42f-160">Create a virtual network</span></span>
<span data-ttu-id="3e42f-161">Tworzenie sieci wirtualnej hello i podsieci hello [sieci wirtualnej](../../virtual-network/virtual-networks-overview.md).</span><span class="sxs-lookup"><span data-stu-id="3e42f-161">Create hello vNet and subnet of hello [virtual network](../../virtual-network/virtual-networks-overview.md).</span></span>

1. <span data-ttu-id="3e42f-162">Utwórz podsieć hello.</span><span class="sxs-lookup"><span data-stu-id="3e42f-162">Create hello subnet.</span></span> <span data-ttu-id="3e42f-163">Witaj poniższy przykład tworzy podsieć o nazwie **mySubnet** w grupie zasobów hello **myResourceGroup** z prefiksu adresu hello **10.0.0.0/24**.</span><span class="sxs-lookup"><span data-stu-id="3e42f-163">hello following sample creates a subnet named **mySubnet** in hello resource group **myResourceGroup** with hello address prefix of **10.0.0.0/24**.</span></span>  
   
    ```powershell
    $rgName = "myResourceGroup"
    $subnetName = "mySubnet"
    $singleSubnet = New-AzureRmVirtualNetworkSubnetConfig -Name $subnetName -AddressPrefix 10.0.0.0/24
    ```
2. <span data-ttu-id="3e42f-164">Utwórz sieć wirtualną hello.</span><span class="sxs-lookup"><span data-stu-id="3e42f-164">Create hello virtual network.</span></span> <span data-ttu-id="3e42f-165">Witaj poniższy przykład tworzy sieć wirtualną o nazwie **myVnet** w hello **zachodnie stany USA** lokalizacji z prefiksu adresu hello **10.0.0.0/16**.</span><span class="sxs-lookup"><span data-stu-id="3e42f-165">hello following sample creates a virtual network named **myVnet** in hello **West US** location with hello address prefix of **10.0.0.0/16**.</span></span>  
   
    ```powershell
    $location = "West US"
    $vnetName = "myVnet"
    $vnet = New-AzureRmVirtualNetwork -Name $vnetName -ResourceGroupName $rgName -Location $location `
        -AddressPrefix 10.0.0.0/16 -Subnet $singleSubnet
    ```    

### <a name="create-a-public-ip-address-and-network-interface"></a><span data-ttu-id="3e42f-166">Tworzenie publicznego adresu IP adres i interfejsu sieciowego</span><span class="sxs-lookup"><span data-stu-id="3e42f-166">Create a public IP address and network interface</span></span>
<span data-ttu-id="3e42f-167">tooenable komunikację z maszyną wirtualną hello w sieci wirtualnej hello, należy [publicznego adresu IP](../../virtual-network/virtual-network-ip-addresses-overview-arm.md) i interfejsu sieciowego.</span><span class="sxs-lookup"><span data-stu-id="3e42f-167">tooenable communication with hello virtual machine in hello virtual network, you need a [public IP address](../../virtual-network/virtual-network-ip-addresses-overview-arm.md) and a network interface.</span></span>

1. <span data-ttu-id="3e42f-168">Utwórz publiczny adres IP.</span><span class="sxs-lookup"><span data-stu-id="3e42f-168">Create a public IP address.</span></span> <span data-ttu-id="3e42f-169">W tym przykładzie jest tworzony publiczny adres IP o nazwie **myPip**.</span><span class="sxs-lookup"><span data-stu-id="3e42f-169">This example creates a public IP address named **myPip**.</span></span> 
   
    ```powershell
    $ipName = "myPip"
    $pip = New-AzureRmPublicIpAddress -Name $ipName -ResourceGroupName $rgName -Location $location `
        -AllocationMethod Dynamic
    ```       
2. <span data-ttu-id="3e42f-170">Utwórz hello karty sieciowej.</span><span class="sxs-lookup"><span data-stu-id="3e42f-170">Create hello NIC.</span></span> <span data-ttu-id="3e42f-171">W tym przykładzie jest tworzony karty Sieciowej o nazwie **myNic**.</span><span class="sxs-lookup"><span data-stu-id="3e42f-171">This example creates a NIC named **myNic**.</span></span> 
   
    ```powershell
    $nicName = "myNic"
    $nic = New-AzureRmNetworkInterface -Name $nicName -ResourceGroupName $rgName -Location $location `
        -SubnetId $vnet.Subnets[0].Id -PublicIpAddressId $pip.Id
    ```

### <a name="create-hello-network-security-group-and-an-rdp-rule"></a><span data-ttu-id="3e42f-172">Tworzenie grupy zabezpieczeń sieci hello i reguły protokołu RDP</span><span class="sxs-lookup"><span data-stu-id="3e42f-172">Create hello network security group and an RDP rule</span></span>
<span data-ttu-id="3e42f-173">toobe stanie toolog w tooyour maszyny Wirtualnej przy użyciu protokołu RDP, należy toohave regułę zabezpieczeń, która udziela dostępu RDP do portu 3389.</span><span class="sxs-lookup"><span data-stu-id="3e42f-173">toobe able toolog in tooyour VM using RDP, you need toohave a security rule that allows RDP access on port 3389.</span></span> 

<span data-ttu-id="3e42f-174">W tym przykładzie tworzy grupy NSG o nazwie **myNsg** zawierający regułę o nazwie **myRdpRule** za pośrednictwem portu 3389 która zezwala na ruch RDP.</span><span class="sxs-lookup"><span data-stu-id="3e42f-174">This example creates an NSG named **myNsg** that contains a rule called **myRdpRule** that allows RDP traffic over port 3389.</span></span> <span data-ttu-id="3e42f-175">Aby uzyskać więcej informacji na temat grup NSG, zobacz [otwierania portów tooa maszyny Wirtualnej na platformie Azure przy użyciu programu PowerShell](nsg-quickstart-powershell.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="3e42f-175">For more information about NSGs, see [Opening ports tooa VM in Azure using PowerShell](nsg-quickstart-powershell.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

```powershell
$nsgName = "myNsg"

$rdpRule = New-AzureRmNetworkSecurityRuleConfig -Name myRdpRule -Description "Allow RDP" `
    -Access Allow -Protocol Tcp -Direction Inbound -Priority 110 `
    -SourceAddressPrefix Internet -SourcePortRange * `
    -DestinationAddressPrefix * -DestinationPortRange 3389

$nsg = New-AzureRmNetworkSecurityGroup -ResourceGroupName $rgName -Location $location `
    -Name $nsgName -SecurityRules $rdpRule
```


### <a name="create-a-variable-for-hello-virtual-network"></a><span data-ttu-id="3e42f-176">Utwórz zmienną hello sieci wirtualnej</span><span class="sxs-lookup"><span data-stu-id="3e42f-176">Create a variable for hello virtual network</span></span>
<span data-ttu-id="3e42f-177">Utwórz zmienną ukończyć powitalnych sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="3e42f-177">Create a variable for hello completed virtual network.</span></span> 

```powershell
$vnet = Get-AzureRmVirtualNetwork -ResourceGroupName $rgName -Name $vnetName
```

### <a name="create-hello-vm"></a><span data-ttu-id="3e42f-178">Utwórz hello maszyny Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="3e42f-178">Create hello VM</span></span>
<span data-ttu-id="3e42f-179">Hello następujące PowerShell kończy hello konfiguracje maszyny wirtualnej i używa niezarządzanej obrazu jako źródła hello hello nowej instalacji.</span><span class="sxs-lookup"><span data-stu-id="3e42f-179">hello following PowerShell completes hello virtual machine configurations and uses unmanaged image as hello source for hello new installation.</span></span>

</br>

```powershell
    # Enter a new user name and password toouse as hello local administrator account 
    # for remotely accessing hello VM.
    $cred = Get-Credential

    # Name of hello storage account where hello VHD is located. This example sets hello 
    # storage account name as "myStorageAccount"
    $storageAccName = "myStorageAccount"

    # Name of hello virtual machine. This example sets hello VM name as "myVM".
    $vmName = "myVM"

    # Size of hello virtual machine. This example creates "Standard_D2_v2" sized VM. 
    # See hello VM sizes documentation for more information: 
    # https://azure.microsoft.com/documentation/articles/virtual-machines-windows-sizes/
    $vmSize = "Standard_D2_v2"

    # Computer name for hello VM. This examples sets hello computer name as "myComputer".
    $computerName = "myComputer"

    # Name of hello disk that holds hello OS. This example sets hello 
    # OS disk name as "myOsDisk"
    $osDiskName = "myOsDisk"

    # Assign a SKU name. This example sets hello SKU name as "Standard_LRS"
    # Valid values for -SkuName are: Standard_LRS - locally redundant storage, Standard_ZRS - zone redundant
    # storage, Standard_GRS - geo redundant storage, Standard_RAGRS - read access geo redundant storage,
    # Premium_LRS - premium locally redundant storage. 
    $skuName = "Standard_LRS"

    # Get hello storage account where hello uploaded image is stored
    $storageAcc = Get-AzureRmStorageAccount -ResourceGroupName $rgName -AccountName $storageAccName

    # Set hello VM name and size
    $vmConfig = New-AzureRmVMConfig -VMName $vmName -VMSize $vmSize

    #Set hello Windows operating system configuration and add hello NIC
    $vm = Set-AzureRmVMOperatingSystem -VM $vmConfig -Windows -ComputerName $computerName `
        -Credential $cred -ProvisionVMAgent -EnableAutoUpdate
    $vm = Add-AzureRmVMNetworkInterface -VM $vm -Id $nic.Id

    # Create hello OS disk URI
    $osDiskUri = '{0}vhds/{1}-{2}.vhd' `
        -f $storageAcc.PrimaryEndpoints.Blob.ToString(), $vmName.ToLower(), $osDiskName

    # Configure hello OS disk toobe created from hello existing VHD image (-CreateOption fromImage).
    $vm = Set-AzureRmVMOSDisk -VM $vm -Name $osDiskName -VhdUri $osDiskUri `
        -CreateOption fromImage -SourceImageUri $imageURI -Windows

    # Create hello new VM
    New-AzureRmVM -ResourceGroupName $rgName -Location $location -VM $vm
```

### <a name="verify-that-hello-vm-was-created"></a><span data-ttu-id="3e42f-180">Sprawdź hello, że maszyna wirtualna została utworzona</span><span class="sxs-lookup"><span data-stu-id="3e42f-180">Verify that hello VM was created</span></span>
<span data-ttu-id="3e42f-181">Po zakończeniu powinien zostać wyświetlony hello nowo utworzony maszyny Wirtualnej w hello [portalu Azure](https://portal.azure.com) w obszarze **Przeglądaj** > **maszyn wirtualnych**, lub za pomocą następujących hello Polecenia programu PowerShell:</span><span class="sxs-lookup"><span data-stu-id="3e42f-181">When complete, you should see hello newly created VM in hello [Azure portal](https://portal.azure.com) under **Browse** > **Virtual machines**, or by using hello following PowerShell commands:</span></span>

```powershell
    $vmList = Get-AzureRmVM -ResourceGroupName $rgName
    $vmList.Name
```

## <a name="next-steps"></a><span data-ttu-id="3e42f-182">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="3e42f-182">Next steps</span></span>
<span data-ttu-id="3e42f-183">toomanage nowej maszyny wirtualnej przy użyciu programu Azure PowerShell, zobacz [zarządzania maszynami wirtualnymi przy użyciu usługi Azure Resource Manager i programu PowerShell](tutorial-manage-vm.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="3e42f-183">toomanage your new virtual machine with Azure PowerShell, see [Manage virtual machines using Azure Resource Manager and PowerShell](tutorial-manage-vm.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>


