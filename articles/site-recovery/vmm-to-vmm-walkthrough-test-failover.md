---
title: "aaaRun test trybu failover dla lokacji dodatkowej tooa replikacji maszyny Wirtualnej funkcji Hyper-V z usługą Azure Site Recovery | Dokumentacja firmy Microsoft"
description: "W tym artykule opisano, jak toorun test trybu failover dla maszyny Wirtualnej funkcji Hyper-V tooa replikacji, lokacji dodatkowej programu System Center VMM, z usługą Azure Site Recovery."
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: a3fd11ce-65a1-4308-8435-45cf954353ef
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/30/2017
ms.author: raynew
ms.openlocfilehash: a60411541c2db001c573735bcb0d651f6618f295
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="step-10-run-a-test-failover-for-hyper-v-replication-tooa-secondary-site"></a><span data-ttu-id="925f4-103">Krok 10: Uruchom test trybu failover dla lokacji dodatkowej tooa replikacji funkcji Hyper-V</span><span class="sxs-lookup"><span data-stu-id="925f4-103">Step 10: Run a test failover for Hyper-V replication tooa secondary site</span></span>


<span data-ttu-id="925f4-104">Po włączeniu replikacji maszyn wirtualnych funkcji Hyper-V (maszyn wirtualnych) z [usługi Azure Site Recovery](site-recovery-overview.md), użyj tego artykułu toorun test trybu failover.</span><span class="sxs-lookup"><span data-stu-id="925f4-104">After you enable replication for Hyper-V virtual machines (VMs) with [Azure Site Recovery](site-recovery-overview.md), use this article toorun a test failover.</span></span> <span data-ttu-id="925f4-105">Test trybu failover sprawdza, czy działa replikacja bez wpływu na środowisko produkcyjne.</span><span class="sxs-lookup"><span data-stu-id="925f4-105">A test failover verifies that replication is working, without impacting your production environment.</span></span> 


<span data-ttu-id="925f4-106">Po przeczytaniu tego artykułu, post wszelkie komentarze u dołu hello, lub na powitania [Forum usług odzyskiwania Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="925f4-106">After reading this article, post any comments at hello bottom, or on hello [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>


## <a name="before-you-start"></a><span data-ttu-id="925f4-107">Przed rozpoczęciem</span><span class="sxs-lookup"><span data-stu-id="925f4-107">Before you start</span></span>

- <span data-ttu-id="925f4-108">Podczas jest wyzwalają test trybu failover, można określić hello sieci toowhich hello testu replikę, którą nawiążą połączenie maszyny wirtualne.</span><span class="sxs-lookup"><span data-stu-id="925f4-108">When you're triggering a test failover, you can specify hello network toowhich hello test replica VMs will connect.</span></span> <span data-ttu-id="925f4-109">[Dowiedz się więcej](site-recovery-test-failover-vmm-to-vmm.md#network-options-in-site-recovery) o opcjach sieci hello.</span><span class="sxs-lookup"><span data-stu-id="925f4-109">[Learn more](site-recovery-test-failover-vmm-to-vmm.md#network-options-in-site-recovery) about hello network options.</span></span>
- <span data-ttu-id="925f4-110">Zaleca się, że nie wybrano sieci z wybranym podczas mapowania sieci.</span><span class="sxs-lookup"><span data-stu-id="925f4-110">We recommend that you don't choose a network that you selected during network mapping.</span></span>
- <span data-ttu-id="925f4-111">Witaj instrukcje w tym artykule opisano sposób toofail za pośrednictwem jednej maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="925f4-111">hello instructions in this article describe how toofail over a single VM.</span></span> <span data-ttu-id="925f4-112">Przeczytaj informacje o [Tworzenie planów odzyskiwania](site-recovery-create-recovery-plans.md) Jeśli chcesz toofail przez wiele maszyn wirtualnych jednocześnie.</span><span class="sxs-lookup"><span data-stu-id="925f4-112">Read about [creating recovery plans](site-recovery-create-recovery-plans.md) if you want toofail over multiple VMs together.</span></span>
- <span data-ttu-id="925f4-113">Przeczytaj informacje o [ograniczenia dotyczące testowy tryb failover](site-recovery-test-failover-vmm-to-vmm.md#things-to-note).</span><span class="sxs-lookup"><span data-stu-id="925f4-113">Read about [limitations for test failovers](site-recovery-test-failover-vmm-to-vmm.md#things-to-note).</span></span>
- <span data-ttu-id="925f4-114">Witaj adres IP podany tooa maszyny Wirtualnej podczas testowania trybu failover jest hello otrzyma tego samego adresu IP, który hello maszyny Wirtualnej dla planowanego lub nieplanowanego trybu failover (przy założeniu, że adres IP hello jest dostępny w testowej sieci trybu failover hello).</span><span class="sxs-lookup"><span data-stu-id="925f4-114">hello IP address given tooa VM during test failover is hello same IP address that hello VM would receive for a planned or unplanned failover (presuming that hello IP address is available in hello test failover network).</span></span> <span data-ttu-id="925f4-115">Jeśli adres IP hello jest niedostępna w testowej sieci trybu failover hello, hello maszyna wirtualna odbiera innego adresu IP, który jest dostępny w testowej sieci trybu failover hello.</span><span class="sxs-lookup"><span data-stu-id="925f4-115">If hello IP address isn't available in hello test failover network, hello VM receives another IP address that is available in hello test failover network.</span></span>
- <span data-ttu-id="925f4-116">Jeśli chcesz toodo test trybu failover w sieci produkcyjnej dla pełnej niepoprawny maszyny łączności sieciowej na całej trasie, należy pamiętać, że:</span><span class="sxs-lookup"><span data-stu-id="925f4-116">If you do want toodo a test failover in your production network, for full validatation of end-to-end network connectivity machine, note that:</span></span>
    - <span data-ttu-id="925f4-117">powitalne podstawowej maszyny Wirtualnej należy zamknąć podczas prowadzenia hello testowy tryb failover.</span><span class="sxs-lookup"><span data-stu-id="925f4-117">hello primary VM should be shut down when you're doing hello test failover.</span></span> <span data-ttu-id="925f4-118">W przeciwnym razie dwóch maszyn wirtualnych o tej samej tożsamości będzie uruchomiony w hello hello sam sieci na powitania tym samym czasie.</span><span class="sxs-lookup"><span data-stu-id="925f4-118">Otherwise, two VMs with hello same identity will be running in hello same network at hello same time.</span></span> 
    - <span data-ttu-id="925f4-119">Jeśli wprowadzisz zmiany tootest maszyn wirtualnych, te zmiany zostaną utracone podczas oczyszczania hello testowania trybu failover.</span><span class="sxs-lookup"><span data-stu-id="925f4-119">If you make changes tootest VMs, those changes are lost when you clean up hello test failover.</span></span> <span data-ttu-id="925f4-120">Te zmiany nie są replikowane toohello wstecz podstawowej maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="925f4-120">These changes aren't replicated back toohello primary VM.</span></span>
    - <span data-ttu-id="925f4-121">Testowanie sieci produkcyjnej prowadzi toodowntime dla obciążeń produkcyjnych.</span><span class="sxs-lookup"><span data-stu-id="925f4-121">Testing a a production network leads toodowntime for your production workloads.</span></span> <span data-ttu-id="925f4-122">Poproś użytkowników nie toouse aplikacji hello gdy wyszczególniania odzyskiwania po awarii hello jest w toku.</span><span class="sxs-lookup"><span data-stu-id="925f4-122">Ask users not toouse hello app when hello disaster recovery drill is in progress.</span></span>  


## <a name="run-a-test-failover-for-a-vm"></a><span data-ttu-id="925f4-123">Uruchom test trybu failover dla maszyny Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="925f4-123">Run a test failover for a VM</span></span>

1. <span data-ttu-id="925f4-124">toofail za pośrednictwem jednej maszyny Wirtualnej w **elementy replikowane**, kliknij przycisk hello maszyny Wirtualnej > **testowy tryb Failover**.</span><span class="sxs-lookup"><span data-stu-id="925f4-124">toofail over a single VM, in **Replicated Items**, click hello VM > **Test Failover**.</span></span>
2. <span data-ttu-id="925f4-125">W **testowego trybu Failover**, określ, jak testu maszyn wirtualnych zostaną połączone toonetworks po hello testowy tryb failover.</span><span class="sxs-lookup"><span data-stu-id="925f4-125">In **Test Failover**, specify how test VMs will be connected toonetworks after hello test failover.</span></span> 
3. <span data-ttu-id="925f4-126">Kliknij przycisk **OK** toobegin hello w tryb failover.</span><span class="sxs-lookup"><span data-stu-id="925f4-126">Click **OK** toobegin hello failover.</span></span> <span data-ttu-id="925f4-127">Śledzenie postępów hello **zadania** kartę.</span><span class="sxs-lookup"><span data-stu-id="925f4-127">Track progress on hello **Jobs** tab.</span></span>
5. <span data-ttu-id="925f4-128">Po zakończeniu trybu failover Sprawdź pomyślnie test hello uruchamiania maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="925f4-128">After failover is complete, verify that hello test VMs start successfully.</span></span>
6. <span data-ttu-id="925f4-129">Gdy wszystko będzie gotowe, kliknij przycisk **oczyszczania testowy tryb failover** na powitania planu odzyskiwania.</span><span class="sxs-lookup"><span data-stu-id="925f4-129">When you're done, click **Cleanup test failover** on hello recovery plan.</span></span>
7. <span data-ttu-id="925f4-130">W **uwagi**, zarejestrować i zapisać wszelkie obserwacje związane z hello testowy tryb failover.</span><span class="sxs-lookup"><span data-stu-id="925f4-130">In **Notes**, record and save any observations associated with hello test failover.</span></span> <span data-ttu-id="925f4-131">Ten krok polega na usunięciu hello maszyn wirtualnych i sieci, które zostały utworzone podczas testowania trybu failover.</span><span class="sxs-lookup"><span data-stu-id="925f4-131">This step deletes hello virtual machines and networks that were created during test failover.</span></span>


## <a name="next-steps"></a><span data-ttu-id="925f4-132">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="925f4-132">Next steps</span></span>

<span data-ttu-id="925f4-133">Po przetestowaniu wdrożenia hello więcej informacji na temat innych typów [pracy awaryjnej](site-recovery-failover.md).</span><span class="sxs-lookup"><span data-stu-id="925f4-133">After you've tested hello deployment, learn more about other types of [failover](site-recovery-failover.md).</span></span>
