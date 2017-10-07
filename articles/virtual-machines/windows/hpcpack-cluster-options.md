---
title: "Opcje w chmurze hello klastrów HPC Pack aaaWindows | Dokumentacja firmy Microsoft"
description: "Więcej informacji na temat opcji toocreate Microsoft HPC Pack i zarządzanie nimi Windows wysokiej wydajności (HPC) klastra w hello Azure cloud przetwarzanie"
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
ms.openlocfilehash: 6158d9dd0cecda38b14f85a2b2080163f18e8cf8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="options-with-hpc-pack-toocreate-and-manage-a-windows-hpc-cluster-in-azure"></a><span data-ttu-id="cc916-103">Opcji za pomocą toocreate HPC Pack i zarządzanie nimi klastra HPC systemu Windows na platformie Azure</span><span class="sxs-lookup"><span data-stu-id="cc916-103">Options with HPC Pack toocreate and manage a Windows HPC cluster in Azure</span></span>
[!INCLUDE [virtual-machines-common-hpcpack-cluster-options](../../../includes/virtual-machines-common-hpcpack-cluster-options.md)]

<span data-ttu-id="cc916-104">Ten artykuł dotyczy toocreate opcje HPC Pack obciążeń systemu Windows toorun klastrów.</span><span class="sxs-lookup"><span data-stu-id="cc916-104">This article focuses on options toocreate HPC Pack clusters toorun Windows workloads.</span></span> <span data-ttu-id="cc916-105">Dostępne są także opcje tworzenia HPC Pack klastrów toorun [obciążeń HPC systemu Linux](../linux/hpcpack-cluster-options.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="cc916-105">There are also options for creating HPC Pack clusters toorun [Linux HPC workloads](../linux/hpcpack-cluster-options.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>


## <a name="run-an-hpc-pack-cluster-in-azure-vms"></a><span data-ttu-id="cc916-106">Uruchomienie klastra HPC Pack w maszynach wirtualnych platformy Azure</span><span class="sxs-lookup"><span data-stu-id="cc916-106">Run an HPC Pack cluster in Azure VMs</span></span>
### <a name="azure-templates"></a><span data-ttu-id="cc916-107">Szablony platformy Azure</span><span class="sxs-lookup"><span data-stu-id="cc916-107">Azure templates</span></span>
* <span data-ttu-id="cc916-108">(GitHub) [Szablony klastra HPC Pack 2016](https://github.com/MsHpcPack/HPCPack2016)</span><span class="sxs-lookup"><span data-stu-id="cc916-108">(GitHub) [HPC Pack 2016 cluster templates](https://github.com/MsHpcPack/HPCPack2016)</span></span>
* <span data-ttu-id="cc916-109">(Marketplace) [Klastra HPC Pack dla obciążeń systemu Windows](https://azure.microsoft.com/marketplace/partners/microsofthpc/newclusterwindowscn/)</span><span class="sxs-lookup"><span data-stu-id="cc916-109">(Marketplace) [HPC Pack cluster for Windows workloads](https://azure.microsoft.com/marketplace/partners/microsofthpc/newclusterwindowscn/)</span></span>
* <span data-ttu-id="cc916-110">(Marketplace) [Klastra HPC Pack dla obciążeń programu Excel](https://azure.microsoft.com/marketplace/partners/microsofthpc/newclusterexcelcn/)</span><span class="sxs-lookup"><span data-stu-id="cc916-110">(Marketplace) [HPC Pack cluster for Excel workloads](https://azure.microsoft.com/marketplace/partners/microsofthpc/newclusterexcelcn/)</span></span>
* <span data-ttu-id="cc916-111">(Szybki Start) [Tworzenia klastra HPC](https://github.com/Azure/azure-quickstart-templates/tree/master/create-hpc-cluster)</span><span class="sxs-lookup"><span data-stu-id="cc916-111">(Quickstart) [Create an HPC cluster](https://github.com/Azure/azure-quickstart-templates/tree/master/create-hpc-cluster)</span></span>
* <span data-ttu-id="cc916-112">(Szybki Start) [Utworzyć klaster HPC z obrazem węzła niestandardowego obliczania](https://github.com/Azure/azure-quickstart-templates/tree/master/create-hpc-cluster-custom-image)</span><span class="sxs-lookup"><span data-stu-id="cc916-112">(Quickstart) [Create an HPC cluster with custom compute node image](https://github.com/Azure/azure-quickstart-templates/tree/master/create-hpc-cluster-custom-image)</span></span>

### <a name="azure-vm-images"></a><span data-ttu-id="cc916-113">Obrazy maszyny Wirtualnej platformy Azure</span><span class="sxs-lookup"><span data-stu-id="cc916-113">Azure VM images</span></span>
* [<span data-ttu-id="cc916-114">Węzłem głównym HPC Pack 2016 w systemie Windows Server 2016</span><span class="sxs-lookup"><span data-stu-id="cc916-114">HPC Pack 2016 head node on Windows Server 2016</span></span>](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/Microsoft.HPCPack2016HeadNodeonWindowsServer2016?tab=Overview)
* [<span data-ttu-id="cc916-115">Węzeł obliczeniowy HPC Pack 2016 w systemie Windows Server 2016</span><span class="sxs-lookup"><span data-stu-id="cc916-115">HPC Pack 2016 compute node on Windows Server 2016</span></span>](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/Microsoft.HPCPack2016ComputeNodeonWindowsServer2016?tab=Overview)
* [<span data-ttu-id="cc916-116">Węzłem głównym HPC Pack 2016 w systemie Windows Server 2012 R2</span><span class="sxs-lookup"><span data-stu-id="cc916-116">HPC Pack 2016 head node on Windows Server 2012 R2</span></span>](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/Microsoft.HPCPack2016HeadNodeonWindowsServer2012R2?tab=Overview)
* [<span data-ttu-id="cc916-117">Węzeł obliczeniowy HPC Pack 2016 w systemie Windows Server 2012 R2</span><span class="sxs-lookup"><span data-stu-id="cc916-117">HPC Pack 2016 compute node on Windows Server 2012 R2</span></span>](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/Microsoft.HPCPack2016ComputeNodeonWindowsServer2012R2?tab=Overview)
* [<span data-ttu-id="cc916-118">Węzłem głównym HPC Pack 2012 R2 w systemie Windows Server 2012 R2</span><span class="sxs-lookup"><span data-stu-id="cc916-118">HPC Pack 2012 R2 head node on Windows Server 2012 R2</span></span>](https://azure.microsoft.com/marketplace/partners/microsoft/hpcpack2012r2onwindowsserver2012r2/)
* [<span data-ttu-id="cc916-119">Węzeł obliczeniowy HPC Pack 2012 R2 w systemie Windows Server 2012 R2</span><span class="sxs-lookup"><span data-stu-id="cc916-119">HPC Pack 2012 R2 compute node on Windows Server 2012 R2</span></span>](https://azure.microsoft.com/marketplace/partners/microsoft/hpcpack2012r2computenodeonwindowsserver2012r2/)
* [<span data-ttu-id="cc916-120">HPC Pack obliczeniowe węzła przy użyciu programu Excel w systemie Windows Server 2012 R2</span><span class="sxs-lookup"><span data-stu-id="cc916-120">HPC Pack compute node with Excel on Windows Server 2012 R2</span></span>](https://azure.microsoft.com/marketplace/partners/microsoft/hpcpack2012r2computenodewithexcelonwindowsserver2012r2/)

### <a name="powershell-deployment-script"></a><span data-ttu-id="cc916-121">Skrypt wdrażania środowiska PowerShell</span><span class="sxs-lookup"><span data-stu-id="cc916-121">PowerShell deployment script</span></span>
* [<span data-ttu-id="cc916-122">Tworzenie klastra HPC z hello skrypt wdrożenia HPC Pack IaaS</span><span class="sxs-lookup"><span data-stu-id="cc916-122">Create an HPC cluster with hello HPC Pack IaaS deployment script</span></span>](classic/hpcpack-cluster-powershell-script.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)

### <a name="tutorials"></a><span data-ttu-id="cc916-123">Samouczki</span><span class="sxs-lookup"><span data-stu-id="cc916-123">Tutorials</span></span>
* [<span data-ttu-id="cc916-124">Samouczek: Wdrażanie klastra HPC Pack 2016 na platformie Azure</span><span class="sxs-lookup"><span data-stu-id="cc916-124">Tutorial: Deploy an HPC Pack 2016 cluster in Azure</span></span>](hpcpack-2016-cluster.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [<span data-ttu-id="cc916-125">Samouczek: Rozpoczynanie pracy z klastra HPC Pack w Azure toorun programu Excel i obciążeń SOA</span><span class="sxs-lookup"><span data-stu-id="cc916-125">Tutorial: Get started with an HPC Pack cluster in Azure toorun Excel and SOA workloads</span></span>](excel-cluster-hpcpack.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

### <a name="manual-deployment-with-hello-azure-portal"></a><span data-ttu-id="cc916-126">Ręczne wdrożenie z hello portalu Azure</span><span class="sxs-lookup"><span data-stu-id="cc916-126">Manual deployment with hello Azure portal</span></span>
* [<span data-ttu-id="cc916-127">Konfigurowanie hello węzła głównego klastra HPC Pack w maszynie Wirtualnej platformy Azure</span><span class="sxs-lookup"><span data-stu-id="cc916-127">Set up hello head node of an HPC Pack cluster in an Azure VM</span></span>](hpcpack-cluster-headnode.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

### <a name="cluster-management"></a><span data-ttu-id="cc916-128">Zarządzanie klastrami</span><span class="sxs-lookup"><span data-stu-id="cc916-128">Cluster management</span></span>
* [<span data-ttu-id="cc916-129">Zarządzanie węzłów obliczeniowych w klastrze HPC Pack na platformie Azure</span><span class="sxs-lookup"><span data-stu-id="cc916-129">Manage compute nodes in an HPC Pack cluster in Azure</span></span>](classic/hpcpack-cluster-node-manage.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)
* [<span data-ttu-id="cc916-130">Zwiększyć lub zmniejszyć zasoby obliczeniowe systemu Azure w klastrze HPC Pack</span><span class="sxs-lookup"><span data-stu-id="cc916-130">Grow and shrink Azure compute resources in an HPC Pack cluster</span></span>](classic/hpcpack-cluster-node-autogrowshrink.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)
* [<span data-ttu-id="cc916-131">Przedstawia klastra HPC Pack tooan zadania na platformie Azure</span><span class="sxs-lookup"><span data-stu-id="cc916-131">Submit jobs tooan HPC Pack cluster in Azure</span></span>](hpcpack-cluster-submit-jobs.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [<span data-ttu-id="cc916-132">Zarządzanie zadaniami w pakiecie HPC</span><span class="sxs-lookup"><span data-stu-id="cc916-132">Job management in HPC Pack</span></span>](https://technet.microsoft.com/library/jj899585.aspx)
* [<span data-ttu-id="cc916-133">Zarządzanie klastra HPC Pack na platformie Azure w usłudze Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="cc916-133">Manage an HPC Pack cluster in Azure with Azure Active Directory</span></span>](hpcpack-cluster-active-directory.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)

## <a name="add-worker-role-nodes-tooan-hpc-pack-cluster"></a><span data-ttu-id="cc916-134">Dodawanie procesu roboczego roli węzłów tooan HPC Pack klastra</span><span class="sxs-lookup"><span data-stu-id="cc916-134">Add worker role nodes tooan HPC Pack cluster</span></span>
* [<span data-ttu-id="cc916-135">Serii wystąpień procesów roboczych tooAzure pakietem HPC</span><span class="sxs-lookup"><span data-stu-id="cc916-135">Burst tooAzure worker instances with HPC Pack</span></span>](https://technet.microsoft.com/library/gg481749.aspx)
* [<span data-ttu-id="cc916-136">Samouczek: Konfigurowanie klastra hybrydowego pakietem HPC w systemie Azure</span><span class="sxs-lookup"><span data-stu-id="cc916-136">Tutorial: Set up a hybrid cluster with HPC Pack in Azure</span></span>](../../cloud-services/cloud-services-setup-hybrid-hpcpack-cluster.md)
* [<span data-ttu-id="cc916-137">Dodaj Azure "serii" węzłów tooan HPC Pack węzła głównego na platformie Azure</span><span class="sxs-lookup"><span data-stu-id="cc916-137">Add Azure "burst" nodes tooan HPC Pack head node in Azure</span></span>](classic/hpcpack-cluster-node-burst.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)

## <a name="integrate-with-azure-batch"></a><span data-ttu-id="cc916-138">Integracja z partii zadań Azure</span><span class="sxs-lookup"><span data-stu-id="cc916-138">Integrate with Azure Batch</span></span>
* [<span data-ttu-id="cc916-139">TooAzure serii partii z pakietem HPC</span><span class="sxs-lookup"><span data-stu-id="cc916-139">Burst tooAzure Batch with HPC Pack</span></span>](https://technet.microsoft.com/library/mt612877.aspx)

## <a name="create-rdma-clusters-for-mpi-workloads"></a><span data-ttu-id="cc916-140">Tworzenie klastrów RDMA dla obciążeń MPI</span><span class="sxs-lookup"><span data-stu-id="cc916-140">Create RDMA clusters for MPI workloads</span></span>
* [<span data-ttu-id="cc916-141">Konfigurowanie klastra Windows RDMA HPC Pack toorun MPI aplikacji</span><span class="sxs-lookup"><span data-stu-id="cc916-141">Set up a Windows RDMA cluster with HPC Pack toorun MPI applications</span></span>](classic/hpcpack-rdma-cluster.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)

