---
title: "aaaSet się magazynu dla funkcji Hyper-V tooAzure replikacji (z programu System Center VMM) przy użyciu usługi Azure Site Recovery | Dokumentacja firmy Microsoft"
description: "Zawiera podsumowanie kroków hello potrzebne tooset się magazynu dla funkcji Hyper-V tooAzure replikacji (w programie VMM) przy użyciu usługi Azure Site Recovery"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: b3cd6f03-c33c-406d-91d4-5cba69f79abd
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 07/23/2017
ms.author: raynew
ms.openlocfilehash: f2c90f3c8b0a48db1e57fefd9829d29cffff8d43
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="step-7-set-up-a-vault-for-hyper-v-replication"></a><span data-ttu-id="cf379-103">Krok 7: Konfigurowanie magazynu dla replikacji funkcji Hyper-V</span><span class="sxs-lookup"><span data-stu-id="cf379-103">Step 7: Set up a vault for Hyper-V replication</span></span>

<span data-ttu-id="cf379-104">W tym artykule opisano sposób tooset Konfigurowanie magazynu i określ sposób tooreplicate z lokalizacji lokalnej, za pomocą hello tooAzure [usługi Azure Site Recovery](site-recovery-overview.md) w hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="cf379-104">This article describes how tooset up a vault, and specify what you want tooreplicate from your on-premises location, tooAzure using hello [Azure Site Recovery](site-recovery-overview.md) service in hello Azure portal.</span></span>


<span data-ttu-id="cf379-105">Opublikuj komentarze i pytania u dołu hello w tym artykule, albo na powitania [Forum usług odzyskiwania Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="cf379-105">Post comments and questions at hello bottom of this article, or on hello [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>

## <a name="create-a-recovery-services-vault"></a><span data-ttu-id="cf379-106">Tworzenie magazynu Usług odzyskiwania</span><span class="sxs-lookup"><span data-stu-id="cf379-106">Create a Recovery Services vault</span></span>

[!INCLUDE [site-recovery-create-vault](../../includes/site-recovery-create-vault.md)]



## <a name="select-a-protection-goal"></a><span data-ttu-id="cf379-107">Wybierz cel ochrony</span><span class="sxs-lookup"><span data-stu-id="cf379-107">Select a protection goal</span></span>

<span data-ttu-id="cf379-108">Wybierz, co ma tooreplicate, i miejsce tooreplicate do.</span><span class="sxs-lookup"><span data-stu-id="cf379-108">Select what you want tooreplicate, and where you want tooreplicate to.</span></span>

1. <span data-ttu-id="cf379-109">Kliknij przycisk **Magazyny usług odzyskiwania** > magazynu.</span><span class="sxs-lookup"><span data-stu-id="cf379-109">Click **Recovery Services vaults** > vault.</span></span>
2. <span data-ttu-id="cf379-110">W Menu zasobów hello, kliknij przycisk **usługi Site Recovery** > **przygotowanie infrastruktury** > **cel ochrony**.</span><span class="sxs-lookup"><span data-stu-id="cf379-110">In hello Resource Menu, click **Site Recovery** > **Prepare Infrastructure** > **Protection goal**.</span></span>
3. <span data-ttu-id="cf379-111">W **cel ochrony**, wybierz pozycję **tooAzure** > **tak, z funkcją Hyper-V**.</span><span class="sxs-lookup"><span data-stu-id="cf379-111">In **Protection goal**, select **tooAzure** > **Yes, with Hyper-V**.</span></span> <span data-ttu-id="cf379-112">Wybierz **tak** tooconfirm jesteś %1./nOdnosi VMM.</span><span class="sxs-lookup"><span data-stu-id="cf379-112">Select **Yes** tooconfirm you're nusing VMM.</span></span> 

     ![Wybieranie celów](./media/vmm-to-azure-walkthrough-create-vault/choose-goals.png)



## <a name="next-steps"></a><span data-ttu-id="cf379-114">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="cf379-114">Next steps</span></span>

<span data-ttu-id="cf379-115">Przejdź do zbyt[krok 8: Konfigurowanie źródłowa i docelowa](vmm-to-azure-walkthrough-source-target.md)</span><span class="sxs-lookup"><span data-stu-id="cf379-115">Go too[Step 8: Set up source and target](vmm-to-azure-walkthrough-source-target.md)</span></span>
