---
title: "aaaReplicate fizycznych tooAzure serwerów z usługą Azure Site Recovery lokalnymi | Dokumentacja firmy Microsoft"
description: "Zawiera omówienie kroków hello replikowania obciążenia uruchomione na lokalnym systemem Windows lub Linux serwerów fizycznych tooAzure z hello usługi Azure Site Recovery."
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: 20122f01-929a-4675-b85b-a9b99d2618bc
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/27/2017
ms.author: raynew
ms.openlocfilehash: f801b9544072d4029ec06cc1abfd4ff370e852e9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="replicate-physical-servers-tooazure-with-site-recovery"></a><span data-ttu-id="539c0-103">Replikowanie tooAzure serwery fizyczne z usługą Site Recovery</span><span class="sxs-lookup"><span data-stu-id="539c0-103">Replicate physical servers tooAzure with Site Recovery</span></span>

<span data-ttu-id="539c0-104">Ten artykuł zawiera omówienie hello kroki wymagane tooreplicate lokalnego systemu Windows i Linux serwerów fizycznych tooAzure, przy użyciu hello [usługi Azure Site Recovery](site-recovery-overview.md) w hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="539c0-104">This article provides an overview of hello steps required tooreplicate on-premises Windows/Linux physical servers tooAzure, using hello [Azure Site Recovery](site-recovery-overview.md) service in hello Azure portal.</span></span>


## <a name="step-1-review-architecture-and-prerequisites"></a><span data-ttu-id="539c0-105">Krok 1: Przegląd architektury i wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="539c0-105">Step 1: Review architecture and prerequisites</span></span>

<span data-ttu-id="539c0-106">Przed rozpoczęciem wdrażania, przejrzyj architektura scenariusza hello i upewnij się, że znasz wszystkie składniki hello należy tooset hello wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="539c0-106">Before you start deployment, review hello scenario architecture, and make sure you understand all hello components you need tooset up hello deployment.</span></span>

<span data-ttu-id="539c0-107">Przejdź do zbyt[krok 1: Przejrzyj hello architektury](physical-walkthrough-architecture.md)</span><span class="sxs-lookup"><span data-stu-id="539c0-107">Go too[Step 1: Review hello architecture](physical-walkthrough-architecture.md)</span></span>


## <a name="step-2-review-prerequisites"></a><span data-ttu-id="539c0-108">Krok 2: Sprawdź wymagania wstępne dotyczące</span><span class="sxs-lookup"><span data-stu-id="539c0-108">Step 2: Review prerequisites</span></span>

<span data-ttu-id="539c0-109">Upewnij się, że hello wymagania wstępne zostały spełnione dla każdego składnika wdrażania:</span><span class="sxs-lookup"><span data-stu-id="539c0-109">Make sure you have hello prerequisites in place for each deployment component:</span></span>

- <span data-ttu-id="539c0-110">**Wymagania wstępne platformy Azure**: wymagane konto Microsoft Azure, sieci platformy Azure i kont magazynu.</span><span class="sxs-lookup"><span data-stu-id="539c0-110">**Azure prerequisites**: You need a Microsoft Azure account, Azure networks, and storage accounts.</span></span>
- <span data-ttu-id="539c0-111">**Składniki usługi Site Recovery lokalnymi**: należy komputera z uruchomionym systemem lokalnymi składnikami usługi Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="539c0-111">**On-premises Site Recovery components**: You need a machine running on-premises Site Recovery components.</span></span>
- <span data-ttu-id="539c0-112">**Replikowane maszyny**: serwery mają tooreplicate muszą toocomply z lokalnymi i wymagania dotyczące usługi Azure.</span><span class="sxs-lookup"><span data-stu-id="539c0-112">**Replicated machines**: Servers you want tooreplicate need toocomply with on-premises and Azure requirements.</span></span>

<span data-ttu-id="539c0-113">Przejdź do zbyt[krok 2: Przejrzyj wymagania wstępne i ograniczenia](physical-walkthrough-prerequisites.md)</span><span class="sxs-lookup"><span data-stu-id="539c0-113">Go too[Step 2: Review prerequisites and limitations](physical-walkthrough-prerequisites.md)</span></span>

## <a name="step-3-plan-capacity"></a><span data-ttu-id="539c0-114">Krok 3: Planowanie pojemności</span><span class="sxs-lookup"><span data-stu-id="539c0-114">Step 3: Plan capacity</span></span>

<span data-ttu-id="539c0-115">Jeśli pełne wdrożenie robimy należy toofigure się, jakie potrzebne zasoby replikacji.</span><span class="sxs-lookup"><span data-stu-id="539c0-115">If you're doing a full deployment you need toofigure out what replication resources you need.</span></span> <span data-ttu-id="539c0-116">Jeśli podczas wykonywania szybkiego skonfigurowania środowiska hello tootest, możesz pominąć ten krok.</span><span class="sxs-lookup"><span data-stu-id="539c0-116">If you're doing a quick set up tootest hello environment, you can skip this step.</span></span>

<span data-ttu-id="539c0-117">Przejdź do zbyt[krok 3: Planowanie pojemności](physical-walkthrough-capacity.md)</span><span class="sxs-lookup"><span data-stu-id="539c0-117">Go too[Step 3: Plan capacity](physical-walkthrough-capacity.md)</span></span>

## <a name="step-4-plan-networking"></a><span data-ttu-id="539c0-118">Krok 4: Planowanie sieci</span><span class="sxs-lookup"><span data-stu-id="539c0-118">Step 4: Plan networking</span></span>

<span data-ttu-id="539c0-119">Należy toodo niektórych planowania tooensure czy maszynach wirtualnych platformy Azure są połączone toonetworks po pracy awaryjnej i czy mają one hello prawo adresów IP sieci.</span><span class="sxs-lookup"><span data-stu-id="539c0-119">You need toodo some network planning tooensure that Azure VMs are connected toonetworks after failover occurs, and  that that they have hello right IP addresses.</span></span>

<span data-ttu-id="539c0-120">Przejdź do zbyt[krok 4: Planowanie sieci](physical-walkthrough-network.md)</span><span class="sxs-lookup"><span data-stu-id="539c0-120">Go too[Step 4: Plan networking](physical-walkthrough-network.md)</span></span>

##  <a name="step-5-prepare-azure-resources"></a><span data-ttu-id="539c0-121">Krok 5: Przygotowanie zasobów platformy Azure</span><span class="sxs-lookup"><span data-stu-id="539c0-121">Step 5: Prepare Azure resources</span></span>

<span data-ttu-id="539c0-122">Konfigurowanie sieci platformy Azure i magazynu przed jego uruchomieniem.</span><span class="sxs-lookup"><span data-stu-id="539c0-122">Set up Azure networks and storage before you start.</span></span> 

<span data-ttu-id="539c0-123">Przejdź do zbyt[krok 5: przygotowanie Azure](physical-walkthrough-prepare-azure.md)</span><span class="sxs-lookup"><span data-stu-id="539c0-123">Go too[Step 5: Prepare Azure](physical-walkthrough-prepare-azure.md)</span></span>


## <a name="step-6-set-up-a-vault"></a><span data-ttu-id="539c0-124">Krok 6: Konfigurowanie magazynu</span><span class="sxs-lookup"><span data-stu-id="539c0-124">Step 6: Set up a vault</span></span>

<span data-ttu-id="539c0-125">Konfigurowanie tooorchestrate magazyn usług odzyskiwania i Zarządzanie replikacją.</span><span class="sxs-lookup"><span data-stu-id="539c0-125">You set up a Recovery Services vault tooorchestrate and manage replication.</span></span> <span data-ttu-id="539c0-126">Po skonfigurowaniu magazynu hello Określ sposób tooreplicate, i miejsce tooreplicate jej.</span><span class="sxs-lookup"><span data-stu-id="539c0-126">When you set up hello vault, you specify what you want tooreplicate, and where you want tooreplicate it to.</span></span>

<span data-ttu-id="539c0-127">Przejdź do zbyt[krok 6: Konfigurowanie magazynu](physical-walkthrough-create-vault.md)</span><span class="sxs-lookup"><span data-stu-id="539c0-127">Go too[Step 6: Set up a vault](physical-walkthrough-create-vault.md)</span></span>

## <a name="step-7-configure-source-and-target-settings"></a><span data-ttu-id="539c0-128">Krok 7: Konfigurowanie ustawień źródłowa i docelowa</span><span class="sxs-lookup"><span data-stu-id="539c0-128">Step 7: Configure source and target settings</span></span>

<span data-ttu-id="539c0-129">Skonfiguruj ustawienia hello źródłowej i docelowej (Azure).</span><span class="sxs-lookup"><span data-stu-id="539c0-129">Configure settings for hello source and target (Azure) site.</span></span> <span data-ttu-id="539c0-130">Ustawienia źródła obejmuje systemem składnikami usługi Site Recovery lokalne powitania tooinstall Unified Instalatora.</span><span class="sxs-lookup"><span data-stu-id="539c0-130">Source settings includes running Unified Setup tooinstall hello on-premises Site Recovery components.</span></span>

<span data-ttu-id="539c0-131">Przejdź do zbyt[kroku 7: Konfigurowanie hello źródłowa i docelowa](physical-walkthrough-source-target.md)</span><span class="sxs-lookup"><span data-stu-id="539c0-131">Go too[Step 7: Set up hello source and target](physical-walkthrough-source-target.md)</span></span>

## <a name="step-8-set-up-a-replication-policy"></a><span data-ttu-id="539c0-132">Krok 8: Konfigurowanie zasad replikacji</span><span class="sxs-lookup"><span data-stu-id="539c0-132">Step 8: Set up a replication policy</span></span>

<span data-ttu-id="539c0-133">Skonfigurowaniu toospecify zasad jak fizycznych serwerów należy replikować.</span><span class="sxs-lookup"><span data-stu-id="539c0-133">You set up a policy toospecify how physical servers should replicate.</span></span>

<span data-ttu-id="539c0-134">Przejdź do zbyt[krok 8: Konfigurowanie zasad replikacji](physical-walkthrough-replication.md)</span><span class="sxs-lookup"><span data-stu-id="539c0-134">Go too[Step 8: Set up a replication policy](physical-walkthrough-replication.md)</span></span>

## <a name="step-9-install-hello-mobility-service"></a><span data-ttu-id="539c0-135">Krok 9: Instalowanie usługi mobilności hello</span><span class="sxs-lookup"><span data-stu-id="539c0-135">Step 9: Install hello Mobility service</span></span>

<span data-ttu-id="539c0-136">Witaj usługi mobilności musi być zainstalowany na każdym serwerze ma tooreplicate.</span><span class="sxs-lookup"><span data-stu-id="539c0-136">hello Mobility service must be installed on each server you want tooreplicate.</span></span> <span data-ttu-id="539c0-137">Istnieje kilka sposobów tooset usługi hello, instalację wypychania i ściągania.</span><span class="sxs-lookup"><span data-stu-id="539c0-137">There are a few ways tooset up hello service, with push or pull installation.</span></span>

<span data-ttu-id="539c0-138">Przejdź zbyt[krok 9: Instalowanie usługi mobilności hello](physical-walkthrough-install-mobility.md)</span><span class="sxs-lookup"><span data-stu-id="539c0-138">Go too[Step 9: Install hello Mobility service](physical-walkthrough-install-mobility.md)</span></span>

## <a name="step-10-enable-replication"></a><span data-ttu-id="539c0-139">Krok 10: Włączanie replikacji</span><span class="sxs-lookup"><span data-stu-id="539c0-139">Step 10: Enable replication</span></span>

<span data-ttu-id="539c0-140">Po hello usługa mobilności jest uruchomiona na serwerze, można włączyć dla niego replikację.</span><span class="sxs-lookup"><span data-stu-id="539c0-140">After hello Mobility service is running on a server, you can enable replication for it.</span></span> <span data-ttu-id="539c0-141">Po włączeniu replikacji początkowej dla maszyny Wirtualnej hello występuje.</span><span class="sxs-lookup"><span data-stu-id="539c0-141">After enabling, initial replication of hello VM occurs.</span></span>

<span data-ttu-id="539c0-142">Przejdź do zbyt[kroku 10: Włączanie replikacji](physical-walkthrough-enable-replication.md)</span><span class="sxs-lookup"><span data-stu-id="539c0-142">Go too[Step 10: Enable replication](physical-walkthrough-enable-replication.md)</span></span>

## <a name="step-11-run-a-test-failover"></a><span data-ttu-id="539c0-143">Krok 11: Uruchom test trybu failover</span><span class="sxs-lookup"><span data-stu-id="539c0-143">Step 11: Run a test failover</span></span>

<span data-ttu-id="539c0-144">Po zakończeniu replikacji początkowej i działa replikacja różnicowa, możesz uruchomić test trybu failover toomake się, że wszystko działa zgodnie z oczekiwaniami.</span><span class="sxs-lookup"><span data-stu-id="539c0-144">After initial replication finishes and delta replication is running, you can run a test failover toomake sure everything works as expected.</span></span>

<span data-ttu-id="539c0-145">Przejdź do zbyt[krok 11: testować tryb failover](physical-walkthrough-test-failover.md)</span><span class="sxs-lookup"><span data-stu-id="539c0-145">Go too[Step 11: Run a test failover](physical-walkthrough-test-failover.md)</span></span>

