---
title: "aaaReplicate maszynach wirtualnych platformy Azure między regiony platformy Azure | Dokumentacja firmy Microsoft"
description: "Podsumowanie hello kroki wymagane tooreplicate maszynach wirtualnych platformy Azure między regiony platformy Azure z usługą Azure Site Recovery hello w hello portalu Azure"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmon
editor: 
ms.assetid: 6dd36239-4363-4538-bf80-a18e71b8ec67
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/01/2017
ms.author: raynew
ms.openlocfilehash: f4ac386f040945131f8a10f02143437f4441e298
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="replicate-azure-vms-between-regions-with-azure-site-recovery"></a><span data-ttu-id="83468-103">Replikowanie maszyn wirtualnych Azure między regionami z usługą Azure Site Recovery</span><span class="sxs-lookup"><span data-stu-id="83468-103">Replicate Azure VMs between regions with Azure Site Recovery</span></span>

><span data-ttu-id="83468-104">Ten artykuł zawiera omówienie tooreplicate wymagane kroki hello Azure maszynach wirtualnych (VM) w jednym regionie Azure tooAzure maszyn wirtualnych w innym regionie.</span><span class="sxs-lookup"><span data-stu-id="83468-104">This article provides an overview of hello steps required tooreplicate Azure virtual machines (VMs) in one Azure region tooAzure VMs in a different region.</span></span> 

>[!NOTE]
>
> <span data-ttu-id="83468-105">Replikacja maszyny Wirtualnej platformy Azure jest obecnie w przeglądzie.</span><span class="sxs-lookup"><span data-stu-id="83468-105">Azure VM replication is currently in preview.</span></span>

<span data-ttu-id="83468-106">Opublikuj komentarze i pytania u dołu hello tym artykułem lub na powitania [forum usług odzyskiwania Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="83468-106">Post comments and questions at hello bottom of this article or on hello [Azure Recovery Services forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>

## <a name="step-1-review-architecture"></a><span data-ttu-id="83468-107">Krok 1: Przegląd architektury</span><span class="sxs-lookup"><span data-stu-id="83468-107">Step 1: Review architecture</span></span>

<span data-ttu-id="83468-108">Przed rozpoczęciem wdrażania zapoznaj się hello scenariusz architektury i składników hello należy toodeploy.</span><span class="sxs-lookup"><span data-stu-id="83468-108">Before you start deployment, review hello scenario architecture, and hello components you need toodeploy.</span></span>

<span data-ttu-id="83468-109">Przejdź do zbyt[krok 1: Przejrzyj hello architektury](azure-to-azure-walkthrough-architecture.md)</span><span class="sxs-lookup"><span data-stu-id="83468-109">Go too[Step 1: Review hello architecture](azure-to-azure-walkthrough-architecture.md)</span></span>


## <a name="step-2-review-prerequisites"></a><span data-ttu-id="83468-110">Krok 2: Sprawdź wymagania wstępne dotyczące</span><span class="sxs-lookup"><span data-stu-id="83468-110">Step 2: Review prerequisites</span></span>

<span data-ttu-id="83468-111">Sprawdź, czy ma hello Azure wymagania wstępne w miejscach, w tym subskrypcji, sieci wirtualne, konta magazynu i wymagania dotyczące maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="83468-111">Check that you have hello Azure prerequisites in places, including a subscription, virtual networks, storage accounts, and VM requirements.</span></span>

<span data-ttu-id="83468-112">Przejdź do zbyt[krok 2: Sprawdź wymagania wstępne i ograniczenia](azure-to-azure-walkthrough-prerequisites.md)</span><span class="sxs-lookup"><span data-stu-id="83468-112">Go too[Step 2: Verify prerequisites and limitations](azure-to-azure-walkthrough-prerequisites.md)</span></span>


## <a name="step-3-plan-networking"></a><span data-ttu-id="83468-113">Krok 3: Planowanie sieci</span><span class="sxs-lookup"><span data-stu-id="83468-113">Step 3: Plan networking</span></span>

<span data-ttu-id="83468-114">Sprawdź, czy łączność wychodząca jest skonfigurowany na maszynach wirtualnych Azure ma tooreplicate i że zostały skonfigurowane połączenia z lokalnym.</span><span class="sxs-lookup"><span data-stu-id="83468-114">Check that outbound connectivity is set up on Azure VMs you want tooreplicate, and that connections from on-premises are set up.</span></span>

<span data-ttu-id="83468-115">Przejdź do zbyt[krok 4: Planowanie sieci](azure-to-azure-walkthrough-network.md)</span><span class="sxs-lookup"><span data-stu-id="83468-115">Go too[Step 4: Plan networking](azure-to-azure-walkthrough-network.md)</span></span>



## <a name="step-4-create-a-vault"></a><span data-ttu-id="83468-116">Krok 4: Tworzenie magazynu</span><span class="sxs-lookup"><span data-stu-id="83468-116">Step 4: Create a vault</span></span> 

<span data-ttu-id="83468-117">Należy tooset się tooorchestrate magazyn usług odzyskiwania i Zarządzanie replikacją i określ region źródła hello.</span><span class="sxs-lookup"><span data-stu-id="83468-117">You need tooset up a Recovery Services vault tooorchestrate and manage replication, and specify hello source region.</span></span>

<span data-ttu-id="83468-118">Przejdź do zbyt[krok 4: Tworzenie magazynu](azure-to-azure-walkthrough-vault.md)</span><span class="sxs-lookup"><span data-stu-id="83468-118">Go too[Step 4: Create a vault](azure-to-azure-walkthrough-vault.md)</span></span>


## <a name="step-5-enable-replication"></a><span data-ttu-id="83468-119">Krok 5: Włączanie replikacji</span><span class="sxs-lookup"><span data-stu-id="83468-119">Step 5: Enable replication</span></span>


<span data-ttu-id="83468-120">Replikacja tooenable, skonfigurować ustawienia lokalizacji docelowej, skonfigurować zasady replikacji i wybierz hello maszynach wirtualnych platformy Azure, które mają tooreplicate.</span><span class="sxs-lookup"><span data-stu-id="83468-120">tooenable replication, you configure target location settings, set up a replication policy, and select hello Azure VMs that you want tooreplicate.</span></span> <span data-ttu-id="83468-121">Po włączeniu replikacji początkowej dla maszyny Wirtualnej hello występuje.</span><span class="sxs-lookup"><span data-stu-id="83468-121">After enabling, initial replication of hello VM occurs.</span></span>

<span data-ttu-id="83468-122">Przejdź do zbyt[krok 5: Włączanie replikacji](azure-to-azure-walkthrough-enable-replication.md)</span><span class="sxs-lookup"><span data-stu-id="83468-122">Go too[Step 5: Enable replication](azure-to-azure-walkthrough-enable-replication.md)</span></span>


## <a name="step-6-run-a-test-failover"></a><span data-ttu-id="83468-123">Krok 6: Uruchamianie testowego trybu failover</span><span class="sxs-lookup"><span data-stu-id="83468-123">Step 6: Run a test failover</span></span>

<span data-ttu-id="83468-124">Po zakończeniu replikacji początkowej, a replikacja różnicowa jest uruchomiony, możesz uruchomić test pracy awaryjnej toomake się, że wszystko działa zgodnie z oczekiwaniami.</span><span class="sxs-lookup"><span data-stu-id="83468-124">After initial replication finishes, and delta replication is running, you can run a test failover toomake sure everything works as expected.</span></span>

<span data-ttu-id="83468-125">Przejdź do zbyt[krok 6: testować tryb failover](azure-to-azure-walkthrough-test-failover.md)</span><span class="sxs-lookup"><span data-stu-id="83468-125">Go too[Step 6: Run a test failover](azure-to-azure-walkthrough-test-failover.md)</span></span>


