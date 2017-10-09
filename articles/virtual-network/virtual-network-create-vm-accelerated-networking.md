---
title: "aaaCreate maszyny wirtualnej platformy Azure za pomocą sieci przyspieszony | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toocreate maszynę wirtualną za pomocą przyspieszony sieci."
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/10/2017
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 241362891bfe083ab32c2f558be54f63f87c0693
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-virtual-machine-with-accelerated-networking"></a><span data-ttu-id="148d3-103">Utwórz maszynę wirtualną za pomocą przyspieszony sieci</span><span class="sxs-lookup"><span data-stu-id="148d3-103">Create a virtual machine with Accelerated Networking</span></span>

<span data-ttu-id="148d3-104">Z tego samouczka, dowiesz się, jak toocreate Azure maszyny wirtualnej (VM) za pomocą przyspieszony sieci.</span><span class="sxs-lookup"><span data-stu-id="148d3-104">In this tutorial, you learn how toocreate an Azure Virtual Machine (VM) with Accelerated Networking.</span></span> <span data-ttu-id="148d3-105">Przyspieszone sieci jest GA dla systemu Windows i w publicznej wersji zapoznawczej dla określonych dystrybucje systemu Linux.</span><span class="sxs-lookup"><span data-stu-id="148d3-105">Accelerated Networking is GA for Windows and in a Public Preview for specific Linux distributions.</span></span> <span data-ttu-id="148d3-106">Przyspieszone sieci umożliwia tooa wirtualizacji (SR-IOV) we/wy z jednym elementem głównym maszyny Wirtualnej, co znacznie poprawia wydajność sieci.</span><span class="sxs-lookup"><span data-stu-id="148d3-106">Accelerated networking enables single root I/O virtualization (SR-IOV) tooa VM, greatly improving its networking performance.</span></span> <span data-ttu-id="148d3-107">Ta ścieżka wysokiej wydajności pomija hello hosta hello ścieżki danych, zmniejszając czas oczekiwania, zakłócenia i użycie procesora CPU do użycia z najbardziej wymagających obciążeń sieci hello na obsługiwanych typów maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="148d3-107">This high-performance path bypasses hello host from hello datapath reducing latency, jitter, and CPU utilization, for use with hello most demanding network workloads on supported VM types.</span></span> <span data-ttu-id="148d3-108">powitania po obraz pokazuje komunikacji między dwóch maszyn wirtualnych (VM) z włączonymi i wyłączonymi przyspieszonego sieci:</span><span class="sxs-lookup"><span data-stu-id="148d3-108">hello following picture shows communication between two virtual machines (VM) with and without accelerated networking:</span></span>

![Porównanie](./media/virtual-network-create-vm-accelerated-networking/image1.png)

<span data-ttu-id="148d3-110">Bez przyspieszonego sieci hello hosta i przełącznik wirtualny hello musi przejść przez cały ruch sieciowy i hello maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="148d3-110">Without accelerated networking, all networking traffic in and out of hello VM must traverse hello host and hello virtual switch.</span></span> <span data-ttu-id="148d3-111">Przełącznik wirtualny Hello udostępnia wszystkie egzekwowanie zasad, takie jako grupy zabezpieczeń sieci dostęp listy kontroli, izolacji i innych ruchu toonetwork usług wirtualizacją sieci.</span><span class="sxs-lookup"><span data-stu-id="148d3-111">hello virtual switch provides all policy enforcement, such as network security groups, access control lists, isolation, and other network virtualized services toonetwork traffic.</span></span> <span data-ttu-id="148d3-112">więcej informacji na temat przełączników wirtualnych, przeczytaj hello toolearn [wirtualizacji sieci funkcji Hyper-V i przełącznik wirtualny](https://technet.microsoft.com/library/jj945275.aspx) artykułu.</span><span class="sxs-lookup"><span data-stu-id="148d3-112">toolearn more about virtual switches, read hello [Hyper-V network virtualization and virtual switch](https://technet.microsoft.com/library/jj945275.aspx) article.</span></span>

<span data-ttu-id="148d3-113">Z przyspieszonego w sieci, ruch sieciowy dociera do lokalizacji hello wirtualna interfejsu sieciowego (NIC) i następnie przekazany toohello maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="148d3-113">With accelerated networking, network traffic arrives at hello VM's network interface (NIC), and is then forwarded toohello VM.</span></span> <span data-ttu-id="148d3-114">Wszystkich zasad sieciowych, które hello przełącznik wirtualny ma zastosowanie bez przyspieszonego sieci są Odciążone i sprzętu.</span><span class="sxs-lookup"><span data-stu-id="148d3-114">All network policies that hello virtual switch applies without accelerated networking are offloaded and applied in hardware.</span></span> <span data-ttu-id="148d3-115">Stosowanie zasad w sprzętu umożliwia hello kart tooforward ruch sieciowy bezpośrednio toohello maszyny Wirtualnej, pomijanie hello hosta i przełącznik wirtualny hello, przy zachowaniu wszystkich zasad hello zastosowaniu hello hosta.</span><span class="sxs-lookup"><span data-stu-id="148d3-115">Applying policy in hardware enables hello NIC tooforward network traffic directly toohello VM, bypassing hello host and hello virtual switch, while maintaining all hello policy it applied in hello host.</span></span>

<span data-ttu-id="148d3-116">Hello zalet przyspieszonego sieci mają zastosowanie tylko toohello maszynę Wirtualną, która jest włączone.</span><span class="sxs-lookup"><span data-stu-id="148d3-116">hello benefits of accelerated networking only apply toohello VM that it is enabled on.</span></span> <span data-ttu-id="148d3-117">Najlepiej hello jest idealny tooenable tę funkcję na co najmniej dwie maszyny wirtualne podłączone toohello tej samej sieci wirtualnej platformy Azure (VNet).</span><span class="sxs-lookup"><span data-stu-id="148d3-117">For hello best results, it is ideal tooenable this feature on at least two VMs connected toohello same Azure Virtual Network (VNet).</span></span> <span data-ttu-id="148d3-118">Podczas komunikacji między sieciami wirtualnymi lub łączącego lokalnymi, ta funkcja ma minimalny wpływ toooverall opóźnienia.</span><span class="sxs-lookup"><span data-stu-id="148d3-118">When communicating across VNets or connecting on-premises, this feature has minimal impact toooverall latency.</span></span>

> [!WARNING]
> <span data-ttu-id="148d3-119">To Linux publicznej wersji zapoznawczej nie może mieć hello sam poziom dostępności i niezawodności, jako funkcje, które są zazwyczaj wydanie z dostępnością.</span><span class="sxs-lookup"><span data-stu-id="148d3-119">This Linux Public Preview may not have hello same level of availability and reliability as features that are in general availability release.</span></span> <span data-ttu-id="148d3-120">Funkcja Hello nie jest obsługiwane, mogą mieć ograniczone możliwości i mogą nie być dostępne we wszystkich lokalizacjach Azure.</span><span class="sxs-lookup"><span data-stu-id="148d3-120">hello feature is not supported, may have constrained capabilities, and may not be available in all Azure locations.</span></span> <span data-ttu-id="148d3-121">Najbardziej aktualne powiadomień hello na dostępność i stan tej funkcji Sprawdź hello Azure Virtual Network aktualizacji strony.</span><span class="sxs-lookup"><span data-stu-id="148d3-121">For hello most up-to-date notifications on availability and status of this feature, check hello Azure Virtual Network updates page.</span></span>

## <a name="benefits"></a><span data-ttu-id="148d3-122">Korzyści</span><span class="sxs-lookup"><span data-stu-id="148d3-122">Benefits</span></span>
* <span data-ttu-id="148d3-123">**Zmniejszyć opóźnienia / wyższy pakietów na sekundę (pps):** hello usunięcie przełącznika wirtualnego z hello ścieżki danych usuwa pakiety poświęcić czas hello w hello hosta dla przetwarzanie zasad i zwiększa hello liczba pakietów, które mogą być przetwarzane wewnątrz hello maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="148d3-123">**Lower Latency / Higher packets per second (pps):** Removing hello virtual switch from hello datapath removes hello time packets spend in hello host for policy processing and increases hello number of packets that can be processed inside hello VM.</span></span>
* <span data-ttu-id="148d3-124">**Zmniejszona zakłócenia:** przełącznik wirtualny przetwarzania zależy od hello ilość zasad, które należy zastosować toobe i obciążenie hello hello procesora CPU, obsługującym hello przetwarzania.</span><span class="sxs-lookup"><span data-stu-id="148d3-124">**Reduced jitter:** Virtual switch processing depends on hello amount of policy that needs toobe applied and hello workload of hello CPU that is doing hello processing.</span></span> <span data-ttu-id="148d3-125">Odciążanie sprzętu toohello wymuszania zasad hello usuwa tego zmienności dostarczania pakietów bezpośrednio zmienia toohello maszyny Wirtualnej, usunięcie hello hosta tooVM komunikacji i wszystkich oprogramowania przerwań i kontekstu.</span><span class="sxs-lookup"><span data-stu-id="148d3-125">Offloading hello policy enforcement toohello hardware removes that variability by delivering packets directly toohello VM, removing hello host tooVM communication and all software interrupts and context switches.</span></span>
* <span data-ttu-id="148d3-126">**Zmniejszyć użycie procesora CPU:** Bypassing hello przełącznika wirtualnego na hoście hello prowadzi tooless użycie procesora CPU do przetwarzania ruchu sieciowego.</span><span class="sxs-lookup"><span data-stu-id="148d3-126">**Decreased CPU utilization:** Bypassing hello virtual switch in hello host leads tooless CPU utilization for processing network traffic.</span></span>

## <span data-ttu-id="148d3-127"><a name="Limitations"></a>Ograniczenia</span><span class="sxs-lookup"><span data-stu-id="148d3-127"><a name="Limitations"></a>Limitations</span></span>
<span data-ttu-id="148d3-128">Podczas przy użyciu tej możliwości istnieją Hello następujące ograniczenia:</span><span class="sxs-lookup"><span data-stu-id="148d3-128">hello following limitations exist when using this capability:</span></span>

* <span data-ttu-id="148d3-129">**Tworzenie interfejsu sieci:** akcelerowanego sieci można włączyć tylko dla nowych kart sieciowych.</span><span class="sxs-lookup"><span data-stu-id="148d3-129">**Network interface creation:** Accelerated networking can only be enabled for a new NIC.</span></span> <span data-ttu-id="148d3-130">Nie można włączyć dla istniejącej karty sieciowej.</span><span class="sxs-lookup"><span data-stu-id="148d3-130">It cannot be enabled for an existing NIC.</span></span>
* <span data-ttu-id="148d3-131">**Tworzenie maszyny Wirtualnej:** A kart interfejsu Sieciowego z włączoną obsługą przyspieszonego sieci może jedynie być dołączone tooa maszyny Wirtualnej, gdy hello zostanie utworzona maszyna wirtualna.</span><span class="sxs-lookup"><span data-stu-id="148d3-131">**VM creation:** A NIC with accelerated networking enabled can only be attached tooa VM when hello VM is created.</span></span> <span data-ttu-id="148d3-132">Witaj karty Sieciowej nie może być dołączone tooan istniejącej maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="148d3-132">hello NIC cannot be attached tooan existing VM.</span></span>
* <span data-ttu-id="148d3-133">**Regiony:** maszyn wirtualnych systemu Windows z przyspieszonego w sieci jest oferowanych w regionach najbardziej platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="148d3-133">**Regions:** Windows VMs with accelerated networking are offered in most Azure regions.</span></span> <span data-ttu-id="148d3-134">Maszyn wirtualnych systemu Linux z przyspieszonego sieci są dostępne w wielu regionach.</span><span class="sxs-lookup"><span data-stu-id="148d3-134">Linux VMs with accelerated networking are offered in multiple regions.</span></span> <span data-ttu-id="148d3-135">rozwija regionów Hello ta funkcja jest dostępna w.</span><span class="sxs-lookup"><span data-stu-id="148d3-135">hello regions this capability is available in is expanding.</span></span> <span data-ttu-id="148d3-136">Zobacz blog Azure aktualizacje dla sieci wirtualnej hello poniżej hello najnowszych informacji.</span><span class="sxs-lookup"><span data-stu-id="148d3-136">Please see hello Azure Virtual Networking Updates blog below for hello latest information.</span></span>   
* <span data-ttu-id="148d3-137">**Obsługiwane systemy operacyjne:** systemu Windows: Microsoft Windows Server 2012 R2 Datacenter i Windows Server 2016.</span><span class="sxs-lookup"><span data-stu-id="148d3-137">**Supported operating systems:** Windows: Microsoft Windows Server 2012 R2 Datacenter and Windows Server 2016.</span></span> <span data-ttu-id="148d3-138">Linux: Ubuntu Server 16.04 LTS i 4.4.0-77 jądra lub nowszą, SLES 12 z dodatkiem SP2, RHEL 7.3 i CentOS 7.3 (opublikowanej przez "Nieautoryzowanego Wave oprogramowanie").</span><span class="sxs-lookup"><span data-stu-id="148d3-138">Linux: Ubuntu Server 16.04 LTS with kernel 4.4.0-77 or higher, SLES 12 SP2, RHEL 7.3 and CentOS 7.3 (Published by “Rogue Wave Software”).</span></span>
* <span data-ttu-id="148d3-139">**Rozmiar maszyny Wirtualnej:** ogólnego przeznaczenia i rozmiary obliczeniowe są zoptymalizowane pod kątem wystąpienia z co najmniej osiem rdzeni.</span><span class="sxs-lookup"><span data-stu-id="148d3-139">**VM Size:** General purpose and compute-optimized instance sizes with eight or more cores.</span></span> <span data-ttu-id="148d3-140">Aby uzyskać więcej informacji, zobacz hello [Windows](../virtual-machines/windows/sizes.md?toc=%2fazure%2fvirtual-network%2ftoc.json) i [Linux](../virtual-machines/linux/sizes.md?toc=%2fazure%2fvirtual-network%2ftoc.json) artykuły rozmiary maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="148d3-140">For more information, see hello [Windows](../virtual-machines/windows/sizes.md?toc=%2fazure%2fvirtual-network%2ftoc.json) and [Linux](../virtual-machines/linux/sizes.md?toc=%2fazure%2fvirtual-network%2ftoc.json) VM sizes articles.</span></span> <span data-ttu-id="148d3-141">Witaj zbiór rozmiarów maszyn wirtualnych obsługiwanych w wystąpieniu rozwinie w przyszłości hello.</span><span class="sxs-lookup"><span data-stu-id="148d3-141">hello set of supported VM instance sizes will expand in hello future.</span></span>
* <span data-ttu-id="148d3-142">**Tylko wdrożenia za pośrednictwem usługi Azure Resource Manager (ARM):** przyspieszony sieci nie jest dostępny do wdrożenia za pomocą funkcji ASM/frontonu REDDOG.</span><span class="sxs-lookup"><span data-stu-id="148d3-142">**Deployment through Azure Resource Manager (ARM) only:** Accelerated Networking is not available for deployment through ASM/RDFE.</span></span>

<span data-ttu-id="148d3-143">Ograniczenia toothese zmiany są ogłaszane za pośrednictwem hello [sieci wirtualnych Azure aktualizuje](https://azure.microsoft.com/updates/accelerated-networking-in-preview) strony.</span><span class="sxs-lookup"><span data-stu-id="148d3-143">Changes toothese limitations are announced through hello [Azure Virtual Networking updates](https://azure.microsoft.com/updates/accelerated-networking-in-preview) page.</span></span>

## <a name="create-a-windows-vm"></a><span data-ttu-id="148d3-144">Tworzenie maszyny wirtualnej z systemem Windows</span><span class="sxs-lookup"><span data-stu-id="148d3-144">Create a Windows VM</span></span>
<span data-ttu-id="148d3-145">Możesz użyć hello portalu Azure lub Azure [PowerShell](#windows-powershell) hello toocreate maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="148d3-145">You can use hello Azure portal or Azure [PowerShell](#windows-powershell) toocreate hello VM.</span></span>

### <span data-ttu-id="148d3-146"><a name="windows-portal"></a>Portal</span><span class="sxs-lookup"><span data-stu-id="148d3-146"><a name="windows-portal"></a>Portal</span></span>

1. <span data-ttu-id="148d3-147">Za pomocą przeglądarki internetowej, otwórz hello Azure [portal](https://portal.azure.com) i zaloguj się przy użyciu platformy Azure [konta](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#account).</span><span class="sxs-lookup"><span data-stu-id="148d3-147">From an Internet browser, open hello Azure [portal](https://portal.azure.com) and sign in with your Azure [account](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#account).</span></span> <span data-ttu-id="148d3-148">Jeśli nie masz już konto, możesz zarejestrować się w celu [bezpłatnej wersji próbnej](https://azure.microsoft.com/offers/ms-azr-0044p).</span><span class="sxs-lookup"><span data-stu-id="148d3-148">If you don't already have an account, you can sign up for a [free trial](https://azure.microsoft.com/offers/ms-azr-0044p).</span></span>
2. <span data-ttu-id="148d3-149">W portalu powitania kliknij **+ nowy** > **obliczeniowe** > **systemu Windows Server Datacenter 2016**.</span><span class="sxs-lookup"><span data-stu-id="148d3-149">In hello portal, click **+ New** > **Compute** > **Windows Server 2016 Datacenter**.</span></span> 
3. <span data-ttu-id="148d3-150">W hello **systemu Windows Server Datacenter 2016** wyświetlonym bloku, pozostaw *Resource Manager* wybranego w obszarze **wybierz model wdrożenia**i kliknij przycisk **Utwórz** .</span><span class="sxs-lookup"><span data-stu-id="148d3-150">In hello **Windows Server 2016 Datacenter** blade that appears, leave *Resource Manager* selected under **Select a deployment model**, and click **Create**.</span></span>
4. <span data-ttu-id="148d3-151">W hello **podstawy** bloku, który pojawia się, wprowadź następujące wartości hello pozostaw hello pozostałe opcje domyślne lub wybierz lub wprowadź własne wartości, a kliknij hello **OK** przycisk:</span><span class="sxs-lookup"><span data-stu-id="148d3-151">In hello **Basics** blade that appears, enter hello following values, leave hello remaining default options or select or enter your own values, and click hello **OK** button:</span></span>

    |<span data-ttu-id="148d3-152">Ustawienie</span><span class="sxs-lookup"><span data-stu-id="148d3-152">Setting</span></span>|<span data-ttu-id="148d3-153">Wartość</span><span class="sxs-lookup"><span data-stu-id="148d3-153">Value</span></span>|
    |---|---|
    |<span data-ttu-id="148d3-154">Nazwa</span><span class="sxs-lookup"><span data-stu-id="148d3-154">Name</span></span>|<span data-ttu-id="148d3-155">MyVm</span><span class="sxs-lookup"><span data-stu-id="148d3-155">MyVm</span></span>|
    |<span data-ttu-id="148d3-156">Grupa zasobów</span><span class="sxs-lookup"><span data-stu-id="148d3-156">Resource group</span></span>|<span data-ttu-id="148d3-157">Pozostaw **Utwórz nowy** zaznaczone, a następnie wprowadź *MyResourceGroup*</span><span class="sxs-lookup"><span data-stu-id="148d3-157">Leave **Create new** selected and enter *MyResourceGroup*</span></span>|
    |<span data-ttu-id="148d3-158">Lokalizacja</span><span class="sxs-lookup"><span data-stu-id="148d3-158">Location</span></span>|<span data-ttu-id="148d3-159">Zachodnie stany USA 2</span><span class="sxs-lookup"><span data-stu-id="148d3-159">West US 2</span></span>|

    <span data-ttu-id="148d3-160">Jeśli nowy tooAzure, Dowiedz się więcej o [grup zasobów](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#resource-group), [subskrypcje](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#subscription), i [lokalizacje](https://azure.microsoft.com/regions) (które są także określony regionów tooas).</span><span class="sxs-lookup"><span data-stu-id="148d3-160">If you're new tooAzure, learn more about [Resource groups](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#resource-group), [subscriptions](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#subscription), and [locations](https://azure.microsoft.com/regions) (which are also referred tooas regions).</span></span>
5. <span data-ttu-id="148d3-161">W hello **wybierz rozmiar** bloku, zostanie wyświetlone, wprowadź *8* w hello **minimalna liczba rdzeni** polu, a następnie kliknij przycisk **Wyświetl wszystkie**.</span><span class="sxs-lookup"><span data-stu-id="148d3-161">In hello **Choose a size** blade that appears, enter *8* in hello **Minimum cores** box, then click **View all**.</span></span>
6. <span data-ttu-id="148d3-162">Kliknij przycisk **DS4_V2 standardowe**, lub dowolny obsługiwany maszyny Wirtualnej, kliknij przycisk hello **wybierz** przycisku.</span><span class="sxs-lookup"><span data-stu-id="148d3-162">Click **DS4_V2 Standard**, or any supported VM, then click hello **Select** button.</span></span>
7. <span data-ttu-id="148d3-163">W hello **ustawienia** bloku, zostanie wyświetlone, pozostaw wszystkie ustawienia jako — jest, z wyjątkiem kliknij **włączone** w obszarze **przyspieszony sieci**, następnie kliknij przycisk hello **OK** przycisku.</span><span class="sxs-lookup"><span data-stu-id="148d3-163">In hello **Settings** blade that appears, leave all settings as-is, except click **Enabled** under **Accelerated networking**, then click hello **OK** button.</span></span> <span data-ttu-id="148d3-164">**Uwaga:** , jeśli w poprzednich krokach wybrane wartości dla rozmiaru maszyny Wirtualnej, system operacyjny lub lokalizacji, które nie są wymienione w hello [ograniczenia](#Limitations) sekcji tego artykułu **sieci akcelerowanego**nie jest widoczny.</span><span class="sxs-lookup"><span data-stu-id="148d3-164">**Note:** If, in previous steps, you selected values for VM size, operating system, or location that aren't listed in hello [Limitations](#Limitations) section of this article, **Accelerated networking** isn't visible.</span></span>
8. <span data-ttu-id="148d3-165">W hello **Podsumowanie** bloku, który jest wyświetlany, kliknij przycisk hello **OK** przycisku.</span><span class="sxs-lookup"><span data-stu-id="148d3-165">In hello **Summary** blade that appears, click hello **OK** button.</span></span> <span data-ttu-id="148d3-166">Azure rozpoczyna tworzenie hello maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="148d3-166">Azure starts creating hello VM.</span></span> <span data-ttu-id="148d3-167">Tworzenie maszyny Wirtualnej trwa kilka minut.</span><span class="sxs-lookup"><span data-stu-id="148d3-167">VM creation takes a few minutes.</span></span>
9. <span data-ttu-id="148d3-168">tooinstall hello przyspieszony sterowników sieciowych systemu Windows, pełną hello etapami hello [Konfigurowanie systemu Windows](#configure-windows) sekcji tego artykułu.</span><span class="sxs-lookup"><span data-stu-id="148d3-168">tooinstall hello accelerated networking driver for Windows, complete hello steps in hello [Configure Windows](#configure-windows) section of this article.</span></span>

### <span data-ttu-id="148d3-169"><a name="windows-powershell"></a>Środowiska PowerShell</span><span class="sxs-lookup"><span data-stu-id="148d3-169"><a name="windows-powershell"></a>PowerShell</span></span>
1. <span data-ttu-id="148d3-170">Zainstaluj najnowszą wersję hello Azure PowerShell hello [AzureRm](https://www.powershellgallery.com/packages/AzureRM/) modułu.</span><span class="sxs-lookup"><span data-stu-id="148d3-170">Install hello latest version of hello Azure PowerShell [AzureRm](https://www.powershellgallery.com/packages/AzureRM/) module.</span></span> <span data-ttu-id="148d3-171">Jeśli jesteś tooAzure nowego środowiska PowerShell odczytu hello [Omówienie programu Azure PowerShell](/powershell/azure/get-started-azureps?toc=%2fazure%2fvirtual-network%2ftoc.json) artykułu.</span><span class="sxs-lookup"><span data-stu-id="148d3-171">If you're new tooAzure PowerShell, read hello [Azure PowerShell overview](/powershell/azure/get-started-azureps?toc=%2fazure%2fvirtual-network%2ftoc.json) article.</span></span>
2. <span data-ttu-id="148d3-172">Uruchom sesję programu PowerShell, klikając przycisk Start systemu Windows hello, wpisując **środowiska powershell**, klikając **PowerShell** hello wyników wyszukiwania.</span><span class="sxs-lookup"><span data-stu-id="148d3-172">Start a PowerShell session by clicking hello Windows Start button, typing **powershell**, then clicking **PowerShell** from hello search results.</span></span>
3. <span data-ttu-id="148d3-173">W oknie programu PowerShell, wprowadź hello `login-azurermaccount` toosign polecenia przy użyciu platformy Azure [konta](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#account).</span><span class="sxs-lookup"><span data-stu-id="148d3-173">In your PowerShell window, enter hello `login-azurermaccount` command toosign in with your Azure [account](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#account).</span></span> <span data-ttu-id="148d3-174">Jeśli nie masz już konto, możesz zarejestrować się w celu [bezpłatnej wersji próbnej](https://azure.microsoft.com/offers/ms-azr-0044p).</span><span class="sxs-lookup"><span data-stu-id="148d3-174">If you don't already have an account, you can sign up for a [free trial](https://azure.microsoft.com/offers/ms-azr-0044p).</span></span>
4. <span data-ttu-id="148d3-175">W przeglądarce skopiuj hello następującego skryptu:</span><span class="sxs-lookup"><span data-stu-id="148d3-175">In your browser, copy hello following script:</span></span>
    ```powershell
    $RgName="MyResourceGroup"
    $Location="westus2"
    
    # Create a resource group
    New-AzureRmResourceGroup `
      -Name $RgName `
      -Location $Location
    
    # Create a subnet
    $Subnet = New-AzureRmVirtualNetworkSubnetConfig `
      -Name MySubnet `
      -AddressPrefix 10.0.0.0/24
    
    # Create a virtual network
    $Vnet=New-AzureRmVirtualNetwork `
      -ResourceGroupName $RgName `
      -Location $Location `
      -Name MyVnet `
      -AddressPrefix 10.0.0.0/16 `
      -Subnet $Subnet

    # Create a public IP address
    $Pip = New-AzureRmPublicIpAddress `
      -Name MyPublicIp `
      -ResourceGroupName $RgName `
      -Location $Location `
      -AllocationMethod Static

    # Create a virtual network interface and associate hello public IP address tooit
    $Nic = New-AzureRmNetworkInterface `
      -Name MyNic `
      -ResourceGroupName $RgName `
      -Location $Location `
      -SubnetId $Vnet.Subnets[0].Id `
      -PublicIpAddressId $Pip.Id `
      -EnableAcceleratedNetworking
     
    # Define a credential object for hello VM. PowerShell prompts you for a username and password.
    $Cred = Get-Credential

    # Create a virtual machine configuration
    $VmConfig = New-AzureRmVMConfig `
      -VMName MyVM -VMSize Standard_DS4_v2 | `
      Set-AzureRmVMOperatingSystem `
      -Windows `
      -ComputerName myVM `
      -Credential $Cred | `
    Set-AzureRmVMSourceImage `
      -PublisherName MicrosoftWindowsServer `
      -Offer WindowsServer `
      -Skus 2016-Datacenter `
      -Version latest | `
    Add-AzureRmVMNetworkInterface -Id $Nic.Id 

    # Create hello virtual machine.    
    New-AzureRmVM `
      -ResourceGroupName $RgName `
      -Location $Location `
      -VM $VmConfig
    #
    ```
5. <span data-ttu-id="148d3-176">W oknie programu PowerShell kliknij prawym przyciskiem myszy skrypt hello toopaste i uruchomienia jej wykonanie.</span><span class="sxs-lookup"><span data-stu-id="148d3-176">In your PowerShell window, right-click toopaste hello script and start executing it.</span></span> <span data-ttu-id="148d3-177">Zostanie wyświetlony monit o nazwę użytkownika i hasło.</span><span class="sxs-lookup"><span data-stu-id="148d3-177">You are prompted for a username and password.</span></span> <span data-ttu-id="148d3-178">Użyj toolog te poświadczenia w toohello maszyny Wirtualnej, łącząc tooit w hello następnego kroku.</span><span class="sxs-lookup"><span data-stu-id="148d3-178">Use these credentials toolog in toohello VM when connecting tooit in hello next step.</span></span> <span data-ttu-id="148d3-179">Jeśli hello skrypt zakończy się niepowodzeniem, a wartości w skrypcie hello zostały zmienione przed jego wykonaniem, potwierdzić wartości hello używane dla rozmiaru maszyny Wirtualnej, system operacyjny i lokalizacja znajduje się w hello [ograniczenia](#Limitations) sekcji tego artykułu.</span><span class="sxs-lookup"><span data-stu-id="148d3-179">If hello script fails, and you changed values in hello script before executing it, confirm hello values you used for VM size, operating system, and location are listed in hello [Limitations](#Limitations) section of this article.</span></span>
6. <span data-ttu-id="148d3-180">tooinstall hello przyspieszony sterowników sieciowych systemu Windows, pełną hello etapami hello [Konfigurowanie systemu Windows](#configure-windows) sekcji tego artykułu.</span><span class="sxs-lookup"><span data-stu-id="148d3-180">tooinstall hello accelerated networking driver for Windows, complete hello steps in hello [Configure Windows](#configure-windows) section of this article.</span></span>

### <span data-ttu-id="148d3-181"><a name="configure-windows"></a>Konfigurowanie systemu Windows</span><span class="sxs-lookup"><span data-stu-id="148d3-181"><a name="configure-windows"></a>Configure Windows</span></span>
<span data-ttu-id="148d3-182">Po utworzeniu hello maszyny Wirtualnej na platformie Azure, należy zainstalować sterownik sieciowy przyspieszonego powitania dla systemu Windows.</span><span class="sxs-lookup"><span data-stu-id="148d3-182">Once you create hello VM in Azure, you must install hello accelerated networking driver for Windows.</span></span> <span data-ttu-id="148d3-183">Przed wykonaniem hello następujące kroki, należy utworzyć Maszynę wirtualną systemu Windows z przyspieszonego w sieci przy użyciu albo hello [portal](#windows-portal) lub [PowerShell](#windows-powershell) kroków w tym artykule.</span><span class="sxs-lookup"><span data-stu-id="148d3-183">Before completing hello following steps, you must have created a Windows VM with accelerated networking using either hello [portal](#windows-portal) or [PowerShell](#windows-powershell) steps in this article.</span></span> 

1. <span data-ttu-id="148d3-184">Za pomocą przeglądarki internetowej, otwórz hello Azure [portal](https://portal.azure.com) i zaloguj się przy użyciu platformy Azure [konta](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#account).</span><span class="sxs-lookup"><span data-stu-id="148d3-184">From an Internet browser, open hello Azure [portal](https://portal.azure.com) and sign in with your Azure [account](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#account).</span></span> <span data-ttu-id="148d3-185">Jeśli nie masz już konto, możesz zarejestrować się w celu [bezpłatnej wersji próbnej](https://azure.microsoft.com/offers/ms-azr-0044p).</span><span class="sxs-lookup"><span data-stu-id="148d3-185">If you don't already have an account, you can sign up for a [free trial](https://azure.microsoft.com/offers/ms-azr-0044p).</span></span>
2. <span data-ttu-id="148d3-186">W polu hello, które zawiera tekst hello *wyszukiwania zasobów* u góry hello hello portalu Azure, wpisz *MyVm*.</span><span class="sxs-lookup"><span data-stu-id="148d3-186">In hello box that contains hello text *Search resources* at hello top of hello Azure portal, type *MyVm*.</span></span> <span data-ttu-id="148d3-187">Gdy **MyVm** pojawia się w wynikach wyszukiwania hello, kliknij ją.</span><span class="sxs-lookup"><span data-stu-id="148d3-187">When **MyVm** appears in hello search results, click it.</span></span>
3. <span data-ttu-id="148d3-188">W hello **MyVm** bloku, który jest wyświetlany, kliknij przycisk hello **Connect** przycisku na powitania lewym górnym rogu bloku hello.</span><span class="sxs-lookup"><span data-stu-id="148d3-188">In hello **MyVm** blade that appears, click hello **Connect** button in hello top left corner of hello blade.</span></span> <span data-ttu-id="148d3-189">**Uwaga:** Jeśli **tworzenie** jest widoczna w obszarze hello **Connect** przycisku Azure nie została jeszcze ukończona tworzenie hello maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="148d3-189">**Note:** If **Creating** is visible under hello **Connect** button, Azure has not yet finished creating hello VM.</span></span> <span data-ttu-id="148d3-190">Kliknij przycisk **Connect** tylko wtedy, gdy nie są już wyświetlane **tworzenie** w obszarze hello **Connect** przycisku.</span><span class="sxs-lookup"><span data-stu-id="148d3-190">Click **Connect** only after you no longer see **Creating** under hello **Connect** button.</span></span>
4. <span data-ttu-id="148d3-191">Zezwalaj na powitania toodownload Twojego przeglądarki **MyVm.rdp** pliku.</span><span class="sxs-lookup"><span data-stu-id="148d3-191">Allow your browser toodownload hello **MyVm.rdp** file.</span></span>  <span data-ttu-id="148d3-192">Po pobraniu, kliknij przycisk tooopen pliku hello go.</span><span class="sxs-lookup"><span data-stu-id="148d3-192">Once downloaded, click hello file tooopen it.</span></span> 
5. <span data-ttu-id="148d3-193">Kliknij przycisk hello **Connect** przycisku na powitania **Podłączanie pulpitu zdalnego** wyświetlonym, powiadamianie o tym, że hello nie można zidentyfikować wydawcy tego połączenia zdalnego hello.</span><span class="sxs-lookup"><span data-stu-id="148d3-193">Click hello **Connect** button in hello **Remote Desktop Connection** box that appears, notifying you that hello publisher of hello remote connection can't be identified.</span></span>
6. <span data-ttu-id="148d3-194">W hello **zabezpieczenia systemu Windows** okno zostanie wyświetlone, kliknij przycisk **więcej opcji**, następnie kliknij przycisk **korzystała z innego konta**.</span><span class="sxs-lookup"><span data-stu-id="148d3-194">In hello **Windows Security** box that appears, click **More choices**, then click **Use a different account**.</span></span> <span data-ttu-id="148d3-195">Wprowadź hello nazwy użytkownika i hasła podanego w kroku 4, a następnie kliknij przycisk hello **OK** przycisku.</span><span class="sxs-lookup"><span data-stu-id="148d3-195">Enter hello username and password you entered in step 4, then click hello **OK** button.</span></span>
7. <span data-ttu-id="148d3-196">Kliknij przycisk hello **tak** przycisk pojawi się powiadomienie, że nie można zweryfikować tożsamości komputera zdalnego hello hello okno Podłączanie pulpitu zdalnego hello.</span><span class="sxs-lookup"><span data-stu-id="148d3-196">Click hello **Yes** button in hello Remote Desktop Connection box that appears, notifying you that hello identity of hello remote computer cannot be verified.</span></span>
8. <span data-ttu-id="148d3-197">Kliknij prawym przyciskiem myszy przycisk Start systemu Windows hello, a następnie kliknij przycisk **Menedżera urządzeń**.</span><span class="sxs-lookup"><span data-stu-id="148d3-197">Right-click hello Windows Start button and click **Device Manager**.</span></span> <span data-ttu-id="148d3-198">Rozwiń węzeł hello **karty sieciowe** węzła.</span><span class="sxs-lookup"><span data-stu-id="148d3-198">Expand hello **Network adapters** node.</span></span> <span data-ttu-id="148d3-199">Upewnij się, że hello **Mellanox ConnectX 3 wirtualnej funkcja Ethernet karty** pojawia się, jak pokazano na poniższej ilustracji hello:</span><span class="sxs-lookup"><span data-stu-id="148d3-199">Confirm that hello **Mellanox ConnectX-3 Virtual Function Ethernet Adapter** appears, as shown in hello following picture:</span></span>
   
    ![Menedżer urządzeń](./media/virtual-network-create-vm-accelerated-networking/image2.png)

9. <span data-ttu-id="148d3-201">Przyspieszone sieci jest teraz włączony dla maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="148d3-201">Accelerated Networking is now enabled for your VM.</span></span>

## <a name="create-a-linux-vm"></a><span data-ttu-id="148d3-202">Tworzenie maszyny wirtualnej z systemem Linux</span><span class="sxs-lookup"><span data-stu-id="148d3-202">Create a Linux VM</span></span>
<span data-ttu-id="148d3-203">Możesz użyć hello portalu Azure lub Azure [PowerShell](#linux-powershell) toocreate Ubuntu lub SLES maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="148d3-203">You can use hello Azure portal or Azure [PowerShell](#linux-powershell) toocreate an Ubuntu or SLES VM.</span></span> <span data-ttu-id="148d3-204">RHEL i maszyny wirtualnej CentOS istnieje inny przepływ pracy.</span><span class="sxs-lookup"><span data-stu-id="148d3-204">For RHEL and CentOS VMs there is a different workflow.</span></span>  <span data-ttu-id="148d3-205">Zobacz poniższe instrukcje hello.</span><span class="sxs-lookup"><span data-stu-id="148d3-205">Please see hello instructions below.</span></span>

### <span data-ttu-id="148d3-206"><a name="linux-portal"></a>Portal</span><span class="sxs-lookup"><span data-stu-id="148d3-206"><a name="linux-portal"></a>Portal</span></span>
1. <span data-ttu-id="148d3-207">Rejestr hello przyspieszony sieci dla systemu Linux w wersji zapoznawczej, wykonując kroki 1 – 5 hello [utworzyć Maszynę wirtualną systemu Linux - PowerShell](#linux-powershell) sekcji tego artykułu.</span><span class="sxs-lookup"><span data-stu-id="148d3-207">Register for hello accelerated networking for Linux preview by completing steps 1-5 of hello [Create a Linux VM - PowerShell](#linux-powershell) section of this article.</span></span>  <span data-ttu-id="148d3-208">Możesz zarejestrować się w wersji zapoznawczej hello w portalu hello.</span><span class="sxs-lookup"><span data-stu-id="148d3-208">You cannot register for hello preview in hello portal.</span></span>
2. <span data-ttu-id="148d3-209">Zakończenie kroki 1 – 8 hello w [utworzyć Maszynę wirtualną systemu Windows — portal](#windows-portal) sekcji tego artykułu.</span><span class="sxs-lookup"><span data-stu-id="148d3-209">Complete steps 1-8 in hello [Create a Windows VM - portal](#windows-portal) section of this article.</span></span> <span data-ttu-id="148d3-210">W kroku 2 kliknij **Ubuntu Server 16.04 LTS** zamiast **systemu Windows Server Datacenter 2016**.</span><span class="sxs-lookup"><span data-stu-id="148d3-210">In step 2, click **Ubuntu Server 16.04 LTS** instead of **Windows Server 2016 Datacenter**.</span></span> <span data-ttu-id="148d3-211">W tym samouczku wybierz toouse hasła, a nie kluczem SSH, chociaż wdrożeń produkcyjnych, możesz użyć dowolnej.</span><span class="sxs-lookup"><span data-stu-id="148d3-211">For this tutorial, choose toouse a password, rather than an SSH key, though for production deployments, you can use either.</span></span> <span data-ttu-id="148d3-212">Jeśli **przyspieszony sieci** nie pojawia się po wykonaniu kroku 7 hello [utworzyć Maszynę wirtualną systemu Windows — portal](#windows-portal) sekcji tego artykułu, prawdopodobnie jednego hello z następujących powodów:</span><span class="sxs-lookup"><span data-stu-id="148d3-212">If **Accelerated networking** does not appear when you complete step 7 of hello [Create a Windows VM - portal](#windows-portal) section of this article, it's likely for one of hello following reasons:</span></span>
    - <span data-ttu-id="148d3-213">Możesz nie zostały jeszcze zarejestrowane hello podglądu.</span><span class="sxs-lookup"><span data-stu-id="148d3-213">You are not yet registered for hello preview.</span></span> <span data-ttu-id="148d3-214">Upewnij się, że stan użytkownika rejestracji to **zarejestrowanej**, zgodnie z objaśnieniem w kroku 4 hello [utworzyć Maszynę wirtualną systemu Linux - Powershell](#linux-powershell) sekcji tego artykułu.</span><span class="sxs-lookup"><span data-stu-id="148d3-214">Confirm that your registration state is **Registered**, as explained in step 4 of hello [Create a Linux VM - Powershell](#linux-powershell) section of this article.</span></span> <span data-ttu-id="148d3-215">**Uwaga:** Jeśli udział w hello akcelerowanego sieci dla maszyn wirtualnych systemu Windows w wersji zapoznawczej (jego nie dłużej toouse niezbędne tooregister przyspieszony sieci dla maszyn wirtualnych systemu Windows), możesz nie są automatycznie zarejestrowane dla hello akcelerowanego sieci dla Podgląd maszyn wirtualnych systemu Linux.</span><span class="sxs-lookup"><span data-stu-id="148d3-215">**Note:** If you participated in hello Accelerated networking for Windows VMs preview (it's no longer necessary tooregister toouse Accelerated networking for Windows VMs), you are not automatically registered for hello Accelerated networking for Linux VMs preview.</span></span> <span data-ttu-id="148d3-216">Należy zarejestrować dla hello akcelerowanego sieci dla maszyn wirtualnych systemu Linux Podgląd tooparticipate w nim.</span><span class="sxs-lookup"><span data-stu-id="148d3-216">You must register for hello Accelerated networking for Linux VMs preview tooparticipate in it.</span></span>
    - <span data-ttu-id="148d3-217">Nie wybrano rozmiar maszyny Wirtualnej, system operacyjny lub lokalizacji na liście hello [ograniczenia](#limitations) sekcji tego artykułu.</span><span class="sxs-lookup"><span data-stu-id="148d3-217">You have not selected a VM size, operating system, or location listed in hello [Limitations](#limitations) section of this article.</span></span>
3. <span data-ttu-id="148d3-218">tooinstall hello przyspieszony sterownik sieciowy dla systemu Linux, pełną hello etapami hello [skonfigurować Linux](#configure-linux) sekcji tego artykułu.</span><span class="sxs-lookup"><span data-stu-id="148d3-218">tooinstall hello accelerated networking driver for Linux, complete hello steps in hello [Configure Linux](#configure-linux) section of this article.</span></span>

### <span data-ttu-id="148d3-219"><a name="linux-powershell"></a>Środowiska PowerShell</span><span class="sxs-lookup"><span data-stu-id="148d3-219"><a name="linux-powershell"></a>PowerShell</span></span>

>[!WARNING]
><span data-ttu-id="148d3-220">Jeśli Tworzenie maszyn wirtualnych systemu Linux z przyspieszonego sieci w ramach subskrypcji, a następnie spróbuj toocreate maszyny Wirtualnej systemu Windows z przyspieszonego sieci w programie hello tej samej subskrypcji, hello tworzenia maszyny Wirtualnej systemu Windows może zakończyć się niepowodzeniem.</span><span class="sxs-lookup"><span data-stu-id="148d3-220">If you create Linux VMs with accelerated networking in a subscription, and then attempt toocreate a Windows VM with accelerated networking in hello same subscription, hello Windows VM creation may fail.</span></span> <span data-ttu-id="148d3-221">Tej wersji zapoznawczej zaleca się testowanie systemu Linux i maszyn wirtualnych systemu Windows z przyspieszonego sieci w oddzielnych subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="148d3-221">During this preview, it's recommended that you test Linux and Windows VMs with accelerated networking in separate subscriptions.</span></span>
>

1. <span data-ttu-id="148d3-222">Zainstaluj najnowszą wersję hello Azure PowerShell hello [AzureRm](https://www.powershellgallery.com/packages/AzureRM/) modułu.</span><span class="sxs-lookup"><span data-stu-id="148d3-222">Install hello latest version of hello Azure PowerShell [AzureRm](https://www.powershellgallery.com/packages/AzureRM/) module.</span></span> <span data-ttu-id="148d3-223">Jeśli jesteś tooAzure nowego środowiska PowerShell odczytu hello [Omówienie programu Azure PowerShell](/powershell/azure/get-started-azureps?toc=%2fazure%2fvirtual-network%2ftoc.json) artykułu.</span><span class="sxs-lookup"><span data-stu-id="148d3-223">If you're new tooAzure PowerShell, read hello [Azure PowerShell overview](/powershell/azure/get-started-azureps?toc=%2fazure%2fvirtual-network%2ftoc.json) article.</span></span>
2. <span data-ttu-id="148d3-224">Uruchom sesję programu PowerShell, klikając przycisk Start systemu Windows hello, wpisując **środowiska powershell**, klikając **PowerShell** hello wyników wyszukiwania.</span><span class="sxs-lookup"><span data-stu-id="148d3-224">Start a PowerShell session by clicking hello Windows Start button, typing **powershell**, then clicking **PowerShell** from hello search results.</span></span>
3. <span data-ttu-id="148d3-225">W oknie programu PowerShell, wprowadź hello `login-azurermaccount` toosign polecenia przy użyciu platformy Azure [konta](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#account).</span><span class="sxs-lookup"><span data-stu-id="148d3-225">In your PowerShell window, enter hello `login-azurermaccount` command toosign in with your Azure [account](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#account).</span></span> <span data-ttu-id="148d3-226">Jeśli nie masz już konto, możesz zarejestrować się w celu [bezpłatnej wersji próbnej](https://azure.microsoft.com/offers/ms-azr-0044p).</span><span class="sxs-lookup"><span data-stu-id="148d3-226">If you don't already have an account, you can sign up for a [free trial](https://azure.microsoft.com/offers/ms-azr-0044p).</span></span>
4. <span data-ttu-id="148d3-227">Rejestr hello przyspieszony sieci platformy Azure w wersji zapoznawczej, wykonując następujące kroki hello:</span><span class="sxs-lookup"><span data-stu-id="148d3-227">Register for hello accelerated networking for Azure preview by completing hello following steps:</span></span>
    - <span data-ttu-id="148d3-228">Wyślij wiadomość e-mail zbyt[ axnpreview@microsoft.com ](mailto:axnpreview@microsoft.com?subject=Request%20to%20enable%20subscription%20%3csubscription%20id%3e) identyfikator subskrypcji platformy Azure i zamierzonego użycia.</span><span class="sxs-lookup"><span data-stu-id="148d3-228">Send an email too[axnpreview@microsoft.com](mailto:axnpreview@microsoft.com?subject=Request%20to%20enable%20subscription%20%3csubscription%20id%3e) with your Azure subscription ID and intended use.</span></span> <span data-ttu-id="148d3-229">Poczekaj, aż wiadomość e-mail z potwierdzeniem od firmy Microsoft dotyczące włączania subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="148d3-229">Please wait for an email confirmation from Microsoft about your subscription being enabled.</span></span>
    - <span data-ttu-id="148d3-230">Wprowadź następujące tooconfirm polecenia, które są zarejestrowane dla podglądu hello hello:</span><span class="sxs-lookup"><span data-stu-id="148d3-230">Enter hello following command tooconfirm you are registered for hello preview:</span></span>
    
        ```powershell
        Get-AzureRmProviderFeature -FeatureName AllowAcceleratedNetworkingForLinux -ProviderNamespace Microsoft.Network
        ```

        <span data-ttu-id="148d3-231">Nie wykonuj kroku 5 do **zarejestrowanej** pojawia się w hello dane wyjściowe po wprowadzeniu hello poprzednie polecenie.</span><span class="sxs-lookup"><span data-stu-id="148d3-231">Do not continue with step 5 until **Registered** appears in hello output after you enter hello previous command.</span></span> <span data-ttu-id="148d3-232">Dane wyjściowe musi wyglądać hello następujących danych wyjściowych, aby kontynuować:</span><span class="sxs-lookup"><span data-stu-id="148d3-232">Your output must look like hello following output before continuing:</span></span>
    
        ```powershell
        FeatureName                        ProviderName      RegistrationState
        -----------                        ------------      -----------------
        AllowAcceleratedNetworkingForLinux Microsoft.Network Registered
        ```
        
      >[!NOTE]
      ><span data-ttu-id="148d3-233">Jeśli udział w hello akcelerowanego sieci dla maszyn wirtualnych systemu Windows w wersji zapoznawczej (jego nie dłużej toouse niezbędne tooregister przyspieszony sieci dla maszyn wirtualnych systemu Windows), możesz nie są automatycznie zarejestrowane dla hello akcelerowanego sieci dla maszyn wirtualnych systemu Linux w wersji zapoznawczej.</span><span class="sxs-lookup"><span data-stu-id="148d3-233">If you participated in hello Accelerated networking for Windows VMs preview (it's no longer necessary tooregister toouse Accelerated networking for Windows VMs), you are not automatically registered for hello Accelerated networking for Linux VMs preview.</span></span> <span data-ttu-id="148d3-234">Należy zarejestrować dla hello akcelerowanego sieci dla maszyn wirtualnych systemu Linux Podgląd tooparticipate w nim.</span><span class="sxs-lookup"><span data-stu-id="148d3-234">You must register for hello Accelerated networking for Linux VMs preview tooparticipate in it.</span></span>
      >
5. <span data-ttu-id="148d3-235">W przeglądarce skopiuj hello następującego skryptu, zastępując Ubuntu lub SLES zgodnie z potrzebami.</span><span class="sxs-lookup"><span data-stu-id="148d3-235">In your browser, copy hello following script substituting Ubuntu or SLES as desired.</span></span>  <span data-ttu-id="148d3-236">Ponownie Redhat i CentOS ma inny przepływ pracy przedstawione poniżej:</span><span class="sxs-lookup"><span data-stu-id="148d3-236">Again, Redhat and CentOS have a different workflow outlined below:</span></span>

    ```powershell
    $RgName="MyResourceGroup"
    $Location="westus2"
    
    # Create a resource group
    New-AzureRmResourceGroup `
      -Name $RgName `
      -Location $Location
    
    # Create a subnet
    $Subnet = New-AzureRmVirtualNetworkSubnetConfig `
      -Name MySubnet `
      -AddressPrefix 10.0.0.0/24
    
    # Create a virtual network
    $Vnet=New-AzureRmVirtualNetwork `
      -ResourceGroupName $RgName `
      -Location $Location `
      -Name MyVnet `
      -AddressPrefix 10.0.0.0/16 `
      -Subnet $Subnet

    # Create a public IP address
    $Pip = New-AzureRmPublicIpAddress `
      -Name MyPublicIp `
      -ResourceGroupName $RgName `
      -Location $Location `
      -AllocationMethod Static

    # Create a virtual network interface and associate hello public IP address tooit
    $Nic = New-AzureRmNetworkInterface `
      -Name MyNic `
      -ResourceGroupName $RgName `
      -Location $Location `
      -SubnetId $Vnet.Subnets[0].Id `
      -PublicIpAddressId $Pip.Id `
      -EnableAcceleratedNetworking
     
    # Create a new Storage account and define hello new VM’s OSDisk name and its URI
    # Must end with ".vhd" extension
    $OSDiskName = "MyOsDiskName.vhd"
    # Storage account name must be between 3 and 24 characters in length and use numbers and lower-case letters only.
    $OSDiskSAName = "thestorageaccountname"  
    $StorageAccount = New-AzureRmStorageAccount -ResourceGroupName $RgName -Name $OSDiskSAName -Type "Standard_GRS" -Location $Location
    $OSDiskUri = $StorageAccount.PrimaryEndpoints.Blob.ToString() + "vhds/" + $OSDiskName
 
    # Define a credential object for hello VM. PowerShell prompts you for a username and password.
    $Cred = Get-Credential

    # Create a virtual machine configuration
    $VmConfig = New-AzureRmVMConfig `
      -VMName MyVM -VMSize Standard_DS4_v2 | `
      Set-AzureRmVMOperatingSystem `
      -Linux `
      -ComputerName myVM `
      -Credential $Cred | `
    Set-AzureRmVMSourceImage `
      -PublisherName Canonical `
      -Offer UbuntuServer `
      -Skus 16.04-LTS `
      -Version latest | `
    Add-AzureRmVMNetworkInterface -Id $Nic.Id | `
    Set-AzureRmVMOSDisk -Name $OSDiskName `
      -VhdUri $OSDiskUri `
      -CreateOption FromImage 

    # Create hello virtual machine.    
    New-AzureRmVM `
      -ResourceGroupName $RgName `
      -Location $Location `
      -VM $VmConfig
    ```
    
6. <span data-ttu-id="148d3-237">W oknie programu PowerShell kliknij prawym przyciskiem myszy skrypt hello toopaste i uruchomienia jej wykonanie.</span><span class="sxs-lookup"><span data-stu-id="148d3-237">In your PowerShell window, right-click toopaste hello script and start executing it.</span></span> <span data-ttu-id="148d3-238">Zostanie wyświetlony monit o nazwę użytkownika i hasło.</span><span class="sxs-lookup"><span data-stu-id="148d3-238">You are prompted for a username and password.</span></span> <span data-ttu-id="148d3-239">Użyj toolog te poświadczenia w toohello maszyny Wirtualnej, łącząc tooit w hello następnego kroku.</span><span class="sxs-lookup"><span data-stu-id="148d3-239">Use these credentials toolog in toohello VM when connecting tooit in hello next step.</span></span> <span data-ttu-id="148d3-240">Jeśli skrypt hello zakończy się niepowodzeniem, upewnij się, że:</span><span class="sxs-lookup"><span data-stu-id="148d3-240">If hello script fails, confirm that:</span></span>
    - <span data-ttu-id="148d3-241">Zarejestrowanych dla podglądu hello, zgodnie z objaśnieniem w kroku 4</span><span class="sxs-lookup"><span data-stu-id="148d3-241">You are registered for hello preview, as explained in step 4</span></span>
    - <span data-ttu-id="148d3-242">Jeśli zmieniono rozmiar, typ systemu operacyjnego lub wartości lokalizacji w skrypcie hello maszyny Wirtualnej przed wykonaniem go, że wartości hello są wymienione w hello [ograniczenia](#Limitations) sekcji tego artykułu.</span><span class="sxs-lookup"><span data-stu-id="148d3-242">If you changed VM size, operating system type, or location values in hello script before executing it, that hello values are listed in hello [Limitations](#Limitations) section of this article.</span></span>
7. <span data-ttu-id="148d3-243">tooinstall hello przyspieszony sterownik sieciowy dla systemu Linux, pełną hello etapami hello [skonfigurować Linux](#configure-linux) sekcji tego artykułu.</span><span class="sxs-lookup"><span data-stu-id="148d3-243">tooinstall hello accelerated networking driver for Linux, complete hello steps in hello [Configure Linux](#configure-linux) section of this article.</span></span>

### <span data-ttu-id="148d3-244"><a name="configure-linux"></a>Konfigurowanie systemu Linux</span><span class="sxs-lookup"><span data-stu-id="148d3-244"><a name="configure-linux"></a>Configure Linux</span></span>

<span data-ttu-id="148d3-245">Po utworzeniu hello maszyny Wirtualnej na platformie Azure, należy zainstalować sterownik sieciowy przyspieszonego powitania dla systemu Linux.</span><span class="sxs-lookup"><span data-stu-id="148d3-245">Once you create hello VM in Azure, you must install hello accelerated networking driver for Linux.</span></span> <span data-ttu-id="148d3-246">Przed wykonaniem hello następujące kroki, należy utworzyć Maszynę wirtualną systemu Linux z przyspieszonego w sieci przy użyciu albo hello [portal](#linux-portal) lub [PowerShell](#linux-powershell) kroków w tym artykule.</span><span class="sxs-lookup"><span data-stu-id="148d3-246">Before completing hello following steps, you must have created a Linux VM with accelerated networking using either hello [portal](#linux-portal) or [PowerShell](#linux-powershell) steps in this article.</span></span> 

1. <span data-ttu-id="148d3-247">Za pomocą przeglądarki internetowej, otwórz hello Azure [portal](https://portal.azure.com) i zaloguj się przy użyciu platformy Azure [konta](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#account).</span><span class="sxs-lookup"><span data-stu-id="148d3-247">From an Internet browser, open hello Azure [portal](https://portal.azure.com) and sign in with your Azure [account](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#account).</span></span> <span data-ttu-id="148d3-248">Jeśli nie masz już konto, możesz zarejestrować się w celu [bezpłatnej wersji próbnej](https://azure.microsoft.com/offers/ms-azr-0044p).</span><span class="sxs-lookup"><span data-stu-id="148d3-248">If you don't already have an account, you can sign up for a [free trial](https://azure.microsoft.com/offers/ms-azr-0044p).</span></span>
2. <span data-ttu-id="148d3-249">U góry hello hello portalu prawym toohello hello *wyszukiwania zasobów* pasek, kliknij przycisk hello **> _** toostart ikona powłoki Bash chmury (wersja zapoznawcza).</span><span class="sxs-lookup"><span data-stu-id="148d3-249">At hello top of hello portal, toohello right of hello *Search resources* bar, click hello **>_** icon toostart a Bash cloud shell (Preview).</span></span> <span data-ttu-id="148d3-250">przedstawia informacje o Hello Bash chmury powłoki pojawi się okienko dole hello hello portalu po kilku sekundach  **username@Azure:~ $** wiersza.</span><span class="sxs-lookup"><span data-stu-id="148d3-250">hello Bash cloud shell pane appears at hello bottom of hello portal and after a few seconds, presents a **username@Azure:~$** prompt.</span></span> <span data-ttu-id="148d3-251">Chociaż możesz toohello SSH maszyny Wirtualnej z Twojego komputera zamiast hello chmury powłoki hello instrukcje w tym samouczku założono, że używasz hello chmury powłoki.</span><span class="sxs-lookup"><span data-stu-id="148d3-251">Though you can SSH toohello VM from your computer, rather than hello cloud shell, hello instructions in this tutorial assume you're using hello cloud shell.</span></span>
3. <span data-ttu-id="148d3-252">U góry hello hello portalu, w polu hello zawierający tekst hello *wyszukiwania zasobów*, typ *MyVm*.</span><span class="sxs-lookup"><span data-stu-id="148d3-252">At hello top of hello portal, in hello box that contains hello text *Search resources*, type *MyVm*.</span></span> <span data-ttu-id="148d3-253">Gdy **MyVm** pojawia się w wynikach wyszukiwania hello, kliknij ją.</span><span class="sxs-lookup"><span data-stu-id="148d3-253">When **MyVm** appears in hello search results, click it.</span></span>
4. <span data-ttu-id="148d3-254">W hello **MyVm** bloku, który jest wyświetlany, kliknij przycisk hello **Connect** przycisku na powitania lewym górnym rogu bloku hello.</span><span class="sxs-lookup"><span data-stu-id="148d3-254">In hello **MyVm** blade that appears, click hello **Connect** button in hello top left corner of hello blade.</span></span> <span data-ttu-id="148d3-255">**Uwaga:** Jeśli **tworzenie** jest widoczna w obszarze hello **Connect** przycisku Azure nie została jeszcze ukończona tworzenie hello maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="148d3-255">**Note:** If **Creating** is visible under hello **Connect** button, Azure has not yet finished creating hello VM.</span></span> <span data-ttu-id="148d3-256">Kliknij przycisk **Connect** tylko wtedy, gdy nie są już wyświetlane **tworzenie** w obszarze hello **Connect** przycisku.</span><span class="sxs-lookup"><span data-stu-id="148d3-256">Click **Connect** only after you no longer see **Creating** under hello **Connect** button.</span></span>
5. <span data-ttu-id="148d3-257">Azure zostanie otwarte okno informujący tooenter hello `ssh adminuser@<ipaddress>`.</span><span class="sxs-lookup"><span data-stu-id="148d3-257">Azure opens a box telling you tooenter hello `ssh adminuser@<ipaddress>`.</span></span> <span data-ttu-id="148d3-258">Wprowadź polecenie w hello chmury powłoki (lub kopiowania go z hello pola, które znajdowały się w kroku 4 i wklej go w powłoce chmury toohello), naciśnij klawisz Enter.</span><span class="sxs-lookup"><span data-stu-id="148d3-258">Enter this command in hello cloud shell (or copy it from hello box that appeared in step 4 and paste it in toohello cloud shell), then press Enter.</span></span>
6. <span data-ttu-id="148d3-259">Wprowadź **tak** pytanie toohello pytania, możesz Jeśli toocontinue połączenie, naciśnij klawisz Enter.</span><span class="sxs-lookup"><span data-stu-id="148d3-259">Enter **yes** toohello question asking you if you want toocontinue connecting, then press Enter.</span></span>
7. <span data-ttu-id="148d3-260">Wprowadź hasło hello, wprowadzona podczas tworzenia hello maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="148d3-260">Enter hello password you entered when creating hello VM.</span></span> <span data-ttu-id="148d3-261">Po pomyślnym zalogowaniu toohello maszyny Wirtualnej, zostanie wyświetlony adminuser@MyVm:~ $ wiersza.</span><span class="sxs-lookup"><span data-stu-id="148d3-261">Once successfully logged in toohello VM, you see an adminuser@MyVm:~$ prompt.</span></span> <span data-ttu-id="148d3-262">Zalogowano Cię teraz toohello maszyny Wirtualnej za pośrednictwem sesję powłoki hello chmury.</span><span class="sxs-lookup"><span data-stu-id="148d3-262">You are now logged in toohello VM through hello cloud shell session.</span></span> <span data-ttu-id="148d3-263">**Uwaga:** limit czasu sesji powłoki w chmurze po 10 minutach braku aktywności.</span><span class="sxs-lookup"><span data-stu-id="148d3-263">**Note:** Cloud shell sessions time out after 10 minutes of inactivity.</span></span>

<span data-ttu-id="148d3-264">W tym momencie instrukcje hello różnić w zależności od dystrybucji hello, którego używasz.</span><span class="sxs-lookup"><span data-stu-id="148d3-264">At this point, hello instructions vary based on hello distribution you are using.</span></span> 

#### <a name="ubuntusles"></a><span data-ttu-id="148d3-265">Ubuntu/SLES</span><span class="sxs-lookup"><span data-stu-id="148d3-265">Ubuntu/SLES</span></span>

1. <span data-ttu-id="148d3-266">W wierszu hello wprowadź `uname -r` i Potwierdź hello wersji:</span><span class="sxs-lookup"><span data-stu-id="148d3-266">At hello prompt, enter `uname -r` and confirm hello version for:</span></span>

    * <span data-ttu-id="148d3-267">Ubuntu jest "4.4.0-77-generic," lub nowszej</span><span class="sxs-lookup"><span data-stu-id="148d3-267">Ubuntu is "4.4.0-77-generic," or greater</span></span>
    * <span data-ttu-id="148d3-268">SLES jest "4.4.59-92.20-default" lub nowszej</span><span class="sxs-lookup"><span data-stu-id="148d3-268">SLES is "4.4.59-92.20-default" or greater</span></span>

2. <span data-ttu-id="148d3-269">Utworzyć rentowność między hello standardowe vNIC sieci i vNIC sieci hello przyspieszony uruchomionych poleceń hello, które należy wykonać.</span><span class="sxs-lookup"><span data-stu-id="148d3-269">Create a bond between hello standard networking vNIC and hello accelerated networking vNIC by running hello commands that follow.</span></span> <span data-ttu-id="148d3-270">Ruch sieciowy używa hello wyższej wykonywania przyspieszonego sieci wirtualnej karty sieciowej, podczas gdy rentowność hello zapewnia ruchu sieciowego nie zostało przerwane przez niektóre zmiany konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="148d3-270">Network traffic uses hello higher performing accelerated networking vNIC, while hello bond ensures that networking traffic is not interrupted across certain configuration changes.</span></span>
          
     ```bash
     wget https://raw.githubusercontent.com/LIS/lis-next/master/tools/sriov/configure_hv_sriov.sh
     chmod +x ./configure_hv_sriov.sh
     sudo ./configure_hv_sriov.sh
     ```
3. <span data-ttu-id="148d3-271">Po uruchamianie skryptu hello hello maszyna wirtualna zostanie ponownie uruchomiona po wstrzymać 60 sekund.</span><span class="sxs-lookup"><span data-stu-id="148d3-271">After running hello script, hello VM will restart after a 60 second pause.</span></span>
4. <span data-ttu-id="148d3-272">Raz powitalne maszyna wirtualna zostanie ponownie uruchomiony, ponownie połącz tooit wykonując kroki 5-7.</span><span class="sxs-lookup"><span data-stu-id="148d3-272">Once hello VM is restarted, reconnect tooit by completing steps 5-7 again.</span></span>
5. <span data-ttu-id="148d3-273">Uruchom hello `ifconfig` polecenie i Potwierdź, że została znaleziona bond0 i interfejs hello jest wyświetlany jako zapasowe.</span><span class="sxs-lookup"><span data-stu-id="148d3-273">Run hello `ifconfig` command and confirm that bond0 has come up and hello interface is showing as UP.</span></span> 
 
 >[!NOTE]
      ><span data-ttu-id="148d3-274">Aplikacje przy użyciu przyspieszonego sieci muszą komunikować się za pośrednictwem hello *bond0* interfejs nie *eth0*.</span><span class="sxs-lookup"><span data-stu-id="148d3-274">Applications using accelerated networking must communicate over hello *bond0* interface, not *eth0*.</span></span>  <span data-ttu-id="148d3-275">Nazwa interfejsu Hello może się zmienić przed przyspieszonego sieci osiągnie ogólnej dostępności.</span><span class="sxs-lookup"><span data-stu-id="148d3-275">hello interface name may change before accelerated networking reaches general availability.</span></span>

#### <a name="rhelcentos"></a><span data-ttu-id="148d3-276">RHEL/CentOS</span><span class="sxs-lookup"><span data-stu-id="148d3-276">RHEL/CentOS</span></span>

<span data-ttu-id="148d3-277">W celu utworzenia Red Hat Enterprise Linux lub wirtualna 7.3 CentOS wymagane pewne dodatkowe kroki tooload hello najnowszej wersji sterowników wymaganych dla funkcji SR-IOV i hello sterownik funkcji wirtualnej funkcji (Wirtualnej) dla karty sieciowej hello.</span><span class="sxs-lookup"><span data-stu-id="148d3-277">Creating a Red Hat Enterprise Linux or CentOS 7.3 VM requires some extra steps tooload hello latest drivers needed for SR-IOV and hello Virtual Function (VF) driver for hello network card.</span></span> <span data-ttu-id="148d3-278">Hello pierwszą fazę instrukcje hello przygotowuje obraz, który może być używane toomake maszyn wirtualnych, które sterowniki hello wstępnie załadowane.</span><span class="sxs-lookup"><span data-stu-id="148d3-278">hello first phase of hello instructions prepares an image that can be used toomake one or more virtual machines that have hello drivers pre-loaded.</span></span>

##### <a name="phase-one-prepare-a-red-hat-enterprise-linux-or-centos-73-base-image"></a><span data-ttu-id="148d3-279">Pierwszej fazy: przygotowanie Red Hat Enterprise Linux lub CentOS 7.3 obrazu podstawowego.</span><span class="sxs-lookup"><span data-stu-id="148d3-279">Phase one: prepare a Red Hat Enterprise Linux or CentOS 7.3 base image.</span></span> 

1.  <span data-ttu-id="148d3-280">Udostępnianie nie - funkcji SR-IOV CentOS 7.3 Maszynę wirtualną na platformie Azure</span><span class="sxs-lookup"><span data-stu-id="148d3-280">Provision a non-SRIOV CentOS 7.3 VM on Azure</span></span>

2.  <span data-ttu-id="148d3-281">Instalowania usług LIS 4.2.2:</span><span class="sxs-lookup"><span data-stu-id="148d3-281">Install LIS 4.2.2:</span></span>
    
    ```bash
    wget http://download.microsoft.com/download/6/8/F/68FE11B8-FAA4-4F8D-8C7D-74DA7F2CFC8C/lis-rpms-4.2.2-2.tar.gz
    tar -xvf lis-rpms-4.2.2-2.tar.gz
    cd LISISO && sudo ./install.sh
    ```

3.  <span data-ttu-id="148d3-282">Pobierz pliki konfiguracji</span><span class="sxs-lookup"><span data-stu-id="148d3-282">Download config files</span></span>
    
    ```bash
    cd /etc/udev/rules.d/  
    sudo wget https://raw.githubusercontent.com/LIS/lis-next/master/tools/sriov/60-hyperv-vf-name.rules 
    cd /usr/sbin/
    sudo wget https://raw.githubusercontent.com/LIS/lis-next/master/tools/sriov/hv_vf_name 
    sudo chmod +x hv_vf_name
    cd /etc/sysconfig/network-scripts/
    sudo wget https://raw.githubusercontent.com/LIS/lis-next/master/tools/sriov/ifcfg-vf1   
    ```

4.  <span data-ttu-id="148d3-283">Anulowanie zastrzeżenia tej maszyny Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="148d3-283">Deprovision this VM</span></span>

    ```bash
    sudo waagent -deprovision+user 
    ```

5.  <span data-ttu-id="148d3-284">Z portalu Azure Zatrzymaj tę maszynę Wirtualną; Przejdź przez tooVM "dyskami", przechwytywania hello OSDisk identyfikator URI dysku VHD.</span><span class="sxs-lookup"><span data-stu-id="148d3-284">From Azure portal, stop this VM; and go tooVM’s "Disks", capture hello OSDisk’s VHD URI.</span></span> <span data-ttu-id="148d3-285">Ten identyfikator URI zawiera nazwę dysku VHD hello obrazu podstawowego i jego konta magazynu.</span><span class="sxs-lookup"><span data-stu-id="148d3-285">This URI contains hello base image’s VHD name and its storage account.</span></span> 
 
##### <a name="phase-two-provision-new-vms-on-azure"></a><span data-ttu-id="148d3-286">Dwie fazy: obsługi administracyjnej nowych maszyn wirtualnych na platformie Azure</span><span class="sxs-lookup"><span data-stu-id="148d3-286">Phase two: Provision new VMs on Azure</span></span>

1.  <span data-ttu-id="148d3-287">Obsługi administracyjnej nowych maszyn wirtualnych na podstawie AzureRMVMConfig nowy przy użyciu hello obraz podstawowy dysk VHD przechwycone na etapie, za pomocą AcceleratedNetworking włączona na karcie vNIC hello:</span><span class="sxs-lookup"><span data-stu-id="148d3-287">Provision new VMs based with New-AzureRMVMConfig using hello base image VHD captured in phase one, with AcceleratedNetworking enabled on hello vNIC:</span></span>

    ```powershell
    $RgName="MyResourceGroup"
    $Location="westus2"
    
    # Create a resource group
    New-AzureRmResourceGroup `
     -Name $RgName `
     -Location $Location

    # Create a subnet
    $Subnet = New-AzureRmVirtualNetworkSubnetConfig `
     -Name MySubnet `
     -AddressPrefix 10.0.0.0/24

    # Create a virtual network
    $Vnet=New-AzureRmVirtualNetwork `
     -ResourceGroupName $RgName `
     -Location $Location `
     -Name MyVnet `
     -AddressPrefix 10.0.0.0/16 `
     -Subnet $Subnet
    
    # Create a public IP address
    $Pip = New-AzureRmPublicIpAddress `
     -Name MyPublicIp `
     -ResourceGroupName $RgName `
     -Location $Location `
     -AllocationMethod Static
    
    # Create a virtual network interface and associate hello public IP address tooit
    $Nic = New-AzureRmNetworkInterface `
     -Name MyNic `
     -ResourceGroupName $RgName `
     -Location $Location `
     -SubnetId $Vnet.Subnets[0].Id `
     -PublicIpAddressId $Pip.Id `
     -EnableAcceleratedNetworking
    
    # Specify hello base image's VHD URI (from phase one step 5). 
    # Note: hello storage account of this base image vhd should have "Storage service encryption" disabled
    # See more from here: https://docs.microsoft.com/en-us/azure/storage/storage-service-encryption
    # This is just an example URI, you will need tooreplace this when running this script
    $sourceUri="https://myexamplesa.blob.core.windows.net/vhds/CentOS73-Base-Test120170629111341.vhd" 

    # Specify a URI for hello location from which hello new image binary large object (BLOB) is copied toostart hello virtual machine. 
    # Must end with ".vhd" extension
    $OsDiskName = "MyOsDiskName.vhd" 
    $destOsDiskUri = "https://myexamplesa.blob.core.windows.net/vhds/" + $OsDiskName
    
    # Define a credential object for hello VM. PowerShell prompts you for a username and password.
    $Cred = Get-Credential
    
    # Create a custom virtual machine configuration
    $VmConfig = New-AzureRmVMConfig `
     -VMName MyVM -VMSize Standard_DS4_v2 | `
    Set-AzureRmVMOperatingSystem `
     -Linux `
     -ComputerName myVM `
     -Credential $Cred | `
    Add-AzureRmVMNetworkInterface -Id $Nic.Id | `
    Set-AzureRmVMOSDisk `
     -Name $OsDiskName `
     -SourceImageUri $sourceUri `
     -VhdUri $destOsDiskUri `
     -CreateOption FromImage `
     -Linux
    
    # Create hello virtual machine.    
    New-AzureRmVM `
     -ResourceGroupName $RgName `
     -Location $Location `
     -VM $VmConfig
    ```

2.  <span data-ttu-id="148d3-288">Po rozruchu maszyn wirtualnych, urządzenia funkcji Wirtualnej hello przez "lspci" i Sprawdź wpis Mellanox hello.</span><span class="sxs-lookup"><span data-stu-id="148d3-288">After VMs boot up, check hello VF device by "lspci" and check hello Mellanox entry.</span></span> <span data-ttu-id="148d3-289">Na przykład możemy powinien zostać wyświetlony ten element w danych wyjściowych lspci hello:</span><span class="sxs-lookup"><span data-stu-id="148d3-289">For example, we should see this item in hello lspci output:</span></span>
    
    ```
    0001:00:02.0 Ethernet controller: Mellanox Technologies MT27500/MT27520 Family [ConnectX-3/ConnectX-3 Pro Virtual Function]
    ```
    
3.  <span data-ttu-id="148d3-290">Uruchom skrypt przez hello przez:</span><span class="sxs-lookup"><span data-stu-id="148d3-290">Run hello bonding script by:</span></span>

    ```bash
    sudo bondvf.sh
    ```

4.  <span data-ttu-id="148d3-291">Ponowny rozruch hello nowych maszyn wirtualnych:</span><span class="sxs-lookup"><span data-stu-id="148d3-291">Reboot hello new VMs:</span></span>

    ```bash
    sudo reboot
    ```

<span data-ttu-id="148d3-292">Hello wirtualna powinien się rozpoczynać od bond0 skonfigurowany i hello ścieżki przyspieszony sieci włączone.</span><span class="sxs-lookup"><span data-stu-id="148d3-292">hello VM should start with bond0 configured and hello Accelerated Networking path enabled.</span></span>  <span data-ttu-id="148d3-293">Uruchom `ifconfig` tooconfirm.</span><span class="sxs-lookup"><span data-stu-id="148d3-293">Run `ifconfig` tooconfirm.</span></span>
