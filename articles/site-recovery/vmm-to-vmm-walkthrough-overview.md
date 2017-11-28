---
title: "aaaReplicate maszyn wirtualnych funkcji Hyper-V tooa lokacja dodatkowa programu VMM z usługą Azure Site Recovery | Dokumentacja firmy Microsoft"
description: "Zawiera omówienie replikowania maszyn wirtualnych funkcji Hyper-V tooa lokacja dodatkowa programu VMM przy użyciu hello portalu Azure."
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: jwhit
editor: 
ms.assetid: 476ca82a-8f5c-4498-9dcf-e1011d60ed59
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/27/2017
ms.author: raynew
ms.openlocfilehash: 90e44bfc2237dfa7646fb2b7b1e533a7f6d83c50
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="replicate-hyper-v-virtual-machines-in-vmm-clouds-tooa-secondary-vmm-site"></a><span data-ttu-id="466bd-103">Replikowanie maszyn wirtualnych funkcji Hyper-V w VMM chmur tooa lokacja dodatkowa programu VMM</span><span class="sxs-lookup"><span data-stu-id="466bd-103">Replicate Hyper-V virtual machines in VMM clouds tooa secondary VMM site</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="466bd-104">Witryna Azure Portal</span><span class="sxs-lookup"><span data-stu-id="466bd-104">Azure portal</span></span>](site-recovery-vmm-to-vmm.md)
> * [<span data-ttu-id="466bd-105">Portal klasyczny</span><span class="sxs-lookup"><span data-stu-id="466bd-105">Classic portal</span></span>](site-recovery-vmm-to-vmm-classic.md)
> * [<span data-ttu-id="466bd-106">Program PowerShell — model usługi Resource Manager</span><span class="sxs-lookup"><span data-stu-id="466bd-106">PowerShell - Resource Manager</span></span>](site-recovery-vmm-to-vmm-powershell-resource-manager.md)
>
>

<span data-ttu-id="466bd-107">Ten artykuł zawiera omówienie hello kroki wymagane tooreplicate maszynach wirtualnych funkcji Hyper-V (VM) zarządzane w chmurach programu System Center Virtual Machine Manager (VMM), lokalizacji dodatkowej VMM tooa lokalnymi przy użyciu [usługi Azure Site Recovery](site-recovery-overview.md)w hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="466bd-107">This article provides an overview of hello steps required tooreplicate on-premises Hyper-V virtual machines (VMs) managed in System Center Virtual Machine Manager (VMM) clouds, tooa secondary VMM location, using [Azure Site Recovery](site-recovery-overview.md) in hello Azure portal.</span></span>

<span data-ttu-id="466bd-108">Po przeczytaniu tego artykułu, post wszelkie komentarze u dołu hello, lub na powitania [Forum usług odzyskiwania Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="466bd-108">After reading this article, post any comments at hello bottom, or on hello [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>


## <a name="step-1-review-hello-scenario-architecture"></a><span data-ttu-id="466bd-109">Krok 1: Przejrzyj hello architektura scenariusza</span><span class="sxs-lookup"><span data-stu-id="466bd-109">Step 1: Review hello scenario architecture</span></span>

<span data-ttu-id="466bd-110">Przed rozpoczęciem wdrażania, przejrzyj architektura scenariusza hello i upewnij się, że znasz wszystkie składniki hello należy toodeploy.</span><span class="sxs-lookup"><span data-stu-id="466bd-110">Before you start deployment, review hello scenario architecture, and make sure that you understand all hello components you need toodeploy.</span></span>

<span data-ttu-id="466bd-111">Przejdź za[krok 1: Przejrzyj architektura hello](vmm-to-vmm-walkthrough-architecture.md).</span><span class="sxs-lookup"><span data-stu-id="466bd-111">Go too[Step 1: Review hello architecture](vmm-to-vmm-walkthrough-architecture.md).</span></span>

## <a name="step-2-review-prerequisites-and-limitations"></a><span data-ttu-id="466bd-112">Krok 2: Sprawdź wymagania wstępne i ograniczenia</span><span class="sxs-lookup"><span data-stu-id="466bd-112">Step 2: Review prerequisites and limitations</span></span>

<span data-ttu-id="466bd-113">Upewnij się, sprawdź wymagania wstępne dotyczące wdrażania hello i ograniczenia.</span><span class="sxs-lookup"><span data-stu-id="466bd-113">Make sure that you understand hello deployment prerequisites and limitations.</span></span>

<span data-ttu-id="466bd-114">**Wymagania wstępne platformy Azure**: potrzebujesz subskrypcji Microsoft Azure i usług odzyskiwania Azure magazyn, tooorchestrate i zarządzać replikacją.</span><span class="sxs-lookup"><span data-stu-id="466bd-114">**Azure prerequisites**: You need a Microsoft Azure subscription, and Azure Recovery Services vault, tooorchestrate and manage replication.</span></span>
<span data-ttu-id="466bd-115">**Serwery lokalne, VMM i hosty funkcji Hyper-V**: Upewnij się, że serwery VMM i hosty funkcji Hyper-V są zgodne i przygotowania się do wdrażania usługi Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="466bd-115">**On-premises VMM servers and Hyper-V hosts**: Make sure that VMM servers and Hyper-V hosts are compliant and prepared for Site Recovery deployment.</span></span>

<span data-ttu-id="466bd-116">Przejdź za[krok 2: Sprawdź wymagania wstępne i ograniczenia](vmm-to-vmm-walkthrough-prerequisites.md).</span><span class="sxs-lookup"><span data-stu-id="466bd-116">Go too[Step 2: Verify prerequisites and limitations](vmm-to-vmm-walkthrough-prerequisites.md).</span></span>

## <a name="step-3-plan-networking"></a><span data-ttu-id="466bd-117">Krok 3: Planowanie sieci</span><span class="sxs-lookup"><span data-stu-id="466bd-117">Step 3: Plan networking</span></span>

<span data-ttu-id="466bd-118">Należy toodo niektórych tooensure skonfigurowanie mapowania sieci między sieciami maszyny Wirtualnej VMM podczas wdrażania scenariusza hello do planowania sieci.</span><span class="sxs-lookup"><span data-stu-id="466bd-118">You need toodo some network planning tooensure that you can configure network mapping between VMM VM networks when you deploy hello scenario.</span></span>

<span data-ttu-id="466bd-119">Przejdź za[krok 3: Planowanie sieci](vmm-to-vmm-walkthrough-network.md).</span><span class="sxs-lookup"><span data-stu-id="466bd-119">Go too[Step 3: Plan networking](vmm-to-vmm-walkthrough-network.md).</span></span>


## <a name="step-4-prepare-vmm-and-hyper-v"></a><span data-ttu-id="466bd-120">Krok 4: Przygotowanie VMM i funkcji Hyper-V</span><span class="sxs-lookup"><span data-stu-id="466bd-120">Step 4: Prepare VMM and Hyper-V</span></span>

<span data-ttu-id="466bd-121">Przygotowanie hello serwery VMM i hosty funkcji Hyper-V do wdrażania usługi Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="466bd-121">Prepare hello VMM servers and Hyper-V hosts for Site Recovery deployment.</span></span>

<span data-ttu-id="466bd-122">Przejdź za[krok 4: Przygotowanie serwerów lokalnych](vmm-to-vmm-walkthrough-vmm-hyper-v.md).</span><span class="sxs-lookup"><span data-stu-id="466bd-122">Go too[Step 4: Prepare on-premises servers](vmm-to-vmm-walkthrough-vmm-hyper-v.md).</span></span>

## <a name="step-5-set-up-a-vault"></a><span data-ttu-id="466bd-123">Krok 5: Konfigurowanie magazynu</span><span class="sxs-lookup"><span data-stu-id="466bd-123">Step 5: Set up a vault</span></span>

<span data-ttu-id="466bd-124">Konfigurowanie magazynu usług odzyskiwania.</span><span class="sxs-lookup"><span data-stu-id="466bd-124">Set up a Recovery Services vault.</span></span> <span data-ttu-id="466bd-125">Magazyn Hello zawiera ustawienia konfiguracji i organizuje replikację.</span><span class="sxs-lookup"><span data-stu-id="466bd-125">hello vault contains configuration settings, and orchestrates replication.</span></span>

<span data-ttu-id="466bd-126">[Krok 5: Konfigurowanie magazynu](vmm-to-vmm-walkthrough-create-vault.md).</span><span class="sxs-lookup"><span data-stu-id="466bd-126">[Step 5: Set up a vault](vmm-to-vmm-walkthrough-create-vault.md).</span></span>

## <a name="step-6-set-up-source-and-target-settings"></a><span data-ttu-id="466bd-127">Krok 6: Konfigurowanie ustawień źródłowa i docelowa</span><span class="sxs-lookup"><span data-stu-id="466bd-127">Step 6: Set up source and target settings</span></span>

<span data-ttu-id="466bd-128">Konfigurowanie hello lokalizacja źródłowa i docelowa replikacji programu VMM.</span><span class="sxs-lookup"><span data-stu-id="466bd-128">Set up hello source and target replication VMM locations.</span></span> <span data-ttu-id="466bd-129">Dodaj magazyn toohello serwery VMM hello i pobierane pliki instalacyjne hello składników usługi Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="466bd-129">Add hello VMM servers toohello vault, and download hello installation files for Site Recovery components.</span></span> <span data-ttu-id="466bd-130">Uruchom Instalatora dostawcy usługi Azure Site Recovery na serwerze VMM hello.</span><span class="sxs-lookup"><span data-stu-id="466bd-130">Run Azure Site Recovery Provider setup on hello VMM server.</span></span> <span data-ttu-id="466bd-131">Instalator instaluje hello dostawcy na serwerze VMM hello i rejestruje hello serwer w magazynie hello.</span><span class="sxs-lookup"><span data-stu-id="466bd-131">Setup installs hello Provider on hello VMM server, and registers hello server in hello vault.</span></span> <span data-ttu-id="466bd-132">Należy zainstalować agenta usług odzyskiwania Microsoft hello na każdym hoście funkcji Hyper-V.</span><span class="sxs-lookup"><span data-stu-id="466bd-132">You install hello Microsoft Recovery Services agent on each Hyper-V host.</span></span>

<span data-ttu-id="466bd-133">Przejdź za[krok 6: Konfigurowanie ustawień źródłowa i docelowa hello](vmm-to-vmm-walkthrough-source-target.md).</span><span class="sxs-lookup"><span data-stu-id="466bd-133">Go too[Step 6: Set up hello source and target settings](vmm-to-vmm-walkthrough-source-target.md).</span></span>

## <a name="step-7-configure-network-mapping"></a><span data-ttu-id="466bd-134">Krok 7. Konfigurowanie mapowania sieci</span><span class="sxs-lookup"><span data-stu-id="466bd-134">Step 7: Configure network mapping</span></span>

<span data-ttu-id="466bd-135">Mapowanie sieci maszyny Wirtualnej programu VMM w hello lokalizacja źródłowa i docelowa.</span><span class="sxs-lookup"><span data-stu-id="466bd-135">Map VMM VM networks in hello source and target locations.</span></span> <span data-ttu-id="466bd-136">Po przejściu w tryb failover maszyny wirtualne są tworzone w sieci docelowej hello tego toohello mapy źródłowej sieci maszyny Wirtualnej w których hello znajduje się źródło maszyny Wirtualnej funkcji Hyper-V.</span><span class="sxs-lookup"><span data-stu-id="466bd-136">After failover, VMs are created in hello target network that maps toohello source VM network in which hello source Hyper-V VM is located.</span></span>

<span data-ttu-id="466bd-137">Przejdź za[kroku 7: Konfigurowanie mapowania sieci](vmm-to-vmm-walkthrough-network-mapping.md).</span><span class="sxs-lookup"><span data-stu-id="466bd-137">Go too[Step 7: Configure network mapping](vmm-to-vmm-walkthrough-network-mapping.md).</span></span>


## <a name="step-8-set-up-a-replication-policy"></a><span data-ttu-id="466bd-138">Krok 8: Konfigurowanie zasad replikacji</span><span class="sxs-lookup"><span data-stu-id="466bd-138">Step 8: Set up a replication policy</span></span>

<span data-ttu-id="466bd-139">Określ, jak będą replikowane maszyny wirtualne między lokacjami programu VMM.</span><span class="sxs-lookup"><span data-stu-id="466bd-139">Specify how  VMs will be replicated between VMM locations.</span></span>

<span data-ttu-id="466bd-140">Przejdź za[krok 8: Skonfiguruj zasady replikacji](vmm-to-vmm-walkthrough-replication.md).</span><span class="sxs-lookup"><span data-stu-id="466bd-140">Go too[Step 8: Set up a replication policy](vmm-to-vmm-walkthrough-replication.md).</span></span>


## <a name="step-9-enable-replication-for-vms"></a><span data-ttu-id="466bd-141">Krok 9: Włączanie replikacji maszyn wirtualnych</span><span class="sxs-lookup"><span data-stu-id="466bd-141">Step 9: Enable replication for VMs</span></span>

<span data-ttu-id="466bd-142">Wybierz maszyny wirtualne hello ma tooreplicate.</span><span class="sxs-lookup"><span data-stu-id="466bd-142">Select hello VMs you want tooreplicate.</span></span> <span data-ttu-id="466bd-143">Włączanie maszyny Wirtualnej dla replikacji wyzwalaczy hello replikacji początkowej toohello dodatkowej lokacji, następuje replikacja różnicowa trwającą.</span><span class="sxs-lookup"><span data-stu-id="466bd-143">Enabling a VM for replication triggers hello initial replication toohello secondary site, followed by ongoing delta replication.</span></span>

<span data-ttu-id="466bd-144">Przejdź za[krok 9: Włączanie replikacji](vmm-to-vmm-walkthrough-enable-replication.md).</span><span class="sxs-lookup"><span data-stu-id="466bd-144">Go too[Step 9: Enable replication](vmm-to-vmm-walkthrough-enable-replication.md).</span></span>


## <a name="step-10-run-a-test-failover"></a><span data-ttu-id="466bd-145">Krok 10: Uruchom test trybu failover</span><span class="sxs-lookup"><span data-stu-id="466bd-145">Step 10: Run a test failover</span></span>

<span data-ttu-id="466bd-146">Uruchom test toomake trybu failover, się, że wszystko działa zgodnie z oczekiwaniami.</span><span class="sxs-lookup"><span data-stu-id="466bd-146">Run a test failover toomake sure everything's working as expected.</span></span>

<span data-ttu-id="466bd-147">Przejdź za[kroku 10: testować tryb failover](vmm-to-vmm-walkthrough-test-failover.md).</span><span class="sxs-lookup"><span data-stu-id="466bd-147">Go too[Step 10: Run a test failover](vmm-to-vmm-walkthrough-test-failover.md).</span></span>
