---
title: O obliczeniowych maszyn wirtualnych w systemie Linux | Dokumentacja firmy Microsoft
description: "Pobierz informacje i zagadnienia dotyczące dla maszyn wirtualnych systemu Linux przy użyciu obliczeniowych rozmiary serii H i A8, A9 A10 i A11"
services: virtual-machines-linux
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: azure-resource-manager,azure-service-management
ms.assetid: 16cf6e2d-f401-4b22-af8c-9a337179f5f6
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 03/14/2017
ms.author: danlep
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: a2307f7055966ec7146b5da0b4daf1ad469abe2b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="about-h-series-and-compute-intensive-a-series-vms-for-linux"></a><span data-ttu-id="39363-103">O H serii i obliczeniowych maszyn wirtualnych A-series dla systemu Linux</span><span class="sxs-lookup"><span data-stu-id="39363-103">About H-series and compute-intensive A-series VMs for Linux</span></span>
<span data-ttu-id="39363-104">Poniżej przedstawiono ogólne informacje oraz pewne zagadnienia dotyczące korzystania z nowszej H-series Azure i wcześniejszych rozmiary A8, A9 A10 i A11, znanej także jako *obliczeniowych* wystąpień.</span><span class="sxs-lookup"><span data-stu-id="39363-104">Here is background information and some considerations for using the newer Azure H-series and the earlier A8, A9, A10, and A11 sizes, also known as *compute-intensive* instances.</span></span> <span data-ttu-id="39363-105">Ten artykuł skupia się na temat używania rozmiary maszyn wirtualnych systemu Linux.</span><span class="sxs-lookup"><span data-stu-id="39363-105">This article focuses on using these sizes for Linux VMs.</span></span> <span data-ttu-id="39363-106">Można również użyć go do [maszyn wirtualnych systemu Windows](../windows/a8-a9-a10-a11-specs.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="39363-106">You can also use them for [Windows VMs](../windows/a8-a9-a10-a11-specs.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> 

<span data-ttu-id="39363-107">Dla podstawowych specyfikacji, pojemności magazynu i dysku szczegółów, zobacz [rozmiary maszyn wirtualnych](sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="39363-107">For basic specs, storage capacities, and disk details, see [Sizes for virtual machines](sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

[!INCLUDE [virtual-machines-common-a8-a9-a10-a11-specs](../../../includes/virtual-machines-common-a8-a9-a10-a11-specs.md)]

## <a name="access-to-the-rdma-network"></a><span data-ttu-id="39363-108">Dostęp do sieci RDMA</span><span class="sxs-lookup"><span data-stu-id="39363-108">Access to the RDMA network</span></span>
<span data-ttu-id="39363-109">Możesz utworzyć klastry z funkcją RDMA maszyn wirtualnych systemu Linux, że uruchom jeden z następujących obsługiwane dystrybucje systemu Linux HPC i obsługiwanych implementacji MPI, aby móc korzystać z sieci Azure RDMA.</span><span class="sxs-lookup"><span data-stu-id="39363-109">You can create clusters of RDMA-capable Linux VMs that run one of the following supported Linux HPC distributions and a supported MPI implementation to take advantage of the Azure RDMA network.</span></span> <span data-ttu-id="39363-110">Zobacz [Konfigurowanie klastra Linux RDMA na uruchamianie aplikacji MPI](classic/rdma-cluster.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json) opcje wdrażania i przykładowe czynności konfiguracyjne.</span><span class="sxs-lookup"><span data-stu-id="39363-110">See [Set up a Linux RDMA cluster to run MPI applications](classic/rdma-cluster.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json) for deployment options and sample configuration steps.</span></span>

* <span data-ttu-id="39363-111">**Dystrybucje** — należy wdrożyć maszyn wirtualnych z funkcją RDMA SUSE Linux Enterprise Server (SLES) lub nieautoryzowanego oprogramowania Wave (dawniej OpenLogic) na podstawie CentOS HPC obrazów w portalu Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="39363-111">**Distributions** - You must deploy VMs from RDMA-capable SUSE Linux Enterprise Server (SLES) or Rogue Wave Software (formerly OpenLogic) CentOS-based HPC images in the Azure Marketplace.</span></span> <span data-ttu-id="39363-112">Na poniższych ilustracjach Marketplace obsługi połączeń RDMA:</span><span class="sxs-lookup"><span data-stu-id="39363-112">The following Marketplace images support RDMA connectivity:</span></span>
  
    * <span data-ttu-id="39363-113">SLES 12 SP1 w przypadku HPC, SLES 12 SP1 w przypadku HPC (Premium)</span><span class="sxs-lookup"><span data-stu-id="39363-113">SLES 12 SP1 for HPC, SLES 12 SP1 for HPC (Premium)</span></span>
    
    * <span data-ttu-id="39363-114">Na podstawie centOS 7.1 HPC, na podstawie CentOS HPC 6.5</span><span class="sxs-lookup"><span data-stu-id="39363-114">CentOS-based 7.1 HPC, CentOS-based 6.5 HPC</span></span>  
 
        > [!NOTE]
        > <span data-ttu-id="39363-115">Dla maszyn wirtualnych, H-series firma Microsoft zaleca SLES 12 SP1 obrazu HPC albo CentOS 7.1 HPC obrazu.</span><span class="sxs-lookup"><span data-stu-id="39363-115">For H-series VMs, we recommend either a SLES 12 SP1 for HPC image or CentOS-based 7.1 HPC image.</span></span>
        >
        > <span data-ttu-id="39363-116">Na obrazach na podstawie CentOS HPC aktualizacji jądra są wyłączone w **yum** pliku konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="39363-116">On the CentOS-based HPC images, kernel updates are disabled in the **yum** configuration file.</span></span> <span data-ttu-id="39363-117">To dlatego sterowniki Linux RDMA są dystrybuowane jako pakiet RPM, a aktualizacje sterowników może nie działać w przypadku jądra jest aktualizowany.</span><span class="sxs-lookup"><span data-stu-id="39363-117">This is because the Linux RDMA drivers are distributed as an RPM package, and driver updates might not work if the kernel is updated.</span></span>
        > 
        > 
* <span data-ttu-id="39363-118">**MPI** — Biblioteka MPI Intel 5.x</span><span class="sxs-lookup"><span data-stu-id="39363-118">**MPI** - Intel MPI Library 5.x</span></span>
  
    <span data-ttu-id="39363-119">W zależności od obrazu z witryny Marketplace można wybrać, oddzielnej licencji, instalacji, albo konfiguracji Intel MPI mogą być potrzebne w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="39363-119">Depending on the Marketplace image you choose, separate licensing, installation, or configuration of Intel MPI may be needed, as follows:</span></span> 
  
  * <span data-ttu-id="39363-120">**SLES 12 SP1 obrazu HPC** -Intel MPI pakiety są dystrybuowane na maszynie Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="39363-120">**SLES 12 SP1 for HPC image** - Intel MPI packages are distributed on the VM.</span></span> <span data-ttu-id="39363-121">Zainstaluj, uruchamiając następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="39363-121">Install by running the following command:</span></span>

      ```bash
      sudo rpm -v -i --nodeps /opt/intelMPI/intel_mpi_packages/*.rpm
      ```

  * <span data-ttu-id="39363-122">**Na podstawie centOS obrazów HPC** -Intel MPI 5.1 jest już zainstalowana.</span><span class="sxs-lookup"><span data-stu-id="39363-122">**CentOS-based HPC images**  - Intel MPI 5.1 is already installed.</span></span>  
    
    <span data-ttu-id="39363-123">Dodatkowy system konfiguracji jest wymagany do uruchomienia zadań MPI na klastrowanych maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="39363-123">Additional system configuration is needed to run MPI jobs on clustered VMs.</span></span> <span data-ttu-id="39363-124">Na przykład w klastrze maszyn wirtualnych, należy ustanowić relację zaufania między węzły obliczeniowe.</span><span class="sxs-lookup"><span data-stu-id="39363-124">For example, on a cluster of VMs, you need to establish trust among the compute nodes.</span></span> <span data-ttu-id="39363-125">W przypadku typowych ustawień, zobacz [Konfigurowanie klastra Linux RDMA na uruchamianie aplikacji MPI](classic/rdma-cluster.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="39363-125">For typical settings, see [Set up a Linux RDMA cluster to run MPI applications](classic/rdma-cluster.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).</span></span>

## <a name="considerations-for-hpc-pack-and-linux"></a><span data-ttu-id="39363-126">Zagadnienia dotyczące HPC Pack i Linux</span><span class="sxs-lookup"><span data-stu-id="39363-126">Considerations for HPC Pack and Linux</span></span>
<span data-ttu-id="39363-127">[HPC Pack](https://technet.microsoft.com/library/jj899572.aspx), rozwiązania firmy Microsoft wolnego HPC klastra i zadania zarządzania, zawiera jedną z opcji można użyć wystąpienia obliczeniowych w systemie Linux.</span><span class="sxs-lookup"><span data-stu-id="39363-127">[HPC Pack](https://technet.microsoft.com/library/jj899572.aspx), Microsoft’s free HPC cluster and job management solution, provides one option for you to use the compute-intensive instances with Linux.</span></span> <span data-ttu-id="39363-128">Najnowsze wersje Obsługa HPC Pack kilka dystrybucje systemu Linux na obliczeniowe węzłów wdrożone w maszynach wirtualnych platformy Azure, zarządzane przez system Windows Server węzła głównego.</span><span class="sxs-lookup"><span data-stu-id="39363-128">The latest releases of HPC Pack support several Linux distributions to run on compute nodes deployed in Azure VMs, managed by a Windows Server head node.</span></span> <span data-ttu-id="39363-129">Węzły obliczeniowe z funkcją RDMA Linux uruchomiony MPI firmy Intel HPC Pack można zaplanować i uruchamiać aplikacje, które uzyskują dostęp do sieci RDMA MPI systemu Linux.</span><span class="sxs-lookup"><span data-stu-id="39363-129">With RDMA-capable Linux compute nodes running Intel MPI, HPC Pack can schedule and run Linux MPI applications that access the RDMA network.</span></span> <span data-ttu-id="39363-130">Aby rozpocząć, zobacz [wprowadzenie węzły obliczeniowe systemu Linux w klastrze HPC Pack na platformie Azure](classic/hpcpack-cluster.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="39363-130">To get started, see [Get started with Linux compute nodes in an HPC Pack cluster in Azure](classic/hpcpack-cluster.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).</span></span>

## <a name="network-topology-considerations"></a><span data-ttu-id="39363-131">Zagadnienia dotyczące topologii sieci</span><span class="sxs-lookup"><span data-stu-id="39363-131">Network topology considerations</span></span>
* <span data-ttu-id="39363-132">W przypadku komputerów z obsługą RDMA maszyn wirtualnych systemu Linux na platformie Azure Eth1 jest zarezerwowana dla ruchu sieciowego RDMA.</span><span class="sxs-lookup"><span data-stu-id="39363-132">On RDMA-enabled Linux VMs in Azure, Eth1 is reserved for RDMA network traffic.</span></span> <span data-ttu-id="39363-133">Nie należy zmieniać ustawienia Eth1 lub wszelkie informacje zawarte w pliku konfiguracji odnoszące się do tej sieci.</span><span class="sxs-lookup"><span data-stu-id="39363-133">Do not change any Eth1 settings or any information in the configuration file referring to this network.</span></span> <span data-ttu-id="39363-134">Eth0 jest zarezerwowana dla regularnych Azure ruchu sieciowego.</span><span class="sxs-lookup"><span data-stu-id="39363-134">Eth0 is reserved for regular Azure network traffic.</span></span>
* <span data-ttu-id="39363-135">IP przez InfiniBand (IB) nie jest obsługiwana na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="39363-135">In Azure, IP over InfiniBand (IB) is not supported.</span></span> <span data-ttu-id="39363-136">Tylko RDMA over IB jest obsługiwana.</span><span class="sxs-lookup"><span data-stu-id="39363-136">Only RDMA over IB is supported.</span></span>



## <a name="next-steps"></a><span data-ttu-id="39363-137">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="39363-137">Next steps</span></span>
* <span data-ttu-id="39363-138">Aby uzyskać szczegółowe informacje o dostępności i cenach rozmiarów obliczeniowych, zobacz [cennik maszyn wirtualnych](https://azure.microsoft.com/pricing/details/virtual-machines/#Linux).</span><span class="sxs-lookup"><span data-stu-id="39363-138">For details about availability and pricing of the compute-intensive sizes, see [Virtual Machines pricing](https://azure.microsoft.com/pricing/details/virtual-machines/#Linux).</span></span>
* <span data-ttu-id="39363-139">Uzyskać wielkości magazynu i dysku szczegółowe informacje, zobacz [rozmiary maszyn wirtualnych](sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="39363-139">For storage capacities and disk details, see [Sizes for virtual machines](sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
* <span data-ttu-id="39363-140">Aby rozpocząć wdrażanie i z protokołem RDMA w systemie Linux przy użyciu obliczeniowych rozmiarów, zobacz [Konfigurowanie klastra Linux RDMA na uruchamianie aplikacji MPI](classic/rdma-cluster.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="39363-140">To get started deploying and using compute-intensive sizes with RDMA on Linux, see [Set up a Linux RDMA cluster to run MPI applications](classic/rdma-cluster.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).</span></span>

