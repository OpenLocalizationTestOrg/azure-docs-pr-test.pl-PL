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
# <a name="about-h-series-and-compute-intensive-a-series-vms-for-linux"></a>O H serii i obliczeniowych maszyn wirtualnych A-series dla systemu Linux
Poniżej przedstawiono ogólne informacje oraz pewne zagadnienia dotyczące korzystania z nowszej H-series Azure i wcześniejszych rozmiary A8, A9 A10 i A11, znanej także jako *obliczeniowych* wystąpień. Ten artykuł skupia się na temat używania rozmiary maszyn wirtualnych systemu Linux. Można również użyć go do [maszyn wirtualnych systemu Windows](../windows/a8-a9-a10-a11-specs.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json). 

Dla podstawowych specyfikacji, pojemności magazynu i dysku szczegółów, zobacz [rozmiary maszyn wirtualnych](sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

[!INCLUDE [virtual-machines-common-a8-a9-a10-a11-specs](../../../includes/virtual-machines-common-a8-a9-a10-a11-specs.md)]

## <a name="access-to-the-rdma-network"></a>Dostęp do sieci RDMA
Możesz utworzyć klastry z funkcją RDMA maszyn wirtualnych systemu Linux, że uruchom jeden z następujących obsługiwane dystrybucje systemu Linux HPC i obsługiwanych implementacji MPI, aby móc korzystać z sieci Azure RDMA. Zobacz [Konfigurowanie klastra Linux RDMA na uruchamianie aplikacji MPI](classic/rdma-cluster.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json) opcje wdrażania i przykładowe czynności konfiguracyjne.

* **Dystrybucje** — należy wdrożyć maszyn wirtualnych z funkcją RDMA SUSE Linux Enterprise Server (SLES) lub nieautoryzowanego oprogramowania Wave (dawniej OpenLogic) na podstawie CentOS HPC obrazów w portalu Azure Marketplace. Na poniższych ilustracjach Marketplace obsługi połączeń RDMA:
  
    * SLES 12 SP1 w przypadku HPC, SLES 12 SP1 w przypadku HPC (Premium)
    
    * Na podstawie centOS 7.1 HPC, na podstawie CentOS HPC 6.5  
 
        > [!NOTE]
        > Dla maszyn wirtualnych, H-series firma Microsoft zaleca SLES 12 SP1 obrazu HPC albo CentOS 7.1 HPC obrazu.
        >
        > Na obrazach na podstawie CentOS HPC aktualizacji jądra są wyłączone w **yum** pliku konfiguracji. To dlatego sterowniki Linux RDMA są dystrybuowane jako pakiet RPM, a aktualizacje sterowników może nie działać w przypadku jądra jest aktualizowany.
        > 
        > 
* **MPI** — Biblioteka MPI Intel 5.x
  
    W zależności od obrazu z witryny Marketplace można wybrać, oddzielnej licencji, instalacji, albo konfiguracji Intel MPI mogą być potrzebne w następujący sposób: 
  
  * **SLES 12 SP1 obrazu HPC** -Intel MPI pakiety są dystrybuowane na maszynie Wirtualnej. Zainstaluj, uruchamiając następujące polecenie:

      ```bash
      sudo rpm -v -i --nodeps /opt/intelMPI/intel_mpi_packages/*.rpm
      ```

  * **Na podstawie centOS obrazów HPC** -Intel MPI 5.1 jest już zainstalowana.  
    
    Dodatkowy system konfiguracji jest wymagany do uruchomienia zadań MPI na klastrowanych maszyn wirtualnych. Na przykład w klastrze maszyn wirtualnych, należy ustanowić relację zaufania między węzły obliczeniowe. W przypadku typowych ustawień, zobacz [Konfigurowanie klastra Linux RDMA na uruchamianie aplikacji MPI](classic/rdma-cluster.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).

## <a name="considerations-for-hpc-pack-and-linux"></a>Zagadnienia dotyczące HPC Pack i Linux
[HPC Pack](https://technet.microsoft.com/library/jj899572.aspx), rozwiązania firmy Microsoft wolnego HPC klastra i zadania zarządzania, zawiera jedną z opcji można użyć wystąpienia obliczeniowych w systemie Linux. Najnowsze wersje Obsługa HPC Pack kilka dystrybucje systemu Linux na obliczeniowe węzłów wdrożone w maszynach wirtualnych platformy Azure, zarządzane przez system Windows Server węzła głównego. Węzły obliczeniowe z funkcją RDMA Linux uruchomiony MPI firmy Intel HPC Pack można zaplanować i uruchamiać aplikacje, które uzyskują dostęp do sieci RDMA MPI systemu Linux. Aby rozpocząć, zobacz [wprowadzenie węzły obliczeniowe systemu Linux w klastrze HPC Pack na platformie Azure](classic/hpcpack-cluster.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).

## <a name="network-topology-considerations"></a>Zagadnienia dotyczące topologii sieci
* W przypadku komputerów z obsługą RDMA maszyn wirtualnych systemu Linux na platformie Azure Eth1 jest zarezerwowana dla ruchu sieciowego RDMA. Nie należy zmieniać ustawienia Eth1 lub wszelkie informacje zawarte w pliku konfiguracji odnoszące się do tej sieci. Eth0 jest zarezerwowana dla regularnych Azure ruchu sieciowego.
* IP przez InfiniBand (IB) nie jest obsługiwana na platformie Azure. Tylko RDMA over IB jest obsługiwana.



## <a name="next-steps"></a>Następne kroki
* Aby uzyskać szczegółowe informacje o dostępności i cenach rozmiarów obliczeniowych, zobacz [cennik maszyn wirtualnych](https://azure.microsoft.com/pricing/details/virtual-machines/#Linux).
* Uzyskać wielkości magazynu i dysku szczegółowe informacje, zobacz [rozmiary maszyn wirtualnych](sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).
* Aby rozpocząć wdrażanie i z protokołem RDMA w systemie Linux przy użyciu obliczeniowych rozmiarów, zobacz [Konfigurowanie klastra Linux RDMA na uruchamianie aplikacji MPI](classic/rdma-cluster.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).

