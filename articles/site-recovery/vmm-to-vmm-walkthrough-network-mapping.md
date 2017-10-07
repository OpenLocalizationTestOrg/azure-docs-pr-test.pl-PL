---
title: "aaaMap sieci dla lokacji dodatkowej tooa replikacji maszyny Wirtualnej funkcji Hyper-V z usługą Azure Site Recovery | Dokumentacja firmy Microsoft"
description: "W tym artykule opisano, jak toomap sieci podczas replikowania maszyn wirtualnych funkcji Hyper-V tooa lokacja dodatkowa programu VMM z usługą Azure Site Recovery."
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: 461b7c1c-ef61-4005-aeec-2324e727a3d0
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/30/2017
ms.author: raynew
ms.openlocfilehash: d4f621df4ce08ae055bc6809daea0b71b76754ad
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="step-7-map-networks-for-hyper-v-vm-replication-tooa-secondary-site"></a><span data-ttu-id="ec7f2-103">Krok 7: Mapowanie sieci dla lokacji dodatkowej tooa replikacji maszyny Wirtualnej funkcji Hyper-V</span><span class="sxs-lookup"><span data-stu-id="ec7f2-103">Step 7: Map networks for Hyper-V VM replication tooa secondary site</span></span>


<span data-ttu-id="ec7f2-104">Po skonfigurowaniu [ustawienia źródłowe i docelowe](vmm-to-vmm-walkthrough-source-target.md) replikację funkcji Hyper-V maszynach wirtualnych (VM) tooa System Center Virtual Machine Manager (VMM) lokacji dodatkowej, użyć tego mapowania artykułu tooconfigure sieci wirtualnej funkcji Hyper-v Maszyna wirtualna replikacji tooa dodatkowej lokacji przy użyciu [usługi Azure Site Recovery](site-recovery-overview.md).</span><span class="sxs-lookup"><span data-stu-id="ec7f2-104">After setting up [source and target settings](vmm-to-vmm-walkthrough-source-target.md) for replicating Hyper-V virtual machines (VMs) tooa secondary System Center Virtual Machine Manager (VMM) site, use this article tooconfigure network mapping for Hyper-V virtual machine (VM) replication tooa secondary site, using  [Azure Site Recovery](site-recovery-overview.md).</span></span>

<span data-ttu-id="ec7f2-105">Po przeczytaniu tego artykułu, post wszelkie komentarze u dołu hello, lub na powitania [Forum usług odzyskiwania Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="ec7f2-105">After reading this article, post any comments at hello bottom, or on hello [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>


## <a name="before-you-start"></a><span data-ttu-id="ec7f2-106">Przed rozpoczęciem</span><span class="sxs-lookup"><span data-stu-id="ec7f2-106">Before you start</span></span>

- <span data-ttu-id="ec7f2-107">Dowiedz się więcej o [mapowania sieci](vmm-to-vmm-walkthrough-network.md#network-mapping-overview) przed jego uruchomieniem.</span><span class="sxs-lookup"><span data-stu-id="ec7f2-107">Learn about [network mapping](vmm-to-vmm-walkthrough-network.md#network-mapping-overview) before you start.</span></span>
- <span data-ttu-id="ec7f2-108">Sprawdź, czy maszyny wirtualne na serwerach VMM są połączone tooa sieci maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="ec7f2-108">Verify that virtual machines on VMM servers are connected tooa VM network.</span></span>

## <a name="configure-network-mapping"></a><span data-ttu-id="ec7f2-109">Konfiguracja mapowania sieci</span><span class="sxs-lookup"><span data-stu-id="ec7f2-109">Configure network mapping</span></span>

1. <span data-ttu-id="ec7f2-110">W **mapowanie sieci** > **mapowania sieci**, kliknij przycisk **+ mapowanie sieci**.</span><span class="sxs-lookup"><span data-stu-id="ec7f2-110">In **Network Mapping** > **Network mappings**, click **+Network Mapping**.</span></span>
2. <span data-ttu-id="ec7f2-111">W **Dodaj mapowanie sieci** , wybierz źródło hello i VMM serwery docelowe.</span><span class="sxs-lookup"><span data-stu-id="ec7f2-111">In **Add network mapping** tab, select hello source and target VMM servers.</span></span> <span data-ttu-id="ec7f2-112">Witaj sieci maszyny Wirtualnej skojarzone z serwerów VMM hello są pobierane.</span><span class="sxs-lookup"><span data-stu-id="ec7f2-112">hello VM networks associated with hello VMM servers are retrieved.</span></span>
3. <span data-ttu-id="ec7f2-113">W **Sieć źródłowa**, wybierz sieć hello ma toouse z listy hello sieci maszyny Wirtualnej skojarzone z hello podstawowy serwer VMM.</span><span class="sxs-lookup"><span data-stu-id="ec7f2-113">In **Source network**, select hello network you want toouse from hello list of VM networks associated with hello primary VMM server.</span></span>
4. <span data-ttu-id="ec7f2-114">W **Sieć docelowa**, wybierz sieć hello ma toouse na powitania pomocniczy serwer programu VMM.</span><span class="sxs-lookup"><span data-stu-id="ec7f2-114">In **Target network**, select hello network you want toouse on hello secondary VMM server.</span></span> <span data-ttu-id="ec7f2-115">Następnie kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="ec7f2-115">Then click **OK**.</span></span>

    ![Mapowanie sieci](./media/vmm-to-vmm-walkthrough-network-mapping/network-mapping2.png)

<span data-ttu-id="ec7f2-117">Oto, co się dzieje po rozpoczęciu mapowania sieci:</span><span class="sxs-lookup"><span data-stu-id="ec7f2-117">Here's what happens when network mapping begins:</span></span>

* <span data-ttu-id="ec7f2-118">Wszystkie istniejące maszyny wirtualne repliki odpowiadające źródłowej sieci maszyny Wirtualnej toohello będzie sieć maszyny Wirtualnej podłączonej toohello docelowej.</span><span class="sxs-lookup"><span data-stu-id="ec7f2-118">Any existing replica virtual machines that correspond toohello source VM network will be connected toohello target VM network.</span></span>
* <span data-ttu-id="ec7f2-119">Nowe maszyny wirtualne, które są połączone toohello źródłowej sieci maszyny Wirtualnej będzie mapowanej sieci docelowej połączonych toohello po replikacji.</span><span class="sxs-lookup"><span data-stu-id="ec7f2-119">New virtual machines that are connected toohello source VM network will be connected toohello target mapped network after replication.</span></span>
* <span data-ttu-id="ec7f2-120">Jeśli zmodyfikujesz istniejące mapowanie, uwzględniając nową sieć maszyn wirtualnych repliki zostaną podłączone z wykorzystaniem nowych ustawień hello.</span><span class="sxs-lookup"><span data-stu-id="ec7f2-120">If you modify an existing mapping with a new network, replica virtual machines will be connected using hello new settings.</span></span>
* <span data-ttu-id="ec7f2-121">Jeśli hello Sieć docelowa ma wiele podsieci i jedna z tych podsieci ma hello znajduje się samą nazwę jak podsieć, w których hello źródłowej maszyny wirtualnej, a następnie hello repliki maszyny wirtualnej zostaną połączone toothat docelowej podsieci po pracy awaryjnej.</span><span class="sxs-lookup"><span data-stu-id="ec7f2-121">If hello target network has multiple subnets and one of those subnets has hello same name as subnet on which hello source virtual machine is located, then hello replica virtual machine will be connected toothat target subnet after failover.</span></span> <span data-ttu-id="ec7f2-122">Jeśli nie ma żadnych docelowa podsieć o pasującej nazwie, maszyna wirtualna hello będzie toohello połączonych pierwszej podsieci w sieci hello.</span><span class="sxs-lookup"><span data-stu-id="ec7f2-122">If there’s no target subnet with a matching name, hello virtual machine will be connected toohello first subnet in hello network.</span></span>



## <a name="next-steps"></a><span data-ttu-id="ec7f2-123">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="ec7f2-123">Next steps</span></span>

<span data-ttu-id="ec7f2-124">Przejdź za[krok 8: Skonfiguruj zasady replikacji](vmm-to-vmm-walkthrough-replication.md).</span><span class="sxs-lookup"><span data-stu-id="ec7f2-124">Go too[Step 8: Configure a replication policy](vmm-to-vmm-walkthrough-replication.md).</span></span>
