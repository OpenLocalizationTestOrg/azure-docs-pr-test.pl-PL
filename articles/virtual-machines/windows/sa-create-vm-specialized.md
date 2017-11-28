---
title: aaaCreate maszyny Wirtualnej z dysku specjalne na platformie Azure | Dokumentacja firmy Microsoft
description: "Dołączanie specjalne dysku niezarządzane, w modelu wdrażania usługi Resource Manager hello, aby utworzyć nową maszynę Wirtualną."
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 3b7d3cd5-e3d7-4041-a2a7-0290447458ea
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 05/23/2017
ms.author: cynthn
ms.openlocfilehash: c88f213b6629a6c1d6ff5845e76c2f7719672714
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-vm-from-a-specialized-vhd-in-a-storage-account"></a><span data-ttu-id="2f9a2-103">Utwórz maszynę Wirtualną z wirtualnego dysku twardego specjalne konta magazynu</span><span class="sxs-lookup"><span data-stu-id="2f9a2-103">Create a VM from a specialized VHD in a storage account</span></span>

<span data-ttu-id="2f9a2-104">Dołączanie dysku niezarządzane specjalne jako dysk systemu operacyjnego hello przy użyciu programu Powershell, aby utworzyć nową maszynę Wirtualną.</span><span class="sxs-lookup"><span data-stu-id="2f9a2-104">Create a new VM by attaching a specialized unmanaged disk as hello OS disk using Powershell.</span></span> <span data-ttu-id="2f9a2-105">Specjalne dysku jest kopią wirtualnego dysku twardego z istniejącą maszynę Wirtualną, która przechowuje konta użytkowników hello, aplikacji i innych danych o stanie z oryginalnego maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="2f9a2-105">A specialized disk is a copy of VHD from an existing VM that maintains hello user accounts, applications and other state data from your original VM.</span></span> 

<span data-ttu-id="2f9a2-106">Dostępne są dwie opcje:</span><span class="sxs-lookup"><span data-stu-id="2f9a2-106">You have two options:</span></span>
* [<span data-ttu-id="2f9a2-107">Przekazywanie wirtualnego dysku twardego</span><span class="sxs-lookup"><span data-stu-id="2f9a2-107">Upload a VHD</span></span>](create-vm-specialized.md#option-1-upload-a-specialized-vhd)
* [<span data-ttu-id="2f9a2-108">Skopiuj hello VHD istniejącej maszyny Wirtualnej Azure</span><span class="sxs-lookup"><span data-stu-id="2f9a2-108">Copy hello VHD of an existing Azure VM</span></span>](create-vm-specialized.md#option-2-copy-an-existing-azure-vm)

## <a name="before-you-begin"></a><span data-ttu-id="2f9a2-109">Przed rozpoczęciem</span><span class="sxs-lookup"><span data-stu-id="2f9a2-109">Before you begin</span></span>
<span data-ttu-id="2f9a2-110">Jeśli używasz programu PowerShell, upewnij się, że masz najnowszą wersję hello modułu AzureRM.Compute PowerShell hello.</span><span class="sxs-lookup"><span data-stu-id="2f9a2-110">If you use PowerShell, make sure that you have hello latest version of hello AzureRM.Compute PowerShell module.</span></span> <span data-ttu-id="2f9a2-111">Uruchom hello następujących tooinstall polecenia.</span><span class="sxs-lookup"><span data-stu-id="2f9a2-111">Run hello following command tooinstall it.</span></span>

```powershell
Install-Module AzureRM.Compute 
```
<span data-ttu-id="2f9a2-112">Aby uzyskać więcej informacji, zobacz [przechowywanie wersji programu Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="2f9a2-112">For more information, see [Azure PowerShell Versioning](/powershell/azure/overview).</span></span>


## <a name="option-1-upload-a-specialized-vhd"></a><span data-ttu-id="2f9a2-113">Opcja 1: Przekazanie specjalne dysku VHD</span><span class="sxs-lookup"><span data-stu-id="2f9a2-113">Option 1: Upload a specialized VHD</span></span>

<span data-ttu-id="2f9a2-114">Możesz przekazać powitalne wirtualnego dysku twardego z specjalistyczne maszyny Wirtualnej utworzone za pomocą wirtualizacji narzędzia lokalnych, takich jak funkcja Hyper-V lub maszyny Wirtualnej wyeksportowane z innej chmury.</span><span class="sxs-lookup"><span data-stu-id="2f9a2-114">You can upload hello VHD from a specialized VM created with an on-premises virtualization tool, like Hyper-V, or a VM exported from another cloud.</span></span>

### <a name="prepare-hello-vm"></a><span data-ttu-id="2f9a2-115">Przygotowanie hello maszyny Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="2f9a2-115">Prepare hello VM</span></span>
<span data-ttu-id="2f9a2-116">Możesz przekazać specjalne wirtualnego dysku twardego, który został utworzony przy użyciu lokalnej maszyny Wirtualnej lub wirtualnego dysku twardego wyeksportowane z innej chmury.</span><span class="sxs-lookup"><span data-stu-id="2f9a2-116">You can upload a specialized VHD that was created using an on-premises VM or a VHD exported from another cloud.</span></span> <span data-ttu-id="2f9a2-117">Specjalne wirtualnego dysku twardego przechowuje hello kont użytkowników, aplikacji i innych danych o stanie z oryginalnego maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="2f9a2-117">A specialized VHD maintains hello user accounts, applications and other state data from your original VM.</span></span> <span data-ttu-id="2f9a2-118">Jeśli planujesz toouse hello wirtualnego dysku twardego — jest toocreate nowej maszyny Wirtualnej, upewnij się, hello następujące kroki zostały zakończone.</span><span class="sxs-lookup"><span data-stu-id="2f9a2-118">If you intend toouse hello VHD as-is toocreate a new VM, ensure hello following steps are completed.</span></span> 
  
  * <span data-ttu-id="2f9a2-119">[Przygotowanie tooAzure tooupload wirtualnego dysku twardego Windows](prepare-for-upload-vhd-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="2f9a2-119">[Prepare a Windows VHD tooupload tooAzure](prepare-for-upload-vhd-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> <span data-ttu-id="2f9a2-120">**Nie** generalize hello maszyny Wirtualnej przy użyciu narzędzia Sysprep.</span><span class="sxs-lookup"><span data-stu-id="2f9a2-120">**Do not** generalize hello VM using Sysprep.</span></span>
  * <span data-ttu-id="2f9a2-121">Usuń wszystkie narzędzia wirtualizacji gościa i agentów, które są zainstalowane na powitania maszyny Wirtualnej (np. narzędzi VMware).</span><span class="sxs-lookup"><span data-stu-id="2f9a2-121">Remove any guest virtualization tools and agents that are installed on hello VM (i.e. VMware tools).</span></span>
  * <span data-ttu-id="2f9a2-122">Upewnij się, hello maszyna wirtualna jest skonfigurowana toopull jego adres IP i ustawienia DNS za pośrednictwem protokołu DHCP.</span><span class="sxs-lookup"><span data-stu-id="2f9a2-122">Ensure hello VM is configured toopull its IP address and DNS settings via DHCP.</span></span> <span data-ttu-id="2f9a2-123">To zapewnia, że ten serwer hello uzyskuje adres IP w ramach hello sieci wirtualnej podczas uruchamiania.</span><span class="sxs-lookup"><span data-stu-id="2f9a2-123">This ensures that hello server obtains an IP address within hello VNet when it starts up.</span></span> 


### <a name="get-hello-storage-account"></a><span data-ttu-id="2f9a2-124">Pobierz hello konta magazynu</span><span class="sxs-lookup"><span data-stu-id="2f9a2-124">Get hello storage account</span></span>
<span data-ttu-id="2f9a2-125">Musisz mieć konto magazynu, w obrazie maszyny Wirtualnej Azure toostore hello przekazany.</span><span class="sxs-lookup"><span data-stu-id="2f9a2-125">You need a storage account in Azure toostore hello uploaded VM image.</span></span> <span data-ttu-id="2f9a2-126">Możesz użyć istniejącego konta magazynu lub Utwórz nową.</span><span class="sxs-lookup"><span data-stu-id="2f9a2-126">You can either use an existing storage account or create a new one.</span></span> 

<span data-ttu-id="2f9a2-127">tooshow hello dostępny magazyn kont, wpisz:</span><span class="sxs-lookup"><span data-stu-id="2f9a2-127">tooshow hello available storage accounts, type:</span></span>

```powershell
Get-AzureRmStorageAccount
```

<span data-ttu-id="2f9a2-128">Jeśli chcesz toouse istniejącego konta magazynu, przejdź toohello [obrazu maszyny Wirtualnej hello przekazywania](#upload-the-vm-vhd-to-your-storage-account) sekcji.</span><span class="sxs-lookup"><span data-stu-id="2f9a2-128">If you want toouse an existing storage account, proceed toohello [Upload hello VM image](#upload-the-vm-vhd-to-your-storage-account) section.</span></span>

<span data-ttu-id="2f9a2-129">Jeśli potrzebujesz toocreate konta magazynu, wykonaj następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="2f9a2-129">If you need toocreate a storage account, follow these steps:</span></span>

1. <span data-ttu-id="2f9a2-130">Potrzebna jest nazwa hello hello grupy zasobów, których można utworzyć konta magazynu hello.</span><span class="sxs-lookup"><span data-stu-id="2f9a2-130">You need hello name of hello resource group where hello storage account should be created.</span></span> <span data-ttu-id="2f9a2-131">toofind limit wszystkie hello grupy zasobów, które są w ramach subskrypcji, wpisz:</span><span class="sxs-lookup"><span data-stu-id="2f9a2-131">toofind out all hello resource groups that are in your subscription, type:</span></span>
   
    ```powershell
    Get-AzureRmResourceGroup
    ```

    <span data-ttu-id="2f9a2-132">Grupa zasobów o nazwie toocreate **myResourceGroup** w hello **zachodnie stany USA** regionu, wpisz:</span><span class="sxs-lookup"><span data-stu-id="2f9a2-132">toocreate a resource group named **myResourceGroup** in hello **West US** region, type:</span></span>

    ```powershell
    New-AzureRmResourceGroup -Name myResourceGroup -Location "West US"
    ```

2. <span data-ttu-id="2f9a2-133">Utwórz konto magazynu o nazwie **mojekontomagazynu** w tej grupie zasobów za pomocą hello [New-AzureRmStorageAccount](/powershell/module/azurerm.storage/new-azurermstorageaccount) polecenia cmdlet:</span><span class="sxs-lookup"><span data-stu-id="2f9a2-133">Create a storage account named **mystorageaccount** in this resource group by using hello [New-AzureRmStorageAccount](/powershell/module/azurerm.storage/new-azurermstorageaccount) cmdlet:</span></span>
   
    ```powershell
    New-AzureRmStorageAccount -ResourceGroupName myResourceGroup -Name mystorageaccount -Location "West US" `
        -SkuName "Standard_LRS" -Kind "Storage"
    ```
   
### <a name="upload-hello-vhd-tooyour-storage-account"></a><span data-ttu-id="2f9a2-134">Przekaż konta magazynu tooyour wirtualnego dysku twardego hello</span><span class="sxs-lookup"><span data-stu-id="2f9a2-134">Upload hello VHD tooyour storage account</span></span>
<span data-ttu-id="2f9a2-135">Użyj hello [AzureRmVhd Dodaj](/powershell/module/azurerm.compute/add-azurermvhd) polecenia cmdlet tooupload hello obrazu tooa kontenera na koncie magazynu.</span><span class="sxs-lookup"><span data-stu-id="2f9a2-135">Use hello [Add-AzureRmVhd](/powershell/module/azurerm.compute/add-azurermvhd) cmdlet tooupload hello image tooa container in your storage account.</span></span> <span data-ttu-id="2f9a2-136">W tym przykładzie przekazywania hello pliku **myVHD.vhd** z `"C:\Users\Public\Documents\Virtual hard disks\"` tooa konto magazynu o nazwie **mojekontomagazynu** w hello **myResourceGroup** grupy zasobów.</span><span class="sxs-lookup"><span data-stu-id="2f9a2-136">This example uploads hello file **myVHD.vhd** from `"C:\Users\Public\Documents\Virtual hard disks\"` tooa storage account named **mystorageaccount** in hello **myResourceGroup** resource group.</span></span> <span data-ttu-id="2f9a2-137">Plik Hello zostaną umieszczone w hello kontener o nazwie **mojkontener** i będzie hello nową nazwę pliku **myUploadedVHD.vhd**.</span><span class="sxs-lookup"><span data-stu-id="2f9a2-137">hello file will be placed into hello container named **mycontainer** and hello new file name will be **myUploadedVHD.vhd**.</span></span>

```powershell
$rgName = "myResourceGroup"
$urlOfUploadedImageVhd = "https://mystorageaccount.blob.core.windows.net/mycontainer/myUploadedVHD.vhd"
Add-AzureRmVhd -ResourceGroupName $rgName -Destination $urlOfUploadedImageVhd `
    -LocalFilePath "C:\Users\Public\Documents\Virtual hard disks\myVHD.vhd"
```


<span data-ttu-id="2f9a2-138">W przypadku powodzenia można uzyskać odpowiedzi, która wygląda podobnie toothis:</span><span class="sxs-lookup"><span data-stu-id="2f9a2-138">If successful, you get a response that looks similar toothis:</span></span>

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

<span data-ttu-id="2f9a2-139">W zależności od połączenia sieciowego i hello rozmiar pliku VHD, polecenie to może chwilę potrwać toocomplete.</span><span class="sxs-lookup"><span data-stu-id="2f9a2-139">Depending on your network connection and hello size of your VHD file, this command may take a while toocomplete.</span></span>


## <a name="option-2-copy-hello-vhd-from-an-existing-azure-vm"></a><span data-ttu-id="2f9a2-140">Opcja 2: Kopiowanie hello wirtualnego dysku twardego z istniejącej maszyny Wirtualnej Azure</span><span class="sxs-lookup"><span data-stu-id="2f9a2-140">Option 2: Copy hello VHD from an existing Azure VM</span></span>

<span data-ttu-id="2f9a2-141">Możesz skopiować toouse konta wirtualnego dysku twardego tooanother magazynu podczas tworzenia nowego, zduplikowany maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="2f9a2-141">You can copy a VHD tooanother storage account toouse when creating a new, duplicate VM.</span></span>

### <a name="before-you-begin"></a><span data-ttu-id="2f9a2-142">Przed rozpoczęciem</span><span class="sxs-lookup"><span data-stu-id="2f9a2-142">Before you begin</span></span>
<span data-ttu-id="2f9a2-143">Upewnij się, że możesz:</span><span class="sxs-lookup"><span data-stu-id="2f9a2-143">Make sure that you:</span></span>

* <span data-ttu-id="2f9a2-144">Informacje o hello **konta magazynu źródłowego i docelowego**.</span><span class="sxs-lookup"><span data-stu-id="2f9a2-144">Have information about hello **source and destination storage accounts**.</span></span> <span data-ttu-id="2f9a2-145">Witaj źródłowej maszyny Wirtualnej należy toohave hello magazynu konto i kontener nazwy.</span><span class="sxs-lookup"><span data-stu-id="2f9a2-145">For hello source VM, you need toohave hello storage account and container names.</span></span> <span data-ttu-id="2f9a2-146">Zazwyczaj nazwa kontenera hello będzie **wirtualne dyski twarde**.</span><span class="sxs-lookup"><span data-stu-id="2f9a2-146">Usually, hello container name will be **vhds**.</span></span> <span data-ttu-id="2f9a2-147">Należy również toohave konto magazynu docelowego.</span><span class="sxs-lookup"><span data-stu-id="2f9a2-147">You also need toohave a destination storage account.</span></span> <span data-ttu-id="2f9a2-148">Jeśli nie masz jeszcze jeden, można utworzyć przy użyciu portalu albo hello (**więcej usług** > kont magazynu > Dodaj) lub przy użyciu hello [New-AzureRmStorageAccount](/powershell/module/azurerm.storage/new-azurermstorageaccount) polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="2f9a2-148">If you don't already have one, you can create one using either hello portal (**More Services** > Storage accounts > Add) or using hello [New-AzureRmStorageAccount](/powershell/module/azurerm.storage/new-azurermstorageaccount) cmdlet.</span></span> 
* <span data-ttu-id="2f9a2-149">Zostały pobrane i zainstalowane hello [narzędzia AzCopy](../../storage/common/storage-use-azcopy.md).</span><span class="sxs-lookup"><span data-stu-id="2f9a2-149">Have downloaded and installed hello [AzCopy tool](../../storage/common/storage-use-azcopy.md).</span></span> 

### <a name="deallocate-hello-vm"></a><span data-ttu-id="2f9a2-150">Cofnięcie przydziału hello maszyny Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="2f9a2-150">Deallocate hello VM</span></span>
<span data-ttu-id="2f9a2-151">Cofnięcie przydziału hello maszyny Wirtualnej, co zwalnia hello toobe VHD kopiowane.</span><span class="sxs-lookup"><span data-stu-id="2f9a2-151">Deallocate hello VM, which frees up hello VHD toobe copied.</span></span> 

* <span data-ttu-id="2f9a2-152">**Portal**: kliknij **maszyn wirtualnych** > **myVM** > Zatrzymaj</span><span class="sxs-lookup"><span data-stu-id="2f9a2-152">**Portal**: Click **Virtual machines** > **myVM** > Stop</span></span>
* <span data-ttu-id="2f9a2-153">**PowerShell**: Użyj [Stop-AzureRmVM](/powershell/module/azurerm.compute/stop-azurermvm) toostop (deallocate) hello maszyny Wirtualnej o nazwie **myVM** w grupie zasobów **myResourceGroup**.</span><span class="sxs-lookup"><span data-stu-id="2f9a2-153">**Powershell**: Use [Stop-AzureRmVM](/powershell/module/azurerm.compute/stop-azurermvm) toostop (deallocate) hello VM named **myVM** in resource group **myResourceGroup**.</span></span>

```powershell
Stop-AzureRmVM -ResourceGroupName myResourceGroup -Name myVM
```

<span data-ttu-id="2f9a2-154">Witaj **stan** dla hello maszyny Wirtualnej w hello Azure portal zmieni się z **zatrzymane** za**zatrzymane (cofnięciu przydziału)**.</span><span class="sxs-lookup"><span data-stu-id="2f9a2-154">hello **Status** for hello VM in hello Azure portal changes from **Stopped** too**Stopped (deallocated)**.</span></span>

### <a name="get-hello-storage-account-urls"></a><span data-ttu-id="2f9a2-155">Uzyskiwanie adresów URL konta magazynu hello</span><span class="sxs-lookup"><span data-stu-id="2f9a2-155">Get hello storage account URLs</span></span>
<span data-ttu-id="2f9a2-156">Należy adresy URL hello hello kont magazynu źródłowego i docelowego.</span><span class="sxs-lookup"><span data-stu-id="2f9a2-156">You need hello URLs of hello source and destination storage accounts.</span></span> <span data-ttu-id="2f9a2-157">Witaj adresy URL wyglądać: `https://<storageaccount>.blob.core.windows.net/<containerName>/`.</span><span class="sxs-lookup"><span data-stu-id="2f9a2-157">hello URLs look like: `https://<storageaccount>.blob.core.windows.net/<containerName>/`.</span></span> <span data-ttu-id="2f9a2-158">Jeśli znasz już nazwę konta i kontener magazynu hello, można po prostu zastąpić hello informacji między toocreate nawiasy hello adres URL.</span><span class="sxs-lookup"><span data-stu-id="2f9a2-158">If you already know hello storage account and container name, you can just replace hello information between hello brackets toocreate your URL.</span></span> 

<span data-ttu-id="2f9a2-159">Program hello portalu Azure lub adres URL hello tooget programu Azure Powershell:</span><span class="sxs-lookup"><span data-stu-id="2f9a2-159">You can use hello Azure portal or Azure Powershell tooget hello URL:</span></span>

* <span data-ttu-id="2f9a2-160">**Portal**: kliknij hello  **>**  dla **więcej usług** > **kont magazynu**  >   *Konto magazynu* > **obiekty BLOB** i pliku wirtualnego dysku twardego źródłowego prawdopodobnie znajduje się w hello **wirtualne dyski twarde** kontenera.</span><span class="sxs-lookup"><span data-stu-id="2f9a2-160">**Portal**: Click hello **>** for **More services** > **Storage accounts** > *storage account* > **Blobs** and your source VHD file is probably in hello **vhds** container.</span></span> <span data-ttu-id="2f9a2-161">Kliknij przycisk **właściwości** hello kontenera i skopiować tekst hello etykietą **adres URL**.</span><span class="sxs-lookup"><span data-stu-id="2f9a2-161">Click **Properties** for hello container, and copy hello text labeled **URL**.</span></span> <span data-ttu-id="2f9a2-162">Będziesz potrzebować adresy URL hello kontenerów zarówno hello źródłowym i docelowym.</span><span class="sxs-lookup"><span data-stu-id="2f9a2-162">You'll need hello URLs of both hello source and destination containers.</span></span> 
* <span data-ttu-id="2f9a2-163">**PowerShell**: Użyj [Get-AzureRmVM](/powershell/module/azurerm.compute/get-azurermvm) tooget hello informacje dotyczące maszyny Wirtualnej o nazwie **myVM** w grupie zasobów hello **myResourceGroup**.</span><span class="sxs-lookup"><span data-stu-id="2f9a2-163">**Powershell**: Use [Get-AzureRmVM](/powershell/module/azurerm.compute/get-azurermvm) tooget hello information for VM named **myVM** in hello resource group **myResourceGroup**.</span></span> <span data-ttu-id="2f9a2-164">W wynikach hello Szukaj w hello **profilu magazynu** sekcji hello **identyfikator Uri dysku Vhd**.</span><span class="sxs-lookup"><span data-stu-id="2f9a2-164">In hello results, look in hello **Storage profile** section for hello **Vhd Uri**.</span></span> <span data-ttu-id="2f9a2-165">Pierwsza część identyfikatora Uri hello Hello jest kontenerem toohello adres URL hello i hello ostatniej części jest hello nazwę wirtualnego dysku twardego systemu operacyjnego hello maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="2f9a2-165">hello first part of hello Uri is hello URL toohello container and hello last part is hello OS VHD name for hello VM.</span></span>

```powershell
Get-AzureRmVM -ResourceGroupName "myResourceGroup" -Name "myVM"
``` 

## <a name="get-hello-storage-access-keys"></a><span data-ttu-id="2f9a2-166">Uzyskaj klucze dostępu do magazynu hello</span><span class="sxs-lookup"><span data-stu-id="2f9a2-166">Get hello storage access keys</span></span>
<span data-ttu-id="2f9a2-167">Znajdź hello klucze dostępu dla hello konta magazynu źródłowego i docelowego.</span><span class="sxs-lookup"><span data-stu-id="2f9a2-167">Find hello access keys for hello source and destination storage accounts.</span></span> <span data-ttu-id="2f9a2-168">Aby uzyskać więcej informacji na temat kluczy dostępu, zobacz [kont magazynu Azure o](../../storage/common/storage-create-storage-account.md).</span><span class="sxs-lookup"><span data-stu-id="2f9a2-168">For more information about access keys, see [About Azure storage accounts](../../storage/common/storage-create-storage-account.md).</span></span>

* <span data-ttu-id="2f9a2-169">**Portal**: kliknij **więcej usług** > **kont magazynu** > *konta magazynu*  >  **Klucze dostępu**.</span><span class="sxs-lookup"><span data-stu-id="2f9a2-169">**Portal**: Click **More services** > **Storage accounts** > *storage account* > **Access keys**.</span></span> <span data-ttu-id="2f9a2-170">Kopia klucza hello oznaczone jako **klucz1**.</span><span class="sxs-lookup"><span data-stu-id="2f9a2-170">Copy hello key labeled as **key1**.</span></span>
* <span data-ttu-id="2f9a2-171">**PowerShell**: Użyj [Get-AzureRmStorageAccountKey](/powershell/module/azurerm.storage/get-azurermstorageaccountkey) tooget hello magazynu klucza dla konta magazynu hello **mojekontomagazynu** w grupie zasobów hello  **myResourceGroup**.</span><span class="sxs-lookup"><span data-stu-id="2f9a2-171">**Powershell**: Use [Get-AzureRmStorageAccountKey](/powershell/module/azurerm.storage/get-azurermstorageaccountkey) tooget hello storage key for hello storage account **mystorageaccount** in hello resource group **myResourceGroup**.</span></span> <span data-ttu-id="2f9a2-172">Kopia klucza hello etykietą **klucz1**.</span><span class="sxs-lookup"><span data-stu-id="2f9a2-172">Copy hello key labeled **key1**.</span></span>

```powershell
Get-AzureRmStorageAccountKey -Name mystorageaccount -ResourceGroupName myResourceGroup
```

### <a name="copy-hello-vhd"></a><span data-ttu-id="2f9a2-173">Skopiuj hello wirtualnego dysku twardego</span><span class="sxs-lookup"><span data-stu-id="2f9a2-173">Copy hello VHD</span></span>
<span data-ttu-id="2f9a2-174">Możesz skopiować pliki między kontami magazynu przy użyciu narzędzia AzCopy.</span><span class="sxs-lookup"><span data-stu-id="2f9a2-174">You can copy files between storage accounts using AzCopy.</span></span> <span data-ttu-id="2f9a2-175">Witaj docelowy kontener Jeśli hello określony kontener nie istnieje, jej zostanie utworzona automatycznie.</span><span class="sxs-lookup"><span data-stu-id="2f9a2-175">For hello destination container, if hello specified container doesn't exist, it will be created for you.</span></span> 

<span data-ttu-id="2f9a2-176">toouse AzCopy, otwórz wiersz polecenia na komputerze lokalnym i przejdź folder toohello, w którym zainstalowano narzędzia AzCopy.</span><span class="sxs-lookup"><span data-stu-id="2f9a2-176">toouse AzCopy, open a command prompt on your local machine and navigate toohello folder where AzCopy is installed.</span></span> <span data-ttu-id="2f9a2-177">Będzie on podobny zbyt*\Microsoft SDKs\Azure\AzCopy C:\Program Files (x86)*.</span><span class="sxs-lookup"><span data-stu-id="2f9a2-177">It will be similar too*C:\Program Files (x86)\Microsoft SDKs\Azure\AzCopy*.</span></span> 

<span data-ttu-id="2f9a2-178">toocopy hello wszystkie pliki znajdujące się w kontenerze, użyj hello **/S** przełącznika.</span><span class="sxs-lookup"><span data-stu-id="2f9a2-178">toocopy all of hello files within a container, you use hello **/S** switch.</span></span> <span data-ttu-id="2f9a2-179">Może to być używane toocopy hello wirtualnego dysku twardego systemu operacyjnego i wszystkich dysków danych hello, jeśli są one hello tego samego kontenera.</span><span class="sxs-lookup"><span data-stu-id="2f9a2-179">This can be used toocopy hello OS VHD and all of hello data disks if they are in hello same container.</span></span> <span data-ttu-id="2f9a2-180">W tym przykładzie pokazano sposób toocopy wszystkie hello pliki w kontenerze hello **mysourcecontainer** na koncie magazynu **mysourcestorageaccount** kontenera toohello **mydestinationcontainer**  w hello **mydestinationstorageaccount** konta magazynu.</span><span class="sxs-lookup"><span data-stu-id="2f9a2-180">This example shows how toocopy all of hello files in hello container **mysourcecontainer** in storage account **mysourcestorageaccount** toohello container **mydestinationcontainer** in hello **mydestinationstorageaccount** storage account.</span></span> <span data-ttu-id="2f9a2-181">Zamień na powitania nazw kont magazynu hello i kontenery własne.</span><span class="sxs-lookup"><span data-stu-id="2f9a2-181">Replace hello names of hello storage accounts and containers with your own.</span></span> <span data-ttu-id="2f9a2-182">Zastąp `<sourceStorageAccountKey1>` i `<destinationStorageAccountKey1>` z własnych kluczy.</span><span class="sxs-lookup"><span data-stu-id="2f9a2-182">Replace `<sourceStorageAccountKey1>` and `<destinationStorageAccountKey1>` with your own keys.</span></span>

```
AzCopy /Source:https://mysourcestorageaccount.blob.core.windows.net/mysourcecontainer `
    /Dest:https://mydestinationatorageaccount.blob.core.windows.net/mydestinationcontainer `
    /SourceKey:<sourceStorageAccountKey1> /DestKey:<destinationStorageAccountKey1> /S
```

<span data-ttu-id="2f9a2-183">Jeśli chcesz tylko toocopy konkretnego dysku VHD w kontenerze z wieloma plikami, można również określić nazwę pliku hello za pomocą przełącznika /Pattern hello.</span><span class="sxs-lookup"><span data-stu-id="2f9a2-183">If you only want toocopy a specific VHD in a container with multiple files, you can also specify hello file name using hello /Pattern switch.</span></span> <span data-ttu-id="2f9a2-184">W tym przykładzie tylko hello plik o nazwie **myFileName.vhd** zostaną skopiowane.</span><span class="sxs-lookup"><span data-stu-id="2f9a2-184">In this example, only hello file named **myFileName.vhd** will be copied.</span></span>

```
AzCopy /Source:https://mysourcestorageaccount.blob.core.windows.net/mysourcecontainer `
  /Dest:https://mydestinationatorageaccount.blob.core.windows.net/mydestinationcontainer `
  /SourceKey:<sourceStorageAccountKey1> /DestKey:<destinationStorageAccountKey1> `
  /Pattern:myFileName.vhd
```


<span data-ttu-id="2f9a2-185">Po zakończeniu otrzymasz wiadomość, która wygląda:</span><span class="sxs-lookup"><span data-stu-id="2f9a2-185">When it is finished, you will get a message that looks something like:</span></span>

```
Finished 2 of total 2 file(s).
[2016/10/07 17:37:41] Transfer summary:
-----------------
Total files transferred: 2
Transfer successfully:   2
Transfer skipped:        0
Transfer failed:         0
Elapsed time:            00.00:13:07
```

### <a name="troubleshooting"></a><span data-ttu-id="2f9a2-186">Rozwiązywanie problemów</span><span class="sxs-lookup"><span data-stu-id="2f9a2-186">Troubleshooting</span></span>
* <span data-ttu-id="2f9a2-187">Korzystając z narzędzia AZCopy, jeśli zostanie wyświetlony błąd hello "Serwer nie powiodło się Żądanie hello tooauthenticate", upewnij się, że hello wartość nagłówka autoryzacji hello jest sformatowany poprawnie tym hello podpisu.</span><span class="sxs-lookup"><span data-stu-id="2f9a2-187">When you use AZCopy, if you see hello error "Server failed tooauthenticate hello request", make sure hello value of hello Authorization header is formed correctly including hello signature.</span></span> <span data-ttu-id="2f9a2-188">Jeśli korzystasz z 2 klucza lub klucza pomocniczego magazynu hello, spróbuj użyć hello klucz podstawowy lub 1 magazynu.</span><span class="sxs-lookup"><span data-stu-id="2f9a2-188">If you are using Key 2 or hello secondary storage key, try using hello primary or 1st storage key.</span></span>

## <a name="create-hello-new-vm"></a><span data-ttu-id="2f9a2-189">Utwórz hello nowej maszyny Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="2f9a2-189">Create hello new VM</span></span> 

<span data-ttu-id="2f9a2-190">Należy toocreate sieci i innych toobe zasoby maszyn wirtualnych używanych przez hello nowej maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="2f9a2-190">You need toocreate networking and other VM resources toobe used by hello new VM.</span></span>

### <a name="create-hello-subnet-and-vnet"></a><span data-ttu-id="2f9a2-191">Tworzenie hello podsieci i sieci wirtualnej</span><span class="sxs-lookup"><span data-stu-id="2f9a2-191">Create hello subNet and vNet</span></span>

<span data-ttu-id="2f9a2-192">Tworzenie sieci wirtualnej hello i podsieci hello [sieci wirtualnej](../../virtual-network/virtual-networks-overview.md).</span><span class="sxs-lookup"><span data-stu-id="2f9a2-192">Create hello vNet and subNet of hello [virtual network](../../virtual-network/virtual-networks-overview.md).</span></span>

1. <span data-ttu-id="2f9a2-193">Utwórz podsieć hello.</span><span class="sxs-lookup"><span data-stu-id="2f9a2-193">Create hello subNet.</span></span> <span data-ttu-id="2f9a2-194">W tym przykładzie tworzy podsieć o nazwie **mySubNet**, w grupie zasobów hello **myResourceGroup**, i ustawia prefiks adresu podsieci hello zbyt**10.0.0.0/24**.</span><span class="sxs-lookup"><span data-stu-id="2f9a2-194">This example creates a subnet named **mySubNet**, in hello resource group **myResourceGroup**, and sets hello subnet address prefix too**10.0.0.0/24**.</span></span>
   
    ```powershell
    $rgName = "myResourceGroup"
    $subnetName = "mySubNet"
    $singleSubnet = New-AzureRmVirtualNetworkSubnetConfig -Name $subnetName -AddressPrefix 10.0.0.0/24
    ```
2. <span data-ttu-id="2f9a2-195">Utwórz sieć wirtualną hello.</span><span class="sxs-lookup"><span data-stu-id="2f9a2-195">Create hello vNet.</span></span> <span data-ttu-id="2f9a2-196">W tym przykładzie zestawy hello toobe nazwa sieci wirtualnej **myVnetName**, zbyt hello lokalizacji**zachodnie stany USA**, i hello prefiks adresu sieci wirtualnej hello zbyt**10.0.0.0/16**.</span><span class="sxs-lookup"><span data-stu-id="2f9a2-196">This example sets hello virtual network name toobe **myVnetName**, hello location too**West US**, and hello address prefix for hello virtual network too**10.0.0.0/16**.</span></span> 
   
    ```powershell
    $location = "West US"
    $vnetName = "myVnetName"
    $vnet = New-AzureRmVirtualNetwork -Name $vnetName -ResourceGroupName $rgName -Location $location `
        -AddressPrefix 10.0.0.0/16 -Subnet $singleSubnet
    ```    

### <a name="create-a-public-ip-address-and-nic"></a><span data-ttu-id="2f9a2-197">Tworzenie publicznego adresu IP i karty Sieciowej</span><span class="sxs-lookup"><span data-stu-id="2f9a2-197">Create a public IP address and NIC</span></span>
<span data-ttu-id="2f9a2-198">tooenable komunikację z maszyną wirtualną hello w sieci wirtualnej hello, należy [publicznego adresu IP](../../virtual-network/virtual-network-ip-addresses-overview-arm.md) i interfejsu sieciowego.</span><span class="sxs-lookup"><span data-stu-id="2f9a2-198">tooenable communication with hello virtual machine in hello virtual network, you need a [public IP address](../../virtual-network/virtual-network-ip-addresses-overview-arm.md) and a network interface.</span></span>

1. <span data-ttu-id="2f9a2-199">Utwórz hello publicznego adresu IP.</span><span class="sxs-lookup"><span data-stu-id="2f9a2-199">Create hello public IP.</span></span> <span data-ttu-id="2f9a2-200">W tym przykładzie ustawiono zbyt hello nazwa publicznego adresu IP**myIP**.</span><span class="sxs-lookup"><span data-stu-id="2f9a2-200">In this example, hello public IP address name is set too**myIP**.</span></span>
   
    ```powershell
    $ipName = "myIP"
    $pip = New-AzureRmPublicIpAddress -Name $ipName -ResourceGroupName $rgName -Location $location `
        -AllocationMethod Dynamic
    ```       
2. <span data-ttu-id="2f9a2-201">Utwórz hello karty sieciowej.</span><span class="sxs-lookup"><span data-stu-id="2f9a2-201">Create hello NIC.</span></span> <span data-ttu-id="2f9a2-202">W tym przykładzie ustawiono zbyt nazwy kart hello**myNicName**.</span><span class="sxs-lookup"><span data-stu-id="2f9a2-202">In this example, hello NIC name is set too**myNicName**.</span></span>
   
    ```powershell
    $nicName = "myNicName"
    $nic = New-AzureRmNetworkInterface -Name $nicName -ResourceGroupName $rgName `
    -Location $location -SubnetId $vnet.Subnets[0].Id -PublicIpAddressId $pip.Id
    ```

### <a name="create-hello-network-security-group-and-an-rdp-rule"></a><span data-ttu-id="2f9a2-203">Tworzenie grupy zabezpieczeń sieci hello i reguły protokołu RDP</span><span class="sxs-lookup"><span data-stu-id="2f9a2-203">Create hello network security group and an RDP rule</span></span>
<span data-ttu-id="2f9a2-204">toobe stanie toolog w tooyour maszyny Wirtualnej przy użyciu protokołu RDP, należy toohave regułę zabezpieczeń, która pozwala dostępu RDP do portu 3389.</span><span class="sxs-lookup"><span data-stu-id="2f9a2-204">toobe able toolog in tooyour VM using RDP, you need toohave an security rule that allows RDP access on port 3389.</span></span> <span data-ttu-id="2f9a2-205">Ponieważ specjalizowany hello wirtualnego dysku twardego dla hello utworzenia nowej maszyny Wirtualnej z istniejącego maszyny Wirtualnej, po utworzeniu hello maszyny Wirtualnej, należy użyć istniejącego konta z hello źródłowa maszyna wirtualna mająca uprawnienia toolog przy użyciu protokołu RDP.</span><span class="sxs-lookup"><span data-stu-id="2f9a2-205">Because hello VHD for hello new VM was created from an existing specialized VM, after hello VM is created you can use an existing account from hello source virtual machine that had permission toolog on using RDP.</span></span>
<span data-ttu-id="2f9a2-206">W tym przykładzie zestawy hello Nazwa grupy NSG zbyt**myNsg** i hello RDP Nazwa reguły zbyt**myRdpRule**.</span><span class="sxs-lookup"><span data-stu-id="2f9a2-206">This example sets hello NSG name too**myNsg** and hello RDP rule name too**myRdpRule**.</span></span>

```powershell
$nsgName = "myNsg"

$rdpRule = New-AzureRmNetworkSecurityRuleConfig -Name myRdpRule -Description "Allow RDP" `
    -Access Allow -Protocol Tcp -Direction Inbound -Priority 110 `
    -SourceAddressPrefix Internet -SourcePortRange * `
    -DestinationAddressPrefix * -DestinationPortRange 3389
$nsg = New-AzureRmNetworkSecurityGroup -ResourceGroupName $rgName -Location $location `
    -Name $nsgName -SecurityRules $rdpRule
    
```

<span data-ttu-id="2f9a2-207">Aby uzyskać więcej informacji na temat punktów końcowych i reguły NSG, zobacz [otwierania portów tooa maszyny Wirtualnej na platformie Azure przy użyciu programu PowerShell](nsg-quickstart-powershell.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="2f9a2-207">For more information about endpoints and NSG rules, see [Opening ports tooa VM in Azure using PowerShell](nsg-quickstart-powershell.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

### <a name="set-hello-vm-name-and-size"></a><span data-ttu-id="2f9a2-208">Nazwa maszyny Wirtualnej hello zestawu i rozmiaru</span><span class="sxs-lookup"><span data-stu-id="2f9a2-208">Set hello VM name and size</span></span>

<span data-ttu-id="2f9a2-209">W tym przykładzie zestawy hello nazwę maszyny Wirtualnej za "myVM" i hello wirtualna rozmiaru zbyt "Standard_A2".</span><span class="sxs-lookup"><span data-stu-id="2f9a2-209">This example sets hello VM name too"myVM" and hello VM size too"Standard_A2".</span></span>
```powershell
$vmName = "myVM"
$vmConfig = New-AzureRmVMConfig -VMName $vmName -VMSize "Standard_A2"
```

### <a name="add-hello-nic"></a><span data-ttu-id="2f9a2-210">Dodaj hello karty Sieciowej</span><span class="sxs-lookup"><span data-stu-id="2f9a2-210">Add hello NIC</span></span>
    
```powershell
$vm = Add-AzureRmVMNetworkInterface -VM $vmConfig -Id $nic.Id
```
    
    
### <a name="configure-hello-os-disk"></a><span data-ttu-id="2f9a2-211">Skonfiguruj dysk hello systemu operacyjnego</span><span class="sxs-lookup"><span data-stu-id="2f9a2-211">Configure hello OS disk</span></span>

1. <span data-ttu-id="2f9a2-212">Ustaw hello identyfikatora URI dla hello wirtualnego dysku twardego, który został przekazany lub skopiowany.</span><span class="sxs-lookup"><span data-stu-id="2f9a2-212">Set hello URI for hello VHD that you uploaded or copied.</span></span> <span data-ttu-id="2f9a2-213">W tym przykładzie hello plik wirtualnego dysku twardego o nazwie **myOsDisk.vhd** jest przechowywana na koncie magazynu o nazwie **Mojekontomagazynu** w kontenerze o nazwie **Mojkontener**.</span><span class="sxs-lookup"><span data-stu-id="2f9a2-213">In this example, hello VHD file named **myOsDisk.vhd** is kept in a storage account named **myStorageAccount** in a container named **myContainer**.</span></span>

    ```powershell
    $osDiskUri = "https://myStorageAccount.blob.core.windows.net/myContainer/myOsDisk.vhd"
    ```
2. <span data-ttu-id="2f9a2-214">Dodaj dysk hello systemu operacyjnego.</span><span class="sxs-lookup"><span data-stu-id="2f9a2-214">Add hello OS disk.</span></span> <span data-ttu-id="2f9a2-215">Po utworzeniu hello dysk systemu operacyjnego, w tym przykładzie hello termin "osDisk" jest appened toohello wirtualna nazwa toocreate hello nazwa dysku systemu operacyjnego.</span><span class="sxs-lookup"><span data-stu-id="2f9a2-215">In this example, when hello OS disk is created, hello term "osDisk" is appened toohello VM name toocreate hello OS disk name.</span></span> <span data-ttu-id="2f9a2-216">W tym przykładzie określa również, że tego dysku VHD systemu Windows powinna być dołączone toohello maszyny Wirtualnej jako dysk systemu operacyjnego hello.</span><span class="sxs-lookup"><span data-stu-id="2f9a2-216">This example also specifies that this Windows-based VHD should be attached toohello VM as hello OS disk.</span></span>
    
    ```powershell
    $osDiskName = $vmName + "osDisk"
    $vm = Set-AzureRmVMOSDisk -VM $vm -Name $osDiskName -VhdUri $osDiskUri -CreateOption attach -Windows
    ```

<span data-ttu-id="2f9a2-217">Opcjonalnie: Jeśli masz dysków z danymi tego toobe potrzeby dołączony toohello maszyny Wirtualnej, dodać hello dysków z danymi przy użyciu adresów URL hello danych wirtualne dyski twarde i hello odpowiedni numer jednostki logicznej (Lun).</span><span class="sxs-lookup"><span data-stu-id="2f9a2-217">Optional: If you have data disks that need toobe attached toohello VM, add hello data disks by using hello URLs of data VHDs and hello appropriate Logical Unit Number (Lun).</span></span>

```powershell
$dataDiskName = $vmName + "dataDisk"
$vm = Add-AzureRmVMDataDisk -VM $vm -Name $dataDiskName -VhdUri $dataDiskUri -Lun 1 -CreateOption attach
```

<span data-ttu-id="2f9a2-218">Korzystając z konta magazynu, adresy URL dysku systemu operacyjnego i danych hello wyglądać mniej więcej tak: `https://StorageAccountName.blob.core.windows.net/BlobContainerName/DiskName.vhd`.</span><span class="sxs-lookup"><span data-stu-id="2f9a2-218">When using a storage account, hello data and operating system disk URLs look something like this: `https://StorageAccountName.blob.core.windows.net/BlobContainerName/DiskName.vhd`.</span></span> <span data-ttu-id="2f9a2-219">To w portalu hello można znaleźć przy przeglądanie kontenera magazynu docelowego toohello, klikając hello systemu operacyjnego lub dane wirtualnego dysku twardego, która została skopiowana, a następnie skopiować zawartość hello hello adresu URL.</span><span class="sxs-lookup"><span data-stu-id="2f9a2-219">You can find this on hello portal by browsing toohello target storage container, clicking hello operating system or data VHD that was copied, and then copying hello contents of hello URL.</span></span>


### <a name="complete-hello-vm"></a><span data-ttu-id="2f9a2-220">Ukończyć powitalnych maszyny Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="2f9a2-220">Complete hello VM</span></span> 

<span data-ttu-id="2f9a2-221">Utwórz hello maszyny Wirtualnej przy użyciu hello konfiguracje, które właśnie utworzyliśmy.</span><span class="sxs-lookup"><span data-stu-id="2f9a2-221">Create hello VM using hello configurations that we just created.</span></span>

```powershell
#Create hello new VM
New-AzureRmVM -ResourceGroupName $rgName -Location $location -VM $vm
```

<span data-ttu-id="2f9a2-222">Jeśli to polecenie zakończyło się pomyślnie, zostanie wyświetlone dane wyjściowe w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="2f9a2-222">If this command was successful, you'll see output like this:</span></span>

```powershell
RequestId IsSuccessStatusCode StatusCode ReasonPhrase
--------- ------------------- ---------- ------------
                         True         OK OK   

```

### <a name="verify-that-hello-vm-was-created"></a><span data-ttu-id="2f9a2-223">Sprawdź hello, że maszyna wirtualna została utworzona</span><span class="sxs-lookup"><span data-stu-id="2f9a2-223">Verify that hello VM was created</span></span>
<span data-ttu-id="2f9a2-224">Powinny pojawić się hello nowo utworzona maszyna wirtualna w hello [portalu Azure](https://portal.azure.com)w obszarze **Przeglądaj** > **maszyn wirtualnych**, lub za pomocą hello następującego środowiska PowerShell polecenia:</span><span class="sxs-lookup"><span data-stu-id="2f9a2-224">You should see hello newly created VM either in hello [Azure portal](https://portal.azure.com), under **Browse** > **Virtual machines**, or by using hello following PowerShell commands:</span></span>

```powershell
$vmList = Get-AzureRmVM -ResourceGroupName $rgName
$vmList.Name
```

## <a name="next-steps"></a><span data-ttu-id="2f9a2-225">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="2f9a2-225">Next steps</span></span>
<span data-ttu-id="2f9a2-226">toosign w tooyour nowej maszyny wirtualnej, przeglądania toohello maszyny Wirtualnej w hello [portal](https://portal.azure.com), kliknij przycisk **Connect**i hello Otwórz plik RDP pulpitu zdalnego.</span><span class="sxs-lookup"><span data-stu-id="2f9a2-226">toosign in tooyour new virtual machine, browse toohello VM in hello [portal](https://portal.azure.com), click **Connect**, and open hello Remote Desktop RDP file.</span></span> <span data-ttu-id="2f9a2-227">Użyj poświadczeń konta hello z oryginalnego toosign maszyny wirtualnej w tooyour nowej maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="2f9a2-227">Use hello account credentials of your original virtual machine toosign in tooyour new virtual machine.</span></span> <span data-ttu-id="2f9a2-228">Aby uzyskać więcej informacji, zobacz [jak dziennika na tooan wirtualnej platformy Azure i tooconnect maszyny, systemem operacyjnym Windows](connect-logon.md).</span><span class="sxs-lookup"><span data-stu-id="2f9a2-228">For more information, see [How tooconnect and log on tooan Azure virtual machine running Windows](connect-logon.md).</span></span>

