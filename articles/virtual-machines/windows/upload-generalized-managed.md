---
title: "aaaCreate na zarządzanej maszynie Wirtualnej Azure z wirtualnego dysku twardego uogólnionego lokalnymi | Dokumentacja firmy Microsoft"
description: "Przekaż uogólniony tooAzure wirtualnego dysku twardego i korzystać z niego toocreate nowych maszyn wirtualnych w modelu wdrażania usługi Resource Manager hello."
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
ms.openlocfilehash: 2fd0c0eec922e6ca8af4e712c1bceb1f9466105c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="upload-a-generalized-vhd-and-use-it-toocreate-new-vms-in-azure"></a><span data-ttu-id="b35ad-103">Przekaż uogólniony wirtualny dysk twardy i korzystać z niego toocreate nowych maszyn wirtualnych na platformie Azure</span><span class="sxs-lookup"><span data-stu-id="b35ad-103">Upload a generalized VHD and use it toocreate new VMs in Azure</span></span>

<span data-ttu-id="b35ad-104">W tym temacie przedstawiono przy użyciu programu PowerShell tooupload dysku VHD uogólniony tooAzure maszyny Wirtualnej, tworzenie obrazu na podstawie hello wirtualnego dysku twardego i utworzyć nową maszynę Wirtualną z tego obrazu.</span><span class="sxs-lookup"><span data-stu-id="b35ad-104">This topic walks you through using PowerShell tooupload a VHD of a generalized VM tooAzure, create an image from hello VHD and create a new VM from that image.</span></span> <span data-ttu-id="b35ad-105">Możesz przekazać dysku VHD wyeksportowane z narzędzia wirtualizacji lokalnej lub innej chmury.</span><span class="sxs-lookup"><span data-stu-id="b35ad-105">You can upload a VHD exported from an on-premises virtualization tool or from another cloud.</span></span> <span data-ttu-id="b35ad-106">Przy użyciu [dysków zarządzanych](managed-disks-overview.md) dla hello upraszcza zarządzanie wirtualna hello nowej maszyny Wirtualnej i zapewnia większą dostępność, gdy hello maszyna wirtualna jest umieszczona w zestawie dostępności.</span><span class="sxs-lookup"><span data-stu-id="b35ad-106">Using [Managed Disks](managed-disks-overview.md) for hello new VM simplifies hello VM managment and provides better availability when hello VM is placed in an availability set.</span></span> 

<span data-ttu-id="b35ad-107">Jeśli chcesz toouse przykładowego skryptu, zobacz [przykładowy skrypt tooupload tooAzure wirtualnego dysku twardego i utworzyć nową maszynę Wirtualną](../scripts/virtual-machines-windows-powershell-upload-generalized-script.md)</span><span class="sxs-lookup"><span data-stu-id="b35ad-107">If you want toouse a sample script, see [Sample script tooupload a VHD tooAzure and create a new VM](../scripts/virtual-machines-windows-powershell-upload-generalized-script.md)</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="b35ad-108">Przed rozpoczęciem</span><span class="sxs-lookup"><span data-stu-id="b35ad-108">Before you begin</span></span>

- <span data-ttu-id="b35ad-109">Przed przekazaniem tooAzure dowolnego wirtualnego dysku twardego, należy wykonać [przygotowanie tooAzure tooupload Windows VHD lub VHDX](prepare-for-upload-vhd-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="b35ad-109">Before uploading any VHD tooAzure, you should follow [Prepare a Windows VHD or VHDX tooupload tooAzure](prepare-for-upload-vhd-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)</span></span>
- <span data-ttu-id="b35ad-110">Przegląd [planowanie migracji hello dysków tooManaged](on-prem-to-azure.md#plan-for-the-migration-to-managed-disks) przed rozpoczęciem migracji zbyt[dysków zarządzanych](managed-disks-overview.md).</span><span class="sxs-lookup"><span data-stu-id="b35ad-110">Review [Plan for hello migration tooManaged Disks](on-prem-to-azure.md#plan-for-the-migration-to-managed-disks) before starting your migration too[Managed Disks](managed-disks-overview.md).</span></span>
- <span data-ttu-id="b35ad-111">Upewnij się, że masz najnowszą wersję hello modułu AzureRM.Compute PowerShell hello.</span><span class="sxs-lookup"><span data-stu-id="b35ad-111">Make sure that you have hello latest version of hello AzureRM.Compute PowerShell module.</span></span> <span data-ttu-id="b35ad-112">Uruchom hello następujących tooinstall polecenia.</span><span class="sxs-lookup"><span data-stu-id="b35ad-112">Run hello following command tooinstall it.</span></span>

    ```powershell
    Install-Module AzureRM.Compute -RequiredVersion 2.6.0
    ```
    <span data-ttu-id="b35ad-113">Aby uzyskać więcej informacji, zobacz [przechowywanie wersji programu Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="b35ad-113">For more information, see [Azure PowerShell Versioning](/powershell/azure/overview).</span></span>


## <a name="generalize-hello-windows-vm-using-sysprep"></a><span data-ttu-id="b35ad-114">Generalize hello maszyny Wirtualnej systemu Windows za pomocą programu Sysprep</span><span class="sxs-lookup"><span data-stu-id="b35ad-114">Generalize hello Windows VM using Sysprep</span></span>

<span data-ttu-id="b35ad-115">Program Sysprep usuwa wszystkie informacje osobiste konto, między innymi i przygotowuje toobe maszyny hello użyty jako obraz.</span><span class="sxs-lookup"><span data-stu-id="b35ad-115">Sysprep removes all your personal account information, among other things, and prepares hello machine toobe used as an image.</span></span> <span data-ttu-id="b35ad-116">Aby uzyskać więcej informacji o narzędziu Sysprep, zobacz [jak tooUse Sysprep: wprowadzenie](http://technet.microsoft.com/library/bb457073.aspx).</span><span class="sxs-lookup"><span data-stu-id="b35ad-116">For details about Sysprep, see [How tooUse Sysprep: An Introduction](http://technet.microsoft.com/library/bb457073.aspx).</span></span>

<span data-ttu-id="b35ad-117">Upewnij się, że hello ról serwera uruchomionych na maszynie hello są obsługiwane przez program Sysprep.</span><span class="sxs-lookup"><span data-stu-id="b35ad-117">Make sure hello server roles running on hello machine are supported by Sysprep.</span></span> <span data-ttu-id="b35ad-118">Aby uzyskać więcej informacji, zobacz [Obsługa programu Sysprep dla ról serwera](https://msdn.microsoft.com/windows/hardware/commercialize/manufacture/desktop/sysprep-support-for-server-roles)</span><span class="sxs-lookup"><span data-stu-id="b35ad-118">For more information, see [Sysprep Support for Server Roles](https://msdn.microsoft.com/windows/hardware/commercialize/manufacture/desktop/sysprep-support-for-server-roles)</span></span>

> [!IMPORTANT]
> <span data-ttu-id="b35ad-119">Jeśli korzystasz z programu Sysprep przed przekazaniem tooAzure Twojego dysku VHD na powitania po raz pierwszy, upewnij się, masz [przygotować maszyny Wirtualnej](prepare-for-upload-vhd-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) przed uruchomieniem programu Sysprep.</span><span class="sxs-lookup"><span data-stu-id="b35ad-119">If you are running Sysprep before uploading your VHD tooAzure for hello first time, make sure you have [prepared your VM](prepare-for-upload-vhd-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) before running Sysprep.</span></span> 
> 
> 

1. <span data-ttu-id="b35ad-120">Zaloguj się toohello maszyny wirtualnej systemu Windows.</span><span class="sxs-lookup"><span data-stu-id="b35ad-120">Sign in toohello Windows virtual machine.</span></span>
2. <span data-ttu-id="b35ad-121">Otwórz okno wiersza polecenia hello jako administrator.</span><span class="sxs-lookup"><span data-stu-id="b35ad-121">Open hello Command Prompt window as an administrator.</span></span> <span data-ttu-id="b35ad-122">Zmień katalog hello zbyt**%windir%\system32\sysprep**, a następnie uruchom `sysprep.exe`.</span><span class="sxs-lookup"><span data-stu-id="b35ad-122">Change hello directory too**%windir%\system32\sysprep**, and then run `sysprep.exe`.</span></span>
3. <span data-ttu-id="b35ad-123">W hello **narzędzie przygotowania systemu** okno dialogowe, wybierz opcję **wprowadź systemu Out-of-Box Experience (OOBE)**i upewnij się, że hello **Generalize** pole wyboru jest zaznaczone.</span><span class="sxs-lookup"><span data-stu-id="b35ad-123">In hello **System Preparation Tool** dialog box, select **Enter System Out-of-Box Experience (OOBE)**, and make sure that hello **Generalize** check box is selected.</span></span>
4. <span data-ttu-id="b35ad-124">W **opcje zamykania**, wybierz pozycję **zamknięcia**.</span><span class="sxs-lookup"><span data-stu-id="b35ad-124">In **Shutdown Options**, select **Shutdown**.</span></span>
5. <span data-ttu-id="b35ad-125">Kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="b35ad-125">Click **OK**.</span></span>
   
    ![Uruchom program Sysprep](./media/upload-generalized-managed/sysprepgeneral.png)
6. <span data-ttu-id="b35ad-127">Po zakończeniu działania programu Sysprep, zamyka hello maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="b35ad-127">When Sysprep completes, it shuts down hello virtual machine.</span></span> <span data-ttu-id="b35ad-128">Nie uruchamiaj ponownie hello maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="b35ad-128">Do not restart hello VM.</span></span>



## <a name="log-in-tooazure"></a><span data-ttu-id="b35ad-129">Zaloguj się za tooAzure</span><span class="sxs-lookup"><span data-stu-id="b35ad-129">Log in tooAzure</span></span>
<span data-ttu-id="b35ad-130">Jeśli nie masz jeszcze programu PowerShell w wersji 1.4 lub nowszy zainstalowany, przeczytaj [jak tooinstall i konfigurowanie programu Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="b35ad-130">If you don't already have PowerShell version 1.4 or above installed, read [How tooinstall and configure Azure PowerShell](/powershell/azure/overview).</span></span>

1. <span data-ttu-id="b35ad-131">Otwórz program Azure PowerShell i zaloguj się na tooyour konto platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="b35ad-131">Open Azure PowerShell and sign in tooyour Azure account.</span></span> <span data-ttu-id="b35ad-132">Zostanie otwarte okno podręczne dla tooenter możesz poświadczenia konta Azure.</span><span class="sxs-lookup"><span data-stu-id="b35ad-132">A pop-up window opens for you tooenter your Azure account credentials.</span></span>
   
    ```powershell
    Login-AzureRmAccount
    ```
2. <span data-ttu-id="b35ad-133">Uzyskanie subskrypcji hello identyfikatorów subskrypcji dostępne.</span><span class="sxs-lookup"><span data-stu-id="b35ad-133">Get hello subscription IDs for your available subscriptions.</span></span>
   
    ```powershell
    Get-AzureRmSubscription
    ```
3. <span data-ttu-id="b35ad-134">Ustaw poprawną subskrypcję hello przy użyciu identyfikatora hello subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="b35ad-134">Set hello correct subscription using hello subscription ID.</span></span> <span data-ttu-id="b35ad-135">Zastąp  *<subscriptionID>*  o identyfikatorze hello hello Popraw subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="b35ad-135">Replace *<subscriptionID>* with hello ID of hello correct subscription.</span></span>
   
    ```powershell
    Select-AzureRmSubscription -SubscriptionId "<subscriptionID>"
    ```

## <a name="get-hello-storage-account"></a><span data-ttu-id="b35ad-136">Pobierz hello konta magazynu</span><span class="sxs-lookup"><span data-stu-id="b35ad-136">Get hello storage account</span></span>
<span data-ttu-id="b35ad-137">Musisz mieć konto magazynu, w obrazie maszyny Wirtualnej Azure toostore hello przekazany.</span><span class="sxs-lookup"><span data-stu-id="b35ad-137">You need a storage account in Azure toostore hello uploaded VM image.</span></span> <span data-ttu-id="b35ad-138">Możesz użyć istniejącego konta magazynu lub Utwórz nową.</span><span class="sxs-lookup"><span data-stu-id="b35ad-138">You can either use an existing storage account or create a new one.</span></span> 

<span data-ttu-id="b35ad-139">Jeśli będziesz używać hello wirtualnego dysku twardego toocreate dysków zarządzanych dla maszyny Wirtualnej, Lokalizacja konta magazynu hello musi być tej samej lokalizacji hello, w którym zostanie utworzony hello maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="b35ad-139">If you will be using hello VHD toocreate a managed disk for a VM, hello storage account location must be same hello location where you will be creating hello VM.</span></span>

<span data-ttu-id="b35ad-140">tooshow hello dostępny magazyn kont, wpisz:</span><span class="sxs-lookup"><span data-stu-id="b35ad-140">tooshow hello available storage accounts, type:</span></span>

```powershell
Get-AzureRmStorageAccount
```

<span data-ttu-id="b35ad-141">Jeśli chcesz toouse istniejącego konta magazynu, przejdź toohello [obrazu maszyny Wirtualnej hello przekazywania](#upload-the-vm-vhd-to-your-storage-account) sekcji.</span><span class="sxs-lookup"><span data-stu-id="b35ad-141">If you want toouse an existing storage account, proceed toohello [Upload hello VM image](#upload-the-vm-vhd-to-your-storage-account) section.</span></span>

<span data-ttu-id="b35ad-142">Jeśli potrzebujesz toocreate konta magazynu, wykonaj następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="b35ad-142">If you need toocreate a storage account, follow these steps:</span></span>

1. <span data-ttu-id="b35ad-143">Potrzebna jest nazwa hello hello grupy zasobów, których można utworzyć konta magazynu hello.</span><span class="sxs-lookup"><span data-stu-id="b35ad-143">You need hello name of hello resource group where hello storage account should be created.</span></span> <span data-ttu-id="b35ad-144">toofind limit wszystkie hello grupy zasobów, które są w ramach subskrypcji, wpisz:</span><span class="sxs-lookup"><span data-stu-id="b35ad-144">toofind out all hello resource groups that are in your subscription, type:</span></span>
   
    ```powershell
    Get-AzureRmResourceGroup
    ```

    <span data-ttu-id="b35ad-145">Grupa zasobów o nazwie toocreate **myResourceGroup** w hello **wschodnie stany USA** regionu, wpisz:</span><span class="sxs-lookup"><span data-stu-id="b35ad-145">toocreate a resource group named **myResourceGroup** in hello **East US** region, type:</span></span>

    ```powershell
    New-AzureRmResourceGroup -Name myResourceGroup -Location "East US"
    ```

2. <span data-ttu-id="b35ad-146">Utwórz konto magazynu o nazwie **mojekontomagazynu** w tej grupie zasobów za pomocą hello [New-AzureRmStorageAccount](/powershell/module/azurerm.storage/new-azurermstorageaccount) polecenia cmdlet:</span><span class="sxs-lookup"><span data-stu-id="b35ad-146">Create a storage account named **mystorageaccount** in this resource group by using hello [New-AzureRmStorageAccount](/powershell/module/azurerm.storage/new-azurermstorageaccount) cmdlet:</span></span>
   
    ```powershell
    New-AzureRmStorageAccount -ResourceGroupName myResourceGroup -Name mystorageaccount -Location "East US"`
        -SkuName "Standard_LRS" -Kind "Storage"
    ```
   
    <span data-ttu-id="b35ad-147">Prawidłowe wartości - SkuName to:</span><span class="sxs-lookup"><span data-stu-id="b35ad-147">Valid values for -SkuName are:</span></span>
   
   * <span data-ttu-id="b35ad-148">**Standard_LRS** — magazyn lokalnie nadmiarowy.</span><span class="sxs-lookup"><span data-stu-id="b35ad-148">**Standard_LRS** - Locally redundant storage.</span></span> 
   * <span data-ttu-id="b35ad-149">**Standard_ZRS** -strefy nadmiarowego magazynu.</span><span class="sxs-lookup"><span data-stu-id="b35ad-149">**Standard_ZRS** - Zone redundant storage.</span></span>
   * <span data-ttu-id="b35ad-150">**Standard_GRS** — z magazynu geograficznie nadmiarowego magazynu.</span><span class="sxs-lookup"><span data-stu-id="b35ad-150">**Standard_GRS** - Geo redundant storage.</span></span> 
   * <span data-ttu-id="b35ad-151">**Standard_RAGRS** -dostęp do odczytu z magazynu geograficznie nadmiarowego magazynu.</span><span class="sxs-lookup"><span data-stu-id="b35ad-151">**Standard_RAGRS** - Read access geo redundant storage.</span></span> 
   * <span data-ttu-id="b35ad-152">**Premium_LRS** — magazyn lokalnie nadmiarowy Premium.</span><span class="sxs-lookup"><span data-stu-id="b35ad-152">**Premium_LRS** - Premium locally redundant storage.</span></span> 

## <a name="upload-hello-vhd-tooyour-storage-account"></a><span data-ttu-id="b35ad-153">Przekaż konta magazynu tooyour wirtualnego dysku twardego hello</span><span class="sxs-lookup"><span data-stu-id="b35ad-153">Upload hello VHD tooyour storage account</span></span>

<span data-ttu-id="b35ad-154">Użyj hello [AzureRmVhd Dodaj](https://msdn.microsoft.com/library/mt603554.aspx) polecenia cmdlet tooupload hello wirtualnego dysku twardego tooa kontenera na koncie magazynu.</span><span class="sxs-lookup"><span data-stu-id="b35ad-154">Use hello [Add-AzureRmVhd](https://msdn.microsoft.com/library/mt603554.aspx) cmdlet tooupload hello VHD tooa container in your storage account.</span></span> <span data-ttu-id="b35ad-155">W tym przykładzie przekazywania hello pliku *myVHD.vhd* z *"dyski twarde C:\Users\Public\Documents\Virtual\"*  tooa konto magazynu o nazwie *mojekontomagazynu*w hello *myResourceGroup* grupy zasobów.</span><span class="sxs-lookup"><span data-stu-id="b35ad-155">This example uploads hello file *myVHD.vhd* from *"C:\Users\Public\Documents\Virtual hard disks\"* tooa storage account named *mystorageaccount* in hello *myResourceGroup* resource group.</span></span> <span data-ttu-id="b35ad-156">Plik Hello zostaną umieszczone w hello kontener o nazwie *mojkontener* i będzie hello nową nazwę pliku *myUploadedVHD.vhd*.</span><span class="sxs-lookup"><span data-stu-id="b35ad-156">hello file will be placed into hello container named *mycontainer* and hello new file name will be *myUploadedVHD.vhd*.</span></span>

```powershell
$rgName = "myResourceGroup"
$urlOfUploadedImageVhd = "https://mystorageaccount.blob.core.windows.net/mycontainer/myUploadedVHD.vhd"
Add-AzureRmVhd -ResourceGroupName $rgName -Destination $urlOfUploadedImageVhd `
    -LocalFilePath "C:\Users\Public\Documents\Virtual hard disks\myVHD.vhd"
```


<span data-ttu-id="b35ad-157">W przypadku powodzenia można uzyskać odpowiedzi, która wygląda podobnie toothis:</span><span class="sxs-lookup"><span data-stu-id="b35ad-157">If successful, you get a response that looks similar toothis:</span></span>

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

<span data-ttu-id="b35ad-158">W zależności od połączenia sieciowego i hello rozmiar pliku VHD, polecenie to może chwilę potrwać toocomplete</span><span class="sxs-lookup"><span data-stu-id="b35ad-158">Depending on your network connection and hello size of your VHD file, this command may take a while toocomplete</span></span>

<span data-ttu-id="b35ad-159">Zapisz hello **docelowy identyfikator URI** toouse ścieżkę później, jeżeli zostanie toocreate dysków zarządzanych lub nowej maszyny Wirtualnej przy użyciu hello przekazywać wirtualnego dysku twardego.</span><span class="sxs-lookup"><span data-stu-id="b35ad-159">Save hello **Destination URI** path toouse later if you are going toocreate a managed disk or a new VM using hello uploaded VHD.</span></span>

### <a name="other-options-for-uploading-a-vhd"></a><span data-ttu-id="b35ad-160">Inne opcje przekazywanie wirtualnego dysku twardego</span><span class="sxs-lookup"><span data-stu-id="b35ad-160">Other options for uploading a VHD</span></span>
 
 
<span data-ttu-id="b35ad-161">Możesz również przekazywać konta magazynu wirtualnego dysku twardego tooyour przy użyciu jednej z następujących hello:</span><span class="sxs-lookup"><span data-stu-id="b35ad-161">You can also upload a VHD tooyour storage account using one of hello following:</span></span>

- [<span data-ttu-id="b35ad-162">Narzędzie AzCopy</span><span class="sxs-lookup"><span data-stu-id="b35ad-162">AzCopy</span></span>](http://aka.ms/downloadazcopy)
- [<span data-ttu-id="b35ad-163">Obiektu Blob magazynu Azure kopiowania interfejsu API</span><span class="sxs-lookup"><span data-stu-id="b35ad-163">Azure Storage Copy Blob API</span></span>](https://msdn.microsoft.com/library/azure/dd894037.aspx)
- [<span data-ttu-id="b35ad-164">Obiekty BLOB magazynu Azure Explorer przekazywania</span><span class="sxs-lookup"><span data-stu-id="b35ad-164">Azure Storage Explorer Uploading Blobs</span></span>](https://azurestorageexplorer.codeplex.com/)
- [<span data-ttu-id="b35ad-165">Dokumentacja interfejsu API REST usługi Import/Eksport magazynu</span><span class="sxs-lookup"><span data-stu-id="b35ad-165">Storage Import/Export Service REST API Reference</span></span>](https://msdn.microsoft.com/library/dn529096.aspx)
-   <span data-ttu-id="b35ad-166">Zaleca się za pomocą usługi Import/eksport, jeśli szacowany czas przekazywania jest dłuższa niż 7 dni.</span><span class="sxs-lookup"><span data-stu-id="b35ad-166">We recommend using Import/Export Service if estimated uploading time is longer than 7 days.</span></span> <span data-ttu-id="b35ad-167">Można użyć [DataTransferSpeedCalculator](https://github.com/Azure-Samples/storage-dotnet-import-export-job-management/blob/master/DataTransferSpeedCalculator.html) tooestimate hello czasu z jednostki rozmiaru i transferu danych.</span><span class="sxs-lookup"><span data-stu-id="b35ad-167">You can use [DataTransferSpeedCalculator](https://github.com/Azure-Samples/storage-dotnet-import-export-job-management/blob/master/DataTransferSpeedCalculator.html) tooestimate hello time from data size and transfer unit.</span></span> 
    <span data-ttu-id="b35ad-168">Import/Eksport można używać konta standard storage tooa toocopy.</span><span class="sxs-lookup"><span data-stu-id="b35ad-168">Import/Export can be used toocopy tooa standard storage account.</span></span> <span data-ttu-id="b35ad-169">Konieczne będzie toocopy z konta magazynu toopremium standard storage przy użyciu narzędzia, takiego jak narzędzie AzCopy.</span><span class="sxs-lookup"><span data-stu-id="b35ad-169">You will need toocopy from standard storage toopremium storage account using a tool like AzCopy.</span></span>


## <a name="create-a-managed-image-from-hello-uploaded-vhd"></a><span data-ttu-id="b35ad-170">Tworzenie zarządzanego obrazu z hello przekazać wirtualnego dysku twardego</span><span class="sxs-lookup"><span data-stu-id="b35ad-170">Create a managed image from hello uploaded VHD</span></span> 

<span data-ttu-id="b35ad-171">Tworzenie obrazu zarządzanych za pomocą programu uogólniony wirtualny dysk twardy systemu operacyjnego.</span><span class="sxs-lookup"><span data-stu-id="b35ad-171">Create a managed image using your generalized OS VHD.</span></span> <span data-ttu-id="b35ad-172">Zastąp wartości hello odpowiednimi informacjami.</span><span class="sxs-lookup"><span data-stu-id="b35ad-172">Replace hello values with your own information.</span></span>


1.  <span data-ttu-id="b35ad-173">Najpierw należy ustawić hello typowe parametry:</span><span class="sxs-lookup"><span data-stu-id="b35ad-173">First, set hello common parameters:</span></span>

    ```powershell
    $vmName = "myVM"
    $computerName = "myComputer"
    $vmSize = "Standard_DS1_v2"
    $location = "East US" 
    $imageName = "yourImageName"
    ```

4.  <span data-ttu-id="b35ad-174">Utwórz obraz powitania przy użyciu Twojej uogólniony wirtualny dysk twardy systemu operacyjnego.</span><span class="sxs-lookup"><span data-stu-id="b35ad-174">Create hello image using your generalized OS VHD.</span></span>

    ```powershell
    $imageConfig = New-AzureRmImageConfig -Location $location
    $imageConfig = Set-AzureRmImageOsDisk -Image $imageConfig -OsType Windows -OsState Generalized -BlobUri $urlOfUploadedImageVhd
    $image = New-AzureRmImage -ImageName $imageName -ResourceGroupName $rgName -Image $imageConfig
    ```

## <a name="create-a-virtual-network"></a><span data-ttu-id="b35ad-175">Tworzenie sieci wirtualnej</span><span class="sxs-lookup"><span data-stu-id="b35ad-175">Create a virtual network</span></span>
<span data-ttu-id="b35ad-176">Tworzenie sieci wirtualnej hello i podsieci hello [sieci wirtualnej](../../virtual-network/virtual-networks-overview.md).</span><span class="sxs-lookup"><span data-stu-id="b35ad-176">Create hello vNet and subnet of hello [virtual network](../../virtual-network/virtual-networks-overview.md).</span></span>

1. <span data-ttu-id="b35ad-177">Utwórz podsieć hello.</span><span class="sxs-lookup"><span data-stu-id="b35ad-177">Create hello subnet.</span></span> <span data-ttu-id="b35ad-178">W tym przykładzie tworzy podsieć o nazwie *mySubnet* z prefiksu adresu hello *10.0.0.0/24*.</span><span class="sxs-lookup"><span data-stu-id="b35ad-178">This example creates a subnet named *mySubnet* with hello address prefix of *10.0.0.0/24*.</span></span>  
   
    ```powershell
    $subnetName = "mySubnet"
    $singleSubnet = New-AzureRmVirtualNetworkSubnetConfig -Name $subnetName -AddressPrefix 10.0.0.0/24
    ```
2. <span data-ttu-id="b35ad-179">Utwórz sieć wirtualną hello.</span><span class="sxs-lookup"><span data-stu-id="b35ad-179">Create hello virtual network.</span></span> <span data-ttu-id="b35ad-180">W tym przykładzie tworzy sieć wirtualną o nazwie *myVnet* z prefiksu adresu hello *10.0.0.0/16*.</span><span class="sxs-lookup"><span data-stu-id="b35ad-180">This example creates a virtual network named *myVnet* with hello address prefix of *10.0.0.0/16*.</span></span>  
   
    ```powershell
    $vnetName = "myVnet"
    $vnet = New-AzureRmVirtualNetwork -Name $vnetName -ResourceGroupName $rgName -Location $location `
        -AddressPrefix 10.0.0.0/16 -Subnet $singleSubnet
    ```    

## <a name="create-a-public-ip-address-and-network-interface"></a><span data-ttu-id="b35ad-181">Tworzenie publicznego adresu IP adres i interfejsu sieciowego</span><span class="sxs-lookup"><span data-stu-id="b35ad-181">Create a public IP address and network interface</span></span>

<span data-ttu-id="b35ad-182">tooenable komunikację z maszyną wirtualną hello w sieci wirtualnej hello, należy [publicznego adresu IP](../../virtual-network/virtual-network-ip-addresses-overview-arm.md) i interfejsu sieciowego.</span><span class="sxs-lookup"><span data-stu-id="b35ad-182">tooenable communication with hello virtual machine in hello virtual network, you need a [public IP address](../../virtual-network/virtual-network-ip-addresses-overview-arm.md) and a network interface.</span></span>

1. <span data-ttu-id="b35ad-183">Utwórz publiczny adres IP.</span><span class="sxs-lookup"><span data-stu-id="b35ad-183">Create a public IP address.</span></span> <span data-ttu-id="b35ad-184">W tym przykładzie jest tworzony publiczny adres IP o nazwie *myPip*.</span><span class="sxs-lookup"><span data-stu-id="b35ad-184">This example creates a public IP address named *myPip*.</span></span> 
   
    ```powershell
    $ipName = "myPip"
    $pip = New-AzureRmPublicIpAddress -Name $ipName -ResourceGroupName $rgName -Location $location `
        -AllocationMethod Dynamic
    ```       
2. <span data-ttu-id="b35ad-185">Utwórz hello karty sieciowej.</span><span class="sxs-lookup"><span data-stu-id="b35ad-185">Create hello NIC.</span></span> <span data-ttu-id="b35ad-186">W tym przykładzie jest tworzony karty Sieciowej o nazwie **myNic**.</span><span class="sxs-lookup"><span data-stu-id="b35ad-186">This example creates a NIC named **myNic**.</span></span> 
   
    ```powershell
    $nicName = "myNic"
    $nic = New-AzureRmNetworkInterface -Name $nicName -ResourceGroupName $rgName -Location $location `
        -SubnetId $vnet.Subnets[0].Id -PublicIpAddressId $pip.Id
    ```

## <a name="create-hello-network-security-group-and-an-rdp-rule"></a><span data-ttu-id="b35ad-187">Tworzenie grupy zabezpieczeń sieci hello i reguły protokołu RDP</span><span class="sxs-lookup"><span data-stu-id="b35ad-187">Create hello network security group and an RDP rule</span></span>

<span data-ttu-id="b35ad-188">toobe stanie toolog w tooyour maszyny Wirtualnej przy użyciu protokołu RDP, należy toohave reguły zabezpieczeń sieci (NSG), umożliwiająca dostęp RDP do portu 3389.</span><span class="sxs-lookup"><span data-stu-id="b35ad-188">toobe able toolog in tooyour VM using RDP, you need toohave a network security rule (NSG) that allows RDP access on port 3389.</span></span> 

<span data-ttu-id="b35ad-189">W tym przykładzie tworzy grupy NSG o nazwie *myNsg* zawierający regułę o nazwie *myRdpRule* za pośrednictwem portu 3389 która zezwala na ruch RDP.</span><span class="sxs-lookup"><span data-stu-id="b35ad-189">This example creates an NSG named *myNsg* that contains a rule called *myRdpRule* that allows RDP traffic over port 3389.</span></span> <span data-ttu-id="b35ad-190">Aby uzyskać więcej informacji na temat grup NSG, zobacz [otwierania portów tooa maszyny Wirtualnej na platformie Azure przy użyciu programu PowerShell](nsg-quickstart-powershell.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="b35ad-190">For more information about NSGs, see [Opening ports tooa VM in Azure using PowerShell](nsg-quickstart-powershell.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

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


## <a name="create-a-variable-for-hello-virtual-network"></a><span data-ttu-id="b35ad-191">Utwórz zmienną hello sieci wirtualnej</span><span class="sxs-lookup"><span data-stu-id="b35ad-191">Create a variable for hello virtual network</span></span>

<span data-ttu-id="b35ad-192">Utwórz zmienną ukończyć powitalnych sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="b35ad-192">Create a variable for hello completed virtual network.</span></span> 

```powershell
$vnet = Get-AzureRmVirtualNetwork -ResourceGroupName $rgName -Name $vnetName

```

## <a name="get-hello-credentials-for-hello-vm"></a><span data-ttu-id="b35ad-193">Uzyskać poświadczenia hello hello maszyny Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="b35ad-193">Get hello credentials for hello VM</span></span>

<span data-ttu-id="b35ad-194">Witaj następującego polecenia cmdlet zostanie otwarte okno którym wprowadza użytkownika nowe toouse nazwę i hasło jako hello konta administratora lokalnego na zdalny dostęp do hello maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="b35ad-194">hello following cmdlet will open a window where you will enter a new user name and password toouse as hello local administrator account for remotely accessing hello VM.</span></span> 

```powershell
$cred = Get-Credential
```

## <a name="add-hello-vm-name-and-size-toohello-vm-configuration"></a><span data-ttu-id="b35ad-195">Dodaj hello nazwę maszyny Wirtualnej i konfiguracji maszyny Wirtualnej toohello rozmiar.</span><span class="sxs-lookup"><span data-stu-id="b35ad-195">Add hello VM name and size toohello VM configuration.</span></span>

```powershell
$vm = New-AzureRmVMConfig -VMName $vmName -VMSize $vmSize
```

## <a name="set-hello-vm-image-as-source-image-for-hello-new-vm"></a><span data-ttu-id="b35ad-196">Obraz maszyny Wirtualnej hello zestawu jako obraz źródłowy dla hello nowej maszyny Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="b35ad-196">Set hello VM image as source image for hello new VM</span></span>

<span data-ttu-id="b35ad-197">Ustaw obraz źródłowy hello przy użyciu Identyfikatora hello hello zarządzanego obrazu maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="b35ad-197">Set hello source image using hello ID of hello managed VM image.</span></span>

```powershell
$vm = Set-AzureRmVMSourceImage -VM $vm -Id $image.Id
```

## <a name="set-hello-os-configuration-and-add-hello-nic"></a><span data-ttu-id="b35ad-198">Ustawienia konfiguracji systemu operacyjnego hello i Dodaj hello karty sieciowej.</span><span class="sxs-lookup"><span data-stu-id="b35ad-198">Set hello OS configuration and add hello NIC.</span></span>

<span data-ttu-id="b35ad-199">Wprowadź typ magazynu hello (PremiumLRS lub StandardLRS) i hello rozmiar dysku systemu operacyjnego hello.</span><span class="sxs-lookup"><span data-stu-id="b35ad-199">Enter hello storage type (PremiumLRS or StandardLRS) and hello size of hello OS disk.</span></span> <span data-ttu-id="b35ad-200">W tym przykładzie typ konta hello zbyt*PremiumLRS*, zbyt hello rozmiar dysku*128 GB* i buforowania dysku zbyt*ReadWrite*.</span><span class="sxs-lookup"><span data-stu-id="b35ad-200">This example sets hello account type too*PremiumLRS*, hello disk size too*128 GB* and disk caching too*ReadWrite*.</span></span>

```powershell
$vm = Set-AzureRmVMOSDisk -VM $vm -DiskSizeInGB 128 `
-CreateOption FromImage -Caching ReadWrite

$vm = Set-AzureRmVMOperatingSystem -VM $vm -Windows -ComputerName $computerName `
-Credential $cred -ProvisionVMAgent -EnableAutoUpdate

$vm = Add-AzureRmVMNetworkInterface -VM $vm -Id $nic.Id
```

## <a name="create-hello-vm"></a><span data-ttu-id="b35ad-201">Utwórz hello maszyny Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="b35ad-201">Create hello VM</span></span>

<span data-ttu-id="b35ad-202">Tworzenie nowej maszyny Wirtualnej za pomocą konfiguracji hello przechowywane w hello hello **$vm** zmiennej.</span><span class="sxs-lookup"><span data-stu-id="b35ad-202">Create hello new VM using hello configuration stored in hello **$vm** variable.</span></span>

```powershell
New-AzureRmVM -VM $vm -ResourceGroupName $rgName -Location $location
```

## <a name="verify-that-hello-vm-was-created"></a><span data-ttu-id="b35ad-203">Sprawdź hello, że maszyna wirtualna została utworzona</span><span class="sxs-lookup"><span data-stu-id="b35ad-203">Verify that hello VM was created</span></span>
<span data-ttu-id="b35ad-204">Po zakończeniu powinien zostać wyświetlony hello nowo utworzony maszyny Wirtualnej w hello [portalu Azure](https://portal.azure.com) w obszarze **Przeglądaj** > **maszyn wirtualnych**, lub za pomocą następujących hello Polecenia programu PowerShell:</span><span class="sxs-lookup"><span data-stu-id="b35ad-204">When complete, you should see hello newly created VM in hello [Azure portal](https://portal.azure.com) under **Browse** > **Virtual machines**, or by using hello following PowerShell commands:</span></span>

```powershell
    $vmList = Get-AzureRmVM -ResourceGroupName $rgName
    $vmList.Name
```

## <a name="next-steps"></a><span data-ttu-id="b35ad-205">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="b35ad-205">Next steps</span></span>

<span data-ttu-id="b35ad-206">toosign w tooyour nowej maszyny wirtualnej, przeglądania toohello maszyny Wirtualnej w hello [portal](https://portal.azure.com), kliknij przycisk **Connect**i hello Otwórz plik RDP pulpitu zdalnego.</span><span class="sxs-lookup"><span data-stu-id="b35ad-206">toosign in tooyour new virtual machine, browse toohello VM in hello [portal](https://portal.azure.com), click **Connect**, and open hello Remote Desktop RDP file.</span></span> <span data-ttu-id="b35ad-207">Użyj poświadczeń konta hello z oryginalnego toosign maszyny wirtualnej w tooyour nowej maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="b35ad-207">Use hello account credentials of your original virtual machine toosign in tooyour new virtual machine.</span></span> <span data-ttu-id="b35ad-208">Aby uzyskać więcej informacji, zobacz [jak dziennika na tooan wirtualnej platformy Azure i tooconnect maszyny, systemem operacyjnym Windows](connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="b35ad-208">For more information, see [How tooconnect and log on tooan Azure virtual machine running Windows](connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> 

