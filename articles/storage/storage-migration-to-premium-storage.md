---
title: aaaMigrating maszyn wirtualnych tooAzure magazyn w warstwie Premium | Dokumentacja firmy Microsoft
description: "Migrowanie istniejących tooAzure maszyn wirtualnych magazyn w warstwie Premium. Magazyn w warstwie Premium oferuje obsługę dysków o wysokiej wydajności i małych opóźnieniach/O wykonujących obciążeń uruchomionych na maszynach wirtualnych platformy Azure."
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
ms.openlocfilehash: cd812bdbe39f43fe053a998d96788045d5a43258
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="migrating-tooazure-premium-storage-unmanaged-disks"></a><span data-ttu-id="253eb-104">Migrowanie tooAzure magazyn w warstwie Premium (niezarządzany dysków)</span><span class="sxs-lookup"><span data-stu-id="253eb-104">Migrating tooAzure Premium Storage (Unmanaged Disks)</span></span>

> [!NOTE]
> <span data-ttu-id="253eb-105">W tym artykule opisano, jak toomigrate maszynę Wirtualną, która używa tooa niezarządzane standardowych dysków maszyny Wirtualnej używającej niezarządzanych dysków premium.</span><span class="sxs-lookup"><span data-stu-id="253eb-105">This article discusses how toomigrate a VM that uses unmanaged standard disks tooa VM that uses unmanaged premium disks.</span></span> <span data-ttu-id="253eb-106">Zaleca się używać dysków zarządzanych Azure dla maszyn wirtualnych i przekonwertowanie poprzedniej dysków toomanaged niezarządzane dysków.</span><span class="sxs-lookup"><span data-stu-id="253eb-106">We recommend that you use Azure Managed Disks for new VMs, and that you convert your previous unmanaged disks toomanaged disks.</span></span> <span data-ttu-id="253eb-107">Zarządzane dyski dojścia hello źródłowego magazynu konta, dzięki czemu nie trzeba.</span><span class="sxs-lookup"><span data-stu-id="253eb-107">Managed Disks handle hello underlying storage accounts so you don't have to.</span></span> <span data-ttu-id="253eb-108">Aby uzyskać więcej informacji, zobacz nasze [omówienie dysków zarządzanych](storage-managed-disks-overview.md).</span><span class="sxs-lookup"><span data-stu-id="253eb-108">For more information, please see our [Managed Disks Overview](storage-managed-disks-overview.md).</span></span>
>

<span data-ttu-id="253eb-109">Usługa Azure Premium Storage oferuje obsługę wysokiej wydajności i małych opóźnieniach dysku dla maszyn wirtualnych uruchomionych/O wykonujących obciążeń.</span><span class="sxs-lookup"><span data-stu-id="253eb-109">Azure Premium Storage delivers high-performance, low-latency disk support for virtual machines running I/O-intensive workloads.</span></span> <span data-ttu-id="253eb-110">Zaletą hello szybkości i wydajności tych dysków może potrwać przy użyciu funkcji migracji aplikacji maszyny Wirtualnej dyski tooAzure magazyn w warstwie Premium.</span><span class="sxs-lookup"><span data-stu-id="253eb-110">You can take advantage of hello speed and performance of these disks by migrating your application's VM disks tooAzure Premium Storage.</span></span>

<span data-ttu-id="253eb-111">przeznaczenie tego przewodnika Hello jest toohelp nowych użytkowników usługi Azure Premium Storage lepsze przygotowanie toomake przejścia z ich bieżącej tooPremium systemu magazynowania.</span><span class="sxs-lookup"><span data-stu-id="253eb-111">hello purpose of this guide is toohelp new users of Azure Premium Storage better prepare toomake a smooth transition from their current system tooPremium Storage.</span></span> <span data-ttu-id="253eb-112">Przewodnik Hello adresów trzy najważniejsze składniki hello tego procesu:</span><span class="sxs-lookup"><span data-stu-id="253eb-112">hello guide addresses three of hello key components in this process:</span></span>

* [<span data-ttu-id="253eb-113">Planowanie hello tooPremium migracji magazynu</span><span class="sxs-lookup"><span data-stu-id="253eb-113">Plan for hello Migration tooPremium Storage</span></span>](#plan-the-migration-to-premium-storage)
* [<span data-ttu-id="253eb-114">Przygotowanie i tooPremium kopiowania wirtualnych dysków twardych (VHD) magazynu</span><span class="sxs-lookup"><span data-stu-id="253eb-114">Prepare and Copy Virtual Hard Disks (VHDs) tooPremium Storage</span></span>](#prepare-and-copy-virtual-hard-disks-VHDs-to-premium-storage)
* [<span data-ttu-id="253eb-115">Utwórz maszynę wirtualną platformy Azure przy użyciu magazyn w warstwie Premium</span><span class="sxs-lookup"><span data-stu-id="253eb-115">Create Azure Virtual Machine using Premium Storage</span></span>](#create-azure-virtual-machine-using-premium-storage)

<span data-ttu-id="253eb-116">Można dokonać migracji maszyn wirtualnych z innych platform tooAzure magazyn w warstwie Premium lub migracji istniejących maszyn wirtualnych platformy Azure z magazynu w warstwie standardowa tooPremium magazynu.</span><span class="sxs-lookup"><span data-stu-id="253eb-116">You can either migrate VMs from other platforms tooAzure Premium Storage or migrate existing Azure VMs from Standard Storage tooPremium Storage.</span></span> <span data-ttu-id="253eb-117">W tym przewodniku opisano kroki dla obu dwa scenariusze.</span><span class="sxs-lookup"><span data-stu-id="253eb-117">This guide covers steps for both two scenarios.</span></span> <span data-ttu-id="253eb-118">Wykonaj kroki hello określone w odpowiedniej sekcji hello w zależności od danego scenariusza.</span><span class="sxs-lookup"><span data-stu-id="253eb-118">Follow hello steps specified in hello relevant section depending on your scenario.</span></span>

> [!NOTE]
> <span data-ttu-id="253eb-119">Omówienie funkcji i cenowych Premium magazynu w warstwie Premium Storage można znaleźć: [magazynu o wysokiej wydajności dla obciążeń maszyny wirtualnej Azure](storage-premium-storage.md).</span><span class="sxs-lookup"><span data-stu-id="253eb-119">You can find a feature overview and pricing of Premium Storage in Premium Storage: [High-Performance Storage for Azure Virtual Machine Workloads](storage-premium-storage.md).</span></span> <span data-ttu-id="253eb-120">Zaleca się migrowanie dyskami maszyny wirtualnej wymagające wysokiej tooAzure IOPS magazyn w warstwie Premium hello najlepszą wydajność aplikacji.</span><span class="sxs-lookup"><span data-stu-id="253eb-120">We recommend migrating any virtual machine disk requiring high IOPS tooAzure Premium Storage for hello best performance for your application.</span></span> <span data-ttu-id="253eb-121">Jeśli dysk nie wymaga wysokiej IOPS, przechowując go w Standard Storage, która przechowuje dane dysku maszyny wirtualnej na stacje dysków twardych (HDD) zamiast dysków SSD można ograniczyć koszty.</span><span class="sxs-lookup"><span data-stu-id="253eb-121">If your disk does not require high IOPS, you can limit costs by maintaining it in Standard Storage, which stores virtual machine disk data on Hard Disk Drives (HDDs) instead of SSDs.</span></span>
>

<span data-ttu-id="253eb-122">Kończenie procesu migracji hello w całości może wymagać dodatkowych akcji przed i po hello z krokami opisanymi w tym przewodniku.</span><span class="sxs-lookup"><span data-stu-id="253eb-122">Completing hello migration process in its entirety may require additional actions both before and after hello steps provided in this guide.</span></span> <span data-ttu-id="253eb-123">Przykładami konfigurowania sieci wirtualnych lub punktów końcowych lub wprowadzania zmian w kodzie aplikacji hello sam wymagające przestój w aplikacji.</span><span class="sxs-lookup"><span data-stu-id="253eb-123">Examples include configuring virtual networks or endpoints or making code changes within hello application itself which may require some downtime in your application.</span></span> <span data-ttu-id="253eb-124">Te akcje są unikatowe tooeach aplikacji i należy je ukończyć wraz z hello z krokami opisanymi w tej przewodnik toomake hello pełne przejście tooPremium magazynu jako bezproblemowe, jak to możliwe.</span><span class="sxs-lookup"><span data-stu-id="253eb-124">These actions are unique tooeach application, and you should complete them along with hello steps provided in this guide toomake hello full transition tooPremium Storage as seamless as possible.</span></span>

## <span data-ttu-id="253eb-125"><a name="plan-the-migration-to-premium-storage"></a>Planowanie hello tooPremium migracji magazynu</span><span class="sxs-lookup"><span data-stu-id="253eb-125"><a name="plan-the-migration-to-premium-storage"></a>Plan for hello migration tooPremium Storage</span></span>
<span data-ttu-id="253eb-126">W tej sekcji gwarantuje, że są gotowe toofollow hello kroki migracji opisane w tym artykule i ułatwia toomake hello najlepszych decyzji w typach maszyny Wirtualnej i dysku.</span><span class="sxs-lookup"><span data-stu-id="253eb-126">This section ensures that you are ready toofollow hello migration steps in this article, and helps you toomake hello best decision on VM and Disk types.</span></span>

### <a name="prerequisites"></a><span data-ttu-id="253eb-127">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="253eb-127">Prerequisites</span></span>
* <span data-ttu-id="253eb-128">Konieczne będzie subskrypcji platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="253eb-128">You will need an Azure subscription.</span></span> <span data-ttu-id="253eb-129">Jeśli nie masz, możesz utworzyć jeden miesiąc [bezpłatnej wersji próbnej](https://azure.microsoft.com/pricing/free-trial/) subskrypcji lub odwiedź stronę [cennik usługi Azure](https://azure.microsoft.com/pricing/) wyświetlić więcej opcji.</span><span class="sxs-lookup"><span data-stu-id="253eb-129">If you don't have one, you can create a one-month [free trial](https://azure.microsoft.com/pricing/free-trial/) subscription or visit [Azure Pricing](https://azure.microsoft.com/pricing/) for more options.</span></span>
* <span data-ttu-id="253eb-130">tooexecute poleceń cmdlet programu PowerShell, należy hello modułu Microsoft Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="253eb-130">tooexecute PowerShell cmdlets, you will need hello Microsoft Azure PowerShell module.</span></span> <span data-ttu-id="253eb-131">Zobacz [jak tooinstall i konfigurowanie programu Azure PowerShell](/powershell/azure/overview) hello zainstalować instrukcje instalacji i punktu.</span><span class="sxs-lookup"><span data-stu-id="253eb-131">See [How tooinstall and configure Azure PowerShell](/powershell/azure/overview) for hello install point and installation instructions.</span></span>
* <span data-ttu-id="253eb-132">Planując maszyn wirtualnych Azure toouse pracujących na magazyn w warstwie Premium, należy toouse hello maszyn wirtualnych z funkcją Magazyn w warstwie Premium.</span><span class="sxs-lookup"><span data-stu-id="253eb-132">When you plan toouse Azure VMs running on Premium Storage, you need toouse hello Premium Storage capable VMs.</span></span> <span data-ttu-id="253eb-133">Dyski w wersjach Standard i Premium Storage służy magazyn w warstwie Premium obsługuje maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="253eb-133">You can use both Standard and Premium Storage disks with Premium Storage capable VMs.</span></span> <span data-ttu-id="253eb-134">Dyski magazynu Premium będą dostępne z większą liczbę typów w przyszłości hello maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="253eb-134">Premium storage disks will be available with more VM types in hello future.</span></span> <span data-ttu-id="253eb-135">Aby uzyskać więcej informacji na wszystkich dostępnych typów dysku maszyny Wirtualnej platformy Azure i rozmiarów, zobacz [rozmiary maszyn wirtualnych](../virtual-machines/windows/sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) i [rozmiary dla usług w chmurze](../cloud-services/cloud-services-sizes-specs.md).</span><span class="sxs-lookup"><span data-stu-id="253eb-135">For more information on all available Azure VM disk types and sizes, see [Sizes for virtual machines](../virtual-machines/windows/sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) and [Sizes for Cloud Services](../cloud-services/cloud-services-sizes-specs.md).</span></span>

### <a name="considerations"></a><span data-ttu-id="253eb-136">Zagadnienia do rozważenia</span><span class="sxs-lookup"><span data-stu-id="253eb-136">Considerations</span></span>
<span data-ttu-id="253eb-137">Maszyny Wirtualnej platformy Azure obsługuje dołączanie kilka dysków Premium Storage, dzięki czemu aplikacji może zawierać maksymalnie too256 TB pamięci masowej dla maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="253eb-137">An Azure VM supports attaching several Premium Storage disks so that your applications can have up too256 TB of storage per VM.</span></span> <span data-ttu-id="253eb-138">Z magazyn w warstwie Premium aplikacje można osiągnąć 80 000 IOPS (operacje wejścia/wyjścia na sekundę) dla maszyny Wirtualnej i 2000 MB na drugi przepływność dysku dla maszyny Wirtualnej z bardzo małych opóźnień operacji odczytu.</span><span class="sxs-lookup"><span data-stu-id="253eb-138">With Premium Storage, your applications can achieve 80,000 IOPS (input/output operations per second) per VM and 2000 MB per second disk throughput per VM with extremely low latencies for read operations.</span></span> <span data-ttu-id="253eb-139">Dostępne są opcje wiele maszyn wirtualnych i dysków.</span><span class="sxs-lookup"><span data-stu-id="253eb-139">You have options in a variety of VMs and Disks.</span></span> <span data-ttu-id="253eb-140">Ta sekcja ma toohelp toofind opcję najlepiej pasującą do obciążenia.</span><span class="sxs-lookup"><span data-stu-id="253eb-140">This section is toohelp you toofind an option that best suits your workload.</span></span>

#### <a name="vm-sizes"></a><span data-ttu-id="253eb-141">Rozmiary maszyn wirtualnych</span><span class="sxs-lookup"><span data-stu-id="253eb-141">VM sizes</span></span>
<span data-ttu-id="253eb-142">specyfikacje rozmiaru maszyny Wirtualnej Azure Hello są wymienione w [rozmiary maszyn wirtualnych](../virtual-machines/windows/sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="253eb-142">hello Azure VM size specifications are listed in [Sizes for virtual machines](../virtual-machines/windows/sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> <span data-ttu-id="253eb-143">Przejrzyj hello charakterystyki wydajności maszyn wirtualnych, które pracować z magazyn w warstwie Premium i wybierz polecenie hello najbardziej odpowiedni rozmiar maszyny Wirtualnej najlepiej pasujące do obciążenia.</span><span class="sxs-lookup"><span data-stu-id="253eb-143">Review hello performance characteristics of virtual machines that work with Premium Storage and choose hello most appropriate VM size that best suits your workload.</span></span> <span data-ttu-id="253eb-144">Upewnij się, czy Brak dostępnej wystarczającą przepustowość na ruchu dysku hello toodrive maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="253eb-144">Make sure that there is sufficient bandwidth available on your VM toodrive hello disk traffic.</span></span>

#### <a name="disk-sizes"></a><span data-ttu-id="253eb-145">Rozmiary dysków</span><span class="sxs-lookup"><span data-stu-id="253eb-145">Disk sizes</span></span>
<span data-ttu-id="253eb-146">Istnieje pięć typów dysków, które mogą być używane z maszyny Wirtualnej, a każdy ma określonych IOPs i przepływność limity.</span><span class="sxs-lookup"><span data-stu-id="253eb-146">There are five types of disks that can be used with your VM and each has specific IOPs and throughput limits.</span></span> <span data-ttu-id="253eb-147">Wziąć pod uwagę następujące limity gdy wybieranie hello typu dysku do maszyny Wirtualnej na podstawie hello potrzeb aplikacji pod względem wydajności, wydajności, skalowalności i ładuje godzinami szczytu.</span><span class="sxs-lookup"><span data-stu-id="253eb-147">Take into consideration these limits when choosing hello disk type for your VM based on hello needs of your application in terms of capacity, performance, scalability, and peak loads.</span></span>

| <span data-ttu-id="253eb-148">Typ dysków Premium</span><span class="sxs-lookup"><span data-stu-id="253eb-148">Premium Disks Type</span></span>  | <span data-ttu-id="253eb-149">P10</span><span class="sxs-lookup"><span data-stu-id="253eb-149">P10</span></span>   | <span data-ttu-id="253eb-150">P20</span><span class="sxs-lookup"><span data-stu-id="253eb-150">P20</span></span>   | <span data-ttu-id="253eb-151">P30</span><span class="sxs-lookup"><span data-stu-id="253eb-151">P30</span></span>            | <span data-ttu-id="253eb-152">P40</span><span class="sxs-lookup"><span data-stu-id="253eb-152">P40</span></span>            | <span data-ttu-id="253eb-153">P50</span><span class="sxs-lookup"><span data-stu-id="253eb-153">P50</span></span>            | 
|:-------------------:|:-----:|:-----:|:--------------:|:--------------:|:--------------:|
| <span data-ttu-id="253eb-154">Rozmiar dysku</span><span class="sxs-lookup"><span data-stu-id="253eb-154">Disk size</span></span>           | <span data-ttu-id="253eb-155">128 GB</span><span class="sxs-lookup"><span data-stu-id="253eb-155">128 GB</span></span>| <span data-ttu-id="253eb-156">512 GB</span><span class="sxs-lookup"><span data-stu-id="253eb-156">512 GB</span></span>| <span data-ttu-id="253eb-157">1024 GB (1 TB)</span><span class="sxs-lookup"><span data-stu-id="253eb-157">1024 GB (1 TB)</span></span> | <span data-ttu-id="253eb-158">2048 GB (2 TB)</span><span class="sxs-lookup"><span data-stu-id="253eb-158">2048 GB (2 TB)</span></span> | <span data-ttu-id="253eb-159">4095 GB (4 TB)</span><span class="sxs-lookup"><span data-stu-id="253eb-159">4095 GB (4 TB)</span></span> | 
| <span data-ttu-id="253eb-160">Liczba operacji wejścia/wyjścia na sekundę na dysk</span><span class="sxs-lookup"><span data-stu-id="253eb-160">IOPS per disk</span></span>       | <span data-ttu-id="253eb-161">500</span><span class="sxs-lookup"><span data-stu-id="253eb-161">500</span></span>   | <span data-ttu-id="253eb-162">2300</span><span class="sxs-lookup"><span data-stu-id="253eb-162">2300</span></span>  | <span data-ttu-id="253eb-163">5000</span><span class="sxs-lookup"><span data-stu-id="253eb-163">5000</span></span>           | <span data-ttu-id="253eb-164">7500</span><span class="sxs-lookup"><span data-stu-id="253eb-164">7500</span></span>           | <span data-ttu-id="253eb-165">7500</span><span class="sxs-lookup"><span data-stu-id="253eb-165">7500</span></span>           | 
| <span data-ttu-id="253eb-166">Przepływność na dysk</span><span class="sxs-lookup"><span data-stu-id="253eb-166">Throughput per disk</span></span> | <span data-ttu-id="253eb-167">100 MB na sekundę</span><span class="sxs-lookup"><span data-stu-id="253eb-167">100 MB per second</span></span> | <span data-ttu-id="253eb-168">150 MB na sekundę</span><span class="sxs-lookup"><span data-stu-id="253eb-168">150 MB per second</span></span> | <span data-ttu-id="253eb-169">200 MB / s</span><span class="sxs-lookup"><span data-stu-id="253eb-169">200 MB per second</span></span> | <span data-ttu-id="253eb-170">250 MB na sekundę</span><span class="sxs-lookup"><span data-stu-id="253eb-170">250 MB per second</span></span> | <span data-ttu-id="253eb-171">250 MB na sekundę</span><span class="sxs-lookup"><span data-stu-id="253eb-171">250 MB per second</span></span> |

<span data-ttu-id="253eb-172">W zależności od obciążenia należy sprawdzić, czy dyski dodatkowe dane są niezbędne dla maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="253eb-172">Depending on your workload, determine if additional data disks are necessary for your VM.</span></span> <span data-ttu-id="253eb-173">Możesz dołączyć kilka tooyour dysków danych maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="253eb-173">You can attach several persistent data disks tooyour VM.</span></span> <span data-ttu-id="253eb-174">W razie potrzeby można paskowych między hello dysków tooincrease hello pojemność i wydajność hello woluminu.</span><span class="sxs-lookup"><span data-stu-id="253eb-174">If needed, you can stripe across hello disks tooincrease hello capacity and performance of hello volume.</span></span> <span data-ttu-id="253eb-175">(Zobacz, co rozkładanie [tutaj](storage-premium-storage-performance.md#disk-striping).) Jeśli paskowych magazyn w warstwie Premium dysków danych za pomocą [miejsca do magazynowania][4], należy ją skonfigurować z jedną kolumną dla każdego dysku, który jest używany.</span><span class="sxs-lookup"><span data-stu-id="253eb-175">(See what is Disk Striping [here](storage-premium-storage-performance.md#disk-striping).) If you stripe Premium Storage data disks using [Storage Spaces][4], you should configure it with one column for each disk that is used.</span></span> <span data-ttu-id="253eb-176">W przeciwnym razie hello ogólnej wydajności hello rozkładane woluminu może być niższa niż oczekiwano powodu dystrybucji toouneven ruchu na dyskach hello.</span><span class="sxs-lookup"><span data-stu-id="253eb-176">Otherwise, hello overall performance of hello striped volume may be lower than expected due toouneven distribution of traffic across hello disks.</span></span> <span data-ttu-id="253eb-177">W przypadku maszyn wirtualnych systemu Linux można użyć hello *mdadm* tooachieve narzędzie hello takie same.</span><span class="sxs-lookup"><span data-stu-id="253eb-177">For Linux VMs you can use hello *mdadm* utility tooachieve hello same.</span></span> <span data-ttu-id="253eb-178">Zobacz artykuł [skonfigurować RAID oprogramowania w systemie Linux](../virtual-machines/linux/configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) szczegółowe informacje.</span><span class="sxs-lookup"><span data-stu-id="253eb-178">See article [Configure Software RAID on Linux](../virtual-machines/linux/configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) for details.</span></span>

#### <a name="storage-account-scalability-targets"></a><span data-ttu-id="253eb-179">Wartości docelowe skalowalności konta magazynu</span><span class="sxs-lookup"><span data-stu-id="253eb-179">Storage account scalability targets</span></span>
<span data-ttu-id="253eb-180">Konta Premium magazynu ma następujące wartości docelowe skalowalności w toohello dodanie hello [cele dotyczące wydajności i skalowalności magazynu Azure](storage-scalability-targets.md).</span><span class="sxs-lookup"><span data-stu-id="253eb-180">Premium Storage accounts have hello following scalability targets in addition toohello [Azure Storage Scalability and Performance Targets](storage-scalability-targets.md).</span></span> <span data-ttu-id="253eb-181">Wymagania aplikacji przekracza hello wartości docelowe skalowalności konta magazynu pojedynczego, kompilacji toouse Twojej aplikacji z wielu kont magazynu i partycji danych przez tych kont magazynu.</span><span class="sxs-lookup"><span data-stu-id="253eb-181">If your application requirements exceed hello scalability targets of a single storage account, build your application toouse multiple storage accounts, and partition your data across those storage accounts.</span></span>

| <span data-ttu-id="253eb-182">Konto łączna pojemność</span><span class="sxs-lookup"><span data-stu-id="253eb-182">Total Account Capacity</span></span> | <span data-ttu-id="253eb-183">Przepustowość konto magazyn lokalnie nadmiarowy</span><span class="sxs-lookup"><span data-stu-id="253eb-183">Total Bandwidth for a Locally Redundant Storage Account</span></span> |
|:--- |:--- |
| <span data-ttu-id="253eb-184">Pojemność dysku: 35TB</span><span class="sxs-lookup"><span data-stu-id="253eb-184">Disk capacity: 35TB</span></span><br /><span data-ttu-id="253eb-185">Migawki pojemności: 10 TB</span><span class="sxs-lookup"><span data-stu-id="253eb-185">Snapshot capacity: 10 TB</span></span> |<span data-ttu-id="253eb-186">Zapasowej too50 gigabity na sekundę dla ruchu przychodzącego i wychodzącego</span><span class="sxs-lookup"><span data-stu-id="253eb-186">Up too50 gigabits per second for Inbound + Outbound</span></span> |

<span data-ttu-id="253eb-187">Dla hello więcej informacji na temat specyfikacji magazyn w warstwie Premium, zapoznaj się z [skalowalność i cele wydajności przy użyciu magazyn w warstwie Premium](storage-premium-storage.md#scalability-and-performance-targets).</span><span class="sxs-lookup"><span data-stu-id="253eb-187">For hello more information on Premium Storage specifications, check out [Scalability and Performance Targets when using Premium Storage](storage-premium-storage.md#scalability-and-performance-targets).</span></span>

#### <a name="disk-caching-policy"></a><span data-ttu-id="253eb-188">Dyskowej pamięci podręcznej zasad</span><span class="sxs-lookup"><span data-stu-id="253eb-188">Disk caching policy</span></span>
<span data-ttu-id="253eb-189">Domyślnie jest dyskowej pamięci podręcznej zasad *tylko do odczytu* dla wszystkich hello dysków danych w warstwie Premium i *odczytu i zapisu* dla dysku systemu operacyjnego Premium hello dołączony toohello maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="253eb-189">By default, disk caching policy is *Read-Only* for all hello Premium data disks, and *Read-Write* for hello Premium operating system disk attached toohello VM.</span></span> <span data-ttu-id="253eb-190">To ustawienie konfiguracji jest zalecane tooachieve hello optymalnej wydajności dla aplikacji systemu IOs.</span><span class="sxs-lookup"><span data-stu-id="253eb-190">This configuration setting is recommended tooachieve hello optimal performance for your application's IOs.</span></span> <span data-ttu-id="253eb-191">W przypadku dysków ciężki zapisu lub w trybie tylko do zapisu danych (takich jak pliki dziennika programu SQL Server) Wyłącz buforowanie dysku, dzięki czemu można osiągnąć lepszą wydajność aplikacji.</span><span class="sxs-lookup"><span data-stu-id="253eb-191">For write-heavy or write-only data disks (such as SQL Server log files), disable disk caching so that you can achieve better application performance.</span></span> <span data-ttu-id="253eb-192">ustawienia pamięci podręcznej Hello istniejących dysków danych można zaktualizować przy użyciu [Azure Portal](https://portal.azure.com) lub hello *- HostCaching* parametru hello *AzureDataDisk zestawu* polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="253eb-192">hello cache settings for existing data disks can be updated using [Azure Portal](https://portal.azure.com) or hello *-HostCaching* parameter of hello *Set-AzureDataDisk* cmdlet.</span></span>

#### <a name="location"></a><span data-ttu-id="253eb-193">Lokalizacja</span><span class="sxs-lookup"><span data-stu-id="253eb-193">Location</span></span>
<span data-ttu-id="253eb-194">Wybierz lokalizację, gdzie dostępna jest usługa Azure Premium Storage.</span><span class="sxs-lookup"><span data-stu-id="253eb-194">Pick a location where Azure Premium Storage is available.</span></span> <span data-ttu-id="253eb-195">Zobacz [regionów platformy Azure](https://azure.microsoft.com/regions/#services) aktualne informacje o dostępnych lokalizacji.</span><span class="sxs-lookup"><span data-stu-id="253eb-195">See [Azure Services by Region](https://azure.microsoft.com/regions/#services) for up-to-date information on available locations.</span></span> <span data-ttu-id="253eb-196">Maszyny wirtualne znajdujące się w hello sam region jako hello konta magazynu, czy magazyny hello dysków dla maszyny Wirtualnej hello zapewni znacznie lepszą wydajność niż jeśli znajdują się w oddzielnych regionach.</span><span class="sxs-lookup"><span data-stu-id="253eb-196">VMs located in hello same region as hello Storage account that stores hello disks for hello VM will give much better performance than if they are in separate regions.</span></span>

#### <a name="other-azure-vm-configuration-settings"></a><span data-ttu-id="253eb-197">Inne ustawienia konfiguracji maszyny Wirtualnej Azure</span><span class="sxs-lookup"><span data-stu-id="253eb-197">Other Azure VM configuration settings</span></span>
<span data-ttu-id="253eb-198">Podczas tworzenia maszyny Wirtualnej platformy Azure, użytkownik będzie proszony tooconfigure niektórych ustawień maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="253eb-198">When creating an Azure VM, you will be asked tooconfigure certain VM settings.</span></span> <span data-ttu-id="253eb-199">Należy pamiętać, że w ustaleniu ustawień kilka hello czas ich istnienia hello maszyny Wirtualnej, podczas gdy można zmodyfikować lub dodać inne później.</span><span class="sxs-lookup"><span data-stu-id="253eb-199">Remember, few settings are fixed for hello lifetime of hello VM, while you can modify or add others later.</span></span> <span data-ttu-id="253eb-200">Przejrzyj te ustawienia konfiguracji maszyny Wirtualnej platformy Azure i upewnij się, że są one poprawnie skonfigurowane, toomatch wymagań obciążenia.</span><span class="sxs-lookup"><span data-stu-id="253eb-200">Review these Azure VM configuration settings and make sure that these are configured appropriately toomatch your workload requirements.</span></span>

### <a name="optimization"></a><span data-ttu-id="253eb-201">Optymalizacja</span><span class="sxs-lookup"><span data-stu-id="253eb-201">Optimization</span></span>
<span data-ttu-id="253eb-202">[Usługa Azure Premium Storage: Projekt o wysokiej wydajności](storage-premium-storage-performance.md) zawiera wskazówki dotyczące tworzenia aplikacji wysokiej wydajności za pomocą usługi Azure Premium Storage.</span><span class="sxs-lookup"><span data-stu-id="253eb-202">[Azure Premium Storage: Design for High Performance](storage-premium-storage-performance.md) provides guidelines for building high-performance applications using Azure Premium Storage.</span></span> <span data-ttu-id="253eb-203">Można użyć wskazówki hello połączone z wydajności najlepszych praktyk stosowanych tootechnologies używanych przez aplikację.</span><span class="sxs-lookup"><span data-stu-id="253eb-203">You can follow hello guidelines combined with performance best practices applicable tootechnologies used by your application.</span></span>

## <span data-ttu-id="253eb-204"><a name="prepare-and-copy-virtual-hard-disks-VHDs-to-premium-storage"></a>Przygotowanie i skopiuj wirtualne dyski twarde (VHD) tooPremium magazynu</span><span class="sxs-lookup"><span data-stu-id="253eb-204"><a name="prepare-and-copy-virtual-hard-disks-VHDs-to-premium-storage"></a>Prepare and copy virtual hard disks (VHDs) tooPremium Storage</span></span>
<span data-ttu-id="253eb-205">powitania po sekcji wskazówki przygotowania wirtualne dyski twarde z maszyny Wirtualnej i kopiowanie wirtualnych dysków twardych tooAzure magazynu.</span><span class="sxs-lookup"><span data-stu-id="253eb-205">hello following section provides guidelines for preparing VHDs from your VM and copying VHDs tooAzure Storage.</span></span>

* [<span data-ttu-id="253eb-206">Scenariusz 1: "I am migracji istniejących maszyn wirtualnych Azure tooAzure magazyn w warstwie Premium."</span><span class="sxs-lookup"><span data-stu-id="253eb-206">Scenario 1: "I am migrating existing Azure VMs tooAzure Premium Storage."</span></span>](#scenario1)
* [<span data-ttu-id="253eb-207">Scenariusz 2: "I am Migrowanie maszyn wirtualnych z innych platform tooAzure magazyn w warstwie Premium."</span><span class="sxs-lookup"><span data-stu-id="253eb-207">Scenario 2: "I am migrating VMs from other platforms tooAzure Premium Storage."</span></span>](#scenario2)

### <a name="prerequisites"></a><span data-ttu-id="253eb-208">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="253eb-208">Prerequisites</span></span>
<span data-ttu-id="253eb-209">Witaj tooprepare wirtualne dyski twarde do migracji, będą potrzebne:</span><span class="sxs-lookup"><span data-stu-id="253eb-209">tooprepare hello VHDs for migration, you'll need:</span></span>

* <span data-ttu-id="253eb-210">Subskrypcja platformy Azure, konta magazynu i kontener, w tym magazynie konta toowhich kopiujesz dysk VHD.</span><span class="sxs-lookup"><span data-stu-id="253eb-210">An Azure subscription, a storage account, and a container in that storage account toowhich you can copy your VHD.</span></span> <span data-ttu-id="253eb-211">Należy pamiętać, że konto magazynu docelowego hello może być kontem Standard lub Premium Storage, w zależności od wymagań.</span><span class="sxs-lookup"><span data-stu-id="253eb-211">Note that hello destination storage account can be a Standard or Premium Storage account depending on your requirement.</span></span>
* <span data-ttu-id="253eb-212">Witaj toogeneralize narzędzie wirtualnego dysku twardego, jeśli planujesz toocreate wielu wystąpień maszyny Wirtualnej z niego.</span><span class="sxs-lookup"><span data-stu-id="253eb-212">A tool toogeneralize hello VHD if you plan toocreate multiple VM instances from it.</span></span> <span data-ttu-id="253eb-213">Na przykład, program sysprep dla systemu Windows lub programu sysprep virt dla Ubuntu.</span><span class="sxs-lookup"><span data-stu-id="253eb-213">For example, sysprep for Windows or virt-sysprep for Ubuntu.</span></span>
* <span data-ttu-id="253eb-214">Narzędzie tooupload hello wirtualnego dysku twardego pliku toohello konta magazynu.</span><span class="sxs-lookup"><span data-stu-id="253eb-214">A tool tooupload hello VHD file toohello Storage account.</span></span> <span data-ttu-id="253eb-215">Zobacz [Transfer danych za pomocą wiersza polecenia Azcopy hello](storage-use-azcopy.md) lub użyj [Eksploratora usługi Azure storage](http://blogs.msdn.com/b/windowsazurestorage/archive/2014/03/11/windows-azure-storage-explorers-2014.aspx).</span><span class="sxs-lookup"><span data-stu-id="253eb-215">See [Transfer data with hello AzCopy Command-Line Utility](storage-use-azcopy.md) or use an [Azure storage explorer](http://blogs.msdn.com/b/windowsazurestorage/archive/2014/03/11/windows-azure-storage-explorers-2014.aspx).</span></span> <span data-ttu-id="253eb-216">Ten przewodnik zawiera opis kopiowanie dysk VHD za pomocą narzędzia AzCopy hello.</span><span class="sxs-lookup"><span data-stu-id="253eb-216">This guide describes copying your VHD using hello AzCopy tool.</span></span>

> [!NOTE]
> <span data-ttu-id="253eb-217">Jeśli wybierzesz opcję synchronicznych kopii z narzędzia AzCopy, aby uzyskać optymalną wydajność, skopiuj dysk VHD, uruchamiając jeden z tych narzędzi z maszyny Wirtualnej platformy Azure, który znajduje się w hello tego samego regionu co konto magazynu docelowego hello.</span><span class="sxs-lookup"><span data-stu-id="253eb-217">If you choose synchronous copy option with AzCopy, for optimal performance, copy your VHD by running one of these tools from an Azure VM that is in hello same region as hello destination storage account.</span></span> <span data-ttu-id="253eb-218">Jeśli kopiujesz dysk VHD maszyny Wirtualnej platformy Azure w innym regionie, wydajność może przebiegać wolniej.</span><span class="sxs-lookup"><span data-stu-id="253eb-218">If you are copying a VHD from an Azure VM in a different region, your performance may be slower.</span></span>
>
> <span data-ttu-id="253eb-219">W przypadku kopiowania dużych ilości danych w ograniczonej przepustowości, rozważ [przy użyciu hello Import/Eksport Azure usługa tootransfer danych tooBlob magazynu](storage-import-export-service.md); umożliwia tootransfer danych przez dysk twardy wysyłki dyski tooan Azure Centrum danych.</span><span class="sxs-lookup"><span data-stu-id="253eb-219">For copying a large amount of data over limited bandwidth, consider [using hello Azure Import/Export service tootransfer data tooBlob Storage](storage-import-export-service.md); this allows you tootransfer your data by shipping hard disk drives tooan Azure datacenter.</span></span> <span data-ttu-id="253eb-220">Możesz użyć hello Import/Eksport Azure usługa toocopy danych tooa konta standard storage tylko.</span><span class="sxs-lookup"><span data-stu-id="253eb-220">You can use hello Azure Import/Export service toocopy data tooa standard storage account only.</span></span> <span data-ttu-id="253eb-221">Po hello danych na koncie magazynu w warstwie standardowa, można użyć albo hello [kopiowania obiektu Blob API](https://msdn.microsoft.com/library/azure/dd894037.aspx) lub konto magazynu premium tooyour danych AzCopy tootransfer hello.</span><span class="sxs-lookup"><span data-stu-id="253eb-221">Once hello data is in your standard storage account, you can use either hello [Copy Blob API](https://msdn.microsoft.com/library/azure/dd894037.aspx) or AzCopy tootransfer hello data tooyour premium storage account.</span></span>
>
> <span data-ttu-id="253eb-222">Należy pamiętać, że Microsoft Azure obsługuje tylko pliki wirtualnego dysku twardego o stałym rozmiarze.</span><span class="sxs-lookup"><span data-stu-id="253eb-222">Note that Microsoft Azure only supports fixed size VHD files.</span></span> <span data-ttu-id="253eb-223">Pliki VHDX lub dynamiczne wirtualne dyski twarde nie są obsługiwane.</span><span class="sxs-lookup"><span data-stu-id="253eb-223">VHDX files or dynamic VHDs are not supported.</span></span> <span data-ttu-id="253eb-224">Jeśli masz dynamicznego wirtualnego dysku twardego, możesz przekonwertować ją przy użyciu hello rozmiar toofixed [Convert-VHD](http://technet.microsoft.com/library/hh848454.aspx) polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="253eb-224">If you have a dynamic VHD, you can convert it toofixed size using hello [Convert-VHD](http://technet.microsoft.com/library/hh848454.aspx) cmdlet.</span></span>
>
>

### <span data-ttu-id="253eb-225"><a name="scenario1"></a>Scenariusz 1: "I am migracji istniejących maszyn wirtualnych Azure tooAzure magazyn w warstwie Premium."</span><span class="sxs-lookup"><span data-stu-id="253eb-225"><a name="scenario1"></a>Scenario 1: "I am migrating existing Azure VMs tooAzure Premium Storage."</span></span>
<span data-ttu-id="253eb-226">W przypadku migracji istniejących maszyn wirtualnych platformy Azure, hello Zatrzymaj maszynę Wirtualną, przygotowanie dysków VHD na typ hello ma wirtualnego dysku twardego, a następnie skopiuj hello wirtualnego dysku twardego z narzędzia AzCopy lub środowiska PowerShell.</span><span class="sxs-lookup"><span data-stu-id="253eb-226">If you are migrating existing Azure VMs, stop hello VM, prepare VHDs per hello type of VHD you want, and then copy hello VHD with AzCopy or PowerShell.</span></span>

<span data-ttu-id="253eb-227">Witaj maszyny Wirtualnej musi toobe całkowicie dół toomigrate stanu czystego.</span><span class="sxs-lookup"><span data-stu-id="253eb-227">hello VM needs toobe completely down toomigrate a clean state.</span></span> <span data-ttu-id="253eb-228">Będzie przestoju dopiero po zakończeniu migracji hello.</span><span class="sxs-lookup"><span data-stu-id="253eb-228">There will be a downtime until hello migration completes.</span></span>

#### <a name="step-1-prepare-vhds-for-migration"></a><span data-ttu-id="253eb-229">Krok 1.</span><span class="sxs-lookup"><span data-stu-id="253eb-229">Step 1.</span></span> <span data-ttu-id="253eb-230">Przygotowanie do migracji dysków VHD</span><span class="sxs-lookup"><span data-stu-id="253eb-230">Prepare VHDs for migration</span></span>
<span data-ttu-id="253eb-231">W przypadku migracji istniejących maszyn wirtualnych platformy Azure tooPremium magazynu, może być dysk VHD:</span><span class="sxs-lookup"><span data-stu-id="253eb-231">If you are migrating existing Azure VMs tooPremium Storage, your VHD may be:</span></span>

* <span data-ttu-id="253eb-232">Obraz systemu operacyjnego ogólnych</span><span class="sxs-lookup"><span data-stu-id="253eb-232">A generalized operating system image</span></span>
* <span data-ttu-id="253eb-233">Dysk systemu operacyjnego</span><span class="sxs-lookup"><span data-stu-id="253eb-233">A unique operating system disk</span></span>
* <span data-ttu-id="253eb-234">Dysk z danymi</span><span class="sxs-lookup"><span data-stu-id="253eb-234">A data disk</span></span>

<span data-ttu-id="253eb-235">Poniżej opisano firma Microsoft za pośrednictwem tych scenariuszy 3 przygotowania dysk VHD.</span><span class="sxs-lookup"><span data-stu-id="253eb-235">Below we walk through these 3 scenarios for preparing your VHD.</span></span>

##### <a name="use-a-generalized-operating-system-vhd-toocreate-multiple-vm-instances"></a><span data-ttu-id="253eb-236">Użyj ogólnych toocreate wirtualnego dysku twardego systemu operacyjnego wielu wystąpień maszyny Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="253eb-236">Use a generalized Operating System VHD toocreate multiple VM instances</span></span>
<span data-ttu-id="253eb-237">Podczas przekazywania wirtualnego dysku twardego, który ma być używane toocreate wiele ogólnych wystąpień maszyny Wirtualnej platformy Azure, musi najpierw generalize plik VHD za pomocą narzędzia sysprep.</span><span class="sxs-lookup"><span data-stu-id="253eb-237">If you are uploading a VHD that will be used toocreate multiple generic Azure VM instances, you must first generalize VHD using a sysprep utility.</span></span> <span data-ttu-id="253eb-238">Dotyczy to tooa wirtualnego dysku twardego, który jest lokalnie lub w chmurze hello.</span><span class="sxs-lookup"><span data-stu-id="253eb-238">This applies tooa VHD that is on-premises or in hello cloud.</span></span> <span data-ttu-id="253eb-239">Program Sysprep usuwa wszystkie informacje dotyczące komputera hello wirtualnego dysku twardego.</span><span class="sxs-lookup"><span data-stu-id="253eb-239">Sysprep removes any machine-specific information from hello VHD.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="253eb-240">Utwórz migawkę lub kopii zapasowej maszyny Wirtualnej przed jej uogólnianie.</span><span class="sxs-lookup"><span data-stu-id="253eb-240">Take a snapshot or backup your VM before generalizing it.</span></span> <span data-ttu-id="253eb-241">Uruchomiony program sysprep spowoduje zatrzymanie i deallocate hello wystąpienia maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="253eb-241">Running sysprep will stop and deallocate hello VM instance.</span></span> <span data-ttu-id="253eb-242">Wykonaj kroki opisane poniżej toosysprep wirtualnego dysku twardego systemu operacyjnego Windows.</span><span class="sxs-lookup"><span data-stu-id="253eb-242">Follow steps below toosysprep a Windows OS VHD.</span></span> <span data-ttu-id="253eb-243">Należy pamiętać, że polecenia Sysprep hello będzie wymagać tooshut maszynę wirtualną hello.</span><span class="sxs-lookup"><span data-stu-id="253eb-243">Note that running hello Sysprep command will require you tooshut down hello virtual machine.</span></span> <span data-ttu-id="253eb-244">Aby uzyskać więcej informacji na temat narzędzia Sysprep, zobacz [Omówienie narzędzia Sysprep](http://technet.microsoft.com/library/hh825209.aspx) lub [techniczne dotyczące narzędzia Sysprep](http://technet.microsoft.com/library/cc766049.aspx).</span><span class="sxs-lookup"><span data-stu-id="253eb-244">For more information about Sysprep, see [Sysprep Overview](http://technet.microsoft.com/library/hh825209.aspx) or [Sysprep Technical Reference](http://technet.microsoft.com/library/cc766049.aspx).</span></span>
>
>

1. <span data-ttu-id="253eb-245">Otwórz okno wiersza polecenia z uprawnieniami administratora.</span><span class="sxs-lookup"><span data-stu-id="253eb-245">Open a Command Prompt window as an administrator.</span></span>
2. <span data-ttu-id="253eb-246">Wprowadź powitania po tooopen polecenia Sysprep:</span><span class="sxs-lookup"><span data-stu-id="253eb-246">Enter hello following command tooopen Sysprep:</span></span>

    ```
    %windir%\system32\sysprep\sysprep.exe
    ```

3. <span data-ttu-id="253eb-247">Hello narzędzie przygotowania systemu, wybierz opcję Wprowadź systemu Out-of-Box (OOBE Experience), hello zaznacz pole wyboru Generalize, wybierz **zamknięcia**, a następnie kliknij przycisk **OK**, jak pokazano w poniższym obrazie hello.</span><span class="sxs-lookup"><span data-stu-id="253eb-247">In hello System Preparation Tool, select Enter System Out-of-Box Experience (OOBE), select hello Generalize check box, select **Shutdown**, and then click **OK**, as shown in hello image below.</span></span> <span data-ttu-id="253eb-248">Narzędzie Sysprep będzie uogólnienia systemu operacyjnego hello i zamknij hello system.</span><span class="sxs-lookup"><span data-stu-id="253eb-248">Sysprep will generalize hello operating system and shut down hello system.</span></span>

    ![][1]

<span data-ttu-id="253eb-249">Dla maszyny Wirtualnej systemu Ubuntu Użyj narzędzia sysprep virt tooachieve hello takie same.</span><span class="sxs-lookup"><span data-stu-id="253eb-249">For an Ubuntu VM, use virt-sysprep tooachieve hello same.</span></span> <span data-ttu-id="253eb-250">Zobacz [virt sysprep](http://manpages.ubuntu.com/manpages/precise/man1/virt-sysprep.1.html) więcej szczegółów.</span><span class="sxs-lookup"><span data-stu-id="253eb-250">See [virt-sysprep](http://manpages.ubuntu.com/manpages/precise/man1/virt-sysprep.1.html) for more details.</span></span> <span data-ttu-id="253eb-251">Zobacz też niektóre typu hello open source [rozbudowy serwerów Linux oprogramowania](http://www.cyberciti.biz/tips/server-provisioning-software.html) dla innych systemów operacyjnych Linux.</span><span class="sxs-lookup"><span data-stu-id="253eb-251">See also some of hello open source [Linux Server Provisioning software](http://www.cyberciti.biz/tips/server-provisioning-software.html) for other Linux operating systems.</span></span>

##### <a name="use-a-unique-operating-system-vhd-toocreate-a-single-vm-instance"></a><span data-ttu-id="253eb-252">Użyj unikatowy toocreate wirtualnego dysku twardego systemu operacyjnego jedno wystąpienie maszyny Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="253eb-252">Use a unique Operating System VHD toocreate a single VM instance</span></span>
<span data-ttu-id="253eb-253">Jeśli masz aplikacji działających na powitania maszyny Wirtualnej, co wymaga dane dotyczące określonego komputera hello nie generalize hello wirtualnego dysku twardego.</span><span class="sxs-lookup"><span data-stu-id="253eb-253">If you have an application running on hello VM which requires hello machine specific data, do not generalize hello VHD.</span></span> <span data-ttu-id="253eb-254">Uogólniony wirtualny dysk twardy może być używane toocreate unikatowego wystąpienia maszyny Wirtualnej platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="253eb-254">A non-generalized VHD can be used toocreate a unique Azure VM instance.</span></span> <span data-ttu-id="253eb-255">Na przykład jeśli kontroler domeny na dysk VHD, wykonywanie programu sysprep, spowoduje to nieefektywne jako kontroler domeny.</span><span class="sxs-lookup"><span data-stu-id="253eb-255">For example, if you have Domain Controller on your VHD, executing sysprep will make it ineffective as a Domain Controller.</span></span> <span data-ttu-id="253eb-256">Przejrzyj hello aplikacji działających w sieci maszyny Wirtualnej i hello wpływ program sysprep na nich przed uogólnianie hello wirtualnego dysku twardego.</span><span class="sxs-lookup"><span data-stu-id="253eb-256">Review hello applications running on your VM and hello impact of running sysprep on them before generalizing hello VHD.</span></span>

##### <a name="register-data-disk-vhd"></a><span data-ttu-id="253eb-257">Zarejestruj dane dysku VHD</span><span class="sxs-lookup"><span data-stu-id="253eb-257">Register data disk VHD</span></span>
<span data-ttu-id="253eb-258">Jeśli masz migracji dysków z danymi w Azure toobe, należy upewnić się, że maszyny wirtualne hello korzystających z tych danych, które dyski są zamknięte.</span><span class="sxs-lookup"><span data-stu-id="253eb-258">If you have data disks in Azure toobe migrated, you must make sure hello VMs that use these data disks are shut down.</span></span>

<span data-ttu-id="253eb-259">Wykonaj kroki hello opisanych poniżej toocopy wirtualnego dysku twardego tooAzure magazyn w warstwie Premium i zarejestrowanie go jako dysk danych elastycznie.</span><span class="sxs-lookup"><span data-stu-id="253eb-259">Follow hello steps described below toocopy VHD tooAzure Premium Storage and register it as a provisioned data disk.</span></span>

#### <a name="step-2-create-hello-destination-for-your-vhd"></a><span data-ttu-id="253eb-260">Krok 2.</span><span class="sxs-lookup"><span data-stu-id="253eb-260">Step 2.</span></span> <span data-ttu-id="253eb-261">Utwórz lokalizację docelową hello dysk VHD</span><span class="sxs-lookup"><span data-stu-id="253eb-261">Create hello destination for your VHD</span></span>
<span data-ttu-id="253eb-262">Utwórz konto magazynu do przechowywania dyski VHD.</span><span class="sxs-lookup"><span data-stu-id="253eb-262">Create a storage account for maintaining your VHDs.</span></span> <span data-ttu-id="253eb-263">Należy wziąć pod uwagę następujące punkty podczas planowania miejsca hello toostore dyski VHD:</span><span class="sxs-lookup"><span data-stu-id="253eb-263">Consider hello following points when planning where toostore your VHDs:</span></span>

* <span data-ttu-id="253eb-264">obiekt docelowy Hello konta magazynu w warstwie Premium.</span><span class="sxs-lookup"><span data-stu-id="253eb-264">hello target Premium storage account.</span></span>
* <span data-ttu-id="253eb-265">Lokalizacja konta magazynu Hello musi być taki sam jak magazyn w warstwie Premium obsługuje maszyny wirtualne Azure utworzysz w ostatnim etapie hello.</span><span class="sxs-lookup"><span data-stu-id="253eb-265">hello storage account location must be same as Premium Storage capable Azure VMs you will create in hello final stage.</span></span> <span data-ttu-id="253eb-266">Można skopiować nowego konta magazynu tooa lub hello toouse planu tego samego konta magazynu na podstawie Twoich potrzeb.</span><span class="sxs-lookup"><span data-stu-id="253eb-266">You could copy tooa new storage account, or plan toouse hello same storage account based on your needs.</span></span>
* <span data-ttu-id="253eb-267">Skopiuj i Zapisz klucz konta magazynu hello konto magazynu docelowego hello hello następny etap.</span><span class="sxs-lookup"><span data-stu-id="253eb-267">Copy and save hello storage account key of hello destination storage account for hello next stage.</span></span>

<span data-ttu-id="253eb-268">Dla dysków z danymi można wybrać tookeep niektóre dyski danych w ramach konta magazynu w warstwie standardowa (na przykład dysków, które mają lodówki magazynu), ale zdecydowanie zalecamy przeniesienie wszystkich danych magazyn w warstwie premium toouse obciążeń produkcyjnych.</span><span class="sxs-lookup"><span data-stu-id="253eb-268">For data disks, you can choose tookeep some data disks in a standard storage account (for example, disks that have cooler storage), but we strongly recommend you moving all data for production workload toouse premium storage.</span></span>

#### <span data-ttu-id="253eb-269"><a name="copy-vhd-with-azcopy-or-powershell"></a>Krok 3.</span><span class="sxs-lookup"><span data-stu-id="253eb-269"><a name="copy-vhd-with-azcopy-or-powershell"></a>Step 3.</span></span> <span data-ttu-id="253eb-270">Skopiuj wirtualny dysk twardy z narzędzia AzCopy lub programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="253eb-270">Copy VHD with AzCopy or PowerShell</span></span>
<span data-ttu-id="253eb-271">Konieczne będzie toofind Twojego ścieżka kontenera i dowolna z tych dwóch opcji konta tooprocess klucza magazynu.</span><span class="sxs-lookup"><span data-stu-id="253eb-271">You will need toofind your container path and storage account key tooprocess either of these two options.</span></span> <span data-ttu-id="253eb-272">Kontener ścieżki i przechowywania klucza konta znajdują się w **Azure Portal** > **magazynu**.</span><span class="sxs-lookup"><span data-stu-id="253eb-272">Container path and storage account key can be found in **Azure Portal** > **Storage**.</span></span> <span data-ttu-id="253eb-273">adresu URL kontenera Hello będzie takie jak "https://myaccount.blob.core.windows.net/mycontainer/".</span><span class="sxs-lookup"><span data-stu-id="253eb-273">hello container URL will be like "https://myaccount.blob.core.windows.net/mycontainer/".</span></span>

##### <a name="option-1-copy-a-vhd-with-azcopy-asynchronous-copy"></a><span data-ttu-id="253eb-274">Opcja 1: Skopiuj dysk VHD o AzCopy (asynchroniczne kopia)</span><span class="sxs-lookup"><span data-stu-id="253eb-274">Option 1: Copy a VHD with AzCopy (Asynchronous copy)</span></span>
<span data-ttu-id="253eb-275">Przy użyciu narzędzia AzCopy, możesz wysłać hello wirtualnego dysku twardego za pośrednictwem hello Internet.</span><span class="sxs-lookup"><span data-stu-id="253eb-275">Using AzCopy, you can easily upload hello VHD over hello Internet.</span></span> <span data-ttu-id="253eb-276">W zależności od rozmiaru hello hello wirtualne dyski twarde to może potrwać.</span><span class="sxs-lookup"><span data-stu-id="253eb-276">Depending on hello size of hello VHDs, this may take time.</span></span> <span data-ttu-id="253eb-277">Należy pamiętać limity konta magazynu toocheck hello w wejście/wyjście, korzystając z tej opcji.</span><span class="sxs-lookup"><span data-stu-id="253eb-277">Remember toocheck hello storage account ingress/egress limits when using this option.</span></span> <span data-ttu-id="253eb-278">Zobacz [cele dotyczące wydajności i skalowalności magazynu Azure](storage-scalability-targets.md) szczegółowe informacje.</span><span class="sxs-lookup"><span data-stu-id="253eb-278">See [Azure Storage Scalability and Performance Targets](storage-scalability-targets.md) for details.</span></span>

1. <span data-ttu-id="253eb-279">Pobierz i zainstaluj narzędzie AzCopy stąd: [najnowszą wersję programu AzCopy](http://aka.ms/downloadazcopy)</span><span class="sxs-lookup"><span data-stu-id="253eb-279">Download and install AzCopy from here: [Latest version of AzCopy](http://aka.ms/downloadazcopy)</span></span>
2. <span data-ttu-id="253eb-280">Otwórz program Azure PowerShell i folder przejdź toohello, w którym zainstalowano narzędzia AzCopy.</span><span class="sxs-lookup"><span data-stu-id="253eb-280">Open Azure PowerShell and go toohello folder where AzCopy is installed.</span></span>
3. <span data-ttu-id="253eb-281">Użyj hello następujące polecenie plik VHD hello toocopy z "Source" za "Miejsce docelowe".</span><span class="sxs-lookup"><span data-stu-id="253eb-281">Use hello following command toocopy hello VHD file from "Source" too"Destination".</span></span>

    ```azcopy
    AzCopy /Source: <source> /SourceKey: <source-account-key> /Dest: <destination> /DestKey: <dest-account-key> /BlobType:page /Pattern: <file-name>
    ```

    <span data-ttu-id="253eb-282">Przykład:</span><span class="sxs-lookup"><span data-stu-id="253eb-282">Example:</span></span>

    ```azcopy
    AzCopy /Source:https://sourceaccount.blob.core.windows.net/mycontainer1 /SourceKey:key1 /Dest:https://destaccount.blob.core.windows.net/mycontainer2 /DestKey:key2 /Pattern:abc.vhd
    ```

    <span data-ttu-id="253eb-283">Poniżej przedstawiono opisy parametrów hello używana w hello polecenia programu AzCopy:</span><span class="sxs-lookup"><span data-stu-id="253eb-283">Here are descriptions of hello parameters used in hello AzCopy command:</span></span>

   * <span data-ttu-id="253eb-284">**/ Źródło:  *&lt;źródła&gt;:***  lokalizację folderu hello lub adresu URL kontenera magazynu zawierającego hello wirtualnego dysku twardego.</span><span class="sxs-lookup"><span data-stu-id="253eb-284">**/Source: *&lt;source&gt;:*** Location of hello folder or storage container URL that contains hello VHD.</span></span>
   * <span data-ttu-id="253eb-285">**/ SourceKey:  *&lt;źródła konta klucza&gt;:***  klucz konta magazynu z konta magazynu źródłowego hello.</span><span class="sxs-lookup"><span data-stu-id="253eb-285">**/SourceKey: *&lt;source-account-key&gt;:*** Storage account key of hello source storage account.</span></span>
   * <span data-ttu-id="253eb-286">**/ Dest:  *&lt;docelowego&gt;:***  toocopy adresu URL kontenera magazynu hello wirtualnego dysku twardego.</span><span class="sxs-lookup"><span data-stu-id="253eb-286">**/Dest: *&lt;destination&gt;:*** Storage container URL toocopy hello VHD to.</span></span>
   * <span data-ttu-id="253eb-287">**/ DestKey:  *&lt;dest konta klucza&gt;:***  klucz konta magazynu konto magazynu docelowego hello.</span><span class="sxs-lookup"><span data-stu-id="253eb-287">**/DestKey: *&lt;dest-account-key&gt;:*** Storage account key of hello destination storage account.</span></span>
   * <span data-ttu-id="253eb-288">**/ Wzorzec:  *&lt;nazwę pliku&gt;:***  Określ nazwę pliku hello hello toocopy wirtualnego dysku twardego.</span><span class="sxs-lookup"><span data-stu-id="253eb-288">**/Pattern: *&lt;file-name&gt;:*** Specify hello file name of hello VHD toocopy.</span></span>

<span data-ttu-id="253eb-289">Aby uzyskać więcej informacji na temat używania narzędzia AzCopy narzędzie, zobacz [Transfer danych za pomocą wiersza polecenia Azcopy hello](storage-use-azcopy.md).</span><span class="sxs-lookup"><span data-stu-id="253eb-289">For details on using AzCopy tool, see [Transfer data with hello AzCopy Command-Line Utility](storage-use-azcopy.md).</span></span>

##### <a name="option-2-copy-a-vhd-with-powershell-synchronized-copy"></a><span data-ttu-id="253eb-290">Opcja 2: Kopiować dysku VHD przy użyciu programu PowerShell (Synchronized kopia)</span><span class="sxs-lookup"><span data-stu-id="253eb-290">Option 2: Copy a VHD with PowerShell (Synchronized copy)</span></span>
<span data-ttu-id="253eb-291">Można także skopiować hello plik VHD za pomocą polecenia cmdlet programu PowerShell hello Start AzureStorageBlobCopy.</span><span class="sxs-lookup"><span data-stu-id="253eb-291">You can also copy hello VHD file using hello PowerShell cmdlet Start-AzureStorageBlobCopy.</span></span> <span data-ttu-id="253eb-292">Użyj hello następujące polecenia na toocopy programu Azure PowerShell wirtualnego dysku twardego.</span><span class="sxs-lookup"><span data-stu-id="253eb-292">Use hello following command on Azure PowerShell toocopy VHD.</span></span> <span data-ttu-id="253eb-293">Zastąp wartości hello <> odpowiednie wartości w ramach konta magazynu źródłowego i docelowego.</span><span class="sxs-lookup"><span data-stu-id="253eb-293">Replace hello values in <> with corresponding values from your source and destination storage account.</span></span> <span data-ttu-id="253eb-294">toouse to polecenie musi mieć kontener o nazwie wirtualne dyski twarde na koncie magazynu docelowego.</span><span class="sxs-lookup"><span data-stu-id="253eb-294">toouse this command, you must have a container called vhds in your destination storage account.</span></span> <span data-ttu-id="253eb-295">Jeśli hello kontener nie istnieje, utwórz je przed uruchomieniem polecenia hello.</span><span class="sxs-lookup"><span data-stu-id="253eb-295">If hello container doesn't exist, create one before running hello command.</span></span>

```powershell
$sourceBlobUri = <source-vhd-uri>

$sourceContext = New-AzureStorageContext  –StorageAccountName <source-account> -StorageAccountKey <source-account-key>

$destinationContext = New-AzureStorageContext  –StorageAccountName <dest-account> -StorageAccountKey <dest-account-key>

Start-AzureStorageBlobCopy -srcUri $sourceBlobUri -SrcContext $sourceContext -DestContainer <dest-container> -DestBlob <dest-disk-name> -DestContext $destinationContext
```

<span data-ttu-id="253eb-296">Przykład:</span><span class="sxs-lookup"><span data-stu-id="253eb-296">Example:</span></span>

```powershell
C:\PS> $sourceBlobUri = "https://sourceaccount.blob.core.windows.net/vhds/myvhd.vhd"

C:\PS> $sourceContext = New-AzureStorageContext  –StorageAccountName "sourceaccount" -StorageAccountKey "J4zUI9T5b8gvHohkiRg"

C:\PS> $destinationContext = New-AzureStorageContext  –StorageAccountName "destaccount" -StorageAccountKey "XZTmqSGKUYFSh7zB5"

C:\PS> Start-AzureStorageBlobCopy -srcUri $sourceBlobUri -SrcContext $sourceContext -DestContainer "vhds" -DestBlob "myvhd.vhd" -DestContext $destinationContext
```

### <span data-ttu-id="253eb-297"><a name="scenario2"></a>Scenariusz 2: "I am Migrowanie maszyn wirtualnych z innych platform tooAzure magazyn w warstwie Premium."</span><span class="sxs-lookup"><span data-stu-id="253eb-297"><a name="scenario2"></a>Scenario 2: "I am migrating VMs from other platforms tooAzure Premium Storage."</span></span>
<span data-ttu-id="253eb-298">W przypadku migracji z tooAzure — z usługi Azure Cloud Storage wirtualnego dysku twardego, należy wyeksportować hello katalogu lokalnego tooa wirtualnego dysku twardego.</span><span class="sxs-lookup"><span data-stu-id="253eb-298">If you are migrating VHD from non-Azure Cloud Storage tooAzure, you must first export hello VHD tooa local directory.</span></span> <span data-ttu-id="253eb-299">Ścieżka źródłowej pełną hello hello katalogu lokalnego wirtualnego dysku twardego przechowywania przydatną i przy użyciu narzędzia AzCopy tooupload on tooAzure magazynu.</span><span class="sxs-lookup"><span data-stu-id="253eb-299">Have hello complete source path of hello local directory where VHD is stored handy, and then using AzCopy tooupload it tooAzure Storage.</span></span>

#### <a name="step-1-export-vhd-tooa-local-directory"></a><span data-ttu-id="253eb-300">Krok 1.</span><span class="sxs-lookup"><span data-stu-id="253eb-300">Step 1.</span></span> <span data-ttu-id="253eb-301">Eksportowanie katalogu lokalnego tooa wirtualnego dysku twardego</span><span class="sxs-lookup"><span data-stu-id="253eb-301">Export VHD tooa local directory</span></span>
##### <a name="copy-a-vhd-from-aws"></a><span data-ttu-id="253eb-302">Skopiuj wirtualny dysk twardy z usług AWS</span><span class="sxs-lookup"><span data-stu-id="253eb-302">Copy a VHD from AWS</span></span>
1. <span data-ttu-id="253eb-303">Jeśli używasz usług AWS wyeksportować hello EC2 wystąpienia tooa wirtualnego dysku twardego w zasobniku Amazon S3.</span><span class="sxs-lookup"><span data-stu-id="253eb-303">If you are using AWS, export hello EC2 instance tooa VHD in an Amazon S3 bucket.</span></span> <span data-ttu-id="253eb-304">Hello kroków opisanych w hello Amazon dokumentacji eksportowanie wystąpień EC2 Amazon tooinstall hello Amazon EC2 interfejsu wiersza polecenia (CLI) narzędzie i uruchom plik VHD tooa hello-wystąpienie export-polecenia Utwórz zadanie tooexport hello EC2 wystąpienia.</span><span class="sxs-lookup"><span data-stu-id="253eb-304">Follow hello steps described in hello Amazon documentation for Exporting Amazon EC2 Instances tooinstall hello Amazon EC2 command-line interface (CLI) tool and run hello create-instance-export-task command tooexport hello EC2 instance tooa VHD file.</span></span> <span data-ttu-id="253eb-305">Należy się toouse **wirtualnego dysku twardego** dla hello dysku &#95; obraz &#95; FORMAT zmiennej podczas uruchamiania hello **tworzenie — wystąpienie export zadania** polecenia.</span><span class="sxs-lookup"><span data-stu-id="253eb-305">Be sure toouse **VHD** for hello DISK&#95;IMAGE&#95;FORMAT variable when running hello **create-instance-export-task** command.</span></span> <span data-ttu-id="253eb-306">Witaj wyeksportowany plik wirtualnego dysku twardego jest zapisywany w zasobniku hello Amazon S3, którą określisz podczas tego procesu.</span><span class="sxs-lookup"><span data-stu-id="253eb-306">hello exported VHD file is saved in hello Amazon S3 bucket you designate during that process.</span></span>

    ```
    aws ec2 create-instance-export-task --instance-id ID --target-environment TARGET_ENVIRONMENT \
      --export-to-s3-task DiskImageFormat=DISK_IMAGE_FORMAT,ContainerFormat=ova,S3Bucket=BUCKET,S3Prefix=PREFIX
    ```

2. <span data-ttu-id="253eb-307">Pobierz plik VHD hello z hello przedział S3.</span><span class="sxs-lookup"><span data-stu-id="253eb-307">Download hello VHD file from hello S3 bucket.</span></span> <span data-ttu-id="253eb-308">Plik VHD wybierz hello, następnie **akcje** > **Pobierz**.</span><span class="sxs-lookup"><span data-stu-id="253eb-308">Select hello VHD file, then **Actions** > **Download**.</span></span>

    ![][3]

##### <a name="copy-a-vhd-from-other-non-azure-cloud"></a><span data-ttu-id="253eb-309">Skopiuj wirtualny dysk twardy z innych chmury Azure z systemem innym niż</span><span class="sxs-lookup"><span data-stu-id="253eb-309">Copy a VHD from other non-Azure cloud</span></span>
<span data-ttu-id="253eb-310">W przypadku migracji z tooAzure — z usługi Azure Cloud Storage wirtualnego dysku twardego, należy wyeksportować hello katalogu lokalnego tooa wirtualnego dysku twardego.</span><span class="sxs-lookup"><span data-stu-id="253eb-310">If you are migrating VHD from non-Azure Cloud Storage tooAzure, you must first export hello VHD tooa local directory.</span></span> <span data-ttu-id="253eb-311">Skopiować hello źródła pełną ścieżkę katalogu lokalnego hello przechowywania wirtualnego dysku twardego.</span><span class="sxs-lookup"><span data-stu-id="253eb-311">Copy hello complete source path of hello local directory where VHD is stored.</span></span>

##### <a name="copy-a-vhd-from-on-premises"></a><span data-ttu-id="253eb-312">Skopiuj wirtualny dysk twardy z lokalnymi</span><span class="sxs-lookup"><span data-stu-id="253eb-312">Copy a VHD from on-premises</span></span>
<span data-ttu-id="253eb-313">W przypadku migracji ze środowiska lokalnego wirtualnego dysku twardego, konieczne będzie ścieżki źródłowej pełną hello przechowywania wirtualnego dysku twardego.</span><span class="sxs-lookup"><span data-stu-id="253eb-313">If you are migrating VHD from an on-premises environment, you will need hello complete source path where VHD is stored.</span></span> <span data-ttu-id="253eb-314">Ścieżka źródłowa Hello może być serwerem lokalizacji lub w udziale plików.</span><span class="sxs-lookup"><span data-stu-id="253eb-314">hello source path could be a server location or file share.</span></span>

#### <a name="step-2-create-hello-destination-for-your-vhd"></a><span data-ttu-id="253eb-315">Krok 2.</span><span class="sxs-lookup"><span data-stu-id="253eb-315">Step 2.</span></span> <span data-ttu-id="253eb-316">Utwórz lokalizację docelową hello dysk VHD</span><span class="sxs-lookup"><span data-stu-id="253eb-316">Create hello destination for your VHD</span></span>
<span data-ttu-id="253eb-317">Utwórz konto magazynu do przechowywania dyski VHD.</span><span class="sxs-lookup"><span data-stu-id="253eb-317">Create a storage account for maintaining your VHDs.</span></span> <span data-ttu-id="253eb-318">Należy wziąć pod uwagę następujące punkty podczas planowania miejsca hello toostore dyski VHD:</span><span class="sxs-lookup"><span data-stu-id="253eb-318">Consider hello following points when planning where toostore your VHDs:</span></span>

* <span data-ttu-id="253eb-319">Witaj docelowe konto magazynu może być standard lub premium magazynu w zależności od wymagań aplikacji.</span><span class="sxs-lookup"><span data-stu-id="253eb-319">hello target storage account could be standard or premium storage depending on your application requirement.</span></span>
* <span data-ttu-id="253eb-320">region konta magazynu Hello musi być taki sam jak magazyn w warstwie Premium obsługuje maszyny wirtualne Azure utworzysz w ostatnim etapie hello.</span><span class="sxs-lookup"><span data-stu-id="253eb-320">hello storage account region must be same as Premium Storage capable Azure VMs you will create in hello final stage.</span></span> <span data-ttu-id="253eb-321">Można skopiować nowego konta magazynu tooa lub hello toouse planu tego samego konta magazynu na podstawie Twoich potrzeb.</span><span class="sxs-lookup"><span data-stu-id="253eb-321">You could copy tooa new storage account, or plan toouse hello same storage account based on your needs.</span></span>
* <span data-ttu-id="253eb-322">Skopiuj i Zapisz klucz konta magazynu hello konto magazynu docelowego hello hello następny etap.</span><span class="sxs-lookup"><span data-stu-id="253eb-322">Copy and save hello storage account key of hello destination storage account for hello next stage.</span></span>

<span data-ttu-id="253eb-323">Stanowczo zaleca się możesz przeniesienie wszystkich danych magazyn w warstwie premium toouse obciążeń produkcyjnych.</span><span class="sxs-lookup"><span data-stu-id="253eb-323">We strongly recommend you moving all data for production workload toouse premium storage.</span></span>

#### <a name="step-3-upload-hello-vhd-tooazure-storage"></a><span data-ttu-id="253eb-324">Krok 3.</span><span class="sxs-lookup"><span data-stu-id="253eb-324">Step 3.</span></span> <span data-ttu-id="253eb-325">Przekaż hello wirtualnego dysku twardego tooAzure magazynu</span><span class="sxs-lookup"><span data-stu-id="253eb-325">Upload hello VHD tooAzure Storage</span></span>
<span data-ttu-id="253eb-326">Teraz, gdy dysk VHD znajdują się w katalogu lokalnym hello, można użyć narzędzia AzCopy lub AzurePowerShell tooupload hello VHD pliku tooAzure magazynu.</span><span class="sxs-lookup"><span data-stu-id="253eb-326">Now that you have your VHD in hello local directory, you can use AzCopy or AzurePowerShell tooupload hello .vhd file tooAzure Storage.</span></span> <span data-ttu-id="253eb-327">Obie te opcje są dostępne w tym miejscu:</span><span class="sxs-lookup"><span data-stu-id="253eb-327">Both options are provided here:</span></span>

##### <a name="option-1-using-azure-powershell-add-azurevhd-tooupload-hello-vhd-file"></a><span data-ttu-id="253eb-328">Opcja 1: Przy użyciu programu Azure PowerShell Add-AzureVhd tooupload hello pliku VHD</span><span class="sxs-lookup"><span data-stu-id="253eb-328">Option 1: Using Azure PowerShell Add-AzureVhd tooupload hello .vhd file</span></span>

```powershell
Add-AzureVhd [-Destination] <Uri> [-LocalFilePath] <FileInfo>
```

<span data-ttu-id="253eb-329">Przykład <Uri> może być ***"https://storagesample.blob.core.windows.net/mycontainer/blob1.vhd"***.</span><span class="sxs-lookup"><span data-stu-id="253eb-329">An example <Uri> might be ***"https://storagesample.blob.core.windows.net/mycontainer/blob1.vhd"***.</span></span> <span data-ttu-id="253eb-330">Przykład <FileInfo> może być ***"C:\path\to\upload.vhd"***.</span><span class="sxs-lookup"><span data-stu-id="253eb-330">An example <FileInfo> might be ***"C:\path\to\upload.vhd"***.</span></span>

##### <a name="option-2-using-azcopy-tooupload-hello-vhd-file"></a><span data-ttu-id="253eb-331">Opcja 2: Przy użyciu pliku VHD hello tooupload AzCopy</span><span class="sxs-lookup"><span data-stu-id="253eb-331">Option 2: Using AzCopy tooupload hello .vhd file</span></span>
<span data-ttu-id="253eb-332">Przy użyciu narzędzia AzCopy, możesz wysłać hello wirtualnego dysku twardego za pośrednictwem hello Internet.</span><span class="sxs-lookup"><span data-stu-id="253eb-332">Using AzCopy, you can easily upload hello VHD over hello Internet.</span></span> <span data-ttu-id="253eb-333">W zależności od rozmiaru hello hello wirtualne dyski twarde to może potrwać.</span><span class="sxs-lookup"><span data-stu-id="253eb-333">Depending on hello size of hello VHDs, this may take time.</span></span> <span data-ttu-id="253eb-334">Należy pamiętać limity konta magazynu toocheck hello w wejście/wyjście, korzystając z tej opcji.</span><span class="sxs-lookup"><span data-stu-id="253eb-334">Remember toocheck hello storage account ingress/egress limits when using this option.</span></span> <span data-ttu-id="253eb-335">Zobacz [cele dotyczące wydajności i skalowalności magazynu Azure](storage-scalability-targets.md) szczegółowe informacje.</span><span class="sxs-lookup"><span data-stu-id="253eb-335">See [Azure Storage Scalability and Performance Targets](storage-scalability-targets.md) for details.</span></span>

1. <span data-ttu-id="253eb-336">Pobierz i zainstaluj narzędzie AzCopy stąd: [najnowszą wersję programu AzCopy](http://aka.ms/downloadazcopy)</span><span class="sxs-lookup"><span data-stu-id="253eb-336">Download and install AzCopy from here: [Latest version of AzCopy](http://aka.ms/downloadazcopy)</span></span>
2. <span data-ttu-id="253eb-337">Otwórz program Azure PowerShell i folder przejdź toohello, w którym zainstalowano narzędzia AzCopy.</span><span class="sxs-lookup"><span data-stu-id="253eb-337">Open Azure PowerShell and go toohello folder where AzCopy is installed.</span></span>
3. <span data-ttu-id="253eb-338">Użyj hello następujące polecenie plik VHD hello toocopy z "Source" za "Miejsce docelowe".</span><span class="sxs-lookup"><span data-stu-id="253eb-338">Use hello following command toocopy hello VHD file from "Source" too"Destination".</span></span>

    ```azcopy
    AzCopy /Source: <source> /SourceKey: <source-account-key> /Dest: <destination> /DestKey: <dest-account-key> /BlobType:page /Pattern: <file-name>
    ```

    <span data-ttu-id="253eb-339">Przykład:</span><span class="sxs-lookup"><span data-stu-id="253eb-339">Example:</span></span>

    ```azcopy
    AzCopy /Source:https://sourceaccount.blob.core.windows.net/mycontainer1 /SourceKey:key1 /Dest:https://destaccount.blob.core.windows.net/mycontainer2 /DestKey:key2 /BlobType:page /Pattern:abc.vhd
    ```

    <span data-ttu-id="253eb-340">Poniżej przedstawiono opisy parametrów hello używana w hello polecenia programu AzCopy:</span><span class="sxs-lookup"><span data-stu-id="253eb-340">Here are descriptions of hello parameters used in hello AzCopy command:</span></span>

   * <span data-ttu-id="253eb-341">**/ Źródło:  *&lt;źródła&gt;:***  lokalizację folderu hello lub adresu URL kontenera magazynu zawierającego hello wirtualnego dysku twardego.</span><span class="sxs-lookup"><span data-stu-id="253eb-341">**/Source: *&lt;source&gt;:*** Location of hello folder or storage container URL that contains hello VHD.</span></span>
   * <span data-ttu-id="253eb-342">**/ SourceKey:  *&lt;źródła konta klucza&gt;:***  klucz konta magazynu z konta magazynu źródłowego hello.</span><span class="sxs-lookup"><span data-stu-id="253eb-342">**/SourceKey: *&lt;source-account-key&gt;:*** Storage account key of hello source storage account.</span></span>
   * <span data-ttu-id="253eb-343">**/ Dest:  *&lt;docelowego&gt;:***  toocopy adresu URL kontenera magazynu hello wirtualnego dysku twardego.</span><span class="sxs-lookup"><span data-stu-id="253eb-343">**/Dest: *&lt;destination&gt;:*** Storage container URL toocopy hello VHD to.</span></span>
   * <span data-ttu-id="253eb-344">**/ DestKey:  *&lt;dest konta klucza&gt;:***  klucz konta magazynu konto magazynu docelowego hello.</span><span class="sxs-lookup"><span data-stu-id="253eb-344">**/DestKey: *&lt;dest-account-key&gt;:*** Storage account key of hello destination storage account.</span></span>
   * <span data-ttu-id="253eb-345">**/ BlobType: strony:** Określa, że docelowy hello stronicowych obiektów blob.</span><span class="sxs-lookup"><span data-stu-id="253eb-345">**/BlobType: page:** Specifies that hello destination is a page blob.</span></span>
   * <span data-ttu-id="253eb-346">**/ Wzorzec:  *&lt;nazwę pliku&gt;:***  Określ nazwę pliku hello hello toocopy wirtualnego dysku twardego.</span><span class="sxs-lookup"><span data-stu-id="253eb-346">**/Pattern: *&lt;file-name&gt;:*** Specify hello file name of hello VHD toocopy.</span></span>

<span data-ttu-id="253eb-347">Aby uzyskać więcej informacji na temat używania narzędzia AzCopy narzędzie, zobacz [Transfer danych za pomocą wiersza polecenia Azcopy hello](storage-use-azcopy.md).</span><span class="sxs-lookup"><span data-stu-id="253eb-347">For details on using AzCopy tool, see [Transfer data with hello AzCopy Command-Line Utility](storage-use-azcopy.md).</span></span>

##### <a name="other-options-for-uploading-a-vhd"></a><span data-ttu-id="253eb-348">Inne opcje przekazywanie wirtualnego dysku twardego</span><span class="sxs-lookup"><span data-stu-id="253eb-348">Other options for uploading a VHD</span></span>
<span data-ttu-id="253eb-349">Możesz również przekazywać przy użyciu jednej z powitania po oznacza, że konto magazynu wirtualnego dysku twardego tooyour:</span><span class="sxs-lookup"><span data-stu-id="253eb-349">You can also upload a VHD tooyour storage account using one of hello following means:</span></span>

* [<span data-ttu-id="253eb-350">Obiektu Blob magazynu Azure kopiowania interfejsu API</span><span class="sxs-lookup"><span data-stu-id="253eb-350">Azure Storage Copy Blob API</span></span>](https://msdn.microsoft.com/library/azure/dd894037.aspx)
* [<span data-ttu-id="253eb-351">Obiekty BLOB magazynu Azure Explorer przekazywania</span><span class="sxs-lookup"><span data-stu-id="253eb-351">Azure Storage Explorer Uploading Blobs</span></span>](https://azurestorageexplorer.codeplex.com/)
* [<span data-ttu-id="253eb-352">Dokumentacja interfejsu API REST usługi Import/Eksport magazynu</span><span class="sxs-lookup"><span data-stu-id="253eb-352">Storage Import/Export Service REST API Reference</span></span>](https://msdn.microsoft.com/library/dn529096.aspx)

> [!NOTE]
> <span data-ttu-id="253eb-353">Zaleca się za pomocą usługi Import/eksport, jeśli szacowany czas przekazywania jest dłuższa niż 7 dni.</span><span class="sxs-lookup"><span data-stu-id="253eb-353">We recommend using Import/Export Service if estimated uploading time is longer than 7 days.</span></span> <span data-ttu-id="253eb-354">Można użyć [DataTransferSpeedCalculator](https://github.com/Azure-Samples/storage-dotnet-import-export-job-management/blob/master/DataTransferSpeedCalculator.html) tooestimate hello czasu z jednostki rozmiaru i transferu danych.</span><span class="sxs-lookup"><span data-stu-id="253eb-354">You can use [DataTransferSpeedCalculator](https://github.com/Azure-Samples/storage-dotnet-import-export-job-management/blob/master/DataTransferSpeedCalculator.html) tooestimate hello time from data size and transfer unit.</span></span>
>
> <span data-ttu-id="253eb-355">Import/Eksport można używać konta standard storage tooa toocopy.</span><span class="sxs-lookup"><span data-stu-id="253eb-355">Import/Export can be used toocopy tooa standard storage account.</span></span> <span data-ttu-id="253eb-356">Konieczne będzie toocopy z konta magazynu toopremium standard storage przy użyciu narzędzia, takiego jak narzędzie AzCopy.</span><span class="sxs-lookup"><span data-stu-id="253eb-356">You will need toocopy from standard storage toopremium storage account using a tool like AzCopy.</span></span>
>
>

## <span data-ttu-id="253eb-357"><a name="create-azure-virtual-machine-using-premium-storage"></a>Tworzenie maszyn wirtualnych platformy Azure przy użyciu magazyn w warstwie Premium</span><span class="sxs-lookup"><span data-stu-id="253eb-357"><a name="create-azure-virtual-machine-using-premium-storage"></a>Create Azure VMs using Premium Storage</span></span>
<span data-ttu-id="253eb-358">Po hello wirtualnego dysku twardego jest przekazany lub kopiowane toohello żądanego konta magazynu, wykonaj instrukcje hello w tej sekcji tooregister hello wirtualnego dysku twardego jako obraz systemu operacyjnego lub dysku systemu operacyjnego, w zależności od scenariusza, a następnie utwórz wystąpienie maszyny Wirtualnej z niego.</span><span class="sxs-lookup"><span data-stu-id="253eb-358">After hello VHD is uploaded or copied toohello desired storage account, follow hello instructions in this section tooregister hello VHD as an OS image, or OS disk depending on your scenario and then create a VM instance from it.</span></span> <span data-ttu-id="253eb-359">dysk danych Hello wirtualnego dysku twardego może być dołączone toohello maszyny Wirtualnej, po jego utworzeniu.</span><span class="sxs-lookup"><span data-stu-id="253eb-359">hello data disk VHD can be attached toohello VM once it is created.</span></span>
<span data-ttu-id="253eb-360">Przykładowy skrypt migracji znajduje się na końcu hello w tej sekcji.</span><span class="sxs-lookup"><span data-stu-id="253eb-360">A sample migration script is provided at hello end of this section.</span></span> <span data-ttu-id="253eb-361">Ten prosty skrypt nie jest zgodna wszystkie scenariusze.</span><span class="sxs-lookup"><span data-stu-id="253eb-361">This simple script does not match all scenarios.</span></span> <span data-ttu-id="253eb-362">Może być konieczne tooupdate hello skryptu toomatch z konkretnego scenariusza.</span><span class="sxs-lookup"><span data-stu-id="253eb-362">You may need tooupdate hello script toomatch with your specific scenario.</span></span> <span data-ttu-id="253eb-363">poniżej toosee, jeśli ten skrypt stosuje scenariuszu tooyour [A przykładowy skrypt migracji](#a-sample-migration-script).</span><span class="sxs-lookup"><span data-stu-id="253eb-363">toosee if this script applies tooyour scenario, see below [A Sample Migration Script](#a-sample-migration-script).</span></span>

### <a name="checklist"></a><span data-ttu-id="253eb-364">Lista kontrolna</span><span class="sxs-lookup"><span data-stu-id="253eb-364">Checklist</span></span>
1. <span data-ttu-id="253eb-365">Zaczekaj na wszystkie dyski VHD hello Kopiowanie zostało ukończone.</span><span class="sxs-lookup"><span data-stu-id="253eb-365">Wait until all hello VHD disks copying is complete.</span></span>
2. <span data-ttu-id="253eb-366">Upewnij się, że magazyn w warstwie Premium jest dostępna w regionie hello, które w przypadku migracji do.</span><span class="sxs-lookup"><span data-stu-id="253eb-366">Make sure Premium Storage is available in hello region you are migrating to.</span></span>
3. <span data-ttu-id="253eb-367">Zdecyduj, hello nowej serii maszyn wirtualnych, które będą używane.</span><span class="sxs-lookup"><span data-stu-id="253eb-367">Decide hello new VM series you will be using.</span></span> <span data-ttu-id="253eb-368">Powinna być funkcją Magazyn w warstwie Premium i hello rozmiar powinien mieścić się w zależności od dostępności hello w regionie hello i zgodnie z potrzebami.</span><span class="sxs-lookup"><span data-stu-id="253eb-368">It should be a Premium Storage capable, and hello size should be depending on hello availability in hello region and based on your needs.</span></span>
4. <span data-ttu-id="253eb-369">Zdecyduj, hello dokładny rozmiar maszyny Wirtualnej, który będzie używany.</span><span class="sxs-lookup"><span data-stu-id="253eb-369">Decide hello exact VM size you will use.</span></span> <span data-ttu-id="253eb-370">Rozmiar maszyny Wirtualnej musi toobe toosupport wystarczająco duży hello liczba dysków danych, do których masz.</span><span class="sxs-lookup"><span data-stu-id="253eb-370">VM size needs toobe large enough toosupport hello number of data disks you have.</span></span> <span data-ttu-id="253eb-371">Na przykład</span><span class="sxs-lookup"><span data-stu-id="253eb-371">E.g.</span></span> <span data-ttu-id="253eb-372">Jeśli masz 4 dyski danych hello maszyna wirtualna musi mieć co najmniej 2 rdzeni.</span><span class="sxs-lookup"><span data-stu-id="253eb-372">if you have 4 data disks, hello VM must have 2 or more cores.</span></span> <span data-ttu-id="253eb-373">Należy również rozważyć przetwarzania zasilania, pamięci i musi przepustowości sieci.</span><span class="sxs-lookup"><span data-stu-id="253eb-373">Also, consider processing power, memory and network bandwidth needs.</span></span>
5. <span data-ttu-id="253eb-374">Tworzenie konta Premium Storage w obszarze docelowym hello.</span><span class="sxs-lookup"><span data-stu-id="253eb-374">Create a Premium Storage account in hello target region.</span></span> <span data-ttu-id="253eb-375">To jest konto hello użyjesz hello nowej maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="253eb-375">This is hello account you will use for hello new VM.</span></span>
6. <span data-ttu-id="253eb-376">Ma hello wirtualna szczegóły bieżącej przydatną tym hello listę dysków i odpowiednie obiekty BLOB dysków VHD.</span><span class="sxs-lookup"><span data-stu-id="253eb-376">Have hello current VM details handy, including hello list of disks and corresponding VHD blobs.</span></span>

<span data-ttu-id="253eb-377">Przygotowanie aplikacji dla przestoju.</span><span class="sxs-lookup"><span data-stu-id="253eb-377">Prepare your application for downtime.</span></span> <span data-ttu-id="253eb-378">toodo czystą migracji należy toostop przetwarzania hello w bieżącym systemie hello.</span><span class="sxs-lookup"><span data-stu-id="253eb-378">toodo a clean migration, you have toostop all hello processing in hello current system.</span></span> <span data-ttu-id="253eb-379">Następnie możesz pobrać go tooconsistent stanu, które można migrować toohello na nowej platformie.</span><span class="sxs-lookup"><span data-stu-id="253eb-379">Only then you can get it tooconsistent state which you can migrate toohello new platform.</span></span> <span data-ttu-id="253eb-380">Czas trwania przestoju będzie zależeć od hello ilości danych w hello toomigrate dysków.</span><span class="sxs-lookup"><span data-stu-id="253eb-380">Downtime duration will depend on hello amount of data in hello disks toomigrate.</span></span>

> [!NOTE]
> <span data-ttu-id="253eb-381">W przypadku tworzenia maszyny Wirtualnej platformy Azure Resource Manager z specjalne dysku VHD, można znaleźć zbyt[ten szablon](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-specialized-vhd) wdrażania Menedżera zasobów maszyny Wirtualnej przy użyciu istniejącego dysku.</span><span class="sxs-lookup"><span data-stu-id="253eb-381">If you are creating an Azure Resource Manager VM from a specialized VHD Disk, please refer too[this template](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-specialized-vhd) for deploying Resource Manager VM using existing disk.</span></span>
>
>

### <a name="register-your-vhd"></a><span data-ttu-id="253eb-382">Zarejestruj dysk VHD</span><span class="sxs-lookup"><span data-stu-id="253eb-382">Register your VHD</span></span>
<span data-ttu-id="253eb-383">toocreate Maszynę wirtualną z wirtualnego dysku twardego systemu operacyjnego lub tooattach tooa dysku danych nowej maszyny Wirtualnej, najpierw należy zarejestrować je.</span><span class="sxs-lookup"><span data-stu-id="253eb-383">toocreate a VM from OS VHD or tooattach a data disk tooa new VM, you must first register them.</span></span> <span data-ttu-id="253eb-384">Wykonaj poniższe kroki w zależności od scenariusza z wirtualnego dysku twardego.</span><span class="sxs-lookup"><span data-stu-id="253eb-384">Follow steps below depending on your VHD's scenario.</span></span>

#### <a name="generalized-operating-system-vhd-toocreate-multiple-azure-vm-instances"></a><span data-ttu-id="253eb-385">Uogólniony wirtualny dysk twardy systemu operacyjnego toocreate wielu wystąpień maszyny Wirtualnej Azure</span><span class="sxs-lookup"><span data-stu-id="253eb-385">Generalized Operating System VHD toocreate multiple Azure VM instances</span></span>
<span data-ttu-id="253eb-386">Po uogólniony obraz systemu operacyjnego, wirtualny dysk twardy jest przekazywane toohello konta magazynu, należy zarejestrować go w formie **obrazu maszyny Wirtualnej Azure** tak, aby z niego można utworzyć co najmniej jedno wystąpienie maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="253eb-386">After generalized OS image VHD is uploaded toohello storage account, register it as an **Azure VM Image** so that you can create one or more VM instances from it.</span></span> <span data-ttu-id="253eb-387">Użyj powitania po tooregister poleceń cmdlet programu PowerShell dysk VHD jako obrazu systemu operacyjnego maszyny Wirtualnej Azure.</span><span class="sxs-lookup"><span data-stu-id="253eb-387">Use hello following PowerShell cmdlets tooregister your VHD as an Azure VM OS image.</span></span> <span data-ttu-id="253eb-388">Podaj adres URL ukończenia kontenera hello gdzie wirtualnego dysku twardego został skopiowany do.</span><span class="sxs-lookup"><span data-stu-id="253eb-388">Provide hello complete container URL where VHD was copied to.</span></span>

```powershell
Add-AzureVMImage -ImageName "OSImageName" -MediaLocation "https://storageaccount.blob.core.windows.net/vhdcontainer/osimage.vhd" -OS Windows
```

<span data-ttu-id="253eb-389">Skopiuj i Zapisz nazwę hello tego nowego obrazu maszyny Wirtualnej Azure.</span><span class="sxs-lookup"><span data-stu-id="253eb-389">Copy and save hello name of this new Azure VM Image.</span></span> <span data-ttu-id="253eb-390">W powyższym przykładzie hello, jest *OSImageName*.</span><span class="sxs-lookup"><span data-stu-id="253eb-390">In hello example above, it is *OSImageName*.</span></span>

#### <a name="unique-operating-system-vhd-toocreate-a-single-azure-vm-instance"></a><span data-ttu-id="253eb-391">Unikatowy wirtualnego dysku twardego systemu operacyjnego toocreate jedno wystąpienie maszyny Wirtualnej Azure</span><span class="sxs-lookup"><span data-stu-id="253eb-391">Unique Operating System VHD toocreate a single Azure VM instance</span></span>
<span data-ttu-id="253eb-392">Hello unikatowy wirtualnego dysku twardego systemu operacyjnego — po magazynu przekazana toohello konto, zarejestruj go w formie **dysk systemu operacyjnego Azure** tak, aby z niego można utworzyć wystąpienia maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="253eb-392">After hello unique OS VHD is uploaded toohello storage account, register it as an **Azure OS Disk** so that you can create a VM instance from it.</span></span> <span data-ttu-id="253eb-393">Użyj tych tooregister poleceń cmdlet programu PowerShell dysk VHD jako dysk systemu operacyjnego Azure.</span><span class="sxs-lookup"><span data-stu-id="253eb-393">Use these PowerShell cmdlets tooregister your VHD as an Azure OS Disk.</span></span> <span data-ttu-id="253eb-394">Podaj adres URL ukończenia kontenera hello gdzie wirtualnego dysku twardego został skopiowany do.</span><span class="sxs-lookup"><span data-stu-id="253eb-394">Provide hello complete container URL where VHD was copied to.</span></span>

```powershell
Add-AzureDisk -DiskName "OSDisk" -MediaLocation "https://storageaccount.blob.core.windows.net/vhdcontainer/osdisk.vhd" -Label "My OS Disk" -OS "Windows"
```

<span data-ttu-id="253eb-395">Skopiuj i Zapisz nazwę hello ten nowy dysk systemu operacyjnego Azure.</span><span class="sxs-lookup"><span data-stu-id="253eb-395">Copy and save hello name of this new Azure OS Disk.</span></span> <span data-ttu-id="253eb-396">W powyższym przykładzie hello, jest *OSDisk*.</span><span class="sxs-lookup"><span data-stu-id="253eb-396">In hello example above, it is *OSDisk*.</span></span>

#### <a name="data-disk-vhd-toobe-attached-toonew-azure-vm-instances"></a><span data-ttu-id="253eb-397">Dane dysku VHD toobe dołączony toonew wystąpienia maszyny Wirtualnej Azure</span><span class="sxs-lookup"><span data-stu-id="253eb-397">Data disk VHD toobe attached toonew Azure VM instance(s)</span></span>
<span data-ttu-id="253eb-398">Po hello danych dysk wirtualny dysk twardy jest przekazany konta toostorage, zarejestruj go jako dysk danych Azure, dzięki czemu mogą być dołączone tooyour nowej serii DS, DSv2 serii lub wystąpienie maszyny Wirtualnej Azure serii GS.</span><span class="sxs-lookup"><span data-stu-id="253eb-398">After hello data disk VHD is uploaded toostorage account, register it as an Azure Data Disk so that it can be attached tooyour new DS Series, DSv2 series or GS Series Azure VM instance.</span></span>

<span data-ttu-id="253eb-399">Użyj tych tooregister poleceń cmdlet programu PowerShell dysk VHD jako dysk danych Azure.</span><span class="sxs-lookup"><span data-stu-id="253eb-399">Use these PowerShell cmdlets tooregister your VHD as an Azure Data Disk.</span></span> <span data-ttu-id="253eb-400">Podaj adres URL ukończenia kontenera hello gdzie wirtualnego dysku twardego został skopiowany do.</span><span class="sxs-lookup"><span data-stu-id="253eb-400">Provide hello complete container URL where VHD was copied to.</span></span>

```powershell
Add-AzureDisk -DiskName "DataDisk" -MediaLocation "https://storageaccount.blob.core.windows.net/vhdcontainer/datadisk.vhd" -Label "My Data Disk"
```

<span data-ttu-id="253eb-401">Skopiuj i Zapisz nazwę hello ten nowy dysk danych Azure.</span><span class="sxs-lookup"><span data-stu-id="253eb-401">Copy and save hello name of this new Azure Data Disk.</span></span> <span data-ttu-id="253eb-402">W powyższym przykładzie hello, jest *DataDisk*.</span><span class="sxs-lookup"><span data-stu-id="253eb-402">In hello example above, it is *DataDisk*.</span></span>

### <a name="create-a-premium-storage-capable-vm"></a><span data-ttu-id="253eb-403">Tworzenie maszyny Wirtualnej obsługuje magazyn w warstwie Premium</span><span class="sxs-lookup"><span data-stu-id="253eb-403">Create a Premium Storage capable VM</span></span>
<span data-ttu-id="253eb-404">Raz hello obrazu systemu operacyjnego lub dysku systemu operacyjnego są rejestrowane, tworzenie nowej serii DS, dsv2 lub GS-series maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="253eb-404">Once hello OS image or OS disk are registered, create a new DS-series, DSv2-series or GS-series VM.</span></span> <span data-ttu-id="253eb-405">Będziesz używać obrazu systemu operacyjnego hello lub nazwa dysku systemu operacyjnego, który został zarejestrowany.</span><span class="sxs-lookup"><span data-stu-id="253eb-405">You will be using hello operating system image or operating system disk name that you registered.</span></span> <span data-ttu-id="253eb-406">Wybierz hello typu maszyny Wirtualnej z warstwy Premium Storage hello.</span><span class="sxs-lookup"><span data-stu-id="253eb-406">Select hello VM type from hello Premium Storage tier.</span></span> <span data-ttu-id="253eb-407">W poniższym przykładzie użyto hello *Standard_DS2* rozmiar maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="253eb-407">In example below, we are using hello *Standard_DS2* VM size.</span></span>

> [!NOTE]
> <span data-ttu-id="253eb-408">Zaktualizuj toomake rozmiar dysku hello taka sama pojemność i wydajność wymagań i hello rozmiary dysku platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="253eb-408">Update hello disk size toomake sure it matches your capacity and performance requirements and hello available Azure disk sizes.</span></span>
>
>

<span data-ttu-id="253eb-409">Polecenia cmdlet programu PowerShell krok po kroku hello wykonaj poniżej toocreate hello nowej maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="253eb-409">Follow hello step by step PowerShell cmdlets below toocreate hello new VM.</span></span> <span data-ttu-id="253eb-410">Najpierw należy ustawić hello typowe parametry:</span><span class="sxs-lookup"><span data-stu-id="253eb-410">First, set hello common parameters:</span></span>

```powershell
$serviceName = "yourVM"
$location = "location-name" (e.g., West US)
$vmSize ="Standard_DS2"
$adminUser = "youradmin"
$adminPassword = "yourpassword"
$vmName ="yourVM"
$vmSize = "Standard_DS2"
```

<span data-ttu-id="253eb-411">Najpierw należy utworzyć usługi w chmurze w którym będą obsługiwać nowych maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="253eb-411">First, create a cloud service in which you will be hosting your new VMs.</span></span>

```powershell
New-AzureService -ServiceName $serviceName -Location $location
```

<span data-ttu-id="253eb-412">Następnie w zależności od scenariusza, utworzyć wystąpienie maszyny Wirtualnej Azure hello hello obrazu systemu operacyjnego lub dysku systemu operacyjnego, który został zarejestrowany.</span><span class="sxs-lookup"><span data-stu-id="253eb-412">Next, depending on your scenario, create hello Azure VM instance from either hello OS Image or OS Disk that you registered.</span></span>

#### <a name="generalized-operating-system-vhd-toocreate-multiple-azure-vm-instances"></a><span data-ttu-id="253eb-413">Uogólniony wirtualny dysk twardy systemu operacyjnego toocreate wielu wystąpień maszyny Wirtualnej Azure</span><span class="sxs-lookup"><span data-stu-id="253eb-413">Generalized Operating System VHD toocreate multiple Azure VM instances</span></span>
<span data-ttu-id="253eb-414">Utwórz co najmniej jednego nowego wystąpienia maszyny Wirtualnej Azure serii DS przy użyciu hello hello **obrazu systemu operacyjnego Azure** który został zarejestrowany.</span><span class="sxs-lookup"><span data-stu-id="253eb-414">Create hello one or more new DS Series Azure VM instances using hello **Azure OS Image** that you registered.</span></span> <span data-ttu-id="253eb-415">Określ nazwę tego obrazu systemu operacyjnego w konfiguracji maszyny Wirtualnej hello, podczas tworzenia nowej maszyny Wirtualnej, jak pokazano poniżej.</span><span class="sxs-lookup"><span data-stu-id="253eb-415">Specify this OS Image name in hello VM configuration when creating new VM as shown below.</span></span>

```powershell
$OSImage = Get-AzureVMImage –ImageName "OSImageName"

$vm = New-AzureVMConfig -Name $vmName –InstanceSize $vmSize -ImageName $OSImage.ImageName

Add-AzureProvisioningConfig -Windows –AdminUserName $adminUser -Password $adminPassword –VM $vm

New-AzureVM -ServiceName $serviceName -VM $vm
```

#### <a name="unique-operating-system-vhd-toocreate-a-single-azure-vm-instance"></a><span data-ttu-id="253eb-416">Unikatowy wirtualnego dysku twardego systemu operacyjnego toocreate jedno wystąpienie maszyny Wirtualnej Azure</span><span class="sxs-lookup"><span data-stu-id="253eb-416">Unique Operating System VHD toocreate a single Azure VM instance</span></span>
<span data-ttu-id="253eb-417">Utwórz wystąpienie maszyny Wirtualnej Azure nowej serii DS przy użyciu hello **dysk systemu operacyjnego Azure** który został zarejestrowany.</span><span class="sxs-lookup"><span data-stu-id="253eb-417">Create a new DS series Azure VM instance using hello **Azure OS Disk** that you registered.</span></span> <span data-ttu-id="253eb-418">Określ w konfiguracji maszyny Wirtualnej hello ta nazwa dysku systemu operacyjnego, podczas tworzenia hello nowej maszyny Wirtualnej, jak pokazano poniżej.</span><span class="sxs-lookup"><span data-stu-id="253eb-418">Specify this OS Disk name in hello VM configuration when creating hello new VM as shown below.</span></span>

```powershell
$OSDisk = Get-AzureDisk –DiskName "OSDisk"

$vm = New-AzureVMConfig -Name $vmName -InstanceSize $vmSize -DiskName $OSDisk.DiskName

New-AzureVM -ServiceName $serviceName –VM $vm
```

<span data-ttu-id="253eb-419">Określ inne informacje maszyny Wirtualnej platformy Azure, takich jak usługi w chmurze, region, konta magazynu, zestawu dostępności i zasad buforowania.</span><span class="sxs-lookup"><span data-stu-id="253eb-419">Specify other Azure VM information, such as a cloud service, region, storage account, availability set, and caching policy.</span></span> <span data-ttu-id="253eb-420">Zauważ, że hello wystąpienia maszyny Wirtualnej musi być wspólnie z skojarzonego z nim systemu operacyjnego lub dysków z danymi, więc hello wybrane chmury usługi, regionu i konto magazynu muszą być wartościami hello tej samej lokalizacji co hello podstawowych dysków VHD tych dysków.</span><span class="sxs-lookup"><span data-stu-id="253eb-420">Note that hello VM instance must be co-located with associated operating system or data disks, so hello selected cloud service, region and storage account must all be in hello same location as hello underlying VHDs of those disks.</span></span>

### <a name="attach-data-disk"></a><span data-ttu-id="253eb-421">Dołączanie dysku danych</span><span class="sxs-lookup"><span data-stu-id="253eb-421">Attach data disk</span></span>
<span data-ttu-id="253eb-422">Ponadto jeśli zarejestrowano danych na dysku VHD, dołącz je toohello nowy magazyn w warstwie Premium obsługuje maszyny Wirtualnej platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="253eb-422">Lastly, if you have registered data disk VHDs, attach them toohello new Premium Storage capable Azure VM.</span></span>

<span data-ttu-id="253eb-423">Skorzystaj z następujących PowerShell polecenia cmdlet tooattach danych dysku toohello nowej maszyny Wirtualnej i określ hello zasad buforowania.</span><span class="sxs-lookup"><span data-stu-id="253eb-423">Use following PowerShell cmdlet tooattach data disk toohello new VM and specify hello caching policy.</span></span> <span data-ttu-id="253eb-424">W przykładzie poniżej hello zasad buforowania ustawiono zbyt*tylko do odczytu*.</span><span class="sxs-lookup"><span data-stu-id="253eb-424">In example below hello caching policy is set too*ReadOnly*.</span></span>

```powershell
$vm = Get-AzureVM -ServiceName $serviceName -Name $vmName

Add-AzureDataDisk -ImportFrom -DiskName "DataDisk" -LUN 0 –HostCaching ReadOnly –VM $vm

Update-AzureVM  -VM $vm
```

> [!NOTE]
> <span data-ttu-id="253eb-425">Może być konieczne toosupport dodatkowe kroki aplikacji, która jest nie obejmuje się w tym przewodniku.</span><span class="sxs-lookup"><span data-stu-id="253eb-425">There may be additional steps necessary toosupport your application that is not be covered by this guide.</span></span>
>
>

### <a name="checking-and-plan-backup"></a><span data-ttu-id="253eb-426">Sprawdzanie i Planowanie tworzenia kopii zapasowej</span><span class="sxs-lookup"><span data-stu-id="253eb-426">Checking and plan backup</span></span>
<span data-ttu-id="253eb-427">Raz powitalne nowej maszyny Wirtualnej jest uruchomiony i działa, hello przy użyciu tego samego identyfikatora logowania i hasło dostępu do jako hello oryginalna maszyna wirtualna, a następnie sprawdź, czy wszystko działa zgodnie z oczekiwaniami.</span><span class="sxs-lookup"><span data-stu-id="253eb-427">Once hello new VM is up and running, access it using hello same login id and password is as hello original VM, and verify that everything is working as expected.</span></span> <span data-ttu-id="253eb-428">Wszystkie ustawienia hello, w tym woluminy rozłożone hello będą obecne w hello nowej maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="253eb-428">All hello settings, including hello striped volumes, would be present in hello new VM.</span></span>

<span data-ttu-id="253eb-429">ostatni krok Hello jest harmonogram tworzenia kopii zapasowej i konserwacji tooplan powitalne nowej maszyny Wirtualnej na podstawie aplikacji hello potrzeb.</span><span class="sxs-lookup"><span data-stu-id="253eb-429">hello last step is tooplan backup and maintenance schedule for hello new VM based on hello application's needs.</span></span>

### <span data-ttu-id="253eb-430"><a name="a-sample-migration-script"></a>Przykładowy skrypt migracji</span><span class="sxs-lookup"><span data-stu-id="253eb-430"><a name="a-sample-migration-script"></a>A sample migration script</span></span>
<span data-ttu-id="253eb-431">Jeśli masz wiele maszyn wirtualnych toomigrate automatyzacji za pomocą skryptów środowiska PowerShell będą przydatne.</span><span class="sxs-lookup"><span data-stu-id="253eb-431">If you have multiple VMs toomigrate, automation through PowerShell scripts will be helpful.</span></span> <span data-ttu-id="253eb-432">Oto przykładowy skrypt, który zautomatyzuje hello migracji maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="253eb-432">Following is a sample script that automates hello migration of a VM.</span></span> <span data-ttu-id="253eb-433">Uwaga poniżej skryptu jest tylko przykładem, a istnieje kilka założeń dotyczących hello bieżącego dysków maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="253eb-433">Note that below script is only an example, and there are few assumptions made about hello current VM disks.</span></span> <span data-ttu-id="253eb-434">Może być konieczne tooupdate hello skryptu toomatch z konkretnego scenariusza.</span><span class="sxs-lookup"><span data-stu-id="253eb-434">You may need tooupdate hello script toomatch with your specific scenario.</span></span>

<span data-ttu-id="253eb-435">założenia Hello są:</span><span class="sxs-lookup"><span data-stu-id="253eb-435">hello assumptions are:</span></span>

* <span data-ttu-id="253eb-436">Tworzysz klasycznych maszyn wirtualnych platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="253eb-436">You are creating classic Azure VMs.</span></span>
* <span data-ttu-id="253eb-437">Źródła dysków systemu operacyjnego i dysków danych źródłowych znajdują się w tym samym koncie magazynu i tego samego kontenera.</span><span class="sxs-lookup"><span data-stu-id="253eb-437">Your source OS Disks and source Data Disks are in same storage account and same container.</span></span> <span data-ttu-id="253eb-438">Jeśli dysków systemu operacyjnego i dysków z danymi nie znajdują się w hello same Umieść, można użyć narzędzia AzCopy lub Azure PowerShell toocopy dysków VHD za pośrednictwem konta magazynu i kontenerów.</span><span class="sxs-lookup"><span data-stu-id="253eb-438">If your OS Disks and Data Disks are not in hello same place, you can use AzCopy or Azure PowerShell toocopy VHDs over storage accounts and containers.</span></span> <span data-ttu-id="253eb-439">Zobacz poprzedni krok toohello: [kopii wirtualnego dysku twardego z narzędzia AzCopy lub środowiska PowerShell](#copy-vhd-with-azcopy-or-powershell).</span><span class="sxs-lookup"><span data-stu-id="253eb-439">Refer toohello previous step: [Copy VHD with AzCopy or PowerShell](#copy-vhd-with-azcopy-or-powershell).</span></span> <span data-ttu-id="253eb-440">Edytowanie toomeet tego skryptu innym rozwiązaniem jest scenariusz, ale zaleca się użycie narzędzia AzCopy lub programu PowerShell, ponieważ jest łatwiejsze i szybsze.</span><span class="sxs-lookup"><span data-stu-id="253eb-440">Editing this script toomeet your scenario is another choice, but we recommend using AzCopy or PowerShell since it is easier and faster.</span></span>

<span data-ttu-id="253eb-441">skrypt automatyzacji Hello podano poniżej.</span><span class="sxs-lookup"><span data-stu-id="253eb-441">hello automation script is provided below.</span></span> <span data-ttu-id="253eb-442">Zastąp tekst z informacjami i zaktualizuj hello toomatch skryptu z konkretnego scenariusza.</span><span class="sxs-lookup"><span data-stu-id="253eb-442">Replace text with your information and update hello script toomatch with your specific scenario.</span></span>

> [!NOTE]
> <span data-ttu-id="253eb-443">Przy użyciu istniejącego skryptu hello nie zachowa konfiguracji sieci hello źródła maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="253eb-443">Using hello existing script does not preserve hello network configuration of your source VM.</span></span> <span data-ttu-id="253eb-444">Potrzebujesz ustawień sieciowych hello toore-config na zmigrowanych maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="253eb-444">You will need toore-config hello networking settings on your migrated VMs.</span></span>
>
>

```
    <#
    .Synopsis
    This script is provided as an EXAMPLE tooshow how toomigrate a VM from a standard storage account tooa premium storage account. You can customize it according tooyour specific requirements.

    .Description
    hello script will copy hello vhds (page blobs) of hello source VM toohello new storage account.
    And then it will create a new VM from these copied vhds based on hello inputs that you specified for hello new VM.
    You can modify hello script toosatisfy your specific requirement, but please be aware of hello items specified
    in hello Terms of Use section.

    .Terms of Use
    Copyright © 2015 Microsoft Corporation.  All rights reserved.

    THIS CODE AND ANY ASSOCIATED INFORMATION ARE PROVIDED "AS IS" WITHOUT WARRANTY OF ANY KIND,
    EITHER EXPRESSED OR IMPLIED, INCLUDING BUT NOT LIMITED toohello IMPLIED WARRANTIES OF MERCHANTABILITY
    AND/OR FITNESS FOR A PARTICULAR PURPOSE. hello ENTIRE RISK OF USE, INABILITY tooUSE, OR
    RESULTS FROM hello USE OF THIS CODE REMAINS WITH hello USER.

    .Example (Save this script as Migrate-AzureVM.ps1)

    .\Migrate-AzureVM.ps1 -SourceServiceName CurrentServiceName -SourceVMName CurrentVMName –DestStorageAccount newpremiumstorageaccount -DestServiceName NewServiceName -DestVMName NewDSVMName -DestVMSize "Standard_DS2" –Location "Southeast Asia"

    .Link
    toofind more information about how tooset up Azure PowerShell, refer toohello following links.
    http://azure.microsoft.com/documentation/articles/powershell-install-configure/
    http://azure.microsoft.com/documentation/articles/storage-powershell-guide-full/
    http://azure.microsoft.com/blog/2014/10/22/migrate-azure-virtual-machines-between-storage-accounts/

    #>

    Param(
    # hello cloud service name of hello VM.
    [Parameter(Mandatory = $true)]
    [string] $SourceServiceName,

    # hello VM name toocopy.
    [Parameter(Mandatory = $true)]
    [String] $SourceVMName,

    # hello destination storage account name.
    [Parameter(Mandatory = $true)]
    [String] $DestStorageAccount,

    # hello destination cloud service name
    [Parameter(Mandatory = $true)]
    [String] $DestServiceName,

    # hello destination vm name
    [Parameter(Mandatory = $true)]
    [String] $DestVMName,

    # hello destination vm size
    [Parameter(Mandatory = $true)]
    [String] $DestVMSize,

    # hello location of destination VM.
    [Parameter(Mandatory = $true)]
    [string] $Location,

    # whether or not toocopy hello os disk, hello default is only copy data disks
    [Parameter(Mandatory = $false)]
    [Bool] $DataDiskOnly = $true,

    # how frequently tooreport hello copy status in sceconds
    [Parameter(Mandatory = $false)]
    [Int32] $CopyStatusReportInterval = 15,

    # hello name suffix tooadd toonew created disks tooavoid conflict with source disk names
    [Parameter(Mandatory = $false)]
    [String]$DiskNameSuffix = "-prem"

    ) #end param

    #######################################################################
    #  Verify Azure PowerShell module and version
    #######################################################################

    #import hello Azure PowerShell module
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


    #Check hello Azure PowerShell module version
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
        Write-Host "[ERROR] - There is no valid Azure subscription found in PowerShell. Please refer toothis article http://azure.microsoft.com/documentation/articles/powershell-install-configure/ tooconnect an Azure subscription. Exiting." -ForegroundColor Red
        Exit
    }


    #######################################################################
    #  Check if hello VM is shut down
    #  Stopping hello VM is a required step so that hello file system is consistent when you do hello copy operation.
    #  Azure does not support live migration at this time..
    #######################################################################

    if (($sourceVM = Get-AzureVM –ServiceName $SourceServiceName –Name $SourceVMName) -eq $null)
    {
        Write-Host "[ERROR] - hello source VM doesn't exist in hello current subscription. Exiting." -ForegroundColor Red
        Exit
    }

    # check if VM is shut down
    if ( $sourceVM.Status -notmatch "Stopped" )
    {
        Write-Host "[Warning] - Stopping hello VM is a required step so that hello file system is consistent when you do hello copy operation. Azure does not support live migration at this time. If you'd like toocreate a VM from a generalized image, sys-prep hello Virtual Machine before stopping it." -ForegroundColor Yellow
        $ContinueAnswer = Read-Host "`n`tDo you wish toostop $SourceVMName now? Input 'N' if you want tooshut down hello VM manually and come back later.(Y/N)"
        If ($ContinueAnswer -ne "Y") { Write-Host "`n Exiting." -ForegroundColor Red;Exit }
        $sourceVM | Stop-AzureVM

        # wait until hello VM is shut down
        $VMStatus = (Get-AzureVM –ServiceName $SourceServiceName –Name $vmName).Status
        while ($VMStatus -notmatch "Stopped")
        {
            Write-Host "`n[Status] - Waiting VM $vmName tooshut down" -ForegroundColor Green
            Sleep -Seconds 5
            $VMStatus = (Get-AzureVM –ServiceName $SourceServiceName –Name $vmName).Status
        }
    }

    # exporting hello sourve vm tooa configuration file, you can restore hello original VM by importing this config file
    # see more information for Import-AzureVM
    $workingDir = (Get-Location).Path
    $vmConfigurationPath = $env:HOMEPATH + "\VM-" + $SourceVMName + ".xml"
    Write-Host "`n[WORKITEM] - Exporting VM configuration too$vmConfigurationPath" -ForegroundColor Yellow
    $exportRe = $sourceVM | Export-AzureVM -Path $vmConfigurationPath


    #######################################################################
    #  Copy hello vhds of hello source vm
    #  You can choose toocopy all disks including os and data disks by specifying the
    #  parameter -DataDiskOnly toobe $false. hello default is toocopy only data disk vhds
    #  and hello new VM will boot from hello original os disk.
    #######################################################################

    $sourceOSDisk = $sourceVM.VM.OSVirtualHardDisk
    $sourceDataDisks = $sourceVM.VM.DataVirtualHardDisks

    # Get source storage account information, not considering hello data disks and os disks are in different accounts
    $sourceStorageAccountName = $sourceOSDisk.MediaLink.Host -split "\." | select -First 1
    $sourceStorageKey = (Get-AzureStorageKey -StorageAccountName $sourceStorageAccountName).Primary
    $sourceContext = New-AzureStorageContext –StorageAccountName $sourceStorageAccountName -StorageAccountKey $sourceStorageKey

    # Create destination context
    $destStorageKey = (Get-AzureStorageKey -StorageAccountName $DestStorageAccount).Primary
    $destContext = New-AzureStorageContext –StorageAccountName $DestStorageAccount -StorageAccountKey $destStorageKey

    # Create a container of vhds if it doesn't exist
    if ((Get-AzureStorageContainer -Context $destContext -Name vhds -ErrorAction SilentlyContinue) -eq $null)
    {
        Write-Host "`n[WORKITEM] - Creating a container vhds in hello destination storage account." -ForegroundColor Yellow
        New-AzureStorageContainer -Context $destContext -Name vhds
    }


    $allDisksToCopy = $sourceDataDisks
    # check if need toocopy os disk
    $sourceOSVHD = $sourceOSDisk.MediaLink.Segments[2]
    if ($DataDiskOnly)
    {
        # copy data disks only, this option requires deleting hello source VM so that dest VM can boot
        # from hello same vhd blob.
        $ContinueAnswer = Read-Host "`n`t[Warning] You chose toocopy data disks only. Moving VM requires removing hello original VM (hello disks and backing vhd files will NOT be deleted) so that hello new VM can boot from hello same vhd. This is an irreversible action. Do you wish tooproceed right now? (Y/N)"
        If ($ContinueAnswer -ne "Y") { Write-Host "`n Exiting." -ForegroundColor Red;Exit }
        $destOSVHD = Get-AzureStorageBlob -Blob $sourceOSVHD -Container vhds -Context $sourceContext
        Write-Host "`n[WORKITEM] - Removing hello original VM (hello vhd files are NOT deleted)." -ForegroundColor Yellow
        Remove-AzureVM -Name $SourceVMName -ServiceName $SourceServiceName

        Write-Host "`n[WORKITEM] - Waiting utill hello OS disk is released by source VM. This may take up tooseveral minutes."
        $diskAttachedTo = (Get-AzureDisk -DiskName $sourceOSDisk.DiskName).AttachedTo
        while ($diskAttachedTo -ne $null)
        {
            Start-Sleep -Seconds 10
            $diskAttachedTo = (Get-AzureDisk -DiskName $sourceOSDisk.DiskName).AttachedTo
        }

    }
    else
    {
        # copy hello os disk vhd
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
        # update hello media link toopoint toohello target blob link
        $disk.MediaLink = $targetBlob.ICloudBlob.Uri.AbsoluteUri
    }

    # Wait until all vhd files are copied.
    $diskComplete = @()
    do
    {
        Write-Host "`n[WORKITEM] - Waiting for all disk copy toocomplete. Checking status every $CopyStatusReportInterval seconds." -ForegroundColor Yellow
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
    #  hello new VM can be created from hello copied disks or hello original os disk.
    #  You can ddd your own logic here toosatisfy your specific requirements of hello vm.
    #######################################################################

    # Create a VM from hello existing os disk
    if ($DataDiskOnly)
    {
        $vm = New-AzureVMConfig -Name $DestVMName -InstanceSize $DestVMSize -DiskName $sourceOSDisk.DiskName
    }
    else
    {
        $newOSDisk = Add-AzureDisk -OS $sourceOSDisk.OS -DiskName ($sourceOSDisk.DiskName + $DiskNameSuffix) -MediaLocation $destOSVHD.ICloudBlob.Uri.AbsoluteUri
        $vm = New-AzureVMConfig -Name $DestVMName -InstanceSize $DestVMSize -DiskName $newOSDisk.DiskName
    }
    # Attached hello copied data disks toohello new VM
    foreach ($dataDisk in $sourceDataDisks)
    {
        # add -DiskLabel $dataDisk.DiskLabel if there are labels for disks of hello source vm
        $diskLabel = "drive" + $dataDisk.Lun
        $vm | Add-AzureDataDisk -ImportFrom -DiskLabel $diskLabel -LUN $dataDisk.Lun -MediaLocation $dataDisk.MediaLink
    }

    # Edit this if you want tooadd more custimization toohello new VM
    # $vm | Add-AzureEndpoint -Protocol tcp -LocalPort 443 -PublicPort 443 -Name 'HTTPs'
    # $vm | Set-AzureSubnet "PubSubnet","PrivSubnet"

    New-AzureVM -ServiceName $DestServiceName -VMs $vm -Location $Location
```

#### <span data-ttu-id="253eb-445"><a name="optimization"></a>Optymalizacja</span><span class="sxs-lookup"><span data-stu-id="253eb-445"><a name="optimization"></a>Optimization</span></span>
<span data-ttu-id="253eb-446">Bieżąca konfiguracja maszyny Wirtualnej można dostosować w szczególności toowork prawidłowo w przypadku standardowych dysków.</span><span class="sxs-lookup"><span data-stu-id="253eb-446">Your current VM configuration may be customized specifically toowork well with Standard disks.</span></span> <span data-ttu-id="253eb-447">Na przykład tooincrease hello wydajności przy użyciu wielu dysków w woluminy rozłożone.</span><span class="sxs-lookup"><span data-stu-id="253eb-447">For instance, tooincrease hello performance by using many disks in a striped volume.</span></span> <span data-ttu-id="253eb-448">Na przykład zamiast 4 dyski osobno na magazyn w warstwie Premium, może być możliwe toooptimize hello koszt przez jednego dysku.</span><span class="sxs-lookup"><span data-stu-id="253eb-448">For example, instead of using 4 disks separately on Premium Storage, you may be able toooptimize hello cost by having a single disk.</span></span> <span data-ttu-id="253eb-449">Optymalizacje, takich jak ta toobe konieczność obsługi na podstawie przypadku i wymagają niestandardowej czynności po migracji hello.</span><span class="sxs-lookup"><span data-stu-id="253eb-449">Optimizations like this need toobe handled on a case by case basis and require custom steps after hello migration.</span></span> <span data-ttu-id="253eb-450">Należy również zauważyć, że ten proces może nie również działać dla baz danych i aplikacji, które są zależne od układ dysku hello zdefiniowane w Instalatorze hello.</span><span class="sxs-lookup"><span data-stu-id="253eb-450">Also, note that this process may not well work for databases and applications that depend on hello disk layout defined in hello setup.</span></span>

##### <a name="preparation"></a><span data-ttu-id="253eb-451">Przygotowanie</span><span class="sxs-lookup"><span data-stu-id="253eb-451">Preparation</span></span>
1. <span data-ttu-id="253eb-452">Zakończenie hello proste migracji, zgodnie z opisem w hello wcześniej sekcji.</span><span class="sxs-lookup"><span data-stu-id="253eb-452">Complete hello Simple Migration as described in hello earlier section.</span></span> <span data-ttu-id="253eb-453">Optymalizacje zostaną wykonane na powitania nowej maszyny Wirtualnej po migracji hello.</span><span class="sxs-lookup"><span data-stu-id="253eb-453">Optimizations will be performed on hello new VM after hello migration.</span></span>
2. <span data-ttu-id="253eb-454">Zdefiniuj hello nowe rozmiary dysku wymagane do konfiguracji hello zoptymalizowane.</span><span class="sxs-lookup"><span data-stu-id="253eb-454">Define hello new disk sizes needed for hello optimized configuration.</span></span>
3. <span data-ttu-id="253eb-455">Należy określić mapowanie specyfikacji hello bieżącego dysków/woluminów toohello nowego dysku.</span><span class="sxs-lookup"><span data-stu-id="253eb-455">Determine mapping of hello current disks/volumes toohello new disk specifications.</span></span>

##### <a name="execution-steps"></a><span data-ttu-id="253eb-456">Wykonanie czynności</span><span class="sxs-lookup"><span data-stu-id="253eb-456">Execution steps</span></span>
1. <span data-ttu-id="253eb-457">Utwórz hello nowe dyski o odpowiednim rozmiarze hello na powitania Premium magazynu z maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="253eb-457">Create hello new disks with hello right sizes on hello Premium Storage VM.</span></span>
2. <span data-ttu-id="253eb-458">Toohello maszyny Wirtualnej i skopiuj hello dane logowania z hello bieżącego woluminu toohello nowego dysku mapowanego toothat woluminu.</span><span class="sxs-lookup"><span data-stu-id="253eb-458">Login toohello VM and copy hello data from hello current volume toohello new disk that maps toothat volume.</span></span> <span data-ttu-id="253eb-459">W tym wszystkie woluminy bieżącego hello, które wymagają toomap tooa nowego dysku.</span><span class="sxs-lookup"><span data-stu-id="253eb-459">Do this for all hello current volumes that need toomap tooa new disk.</span></span>
3. <span data-ttu-id="253eb-460">Następnie zmienić hello aplikacji ustawienia tooswitch toohello nowe dyski i odłączyć hello starszych woluminów.</span><span class="sxs-lookup"><span data-stu-id="253eb-460">Next, change hello application settings tooswitch toohello new disks, and detach hello old volumes.</span></span>

<span data-ttu-id="253eb-461">Dostrajanie aplikacji hello w celu zapewnienia lepszej wydajności dysku, można znaleźć w artykule zbyt[optymalizacji wydajności aplikacji](storage-premium-storage-performance.md#optimizing-application-performance).</span><span class="sxs-lookup"><span data-stu-id="253eb-461">For tuning hello application for better disk performance, please refer too[Optimizing Application Performance](storage-premium-storage-performance.md#optimizing-application-performance).</span></span>

### <a name="application-migrations"></a><span data-ttu-id="253eb-462">Migracja aplikacji</span><span class="sxs-lookup"><span data-stu-id="253eb-462">Application migrations</span></span>
<span data-ttu-id="253eb-463">Baz danych i innych złożonych aplikacji może wymagać specjalne kroki zgodnie z definicją w dostawcy aplikacji hello hello migracji.</span><span class="sxs-lookup"><span data-stu-id="253eb-463">Databases and other complex applications may require special steps as defined by hello application provider for hello migration.</span></span> <span data-ttu-id="253eb-464">Można znaleźć w dokumentacji aplikacji toorespective.</span><span class="sxs-lookup"><span data-stu-id="253eb-464">Please refer toorespective application documentation.</span></span> <span data-ttu-id="253eb-465">Na przykład</span><span class="sxs-lookup"><span data-stu-id="253eb-465">E.g.</span></span> <span data-ttu-id="253eb-466">zwykle baz danych można poddać migracji za pomocą kopii zapasowej i przywracania.</span><span class="sxs-lookup"><span data-stu-id="253eb-466">typically databases can be migrated through backup and restore.</span></span>

## <a name="next-steps"></a><span data-ttu-id="253eb-467">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="253eb-467">Next steps</span></span>
<span data-ttu-id="253eb-468">Zobacz następujące zasoby w określonych scenariuszach migracji maszyn wirtualnych hello:</span><span class="sxs-lookup"><span data-stu-id="253eb-468">See hello following resources for specific scenarios for migrating virtual machines:</span></span>

* [<span data-ttu-id="253eb-469">Migrowanie maszyn wirtualnych platformy Azure między kontami magazynu</span><span class="sxs-lookup"><span data-stu-id="253eb-469">Migrate Azure Virtual Machines between Storage Accounts</span></span>](https://azure.microsoft.com/blog/2014/10/22/migrate-azure-virtual-machines-between-storage-accounts/)
* [<span data-ttu-id="253eb-470">Tworzenie i przekazywanie tooAzure wirtualnego dysku twardego z systemem Windows Server.</span><span class="sxs-lookup"><span data-stu-id="253eb-470">Create and upload a Windows Server VHD tooAzure.</span></span>](../virtual-machines/windows/classic/createupload-vhd.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)
* [<span data-ttu-id="253eb-471">Tworzenie i przekazywanie wirtualnego dysku twardego zawierający hello System operacyjny Linux</span><span class="sxs-lookup"><span data-stu-id="253eb-471">Creating and Uploading a Virtual Hard Disk that Contains hello Linux Operating System</span></span>](../virtual-machines/linux/classic/create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)
* [<span data-ttu-id="253eb-472">Migrowanie maszyn wirtualnych z usług AWS Amazon tooMicrosoft Azure</span><span class="sxs-lookup"><span data-stu-id="253eb-472">Migrating Virtual Machines from Amazon AWS tooMicrosoft Azure</span></span>](http://channel9.msdn.com/Series/Migrating-Virtual-Machines-from-Amazon-AWS-to-Microsoft-Azure)

<span data-ttu-id="253eb-473">Zobacz też hello następujące zasoby toolearn więcej informacji na temat usługi Azure Storage i maszyn wirtualnych platformy Azure:</span><span class="sxs-lookup"><span data-stu-id="253eb-473">Also, see hello following resources toolearn more about Azure Storage and Azure Virtual Machines:</span></span>

* [<span data-ttu-id="253eb-474">Azure Storage</span><span class="sxs-lookup"><span data-stu-id="253eb-474">Azure Storage</span></span>](https://azure.microsoft.com/documentation/services/storage/)
* [<span data-ttu-id="253eb-475">Maszyny wirtualne platformy Azure</span><span class="sxs-lookup"><span data-stu-id="253eb-475">Azure Virtual Machines</span></span>](https://azure.microsoft.com/documentation/services/virtual-machines/)
* [<span data-ttu-id="253eb-476">Premium Storage: magazyn o wysokiej wydajności dla obciążeń maszyn wirtualnych platformy Azure</span><span class="sxs-lookup"><span data-stu-id="253eb-476">Premium Storage: High-Performance Storage for Azure Virtual Machine Workloads</span></span>](storage-premium-storage.md)

[1]:./media/storage-migration-to-premium-storage/migration-to-premium-storage-1.png
[2]:./media/storage-migration-to-premium-storage/migration-to-premium-storage-1.png
[3]:./media/storage-migration-to-premium-storage/migration-to-premium-storage-3.png
[4]: http://technet.microsoft.com/library/hh831739.aspx
