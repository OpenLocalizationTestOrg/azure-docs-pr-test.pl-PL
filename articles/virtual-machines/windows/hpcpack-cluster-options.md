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
# <a name="options-with-hpc-pack-to-create-and-manage-a-windows-hpc-cluster-in-azure"></a>Opcje pakietem HPC tworzenie i zarządzanie nimi w klastrze HPC systemu Windows na platformie Azure
[!INCLUDE [virtual-machines-common-hpcpack-cluster-options](../../../includes/virtual-machines-common-hpcpack-cluster-options.md)]

Ten artykuł skupia się na temat opcji do tworzenia klastrów HPC Pack do uruchamiania obciążeń systemu Windows. Dostępne są także opcje tworzenia klastrów HPC Pack do uruchomienia [obciążeń HPC systemu Linux](../linux/hpcpack-cluster-options.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).


## <a name="run-an-hpc-pack-cluster-in-azure-vms"></a>Uruchomienie klastra HPC Pack w maszynach wirtualnych platformy Azure
### <a name="azure-templates"></a>Szablony platformy Azure
* (GitHub) [Szablony klastra HPC Pack 2016](https://github.com/MsHpcPack/HPCPack2016)
* (Marketplace) [Klastra HPC Pack dla obciążeń systemu Windows](https://azure.microsoft.com/marketplace/partners/microsofthpc/newclusterwindowscn/)
* (Marketplace) [Klastra HPC Pack dla obciążeń programu Excel](https://azure.microsoft.com/marketplace/partners/microsofthpc/newclusterexcelcn/)
* (Szybki Start) [Tworzenia klastra HPC](https://github.com/Azure/azure-quickstart-templates/tree/master/create-hpc-cluster)
* (Szybki Start) [Utworzyć klaster HPC z obrazem węzła niestandardowego obliczania](https://github.com/Azure/azure-quickstart-templates/tree/master/create-hpc-cluster-custom-image)

### <a name="azure-vm-images"></a>Obrazy maszyny Wirtualnej platformy Azure
* [Węzłem głównym HPC Pack 2016 w systemie Windows Server 2016](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/Microsoft.HPCPack2016HeadNodeonWindowsServer2016?tab=Overview)
* [Węzeł obliczeniowy HPC Pack 2016 w systemie Windows Server 2016](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/Microsoft.HPCPack2016ComputeNodeonWindowsServer2016?tab=Overview)
* [Węzłem głównym HPC Pack 2016 w systemie Windows Server 2012 R2](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/Microsoft.HPCPack2016HeadNodeonWindowsServer2012R2?tab=Overview)
* [Węzeł obliczeniowy HPC Pack 2016 w systemie Windows Server 2012 R2](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/Microsoft.HPCPack2016ComputeNodeonWindowsServer2012R2?tab=Overview)
* [Węzłem głównym HPC Pack 2012 R2 w systemie Windows Server 2012 R2](https://azure.microsoft.com/marketplace/partners/microsoft/hpcpack2012r2onwindowsserver2012r2/)
* [Węzeł obliczeniowy HPC Pack 2012 R2 w systemie Windows Server 2012 R2](https://azure.microsoft.com/marketplace/partners/microsoft/hpcpack2012r2computenodeonwindowsserver2012r2/)
* [HPC Pack obliczeniowe węzła przy użyciu programu Excel w systemie Windows Server 2012 R2](https://azure.microsoft.com/marketplace/partners/microsoft/hpcpack2012r2computenodewithexcelonwindowsserver2012r2/)

### <a name="powershell-deployment-script"></a>Skrypt wdrażania środowiska PowerShell
* [Tworzenie klastra HPC z skrypt wdrożenia HPC Pack IaaS](classic/hpcpack-cluster-powershell-script.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)

### <a name="tutorials"></a>Samouczki
* [Samouczek: Wdrażanie klastra HPC Pack 2016 na platformie Azure](hpcpack-2016-cluster.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [Samouczek: Rozpoczynanie pracy z klastra HPC Pack na platformie Azure, aby uruchomić program Excel i SOA obciążeń](excel-cluster-hpcpack.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

### <a name="manual-deployment-with-the-azure-portal"></a>Ręczne wdrożenie z portalu Azure
* [Konfigurowanie węzła głównego klastra HPC Pack w maszynie Wirtualnej platformy Azure](hpcpack-cluster-headnode.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

### <a name="cluster-management"></a>Zarządzanie klastrami
* [Zarządzanie węzłów obliczeniowych w klastrze HPC Pack na platformie Azure](classic/hpcpack-cluster-node-manage.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)
* [Zwiększyć lub zmniejszyć zasoby obliczeniowe systemu Azure w klastrze HPC Pack](classic/hpcpack-cluster-node-autogrowshrink.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)
* [Przesyłanie zadań do klastra HPC Pack na platformie Azure](hpcpack-cluster-submit-jobs.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [Zarządzanie zadaniami w pakiecie HPC](https://technet.microsoft.com/library/jj899585.aspx)
* [Zarządzanie klastra HPC Pack na platformie Azure w usłudze Azure Active Directory](hpcpack-cluster-active-directory.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)

## <a name="add-worker-role-nodes-to-an-hpc-pack-cluster"></a>Dodaj węzły roli procesu roboczego w klastrze HPC Pack
* [Serii do wystąpień procesu roboczego platformy Azure z pakietem HPC](https://technet.microsoft.com/library/gg481749.aspx)
* [Samouczek: Konfigurowanie klastra hybrydowego pakietem HPC w systemie Azure](../../cloud-services/cloud-services-setup-hybrid-hpcpack-cluster.md)
* [Dodaj węzły platformy Azure "serii" z węzłem głównym HPC Pack na platformie Azure](classic/hpcpack-cluster-node-burst.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)

## <a name="integrate-with-azure-batch"></a>Integracja z partii zadań Azure
* [Serii do partii zadań Azure z pakietem HPC](https://technet.microsoft.com/library/mt612877.aspx)

## <a name="create-rdma-clusters-for-mpi-workloads"></a>Tworzenie klastrów RDMA dla obciążeń MPI
* [Konfigurowanie klastra RDMA systemu Windows z pakietem HPC do uruchamiania aplikacji MPI](classic/hpcpack-rdma-cluster.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)

