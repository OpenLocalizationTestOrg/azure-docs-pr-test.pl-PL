---
title: "aaaCreate dysków zarządzanych z dysku VHD na platformie Azure | Dokumentacja firmy Microsoft"
description: "Tworzenie dysku zarządzanego z dysku VHD, które jest obecnie kontem magazynu platformy Azure przy użyciu modelu wdrażania usługi Resource Manager hello."
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
ms.date: 02/05/2017
ms.author: cynthn
ms.openlocfilehash: 77adaac5419186ff85039fe2c4752f021aa5e448
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-managed-disks-from-unmanaged-disks-in-a-storage-account"></a><span data-ttu-id="18121-103">Tworzenie dysków zarządzanych z niezarządzanego dysków na koncie magazynu</span><span class="sxs-lookup"><span data-stu-id="18121-103">Create managed disks from unmanaged disks in a storage account</span></span>

<span data-ttu-id="18121-104">Dysk zarządzany mogą być tworzone z istniejącego dysku danych lub dysk systemu operacyjnego, które jest obecnie konta magazynu platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="18121-104">A managed disk can be created from an existing data disk or an OS disk that is currently in an Azure storage account.</span></span> <span data-ttu-id="18121-105">Można również utworzyć pusty dysk, który może służyć jako nowego dysku danych maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="18121-105">You can also create an empty disk that can be used as a new data disk for a VM.</span></span> 

## <a name="before-you-begin"></a><span data-ttu-id="18121-106">Przed rozpoczęciem</span><span class="sxs-lookup"><span data-stu-id="18121-106">Before you begin</span></span>
<span data-ttu-id="18121-107">Jeśli używasz programu PowerShell, upewnij się, że masz najnowszą wersję hello modułu AzureRM.Compute PowerShell hello.</span><span class="sxs-lookup"><span data-stu-id="18121-107">If you use PowerShell, make sure that you have hello latest version of hello AzureRM.Compute PowerShell module.</span></span> <span data-ttu-id="18121-108">Uruchom hello następujących tooinstall polecenia.</span><span class="sxs-lookup"><span data-stu-id="18121-108">Run hello following command tooinstall it.</span></span>

```powershell
Install-Module AzureRM.Compute -RequiredVersion 2.6.0
```
<span data-ttu-id="18121-109">Aby uzyskać więcej informacji, zobacz [przechowywanie wersji programu Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="18121-109">For more information, see [Azure PowerShell Versioning](/powershell/azure/overview).</span></span>


## <a name="create-a-managed-disk-from-a-vhd-in-an-azure-storage-account"></a><span data-ttu-id="18121-110">Tworzenie dysku zarządzanego z dysku VHD w koncie magazynu platformy Azure</span><span class="sxs-lookup"><span data-stu-id="18121-110">Create a managed disk from a VHD in an Azure storage account</span></span>

<span data-ttu-id="18121-111">W przykładzie hello możemy utworzyć dysk z wirtualnego dysku twardego dysków zarządzanych i przypisz do niego parametru toohello **dysk 1 $** toouse później.</span><span class="sxs-lookup"><span data-stu-id="18121-111">In hello example we create a disk from a VHD as managed disk and assign it toohello parameter **$disk1** toouse later.</span></span> 

<span data-ttu-id="18121-112">Witaj dysków zarządzanych zostaną utworzone w hello **zachodnie-US** lokalizacji, w grupie zasobów o nazwie **myResourceGroup**.</span><span class="sxs-lookup"><span data-stu-id="18121-112">hello managed disk will be created in hello **West-US** location, in a resource group named **myResourceGroup**.</span></span> <span data-ttu-id="18121-113">Witaj dysku będzie miała nazwę **myDisk** i zostanie utworzony z pliku wirtualnego dysku twardego o nazwie **myDisk.vhd** możemy wcześniej przekazany tooa konto magazynu o nazwie **mojekontomagazynu**.</span><span class="sxs-lookup"><span data-stu-id="18121-113">hello disk will be named **myDisk** and it will be created from a VHD file named **myDisk.vhd** we previously uploaded tooa storage account named **mystorageaccount**.</span></span> <span data-ttu-id="18121-114">zostanie utworzona Hello dysków zarządzanych w warstwie premium magazyn lokalnie nadmiarowy (LRS).</span><span class="sxs-lookup"><span data-stu-id="18121-114">hello managed disk will be created in premium locally-redundant storage (LRS).</span></span> <span data-ttu-id="18121-115">StandardLRS i PremiumLRS są tylko hello **- AccountType** opcje dostępne dla zarządzanych dysków.</span><span class="sxs-lookup"><span data-stu-id="18121-115">StandardLRS and PremiumLRS are hello only **-AccountType** options available for managed disks.</span></span> 

1.  <span data-ttu-id="18121-116">Ustaw niektórych parametrów</span><span class="sxs-lookup"><span data-stu-id="18121-116">Set some parameters</span></span>

    ```powershell
    $rgName = "myResourceGroup"
    $location = "West Central US"
    $diskName = "myDisk"
    $vhdUri = "https://mystorageaccount.blob.core.windows.net/vhds/myDisk.vhd"
    ```

2. <span data-ttu-id="18121-117">Utwórz dysk danych hello.</span><span class="sxs-lookup"><span data-stu-id="18121-117">Create hello data disk.</span></span> 
    ```powershell
    $disk1 = New-AzureRmDisk -DiskName $diskName -Disk (New-AzureRmDiskConfig -AccountType PremiumLRS -Location $location -CreateOption Import -SourceUri $vhdUri) -ResourceGroupName $rgName
    ```
    
    

## <a name="create-an-empty-data-disk-as-a-managed-disk"></a><span data-ttu-id="18121-118">Utwórz dysk danych puste jako dysków zarządzanych</span><span class="sxs-lookup"><span data-stu-id="18121-118">Create an empty data disk as a managed disk</span></span>

<span data-ttu-id="18121-119">W przykładzie hello możemy utworzyć dysk danych puste jako dysków zarządzanych w i przypisz do niego parametru toohello **$dataDisk2** toouse później.</span><span class="sxs-lookup"><span data-stu-id="18121-119">In hello example we create an empty data disk as managed disk and assign it toohello parameter **$dataDisk2** toouse later.</span></span> <span data-ttu-id="18121-120">Dysku danych puste, należy zainicjować toobe logowanie toohello maszyny Wirtualnej i przy użyciu diskmgmt.msc lub [zdalnie za pomocą usługi WinRM i skrypt](attach-disk-ps.md#initialize-the-disk), po dołączonych tooa uruchamiania maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="18121-120">An empty data disk will need toobe initialized logging in toohello VM and using diskmgmt.msc or [remotely using WinRM and a script](attach-disk-ps.md#initialize-the-disk), once it is attached tooa running VM.</span></span>

<span data-ttu-id="18121-121">Hello danych pusty dysk zostanie utworzony w hello **zachodnie centralnej nam** lokalizacji, w grupie zasobów o nazwie **myResourceGroup**.</span><span class="sxs-lookup"><span data-stu-id="18121-121">hello empty data disk will be created in hello **West Central US** location, in a resource group named **myResourceGroup**.</span></span> <span data-ttu-id="18121-122">Witaj dysku będzie miała nazwę **myEmptyDataDisk**.</span><span class="sxs-lookup"><span data-stu-id="18121-122">hello disk will be named **myEmptyDataDisk**.</span></span> <span data-ttu-id="18121-123">pusty dysk Hello zostaną utworzone w warstwie premium magazyn lokalnie nadmiarowy (LRS).</span><span class="sxs-lookup"><span data-stu-id="18121-123">hello empty disk will be created in premium locally-redundant storage (LRS).</span></span> <span data-ttu-id="18121-124">StandardLRS i PremiumLRS są tylko hello **- AccountType** opcje dostępne dla zarządzanych dysków.</span><span class="sxs-lookup"><span data-stu-id="18121-124">StandardLRS and PremiumLRS are hello only **-AccountType** options available for managed disks.</span></span>

<span data-ttu-id="18121-125">rozmiar dysku Hello w tym przykładzie jest 128GB, ale należy wybrać rozmiar, który spełnia potrzeby hello wszystkie aplikacje uruchomione na maszynie Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="18121-125">hello disk size in this example is 128GB, but you should choose a size that meets hello needs of any applications running on your VM.</span></span>

1.  <span data-ttu-id="18121-126">Ustaw niektórych parametrów</span><span class="sxs-lookup"><span data-stu-id="18121-126">Set some parameters</span></span>

    ```powershell
    $rgName = "myResourceGroup"
    $location = "West Central US"
    $dataDiskName = "myEmptyDataDisk"
    ```

2. <span data-ttu-id="18121-127">Utwórz dysk danych hello.</span><span class="sxs-lookup"><span data-stu-id="18121-127">Create hello data disk.</span></span>
    ```powershell
    $dataDisk2 = New-AzureRmDisk -DiskName $dataDiskName -Disk (New-AzureRmDiskConfig -AccountType PremiumLRS -Location $location -CreateOption Empty -DiskSizeGB 128) -ResourceGroupName $rgName
    ```
    
## <a name="next-steps"></a><span data-ttu-id="18121-128">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="18121-128">Next Steps</span></span>   
- <span data-ttu-id="18121-129">Jeśli masz już Maszynę wirtualną, możesz [dołączenie dysku danych](attach-disk-portal.md).</span><span class="sxs-lookup"><span data-stu-id="18121-129">If you already have a VM, you can [attach a data disk](attach-disk-portal.md).</span></span>
