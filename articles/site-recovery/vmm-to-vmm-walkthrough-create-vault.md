---
title: "aaaCreate magazynu dla lokacji dodatkowej tooa replikacji funkcji Hyper-V z usługą Azure Site Recovery | Dokumentacja firmy Microsoft"
description: "W tym artykule opisano, jak toocreate magazynu podczas replikowania maszyn wirtualnych funkcji Hyper-V tooa, lokacji dodatkowej programu System Center VMM, z usługą Azure Site Recovery."
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: ff65dbfb-cb26-410e-ab48-76971625db08
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/30/2017
ms.author: raynew
ms.openlocfilehash: 96ee09cbf2376a5089b9efa09dc7ab3fb7d472cb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="step-5-create-a-vault-for-hyper-v-replication-tooa-secondary-site"></a><span data-ttu-id="fb345-103">Krok 5: Tworzenie magazynu dla lokacji dodatkowej tooa replikacji funkcji Hyper-V</span><span class="sxs-lookup"><span data-stu-id="fb345-103">Step 5: Create a vault for Hyper-V replication tooa secondary site</span></span>

<span data-ttu-id="fb345-104">Po przygotowaniu lokalnymi [programu System Center Virtual Machine Manager (VMM) serwerów i klastrów hostów Hyper-V](vmm-to-vmm-walkthrough-vmm-hyper-v.md) dla funkcji Hyper-V replikacji tooa dodatkowej lokacji przy użyciu [usługi Azure Site Recovery](site-recovery-overview.md), można utworzyć Magazyn usług odzyskiwania i wybierz hello scenariusza replikacji.</span><span class="sxs-lookup"><span data-stu-id="fb345-104">After preparing on-premises [System Center Virtual Machine Manager (VMM) servers and Hyper-V hosts/clusters](vmm-to-vmm-walkthrough-vmm-hyper-v.md) for Hyper-V replication tooa secondary site using [Azure Site Recovery](site-recovery-overview.md), you can create a Recovery Services vault, and select hello replication scenario.</span></span>

<span data-ttu-id="fb345-105">Po przeczytaniu tego artykułu, post wszelkie komentarze u dołu hello, lub na powitania [Forum usług odzyskiwania Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="fb345-105">After reading this article, post any comments at hello bottom, or on hello [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>


## <a name="create-a-recovery-services-vault"></a><span data-ttu-id="fb345-106">Tworzenie magazynu Usług odzyskiwania</span><span class="sxs-lookup"><span data-stu-id="fb345-106">Create a Recovery Services vault</span></span>

[!INCLUDE [site-recovery-create-vault](../../includes/site-recovery-create-vault.md)]


## <a name="choose-a-protection-goal"></a><span data-ttu-id="fb345-107">Wybierz cel ochrony</span><span class="sxs-lookup"><span data-stu-id="fb345-107">Choose a protection goal</span></span>

<span data-ttu-id="fb345-108">Wybierz, co ma tooreplicate i miejscu tooreplicate do.</span><span class="sxs-lookup"><span data-stu-id="fb345-108">Select what you want tooreplicate and where you want tooreplicate to.</span></span>

1. <span data-ttu-id="fb345-109">Kliknij przycisk **usługi Site Recovery** > **krok 1: Przygotowanie infrastruktury** > **cel ochrony**.</span><span class="sxs-lookup"><span data-stu-id="fb345-109">Click **Site Recovery** > **Step 1: Prepare Infrastructure** > **Protection goal**.</span></span>
2. <span data-ttu-id="fb345-110">Wybierz **lokacji toorecovery**i wybierz **tak, z funkcją Hyper-V**.</span><span class="sxs-lookup"><span data-stu-id="fb345-110">Select **toorecovery site**, and select **Yes, with Hyper-V**.</span></span>
3. <span data-ttu-id="fb345-111">Wybierz **tak** tooindicate używasz hostów funkcji Hyper-V hello toomanage programu VMM.</span><span class="sxs-lookup"><span data-stu-id="fb345-111">Select **Yes** tooindicate you're using VMM toomanage hello Hyper-V hosts.</span></span>
4. <span data-ttu-id="fb345-112">Wybierz **tak** Jeśli pomocniczy serwer programu VMM.</span><span class="sxs-lookup"><span data-stu-id="fb345-112">Select **Yes** if you have a secondary VMM server.</span></span> <span data-ttu-id="fb345-113">Jeśli wdrażasz replikacji między chmurami na jednym serwerze programu VMM, kliknij przycisk **nr**.</span><span class="sxs-lookup"><span data-stu-id="fb345-113">If you're deploying replication between clouds on a single VMM server, click **No**.</span></span> <span data-ttu-id="fb345-114">Następnie kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="fb345-114">Then click **OK**.</span></span>

    ![Wybieranie celów](./media/vmm-to-vmm-walkthrough-create-vault/choose-goals.png)



## <a name="next-steps"></a><span data-ttu-id="fb345-116">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="fb345-116">Next steps</span></span>

<span data-ttu-id="fb345-117">Przejdź za[krok 6: Konfigurowanie hello replikacji źródłowa i docelowa](vmm-to-vmm-walkthrough-source-target.md).</span><span class="sxs-lookup"><span data-stu-id="fb345-117">Go too[Step 6: Set up hello replication source and target](vmm-to-vmm-walkthrough-source-target.md).</span></span>
