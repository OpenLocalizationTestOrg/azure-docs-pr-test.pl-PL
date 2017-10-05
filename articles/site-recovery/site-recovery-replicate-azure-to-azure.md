---
title: Replikowanie aplikacji (Azure do platformy Azure) | Dokumentacja firmy Microsoft
description: "W tym artykule opisano sposób skonfigurowania replikacji maszyn wirtualnych działających w jednym regionie Azure do innego regionu na platformie Azure."
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
ms.openlocfilehash: f9f97cf840b722c8cfee169dd1640e0682f287ff
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="replicate-azure-virtual-machines-to-another-azure-region"></a><span data-ttu-id="a2c72-103">Replikowanie maszyn wirtualnych platformy Azure do innego regionu systemu Azure</span><span class="sxs-lookup"><span data-stu-id="a2c72-103">Replicate Azure virtual machines to another Azure region</span></span>



>[!NOTE]
>
> <span data-ttu-id="a2c72-104">Replikacja lokacji odzyskiwania maszyn wirtualnych platformy Azure jest obecnie w przeglądzie.</span><span class="sxs-lookup"><span data-stu-id="a2c72-104">Site Recovery replication for Azure virtual machines is currently in preview.</span></span>

<span data-ttu-id="a2c72-105">W tym artykule opisano sposób skonfigurowania replikacji maszyn wirtualnych działających w jednym regionie Azure do innego regionu systemu Azure.</span><span class="sxs-lookup"><span data-stu-id="a2c72-105">This article describes how to set up replication of virtual machines running in one Azure region to another Azure region.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a2c72-106">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="a2c72-106">Prerequisites</span></span>

* <span data-ttu-id="a2c72-107">Artykule przyjęto założenie, że już wiedzę na temat odzyskiwania lokacji i magazynu usług odzyskiwania.</span><span class="sxs-lookup"><span data-stu-id="a2c72-107">The article assumes that you already know about Site Recovery and Recovery Services Vault.</span></span> <span data-ttu-id="a2c72-108">Musisz mieć sprzed "Magazyn usług odzyskiwania", utworzony.</span><span class="sxs-lookup"><span data-stu-id="a2c72-108">You need to have a 'Recovery services vault' pre created.</span></span>

    >[!NOTE]
    >
    > <span data-ttu-id="a2c72-109">Zalecane jest tworzenie magazynu usług odzyskiwania w miejscu, gdzie ma maszyny wirtualne do replikacji.</span><span class="sxs-lookup"><span data-stu-id="a2c72-109">It is recommended that you create the 'Recovery services vault' in the location where you want your VMs to replicate.</span></span> <span data-ttu-id="a2c72-110">Na przykład jeśli lokalizacja docelowej środkowe stany USA, należy utworzyć magazynu w środkowe stany USA.</span><span class="sxs-lookup"><span data-stu-id="a2c72-110">For example, if your target location is 'Central US', create vault in 'Central US'.</span></span>

* <span data-ttu-id="a2c72-111">Upewnij się, jeśli używane są zasady grupy zabezpieczeń sieci (NSG) lub serwer proxy zapory do kontrolowania dostępu do wychodzące połączenie z Internetem na maszynach wirtualnych Azure, tym możesz dozwolonych wymagane adresy URL lub adresów IP.</span><span class="sxs-lookup"><span data-stu-id="a2c72-111">If you are using Network Security Groups (NSG) rules or firewall proxy to control access to outbound internet connectivity on the Azure VMs, ensure that you whitelist the required URLs or IPs.</span></span> <span data-ttu-id="a2c72-112">Zapoznaj się [sieci wytycznych](./site-recovery-azure-to-azure-networking-guidance.md) więcej szczegółów.</span><span class="sxs-lookup"><span data-stu-id="a2c72-112">Refer to [Networking guidance document](./site-recovery-azure-to-azure-networking-guidance.md) for more details.</span></span>

* <span data-ttu-id="a2c72-113">Jeśli masz usługi ExpressRoute lub połączeń VPN między lokalnymi a lokalizacją źródłową na platformie Azure, wykonaj [zagadnienia dotyczące odzyskiwania lokacji dla platformy Azure lokalnej usługi expressroute / konfiguracji sieci VPN](site-recovery-azure-to-azure-networking-guidance.md#guidelines-for-existing-azure-to-on-premises-expressroutevpn-configuration) dokumentu.</span><span class="sxs-lookup"><span data-stu-id="a2c72-113">If you have an ExpressRoute or a VPN connection between on-premises and the source location in Azure, follow [Site Recovery Considerations for Azure to on-premises ExpressRoute / VPN configuration](site-recovery-azure-to-azure-networking-guidance.md#guidelines-for-existing-azure-to-on-premises-expressroutevpn-configuration) document.</span></span>

* <span data-ttu-id="a2c72-114">Twoje konto użytkownika usługi Azure musi mieć niektórych [uprawnienia](site-recovery-role-based-linked-access-control.md#permissions-required-to-enable-replication-for-new-virtual-machines) Aby włączyć replikację maszyny wirtualnej platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="a2c72-114">Your Azure user account needs to have certain [permissions](site-recovery-role-based-linked-access-control.md#permissions-required-to-enable-replication-for-new-virtual-machines) to enable replication of an Azure virtual machine.</span></span>

* <span data-ttu-id="a2c72-115">Do tworzenia maszyn wirtualnych w lokalizacji docelowej, który ma być używany jako region odzyskiwania po awarii powinna być włączona subskrypcji platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="a2c72-115">Your Azure subscription should be enabled to create VMs in the target location you want to use as DR region.</span></span> <span data-ttu-id="a2c72-116">Można skontaktuj się z pomocą techniczną, aby włączyć wymagane przydziału.</span><span class="sxs-lookup"><span data-stu-id="a2c72-116">You can contact support to enable the required quota.</span></span>

## <a name="enable-replication-from-azure-site-recovery-vault"></a><span data-ttu-id="a2c72-117">Włącz replikację z magazynu usługi Azure Site Recovery</span><span class="sxs-lookup"><span data-stu-id="a2c72-117">Enable replication from Azure Site Recovery vault</span></span>
<span data-ttu-id="a2c72-118">Na tej ilustracji, firma Microsoft będzie replikowanie maszyn wirtualnych uruchomionych w Azja Wschodnia lokalizacji platformy Azure w lokalizacji "Azja południowo-wschodnia".</span><span class="sxs-lookup"><span data-stu-id="a2c72-118">For this illustration, we will replicate VMs running  in the ‘East Asia’ Azure location to the ‘South East Asia’ location.</span></span> <span data-ttu-id="a2c72-119">Dostępne są następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="a2c72-119">The steps are as follows:</span></span>

 <span data-ttu-id="a2c72-120">Kliknij przycisk **+ Replikuj** w magazynie, aby włączyć replikację dla maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="a2c72-120">Click **+Replicate** in the vault to enable replication for the virtual machines.</span></span>

1. <span data-ttu-id="a2c72-121">**Źródło:** odnosi się do punktu pochodzenia maszyn, w tym przypadku jest **Azure**.</span><span class="sxs-lookup"><span data-stu-id="a2c72-121">**Source:** It refers to the point of origin of the machines which in this case is **Azure**.</span></span>

2. <span data-ttu-id="a2c72-122">**Lokalizacja źródłowa:** jest region platformy Azure, z której mają być chronione maszyny wirtualne.</span><span class="sxs-lookup"><span data-stu-id="a2c72-122">**Source location:** It is the Azure region from where you want to protect your virtual machines.</span></span> <span data-ttu-id="a2c72-123">Na tej ilustracji lokalizacja źródłowa będzie "Azja Wschodnia"</span><span class="sxs-lookup"><span data-stu-id="a2c72-123">For this illustration, the source location will be 'East Asia'</span></span>

3. <span data-ttu-id="a2c72-124">**Model wdrażania:** odnosi się do modelu wdrożenia usługi Azure maszyna źródłowa.</span><span class="sxs-lookup"><span data-stu-id="a2c72-124">**Deployment model:** It refers to the Azure deployment model of the source machines.</span></span> <span data-ttu-id="a2c72-125">Można wybrać obu classic lub Menedżera zasobów i komputery należące do określonego modelu zostaną wyświetlone w celu ochrony w następnym kroku.</span><span class="sxs-lookup"><span data-stu-id="a2c72-125">You can select either classic or resource manager and machines belonging to the specific model will be listed for protection in the next step.</span></span>

      >[!NOTE]
      >
      > <span data-ttu-id="a2c72-126">Można tylko replikowanie klasyczne maszyny wirtualnej i odzyskać ją jako maszynę wirtualną w klasycznym.</span><span class="sxs-lookup"><span data-stu-id="a2c72-126">You can only replicate a classic virtual machine and recover it as a classic virtual machine.</span></span> <span data-ttu-id="a2c72-127">Nie można go odzyskać jako maszynę wirtualną Menedżera zasobów.</span><span class="sxs-lookup"><span data-stu-id="a2c72-127">You cannot recover it as a Resource Manager virtual machine.</span></span>

4. <span data-ttu-id="a2c72-128">**Grupa zasobów:** jest grupa zasobów, do której należy źródło maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="a2c72-128">**Resource Group:** It’s the resource group to which your source virtual machines belong.</span></span> <span data-ttu-id="a2c72-129">Zostaną wyświetlone wszystkie maszyny wirtualne w wybranej grupy zasobów do ochrony w następnym kroku.</span><span class="sxs-lookup"><span data-stu-id="a2c72-129">All the VMs under the selected resource group will be listed for protection in the next step.</span></span>

    ![Włączanie replikacji](./media/site-recovery-replicate-azure-to-azure/enabledrwizard1.png)

<span data-ttu-id="a2c72-131">W **maszyny wirtualnej > Wybierz maszyny wirtualne**, kliknij i zaznacz każdej maszynie, którą chcesz replikować.</span><span class="sxs-lookup"><span data-stu-id="a2c72-131">In **Virtual Machines > Select virtual machines**, click and select each machine you want to replicate.</span></span> <span data-ttu-id="a2c72-132">Możesz wybrać tylko te maszyny, dla których można włączyć replikację.</span><span class="sxs-lookup"><span data-stu-id="a2c72-132">You can only select machines for which replication can be enabled.</span></span> <span data-ttu-id="a2c72-133">Następnie kliknij przycisk OK.</span><span class="sxs-lookup"><span data-stu-id="a2c72-133">Then click OK.</span></span>
    <span data-ttu-id="a2c72-134">![Włączanie replikacji](./media/site-recovery-replicate-azure-to-azure/virtualmachine_selection.png)</span><span class="sxs-lookup"><span data-stu-id="a2c72-134">![Enable replication](./media/site-recovery-replicate-azure-to-azure/virtualmachine_selection.png)</span></span>


<span data-ttu-id="a2c72-135">W sekcji Ustawienia można skonfigurować właściwości lokacji docelowej</span><span class="sxs-lookup"><span data-stu-id="a2c72-135">Under Settings section you can configure target site properties</span></span>

1. <span data-ttu-id="a2c72-136">**Lokalizacja docelowa:** jest to lokalizacja, w którym będą replikowane dane źródłowe maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="a2c72-136">**Target Location:**  This is the location where your source virtual machine data will be replicated.</span></span> <span data-ttu-id="a2c72-137">W zależności od lokalizacji wybranych maszyn Site Recovery zapewnia listę regionów odpowiedniego elementu docelowego.</span><span class="sxs-lookup"><span data-stu-id="a2c72-137">Depending upon your selected machines location, Site Recovery will provide you the list of suitable target regions.</span></span>

    > [!TIP]
    > <span data-ttu-id="a2c72-138">Zaleca się zachowanie lokalizacji docelowej takie same jak odzyskiwania usług magazynu.</span><span class="sxs-lookup"><span data-stu-id="a2c72-138">It is recommended to keep target location same as of your recovery services vault.</span></span>

2. <span data-ttu-id="a2c72-139">**Docelowa grupa zasobów:** jest grupa zasobów, aby wszystkie zreplikowanej maszyny wirtualne będą należeć. Domyślnie funkcja automatycznego odzyskiwania systemu utworzy nową grupę zasobów w regionie docelowych z nazwą składającą się z sufiksem "asr".</span><span class="sxs-lookup"><span data-stu-id="a2c72-139">**Target resource group :** It is the resource group to which all your replicated virtual machines will belong.By default ASR will create a new resource group in the target region with name having "asr" suffix.</span></span> <span data-ttu-id="a2c72-140">W przypadku grupy zasobów utworzonej przez ASR już istnieje, zostanie ono użyte ponownie. Można również dostosować go, jak pokazano w poniższej sekcji.</span><span class="sxs-lookup"><span data-stu-id="a2c72-140">In case resource group created by ASR already exist, it will be reused.You can also choose to customize it as shown in the section below.</span></span>    
3. <span data-ttu-id="a2c72-141">**Sieć wirtualna docelowa:** domyślnie ASR spowoduje utworzenie nowej sieci wirtualnej w regionie docelowej z nazwą składającą się z sufiksem "asr".</span><span class="sxs-lookup"><span data-stu-id="a2c72-141">**Target Virtual Network:** By default, ASR will create a new virtual network in the target region with name having "asr" suffix.</span></span> <span data-ttu-id="a2c72-142">To zostaną zmapowane do źródłowej sieci i będzie służyć do przyszłych ochrony.</span><span class="sxs-lookup"><span data-stu-id="a2c72-142">This will be mapped to your source network and will be used for any future protection.</span></span>

    > [!NOTE]
    > <span data-ttu-id="a2c72-143">[Sprawdź szczegóły sieci](site-recovery-network-mapping-azure-to-azure.md) Aby dowiedzieć się więcej o mapowania sieci.</span><span class="sxs-lookup"><span data-stu-id="a2c72-143">[Check networking details](site-recovery-network-mapping-azure-to-azure.md) to know more about network mapping.</span></span>

4. <span data-ttu-id="a2c72-144">**Docelowa kont magazynu:** domyślnie ASR utworzy nowe konto magazynu docelowego mimicking konfigurację magazynu maszyny Wirtualnej źródłowego.</span><span class="sxs-lookup"><span data-stu-id="a2c72-144">**Target Storage accounts:** By default, ASR will create the new target storage account mimicking your source VM storage configuration.</span></span> <span data-ttu-id="a2c72-145">W przypadku konta magazynu utworzone przez usługi ASR już istnieje, zostanie ono użyte ponownie.</span><span class="sxs-lookup"><span data-stu-id="a2c72-145">In case storage account created by ASR already exist, it will be reused.</span></span>

5. <span data-ttu-id="a2c72-146">**Buforowanie kont magazynu:** ASR wymaga konta dodatkowego magazynu o nazwie magazynu pamięci podręcznej w regionie źródła.</span><span class="sxs-lookup"><span data-stu-id="a2c72-146">**Cache Storage accounts:** ASR needs extra storage account called cache storage in the source region.</span></span> <span data-ttu-id="a2c72-147">Wszystkie zmiany, które są wykonywane na maszynach wirtualnych źródła są śledzone i wysyłane do konta magazynu pamięci podręcznej przed replikowanie tych do lokalizacji docelowej.</span><span class="sxs-lookup"><span data-stu-id="a2c72-147">All the changes happening on the source VMs are tracked and sent to cache storage account before replicating those to the target location.</span></span>

6. <span data-ttu-id="a2c72-148">**Zestaw dostępności:** domyślnie ASR utworzy nowy zestawem dostępności w region docelowy z nazwą składającą się z sufiksem "asr".</span><span class="sxs-lookup"><span data-stu-id="a2c72-148">**Availability set :** By default, ASR will create a new availability set in the target region with name having "asr" suffix.</span></span> <span data-ttu-id="a2c72-149">W przypadku, gdy zestaw dostępności utworzony przez ASR już istnieje, zostanie ono użyte ponownie.</span><span class="sxs-lookup"><span data-stu-id="a2c72-149">In case availability set created by ASR already exist, it will be reused.</span></span>

7.  <span data-ttu-id="a2c72-150">**Zasady replikacji:** definiuje ustawienia odzyskiwania punktu przechowywania historii i aplikacji migawki dotyczącej spójności częstotliwości.</span><span class="sxs-lookup"><span data-stu-id="a2c72-150">**Replication Policy:** It defines the settings for recovery point retention history and app consistent snapshot frequency.</span></span> <span data-ttu-id="a2c72-151">Domyślnie funkcja automatycznego odzyskiwania systemu utworzy nowe zasady replikacji z ustawieniami domyślnymi 24 godzin przechowywania punktu odzyskiwania i "60 minut częstotliwości migawki dotyczącej spójności aplikacji.</span><span class="sxs-lookup"><span data-stu-id="a2c72-151">By default, ASR will create a new replication policy with default settings of ‘24 hours’ for recovery point retention and ’60 minutes’ for app consistent snapshot frequency.</span></span>

    ![Włączanie replikacji](./media/site-recovery-replicate-azure-to-azure/enabledrwizard3.PNG)

## <a name="customize-target-resources"></a><span data-ttu-id="a2c72-153">Dostosowywanie zasobami obiektów docelowych</span><span class="sxs-lookup"><span data-stu-id="a2c72-153">Customize target resources</span></span>

<span data-ttu-id="a2c72-154">W przypadku, gdy chcesz zmienić ustawienia domyślne używane przez usługi ASR, możesz zmienić ustawienia, na podstawie Twoich potrzeb.</span><span class="sxs-lookup"><span data-stu-id="a2c72-154">In case you want to change the defaults used by ASR, you can change the settings based on your needs.</span></span>

1. <span data-ttu-id="a2c72-155">**Dostosowywanie:** kliknij go, aby zmienić ustawienia domyślne używane przez usługi ASR.</span><span class="sxs-lookup"><span data-stu-id="a2c72-155">**Customize:** Click it to change the defaults used by ASR.</span></span>

2. <span data-ttu-id="a2c72-156">**Docelowa grupa zasobów:** grupy zasobów można wybrać z listy grup zasobów istniejących w miejscu docelowym w ramach subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="a2c72-156">**Target resource group :**  You can select the resource group from the list of all the resource groups existing in the target location within the subscription.</span></span>

3. <span data-ttu-id="a2c72-157">**Sieć wirtualna docelowa:** można znaleźć na liście sieci wirtualnej w lokalizacji docelowej.</span><span class="sxs-lookup"><span data-stu-id="a2c72-157">**Target Virtual Network:** You can find the list of all the virtual network in the target location.</span></span>

4. <span data-ttu-id="a2c72-158">**Zestaw dostępności:** ustawienia zestawy dostępności można dodawać tylko do maszyn wirtualnych, które są częścią dostępności w regionie źródła.</span><span class="sxs-lookup"><span data-stu-id="a2c72-158">**Availability set :** You can only add availability sets settings to the virtual machines which are a part of availability in source region.</span></span>

5. <span data-ttu-id="a2c72-159">**Konta magazynu docelowego:**</span><span class="sxs-lookup"><span data-stu-id="a2c72-159">**Target Storage accounts:**</span></span>

<span data-ttu-id="a2c72-160">![Włącz replikację](./media/site-recovery-replicate-azure-to-azure/customize.PNG) kliknij **tworzenie zasobu docelowego** i włączyć replikację</span><span class="sxs-lookup"><span data-stu-id="a2c72-160">![Enable replication](./media/site-recovery-replicate-azure-to-azure/customize.PNG) Click on **Create target resource** and Enable Replication</span></span>


<span data-ttu-id="a2c72-161">Gdy są chronione maszyny wirtualne można sprawdzić stan kondycji maszyn wirtualnych w obszarze **zreplikowane elementy**</span><span class="sxs-lookup"><span data-stu-id="a2c72-161">Once virtual machines are protected you can check the status of VMs health under **Replicated items**</span></span>

>[!NOTE]
><span data-ttu-id="a2c72-162">Podczas replikacji początkowej można możliwości stan czas, aby odświeżyć, a nie widzisz postępu przez pewien czas.</span><span class="sxs-lookup"><span data-stu-id="a2c72-162">During the time of initial replication there could a possibility that status takes time to refresh and you don't see progress for some time.</span></span> <span data-ttu-id="a2c72-163">Kliknięcie przycisku Odśwież w górnej części bloku, aby pobrać najnowszy stan.</span><span class="sxs-lookup"><span data-stu-id="a2c72-163">You can click the Refresh button on the top of the blade to get the latest status.</span></span>
>

![Włączanie replikacji](./media/site-recovery-replicate-azure-to-azure/replicateditems.PNG)


## <a name="next-steps"></a><span data-ttu-id="a2c72-165">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="a2c72-165">Next steps</span></span>
- <span data-ttu-id="a2c72-166">[Dowiedz się więcej](site-recovery-test-failover-to-azure.md) uruchomiony test trybu failover.</span><span class="sxs-lookup"><span data-stu-id="a2c72-166">[Learn more](site-recovery-test-failover-to-azure.md) about running a test failover.</span></span>
- <span data-ttu-id="a2c72-167">[Dowiedz się więcej](site-recovery-failover.md) o różnych typach trybu failover i sposobu ich uruchamiania.</span><span class="sxs-lookup"><span data-stu-id="a2c72-167">[Learn more](site-recovery-failover.md) about different types of failovers, and how to run them.</span></span>
- <span data-ttu-id="a2c72-168">Dowiedz się więcej o [przy użyciu planów odzyskiwania](site-recovery-create-recovery-plans.md) zmniejszenie RTO.</span><span class="sxs-lookup"><span data-stu-id="a2c72-168">Learn more about [using recovery plans](site-recovery-create-recovery-plans.md) to reduce RTO.</span></span>
- <span data-ttu-id="a2c72-169">Dowiedz się więcej o [ponownej ochrony maszyn wirtualnych platformy Azure](site-recovery-how-to-reprotect.md) po pracy awaryjnej.</span><span class="sxs-lookup"><span data-stu-id="a2c72-169">Learn more about [reprotecting Azure  VMs](site-recovery-how-to-reprotect.md) after failover.</span></span>
