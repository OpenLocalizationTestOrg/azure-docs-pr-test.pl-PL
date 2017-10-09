---
title: "aaaSet się zasady replikacji dla maszyny Wirtualnej funkcji Hyper-V tooAzure replikacji (bez programu System Center VMM) z usługą Azure Site Recovery | Dokumentacja firmy Microsoft"
description: "Zawiera podsumowanie kroków hello należy tooset się zasady replikacji podczas replikowania maszyn wirtualnych funkcji Hyper-V tooAzure magazynu"
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: 1777e0eb-accb-42b5-a747-11272e131a52
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 06/22/2017
ms.author: raynew
ms.openlocfilehash: 4bd7161f4a0f015da0ecf595fbc6861ede5d68b0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="step-9-set-up-a-replication-policy-for-hyper-v-vm-replication-tooazure"></a><span data-ttu-id="0af41-103">Krok 9: Konfigurowanie zasady replikacji w przypadku tooAzure replikacji maszyny Wirtualnej funkcji Hyper-V</span><span class="sxs-lookup"><span data-stu-id="0af41-103">Step 9: Set up a replication policy for Hyper-V VM replication tooAzure</span></span>

<span data-ttu-id="0af41-104">W tym artykule opisano sposób tooset się zasady replikacji w przypadku replikacji tooAzure maszyn wirtualnych funkcji Hyper-V (bez programu System Center VMM) przy użyciu hello [usługi Azure Site Recovery](site-recovery-overview.md) w hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="0af41-104">This article describes how tooset up a replication policy when you're replicating Hyper-V VMs tooAzure (without System Center VMM) using hello [Azure Site Recovery](site-recovery-overview.md) service in hello Azure portal.</span></span>


<span data-ttu-id="0af41-105">Opublikuj komentarze i pytania u dołu hello w tym artykule, albo na powitania [Forum usług odzyskiwania Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="0af41-105">Post comments and questions at hello bottom of this article, or on hello [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>

## <a name="about-snapshots"></a><span data-ttu-id="0af41-106">Temat migawek</span><span class="sxs-lookup"><span data-stu-id="0af41-106">About snapshots</span></span>

<span data-ttu-id="0af41-107">Funkcja Hyper-V wykorzystuje dwa typy migawek — standardową migawkę, która jest przyrostową migawką całej maszyny wirtualnej hello i migawki spójne z aplikacją, która tworzy migawkę danych aplikacji hello wewnątrz maszyny wirtualnej hello punktu w czasie.</span><span class="sxs-lookup"><span data-stu-id="0af41-107">Hyper-V uses two types of snapshots — a standard snapshot that provides an incremental snapshot of hello entire virtual machine, and an application-consistent snapshot that takes a point-in-time snapshot of hello application data inside hello virtual machine.</span></span>
    - <span data-ttu-id="0af41-108">Migawki spójne z aplikacjami Użyj tooensure usługi kopiowania woluminów w tle (VSS), które aplikacje są w spójnym stanie podczas hello migawki.</span><span class="sxs-lookup"><span data-stu-id="0af41-108">Application-consistent snapshots use Volume Shadow Copy Service (VSS) tooensure that applications are in a consistent state when hello snapshot is taken.</span></span>
    - <span data-ttu-id="0af41-109">Włącz migawki spójne z aplikacjami, wpłynie na powitania wydajność aplikacji uruchomionych na źródłowych maszynach wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="0af41-109">If you enable application-consistent snapshots, it will affect hello performance of applications running on source virtual machines.</span></span> <span data-ttu-id="0af41-110">Upewnij się, że ustawiona wartość hello jest mniejsza niż liczba hello punktów odzyskiwania dodatkowe, które można skonfigurować.</span><span class="sxs-lookup"><span data-stu-id="0af41-110">Ensure that hello value you set is less than hello number of additional recovery points you configure.</span></span>

## <a name="set-up-a-replication-policy"></a><span data-ttu-id="0af41-111">Konfigurowanie zasad replikacji</span><span class="sxs-lookup"><span data-stu-id="0af41-111">Set up a replication policy</span></span>

1. <span data-ttu-id="0af41-112">Kliknij przycisk toocreate nowe zasady replikacji, **przygotowanie infrastruktury** > **ustawienia replikacji** > **+ Utwórz i skojarz**.</span><span class="sxs-lookup"><span data-stu-id="0af41-112">toocreate a new replication policy, click **Prepare infrastructure** > **Replication Settings** > **+Create and associate**.</span></span>

    ![Sieć](./media/hyper-v-site-walkthrough-replication/gs-replication.png)
2. <span data-ttu-id="0af41-114">W obszarze **Utwórz i skojarz zasady** określ nazwę zasad.</span><span class="sxs-lookup"><span data-stu-id="0af41-114">In **Create and associate policy**, specify a policy name.</span></span>
3. <span data-ttu-id="0af41-115">W **częstotliwość kopiowania**, określić, jak często dane różnicowe tooreplicate po replikacji początkowej hello (co 30 sekund, 5 lub 15 minut).</span><span class="sxs-lookup"><span data-stu-id="0af41-115">In **Copy frequency**, specify how often you want tooreplicate delta data after hello initial replication (every 30 seconds, 5 or 15 minutes).</span></span>

    > [!NOTE]
    > <span data-ttu-id="0af41-116">30 częstotliwość drugiego nie jest obsługiwane podczas replikowania toopremium magazynu.</span><span class="sxs-lookup"><span data-stu-id="0af41-116">A 30 second frequency isn't supported when replicating toopremium storage.</span></span> <span data-ttu-id="0af41-117">ograniczenie Hello jest określana przez hello liczby migawek dla obiekt blob (w 100) obsługiwane przez Magazyn w warstwie premium.</span><span class="sxs-lookup"><span data-stu-id="0af41-117">hello limitation is determined by hello number of snapshots per blob (100) supported by premium storage.</span></span> <span data-ttu-id="0af41-118">[Dowiedz się więcej](../storage/common/storage-premium-storage.md#snapshots-and-copy-blob).</span><span class="sxs-lookup"><span data-stu-id="0af41-118">[Learn more](../storage/common/storage-premium-storage.md#snapshots-and-copy-blob).</span></span>

4. <span data-ttu-id="0af41-119">W **przechowywania punktu odzyskiwania**, określ w godzinach, jak długo jest hello okna przechowywania dla każdego punktu odzyskiwania.</span><span class="sxs-lookup"><span data-stu-id="0af41-119">In **Recovery point retention**, specify in hours how long hello retention window is for each recovery point.</span></span> <span data-ttu-id="0af41-120">Maszyny wirtualne mogą zostać odzyskane tooany punktu, w tym oknie.</span><span class="sxs-lookup"><span data-stu-id="0af41-120">VMs can be recovered tooany point within a window.</span></span>
5. <span data-ttu-id="0af41-121">W **częstotliwość migawek spójności aplikacji**, określ, jak często (1 – 12 godzin) punkty odzyskiwania zawierające migawki spójne z aplikacjami są tworzone.</span><span class="sxs-lookup"><span data-stu-id="0af41-121">In **App-consistent snapshot frequency**, specify how frequently (1-12 hours) recovery points containing application-consistent snapshots are created.</span></span>
6. <span data-ttu-id="0af41-122">W **czas rozpoczęcia replikacji początkowej**, określ, kiedy toostart hello replikacji początkowej.</span><span class="sxs-lookup"><span data-stu-id="0af41-122">In **Initial replication start time**, specify when toostart hello initial replication.</span></span> <span data-ttu-id="0af41-123">Hello replikacja odbywa się za pośrednictwem przepustowości połączenia z Internetem, może być tooschedule ją poza najbardziej obciążonymi godzinami.</span><span class="sxs-lookup"><span data-stu-id="0af41-123">hello replication occurs over your internet bandwidth so you might want tooschedule it outside your busy hours.</span></span> <span data-ttu-id="0af41-124">Następnie kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="0af41-124">Then click **OK**.</span></span>

    ![Zasady replikacji](./media/hyper-v-site-walkthrough-replication/gs-replication2.png)

<span data-ttu-id="0af41-126">Podczas tworzenia nowych zasad, zostaną one automatycznie skojarzone z hello lokacji funkcji Hyper-V.</span><span class="sxs-lookup"><span data-stu-id="0af41-126">When you create a new policy, it's automatically associated with hello Hyper-V site.</span></span> <span data-ttu-id="0af41-127">Można skojarzyć z wieloma zasadami replikacji w lokacji funkcji Hyper-V (i hello maszyn wirtualnych w nim) **replikacji** > Nazwa zasady > **skojarzyć lokacji funkcji Hyper-V**.</span><span class="sxs-lookup"><span data-stu-id="0af41-127">You can associate a Hyper-V site (and hello VMs in it) with multiple replication policies in **Replication** > policy-name > **Associate Hyper-V Site**.</span></span>



## <a name="next-steps"></a><span data-ttu-id="0af41-128">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="0af41-128">Next steps</span></span>

<span data-ttu-id="0af41-129">Przejdź do zbyt[kroku 10: Włączanie replikacji](hyper-v-site-walkthrough-enable-replication.md)</span><span class="sxs-lookup"><span data-stu-id="0af41-129">Go too[Step 10: Enable replication](hyper-v-site-walkthrough-enable-replication.md)</span></span>
