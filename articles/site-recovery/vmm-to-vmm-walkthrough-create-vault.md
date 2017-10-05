---
title: "Tworzenie magazynu dla funkcji Hyper-V replikacji do lokacji dodatkowej z usługą Azure Site Recovery | Dokumentacja firmy Microsoft"
description: "Opisuje sposób tworzenia magazynu podczas replikowania maszyn wirtualnych funkcji Hyper-V do lokacji dodatkowej programu System Center VMM z usługą Azure Site Recovery."
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
ms.openlocfilehash: 28cfcf12b2e369f96664c163c0b6f2aa8a6ddcb9
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="step-5-create-a-vault-for-hyper-v-replication-to-a-secondary-site"></a><span data-ttu-id="19200-103">Krok 5: Tworzenie magazynu dla funkcji Hyper-V replikacji do lokacji dodatkowej</span><span class="sxs-lookup"><span data-stu-id="19200-103">Step 5: Create a vault for Hyper-V replication to a secondary site</span></span>

<span data-ttu-id="19200-104">Po przygotowaniu lokalnymi [programu System Center Virtual Machine Manager (VMM) serwerów i klastrów hostów Hyper-V](vmm-to-vmm-walkthrough-vmm-hyper-v.md) na lokacji dodatkowej przy użyciu replikacji funkcji Hyper-V [usługi Azure Site Recovery](site-recovery-overview.md), można utworzyć magazyn usług odzyskiwania i wybrać scenariusz replikacji.</span><span class="sxs-lookup"><span data-stu-id="19200-104">After preparing on-premises [System Center Virtual Machine Manager (VMM) servers and Hyper-V hosts/clusters](vmm-to-vmm-walkthrough-vmm-hyper-v.md) for Hyper-V replication to a secondary site using [Azure Site Recovery](site-recovery-overview.md), you can create a Recovery Services vault, and select the replication scenario.</span></span>

<span data-ttu-id="19200-105">Po przeczytaniu tego artykułu zamieść wszelkie komentarze u dołu lub na [forum usług Azure Recovery Services](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="19200-105">After reading this article, post any comments at the bottom, or on the [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>


## <a name="create-a-recovery-services-vault"></a><span data-ttu-id="19200-106">Tworzenie magazynu Usług odzyskiwania</span><span class="sxs-lookup"><span data-stu-id="19200-106">Create a Recovery Services vault</span></span>

[!INCLUDE [site-recovery-create-vault](../../includes/site-recovery-create-vault.md)]


## <a name="choose-a-protection-goal"></a><span data-ttu-id="19200-107">Wybierz cel ochrony</span><span class="sxs-lookup"><span data-stu-id="19200-107">Choose a protection goal</span></span>

<span data-ttu-id="19200-108">Wybierz, co chcesz replikować, i miejsce, do którego chcesz przeprowadzać replikację.</span><span class="sxs-lookup"><span data-stu-id="19200-108">Select what you want to replicate and where you want to replicate to.</span></span>

1. <span data-ttu-id="19200-109">Kliknij przycisk **usługi Site Recovery** > **krok 1: Przygotowanie infrastruktury** > **cel ochrony**.</span><span class="sxs-lookup"><span data-stu-id="19200-109">Click **Site Recovery** > **Step 1: Prepare Infrastructure** > **Protection goal**.</span></span>
2. <span data-ttu-id="19200-110">Wybierz **do odzyskiwania lokacji**i wybierz **tak, z funkcją Hyper-V**.</span><span class="sxs-lookup"><span data-stu-id="19200-110">Select **To recovery site**, and select **Yes, with Hyper-V**.</span></span>
3. <span data-ttu-id="19200-111">Wybierz **tak** aby wskazać, że używasz programu VMM na potrzeby zarządzania hostami funkcji Hyper-V.</span><span class="sxs-lookup"><span data-stu-id="19200-111">Select **Yes** to indicate you're using VMM to manage the Hyper-V hosts.</span></span>
4. <span data-ttu-id="19200-112">Wybierz **tak** Jeśli pomocniczy serwer programu VMM.</span><span class="sxs-lookup"><span data-stu-id="19200-112">Select **Yes** if you have a secondary VMM server.</span></span> <span data-ttu-id="19200-113">Jeśli wdrażasz replikacji między chmurami na jednym serwerze programu VMM, kliknij przycisk **nr**.</span><span class="sxs-lookup"><span data-stu-id="19200-113">If you're deploying replication between clouds on a single VMM server, click **No**.</span></span> <span data-ttu-id="19200-114">Następnie kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="19200-114">Then click **OK**.</span></span>

    ![Wybieranie celów](./media/vmm-to-vmm-walkthrough-create-vault/choose-goals.png)



## <a name="next-steps"></a><span data-ttu-id="19200-116">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="19200-116">Next steps</span></span>

<span data-ttu-id="19200-117">Przejdź do [krok 6: Konfigurowanie replikacji źródłowych i docelowych](vmm-to-vmm-walkthrough-source-target.md).</span><span class="sxs-lookup"><span data-stu-id="19200-117">Go to [Step 6: Set up the replication source and target](vmm-to-vmm-walkthrough-source-target.md).</span></span>