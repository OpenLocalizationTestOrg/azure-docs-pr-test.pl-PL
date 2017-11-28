---
title: "Utwórz kopię dysku zarządzanego Azure dla kopii zapasowej | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak utworzyć kopię dysku zarządzanego Azure na potrzeby kopii lub rozwiązywania problemów z dysku."
documentationcenter: 
author: cwatson-cat
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 15eb778e-fc07-45ef-bdc8-9090193a6d20
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 2/9/2017
ms.author: cwatson
ms.openlocfilehash: a7527b12f4f0d2b45713a0c0109d81ff51293fd8
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
# <a name="create-a-copy-of-a-vhd-stored-as-an-azure-managed-disk-by-using-managed-snapshots"></a><span data-ttu-id="d674b-103">Utwórz kopię plik VHD przechowywany jako dysk zarządzane Azure przy użyciu migawek zarządzane</span><span class="sxs-lookup"><span data-stu-id="d674b-103">Create a copy of a VHD stored as an Azure Managed Disk by using Managed Snapshots</span></span>
<span data-ttu-id="d674b-104">Migawki zarządzane dysku do utworzenia kopii zapasowej lub Utwórz dysk zarządzane z migawki i dołączenie go do testowej maszyny wirtualnej, aby rozwiązać problemy.</span><span class="sxs-lookup"><span data-stu-id="d674b-104">Take a snapshot of a Managed Disk for backup or create a Managed Disk from the snapshot and attach it to a test virtual machine to troubleshoot.</span></span> <span data-ttu-id="d674b-105">Zarządzane migawki jest kopią pełnej w momencie zarządzane dysku maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="d674b-105">A Managed Snapshot is a full point-in-time copy of a VM Managed Disk.</span></span> <span data-ttu-id="d674b-106">Tworzy kopię tylko do odczytu z wirtualnego dysku twardego i, domyślnie zapisuje go jako dysk standardowy zarządzane.</span><span class="sxs-lookup"><span data-stu-id="d674b-106">It creates a read-only copy of your VHD and, by default, stores it as a Standard Managed Disk.</span></span> <span data-ttu-id="d674b-107">Aby uzyskać więcej informacji o dyskach zarządzanych, zobacz [dysków zarządzanych Azure — omówienie](managed-disks-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="d674b-107">For more information about Managed Disks, see [Azure Managed Disks overview](managed-disks-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)</span></span>

<span data-ttu-id="d674b-108">Aby uzyskać informacje o cenach, zobacz [cennik usługi Azure Storage](https://azure.microsoft.com/pricing/details/managed-disks/).</span><span class="sxs-lookup"><span data-stu-id="d674b-108">For information about pricing, see [Azure Storage Pricing](https://azure.microsoft.com/pricing/details/managed-disks/).</span></span> 

## <a name="before-you-begin"></a><span data-ttu-id="d674b-109">Przed rozpoczęciem</span><span class="sxs-lookup"><span data-stu-id="d674b-109">Before you begin</span></span>
<span data-ttu-id="d674b-110">Jeśli używasz programu PowerShell, upewnij się, że masz najnowszą wersję modułu programu AzureRM.Compute PowerShell.</span><span class="sxs-lookup"><span data-stu-id="d674b-110">If you use PowerShell, make sure that you have the latest version of the AzureRM.Compute PowerShell module.</span></span> <span data-ttu-id="d674b-111">Uruchom następujące polecenie, aby go zainstalować.</span><span class="sxs-lookup"><span data-stu-id="d674b-111">Run the following command to install it.</span></span>

```
Install-Module AzureRM.Compute -RequiredVersion 2.6.0
```
<span data-ttu-id="d674b-112">Aby uzyskać więcej informacji, zobacz [przechowywanie wersji programu Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="d674b-112">For more information, see [Azure PowerShell Versioning](/powershell/azure/overview).</span></span>

## <a name="copy-the-vhd-with-a-snapshot"></a><span data-ttu-id="d674b-113">Skopiuj wirtualny dysk twardy z migawki</span><span class="sxs-lookup"><span data-stu-id="d674b-113">Copy the VHD with a snapshot</span></span>
<span data-ttu-id="d674b-114">Umożliwia utworzenie migawki dysków zarządzanych w portalu Azure lub programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="d674b-114">Use either the Azure portal or PowerShell to take a snapshot of the Managed Disk.</span></span>

### <a name="use-azure-portal-to-take-a-snapshot"></a><span data-ttu-id="d674b-115">Utworzenie migawki za pomocą portalu Azure</span><span class="sxs-lookup"><span data-stu-id="d674b-115">Use Azure portal to take a snapshot</span></span> 

1. <span data-ttu-id="d674b-116">Zaloguj się w witrynie [Azure Portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="d674b-116">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="d674b-117">Uruchamianie w lewym górnym rogu, kliknij przycisk **nowy** i wyszukaj **migawki**.</span><span class="sxs-lookup"><span data-stu-id="d674b-117">Starting in the upper left, click **New** and search for **snapshot**.</span></span>
3. <span data-ttu-id="d674b-118">W bloku migawki kliknij **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="d674b-118">In the Snapshot blade, click **Create**.</span></span>
4. <span data-ttu-id="d674b-119">Wprowadź **nazwa** dla migawki.</span><span class="sxs-lookup"><span data-stu-id="d674b-119">Enter a **Name** for the snapshot.</span></span>
5. <span data-ttu-id="d674b-120">Wybierz istniejącą [grupę zasobów](../../azure-resource-manager/resource-group-overview.md#resource-groups) lub wprowadź nazwę nowej grupy zasobów.</span><span class="sxs-lookup"><span data-stu-id="d674b-120">Select an existing [Resource group](../../azure-resource-manager/resource-group-overview.md#resource-groups) or type the name for a new one.</span></span> 
6. <span data-ttu-id="d674b-121">Wybierz centrum danych Azure lokalizacji.</span><span class="sxs-lookup"><span data-stu-id="d674b-121">Select an Azure datacenter Location.</span></span>  
7. <span data-ttu-id="d674b-122">Dla **dysku źródłowego**, wybierz zarządzany dysk do migawki.</span><span class="sxs-lookup"><span data-stu-id="d674b-122">For **Source disk**, select the Managed Disk to snapshot.</span></span>
8. <span data-ttu-id="d674b-123">Wybierz **typ konta** do przechowywania migawki.</span><span class="sxs-lookup"><span data-stu-id="d674b-123">Select the **Account type** to use to store the snapshot.</span></span> <span data-ttu-id="d674b-124">Firma Microsoft zaleca **Standard_LRS** chyba że ma być przechowywane na dysku wysokiej wydajności.</span><span class="sxs-lookup"><span data-stu-id="d674b-124">We recommend **Standard_LRS** unless you need it stored on a high performing disk.</span></span>
9. <span data-ttu-id="d674b-125">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="d674b-125">Click **Create**.</span></span>

### <a name="use-powershell-to-take-a-snapshot"></a><span data-ttu-id="d674b-126">Utworzenie migawki za pomocą programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="d674b-126">Use PowerShell to take a snapshot</span></span>
<span data-ttu-id="d674b-127">Poniższe kroki pokazują jak uzyskać dysku VHD do skopiowania, Tworzenie migawki konfiguracji i migawki dysku za pomocą polecenia cmdlet New-AzureRmSnapshot<!--Add link to cmdlet when available-->.</span><span class="sxs-lookup"><span data-stu-id="d674b-127">The following steps show you how to get the VHD disk to be copied, create the snapshot configurations, and take a snapshot of the disk by using the New-AzureRmSnapshot cmdlet<!--Add link to cmdlet when available-->.</span></span> 

1. <span data-ttu-id="d674b-128">Ustaw niektórych parametrów.</span><span class="sxs-lookup"><span data-stu-id="d674b-128">Set some parameters.</span></span> 

 ```powershell
$resourceGroupName = 'myResourceGroup' 
$location = 'southeastasia' 
$dataDiskName = 'ContosoMD_datadisk1' 
$snapshotName = 'ContosoMD_datadisk1_snapshot1'  
```
  <span data-ttu-id="d674b-129">Zastąp wartości parametrów:</span><span class="sxs-lookup"><span data-stu-id="d674b-129">Replace the parameter values:</span></span>
  -  <span data-ttu-id="d674b-130">"myResourceGroup" z grupy zasobów maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="d674b-130">"myResourceGroup" with the VM's resource group.</span></span>
  -  <span data-ttu-id="d674b-131">"southeastasia" z lokalizacji geograficznej miejscu migawki zarządzane przechowywane.</span><span class="sxs-lookup"><span data-stu-id="d674b-131">"southeastasia" with the geographic location where you want your Managed Snapshot stored.</span></span> <!---How do you look these up? -->
  -  <span data-ttu-id="d674b-132">"ContosoMD_datadisk1" o nazwie dysku wirtualnego dysku twardego, który chcesz skopiować.</span><span class="sxs-lookup"><span data-stu-id="d674b-132">"ContosoMD_datadisk1" with the name of the VHD disk that you want to copy.</span></span>
  -  <span data-ttu-id="d674b-133">"ContosoMD_datadisk1_snapshot1" o nazwie chcesz użyć dla nowej migawki.</span><span class="sxs-lookup"><span data-stu-id="d674b-133">"ContosoMD_datadisk1_snapshot1" with the name you want to use for the new snapshot.</span></span>

2. <span data-ttu-id="d674b-134">Pobierz dysku VHD do skopiowania.</span><span class="sxs-lookup"><span data-stu-id="d674b-134">Get the VHD disk to be copied.</span></span>

 ```powershell
$disk = Get-AzureRmDisk -ResourceGroupName $resourceGroupName -DiskName $dataDiskName 
```
3. <span data-ttu-id="d674b-135">Tworzenie migawki konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="d674b-135">Create the snapshot configurations.</span></span> 

 ```powershell
$snapshot =  New-AzureRmSnapshotConfig -SourceUri $disk.Id -CreateOption Copy -Location $location 
```
4. <span data-ttu-id="d674b-136">Migawki.</span><span class="sxs-lookup"><span data-stu-id="d674b-136">Take the snapshot.</span></span>

 ```powershell
New-AzureRmSnapshot -Snapshot $snapshot -SnapshotName $snapshotName -ResourceGroupName $resourceGroupName 
```
<span data-ttu-id="d674b-137">Jeśli planujesz użyć migawki, aby utworzyć dysk zarządzany i dołączyć maszynę Wirtualną, która musi być wydajnych, użyj parametru `-AccountType Premium_LRS` przy użyciu polecenia New-AzureRmSnapshot.</span><span class="sxs-lookup"><span data-stu-id="d674b-137">If you plan to use the snapshot to create a Managed Disk and attach it a VM that needs to be high performing, use the parameter `-AccountType Premium_LRS` with the New-AzureRmSnapshot command.</span></span> <span data-ttu-id="d674b-138">Parametr tworzy migawkę tak, aby była przechowywana jako dysk zarządzane Premium.</span><span class="sxs-lookup"><span data-stu-id="d674b-138">The parameter creates the snapshot so that it's stored as a Premium Managed Disk.</span></span> <span data-ttu-id="d674b-139">Dysków zarządzanych w warstwie Premium są droższe niż standardowe.</span><span class="sxs-lookup"><span data-stu-id="d674b-139">Premium Managed Disks are more expensive than Standard.</span></span> <span data-ttu-id="d674b-140">Dlatego upewnij się, że naprawdę potrzebny Premium przed użyciem tego parametru.</span><span class="sxs-lookup"><span data-stu-id="d674b-140">So be sure you really need Premium before using that parameter.</span></span>


