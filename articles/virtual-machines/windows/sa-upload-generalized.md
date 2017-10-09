---
title: aaaUpload toocreate wirtualnego dysku twardego generalize wiele maszyn wirtualnych na platformie Azure | Dokumentacja firmy Microsoft
description: "Przekaż uogólniony wirtualny dysk twardy tooan magazynu Azure konta toocreate toouse maszyny Wirtualnej systemu Windows, z modelu wdrażania usługi Resource Manager hello."
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
ms.date: 05/18/2017
ms.author: cynthn
ms.openlocfilehash: aa1af2a0acf81685e62853de71afa51e819cb696
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="upload-a-generalized-vhd-tooazure-toocreate-a-new-vm"></a><span data-ttu-id="747f3-103">Przekaż uogólniony wirtualny dysk twardy tooAzure toocreate nowej maszyny Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="747f3-103">Upload a generalized VHD tooAzure toocreate a new VM</span></span>

<span data-ttu-id="747f3-104">W tym temacie omówiono przekazywania konta magazynu tooa uogólniony dysk niezarządzane, a następnie utworzenie nowej maszyny Wirtualnej przy użyciu dysku hello przekazany.</span><span class="sxs-lookup"><span data-stu-id="747f3-104">This topic covers uploading a generalized unmanaged disk tooa storage account and then creating a new VM using hello uploaded disk.</span></span> <span data-ttu-id="747f3-105">Obraz uogólniony wirtualny dysk twardy ma wszystkie informacje osobiste Konto usunięte za pomocą programu Sysprep.</span><span class="sxs-lookup"><span data-stu-id="747f3-105">A generalized VHD image has had all of your personal account information removed using Sysprep.</span></span> 

<span data-ttu-id="747f3-106">Jeśli chcesz toocreate Maszynę wirtualną z wirtualnego dysku twardego specjalne na koncie magazynu, zobacz [tworzenie maszyny Wirtualnej z dysku VHD specjalne](sa-create-vm-specialized.md).</span><span class="sxs-lookup"><span data-stu-id="747f3-106">If you want toocreate a VM from a specialized VHD in a storage account, see [Create a VM from a specialized VHD](sa-create-vm-specialized.md).</span></span>

<span data-ttu-id="747f3-107">W tym temacie omówiono używanie kont magazynu, ale zaleca się, że klienci przenoszenie dysków zarządzanych toousing zamiast tego.</span><span class="sxs-lookup"><span data-stu-id="747f3-107">This topic covers using storage accounts, but we recommend customers move toousing Managed Disks instead.</span></span> <span data-ttu-id="747f3-108">Na dyskach zarządzanych pełny przewodnik sposobu tooprepare, przekazywanie i Utwórz nowe przy użyciu maszyny Wirtualnej, zobacz [Utwórz nową maszynę Wirtualną z ogólnych tooAzure przekazany wirtualny dysk twardy za pomocą dysków zarządzanych](upload-generalized-managed.md).</span><span class="sxs-lookup"><span data-stu-id="747f3-108">For a complete walk-through of how tooprepare, upload and create a new VM using managed disks, see [Create a new VM from a generalized VHD uploaded tooAzure using Managed Disks](upload-generalized-managed.md).</span></span>



## <a name="prepare-hello-vm"></a><span data-ttu-id="747f3-109">Przygotowanie hello maszyny Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="747f3-109">Prepare hello VM</span></span>

<span data-ttu-id="747f3-110">Uogólniony wirtualny dysk twardy ma wszystkie informacje osobiste Konto usunięte za pomocą programu Sysprep.</span><span class="sxs-lookup"><span data-stu-id="747f3-110">A generalized VHD has had all of your personal account information removed using Sysprep.</span></span> <span data-ttu-id="747f3-111">Jeśli planujesz hello toouse toocreate obrazu wirtualnego dysku twardego nowych maszyn wirtualnych z, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="747f3-111">If you intend toouse hello VHD as an image toocreate new VMs from, you should:</span></span>
  
  * <span data-ttu-id="747f3-112">[Przygotowanie tooAzure tooupload wirtualnego dysku twardego Windows](prepare-for-upload-vhd-image.md).</span><span class="sxs-lookup"><span data-stu-id="747f3-112">[Prepare a Windows VHD tooupload tooAzure](prepare-for-upload-vhd-image.md).</span></span> 
  * <span data-ttu-id="747f3-113">Hello maszyny wirtualnej za pomocą programu Sysprep do uogólnienia</span><span class="sxs-lookup"><span data-stu-id="747f3-113">Generalize hello virtual machine using Sysprep</span></span>

### <a name="generalize-a-windows-virtual-machine-using-sysprep"></a><span data-ttu-id="747f3-114">Maszyny wirtualnej systemu Windows za pomocą programu Sysprep do uogólnienia</span><span class="sxs-lookup"><span data-stu-id="747f3-114">Generalize a Windows virtual machine using Sysprep</span></span>
<span data-ttu-id="747f3-115">W tej sekcji opisano sposób toogeneralize maszyny wirtualnej systemu Windows do użycia jako obraz.</span><span class="sxs-lookup"><span data-stu-id="747f3-115">This section shows you how toogeneralize your Windows virtual machine for use as an image.</span></span> <span data-ttu-id="747f3-116">Program Sysprep usuwa wszystkie informacje osobiste konto, między innymi i przygotowuje toobe maszyny hello użyty jako obraz.</span><span class="sxs-lookup"><span data-stu-id="747f3-116">Sysprep removes all your personal account information, among other things, and prepares hello machine toobe used as an image.</span></span> <span data-ttu-id="747f3-117">Aby uzyskać więcej informacji o narzędziu Sysprep, zobacz [jak tooUse Sysprep: wprowadzenie](http://technet.microsoft.com/library/bb457073.aspx).</span><span class="sxs-lookup"><span data-stu-id="747f3-117">For details about Sysprep, see [How tooUse Sysprep: An Introduction](http://technet.microsoft.com/library/bb457073.aspx).</span></span>

<span data-ttu-id="747f3-118">Upewnij się, że hello ról serwera uruchomionych na maszynie hello są obsługiwane przez program Sysprep.</span><span class="sxs-lookup"><span data-stu-id="747f3-118">Make sure hello server roles running on hello machine are supported by Sysprep.</span></span> <span data-ttu-id="747f3-119">Aby uzyskać więcej informacji, zobacz [Obsługa programu Sysprep dla ról serwera](https://msdn.microsoft.com/windows/hardware/commercialize/manufacture/desktop/sysprep-support-for-server-roles)</span><span class="sxs-lookup"><span data-stu-id="747f3-119">For more information, see [Sysprep Support for Server Roles](https://msdn.microsoft.com/windows/hardware/commercialize/manufacture/desktop/sysprep-support-for-server-roles)</span></span>

> [!IMPORTANT]
> <span data-ttu-id="747f3-120">Jeśli korzystasz z programu Sysprep przed przekazaniem tooAzure Twojego dysku VHD na powitania po raz pierwszy, upewnij się, masz [przygotować maszyny Wirtualnej](prepare-for-upload-vhd-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) przed uruchomieniem programu Sysprep.</span><span class="sxs-lookup"><span data-stu-id="747f3-120">If you are running Sysprep before uploading your VHD tooAzure for hello first time, make sure you have [prepared your VM](prepare-for-upload-vhd-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) before running Sysprep.</span></span> 
> 
> 

1. <span data-ttu-id="747f3-121">Zaloguj się toohello maszyny wirtualnej systemu Windows.</span><span class="sxs-lookup"><span data-stu-id="747f3-121">Sign in toohello Windows virtual machine.</span></span>
2. <span data-ttu-id="747f3-122">Otwórz okno wiersza polecenia hello jako administrator.</span><span class="sxs-lookup"><span data-stu-id="747f3-122">Open hello Command Prompt window as an administrator.</span></span> <span data-ttu-id="747f3-123">Zmień katalog hello zbyt**%windir%\system32\sysprep**, a następnie uruchom `sysprep.exe`.</span><span class="sxs-lookup"><span data-stu-id="747f3-123">Change hello directory too**%windir%\system32\sysprep**, and then run `sysprep.exe`.</span></span>
3. <span data-ttu-id="747f3-124">W hello **narzędzie przygotowania systemu** okno dialogowe, wybierz opcję **wprowadź systemu Out-of-Box Experience (OOBE)**i upewnij się, że hello **Generalize** pole wyboru jest zaznaczone.</span><span class="sxs-lookup"><span data-stu-id="747f3-124">In hello **System Preparation Tool** dialog box, select **Enter System Out-of-Box Experience (OOBE)**, and make sure that hello **Generalize** check box is selected.</span></span>
4. <span data-ttu-id="747f3-125">W **opcje zamykania**, wybierz pozycję **zamknięcia**.</span><span class="sxs-lookup"><span data-stu-id="747f3-125">In **Shutdown Options**, select **Shutdown**.</span></span>
5. <span data-ttu-id="747f3-126">Kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="747f3-126">Click **OK**.</span></span>
   
    ![Uruchom program Sysprep](./media/upload-generalized-managed/sysprepgeneral.png)
6. <span data-ttu-id="747f3-128">Po zakończeniu działania programu Sysprep, zamyka hello maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="747f3-128">When Sysprep completes, it shuts down hello virtual machine.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="747f3-129">Nie uruchamiaj ponownie hello maszyny Wirtualnej, dopóki nie są gotowe, przesyłania tooAzure wirtualnego dysku twardego hello lub Tworzenie obrazu z hello maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="747f3-129">Do not restart hello VM until you are done uploading hello VHD tooAzure or creating an image from hello VM.</span></span> <span data-ttu-id="747f3-130">Jeśli hello wirtualna przypadkowo pobiera ponownie uruchomione, uruchom Sysprep toogeneralize go ponownie.</span><span class="sxs-lookup"><span data-stu-id="747f3-130">If hello VM accidentally gets restarted, run Sysprep toogeneralize it again.</span></span>
> 
> 


## <a name="upload-hello-vhd"></a><span data-ttu-id="747f3-131">Przekaż hello wirtualnego dysku twardego</span><span class="sxs-lookup"><span data-stu-id="747f3-131">Upload hello VHD</span></span>

<span data-ttu-id="747f3-132">Przekaż hello wirtualnego dysku twardego tooan konta magazynu Azure.</span><span class="sxs-lookup"><span data-stu-id="747f3-132">Upload hello VHD tooan Azure storage account.</span></span>

### <a name="log-in-tooazure"></a><span data-ttu-id="747f3-133">Zaloguj się za tooAzure</span><span class="sxs-lookup"><span data-stu-id="747f3-133">Log in tooAzure</span></span>
<span data-ttu-id="747f3-134">Jeśli nie masz jeszcze programu PowerShell w wersji 1.4 lub nowszy zainstalowany, przeczytaj [jak tooinstall i konfigurowanie programu Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="747f3-134">If you don't already have PowerShell version 1.4 or above installed, read [How tooinstall and configure Azure PowerShell](/powershell/azure/overview).</span></span>

1. <span data-ttu-id="747f3-135">Otwórz program Azure PowerShell i zaloguj się na tooyour konto platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="747f3-135">Open Azure PowerShell and sign in tooyour Azure account.</span></span> <span data-ttu-id="747f3-136">Zostanie otwarte okno podręczne dla tooenter możesz poświadczenia konta Azure.</span><span class="sxs-lookup"><span data-stu-id="747f3-136">A pop-up window opens for you tooenter your Azure account credentials.</span></span>
   
    ```powershell
    Login-AzureRmAccount
    ```
2. <span data-ttu-id="747f3-137">Uzyskanie subskrypcji hello identyfikatorów subskrypcji dostępne.</span><span class="sxs-lookup"><span data-stu-id="747f3-137">Get hello subscription IDs for your available subscriptions.</span></span>
   
    ```powershell
    Get-AzureRmSubscription
    ```
3. <span data-ttu-id="747f3-138">Ustaw poprawną subskrypcję hello przy użyciu identyfikatora hello subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="747f3-138">Set hello correct subscription using hello subscription ID.</span></span> <span data-ttu-id="747f3-139">Zastąp `<subscriptionID>` o identyfikatorze hello hello Popraw subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="747f3-139">Replace `<subscriptionID>` with hello ID of hello correct subscription.</span></span>
   
    ```powershell
    Select-AzureRmSubscription -SubscriptionId "<subscriptionID>"
    ```

### <a name="get-hello-storage-account"></a><span data-ttu-id="747f3-140">Pobierz hello konta magazynu</span><span class="sxs-lookup"><span data-stu-id="747f3-140">Get hello storage account</span></span>
<span data-ttu-id="747f3-141">Musisz mieć konto magazynu, w obrazie maszyny Wirtualnej Azure toostore hello przekazany.</span><span class="sxs-lookup"><span data-stu-id="747f3-141">You need a storage account in Azure toostore hello uploaded VM image.</span></span> <span data-ttu-id="747f3-142">Możesz użyć istniejącego konta magazynu lub Utwórz nową.</span><span class="sxs-lookup"><span data-stu-id="747f3-142">You can either use an existing storage account or create a new one.</span></span> 

<span data-ttu-id="747f3-143">tooshow hello dostępny magazyn kont, wpisz:</span><span class="sxs-lookup"><span data-stu-id="747f3-143">tooshow hello available storage accounts, type:</span></span>

```powershell
Get-AzureRmStorageAccount
```

<span data-ttu-id="747f3-144">Jeśli chcesz toouse istniejącego konta magazynu, przejdź toohello [obrazu maszyny Wirtualnej hello przekazywania](#upload-the-vm-vhd-to-your-storage-account) sekcji.</span><span class="sxs-lookup"><span data-stu-id="747f3-144">If you want toouse an existing storage account, proceed toohello [Upload hello VM image](#upload-the-vm-vhd-to-your-storage-account) section.</span></span>

<span data-ttu-id="747f3-145">Jeśli potrzebujesz toocreate konta magazynu, wykonaj następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="747f3-145">If you need toocreate a storage account, follow these steps:</span></span>

1. <span data-ttu-id="747f3-146">Potrzebna jest nazwa hello hello grupy zasobów, których można utworzyć konta magazynu hello.</span><span class="sxs-lookup"><span data-stu-id="747f3-146">You need hello name of hello resource group where hello storage account should be created.</span></span> <span data-ttu-id="747f3-147">toofind limit wszystkie hello grupy zasobów, które są w ramach subskrypcji, wpisz:</span><span class="sxs-lookup"><span data-stu-id="747f3-147">toofind out all hello resource groups that are in your subscription, type:</span></span>
   
    ```powershell
    Get-AzureRmResourceGroup
    ```

    <span data-ttu-id="747f3-148">Grupa zasobów o nazwie toocreate **myResourceGroup** w hello **zachodnie stany USA** regionu, wpisz:</span><span class="sxs-lookup"><span data-stu-id="747f3-148">toocreate a resource group named **myResourceGroup** in hello **West US** region, type:</span></span>

    ```powershell
    New-AzureRmResourceGroup -Name myResourceGroup -Location "West US"
    ```

2. <span data-ttu-id="747f3-149">Utwórz konto magazynu o nazwie **mojekontomagazynu** w tej grupie zasobów za pomocą hello [New-AzureRmStorageAccount](/powershell/module/azurerm.storage/new-azurermstorageaccount) polecenia cmdlet:</span><span class="sxs-lookup"><span data-stu-id="747f3-149">Create a storage account named **mystorageaccount** in this resource group by using hello [New-AzureRmStorageAccount](/powershell/module/azurerm.storage/new-azurermstorageaccount) cmdlet:</span></span>
   
    ```powershell
    New-AzureRmStorageAccount -ResourceGroupName myResourceGroup -Name mystorageaccount -Location "West US" `
        -SkuName "Standard_LRS" -Kind "Storage"
    ```
 
### <a name="start-hello-upload"></a><span data-ttu-id="747f3-150">Rozpocznij przekazywanie hello</span><span class="sxs-lookup"><span data-stu-id="747f3-150">Start hello upload</span></span> 

<span data-ttu-id="747f3-151">Użyj hello [AzureRmVhd Dodaj](/powershell/module/azurerm.compute/add-azurermvhd) polecenia cmdlet tooupload hello obrazu tooa kontenera na koncie magazynu.</span><span class="sxs-lookup"><span data-stu-id="747f3-151">Use hello [Add-AzureRmVhd](/powershell/module/azurerm.compute/add-azurermvhd) cmdlet tooupload hello image tooa container in your storage account.</span></span> <span data-ttu-id="747f3-152">W tym przykładzie przekazywania hello pliku **myVHD.vhd** z `"C:\Users\Public\Documents\Virtual hard disks\"` tooa konto magazynu o nazwie **mojekontomagazynu** w hello **myResourceGroup** grupy zasobów.</span><span class="sxs-lookup"><span data-stu-id="747f3-152">This example uploads hello file **myVHD.vhd** from `"C:\Users\Public\Documents\Virtual hard disks\"` tooa storage account named **mystorageaccount** in hello **myResourceGroup** resource group.</span></span> <span data-ttu-id="747f3-153">Plik Hello zostaną umieszczone w hello kontener o nazwie **mojkontener** i będzie hello nową nazwę pliku **myUploadedVHD.vhd**.</span><span class="sxs-lookup"><span data-stu-id="747f3-153">hello file will be placed into hello container named **mycontainer** and hello new file name will be **myUploadedVHD.vhd**.</span></span>

```powershell
$rgName = "myResourceGroup"
$urlOfUploadedImageVhd = "https://mystorageaccount.blob.core.windows.net/mycontainer/myUploadedVHD.vhd"
Add-AzureRmVhd -ResourceGroupName $rgName -Destination $urlOfUploadedImageVhd `
    -LocalFilePath "C:\Users\Public\Documents\Virtual hard disks\myVHD.vhd"
```


<span data-ttu-id="747f3-154">W przypadku powodzenia można uzyskać odpowiedzi, która wygląda podobnie toothis:</span><span class="sxs-lookup"><span data-stu-id="747f3-154">If successful, you get a response that looks similar toothis:</span></span>

```powershell
MD5 hash is being calculated for hello file C:\Users\Public\Documents\Virtual hard disks\myVHD.vhd.
MD5 hash calculation is completed.
Elapsed time for hello operation: 00:03:35
Creating new page blob of size 53687091712...
Elapsed time for upload: 01:12:49

LocalFilePath           DestinationUri
-------------           --------------
C:\Users\Public\Doc...  https://mystorageaccount.blob.core.windows.net/mycontainer/myUploadedVHD.vhd
```

<span data-ttu-id="747f3-155">W zależności od połączenia sieciowego i hello rozmiar pliku VHD, polecenie to może chwilę potrwać toocomplete.</span><span class="sxs-lookup"><span data-stu-id="747f3-155">Depending on your network connection and hello size of your VHD file, this command may take a while toocomplete.</span></span>


## <a name="create-a-new-vm"></a><span data-ttu-id="747f3-156">Tworzenie nowej maszyny Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="747f3-156">Create a new VM</span></span> 

<span data-ttu-id="747f3-157">Możesz teraz hello Użyj przekazać toocreate wirtualnego dysku twardego nowej maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="747f3-157">You can now use hello uploaded VHD toocreate a new VM.</span></span> 

### <a name="set-hello-uri-of-hello-vhd"></a><span data-ttu-id="747f3-158">Ustaw hello URI hello wirtualnego dysku twardego</span><span class="sxs-lookup"><span data-stu-id="747f3-158">Set hello URI of hello VHD</span></span>

<span data-ttu-id="747f3-159">Hello identyfikatora URI dla toouse wirtualnego dysku twardego hello jest w formacie hello: https://**mojekontomagazynu**.blob.core.windows.net/**mojkontener**/**MyVhdName**VHD.</span><span class="sxs-lookup"><span data-stu-id="747f3-159">hello URI for hello VHD toouse is in hello format: https://**mystorageaccount**.blob.core.windows.net/**mycontainer**/**MyVhdName**.vhd.</span></span> <span data-ttu-id="747f3-160">W tym przykładzie hello wirtualnego dysku twardego o nazwie **myVHD** jest na koncie magazynu hello **mojekontomagazynu** w kontenerze hello **mojkontener**.</span><span class="sxs-lookup"><span data-stu-id="747f3-160">In this example hello VHD named **myVHD** is in hello storage account **mystorageaccount** in hello container **mycontainer**.</span></span>

```powershell
$imageURI = "https://mystorageaccount.blob.core.windows.net/mycontainer/myVhd.vhd"
```


### <a name="create-a-virtual-network"></a><span data-ttu-id="747f3-161">Tworzenie sieci wirtualnej</span><span class="sxs-lookup"><span data-stu-id="747f3-161">Create a virtual network</span></span>
<span data-ttu-id="747f3-162">Tworzenie sieci wirtualnej hello i podsieci hello [sieci wirtualnej](../../virtual-network/virtual-networks-overview.md).</span><span class="sxs-lookup"><span data-stu-id="747f3-162">Create hello vNet and subnet of hello [virtual network](../../virtual-network/virtual-networks-overview.md).</span></span>

1. <span data-ttu-id="747f3-163">Utwórz podsieć hello.</span><span class="sxs-lookup"><span data-stu-id="747f3-163">Create hello subnet.</span></span> <span data-ttu-id="747f3-164">Witaj poniższy przykład tworzy podsieć o nazwie **mySubnet** w grupie zasobów hello **myResourceGroup** z prefiksu adresu hello **10.0.0.0/24**.</span><span class="sxs-lookup"><span data-stu-id="747f3-164">hello following sample creates a subnet named **mySubnet** in hello resource group **myResourceGroup** with hello address prefix of **10.0.0.0/24**.</span></span>  
   
    ```powershell
    $rgName = "myResourceGroup"
    $subnetName = "mySubnet"
    $singleSubnet = New-AzureRmVirtualNetworkSubnetConfig -Name $subnetName -AddressPrefix 10.0.0.0/24
    ```
2. <span data-ttu-id="747f3-165">Utwórz sieć wirtualną hello.</span><span class="sxs-lookup"><span data-stu-id="747f3-165">Create hello virtual network.</span></span> <span data-ttu-id="747f3-166">Witaj poniższy przykład tworzy sieć wirtualną o nazwie **myVnet** w hello **zachodnie stany USA** lokalizacji z prefiksu adresu hello **10.0.0.0/16**.</span><span class="sxs-lookup"><span data-stu-id="747f3-166">hello following sample creates a virtual network named **myVnet** in hello **West US** location with hello address prefix of **10.0.0.0/16**.</span></span>  
   
    ```powershell
    $location = "West US"
    $vnetName = "myVnet"
    $vnet = New-AzureRmVirtualNetwork -Name $vnetName -ResourceGroupName $rgName -Location $location `
        -AddressPrefix 10.0.0.0/16 -Subnet $singleSubnet
    ```    

### <a name="create-a-public-ip-address-and-network-interface"></a><span data-ttu-id="747f3-167">Tworzenie publicznego adresu IP adres i interfejsu sieciowego</span><span class="sxs-lookup"><span data-stu-id="747f3-167">Create a public IP address and network interface</span></span>
<span data-ttu-id="747f3-168">tooenable komunikację z maszyną wirtualną hello w sieci wirtualnej hello, należy [publicznego adresu IP](../../virtual-network/virtual-network-ip-addresses-overview-arm.md) i interfejsu sieciowego.</span><span class="sxs-lookup"><span data-stu-id="747f3-168">tooenable communication with hello virtual machine in hello virtual network, you need a [public IP address](../../virtual-network/virtual-network-ip-addresses-overview-arm.md) and a network interface.</span></span>

1. <span data-ttu-id="747f3-169">Utwórz publiczny adres IP.</span><span class="sxs-lookup"><span data-stu-id="747f3-169">Create a public IP address.</span></span> <span data-ttu-id="747f3-170">W tym przykładzie jest tworzony publiczny adres IP o nazwie **myPip**.</span><span class="sxs-lookup"><span data-stu-id="747f3-170">This example creates a public IP address named **myPip**.</span></span> 
   
    ```powershell
    $ipName = "myPip"
    $pip = New-AzureRmPublicIpAddress -Name $ipName -ResourceGroupName $rgName -Location $location `
        -AllocationMethod Dynamic
    ```       
2. <span data-ttu-id="747f3-171">Utwórz hello karty sieciowej.</span><span class="sxs-lookup"><span data-stu-id="747f3-171">Create hello NIC.</span></span> <span data-ttu-id="747f3-172">W tym przykładzie jest tworzony karty Sieciowej o nazwie **myNic**.</span><span class="sxs-lookup"><span data-stu-id="747f3-172">This example creates a NIC named **myNic**.</span></span> 
   
    ```powershell
    $nicName = "myNic"
    $nic = New-AzureRmNetworkInterface -Name $nicName -ResourceGroupName $rgName -Location $location `
        -SubnetId $vnet.Subnets[0].Id -PublicIpAddressId $pip.Id
    ```

### <a name="create-hello-network-security-group-and-an-rdp-rule"></a><span data-ttu-id="747f3-173">Tworzenie grupy zabezpieczeń sieci hello i reguły protokołu RDP</span><span class="sxs-lookup"><span data-stu-id="747f3-173">Create hello network security group and an RDP rule</span></span>
<span data-ttu-id="747f3-174">toobe stanie toolog w tooyour maszyny Wirtualnej przy użyciu protokołu RDP, należy toohave regułę zabezpieczeń, która udziela dostępu RDP do portu 3389.</span><span class="sxs-lookup"><span data-stu-id="747f3-174">toobe able toolog in tooyour VM using RDP, you need toohave a security rule that allows RDP access on port 3389.</span></span> 

<span data-ttu-id="747f3-175">W tym przykładzie tworzy grupy NSG o nazwie **myNsg** zawierający regułę o nazwie **myRdpRule** za pośrednictwem portu 3389 która zezwala na ruch RDP.</span><span class="sxs-lookup"><span data-stu-id="747f3-175">This example creates an NSG named **myNsg** that contains a rule called **myRdpRule** that allows RDP traffic over port 3389.</span></span> <span data-ttu-id="747f3-176">Aby uzyskać więcej informacji na temat grup NSG, zobacz [otwierania portów tooa maszyny Wirtualnej na platformie Azure przy użyciu programu PowerShell](nsg-quickstart-powershell.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="747f3-176">For more information about NSGs, see [Opening ports tooa VM in Azure using PowerShell](nsg-quickstart-powershell.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

```powershell
$nsgName = "myNsg"

$rdpRule = New-AzureRmNetworkSecurityRuleConfig -Name myRdpRule -Description "Allow RDP" `
    -Access Allow -Protocol Tcp -Direction Inbound -Priority 110 `
    -SourceAddressPrefix Internet -SourcePortRange * `
    -DestinationAddressPrefix * -DestinationPortRange 3389

$nsg = New-AzureRmNetworkSecurityGroup -ResourceGroupName $rgName -Location $location `
    -Name $nsgName -SecurityRules $rdpRule
```


### <a name="create-a-variable-for-hello-virtual-network"></a><span data-ttu-id="747f3-177">Utwórz zmienną hello sieci wirtualnej</span><span class="sxs-lookup"><span data-stu-id="747f3-177">Create a variable for hello virtual network</span></span>
<span data-ttu-id="747f3-178">Utwórz zmienną ukończyć powitalnych sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="747f3-178">Create a variable for hello completed virtual network.</span></span> 

```powershell
$vnet = Get-AzureRmVirtualNetwork -ResourceGroupName $rgName -Name $vnetName
```

### <a name="create-hello-vm"></a><span data-ttu-id="747f3-179">Utwórz hello maszyny Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="747f3-179">Create hello VM</span></span>
<span data-ttu-id="747f3-180">Witaj następujący skrypt programu PowerShell pokazuje sposób tooset hello konfiguracje maszyny wirtualnej i użyj hello przekazać obraz maszyny Wirtualnej jako źródło hello hello nowa instalacja.</span><span class="sxs-lookup"><span data-stu-id="747f3-180">hello following PowerShell script shows how tooset up hello virtual machine configurations and use hello uploaded VM image as hello source for hello new installation.</span></span>



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

## <a name="verify-that-hello-vm-was-created"></a><span data-ttu-id="747f3-181">Sprawdź hello, że maszyna wirtualna została utworzona</span><span class="sxs-lookup"><span data-stu-id="747f3-181">Verify that hello VM was created</span></span>
<span data-ttu-id="747f3-182">Po zakończeniu powinien zostać wyświetlony hello nowo utworzony maszyny Wirtualnej w hello [portalu Azure](https://portal.azure.com) w obszarze **Przeglądaj** > **maszyn wirtualnych**, lub za pomocą następujących hello Polecenia programu PowerShell:</span><span class="sxs-lookup"><span data-stu-id="747f3-182">When complete, you should see hello newly created VM in hello [Azure portal](https://portal.azure.com) under **Browse** > **Virtual machines**, or by using hello following PowerShell commands:</span></span>

```powershell
    $vmList = Get-AzureRmVM -ResourceGroupName $rgName
    $vmList.Name
```

## <a name="next-steps"></a><span data-ttu-id="747f3-183">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="747f3-183">Next steps</span></span>
<span data-ttu-id="747f3-184">toomanage nowej maszyny wirtualnej przy użyciu programu Azure PowerShell, zobacz [zarządzania maszynami wirtualnymi przy użyciu usługi Azure Resource Manager i programu PowerShell](tutorial-manage-vm.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="747f3-184">toomanage your new virtual machine with Azure PowerShell, see [Manage virtual machines using Azure Resource Manager and PowerShell](tutorial-manage-vm.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>


