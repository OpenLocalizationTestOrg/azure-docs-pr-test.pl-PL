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
# <a name="options-with-hpc-pack-toocreate-and-manage-a-windows-hpc-cluster-in-azure"></a>Opcji za pomocą toocreate HPC Pack i zarządzanie nimi klastra HPC systemu Windows na platformie Azure
[!INCLUDE [virtual-machines-common-hpcpack-cluster-options](../../../includes/virtual-machines-common-hpcpack-cluster-options.md)]

Ten artykuł dotyczy toocreate opcje HPC Pack obciążeń systemu Windows toorun klastrów. Dostępne są także opcje tworzenia HPC Pack klastrów toorun [obciążeń HPC systemu Linux](../linux/hpcpack-cluster-options.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).


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
* [Tworzenie klastra HPC z hello skrypt wdrożenia HPC Pack IaaS](classic/hpcpack-cluster-powershell-script.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)

### <a name="tutorials"></a>Samouczki
* [Samouczek: Wdrażanie klastra HPC Pack 2016 na platformie Azure](hpcpack-2016-cluster.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [Samouczek: Rozpoczynanie pracy z klastra HPC Pack w Azure toorun programu Excel i obciążeń SOA](excel-cluster-hpcpack.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

### <a name="manual-deployment-with-hello-azure-portal"></a>Ręczne wdrożenie z hello portalu Azure
* [Konfigurowanie hello węzła głównego klastra HPC Pack w maszynie Wirtualnej platformy Azure](hpcpack-cluster-headnode.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

### <a name="cluster-management"></a>Zarządzanie klastrami
* [Zarządzanie węzłów obliczeniowych w klastrze HPC Pack na platformie Azure](classic/hpcpack-cluster-node-manage.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)
* [Zwiększyć lub zmniejszyć zasoby obliczeniowe systemu Azure w klastrze HPC Pack](classic/hpcpack-cluster-node-autogrowshrink.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)
* [Przedstawia klastra HPC Pack tooan zadania na platformie Azure](hpcpack-cluster-submit-jobs.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [Zarządzanie zadaniami w pakiecie HPC](https://technet.microsoft.com/library/jj899585.aspx)
* [Zarządzanie klastra HPC Pack na platformie Azure w usłudze Azure Active Directory](hpcpack-cluster-active-directory.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)

## <a name="add-worker-role-nodes-tooan-hpc-pack-cluster"></a>Dodawanie procesu roboczego roli węzłów tooan HPC Pack klastra
* [Serii wystąpień procesów roboczych tooAzure pakietem HPC](https://technet.microsoft.com/library/gg481749.aspx)
* [Samouczek: Konfigurowanie klastra hybrydowego pakietem HPC w systemie Azure](../../cloud-services/cloud-services-setup-hybrid-hpcpack-cluster.md)
* [Dodaj Azure "serii" węzłów tooan HPC Pack węzła głównego na platformie Azure](classic/hpcpack-cluster-node-burst.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)

## <a name="integrate-with-azure-batch"></a>Integracja z partii zadań Azure
* [TooAzure serii partii z pakietem HPC](https://technet.microsoft.com/library/mt612877.aspx)

## <a name="create-rdma-clusters-for-mpi-workloads"></a>Tworzenie klastrów RDMA dla obciążeń MPI
* [Konfigurowanie klastra Windows RDMA HPC Pack toorun MPI aplikacji](classic/hpcpack-rdma-cluster.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)

