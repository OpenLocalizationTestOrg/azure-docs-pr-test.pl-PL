---
title: "Włącz replikację funkcji Hyper-V do lokacji dodatkowej z usługą Azure Site Recovery | Dokumentacja firmy Microsoft"
description: "W tym artykule opisano, jak włączyć replikację dla maszyn wirtualnych funkcji Hyper-V replikację do dodatkowej lokacji programu System Center VMM z usługą Azure Site Recovery."
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: d8782d14-9fef-4396-8912-ff945efc851b
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/30/2017
ms.author: raynew
ms.openlocfilehash: 6673d192dbc18bfc955d9e7e3c55893512511ffb
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="step-9-enable-replication-to-a-secondary-site-for-hyper-v-vms"></a><span data-ttu-id="5bd7f-103">Krok 9: Włączanie replikacji do lokacji dodatkowej dla maszyn wirtualnych funkcji Hyper-V</span><span class="sxs-lookup"><span data-stu-id="5bd7f-103">Step 9: Enable replication to a secondary site for Hyper-V VMs</span></span>


<span data-ttu-id="5bd7f-104">Po konfigurowania zasad replikacji, użyj w tym artykule, aby włączyć replikacji do lokacji dodatkowej programu System Center Virtual Machine Manager (VMM) dla maszyn wirtualnych funkcji Hyper-V lokalnymi (VM), za pomocą [usługi Azure Site Recovery](site-recovery-overview.md).</span><span class="sxs-lookup"><span data-stu-id="5bd7f-104">After setting up a replication policy, use this article to enable replication to a secondary System Center Virtual Machine Manager (VMM) site for on-premises Hyper-V virtual machines (VM), using [Azure Site Recovery](site-recovery-overview.md).</span></span>

<span data-ttu-id="5bd7f-105">Po przeczytaniu tego artykułu zamieść wszelkie komentarze u dołu lub na [forum usług Azure Recovery Services](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="5bd7f-105">After reading this article, post any comments at the bottom, or on the [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>



## <a name="select-vms-to-replicate"></a><span data-ttu-id="5bd7f-106">Wybierz maszyny wirtualne do replikacji</span><span class="sxs-lookup"><span data-stu-id="5bd7f-106">Select VMs to replicate</span></span>

1. <span data-ttu-id="5bd7f-107">Kliknij kolejno pozycje **Krok 2. Replikowanie aplikacji** > **Źródło**.</span><span class="sxs-lookup"><span data-stu-id="5bd7f-107">Click **Step 2: Replicate application** > **Source**.</span></span> 

    ![Włączanie replikacji](./media/vmm-to-vmm-walkthrough-enable-replication/enable-replication1.png)

2. <span data-ttu-id="5bd7f-109">W **źródła**, wybierz serwer programu VMM oraz chmury, w którym znajdują się hosty funkcji Hyper-V mają być replikowane.</span><span class="sxs-lookup"><span data-stu-id="5bd7f-109">In **Source**, select the VMM server, and the cloud in which the Hyper-V hosts you want to replicate are located.</span></span> <span data-ttu-id="5bd7f-110">Następnie kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="5bd7f-110">Then click **OK**.</span></span>

    ![Włączanie replikacji](./media/vmm-to-vmm-walkthrough-enable-replication/enable-replication2.png)
3. <span data-ttu-id="5bd7f-112">W **docelowego**, sprawdź pomocniczy serwer programu VMM i w chmurze.</span><span class="sxs-lookup"><span data-stu-id="5bd7f-112">In **Target**, verify the secondary VMM server and cloud.</span></span>
4. <span data-ttu-id="5bd7f-113">W **maszyn wirtualnych**, wybierz maszyny wirtualne, które chcesz chronić z listy.</span><span class="sxs-lookup"><span data-stu-id="5bd7f-113">In **Virtual machines**, select the VMs you want to protect from the list.</span></span>

    ![Włączanie ochrony maszyny wirtualnej](./media/vmm-to-vmm-walkthrough-enable-replication/enable-replication5.png)

<span data-ttu-id="5bd7f-115">Możesz śledzić postęp **Włącz ochronę** akcji w **zadania** > **zadania usługi Site Recovery**.</span><span class="sxs-lookup"><span data-stu-id="5bd7f-115">You can track progress of the **Enable Protection** action in **Jobs** > **Site Recovery jobs**.</span></span> <span data-ttu-id="5bd7f-116">Po **zakończenia ochrony** zadanie zostało ukończone, Replikacja początkowa została zakończona i maszyna wirtualna jest gotowa do pracy awaryjnej.</span><span class="sxs-lookup"><span data-stu-id="5bd7f-116">After the **Finalize Protection** job completes, the initial replication is complete, and the virtual machine is ready for failover.</span></span>

<span data-ttu-id="5bd7f-117">Należy pamiętać, że:</span><span class="sxs-lookup"><span data-stu-id="5bd7f-117">Note that:</span></span>

- <span data-ttu-id="5bd7f-118">Można również włączyć ochronę maszyn wirtualnych w konsoli programu VMM.</span><span class="sxs-lookup"><span data-stu-id="5bd7f-118">You can also enable protection for virtual machines in the VMM console.</span></span> <span data-ttu-id="5bd7f-119">Kliknij przycisk **Włącz ochronę** na pasku narzędzi we właściwościach maszyny wirtualnej > **usługi Azure Site Recovery** kartę.</span><span class="sxs-lookup"><span data-stu-id="5bd7f-119">Click **Enable Protection** on the toolbar in the virtual machine properties > **Azure Site Recovery** tab.</span></span>
- <span data-ttu-id="5bd7f-120">Po włączeniu replikacji można wyświetlić właściwości dla maszyny Wirtualnej w ramach **elementy replikowane**.</span><span class="sxs-lookup"><span data-stu-id="5bd7f-120">After you've enabled replication, you can view properties for the VM in **Replicated Items**.</span></span> <span data-ttu-id="5bd7f-121">Na **Essentials** pulpitu nawigacyjnego, znajdują się informacje dotyczące zasad replikacji dla maszyny Wirtualnej i jej stanie.</span><span class="sxs-lookup"><span data-stu-id="5bd7f-121">On the **Essentials** dashboard, you can see information about the replication policy for the VM and its status.</span></span> <span data-ttu-id="5bd7f-122">Kliknij przycisk **właściwości** więcej szczegółów.</span><span class="sxs-lookup"><span data-stu-id="5bd7f-122">Click **Properties** for more details.</span></span>

## <a name="onboard-existing-vms"></a><span data-ttu-id="5bd7f-123">Dodaj istniejące maszyny wirtualne</span><span class="sxs-lookup"><span data-stu-id="5bd7f-123">Onboard existing VMs</span></span>

<span data-ttu-id="5bd7f-124">Jeśli masz istniejące maszyny wirtualne w programie VMM, które są replikowane z funkcji Hyper-V Replica, możesz dołączyć je do replikacji usługi Azure Site Recovery w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="5bd7f-124">If you have existing virtual machines in VMM that are replicating with Hyper-V Replica, you can onboard them for Azure Site Recovery replication as follows:</span></span>

1. <span data-ttu-id="5bd7f-125">Upewnij się, że serwer funkcji Hyper-V hosting istniejącej maszyny Wirtualnej znajduje się w chmurze podstawowej oraz że serwera funkcji Hyper-V obsługującego maszyny wirtualnej repliki znajduje się w chmurze dodatkowej.</span><span class="sxs-lookup"><span data-stu-id="5bd7f-125">Ensure that the Hyper-V server hosting the existing VM is located in the primary cloud, and that the Hyper-V server hosting the replica virtual machine is located in the secondary cloud.</span></span>
2. <span data-ttu-id="5bd7f-126">Upewnij się, że skonfigurowano zasady replikacji dla chmury VMM podstawowej.</span><span class="sxs-lookup"><span data-stu-id="5bd7f-126">Make sure a replication policy is configured for the primary VMM cloud.</span></span>
3. <span data-ttu-id="5bd7f-127">Włączanie replikacji podstawowej maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="5bd7f-127">Enable replication for the primary virtual machine.</span></span> <span data-ttu-id="5bd7f-128">Azure Site Recovery i VMM upewnij się, że wykrycia tego samego hosta repliki i maszyny wirtualne i usługi Azure Site Recovery spowoduje ponowne użycie i ponownie ustanowić replikację przy użyciu określonych ustawień.</span><span class="sxs-lookup"><span data-stu-id="5bd7f-128">Azure Site Recovery and VMM ensure that the same replica host and virtual machine is detected, and Azure Site Recovery will reuse and reestablish replication using the specified settings.</span></span>


## <a name="next-steps"></a><span data-ttu-id="5bd7f-129">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="5bd7f-129">Next steps</span></span>

<span data-ttu-id="5bd7f-130">Przejdź do [kroku 10: testować tryb failover](vmm-to-vmm-walkthrough-test-failover.md).</span><span class="sxs-lookup"><span data-stu-id="5bd7f-130">Go to [Step 10: Run a test failover](vmm-to-vmm-walkthrough-test-failover.md).</span></span>
