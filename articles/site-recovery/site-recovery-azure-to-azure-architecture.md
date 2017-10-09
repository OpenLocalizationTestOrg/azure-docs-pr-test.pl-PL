---
title: "aaaHow czy replikacja maszyny wirtualnej platformy Azure między pracy regiony platformy Azure w usłudze Azure Site Recovery?  | Microsoft Docs"
description: "Ten artykuł zawiera omówienie składników i architektury używane podczas replikowania maszyn wirtualnych platformy Azure między regiony platformy Azure przy użyciu usługi Azure Site Recovery hello."
services: site-recovery
documentationcenter: 
author: sujayt
manager: rochakm
editor: 
ms.assetid: 
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 05/29/2017
ms.author: sujayt
ms.openlocfilehash: 01eda83e490821f8afc8a2973c18a19453a2e84a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-does-azure-vm-replication-work-in-site-recovery"></a><span data-ttu-id="6d17f-104">Jak działa replikacja maszyny Wirtualnej platformy Azure w usłudze Site Recovery?</span><span class="sxs-lookup"><span data-stu-id="6d17f-104">How does Azure VM replication work in Site Recovery?</span></span>


<span data-ttu-id="6d17f-105">W tym artykule opisano składniki hello i procesy wykonywane w replikacji i odzyskiwania maszyn wirtualnych platformy Azure (maszyn wirtualnych) z jednego regionu tooanother przy użyciu hello [usługi Azure Site Recovery](site-recovery-overview.md) usługi.</span><span class="sxs-lookup"><span data-stu-id="6d17f-105">This article describes hello components and processes involved in replicating and recovering Azure virtual machines (VMs) from one region tooanother by using hello [Azure Site Recovery](site-recovery-overview.md) service.</span></span>

>[!NOTE]
><span data-ttu-id="6d17f-106">Azure replikacji maszyny Wirtualnej za pomocą hello usługi Site Recovery jest obecnie w przeglądzie.</span><span class="sxs-lookup"><span data-stu-id="6d17f-106">Azure VM replication with hello Site Recovery service is currently in preview.</span></span>

<span data-ttu-id="6d17f-107">Opublikuj wszelkie komentarze u dołu hello w tym artykule, lub zadać pytania w hello [Forum usług odzyskiwania Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="6d17f-107">Post any comments at hello bottom of this article, or ask questions in hello [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>

## <a name="architectural-components"></a><span data-ttu-id="6d17f-108">Składniki architektury</span><span class="sxs-lookup"><span data-stu-id="6d17f-108">Architectural components</span></span>

<span data-ttu-id="6d17f-109">powitania po diagram przedstawia ogólny widok środowiska maszyny Wirtualnej platformy Azure w określonym regionie (w tym przykładzie hello wschodnie stany USA lokalizacji).</span><span class="sxs-lookup"><span data-stu-id="6d17f-109">hello following diagram provides a high-level view of an Azure VM environment in a specific region (in this example, hello East US location).</span></span> <span data-ttu-id="6d17f-110">W środowisku maszyny Wirtualnej platformy Azure:</span><span class="sxs-lookup"><span data-stu-id="6d17f-110">In an Azure VM environment:</span></span>
- <span data-ttu-id="6d17f-111">Aplikacje mogą działać na maszynach wirtualnych z dyskami rozmieszczenie do kont magazynu.</span><span class="sxs-lookup"><span data-stu-id="6d17f-111">Apps can be running on VMs with disks spread across storage accounts.</span></span>
- <span data-ttu-id="6d17f-112">Witaj maszyny wirtualne mogą zostać włączone w co najmniej jednej podsieci sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="6d17f-112">hello VMs can be included in one or more subnets within a virtual network.</span></span>

![środowisko klienta](./media/site-recovery-azure-to-azure-architecture/source-environment.png)

<span data-ttu-id="6d17f-114">Dowiedz się więcej o wymaganiach wstępnych wdrożenia hello oraz wymagań dotyczących hello [macierz obsługi](site-recovery-support-matrix-azure-to-azure.md).</span><span class="sxs-lookup"><span data-stu-id="6d17f-114">Learn about hello deployment prerequisites and requirements in hello [support matrix](site-recovery-support-matrix-azure-to-azure.md).</span></span>

## <a name="replication-process"></a><span data-ttu-id="6d17f-115">Proces replikacji</span><span class="sxs-lookup"><span data-stu-id="6d17f-115">Replication process</span></span>

### <a name="step-1"></a><span data-ttu-id="6d17f-116">Krok 1</span><span class="sxs-lookup"><span data-stu-id="6d17f-116">Step 1</span></span>

<span data-ttu-id="6d17f-117">Po włączeniu replikacji maszyny Wirtualnej platformy Azure w portalu Azure hello hello pokazane w powitania po diagram i tabeli są tworzone automatycznie w region docelowy hello zasobów.</span><span class="sxs-lookup"><span data-stu-id="6d17f-117">When you enable Azure VM replication in hello Azure portal, hello resources shown in hello following diagram and table are automatically created in hello target region.</span></span> <span data-ttu-id="6d17f-118">Domyślnie zasoby są tworzone zgodnie z ustawieniami region źródła.</span><span class="sxs-lookup"><span data-stu-id="6d17f-118">By default, resources are created based on source region settings.</span></span> <span data-ttu-id="6d17f-119">Można dostosować ustawienia obiektu docelowego hello zgodnie z potrzebami.</span><span class="sxs-lookup"><span data-stu-id="6d17f-119">You can customize hello target settings as required.</span></span> <span data-ttu-id="6d17f-120">[Dowiedz się więcej](site-recovery-replicate-azure-to-azure.md).</span><span class="sxs-lookup"><span data-stu-id="6d17f-120">[Learn more](site-recovery-replicate-azure-to-azure.md).</span></span>

![Włącz proces replikacji, krok 1](./media/site-recovery-azure-to-azure-architecture/enable-replication-step-1.png)

<span data-ttu-id="6d17f-122">**Zasób**</span><span class="sxs-lookup"><span data-stu-id="6d17f-122">**Resource**</span></span> | <span data-ttu-id="6d17f-123">**Szczegóły**</span><span class="sxs-lookup"><span data-stu-id="6d17f-123">**Details**</span></span>
--- | ---
<span data-ttu-id="6d17f-124">**Docelowa grupa zasobów**</span><span class="sxs-lookup"><span data-stu-id="6d17f-124">**Target resource group**</span></span> | <span data-ttu-id="6d17f-125">Witaj toowhich grupy zasobów należy replikowanych maszyn wirtualnych po pracy awaryjnej.</span><span class="sxs-lookup"><span data-stu-id="6d17f-125">hello resource group toowhich replicated VMs belong after failover.</span></span>
<span data-ttu-id="6d17f-126">**Docelowy sieci wirtualnej**</span><span class="sxs-lookup"><span data-stu-id="6d17f-126">**Target virtual network**</span></span> | <span data-ttu-id="6d17f-127">sieć wirtualna Hello w którym replikowanych maszyn wirtualnych znajdują się po pracy awaryjnej.</span><span class="sxs-lookup"><span data-stu-id="6d17f-127">hello virtual network in which replicated VMs are located after failover.</span></span> <span data-ttu-id="6d17f-128">Mapowanie sieci jest tworzony między sieciami wirtualnymi źródłowym i docelowym i na odwrót.</span><span class="sxs-lookup"><span data-stu-id="6d17f-128">A network mapping is created between source and target virtual networks, and vice versa.</span></span>
<span data-ttu-id="6d17f-129">**Konta magazynu pamięci podręcznej**</span><span class="sxs-lookup"><span data-stu-id="6d17f-129">**Cache storage accounts**</span></span> | <span data-ttu-id="6d17f-130">Przed zmian w źródle, które maszyny wirtualne są replikowane toohello docelowe konto magazynu, są śledzone i wysłane konta magazynu pamięci podręcznej toohello w miejscu docelowym hello.</span><span class="sxs-lookup"><span data-stu-id="6d17f-130">Before changes on source VMs are replicated toohello target storage account, they are tracked and sent toohello cache storage account in hello target location.</span></span> <span data-ttu-id="6d17f-131">Dzięki temu minimalny wpływ na produkcji aplikacje działające na powitania maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="6d17f-131">This ensures minimal impact on production apps running on hello VM.</span></span>
<span data-ttu-id="6d17f-132">**Konta magazynu docelowego**</span><span class="sxs-lookup"><span data-stu-id="6d17f-132">**Target storage accounts**</span></span>  | <span data-ttu-id="6d17f-133">Konta magazynu w hello docelowej lokalizacji toowhich hello dane są replikowane.</span><span class="sxs-lookup"><span data-stu-id="6d17f-133">Storage accounts in hello target location toowhich hello data is replicated.</span></span>
<span data-ttu-id="6d17f-134">**Docelowy zestawów dostępności**</span><span class="sxs-lookup"><span data-stu-id="6d17f-134">**Target availability sets**</span></span>  | <span data-ttu-id="6d17f-135">Zestawy dostępności w których hello replikowane maszyny wirtualne znajdują się po pracy awaryjnej.</span><span class="sxs-lookup"><span data-stu-id="6d17f-135">Availability sets in which hello replicated VMs are located after failover.</span></span>

### <a name="step-2"></a><span data-ttu-id="6d17f-136">Krok 2</span><span class="sxs-lookup"><span data-stu-id="6d17f-136">Step 2</span></span>

<span data-ttu-id="6d17f-137">Ponieważ replikacja jest włączona, hello rozszerzenia usługi Site Recovery usługi mobilności jest automatycznie instalowany na powitania maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="6d17f-137">As replication is enabled, hello Site Recovery extension Mobility service is automatically installed on hello VM.</span></span> <span data-ttu-id="6d17f-138">występuje Hello następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="6d17f-138">hello following occurs:</span></span>

1. <span data-ttu-id="6d17f-139">Witaj maszyny Wirtualnej jest zarejestrowany z usługą Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="6d17f-139">hello VM is registered with Site Recovery.</span></span>

2. <span data-ttu-id="6d17f-140">Ciągła replikacja jest skonfigurowana dla hello maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="6d17f-140">Continuous replication is configured for hello VM.</span></span> <span data-ttu-id="6d17f-141">Zapisuje dane na powitania maszyny Wirtualnej dyski są stale toohello konta magazynu pamięci podręcznej w lokalizacji źródłowej hello transferu.</span><span class="sxs-lookup"><span data-stu-id="6d17f-141">Data writes on hello VM disks are continuously transferred toohello cache storage account in hello source location.</span></span>

   ![Włącz proces replikacji, krok 2](./media/site-recovery-azure-to-azure-architecture/enable-replication-step-2.png)

   >[!IMPORTANT]
   > <span data-ttu-id="6d17f-143">Usługa Site Recovery nigdy nie musi toohello przychodzących połączeń maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="6d17f-143">Site Recovery never needs inbound connectivity toohello VM.</span></span> <span data-ttu-id="6d17f-144">Witaj maszyny Wirtualnej musi tylko adresy IP/adresy URL usługi odzyskiwania tooSite łączność wychodząca, adresy IP/adresy URL uwierzytelniania usługi Office 365 i adresy IP konta magazynu pamięci podręcznej.</span><span class="sxs-lookup"><span data-stu-id="6d17f-144">hello VM needs only outbound connectivity tooSite Recovery service URLs/IP addresses, Office 365 authentication URLs/IP addresses, and cache storage account IP addresses.</span></span> <span data-ttu-id="6d17f-145">Aby uzyskać więcej informacji, zobacz hello [sieci wskazówki dotyczące replikowanie maszyn wirtualnych platformy Azure](site-recovery-azure-to-azure-networking-guidance.md) artykułu.</span><span class="sxs-lookup"><span data-stu-id="6d17f-145">For more information, see hello [Networking guidance for replicating Azure virtual machines](site-recovery-azure-to-azure-networking-guidance.md) article.</span></span>

## <a name="continuous-replication-process"></a><span data-ttu-id="6d17f-146">Proces replikacji ciągłej</span><span class="sxs-lookup"><span data-stu-id="6d17f-146">Continuous replication process</span></span>

<span data-ttu-id="6d17f-147">Po replikacji ciągłej działa, dysk, który zapisuje są natychmiast przekazywane konta magazynu pamięci podręcznej toohello.</span><span class="sxs-lookup"><span data-stu-id="6d17f-147">After continuous replication is working, disk writes are immediately transferred toohello cache storage account.</span></span> <span data-ttu-id="6d17f-148">Usługa Site Recovery przetwarza dane hello i wysyła je toohello docelowe konto magazynu.</span><span class="sxs-lookup"><span data-stu-id="6d17f-148">Site Recovery processes hello data and sends it toohello target storage account.</span></span> <span data-ttu-id="6d17f-149">Po przetworzeniu danych hello punkty odzyskiwania są generowane w hello docelowe konto magazynu, co kilka minut.</span><span class="sxs-lookup"><span data-stu-id="6d17f-149">After hello data is processed, recovery points are generated in hello target storage account every few minutes.</span></span>

## <a name="failover-process"></a><span data-ttu-id="6d17f-150">Proces trybu failover</span><span class="sxs-lookup"><span data-stu-id="6d17f-150">Failover process</span></span>

<span data-ttu-id="6d17f-151">Po zainicjowaniu tryb failover maszyny wirtualne są tworzone w hello docelowa grupa zasobów, wirtualnych sieci docelowej, podsieci docelowej powitalne i hello docelowego zestawu dostępności.</span><span class="sxs-lookup"><span data-stu-id="6d17f-151">When you initiate a failover, hello VMs are created in hello target resource group, target virtual network, target subnet, and hello target availability set.</span></span> <span data-ttu-id="6d17f-152">Podczas pracy awaryjnej można użyć dowolnego punktu odzyskiwania.</span><span class="sxs-lookup"><span data-stu-id="6d17f-152">During a failover, you can use any recovery point.</span></span>

![Proces trybu failover](./media/site-recovery-azure-to-azure-architecture/failover.png)

## <a name="next-steps"></a><span data-ttu-id="6d17f-154">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="6d17f-154">Next steps</span></span>

- <span data-ttu-id="6d17f-155">Dowiedz się więcej o [sieci](site-recovery-azure-to-azure-networking-guidance.md) replikacji maszyny Wirtualnej platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="6d17f-155">Learn about [networking](site-recovery-azure-to-azure-networking-guidance.md) for Azure VM replication.</span></span>
- <span data-ttu-id="6d17f-156">Wykonaj przewodnik zbyt[replikowanie maszyn wirtualnych Azure.](site-recovery-azure-to-azure.md)</span><span class="sxs-lookup"><span data-stu-id="6d17f-156">Follow a walkthrough too[replicate Azure VMs.](site-recovery-azure-to-azure.md)</span></span>
