---
title: "Włącz replikację maszyn wirtualnych VMware replikację do platformy Azure z usługą Azure Site Recovery | Dokumentacja firmy Microsoft"
description: "Zawiera podsumowanie kroków należy włączyć replikację do platformy Azure dla maszyn wirtualnych VMware przy użyciu usługi Azure Site Recovery"
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: 519c5559-7032-4954-b8b5-f24f5242a954
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/27/2017
ms.author: raynew
ms.openlocfilehash: 470b9ddd8df4a4e74ec7174f79020c252323e502
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="step-11-enable-replication-for-vmware-virtual-machines-to-azure"></a><span data-ttu-id="43168-103">Krok 11: Włączanie replikacji maszyn wirtualnych VMware do platformy Azure</span><span class="sxs-lookup"><span data-stu-id="43168-103">Step 11: Enable replication for VMware virtual machines to Azure</span></span>


<span data-ttu-id="43168-104">W tym artykule opisano sposób włączania replikacji dla lokalnych maszyn wirtualnych VMware do platformy Azure, przy użyciu [usługi Azure Site Recovery](site-recovery-overview.md) w portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="43168-104">This article describes how to enable replication for on-premises VMware virtual machines to Azure, using the [Azure Site Recovery](site-recovery-overview.md) service in the Azure portal.</span></span>

<span data-ttu-id="43168-105">Opublikuj komentarze i pytania w dolnej części tego artykułu lub na [Forum usług odzyskiwania Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="43168-105">Post comments and questions at the bottom of this article, or on the [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>


## <a name="before-you-start"></a><span data-ttu-id="43168-106">Przed rozpoczęciem</span><span class="sxs-lookup"><span data-stu-id="43168-106">Before you start</span></span>

- <span data-ttu-id="43168-107">Maszyny wirtualne VMware muszą mieć [zainstalowanie składnika usługi Mobility](vmware-walkthrough-install-mobility.md).</span><span class="sxs-lookup"><span data-stu-id="43168-107">VMware VMs must have the [Mobility service component installed](vmware-walkthrough-install-mobility.md).</span></span> <span data-ttu-id="43168-108">— Jeśli maszyna wirtualna jest gotowy do instalacji w trybie wypychania, serwer przetwarzania automatycznie instaluje usługi mobilności, po włączeniu replikacji.</span><span class="sxs-lookup"><span data-stu-id="43168-108">- If a VM is prepared for push installation, the process server automatically installs the Mobility service when you enable replication.</span></span>
- <span data-ttu-id="43168-109">Twoje konto użytkownika systemu Azure wymaga określonych [uprawnienia](site-recovery-role-based-linked-access-control.md#permissions-required-to-enable-replication-for-new-virtual-machines) Aby włączyć replikację maszyny wirtualnej na platformie Azure</span><span class="sxs-lookup"><span data-stu-id="43168-109">Your Azure user account needs specific [permissions](site-recovery-role-based-linked-access-control.md#permissions-required-to-enable-replication-for-new-virtual-machines) to enable replication of a VM to Azure</span></span>
- <span data-ttu-id="43168-110">Podczas dodawania lub modyfikowania maszyn wirtualnych może potrwać do 15 minut lub dłużej aby zmiany zaczęły obowiązywać, a były widoczne w portalu.</span><span class="sxs-lookup"><span data-stu-id="43168-110">When you add or modify VMs, it can take up to 15 minutes or longer for changes to take effect, and for them to appear in the portal.</span></span>
- <span data-ttu-id="43168-111">Możesz sprawdzić czas ostatniego odnalezionych dla maszyn wirtualnych w **serwery konfiguracji** > **ostatniego kontaktu w**.</span><span class="sxs-lookup"><span data-stu-id="43168-111">You can check the last discovered time for VMs in **Configuration Servers** > **Last Contact At**.</span></span>
- <span data-ttu-id="43168-112">Aby dodać maszyn wirtualnych bez oczekiwania na zaplanowanego odnajdywania, zaznacz serwer konfiguracji (nie klikaj pozycji go) i kliknij przycisk **Odśwież**.</span><span class="sxs-lookup"><span data-stu-id="43168-112">To add VMs without waiting for the scheduled discovery, highlight the configuration server (don’t click it), and click **Refresh**.</span></span>



## <a name="exclude-disks-from-replication"></a><span data-ttu-id="43168-113">Wykluczanie dysków z replikacji</span><span class="sxs-lookup"><span data-stu-id="43168-113">Exclude disks from replication</span></span>

<span data-ttu-id="43168-114">Domyślnie wszystkie dyski na komputerze są replikowane.</span><span class="sxs-lookup"><span data-stu-id="43168-114">By default all disks on a machine are replicated.</span></span> <span data-ttu-id="43168-115">Dyski można wykluczyć z replikacji.</span><span class="sxs-lookup"><span data-stu-id="43168-115">You can exclude disks from replication.</span></span> <span data-ttu-id="43168-116">Na przykład nie może być mają być replikowane dyski danych tymczasowych lub dane, które odświeżył każdym komputerze lub ponownym uruchomieniem aplikacji (na przykład pagefile.sys lub tempdb serwera SQL).</span><span class="sxs-lookup"><span data-stu-id="43168-116">For example you might not want to replicate disks with temporary data, or data that's refreshed each time a machine or application restarts (for example pagefile.sys or SQL Server tempdb).</span></span> [<span data-ttu-id="43168-117">Dowiedz się więcej</span><span class="sxs-lookup"><span data-stu-id="43168-117">Learn more</span></span>](site-recovery-exclude-disk.md)

## <a name="replicate-vms"></a><span data-ttu-id="43168-118">Replikowanie maszyn wirtualnych</span><span class="sxs-lookup"><span data-stu-id="43168-118">Replicate VMs</span></span>

<span data-ttu-id="43168-119">Przed rozpoczęciem, Obejrzyj to szybki przegląd wideo</span><span class="sxs-lookup"><span data-stu-id="43168-119">Before you start, watch a quick video overview</span></span>

>[!VIDEO https://channel9.msdn.com/Series/Azure-Site-Recovery/VMware-to-Azure-with-ASR-Video3-Protect-VMware-Virtual-Machines/player]

1. <span data-ttu-id="43168-120">Kliknij kolejno pozycje **Krok 2. Replikowanie aplikacji** > **Źródło**.</span><span class="sxs-lookup"><span data-stu-id="43168-120">Click **Step 2: Replicate application** > **Source**.</span></span>
2. <span data-ttu-id="43168-121">W **źródła**, wybierz serwer konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="43168-121">In **Source**, select the configuration server.</span></span>
3. <span data-ttu-id="43168-122">W **komputera typu**, wybierz pozycję **maszyn wirtualnych**.</span><span class="sxs-lookup"><span data-stu-id="43168-122">In **Machine type**, select **Virtual Machines**.</span></span>
4. <span data-ttu-id="43168-123">W **vCenter/vSphere Hypervisor**, wybierz serwer vCenter, który zarządza hostem vSphere lub wybierz host.</span><span class="sxs-lookup"><span data-stu-id="43168-123">In **vCenter/vSphere Hypervisor**, select the vCenter server that manages the vSphere host, or select the host.</span></span>
5. <span data-ttu-id="43168-124">Wybierz serwer przetwarzania.</span><span class="sxs-lookup"><span data-stu-id="43168-124">Select the process server.</span></span> <span data-ttu-id="43168-125">Jeśli nie utworzono żadnych serwerów dodatkowych procesów będzie serwera konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="43168-125">If you haven't created any additional process servers this will be the configuration server.</span></span> <span data-ttu-id="43168-126">Następnie kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="43168-126">Then click **OK**.</span></span>

    ![Włączanie replikacji](./media/vmware-walkthrough-enable-replication/enable-replication2.png)

6. <span data-ttu-id="43168-128">W **docelowego**, wybierz subskrypcji i grupy zasobów, w którym chcesz utworzyć nieudane przez maszyny wirtualne.</span><span class="sxs-lookup"><span data-stu-id="43168-128">In **Target**, select the subscription and the resource group in which you want to create the failed over VMs.</span></span> <span data-ttu-id="43168-129">Wybierz model wdrażania, który ma być używany na platformie Azure (Zarządzanie zasobu lub classic) dla w trybie Failover maszyny wirtualne.</span><span class="sxs-lookup"><span data-stu-id="43168-129">Choose the deployment model that you want to use in Azure (classic or resource management), for the failed over VMs.</span></span>


7. <span data-ttu-id="43168-130">Wybierz konto magazynu Azure, którego chcesz użyć do replikacji danych.</span><span class="sxs-lookup"><span data-stu-id="43168-130">Select the Azure storage account you want to use for replicating data.</span></span> <span data-ttu-id="43168-131">Jeśli nie chcesz użyć konta, które zostały już skonfigurowane, można utworzyć nowy.</span><span class="sxs-lookup"><span data-stu-id="43168-131">If you don't want to use an account you've already set up, you can create a new one.</span></span>

8. <span data-ttu-id="43168-132">Wybierz sieć platformy Azure i podsieć, z którą nawiążą połączenie maszyny wirtualne platformy Azure, gdy zostaną uruchomione po przejściu do trybu failover.</span><span class="sxs-lookup"><span data-stu-id="43168-132">Select the Azure network and subnet to which Azure VMs will connect, when they're created after failover.</span></span> <span data-ttu-id="43168-133">Wybierz opcję **Konfiguruj teraz dla wybranych maszyn**, aby zastosować ustawienia sieci do wszystkich maszyn wybranych do ochrony.</span><span class="sxs-lookup"><span data-stu-id="43168-133">Select **Configure now for selected machines**, to apply the network setting to all machines you select for protection.</span></span> <span data-ttu-id="43168-134">Wybierz opcję **Konfiguruj później**, aby wybrać sieć platformy Azure dla poszczególnych maszyn.</span><span class="sxs-lookup"><span data-stu-id="43168-134">Select **Configure later** to select the Azure network per machine.</span></span> <span data-ttu-id="43168-135">Jeśli nie chcesz użyć istniejącej sieci, można go utworzyć.</span><span class="sxs-lookup"><span data-stu-id="43168-135">If you don't want to use an existing network, you can create one.</span></span>

    ![Włączanie replikacji](./media/vmware-walkthrough-enable-replication/enable-rep3.png)
9. <span data-ttu-id="43168-137">W pozycji **Maszyny wirtualne** > **Wybierz maszyny wirtualne** kliknij i zaznacz każdą maszynę, którą chcesz replikować.</span><span class="sxs-lookup"><span data-stu-id="43168-137">In **Virtual Machines** > **Select virtual machines**, click and select each machine you want to replicate.</span></span> <span data-ttu-id="43168-138">Możesz wybrać tylko te maszyny, dla których można włączyć replikację.</span><span class="sxs-lookup"><span data-stu-id="43168-138">You can only select machines for which replication can be enabled.</span></span> <span data-ttu-id="43168-139">Następnie kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="43168-139">Then click **OK**.</span></span>

    ![Włączanie replikacji](./media/vmware-walkthrough-enable-replication/enable-replication5.png)
10. <span data-ttu-id="43168-141">W **właściwości** > **skonfigurować właściwości**, wybierz konto, które będzie używane przez serwer przetwarzania Aby automatycznie zainstalować usługi mobilności na maszynie.</span><span class="sxs-lookup"><span data-stu-id="43168-141">In **Properties** > **Configure properties**, select the account that will be used by the process server to automatically install the Mobility service on the machine.</span></span>
11. <span data-ttu-id="43168-142">Domyślnie wszystkie dyski są replikowane.</span><span class="sxs-lookup"><span data-stu-id="43168-142">By default all disks are replicated.</span></span> <span data-ttu-id="43168-143">Kliknij przycisk **wszystkie dyski** i wyczyść wszystkie dyski, które nie mają być replikowane.</span><span class="sxs-lookup"><span data-stu-id="43168-143">Click **All Disks** and clear any disks you don't want to replicate.</span></span> <span data-ttu-id="43168-144">Następnie kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="43168-144">Then click **OK**.</span></span> <span data-ttu-id="43168-145">Później można ustawić dodatkowe właściwości maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="43168-145">You can set additional VM properties later.</span></span>

    ![Włączanie replikacji](./media/vmware-walkthrough-enable-replication/enable-replication6.png)
11. <span data-ttu-id="43168-147">W **ustawienia replikacji** > **Konfigurowanie ustawień replikacji**, sprawdź, czy jest wybrane zasady replikacji poprawne.</span><span class="sxs-lookup"><span data-stu-id="43168-147">In **Replication settings** > **Configure replication settings**, verify that the correct replication policy is selected.</span></span> <span data-ttu-id="43168-148">Jeśli zmodyfikujesz zasady, zmiany zostaną zastosowane do replikowania maszyny i nowych maszyn.</span><span class="sxs-lookup"><span data-stu-id="43168-148">If you modify a policy, changes will be applied to replicating machine, and to new machines.</span></span>
12. <span data-ttu-id="43168-149">Włącz **spójności wielu maszyn wirtualnych** Jeśli chcesz zebrać maszyn w grupie replikacji i określ nazwę grupy.</span><span class="sxs-lookup"><span data-stu-id="43168-149">Enable **Multi-VM consistency** if you want to gather machines into a replication group, and specify a name for the group.</span></span> <span data-ttu-id="43168-150">Następnie kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="43168-150">Then click **OK**.</span></span> <span data-ttu-id="43168-151">Należy pamiętać, że:</span><span class="sxs-lookup"><span data-stu-id="43168-151">Note that:</span></span>

    * <span data-ttu-id="43168-152">Komputery w grupach replikacji replikowane wspólnie i udostępnione punkty odzyskiwania spójna w razie awarii i spójności aplikacji podczas ich w tryb failover.</span><span class="sxs-lookup"><span data-stu-id="43168-152">Machines in replication groups replicate together, and have shared crash-consistent and app-consistent recovery points when they fail over.</span></span>
    * <span data-ttu-id="43168-153">Zaleca się, że użytkownik zbiera maszyn wirtualnych i serwerów fizycznych, aby odzwierciedlały obciążeń.</span><span class="sxs-lookup"><span data-stu-id="43168-153">We recommend that you gather VMs and physical servers together so that they mirror your workloads.</span></span> <span data-ttu-id="43168-154">Włączenie spójności wielu maszyn wirtualnych może wpłynąć na wydajność obciążeń i należy używać tylko w przypadku maszyn działają te same obciążenia i wymagana jest spójność.</span><span class="sxs-lookup"><span data-stu-id="43168-154">Enabling multi-VM consistency can impact workload performance, and should only be used if machines are running the same workload and you need consistency.</span></span>

    ![Włączanie replikacji](./media/vmware-walkthrough-enable-replication/enable-replication7.png)
13. <span data-ttu-id="43168-156">Kliknij przycisk **włączyć replikację**.</span><span class="sxs-lookup"><span data-stu-id="43168-156">Click **Enable Replication**.</span></span> <span data-ttu-id="43168-157">Możesz śledzić postęp **Włącz ochronę** zadania w **ustawienia** > **zadania** > **zadania usługi Site Recovery**.</span><span class="sxs-lookup"><span data-stu-id="43168-157">You can track progress of the **Enable Protection** job in **Settings** > **Jobs** > **Site Recovery Jobs**.</span></span> <span data-ttu-id="43168-158">Po uruchomieniu zadania **Sfinalizuj ochronę** maszyna jest gotowa do przejścia w tryb failover.</span><span class="sxs-lookup"><span data-stu-id="43168-158">After the **Finalize Protection** job runs the machine is ready for failover.</span></span>

## <a name="next-steps"></a><span data-ttu-id="43168-159">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="43168-159">Next steps</span></span>

<span data-ttu-id="43168-160">Przejdź do [krok 12: testować tryb failover](vmware-walkthrough-test-failover.md)</span><span class="sxs-lookup"><span data-stu-id="43168-160">Go to [Step 12: Run a test failover](vmware-walkthrough-test-failover.md)</span></span>
