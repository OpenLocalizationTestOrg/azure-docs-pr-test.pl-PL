---
title: Rozmiar maszyny Wirtualnej systemu Linux platformy Azure - GPU | Dokumentacja firmy Microsoft
description: "Wyświetla różne procesora GPU zoptymalizowanych pod kątem dostępne dla maszyn wirtualnych systemu Linux na platformie Azure."
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
ms.openlocfilehash: 5c9bf89feba519147b07f2810fe4da882664e89e
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="gpu-linux-vm-sizes"></a><span data-ttu-id="3555b-103">Rozmiary maszyn wirtualnych systemu Linux procesora GPU</span><span class="sxs-lookup"><span data-stu-id="3555b-103">GPU Linux VM sizes</span></span>

[!INCLUDE [virtual-machines-common-sizes-gpu](../../../includes/virtual-machines-common-sizes-gpu.md)]


[!INCLUDE [virtual-machines-common-sizes-table-defs](../../../includes/virtual-machines-common-sizes-table-defs.md)]

[!INCLUDE [virtual-machines-n-series-linux-support](../../../includes/virtual-machines-n-series-linux-support.md)]

<span data-ttu-id="3555b-104">Sterownik instalacji i weryfikacja kroki opisane w artykule [N-series sterownik Instalatora dla systemu Linux](n-series-driver-setup.md).</span><span class="sxs-lookup"><span data-stu-id="3555b-104">For driver installation and verification steps, see [N-series driver setup for Linux](n-series-driver-setup.md).</span></span>

[!INCLUDE [virtual-machines-n-series-considerations](../../../includes/virtual-machines-n-series-considerations.md)]

* <span data-ttu-id="3555b-105">Nie zaleca się instalowanie X serwera lub innych systemów, które używają sterownika nouveau na maszynach wirtualnych NC Ubuntu.</span><span class="sxs-lookup"><span data-stu-id="3555b-105">We don't recommend installing X server or other systems that use the nouveau driver on Ubuntu NC VMs.</span></span> <span data-ttu-id="3555b-106">Przed zainstalowaniem wersji sterowników procesora GPU NVIDIA, należy wyłączyć sterownik nouveau.</span><span class="sxs-lookup"><span data-stu-id="3555b-106">Before installing NVIDIA GPU drivers, you need to disable the nouveau driver.</span></span>  

## <a name="other-sizes"></a><span data-ttu-id="3555b-107">Innych rozmiarach</span><span class="sxs-lookup"><span data-stu-id="3555b-107">Other sizes</span></span>
- [<span data-ttu-id="3555b-108">Zastosowania ogólne</span><span class="sxs-lookup"><span data-stu-id="3555b-108">General purpose</span></span>](sizes-general.md)
- [<span data-ttu-id="3555b-109">Optymalizacja pod kątem obliczeń</span><span class="sxs-lookup"><span data-stu-id="3555b-109">Compute optimized</span></span>](sizes-compute.md)
- [<span data-ttu-id="3555b-110">Optymalizacja pod kątem pamięci</span><span class="sxs-lookup"><span data-stu-id="3555b-110">Memory optimized</span></span>](sizes-memory.md)
- [<span data-ttu-id="3555b-111">Optymalizacja pod kątem magazynu</span><span class="sxs-lookup"><span data-stu-id="3555b-111">Storage optimized</span></span>](sizes-storage.md)
- [<span data-ttu-id="3555b-112">Obliczenia o wysokiej wydajności</span><span class="sxs-lookup"><span data-stu-id="3555b-112">High performance compute</span></span>](sizes-hpc.md)

## <a name="next-steps"></a><span data-ttu-id="3555b-113">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="3555b-113">Next steps</span></span>
<span data-ttu-id="3555b-114">Dowiedz się więcej na temat [jednostki (ACU) rozwiązań usługi obliczenia Azure](acu.md) ułatwia porównanie wydajności obliczeniowej różnych jednostki SKU Azure.</span><span class="sxs-lookup"><span data-stu-id="3555b-114">Learn more about how [Azure compute units (ACU)](acu.md) can help you compare compute performance across Azure SKUs.</span></span>