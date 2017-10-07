---
title: "aaaEnable replikację dla maszyn wirtualnych platformy Azure tooanother region platformy Azure z usługą Azure Site Recovery | Dokumentacja firmy Microsoft"
description: "Zawiera podsumowanie kroków hello potrzebne tooenable replikacji tooanother region platformy Azure dla maszyn wirtualnych platformy Azure przy użyciu usługi Azure Site Recovery hello"
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
ms.openlocfilehash: 2fa03db45a18ccb8b9f31ed05589be0dd6d5f031
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="step-5-enable-replication-for-azure-vms"></a><span data-ttu-id="14188-103">Krok 5: Włączanie replikacji maszyn wirtualnych Azure</span><span class="sxs-lookup"><span data-stu-id="14188-103">Step 5: Enable replication for Azure VMs</span></span>


<span data-ttu-id="14188-104">Po skonfigurowaniu [magazyn usług odzyskiwania i](azure-to-azure-walkthrough-vault.md), za pomocą tego artykułu replikacji tooenable maszyn wirtualnych (VM), tooanother regionu Azure, [usługi Azure Site Recovery](site-recovery-overview.md).</span><span class="sxs-lookup"><span data-stu-id="14188-104">After setting up a [Recovery Services vault](azure-to-azure-walkthrough-vault.md), use this article tooenable replication of virtual machines (VMs), tooanother Azure region, with [Azure Site Recovery](site-recovery-overview.md).</span></span> <span data-ttu-id="14188-105">tooenable replikacji, należy skonfigurować ustawienia źródłowym i docelowym, sprawdź hello zasad replikacji, a następnie wybierz maszyny wirtualne mają tooreplicate.</span><span class="sxs-lookup"><span data-stu-id="14188-105">tooenable replication, you set up source and target settings, verify hello replication policy, and select VMs you want tooreplicate.</span></span>

- <span data-ttu-id="14188-106">Po zakończeniu hello artykułu, maszynach wirtualnych platformy Azure powinna być replikacja toohello dodatkowej region platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="14188-106">When you finish hello article, your Azure VMs should be replicating toohello secondary Azure region.</span></span>
- <span data-ttu-id="14188-107">Opublikuj wszelkie komentarze u dołu hello w tym artykule, lub zadać pytania w hello [Forum usług odzyskiwania Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr)</span><span class="sxs-lookup"><span data-stu-id="14188-107">Post any comments at hello bottom of this article, or ask questions in hello [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr)</span></span>

>[!NOTE]
>
> <span data-ttu-id="14188-108">Replikacja maszyny Wirtualnej platformy Azure jest obecnie w przeglądzie.</span><span class="sxs-lookup"><span data-stu-id="14188-108">Azure VM replication is currently in preview.</span></span>


## <a name="select-hello-source"></a><span data-ttu-id="14188-109">Wybierz źródło hello</span><span class="sxs-lookup"><span data-stu-id="14188-109">Select hello source</span></span> 

1. <span data-ttu-id="14188-110">Magazyny usług odzyskiwania, kliknij nazwę magazynu hello > **+ Replikuj**.</span><span class="sxs-lookup"><span data-stu-id="14188-110">In Recovery Services vaults, click hello vault name > **+Replicate**.</span></span>
2. <span data-ttu-id="14188-111">W **źródła**, wybierz pozycję **Azure — wersja ZAPOZNAWCZA**.</span><span class="sxs-lookup"><span data-stu-id="14188-111">In **Source**, select **Azure - PREVIEW**.</span></span>
2. <span data-ttu-id="14188-112">W **lokalizacja źródłowa**, wybierz źródło hello region platformy Azure, w którym są uruchomione maszyny wirtualne.</span><span class="sxs-lookup"><span data-stu-id="14188-112">In **Source location**, select hello source Azure region where your VMs are currently running.</span></span>
3. <span data-ttu-id="14188-113">Wybierz hello **modelu wdrażania maszyny wirtualnej platformy Azure** dla maszyn wirtualnych: **Resource Manager** lub **klasycznego**.</span><span class="sxs-lookup"><span data-stu-id="14188-113">Select hello **Azure virtual machine deployment model** for VMs: **Resource Manager** or **Classic**.</span></span>
4. <span data-ttu-id="14188-114">Wybierz hello **źródłowa grupa zasobów** dla maszyn wirtualnych Menedżera zasobów lub **usługi w chmurze** klasycznych maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="14188-114">Select hello **Source resource group** for Resource Manager VMs, or **cloud service** for classic VMs.</span></span>
5. <span data-ttu-id="14188-115">Kliknij przycisk **OK** toosave hello ustawienia.</span><span class="sxs-lookup"><span data-stu-id="14188-115">Click **OK** toosave hello settings.</span></span>

    ![Konfigurowanie źródła hello](./media/azure-to-azure-walkthrough-enable-replication/source.png)

## <a name="select-hello-vms"></a><span data-ttu-id="14188-117">Wybierz hello maszyny wirtualne</span><span class="sxs-lookup"><span data-stu-id="14188-117">Select hello VMs</span></span>

<span data-ttu-id="14188-118">Usługa Site Recovery pobiera listę hello maszyn wirtualnych z którą skojarzona hello subskrypcji i zasobu grupy/usługa w chmurze.</span><span class="sxs-lookup"><span data-stu-id="14188-118">Site Recovery retrieves a list of hello VMs associated with hello subscription and resource group/cloud service.</span></span>

1. <span data-ttu-id="14188-119">W **maszyn wirtualnych**, wybierz hello maszyny wirtualne mają tooreplicate.</span><span class="sxs-lookup"><span data-stu-id="14188-119">In **Virtual Machines**, select hello VMs you want tooreplicate.</span></span>
2. <span data-ttu-id="14188-120">Kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="14188-120">Click **OK**.</span></span>

    ![Wybierz maszyny wirtualne](./media/azure-to-azure-walkthrough-enable-replication/vms.png)


## <a name="configure-settings"></a><span data-ttu-id="14188-122">Konfigurowanie ustawień</span><span class="sxs-lookup"><span data-stu-id="14188-122">Configure settings</span></span>

<span data-ttu-id="14188-123">Domyślne ustawienia dla region docelowy hello (na podstawie hello źródła region ustawień), udostępnia usługi Site Recovery i zasad replikacji hello:</span><span class="sxs-lookup"><span data-stu-id="14188-123">Site Recovery provisions default settings for hello target region (based on hello source region settings), and hello replication policy:</span></span>

   - <span data-ttu-id="14188-124">**Lokalizacja docelowa**: hello region docelowy ma toouse odzyskiwania po awarii.</span><span class="sxs-lookup"><span data-stu-id="14188-124">**Target location**: hello target region you want toouse for disaster recovery.</span></span> <span data-ttu-id="14188-125">Firma Microsoft zaleca zgodność hello lokalizację magazynu usługi Site Recovery hello hello lokalizacji docelowej.</span><span class="sxs-lookup"><span data-stu-id="14188-125">We recommend that hello target location matches hello location of hello Site Recovery vault.</span></span>
   - <span data-ttu-id="14188-126">**Docelowa grupa zasobów**: toowhich grupy zasobów maszyn wirtualnych Azure w region docelowy hello będą należeć po pracy awaryjnej.</span><span class="sxs-lookup"><span data-stu-id="14188-126">**Target resource group**: Resource group toowhich Azure VMs in hello target region will belong after failover.</span></span> <span data-ttu-id="14188-127">Domyślnie usługi Site Recovery tworzy nową grupę zasobów w regionie docelowym hello z sufiksem "asr".</span><span class="sxs-lookup"><span data-stu-id="14188-127">By default, Site Recovery creates a new resource group in hello target region with an "asr" suffix.</span></span> 
   - <span data-ttu-id="14188-128">**Wirtualne sieci docelowej**: hello sieci, na których maszynach wirtualnych Azure w hello region docelowy zostaną umieszczone po pracy awaryjnej.</span><span class="sxs-lookup"><span data-stu-id="14188-128">**Target virtual network**: hello network in which Azure VMs in hello target region will be located after failover.</span></span> <span data-ttu-id="14188-129">Domyślnie usługa Site Recovery tworzy nową sieć wirtualną (i podsieci) region docelowy hello z sufiksem "asr".</span><span class="sxs-lookup"><span data-stu-id="14188-129">By default, Site Recovery creates a new virtual network (and subnets) in hello target region with an "asr" suffix.</span></span> <span data-ttu-id="14188-130">Ta sieć jest siecią źródła tooyour mapowane.</span><span class="sxs-lookup"><span data-stu-id="14188-130">This network is mapped tooyour source network.</span></span> <span data-ttu-id="14188-131">Należy pamiętać, że po przejściu w tryb failover maszyny wirtualnej można przypisać określony adres IP, jeśli potrzebujesz tooretain hello sam adres IP w lokalizacji źródłowej i docelowej hello.</span><span class="sxs-lookup"><span data-stu-id="14188-131">Note that you can assign a specific IP address after failover of a VM, if you need tooretain hello same IP address in hello source and target locations.</span></span> 
   - <span data-ttu-id="14188-132">**Buforowanie kont magazynu**: Usługa Site Recovery używa konta magazynu w regionie źródła hello.</span><span class="sxs-lookup"><span data-stu-id="14188-132">**Cache storage accounts**: Site Recovery uses a storage account in hello source region.</span></span> <span data-ttu-id="14188-133">Zmiany dotyczące źródłowe maszyny wirtualne będą wysyłane konta toothis przed lokalizacji docelowej toohello replikacji.</span><span class="sxs-lookup"><span data-stu-id="14188-133">Changes on source VMs are sent toothis account, before replication toohello target location.</span></span> 
   - <span data-ttu-id="14188-134">**Docelowa kont magazynu**: Domyślnie, Usługa Site Recovery tworzy nowe konto magazynu w regionie docelowym hello, toomirror hello źródła konta magazynu maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="14188-134">**Target storage accounts**: By default, Site Recovery creates a new storage account in hello target region, toomirror hello source VM storage account.</span></span>
   -  <span data-ttu-id="14188-135">**Docelowa zestawów dostępności**: Domyślnie, Usługa Site Recovery tworzy nowy zestawem dostępności w hello region docelowy, z sufiksem "asr" hello.</span><span class="sxs-lookup"><span data-stu-id="14188-135">**Target availability sets**: By default, Site Recovery creates a new availability set in hello target region, with hello "asr" suffix.</span></span> 
   - <span data-ttu-id="14188-136">**Nazwa zasad replikacji**: Nazwa zasad.</span><span class="sxs-lookup"><span data-stu-id="14188-136">**Replication policy name**: Policy name.</span></span>
   - <span data-ttu-id="14188-137">**Przechowywania punktu odzyskiwania**: domyślnie Site Recovery przechowuje punkty odzyskiwania przez 24 godziny.</span><span class="sxs-lookup"><span data-stu-id="14188-137">**Recovery point retention**: By default Site Recovery keeps recovery points for 24 hours.</span></span> <span data-ttu-id="14188-138">Można skonfigurować wartość z zakresu od 1 do 72 godzin.</span><span class="sxs-lookup"><span data-stu-id="14188-138">You can configure a value between 1 and 72 hours.</span></span>
   - <span data-ttu-id="14188-139">**Częstotliwość migawek spójności aplikacji**: domyślnie Site Recovery przyjmuje migawki dotyczącej spójności aplikacji co 4 godziny.</span><span class="sxs-lookup"><span data-stu-id="14188-139">**App-consistent snapshot frequency**: By default Site Recovery takes an app-consistent snapshot every 4 hours.</span></span> <span data-ttu-id="14188-140">Można skonfigurować dowolną wartość z zakresu od 1 do 12 godzin.</span><span class="sxs-lookup"><span data-stu-id="14188-140">You can configure any value between 1 and 12 hours.</span></span> <span data-ttu-id="14188-141">Dane są replikowane w sposób ciągły:</span><span class="sxs-lookup"><span data-stu-id="14188-141">Data is replicated continuously:</span></span>
    - <span data-ttu-id="14188-142">Punktów odzyskiwania zapewniających spójność awarii zachowania spójności danych zapisu kolejności podczas tworzenia.</span><span class="sxs-lookup"><span data-stu-id="14188-142">Crash-consistent recovery points maintain consistent data write-order when created.</span></span> <span data-ttu-id="14188-143">Ten rodzaj punktu odzyskiwania jest zwykle wystarczające, jeśli aplikacja jest zaprojektowana toorecover z awarii bez niespójności danych</span><span class="sxs-lookup"><span data-stu-id="14188-143">This type of recovery point is usually sufficient if your app is designed toorecover from a crash without data inconsistencies</span></span>
    - <span data-ttu-id="14188-144">Punktów odzyskiwania zapewniających spójność awarii są generowane co kilka minut.</span><span class="sxs-lookup"><span data-stu-id="14188-144">Crash-consistent recovery points are generated every few minutes.</span></span> <span data-ttu-id="14188-145">Przy użyciu tych toofail punkty odzyskiwania przez i odzyskiwanie maszyn wirtualnych zapewnia odzyskiwania punktu cel (RPO) w kolejności hello minut.</span><span class="sxs-lookup"><span data-stu-id="14188-145">Using these recovery points toofail over and recover your VMs provides a Recovery Point Objective (RPO) in hello order of minutes.</span></span>
    - <span data-ttu-id="14188-146">Punktów odzyskiwania zapewniających spójność aplikacji (w spójności kolejności toowrite dodanie) zapewnić ukończenie wszystkich operacji uruchomionych aplikacji i opróżnienia buforów toodisk (przełączany w stan spoczynku aplikacji).</span><span class="sxs-lookup"><span data-stu-id="14188-146">App-consistent recovery points (in addition toowrite-order consistency) ensure that running apps complete all operations and flush buffers toodisk (application quiescing).</span></span> <span data-ttu-id="14188-147">Firma Microsoft zaleca korzystanie z tych punktów odzyskiwania dla bazy danych aplikacji, takich jak SQL Server, Oracle i Exchange.</span><span class="sxs-lookup"><span data-stu-id="14188-147">We recommend you use these recovery points for database apps such as SQL Server, Oracle, and Exchange.</span></span>
        
    ![Konfigurowanie ustawień](./media/azure-to-azure-walkthrough-enable-replication/settings.png)


### <a name="modify-settings"></a><span data-ttu-id="14188-149">Modyfikowanie ustawień</span><span class="sxs-lookup"><span data-stu-id="14188-149">Modify settings</span></span>

<span data-ttu-id="14188-150">Jeśli chcesz, aby ustawienia zasad replikacji i docelowe toomodify, hello następujące:</span><span class="sxs-lookup"><span data-stu-id="14188-150">If you want toomodify target and replication policy settings, do hello following:</span></span>

1. <span data-ttu-id="14188-151">tooview lub zmodyfikować ustawienia obiektu docelowego, kliknij przycisk **ustawienia**.</span><span class="sxs-lookup"><span data-stu-id="14188-151">tooview or modify target settings, click **Settings**.</span></span>
2. <span data-ttu-id="14188-152">toooverride hello domyślne ustawień obiektu docelowego, kliknij przycisk **Dostosuj**.</span><span class="sxs-lookup"><span data-stu-id="14188-152">toooverride hello default target settings, click **Customize**.</span></span> <span data-ttu-id="14188-153">Można określić docelowa grupa zasobów, sieć wirtualną, zestawu dostępności i docelowe konto magazynu.</span><span class="sxs-lookup"><span data-stu-id="14188-153">You can specify a target resource group, virtual network, availability set, and target storage account.</span></span> <span data-ttu-id="14188-154">Zestawy dostępności można dodawać tylko, jeśli maszyny wirtualne są częścią zestawu w regionie źródła hello.</span><span class="sxs-lookup"><span data-stu-id="14188-154">You can only add availability sets if VMs are part of a set in hello source region.</span></span>

    ![Konfigurowanie ustawień](./media/azure-to-azure-walkthrough-enable-replication/customize-target.png)

3. <span data-ttu-id="14188-156">ustawienia replikacji toooverride punktów odzyskiwania oraz migawki spójne z aplikacjami, kliknij przycisk **Dostosuj** dalej zbyt**zasad replikacji**.</span><span class="sxs-lookup"><span data-stu-id="14188-156">toooverride replication settings for recovery points and app-consistent snapshots, click **Customize** next too**Replication Policy**.</span></span>
 
    ![Konfigurowanie ustawień](./media/azure-to-azure-walkthrough-enable-replication/customize-policy.png)

4. <span data-ttu-id="14188-158">toostart inicjowania obsługi administracyjnej hello zasobów docelowych, kliknij przycisk **Utwórz zasoby docelowe**.</span><span class="sxs-lookup"><span data-stu-id="14188-158">toostart provisioning hello target resources, click **Create target resources**.</span></span> <span data-ttu-id="14188-159">Inicjowanie obsługi administracyjnej ma minuty.</span><span class="sxs-lookup"><span data-stu-id="14188-159">Provisioning takes a minute or so.</span></span> <span data-ttu-id="14188-160">Nie zamykaj bloku hello podczas inicjowania obsługi lub toostart będziesz mieć za pośrednictwem.</span><span class="sxs-lookup"><span data-stu-id="14188-160">Don't close hello blade during provisioning, or you'll have toostart over.</span></span>




## <a name="enable-replication"></a><span data-ttu-id="14188-161">Włączanie replikacji</span><span class="sxs-lookup"><span data-stu-id="14188-161">Enable replication</span></span>

1. <span data-ttu-id="14188-162">W **ustawienia**, kliknij przycisk **włączyć replikację**.</span><span class="sxs-lookup"><span data-stu-id="14188-162">In **Settings**, click **Enable replication**.</span></span> <span data-ttu-id="14188-163">Dzięki temu replikacji początkowej hello wybranych maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="14188-163">This enables initial replication of hello VMs you selected.</span></span> <span data-ttu-id="14188-164">Stan replikacji początkowej może potrwać kilka toorefresh czas.</span><span class="sxs-lookup"><span data-stu-id="14188-164">Initial replication status might take some time toorefresh.</span></span> <span data-ttu-id="14188-165">Kliknij przycisk **Odśwież** tooget hello najnowszy stan.</span><span class="sxs-lookup"><span data-stu-id="14188-165">Click **Refresh** tooget hello latest status.</span></span>

2. <span data-ttu-id="14188-166">Możesz śledzić postępy hello **Włącz ochronę** zadania w **ustawienia** > **zadania** > **zadania usługi Site Recovery**.</span><span class="sxs-lookup"><span data-stu-id="14188-166">You can track progress of hello **Enable protection** job in **Settings** > **Jobs** > **Site Recovery Jobs**.</span></span>

3. <span data-ttu-id="14188-167">W **ustawienia** > **elementy replikowane**, można wyświetlić stan hello maszyn wirtualnych i hello postęp replikacji początkowej.</span><span class="sxs-lookup"><span data-stu-id="14188-167">In **Settings** > **Replicated Items**, you can view hello status of VMs and hello initial replication progress.</span></span> <span data-ttu-id="14188-168">Kliknij przycisk hello toodrill maszyny Wirtualnej w dół do jego ustawień.</span><span class="sxs-lookup"><span data-stu-id="14188-168">Click hello VM toodrill down into its settings.</span></span>



## <a name="next-steps"></a><span data-ttu-id="14188-169">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="14188-169">Next steps</span></span>

<span data-ttu-id="14188-170">Przejdź do zbyt[krok 6: testować tryb failover](azure-to-azure-walkthrough-test-failover.md)</span><span class="sxs-lookup"><span data-stu-id="14188-170">Go too[Step 6: Run a test failover](azure-to-azure-walkthrough-test-failover.md)</span></span>
