---
title: "aaaSet się magazynu dla maszyny Wirtualnej Azure repliction między regionami z usługą Azure Site Recovery | Dokumentacja firmy Microsoft"
description: "Zawiera podsumowanie kroków hello należy tooset się magazynu Azure replikacji między regiony platformy Azure przy użyciu usługi Azure Site Recovery"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmon
editor: 
ms.assetid: 40472189-3d80-4963-b175-8bddcbc2f61f
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/01/2017
ms.author: raynew
ms.openlocfilehash: 9959c59c7ea57114763f13bf060404ddd267ba80
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="step-4-set-up-a-vault-for-azure-tooazure-replication"></a><span data-ttu-id="eba4e-103">Krok 4: Konfigurowanie magazynu Azure tooAzure replikacji</span><span class="sxs-lookup"><span data-stu-id="eba4e-103">Step 4: Set up a vault for Azure tooAzure replication</span></span>

<span data-ttu-id="eba4e-104">Po [Planowanie sieci](azure-to-azure-walkthrough-network.md), użyj tego tooset artykułu zapasowej magazynu, maszyn wirtualnych platformy Azure (maszyny wirtualne) replikowanie tooanother region platformy Azure przy użyciu hello [usługi Azure Site Recovery](site-recovery-overview.md) w hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="eba4e-104">After [planning networks](azure-to-azure-walkthrough-network.md), use this article tooset up a vault, for Azure virtual machines (VMs) replicating tooanother Azure region, using hello [Azure Site Recovery](site-recovery-overview.md) service in hello Azure portal.</span></span>

- <span data-ttu-id="eba4e-105">Po zakończeniu artykułu hello powinny mieć Konfigurowanie magazynu usług odzyskiwania.</span><span class="sxs-lookup"><span data-stu-id="eba4e-105">When you finish hello article, you should have a Recovery Services vault set up.</span></span>
- <span data-ttu-id="eba4e-106">Opublikuj wszelkie komentarze u dołu hello w tym artykule, lub zadać pytania w hello [Forum usług odzyskiwania Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="eba4e-106">Post any comments at hello bottom of this article, or ask questions in hello [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>



>[!NOTE]
>
> <span data-ttu-id="eba4e-107">Replikacja maszyny Wirtualnej platformy Azure jest obecnie w przeglądzie.</span><span class="sxs-lookup"><span data-stu-id="eba4e-107">Azure VM replication is currently in preview.</span></span>




## <a name="create-a-vault"></a><span data-ttu-id="eba4e-108">Tworzenie magazynu</span><span class="sxs-lookup"><span data-stu-id="eba4e-108">Create a vault</span></span>

[!INCLUDE [site-recovery-create-vault](../../includes/site-recovery-create-vault.md)]

>[!NOTE]
>
> <span data-ttu-id="eba4e-109">Zaleca się tworzenie magazynu usług odzyskiwania hello w hello lokalizację tooreplicate sieci maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="eba4e-109">We recommend that you create hello Recovery Services vault in hello location where you want your VMs tooreplicate.</span></span> <span data-ttu-id="eba4e-110">Na przykład, jeśli w lokalizacji docelowej jest hello centralnego nam, utwórz magazyn hello w **środkowe stany USA**.</span><span class="sxs-lookup"><span data-stu-id="eba4e-110">For example, if your target location is hello central US, create hello vault in **Central US**.</span></span>


## <a name="next-steps"></a><span data-ttu-id="eba4e-111">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="eba4e-111">Next steps</span></span>

<span data-ttu-id="eba4e-112">Przejdź do zbyt[krok 5: Włączanie replikacji](azure-to-azure-walkthrough-enable-replication.md)</span><span class="sxs-lookup"><span data-stu-id="eba4e-112">Go too[Step 5: Enable replication](azure-to-azure-walkthrough-enable-replication.md)</span></span>
