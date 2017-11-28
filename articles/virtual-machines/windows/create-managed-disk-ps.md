---
title: "Tworzenie dysku zarządzanego z dysku VHD na platformie Azure | Dokumentacja firmy Microsoft"
description: "Tworzenie dysku zarządzanego z dysku VHD, które jest obecnie kontem magazynu platformy Azure przy użyciu modelu wdrażania Menedżera zasobów."
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
ms.openlocfilehash: c03ebf73f1090b595149daf2eb3e274b05822f4f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="create-managed-disks-from-unmanaged-disks-in-a-storage-account"></a><span data-ttu-id="57259-103">Tworzenie dysków zarządzanych z niezarządzanego dysków na koncie magazynu</span><span class="sxs-lookup"><span data-stu-id="57259-103">Create managed disks from unmanaged disks in a storage account</span></span>

<span data-ttu-id="57259-104">Dysk zarządzany mogą być tworzone z istniejącego dysku danych lub dysk systemu operacyjnego, które jest obecnie konta magazynu platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="57259-104">A managed disk can be created from an existing data disk or an OS disk that is currently in an Azure storage account.</span></span> <span data-ttu-id="57259-105">Można również utworzyć pusty dysk, który może służyć jako nowego dysku danych maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="57259-105">You can also create an empty disk that can be used as a new data disk for a VM.</span></span> 

## <a name="before-you-begin"></a><span data-ttu-id="57259-106">Przed rozpoczęciem</span><span class="sxs-lookup"><span data-stu-id="57259-106">Before you begin</span></span>
<span data-ttu-id="57259-107">Jeśli używasz programu PowerShell, upewnij się, że masz najnowszą wersję modułu programu AzureRM.Compute PowerShell.</span><span class="sxs-lookup"><span data-stu-id="57259-107">If you use PowerShell, make sure that you have the latest version of the AzureRM.Compute PowerShell module.</span></span> <span data-ttu-id="57259-108">Uruchom następujące polecenie, aby go zainstalować.</span><span class="sxs-lookup"><span data-stu-id="57259-108">Run the following command to install it.</span></span>

```powershell
Install-Module AzureRM.Compute -RequiredVersion 2.6.0
```
<span data-ttu-id="57259-109">Aby uzyskać więcej informacji, zobacz [przechowywanie wersji programu Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="57259-109">For more information, see [Azure PowerShell Versioning](/powershell/azure/overview).</span></span>


## <a name="create-a-managed-disk-from-a-vhd-in-an-azure-storage-account"></a><span data-ttu-id="57259-110">Tworzenie dysku zarządzanego z dysku VHD w koncie magazynu platformy Azure</span><span class="sxs-lookup"><span data-stu-id="57259-110">Create a managed disk from a VHD in an Azure storage account</span></span>

<span data-ttu-id="57259-111">W tym przykładzie, możemy utworzyć dysk z wirtualnego dysku twardego zarządzanego dysku i przypisz je do parametru **$ dysk 1** do użycia w przyszłości.</span><span class="sxs-lookup"><span data-stu-id="57259-111">In the example we create a disk from a VHD as managed disk and assign it to the parameter **$disk1** to use later.</span></span> 

<span data-ttu-id="57259-112">Zostaną utworzone dysków zarządzanych w **zachodnie-US** lokalizacji, w grupie zasobów o nazwie **myResourceGroup**.</span><span class="sxs-lookup"><span data-stu-id="57259-112">The managed disk will be created in the **West-US** location, in a resource group named **myResourceGroup**.</span></span> <span data-ttu-id="57259-113">Dysk będzie miała nazwę **myDisk** i zostanie utworzony z pliku wirtualnego dysku twardego o nazwie **myDisk.vhd** możemy wcześniej przekazany do konta magazynu o nazwie **mojekontomagazynu**.</span><span class="sxs-lookup"><span data-stu-id="57259-113">The disk will be named **myDisk** and it will be created from a VHD file named **myDisk.vhd** we previously uploaded to a storage account named **mystorageaccount**.</span></span> <span data-ttu-id="57259-114">Zostanie utworzona dysków zarządzanych w warstwie premium magazyn lokalnie nadmiarowy (LRS).</span><span class="sxs-lookup"><span data-stu-id="57259-114">The managed disk will be created in premium locally-redundant storage (LRS).</span></span> <span data-ttu-id="57259-115">StandardLRS i PremiumLRS są tylko **- AccountType** opcje dostępne dla zarządzanych dysków.</span><span class="sxs-lookup"><span data-stu-id="57259-115">StandardLRS and PremiumLRS are the only **-AccountType** options available for managed disks.</span></span> 

1.  <span data-ttu-id="57259-116">Ustaw niektórych parametrów</span><span class="sxs-lookup"><span data-stu-id="57259-116">Set some parameters</span></span>

    ```powershell
    $rgName = "myResourceGroup"
    $location = "West Central US"
    $diskName = "myDisk"
    $vhdUri = "https://mystorageaccount.blob.core.windows.net/vhds/myDisk.vhd"
    ```

2. <span data-ttu-id="57259-117">Utwórz dysk z danymi.</span><span class="sxs-lookup"><span data-stu-id="57259-117">Create the data disk.</span></span> 
    ```powershell
    $disk1 = New-AzureRmDisk -DiskName $diskName -Disk (New-AzureRmDiskConfig -AccountType PremiumLRS -Location $location -CreateOption Import -SourceUri $vhdUri) -ResourceGroupName $rgName
    ```
    
    

## <a name="create-an-empty-data-disk-as-a-managed-disk"></a><span data-ttu-id="57259-118">Utwórz dysk danych puste jako dysków zarządzanych</span><span class="sxs-lookup"><span data-stu-id="57259-118">Create an empty data disk as a managed disk</span></span>

<span data-ttu-id="57259-119">W tym przykładzie firma Microsoft Utwórz dysk danych puste jako dysków zarządzanych i przypisz je do parametru **$dataDisk2** do użycia w przyszłości.</span><span class="sxs-lookup"><span data-stu-id="57259-119">In the example we create an empty data disk as managed disk and assign it to the parameter **$dataDisk2** to use later.</span></span> <span data-ttu-id="57259-120">Musi być zainicjowana logowanie do maszyny Wirtualnej i przy użyciu diskmgmt.msc dysku danych puste lub [zdalnie za pomocą usługi WinRM i skrypt](attach-disk-ps.md#initialize-the-disk), gdy jest on dołączony do uruchomionej maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="57259-120">An empty data disk will need to be initialized logging in to the VM and using diskmgmt.msc or [remotely using WinRM and a script](attach-disk-ps.md#initialize-the-disk), once it is attached to a running VM.</span></span>

<span data-ttu-id="57259-121">Dysk z danymi puste, zostanie utworzony w **zachodnie centralnej nam** lokalizacji, w grupie zasobów o nazwie **myResourceGroup**.</span><span class="sxs-lookup"><span data-stu-id="57259-121">The empty data disk will be created in the **West Central US** location, in a resource group named **myResourceGroup**.</span></span> <span data-ttu-id="57259-122">Dysk będzie miała nazwę **myEmptyDataDisk**.</span><span class="sxs-lookup"><span data-stu-id="57259-122">The disk will be named **myEmptyDataDisk**.</span></span> <span data-ttu-id="57259-123">Pusty dysk zostanie utworzony w warstwie premium magazyn lokalnie nadmiarowy (LRS).</span><span class="sxs-lookup"><span data-stu-id="57259-123">The empty disk will be created in premium locally-redundant storage (LRS).</span></span> <span data-ttu-id="57259-124">StandardLRS i PremiumLRS są tylko **- AccountType** opcje dostępne dla zarządzanych dysków.</span><span class="sxs-lookup"><span data-stu-id="57259-124">StandardLRS and PremiumLRS are the only **-AccountType** options available for managed disks.</span></span>

<span data-ttu-id="57259-125">Rozmiar dysku w tym przykładzie jest 128GB, ale należy wybrać rozmiar, które zaspokoi potrzeby wszystkie aplikacje uruchomione na maszynie Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="57259-125">The disk size in this example is 128GB, but you should choose a size that meets the needs of any applications running on your VM.</span></span>

1.  <span data-ttu-id="57259-126">Ustaw niektórych parametrów</span><span class="sxs-lookup"><span data-stu-id="57259-126">Set some parameters</span></span>

    ```powershell
    $rgName = "myResourceGroup"
    $location = "West Central US"
    $dataDiskName = "myEmptyDataDisk"
    ```

2. <span data-ttu-id="57259-127">Utwórz dysk z danymi.</span><span class="sxs-lookup"><span data-stu-id="57259-127">Create the data disk.</span></span>
    ```powershell
    $dataDisk2 = New-AzureRmDisk -DiskName $dataDiskName -Disk (New-AzureRmDiskConfig -AccountType PremiumLRS -Location $location -CreateOption Empty -DiskSizeGB 128) -ResourceGroupName $rgName
    ```
    
## <a name="next-steps"></a><span data-ttu-id="57259-128">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="57259-128">Next Steps</span></span>   
- <span data-ttu-id="57259-129">Jeśli masz już Maszynę wirtualną, możesz [dołączenie dysku danych](attach-disk-portal.md).</span><span class="sxs-lookup"><span data-stu-id="57259-129">If you already have a VM, you can [attach a data disk](attach-disk-portal.md).</span></span>
