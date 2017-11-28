---
title: "lokacja dodatkowa tooa replikacji aaaEnable funkcji Hyper-V z usługi Azure Site Recovery | Dokumentacja firmy Microsoft"
description: "W tym artykule opisano, jak tooenable replikację dla maszyn wirtualnych funkcji Hyper-V, replikacja tooa, lokacji dodatkowej programu System Center VMM, z usługą Azure Site Recovery."
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: d8782d14-9fef-4396-8912-ff945efc851b
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/30/2017
ms.author: raynew
ms.openlocfilehash: b4484e0118cb23f343187fe867d9795d30926baf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="step-9-enable-replication-tooa-secondary-site-for-hyper-v-vms"></a><span data-ttu-id="549a2-103">Krok 9: Włącz lokacji dodatkowej tooa replikację dla maszyn wirtualnych funkcji Hyper-V</span><span class="sxs-lookup"><span data-stu-id="549a2-103">Step 9: Enable replication tooa secondary site for Hyper-V VMs</span></span>


<span data-ttu-id="549a2-104">Po skonfigurowaniu zasad replikacji, należy używać lokacji programu System Center Virtual Machine Manager (VMM) dodatkowej tooa tego artykułu tooenable replikacji lokalnym funkcji Hyper-V maszyn wirtualnych (VM), za pomocą [usługi Azure Site Recovery](site-recovery-overview.md).</span><span class="sxs-lookup"><span data-stu-id="549a2-104">After setting up a replication policy, use this article tooenable replication tooa secondary System Center Virtual Machine Manager (VMM) site for on-premises Hyper-V virtual machines (VM), using [Azure Site Recovery](site-recovery-overview.md).</span></span>

<span data-ttu-id="549a2-105">Po przeczytaniu tego artykułu, post wszelkie komentarze u dołu hello, lub na powitania [Forum usług odzyskiwania Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="549a2-105">After reading this article, post any comments at hello bottom, or on hello [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>



## <a name="select-vms-tooreplicate"></a><span data-ttu-id="549a2-106">Wybierz tooreplicate maszyny wirtualne</span><span class="sxs-lookup"><span data-stu-id="549a2-106">Select VMs tooreplicate</span></span>

1. <span data-ttu-id="549a2-107">Kliknij kolejno pozycje **Krok 2. Replikowanie aplikacji** > **Źródło**.</span><span class="sxs-lookup"><span data-stu-id="549a2-107">Click **Step 2: Replicate application** > **Source**.</span></span> 

    ![Włączanie replikacji](./media/vmm-to-vmm-walkthrough-enable-replication/enable-replication1.png)

2. <span data-ttu-id="549a2-109">W **źródła**, wybierz serwer VMM hello i hello chmury, w których hello znajdują się hosty funkcji Hyper-V ma tooreplicate.</span><span class="sxs-lookup"><span data-stu-id="549a2-109">In **Source**, select hello VMM server, and hello cloud in which hello Hyper-V hosts you want tooreplicate are located.</span></span> <span data-ttu-id="549a2-110">Następnie kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="549a2-110">Then click **OK**.</span></span>

    ![Włączanie replikacji](./media/vmm-to-vmm-walkthrough-enable-replication/enable-replication2.png)
3. <span data-ttu-id="549a2-112">W **docelowego**, sprawdź hello pomocniczy serwer programu VMM i w chmurze.</span><span class="sxs-lookup"><span data-stu-id="549a2-112">In **Target**, verify hello secondary VMM server and cloud.</span></span>
4. <span data-ttu-id="549a2-113">W **maszyn wirtualnych**, wybierz hello maszyny wirtualne mają tooprotect z listy hello.</span><span class="sxs-lookup"><span data-stu-id="549a2-113">In **Virtual machines**, select hello VMs you want tooprotect from hello list.</span></span>

    ![Włączanie ochrony maszyny wirtualnej](./media/vmm-to-vmm-walkthrough-enable-replication/enable-replication5.png)

<span data-ttu-id="549a2-115">Możesz śledzić postępy hello **Włącz ochronę** akcji w **zadania** > **zadania usługi Site Recovery**.</span><span class="sxs-lookup"><span data-stu-id="549a2-115">You can track progress of hello **Enable Protection** action in **Jobs** > **Site Recovery jobs**.</span></span> <span data-ttu-id="549a2-116">Po hello **zakończenia ochrony** zadanie zostało ukończone, hello początkowej replikacji i maszyny wirtualnej hello jest gotowy do trybu failover.</span><span class="sxs-lookup"><span data-stu-id="549a2-116">After hello **Finalize Protection** job completes, hello initial replication is complete, and hello virtual machine is ready for failover.</span></span>

<span data-ttu-id="549a2-117">Należy pamiętać, że:</span><span class="sxs-lookup"><span data-stu-id="549a2-117">Note that:</span></span>

- <span data-ttu-id="549a2-118">Można również włączyć ochronę maszyn wirtualnych w konsoli programu VMM hello.</span><span class="sxs-lookup"><span data-stu-id="549a2-118">You can also enable protection for virtual machines in hello VMM console.</span></span> <span data-ttu-id="549a2-119">Kliknij przycisk **Włącz ochronę** na pasku narzędzi hello we właściwościach maszyny wirtualnej hello > **usługi Azure Site Recovery** kartę.</span><span class="sxs-lookup"><span data-stu-id="549a2-119">Click **Enable Protection** on hello toolbar in hello virtual machine properties > **Azure Site Recovery** tab.</span></span>
- <span data-ttu-id="549a2-120">Po włączeniu replikacji można wyświetlić właściwości hello maszyny Wirtualnej w **elementy replikowane**.</span><span class="sxs-lookup"><span data-stu-id="549a2-120">After you've enabled replication, you can view properties for hello VM in **Replicated Items**.</span></span> <span data-ttu-id="549a2-121">Na powitania **Essentials** pulpitu nawigacyjnego, wyświetlane są informacje dotyczące zasad replikacji hello hello maszyny Wirtualnej i jej stan.</span><span class="sxs-lookup"><span data-stu-id="549a2-121">On hello **Essentials** dashboard, you can see information about hello replication policy for hello VM and its status.</span></span> <span data-ttu-id="549a2-122">Kliknij przycisk **właściwości** więcej szczegółów.</span><span class="sxs-lookup"><span data-stu-id="549a2-122">Click **Properties** for more details.</span></span>

## <a name="onboard-existing-vms"></a><span data-ttu-id="549a2-123">Dodaj istniejące maszyny wirtualne</span><span class="sxs-lookup"><span data-stu-id="549a2-123">Onboard existing VMs</span></span>

<span data-ttu-id="549a2-124">Jeśli masz istniejące maszyny wirtualne w programie VMM, które są replikowane z funkcji Hyper-V Replica, możesz dołączyć je do replikacji usługi Azure Site Recovery w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="549a2-124">If you have existing virtual machines in VMM that are replicating with Hyper-V Replica, you can onboard them for Azure Site Recovery replication as follows:</span></span>

1. <span data-ttu-id="549a2-125">Upewnij się, że serwer hello funkcji Hyper-V hosting hello istniejącej maszyny Wirtualnej znajduje się w chmurze podstawowej hello oraz tego serwera funkcji Hyper-V hello obsługującego maszyny wirtualnej repliki hello znajduje się w chmurze dodatkowej hello.</span><span class="sxs-lookup"><span data-stu-id="549a2-125">Ensure that hello Hyper-V server hosting hello existing VM is located in hello primary cloud, and that hello Hyper-V server hosting hello replica virtual machine is located in hello secondary cloud.</span></span>
2. <span data-ttu-id="549a2-126">Upewnij się, że skonfigurowano zasady replikacji dla chmury VMM podstawowej hello.</span><span class="sxs-lookup"><span data-stu-id="549a2-126">Make sure a replication policy is configured for hello primary VMM cloud.</span></span>
3. <span data-ttu-id="549a2-127">Włącz replikację hello podstawowej maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="549a2-127">Enable replication for hello primary virtual machine.</span></span> <span data-ttu-id="549a2-128">Azure Site Recovery i VMM upewnij się, że hello tego samego hosta repliki i maszyny wirtualnej zostanie wykryte i będzie używał usługi Azure Site Recovery i ponownie ustanowić replikację przy użyciu hello określonych ustawień.</span><span class="sxs-lookup"><span data-stu-id="549a2-128">Azure Site Recovery and VMM ensure that hello same replica host and virtual machine is detected, and Azure Site Recovery will reuse and reestablish replication using hello specified settings.</span></span>


## <a name="next-steps"></a><span data-ttu-id="549a2-129">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="549a2-129">Next steps</span></span>

<span data-ttu-id="549a2-130">Przejdź za[kroku 10: testować tryb failover](vmm-to-vmm-walkthrough-test-failover.md).</span><span class="sxs-lookup"><span data-stu-id="549a2-130">Go too[Step 10: Run a test failover](vmm-to-vmm-walkthrough-test-failover.md).</span></span>
