---
title: "aaaMigrate tooan klasyczne maszyny Wirtualnej VM dysku zarządzanego ARM | Dokumentacja firmy Microsoft"
description: "Migrację jednej maszyny Wirtualnej platformy Azure z hello wdrażania klasycznego modelu tooManaged dysków w modelu wdrażania usługi Resource Manager hello."
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
ms.openlocfilehash: d8c4b9431f5dd8a071fcbc2ee36581a33f76ba62
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="manually-migrate-a-classic-vm-tooa-new-arm-managed-disk-vm-from-hello-vhd"></a><span data-ttu-id="90717-103">Ręcznej migracji tooa klasycznego wirtualna nowej ARM zarządzane dysku maszyny Wirtualnej z hello wirtualnego dysku twardego</span><span class="sxs-lookup"><span data-stu-id="90717-103">Manually migrate a Classic VM tooa new ARM Managed Disk VM from hello VHD</span></span> 


<span data-ttu-id="90717-104">Ta sekcja pomoże toomigrate możesz istniejących maszyn wirtualnych platformy Azure z hello klasycznego modelu wdrażania zbyt[dysków zarządzanych](managed-disks-overview.md) w modelu wdrażania usługi Resource Manager hello.</span><span class="sxs-lookup"><span data-stu-id="90717-104">This section helps you toomigrate your existing Azure VMs from hello classic deployment model too[Managed Disks](managed-disks-overview.md) in hello Resource Manager deployment model.</span></span>


## <a name="plan-for-hello-migration-toomanaged-disks"></a><span data-ttu-id="90717-105">Planowanie migracji hello tooManaged dysków</span><span class="sxs-lookup"><span data-stu-id="90717-105">Plan for hello migration tooManaged Disks</span></span>

<span data-ttu-id="90717-106">Ta sekcja pomoże toomake hello najlepszych decyzji w typach maszyny Wirtualnej i dysku.</span><span class="sxs-lookup"><span data-stu-id="90717-106">This section helps you toomake hello best decision on VM and disk types.</span></span>


### <a name="location"></a><span data-ttu-id="90717-107">Lokalizacja</span><span class="sxs-lookup"><span data-stu-id="90717-107">Location</span></span>

<span data-ttu-id="90717-108">Wybierz lokalizację, w której są dostępne dyski zarządzanych Azure.</span><span class="sxs-lookup"><span data-stu-id="90717-108">Pick a location where Azure Managed Disks are available.</span></span> <span data-ttu-id="90717-109">W przypadku migracji dysków zarządzanych tooPremium, upewnij się również magazyn w warstwie Premium jest dostępna w regionie hello planowanego toomigrate do.</span><span class="sxs-lookup"><span data-stu-id="90717-109">If you are migrating tooPremium Managed Disks, also ensure that Premium storage is available in hello region where you are planning toomigrate to.</span></span> <span data-ttu-id="90717-110">Zobacz [byRegion usług Azure](https://azure.microsoft.com/regions/#services) aktualne informacje o dostępnych lokalizacji.</span><span class="sxs-lookup"><span data-stu-id="90717-110">See [Azure Services byRegion](https://azure.microsoft.com/regions/#services) for up-to-date information on available locations.</span></span>

### <a name="vm-sizes"></a><span data-ttu-id="90717-111">Rozmiary maszyn wirtualnych</span><span class="sxs-lookup"><span data-stu-id="90717-111">VM sizes</span></span>

<span data-ttu-id="90717-112">W przypadku migracji dysków zarządzanych tooPremium masz tooupdate rozmiar hello hello wirtualna tooPremium rozmiar możliwością magazynu dostępnych w regionie hello, w którym znajduje się maszyna wirtualna.</span><span class="sxs-lookup"><span data-stu-id="90717-112">If you are migrating tooPremium Managed Disks, you have tooupdate hello size of hello VM tooPremium Storage capable size available in hello region where VM is located.</span></span> <span data-ttu-id="90717-113">Przejrzyj hello rozmiarów maszyn wirtualnych, które są funkcją Magazyn w warstwie Premium.</span><span class="sxs-lookup"><span data-stu-id="90717-113">Review hello VM sizes that are Premium Storage capable.</span></span> <span data-ttu-id="90717-114">specyfikacje rozmiaru maszyny Wirtualnej Azure Hello są wymienione w [rozmiary maszyn wirtualnych](sizes.md).</span><span class="sxs-lookup"><span data-stu-id="90717-114">hello Azure VM size specifications are listed in [Sizes for virtual machines](sizes.md).</span></span>
<span data-ttu-id="90717-115">Przejrzyj hello charakterystyki wydajności maszyn wirtualnych, które pracować z magazyn w warstwie Premium i wybierz polecenie hello najbardziej odpowiedni rozmiar maszyny Wirtualnej najlepiej pasujące do obciążenia.</span><span class="sxs-lookup"><span data-stu-id="90717-115">Review hello performance characteristics of virtual machines that work with Premium Storage and choose hello most appropriate VM size that best suits your workload.</span></span> <span data-ttu-id="90717-116">Upewnij się, czy Brak dostępnej wystarczającą przepustowość na ruchu dysku hello toodrive maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="90717-116">Make sure that there is sufficient bandwidth available on your VM toodrive hello disk traffic.</span></span>

### <a name="disk-sizes"></a><span data-ttu-id="90717-117">Rozmiary dysków</span><span class="sxs-lookup"><span data-stu-id="90717-117">Disk sizes</span></span>

<span data-ttu-id="90717-118">**Dysków zarządzanych w warstwie Premium**</span><span class="sxs-lookup"><span data-stu-id="90717-118">**Premium Managed Disks**</span></span>

<span data-ttu-id="90717-119">Istnieje siedem typów dysków zarządzane premium, które mogą być używane z maszyny Wirtualnej i każdy ma określonych IOPs i przepływność limity.</span><span class="sxs-lookup"><span data-stu-id="90717-119">There are seven types of premium Managed disks that can be used with your VM and each has specific IOPs and throughput limits.</span></span> <span data-ttu-id="90717-120">W przypadku wybrania hello Premium typ dysku dla maszyny Wirtualnej na podstawie hello potrzeb aplikacji pod względem wydajności, wydajności, skalowalności i ładuje szczytu, należy wziąć pod uwagę te limity.</span><span class="sxs-lookup"><span data-stu-id="90717-120">Consider these limits when choosing hello Premium disk type for your VM based on hello needs of your application in terms of capacity, performance, scalability, and peak loads.</span></span>

| <span data-ttu-id="90717-121">Typ dysków Premium</span><span class="sxs-lookup"><span data-stu-id="90717-121">Premium Disks Type</span></span>  | <span data-ttu-id="90717-122">P4</span><span class="sxs-lookup"><span data-stu-id="90717-122">P4</span></span>    | <span data-ttu-id="90717-123">P6</span><span class="sxs-lookup"><span data-stu-id="90717-123">P6</span></span>    | <span data-ttu-id="90717-124">P10</span><span class="sxs-lookup"><span data-stu-id="90717-124">P10</span></span>   | <span data-ttu-id="90717-125">P20</span><span class="sxs-lookup"><span data-stu-id="90717-125">P20</span></span>   | <span data-ttu-id="90717-126">P30</span><span class="sxs-lookup"><span data-stu-id="90717-126">P30</span></span>   | <span data-ttu-id="90717-127">P40</span><span class="sxs-lookup"><span data-stu-id="90717-127">P40</span></span>   | <span data-ttu-id="90717-128">P50</span><span class="sxs-lookup"><span data-stu-id="90717-128">P50</span></span>   | 
|---------------------|-------|-------|-------|-------|-------|-------|-------|
| <span data-ttu-id="90717-129">Rozmiar dysku</span><span class="sxs-lookup"><span data-stu-id="90717-129">Disk size</span></span>           | <span data-ttu-id="90717-130">128 GB</span><span class="sxs-lookup"><span data-stu-id="90717-130">128 GB</span></span>| <span data-ttu-id="90717-131">512 GB</span><span class="sxs-lookup"><span data-stu-id="90717-131">512 GB</span></span>| <span data-ttu-id="90717-132">128 GB</span><span class="sxs-lookup"><span data-stu-id="90717-132">128 GB</span></span>| <span data-ttu-id="90717-133">512 GB</span><span class="sxs-lookup"><span data-stu-id="90717-133">512 GB</span></span>            | <span data-ttu-id="90717-134">1024 GB (1 TB)</span><span class="sxs-lookup"><span data-stu-id="90717-134">1024 GB (1 TB)</span></span>    | <span data-ttu-id="90717-135">2048 GB (2 TB)</span><span class="sxs-lookup"><span data-stu-id="90717-135">2048 GB (2 TB)</span></span>    | <span data-ttu-id="90717-136">4095 GB (4 TB)</span><span class="sxs-lookup"><span data-stu-id="90717-136">4095 GB (4 TB)</span></span>    | 
| <span data-ttu-id="90717-137">Liczba operacji wejścia/wyjścia na sekundę na dysk</span><span class="sxs-lookup"><span data-stu-id="90717-137">IOPS per disk</span></span>       | <span data-ttu-id="90717-138">120</span><span class="sxs-lookup"><span data-stu-id="90717-138">120</span></span>   | <span data-ttu-id="90717-139">240</span><span class="sxs-lookup"><span data-stu-id="90717-139">240</span></span>   | <span data-ttu-id="90717-140">500</span><span class="sxs-lookup"><span data-stu-id="90717-140">500</span></span>   | <span data-ttu-id="90717-141">2300</span><span class="sxs-lookup"><span data-stu-id="90717-141">2300</span></span>              | <span data-ttu-id="90717-142">5000</span><span class="sxs-lookup"><span data-stu-id="90717-142">5000</span></span>              | <span data-ttu-id="90717-143">7500</span><span class="sxs-lookup"><span data-stu-id="90717-143">7500</span></span>              | <span data-ttu-id="90717-144">7500</span><span class="sxs-lookup"><span data-stu-id="90717-144">7500</span></span>              | 
| <span data-ttu-id="90717-145">Przepływność na dysk</span><span class="sxs-lookup"><span data-stu-id="90717-145">Throughput per disk</span></span> | <span data-ttu-id="90717-146">25 MB na sekundę</span><span class="sxs-lookup"><span data-stu-id="90717-146">25 MB per second</span></span>  | <span data-ttu-id="90717-147">50 MB / s</span><span class="sxs-lookup"><span data-stu-id="90717-147">50 MB per second</span></span>  | <span data-ttu-id="90717-148">100 MB na sekundę</span><span class="sxs-lookup"><span data-stu-id="90717-148">100 MB per second</span></span> | <span data-ttu-id="90717-149">150 MB na sekundę</span><span class="sxs-lookup"><span data-stu-id="90717-149">150 MB per second</span></span> | <span data-ttu-id="90717-150">200 MB / s</span><span class="sxs-lookup"><span data-stu-id="90717-150">200 MB per second</span></span> | <span data-ttu-id="90717-151">250 MB na sekundę</span><span class="sxs-lookup"><span data-stu-id="90717-151">250 MB per second</span></span> | <span data-ttu-id="90717-152">250 MB na sekundę</span><span class="sxs-lookup"><span data-stu-id="90717-152">250 MB per second</span></span> | 

<span data-ttu-id="90717-153">**Dyski standardowe zarządzanych**</span><span class="sxs-lookup"><span data-stu-id="90717-153">**Standard Managed Disks**</span></span>

<span data-ttu-id="90717-154">Istnieje siedem typów zarządzane standardowych dysków, które mogą być używane z maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="90717-154">There are seven types of Standard Managed disks that can be used with your VM.</span></span> <span data-ttu-id="90717-155">Każdej z nich ma inną wydajności, ale ma tego samego IOPS i limity przepustowości.</span><span class="sxs-lookup"><span data-stu-id="90717-155">Each of them have different capacity but have same IOPS and throughput limits.</span></span> <span data-ttu-id="90717-156">Wybierz typ hello dyski standardowe zarządzane na podstawie hello pojemności potrzeb aplikacji.</span><span class="sxs-lookup"><span data-stu-id="90717-156">Choose hello type of Standard Managed disks based on hello capacity needs of your application.</span></span>

| <span data-ttu-id="90717-157">Typ dysku standardowego</span><span class="sxs-lookup"><span data-stu-id="90717-157">Standard Disk Type</span></span>  | <span data-ttu-id="90717-158">S4</span><span class="sxs-lookup"><span data-stu-id="90717-158">S4</span></span>               | <span data-ttu-id="90717-159">S6</span><span class="sxs-lookup"><span data-stu-id="90717-159">S6</span></span>               | <span data-ttu-id="90717-160">S10</span><span class="sxs-lookup"><span data-stu-id="90717-160">S10</span></span>              | <span data-ttu-id="90717-161">S20</span><span class="sxs-lookup"><span data-stu-id="90717-161">S20</span></span>              | <span data-ttu-id="90717-162">S30</span><span class="sxs-lookup"><span data-stu-id="90717-162">S30</span></span>              | <span data-ttu-id="90717-163">S40</span><span class="sxs-lookup"><span data-stu-id="90717-163">S40</span></span>              | <span data-ttu-id="90717-164">S50</span><span class="sxs-lookup"><span data-stu-id="90717-164">S50</span></span>              | 
|---------------------|---------------------|---------------------|------------------|------------------|------------------|------------------|------------------| 
| <span data-ttu-id="90717-165">Rozmiar dysku</span><span class="sxs-lookup"><span data-stu-id="90717-165">Disk size</span></span>           | <span data-ttu-id="90717-166">30 GB</span><span class="sxs-lookup"><span data-stu-id="90717-166">30 GB</span></span>            | <span data-ttu-id="90717-167">64 GB</span><span class="sxs-lookup"><span data-stu-id="90717-167">64 GB</span></span>            | <span data-ttu-id="90717-168">128 GB</span><span class="sxs-lookup"><span data-stu-id="90717-168">128 GB</span></span>           | <span data-ttu-id="90717-169">512 GB</span><span class="sxs-lookup"><span data-stu-id="90717-169">512 GB</span></span>           | <span data-ttu-id="90717-170">1024 GB (1 TB)</span><span class="sxs-lookup"><span data-stu-id="90717-170">1024 GB (1 TB)</span></span>   | <span data-ttu-id="90717-171">2048 GB (2TB)</span><span class="sxs-lookup"><span data-stu-id="90717-171">2048 GB (2TB)</span></span>    | <span data-ttu-id="90717-172">4095 GB (4 TB)</span><span class="sxs-lookup"><span data-stu-id="90717-172">4095 GB (4 TB)</span></span>   | 
| <span data-ttu-id="90717-173">Liczba operacji wejścia/wyjścia na sekundę na dysk</span><span class="sxs-lookup"><span data-stu-id="90717-173">IOPS per disk</span></span>       | <span data-ttu-id="90717-174">500</span><span class="sxs-lookup"><span data-stu-id="90717-174">500</span></span>              | <span data-ttu-id="90717-175">500</span><span class="sxs-lookup"><span data-stu-id="90717-175">500</span></span>              | <span data-ttu-id="90717-176">500</span><span class="sxs-lookup"><span data-stu-id="90717-176">500</span></span>              | <span data-ttu-id="90717-177">500</span><span class="sxs-lookup"><span data-stu-id="90717-177">500</span></span>              | <span data-ttu-id="90717-178">500</span><span class="sxs-lookup"><span data-stu-id="90717-178">500</span></span>              | <span data-ttu-id="90717-179">500</span><span class="sxs-lookup"><span data-stu-id="90717-179">500</span></span>             | <span data-ttu-id="90717-180">500</span><span class="sxs-lookup"><span data-stu-id="90717-180">500</span></span>              | 
| <span data-ttu-id="90717-181">Przepływność na dysk</span><span class="sxs-lookup"><span data-stu-id="90717-181">Throughput per disk</span></span> | <span data-ttu-id="90717-182">60 MB na sekundę</span><span class="sxs-lookup"><span data-stu-id="90717-182">60 MB per second</span></span> | <span data-ttu-id="90717-183">60 MB na sekundę</span><span class="sxs-lookup"><span data-stu-id="90717-183">60 MB per second</span></span> | <span data-ttu-id="90717-184">60 MB na sekundę</span><span class="sxs-lookup"><span data-stu-id="90717-184">60 MB per second</span></span> | <span data-ttu-id="90717-185">60 MB na sekundę</span><span class="sxs-lookup"><span data-stu-id="90717-185">60 MB per second</span></span> | <span data-ttu-id="90717-186">60 MB na sekundę</span><span class="sxs-lookup"><span data-stu-id="90717-186">60 MB per second</span></span> | <span data-ttu-id="90717-187">60 MB na sekundę</span><span class="sxs-lookup"><span data-stu-id="90717-187">60 MB per second</span></span> | <span data-ttu-id="90717-188">60 MB na sekundę</span><span class="sxs-lookup"><span data-stu-id="90717-188">60 MB per second</span></span> | 


### <a name="disk-caching-policy"></a><span data-ttu-id="90717-189">Dyskowej pamięci podręcznej zasad</span><span class="sxs-lookup"><span data-stu-id="90717-189">Disk caching policy</span></span> 

<span data-ttu-id="90717-190">**Dysków zarządzanych w warstwie Premium**</span><span class="sxs-lookup"><span data-stu-id="90717-190">**Premium Managed Disks**</span></span>

<span data-ttu-id="90717-191">Domyślnie jest dyskowej pamięci podręcznej zasad *tylko do odczytu* dla wszystkich hello dysków danych w warstwie Premium i *odczytu i zapisu* dla dysku systemu operacyjnego Premium hello dołączony toohello maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="90717-191">By default, disk caching policy is *Read-Only* for all hello Premium data disks, and *Read-Write* for hello Premium operating system disk attached toohello VM.</span></span> <span data-ttu-id="90717-192">To ustawienie konfiguracji jest zalecane tooachieve hello optymalnej wydajności dla aplikacji systemu IOs.</span><span class="sxs-lookup"><span data-stu-id="90717-192">This configuration setting is recommended tooachieve hello optimal performance for your application’s IOs.</span></span> <span data-ttu-id="90717-193">W przypadku dysków ciężki zapisu lub w trybie tylko do zapisu danych (takich jak pliki dziennika programu SQL Server) Wyłącz buforowanie dysku, dzięki czemu można osiągnąć lepszą wydajność aplikacji.</span><span class="sxs-lookup"><span data-stu-id="90717-193">For write-heavy or write-only data disks (such as SQL Server log files), disable disk caching so that you can achieve better application performance.</span></span>

### <a name="pricing"></a><span data-ttu-id="90717-194">Cennik</span><span class="sxs-lookup"><span data-stu-id="90717-194">Pricing</span></span>

<span data-ttu-id="90717-195">Przejrzyj hello [ceny dysków zarządzanych](https://azure.microsoft.com/en-us/pricing/details/managed-disks/).</span><span class="sxs-lookup"><span data-stu-id="90717-195">Review hello [pricing for Managed Disks](https://azure.microsoft.com/en-us/pricing/details/managed-disks/).</span></span> <span data-ttu-id="90717-196">Cen dysków zarządzanych w warstwie Premium jest taka sama jak hello niezarządzane dysków Premium.</span><span class="sxs-lookup"><span data-stu-id="90717-196">Pricing of Premium Managed Disks is same as hello Premium Unmanaged Disks.</span></span> <span data-ttu-id="90717-197">Ale ceny dyski standardowe zarządzanych jest inny niż dyski standardowe niezarządzane.</span><span class="sxs-lookup"><span data-stu-id="90717-197">But pricing for Standard Managed Disks is different than Standard Unmanaged Disks.</span></span>


## <a name="checklist"></a><span data-ttu-id="90717-198">Lista kontrolna</span><span class="sxs-lookup"><span data-stu-id="90717-198">Checklist</span></span>

1.  <span data-ttu-id="90717-199">W przypadku migracji dysków zarządzanych tooPremium, upewnij się, że jest dostępna w regionie hello, które w przypadku migracji do.</span><span class="sxs-lookup"><span data-stu-id="90717-199">If you are migrating tooPremium Managed Disks, make sure it is available in hello region you are migrating to.</span></span>

2.  <span data-ttu-id="90717-200">Zdecyduj, hello nowej serii maszyn wirtualnych, które będą używane.</span><span class="sxs-lookup"><span data-stu-id="90717-200">Decide hello new VM series you will be using.</span></span> <span data-ttu-id="90717-201">Jeśli przeprowadzasz migrację dysków zarządzanych tooPremium powinno być funkcją Magazyn w warstwie Premium.</span><span class="sxs-lookup"><span data-stu-id="90717-201">It should be a Premium Storage capable if you are migrating tooPremium Managed Disks.</span></span>

3.  <span data-ttu-id="90717-202">Zdecyduj, hello dokładny rozmiar maszyny Wirtualnej, który będzie używany, które są dostępne w regionie hello, które w przypadku migracji do.</span><span class="sxs-lookup"><span data-stu-id="90717-202">Decide hello exact VM size you will use which are available in hello region you are migrating to.</span></span> <span data-ttu-id="90717-203">Rozmiar maszyny Wirtualnej musi toobe toosupport wystarczająco duży hello liczba dysków danych, do których masz.</span><span class="sxs-lookup"><span data-stu-id="90717-203">VM size needs toobe large enough toosupport hello number of data disks you have.</span></span> <span data-ttu-id="90717-204">Na przykład jeśli masz cztery dyski danych hello maszyna wirtualna musi mieć co najmniej dwa rdzenie.</span><span class="sxs-lookup"><span data-stu-id="90717-204">For example, if you have four data disks, hello VM must have two or more cores.</span></span> <span data-ttu-id="90717-205">Należy również rozważyć przetwarzania zasilania, pamięci i musi przepustowości sieci.</span><span class="sxs-lookup"><span data-stu-id="90717-205">Also, consider processing power, memory and network bandwidth needs.</span></span>

4.  <span data-ttu-id="90717-206">Ma hello wirtualna szczegóły bieżącej przydatną tym hello listę dysków i odpowiednie obiekty BLOB dysków VHD.</span><span class="sxs-lookup"><span data-stu-id="90717-206">Have hello current VM details handy, including hello list of disks and corresponding VHD blobs.</span></span>

<span data-ttu-id="90717-207">Przygotowanie aplikacji dla przestoju.</span><span class="sxs-lookup"><span data-stu-id="90717-207">Prepare your application for downtime.</span></span> <span data-ttu-id="90717-208">toodo czystą migracji należy toostop przetwarzania hello w bieżącym systemie hello.</span><span class="sxs-lookup"><span data-stu-id="90717-208">toodo a clean migration, you have toostop all hello processing in hello current system.</span></span> <span data-ttu-id="90717-209">Następnie możesz pobrać go tooconsistent stanu, które można migrować toohello na nowej platformie.</span><span class="sxs-lookup"><span data-stu-id="90717-209">Only then you can get it tooconsistent state which you can migrate toohello new platform.</span></span> <span data-ttu-id="90717-210">Czas trwania przestoju zależy od hello ilości danych w hello toomigrate dysków.</span><span class="sxs-lookup"><span data-stu-id="90717-210">Downtime duration depends on hello amount of data in hello disks toomigrate.</span></span>


## <a name="migrate-hello-vm"></a><span data-ttu-id="90717-211">Migrowanie hello maszyny Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="90717-211">Migrate hello VM</span></span>

<span data-ttu-id="90717-212">Przygotowanie aplikacji dla przestoju.</span><span class="sxs-lookup"><span data-stu-id="90717-212">Prepare your application for downtime.</span></span> <span data-ttu-id="90717-213">toodo czystą migracji należy toostop przetwarzania hello w bieżącym systemie hello.</span><span class="sxs-lookup"><span data-stu-id="90717-213">toodo a clean migration, you have toostop all hello processing in hello current system.</span></span> <span data-ttu-id="90717-214">Następnie możesz pobrać go tooconsistent stanu, które można migrować toohello na nowej platformie.</span><span class="sxs-lookup"><span data-stu-id="90717-214">Only then you can get it tooconsistent state which you can migrate toohello new platform.</span></span> <span data-ttu-id="90717-215">Czas trwania przestoju zależy od hello ilości danych w hello toomigrate dysków.</span><span class="sxs-lookup"><span data-stu-id="90717-215">Downtime duration depends hello amount of data in hello disks toomigrate.</span></span>


1.  <span data-ttu-id="90717-216">Najpierw należy ustawić hello typowe parametry:</span><span class="sxs-lookup"><span data-stu-id="90717-216">First, set hello common parameters:</span></span>

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

2.  <span data-ttu-id="90717-217">Tworzenie zarządzanego dysku systemu operacyjnego przy użyciu hello wirtualnego dysku twardego z hello klasyczne maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="90717-217">Create a managed OS disk using hello VHD from hello classic VM.</span></span>

    <span data-ttu-id="90717-218">Upewnij się, że masz pod warunkiem hello ukończyć URI hello parametru toohello $osVhdUri wirtualnego dysku twardego systemu operacyjnego.</span><span class="sxs-lookup"><span data-stu-id="90717-218">Ensure that you have provided hello complete URI of hello OS VHD toohello $osVhdUri parameter.</span></span> <span data-ttu-id="90717-219">Wprowadź też **- AccountType** jako **PremiumLRS** lub **StandardLRS** na podstawie typu dysków (Premium lub Standard) w przypadku migracji do.</span><span class="sxs-lookup"><span data-stu-id="90717-219">Also, enter **-AccountType** as **PremiumLRS** or **StandardLRS** based on type of disks (Premium or Standard) you are migrating to.</span></span>

    ```powershell
    $osDisk = New-AzureRmDisk -DiskName $osDiskName -Disk (New-AzureRmDiskConfig '
    -AccountType PremiumLRS -Location $location -CreateOption Import -SourceUri $osVhdUri) '
    -ResourceGroupName $resourceGroupName
    ```

3.  <span data-ttu-id="90717-220">Dołącz toohello dysku systemu operacyjnego hello nowej maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="90717-220">Attach hello OS disk toohello new VM.</span></span>

    ```powershell
    $VirtualMachine = New-AzureRmVMConfig -VMName $virtualMachineName -VMSize $virtualMachineSize
    $VirtualMachine = Set-AzureRmVMOSDisk -VM $VirtualMachine -ManagedDiskId $osDisk.Id '
    -StorageAccountType PremiumLRS -DiskSizeInGB 128 -CreateOption Attach -Windows
    ```

4.  <span data-ttu-id="90717-221">Utwórz dysk danych zarządzanych z pliku VHD danych hello i dodaj go toohello nowej maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="90717-221">Create a managed data disk from hello data VHD file and add it toohello new VM.</span></span>

    ```powershell
    $dataDisk1 = New-AzureRmDisk -DiskName $dataDiskName -Disk (New-AzureRmDiskConfig '
    -AccountType PremiumLRS -Location $location -CreationDataCreateOption Import '
    -SourceUri $dataVhdUri ) -ResourceGroupName $resourceGroupName
    
    $VirtualMachine = Add-AzureRmVMDataDisk -VM $VirtualMachine -Name $dataDiskName '
    -CreateOption Attach -ManagedDiskId $dataDisk1.Id -Lun 1
    ```

5.  <span data-ttu-id="90717-222">Utwórz hello nowej maszyny Wirtualnej przez ustawienie publicznego adresu IP, sieci wirtualnej i karty sieciowej.</span><span class="sxs-lookup"><span data-stu-id="90717-222">Create hello new VM by setting public IP, Virtual Network and NIC.</span></span>

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
><span data-ttu-id="90717-223">Może być konieczne toosupport dodatkowe kroki aplikacji, która jest nie obejmuje się w tym przewodniku.</span><span class="sxs-lookup"><span data-stu-id="90717-223">There may be additional steps necessary toosupport your application that is not be covered by this guide.</span></span>
>
>

## <a name="next-steps"></a><span data-ttu-id="90717-224">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="90717-224">Next steps</span></span>

- <span data-ttu-id="90717-225">Połącz toohello maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="90717-225">Connect toohello virtual machine.</span></span> <span data-ttu-id="90717-226">Aby uzyskać instrukcje, zobacz [jak dziennika na tooan wirtualnej platformy Azure i tooconnect maszyny, systemem operacyjnym Windows](connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="90717-226">For instructions, see [How tooconnect and log on tooan Azure virtual machine running Windows](connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

