---
title: Rozmiary maszyny Wirtualnej systemu Windows Azure - HPC | Dokumentacja firmy Microsoft
description: "Wyświetla listę różnych rozmiarów dostępnych Windows komputerowych o wysokiej wydajności maszyn wirtualnych na platformie Azure."
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
ms.openlocfilehash: a0596d134e9c26877848f93d72f35bfd2c957570
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="high-performance-compute-vm-sizes"></a><span data-ttu-id="6f2b6-103">Rozmiary maszyn wirtualnych wysokiej wydajności obliczeniowej</span><span class="sxs-lookup"><span data-stu-id="6f2b6-103">High performance compute VM sizes</span></span>

[!INCLUDE [virtual-machines-common-sizes-hpc](../../../includes/virtual-machines-common-sizes-hpc.md)]

[!INCLUDE [virtual-machines-common-sizes-table-defs](../../../includes/virtual-machines-common-sizes-table-defs.md)]

[!INCLUDE [virtual-machines-common-a8-a9-a10-a11-specs](../../../includes/virtual-machines-common-a8-a9-a10-a11-specs.md)]

## <a name="rdma-capable-instances"></a><span data-ttu-id="6f2b6-104">Z funkcją RDMA wystąpień</span><span class="sxs-lookup"><span data-stu-id="6f2b6-104">RDMA-capable instances</span></span>
<span data-ttu-id="6f2b6-105">Podzbiór wystąpień obliczeniowych (H16r, H16mr A8 i A9) funkcji interfejsu sieciowego dla zdalnego pamięci bezpośredniego dostępu (do pamięci RDMA) łączności.</span><span class="sxs-lookup"><span data-stu-id="6f2b6-105">A subset of the compute-intensive instances (H16r, H16mr, A8, and A9) feature a network interface for remote direct memory access (RDMA) connectivity.</span></span> <span data-ttu-id="6f2b6-106">Ten interfejs jest oprócz interfejsu standardowe sieć platformy Azure, dostępne dla innych rozmiarów maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="6f2b6-106">This interface is in addition to the standard Azure network interface available to other VM sizes.</span></span> 
  
<span data-ttu-id="6f2b6-107">Ten interfejs umożliwia wystąpienia z funkcją RDMA do komunikacji za pośrednictwem sieci InfiniBand, działających z rozdzielczością stawki FDR H16r i H16mr maszyn wirtualnych i szybkości QDR A8 i A9 maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="6f2b6-107">This interface allows the RDMA-capable instances to communicate over an InfiniBand network, operating at FDR rates for H16r and H16mr virtual machines, and QDR rates for A8 and A9 virtual machines.</span></span> <span data-ttu-id="6f2b6-108">Tych funkcji RDMA może zwiększyć skalowalność i wydajność aplikacji komunikat interfejsu (Passing Interface).</span><span class="sxs-lookup"><span data-stu-id="6f2b6-108">These RDMA capabilities can boost the scalability and performance of Message Passing Interface (MPI) applications.</span></span>

<span data-ttu-id="6f2b6-109">Poniżej przedstawiono wymagania dotyczące maszyn wirtualnych systemu Windows z funkcją RDMA do uzyskania dostępu do sieci Azure RDMA:</span><span class="sxs-lookup"><span data-stu-id="6f2b6-109">Following are requirements for RDMA-capable Windows VMs to access the Azure RDMA network:</span></span> 

* <span data-ttu-id="6f2b6-110">**System operacyjny**</span><span class="sxs-lookup"><span data-stu-id="6f2b6-110">**Operating system**</span></span>
  
  <span data-ttu-id="6f2b6-111">Windows Server 2012 R2, Windows Server 2012</span><span class="sxs-lookup"><span data-stu-id="6f2b6-111">Windows Server 2012 R2, Windows Server 2012</span></span>
  
  > [!NOTE]
  > <span data-ttu-id="6f2b6-112">Windows Server 2016 nie obsługuje obecnie, łączności RDMA na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="6f2b6-112">Currently, Windows Server 2016 does not support RDMA connectivity in Azure.</span></span>
  >

* <span data-ttu-id="6f2b6-113">**Zestaw dostępności lub usługi w chmurze** — wdrażanie maszyn wirtualnych z funkcją RDMA w tym samym zestawie dostępności (przy użyciu modelu wdrażania usługi Azure Resource Manager) lub samej usługi w chmurze (przy użyciu klasycznego modelu wdrażania).</span><span class="sxs-lookup"><span data-stu-id="6f2b6-113">**Availability set or cloud service** – Deploy the RDMA-capable VMs in the same availability set (when you use the Azure Resource Manager deployment model) or the same cloud service (when you use the classic deployment model).</span></span> <span data-ttu-id="6f2b6-114">Jeśli używasz partii zadań Azure, maszyny wirtualne z funkcją RDMA musi być w tej samej puli.</span><span class="sxs-lookup"><span data-stu-id="6f2b6-114">If you use Azure Batch, the RDMA-capable VMs must be in the same pool.</span></span>

* <span data-ttu-id="6f2b6-115">**MPI** -MPI firmy Microsoft (MS-MPI) 2012 R2 lub nowszym, Intel MPI biblioteki 5.x</span><span class="sxs-lookup"><span data-stu-id="6f2b6-115">**MPI** - Microsoft MPI (MS-MPI) 2012 R2 or later, Intel MPI Library 5.x</span></span>

  <span data-ttu-id="6f2b6-116">Obsługiwanych implementacje MPI Użyj interfejsu Network Direct Microsoft interfejsu do komunikacji między wystąpieniami.</span><span class="sxs-lookup"><span data-stu-id="6f2b6-116">Supported MPI implementations use the Microsoft Network Direct interface to communicate between instances.</span></span> 

* <span data-ttu-id="6f2b6-117">**Przestrzeń adresową sieci RDMA** -RDMA sieci na platformie Azure rezerwuje 172.16.0.0/16 przestrzeni adresowej.</span><span class="sxs-lookup"><span data-stu-id="6f2b6-117">**RDMA network address space** - The RDMA network in Azure reserves the address space 172.16.0.0/16.</span></span> <span data-ttu-id="6f2b6-118">Do uruchamiania aplikacji MPI w wystąpieniach wdrożony w sieci wirtualnej platformy Azure, upewnij się, że przestrzeń adresową sieci wirtualnej nakłada się na sieciowych RDMA.</span><span class="sxs-lookup"><span data-stu-id="6f2b6-118">To run MPI applications on instances deployed in an Azure virtual network, make sure that the virtual network address space does not overlap the RDMA network.</span></span>

* <span data-ttu-id="6f2b6-119">**Rozszerzenia maszyny Wirtualnej HpcVmDrivers** — na maszynach wirtualnych z funkcją RDMA, należy dodać rozszerzenie HpcVmDrivers, aby zainstalować sterowniki urządzeń sieciowych systemu Windows dla łączności RDMA.</span><span class="sxs-lookup"><span data-stu-id="6f2b6-119">**HpcVmDrivers VM extension** - On RDMA-capable VMs, you must add the HpcVmDrivers extension to install Windows network device drivers for RDMA connectivity.</span></span> <span data-ttu-id="6f2b6-120">(W przypadku niektórych wdrożeń wystąpień A8 i A9, rozszerzenia HpcVmDrivers jest dodawane automatycznie). Aby dodać rozszerzenie maszyny Wirtualnej do maszyny Wirtualnej, można użyć [programu Azure PowerShell](/powershell/azure/overview) polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="6f2b6-120">(In certain deployments of A8 and A9 instances, the HpcVmDrivers extension is added automatically.) To add the VM extension to a VM, you can use [Azure PowerShell](/powershell/azure/overview) cmdlets.</span></span> 

  
  <span data-ttu-id="6f2b6-121">Polecenie instaluje najnowsze rozszerzenia HpcVMDrivers wersji 1.1 na istniejącej maszyny Wirtualnej z funkcją RDMA, o nazwie *myVM* wdrożone w grupie zasobów o nazwie *myResourceGroup* w  *Zachodnie stany USA* regionu:</span><span class="sxs-lookup"><span data-stu-id="6f2b6-121">The following command installs the latest version 1.1 HpcVMDrivers extension on an existing RDMA-capable VM named *myVM* deployed in the resource group named *myResourceGroup* in the *West US* region:</span></span>

  ```PowerShell
  Set-AzureRmVMExtension -ResourceGroupName "myResourceGroup" -Location "westus" -VMName "myVM" -ExtensionName "HpcVmDrivers" -Publisher "Microsoft.HpcCompute" -Type "HpcVmDrivers" -TypeHandlerVersion "1.1"
  ```
  
  <span data-ttu-id="6f2b6-122">Aby uzyskać więcej informacji, zobacz [rozszerzenia maszyn wirtualnych i funkcji](extensions-features.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="6f2b6-122">For more information, see [Virtual machine extensions and features](extensions-features.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> <span data-ttu-id="6f2b6-123">Może również współpracować z rozszerzeniami dla maszyn wirtualnych wdrożonych w [klasycznego modelu wdrażania](classic/manage-extensions.md).</span><span class="sxs-lookup"><span data-stu-id="6f2b6-123">You can also work with extensions for VMs deployed in the [classic deployment model](classic/manage-extensions.md).</span></span>


## <a name="using-hpc-pack"></a><span data-ttu-id="6f2b6-124">Przy użyciu pakietu HPC</span><span class="sxs-lookup"><span data-stu-id="6f2b6-124">Using HPC Pack</span></span>

<span data-ttu-id="6f2b6-125">[Microsoft HPC Pack](https://technet.microsoft.com/library/jj899572.aspx), rozwiązania firmy Microsoft wolnego HPC klastra i zadania zarządzania, jest jedną z opcji tworzenia klastra obliczeniowego na platformie Azure do uruchamiania aplikacji opartych na systemie Windows MPI i innych obciążeń HPC.</span><span class="sxs-lookup"><span data-stu-id="6f2b6-125">[Microsoft HPC Pack](https://technet.microsoft.com/library/jj899572.aspx), Microsoft’s free HPC cluster and job management solution, is one option for you to create a compute cluster in Azure to run Windows-based MPI applications and other HPC workloads.</span></span> <span data-ttu-id="6f2b6-126">HPC Pack 2012 R2 i nowsze wersje zawierają środowisko uruchomieniowe MPI MS wykorzystującego sieć Azure RDMA po wdrożeniu na maszynach wirtualnych z funkcją RDMA.</span><span class="sxs-lookup"><span data-stu-id="6f2b6-126">HPC Pack 2012 R2 and later versions include a runtime environment for MS-MPI that uses the Azure RDMA network when deployed on RDMA-capable VMs.</span></span>




## <a name="other-sizes"></a><span data-ttu-id="6f2b6-127">Innych rozmiarach</span><span class="sxs-lookup"><span data-stu-id="6f2b6-127">Other sizes</span></span>
- [<span data-ttu-id="6f2b6-128">Zastosowania ogólne</span><span class="sxs-lookup"><span data-stu-id="6f2b6-128">General purpose</span></span>](sizes-general.md)
- [<span data-ttu-id="6f2b6-129">Optymalizacja pod kątem obliczeń</span><span class="sxs-lookup"><span data-stu-id="6f2b6-129">Compute optimized</span></span>](sizes-compute.md)
- [<span data-ttu-id="6f2b6-130">Optymalizacja pod kątem pamięci</span><span class="sxs-lookup"><span data-stu-id="6f2b6-130">Memory optimized</span></span>](../virtual-machines-windows-sizes-memory.md)
- [<span data-ttu-id="6f2b6-131">Optymalizacja pod kątem magazynu</span><span class="sxs-lookup"><span data-stu-id="6f2b6-131">Storage optimized</span></span>](../virtual-machines-windows-sizes-storage.md)
- [<span data-ttu-id="6f2b6-132">Optymalizacja pod kątem procesora GPU</span><span class="sxs-lookup"><span data-stu-id="6f2b6-132">GPU optimized</span></span>](sizes-gpu.md)

## <a name="next-steps"></a><span data-ttu-id="6f2b6-133">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="6f2b6-133">Next steps</span></span>

- <span data-ttu-id="6f2b6-134">Dla listy kontrolne użyć wystąpienia obliczeniowych pakietem HPC w systemie Windows Server, zobacz [Konfigurowanie klastra RDMA systemu Windows z pakietem HPC do uruchamiania aplikacji MPI](classic/hpcpack-rdma-cluster.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="6f2b6-134">For checklists to use the compute-intensive instances with HPC Pack on Windows Server, see [Set up a Windows RDMA cluster with HPC Pack to run MPI applications](classic/hpcpack-rdma-cluster.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span></span>

- <span data-ttu-id="6f2b6-135">Aby użyć wystąpienia obliczeniowych, podczas uruchamiania aplikacji MPI za pomocą partii zadań Azure, zobacz [korzystać z zadań w wielu wystąpieniach na uruchamianie aplikacji komunikat interfejsu (Passing Interface) w partii zadań Azure](../../batch/batch-mpi.md).</span><span class="sxs-lookup"><span data-stu-id="6f2b6-135">To use compute-intensive instances when running MPI applications with Azure Batch, see [Use multi-instance tasks to run Message Passing Interface (MPI) applications in Azure Batch](../../batch/batch-mpi.md).</span></span>

- <span data-ttu-id="6f2b6-136">Dowiedz się więcej na temat [jednostki (ACU) rozwiązań usługi obliczenia Azure](acu.md) ułatwia porównanie wydajności obliczeniowej różnych jednostki SKU Azure.</span><span class="sxs-lookup"><span data-stu-id="6f2b6-136">Learn more about how [Azure compute units (ACU)](acu.md) can help you compare compute performance across Azure SKUs.</span></span>




