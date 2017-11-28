---
title: "Migrowanie klasyczne maszyny Wirtualnej do dysków zarządzanych w ARM maszyny Wirtualnej | Dokumentacja firmy Microsoft"
description: "Przeprowadź migrację jednej maszyny Wirtualnej platformy Azure z klasycznym modelu wdrażania do zarządzanych dysków w modelu wdrażania usługi Resource Manager."
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 06/15/2017
ms.author: cynthn
ms.openlocfilehash: 82389834d85981c0ed71bdcc891fbfdbe1377654
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
# <a name="manually-migrate-a-classic-vm-to-a-new-arm-managed-disk-vm-from-the-vhd"></a><span data-ttu-id="5646d-103">Ręcznie Migrowanie klasyczne maszyny Wirtualnej do nowej ARM zarządzane dysku maszyny Wirtualnej z dysku VHD</span><span class="sxs-lookup"><span data-stu-id="5646d-103">Manually migrate a Classic VM to a new ARM Managed Disk VM from the VHD</span></span> 


<span data-ttu-id="5646d-104">Ta sekcja pomoże Ci do dokonania migracji istniejących maszyn wirtualnych platformy Azure z klasycznym modelu wdrażania do [dysków zarządzanych](managed-disks-overview.md) w modelu wdrażania usługi Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="5646d-104">This section helps you to migrate your existing Azure VMs from the classic deployment model to [Managed Disks](managed-disks-overview.md) in the Resource Manager deployment model.</span></span>


## <a name="plan-for-the-migration-to-managed-disks"></a><span data-ttu-id="5646d-105">Planowanie migracji do zarządzanych dysków</span><span class="sxs-lookup"><span data-stu-id="5646d-105">Plan for the migration to Managed Disks</span></span>

<span data-ttu-id="5646d-106">Ta sekcja umożliwia podjęcie najlepszych decyzji w typach maszyny Wirtualnej i dysku.</span><span class="sxs-lookup"><span data-stu-id="5646d-106">This section helps you to make the best decision on VM and disk types.</span></span>


### <a name="location"></a><span data-ttu-id="5646d-107">Lokalizacja</span><span class="sxs-lookup"><span data-stu-id="5646d-107">Location</span></span>

<span data-ttu-id="5646d-108">Wybierz lokalizację, w której są dostępne dyski zarządzanych Azure.</span><span class="sxs-lookup"><span data-stu-id="5646d-108">Pick a location where Azure Managed Disks are available.</span></span> <span data-ttu-id="5646d-109">W przypadku migracji dysków zarządzanych w warstwie Premium również upewnij się, że magazyn w warstwie Premium jest dostępna w regionie, w którym jest planowana migracja do.</span><span class="sxs-lookup"><span data-stu-id="5646d-109">If you are migrating to Premium Managed Disks, also ensure that Premium storage is available in the region where you are planning to migrate to.</span></span> <span data-ttu-id="5646d-110">Zobacz [byRegion usług Azure](https://azure.microsoft.com/regions/#services) aktualne informacje o dostępnych lokalizacji.</span><span class="sxs-lookup"><span data-stu-id="5646d-110">See [Azure Services byRegion](https://azure.microsoft.com/regions/#services) for up-to-date information on available locations.</span></span>

### <a name="vm-sizes"></a><span data-ttu-id="5646d-111">Rozmiary maszyn wirtualnych</span><span class="sxs-lookup"><span data-stu-id="5646d-111">VM sizes</span></span>

<span data-ttu-id="5646d-112">W przypadku migracji dysków zarządzanych w warstwie Premium, należy zaktualizować rozmiaru maszyny wirtualnej do magazyn w warstwie Premium obsługuje rozmiaru dostępna w regionie, w którym znajduje się maszyna wirtualna.</span><span class="sxs-lookup"><span data-stu-id="5646d-112">If you are migrating to Premium Managed Disks, you have to update the size of the VM to Premium Storage capable size available in the region where VM is located.</span></span> <span data-ttu-id="5646d-113">Przejrzyj rozmiarów maszyn wirtualnych, które są funkcją Magazyn w warstwie Premium.</span><span class="sxs-lookup"><span data-stu-id="5646d-113">Review the VM sizes that are Premium Storage capable.</span></span> <span data-ttu-id="5646d-114">Specyfikacje rozmiaru maszyny Wirtualnej platformy Azure są wymienione w [rozmiary maszyn wirtualnych](sizes.md).</span><span class="sxs-lookup"><span data-stu-id="5646d-114">The Azure VM size specifications are listed in [Sizes for virtual machines](sizes.md).</span></span>
<span data-ttu-id="5646d-115">Przejrzyj charakterystyki wydajności maszyn wirtualnych, które pracy z magazyn w warstwie Premium i wybierz najbardziej odpowiedni rozmiar maszyny Wirtualnej, który najlepiej odpowiada obciążenie.</span><span class="sxs-lookup"><span data-stu-id="5646d-115">Review the performance characteristics of virtual machines that work with Premium Storage and choose the most appropriate VM size that best suits your workload.</span></span> <span data-ttu-id="5646d-116">Należy upewnić się, że wystarczającą przepustowość dostępne na maszynie Wirtualnej do kierowania ruchu dysku.</span><span class="sxs-lookup"><span data-stu-id="5646d-116">Make sure that there is sufficient bandwidth available on your VM to drive the disk traffic.</span></span>

### <a name="disk-sizes"></a><span data-ttu-id="5646d-117">Rozmiary dysków</span><span class="sxs-lookup"><span data-stu-id="5646d-117">Disk sizes</span></span>

<span data-ttu-id="5646d-118">**Dysków zarządzanych w warstwie Premium**</span><span class="sxs-lookup"><span data-stu-id="5646d-118">**Premium Managed Disks**</span></span>

<span data-ttu-id="5646d-119">Istnieje siedem typów dysków zarządzane premium, które mogą być używane z maszyny Wirtualnej i każdy ma określonych IOPs i przepływność limity.</span><span class="sxs-lookup"><span data-stu-id="5646d-119">There are seven types of premium Managed disks that can be used with your VM and each has specific IOPs and throughput limits.</span></span> <span data-ttu-id="5646d-120">Należy wziąć pod uwagę następujące limity podczas wybierania typu dysku Premium dla maszyny Wirtualnej na podstawie potrzeb aplikacji pod względem wydajności, wydajności, skalowalności i ładuje godzinami szczytu.</span><span class="sxs-lookup"><span data-stu-id="5646d-120">Consider these limits when choosing the Premium disk type for your VM based on the needs of your application in terms of capacity, performance, scalability, and peak loads.</span></span>

| <span data-ttu-id="5646d-121">Typ dysków Premium</span><span class="sxs-lookup"><span data-stu-id="5646d-121">Premium Disks Type</span></span>  | <span data-ttu-id="5646d-122">P4</span><span class="sxs-lookup"><span data-stu-id="5646d-122">P4</span></span>    | <span data-ttu-id="5646d-123">P6</span><span class="sxs-lookup"><span data-stu-id="5646d-123">P6</span></span>    | <span data-ttu-id="5646d-124">P10</span><span class="sxs-lookup"><span data-stu-id="5646d-124">P10</span></span>   | <span data-ttu-id="5646d-125">P20</span><span class="sxs-lookup"><span data-stu-id="5646d-125">P20</span></span>   | <span data-ttu-id="5646d-126">P30</span><span class="sxs-lookup"><span data-stu-id="5646d-126">P30</span></span>   | <span data-ttu-id="5646d-127">P40</span><span class="sxs-lookup"><span data-stu-id="5646d-127">P40</span></span>   | <span data-ttu-id="5646d-128">P50</span><span class="sxs-lookup"><span data-stu-id="5646d-128">P50</span></span>   | 
|---------------------|-------|-------|-------|-------|-------|-------|-------|
| <span data-ttu-id="5646d-129">Rozmiar dysku</span><span class="sxs-lookup"><span data-stu-id="5646d-129">Disk size</span></span>           | <span data-ttu-id="5646d-130">128 GB</span><span class="sxs-lookup"><span data-stu-id="5646d-130">128 GB</span></span>| <span data-ttu-id="5646d-131">512 GB</span><span class="sxs-lookup"><span data-stu-id="5646d-131">512 GB</span></span>| <span data-ttu-id="5646d-132">128 GB</span><span class="sxs-lookup"><span data-stu-id="5646d-132">128 GB</span></span>| <span data-ttu-id="5646d-133">512 GB</span><span class="sxs-lookup"><span data-stu-id="5646d-133">512 GB</span></span>            | <span data-ttu-id="5646d-134">1024 GB (1 TB)</span><span class="sxs-lookup"><span data-stu-id="5646d-134">1024 GB (1 TB)</span></span>    | <span data-ttu-id="5646d-135">2048 GB (2 TB)</span><span class="sxs-lookup"><span data-stu-id="5646d-135">2048 GB (2 TB)</span></span>    | <span data-ttu-id="5646d-136">4095 GB (4 TB)</span><span class="sxs-lookup"><span data-stu-id="5646d-136">4095 GB (4 TB)</span></span>    | 
| <span data-ttu-id="5646d-137">Liczba operacji wejścia/wyjścia na sekundę na dysk</span><span class="sxs-lookup"><span data-stu-id="5646d-137">IOPS per disk</span></span>       | <span data-ttu-id="5646d-138">120</span><span class="sxs-lookup"><span data-stu-id="5646d-138">120</span></span>   | <span data-ttu-id="5646d-139">240</span><span class="sxs-lookup"><span data-stu-id="5646d-139">240</span></span>   | <span data-ttu-id="5646d-140">500</span><span class="sxs-lookup"><span data-stu-id="5646d-140">500</span></span>   | <span data-ttu-id="5646d-141">2300</span><span class="sxs-lookup"><span data-stu-id="5646d-141">2300</span></span>              | <span data-ttu-id="5646d-142">5000</span><span class="sxs-lookup"><span data-stu-id="5646d-142">5000</span></span>              | <span data-ttu-id="5646d-143">7500</span><span class="sxs-lookup"><span data-stu-id="5646d-143">7500</span></span>              | <span data-ttu-id="5646d-144">7500</span><span class="sxs-lookup"><span data-stu-id="5646d-144">7500</span></span>              | 
| <span data-ttu-id="5646d-145">Przepływność na dysk</span><span class="sxs-lookup"><span data-stu-id="5646d-145">Throughput per disk</span></span> | <span data-ttu-id="5646d-146">25 MB na sekundę</span><span class="sxs-lookup"><span data-stu-id="5646d-146">25 MB per second</span></span>  | <span data-ttu-id="5646d-147">50 MB / s</span><span class="sxs-lookup"><span data-stu-id="5646d-147">50 MB per second</span></span>  | <span data-ttu-id="5646d-148">100 MB na sekundę</span><span class="sxs-lookup"><span data-stu-id="5646d-148">100 MB per second</span></span> | <span data-ttu-id="5646d-149">150 MB na sekundę</span><span class="sxs-lookup"><span data-stu-id="5646d-149">150 MB per second</span></span> | <span data-ttu-id="5646d-150">200 MB / s</span><span class="sxs-lookup"><span data-stu-id="5646d-150">200 MB per second</span></span> | <span data-ttu-id="5646d-151">250 MB na sekundę</span><span class="sxs-lookup"><span data-stu-id="5646d-151">250 MB per second</span></span> | <span data-ttu-id="5646d-152">250 MB na sekundę</span><span class="sxs-lookup"><span data-stu-id="5646d-152">250 MB per second</span></span> | 

<span data-ttu-id="5646d-153">**Dyski standardowe zarządzanych**</span><span class="sxs-lookup"><span data-stu-id="5646d-153">**Standard Managed Disks**</span></span>

<span data-ttu-id="5646d-154">Istnieje siedem typów zarządzane standardowych dysków, które mogą być używane z maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="5646d-154">There are seven types of Standard Managed disks that can be used with your VM.</span></span> <span data-ttu-id="5646d-155">Każdej z nich ma inną wydajności, ale ma tego samego IOPS i limity przepustowości.</span><span class="sxs-lookup"><span data-stu-id="5646d-155">Each of them have different capacity but have same IOPS and throughput limits.</span></span> <span data-ttu-id="5646d-156">Wybierz typ dyski standardowe zarządzane na podstawie potrzeb wydajność aplikacji.</span><span class="sxs-lookup"><span data-stu-id="5646d-156">Choose the type of Standard Managed disks based on the capacity needs of your application.</span></span>

| <span data-ttu-id="5646d-157">Typ dysku standardowego</span><span class="sxs-lookup"><span data-stu-id="5646d-157">Standard Disk Type</span></span>  | <span data-ttu-id="5646d-158">S4</span><span class="sxs-lookup"><span data-stu-id="5646d-158">S4</span></span>               | <span data-ttu-id="5646d-159">S6</span><span class="sxs-lookup"><span data-stu-id="5646d-159">S6</span></span>               | <span data-ttu-id="5646d-160">S10</span><span class="sxs-lookup"><span data-stu-id="5646d-160">S10</span></span>              | <span data-ttu-id="5646d-161">S20</span><span class="sxs-lookup"><span data-stu-id="5646d-161">S20</span></span>              | <span data-ttu-id="5646d-162">S30</span><span class="sxs-lookup"><span data-stu-id="5646d-162">S30</span></span>              | <span data-ttu-id="5646d-163">S40</span><span class="sxs-lookup"><span data-stu-id="5646d-163">S40</span></span>              | <span data-ttu-id="5646d-164">S50</span><span class="sxs-lookup"><span data-stu-id="5646d-164">S50</span></span>              | 
|---------------------|---------------------|---------------------|------------------|------------------|------------------|------------------|------------------| 
| <span data-ttu-id="5646d-165">Rozmiar dysku</span><span class="sxs-lookup"><span data-stu-id="5646d-165">Disk size</span></span>           | <span data-ttu-id="5646d-166">30 GB</span><span class="sxs-lookup"><span data-stu-id="5646d-166">30 GB</span></span>            | <span data-ttu-id="5646d-167">64 GB</span><span class="sxs-lookup"><span data-stu-id="5646d-167">64 GB</span></span>            | <span data-ttu-id="5646d-168">128 GB</span><span class="sxs-lookup"><span data-stu-id="5646d-168">128 GB</span></span>           | <span data-ttu-id="5646d-169">512 GB</span><span class="sxs-lookup"><span data-stu-id="5646d-169">512 GB</span></span>           | <span data-ttu-id="5646d-170">1024 GB (1 TB)</span><span class="sxs-lookup"><span data-stu-id="5646d-170">1024 GB (1 TB)</span></span>   | <span data-ttu-id="5646d-171">2048 GB (2TB)</span><span class="sxs-lookup"><span data-stu-id="5646d-171">2048 GB (2TB)</span></span>    | <span data-ttu-id="5646d-172">4095 GB (4 TB)</span><span class="sxs-lookup"><span data-stu-id="5646d-172">4095 GB (4 TB)</span></span>   | 
| <span data-ttu-id="5646d-173">Liczba operacji wejścia/wyjścia na sekundę na dysk</span><span class="sxs-lookup"><span data-stu-id="5646d-173">IOPS per disk</span></span>       | <span data-ttu-id="5646d-174">500</span><span class="sxs-lookup"><span data-stu-id="5646d-174">500</span></span>              | <span data-ttu-id="5646d-175">500</span><span class="sxs-lookup"><span data-stu-id="5646d-175">500</span></span>              | <span data-ttu-id="5646d-176">500</span><span class="sxs-lookup"><span data-stu-id="5646d-176">500</span></span>              | <span data-ttu-id="5646d-177">500</span><span class="sxs-lookup"><span data-stu-id="5646d-177">500</span></span>              | <span data-ttu-id="5646d-178">500</span><span class="sxs-lookup"><span data-stu-id="5646d-178">500</span></span>              | <span data-ttu-id="5646d-179">500</span><span class="sxs-lookup"><span data-stu-id="5646d-179">500</span></span>             | <span data-ttu-id="5646d-180">500</span><span class="sxs-lookup"><span data-stu-id="5646d-180">500</span></span>              | 
| <span data-ttu-id="5646d-181">Przepływność na dysk</span><span class="sxs-lookup"><span data-stu-id="5646d-181">Throughput per disk</span></span> | <span data-ttu-id="5646d-182">60 MB na sekundę</span><span class="sxs-lookup"><span data-stu-id="5646d-182">60 MB per second</span></span> | <span data-ttu-id="5646d-183">60 MB na sekundę</span><span class="sxs-lookup"><span data-stu-id="5646d-183">60 MB per second</span></span> | <span data-ttu-id="5646d-184">60 MB na sekundę</span><span class="sxs-lookup"><span data-stu-id="5646d-184">60 MB per second</span></span> | <span data-ttu-id="5646d-185">60 MB na sekundę</span><span class="sxs-lookup"><span data-stu-id="5646d-185">60 MB per second</span></span> | <span data-ttu-id="5646d-186">60 MB na sekundę</span><span class="sxs-lookup"><span data-stu-id="5646d-186">60 MB per second</span></span> | <span data-ttu-id="5646d-187">60 MB na sekundę</span><span class="sxs-lookup"><span data-stu-id="5646d-187">60 MB per second</span></span> | <span data-ttu-id="5646d-188">60 MB na sekundę</span><span class="sxs-lookup"><span data-stu-id="5646d-188">60 MB per second</span></span> | 


### <a name="disk-caching-policy"></a><span data-ttu-id="5646d-189">Dyskowej pamięci podręcznej zasad</span><span class="sxs-lookup"><span data-stu-id="5646d-189">Disk caching policy</span></span> 

<span data-ttu-id="5646d-190">**Dysków zarządzanych w warstwie Premium**</span><span class="sxs-lookup"><span data-stu-id="5646d-190">**Premium Managed Disks**</span></span>

<span data-ttu-id="5646d-191">Domyślnie jest dyskowej pamięci podręcznej zasad *tylko do odczytu* dla wszystkich danych dysków Premium i *odczytu i zapisu* dla dysku systemu operacyjnego Premium dołączony do maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="5646d-191">By default, disk caching policy is *Read-Only* for all the Premium data disks, and *Read-Write* for the Premium operating system disk attached to the VM.</span></span> <span data-ttu-id="5646d-192">To ustawienie konfiguracji jest zalecane w celu osiągnięcia optymalnej wydajności dla aplikacji systemu IOs.</span><span class="sxs-lookup"><span data-stu-id="5646d-192">This configuration setting is recommended to achieve the optimal performance for your application’s IOs.</span></span> <span data-ttu-id="5646d-193">W przypadku dysków ciężki zapisu lub w trybie tylko do zapisu danych (takich jak pliki dziennika programu SQL Server) Wyłącz buforowanie dysku, dzięki czemu można osiągnąć lepszą wydajność aplikacji.</span><span class="sxs-lookup"><span data-stu-id="5646d-193">For write-heavy or write-only data disks (such as SQL Server log files), disable disk caching so that you can achieve better application performance.</span></span>

### <a name="pricing"></a><span data-ttu-id="5646d-194">Cennik</span><span class="sxs-lookup"><span data-stu-id="5646d-194">Pricing</span></span>

<span data-ttu-id="5646d-195">Przegląd [ceny dysków zarządzanych](https://azure.microsoft.com/en-us/pricing/details/managed-disks/).</span><span class="sxs-lookup"><span data-stu-id="5646d-195">Review the [pricing for Managed Disks](https://azure.microsoft.com/en-us/pricing/details/managed-disks/).</span></span> <span data-ttu-id="5646d-196">Cen dysków zarządzanych w warstwie Premium jest taka sama jak niezarządzane dysków Premium.</span><span class="sxs-lookup"><span data-stu-id="5646d-196">Pricing of Premium Managed Disks is same as the Premium Unmanaged Disks.</span></span> <span data-ttu-id="5646d-197">Ale ceny dyski standardowe zarządzanych jest inny niż dyski standardowe niezarządzane.</span><span class="sxs-lookup"><span data-stu-id="5646d-197">But pricing for Standard Managed Disks is different than Standard Unmanaged Disks.</span></span>


## <a name="checklist"></a><span data-ttu-id="5646d-198">Lista kontrolna</span><span class="sxs-lookup"><span data-stu-id="5646d-198">Checklist</span></span>

1.  <span data-ttu-id="5646d-199">W przypadku migracji do zarządzanych dysków Premium upewnij się, że jest dostępna w regionie, który w przypadku migracji do.</span><span class="sxs-lookup"><span data-stu-id="5646d-199">If you are migrating to Premium Managed Disks, make sure it is available in the region you are migrating to.</span></span>

2.  <span data-ttu-id="5646d-200">Zdecyduj, nowej serii maszyny Wirtualnej, który będzie używany.</span><span class="sxs-lookup"><span data-stu-id="5646d-200">Decide the new VM series you will be using.</span></span> <span data-ttu-id="5646d-201">Magazyn w warstwie Premium obsługuje powinno być migrowania do dysków zarządzanych w warstwie Premium.</span><span class="sxs-lookup"><span data-stu-id="5646d-201">It should be a Premium Storage capable if you are migrating to Premium Managed Disks.</span></span>

3.  <span data-ttu-id="5646d-202">Określ dokładnie rozmiar maszyny Wirtualnej, który będzie używany, które są dostępne w regionie, w którym w przypadku migracji do.</span><span class="sxs-lookup"><span data-stu-id="5646d-202">Decide the exact VM size you will use which are available in the region you are migrating to.</span></span> <span data-ttu-id="5646d-203">Rozmiar maszyny Wirtualnej musi być wystarczająco duży, aby obsługiwał liczba dysków danych, do których masz.</span><span class="sxs-lookup"><span data-stu-id="5646d-203">VM size needs to be large enough to support the number of data disks you have.</span></span> <span data-ttu-id="5646d-204">Na przykład jeśli masz cztery dysków danych maszyny Wirtualnej musi mieć co najmniej dwa rdzenie.</span><span class="sxs-lookup"><span data-stu-id="5646d-204">For example, if you have four data disks, the VM must have two or more cores.</span></span> <span data-ttu-id="5646d-205">Należy również rozważyć przetwarzania zasilania, pamięci i musi przepustowości sieci.</span><span class="sxs-lookup"><span data-stu-id="5646d-205">Also, consider processing power, memory and network bandwidth needs.</span></span>

4.  <span data-ttu-id="5646d-206">Mieć bieżące szczegóły maszyny Wirtualnej pod ręką, w tym listę dysków i odpowiednie obiekty BLOB dysków VHD.</span><span class="sxs-lookup"><span data-stu-id="5646d-206">Have the current VM details handy, including the list of disks and corresponding VHD blobs.</span></span>

<span data-ttu-id="5646d-207">Przygotowanie aplikacji dla przestoju.</span><span class="sxs-lookup"><span data-stu-id="5646d-207">Prepare your application for downtime.</span></span> <span data-ttu-id="5646d-208">Przeprowadzenie czystej migracji, należy zatrzymać wszystkie przetwarzania w systemie.</span><span class="sxs-lookup"><span data-stu-id="5646d-208">To do a clean migration, you have to stop all the processing in the current system.</span></span> <span data-ttu-id="5646d-209">Następnie możesz pobrać go do spójnego stanu, które można migrować do nowej platformie.</span><span class="sxs-lookup"><span data-stu-id="5646d-209">Only then you can get it to consistent state which you can migrate to the new platform.</span></span> <span data-ttu-id="5646d-210">Czas trwania przestoju zależy od ilości danych na dyskach, aby przeprowadzić migrację.</span><span class="sxs-lookup"><span data-stu-id="5646d-210">Downtime duration depends on the amount of data in the disks to migrate.</span></span>


## <a name="migrate-the-vm"></a><span data-ttu-id="5646d-211">Migrowanie maszyny Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="5646d-211">Migrate the VM</span></span>

<span data-ttu-id="5646d-212">Przygotowanie aplikacji dla przestoju.</span><span class="sxs-lookup"><span data-stu-id="5646d-212">Prepare your application for downtime.</span></span> <span data-ttu-id="5646d-213">Przeprowadzenie czystej migracji, należy zatrzymać wszystkie przetwarzania w systemie.</span><span class="sxs-lookup"><span data-stu-id="5646d-213">To do a clean migration, you have to stop all the processing in the current system.</span></span> <span data-ttu-id="5646d-214">Następnie możesz pobrać go do spójnego stanu, które można migrować do nowej platformie.</span><span class="sxs-lookup"><span data-stu-id="5646d-214">Only then you can get it to consistent state which you can migrate to the new platform.</span></span> <span data-ttu-id="5646d-215">Czas trwania przestoju zależy od ilości danych na dyskach, aby przeprowadzić migrację.</span><span class="sxs-lookup"><span data-stu-id="5646d-215">Downtime duration depends the amount of data in the disks to migrate.</span></span>


1.  <span data-ttu-id="5646d-216">Najpierw należy ustawić wspólne parametry:</span><span class="sxs-lookup"><span data-stu-id="5646d-216">First, set the common parameters:</span></span>

    ```powershell
    $resourceGroupName = 'yourResourceGroupName'
    
    $location = 'your location' 
    
    $virtualNetworkName = 'yourExistingVirtualNetworkName'
    
    $virtualMachineName = 'yourVMName'
    
    $virtualMachineSize = 'Standard_DS3'
    
    $adminUserName = "youradminusername"
    
    $adminPassword = "yourpassword" | ConvertTo-SecureString -AsPlainText -Force
    
    $imageName = 'yourImageName'
    
    $osVhdUri = 'https://storageaccount.blob.core.windows.net/vhdcontainer/osdisk.vhd'
    
    $dataVhdUri = 'https://storageaccount.blob.core.windows.net/vhdcontainer/datadisk1.vhd'
    
    $dataDiskName = 'dataDisk1'
    ```

2.  <span data-ttu-id="5646d-217">Tworzenie zarządzanego dysku systemu operacyjnego przy użyciu wirtualnego dysku twardego z klasycznym maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="5646d-217">Create a managed OS disk using the VHD from the classic VM.</span></span>

    <span data-ttu-id="5646d-218">Upewnij się, że podano pełny identyfikator URI wirtualnego dysku twardego systemu operacyjnego do parametru $osVhdUri.</span><span class="sxs-lookup"><span data-stu-id="5646d-218">Ensure that you have provided the complete URI of the OS VHD to the $osVhdUri parameter.</span></span> <span data-ttu-id="5646d-219">Wprowadź też **- AccountType** jako **PremiumLRS** lub **StandardLRS** na podstawie typu dysków (Premium lub Standard) w przypadku migracji do.</span><span class="sxs-lookup"><span data-stu-id="5646d-219">Also, enter **-AccountType** as **PremiumLRS** or **StandardLRS** based on type of disks (Premium or Standard) you are migrating to.</span></span>

    ```powershell
    $osDisk = New-AzureRmDisk -DiskName $osDiskName -Disk (New-AzureRmDiskConfig '
    -AccountType PremiumLRS -Location $location -CreateOption Import -SourceUri $osVhdUri) '
    -ResourceGroupName $resourceGroupName
    ```

3.  <span data-ttu-id="5646d-220">Dołączenie dysku systemu operacyjnego do nowej maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="5646d-220">Attach the OS disk to the new VM.</span></span>

    ```powershell
    $VirtualMachine = New-AzureRmVMConfig -VMName $virtualMachineName -VMSize $virtualMachineSize
    $VirtualMachine = Set-AzureRmVMOSDisk -VM $VirtualMachine -ManagedDiskId $osDisk.Id '
    -StorageAccountType PremiumLRS -DiskSizeInGB 128 -CreateOption Attach -Windows
    ```

4.  <span data-ttu-id="5646d-221">Tworzenie dysku danych zarządzanych z pliku VHD danych i dodaj go do nowej maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="5646d-221">Create a managed data disk from the data VHD file and add it to the new VM.</span></span>

    ```powershell
    $dataDisk1 = New-AzureRmDisk -DiskName $dataDiskName -Disk (New-AzureRmDiskConfig '
    -AccountType PremiumLRS -Location $location -CreationDataCreateOption Import '
    -SourceUri $dataVhdUri ) -ResourceGroupName $resourceGroupName
    
    $VirtualMachine = Add-AzureRmVMDataDisk -VM $VirtualMachine -Name $dataDiskName '
    -CreateOption Attach -ManagedDiskId $dataDisk1.Id -Lun 1
    ```

5.  <span data-ttu-id="5646d-222">Tworzenie nowej maszyny Wirtualnej przez ustawienie publicznego adresu IP, sieci wirtualnej i karty sieciowej.</span><span class="sxs-lookup"><span data-stu-id="5646d-222">Create the new VM by setting public IP, Virtual Network and NIC.</span></span>

    ```powershell
    $publicIp = New-AzureRmPublicIpAddress -Name ($VirtualMachineName.ToLower()+'_ip') '
    -ResourceGroupName $resourceGroupName -Location $location -AllocationMethod Dynamic
    
    $vnet = Get-AzureRmVirtualNetwork -Name $virtualNetworkName -ResourceGroupName $resourceGroupName
    
    $nic = New-AzureRmNetworkInterface -Name ($VirtualMachineName.ToLower()+'_nic') '
    -ResourceGroupName $resourceGroupName -Location $location -SubnetId $vnet.Subnets[0].Id '
    -PublicIpAddressId $publicIp.Id
    
    $VirtualMachine = Add-AzureRmVMNetworkInterface -VM $VirtualMachine -Id $nic.Id
    
    New-AzureRmVM -VM $VirtualMachine -ResourceGroupName $resourceGroupName -Location $location
    ```

> [!NOTE]
><span data-ttu-id="5646d-223">Mogą istnieć dodatkowe kroki niezbędne do obsługi tej aplikacji, która jest nie obejmuje się w tym przewodniku.</span><span class="sxs-lookup"><span data-stu-id="5646d-223">There may be additional steps necessary to support your application that is not be covered by this guide.</span></span>
>
>

## <a name="next-steps"></a><span data-ttu-id="5646d-224">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="5646d-224">Next steps</span></span>

- <span data-ttu-id="5646d-225">Połączenie z maszyną wirtualną.</span><span class="sxs-lookup"><span data-stu-id="5646d-225">Connect to the virtual machine.</span></span> <span data-ttu-id="5646d-226">Aby uzyskać instrukcje, zobacz [jak połączenia i zaloguj się do maszyny wirtualnej platformy Azure systemem Windows](connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="5646d-226">For instructions, see [How to connect and log on to an Azure virtual machine running Windows](connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

