---
title: "aaaSupportability dodawania istniejącego zestawu dostępności maszyny wirtualne Azure tooan | Dokumentacja firmy Microsoft"
description: "Możliwość obsługi dodawania istniejącego zestawu dostępności tooan maszynach wirtualnych platformy Azure."
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
ms.openlocfilehash: dc2bd86b916f1d1a0a0d4c9e870df829434c96b8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="supportability-of-adding-azure-vms-tooan-existing-availability-set"></a><span data-ttu-id="6fa2c-103">Możliwość obsługi dodawania maszyn wirtualnych platformy Azure tooan istniejącego zestawu dostępności</span><span class="sxs-lookup"><span data-stu-id="6fa2c-103">Supportability of adding Azure VMs tooan existing availability set</span></span>

<span data-ttu-id="6fa2c-104">Czasami mogą wystąpić ograniczenia, po dodaniu nowych maszynach wirtualnych (VM) tooan istniejącego zestawu dostępności.</span><span class="sxs-lookup"><span data-stu-id="6fa2c-104">You may occasionally encounter limitations when you add new virtual machines (VMs) tooan existing availability set.</span></span> <span data-ttu-id="6fa2c-105">Witaj, poniższe informacje wykresu serii maszyn wirtualnych, które można łączyć w hello tego samego zestawu dostępności.</span><span class="sxs-lookup"><span data-stu-id="6fa2c-105">hello following chart details which VM series you can mix in hello same availability set.</span></span>

<span data-ttu-id="6fa2c-106">Oto hello obsługi macierzy toomix różne typy maszyn wirtualnych:</span><span class="sxs-lookup"><span data-stu-id="6fa2c-106">Here is hello supportability matrix toomix different types of VMs:</span></span>

<span data-ttu-id="6fa2c-107">& Serii zestawu dostępności</span><span class="sxs-lookup"><span data-stu-id="6fa2c-107">Series & Availability Set</span></span>|<span data-ttu-id="6fa2c-108">Drugi maszyny Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="6fa2c-108">Second VM</span></span>|<span data-ttu-id="6fa2c-109">A</span><span class="sxs-lookup"><span data-stu-id="6fa2c-109">A</span></span>|<span data-ttu-id="6fa2c-110">Av2</span><span class="sxs-lookup"><span data-stu-id="6fa2c-110">Av2</span></span>|<span data-ttu-id="6fa2c-111">D</span><span class="sxs-lookup"><span data-stu-id="6fa2c-111">D</span></span>|<span data-ttu-id="6fa2c-112">Dv2</span><span class="sxs-lookup"><span data-stu-id="6fa2c-112">Dv2</span></span>|<span data-ttu-id="6fa2c-113">Dv3</span><span class="sxs-lookup"><span data-stu-id="6fa2c-113">Dv3</span></span>|
|---|---|---|---|---|---|---|
|<span data-ttu-id="6fa2c-114">Pierwsza maszyna wirtualna</span><span class="sxs-lookup"><span data-stu-id="6fa2c-114">First VM</span></span>|||||||
|<span data-ttu-id="6fa2c-115">A</span><span class="sxs-lookup"><span data-stu-id="6fa2c-115">A</span></span>||<span data-ttu-id="6fa2c-116">OK</span><span class="sxs-lookup"><span data-stu-id="6fa2c-116">OK</span></span>|<span data-ttu-id="6fa2c-117">OK</span><span class="sxs-lookup"><span data-stu-id="6fa2c-117">OK</span></span>|<span data-ttu-id="6fa2c-118">OK</span><span class="sxs-lookup"><span data-stu-id="6fa2c-118">OK</span></span>|<span data-ttu-id="6fa2c-119">OK</span><span class="sxs-lookup"><span data-stu-id="6fa2c-119">OK</span></span>|<span data-ttu-id="6fa2c-120">OK</span><span class="sxs-lookup"><span data-stu-id="6fa2c-120">OK</span></span>|
|<span data-ttu-id="6fa2c-121">Av2</span><span class="sxs-lookup"><span data-stu-id="6fa2c-121">Av2</span></span>||<span data-ttu-id="6fa2c-122">OK</span><span class="sxs-lookup"><span data-stu-id="6fa2c-122">OK</span></span>|<span data-ttu-id="6fa2c-123">OK</span><span class="sxs-lookup"><span data-stu-id="6fa2c-123">OK</span></span>|<span data-ttu-id="6fa2c-124">OK</span><span class="sxs-lookup"><span data-stu-id="6fa2c-124">OK</span></span>|<span data-ttu-id="6fa2c-125">OK</span><span class="sxs-lookup"><span data-stu-id="6fa2c-125">OK</span></span>|<span data-ttu-id="6fa2c-126">OK</span><span class="sxs-lookup"><span data-stu-id="6fa2c-126">OK</span></span>|
|<span data-ttu-id="6fa2c-127">D</span><span class="sxs-lookup"><span data-stu-id="6fa2c-127">D</span></span>||<span data-ttu-id="6fa2c-128">OK</span><span class="sxs-lookup"><span data-stu-id="6fa2c-128">OK</span></span>|<span data-ttu-id="6fa2c-129">OK</span><span class="sxs-lookup"><span data-stu-id="6fa2c-129">OK</span></span>|<span data-ttu-id="6fa2c-130">OK</span><span class="sxs-lookup"><span data-stu-id="6fa2c-130">OK</span></span>|<span data-ttu-id="6fa2c-131">OK</span><span class="sxs-lookup"><span data-stu-id="6fa2c-131">OK</span></span>|<span data-ttu-id="6fa2c-132">OK</span><span class="sxs-lookup"><span data-stu-id="6fa2c-132">OK</span></span>|
|<span data-ttu-id="6fa2c-133">Dv2</span><span class="sxs-lookup"><span data-stu-id="6fa2c-133">Dv2</span></span>||<span data-ttu-id="6fa2c-134">OK</span><span class="sxs-lookup"><span data-stu-id="6fa2c-134">OK</span></span>|<span data-ttu-id="6fa2c-135">OK</span><span class="sxs-lookup"><span data-stu-id="6fa2c-135">OK</span></span>|<span data-ttu-id="6fa2c-136">OK</span><span class="sxs-lookup"><span data-stu-id="6fa2c-136">OK</span></span>|<span data-ttu-id="6fa2c-137">OK</span><span class="sxs-lookup"><span data-stu-id="6fa2c-137">OK</span></span>|<span data-ttu-id="6fa2c-138">OK</span><span class="sxs-lookup"><span data-stu-id="6fa2c-138">OK</span></span>|
|<span data-ttu-id="6fa2c-139">Dv3</span><span class="sxs-lookup"><span data-stu-id="6fa2c-139">Dv3</span></span>||<span data-ttu-id="6fa2c-140">OK</span><span class="sxs-lookup"><span data-stu-id="6fa2c-140">OK</span></span>|<span data-ttu-id="6fa2c-141">OK</span><span class="sxs-lookup"><span data-stu-id="6fa2c-141">OK</span></span>|<span data-ttu-id="6fa2c-142">OK</span><span class="sxs-lookup"><span data-stu-id="6fa2c-142">OK</span></span>|<span data-ttu-id="6fa2c-143">OK</span><span class="sxs-lookup"><span data-stu-id="6fa2c-143">OK</span></span>|<span data-ttu-id="6fa2c-144">OK</span><span class="sxs-lookup"><span data-stu-id="6fa2c-144">OK</span></span>|

<span data-ttu-id="6fa2c-145">Wszystkie inne serii nie może być w hello tego samego zestawu danych o dostępności, ponieważ wymagają one konkretnego sprzętu.</span><span class="sxs-lookup"><span data-stu-id="6fa2c-145">All other series could not be in hello same availability set because they require a specific hardware.</span></span>
