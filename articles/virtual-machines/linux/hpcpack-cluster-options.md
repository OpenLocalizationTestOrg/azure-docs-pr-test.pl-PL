---
title: Opcje klastra HPC Pack aaaLinux w chmurze hello | Dokumentacja firmy Microsoft
description: "Więcej informacji na temat opcji toocreate Microsoft HPC Pack i zarządzanie nimi Linux wysokiej wydajności (HPC) klastra w hello Azure cloud przetwarzanie"
services: virtual-machines-linux,cloud-services
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: azure-resource-manager,azure-service-management,hpc-pack
ms.assetid: ac60624e-aefa-40c3-8bc1-ef6d5c0ef1a2
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: big-compute
ms.date: 02/06/2017
ms.author: danlep
ms.openlocfilehash: 60d093b466f44a0391815842c421c328e8c7a0d8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="options-with-hpc-pack-toocreate-and-manage-an-hpc-cluster-in-azure-for-linux-workloads"></a><span data-ttu-id="96ada-103">Opcji za pomocą toocreate HPC Pack i zarządzanie nimi klastra HPC dla obciążeń systemu Linux na platformie Azure</span><span class="sxs-lookup"><span data-stu-id="96ada-103">Options with HPC Pack toocreate and manage an HPC cluster in Azure for Linux workloads</span></span>
[!INCLUDE [virtual-machines-common-hpcpack-cluster-options](../../../includes/virtual-machines-common-hpcpack-cluster-options.md)]

<span data-ttu-id="96ada-104">Ten artykuł skupia się na opcje toouse HPC Pack toorun Linux obciążeń.</span><span class="sxs-lookup"><span data-stu-id="96ada-104">This article focuses on options toouse HPC Pack toorun Linux workloads.</span></span> <span data-ttu-id="96ada-105">Dostępne są także opcje do uruchomienia [obciążeń HPC systemu Windows z pakietem HPC](../windows/hpcpack-cluster-options.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="96ada-105">There are also options for running [Windows HPC workloads with HPC Pack](../windows/hpcpack-cluster-options.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

## <a name="run-an-hpc-pack-cluster-in-azure-vms"></a><span data-ttu-id="96ada-106">Uruchomienie klastra HPC Pack w maszynach wirtualnych platformy Azure</span><span class="sxs-lookup"><span data-stu-id="96ada-106">Run an HPC Pack cluster in Azure VMs</span></span>
### <a name="azure-templates"></a><span data-ttu-id="96ada-107">Szablony platformy Azure</span><span class="sxs-lookup"><span data-stu-id="96ada-107">Azure templates</span></span>
* <span data-ttu-id="96ada-108">(GitHub) [Szablony klastra HPC Pack 2016](https://github.com/MsHpcPack/HPCPack2016)</span><span class="sxs-lookup"><span data-stu-id="96ada-108">(GitHub) [HPC Pack 2016 cluster templates](https://github.com/MsHpcPack/HPCPack2016)</span></span>
* <span data-ttu-id="96ada-109">(Marketplace) [Klastra HPC Pack dla obciążeń systemu Linux](https://azure.microsoft.com/marketplace/partners/microsofthpc/newclusterlinuxcn/)</span><span class="sxs-lookup"><span data-stu-id="96ada-109">(Marketplace) [HPC Pack cluster for Linux workloads](https://azure.microsoft.com/marketplace/partners/microsofthpc/newclusterlinuxcn/)</span></span>
* <span data-ttu-id="96ada-110">(Szybki Start) [Utwórz klaster HPC z węzłami obliczeniowymi systemu Linux](https://github.com/Azure/azure-quickstart-templates/tree/master/create-hpc-cluster-linux-cn)</span><span class="sxs-lookup"><span data-stu-id="96ada-110">(Quickstart) [Create an HPC cluster with Linux compute nodes](https://github.com/Azure/azure-quickstart-templates/tree/master/create-hpc-cluster-linux-cn)</span></span>

### <a name="powershell-deployment-script"></a><span data-ttu-id="96ada-111">Skrypt wdrażania środowiska PowerShell</span><span class="sxs-lookup"><span data-stu-id="96ada-111">PowerShell deployment script</span></span>
* [<span data-ttu-id="96ada-112">Tworzenie klastra HPC systemu Linux z hello skrypt wdrożenia HPC Pack IaaS</span><span class="sxs-lookup"><span data-stu-id="96ada-112">Create a Linux HPC cluster with hello HPC Pack IaaS deployment script</span></span>](../windows/classic/hpcpack-cluster-powershell-script.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)

### <a name="tutorials"></a><span data-ttu-id="96ada-113">Samouczki</span><span class="sxs-lookup"><span data-stu-id="96ada-113">Tutorials</span></span>
* [<span data-ttu-id="96ada-114">Samouczek: Rozpoczynanie pracy z węzłów obliczeniowych systemu Linux w klastrze HPC Pack na platformie Azure</span><span class="sxs-lookup"><span data-stu-id="96ada-114">Tutorial: Get started with Linux compute nodes in an HPC Pack cluster in Azure</span></span>](classic/hpcpack-cluster.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)
* [<span data-ttu-id="96ada-115">Samouczek: Uruchom NAMD z pakietem Microsoft HPC w systemie Linux obliczeniowe węzłów na platformie Azure</span><span class="sxs-lookup"><span data-stu-id="96ada-115">Tutorial: Run NAMD with Microsoft HPC Pack on Linux compute nodes in Azure</span></span>](classic/hpcpack-cluster-namd.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)
* [<span data-ttu-id="96ada-116">Samouczek: Uruchom OpenFOAM z pakietem Microsoft HPC w klastrze RDMA systemu Linux na platformie Azure</span><span class="sxs-lookup"><span data-stu-id="96ada-116">Tutorial: Run OpenFOAM with Microsoft HPC Pack on a Linux RDMA cluster in Azure</span></span>](classic/hpcpack-cluster-openfoam.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)
* [<span data-ttu-id="96ada-117">Samouczek: Uruchom GWIAZDKĘ — CCM + z pakietem Microsoft HPC na Linux RDMA klaster na platformie Azure</span><span class="sxs-lookup"><span data-stu-id="96ada-117">Tutorial: Run STAR-CCM+ with Microsoft HPC Pack on a Linux RDMA cluster in Azure</span></span>](classic/hpcpack-cluster-starccm.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)

### <a name="cluster-management"></a><span data-ttu-id="96ada-118">Zarządzanie klastrami</span><span class="sxs-lookup"><span data-stu-id="96ada-118">Cluster management</span></span>
* [<span data-ttu-id="96ada-119">Przedstawia klastra HPC Pack tooan zadania na platformie Azure</span><span class="sxs-lookup"><span data-stu-id="96ada-119">Submit jobs tooan HPC Pack cluster in Azure</span></span>](../windows/hpcpack-cluster-submit-jobs.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [<span data-ttu-id="96ada-120">Zarządzanie zadaniami w pakiecie HPC</span><span class="sxs-lookup"><span data-stu-id="96ada-120">Job management in HPC Pack</span></span>](https://technet.microsoft.com/library/jj899585.aspx)

## <a name="create-rdma-clusters-for-mpi-workloads"></a><span data-ttu-id="96ada-121">Tworzenie klastrów RDMA dla obciążeń MPI</span><span class="sxs-lookup"><span data-stu-id="96ada-121">Create RDMA clusters for MPI workloads</span></span>
* [<span data-ttu-id="96ada-122">Samouczek: Uruchom OpenFOAM z pakietem Microsoft HPC w klastrze RDMA systemu Linux na platformie Azure</span><span class="sxs-lookup"><span data-stu-id="96ada-122">Tutorial: Run OpenFOAM with Microsoft HPC Pack on a Linux RDMA cluster in Azure</span></span>](classic/hpcpack-cluster-openfoam.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)
* [<span data-ttu-id="96ada-123">Skonfiguruj aplikacje MPI toorun Linux RDMA klastra</span><span class="sxs-lookup"><span data-stu-id="96ada-123">Set up a Linux RDMA cluster toorun MPI applications</span></span>](classic/rdma-cluster.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)

