---
title: "aaaSet hello źródła i celu tooAzure replikacji funkcji Hyper-V (bez programu System Center VMM) z usługą Azure Site Recovery | Dokumentacja firmy Microsoft"
description: "Podsumowanie tooset kroki hello źródłowa i docelowa ustawień replikacji maszyn wirtualnych funkcji Hyper-V tooAzure magazynu z usługą Azure Site Recovery"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: d2010d85-77fd-4dea-84f3-1c960ed4c63f
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 06/22/2017
ms.author: raynew
ms.openlocfilehash: 105b90e6ac053d5b842c54a36c460a26d0f5c2ef
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="step-8-set-up-hello-source-and-target-for-hyper-v-replication-tooazure"></a><span data-ttu-id="17bb6-103">Krok 8: Konfigurowanie hello źródłowa i docelowa dla tooAzure replikacji funkcji Hyper-V</span><span class="sxs-lookup"><span data-stu-id="17bb6-103">Step 8: Set up hello source and target for Hyper-V replication tooAzure</span></span>

<span data-ttu-id="17bb6-104">W tym artykule opisano sposób tooconfigure źródłowa i docelowa ustawień podczas replikowania lokalnie tooAzure maszyn wirtualnych (bez programu System Center VMM) funkcji Hyper-V, za pomocą hello [usługi Azure Site Recovery](site-recovery-overview.md) w hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="17bb6-104">This article describes how tooconfigure source and target settings when replicating on-premises Hyper-V virtual machines (without System Center VMM) tooAzure, using hello [Azure Site Recovery](site-recovery-overview.md) service in hello Azure portal.</span></span>

<span data-ttu-id="17bb6-105">Opublikuj komentarze i pytania u dołu hello w tym artykule, albo na powitania [Forum usług odzyskiwania Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="17bb6-105">Post comments and questions at hello bottom of this article, or on hello [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>


## <a name="set-up-hello-source-environment"></a><span data-ttu-id="17bb6-106">Konfigurowanie środowiska źródłowego hello</span><span class="sxs-lookup"><span data-stu-id="17bb6-106">Set up hello source environment</span></span>

<span data-ttu-id="17bb6-107">Skonfigurować witrynę hello funkcji Hyper-V, zainstaluj hello dostawcy usługi Azure Site Recovery i agent usług odzyskiwania Azure hello na hostach funkcji Hyper-V i Zarejestruj w magazynie hello hello lokacji.</span><span class="sxs-lookup"><span data-stu-id="17bb6-107">Set up hello Hyper-V site, install hello Azure Site Recovery Provider and hello Azure Recovery Services agent on Hyper-V hosts, and register hello site in hello vault.</span></span>

1. <span data-ttu-id="17bb6-108">W **przygotowanie infrastruktury**, kliknij przycisk **źródła**.</span><span class="sxs-lookup"><span data-stu-id="17bb6-108">In **Prepare Infrastructure**, click **Source**.</span></span> <span data-ttu-id="17bb6-109">tooadd nowej lokacji funkcji Hyper-V jako kontener dla hostów funkcji Hyper-V lub klastry, kliknij przycisk **+ lokacja funkcji Hyper-V**.</span><span class="sxs-lookup"><span data-stu-id="17bb6-109">tooadd a new Hyper-V site as a container for your Hyper-V hosts or clusters, click **+Hyper-V Site**.</span></span>

    ![Konfiguracja źródła](./media/hyper-v-site-walkthrough-source-target/set-source1.png)
2. <span data-ttu-id="17bb6-111">W **lokacji funkcji Hyper-V Utwórz**, określ nazwę lokacji hello.</span><span class="sxs-lookup"><span data-stu-id="17bb6-111">In **Create Hyper-V site**, specify a name for hello site.</span></span> <span data-ttu-id="17bb6-112">Następnie kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="17bb6-112">Then click **OK**.</span></span> <span data-ttu-id="17bb6-113">Teraz, wybierz witrynę hello utworzone i kliknij **+ serwer funkcji Hyper-V** tooadd toohello serwera lokacji.</span><span class="sxs-lookup"><span data-stu-id="17bb6-113">Now, select hello site you created, and click **+Hyper-V Server** tooadd a server toohello site.</span></span>

    ![Konfiguracja źródła](./media/hyper-v-site-walkthrough-source-target/set-source2.png)

3. <span data-ttu-id="17bb6-115">W **Dodaj serwer** > **typ serwera**, sprawdź, czy **serwera funkcji Hyper-V** jest wyświetlany.</span><span class="sxs-lookup"><span data-stu-id="17bb6-115">In **Add Server** > **Server type**, check that **Hyper-V server** is displayed.</span></span>

    - <span data-ttu-id="17bb6-116">Sprawdź, czy ten serwer hello funkcji Hyper-V ma spełnia tooadd hello [wymagania wstępne](#on-premises-prerequisites), i jest w stanie tooaccess hello określonych adresów URL.</span><span class="sxs-lookup"><span data-stu-id="17bb6-116">Make sure that hello Hyper-V server you want tooadd complies with hello [prerequisites](#on-premises-prerequisites), and is able tooaccess hello specified URLs.</span></span>
    - <span data-ttu-id="17bb6-117">Pobierz plik instalacyjny dostawcy usługi Azure Site Recovery hello.</span><span class="sxs-lookup"><span data-stu-id="17bb6-117">Download hello Azure Site Recovery Provider installation file.</span></span> <span data-ttu-id="17bb6-118">Uruchom ten plik tooinstall hello dostawcy i hello agenta usług odzyskiwania na każdym hoście funkcji Hyper-V.</span><span class="sxs-lookup"><span data-stu-id="17bb6-118">You run this file tooinstall hello Provider and hello Recovery Services agent on each Hyper-V host.</span></span>

    ![Konfiguracja źródła](./media/hyper-v-site-walkthrough-source-target/set-source3.png)


## <a name="install-hello-provider-and-agent"></a><span data-ttu-id="17bb6-120">Zainstaluj hello dostawca i agent</span><span class="sxs-lookup"><span data-stu-id="17bb6-120">Install hello Provider and agent</span></span>

1. <span data-ttu-id="17bb6-121">Uruchom plik Instalatora dostawcy hello na każdym hoście po dodaniu lokacji toohello funkcji Hyper-V.</span><span class="sxs-lookup"><span data-stu-id="17bb6-121">Run hello Provider setup file on each host you added toohello Hyper-V site.</span></span> <span data-ttu-id="17bb6-122">Jeśli instalujesz w klastrze funkcji Hyper-V, uruchom Instalatora na każdym węźle klastra.</span><span class="sxs-lookup"><span data-stu-id="17bb6-122">If you're installing on a Hyper-V cluster, run setup on each cluster node.</span></span> <span data-ttu-id="17bb6-123">Instalowanie i rejestrowanie w każdym węźle klastra funkcji Hyper-V zapewnia ochronę maszyn wirtualnych, nawet w przypadku migrowania między węzłami.</span><span class="sxs-lookup"><span data-stu-id="17bb6-123">Installing and registering each Hyper-V cluster node ensures that VMs are protected, even if they migrate across nodes.</span></span>
2. <span data-ttu-id="17bb6-124">W usłudze **Microsoft Update** można włączyć aktualizacje, aby aktualizacje dostawcy były instalowane zgodnie z zasadami Microsoft Update.</span><span class="sxs-lookup"><span data-stu-id="17bb6-124">In **Microsoft Update**, you can opt in for updates so that Provider updates are installed in accordance with your Microsoft Update policy.</span></span>
3. <span data-ttu-id="17bb6-125">W **instalacji**, Zaakceptuj lub zmodyfikuj hello domyślną lokalizację instalacji dostawcy i kliknij przycisk **zainstalować**.</span><span class="sxs-lookup"><span data-stu-id="17bb6-125">In **Installation**, accept or modify hello default Provider installation location and click **Install**.</span></span>
4. <span data-ttu-id="17bb6-126">W **ustawienia magazynu**, kliknij przycisk **Przeglądaj** tooselect hello magazynu kluczy pobranego pliku.</span><span class="sxs-lookup"><span data-stu-id="17bb6-126">In **Vault Settings**, click **Browse** tooselect hello vault key file that you downloaded.</span></span> <span data-ttu-id="17bb6-127">Określ subskrypcję usługi Azure Site Recovery hello, hello nazwę magazynu, i należy serwer hello funkcji Hyper-V toowhich hello funkcji Hyper-V w lokacji.</span><span class="sxs-lookup"><span data-stu-id="17bb6-127">Specify hello Azure Site Recovery subscription, hello vault name, and hello Hyper-V site toowhich hello Hyper-V server belongs.</span></span>

    ![Rejestracja serwera](./media/hyper-v-site-walkthrough-source-target/provider3.png)

5. <span data-ttu-id="17bb6-129">W **ustawienia serwera Proxy**, określ, jak dostawca uruchomiony na hostach funkcji Hyper-V łączy tooAzure usługi Site Recovery za pośrednictwem hello hello internet.</span><span class="sxs-lookup"><span data-stu-id="17bb6-129">In **Proxy Settings**, specify how hello Provider running on Hyper-V hosts connects tooAzure Site Recovery over hello internet.</span></span>

    * <span data-ttu-id="17bb6-130">Jeśli chcesz tooconnect dostawcy hello bezpośrednio wybierz **łączą się bezpośrednio tooAzure odzyskiwania lokacji bez serwera proxy**.</span><span class="sxs-lookup"><span data-stu-id="17bb6-130">If you want hello Provider tooconnect directly select **Connect directly tooAzure Site Recovery without a proxy**.</span></span>
    * <span data-ttu-id="17bb6-131">Zaznacz, jeśli istniejący serwer proxy wymaga uwierzytelniania lub chcesz toouse niestandardowego serwera proxy dla połączenia z dostawcą hello **połączyć tooAzure Przywracanie lokacji z użyciem serwera proxy**.</span><span class="sxs-lookup"><span data-stu-id="17bb6-131">If your existing proxy requires authentication, or you want toouse a custom proxy for hello Provider connection, select **Connect tooAzure Site Recovery using a proxy server**.</span></span>
    * <span data-ttu-id="17bb6-132">Jeśli używasz serwera proxy:</span><span class="sxs-lookup"><span data-stu-id="17bb6-132">If you use a proxy:</span></span>
        - <span data-ttu-id="17bb6-133">Określ adres hello, port i poświadczenia</span><span class="sxs-lookup"><span data-stu-id="17bb6-133">Specify hello address, port, and credentials</span></span>
        - <span data-ttu-id="17bb6-134">Upewnij się, że hello adresy URL opisane w hello [wymagania wstępne](#prerequisites) mogą za pośrednictwem serwera proxy hello.</span><span class="sxs-lookup"><span data-stu-id="17bb6-134">Make sure hello URLs described in hello [prerequisites](#prerequisites) are allowed through hello proxy.</span></span>

    ![Internet](./media/hyper-v-site-walkthrough-source-target/provider7.png)

6. <span data-ttu-id="17bb6-136">Po zakończeniu instalacji kliknij przycisk **zarejestrować** tooregister powitania serwera w magazynie hello.</span><span class="sxs-lookup"><span data-stu-id="17bb6-136">After installation finishes, click **Register** tooregister hello server in hello vault.</span></span>

    ![Lokalizacja instalacji](./media/hyper-v-site-walkthrough-source-target/provider2.png)

7. <span data-ttu-id="17bb6-138">Po zakończeniu rejestracji metadane z serwera funkcji Hyper-V hello są pobierane przez usługę Azure Site Recovery, a powitania serwera są wyświetlane w **infrastruktura usługi Site Recovery** > **hosty funkcji Hyper-V**.</span><span class="sxs-lookup"><span data-stu-id="17bb6-138">After registration finishes, metadata from hello Hyper-V server is retrieved by Azure Site Recovery, and hello server is displayed in **Site Recovery Infrastructure** > **Hyper-V Hosts**.</span></span>


## <a name="set-up-hello-target-environment"></a><span data-ttu-id="17bb6-139">Konfigurowanie środowiska docelowego hello</span><span class="sxs-lookup"><span data-stu-id="17bb6-139">Set up hello target environment</span></span>

<span data-ttu-id="17bb6-140">Określ konto magazynu Azure hello replikacji, a hello toowhich sieć platformy Azure, maszyny wirtualne Azure będą się łączyć po pracy awaryjnej.</span><span class="sxs-lookup"><span data-stu-id="17bb6-140">Specify hello Azure storage account for replication, and hello Azure network toowhich Azure VMs will connect after failover.</span></span>

1. <span data-ttu-id="17bb6-141">Kliknij przycisk **przygotowanie infrastruktury** > **docelowej**.</span><span class="sxs-lookup"><span data-stu-id="17bb6-141">Click **Prepare infrastructure** > **Target**.</span></span>
2. <span data-ttu-id="17bb6-142">Wybierz hello subskrypcji i grupy zasobów hello mają toocreate hello Azure maszyn wirtualnych po pracy awaryjnej.</span><span class="sxs-lookup"><span data-stu-id="17bb6-142">Select hello subscription and hello resource group in which you want toocreate hello Azure VMs after failover.</span></span> <span data-ttu-id="17bb6-143">Wybierz wdrożenia hello modelu mają toouse na platformie Azure (Zarządzanie zasobu lub classic) dla hello maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="17bb6-143">Choose hello deployment model that you want toouse in Azure (classic or resource management) for hello VMs.</span></span>

3. <span data-ttu-id="17bb6-144">Usługa Site Recovery sprawdza, czy masz co najmniej jedno zgodne konto magazynu Azure i co najmniej jedną sieć platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="17bb6-144">Site Recovery checks that you have one or more compatible Azure storage accounts and networks.</span></span>

    - <span data-ttu-id="17bb6-145">Jeśli nie masz konta magazynu, kliknij przycisk **i magazyn** toocreate wbudowanego konta Menedżera zasobów.</span><span class="sxs-lookup"><span data-stu-id="17bb6-145">If you don't have a storage account, click **+Storage** toocreate a Resource Manager-based account inline.</span></span> 
    - <span data-ttu-id="17bb6-146">Jeśli nie masz sieć platformy Azure, kliknij przycisk **+ sieć** toocreate wbudowanego sieci przy użyciu usługi Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="17bb6-146">If you don't have a Azure network, click **+Network** toocreate a Resource Manager-based network inline.</span></span>






## <a name="next-steps"></a><span data-ttu-id="17bb6-147">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="17bb6-147">Next steps</span></span>

<span data-ttu-id="17bb6-148">Przejdź do zbyt[krok 9: Konfigurowanie zasad replikacji](hyper-v-site-walkthrough-replication.md)</span><span class="sxs-lookup"><span data-stu-id="17bb6-148">Go too[Step 9: Set up a replication policy](hyper-v-site-walkthrough-replication.md)</span></span>
