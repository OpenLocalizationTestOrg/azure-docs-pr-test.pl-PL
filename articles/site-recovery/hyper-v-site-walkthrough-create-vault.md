---
title: "aaaSet się magazynu dla funkcji Hyper-V tooAzure replikacji (bez programu System Center VMM) przy użyciu usługi Azure Site Recovery | Dokumentacja firmy Microsoft"
description: "Zawiera podsumowanie kroków hello potrzebne tooset się magazynu dla tooAzure replikacji funkcji Hyper-V za pomocą usługi Azure Site Recovery"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: a936b3e2-0dbe-47ac-a98e-5285d96dc786
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 06/22/2017
ms.author: raynew
ms.openlocfilehash: e3ef8758faab36d19d0968d98a23105bed7830f6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="step-7-set-up-a-vault-for-hyper-v-replication"></a><span data-ttu-id="ff8fe-103">Krok 7: Konfigurowanie magazynu dla replikacji funkcji Hyper-V</span><span class="sxs-lookup"><span data-stu-id="ff8fe-103">Step 7: Set up a vault for Hyper-V replication</span></span>

<span data-ttu-id="ff8fe-104">W tym artykule opisano sposób tooset Konfigurowanie magazynu i określ sposób tooreplicate z lokalizacji lokalnej, za pomocą hello tooAzure [usługi Azure Site Recovery](site-recovery-overview.md) w hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="ff8fe-104">This article describes how tooset up a vault, and specify what you want tooreplicate from your on-premises location, tooAzure using hello [Azure Site Recovery](site-recovery-overview.md) service in hello Azure portal.</span></span>


<span data-ttu-id="ff8fe-105">Opublikuj komentarze i pytania u dołu hello w tym artykule, albo na powitania [Forum usług odzyskiwania Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="ff8fe-105">Post comments and questions at hello bottom of this article, or on hello [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>

## <a name="create-a-recovery-services-vault"></a><span data-ttu-id="ff8fe-106">Tworzenie magazynu Usług odzyskiwania</span><span class="sxs-lookup"><span data-stu-id="ff8fe-106">Create a Recovery Services vault</span></span>

[!INCLUDE [site-recovery-create-vault](../../includes/site-recovery-create-vault.md)]



## <a name="select-a-protection-goal"></a><span data-ttu-id="ff8fe-107">Wybierz cel ochrony</span><span class="sxs-lookup"><span data-stu-id="ff8fe-107">Select a protection goal</span></span>

<span data-ttu-id="ff8fe-108">Wybierz, co ma tooreplicate, i miejsce tooreplicate do.</span><span class="sxs-lookup"><span data-stu-id="ff8fe-108">Select what you want tooreplicate, and where you want tooreplicate to.</span></span>

1. <span data-ttu-id="ff8fe-109">Kliknij przycisk **Magazyny usług odzyskiwania** > magazynu.</span><span class="sxs-lookup"><span data-stu-id="ff8fe-109">Click **Recovery Services vaults** > vault.</span></span>
2. <span data-ttu-id="ff8fe-110">W Menu zasobów hello, kliknij przycisk **usługi Site Recovery** > **przygotowanie infrastruktury** > **cel ochrony**.</span><span class="sxs-lookup"><span data-stu-id="ff8fe-110">In hello Resource Menu, click **Site Recovery** > **Prepare Infrastructure** > **Protection goal**.</span></span>
3. <span data-ttu-id="ff8fe-111">W **cel ochrony**, wybierz pozycję **tooAzure** > **tak, z funkcją Hyper-V**.</span><span class="sxs-lookup"><span data-stu-id="ff8fe-111">In **Protection goal**, select **tooAzure** > **Yes, with Hyper-V**.</span></span> <span data-ttu-id="ff8fe-112">Wybierz **nr** tooconfirm nie używasz programu VMM.</span><span class="sxs-lookup"><span data-stu-id="ff8fe-112">Select **No** tooconfirm you're not using VMM.</span></span> 

    ![Wybieranie celów](./media/hyper-v-site-walkthrough-create-vault/choose-goals2.png)



## <a name="next-steps"></a><span data-ttu-id="ff8fe-114">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="ff8fe-114">Next steps</span></span>

<span data-ttu-id="ff8fe-115">Przejdź do zbyt[krok 8: Konfigurowanie źródłowa i docelowa](hyper-v-site-walkthrough-source-target.md)</span><span class="sxs-lookup"><span data-stu-id="ff8fe-115">Go too[Step 8: Set up source and target](hyper-v-site-walkthrough-source-target.md)</span></span>
