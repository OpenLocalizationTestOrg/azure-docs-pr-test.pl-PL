---
title: "Skonfiguruj zasady replikacji w przypadku replikacji maszyn wirtualnych funkcji Hyper-V (bez programu System Center VMM) na platformie Azure za pomocą usługi Azure Site Recovery | Dokumentacja firmy Microsoft"
description: "Zawiera podsumowanie kroków, które należy skonfigurować zasady replikacji podczas replikowania maszyn wirtualnych funkcji Hyper-V do magazynu Azure"
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
ms.openlocfilehash: ca5bec5cf1152e6259b9fe7a869edd2d62b88e1a
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
# <a name="step-9-set-up-a-replication-policy-for-hyper-v-vm-replication-to-azure"></a><span data-ttu-id="69ac2-103">Krok 9: Konfigurowanie zasady replikacji w przypadku replikacji maszyn wirtualnych funkcji Hyper-V do platformy Azure</span><span class="sxs-lookup"><span data-stu-id="69ac2-103">Step 9: Set up a replication policy for Hyper-V VM replication to Azure</span></span>

<span data-ttu-id="69ac2-104">W tym artykule opisano sposób konfigurowania zasad replikacji w przypadku replikacji maszyn wirtualnych funkcji Hyper-V do platformy Azure (bez programu System Center VMM) przy użyciu [usługi Azure Site Recovery](site-recovery-overview.md) w portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="69ac2-104">This article describes how to set up a replication policy when you're replicating Hyper-V VMs to Azure (without System Center VMM) using the [Azure Site Recovery](site-recovery-overview.md) service in the Azure portal.</span></span>


<span data-ttu-id="69ac2-105">Opublikuj komentarze i pytania w dolnej części tego artykułu lub na [Forum usług odzyskiwania Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="69ac2-105">Post comments and questions at the bottom of this article, or on the [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>

## <a name="about-snapshots"></a><span data-ttu-id="69ac2-106">Temat migawek</span><span class="sxs-lookup"><span data-stu-id="69ac2-106">About snapshots</span></span>

<span data-ttu-id="69ac2-107">Funkcja Hyper-V wykorzystuje dwa typy migawek — standardową migawkę, która jest przyrostową migawką całej maszyny wirtualnej oraz migawkę spójności aplikacji, która wykonuje migawkę danych aplikacji wewnątrz maszyny wirtualnej w danym punkcie w czasie.</span><span class="sxs-lookup"><span data-stu-id="69ac2-107">Hyper-V uses two types of snapshots — a standard snapshot that provides an incremental snapshot of the entire virtual machine, and an application-consistent snapshot that takes a point-in-time snapshot of the application data inside the virtual machine.</span></span>
    - <span data-ttu-id="69ac2-108">Migawki spójne z aplikacjami używają usługi Volume Shadow Copy (VSS), aby zapewnić, że aplikacje są w spójnym stanie podczas wykonywania migawki.</span><span class="sxs-lookup"><span data-stu-id="69ac2-108">Application-consistent snapshots use Volume Shadow Copy Service (VSS) to ensure that applications are in a consistent state when the snapshot is taken.</span></span>
    - <span data-ttu-id="69ac2-109">Jeśli włączysz migawki spójne z aplikacjami, ma wpływ na wydajność aplikacji uruchomionych na źródłowych maszynach wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="69ac2-109">If you enable application-consistent snapshots, it will affect the performance of applications running on source virtual machines.</span></span> <span data-ttu-id="69ac2-110">Upewnij się, że ustawiona wartość jest mniejsza od liczby skonfigurowanych dodatkowych punktów odzyskiwania.</span><span class="sxs-lookup"><span data-stu-id="69ac2-110">Ensure that the value you set is less than the number of additional recovery points you configure.</span></span>

## <a name="set-up-a-replication-policy"></a><span data-ttu-id="69ac2-111">Konfigurowanie zasad replikacji</span><span class="sxs-lookup"><span data-stu-id="69ac2-111">Set up a replication policy</span></span>

1. <span data-ttu-id="69ac2-112">Aby utworzyć nowe zasady replikacji, kliknij kolejno pozycje **Przygotowanie infrastruktury** > **Ustawienia replikacji** > **+ Utwórz i skojarz**.</span><span class="sxs-lookup"><span data-stu-id="69ac2-112">To create a new replication policy, click **Prepare infrastructure** > **Replication Settings** > **+Create and associate**.</span></span>

    ![Sieć](./media/hyper-v-site-walkthrough-replication/gs-replication.png)
2. <span data-ttu-id="69ac2-114">W obszarze **Utwórz i skojarz zasady** określ nazwę zasad.</span><span class="sxs-lookup"><span data-stu-id="69ac2-114">In **Create and associate policy**, specify a policy name.</span></span>
3. <span data-ttu-id="69ac2-115">W obszarze **Częstotliwość kopiowania** określ, jak często mają być replikowane dane przyrostowe po replikacji początkowej (co 30 sekund, 5 lub 15 minut).</span><span class="sxs-lookup"><span data-stu-id="69ac2-115">In **Copy frequency**, specify how often you want to replicate delta data after the initial replication (every 30 seconds, 5 or 15 minutes).</span></span>

    > [!NOTE]
    > <span data-ttu-id="69ac2-116">Częstotliwość 30-sekundowa nie jest obsługiwana w przypadku replikowania do usługi Premium Storage.</span><span class="sxs-lookup"><span data-stu-id="69ac2-116">A 30 second frequency isn't supported when replicating to premium storage.</span></span> <span data-ttu-id="69ac2-117">To ograniczenie wynika z liczby migawek na obiekt blob (100) obsługiwanych przez usługę Premium Storage.</span><span class="sxs-lookup"><span data-stu-id="69ac2-117">The limitation is determined by the number of snapshots per blob (100) supported by premium storage.</span></span> <span data-ttu-id="69ac2-118">[Dowiedz się więcej](../storage/common/storage-premium-storage.md#snapshots-and-copy-blob).</span><span class="sxs-lookup"><span data-stu-id="69ac2-118">[Learn more](../storage/common/storage-premium-storage.md#snapshots-and-copy-blob).</span></span>

4. <span data-ttu-id="69ac2-119">W **przechowywania punktu odzyskiwania**, określ w godzinach, jak długo trwa okna przechowywania dla każdego punktu odzyskiwania.</span><span class="sxs-lookup"><span data-stu-id="69ac2-119">In **Recovery point retention**, specify in hours how long the retention window is for each recovery point.</span></span> <span data-ttu-id="69ac2-120">Maszyny wirtualne można odzyskać do dowolnego punktu w tym oknie.</span><span class="sxs-lookup"><span data-stu-id="69ac2-120">VMs can be recovered to any point within a window.</span></span>
5. <span data-ttu-id="69ac2-121">W **częstotliwość migawek spójności aplikacji**, określ, jak często (1 – 12 godzin) punkty odzyskiwania zawierające migawki spójne z aplikacjami są tworzone.</span><span class="sxs-lookup"><span data-stu-id="69ac2-121">In **App-consistent snapshot frequency**, specify how frequently (1-12 hours) recovery points containing application-consistent snapshots are created.</span></span>
6. <span data-ttu-id="69ac2-122">W **czas rozpoczęcia replikacji początkowej**, określ, kiedy można uruchomić replikacji początkowej.</span><span class="sxs-lookup"><span data-stu-id="69ac2-122">In **Initial replication start time**, specify when to start the initial replication.</span></span> <span data-ttu-id="69ac2-123">Replikacja odbywa się z wykorzystaniem przepustowości Internetu, dlatego warto zaplanować ją poza najbardziej obciążonymi godzinami.</span><span class="sxs-lookup"><span data-stu-id="69ac2-123">The replication occurs over your internet bandwidth so you might want to schedule it outside your busy hours.</span></span> <span data-ttu-id="69ac2-124">Następnie kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="69ac2-124">Then click **OK**.</span></span>

    ![Zasady replikacji](./media/hyper-v-site-walkthrough-replication/gs-replication2.png)

<span data-ttu-id="69ac2-126">Podczas tworzenia nowych zasad, zostaną one automatycznie skojarzone z lokacji funkcji Hyper-V.</span><span class="sxs-lookup"><span data-stu-id="69ac2-126">When you create a new policy, it's automatically associated with the Hyper-V site.</span></span> <span data-ttu-id="69ac2-127">Można skojarzyć z wieloma zasadami replikacji w lokacji funkcji Hyper-V (oraz maszyny wirtualne w nim) **replikacji** > Nazwa zasady > **skojarzyć lokacji funkcji Hyper-V**.</span><span class="sxs-lookup"><span data-stu-id="69ac2-127">You can associate a Hyper-V site (and the VMs in it) with multiple replication policies in **Replication** > policy-name > **Associate Hyper-V Site**.</span></span>



## <a name="next-steps"></a><span data-ttu-id="69ac2-128">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="69ac2-128">Next steps</span></span>

<span data-ttu-id="69ac2-129">Przejdź do [kroku 10: Włączanie replikacji](hyper-v-site-walkthrough-enable-replication.md)</span><span class="sxs-lookup"><span data-stu-id="69ac2-129">Go to [Step 10: Enable replication](hyper-v-site-walkthrough-enable-replication.md)</span></span>
