---
title: rozmiary aaaLinux maszyny Wirtualnej na platformie Azure | Dokumentacja firmy Microsoft
description: "Wyświetla listę różnych rozmiarów hello dostępnej dla maszyn wirtualnych systemu Linux na platformie Azure."
services: virtual-machines-linux
documentationcenter: 
author: jonbeck7
manager: timlt
editor: 
tags: azure-resource-manager,azure-service-management
ms.assetid: da681171-f045-4c80-a5a9-d8bd47964673
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 07/28/2017
ms.author: jonbeck
ms.openlocfilehash: 56cbe0a0d7d34def07636edba74c4c699e336012
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="sizes-for-linux-virtual-machines-in-azure"></a><span data-ttu-id="0c0f9-103">Rozmiary maszyn wirtualnych systemu Linux na platformie Azure</span><span class="sxs-lookup"><span data-stu-id="0c0f9-103">Sizes for Linux virtual machines in Azure</span></span>
<span data-ttu-id="0c0f9-104">W tym artykule opisano dostępne rozmiary hello i opcje dla hello służy toorun Linux aplikacji i obciążeń maszyn wirtualnych platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="0c0f9-104">This article describes hello available sizes and options for hello Azure virtual machines you can use toorun your Linux apps and workloads.</span></span> <span data-ttu-id="0c0f9-105">Umożliwia także toobe zagadnienia dotyczące wdrażania uwagę podczas planowania toouse tych zasobów.</span><span class="sxs-lookup"><span data-stu-id="0c0f9-105">It also provides deployment considerations toobe aware of when you're planning toouse these resources.</span></span> <span data-ttu-id="0c0f9-106">W tym artykule jest również dostępny do [maszyn wirtualnych Windows](../windows/sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="0c0f9-106">This article is also available for [Windows virtual machines](../windows/sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>


| <span data-ttu-id="0c0f9-107">Typ</span><span class="sxs-lookup"><span data-stu-id="0c0f9-107">Type</span></span>                     | <span data-ttu-id="0c0f9-108">Rozmiary</span><span class="sxs-lookup"><span data-stu-id="0c0f9-108">Sizes</span></span>           |    <span data-ttu-id="0c0f9-109">Opis</span><span class="sxs-lookup"><span data-stu-id="0c0f9-109">Description</span></span>       |
|--------------------------|-------------------|------------------------------------------------------------------------------------------------------------------------------------|
| [<span data-ttu-id="0c0f9-110">Zastosowania ogólne</span><span class="sxs-lookup"><span data-stu-id="0c0f9-110">General purpose</span></span>](sizes-general.md)          | <span data-ttu-id="0c0f9-111">Dsv3, Dv3, DSv2, Dv2, DS, D, Av2, A0-7</span><span class="sxs-lookup"><span data-stu-id="0c0f9-111">Dsv3, Dv3, DSv2, Dv2, DS, D, Av2, A0-7,</span></span>  | <span data-ttu-id="0c0f9-112">Zrównoważona moc procesora CPU w stosunku do pamięci.</span><span class="sxs-lookup"><span data-stu-id="0c0f9-112">Balanced CPU-to-memory ratio.</span></span> <span data-ttu-id="0c0f9-113">Idealnym badań i rozwoju, toomedium małych baz danych i serwerów sieci web ruchu toomedium niski.</span><span class="sxs-lookup"><span data-stu-id="0c0f9-113">Ideal for testing and development, small toomedium databases, and low toomedium traffic web servers.</span></span> |
| [<span data-ttu-id="0c0f9-114">Optymalizacja pod kątem obliczeń</span><span class="sxs-lookup"><span data-stu-id="0c0f9-114">Compute optimized</span></span>](sizes-compute.md)        | <span data-ttu-id="0c0f9-115">FS, F</span><span class="sxs-lookup"><span data-stu-id="0c0f9-115">Fs, F</span></span>             | <span data-ttu-id="0c0f9-116">Duża moc procesora CPU w stosunku do pamięci.</span><span class="sxs-lookup"><span data-stu-id="0c0f9-116">High CPU-to-memory ratio.</span></span> <span data-ttu-id="0c0f9-117">Nadaje się do serwerów sieci web średnia ruchu, urządzenia sieciowe, łaźni procesy i serwerów aplikacji.</span><span class="sxs-lookup"><span data-stu-id="0c0f9-117">Good for medium traffic web servers, network appliances, bath processes, and application servers.</span></span>        |
| [<span data-ttu-id="0c0f9-118">Optymalizacja pod kątem pamięci</span><span class="sxs-lookup"><span data-stu-id="0c0f9-118">Memory optimized</span></span>](sizes-memory.md)         | <span data-ttu-id="0c0f9-119">Esv3, Ev3, M, GS, G, DSv2, DS, Dv2, D</span><span class="sxs-lookup"><span data-stu-id="0c0f9-119">Esv3, Ev3, M, GS, G, DSv2, DS, Dv2, D</span></span>   | <span data-ttu-id="0c0f9-120">Wysoki współczynnik pamięci do Procesora.</span><span class="sxs-lookup"><span data-stu-id="0c0f9-120">High memory-to-CPU ratio.</span></span> <span data-ttu-id="0c0f9-121">Świetnie relacyjnej bazy danych serwerów, pamięci podręcznych średnia toolarge i analizy w pamięci.</span><span class="sxs-lookup"><span data-stu-id="0c0f9-121">Great for relational database servers, medium toolarge caches, and in-memory analytics.</span></span>                 |
| [<span data-ttu-id="0c0f9-122">Optymalizacja pod kątem magazynu</span><span class="sxs-lookup"><span data-stu-id="0c0f9-122">Storage optimized</span></span>](sizes-storage.md)        | <span data-ttu-id="0c0f9-123">Ls</span><span class="sxs-lookup"><span data-stu-id="0c0f9-123">Ls</span></span>                | <span data-ttu-id="0c0f9-124">Wysoka przepływność dysku i operacje we/wy.</span><span class="sxs-lookup"><span data-stu-id="0c0f9-124">High disk throughput and IO.</span></span> <span data-ttu-id="0c0f9-125">Idealne rozwiązanie w przypadku danych big data oraz baz danych SQL i NoSQL.</span><span class="sxs-lookup"><span data-stu-id="0c0f9-125">Ideal for Big Data, SQL, and NoSQL databases.</span></span>                                                         |
| [<span data-ttu-id="0c0f9-126">Procesor GPU</span><span class="sxs-lookup"><span data-stu-id="0c0f9-126">GPU</span></span>](sizes-gpu.md)            | <span data-ttu-id="0c0f9-127">WIRTUALIZACJĄ SIECI, NC</span><span class="sxs-lookup"><span data-stu-id="0c0f9-127">NV, NC</span></span>            | <span data-ttu-id="0c0f9-128">Celem duże Renderowanie grafiki i wideo edycji specjalne maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="0c0f9-128">Specialized virtual machines targeted for heavy graphic rendering and video editing.</span></span> <span data-ttu-id="0c0f9-129">Dostępne z jednego lub wielu procesorów graficznych.</span><span class="sxs-lookup"><span data-stu-id="0c0f9-129">Available with single or multiple GPUs.</span></span>       |
| [<span data-ttu-id="0c0f9-130">Obliczenia o wysokiej wydajności</span><span class="sxs-lookup"><span data-stu-id="0c0f9-130">High performance compute</span></span>](sizes-hpc.md) | <span data-ttu-id="0c0f9-131">H-A8 11</span><span class="sxs-lookup"><span data-stu-id="0c0f9-131">H, A8-11</span></span>          | <span data-ttu-id="0c0f9-132">Maszyny wirtualne z najszybszymi i najbardziej wydajnymi procesorami CPU oraz, opcjonalnie, interfejsami sieciowymi zapewniającymi wysoką przepływność (RDMA).</span><span class="sxs-lookup"><span data-stu-id="0c0f9-132">Our fastest and most powerful CPU virtual machines with optional high-throughput network interfaces (RDMA).</span></span> 

<br>

- <span data-ttu-id="0c0f9-133">Aby uzyskać informacje o cenach z hello różne rozmiary, zobacz [cennik maszyn wirtualnych](https://azure.microsoft.com/pricing/details/virtual-machines/#Linux).</span><span class="sxs-lookup"><span data-stu-id="0c0f9-133">For information about pricing of hello various sizes, see [Virtual Machines Pricing](https://azure.microsoft.com/pricing/details/virtual-machines/#Linux).</span></span> 
- <span data-ttu-id="0c0f9-134">Dostępność rozmiarów maszyn wirtualnych w regionach platformy Azure, zobacz [produkty, które są dostępne w regionie](https://azure.microsoft.com/regions/services/).</span><span class="sxs-lookup"><span data-stu-id="0c0f9-134">For availability of VM sizes in Azure regions, see [Products available by region](https://azure.microsoft.com/regions/services/).</span></span>
- <span data-ttu-id="0c0f9-135">ograniczenia ogólne toosee na maszynach wirtualnych Azure, zobacz [subskrypcji platformy Azure i usługi limity, przydziały i ograniczenia](../../azure-subscription-service-limits.md).</span><span class="sxs-lookup"><span data-stu-id="0c0f9-135">toosee general limits on Azure VMs, see [Azure subscription and service limits, quotas, and constraints](../../azure-subscription-service-limits.md).</span></span>
- <span data-ttu-id="0c0f9-136">Dowiedz się więcej na temat [jednostki (ACU) rozwiązań usługi obliczenia Azure](../windows/acu.md) ułatwia porównanie wydajności obliczeniowej różnych jednostki SKU Azure.</span><span class="sxs-lookup"><span data-stu-id="0c0f9-136">Learn more about how [Azure compute units (ACU)](../windows/acu.md) can help you compare compute performance across Azure SKUs.</span></span>


## <a name="rest-api"></a><span data-ttu-id="0c0f9-137">Interfejs API REST</span><span class="sxs-lookup"><span data-stu-id="0c0f9-137">Rest API</span></span>

<span data-ttu-id="0c0f9-138">Dla informacji o używaniu tooquery interfejsu API REST hello rozmiarów maszyn wirtualnych zobacz następujące hello:</span><span class="sxs-lookup"><span data-stu-id="0c0f9-138">For information on using hello REST API tooquery for VM sizes, see hello following:</span></span>

- [<span data-ttu-id="0c0f9-139">Lista dostępne rozmiary maszyny wirtualnej do zmiany rozmiaru</span><span class="sxs-lookup"><span data-stu-id="0c0f9-139">List available virtual machine sizes for resizing</span></span>](https://docs.microsoft.com/rest/api/compute/virtualmachines/virtualmachines-list-sizes-for-resizing)
- [<span data-ttu-id="0c0f9-140">Lista dostępne rozmiary maszyny wirtualnej w ramach subskrypcji</span><span class="sxs-lookup"><span data-stu-id="0c0f9-140">List available virtual machine sizes for a subscription</span></span>](https://docs.microsoft.com/rest/api/compute/virtualmachines/virtualmachines-list-sizes-region)
- [<span data-ttu-id="0c0f9-141">Lista dostępne rozmiary maszyny wirtualnej w zestawie dostępności</span><span class="sxs-lookup"><span data-stu-id="0c0f9-141">List available virtual machine sizes in an availability set</span></span>](
https://docs.microsoft.com/rest/api/compute/virtualmachines/virtualmachines-list-sizes-availability-set)

## <a name="acu"></a><span data-ttu-id="0c0f9-142">ACU</span><span class="sxs-lookup"><span data-stu-id="0c0f9-142">ACU</span></span>

<span data-ttu-id="0c0f9-143">Dowiedz się więcej na temat [jednostki (ACU) rozwiązań usługi obliczenia Azure](acu.md) ułatwia porównanie wydajności obliczeniowej różnych jednostki SKU Azure.</span><span class="sxs-lookup"><span data-stu-id="0c0f9-143">Learn more about how [Azure compute units (ACU)](acu.md) can help you compare compute performance across Azure SKUs.</span></span>

## <a name="next-steps"></a><span data-ttu-id="0c0f9-144">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="0c0f9-144">Next steps</span></span>

<span data-ttu-id="0c0f9-145">Dowiedz się więcej na temat hello różnych rozmiarów maszyn wirtualnych, które są dostępne:</span><span class="sxs-lookup"><span data-stu-id="0c0f9-145">Learn more about hello different VM sizes that are available:</span></span>
- [<span data-ttu-id="0c0f9-146">Zastosowania ogólne</span><span class="sxs-lookup"><span data-stu-id="0c0f9-146">General purpose</span></span>](sizes-general.md)
- [<span data-ttu-id="0c0f9-147">Optymalizacja pod kątem obliczeń</span><span class="sxs-lookup"><span data-stu-id="0c0f9-147">Compute optimized</span></span>](sizes-compute.md)
- [<span data-ttu-id="0c0f9-148">Optymalizacja pod kątem pamięci</span><span class="sxs-lookup"><span data-stu-id="0c0f9-148">Memory optimized</span></span>](sizes-memory.md)
- [<span data-ttu-id="0c0f9-149">Optymalizacja pod kątem magazynu</span><span class="sxs-lookup"><span data-stu-id="0c0f9-149">Storage optimized</span></span>](sizes-storage.md)
- [<span data-ttu-id="0c0f9-150">Procesor GPU</span><span class="sxs-lookup"><span data-stu-id="0c0f9-150">GPU</span></span>](sizes-gpu.md)
- [<span data-ttu-id="0c0f9-151">Obliczenia o wysokiej wydajności</span><span class="sxs-lookup"><span data-stu-id="0c0f9-151">High performance compute</span></span>](sizes-hpc.md)



