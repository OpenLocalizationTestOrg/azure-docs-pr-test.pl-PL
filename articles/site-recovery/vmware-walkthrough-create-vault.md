---
title: "aaaSet się magazynu dla VMware tooAzure replikacji przy użyciu usługi Azure Site Recovery | Dokumentacja firmy Microsoft"
description: "Zawiera podsumowanie kroków hello potrzebne tooset się magazynu dla VMware tooAzure replikacji przy użyciu usługi Azure Site Recovery"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: 8bce940e-f19f-4418-8360-aee7b073519a
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/27/2017
ms.author: raynew
ms.openlocfilehash: 8a7755a6c9a3f55f241c615e425285bc4b782493
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="step-7-set-up-a-vault-for-vmware-replication-tooazure"></a><span data-ttu-id="2d64b-103">Krok 7: Konfigurowanie magazynu dla tooAzure replikacji VMware</span><span class="sxs-lookup"><span data-stu-id="2d64b-103">Step 7: Set up a vault for VMware replication tooAzure</span></span>


<span data-ttu-id="2d64b-104">W tym artykule opisano sposób tooset Konfigurowanie magazynu i określ sposób tooreplicate z lokalizacji lokalnej, za pomocą hello tooAzure [usługi Azure Site Recovery](site-recovery-overview.md) w hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="2d64b-104">This article describes how tooset up a vault, and specify what you want tooreplicate from your on-premises location, tooAzure using hello [Azure Site Recovery](site-recovery-overview.md) service in hello Azure portal.</span></span>


<span data-ttu-id="2d64b-105">Opublikuj komentarze i pytania u dołu hello w tym artykule, albo na powitania [Forum usług odzyskiwania Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="2d64b-105">Post comments and questions at hello bottom of this article, or on hello [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>




## <a name="create-a-recovery-services-vault"></a><span data-ttu-id="2d64b-106">Tworzenie magazynu Usług odzyskiwania</span><span class="sxs-lookup"><span data-stu-id="2d64b-106">Create a Recovery Services vault</span></span>

[!INCLUDE [site-recovery-create-vault](../../includes/site-recovery-create-vault.md)]

## <a name="select-a-protection-goal"></a><span data-ttu-id="2d64b-107">Wybierz cel ochrony</span><span class="sxs-lookup"><span data-stu-id="2d64b-107">Select a protection goal</span></span>

<span data-ttu-id="2d64b-108">Wybierz, co ma tooreplicate, i miejsce tooreplicate do.</span><span class="sxs-lookup"><span data-stu-id="2d64b-108">Select what you want tooreplicate, and where you want tooreplicate to.</span></span>

1. <span data-ttu-id="2d64b-109">Kliknij przycisk **Magazyny usług odzyskiwania** > magazynu.</span><span class="sxs-lookup"><span data-stu-id="2d64b-109">Click **Recovery Services vaults** > vault.</span></span>
2. <span data-ttu-id="2d64b-110">W Menu zasobów hello, kliknij przycisk **usługi Site Recovery** > **przygotowanie infrastruktury** > **cel ochrony**.</span><span class="sxs-lookup"><span data-stu-id="2d64b-110">In hello Resource Menu, click **Site Recovery** > **Prepare Infrastructure** > **Protection goal**.</span></span>
3. <span data-ttu-id="2d64b-111">W **cel ochrony**, wybierz pozycję **tooAzure** > **tak, z programem VMware vSphere Hypervisor**.</span><span class="sxs-lookup"><span data-stu-id="2d64b-111">In **Protection goal**, select **tooAzure** > **Yes, with VMware vSphere Hypervisor**.</span></span>



## <a name="next-steps"></a><span data-ttu-id="2d64b-112">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="2d64b-112">Next steps</span></span>

<span data-ttu-id="2d64b-113">Przejdź do zbyt[krok 8: Konfigurowanie źródłowa i docelowa](vmware-walkthrough-source-target.md)</span><span class="sxs-lookup"><span data-stu-id="2d64b-113">Go too[Step 8: Set up source and target](vmware-walkthrough-source-target.md)</span></span>
