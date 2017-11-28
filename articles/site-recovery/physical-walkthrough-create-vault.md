---
title: "aaaSet się magazynu dla serwera fizycznego tooAzure replikacji przy użyciu usługi Azure Site Recovery | Dokumentacja firmy Microsoft"
description: "Zawiera podsumowanie kroków hello należy tooset się tooAzure serwerów fizycznych tooreplicate magazynu przy użyciu usługi Azure Site Recovery"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: d99f2605-f417-4995-be77-5323136b814f
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/27/2017
ms.author: raynew
ms.openlocfilehash: 988928e3ece31116823f132cc39223fe44443468
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="step-6-set-up-a-vault-for-physical-server-replication-tooazure"></a><span data-ttu-id="33d1d-103">Krok 6: Konfigurowanie magazynu dla tooAzure replikacji serwera fizycznego</span><span class="sxs-lookup"><span data-stu-id="33d1d-103">Step 6: Set up a vault for physical server replication tooAzure</span></span>


<span data-ttu-id="33d1d-104">W tym artykule opisano sposób tooset się magazynu.</span><span class="sxs-lookup"><span data-stu-id="33d1d-104">This article describes how tooset up a vault.</span></span> <span data-ttu-id="33d1d-105">Utwórz magazyn hello i określ sposób tooreplicate z sieci lokalnej lokalizacji tooAzure, przy użyciu hello [usługi Azure Site Recovery](site-recovery-overview.md) w hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="33d1d-105">You create hello vault, and specify what you want tooreplicate from your on-premises location tooAzure, using hello [Azure Site Recovery](site-recovery-overview.md) service in hello Azure portal.</span></span>


<span data-ttu-id="33d1d-106">Opublikuj komentarze i pytania u dołu hello w tym artykule, albo na powitania [Forum usług odzyskiwania Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="33d1d-106">Post comments and questions at hello bottom of this article, or on hello [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>




## <a name="create-a-recovery-services-vault"></a><span data-ttu-id="33d1d-107">Tworzenie magazynu Usług odzyskiwania</span><span class="sxs-lookup"><span data-stu-id="33d1d-107">Create a Recovery Services vault</span></span>

[!INCLUDE [site-recovery-create-vault](../../includes/site-recovery-create-vault.md)]

## <a name="select-a-protection-goal"></a><span data-ttu-id="33d1d-108">Wybierz cel ochrony</span><span class="sxs-lookup"><span data-stu-id="33d1d-108">Select a protection goal</span></span>

<span data-ttu-id="33d1d-109">Wybierz, co ma tooreplicate, i miejsce tooreplicate do.</span><span class="sxs-lookup"><span data-stu-id="33d1d-109">Select what you want tooreplicate, and where you want tooreplicate to.</span></span>

1. <span data-ttu-id="33d1d-110">Kliknij przycisk **Magazyny usług odzyskiwania** > magazynu.</span><span class="sxs-lookup"><span data-stu-id="33d1d-110">Click **Recovery Services vaults** > vault.</span></span>
2. <span data-ttu-id="33d1d-111">W Menu zasobów hello, kliknij przycisk **usługi Site Recovery** > **przygotowanie infrastruktury** > **cel ochrony**.</span><span class="sxs-lookup"><span data-stu-id="33d1d-111">In hello Resource Menu, click **Site Recovery** > **Prepare Infrastructure** > **Protection goal**.</span></span>
3. <span data-ttu-id="33d1d-112">W **cel ochrony**, wybierz pozycję **tooAzure** > **nie zwirtualizowanych/inne**.</span><span class="sxs-lookup"><span data-stu-id="33d1d-112">In **Protection goal**, select **tooAzure** > **Not virtualized/Other**.</span></span>


## <a name="next-steps"></a><span data-ttu-id="33d1d-113">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="33d1d-113">Next steps</span></span>

<span data-ttu-id="33d1d-114">Przejdź do zbyt[kroku 7: Konfigurowanie źródłowa i docelowa](physical-walkthrough-source-target.md)</span><span class="sxs-lookup"><span data-stu-id="33d1d-114">Go too[Step 7: Set up source and target](physical-walkthrough-source-target.md)</span></span>
