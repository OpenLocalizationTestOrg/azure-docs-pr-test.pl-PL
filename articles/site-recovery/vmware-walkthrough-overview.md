---
title: "Replikowanie maszyn wirtualnych VMware do platformy Azure z usługą Azure Site Recovery | Dokumentacja firmy Microsoft"
description: "Zawiera omówienie kroków replikowania obciążeń uruchomionych na maszynach wirtualnych VMware do platformy Azure"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: dab98aa5-9c41-4475-b7dc-2e07ab1cfd18
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/27/2017
ms.author: raynew
ms.openlocfilehash: db6f5f95929503e82a529dba26b56af1edb0767f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="replicate-vmware-vms-to-azure-with-site-recovery"></a><span data-ttu-id="06f58-103">Replikowanie maszyn wirtualnych VMware do platformy Azure z usługą Site Recovery</span><span class="sxs-lookup"><span data-stu-id="06f58-103">Replicate VMware VMs to Azure with Site Recovery</span></span>

<span data-ttu-id="06f58-104">W tym artykule omówiono kroki wymagane do replikowania maszyn wirtualnych VMware lokalnej na platformie Azure, przy użyciu [usługi Azure Site Recovery](site-recovery-overview.md) w portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="06f58-104">This article provides an overview of the steps required to replicate on-premises VMware virtual machines to Azure, using the [Azure Site Recovery](site-recovery-overview.md) service in the Azure portal.</span></span>


![Proces wdrażania](./media/vmware-walkthrough-overview/vmware-to-azure-process.png)

<span data-ttu-id="06f58-106">**Rysunek 1: Podsumowanie procesu wdrożenia**</span><span class="sxs-lookup"><span data-stu-id="06f58-106">**Figure 1: Deployment process summary**</span></span>

## <a name="step-1-review-architecture-and-prerequisites"></a><span data-ttu-id="06f58-107">Krok 1: Przegląd architektury i wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="06f58-107">Step 1: Review architecture and prerequisites</span></span>

<span data-ttu-id="06f58-108">Przed rozpoczęciem wdrażania zapoznaj się z architekturą scenariusza i upewnij się, że znasz wszystkie składniki potrzebne do wdrożenia</span><span class="sxs-lookup"><span data-stu-id="06f58-108">Before you start deployment, review the scenario architecture, and make sure you understand all the components you need to deploy</span></span>

<span data-ttu-id="06f58-109">Przejdź do [krok 1: Przejrzyj architektury](vmware-walkthrough-architecture.md)</span><span class="sxs-lookup"><span data-stu-id="06f58-109">Go to [Step 1: Review the architecture](vmware-walkthrough-architecture.md)</span></span>


## <a name="step-2-review-prerequisites"></a><span data-ttu-id="06f58-110">Krok 2: Sprawdź wymagania wstępne dotyczące</span><span class="sxs-lookup"><span data-stu-id="06f58-110">Step 2: Review prerequisites</span></span>

<span data-ttu-id="06f58-111">Upewnij się, że zostały spełnione wymagania wstępne w przypadku każdego składnika wdrażania:</span><span class="sxs-lookup"><span data-stu-id="06f58-111">Make sure you have the prerequisites in place for each deployment component:</span></span>

- <span data-ttu-id="06f58-112">**Wymagania wstępne platformy Azure**: wymagane konto Microsoft Azure, sieci platformy Azure i kont magazynu.</span><span class="sxs-lookup"><span data-stu-id="06f58-112">**Azure prerequisites**: You need a Microsoft Azure account, Azure networks, and storage accounts.</span></span>
- <span data-ttu-id="06f58-113">**Składniki usługi Site Recovery lokalnymi**: należy komputera z uruchomionym systemem lokalnymi składnikami usługi Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="06f58-113">**On-premises Site Recovery components**: You need a machine running on-premises Site Recovery components.</span></span>
- <span data-ttu-id="06f58-114">**Lokalne wstępnych VMware**: należy ustawić kont, dzięki czemu usługa Site Recovery mogą uzyskiwać dostęp do serwerów VMware i maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="06f58-114">**On-premises VMware prerequisites**: You need to set up accounts so that Site Recovery can access VMware servers and VMs.</span></span>
- <span data-ttu-id="06f58-115">**Maszyny wirtualne replikowane**: chcesz replikować maszyny wirtualne muszą spełniać wymagania dotyczące usługi Azure i zainstalowano składnika usługi Mobility.</span><span class="sxs-lookup"><span data-stu-id="06f58-115">**Replicated VMs**: VMs you want to replicate need to comply with Azure requirements, and have the Mobility service component installed.</span></span>

<span data-ttu-id="06f58-116">Przejdź do [krok 2: Przejrzyj wymagania wstępne i ograniczenia](vmware-walkthrough-prerequisites.md)</span><span class="sxs-lookup"><span data-stu-id="06f58-116">Go to [Step 2: Review prerequisites and limitations](vmware-walkthrough-prerequisites.md)</span></span>

## <a name="step-3-plan-capacity"></a><span data-ttu-id="06f58-117">Krok 3: Planowanie pojemności</span><span class="sxs-lookup"><span data-stu-id="06f58-117">Step 3: Plan capacity</span></span>

<span data-ttu-id="06f58-118">Jeśli pełne wdrożenie robimy należy dowiedzieć się, jakie potrzebne zasoby replikacji.</span><span class="sxs-lookup"><span data-stu-id="06f58-118">If you're doing a full deployment you need to figure out what replication resources you need.</span></span> <span data-ttu-id="06f58-119">Istnieje kilka narzędzi ułatwiających to zrobić.</span><span class="sxs-lookup"><span data-stu-id="06f58-119">There are a couple of tools available to help you do this.</span></span> <span data-ttu-id="06f58-120">Przejdź do kroku 2.</span><span class="sxs-lookup"><span data-stu-id="06f58-120">Go to Step 2.</span></span> <span data-ttu-id="06f58-121">Jeśli podczas wykonywania zestawu szybkiego się do środowiska testowego można pominąć ten krok.</span><span class="sxs-lookup"><span data-stu-id="06f58-121">If you're doing a quick set up to test the environment you can skip this step.</span></span>

<span data-ttu-id="06f58-122">Przejdź do sekcji [Krok 3. Planowanie wydajności](vmware-walkthrough-capacity.md)</span><span class="sxs-lookup"><span data-stu-id="06f58-122">Go to [Step 3: Plan capacity](vmware-walkthrough-capacity.md)</span></span>

## <a name="step-4-plan-networking"></a><span data-ttu-id="06f58-123">Krok 4: Planowanie sieci</span><span class="sxs-lookup"><span data-stu-id="06f58-123">Step 4: Plan networking</span></span>

<span data-ttu-id="06f58-124">Należy wykonać niektóre sieci, planowanie upewnić się, czy maszynach wirtualnych platformy Azure są połączone z sieciami po pracy awaryjnej i które mają prawo IP adresy.</span><span class="sxs-lookup"><span data-stu-id="06f58-124">You need to do some network planning to ensure that Azure VMs are connected to networks after failover occurs, and  that that they have the right IP addresses.</span></span>

<span data-ttu-id="06f58-125">Przejdź do [krok 4: Planowanie sieci](vmware-walkthrough-network.md)</span><span class="sxs-lookup"><span data-stu-id="06f58-125">Go to [Step 4: Plan networking](vmware-walkthrough-network.md)</span></span>

##  <a name="step-5-prepare-azure-resources"></a><span data-ttu-id="06f58-126">Krok 5: Przygotowanie zasobów platformy Azure</span><span class="sxs-lookup"><span data-stu-id="06f58-126">Step 5: Prepare Azure resources</span></span>

<span data-ttu-id="06f58-127">Konfigurowanie sieci platformy Azure i magazynu przed jego uruchomieniem.</span><span class="sxs-lookup"><span data-stu-id="06f58-127">Set up Azure networks and storage before you start.</span></span> <span data-ttu-id="06f58-128">Można to zrobić podczas wdrażania, ale zaleca się, że można to zrobić przed rozpoczęciem.</span><span class="sxs-lookup"><span data-stu-id="06f58-128">You can do this during deployment, but we recommend you do this before you start.</span></span>

<span data-ttu-id="06f58-129">Przejdź do [krok 5: przygotowanie Azure](vmware-walkthrough-prepare-azure.md)</span><span class="sxs-lookup"><span data-stu-id="06f58-129">Go to [Step 5: Prepare Azure](vmware-walkthrough-prepare-azure.md)</span></span>


## <a name="step-6-prepare-vmware"></a><span data-ttu-id="06f58-130">Krok 6: Przygotowanie VMware</span><span class="sxs-lookup"><span data-stu-id="06f58-130">Step 6: Prepare VMware</span></span>

<span data-ttu-id="06f58-131">Należy skonfigurować konta używających usługi Site Recovery do:</span><span class="sxs-lookup"><span data-stu-id="06f58-131">You need to set up accounts that Site Recovery will use to:</span></span>

- <span data-ttu-id="06f58-132">Dostęp do serwera wirtualizacji VMware, aby automatycznie wykrywać maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="06f58-132">Access VMware virtualization servers to automatically detect VMs.</span></span>
- <span data-ttu-id="06f58-133">Dostęp do maszyn wirtualnych do zainstalowania usługi mobilności.</span><span class="sxs-lookup"><span data-stu-id="06f58-133">Access VMs to install the Mobility service.</span></span> <span data-ttu-id="06f58-134">Każda maszyna wirtualna, które chcesz replikować musi mieć agent usługi mobilności, zainstalowane, aby można było włączyć dla niego replikację.</span><span class="sxs-lookup"><span data-stu-id="06f58-134">Each VM you want to replicate must have the Mobility service agent installed before you can enable replication for it.</span></span>

<span data-ttu-id="06f58-135">Przejdź do [krok 6: przygotowanie VMware](vmware-walkthrough-prepare-vmware.md)</span><span class="sxs-lookup"><span data-stu-id="06f58-135">Go to [Step 6: Prepare VMware](vmware-walkthrough-prepare-vmware.md)</span></span>

## <a name="step-7-set-up-a-vault"></a><span data-ttu-id="06f58-136">Krok 7: Konfigurowanie magazynu</span><span class="sxs-lookup"><span data-stu-id="06f58-136">Step 7: Set up a vault</span></span>

<span data-ttu-id="06f58-137">Należy skonfigurować magazyn usług odzyskiwania do organizowania replikacji.</span><span class="sxs-lookup"><span data-stu-id="06f58-137">You need to set up a Recovery Services vault to orchestrate and manage replication.</span></span> <span data-ttu-id="06f58-138">Po skonfigurowaniu magazynu można określić co chcesz replikować, a które chcesz replikować go do.</span><span class="sxs-lookup"><span data-stu-id="06f58-138">When you set up the vault, you specify what you want to replicate, and where you want to replicate it to.</span></span>

<span data-ttu-id="06f58-139">Przejdź do [kroku 7: Konfigurowanie magazynu](vmware-walkthrough-create-vault.md)</span><span class="sxs-lookup"><span data-stu-id="06f58-139">Go to [Step 7: Set up a vault](vmware-walkthrough-create-vault.md)</span></span>

## <a name="step-8-configure-source-and-target-settings"></a><span data-ttu-id="06f58-140">Krok 8: Konfigurowanie ustawień źródłowa i docelowa</span><span class="sxs-lookup"><span data-stu-id="06f58-140">Step 8: Configure source and target settings</span></span>

<span data-ttu-id="06f58-141">Skonfiguruj źródłowy i docelowy, który jest używany do replikacji.</span><span class="sxs-lookup"><span data-stu-id="06f58-141">Set up the source and target that's used for replication.</span></span> <span data-ttu-id="06f58-142">Konfigurowanie ustawień źródła obejmuje uruchomione Unified Instalatora, aby zainstalować składniki usługi Site Recovery lokalnymi.</span><span class="sxs-lookup"><span data-stu-id="06f58-142">Setting up source settings includes running Unified Setup to install the on-premises Site Recovery components.</span></span>

<span data-ttu-id="06f58-143">Przejdź do [krok 8: Konfigurowanie źródłowych i docelowych](vmware-walkthrough-source-target.md)</span><span class="sxs-lookup"><span data-stu-id="06f58-143">Go to [Step 8: Set up the source and target](vmware-walkthrough-source-target.md)</span></span>

## <a name="step-9-set-up-a-replication-policy"></a><span data-ttu-id="06f58-144">Krok 9: Konfigurowanie zasad replikacji</span><span class="sxs-lookup"><span data-stu-id="06f58-144">Step 9: Set up a replication policy</span></span>

<span data-ttu-id="06f58-145">Aby określić ustawienia replikacji dla maszyn wirtualnych VMware w magazynie skonfigurować zasadę.</span><span class="sxs-lookup"><span data-stu-id="06f58-145">You set up a policy to specify replication settings for VMware VMs in the vault.</span></span>

<span data-ttu-id="06f58-146">Przejdź do [krok 9: Konfigurowanie zasad replikacji](vmware-walkthrough-replication.md)</span><span class="sxs-lookup"><span data-stu-id="06f58-146">Go to [Step 9: Set up a replication policy](vmware-walkthrough-replication.md)</span></span>

## <a name="step-10-install-the-mobility-service"></a><span data-ttu-id="06f58-147">Krok 10: Zainstaluj usługę mobilności</span><span class="sxs-lookup"><span data-stu-id="06f58-147">Step 10: Install the Mobility service</span></span>

<span data-ttu-id="06f58-148">Musi być zainstalowana usługa mobilności na każdej maszynie Wirtualnej, którą chcesz replikować.</span><span class="sxs-lookup"><span data-stu-id="06f58-148">The Mobility service must be installed on each VM you want to replicate.</span></span> <span data-ttu-id="06f58-149">Istnieje kilka sposobów, aby skonfigurować usługę za pomocą wypychania lub ściągania instalacji.</span><span class="sxs-lookup"><span data-stu-id="06f58-149">There are a few ways to set up the service with push or pull installation.</span></span>

<span data-ttu-id="06f58-150">Przejdź do [kroku 10: Zainstaluj usługę mobilności](vmware-walkthrough-install-mobility.md)</span><span class="sxs-lookup"><span data-stu-id="06f58-150">Go to [Step 10: Install the Mobility service](vmware-walkthrough-install-mobility.md)</span></span>

## <a name="step-11-enable-replication"></a><span data-ttu-id="06f58-151">Krok 11: Włączanie replikacji</span><span class="sxs-lookup"><span data-stu-id="06f58-151">Step 11: Enable replication</span></span>

<span data-ttu-id="06f58-152">Po uruchomieniu usługi mobilności na maszynie Wirtualnej można włączyć dla niego replikację.</span><span class="sxs-lookup"><span data-stu-id="06f58-152">After the Mobility service is running on a VM you can enable replication for it.</span></span> <span data-ttu-id="06f58-153">Po włączeniu odbywa się Replikacja początkowa maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="06f58-153">After enabling, initial replication of the VM occurs.</span></span>

<span data-ttu-id="06f58-154">Przejdź do [krok 11: Włączanie replikacji](vmware-walkthrough-enable-replication.md)</span><span class="sxs-lookup"><span data-stu-id="06f58-154">Go to [Step 11: Enable replication](vmware-walkthrough-enable-replication.md)</span></span>

## <a name="step-12-run-a-test-failover"></a><span data-ttu-id="06f58-155">Krok 12: Uruchom test trybu failover</span><span class="sxs-lookup"><span data-stu-id="06f58-155">Step 12: Run a test failover</span></span>

<span data-ttu-id="06f58-156">Po zakończeniu replikacji początkowej, a replikacja różnicowa jest uruchomiony, możesz uruchomić test trybu failover, aby upewnić się, że wszystko działa zgodnie z oczekiwaniami.</span><span class="sxs-lookup"><span data-stu-id="06f58-156">After initial replication finishes, and delta replication is running, you can run a test failover to make sure everything works as expected.</span></span>

<span data-ttu-id="06f58-157">Przejdź do [krok 12: testować tryb failover](vmware-walkthrough-test-failover.md)</span><span class="sxs-lookup"><span data-stu-id="06f58-157">Go to [Step 12: Run a test failover](vmware-walkthrough-test-failover.md)</span></span>
