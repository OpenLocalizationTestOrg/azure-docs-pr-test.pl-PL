---
title: "Ustaw obsługi dodawania maszyn wirtualnych platformy Azure do istniejących dostępności | Dokumentacja firmy Microsoft"
description: "Możliwość obsługi dodawania maszyn wirtualnych platformy Azure do istniejącego zestawu dostępności."
services: virtual-machines-linux
documentationcenter: 
author: Deland-Han
manager: cshepard
editor: 
ms.assetid: 
ms.service: virtual-machines
ms.workload: virtual-machines
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 7/15/2017
ms.author: delhan
ms.openlocfilehash: 3ce9b8a79108cb9e57df14bcb3354cc637193233
ms.sourcegitcommit: 422efcbac5b6b68295064bd545132fcc98349d01
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/29/2017
---
# <a name="supportability-of-adding-azure-vms-to-an-existing-availability-set"></a><span data-ttu-id="2be99-103">Możliwość obsługi dodawania maszyn wirtualnych platformy Azure do istniejącego zestawu dostępności</span><span class="sxs-lookup"><span data-stu-id="2be99-103">Supportability of adding Azure VMs to an existing availability set</span></span>

<span data-ttu-id="2be99-104">Można czasami napotkać ograniczenia podczas dodawania nowych maszyn wirtualnych (VM) do istniejącego zestawu dostępności.</span><span class="sxs-lookup"><span data-stu-id="2be99-104">You may occasionally encounter limitations when you add new virtual machines (VMs) to an existing availability set.</span></span> <span data-ttu-id="2be99-105">Poniższy schemat zawiera szczegóły serii maszyn wirtualnych, które można łączyć w tym samym zestawie dostępności.</span><span class="sxs-lookup"><span data-stu-id="2be99-105">The following chart details which VM series you can mix in the same availability set.</span></span>

<span data-ttu-id="2be99-106">Oto macierz obsługi mieszać różnego rodzaju maszyn wirtualnych:</span><span class="sxs-lookup"><span data-stu-id="2be99-106">Here is the supportability matrix to mix different types of VMs:</span></span>

<span data-ttu-id="2be99-107">& Serii zestawu dostępności</span><span class="sxs-lookup"><span data-stu-id="2be99-107">Series & Availability Set</span></span>|<span data-ttu-id="2be99-108">Drugi maszyny Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="2be99-108">Second VM</span></span>|<span data-ttu-id="2be99-109">A</span><span class="sxs-lookup"><span data-stu-id="2be99-109">A</span></span>|<span data-ttu-id="2be99-110">Av2</span><span class="sxs-lookup"><span data-stu-id="2be99-110">Av2</span></span>|<span data-ttu-id="2be99-111">D</span><span class="sxs-lookup"><span data-stu-id="2be99-111">D</span></span>|<span data-ttu-id="2be99-112">Dv2</span><span class="sxs-lookup"><span data-stu-id="2be99-112">Dv2</span></span>|<span data-ttu-id="2be99-113">Dv3</span><span class="sxs-lookup"><span data-stu-id="2be99-113">Dv3</span></span>|
|---|---|---|---|---|---|---|
|<span data-ttu-id="2be99-114">Pierwsza maszyna wirtualna</span><span class="sxs-lookup"><span data-stu-id="2be99-114">First VM</span></span>|||||||
|<span data-ttu-id="2be99-115">A</span><span class="sxs-lookup"><span data-stu-id="2be99-115">A</span></span>||<span data-ttu-id="2be99-116">OK</span><span class="sxs-lookup"><span data-stu-id="2be99-116">OK</span></span>|<span data-ttu-id="2be99-117">OK</span><span class="sxs-lookup"><span data-stu-id="2be99-117">OK</span></span>|<span data-ttu-id="2be99-118">OK</span><span class="sxs-lookup"><span data-stu-id="2be99-118">OK</span></span>|<span data-ttu-id="2be99-119">OK</span><span class="sxs-lookup"><span data-stu-id="2be99-119">OK</span></span>|<span data-ttu-id="2be99-120">OK</span><span class="sxs-lookup"><span data-stu-id="2be99-120">OK</span></span>|
|<span data-ttu-id="2be99-121">Av2</span><span class="sxs-lookup"><span data-stu-id="2be99-121">Av2</span></span>||<span data-ttu-id="2be99-122">OK</span><span class="sxs-lookup"><span data-stu-id="2be99-122">OK</span></span>|<span data-ttu-id="2be99-123">OK</span><span class="sxs-lookup"><span data-stu-id="2be99-123">OK</span></span>|<span data-ttu-id="2be99-124">OK</span><span class="sxs-lookup"><span data-stu-id="2be99-124">OK</span></span>|<span data-ttu-id="2be99-125">OK</span><span class="sxs-lookup"><span data-stu-id="2be99-125">OK</span></span>|<span data-ttu-id="2be99-126">OK</span><span class="sxs-lookup"><span data-stu-id="2be99-126">OK</span></span>|
|<span data-ttu-id="2be99-127">D</span><span class="sxs-lookup"><span data-stu-id="2be99-127">D</span></span>||<span data-ttu-id="2be99-128">OK</span><span class="sxs-lookup"><span data-stu-id="2be99-128">OK</span></span>|<span data-ttu-id="2be99-129">OK</span><span class="sxs-lookup"><span data-stu-id="2be99-129">OK</span></span>|<span data-ttu-id="2be99-130">OK</span><span class="sxs-lookup"><span data-stu-id="2be99-130">OK</span></span>|<span data-ttu-id="2be99-131">OK</span><span class="sxs-lookup"><span data-stu-id="2be99-131">OK</span></span>|<span data-ttu-id="2be99-132">OK</span><span class="sxs-lookup"><span data-stu-id="2be99-132">OK</span></span>|
|<span data-ttu-id="2be99-133">Dv2</span><span class="sxs-lookup"><span data-stu-id="2be99-133">Dv2</span></span>||<span data-ttu-id="2be99-134">OK</span><span class="sxs-lookup"><span data-stu-id="2be99-134">OK</span></span>|<span data-ttu-id="2be99-135">OK</span><span class="sxs-lookup"><span data-stu-id="2be99-135">OK</span></span>|<span data-ttu-id="2be99-136">OK</span><span class="sxs-lookup"><span data-stu-id="2be99-136">OK</span></span>|<span data-ttu-id="2be99-137">OK</span><span class="sxs-lookup"><span data-stu-id="2be99-137">OK</span></span>|<span data-ttu-id="2be99-138">OK</span><span class="sxs-lookup"><span data-stu-id="2be99-138">OK</span></span>|
|<span data-ttu-id="2be99-139">Dv3</span><span class="sxs-lookup"><span data-stu-id="2be99-139">Dv3</span></span>||<span data-ttu-id="2be99-140">OK</span><span class="sxs-lookup"><span data-stu-id="2be99-140">OK</span></span>|<span data-ttu-id="2be99-141">OK</span><span class="sxs-lookup"><span data-stu-id="2be99-141">OK</span></span>|<span data-ttu-id="2be99-142">OK</span><span class="sxs-lookup"><span data-stu-id="2be99-142">OK</span></span>|<span data-ttu-id="2be99-143">OK</span><span class="sxs-lookup"><span data-stu-id="2be99-143">OK</span></span>|<span data-ttu-id="2be99-144">OK</span><span class="sxs-lookup"><span data-stu-id="2be99-144">OK</span></span>|

<span data-ttu-id="2be99-145">Wszystkie inne serii nie można w tym samym zestawie, ponieważ wymagają one konkretnego sprzętu dostępności.</span><span class="sxs-lookup"><span data-stu-id="2be99-145">All other series could not be in the same availability set because they require a specific hardware.</span></span>