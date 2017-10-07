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
# <a name="about-h-series-and-compute-intensive-a-series-vms-for-linux"></a>O H serii i obliczeniowych maszyn wirtualnych A-series dla systemu Linux
Poniżej przedstawiono ogólne informacje i kilka kwestii dotyczących przy użyciu hello nowszej serii Azure H i hello wcześniejszych rozmiary A8, A9 A10 i A11, znanej także jako *obliczeniowych* wystąpień. Ten artykuł skupia się na temat używania rozmiary maszyn wirtualnych systemu Linux. Można również użyć go do [maszyn wirtualnych systemu Windows](../windows/a8-a9-a10-a11-specs.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json). 

Dla podstawowych specyfikacji, pojemności magazynu i dysku szczegółów, zobacz [rozmiary maszyn wirtualnych](sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

[!INCLUDE [virtual-machines-common-a8-a9-a10-a11-specs](../../../includes/virtual-machines-common-a8-a9-a10-a11-specs.md)]

## <a name="access-toohello-rdma-network"></a>Sieć RDMA toohello dostępu
Można utworzyć klastry z funkcją RDMA Uruchom jedno z hello obsługiwane dystrybucje systemu Linux HPC i obsługiwanych MPI implementacji tootake zalety hello Azure RDMA sieci maszyn wirtualnych w systemie Linux. Zobacz [skonfigurowanie aplikacji MPI Linux RDMA klastra toorun](classic/rdma-cluster.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json) opcje wdrażania i przykładowe czynności konfiguracyjne.

* **Dystrybucje** — należy wdrożyć maszyn wirtualnych z funkcją RDMA SUSE Linux Enterprise Server (SLES) lub obrazów nieautoryzowanego oprogramowania Wave (dawniej OpenLogic) na podstawie CentOS HPC w hello Azure Marketplace. Witaj następujące obrazy Marketplace obsługi funkcji RDMA połączeń:
  
    * SLES 12 SP1 w przypadku HPC, SLES 12 SP1 w przypadku HPC (Premium)
    
    * Na podstawie centOS 7.1 HPC, na podstawie CentOS HPC 6.5  
 
        > [!NOTE]
        > Dla maszyn wirtualnych, H-series firma Microsoft zaleca SLES 12 SP1 obrazu HPC albo CentOS 7.1 HPC obrazu.
        >
        > Na obrazach na podstawie CentOS HPC hello, aktualizacji jądra są wyłączone w hello **yum** pliku konfiguracji. To dlatego hello Linux RDMA sterowniki są dystrybuowane jako pakiet RPM, a aktualizacje sterowników może nie działać w przypadku jądra hello jest aktualizowany.
        > 
        > 
* **MPI** — Biblioteka MPI Intel 5.x
  
    W zależności od obrazu z witryny Marketplace hello można wybrać, oddzielnej licencji, instalacji, albo konfiguracji Intel MPI mogą być potrzebne w następujący sposób: 
  
  * **SLES 12 SP1 obrazu HPC** -Intel MPI pakiety są dystrybuowane na powitania maszyny Wirtualnej. Zainstalować, uruchamiając następujące polecenie hello:

      ```bash
      sudo rpm -v -i --nodeps /opt/intelMPI/intel_mpi_packages/*.rpm
      ```

  * **Na podstawie centOS obrazów HPC** -Intel MPI 5.1 jest już zainstalowana.  
    
    Konfiguracja dodatkowych systemu jest wymagane toorun zadań MPI w klastrowanych maszyn wirtualnych. Na przykład w klastrze maszyn wirtualnych, należy tooestablish relacji zaufania między hello węzły obliczeniowe. W przypadku typowych ustawień, zobacz [skonfigurowanie aplikacji MPI Linux RDMA klastra toorun](classic/rdma-cluster.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).

## <a name="considerations-for-hpc-pack-and-linux"></a>Zagadnienia dotyczące HPC Pack i Linux
[HPC Pack](https://technet.microsoft.com/library/jj899572.aspx), rozwiązania firmy Microsoft wolnego HPC klastra i zadania zarządzania, zawiera jedną opcję toouse hello obliczeniowych wystąpień z systemem Linux. najnowsze wersje Hello HPC Pack obsługuje kilka dystrybucje systemu Linux toorun na obliczeniowe węzłów wdrożone w maszynach wirtualnych platformy Azure, zarządzane przez system Windows Server węzła głównego. Z systemem Intel MPI węzły obliczeniowe Linux z funkcją RDMA HPC Pack można zaplanować i uruchamianie aplikacji Linux MPI RDMA hello dostępu do sieci. Zobacz tooget pracę, [wprowadzenie węzły obliczeniowe systemu Linux w klastrze HPC Pack na platformie Azure](classic/hpcpack-cluster.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).

## <a name="network-topology-considerations"></a>Zagadnienia dotyczące topologii sieci
* W przypadku komputerów z obsługą RDMA maszyn wirtualnych systemu Linux na platformie Azure Eth1 jest zarezerwowana dla ruchu sieciowego RDMA. Nie należy zmieniać ustawienia Eth1 lub wszelkie informacje zawarte w pliku konfiguracji hello odwołujących się toothis sieci. Eth0 jest zarezerwowana dla regularnych Azure ruchu sieciowego.
* IP przez InfiniBand (IB) nie jest obsługiwana na platformie Azure. Tylko RDMA over IB jest obsługiwana.



## <a name="next-steps"></a>Następne kroki
* Aby uzyskać szczegółowe informacje o dostępności i cenach hello obliczeniowych rozmiarów, zobacz [cennik maszyn wirtualnych](https://azure.microsoft.com/pricing/details/virtual-machines/#Linux).
* Uzyskać wielkości magazynu i dysku szczegółowe informacje, zobacz [rozmiary maszyn wirtualnych](sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).
* Zobacz tooget uruchomiono wdrażanie i z protokołem RDMA w systemie Linux przy użyciu obliczeniowych rozmiary [skonfigurowanie aplikacji MPI Linux RDMA klastra toorun](classic/rdma-cluster.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).

