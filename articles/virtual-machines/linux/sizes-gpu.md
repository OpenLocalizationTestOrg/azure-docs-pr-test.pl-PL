---
title: rozmiar maszyny Wirtualnej systemu Linux aaaAzure - GPU | Dokumentacja firmy Microsoft
description: "Wyświetla listę hello innego procesora GPU zoptymalizowanych pod kątem dostępnych rozmiarów maszyn wirtualnych systemu Linux na platformie Azure."
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
ms.openlocfilehash: e98f720499be37df4048aeb513aa4f6b187b7335
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="gpu-linux-vm-sizes"></a><span data-ttu-id="21032-103">Rozmiary maszyn wirtualnych systemu Linux procesora GPU</span><span class="sxs-lookup"><span data-stu-id="21032-103">GPU Linux VM sizes</span></span>

[!INCLUDE [virtual-machines-common-sizes-gpu](../../../includes/virtual-machines-common-sizes-gpu.md)]


[!INCLUDE [virtual-machines-common-sizes-table-defs](../../../includes/virtual-machines-common-sizes-table-defs.md)]

[!INCLUDE [virtual-machines-n-series-linux-support](../../../includes/virtual-machines-n-series-linux-support.md)]

<span data-ttu-id="21032-104">Sterownik instalacji i weryfikacja kroki opisane w artykule [N-series sterownik Instalatora dla systemu Linux](n-series-driver-setup.md).</span><span class="sxs-lookup"><span data-stu-id="21032-104">For driver installation and verification steps, see [N-series driver setup for Linux](n-series-driver-setup.md).</span></span>

[!INCLUDE [virtual-machines-n-series-considerations](../../../includes/virtual-machines-n-series-considerations.md)]

* <span data-ttu-id="21032-105">Nie zaleca się instalowanie X serwera lub innych systemów, które używają sterownika nouveau hello na maszynach wirtualnych NC Ubuntu.</span><span class="sxs-lookup"><span data-stu-id="21032-105">We don't recommend installing X server or other systems that use hello nouveau driver on Ubuntu NC VMs.</span></span> <span data-ttu-id="21032-106">Przed zainstalowaniem wersji sterowników procesora GPU NVIDIA, potrzebujesz toodisable hello nouveau sterownika.</span><span class="sxs-lookup"><span data-stu-id="21032-106">Before installing NVIDIA GPU drivers, you need toodisable hello nouveau driver.</span></span>  

## <a name="other-sizes"></a><span data-ttu-id="21032-107">Innych rozmiarach</span><span class="sxs-lookup"><span data-stu-id="21032-107">Other sizes</span></span>
- [<span data-ttu-id="21032-108">Zastosowania ogólne</span><span class="sxs-lookup"><span data-stu-id="21032-108">General purpose</span></span>](sizes-general.md)
- [<span data-ttu-id="21032-109">Optymalizacja pod kątem obliczeń</span><span class="sxs-lookup"><span data-stu-id="21032-109">Compute optimized</span></span>](sizes-compute.md)
- [<span data-ttu-id="21032-110">Optymalizacja pod kątem pamięci</span><span class="sxs-lookup"><span data-stu-id="21032-110">Memory optimized</span></span>](sizes-memory.md)
- [<span data-ttu-id="21032-111">Optymalizacja pod kątem magazynu</span><span class="sxs-lookup"><span data-stu-id="21032-111">Storage optimized</span></span>](sizes-storage.md)
- [<span data-ttu-id="21032-112">Obliczenia o wysokiej wydajności</span><span class="sxs-lookup"><span data-stu-id="21032-112">High performance compute</span></span>](sizes-hpc.md)

## <a name="next-steps"></a><span data-ttu-id="21032-113">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="21032-113">Next steps</span></span>
<span data-ttu-id="21032-114">Dowiedz się więcej na temat [jednostki (ACU) rozwiązań usługi obliczenia Azure](acu.md) ułatwia porównanie wydajności obliczeniowej różnych jednostki SKU Azure.</span><span class="sxs-lookup"><span data-stu-id="21032-114">Learn more about how [Azure compute units (ACU)](acu.md) can help you compare compute performance across Azure SKUs.</span></span>