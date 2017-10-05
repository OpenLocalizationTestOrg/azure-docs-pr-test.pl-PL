---
title: "Konfigurowanie źródłowych i docelowych replikacji funkcji Hyper-V do platformy Azure (bez programu System Center VMM) z usługą Azure Site Recovery | Dokumentacja firmy Microsoft"
description: "Przedstawiono kroki, aby skonfigurować ustawienia źródłowe i docelowe dla replikacji maszyn wirtualnych funkcji Hyper-V do magazynu Azure z usługą Azure Site Recovery"
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
ms.openlocfilehash: b38eb3a011d46f2239891ea1d1bcac2a4059a866
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="step-8-set-up-the-source-and-target-for-hyper-v-replication-to-azure"></a><span data-ttu-id="2fc66-103">Krok 8: Konfigurowanie źródłowych i docelowych replikacji funkcji Hyper-V w systemie Azure</span><span class="sxs-lookup"><span data-stu-id="2fc66-103">Step 8: Set up the source and target for Hyper-V replication to Azure</span></span>

<span data-ttu-id="2fc66-104">W tym artykule opisano sposób konfigurowania ustawień źródłowym i docelowym, gdy Replikowanie lokalnych maszyn wirtualnych funkcji Hyper-V (bez programu System Center VMM) na platformie Azure, przy użyciu [usługi Azure Site Recovery](site-recovery-overview.md) w portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="2fc66-104">This article describes how to configure source and target settings when replicating on-premises Hyper-V virtual machines (without System Center VMM) to Azure, using the [Azure Site Recovery](site-recovery-overview.md) service in the Azure portal.</span></span>

<span data-ttu-id="2fc66-105">Opublikuj komentarze i pytania w dolnej części tego artykułu lub na [Forum usług odzyskiwania Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="2fc66-105">Post comments and questions at the bottom of this article, or on the [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>


## <a name="set-up-the-source-environment"></a><span data-ttu-id="2fc66-106">Konfigurowanie środowiska źródłowego</span><span class="sxs-lookup"><span data-stu-id="2fc66-106">Set up the source environment</span></span>

<span data-ttu-id="2fc66-107">Konfigurowanie lokacji funkcji Hyper-V, zainstaluj dostawcę usługi Azure Site Recovery i agent usług odzyskiwania Azure na hostach funkcji Hyper-V i zarejestrować witrynę w magazynie.</span><span class="sxs-lookup"><span data-stu-id="2fc66-107">Set up the Hyper-V site, install the Azure Site Recovery Provider and the Azure Recovery Services agent on Hyper-V hosts, and register the site in the vault.</span></span>

1. <span data-ttu-id="2fc66-108">W **przygotowanie infrastruktury**, kliknij przycisk **źródła**.</span><span class="sxs-lookup"><span data-stu-id="2fc66-108">In **Prepare Infrastructure**, click **Source**.</span></span> <span data-ttu-id="2fc66-109">Aby dodać nową lokację funkcji Hyper-V jako kontener dla hostów funkcji Hyper-V lub klastry, kliknij przycisk **+ lokacja funkcji Hyper-V**.</span><span class="sxs-lookup"><span data-stu-id="2fc66-109">To add a new Hyper-V site as a container for your Hyper-V hosts or clusters, click **+Hyper-V Site**.</span></span>

    ![Konfiguracja źródła](./media/hyper-v-site-walkthrough-source-target/set-source1.png)
2. <span data-ttu-id="2fc66-111">W **lokacji funkcji Hyper-V Utwórz**, określ nazwę lokacji.</span><span class="sxs-lookup"><span data-stu-id="2fc66-111">In **Create Hyper-V site**, specify a name for the site.</span></span> <span data-ttu-id="2fc66-112">Następnie kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="2fc66-112">Then click **OK**.</span></span> <span data-ttu-id="2fc66-113">Teraz, wybierz lokację, możesz utworzyć i kliknij przycisk **+ serwer funkcji Hyper-V** Aby dodać serwer do lokacji.</span><span class="sxs-lookup"><span data-stu-id="2fc66-113">Now, select the site you created, and click **+Hyper-V Server** to add a server to the site.</span></span>

    ![Konfiguracja źródła](./media/hyper-v-site-walkthrough-source-target/set-source2.png)

3. <span data-ttu-id="2fc66-115">W **Dodaj serwer** > **typ serwera**, sprawdź, czy **serwera funkcji Hyper-V** jest wyświetlany.</span><span class="sxs-lookup"><span data-stu-id="2fc66-115">In **Add Server** > **Server type**, check that **Hyper-V server** is displayed.</span></span>

    - <span data-ttu-id="2fc66-116">Upewnij się, że spełnia serwera funkcji Hyper-V, które chcesz dodać [wymagania wstępne](#on-premises-prerequisites)i jest w stanie uzyskać dostępu do określonych adresów URL.</span><span class="sxs-lookup"><span data-stu-id="2fc66-116">Make sure that the Hyper-V server you want to add complies with the [prerequisites](#on-premises-prerequisites), and is able to access the specified URLs.</span></span>
    - <span data-ttu-id="2fc66-117">Pobierz plik instalacyjny dostawcy usługi Azure Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="2fc66-117">Download the Azure Site Recovery Provider installation file.</span></span> <span data-ttu-id="2fc66-118">Możesz uruchomić ten plik, aby zainstalować agenta usług odzyskiwania i dostawcy na każdym hoście funkcji Hyper-V.</span><span class="sxs-lookup"><span data-stu-id="2fc66-118">You run this file to install the Provider and the Recovery Services agent on each Hyper-V host.</span></span>

    ![Konfiguracja źródła](./media/hyper-v-site-walkthrough-source-target/set-source3.png)


## <a name="install-the-provider-and-agent"></a><span data-ttu-id="2fc66-120">Zainstalowany dostawca i agent</span><span class="sxs-lookup"><span data-stu-id="2fc66-120">Install the Provider and agent</span></span>

1. <span data-ttu-id="2fc66-121">Uruchom plik Instalatora na każdym hoście, dodane do lokacji funkcji Hyper-V dostawcę.</span><span class="sxs-lookup"><span data-stu-id="2fc66-121">Run the Provider setup file on each host you added to the Hyper-V site.</span></span> <span data-ttu-id="2fc66-122">Jeśli instalujesz w klastrze funkcji Hyper-V, uruchom Instalatora na każdym węźle klastra.</span><span class="sxs-lookup"><span data-stu-id="2fc66-122">If you're installing on a Hyper-V cluster, run setup on each cluster node.</span></span> <span data-ttu-id="2fc66-123">Instalowanie i rejestrowanie w każdym węźle klastra funkcji Hyper-V zapewnia ochronę maszyn wirtualnych, nawet w przypadku migrowania między węzłami.</span><span class="sxs-lookup"><span data-stu-id="2fc66-123">Installing and registering each Hyper-V cluster node ensures that VMs are protected, even if they migrate across nodes.</span></span>
2. <span data-ttu-id="2fc66-124">W usłudze **Microsoft Update** można włączyć aktualizacje, aby aktualizacje dostawcy były instalowane zgodnie z zasadami Microsoft Update.</span><span class="sxs-lookup"><span data-stu-id="2fc66-124">In **Microsoft Update**, you can opt in for updates so that Provider updates are installed in accordance with your Microsoft Update policy.</span></span>
3. <span data-ttu-id="2fc66-125">W obszarze **Instalacja** zaakceptuj lub zmodyfikuj domyślną lokalizację instalacji dostawcy i kliknij przycisk **Zainstaluj**.</span><span class="sxs-lookup"><span data-stu-id="2fc66-125">In **Installation**, accept or modify the default Provider installation location and click **Install**.</span></span>
4. <span data-ttu-id="2fc66-126">W **ustawienia magazynu**, kliknij przycisk **Przeglądaj** wybierz pobrany plik klucza magazynu.</span><span class="sxs-lookup"><span data-stu-id="2fc66-126">In **Vault Settings**, click **Browse** to select the vault key file that you downloaded.</span></span> <span data-ttu-id="2fc66-127">Określ subskrypcję usługi Azure Site Recovery, nazwę magazynu i lokacji funkcji Hyper-V, do której należy serwer funkcji Hyper-V.</span><span class="sxs-lookup"><span data-stu-id="2fc66-127">Specify the Azure Site Recovery subscription, the vault name, and the Hyper-V site to which the Hyper-V server belongs.</span></span>

    ![Rejestracja serwera](./media/hyper-v-site-walkthrough-source-target/provider3.png)

5. <span data-ttu-id="2fc66-129">W **ustawienia serwera Proxy**, określ, jak dostawca uruchomiony na hostach funkcji Hyper-V łączy się z usługi Azure Site Recovery za pośrednictwem Internetu.</span><span class="sxs-lookup"><span data-stu-id="2fc66-129">In **Proxy Settings**, specify how the Provider running on Hyper-V hosts connects to Azure Site Recovery over the internet.</span></span>

    * <span data-ttu-id="2fc66-130">Jeśli chcesz, aby dostawca łączył się bezpośrednio, wybierz opcję **Połącz bezpośrednio z usługą Azure Site Recovery bez serwera proxy**.</span><span class="sxs-lookup"><span data-stu-id="2fc66-130">If you want the Provider to connect directly select **Connect directly to Azure Site Recovery without a proxy**.</span></span>
    * <span data-ttu-id="2fc66-131">Jeśli istniejący serwer proxy wymaga uwierzytelniania lub chcesz użyć niestandardowego serwera proxy dla połączenia dostawcy, wybierz opcję **nawiązywanie połączenia z usługi Azure Site Recovery przy użyciu serwera proxy**.</span><span class="sxs-lookup"><span data-stu-id="2fc66-131">If your existing proxy requires authentication, or you want to use a custom proxy for the Provider connection, select **Connect to Azure Site Recovery using a proxy server**.</span></span>
    * <span data-ttu-id="2fc66-132">Jeśli używasz serwera proxy:</span><span class="sxs-lookup"><span data-stu-id="2fc66-132">If you use a proxy:</span></span>
        - <span data-ttu-id="2fc66-133">Określ adres, port i poświadczenia</span><span class="sxs-lookup"><span data-stu-id="2fc66-133">Specify the address, port, and credentials</span></span>
        - <span data-ttu-id="2fc66-134">Upewnij się, że adresy URL opisane w [wymagania wstępne](#prerequisites) są dozwolone przez serwer proxy.</span><span class="sxs-lookup"><span data-stu-id="2fc66-134">Make sure the URLs described in the [prerequisites](#prerequisites) are allowed through the proxy.</span></span>

    ![Internet](./media/hyper-v-site-walkthrough-source-target/provider7.png)

6. <span data-ttu-id="2fc66-136">Po zakończeniu instalacji kliknij przycisk **zarejestrować** Aby zarejestrować serwer w magazynie.</span><span class="sxs-lookup"><span data-stu-id="2fc66-136">After installation finishes, click **Register** to register the server in the vault.</span></span>

    ![Lokalizacja instalacji](./media/hyper-v-site-walkthrough-source-target/provider2.png)

7. <span data-ttu-id="2fc66-138">Po zakończeniu rejestracji metadane z serwera funkcji Hyper-V są pobierane przez usługę Azure Site Recovery, a serwer jest wyświetlany w **infrastruktura usługi Site Recovery** > **hosty funkcji Hyper-V**.</span><span class="sxs-lookup"><span data-stu-id="2fc66-138">After registration finishes, metadata from the Hyper-V server is retrieved by Azure Site Recovery, and the server is displayed in **Site Recovery Infrastructure** > **Hyper-V Hosts**.</span></span>


## <a name="set-up-the-target-environment"></a><span data-ttu-id="2fc66-139">Konfigurowanie środowiska docelowego</span><span class="sxs-lookup"><span data-stu-id="2fc66-139">Set up the target environment</span></span>

<span data-ttu-id="2fc66-140">Określ konto magazynu Azure dla replikacji i sieć platformy Azure, z którą maszyny wirtualne Azure będą się łączyć po pracy awaryjnej.</span><span class="sxs-lookup"><span data-stu-id="2fc66-140">Specify the Azure storage account for replication, and the Azure network to which Azure VMs will connect after failover.</span></span>

1. <span data-ttu-id="2fc66-141">Kliknij przycisk **przygotowanie infrastruktury** > **docelowej**.</span><span class="sxs-lookup"><span data-stu-id="2fc66-141">Click **Prepare infrastructure** > **Target**.</span></span>
2. <span data-ttu-id="2fc66-142">Wybierz subskrypcji i grupy zasobów, w którym chcesz utworzyć maszynach wirtualnych Azure po pracy awaryjnej.</span><span class="sxs-lookup"><span data-stu-id="2fc66-142">Select the subscription and the resource group in which you want to create the Azure VMs after failover.</span></span> <span data-ttu-id="2fc66-143">Wybierz model wdrażania, który ma być używany na platformie Azure (Zarządzanie zasobu lub classic) dla maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="2fc66-143">Choose the deployment model that you want to use in Azure (classic or resource management) for the VMs.</span></span>

3. <span data-ttu-id="2fc66-144">Usługa Site Recovery sprawdza, czy masz co najmniej jedno zgodne konto magazynu Azure i co najmniej jedną sieć platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="2fc66-144">Site Recovery checks that you have one or more compatible Azure storage accounts and networks.</span></span>

    - <span data-ttu-id="2fc66-145">Jeśli nie masz konta magazynu, kliknij przycisk **i magazyn** utworzyć wbudowanego konta Menedżera zasobów.</span><span class="sxs-lookup"><span data-stu-id="2fc66-145">If you don't have a storage account, click **+Storage** to create a Resource Manager-based account inline.</span></span> 
    - <span data-ttu-id="2fc66-146">Jeśli nie masz sieć platformy Azure, kliknij przycisk **+ sieć** utworzyć wbudowany sieci przy użyciu usługi Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="2fc66-146">If you don't have a Azure network, click **+Network** to create a Resource Manager-based network inline.</span></span>






## <a name="next-steps"></a><span data-ttu-id="2fc66-147">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="2fc66-147">Next steps</span></span>

<span data-ttu-id="2fc66-148">Przejdź do [krok 9: Konfigurowanie zasad replikacji](hyper-v-site-walkthrough-replication.md)</span><span class="sxs-lookup"><span data-stu-id="2fc66-148">Go to [Step 9: Set up a replication policy](hyper-v-site-walkthrough-replication.md)</span></span>
