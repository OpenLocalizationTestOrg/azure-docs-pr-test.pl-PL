---
title: "Jak działa replikacja maszyny wirtualnej platformy Azure między regiony platformy Azure w usłudze Azure Site Recovery?  | Microsoft Docs"
description: "Ten artykuł zawiera omówienie składników i architektury używane podczas replikowania maszyn wirtualnych platformy Azure między regiony platformy Azure przy użyciu usługi Azure Site Recovery."
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
ms.openlocfilehash: ec397eaeda963f257d1bd996f1f57189bcde17ca
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="how-does-azure-vm-replication-work-in-site-recovery"></a><span data-ttu-id="67456-104">Jak działa replikacja maszyny Wirtualnej platformy Azure w usłudze Site Recovery?</span><span class="sxs-lookup"><span data-stu-id="67456-104">How does Azure VM replication work in Site Recovery?</span></span>


<span data-ttu-id="67456-105">W tym artykule opisano składniki i procesy zaangażowane w replikacji i odzyskiwania maszyn wirtualnych platformy Azure (maszyn wirtualnych) z jednego regionu do drugiego za pomocą [usługi Azure Site Recovery](site-recovery-overview.md) usługi.</span><span class="sxs-lookup"><span data-stu-id="67456-105">This article describes the components and processes involved in replicating and recovering Azure virtual machines (VMs) from one region to another by using the [Azure Site Recovery](site-recovery-overview.md) service.</span></span>

>[!NOTE]
><span data-ttu-id="67456-106">Azure replikacji maszyny Wirtualnej za pomocą usługi Site Recovery jest obecnie w przeglądzie.</span><span class="sxs-lookup"><span data-stu-id="67456-106">Azure VM replication with the Site Recovery service is currently in preview.</span></span>

<span data-ttu-id="67456-107">Wszelkie komentarze umieszczaj pod tym artykułem lub zadawaj pytania na [Forum usług Azure Recovery Services](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="67456-107">Post any comments at the bottom of this article, or ask questions in the [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>

## <a name="architectural-components"></a><span data-ttu-id="67456-108">Składniki architektury</span><span class="sxs-lookup"><span data-stu-id="67456-108">Architectural components</span></span>

<span data-ttu-id="67456-109">Poniższy diagram przedstawia ogólny widok środowiska maszyny Wirtualnej platformy Azure w określonym regionie (w tym przykładzie lokalizacji wschodnie stany USA).</span><span class="sxs-lookup"><span data-stu-id="67456-109">The following diagram provides a high-level view of an Azure VM environment in a specific region (in this example, the East US location).</span></span> <span data-ttu-id="67456-110">W środowisku maszyny Wirtualnej platformy Azure:</span><span class="sxs-lookup"><span data-stu-id="67456-110">In an Azure VM environment:</span></span>
- <span data-ttu-id="67456-111">Aplikacje mogą działać na maszynach wirtualnych z dyskami rozmieszczenie do kont magazynu.</span><span class="sxs-lookup"><span data-stu-id="67456-111">Apps can be running on VMs with disks spread across storage accounts.</span></span>
- <span data-ttu-id="67456-112">Maszyny wirtualne mogą zostać włączone w co najmniej jednej podsieci sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="67456-112">The VMs can be included in one or more subnets within a virtual network.</span></span>

![środowisko klienta](./media/site-recovery-azure-to-azure-architecture/source-environment.png)

<span data-ttu-id="67456-114">Dowiedz się więcej o wymaganiach wstępnych dotyczących wdrożenia i wymagań w [macierz obsługi](site-recovery-support-matrix-azure-to-azure.md).</span><span class="sxs-lookup"><span data-stu-id="67456-114">Learn about the deployment prerequisites and requirements in the [support matrix](site-recovery-support-matrix-azure-to-azure.md).</span></span>

## <a name="replication-process"></a><span data-ttu-id="67456-115">Proces replikacji</span><span class="sxs-lookup"><span data-stu-id="67456-115">Replication process</span></span>

### <a name="step-1"></a><span data-ttu-id="67456-116">Krok 1</span><span class="sxs-lookup"><span data-stu-id="67456-116">Step 1</span></span>

<span data-ttu-id="67456-117">Po włączeniu replikacji maszyny Wirtualnej platformy Azure w portalu Azure w region docelowy są automatycznie tworzone zasoby pokazano na poniższym diagramie i tabeli.</span><span class="sxs-lookup"><span data-stu-id="67456-117">When you enable Azure VM replication in the Azure portal, the resources shown in the following diagram and table are automatically created in the target region.</span></span> <span data-ttu-id="67456-118">Domyślnie zasoby są tworzone zgodnie z ustawieniami region źródła.</span><span class="sxs-lookup"><span data-stu-id="67456-118">By default, resources are created based on source region settings.</span></span> <span data-ttu-id="67456-119">Można dostosować ustawienia obiektu docelowego, zgodnie z wymaganiami.</span><span class="sxs-lookup"><span data-stu-id="67456-119">You can customize the target settings as required.</span></span> <span data-ttu-id="67456-120">[Dowiedz się więcej](site-recovery-replicate-azure-to-azure.md).</span><span class="sxs-lookup"><span data-stu-id="67456-120">[Learn more](site-recovery-replicate-azure-to-azure.md).</span></span>

![Włącz proces replikacji, krok 1](./media/site-recovery-azure-to-azure-architecture/enable-replication-step-1.png)

<span data-ttu-id="67456-122">**Zasób**</span><span class="sxs-lookup"><span data-stu-id="67456-122">**Resource**</span></span> | <span data-ttu-id="67456-123">**Szczegóły**</span><span class="sxs-lookup"><span data-stu-id="67456-123">**Details**</span></span>
--- | ---
<span data-ttu-id="67456-124">**Docelowa grupa zasobów**</span><span class="sxs-lookup"><span data-stu-id="67456-124">**Target resource group**</span></span> | <span data-ttu-id="67456-125">Grupa zasobów replikowane maszyny wirtualne należą po pracy awaryjnej.</span><span class="sxs-lookup"><span data-stu-id="67456-125">The resource group to which replicated VMs belong after failover.</span></span>
<span data-ttu-id="67456-126">**Docelowy sieci wirtualnej**</span><span class="sxs-lookup"><span data-stu-id="67456-126">**Target virtual network**</span></span> | <span data-ttu-id="67456-127">Sieć wirtualna, w którym replikowanych maszyn wirtualnych znajdują się po pracy awaryjnej.</span><span class="sxs-lookup"><span data-stu-id="67456-127">The virtual network in which replicated VMs are located after failover.</span></span> <span data-ttu-id="67456-128">Mapowanie sieci jest tworzony między sieciami wirtualnymi źródłowym i docelowym i na odwrót.</span><span class="sxs-lookup"><span data-stu-id="67456-128">A network mapping is created between source and target virtual networks, and vice versa.</span></span>
<span data-ttu-id="67456-129">**Konta magazynu pamięci podręcznej**</span><span class="sxs-lookup"><span data-stu-id="67456-129">**Cache storage accounts**</span></span> | <span data-ttu-id="67456-130">Przed Replikacja zmian na maszynach wirtualnych źródłowego na docelowe konto magazynu, są one śledzone i wysyłane do konta magazynu pamięci podręcznej w lokalizacji docelowej.</span><span class="sxs-lookup"><span data-stu-id="67456-130">Before changes on source VMs are replicated to the target storage account, they are tracked and sent to the cache storage account in the target location.</span></span> <span data-ttu-id="67456-131">Dzięki temu minimalny wpływ na aplikacje produkcji działające na maszynie Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="67456-131">This ensures minimal impact on production apps running on the VM.</span></span>
<span data-ttu-id="67456-132">**Konta magazynu docelowego**</span><span class="sxs-lookup"><span data-stu-id="67456-132">**Target storage accounts**</span></span>  | <span data-ttu-id="67456-133">Konta magazynu w lokalizacji docelowej, do którego dane są replikowane.</span><span class="sxs-lookup"><span data-stu-id="67456-133">Storage accounts in the target location to which the data is replicated.</span></span>
<span data-ttu-id="67456-134">**Docelowy zestawów dostępności**</span><span class="sxs-lookup"><span data-stu-id="67456-134">**Target availability sets**</span></span>  | <span data-ttu-id="67456-135">Zestawy dostępności, której replikowanych maszyn wirtualnych znajdują się po pracy awaryjnej.</span><span class="sxs-lookup"><span data-stu-id="67456-135">Availability sets in which the replicated VMs are located after failover.</span></span>

### <a name="step-2"></a><span data-ttu-id="67456-136">Krok 2</span><span class="sxs-lookup"><span data-stu-id="67456-136">Step 2</span></span>

<span data-ttu-id="67456-137">Ponieważ replikacja jest włączona, rozszerzenia usługi Site Recovery usługa mobilności jest automatycznie instalowany na maszynie Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="67456-137">As replication is enabled, the Site Recovery extension Mobility service is automatically installed on the VM.</span></span> <span data-ttu-id="67456-138">Następujące operacje:</span><span class="sxs-lookup"><span data-stu-id="67456-138">The following occurs:</span></span>

1. <span data-ttu-id="67456-139">Maszyna wirtualna jest zarejestrowany z usługą Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="67456-139">The VM is registered with Site Recovery.</span></span>

2. <span data-ttu-id="67456-140">Ciągła replikacja jest skonfigurowana dla maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="67456-140">Continuous replication is configured for the VM.</span></span> <span data-ttu-id="67456-141">Zapisuje dane na dyskach maszyny Wirtualnej stale są przenoszone do konta magazynu pamięci podręcznej w lokalizacji źródłowej.</span><span class="sxs-lookup"><span data-stu-id="67456-141">Data writes on the VM disks are continuously transferred to the cache storage account in the source location.</span></span>

   ![Włącz proces replikacji, krok 2](./media/site-recovery-azure-to-azure-architecture/enable-replication-step-2.png)

   >[!IMPORTANT]
   > <span data-ttu-id="67456-143">Usługi Site Recovery, nigdy nie musi mieć łączność przychodzący do maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="67456-143">Site Recovery never needs inbound connectivity to the VM.</span></span> <span data-ttu-id="67456-144">Maszyna wirtualna musi mieć tylko ruchu wychodzącego łączność adresy IP/adresy URL usługi Site Recovery, adresy IP/adresy URL uwierzytelniania usługi Office 365 i adresów IP konta magazynu pamięci podręcznej.</span><span class="sxs-lookup"><span data-stu-id="67456-144">The VM needs only outbound connectivity to Site Recovery service URLs/IP addresses, Office 365 authentication URLs/IP addresses, and cache storage account IP addresses.</span></span> <span data-ttu-id="67456-145">Aby uzyskać więcej informacji, zobacz [sieci wskazówki dotyczące replikowanie maszyn wirtualnych platformy Azure](site-recovery-azure-to-azure-networking-guidance.md) artykułu.</span><span class="sxs-lookup"><span data-stu-id="67456-145">For more information, see the [Networking guidance for replicating Azure virtual machines](site-recovery-azure-to-azure-networking-guidance.md) article.</span></span>

## <a name="continuous-replication-process"></a><span data-ttu-id="67456-146">Proces replikacji ciągłej</span><span class="sxs-lookup"><span data-stu-id="67456-146">Continuous replication process</span></span>

<span data-ttu-id="67456-147">Po replikacji ciągłej działa, dysku operacje zapisu natychmiast są przenoszone do konta magazynu pamięci podręcznej.</span><span class="sxs-lookup"><span data-stu-id="67456-147">After continuous replication is working, disk writes are immediately transferred to the cache storage account.</span></span> <span data-ttu-id="67456-148">Usługa Site Recovery przetwarza dane i wysyła je do docelowe konto magazynu.</span><span class="sxs-lookup"><span data-stu-id="67456-148">Site Recovery processes the data and sends it to the target storage account.</span></span> <span data-ttu-id="67456-149">Po przetworzeniu danych punkty odzyskiwania są generowane w docelowe konto magazynu, co kilka minut.</span><span class="sxs-lookup"><span data-stu-id="67456-149">After the data is processed, recovery points are generated in the target storage account every few minutes.</span></span>

## <a name="failover-process"></a><span data-ttu-id="67456-150">Proces trybu failover</span><span class="sxs-lookup"><span data-stu-id="67456-150">Failover process</span></span>

<span data-ttu-id="67456-151">Po zainicjowaniu tryb failover maszyn wirtualnych są tworzone w docelowa grupa zasobów, wirtualne sieci docelowej, podsieci docelowej i zestawu dostępności docelowego.</span><span class="sxs-lookup"><span data-stu-id="67456-151">When you initiate a failover, the VMs are created in the target resource group, target virtual network, target subnet, and the target availability set.</span></span> <span data-ttu-id="67456-152">Podczas pracy awaryjnej można użyć dowolnego punktu odzyskiwania.</span><span class="sxs-lookup"><span data-stu-id="67456-152">During a failover, you can use any recovery point.</span></span>

![Proces trybu failover](./media/site-recovery-azure-to-azure-architecture/failover.png)

## <a name="next-steps"></a><span data-ttu-id="67456-154">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="67456-154">Next steps</span></span>

- <span data-ttu-id="67456-155">Dowiedz się więcej o [sieci](site-recovery-azure-to-azure-networking-guidance.md) replikacji maszyny Wirtualnej platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="67456-155">Learn about [networking](site-recovery-azure-to-azure-networking-guidance.md) for Azure VM replication.</span></span>
- <span data-ttu-id="67456-156">Wykonaj wskazówki do [replikowanie maszyn wirtualnych Azure.](site-recovery-azure-to-azure.md)</span><span class="sxs-lookup"><span data-stu-id="67456-156">Follow a walkthrough to [replicate Azure VMs.](site-recovery-azure-to-azure.md)</span></span>
