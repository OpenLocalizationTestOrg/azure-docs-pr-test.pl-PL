---
title: "aaaSet się zasady replikacji w przypadku tooAzure replikacji serwerze fizycznym z usługą Azure Site Recovery | Dokumentacja firmy Microsoft"
description: "Zawiera podsumowanie kroków hello należy tooset się zasady replikacji, jeśli Replikowanie lokalnych serwerów fizycznych tooAzure magazynu przy użyciu usługi Azure Site Recovery hello"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: d7874bd8-6626-4668-9ec9-dbd2d26f8f81
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/27/2017
ms.author: raynew
ms.openlocfilehash: d6bdeeffc24ffc8eaba24311f7c76452edb65648
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="step-8-set-up-a-replication-policy-for-physical-server-replication-tooazure"></a><span data-ttu-id="70169-103">Krok 8: Skonfiguruj zasady replikacji w przypadku tooAzure replikacji serwera fizycznego</span><span class="sxs-lookup"><span data-stu-id="70169-103">Step 8: Set up a replication policy for physical server replication tooAzure</span></span>


<span data-ttu-id="70169-104">W tym artykule opisano sposób tooset się zasady replikacji w przypadku replikacji tooAzure serwerach fizycznych systemu Windows i Linux przy użyciu hello [usługi Azure Site Recovery](site-recovery-overview.md) w hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="70169-104">This article describes how tooset up a replication policy when you're replicating Windows/Linux physical servers tooAzure using hello [Azure Site Recovery](site-recovery-overview.md) service in hello Azure portal.</span></span>


<span data-ttu-id="70169-105">Opublikuj komentarze i pytania u dołu hello w tym artykule, albo na powitania [Forum usług odzyskiwania Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="70169-105">Post comments and questions at hello bottom of this article, or on hello [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>


## <a name="configure-a-policy"></a><span data-ttu-id="70169-106">Konfigurowanie zasad</span><span class="sxs-lookup"><span data-stu-id="70169-106">Configure a policy</span></span>

1. <span data-ttu-id="70169-107">Kliknij przycisk **infrastruktura usługi Site Recovery** > **zasady replikacji** > **+ zasad replikacji**.</span><span class="sxs-lookup"><span data-stu-id="70169-107">Click **Site Recovery infrastructure** > **Replication Policies** > **+Replication Policy**.</span></span>
2. <span data-ttu-id="70169-108">W **Utwórz zasady replikacji**, określ nazwę zasady.</span><span class="sxs-lookup"><span data-stu-id="70169-108">In **Create replication policy**, specify a policy name.</span></span>
3. <span data-ttu-id="70169-109">W **próg RPO**, określ hello RPO limit.</span><span class="sxs-lookup"><span data-stu-id="70169-109">In **RPO threshold**, specify hello RPO limit.</span></span> <span data-ttu-id="70169-110">Ta wartość określa, jak często są tworzone punkty odzyskiwania danych.</span><span class="sxs-lookup"><span data-stu-id="70169-110">This value indicates how often data recovery points are created.</span></span> <span data-ttu-id="70169-111">Alert jest generowany, gdy ciągłej replikacji przekracza ten limit.</span><span class="sxs-lookup"><span data-stu-id="70169-111">An alert is generated if continuous replication exceeds this limit.</span></span>
4. <span data-ttu-id="70169-112">W **przechowywania punktu odzyskiwania**, określ czas (w godzinach) jest hello okna przechowywania dla każdego punktu odzyskiwania.</span><span class="sxs-lookup"><span data-stu-id="70169-112">In **Recovery point retention**, specify (in hours) how long hello retention window is for each recovery point.</span></span> <span data-ttu-id="70169-113">Replikowane maszyny wirtualne można odzyskać punktu tooany w oknie.</span><span class="sxs-lookup"><span data-stu-id="70169-113">Replicated VMs can be recovered tooany point in a window.</span></span> <span data-ttu-id="70169-114">Zapasowej too24 godzin przechowywania jest obsługiwana dla maszyn replikowane toopremium magazynu i 72 godziny dla magazynu w warstwie standardowa.</span><span class="sxs-lookup"><span data-stu-id="70169-114">Up too24 hours retention is supported for machines replicated toopremium storage, and 72 hours for standard storage.</span></span>
5. <span data-ttu-id="70169-115">W **częstotliwość migawek spójności aplikacji**, określ częstotliwość (w minutach) będą tworzone punkty odzyskiwana zawierające migawki spójne z aplikacjami.</span><span class="sxs-lookup"><span data-stu-id="70169-115">In **App-consistent snapshot frequency**, specify how often (in minutes) recovery points containing application-consistent snapshots will be created.</span></span> <span data-ttu-id="70169-116">Kliknij przycisk **OK** toocreate hello zasad.</span><span class="sxs-lookup"><span data-stu-id="70169-116">Click **OK** toocreate hello policy.</span></span>

    ![Zasady replikacji](./media/physical-walkthrough-replication/gs-replication2.png)
8. <span data-ttu-id="70169-118">Podczas tworzenia nowej zasady zostaną one automatycznie skojarzone z serwerem konfiguracji hello.</span><span class="sxs-lookup"><span data-stu-id="70169-118">When you create a new policy it's automatically associated with hello configuration server.</span></span> <span data-ttu-id="70169-119">Domyślnie zasady uzgadniania jest tworzony automatycznie powrotu po awarii.</span><span class="sxs-lookup"><span data-stu-id="70169-119">By default, a matching policy is automatically created for failback.</span></span> <span data-ttu-id="70169-120">Na przykład jeśli hello zasad replikacji jest **rep zasad** będzie zasady powrotu po awarii hello **rep zasad-powrotu po awarii**.</span><span class="sxs-lookup"><span data-stu-id="70169-120">For example, if hello replication policy is **rep-policy** then hello failback policy will be **rep-policy-failback**.</span></span> <span data-ttu-id="70169-121">Ta zasada nie jest używany, dopiero po zainicjowaniu powrotu po awarii z platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="70169-121">This policy isn't used until you initiate a failback from Azure.</span></span>

## <a name="next-steps"></a><span data-ttu-id="70169-122">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="70169-122">Next steps</span></span>

<span data-ttu-id="70169-123">Przejdź zbyt[krok 9: Instalowanie usługi mobilności hello](physical-walkthrough-install-mobility.md)</span><span class="sxs-lookup"><span data-stu-id="70169-123">Go too[Step 9: Install hello Mobility service](physical-walkthrough-install-mobility.md)</span></span>
