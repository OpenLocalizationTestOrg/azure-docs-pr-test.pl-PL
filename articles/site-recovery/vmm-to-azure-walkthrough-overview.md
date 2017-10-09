---
title: "aaaReplicate maszyn wirtualnych funkcji Hyper-V w programie VMM chmur tooAzure z usługą Azure Site Recovery | Dokumentacja firmy Microsoft"
description: "Zawiera omówienie replikowania maszyn wirtualnych funkcji Hyper-V w tooAzure chmur programu VMM przy użyciu usługi Azure Site Recovery hello"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: 8e7d868e-00f3-4e8b-9a9e-f23365abf6ac
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/14/2017
ms.author: raynew
ms.openlocfilehash: d6f729a49cc86ea07bebc4d7266fd7b58b3998f7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="replicate-hyper-v-virtual-machines-in-vmm-clouds-tooazure-using-site-recovery-in-hello-azure-portal"></a><span data-ttu-id="fd2ba-103">Replikowanie maszyn wirtualnych funkcji Hyper-V w tooAzure chmur programu VMM przy użyciu usługi Site Recovery w portalu Azure hello</span><span class="sxs-lookup"><span data-stu-id="fd2ba-103">Replicate Hyper-V virtual machines in VMM clouds tooAzure using Site Recovery in hello Azure portal</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="fd2ba-104">Witryna Azure Portal</span><span class="sxs-lookup"><span data-stu-id="fd2ba-104">Azure portal</span></span>](site-recovery-vmm-to-azure.md)
> * [<span data-ttu-id="fd2ba-105">Klasyczny portal Azure</span><span class="sxs-lookup"><span data-stu-id="fd2ba-105">Azure classic</span></span>](site-recovery-vmm-to-azure-classic.md)
> * [<span data-ttu-id="fd2ba-106">Program PowerShell — model usługi Resource Manager</span><span class="sxs-lookup"><span data-stu-id="fd2ba-106">PowerShell Resource Manager</span></span>](site-recovery-vmm-to-azure-powershell-resource-manager.md)
> * [<span data-ttu-id="fd2ba-107">PowerShell — model klasyczny</span><span class="sxs-lookup"><span data-stu-id="fd2ba-107">PowerShell classic</span></span>](site-recovery-deploy-with-powershell.md)


<span data-ttu-id="fd2ba-108">Ten artykuł zawiera omówienie tooreplicate wymagane kroki hello lokalnych maszyn wirtualnych funkcji Hyper-V (VM) zarządzanych w tooAzure chmur programu System Center Virtual Machine Manager (VMM), za pomocą hello [usługi Azure Site Recovery](site-recovery-overview.md) w Witaj portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="fd2ba-108">This article provides an overview of hello steps required tooreplicate on-premises Hyper-V virtual machines (VMs) managed in System Center Virtual Machine Manager (VMM) clouds tooAzure, using hello [Azure Site Recovery](site-recovery-overview.md) service in hello Azure portal.</span></span>

<span data-ttu-id="fd2ba-109">Po przeczytaniu tego artykułu, post wszelkie komentarze u dołu hello, lub na powitania [Forum usług odzyskiwania Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="fd2ba-109">After reading this article, post any comments at hello bottom, or on hello [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>


## <a name="step-1-review-hello-scenario-architecture"></a><span data-ttu-id="fd2ba-110">Krok 1: Przejrzyj hello architektura scenariusza</span><span class="sxs-lookup"><span data-stu-id="fd2ba-110">Step 1: Review hello scenario architecture</span></span>

<span data-ttu-id="fd2ba-111">Przed rozpoczęciem wdrażania, przejrzyj architektura scenariusza hello i upewnij się, że znasz wszystkie składniki hello należy toodeploy.</span><span class="sxs-lookup"><span data-stu-id="fd2ba-111">Before you start deployment, review hello scenario architecture, and make sure that you understand all hello components you need toodeploy.</span></span>

<span data-ttu-id="fd2ba-112">Przejdź do zbyt[krok 1: Przejrzyj hello architektury](vmm-to-azure-walkthrough-architecture.md)</span><span class="sxs-lookup"><span data-stu-id="fd2ba-112">Go too[Step 1: Review hello architecture](vmm-to-azure-walkthrough-architecture.md)</span></span>

## <a name="step-2-review-prerequisites-and-limitations"></a><span data-ttu-id="fd2ba-113">Krok 2: Sprawdź wymagania wstępne i ograniczenia</span><span class="sxs-lookup"><span data-stu-id="fd2ba-113">Step 2: Review prerequisites and limitations</span></span>

<span data-ttu-id="fd2ba-114">Upewnij się, sprawdź wymagania wstępne dotyczące wdrażania hello i ograniczenia.</span><span class="sxs-lookup"><span data-stu-id="fd2ba-114">Make sure that you understand hello deployment prerequisites and limitations.</span></span>

<span data-ttu-id="fd2ba-115">**Wymagania wstępne platformy Azure**: wymagane konto Microsoft Azure, sieci platformy Azure i kont magazynu.</span><span class="sxs-lookup"><span data-stu-id="fd2ba-115">**Azure prerequisites**: You need a Microsoft Azure account, Azure networks, and storage accounts.</span></span>
<span data-ttu-id="fd2ba-116">**Serwery lokalne, VMM i hosty funkcji Hyper-V**: Upewnij się, że serwery VMM i hosty funkcji Hyper-V są zgodne i przygotowania się do wdrażania usługi Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="fd2ba-116">**On-premises VMM servers and Hyper-V hosts**: Make sure that VMM servers and Hyper-V hosts are compliant and prepared for Site Recovery deployment.</span></span>
<span data-ttu-id="fd2ba-117">**Maszyny wirtualne replikowane**: Sprawdź, czy maszyny wirtualne mają tooreplicate spełniają wymagania dotyczące usługi Azure.</span><span class="sxs-lookup"><span data-stu-id="fd2ba-117">**Replicated VMs**: Check that VMs you want tooreplicate comply with Azure requirements.</span></span>

<span data-ttu-id="fd2ba-118">Przejdź do zbyt[krok 2: Sprawdź wymagania wstępne i ograniczenia](vmm-to-azure-walkthrough-prerequisites.md)</span><span class="sxs-lookup"><span data-stu-id="fd2ba-118">Go too[Step 2: Verify prerequisites and limitations](vmm-to-azure-walkthrough-prerequisites.md)</span></span>

## <a name="step-3-plan-capacity"></a><span data-ttu-id="fd2ba-119">Krok 3: Planowanie pojemności</span><span class="sxs-lookup"><span data-stu-id="fd2ba-119">Step 3: Plan capacity</span></span>

<span data-ttu-id="fd2ba-120">Pełne wdrożenie robimy, należy najpierw toofigure się, jakie potrzebne zasoby replikacji.</span><span class="sxs-lookup"><span data-stu-id="fd2ba-120">If you're doing a full deployment, you need toofigure out what replication resources you need.</span></span> <span data-ttu-id="fd2ba-121">Istnieje kilka z toohelp dostępne narzędzia można to zrobić.</span><span class="sxs-lookup"><span data-stu-id="fd2ba-121">There are a couple of tools available toohelp you do this.</span></span> <span data-ttu-id="fd2ba-122">Jeśli podczas wykonywania szybkiego skonfigurowania środowiska hello tootest, możesz pominąć ten krok.</span><span class="sxs-lookup"><span data-stu-id="fd2ba-122">If you're doing a quick set up tootest hello environment, you can skip this step.</span></span>

<span data-ttu-id="fd2ba-123">Przejdź do zbyt[krok 3: Planowanie pojemności](vmm-to-azure-walkthrough-capacity.md)</span><span class="sxs-lookup"><span data-stu-id="fd2ba-123">Go too[Step 3: Plan capacity](vmm-to-azure-walkthrough-capacity.md)</span></span>

## <a name="step-4-plan-networking"></a><span data-ttu-id="fd2ba-124">Krok 4: Planowanie sieci</span><span class="sxs-lookup"><span data-stu-id="fd2ba-124">Step 4: Plan networking</span></span>

<span data-ttu-id="fd2ba-125">Należy toodo niektórych tooensure, które można skonfigurować mapowanie sieci, podczas wdrażania scenariusza hello do planowania sieci maszyn wirtualnych platformy Azure będzie tooAzure połączonych sieci wirtualnych po pracy awaryjnej, oraz że je przypisano odpowiednie IP adresów.</span><span class="sxs-lookup"><span data-stu-id="fd2ba-125">You need toodo some network planning tooensure that you can configure network mapping when you deploy hello scenario, that Azure VMs will be connected tooAzure virtual networks after failover occurs, and that that they're assigned appropriate IP addresses.</span></span>

<span data-ttu-id="fd2ba-126">Przejdź do zbyt[krok 4: Planowanie sieci](vmm-to-azure-walkthrough-network.md)</span><span class="sxs-lookup"><span data-stu-id="fd2ba-126">Go too[Step 4: Plan networking](vmm-to-azure-walkthrough-network.md)</span></span>


## <a name="step-5-prepare-azure-resources"></a><span data-ttu-id="fd2ba-127">Krok 5: Przygotowanie zasobów platformy Azure</span><span class="sxs-lookup"><span data-stu-id="fd2ba-127">Step 5: Prepare Azure resources</span></span>

<span data-ttu-id="fd2ba-128">Konfigurowanie konta platformy Azure, sieci i magazynu.</span><span class="sxs-lookup"><span data-stu-id="fd2ba-128">Set up an Azure account, networks, and storage.</span></span> <span data-ttu-id="fd2ba-129">Można to zrobić podczas wdrażania, ale zaleca się, że można to zrobić przed rozpoczęciem.</span><span class="sxs-lookup"><span data-stu-id="fd2ba-129">You can do this during deployment, but we recommend you do this before you start.</span></span>

<span data-ttu-id="fd2ba-130">Przejdź do zbyt[krok 5: przygotowanie Azure](vmm-to-azure-walkthrough-prepare-azure.md)</span><span class="sxs-lookup"><span data-stu-id="fd2ba-130">Go too[Step 5: Prepare Azure](vmm-to-azure-walkthrough-prepare-azure.md)</span></span>

## <a name="step-6-prepare-vmm-and-hyper-v"></a><span data-ttu-id="fd2ba-131">Krok 6: Przygotowanie VMM i funkcji Hyper-V</span><span class="sxs-lookup"><span data-stu-id="fd2ba-131">Step 6: Prepare VMM and Hyper-V</span></span>

<span data-ttu-id="fd2ba-132">Przygotuj serwery lokalne powitania, VMM i hosty funkcji Hyper-V do wdrażania usługi Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="fd2ba-132">Prepare hello on-premises VMM servers and Hyper-V hosts for Site Recovery deployment.</span></span>

<span data-ttu-id="fd2ba-133">Przejdź do zbyt[krok 6: Przygotowanie serwerów lokalnych](vmm-to-azure-walkthrough-vmm-hyper-v.md)</span><span class="sxs-lookup"><span data-stu-id="fd2ba-133">Go too[Step 6: Prepare on-premises servers](vmm-to-azure-walkthrough-vmm-hyper-v.md)</span></span>

## <a name="step-7-set-up-a-vault"></a><span data-ttu-id="fd2ba-134">Krok 7: Konfigurowanie magazynu</span><span class="sxs-lookup"><span data-stu-id="fd2ba-134">Step 7: Set up a vault</span></span>

<span data-ttu-id="fd2ba-135">Konfigurowanie magazynu usług odzyskiwania.</span><span class="sxs-lookup"><span data-stu-id="fd2ba-135">Set up a Recovery Services vault.</span></span> <span data-ttu-id="fd2ba-136">Magazyn Hello zawiera ustawienia konfiguracji i organizuje replikację.</span><span class="sxs-lookup"><span data-stu-id="fd2ba-136">hello vault contains configuration settings, and orchestrates replication.</span></span>

[<span data-ttu-id="fd2ba-137">Krok 7: Konfigurowanie magazynu</span><span class="sxs-lookup"><span data-stu-id="fd2ba-137">Step 7: Set up a vault</span></span>](vmm-to-azure-walkthrough-create-vault.md)

## <a name="step-8-configure-source-and-target-settings"></a><span data-ttu-id="fd2ba-138">Krok 8: Konfigurowanie ustawień źródłowa i docelowa</span><span class="sxs-lookup"><span data-stu-id="fd2ba-138">Step 8: Configure source and target settings</span></span>

<span data-ttu-id="fd2ba-139">Konfigurowanie hello źródłowe i docelowe lokalizacje replikacji.</span><span class="sxs-lookup"><span data-stu-id="fd2ba-139">Set up hello source and target replication locations.</span></span> <span data-ttu-id="fd2ba-140">Dodaj magazyn toohello serwera VMM hello i pobierane pliki instalacyjne hello składników usługi Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="fd2ba-140">Add hello VMM server toohello vault, and download hello installation files for Site Recovery components.</span></span> <span data-ttu-id="fd2ba-141">Uruchom Instalatora dostawcy usługi Azure Site Recovery na serwerze VMM hello.</span><span class="sxs-lookup"><span data-stu-id="fd2ba-141">Run Azure Site Recovery Provider setup on hello VMM server.</span></span> <span data-ttu-id="fd2ba-142">Instalator instaluje hello dostawcy na serwerze VMM hello i rejestruje hello serwer w magazynie hello.</span><span class="sxs-lookup"><span data-stu-id="fd2ba-142">Setup installs hello Provider on hello VMM server, and registers hello server in hello vault.</span></span> <span data-ttu-id="fd2ba-143">Należy zainstalować agenta usług odzyskiwania Microsoft hello na każdym hoście funkcji Hyper-V.</span><span class="sxs-lookup"><span data-stu-id="fd2ba-143">You install hello Microsoft Recovery Services agent on each Hyper-V host.</span></span>

<span data-ttu-id="fd2ba-144">Przejdź zbyt[krok 8: Konfigurowanie ustawień źródłowa i docelowa](vmm-to-azure-walkthrough-source-target.md)</span><span class="sxs-lookup"><span data-stu-id="fd2ba-144">Go too[Step 8: Configure source and target settings](vmm-to-azure-walkthrough-source-target.md)</span></span>

## <a name="step-9-configure-network-mapping"></a><span data-ttu-id="fd2ba-145">Krok 9: Konfigurowanie mapowania sieci</span><span class="sxs-lookup"><span data-stu-id="fd2ba-145">Step 9: Configure network mapping</span></span>

<span data-ttu-id="fd2ba-146">Mapa lokalnych sieci wirtualnych tooAzure sieci maszyny Wirtualnej programu VMM.</span><span class="sxs-lookup"><span data-stu-id="fd2ba-146">Map on-premises VMM VM networks tooAzure virtual networks.</span></span> <span data-ttu-id="fd2ba-147">Po przejściu w tryb failover maszynach wirtualnych platformy Azure są tworzone w hello sieć platformy Azure, która mapuje maszyny Wirtualnej sieci lokalnej toohello, w których hello znajduje się źródło funkcji Hyper-V.</span><span class="sxs-lookup"><span data-stu-id="fd2ba-147">After failover, Azure VMs are created in hello Azure network that maps toohello on-premises VM network in which hello source Hyper-V is located.</span></span>

<span data-ttu-id="fd2ba-148">Przejdź do zbyt[krok 9: Konfigurowanie mapowania sieci](vmm-to-azure-walkthrough-network-mapping.md)</span><span class="sxs-lookup"><span data-stu-id="fd2ba-148">Go too[Step 9: Configure network mapping](vmm-to-azure-walkthrough-network-mapping.md)</span></span>


## <a name="step-10-set-up-a-replication-policy"></a><span data-ttu-id="fd2ba-149">Krok 10: Konfigurowanie zasad replikacji</span><span class="sxs-lookup"><span data-stu-id="fd2ba-149">Step 10: Set up a replication policy</span></span>

<span data-ttu-id="fd2ba-150">Określ sposób lokalnych maszyn wirtualnych będą replikowane tooAzure.</span><span class="sxs-lookup"><span data-stu-id="fd2ba-150">Specify how on-premises VMs will be replicated tooAzure.</span></span>

<span data-ttu-id="fd2ba-151">Przejdź zbyt[10 kroku: Konfigurowanie zasad replikacji](vmm-to-azure-walkthrough-replication.md)</span><span class="sxs-lookup"><span data-stu-id="fd2ba-151">Go too[Step 10: Set up a replication policy](vmm-to-azure-walkthrough-replication.md)</span></span>


## <a name="step-11-enable-replication-for-vms"></a><span data-ttu-id="fd2ba-152">Krok 11: Włączanie replikacji maszyn wirtualnych</span><span class="sxs-lookup"><span data-stu-id="fd2ba-152">Step 11: Enable replication for VMs</span></span>

<span data-ttu-id="fd2ba-153">Wybierz maszyny wirtualne hello ma tooreplicate.</span><span class="sxs-lookup"><span data-stu-id="fd2ba-153">Select hello VMs you want tooreplicate.</span></span> <span data-ttu-id="fd2ba-154">Włączanie replikacji wyzwalaczy hello replikacji początkowej tooAzure maszynę Wirtualną, po replikacji różnicowej trwającą.</span><span class="sxs-lookup"><span data-stu-id="fd2ba-154">ENabling a VM for replication triggers hello initial replication tooAzure, followed by ongoing delta replication.</span></span>

<span data-ttu-id="fd2ba-155">Przejdź do zbyt[krok 11: Włączanie replikacji](vmm-to-azure-walkthrough-enable-replication.md)</span><span class="sxs-lookup"><span data-stu-id="fd2ba-155">Go too[Step 11: Enable replication](vmm-to-azure-walkthrough-enable-replication.md)</span></span>


## <a name="step-12-run-a-test-failover"></a><span data-ttu-id="fd2ba-156">Krok 12: Uruchom test trybu failover</span><span class="sxs-lookup"><span data-stu-id="fd2ba-156">Step 12: Run a test failover</span></span>

<span data-ttu-id="fd2ba-157">Uruchom test toomake trybu failover, się, że wszystko działa zgodnie z oczekiwaniami.</span><span class="sxs-lookup"><span data-stu-id="fd2ba-157">Run a test failover toomake sure everything's working as expected.</span></span>

<span data-ttu-id="fd2ba-158">Przejdź do zbyt[krok 12: testować tryb failover](vmm-to-azure-walkthrough-test-failover.md)</span><span class="sxs-lookup"><span data-stu-id="fd2ba-158">Go too[Step 12: Run a test failover](vmm-to-azure-walkthrough-test-failover.md)</span></span>


