---
title: "Konfigurowanie mapowania sieci replikowania maszyn wirtualnych funkcji Hyper-V w chmurach programu VMM na platformie Azure za pomocą usługi Azure Site Recovery | Dokumentacja firmy Microsoft"
description: "Opisuje sposób konfigurowania mapowania sieci podczas replikowania maszyn wirtualnych funkcji Hyper-V w chmurach VMM do platformy Azure z usługą Azure Site Recovery"
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
ms.openlocfilehash: ed6f73d8baea5af0d2aa5f0ae885f305911ccc82
ms.sourcegitcommit: 422efcbac5b6b68295064bd545132fcc98349d01
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/29/2017
---
# <a name="step-9-configure-network-mapping-for-hyper-v-replication-with-vmm-to-azure"></a><span data-ttu-id="6bddb-103">Krok 9: Konfigurowanie mapowania sieci dla replikacji funkcji Hyper-V (w programie VMM) na platformie Azure</span><span class="sxs-lookup"><span data-stu-id="6bddb-103">Step 9: Configure network mapping for Hyper-V replication (with VMM) to Azure</span></span>

<span data-ttu-id="6bddb-104">Po skonfigurowaniu [źródłowa i docelowa ustawień replikacji](vmm-to-azure-walkthrough-source-target.md), użyj w tym artykule, aby skonfigurować mapowanie sieci do mapowania między sieciami maszyn wirtualnych VMM lokalnych i sieci platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="6bddb-104">After you set up the [source and target replication settings](vmm-to-azure-walkthrough-source-target.md), use this article to configure network mapping to map between on-premises VMM VM networks, and Azure networks.</span></span>

<span data-ttu-id="6bddb-105">Opublikuj komentarze i pytania w dolnej części tego artykułu lub na [Forum usług odzyskiwania Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="6bddb-105">Post comments and questions at the bottom of this article, or on the [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>

## <a name="before-you-start"></a><span data-ttu-id="6bddb-106">Przed rozpoczęciem</span><span class="sxs-lookup"><span data-stu-id="6bddb-106">Before you start</span></span>

- <span data-ttu-id="6bddb-107">Dowiedz się więcej o [mapowania sieci](vmm-to-azure-walkthrough-network.md#network-mapping-for-replication-to-azure).</span><span class="sxs-lookup"><span data-stu-id="6bddb-107">Learn about [network mapping](vmm-to-azure-walkthrough-network.md#network-mapping-for-replication-to-azure).</span></span>
- <span data-ttu-id="6bddb-108">[Przygotowanie programu VMM do mapowania sieci](vmm-to-azure-walkthrough-network.md#prepare-vmm-for-network-mapping).</span><span class="sxs-lookup"><span data-stu-id="6bddb-108">[Prepare VMM for network mapping](vmm-to-azure-walkthrough-network.md#prepare-vmm-for-network-mapping).</span></span> 
- <span data-ttu-id="6bddb-109">Sprawdź, czy maszyny wirtualne na serwerze VMM zostały połączone z siecią maszyny wirtualnej i czy utworzono przynajmniej jedną sieć wirtualną platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="6bddb-109">Verify that virtual machines on the VMM server are connected to a VM network, and that you've created at least one Azure virtual network.</span></span> <span data-ttu-id="6bddb-110">Wiele sieci maszyn wirtualnych można mapować do pojedynczej sieci platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="6bddb-110">Multiple VM networks can be mapped to a single Azure network.</span></span>

## <a name="configure-mapping"></a><span data-ttu-id="6bddb-111">Skonfiguruj mapowanie</span><span class="sxs-lookup"><span data-stu-id="6bddb-111">Configure mapping</span></span>

<span data-ttu-id="6bddb-112">Skonfiguruj mapowanie w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="6bddb-112">Configure mapping as follows:</span></span>

1. <span data-ttu-id="6bddb-113">W obszarze **Infrastruktura usługi Site Recovery** > **Mapowania sieci** > **Mapowanie sieci** kliknij ikonę **+ Mapowanie sieci**.</span><span class="sxs-lookup"><span data-stu-id="6bddb-113">In **Site Recovery Infrastructure** > **Network mappings** > **Network Mapping**, click the **+Network Mapping** icon.</span></span>

    ![Mapowanie sieci](./media/vmm-to-azure-walkthrough-network-mapping/network-mapping1.png)
2. <span data-ttu-id="6bddb-115">W obszarze **Dodawanie mapowania sieci** wybierz źródłowy serwer programu VMM i ustaw **Azure** jako element docelowy.</span><span class="sxs-lookup"><span data-stu-id="6bddb-115">In **Add network mapping**, select the source VMM server, and **Azure** as the target.</span></span>
3. <span data-ttu-id="6bddb-116">Sprawdź subskrypcję i model wdrożenia po przejściu do trybu failover.</span><span class="sxs-lookup"><span data-stu-id="6bddb-116">Verify the subscription and the deployment model after failover.</span></span>
4. <span data-ttu-id="6bddb-117">W obszarze **Sieć źródłowa** wybierz lokalną sieć maszyny wirtualnej do mapowania z listy skojarzonej z serwerem VMM.</span><span class="sxs-lookup"><span data-stu-id="6bddb-117">In **Source network**, select the source on-premises VM network you want to map from the list associated with the VMM server.</span></span>
5. <span data-ttu-id="6bddb-118">W obszarze **Sieć docelowa** wybierz sieć platformy Azure, w której znajdą się repliki maszyn wirtualnych Azure po ich utworzeniu.</span><span class="sxs-lookup"><span data-stu-id="6bddb-118">In **Target network**, select the Azure network in which replica Azure VMs will be located when they're created.</span></span> <span data-ttu-id="6bddb-119">Następnie kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="6bddb-119">Then click **OK**.</span></span>

    ![Mapowanie sieci](./media/vmm-to-azure-walkthrough-network-mapping/network-mapping2.png)

<span data-ttu-id="6bddb-121">Oto, co się dzieje po rozpoczęciu mapowania sieci:</span><span class="sxs-lookup"><span data-stu-id="6bddb-121">Here's what happens when network mapping begins:</span></span>

* <span data-ttu-id="6bddb-122">Istniejące maszyny wirtualne w źródłowej sieci maszyn wirtualnych są podłączane do docelowej sieci po rozpoczęciu mapowania.</span><span class="sxs-lookup"><span data-stu-id="6bddb-122">Existing VMs on the source VM network are connected to the target network when mapping begins.</span></span> <span data-ttu-id="6bddb-123">Nowe maszyny wirtualne, połączone ze źródłową siecią maszyn wirtualnych, są łączone z mapowaną siecią platformy Azure po replikacji.</span><span class="sxs-lookup"><span data-stu-id="6bddb-123">New VMs connected to the source VM network are connected to the mapped Azure network when replication occurs.</span></span>
* <span data-ttu-id="6bddb-124">Jeśli modyfikujesz istniejące mapowanie sieci, repliki maszyn wirtualnych są łączone z wykorzystaniem nowych ustawień.</span><span class="sxs-lookup"><span data-stu-id="6bddb-124">If you modify an existing network mapping, replica virtual machines connect using the new settings.</span></span>
* <span data-ttu-id="6bddb-125">Jeśli sieć docelowa ma wiele podsieci i jedna z tych podsieci ma taką samą nazwę, jak podsieć, w której znajduje się źródłowa maszyna wirtualna, replika maszyny wirtualnej jest łączona z tą docelową podsiecią po przejściu do trybu failover.</span><span class="sxs-lookup"><span data-stu-id="6bddb-125">If the target network has multiple subnets, and one of those subnets has the same name as subnet on which the source virtual machine is located, then the replica virtual machine connects to that target subnet after failover.</span></span>
* <span data-ttu-id="6bddb-126">Jeśli nie istnieje docelowa podsieć o takiej samej nazwie, maszyna wirtualna jest łączona z pierwszą podsiecią w sieci.</span><span class="sxs-lookup"><span data-stu-id="6bddb-126">If there’s no target subnet with a matching name, the virtual machine connects to the first subnet in the network.</span></span>



## <a name="next-steps"></a><span data-ttu-id="6bddb-127">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="6bddb-127">Next steps</span></span>

<span data-ttu-id="6bddb-128">Przejdź do [kroku 10: Tworzenie zasad replikacji](vmm-to-azure-walkthrough-replication.md)</span><span class="sxs-lookup"><span data-stu-id="6bddb-128">Go to [Step 10: Create a replication policy](vmm-to-azure-walkthrough-replication.md)</span></span>
