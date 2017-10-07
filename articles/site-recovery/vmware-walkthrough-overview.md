---
title: "aaaReplicate tooAzure maszyn wirtualnych VMware z usługą Azure Site Recovery | Dokumentacja firmy Microsoft"
description: "Zawiera omówienie kroków hello replikowania obciążeń uruchomionych na maszynach wirtualnych VMware tooAzure"
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
ms.openlocfilehash: 7104f67a3635b916048dcb61bca770c89f0c77fc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="replicate-vmware-vms-tooazure-with-site-recovery"></a><span data-ttu-id="565a1-103">Replikowanie maszyn wirtualnych VMware tooAzure z usługą Site Recovery</span><span class="sxs-lookup"><span data-stu-id="565a1-103">Replicate VMware VMs tooAzure with Site Recovery</span></span>

<span data-ttu-id="565a1-104">Ten artykuł zawiera omówienie hello kroki wymagane tooreplicate lokalnymi VMware maszyn wirtualnych tooAzure, przy użyciu hello [usługi Azure Site Recovery](site-recovery-overview.md) w hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="565a1-104">This article provides an overview of hello steps required tooreplicate on-premises VMware virtual machines tooAzure, using hello [Azure Site Recovery](site-recovery-overview.md) service in hello Azure portal.</span></span>


![Proces wdrażania](./media/vmware-walkthrough-overview/vmware-to-azure-process.png)

<span data-ttu-id="565a1-106">**Rysunek 1: Podsumowanie procesu wdrożenia**</span><span class="sxs-lookup"><span data-stu-id="565a1-106">**Figure 1: Deployment process summary**</span></span>

## <a name="step-1-review-architecture-and-prerequisites"></a><span data-ttu-id="565a1-107">Krok 1: Przegląd architektury i wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="565a1-107">Step 1: Review architecture and prerequisites</span></span>

<span data-ttu-id="565a1-108">Przed rozpoczęciem wdrażania, przejrzyj architektura scenariusza hello i upewnij się, że znasz wszystkie składniki hello należy toodeploy</span><span class="sxs-lookup"><span data-stu-id="565a1-108">Before you start deployment, review hello scenario architecture, and make sure you understand all hello components you need toodeploy</span></span>

<span data-ttu-id="565a1-109">Przejdź do zbyt[krok 1: Przejrzyj hello architektury](vmware-walkthrough-architecture.md)</span><span class="sxs-lookup"><span data-stu-id="565a1-109">Go too[Step 1: Review hello architecture](vmware-walkthrough-architecture.md)</span></span>


## <a name="step-2-review-prerequisites"></a><span data-ttu-id="565a1-110">Krok 2: Sprawdź wymagania wstępne dotyczące</span><span class="sxs-lookup"><span data-stu-id="565a1-110">Step 2: Review prerequisites</span></span>

<span data-ttu-id="565a1-111">Upewnij się, że hello wymagania wstępne zostały spełnione dla każdego składnika wdrażania:</span><span class="sxs-lookup"><span data-stu-id="565a1-111">Make sure you have hello prerequisites in place for each deployment component:</span></span>

- <span data-ttu-id="565a1-112">**Wymagania wstępne platformy Azure**: wymagane konto Microsoft Azure, sieci platformy Azure i kont magazynu.</span><span class="sxs-lookup"><span data-stu-id="565a1-112">**Azure prerequisites**: You need a Microsoft Azure account, Azure networks, and storage accounts.</span></span>
- <span data-ttu-id="565a1-113">**Składniki usługi Site Recovery lokalnymi**: należy komputera z uruchomionym systemem lokalnymi składnikami usługi Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="565a1-113">**On-premises Site Recovery components**: You need a machine running on-premises Site Recovery components.</span></span>
- <span data-ttu-id="565a1-114">**Lokalne wstępnych VMware**: należy tooset kont, dzięki czemu usługa Site Recovery mogą uzyskiwać dostęp do serwerów VMware i maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="565a1-114">**On-premises VMware prerequisites**: You need tooset up accounts so that Site Recovery can access VMware servers and VMs.</span></span>
- <span data-ttu-id="565a1-115">**Maszyny wirtualne replikowane**: maszyny wirtualne mają toocomply potrzeby tooreplicate z wymaganiami platformy Azure i mieć zainstalowanie składnika usługi Mobility hello.</span><span class="sxs-lookup"><span data-stu-id="565a1-115">**Replicated VMs**: VMs you want tooreplicate need toocomply with Azure requirements, and have hello Mobility service component installed.</span></span>

<span data-ttu-id="565a1-116">Przejdź do zbyt[krok 2: Przejrzyj wymagania wstępne i ograniczenia](vmware-walkthrough-prerequisites.md)</span><span class="sxs-lookup"><span data-stu-id="565a1-116">Go too[Step 2: Review prerequisites and limitations](vmware-walkthrough-prerequisites.md)</span></span>

## <a name="step-3-plan-capacity"></a><span data-ttu-id="565a1-117">Krok 3: Planowanie pojemności</span><span class="sxs-lookup"><span data-stu-id="565a1-117">Step 3: Plan capacity</span></span>

<span data-ttu-id="565a1-118">Jeśli pełne wdrożenie robimy należy toofigure się, jakie potrzebne zasoby replikacji.</span><span class="sxs-lookup"><span data-stu-id="565a1-118">If you're doing a full deployment you need toofigure out what replication resources you need.</span></span> <span data-ttu-id="565a1-119">Istnieje kilka z toohelp dostępne narzędzia można to zrobić.</span><span class="sxs-lookup"><span data-stu-id="565a1-119">There are a couple of tools available toohelp you do this.</span></span> <span data-ttu-id="565a1-120">Przejdź tooStep 2.</span><span class="sxs-lookup"><span data-stu-id="565a1-120">Go tooStep 2.</span></span> <span data-ttu-id="565a1-121">Jeśli podczas wykonywania szybkiego skonfigurowania środowiska hello tootest można pominąć ten krok.</span><span class="sxs-lookup"><span data-stu-id="565a1-121">If you're doing a quick set up tootest hello environment you can skip this step.</span></span>

<span data-ttu-id="565a1-122">Przejdź do zbyt[krok 3: Planowanie pojemności](vmware-walkthrough-capacity.md)</span><span class="sxs-lookup"><span data-stu-id="565a1-122">Go too[Step 3: Plan capacity](vmware-walkthrough-capacity.md)</span></span>

## <a name="step-4-plan-networking"></a><span data-ttu-id="565a1-123">Krok 4: Planowanie sieci</span><span class="sxs-lookup"><span data-stu-id="565a1-123">Step 4: Plan networking</span></span>

<span data-ttu-id="565a1-124">Należy toodo niektórych planowania tooensure czy maszynach wirtualnych platformy Azure są połączone toonetworks po pracy awaryjnej i czy mają one hello prawo adresów IP sieci.</span><span class="sxs-lookup"><span data-stu-id="565a1-124">You need toodo some network planning tooensure that Azure VMs are connected toonetworks after failover occurs, and  that that they have hello right IP addresses.</span></span>

<span data-ttu-id="565a1-125">Przejdź do zbyt[krok 4: Planowanie sieci](vmware-walkthrough-network.md)</span><span class="sxs-lookup"><span data-stu-id="565a1-125">Go too[Step 4: Plan networking](vmware-walkthrough-network.md)</span></span>

##  <a name="step-5-prepare-azure-resources"></a><span data-ttu-id="565a1-126">Krok 5: Przygotowanie zasobów platformy Azure</span><span class="sxs-lookup"><span data-stu-id="565a1-126">Step 5: Prepare Azure resources</span></span>

<span data-ttu-id="565a1-127">Konfigurowanie sieci platformy Azure i magazynu przed jego uruchomieniem.</span><span class="sxs-lookup"><span data-stu-id="565a1-127">Set up Azure networks and storage before you start.</span></span> <span data-ttu-id="565a1-128">Można to zrobić podczas wdrażania, ale zaleca się, że można to zrobić przed rozpoczęciem.</span><span class="sxs-lookup"><span data-stu-id="565a1-128">You can do this during deployment, but we recommend you do this before you start.</span></span>

<span data-ttu-id="565a1-129">Przejdź do zbyt[krok 5: przygotowanie Azure](vmware-walkthrough-prepare-azure.md)</span><span class="sxs-lookup"><span data-stu-id="565a1-129">Go too[Step 5: Prepare Azure](vmware-walkthrough-prepare-azure.md)</span></span>


## <a name="step-6-prepare-vmware"></a><span data-ttu-id="565a1-130">Krok 6: Przygotowanie VMware</span><span class="sxs-lookup"><span data-stu-id="565a1-130">Step 6: Prepare VMware</span></span>

<span data-ttu-id="565a1-131">Należy tooset kont używanych Site Recovery do:</span><span class="sxs-lookup"><span data-stu-id="565a1-131">You need tooset up accounts that Site Recovery will use to:</span></span>

- <span data-ttu-id="565a1-132">Tooautomatically serwerów wirtualizacji VMware dostępu wykryć maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="565a1-132">Access VMware virtualization servers tooautomatically detect VMs.</span></span>
- <span data-ttu-id="565a1-133">Dostęp do usługi mobilności hello tooinstall maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="565a1-133">Access VMs tooinstall hello Mobility service.</span></span> <span data-ttu-id="565a1-134">Każda maszyna wirtualna ma tooreplicate musi mieć agent usługi mobilności hello przed można włączyć dla niego replikację.</span><span class="sxs-lookup"><span data-stu-id="565a1-134">Each VM you want tooreplicate must have hello Mobility service agent installed before you can enable replication for it.</span></span>

<span data-ttu-id="565a1-135">Przejdź do zbyt[krok 6: przygotowanie VMware](vmware-walkthrough-prepare-vmware.md)</span><span class="sxs-lookup"><span data-stu-id="565a1-135">Go too[Step 6: Prepare VMware](vmware-walkthrough-prepare-vmware.md)</span></span>

## <a name="step-7-set-up-a-vault"></a><span data-ttu-id="565a1-136">Krok 7: Konfigurowanie magazynu</span><span class="sxs-lookup"><span data-stu-id="565a1-136">Step 7: Set up a vault</span></span>

<span data-ttu-id="565a1-137">Należy tooset się tooorchestrate magazyn usług odzyskiwania i Zarządzanie replikacją.</span><span class="sxs-lookup"><span data-stu-id="565a1-137">You need tooset up a Recovery Services vault tooorchestrate and manage replication.</span></span> <span data-ttu-id="565a1-138">Po skonfigurowaniu magazynu hello Określ sposób tooreplicate, i miejsce tooreplicate jej.</span><span class="sxs-lookup"><span data-stu-id="565a1-138">When you set up hello vault, you specify what you want tooreplicate, and where you want tooreplicate it to.</span></span>

<span data-ttu-id="565a1-139">Przejdź do zbyt[kroku 7: Konfigurowanie magazynu](vmware-walkthrough-create-vault.md)</span><span class="sxs-lookup"><span data-stu-id="565a1-139">Go too[Step 7: Set up a vault](vmware-walkthrough-create-vault.md)</span></span>

## <a name="step-8-configure-source-and-target-settings"></a><span data-ttu-id="565a1-140">Krok 8: Konfigurowanie ustawień źródłowa i docelowa</span><span class="sxs-lookup"><span data-stu-id="565a1-140">Step 8: Configure source and target settings</span></span>

<span data-ttu-id="565a1-141">Konfigurowanie hello źródłowy i docelowy, który jest używany do replikacji.</span><span class="sxs-lookup"><span data-stu-id="565a1-141">Set up hello source and target that's used for replication.</span></span> <span data-ttu-id="565a1-142">Konfigurowanie ustawień źródła obejmuje systemem składnikami usługi Site Recovery lokalne powitania tooinstall Unified Instalatora.</span><span class="sxs-lookup"><span data-stu-id="565a1-142">Setting up source settings includes running Unified Setup tooinstall hello on-premises Site Recovery components.</span></span>

<span data-ttu-id="565a1-143">Przejdź do zbyt[krok 8: Konfigurowanie hello źródłowa i docelowa](vmware-walkthrough-source-target.md)</span><span class="sxs-lookup"><span data-stu-id="565a1-143">Go too[Step 8: Set up hello source and target](vmware-walkthrough-source-target.md)</span></span>

## <a name="step-9-set-up-a-replication-policy"></a><span data-ttu-id="565a1-144">Krok 9: Konfigurowanie zasad replikacji</span><span class="sxs-lookup"><span data-stu-id="565a1-144">Step 9: Set up a replication policy</span></span>

<span data-ttu-id="565a1-145">Skonfigurowane ustawienia zasad toospecify replikacji w maszynach wirtualnych VMware w magazynie hello.</span><span class="sxs-lookup"><span data-stu-id="565a1-145">You set up a policy toospecify replication settings for VMware VMs in hello vault.</span></span>

<span data-ttu-id="565a1-146">Przejdź do zbyt[krok 9: Konfigurowanie zasad replikacji](vmware-walkthrough-replication.md)</span><span class="sxs-lookup"><span data-stu-id="565a1-146">Go too[Step 9: Set up a replication policy](vmware-walkthrough-replication.md)</span></span>

## <a name="step-10-install-hello-mobility-service"></a><span data-ttu-id="565a1-147">Krok 10: Zainstaluj usługę mobilności hello</span><span class="sxs-lookup"><span data-stu-id="565a1-147">Step 10: Install hello Mobility service</span></span>

<span data-ttu-id="565a1-148">musi być zainstalowany Hello usługi mobilności na każdej maszynie Wirtualnej ma tooreplicate.</span><span class="sxs-lookup"><span data-stu-id="565a1-148">hello Mobility service must be installed on each VM you want tooreplicate.</span></span> <span data-ttu-id="565a1-149">Istnieje kilka sposobów tooset usługi hello instalację wypychania i ściągania.</span><span class="sxs-lookup"><span data-stu-id="565a1-149">There are a few ways tooset up hello service with push or pull installation.</span></span>

<span data-ttu-id="565a1-150">Przejdź do zbyt[kroku 10: zainstalować usługi mobilności hello](vmware-walkthrough-install-mobility.md)</span><span class="sxs-lookup"><span data-stu-id="565a1-150">Go too[Step 10: Install hello Mobility service](vmware-walkthrough-install-mobility.md)</span></span>

## <a name="step-11-enable-replication"></a><span data-ttu-id="565a1-151">Krok 11: Włączanie replikacji</span><span class="sxs-lookup"><span data-stu-id="565a1-151">Step 11: Enable replication</span></span>

<span data-ttu-id="565a1-152">Po uruchomieniu hello usługi mobilności na maszynie Wirtualnej można włączyć dla niego replikację.</span><span class="sxs-lookup"><span data-stu-id="565a1-152">After hello Mobility service is running on a VM you can enable replication for it.</span></span> <span data-ttu-id="565a1-153">Po włączeniu replikacji początkowej dla maszyny Wirtualnej hello występuje.</span><span class="sxs-lookup"><span data-stu-id="565a1-153">After enabling, initial replication of hello VM occurs.</span></span>

<span data-ttu-id="565a1-154">Przejdź do zbyt[krok 11: Włączanie replikacji](vmware-walkthrough-enable-replication.md)</span><span class="sxs-lookup"><span data-stu-id="565a1-154">Go too[Step 11: Enable replication](vmware-walkthrough-enable-replication.md)</span></span>

## <a name="step-12-run-a-test-failover"></a><span data-ttu-id="565a1-155">Krok 12: Uruchom test trybu failover</span><span class="sxs-lookup"><span data-stu-id="565a1-155">Step 12: Run a test failover</span></span>

<span data-ttu-id="565a1-156">Po zakończeniu replikacji początkowej, a replikacja różnicowa jest uruchomiony, możesz uruchomić test pracy awaryjnej toomake się, że wszystko działa zgodnie z oczekiwaniami.</span><span class="sxs-lookup"><span data-stu-id="565a1-156">After initial replication finishes, and delta replication is running, you can run a test failover toomake sure everything works as expected.</span></span>

<span data-ttu-id="565a1-157">Przejdź do zbyt[krok 12: testować tryb failover](vmware-walkthrough-test-failover.md)</span><span class="sxs-lookup"><span data-stu-id="565a1-157">Go too[Step 12: Run a test failover](vmware-walkthrough-test-failover.md)</span></span>
