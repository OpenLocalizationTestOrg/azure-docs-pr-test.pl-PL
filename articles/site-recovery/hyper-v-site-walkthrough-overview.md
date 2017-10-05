---
title: "Replikowanie maszyn wirtualnych funkcji Hyper-V na platformie Azure za pomocą usługi Azure Site Recovery | Dokumentacja firmy Microsoft"
description: "Opisuje sposób organizowania replikacji, trybu failover i odzyskiwania maszyn wirtualnych funkcji Hyper-V lokalnego do platformy Azure"
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
ms.openlocfilehash: da10b213bc2543942b5ac77cf5c5d8547c00220c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="replicate-hyper-v-virtual-machines-without-vmm-to-azure"></a><span data-ttu-id="95607-103">Replikowanie maszyn wirtualnych funkcji Hyper-V (bez VMM) na platformie Azure</span><span class="sxs-lookup"><span data-stu-id="95607-103">Replicate Hyper-V virtual machines (without VMM) to Azure</span></span> 

> [!div class="op_single_selector"]
> * [<span data-ttu-id="95607-104">Witryna Azure Portal</span><span class="sxs-lookup"><span data-stu-id="95607-104">Azure portal</span></span>](site-recovery-hyper-v-site-to-azure.md)
> * [<span data-ttu-id="95607-105">Klasyczny portal Azure</span><span class="sxs-lookup"><span data-stu-id="95607-105">Azure classic</span></span>](site-recovery-hyper-v-site-to-azure-classic.md)
> * [<span data-ttu-id="95607-106">Program PowerShell — model usługi Resource Manager</span><span class="sxs-lookup"><span data-stu-id="95607-106">PowerShell - Resource Manager</span></span>](site-recovery-deploy-with-powershell-resource-manager.md)
>
>

<span data-ttu-id="95607-107">W tym artykule omówiono kroki wymagane do replikowania maszyn wirtualnych funkcji Hyper-V lokalnej na platformie Azure, przy użyciu [usługi Azure Site Recovery](site-recovery-overview.md) w portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="95607-107">This article provides an overview of the steps required to replicate on-premises Hyper-V virtual machines to Azure, using the [Azure Site Recovery](site-recovery-overview.md) in the Azure portal.</span></span> <span data-ttu-id="95607-108">W tym maszyn wirtualnych funkcji Hyper-V wdrożenia nie są zarządzane przez System Center Virtual Machine Manager (VMM).</span><span class="sxs-lookup"><span data-stu-id="95607-108">In this deployment Hyper-V VMs aren't managed by System Center Virtual Machine Manager (VMM).</span></span>


<span data-ttu-id="95607-109">Po przeczytaniu tego artykułu, post wszelkie komentarze u dołu i zadawaj pytania techniczne na [Forum usług odzyskiwania Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="95607-109">After reading this article, post any comments at the bottom, or ask technical questions on the [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>


## <a name="step-1-review-architecture-and-prerequisites"></a><span data-ttu-id="95607-110">Krok 1: Przegląd architektury i wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="95607-110">Step 1: Review architecture and prerequisites</span></span>

<span data-ttu-id="95607-111">Przed rozpoczęciem wdrażania zapoznaj się z architekturą scenariusza i upewnij się, że znasz wszystkie składniki potrzebne do wdrożenia</span><span class="sxs-lookup"><span data-stu-id="95607-111">Before you start deployment, review the scenario architecture, and make sure you understand all the components you need to deploy</span></span>

<span data-ttu-id="95607-112">Przejdź do [krok 1: Przejrzyj architektury](hyper-v-site-walkthrough-architecture.md)</span><span class="sxs-lookup"><span data-stu-id="95607-112">Go to [Step 1: Review the architecture](hyper-v-site-walkthrough-architecture.md)</span></span>


## <a name="step-2-review-prerequisites"></a><span data-ttu-id="95607-113">Krok 2: Sprawdź wymagania wstępne dotyczące</span><span class="sxs-lookup"><span data-stu-id="95607-113">Step 2: Review prerequisites</span></span>

<span data-ttu-id="95607-114">Upewnij się, że zostały spełnione wymagania wstępne w przypadku każdego składnika wdrażania:</span><span class="sxs-lookup"><span data-stu-id="95607-114">Make sure you have the prerequisites in place for each deployment component:</span></span>

- <span data-ttu-id="95607-115">**Wymagania wstępne platformy Azure**: wymagane konto Microsoft Azure, sieci platformy Azure i kont magazynu.</span><span class="sxs-lookup"><span data-stu-id="95607-115">**Azure prerequisites**: You need a Microsoft Azure account, Azure networks, and storage accounts.</span></span>
- <span data-ttu-id="95607-116">**Wymagania wstępne funkcji Hyper-V lokalnymi**: Upewnij się, że hosty funkcji Hyper-V są przygotowane do wdrażania usługi Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="95607-116">**On-premises Hyper-V prerequisites**: Make sure Hyper-V hosts are prepared for Site Recovery deployment.</span></span>
- <span data-ttu-id="95607-117">**Maszyny wirtualne replikowane**: maszyny wirtualne mają być replikowane musi spełniać wymagania dotyczące usługi Azure.</span><span class="sxs-lookup"><span data-stu-id="95607-117">**Replicated VMs**: VMs you want to replicate need to comply with Azure requirements.</span></span>

<span data-ttu-id="95607-118">Przejdź do [krok 2: Sprawdź wymagania wstępne i ograniczenia](hyper-v-site-walkthrough-prerequisites.md)</span><span class="sxs-lookup"><span data-stu-id="95607-118">Go to [Step 2: Verify prerequisites and limitations](hyper-v-site-walkthrough-prerequisites.md)</span></span>

## <a name="step-3-plan-capacity"></a><span data-ttu-id="95607-119">Krok 3: Planowanie pojemności</span><span class="sxs-lookup"><span data-stu-id="95607-119">Step 3: Plan capacity</span></span>

<span data-ttu-id="95607-120">Jeśli pełne wdrożenie robimy należy dowiedzieć się, jakie potrzebne zasoby replikacji.</span><span class="sxs-lookup"><span data-stu-id="95607-120">If you're doing a full deployment you need to figure out what replication resources you need.</span></span> <span data-ttu-id="95607-121">Istnieje kilka narzędzi ułatwiających to zrobić.</span><span class="sxs-lookup"><span data-stu-id="95607-121">There are a couple of tools available to help you do this.</span></span> <span data-ttu-id="95607-122">Przejdź do kroku 2.</span><span class="sxs-lookup"><span data-stu-id="95607-122">Go to Step 2.</span></span> <span data-ttu-id="95607-123">Jeśli podczas wykonywania zestawu szybkiego się do środowiska testowego można pominąć ten krok.</span><span class="sxs-lookup"><span data-stu-id="95607-123">If you're doing a quick set up to test the environment you can skip this step.</span></span>

<span data-ttu-id="95607-124">Przejdź do sekcji [Krok 3. Planowanie wydajności](hyper-v-site-walkthrough-capacity.md)</span><span class="sxs-lookup"><span data-stu-id="95607-124">Go to [Step 3: Plan capacity](hyper-v-site-walkthrough-capacity.md)</span></span>

## <a name="step-4-plan-networking"></a><span data-ttu-id="95607-125">Krok 4: Planowanie sieci</span><span class="sxs-lookup"><span data-stu-id="95607-125">Step 4: Plan networking</span></span>

<span data-ttu-id="95607-126">Należy wykonać niektóre sieci, planowanie upewnić się, czy maszynach wirtualnych platformy Azure są połączone z sieciami po pracy awaryjnej i które mają prawo IP adresy.</span><span class="sxs-lookup"><span data-stu-id="95607-126">You need to do some network planning to ensure that Azure VMs are connected to networks after failover occurs, and  that that they have the right IP addresses.</span></span>

<span data-ttu-id="95607-127">Przejdź do [krok 4: Planowanie sieci](hyper-v-site-walkthrough-network.md)</span><span class="sxs-lookup"><span data-stu-id="95607-127">Go to [Step 4: Plan networking](hyper-v-site-walkthrough-network.md)</span></span>

##  <a name="step-5-prepare-azure-resources"></a><span data-ttu-id="95607-128">Krok 5: Przygotowanie zasobów platformy Azure</span><span class="sxs-lookup"><span data-stu-id="95607-128">Step 5: Prepare Azure resources</span></span>

<span data-ttu-id="95607-129">Konfigurowanie sieci platformy Azure i magazynu przed jego uruchomieniem.</span><span class="sxs-lookup"><span data-stu-id="95607-129">Set up Azure networks and storage before you start.</span></span> <span data-ttu-id="95607-130">Można to zrobić podczas wdrażania, ale zaleca się, że można to zrobić przed rozpoczęciem.</span><span class="sxs-lookup"><span data-stu-id="95607-130">You can do this during deployment, but we recommend you do this before you start.</span></span>

<span data-ttu-id="95607-131">Przejdź do [krok 5: przygotowanie Azure](hyper-v-site-walkthrough-prepare-azure.md)</span><span class="sxs-lookup"><span data-stu-id="95607-131">Go to [Step 5: Prepare Azure](hyper-v-site-walkthrough-prepare-azure.md)</span></span>


## <a name="step-6-prepare-hyper-v"></a><span data-ttu-id="95607-132">Krok 6: Przygotowanie funkcji Hyper-V</span><span class="sxs-lookup"><span data-stu-id="95607-132">Step 6: Prepare Hyper-V</span></span>

<span data-ttu-id="95607-133">Upewnij się, że serwery funkcji Hyper-V spełniają wymagania dotyczące wdrażania usługi Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="95607-133">Make sure that Hyper-V servers meet Site Recovery deployment requirements.</span></span>

<span data-ttu-id="95607-134">Przejdź do [krok 6: Przygotowanie funkcji Hyper-V](hyper-v-site-walkthrough-prepare-hyper-v.md)</span><span class="sxs-lookup"><span data-stu-id="95607-134">Go to [Step 6: Prepare Hyper-V](hyper-v-site-walkthrough-prepare-hyper-v.md)</span></span>

## <a name="step-7-set-up-a-vault"></a><span data-ttu-id="95607-135">Krok 7: Konfigurowanie magazynu</span><span class="sxs-lookup"><span data-stu-id="95607-135">Step 7: Set up a vault</span></span>

<span data-ttu-id="95607-136">Należy skonfigurować magazyn usług odzyskiwania do organizowania replikacji.</span><span class="sxs-lookup"><span data-stu-id="95607-136">You need to set up a Recovery Services vault to orchestrate and manage replication.</span></span> <span data-ttu-id="95607-137">Po skonfigurowaniu magazynu można określić co chcesz replikować, a które chcesz replikować go do.</span><span class="sxs-lookup"><span data-stu-id="95607-137">When you set up the vault, you specify what you want to replicate, and where you want to replicate it to.</span></span>

<span data-ttu-id="95607-138">Przejdź do [kroku 7: Tworzenie magazynu](hyper-v-site-walkthrough-create-vault.md)</span><span class="sxs-lookup"><span data-stu-id="95607-138">Go to [Step 7: Create a vault](hyper-v-site-walkthrough-create-vault.md)</span></span>

## <a name="step-8-configure-source-and-target-settings"></a><span data-ttu-id="95607-139">Krok 8: Konfigurowanie ustawień źródłowa i docelowa</span><span class="sxs-lookup"><span data-stu-id="95607-139">Step 8: Configure source and target settings</span></span>

<span data-ttu-id="95607-140">Skonfiguruj źródłowy i docelowy, który jest używany do replikacji.</span><span class="sxs-lookup"><span data-stu-id="95607-140">Set up the source and target that's used for replication.</span></span> <span data-ttu-id="95607-141">Konfigurowanie ustawień źródła obejmuje dodawanie hostów funkcji Hyper-V do lokacji funkcji Hyper-V, zainstalowanie agenta dostawcy usługi Site Recovery i usług odzyskiwania na każdym hoście funkcji Hyper-V i rejestrowanie w magazynie usług odzyskiwania lokacji.</span><span class="sxs-lookup"><span data-stu-id="95607-141">Setting up source settings includes adding Hyper-V hosts to a Hyper-V site, installing the Site Recovery Provider and Recovery Services agent on each Hyper-V host, and registering the site in the Recovery Services vault.</span></span>

<span data-ttu-id="95607-142">Przejdź do [krok 8: Konfigurowanie źródłowych i docelowych](hyper-v-site-walkthrough-source-target.md)</span><span class="sxs-lookup"><span data-stu-id="95607-142">Go to [Step 8: Set up the source and target](hyper-v-site-walkthrough-source-target.md)</span></span>

## <a name="step-9-set-up-a-replication-policy"></a><span data-ttu-id="95607-143">Krok 9: Konfigurowanie zasad replikacji</span><span class="sxs-lookup"><span data-stu-id="95607-143">Step 9: Set up a replication policy</span></span>

<span data-ttu-id="95607-144">Aby określić ustawienia replikacji dla maszyn wirtualnych funkcji Hyper-V w magazynie skonfigurować zasadę.</span><span class="sxs-lookup"><span data-stu-id="95607-144">You set up a policy to specify replication settings for Hyper-V VMs in the vault.</span></span>

<span data-ttu-id="95607-145">Przejdź do [krok 9: Konfigurowanie zasad replikacji](hyper-v-site-walkthrough-replication.md)</span><span class="sxs-lookup"><span data-stu-id="95607-145">Go to [Step 9: Set up a replication policy](hyper-v-site-walkthrough-replication.md)</span></span>


## <a name="step-10-enable-replication"></a><span data-ttu-id="95607-146">Krok 10: Włączanie replikacji</span><span class="sxs-lookup"><span data-stu-id="95607-146">Step 10: Enable replication</span></span>

<span data-ttu-id="95607-147">Po utworzeniu zasad replikacji w miejscu, po włączeniu występuje początkowej replikacji maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="95607-147">After you have a replication policy in place,  After enabling, initial replication of the VM occurs.</span></span>

<span data-ttu-id="95607-148">Przejdź do [kroku 10: Włączanie replikacji](hyper-v-site-walkthrough-enable-replication.md)</span><span class="sxs-lookup"><span data-stu-id="95607-148">Go to [Step 10: Enable replication](hyper-v-site-walkthrough-enable-replication.md)</span></span>

## <a name="step-11-run-a-test-failover"></a><span data-ttu-id="95607-149">Krok 11: Uruchom test trybu failover</span><span class="sxs-lookup"><span data-stu-id="95607-149">Step 11: Run a test failover</span></span>

<span data-ttu-id="95607-150">Po zakończeniu replikacji początkowej, a replikacja różnicowa jest uruchomiony, możesz uruchomić test trybu failover, aby upewnić się, że wszystko działa zgodnie z oczekiwaniami.</span><span class="sxs-lookup"><span data-stu-id="95607-150">After initial replication finishes, and delta replication is running, you can run a test failover to make sure everything works as expected.</span></span>

<span data-ttu-id="95607-151">Przejdź do [krok 11: testować tryb failover](hyper-v-site-walkthrough-test-failover.md)</span><span class="sxs-lookup"><span data-stu-id="95607-151">Go to [Step 11: Run a test failover](hyper-v-site-walkthrough-test-failover.md)</span></span>
