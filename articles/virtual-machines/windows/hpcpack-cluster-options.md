---
title: Opcje klastra systemu Windows HPC Pack w chmurze | Dokumentacja firmy Microsoft
description: "Dowiedz się więcej o opcjach z pakietem Microsoft HPC tworzenie i zarządzanie nimi Windows wysokiej wydajności obliczeniowej klastra (HPC) w chmurze Azure"
services: virtual-machines-windows,cloud-services,batch
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: azure-resource-manager,azure-service-management,hpc-pack
ms.assetid: 02c5566d-2129-483c-9ecf-0d61030442d7
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: big-compute
ms.date: 02/06/2017
ms.author: danlep
ms.openlocfilehash: 96a5520d8440af7d8a880c2675a5d4eb4121e9ab
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="options-with-hpc-pack-to-create-and-manage-a-windows-hpc-cluster-in-azure"></a><span data-ttu-id="5b599-103">Opcje pakietem HPC tworzenie i zarządzanie nimi w klastrze HPC systemu Windows na platformie Azure</span><span class="sxs-lookup"><span data-stu-id="5b599-103">Options with HPC Pack to create and manage a Windows HPC cluster in Azure</span></span>
[!INCLUDE [virtual-machines-common-hpcpack-cluster-options](../../../includes/virtual-machines-common-hpcpack-cluster-options.md)]

<span data-ttu-id="5b599-104">Ten artykuł skupia się na temat opcji do tworzenia klastrów HPC Pack do uruchamiania obciążeń systemu Windows.</span><span class="sxs-lookup"><span data-stu-id="5b599-104">This article focuses on options to create HPC Pack clusters to run Windows workloads.</span></span> <span data-ttu-id="5b599-105">Dostępne są także opcje tworzenia klastrów HPC Pack do uruchomienia [obciążeń HPC systemu Linux](../linux/hpcpack-cluster-options.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="5b599-105">There are also options for creating HPC Pack clusters to run [Linux HPC workloads](../linux/hpcpack-cluster-options.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>


## <a name="run-an-hpc-pack-cluster-in-azure-vms"></a><span data-ttu-id="5b599-106">Uruchomienie klastra HPC Pack w maszynach wirtualnych platformy Azure</span><span class="sxs-lookup"><span data-stu-id="5b599-106">Run an HPC Pack cluster in Azure VMs</span></span>
### <a name="azure-templates"></a><span data-ttu-id="5b599-107">Szablony platformy Azure</span><span class="sxs-lookup"><span data-stu-id="5b599-107">Azure templates</span></span>
* <span data-ttu-id="5b599-108">(GitHub) [Szablony klastra HPC Pack 2016](https://github.com/MsHpcPack/HPCPack2016)</span><span class="sxs-lookup"><span data-stu-id="5b599-108">(GitHub) [HPC Pack 2016 cluster templates](https://github.com/MsHpcPack/HPCPack2016)</span></span>
* <span data-ttu-id="5b599-109">(Marketplace) [Klastra HPC Pack dla obciążeń systemu Windows](https://azure.microsoft.com/marketplace/partners/microsofthpc/newclusterwindowscn/)</span><span class="sxs-lookup"><span data-stu-id="5b599-109">(Marketplace) [HPC Pack cluster for Windows workloads](https://azure.microsoft.com/marketplace/partners/microsofthpc/newclusterwindowscn/)</span></span>
* <span data-ttu-id="5b599-110">(Marketplace) [Klastra HPC Pack dla obciążeń programu Excel](https://azure.microsoft.com/marketplace/partners/microsofthpc/newclusterexcelcn/)</span><span class="sxs-lookup"><span data-stu-id="5b599-110">(Marketplace) [HPC Pack cluster for Excel workloads](https://azure.microsoft.com/marketplace/partners/microsofthpc/newclusterexcelcn/)</span></span>
* <span data-ttu-id="5b599-111">(Szybki Start) [Tworzenia klastra HPC](https://github.com/Azure/azure-quickstart-templates/tree/master/create-hpc-cluster)</span><span class="sxs-lookup"><span data-stu-id="5b599-111">(Quickstart) [Create an HPC cluster](https://github.com/Azure/azure-quickstart-templates/tree/master/create-hpc-cluster)</span></span>
* <span data-ttu-id="5b599-112">(Szybki Start) [Utworzyć klaster HPC z obrazem węzła niestandardowego obliczania](https://github.com/Azure/azure-quickstart-templates/tree/master/create-hpc-cluster-custom-image)</span><span class="sxs-lookup"><span data-stu-id="5b599-112">(Quickstart) [Create an HPC cluster with custom compute node image](https://github.com/Azure/azure-quickstart-templates/tree/master/create-hpc-cluster-custom-image)</span></span>

### <a name="azure-vm-images"></a><span data-ttu-id="5b599-113">Obrazy maszyny Wirtualnej platformy Azure</span><span class="sxs-lookup"><span data-stu-id="5b599-113">Azure VM images</span></span>
* [<span data-ttu-id="5b599-114">Węzłem głównym HPC Pack 2016 w systemie Windows Server 2016</span><span class="sxs-lookup"><span data-stu-id="5b599-114">HPC Pack 2016 head node on Windows Server 2016</span></span>](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/Microsoft.HPCPack2016HeadNodeonWindowsServer2016?tab=Overview)
* [<span data-ttu-id="5b599-115">Węzeł obliczeniowy HPC Pack 2016 w systemie Windows Server 2016</span><span class="sxs-lookup"><span data-stu-id="5b599-115">HPC Pack 2016 compute node on Windows Server 2016</span></span>](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/Microsoft.HPCPack2016ComputeNodeonWindowsServer2016?tab=Overview)
* [<span data-ttu-id="5b599-116">Węzłem głównym HPC Pack 2016 w systemie Windows Server 2012 R2</span><span class="sxs-lookup"><span data-stu-id="5b599-116">HPC Pack 2016 head node on Windows Server 2012 R2</span></span>](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/Microsoft.HPCPack2016HeadNodeonWindowsServer2012R2?tab=Overview)
* [<span data-ttu-id="5b599-117">Węzeł obliczeniowy HPC Pack 2016 w systemie Windows Server 2012 R2</span><span class="sxs-lookup"><span data-stu-id="5b599-117">HPC Pack 2016 compute node on Windows Server 2012 R2</span></span>](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/Microsoft.HPCPack2016ComputeNodeonWindowsServer2012R2?tab=Overview)
* [<span data-ttu-id="5b599-118">Węzłem głównym HPC Pack 2012 R2 w systemie Windows Server 2012 R2</span><span class="sxs-lookup"><span data-stu-id="5b599-118">HPC Pack 2012 R2 head node on Windows Server 2012 R2</span></span>](https://azure.microsoft.com/marketplace/partners/microsoft/hpcpack2012r2onwindowsserver2012r2/)
* [<span data-ttu-id="5b599-119">Węzeł obliczeniowy HPC Pack 2012 R2 w systemie Windows Server 2012 R2</span><span class="sxs-lookup"><span data-stu-id="5b599-119">HPC Pack 2012 R2 compute node on Windows Server 2012 R2</span></span>](https://azure.microsoft.com/marketplace/partners/microsoft/hpcpack2012r2computenodeonwindowsserver2012r2/)
* [<span data-ttu-id="5b599-120">HPC Pack obliczeniowe węzła przy użyciu programu Excel w systemie Windows Server 2012 R2</span><span class="sxs-lookup"><span data-stu-id="5b599-120">HPC Pack compute node with Excel on Windows Server 2012 R2</span></span>](https://azure.microsoft.com/marketplace/partners/microsoft/hpcpack2012r2computenodewithexcelonwindowsserver2012r2/)

### <a name="powershell-deployment-script"></a><span data-ttu-id="5b599-121">Skrypt wdrażania środowiska PowerShell</span><span class="sxs-lookup"><span data-stu-id="5b599-121">PowerShell deployment script</span></span>
* [<span data-ttu-id="5b599-122">Tworzenie klastra HPC z skrypt wdrożenia HPC Pack IaaS</span><span class="sxs-lookup"><span data-stu-id="5b599-122">Create an HPC cluster with the HPC Pack IaaS deployment script</span></span>](classic/hpcpack-cluster-powershell-script.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)

### <a name="tutorials"></a><span data-ttu-id="5b599-123">Samouczki</span><span class="sxs-lookup"><span data-stu-id="5b599-123">Tutorials</span></span>
* [<span data-ttu-id="5b599-124">Samouczek: Wdrażanie klastra HPC Pack 2016 na platformie Azure</span><span class="sxs-lookup"><span data-stu-id="5b599-124">Tutorial: Deploy an HPC Pack 2016 cluster in Azure</span></span>](hpcpack-2016-cluster.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [<span data-ttu-id="5b599-125">Samouczek: Rozpoczynanie pracy z klastra HPC Pack na platformie Azure, aby uruchomić program Excel i SOA obciążeń</span><span class="sxs-lookup"><span data-stu-id="5b599-125">Tutorial: Get started with an HPC Pack cluster in Azure to run Excel and SOA workloads</span></span>](excel-cluster-hpcpack.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

### <a name="manual-deployment-with-the-azure-portal"></a><span data-ttu-id="5b599-126">Ręczne wdrożenie z portalu Azure</span><span class="sxs-lookup"><span data-stu-id="5b599-126">Manual deployment with the Azure portal</span></span>
* [<span data-ttu-id="5b599-127">Konfigurowanie węzła głównego klastra HPC Pack w maszynie Wirtualnej platformy Azure</span><span class="sxs-lookup"><span data-stu-id="5b599-127">Set up the head node of an HPC Pack cluster in an Azure VM</span></span>](hpcpack-cluster-headnode.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

### <a name="cluster-management"></a><span data-ttu-id="5b599-128">Zarządzanie klastrami</span><span class="sxs-lookup"><span data-stu-id="5b599-128">Cluster management</span></span>
* [<span data-ttu-id="5b599-129">Zarządzanie węzłów obliczeniowych w klastrze HPC Pack na platformie Azure</span><span class="sxs-lookup"><span data-stu-id="5b599-129">Manage compute nodes in an HPC Pack cluster in Azure</span></span>](classic/hpcpack-cluster-node-manage.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)
* [<span data-ttu-id="5b599-130">Zwiększyć lub zmniejszyć zasoby obliczeniowe systemu Azure w klastrze HPC Pack</span><span class="sxs-lookup"><span data-stu-id="5b599-130">Grow and shrink Azure compute resources in an HPC Pack cluster</span></span>](classic/hpcpack-cluster-node-autogrowshrink.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)
* [<span data-ttu-id="5b599-131">Przesyłanie zadań do klastra HPC Pack na platformie Azure</span><span class="sxs-lookup"><span data-stu-id="5b599-131">Submit jobs to an HPC Pack cluster in Azure</span></span>](hpcpack-cluster-submit-jobs.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [<span data-ttu-id="5b599-132">Zarządzanie zadaniami w pakiecie HPC</span><span class="sxs-lookup"><span data-stu-id="5b599-132">Job management in HPC Pack</span></span>](https://technet.microsoft.com/library/jj899585.aspx)
* [<span data-ttu-id="5b599-133">Zarządzanie klastra HPC Pack na platformie Azure w usłudze Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="5b599-133">Manage an HPC Pack cluster in Azure with Azure Active Directory</span></span>](hpcpack-cluster-active-directory.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)

## <a name="add-worker-role-nodes-to-an-hpc-pack-cluster"></a><span data-ttu-id="5b599-134">Dodaj węzły roli procesu roboczego w klastrze HPC Pack</span><span class="sxs-lookup"><span data-stu-id="5b599-134">Add worker role nodes to an HPC Pack cluster</span></span>
* [<span data-ttu-id="5b599-135">Serii do wystąpień procesu roboczego platformy Azure z pakietem HPC</span><span class="sxs-lookup"><span data-stu-id="5b599-135">Burst to Azure worker instances with HPC Pack</span></span>](https://technet.microsoft.com/library/gg481749.aspx)
* [<span data-ttu-id="5b599-136">Samouczek: Konfigurowanie klastra hybrydowego pakietem HPC w systemie Azure</span><span class="sxs-lookup"><span data-stu-id="5b599-136">Tutorial: Set up a hybrid cluster with HPC Pack in Azure</span></span>](../../cloud-services/cloud-services-setup-hybrid-hpcpack-cluster.md)
* [<span data-ttu-id="5b599-137">Dodaj węzły platformy Azure "serii" z węzłem głównym HPC Pack na platformie Azure</span><span class="sxs-lookup"><span data-stu-id="5b599-137">Add Azure "burst" nodes to an HPC Pack head node in Azure</span></span>](classic/hpcpack-cluster-node-burst.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)

## <a name="integrate-with-azure-batch"></a><span data-ttu-id="5b599-138">Integracja z partii zadań Azure</span><span class="sxs-lookup"><span data-stu-id="5b599-138">Integrate with Azure Batch</span></span>
* [<span data-ttu-id="5b599-139">Serii do partii zadań Azure z pakietem HPC</span><span class="sxs-lookup"><span data-stu-id="5b599-139">Burst to Azure Batch with HPC Pack</span></span>](https://technet.microsoft.com/library/mt612877.aspx)

## <a name="create-rdma-clusters-for-mpi-workloads"></a><span data-ttu-id="5b599-140">Tworzenie klastrów RDMA dla obciążeń MPI</span><span class="sxs-lookup"><span data-stu-id="5b599-140">Create RDMA clusters for MPI workloads</span></span>
* [<span data-ttu-id="5b599-141">Konfigurowanie klastra RDMA systemu Windows z pakietem HPC do uruchamiania aplikacji MPI</span><span class="sxs-lookup"><span data-stu-id="5b599-141">Set up a Windows RDMA cluster with HPC Pack to run MPI applications</span></span>](classic/hpcpack-rdma-cluster.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)

