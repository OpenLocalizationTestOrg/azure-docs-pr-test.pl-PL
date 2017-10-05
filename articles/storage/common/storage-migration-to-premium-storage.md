---
title: Migrowanie maszyn wirtualnych do magazynu Azure Premium | Dokumentacja firmy Microsoft
description: "Migrowanie istniejących maszyn wirtualnych do usługi Azure Premium Storage. Magazyn w warstwie Premium oferuje obsługę dysków o wysokiej wydajności i małych opóźnieniach/O wykonujących obciążeń uruchomionych na maszynach wirtualnych platformy Azure."
services: storage
documentationcenter: na
author: yuemlu
manager: tadb
editor: tysonn
ms.assetid: 272250b3-fd4e-41d2-8e34-fd8cc341ec87
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/27/2017
ms.author: yuemlu
ms.openlocfilehash: ca893f87b155a92c457e3bf6d9d39aaf86bf5fb3
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
# <a name="migrating-to-azure-premium-storage-unmanaged-disks"></a><span data-ttu-id="64238-104">Migrowanie do magazynu Azure Premium (niezarządzany dysków)</span><span class="sxs-lookup"><span data-stu-id="64238-104">Migrating to Azure Premium Storage (Unmanaged Disks)</span></span>

> [!NOTE]
> <span data-ttu-id="64238-105">W tym artykule omówiono sposób migracji maszyny Wirtualnej, który używa niezarządzane standardowych dysków do maszyny Wirtualnej używającej dysków premium niezarządzane.</span><span class="sxs-lookup"><span data-stu-id="64238-105">This article discusses how to migrate a VM that uses unmanaged standard disks to a VM that uses unmanaged premium disks.</span></span> <span data-ttu-id="64238-106">Zaleca się używać dysków zarządzanych Azure dla maszyn wirtualnych i przekonwertować poprzedniej dysków niezarządzanych do zarządzanych dysków.</span><span class="sxs-lookup"><span data-stu-id="64238-106">We recommend that you use Azure Managed Disks for new VMs, and that you convert your previous unmanaged disks to managed disks.</span></span> <span data-ttu-id="64238-107">Zarządzane dojścia dysków podstawowych kont magazynu, nie trzeba.</span><span class="sxs-lookup"><span data-stu-id="64238-107">Managed Disks handle the underlying storage accounts so you don't have to.</span></span> <span data-ttu-id="64238-108">Aby uzyskać więcej informacji, zobacz nasze [omówienie dysków zarządzanych](../../virtual-machines/windows/managed-disks-overview.md).</span><span class="sxs-lookup"><span data-stu-id="64238-108">For more information, please see our [Managed Disks Overview](../../virtual-machines/windows/managed-disks-overview.md).</span></span>
>

<span data-ttu-id="64238-109">Usługa Azure Premium Storage oferuje obsługę wysokiej wydajności i małych opóźnieniach dysku dla maszyn wirtualnych uruchomionych/O wykonujących obciążeń.</span><span class="sxs-lookup"><span data-stu-id="64238-109">Azure Premium Storage delivers high-performance, low-latency disk support for virtual machines running I/O-intensive workloads.</span></span> <span data-ttu-id="64238-110">Przeprowadź migrację aplikacji dysków maszyny Wirtualnej do usługi Azure Premium Storage może zająć wykorzystują szybkości i wydajności tych dysków.</span><span class="sxs-lookup"><span data-stu-id="64238-110">You can take advantage of the speed and performance of these disks by migrating your application's VM disks to Azure Premium Storage.</span></span>

<span data-ttu-id="64238-111">Przeznaczenie tego przewodnika jest pomoc nowych użytkowników usługi Azure Premium Storage lepsze przygotowanie do płynne przejście z bieżącego systemu do magazynu w warstwie Premium.</span><span class="sxs-lookup"><span data-stu-id="64238-111">The purpose of this guide is to help new users of Azure Premium Storage better prepare to make a smooth transition from their current system to Premium Storage.</span></span> <span data-ttu-id="64238-112">Przewodnik dotyczy trzy najważniejsze składniki w tym procesie:</span><span class="sxs-lookup"><span data-stu-id="64238-112">The guide addresses three of the key components in this process:</span></span>

* [<span data-ttu-id="64238-113">Planowanie migracji do magazyn w warstwie Premium</span><span class="sxs-lookup"><span data-stu-id="64238-113">Plan for the Migration to Premium Storage</span></span>](#plan-the-migration-to-premium-storage)
* [<span data-ttu-id="64238-114">Przygotowanie i skopiuj wirtualne dyski twarde (VHD) na magazyn w warstwie Premium</span><span class="sxs-lookup"><span data-stu-id="64238-114">Prepare and Copy Virtual Hard Disks (VHDs) to Premium Storage</span></span>](#prepare-and-copy-virtual-hard-disks-VHDs-to-premium-storage)
* [<span data-ttu-id="64238-115">Utwórz maszynę wirtualną platformy Azure przy użyciu magazyn w warstwie Premium</span><span class="sxs-lookup"><span data-stu-id="64238-115">Create Azure Virtual Machine using Premium Storage</span></span>](#create-azure-virtual-machine-using-premium-storage)

<span data-ttu-id="64238-116">Można dokonać migracji maszyn wirtualnych z innych platform do magazynu Azure Premium lub migracji istniejących maszyn wirtualnych platformy Azure z magazynu w warstwie standardowa do magazyn w warstwie Premium.</span><span class="sxs-lookup"><span data-stu-id="64238-116">You can either migrate VMs from other platforms to Azure Premium Storage or migrate existing Azure VMs from Standard Storage to Premium Storage.</span></span> <span data-ttu-id="64238-117">W tym przewodniku opisano kroki dla obu dwa scenariusze.</span><span class="sxs-lookup"><span data-stu-id="64238-117">This guide covers steps for both two scenarios.</span></span> <span data-ttu-id="64238-118">Wykonaj kroki określone w odpowiedniej sekcji w zależności od danego scenariusza.</span><span class="sxs-lookup"><span data-stu-id="64238-118">Follow the steps specified in the relevant section depending on your scenario.</span></span>

> [!NOTE]
> <span data-ttu-id="64238-119">Omówienie funkcji i cenowych Premium magazynu w warstwie Premium Storage można znaleźć: [magazynu o wysokiej wydajności dla obciążeń maszyny wirtualnej Azure](storage-premium-storage.md).</span><span class="sxs-lookup"><span data-stu-id="64238-119">You can find a feature overview and pricing of Premium Storage in Premium Storage: [High-Performance Storage for Azure Virtual Machine Workloads](storage-premium-storage.md).</span></span> <span data-ttu-id="64238-120">Zaleca się migrowanie dyskami maszyny wirtualnej wymagające wysoką wartość IOPS dla usługi Azure Premium Storage, aby uzyskać najlepszą wydajność aplikacji.</span><span class="sxs-lookup"><span data-stu-id="64238-120">We recommend migrating any virtual machine disk requiring high IOPS to Azure Premium Storage for the best performance for your application.</span></span> <span data-ttu-id="64238-121">Jeśli dysk nie wymaga wysokiej IOPS, przechowując go w Standard Storage, która przechowuje dane dysku maszyny wirtualnej na stacje dysków twardych (HDD) zamiast dysków SSD można ograniczyć koszty.</span><span class="sxs-lookup"><span data-stu-id="64238-121">If your disk does not require high IOPS, you can limit costs by maintaining it in Standard Storage, which stores virtual machine disk data on Hard Disk Drives (HDDs) instead of SSDs.</span></span>
>

<span data-ttu-id="64238-122">Kończenie procesu migracji, w całości może wymagać dodatkowych akcji przed i po zgodnie z krokami opisanymi w tym przewodniku.</span><span class="sxs-lookup"><span data-stu-id="64238-122">Completing the migration process in its entirety may require additional actions both before and after the steps provided in this guide.</span></span> <span data-ttu-id="64238-123">Przykładami konfigurowania sieci wirtualnych lub punktów końcowych lub zmiany kodu samej aplikacji, które mogą wymagać przestój w aplikacji.</span><span class="sxs-lookup"><span data-stu-id="64238-123">Examples include configuring virtual networks or endpoints or making code changes within the application itself which may require some downtime in your application.</span></span> <span data-ttu-id="64238-124">Te akcje są unikatowe dla każdej aplikacji i należy je ukończyć wraz z krokami opisanymi w tym przewodniku, aby wprowadzić pełną przejścia magazyn w warstwie Premium jako bezproblemowe, jak to możliwe.</span><span class="sxs-lookup"><span data-stu-id="64238-124">These actions are unique to each application, and you should complete them along with the steps provided in this guide to make the full transition to Premium Storage as seamless as possible.</span></span>

## <span data-ttu-id="64238-125"><a name="plan-the-migration-to-premium-storage"></a>Planowanie migracji do magazyn w warstwie Premium</span><span class="sxs-lookup"><span data-stu-id="64238-125"><a name="plan-the-migration-to-premium-storage"></a>Plan for the migration to Premium Storage</span></span>
<span data-ttu-id="64238-126">W tej sekcji gwarantuje, że są gotowe do wykonania tych kroków migracji, w tym artykule i ułatwia podjęcie najlepszych decyzji w typach maszyny Wirtualnej i dysku.</span><span class="sxs-lookup"><span data-stu-id="64238-126">This section ensures that you are ready to follow the migration steps in this article, and helps you to make the best decision on VM and Disk types.</span></span>

### <a name="prerequisites"></a><span data-ttu-id="64238-127">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="64238-127">Prerequisites</span></span>
* <span data-ttu-id="64238-128">Konieczne będzie subskrypcji platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="64238-128">You will need an Azure subscription.</span></span> <span data-ttu-id="64238-129">Jeśli nie masz, możesz utworzyć jeden miesiąc [bezpłatnej wersji próbnej](https://azure.microsoft.com/pricing/free-trial/) subskrypcji lub odwiedź stronę [cennik usługi Azure](https://azure.microsoft.com/pricing/) wyświetlić więcej opcji.</span><span class="sxs-lookup"><span data-stu-id="64238-129">If you don't have one, you can create a one-month [free trial](https://azure.microsoft.com/pricing/free-trial/) subscription or visit [Azure Pricing](https://azure.microsoft.com/pricing/) for more options.</span></span>
* <span data-ttu-id="64238-130">Do wykonania polecenia cmdlet programu PowerShell, konieczne będzie modułu Microsoft Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="64238-130">To execute PowerShell cmdlets, you will need the Microsoft Azure PowerShell module.</span></span> <span data-ttu-id="64238-131">Aby uzyskać informacje o punkcie instalacji oraz instrukcje dotyczące instalacji, zobacz [How to install and configure Azure PowerShell](/powershell/azure/overview) (Jak zainstalować i skonfigurować program Azure PowerShell).</span><span class="sxs-lookup"><span data-stu-id="64238-131">See [How to install and configure Azure PowerShell](/powershell/azure/overview) for the install point and installation instructions.</span></span>
* <span data-ttu-id="64238-132">Jeśli planujesz używać usługi Azure maszyn wirtualnych uruchomionych na magazyn w warstwie Premium, należy użyć maszyn wirtualnych obsługujących magazyn w warstwie Premium.</span><span class="sxs-lookup"><span data-stu-id="64238-132">When you plan to use Azure VMs running on Premium Storage, you need to use the Premium Storage capable VMs.</span></span> <span data-ttu-id="64238-133">Dyski w wersjach Standard i Premium Storage służy magazyn w warstwie Premium obsługuje maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="64238-133">You can use both Standard and Premium Storage disks with Premium Storage capable VMs.</span></span> <span data-ttu-id="64238-134">Dyski magazynu Premium będą dostępne z większą liczbę typów maszyny Wirtualnej w przyszłości.</span><span class="sxs-lookup"><span data-stu-id="64238-134">Premium storage disks will be available with more VM types in the future.</span></span> <span data-ttu-id="64238-135">Aby uzyskać więcej informacji na wszystkich dostępnych typów dysku maszyny Wirtualnej platformy Azure i rozmiarów, zobacz [rozmiary maszyn wirtualnych](../../virtual-machines/windows/sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) i [rozmiary dla usług w chmurze](../../cloud-services/cloud-services-sizes-specs.md).</span><span class="sxs-lookup"><span data-stu-id="64238-135">For more information on all available Azure VM disk types and sizes, see [Sizes for virtual machines](../../virtual-machines/windows/sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) and [Sizes for Cloud Services](../../cloud-services/cloud-services-sizes-specs.md).</span></span>

### <a name="considerations"></a><span data-ttu-id="64238-136">Zagadnienia do rozważenia</span><span class="sxs-lookup"><span data-stu-id="64238-136">Considerations</span></span>
<span data-ttu-id="64238-137">Maszyny Wirtualnej platformy Azure obsługuje dołączanie kilka dysków Premium Storage, dzięki czemu aplikacje mogą mieć maksymalnie 256 TB pamięci masowej dla maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="64238-137">An Azure VM supports attaching several Premium Storage disks so that your applications can have up to 256 TB of storage per VM.</span></span> <span data-ttu-id="64238-138">Z magazyn w warstwie Premium aplikacje można osiągnąć 80 000 IOPS (operacje wejścia/wyjścia na sekundę) dla maszyny Wirtualnej i 2000 MB na drugi przepływność dysku dla maszyny Wirtualnej z bardzo małych opóźnień operacji odczytu.</span><span class="sxs-lookup"><span data-stu-id="64238-138">With Premium Storage, your applications can achieve 80,000 IOPS (input/output operations per second) per VM and 2000 MB per second disk throughput per VM with extremely low latencies for read operations.</span></span> <span data-ttu-id="64238-139">Dostępne są opcje wiele maszyn wirtualnych i dysków.</span><span class="sxs-lookup"><span data-stu-id="64238-139">You have options in a variety of VMs and Disks.</span></span> <span data-ttu-id="64238-140">W tej sekcji jest ułatwiają znajdowanie opcję najlepiej pasującą do obciążenia.</span><span class="sxs-lookup"><span data-stu-id="64238-140">This section is to help you to find an option that best suits your workload.</span></span>

#### <a name="vm-sizes"></a><span data-ttu-id="64238-141">Rozmiary maszyn wirtualnych</span><span class="sxs-lookup"><span data-stu-id="64238-141">VM sizes</span></span>
<span data-ttu-id="64238-142">Specyfikacje rozmiaru maszyny Wirtualnej platformy Azure są wymienione w [rozmiary maszyn wirtualnych](../../virtual-machines/windows/sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="64238-142">The Azure VM size specifications are listed in [Sizes for virtual machines](../../virtual-machines/windows/sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> <span data-ttu-id="64238-143">Przejrzyj charakterystyki wydajności maszyn wirtualnych, które pracy z magazyn w warstwie Premium i wybierz najbardziej odpowiedni rozmiar maszyny Wirtualnej, który najlepiej odpowiada obciążenie.</span><span class="sxs-lookup"><span data-stu-id="64238-143">Review the performance characteristics of virtual machines that work with Premium Storage and choose the most appropriate VM size that best suits your workload.</span></span> <span data-ttu-id="64238-144">Należy upewnić się, że wystarczającą przepustowość dostępne na maszynie Wirtualnej do kierowania ruchu dysku.</span><span class="sxs-lookup"><span data-stu-id="64238-144">Make sure that there is sufficient bandwidth available on your VM to drive the disk traffic.</span></span>

#### <a name="disk-sizes"></a><span data-ttu-id="64238-145">Rozmiary dysków</span><span class="sxs-lookup"><span data-stu-id="64238-145">Disk sizes</span></span>
<span data-ttu-id="64238-146">Istnieje pięć typów dysków, które mogą być używane z maszyny Wirtualnej, a każdy ma określonych IOPs i przepływność limity.</span><span class="sxs-lookup"><span data-stu-id="64238-146">There are five types of disks that can be used with your VM and each has specific IOPs and throughput limits.</span></span> <span data-ttu-id="64238-147">Wziąć pod uwagę następujące limity gdy wybieranie typu dysku do maszyny Wirtualnej na podstawie potrzeb aplikacji pod względem wydajności, wydajności, skalowalności i ładuje godzinami szczytu.</span><span class="sxs-lookup"><span data-stu-id="64238-147">Take into consideration these limits when choosing the disk type for your VM based on the needs of your application in terms of capacity, performance, scalability, and peak loads.</span></span>

| <span data-ttu-id="64238-148">Typ dysków Premium</span><span class="sxs-lookup"><span data-stu-id="64238-148">Premium Disks Type</span></span>  | <span data-ttu-id="64238-149">P10</span><span class="sxs-lookup"><span data-stu-id="64238-149">P10</span></span>   | <span data-ttu-id="64238-150">P20</span><span class="sxs-lookup"><span data-stu-id="64238-150">P20</span></span>   | <span data-ttu-id="64238-151">P30</span><span class="sxs-lookup"><span data-stu-id="64238-151">P30</span></span>            | <span data-ttu-id="64238-152">P40</span><span class="sxs-lookup"><span data-stu-id="64238-152">P40</span></span>            | <span data-ttu-id="64238-153">P50</span><span class="sxs-lookup"><span data-stu-id="64238-153">P50</span></span>            | 
|:-------------------:|:-----:|:-----:|:--------------:|:--------------:|:--------------:|
| <span data-ttu-id="64238-154">Rozmiar dysku</span><span class="sxs-lookup"><span data-stu-id="64238-154">Disk size</span></span>           | <span data-ttu-id="64238-155">128 GB</span><span class="sxs-lookup"><span data-stu-id="64238-155">128 GB</span></span>| <span data-ttu-id="64238-156">512 GB</span><span class="sxs-lookup"><span data-stu-id="64238-156">512 GB</span></span>| <span data-ttu-id="64238-157">1024 GB (1 TB)</span><span class="sxs-lookup"><span data-stu-id="64238-157">1024 GB (1 TB)</span></span> | <span data-ttu-id="64238-158">2048 GB (2 TB)</span><span class="sxs-lookup"><span data-stu-id="64238-158">2048 GB (2 TB)</span></span> | <span data-ttu-id="64238-159">4095 GB (4 TB)</span><span class="sxs-lookup"><span data-stu-id="64238-159">4095 GB (4 TB)</span></span> | 
| <span data-ttu-id="64238-160">Liczba operacji wejścia/wyjścia na sekundę na dysk</span><span class="sxs-lookup"><span data-stu-id="64238-160">IOPS per disk</span></span>       | <span data-ttu-id="64238-161">500</span><span class="sxs-lookup"><span data-stu-id="64238-161">500</span></span>   | <span data-ttu-id="64238-162">2300</span><span class="sxs-lookup"><span data-stu-id="64238-162">2300</span></span>  | <span data-ttu-id="64238-163">5000</span><span class="sxs-lookup"><span data-stu-id="64238-163">5000</span></span>           | <span data-ttu-id="64238-164">7500</span><span class="sxs-lookup"><span data-stu-id="64238-164">7500</span></span>           | <span data-ttu-id="64238-165">7500</span><span class="sxs-lookup"><span data-stu-id="64238-165">7500</span></span>           | 
| <span data-ttu-id="64238-166">Przepływność na dysk</span><span class="sxs-lookup"><span data-stu-id="64238-166">Throughput per disk</span></span> | <span data-ttu-id="64238-167">100 MB na sekundę</span><span class="sxs-lookup"><span data-stu-id="64238-167">100 MB per second</span></span> | <span data-ttu-id="64238-168">150 MB na sekundę</span><span class="sxs-lookup"><span data-stu-id="64238-168">150 MB per second</span></span> | <span data-ttu-id="64238-169">200 MB / s</span><span class="sxs-lookup"><span data-stu-id="64238-169">200 MB per second</span></span> | <span data-ttu-id="64238-170">250 MB na sekundę</span><span class="sxs-lookup"><span data-stu-id="64238-170">250 MB per second</span></span> | <span data-ttu-id="64238-171">250 MB na sekundę</span><span class="sxs-lookup"><span data-stu-id="64238-171">250 MB per second</span></span> |

<span data-ttu-id="64238-172">W zależności od obciążenia należy sprawdzić, czy dyski dodatkowe dane są niezbędne dla maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="64238-172">Depending on your workload, determine if additional data disks are necessary for your VM.</span></span> <span data-ttu-id="64238-173">Możesz dołączyć kilka dysków danych trwałych do maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="64238-173">You can attach several persistent data disks to your VM.</span></span> <span data-ttu-id="64238-174">W razie potrzeby można paskowych na dyskach w celu zwiększenia pojemności i wydajności woluminu.</span><span class="sxs-lookup"><span data-stu-id="64238-174">If needed, you can stripe across the disks to increase the capacity and performance of the volume.</span></span> <span data-ttu-id="64238-175">(Zobacz, co rozkładanie [tutaj](storage-premium-storage-performance.md#disk-striping).) Jeśli paskowych magazyn w warstwie Premium dysków danych za pomocą [miejsca do magazynowania][4], należy ją skonfigurować z jedną kolumną dla każdego dysku, który jest używany.</span><span class="sxs-lookup"><span data-stu-id="64238-175">(See what is Disk Striping [here](storage-premium-storage-performance.md#disk-striping).) If you stripe Premium Storage data disks using [Storage Spaces][4], you should configure it with one column for each disk that is used.</span></span> <span data-ttu-id="64238-176">W przeciwnym razie ogólną wydajność woluminów rozłożonych może być niższa niż oczekiwano z powodu nierówna Dystrybucja ruchu na dyskach.</span><span class="sxs-lookup"><span data-stu-id="64238-176">Otherwise, the overall performance of the striped volume may be lower than expected due to uneven distribution of traffic across the disks.</span></span> <span data-ttu-id="64238-177">W przypadku maszyn wirtualnych systemu Linux można użyć *mdadm* narzędzie w celu osiągnięcia takie same.</span><span class="sxs-lookup"><span data-stu-id="64238-177">For Linux VMs you can use the *mdadm* utility to achieve the same.</span></span> <span data-ttu-id="64238-178">Zobacz artykuł [skonfigurować RAID oprogramowania w systemie Linux](../../virtual-machines/linux/configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) szczegółowe informacje.</span><span class="sxs-lookup"><span data-stu-id="64238-178">See article [Configure Software RAID on Linux](../../virtual-machines/linux/configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) for details.</span></span>

#### <a name="storage-account-scalability-targets"></a><span data-ttu-id="64238-179">Wartości docelowe skalowalności konta magazynu</span><span class="sxs-lookup"><span data-stu-id="64238-179">Storage account scalability targets</span></span>
<span data-ttu-id="64238-180">Konta Premium magazynu ma następujące wartości docelowe skalowalności oprócz [cele dotyczące wydajności i skalowalności magazynu Azure](storage-scalability-targets.md).</span><span class="sxs-lookup"><span data-stu-id="64238-180">Premium Storage accounts have the following scalability targets in addition to the [Azure Storage Scalability and Performance Targets](storage-scalability-targets.md).</span></span> <span data-ttu-id="64238-181">Jeśli wymagań aplikacji może przekraczać wartości docelowe skalowalności konta magazynu pojedynczego, skompilować aplikację do korzystania z wielu kont magazynu i partycji danych przez tych kont magazynu.</span><span class="sxs-lookup"><span data-stu-id="64238-181">If your application requirements exceed the scalability targets of a single storage account, build your application to use multiple storage accounts, and partition your data across those storage accounts.</span></span>

| <span data-ttu-id="64238-182">Konto łączna pojemność</span><span class="sxs-lookup"><span data-stu-id="64238-182">Total Account Capacity</span></span> | <span data-ttu-id="64238-183">Przepustowość konto magazyn lokalnie nadmiarowy</span><span class="sxs-lookup"><span data-stu-id="64238-183">Total Bandwidth for a Locally Redundant Storage Account</span></span> |
|:--- |:--- |
| <span data-ttu-id="64238-184">Pojemność dysku: 35TB</span><span class="sxs-lookup"><span data-stu-id="64238-184">Disk capacity: 35TB</span></span><br /><span data-ttu-id="64238-185">Migawki pojemności: 10 TB</span><span class="sxs-lookup"><span data-stu-id="64238-185">Snapshot capacity: 10 TB</span></span> |<span data-ttu-id="64238-186">Maksymalnie 50 GB na sekundę dla ruchu przychodzącego i wychodzącego</span><span class="sxs-lookup"><span data-stu-id="64238-186">Up to 50 gigabits per second for Inbound + Outbound</span></span> |

<span data-ttu-id="64238-187">Aby uzyskać więcej informacji dotyczących specyfikacji magazyn w warstwie Premium, zapoznaj się z [skalowalność i cele wydajności przy użyciu magazyn w warstwie Premium](storage-premium-storage.md#scalability-and-performance-targets).</span><span class="sxs-lookup"><span data-stu-id="64238-187">For the more information on Premium Storage specifications, check out [Scalability and Performance Targets when using Premium Storage](storage-premium-storage.md#scalability-and-performance-targets).</span></span>

#### <a name="disk-caching-policy"></a><span data-ttu-id="64238-188">Dyskowej pamięci podręcznej zasad</span><span class="sxs-lookup"><span data-stu-id="64238-188">Disk caching policy</span></span>
<span data-ttu-id="64238-189">Domyślnie jest dyskowej pamięci podręcznej zasad *tylko do odczytu* dla wszystkich danych dysków Premium i *odczytu i zapisu* dla dysku systemu operacyjnego Premium dołączony do maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="64238-189">By default, disk caching policy is *Read-Only* for all the Premium data disks, and *Read-Write* for the Premium operating system disk attached to the VM.</span></span> <span data-ttu-id="64238-190">To ustawienie konfiguracji jest zalecane w celu osiągnięcia optymalnej wydajności dla aplikacji systemu IOs.</span><span class="sxs-lookup"><span data-stu-id="64238-190">This configuration setting is recommended to achieve the optimal performance for your application's IOs.</span></span> <span data-ttu-id="64238-191">W przypadku dysków ciężki zapisu lub w trybie tylko do zapisu danych (takich jak pliki dziennika programu SQL Server) Wyłącz buforowanie dysku, dzięki czemu można osiągnąć lepszą wydajność aplikacji.</span><span class="sxs-lookup"><span data-stu-id="64238-191">For write-heavy or write-only data disks (such as SQL Server log files), disable disk caching so that you can achieve better application performance.</span></span> <span data-ttu-id="64238-192">Ustawienia pamięci podręcznej dla istniejących dysków danych można zaktualizować przy użyciu [Azure Portal](https://portal.azure.com) lub *- HostCaching* parametr *AzureDataDisk zestaw* polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="64238-192">The cache settings for existing data disks can be updated using [Azure Portal](https://portal.azure.com) or the *-HostCaching* parameter of the *Set-AzureDataDisk* cmdlet.</span></span>

#### <a name="location"></a><span data-ttu-id="64238-193">Lokalizacja</span><span class="sxs-lookup"><span data-stu-id="64238-193">Location</span></span>
<span data-ttu-id="64238-194">Wybierz lokalizację, gdzie dostępna jest usługa Azure Premium Storage.</span><span class="sxs-lookup"><span data-stu-id="64238-194">Pick a location where Azure Premium Storage is available.</span></span> <span data-ttu-id="64238-195">Zobacz [regionów platformy Azure](https://azure.microsoft.com/regions/#services) aktualne informacje o dostępnych lokalizacji.</span><span class="sxs-lookup"><span data-stu-id="64238-195">See [Azure Services by Region](https://azure.microsoft.com/regions/#services) for up-to-date information on available locations.</span></span> <span data-ttu-id="64238-196">Maszyny wirtualne znajdujące się w tym samym regionie co konto magazynu, że magazynów dysków dla maszyny Wirtualnej zapewni znacznie lepszą wydajność niż jeśli znajdują się w oddzielnych regionach.</span><span class="sxs-lookup"><span data-stu-id="64238-196">VMs located in the same region as the Storage account that stores the disks for the VM will give much better performance than if they are in separate regions.</span></span>

#### <a name="other-azure-vm-configuration-settings"></a><span data-ttu-id="64238-197">Inne ustawienia konfiguracji maszyny Wirtualnej Azure</span><span class="sxs-lookup"><span data-stu-id="64238-197">Other Azure VM configuration settings</span></span>
<span data-ttu-id="64238-198">Podczas tworzenia maszyny Wirtualnej platformy Azure, użytkownik jest proszony o Konfigurowanie niektórych ustawień maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="64238-198">When creating an Azure VM, you will be asked to configure certain VM settings.</span></span> <span data-ttu-id="64238-199">Należy pamiętać, że w ustaleniu ustawień kilka przez czas ich istnienia maszyny wirtualnej, podczas gdy można zmodyfikować lub dodać inne później.</span><span class="sxs-lookup"><span data-stu-id="64238-199">Remember, few settings are fixed for the lifetime of the VM, while you can modify or add others later.</span></span> <span data-ttu-id="64238-200">Przejrzyj te ustawienia konfiguracji maszyny Wirtualnej platformy Azure i upewnij się, że te są skonfigurowane odpowiednio dostosować do swoich potrzeb obciążenia.</span><span class="sxs-lookup"><span data-stu-id="64238-200">Review these Azure VM configuration settings and make sure that these are configured appropriately to match your workload requirements.</span></span>

### <a name="optimization"></a><span data-ttu-id="64238-201">Optymalizacja</span><span class="sxs-lookup"><span data-stu-id="64238-201">Optimization</span></span>
<span data-ttu-id="64238-202">[Usługa Azure Premium Storage: Projekt o wysokiej wydajności](storage-premium-storage-performance.md) zawiera wskazówki dotyczące tworzenia aplikacji wysokiej wydajności za pomocą usługi Azure Premium Storage.</span><span class="sxs-lookup"><span data-stu-id="64238-202">[Azure Premium Storage: Design for High Performance](storage-premium-storage-performance.md) provides guidelines for building high-performance applications using Azure Premium Storage.</span></span> <span data-ttu-id="64238-203">Można użyć wskazówki łączyć się z najlepszymi rozwiązaniami wydajności mające zastosowanie do technologii używanych przez aplikację.</span><span class="sxs-lookup"><span data-stu-id="64238-203">You can follow the guidelines combined with performance best practices applicable to technologies used by your application.</span></span>

## <span data-ttu-id="64238-204"><a name="prepare-and-copy-virtual-hard-disks-VHDs-to-premium-storage"></a>Przygotowanie i skopiuj wirtualne dyski twarde (VHD) na magazyn w warstwie Premium</span><span class="sxs-lookup"><span data-stu-id="64238-204"><a name="prepare-and-copy-virtual-hard-disks-VHDs-to-premium-storage"></a>Prepare and copy virtual hard disks (VHDs) to Premium Storage</span></span>
<span data-ttu-id="64238-205">Poniższa sekcja zawiera wskazówki dotyczące przygotowania wirtualne dyski twarde z maszyny Wirtualnej i kopiowania wirtualnych dysków twardych do magazynu Azure.</span><span class="sxs-lookup"><span data-stu-id="64238-205">The following section provides guidelines for preparing VHDs from your VM and copying VHDs to Azure Storage.</span></span>

* [<span data-ttu-id="64238-206">Scenariusz 1: "I am migracji istniejących maszyn wirtualnych platformy Azure do magazynu Azure Premium."</span><span class="sxs-lookup"><span data-stu-id="64238-206">Scenario 1: "I am migrating existing Azure VMs to Azure Premium Storage."</span></span>](#scenario1)
* [<span data-ttu-id="64238-207">Scenariusz 2: "I am Migrowanie maszyn wirtualnych z innych platform do magazynu Azure Premium."</span><span class="sxs-lookup"><span data-stu-id="64238-207">Scenario 2: "I am migrating VMs from other platforms to Azure Premium Storage."</span></span>](#scenario2)

### <a name="prerequisites"></a><span data-ttu-id="64238-208">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="64238-208">Prerequisites</span></span>
<span data-ttu-id="64238-209">Aby przygotować dyski VHD do migracji, potrzebne są:</span><span class="sxs-lookup"><span data-stu-id="64238-209">To prepare the VHDs for migration, you'll need:</span></span>

* <span data-ttu-id="64238-210">Subskrypcja platformy Azure, konta magazynu i kontener na tym koncie magazynu, do którego można skopiować dysk VHD.</span><span class="sxs-lookup"><span data-stu-id="64238-210">An Azure subscription, a storage account, and a container in that storage account to which you can copy your VHD.</span></span> <span data-ttu-id="64238-211">Należy pamiętać, że konto magazynu docelowego może być kontem Standard lub Premium Storage, w zależności od wymagań.</span><span class="sxs-lookup"><span data-stu-id="64238-211">Note that the destination storage account can be a Standard or Premium Storage account depending on your requirement.</span></span>
* <span data-ttu-id="64238-212">Narzędzie do uogólnienia wirtualny dysk twardy, jeśli zamierzasz utworzyć wiele wystąpień maszyn wirtualnych z niego.</span><span class="sxs-lookup"><span data-stu-id="64238-212">A tool to generalize the VHD if you plan to create multiple VM instances from it.</span></span> <span data-ttu-id="64238-213">Na przykład, program sysprep dla systemu Windows lub programu sysprep virt dla Ubuntu.</span><span class="sxs-lookup"><span data-stu-id="64238-213">For example, sysprep for Windows or virt-sysprep for Ubuntu.</span></span>
* <span data-ttu-id="64238-214">Narzędzie można przekazać pliku wirtualnego dysku twardego do konta magazynu.</span><span class="sxs-lookup"><span data-stu-id="64238-214">A tool to upload the VHD file to the Storage account.</span></span> <span data-ttu-id="64238-215">Zobacz [Transfer danych za pomocą wiersza polecenia Azcopy](storage-use-azcopy.md) lub użyj [Eksploratora usługi Azure storage](http://blogs.msdn.com/b/windowsazurestorage/archive/2014/03/11/windows-azure-storage-explorers-2014.aspx).</span><span class="sxs-lookup"><span data-stu-id="64238-215">See [Transfer data with the AzCopy Command-Line Utility](storage-use-azcopy.md) or use an [Azure storage explorer](http://blogs.msdn.com/b/windowsazurestorage/archive/2014/03/11/windows-azure-storage-explorers-2014.aspx).</span></span> <span data-ttu-id="64238-216">Ten przewodnik zawiera opis kopiowanie dysk VHD za pomocą narzędzia AzCopy.</span><span class="sxs-lookup"><span data-stu-id="64238-216">This guide describes copying your VHD using the AzCopy tool.</span></span>

> [!NOTE]
> <span data-ttu-id="64238-217">Jeśli wybierzesz opcję kopiowania synchroniczne z narzędzia AzCopy, aby uzyskać optymalną wydajność, skopiuj dysk VHD, uruchamiając jeden z tych narzędzi z maszyny Wirtualnej platformy Azure, który znajduje się w tym samym regionie co konto magazynu docelowego.</span><span class="sxs-lookup"><span data-stu-id="64238-217">If you choose synchronous copy option with AzCopy, for optimal performance, copy your VHD by running one of these tools from an Azure VM that is in the same region as the destination storage account.</span></span> <span data-ttu-id="64238-218">Jeśli kopiujesz dysk VHD maszyny Wirtualnej platformy Azure w innym regionie, wydajność może przebiegać wolniej.</span><span class="sxs-lookup"><span data-stu-id="64238-218">If you are copying a VHD from an Azure VM in a different region, your performance may be slower.</span></span>
>
> <span data-ttu-id="64238-219">W przypadku kopiowania dużych ilości danych w ograniczonej przepustowości, rozważ [na przesyłanie danych do magazynu obiektów Blob za pomocą usługi Import/Eksport Azure](../storage-import-export-service.md); dzięki temu można przenieść dane poprzez wysyłanie dysków twardych do centrum danych Azure.</span><span class="sxs-lookup"><span data-stu-id="64238-219">For copying a large amount of data over limited bandwidth, consider [using the Azure Import/Export service to transfer data to Blob Storage](../storage-import-export-service.md); this allows you to transfer your data by shipping hard disk drives to an Azure datacenter.</span></span> <span data-ttu-id="64238-220">Usługa Import/Eksport Azure umożliwia kopiowanie danych na konto magazynu w warstwie standardowa tylko.</span><span class="sxs-lookup"><span data-stu-id="64238-220">You can use the Azure Import/Export service to copy data to a standard storage account only.</span></span> <span data-ttu-id="64238-221">Po zaimportowaniu danych na koncie magazynu w warstwie standardowa, możesz użyć dowolnej [kopiowania obiektu Blob API](https://msdn.microsoft.com/library/azure/dd894037.aspx) lub AzCopy do transferu danych do swojego konta magazynu premium.</span><span class="sxs-lookup"><span data-stu-id="64238-221">Once the data is in your standard storage account, you can use either the [Copy Blob API](https://msdn.microsoft.com/library/azure/dd894037.aspx) or AzCopy to transfer the data to your premium storage account.</span></span>
>
> <span data-ttu-id="64238-222">Należy pamiętać, że Microsoft Azure obsługuje tylko pliki wirtualnego dysku twardego o stałym rozmiarze.</span><span class="sxs-lookup"><span data-stu-id="64238-222">Note that Microsoft Azure only supports fixed size VHD files.</span></span> <span data-ttu-id="64238-223">Pliki VHDX lub dynamiczne wirtualne dyski twarde nie są obsługiwane.</span><span class="sxs-lookup"><span data-stu-id="64238-223">VHDX files or dynamic VHDs are not supported.</span></span> <span data-ttu-id="64238-224">Jeśli masz dysk dynamiczny VHD można przekonwertować go na o ustalonym rozmiarze przy użyciu [Convert-VHD](http://technet.microsoft.com/library/hh848454.aspx) polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="64238-224">If you have a dynamic VHD, you can convert it to fixed size using the [Convert-VHD](http://technet.microsoft.com/library/hh848454.aspx) cmdlet.</span></span>
>
>

### <span data-ttu-id="64238-225"><a name="scenario1"></a>Scenariusz 1: "I am migracji istniejących maszyn wirtualnych platformy Azure do magazynu Azure Premium."</span><span class="sxs-lookup"><span data-stu-id="64238-225"><a name="scenario1"></a>Scenario 1: "I am migrating existing Azure VMs to Azure Premium Storage."</span></span>
<span data-ttu-id="64238-226">W przypadku migracji istniejących maszyn wirtualnych platformy Azure, Zatrzymaj maszynę Wirtualną, przygotowanie dysków VHD na typ wirtualnego dysku twardego mają, a następnie skopiuj wirtualny dysk twardy z narzędzia AzCopy lub środowiska PowerShell.</span><span class="sxs-lookup"><span data-stu-id="64238-226">If you are migrating existing Azure VMs, stop the VM, prepare VHDs per the type of VHD you want, and then copy the VHD with AzCopy or PowerShell.</span></span>

<span data-ttu-id="64238-227">Maszyna wirtualna musi być całkowicie w dół do migracji stanu czystego.</span><span class="sxs-lookup"><span data-stu-id="64238-227">The VM needs to be completely down to migrate a clean state.</span></span> <span data-ttu-id="64238-228">Będzie przestoju dopiero po zakończeniu migracji.</span><span class="sxs-lookup"><span data-stu-id="64238-228">There will be a downtime until the migration completes.</span></span>

#### <a name="step-1-prepare-vhds-for-migration"></a><span data-ttu-id="64238-229">Krok 1.</span><span class="sxs-lookup"><span data-stu-id="64238-229">Step 1.</span></span> <span data-ttu-id="64238-230">Przygotowanie do migracji dysków VHD</span><span class="sxs-lookup"><span data-stu-id="64238-230">Prepare VHDs for migration</span></span>
<span data-ttu-id="64238-231">W przypadku migracji istniejących maszyn wirtualnych platformy Azure do magazyn w warstwie Premium, może być dysk VHD:</span><span class="sxs-lookup"><span data-stu-id="64238-231">If you are migrating existing Azure VMs to Premium Storage, your VHD may be:</span></span>

* <span data-ttu-id="64238-232">Obraz systemu operacyjnego ogólnych</span><span class="sxs-lookup"><span data-stu-id="64238-232">A generalized operating system image</span></span>
* <span data-ttu-id="64238-233">Dysk systemu operacyjnego</span><span class="sxs-lookup"><span data-stu-id="64238-233">A unique operating system disk</span></span>
* <span data-ttu-id="64238-234">Dysk z danymi</span><span class="sxs-lookup"><span data-stu-id="64238-234">A data disk</span></span>

<span data-ttu-id="64238-235">Poniżej opisano firma Microsoft za pośrednictwem tych scenariuszy 3 przygotowania dysk VHD.</span><span class="sxs-lookup"><span data-stu-id="64238-235">Below we walk through these 3 scenarios for preparing your VHD.</span></span>

##### <a name="use-a-generalized-operating-system-vhd-to-create-multiple-vm-instances"></a><span data-ttu-id="64238-236">Umożliwia tworzenie wielu wystąpień maszyny Wirtualnej uogólniony wirtualny dysk twardy systemu operacyjnego</span><span class="sxs-lookup"><span data-stu-id="64238-236">Use a generalized Operating System VHD to create multiple VM instances</span></span>
<span data-ttu-id="64238-237">Podczas przekazywania wirtualnego dysku twardego używanego do utworzenia wielu wystąpień maszyny Wirtualnej Azure ogólny, należy najpierw generalize plik VHD za pomocą narzędzia sysprep.</span><span class="sxs-lookup"><span data-stu-id="64238-237">If you are uploading a VHD that will be used to create multiple generic Azure VM instances, you must first generalize VHD using a sysprep utility.</span></span> <span data-ttu-id="64238-238">Dotyczy to do wirtualnego dysku twardego, który jest lokalnie lub w chmurze.</span><span class="sxs-lookup"><span data-stu-id="64238-238">This applies to a VHD that is on-premises or in the cloud.</span></span> <span data-ttu-id="64238-239">Program Sysprep usuwa wszystkie informacje dotyczące komputera z dysku VHD.</span><span class="sxs-lookup"><span data-stu-id="64238-239">Sysprep removes any machine-specific information from the VHD.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="64238-240">Utwórz migawkę lub kopii zapasowej maszyny Wirtualnej przed jej uogólnianie.</span><span class="sxs-lookup"><span data-stu-id="64238-240">Take a snapshot or backup your VM before generalizing it.</span></span> <span data-ttu-id="64238-241">Uruchomiony program sysprep będzie zatrzymać i cofnięcia przydzielenia wystąpienia maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="64238-241">Running sysprep will stop and deallocate the VM instance.</span></span> <span data-ttu-id="64238-242">Należy wykonać poniższe czynności, aby program sysprep wirtualnego dysku twardego systemu operacyjnego Windows.</span><span class="sxs-lookup"><span data-stu-id="64238-242">Follow steps below to sysprep a Windows OS VHD.</span></span> <span data-ttu-id="64238-243">Należy pamiętać, że polecenia Sysprep będzie wymagać Zamknij maszynę wirtualną.</span><span class="sxs-lookup"><span data-stu-id="64238-243">Note that running the Sysprep command will require you to shut down the virtual machine.</span></span> <span data-ttu-id="64238-244">Aby uzyskać więcej informacji na temat narzędzia Sysprep, zobacz [Omówienie narzędzia Sysprep](http://technet.microsoft.com/library/hh825209.aspx) lub [techniczne dotyczące narzędzia Sysprep](http://technet.microsoft.com/library/cc766049.aspx).</span><span class="sxs-lookup"><span data-stu-id="64238-244">For more information about Sysprep, see [Sysprep Overview](http://technet.microsoft.com/library/hh825209.aspx) or [Sysprep Technical Reference](http://technet.microsoft.com/library/cc766049.aspx).</span></span>
>
>

1. <span data-ttu-id="64238-245">Otwórz okno wiersza polecenia z uprawnieniami administratora.</span><span class="sxs-lookup"><span data-stu-id="64238-245">Open a Command Prompt window as an administrator.</span></span>
2. <span data-ttu-id="64238-246">Wprowadź następujące polecenie, aby otworzyć narzędzie Sysprep:</span><span class="sxs-lookup"><span data-stu-id="64238-246">Enter the following command to open Sysprep:</span></span>

    ```
    %windir%\system32\sysprep\sysprep.exe
    ```

3. <span data-ttu-id="64238-247">Narzędzie przygotowywania systemu wybierz System wprowadź Out-of-Box Experience (OOBE), zaznacz pole wyboru Generalize, wybierz **zamknięcia**, a następnie kliknij przycisk **OK**, jak pokazano na poniższej ilustracji.</span><span class="sxs-lookup"><span data-stu-id="64238-247">In the System Preparation Tool, select Enter System Out-of-Box Experience (OOBE), select the Generalize check box, select **Shutdown**, and then click **OK**, as shown in the image below.</span></span> <span data-ttu-id="64238-248">Narzędzie Sysprep uogólnienia systemu operacyjnego, a następnie zamknij system.</span><span class="sxs-lookup"><span data-stu-id="64238-248">Sysprep will generalize the operating system and shut down the system.</span></span>

    ![][1]

<span data-ttu-id="64238-249">Dla maszyny Wirtualnej systemu Ubuntu należy użyć narzędzia sysprep na virt do osiągnięcia takie same.</span><span class="sxs-lookup"><span data-stu-id="64238-249">For an Ubuntu VM, use virt-sysprep to achieve the same.</span></span> <span data-ttu-id="64238-250">Zobacz [virt sysprep](http://manpages.ubuntu.com/manpages/precise/man1/virt-sysprep.1.html) więcej szczegółów.</span><span class="sxs-lookup"><span data-stu-id="64238-250">See [virt-sysprep](http://manpages.ubuntu.com/manpages/precise/man1/virt-sysprep.1.html) for more details.</span></span> <span data-ttu-id="64238-251">Zobacz też niektóre typu open source [rozbudowy serwerów Linux oprogramowania](http://www.cyberciti.biz/tips/server-provisioning-software.html) dla innych systemów operacyjnych Linux.</span><span class="sxs-lookup"><span data-stu-id="64238-251">See also some of the open source [Linux Server Provisioning software](http://www.cyberciti.biz/tips/server-provisioning-software.html) for other Linux operating systems.</span></span>

##### <a name="use-a-unique-operating-system-vhd-to-create-a-single-vm-instance"></a><span data-ttu-id="64238-252">Użyj wirtualnego dysku twardego systemu operacyjnego unikatowy, aby utworzyć jedno wystąpienie maszyny Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="64238-252">Use a unique Operating System VHD to create a single VM instance</span></span>
<span data-ttu-id="64238-253">Jeśli masz aplikacji działających na maszynie Wirtualnej, która wymaga danych określonego komputera nie generalize wirtualnego dysku twardego.</span><span class="sxs-lookup"><span data-stu-id="64238-253">If you have an application running on the VM which requires the machine specific data, do not generalize the VHD.</span></span> <span data-ttu-id="64238-254">Uogólniony wirtualny dysk twardy może służyć do utworzenia unikatowego wystąpienia maszyny Wirtualnej platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="64238-254">A non-generalized VHD can be used to create a unique Azure VM instance.</span></span> <span data-ttu-id="64238-255">Na przykład jeśli kontroler domeny na dysk VHD, wykonywanie programu sysprep, spowoduje to nieefektywne jako kontroler domeny.</span><span class="sxs-lookup"><span data-stu-id="64238-255">For example, if you have Domain Controller on your VHD, executing sysprep will make it ineffective as a Domain Controller.</span></span> <span data-ttu-id="64238-256">Przejrzyj aplikacji uruchomionych na maszynie Wirtualnej i wpływ program sysprep na nich przed uogólnianie wirtualnego dysku twardego.</span><span class="sxs-lookup"><span data-stu-id="64238-256">Review the applications running on your VM and the impact of running sysprep on them before generalizing the VHD.</span></span>

##### <a name="register-data-disk-vhd"></a><span data-ttu-id="64238-257">Zarejestruj dane dysku VHD</span><span class="sxs-lookup"><span data-stu-id="64238-257">Register data disk VHD</span></span>
<span data-ttu-id="64238-258">Jeśli masz dysków z danymi na platformie Azure do migracji, należy się upewnić się, że maszyny wirtualne korzystające z tych dysków danych są zamknięte.</span><span class="sxs-lookup"><span data-stu-id="64238-258">If you have data disks in Azure to be migrated, you must make sure the VMs that use these data disks are shut down.</span></span>

<span data-ttu-id="64238-259">Wykonaj kroki opisane poniżej, skopiuj wirtualny dysk twardy do usługi Azure Premium Storage i zarejestruj go jako dysk danych elastycznie.</span><span class="sxs-lookup"><span data-stu-id="64238-259">Follow the steps described below to copy VHD to Azure Premium Storage and register it as a provisioned data disk.</span></span>

#### <a name="step-2-create-the-destination-for-your-vhd"></a><span data-ttu-id="64238-260">Krok 2.</span><span class="sxs-lookup"><span data-stu-id="64238-260">Step 2.</span></span> <span data-ttu-id="64238-261">Utwórz obiekt docelowy dysk VHD</span><span class="sxs-lookup"><span data-stu-id="64238-261">Create the destination for your VHD</span></span>
<span data-ttu-id="64238-262">Utwórz konto magazynu do przechowywania dyski VHD.</span><span class="sxs-lookup"><span data-stu-id="64238-262">Create a storage account for maintaining your VHDs.</span></span> <span data-ttu-id="64238-263">Podczas planowania miejsca przechowywania dyski VHD, należy wziąć pod uwagę następujące kwestie:</span><span class="sxs-lookup"><span data-stu-id="64238-263">Consider the following points when planning where to store your VHDs:</span></span>

* <span data-ttu-id="64238-264">Element docelowy konta magazynu w warstwie Premium.</span><span class="sxs-lookup"><span data-stu-id="64238-264">The target Premium storage account.</span></span>
* <span data-ttu-id="64238-265">Lokalizacja konta magazynu musi być taki sam jak magazyn w warstwie Premium obsługuje maszyny wirtualne Azure utworzysz w ostatnim etapie.</span><span class="sxs-lookup"><span data-stu-id="64238-265">The storage account location must be same as Premium Storage capable Azure VMs you will create in the final stage.</span></span> <span data-ttu-id="64238-266">Można skopiować do nowego konta magazynu lub planu, aby używać tego samego konta magazynu, na podstawie Twoich potrzeb.</span><span class="sxs-lookup"><span data-stu-id="64238-266">You could copy to a new storage account, or plan to use the same storage account based on your needs.</span></span>
* <span data-ttu-id="64238-267">Skopiuj i Zapisz klucz konta magazynu docelowego konta magazynu do kolejnego etapu.</span><span class="sxs-lookup"><span data-stu-id="64238-267">Copy and save the storage account key of the destination storage account for the next stage.</span></span>

<span data-ttu-id="64238-268">W przypadku dysków danych można zachować niektóre dyski danych w ramach konta magazynu w warstwie standardowa (na przykład dysków, które mają lodówki magazynu), ale zdecydowanie zalecamy przeniesienie wszystkich danych produkcyjnych obciążenie korzysta Magazyn w warstwie premium.</span><span class="sxs-lookup"><span data-stu-id="64238-268">For data disks, you can choose to keep some data disks in a standard storage account (for example, disks that have cooler storage), but we strongly recommend you moving all data for production workload to use premium storage.</span></span>

#### <span data-ttu-id="64238-269"><a name="copy-vhd-with-azcopy-or-powershell"></a>Krok 3.</span><span class="sxs-lookup"><span data-stu-id="64238-269"><a name="copy-vhd-with-azcopy-or-powershell"></a>Step 3.</span></span> <span data-ttu-id="64238-270">Skopiuj wirtualny dysk twardy z narzędzia AzCopy lub programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="64238-270">Copy VHD with AzCopy or PowerShell</span></span>
<span data-ttu-id="64238-271">Należy znaleźć kontenera ścieżkę i magazynu klucz konta do przetwarzania jednej z tych dwóch opcji.</span><span class="sxs-lookup"><span data-stu-id="64238-271">You will need to find your container path and storage account key to process either of these two options.</span></span> <span data-ttu-id="64238-272">Kontener ścieżki i przechowywania klucza konta znajdują się w **Azure Portal** > **magazynu**.</span><span class="sxs-lookup"><span data-stu-id="64238-272">Container path and storage account key can be found in **Azure Portal** > **Storage**.</span></span> <span data-ttu-id="64238-273">Adres URL kontenera będzie takie jak "https://myaccount.blob.core.windows.net/mycontainer/".</span><span class="sxs-lookup"><span data-stu-id="64238-273">The container URL will be like "https://myaccount.blob.core.windows.net/mycontainer/".</span></span>

##### <a name="option-1-copy-a-vhd-with-azcopy-asynchronous-copy"></a><span data-ttu-id="64238-274">Opcja 1: Skopiuj dysk VHD o AzCopy (asynchroniczne kopia)</span><span class="sxs-lookup"><span data-stu-id="64238-274">Option 1: Copy a VHD with AzCopy (Asynchronous copy)</span></span>
<span data-ttu-id="64238-275">Przy użyciu narzędzia AzCopy, można łatwo przekazanie dysku VHD w Internecie.</span><span class="sxs-lookup"><span data-stu-id="64238-275">Using AzCopy, you can easily upload the VHD over the Internet.</span></span> <span data-ttu-id="64238-276">W zależności od rozmiaru dysków VHD może to potrwać.</span><span class="sxs-lookup"><span data-stu-id="64238-276">Depending on the size of the VHDs, this may take time.</span></span> <span data-ttu-id="64238-277">Pamiętaj, aby sprawdzić wejście/wyjście limity konta magazynu w przypadku użycia tej opcji.</span><span class="sxs-lookup"><span data-stu-id="64238-277">Remember to check the storage account ingress/egress limits when using this option.</span></span> <span data-ttu-id="64238-278">Zobacz [cele dotyczące wydajności i skalowalności magazynu Azure](storage-scalability-targets.md) szczegółowe informacje.</span><span class="sxs-lookup"><span data-stu-id="64238-278">See [Azure Storage Scalability and Performance Targets](storage-scalability-targets.md) for details.</span></span>

1. <span data-ttu-id="64238-279">Pobierz i zainstaluj narzędzie AzCopy stąd: [najnowszą wersję programu AzCopy](http://aka.ms/downloadazcopy)</span><span class="sxs-lookup"><span data-stu-id="64238-279">Download and install AzCopy from here: [Latest version of AzCopy](http://aka.ms/downloadazcopy)</span></span>
2. <span data-ttu-id="64238-280">Otwórz program Azure PowerShell i przejdź do folderu, w którym zainstalowano narzędzia AzCopy.</span><span class="sxs-lookup"><span data-stu-id="64238-280">Open Azure PowerShell and go to the folder where AzCopy is installed.</span></span>
3. <span data-ttu-id="64238-281">Użyj następującego polecenia, aby skopiować plik wirtualnego dysku twardego z "Source" do "Miejsce docelowe".</span><span class="sxs-lookup"><span data-stu-id="64238-281">Use the following command to copy the VHD file from "Source" to "Destination".</span></span>

    ```azcopy
    AzCopy /Source: <source> /SourceKey: <source-account-key> /Dest: <destination> /DestKey: <dest-account-key> /BlobType:page /Pattern: <file-name>
    ```

    <span data-ttu-id="64238-282">Przykład:</span><span class="sxs-lookup"><span data-stu-id="64238-282">Example:</span></span>

    ```azcopy
    AzCopy /Source:https://sourceaccount.blob.core.windows.net/mycontainer1 /SourceKey:key1 /Dest:https://destaccount.blob.core.windows.net/mycontainer2 /DestKey:key2 /Pattern:abc.vhd
    ```

    <span data-ttu-id="64238-283">Poniżej przedstawiono opisy parametrów polecenia AzCopy:</span><span class="sxs-lookup"><span data-stu-id="64238-283">Here are descriptions of the parameters used in the AzCopy command:</span></span>

   * <span data-ttu-id="64238-284">**/ Źródło:  *&lt;źródła&gt;:***  lokalizację folderu lub adresu URL kontenera magazynu, która zawiera wirtualny dysk twardy.</span><span class="sxs-lookup"><span data-stu-id="64238-284">**/Source: *&lt;source&gt;:*** Location of the folder or storage container URL that contains the VHD.</span></span>
   * <span data-ttu-id="64238-285">**/ SourceKey:  *&lt;źródła konta klucza&gt;:***  klucz konta magazynu źródłowego konta magazynu.</span><span class="sxs-lookup"><span data-stu-id="64238-285">**/SourceKey: *&lt;source-account-key&gt;:*** Storage account key of the source storage account.</span></span>
   * <span data-ttu-id="64238-286">**/ Dest:  *&lt;docelowego&gt;:***  adresu URL kontenera magazynu, aby skopiować dysk VHD do.</span><span class="sxs-lookup"><span data-stu-id="64238-286">**/Dest: *&lt;destination&gt;:*** Storage container URL to copy the VHD to.</span></span>
   * <span data-ttu-id="64238-287">**/ DestKey:  *&lt;dest konta klucza&gt;:***  klucz konta magazynu docelowego konta magazynu.</span><span class="sxs-lookup"><span data-stu-id="64238-287">**/DestKey: *&lt;dest-account-key&gt;:*** Storage account key of the destination storage account.</span></span>
   * <span data-ttu-id="64238-288">**/ Wzorzec:  *&lt;nazwę pliku&gt;:***  Określ nazwę pliku wirtualnego dysku twardego do skopiowania.</span><span class="sxs-lookup"><span data-stu-id="64238-288">**/Pattern: *&lt;file-name&gt;:*** Specify the file name of the VHD to copy.</span></span>

<span data-ttu-id="64238-289">Aby uzyskać więcej informacji na temat używania narzędzia AzCopy narzędzie, zobacz [Transfer danych za pomocą wiersza polecenia Azcopy](storage-use-azcopy.md).</span><span class="sxs-lookup"><span data-stu-id="64238-289">For details on using AzCopy tool, see [Transfer data with the AzCopy Command-Line Utility](storage-use-azcopy.md).</span></span>

##### <a name="option-2-copy-a-vhd-with-powershell-synchronized-copy"></a><span data-ttu-id="64238-290">Opcja 2: Kopiować dysku VHD przy użyciu programu PowerShell (Synchronized kopia)</span><span class="sxs-lookup"><span data-stu-id="64238-290">Option 2: Copy a VHD with PowerShell (Synchronized copy)</span></span>
<span data-ttu-id="64238-291">Możesz również skopiować plik VHD za pomocą polecenia cmdlet programu PowerShell Start-AzureStorageBlobCopy.</span><span class="sxs-lookup"><span data-stu-id="64238-291">You can also copy the VHD file using the PowerShell cmdlet Start-AzureStorageBlobCopy.</span></span> <span data-ttu-id="64238-292">Użyj następującego polecenia na programu Azure PowerShell, aby skopiować wirtualny dysk twardy.</span><span class="sxs-lookup"><span data-stu-id="64238-292">Use the following command on Azure PowerShell to copy VHD.</span></span> <span data-ttu-id="64238-293">Zastąp wartości w <> odpowiednie wartości w ramach konta magazynu źródłowego i docelowego.</span><span class="sxs-lookup"><span data-stu-id="64238-293">Replace the values in <> with corresponding values from your source and destination storage account.</span></span> <span data-ttu-id="64238-294">Aby użyć tego polecenia, musi mieć kontener o nazwie wirtualne dyski twarde na koncie magazynu docelowego.</span><span class="sxs-lookup"><span data-stu-id="64238-294">To use this command, you must have a container called vhds in your destination storage account.</span></span> <span data-ttu-id="64238-295">Jeśli kontener nie istnieje, utwórz je przed uruchomieniem polecenia.</span><span class="sxs-lookup"><span data-stu-id="64238-295">If the container doesn't exist, create one before running the command.</span></span>

```powershell
$sourceBlobUri = <source-vhd-uri>

$sourceContext = New-AzureStorageContext  –StorageAccountName <source-account> -StorageAccountKey <source-account-key>

$destinationContext = New-AzureStorageContext  –StorageAccountName <dest-account> -StorageAccountKey <dest-account-key>

Start-AzureStorageBlobCopy -srcUri $sourceBlobUri -SrcContext $sourceContext -DestContainer <dest-container> -DestBlob <dest-disk-name> -DestContext $destinationContext
```

<span data-ttu-id="64238-296">Przykład:</span><span class="sxs-lookup"><span data-stu-id="64238-296">Example:</span></span>

```powershell
C:\PS> $sourceBlobUri = "https://sourceaccount.blob.core.windows.net/vhds/myvhd.vhd"

C:\PS> $sourceContext = New-AzureStorageContext  –StorageAccountName "sourceaccount" -StorageAccountKey "J4zUI9T5b8gvHohkiRg"

C:\PS> $destinationContext = New-AzureStorageContext  –StorageAccountName "destaccount" -StorageAccountKey "XZTmqSGKUYFSh7zB5"

C:\PS> Start-AzureStorageBlobCopy -srcUri $sourceBlobUri -SrcContext $sourceContext -DestContainer "vhds" -DestBlob "myvhd.vhd" -DestContext $destinationContext
```

### <span data-ttu-id="64238-297"><a name="scenario2"></a>Scenariusz 2: "I am Migrowanie maszyn wirtualnych z innych platform do magazynu Azure Premium."</span><span class="sxs-lookup"><span data-stu-id="64238-297"><a name="scenario2"></a>Scenario 2: "I am migrating VMs from other platforms to Azure Premium Storage."</span></span>
<span data-ttu-id="64238-298">W przypadku migracji wirtualnego dysku twardego z innych niż - Azure magazynu w chmurze na platformie Azure, możesz wyeksportować wirtualnego dysku twardego do katalogu lokalnego.</span><span class="sxs-lookup"><span data-stu-id="64238-298">If you are migrating VHD from non-Azure Cloud Storage to Azure, you must first export the VHD to a local directory.</span></span> <span data-ttu-id="64238-299">Ścieżka źródłowej pełną katalogu lokalnego wirtualnego dysku twardego przechowywania przydatną i przekaż go do usługi Azure Storage za pomocą narzędzia AzCopy.</span><span class="sxs-lookup"><span data-stu-id="64238-299">Have the complete source path of the local directory where VHD is stored handy, and then using AzCopy to upload it to Azure Storage.</span></span>

#### <a name="step-1-export-vhd-to-a-local-directory"></a><span data-ttu-id="64238-300">Krok 1.</span><span class="sxs-lookup"><span data-stu-id="64238-300">Step 1.</span></span> <span data-ttu-id="64238-301">Eksportowanie do katalogu lokalnego wirtualnego dysku twardego</span><span class="sxs-lookup"><span data-stu-id="64238-301">Export VHD to a local directory</span></span>
##### <a name="copy-a-vhd-from-aws"></a><span data-ttu-id="64238-302">Skopiuj wirtualny dysk twardy z usług AWS</span><span class="sxs-lookup"><span data-stu-id="64238-302">Copy a VHD from AWS</span></span>
1. <span data-ttu-id="64238-303">Jeśli używasz usług AWS wyeksportować wystąpienia EC2 do dysku VHD w zasobniku Amazon S3.</span><span class="sxs-lookup"><span data-stu-id="64238-303">If you are using AWS, export the EC2 instance to a VHD in an Amazon S3 bucket.</span></span> <span data-ttu-id="64238-304">Wykonaj kroki opisane w dokumentacji usługi Amazon eksportowanie Amazon EC2 wystąpień Zainstaluj narzędzie Amazon EC2 interfejsu wiersza polecenia (CLI) i uruchom polecenie eksportu zadań, Utwórz wystąpienie w — Aby wyeksportować wystąpienia EC2 do pliku dysku VHD.</span><span class="sxs-lookup"><span data-stu-id="64238-304">Follow the steps described in the Amazon documentation for Exporting Amazon EC2 Instances to install the Amazon EC2 command-line interface (CLI) tool and run the create-instance-export-task command to export the EC2 instance to a VHD file.</span></span> <span data-ttu-id="64238-305">Należy użyć **wirtualnego dysku twardego** dla dysku &#95; obraz &#95; FORMAT zmiennej podczas uruchamiania **tworzenie — wystąpienie export zadania** polecenia.</span><span class="sxs-lookup"><span data-stu-id="64238-305">Be sure to use **VHD** for the DISK&#95;IMAGE&#95;FORMAT variable when running the **create-instance-export-task** command.</span></span> <span data-ttu-id="64238-306">Wyeksportowany plik wirtualnego dysku twardego jest zapisany w zasobniku Amazon S3, którą określisz podczas tego procesu.</span><span class="sxs-lookup"><span data-stu-id="64238-306">The exported VHD file is saved in the Amazon S3 bucket you designate during that process.</span></span>

    ```
    aws ec2 create-instance-export-task --instance-id ID --target-environment TARGET_ENVIRONMENT \
      --export-to-s3-task DiskImageFormat=DISK_IMAGE_FORMAT,ContainerFormat=ova,S3Bucket=BUCKET,S3Prefix=PREFIX
    ```

2. <span data-ttu-id="64238-307">Pobierz plik VHD z przedział S3.</span><span class="sxs-lookup"><span data-stu-id="64238-307">Download the VHD file from the S3 bucket.</span></span> <span data-ttu-id="64238-308">Wybierz plik dysku VHD, a następnie **akcje** > **Pobierz**.</span><span class="sxs-lookup"><span data-stu-id="64238-308">Select the VHD file, then **Actions** > **Download**.</span></span>

    ![][3]

##### <a name="copy-a-vhd-from-other-non-azure-cloud"></a><span data-ttu-id="64238-309">Skopiuj wirtualny dysk twardy z innych chmury Azure z systemem innym niż</span><span class="sxs-lookup"><span data-stu-id="64238-309">Copy a VHD from other non-Azure cloud</span></span>
<span data-ttu-id="64238-310">W przypadku migracji wirtualnego dysku twardego z innych niż - Azure magazynu w chmurze na platformie Azure, możesz wyeksportować wirtualnego dysku twardego do katalogu lokalnego.</span><span class="sxs-lookup"><span data-stu-id="64238-310">If you are migrating VHD from non-Azure Cloud Storage to Azure, you must first export the VHD to a local directory.</span></span> <span data-ttu-id="64238-311">Skopiuj ścieżkę źródłową pełny katalog lokalny, w którym przechowywana jest wirtualnego dysku twardego.</span><span class="sxs-lookup"><span data-stu-id="64238-311">Copy the complete source path of the local directory where VHD is stored.</span></span>

##### <a name="copy-a-vhd-from-on-premises"></a><span data-ttu-id="64238-312">Skopiuj wirtualny dysk twardy z lokalnymi</span><span class="sxs-lookup"><span data-stu-id="64238-312">Copy a VHD from on-premises</span></span>
<span data-ttu-id="64238-313">W przypadku migracji ze środowiska lokalnego wirtualnego dysku twardego, konieczne będzie ścieżki źródłowej pełną przechowywania wirtualnego dysku twardego.</span><span class="sxs-lookup"><span data-stu-id="64238-313">If you are migrating VHD from an on-premises environment, you will need the complete source path where VHD is stored.</span></span> <span data-ttu-id="64238-314">Ścieżka źródłowa może być serwerem lokalizacji lub w udziale plików.</span><span class="sxs-lookup"><span data-stu-id="64238-314">The source path could be a server location or file share.</span></span>

#### <a name="step-2-create-the-destination-for-your-vhd"></a><span data-ttu-id="64238-315">Krok 2.</span><span class="sxs-lookup"><span data-stu-id="64238-315">Step 2.</span></span> <span data-ttu-id="64238-316">Utwórz obiekt docelowy dysk VHD</span><span class="sxs-lookup"><span data-stu-id="64238-316">Create the destination for your VHD</span></span>
<span data-ttu-id="64238-317">Utwórz konto magazynu do przechowywania dyski VHD.</span><span class="sxs-lookup"><span data-stu-id="64238-317">Create a storage account for maintaining your VHDs.</span></span> <span data-ttu-id="64238-318">Podczas planowania miejsca przechowywania dyski VHD, należy wziąć pod uwagę następujące kwestie:</span><span class="sxs-lookup"><span data-stu-id="64238-318">Consider the following points when planning where to store your VHDs:</span></span>

* <span data-ttu-id="64238-319">Docelowe konto magazynu może być standard lub premium magazynu w zależności od wymagań aplikacji.</span><span class="sxs-lookup"><span data-stu-id="64238-319">The target storage account could be standard or premium storage depending on your application requirement.</span></span>
* <span data-ttu-id="64238-320">Region konta magazynu musi być taki sam jak magazyn w warstwie Premium obsługuje maszyny wirtualne Azure utworzysz w ostatnim etapie.</span><span class="sxs-lookup"><span data-stu-id="64238-320">The storage account region must be same as Premium Storage capable Azure VMs you will create in the final stage.</span></span> <span data-ttu-id="64238-321">Można skopiować do nowego konta magazynu lub planu, aby używać tego samego konta magazynu, na podstawie Twoich potrzeb.</span><span class="sxs-lookup"><span data-stu-id="64238-321">You could copy to a new storage account, or plan to use the same storage account based on your needs.</span></span>
* <span data-ttu-id="64238-322">Skopiuj i Zapisz klucz konta magazynu docelowego konta magazynu do kolejnego etapu.</span><span class="sxs-lookup"><span data-stu-id="64238-322">Copy and save the storage account key of the destination storage account for the next stage.</span></span>

<span data-ttu-id="64238-323">Ale zdecydowanie zalecamy przeniesienie wszystkich danych produkcyjnych obciążenie korzysta Magazyn w warstwie premium.</span><span class="sxs-lookup"><span data-stu-id="64238-323">We strongly recommend you moving all data for production workload to use premium storage.</span></span>

#### <a name="step-3-upload-the-vhd-to-azure-storage"></a><span data-ttu-id="64238-324">Krok 3.</span><span class="sxs-lookup"><span data-stu-id="64238-324">Step 3.</span></span> <span data-ttu-id="64238-325">Przekazywanie wirtualnego dysku twardego do magazynu Azure</span><span class="sxs-lookup"><span data-stu-id="64238-325">Upload the VHD to Azure Storage</span></span>
<span data-ttu-id="64238-326">Dysk VHD jest już w katalogu lokalnym, można użyć narzędzia AzCopy lub AzurePowerShell można przekazać pliku VHD do magazynu Azure.</span><span class="sxs-lookup"><span data-stu-id="64238-326">Now that you have your VHD in the local directory, you can use AzCopy or AzurePowerShell to upload the .vhd file to Azure Storage.</span></span> <span data-ttu-id="64238-327">Obie te opcje są dostępne w tym miejscu:</span><span class="sxs-lookup"><span data-stu-id="64238-327">Both options are provided here:</span></span>

##### <a name="option-1-using-azure-powershell-add-azurevhd-to-upload-the-vhd-file"></a><span data-ttu-id="64238-328">Opcja 1: Przy użyciu usługi Azure PowerShell Add-AzureVhd przekazać plik VHD</span><span class="sxs-lookup"><span data-stu-id="64238-328">Option 1: Using Azure PowerShell Add-AzureVhd to upload the .vhd file</span></span>

```powershell
Add-AzureVhd [-Destination] <Uri> [-LocalFilePath] <FileInfo>
```

<span data-ttu-id="64238-329">Przykład <Uri> może być ***"https://storagesample.blob.core.windows.net/mycontainer/blob1.vhd"***.</span><span class="sxs-lookup"><span data-stu-id="64238-329">An example <Uri> might be ***"https://storagesample.blob.core.windows.net/mycontainer/blob1.vhd"***.</span></span> <span data-ttu-id="64238-330">Przykład <FileInfo> może być ***"C:\path\to\upload.vhd"***.</span><span class="sxs-lookup"><span data-stu-id="64238-330">An example <FileInfo> might be ***"C:\path\to\upload.vhd"***.</span></span>

##### <a name="option-2-using-azcopy-to-upload-the-vhd-file"></a><span data-ttu-id="64238-331">Opcja 2: Przy użyciu narzędzia AzCopy można przekazać pliku VHD</span><span class="sxs-lookup"><span data-stu-id="64238-331">Option 2: Using AzCopy to upload the .vhd file</span></span>
<span data-ttu-id="64238-332">Przy użyciu narzędzia AzCopy, można łatwo przekazanie dysku VHD w Internecie.</span><span class="sxs-lookup"><span data-stu-id="64238-332">Using AzCopy, you can easily upload the VHD over the Internet.</span></span> <span data-ttu-id="64238-333">W zależności od rozmiaru dysków VHD może to potrwać.</span><span class="sxs-lookup"><span data-stu-id="64238-333">Depending on the size of the VHDs, this may take time.</span></span> <span data-ttu-id="64238-334">Pamiętaj, aby sprawdzić wejście/wyjście limity konta magazynu w przypadku użycia tej opcji.</span><span class="sxs-lookup"><span data-stu-id="64238-334">Remember to check the storage account ingress/egress limits when using this option.</span></span> <span data-ttu-id="64238-335">Zobacz [cele dotyczące wydajności i skalowalności magazynu Azure](storage-scalability-targets.md) szczegółowe informacje.</span><span class="sxs-lookup"><span data-stu-id="64238-335">See [Azure Storage Scalability and Performance Targets](storage-scalability-targets.md) for details.</span></span>

1. <span data-ttu-id="64238-336">Pobierz i zainstaluj narzędzie AzCopy stąd: [najnowszą wersję programu AzCopy](http://aka.ms/downloadazcopy)</span><span class="sxs-lookup"><span data-stu-id="64238-336">Download and install AzCopy from here: [Latest version of AzCopy](http://aka.ms/downloadazcopy)</span></span>
2. <span data-ttu-id="64238-337">Otwórz program Azure PowerShell i przejdź do folderu, w którym zainstalowano narzędzia AzCopy.</span><span class="sxs-lookup"><span data-stu-id="64238-337">Open Azure PowerShell and go to the folder where AzCopy is installed.</span></span>
3. <span data-ttu-id="64238-338">Użyj następującego polecenia, aby skopiować plik wirtualnego dysku twardego z "Source" do "Miejsce docelowe".</span><span class="sxs-lookup"><span data-stu-id="64238-338">Use the following command to copy the VHD file from "Source" to "Destination".</span></span>

    ```azcopy
    AzCopy /Source: <source> /SourceKey: <source-account-key> /Dest: <destination> /DestKey: <dest-account-key> /BlobType:page /Pattern: <file-name>
    ```

    <span data-ttu-id="64238-339">Przykład:</span><span class="sxs-lookup"><span data-stu-id="64238-339">Example:</span></span>

    ```azcopy
    AzCopy /Source:https://sourceaccount.blob.core.windows.net/mycontainer1 /SourceKey:key1 /Dest:https://destaccount.blob.core.windows.net/mycontainer2 /DestKey:key2 /BlobType:page /Pattern:abc.vhd
    ```

    <span data-ttu-id="64238-340">Poniżej przedstawiono opisy parametrów polecenia AzCopy:</span><span class="sxs-lookup"><span data-stu-id="64238-340">Here are descriptions of the parameters used in the AzCopy command:</span></span>

   * <span data-ttu-id="64238-341">**/ Źródło:  *&lt;źródła&gt;:***  lokalizację folderu lub adresu URL kontenera magazynu, która zawiera wirtualny dysk twardy.</span><span class="sxs-lookup"><span data-stu-id="64238-341">**/Source: *&lt;source&gt;:*** Location of the folder or storage container URL that contains the VHD.</span></span>
   * <span data-ttu-id="64238-342">**/ SourceKey:  *&lt;źródła konta klucza&gt;:***  klucz konta magazynu źródłowego konta magazynu.</span><span class="sxs-lookup"><span data-stu-id="64238-342">**/SourceKey: *&lt;source-account-key&gt;:*** Storage account key of the source storage account.</span></span>
   * <span data-ttu-id="64238-343">**/ Dest:  *&lt;docelowego&gt;:***  adresu URL kontenera magazynu, aby skopiować dysk VHD do.</span><span class="sxs-lookup"><span data-stu-id="64238-343">**/Dest: *&lt;destination&gt;:*** Storage container URL to copy the VHD to.</span></span>
   * <span data-ttu-id="64238-344">**/ DestKey:  *&lt;dest konta klucza&gt;:***  klucz konta magazynu docelowego konta magazynu.</span><span class="sxs-lookup"><span data-stu-id="64238-344">**/DestKey: *&lt;dest-account-key&gt;:*** Storage account key of the destination storage account.</span></span>
   * <span data-ttu-id="64238-345">**/ BlobType: strony:** Określa, że docelowy stronicowych obiektów blob.</span><span class="sxs-lookup"><span data-stu-id="64238-345">**/BlobType: page:** Specifies that the destination is a page blob.</span></span>
   * <span data-ttu-id="64238-346">**/ Wzorzec:  *&lt;nazwę pliku&gt;:***  Określ nazwę pliku wirtualnego dysku twardego do skopiowania.</span><span class="sxs-lookup"><span data-stu-id="64238-346">**/Pattern: *&lt;file-name&gt;:*** Specify the file name of the VHD to copy.</span></span>

<span data-ttu-id="64238-347">Aby uzyskać więcej informacji na temat używania narzędzia AzCopy narzędzie, zobacz [Transfer danych za pomocą wiersza polecenia Azcopy](storage-use-azcopy.md).</span><span class="sxs-lookup"><span data-stu-id="64238-347">For details on using AzCopy tool, see [Transfer data with the AzCopy Command-Line Utility](storage-use-azcopy.md).</span></span>

##### <a name="other-options-for-uploading-a-vhd"></a><span data-ttu-id="64238-348">Inne opcje przekazywanie wirtualnego dysku twardego</span><span class="sxs-lookup"><span data-stu-id="64238-348">Other options for uploading a VHD</span></span>
<span data-ttu-id="64238-349">Możesz również przekazywać dysku VHD do konta magazynu przy użyciu jednej z następujących sposobów:</span><span class="sxs-lookup"><span data-stu-id="64238-349">You can also upload a VHD to your storage account using one of the following means:</span></span>

* [<span data-ttu-id="64238-350">Obiektu Blob magazynu Azure kopiowania interfejsu API</span><span class="sxs-lookup"><span data-stu-id="64238-350">Azure Storage Copy Blob API</span></span>](https://msdn.microsoft.com/library/azure/dd894037.aspx)
* [<span data-ttu-id="64238-351">Obiekty BLOB magazynu Azure Explorer przekazywania</span><span class="sxs-lookup"><span data-stu-id="64238-351">Azure Storage Explorer Uploading Blobs</span></span>](https://azurestorageexplorer.codeplex.com/)
* [<span data-ttu-id="64238-352">Dokumentacja interfejsu API REST usługi Import/Eksport magazynu</span><span class="sxs-lookup"><span data-stu-id="64238-352">Storage Import/Export Service REST API Reference</span></span>](https://msdn.microsoft.com/library/dn529096.aspx)

> [!NOTE]
> <span data-ttu-id="64238-353">Zaleca się za pomocą usługi Import/eksport, jeśli szacowany czas przekazywania jest dłuższa niż 7 dni.</span><span class="sxs-lookup"><span data-stu-id="64238-353">We recommend using Import/Export Service if estimated uploading time is longer than 7 days.</span></span> <span data-ttu-id="64238-354">Można użyć [DataTransferSpeedCalculator](https://github.com/Azure-Samples/storage-dotnet-import-export-job-management/blob/master/DataTransferSpeedCalculator.html) oszacowanie godzinę z jednostki rozmiaru i transferu danych.</span><span class="sxs-lookup"><span data-stu-id="64238-354">You can use [DataTransferSpeedCalculator](https://github.com/Azure-Samples/storage-dotnet-import-export-job-management/blob/master/DataTransferSpeedCalculator.html) to estimate the time from data size and transfer unit.</span></span>
>
> <span data-ttu-id="64238-355">Narzędzie importu/eksportu może służyć do skopiowania do konta magazynu w warstwie standardowa.</span><span class="sxs-lookup"><span data-stu-id="64238-355">Import/Export can be used to copy to a standard storage account.</span></span> <span data-ttu-id="64238-356">Należy skopiować z magazynu w warstwie standardowa do konta magazynu premium za pomocą narzędzia, takiego jak narzędzie AzCopy.</span><span class="sxs-lookup"><span data-stu-id="64238-356">You will need to copy from standard storage to premium storage account using a tool like AzCopy.</span></span>
>
>

## <span data-ttu-id="64238-357"><a name="create-azure-virtual-machine-using-premium-storage"></a>Tworzenie maszyn wirtualnych platformy Azure przy użyciu magazyn w warstwie Premium</span><span class="sxs-lookup"><span data-stu-id="64238-357"><a name="create-azure-virtual-machine-using-premium-storage"></a>Create Azure VMs using Premium Storage</span></span>
<span data-ttu-id="64238-358">Po wirtualny dysk twardy jest przekazany lub kopiowane do odpowiednie konto magazynu, postępuj zgodnie z instrukcjami w tej sekcji, aby zarejestrować wirtualnego dysku twardego jako obraz systemu operacyjnego lub dysku systemu operacyjnego, w zależności od scenariusza, a następnie utwórz wystąpienie maszyny Wirtualnej z niego.</span><span class="sxs-lookup"><span data-stu-id="64238-358">After the VHD is uploaded or copied to the desired storage account, follow the instructions in this section to register the VHD as an OS image, or OS disk depending on your scenario and then create a VM instance from it.</span></span> <span data-ttu-id="64238-359">Dane dysku VHD może zostać dołączona do maszyny Wirtualnej, po jego utworzeniu.</span><span class="sxs-lookup"><span data-stu-id="64238-359">The data disk VHD can be attached to the VM once it is created.</span></span>
<span data-ttu-id="64238-360">Przykładowy skrypt migracji znajduje się na końcu tej sekcji.</span><span class="sxs-lookup"><span data-stu-id="64238-360">A sample migration script is provided at the end of this section.</span></span> <span data-ttu-id="64238-361">Ten prosty skrypt nie jest zgodna wszystkie scenariusze.</span><span class="sxs-lookup"><span data-stu-id="64238-361">This simple script does not match all scenarios.</span></span> <span data-ttu-id="64238-362">Może być konieczne zaktualizowanie skryptu pasuje do konkretnego scenariusza.</span><span class="sxs-lookup"><span data-stu-id="64238-362">You may need to update the script to match with your specific scenario.</span></span> <span data-ttu-id="64238-363">Aby sprawdzić, czy ten skrypt ma zastosowanie do danego scenariusza, zobacz poniżej [A przykładowy skrypt migracji](#a-sample-migration-script).</span><span class="sxs-lookup"><span data-stu-id="64238-363">To see if this script applies to your scenario, see below [A Sample Migration Script](#a-sample-migration-script).</span></span>

### <a name="checklist"></a><span data-ttu-id="64238-364">Lista kontrolna</span><span class="sxs-lookup"><span data-stu-id="64238-364">Checklist</span></span>
1. <span data-ttu-id="64238-365">Zaczekaj na wszystkie dyski VHD Kopiowanie zostało ukończone.</span><span class="sxs-lookup"><span data-stu-id="64238-365">Wait until all the VHD disks copying is complete.</span></span>
2. <span data-ttu-id="64238-366">Upewnij się, że magazyn w warstwie Premium jest dostępna w regionie, który w przypadku migracji do.</span><span class="sxs-lookup"><span data-stu-id="64238-366">Make sure Premium Storage is available in the region you are migrating to.</span></span>
3. <span data-ttu-id="64238-367">Zdecyduj, nowej serii maszyny Wirtualnej, który będzie używany.</span><span class="sxs-lookup"><span data-stu-id="64238-367">Decide the new VM series you will be using.</span></span> <span data-ttu-id="64238-368">Powinna być funkcją Magazyn w warstwie Premium, a rozmiar powinien być w zależności od dostępności w regionie i na podstawie Twoich potrzeb.</span><span class="sxs-lookup"><span data-stu-id="64238-368">It should be a Premium Storage capable, and the size should be depending on the availability in the region and based on your needs.</span></span>
4. <span data-ttu-id="64238-369">Zdecyduj, dokładne rozmiar maszyny Wirtualnej, które będą używane.</span><span class="sxs-lookup"><span data-stu-id="64238-369">Decide the exact VM size you will use.</span></span> <span data-ttu-id="64238-370">Rozmiar maszyny Wirtualnej musi być wystarczająco duży, aby obsługiwał liczba dysków danych, do których masz.</span><span class="sxs-lookup"><span data-stu-id="64238-370">VM size needs to be large enough to support the number of data disks you have.</span></span> <span data-ttu-id="64238-371">Na przykład</span><span class="sxs-lookup"><span data-stu-id="64238-371">E.g.</span></span> <span data-ttu-id="64238-372">Jeśli masz 4 dysków danych maszyny Wirtualnej musi mieć co najmniej 2 rdzeni.</span><span class="sxs-lookup"><span data-stu-id="64238-372">if you have 4 data disks, the VM must have 2 or more cores.</span></span> <span data-ttu-id="64238-373">Należy również rozważyć przetwarzania zasilania, pamięci i musi przepustowości sieci.</span><span class="sxs-lookup"><span data-stu-id="64238-373">Also, consider processing power, memory and network bandwidth needs.</span></span>
5. <span data-ttu-id="64238-374">Tworzenie konta Premium Storage w obszarze docelowym.</span><span class="sxs-lookup"><span data-stu-id="64238-374">Create a Premium Storage account in the target region.</span></span> <span data-ttu-id="64238-375">Jest to konto, które będą używane dla nowej maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="64238-375">This is the account you will use for the new VM.</span></span>
6. <span data-ttu-id="64238-376">Mieć bieżące szczegóły maszyny Wirtualnej pod ręką, w tym listę dysków i odpowiednie obiekty BLOB dysków VHD.</span><span class="sxs-lookup"><span data-stu-id="64238-376">Have the current VM details handy, including the list of disks and corresponding VHD blobs.</span></span>

<span data-ttu-id="64238-377">Przygotowanie aplikacji dla przestoju.</span><span class="sxs-lookup"><span data-stu-id="64238-377">Prepare your application for downtime.</span></span> <span data-ttu-id="64238-378">Przeprowadzenie czystej migracji, należy zatrzymać wszystkie przetwarzania w systemie.</span><span class="sxs-lookup"><span data-stu-id="64238-378">To do a clean migration, you have to stop all the processing in the current system.</span></span> <span data-ttu-id="64238-379">Następnie możesz pobrać go do spójnego stanu, które można migrować do nowej platformie.</span><span class="sxs-lookup"><span data-stu-id="64238-379">Only then you can get it to consistent state which you can migrate to the new platform.</span></span> <span data-ttu-id="64238-380">Czas trwania przestoju zależy od ilości danych na dyskach, aby przeprowadzić migrację.</span><span class="sxs-lookup"><span data-stu-id="64238-380">Downtime duration will depend on the amount of data in the disks to migrate.</span></span>

> [!NOTE]
> <span data-ttu-id="64238-381">W przypadku tworzenia maszyny Wirtualnej platformy Azure Resource Manager z specjalne dysku VHD, zapoznaj się z [ten szablon](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-specialized-vhd) wdrażania Menedżera zasobów maszyny Wirtualnej przy użyciu istniejącego dysku.</span><span class="sxs-lookup"><span data-stu-id="64238-381">If you are creating an Azure Resource Manager VM from a specialized VHD Disk, please refer to [this template](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-specialized-vhd) for deploying Resource Manager VM using existing disk.</span></span>
>
>

### <a name="register-your-vhd"></a><span data-ttu-id="64238-382">Zarejestruj dysk VHD</span><span class="sxs-lookup"><span data-stu-id="64238-382">Register your VHD</span></span>
<span data-ttu-id="64238-383">Aby utworzyć Maszynę wirtualną z wirtualnego dysku twardego systemu operacyjnego lub można dołączyć dysku danych do nowej maszyny Wirtualnej, należy je najpierw zarejestrować.</span><span class="sxs-lookup"><span data-stu-id="64238-383">To create a VM from OS VHD or to attach a data disk to a new VM, you must first register them.</span></span> <span data-ttu-id="64238-384">Wykonaj poniższe kroki w zależności od scenariusza z wirtualnego dysku twardego.</span><span class="sxs-lookup"><span data-stu-id="64238-384">Follow steps below depending on your VHD's scenario.</span></span>

#### <a name="generalized-operating-system-vhd-to-create-multiple-azure-vm-instances"></a><span data-ttu-id="64238-385">Uogólniony wirtualny dysk twardy systemu operacyjnego do utworzenia wielu wystąpień maszyny Wirtualnej Azure</span><span class="sxs-lookup"><span data-stu-id="64238-385">Generalized Operating System VHD to create multiple Azure VM instances</span></span>
<span data-ttu-id="64238-386">Po obrazu systemu operacyjnego uogólniony wirtualny dysk twardy zostanie przekazany do konta magazynu, należy zarejestrować go w formie **obrazu maszyny Wirtualnej Azure** tak, aby z niego można utworzyć co najmniej jedno wystąpienie maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="64238-386">After generalized OS image VHD is uploaded to the storage account, register it as an **Azure VM Image** so that you can create one or more VM instances from it.</span></span> <span data-ttu-id="64238-387">Aby zarejestrować dysk VHD jako obrazu systemu operacyjnego maszyny Wirtualnej Azure, użyj następujących poleceń cmdlet programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="64238-387">Use the following PowerShell cmdlets to register your VHD as an Azure VM OS image.</span></span> <span data-ttu-id="64238-388">Podaj adres URL kontenera pełną, gdzie wirtualnego dysku twardego został skopiowany do.</span><span class="sxs-lookup"><span data-stu-id="64238-388">Provide the complete container URL where VHD was copied to.</span></span>

```powershell
Add-AzureVMImage -ImageName "OSImageName" -MediaLocation "https://storageaccount.blob.core.windows.net/vhdcontainer/osimage.vhd" -OS Windows
```

<span data-ttu-id="64238-389">Skopiuj i Zapisz nazwę tego nowego obrazu maszyny Wirtualnej Azure.</span><span class="sxs-lookup"><span data-stu-id="64238-389">Copy and save the name of this new Azure VM Image.</span></span> <span data-ttu-id="64238-390">W powyższym przykładzie jest *OSImageName*.</span><span class="sxs-lookup"><span data-stu-id="64238-390">In the example above, it is *OSImageName*.</span></span>

#### <a name="unique-operating-system-vhd-to-create-a-single-azure-vm-instance"></a><span data-ttu-id="64238-391">Unikatowy wirtualnego dysku twardego systemu operacyjnego można utworzyć jedno wystąpienie maszyny Wirtualnej Azure</span><span class="sxs-lookup"><span data-stu-id="64238-391">Unique Operating System VHD to create a single Azure VM instance</span></span>
<span data-ttu-id="64238-392">Po przekazaniu unikatowy wirtualnego dysku twardego systemu operacyjnego z kontem magazynu, zarejestruj je jako **dysk systemu operacyjnego Azure** tak, aby z niego można utworzyć wystąpienia maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="64238-392">After the unique OS VHD is uploaded to the storage account, register it as an **Azure OS Disk** so that you can create a VM instance from it.</span></span> <span data-ttu-id="64238-393">Aby zarejestrować dysk VHD jako dysk systemu operacyjnego Azure, użyj tych poleceń cmdlet programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="64238-393">Use these PowerShell cmdlets to register your VHD as an Azure OS Disk.</span></span> <span data-ttu-id="64238-394">Podaj adres URL kontenera pełną, gdzie wirtualnego dysku twardego został skopiowany do.</span><span class="sxs-lookup"><span data-stu-id="64238-394">Provide the complete container URL where VHD was copied to.</span></span>

```powershell
Add-AzureDisk -DiskName "OSDisk" -MediaLocation "https://storageaccount.blob.core.windows.net/vhdcontainer/osdisk.vhd" -Label "My OS Disk" -OS "Windows"
```

<span data-ttu-id="64238-395">Skopiuj i Zapisz nazwę tego nowego dysku systemu operacyjnego Azure.</span><span class="sxs-lookup"><span data-stu-id="64238-395">Copy and save the name of this new Azure OS Disk.</span></span> <span data-ttu-id="64238-396">W powyższym przykładzie jest *OSDisk*.</span><span class="sxs-lookup"><span data-stu-id="64238-396">In the example above, it is *OSDisk*.</span></span>

#### <a name="data-disk-vhd-to-be-attached-to-new-azure-vm-instances"></a><span data-ttu-id="64238-397">Dane na dysku VHD jest dołączony do nowego wystąpienia maszyny Wirtualnej Azure</span><span class="sxs-lookup"><span data-stu-id="64238-397">Data disk VHD to be attached to new Azure VM instance(s)</span></span>
<span data-ttu-id="64238-398">Po przekazaniu danych dysk VHD do konta magazynu, zarejestruj go jako dysk danych Azure, dzięki czemu będzie można dołączyć do nowej serii DS, DSv2 serii lub wystąpienie maszyny Wirtualnej Azure serii GS.</span><span class="sxs-lookup"><span data-stu-id="64238-398">After the data disk VHD is uploaded to storage account, register it as an Azure Data Disk so that it can be attached to your new DS Series, DSv2 series or GS Series Azure VM instance.</span></span>

<span data-ttu-id="64238-399">Aby zarejestrować dysk VHD jako dysk danych Azure, użyj tych poleceń cmdlet programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="64238-399">Use these PowerShell cmdlets to register your VHD as an Azure Data Disk.</span></span> <span data-ttu-id="64238-400">Podaj adres URL kontenera pełną, gdzie wirtualnego dysku twardego został skopiowany do.</span><span class="sxs-lookup"><span data-stu-id="64238-400">Provide the complete container URL where VHD was copied to.</span></span>

```powershell
Add-AzureDisk -DiskName "DataDisk" -MediaLocation "https://storageaccount.blob.core.windows.net/vhdcontainer/datadisk.vhd" -Label "My Data Disk"
```

<span data-ttu-id="64238-401">Skopiuj i Zapisz nazwę tego nowego dysku danych Azure.</span><span class="sxs-lookup"><span data-stu-id="64238-401">Copy and save the name of this new Azure Data Disk.</span></span> <span data-ttu-id="64238-402">W powyższym przykładzie jest *DataDisk*.</span><span class="sxs-lookup"><span data-stu-id="64238-402">In the example above, it is *DataDisk*.</span></span>

### <a name="create-a-premium-storage-capable-vm"></a><span data-ttu-id="64238-403">Tworzenie maszyny Wirtualnej obsługuje magazyn w warstwie Premium</span><span class="sxs-lookup"><span data-stu-id="64238-403">Create a Premium Storage capable VM</span></span>
<span data-ttu-id="64238-404">Raz obrazu systemu operacyjnego lub dysku systemu operacyjnego są rejestrowane, tworzenie nowej serii DS, dsv2 lub GS-series maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="64238-404">Once the OS image or OS disk are registered, create a new DS-series, DSv2-series or GS-series VM.</span></span> <span data-ttu-id="64238-405">Będziesz używać obrazu systemu operacyjnego lub nazwa dysku systemu operacyjnego, który został zarejestrowany.</span><span class="sxs-lookup"><span data-stu-id="64238-405">You will be using the operating system image or operating system disk name that you registered.</span></span> <span data-ttu-id="64238-406">Wybierz typ maszyny Wirtualnej z warstwy Premium Storage.</span><span class="sxs-lookup"><span data-stu-id="64238-406">Select the VM type from the Premium Storage tier.</span></span> <span data-ttu-id="64238-407">W poniższym przykładzie użyto *Standard_DS2* rozmiar maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="64238-407">In example below, we are using the *Standard_DS2* VM size.</span></span>

> [!NOTE]
> <span data-ttu-id="64238-408">Zaktualizuj rozmiar dysku do upewnij się, że jest on zgodny wydajność i wymagania dotyczące wydajności i rozmiary dysku platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="64238-408">Update the disk size to make sure it matches your capacity and performance requirements and the available Azure disk sizes.</span></span>
>
>

<span data-ttu-id="64238-409">Wykonaj krok po kroku poleceń cmdlet programu PowerShell poniżej, aby utworzyć nową maszynę Wirtualną.</span><span class="sxs-lookup"><span data-stu-id="64238-409">Follow the step by step PowerShell cmdlets below to create the new VM.</span></span> <span data-ttu-id="64238-410">Najpierw należy ustawić wspólne parametry:</span><span class="sxs-lookup"><span data-stu-id="64238-410">First, set the common parameters:</span></span>

```powershell
$serviceName = "yourVM"
$location = "location-name" (e.g., West US)
$vmSize ="Standard_DS2"
$adminUser = "youradmin"
$adminPassword = "yourpassword"
$vmName ="yourVM"
$vmSize = "Standard_DS2"
```

<span data-ttu-id="64238-411">Najpierw należy utworzyć usługi w chmurze w którym będą obsługiwać nowych maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="64238-411">First, create a cloud service in which you will be hosting your new VMs.</span></span>

```powershell
New-AzureService -ServiceName $serviceName -Location $location
```

<span data-ttu-id="64238-412">Następnie w zależności od scenariusza, należy utworzyć wystąpienie maszyny Wirtualnej platformy Azure z obrazu systemu operacyjnego lub dysku systemu operacyjnego, który został zarejestrowany.</span><span class="sxs-lookup"><span data-stu-id="64238-412">Next, depending on your scenario, create the Azure VM instance from either the OS Image or OS Disk that you registered.</span></span>

#### <a name="generalized-operating-system-vhd-to-create-multiple-azure-vm-instances"></a><span data-ttu-id="64238-413">Uogólniony wirtualny dysk twardy systemu operacyjnego do utworzenia wielu wystąpień maszyny Wirtualnej Azure</span><span class="sxs-lookup"><span data-stu-id="64238-413">Generalized Operating System VHD to create multiple Azure VM instances</span></span>
<span data-ttu-id="64238-414">Utwórz co najmniej jeden nowej maszyny Wirtualnej Azure serii DS wystąpienia przy użyciu **obrazu systemu operacyjnego Azure** który został zarejestrowany.</span><span class="sxs-lookup"><span data-stu-id="64238-414">Create the one or more new DS Series Azure VM instances using the **Azure OS Image** that you registered.</span></span> <span data-ttu-id="64238-415">Określ nazwę tego obrazu systemu operacyjnego w konfiguracji maszyny Wirtualnej, podczas tworzenia nowej maszyny Wirtualnej, jak pokazano poniżej.</span><span class="sxs-lookup"><span data-stu-id="64238-415">Specify this OS Image name in the VM configuration when creating new VM as shown below.</span></span>

```powershell
$OSImage = Get-AzureVMImage –ImageName "OSImageName"

$vm = New-AzureVMConfig -Name $vmName –InstanceSize $vmSize -ImageName $OSImage.ImageName

Add-AzureProvisioningConfig -Windows –AdminUserName $adminUser -Password $adminPassword –VM $vm

New-AzureVM -ServiceName $serviceName -VM $vm
```

#### <a name="unique-operating-system-vhd-to-create-a-single-azure-vm-instance"></a><span data-ttu-id="64238-416">Unikatowy wirtualnego dysku twardego systemu operacyjnego można utworzyć jedno wystąpienie maszyny Wirtualnej Azure</span><span class="sxs-lookup"><span data-stu-id="64238-416">Unique Operating System VHD to create a single Azure VM instance</span></span>
<span data-ttu-id="64238-417">Tworzenie nowego DS serii maszyny Wirtualnej Azure wystąpienia przy użyciu **dysk systemu operacyjnego Azure** który został zarejestrowany.</span><span class="sxs-lookup"><span data-stu-id="64238-417">Create a new DS series Azure VM instance using the **Azure OS Disk** that you registered.</span></span> <span data-ttu-id="64238-418">Określ nazwę tego dysku systemu operacyjnego w konfiguracji maszyny Wirtualnej, podczas tworzenia nowej maszyny Wirtualnej, jak pokazano poniżej.</span><span class="sxs-lookup"><span data-stu-id="64238-418">Specify this OS Disk name in the VM configuration when creating the new VM as shown below.</span></span>

```powershell
$OSDisk = Get-AzureDisk –DiskName "OSDisk"

$vm = New-AzureVMConfig -Name $vmName -InstanceSize $vmSize -DiskName $OSDisk.DiskName

New-AzureVM -ServiceName $serviceName –VM $vm
```

<span data-ttu-id="64238-419">Określ inne informacje maszyny Wirtualnej platformy Azure, takich jak usługi w chmurze, region, konta magazynu, zestawu dostępności i zasad buforowania.</span><span class="sxs-lookup"><span data-stu-id="64238-419">Specify other Azure VM information, such as a cloud service, region, storage account, availability set, and caching policy.</span></span> <span data-ttu-id="64238-420">Należy pamiętać, że wystąpienie maszyny Wirtualnej musi być wspólnie z skojarzonego z nim systemu operacyjnego lub dysków danych, wybrana chmura konto usługi, regionu i magazynu musi być w tej samej lokalizacji co podstawowych dysków VHD tych dysków.</span><span class="sxs-lookup"><span data-stu-id="64238-420">Note that the VM instance must be co-located with associated operating system or data disks, so the selected cloud service, region and storage account must all be in the same location as the underlying VHDs of those disks.</span></span>

### <a name="attach-data-disk"></a><span data-ttu-id="64238-421">Dołączanie dysku danych</span><span class="sxs-lookup"><span data-stu-id="64238-421">Attach data disk</span></span>
<span data-ttu-id="64238-422">Ponadto jeśli zarejestrowano danych dysku VHD, dołącz je do nowy magazyn w warstwie Premium obsługuje maszyny Wirtualnej Azure.</span><span class="sxs-lookup"><span data-stu-id="64238-422">Lastly, if you have registered data disk VHDs, attach them to the new Premium Storage capable Azure VM.</span></span>

<span data-ttu-id="64238-423">Skorzystaj z następujących polecenia cmdlet programu PowerShell dołączyć dysku danych do nowej maszyny Wirtualnej i określ zasad buforowania.</span><span class="sxs-lookup"><span data-stu-id="64238-423">Use following PowerShell cmdlet to attach data disk to the new VM and specify the caching policy.</span></span> <span data-ttu-id="64238-424">W poniższym przykładzie ustawiono zasad buforowania *tylko do odczytu*.</span><span class="sxs-lookup"><span data-stu-id="64238-424">In example below the caching policy is set to *ReadOnly*.</span></span>

```powershell
$vm = Get-AzureVM -ServiceName $serviceName -Name $vmName

Add-AzureDataDisk -ImportFrom -DiskName "DataDisk" -LUN 0 –HostCaching ReadOnly –VM $vm

Update-AzureVM  -VM $vm
```

> [!NOTE]
> <span data-ttu-id="64238-425">Mogą istnieć dodatkowe kroki niezbędne do obsługi tej aplikacji, która jest nie obejmuje się w tym przewodniku.</span><span class="sxs-lookup"><span data-stu-id="64238-425">There may be additional steps necessary to support your application that is not be covered by this guide.</span></span>
>
>

### <a name="checking-and-plan-backup"></a><span data-ttu-id="64238-426">Sprawdzanie i Planowanie tworzenia kopii zapasowej</span><span class="sxs-lookup"><span data-stu-id="64238-426">Checking and plan backup</span></span>
<span data-ttu-id="64238-427">Po nowa maszyna wirtualna jest uruchomiona, dostęp do niego przy użyciu tego samego identyfikatora logowania i hasła jest co oryginalna maszyna wirtualna i sprawdź, czy że wszystko działa zgodnie z oczekiwaniami.</span><span class="sxs-lookup"><span data-stu-id="64238-427">Once the new VM is up and running, access it using the same login id and password is as the original VM, and verify that everything is working as expected.</span></span> <span data-ttu-id="64238-428">Wszystkie ustawienia, w tym woluminy rozłożone będą obecne w nowej maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="64238-428">All the settings, including the striped volumes, would be present in the new VM.</span></span>

<span data-ttu-id="64238-429">Ostatnim krokiem jest planowanie tworzenia kopii zapasowej i harmonogram konserwacji dla nowej maszyny Wirtualnej na podstawie potrzeb aplikacji.</span><span class="sxs-lookup"><span data-stu-id="64238-429">The last step is to plan backup and maintenance schedule for the new VM based on the application's needs.</span></span>

### <span data-ttu-id="64238-430"><a name="a-sample-migration-script"></a>Przykładowy skrypt migracji</span><span class="sxs-lookup"><span data-stu-id="64238-430"><a name="a-sample-migration-script"></a>A sample migration script</span></span>
<span data-ttu-id="64238-431">Jeśli masz wiele maszyn wirtualnych do migracji automatyzacji za pomocą skryptów środowiska PowerShell będą przydatne.</span><span class="sxs-lookup"><span data-stu-id="64238-431">If you have multiple VMs to migrate, automation through PowerShell scripts will be helpful.</span></span> <span data-ttu-id="64238-432">Oto przykładowy skrypt, który zautomatyzuje migracji maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="64238-432">Following is a sample script that automates the migration of a VM.</span></span> <span data-ttu-id="64238-433">Uwaga poniżej skryptu jest tylko przykładem i istnieje kilka założeniom o bieżącym dysków maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="64238-433">Note that below script is only an example, and there are few assumptions made about the current VM disks.</span></span> <span data-ttu-id="64238-434">Może być konieczne zaktualizowanie skryptu pasuje do konkretnego scenariusza.</span><span class="sxs-lookup"><span data-stu-id="64238-434">You may need to update the script to match with your specific scenario.</span></span>

<span data-ttu-id="64238-435">Założeń są:</span><span class="sxs-lookup"><span data-stu-id="64238-435">The assumptions are:</span></span>

* <span data-ttu-id="64238-436">Tworzysz klasycznych maszyn wirtualnych platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="64238-436">You are creating classic Azure VMs.</span></span>
* <span data-ttu-id="64238-437">Źródła dysków systemu operacyjnego i dysków danych źródłowych znajdują się w tym samym koncie magazynu i tego samego kontenera.</span><span class="sxs-lookup"><span data-stu-id="64238-437">Your source OS Disks and source Data Disks are in same storage account and same container.</span></span> <span data-ttu-id="64238-438">Dysków systemu operacyjnego i dysków z danymi nie są w tym samym miejscu, aby skopiować wirtualne dyski twarde za pośrednictwem konta magazynu i kontenery można użyć narzędzia AzCopy lub Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="64238-438">If your OS Disks and Data Disks are not in the same place, you can use AzCopy or Azure PowerShell to copy VHDs over storage accounts and containers.</span></span> <span data-ttu-id="64238-439">Można znaleźć w poprzednim kroku: [kopii wirtualnego dysku twardego z narzędzia AzCopy lub środowiska PowerShell](#copy-vhd-with-azcopy-or-powershell).</span><span class="sxs-lookup"><span data-stu-id="64238-439">Refer to the previous step: [Copy VHD with AzCopy or PowerShell](#copy-vhd-with-azcopy-or-powershell).</span></span> <span data-ttu-id="64238-440">Edytowanie tego skryptu w celu spełnienia danego scenariusza innym rozwiązaniem jest, ale zaleca się użycie narzędzia AzCopy lub programu PowerShell, ponieważ jest łatwiejsze i szybsze.</span><span class="sxs-lookup"><span data-stu-id="64238-440">Editing this script to meet your scenario is another choice, but we recommend using AzCopy or PowerShell since it is easier and faster.</span></span>

<span data-ttu-id="64238-441">Skrypt automatyzacji podano poniżej.</span><span class="sxs-lookup"><span data-stu-id="64238-441">The automation script is provided below.</span></span> <span data-ttu-id="64238-442">Zastąp tekst z informacjami i zaktualizować ten skrypt, aby dopasować z konkretnego scenariusza.</span><span class="sxs-lookup"><span data-stu-id="64238-442">Replace text with your information and update the script to match with your specific scenario.</span></span>

> [!NOTE]
> <span data-ttu-id="64238-443">Przy użyciu istniejącego skryptu nie zachowa konfiguracji sieci źródła maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="64238-443">Using the existing script does not preserve the network configuration of your source VM.</span></span> <span data-ttu-id="64238-444">Konieczne będzie ponowna konfiguracja ustawień sieciowych na zmigrowanych maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="64238-444">You will need to re-config the networking settings on your migrated VMs.</span></span>
>
>

```
    <#
    .Synopsis
    This script is provided as an EXAMPLE to show how to migrate a VM from a standard storage account to a premium storage account. You can customize it according to your specific requirements.

    .Description
    The script will copy the vhds (page blobs) of the source VM to the new storage account.
    And then it will create a new VM from these copied vhds based on the inputs that you specified for the new VM.
    You can modify the script to satisfy your specific requirement, but please be aware of the items specified
    in the Terms of Use section.

    .Terms of Use
    Copyright © 2015 Microsoft Corporation.  All rights reserved.

    THIS CODE AND ANY ASSOCIATED INFORMATION ARE PROVIDED "AS IS" WITHOUT WARRANTY OF ANY KIND,
    EITHER EXPRESSED OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE IMPLIED WARRANTIES OF MERCHANTABILITY
    AND/OR FITNESS FOR A PARTICULAR PURPOSE. THE ENTIRE RISK OF USE, INABILITY TO USE, OR
    RESULTS FROM THE USE OF THIS CODE REMAINS WITH THE USER.

    .Example (Save this script as Migrate-AzureVM.ps1)

    .\Migrate-AzureVM.ps1 -SourceServiceName CurrentServiceName -SourceVMName CurrentVMName –DestStorageAccount newpremiumstorageaccount -DestServiceName NewServiceName -DestVMName NewDSVMName -DestVMSize "Standard_DS2" –Location "Southeast Asia"

    .Link
    To find more information about how to set up Azure PowerShell, refer to the following links.
    http://azure.microsoft.com/documentation/articles/powershell-install-configure/
    http://azure.microsoft.com/documentation/articles/storage-powershell-guide-full/
    http://azure.microsoft.com/blog/2014/10/22/migrate-azure-virtual-machines-between-storage-accounts/

    #>

    Param(
    # the cloud service name of the VM.
    [Parameter(Mandatory = $true)]
    [string] $SourceServiceName,

    # The VM name to copy.
    [Parameter(Mandatory = $true)]
    [String] $SourceVMName,

    # The destination storage account name.
    [Parameter(Mandatory = $true)]
    [String] $DestStorageAccount,

    # The destination cloud service name
    [Parameter(Mandatory = $true)]
    [String] $DestServiceName,

    # the destination vm name
    [Parameter(Mandatory = $true)]
    [String] $DestVMName,

    # the destination vm size
    [Parameter(Mandatory = $true)]
    [String] $DestVMSize,

    # the location of destination VM.
    [Parameter(Mandatory = $true)]
    [string] $Location,

    # whether or not to copy the os disk, the default is only copy data disks
    [Parameter(Mandatory = $false)]
    [Bool] $DataDiskOnly = $true,

    # how frequently to report the copy status in sceconds
    [Parameter(Mandatory = $false)]
    [Int32] $CopyStatusReportInterval = 15,

    # the name suffix to add to new created disks to avoid conflict with source disk names
    [Parameter(Mandatory = $false)]
    [String]$DiskNameSuffix = "-prem"

    ) #end param

    #######################################################################
    #  Verify Azure PowerShell module and version
    #######################################################################

    #import the Azure PowerShell module
    Write-Host "`n[WORKITEM] - Importing Azure PowerShell module" -ForegroundColor Yellow
    $azureModule = Import-Module Azure -PassThru

    if ($azureModule -ne $null)
    {
        Write-Host "`tSuccess" -ForegroundColor Green
    }
    else
    {
        #show module not found interaction and bail out
        Write-Host "[ERROR] - PowerShell module not found. Exiting." -ForegroundColor Red
        Exit
    }


    #Check the Azure PowerShell module version
    Write-Host "`n[WORKITEM] - Checking Azure PowerShell module verion" -ForegroundColor Yellow
    If ($azureModule.Version -ge (New-Object System.Version -ArgumentList "0.8.14"))
    {
        Write-Host "`tSuccess" -ForegroundColor Green
    }
    Else
    {
        Write-Host "[ERROR] - Azure PowerShell module must be version 0.8.14 or higher. Exiting." -ForegroundColor Red
        Exit
    }

    #Check if there is an azure subscription set up in PowerShell
    Write-Host "`n[WORKITEM] - Checking Azure Subscription" -ForegroundColor Yellow
    $currentSubs = Get-AzureSubscription -Current
    if ($currentSubs -ne $null)
    {
        Write-Host "`tSuccess" -ForegroundColor Green
        Write-Host "`tYour current azure subscription in PowerShell is $($currentSubs.SubscriptionName)." -ForegroundColor Green
    }
    else
    {
        Write-Host "[ERROR] - There is no valid Azure subscription found in PowerShell. Please refer to this article http://azure.microsoft.com/documentation/articles/powershell-install-configure/ to connect an Azure subscription. Exiting." -ForegroundColor Red
        Exit
    }


    #######################################################################
    #  Check if the VM is shut down
    #  Stopping the VM is a required step so that the file system is consistent when you do the copy operation.
    #  Azure does not support live migration at this time..
    #######################################################################

    if (($sourceVM = Get-AzureVM –ServiceName $SourceServiceName –Name $SourceVMName) -eq $null)
    {
        Write-Host "[ERROR] - The source VM doesn't exist in the current subscription. Exiting." -ForegroundColor Red
        Exit
    }

    # check if VM is shut down
    if ( $sourceVM.Status -notmatch "Stopped" )
    {
        Write-Host "[Warning] - Stopping the VM is a required step so that the file system is consistent when you do the copy operation. Azure does not support live migration at this time. If you'd like to create a VM from a generalized image, sys-prep the Virtual Machine before stopping it." -ForegroundColor Yellow
        $ContinueAnswer = Read-Host "`n`tDo you wish to stop $SourceVMName now? Input 'N' if you want to shut down the VM manually and come back later.(Y/N)"
        If ($ContinueAnswer -ne "Y") { Write-Host "`n Exiting." -ForegroundColor Red;Exit }
        $sourceVM | Stop-AzureVM

        # wait until the VM is shut down
        $VMStatus = (Get-AzureVM –ServiceName $SourceServiceName –Name $vmName).Status
        while ($VMStatus -notmatch "Stopped")
        {
            Write-Host "`n[Status] - Waiting VM $vmName to shut down" -ForegroundColor Green
            Sleep -Seconds 5
            $VMStatus = (Get-AzureVM –ServiceName $SourceServiceName –Name $vmName).Status
        }
    }

    # exporting the sourve vm to a configuration file, you can restore the original VM by importing this config file
    # see more information for Import-AzureVM
    $workingDir = (Get-Location).Path
    $vmConfigurationPath = $env:HOMEPATH + "\VM-" + $SourceVMName + ".xml"
    Write-Host "`n[WORKITEM] - Exporting VM configuration to $vmConfigurationPath" -ForegroundColor Yellow
    $exportRe = $sourceVM | Export-AzureVM -Path $vmConfigurationPath


    #######################################################################
    #  Copy the vhds of the source vm
    #  You can choose to copy all disks including os and data disks by specifying the
    #  parameter -DataDiskOnly to be $false. The default is to copy only data disk vhds
    #  and the new VM will boot from the original os disk.
    #######################################################################

    $sourceOSDisk = $sourceVM.VM.OSVirtualHardDisk
    $sourceDataDisks = $sourceVM.VM.DataVirtualHardDisks

    # Get source storage account information, not considering the data disks and os disks are in different accounts
    $sourceStorageAccountName = $sourceOSDisk.MediaLink.Host -split "\." | select -First 1
    $sourceStorageKey = (Get-AzureStorageKey -StorageAccountName $sourceStorageAccountName).Primary
    $sourceContext = New-AzureStorageContext –StorageAccountName $sourceStorageAccountName -StorageAccountKey $sourceStorageKey

    # Create destination context
    $destStorageKey = (Get-AzureStorageKey -StorageAccountName $DestStorageAccount).Primary
    $destContext = New-AzureStorageContext –StorageAccountName $DestStorageAccount -StorageAccountKey $destStorageKey

    # Create a container of vhds if it doesn't exist
    if ((Get-AzureStorageContainer -Context $destContext -Name vhds -ErrorAction SilentlyContinue) -eq $null)
    {
        Write-Host "`n[WORKITEM] - Creating a container vhds in the destination storage account." -ForegroundColor Yellow
        New-AzureStorageContainer -Context $destContext -Name vhds
    }


    $allDisksToCopy = $sourceDataDisks
    # check if need to copy os disk
    $sourceOSVHD = $sourceOSDisk.MediaLink.Segments[2]
    if ($DataDiskOnly)
    {
        # copy data disks only, this option requires deleting the source VM so that dest VM can boot
        # from the same vhd blob.
        $ContinueAnswer = Read-Host "`n`t[Warning] You chose to copy data disks only. Moving VM requires removing the original VM (the disks and backing vhd files will NOT be deleted) so that the new VM can boot from the same vhd. This is an irreversible action. Do you wish to proceed right now? (Y/N)"
        If ($ContinueAnswer -ne "Y") { Write-Host "`n Exiting." -ForegroundColor Red;Exit }
        $destOSVHD = Get-AzureStorageBlob -Blob $sourceOSVHD -Container vhds -Context $sourceContext
        Write-Host "`n[WORKITEM] - Removing the original VM (the vhd files are NOT deleted)." -ForegroundColor Yellow
        Remove-AzureVM -Name $SourceVMName -ServiceName $SourceServiceName

        Write-Host "`n[WORKITEM] - Waiting utill the OS disk is released by source VM. This may take up to several minutes."
        $diskAttachedTo = (Get-AzureDisk -DiskName $sourceOSDisk.DiskName).AttachedTo
        while ($diskAttachedTo -ne $null)
        {
            Start-Sleep -Seconds 10
            $diskAttachedTo = (Get-AzureDisk -DiskName $sourceOSDisk.DiskName).AttachedTo
        }

    }
    else
    {
        # copy the os disk vhd
        Write-Host "`n[WORKITEM] - Starting copying os disk $($disk.DiskName) at $(get-date)." -ForegroundColor Yellow
        $allDisksToCopy += @($sourceOSDisk)
        $targetBlob = Start-AzureStorageBlobCopy -SrcContainer vhds -SrcBlob $sourceOSVHD -DestContainer vhds -DestBlob $sourceOSVHD -Context $sourceContext -DestContext $destContext -Force
        $destOSVHD = $targetBlob
    }


    # Copy all data disk vhds
    # Start all async copy requests in parallel.
    foreach($disk in $sourceDataDisks)
    {
        $blobName = $disk.MediaLink.Segments[2]
        # copy all data disks
        Write-Host "`n[WORKITEM] - Starting copying data disk $($disk.DiskName) at $(get-date)." -ForegroundColor Yellow
        $targetBlob = Start-AzureStorageBlobCopy -SrcContainer vhds -SrcBlob $blobName -DestContainer vhds -DestBlob $blobName -Context $sourceContext -DestContext $destContext -Force
        # update the media link to point to the target blob link
        $disk.MediaLink = $targetBlob.ICloudBlob.Uri.AbsoluteUri
    }

    # Wait until all vhd files are copied.
    $diskComplete = @()
    do
    {
        Write-Host "`n[WORKITEM] - Waiting for all disk copy to complete. Checking status every $CopyStatusReportInterval seconds." -ForegroundColor Yellow
        # check status every 30 seconds
        Sleep -Seconds $CopyStatusReportInterval
        foreach ( $disk in $allDisksToCopy)
        {
            if ($diskComplete -contains $disk)
            {
                Continue
            }
            $blobName = $disk.MediaLink.Segments[2]
            $copyState = Get-AzureStorageBlobCopyState -Blob $blobName -Container vhds -Context $destContext
            if ($copyState.Status -eq "Success")
            {
                Write-Host "`n[Status] - Success for disk copy $($disk.DiskName) at $($copyState.CompletionTime)" -ForegroundColor Green
                $diskComplete += $disk
            }
            else
            {
                if ($copyState.TotalBytes -gt 0)
                {
                    $percent = ($copyState.BytesCopied / $copyState.TotalBytes) * 100
                    Write-Host "`n[Status] - $('{0:N2}' -f $percent)% Complete for disk copy $($disk.DiskName)" -ForegroundColor Green
                }
            }
        }
    }
    while($diskComplete.Count -lt $allDisksToCopy.Count)

    #######################################################################
    #  Create a new vm
    #  the new VM can be created from the copied disks or the original os disk.
    #  You can ddd your own logic here to satisfy your specific requirements of the vm.
    #######################################################################

    # Create a VM from the existing os disk
    if ($DataDiskOnly)
    {
        $vm = New-AzureVMConfig -Name $DestVMName -InstanceSize $DestVMSize -DiskName $sourceOSDisk.DiskName
    }
    else
    {
        $newOSDisk = Add-AzureDisk -OS $sourceOSDisk.OS -DiskName ($sourceOSDisk.DiskName + $DiskNameSuffix) -MediaLocation $destOSVHD.ICloudBlob.Uri.AbsoluteUri
        $vm = New-AzureVMConfig -Name $DestVMName -InstanceSize $DestVMSize -DiskName $newOSDisk.DiskName
    }
    # Attached the copied data disks to the new VM
    foreach ($dataDisk in $sourceDataDisks)
    {
        # add -DiskLabel $dataDisk.DiskLabel if there are labels for disks of the source vm
        $diskLabel = "drive" + $dataDisk.Lun
        $vm | Add-AzureDataDisk -ImportFrom -DiskLabel $diskLabel -LUN $dataDisk.Lun -MediaLocation $dataDisk.MediaLink
    }

    # Edit this if you want to add more custimization to the new VM
    # $vm | Add-AzureEndpoint -Protocol tcp -LocalPort 443 -PublicPort 443 -Name 'HTTPs'
    # $vm | Set-AzureSubnet "PubSubnet","PrivSubnet"

    New-AzureVM -ServiceName $DestServiceName -VMs $vm -Location $Location
```

#### <span data-ttu-id="64238-445"><a name="optimization"></a>Optymalizacja</span><span class="sxs-lookup"><span data-stu-id="64238-445"><a name="optimization"></a>Optimization</span></span>
<span data-ttu-id="64238-446">Bieżąca konfiguracja maszyny Wirtualnej można dostosować w szczególności do pracy ze standardowych dysków.</span><span class="sxs-lookup"><span data-stu-id="64238-446">Your current VM configuration may be customized specifically to work well with Standard disks.</span></span> <span data-ttu-id="64238-447">Na przykład aby zwiększyć wydajność przy użyciu wielu dysków w woluminy rozłożone.</span><span class="sxs-lookup"><span data-stu-id="64238-447">For instance, to increase the performance by using many disks in a striped volume.</span></span> <span data-ttu-id="64238-448">Na przykład zamiast 4 dyski osobno na magazyn w warstwie Premium, można zoptymalizować koszt przez jednego dysku.</span><span class="sxs-lookup"><span data-stu-id="64238-448">For example, instead of using 4 disks separately on Premium Storage, you may be able to optimize the cost by having a single disk.</span></span> <span data-ttu-id="64238-449">Optymalizacje takie jak konieczność obsługi na podstawie przypadku i wymagają niestandardowej czynności po migracji.</span><span class="sxs-lookup"><span data-stu-id="64238-449">Optimizations like this need to be handled on a case by case basis and require custom steps after the migration.</span></span> <span data-ttu-id="64238-450">Należy również zauważyć, że ten proces może nie również działać dla baz danych i aplikacji, które są zależne od zdefiniowany w ustawieniach układu dysku.</span><span class="sxs-lookup"><span data-stu-id="64238-450">Also, note that this process may not well work for databases and applications that depend on the disk layout defined in the setup.</span></span>

##### <a name="preparation"></a><span data-ttu-id="64238-451">Przygotowanie</span><span class="sxs-lookup"><span data-stu-id="64238-451">Preparation</span></span>
1. <span data-ttu-id="64238-452">Wykonaj proste migracji, zgodnie z opisem w we wcześniejszej sekcji.</span><span class="sxs-lookup"><span data-stu-id="64238-452">Complete the Simple Migration as described in the earlier section.</span></span> <span data-ttu-id="64238-453">Optymalizacje odbędzie się w nowej maszyny Wirtualnej po migracji.</span><span class="sxs-lookup"><span data-stu-id="64238-453">Optimizations will be performed on the new VM after the migration.</span></span>
2. <span data-ttu-id="64238-454">Zdefiniuj nowe rozmiary dysku wymagane do konfiguracji zoptymalizowane.</span><span class="sxs-lookup"><span data-stu-id="64238-454">Define the new disk sizes needed for the optimized configuration.</span></span>
3. <span data-ttu-id="64238-455">Należy określić mapowanie bieżącego dysków/woluminów do specyfikacji nowego dysku.</span><span class="sxs-lookup"><span data-stu-id="64238-455">Determine mapping of the current disks/volumes to the new disk specifications.</span></span>

##### <a name="execution-steps"></a><span data-ttu-id="64238-456">Wykonanie czynności</span><span class="sxs-lookup"><span data-stu-id="64238-456">Execution steps</span></span>
1. <span data-ttu-id="64238-457">Utwórz nowe dyski o odpowiednim rozmiarze na Maszynie wirtualnej — wersja Premium magazynu.</span><span class="sxs-lookup"><span data-stu-id="64238-457">Create the new disks with the right sizes on the Premium Storage VM.</span></span>
2. <span data-ttu-id="64238-458">Zaloguj się do maszyny Wirtualnej i kopiowania danych z bieżącego woluminu na nowy dysk, który jest mapowany na tym woluminie.</span><span class="sxs-lookup"><span data-stu-id="64238-458">Login to the VM and copy the data from the current volume to the new disk that maps to that volume.</span></span> <span data-ttu-id="64238-459">W tym wszystkie woluminy bieżącego, które należy mapować na nowy dysk.</span><span class="sxs-lookup"><span data-stu-id="64238-459">Do this for all the current volumes that need to map to a new disk.</span></span>
3. <span data-ttu-id="64238-460">Następnie zmienić ustawienia aplikacji, aby przełączyć się do nowych dysków i odłączyć starszych woluminów.</span><span class="sxs-lookup"><span data-stu-id="64238-460">Next, change the application settings to switch to the new disks, and detach the old volumes.</span></span>

<span data-ttu-id="64238-461">Dostrajanie aplikacji w celu zapewnienia lepszej wydajności dysku, można znaleźć na stronie [optymalizacji wydajności aplikacji](storage-premium-storage-performance.md#optimizing-application-performance).</span><span class="sxs-lookup"><span data-stu-id="64238-461">For tuning the application for better disk performance, please refer to [Optimizing Application Performance](storage-premium-storage-performance.md#optimizing-application-performance).</span></span>

### <a name="application-migrations"></a><span data-ttu-id="64238-462">Migracja aplikacji</span><span class="sxs-lookup"><span data-stu-id="64238-462">Application migrations</span></span>
<span data-ttu-id="64238-463">Baz danych i innych złożonych aplikacji może wymagać specjalne kroki zgodnie z definicją w dostawcy aplikacji do migracji.</span><span class="sxs-lookup"><span data-stu-id="64238-463">Databases and other complex applications may require special steps as defined by the application provider for the migration.</span></span> <span data-ttu-id="64238-464">Zapoznaj się z dokumentacją odpowiedniej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="64238-464">Please refer to respective application documentation.</span></span> <span data-ttu-id="64238-465">Na przykład</span><span class="sxs-lookup"><span data-stu-id="64238-465">E.g.</span></span> <span data-ttu-id="64238-466">zwykle baz danych można poddać migracji za pomocą kopii zapasowej i przywracania.</span><span class="sxs-lookup"><span data-stu-id="64238-466">typically databases can be migrated through backup and restore.</span></span>

## <a name="next-steps"></a><span data-ttu-id="64238-467">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="64238-467">Next steps</span></span>
<span data-ttu-id="64238-468">Zobacz następujące zasoby w określonych scenariuszach migracji maszyn wirtualnych:</span><span class="sxs-lookup"><span data-stu-id="64238-468">See the following resources for specific scenarios for migrating virtual machines:</span></span>

* [<span data-ttu-id="64238-469">Migrowanie maszyn wirtualnych platformy Azure między kontami magazynu</span><span class="sxs-lookup"><span data-stu-id="64238-469">Migrate Azure Virtual Machines between Storage Accounts</span></span>](https://azure.microsoft.com/blog/2014/10/22/migrate-azure-virtual-machines-between-storage-accounts/)
* [<span data-ttu-id="64238-470">Tworzenie i przekazywanie wirtualnego dysku twardego serwera Windows Azure.</span><span class="sxs-lookup"><span data-stu-id="64238-470">Create and upload a Windows Server VHD to Azure.</span></span>](../../virtual-machines/windows/classic/createupload-vhd.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)
* [<span data-ttu-id="64238-471">Tworzenie i przekazywanie wirtualnego dysku twardego, który zawiera System operacyjny Linux</span><span class="sxs-lookup"><span data-stu-id="64238-471">Creating and Uploading a Virtual Hard Disk that Contains the Linux Operating System</span></span>](../../virtual-machines/linux/classic/create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)
* [<span data-ttu-id="64238-472">Migrowanie maszyn wirtualnych z Amazon usług AWS na platformie Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="64238-472">Migrating Virtual Machines from Amazon AWS to Microsoft Azure</span></span>](http://channel9.msdn.com/Series/Migrating-Virtual-Machines-from-Amazon-AWS-to-Microsoft-Azure)

<span data-ttu-id="64238-473">Zobacz też następujące zasoby, aby dowiedzieć się więcej na temat usługi Azure Storage i maszyn wirtualnych platformy Azure:</span><span class="sxs-lookup"><span data-stu-id="64238-473">Also, see the following resources to learn more about Azure Storage and Azure Virtual Machines:</span></span>

* [<span data-ttu-id="64238-474">Azure Storage</span><span class="sxs-lookup"><span data-stu-id="64238-474">Azure Storage</span></span>](https://azure.microsoft.com/documentation/services/storage/)
* [<span data-ttu-id="64238-475">Maszyny wirtualne platformy Azure</span><span class="sxs-lookup"><span data-stu-id="64238-475">Azure Virtual Machines</span></span>](https://azure.microsoft.com/documentation/services/virtual-machines/)
* [<span data-ttu-id="64238-476">Premium Storage: magazyn o wysokiej wydajności dla obciążeń maszyn wirtualnych platformy Azure</span><span class="sxs-lookup"><span data-stu-id="64238-476">Premium Storage: High-Performance Storage for Azure Virtual Machine Workloads</span></span>](storage-premium-storage.md)

[1]:./media/storage-migration-to-premium-storage/migration-to-premium-storage-1.png
[2]:./media/storage-migration-to-premium-storage/migration-to-premium-storage-1.png
[3]:./media/storage-migration-to-premium-storage/migration-to-premium-storage-3.png
[4]: http://technet.microsoft.com/library/hh831739.aspx
