---
title: Tworzenie maszyny Wirtualnej z dysku specjalne na platformie Azure | Dokumentacja firmy Microsoft
description: "Dołączanie specjalne dysku niezarządzane, w modelu wdrażania usługi Resource Manager, aby utworzyć nową maszynę Wirtualną."
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
ms.openlocfilehash: 974d89aa96cba94fedfd1acbaf4f1d30ac8e6257
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
# <a name="create-a-vm-from-a-specialized-vhd-in-a-storage-account"></a><span data-ttu-id="6e21b-103">Utwórz maszynę Wirtualną z wirtualnego dysku twardego specjalne konta magazynu</span><span class="sxs-lookup"><span data-stu-id="6e21b-103">Create a VM from a specialized VHD in a storage account</span></span>

<span data-ttu-id="6e21b-104">Tworzenie nowej maszyny Wirtualnej przez dołączenie dysku niezarządzane specjalne jako dysk systemu operacyjnego przy użyciu programu Powershell.</span><span class="sxs-lookup"><span data-stu-id="6e21b-104">Create a new VM by attaching a specialized unmanaged disk as the OS disk using Powershell.</span></span> <span data-ttu-id="6e21b-105">Specjalne dysku jest kopią wirtualnego dysku twardego z istniejącej maszyny Wirtualnej, który przechowuje konta użytkowników, aplikacji i innych danych o stanie z oryginalnego maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="6e21b-105">A specialized disk is a copy of VHD from an existing VM that maintains the user accounts, applications and other state data from your original VM.</span></span> 

<span data-ttu-id="6e21b-106">Dostępne są dwie opcje:</span><span class="sxs-lookup"><span data-stu-id="6e21b-106">You have two options:</span></span>
* [<span data-ttu-id="6e21b-107">Przekazywanie wirtualnego dysku twardego</span><span class="sxs-lookup"><span data-stu-id="6e21b-107">Upload a VHD</span></span>](create-vm-specialized.md#option-1-upload-a-specialized-vhd)
* [<span data-ttu-id="6e21b-108">Skopiuj wirtualny dysk twardy z istniejącej maszyny Wirtualnej Azure</span><span class="sxs-lookup"><span data-stu-id="6e21b-108">Copy the VHD of an existing Azure VM</span></span>](create-vm-specialized.md#option-2-copy-an-existing-azure-vm)

## <a name="before-you-begin"></a><span data-ttu-id="6e21b-109">Przed rozpoczęciem</span><span class="sxs-lookup"><span data-stu-id="6e21b-109">Before you begin</span></span>
<span data-ttu-id="6e21b-110">Jeśli używasz programu PowerShell, upewnij się, że masz najnowszą wersję modułu programu AzureRM.Compute PowerShell.</span><span class="sxs-lookup"><span data-stu-id="6e21b-110">If you use PowerShell, make sure that you have the latest version of the AzureRM.Compute PowerShell module.</span></span> <span data-ttu-id="6e21b-111">Uruchom następujące polecenie, aby go zainstalować.</span><span class="sxs-lookup"><span data-stu-id="6e21b-111">Run the following command to install it.</span></span>

```powershell
Install-Module AzureRM.Compute 
```
<span data-ttu-id="6e21b-112">Aby uzyskać więcej informacji, zobacz [przechowywanie wersji programu Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="6e21b-112">For more information, see [Azure PowerShell Versioning](/powershell/azure/overview).</span></span>


## <a name="option-1-upload-a-specialized-vhd"></a><span data-ttu-id="6e21b-113">Opcja 1: Przekazanie specjalne dysku VHD</span><span class="sxs-lookup"><span data-stu-id="6e21b-113">Option 1: Upload a specialized VHD</span></span>

<span data-ttu-id="6e21b-114">Możesz przekazać wirtualnego dysku twardego z specjalne utworzone za pomocą wirtualizacji narzędzia lokalnych, takich jak funkcja Hyper-V lub maszyny Wirtualnej wyeksportowane z innej maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="6e21b-114">You can upload the VHD from a specialized VM created with an on-premises virtualization tool, like Hyper-V, or a VM exported from another cloud.</span></span>

### <a name="prepare-the-vm"></a><span data-ttu-id="6e21b-115">Przygotowywanie maszyny wirtualnej</span><span class="sxs-lookup"><span data-stu-id="6e21b-115">Prepare the VM</span></span>
<span data-ttu-id="6e21b-116">Możesz przekazać specjalne wirtualnego dysku twardego, który został utworzony przy użyciu lokalnej maszyny Wirtualnej lub wirtualnego dysku twardego wyeksportowane z innej chmury.</span><span class="sxs-lookup"><span data-stu-id="6e21b-116">You can upload a specialized VHD that was created using an on-premises VM or a VHD exported from another cloud.</span></span> <span data-ttu-id="6e21b-117">Specjalne wirtualnego dysku twardego przechowuje konta użytkowników, aplikacji i innych danych o stanie z oryginalnego maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="6e21b-117">A specialized VHD maintains the user accounts, applications and other state data from your original VM.</span></span> <span data-ttu-id="6e21b-118">Jeśli zamierzasz używać wirtualnego dysku twardego jako — jest, aby utworzyć nową maszynę Wirtualną, upewnij się, wykonywane są następujące czynności.</span><span class="sxs-lookup"><span data-stu-id="6e21b-118">If you intend to use the VHD as-is to create a new VM, ensure the following steps are completed.</span></span> 
  
  * <span data-ttu-id="6e21b-119">[Przygotowywanie dysku VHD systemu Windows, aby przekazać do usługi Azure](prepare-for-upload-vhd-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="6e21b-119">[Prepare a Windows VHD to upload to Azure](prepare-for-upload-vhd-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> <span data-ttu-id="6e21b-120">**Nie** generalize maszyny Wirtualnej za pomocą programu Sysprep.</span><span class="sxs-lookup"><span data-stu-id="6e21b-120">**Do not** generalize the VM using Sysprep.</span></span>
  * <span data-ttu-id="6e21b-121">Usuń wszystkie narzędzia wirtualizacji gościa i agentów, które są zainstalowane na maszynie Wirtualnej (np. narzędzi VMware).</span><span class="sxs-lookup"><span data-stu-id="6e21b-121">Remove any guest virtualization tools and agents that are installed on the VM (i.e. VMware tools).</span></span>
  * <span data-ttu-id="6e21b-122">Upewnij się, że maszyna wirtualna jest skonfigurowana do pobierania jego adres IP i ustawienia DNS za pośrednictwem protokołu DHCP.</span><span class="sxs-lookup"><span data-stu-id="6e21b-122">Ensure the VM is configured to pull its IP address and DNS settings via DHCP.</span></span> <span data-ttu-id="6e21b-123">Daje to pewność, że serwer uzyskuje adres IP w sieci wirtualnej podczas uruchamiania.</span><span class="sxs-lookup"><span data-stu-id="6e21b-123">This ensures that the server obtains an IP address within the VNet when it starts up.</span></span> 


### <a name="get-the-storage-account"></a><span data-ttu-id="6e21b-124">Uzyskaj konto magazynu</span><span class="sxs-lookup"><span data-stu-id="6e21b-124">Get the storage account</span></span>
<span data-ttu-id="6e21b-125">Potrzebujesz konta magazynu na platformie Azure do przechowywania załadowanego obrazu maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="6e21b-125">You need a storage account in Azure to store the uploaded VM image.</span></span> <span data-ttu-id="6e21b-126">Możesz użyć istniejącego konta magazynu lub Utwórz nową.</span><span class="sxs-lookup"><span data-stu-id="6e21b-126">You can either use an existing storage account or create a new one.</span></span> 

<span data-ttu-id="6e21b-127">Aby wyświetlić konta dostępny magazyn, wpisz:</span><span class="sxs-lookup"><span data-stu-id="6e21b-127">To show the available storage accounts, type:</span></span>

```powershell
Get-AzureRmStorageAccount
```

<span data-ttu-id="6e21b-128">Jeśli chcesz użyć istniejącego konta magazynu, przejdź do [przekazać obraz maszyny Wirtualnej](#upload-the-vm-vhd-to-your-storage-account) sekcji.</span><span class="sxs-lookup"><span data-stu-id="6e21b-128">If you want to use an existing storage account, proceed to the [Upload the VM image](#upload-the-vm-vhd-to-your-storage-account) section.</span></span>

<span data-ttu-id="6e21b-129">Jeśli musisz utworzyć konto magazynu, wykonaj następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="6e21b-129">If you need to create a storage account, follow these steps:</span></span>

1. <span data-ttu-id="6e21b-130">Potrzebna jest nazwa grupy zasobów, w którym ma zostać utworzony na koncie magazynu.</span><span class="sxs-lookup"><span data-stu-id="6e21b-130">You need the name of the resource group where the storage account should be created.</span></span> <span data-ttu-id="6e21b-131">Aby dowiedzieć się, wszystkie grupy zasobów, które są w ramach subskrypcji, wpisz:</span><span class="sxs-lookup"><span data-stu-id="6e21b-131">To find out all the resource groups that are in your subscription, type:</span></span>
   
    ```powershell
    Get-AzureRmResourceGroup
    ```

    <span data-ttu-id="6e21b-132">Aby utworzyć grupę zasobów o nazwie **myResourceGroup** w **zachodnie stany USA** regionu, wpisz:</span><span class="sxs-lookup"><span data-stu-id="6e21b-132">To create a resource group named **myResourceGroup** in the **West US** region, type:</span></span>

    ```powershell
    New-AzureRmResourceGroup -Name myResourceGroup -Location "West US"
    ```

2. <span data-ttu-id="6e21b-133">Utwórz konto magazynu o nazwie **mojekontomagazynu** w tej grupie zasobów za pomocą [New-AzureRmStorageAccount](/powershell/module/azurerm.storage/new-azurermstorageaccount) polecenia cmdlet:</span><span class="sxs-lookup"><span data-stu-id="6e21b-133">Create a storage account named **mystorageaccount** in this resource group by using the [New-AzureRmStorageAccount](/powershell/module/azurerm.storage/new-azurermstorageaccount) cmdlet:</span></span>
   
    ```powershell
    New-AzureRmStorageAccount -ResourceGroupName myResourceGroup -Name mystorageaccount -Location "West US" `
        -SkuName "Standard_LRS" -Kind "Storage"
    ```
   
### <a name="upload-the-vhd-to-your-storage-account"></a><span data-ttu-id="6e21b-134">Przekazanie dysku VHD do konta magazynu</span><span class="sxs-lookup"><span data-stu-id="6e21b-134">Upload the VHD to your storage account</span></span>
<span data-ttu-id="6e21b-135">Użyj [AzureRmVhd Dodaj](/powershell/module/azurerm.compute/add-azurermvhd) polecenia cmdlet, aby przekazać obraz do kontenera na koncie magazynu.</span><span class="sxs-lookup"><span data-stu-id="6e21b-135">Use the [Add-AzureRmVhd](/powershell/module/azurerm.compute/add-azurermvhd) cmdlet to upload the image to a container in your storage account.</span></span> <span data-ttu-id="6e21b-136">W tym przykładzie powoduje przekazanie pliku **myVHD.vhd** z `"C:\Users\Public\Documents\Virtual hard disks\"` na konto magazynu o nazwie **mojekontomagazynu** w **myResourceGroup** grupy zasobów.</span><span class="sxs-lookup"><span data-stu-id="6e21b-136">This example uploads the file **myVHD.vhd** from `"C:\Users\Public\Documents\Virtual hard disks\"` to a storage account named **mystorageaccount** in the **myResourceGroup** resource group.</span></span> <span data-ttu-id="6e21b-137">Plik zostaną umieszczone w kontenerze o nazwie **mojkontener** i Nowa nazwa pliku będzie **myUploadedVHD.vhd**.</span><span class="sxs-lookup"><span data-stu-id="6e21b-137">The file will be placed into the container named **mycontainer** and the new file name will be **myUploadedVHD.vhd**.</span></span>

```powershell
$rgName = "myResourceGroup"
$urlOfUploadedImageVhd = "https://mystorageaccount.blob.core.windows.net/mycontainer/myUploadedVHD.vhd"
Add-AzureRmVhd -ResourceGroupName $rgName -Destination $urlOfUploadedImageVhd `
    -LocalFilePath "C:\Users\Public\Documents\Virtual hard disks\myVHD.vhd"
```


<span data-ttu-id="6e21b-138">W przypadku powodzenia można uzyskać odpowiedzi, która wygląda podobnie do poniższego:</span><span class="sxs-lookup"><span data-stu-id="6e21b-138">If successful, you get a response that looks similar to this:</span></span>

```powershell
MD5 hash is being calculated for the file C:\Users\Public\Documents\Virtual hard disks\myVHD.vhd.
MD5 hash calculation is completed.
Elapsed time for the operation: 00:03:35
Creating new page blob of size 53687091712...
Elapsed time for upload: 01:12:49

LocalFilePath           DestinationUri
-------------           --------------
C:\Users\Public\Doc...  https://mystorageaccount.blob.core.windows.net/mycontainer/myUploadedVHD.vhd
```

<span data-ttu-id="6e21b-139">W zależności od połączenia sieciowego i rozmiar pliku VHD to polecenie może zająć trochę czasu, aby zakończyć.</span><span class="sxs-lookup"><span data-stu-id="6e21b-139">Depending on your network connection and the size of your VHD file, this command may take a while to complete.</span></span>


## <a name="option-2-copy-the-vhd-from-an-existing-azure-vm"></a><span data-ttu-id="6e21b-140">Opcja 2: Skopiuj wirtualny dysk twardy z istniejącej maszyny Wirtualnej Azure</span><span class="sxs-lookup"><span data-stu-id="6e21b-140">Option 2: Copy the VHD from an existing Azure VM</span></span>

<span data-ttu-id="6e21b-141">Wirtualny dysk twardy można skopiować do innego konta magazynu do użycia podczas tworzenia nowego, zduplikowany maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="6e21b-141">You can copy a VHD to another storage account to use when creating a new, duplicate VM.</span></span>

### <a name="before-you-begin"></a><span data-ttu-id="6e21b-142">Przed rozpoczęciem</span><span class="sxs-lookup"><span data-stu-id="6e21b-142">Before you begin</span></span>
<span data-ttu-id="6e21b-143">Upewnij się, że możesz:</span><span class="sxs-lookup"><span data-stu-id="6e21b-143">Make sure that you:</span></span>

* <span data-ttu-id="6e21b-144">Ma informacje o **konta magazynu źródłowego i docelowego**.</span><span class="sxs-lookup"><span data-stu-id="6e21b-144">Have information about the **source and destination storage accounts**.</span></span> <span data-ttu-id="6e21b-145">Dla źródłowej maszyny Wirtualnej musisz mieć nazwy konta i kontener magazynu.</span><span class="sxs-lookup"><span data-stu-id="6e21b-145">For the source VM, you need to have the storage account and container names.</span></span> <span data-ttu-id="6e21b-146">Zazwyczaj nazwa kontenera będzie **wirtualne dyski twarde**.</span><span class="sxs-lookup"><span data-stu-id="6e21b-146">Usually, the container name will be **vhds**.</span></span> <span data-ttu-id="6e21b-147">Należy również mieć konto magazynu docelowego.</span><span class="sxs-lookup"><span data-stu-id="6e21b-147">You also need to have a destination storage account.</span></span> <span data-ttu-id="6e21b-148">Jeśli nie masz jeszcze jeden, możesz utworzyć jedną przy użyciu albo portalu (**więcej usług** > kont magazynu > Dodaj) lub przy użyciu [New-AzureRmStorageAccount](/powershell/module/azurerm.storage/new-azurermstorageaccount) polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="6e21b-148">If you don't already have one, you can create one using either the portal (**More Services** > Storage accounts > Add) or using the [New-AzureRmStorageAccount](/powershell/module/azurerm.storage/new-azurermstorageaccount) cmdlet.</span></span> 
* <span data-ttu-id="6e21b-149">Zostały pobrane i zainstalowane [narzędzia AzCopy](../../storage/common/storage-use-azcopy.md).</span><span class="sxs-lookup"><span data-stu-id="6e21b-149">Have downloaded and installed the [AzCopy tool](../../storage/common/storage-use-azcopy.md).</span></span> 

### <a name="deallocate-the-vm"></a><span data-ttu-id="6e21b-150">Cofnięcie przydziału maszyny Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="6e21b-150">Deallocate the VM</span></span>
<span data-ttu-id="6e21b-151">Cofnięcie przydziału maszyny Wirtualnej, co zwalnia dysk VHD do skopiowania.</span><span class="sxs-lookup"><span data-stu-id="6e21b-151">Deallocate the VM, which frees up the VHD to be copied.</span></span> 

* <span data-ttu-id="6e21b-152">**Portal**: kliknij **maszyn wirtualnych** > **myVM** > Zatrzymaj</span><span class="sxs-lookup"><span data-stu-id="6e21b-152">**Portal**: Click **Virtual machines** > **myVM** > Stop</span></span>
* <span data-ttu-id="6e21b-153">**PowerShell**: Użyj [Stop-AzureRmVM](/powershell/module/azurerm.compute/stop-azurermvm) zatrzymania (deallocate) maszyny Wirtualnej o nazwie **myVM** w grupie zasobów **myResourceGroup**.</span><span class="sxs-lookup"><span data-stu-id="6e21b-153">**Powershell**: Use [Stop-AzureRmVM](/powershell/module/azurerm.compute/stop-azurermvm) to stop (deallocate) the VM named **myVM** in resource group **myResourceGroup**.</span></span>

```powershell
Stop-AzureRmVM -ResourceGroupName myResourceGroup -Name myVM
```

<span data-ttu-id="6e21b-154">**Stan** dla maszyny Wirtualnej na platformie Azure portal zmieni się z **zatrzymane** do **zatrzymane (cofnięciu przydziału)**.</span><span class="sxs-lookup"><span data-stu-id="6e21b-154">The **Status** for the VM in the Azure portal changes from **Stopped** to **Stopped (deallocated)**.</span></span>

### <a name="get-the-storage-account-urls"></a><span data-ttu-id="6e21b-155">Uzyskiwanie adresów URL konta magazynu</span><span class="sxs-lookup"><span data-stu-id="6e21b-155">Get the storage account URLs</span></span>
<span data-ttu-id="6e21b-156">Należy adresy URL konta magazynu źródłowego i docelowego.</span><span class="sxs-lookup"><span data-stu-id="6e21b-156">You need the URLs of the source and destination storage accounts.</span></span> <span data-ttu-id="6e21b-157">Adresy URL wygląda jak: `https://<storageaccount>.blob.core.windows.net/<containerName>/`.</span><span class="sxs-lookup"><span data-stu-id="6e21b-157">The URLs look like: `https://<storageaccount>.blob.core.windows.net/<containerName>/`.</span></span> <span data-ttu-id="6e21b-158">Jeśli znasz już nazwę konta i kontener magazynu, trzeba po prostu zastąpić informacji między nawiasy, aby utworzyć adres URL.</span><span class="sxs-lookup"><span data-stu-id="6e21b-158">If you already know the storage account and container name, you can just replace the information between the brackets to create your URL.</span></span> 

<span data-ttu-id="6e21b-159">Aby uzyskać adres URL, można użyć portalu Azure lub programu Azure Powershell:</span><span class="sxs-lookup"><span data-stu-id="6e21b-159">You can use the Azure portal or Azure Powershell to get the URL:</span></span>

* <span data-ttu-id="6e21b-160">**Portal**: kliknij  **>**  dla **więcej usług** > **kont magazynu**  >   *Konto magazynu* > **obiekty BLOB** i pliku wirtualnego dysku twardego źródłowego jest prawdopodobnie w **wirtualne dyski twarde** kontenera.</span><span class="sxs-lookup"><span data-stu-id="6e21b-160">**Portal**: Click the **>** for **More services** > **Storage accounts** > *storage account* > **Blobs** and your source VHD file is probably in the **vhds** container.</span></span> <span data-ttu-id="6e21b-161">Kliknij przycisk **właściwości** dla kontenera, a następnie skopiuj tekst, którego etykietą jest **adres URL**.</span><span class="sxs-lookup"><span data-stu-id="6e21b-161">Click **Properties** for the container, and copy the text labeled **URL**.</span></span> <span data-ttu-id="6e21b-162">Będziesz potrzebować adresy URL kontenery źródłowym i docelowym.</span><span class="sxs-lookup"><span data-stu-id="6e21b-162">You'll need the URLs of both the source and destination containers.</span></span> 
* <span data-ttu-id="6e21b-163">**PowerShell**: Użyj [Get-AzureRmVM](/powershell/module/azurerm.compute/get-azurermvm) Aby uzyskać informacje dotyczące maszyny Wirtualnej o nazwie **myVM** w grupie zasobów **myResourceGroup**.</span><span class="sxs-lookup"><span data-stu-id="6e21b-163">**Powershell**: Use [Get-AzureRmVM](/powershell/module/azurerm.compute/get-azurermvm) to get the information for VM named **myVM** in the resource group **myResourceGroup**.</span></span> <span data-ttu-id="6e21b-164">W wynikach wyszukiwania **profilu magazynu** sekcji **identyfikator Uri dysku Vhd**.</span><span class="sxs-lookup"><span data-stu-id="6e21b-164">In the results, look in the **Storage profile** section for the **Vhd Uri**.</span></span> <span data-ttu-id="6e21b-165">Pierwsza część identyfikatora Uri jest adres URL do kontenera i ostatniej części jest nazwa wirtualnego dysku twardego systemu operacyjnego dla maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="6e21b-165">The first part of the Uri is the URL to the container and the last part is the OS VHD name for the VM.</span></span>

```powershell
Get-AzureRmVM -ResourceGroupName "myResourceGroup" -Name "myVM"
``` 

## <a name="get-the-storage-access-keys"></a><span data-ttu-id="6e21b-166">Uzyskaj klucze dostępu do magazynu</span><span class="sxs-lookup"><span data-stu-id="6e21b-166">Get the storage access keys</span></span>
<span data-ttu-id="6e21b-167">Znajdź klucze dostępu dla serwera źródłowego i docelowego konta magazynu.</span><span class="sxs-lookup"><span data-stu-id="6e21b-167">Find the access keys for the source and destination storage accounts.</span></span> <span data-ttu-id="6e21b-168">Aby uzyskać więcej informacji na temat kluczy dostępu, zobacz [kont magazynu Azure o](../../storage/common/storage-create-storage-account.md).</span><span class="sxs-lookup"><span data-stu-id="6e21b-168">For more information about access keys, see [About Azure storage accounts](../../storage/common/storage-create-storage-account.md).</span></span>

* <span data-ttu-id="6e21b-169">**Portal**: kliknij **więcej usług** > **kont magazynu** > *konta magazynu*  >  **Klucze dostępu**.</span><span class="sxs-lookup"><span data-stu-id="6e21b-169">**Portal**: Click **More services** > **Storage accounts** > *storage account* > **Access keys**.</span></span> <span data-ttu-id="6e21b-170">Skopiuj klucz oznaczony jako **klucz1**.</span><span class="sxs-lookup"><span data-stu-id="6e21b-170">Copy the key labeled as **key1**.</span></span>
* <span data-ttu-id="6e21b-171">**PowerShell**: Użyj [Get-AzureRmStorageAccountKey](/powershell/module/azurerm.storage/get-azurermstorageaccountkey) można uzyskać klucza magazynu dla konta magazynu **mojekontomagazynu** w grupie zasobów **myResourceGroup**.</span><span class="sxs-lookup"><span data-stu-id="6e21b-171">**Powershell**: Use [Get-AzureRmStorageAccountKey](/powershell/module/azurerm.storage/get-azurermstorageaccountkey) to get the storage key for the storage account **mystorageaccount** in the resource group **myResourceGroup**.</span></span> <span data-ttu-id="6e21b-172">Skopiuj klucz z etykietą **klucz1**.</span><span class="sxs-lookup"><span data-stu-id="6e21b-172">Copy the key labeled **key1**.</span></span>

```powershell
Get-AzureRmStorageAccountKey -Name mystorageaccount -ResourceGroupName myResourceGroup
```

### <a name="copy-the-vhd"></a><span data-ttu-id="6e21b-173">Skopiuj wirtualny dysk twardy</span><span class="sxs-lookup"><span data-stu-id="6e21b-173">Copy the VHD</span></span>
<span data-ttu-id="6e21b-174">Możesz skopiować pliki między kontami magazynu przy użyciu narzędzia AzCopy.</span><span class="sxs-lookup"><span data-stu-id="6e21b-174">You can copy files between storage accounts using AzCopy.</span></span> <span data-ttu-id="6e21b-175">Docelowy kontener Jeśli określony kontener nie istnieje, jej zostanie utworzona automatycznie.</span><span class="sxs-lookup"><span data-stu-id="6e21b-175">For the destination container, if the specified container doesn't exist, it will be created for you.</span></span> 

<span data-ttu-id="6e21b-176">Aby użyć narzędzia AzCopy, otwórz wiersz polecenia na komputerze lokalnym, a następnie przejdź do folderu, w którym zainstalowano narzędzia AzCopy.</span><span class="sxs-lookup"><span data-stu-id="6e21b-176">To use AzCopy, open a command prompt on your local machine and navigate to the folder where AzCopy is installed.</span></span> <span data-ttu-id="6e21b-177">Powinien być podobny do *\Microsoft SDKs\Azure\AzCopy C:\Program Files (x86)*.</span><span class="sxs-lookup"><span data-stu-id="6e21b-177">It will be similar to *C:\Program Files (x86)\Microsoft SDKs\Azure\AzCopy*.</span></span> 

<span data-ttu-id="6e21b-178">Aby skopiować wszystkie pliki znajdujące się w kontenerze, należy użyć **/S** przełącznika.</span><span class="sxs-lookup"><span data-stu-id="6e21b-178">To copy all of the files within a container, you use the **/S** switch.</span></span> <span data-ttu-id="6e21b-179">Może to służyć do Skopiuj wirtualny dysk twardy systemu operacyjnego i wszystkich dysków danych, jeśli są w tym samym kontenerze.</span><span class="sxs-lookup"><span data-stu-id="6e21b-179">This can be used to copy the OS VHD and all of the data disks if they are in the same container.</span></span> <span data-ttu-id="6e21b-180">W tym przykładzie pokazano, jak skopiować wszystkie pliki w kontenerze **mysourcecontainer** na koncie magazynu **mysourcestorageaccount** do kontenera **mydestinationcontainer**w **mydestinationstorageaccount** konta magazynu.</span><span class="sxs-lookup"><span data-stu-id="6e21b-180">This example shows how to copy all of the files in the container **mysourcecontainer** in storage account **mysourcestorageaccount** to the container **mydestinationcontainer** in the **mydestinationstorageaccount** storage account.</span></span> <span data-ttu-id="6e21b-181">Zamień nazwy konta magazynu i kontenery własne.</span><span class="sxs-lookup"><span data-stu-id="6e21b-181">Replace the names of the storage accounts and containers with your own.</span></span> <span data-ttu-id="6e21b-182">Zastąp `<sourceStorageAccountKey1>` i `<destinationStorageAccountKey1>` z własnych kluczy.</span><span class="sxs-lookup"><span data-stu-id="6e21b-182">Replace `<sourceStorageAccountKey1>` and `<destinationStorageAccountKey1>` with your own keys.</span></span>

```
AzCopy /Source:https://mysourcestorageaccount.blob.core.windows.net/mysourcecontainer `
    /Dest:https://mydestinationatorageaccount.blob.core.windows.net/mydestinationcontainer `
    /SourceKey:<sourceStorageAccountKey1> /DestKey:<destinationStorageAccountKey1> /S
```

<span data-ttu-id="6e21b-183">Jeśli chcesz skopiować konkretnego dysku VHD w kontenerze z wieloma plikami, można również określić nazwę pliku za pomocą przełącznika /Pattern.</span><span class="sxs-lookup"><span data-stu-id="6e21b-183">If you only want to copy a specific VHD in a container with multiple files, you can also specify the file name using the /Pattern switch.</span></span> <span data-ttu-id="6e21b-184">W tym przykładzie tylko plik o nazwie **myFileName.vhd** zostaną skopiowane.</span><span class="sxs-lookup"><span data-stu-id="6e21b-184">In this example, only the file named **myFileName.vhd** will be copied.</span></span>

```
AzCopy /Source:https://mysourcestorageaccount.blob.core.windows.net/mysourcecontainer `
  /Dest:https://mydestinationatorageaccount.blob.core.windows.net/mydestinationcontainer `
  /SourceKey:<sourceStorageAccountKey1> /DestKey:<destinationStorageAccountKey1> `
  /Pattern:myFileName.vhd
```


<span data-ttu-id="6e21b-185">Po zakończeniu otrzymasz wiadomość, która wygląda:</span><span class="sxs-lookup"><span data-stu-id="6e21b-185">When it is finished, you will get a message that looks something like:</span></span>

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

### <a name="troubleshooting"></a><span data-ttu-id="6e21b-186">Rozwiązywanie problemów</span><span class="sxs-lookup"><span data-stu-id="6e21b-186">Troubleshooting</span></span>
* <span data-ttu-id="6e21b-187">Korzystając z narzędzia AZCopy, jeśli zostanie wyświetlony błąd "Serwer nie można uwierzytelnić żądania", upewnij się, że wartość nagłówka autoryzacji jest sformatowany poprawnie tym podpisu.</span><span class="sxs-lookup"><span data-stu-id="6e21b-187">When you use AZCopy, if you see the error "Server failed to authenticate the request", make sure the value of the Authorization header is formed correctly including the signature.</span></span> <span data-ttu-id="6e21b-188">Jeśli używasz 2 klucza lub klucza pomocniczego magazynu, spróbuj użyć klucza podstawowego lub 1 magazynu.</span><span class="sxs-lookup"><span data-stu-id="6e21b-188">If you are using Key 2 or the secondary storage key, try using the primary or 1st storage key.</span></span>

## <a name="create-the-new-vm"></a><span data-ttu-id="6e21b-189">Tworzenie nowej maszyny Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="6e21b-189">Create the new VM</span></span> 

<span data-ttu-id="6e21b-190">Należy utworzyć sieci i innych zasobów maszyny Wirtualnej do użycia przez nowej maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="6e21b-190">You need to create networking and other VM resources to be used by the new VM.</span></span>

### <a name="create-the-subnet-and-vnet"></a><span data-ttu-id="6e21b-191">Utwórz podsieć i sieć wirtualna</span><span class="sxs-lookup"><span data-stu-id="6e21b-191">Create the subNet and vNet</span></span>

<span data-ttu-id="6e21b-192">Utwórz sieć wirtualną i podsieć [sieci wirtualnej](../../virtual-network/virtual-networks-overview.md).</span><span class="sxs-lookup"><span data-stu-id="6e21b-192">Create the vNet and subNet of the [virtual network](../../virtual-network/virtual-networks-overview.md).</span></span>

1. <span data-ttu-id="6e21b-193">Utwórz podsieć.</span><span class="sxs-lookup"><span data-stu-id="6e21b-193">Create the subNet.</span></span> <span data-ttu-id="6e21b-194">W tym przykładzie tworzy podsieć o nazwie **mySubNet**, w grupie zasobów **myResourceGroup**i ustawia prefiks adresu podsieci **10.0.0.0/24**.</span><span class="sxs-lookup"><span data-stu-id="6e21b-194">This example creates a subnet named **mySubNet**, in the resource group **myResourceGroup**, and sets the subnet address prefix to **10.0.0.0/24**.</span></span>
   
    ```powershell
    $rgName = "myResourceGroup"
    $subnetName = "mySubNet"
    $singleSubnet = New-AzureRmVirtualNetworkSubnetConfig -Name $subnetName -AddressPrefix 10.0.0.0/24
    ```
2. <span data-ttu-id="6e21b-195">Tworzenie sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="6e21b-195">Create the vNet.</span></span> <span data-ttu-id="6e21b-196">W tym przykładzie nazwa sieci wirtualnej, który ma zostać **myVnetName**, lokalizacja **zachodnie stany USA**i prefiksu adresu dla sieci wirtualnej do **10.0.0.0/16**.</span><span class="sxs-lookup"><span data-stu-id="6e21b-196">This example sets the virtual network name to be **myVnetName**, the location to **West US**, and the address prefix for the virtual network to **10.0.0.0/16**.</span></span> 
   
    ```powershell
    $location = "West US"
    $vnetName = "myVnetName"
    $vnet = New-AzureRmVirtualNetwork -Name $vnetName -ResourceGroupName $rgName -Location $location `
        -AddressPrefix 10.0.0.0/16 -Subnet $singleSubnet
    ```    

### <a name="create-a-public-ip-address-and-nic"></a><span data-ttu-id="6e21b-197">Tworzenie publicznego adresu IP i karty Sieciowej</span><span class="sxs-lookup"><span data-stu-id="6e21b-197">Create a public IP address and NIC</span></span>
<span data-ttu-id="6e21b-198">Aby umożliwić komunikację z maszyną wirtualną w sieci wirtualnej, potrzebujesz [publicznego adresu IP](../../virtual-network/virtual-network-ip-addresses-overview-arm.md) i interfejsu sieciowego.</span><span class="sxs-lookup"><span data-stu-id="6e21b-198">To enable communication with the virtual machine in the virtual network, you need a [public IP address](../../virtual-network/virtual-network-ip-addresses-overview-arm.md) and a network interface.</span></span>

1. <span data-ttu-id="6e21b-199">Tworzenie publicznego adresu IP.</span><span class="sxs-lookup"><span data-stu-id="6e21b-199">Create the public IP.</span></span> <span data-ttu-id="6e21b-200">W tym przykładzie ustawiono nazwa publicznego adresu IP **myIP**.</span><span class="sxs-lookup"><span data-stu-id="6e21b-200">In this example, the public IP address name is set to **myIP**.</span></span>
   
    ```powershell
    $ipName = "myIP"
    $pip = New-AzureRmPublicIpAddress -Name $ipName -ResourceGroupName $rgName -Location $location `
        -AllocationMethod Dynamic
    ```       
2. <span data-ttu-id="6e21b-201">Utwórz kartę sieciową.</span><span class="sxs-lookup"><span data-stu-id="6e21b-201">Create the NIC.</span></span> <span data-ttu-id="6e21b-202">W tym przykładzie nazwa karty Sieciowej jest ustawiona **myNicName**.</span><span class="sxs-lookup"><span data-stu-id="6e21b-202">In this example, the NIC name is set to **myNicName**.</span></span>
   
    ```powershell
    $nicName = "myNicName"
    $nic = New-AzureRmNetworkInterface -Name $nicName -ResourceGroupName $rgName `
    -Location $location -SubnetId $vnet.Subnets[0].Id -PublicIpAddressId $pip.Id
    ```

### <a name="create-the-network-security-group-and-an-rdp-rule"></a><span data-ttu-id="6e21b-203">Tworzenie grupy zabezpieczeń sieci i reguły protokołu RDP</span><span class="sxs-lookup"><span data-stu-id="6e21b-203">Create the network security group and an RDP rule</span></span>
<span data-ttu-id="6e21b-204">Aby móc zalogować się do maszyny Wirtualnej za pomocą protokołu RDP, musisz mieć regułę zabezpieczeń, która pozwala dostępu RDP do portu 3389.</span><span class="sxs-lookup"><span data-stu-id="6e21b-204">To be able to log in to your VM using RDP, you need to have an security rule that allows RDP access on port 3389.</span></span> <span data-ttu-id="6e21b-205">Ponieważ wirtualny dysk twardy dla nowej maszyny Wirtualnej został utworzony z istniejącego specjalistyczne maszyny Wirtualnej, po utworzeniu maszyny Wirtualnej, możesz można Użyj istniejącego konta ze źródłowej maszyny wirtualnej, który ma uprawnienia do logowania się za pomocą protokołu RDP.</span><span class="sxs-lookup"><span data-stu-id="6e21b-205">Because the VHD for the new VM was created from an existing specialized VM, after the VM is created you can use an existing account from the source virtual machine that had permission to log on using RDP.</span></span>
<span data-ttu-id="6e21b-206">W tym przykładzie nazwa grupy NSG **myNsg** i nazwa reguły protokołu RDP do **myRdpRule**.</span><span class="sxs-lookup"><span data-stu-id="6e21b-206">This example sets the NSG name to **myNsg** and the RDP rule name to **myRdpRule**.</span></span>

```powershell
$nsgName = "myNsg"

$rdpRule = New-AzureRmNetworkSecurityRuleConfig -Name myRdpRule -Description "Allow RDP" `
    -Access Allow -Protocol Tcp -Direction Inbound -Priority 110 `
    -SourceAddressPrefix Internet -SourcePortRange * `
    -DestinationAddressPrefix * -DestinationPortRange 3389
$nsg = New-AzureRmNetworkSecurityGroup -ResourceGroupName $rgName -Location $location `
    -Name $nsgName -SecurityRules $rdpRule
    
```

<span data-ttu-id="6e21b-207">Aby uzyskać więcej informacji na temat punktów końcowych i reguły NSG, zobacz [Otwieranie portów dla maszyny Wirtualnej na platformie Azure przy użyciu programu PowerShell](nsg-quickstart-powershell.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="6e21b-207">For more information about endpoints and NSG rules, see [Opening ports to a VM in Azure using PowerShell](nsg-quickstart-powershell.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

### <a name="set-the-vm-name-and-size"></a><span data-ttu-id="6e21b-208">Ustaw nazwę maszyny Wirtualnej i rozmiar</span><span class="sxs-lookup"><span data-stu-id="6e21b-208">Set the VM name and size</span></span>

<span data-ttu-id="6e21b-209">W tym przykładzie nazwa maszyny Wirtualnej na "myVM" i rozmiaru maszyny Wirtualnej "Standard_A2".</span><span class="sxs-lookup"><span data-stu-id="6e21b-209">This example sets the VM name to "myVM" and the VM size to "Standard_A2".</span></span>
```powershell
$vmName = "myVM"
$vmConfig = New-AzureRmVMConfig -VMName $vmName -VMSize "Standard_A2"
```

### <a name="add-the-nic"></a><span data-ttu-id="6e21b-210">Dodaj kartę Sieciową</span><span class="sxs-lookup"><span data-stu-id="6e21b-210">Add the NIC</span></span>
    
```powershell
$vm = Add-AzureRmVMNetworkInterface -VM $vmConfig -Id $nic.Id
```
    
    
### <a name="configure-the-os-disk"></a><span data-ttu-id="6e21b-211">Skonfiguruj dysk systemu operacyjnego</span><span class="sxs-lookup"><span data-stu-id="6e21b-211">Configure the OS disk</span></span>

1. <span data-ttu-id="6e21b-212">Ustaw identyfikator URI dysku VHD, który został przekazany lub skopiowany.</span><span class="sxs-lookup"><span data-stu-id="6e21b-212">Set the URI for the VHD that you uploaded or copied.</span></span> <span data-ttu-id="6e21b-213">W tym przykładzie pliku wirtualnego dysku twardego o nazwie **myOsDisk.vhd** jest przechowywana na koncie magazynu o nazwie **Mojekontomagazynu** w kontenerze o nazwie **Mojkontener**.</span><span class="sxs-lookup"><span data-stu-id="6e21b-213">In this example, the VHD file named **myOsDisk.vhd** is kept in a storage account named **myStorageAccount** in a container named **myContainer**.</span></span>

    ```powershell
    $osDiskUri = "https://myStorageAccount.blob.core.windows.net/myContainer/myOsDisk.vhd"
    ```
2. <span data-ttu-id="6e21b-214">Dodaj dysk systemu operacyjnego.</span><span class="sxs-lookup"><span data-stu-id="6e21b-214">Add the OS disk.</span></span> <span data-ttu-id="6e21b-215">Gdy tworzony jest dysk systemu operacyjnego, w tym przykładzie termin "osDisk" jest appened na nazwę maszyny Wirtualnej, aby utworzyć nazwa dysku systemu operacyjnego.</span><span class="sxs-lookup"><span data-stu-id="6e21b-215">In this example, when the OS disk is created, the term "osDisk" is appened to the VM name to create the OS disk name.</span></span> <span data-ttu-id="6e21b-216">W tym przykładzie określa również, że ten dysku VHD systemu Windows musi być podłączona do maszyny Wirtualnej jako dysk systemu operacyjnego.</span><span class="sxs-lookup"><span data-stu-id="6e21b-216">This example also specifies that this Windows-based VHD should be attached to the VM as the OS disk.</span></span>
    
    ```powershell
    $osDiskName = $vmName + "osDisk"
    $vm = Set-AzureRmVMOSDisk -VM $vm -Name $osDiskName -VhdUri $osDiskUri -CreateOption attach -Windows
    ```

<span data-ttu-id="6e21b-217">Opcjonalnie: Jeśli masz dysków z danymi, które muszą być podłączone do maszyny Wirtualnej, dodać dyski danych przy użyciu adresów URL danych wirtualne dyski twarde i odpowiedni numer jednostki logicznej (Lun).</span><span class="sxs-lookup"><span data-stu-id="6e21b-217">Optional: If you have data disks that need to be attached to the VM, add the data disks by using the URLs of data VHDs and the appropriate Logical Unit Number (Lun).</span></span>

```powershell
$dataDiskName = $vmName + "dataDisk"
$vm = Add-AzureRmVMDataDisk -VM $vm -Name $dataDiskName -VhdUri $dataDiskUri -Lun 1 -CreateOption attach
```

<span data-ttu-id="6e21b-218">Korzystając z konta magazynu, danych i adresy URL dysku systemu operacyjnego wyglądać mniej więcej tak: `https://StorageAccountName.blob.core.windows.net/BlobContainerName/DiskName.vhd`.</span><span class="sxs-lookup"><span data-stu-id="6e21b-218">When using a storage account, the data and operating system disk URLs look something like this: `https://StorageAccountName.blob.core.windows.net/BlobContainerName/DiskName.vhd`.</span></span> <span data-ttu-id="6e21b-219">To w portalu można znaleźć przeglądanie do kontenera magazynu docelowego, klikając systemu operacyjnego lub dane wirtualnego dysku twardego, która została skopiowana, a następnie skopiować zawartość adresu URL.</span><span class="sxs-lookup"><span data-stu-id="6e21b-219">You can find this on the portal by browsing to the target storage container, clicking the operating system or data VHD that was copied, and then copying the contents of the URL.</span></span>


### <a name="complete-the-vm"></a><span data-ttu-id="6e21b-220">Zakończenie maszyny Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="6e21b-220">Complete the VM</span></span> 

<span data-ttu-id="6e21b-221">Utwórz maszynę Wirtualną przy użyciu konfiguracji, które właśnie utworzyliśmy.</span><span class="sxs-lookup"><span data-stu-id="6e21b-221">Create the VM using the configurations that we just created.</span></span>

```powershell
#Create the new VM
New-AzureRmVM -ResourceGroupName $rgName -Location $location -VM $vm
```

<span data-ttu-id="6e21b-222">Jeśli to polecenie zakończyło się pomyślnie, zostanie wyświetlone dane wyjściowe w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="6e21b-222">If this command was successful, you'll see output like this:</span></span>

```powershell
RequestId IsSuccessStatusCode StatusCode ReasonPhrase
--------- ------------------- ---------- ------------
                         True         OK OK   

```

### <a name="verify-that-the-vm-was-created"></a><span data-ttu-id="6e21b-223">Sprawdź, czy maszyna wirtualna została utworzona</span><span class="sxs-lookup"><span data-stu-id="6e21b-223">Verify that the VM was created</span></span>
<span data-ttu-id="6e21b-224">Nowo utworzona maszyna wirtualna powinna być widoczna albo w [portalu Azure](https://portal.azure.com)w obszarze **Przeglądaj** > **maszyn wirtualnych**, lub za pomocą następujących poleceń programu PowerShell:</span><span class="sxs-lookup"><span data-stu-id="6e21b-224">You should see the newly created VM either in the [Azure portal](https://portal.azure.com), under **Browse** > **Virtual machines**, or by using the following PowerShell commands:</span></span>

```powershell
$vmList = Get-AzureRmVM -ResourceGroupName $rgName
$vmList.Name
```

## <a name="next-steps"></a><span data-ttu-id="6e21b-225">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="6e21b-225">Next steps</span></span>
<span data-ttu-id="6e21b-226">Aby zalogować się do nowej maszyny wirtualnej, przejdź do maszyny Wirtualnej w [portal](https://portal.azure.com), kliknij przycisk **Connect**i Otwórz plik RDP pulpitu zdalnego.</span><span class="sxs-lookup"><span data-stu-id="6e21b-226">To sign in to your new virtual machine, browse to the VM in the [portal](https://portal.azure.com), click **Connect**, and open the Remote Desktop RDP file.</span></span> <span data-ttu-id="6e21b-227">Korzystać z poświadczeń konta oryginalnego maszyny wirtualnej, aby zalogować się do nowej maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="6e21b-227">Use the account credentials of your original virtual machine to sign in to your new virtual machine.</span></span> <span data-ttu-id="6e21b-228">Aby uzyskać więcej informacji, zobacz [jak połączenia i zaloguj się do maszyny wirtualnej platformy Azure systemem Windows](connect-logon.md).</span><span class="sxs-lookup"><span data-stu-id="6e21b-228">For more information, see [How to connect and log on to an Azure virtual machine running Windows](connect-logon.md).</span></span>

