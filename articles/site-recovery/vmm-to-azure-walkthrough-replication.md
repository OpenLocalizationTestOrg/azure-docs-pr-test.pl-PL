---
title: "Skonfiguruj zasady replikacji w przypadku replikacji maszyn wirtualnych funkcji Hyper-V (w programie VMM) na platformie Azure z usługą Azure Site Recovery | Dokumentacja firmy Microsoft"
description: "Zawiera opis sposobu konfigurowania zasady replikacji w przypadku replikacji maszyn wirtualnych funkcji Hyper-V (w programie VMM) na platformie Azure z usługą Azure Site Recovery"
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
ms.openlocfilehash: 592e1c3f647e5b1f1d9aa776657e8f89b60349e1
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
# <a name="step-10-set-up-a-replication-policy-for-hyper-v-vm-replication-with-vmm-to-azure"></a><span data-ttu-id="fecc6-103">Krok 10: Skonfiguruj zasady replikacji w przypadku replikacji maszyn wirtualnych funkcji Hyper-V (w programie VMM) na platformie Azure</span><span class="sxs-lookup"><span data-stu-id="fecc6-103">Step 10: Set up a replication policy for Hyper-V VM replication (with VMM) to Azure</span></span>


<span data-ttu-id="fecc6-104">Po skonfigurowaniu [mapowania sieci](vmm-to-azure-walkthrough-network-mapping.md), użyj w tym artykule, aby skonfigurować zasady replikacji T\to replikowania lokalnych maszyn wirtualnych funkcji Hyper-V zarządzane w chmurach programu System Center Virtual Machine Manager (VMM) na platformie Azure, przy użyciu [Usługi azure Site Recovery](site-recovery-overview.md) w portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="fecc6-104">After setting up [network mapping](vmm-to-azure-walkthrough-network-mapping.md), use this article to configure a replication policy T\to replicate on-premises Hyper-V virtual machines managed in System Center Virtual Machine Manager (VMM) clouds to Azure, using the [Azure Site Recovery](site-recovery-overview.md) service in the Azure portal.</span></span>

<span data-ttu-id="fecc6-105">Po przeczytaniu tego artykułu zamieść wszelkie komentarze u dołu lub na [forum usług Azure Recovery Services](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="fecc6-105">After reading this article, post any comments at the bottom, or on the [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>



## <a name="create-a-policy"></a><span data-ttu-id="fecc6-106">Tworzenie zasad</span><span class="sxs-lookup"><span data-stu-id="fecc6-106">Create a policy</span></span>

1. <span data-ttu-id="fecc6-107">Aby utworzyć nowe zasady replikacji, kliknij kolejno pozycje **Przygotowanie infrastruktury** > **Ustawienia replikacji** > **+ Utwórz i skojarz**.</span><span class="sxs-lookup"><span data-stu-id="fecc6-107">To create a new replication policy, click **Prepare infrastructure** > **Replication Settings** > **+Create and associate**.</span></span>

    ![Sieć](./media/vmm-to-azure-walkthrough-replication/gs-replication.png)
2. <span data-ttu-id="fecc6-109">W obszarze **Utwórz i skojarz zasady** określ nazwę zasad.</span><span class="sxs-lookup"><span data-stu-id="fecc6-109">In **Create and associate policy**, specify a policy name.</span></span>
3. <span data-ttu-id="fecc6-110">W obszarze **Częstotliwość kopiowania** określ, jak często mają być replikowane dane przyrostowe po replikacji początkowej (co 30 sekund, 5 lub 15 minut).</span><span class="sxs-lookup"><span data-stu-id="fecc6-110">In **Copy frequency**, specify how often you want to replicate delta data after the initial replication (every 30 seconds, 5 or 15 minutes).</span></span>

    > [!NOTE]
    >  <span data-ttu-id="fecc6-111">Częstotliwość 30-sekundowa nie jest obsługiwana w przypadku replikowania do usługi Premium Storage.</span><span class="sxs-lookup"><span data-stu-id="fecc6-111">A 30 second frequency isn't supported when replicating to premium storage.</span></span> <span data-ttu-id="fecc6-112">To ograniczenie wynika z liczby migawek na obiekt blob (100) obsługiwanych przez usługę Premium Storage.</span><span class="sxs-lookup"><span data-stu-id="fecc6-112">The limitation is determined by the number of snapshots per blob (100) supported by premium storage.</span></span> [<span data-ttu-id="fecc6-113">Dowiedz się więcej</span><span class="sxs-lookup"><span data-stu-id="fecc6-113">Learn more</span></span>](../storage/common/storage-premium-storage.md#snapshots-and-copy-blob)

4. <span data-ttu-id="fecc6-114">W obszarze **Przechowywanie punktu odzyskiwania** określ w godzinach, jak długie będzie okno przechowywania dla każdego punktu odzyskiwania.</span><span class="sxs-lookup"><span data-stu-id="fecc6-114">In **Recovery point retention**, specify in hours how long the retention window will be for each recovery point.</span></span> <span data-ttu-id="fecc6-115">Chronione maszyny można odzyskać do dowolnego punktu w tym oknie.</span><span class="sxs-lookup"><span data-stu-id="fecc6-115">Protected machines can be recovered to any point within a window.</span></span>
5. <span data-ttu-id="fecc6-116">W obszarze **Częstotliwość migawek spójności aplikacji** określ, jak często (1–12 godzin) będą tworzone punkty odzyskiwania zawierające migawki spójne z aplikacjami.</span><span class="sxs-lookup"><span data-stu-id="fecc6-116">In **App-consistent snapshot frequency**, specify how frequently (1-12 hours) recovery points containing application-consistent snapshots will be created.</span></span> <span data-ttu-id="fecc6-117">Funkcja Hyper-V wykorzystuje dwa typy migawek — standardową migawkę, która jest przyrostową migawką całej maszyny wirtualnej oraz migawkę spójności aplikacji, która wykonuje migawkę danych aplikacji wewnątrz maszyny wirtualnej w danym punkcie w czasie.</span><span class="sxs-lookup"><span data-stu-id="fecc6-117">Hyper-V uses two types of snapshots — a standard snapshot that provides an incremental snapshot of the entire virtual machine, and an application-consistent snapshot that takes a point-in-time snapshot of the application data inside the virtual machine.</span></span> <span data-ttu-id="fecc6-118">Migawki spójne z aplikacjami używają usługi Volume Shadow Copy (VSS), aby zapewnić, że aplikacje są w spójnym stanie podczas wykonywania migawki.</span><span class="sxs-lookup"><span data-stu-id="fecc6-118">Application-consistent snapshots use Volume Shadow Copy Service (VSS) to ensure that applications are in a consistent state when the snapshot is taken.</span></span> <span data-ttu-id="fecc6-119">Należy pamiętać, że jeśli migawki spójne z aplikacjami zostaną włączone, będzie to miało wpływ na wydajność aplikacji uruchomionych na źródłowych maszynach wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="fecc6-119">Note that if you enable application-consistent snapshots, it will affect the performance of applications running on source virtual machines.</span></span> <span data-ttu-id="fecc6-120">Upewnij się, że ustawiona wartość jest mniejsza od liczby skonfigurowanych dodatkowych punktów odzyskiwania.</span><span class="sxs-lookup"><span data-stu-id="fecc6-120">Ensure that the value you set is less than the number of additional recovery points you configure.</span></span>
6. <span data-ttu-id="fecc6-121">W obszarze **Czas rozpoczęcia replikacji początkowej** określ, kiedy rozpoczyna się replikacja początkowa.</span><span class="sxs-lookup"><span data-stu-id="fecc6-121">In **Initial replication start time**, indicate when to start the initial replication.</span></span> <span data-ttu-id="fecc6-122">Replikacja odbywa się z wykorzystaniem przepustowości Internetu, dlatego warto zaplanować ją poza najbardziej obciążonymi godzinami.</span><span class="sxs-lookup"><span data-stu-id="fecc6-122">The replication occurs over your internet bandwidth so you might want to schedule it outside your busy hours.</span></span>
7. <span data-ttu-id="fecc6-123">W obszarze **Szyfrowanie danych przechowywanych na platformie Azure** określ, czy należy szyfrować dane w stanie spoczynku w usłudze Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="fecc6-123">In **Encrypt data stored on Azure**, specify whether to encrypt at rest data in Azure storage.</span></span> <span data-ttu-id="fecc6-124">Następnie kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="fecc6-124">Then click **OK**.</span></span>

    ![Zasady replikacji](./media/vmm-to-azure-walkthrough-replication/gs-replication2.png)
8. <span data-ttu-id="fecc6-126">Jeśli utworzysz nowe zasady, zostaną one automatycznie skojarzone z chmurą VMM.</span><span class="sxs-lookup"><span data-stu-id="fecc6-126">When you create a new policy it's automatically associated with the VMM cloud.</span></span> <span data-ttu-id="fecc6-127">Kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="fecc6-127">Click **OK**.</span></span> <span data-ttu-id="fecc6-128">Możesz skojarzyć dodatkowe chmury VMM (oraz maszyny wirtualne w tych chmurach) z zasadami replikacji w obszarze **Replikacja** > nazwa_zasad > **Skojarz chmurę VMM**.</span><span class="sxs-lookup"><span data-stu-id="fecc6-128">You can associate additional VMM clouds (and the VMs in them) with this replication policy in **Replication** > policy name > **Associate VMM Cloud**.</span></span>

    ![Zasady replikacji](./media/vmm-to-azure-walkthrough-replication/policy-associate.png)



## <a name="next-steps"></a><span data-ttu-id="fecc6-130">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="fecc6-130">Next steps</span></span>

<span data-ttu-id="fecc6-131">Przejdź do [krok 11: Włączanie replikacji](vmm-to-azure-walkthrough-enable-replication.md)</span><span class="sxs-lookup"><span data-stu-id="fecc6-131">Go to [Step 11: Enable replication](vmm-to-azure-walkthrough-enable-replication.md)</span></span>
