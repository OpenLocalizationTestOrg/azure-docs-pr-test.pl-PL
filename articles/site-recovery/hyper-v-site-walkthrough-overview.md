---
title: "aaaReplicate tooAzure maszyn wirtualnych funkcji Hyper-V z usługą Azure Site Recovery | Dokumentacja firmy Microsoft"
description: "Opisuje sposób tooorchestrate replikacji, trybu failover i odzyskiwania lokalnych funkcji Hyper-V VMs tooAzure"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: efddd986-bc13-4a1d-932d-5484cdc7ad8d
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 06/21/2017
ms.author: raynew
ms.openlocfilehash: ab9cd14149ef32a416428d0f4327aa18b042e9c3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="replicate-hyper-v-virtual-machines-without-vmm-tooazure"></a><span data-ttu-id="eb0ba-103">Replikację funkcji Hyper-V tooAzure maszyn wirtualnych (bez VMM)</span><span class="sxs-lookup"><span data-stu-id="eb0ba-103">Replicate Hyper-V virtual machines (without VMM) tooAzure</span></span> 

> [!div class="op_single_selector"]
> * [<span data-ttu-id="eb0ba-104">Witryna Azure Portal</span><span class="sxs-lookup"><span data-stu-id="eb0ba-104">Azure portal</span></span>](site-recovery-hyper-v-site-to-azure.md)
> * [<span data-ttu-id="eb0ba-105">Klasyczny portal Azure</span><span class="sxs-lookup"><span data-stu-id="eb0ba-105">Azure classic</span></span>](site-recovery-hyper-v-site-to-azure-classic.md)
> * [<span data-ttu-id="eb0ba-106">Program PowerShell — model usługi Resource Manager</span><span class="sxs-lookup"><span data-stu-id="eb0ba-106">PowerShell - Resource Manager</span></span>](site-recovery-deploy-with-powershell-resource-manager.md)
>
>

<span data-ttu-id="eb0ba-107">Ten artykuł zawiera omówienie hello kroki wymagane tooreplicate lokalnym funkcji Hyper-V maszyny wirtualne tooAzure, przy użyciu hello [usługi Azure Site Recovery](site-recovery-overview.md) w hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="eb0ba-107">This article provides an overview of hello steps required tooreplicate on-premises Hyper-V virtual machines tooAzure, using hello [Azure Site Recovery](site-recovery-overview.md) in hello Azure portal.</span></span> <span data-ttu-id="eb0ba-108">W tym maszyn wirtualnych funkcji Hyper-V wdrożenia nie są zarządzane przez System Center Virtual Machine Manager (VMM).</span><span class="sxs-lookup"><span data-stu-id="eb0ba-108">In this deployment Hyper-V VMs aren't managed by System Center Virtual Machine Manager (VMM).</span></span>


<span data-ttu-id="eb0ba-109">Po przeczytaniu tego artykułu, post wszelkie komentarze u dołu hello, lub zadać pytania techniczne na powitania [Forum usług odzyskiwania Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="eb0ba-109">After reading this article, post any comments at hello bottom, or ask technical questions on hello [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>


## <a name="step-1-review-architecture-and-prerequisites"></a><span data-ttu-id="eb0ba-110">Krok 1: Przegląd architektury i wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="eb0ba-110">Step 1: Review architecture and prerequisites</span></span>

<span data-ttu-id="eb0ba-111">Przed rozpoczęciem wdrażania, przejrzyj architektura scenariusza hello i upewnij się, że znasz wszystkie składniki hello należy toodeploy</span><span class="sxs-lookup"><span data-stu-id="eb0ba-111">Before you start deployment, review hello scenario architecture, and make sure you understand all hello components you need toodeploy</span></span>

<span data-ttu-id="eb0ba-112">Przejdź do zbyt[krok 1: Przejrzyj hello architektury](hyper-v-site-walkthrough-architecture.md)</span><span class="sxs-lookup"><span data-stu-id="eb0ba-112">Go too[Step 1: Review hello architecture](hyper-v-site-walkthrough-architecture.md)</span></span>


## <a name="step-2-review-prerequisites"></a><span data-ttu-id="eb0ba-113">Krok 2: Sprawdź wymagania wstępne dotyczące</span><span class="sxs-lookup"><span data-stu-id="eb0ba-113">Step 2: Review prerequisites</span></span>

<span data-ttu-id="eb0ba-114">Upewnij się, że hello wymagania wstępne zostały spełnione dla każdego składnika wdrażania:</span><span class="sxs-lookup"><span data-stu-id="eb0ba-114">Make sure you have hello prerequisites in place for each deployment component:</span></span>

- <span data-ttu-id="eb0ba-115">**Wymagania wstępne platformy Azure**: wymagane konto Microsoft Azure, sieci platformy Azure i kont magazynu.</span><span class="sxs-lookup"><span data-stu-id="eb0ba-115">**Azure prerequisites**: You need a Microsoft Azure account, Azure networks, and storage accounts.</span></span>
- <span data-ttu-id="eb0ba-116">**Wymagania wstępne funkcji Hyper-V lokalnymi**: Upewnij się, że hosty funkcji Hyper-V są przygotowane do wdrażania usługi Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="eb0ba-116">**On-premises Hyper-V prerequisites**: Make sure Hyper-V hosts are prepared for Site Recovery deployment.</span></span>
- <span data-ttu-id="eb0ba-117">**Maszyny wirtualne replikowane**: maszyny wirtualne mają tooreplicate muszą toocomply z wymaganiami platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="eb0ba-117">**Replicated VMs**: VMs you want tooreplicate need toocomply with Azure requirements.</span></span>

<span data-ttu-id="eb0ba-118">Przejdź do zbyt[krok 2: Sprawdź wymagania wstępne i ograniczenia](hyper-v-site-walkthrough-prerequisites.md)</span><span class="sxs-lookup"><span data-stu-id="eb0ba-118">Go too[Step 2: Verify prerequisites and limitations](hyper-v-site-walkthrough-prerequisites.md)</span></span>

## <a name="step-3-plan-capacity"></a><span data-ttu-id="eb0ba-119">Krok 3: Planowanie pojemności</span><span class="sxs-lookup"><span data-stu-id="eb0ba-119">Step 3: Plan capacity</span></span>

<span data-ttu-id="eb0ba-120">Jeśli pełne wdrożenie robimy należy toofigure się, jakie potrzebne zasoby replikacji.</span><span class="sxs-lookup"><span data-stu-id="eb0ba-120">If you're doing a full deployment you need toofigure out what replication resources you need.</span></span> <span data-ttu-id="eb0ba-121">Istnieje kilka z toohelp dostępne narzędzia można to zrobić.</span><span class="sxs-lookup"><span data-stu-id="eb0ba-121">There are a couple of tools available toohelp you do this.</span></span> <span data-ttu-id="eb0ba-122">Przejdź tooStep 2.</span><span class="sxs-lookup"><span data-stu-id="eb0ba-122">Go tooStep 2.</span></span> <span data-ttu-id="eb0ba-123">Jeśli podczas wykonywania szybkiego skonfigurowania środowiska hello tootest można pominąć ten krok.</span><span class="sxs-lookup"><span data-stu-id="eb0ba-123">If you're doing a quick set up tootest hello environment you can skip this step.</span></span>

<span data-ttu-id="eb0ba-124">Przejdź do zbyt[krok 3: Planowanie pojemności](hyper-v-site-walkthrough-capacity.md)</span><span class="sxs-lookup"><span data-stu-id="eb0ba-124">Go too[Step 3: Plan capacity](hyper-v-site-walkthrough-capacity.md)</span></span>

## <a name="step-4-plan-networking"></a><span data-ttu-id="eb0ba-125">Krok 4: Planowanie sieci</span><span class="sxs-lookup"><span data-stu-id="eb0ba-125">Step 4: Plan networking</span></span>

<span data-ttu-id="eb0ba-126">Należy toodo niektórych planowania tooensure czy maszynach wirtualnych platformy Azure są połączone toonetworks po pracy awaryjnej i czy mają one hello prawo adresów IP sieci.</span><span class="sxs-lookup"><span data-stu-id="eb0ba-126">You need toodo some network planning tooensure that Azure VMs are connected toonetworks after failover occurs, and  that that they have hello right IP addresses.</span></span>

<span data-ttu-id="eb0ba-127">Przejdź do zbyt[krok 4: Planowanie sieci](hyper-v-site-walkthrough-network.md)</span><span class="sxs-lookup"><span data-stu-id="eb0ba-127">Go too[Step 4: Plan networking](hyper-v-site-walkthrough-network.md)</span></span>

##  <a name="step-5-prepare-azure-resources"></a><span data-ttu-id="eb0ba-128">Krok 5: Przygotowanie zasobów platformy Azure</span><span class="sxs-lookup"><span data-stu-id="eb0ba-128">Step 5: Prepare Azure resources</span></span>

<span data-ttu-id="eb0ba-129">Konfigurowanie sieci platformy Azure i magazynu przed jego uruchomieniem.</span><span class="sxs-lookup"><span data-stu-id="eb0ba-129">Set up Azure networks and storage before you start.</span></span> <span data-ttu-id="eb0ba-130">Można to zrobić podczas wdrażania, ale zaleca się, że można to zrobić przed rozpoczęciem.</span><span class="sxs-lookup"><span data-stu-id="eb0ba-130">You can do this during deployment, but we recommend you do this before you start.</span></span>

<span data-ttu-id="eb0ba-131">Przejdź do zbyt[krok 5: przygotowanie Azure](hyper-v-site-walkthrough-prepare-azure.md)</span><span class="sxs-lookup"><span data-stu-id="eb0ba-131">Go too[Step 5: Prepare Azure](hyper-v-site-walkthrough-prepare-azure.md)</span></span>


## <a name="step-6-prepare-hyper-v"></a><span data-ttu-id="eb0ba-132">Krok 6: Przygotowanie funkcji Hyper-V</span><span class="sxs-lookup"><span data-stu-id="eb0ba-132">Step 6: Prepare Hyper-V</span></span>

<span data-ttu-id="eb0ba-133">Upewnij się, że serwery funkcji Hyper-V spełniają wymagania dotyczące wdrażania usługi Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="eb0ba-133">Make sure that Hyper-V servers meet Site Recovery deployment requirements.</span></span>

<span data-ttu-id="eb0ba-134">Przejdź do zbyt[krok 6: Przygotowanie funkcji Hyper-V](hyper-v-site-walkthrough-prepare-hyper-v.md)</span><span class="sxs-lookup"><span data-stu-id="eb0ba-134">Go too[Step 6: Prepare Hyper-V](hyper-v-site-walkthrough-prepare-hyper-v.md)</span></span>

## <a name="step-7-set-up-a-vault"></a><span data-ttu-id="eb0ba-135">Krok 7: Konfigurowanie magazynu</span><span class="sxs-lookup"><span data-stu-id="eb0ba-135">Step 7: Set up a vault</span></span>

<span data-ttu-id="eb0ba-136">Należy tooset się tooorchestrate magazyn usług odzyskiwania i Zarządzanie replikacją.</span><span class="sxs-lookup"><span data-stu-id="eb0ba-136">You need tooset up a Recovery Services vault tooorchestrate and manage replication.</span></span> <span data-ttu-id="eb0ba-137">Po skonfigurowaniu magazynu hello Określ sposób tooreplicate, i miejsce tooreplicate jej.</span><span class="sxs-lookup"><span data-stu-id="eb0ba-137">When you set up hello vault, you specify what you want tooreplicate, and where you want tooreplicate it to.</span></span>

<span data-ttu-id="eb0ba-138">Przejdź do zbyt[kroku 7: Tworzenie magazynu](hyper-v-site-walkthrough-create-vault.md)</span><span class="sxs-lookup"><span data-stu-id="eb0ba-138">Go too[Step 7: Create a vault](hyper-v-site-walkthrough-create-vault.md)</span></span>

## <a name="step-8-configure-source-and-target-settings"></a><span data-ttu-id="eb0ba-139">Krok 8: Konfigurowanie ustawień źródłowa i docelowa</span><span class="sxs-lookup"><span data-stu-id="eb0ba-139">Step 8: Configure source and target settings</span></span>

<span data-ttu-id="eb0ba-140">Konfigurowanie hello źródłowy i docelowy, który jest używany do replikacji.</span><span class="sxs-lookup"><span data-stu-id="eb0ba-140">Set up hello source and target that's used for replication.</span></span> <span data-ttu-id="eb0ba-141">Konfigurowanie ustawień źródła obejmuje dodanie funkcji Hyper-V hosts tooa funkcji Hyper-V lokacji, instalowanie hello dostawcy usługi Site Recovery i agent usług odzyskiwania na każdym hoście funkcji Hyper-V i rejestrowanie lokacji hello w powitalne magazyn usług odzyskiwania.</span><span class="sxs-lookup"><span data-stu-id="eb0ba-141">Setting up source settings includes adding Hyper-V hosts tooa Hyper-V site, installing hello Site Recovery Provider and Recovery Services agent on each Hyper-V host, and registering hello site in hello Recovery Services vault.</span></span>

<span data-ttu-id="eb0ba-142">Przejdź do zbyt[krok 8: Konfigurowanie hello źródłowa i docelowa](hyper-v-site-walkthrough-source-target.md)</span><span class="sxs-lookup"><span data-stu-id="eb0ba-142">Go too[Step 8: Set up hello source and target](hyper-v-site-walkthrough-source-target.md)</span></span>

## <a name="step-9-set-up-a-replication-policy"></a><span data-ttu-id="eb0ba-143">Krok 9: Konfigurowanie zasad replikacji</span><span class="sxs-lookup"><span data-stu-id="eb0ba-143">Step 9: Set up a replication policy</span></span>

<span data-ttu-id="eb0ba-144">Skonfigurowane ustawienia replikacji toospecify zasad dla maszyn wirtualnych funkcji Hyper-V w magazynie hello.</span><span class="sxs-lookup"><span data-stu-id="eb0ba-144">You set up a policy toospecify replication settings for Hyper-V VMs in hello vault.</span></span>

<span data-ttu-id="eb0ba-145">Przejdź do zbyt[krok 9: Konfigurowanie zasad replikacji](hyper-v-site-walkthrough-replication.md)</span><span class="sxs-lookup"><span data-stu-id="eb0ba-145">Go too[Step 9: Set up a replication policy](hyper-v-site-walkthrough-replication.md)</span></span>


## <a name="step-10-enable-replication"></a><span data-ttu-id="eb0ba-146">Krok 10: Włączanie replikacji</span><span class="sxs-lookup"><span data-stu-id="eb0ba-146">Step 10: Enable replication</span></span>

<span data-ttu-id="eb0ba-147">Po utworzeniu zasad replikacji w miejscu, po włączeniu replikacji początkowej dla maszyny Wirtualnej hello występuje.</span><span class="sxs-lookup"><span data-stu-id="eb0ba-147">After you have a replication policy in place,  After enabling, initial replication of hello VM occurs.</span></span>

<span data-ttu-id="eb0ba-148">Przejdź do zbyt[kroku 10: Włączanie replikacji](hyper-v-site-walkthrough-enable-replication.md)</span><span class="sxs-lookup"><span data-stu-id="eb0ba-148">Go too[Step 10: Enable replication](hyper-v-site-walkthrough-enable-replication.md)</span></span>

## <a name="step-11-run-a-test-failover"></a><span data-ttu-id="eb0ba-149">Krok 11: Uruchom test trybu failover</span><span class="sxs-lookup"><span data-stu-id="eb0ba-149">Step 11: Run a test failover</span></span>

<span data-ttu-id="eb0ba-150">Po zakończeniu replikacji początkowej, a replikacja różnicowa jest uruchomiony, możesz uruchomić test pracy awaryjnej toomake się, że wszystko działa zgodnie z oczekiwaniami.</span><span class="sxs-lookup"><span data-stu-id="eb0ba-150">After initial replication finishes, and delta replication is running, you can run a test failover toomake sure everything works as expected.</span></span>

<span data-ttu-id="eb0ba-151">Przejdź do zbyt[krok 11: testować tryb failover](hyper-v-site-walkthrough-test-failover.md)</span><span class="sxs-lookup"><span data-stu-id="eb0ba-151">Go too[Step 11: Run a test failover](hyper-v-site-walkthrough-test-failover.md)</span></span>
