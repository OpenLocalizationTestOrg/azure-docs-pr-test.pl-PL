---
title: rozmiary maszyny Wirtualnej systemu Windows aaaAzure - HPC | Dokumentacja firmy Microsoft
description: "Wyświetla listę różnych rozmiarów hello dostępne Windows komputerowych o wysokiej wydajności maszyn wirtualnych na platformie Azure."
services: virtual-machines-windows
documentationcenter: 
author: jonbeck7
manager: timlt
editor: 
tags: azure-resource-manager,azure-service-management
ms.assetid: 
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 07/28/2017
ms.author: jonbeck
ms.openlocfilehash: 092bc32cfe048f439ad833911bef4ed17eda7977
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="high-performance-compute-vm-sizes"></a>Rozmiary maszyn wirtualnych wysokiej wydajności obliczeniowej

[!INCLUDE [virtual-machines-common-sizes-hpc](../../../includes/virtual-machines-common-sizes-hpc.md)]

[!INCLUDE [virtual-machines-common-sizes-table-defs](../../../includes/virtual-machines-common-sizes-table-defs.md)]

[!INCLUDE [virtual-machines-common-a8-a9-a10-a11-specs](../../../includes/virtual-machines-common-a8-a9-a10-a11-specs.md)]

## <a name="rdma-capable-instances"></a>Z funkcją RDMA wystąpień
Podzbiór hello obliczeniowych wystąpień (H16r, H16mr A8 i A9) funkcji interfejsu sieciowego dla zdalnego pamięci bezpośredniego dostępu (do pamięci RDMA) łączności. Ten interfejs jest ponadto rozmiarów maszyn wirtualnych dostępne tooother toohello standardowe sieć platformy Azure interfejsu. 
  
Ten interfejs umożliwia toocommunicate wystąpień z funkcją RDMA hello za pośrednictwem sieci InfiniBand, działających z rozdzielczością stawki FDR H16r i H16mr maszyn wirtualnych i szybkości QDR A8 i A9 maszyn wirtualnych. Tych funkcji RDMA można zwiększyć hello skalowalność i wydajność aplikacji komunikat interfejsu (Passing Interface).

Poniżej przedstawiono wymagania dla maszyn wirtualnych systemu Windows z funkcją RDMA tooaccess hello Azure RDMA sieci: 

* **System operacyjny**
  
  Windows Server 2012 R2, Windows Server 2012
  
  > [!NOTE]
  > Windows Server 2016 nie obsługuje obecnie, łączności RDMA na platformie Azure.
  >

* **Zestaw dostępności lub usługi w chmurze** — maszyny wirtualne z funkcją RDMA hello Wdróż w hello tym samym zestawie (Jeśli używasz modelu wdrażania usługi Azure Resource Manager hello) dostępności lub hello tej samej usługi w chmurze (Jeśli używasz hello klasycznego modelu wdrażania). Jeśli używasz partii zadań Azure hello maszyn wirtualnych z funkcją RDMA muszą być w hello tej samej puli.

* **MPI** -MPI firmy Microsoft (MS-MPI) 2012 R2 lub nowszym, Intel MPI biblioteki 5.x

  Obsługiwane implementacje MPI za pomocą interfejsu Network Direct Microsoft toocommunicate interfejsu hello między wystąpieniami. 

* **Przestrzeń adresową sieci RDMA** -172.16.0.0/16 przestrzeni adresowej hello rezerwuje hello RDMA sieci na platformie Azure. toorun MPI aplikacji w wystąpieniach wdrożony w sieci wirtualnej platformy Azure, upewnij się, czy przestrzeń adresową sieci wirtualnej hello nakłada się na powitania RDMA sieci.

* **Rozszerzenia maszyny Wirtualnej HpcVmDrivers** — na maszynach wirtualnych z funkcją RDMA, należy dodać hello HpcVmDrivers rozszerzenia tooinstall sieci sterowniki urządzeń systemu Windows dla łączności funkcji RDMA. (W przypadku niektórych wdrożeń wystąpień A8 i A9, hello HpcVmDrivers rozszerzenia jest dodawane automatycznie). tooadd hello wirtualna rozszerzenia tooa maszyny Wirtualnej, można użyć [programu Azure PowerShell](/powershell/azure/overview) polecenia cmdlet. 

  
  Witaj, następujące polecenia instaluje hello najnowszej wersji 1.1 HpcVMDrivers rozszerzenia na istniejącej maszyny Wirtualnej z funkcją RDMA, o nazwie *myVM* wdrożone w grupie zasobów hello o nazwie *myResourceGroup* w hello  *Zachodnie stany USA* regionu:

  ```PowerShell
  Set-AzureRmVMExtension -ResourceGroupName "myResourceGroup" -Location "westus" -VMName "myVM" -ExtensionName "HpcVmDrivers" -Publisher "Microsoft.HpcCompute" -Type "HpcVmDrivers" -TypeHandlerVersion "1.1"
  ```
  
  Aby uzyskać więcej informacji, zobacz [rozszerzenia maszyn wirtualnych i funkcji](extensions-features.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json). Może również współpracować z rozszerzeniami dla maszyn wirtualnych wdrożonych w hello [klasycznego modelu wdrażania](classic/manage-extensions.md).


## <a name="using-hpc-pack"></a>Przy użyciu pakietu HPC

[Microsoft HPC Pack](https://technet.microsoft.com/library/jj899572.aspx), rozwiązania firmy Microsoft wolnego HPC klastra i zadania zarządzania, jest jedną z opcji toocreate klastra obliczeniowego w aplikacjach opartych na systemie Windows MPI Azure toorun i innych obciążeń HPC. HPC Pack 2012 R2 i nowsze wersje zawierają środowiska uruchomieniowego dla MPI MS, który używa hello Azure RDMA sieci po wdrożeniu na maszynach wirtualnych z funkcją RDMA.




## <a name="other-sizes"></a>Innych rozmiarach
- [Zastosowania ogólne](sizes-general.md)
- [Optymalizacja pod kątem obliczeń](sizes-compute.md)
- [Optymalizacja pod kątem pamięci](../virtual-machines-windows-sizes-memory.md)
- [Optymalizacja pod kątem magazynu](../virtual-machines-windows-sizes-storage.md)
- [Optymalizacja pod kątem procesora GPU](sizes-gpu.md)

## <a name="next-steps"></a>Następne kroki

- Listy kontrolne toouse hello obliczeniowych wystąpień pakietem HPC w systemie Windows Server, zobacz [Konfigurowanie klastra RDMA systemu Windows z aplikacjami MPI toorun HPC Pack](classic/hpcpack-rdma-cluster.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).

- toouse obliczeniowych wystąpień podczas uruchamiania aplikacji MPI za pomocą partii zadań Azure, zobacz [użycie wielu wystąpień zadań toorun komunikat interfejsu (Passing Interface) aplikacji w partii zadań Azure](../../batch/batch-mpi.md).

- Dowiedz się więcej na temat [jednostki (ACU) rozwiązań usługi obliczenia Azure](acu.md) ułatwia porównanie wydajności obliczeniowej różnych jednostki SKU Azure.




