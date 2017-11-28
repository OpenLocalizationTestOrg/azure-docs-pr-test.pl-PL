---
title: dyski aaaManage Azure z hello Azure PowerShell | Dokumentacja firmy Microsoft
description: "Samouczek — Zarządzanie dyskami Azure z hello Azure PowerShell"
services: virtual-machines-windows
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: 
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 05/02/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: 2f61ad18bc94bab527d7ae593da603c6073adc89
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="manage-azure-disks-with-powershell"></a><span data-ttu-id="7a4aa-103">Zarządzanie dyskami Azure przy użyciu programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="7a4aa-103">Manage Azure disks with PowerShell</span></span>

<span data-ttu-id="7a4aa-104">Maszyny wirtualne platformy Azure, użyj systemu operacyjnego dyski toostore hello maszyn wirtualnych, aplikacji i danych.</span><span class="sxs-lookup"><span data-stu-id="7a4aa-104">Azure virtual machines use disks toostore hello VMs operating system, applications, and data.</span></span> <span data-ttu-id="7a4aa-105">Podczas tworzenia maszyny Wirtualnej jest ważne toochoose rozmiar dysku i obciążenia odpowiednie toohello oczekiwano konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="7a4aa-105">When creating a VM it is important toochoose a disk size and configuration appropriate toohello expected workload.</span></span> <span data-ttu-id="7a4aa-106">W tym samouczku opisano wdrażanie i Zarządzanie dyskami maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="7a4aa-106">This tutorial covers deploying and managing VM disks.</span></span> <span data-ttu-id="7a4aa-107">Informacje o:</span><span class="sxs-lookup"><span data-stu-id="7a4aa-107">You learn about:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="7a4aa-108">Dyski systemu operacyjnego i tymczasowego</span><span class="sxs-lookup"><span data-stu-id="7a4aa-108">OS disks and temporary disks</span></span>
> * <span data-ttu-id="7a4aa-109">Dyski danych</span><span class="sxs-lookup"><span data-stu-id="7a4aa-109">Data disks</span></span>
> * <span data-ttu-id="7a4aa-110">Standard i dysków w warstwie Premium</span><span class="sxs-lookup"><span data-stu-id="7a4aa-110">Standard and Premium disks</span></span>
> * <span data-ttu-id="7a4aa-111">Wydajność dysku</span><span class="sxs-lookup"><span data-stu-id="7a4aa-111">Disk performance</span></span>
> * <span data-ttu-id="7a4aa-112">Dołączanie i przygotowywania dysków z danymi</span><span class="sxs-lookup"><span data-stu-id="7a4aa-112">Attaching and preparing data disks</span></span>

<span data-ttu-id="7a4aa-113">Ten samouczek wymaga hello Azure PowerShell w wersji modułu 3,6 lub nowszej.</span><span class="sxs-lookup"><span data-stu-id="7a4aa-113">This tutorial requires hello Azure PowerShell module version 3.6 or later.</span></span> <span data-ttu-id="7a4aa-114">Uruchom ` Get-Module -ListAvailable AzureRM` toofind hello wersji.</span><span class="sxs-lookup"><span data-stu-id="7a4aa-114">Run ` Get-Module -ListAvailable AzureRM` toofind hello version.</span></span> <span data-ttu-id="7a4aa-115">Jeśli potrzebujesz tooupgrade, zobacz [modułu instalacji programu Azure PowerShell](/powershell/azure/install-azurerm-ps).</span><span class="sxs-lookup"><span data-stu-id="7a4aa-115">If you need tooupgrade, see [Install Azure PowerShell module](/powershell/azure/install-azurerm-ps).</span></span>

## <a name="default-azure-disks"></a><span data-ttu-id="7a4aa-116">Domyślna dysku systemu Azure</span><span class="sxs-lookup"><span data-stu-id="7a4aa-116">Default Azure disks</span></span>

<span data-ttu-id="7a4aa-117">Po utworzeniu maszyny wirtualnej platformy Azure, dwa dyski są automatycznie dołączone toohello maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="7a4aa-117">When an Azure virtual machine is created, two disks are automatically attached toohello virtual machine.</span></span> 

<span data-ttu-id="7a4aa-118">**Dysk systemu operacyjnego** — dysków systemu operacyjnego mogą być określane w górę terabajt too1 i hosty hello maszyn wirtualnych systemu operacyjnego.</span><span class="sxs-lookup"><span data-stu-id="7a4aa-118">**Operating system disk** - Operating system disks can be sized up too1 terabyte, and hosts hello VMs operating system.</span></span>  <span data-ttu-id="7a4aa-119">dysk systemu operacyjnego Hello jest przypisanej litery dysku z *c:* domyślnie.</span><span class="sxs-lookup"><span data-stu-id="7a4aa-119">hello OS disk is assigned a drive letter of *c:* by default.</span></span> <span data-ttu-id="7a4aa-120">Witaj dyskowej pamięci podręcznej konfiguracji dysku systemu operacyjnego hello jest zoptymalizowana pod kątem wydajności systemu operacyjnego.</span><span class="sxs-lookup"><span data-stu-id="7a4aa-120">hello disk caching configuration of hello OS disk is optimized for OS performance.</span></span> <span data-ttu-id="7a4aa-121">dysk systemu operacyjnego Hello **nie powinien** hosta aplikacji i danych.</span><span class="sxs-lookup"><span data-stu-id="7a4aa-121">hello OS disk **should not** host applications or data.</span></span> <span data-ttu-id="7a4aa-122">Dla aplikacji i danych należy użyć dysku danych, które szczegółowo w dalszej części tego artykułu.</span><span class="sxs-lookup"><span data-stu-id="7a4aa-122">For applications and data, use a data disk, which is detailed later in this article.</span></span>

<span data-ttu-id="7a4aa-123">**Dysku tymczasowym** -tymczasowego dysków używać dysków SSD, który znajduje się na powitania tego samego hosta platformy Azure jako hello maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="7a4aa-123">**Temporary disk** - Temporary disks use a solid-state drive that is located on hello same Azure host as hello VM.</span></span> <span data-ttu-id="7a4aa-124">Tymczasowy dyski są wysokiej wydajności i mogą być używane do operacji, takich jak przetwarzanie danych tymczasowych.</span><span class="sxs-lookup"><span data-stu-id="7a4aa-124">Temp disks are highly performant and may be used for operations such as temporary data processing.</span></span> <span data-ttu-id="7a4aa-125">Jednak hello maszyny Wirtualnej w przypadku tooa przeniesiony na nowy host, zostaną usunięte wszystkie dane przechowywane na dysku tymczasowym.</span><span class="sxs-lookup"><span data-stu-id="7a4aa-125">However, if hello VM is moved tooa new host, any data stored on a temporary disk is removed.</span></span> <span data-ttu-id="7a4aa-126">rozmiar dysku tymczasowym hello Hello jest określana przez hello rozmiar maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="7a4aa-126">hello size of hello temporary disk is determined by hello VM size.</span></span> <span data-ttu-id="7a4aa-127">Tymczasowe dyski są przypisane literę dysku *d:* domyślnie.</span><span class="sxs-lookup"><span data-stu-id="7a4aa-127">Temporary disks are assigned a drive letter of *d:* by default.</span></span>

### <a name="temporary-disk-sizes"></a><span data-ttu-id="7a4aa-128">Rozmiary dysku tymczasowym</span><span class="sxs-lookup"><span data-stu-id="7a4aa-128">Temporary disk sizes</span></span>

| <span data-ttu-id="7a4aa-129">Typ</span><span class="sxs-lookup"><span data-stu-id="7a4aa-129">Type</span></span> | <span data-ttu-id="7a4aa-130">Rozmiar maszyny Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="7a4aa-130">VM Size</span></span> | <span data-ttu-id="7a4aa-131">Maksymalny rozmiar dysku tymczasowego (GB)</span><span class="sxs-lookup"><span data-stu-id="7a4aa-131">Max temp disk size (GB)</span></span> |
|----|----|----|
| [<span data-ttu-id="7a4aa-132">Zastosowania ogólne</span><span class="sxs-lookup"><span data-stu-id="7a4aa-132">General purpose</span></span>](sizes-general.md) | <span data-ttu-id="7a4aa-133">A i serii D</span><span class="sxs-lookup"><span data-stu-id="7a4aa-133">A and D series</span></span> | <span data-ttu-id="7a4aa-134">800</span><span class="sxs-lookup"><span data-stu-id="7a4aa-134">800</span></span> |
| [<span data-ttu-id="7a4aa-135">Optymalizacja pod kątem obliczeń</span><span class="sxs-lookup"><span data-stu-id="7a4aa-135">Compute optimized</span></span>](sizes-compute.md) | <span data-ttu-id="7a4aa-136">Seria F</span><span class="sxs-lookup"><span data-stu-id="7a4aa-136">F series</span></span> | <span data-ttu-id="7a4aa-137">800</span><span class="sxs-lookup"><span data-stu-id="7a4aa-137">800</span></span> |
| [<span data-ttu-id="7a4aa-138">Optymalizacja pod kątem pamięci</span><span class="sxs-lookup"><span data-stu-id="7a4aa-138">Memory optimized</span></span>](../virtual-machines-windows-sizes-memory.md) | <span data-ttu-id="7a4aa-139">D i G serii</span><span class="sxs-lookup"><span data-stu-id="7a4aa-139">D and G series</span></span> | <span data-ttu-id="7a4aa-140">6144</span><span class="sxs-lookup"><span data-stu-id="7a4aa-140">6144</span></span> |
| [<span data-ttu-id="7a4aa-141">Optymalizacja pod kątem magazynu</span><span class="sxs-lookup"><span data-stu-id="7a4aa-141">Storage optimized</span></span>](../virtual-machines-windows-sizes-storage.md) | <span data-ttu-id="7a4aa-142">Seria L</span><span class="sxs-lookup"><span data-stu-id="7a4aa-142">L series</span></span> | <span data-ttu-id="7a4aa-143">5630</span><span class="sxs-lookup"><span data-stu-id="7a4aa-143">5630</span></span> |
| [<span data-ttu-id="7a4aa-144">Procesor GPU</span><span class="sxs-lookup"><span data-stu-id="7a4aa-144">GPU</span></span>](sizes-gpu.md) | <span data-ttu-id="7a4aa-145">N serii</span><span class="sxs-lookup"><span data-stu-id="7a4aa-145">N series</span></span> | <span data-ttu-id="7a4aa-146">1440</span><span class="sxs-lookup"><span data-stu-id="7a4aa-146">1440</span></span> |
| [<span data-ttu-id="7a4aa-147">Wysoka wydajność</span><span class="sxs-lookup"><span data-stu-id="7a4aa-147">High performance</span></span>](sizes-hpc.md) | <span data-ttu-id="7a4aa-148">A i serii H</span><span class="sxs-lookup"><span data-stu-id="7a4aa-148">A and H series</span></span> | <span data-ttu-id="7a4aa-149">2000</span><span class="sxs-lookup"><span data-stu-id="7a4aa-149">2000</span></span> |

## <a name="azure-data-disks"></a><span data-ttu-id="7a4aa-150">Dyski danych Azure</span><span class="sxs-lookup"><span data-stu-id="7a4aa-150">Azure data disks</span></span>

<span data-ttu-id="7a4aa-151">Instalowanie aplikacji i przechowywania danych można dodać dodatkowego dysku z danymi.</span><span class="sxs-lookup"><span data-stu-id="7a4aa-151">Additional data disks can be added for installing applications and storing data.</span></span> <span data-ttu-id="7a4aa-152">Dyski danych używanego w sytuacji, gdy wymagane jest trwałe i szybko reagowały pamięci masowej.</span><span class="sxs-lookup"><span data-stu-id="7a4aa-152">Data disks should be used in any situation where durable and responsive data storage is desired.</span></span> <span data-ttu-id="7a4aa-153">Każdy dysk danych ma maksymalną pojemność 1 terabajt.</span><span class="sxs-lookup"><span data-stu-id="7a4aa-153">Each data disk has a maximum capacity of 1 terabyte.</span></span> <span data-ttu-id="7a4aa-154">rozmiar Hello hello maszyny wirtualnej Określa, jak wiele dysków z danymi mogą być dołączone tooa maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="7a4aa-154">hello size of hello virtual machine determines how many data disks can be attached tooa VM.</span></span> <span data-ttu-id="7a4aa-155">Dla każdej podstawowej maszyny Wirtualnej można dołączyć danych dwóch dysków.</span><span class="sxs-lookup"><span data-stu-id="7a4aa-155">For each VM core, two data disks can be attached.</span></span> 

### <a name="max-data-disks-per-vm"></a><span data-ttu-id="7a4aa-156">Maksymalna liczba dysków z danymi dla maszyny Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="7a4aa-156">Max data disks per VM</span></span>

| <span data-ttu-id="7a4aa-157">Typ</span><span class="sxs-lookup"><span data-stu-id="7a4aa-157">Type</span></span> | <span data-ttu-id="7a4aa-158">Rozmiar maszyny Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="7a4aa-158">VM Size</span></span> | <span data-ttu-id="7a4aa-159">Maksymalna liczba dysków z danymi dla maszyny Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="7a4aa-159">Max data disks per VM</span></span> |
|----|----|----|
| [<span data-ttu-id="7a4aa-160">Zastosowania ogólne</span><span class="sxs-lookup"><span data-stu-id="7a4aa-160">General purpose</span></span>](sizes-general.md) | <span data-ttu-id="7a4aa-161">A i serii D</span><span class="sxs-lookup"><span data-stu-id="7a4aa-161">A and D series</span></span> | <span data-ttu-id="7a4aa-162">32</span><span class="sxs-lookup"><span data-stu-id="7a4aa-162">32</span></span> |
| [<span data-ttu-id="7a4aa-163">Optymalizacja pod kątem obliczeń</span><span class="sxs-lookup"><span data-stu-id="7a4aa-163">Compute optimized</span></span>](sizes-compute.md) | <span data-ttu-id="7a4aa-164">Seria F</span><span class="sxs-lookup"><span data-stu-id="7a4aa-164">F series</span></span> | <span data-ttu-id="7a4aa-165">32</span><span class="sxs-lookup"><span data-stu-id="7a4aa-165">32</span></span> |
| [<span data-ttu-id="7a4aa-166">Optymalizacja pod kątem pamięci</span><span class="sxs-lookup"><span data-stu-id="7a4aa-166">Memory optimized</span></span>](../virtual-machines-windows-sizes-memory.md) | <span data-ttu-id="7a4aa-167">D i G serii</span><span class="sxs-lookup"><span data-stu-id="7a4aa-167">D and G series</span></span> | <span data-ttu-id="7a4aa-168">64</span><span class="sxs-lookup"><span data-stu-id="7a4aa-168">64</span></span> |
| [<span data-ttu-id="7a4aa-169">Optymalizacja pod kątem magazynu</span><span class="sxs-lookup"><span data-stu-id="7a4aa-169">Storage optimized</span></span>](../virtual-machines-windows-sizes-storage.md) | <span data-ttu-id="7a4aa-170">Seria L</span><span class="sxs-lookup"><span data-stu-id="7a4aa-170">L series</span></span> | <span data-ttu-id="7a4aa-171">64</span><span class="sxs-lookup"><span data-stu-id="7a4aa-171">64</span></span> |
| [<span data-ttu-id="7a4aa-172">Procesor GPU</span><span class="sxs-lookup"><span data-stu-id="7a4aa-172">GPU</span></span>](sizes-gpu.md) | <span data-ttu-id="7a4aa-173">N serii</span><span class="sxs-lookup"><span data-stu-id="7a4aa-173">N series</span></span> | <span data-ttu-id="7a4aa-174">48</span><span class="sxs-lookup"><span data-stu-id="7a4aa-174">48</span></span> |
| [<span data-ttu-id="7a4aa-175">Wysoka wydajność</span><span class="sxs-lookup"><span data-stu-id="7a4aa-175">High performance</span></span>](sizes-hpc.md) | <span data-ttu-id="7a4aa-176">A i serii H</span><span class="sxs-lookup"><span data-stu-id="7a4aa-176">A and H series</span></span> | <span data-ttu-id="7a4aa-177">32</span><span class="sxs-lookup"><span data-stu-id="7a4aa-177">32</span></span> |

## <a name="vm-disk-types"></a><span data-ttu-id="7a4aa-178">Typy dysków maszyny Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="7a4aa-178">VM disk types</span></span>

<span data-ttu-id="7a4aa-179">Platforma Azure oferuje dwa rodzaje dysku.</span><span class="sxs-lookup"><span data-stu-id="7a4aa-179">Azure provides two types of disk.</span></span>

### <a name="standard-disk"></a><span data-ttu-id="7a4aa-180">Dysków w warstwie standardowa</span><span class="sxs-lookup"><span data-stu-id="7a4aa-180">Standard disk</span></span>

<span data-ttu-id="7a4aa-181">Magazyn Standard Storage bazuje na dyskach twardych (HDD) i stanowi ekonomiczne, chociaż wciąż wydajne rozwiązanie.</span><span class="sxs-lookup"><span data-stu-id="7a4aa-181">Standard Storage is backed by HDDs, and delivers cost-effective storage while still being performant.</span></span> <span data-ttu-id="7a4aa-182">Dyski standardowe idealnie nadają się do deweloperów ekonomiczne i testów obciążenia.</span><span class="sxs-lookup"><span data-stu-id="7a4aa-182">Standard disks are ideal for a cost effective dev and test workload.</span></span>

### <a name="premium-disk"></a><span data-ttu-id="7a4aa-183">Dysku Premium</span><span class="sxs-lookup"><span data-stu-id="7a4aa-183">Premium disk</span></span>

<span data-ttu-id="7a4aa-184">Dyski Premium bazują na dysk SSD dysku wysokiej wydajności i małych opóźnień.</span><span class="sxs-lookup"><span data-stu-id="7a4aa-184">Premium disks are backed by SSD-based high-performance, low-latency disk.</span></span> <span data-ttu-id="7a4aa-185">Idealny dla maszyn wirtualnych obciążeniu produkcji.</span><span class="sxs-lookup"><span data-stu-id="7a4aa-185">Perfect for VMs running production workload.</span></span> <span data-ttu-id="7a4aa-186">Magazyn w warstwie Premium obsługuje serii DS, DSv2 serii GS-series i FS serii maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="7a4aa-186">Premium Storage supports DS-series, DSv2-series, GS-series, and FS-series VMs.</span></span> <span data-ttu-id="7a4aa-187">Dysków w warstwie Premium są dostępne w trzech typów (P10, P20, P30), rozmiar hello dysku hello Określa typ dysku hello.</span><span class="sxs-lookup"><span data-stu-id="7a4aa-187">Premium disks come in three types (P10, P20, P30), hello size of hello disk determines hello disk type.</span></span> <span data-ttu-id="7a4aa-188">Podczas wybierania, wartość hello rozmiaru dysku jest zaokrąglana toohello dalej typu.</span><span class="sxs-lookup"><span data-stu-id="7a4aa-188">When selecting, a disk size hello value is rounded up toohello next type.</span></span> <span data-ttu-id="7a4aa-189">Na przykład jeśli rozmiar hello jest poniżej typ dysku hello 128 GB będzie P10, między 129 i 512 P20 i ponad 512 P30.</span><span class="sxs-lookup"><span data-stu-id="7a4aa-189">For example, if hello size is below 128 GB hello disk type will be P10, between 129 and 512 P20, and over 512 P30.</span></span> 

### <a name="premium-disk-performance"></a><span data-ttu-id="7a4aa-190">Wydajność dysku Premium</span><span class="sxs-lookup"><span data-stu-id="7a4aa-190">Premium disk performance</span></span>

|<span data-ttu-id="7a4aa-191">Typ dysku magazynu w warstwie Premium</span><span class="sxs-lookup"><span data-stu-id="7a4aa-191">Premium storage disk type</span></span> | <span data-ttu-id="7a4aa-192">P10</span><span class="sxs-lookup"><span data-stu-id="7a4aa-192">P10</span></span> | <span data-ttu-id="7a4aa-193">P20</span><span class="sxs-lookup"><span data-stu-id="7a4aa-193">P20</span></span> | <span data-ttu-id="7a4aa-194">P30</span><span class="sxs-lookup"><span data-stu-id="7a4aa-194">P30</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="7a4aa-195">Rozmiar dysku (zaokrąglony)</span><span class="sxs-lookup"><span data-stu-id="7a4aa-195">Disk size (round up)</span></span> | <span data-ttu-id="7a4aa-196">128 GB</span><span class="sxs-lookup"><span data-stu-id="7a4aa-196">128 GB</span></span> | <span data-ttu-id="7a4aa-197">512 GB</span><span class="sxs-lookup"><span data-stu-id="7a4aa-197">512 GB</span></span> | <span data-ttu-id="7a4aa-198">1024 GB (1 TB)</span><span class="sxs-lookup"><span data-stu-id="7a4aa-198">1,024 GB (1 TB)</span></span> |
| <span data-ttu-id="7a4aa-199">Liczba operacji wejścia/wyjścia na sekundę na dysk</span><span class="sxs-lookup"><span data-stu-id="7a4aa-199">IOPS per disk</span></span> | <span data-ttu-id="7a4aa-200">500</span><span class="sxs-lookup"><span data-stu-id="7a4aa-200">500</span></span> | <span data-ttu-id="7a4aa-201">2,300</span><span class="sxs-lookup"><span data-stu-id="7a4aa-201">2,300</span></span> | <span data-ttu-id="7a4aa-202">5,000</span><span class="sxs-lookup"><span data-stu-id="7a4aa-202">5,000</span></span> |
<span data-ttu-id="7a4aa-203">Przepływność na dysk</span><span class="sxs-lookup"><span data-stu-id="7a4aa-203">Throughput per disk</span></span> | <span data-ttu-id="7a4aa-204">100 MB/s</span><span class="sxs-lookup"><span data-stu-id="7a4aa-204">100 MB/s</span></span> | <span data-ttu-id="7a4aa-205">150 MB/s</span><span class="sxs-lookup"><span data-stu-id="7a4aa-205">150 MB/s</span></span> | <span data-ttu-id="7a4aa-206">200 MB/s</span><span class="sxs-lookup"><span data-stu-id="7a4aa-206">200 MB/s</span></span> |

<span data-ttu-id="7a4aa-207">Gdy hello powyżej tabeli określa maksymalną liczbę IOPS dla każdego dysku, można osiągnąć wyższy poziom wydajności przez stosowanie wielu dysków z danymi.</span><span class="sxs-lookup"><span data-stu-id="7a4aa-207">While hello above table identifies max IOPS per disk, a higher level of performance can be achieved by striping multiple data disks.</span></span> <span data-ttu-id="7a4aa-208">Na przykład 64 dane, które dyski mogą być dołączony tooStandard_GS5 maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="7a4aa-208">For instance, 64 data disks can be attached tooStandard_GS5 VM.</span></span> <span data-ttu-id="7a4aa-209">Jeśli każda z tych dysków o jako P30 można osiągnąć maksymalnie 80 000 IOPS.</span><span class="sxs-lookup"><span data-stu-id="7a4aa-209">If each of these disks are sized as a P30, a maximum of 80,000 IOPS can be achieved.</span></span> <span data-ttu-id="7a4aa-210">Aby uzyskać szczegółowe informacje o maksymalnej IOPS dla maszyny Wirtualnej, zobacz [rozmiarów maszyn wirtualnych systemu Linux](./sizes.md).</span><span class="sxs-lookup"><span data-stu-id="7a4aa-210">For detailed information on max IOPS per VM, see [Linux VM sizes](./sizes.md).</span></span>

## <a name="create-and-attach-disks"></a><span data-ttu-id="7a4aa-211">Utwórz i Dołącz dysków</span><span class="sxs-lookup"><span data-stu-id="7a4aa-211">Create and attach disks</span></span>

<span data-ttu-id="7a4aa-212">przykład Witaj toocomplete w tym samouczku, musi mieć istniejącej maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="7a4aa-212">toocomplete hello example in this tutorial, you must have an existing virtual machine.</span></span> <span data-ttu-id="7a4aa-213">Jeśli to konieczne, to [przykładowym skrypcie](../scripts/virtual-machines-windows-powershell-sample-create-vm.md) można utworzyć.</span><span class="sxs-lookup"><span data-stu-id="7a4aa-213">If needed, this [script sample](../scripts/virtual-machines-windows-powershell-sample-create-vm.md) can create one for you.</span></span> <span data-ttu-id="7a4aa-214">Podczas pracy nad hello samouczek, Zastąp maszyny Wirtualnej i grupy zasobów hello nazwy w razie potrzeby.</span><span class="sxs-lookup"><span data-stu-id="7a4aa-214">When working through hello tutorial, replace hello resource group and VM names where needed.</span></span>

<span data-ttu-id="7a4aa-215">Tworzenie początkowej konfiguracji hello o [AzureRmDiskConfig nowy](/powershell/module/azurerm.compute/new-azurermdiskconfig).</span><span class="sxs-lookup"><span data-stu-id="7a4aa-215">Create hello initial configuration with [New-AzureRmDiskConfig](/powershell/module/azurerm.compute/new-azurermdiskconfig).</span></span> <span data-ttu-id="7a4aa-216">Poniższy przykład Hello konfiguruje dysku, który wynosi 128 GB w rozmiarze.</span><span class="sxs-lookup"><span data-stu-id="7a4aa-216">hello following example configures a disk that is 128 gigabytes in size.</span></span>

```powershell
$diskConfig = New-AzureRmDiskConfig -Location EastUS -CreateOption Empty -DiskSizeGB 128
```

<span data-ttu-id="7a4aa-217">Utwórz dysk danych hello z hello [AzureRmDisk nowy](/powershell/module/azurerm.compute/new-azurermdisk) polecenia.</span><span class="sxs-lookup"><span data-stu-id="7a4aa-217">Create hello data disk with hello [New-AzureRmDisk](/powershell/module/azurerm.compute/new-azurermdisk) command.</span></span>

```powershell
$dataDisk = New-AzureRmDisk -ResourceGroupName myResourceGroup -DiskName myDataDisk -Disk $diskConfig
```

<span data-ttu-id="7a4aa-218">Maszyna wirtualna hello GET, które mają tooadd hello danych dysku toowith hello [Get-AzureRmVM](/powershell/module/azurerm.compute/get-azurermvm) polecenia.</span><span class="sxs-lookup"><span data-stu-id="7a4aa-218">Get hello virtual machine that you want tooadd hello data disk toowith hello [Get-AzureRmVM](/powershell/module/azurerm.compute/get-azurermvm) command.</span></span>

```powershell
$vm = Get-AzureRmVM -ResourceGroupName myResourceGroup -Name myVM
```

<span data-ttu-id="7a4aa-219">Dodaj hello danych dysku toohello konfiguracji maszyny wirtualnej z hello [AzureRmVMDataDisk Dodaj](/powershell/module/azurerm.compute/add-azurermvmdatadisk) polecenia.</span><span class="sxs-lookup"><span data-stu-id="7a4aa-219">Add hello data disk toohello virtual machine configuration with hello [Add-AzureRmVMDataDisk](/powershell/module/azurerm.compute/add-azurermvmdatadisk) command.</span></span>

```powershell
$vm = Add-AzureRmVMDataDisk -VM $vm -Name myDataDisk -CreateOption Attach -ManagedDiskId $dataDisk.Id -Lun 1
```

<span data-ttu-id="7a4aa-220">Zaktualizuj maszynę wirtualną hello za pomocą hello [AzureRmVM aktualizacji](/powershell/module/azurerm.compute/add-azurermvmdatadisk) polecenia.</span><span class="sxs-lookup"><span data-stu-id="7a4aa-220">Update hello virtual machine with hello [Update-AzureRmVM](/powershell/module/azurerm.compute/add-azurermvmdatadisk) command.</span></span>

```powershell
Update-AzureRmVM -ResourceGroupName myResourceGroup -VM $vm
```

## <a name="prepare-data-disks"></a><span data-ttu-id="7a4aa-221">Przygotowanie dysków z danymi</span><span class="sxs-lookup"><span data-stu-id="7a4aa-221">Prepare data disks</span></span>

<span data-ttu-id="7a4aa-222">Po dysku maszyny wirtualnej podłączone toohello, system operacyjny hello musi toobe skonfigurowane toouse hello dysku.</span><span class="sxs-lookup"><span data-stu-id="7a4aa-222">Once a disk has been attached toohello virtual machine, hello operating system needs toobe configured toouse hello disk.</span></span> <span data-ttu-id="7a4aa-223">Witaj poniższym przykładzie przedstawiono toomanually konfiguracji hello pierwszego dysku dodane toohello maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="7a4aa-223">hello following example shows how toomanually configure hello first disk added toohello VM.</span></span> <span data-ttu-id="7a4aa-224">Ten proces można również zautomatyzować przy użyciu hello [niestandardowe rozszerzenie skryptu](./tutorial-automate-vm-deployment.md).</span><span class="sxs-lookup"><span data-stu-id="7a4aa-224">This process can also be automated using hello [custom script extension](./tutorial-automate-vm-deployment.md).</span></span>

### <a name="manual-configuration"></a><span data-ttu-id="7a4aa-225">Konfiguracja ręczna</span><span class="sxs-lookup"><span data-stu-id="7a4aa-225">Manual configuration</span></span>

<span data-ttu-id="7a4aa-226">Utwórz połączenie RDP z maszyny wirtualnej hello.</span><span class="sxs-lookup"><span data-stu-id="7a4aa-226">Create an RDP connection with hello virtual machine.</span></span> <span data-ttu-id="7a4aa-227">Otwieranie programu PowerShell i uruchom ten skrypt.</span><span class="sxs-lookup"><span data-stu-id="7a4aa-227">Open up PowerShell and run this script.</span></span>

```powershell
Get-Disk | Where partitionstyle -eq 'raw' | `
Initialize-Disk -PartitionStyle MBR -PassThru | `
New-Partition -AssignDriveLetter -UseMaximumSize | `
Format-Volume -FileSystem NTFS -NewFileSystemLabel "myDataDisk" -Confirm:$false
```

## <a name="next-steps"></a><span data-ttu-id="7a4aa-228">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="7a4aa-228">Next steps</span></span>

<span data-ttu-id="7a4aa-229">W tym samouczku przedstawiono tematy dysków maszyny Wirtualnej takich jak:</span><span class="sxs-lookup"><span data-stu-id="7a4aa-229">In this tutorial, you learned about VM disks topics such as:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="7a4aa-230">Dyski systemu operacyjnego i tymczasowego</span><span class="sxs-lookup"><span data-stu-id="7a4aa-230">OS disks and temporary disks</span></span>
> * <span data-ttu-id="7a4aa-231">Dyski danych</span><span class="sxs-lookup"><span data-stu-id="7a4aa-231">Data disks</span></span>
> * <span data-ttu-id="7a4aa-232">Standard i dysków w warstwie Premium</span><span class="sxs-lookup"><span data-stu-id="7a4aa-232">Standard and Premium disks</span></span>
> * <span data-ttu-id="7a4aa-233">Wydajność dysku</span><span class="sxs-lookup"><span data-stu-id="7a4aa-233">Disk performance</span></span>
> * <span data-ttu-id="7a4aa-234">Dołączanie i przygotowywania dysków z danymi</span><span class="sxs-lookup"><span data-stu-id="7a4aa-234">Attaching and preparing data disks</span></span>

<span data-ttu-id="7a4aa-235">Przejdź dalej toolearn samouczka toohello dotyczące automatyzowania konfiguracji maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="7a4aa-235">Advance toohello next tutorial toolearn about automating VM configuration.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="7a4aa-236">Automatyzowanie konfiguracji maszyny wirtualnej</span><span class="sxs-lookup"><span data-stu-id="7a4aa-236">Automate VM configuration</span></span>](./tutorial-automate-vm-deployment.md)
