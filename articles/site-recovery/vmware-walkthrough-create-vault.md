---
title: "Konfigurowanie magazynu dla replikacji maszyn wirtualnych VMware do platformy Azure przy użyciu usługi Azure Site Recovery | Dokumentacja firmy Microsoft"
description: "Zawiera podsumowanie kroków, które należy skonfigurować magazynu dla replikacji maszyn wirtualnych VMware do platformy Azure przy użyciu usługi Azure Site Recovery"
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
ms.openlocfilehash: dca95ad46b8de587140c3573ba6ed5702a122032
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="step-7-set-up-a-vault-for-vmware-replication-to-azure"></a><span data-ttu-id="fb1b3-103">Krok 7: Konfigurowanie magazynu dla replikacji maszyn wirtualnych VMware do platformy Azure</span><span class="sxs-lookup"><span data-stu-id="fb1b3-103">Step 7: Set up a vault for VMware replication to Azure</span></span>


<span data-ttu-id="fb1b3-104">W tym artykule opisano sposób konfigurowania magazynu i określ, co chcesz replikować z tej lokalizacji lokalnego do platformy Azure przy użyciu [usługi Azure Site Recovery](site-recovery-overview.md) w portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="fb1b3-104">This article describes how to set up a vault, and specify what you want to replicate from your on-premises location, to Azure using the [Azure Site Recovery](site-recovery-overview.md) service in the Azure portal.</span></span>


<span data-ttu-id="fb1b3-105">Opublikuj komentarze i pytania w dolnej części tego artykułu lub na [Forum usług odzyskiwania Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="fb1b3-105">Post comments and questions at the bottom of this article, or on the [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>




## <a name="create-a-recovery-services-vault"></a><span data-ttu-id="fb1b3-106">Tworzenie magazynu Usług odzyskiwania</span><span class="sxs-lookup"><span data-stu-id="fb1b3-106">Create a Recovery Services vault</span></span>

[!INCLUDE [site-recovery-create-vault](../../includes/site-recovery-create-vault.md)]

## <a name="select-a-protection-goal"></a><span data-ttu-id="fb1b3-107">Wybierz cel ochrony</span><span class="sxs-lookup"><span data-stu-id="fb1b3-107">Select a protection goal</span></span>

<span data-ttu-id="fb1b3-108">Wybierz, co chcesz replikować, i miejsce, do którego chcesz przeprowadzać replikację.</span><span class="sxs-lookup"><span data-stu-id="fb1b3-108">Select what you want to replicate, and where you want to replicate to.</span></span>

1. <span data-ttu-id="fb1b3-109">Kliknij przycisk **Magazyny usług odzyskiwania** > magazynu.</span><span class="sxs-lookup"><span data-stu-id="fb1b3-109">Click **Recovery Services vaults** > vault.</span></span>
2. <span data-ttu-id="fb1b3-110">W Menu zasobów kliknij **usługi Site Recovery** > **przygotowanie infrastruktury** > **cel ochrony**.</span><span class="sxs-lookup"><span data-stu-id="fb1b3-110">In the Resource Menu, click **Site Recovery** > **Prepare Infrastructure** > **Protection goal**.</span></span>
3. <span data-ttu-id="fb1b3-111">W **cel ochrony**, wybierz pozycję **do platformy Azure** > **tak, z programem VMware vSphere Hypervisor**.</span><span class="sxs-lookup"><span data-stu-id="fb1b3-111">In **Protection goal**, select **To Azure** > **Yes, with VMware vSphere Hypervisor**.</span></span>



## <a name="next-steps"></a><span data-ttu-id="fb1b3-112">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="fb1b3-112">Next steps</span></span>

<span data-ttu-id="fb1b3-113">Przejdź do [krok 8: Konfigurowanie źródłowa i docelowa](vmware-walkthrough-source-target.md)</span><span class="sxs-lookup"><span data-stu-id="fb1b3-113">Go to [Step 8: Set up source and target](vmware-walkthrough-source-target.md)</span></span>
