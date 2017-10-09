---
title: "Mapowanie sieci aaaConfigure replikowania maszyn wirtualnych funkcji Hyper-V w programie VMM chmur tooAzure z usługą Azure Site Recovery | Dokumentacja firmy Microsoft"
description: "W tym artykule opisano, jak tooconfigure mapowania sieci podczas replikowania maszyn wirtualnych funkcji Hyper-V w programie VMM chmur tooAzure z usługą Azure Site Recovery"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: jwhit
editor: tysonn
ms.assetid: 8e7d868e-00f3-4e8b-9a9e-f23365abf6ac
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/23/2017
ms.author: raynew
ms.openlocfilehash: 081a9fdb0ffa4114099e9bcb9c1b1e43ad26ecbb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="step-9-configure-network-mapping-for-hyper-v-replication-with-vmm-tooazure"></a><span data-ttu-id="1d6e1-103">Krok 9: Konfigurowanie mapowania sieci dla funkcji Hyper-V tooAzure replikacji (w programie VMM)</span><span class="sxs-lookup"><span data-stu-id="1d6e1-103">Step 9: Configure network mapping for Hyper-V replication (with VMM) tooAzure</span></span>

<span data-ttu-id="1d6e1-104">Po skonfigurowaniu hello [źródłowa i docelowa ustawień replikacji](vmm-to-azure-walkthrough-source-target.md), użyj tego artykułu tooconfigure sieci mapowania toomap między sieciami maszyn wirtualnych VMM lokalnych i sieci platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="1d6e1-104">After you set up hello [source and target replication settings](vmm-to-azure-walkthrough-source-target.md), use this article tooconfigure network mapping toomap between on-premises VMM VM networks, and Azure networks.</span></span>

<span data-ttu-id="1d6e1-105">Opublikuj komentarze i pytania u dołu hello w tym artykule, albo na powitania [Forum usług odzyskiwania Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="1d6e1-105">Post comments and questions at hello bottom of this article, or on hello [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>

## <a name="before-you-start"></a><span data-ttu-id="1d6e1-106">Przed rozpoczęciem</span><span class="sxs-lookup"><span data-stu-id="1d6e1-106">Before you start</span></span>

- <span data-ttu-id="1d6e1-107">Dowiedz się więcej o [mapowania sieci](vmm-to-azure-walkthrough-network.md#network-mapping-for-replication-to-azure).</span><span class="sxs-lookup"><span data-stu-id="1d6e1-107">Learn about [network mapping](vmm-to-azure-walkthrough-network.md#network-mapping-for-replication-to-azure).</span></span>
- <span data-ttu-id="1d6e1-108">[Przygotowanie programu VMM do mapowania sieci](vmm-to-azure-walkthrough-network.md#prepare-vmm-for-network-mapping).</span><span class="sxs-lookup"><span data-stu-id="1d6e1-108">[Prepare VMM for network mapping](vmm-to-azure-walkthrough-network.md#prepare-vmm-for-network-mapping).</span></span> 
- <span data-ttu-id="1d6e1-109">Sprawdź, czy maszyny wirtualne na serwerze VMM hello tooa połączonych sieci maszyny Wirtualnej i czy utworzono przynajmniej jedną sieć wirtualną platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="1d6e1-109">Verify that virtual machines on hello VMM server are connected tooa VM network, and that you've created at least one Azure virtual network.</span></span> <span data-ttu-id="1d6e1-110">Wiele sieci Vmnetwork może być zmapowane tooa pojedynczej sieci platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="1d6e1-110">Multiple VM networks can be mapped tooa single Azure network.</span></span>

## <a name="configure-mapping"></a><span data-ttu-id="1d6e1-111">Skonfiguruj mapowanie</span><span class="sxs-lookup"><span data-stu-id="1d6e1-111">Configure mapping</span></span>

<span data-ttu-id="1d6e1-112">Skonfiguruj mapowanie w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="1d6e1-112">Configure mapping as follows:</span></span>

1. <span data-ttu-id="1d6e1-113">W **infrastruktura usługi Site Recovery** > **mapowania sieci** > **mapowanie sieci**, kliknij przycisk hello **+ mapowanie sieci**  ikony.</span><span class="sxs-lookup"><span data-stu-id="1d6e1-113">In **Site Recovery Infrastructure** > **Network mappings** > **Network Mapping**, click hello **+Network Mapping** icon.</span></span>

    ![Mapowanie sieci](./media/vmm-to-azure-walkthrough-network-mapping/network-mapping1.png)
2. <span data-ttu-id="1d6e1-115">W **Dodaj mapowanie sieci**, wybierz pozycję hello źródłowy serwer VMM i **Azure** jako cel hello.</span><span class="sxs-lookup"><span data-stu-id="1d6e1-115">In **Add network mapping**, select hello source VMM server, and **Azure** as hello target.</span></span>
3. <span data-ttu-id="1d6e1-116">Sprawdź hello subskrypcji i modelu wdrażania powitania po pracy awaryjnej.</span><span class="sxs-lookup"><span data-stu-id="1d6e1-116">Verify hello subscription and hello deployment model after failover.</span></span>
4. <span data-ttu-id="1d6e1-117">W **Sieć źródłowa**, wybierz pozycję hello źródłowej lokalnej sieci maszyny Wirtualnej ma toomap z listy hello skojarzone z serwerem VMM hello.</span><span class="sxs-lookup"><span data-stu-id="1d6e1-117">In **Source network**, select hello source on-premises VM network you want toomap from hello list associated with hello VMM server.</span></span>
5. <span data-ttu-id="1d6e1-118">W **Sieć docelowa**, wybierz hello sieć platformy Azure, w którym replika Azure zostaną umieszczone podczas są tworzone.</span><span class="sxs-lookup"><span data-stu-id="1d6e1-118">In **Target network**, select hello Azure network in which replica Azure VMs will be located when they're created.</span></span> <span data-ttu-id="1d6e1-119">Następnie kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="1d6e1-119">Then click **OK**.</span></span>

    ![Mapowanie sieci](./media/vmm-to-azure-walkthrough-network-mapping/network-mapping2.png)

<span data-ttu-id="1d6e1-121">Oto, co się dzieje po rozpoczęciu mapowania sieci:</span><span class="sxs-lookup"><span data-stu-id="1d6e1-121">Here's what happens when network mapping begins:</span></span>

* <span data-ttu-id="1d6e1-122">Istniejące maszyny wirtualne w źródłowej sieci maszyny Wirtualnej hello są toohello połączonych sieci docelowej po rozpoczęciu mapowania.</span><span class="sxs-lookup"><span data-stu-id="1d6e1-122">Existing VMs on hello source VM network are connected toohello target network when mapping begins.</span></span> <span data-ttu-id="1d6e1-123">Nowych maszyn wirtualnych połączonych toohello źródłowej sieci maszyny Wirtualnej są połączone toohello mapowane sieć platformy Azure, podczas replikacji.</span><span class="sxs-lookup"><span data-stu-id="1d6e1-123">New VMs connected toohello source VM network are connected toohello mapped Azure network when replication occurs.</span></span>
* <span data-ttu-id="1d6e1-124">Jeśli zmodyfikujesz istniejące mapowanie sieci maszyn wirtualnych repliki Połącz przy użyciu nowych ustawień hello.</span><span class="sxs-lookup"><span data-stu-id="1d6e1-124">If you modify an existing network mapping, replica virtual machines connect using hello new settings.</span></span>
* <span data-ttu-id="1d6e1-125">Jeśli hello Sieć docelowa ma wiele podsieci i jedna z tych podsieci ma hello znajduje się samą nazwę jak podsieć, w których hello źródłowej maszyny wirtualnej, a następnie maszyny wirtualnej repliki hello łączy toothat docelowej podsieci po pracy awaryjnej.</span><span class="sxs-lookup"><span data-stu-id="1d6e1-125">If hello target network has multiple subnets, and one of those subnets has hello same name as subnet on which hello source virtual machine is located, then hello replica virtual machine connects toothat target subnet after failover.</span></span>
* <span data-ttu-id="1d6e1-126">Jeśli nie ma żadnych docelowa podsieć o pasującej nazwie, maszyna wirtualna hello łączy toohello pierwszej podsieci w sieci hello.</span><span class="sxs-lookup"><span data-stu-id="1d6e1-126">If there’s no target subnet with a matching name, hello virtual machine connects toohello first subnet in hello network.</span></span>



## <a name="next-steps"></a><span data-ttu-id="1d6e1-127">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="1d6e1-127">Next steps</span></span>

<span data-ttu-id="1d6e1-128">Przejdź do zbyt[kroku 10: Tworzenie zasad replikacji](vmm-to-azure-walkthrough-replication.md)</span><span class="sxs-lookup"><span data-stu-id="1d6e1-128">Go too[Step 10: Create a replication policy](vmm-to-azure-walkthrough-replication.md)</span></span>
