---
title: "Tworzenie zarządzanego maszyny Wirtualnej platformy Azure z wirtualnego dysku twardego uogólnionego lokalnymi | Dokumentacja firmy Microsoft"
description: "Przekazać uogólniony wirtualny dysk twardy na platformie Azure, aby go użyć do utworzenia nowych maszyn wirtualnych, w modelu wdrażania usługi Resource Manager."
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
ms.date: 05/19/2017
ms.author: cynthn
ms.openlocfilehash: d802ba16ecb4e32e2adb7be3a8e99c72a1625841
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
# <a name="upload-a-generalized-vhd-and-use-it-to-create-new-vms-in-azure"></a><span data-ttu-id="3c7d3-103">Przekazywanie uogólniony wirtualny dysk twardy i umożliwia tworzenie nowych maszyn wirtualnych na platformie Azure</span><span class="sxs-lookup"><span data-stu-id="3c7d3-103">Upload a generalized VHD and use it to create new VMs in Azure</span></span>

<span data-ttu-id="3c7d3-104">Ten temat przeprowadzi Cię przez przekazywanie wirtualnego dysku twardego uogólnionego maszyny wirtualnej na platformie Azure, tworzenie obrazu na podstawie wirtualnego dysku twardego i utworzyć nową maszynę Wirtualną z tego obrazu przy użyciu programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="3c7d3-104">This topic walks you through using PowerShell to upload a VHD of a generalized VM to Azure, create an image from the VHD and create a new VM from that image.</span></span> <span data-ttu-id="3c7d3-105">Możesz przekazać dysku VHD wyeksportowane z narzędzia wirtualizacji lokalnej lub innej chmury.</span><span class="sxs-lookup"><span data-stu-id="3c7d3-105">You can upload a VHD exported from an on-premises virtualization tool or from another cloud.</span></span> <span data-ttu-id="3c7d3-106">Przy użyciu [dysków zarządzanych](managed-disks-overview.md) dla nowej maszyny Wirtualnej upraszcza zarządzanie maszyny Wirtualnej i zapewnia większą dostępność, gdy maszyna wirtualna jest umieszczona w zestawie dostępności.</span><span class="sxs-lookup"><span data-stu-id="3c7d3-106">Using [Managed Disks](managed-disks-overview.md) for the new VM simplifies the VM managment and provides better availability when the VM is placed in an availability set.</span></span> 

<span data-ttu-id="3c7d3-107">Jeśli chcesz użyć przykładowego skryptu, zobacz [przykładowy skrypt do przekazania dysku VHD na platformie Azure i utworzyć nową maszynę Wirtualną](../scripts/virtual-machines-windows-powershell-upload-generalized-script.md)</span><span class="sxs-lookup"><span data-stu-id="3c7d3-107">If you want to use a sample script, see [Sample script to upload a VHD to Azure and create a new VM](../scripts/virtual-machines-windows-powershell-upload-generalized-script.md)</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="3c7d3-108">Przed rozpoczęciem</span><span class="sxs-lookup"><span data-stu-id="3c7d3-108">Before you begin</span></span>

- <span data-ttu-id="3c7d3-109">Przed przekazaniem jakiegokolwiek dysku VHD na platformę Azure, należy wykonać [Przygotowywanie wirtualnego dysku twardego Windows lub VHDX do przekazania do platformy Azure](prepare-for-upload-vhd-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="3c7d3-109">Before uploading any VHD to Azure, you should follow [Prepare a Windows VHD or VHDX to upload to Azure](prepare-for-upload-vhd-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)</span></span>
- <span data-ttu-id="3c7d3-110">Przegląd [planowanie migracji do zarządzanych dysków](on-prem-to-azure.md#plan-for-the-migration-to-managed-disks) przed rozpoczęciem migracji do [dysków zarządzanych](managed-disks-overview.md).</span><span class="sxs-lookup"><span data-stu-id="3c7d3-110">Review [Plan for the migration to Managed Disks](on-prem-to-azure.md#plan-for-the-migration-to-managed-disks) before starting your migration to [Managed Disks](managed-disks-overview.md).</span></span>
- <span data-ttu-id="3c7d3-111">Upewnij się, że masz najnowszą wersję modułu programu AzureRM.Compute PowerShell.</span><span class="sxs-lookup"><span data-stu-id="3c7d3-111">Make sure that you have the latest version of the AzureRM.Compute PowerShell module.</span></span> <span data-ttu-id="3c7d3-112">Uruchom następujące polecenie, aby go zainstalować.</span><span class="sxs-lookup"><span data-stu-id="3c7d3-112">Run the following command to install it.</span></span>

    ```powershell
    Install-Module AzureRM.Compute -RequiredVersion 2.6.0
    ```
    <span data-ttu-id="3c7d3-113">Aby uzyskać więcej informacji, zobacz [przechowywanie wersji programu Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="3c7d3-113">For more information, see [Azure PowerShell Versioning](/powershell/azure/overview).</span></span>


## <a name="generalize-the-windows-vm-using-sysprep"></a><span data-ttu-id="3c7d3-114">Maszyny Wirtualnej systemu Windows za pomocą programu Sysprep do uogólnienia</span><span class="sxs-lookup"><span data-stu-id="3c7d3-114">Generalize the Windows VM using Sysprep</span></span>

<span data-ttu-id="3c7d3-115">Program Sysprep usuwa wszystkie informacje osobiste konto, między innymi i przygotowuje komputer do użycia jako obraz.</span><span class="sxs-lookup"><span data-stu-id="3c7d3-115">Sysprep removes all your personal account information, among other things, and prepares the machine to be used as an image.</span></span> <span data-ttu-id="3c7d3-116">Aby uzyskać więcej informacji o narzędziu Sysprep, zobacz [sposobu użycia programu Sysprep: wprowadzenie](http://technet.microsoft.com/library/bb457073.aspx).</span><span class="sxs-lookup"><span data-stu-id="3c7d3-116">For details about Sysprep, see [How to Use Sysprep: An Introduction](http://technet.microsoft.com/library/bb457073.aspx).</span></span>

<span data-ttu-id="3c7d3-117">Upewnij się, że ról serwera uruchomionych na komputerze są obsługiwane przez program Sysprep.</span><span class="sxs-lookup"><span data-stu-id="3c7d3-117">Make sure the server roles running on the machine are supported by Sysprep.</span></span> <span data-ttu-id="3c7d3-118">Aby uzyskać więcej informacji, zobacz [Obsługa programu Sysprep dla ról serwera](https://msdn.microsoft.com/windows/hardware/commercialize/manufacture/desktop/sysprep-support-for-server-roles)</span><span class="sxs-lookup"><span data-stu-id="3c7d3-118">For more information, see [Sysprep Support for Server Roles](https://msdn.microsoft.com/windows/hardware/commercialize/manufacture/desktop/sysprep-support-for-server-roles)</span></span>

> [!IMPORTANT]
> <span data-ttu-id="3c7d3-119">Jeśli korzystasz z programu Sysprep przed przekazaniem dysk VHD do platformy Azure po raz pierwszy, upewnij się, masz [przygotować maszyny Wirtualnej](prepare-for-upload-vhd-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) przed uruchomieniem programu Sysprep.</span><span class="sxs-lookup"><span data-stu-id="3c7d3-119">If you are running Sysprep before uploading your VHD to Azure for the first time, make sure you have [prepared your VM](prepare-for-upload-vhd-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) before running Sysprep.</span></span> 
> 
> 

1. <span data-ttu-id="3c7d3-120">Zaloguj się do maszyny wirtualnej systemu Windows.</span><span class="sxs-lookup"><span data-stu-id="3c7d3-120">Sign in to the Windows virtual machine.</span></span>
2. <span data-ttu-id="3c7d3-121">Otwórz okno Wiersz polecenia jako administrator.</span><span class="sxs-lookup"><span data-stu-id="3c7d3-121">Open the Command Prompt window as an administrator.</span></span> <span data-ttu-id="3c7d3-122">Zmień katalog na **%windir%\system32\sysprep**, a następnie uruchom `sysprep.exe`.</span><span class="sxs-lookup"><span data-stu-id="3c7d3-122">Change the directory to **%windir%\system32\sysprep**, and then run `sysprep.exe`.</span></span>
3. <span data-ttu-id="3c7d3-123">W **narzędzie przygotowania systemu** okno dialogowe, wybierz opcję **wprowadź systemu Out-of-Box Experience (OOBE)**i upewnij się, że **Generalize** pole wyboru jest zaznaczone.</span><span class="sxs-lookup"><span data-stu-id="3c7d3-123">In the **System Preparation Tool** dialog box, select **Enter System Out-of-Box Experience (OOBE)**, and make sure that the **Generalize** check box is selected.</span></span>
4. <span data-ttu-id="3c7d3-124">W **opcje zamykania**, wybierz pozycję **zamknięcia**.</span><span class="sxs-lookup"><span data-stu-id="3c7d3-124">In **Shutdown Options**, select **Shutdown**.</span></span>
5. <span data-ttu-id="3c7d3-125">Kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="3c7d3-125">Click **OK**.</span></span>
   
    ![Uruchom program Sysprep](./media/upload-generalized-managed/sysprepgeneral.png)
6. <span data-ttu-id="3c7d3-127">Po zakończeniu działania programu Sysprep, zamyka maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="3c7d3-127">When Sysprep completes, it shuts down the virtual machine.</span></span> <span data-ttu-id="3c7d3-128">Nie uruchamiaj ponownie maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="3c7d3-128">Do not restart the VM.</span></span>



## <a name="log-in-to-azure"></a><span data-ttu-id="3c7d3-129">Zaloguj się do platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="3c7d3-129">Log in to Azure</span></span>
<span data-ttu-id="3c7d3-130">Jeśli nie masz jeszcze programu PowerShell w wersji 1.4 lub nowszy zainstalowany, przeczytaj [jak instalowanie i konfigurowanie programu Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="3c7d3-130">If you don't already have PowerShell version 1.4 or above installed, read [How to install and configure Azure PowerShell](/powershell/azure/overview).</span></span>

1. <span data-ttu-id="3c7d3-131">Otwórz program Azure PowerShell i zaloguj się do konta platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="3c7d3-131">Open Azure PowerShell and sign in to your Azure account.</span></span> <span data-ttu-id="3c7d3-132">Otwiera okno podręczne wprowadzenie poświadczeń konta platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="3c7d3-132">A pop-up window opens for you to enter your Azure account credentials.</span></span>
   
    ```powershell
    Login-AzureRmAccount
    ```
2. <span data-ttu-id="3c7d3-133">Pobierz identyfikatory subskrypcji dla dostępnych subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="3c7d3-133">Get the subscription IDs for your available subscriptions.</span></span>
   
    ```powershell
    Get-AzureRmSubscription
    ```
3. <span data-ttu-id="3c7d3-134">Ustaw poprawną subskrypcję za pomocą identyfikatora subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="3c7d3-134">Set the correct subscription using the subscription ID.</span></span> <span data-ttu-id="3c7d3-135">Zastąp  *<subscriptionID>*  o identyfikatorze poprawną subskrypcję.</span><span class="sxs-lookup"><span data-stu-id="3c7d3-135">Replace *<subscriptionID>* with the ID of the correct subscription.</span></span>
   
    ```powershell
    Select-AzureRmSubscription -SubscriptionId "<subscriptionID>"
    ```

## <a name="get-the-storage-account"></a><span data-ttu-id="3c7d3-136">Uzyskaj konto magazynu</span><span class="sxs-lookup"><span data-stu-id="3c7d3-136">Get the storage account</span></span>
<span data-ttu-id="3c7d3-137">Potrzebujesz konta magazynu na platformie Azure do przechowywania załadowanego obrazu maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="3c7d3-137">You need a storage account in Azure to store the uploaded VM image.</span></span> <span data-ttu-id="3c7d3-138">Możesz użyć istniejącego konta magazynu lub Utwórz nową.</span><span class="sxs-lookup"><span data-stu-id="3c7d3-138">You can either use an existing storage account or create a new one.</span></span> 

<span data-ttu-id="3c7d3-139">Jeśli wirtualny dysk twardy będzie używany do tworzenia zarządzanego dysku dla maszyny Wirtualnej, Lokalizacja konta magazynu musi być w tej samej lokalizacji, w którym zostanie utworzenie maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="3c7d3-139">If you will be using the VHD to create a managed disk for a VM, the storage account location must be same the location where you will be creating the VM.</span></span>

<span data-ttu-id="3c7d3-140">Aby wyświetlić konta dostępny magazyn, wpisz:</span><span class="sxs-lookup"><span data-stu-id="3c7d3-140">To show the available storage accounts, type:</span></span>

```powershell
Get-AzureRmStorageAccount
```

<span data-ttu-id="3c7d3-141">Jeśli chcesz użyć istniejącego konta magazynu, przejdź do [przekazać obraz maszyny Wirtualnej](#upload-the-vm-vhd-to-your-storage-account) sekcji.</span><span class="sxs-lookup"><span data-stu-id="3c7d3-141">If you want to use an existing storage account, proceed to the [Upload the VM image](#upload-the-vm-vhd-to-your-storage-account) section.</span></span>

<span data-ttu-id="3c7d3-142">Jeśli musisz utworzyć konto magazynu, wykonaj następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="3c7d3-142">If you need to create a storage account, follow these steps:</span></span>

1. <span data-ttu-id="3c7d3-143">Potrzebna jest nazwa grupy zasobów, w którym ma zostać utworzony na koncie magazynu.</span><span class="sxs-lookup"><span data-stu-id="3c7d3-143">You need the name of the resource group where the storage account should be created.</span></span> <span data-ttu-id="3c7d3-144">Aby dowiedzieć się, wszystkie grupy zasobów, które są w ramach subskrypcji, wpisz:</span><span class="sxs-lookup"><span data-stu-id="3c7d3-144">To find out all the resource groups that are in your subscription, type:</span></span>
   
    ```powershell
    Get-AzureRmResourceGroup
    ```

    <span data-ttu-id="3c7d3-145">Aby utworzyć grupę zasobów o nazwie **myResourceGroup** w **wschodnie stany USA** regionu, wpisz:</span><span class="sxs-lookup"><span data-stu-id="3c7d3-145">To create a resource group named **myResourceGroup** in the **East US** region, type:</span></span>

    ```powershell
    New-AzureRmResourceGroup -Name myResourceGroup -Location "East US"
    ```

2. <span data-ttu-id="3c7d3-146">Utwórz konto magazynu o nazwie **mojekontomagazynu** w tej grupie zasobów za pomocą [New-AzureRmStorageAccount](/powershell/module/azurerm.storage/new-azurermstorageaccount) polecenia cmdlet:</span><span class="sxs-lookup"><span data-stu-id="3c7d3-146">Create a storage account named **mystorageaccount** in this resource group by using the [New-AzureRmStorageAccount](/powershell/module/azurerm.storage/new-azurermstorageaccount) cmdlet:</span></span>
   
    ```powershell
    New-AzureRmStorageAccount -ResourceGroupName myResourceGroup -Name mystorageaccount -Location "East US"`
        -SkuName "Standard_LRS" -Kind "Storage"
    ```
   
    <span data-ttu-id="3c7d3-147">Prawidłowe wartości - SkuName to:</span><span class="sxs-lookup"><span data-stu-id="3c7d3-147">Valid values for -SkuName are:</span></span>
   
   * <span data-ttu-id="3c7d3-148">**Standard_LRS** — magazyn lokalnie nadmiarowy.</span><span class="sxs-lookup"><span data-stu-id="3c7d3-148">**Standard_LRS** - Locally redundant storage.</span></span> 
   * <span data-ttu-id="3c7d3-149">**Standard_ZRS** -strefy nadmiarowego magazynu.</span><span class="sxs-lookup"><span data-stu-id="3c7d3-149">**Standard_ZRS** - Zone redundant storage.</span></span>
   * <span data-ttu-id="3c7d3-150">**Standard_GRS** — z magazynu geograficznie nadmiarowego magazynu.</span><span class="sxs-lookup"><span data-stu-id="3c7d3-150">**Standard_GRS** - Geo redundant storage.</span></span> 
   * <span data-ttu-id="3c7d3-151">**Standard_RAGRS** -dostęp do odczytu z magazynu geograficznie nadmiarowego magazynu.</span><span class="sxs-lookup"><span data-stu-id="3c7d3-151">**Standard_RAGRS** - Read access geo redundant storage.</span></span> 
   * <span data-ttu-id="3c7d3-152">**Premium_LRS** — magazyn lokalnie nadmiarowy Premium.</span><span class="sxs-lookup"><span data-stu-id="3c7d3-152">**Premium_LRS** - Premium locally redundant storage.</span></span> 

## <a name="upload-the-vhd-to-your-storage-account"></a><span data-ttu-id="3c7d3-153">Przekazanie dysku VHD do konta magazynu</span><span class="sxs-lookup"><span data-stu-id="3c7d3-153">Upload the VHD to your storage account</span></span>

<span data-ttu-id="3c7d3-154">Użyj [AzureRmVhd Dodaj](https://msdn.microsoft.com/library/mt603554.aspx) polecenia cmdlet w celu przekazania dysku VHD do kontenera na koncie magazynu.</span><span class="sxs-lookup"><span data-stu-id="3c7d3-154">Use the [Add-AzureRmVhd](https://msdn.microsoft.com/library/mt603554.aspx) cmdlet to upload the VHD to a container in your storage account.</span></span> <span data-ttu-id="3c7d3-155">W tym przykładzie powoduje przekazanie pliku *myVHD.vhd* z *"dyski twarde C:\Users\Public\Documents\Virtual\"*  na konto magazynu o nazwie *mojekontomagazynu* w *myResourceGroup* grupy zasobów.</span><span class="sxs-lookup"><span data-stu-id="3c7d3-155">This example uploads the file *myVHD.vhd* from *"C:\Users\Public\Documents\Virtual hard disks\"* to a storage account named *mystorageaccount* in the *myResourceGroup* resource group.</span></span> <span data-ttu-id="3c7d3-156">Plik zostaną umieszczone w kontenerze o nazwie *mojkontener* i Nowa nazwa pliku będzie *myUploadedVHD.vhd*.</span><span class="sxs-lookup"><span data-stu-id="3c7d3-156">The file will be placed into the container named *mycontainer* and the new file name will be *myUploadedVHD.vhd*.</span></span>

```powershell
$rgName = "myResourceGroup"
$urlOfUploadedImageVhd = "https://mystorageaccount.blob.core.windows.net/mycontainer/myUploadedVHD.vhd"
Add-AzureRmVhd -ResourceGroupName $rgName -Destination $urlOfUploadedImageVhd `
    -LocalFilePath "C:\Users\Public\Documents\Virtual hard disks\myVHD.vhd"
```


<span data-ttu-id="3c7d3-157">W przypadku powodzenia można uzyskać odpowiedzi, która wygląda podobnie do poniższego:</span><span class="sxs-lookup"><span data-stu-id="3c7d3-157">If successful, you get a response that looks similar to this:</span></span>

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

<span data-ttu-id="3c7d3-158">W zależności od połączenia sieciowego i rozmiar pliku VHD to polecenie może zająć trochę czasu, aby zakończyć</span><span class="sxs-lookup"><span data-stu-id="3c7d3-158">Depending on your network connection and the size of your VHD file, this command may take a while to complete</span></span>

<span data-ttu-id="3c7d3-159">Zapisz **docelowy identyfikator URI** ścieżkę do użycia w przyszłości, jeśli zamierzasz utworzyć dysków zarządzanych lub nowej maszyny Wirtualnej przy użyciu przekazywanego wirtualnego dysku twardego.</span><span class="sxs-lookup"><span data-stu-id="3c7d3-159">Save the **Destination URI** path to use later if you are going to create a managed disk or a new VM using the uploaded VHD.</span></span>

### <a name="other-options-for-uploading-a-vhd"></a><span data-ttu-id="3c7d3-160">Inne opcje przekazywanie wirtualnego dysku twardego</span><span class="sxs-lookup"><span data-stu-id="3c7d3-160">Other options for uploading a VHD</span></span>
 
 
<span data-ttu-id="3c7d3-161">Możesz również przekazywać dysku VHD do konta magazynu przy użyciu jednej z następujących czynności:</span><span class="sxs-lookup"><span data-stu-id="3c7d3-161">You can also upload a VHD to your storage account using one of the following:</span></span>

- [<span data-ttu-id="3c7d3-162">Narzędzie AzCopy</span><span class="sxs-lookup"><span data-stu-id="3c7d3-162">AzCopy</span></span>](http://aka.ms/downloadazcopy)
- [<span data-ttu-id="3c7d3-163">Obiektu Blob magazynu Azure kopiowania interfejsu API</span><span class="sxs-lookup"><span data-stu-id="3c7d3-163">Azure Storage Copy Blob API</span></span>](https://msdn.microsoft.com/library/azure/dd894037.aspx)
- [<span data-ttu-id="3c7d3-164">Obiekty BLOB magazynu Azure Explorer przekazywania</span><span class="sxs-lookup"><span data-stu-id="3c7d3-164">Azure Storage Explorer Uploading Blobs</span></span>](https://azurestorageexplorer.codeplex.com/)
- [<span data-ttu-id="3c7d3-165">Dokumentacja interfejsu API REST usługi Import/Eksport magazynu</span><span class="sxs-lookup"><span data-stu-id="3c7d3-165">Storage Import/Export Service REST API Reference</span></span>](https://msdn.microsoft.com/library/dn529096.aspx)
-   <span data-ttu-id="3c7d3-166">Zaleca się za pomocą usługi Import/eksport, jeśli szacowany czas przekazywania jest dłuższa niż 7 dni.</span><span class="sxs-lookup"><span data-stu-id="3c7d3-166">We recommend using Import/Export Service if estimated uploading time is longer than 7 days.</span></span> <span data-ttu-id="3c7d3-167">Można użyć [DataTransferSpeedCalculator](https://github.com/Azure-Samples/storage-dotnet-import-export-job-management/blob/master/DataTransferSpeedCalculator.html) oszacowanie godzinę z jednostki rozmiaru i transferu danych.</span><span class="sxs-lookup"><span data-stu-id="3c7d3-167">You can use [DataTransferSpeedCalculator](https://github.com/Azure-Samples/storage-dotnet-import-export-job-management/blob/master/DataTransferSpeedCalculator.html) to estimate the time from data size and transfer unit.</span></span> 
    <span data-ttu-id="3c7d3-168">Narzędzie importu/eksportu może służyć do skopiowania do konta magazynu w warstwie standardowa.</span><span class="sxs-lookup"><span data-stu-id="3c7d3-168">Import/Export can be used to copy to a standard storage account.</span></span> <span data-ttu-id="3c7d3-169">Należy skopiować z magazynu w warstwie standardowa do konta magazynu premium za pomocą narzędzia, takiego jak narzędzie AzCopy.</span><span class="sxs-lookup"><span data-stu-id="3c7d3-169">You will need to copy from standard storage to premium storage account using a tool like AzCopy.</span></span>


## <a name="create-a-managed-image-from-the-uploaded-vhd"></a><span data-ttu-id="3c7d3-170">Tworzenie zarządzanego obrazu z przekazanego wirtualnego dysku twardego</span><span class="sxs-lookup"><span data-stu-id="3c7d3-170">Create a managed image from the uploaded VHD</span></span> 

<span data-ttu-id="3c7d3-171">Tworzenie obrazu zarządzanych za pomocą programu uogólniony wirtualny dysk twardy systemu operacyjnego.</span><span class="sxs-lookup"><span data-stu-id="3c7d3-171">Create a managed image using your generalized OS VHD.</span></span> <span data-ttu-id="3c7d3-172">Zastąp wartości odpowiednimi informacjami.</span><span class="sxs-lookup"><span data-stu-id="3c7d3-172">Replace the values with your own information.</span></span>


1.  <span data-ttu-id="3c7d3-173">Najpierw należy ustawić wspólne parametry:</span><span class="sxs-lookup"><span data-stu-id="3c7d3-173">First, set the common parameters:</span></span>

    ```powershell
    $vmName = "myVM"
    $computerName = "myComputer"
    $vmSize = "Standard_DS1_v2"
    $location = "East US" 
    $imageName = "yourImageName"
    ```

4.  <span data-ttu-id="3c7d3-174">Utworzyć obraz przy użyciu programu uogólniony wirtualny dysk twardy systemu operacyjnego.</span><span class="sxs-lookup"><span data-stu-id="3c7d3-174">Create the image using your generalized OS VHD.</span></span>

    ```powershell
    $imageConfig = New-AzureRmImageConfig -Location $location
    $imageConfig = Set-AzureRmImageOsDisk -Image $imageConfig -OsType Windows -OsState Generalized -BlobUri $urlOfUploadedImageVhd
    $image = New-AzureRmImage -ImageName $imageName -ResourceGroupName $rgName -Image $imageConfig
    ```

## <a name="create-a-virtual-network"></a><span data-ttu-id="3c7d3-175">Tworzenie sieci wirtualnej</span><span class="sxs-lookup"><span data-stu-id="3c7d3-175">Create a virtual network</span></span>
<span data-ttu-id="3c7d3-176">Utwórz sieć wirtualną i podsieć [sieci wirtualnej](../../virtual-network/virtual-networks-overview.md).</span><span class="sxs-lookup"><span data-stu-id="3c7d3-176">Create the vNet and subnet of the [virtual network](../../virtual-network/virtual-networks-overview.md).</span></span>

1. <span data-ttu-id="3c7d3-177">Utwórz podsieć.</span><span class="sxs-lookup"><span data-stu-id="3c7d3-177">Create the subnet.</span></span> <span data-ttu-id="3c7d3-178">W tym przykładzie tworzy podsieć o nazwie *mySubnet* z prefiksem adresu o *10.0.0.0/24*.</span><span class="sxs-lookup"><span data-stu-id="3c7d3-178">This example creates a subnet named *mySubnet* with the address prefix of *10.0.0.0/24*.</span></span>  
   
    ```powershell
    $subnetName = "mySubnet"
    $singleSubnet = New-AzureRmVirtualNetworkSubnetConfig -Name $subnetName -AddressPrefix 10.0.0.0/24
    ```
2. <span data-ttu-id="3c7d3-179">Utwórz sieć wirtualną.</span><span class="sxs-lookup"><span data-stu-id="3c7d3-179">Create the virtual network.</span></span> <span data-ttu-id="3c7d3-180">W tym przykładzie tworzy sieć wirtualną o nazwie *myVnet* z prefiksem adresu o *10.0.0.0/16*.</span><span class="sxs-lookup"><span data-stu-id="3c7d3-180">This example creates a virtual network named *myVnet* with the address prefix of *10.0.0.0/16*.</span></span>  
   
    ```powershell
    $vnetName = "myVnet"
    $vnet = New-AzureRmVirtualNetwork -Name $vnetName -ResourceGroupName $rgName -Location $location `
        -AddressPrefix 10.0.0.0/16 -Subnet $singleSubnet
    ```    

## <a name="create-a-public-ip-address-and-network-interface"></a><span data-ttu-id="3c7d3-181">Tworzenie publicznego adresu IP adres i interfejsu sieciowego</span><span class="sxs-lookup"><span data-stu-id="3c7d3-181">Create a public IP address and network interface</span></span>

<span data-ttu-id="3c7d3-182">Aby umożliwić komunikację z maszyną wirtualną w sieci wirtualnej, potrzebujesz [publicznego adresu IP](../../virtual-network/virtual-network-ip-addresses-overview-arm.md) i interfejsu sieciowego.</span><span class="sxs-lookup"><span data-stu-id="3c7d3-182">To enable communication with the virtual machine in the virtual network, you need a [public IP address](../../virtual-network/virtual-network-ip-addresses-overview-arm.md) and a network interface.</span></span>

1. <span data-ttu-id="3c7d3-183">Utwórz publiczny adres IP.</span><span class="sxs-lookup"><span data-stu-id="3c7d3-183">Create a public IP address.</span></span> <span data-ttu-id="3c7d3-184">W tym przykładzie jest tworzony publiczny adres IP o nazwie *myPip*.</span><span class="sxs-lookup"><span data-stu-id="3c7d3-184">This example creates a public IP address named *myPip*.</span></span> 
   
    ```powershell
    $ipName = "myPip"
    $pip = New-AzureRmPublicIpAddress -Name $ipName -ResourceGroupName $rgName -Location $location `
        -AllocationMethod Dynamic
    ```       
2. <span data-ttu-id="3c7d3-185">Utwórz kartę sieciową.</span><span class="sxs-lookup"><span data-stu-id="3c7d3-185">Create the NIC.</span></span> <span data-ttu-id="3c7d3-186">W tym przykładzie jest tworzony karty Sieciowej o nazwie **myNic**.</span><span class="sxs-lookup"><span data-stu-id="3c7d3-186">This example creates a NIC named **myNic**.</span></span> 
   
    ```powershell
    $nicName = "myNic"
    $nic = New-AzureRmNetworkInterface -Name $nicName -ResourceGroupName $rgName -Location $location `
        -SubnetId $vnet.Subnets[0].Id -PublicIpAddressId $pip.Id
    ```

## <a name="create-the-network-security-group-and-an-rdp-rule"></a><span data-ttu-id="3c7d3-187">Tworzenie grupy zabezpieczeń sieci i reguły protokołu RDP</span><span class="sxs-lookup"><span data-stu-id="3c7d3-187">Create the network security group and an RDP rule</span></span>

<span data-ttu-id="3c7d3-188">Aby móc zalogować się do maszyny Wirtualnej za pomocą protokołu RDP, musisz mieć reguły zabezpieczeń sieci (NSG), umożliwiająca dostęp RDP do portu 3389.</span><span class="sxs-lookup"><span data-stu-id="3c7d3-188">To be able to log in to your VM using RDP, you need to have a network security rule (NSG) that allows RDP access on port 3389.</span></span> 

<span data-ttu-id="3c7d3-189">W tym przykładzie tworzy grupy NSG o nazwie *myNsg* zawierający regułę o nazwie *myRdpRule* za pośrednictwem portu 3389 która zezwala na ruch RDP.</span><span class="sxs-lookup"><span data-stu-id="3c7d3-189">This example creates an NSG named *myNsg* that contains a rule called *myRdpRule* that allows RDP traffic over port 3389.</span></span> <span data-ttu-id="3c7d3-190">Aby uzyskać więcej informacji na temat grup NSG, zobacz [Otwieranie portów dla maszyny Wirtualnej na platformie Azure przy użyciu programu PowerShell](nsg-quickstart-powershell.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="3c7d3-190">For more information about NSGs, see [Opening ports to a VM in Azure using PowerShell](nsg-quickstart-powershell.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

```powershell
$nsgName = "myNsg"
$ruleName = "myRdpRule"
$rdpRule = New-AzureRmNetworkSecurityRuleConfig -Name $ruleName -Description "Allow RDP" `
    -Access Allow -Protocol Tcp -Direction Inbound -Priority 110 `
    -SourceAddressPrefix Internet -SourcePortRange * `
    -DestinationAddressPrefix * -DestinationPortRange 3389

$nsg = New-AzureRmNetworkSecurityGroup -ResourceGroupName $rgName -Location $location `
    -Name $nsgName -SecurityRules $rdpRule
```


## <a name="create-a-variable-for-the-virtual-network"></a><span data-ttu-id="3c7d3-191">Utwórz zmienną dla sieci wirtualnej</span><span class="sxs-lookup"><span data-stu-id="3c7d3-191">Create a variable for the virtual network</span></span>

<span data-ttu-id="3c7d3-192">Utwórz zmienną dla ukończonych sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="3c7d3-192">Create a variable for the completed virtual network.</span></span> 

```powershell
$vnet = Get-AzureRmVirtualNetwork -ResourceGroupName $rgName -Name $vnetName

```

## <a name="get-the-credentials-for-the-vm"></a><span data-ttu-id="3c7d3-193">Uzyskiwanie poświadczeń dla maszyny Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="3c7d3-193">Get the credentials for the VM</span></span>

<span data-ttu-id="3c7d3-194">Następujące polecenie cmdlet zostanie otwarte okno gdzie będą wprowadź nową nazwę użytkownika i hasło do użycia jako konto administratora lokalnego na zdalny dostęp do maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="3c7d3-194">The following cmdlet will open a window where you will enter a new user name and password to use as the local administrator account for remotely accessing the VM.</span></span> 

```powershell
$cred = Get-Credential
```

## <a name="add-the-vm-name-and-size-to-the-vm-configuration"></a><span data-ttu-id="3c7d3-195">Dodaj nazwę maszyny Wirtualnej i rozmiar do konfiguracji maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="3c7d3-195">Add the VM name and size to the VM configuration.</span></span>

```powershell
$vm = New-AzureRmVMConfig -VMName $vmName -VMSize $vmSize
```

## <a name="set-the-vm-image-as-source-image-for-the-new-vm"></a><span data-ttu-id="3c7d3-196">Ustaw obraz maszyny Wirtualnej jako źródło obrazu dla nowej maszyny Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="3c7d3-196">Set the VM image as source image for the new VM</span></span>

<span data-ttu-id="3c7d3-197">Ustaw obraz źródłowy przy użyciu Identyfikatora zarządzanego obrazu maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="3c7d3-197">Set the source image using the ID of the managed VM image.</span></span>

```powershell
$vm = Set-AzureRmVMSourceImage -VM $vm -Id $image.Id
```

## <a name="set-the-os-configuration-and-add-the-nic"></a><span data-ttu-id="3c7d3-198">Ustawienia konfiguracji systemu operacyjnego i Dodaj kartę sieciową.</span><span class="sxs-lookup"><span data-stu-id="3c7d3-198">Set the OS configuration and add the NIC.</span></span>

<span data-ttu-id="3c7d3-199">Wprowadź typ magazynu (PremiumLRS lub StandardLRS) i rozmiar dysku systemu operacyjnego.</span><span class="sxs-lookup"><span data-stu-id="3c7d3-199">Enter the storage type (PremiumLRS or StandardLRS) and the size of the OS disk.</span></span> <span data-ttu-id="3c7d3-200">W tym przykładzie typ konta w *PremiumLRS*, rozmiar dysku do *128 GB* i buforowanie dysku, aby *ReadWrite*.</span><span class="sxs-lookup"><span data-stu-id="3c7d3-200">This example sets the account type to *PremiumLRS*, the disk size to *128 GB* and disk caching to *ReadWrite*.</span></span>

```powershell
$vm = Set-AzureRmVMOSDisk -VM $vm -DiskSizeInGB 128 `
-CreateOption FromImage -Caching ReadWrite

$vm = Set-AzureRmVMOperatingSystem -VM $vm -Windows -ComputerName $computerName `
-Credential $cred -ProvisionVMAgent -EnableAutoUpdate

$vm = Add-AzureRmVMNetworkInterface -VM $vm -Id $nic.Id
```

## <a name="create-the-vm"></a><span data-ttu-id="3c7d3-201">Tworzenie maszyny wirtualnej</span><span class="sxs-lookup"><span data-stu-id="3c7d3-201">Create the VM</span></span>

<span data-ttu-id="3c7d3-202">Tworzenie nowej maszyny Wirtualnej za pomocą konfiguracji przechowywanej w **$vm** zmiennej.</span><span class="sxs-lookup"><span data-stu-id="3c7d3-202">Create the new VM using the configuration stored in the **$vm** variable.</span></span>

```powershell
New-AzureRmVM -VM $vm -ResourceGroupName $rgName -Location $location
```

## <a name="verify-that-the-vm-was-created"></a><span data-ttu-id="3c7d3-203">Sprawdź, czy maszyna wirtualna została utworzona</span><span class="sxs-lookup"><span data-stu-id="3c7d3-203">Verify that the VM was created</span></span>
<span data-ttu-id="3c7d3-204">Po zakończeniu powinien zostać wyświetlony nowo utworzony maszyny Wirtualnej w ramach [portalu Azure](https://portal.azure.com) w obszarze **Przeglądaj** > **maszyn wirtualnych**, lub za pomocą następujących poleceń programu PowerShell:</span><span class="sxs-lookup"><span data-stu-id="3c7d3-204">When complete, you should see the newly created VM in the [Azure portal](https://portal.azure.com) under **Browse** > **Virtual machines**, or by using the following PowerShell commands:</span></span>

```powershell
    $vmList = Get-AzureRmVM -ResourceGroupName $rgName
    $vmList.Name
```

## <a name="next-steps"></a><span data-ttu-id="3c7d3-205">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="3c7d3-205">Next steps</span></span>

<span data-ttu-id="3c7d3-206">Aby zalogować się do nowej maszyny wirtualnej, przejdź do maszyny Wirtualnej w [portal](https://portal.azure.com), kliknij przycisk **Connect**i Otwórz plik RDP pulpitu zdalnego.</span><span class="sxs-lookup"><span data-stu-id="3c7d3-206">To sign in to your new virtual machine, browse to the VM in the [portal](https://portal.azure.com), click **Connect**, and open the Remote Desktop RDP file.</span></span> <span data-ttu-id="3c7d3-207">Korzystać z poświadczeń konta oryginalnego maszyny wirtualnej, aby zalogować się do nowej maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="3c7d3-207">Use the account credentials of your original virtual machine to sign in to your new virtual machine.</span></span> <span data-ttu-id="3c7d3-208">Aby uzyskać więcej informacji, zobacz [jak połączenia i zaloguj się do maszyny wirtualnej platformy Azure systemem Windows](connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="3c7d3-208">For more information, see [How to connect and log on to an Azure virtual machine running Windows](connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> 

