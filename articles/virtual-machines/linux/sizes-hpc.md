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
# <a name="high-performance-compute-linux-vm-sizes"></a>Wysoka wydajność obliczeniowe rozmiary maszyny Wirtualnej systemu Linux

[!INCLUDE [virtual-machines-common-sizes-hpc](../../../includes/virtual-machines-common-sizes-hpc.md)]

[!INCLUDE [virtual-machines-common-sizes-table-defs](../../../includes/virtual-machines-common-sizes-table-defs.md)]

[!INCLUDE [virtual-machines-common-a8-a9-a10-a11-specs](../../../includes/virtual-machines-common-a8-a9-a10-a11-specs.md)]

## <a name="rdma-capable-instances"></a>Z funkcją RDMA wystąpień
Podzbiór hello obliczeniowych wystąpień (H16r, H16mr A8 i A9) funkcji interfejsu sieciowego dla zdalnego pamięci bezpośredniego dostępu (do pamięci RDMA) łączności. Ten interfejs jest ponadto rozmiarów maszyn wirtualnych dostępne tooother toohello standardowe sieć platformy Azure interfejsu. 
  
Ten interfejs umożliwia toocommunicate wystąpień z funkcją RDMA hello za pośrednictwem sieci InfiniBand, działających z rozdzielczością stawki FDR H16r i H16mr maszyn wirtualnych i szybkości QDR A8 i A9 maszyn wirtualnych. Tych funkcji RDMA można zwiększyć hello skalowalność i wydajność aplikacji komunikat interfejsu (Passing Interface).

Poniżej przedstawiono wymagania dla maszyn wirtualnych systemu Linux z funkcją RDMA tooaccess hello Azure RDMA sieci:
 
* **Dystrybucje** — należy wdrożyć maszyn wirtualnych z funkcją RDMA SUSE Linux Enterprise Server (SLES) lub obrazów nieautoryzowanego oprogramowania Wave (dawniej OpenLogic) na podstawie CentOS HPC w hello Azure Marketplace. Witaj następujące obrazy Marketplace obsługi funkcji RDMA połączeń:
  
    * SLES 12 SP1 HPC lub SLES 12 SP1 w przypadku HPC (Premium)
    
    * Na podstawie centOS 7.3 HPC, na podstawie CentOS 7.1 HPC, na podstawie CentOS 6.8 HPC lub na podstawie CentOS HPC 6.5  
 
        > [!NOTE]
        > Dla maszyn wirtualnych, H-series firma Microsoft zaleca SLES 12 SP1 HPC obrazu lub na podstawie CentOS 7.1 lub nowszym HPC obrazu.
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
    
    Konfiguracja dodatkowych systemu jest wymagane toorun zadań MPI w klastrowanych maszyn wirtualnych. Na przykład w klastrze maszyn wirtualnych, należy tooestablish relacji zaufania między hello węzły obliczeniowe. W przypadku typowych ustawień, zobacz [skonfigurowanie Linux RDMA klastra toorun MPI aplikacji](classic/rdma-cluster.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)

### <a name="network-topology-considerations"></a>Zagadnienia dotyczące topologii sieci
* W przypadku komputerów z obsługą RDMA maszyn wirtualnych systemu Linux na platformie Azure Eth1 jest zarezerwowana dla ruchu sieciowego RDMA. Nie należy zmieniać ustawienia Eth1 lub wszelkie informacje zawarte w pliku konfiguracji hello odwołujących się toothis sieci. Eth0 jest zarezerwowana dla regularnych Azure ruchu sieciowego.

* IP przez InfiniBand (IB) nie jest obsługiwana na platformie Azure. Tylko RDMA over IB jest obsługiwana.

## <a name="using-hpc-pack"></a>Przy użyciu pakietu HPC
[HPC Pack](https://technet.microsoft.com/library/jj899572.aspx), rozwiązania firmy Microsoft wolnego HPC klastra i zadania zarządzania, jest jedną z opcji można instancji obliczeniowych hello toouse z systemem Linux. najnowsze wersje Hello HPC Pack obsługuje kilka dystrybucje systemu Linux toorun na obliczeniowe węzłów wdrożone w maszynach wirtualnych platformy Azure, zarządzane przez system Windows Server węzła głównego. Z systemem Intel MPI węzły obliczeniowe Linux z funkcją RDMA HPC Pack można zaplanować i uruchamianie aplikacji Linux MPI RDMA hello dostępu do sieci. Zobacz [wprowadzenie węzły obliczeniowe systemu Linux w klastrze HPC Pack na platformie Azure](classic/hpcpack-cluster.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).

## <a name="other-sizes"></a>Innych rozmiarach
- [Zastosowania ogólne](sizes-general.md)
- [Optymalizacja pod kątem obliczeń](sizes-compute.md)
- [Optymalizacja pod kątem pamięci](sizes-memory.md)
- [Optymalizacja pod kątem magazynu](sizes-storage.md)
- [Procesor GPU](../windows/sizes-gpu.md)


## <a name="next-steps"></a>Następne kroki

- Zobacz tooget uruchomiono wdrażanie i z protokołem RDMA w systemie Linux przy użyciu obliczeniowych rozmiary [skonfigurowanie aplikacji MPI Linux RDMA klastra toorun](classic/rdma-cluster.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).

- Dowiedz się więcej na temat [jednostki (ACU) rozwiązań usługi obliczenia Azure](acu.md) ułatwia porównanie wydajności obliczeniowej różnych jednostki SKU Azure.




