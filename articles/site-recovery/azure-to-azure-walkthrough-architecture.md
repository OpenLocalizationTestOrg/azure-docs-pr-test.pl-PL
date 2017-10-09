---
title: "Architektura hello aaaReview replikacji maszyn wirtualnych Azure między regiony platformy Azure | Dokumentacja firmy Microsoft"
description: "Ten artykuł zawiera omówienie składników i architektury używane podczas replikowania maszyn wirtualnych platformy Azure między regiony platformy Azure przy użyciu usługi Azure Site Recovery hello."
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: 
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 07/12/2017
ms.author: raynew
ms.openlocfilehash: 4caab4e7a764040f317201d1345c40c73f836d81
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="step-1-review-hello-architecture-for-azure-vm-replication-between-azure-regions"></a><span data-ttu-id="de5a1-103">Krok 1: Przegląd architektury hello replikacji maszyny Wirtualnej Azure między regiony platformy Azure</span><span class="sxs-lookup"><span data-stu-id="de5a1-103">Step 1: Review hello architecture for Azure VM replication between Azure regions</span></span>


<span data-ttu-id="de5a1-104">Po przejrzeniu hello [czynności przeglądu](azure-to-azure-walkthrough-overview.md) dla tego wdrożenia, przeczytaj ten artykuł toounderstand hello składniki i procesy stosowane podczas replikacji i odzyskiwania maszyn wirtualnych platformy Azure (maszyny wirtualne) z jedną tooanother region platformy Azure, przy użyciu [Usługi azure Site Recovery](site-recovery-overview.md).</span><span class="sxs-lookup"><span data-stu-id="de5a1-104">After reviewing hello [overview steps](azure-to-azure-walkthrough-overview.md) for this deployment, read this article toounderstand hello components and processes used when replicating and recovering Azure virtual machines (VMs) from one Azure region tooanother, using [Azure Site Recovery](site-recovery-overview.md).</span></span>

- <span data-ttu-id="de5a1-105">Po zakończeniu hello artykuł ma przejrzysty działania region tooanother replikacji maszyny Wirtualnej platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="de5a1-105">When you finish hello article, you should have a clear understanding of how Azure VM replication tooanother region works.</span></span>
- <span data-ttu-id="de5a1-106">Opublikuj wszelkie komentarze u dołu hello w tym artykule, lub zadać pytania w hello [Forum usług odzyskiwania Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="de5a1-106">Post any comments at hello bottom of this article, or ask questions in hello [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>

>[!NOTE]
><span data-ttu-id="de5a1-107">Azure replikacji maszyny Wirtualnej za pomocą hello usługi Site Recovery jest obecnie w przeglądzie.</span><span class="sxs-lookup"><span data-stu-id="de5a1-107">Azure VM replication with hello Site Recovery service is currently in preview.</span></span>



## <a name="architectural-components"></a><span data-ttu-id="de5a1-108">Składniki architektury</span><span class="sxs-lookup"><span data-stu-id="de5a1-108">Architectural components</span></span>

<span data-ttu-id="de5a1-109">powitania po diagram przedstawia ogólny widok środowiska maszyny Wirtualnej platformy Azure w określonym regionie (w tym przykładzie hello wschodnie stany USA lokalizacji).</span><span class="sxs-lookup"><span data-stu-id="de5a1-109">hello following diagram provides a high-level view of an Azure VM environment in a specific region (in this example, hello East US location).</span></span> <span data-ttu-id="de5a1-110">W środowisku maszyny Wirtualnej platformy Azure:</span><span class="sxs-lookup"><span data-stu-id="de5a1-110">In an Azure VM environment:</span></span>
- <span data-ttu-id="de5a1-111">Aplikacje mogą działać na maszynach wirtualnych z dyskami rozmieszczenie do kont magazynu.</span><span class="sxs-lookup"><span data-stu-id="de5a1-111">Apps can be running on VMs with disks spread across storage accounts.</span></span>
- <span data-ttu-id="de5a1-112">Witaj maszyny wirtualne mogą zostać włączone w co najmniej jednej podsieci sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="de5a1-112">hello VMs can be included in one or more subnets within a virtual network.</span></span>

![środowisko klienta](./media/azure-to-azure-walkthrough-architecture/source-environment.png)

## <a name="replication-process"></a><span data-ttu-id="de5a1-114">Proces replikacji</span><span class="sxs-lookup"><span data-stu-id="de5a1-114">Replication process</span></span>

### <a name="step-1"></a><span data-ttu-id="de5a1-115">Krok 1</span><span class="sxs-lookup"><span data-stu-id="de5a1-115">Step 1</span></span>

<span data-ttu-id="de5a1-116">Po włączeniu replikacji maszyny Wirtualnej platformy Azure w portalu Azure hello hello pokazane w powitania po diagram i tabeli są tworzone automatycznie w region docelowy hello zasobów.</span><span class="sxs-lookup"><span data-stu-id="de5a1-116">When you enable Azure VM replication in hello Azure portal, hello resources shown in hello following diagram and table are automatically created in hello target region.</span></span> <span data-ttu-id="de5a1-117">Domyślnie zasoby są tworzone zgodnie z ustawieniami region źródła.</span><span class="sxs-lookup"><span data-stu-id="de5a1-117">By default, resources are created based on source region settings.</span></span> <span data-ttu-id="de5a1-118">Można dostosować ustawienia obiektu docelowego hello zgodnie z potrzebami.</span><span class="sxs-lookup"><span data-stu-id="de5a1-118">You can customize hello target settings as required.</span></span> <span data-ttu-id="de5a1-119">[Dowiedz się więcej](site-recovery-replicate-azure-to-azure.md).</span><span class="sxs-lookup"><span data-stu-id="de5a1-119">[Learn more](site-recovery-replicate-azure-to-azure.md).</span></span>

![Włącz proces replikacji, krok 1](./media/azure-to-azure-walkthrough-architecture/enable-replication-step-1.png)

<span data-ttu-id="de5a1-121">**Zasób**</span><span class="sxs-lookup"><span data-stu-id="de5a1-121">**Resource**</span></span> | <span data-ttu-id="de5a1-122">**Szczegóły**</span><span class="sxs-lookup"><span data-stu-id="de5a1-122">**Details**</span></span>
--- | ---
<span data-ttu-id="de5a1-123">**Docelowa grupa zasobów**</span><span class="sxs-lookup"><span data-stu-id="de5a1-123">**Target resource group**</span></span> | <span data-ttu-id="de5a1-124">Witaj toowhich grupy zasobów należy replikowanych maszyn wirtualnych po pracy awaryjnej.</span><span class="sxs-lookup"><span data-stu-id="de5a1-124">hello resource group toowhich replicated VMs belong after failover.</span></span>
<span data-ttu-id="de5a1-125">**Docelowy sieci wirtualnej**</span><span class="sxs-lookup"><span data-stu-id="de5a1-125">**Target virtual network**</span></span> | <span data-ttu-id="de5a1-126">sieć wirtualna Hello w którym replikowanych maszyn wirtualnych znajdują się po pracy awaryjnej.</span><span class="sxs-lookup"><span data-stu-id="de5a1-126">hello virtual network in which replicated VMs are located after failover.</span></span> <span data-ttu-id="de5a1-127">Mapowanie sieci jest tworzony między sieciami wirtualnymi źródłowym i docelowym i na odwrót.</span><span class="sxs-lookup"><span data-stu-id="de5a1-127">A network mapping is created between source and target virtual networks, and vice versa.</span></span>
<span data-ttu-id="de5a1-128">**Konta magazynu pamięci podręcznej**</span><span class="sxs-lookup"><span data-stu-id="de5a1-128">**Cache storage accounts**</span></span> | <span data-ttu-id="de5a1-129">Przed zmian w źródle, które maszyny wirtualne są replikowane toohello docelowe konto magazynu, są śledzone i wysłane konta magazynu pamięci podręcznej toohello w miejscu docelowym hello.</span><span class="sxs-lookup"><span data-stu-id="de5a1-129">Before changes on source VMs are replicated toohello target storage account, they are tracked and sent toohello cache storage account in hello target location.</span></span> <span data-ttu-id="de5a1-130">Dzięki temu minimalny wpływ na produkcji aplikacje działające na powitania maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="de5a1-130">This ensures minimal impact on production apps running on hello VM.</span></span>
<span data-ttu-id="de5a1-131">**Konta magazynu docelowego**</span><span class="sxs-lookup"><span data-stu-id="de5a1-131">**Target storage accounts**</span></span>  | <span data-ttu-id="de5a1-132">Konta magazynu w hello docelowej lokalizacji toowhich hello dane są replikowane.</span><span class="sxs-lookup"><span data-stu-id="de5a1-132">Storage accounts in hello target location toowhich hello data is replicated.</span></span>
<span data-ttu-id="de5a1-133">**Docelowy zestawów dostępności**</span><span class="sxs-lookup"><span data-stu-id="de5a1-133">**Target availability sets**</span></span>  | <span data-ttu-id="de5a1-134">Zestawy dostępności w których hello replikowane maszyny wirtualne znajdują się po pracy awaryjnej.</span><span class="sxs-lookup"><span data-stu-id="de5a1-134">Availability sets in which hello replicated VMs are located after failover.</span></span>

### <a name="step-2"></a><span data-ttu-id="de5a1-135">Krok 2</span><span class="sxs-lookup"><span data-stu-id="de5a1-135">Step 2</span></span>

<span data-ttu-id="de5a1-136">Ponieważ replikacja jest włączona, hello rozszerzenia usługi Site Recovery usługi mobilności jest automatycznie instalowany na powitania maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="de5a1-136">As replication is enabled, hello Site Recovery extension Mobility service is automatically installed on hello VM.</span></span> <span data-ttu-id="de5a1-137">występuje Hello następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="de5a1-137">hello following occurs:</span></span>

1. <span data-ttu-id="de5a1-138">Witaj maszyny Wirtualnej jest zarejestrowany z usługą Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="de5a1-138">hello VM is registered with Site Recovery.</span></span>

2. <span data-ttu-id="de5a1-139">Ciągła replikacja jest skonfigurowana dla hello maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="de5a1-139">Continuous replication is configured for hello VM.</span></span> <span data-ttu-id="de5a1-140">Zapisuje dane na powitania maszyny Wirtualnej dyski są stale toohello konta magazynu pamięci podręcznej w lokalizacji źródłowej hello transferu.</span><span class="sxs-lookup"><span data-stu-id="de5a1-140">Data writes on hello VM disks are continuously transferred toohello cache storage account in hello source location.</span></span>

   ![Włącz proces replikacji, krok 2](./media/azure-to-azure-walkthrough-architecture/enable-replication-step-2.png)

  
  <span data-ttu-id="de5a1-142">Należy pamiętać, że Site Recovery nigdy nie wymaga ruchu przychodzącego toohello łączności maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="de5a1-142">Note that Site Recovery never needs inbound connectivity toohello VM.</span></span> <span data-ttu-id="de5a1-143">Wychodzące tylko adresów URL/IP usługa odzyskiwania tooSite łączności, adresy URL/IP uwierzytelnianie usługi Office 365 i adresy IP konta magazynu pamięci podręcznej jest wymagana.</span><span class="sxs-lookup"><span data-stu-id="de5a1-143">Only outbound connectivity tooSite Recovery service URLs/IP addresses, Office 365 authentication URLs/IP addresses, and cache storage account IP addresses is needed.</span></span> 

## <a name="continuous-replication-process"></a><span data-ttu-id="de5a1-144">Proces replikacji ciągłej</span><span class="sxs-lookup"><span data-stu-id="de5a1-144">Continuous replication process</span></span>

<span data-ttu-id="de5a1-145">Po replikacji ciągłej działa, dysk, który zapisuje są natychmiast przekazywane konta magazynu pamięci podręcznej toohello.</span><span class="sxs-lookup"><span data-stu-id="de5a1-145">After continuous replication is working, disk writes are immediately transferred toohello cache storage account.</span></span> <span data-ttu-id="de5a1-146">Usługa Site Recovery przetwarza dane hello i wysyła je toohello docelowe konto magazynu.</span><span class="sxs-lookup"><span data-stu-id="de5a1-146">Site Recovery processes hello data and sends it toohello target storage account.</span></span> <span data-ttu-id="de5a1-147">Po przetworzeniu danych hello punkty odzyskiwania są generowane w hello docelowe konto magazynu, co kilka minut.</span><span class="sxs-lookup"><span data-stu-id="de5a1-147">After hello data is processed, recovery points are generated in hello target storage account every few minutes.</span></span>

## <a name="failover-process"></a><span data-ttu-id="de5a1-148">Proces trybu failover</span><span class="sxs-lookup"><span data-stu-id="de5a1-148">Failover process</span></span>

<span data-ttu-id="de5a1-149">Po zainicjowaniu tryb failover maszyny wirtualne są tworzone w hello docelowa grupa zasobów, wirtualnych sieci docelowej, podsieci docelowej powitalne i hello docelowego zestawu dostępności.</span><span class="sxs-lookup"><span data-stu-id="de5a1-149">When you initiate a failover, hello VMs are created in hello target resource group, target virtual network, target subnet, and hello target availability set.</span></span> <span data-ttu-id="de5a1-150">Podczas pracy awaryjnej można użyć dowolnego punktu odzyskiwania.</span><span class="sxs-lookup"><span data-stu-id="de5a1-150">During a failover, you can use any recovery point.</span></span>

![Proces trybu failover](./media/azure-to-azure-walkthrough-architecture/failover.png)

## <a name="next-steps"></a><span data-ttu-id="de5a1-152">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="de5a1-152">Next steps</span></span>

<span data-ttu-id="de5a1-153">Przejdź do zbyt[krok 2: Sprawdź wymagania wstępne i ograniczenia](azure-to-azure-walkthrough-prerequisites.md)</span><span class="sxs-lookup"><span data-stu-id="de5a1-153">Go too[Step 2: Verify prerequisites and limitations](azure-to-azure-walkthrough-prerequisites.md)</span></span>
