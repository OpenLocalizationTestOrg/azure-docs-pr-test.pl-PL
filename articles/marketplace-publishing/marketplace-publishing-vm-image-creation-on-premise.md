---
title: Tworzenie obrazu maszyny wirtualnej lokalnej do portalu Azure Marketplace | Dokumentacja firmy Microsoft
description: "Zrozumienie i wykonaj kroki, aby utworzyć lokalnej obrazu maszyny Wirtualnej i wdrażanie w portalu Azure Marketplace innym osobom do zakupu."
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
ms.openlocfilehash: 8f6b9a9293dc149586e6e5fd55028170ea825b07
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="develop-an-on-premises-virtual-machine-image-for-the-azure-marketplace"></a><span data-ttu-id="d369b-103">Tworzenie obrazu maszyny wirtualnej lokalnej dla portalu Azure Marketplace</span><span class="sxs-lookup"><span data-stu-id="d369b-103">Develop an on-premises virtual machine image for the Azure Marketplace</span></span>
<span data-ttu-id="d369b-104">Zdecydowanie zaleca się tworzenie Azure wirtualnych dysków twardych (VHD) bezpośrednio w chmurze przy użyciu protokołu Remote Desktop Protocol.</span><span class="sxs-lookup"><span data-stu-id="d369b-104">We strongly recommend that you develop Azure virtual hard disks (VHDs) directly in the cloud by using Remote Desktop Protocol.</span></span> <span data-ttu-id="d369b-105">Jeśli musisz, prawdopodobnie Pobierz wirtualnego dysku twardego i opracowanie go za pomocą infrastruktury lokalnej.</span><span class="sxs-lookup"><span data-stu-id="d369b-105">However, if you must, it is possible to download a VHD and develop it by using on-premises infrastructure.</span></span>  

<span data-ttu-id="d369b-106">Dla rozwoju lokalnych możesz pobrać systemu operacyjnego wirtualnego dysku twardego utworzonego maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="d369b-106">For on-premises development, you must download the operating system VHD of the created VM.</span></span> <span data-ttu-id="d369b-107">Te kroki nastąpiłoby w ramach kroku 3.3 powyżej.</span><span class="sxs-lookup"><span data-stu-id="d369b-107">These steps would take place as part of step 3.3, above.</span></span>  

## <a name="download-a-vhd-image"></a><span data-ttu-id="d369b-108">Pobranie obrazu wirtualnego dysku twardego</span><span class="sxs-lookup"><span data-stu-id="d369b-108">Download a VHD image</span></span>
### <a name="locate-a-blob-url"></a><span data-ttu-id="d369b-109">Znajdź adres URL obiektu blob</span><span class="sxs-lookup"><span data-stu-id="d369b-109">Locate a blob URL</span></span>
<span data-ttu-id="d369b-110">W celu pobrania dysku VHD, w pierwszej kolejności zlokalizować adresu URL obiektu blob dla dysku systemu operacyjnego.</span><span class="sxs-lookup"><span data-stu-id="d369b-110">In order to download the VHD, first locate the blob URL for the operating system disk.</span></span>

<span data-ttu-id="d369b-111">Znajdź adres URL obiektu blob w ramach nowego [portalu Microsoft Azure](https://portal.azure.com):</span><span class="sxs-lookup"><span data-stu-id="d369b-111">Locate the blob URL from the new [Microsoft Azure portal](https://portal.azure.com):</span></span>

1. <span data-ttu-id="d369b-112">Przejdź do **Przeglądaj** > **maszyn wirtualnych**, a następnie wybierz wdrożonej maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="d369b-112">Go to **Browse** > **VMs**, and then select the deployed VM.</span></span>
2. <span data-ttu-id="d369b-113">W obszarze **Konfiguruj**, wybierz pozycję **dysków** kafelka, która otwiera blok dysków.</span><span class="sxs-lookup"><span data-stu-id="d369b-113">Under **Configure**, select the **Disks** tile, which opens the Disks blade.</span></span>
   
   ![Rysowanie](media/marketplace-publishing-vm-image-creation-on-premise/img01.png)
3. <span data-ttu-id="d369b-115">Wybierz **dysk systemu operacyjnego**, który zostanie otwarty kolejny blok zawierający właściwości dysku, w tym lokalizacja wirtualnego dysku twardego.</span><span class="sxs-lookup"><span data-stu-id="d369b-115">Select the **OS Disk**, which opens another blade that displays disk properties, including the VHD location.</span></span>
4. <span data-ttu-id="d369b-116">Skopiuj ten adres URL obiektu blob.</span><span class="sxs-lookup"><span data-stu-id="d369b-116">Copy this blob URL.</span></span>
   
   ![Rysowanie](media/marketplace-publishing-vm-image-creation-on-premise/img02.png)
5. <span data-ttu-id="d369b-118">Teraz Usuń wdrożonej maszyny Wirtualnej bez usuwania dysków zapasowego.</span><span class="sxs-lookup"><span data-stu-id="d369b-118">Now, delete the deployed VM without deleting the backing disks.</span></span> <span data-ttu-id="d369b-119">Można również zatrzymać maszynę Wirtualną zamiast usuwania.</span><span class="sxs-lookup"><span data-stu-id="d369b-119">You can also stop the VM instead of deleting it.</span></span> <span data-ttu-id="d369b-120">Nie pobieraj wirtualnego dysku twardego systemu operacyjnego, gdy maszyna wirtualna jest uruchomiona.</span><span class="sxs-lookup"><span data-stu-id="d369b-120">Do not download the operating system VHD when the VM is running.</span></span>
   
   ![Rysowanie](media/marketplace-publishing-vm-image-creation-on-premise/img03.png)

### <a name="download-a-vhd"></a><span data-ttu-id="d369b-122">Pobieranie wirtualnego dysku twardego</span><span class="sxs-lookup"><span data-stu-id="d369b-122">Download a VHD</span></span>
<span data-ttu-id="d369b-123">Po określeniu adresu URL obiektu blob dysku VHD można pobrać za pomocą [portalu Azure](http://manage.windowsazure.com/) lub programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="d369b-123">After you know the blob URL, you can download the VHD by using the [Azure portal](http://manage.windowsazure.com/) or PowerShell.</span></span>  

> [!NOTE]
> <span data-ttu-id="d369b-124">Podczas tworzenia tego przewodnika funkcji do pobrania dysku VHD nie ma jeszcze w nowego portalu Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="d369b-124">At the time of this guide’s creation, the functionality to download a VHD is not yet present in the new Microsoft Azure portal.</span></span>  
> 
> 

<span data-ttu-id="d369b-125">**Pobierz system operacyjny dysku VHD za pomocą bieżącego [portalu Azure](http://manage.windowsazure.com/)**</span><span class="sxs-lookup"><span data-stu-id="d369b-125">**Download the operating system VHD via the current [Azure portal](http://manage.windowsazure.com/)**</span></span>

1. <span data-ttu-id="d369b-126">Zaloguj się do portalu Azure, jeśli nie zostało to jeszcze zrobione.</span><span class="sxs-lookup"><span data-stu-id="d369b-126">Sign in to the Azure portal if you have not done so already.</span></span>
2. <span data-ttu-id="d369b-127">Kliknij przycisk **magazynu** kartę.</span><span class="sxs-lookup"><span data-stu-id="d369b-127">Click the **Storage** tab.</span></span>
3. <span data-ttu-id="d369b-128">Wybierz konto magazynu, w którym znajduje się wirtualny dysk twardy.</span><span class="sxs-lookup"><span data-stu-id="d369b-128">Select the storage account within which the VHD is stored.</span></span>
   
   ![Rysowanie](media/marketplace-publishing-vm-image-creation-on-premise/img04.png)
4. <span data-ttu-id="d369b-130">Spowoduje to wyświetlenie właściwości konta magazynu.</span><span class="sxs-lookup"><span data-stu-id="d369b-130">This displays storage account properties.</span></span> <span data-ttu-id="d369b-131">Wybierz **kontenery** kartę.</span><span class="sxs-lookup"><span data-stu-id="d369b-131">Select the **Containers** tab.</span></span>
   
   ![Rysowanie](media/marketplace-publishing-vm-image-creation-on-premise/img05.png)
5. <span data-ttu-id="d369b-133">Wybierz kontener, w którym znajduje się wirtualny dysk twardy.</span><span class="sxs-lookup"><span data-stu-id="d369b-133">Select the container in which the VHD is stored.</span></span> <span data-ttu-id="d369b-134">Domyślnie jeśli utworzone w portalu wirtualny dysk twardy jest przechowywany w kontenerze wirtualne dyski twarde.</span><span class="sxs-lookup"><span data-stu-id="d369b-134">By default, when created from the portal, the VHD is stored in a vhds container.</span></span>
   
   ![Rysowanie](media/marketplace-publishing-vm-image-creation-on-premise/img06.png)
6. <span data-ttu-id="d369b-136">Wybierz poprawny system operacyjny dysku VHD, porównując adres URL do tego, który został zapisany.</span><span class="sxs-lookup"><span data-stu-id="d369b-136">Select the correct operating system VHD by comparing the URL to the one you saved.</span></span>
7. <span data-ttu-id="d369b-137">Kliknij pozycję **Pobierz**.</span><span class="sxs-lookup"><span data-stu-id="d369b-137">Click **Download**.</span></span>
   
   ![Rysowanie](media/marketplace-publishing-vm-image-creation-on-premise/img07.png)

### <a name="download-a-vhd-by-using-powershell"></a><span data-ttu-id="d369b-139">Pobierz dysku VHD za pomocą programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="d369b-139">Download a VHD by using PowerShell</span></span>
<span data-ttu-id="d369b-140">Oprócz przy użyciu portalu Azure, możesz użyć [Save-AzureVhd](http://msdn.microsoft.com/library/dn495297.aspx) polecenia cmdlet, aby pobierać system operacyjny dysku VHD.</span><span class="sxs-lookup"><span data-stu-id="d369b-140">In addition to using the Azure portal, you can use the [Save-AzureVhd](http://msdn.microsoft.com/library/dn495297.aspx) cmdlet to download the operating system VHD.</span></span>

        Save-AzureVhd –Source <storageURIOfVhd> `
        -LocalFilePath <diskLocationOnWorkstation> `
        -StorageKey <keyForStorageAccount>
<span data-ttu-id="d369b-141">Na przykład Zapisz-AzureVhd-źródła "https://baseimagevm.blob.core.windows.net/vhds/BaseImageVM-6820cq00-BaseImageVM-os-1411003770191.vhd" - LocalFilePath "C:\Users\Administrator\Desktop\baseimagevm.vhd" - atrybutu StorageKey<String></span><span class="sxs-lookup"><span data-stu-id="d369b-141">For example, Save-AzureVhd -Source “https://baseimagevm.blob.core.windows.net/vhds/BaseImageVM-6820cq00-BaseImageVM-os-1411003770191.vhd” -LocalFilePath “C:\Users\Administrator\Desktop\baseimagevm.vhd” -StorageKey <String></span></span>

> [!NOTE]
> <span data-ttu-id="d369b-142">**Zapisz-AzureVhd** ma również **NumberOfThreads** opcja, która może służyć do zwiększenia równoległości, aby jak najlepiej wykorzystać dostępnej przepustowości dla pobierania.</span><span class="sxs-lookup"><span data-stu-id="d369b-142">**Save-AzureVhd** also has a **NumberOfThreads** option that can be used to increase parallelism to make the best use of available bandwidth for the download.</span></span>
> 
> 

## <a name="upload-vhds-to-an-azure-storage-account"></a><span data-ttu-id="d369b-143">Przekaż wirtualne dyski twarde do konta magazynu platformy Azure</span><span class="sxs-lookup"><span data-stu-id="d369b-143">Upload VHDs to an Azure storage account</span></span>
<span data-ttu-id="d369b-144">Przygotowane wirtualne dyski twarde lokalnej, należy przekazać je do konta magazynu na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="d369b-144">If you prepared your VHDs on-premises, you need to upload them into a storage account in Azure.</span></span> <span data-ttu-id="d369b-145">Ten krok ma miejsce po tworzenie dysk VHD lokalnie, ale przed uzyskaniem certyfikacji dla obrazu maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="d369b-145">This step takes place after creating your VHD on-premises but before obtaining certification for your VM image.</span></span>

### <a name="create-a-storage-account-and-container"></a><span data-ttu-id="d369b-146">Utwórz konto magazynu i kontener</span><span class="sxs-lookup"><span data-stu-id="d369b-146">Create a storage account and container</span></span>
<span data-ttu-id="d369b-147">Zaleca się, że wirtualne dyski twarde można przekazać do konta magazynu w regionie w Stanach Zjednoczonych.</span><span class="sxs-lookup"><span data-stu-id="d369b-147">We recommend that VHDs be uploaded into a storage account in a region in the United States.</span></span> <span data-ttu-id="d369b-148">Wszystkie wirtualne dyski twarde dla jednej jednostki SKU powinna zostać umieszczona w jeden kontener w ramach konta pojedynczy magazyn.</span><span class="sxs-lookup"><span data-stu-id="d369b-148">All VHDs for a single SKU should be placed in a single container within a single storage account.</span></span>

<span data-ttu-id="d369b-149">Aby utworzyć konto magazynu, można użyć [portalu Microsoft Azure](https://portal.azure.com/), programu PowerShell lub systemu Linux narzędzia wiersza polecenia.</span><span class="sxs-lookup"><span data-stu-id="d369b-149">To create a storage account, you can use the [Microsoft Azure portal](https://portal.azure.com/), PowerShell, or the Linux command-line tool.</span></span>  

<span data-ttu-id="d369b-150">**Utwórz konto magazynu z portalu Microsoft Azure**</span><span class="sxs-lookup"><span data-stu-id="d369b-150">**Create a storage account from the Microsoft Azure portal**</span></span>

1. <span data-ttu-id="d369b-151">Kliknij przycisk **Nowy**.</span><span class="sxs-lookup"><span data-stu-id="d369b-151">Click **New**.</span></span>
2. <span data-ttu-id="d369b-152">Wybierz **magazynu**.</span><span class="sxs-lookup"><span data-stu-id="d369b-152">Select **Storage**.</span></span>
3. <span data-ttu-id="d369b-153">Wprowadź nazwę konta magazynu, a następnie wybierz lokalizację.</span><span class="sxs-lookup"><span data-stu-id="d369b-153">Fill in the storage account name, and then select a location.</span></span>
   
   ![Rysowanie](media/marketplace-publishing-vm-image-creation-on-premise/img08.png)
4. <span data-ttu-id="d369b-155">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="d369b-155">Click **Create**.</span></span>
5. <span data-ttu-id="d369b-156">Blok dla konta magazynu utworzone powinien być otwarty.</span><span class="sxs-lookup"><span data-stu-id="d369b-156">The blade for the created storage account should be open.</span></span> <span data-ttu-id="d369b-157">Jeśli nie, wybierz **Przeglądaj** > **kont magazynu**.</span><span class="sxs-lookup"><span data-stu-id="d369b-157">If not, select **Browse** > **Storage Accounts**.</span></span> <span data-ttu-id="d369b-158">W bloku konta magazynu wybierz utworzone konto magazynu.</span><span class="sxs-lookup"><span data-stu-id="d369b-158">On the Storage account blade, select the storage account created.</span></span>
6. <span data-ttu-id="d369b-159">Wybierz **kontenery**.</span><span class="sxs-lookup"><span data-stu-id="d369b-159">Select **Containers**.</span></span>
   
   ![Rysowanie](media/marketplace-publishing-vm-image-creation-on-premise/img09.png) 
7. <span data-ttu-id="d369b-161">W bloku kontenery wybierz **Dodaj**, a następnie wprowadź nazwę kontenera i uprawnień kontenera.</span><span class="sxs-lookup"><span data-stu-id="d369b-161">On the Containers blade, select **Add**, and then enter a container name and the container permissions.</span></span> <span data-ttu-id="d369b-162">Wybierz **prywatnej** uprawnienia do kontenera.</span><span class="sxs-lookup"><span data-stu-id="d369b-162">Select **Private** for container permissions.</span></span>

> [!TIP]
> <span data-ttu-id="d369b-163">Firma Microsoft zaleca utworzenie jednego kontenera na jednostka SKU, które planujesz opublikować.</span><span class="sxs-lookup"><span data-stu-id="d369b-163">We recommend that you create one container per SKU that you are planning to publish.</span></span>
> 
> 

  ![Rysowanie](media/marketplace-publishing-vm-image-creation-on-premise/img10.png)

### <a name="create-a-storage-account-by-using-powershell"></a><span data-ttu-id="d369b-165">Utwórz konto magazynu przy użyciu programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="d369b-165">Create a storage account by using PowerShell</span></span>
<span data-ttu-id="d369b-166">Przy użyciu programu PowerShell, Utwórz konto magazynu przy użyciu [AzureStorageAccount nowy](http://msdn.microsoft.com/library/dn495115.aspx) polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="d369b-166">Using PowerShell, create a storage account by using the [New-AzureStorageAccount](http://msdn.microsoft.com/library/dn495115.aspx) cmdlet.</span></span>

        New-AzureStorageAccount -StorageAccountName “mystorageaccount” -Location “West US”

<span data-ttu-id="d369b-167">Następnie można utworzyć kontener w ramach tego konta magazynu przy użyciu [NewAzureStorageContainer](http://msdn.microsoft.com/library/dn495291.aspx) polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="d369b-167">Then you can create a container within that storage account by using the [NewAzureStorageContainer](http://msdn.microsoft.com/library/dn495291.aspx) cmdlet.</span></span>

        New-AzureStorageContainer -Name “containername” -Permission “Off”

> [!NOTE]
> <span data-ttu-id="d369b-168">Tych poleceniach założono, że bieżący kontekst konta magazynu został już ustawiony w programie PowerShell.</span><span class="sxs-lookup"><span data-stu-id="d369b-168">Those commands assume that the current storage account context has already been set in PowerShell.</span></span>   <span data-ttu-id="d369b-169">Zapoznaj się [Konfigurowanie programu Azure PowerShell](marketplace-publishing-powershell-setup.md) uzyskać więcej informacji dotyczących instalacji programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="d369b-169">Refer to [Setting up Azure PowerShell](marketplace-publishing-powershell-setup.md) for more details on PowerShell setup.</span></span>  
> 
> ### <a name="create-a-storage-account-by-using-the-command-line-tool-for-mac-and-linux"></a><span data-ttu-id="d369b-170">Utwórz konto magazynu przy użyciu narzędzia wiersza polecenia dla komputerów Mac i Linux</span><span class="sxs-lookup"><span data-stu-id="d369b-170">Create a storage account by using the command-line tool for Mac and Linux</span></span>
> <span data-ttu-id="d369b-171">Z [narzędzia wiersza polecenia systemu Linux](../virtual-machines/linux/cli-manage.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json), Utwórz konto magazynu w następujący sposób.</span><span class="sxs-lookup"><span data-stu-id="d369b-171">From [Linux command-line tool](../virtual-machines/linux/cli-manage.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json), create a storage account as follows.</span></span>
> 
> 

        azure storage account create mystorageaccount --location "West US"

<span data-ttu-id="d369b-172">Utwórz kontener w następujący sposób.</span><span class="sxs-lookup"><span data-stu-id="d369b-172">Create a container as follows.</span></span>

        azure storage container create containername --account-name mystorageaccount --accountkey <accountKey>

## <a name="upload-a-vhd"></a><span data-ttu-id="d369b-173">Przekazywanie wirtualnego dysku twardego</span><span class="sxs-lookup"><span data-stu-id="d369b-173">Upload a VHD</span></span>
<span data-ttu-id="d369b-174">Po utworzeniu konta magazynu i kontener, możesz przekazać go przygotować dyski VHD.</span><span class="sxs-lookup"><span data-stu-id="d369b-174">After the storage account and container are created, you can upload your prepared VHDs.</span></span> <span data-ttu-id="d369b-175">Można użyć programu PowerShell, narzędzie wiersza polecenia systemu Linux lub innych narzędzi do zarządzania usługi Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="d369b-175">You can use PowerShell, the Linux command-line tool, or other Azure Storage management tools.</span></span>

### <a name="upload-a-vhd-via-powershell"></a><span data-ttu-id="d369b-176">Przekazywanie wirtualnego dysku twardego za pomocą programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="d369b-176">Upload a VHD via PowerShell</span></span>
<span data-ttu-id="d369b-177">Użyj [Add-AzureVhd](http://msdn.microsoft.com/library/dn495173.aspx) polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="d369b-177">Use the [Add-AzureVhd](http://msdn.microsoft.com/library/dn495173.aspx) cmdlet.</span></span>

        Add-AzureVhd –Destination “http://mystorageaccount.blob.core.windows.net/containername/vmsku.vhd” -LocalFilePath “C:\Users\Administrator\Desktop\vmsku.vhd”

### <a name="upload-a-vhd-by-using-the-command-line-tool-for-mac-and-linux"></a><span data-ttu-id="d369b-178">Przekazywanie wirtualnego dysku twardego za pomocą narzędzia wiersza polecenia dla komputerów Mac i Linux</span><span class="sxs-lookup"><span data-stu-id="d369b-178">Upload a VHD by using the command-line tool for Mac and Linux</span></span>
<span data-ttu-id="d369b-179">Z [narzędzia wiersza polecenia systemu Linux](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2), należy użyć następującego: Tworzenie obrazu maszyny wirtualnej azure <image name> — lokalizacji <Location of the data center> — system operacyjny Linux<LocationOfLocalVHD></span><span class="sxs-lookup"><span data-stu-id="d369b-179">With the [Linux command-line tool](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2), use the following: azure vm image create <image name> --location <Location of the data center> --OS Linux <LocationOfLocalVHD></span></span>

## <a name="see-also"></a><span data-ttu-id="d369b-180">Zobacz też</span><span class="sxs-lookup"><span data-stu-id="d369b-180">See also</span></span>
* [<span data-ttu-id="d369b-181">Tworzenie obrazu maszyny wirtualnej dla witryny Marketplace</span><span class="sxs-lookup"><span data-stu-id="d369b-181">Creating a virtual machine image for the Marketplace</span></span>](marketplace-publishing-vm-image-creation.md)
* [<span data-ttu-id="d369b-182">Konfigurowanie programu Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="d369b-182">Setting up Azure PowerShell</span></span>](marketplace-publishing-powershell-setup.md)

