---
title: "aaaEnable replikację dla maszyn wirtualnych funkcji Hyper-V, replikacja tooAzure (bez programu System Center VMM) z usługą Azure Site Recovery | Dokumentacja firmy Microsoft"
description: "Zawiera podsumowanie kroków hello należy tooenable tooAzure replikację dla maszyn wirtualnych funkcji Hyper-V przy użyciu usługi Azure Site Recovery hello"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: bd31ef01-69f1-4591-a519-e42510a6e2f4
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 06/21/2017
ms.author: raynew
ms.openlocfilehash: 1589cb7aa1fe954e075cb7bf1f4a4ec199ed3ec7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="step-10-enable-replication-for-hyper-v-vms-replicating-tooazure"></a><span data-ttu-id="3b6cd-103">Krok 10: Włączanie replikacji maszyn wirtualnych funkcji Hyper-V, replikacja tooAzure</span><span class="sxs-lookup"><span data-stu-id="3b6cd-103">Step 10: Enable replication for Hyper-V VMs replicating tooAzure</span></span>


<span data-ttu-id="3b6cd-104">W tym artykule opisano sposób replikacji tooenable dla lokalnych maszyn wirtualnych funkcji Hyper-V (nie zarządzanych przez program System Center VMM) tooAzure przy użyciu hello [usługi Azure Site Recovery](site-recovery-overview.md) w hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="3b6cd-104">This article describes how tooenable replication for on-premises Hyper-V virtual machines (not managed by System Center VMM) tooAzure, using hello [Azure Site Recovery](site-recovery-overview.md) service in hello Azure portal.</span></span>

<span data-ttu-id="3b6cd-105">Opublikuj komentarze i pytania u dołu hello w tym artykule, albo na powitania [Forum usług odzyskiwania Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="3b6cd-105">Post comments and questions at hello bottom of this article, or on hello [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>




## <a name="before-you-start"></a><span data-ttu-id="3b6cd-106">Przed rozpoczęciem</span><span class="sxs-lookup"><span data-stu-id="3b6cd-106">Before you start</span></span>

<span data-ttu-id="3b6cd-107">Przed rozpoczęciem należy upewnić się, że konto użytkownika usługi Azure ma hello wymagane [uprawnienia](site-recovery-role-based-linked-access-control.md#permissions-required-to-enable-replication-for-new-virtual-machines) tooenable replikację nowego tooAzure maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="3b6cd-107">Before you start, ensure that your Azure user account has hello required [permissions](site-recovery-role-based-linked-access-control.md#permissions-required-to-enable-replication-for-new-virtual-machines) tooenable replication of a new virtual machine tooAzure.</span></span>

## <a name="exclude-disks-from-replication"></a><span data-ttu-id="3b6cd-108">Wykluczanie dysków z replikacji</span><span class="sxs-lookup"><span data-stu-id="3b6cd-108">Exclude disks from replication</span></span>

<span data-ttu-id="3b6cd-109">Domyślnie wszystkie dyski na komputerze są replikowane.</span><span class="sxs-lookup"><span data-stu-id="3b6cd-109">By default all disks on a machine are replicated.</span></span> <span data-ttu-id="3b6cd-110">Dyski można wykluczyć z replikacji.</span><span class="sxs-lookup"><span data-stu-id="3b6cd-110">You can exclude disks from replication.</span></span> <span data-ttu-id="3b6cd-111">Na przykład nie ma dysków tooreplicate przy użyciu danych tymczasowych lub dane, które odświeżył każdym komputerze lub ponownym uruchomieniem aplikacji (na przykład pagefile.sys lub tempdb serwera SQL).</span><span class="sxs-lookup"><span data-stu-id="3b6cd-111">For example you might not want tooreplicate disks with temporary data, or data that's refreshed each time a machine or application restarts (for example pagefile.sys or SQL Server tempdb).</span></span> [<span data-ttu-id="3b6cd-112">Dowiedz się więcej</span><span class="sxs-lookup"><span data-stu-id="3b6cd-112">Learn more</span></span>](site-recovery-exclude-disk.md)


## <a name="replicate-vms"></a><span data-ttu-id="3b6cd-113">Replikowanie maszyn wirtualnych</span><span class="sxs-lookup"><span data-stu-id="3b6cd-113">Replicate VMs</span></span>

<span data-ttu-id="3b6cd-114">Włącz replikację dla maszyn wirtualnych w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="3b6cd-114">Enable replication for VMs as follows:</span></span>          

1. <span data-ttu-id="3b6cd-115">Kliknij przycisk **Replikowanie aplikacji** > **źródła**.</span><span class="sxs-lookup"><span data-stu-id="3b6cd-115">Click **Replicate application** > **Source**.</span></span> <span data-ttu-id="3b6cd-116">Po skonfigurowaniu replikacji dla powitania po raz pierwszy, możesz kliknąć **+ Replikuj** tooenable replikację dla dodatkowych maszyn.</span><span class="sxs-lookup"><span data-stu-id="3b6cd-116">After you've set up replication for hello first time, you can click **+Replicate** tooenable replication for additional machines.</span></span>

    ![Włączanie replikacji](./media/hyper-v-site-walkthrough-enable-replication/enable-replication.png)
2. <span data-ttu-id="3b6cd-118">W **źródła**, wybierz pozycję witryny hello funkcji Hyper-V.</span><span class="sxs-lookup"><span data-stu-id="3b6cd-118">In **Source**, select hello Hyper-V site.</span></span> <span data-ttu-id="3b6cd-119">Następnie kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="3b6cd-119">Then click **OK**.</span></span>
3. <span data-ttu-id="3b6cd-120">W **docelowego**, wybierz subskrypcję magazynu hello i hello model trybu failover ma toouse na platformie Azure (Zarządzanie zasobu lub classic) po pracy awaryjnej.</span><span class="sxs-lookup"><span data-stu-id="3b6cd-120">In **Target**, select hello vault subscription, and hello failover model you want toouse in Azure (classic or resource management) after failover.</span></span>
4. <span data-ttu-id="3b6cd-121">Wybierz konto magazynu hello, które chcesz toouse.</span><span class="sxs-lookup"><span data-stu-id="3b6cd-121">Select hello storage account you want toouse.</span></span> <span data-ttu-id="3b6cd-122">Jeśli nie masz konta toouse, możesz [utworzyć](#set-up-an-azure-storage-account).</span><span class="sxs-lookup"><span data-stu-id="3b6cd-122">If you don't have an account you want toouse, you can [create one](#set-up-an-azure-storage-account).</span></span> <span data-ttu-id="3b6cd-123">Następnie kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="3b6cd-123">Then click **OK**.</span></span>
5. <span data-ttu-id="3b6cd-124">Wybierz hello Azure toowhich sieci i podsieci maszyn wirtualnych platformy Azure będzie Połącz, gdy są tworzone trybu failover.</span><span class="sxs-lookup"><span data-stu-id="3b6cd-124">Select hello Azure network and subnet toowhich Azure VMs will connect when they're created failover.</span></span>

    - <span data-ttu-id="3b6cd-125">Wybierz tooapply hello ustawienia tooall komputerów sieci można włączyć replikacji **Konfiguruj teraz dla wybranych maszyn**.</span><span class="sxs-lookup"><span data-stu-id="3b6cd-125">tooapply hello network settings tooall machines you enable for replication, select **Configure now for selected machines**.</span></span>
    - <span data-ttu-id="3b6cd-126">Wybierz **później skonfigurować** hello tooselect sieć platformy Azure dla poszczególnych komputerów.</span><span class="sxs-lookup"><span data-stu-id="3b6cd-126">Select **Configure later** tooselect hello Azure network per machine.</span></span>
    - <span data-ttu-id="3b6cd-127">Jeśli nie masz sieci ma toouse, możesz [utworzyć](#set-up-an-azure-network).</span><span class="sxs-lookup"><span data-stu-id="3b6cd-127">If you don't have a network you want toouse, you can [create one](#set-up-an-azure-network).</span></span> <span data-ttu-id="3b6cd-128">Wybierz podsieć, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="3b6cd-128">Select a subnet if applicable.</span></span> <span data-ttu-id="3b6cd-129">Następnie kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="3b6cd-129">Then click **OK**.</span></span>

   ![Włączanie replikacji](./media/hyper-v-site-walkthrough-enable-replication/enable-replication11.png)

6. <span data-ttu-id="3b6cd-131">W **maszyn wirtualnych** > **wybierz maszyny wirtualne**, kliknij i zaznacz każdy komputer ma tooreplicate.</span><span class="sxs-lookup"><span data-stu-id="3b6cd-131">In **Virtual Machines** > **Select virtual machines**, click and select each machine you want tooreplicate.</span></span> <span data-ttu-id="3b6cd-132">Możesz wybrać tylko te maszyny, dla których można włączyć replikację.</span><span class="sxs-lookup"><span data-stu-id="3b6cd-132">You can only select machines for which replication can be enabled.</span></span> <span data-ttu-id="3b6cd-133">Następnie kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="3b6cd-133">Then click **OK**.</span></span>

    ![Włączanie replikacji](./media/hyper-v-site-walkthrough-enable-replication/enable-replication5-for-exclude-disk.png)

7. <span data-ttu-id="3b6cd-135">W **właściwości** > **skonfigurować właściwości**, wybierz system operacyjny hello hello wybrane maszyn wirtualnych i hello dysku systemu operacyjnego.</span><span class="sxs-lookup"><span data-stu-id="3b6cd-135">In **Properties** > **Configure properties**, select hello operating system for hello selected VMs, and hello OS disk.</span></span>
8. <span data-ttu-id="3b6cd-136">Sprawdź, że hello maszyny Wirtualnej Azure nazwę (docelowy) jest zgodna z [wymagania maszyny wirtualnej platformy Azure](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements).</span><span class="sxs-lookup"><span data-stu-id="3b6cd-136">Verify that hello Azure VM name (target name) complies with [Azure virtual machine requirements](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements).</span></span>
9. <span data-ttu-id="3b6cd-137">Domyślnie wybrane są wszystkie dyski hello hello maszyny Wirtualnej do replikacji.</span><span class="sxs-lookup"><span data-stu-id="3b6cd-137">By default all hello disks of hello VM are selected for replication.</span></span> <span data-ttu-id="3b6cd-138">Wyczyść dysków tooexclude je.</span><span class="sxs-lookup"><span data-stu-id="3b6cd-138">Clear disks tooexclude them.</span></span>
10. <span data-ttu-id="3b6cd-139">Kliknij przycisk **OK** toosave zmiany.</span><span class="sxs-lookup"><span data-stu-id="3b6cd-139">Click **OK** toosave changes.</span></span> <span data-ttu-id="3b6cd-140">Później możesz skonfigurować dodatkowe właściwości.</span><span class="sxs-lookup"><span data-stu-id="3b6cd-140">You can set additional properties later.</span></span>

    ![Włączanie replikacji](./media/hyper-v-site-walkthrough-enable-replication/enable-replication6-with-exclude-disk.png)

11. <span data-ttu-id="3b6cd-142">W **ustawienia replikacji** > **Konfigurowanie ustawień replikacji**, wybierz zasady replikacji hello ma tooapply hello chronionych maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="3b6cd-142">In **Replication settings** > **Configure replication settings**, select hello replication policy you want tooapply for hello protected VMs.</span></span> <span data-ttu-id="3b6cd-143">Następnie kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="3b6cd-143">Then click **OK**.</span></span> <span data-ttu-id="3b6cd-144">Możesz zmodyfikować zasady replikacji hello w **zasady replikacji** > Nazwa zasady > **Edytuj ustawienia**.</span><span class="sxs-lookup"><span data-stu-id="3b6cd-144">You can modify hello replication policy in **Replication policies** > policy-name > **Edit Settings**.</span></span> <span data-ttu-id="3b6cd-145">Zastosowane zmiany będą używane dla obecnie replikowanych i nowych maszyn.</span><span class="sxs-lookup"><span data-stu-id="3b6cd-145">Changes you apply will be used for machines that are already replicating, and new machines.</span></span>


   ![Włączanie replikacji](./media/hyper-v-site-walkthrough-enable-replication/enable-replication7.png)

<span data-ttu-id="3b6cd-147">Możesz śledzić postępy hello **Włącz ochronę** zadania w **zadania** > **zadania usługi Site Recovery**.</span><span class="sxs-lookup"><span data-stu-id="3b6cd-147">You can track progress of hello **Enable Protection** job in **Jobs** > **Site Recovery jobs**.</span></span> <span data-ttu-id="3b6cd-148">Po hello **zakończenia ochrony** zadania działa hello maszyna jest gotowa do pracy awaryjnej.</span><span class="sxs-lookup"><span data-stu-id="3b6cd-148">After hello **Finalize Protection** job runs hello machine is ready for failover.</span></span>


## <a name="next-steps"></a><span data-ttu-id="3b6cd-149">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="3b6cd-149">Next steps</span></span>


<span data-ttu-id="3b6cd-150">Przejdź do zbyt[krok 11: testować tryb failover](hyper-v-site-walkthrough-test-failover.md)</span><span class="sxs-lookup"><span data-stu-id="3b6cd-150">Go too[Step 11: Run a test failover](hyper-v-site-walkthrough-test-failover.md)</span></span>
