---
title: "maszyny wirtualne aaaReplicate funkcji Hyper-V w chmurach programu VMM przy użyciu usługi Azure Site Recovery i środowiska PowerShell (Resource Manager) | Dokumentacja firmy Microsoft"
description: "Replikowanie maszyn wirtualnych funkcji Hyper-V w chmurach programu VMM przy użyciu usługi Azure Site Recovery i programu PowerShell"
services: site-recovery
documentationcenter: 
author: Rajani-Janaki-Ram
manager: rochakm
editor: raynew
ms.assetid: 6ac509ad-5024-43d8-b621-d8fec019b9a9
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/05/2017
ms.author: rajanaki
ms.openlocfilehash: b0f641de4e10a600ead415ceb9bd488fb4d1659d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="replicate-hyper-v-virtual-machines-in-vmm-clouds-tooazure-using-powershell-and-azure-resource-manager"></a><span data-ttu-id="b7939-103">Replikowanie maszyn wirtualnych funkcji Hyper-V w tooAzure chmur programu VMM przy użyciu programu PowerShell i usługi Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="b7939-103">Replicate Hyper-V virtual machines in VMM clouds tooAzure using PowerShell and Azure Resource Manager</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="b7939-104">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="b7939-104">Azure Portal</span></span>](site-recovery-vmm-to-azure.md)
> * [<span data-ttu-id="b7939-105">Program PowerShell — model usługi Resource Manager</span><span class="sxs-lookup"><span data-stu-id="b7939-105">PowerShell - Resource Manager</span></span>](site-recovery-vmm-to-azure-powershell-resource-manager.md)
> * [<span data-ttu-id="b7939-106">Klasyczny portal</span><span class="sxs-lookup"><span data-stu-id="b7939-106">Classic Portal</span></span>](site-recovery-vmm-to-azure-classic.md)
> * [<span data-ttu-id="b7939-107">PowerShell — model klasyczny</span><span class="sxs-lookup"><span data-stu-id="b7939-107">PowerShell - Classic</span></span>](site-recovery-deploy-with-powershell.md)
>
>

## <a name="overview"></a><span data-ttu-id="b7939-108">Omówienie</span><span class="sxs-lookup"><span data-stu-id="b7939-108">Overview</span></span>
<span data-ttu-id="b7939-109">Usługa Azure Site Recovery przyczynia się tooyour ciągłości i odzyskiwaniem po awarii (BCDR) odzyskiwania strategii biznesowej poprzez organizowanie replikacji, trybu failover i odzyskiwania maszyn wirtualnych w różnych scenariuszy wdrażania.</span><span class="sxs-lookup"><span data-stu-id="b7939-109">Azure Site Recovery contributes tooyour business continuity and disaster recovery (BCDR) strategy by orchestrating replication, failover and recovery of virtual machines in a number of deployment scenarios.</span></span> <span data-ttu-id="b7939-110">Pełną listę wdrażania scenariuszy dla hello [Omówienie usługi Azure Site Recovery](site-recovery-overview.md).</span><span class="sxs-lookup"><span data-stu-id="b7939-110">For a full list of deployment scenarios see hello [Azure Site Recovery overview](site-recovery-overview.md).</span></span>

<span data-ttu-id="b7939-111">W tym artykule opisano, jak toouse PowerShell tooautomate typowych zadań należy tooperform podczas konfigurowania maszyny wirtualne funkcji Hyper-V tooreplicate usługi Azure Site Recovery w magazynie tooAzure chmur programu System Center VMM.</span><span class="sxs-lookup"><span data-stu-id="b7939-111">This article shows you how toouse PowerShell tooautomate common tasks you need tooperform when you set up Azure Site Recovery tooreplicate Hyper-V virtual machines in System Center VMM clouds tooAzure storage.</span></span>

<span data-ttu-id="b7939-112">Hello artykuł zawiera wymagania wstępne dla scenariusza hello i pokazuje</span><span class="sxs-lookup"><span data-stu-id="b7939-112">hello article includes prerequisites for hello scenario, and shows you</span></span>

* <span data-ttu-id="b7939-113">Jak tooset się magazynu usług odzyskiwania</span><span class="sxs-lookup"><span data-stu-id="b7939-113">How tooset up a Recovery Services Vault</span></span>
* <span data-ttu-id="b7939-114">Zainstaluj hello dostawcy usługi Azure Site Recovery na źródłowym serwerze programu VMM hello</span><span class="sxs-lookup"><span data-stu-id="b7939-114">Install hello Azure Site Recovery Provider on hello source VMM server</span></span>
* <span data-ttu-id="b7939-115">Zarejestruj serwer hello w magazynie hello, Dodaj konto magazynu platformy Azure</span><span class="sxs-lookup"><span data-stu-id="b7939-115">Register hello server in hello vault, add an Azure storage account</span></span>
* <span data-ttu-id="b7939-116">Zainstaluj agenta usług odzyskiwania Azure hello na serwerach hostów funkcji Hyper-V</span><span class="sxs-lookup"><span data-stu-id="b7939-116">Install hello Azure Recovery Services agent on Hyper-V host servers</span></span>
* <span data-ttu-id="b7939-117">Skonfiguruj ustawienia ochrony chmury VMM, które mają być zastosowane tooall chronione maszyny wirtualne</span><span class="sxs-lookup"><span data-stu-id="b7939-117">Configure protection settings for VMM clouds, that will be applied tooall protected virtual machines</span></span>
* <span data-ttu-id="b7939-118">Włącz ochronę tych maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="b7939-118">Enable protection for those virtual machines.</span></span>
* <span data-ttu-id="b7939-119">Przetestuj hello awaryjnej toomake się, że wszystko działa zgodnie z oczekiwaniami.</span><span class="sxs-lookup"><span data-stu-id="b7939-119">Test hello fail-over toomake sure everything's working as expected.</span></span>

<span data-ttu-id="b7939-120">Jeśli napotkasz problem ze skonfigurowaniem w tym scenariuszu Opublikuj swoje pytania na powitania [Forum usług odzyskiwania Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="b7939-120">If you run into problems setting up this scenario, post your questions on hello [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>

> [!NOTE]
> <span data-ttu-id="b7939-121">Platforma Azure ma dwa różne modele wdrażania do tworzenia i pracy z zasobami: [Resource Manager i Model Klasyczny](../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="b7939-121">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../azure-resource-manager/resource-manager-deployment-model.md).</span></span> <span data-ttu-id="b7939-122">W tym artykule omówiono przy użyciu modelu wdrażania usługi Resource Manager hello.</span><span class="sxs-lookup"><span data-stu-id="b7939-122">This article covers using hello Resource Manager deployment model.</span></span>
>
>

## <a name="before-you-start"></a><span data-ttu-id="b7939-123">Przed rozpoczęciem</span><span class="sxs-lookup"><span data-stu-id="b7939-123">Before you start</span></span>
<span data-ttu-id="b7939-124">Upewnij się, że te wymagania wstępne zostały spełnione:</span><span class="sxs-lookup"><span data-stu-id="b7939-124">Make sure you have these prerequisites in place:</span></span>

### <a name="azure-prerequisites"></a><span data-ttu-id="b7939-125">Wymagania wstępne platformy Azure</span><span class="sxs-lookup"><span data-stu-id="b7939-125">Azure prerequisites</span></span>
* <span data-ttu-id="b7939-126">Będziesz potrzebować konta platformy [Microsoft Azure](https://azure.microsoft.com/).</span><span class="sxs-lookup"><span data-stu-id="b7939-126">You'll need a [Microsoft Azure](https://azure.microsoft.com/) account.</span></span> <span data-ttu-id="b7939-127">Jeśli nie masz, Rozpocznij od [bezpłatne konto](https://azure.microsoft.com/free).</span><span class="sxs-lookup"><span data-stu-id="b7939-127">If you don't have one, start with a [free account](https://azure.microsoft.com/free).</span></span> <span data-ttu-id="b7939-128">Ponadto możesz przeczytać temat hello [cennik usługi Azure Site Recovery Manager](https://azure.microsoft.com/pricing/details/site-recovery/).</span><span class="sxs-lookup"><span data-stu-id="b7939-128">In addition, you can read about hello [Azure Site Recovery Manager pricing](https://azure.microsoft.com/pricing/details/site-recovery/).</span></span>
* <span data-ttu-id="b7939-129">Będziesz potrzebować subskrypcji dostawcy usług Kryptograficznych, jeśli próbujesz się hello replikacji tooa dostawcy usług Kryptograficznych subskrypcji scenariusza.</span><span class="sxs-lookup"><span data-stu-id="b7939-129">You'll need a CSP subscription if you are trying out hello replication tooa CSP subscription scenario.</span></span> <span data-ttu-id="b7939-130">Dowiedz się więcej o programie dostawcy usług Kryptograficznych hello w [jak tooenroll w programie dostawcy usług Kryptograficznych hello](https://msdn.microsoft.com/library/partnercenter/mt156995.aspx).</span><span class="sxs-lookup"><span data-stu-id="b7939-130">Learn more about hello CSP program in [how tooenroll in hello CSP program](https://msdn.microsoft.com/library/partnercenter/mt156995.aspx).</span></span>
* <span data-ttu-id="b7939-131">Będziesz potrzebować tooAzure danych replikowanych toostore konta platformy Azure w wersji 2 magazynu (Resource Manager).</span><span class="sxs-lookup"><span data-stu-id="b7939-131">You'll need an Azure v2 storage (Resource Manager) account toostore data replicated tooAzure.</span></span> <span data-ttu-id="b7939-132">Konto Hello musi włączyć replikację geograficzną.</span><span class="sxs-lookup"><span data-stu-id="b7939-132">hello account needs geo-replication enabled.</span></span> <span data-ttu-id="b7939-133">Należy go w hello na tym samym regionie co hello usługi Azure Site Recovery i musi być skojarzone z hello tej samej subskrypcji lub hello dostawcy usług Kryptograficznych subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="b7939-133">It should be in hello same region as hello Azure Site Recovery service, and be associated with hello same subscription or hello CSP subscription.</span></span> <span data-ttu-id="b7939-134">toolearn więcej informacji na temat konfigurowania magazynu Azure, zobacz hello [tooMicrosoft wprowadzenie usługi Azure Storage](../storage/common/storage-introduction.md) odwołania.</span><span class="sxs-lookup"><span data-stu-id="b7939-134">toolearn more about setting up Azure storage, see hello [Introduction tooMicrosoft Azure Storage](../storage/common/storage-introduction.md) for reference.</span></span>
* <span data-ttu-id="b7939-135">Należy się upewnić, że maszyny wirtualne mają tooprotect spełniają hello toomake [wymagania wstępne maszyny wirtualnej platformy Azure](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements).</span><span class="sxs-lookup"><span data-stu-id="b7939-135">You'll need toomake sure that virtual machines you want tooprotect comply with hello [Azure virtual machine prerequisites](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements).</span></span>

> [!NOTE]
> <span data-ttu-id="b7939-136">Obecnie tylko operacje poziomu maszyny Wirtualnej jest możliwe za pośrednictwem programu Powershell.</span><span class="sxs-lookup"><span data-stu-id="b7939-136">Currently, only VM level operations are possible through Powershell.</span></span> <span data-ttu-id="b7939-137">Obsługa operacji poziomu planu odzyskiwania zostaną wprowadzone wkrótce.</span><span class="sxs-lookup"><span data-stu-id="b7939-137">Support for recovery plan level operations will be made soon.</span></span>  <span data-ttu-id="b7939-138">Obecnie masz ograniczone tooperforming przełączanie w trybie Failover tylko na poziom szczegółowości "chronione maszyny Wirtualnej", a nie na poziomie planu odzyskiwania.</span><span class="sxs-lookup"><span data-stu-id="b7939-138">For now, you are limited tooperforming fail-overs only at a ‘protected VM’ granularity and not at a Recovery Plan level.</span></span>
>
>

### <a name="vmm-prerequisites"></a><span data-ttu-id="b7939-139">Wymagania wstępne programu VMM</span><span class="sxs-lookup"><span data-stu-id="b7939-139">VMM prerequisites</span></span>
* <span data-ttu-id="b7939-140">Należy na serwerze programu VMM działa na System Center 2012 R2.</span><span class="sxs-lookup"><span data-stu-id="b7939-140">You'll need VMM server running on System Center 2012 R2.</span></span>
* <span data-ttu-id="b7939-141">Żadnym serwerze VMM obejmującego maszyny wirtualne mają tooprotect musi być uruchomiona hello dostawcy usługi Azure Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="b7939-141">Any VMM server containing virtual machines you want tooprotect must be running hello Azure Site Recovery Provider.</span></span> <span data-ttu-id="b7939-142">To jest instalowany podczas wdrażania usługi Azure Site Recovery hello.</span><span class="sxs-lookup"><span data-stu-id="b7939-142">This is installed during hello Azure Site Recovery deployment.</span></span>
* <span data-ttu-id="b7939-143">Będziesz potrzebować co najmniej jedna chmura na powitania serwera VMM ma tooprotect.</span><span class="sxs-lookup"><span data-stu-id="b7939-143">You'll need at least one cloud on hello VMM server you want tooprotect.</span></span> <span data-ttu-id="b7939-144">Chmura Hello powinna zawierać:</span><span class="sxs-lookup"><span data-stu-id="b7939-144">hello cloud should contain:</span></span>
  * <span data-ttu-id="b7939-145">Co najmniej jedną grupę hostów programu VMM.</span><span class="sxs-lookup"><span data-stu-id="b7939-145">One or more VMM host groups.</span></span>
  * <span data-ttu-id="b7939-146">Co najmniej jeden serwer hosta lub klaster funkcji Hyper-V w każdej grupie hostów.</span><span class="sxs-lookup"><span data-stu-id="b7939-146">One or more Hyper-V host servers or clusters in each host group.</span></span>
  * <span data-ttu-id="b7939-147">Co najmniej jednej maszyny wirtualnej na powitania serwera źródłowego funkcji Hyper-V.</span><span class="sxs-lookup"><span data-stu-id="b7939-147">One or more virtual machines on hello source Hyper-V server.</span></span>
* <span data-ttu-id="b7939-148">Dowiedz się więcej o konfigurowaniu chmur VMM:</span><span class="sxs-lookup"><span data-stu-id="b7939-148">Learn more about setting up VMM clouds:</span></span>
  * <span data-ttu-id="b7939-149">Dowiedz się więcej o prywatnych chmur programu VMM [What's New in chmury prywatnej z programu System Center 2012 R2 VMM](http://go.microsoft.com/fwlink/?LinkId=324952) i [chmur VMM 2012 i hello](http://go.microsoft.com/fwlink/?LinkId=324956).</span><span class="sxs-lookup"><span data-stu-id="b7939-149">Read more about private VMM clouds in [What’s New in Private Cloud with System Center 2012 R2 VMM](http://go.microsoft.com/fwlink/?LinkId=324952) and in [VMM 2012 and hello clouds](http://go.microsoft.com/fwlink/?LinkId=324956).</span></span>
  * <span data-ttu-id="b7939-150">Dowiedz się więcej o [sieci szkieletowej chmury hello Konfigurowanie programu VMM](https://msdn.microsoft.com/library/azure/dn469075.aspx#BKMK_Fabric)</span><span class="sxs-lookup"><span data-stu-id="b7939-150">Learn about [Configuring hello VMM cloud fabric](https://msdn.microsoft.com/library/azure/dn469075.aspx#BKMK_Fabric)</span></span>
  * <span data-ttu-id="b7939-151">Po elementów sieci szkieletowej chmury w miejscu więcej informacji o tworzeniu chmur prywatnych w [tworzenia chmury prywatnej w programie VMM](http://go.microsoft.com/fwlink/p/?LinkId=324953) i [wskazówki: tworzenie chmur prywatnych z programu System Center 2012 SP1 VMM](http://go.microsoft.com/fwlink/p/?LinkId=324954).</span><span class="sxs-lookup"><span data-stu-id="b7939-151">After your cloud fabric elements are in place learn about creating private clouds in [Creating a private cloud in VMM](http://go.microsoft.com/fwlink/p/?LinkId=324953) and in [Walkthrough: Creating private clouds with System Center 2012 SP1 VMM](http://go.microsoft.com/fwlink/p/?LinkId=324954).</span></span>

### <a name="hyper-v-prerequisites"></a><span data-ttu-id="b7939-152">Wymagania wstępne funkcji Hyper-V</span><span class="sxs-lookup"><span data-stu-id="b7939-152">Hyper-V prerequisites</span></span>
* <span data-ttu-id="b7939-153">Witaj Serwery hosta funkcji Hyper-V musi działać co najmniej **systemu Windows Server 2012** z rolą funkcji Hyper-V lub **Microsoft Hyper-V Server 2012** i mieć hello zainstalowane najnowsze aktualizacje.</span><span class="sxs-lookup"><span data-stu-id="b7939-153">hello host Hyper-V servers must be running at least **Windows Server 2012** with Hyper-V role or **Microsoft Hyper-V Server 2012** and have hello latest updates installed.</span></span>
* <span data-ttu-id="b7939-154">Jeśli używasz funkcji Hyper-V w klastrze, broker klastra nie jest tworzony automatycznie, jeśli masz klaster oparty na statycznym adresie IP.</span><span class="sxs-lookup"><span data-stu-id="b7939-154">If you're running Hyper-V in a cluster note that cluster broker isn't created automatically if you have a static IP address-based cluster.</span></span> <span data-ttu-id="b7939-155">Będziesz potrzebować brokera klastra hello tooconfigure ręcznie.</span><span class="sxs-lookup"><span data-stu-id="b7939-155">You'll need tooconfigure hello cluster broker manually.</span></span> <span data-ttu-id="b7939-156">dla</span><span class="sxs-lookup"><span data-stu-id="b7939-156">For</span></span>
* <span data-ttu-id="b7939-157">Instrukcje można znaleźć [jak tooConfigure brokera funkcji Hyper-V Replica](http://blogs.technet.com/b/haroldwong/archive/2013/03/27/server-virtualization-series-hyper-v-replica-broker-explained-part-15-of-20-by-yung-chou.aspx).</span><span class="sxs-lookup"><span data-stu-id="b7939-157">For instructions see [How tooConfigure Hyper-V Replica Broker](http://blogs.technet.com/b/haroldwong/archive/2013/03/27/server-virtualization-series-hyper-v-replica-broker-explained-part-15-of-20-by-yung-chou.aspx).</span></span>
* <span data-ttu-id="b7939-158">Dowolnego serwera hosta funkcji Hyper-V lub klaster, dla którego ma zostać toomanage ochrony musi być uwzględniona w chmurze VMM.</span><span class="sxs-lookup"><span data-stu-id="b7939-158">Any Hyper-V host server or cluster for which you want toomanage protection must be included in a VMM cloud.</span></span>

### <a name="network-mapping-prerequisites"></a><span data-ttu-id="b7939-159">Wymagania wstępne związane z mapowaniem sieci</span><span class="sxs-lookup"><span data-stu-id="b7939-159">Network mapping prerequisites</span></span>
<span data-ttu-id="b7939-160">W przypadku ochrony maszyn wirtualnych na platformie Azure, mapowanie sieci hello mapuje hello sieci maszyn wirtualnych na źródłowym serwerze programu VMM hello i docelowej sieci platformy Azure tooenable hello poniżej:</span><span class="sxs-lookup"><span data-stu-id="b7939-160">When you protect virtual machines in Azure, hello network mapping  maps hello virtual machine networks on hello source VMM server and target Azure networks tooenable hello following:</span></span>

* <span data-ttu-id="b7939-161">Wszystkie komputery, które w tryb failover na powitania sam połączyć tooeach innych, niezależnie od tego, jakiego planu odzyskiwania, które znajdują się w sieci.</span><span class="sxs-lookup"><span data-stu-id="b7939-161">All machines which fail over on hello same network can connect tooeach other, irrespective of which recovery plan they are in.</span></span>
* <span data-ttu-id="b7939-162">Jeśli brama sieci została skonfigurowana w hello docelową sieć platformy Azure, maszyny wirtualne można łączyć z tooother lokalnych maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="b7939-162">If a network gateway is setup on hello target Azure network, virtual machines can connect tooother on-premises virtual machines.</span></span>
* <span data-ttu-id="b7939-163">Jeśli nie skonfigurujesz mapowania sieci tylko hello maszyn wirtualnych, które w tryb failover w hello sam plan odzyskiwania będą mogli tooconnect tooeach innych po tooAzure awaryjnej.</span><span class="sxs-lookup"><span data-stu-id="b7939-163">If you don’t configure network mapping, only hello virtual machines that fail over in hello same recovery plan will be able tooconnect tooeach other after fail-over tooAzure.</span></span>

<span data-ttu-id="b7939-164">Jeśli chcesz, aby mapowanie sieci toodeploy potrzebne są następujące hello:</span><span class="sxs-lookup"><span data-stu-id="b7939-164">If you want toodeploy network mapping you'll need hello following:</span></span>

* <span data-ttu-id="b7939-165">maszyny wirtualne Hello ma tooprotect na źródłowym serwerze programu VMM hello powinna być tooa połączonych sieci maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="b7939-165">hello virtual machines you want tooprotect on hello source VMM server should be connected tooa VM network.</span></span> <span data-ttu-id="b7939-166">Ta sieć powinna być tooa połączone sieci logicznej, która jest skojarzona z chmurą hello.</span><span class="sxs-lookup"><span data-stu-id="b7939-166">That network should be linked tooa logical network that is associated with hello cloud.</span></span>
* <span data-ttu-id="b7939-167">Maszyny wirtualne replikowane toowhich sieć platformy Azure mogą łączyć po awaryjnym.</span><span class="sxs-lookup"><span data-stu-id="b7939-167">An Azure network toowhich replicated virtual machines can connect after fail-over.</span></span> <span data-ttu-id="b7939-168">Należy wybrać tej sieci w czasie hello awaryjnym.</span><span class="sxs-lookup"><span data-stu-id="b7939-168">You'll select this network at hello time of fail-over.</span></span> <span data-ttu-id="b7939-169">Witaj sieć powinna znajdować się w hello tym samym regionie co subskrypcja usługi Azure Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="b7939-169">hello network should be in hello same region as your Azure Site Recovery subscription.</span></span>

<span data-ttu-id="b7939-170">Dowiedz się więcej o mapowanie sieci w</span><span class="sxs-lookup"><span data-stu-id="b7939-170">Learn more about network mapping in</span></span>

* [<span data-ttu-id="b7939-171">Jak tooconfigure sieci logicznych w programie VMM</span><span class="sxs-lookup"><span data-stu-id="b7939-171">How tooconfigure logical networks in VMM</span></span>](http://go.microsoft.com/fwlink/p/?LinkId=386307)
* [<span data-ttu-id="b7939-172">Jak tooconfigure maszyny Wirtualnej sieci i bram w programie VMM</span><span class="sxs-lookup"><span data-stu-id="b7939-172">How tooconfigure VM networks and gateways in VMM</span></span>](http://go.microsoft.com/fwlink/p/?LinkId=386308)
* [<span data-ttu-id="b7939-173">Jak tooconfigure i monitor sieci wirtualne na platformie Azure</span><span class="sxs-lookup"><span data-stu-id="b7939-173">How tooconfigure and monitor virtual networks in Azure</span></span>](https://azure.microsoft.com/documentation/services/virtual-network/)

### <a name="powershell-prerequisites"></a><span data-ttu-id="b7939-174">Wymagania wstępne programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="b7939-174">PowerShell prerequisites</span></span>
<span data-ttu-id="b7939-175">Upewnij się, że masz toogo gotowy programu Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="b7939-175">Make sure you have Azure PowerShell ready toogo.</span></span> <span data-ttu-id="b7939-176">Jeśli korzystasz już z programu PowerShell, potrzebujesz tooupgrade tooversion 0.8.10 lub nowszym.</span><span class="sxs-lookup"><span data-stu-id="b7939-176">If you are already using PowerShell, you'll need tooupgrade tooversion 0.8.10 or later.</span></span> <span data-ttu-id="b7939-177">Aby uzyskać informacje o konfigurowaniu programu PowerShell, zobacz hello [prowadzą tooinstall i konfigurowanie programu Azure PowerShell](/powershell/azureps-cmdlets-docs).</span><span class="sxs-lookup"><span data-stu-id="b7939-177">For information about setting up PowerShell, see hello [Guide tooinstall and configure Azure PowerShell](/powershell/azureps-cmdlets-docs).</span></span> <span data-ttu-id="b7939-178">Po należy skonfigurować i skonfigurowaniu programu PowerShell można wyświetlić wszystkie dostępne polecenia cmdlet hello hello usługi [tutaj](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="b7939-178">Once you have set up and configured PowerShell, you can view all of hello available cmdlets for hello service [here](/powershell/azure/overview).</span></span>

<span data-ttu-id="b7939-179">toolearn o porad ułatwiających przy użyciu poleceń cmdlet hello, takich jak jak wartości parametru, dane wejściowe i dane wyjściowe są zazwyczaj obsługiwane w programie Azure PowerShell, zobacz hello [przewodnik tooget uruchomiona za pomocą poleceń cmdlet Azure](/powershell/azure/get-started-azureps).</span><span class="sxs-lookup"><span data-stu-id="b7939-179">toolearn about tips that can help you use hello cmdlets, such as how parameter values, inputs, and outputs are typically handled in Azure PowerShell, see hello [Guide tooget Started with Azure Cmdlets](/powershell/azure/get-started-azureps).</span></span>

## <a name="step-1-set-hello-subscription"></a><span data-ttu-id="b7939-180">Krok 1: Ustaw hello subskrypcji</span><span class="sxs-lookup"><span data-stu-id="b7939-180">Step 1: Set hello subscription</span></span>
1. <span data-ttu-id="b7939-181">Z programu Azure powershell tooyour logowania konta platformy Azure: za pomocą następującego polecenia cmdlet hello</span><span class="sxs-lookup"><span data-stu-id="b7939-181">From Azure powershell, login tooyour Azure account: using hello following cmdlets</span></span>

        $UserName = "<user@live.com>"
        $Password = "<password>"
        $SecurePassword = ConvertTo-SecureString -AsPlainText $Password -Force
        $Cred = New-Object System.Management.Automation.PSCredential -ArgumentList $UserName, $SecurePassword
        Login-AzureRmAccount #-Credential $Cred
2. <span data-ttu-id="b7939-182">Pobierz listę subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="b7939-182">Get a list of your subscriptions.</span></span> <span data-ttu-id="b7939-183">To wyświetla również hello subscriptionIDs dla każdego hello subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="b7939-183">This will also list hello subscriptionIDs for each of hello subscriptions.</span></span> <span data-ttu-id="b7939-184">Zanotuj identyfikator subskrypcji hello hello subskrypcji, w którym chcesz magazynu usług odzyskiwania hello toocreate</span><span class="sxs-lookup"><span data-stu-id="b7939-184">Note down hello subscriptionID of hello subscription in which you wish toocreate hello recovery services vault</span></span>

        Get-AzureRmSubscription
3. <span data-ttu-id="b7939-185">Ustaw hello subskrypcji, w których hello magazynu usług odzyskiwania jest utworzony, podając identyfikator subskrypcji hello toobe</span><span class="sxs-lookup"><span data-stu-id="b7939-185">Set hello subscription in which hello recovery services vault is toobe created by mentioning hello subscription ID</span></span>

        Set-AzureRmContext –SubscriptionID <subscriptionId>

## <a name="step-2-create-a-recovery-services-vault"></a><span data-ttu-id="b7939-186">Krok 2. Tworzenie magazynu Usług odzyskiwania</span><span class="sxs-lookup"><span data-stu-id="b7939-186">Step 2: Create a Recovery Services vault</span></span>
1. <span data-ttu-id="b7939-187">Utwórz grupę zasobów usługi Azure Resource Manager, jeśli nie masz już</span><span class="sxs-lookup"><span data-stu-id="b7939-187">Create a resource group  in Azure Resource Manager if you don't have one already</span></span>

        New-AzureRmResourceGroup -Name #ResourceGroupName -Location #location
2. <span data-ttu-id="b7939-188">Utwórz nowy magazyn usług odzyskiwania i zapisać hello utworzony obiekt magazynu ASR w zmiennej (zostanie później użyty).</span><span class="sxs-lookup"><span data-stu-id="b7939-188">Create a new Recovery Services vault and save hello created ASR vault object in a variable (will be used later).</span></span> <span data-ttu-id="b7939-189">Można również pobierać hello ASR magazynu obiektu post tworzenia przy użyciu polecenia cmdlet Get-AzureRMRecoveryServicesVault hello:-</span><span class="sxs-lookup"><span data-stu-id="b7939-189">You can also retrieve hello ASR vault object post creation using hello Get-AzureRMRecoveryServicesVault cmdlet:-</span></span>

        $vault = New-AzureRmRecoveryServicesVault -Name #vaultname -ResouceGroupName #ResourceGroupName -Location #location

## <a name="step-3-set-hello-recovery-services-vault-context"></a><span data-ttu-id="b7939-190">Krok 3: Ustaw hello kontekst magazynu usług odzyskiwania</span><span class="sxs-lookup"><span data-stu-id="b7939-190">Step 3: Set hello Recovery Services Vault context</span></span>

<span data-ttu-id="b7939-191">Ustaw kontekst magazynu hello uruchamiając hello poniżej polecenia.</span><span class="sxs-lookup"><span data-stu-id="b7939-191">Set hello vault context by running hello below command.</span></span>

       Set-AzureRmSiteRecoveryVaultSettings -ARSVault $vault

## <a name="step-4-install-hello-azure-site-recovery-provider"></a><span data-ttu-id="b7939-192">Krok 4: Instalowanie hello dostawcy usługi Azure Site Recovery</span><span class="sxs-lookup"><span data-stu-id="b7939-192">Step 4: Install hello Azure Site Recovery Provider</span></span>
1. <span data-ttu-id="b7939-193">Na maszynie VMM hello należy utworzyć katalog, uruchamiając następujące polecenie hello:</span><span class="sxs-lookup"><span data-stu-id="b7939-193">On hello VMM machine, create a directory by running hello following command:</span></span>

       New-Item c:\ASR -type directory
2. <span data-ttu-id="b7939-194">Wyodrębnij pliki hello przy użyciu dostawcy hello pobrane, uruchamiając następujące polecenie hello</span><span class="sxs-lookup"><span data-stu-id="b7939-194">Extract hello files using hello downloaded provider by running hello following command</span></span>

       pushd C:\ASR\
       .\AzureSiteRecoveryProvider.exe /x:. /q
3. <span data-ttu-id="b7939-195">Zainstaluj dostawcę hello przy użyciu hello następującego polecenia:</span><span class="sxs-lookup"><span data-stu-id="b7939-195">Install hello provider using hello following commands:</span></span>

       .\SetupDr.exe /i
       $installationRegPath = "hklm:\software\Microsoft\Microsoft System Center Virtual Machine Manager Server\DRAdapter"
       do
       {
         $isNotInstalled = $true;
         if(Test-Path $installationRegPath)
         {
           $isNotInstalled = $false;
         }
       }While($isNotInstalled)

   <span data-ttu-id="b7939-196">Poczekaj na powitania toofinish instalacji.</span><span class="sxs-lookup"><span data-stu-id="b7939-196">Wait for hello installation toofinish.</span></span>
4. <span data-ttu-id="b7939-197">Zarejestruj serwer hello w magazynie hello przy użyciu hello następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="b7939-197">Register hello server in hello vault using hello following command:</span></span>

       $BinPath = $env:SystemDrive+"\Program Files\Microsoft System Center 2012 R2\Virtual Machine Manager\bin"
       pushd $BinPath
       $encryptionFilePath = "C:\temp\".\DRConfigurator.exe /r /Credentials $VaultSettingFilePath /vmmfriendlyname $env:COMPUTERNAME /dataencryptionenabled $encryptionFilePath /startvmmservice

## <a name="step-5-create-an-azure-storage-account"></a><span data-ttu-id="b7939-198">Krok 5: Tworzenie konta magazynu platformy Azure</span><span class="sxs-lookup"><span data-stu-id="b7939-198">Step 5: Create an Azure storage account</span></span>

<span data-ttu-id="b7939-199">Jeśli nie masz konta magazynu platformy Azure, Utwórz konto włączono replikację geograficzną w hello tej samej lokalizacji geograficznej co hello magazynu, uruchamiając następujące polecenie hello:</span><span class="sxs-lookup"><span data-stu-id="b7939-199">If you don't have an Azure storage account, create a geo-replication enabled account in hello same geo as hello vault by running hello following command:</span></span>

        $StorageAccountName = "teststorageacc1"    #StorageAccountname
        $StorageAccountGeo  = "Southeast Asia"     
        $ResourceGroupName =  “myRG”             #ResourceGroupName
        $RecoveryStorageAccount = New-AzureRmStorageAccount -ResourceGroupName $ResourceGroupName -Name $StorageAccountName -Type “StandardGRS” -Location $StorageAccountGeo

<span data-ttu-id="b7939-200">Należy pamiętać, że konto magazynu hello musi być w tym samym regionie co usługa Azure Site Recovery hello hello i skojarzone z hello tej samej subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="b7939-200">Note that hello storage account must be in hello same region as hello Azure Site Recovery service, and be associated with hello same subscription.</span></span>

## <a name="step-6-install-hello-azure-recovery-services-agent"></a><span data-ttu-id="b7939-201">Krok 6: Hello instalacji agenta usług odzyskiwania Azure</span><span class="sxs-lookup"><span data-stu-id="b7939-201">Step 6: Install hello Azure Recovery Services Agent</span></span>
1. <span data-ttu-id="b7939-202">Pobierz agenta usług odzyskiwania Azure hello na [http://aka.ms/latestmarsagent](http://aka.ms/latestmarsagent) i zainstaluj go na każdym serwerze hosta funkcji Hyper-V znajdujące się w hello VMM możesz chmur mają tooprotect.</span><span class="sxs-lookup"><span data-stu-id="b7939-202">Download hello Azure Recovery Services agent at [http://aka.ms/latestmarsagent](http://aka.ms/latestmarsagent) and install it on each Hyper-V host server located in hello VMM clouds you want tooprotect.</span></span>
2. <span data-ttu-id="b7939-203">Uruchom następujące polecenie na wszystkich hostach VMM hello:</span><span class="sxs-lookup"><span data-stu-id="b7939-203">Run hello following command on all VMM hosts:</span></span>

       marsagentinstaller.exe /q /nu

## <a name="step-7-configure-cloud-protection-settings"></a><span data-ttu-id="b7939-204">Krok 7: Konfigurowanie chmury ustawienia ochrony</span><span class="sxs-lookup"><span data-stu-id="b7939-204">Step 7: Configure cloud protection settings</span></span>
1. <span data-ttu-id="b7939-205">Utwórz tooAzure zasady replikacji, uruchamiając następujące polecenie hello:</span><span class="sxs-lookup"><span data-stu-id="b7939-205">Create a replication policy tooAzure by running hello following command:</span></span>

        $ReplicationFrequencyInSeconds = "300";        #options are 30,300,900
        $PolicyName = “replicapolicy”
        $Recoverypoints = 6                    #specify hello number of recovery points

        $policryresult = New-AzureRmSiteRecoveryPolicy -Name $policyname -ReplicationProvider HyperVReplicaAzure -ReplicationFrequencyInSeconds $replicationfrequencyinseconds -RecoveryPoints $recoverypoints -ApplicationConsistentSnapshotFrequencyInHours 1 -RecoveryAzureStorageAccountId "/subscriptions/q1345667/resourceGroups/test/providers/Microsoft.Storage/storageAccounts/teststorageacc1"

1. <span data-ttu-id="b7939-206">Pobierz kontenera ochrony, uruchamiając następujące polecenia hello:</span><span class="sxs-lookup"><span data-stu-id="b7939-206">Get a protection container by running hello following commands:</span></span>

       $PrimaryCloud = "testcloud"
       $protectionContainer = Get-AzureRmSiteRecoveryProtectionContainer -friendlyName $PrimaryCloud;  
2. <span data-ttu-id="b7939-207">Pobierz hello zasad szczegóły tooa zmienną przy użyciu zadania hello, który został utworzony i podając hello zasad przyjazną nazwę:</span><span class="sxs-lookup"><span data-stu-id="b7939-207">Get hello policy details tooa variable using hello job that was created and mentioning hello friendly policy name:</span></span>

       $policy = Get-AzureRmSiteRecoveryPolicy -FriendlyName $policyname
3. <span data-ttu-id="b7939-208">Uruchom skojarzenie hello kontenera ochrony hello z zasadami replikacji hello:</span><span class="sxs-lookup"><span data-stu-id="b7939-208">Start hello association of hello protection container with hello replication policy:</span></span>

       $associationJob  = Start-AzureRmSiteRecoveryPolicyAssociationJob -Policy     $Policy -PrimaryProtectionContainer $protectionContainer  
4. <span data-ttu-id="b7939-209">Po zakończeniu zadania hello, uruchom następujące polecenie hello:</span><span class="sxs-lookup"><span data-stu-id="b7939-209">After hello job has finished, run hello following command:</span></span>

       $job = Get-AzureRmSiteRecoveryJob -Job $associationJob

       if($job -eq $null -or $job.StateDescription -ne "Completed")
       {
         $isJobLeftForProcessing = $true;
       }
5. <span data-ttu-id="b7939-210">Po zakończeniu przetwarzania zadania hello, uruchom następujące polecenie hello:</span><span class="sxs-lookup"><span data-stu-id="b7939-210">After hello job has finished processing, run hello following command:</span></span>

       if($isJobLeftForProcessing)
       {
         Start-Sleep -Seconds 60
       }
       }While($isJobLeftForProcessing)

<span data-ttu-id="b7939-211">toocheck hello ukończenia operacji hello, wykonaj kroki hello w [monitorowanie aktywności](#monitor).</span><span class="sxs-lookup"><span data-stu-id="b7939-211">toocheck hello completion of hello operation, follow hello steps in [Monitor Activity](#monitor).</span></span>

## <a name="step-8-configure-network-mapping"></a><span data-ttu-id="b7939-212">Krok 8: Konfigurowanie mapowania sieci</span><span class="sxs-lookup"><span data-stu-id="b7939-212">Step 8: Configure network mapping</span></span>
<span data-ttu-id="b7939-213">Przed rozpoczęciem mapowania sieci Sprawdź, czy maszyny wirtualne na źródłowym serwerze programu VMM hello są połączone tooa sieci maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="b7939-213">Before you begin network mapping verify that virtual machines on hello source VMM server are connected tooa VM network.</span></span> <span data-ttu-id="b7939-214">Ponadto należy utworzyć jeden lub więcej sieci wirtualnych platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="b7939-214">In addition, create one or more Azure virtual networks.</span></span>

<span data-ttu-id="b7939-215">Dowiedz się więcej na temat sposobu toocreate a wirtualnych sieci, za pomocą usługi Azure Resource Manager i programu PowerShell, w [tworzenie sieci wirtualnej za pomocą połączenia sieci VPN lokacja lokacja za pomocą usługi Azure Resource Manager i programu PowerShell](../vpn-gateway/vpn-gateway-create-site-to-site-rm-powershell.md)</span><span class="sxs-lookup"><span data-stu-id="b7939-215">Learn more about how toocreate a virtual network using Azure Resource Manager and PowerShell, in [Create a virtual network with a site-to-site VPN connection using Azure Resource Manager and PowerShell](../vpn-gateway/vpn-gateway-create-site-to-site-rm-powershell.md)</span></span>

<span data-ttu-id="b7939-216">Należy zauważyć, że wiele sieci maszyn wirtualnych mogą być mapowane tooa pojedynczej sieci platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="b7939-216">Note that multiple Virtual Machine networks can be mapped tooa single Azure network.</span></span> <span data-ttu-id="b7939-217">Jeśli hello Sieć docelowa ma wiele podsieci i jedna z tych podsieci ma hello znajduje się samą nazwę jak podsieć, w których hello źródłowej maszyny wirtualnej, a następnie hello repliki maszyny wirtualnej zostaną połączone toothat docelowej podsieci po awaryjnym.</span><span class="sxs-lookup"><span data-stu-id="b7939-217">If hello target network has multiple subnets and one of those subnets has hello same name as subnet on which hello source virtual machine is located, then hello replica virtual machine will be connected toothat target subnet after fail-over.</span></span> <span data-ttu-id="b7939-218">Jeśli nie ma żadnych docelowa podsieć o pasującej nazwie, maszyna wirtualna hello będzie toohello połączonych pierwszej podsieci w sieci hello.</span><span class="sxs-lookup"><span data-stu-id="b7939-218">If there is no target subnet with a matching name, hello virtual machine will be connected toohello first subnet in hello network.</span></span>

1. <span data-ttu-id="b7939-219">Witaj pierwsze polecenie pobiera serwerów hello bieżący magazyn Azure Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="b7939-219">hello first command gets servers for hello current Azure Site Recovery vault.</span></span> <span data-ttu-id="b7939-220">polecenie Hello przechowuje hello serwerów Microsoft Azure Site Recovery w hello $Servers tablicy zmiennej.</span><span class="sxs-lookup"><span data-stu-id="b7939-220">hello command stores hello Microsoft Azure Site Recovery servers in hello $Servers array variable.</span></span>

        $Servers = Get-AzureRmSiteRecoveryServer
2. <span data-ttu-id="b7939-221">Hello drugie polecenie pobiera hello sieci odzyskiwania lokacji dla pierwszego serwera hello hello $Servers tablicy.</span><span class="sxs-lookup"><span data-stu-id="b7939-221">hello second command gets hello site recovery network for hello first server in hello $Servers array.</span></span> <span data-ttu-id="b7939-222">polecenie Hello przechowuje hello sieci w zmiennej hello $Networks.</span><span class="sxs-lookup"><span data-stu-id="b7939-222">hello command stores hello networks in hello $Networks variable.</span></span>

        $Networks = Get-AzureRmSiteRecoveryNetwork -Server $Servers[0]

1. <span data-ttu-id="b7939-223">trzecie polecenie Hello pobiera sieci wirtualnych platformy Azure, a następnie tę wartość w zmiennej hello $AzureVmNetworks.</span><span class="sxs-lookup"><span data-stu-id="b7939-223">hello third command gets Azure virtual networks, and then that value in hello $AzureVmNetworks variable.</span></span>

        $AzureVmNetworks =  Get-AzureRmVirtualNetwork
2. <span data-ttu-id="b7939-224">polecenie cmdlet końcowego Hello tworzy mapowanie między hello sieci podstawowej i hello sieci maszyny wirtualnej platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="b7939-224">hello final cmdlet creates a mapping between hello primary network and hello Azure virtual machine network.</span></span> <span data-ttu-id="b7939-225">polecenia cmdlet Hello określa hello sieci podstawowej jako pierwszy element $Networks hello.</span><span class="sxs-lookup"><span data-stu-id="b7939-225">hello cmdlet specifies hello primary network as hello first element of $Networks.</span></span> <span data-ttu-id="b7939-226">polecenia cmdlet Hello określa sieć maszyny wirtualnej jako pierwszy element $AzureVmNetworks hello.</span><span class="sxs-lookup"><span data-stu-id="b7939-226">hello cmdlet specifies a virtual machine network as hello first element of $AzureVmNetworks.</span></span>

        New-AzureRmSiteRecoveryNetworkMapping -PrimaryNetwork $Networks[0] -AzureVMNetworkId $AzureVmNetworks[0]

## <a name="step-9-enable-protection-for-virtual-machines"></a><span data-ttu-id="b7939-227">Krok 9: Włączanie ochrony dla maszyn wirtualnych</span><span class="sxs-lookup"><span data-stu-id="b7939-227">Step 9: Enable protection for virtual machines</span></span>
<span data-ttu-id="b7939-228">Po hello serwerów, chmur i sieci są skonfigurowane poprawnie, można włączyć ochrony dla maszyn wirtualnych w chmurze hello.</span><span class="sxs-lookup"><span data-stu-id="b7939-228">After hello servers, clouds and networks are configured correctly, you can enable protection for virtual machines in hello cloud.</span></span>

 <span data-ttu-id="b7939-229">Należy uwzględnić następujące hello:</span><span class="sxs-lookup"><span data-stu-id="b7939-229">Note hello following:</span></span>

* <span data-ttu-id="b7939-230">Maszyny wirtualne muszą spełniać wymagania dotyczące usługi Azure.</span><span class="sxs-lookup"><span data-stu-id="b7939-230">Virtual machines must meet Azure requirements.</span></span> <span data-ttu-id="b7939-231">Sprawdź je w [warunki wstępne i pomocy technicznej](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements) w przewodniku planowania hello.</span><span class="sxs-lookup"><span data-stu-id="b7939-231">Check these in [Prerequisites and Support](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements) in hello planning guide.</span></span>
* <span data-ttu-id="b7939-232">dla maszyny wirtualnej hello musi być ustawiona ochrona tooenable, hello systemu operacyjnego i właściwości dysku systemu operacyjnego.</span><span class="sxs-lookup"><span data-stu-id="b7939-232">tooenable protection, hello operating system and operating system disk properties must be set for hello virtual machine.</span></span> <span data-ttu-id="b7939-233">Podczas tworzenia maszyny wirtualnej w programie VMM przy użyciu szablonu maszyny wirtualnej można ustawić właściwości hello.</span><span class="sxs-lookup"><span data-stu-id="b7939-233">When you create a virtual machine in VMM using a virtual machine template you can set hello property.</span></span> <span data-ttu-id="b7939-234">Można również ustawić te właściwości dla istniejących maszyn wirtualnych na powitania **ogólne** i **konfiguracja sprzętu** karty hello właściwości maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="b7939-234">You can also set these properties for existing virtual machines on hello **General** and **Hardware Configuration** tabs of hello virtual machine properties.</span></span> <span data-ttu-id="b7939-235">Jeśli nie ustawisz tych właściwości w programie VMM będziesz w stanie tooconfigure je w portalu usługi Azure Site Recovery hello.</span><span class="sxs-lookup"><span data-stu-id="b7939-235">If you don't set these properties in VMM you'll be able tooconfigure them in hello Azure Site Recovery portal.</span></span>

1. <span data-ttu-id="b7939-236">Ochrona tooenable hello uruchom następujące polecenia kontenera ochrony hello tooget:</span><span class="sxs-lookup"><span data-stu-id="b7939-236">tooenable protection, run hello following command tooget hello protection container:</span></span>

          $ProtectionContainer = Get-AzureRmSiteRecoveryProtectionContainer -friendlyName $CloudName
2. <span data-ttu-id="b7939-237">Pobierz jednostki ochrony hello (VM), uruchamiając następujące polecenie hello:</span><span class="sxs-lookup"><span data-stu-id="b7939-237">Get hello protection entity (VM) by running hello following command:</span></span>

           $protectionEntity = Get-AzureRmSiteRecoveryProtectionEntity -friendlyName $VMName -ProtectionContainer $protectionContainer
3. <span data-ttu-id="b7939-238">Włącz hello DR dla maszyny Wirtualnej hello, uruchamiając następujące polecenie hello:</span><span class="sxs-lookup"><span data-stu-id="b7939-238">Enable hello DR for hello VM by running hello following command:</span></span>

          $jobResult = Set-AzureRmSiteRecoveryProtectionEntity -ProtectionEntity $protectionentity -Protection Enable –Force -Policy $policy -RecoveryAzureStorageAccountId  $storageID "/subscriptions/217653172865hcvkchgvd/resourceGroups/rajanirgps/providers/Microsoft.Storage/storageAccounts/teststorageacc1

## <a name="test-your-deployment"></a><span data-ttu-id="b7939-239">Testowanie wdrożenia</span><span class="sxs-lookup"><span data-stu-id="b7939-239">Test your deployment</span></span>
<span data-ttu-id="b7939-240">tootest wdrożenia można uruchomić testu Failover dla jednej maszyny wirtualnej, lub utworzyć plan odzyskiwania uwzględniający wiele maszyn wirtualnych i uruchom test awaryjnej hello planu.</span><span class="sxs-lookup"><span data-stu-id="b7939-240">tootest your deployment you can run a test fail-over for a single virtual machine, or create a recovery plan consisting of multiple virtual machines and run a test fail-over for hello plan.</span></span> <span data-ttu-id="b7939-241">Awaryjnej testu symuluje z mechanizmu awaryjnej i odzyskiwania w sieci izolowanej.</span><span class="sxs-lookup"><span data-stu-id="b7939-241">Test fail-over simulates your fail-over and recovery mechanism in an isolated network.</span></span> <span data-ttu-id="b7939-242">Należy pamiętać, że:</span><span class="sxs-lookup"><span data-stu-id="b7939-242">Note that:</span></span>

* <span data-ttu-id="b7939-243">Tooconnect toohello maszyny wirtualnej platformy Azure przy użyciu pulpitu zdalnego po awaryjnym hello, należy włączyć połączenia pulpitu zdalnego na maszynie wirtualnej hello przed rozpoczęciem powitalne testowy tryb failover.</span><span class="sxs-lookup"><span data-stu-id="b7939-243">If you want tooconnect toohello virtual machine in Azure using Remote Desktop after hello fail-over, enable Remote Desktop Connection on hello virtual machine before you run hello test failover.</span></span>
* <span data-ttu-id="b7939-244">Po miała użyjesz publicznego adresu IP address tooconnect toohello maszynę wirtualną na platformie Azure przy użyciu pulpitu zdalnego.</span><span class="sxs-lookup"><span data-stu-id="b7939-244">After fail-over, you'll use a public IP address tooconnect toohello virtual machine in Azure using Remote Desktop.</span></span> <span data-ttu-id="b7939-245">Jeśli chcesz toodo to, upewnij się, że nie ma żadnych zasad domeny, które uniemożliwiają łączącego tooa maszyny wirtualnej przy użyciu adresu publicznego.</span><span class="sxs-lookup"><span data-stu-id="b7939-245">If you want toodo this, ensure you don't have any domain policies that prevent you from connecting tooa virtual machine using a public address.</span></span>

<span data-ttu-id="b7939-246">toocheck hello ukończenia operacji hello, wykonaj kroki hello w [monitorowanie aktywności](#monitor).</span><span class="sxs-lookup"><span data-stu-id="b7939-246">toocheck hello completion of hello operation, follow hello steps in [Monitor Activity](#monitor).</span></span>

### <a name="run-a-test-failover"></a><span data-ttu-id="b7939-247">Wykonywanie próby przejścia w tryb failover</span><span class="sxs-lookup"><span data-stu-id="b7939-247">Run a test failover</span></span>
- <span data-ttu-id="b7939-248">Uruchom hello testowy tryb failover, uruchamiając następujące polecenie hello:</span><span class="sxs-lookup"><span data-stu-id="b7939-248">Start hello test failover by running hello following command:</span></span>

       $protectionEntity = Get-AzureRmSiteRecoveryProtectionEntity -Name $VMName -ProtectionContainer $protectionContainer

       $jobIDResult =  Start-AzureRmSiteRecoveryTestFailoverJob -Direction PrimaryToRecovery -ProtectionEntity $protectionEntity -AzureVMNetworkId <string>  

### <a name="run-a-planned-failover"></a><span data-ttu-id="b7939-249">Realizacja planowanego trybu failover</span><span class="sxs-lookup"><span data-stu-id="b7939-249">Run a planned failover</span></span>
- <span data-ttu-id="b7939-250">Uruchom hello planowanego trybu failover, uruchamiając następujące polecenie hello:</span><span class="sxs-lookup"><span data-stu-id="b7939-250">Start hello planned failover by running hello following command:</span></span>

        $protectionEntity = Get-AzureRmSiteRecoveryProtectionEntity -Name $VMName -ProtectionContainer $protectionContainer

        $jobIDResult =  Start-AzureRmSiteRecoveryPlannedFailoverJob -Direction PrimaryToRecovery -ProtectionEntity $protectionEntity -AzureVMNetworkId <string>  

### <a name="run-an-unplanned-failover"></a><span data-ttu-id="b7939-251">Uruchom nieplanowanego trybu failover</span><span class="sxs-lookup"><span data-stu-id="b7939-251">Run an unplanned failover</span></span>
- <span data-ttu-id="b7939-252">Uruchom hello nieplanowanego trybu failover, uruchamiając następujące polecenie hello:</span><span class="sxs-lookup"><span data-stu-id="b7939-252">Start hello unplanned failover by running hello following command:</span></span>

        $protectionEntity = Get-AzureRmSiteRecoveryProtectionEntity -Name $VMName -ProtectionContainer $protectionContainer

        $jobIDResult =  Start-AzureRmSiteRecoveryUnPlannedFailoverJob -Direction PrimaryToRecovery -ProtectionEntity $protectionEntity -AzureVMNetworkId <string>  

## <span data-ttu-id="b7939-253"><a name=monitor></a>Monitorowanie aktywności</span><span class="sxs-lookup"><span data-stu-id="b7939-253"><a name=monitor></a> Monitor Activity</span></span>
<span data-ttu-id="b7939-254">Witaj Użyj następującego polecenia toomonitor hello działania.</span><span class="sxs-lookup"><span data-stu-id="b7939-254">Use hello following commands toomonitor hello activity.</span></span> <span data-ttu-id="b7939-255">Należy pamiętać, że masz toowait Between zadania hello toofinish przetwarzania.</span><span class="sxs-lookup"><span data-stu-id="b7939-255">Note that you have toowait in between jobs for hello processing toofinish.</span></span>

    Do
    {
        $job = Get-AzureSiteRecoveryJob -Id $associationJob.JobId;
        Write-Host "Job State:{0}, StateDescription:{1}" -f Job.State, $job.StateDescription;
        if($job -eq $null -or $job.StateDescription -ne "Completed")
        {
            $isJobLeftForProcessing = $true;
        }

    if($isJobLeftForProcessing)
        {
            Start-Sleep -Seconds 60
        }
    }While($isJobLeftForProcessing)



## <a name="next-steps"></a><span data-ttu-id="b7939-256">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="b7939-256">Next steps</span></span>
<span data-ttu-id="b7939-257">[Dowiedz się więcej](/powershell/module/azurerm.recoveryservices.backup/#recovery) dotyczące usługi Azure Site Recovery za pomocą poleceń cmdlet programu PowerShell usługi Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="b7939-257">[Read more](/powershell/module/azurerm.recoveryservices.backup/#recovery) about Azure Site Recovery with Azure Resource Manager PowerShell cmdlets.</span></span>
