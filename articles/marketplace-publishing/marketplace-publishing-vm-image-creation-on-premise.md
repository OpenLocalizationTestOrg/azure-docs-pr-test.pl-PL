---
title: aaaCreating obrazu maszyny wirtualnej lokalnymi hello Azure Marketplace | Dokumentacja firmy Microsoft
description: "Zrozumienie i wykonać hello kroki toocreate lokalnej obrazu maszyny Wirtualnej i wdrożenie toohello portalu Azure Marketplace innym toopurchase."
services: marketplace-publishing
documentationcenter: 
author: HannibalSII
manager: hascipio
editor: 
ms.assetid: 26dfbd5a-8685-4b19-987e-c20ca60540ec
ms.service: marketplace
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: Azure
ms.workload: na
ms.date: 04/29/2016
ms.author: hascipio; v-divte
ms.openlocfilehash: c7a265330f1e494db8d0e981a38ee00d85746bb1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="develop-an-on-premises-virtual-machine-image-for-hello-azure-marketplace"></a><span data-ttu-id="6de9e-103">Tworzenie obrazu maszyny wirtualnej lokalnymi hello Azure Marketplace</span><span class="sxs-lookup"><span data-stu-id="6de9e-103">Develop an on-premises virtual machine image for hello Azure Marketplace</span></span>
<span data-ttu-id="6de9e-104">Zdecydowanie zaleca się tworzenie Azure wirtualnych dysków twardych (VHD) bezpośrednio w chmurze hello przy użyciu protokołu Remote Desktop Protocol.</span><span class="sxs-lookup"><span data-stu-id="6de9e-104">We strongly recommend that you develop Azure virtual hard disks (VHDs) directly in hello cloud by using Remote Desktop Protocol.</span></span> <span data-ttu-id="6de9e-105">Jednak jeśli użytkownik musi jest możliwe toodownload wirtualnego dysku twardego i opracowanie go za pomocą infrastruktury lokalnej.</span><span class="sxs-lookup"><span data-stu-id="6de9e-105">However, if you must, it is possible toodownload a VHD and develop it by using on-premises infrastructure.</span></span>  

<span data-ttu-id="6de9e-106">Dla rozwoju lokalnych, należy pobrać systemu operacyjnego hello hello utworzony dysk VHD maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="6de9e-106">For on-premises development, you must download hello operating system VHD of hello created VM.</span></span> <span data-ttu-id="6de9e-107">Te kroki nastąpiłoby w ramach kroku 3.3 powyżej.</span><span class="sxs-lookup"><span data-stu-id="6de9e-107">These steps would take place as part of step 3.3, above.</span></span>  

## <a name="download-a-vhd-image"></a><span data-ttu-id="6de9e-108">Pobranie obrazu wirtualnego dysku twardego</span><span class="sxs-lookup"><span data-stu-id="6de9e-108">Download a VHD image</span></span>
### <a name="locate-a-blob-url"></a><span data-ttu-id="6de9e-109">Znajdź adres URL obiektu blob</span><span class="sxs-lookup"><span data-stu-id="6de9e-109">Locate a blob URL</span></span>
<span data-ttu-id="6de9e-110">W kolejności toodownload hello dysku VHD w pierwszej kolejności zlokalizować adresu URL obiektu blob hello hello dysku systemu operacyjnego.</span><span class="sxs-lookup"><span data-stu-id="6de9e-110">In order toodownload hello VHD, first locate hello blob URL for hello operating system disk.</span></span>

<span data-ttu-id="6de9e-111">Znajdź nowego adresu URL obiektu blob hello z hello [portalu Microsoft Azure](https://portal.azure.com):</span><span class="sxs-lookup"><span data-stu-id="6de9e-111">Locate hello blob URL from hello new [Microsoft Azure portal](https://portal.azure.com):</span></span>

1. <span data-ttu-id="6de9e-112">Przejdź za**Przeglądaj** > **maszyn wirtualnych**, i wybierz opcję hello wdrożeniu maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="6de9e-112">Go too**Browse** > **VMs**, and then select hello deployed VM.</span></span>
2. <span data-ttu-id="6de9e-113">W obszarze **Konfiguruj**, wybierz pozycję hello **dysków** kafelka, która otwiera blok dysków hello.</span><span class="sxs-lookup"><span data-stu-id="6de9e-113">Under **Configure**, select hello **Disks** tile, which opens hello Disks blade.</span></span>
   
   ![Rysowanie](media/marketplace-publishing-vm-image-creation-on-premise/img01.png)
3. <span data-ttu-id="6de9e-115">Wybierz hello **dysk systemu operacyjnego**, która otwiera blok innego, który wyświetla właściwości dysku, w tym hello lokalizacja wirtualnego dysku twardego.</span><span class="sxs-lookup"><span data-stu-id="6de9e-115">Select hello **OS Disk**, which opens another blade that displays disk properties, including hello VHD location.</span></span>
4. <span data-ttu-id="6de9e-116">Skopiuj ten adres URL obiektu blob.</span><span class="sxs-lookup"><span data-stu-id="6de9e-116">Copy this blob URL.</span></span>
   
   ![Rysowanie](media/marketplace-publishing-vm-image-creation-on-premise/img02.png)
5. <span data-ttu-id="6de9e-118">Teraz, Usuń hello wdrożyć maszyny Wirtualnej bez usuwania hello zapasowy dysków.</span><span class="sxs-lookup"><span data-stu-id="6de9e-118">Now, delete hello deployed VM without deleting hello backing disks.</span></span> <span data-ttu-id="6de9e-119">Można też zatrzymać hello maszyny Wirtualnej, zamiast usuwania.</span><span class="sxs-lookup"><span data-stu-id="6de9e-119">You can also stop hello VM instead of deleting it.</span></span> <span data-ttu-id="6de9e-120">Nie pobieraj systemu operacyjnego hello wirtualnego dysku twardego, gdy hello maszyna wirtualna jest uruchomiona.</span><span class="sxs-lookup"><span data-stu-id="6de9e-120">Do not download hello operating system VHD when hello VM is running.</span></span>
   
   ![Rysowanie](media/marketplace-publishing-vm-image-creation-on-premise/img03.png)

### <a name="download-a-vhd"></a><span data-ttu-id="6de9e-122">Pobieranie wirtualnego dysku twardego</span><span class="sxs-lookup"><span data-stu-id="6de9e-122">Download a VHD</span></span>
<span data-ttu-id="6de9e-123">Po określeniu adresu URL obiektu blob hello hello wirtualnego dysku twardego można pobrać przy użyciu hello [portalu Azure](http://manage.windowsazure.com/) lub programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="6de9e-123">After you know hello blob URL, you can download hello VHD by using hello [Azure portal](http://manage.windowsazure.com/) or PowerShell.</span></span>  

> [!NOTE]
> <span data-ttu-id="6de9e-124">Na powitania czasu utworzenia tego przewodnika toodownload funkcji hello dysku VHD nie ma jeszcze w hello nowego portalu Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="6de9e-124">At hello time of this guide’s creation, hello functionality toodownload a VHD is not yet present in hello new Microsoft Azure portal.</span></span>  
> 
> 

<span data-ttu-id="6de9e-125">**Pobierz system operacyjny hello wirtualnego dysku twardego za pomocą bieżącego hello [portalu Azure](http://manage.windowsazure.com/)**</span><span class="sxs-lookup"><span data-stu-id="6de9e-125">**Download hello operating system VHD via hello current [Azure portal](http://manage.windowsazure.com/)**</span></span>

1. <span data-ttu-id="6de9e-126">Jeśli nie zostało to jeszcze zrobione, zaloguj się w toohello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="6de9e-126">Sign in toohello Azure portal if you have not done so already.</span></span>
2. <span data-ttu-id="6de9e-127">Kliknij przycisk hello **magazynu** kartę.</span><span class="sxs-lookup"><span data-stu-id="6de9e-127">Click hello **Storage** tab.</span></span>
3. <span data-ttu-id="6de9e-128">Wybierz konto magazynu hello, w których hello wirtualnego dysku twardego są przechowywane.</span><span class="sxs-lookup"><span data-stu-id="6de9e-128">Select hello storage account within which hello VHD is stored.</span></span>
   
   ![Rysowanie](media/marketplace-publishing-vm-image-creation-on-premise/img04.png)
4. <span data-ttu-id="6de9e-130">Spowoduje to wyświetlenie właściwości konta magazynu.</span><span class="sxs-lookup"><span data-stu-id="6de9e-130">This displays storage account properties.</span></span> <span data-ttu-id="6de9e-131">Wybierz hello **kontenery** kartę.</span><span class="sxs-lookup"><span data-stu-id="6de9e-131">Select hello **Containers** tab.</span></span>
   
   ![Rysowanie](media/marketplace-publishing-vm-image-creation-on-premise/img05.png)
5. <span data-ttu-id="6de9e-133">Wybierz kontener hello, w których hello wirtualnego dysku twardego są przechowywane.</span><span class="sxs-lookup"><span data-stu-id="6de9e-133">Select hello container in which hello VHD is stored.</span></span> <span data-ttu-id="6de9e-134">Domyślnie podczas tworzenia z portalu hello hello wirtualnego dysku twardego przechowywanego w kontenera VHD.</span><span class="sxs-lookup"><span data-stu-id="6de9e-134">By default, when created from hello portal, hello VHD is stored in a vhds container.</span></span>
   
   ![Rysowanie](media/marketplace-publishing-vm-image-creation-on-premise/img06.png)
6. <span data-ttu-id="6de9e-136">Wybierz hello poprawny system operacyjny dysku VHD, porównując hello toohello adres URL, jeden zapisany.</span><span class="sxs-lookup"><span data-stu-id="6de9e-136">Select hello correct operating system VHD by comparing hello URL toohello one you saved.</span></span>
7. <span data-ttu-id="6de9e-137">Kliknij pozycję **Pobierz**.</span><span class="sxs-lookup"><span data-stu-id="6de9e-137">Click **Download**.</span></span>
   
   ![Rysowanie](media/marketplace-publishing-vm-image-creation-on-premise/img07.png)

### <a name="download-a-vhd-by-using-powershell"></a><span data-ttu-id="6de9e-139">Pobierz dysku VHD za pomocą programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="6de9e-139">Download a VHD by using PowerShell</span></span>
<span data-ttu-id="6de9e-140">Ponadto toousing hello portalu Azure, możesz użyć hello [Save-AzureVhd](http://msdn.microsoft.com/library/dn495297.aspx) wirtualnego dysku twardego systemu operacyjnego hello toodownload polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="6de9e-140">In addition toousing hello Azure portal, you can use hello [Save-AzureVhd](http://msdn.microsoft.com/library/dn495297.aspx) cmdlet toodownload hello operating system VHD.</span></span>

        Save-AzureVhd –Source <storageURIOfVhd> `
        -LocalFilePath <diskLocationOnWorkstation> `
        -StorageKey <keyForStorageAccount>
<span data-ttu-id="6de9e-141">Na przykład Zapisz-AzureVhd-źródła "https://baseimagevm.blob.core.windows.net/vhds/BaseImageVM-6820cq00-BaseImageVM-os-1411003770191.vhd" - LocalFilePath "C:\Users\Administrator\Desktop\baseimagevm.vhd" - atrybutu StorageKey<String></span><span class="sxs-lookup"><span data-stu-id="6de9e-141">For example, Save-AzureVhd -Source “https://baseimagevm.blob.core.windows.net/vhds/BaseImageVM-6820cq00-BaseImageVM-os-1411003770191.vhd” -LocalFilePath “C:\Users\Administrator\Desktop\baseimagevm.vhd” -StorageKey <String></span></span>

> [!NOTE]
> <span data-ttu-id="6de9e-142">**Zapisz-AzureVhd** ma również **NumberOfThreads** opcji, które mogą być używane do pobrania hello tooincrease równoległości toomake hello najlepsze wykorzystanie przepustowości.</span><span class="sxs-lookup"><span data-stu-id="6de9e-142">**Save-AzureVhd** also has a **NumberOfThreads** option that can be used tooincrease parallelism toomake hello best use of available bandwidth for hello download.</span></span>
> 
> 

## <a name="upload-vhds-tooan-azure-storage-account"></a><span data-ttu-id="6de9e-143">Przekaż wirtualne dyski twarde tooan konta magazynu Azure</span><span class="sxs-lookup"><span data-stu-id="6de9e-143">Upload VHDs tooan Azure storage account</span></span>
<span data-ttu-id="6de9e-144">Przygotowane wirtualne dyski twarde lokalnej, należy najpierw tooupload je do magazynu konta w usłudze Azure.</span><span class="sxs-lookup"><span data-stu-id="6de9e-144">If you prepared your VHDs on-premises, you need tooupload them into a storage account in Azure.</span></span> <span data-ttu-id="6de9e-145">Ten krok ma miejsce po tworzenie dysk VHD lokalnie, ale przed uzyskaniem certyfikacji dla obrazu maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="6de9e-145">This step takes place after creating your VHD on-premises but before obtaining certification for your VM image.</span></span>

### <a name="create-a-storage-account-and-container"></a><span data-ttu-id="6de9e-146">Utwórz konto magazynu i kontener</span><span class="sxs-lookup"><span data-stu-id="6de9e-146">Create a storage account and container</span></span>
<span data-ttu-id="6de9e-147">Zaleca się, że wirtualne dyski twarde można przekazać do konta magazynu w regionie hello Stanów Zjednoczonych.</span><span class="sxs-lookup"><span data-stu-id="6de9e-147">We recommend that VHDs be uploaded into a storage account in a region in hello United States.</span></span> <span data-ttu-id="6de9e-148">Wszystkie wirtualne dyski twarde dla jednej jednostki SKU powinna zostać umieszczona w jeden kontener w ramach konta pojedynczy magazyn.</span><span class="sxs-lookup"><span data-stu-id="6de9e-148">All VHDs for a single SKU should be placed in a single container within a single storage account.</span></span>

<span data-ttu-id="6de9e-149">toocreate konto magazynu, można użyć hello [portalu Microsoft Azure](https://portal.azure.com/), programu PowerShell lub narzędzia wiersza polecenia hello systemu Linux.</span><span class="sxs-lookup"><span data-stu-id="6de9e-149">toocreate a storage account, you can use hello [Microsoft Azure portal](https://portal.azure.com/), PowerShell, or hello Linux command-line tool.</span></span>  

<span data-ttu-id="6de9e-150">**Utwórz konto magazynu z portalu Microsoft Azure hello**</span><span class="sxs-lookup"><span data-stu-id="6de9e-150">**Create a storage account from hello Microsoft Azure portal**</span></span>

1. <span data-ttu-id="6de9e-151">Kliknij przycisk **Nowy**.</span><span class="sxs-lookup"><span data-stu-id="6de9e-151">Click **New**.</span></span>
2. <span data-ttu-id="6de9e-152">Wybierz **magazynu**.</span><span class="sxs-lookup"><span data-stu-id="6de9e-152">Select **Storage**.</span></span>
3. <span data-ttu-id="6de9e-153">Wprowadź nazwę konta magazynu hello, a następnie wybierz lokalizację.</span><span class="sxs-lookup"><span data-stu-id="6de9e-153">Fill in hello storage account name, and then select a location.</span></span>
   
   ![Rysowanie](media/marketplace-publishing-vm-image-creation-on-premise/img08.png)
4. <span data-ttu-id="6de9e-155">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="6de9e-155">Click **Create**.</span></span>
5. <span data-ttu-id="6de9e-156">Witaj bloku hello utworzono konto magazynu powinien być otwarty.</span><span class="sxs-lookup"><span data-stu-id="6de9e-156">hello blade for hello created storage account should be open.</span></span> <span data-ttu-id="6de9e-157">Jeśli nie, wybierz **Przeglądaj** > **kont magazynu**.</span><span class="sxs-lookup"><span data-stu-id="6de9e-157">If not, select **Browse** > **Storage Accounts**.</span></span> <span data-ttu-id="6de9e-158">Na powitania magazynu konto bloku, wybierz utworzone konto magazynu hello.</span><span class="sxs-lookup"><span data-stu-id="6de9e-158">On hello Storage account blade, select hello storage account created.</span></span>
6. <span data-ttu-id="6de9e-159">Wybierz **kontenery**.</span><span class="sxs-lookup"><span data-stu-id="6de9e-159">Select **Containers**.</span></span>
   
   ![Rysowanie](media/marketplace-publishing-vm-image-creation-on-premise/img09.png) 
7. <span data-ttu-id="6de9e-161">W bloku kontenery hello, wybierz **Dodaj**, a następnie wprowadź uprawnień kontenera kontenera, jak nazwa i hello.</span><span class="sxs-lookup"><span data-stu-id="6de9e-161">On hello Containers blade, select **Add**, and then enter a container name and hello container permissions.</span></span> <span data-ttu-id="6de9e-162">Wybierz **prywatnej** uprawnienia do kontenera.</span><span class="sxs-lookup"><span data-stu-id="6de9e-162">Select **Private** for container permissions.</span></span>

> [!TIP]
> <span data-ttu-id="6de9e-163">Firma Microsoft zaleca utworzenie jednego kontenera na planowania toopublish jednostki SKU.</span><span class="sxs-lookup"><span data-stu-id="6de9e-163">We recommend that you create one container per SKU that you are planning toopublish.</span></span>
> 
> 

  ![Rysowanie](media/marketplace-publishing-vm-image-creation-on-premise/img10.png)

### <a name="create-a-storage-account-by-using-powershell"></a><span data-ttu-id="6de9e-165">Utwórz konto magazynu przy użyciu programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="6de9e-165">Create a storage account by using PowerShell</span></span>
<span data-ttu-id="6de9e-166">Przy użyciu programu PowerShell, Utwórz konto magazynu przy użyciu hello [AzureStorageAccount nowy](http://msdn.microsoft.com/library/dn495115.aspx) polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="6de9e-166">Using PowerShell, create a storage account by using hello [New-AzureStorageAccount](http://msdn.microsoft.com/library/dn495115.aspx) cmdlet.</span></span>

        New-AzureStorageAccount -StorageAccountName “mystorageaccount” -Location “West US”

<span data-ttu-id="6de9e-167">Następnie można utworzyć kontener w ramach tego konta magazynu przy użyciu hello [NewAzureStorageContainer](http://msdn.microsoft.com/library/dn495291.aspx) polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="6de9e-167">Then you can create a container within that storage account by using hello [NewAzureStorageContainer](http://msdn.microsoft.com/library/dn495291.aspx) cmdlet.</span></span>

        New-AzureStorageContainer -Name “containername” -Permission “Off”

> [!NOTE]
> <span data-ttu-id="6de9e-168">Te polecenia przyjęto założenie, że ten kontekst hello bieżącego konta magazynu został już ustawiony w programie PowerShell.</span><span class="sxs-lookup"><span data-stu-id="6de9e-168">Those commands assume that hello current storage account context has already been set in PowerShell.</span></span>   <span data-ttu-id="6de9e-169">Odwołuje się zbyt[Konfigurowanie programu Azure PowerShell](marketplace-publishing-powershell-setup.md) uzyskać więcej informacji dotyczących instalacji programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="6de9e-169">Refer too[Setting up Azure PowerShell](marketplace-publishing-powershell-setup.md) for more details on PowerShell setup.</span></span>  
> 
> ### <a name="create-a-storage-account-by-using-hello-command-line-tool-for-mac-and-linux"></a><span data-ttu-id="6de9e-170">Utwórz konto magazynu przy użyciu narzędzia wiersza polecenia hello for Mac i Linux</span><span class="sxs-lookup"><span data-stu-id="6de9e-170">Create a storage account by using hello command-line tool for Mac and Linux</span></span>
> <span data-ttu-id="6de9e-171">Z [narzędzia wiersza polecenia systemu Linux](../virtual-machines/linux/cli-manage.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json), Utwórz konto magazynu w następujący sposób.</span><span class="sxs-lookup"><span data-stu-id="6de9e-171">From [Linux command-line tool](../virtual-machines/linux/cli-manage.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json), create a storage account as follows.</span></span>
> 
> 

        azure storage account create mystorageaccount --location "West US"

<span data-ttu-id="6de9e-172">Utwórz kontener w następujący sposób.</span><span class="sxs-lookup"><span data-stu-id="6de9e-172">Create a container as follows.</span></span>

        azure storage container create containername --account-name mystorageaccount --accountkey <accountKey>

## <a name="upload-a-vhd"></a><span data-ttu-id="6de9e-173">Przekazywanie wirtualnego dysku twardego</span><span class="sxs-lookup"><span data-stu-id="6de9e-173">Upload a VHD</span></span>
<span data-ttu-id="6de9e-174">Po utworzeniu hello konto magazynu i kontener, możesz przekazać go przygotować dyski VHD.</span><span class="sxs-lookup"><span data-stu-id="6de9e-174">After hello storage account and container are created, you can upload your prepared VHDs.</span></span> <span data-ttu-id="6de9e-175">Można użyć programu PowerShell, narzędzia wiersza polecenia systemu Linux hello lub innych narzędzi do zarządzania usługi Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="6de9e-175">You can use PowerShell, hello Linux command-line tool, or other Azure Storage management tools.</span></span>

### <a name="upload-a-vhd-via-powershell"></a><span data-ttu-id="6de9e-176">Przekazywanie wirtualnego dysku twardego za pomocą programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="6de9e-176">Upload a VHD via PowerShell</span></span>
<span data-ttu-id="6de9e-177">Użyj hello [Add-AzureVhd](http://msdn.microsoft.com/library/dn495173.aspx) polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="6de9e-177">Use hello [Add-AzureVhd](http://msdn.microsoft.com/library/dn495173.aspx) cmdlet.</span></span>

        Add-AzureVhd –Destination “http://mystorageaccount.blob.core.windows.net/containername/vmsku.vhd” -LocalFilePath “C:\Users\Administrator\Desktop\vmsku.vhd”

### <a name="upload-a-vhd-by-using-hello-command-line-tool-for-mac-and-linux"></a><span data-ttu-id="6de9e-178">Przekazywanie wirtualnego dysku twardego za pomocą narzędzia wiersza polecenia hello for Mac i Linux</span><span class="sxs-lookup"><span data-stu-id="6de9e-178">Upload a VHD by using hello command-line tool for Mac and Linux</span></span>
<span data-ttu-id="6de9e-179">Z hello [narzędzia wiersza polecenia systemu Linux](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2), poniższych hello: Tworzenie obrazu maszyny wirtualnej azure <image name> — lokalizacji <Location of hello data center> — system operacyjny Linux<LocationOfLocalVHD></span><span class="sxs-lookup"><span data-stu-id="6de9e-179">With hello [Linux command-line tool](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2), use hello following: azure vm image create <image name> --location <Location of hello data center> --OS Linux <LocationOfLocalVHD></span></span>

## <a name="see-also"></a><span data-ttu-id="6de9e-180">Zobacz też</span><span class="sxs-lookup"><span data-stu-id="6de9e-180">See also</span></span>
* [<span data-ttu-id="6de9e-181">Tworzenie obrazu maszyny wirtualnej dla hello Marketplace</span><span class="sxs-lookup"><span data-stu-id="6de9e-181">Creating a virtual machine image for hello Marketplace</span></span>](marketplace-publishing-vm-image-creation.md)
* [<span data-ttu-id="6de9e-182">Konfigurowanie programu Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="6de9e-182">Setting up Azure PowerShell</span></span>](marketplace-publishing-powershell-setup.md)

