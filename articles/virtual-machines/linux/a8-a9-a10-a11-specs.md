---
title: aaaAbout obliczeniowych maszyn wirtualnych z systemem Linux | Dokumentacja firmy Microsoft
description: "Pobierz informacje i zagadnień dotyczących używania hello H serii i A8, A9 A10 i A11 obliczeniowych rozmiary maszyn wirtualnych systemu Linux"
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
ms.openlocfilehash: 37636840a3f809ac19354a5a7993257216f675f6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="about-h-series-and-compute-intensive-a-series-vms-for-linux"></a><span data-ttu-id="51c6d-103">O H serii i obliczeniowych maszyn wirtualnych A-series dla systemu Linux</span><span class="sxs-lookup"><span data-stu-id="51c6d-103">About H-series and compute-intensive A-series VMs for Linux</span></span>
<span data-ttu-id="51c6d-104">Poniżej przedstawiono ogólne informacje i kilka kwestii dotyczących przy użyciu hello nowszej serii Azure H i hello wcześniejszych rozmiary A8, A9 A10 i A11, znanej także jako *obliczeniowych* wystąpień.</span><span class="sxs-lookup"><span data-stu-id="51c6d-104">Here is background information and some considerations for using hello newer Azure H-series and hello earlier A8, A9, A10, and A11 sizes, also known as *compute-intensive* instances.</span></span> <span data-ttu-id="51c6d-105">Ten artykuł skupia się na temat używania rozmiary maszyn wirtualnych systemu Linux.</span><span class="sxs-lookup"><span data-stu-id="51c6d-105">This article focuses on using these sizes for Linux VMs.</span></span> <span data-ttu-id="51c6d-106">Można również użyć go do [maszyn wirtualnych systemu Windows](../windows/a8-a9-a10-a11-specs.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="51c6d-106">You can also use them for [Windows VMs](../windows/a8-a9-a10-a11-specs.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> 

<span data-ttu-id="51c6d-107">Dla podstawowych specyfikacji, pojemności magazynu i dysku szczegółów, zobacz [rozmiary maszyn wirtualnych](sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="51c6d-107">For basic specs, storage capacities, and disk details, see [Sizes for virtual machines](sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

[!INCLUDE [virtual-machines-common-a8-a9-a10-a11-specs](../../../includes/virtual-machines-common-a8-a9-a10-a11-specs.md)]

## <a name="access-toohello-rdma-network"></a><span data-ttu-id="51c6d-108">Sieć RDMA toohello dostępu</span><span class="sxs-lookup"><span data-stu-id="51c6d-108">Access toohello RDMA network</span></span>
<span data-ttu-id="51c6d-109">Można utworzyć klastry z funkcją RDMA Uruchom jedno z hello obsługiwane dystrybucje systemu Linux HPC i obsługiwanych MPI implementacji tootake zalety hello Azure RDMA sieci maszyn wirtualnych w systemie Linux.</span><span class="sxs-lookup"><span data-stu-id="51c6d-109">You can create clusters of RDMA-capable Linux VMs that run one of hello following supported Linux HPC distributions and a supported MPI implementation tootake advantage of hello Azure RDMA network.</span></span> <span data-ttu-id="51c6d-110">Zobacz [skonfigurowanie aplikacji MPI Linux RDMA klastra toorun](classic/rdma-cluster.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json) opcje wdrażania i przykładowe czynności konfiguracyjne.</span><span class="sxs-lookup"><span data-stu-id="51c6d-110">See [Set up a Linux RDMA cluster toorun MPI applications](classic/rdma-cluster.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json) for deployment options and sample configuration steps.</span></span>

* <span data-ttu-id="51c6d-111">**Dystrybucje** — należy wdrożyć maszyn wirtualnych z funkcją RDMA SUSE Linux Enterprise Server (SLES) lub obrazów nieautoryzowanego oprogramowania Wave (dawniej OpenLogic) na podstawie CentOS HPC w hello Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="51c6d-111">**Distributions** - You must deploy VMs from RDMA-capable SUSE Linux Enterprise Server (SLES) or Rogue Wave Software (formerly OpenLogic) CentOS-based HPC images in hello Azure Marketplace.</span></span> <span data-ttu-id="51c6d-112">Witaj następujące obrazy Marketplace obsługi funkcji RDMA połączeń:</span><span class="sxs-lookup"><span data-stu-id="51c6d-112">hello following Marketplace images support RDMA connectivity:</span></span>
  
    * <span data-ttu-id="51c6d-113">SLES 12 SP1 w przypadku HPC, SLES 12 SP1 w przypadku HPC (Premium)</span><span class="sxs-lookup"><span data-stu-id="51c6d-113">SLES 12 SP1 for HPC, SLES 12 SP1 for HPC (Premium)</span></span>
    
    * <span data-ttu-id="51c6d-114">Na podstawie centOS 7.1 HPC, na podstawie CentOS HPC 6.5</span><span class="sxs-lookup"><span data-stu-id="51c6d-114">CentOS-based 7.1 HPC, CentOS-based 6.5 HPC</span></span>  
 
        > [!NOTE]
        > <span data-ttu-id="51c6d-115">Dla maszyn wirtualnych, H-series firma Microsoft zaleca SLES 12 SP1 obrazu HPC albo CentOS 7.1 HPC obrazu.</span><span class="sxs-lookup"><span data-stu-id="51c6d-115">For H-series VMs, we recommend either a SLES 12 SP1 for HPC image or CentOS-based 7.1 HPC image.</span></span>
        >
        > <span data-ttu-id="51c6d-116">Na obrazach na podstawie CentOS HPC hello, aktualizacji jądra są wyłączone w hello **yum** pliku konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="51c6d-116">On hello CentOS-based HPC images, kernel updates are disabled in hello **yum** configuration file.</span></span> <span data-ttu-id="51c6d-117">To dlatego hello Linux RDMA sterowniki są dystrybuowane jako pakiet RPM, a aktualizacje sterowników może nie działać w przypadku jądra hello jest aktualizowany.</span><span class="sxs-lookup"><span data-stu-id="51c6d-117">This is because hello Linux RDMA drivers are distributed as an RPM package, and driver updates might not work if hello kernel is updated.</span></span>
        > 
        > 
* <span data-ttu-id="51c6d-118">**MPI** — Biblioteka MPI Intel 5.x</span><span class="sxs-lookup"><span data-stu-id="51c6d-118">**MPI** - Intel MPI Library 5.x</span></span>
  
    <span data-ttu-id="51c6d-119">W zależności od obrazu z witryny Marketplace hello można wybrać, oddzielnej licencji, instalacji, albo konfiguracji Intel MPI mogą być potrzebne w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="51c6d-119">Depending on hello Marketplace image you choose, separate licensing, installation, or configuration of Intel MPI may be needed, as follows:</span></span> 
  
  * <span data-ttu-id="51c6d-120">**SLES 12 SP1 obrazu HPC** -Intel MPI pakiety są dystrybuowane na powitania maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="51c6d-120">**SLES 12 SP1 for HPC image** - Intel MPI packages are distributed on hello VM.</span></span> <span data-ttu-id="51c6d-121">Zainstalować, uruchamiając następujące polecenie hello:</span><span class="sxs-lookup"><span data-stu-id="51c6d-121">Install by running hello following command:</span></span>

      ```bash
      sudo rpm -v -i --nodeps /opt/intelMPI/intel_mpi_packages/*.rpm
      ```

  * <span data-ttu-id="51c6d-122">**Na podstawie centOS obrazów HPC** -Intel MPI 5.1 jest już zainstalowana.</span><span class="sxs-lookup"><span data-stu-id="51c6d-122">**CentOS-based HPC images**  - Intel MPI 5.1 is already installed.</span></span>  
    
    <span data-ttu-id="51c6d-123">Konfiguracja dodatkowych systemu jest wymagane toorun zadań MPI w klastrowanych maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="51c6d-123">Additional system configuration is needed toorun MPI jobs on clustered VMs.</span></span> <span data-ttu-id="51c6d-124">Na przykład w klastrze maszyn wirtualnych, należy tooestablish relacji zaufania między hello węzły obliczeniowe.</span><span class="sxs-lookup"><span data-stu-id="51c6d-124">For example, on a cluster of VMs, you need tooestablish trust among hello compute nodes.</span></span> <span data-ttu-id="51c6d-125">W przypadku typowych ustawień, zobacz [skonfigurowanie aplikacji MPI Linux RDMA klastra toorun](classic/rdma-cluster.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="51c6d-125">For typical settings, see [Set up a Linux RDMA cluster toorun MPI applications](classic/rdma-cluster.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).</span></span>

## <a name="considerations-for-hpc-pack-and-linux"></a><span data-ttu-id="51c6d-126">Zagadnienia dotyczące HPC Pack i Linux</span><span class="sxs-lookup"><span data-stu-id="51c6d-126">Considerations for HPC Pack and Linux</span></span>
<span data-ttu-id="51c6d-127">[HPC Pack](https://technet.microsoft.com/library/jj899572.aspx), rozwiązania firmy Microsoft wolnego HPC klastra i zadania zarządzania, zawiera jedną opcję toouse hello obliczeniowych wystąpień z systemem Linux.</span><span class="sxs-lookup"><span data-stu-id="51c6d-127">[HPC Pack](https://technet.microsoft.com/library/jj899572.aspx), Microsoft’s free HPC cluster and job management solution, provides one option for you toouse hello compute-intensive instances with Linux.</span></span> <span data-ttu-id="51c6d-128">najnowsze wersje Hello HPC Pack obsługuje kilka dystrybucje systemu Linux toorun na obliczeniowe węzłów wdrożone w maszynach wirtualnych platformy Azure, zarządzane przez system Windows Server węzła głównego.</span><span class="sxs-lookup"><span data-stu-id="51c6d-128">hello latest releases of HPC Pack support several Linux distributions toorun on compute nodes deployed in Azure VMs, managed by a Windows Server head node.</span></span> <span data-ttu-id="51c6d-129">Z systemem Intel MPI węzły obliczeniowe Linux z funkcją RDMA HPC Pack można zaplanować i uruchamianie aplikacji Linux MPI RDMA hello dostępu do sieci.</span><span class="sxs-lookup"><span data-stu-id="51c6d-129">With RDMA-capable Linux compute nodes running Intel MPI, HPC Pack can schedule and run Linux MPI applications that access hello RDMA network.</span></span> <span data-ttu-id="51c6d-130">Zobacz tooget pracę, [wprowadzenie węzły obliczeniowe systemu Linux w klastrze HPC Pack na platformie Azure](classic/hpcpack-cluster.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="51c6d-130">tooget started, see [Get started with Linux compute nodes in an HPC Pack cluster in Azure](classic/hpcpack-cluster.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).</span></span>

## <a name="network-topology-considerations"></a><span data-ttu-id="51c6d-131">Zagadnienia dotyczące topologii sieci</span><span class="sxs-lookup"><span data-stu-id="51c6d-131">Network topology considerations</span></span>
* <span data-ttu-id="51c6d-132">W przypadku komputerów z obsługą RDMA maszyn wirtualnych systemu Linux na platformie Azure Eth1 jest zarezerwowana dla ruchu sieciowego RDMA.</span><span class="sxs-lookup"><span data-stu-id="51c6d-132">On RDMA-enabled Linux VMs in Azure, Eth1 is reserved for RDMA network traffic.</span></span> <span data-ttu-id="51c6d-133">Nie należy zmieniać ustawienia Eth1 lub wszelkie informacje zawarte w pliku konfiguracji hello odwołujących się toothis sieci.</span><span class="sxs-lookup"><span data-stu-id="51c6d-133">Do not change any Eth1 settings or any information in hello configuration file referring toothis network.</span></span> <span data-ttu-id="51c6d-134">Eth0 jest zarezerwowana dla regularnych Azure ruchu sieciowego.</span><span class="sxs-lookup"><span data-stu-id="51c6d-134">Eth0 is reserved for regular Azure network traffic.</span></span>
* <span data-ttu-id="51c6d-135">IP przez InfiniBand (IB) nie jest obsługiwana na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="51c6d-135">In Azure, IP over InfiniBand (IB) is not supported.</span></span> <span data-ttu-id="51c6d-136">Tylko RDMA over IB jest obsługiwana.</span><span class="sxs-lookup"><span data-stu-id="51c6d-136">Only RDMA over IB is supported.</span></span>



## <a name="next-steps"></a><span data-ttu-id="51c6d-137">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="51c6d-137">Next steps</span></span>
* <span data-ttu-id="51c6d-138">Aby uzyskać szczegółowe informacje o dostępności i cenach hello obliczeniowych rozmiarów, zobacz [cennik maszyn wirtualnych](https://azure.microsoft.com/pricing/details/virtual-machines/#Linux).</span><span class="sxs-lookup"><span data-stu-id="51c6d-138">For details about availability and pricing of hello compute-intensive sizes, see [Virtual Machines pricing](https://azure.microsoft.com/pricing/details/virtual-machines/#Linux).</span></span>
* <span data-ttu-id="51c6d-139">Uzyskać wielkości magazynu i dysku szczegółowe informacje, zobacz [rozmiary maszyn wirtualnych](sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="51c6d-139">For storage capacities and disk details, see [Sizes for virtual machines](sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
* <span data-ttu-id="51c6d-140">Zobacz tooget uruchomiono wdrażanie i z protokołem RDMA w systemie Linux przy użyciu obliczeniowych rozmiary [skonfigurowanie aplikacji MPI Linux RDMA klastra toorun](classic/rdma-cluster.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="51c6d-140">tooget started deploying and using compute-intensive sizes with RDMA on Linux, see [Set up a Linux RDMA cluster toorun MPI applications](classic/rdma-cluster.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).</span></span>

