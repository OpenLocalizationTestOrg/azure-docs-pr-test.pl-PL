---
title: "Zarządzanie dyskami Azure z wiersza polecenia platformy Azure | Dokumentacja firmy Microsoft"
description: "Samouczek — Zarządzanie dyskami Azure z wiersza polecenia platformy Azure"
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
ms.openlocfilehash: d77dd2b44dca8cee6fa2e93e79cda76c80ccfe1a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="manage-azure-disks-with-the-azure-cli"></a><span data-ttu-id="98faf-103">Zarządzanie dyskami Azure z wiersza polecenia platformy Azure</span><span class="sxs-lookup"><span data-stu-id="98faf-103">Manage Azure disks with the Azure CLI</span></span>

<span data-ttu-id="98faf-104">Maszyny wirtualne platformy Azure dysków do przechowywania systemu operacyjnego, aplikacje i dane maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="98faf-104">Azure virtual machines use disks to store the VMs operating system, applications, and data.</span></span> <span data-ttu-id="98faf-105">Podczas tworzenia maszyny Wirtualnej jest ważne wybrać rozmiar dysku i odpowiednie do oczekiwanego obciążenia w konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="98faf-105">When creating a VM it is important to choose a disk size and configuration appropriate to the expected workload.</span></span> <span data-ttu-id="98faf-106">W tym samouczku opisano wdrażanie i Zarządzanie dyskami maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="98faf-106">This tutorial covers deploying and managing VM disks.</span></span> <span data-ttu-id="98faf-107">Informacje o:</span><span class="sxs-lookup"><span data-stu-id="98faf-107">You learn about:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="98faf-108">Dyski systemu operacyjnego i tymczasowego</span><span class="sxs-lookup"><span data-stu-id="98faf-108">OS disks and temporary disks</span></span>
> * <span data-ttu-id="98faf-109">Dyski danych</span><span class="sxs-lookup"><span data-stu-id="98faf-109">Data disks</span></span>
> * <span data-ttu-id="98faf-110">Standard i dysków w warstwie Premium</span><span class="sxs-lookup"><span data-stu-id="98faf-110">Standard and Premium disks</span></span>
> * <span data-ttu-id="98faf-111">Wydajność dysku</span><span class="sxs-lookup"><span data-stu-id="98faf-111">Disk performance</span></span>
> * <span data-ttu-id="98faf-112">Dołączanie i przygotowywania dysków z danymi</span><span class="sxs-lookup"><span data-stu-id="98faf-112">Attaching and preparing data disks</span></span>
> * <span data-ttu-id="98faf-113">Zmiana rozmiaru dysków</span><span class="sxs-lookup"><span data-stu-id="98faf-113">Resizing disks</span></span>
> * <span data-ttu-id="98faf-114">Migawki dysków</span><span class="sxs-lookup"><span data-stu-id="98faf-114">Disk snapshots</span></span>


[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="98faf-115">Jeśli wybierzesz do zainstalowania i używania interfejsu wiersza polecenia lokalnie, w tym samouczku wymaga używasz interfejsu wiersza polecenia Azure w wersji 2.0.4 lub nowszej.</span><span class="sxs-lookup"><span data-stu-id="98faf-115">If you choose to install and use the CLI locally, this tutorial requires that you are running the Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="98faf-116">Uruchom polecenie `az --version`, aby dowiedzieć się, jaka wersja jest używana.</span><span class="sxs-lookup"><span data-stu-id="98faf-116">Run `az --version` to find the version.</span></span> <span data-ttu-id="98faf-117">Jeśli konieczna będzie instalacja lub uaktualnienie, zobacz [Instalowanie interfejsu wiersza polecenia platformy Azure 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="98faf-117">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="default-azure-disks"></a><span data-ttu-id="98faf-118">Domyślna dysku systemu Azure</span><span class="sxs-lookup"><span data-stu-id="98faf-118">Default Azure disks</span></span>

<span data-ttu-id="98faf-119">Po utworzeniu maszyny wirtualnej platformy Azure, dwa dyski są automatycznie dołączane do maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="98faf-119">When an Azure virtual machine is created, two disks are automatically attached to the virtual machine.</span></span> 

<span data-ttu-id="98faf-120">**Dysk systemu operacyjnego** -dysków systemu operacyjnego może być o rozmiarze maksymalnie 1 terabajt oraz hostów maszyn wirtualnych systemu operacyjnego.</span><span class="sxs-lookup"><span data-stu-id="98faf-120">**Operating system disk** - Operating system disks can be sized up to 1 terabyte, and hosts the VMs operating system.</span></span> <span data-ttu-id="98faf-121">Dysk systemu operacyjnego jest oznaczony */dev/sda* domyślnie.</span><span class="sxs-lookup"><span data-stu-id="98faf-121">The OS disk is labeled */dev/sda* by default.</span></span> <span data-ttu-id="98faf-122">Dysk buforowanie konfiguracji dysku systemu operacyjnego jest zoptymalizowana pod kątem wydajności systemu operacyjnego.</span><span class="sxs-lookup"><span data-stu-id="98faf-122">The disk caching configuration of the OS disk is optimized for OS performance.</span></span> <span data-ttu-id="98faf-123">Z powodu tej konfiguracji dysku systemu operacyjnego **nie powinien** hosta aplikacji i danych.</span><span class="sxs-lookup"><span data-stu-id="98faf-123">Because of this configuration, the OS disk **should not** host applications or data.</span></span> <span data-ttu-id="98faf-124">Dla aplikacji i danych użycia dysków danych, które opisano szczegółowo w dalszej części tego artykułu.</span><span class="sxs-lookup"><span data-stu-id="98faf-124">For applications and data, use data disks, which are detailed later in this article.</span></span> 

<span data-ttu-id="98faf-125">**Dysku tymczasowym** -tymczasowego dysków używać dysków SSD, który znajduje się na tym samym hoście Azure co maszyna wirtualna.</span><span class="sxs-lookup"><span data-stu-id="98faf-125">**Temporary disk** - Temporary disks use a solid-state drive that is located on the same Azure host as the VM.</span></span> <span data-ttu-id="98faf-126">Tymczasowy dyski są wysokiej wydajności i mogą być używane do operacji, takich jak przetwarzanie danych tymczasowych.</span><span class="sxs-lookup"><span data-stu-id="98faf-126">Temp disks are highly performant and may be used for operations such as temporary data processing.</span></span> <span data-ttu-id="98faf-127">Jednak jeśli maszyna wirtualna zostanie przeniesiona do nowego hosta, zostaną usunięte wszystkie dane przechowywane na dysku tymczasowym.</span><span class="sxs-lookup"><span data-stu-id="98faf-127">However, if the VM is moved to a new host, any data stored on a temporary disk is removed.</span></span> <span data-ttu-id="98faf-128">Rozmiar dysku tymczasowym zależy od rozmiaru maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="98faf-128">The size of the temporary disk is determined by the VM size.</span></span> <span data-ttu-id="98faf-129">Tymczasowe dyski są oznaczone jako */dev/sdb* i mieć punktu instalacji z *katalogu/mnt*.</span><span class="sxs-lookup"><span data-stu-id="98faf-129">Temporary disks are labeled */dev/sdb* and have a mountpoint of */mnt*.</span></span>

### <a name="temporary-disk-sizes"></a><span data-ttu-id="98faf-130">Rozmiary dysku tymczasowym</span><span class="sxs-lookup"><span data-stu-id="98faf-130">Temporary disk sizes</span></span>

| <span data-ttu-id="98faf-131">Typ</span><span class="sxs-lookup"><span data-stu-id="98faf-131">Type</span></span> | <span data-ttu-id="98faf-132">Rozmiar maszyny Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="98faf-132">VM Size</span></span> | <span data-ttu-id="98faf-133">Maksymalny rozmiar dysku tymczasowego (GB)</span><span class="sxs-lookup"><span data-stu-id="98faf-133">Max temp disk size (GB)</span></span> |
|----|----|----|
| [<span data-ttu-id="98faf-134">Zastosowania ogólne</span><span class="sxs-lookup"><span data-stu-id="98faf-134">General purpose</span></span>](sizes-general.md) | <span data-ttu-id="98faf-135">A i serii D</span><span class="sxs-lookup"><span data-stu-id="98faf-135">A and D series</span></span> | <span data-ttu-id="98faf-136">800</span><span class="sxs-lookup"><span data-stu-id="98faf-136">800</span></span> |
| [<span data-ttu-id="98faf-137">Optymalizacja pod kątem obliczeń</span><span class="sxs-lookup"><span data-stu-id="98faf-137">Compute optimized</span></span>](sizes-compute.md) | <span data-ttu-id="98faf-138">Seria F</span><span class="sxs-lookup"><span data-stu-id="98faf-138">F series</span></span> | <span data-ttu-id="98faf-139">800</span><span class="sxs-lookup"><span data-stu-id="98faf-139">800</span></span> |
| [<span data-ttu-id="98faf-140">Optymalizacja pod kątem pamięci</span><span class="sxs-lookup"><span data-stu-id="98faf-140">Memory optimized</span></span>](../virtual-machines-windows-sizes-memory.md) | <span data-ttu-id="98faf-141">D i G serii</span><span class="sxs-lookup"><span data-stu-id="98faf-141">D and G series</span></span> | <span data-ttu-id="98faf-142">6144</span><span class="sxs-lookup"><span data-stu-id="98faf-142">6144</span></span> |
| [<span data-ttu-id="98faf-143">Optymalizacja pod kątem magazynu</span><span class="sxs-lookup"><span data-stu-id="98faf-143">Storage optimized</span></span>](../virtual-machines-windows-sizes-storage.md) | <span data-ttu-id="98faf-144">Seria L</span><span class="sxs-lookup"><span data-stu-id="98faf-144">L series</span></span> | <span data-ttu-id="98faf-145">5630</span><span class="sxs-lookup"><span data-stu-id="98faf-145">5630</span></span> |
| [<span data-ttu-id="98faf-146">Procesor GPU</span><span class="sxs-lookup"><span data-stu-id="98faf-146">GPU</span></span>](sizes-gpu.md) | <span data-ttu-id="98faf-147">N serii</span><span class="sxs-lookup"><span data-stu-id="98faf-147">N series</span></span> | <span data-ttu-id="98faf-148">1440</span><span class="sxs-lookup"><span data-stu-id="98faf-148">1440</span></span> |
| [<span data-ttu-id="98faf-149">Wysoka wydajność</span><span class="sxs-lookup"><span data-stu-id="98faf-149">High performance</span></span>](sizes-hpc.md) | <span data-ttu-id="98faf-150">A i serii H</span><span class="sxs-lookup"><span data-stu-id="98faf-150">A and H series</span></span> | <span data-ttu-id="98faf-151">2000</span><span class="sxs-lookup"><span data-stu-id="98faf-151">2000</span></span> |

## <a name="azure-data-disks"></a><span data-ttu-id="98faf-152">Dyski danych Azure</span><span class="sxs-lookup"><span data-stu-id="98faf-152">Azure data disks</span></span>

<span data-ttu-id="98faf-153">Instalowanie aplikacji i przechowywania danych można dodać dodatkowego dysku z danymi.</span><span class="sxs-lookup"><span data-stu-id="98faf-153">Additional data disks can be added for installing applications and storing data.</span></span> <span data-ttu-id="98faf-154">Dyski danych używanego w sytuacji, gdy wymagane jest trwałe i szybko reagowały pamięci masowej.</span><span class="sxs-lookup"><span data-stu-id="98faf-154">Data disks should be used in any situation where durable and responsive data storage is desired.</span></span> <span data-ttu-id="98faf-155">Każdy dysk danych ma maksymalną pojemność 1 terabajt.</span><span class="sxs-lookup"><span data-stu-id="98faf-155">Each data disk has a maximum capacity of 1 terabyte.</span></span> <span data-ttu-id="98faf-156">Rozmiar maszyny wirtualnej Określa, jak wiele dysków z danymi może zostać dołączony do maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="98faf-156">The size of the virtual machine determines how many data disks can be attached to a VM.</span></span> <span data-ttu-id="98faf-157">Dla każdej podstawowej maszyny Wirtualnej można dołączyć danych dwóch dysków.</span><span class="sxs-lookup"><span data-stu-id="98faf-157">For each VM core, two data disks can be attached.</span></span> 

### <a name="max-data-disks-per-vm"></a><span data-ttu-id="98faf-158">Maksymalna liczba dysków z danymi dla maszyny Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="98faf-158">Max data disks per VM</span></span>

| <span data-ttu-id="98faf-159">Typ</span><span class="sxs-lookup"><span data-stu-id="98faf-159">Type</span></span> | <span data-ttu-id="98faf-160">Rozmiar maszyny Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="98faf-160">VM Size</span></span> | <span data-ttu-id="98faf-161">Maksymalna liczba dysków z danymi dla maszyny Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="98faf-161">Max data disks per VM</span></span> |
|----|----|----|
| [<span data-ttu-id="98faf-162">Zastosowania ogólne</span><span class="sxs-lookup"><span data-stu-id="98faf-162">General purpose</span></span>](sizes-general.md) | <span data-ttu-id="98faf-163">A i serii D</span><span class="sxs-lookup"><span data-stu-id="98faf-163">A and D series</span></span> | <span data-ttu-id="98faf-164">32</span><span class="sxs-lookup"><span data-stu-id="98faf-164">32</span></span> |
| [<span data-ttu-id="98faf-165">Optymalizacja pod kątem obliczeń</span><span class="sxs-lookup"><span data-stu-id="98faf-165">Compute optimized</span></span>](sizes-compute.md) | <span data-ttu-id="98faf-166">Seria F</span><span class="sxs-lookup"><span data-stu-id="98faf-166">F series</span></span> | <span data-ttu-id="98faf-167">32</span><span class="sxs-lookup"><span data-stu-id="98faf-167">32</span></span> |
| [<span data-ttu-id="98faf-168">Optymalizacja pod kątem pamięci</span><span class="sxs-lookup"><span data-stu-id="98faf-168">Memory optimized</span></span>](../virtual-machines-windows-sizes-memory.md) | <span data-ttu-id="98faf-169">D i G serii</span><span class="sxs-lookup"><span data-stu-id="98faf-169">D and G series</span></span> | <span data-ttu-id="98faf-170">64</span><span class="sxs-lookup"><span data-stu-id="98faf-170">64</span></span> |
| [<span data-ttu-id="98faf-171">Optymalizacja pod kątem magazynu</span><span class="sxs-lookup"><span data-stu-id="98faf-171">Storage optimized</span></span>](../virtual-machines-windows-sizes-storage.md) | <span data-ttu-id="98faf-172">Seria L</span><span class="sxs-lookup"><span data-stu-id="98faf-172">L series</span></span> | <span data-ttu-id="98faf-173">64</span><span class="sxs-lookup"><span data-stu-id="98faf-173">64</span></span> |
| [<span data-ttu-id="98faf-174">Procesor GPU</span><span class="sxs-lookup"><span data-stu-id="98faf-174">GPU</span></span>](sizes-gpu.md) | <span data-ttu-id="98faf-175">N serii</span><span class="sxs-lookup"><span data-stu-id="98faf-175">N series</span></span> | <span data-ttu-id="98faf-176">48</span><span class="sxs-lookup"><span data-stu-id="98faf-176">48</span></span> |
| [<span data-ttu-id="98faf-177">Wysoka wydajność</span><span class="sxs-lookup"><span data-stu-id="98faf-177">High performance</span></span>](sizes-hpc.md) | <span data-ttu-id="98faf-178">A i serii H</span><span class="sxs-lookup"><span data-stu-id="98faf-178">A and H series</span></span> | <span data-ttu-id="98faf-179">32</span><span class="sxs-lookup"><span data-stu-id="98faf-179">32</span></span> |

## <a name="vm-disk-types"></a><span data-ttu-id="98faf-180">Typy dysków maszyny Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="98faf-180">VM disk types</span></span>

<span data-ttu-id="98faf-181">Platforma Azure oferuje dwa rodzaje dysku.</span><span class="sxs-lookup"><span data-stu-id="98faf-181">Azure provides two types of disk.</span></span>

### <a name="standard-disk"></a><span data-ttu-id="98faf-182">Dysków w warstwie standardowa</span><span class="sxs-lookup"><span data-stu-id="98faf-182">Standard disk</span></span>

<span data-ttu-id="98faf-183">Magazyn Standard Storage bazuje na dyskach twardych (HDD) i stanowi ekonomiczne, chociaż wciąż wydajne rozwiązanie.</span><span class="sxs-lookup"><span data-stu-id="98faf-183">Standard Storage is backed by HDDs, and delivers cost-effective storage while still being performant.</span></span> <span data-ttu-id="98faf-184">Dyski standardowe idealnie nadają się do deweloperów ekonomiczne i testów obciążenia.</span><span class="sxs-lookup"><span data-stu-id="98faf-184">Standard disks are ideal for a cost effective dev and test workload.</span></span>

### <a name="premium-disk"></a><span data-ttu-id="98faf-185">Dysku Premium</span><span class="sxs-lookup"><span data-stu-id="98faf-185">Premium disk</span></span>

<span data-ttu-id="98faf-186">Dyski Premium bazują na dysk SSD dysku wysokiej wydajności i małych opóźnień.</span><span class="sxs-lookup"><span data-stu-id="98faf-186">Premium disks are backed by SSD-based high-performance, low-latency disk.</span></span> <span data-ttu-id="98faf-187">Idealny dla maszyn wirtualnych obciążeniu produkcji.</span><span class="sxs-lookup"><span data-stu-id="98faf-187">Perfect for VMs running production workload.</span></span> <span data-ttu-id="98faf-188">Magazyn w warstwie Premium obsługuje serii DS, DSv2 serii GS-series i FS serii maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="98faf-188">Premium Storage supports DS-series, DSv2-series, GS-series, and FS-series VMs.</span></span> <span data-ttu-id="98faf-189">Dyski w warstwie Premium są dostępne w trzech typów (P10, P20, P30), rozmiar dysku Określa typ dysku.</span><span class="sxs-lookup"><span data-stu-id="98faf-189">Premium disks come in three types (P10, P20, P30), the size of the disk determines the disk type.</span></span> <span data-ttu-id="98faf-190">Podczas wybierania, rozmiar dysku wartość jest zaokrąglana do dalej typu.</span><span class="sxs-lookup"><span data-stu-id="98faf-190">When selecting, a disk size the value is rounded up to the next type.</span></span> <span data-ttu-id="98faf-191">Na przykład jeśli rozmiar dysku jest mniejszy niż 128 GB, typ dysku jest P10.</span><span class="sxs-lookup"><span data-stu-id="98faf-191">For example, if the disk size is less than 128 GB, the disk type is P10.</span></span> <span data-ttu-id="98faf-192">Jeśli rozmiar dysku wynosi 129 GB i 512, rozmiar jest P20.</span><span class="sxs-lookup"><span data-stu-id="98faf-192">If the disk size is between 129 GB and 512 GB, the size is a P20.</span></span> <span data-ttu-id="98faf-193">Niczego ponad 512 GB, rozmiar jest P30.</span><span class="sxs-lookup"><span data-stu-id="98faf-193">Anything over 512 GB, the size is a P30.</span></span>

### <a name="premium-disk-performance"></a><span data-ttu-id="98faf-194">Wydajność dysku Premium</span><span class="sxs-lookup"><span data-stu-id="98faf-194">Premium disk performance</span></span>

|<span data-ttu-id="98faf-195">Typ dysku magazynu w warstwie Premium</span><span class="sxs-lookup"><span data-stu-id="98faf-195">Premium storage disk type</span></span> | <span data-ttu-id="98faf-196">P10</span><span class="sxs-lookup"><span data-stu-id="98faf-196">P10</span></span> | <span data-ttu-id="98faf-197">P20</span><span class="sxs-lookup"><span data-stu-id="98faf-197">P20</span></span> | <span data-ttu-id="98faf-198">P30</span><span class="sxs-lookup"><span data-stu-id="98faf-198">P30</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="98faf-199">Rozmiar dysku (zaokrąglony)</span><span class="sxs-lookup"><span data-stu-id="98faf-199">Disk size (round up)</span></span> | <span data-ttu-id="98faf-200">128 GB</span><span class="sxs-lookup"><span data-stu-id="98faf-200">128 GB</span></span> | <span data-ttu-id="98faf-201">512 GB</span><span class="sxs-lookup"><span data-stu-id="98faf-201">512 GB</span></span> | <span data-ttu-id="98faf-202">1024 GB (1 TB)</span><span class="sxs-lookup"><span data-stu-id="98faf-202">1,024 GB (1 TB)</span></span> |
| <span data-ttu-id="98faf-203">Maksymalna liczba operacji wejścia/wyjścia na sekundę na dysk</span><span class="sxs-lookup"><span data-stu-id="98faf-203">Max IOPS per disk</span></span> | <span data-ttu-id="98faf-204">500</span><span class="sxs-lookup"><span data-stu-id="98faf-204">500</span></span> | <span data-ttu-id="98faf-205">2,300</span><span class="sxs-lookup"><span data-stu-id="98faf-205">2,300</span></span> | <span data-ttu-id="98faf-206">5,000</span><span class="sxs-lookup"><span data-stu-id="98faf-206">5,000</span></span> |
<span data-ttu-id="98faf-207">Przepływność na dysk</span><span class="sxs-lookup"><span data-stu-id="98faf-207">Throughput per disk</span></span> | <span data-ttu-id="98faf-208">100 MB/s</span><span class="sxs-lookup"><span data-stu-id="98faf-208">100 MB/s</span></span> | <span data-ttu-id="98faf-209">150 MB/s</span><span class="sxs-lookup"><span data-stu-id="98faf-209">150 MB/s</span></span> | <span data-ttu-id="98faf-210">200 MB/s</span><span class="sxs-lookup"><span data-stu-id="98faf-210">200 MB/s</span></span> |

<span data-ttu-id="98faf-211">Gdy powyższej tabeli określa maksymalną liczbę IOPS dla każdego dysku, można osiągnąć wyższy poziom wydajności przez stosowanie wielu dysków z danymi.</span><span class="sxs-lookup"><span data-stu-id="98faf-211">While the above table identifies max IOPS per disk, a higher level of performance can be achieved by striping multiple data disks.</span></span> <span data-ttu-id="98faf-212">Na przykład Standard_GS5 maszyny Wirtualnej można osiągnąć maksymalnie 80 000 IOPS.</span><span class="sxs-lookup"><span data-stu-id="98faf-212">For instance, a Standard_GS5 VM can achieve a maximum of 80,000 IOPS.</span></span> <span data-ttu-id="98faf-213">Aby uzyskać szczegółowe informacje o maksymalnej IOPS dla maszyny Wirtualnej, zobacz [rozmiarów maszyn wirtualnych systemu Linux](sizes.md).</span><span class="sxs-lookup"><span data-stu-id="98faf-213">For detailed information on max IOPS per VM, see [Linux VM sizes](sizes.md).</span></span>

## <a name="create-and-attach-disks"></a><span data-ttu-id="98faf-214">Utwórz i Dołącz dysków</span><span class="sxs-lookup"><span data-stu-id="98faf-214">Create and attach disks</span></span>

<span data-ttu-id="98faf-215">Dyski danych można tworzyć i dołączone w czasie tworzenia maszyny Wirtualnej lub do istniejącej maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="98faf-215">Data disks can be created and attached at VM creation time or to an existing VM.</span></span>

### <a name="attach-disk-at-vm-creation"></a><span data-ttu-id="98faf-216">Dołączenie dysku podczas tworzenia maszyny Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="98faf-216">Attach disk at VM creation</span></span>

<span data-ttu-id="98faf-217">Utwórz grupę zasobów za pomocą polecenia [az group create](https://docs.microsoft.com/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="98faf-217">Create a resource group with the [az group create](https://docs.microsoft.com/cli/azure/group#create) command.</span></span> 

```azurecli-interactive 
az group create --name myResourceGroupDisk --location eastus
```

<span data-ttu-id="98faf-218">Utwórz maszynę Wirtualną przy użyciu [tworzenia maszyny wirtualnej az]( /cli/azure/vm#create) polecenia.</span><span class="sxs-lookup"><span data-stu-id="98faf-218">Create a VM using the [az vm create]( /cli/azure/vm#create) command.</span></span> <span data-ttu-id="98faf-219">`--datadisk-sizes-gb` Argument jest używany do określenia, czy dodatkowy dysk należy utworzyć i podłączony do maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="98faf-219">The `--datadisk-sizes-gb` argument is used to specify that an additional disk should be created and attached to the virtual machine.</span></span> <span data-ttu-id="98faf-220">Aby utworzyć i dołączyć więcej niż jeden dysk, użyj rozdzieloną spacjami listę wartości rozmiaru dysku.</span><span class="sxs-lookup"><span data-stu-id="98faf-220">To create and attach more than one disk, use a space-delimited list of disk size values.</span></span> <span data-ttu-id="98faf-221">W poniższym przykładzie maszyna wirtualna zostanie utworzona z dwóch dysków, zarówno 128 GB.</span><span class="sxs-lookup"><span data-stu-id="98faf-221">In the following example, a VM is created with two data disks, both 128 GB.</span></span> <span data-ttu-id="98faf-222">Ponieważ rozmiary dysków wynoszą 128 GB, te dyski obydwa są skonfigurowane jako P10s, które zapewniają maksymalną 500 IOPS dla każdego dysku.</span><span class="sxs-lookup"><span data-stu-id="98faf-222">Because the disk sizes are 128 GB, these disks are both configured as P10s, which provide maximum 500 IOPS per disk.</span></span>

```azurecli-interactive 
az vm create \
  --resource-group myResourceGroupDisk \
  --name myVM \
  --image UbuntuLTS \
  --size Standard_DS2_v2 \
  --data-disk-sizes-gb 128 128 \
  --generate-ssh-keys
```

### <a name="attach-disk-to-existing-vm"></a><span data-ttu-id="98faf-223">Dołączanie dysku do istniejącej maszyny Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="98faf-223">Attach disk to existing VM</span></span>

<span data-ttu-id="98faf-224">Aby utworzyć i dołączyć nowego dysku do istniejącej maszyny wirtualnej, użyj [dołączyć dysku maszyny wirtualnej az](/cli/azure/vm/disk#attach) polecenia.</span><span class="sxs-lookup"><span data-stu-id="98faf-224">To create and attach a new disk to an existing virtual machine, use the [az vm disk attach](/cli/azure/vm/disk#attach) command.</span></span> <span data-ttu-id="98faf-225">Poniższy przykład tworzy dysk premium 128 GB w rozmiarze i dołącza go do maszyny Wirtualnej utworzone w ostatnim kroku.</span><span class="sxs-lookup"><span data-stu-id="98faf-225">The following example creates a premium disk, 128 gigabytes in size, and attaches it to the VM created in the last step.</span></span>

```azurecli-interactive 
az vm disk attach --vm-name myVM --resource-group myResourceGroupDisk --disk myDataDisk --size-gb 128 --sku Premium_LRS --new 
```

## <a name="prepare-data-disks"></a><span data-ttu-id="98faf-226">Przygotowanie dysków z danymi</span><span class="sxs-lookup"><span data-stu-id="98faf-226">Prepare data disks</span></span>

<span data-ttu-id="98faf-227">Po dysk został dołączony do maszyny wirtualnej, musi być skonfigurowana do używania dysku systemu operacyjnego.</span><span class="sxs-lookup"><span data-stu-id="98faf-227">Once a disk has been attached to the virtual machine, the operating system needs to be configured to use the disk.</span></span> <span data-ttu-id="98faf-228">Poniższy przykład pokazuje, jak ręcznie skonfigurować dysk.</span><span class="sxs-lookup"><span data-stu-id="98faf-228">The following example shows how to manually configure a disk.</span></span> <span data-ttu-id="98faf-229">Ten proces można również zautomatyzować, używając inicjowaniem chmury, które są objęte w [nowsze samouczek](./tutorial-automate-vm-deployment.md).</span><span class="sxs-lookup"><span data-stu-id="98faf-229">This process can also be automated using cloud-init, which is covered in a [later tutorial](./tutorial-automate-vm-deployment.md).</span></span>

### <a name="manual-configuration"></a><span data-ttu-id="98faf-230">Konfiguracja ręczna</span><span class="sxs-lookup"><span data-stu-id="98faf-230">Manual configuration</span></span>

<span data-ttu-id="98faf-231">Utwórz połączenie SSH z maszyną wirtualną.</span><span class="sxs-lookup"><span data-stu-id="98faf-231">Create an SSH connection with the virtual machine.</span></span> <span data-ttu-id="98faf-232">Zamień adres IP przykład publiczny adres IP maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="98faf-232">Replace the example IP address with the public IP of the virtual machine.</span></span>

```azurecli-interactive 
ssh 52.174.34.95
```

<span data-ttu-id="98faf-233">Partycji dysku z `fdisk`.</span><span class="sxs-lookup"><span data-stu-id="98faf-233">Partition the disk with `fdisk`.</span></span>

```bash
(echo n; echo p; echo 1; echo ; echo ; echo w) | sudo fdisk /dev/sdc
```

<span data-ttu-id="98faf-234">Zapis systemu plików do partycji przy użyciu `mkfs` polecenia.</span><span class="sxs-lookup"><span data-stu-id="98faf-234">Write a file system to the partition by using the `mkfs` command.</span></span>

```bash
sudo mkfs -t ext4 /dev/sdc1
```

<span data-ttu-id="98faf-235">Zainstaluj nowy dysk, aby była dostępna w systemie operacyjnym.</span><span class="sxs-lookup"><span data-stu-id="98faf-235">Mount the new disk so that it is accessible in the operating system.</span></span>

```bash
sudo mkdir /datadrive && sudo mount /dev/sdc1 /datadrive
```

<span data-ttu-id="98faf-236">Dysk jest teraz dostępna za pośrednictwem *datadrive* punktu instalacji, który można zweryfikować, uruchamiając `df -h` polecenia.</span><span class="sxs-lookup"><span data-stu-id="98faf-236">The disk can now be accessed through the *datadrive* mountpoint, which can be verified by running the `df -h` command.</span></span> 

```bash
df -h
```

<span data-ttu-id="98faf-237">Dane wyjściowe zawierają nowy dysk zainstalowany na */datadrive*.</span><span class="sxs-lookup"><span data-stu-id="98faf-237">The output shows the new drive mounted on */datadrive*.</span></span>

```bash
Filesystem      Size  Used Avail Use% Mounted on
/dev/sda1        30G  1.4G   28G   5% /
/dev/sdb1       6.8G   16M  6.4G   1% /mnt
/dev/sdc1        50G   52M   47G   1% /datadrive
```

<span data-ttu-id="98faf-238">Aby upewnić się, że dysk jest ponownej instalacji po ponownym uruchomieniu, musi zostać dodany do */etc/fstab* pliku.</span><span class="sxs-lookup"><span data-stu-id="98faf-238">To ensure that the drive is remounted after a reboot, it must be added to the */etc/fstab* file.</span></span> <span data-ttu-id="98faf-239">Aby to zrobić, należy uzyskać identyfikator UUID dysku o `blkid` narzędzia.</span><span class="sxs-lookup"><span data-stu-id="98faf-239">To do so, get the UUID of the disk with the `blkid` utility.</span></span>

```bash
sudo -i blkid
```

<span data-ttu-id="98faf-240">Identyfikator UUID dysku, wyświetla dane wyjściowe `/dev/sdc1` w takim przypadku.</span><span class="sxs-lookup"><span data-stu-id="98faf-240">The output displays the UUID of the drive, `/dev/sdc1` in this case.</span></span>

```bash
/dev/sdc1: UUID="33333333-3b3b-3c3c-3d3d-3e3e3e3e3e3e" TYPE="ext4"
```

<span data-ttu-id="98faf-241">Dodaj wiersz podobny do następującego do */etc/fstab* pliku.</span><span class="sxs-lookup"><span data-stu-id="98faf-241">Add a line similar to the following to the */etc/fstab* file.</span></span> <span data-ttu-id="98faf-242">Również należy pamiętać, że zapis bariery można wyłączyć za pomocą *bariery = 0*, ta konfiguracja może poprawić wydajność dysku.</span><span class="sxs-lookup"><span data-stu-id="98faf-242">Also note that write barriers can be disabled using *barrier=0*, this configuration can improve disk performance.</span></span> 

```bash
UUID=33333333-3b3b-3c3c-3d3d-3e3e3e3e3e3e   /datadrive  ext4    defaults,nofail,barrier=0   1  2
```

<span data-ttu-id="98faf-243">Teraz, dysk został skonfigurowany, Zamknij sesję SSH.</span><span class="sxs-lookup"><span data-stu-id="98faf-243">Now that the disk has been configured, close the SSH session.</span></span>

```bash
exit
```

## <a name="resize-vm-disk"></a><span data-ttu-id="98faf-244">Zmiana rozmiaru dysku maszyny Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="98faf-244">Resize VM disk</span></span>

<span data-ttu-id="98faf-245">Po wdrożeniu maszyny Wirtualnej, dysk systemu operacyjnego lub żadnych dysków dołączonych danych można zwiększyć rozmiar.</span><span class="sxs-lookup"><span data-stu-id="98faf-245">Once a VM has been deployed, the operating system disk or any attached data disks can be increased in size.</span></span> <span data-ttu-id="98faf-246">Zwiększenie rozmiaru dysku jest przydatne, gdy wymagające więcej miejsca do magazynowania lub wyższego poziomu wydajności (P10 P20, P30).</span><span class="sxs-lookup"><span data-stu-id="98faf-246">Increasing the size of a disk is beneficial when needing more storage space or a higher level of performance (P10, P20, P30).</span></span> <span data-ttu-id="98faf-247">Zauważ, że dyski nie można zmniejszyć rozmiar.</span><span class="sxs-lookup"><span data-stu-id="98faf-247">Note, disks cannot be decreased in size.</span></span>

<span data-ttu-id="98faf-248">Przed zwiększeniem rozmiaru dysku, wymagany jest identyfikator lub nazwę dysku.</span><span class="sxs-lookup"><span data-stu-id="98faf-248">Before increasing disk size, the Id or name of the disk is needed.</span></span> <span data-ttu-id="98faf-249">Użyj [Lista dysków az](/cli/azure/vm/disk#list) polecenia, aby zwrócić wszystkie dyski w grupie zasobów.</span><span class="sxs-lookup"><span data-stu-id="98faf-249">Use the [az disk list](/cli/azure/vm/disk#list) command to return all disks in a resource group.</span></span> <span data-ttu-id="98faf-250">Zanotuj nazwę dysku, który chcesz zmienić rozmiar.</span><span class="sxs-lookup"><span data-stu-id="98faf-250">Take note of the disk name that you would like to resize.</span></span>

```azurecli-interactive 
az disk list -g myResourceGroupDisk --query '[*].{Name:name,Gb:diskSizeGb,Tier:accountType}' --output table
```

<span data-ttu-id="98faf-251">Maszyna wirtualna musi również być alokację.</span><span class="sxs-lookup"><span data-stu-id="98faf-251">The VM must also be deallocated.</span></span> <span data-ttu-id="98faf-252">Użyj [deallocate wirtualna az]( /cli/azure/vm#deallocate) polecenie, aby zatrzymać i cofnięcia przydzielenia Maszynie wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="98faf-252">Use the [az vm deallocate]( /cli/azure/vm#deallocate) command to stop and deallocate the VM.</span></span>

```azurecli-interactive 
az vm deallocate --resource-group myResourceGroupDisk --name myVM
```

<span data-ttu-id="98faf-253">Użyj [aktualizacja dysku az](/cli/azure/vm/disk#update) polecenia zmiany rozmiaru dysku.</span><span class="sxs-lookup"><span data-stu-id="98faf-253">Use the [az disk update](/cli/azure/vm/disk#update) command to resize the disk.</span></span> <span data-ttu-id="98faf-254">W tym przykładzie zmienia rozmiar dysku o nazwie *myDataDisk* do 1 terabajt.</span><span class="sxs-lookup"><span data-stu-id="98faf-254">This example resizes a disk named *myDataDisk* to 1 terabyte.</span></span>

```azurecli-interactive 
az disk update --name myDataDisk --resource-group myResourceGroupDisk --size-gb 1023
```

<span data-ttu-id="98faf-255">Po ukończeniu operacji zmiany rozmiaru, uruchom maszynę Wirtualną.</span><span class="sxs-lookup"><span data-stu-id="98faf-255">Once the resize operation has completed, start the VM.</span></span>

```azurecli-interactive 
az vm start --resource-group myResourceGroupDisk --name myVM
```

<span data-ttu-id="98faf-256">Jeśli dysk systemu operacyjnego został zmieniony, jest automatycznie rozszerzana partycji.</span><span class="sxs-lookup"><span data-stu-id="98faf-256">If you’ve resized the operating system disk, the partition is automatically be expanded.</span></span> <span data-ttu-id="98faf-257">Jeśli zmieniono dysk z danymi, wszystkie partycje bieżącego musi zostać rozszerzony w systemie operacyjnym maszyny wirtualne.</span><span class="sxs-lookup"><span data-stu-id="98faf-257">If you have resized a data disk, any current partitions need to be expanded in the VMs operating system.</span></span>

## <a name="snapshot-azure-disks"></a><span data-ttu-id="98faf-258">Migawki dysków Azure</span><span class="sxs-lookup"><span data-stu-id="98faf-258">Snapshot Azure disks</span></span>

<span data-ttu-id="98faf-259">Tworzenie migawki dysku tworzy odczytu tylko, w momencie kopii dysku.</span><span class="sxs-lookup"><span data-stu-id="98faf-259">Taking a disk snapshot creates a read only, point-in-time copy of the disk.</span></span> <span data-ttu-id="98faf-260">Migawki maszyny Wirtualnej platformy Azure są przydatne do szybkiego zapisywania stanu maszyny wirtualnej przed wprowadzeniem zmian w konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="98faf-260">Azure VM snapshots are useful for quickly saving the state of a VM before making configuration changes.</span></span> <span data-ttu-id="98faf-261">W przypadku zmiany konfiguracji okazać się niepożądane, można przywrócić stan maszyny Wirtualnej za pomocą migawki.</span><span class="sxs-lookup"><span data-stu-id="98faf-261">In the event the configuration changes prove to be undesired, VM state can be restored using the snapshot.</span></span> <span data-ttu-id="98faf-262">Gdy maszyna wirtualna ma więcej niż jeden dysk, migawki każdego dysku, niezależnie od innych.</span><span class="sxs-lookup"><span data-stu-id="98faf-262">When a VM has more than one disk, a snapshot is taken of each disk independently of the others.</span></span> <span data-ttu-id="98faf-263">Do wykonywania kopii zapasowych spójności aplikacji, należy wziąć pod uwagę zatrzymanie maszyny Wirtualnej przed wykonaniem migawki dysków.</span><span class="sxs-lookup"><span data-stu-id="98faf-263">For taking application consistent backups, consider stopping the VM before taking disk snapshots.</span></span> <span data-ttu-id="98faf-264">Można również użyć [usługi Kopia zapasowa Azure](/azure/backup/), który służy do wykonywania automatycznych kopii zapasowych uruchomionej maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="98faf-264">Alternatively, use the [Azure Backup service](/azure/backup/), which enables you to perform automated backups while the VM is running.</span></span>

### <a name="create-snapshot"></a><span data-ttu-id="98faf-265">Tworzenie migawki</span><span class="sxs-lookup"><span data-stu-id="98faf-265">Create snapshot</span></span>

<span data-ttu-id="98faf-266">Przed utworzeniem migawek dysków maszyny wirtualnej, wymagany jest identyfikator lub nazwę dysku.</span><span class="sxs-lookup"><span data-stu-id="98faf-266">Before creating a virtual machine disk snapshot, the Id or name of the disk is needed.</span></span> <span data-ttu-id="98faf-267">Użyj [az maszyny wirtualnej pokazu](https://docs.microsoft.com/en-us/cli/azure/vm#show) poleceniu, aby uzyskać identyfikator dysku.</span><span class="sxs-lookup"><span data-stu-id="98faf-267">Use the [az vm show](https://docs.microsoft.com/en-us/cli/azure/vm#show) command to return the disk id.</span></span> <span data-ttu-id="98faf-268">W tym przykładzie identyfikator dysku jest przechowywana w zmiennej, dzięki czemu mogą być używane w kolejnym kroku.</span><span class="sxs-lookup"><span data-stu-id="98faf-268">In this example, the disk id is stored in a variable so that it can be used in a later step.</span></span>

```azurecli-interactive 
osdiskid=$(az vm show -g myResourceGroupDisk -n myVM --query "storageProfile.osDisk.managedDisk.id" -o tsv)
```

<span data-ttu-id="98faf-269">Teraz, gdy masz identyfikator dysku maszyny wirtualnej, polecenie tworzy migawkę dysku.</span><span class="sxs-lookup"><span data-stu-id="98faf-269">Now that you have the id of the virtual machine disk, the following command creates a snapshot of the disk.</span></span>

```azurcli
az snapshot create -g myResourceGroupDisk --source "$osdiskid" --name osDisk-backup
```

### <a name="create-disk-from-snapshot"></a><span data-ttu-id="98faf-270">Utwórz dysk z migawki</span><span class="sxs-lookup"><span data-stu-id="98faf-270">Create disk from snapshot</span></span>

<span data-ttu-id="98faf-271">Następnie można przekonwertować tej migawki na dysk, którego można użyć w celu ponownego utworzenia maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="98faf-271">This snapshot can then be converted into a disk, which can be used to recreate the virtual machine.</span></span>

```azurecli-interactive 
az disk create --resource-group myResourceGroupDisk --name mySnapshotDisk --source osDisk-backup
```

### <a name="restore-virtual-machine-from-snapshot"></a><span data-ttu-id="98faf-272">Przywracanie z migawki maszyny wirtualnej</span><span class="sxs-lookup"><span data-stu-id="98faf-272">Restore virtual machine from snapshot</span></span>

<span data-ttu-id="98faf-273">Aby zademonstrować odzyskiwanie maszyny wirtualnej, usuń istniejącą maszynę wirtualną.</span><span class="sxs-lookup"><span data-stu-id="98faf-273">To demonstrate virtual machine recovery, delete the existing virtual machine.</span></span> 

```azurecli-interactive 
az vm delete --resource-group myResourceGroupDisk --name myVM
```

<span data-ttu-id="98faf-274">Utwórz nową maszynę wirtualną na podstawie dysku migawki.</span><span class="sxs-lookup"><span data-stu-id="98faf-274">Create a new virtual machine from the snapshot disk.</span></span>

```azurecli-interactive 
az vm create --resource-group myResourceGroupDisk --name myVM --attach-os-disk mySnapshotDisk --os-type linux
```

### <a name="reattach-data-disk"></a><span data-ttu-id="98faf-275">Podłącz dysk danych</span><span class="sxs-lookup"><span data-stu-id="98faf-275">Reattach data disk</span></span>

<span data-ttu-id="98faf-276">Wszystkie dyski danych muszą zostać ponownie nałożona do maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="98faf-276">All data disks need to be reattached to the virtual machine.</span></span>

<span data-ttu-id="98faf-277">Najpierw znaleźć, używając nazwy dysku danych [Lista dysków az](https://docs.microsoft.com/cli/azure/disk#list) polecenia.</span><span class="sxs-lookup"><span data-stu-id="98faf-277">First find the data disk name using the [az disk list](https://docs.microsoft.com/cli/azure/disk#list) command.</span></span> <span data-ttu-id="98faf-278">W tym przykładzie umieszcza nazwę dysku w zmiennej o nazwie *datadisk*, która jest używana w następnym kroku.</span><span class="sxs-lookup"><span data-stu-id="98faf-278">This example places the name of the disk in a variable named *datadisk*, which is used in the next step.</span></span>

```azurecli-interactive 
datadisk=$(az disk list -g myResourceGroupDisk --query "[?contains(name,'myVM')].[name]" -o tsv)
```

<span data-ttu-id="98faf-279">Użyj [dołączyć dysku maszyny wirtualnej az](https://docs.microsoft.com/cli/azure/vm/disk#attach) polecenie, aby podłączyć dysk.</span><span class="sxs-lookup"><span data-stu-id="98faf-279">Use the [az vm disk attach](https://docs.microsoft.com/cli/azure/vm/disk#attach) command to attach the disk.</span></span>

```azurecli-interactive 
az vm disk attach –g myResourceGroupDisk –-vm-name myVM –-disk $datadisk
```

## <a name="next-steps"></a><span data-ttu-id="98faf-280">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="98faf-280">Next steps</span></span>

<span data-ttu-id="98faf-281">W tym samouczku przedstawiono tematy dysków maszyny Wirtualnej takich jak:</span><span class="sxs-lookup"><span data-stu-id="98faf-281">In this tutorial, you learned about VM disks topics such as:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="98faf-282">Dyski systemu operacyjnego i tymczasowego</span><span class="sxs-lookup"><span data-stu-id="98faf-282">OS disks and temporary disks</span></span>
> * <span data-ttu-id="98faf-283">Dyski danych</span><span class="sxs-lookup"><span data-stu-id="98faf-283">Data disks</span></span>
> * <span data-ttu-id="98faf-284">Standard i dysków w warstwie Premium</span><span class="sxs-lookup"><span data-stu-id="98faf-284">Standard and Premium disks</span></span>
> * <span data-ttu-id="98faf-285">Wydajność dysku</span><span class="sxs-lookup"><span data-stu-id="98faf-285">Disk performance</span></span>
> * <span data-ttu-id="98faf-286">Dołączanie i przygotowywania dysków z danymi</span><span class="sxs-lookup"><span data-stu-id="98faf-286">Attaching and preparing data disks</span></span>
> * <span data-ttu-id="98faf-287">Zmiana rozmiaru dysków</span><span class="sxs-lookup"><span data-stu-id="98faf-287">Resizing disks</span></span>
> * <span data-ttu-id="98faf-288">Migawki dysków</span><span class="sxs-lookup"><span data-stu-id="98faf-288">Disk snapshots</span></span>

<span data-ttu-id="98faf-289">Przejdź do następnego w samouczku więcej informacji na temat automatyzacji konfiguracji maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="98faf-289">Advance to the next tutorial to learn about automating VM configuration.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="98faf-290">Automatyzowanie konfiguracji maszyny wirtualnej</span><span class="sxs-lookup"><span data-stu-id="98faf-290">Automate VM configuration</span></span>](./tutorial-automate-vm-deployment.md)
