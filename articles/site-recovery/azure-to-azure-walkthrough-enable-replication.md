---
title: "Włącz replikację dla maszyn wirtualnych platformy Azure do innego regionu Azure z usługą Azure Site Recovery | Dokumentacja firmy Microsoft"
description: "Zawiera podsumowanie kroków należy włączyć replikację do innego regionu Azure dla maszyn wirtualnych platformy Azure przy użyciu usługi Azure Site Recovery"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: a309644f-d36b-4188-bba7-ad45a2d9bede
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 8/01/2017
ms.author: raynew
ms.openlocfilehash: f426ba4341e61d3c7da820d7d5097b217e94ca0e
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="step-5-enable-replication-for-azure-vms"></a><span data-ttu-id="88364-103">Krok 5: Włączanie replikacji maszyn wirtualnych Azure</span><span class="sxs-lookup"><span data-stu-id="88364-103">Step 5: Enable replication for Azure VMs</span></span>


<span data-ttu-id="88364-104">Po skonfigurowaniu [magazyn usług odzyskiwania i](azure-to-azure-walkthrough-vault.md), użyj w tym artykule, aby włączyć replikację maszyn wirtualnych (VM) do innego regionu Azure, z [usługi Azure Site Recovery](site-recovery-overview.md).</span><span class="sxs-lookup"><span data-stu-id="88364-104">After setting up a [Recovery Services vault](azure-to-azure-walkthrough-vault.md), use this article to enable replication of virtual machines (VMs), to another Azure region, with [Azure Site Recovery](site-recovery-overview.md).</span></span> <span data-ttu-id="88364-105">Aby włączyć replikację, należy skonfigurować ustawienia źródłowym i docelowym, sprawdź zasady replikacji, a następnie wybierz maszyny wirtualne mają być replikowane.</span><span class="sxs-lookup"><span data-stu-id="88364-105">To enable replication, you set up source and target settings, verify the replication policy, and select VMs you want to replicate.</span></span>

- <span data-ttu-id="88364-106">Po zakończeniu tego artykułu, maszynach wirtualnych platformy Azure należy replikację do dodatkowej regionu Azure.</span><span class="sxs-lookup"><span data-stu-id="88364-106">When you finish the article, your Azure VMs should be replicating to the secondary Azure region.</span></span>
- <span data-ttu-id="88364-107">Opublikuj wszelkie komentarze u dołu w tym artykule, lub zadać pytania w [Forum usług odzyskiwania Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr)</span><span class="sxs-lookup"><span data-stu-id="88364-107">Post any comments at the bottom of this article, or ask questions in the [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr)</span></span>

>[!NOTE]
>
> <span data-ttu-id="88364-108">Replikacja maszyny Wirtualnej platformy Azure jest obecnie w przeglądzie.</span><span class="sxs-lookup"><span data-stu-id="88364-108">Azure VM replication is currently in preview.</span></span>


## <a name="select-the-source"></a><span data-ttu-id="88364-109">Wybierz źródło</span><span class="sxs-lookup"><span data-stu-id="88364-109">Select the source</span></span> 

1. <span data-ttu-id="88364-110">Magazyny usług odzyskiwania, kliknij nazwę magazynu > **+ Replikuj**.</span><span class="sxs-lookup"><span data-stu-id="88364-110">In Recovery Services vaults, click the vault name > **+Replicate**.</span></span>
2. <span data-ttu-id="88364-111">W **źródła**, wybierz pozycję **Azure — wersja ZAPOZNAWCZA**.</span><span class="sxs-lookup"><span data-stu-id="88364-111">In **Source**, select **Azure - PREVIEW**.</span></span>
2. <span data-ttu-id="88364-112">W **lokalizacja źródłowa**, wybierz źródło region platformy Azure, w którym są uruchomione maszyny wirtualne.</span><span class="sxs-lookup"><span data-stu-id="88364-112">In **Source location**, select the source Azure region where your VMs are currently running.</span></span>
3. <span data-ttu-id="88364-113">Wybierz **modelu wdrażania maszyny wirtualnej platformy Azure** dla maszyn wirtualnych: **Resource Manager** lub **klasycznego**.</span><span class="sxs-lookup"><span data-stu-id="88364-113">Select the **Azure virtual machine deployment model** for VMs: **Resource Manager** or **Classic**.</span></span>
4. <span data-ttu-id="88364-114">Wybierz **źródłowa grupa zasobów** dla maszyn wirtualnych Menedżera zasobów lub **usługi w chmurze** klasycznych maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="88364-114">Select the **Source resource group** for Resource Manager VMs, or **cloud service** for classic VMs.</span></span>
5. <span data-ttu-id="88364-115">Kliknij pozycję **OK**, aby zapisać ustawienia.</span><span class="sxs-lookup"><span data-stu-id="88364-115">Click **OK** to save the settings.</span></span>

    ![Skonfiguruj źródło](./media/azure-to-azure-walkthrough-enable-replication/source.png)

## <a name="select-the-vms"></a><span data-ttu-id="88364-117">Wybierz maszyny wirtualne</span><span class="sxs-lookup"><span data-stu-id="88364-117">Select the VMs</span></span>

<span data-ttu-id="88364-118">Usługa Site Recovery pobiera listę maszyn wirtualnych, związanych z subskrypcji i zasobu grupy/usługa w chmurze.</span><span class="sxs-lookup"><span data-stu-id="88364-118">Site Recovery retrieves a list of the VMs associated with the subscription and resource group/cloud service.</span></span>

1. <span data-ttu-id="88364-119">W **maszyn wirtualnych**, wybierz maszyny wirtualne mają być replikowane.</span><span class="sxs-lookup"><span data-stu-id="88364-119">In **Virtual Machines**, select the VMs you want to replicate.</span></span>
2. <span data-ttu-id="88364-120">Kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="88364-120">Click **OK**.</span></span>

    ![Wybierz maszyny wirtualne](./media/azure-to-azure-walkthrough-enable-replication/vms.png)


## <a name="configure-settings"></a><span data-ttu-id="88364-122">Konfigurowanie ustawień</span><span class="sxs-lookup"><span data-stu-id="88364-122">Configure settings</span></span>

<span data-ttu-id="88364-123">Przepisy odzyskiwania lokacji domyślne ustawienia dla region docelowy (zgodnie z ustawieniami region źródłowego), a zasady replikacji:</span><span class="sxs-lookup"><span data-stu-id="88364-123">Site Recovery provisions default settings for the target region (based on the source region settings), and the replication policy:</span></span>

   - <span data-ttu-id="88364-124">**Lokalizacja docelowa**: region docelowy, którego chcesz użyć do odzyskiwania po awarii.</span><span class="sxs-lookup"><span data-stu-id="88364-124">**Target location**: The target region you want to use for disaster recovery.</span></span> <span data-ttu-id="88364-125">Zaleca się, że lokalizacja docelowa odpowiada lokalizacji magazynu usługi Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="88364-125">We recommend that the target location matches the location of the Site Recovery vault.</span></span>
   - <span data-ttu-id="88364-126">**Docelowa grupa zasobów**: grupy zasobów, do których maszynach wirtualnych platformy Azure w celu region będzie należał po pracy awaryjnej.</span><span class="sxs-lookup"><span data-stu-id="88364-126">**Target resource group**: Resource group to which Azure VMs in the target region will belong after failover.</span></span> <span data-ttu-id="88364-127">Domyślnie usługi Site Recovery tworzy nową grupę zasobów w regionie docelowych z sufiksem "asr".</span><span class="sxs-lookup"><span data-stu-id="88364-127">By default, Site Recovery creates a new resource group in the target region with an "asr" suffix.</span></span> 
   - <span data-ttu-id="88364-128">**Wirtualne sieci docelowej**: sieci, na których maszynach wirtualnych Azure w celu region zostaną umieszczone po pracy awaryjnej.</span><span class="sxs-lookup"><span data-stu-id="88364-128">**Target virtual network**: The network in which Azure VMs in the target region will be located after failover.</span></span> <span data-ttu-id="88364-129">Domyślnie usługa Site Recovery tworzy nową sieć wirtualną (i podsieci) w regionie docelowych z sufiksem "asr".</span><span class="sxs-lookup"><span data-stu-id="88364-129">By default, Site Recovery creates a new virtual network (and subnets) in the target region with an "asr" suffix.</span></span> <span data-ttu-id="88364-130">Ta sieć jest zamapowana na sieć źródła.</span><span class="sxs-lookup"><span data-stu-id="88364-130">This network is mapped to your source network.</span></span> <span data-ttu-id="88364-131">Należy pamiętać, przypisanie określonego adresu IP po przejściu w tryb failover maszyny wirtualnej, jeśli chcesz zachować ten sam adres IP w lokalizacji źródłowej i docelowej.</span><span class="sxs-lookup"><span data-stu-id="88364-131">Note that you can assign a specific IP address after failover of a VM, if you need to retain the same IP address in the source and target locations.</span></span> 
   - <span data-ttu-id="88364-132">**Buforowanie kont magazynu**: Usługa Site Recovery używa konta magazynu w regionie źródła.</span><span class="sxs-lookup"><span data-stu-id="88364-132">**Cache storage accounts**: Site Recovery uses a storage account in the source region.</span></span> <span data-ttu-id="88364-133">Zmiany w źródłowe maszyny wirtualne są wysyłane do tego konta, przed replikacji do lokalizacji docelowej.</span><span class="sxs-lookup"><span data-stu-id="88364-133">Changes on source VMs are sent to this account, before replication to the target location.</span></span> 
   - <span data-ttu-id="88364-134">**Docelowa kont magazynu**: Domyślnie, Usługa Site Recovery tworzy nowe konto magazynu, w obszarze docelowym dublowanego źródła konta magazynu maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="88364-134">**Target storage accounts**: By default, Site Recovery creates a new storage account in the target region, to mirror the source VM storage account.</span></span>
   -  <span data-ttu-id="88364-135">**Docelowa zestawów dostępności**: Domyślnie, Usługa Site Recovery tworzy nowy zestawem dostępności w region docelowy, wraz z sufiksem "asr".</span><span class="sxs-lookup"><span data-stu-id="88364-135">**Target availability sets**: By default, Site Recovery creates a new availability set in the target region, with the "asr" suffix.</span></span> 
   - <span data-ttu-id="88364-136">**Nazwa zasad replikacji**: Nazwa zasad.</span><span class="sxs-lookup"><span data-stu-id="88364-136">**Replication policy name**: Policy name.</span></span>
   - <span data-ttu-id="88364-137">**Przechowywania punktu odzyskiwania**: domyślnie Site Recovery przechowuje punkty odzyskiwania przez 24 godziny.</span><span class="sxs-lookup"><span data-stu-id="88364-137">**Recovery point retention**: By default Site Recovery keeps recovery points for 24 hours.</span></span> <span data-ttu-id="88364-138">Można skonfigurować wartość z zakresu od 1 do 72 godzin.</span><span class="sxs-lookup"><span data-stu-id="88364-138">You can configure a value between 1 and 72 hours.</span></span>
   - <span data-ttu-id="88364-139">**Częstotliwość migawek spójności aplikacji**: domyślnie Site Recovery przyjmuje migawki dotyczącej spójności aplikacji co 4 godziny.</span><span class="sxs-lookup"><span data-stu-id="88364-139">**App-consistent snapshot frequency**: By default Site Recovery takes an app-consistent snapshot every 4 hours.</span></span> <span data-ttu-id="88364-140">Można skonfigurować dowolną wartość z zakresu od 1 do 12 godzin.</span><span class="sxs-lookup"><span data-stu-id="88364-140">You can configure any value between 1 and 12 hours.</span></span> <span data-ttu-id="88364-141">Dane są replikowane w sposób ciągły:</span><span class="sxs-lookup"><span data-stu-id="88364-141">Data is replicated continuously:</span></span>
    - <span data-ttu-id="88364-142">Punktów odzyskiwania zapewniających spójność awarii zachowania spójności danych zapisu kolejności podczas tworzenia.</span><span class="sxs-lookup"><span data-stu-id="88364-142">Crash-consistent recovery points maintain consistent data write-order when created.</span></span> <span data-ttu-id="88364-143">Ten rodzaj punktu odzyskiwania jest zwykle wystarczające, jeśli aplikacja jest przeznaczona Aby dokonać odzyskiwania po awarii bez niespójności w danych</span><span class="sxs-lookup"><span data-stu-id="88364-143">This type of recovery point is usually sufficient if your app is designed to recover from a crash without data inconsistencies</span></span>
    - <span data-ttu-id="88364-144">Punktów odzyskiwania zapewniających spójność awarii są generowane co kilka minut.</span><span class="sxs-lookup"><span data-stu-id="88364-144">Crash-consistent recovery points are generated every few minutes.</span></span> <span data-ttu-id="88364-145">Przy użyciu tych punktów odzyskiwania w tryb failover i odzyskiwania maszyn wirtualnych zapewnia odzyskiwania punktu cel (RPO) kolejności minut.</span><span class="sxs-lookup"><span data-stu-id="88364-145">Using these recovery points to fail over and recover your VMs provides a Recovery Point Objective (RPO) in the order of minutes.</span></span>
    - <span data-ttu-id="88364-146">Punktów odzyskiwania zapewniających spójność aplikacji (oprócz spójności zapisu kolejności) zapewnić ukończenie wszystkich operacji uruchomionych aplikacji i opróżnienia buforów na dysku (przełączany w stan spoczynku aplikacji).</span><span class="sxs-lookup"><span data-stu-id="88364-146">App-consistent recovery points (in addition to write-order consistency) ensure that running apps complete all operations and flush buffers to disk (application quiescing).</span></span> <span data-ttu-id="88364-147">Firma Microsoft zaleca korzystanie z tych punktów odzyskiwania dla bazy danych aplikacji, takich jak SQL Server, Oracle i Exchange.</span><span class="sxs-lookup"><span data-stu-id="88364-147">We recommend you use these recovery points for database apps such as SQL Server, Oracle, and Exchange.</span></span>
        
    ![Konfigurowanie ustawień](./media/azure-to-azure-walkthrough-enable-replication/settings.png)


### <a name="modify-settings"></a><span data-ttu-id="88364-149">Modyfikowanie ustawień</span><span class="sxs-lookup"><span data-stu-id="88364-149">Modify settings</span></span>

<span data-ttu-id="88364-150">Jeśli chcesz zmodyfikować ustawienia zasad docelowych i replikacji, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="88364-150">If you want to modify target and replication policy settings, do the following:</span></span>

1. <span data-ttu-id="88364-151">Aby wyświetlić lub zmodyfikować ustawienia obiektu docelowego, kliknij przycisk **ustawienia**.</span><span class="sxs-lookup"><span data-stu-id="88364-151">To view or modify target settings, click **Settings**.</span></span>
2. <span data-ttu-id="88364-152">Aby zastąpić domyślne ustawienia docelowych, kliknij przycisk **Dostosuj**.</span><span class="sxs-lookup"><span data-stu-id="88364-152">To override the default target settings, click **Customize**.</span></span> <span data-ttu-id="88364-153">Można określić docelowa grupa zasobów, sieć wirtualną, zestawu dostępności i docelowe konto magazynu.</span><span class="sxs-lookup"><span data-stu-id="88364-153">You can specify a target resource group, virtual network, availability set, and target storage account.</span></span> <span data-ttu-id="88364-154">Zestawy dostępności można dodawać tylko, jeśli maszyny wirtualne są częścią zestawu w regionie źródła.</span><span class="sxs-lookup"><span data-stu-id="88364-154">You can only add availability sets if VMs are part of a set in the source region.</span></span>

    ![Konfigurowanie ustawień](./media/azure-to-azure-walkthrough-enable-replication/customize-target.png)

3. <span data-ttu-id="88364-156">Aby zastąpić ustawienia replikacji dla punktów odzyskiwania i migawek spójności aplikacji, kliknij przycisk **Dostosuj** obok **zasad replikacji**.</span><span class="sxs-lookup"><span data-stu-id="88364-156">To override replication settings for recovery points and app-consistent snapshots, click **Customize** next to **Replication Policy**.</span></span>
 
    ![Konfigurowanie ustawień](./media/azure-to-azure-walkthrough-enable-replication/customize-policy.png)

4. <span data-ttu-id="88364-158">Aby rozpocząć Inicjowanie obsługi zasobów docelowych, kliknij **Utwórz zasoby docelowe**.</span><span class="sxs-lookup"><span data-stu-id="88364-158">To start provisioning the target resources, click **Create target resources**.</span></span> <span data-ttu-id="88364-159">Inicjowanie obsługi administracyjnej ma minuty.</span><span class="sxs-lookup"><span data-stu-id="88364-159">Provisioning takes a minute or so.</span></span> <span data-ttu-id="88364-160">Nie zamykaj bloku podczas inicjowania obsługi lub należy zacząć od początku.</span><span class="sxs-lookup"><span data-stu-id="88364-160">Don't close the blade during provisioning, or you'll have to start over.</span></span>




## <a name="enable-replication"></a><span data-ttu-id="88364-161">Włączanie replikacji</span><span class="sxs-lookup"><span data-stu-id="88364-161">Enable replication</span></span>

1. <span data-ttu-id="88364-162">W **ustawienia**, kliknij przycisk **włączyć replikację**.</span><span class="sxs-lookup"><span data-stu-id="88364-162">In **Settings**, click **Enable replication**.</span></span> <span data-ttu-id="88364-163">Dzięki temu replikacji początkowej wybranych maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="88364-163">This enables initial replication of the VMs you selected.</span></span> <span data-ttu-id="88364-164">Stan replikacji początkowej może potrwać pewien czas, aby odświeżyć.</span><span class="sxs-lookup"><span data-stu-id="88364-164">Initial replication status might take some time to refresh.</span></span> <span data-ttu-id="88364-165">Kliknij przycisk **Odśwież** można pobrać najnowszy stan.</span><span class="sxs-lookup"><span data-stu-id="88364-165">Click **Refresh** to get the latest status.</span></span>

2. <span data-ttu-id="88364-166">Możesz śledzić postęp **Włącz ochronę** zadania w **ustawienia** > **zadania** > **zadania usługi Site Recovery**.</span><span class="sxs-lookup"><span data-stu-id="88364-166">You can track progress of the **Enable protection** job in **Settings** > **Jobs** > **Site Recovery Jobs**.</span></span>

3. <span data-ttu-id="88364-167">W **ustawienia** > **elementy replikowane**, można wyświetlić stan maszyn wirtualnych i postęp replikacji początkowej.</span><span class="sxs-lookup"><span data-stu-id="88364-167">In **Settings** > **Replicated Items**, you can view the status of VMs and the initial replication progress.</span></span> <span data-ttu-id="88364-168">Kliknij maszynę Wirtualną, aby przejść do jego ustawień.</span><span class="sxs-lookup"><span data-stu-id="88364-168">Click the VM to drill down into its settings.</span></span>



## <a name="next-steps"></a><span data-ttu-id="88364-169">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="88364-169">Next steps</span></span>

<span data-ttu-id="88364-170">Przejdź do [krok 6: testować tryb failover](azure-to-azure-walkthrough-test-failover.md)</span><span class="sxs-lookup"><span data-stu-id="88364-170">Go to [Step 6: Run a test failover](azure-to-azure-walkthrough-test-failover.md)</span></span>
