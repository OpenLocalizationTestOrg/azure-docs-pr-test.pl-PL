---
title: "Przegląd architektury replikacji funkcji Hyper-V do lokacji dodatkowej za pomocą usługi Azure Site Recovery | Microsoft Docs"
description: "Ten artykuł zawiera omówienie architektury używanej podczas replikowania lokalnych maszyn wirtualnych funkcji Hyper-V do lokacji dodatkowej z programem System Center VMM za pomocą usługi Azure Site Recovery."
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
ms.openlocfilehash: b78cd0d5a5395873afaddc8856004775f447e8ea
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="step-1-review-the-architecture-for-hyper-v-replication-to-a-secondary-site"></a><span data-ttu-id="a7f8b-103">Krok 1. Przegląd architektury replikacji funkcji Hyper-V do lokacji dodatkowej</span><span class="sxs-lookup"><span data-stu-id="a7f8b-103">Step 1: Review the architecture for Hyper-V replication to a secondary site</span></span>

<span data-ttu-id="a7f8b-104">Ten artykuł zawiera opis składników i procesów związanych z replikacją lokalnych maszyn wirtualnych funkcji Hyper-V w chmurach programu System Center Virtual Machine Manager (VMM) do lokacji dodatkowej z programem VMM za pomocą usługi [Azure Site Recovery](site-recovery-overview.md) w witrynie Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="a7f8b-104">This article describes the components and processes involved when replicating on-premises Hyper-V virtual machines (VMs) in System Center Virtual Machine Manager (VMM) clouds, to a secondary VMM site using the [Azure Site Recovery](site-recovery-overview.md) service in the Azure portal.</span></span>

<span data-ttu-id="a7f8b-105">Zamieść wszelkie komentarze pod tym artykułem lub na [forum usług Azure Recovery Services](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="a7f8b-105">Post any comments at the bottom of this article, or in the [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>



## <a name="architectural-components"></a><span data-ttu-id="a7f8b-106">Składniki architektury</span><span class="sxs-lookup"><span data-stu-id="a7f8b-106">Architectural components</span></span>

<span data-ttu-id="a7f8b-107">Poniżej przedstawiono wymagania dotyczące replikowania maszyn wirtualnych funkcji Hyper-V do lokacji dodatkowej z programem VMM.</span><span class="sxs-lookup"><span data-stu-id="a7f8b-107">Here's what you need for replicating Hyper-V VMs to a secondary VMM site.</span></span>

<span data-ttu-id="a7f8b-108">**Składnik**</span><span class="sxs-lookup"><span data-stu-id="a7f8b-108">**Component**</span></span> | <span data-ttu-id="a7f8b-109">**Lokalizacja**</span><span class="sxs-lookup"><span data-stu-id="a7f8b-109">**Location**</span></span> | <span data-ttu-id="a7f8b-110">**Szczegóły**</span><span class="sxs-lookup"><span data-stu-id="a7f8b-110">**Details**</span></span>
--- | --- | ---
<span data-ttu-id="a7f8b-111">**Azure**</span><span class="sxs-lookup"><span data-stu-id="a7f8b-111">**Azure**</span></span> | <span data-ttu-id="a7f8b-112">Subskrypcja na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="a7f8b-112">Subscription in Azure.</span></span> | <span data-ttu-id="a7f8b-113">Magazyn usługi Recovery Services tworzy się w subskrypcji platformy Azure, aby organizować replikację między lokalizacjami z programem VMM i nią zarządzać.</span><span class="sxs-lookup"><span data-stu-id="a7f8b-113">You create a Recovery Services vault in the Azure subscription, to orchestrate and manage replication between VMM locations.</span></span>
<span data-ttu-id="a7f8b-114">**Serwer VMM**</span><span class="sxs-lookup"><span data-stu-id="a7f8b-114">**VMM server**</span></span> | <span data-ttu-id="a7f8b-115">Potrzebujesz podstawowej i dodatkowej lokalizacji z programem VMM.</span><span class="sxs-lookup"><span data-stu-id="a7f8b-115">You need a VMM primary and secondary location.</span></span> | <span data-ttu-id="a7f8b-116">Zalecamy, aby zarówno w lokacji głównej, jak i dodatkowej znajdował się jeden serwer VMM</span><span class="sxs-lookup"><span data-stu-id="a7f8b-116">We recommend a VMM server in the primary site, and one in the secondary site</span></span> 
<span data-ttu-id="a7f8b-117">**Serwer funkcji Hyper-V**</span><span class="sxs-lookup"><span data-stu-id="a7f8b-117">**Hyper-V server**</span></span> |  <span data-ttu-id="a7f8b-118">Co najmniej jeden serwer hosta funkcji Hyper-V w głównych i dodatkowych chmurach programu VMM.</span><span class="sxs-lookup"><span data-stu-id="a7f8b-118">One or more Hyper-V host servers in the primary and secondary VMM clouds.</span></span> | <span data-ttu-id="a7f8b-119">Dane są replikowane między głównymi i dodatkowymi serwerami hosta funkcji Hyper-V za pośrednictwem sieci LAN albo sieci VPN korzystającej z protokołu Kerberos lub uwierzytelniania certyfikatu.</span><span class="sxs-lookup"><span data-stu-id="a7f8b-119">Data is replicated between the primary and secondary Hyper-V host servers over the LAN or VPN, using Kerberos or certificate authentication.</span></span>  
<span data-ttu-id="a7f8b-120">**Maszyny wirtualne funkcji Hyper-V**</span><span class="sxs-lookup"><span data-stu-id="a7f8b-120">**Hyper-V VMs**</span></span> | <span data-ttu-id="a7f8b-121">Na serwerze hosta funkcji Hyper-V.</span><span class="sxs-lookup"><span data-stu-id="a7f8b-121">On Hyper-V host server.</span></span> | <span data-ttu-id="a7f8b-122">Źródłowy serwer hosta powinien mieć co najmniej jedną maszynę wirtualną, która ma być replikowana.</span><span class="sxs-lookup"><span data-stu-id="a7f8b-122">The source host server should have at least one VM that you want to replicate.</span></span>

## <a name="replication-process"></a><span data-ttu-id="a7f8b-123">Proces replikacji</span><span class="sxs-lookup"><span data-stu-id="a7f8b-123">Replication process</span></span>

1. <span data-ttu-id="a7f8b-124">Należy skonfigurować konto platformy Azure, utworzyć magazyn usługi Recovery Services i określić elementy do replikacji.</span><span class="sxs-lookup"><span data-stu-id="a7f8b-124">You set up the Azure account, create a Recovery Services vault, and specify what you want to replicate.</span></span>
2. <span data-ttu-id="a7f8b-125">Możesz skonfigurować źródłowe i docelowe ustawienia replikacji, co obejmuje instalowanie dostawcy usługi Azure Service Recovery na serwerach VMM oraz agenta usługi Microsoft Azure Recovery Services na każdym hoście funkcji Hyper-V.</span><span class="sxs-lookup"><span data-stu-id="a7f8b-125">You configure the source and target replication settings, which includes installing the Azure Site Recovery Provider on VMM servers, and the Microsoft Azure Recovery Services agent on each Hyper-V host.</span></span>
3. <span data-ttu-id="a7f8b-126">Należy utworzyć zasady replikacji dla źródłowej chmury programu VMM.</span><span class="sxs-lookup"><span data-stu-id="a7f8b-126">You create a replication policy for the source VMM cloud.</span></span> <span data-ttu-id="a7f8b-127">Te zasady są stosowane do wszystkich maszyn wirtualnych znajdujących się na hostach w chmurze.</span><span class="sxs-lookup"><span data-stu-id="a7f8b-127">The policy is applied to all VMs located on hosts in the cloud.</span></span>
4. <span data-ttu-id="a7f8b-128">Należy włączyć replikację dla każdego programu VMM, po czym nastąpi replikacja początkowa maszyny wirtualnej zgodnie z wybranymi ustawieniami.</span><span class="sxs-lookup"><span data-stu-id="a7f8b-128">You enable replication for each VMM, and initial replication of a VM occurs in accordance with the settings you choose.</span></span>
5. <span data-ttu-id="a7f8b-129">Po replikacji początkowej rozpocznie się replikacja zmian różnicowych.</span><span class="sxs-lookup"><span data-stu-id="a7f8b-129">After initial replication, replication of delta changes begins.</span></span> <span data-ttu-id="a7f8b-130">Śledzone zmiany elementu są przechowywane w pliku hrl.</span><span class="sxs-lookup"><span data-stu-id="a7f8b-130">Tracked changes for an item are held in a .hrl file.</span></span>


![Ze środowiska lokalnego do środowiska lokalnego](./media/vmm-to-vmm-walkthrough-architecture/arch-onprem-onprem.png)

## <a name="failover-and-failback-process"></a><span data-ttu-id="a7f8b-132">Proces pracy w trybie failover i podczas powrotu po awarii</span><span class="sxs-lookup"><span data-stu-id="a7f8b-132">Failover and failback process</span></span>

1. <span data-ttu-id="a7f8b-133">Planowane lub nieplanowane przejście w tryb [failover](site-recovery-failover.md) można uruchomić między lokacjami lokalnymi.</span><span class="sxs-lookup"><span data-stu-id="a7f8b-133">You can run a planned or unplanned [failover](site-recovery-failover.md) between on-premises sites.</span></span> <span data-ttu-id="a7f8b-134">Jeśli zostanie uruchomione planowane przejście w tryb failover, źródłowe maszyny wirtualne zostaną wyłączone w celu zapewnienia, że nie będzie miała miejsca utrata danych.</span><span class="sxs-lookup"><span data-stu-id="a7f8b-134">If you run a planned failover, then source VMs are shut down to ensure no data loss.</span></span>
2. <span data-ttu-id="a7f8b-135">W tryb failover można przełączyć pojedynczą maszynę lub można utworzyć [plany odzyskiwania](site-recovery-create-recovery-plans.md), aby zarządzać trybem failover na wielu maszynach.</span><span class="sxs-lookup"><span data-stu-id="a7f8b-135">You can fail over a single machine, or create [recovery plans](site-recovery-create-recovery-plans.md) to orchestrate failover of multiple machines.</span></span>
4. <span data-ttu-id="a7f8b-136">Jeśli wykonywane jest nieplanowane przejście w tryb failover do lokacji dodatkowej, po przejściu w tryb failover na maszynach znajdujących się w lokalizacji dodatkowej nie jest włączona ochrona ani replikacja.</span><span class="sxs-lookup"><span data-stu-id="a7f8b-136">If you perform an unplanned failover to a secondary site, after the failover machines in the secondary location aren't enabled for protection or replication.</span></span> <span data-ttu-id="a7f8b-137">Jeśli dokonano planowanego przejścia w tryb failover, po przejściu w tryb failover maszyny znajdujące się w lokalizacji dodatkowej są chronione.</span><span class="sxs-lookup"><span data-stu-id="a7f8b-137">If you ran a planned failover, after the failover, machines in the secondary location are protected.</span></span>
5. <span data-ttu-id="a7f8b-138">Następnie należy zatwierdzić tryb failover, aby można było rozpocząć uzyskiwanie dostępu do obciążenia z poziomu repliki maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="a7f8b-138">Then, you commit the failover to start accessing the workload from the replica VM.</span></span>
6. <span data-ttu-id="a7f8b-139">Gdy lokacja główna będzie znowu dostępna, należy zainicjować replikację odwrotną w celu przeprowadzenia replikacji z lokacji dodatkowej do lokacji głównej.</span><span class="sxs-lookup"><span data-stu-id="a7f8b-139">When your primary site is available again, you initiate reverse replication to replicate from the secondary site to the primary.</span></span> <span data-ttu-id="a7f8b-140">Replikacja odwrotna powoduje przełączenie maszyn wirtualnych do stanu chronionego, ale aktywną lokalizacją jest nadal dodatkowe centrum danych.</span><span class="sxs-lookup"><span data-stu-id="a7f8b-140">Reverse replication brings the virtual machines into a protected state, but the secondary datacenter is still the active location.</span></span>
7. <span data-ttu-id="a7f8b-141">Aby lokacja główna stała się z powrotem lokalizacją aktywną, należy zainicjować planowane przejście w tryb failover z lokacji dodatkowej do głównej, a następnie przeprowadzić kolejną replikację odwrotną.</span><span class="sxs-lookup"><span data-stu-id="a7f8b-141">To make the primary site into the active location again, you initiate a planned failover from secondary to primary, followed by another reverse replication.</span></span>



## <a name="next-steps"></a><span data-ttu-id="a7f8b-142">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="a7f8b-142">Next steps</span></span>

<span data-ttu-id="a7f8b-143">Przejdź do części [Krok 2. Przegląd wymagań wstępnych i ograniczeń](vmm-to-vmm-walkthrough-prerequisites.md).</span><span class="sxs-lookup"><span data-stu-id="a7f8b-143">Go to [Step 2: Review the prerequisites and limitations](vmm-to-vmm-walkthrough-prerequisites.md).</span></span>
