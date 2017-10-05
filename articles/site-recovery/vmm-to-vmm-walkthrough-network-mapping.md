---
title: "Mapowanie sieci dla maszyny Wirtualnej funkcji Hyper-V replikacji do lokacji dodatkowej z usługą Azure Site Recovery | Dokumentacja firmy Microsoft"
description: "Opisuje sposób mapowania sieci podczas replikowania maszyn wirtualnych funkcji Hyper-V do lokacji dodatkowej programu VMM z usługą Azure Site Recovery."
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
ms.openlocfilehash: 606e2d3d0e31b9d80200105e812f9d7bbbcf939c
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="step-7-map-networks-for-hyper-v-vm-replication-to-a-secondary-site"></a><span data-ttu-id="159dd-103">Krok 7: Mapowanie sieci dla maszyny Wirtualnej funkcji Hyper-V replikacji do lokacji dodatkowej</span><span class="sxs-lookup"><span data-stu-id="159dd-103">Step 7: Map networks for Hyper-V VM replication to a secondary site</span></span>


<span data-ttu-id="159dd-104">Po skonfigurowaniu [ustawienia źródłowe i docelowe](vmm-to-vmm-walkthrough-source-target.md) replikowania maszyn wirtualnych funkcji Hyper-V (VM) do lokacji dodatkowej programu System Center Virtual Machine Manager (VMM), użyj w tym artykule, aby skonfigurować mapowanie sieci dla funkcji Hyper-V maszyny wirtualnej ( Replikacja maszyny Wirtualnej) do dodatkowej lokacji przy użyciu [usługi Azure Site Recovery](site-recovery-overview.md).</span><span class="sxs-lookup"><span data-stu-id="159dd-104">After setting up [source and target settings](vmm-to-vmm-walkthrough-source-target.md) for replicating Hyper-V virtual machines (VMs) to a secondary System Center Virtual Machine Manager (VMM) site, use this article to configure network mapping for Hyper-V virtual machine (VM) replication to a secondary site, using  [Azure Site Recovery](site-recovery-overview.md).</span></span>

<span data-ttu-id="159dd-105">Po przeczytaniu tego artykułu zamieść wszelkie komentarze u dołu lub na [forum usług Azure Recovery Services](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="159dd-105">After reading this article, post any comments at the bottom, or on the [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>


## <a name="before-you-start"></a><span data-ttu-id="159dd-106">Przed rozpoczęciem</span><span class="sxs-lookup"><span data-stu-id="159dd-106">Before you start</span></span>

- <span data-ttu-id="159dd-107">Dowiedz się więcej o [mapowania sieci](vmm-to-vmm-walkthrough-network.md#network-mapping-overview) przed jego uruchomieniem.</span><span class="sxs-lookup"><span data-stu-id="159dd-107">Learn about [network mapping](vmm-to-vmm-walkthrough-network.md#network-mapping-overview) before you start.</span></span>
- <span data-ttu-id="159dd-108">Sprawdź, czy maszyny wirtualne na serwerach VMM są połączone z siecią maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="159dd-108">Verify that virtual machines on VMM servers are connected to a VM network.</span></span>

## <a name="configure-network-mapping"></a><span data-ttu-id="159dd-109">Konfiguracja mapowania sieci</span><span class="sxs-lookup"><span data-stu-id="159dd-109">Configure network mapping</span></span>

1. <span data-ttu-id="159dd-110">W **mapowanie sieci** > **mapowania sieci**, kliknij przycisk **+ mapowanie sieci**.</span><span class="sxs-lookup"><span data-stu-id="159dd-110">In **Network Mapping** > **Network mappings**, click **+Network Mapping**.</span></span>
2. <span data-ttu-id="159dd-111">W **Dodaj mapowanie sieci** , wybierz źródło i VMM serwery docelowe.</span><span class="sxs-lookup"><span data-stu-id="159dd-111">In **Add network mapping** tab, select the source and target VMM servers.</span></span> <span data-ttu-id="159dd-112">Pobierane są wszystkie sieci maszyny Wirtualnej skojarzone z serwerów programu VMM.</span><span class="sxs-lookup"><span data-stu-id="159dd-112">The VM networks associated with the VMM servers are retrieved.</span></span>
3. <span data-ttu-id="159dd-113">W **Sieć źródłowa**, wybierz sieć, którego chcesz użyć na liście sieci maszyny Wirtualnej skojarzone z podstawowym serwerem programu VMM.</span><span class="sxs-lookup"><span data-stu-id="159dd-113">In **Source network**, select the network you want to use from the list of VM networks associated with the primary VMM server.</span></span>
4. <span data-ttu-id="159dd-114">W **Sieć docelowa**, wybierz sieć, którego chcesz użyć na pomocniczym serwerze programu VMM.</span><span class="sxs-lookup"><span data-stu-id="159dd-114">In **Target network**, select the network you want to use on the secondary VMM server.</span></span> <span data-ttu-id="159dd-115">Następnie kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="159dd-115">Then click **OK**.</span></span>

    ![Mapowanie sieci](./media/vmm-to-vmm-walkthrough-network-mapping/network-mapping2.png)

<span data-ttu-id="159dd-117">Oto, co się dzieje po rozpoczęciu mapowania sieci:</span><span class="sxs-lookup"><span data-stu-id="159dd-117">Here's what happens when network mapping begins:</span></span>

* <span data-ttu-id="159dd-118">Wszystkie istniejące maszyny wirtualne repliki odpowiadające źródłowej sieci maszyny Wirtualnej zostaną podłączone do sieci docelowej maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="159dd-118">Any existing replica virtual machines that correspond to the source VM network will be connected to the target VM network.</span></span>
* <span data-ttu-id="159dd-119">Nowe maszyny wirtualne, które są podłączone do źródłowej sieci maszyny Wirtualnej zostanie podłączona do sieci docelowej mapowane po replikacji.</span><span class="sxs-lookup"><span data-stu-id="159dd-119">New virtual machines that are connected to the source VM network will be connected to the target mapped network after replication.</span></span>
* <span data-ttu-id="159dd-120">Jeśli zmodyfikujesz istniejące mapowanie, uwzględniając nową sieć, maszyn wirtualne repliki zostaną podłączone z wykorzystaniem nowych ustawień.</span><span class="sxs-lookup"><span data-stu-id="159dd-120">If you modify an existing mapping with a new network, replica virtual machines will be connected using the new settings.</span></span>
* <span data-ttu-id="159dd-121">Jeśli sieć docelowa ma wiele podsieci i jedna z tych podsieci ma taką samą nazwę, jak podsieć, w której znajduje się źródłowa maszyna wirtualna, replika maszyny wirtualnej zostanie podłączona do tej docelowej podsieci po przejściu do trybu failover.</span><span class="sxs-lookup"><span data-stu-id="159dd-121">If the target network has multiple subnets and one of those subnets has the same name as subnet on which the source virtual machine is located, then the replica virtual machine will be connected to that target subnet after failover.</span></span> <span data-ttu-id="159dd-122">Jeśli nie istnieje docelowa podsieć o takiej samej nazwie, maszyna wirtualna zostanie podłączona do pierwszej podsieci w sieci.</span><span class="sxs-lookup"><span data-stu-id="159dd-122">If there’s no target subnet with a matching name, the virtual machine will be connected to the first subnet in the network.</span></span>



## <a name="next-steps"></a><span data-ttu-id="159dd-123">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="159dd-123">Next steps</span></span>

<span data-ttu-id="159dd-124">Przejdź do [krok 8: Skonfiguruj zasady replikacji](vmm-to-vmm-walkthrough-replication.md).</span><span class="sxs-lookup"><span data-stu-id="159dd-124">Go to [Step 8: Configure a replication policy](vmm-to-vmm-walkthrough-replication.md).</span></span>