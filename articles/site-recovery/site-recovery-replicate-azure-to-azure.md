---
title: aplikacje aaaReplicate (Azure tooAzure) | Dokumentacja firmy Microsoft
description: "W tym artykule opisano, jak tooset replikacji wirtualnej maszyny działa w jednym regionie Azure zbyt innego regionu na platformie Azure."
services: site-recovery
documentationcenter: 
author: asgang
manager: rochakm
editor: 
ms.assetid: 
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 5/22/2017
ms.author: asgang
ms.openlocfilehash: fb190dac14419f892a1c6b45a3d991d8005e4bd0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="replicate-azure-virtual-machines-tooanother-azure-region"></a><span data-ttu-id="7f1b1-103">Replikowanie maszyn wirtualnych platformy Azure tooanother region platformy Azure</span><span class="sxs-lookup"><span data-stu-id="7f1b1-103">Replicate Azure virtual machines tooanother Azure region</span></span>



>[!NOTE]
>
> <span data-ttu-id="7f1b1-104">Replikacja lokacji odzyskiwania maszyn wirtualnych platformy Azure jest obecnie w przeglądzie.</span><span class="sxs-lookup"><span data-stu-id="7f1b1-104">Site Recovery replication for Azure virtual machines is currently in preview.</span></span>

<span data-ttu-id="7f1b1-105">W tym artykule opisano, jak tooset replikacji wirtualnej maszyny działa w jednym regionie Azure tooanother region platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="7f1b1-105">This article describes how tooset up replication of virtual machines running in one Azure region tooanother Azure region.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7f1b1-106">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="7f1b1-106">Prerequisites</span></span>

* <span data-ttu-id="7f1b1-107">Artykuł Hello przyjęto założenie, że już wiedzę na temat odzyskiwania lokacji i magazynu usług odzyskiwania.</span><span class="sxs-lookup"><span data-stu-id="7f1b1-107">hello article assumes that you already know about Site Recovery and Recovery Services Vault.</span></span> <span data-ttu-id="7f1b1-108">Należy toohave sprzed "Magazyn usług odzyskiwania", utworzony.</span><span class="sxs-lookup"><span data-stu-id="7f1b1-108">You need toohave a 'Recovery services vault' pre created.</span></span>

    >[!NOTE]
    >
    > <span data-ttu-id="7f1b1-109">Zalecane jest utworzenie hello "Magazyn usług odzyskiwania" w hello lokalizację tooreplicate sieci maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="7f1b1-109">It is recommended that you create hello 'Recovery services vault' in hello location where you want your VMs tooreplicate.</span></span> <span data-ttu-id="7f1b1-110">Na przykład jeśli lokalizacja docelowej środkowe stany USA, należy utworzyć magazynu w środkowe stany USA.</span><span class="sxs-lookup"><span data-stu-id="7f1b1-110">For example, if your target location is 'Central US', create vault in 'Central US'.</span></span>

* <span data-ttu-id="7f1b1-111">Jeśli używane są zasady grupy zabezpieczeń sieci (NSG) lub połączenie internetowe toooutbound dostępu zapory serwera proxy toocontrol na powitania maszynach wirtualnych platformy Azure, upewnij się, że ten użytkownik dozwolonych hello wymagane adresy URL lub adresów IP.</span><span class="sxs-lookup"><span data-stu-id="7f1b1-111">If you are using Network Security Groups (NSG) rules or firewall proxy toocontrol access toooutbound internet connectivity on hello Azure VMs, ensure that you whitelist hello required URLs or IPs.</span></span> <span data-ttu-id="7f1b1-112">Odwołuje się zbyt[sieci wytycznych](./site-recovery-azure-to-azure-networking-guidance.md) więcej szczegółów.</span><span class="sxs-lookup"><span data-stu-id="7f1b1-112">Refer too[Networking guidance document](./site-recovery-azure-to-azure-networking-guidance.md) for more details.</span></span>

* <span data-ttu-id="7f1b1-113">Jeśli masz usługi ExpressRoute lub połączenie sieci VPN między lokalnymi i hello źródła lokalizacji na platformie Azure, wykonaj [lokacji zagadnienia związane z lokalnym tooon Azure ExpressRoute / konfiguracji sieci VPN](site-recovery-azure-to-azure-networking-guidance.md#guidelines-for-existing-azure-to-on-premises-expressroutevpn-configuration) dokumentu.</span><span class="sxs-lookup"><span data-stu-id="7f1b1-113">If you have an ExpressRoute or a VPN connection between on-premises and hello source location in Azure, follow [Site Recovery Considerations for Azure tooon-premises ExpressRoute / VPN configuration](site-recovery-azure-to-azure-networking-guidance.md#guidelines-for-existing-azure-to-on-premises-expressroutevpn-configuration) document.</span></span>

* <span data-ttu-id="7f1b1-114">Twoje konto użytkownika systemu Azure wymaga toohave niektórych [uprawnienia](site-recovery-role-based-linked-access-control.md#permissions-required-to-enable-replication-for-new-virtual-machines) tooenable replikacji maszyny wirtualnej platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="7f1b1-114">Your Azure user account needs toohave certain [permissions](site-recovery-role-based-linked-access-control.md#permissions-required-to-enable-replication-for-new-virtual-machines) tooenable replication of an Azure virtual machine.</span></span>

* <span data-ttu-id="7f1b1-115">Subskrypcji platformy Azure powinna być włączona toocreate maszyn wirtualnych w miejscu docelowym hello ma toouse jako region odzyskiwania po awarii.</span><span class="sxs-lookup"><span data-stu-id="7f1b1-115">Your Azure subscription should be enabled toocreate VMs in hello target location you want toouse as DR region.</span></span> <span data-ttu-id="7f1b1-116">Możesz skontaktować się przydział wymagany hello tooenable pomocy technicznej.</span><span class="sxs-lookup"><span data-stu-id="7f1b1-116">You can contact support tooenable hello required quota.</span></span>

## <a name="enable-replication-from-azure-site-recovery-vault"></a><span data-ttu-id="7f1b1-117">Włącz replikację z magazynu usługi Azure Site Recovery</span><span class="sxs-lookup"><span data-stu-id="7f1b1-117">Enable replication from Azure Site Recovery vault</span></span>
<span data-ttu-id="7f1b1-118">Na tej ilustracji możemy będą replikowane maszyny wirtualne uruchomione w toohello lokalizacji platformy Azure "Azja Wschodnia" hello "Azja południowo-wschodnia" lokalizacji.</span><span class="sxs-lookup"><span data-stu-id="7f1b1-118">For this illustration, we will replicate VMs running  in hello ‘East Asia’ Azure location toohello ‘South East Asia’ location.</span></span> <span data-ttu-id="7f1b1-119">Witaj obejmuje następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="7f1b1-119">hello steps are as follows:</span></span>

 <span data-ttu-id="7f1b1-120">Kliknij przycisk **+ Replikuj** w hello magazynu tooenable replikacji hello maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="7f1b1-120">Click **+Replicate** in hello vault tooenable replication for hello virtual machines.</span></span>

1. <span data-ttu-id="7f1b1-121">**Źródło:** odnosi się toohello punkt początkowy maszyn hello, w tym przypadku jest **Azure**.</span><span class="sxs-lookup"><span data-stu-id="7f1b1-121">**Source:** It refers toohello point of origin of hello machines which in this case is **Azure**.</span></span>

2. <span data-ttu-id="7f1b1-122">**Lokalizacja źródłowa:** jest hello region platformy Azure, z którym chcesz tooprotect maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="7f1b1-122">**Source location:** It is hello Azure region from where you want tooprotect your virtual machines.</span></span> <span data-ttu-id="7f1b1-123">Na tej ilustracji lokalizacji źródłowej hello będzie "Azja Wschodnia"</span><span class="sxs-lookup"><span data-stu-id="7f1b1-123">For this illustration, hello source location will be 'East Asia'</span></span>

3. <span data-ttu-id="7f1b1-124">**Model wdrażania:** odnosi się model wdrożenia usługi Azure toohello hello maszyny źródłowej.</span><span class="sxs-lookup"><span data-stu-id="7f1b1-124">**Deployment model:** It refers toohello Azure deployment model of hello source machines.</span></span> <span data-ttu-id="7f1b1-125">Można wybrać obu classic lub Menedżera zasobów i komputery należące do określonego modelu toohello zostaną wyświetlone w celu ochrony w hello następnego kroku.</span><span class="sxs-lookup"><span data-stu-id="7f1b1-125">You can select either classic or resource manager and machines belonging toohello specific model will be listed for protection in hello next step.</span></span>

      >[!NOTE]
      >
      > <span data-ttu-id="7f1b1-126">Można tylko replikowanie klasyczne maszyny wirtualnej i odzyskać ją jako maszynę wirtualną w klasycznym.</span><span class="sxs-lookup"><span data-stu-id="7f1b1-126">You can only replicate a classic virtual machine and recover it as a classic virtual machine.</span></span> <span data-ttu-id="7f1b1-127">Nie można go odzyskać jako maszynę wirtualną Menedżera zasobów.</span><span class="sxs-lookup"><span data-stu-id="7f1b1-127">You cannot recover it as a Resource Manager virtual machine.</span></span>

4. <span data-ttu-id="7f1b1-128">**Grupa zasobów:** tego toowhich grupy zasobów hello należą źródła maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="7f1b1-128">**Resource Group:** It’s hello resource group toowhich your source virtual machines belong.</span></span> <span data-ttu-id="7f1b1-129">W celu ochrony w następnym krokiem hello wyświetlą się hello wszystkich maszyn wirtualnych w obszarze hello wybranej grupy zasobów.</span><span class="sxs-lookup"><span data-stu-id="7f1b1-129">All hello VMs under hello selected resource group will be listed for protection in hello next step.</span></span>

    ![Włączanie replikacji](./media/site-recovery-replicate-azure-to-azure/enabledrwizard1.png)

<span data-ttu-id="7f1b1-131">W **maszyny wirtualnej > Wybierz maszyny wirtualne**, kliknij i zaznacz każdy komputer ma tooreplicate.</span><span class="sxs-lookup"><span data-stu-id="7f1b1-131">In **Virtual Machines > Select virtual machines**, click and select each machine you want tooreplicate.</span></span> <span data-ttu-id="7f1b1-132">Możesz wybrać tylko te maszyny, dla których można włączyć replikację.</span><span class="sxs-lookup"><span data-stu-id="7f1b1-132">You can only select machines for which replication can be enabled.</span></span> <span data-ttu-id="7f1b1-133">Następnie kliknij przycisk OK.</span><span class="sxs-lookup"><span data-stu-id="7f1b1-133">Then click OK.</span></span>
    <span data-ttu-id="7f1b1-134">![Włączanie replikacji](./media/site-recovery-replicate-azure-to-azure/virtualmachine_selection.png)</span><span class="sxs-lookup"><span data-stu-id="7f1b1-134">![Enable replication](./media/site-recovery-replicate-azure-to-azure/virtualmachine_selection.png)</span></span>


<span data-ttu-id="7f1b1-135">W sekcji Ustawienia można skonfigurować właściwości lokacji docelowej</span><span class="sxs-lookup"><span data-stu-id="7f1b1-135">Under Settings section you can configure target site properties</span></span>

1. <span data-ttu-id="7f1b1-136">**Lokalizacja docelowa:** hello lokalizacja, gdzie będą replikowane dane źródłowe maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="7f1b1-136">**Target Location:**  This is hello location where your source virtual machine data will be replicated.</span></span> <span data-ttu-id="7f1b1-137">W zależności od lokalizacji wybranych maszyn Site Recovery umożliwi hello listę regionów odpowiedniego elementu docelowego.</span><span class="sxs-lookup"><span data-stu-id="7f1b1-137">Depending upon your selected machines location, Site Recovery will provide you hello list of suitable target regions.</span></span>

    > [!TIP]
    > <span data-ttu-id="7f1b1-138">Zalecane jest lokalizacja docelowa tookeep takie same jak odzyskiwania usług magazynu.</span><span class="sxs-lookup"><span data-stu-id="7f1b1-138">It is recommended tookeep target location same as of your recovery services vault.</span></span>

2. <span data-ttu-id="7f1b1-139">**Docelowa grupa zasobów:** jest toowhich grupy zasobów hello wszystkie zreplikowanej maszyny wirtualne będą należeć. Domyślnie funkcja automatycznego odzyskiwania systemu utworzy nową grupę zasobów w regionie docelowym hello z nazwą składającą się z sufiksem "asr".</span><span class="sxs-lookup"><span data-stu-id="7f1b1-139">**Target resource group :** It is hello resource group toowhich all your replicated virtual machines will belong.By default ASR will create a new resource group in hello target region with name having "asr" suffix.</span></span> <span data-ttu-id="7f1b1-140">W przypadku grupy zasobów utworzonej przez ASR już istnieje, zostanie ono użyte ponownie. Możesz również toocustomize go jak pokazano w poniższej sekcji hello.</span><span class="sxs-lookup"><span data-stu-id="7f1b1-140">In case resource group created by ASR already exist, it will be reused.You can also choose toocustomize it as shown in hello section below.</span></span>    
3. <span data-ttu-id="7f1b1-141">**Sieć wirtualna docelowa:** domyślnie ASR spowoduje utworzenie nowej sieci wirtualnej w region docelowy hello z nazwą składającą się z sufiksem "asr".</span><span class="sxs-lookup"><span data-stu-id="7f1b1-141">**Target Virtual Network:** By default, ASR will create a new virtual network in hello target region with name having "asr" suffix.</span></span> <span data-ttu-id="7f1b1-142">To zostanie zamapowane tooyour źródłowej sieci i będzie służyć do przyszłych ochrony.</span><span class="sxs-lookup"><span data-stu-id="7f1b1-142">This will be mapped tooyour source network and will be used for any future protection.</span></span>

    > [!NOTE]
    > <span data-ttu-id="7f1b1-143">[Sprawdź szczegóły sieci](site-recovery-network-mapping-azure-to-azure.md) tooknow więcej informacji na temat mapowania sieci.</span><span class="sxs-lookup"><span data-stu-id="7f1b1-143">[Check networking details](site-recovery-network-mapping-azure-to-azure.md) tooknow more about network mapping.</span></span>

4. <span data-ttu-id="7f1b1-144">**Docelowa kont magazynu:** domyślnie ASR utworzy hello nowe docelowe konto magazynu mimicking konfigurację magazynu maszyny Wirtualnej źródłowego.</span><span class="sxs-lookup"><span data-stu-id="7f1b1-144">**Target Storage accounts:** By default, ASR will create hello new target storage account mimicking your source VM storage configuration.</span></span> <span data-ttu-id="7f1b1-145">W przypadku konta magazynu utworzone przez usługi ASR już istnieje, zostanie ono użyte ponownie.</span><span class="sxs-lookup"><span data-stu-id="7f1b1-145">In case storage account created by ASR already exist, it will be reused.</span></span>

5. <span data-ttu-id="7f1b1-146">**Buforowanie kont magazynu:** ASR wymaga konta dodatkowego magazynu o nazwie magazynu pamięci podręcznej w regionie źródła hello.</span><span class="sxs-lookup"><span data-stu-id="7f1b1-146">**Cache Storage accounts:** ASR needs extra storage account called cache storage in hello source region.</span></span> <span data-ttu-id="7f1b1-147">Witaj wszystkie zmiany wykonywane na powitania źródłowe maszyny wirtualne są śledzone i przed replikowanie tych lokalizacji docelowej toohello wysyłane toocache konta magazynu.</span><span class="sxs-lookup"><span data-stu-id="7f1b1-147">All hello changes happening on hello source VMs are tracked and sent toocache storage account before replicating those toohello target location.</span></span>

6. <span data-ttu-id="7f1b1-148">**Zestaw dostępności:** domyślnie ASR utworzy nowy zestawem dostępności w region docelowy hello z nazwą składającą się z sufiksem "asr".</span><span class="sxs-lookup"><span data-stu-id="7f1b1-148">**Availability set :** By default, ASR will create a new availability set in hello target region with name having "asr" suffix.</span></span> <span data-ttu-id="7f1b1-149">W przypadku, gdy zestaw dostępności utworzony przez ASR już istnieje, zostanie ono użyte ponownie.</span><span class="sxs-lookup"><span data-stu-id="7f1b1-149">In case availability set created by ASR already exist, it will be reused.</span></span>

7.  <span data-ttu-id="7f1b1-150">**Zasady replikacji:** definiuje ustawienia hello częstotliwości odzyskiwania punktu przechowywania historii i aplikacji migawki dotyczącej spójności.</span><span class="sxs-lookup"><span data-stu-id="7f1b1-150">**Replication Policy:** It defines hello settings for recovery point retention history and app consistent snapshot frequency.</span></span> <span data-ttu-id="7f1b1-151">Domyślnie funkcja automatycznego odzyskiwania systemu utworzy nowe zasady replikacji z ustawieniami domyślnymi 24 godzin przechowywania punktu odzyskiwania i "60 minut częstotliwości migawki dotyczącej spójności aplikacji.</span><span class="sxs-lookup"><span data-stu-id="7f1b1-151">By default, ASR will create a new replication policy with default settings of ‘24 hours’ for recovery point retention and ’60 minutes’ for app consistent snapshot frequency.</span></span>

    ![Włączanie replikacji](./media/site-recovery-replicate-azure-to-azure/enabledrwizard3.PNG)

## <a name="customize-target-resources"></a><span data-ttu-id="7f1b1-153">Dostosowywanie zasobami obiektów docelowych</span><span class="sxs-lookup"><span data-stu-id="7f1b1-153">Customize target resources</span></span>

<span data-ttu-id="7f1b1-154">W przypadku, gdy chcesz toochange hello domyślne używane przez usługi ASR, możesz zmienić ustawienia hello na podstawie Twoich potrzeb.</span><span class="sxs-lookup"><span data-stu-id="7f1b1-154">In case you want toochange hello defaults used by ASR, you can change hello settings based on your needs.</span></span>

1. <span data-ttu-id="7f1b1-155">**Dostosowywanie:** kliknij go toochange hello wartości domyślne używane przez usługi ASR.</span><span class="sxs-lookup"><span data-stu-id="7f1b1-155">**Customize:** Click it toochange hello defaults used by ASR.</span></span>

2. <span data-ttu-id="7f1b1-156">**Docelowa grupa zasobów:** hello grupy zasobów można wybrać z listy hello wszystkich grup zasobów hello istniejące w lokalizacji docelowej hello w ramach subskrypcji hello.</span><span class="sxs-lookup"><span data-stu-id="7f1b1-156">**Target resource group :**  You can select hello resource group from hello list of all hello resource groups existing in hello target location within hello subscription.</span></span>

3. <span data-ttu-id="7f1b1-157">**Sieć wirtualna docelowa:** hello listę wszystkich hello sieci wirtualnej można znaleźć w miejscu docelowym hello.</span><span class="sxs-lookup"><span data-stu-id="7f1b1-157">**Target Virtual Network:** You can find hello list of all hello virtual network in hello target location.</span></span>

4. <span data-ttu-id="7f1b1-158">**Zestaw dostępności:** można dodawać tylko dostępność zestawów ustawień toohello maszyn wirtualnych, które są częścią dostępności w regionie źródła.</span><span class="sxs-lookup"><span data-stu-id="7f1b1-158">**Availability set :** You can only add availability sets settings toohello virtual machines which are a part of availability in source region.</span></span>

5. <span data-ttu-id="7f1b1-159">**Konta magazynu docelowego:**</span><span class="sxs-lookup"><span data-stu-id="7f1b1-159">**Target Storage accounts:**</span></span>

<span data-ttu-id="7f1b1-160">![Włącz replikację](./media/site-recovery-replicate-azure-to-azure/customize.PNG) kliknij **tworzenie zasobu docelowego** i włączyć replikację</span><span class="sxs-lookup"><span data-stu-id="7f1b1-160">![Enable replication](./media/site-recovery-replicate-azure-to-azure/customize.PNG) Click on **Create target resource** and Enable Replication</span></span>


<span data-ttu-id="7f1b1-161">Gdy są chronione maszyny wirtualne można sprawdzić hello stan kondycji maszyn wirtualnych w obszarze **zreplikowane elementy**</span><span class="sxs-lookup"><span data-stu-id="7f1b1-161">Once virtual machines are protected you can check hello status of VMs health under **Replicated items**</span></span>

>[!NOTE]
><span data-ttu-id="7f1b1-162">Podczas hello replikacji początkowej można możliwość, że stan przyjmuje toorefresh czasu i nie widzisz postępu przez pewien czas.</span><span class="sxs-lookup"><span data-stu-id="7f1b1-162">During hello time of initial replication there could a possibility that status takes time toorefresh and you don't see progress for some time.</span></span> <span data-ttu-id="7f1b1-163">Możesz kliknąć przycisk Odśwież hello na początku hello hello bloku tooget hello najnowszy stan.</span><span class="sxs-lookup"><span data-stu-id="7f1b1-163">You can click hello Refresh button on hello top of hello blade tooget hello latest status.</span></span>
>

![Włączanie replikacji](./media/site-recovery-replicate-azure-to-azure/replicateditems.PNG)


## <a name="next-steps"></a><span data-ttu-id="7f1b1-165">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="7f1b1-165">Next steps</span></span>
- <span data-ttu-id="7f1b1-166">[Dowiedz się więcej](site-recovery-test-failover-to-azure.md) uruchomiony test trybu failover.</span><span class="sxs-lookup"><span data-stu-id="7f1b1-166">[Learn more](site-recovery-test-failover-to-azure.md) about running a test failover.</span></span>
- <span data-ttu-id="7f1b1-167">[Dowiedz się więcej](site-recovery-failover.md) o różnych typach trybu failover i w jaki sposób toorun je.</span><span class="sxs-lookup"><span data-stu-id="7f1b1-167">[Learn more](site-recovery-failover.md) about different types of failovers, and how toorun them.</span></span>
- <span data-ttu-id="7f1b1-168">Dowiedz się więcej o [przy użyciu planów odzyskiwania](site-recovery-create-recovery-plans.md) tooreduce RTO.</span><span class="sxs-lookup"><span data-stu-id="7f1b1-168">Learn more about [using recovery plans](site-recovery-create-recovery-plans.md) tooreduce RTO.</span></span>
- <span data-ttu-id="7f1b1-169">Dowiedz się więcej o [ponownej ochrony maszyn wirtualnych platformy Azure](site-recovery-how-to-reprotect.md) po pracy awaryjnej.</span><span class="sxs-lookup"><span data-stu-id="7f1b1-169">Learn more about [reprotecting Azure  VMs](site-recovery-how-to-reprotect.md) after failover.</span></span>
