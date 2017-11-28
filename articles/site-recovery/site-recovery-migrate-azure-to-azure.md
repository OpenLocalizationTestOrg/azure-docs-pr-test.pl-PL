---
title: "aaaMigrate maszyn wirtualnych IaaS platformy Azure między regiony platformy Azure | Dokumentacja firmy Microsoft"
description: "Użyj maszyn wirtualnych Azure IaaS toomigrate usługi Azure Site Recovery z jednego tooanother region platformy Azure."
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: jwhit
editor: tysonn
ms.assetid: 8a29e0d9-0010-4739-972f-02b8bdf360f6
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/14/2017
ms.author: raynew
ms.openlocfilehash: c84dc77716b8d19969eab60707ed1332ca39b893
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="migrate-azure-iaas-virtual-machines-between-azure-regions-with-azure-site-recovery"></a><span data-ttu-id="5f7b6-103">Migracja maszyn wirtualnych Azure IaaS między regiony platformy Azure z usługą Azure Site Recovery</span><span class="sxs-lookup"><span data-stu-id="5f7b6-103">Migrate Azure IaaS virtual machines between Azure regions with Azure Site Recovery</span></span>
## <a name="overview"></a><span data-ttu-id="5f7b6-104">Omówienie</span><span class="sxs-lookup"><span data-stu-id="5f7b6-104">Overview</span></span>
<span data-ttu-id="5f7b6-105">Usługa Site Recovery tooAzure Zapraszamy!</span><span class="sxs-lookup"><span data-stu-id="5f7b6-105">Welcome tooAzure Site Recovery!</span></span> <span data-ttu-id="5f7b6-106">W tym artykule należy użyć, jeśli maszyny wirtualne Azure toomigrate między regiony platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="5f7b6-106">Use this article if you want toomigrate Azure VMs between Azure regions.</span></span> <span data-ttu-id="5f7b6-107">Przed rozpoczęciem należy pamiętać, że:</span><span class="sxs-lookup"><span data-stu-id="5f7b6-107">Before you start, note that:</span></span>

* <span data-ttu-id="5f7b6-108">Platforma Azure ma dwa różne modele wdrażania do tworzenia i pracy z zasobami: Azure Resource Manager i model klasyczny.</span><span class="sxs-lookup"><span data-stu-id="5f7b6-108">Azure has two different deployment models for creating and working with resources: Azure Resource Manager and classic.</span></span> <span data-ttu-id="5f7b6-109">Azure ma dwa portale — klasyczny portal Azure obsługującym hello klasycznego modelu wdrażania hello i hello portalu Azure z obsługą oba modele wdrażania.</span><span class="sxs-lookup"><span data-stu-id="5f7b6-109">Azure also has two portals – hello Azure classic portal that supports hello classic deployment model, and hello Azure portal with support for both deployment models.</span></span> <span data-ttu-id="5f7b6-110">Witaj podstawowe kroki migracji są hello sama czy w przypadku konfigurowania usługi Site Recovery w Menedżerze zasobów lub w klasycznym.</span><span class="sxs-lookup"><span data-stu-id="5f7b6-110">hello basic steps for migration are hello same whether you're configuring Site Recovery in Resource Manager or in classic.</span></span> <span data-ttu-id="5f7b6-111">Jednak hello instrukcje interfejsu użytkownika i zrzuty ekranu w tym artykule dotyczą hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="5f7b6-111">However hello UI instructions and screenshots in this article are relevant for hello Azure portal.</span></span>
* <span data-ttu-id="5f7b6-112">**Obecnie można wykonywać migrację tylko z jednego regionu tooanother. Możesz w trybie Failover maszyny wirtualne z jednego tooanother region platformy Azure, ale nie jest możliwy ich powrót ponownie.**</span><span class="sxs-lookup"><span data-stu-id="5f7b6-112">**Currently you can only migrate from one region tooanother. You can fail over VMs from one Azure region tooanother, but you can't fail them back again.**</span></span>

<span data-ttu-id="5f7b6-113">Zamieść wszelkie komentarze lub pytania u dołu hello w tym artykule, albo na powitania [Forum usług odzyskiwania Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="5f7b6-113">Post any comments or questions at hello bottom of this article, or on hello [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5f7b6-114">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="5f7b6-114">Prerequisites</span></span>
<span data-ttu-id="5f7b6-115">Oto, co jest potrzebne dla tego wdrożenia:</span><span class="sxs-lookup"><span data-stu-id="5f7b6-115">Here's what you need for this deployment:</span></span>

* <span data-ttu-id="5f7b6-116">**Maszyny wirtualne IaaS**: hello ma toomigrate maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="5f7b6-116">**IaaS virtual machines**: hello VMs you want toomigrate.</span></span> <span data-ttu-id="5f7b6-117">Należy przeprowadzić migrację tych maszyn wirtualnych, traktując je jako maszyn fizycznych.</span><span class="sxs-lookup"><span data-stu-id="5f7b6-117">You migrate these VMs by treating them as physical machines.</span></span>

## <a name="deployment-steps"></a><span data-ttu-id="5f7b6-118">Kroki wdrażania</span><span class="sxs-lookup"><span data-stu-id="5f7b6-118">Deployment steps</span></span>
<span data-ttu-id="5f7b6-119">W tej sekcji opisano kroki wdrażania hello hello nowego portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="5f7b6-119">This section describes hello deployment steps in hello new Azure portal.</span></span>

1. <span data-ttu-id="5f7b6-120">[Tworzenie magazynu](site-recovery-vmware-to-azure.md).</span><span class="sxs-lookup"><span data-stu-id="5f7b6-120">[Create a vault](site-recovery-vmware-to-azure.md).</span></span>
2. <span data-ttu-id="5f7b6-121">[Włącz replikację](site-recovery-vmware-to-azure.md).</span><span class="sxs-lookup"><span data-stu-id="5f7b6-121">[Enable replication](site-recovery-vmware-to-azure.md).</span></span> <span data-ttu-id="5f7b6-122">Włącz replikację hello maszyn wirtualnych toomigrate, a następnie wybierz pozycję Azure jako źródła.</span><span class="sxs-lookup"><span data-stu-id="5f7b6-122">Enable replication for hello VMs you want toomigrate, and choose Azure as source.</span></span> 
3. <span data-ttu-id="5f7b6-123">[Uruchomić nieplanowany tryb failover](site-recovery-failover.md).</span><span class="sxs-lookup"><span data-stu-id="5f7b6-123">[ Run an unplanned failover](site-recovery-failover.md).</span></span> <span data-ttu-id="5f7b6-124">Po zakończeniu replikacji początkowej można uruchomić nieplanowanego trybu failover z jednym tooanother region platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="5f7b6-124">After initial replication is complete, you can run an unplanned failover from one Azure region tooanother.</span></span> <span data-ttu-id="5f7b6-125">Opcjonalnie możesz utworzyć plan odzyskiwania i uruchomić nieplanowanego trybu failover, toomigrate wiele maszyn wirtualnych między regionami.</span><span class="sxs-lookup"><span data-stu-id="5f7b6-125">Optionally, you can create a recovery plan and run an unplanned failover, toomigrate multiple virtual machines between regions.</span></span> <span data-ttu-id="5f7b6-126">[Dowiedz się więcej](site-recovery-create-recovery-plans.md) o planach odzyskiwania.</span><span class="sxs-lookup"><span data-stu-id="5f7b6-126">[Learn more](site-recovery-create-recovery-plans.md) about recovery plans.</span></span>

## <a name="next-steps"></a><span data-ttu-id="5f7b6-127">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="5f7b6-127">Next steps</span></span>
<span data-ttu-id="5f7b6-128">Dowiedz się więcej o innych scenariuszy replikacji w [co to jest Azure Site Recovery?](site-recovery-overview.md)</span><span class="sxs-lookup"><span data-stu-id="5f7b6-128">Learn more about other replication scenarios in [What is Azure Site Recovery?](site-recovery-overview.md)</span></span>
