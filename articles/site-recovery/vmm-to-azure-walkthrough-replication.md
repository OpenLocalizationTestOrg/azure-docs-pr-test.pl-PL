---
title: "aaaSet się zasady replikacji w przypadku tooAzure replikacji maszyny Wirtualnej funkcji Hyper-V (w programie VMM) z usługą Azure Site Recovery | Dokumentacja firmy Microsoft"
description: "Opisuje sposób tooset się zasady replikacji w przypadku tooAzure replikacji maszyny Wirtualnej funkcji Hyper-V (w programie VMM) z usługą Azure Site Recovery"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: ee808b20-324b-4198-b831-edb65b95e8b7
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/23/2017
ms.author: raynew
ms.openlocfilehash: e1579fde559ca34eca19a01e740fec28a0df2f9e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="step-10-set-up-a-replication-policy-for-hyper-v-vm-replication-with-vmm-tooazure"></a><span data-ttu-id="4a005-103">Krok 10: Konfigurowanie zasad replikacji dla maszyny Wirtualnej funkcji Hyper-V tooAzure replikacji (w programie VMM)</span><span class="sxs-lookup"><span data-stu-id="4a005-103">Step 10: Set up a replication policy for Hyper-V VM replication (with VMM) tooAzure</span></span>


<span data-ttu-id="4a005-104">Po skonfigurowaniu [mapowania sieci](vmm-to-azure-walkthrough-network-mapping.md), użyj tego artykułu tooconfigure zasad replikacji T\tooreplicate lokalnych maszyn wirtualnych funkcji Hyper-V zarządzanych w tooAzure chmur programu System Center Virtual Machine Manager (VMM), za pomocą hello [ Usługa Azure Site Recovery](site-recovery-overview.md) w hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="4a005-104">After setting up [network mapping](vmm-to-azure-walkthrough-network-mapping.md), use this article tooconfigure a replication policy T\tooreplicate on-premises Hyper-V virtual machines managed in System Center Virtual Machine Manager (VMM) clouds tooAzure, using hello [Azure Site Recovery](site-recovery-overview.md) service in hello Azure portal.</span></span>

<span data-ttu-id="4a005-105">Po przeczytaniu tego artykułu, post wszelkie komentarze u dołu hello, lub na powitania [Forum usług odzyskiwania Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="4a005-105">After reading this article, post any comments at hello bottom, or on hello [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>



## <a name="create-a-policy"></a><span data-ttu-id="4a005-106">Tworzenie zasad</span><span class="sxs-lookup"><span data-stu-id="4a005-106">Create a policy</span></span>

1. <span data-ttu-id="4a005-107">Kliknij przycisk toocreate nowe zasady replikacji, **przygotowanie infrastruktury** > **ustawienia replikacji** > **+ Utwórz i skojarz**.</span><span class="sxs-lookup"><span data-stu-id="4a005-107">toocreate a new replication policy, click **Prepare infrastructure** > **Replication Settings** > **+Create and associate**.</span></span>

    ![Sieć](./media/vmm-to-azure-walkthrough-replication/gs-replication.png)
2. <span data-ttu-id="4a005-109">W obszarze **Utwórz i skojarz zasady** określ nazwę zasad.</span><span class="sxs-lookup"><span data-stu-id="4a005-109">In **Create and associate policy**, specify a policy name.</span></span>
3. <span data-ttu-id="4a005-110">W **częstotliwość kopiowania**, określić, jak często dane różnicowe tooreplicate po replikacji początkowej hello (co 30 sekund, 5 lub 15 minut).</span><span class="sxs-lookup"><span data-stu-id="4a005-110">In **Copy frequency**, specify how often you want tooreplicate delta data after hello initial replication (every 30 seconds, 5 or 15 minutes).</span></span>

    > [!NOTE]
    >  <span data-ttu-id="4a005-111">30 częstotliwość drugiego nie jest obsługiwane podczas replikowania toopremium magazynu.</span><span class="sxs-lookup"><span data-stu-id="4a005-111">A 30 second frequency isn't supported when replicating toopremium storage.</span></span> <span data-ttu-id="4a005-112">ograniczenie Hello jest określana przez hello liczby migawek dla obiekt blob (w 100) obsługiwane przez Magazyn w warstwie premium.</span><span class="sxs-lookup"><span data-stu-id="4a005-112">hello limitation is determined by hello number of snapshots per blob (100) supported by premium storage.</span></span> [<span data-ttu-id="4a005-113">Dowiedz się więcej</span><span class="sxs-lookup"><span data-stu-id="4a005-113">Learn more</span></span>](../storage/common/storage-premium-storage.md#snapshots-and-copy-blob)

4. <span data-ttu-id="4a005-114">W **przechowywania punktu odzyskiwania**, określ w godzinach, jak długo będą hello okna przechowywania dla każdego punktu odzyskiwania.</span><span class="sxs-lookup"><span data-stu-id="4a005-114">In **Recovery point retention**, specify in hours how long hello retention window will be for each recovery point.</span></span> <span data-ttu-id="4a005-115">Chronione maszyny można odzyskać tooany punktu, w tym oknie.</span><span class="sxs-lookup"><span data-stu-id="4a005-115">Protected machines can be recovered tooany point within a window.</span></span>
5. <span data-ttu-id="4a005-116">W obszarze **Częstotliwość migawek spójności aplikacji** określ, jak często (1–12 godzin) będą tworzone punkty odzyskiwania zawierające migawki spójne z aplikacjami.</span><span class="sxs-lookup"><span data-stu-id="4a005-116">In **App-consistent snapshot frequency**, specify how frequently (1-12 hours) recovery points containing application-consistent snapshots will be created.</span></span> <span data-ttu-id="4a005-117">Funkcja Hyper-V wykorzystuje dwa typy migawek — standardową migawkę, która jest przyrostową migawką całej maszyny wirtualnej hello i migawki spójne z aplikacją, która tworzy migawkę danych aplikacji hello wewnątrz maszyny wirtualnej hello punktu w czasie.</span><span class="sxs-lookup"><span data-stu-id="4a005-117">Hyper-V uses two types of snapshots — a standard snapshot that provides an incremental snapshot of hello entire virtual machine, and an application-consistent snapshot that takes a point-in-time snapshot of hello application data inside hello virtual machine.</span></span> <span data-ttu-id="4a005-118">Migawki spójne z aplikacjami Użyj tooensure usługi kopiowania woluminów w tle (VSS), które aplikacje są w spójnym stanie podczas hello migawki.</span><span class="sxs-lookup"><span data-stu-id="4a005-118">Application-consistent snapshots use Volume Shadow Copy Service (VSS) tooensure that applications are in a consistent state when hello snapshot is taken.</span></span> <span data-ttu-id="4a005-119">Należy pamiętać, że po włączeniu migawek spójnych z aplikacją ma wpływ na powitania wydajność aplikacji uruchomionych na źródłowych maszynach wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="4a005-119">Note that if you enable application-consistent snapshots, it will affect hello performance of applications running on source virtual machines.</span></span> <span data-ttu-id="4a005-120">Upewnij się, że ustawiona wartość hello jest mniejsza niż liczba hello punktów odzyskiwania dodatkowe, które można skonfigurować.</span><span class="sxs-lookup"><span data-stu-id="4a005-120">Ensure that hello value you set is less than hello number of additional recovery points you configure.</span></span>
6. <span data-ttu-id="4a005-121">W **czas rozpoczęcia replikacji początkowej**, wskazuje, kiedy toostart hello replikacji początkowej.</span><span class="sxs-lookup"><span data-stu-id="4a005-121">In **Initial replication start time**, indicate when toostart hello initial replication.</span></span> <span data-ttu-id="4a005-122">Hello replikacja odbywa się za pośrednictwem przepustowości połączenia z Internetem, może być tooschedule ją poza najbardziej obciążonymi godzinami.</span><span class="sxs-lookup"><span data-stu-id="4a005-122">hello replication occurs over your internet bandwidth so you might want tooschedule it outside your busy hours.</span></span>
7. <span data-ttu-id="4a005-123">W **Szyfruj dane przechowywane na platformie Azure**, określ, czy tooencrypt dane w stanie spoczynku w magazynie Azure.</span><span class="sxs-lookup"><span data-stu-id="4a005-123">In **Encrypt data stored on Azure**, specify whether tooencrypt at rest data in Azure storage.</span></span> <span data-ttu-id="4a005-124">Następnie kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="4a005-124">Then click **OK**.</span></span>

    ![Zasady replikacji](./media/vmm-to-azure-walkthrough-replication/gs-replication2.png)
8. <span data-ttu-id="4a005-126">Podczas tworzenia nowych zasad jest ona automatycznie skojarzona z hello chmury VMM.</span><span class="sxs-lookup"><span data-stu-id="4a005-126">When you create a new policy it's automatically associated with hello VMM cloud.</span></span> <span data-ttu-id="4a005-127">Kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="4a005-127">Click **OK**.</span></span> <span data-ttu-id="4a005-128">Dodatkowe chmury VMM (oraz hello maszyn wirtualnych w nich) można skojarzyć z zasadami replikacji w **replikacji** > nazwa_zasady > **Skojarz chmurę VMM**.</span><span class="sxs-lookup"><span data-stu-id="4a005-128">You can associate additional VMM clouds (and hello VMs in them) with this replication policy in **Replication** > policy name > **Associate VMM Cloud**.</span></span>

    ![Zasady replikacji](./media/vmm-to-azure-walkthrough-replication/policy-associate.png)



## <a name="next-steps"></a><span data-ttu-id="4a005-130">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="4a005-130">Next steps</span></span>

<span data-ttu-id="4a005-131">Przejdź do zbyt[krok 11: Włączanie replikacji](vmm-to-azure-walkthrough-enable-replication.md)</span><span class="sxs-lookup"><span data-stu-id="4a005-131">Go too[Step 11: Enable replication](vmm-to-azure-walkthrough-enable-replication.md)</span></span>
