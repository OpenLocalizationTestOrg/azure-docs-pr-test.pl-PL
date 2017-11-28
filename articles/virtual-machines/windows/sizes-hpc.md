---
title: rozmiary maszyny Wirtualnej systemu Windows aaaAzure - HPC | Dokumentacja firmy Microsoft
description: "Wyświetla listę różnych rozmiarów hello dostępne Windows komputerowych o wysokiej wydajności maszyn wirtualnych na platformie Azure."
services: virtual-machines-windows
documentationcenter: 
author: jonbeck7
manager: timlt
editor: 
tags: azure-resource-manager,azure-service-management
ms.assetid: 
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 07/28/2017
ms.author: jonbeck
ms.openlocfilehash: 092bc32cfe048f439ad833911bef4ed17eda7977
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="high-performance-compute-vm-sizes"></a><span data-ttu-id="9d83b-103">Rozmiary maszyn wirtualnych wysokiej wydajności obliczeniowej</span><span class="sxs-lookup"><span data-stu-id="9d83b-103">High performance compute VM sizes</span></span>

[!INCLUDE [virtual-machines-common-sizes-hpc](../../../includes/virtual-machines-common-sizes-hpc.md)]

[!INCLUDE [virtual-machines-common-sizes-table-defs](../../../includes/virtual-machines-common-sizes-table-defs.md)]

[!INCLUDE [virtual-machines-common-a8-a9-a10-a11-specs](../../../includes/virtual-machines-common-a8-a9-a10-a11-specs.md)]

## <a name="rdma-capable-instances"></a><span data-ttu-id="9d83b-104">Z funkcją RDMA wystąpień</span><span class="sxs-lookup"><span data-stu-id="9d83b-104">RDMA-capable instances</span></span>
<span data-ttu-id="9d83b-105">Podzbiór hello obliczeniowych wystąpień (H16r, H16mr A8 i A9) funkcji interfejsu sieciowego dla zdalnego pamięci bezpośredniego dostępu (do pamięci RDMA) łączności.</span><span class="sxs-lookup"><span data-stu-id="9d83b-105">A subset of hello compute-intensive instances (H16r, H16mr, A8, and A9) feature a network interface for remote direct memory access (RDMA) connectivity.</span></span> <span data-ttu-id="9d83b-106">Ten interfejs jest ponadto rozmiarów maszyn wirtualnych dostępne tooother toohello standardowe sieć platformy Azure interfejsu.</span><span class="sxs-lookup"><span data-stu-id="9d83b-106">This interface is in addition toohello standard Azure network interface available tooother VM sizes.</span></span> 
  
<span data-ttu-id="9d83b-107">Ten interfejs umożliwia toocommunicate wystąpień z funkcją RDMA hello za pośrednictwem sieci InfiniBand, działających z rozdzielczością stawki FDR H16r i H16mr maszyn wirtualnych i szybkości QDR A8 i A9 maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="9d83b-107">This interface allows hello RDMA-capable instances toocommunicate over an InfiniBand network, operating at FDR rates for H16r and H16mr virtual machines, and QDR rates for A8 and A9 virtual machines.</span></span> <span data-ttu-id="9d83b-108">Tych funkcji RDMA można zwiększyć hello skalowalność i wydajność aplikacji komunikat interfejsu (Passing Interface).</span><span class="sxs-lookup"><span data-stu-id="9d83b-108">These RDMA capabilities can boost hello scalability and performance of Message Passing Interface (MPI) applications.</span></span>

<span data-ttu-id="9d83b-109">Poniżej przedstawiono wymagania dla maszyn wirtualnych systemu Windows z funkcją RDMA tooaccess hello Azure RDMA sieci:</span><span class="sxs-lookup"><span data-stu-id="9d83b-109">Following are requirements for RDMA-capable Windows VMs tooaccess hello Azure RDMA network:</span></span> 

* <span data-ttu-id="9d83b-110">**System operacyjny**</span><span class="sxs-lookup"><span data-stu-id="9d83b-110">**Operating system**</span></span>
  
  <span data-ttu-id="9d83b-111">Windows Server 2012 R2, Windows Server 2012</span><span class="sxs-lookup"><span data-stu-id="9d83b-111">Windows Server 2012 R2, Windows Server 2012</span></span>
  
  > [!NOTE]
  > <span data-ttu-id="9d83b-112">Windows Server 2016 nie obsługuje obecnie, łączności RDMA na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="9d83b-112">Currently, Windows Server 2016 does not support RDMA connectivity in Azure.</span></span>
  >

* <span data-ttu-id="9d83b-113">**Zestaw dostępności lub usługi w chmurze** — maszyny wirtualne z funkcją RDMA hello Wdróż w hello tym samym zestawie (Jeśli używasz modelu wdrażania usługi Azure Resource Manager hello) dostępności lub hello tej samej usługi w chmurze (Jeśli używasz hello klasycznego modelu wdrażania).</span><span class="sxs-lookup"><span data-stu-id="9d83b-113">**Availability set or cloud service** – Deploy hello RDMA-capable VMs in hello same availability set (when you use hello Azure Resource Manager deployment model) or hello same cloud service (when you use hello classic deployment model).</span></span> <span data-ttu-id="9d83b-114">Jeśli używasz partii zadań Azure hello maszyn wirtualnych z funkcją RDMA muszą być w hello tej samej puli.</span><span class="sxs-lookup"><span data-stu-id="9d83b-114">If you use Azure Batch, hello RDMA-capable VMs must be in hello same pool.</span></span>

* <span data-ttu-id="9d83b-115">**MPI** -MPI firmy Microsoft (MS-MPI) 2012 R2 lub nowszym, Intel MPI biblioteki 5.x</span><span class="sxs-lookup"><span data-stu-id="9d83b-115">**MPI** - Microsoft MPI (MS-MPI) 2012 R2 or later, Intel MPI Library 5.x</span></span>

  <span data-ttu-id="9d83b-116">Obsługiwane implementacje MPI za pomocą interfejsu Network Direct Microsoft toocommunicate interfejsu hello między wystąpieniami.</span><span class="sxs-lookup"><span data-stu-id="9d83b-116">Supported MPI implementations use hello Microsoft Network Direct interface toocommunicate between instances.</span></span> 

* <span data-ttu-id="9d83b-117">**Przestrzeń adresową sieci RDMA** -172.16.0.0/16 przestrzeni adresowej hello rezerwuje hello RDMA sieci na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="9d83b-117">**RDMA network address space** - hello RDMA network in Azure reserves hello address space 172.16.0.0/16.</span></span> <span data-ttu-id="9d83b-118">toorun MPI aplikacji w wystąpieniach wdrożony w sieci wirtualnej platformy Azure, upewnij się, czy przestrzeń adresową sieci wirtualnej hello nakłada się na powitania RDMA sieci.</span><span class="sxs-lookup"><span data-stu-id="9d83b-118">toorun MPI applications on instances deployed in an Azure virtual network, make sure that hello virtual network address space does not overlap hello RDMA network.</span></span>

* <span data-ttu-id="9d83b-119">**Rozszerzenia maszyny Wirtualnej HpcVmDrivers** — na maszynach wirtualnych z funkcją RDMA, należy dodać hello HpcVmDrivers rozszerzenia tooinstall sieci sterowniki urządzeń systemu Windows dla łączności funkcji RDMA.</span><span class="sxs-lookup"><span data-stu-id="9d83b-119">**HpcVmDrivers VM extension** - On RDMA-capable VMs, you must add hello HpcVmDrivers extension tooinstall Windows network device drivers for RDMA connectivity.</span></span> <span data-ttu-id="9d83b-120">(W przypadku niektórych wdrożeń wystąpień A8 i A9, hello HpcVmDrivers rozszerzenia jest dodawane automatycznie). tooadd hello wirtualna rozszerzenia tooa maszyny Wirtualnej, można użyć [programu Azure PowerShell](/powershell/azure/overview) polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="9d83b-120">(In certain deployments of A8 and A9 instances, hello HpcVmDrivers extension is added automatically.) tooadd hello VM extension tooa VM, you can use [Azure PowerShell](/powershell/azure/overview) cmdlets.</span></span> 

  
  <span data-ttu-id="9d83b-121">Witaj, następujące polecenia instaluje hello najnowszej wersji 1.1 HpcVMDrivers rozszerzenia na istniejącej maszyny Wirtualnej z funkcją RDMA, o nazwie *myVM* wdrożone w grupie zasobów hello o nazwie *myResourceGroup* w hello  *Zachodnie stany USA* regionu:</span><span class="sxs-lookup"><span data-stu-id="9d83b-121">hello following command installs hello latest version 1.1 HpcVMDrivers extension on an existing RDMA-capable VM named *myVM* deployed in hello resource group named *myResourceGroup* in hello *West US* region:</span></span>

  ```PowerShell
  Set-AzureRmVMExtension -ResourceGroupName "myResourceGroup" -Location "westus" -VMName "myVM" -ExtensionName "HpcVmDrivers" -Publisher "Microsoft.HpcCompute" -Type "HpcVmDrivers" -TypeHandlerVersion "1.1"
  ```
  
  <span data-ttu-id="9d83b-122">Aby uzyskać więcej informacji, zobacz [rozszerzenia maszyn wirtualnych i funkcji](extensions-features.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="9d83b-122">For more information, see [Virtual machine extensions and features](extensions-features.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> <span data-ttu-id="9d83b-123">Może również współpracować z rozszerzeniami dla maszyn wirtualnych wdrożonych w hello [klasycznego modelu wdrażania](classic/manage-extensions.md).</span><span class="sxs-lookup"><span data-stu-id="9d83b-123">You can also work with extensions for VMs deployed in hello [classic deployment model](classic/manage-extensions.md).</span></span>


## <a name="using-hpc-pack"></a><span data-ttu-id="9d83b-124">Przy użyciu pakietu HPC</span><span class="sxs-lookup"><span data-stu-id="9d83b-124">Using HPC Pack</span></span>

<span data-ttu-id="9d83b-125">[Microsoft HPC Pack](https://technet.microsoft.com/library/jj899572.aspx), rozwiązania firmy Microsoft wolnego HPC klastra i zadania zarządzania, jest jedną z opcji toocreate klastra obliczeniowego w aplikacjach opartych na systemie Windows MPI Azure toorun i innych obciążeń HPC.</span><span class="sxs-lookup"><span data-stu-id="9d83b-125">[Microsoft HPC Pack](https://technet.microsoft.com/library/jj899572.aspx), Microsoft’s free HPC cluster and job management solution, is one option for you toocreate a compute cluster in Azure toorun Windows-based MPI applications and other HPC workloads.</span></span> <span data-ttu-id="9d83b-126">HPC Pack 2012 R2 i nowsze wersje zawierają środowiska uruchomieniowego dla MPI MS, który używa hello Azure RDMA sieci po wdrożeniu na maszynach wirtualnych z funkcją RDMA.</span><span class="sxs-lookup"><span data-stu-id="9d83b-126">HPC Pack 2012 R2 and later versions include a runtime environment for MS-MPI that uses hello Azure RDMA network when deployed on RDMA-capable VMs.</span></span>




## <a name="other-sizes"></a><span data-ttu-id="9d83b-127">Innych rozmiarach</span><span class="sxs-lookup"><span data-stu-id="9d83b-127">Other sizes</span></span>
- [<span data-ttu-id="9d83b-128">Zastosowania ogólne</span><span class="sxs-lookup"><span data-stu-id="9d83b-128">General purpose</span></span>](sizes-general.md)
- [<span data-ttu-id="9d83b-129">Optymalizacja pod kątem obliczeń</span><span class="sxs-lookup"><span data-stu-id="9d83b-129">Compute optimized</span></span>](sizes-compute.md)
- [<span data-ttu-id="9d83b-130">Optymalizacja pod kątem pamięci</span><span class="sxs-lookup"><span data-stu-id="9d83b-130">Memory optimized</span></span>](../virtual-machines-windows-sizes-memory.md)
- [<span data-ttu-id="9d83b-131">Optymalizacja pod kątem magazynu</span><span class="sxs-lookup"><span data-stu-id="9d83b-131">Storage optimized</span></span>](../virtual-machines-windows-sizes-storage.md)
- [<span data-ttu-id="9d83b-132">Optymalizacja pod kątem procesora GPU</span><span class="sxs-lookup"><span data-stu-id="9d83b-132">GPU optimized</span></span>](sizes-gpu.md)

## <a name="next-steps"></a><span data-ttu-id="9d83b-133">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="9d83b-133">Next steps</span></span>

- <span data-ttu-id="9d83b-134">Listy kontrolne toouse hello obliczeniowych wystąpień pakietem HPC w systemie Windows Server, zobacz [Konfigurowanie klastra RDMA systemu Windows z aplikacjami MPI toorun HPC Pack](classic/hpcpack-rdma-cluster.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="9d83b-134">For checklists toouse hello compute-intensive instances with HPC Pack on Windows Server, see [Set up a Windows RDMA cluster with HPC Pack toorun MPI applications](classic/hpcpack-rdma-cluster.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span></span>

- <span data-ttu-id="9d83b-135">toouse obliczeniowych wystąpień podczas uruchamiania aplikacji MPI za pomocą partii zadań Azure, zobacz [użycie wielu wystąpień zadań toorun komunikat interfejsu (Passing Interface) aplikacji w partii zadań Azure](../../batch/batch-mpi.md).</span><span class="sxs-lookup"><span data-stu-id="9d83b-135">toouse compute-intensive instances when running MPI applications with Azure Batch, see [Use multi-instance tasks toorun Message Passing Interface (MPI) applications in Azure Batch](../../batch/batch-mpi.md).</span></span>

- <span data-ttu-id="9d83b-136">Dowiedz się więcej na temat [jednostki (ACU) rozwiązań usługi obliczenia Azure](acu.md) ułatwia porównanie wydajności obliczeniowej różnych jednostki SKU Azure.</span><span class="sxs-lookup"><span data-stu-id="9d83b-136">Learn more about how [Azure compute units (ACU)](acu.md) can help you compare compute performance across Azure SKUs.</span></span>




