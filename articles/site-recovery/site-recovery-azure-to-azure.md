---
title: "Replikowanie maszyn wirtualnych platformy Azure między regiony platformy Azure na potrzeby odzyskiwania po awarii: Azure tooAzure | Dokumentacja firmy Microsoft"
description: "Zawiera podsumowanie kroków hello należy maszynach wirtualnych platformy Azure tooreplicate między regiony platformy Azure (Azure-Azure) z usługą Azure Site Recovery hello na potrzeby odzyskiwania po awarii."
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmon
editor: 
ms.assetid: dab98aa5-9c41-4475-b7dc-2e07ab1cfd18
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/10/2017
ms.author: raynew
ms.openlocfilehash: c4c425af260a9bcc3dd4dcc13da26109e20f03bb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="replicate-azure-vms-between-regions-with-azure-site-recovery"></a><span data-ttu-id="65e93-103">Replikowanie maszyn wirtualnych Azure między regionami z usługą Azure Site Recovery</span><span class="sxs-lookup"><span data-stu-id="65e93-103">Replicate Azure VMs between regions with Azure Site Recovery</span></span>

>[!NOTE]
>
> <span data-ttu-id="65e93-104">Azure Site Recovery replikacji maszyn wirtualnych platformy Azure (VM) jest obecnie w przeglądzie.</span><span class="sxs-lookup"><span data-stu-id="65e93-104">Azure Site Recovery replication for Azure virtual machines (VMs) is currently in preview.</span></span>

<span data-ttu-id="65e93-105">W tym artykule opisano, jak hello tooreplicate maszynach wirtualnych platformy Azure między regiony platformy Azure przy użyciu [usługi Site Recovery](site-recovery-overview.md) w hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="65e93-105">This article describes how tooreplicate Azure VMs between Azure regions by using hello [Site Recovery](site-recovery-overview.md) service in hello Azure portal.</span></span>

<span data-ttu-id="65e93-106">Opublikuj komentarze i pytania u dołu hello tym artykułem lub na powitania [forum usług odzyskiwania Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="65e93-106">Post comments and questions at hello bottom of this article or on hello [Azure Recovery Services forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>

## <a name="disaster-recovery-in-azure"></a><span data-ttu-id="65e93-107">Odzyskiwanie po awarii na platformie Azure</span><span class="sxs-lookup"><span data-stu-id="65e93-107">Disaster recovery in Azure</span></span>

<span data-ttu-id="65e93-108">Funkcje i możliwości wbudowanego infrastruktury platformy Azure wpływ tooa strategii dostępności niezawodny i odporność dla zadań uruchamianych na maszynach wirtualnych platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="65e93-108">Built-in Azure infrastructure capabilities and features contribute tooa robust and resilient availability strategy for workloads that run on Azure VMs.</span></span> <span data-ttu-id="65e93-109">Istnieje jednak wiele przyczyn, czego potrzebujesz tooplan odzyskiwania po awarii między regiony platformy Azure samodzielnie:</span><span class="sxs-lookup"><span data-stu-id="65e93-109">However, there are many reasons why you need tooplan for disaster recovery between Azure regions yourself:</span></span>

- <span data-ttu-id="65e93-110">Należy toomeet wytycznych dotyczących zgodności określonych aplikacji i obciążeń, które wymagają ciągłość prowadzenia działalności biznesowej i strategia odzyskiwania (BCDR).</span><span class="sxs-lookup"><span data-stu-id="65e93-110">You need toomeet compliance guidelines for specific apps and workloads that require a business continuity and disaster recovery (BCDR) strategy.</span></span>
- <span data-ttu-id="65e93-111">Mają hello możliwości tooprotect i odzyskiwania maszyn wirtualnych platformy Azure w zależności od decyzji biznesowych, a nie tylko oparte na wbudowanych funkcji platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="65e93-111">You want hello ability tooprotect and recover Azure VMs based on your business decisions, and not only based on inbuilt Azure functionality.</span></span>
- <span data-ttu-id="65e93-112">Należy tootest trybu failover i odzyskiwania zgodnie z potrzebami działalności biznesowej i zgodności bez wpływu na produkcję.</span><span class="sxs-lookup"><span data-stu-id="65e93-112">You need tootest failover and recovery in accordance with your business and compliance needs, with no impact on production.</span></span>
- <span data-ttu-id="65e93-113">Wymagana jest toofail toohello region odzyskiwania w razie awarii hello i bezproblemowo niepowodzenie wstecz toohello oryginalnego źródła regionu.</span><span class="sxs-lookup"><span data-stu-id="65e93-113">You need toofail over toohello recovery region in hello event of a disaster and fail back toohello original source region seamlessly.</span></span>

<span data-ttu-id="65e93-114">Użyj usługi Site Recovery dla maszyny Wirtualnej Azure-Azure replikacji toohelp wykonać te zadania.</span><span class="sxs-lookup"><span data-stu-id="65e93-114">Use Site Recovery for Azure-to-Azure VM replication toohelp you do all these tasks.</span></span>


## <a name="why-use-site-recovery"></a><span data-ttu-id="65e93-115">Dlaczego warto używać usługi Site Recovery?</span><span class="sxs-lookup"><span data-stu-id="65e93-115">Why use Site Recovery?</span></span>      

<span data-ttu-id="65e93-116">Usługa Site Recovery zapewnia tooreplicate prosty sposób maszynach wirtualnych platformy Azure między regionami:</span><span class="sxs-lookup"><span data-stu-id="65e93-116">Site Recovery provides a simple way tooreplicate Azure VMs between regions:</span></span>

- <span data-ttu-id="65e93-117">**Automatyczne wdrażanie**.</span><span class="sxs-lookup"><span data-stu-id="65e93-117">**Automatic deployment**.</span></span> <span data-ttu-id="65e93-118">W przeciwieństwie do modelu typu aktywny aktywny replikacji nie istnieje potrzeba infrastruktury kosztowne i złożone w regionie pomocniczym hello.</span><span class="sxs-lookup"><span data-stu-id="65e93-118">Unlike an active-active replication model, there's no need for an expensive and complex infrastructure in hello secondary region.</span></span> <span data-ttu-id="65e93-119">Po włączeniu replikacji usługi Site Recovery automatycznie tworzy hello wymagane zasoby w hello region docelowy, na podstawie ustawień regionu źródła.</span><span class="sxs-lookup"><span data-stu-id="65e93-119">When you enable replication, Site Recovery automatically creates hello required resources in hello target region, based on source region settings.</span></span>
- <span data-ttu-id="65e93-120">**Kontrolowanie regionów**.</span><span class="sxs-lookup"><span data-stu-id="65e93-120">**Control regions**.</span></span> <span data-ttu-id="65e93-121">Z usługą Site Recovery może replikować wszelkie tooany regionu w kontynencie.</span><span class="sxs-lookup"><span data-stu-id="65e93-121">With Site Recovery, you can replicate from any region tooany region within a continent.</span></span> <span data-ttu-id="65e93-122">To porównać z magazynu geograficznie nadmiarowego dostęp do odczytu, która asynchronicznie replikuje dane między standard [łączyć regionów](https://docs.microsoft.com/azure/best-practices-availability-paired-regions) tylko.</span><span class="sxs-lookup"><span data-stu-id="65e93-122">Compare this with read-access geo-redundant storage, which replicates asynchronously between standard [paired regions](https://docs.microsoft.com/azure/best-practices-availability-paired-regions) only.</span></span> <span data-ttu-id="65e93-123">Dostęp do odczytu magazynu geograficznie nadmiarowego udostępnia dane toohello dostęp tylko do odczytu w hello region docelowy.</span><span class="sxs-lookup"><span data-stu-id="65e93-123">Read-access geo-redundant storage provides read-only access toohello data in hello target region.</span></span>
- <span data-ttu-id="65e93-124">**Automatyczne replikacji**.</span><span class="sxs-lookup"><span data-stu-id="65e93-124">**Automated replication**.</span></span> <span data-ttu-id="65e93-125">Usługa Site Recovery zapewnia zautomatyzowane replikacji ciągłej.</span><span class="sxs-lookup"><span data-stu-id="65e93-125">Site Recovery provides automated continuous replication.</span></span> <span data-ttu-id="65e93-126">Tryb failover i powrotu po awarii może być uruchomiona za pomocą jednego kliknięcia.</span><span class="sxs-lookup"><span data-stu-id="65e93-126">Failover and failback can be triggered with a single click.</span></span>
- <span data-ttu-id="65e93-127">**RTO i RPO**.</span><span class="sxs-lookup"><span data-stu-id="65e93-127">**RTO and RPO**.</span></span> <span data-ttu-id="65e93-128">Odzyskiwanie lokacji korzysta z infrastruktury sieci Azure hello łączy tookeep regionów RTO i RPO bardzo niskie.</span><span class="sxs-lookup"><span data-stu-id="65e93-128">Site Recovery takes advantage of hello Azure network infrastructure that connects regions tookeep RTO and RPO very low.</span></span>
- <span data-ttu-id="65e93-129">**Testowanie**.</span><span class="sxs-lookup"><span data-stu-id="65e93-129">**Testing**.</span></span> <span data-ttu-id="65e93-130">Testowanie odzyskiwania po awarii można uruchomić z na żądanie testu pracy w trybie Failover, gdy potrzebne bez wpływu na Twoje obciążeń produkcyjnych lub trwającej replikacji.</span><span class="sxs-lookup"><span data-stu-id="65e93-130">You can run disaster-recovery drills with on-demand test failovers, as and when needed, without affecting your production workloads or ongoing replication.</span></span>
- <span data-ttu-id="65e93-131">**Plany odzyskiwania**.</span><span class="sxs-lookup"><span data-stu-id="65e93-131">**Recovery plans**.</span></span> <span data-ttu-id="65e93-132">Można użyć trybu failover tooorchestrate planów odzyskiwania i powrotu po awarii całej aplikacji hello działające na wielu maszynach wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="65e93-132">You can use recovery plans tooorchestrate failover and failback of hello entire application running on multiple VMs.</span></span> <span data-ttu-id="65e93-133">Funkcja planu odzyskiwania Hello ma sformatowanego najwyższej jakości integracji z elementu runbook usługi Automatyzacja Azure.</span><span class="sxs-lookup"><span data-stu-id="65e93-133">hello recovery plan feature has rich first-class integration with Azure automation runbooks.</span></span>


## <a name="deployment-summary"></a><span data-ttu-id="65e93-134">Podsumowanie wdrożenia</span><span class="sxs-lookup"><span data-stu-id="65e93-134">Deployment summary</span></span>

<span data-ttu-id="65e93-135">Oto co należy podsumowanie tooset toodo replikacji maszyn wirtualnych między regiony platformy Azure:</span><span class="sxs-lookup"><span data-stu-id="65e93-135">Here's a summary of what you need toodo tooset up replication of VMs between Azure regions:</span></span>

1. <span data-ttu-id="65e93-136">Utwórz magazyn usługi Recovery Services.</span><span class="sxs-lookup"><span data-stu-id="65e93-136">Create a Recovery Services vault.</span></span> <span data-ttu-id="65e93-137">Magazyn Hello zawiera ustawienia konfiguracji i organizuje replikację.</span><span class="sxs-lookup"><span data-stu-id="65e93-137">hello vault contains configuration settings and orchestrates replication.</span></span>
2. <span data-ttu-id="65e93-138">Włącz replikację hello maszynach wirtualnych platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="65e93-138">Enable replication for hello Azure VMs.</span></span>
3. <span data-ttu-id="65e93-139">Uruchom test toomake trybu failover, się, że wszystko działa zgodnie z oczekiwaniami.</span><span class="sxs-lookup"><span data-stu-id="65e93-139">Run a test failover toomake sure that everything's working as expected.</span></span>

>[!IMPORTANT]
>
> <span data-ttu-id="65e93-140">Możesz sprawdzić hello [macierzy obsługi replikacji maszyny Wirtualnej Azure](./site-recovery-support-matrix-azure-to-azure.md).</span><span class="sxs-lookup"><span data-stu-id="65e93-140">You can check hello [support matrix for Azure VM replication](./site-recovery-support-matrix-azure-to-azure.md).</span></span>

>[!IMPORTANT]
>
> <span data-ttu-id="65e93-141">Aby informacji na temat sposobu tooconfigure hello wymagane wychodzące połączenie sieciowe dla maszyn wirtualnych platformy Azure dla replikacji usługi Site Recovery, zobacz hello [sieci wytycznych](./site-recovery-azure-to-azure-networking-guidance.md).</span><span class="sxs-lookup"><span data-stu-id="65e93-141">For information on how tooconfigure hello required network outbound connectivity for Azure VMs for Site Recovery replication, see hello [networking guidance document](./site-recovery-azure-to-azure-networking-guidance.md).</span></span>

### <a name="before-you-start"></a><span data-ttu-id="65e93-142">Przed rozpoczęciem</span><span class="sxs-lookup"><span data-stu-id="65e93-142">Before you start</span></span>

* <span data-ttu-id="65e93-143">Twoje konto użytkownika systemu Azure wymaga toohave niektórych [uprawnienia](site-recovery-role-based-linked-access-control.md#permissions-required-to-enable-replication-for-new-virtual-machines) tooenable replikacji maszyny wirtualnej platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="65e93-143">Your Azure user account needs toohave certain [permissions](site-recovery-role-based-linked-access-control.md#permissions-required-to-enable-replication-for-new-virtual-machines) tooenable replication of an Azure virtual machine.</span></span>
* <span data-ttu-id="65e93-144">Subskrypcja platformy Azure powinna być maszyn wirtualnych toocreate włączone w miejscu docelowym hello, które mają toouse jako region odzyskiwania po awarii hello.</span><span class="sxs-lookup"><span data-stu-id="65e93-144">Your Azure subscription should be enabled toocreate VMs in hello target location that you want toouse as hello disaster recovery region.</span></span> <span data-ttu-id="65e93-145">Skontaktuj się z pomocą techniczną tooenable hello wymagane limitu przydziału.</span><span class="sxs-lookup"><span data-stu-id="65e93-145">Contact support tooenable hello required quota.</span></span>

## <a name="create-a-recovery-services-vault"></a><span data-ttu-id="65e93-146">Tworzenie magazynu Usług odzyskiwania</span><span class="sxs-lookup"><span data-stu-id="65e93-146">Create a Recovery Services vault</span></span>

[!INCLUDE [site-recovery-create-vault](../../includes/site-recovery-create-vault.md)]

>[!NOTE]
>
> <span data-ttu-id="65e93-147">Zaleca się tworzenie magazynu usług odzyskiwania hello w hello lokalizację tooreplicate sieci maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="65e93-147">We recommend that you create hello Recovery Services vault in hello location where you want your VMs tooreplicate.</span></span> <span data-ttu-id="65e93-148">Na przykład, jeśli w lokalizacji docelowej jest hello centralnego nam, utwórz magazyn hello w **środkowe stany USA**.</span><span class="sxs-lookup"><span data-stu-id="65e93-148">For example, if your target location is hello central US, create hello vault in **Central US**.</span></span>

## <a name="enable-replication"></a><span data-ttu-id="65e93-149">Włączanie replikacji</span><span class="sxs-lookup"><span data-stu-id="65e93-149">Enable replication</span></span>

<span data-ttu-id="65e93-150">W **Magazyny usług odzyskiwania**, kliknij nazwę magazynu hello.</span><span class="sxs-lookup"><span data-stu-id="65e93-150">In **Recovery Services vaults**, click hello vault name.</span></span> <span data-ttu-id="65e93-151">W magazynie powitania kliknij hello **+ Replikuj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="65e93-151">In hello vault, click hello **+Replicate** button.</span></span>

### <a name="step-1-configure-hello-source"></a><span data-ttu-id="65e93-152">Krok 1.</span><span class="sxs-lookup"><span data-stu-id="65e93-152">Step 1.</span></span> <span data-ttu-id="65e93-153">Konfigurowanie źródła hello</span><span class="sxs-lookup"><span data-stu-id="65e93-153">Configure hello source</span></span>
1. <span data-ttu-id="65e93-154">W **źródła**, wybierz pozycję **Azure — wersja ZAPOZNAWCZA**.</span><span class="sxs-lookup"><span data-stu-id="65e93-154">In **Source**, select **Azure - PREVIEW**.</span></span>
2. <span data-ttu-id="65e93-155">W **lokalizacja źródłowa**, wybierz źródło hello region platformy Azure, w którym są uruchomione maszyny wirtualne.</span><span class="sxs-lookup"><span data-stu-id="65e93-155">In **Source location**, select hello source Azure region where your VMs are currently running.</span></span>
3. <span data-ttu-id="65e93-156">Hello wybierz model wdrażania maszyn wirtualnych: **Resource Manager** lub **klasycznego**.</span><span class="sxs-lookup"><span data-stu-id="65e93-156">Select hello deployment model of your VMs: **Resource Manager** or **Classic**.</span></span>
4. <span data-ttu-id="65e93-157">Wybierz hello **źródłowa grupa zasobów** dla maszyn wirtualnych Menedżera zasobów lub **usługi w chmurze** klasycznych maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="65e93-157">Select hello **Source resource group** for Resource Manager VMs or **cloud service** for classic VMs.</span></span>

    ![Konfigurowanie źródła hello](./media/site-recovery-azure-to-azure/source.png)

### <a name="step-2-select-virtual-machines"></a><span data-ttu-id="65e93-159">Krok 2.</span><span class="sxs-lookup"><span data-stu-id="65e93-159">Step 2.</span></span> <span data-ttu-id="65e93-160">Wybierz maszyny wirtualne</span><span class="sxs-lookup"><span data-stu-id="65e93-160">Select virtual machines</span></span>

* <span data-ttu-id="65e93-161">Wybierz VMs hello tooreplicate, a następnie kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="65e93-161">Select hello VMs you want tooreplicate, and then click **OK**.</span></span>

    ![Wybierz maszyny wirtualne](./media/site-recovery-azure-to-azure/vms.png)

### <a name="step-3-configure-settings"></a><span data-ttu-id="65e93-163">Krok 3.</span><span class="sxs-lookup"><span data-stu-id="65e93-163">Step 3.</span></span> <span data-ttu-id="65e93-164">Konfigurowanie ustawień</span><span class="sxs-lookup"><span data-stu-id="65e93-164">Configure settings</span></span>

1. <span data-ttu-id="65e93-165">domyślne hello toooverride target ustawienia i określ ustawienia hello wybór, kliknij przycisk **Dostosuj**.</span><span class="sxs-lookup"><span data-stu-id="65e93-165">toooverride hello default target settings and specify hello settings of your choice, click **Customize**.</span></span> <span data-ttu-id="65e93-166">Aby uzyskać więcej informacji, zobacz [dostosować zasoby docelowe](site-recovery-replicate-azure-to-azure.md##customize-target-resources).</span><span class="sxs-lookup"><span data-stu-id="65e93-166">For more information, see [Customize target resources](site-recovery-replicate-azure-to-azure.md##customize-target-resources).</span></span>

    ![Konfigurowanie ustawień](./media/site-recovery-azure-to-azure/settings.png)


2. <span data-ttu-id="65e93-168">Domyślnie usługa Site Recovery tworzy zasady replikacji, która przyjmuje migawki spójne z aplikacjami co 4 godziny i przechowuje punkty odzyskiwania przez 24 godziny.</span><span class="sxs-lookup"><span data-stu-id="65e93-168">By default, Site Recovery creates a replication policy that takes app-consistent snapshots every 4 hours and retains recovery points for 24 hours.</span></span> <span data-ttu-id="65e93-169">Kliknij toocreate zasady z różnymi ustawieniami **Dostosuj** dalej zbyt**zasad replikacji**.</span><span class="sxs-lookup"><span data-stu-id="65e93-169">toocreate a policy with different settings, click **Customize** next too**Replication Policy**.</span></span>

    ![Dostosuj zasady](./media/site-recovery-azure-to-azure/customize-policy.png)

3. <span data-ttu-id="65e93-171">toostart inicjowania obsługi administracyjnej hello zasobów docelowych, kliknij przycisk **Utwórz zasoby docelowe**.</span><span class="sxs-lookup"><span data-stu-id="65e93-171">toostart provisioning hello target resources, click **Create target resources**.</span></span> <span data-ttu-id="65e93-172">Inicjowanie obsługi administracyjnej ma minuty.</span><span class="sxs-lookup"><span data-stu-id="65e93-172">Provisioning takes a minute or so.</span></span> <span data-ttu-id="65e93-173">Nie zamykaj bloku hello podczas inicjowania obsługi lub wymagana jest toostart.</span><span class="sxs-lookup"><span data-stu-id="65e93-173">Don't close hello blade during provisioning, or you need toostart over.</span></span>

4. <span data-ttu-id="65e93-174">Replikacja tootrigger hello zaznaczone maszyny Wirtualnej, kliknij przycisk **włączyć replikację**.</span><span class="sxs-lookup"><span data-stu-id="65e93-174">tootrigger replication of hello selected VM, click **Enable replication**.</span></span>

5. <span data-ttu-id="65e93-175">Możesz śledzić postępy hello **Włącz ochronę** zadania w **ustawienia** > **zadania** > **zadania usługi Site Recovery**.</span><span class="sxs-lookup"><span data-stu-id="65e93-175">You can track progress of hello **Enable protection** job in **Settings** > **Jobs** > **Site Recovery Jobs**.</span></span>

6. <span data-ttu-id="65e93-176">W **ustawienia** > **elementy replikowane**, można wyświetlić stan hello maszyn wirtualnych i hello postęp replikacji początkowej.</span><span class="sxs-lookup"><span data-stu-id="65e93-176">In **Settings** > **Replicated Items**, you can view hello status of VMs and hello initial replication progress.</span></span> <span data-ttu-id="65e93-177">Kliknij przycisk hello toodrill maszyny Wirtualnej w dół do jego ustawień.</span><span class="sxs-lookup"><span data-stu-id="65e93-177">Click hello VM toodrill down into its settings.</span></span>

## <a name="run-a-test-failover"></a><span data-ttu-id="65e93-178">Wykonywanie próby przejścia w tryb failover</span><span class="sxs-lookup"><span data-stu-id="65e93-178">Run a test failover</span></span>

<span data-ttu-id="65e93-179">Po skonfigurowaniu wszystko, uruchom test toomake trybu failover, czy wszystko działa zgodnie z oczekiwaniami:</span><span class="sxs-lookup"><span data-stu-id="65e93-179">After you set up everything, run a test failover toomake sure everything's working as expected:</span></span>

1. <span data-ttu-id="65e93-180">toofail na jednym komputerze, w **ustawienia** > **elementy replikowane**, kliknij przycisk hello wirtualna **+ testowy tryb Failover** ikony.</span><span class="sxs-lookup"><span data-stu-id="65e93-180">toofail over a single machine, in **Settings** > **Replicated Items**, click hello VM **+Test Failover** icon.</span></span>

2. <span data-ttu-id="65e93-181">zaplanować toofail za pośrednictwem odzyskiwania, **ustawienia** > **plany odzyskiwania**, kliknij prawym przyciskiem myszy hello planu **testowy tryb Failover**.</span><span class="sxs-lookup"><span data-stu-id="65e93-181">toofail over a recovery plan, in **Settings** > **Recovery Plans**, right-click hello plan **Test Failover**.</span></span> <span data-ttu-id="65e93-182">toocreate planu odzyskiwania [wykonaj te instrukcje](site-recovery-create-recovery-plans.md).</span><span class="sxs-lookup"><span data-stu-id="65e93-182">toocreate a recovery plan, [follow these instructions](site-recovery-create-recovery-plans.md).</span></span> 

3. <span data-ttu-id="65e93-183">W **testowy tryb Failover**, wybierz pozycję hello docelowej sieci wirtualnej platformy Azure toowhich maszynach wirtualnych platformy Azure są połączone po hello pracy awaryjnej.</span><span class="sxs-lookup"><span data-stu-id="65e93-183">In **Test Failover**, select hello target Azure virtual network toowhich Azure VMs are connected after hello failover occurs.</span></span>

4. <span data-ttu-id="65e93-184">toostart hello trybu failover, kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="65e93-184">toostart hello failover, click **OK**.</span></span> <span data-ttu-id="65e93-185">tootrack postępu, kliknij przycisk tooopen wirtualna hello jego właściwości.</span><span class="sxs-lookup"><span data-stu-id="65e93-185">tootrack progress, click hello VM tooopen its properties.</span></span> <span data-ttu-id="65e93-186">Można też kliknąć przycisk hello **testowy tryb Failover** zadania w nazwie magazynu hello > **ustawienia** > **zadania** > **zadania usługi Site Recovery**.</span><span class="sxs-lookup"><span data-stu-id="65e93-186">Or you can click hello **Test Failover** job in hello vault name > **Settings** > **Jobs** > **Site Recovery jobs**.</span></span>

5. <span data-ttu-id="65e93-187">Po hello trybu failover zakończy, replika hello Azure maszyny pojawia się w hello portalu Azure > **maszyn wirtualnych**.</span><span class="sxs-lookup"><span data-stu-id="65e93-187">After hello failover finishes, hello replica Azure machine appears in hello Azure portal > **Virtual Machines**.</span></span> <span data-ttu-id="65e93-188">Upewnij się, że tej maszyny Wirtualnej hello jest hello odpowiedni rozmiar, który połączył toohello odpowiedniej sieci i czy działa.</span><span class="sxs-lookup"><span data-stu-id="65e93-188">Make sure that hello VM is hello appropriate size, that it's connected toohello appropriate network, and that it's running.</span></span>

6. <span data-ttu-id="65e93-189">toodelete hello maszyn wirtualnych, które zostały utworzone podczas hello testowania trybu failover kliknij **oczyszczania testowy tryb failover** na powitania replikowane element lub hello planu odzyskiwania.</span><span class="sxs-lookup"><span data-stu-id="65e93-189">toodelete hello VMs that were created during hello test failover, click **Cleanup test failover** on hello replicated item or hello recovery plan.</span></span> <span data-ttu-id="65e93-190">W **uwagi**, zarejestrować i zapisać wszelkie obserwacje związane z hello testowy tryb failover.</span><span class="sxs-lookup"><span data-stu-id="65e93-190">In **Notes**, record and save any observations associated with hello test failover.</span></span> 

<span data-ttu-id="65e93-191">[Dowiedz się więcej](site-recovery-test-failover-to-azure.md) o testowy tryb failover.</span><span class="sxs-lookup"><span data-stu-id="65e93-191">[Learn more](site-recovery-test-failover-to-azure.md) about test failovers.</span></span>


## <a name="next-steps"></a><span data-ttu-id="65e93-192">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="65e93-192">Next steps</span></span>

<span data-ttu-id="65e93-193">Po przetestowaniu hello wdrażania:</span><span class="sxs-lookup"><span data-stu-id="65e93-193">After you test hello deployment:</span></span>

- <span data-ttu-id="65e93-194">[Dowiedz się więcej](site-recovery-failover.md) o różnych typach trybu failover i w jaki sposób toorun je.</span><span class="sxs-lookup"><span data-stu-id="65e93-194">[Learn more](site-recovery-failover.md) about different types of failovers and how toorun them.</span></span>
- <span data-ttu-id="65e93-195">Dowiedz się więcej o [przy użyciu planów odzyskiwania](site-recovery-create-recovery-plans.md) tooreduce RTO.</span><span class="sxs-lookup"><span data-stu-id="65e93-195">Learn more about [using recovery plans](site-recovery-create-recovery-plans.md) tooreduce RTO.</span></span>
