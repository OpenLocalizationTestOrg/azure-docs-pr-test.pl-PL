---
title: "Architektura hello aaaReview dla lokacji dodatkowej tooa replikacji funkcji Hyper-V z usługą Azure Site Recovery | Dokumentacja firmy Microsoft"
description: "Ten artykuł zawiera omówienie architektury hello replikowania lokalnych maszyn wirtualnych funkcji Hyper-V tooa programu System Center VMM lokacja dodatkowa z usługi Azure Site Recovery."
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: 07099161-4cc7-4f32-8eb9-2a71bbf0750b
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/30/2017
ms.author: raynew
ms.openlocfilehash: 0de4b4e8601116c73e6fd710597ce4e561884368
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="step-1-review-hello-architecture-for-hyper-v-replication-tooa-secondary-site"></a><span data-ttu-id="770e5-103">Krok 1: Przegląd architektury powitania dla lokacji dodatkowej tooa replikacji funkcji Hyper-V</span><span class="sxs-lookup"><span data-stu-id="770e5-103">Step 1: Review hello architecture for Hyper-V replication tooa secondary site</span></span>

<span data-ttu-id="770e5-104">W tym artykule opisano składniki hello i procesów podczas replikowania lokalnych maszyn wirtualnych (VM) funkcji Hyper-V w chmurach programu System Center Virtual Machine Manager (VMM), tooa lokacja dodatkowa programu VMM przy użyciu hello [usługi Azure Site Recovery](site-recovery-overview.md)w hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="770e5-104">This article describes hello components and processes involved when replicating on-premises Hyper-V virtual machines (VMs) in System Center Virtual Machine Manager (VMM) clouds, tooa secondary VMM site using hello [Azure Site Recovery](site-recovery-overview.md) service in hello Azure portal.</span></span>

<span data-ttu-id="770e5-105">Opublikuj wszelkie komentarze u dołu hello tego artykułu lub hello [Forum usług odzyskiwania Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="770e5-105">Post any comments at hello bottom of this article, or in hello [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>



## <a name="architectural-components"></a><span data-ttu-id="770e5-106">Składniki architektury</span><span class="sxs-lookup"><span data-stu-id="770e5-106">Architectural components</span></span>

<span data-ttu-id="770e5-107">Oto, co jest potrzebne do replikowania maszyn wirtualnych funkcji Hyper-V tooa dodatkowej lokacji programu VMM.</span><span class="sxs-lookup"><span data-stu-id="770e5-107">Here's what you need for replicating Hyper-V VMs tooa secondary VMM site.</span></span>

<span data-ttu-id="770e5-108">**Składnik**</span><span class="sxs-lookup"><span data-stu-id="770e5-108">**Component**</span></span> | <span data-ttu-id="770e5-109">**Lokalizacja**</span><span class="sxs-lookup"><span data-stu-id="770e5-109">**Location**</span></span> | <span data-ttu-id="770e5-110">**Szczegóły**</span><span class="sxs-lookup"><span data-stu-id="770e5-110">**Details**</span></span>
--- | --- | ---
<span data-ttu-id="770e5-111">**Azure**</span><span class="sxs-lookup"><span data-stu-id="770e5-111">**Azure**</span></span> | <span data-ttu-id="770e5-112">Subskrypcja na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="770e5-112">Subscription in Azure.</span></span> | <span data-ttu-id="770e5-113">Tworzenie magazynu usług odzyskiwania w hello subskrypcji platformy Azure, tooorchestrate i zarządzanie usługą replikacji między lokacjami programu VMM.</span><span class="sxs-lookup"><span data-stu-id="770e5-113">You create a Recovery Services vault in hello Azure subscription, tooorchestrate and manage replication between VMM locations.</span></span>
<span data-ttu-id="770e5-114">**Serwer VMM**</span><span class="sxs-lookup"><span data-stu-id="770e5-114">**VMM server**</span></span> | <span data-ttu-id="770e5-115">Potrzebujesz podstawowej i dodatkowej lokalizacji z programem VMM.</span><span class="sxs-lookup"><span data-stu-id="770e5-115">You need a VMM primary and secondary location.</span></span> | <span data-ttu-id="770e5-116">Zalecamy, aby serwer VMM w lokacji głównej hello i jeden w lokacji dodatkowej hello</span><span class="sxs-lookup"><span data-stu-id="770e5-116">We recommend a VMM server in hello primary site, and one in hello secondary site</span></span> 
<span data-ttu-id="770e5-117">**Serwer funkcji Hyper-V**</span><span class="sxs-lookup"><span data-stu-id="770e5-117">**Hyper-V server**</span></span> |  <span data-ttu-id="770e5-118">Jeden lub więcej funkcji Hyper-V serwerami hosta w hello głównych i dodatkowych chmurach VMM.</span><span class="sxs-lookup"><span data-stu-id="770e5-118">One or more Hyper-V host servers in hello primary and secondary VMM clouds.</span></span> | <span data-ttu-id="770e5-119">Dane są replikowane między hello podstawowych i pomocniczych serwerów Hyper-V hosta za pośrednictwem sieci LAN hello lub sieci VPN, korzystających z uwierzytelniania Kerberos lub certyfikatów.</span><span class="sxs-lookup"><span data-stu-id="770e5-119">Data is replicated between hello primary and secondary Hyper-V host servers over hello LAN or VPN, using Kerberos or certificate authentication.</span></span>  
<span data-ttu-id="770e5-120">**Maszyny wirtualne funkcji Hyper-V**</span><span class="sxs-lookup"><span data-stu-id="770e5-120">**Hyper-V VMs**</span></span> | <span data-ttu-id="770e5-121">Na serwerze hosta funkcji Hyper-V.</span><span class="sxs-lookup"><span data-stu-id="770e5-121">On Hyper-V host server.</span></span> | <span data-ttu-id="770e5-122">serwer hosta źródłowego Hello powinien mieć co najmniej jedną maszynę Wirtualną, które mają tooreplicate.</span><span class="sxs-lookup"><span data-stu-id="770e5-122">hello source host server should have at least one VM that you want tooreplicate.</span></span>

## <a name="replication-process"></a><span data-ttu-id="770e5-123">Proces replikacji</span><span class="sxs-lookup"><span data-stu-id="770e5-123">Replication process</span></span>

1. <span data-ttu-id="770e5-124">Konfigurowanie hello konto platformy Azure, utworzyć magazyn usług odzyskiwania i określ sposób tooreplicate.</span><span class="sxs-lookup"><span data-stu-id="770e5-124">You set up hello Azure account, create a Recovery Services vault, and specify what you want tooreplicate.</span></span>
2. <span data-ttu-id="770e5-125">Możesz skonfigurować hello źródłowa i docelowa ustawienia replikacji, takich jak instalowanie hello dostawcy usługi Azure Site Recovery na serwerach VMM oraz agenta usług odzyskiwania Microsoft Azure hello na każdym hoście funkcji Hyper-V.</span><span class="sxs-lookup"><span data-stu-id="770e5-125">You configure hello source and target replication settings, which includes installing hello Azure Site Recovery Provider on VMM servers, and hello Microsoft Azure Recovery Services agent on each Hyper-V host.</span></span>
3. <span data-ttu-id="770e5-126">Możesz utworzyć zasady replikacji dla źródła hello chmury VMM.</span><span class="sxs-lookup"><span data-stu-id="770e5-126">You create a replication policy for hello source VMM cloud.</span></span> <span data-ttu-id="770e5-127">Hello zasady są stosowane tooall maszyn wirtualnych znajdujących się na hostach w chmurze hello.</span><span class="sxs-lookup"><span data-stu-id="770e5-127">hello policy is applied tooall VMs located on hosts in hello cloud.</span></span>
4. <span data-ttu-id="770e5-128">Możesz włączyć replikację dla każdego programu VMM i następuje Replikacja początkowa maszyny wirtualnej zgodnie z ustawieniami hello, którą wybierzesz.</span><span class="sxs-lookup"><span data-stu-id="770e5-128">You enable replication for each VMM, and initial replication of a VM occurs in accordance with hello settings you choose.</span></span>
5. <span data-ttu-id="770e5-129">Po replikacji początkowej rozpocznie się replikacja zmian różnicowych.</span><span class="sxs-lookup"><span data-stu-id="770e5-129">After initial replication, replication of delta changes begins.</span></span> <span data-ttu-id="770e5-130">Śledzone zmiany elementu są przechowywane w pliku hrl.</span><span class="sxs-lookup"><span data-stu-id="770e5-130">Tracked changes for an item are held in a .hrl file.</span></span>


![Lokalne tooon lokalnej](./media/vmm-to-vmm-walkthrough-architecture/arch-onprem-onprem.png)

## <a name="failover-and-failback-process"></a><span data-ttu-id="770e5-132">Proces pracy w trybie failover i podczas powrotu po awarii</span><span class="sxs-lookup"><span data-stu-id="770e5-132">Failover and failback process</span></span>

1. <span data-ttu-id="770e5-133">Planowane lub nieplanowane przejście w tryb [failover](site-recovery-failover.md) można uruchomić między lokacjami lokalnymi.</span><span class="sxs-lookup"><span data-stu-id="770e5-133">You can run a planned or unplanned [failover](site-recovery-failover.md) between on-premises sites.</span></span> <span data-ttu-id="770e5-134">Jeśli realizacja planowanego trybu failover, a następnie źródłowe maszyny wirtualne są zamknięte tooensure bez utraty danych.</span><span class="sxs-lookup"><span data-stu-id="770e5-134">If you run a planned failover, then source VMs are shut down tooensure no data loss.</span></span>
2. <span data-ttu-id="770e5-135">Można przełączyć jednego komputera lub utworzyć [planów odzyskiwania](site-recovery-create-recovery-plans.md) tooorchestrate pracy w trybie failover wiele maszyn.</span><span class="sxs-lookup"><span data-stu-id="770e5-135">You can fail over a single machine, or create [recovery plans](site-recovery-create-recovery-plans.md) tooorchestrate failover of multiple machines.</span></span>
4. <span data-ttu-id="770e5-136">Jeśli nieplanowany tryb failover tooa lokacji dodatkowej, należy wykonać po hello trybu failover maszyny w lokalizacji dodatkowej hello nie są włączone dla ochrony lub replikacji.</span><span class="sxs-lookup"><span data-stu-id="770e5-136">If you perform an unplanned failover tooa secondary site, after hello failover machines in hello secondary location aren't enabled for protection or replication.</span></span> <span data-ttu-id="770e5-137">Po przeprowadzeniu planowany tryb failover po hello w tryb failover maszyny w lokalizacji dodatkowej hello są chronione.</span><span class="sxs-lookup"><span data-stu-id="770e5-137">If you ran a planned failover, after hello failover, machines in hello secondary location are protected.</span></span>
5. <span data-ttu-id="770e5-138">Następnie Zatwierdź hello trybu failover toostart podczas uzyskiwania dostępu do hello obciążenia z hello repliki maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="770e5-138">Then, you commit hello failover toostart accessing hello workload from hello replica VM.</span></span>
6. <span data-ttu-id="770e5-139">Gdy lokacji głównej jest ponownie dostępny, zainicjowaniu tooreplicate replikacji odwrotnej z toohello lokacji dodatkowej hello podstawowego.</span><span class="sxs-lookup"><span data-stu-id="770e5-139">When your primary site is available again, you initiate reverse replication tooreplicate from hello secondary site toohello primary.</span></span> <span data-ttu-id="770e5-140">Replikacji odwrotnej przełącza hello maszyny wirtualne w stanie chronionym hello dodatkowego centrum danych jest jednak nadal hello lokalizacji usługi active.</span><span class="sxs-lookup"><span data-stu-id="770e5-140">Reverse replication brings hello virtual machines into a protected state, but hello secondary datacenter is still hello active location.</span></span>
7. <span data-ttu-id="770e5-141">toomake hello lokacji głównej do lokalizacji usługi active hello ponownie inicjuje planowanego trybu failover z tooprimary dodatkowej, następuje innego replikacji odwrotnej.</span><span class="sxs-lookup"><span data-stu-id="770e5-141">toomake hello primary site into hello active location again, you initiate a planned failover from secondary tooprimary, followed by another reverse replication.</span></span>



## <a name="next-steps"></a><span data-ttu-id="770e5-142">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="770e5-142">Next steps</span></span>

<span data-ttu-id="770e5-143">Przejdź za[krok 2: Przejrzyj hello wymagania wstępne i ograniczenia](vmm-to-vmm-walkthrough-prerequisites.md).</span><span class="sxs-lookup"><span data-stu-id="770e5-143">Go too[Step 2: Review hello prerequisites and limitations](vmm-to-vmm-walkthrough-prerequisites.md).</span></span>
