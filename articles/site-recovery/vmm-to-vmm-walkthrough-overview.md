---
title: "Replikowanie maszyn wirtualnych funkcji Hyper-V do lokacji dodatkowej programu VMM z usługą Azure Site Recovery | Dokumentacja firmy Microsoft"
description: "Zawiera omówienie replikowania maszyn wirtualnych funkcji Hyper-V na lokacja dodatkowa programu VMM przy użyciu portalu Azure."
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
ms.openlocfilehash: b422dd2cf23426de2f154a553b38509082536309
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="replicate-hyper-v-virtual-machines-in-vmm-clouds-to-a-secondary-vmm-site"></a><span data-ttu-id="78463-103">Replikowanie maszyn wirtualnych funkcji Hyper-V w chmurach VMM do dodatkowej lokacji programu VMM</span><span class="sxs-lookup"><span data-stu-id="78463-103">Replicate Hyper-V virtual machines in VMM clouds to a secondary VMM site</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="78463-104">Witryna Azure Portal</span><span class="sxs-lookup"><span data-stu-id="78463-104">Azure portal</span></span>](site-recovery-vmm-to-vmm.md)
> * [<span data-ttu-id="78463-105">Portal klasyczny</span><span class="sxs-lookup"><span data-stu-id="78463-105">Classic portal</span></span>](site-recovery-vmm-to-vmm-classic.md)
> * [<span data-ttu-id="78463-106">Program PowerShell — model usługi Resource Manager</span><span class="sxs-lookup"><span data-stu-id="78463-106">PowerShell - Resource Manager</span></span>](site-recovery-vmm-to-vmm-powershell-resource-manager.md)
>
>

<span data-ttu-id="78463-107">Ten artykuł zawiera omówienie kroków wymaganych do replikowania maszyn wirtualnych funkcji Hyper-V lokalnymi (VM) zarządzane w programie System Center Virtual Machine Manager (VMM) chmury do dodatkowej lokalizacji programu VMM, przy użyciu [usługi Azure Site Recovery](site-recovery-overview.md) w portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="78463-107">This article provides an overview of the steps required to replicate on-premises Hyper-V virtual machines (VMs) managed in System Center Virtual Machine Manager (VMM) clouds, to a secondary VMM location, using [Azure Site Recovery](site-recovery-overview.md) in the Azure portal.</span></span>

<span data-ttu-id="78463-108">Po przeczytaniu tego artykułu zamieść wszelkie komentarze u dołu lub na [forum usług Azure Recovery Services](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="78463-108">After reading this article, post any comments at the bottom, or on the [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>


## <a name="step-1-review-the-scenario-architecture"></a><span data-ttu-id="78463-109">Krok 1: Przejrzyj architektura scenariusza</span><span class="sxs-lookup"><span data-stu-id="78463-109">Step 1: Review the scenario architecture</span></span>

<span data-ttu-id="78463-110">Przed rozpoczęciem wdrażania, przejrzyj architektura scenariusza i upewnij się, że znasz wszystkie składniki potrzebne do wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="78463-110">Before you start deployment, review the scenario architecture, and make sure that you understand all the components you need to deploy.</span></span>

<span data-ttu-id="78463-111">Przejdź do [krok 1: Przejrzyj architektury](vmm-to-vmm-walkthrough-architecture.md).</span><span class="sxs-lookup"><span data-stu-id="78463-111">Go to [Step 1: Review the architecture](vmm-to-vmm-walkthrough-architecture.md).</span></span>

## <a name="step-2-review-prerequisites-and-limitations"></a><span data-ttu-id="78463-112">Krok 2: Sprawdź wymagania wstępne i ograniczenia</span><span class="sxs-lookup"><span data-stu-id="78463-112">Step 2: Review prerequisites and limitations</span></span>

<span data-ttu-id="78463-113">Upewnij się, że rozumiesz wymagania wstępne dotyczące wdrażania i ograniczenia.</span><span class="sxs-lookup"><span data-stu-id="78463-113">Make sure that you understand the deployment prerequisites and limitations.</span></span>

<span data-ttu-id="78463-114">**Wymagania wstępne platformy Azure**: potrzebujesz subskrypcji Microsoft Azure, a magazyn usług odzyskiwania Azure, do organizowania replikacji.</span><span class="sxs-lookup"><span data-stu-id="78463-114">**Azure prerequisites**: You need a Microsoft Azure subscription, and Azure Recovery Services vault, to orchestrate and manage replication.</span></span>
<span data-ttu-id="78463-115">**Serwery lokalne, VMM i hosty funkcji Hyper-V**: Upewnij się, że serwery VMM i hosty funkcji Hyper-V są zgodne i przygotowania się do wdrażania usługi Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="78463-115">**On-premises VMM servers and Hyper-V hosts**: Make sure that VMM servers and Hyper-V hosts are compliant and prepared for Site Recovery deployment.</span></span>

<span data-ttu-id="78463-116">Przejdź do [krok 2: Sprawdź wymagania wstępne i ograniczenia](vmm-to-vmm-walkthrough-prerequisites.md).</span><span class="sxs-lookup"><span data-stu-id="78463-116">Go to [Step 2: Verify prerequisites and limitations](vmm-to-vmm-walkthrough-prerequisites.md).</span></span>

## <a name="step-3-plan-networking"></a><span data-ttu-id="78463-117">Krok 3: Planowanie sieci</span><span class="sxs-lookup"><span data-stu-id="78463-117">Step 3: Plan networking</span></span>

<span data-ttu-id="78463-118">Należy wykonać niektóre sieci, planowanie upewnić się, że możesz skonfigurować mapowanie sieci między sieciami maszyny Wirtualnej VMM podczas wdrażania tego scenariusza.</span><span class="sxs-lookup"><span data-stu-id="78463-118">You need to do some network planning to ensure that you can configure network mapping between VMM VM networks when you deploy the scenario.</span></span>

<span data-ttu-id="78463-119">Przejdź do [krok 3: Planowanie sieci](vmm-to-vmm-walkthrough-network.md).</span><span class="sxs-lookup"><span data-stu-id="78463-119">Go to [Step 3: Plan networking](vmm-to-vmm-walkthrough-network.md).</span></span>


## <a name="step-4-prepare-vmm-and-hyper-v"></a><span data-ttu-id="78463-120">Krok 4: Przygotowanie VMM i funkcji Hyper-V</span><span class="sxs-lookup"><span data-stu-id="78463-120">Step 4: Prepare VMM and Hyper-V</span></span>

<span data-ttu-id="78463-121">Przygotowanie serwerów programu VMM i hosty funkcji Hyper-V do wdrażania usługi Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="78463-121">Prepare the VMM servers and Hyper-V hosts for Site Recovery deployment.</span></span>

<span data-ttu-id="78463-122">Przejdź do [krok 4: Przygotowanie serwerów lokalnych](vmm-to-vmm-walkthrough-vmm-hyper-v.md).</span><span class="sxs-lookup"><span data-stu-id="78463-122">Go to [Step 4: Prepare on-premises servers](vmm-to-vmm-walkthrough-vmm-hyper-v.md).</span></span>

## <a name="step-5-set-up-a-vault"></a><span data-ttu-id="78463-123">Krok 5: Konfigurowanie magazynu</span><span class="sxs-lookup"><span data-stu-id="78463-123">Step 5: Set up a vault</span></span>

<span data-ttu-id="78463-124">Konfigurowanie magazynu usług odzyskiwania.</span><span class="sxs-lookup"><span data-stu-id="78463-124">Set up a Recovery Services vault.</span></span> <span data-ttu-id="78463-125">Magazyn zawiera ustawienia konfiguracji i aranżuje replikację.</span><span class="sxs-lookup"><span data-stu-id="78463-125">The vault contains configuration settings, and orchestrates replication.</span></span>

<span data-ttu-id="78463-126">[Krok 5: Konfigurowanie magazynu](vmm-to-vmm-walkthrough-create-vault.md).</span><span class="sxs-lookup"><span data-stu-id="78463-126">[Step 5: Set up a vault](vmm-to-vmm-walkthrough-create-vault.md).</span></span>

## <a name="step-6-set-up-source-and-target-settings"></a><span data-ttu-id="78463-127">Krok 6: Konfigurowanie ustawień źródłowa i docelowa</span><span class="sxs-lookup"><span data-stu-id="78463-127">Step 6: Set up source and target settings</span></span>

<span data-ttu-id="78463-128">Konfigurowanie lokalizacja źródłowa i docelowa replikacji programu VMM.</span><span class="sxs-lookup"><span data-stu-id="78463-128">Set up the source and target replication VMM locations.</span></span> <span data-ttu-id="78463-129">Dodawanie serwerów programu VMM w magazynie i pobierane pliki instalacyjne dla składników usługi Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="78463-129">Add the VMM servers to the vault, and download the installation files for Site Recovery components.</span></span> <span data-ttu-id="78463-130">Uruchom Instalatora dostawcy usługi Azure Site Recovery na serwerze programu VMM.</span><span class="sxs-lookup"><span data-stu-id="78463-130">Run Azure Site Recovery Provider setup on the VMM server.</span></span> <span data-ttu-id="78463-131">Instalator instaluje dostawcę na serwerze programu VMM i rejestruje serwer w magazynie.</span><span class="sxs-lookup"><span data-stu-id="78463-131">Setup installs the Provider on the VMM server, and registers the server in the vault.</span></span> <span data-ttu-id="78463-132">Agent usług odzyskiwania Microsoft należy zainstalować na każdym hoście funkcji Hyper-V.</span><span class="sxs-lookup"><span data-stu-id="78463-132">You install the Microsoft Recovery Services agent on each Hyper-V host.</span></span>

<span data-ttu-id="78463-133">Przejdź do [krok 6: Konfigurowanie ustawień źródłowa i docelowa](vmm-to-vmm-walkthrough-source-target.md).</span><span class="sxs-lookup"><span data-stu-id="78463-133">Go to [Step 6: Set up the source and target settings](vmm-to-vmm-walkthrough-source-target.md).</span></span>

## <a name="step-7-configure-network-mapping"></a><span data-ttu-id="78463-134">Krok 7. Konfigurowanie mapowania sieci</span><span class="sxs-lookup"><span data-stu-id="78463-134">Step 7: Configure network mapping</span></span>

<span data-ttu-id="78463-135">Mapowanie sieci maszyny Wirtualnej programu VMM w lokalizacji źródłowej i docelowej.</span><span class="sxs-lookup"><span data-stu-id="78463-135">Map VMM VM networks in the source and target locations.</span></span> <span data-ttu-id="78463-136">Po przejściu w tryb failover maszyny wirtualne są tworzone w sieci docelowej, który jest mapowany na źródłowej sieci maszyny Wirtualnej, w którym znajduje się źródłowej maszyny Wirtualnej funkcji Hyper-V.</span><span class="sxs-lookup"><span data-stu-id="78463-136">After failover, VMs are created in the target network that maps to the source VM network in which the source Hyper-V VM is located.</span></span>

<span data-ttu-id="78463-137">Przejdź do [kroku 7: Konfigurowanie mapowania sieci](vmm-to-vmm-walkthrough-network-mapping.md).</span><span class="sxs-lookup"><span data-stu-id="78463-137">Go to [Step 7: Configure network mapping](vmm-to-vmm-walkthrough-network-mapping.md).</span></span>


## <a name="step-8-set-up-a-replication-policy"></a><span data-ttu-id="78463-138">Krok 8: Konfigurowanie zasad replikacji</span><span class="sxs-lookup"><span data-stu-id="78463-138">Step 8: Set up a replication policy</span></span>

<span data-ttu-id="78463-139">Określ, jak będą replikowane maszyny wirtualne między lokacjami programu VMM.</span><span class="sxs-lookup"><span data-stu-id="78463-139">Specify how  VMs will be replicated between VMM locations.</span></span>

<span data-ttu-id="78463-140">Przejdź do [krok 8: Skonfiguruj zasady replikacji](vmm-to-vmm-walkthrough-replication.md).</span><span class="sxs-lookup"><span data-stu-id="78463-140">Go to [Step 8: Set up a replication policy](vmm-to-vmm-walkthrough-replication.md).</span></span>


## <a name="step-9-enable-replication-for-vms"></a><span data-ttu-id="78463-141">Krok 9: Włączanie replikacji maszyn wirtualnych</span><span class="sxs-lookup"><span data-stu-id="78463-141">Step 9: Enable replication for VMs</span></span>

<span data-ttu-id="78463-142">Wybierz maszyny wirtualne mają być replikowane.</span><span class="sxs-lookup"><span data-stu-id="78463-142">Select the VMs you want to replicate.</span></span> <span data-ttu-id="78463-143">Włączanie replikacji maszyny Wirtualnej wyzwala na lokacji dodatkowej, następuje replikacja różnicowa trwającej replikacji początkowej.</span><span class="sxs-lookup"><span data-stu-id="78463-143">Enabling a VM for replication triggers the initial replication to the secondary site, followed by ongoing delta replication.</span></span>

<span data-ttu-id="78463-144">Przejdź do [krok 9: Włączanie replikacji](vmm-to-vmm-walkthrough-enable-replication.md).</span><span class="sxs-lookup"><span data-stu-id="78463-144">Go to [Step 9: Enable replication](vmm-to-vmm-walkthrough-enable-replication.md).</span></span>


## <a name="step-10-run-a-test-failover"></a><span data-ttu-id="78463-145">Krok 10: Uruchom test trybu failover</span><span class="sxs-lookup"><span data-stu-id="78463-145">Step 10: Run a test failover</span></span>

<span data-ttu-id="78463-146">Uruchom testowanie trybu failover, aby upewnić się, że wszystko działa zgodnie z oczekiwaniami.</span><span class="sxs-lookup"><span data-stu-id="78463-146">Run a test failover to make sure everything's working as expected.</span></span>

<span data-ttu-id="78463-147">Przejdź do [kroku 10: testować tryb failover](vmm-to-vmm-walkthrough-test-failover.md).</span><span class="sxs-lookup"><span data-stu-id="78463-147">Go to [Step 10: Run a test failover](vmm-to-vmm-walkthrough-test-failover.md).</span></span>
