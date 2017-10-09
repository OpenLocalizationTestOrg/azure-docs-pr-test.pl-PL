---
title: "aaaCreate kopii dysku zarządzanego Azure wykonywać kopie zapasowe | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toocreate kopię toouse Azure zarządzanych dysku dla dysku z powrotem się lub rozwiązywania problemów problemy."
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
ms.openlocfilehash: 2f33dbbee624bcd813f3c7c3e3401072d0933714
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-copy-of-a-vhd-stored-as-an-azure-managed-disk-by-using-managed-snapshots"></a><span data-ttu-id="120a8-103">Utwórz kopię plik VHD przechowywany jako dysk zarządzane Azure przy użyciu migawek zarządzane</span><span class="sxs-lookup"><span data-stu-id="120a8-103">Create a copy of a VHD stored as an Azure Managed Disk by using Managed Snapshots</span></span>
<span data-ttu-id="120a8-104">Migawki zarządzane dysku do utworzenia kopii zapasowej lub Utwórz dysk zarządzane z migawki hello i dołączenie go tooa test maszyny wirtualnej tootroubleshoot.</span><span class="sxs-lookup"><span data-stu-id="120a8-104">Take a snapshot of a Managed Disk for backup or create a Managed Disk from hello snapshot and attach it tooa test virtual machine tootroubleshoot.</span></span> <span data-ttu-id="120a8-105">Zarządzane migawki jest kopią pełnej w momencie zarządzane dysku maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="120a8-105">A Managed Snapshot is a full point-in-time copy of a VM Managed Disk.</span></span> <span data-ttu-id="120a8-106">Tworzy kopię tylko do odczytu z wirtualnego dysku twardego i, domyślnie zapisuje go jako dysk standardowy zarządzane.</span><span class="sxs-lookup"><span data-stu-id="120a8-106">It creates a read-only copy of your VHD and, by default, stores it as a Standard Managed Disk.</span></span> <span data-ttu-id="120a8-107">Aby uzyskać więcej informacji o dyskach zarządzanych, zobacz [dysków zarządzanych Azure — omówienie](managed-disks-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="120a8-107">For more information about Managed Disks, see [Azure Managed Disks overview](managed-disks-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)</span></span>

<span data-ttu-id="120a8-108">Aby uzyskać informacje o cenach, zobacz [cennik usługi Azure Storage](https://azure.microsoft.com/pricing/details/managed-disks/).</span><span class="sxs-lookup"><span data-stu-id="120a8-108">For information about pricing, see [Azure Storage Pricing](https://azure.microsoft.com/pricing/details/managed-disks/).</span></span> 

## <a name="before-you-begin"></a><span data-ttu-id="120a8-109">Przed rozpoczęciem</span><span class="sxs-lookup"><span data-stu-id="120a8-109">Before you begin</span></span>
<span data-ttu-id="120a8-110">Jeśli używasz programu PowerShell, upewnij się, że masz najnowszą wersję hello modułu AzureRM.Compute PowerShell hello.</span><span class="sxs-lookup"><span data-stu-id="120a8-110">If you use PowerShell, make sure that you have hello latest version of hello AzureRM.Compute PowerShell module.</span></span> <span data-ttu-id="120a8-111">Uruchom hello następujących tooinstall polecenia.</span><span class="sxs-lookup"><span data-stu-id="120a8-111">Run hello following command tooinstall it.</span></span>

```
Install-Module AzureRM.Compute -RequiredVersion 2.6.0
```
<span data-ttu-id="120a8-112">Aby uzyskać więcej informacji, zobacz [przechowywanie wersji programu Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="120a8-112">For more information, see [Azure PowerShell Versioning](/powershell/azure/overview).</span></span>

## <a name="copy-hello-vhd-with-a-snapshot"></a><span data-ttu-id="120a8-113">Skopiuj hello wirtualnego dysku twardego z migawki</span><span class="sxs-lookup"><span data-stu-id="120a8-113">Copy hello VHD with a snapshot</span></span>
<span data-ttu-id="120a8-114">Użyj hello portalu Azure lub programu PowerShell tootake migawkę hello dysku zarządzanego.</span><span class="sxs-lookup"><span data-stu-id="120a8-114">Use either hello Azure portal or PowerShell tootake a snapshot of hello Managed Disk.</span></span>

### <a name="use-azure-portal-tootake-a-snapshot"></a><span data-ttu-id="120a8-115">Użyj tootake portalu Azure migawki</span><span class="sxs-lookup"><span data-stu-id="120a8-115">Use Azure portal tootake a snapshot</span></span> 

1. <span data-ttu-id="120a8-116">Zaloguj się toohello [portalu Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="120a8-116">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="120a8-117">Począwszy od lewego górnego rogu powitania kliknij **nowy** i wyszukaj **migawki**.</span><span class="sxs-lookup"><span data-stu-id="120a8-117">Starting in hello upper left, click **New** and search for **snapshot**.</span></span>
3. <span data-ttu-id="120a8-118">W bloku migawki powitania kliknij **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="120a8-118">In hello Snapshot blade, click **Create**.</span></span>
4. <span data-ttu-id="120a8-119">Wprowadź **nazwa** hello migawki.</span><span class="sxs-lookup"><span data-stu-id="120a8-119">Enter a **Name** for hello snapshot.</span></span>
5. <span data-ttu-id="120a8-120">Wybierz istniejący [grupy zasobów](../../azure-resource-manager/resource-group-overview.md#resource-groups) lub nazwa typu hello nowej.</span><span class="sxs-lookup"><span data-stu-id="120a8-120">Select an existing [Resource group](../../azure-resource-manager/resource-group-overview.md#resource-groups) or type hello name for a new one.</span></span> 
6. <span data-ttu-id="120a8-121">Wybierz centrum danych Azure lokalizacji.</span><span class="sxs-lookup"><span data-stu-id="120a8-121">Select an Azure datacenter Location.</span></span>  
7. <span data-ttu-id="120a8-122">Aby uzyskać **dysku źródłowego**, wybierz hello toosnapshot dysku zarządzanego.</span><span class="sxs-lookup"><span data-stu-id="120a8-122">For **Source disk**, select hello Managed Disk toosnapshot.</span></span>
8. <span data-ttu-id="120a8-123">Wybierz hello **typ konta** toouse toostore hello migawki.</span><span class="sxs-lookup"><span data-stu-id="120a8-123">Select hello **Account type** toouse toostore hello snapshot.</span></span> <span data-ttu-id="120a8-124">Firma Microsoft zaleca **Standard_LRS** chyba że ma być przechowywane na dysku wysokiej wydajności.</span><span class="sxs-lookup"><span data-stu-id="120a8-124">We recommend **Standard_LRS** unless you need it stored on a high performing disk.</span></span>
9. <span data-ttu-id="120a8-125">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="120a8-125">Click **Create**.</span></span>

### <a name="use-powershell-tootake-a-snapshot"></a><span data-ttu-id="120a8-126">Użyj programu PowerShell tootake migawki</span><span class="sxs-lookup"><span data-stu-id="120a8-126">Use PowerShell tootake a snapshot</span></span>
<span data-ttu-id="120a8-127">Witaj następujące kroki pokazują, jak hello tooget wirtualnego dysku twardego na dysku toobe kopiowane, tworzyć hello konfiguracje migawek i migawki hello dysku za pomocą polecenia cmdlet hello AzureRmSnapshot nowy<!--Add link toocmdlet when available-->.</span><span class="sxs-lookup"><span data-stu-id="120a8-127">hello following steps show you how tooget hello VHD disk toobe copied, create hello snapshot configurations, and take a snapshot of hello disk by using hello New-AzureRmSnapshot cmdlet<!--Add link toocmdlet when available-->.</span></span> 

1. <span data-ttu-id="120a8-128">Ustaw niektórych parametrów.</span><span class="sxs-lookup"><span data-stu-id="120a8-128">Set some parameters.</span></span> 

 ```powershell
$resourceGroupName = 'myResourceGroup' 
$location = 'southeastasia' 
$dataDiskName = 'ContosoMD_datadisk1' 
$snapshotName = 'ContosoMD_datadisk1_snapshot1'  
```
  <span data-ttu-id="120a8-129">Zastąp wartości parametrów hello:</span><span class="sxs-lookup"><span data-stu-id="120a8-129">Replace hello parameter values:</span></span>
  -  <span data-ttu-id="120a8-130">"myResourceGroup" hello wirtualna grupą zasobów.</span><span class="sxs-lookup"><span data-stu-id="120a8-130">"myResourceGroup" with hello VM's resource group.</span></span>
  -  <span data-ttu-id="120a8-131">"southeastasia" z lokalizacji geograficznej hello miejscu migawki zarządzane przechowywane.</span><span class="sxs-lookup"><span data-stu-id="120a8-131">"southeastasia" with hello geographic location where you want your Managed Snapshot stored.</span></span> <!---How do you look these up? -->
  -  <span data-ttu-id="120a8-132">"ContosoMD_datadisk1" o nazwie hello hello dysku VHD, które mają toocopy.</span><span class="sxs-lookup"><span data-stu-id="120a8-132">"ContosoMD_datadisk1" with hello name of hello VHD disk that you want toocopy.</span></span>
  -  <span data-ttu-id="120a8-133">Nazwa "ContosoMD_datadisk1_snapshot1" z hello mają toouse dla hello nową migawkę.</span><span class="sxs-lookup"><span data-stu-id="120a8-133">"ContosoMD_datadisk1_snapshot1" with hello name you want toouse for hello new snapshot.</span></span>

2. <span data-ttu-id="120a8-134">Pobierz toobe dysku VHD hello skopiowane.</span><span class="sxs-lookup"><span data-stu-id="120a8-134">Get hello VHD disk toobe copied.</span></span>

 ```powershell
$disk = Get-AzureRmDisk -ResourceGroupName $resourceGroupName -DiskName $dataDiskName 
```
3. <span data-ttu-id="120a8-135">Utwórz hello konfiguracje migawek.</span><span class="sxs-lookup"><span data-stu-id="120a8-135">Create hello snapshot configurations.</span></span> 

 ```powershell
$snapshot =  New-AzureRmSnapshotConfig -SourceUri $disk.Id -CreateOption Copy -Location $location 
```
4. <span data-ttu-id="120a8-136">Witaj migawki.</span><span class="sxs-lookup"><span data-stu-id="120a8-136">Take hello snapshot.</span></span>

 ```powershell
New-AzureRmSnapshot -Snapshot $snapshot -SnapshotName $snapshotName -ResourceGroupName $resourceGroupName 
```
<span data-ttu-id="120a8-137">Jeśli planujesz toouse hello migawki toocreate dysku zarządzanego dołączyć maszynę Wirtualną, która wymaga wydajnych toobe, użyj parametru hello `-AccountType Premium_LRS` za pomocą polecenia hello AzureRmSnapshot nowy.</span><span class="sxs-lookup"><span data-stu-id="120a8-137">If you plan toouse hello snapshot toocreate a Managed Disk and attach it a VM that needs toobe high performing, use hello parameter `-AccountType Premium_LRS` with hello New-AzureRmSnapshot command.</span></span> <span data-ttu-id="120a8-138">Parametr Hello tworzy migawkę hello, aby są przechowywane jako dysk zarządzane Premium.</span><span class="sxs-lookup"><span data-stu-id="120a8-138">hello parameter creates hello snapshot so that it's stored as a Premium Managed Disk.</span></span> <span data-ttu-id="120a8-139">Dysków zarządzanych w warstwie Premium są droższe niż standardowe.</span><span class="sxs-lookup"><span data-stu-id="120a8-139">Premium Managed Disks are more expensive than Standard.</span></span> <span data-ttu-id="120a8-140">Dlatego upewnij się, że naprawdę potrzebny Premium przed użyciem tego parametru.</span><span class="sxs-lookup"><span data-stu-id="120a8-140">So be sure you really need Premium before using that parameter.</span></span>


