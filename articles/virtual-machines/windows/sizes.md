---
title: rozmiary aaaWindows maszyny Wirtualnej na platformie Azure | Dokumentacja firmy Microsoft
description: "Wyświetla listę różnych rozmiarów hello dostępnej dla maszyn wirtualnych systemu Windows na platformie Azure."
services: virtual-machines-windows
documentationcenter: 
author: jonbeck7
manager: timlt
editor: 
tags: azure-resource-manager,azure-service-management
ms.assetid: aabf0d30-04eb-4d34-b44a-69f8bfb84f22
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 07/28/2017
ms.author: jonbeck
ms.openlocfilehash: 80bd8241b134031c41b56224e841c7557c4845cf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="sizes-for-windows-virtual-machines-in-azure"></a><span data-ttu-id="d305f-103">Rozmiary maszyn wirtualnych systemu Windows na platformie Azure</span><span class="sxs-lookup"><span data-stu-id="d305f-103">Sizes for Windows virtual machines in Azure</span></span>

<span data-ttu-id="d305f-104">W tym artykule opisano dostępne rozmiary hello i opcje dla hello toorun można użyć w aplikacji systemu Windows i obciążeń maszyn wirtualnych platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="d305f-104">This article describes hello available sizes and options for hello Azure virtual machines you can use toorun your Windows apps and workloads.</span></span> <span data-ttu-id="d305f-105">Umożliwia także toobe zagadnienia dotyczące wdrażania uwagę podczas planowania toouse tych zasobów.</span><span class="sxs-lookup"><span data-stu-id="d305f-105">It also provides deployment considerations toobe aware of when you're planning toouse these resources.</span></span>  <span data-ttu-id="d305f-106">W tym artykule jest również dostępny do [maszyn wirtualnych systemu Linux](../linux/sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="d305f-106">This article is also available for [Linux virtual machines](../linux/sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>


| <span data-ttu-id="d305f-107">Typ</span><span class="sxs-lookup"><span data-stu-id="d305f-107">Type</span></span>                     | <span data-ttu-id="d305f-108">Rozmiary</span><span class="sxs-lookup"><span data-stu-id="d305f-108">Sizes</span></span>           |    <span data-ttu-id="d305f-109">Opis</span><span class="sxs-lookup"><span data-stu-id="d305f-109">Description</span></span>       |
|--------------------------|-------------------|------------------------------------------------------------------------------------------------------------------------------------|
| [<span data-ttu-id="d305f-110">Zastosowania ogólne</span><span class="sxs-lookup"><span data-stu-id="d305f-110">General purpose</span></span>](sizes-general.md)          | <span data-ttu-id="d305f-111">Dsv3, Dv3, DSv2, Dv2, DS, D, Av2, A0 7</span><span class="sxs-lookup"><span data-stu-id="d305f-111">Dsv3, Dv3, DSv2, Dv2, DS, D, Av2, A0-7</span></span> | <span data-ttu-id="d305f-112">Zrównoważona moc procesora CPU w stosunku do pamięci.</span><span class="sxs-lookup"><span data-stu-id="d305f-112">Balanced CPU-to-memory ratio.</span></span> <span data-ttu-id="d305f-113">Idealnym badań i rozwoju, toomedium małych baz danych i serwerów sieci web ruchu toomedium niski.</span><span class="sxs-lookup"><span data-stu-id="d305f-113">Ideal for testing and development, small toomedium databases, and low toomedium traffic web servers.</span></span> |
| [<span data-ttu-id="d305f-114">Optymalizacja pod kątem obliczeń</span><span class="sxs-lookup"><span data-stu-id="d305f-114">Compute optimized</span></span>](sizes-compute.md)        | <span data-ttu-id="d305f-115">FS, F</span><span class="sxs-lookup"><span data-stu-id="d305f-115">Fs, F</span></span>             | <span data-ttu-id="d305f-116">Duża moc procesora CPU w stosunku do pamięci.</span><span class="sxs-lookup"><span data-stu-id="d305f-116">High CPU-to-memory ratio.</span></span> <span data-ttu-id="d305f-117">Dobrze sprawdzają się w przypadku serwerów sieci Web o średnim ruchu, urządzeń sieciowych, procesów wsadowych i serwerów aplikacji.</span><span class="sxs-lookup"><span data-stu-id="d305f-117">Good for medium traffic web servers, network appliances, batch processes, and application servers.</span></span>        |
| [<span data-ttu-id="d305f-118">Optymalizacja pod kątem pamięci</span><span class="sxs-lookup"><span data-stu-id="d305f-118">Memory optimized</span></span>](../virtual-machines-windows-sizes-memory.md)         | <span data-ttu-id="d305f-119">Esv3, Ev3, M, GS, G, DSv2, DS, Dv2, D</span><span class="sxs-lookup"><span data-stu-id="d305f-119">Esv3, Ev3, M, GS, G, DSv2, DS, Dv2, D</span></span>   | <span data-ttu-id="d305f-120">Wysoki współczynnik pamięci do Procesora.</span><span class="sxs-lookup"><span data-stu-id="d305f-120">High memory-to-CPU ratio.</span></span> <span data-ttu-id="d305f-121">Świetnie relacyjnej bazy danych serwerów, pamięci podręcznych średnia toolarge i analizy w pamięci.</span><span class="sxs-lookup"><span data-stu-id="d305f-121">Great for relational database servers, medium toolarge caches, and in-memory analytics.</span></span>                 |
| [<span data-ttu-id="d305f-122">Optymalizacja pod kątem magazynu</span><span class="sxs-lookup"><span data-stu-id="d305f-122">Storage optimized</span></span>](../virtual-machines-windows-sizes-storage.md)        | <span data-ttu-id="d305f-123">Ls</span><span class="sxs-lookup"><span data-stu-id="d305f-123">Ls</span></span>                | <span data-ttu-id="d305f-124">Wysoka przepływność dysku i operacje we/wy.</span><span class="sxs-lookup"><span data-stu-id="d305f-124">High disk throughput and IO.</span></span> <span data-ttu-id="d305f-125">Idealne rozwiązanie w przypadku danych big data oraz baz danych SQL i NoSQL.</span><span class="sxs-lookup"><span data-stu-id="d305f-125">Ideal for Big Data, SQL, and NoSQL databases.</span></span>                                                         |
| [<span data-ttu-id="d305f-126">Procesor GPU</span><span class="sxs-lookup"><span data-stu-id="d305f-126">GPU</span></span>](sizes-gpu.md)            | <span data-ttu-id="d305f-127">WIRTUALIZACJĄ SIECI, NC</span><span class="sxs-lookup"><span data-stu-id="d305f-127">NV, NC</span></span>            | <span data-ttu-id="d305f-128">Celem duże Renderowanie grafiki i wideo edycji specjalne maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="d305f-128">Specialized virtual machines targeted for heavy graphic rendering and video editing.</span></span> <span data-ttu-id="d305f-129">Dostępne z jednego lub wielu procesorów graficznych.</span><span class="sxs-lookup"><span data-stu-id="d305f-129">Available with single or multiple GPUs.</span></span>       |
| [<span data-ttu-id="d305f-130">Obliczenia o wysokiej wydajności</span><span class="sxs-lookup"><span data-stu-id="d305f-130">High performance compute</span></span>](sizes-hpc.md) | <span data-ttu-id="d305f-131">H-A8 11</span><span class="sxs-lookup"><span data-stu-id="d305f-131">H, A8-11</span></span>          | <span data-ttu-id="d305f-132">Maszyny wirtualne z najszybszymi i najbardziej wydajnymi procesorami CPU oraz, opcjonalnie, interfejsami sieciowymi zapewniającymi wysoką przepływność (RDMA).</span><span class="sxs-lookup"><span data-stu-id="d305f-132">Our fastest and most powerful CPU virtual machines with optional high-throughput network interfaces (RDMA).</span></span> 

<br> 

- <span data-ttu-id="d305f-133">Aby uzyskać informacje o cenach z hello różne rozmiary, zobacz [cennik maszyn wirtualnych](https://azure.microsoft.com/pricing/details/virtual-machines/#Windows).</span><span class="sxs-lookup"><span data-stu-id="d305f-133">For information about pricing of hello various sizes, see [Virtual Machines Pricing](https://azure.microsoft.com/pricing/details/virtual-machines/#Windows).</span></span> 
- <span data-ttu-id="d305f-134">ograniczenia ogólne toosee na maszynach wirtualnych Azure, zobacz [subskrypcji platformy Azure i usługi limity, przydziały i ograniczenia](../../azure-subscription-service-limits.md).</span><span class="sxs-lookup"><span data-stu-id="d305f-134">toosee general limits on Azure VMs, see [Azure subscription and service limits, quotas, and constraints](../../azure-subscription-service-limits.md).</span></span>
- <span data-ttu-id="d305f-135">Koszty przechowywania są obliczane osobno na podstawie używane strony w hello konta magazynu.</span><span class="sxs-lookup"><span data-stu-id="d305f-135">Storage costs are calculated separately based on used pages in hello storage account.</span></span> <span data-ttu-id="d305f-136">Aby uzyskać szczegółowe informacje [cennik usługi Azure Storage](https://azure.microsoft.com/pricing/details/storage/).</span><span class="sxs-lookup"><span data-stu-id="d305f-136">For details, [Azure Storage Pricing](https://azure.microsoft.com/pricing/details/storage/).</span></span>
- <span data-ttu-id="d305f-137">Dowiedz się więcej na temat [jednostki (ACU) rozwiązań usługi obliczenia Azure](acu.md) ułatwia porównanie wydajności obliczeniowej różnych jednostki SKU Azure.</span><span class="sxs-lookup"><span data-stu-id="d305f-137">Learn more about how [Azure compute units (ACU)](acu.md) can help you compare compute performance across Azure SKUs.</span></span>



## <a name="rest-api"></a><span data-ttu-id="d305f-138">Interfejs API REST</span><span class="sxs-lookup"><span data-stu-id="d305f-138">Rest API</span></span>

<span data-ttu-id="d305f-139">Dla informacji o używaniu tooquery interfejsu API REST hello rozmiarów maszyn wirtualnych zobacz następujące hello:</span><span class="sxs-lookup"><span data-stu-id="d305f-139">For information on using hello REST API tooquery for VM sizes, see hello following:</span></span>

- [<span data-ttu-id="d305f-140">Lista dostępne rozmiary maszyny wirtualnej do zmiany rozmiaru</span><span class="sxs-lookup"><span data-stu-id="d305f-140">List available virtual machine sizes for resizing</span></span>](https://docs.microsoft.com/rest/api/compute/virtualmachines/virtualmachines-list-sizes-for-resizing)
- [<span data-ttu-id="d305f-141">Lista dostępne rozmiary maszyny wirtualnej w ramach subskrypcji</span><span class="sxs-lookup"><span data-stu-id="d305f-141">List available virtual machine sizes for a subscription</span></span>](https://docs.microsoft.com/rest/api/compute/virtualmachines/virtualmachines-list-sizes-region)
- [<span data-ttu-id="d305f-142">Lista dostępne rozmiary maszyny wirtualnej w zestawie dostępności</span><span class="sxs-lookup"><span data-stu-id="d305f-142">List available virtual machine sizes in an availability set</span></span>](
https://docs.microsoft.com/rest/api/compute/virtualmachines/virtualmachines-list-sizes-availability-set)

## <a name="acu"></a><span data-ttu-id="d305f-143">ACU</span><span class="sxs-lookup"><span data-stu-id="d305f-143">ACU</span></span>

<span data-ttu-id="d305f-144">Dowiedz się więcej na temat [jednostki (ACU) rozwiązań usługi obliczenia Azure](acu.md) ułatwia porównanie wydajności obliczeniowej różnych jednostki SKU Azure.</span><span class="sxs-lookup"><span data-stu-id="d305f-144">Learn more about how [Azure compute units (ACU)](acu.md) can help you compare compute performance across Azure SKUs.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d305f-145">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="d305f-145">Next steps</span></span>

<span data-ttu-id="d305f-146">Dowiedz się więcej na temat hello różnych rozmiarów maszyn wirtualnych, które są dostępne:</span><span class="sxs-lookup"><span data-stu-id="d305f-146">Learn more about hello different VM sizes that are available:</span></span>
- [<span data-ttu-id="d305f-147">Zastosowania ogólne</span><span class="sxs-lookup"><span data-stu-id="d305f-147">General purpose</span></span>](sizes-general.md)
- [<span data-ttu-id="d305f-148">Optymalizacja pod kątem obliczeń</span><span class="sxs-lookup"><span data-stu-id="d305f-148">Compute optimized</span></span>](sizes-compute.md)
- [<span data-ttu-id="d305f-149">Optymalizacja pod kątem pamięci</span><span class="sxs-lookup"><span data-stu-id="d305f-149">Memory optimized</span></span>](../virtual-machines-windows-sizes-memory.md)
- [<span data-ttu-id="d305f-150">Optymalizacja pod kątem magazynu</span><span class="sxs-lookup"><span data-stu-id="d305f-150">Storage optimized</span></span>](../virtual-machines-windows-sizes-storage.md)
- [<span data-ttu-id="d305f-151">Optymalizacja pod kątem procesora GPU</span><span class="sxs-lookup"><span data-stu-id="d305f-151">GPU optimized</span></span>](sizes-gpu.md)
- [<span data-ttu-id="d305f-152">Obliczenia o wysokiej wydajności</span><span class="sxs-lookup"><span data-stu-id="d305f-152">High performance compute</span></span>](sizes-hpc.md)



