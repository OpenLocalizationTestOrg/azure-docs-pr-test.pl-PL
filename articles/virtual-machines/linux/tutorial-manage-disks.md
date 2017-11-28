---
title: dyski aaaManage Azure z hello Azure CLI | Dokumentacja firmy Microsoft
description: "Samouczek — Zarządzanie dyskami Azure z hello wiersza polecenia platformy Azure"
services: virtual-machines-linux
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 05/02/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: ad29cfbec5f9738f47705b19d0450c9a2f555492
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="manage-azure-disks-with-hello-azure-cli"></a><span data-ttu-id="345a9-103">Zarządzanie dyskami Azure z hello wiersza polecenia platformy Azure</span><span class="sxs-lookup"><span data-stu-id="345a9-103">Manage Azure disks with hello Azure CLI</span></span>

<span data-ttu-id="345a9-104">Maszyny wirtualne platformy Azure, użyj systemu operacyjnego dyski toostore hello maszyn wirtualnych, aplikacji i danych.</span><span class="sxs-lookup"><span data-stu-id="345a9-104">Azure virtual machines use disks toostore hello VMs operating system, applications, and data.</span></span> <span data-ttu-id="345a9-105">Podczas tworzenia maszyny Wirtualnej jest ważne toochoose rozmiar dysku i obciążenia odpowiednie toohello oczekiwano konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="345a9-105">When creating a VM it is important toochoose a disk size and configuration appropriate toohello expected workload.</span></span> <span data-ttu-id="345a9-106">W tym samouczku opisano wdrażanie i Zarządzanie dyskami maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="345a9-106">This tutorial covers deploying and managing VM disks.</span></span> <span data-ttu-id="345a9-107">Informacje o:</span><span class="sxs-lookup"><span data-stu-id="345a9-107">You learn about:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="345a9-108">Dyski systemu operacyjnego i tymczasowego</span><span class="sxs-lookup"><span data-stu-id="345a9-108">OS disks and temporary disks</span></span>
> * <span data-ttu-id="345a9-109">Dyski danych</span><span class="sxs-lookup"><span data-stu-id="345a9-109">Data disks</span></span>
> * <span data-ttu-id="345a9-110">Standard i dysków w warstwie Premium</span><span class="sxs-lookup"><span data-stu-id="345a9-110">Standard and Premium disks</span></span>
> * <span data-ttu-id="345a9-111">Wydajność dysku</span><span class="sxs-lookup"><span data-stu-id="345a9-111">Disk performance</span></span>
> * <span data-ttu-id="345a9-112">Dołączanie i przygotowywania dysków z danymi</span><span class="sxs-lookup"><span data-stu-id="345a9-112">Attaching and preparing data disks</span></span>
> * <span data-ttu-id="345a9-113">Zmiana rozmiaru dysków</span><span class="sxs-lookup"><span data-stu-id="345a9-113">Resizing disks</span></span>
> * <span data-ttu-id="345a9-114">Migawki dysków</span><span class="sxs-lookup"><span data-stu-id="345a9-114">Disk snapshots</span></span>


[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="345a9-115">Jeśli wybierz tooinstall i użyj interfejsu wiersza polecenia hello lokalnie, w tym samouczku wymaga działają hello Azure CLI w wersji 2.0.4 lub nowszej.</span><span class="sxs-lookup"><span data-stu-id="345a9-115">If you choose tooinstall and use hello CLI locally, this tutorial requires that you are running hello Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="345a9-116">Uruchom `az --version` toofind hello wersji.</span><span class="sxs-lookup"><span data-stu-id="345a9-116">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="345a9-117">Jeśli potrzebujesz tooinstall lub uaktualniania, zobacz [zainstalować Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="345a9-117">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="default-azure-disks"></a><span data-ttu-id="345a9-118">Domyślna dysku systemu Azure</span><span class="sxs-lookup"><span data-stu-id="345a9-118">Default Azure disks</span></span>

<span data-ttu-id="345a9-119">Po utworzeniu maszyny wirtualnej platformy Azure, dwa dyski są automatycznie dołączone toohello maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="345a9-119">When an Azure virtual machine is created, two disks are automatically attached toohello virtual machine.</span></span> 

<span data-ttu-id="345a9-120">**Dysk systemu operacyjnego** — dysków systemu operacyjnego mogą być określane w górę terabajt too1 i hosty hello maszyn wirtualnych systemu operacyjnego.</span><span class="sxs-lookup"><span data-stu-id="345a9-120">**Operating system disk** - Operating system disks can be sized up too1 terabyte, and hosts hello VMs operating system.</span></span> <span data-ttu-id="345a9-121">ma oznaczenie dysku systemu operacyjnego Hello */dev/sda* domyślnie.</span><span class="sxs-lookup"><span data-stu-id="345a9-121">hello OS disk is labeled */dev/sda* by default.</span></span> <span data-ttu-id="345a9-122">Witaj dyskowej pamięci podręcznej konfiguracji dysku systemu operacyjnego hello jest zoptymalizowana pod kątem wydajności systemu operacyjnego.</span><span class="sxs-lookup"><span data-stu-id="345a9-122">hello disk caching configuration of hello OS disk is optimized for OS performance.</span></span> <span data-ttu-id="345a9-123">Z powodu tej konfiguracji hello dysk systemu operacyjnego **nie powinien** hosta aplikacji i danych.</span><span class="sxs-lookup"><span data-stu-id="345a9-123">Because of this configuration, hello OS disk **should not** host applications or data.</span></span> <span data-ttu-id="345a9-124">Dla aplikacji i danych użycia dysków danych, które opisano szczegółowo w dalszej części tego artykułu.</span><span class="sxs-lookup"><span data-stu-id="345a9-124">For applications and data, use data disks, which are detailed later in this article.</span></span> 

<span data-ttu-id="345a9-125">**Dysku tymczasowym** -tymczasowego dysków używać dysków SSD, który znajduje się na powitania tego samego hosta platformy Azure jako hello maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="345a9-125">**Temporary disk** - Temporary disks use a solid-state drive that is located on hello same Azure host as hello VM.</span></span> <span data-ttu-id="345a9-126">Tymczasowy dyski są wysokiej wydajności i mogą być używane do operacji, takich jak przetwarzanie danych tymczasowych.</span><span class="sxs-lookup"><span data-stu-id="345a9-126">Temp disks are highly performant and may be used for operations such as temporary data processing.</span></span> <span data-ttu-id="345a9-127">Jednak hello maszyny Wirtualnej w przypadku tooa przeniesiony na nowy host, zostaną usunięte wszystkie dane przechowywane na dysku tymczasowym.</span><span class="sxs-lookup"><span data-stu-id="345a9-127">However, if hello VM is moved tooa new host, any data stored on a temporary disk is removed.</span></span> <span data-ttu-id="345a9-128">rozmiar dysku tymczasowym hello Hello jest określana przez hello rozmiar maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="345a9-128">hello size of hello temporary disk is determined by hello VM size.</span></span> <span data-ttu-id="345a9-129">Tymczasowe dyski są oznaczone jako */dev/sdb* i mieć punktu instalacji z *katalogu/mnt*.</span><span class="sxs-lookup"><span data-stu-id="345a9-129">Temporary disks are labeled */dev/sdb* and have a mountpoint of */mnt*.</span></span>

### <a name="temporary-disk-sizes"></a><span data-ttu-id="345a9-130">Rozmiary dysku tymczasowym</span><span class="sxs-lookup"><span data-stu-id="345a9-130">Temporary disk sizes</span></span>

| <span data-ttu-id="345a9-131">Typ</span><span class="sxs-lookup"><span data-stu-id="345a9-131">Type</span></span> | <span data-ttu-id="345a9-132">Rozmiar maszyny Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="345a9-132">VM Size</span></span> | <span data-ttu-id="345a9-133">Maksymalny rozmiar dysku tymczasowego (GB)</span><span class="sxs-lookup"><span data-stu-id="345a9-133">Max temp disk size (GB)</span></span> |
|----|----|----|
| [<span data-ttu-id="345a9-134">Zastosowania ogólne</span><span class="sxs-lookup"><span data-stu-id="345a9-134">General purpose</span></span>](sizes-general.md) | <span data-ttu-id="345a9-135">A i serii D</span><span class="sxs-lookup"><span data-stu-id="345a9-135">A and D series</span></span> | <span data-ttu-id="345a9-136">800</span><span class="sxs-lookup"><span data-stu-id="345a9-136">800</span></span> |
| [<span data-ttu-id="345a9-137">Optymalizacja pod kątem obliczeń</span><span class="sxs-lookup"><span data-stu-id="345a9-137">Compute optimized</span></span>](sizes-compute.md) | <span data-ttu-id="345a9-138">Seria F</span><span class="sxs-lookup"><span data-stu-id="345a9-138">F series</span></span> | <span data-ttu-id="345a9-139">800</span><span class="sxs-lookup"><span data-stu-id="345a9-139">800</span></span> |
| [<span data-ttu-id="345a9-140">Optymalizacja pod kątem pamięci</span><span class="sxs-lookup"><span data-stu-id="345a9-140">Memory optimized</span></span>](../virtual-machines-windows-sizes-memory.md) | <span data-ttu-id="345a9-141">D i G serii</span><span class="sxs-lookup"><span data-stu-id="345a9-141">D and G series</span></span> | <span data-ttu-id="345a9-142">6144</span><span class="sxs-lookup"><span data-stu-id="345a9-142">6144</span></span> |
| [<span data-ttu-id="345a9-143">Optymalizacja pod kątem magazynu</span><span class="sxs-lookup"><span data-stu-id="345a9-143">Storage optimized</span></span>](../virtual-machines-windows-sizes-storage.md) | <span data-ttu-id="345a9-144">Seria L</span><span class="sxs-lookup"><span data-stu-id="345a9-144">L series</span></span> | <span data-ttu-id="345a9-145">5630</span><span class="sxs-lookup"><span data-stu-id="345a9-145">5630</span></span> |
| [<span data-ttu-id="345a9-146">Procesor GPU</span><span class="sxs-lookup"><span data-stu-id="345a9-146">GPU</span></span>](sizes-gpu.md) | <span data-ttu-id="345a9-147">N serii</span><span class="sxs-lookup"><span data-stu-id="345a9-147">N series</span></span> | <span data-ttu-id="345a9-148">1440</span><span class="sxs-lookup"><span data-stu-id="345a9-148">1440</span></span> |
| [<span data-ttu-id="345a9-149">Wysoka wydajność</span><span class="sxs-lookup"><span data-stu-id="345a9-149">High performance</span></span>](sizes-hpc.md) | <span data-ttu-id="345a9-150">A i serii H</span><span class="sxs-lookup"><span data-stu-id="345a9-150">A and H series</span></span> | <span data-ttu-id="345a9-151">2000</span><span class="sxs-lookup"><span data-stu-id="345a9-151">2000</span></span> |

## <a name="azure-data-disks"></a><span data-ttu-id="345a9-152">Dyski danych Azure</span><span class="sxs-lookup"><span data-stu-id="345a9-152">Azure data disks</span></span>

<span data-ttu-id="345a9-153">Instalowanie aplikacji i przechowywania danych można dodać dodatkowego dysku z danymi.</span><span class="sxs-lookup"><span data-stu-id="345a9-153">Additional data disks can be added for installing applications and storing data.</span></span> <span data-ttu-id="345a9-154">Dyski danych używanego w sytuacji, gdy wymagane jest trwałe i szybko reagowały pamięci masowej.</span><span class="sxs-lookup"><span data-stu-id="345a9-154">Data disks should be used in any situation where durable and responsive data storage is desired.</span></span> <span data-ttu-id="345a9-155">Każdy dysk danych ma maksymalną pojemność 1 terabajt.</span><span class="sxs-lookup"><span data-stu-id="345a9-155">Each data disk has a maximum capacity of 1 terabyte.</span></span> <span data-ttu-id="345a9-156">rozmiar Hello hello maszyny wirtualnej Określa, jak wiele dysków z danymi mogą być dołączone tooa maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="345a9-156">hello size of hello virtual machine determines how many data disks can be attached tooa VM.</span></span> <span data-ttu-id="345a9-157">Dla każdej podstawowej maszyny Wirtualnej można dołączyć danych dwóch dysków.</span><span class="sxs-lookup"><span data-stu-id="345a9-157">For each VM core, two data disks can be attached.</span></span> 

### <a name="max-data-disks-per-vm"></a><span data-ttu-id="345a9-158">Maksymalna liczba dysków z danymi dla maszyny Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="345a9-158">Max data disks per VM</span></span>

| <span data-ttu-id="345a9-159">Typ</span><span class="sxs-lookup"><span data-stu-id="345a9-159">Type</span></span> | <span data-ttu-id="345a9-160">Rozmiar maszyny Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="345a9-160">VM Size</span></span> | <span data-ttu-id="345a9-161">Maksymalna liczba dysków z danymi dla maszyny Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="345a9-161">Max data disks per VM</span></span> |
|----|----|----|
| [<span data-ttu-id="345a9-162">Zastosowania ogólne</span><span class="sxs-lookup"><span data-stu-id="345a9-162">General purpose</span></span>](sizes-general.md) | <span data-ttu-id="345a9-163">A i serii D</span><span class="sxs-lookup"><span data-stu-id="345a9-163">A and D series</span></span> | <span data-ttu-id="345a9-164">32</span><span class="sxs-lookup"><span data-stu-id="345a9-164">32</span></span> |
| [<span data-ttu-id="345a9-165">Optymalizacja pod kątem obliczeń</span><span class="sxs-lookup"><span data-stu-id="345a9-165">Compute optimized</span></span>](sizes-compute.md) | <span data-ttu-id="345a9-166">Seria F</span><span class="sxs-lookup"><span data-stu-id="345a9-166">F series</span></span> | <span data-ttu-id="345a9-167">32</span><span class="sxs-lookup"><span data-stu-id="345a9-167">32</span></span> |
| [<span data-ttu-id="345a9-168">Optymalizacja pod kątem pamięci</span><span class="sxs-lookup"><span data-stu-id="345a9-168">Memory optimized</span></span>](../virtual-machines-windows-sizes-memory.md) | <span data-ttu-id="345a9-169">D i G serii</span><span class="sxs-lookup"><span data-stu-id="345a9-169">D and G series</span></span> | <span data-ttu-id="345a9-170">64</span><span class="sxs-lookup"><span data-stu-id="345a9-170">64</span></span> |
| [<span data-ttu-id="345a9-171">Optymalizacja pod kątem magazynu</span><span class="sxs-lookup"><span data-stu-id="345a9-171">Storage optimized</span></span>](../virtual-machines-windows-sizes-storage.md) | <span data-ttu-id="345a9-172">Seria L</span><span class="sxs-lookup"><span data-stu-id="345a9-172">L series</span></span> | <span data-ttu-id="345a9-173">64</span><span class="sxs-lookup"><span data-stu-id="345a9-173">64</span></span> |
| [<span data-ttu-id="345a9-174">Procesor GPU</span><span class="sxs-lookup"><span data-stu-id="345a9-174">GPU</span></span>](sizes-gpu.md) | <span data-ttu-id="345a9-175">N serii</span><span class="sxs-lookup"><span data-stu-id="345a9-175">N series</span></span> | <span data-ttu-id="345a9-176">48</span><span class="sxs-lookup"><span data-stu-id="345a9-176">48</span></span> |
| [<span data-ttu-id="345a9-177">Wysoka wydajność</span><span class="sxs-lookup"><span data-stu-id="345a9-177">High performance</span></span>](sizes-hpc.md) | <span data-ttu-id="345a9-178">A i serii H</span><span class="sxs-lookup"><span data-stu-id="345a9-178">A and H series</span></span> | <span data-ttu-id="345a9-179">32</span><span class="sxs-lookup"><span data-stu-id="345a9-179">32</span></span> |

## <a name="vm-disk-types"></a><span data-ttu-id="345a9-180">Typy dysków maszyny Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="345a9-180">VM disk types</span></span>

<span data-ttu-id="345a9-181">Platforma Azure oferuje dwa rodzaje dysku.</span><span class="sxs-lookup"><span data-stu-id="345a9-181">Azure provides two types of disk.</span></span>

### <a name="standard-disk"></a><span data-ttu-id="345a9-182">Dysków w warstwie standardowa</span><span class="sxs-lookup"><span data-stu-id="345a9-182">Standard disk</span></span>

<span data-ttu-id="345a9-183">Magazyn Standard Storage bazuje na dyskach twardych (HDD) i stanowi ekonomiczne, chociaż wciąż wydajne rozwiązanie.</span><span class="sxs-lookup"><span data-stu-id="345a9-183">Standard Storage is backed by HDDs, and delivers cost-effective storage while still being performant.</span></span> <span data-ttu-id="345a9-184">Dyski standardowe idealnie nadają się do deweloperów ekonomiczne i testów obciążenia.</span><span class="sxs-lookup"><span data-stu-id="345a9-184">Standard disks are ideal for a cost effective dev and test workload.</span></span>

### <a name="premium-disk"></a><span data-ttu-id="345a9-185">Dysku Premium</span><span class="sxs-lookup"><span data-stu-id="345a9-185">Premium disk</span></span>

<span data-ttu-id="345a9-186">Dyski Premium bazują na dysk SSD dysku wysokiej wydajności i małych opóźnień.</span><span class="sxs-lookup"><span data-stu-id="345a9-186">Premium disks are backed by SSD-based high-performance, low-latency disk.</span></span> <span data-ttu-id="345a9-187">Idealny dla maszyn wirtualnych obciążeniu produkcji.</span><span class="sxs-lookup"><span data-stu-id="345a9-187">Perfect for VMs running production workload.</span></span> <span data-ttu-id="345a9-188">Magazyn w warstwie Premium obsługuje serii DS, DSv2 serii GS-series i FS serii maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="345a9-188">Premium Storage supports DS-series, DSv2-series, GS-series, and FS-series VMs.</span></span> <span data-ttu-id="345a9-189">Dysków w warstwie Premium są dostępne w trzech typów (P10, P20, P30), rozmiar hello dysku hello Określa typ dysku hello.</span><span class="sxs-lookup"><span data-stu-id="345a9-189">Premium disks come in three types (P10, P20, P30), hello size of hello disk determines hello disk type.</span></span> <span data-ttu-id="345a9-190">Podczas wybierania, wartość hello rozmiaru dysku jest zaokrąglana toohello dalej typu.</span><span class="sxs-lookup"><span data-stu-id="345a9-190">When selecting, a disk size hello value is rounded up toohello next type.</span></span> <span data-ttu-id="345a9-191">Na przykład jeśli rozmiar dysku hello jest mniejsza niż 128 GB, typ dysku hello jest P10.</span><span class="sxs-lookup"><span data-stu-id="345a9-191">For example, if hello disk size is less than 128 GB, hello disk type is P10.</span></span> <span data-ttu-id="345a9-192">Jeśli rozmiar dysku hello wynosi 129 GB i 512, rozmiar hello jest P20.</span><span class="sxs-lookup"><span data-stu-id="345a9-192">If hello disk size is between 129 GB and 512 GB, hello size is a P20.</span></span> <span data-ttu-id="345a9-193">Niczego ponad 512 GB, rozmiar hello jest P30.</span><span class="sxs-lookup"><span data-stu-id="345a9-193">Anything over 512 GB, hello size is a P30.</span></span>

### <a name="premium-disk-performance"></a><span data-ttu-id="345a9-194">Wydajność dysku Premium</span><span class="sxs-lookup"><span data-stu-id="345a9-194">Premium disk performance</span></span>

|<span data-ttu-id="345a9-195">Typ dysku magazynu w warstwie Premium</span><span class="sxs-lookup"><span data-stu-id="345a9-195">Premium storage disk type</span></span> | <span data-ttu-id="345a9-196">P10</span><span class="sxs-lookup"><span data-stu-id="345a9-196">P10</span></span> | <span data-ttu-id="345a9-197">P20</span><span class="sxs-lookup"><span data-stu-id="345a9-197">P20</span></span> | <span data-ttu-id="345a9-198">P30</span><span class="sxs-lookup"><span data-stu-id="345a9-198">P30</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="345a9-199">Rozmiar dysku (zaokrąglony)</span><span class="sxs-lookup"><span data-stu-id="345a9-199">Disk size (round up)</span></span> | <span data-ttu-id="345a9-200">128 GB</span><span class="sxs-lookup"><span data-stu-id="345a9-200">128 GB</span></span> | <span data-ttu-id="345a9-201">512 GB</span><span class="sxs-lookup"><span data-stu-id="345a9-201">512 GB</span></span> | <span data-ttu-id="345a9-202">1024 GB (1 TB)</span><span class="sxs-lookup"><span data-stu-id="345a9-202">1,024 GB (1 TB)</span></span> |
| <span data-ttu-id="345a9-203">Maksymalna liczba operacji wejścia/wyjścia na sekundę na dysk</span><span class="sxs-lookup"><span data-stu-id="345a9-203">Max IOPS per disk</span></span> | <span data-ttu-id="345a9-204">500</span><span class="sxs-lookup"><span data-stu-id="345a9-204">500</span></span> | <span data-ttu-id="345a9-205">2,300</span><span class="sxs-lookup"><span data-stu-id="345a9-205">2,300</span></span> | <span data-ttu-id="345a9-206">5,000</span><span class="sxs-lookup"><span data-stu-id="345a9-206">5,000</span></span> |
<span data-ttu-id="345a9-207">Przepływność na dysk</span><span class="sxs-lookup"><span data-stu-id="345a9-207">Throughput per disk</span></span> | <span data-ttu-id="345a9-208">100 MB/s</span><span class="sxs-lookup"><span data-stu-id="345a9-208">100 MB/s</span></span> | <span data-ttu-id="345a9-209">150 MB/s</span><span class="sxs-lookup"><span data-stu-id="345a9-209">150 MB/s</span></span> | <span data-ttu-id="345a9-210">200 MB/s</span><span class="sxs-lookup"><span data-stu-id="345a9-210">200 MB/s</span></span> |

<span data-ttu-id="345a9-211">Gdy hello powyżej tabeli określa maksymalną liczbę IOPS dla każdego dysku, można osiągnąć wyższy poziom wydajności przez stosowanie wielu dysków z danymi.</span><span class="sxs-lookup"><span data-stu-id="345a9-211">While hello above table identifies max IOPS per disk, a higher level of performance can be achieved by striping multiple data disks.</span></span> <span data-ttu-id="345a9-212">Na przykład Standard_GS5 maszyny Wirtualnej można osiągnąć maksymalnie 80 000 IOPS.</span><span class="sxs-lookup"><span data-stu-id="345a9-212">For instance, a Standard_GS5 VM can achieve a maximum of 80,000 IOPS.</span></span> <span data-ttu-id="345a9-213">Aby uzyskać szczegółowe informacje o maksymalnej IOPS dla maszyny Wirtualnej, zobacz [rozmiarów maszyn wirtualnych systemu Linux](sizes.md).</span><span class="sxs-lookup"><span data-stu-id="345a9-213">For detailed information on max IOPS per VM, see [Linux VM sizes](sizes.md).</span></span>

## <a name="create-and-attach-disks"></a><span data-ttu-id="345a9-214">Utwórz i Dołącz dysków</span><span class="sxs-lookup"><span data-stu-id="345a9-214">Create and attach disks</span></span>

<span data-ttu-id="345a9-215">Dyski danych można tworzyć i dołączone w czasie tworzenia maszyny Wirtualnej lub tooan istniejącej maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="345a9-215">Data disks can be created and attached at VM creation time or tooan existing VM.</span></span>

### <a name="attach-disk-at-vm-creation"></a><span data-ttu-id="345a9-216">Dołączenie dysku podczas tworzenia maszyny Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="345a9-216">Attach disk at VM creation</span></span>

<span data-ttu-id="345a9-217">Utwórz grupę zasobów o hello [Tworzenie grupy az](https://docs.microsoft.com/cli/azure/group#create) polecenia.</span><span class="sxs-lookup"><span data-stu-id="345a9-217">Create a resource group with hello [az group create](https://docs.microsoft.com/cli/azure/group#create) command.</span></span> 

```azurecli-interactive 
az group create --name myResourceGroupDisk --location eastus
```

<span data-ttu-id="345a9-218">Utwórz maszynę Wirtualną przy użyciu hello [tworzenia maszyny wirtualnej az]( /cli/azure/vm#create) polecenia.</span><span class="sxs-lookup"><span data-stu-id="345a9-218">Create a VM using hello [az vm create]( /cli/azure/vm#create) command.</span></span> <span data-ttu-id="345a9-219">Witaj `--datadisk-sizes-gb` argument jest używany toospecify, że dodatkowy dysk należy utworzyć i dołączyć toohello maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="345a9-219">hello `--datadisk-sizes-gb` argument is used toospecify that an additional disk should be created and attached toohello virtual machine.</span></span> <span data-ttu-id="345a9-220">toocreate i dołączyć więcej niż jeden dysk, użyj rozdzieloną spacjami listę wartości rozmiaru dysku.</span><span class="sxs-lookup"><span data-stu-id="345a9-220">toocreate and attach more than one disk, use a space-delimited list of disk size values.</span></span> <span data-ttu-id="345a9-221">W hello poniższy przykład maszyna wirtualna zostanie utworzona z dwóch dysków, zarówno 128 GB.</span><span class="sxs-lookup"><span data-stu-id="345a9-221">In hello following example, a VM is created with two data disks, both 128 GB.</span></span> <span data-ttu-id="345a9-222">Ponieważ hello rozmiary dysków wynoszą 128 GB, te dyski obydwa są skonfigurowane jako P10s, które zapewniają maksymalną 500 IOPS dla każdego dysku.</span><span class="sxs-lookup"><span data-stu-id="345a9-222">Because hello disk sizes are 128 GB, these disks are both configured as P10s, which provide maximum 500 IOPS per disk.</span></span>

```azurecli-interactive 
az vm create \
  --resource-group myResourceGroupDisk \
  --name myVM \
  --image UbuntuLTS \
  --size Standard_DS2_v2 \
  --data-disk-sizes-gb 128 128 \
  --generate-ssh-keys
```

### <a name="attach-disk-tooexisting-vm"></a><span data-ttu-id="345a9-223">Dołącz tooexisting dysku maszyny Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="345a9-223">Attach disk tooexisting VM</span></span>

<span data-ttu-id="345a9-224">toocreate i dołączyć nowego dysku tooan istniejącej maszyny wirtualnej, użyj hello [dołączyć dysku maszyny wirtualnej az](/cli/azure/vm/disk#attach) polecenia.</span><span class="sxs-lookup"><span data-stu-id="345a9-224">toocreate and attach a new disk tooan existing virtual machine, use hello [az vm disk attach](/cli/azure/vm/disk#attach) command.</span></span> <span data-ttu-id="345a9-225">Witaj poniższy przykład tworzy dysk premium 128 GB w rozmiarze i dołącza go toohello maszyny Wirtualnej utworzone w ostatnim kroku hello.</span><span class="sxs-lookup"><span data-stu-id="345a9-225">hello following example creates a premium disk, 128 gigabytes in size, and attaches it toohello VM created in hello last step.</span></span>

```azurecli-interactive 
az vm disk attach --vm-name myVM --resource-group myResourceGroupDisk --disk myDataDisk --size-gb 128 --sku Premium_LRS --new 
```

## <a name="prepare-data-disks"></a><span data-ttu-id="345a9-226">Przygotowanie dysków z danymi</span><span class="sxs-lookup"><span data-stu-id="345a9-226">Prepare data disks</span></span>

<span data-ttu-id="345a9-227">Po dysku maszyny wirtualnej podłączone toohello, system operacyjny hello musi toobe skonfigurowane toouse hello dysku.</span><span class="sxs-lookup"><span data-stu-id="345a9-227">Once a disk has been attached toohello virtual machine, hello operating system needs toobe configured toouse hello disk.</span></span> <span data-ttu-id="345a9-228">Witaj poniższy przykład pokazuje, jak toomanually konfigurowania dysku.</span><span class="sxs-lookup"><span data-stu-id="345a9-228">hello following example shows how toomanually configure a disk.</span></span> <span data-ttu-id="345a9-229">Ten proces można również zautomatyzować, używając inicjowaniem chmury, które są objęte w [nowsze samouczek](./tutorial-automate-vm-deployment.md).</span><span class="sxs-lookup"><span data-stu-id="345a9-229">This process can also be automated using cloud-init, which is covered in a [later tutorial](./tutorial-automate-vm-deployment.md).</span></span>

### <a name="manual-configuration"></a><span data-ttu-id="345a9-230">Konfiguracja ręczna</span><span class="sxs-lookup"><span data-stu-id="345a9-230">Manual configuration</span></span>

<span data-ttu-id="345a9-231">Utwórz połączenie SSH z maszyną wirtualną hello.</span><span class="sxs-lookup"><span data-stu-id="345a9-231">Create an SSH connection with hello virtual machine.</span></span> <span data-ttu-id="345a9-232">Zastąp hello publicznego adresu IP maszyny wirtualnej hello hello przykładowego adresu IP.</span><span class="sxs-lookup"><span data-stu-id="345a9-232">Replace hello example IP address with hello public IP of hello virtual machine.</span></span>

```azurecli-interactive 
ssh 52.174.34.95
```

<span data-ttu-id="345a9-233">Witaj partycji z `fdisk`.</span><span class="sxs-lookup"><span data-stu-id="345a9-233">Partition hello disk with `fdisk`.</span></span>

```bash
(echo n; echo p; echo 1; echo ; echo ; echo w) | sudo fdisk /dev/sdc
```

<span data-ttu-id="345a9-234">Zapis systemu plików toohello partycji przy użyciu hello `mkfs` polecenia.</span><span class="sxs-lookup"><span data-stu-id="345a9-234">Write a file system toohello partition by using hello `mkfs` command.</span></span>

```bash
sudo mkfs -t ext4 /dev/sdc1
```

<span data-ttu-id="345a9-235">Zainstaluj nowy dysk hello tak, aby była dostępna w systemie operacyjnym hello.</span><span class="sxs-lookup"><span data-stu-id="345a9-235">Mount hello new disk so that it is accessible in hello operating system.</span></span>

```bash
sudo mkdir /datadrive && sudo mount /dev/sdc1 /datadrive
```

<span data-ttu-id="345a9-236">dysk Hello jest teraz dostępna za pośrednictwem hello *datadrive* punktu instalacji, który można zweryfikować, uruchamiając hello `df -h` polecenia.</span><span class="sxs-lookup"><span data-stu-id="345a9-236">hello disk can now be accessed through hello *datadrive* mountpoint, which can be verified by running hello `df -h` command.</span></span> 

```bash
df -h
```

<span data-ttu-id="345a9-237">dane wyjściowe Hello zawierają hello nowy dysk zainstalowany na */datadrive*.</span><span class="sxs-lookup"><span data-stu-id="345a9-237">hello output shows hello new drive mounted on */datadrive*.</span></span>

```bash
Filesystem      Size  Used Avail Use% Mounted on
/dev/sda1        30G  1.4G   28G   5% /
/dev/sdb1       6.8G   16M  6.4G   1% /mnt
/dev/sdc1        50G   52M   47G   1% /datadrive
```

<span data-ttu-id="345a9-238">tooensure, który hello dysku jest ponownej instalacji po ponownym uruchomieniu, należy dodać go toohello */etc/fstab* pliku.</span><span class="sxs-lookup"><span data-stu-id="345a9-238">tooensure that hello drive is remounted after a reboot, it must be added toohello */etc/fstab* file.</span></span> <span data-ttu-id="345a9-239">toodo tak, Pobierz hello UUID dysku hello z hello `blkid` narzędzia.</span><span class="sxs-lookup"><span data-stu-id="345a9-239">toodo so, get hello UUID of hello disk with hello `blkid` utility.</span></span>

```bash
sudo -i blkid
```

<span data-ttu-id="345a9-240">dane wyjściowe Hello Wyświetla hello identyfikatora UUID dysku hello `/dev/sdc1` w takim przypadku.</span><span class="sxs-lookup"><span data-stu-id="345a9-240">hello output displays hello UUID of hello drive, `/dev/sdc1` in this case.</span></span>

```bash
/dev/sdc1: UUID="33333333-3b3b-3c3c-3d3d-3e3e3e3e3e3e" TYPE="ext4"
```

<span data-ttu-id="345a9-241">Dodaj wiersz toohello podobne, po toohello */etc/fstab* pliku.</span><span class="sxs-lookup"><span data-stu-id="345a9-241">Add a line similar toohello following toohello */etc/fstab* file.</span></span> <span data-ttu-id="345a9-242">Również należy pamiętać, że zapis bariery można wyłączyć za pomocą *bariery = 0*, ta konfiguracja może poprawić wydajność dysku.</span><span class="sxs-lookup"><span data-stu-id="345a9-242">Also note that write barriers can be disabled using *barrier=0*, this configuration can improve disk performance.</span></span> 

```bash
UUID=33333333-3b3b-3c3c-3d3d-3e3e3e3e3e3e   /datadrive  ext4    defaults,nofail,barrier=0   1  2
```

<span data-ttu-id="345a9-243">Teraz, gdy hello dysk został skonfigurowany, Zamknij sesję SSH hello.</span><span class="sxs-lookup"><span data-stu-id="345a9-243">Now that hello disk has been configured, close hello SSH session.</span></span>

```bash
exit
```

## <a name="resize-vm-disk"></a><span data-ttu-id="345a9-244">Zmiana rozmiaru dysku maszyny Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="345a9-244">Resize VM disk</span></span>

<span data-ttu-id="345a9-245">Po wdrożeniu maszyny Wirtualnej, dysk systemu operacyjnego hello lub żadnych dysków dołączonych danych można zwiększyć rozmiar.</span><span class="sxs-lookup"><span data-stu-id="345a9-245">Once a VM has been deployed, hello operating system disk or any attached data disks can be increased in size.</span></span> <span data-ttu-id="345a9-246">Zwiększenie rozmiaru dysku hello jest korzystne w przypadku, gdy wymagające więcej miejsca do magazynowania lub wyższego poziomu wydajności (P10 P20, P30).</span><span class="sxs-lookup"><span data-stu-id="345a9-246">Increasing hello size of a disk is beneficial when needing more storage space or a higher level of performance (P10, P20, P30).</span></span> <span data-ttu-id="345a9-247">Zauważ, że dyski nie można zmniejszyć rozmiar.</span><span class="sxs-lookup"><span data-stu-id="345a9-247">Note, disks cannot be decreased in size.</span></span>

<span data-ttu-id="345a9-248">Przed zwiększeniem rozmiaru dysku, hello identyfikatora lub nazwy dysku hello jest wymagana.</span><span class="sxs-lookup"><span data-stu-id="345a9-248">Before increasing disk size, hello Id or name of hello disk is needed.</span></span> <span data-ttu-id="345a9-249">Użyj hello [Lista dysków az](/cli/azure/vm/disk#list) tooreturn polecenia wszystkich dysków w grupie zasobów.</span><span class="sxs-lookup"><span data-stu-id="345a9-249">Use hello [az disk list](/cli/azure/vm/disk#list) command tooreturn all disks in a resource group.</span></span> <span data-ttu-id="345a9-250">Zanotuj nazwę dysku hello chcesz tooresize.</span><span class="sxs-lookup"><span data-stu-id="345a9-250">Take note of hello disk name that you would like tooresize.</span></span>

```azurecli-interactive 
az disk list -g myResourceGroupDisk --query '[*].{Name:name,Gb:diskSizeGb,Tier:accountType}' --output table
```

<span data-ttu-id="345a9-251">należy również deallocated Hello maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="345a9-251">hello VM must also be deallocated.</span></span> <span data-ttu-id="345a9-252">Użyj hello [deallocate wirtualna az]( /cli/azure/vm#deallocate) polecenia toostop i cofnięcia przydzielenia hello maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="345a9-252">Use hello [az vm deallocate]( /cli/azure/vm#deallocate) command toostop and deallocate hello VM.</span></span>

```azurecli-interactive 
az vm deallocate --resource-group myResourceGroupDisk --name myVM
```

<span data-ttu-id="345a9-253">Użyj hello [aktualizacja dysku az](/cli/azure/vm/disk#update) polecenia tooresize hello dysku.</span><span class="sxs-lookup"><span data-stu-id="345a9-253">Use hello [az disk update](/cli/azure/vm/disk#update) command tooresize hello disk.</span></span> <span data-ttu-id="345a9-254">W tym przykładzie zmienia rozmiar dysku o nazwie *myDataDisk* too1 terabajt.</span><span class="sxs-lookup"><span data-stu-id="345a9-254">This example resizes a disk named *myDataDisk* too1 terabyte.</span></span>

```azurecli-interactive 
az disk update --name myDataDisk --resource-group myResourceGroupDisk --size-gb 1023
```

<span data-ttu-id="345a9-255">Po zakończeniu operacji zmiany rozmiaru hello start hello maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="345a9-255">Once hello resize operation has completed, start hello VM.</span></span>

```azurecli-interactive 
az vm start --resource-group myResourceGroupDisk --name myVM
```

<span data-ttu-id="345a9-256">Jeśli został zmieniony hello dysk systemu operacyjnego, jest automatycznie rozszerzana hello partycji.</span><span class="sxs-lookup"><span data-stu-id="345a9-256">If you’ve resized hello operating system disk, hello partition is automatically be expanded.</span></span> <span data-ttu-id="345a9-257">Jeśli zmieniono dysk z danymi, wszystkie partycje bieżącego muszą toobe rozwinięty w systemie operacyjnym hello maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="345a9-257">If you have resized a data disk, any current partitions need toobe expanded in hello VMs operating system.</span></span>

## <a name="snapshot-azure-disks"></a><span data-ttu-id="345a9-258">Migawki dysków Azure</span><span class="sxs-lookup"><span data-stu-id="345a9-258">Snapshot Azure disks</span></span>

<span data-ttu-id="345a9-259">Tworzenie migawki dysku tworzy odczytu tylko, w momencie kopię hello dysku.</span><span class="sxs-lookup"><span data-stu-id="345a9-259">Taking a disk snapshot creates a read only, point-in-time copy of hello disk.</span></span> <span data-ttu-id="345a9-260">Migawki maszyny Wirtualnej platformy Azure są przydatne do szybkiego Zapisywanie stanu hello maszyny wirtualnej przed wprowadzeniem zmian w konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="345a9-260">Azure VM snapshots are useful for quickly saving hello state of a VM before making configuration changes.</span></span> <span data-ttu-id="345a9-261">W przypadku hello hello zmian konfiguracji potwierdzenia toobe niepożądane, można przywrócić stan maszyny Wirtualnej przy użyciu hello migawki.</span><span class="sxs-lookup"><span data-stu-id="345a9-261">In hello event hello configuration changes prove toobe undesired, VM state can be restored using hello snapshot.</span></span> <span data-ttu-id="345a9-262">Gdy maszyna wirtualna ma więcej niż jeden dysk, migawki każdego dysku, niezależnie od hello innych użytkowników.</span><span class="sxs-lookup"><span data-stu-id="345a9-262">When a VM has more than one disk, a snapshot is taken of each disk independently of hello others.</span></span> <span data-ttu-id="345a9-263">Do wykonywania kopii zapasowych spójności aplikacji, należy wziąć pod uwagę zatrzymywanie hello maszyny Wirtualnej przed wykonaniem migawki dysków.</span><span class="sxs-lookup"><span data-stu-id="345a9-263">For taking application consistent backups, consider stopping hello VM before taking disk snapshots.</span></span> <span data-ttu-id="345a9-264">Można również użyć hello [usługi Kopia zapasowa Azure](/azure/backup/), co pozwoli tooperform możesz automatycznego tworzenia kopii zapasowych podczas hello wirtualna jest uruchomiona.</span><span class="sxs-lookup"><span data-stu-id="345a9-264">Alternatively, use hello [Azure Backup service](/azure/backup/), which enables you tooperform automated backups while hello VM is running.</span></span>

### <a name="create-snapshot"></a><span data-ttu-id="345a9-265">Tworzenie migawki</span><span class="sxs-lookup"><span data-stu-id="345a9-265">Create snapshot</span></span>

<span data-ttu-id="345a9-266">Przed utworzeniem migawek dysków maszyny wirtualnej, hello identyfikatora lub nazwy dysku hello jest wymagane.</span><span class="sxs-lookup"><span data-stu-id="345a9-266">Before creating a virtual machine disk snapshot, hello Id or name of hello disk is needed.</span></span> <span data-ttu-id="345a9-267">Użyj hello [az maszyny wirtualnej pokazu](https://docs.microsoft.com/en-us/cli/azure/vm#show) identyfikator dysku hello tooreturn polecenia. W tym przykładzie identyfikator dysku hello jest przechowywana w zmiennej, dzięki czemu mogą być używane w kolejnym kroku.</span><span class="sxs-lookup"><span data-stu-id="345a9-267">Use hello [az vm show](https://docs.microsoft.com/en-us/cli/azure/vm#show) command tooreturn hello disk id. In this example, hello disk id is stored in a variable so that it can be used in a later step.</span></span>

```azurecli-interactive 
osdiskid=$(az vm show -g myResourceGroupDisk -n myVM --query "storageProfile.osDisk.managedDisk.id" -o tsv)
```

<span data-ttu-id="345a9-268">Teraz, gdy masz hello identyfikator dysku maszyny wirtualnej hello hello następujące polecenie tworzy migawkę hello dysku.</span><span class="sxs-lookup"><span data-stu-id="345a9-268">Now that you have hello id of hello virtual machine disk, hello following command creates a snapshot of hello disk.</span></span>

```azurcli
az snapshot create -g myResourceGroupDisk --source "$osdiskid" --name osDisk-backup
```

### <a name="create-disk-from-snapshot"></a><span data-ttu-id="345a9-269">Utwórz dysk z migawki</span><span class="sxs-lookup"><span data-stu-id="345a9-269">Create disk from snapshot</span></span>

<span data-ttu-id="345a9-270">Następnie można przekonwertować tej migawki na dysku, który może być maszyny wirtualnej hello toorecreate używane.</span><span class="sxs-lookup"><span data-stu-id="345a9-270">This snapshot can then be converted into a disk, which can be used toorecreate hello virtual machine.</span></span>

```azurecli-interactive 
az disk create --resource-group myResourceGroupDisk --name mySnapshotDisk --source osDisk-backup
```

### <a name="restore-virtual-machine-from-snapshot"></a><span data-ttu-id="345a9-271">Przywracanie z migawki maszyny wirtualnej</span><span class="sxs-lookup"><span data-stu-id="345a9-271">Restore virtual machine from snapshot</span></span>

<span data-ttu-id="345a9-272">odzyskiwanie maszyny wirtualnej toodemonstrate, Usuń hello istniejącej maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="345a9-272">toodemonstrate virtual machine recovery, delete hello existing virtual machine.</span></span> 

```azurecli-interactive 
az vm delete --resource-group myResourceGroupDisk --name myVM
```

<span data-ttu-id="345a9-273">Utwórz nową maszynę wirtualną na podstawie hello migawki dysku.</span><span class="sxs-lookup"><span data-stu-id="345a9-273">Create a new virtual machine from hello snapshot disk.</span></span>

```azurecli-interactive 
az vm create --resource-group myResourceGroupDisk --name myVM --attach-os-disk mySnapshotDisk --os-type linux
```

### <a name="reattach-data-disk"></a><span data-ttu-id="345a9-274">Podłącz dysk danych</span><span class="sxs-lookup"><span data-stu-id="345a9-274">Reattach data disk</span></span>

<span data-ttu-id="345a9-275">Wszystkie dyski danych powinny maszyny wirtualnej toohello toobe ponownie nałożona.</span><span class="sxs-lookup"><span data-stu-id="345a9-275">All data disks need toobe reattached toohello virtual machine.</span></span>

<span data-ttu-id="345a9-276">Najpierw znaleźć nazwy dysku danych hello przy użyciu hello [Lista dysków az](https://docs.microsoft.com/cli/azure/disk#list) polecenia.</span><span class="sxs-lookup"><span data-stu-id="345a9-276">First find hello data disk name using hello [az disk list](https://docs.microsoft.com/cli/azure/disk#list) command.</span></span> <span data-ttu-id="345a9-277">W tym przykładzie miejsca hello nazwę dysku hello w zmiennej o nazwie *datadisk*, która jest używana w hello następnego kroku.</span><span class="sxs-lookup"><span data-stu-id="345a9-277">This example places hello name of hello disk in a variable named *datadisk*, which is used in hello next step.</span></span>

```azurecli-interactive 
datadisk=$(az disk list -g myResourceGroupDisk --query "[?contains(name,'myVM')].[name]" -o tsv)
```

<span data-ttu-id="345a9-278">Użyj hello [dołączyć dysku maszyny wirtualnej az](https://docs.microsoft.com/cli/azure/vm/disk#attach) polecenia tooattach hello dysku.</span><span class="sxs-lookup"><span data-stu-id="345a9-278">Use hello [az vm disk attach](https://docs.microsoft.com/cli/azure/vm/disk#attach) command tooattach hello disk.</span></span>

```azurecli-interactive 
az vm disk attach –g myResourceGroupDisk –-vm-name myVM –-disk $datadisk
```

## <a name="next-steps"></a><span data-ttu-id="345a9-279">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="345a9-279">Next steps</span></span>

<span data-ttu-id="345a9-280">W tym samouczku przedstawiono tematy dysków maszyny Wirtualnej takich jak:</span><span class="sxs-lookup"><span data-stu-id="345a9-280">In this tutorial, you learned about VM disks topics such as:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="345a9-281">Dyski systemu operacyjnego i tymczasowego</span><span class="sxs-lookup"><span data-stu-id="345a9-281">OS disks and temporary disks</span></span>
> * <span data-ttu-id="345a9-282">Dyski danych</span><span class="sxs-lookup"><span data-stu-id="345a9-282">Data disks</span></span>
> * <span data-ttu-id="345a9-283">Standard i dysków w warstwie Premium</span><span class="sxs-lookup"><span data-stu-id="345a9-283">Standard and Premium disks</span></span>
> * <span data-ttu-id="345a9-284">Wydajność dysku</span><span class="sxs-lookup"><span data-stu-id="345a9-284">Disk performance</span></span>
> * <span data-ttu-id="345a9-285">Dołączanie i przygotowywania dysków z danymi</span><span class="sxs-lookup"><span data-stu-id="345a9-285">Attaching and preparing data disks</span></span>
> * <span data-ttu-id="345a9-286">Zmiana rozmiaru dysków</span><span class="sxs-lookup"><span data-stu-id="345a9-286">Resizing disks</span></span>
> * <span data-ttu-id="345a9-287">Migawki dysków</span><span class="sxs-lookup"><span data-stu-id="345a9-287">Disk snapshots</span></span>

<span data-ttu-id="345a9-288">Przejdź dalej toolearn samouczka toohello dotyczące automatyzowania konfiguracji maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="345a9-288">Advance toohello next tutorial toolearn about automating VM configuration.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="345a9-289">Automatyzowanie konfiguracji maszyny wirtualnej</span><span class="sxs-lookup"><span data-stu-id="345a9-289">Automate VM configuration</span></span>](./tutorial-automate-vm-deployment.md)
