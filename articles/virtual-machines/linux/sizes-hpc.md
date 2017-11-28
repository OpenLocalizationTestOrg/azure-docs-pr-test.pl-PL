---
title: rozmiary aaaAzure maszyny Wirtualnej systemu Linux - HPC | Dokumentacja firmy Microsoft
description: "Wyświetla listę różnych rozmiarów hello dostępne Linux komputerowych o wysokiej wydajności maszyn wirtualnych na platformie Azure."
services: virtual-machines-linux
documentationcenter: 
author: jonbeck7
manager: timlt
editor: 
tags: azure-resource-manager,azure-service-management
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 07/28/2017
ms.author: jonbeck
ms.openlocfilehash: 0b02ee592902ff8097a71898faea1ac17a947d1a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="high-performance-compute-linux-vm-sizes"></a><span data-ttu-id="b2b21-103">Wysoka wydajność obliczeniowe rozmiary maszyny Wirtualnej systemu Linux</span><span class="sxs-lookup"><span data-stu-id="b2b21-103">High performance compute Linux VM sizes</span></span>

[!INCLUDE [virtual-machines-common-sizes-hpc](../../../includes/virtual-machines-common-sizes-hpc.md)]

[!INCLUDE [virtual-machines-common-sizes-table-defs](../../../includes/virtual-machines-common-sizes-table-defs.md)]

[!INCLUDE [virtual-machines-common-a8-a9-a10-a11-specs](../../../includes/virtual-machines-common-a8-a9-a10-a11-specs.md)]

## <a name="rdma-capable-instances"></a><span data-ttu-id="b2b21-104">Z funkcją RDMA wystąpień</span><span class="sxs-lookup"><span data-stu-id="b2b21-104">RDMA-capable instances</span></span>
<span data-ttu-id="b2b21-105">Podzbiór hello obliczeniowych wystąpień (H16r, H16mr A8 i A9) funkcji interfejsu sieciowego dla zdalnego pamięci bezpośredniego dostępu (do pamięci RDMA) łączności.</span><span class="sxs-lookup"><span data-stu-id="b2b21-105">A subset of hello compute-intensive instances (H16r, H16mr, A8, and A9) feature a network interface for remote direct memory access (RDMA) connectivity.</span></span> <span data-ttu-id="b2b21-106">Ten interfejs jest ponadto rozmiarów maszyn wirtualnych dostępne tooother toohello standardowe sieć platformy Azure interfejsu.</span><span class="sxs-lookup"><span data-stu-id="b2b21-106">This interface is in addition toohello standard Azure network interface available tooother VM sizes.</span></span> 
  
<span data-ttu-id="b2b21-107">Ten interfejs umożliwia toocommunicate wystąpień z funkcją RDMA hello za pośrednictwem sieci InfiniBand, działających z rozdzielczością stawki FDR H16r i H16mr maszyn wirtualnych i szybkości QDR A8 i A9 maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="b2b21-107">This interface allows hello RDMA-capable instances toocommunicate over an InfiniBand network, operating at FDR rates for H16r and H16mr virtual machines, and QDR rates for A8 and A9 virtual machines.</span></span> <span data-ttu-id="b2b21-108">Tych funkcji RDMA można zwiększyć hello skalowalność i wydajność aplikacji komunikat interfejsu (Passing Interface).</span><span class="sxs-lookup"><span data-stu-id="b2b21-108">These RDMA capabilities can boost hello scalability and performance of Message Passing Interface (MPI) applications.</span></span>

<span data-ttu-id="b2b21-109">Poniżej przedstawiono wymagania dla maszyn wirtualnych systemu Linux z funkcją RDMA tooaccess hello Azure RDMA sieci:</span><span class="sxs-lookup"><span data-stu-id="b2b21-109">Following are requirements for RDMA-capable Linux VMs tooaccess hello Azure RDMA network:</span></span>
 
* <span data-ttu-id="b2b21-110">**Dystrybucje** — należy wdrożyć maszyn wirtualnych z funkcją RDMA SUSE Linux Enterprise Server (SLES) lub obrazów nieautoryzowanego oprogramowania Wave (dawniej OpenLogic) na podstawie CentOS HPC w hello Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="b2b21-110">**Distributions** - You must deploy VMs from RDMA-capable SUSE Linux Enterprise Server (SLES) or Rogue Wave Software (formerly OpenLogic) CentOS-based HPC images in hello Azure Marketplace.</span></span> <span data-ttu-id="b2b21-111">Witaj następujące obrazy Marketplace obsługi funkcji RDMA połączeń:</span><span class="sxs-lookup"><span data-stu-id="b2b21-111">hello following Marketplace images support RDMA connectivity:</span></span>
  
    * <span data-ttu-id="b2b21-112">SLES 12 SP1 HPC lub SLES 12 SP1 w przypadku HPC (Premium)</span><span class="sxs-lookup"><span data-stu-id="b2b21-112">SLES 12 SP1 for HPC, or SLES 12 SP1 for HPC (Premium)</span></span>
    
    * <span data-ttu-id="b2b21-113">Na podstawie centOS 7.3 HPC, na podstawie CentOS 7.1 HPC, na podstawie CentOS 6.8 HPC lub na podstawie CentOS HPC 6.5</span><span class="sxs-lookup"><span data-stu-id="b2b21-113">CentOS-based 7.3 HPC, CentOS-based 7.1 HPC, CentOS-based 6.8 HPC, or CentOS-based 6.5 HPC</span></span>  
 
        > [!NOTE]
        > <span data-ttu-id="b2b21-114">Dla maszyn wirtualnych, H-series firma Microsoft zaleca SLES 12 SP1 HPC obrazu lub na podstawie CentOS 7.1 lub nowszym HPC obrazu.</span><span class="sxs-lookup"><span data-stu-id="b2b21-114">For H-series VMs, we recommend either a SLES 12 SP1 for HPC image or CentOS-based 7.1 or later HPC image.</span></span>
        >
        > <span data-ttu-id="b2b21-115">Na obrazach na podstawie CentOS HPC hello, aktualizacji jądra są wyłączone w hello **yum** pliku konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="b2b21-115">On hello CentOS-based HPC images, kernel updates are disabled in hello **yum** configuration file.</span></span> <span data-ttu-id="b2b21-116">To dlatego hello Linux RDMA sterowniki są dystrybuowane jako pakiet RPM, a aktualizacje sterowników może nie działać w przypadku jądra hello jest aktualizowany.</span><span class="sxs-lookup"><span data-stu-id="b2b21-116">This is because hello Linux RDMA drivers are distributed as an RPM package, and driver updates might not work if hello kernel is updated.</span></span>
        > 
        > 
* <span data-ttu-id="b2b21-117">**MPI** — Biblioteka MPI Intel 5.x</span><span class="sxs-lookup"><span data-stu-id="b2b21-117">**MPI** - Intel MPI Library 5.x</span></span>
  
    <span data-ttu-id="b2b21-118">W zależności od obrazu z witryny Marketplace hello można wybrać, oddzielnej licencji, instalacji, albo konfiguracji Intel MPI mogą być potrzebne w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="b2b21-118">Depending on hello Marketplace image you choose, separate licensing, installation, or configuration of Intel MPI may be needed, as follows:</span></span> 
  
  * <span data-ttu-id="b2b21-119">**SLES 12 SP1 obrazu HPC** -Intel MPI pakiety są dystrybuowane na powitania maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="b2b21-119">**SLES 12 SP1 for HPC image** - Intel MPI packages are distributed on hello VM.</span></span> <span data-ttu-id="b2b21-120">Zainstalować, uruchamiając następujące polecenie hello:</span><span class="sxs-lookup"><span data-stu-id="b2b21-120">Install by running hello following command:</span></span>

      ```bash
      sudo rpm -v -i --nodeps /opt/intelMPI/intel_mpi_packages/*.rpm
      ```

  * <span data-ttu-id="b2b21-121">**Na podstawie centOS obrazów HPC** -Intel MPI 5.1 jest już zainstalowana.</span><span class="sxs-lookup"><span data-stu-id="b2b21-121">**CentOS-based HPC images**  - Intel MPI 5.1 is already installed.</span></span>  
    
    <span data-ttu-id="b2b21-122">Konfiguracja dodatkowych systemu jest wymagane toorun zadań MPI w klastrowanych maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="b2b21-122">Additional system configuration is needed toorun MPI jobs on clustered VMs.</span></span> <span data-ttu-id="b2b21-123">Na przykład w klastrze maszyn wirtualnych, należy tooestablish relacji zaufania między hello węzły obliczeniowe.</span><span class="sxs-lookup"><span data-stu-id="b2b21-123">For example, on a cluster of VMs, you need tooestablish trust among hello compute nodes.</span></span> <span data-ttu-id="b2b21-124">W przypadku typowych ustawień, zobacz [skonfigurowanie Linux RDMA klastra toorun MPI aplikacji](classic/rdma-cluster.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="b2b21-124">For typical settings, see [Set up a Linux RDMA cluster toorun MPI applications](classic/rdma-cluster.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)</span></span>

### <a name="network-topology-considerations"></a><span data-ttu-id="b2b21-125">Zagadnienia dotyczące topologii sieci</span><span class="sxs-lookup"><span data-stu-id="b2b21-125">Network topology considerations</span></span>
* <span data-ttu-id="b2b21-126">W przypadku komputerów z obsługą RDMA maszyn wirtualnych systemu Linux na platformie Azure Eth1 jest zarezerwowana dla ruchu sieciowego RDMA.</span><span class="sxs-lookup"><span data-stu-id="b2b21-126">On RDMA-enabled Linux VMs in Azure, Eth1 is reserved for RDMA network traffic.</span></span> <span data-ttu-id="b2b21-127">Nie należy zmieniać ustawienia Eth1 lub wszelkie informacje zawarte w pliku konfiguracji hello odwołujących się toothis sieci.</span><span class="sxs-lookup"><span data-stu-id="b2b21-127">Do not change any Eth1 settings or any information in hello configuration file referring toothis network.</span></span> <span data-ttu-id="b2b21-128">Eth0 jest zarezerwowana dla regularnych Azure ruchu sieciowego.</span><span class="sxs-lookup"><span data-stu-id="b2b21-128">Eth0 is reserved for regular Azure network traffic.</span></span>

* <span data-ttu-id="b2b21-129">IP przez InfiniBand (IB) nie jest obsługiwana na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="b2b21-129">In Azure, IP over InfiniBand (IB) is not supported.</span></span> <span data-ttu-id="b2b21-130">Tylko RDMA over IB jest obsługiwana.</span><span class="sxs-lookup"><span data-stu-id="b2b21-130">Only RDMA over IB is supported.</span></span>

## <a name="using-hpc-pack"></a><span data-ttu-id="b2b21-131">Przy użyciu pakietu HPC</span><span class="sxs-lookup"><span data-stu-id="b2b21-131">Using HPC Pack</span></span>
<span data-ttu-id="b2b21-132">[HPC Pack](https://technet.microsoft.com/library/jj899572.aspx), rozwiązania firmy Microsoft wolnego HPC klastra i zadania zarządzania, jest jedną z opcji można instancji obliczeniowych hello toouse z systemem Linux.</span><span class="sxs-lookup"><span data-stu-id="b2b21-132">[HPC Pack](https://technet.microsoft.com/library/jj899572.aspx), Microsoft’s free HPC cluster and job management solution, is one option for you toouse hello compute-intensive instances with Linux.</span></span> <span data-ttu-id="b2b21-133">najnowsze wersje Hello HPC Pack obsługuje kilka dystrybucje systemu Linux toorun na obliczeniowe węzłów wdrożone w maszynach wirtualnych platformy Azure, zarządzane przez system Windows Server węzła głównego.</span><span class="sxs-lookup"><span data-stu-id="b2b21-133">hello latest releases of HPC Pack support several Linux distributions toorun on compute nodes deployed in Azure VMs, managed by a Windows Server head node.</span></span> <span data-ttu-id="b2b21-134">Z systemem Intel MPI węzły obliczeniowe Linux z funkcją RDMA HPC Pack można zaplanować i uruchamianie aplikacji Linux MPI RDMA hello dostępu do sieci.</span><span class="sxs-lookup"><span data-stu-id="b2b21-134">With RDMA-capable Linux compute nodes running Intel MPI, HPC Pack can schedule and run Linux MPI applications that access hello RDMA network.</span></span> <span data-ttu-id="b2b21-135">Zobacz [wprowadzenie węzły obliczeniowe systemu Linux w klastrze HPC Pack na platformie Azure](classic/hpcpack-cluster.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="b2b21-135">See [Get started with Linux compute nodes in an HPC Pack cluster in Azure](classic/hpcpack-cluster.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).</span></span>

## <a name="other-sizes"></a><span data-ttu-id="b2b21-136">Innych rozmiarach</span><span class="sxs-lookup"><span data-stu-id="b2b21-136">Other sizes</span></span>
- [<span data-ttu-id="b2b21-137">Zastosowania ogólne</span><span class="sxs-lookup"><span data-stu-id="b2b21-137">General purpose</span></span>](sizes-general.md)
- [<span data-ttu-id="b2b21-138">Optymalizacja pod kątem obliczeń</span><span class="sxs-lookup"><span data-stu-id="b2b21-138">Compute optimized</span></span>](sizes-compute.md)
- [<span data-ttu-id="b2b21-139">Optymalizacja pod kątem pamięci</span><span class="sxs-lookup"><span data-stu-id="b2b21-139">Memory optimized</span></span>](sizes-memory.md)
- [<span data-ttu-id="b2b21-140">Optymalizacja pod kątem magazynu</span><span class="sxs-lookup"><span data-stu-id="b2b21-140">Storage optimized</span></span>](sizes-storage.md)
- [<span data-ttu-id="b2b21-141">Procesor GPU</span><span class="sxs-lookup"><span data-stu-id="b2b21-141">GPU</span></span>](../windows/sizes-gpu.md)


## <a name="next-steps"></a><span data-ttu-id="b2b21-142">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="b2b21-142">Next steps</span></span>

- <span data-ttu-id="b2b21-143">Zobacz tooget uruchomiono wdrażanie i z protokołem RDMA w systemie Linux przy użyciu obliczeniowych rozmiary [skonfigurowanie aplikacji MPI Linux RDMA klastra toorun](classic/rdma-cluster.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="b2b21-143">tooget started deploying and using compute-intensive sizes with RDMA on Linux, see [Set up a Linux RDMA cluster toorun MPI applications](classic/rdma-cluster.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).</span></span>

- <span data-ttu-id="b2b21-144">Dowiedz się więcej na temat [jednostki (ACU) rozwiązań usługi obliczenia Azure](acu.md) ułatwia porównanie wydajności obliczeniowej różnych jednostki SKU Azure.</span><span class="sxs-lookup"><span data-stu-id="b2b21-144">Learn more about how [Azure compute units (ACU)](acu.md) can help you compare compute performance across Azure SKUs.</span></span>




