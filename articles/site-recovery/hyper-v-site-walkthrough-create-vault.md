---
title: "Konfigurowanie magazynu dla replikacji funkcji Hyper-V (bez programu System Center VMM) na platformie Azure przy użyciu usługi Azure Site Recovery | Dokumentacja firmy Microsoft"
description: "Zawiera podsumowanie kroków, które należy skonfigurować Magazyn replikacji funkcji Hyper-V do platformy Azure przy użyciu usługi Azure Site Recovery"
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
ms.openlocfilehash: 8212ff011633c3a89d3310e828b6d5f1cda6ce3f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="step-7-set-up-a-vault-for-hyper-v-replication"></a><span data-ttu-id="f27c4-103">Krok 7: Konfigurowanie magazynu dla replikacji funkcji Hyper-V</span><span class="sxs-lookup"><span data-stu-id="f27c4-103">Step 7: Set up a vault for Hyper-V replication</span></span>

<span data-ttu-id="f27c4-104">W tym artykule opisano sposób konfigurowania magazynu i określ, co chcesz replikować z tej lokalizacji lokalnego do platformy Azure przy użyciu [usługi Azure Site Recovery](site-recovery-overview.md) w portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="f27c4-104">This article describes how to set up a vault, and specify what you want to replicate from your on-premises location, to Azure using the [Azure Site Recovery](site-recovery-overview.md) service in the Azure portal.</span></span>


<span data-ttu-id="f27c4-105">Opublikuj komentarze i pytania w dolnej części tego artykułu lub na [Forum usług odzyskiwania Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="f27c4-105">Post comments and questions at the bottom of this article, or on the [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>

## <a name="create-a-recovery-services-vault"></a><span data-ttu-id="f27c4-106">Tworzenie magazynu Usług odzyskiwania</span><span class="sxs-lookup"><span data-stu-id="f27c4-106">Create a Recovery Services vault</span></span>

[!INCLUDE [site-recovery-create-vault](../../includes/site-recovery-create-vault.md)]



## <a name="select-a-protection-goal"></a><span data-ttu-id="f27c4-107">Wybierz cel ochrony</span><span class="sxs-lookup"><span data-stu-id="f27c4-107">Select a protection goal</span></span>

<span data-ttu-id="f27c4-108">Wybierz, co chcesz replikować, i miejsce, do którego chcesz przeprowadzać replikację.</span><span class="sxs-lookup"><span data-stu-id="f27c4-108">Select what you want to replicate, and where you want to replicate to.</span></span>

1. <span data-ttu-id="f27c4-109">Kliknij przycisk **Magazyny usług odzyskiwania** > magazynu.</span><span class="sxs-lookup"><span data-stu-id="f27c4-109">Click **Recovery Services vaults** > vault.</span></span>
2. <span data-ttu-id="f27c4-110">W Menu zasobów kliknij **usługi Site Recovery** > **przygotowanie infrastruktury** > **cel ochrony**.</span><span class="sxs-lookup"><span data-stu-id="f27c4-110">In the Resource Menu, click **Site Recovery** > **Prepare Infrastructure** > **Protection goal**.</span></span>
3. <span data-ttu-id="f27c4-111">W **cel ochrony**, wybierz pozycję **do platformy Azure** > **tak, z funkcją Hyper-V**.</span><span class="sxs-lookup"><span data-stu-id="f27c4-111">In **Protection goal**, select **To Azure** > **Yes, with Hyper-V**.</span></span> <span data-ttu-id="f27c4-112">Wybierz **nr** aby upewnić się, że nie używasz programu VMM.</span><span class="sxs-lookup"><span data-stu-id="f27c4-112">Select **No** to confirm you're not using VMM.</span></span> 

    ![Wybieranie celów](./media/hyper-v-site-walkthrough-create-vault/choose-goals2.png)



## <a name="next-steps"></a><span data-ttu-id="f27c4-114">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="f27c4-114">Next steps</span></span>

<span data-ttu-id="f27c4-115">Przejdź do [krok 8: Konfigurowanie źródłowa i docelowa](hyper-v-site-walkthrough-source-target.md)</span><span class="sxs-lookup"><span data-stu-id="f27c4-115">Go to [Step 8: Set up source and target](hyper-v-site-walkthrough-source-target.md)</span></span>
