---
title: "Konfigurowanie źródłowych i docelowych replikacji funkcji Hyper-V do platformy Azure (w programie System Center VMM) z usługą Azure Site Recovery | Dokumentacja firmy Microsoft"
description: "Zawiera podsumowanie kroków, aby skonfigurować ustawienia źródłowego i docelowego replikacji maszyn wirtualnych funkcji Hyper-V w chmurach VMM do magazynu Azure z usługą Azure Site Recovery"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: 5edb6d87-25a5-40fe-b6f1-ddf7b55a6b31
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 07/25/2017
ms.author: raynew
ms.openlocfilehash: c72f839d0a1288dccb7deb3e44fc2b20d64818f0
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
# <a name="step-8-set-up-the-source-and-target-for-hyper-v-with-vmm-replication-to-azure"></a><span data-ttu-id="7ec8c-103">Krok 8: Konfigurowanie źródłowych i docelowych dla replikacji funkcji Hyper-V (w programie VMM) na platformie Azure</span><span class="sxs-lookup"><span data-stu-id="7ec8c-103">Step 8: Set up the source and target for Hyper-V (with VMM) replication to Azure</span></span>

<span data-ttu-id="7ec8c-104">Po [utworzenie magazynu](vmm-to-azure-walkthrough-create-vault.md) i określenie, co chcesz replikować, użyj w tym artykule do skonfigurowania ustawień źródłowym i docelowym, podczas replikowania lokalnych maszyn wirtualnych funkcji Hyper-V w chmurach programu System Center Virtual Machine Manager (VMM) na platformie Azure przy użyciu [usługi Azure Site Recovery](site-recovery-overview.md) w portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="7ec8c-104">After [creating a vault](vmm-to-azure-walkthrough-create-vault.md) and specifying what you want to replicate, use this article to configure source and target settings when replicating on-premises Hyper-V virtual machines in System Center Virtual Machine Manager (VMM) clouds to Azure, using the [Azure Site Recovery](site-recovery-overview.md) service in the Azure portal.</span></span>

<span data-ttu-id="7ec8c-105">Opublikuj komentarze i pytania w dolnej części tego artykułu lub na [Forum usług odzyskiwania Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="7ec8c-105">Post comments and questions at the bottom of this article, or on the [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>


## <a name="set-up-the-source-environment"></a><span data-ttu-id="7ec8c-106">Konfigurowanie środowiska źródłowego</span><span class="sxs-lookup"><span data-stu-id="7ec8c-106">Set up the source environment</span></span>

<span data-ttu-id="7ec8c-107">S1.</span><span class="sxs-lookup"><span data-stu-id="7ec8c-107">S1.</span></span> <span data-ttu-id="7ec8c-108">Kliknij pozycję **Przygotowanie infrastruktury** > **Źródło**.</span><span class="sxs-lookup"><span data-stu-id="7ec8c-108">Click **Prepare Infrastructure** > **Source**.</span></span>

    ![Set up source](./media/vmm-to-azure-walkthrough-source-target/set-source1.png)

2. <span data-ttu-id="7ec8c-109">W obszarze **Przygotowywanie źródła** kliknij pozycję **+ VMM**, aby dodać serwer programu VMM.</span><span class="sxs-lookup"><span data-stu-id="7ec8c-109">In **Prepare source**, click **+ VMM** to add a VMM server.</span></span>

    ![Konfiguracja źródła](./media/vmm-to-azure-walkthrough-source-target/set-source2.png)

3. <span data-ttu-id="7ec8c-111">W obszarze **Dodawanie serwera** sprawdź, czy **Serwer programu System Center VMM** pojawia się w sekcji **Typ serwera** i czy serwer VMM spełnia [warunki wstępne i wymagania dotyczące adresu URL](#prerequisites).</span><span class="sxs-lookup"><span data-stu-id="7ec8c-111">In **Add Server**, check that **System Center VMM server** appears in **Server type** and that the VMM server meets the [prerequisites and URL requirements](#prerequisites).</span></span>
4. <span data-ttu-id="7ec8c-112">Pobierz plik instalacyjny dostawcy usługi Azure Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="7ec8c-112">Download the Azure Site Recovery Provider installation file.</span></span>
5. <span data-ttu-id="7ec8c-113">Pobierz klucz rejestracji.</span><span class="sxs-lookup"><span data-stu-id="7ec8c-113">Download the registration key.</span></span> <span data-ttu-id="7ec8c-114">Będzie on potrzebny po uruchomieniu Instalatora.</span><span class="sxs-lookup"><span data-stu-id="7ec8c-114">You need this when you run setup.</span></span> <span data-ttu-id="7ec8c-115">Klucz jest ważny przez pięć dni po jego wygenerowaniu.</span><span class="sxs-lookup"><span data-stu-id="7ec8c-115">The key is valid for five days after you generate it.</span></span>

    ![Konfiguracja źródła](./media/vmm-to-azure-walkthrough-source-target/set-source3.png)

## <a name="install-the-provider-on-the-vmm-server"></a><span data-ttu-id="7ec8c-117">Instalowanie dostawcy na serwerze VMM</span><span class="sxs-lookup"><span data-stu-id="7ec8c-117">Install the Provider on the VMM server</span></span>

1. <span data-ttu-id="7ec8c-118">Uruchom plik Instalatora dostawcy na serwerze VMM.</span><span class="sxs-lookup"><span data-stu-id="7ec8c-118">Run the Provider setup file on the VMM server.</span></span>
2. <span data-ttu-id="7ec8c-119">W usłudze **Microsoft Update** można włączyć aktualizacje, aby aktualizacje dostawcy były instalowane zgodnie z zasadami Microsoft Update.</span><span class="sxs-lookup"><span data-stu-id="7ec8c-119">In **Microsoft Update**, you can opt in for updates so that Provider updates are installed in accordance with your Microsoft Update policy.</span></span>
3. <span data-ttu-id="7ec8c-120">W obszarze **Instalacja** zaakceptuj lub zmodyfikuj domyślną lokalizację instalacji dostawcy i kliknij przycisk **Zainstaluj**.</span><span class="sxs-lookup"><span data-stu-id="7ec8c-120">In **Installation**, accept or modify the default Provider installation location and click **Install**.</span></span>

    ![Lokalizacja instalacji](./media/vmm-to-azure-walkthrough-source-target/provider2.png)
4. <span data-ttu-id="7ec8c-122">Po zakończeniu instalacji kliknij przycisk **Zarejestruj**, aby zarejestrować serwer programu VMM w magazynie.</span><span class="sxs-lookup"><span data-stu-id="7ec8c-122">When installation finishes, click **Register** to register the VMM server in the vault.</span></span>
5. <span data-ttu-id="7ec8c-123">Na stronie **Ustawienia magazynu** kliknij przycisk **Przeglądaj**, aby wybrać plik klucza magazynu.</span><span class="sxs-lookup"><span data-stu-id="7ec8c-123">In the **Vault Settings** page, click **Browse** to select the vault key file.</span></span> <span data-ttu-id="7ec8c-124">Określ subskrypcję usługi Azure Site Recovery oraz nazwę magazynu.</span><span class="sxs-lookup"><span data-stu-id="7ec8c-124">Specify the Azure Site Recovery subscription and the vault name.</span></span>

    ![Rejestracja serwera](./media/vmm-to-azure-walkthrough-source-target/provider10.png)
6. <span data-ttu-id="7ec8c-126">W obszarze **Połączenie internetowe** określ, jak dostawca uruchomiony na serwerze próbujemy VMM będzie się łączyć z usługą Site Recovery za pośrednictwem Internetu.</span><span class="sxs-lookup"><span data-stu-id="7ec8c-126">In **Internet Connection**, specify how the Provider running on the VMM server will connect to Site Recovery over the internet.</span></span>

   * <span data-ttu-id="7ec8c-127">Jeśli chcesz, aby dostawca łączył się bezpośrednio, wybierz opcję **Połącz bezpośrednio z usługą Azure Site Recovery bez serwera proxy**.</span><span class="sxs-lookup"><span data-stu-id="7ec8c-127">If you want the Provider to connect directly, select **Connect directly to Azure Site Recovery without a proxy**.</span></span>
   * <span data-ttu-id="7ec8c-128">Jeśli istniejący serwer proxy wymaga uwierzytelniania lub chcesz użyć niestandardowego serwera proxy, wybierz opcję **Połącz z usługą Azure Site Recovery przy użyciu serwera proxy**.</span><span class="sxs-lookup"><span data-stu-id="7ec8c-128">If your existing proxy requires authentication, or you want to use a custom proxy, select **Connect to Azure Site Recovery using a proxy server**.</span></span>
   * <span data-ttu-id="7ec8c-129">Jeśli używasz niestandardowego serwera proxy, określ adres, port i poświadczenia.</span><span class="sxs-lookup"><span data-stu-id="7ec8c-129">If you use a custom proxy, specify the address, port, and credentials.</span></span>
   * <span data-ttu-id="7ec8c-130">W przypadku użycia serwera proxy już zezwolono na użycie adresów URL opisanych w [wymaganiach wstępnych](#on-premises-prerequisites).</span><span class="sxs-lookup"><span data-stu-id="7ec8c-130">If you're using a proxy, you should have already allowed the URLs described in [prerequisites](#on-premises-prerequisites).</span></span>
   * <span data-ttu-id="7ec8c-131">W przypadku użycia niestandardowego serwera proxy konto Uruchom jako programu VMM (DRAProxyAccount) zostanie automatycznie utworzone przy użyciu określonych poświadczeń serwera proxy.</span><span class="sxs-lookup"><span data-stu-id="7ec8c-131">If you use a custom proxy, a VMM RunAs account (DRAProxyAccount) will be created automatically using the specified proxy credentials.</span></span> <span data-ttu-id="7ec8c-132">Skonfiguruj serwer proxy tak, aby to konto mogło być pomyślnie uwierzytelnione.</span><span class="sxs-lookup"><span data-stu-id="7ec8c-132">Configure the proxy server so that this account can authenticate successfully.</span></span> <span data-ttu-id="7ec8c-133">Ustawienia konta Uruchom jako programu VMM można zmodyfikować w konsoli programu VMM.</span><span class="sxs-lookup"><span data-stu-id="7ec8c-133">The VMM RunAs account settings can be modified in the VMM console.</span></span> <span data-ttu-id="7ec8c-134">W obszarze **Ustawienia** rozwiń pozycję **Zabezpieczenia** > **Konta Uruchom jako**, a następnie zmodyfikuj hasło dla konta DRAProxyAccount.</span><span class="sxs-lookup"><span data-stu-id="7ec8c-134">In **Settings**, expand **Security** > **Run As Accounts**, and then modify the password for DRAProxyAccount.</span></span> <span data-ttu-id="7ec8c-135">Aby to ustawienie zostało zastosowane, należy ponownie uruchomić usługę programu VMM.</span><span class="sxs-lookup"><span data-stu-id="7ec8c-135">You’ll need to restart the VMM service so that this setting takes effect.</span></span>

     ![Internet](./media/vmm-to-azure-walkthrough-source-target/provider13.png)
7. <span data-ttu-id="7ec8c-137">Zaakceptuj lub zmodyfikuj lokalizację certyfikatu SSL, który jest automatycznie generowany w związku z szyfrowaniem danych.</span><span class="sxs-lookup"><span data-stu-id="7ec8c-137">Accept or modify the location of an SSL certificate that’s automatically generated for data encryption.</span></span> <span data-ttu-id="7ec8c-138">Ten certyfikat jest wykorzystywany, jeśli włączysz szyfrowanie danych dla chmury chronionej przez platformę Azure w portalu usługi Azure Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="7ec8c-138">This certificate is used if you enable data encryption for a cloud protected by Azure in the Azure Site Recovery portal.</span></span> <span data-ttu-id="7ec8c-139">Przechowuj ten certyfikat w bezpiecznym miejscu.</span><span class="sxs-lookup"><span data-stu-id="7ec8c-139">Keep this certificate safe.</span></span> <span data-ttu-id="7ec8c-140">Po uruchomieniu trybu failover na platformie Azure certyfikat będzie potrzebny do odszyfrowania danych, jeśli włączono szyfrowanie.</span><span class="sxs-lookup"><span data-stu-id="7ec8c-140">When you run a failover to Azure you’ll need it to decrypt, if data encryption is enabled.</span></span>
8. <span data-ttu-id="7ec8c-141">W polu **Nazwa serwera** wprowadź przyjazną nazwę identyfikującą serwer VMM w magazynie.</span><span class="sxs-lookup"><span data-stu-id="7ec8c-141">In **Server name**, specify a friendly name to identify the VMM server in the vault.</span></span> <span data-ttu-id="7ec8c-142">W konfiguracji klastra określ nazwę roli klastra VMM.</span><span class="sxs-lookup"><span data-stu-id="7ec8c-142">In a cluster configuration, specify the VMM cluster role name.</span></span>
9. <span data-ttu-id="7ec8c-143">Włącz **synchronizację metadanych chmury**, jeśli chcesz synchronizować metadane dla wszystkich chmur na serwerze VMM w magazynie.</span><span class="sxs-lookup"><span data-stu-id="7ec8c-143">Enable **Sync cloud metadata**, if you want to synchronize metadata for all clouds on the VMM server with the vault.</span></span> <span data-ttu-id="7ec8c-144">To działanie ma miejsce tylko raz na każdym serwerze.</span><span class="sxs-lookup"><span data-stu-id="7ec8c-144">This action only needs to happen once on each server.</span></span> <span data-ttu-id="7ec8c-145">Jeśli nie chcesz synchronizować wszystkich chmur, możesz nie zaznaczać tego ustawienia i synchronizować poszczególne chmury indywidualnie we właściwościach chmury w konsoli programu VMM.</span><span class="sxs-lookup"><span data-stu-id="7ec8c-145">If you don't want to synchronize all clouds, you can leave this setting unchecked and synchronize each cloud individually in the cloud properties in the VMM console.</span></span> <span data-ttu-id="7ec8c-146">Kliknij przycisk **Zarejestruj**, aby zakończyć proces.</span><span class="sxs-lookup"><span data-stu-id="7ec8c-146">Click **Register** to complete the process.</span></span>

    ![Rejestracja serwera](./media/vmm-to-azure-walkthrough-source-target/provider16.png)
10. <span data-ttu-id="7ec8c-148">Rozpoczyna się rejestracja.</span><span class="sxs-lookup"><span data-stu-id="7ec8c-148">Registration starts.</span></span> <span data-ttu-id="7ec8c-149">Po zakończeniu rejestracji serwer jest wyświetlany w obszarze **Infrastruktura usługi Site Recovery** > **Serwery VMM**.</span><span class="sxs-lookup"><span data-stu-id="7ec8c-149">After registration finishes, the server is displayed in **Site Recovery Infrastructure** > **VMM Servers**.</span></span>


## <a name="install-the-azure-recovery-services-agent-on-hyper-v-hosts"></a><span data-ttu-id="7ec8c-150">Instalacja agenta Usług odzyskiwania Azure na hostach funkcji Hyper-V</span><span class="sxs-lookup"><span data-stu-id="7ec8c-150">Install the Azure Recovery Services agent on Hyper-V hosts</span></span>

1. <span data-ttu-id="7ec8c-151">Po skonfigurowaniu dostawcy należy pobrać plik instalacyjny agenta usług Azure Recovery Services.</span><span class="sxs-lookup"><span data-stu-id="7ec8c-151">After you've set up the Provider, you need to download the installation file for the Azure Recovery Services agent.</span></span> <span data-ttu-id="7ec8c-152">Uruchom Instalator na każdym serwerze funkcji Hyper-V w chmurze VMM.</span><span class="sxs-lookup"><span data-stu-id="7ec8c-152">Run setup on each Hyper-V server in the VMM cloud.</span></span>

    ![Lokacje funkcji Hyper-V](./media/vmm-to-azure-walkthrough-source-target/hyperv-agent1.png)
2. <span data-ttu-id="7ec8c-154">W obszarze **Sprawdzanie wymagań wstępnych** kliknij przycisk **Dalej**.</span><span class="sxs-lookup"><span data-stu-id="7ec8c-154">In **Prerequisites Check**, click **Next**.</span></span> <span data-ttu-id="7ec8c-155">Wszystkie brakujące wymagania wstępne zostaną zainstalowane automatycznie.</span><span class="sxs-lookup"><span data-stu-id="7ec8c-155">Any missing prerequisites will be automatically installed.</span></span>

    ![Wymagania wstępne dotyczące agenta Usług odzyskiwania](./media/vmm-to-azure-walkthrough-source-target/hyperv-agent2.png)
3. <span data-ttu-id="7ec8c-157">W obszarze **Ustawienia instalacji** zaakceptuj lub zmodyfikuj lokalizację instalacji i lokalizację pamięci podręcznej.</span><span class="sxs-lookup"><span data-stu-id="7ec8c-157">In **Installation Settings**, accept or modify the installation location, and the cache location.</span></span> <span data-ttu-id="7ec8c-158">Możesz skonfigurować pamięć podręczną na dysku, który ma co najmniej 5 GB dostępnego miejsca, ale zalecamy dysk pamięci podręcznej z co najmniej 600 GB wolnego miejsca.</span><span class="sxs-lookup"><span data-stu-id="7ec8c-158">You can configure the cache on a drive that has at least 5 GB of storage available but we recommend a cache drive with 600 GB or more of free space.</span></span> <span data-ttu-id="7ec8c-159">Następnie kliknij pozycję **Zainstaluj**.</span><span class="sxs-lookup"><span data-stu-id="7ec8c-159">Then click **Install**.</span></span>
4. <span data-ttu-id="7ec8c-160">Po zakończeniu instalacji kliknij przycisk **Zamknij**, aby zakończyć.</span><span class="sxs-lookup"><span data-stu-id="7ec8c-160">After installation is complete, click **Close** to finish.</span></span>

    ![Rejestracja agenta MARS](./media/vmm-to-azure-walkthrough-source-target/hyperv-agent3.png)

### <a name="command-line-installation"></a><span data-ttu-id="7ec8c-162">Instalacja przy użyciu wiersza polecenia</span><span class="sxs-lookup"><span data-stu-id="7ec8c-162">Command line installation</span></span>
<span data-ttu-id="7ec8c-163">Agenta Usług odzyskiwania Microsoft Azure można zainstalować z poziomu wiersza polecenia przy użyciu następującego polecenia:</span><span class="sxs-lookup"><span data-stu-id="7ec8c-163">You can install the Microsoft Azure Recovery Services Agent from command line using the following command:</span></span>

     marsagentinstaller.exe /q /nu

### <a name="set-up-internet-proxy-access-to-site-recovery-from-hyper-v-hosts"></a><span data-ttu-id="7ec8c-164">Konfigurowanie internetowego dostępu serwera proxy do usługi Site Recovery na hostach funkcji Hyper-V</span><span class="sxs-lookup"><span data-stu-id="7ec8c-164">Set up internet proxy access to Site Recovery from Hyper-V hosts</span></span>

<span data-ttu-id="7ec8c-165">Agent Usług odzyskiwania uruchomiony na hostach funkcji Hyper-V wymaga internetowego dostępu do platformy Azure, aby umożliwić replikację maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="7ec8c-165">The Recovery Services agent running on Hyper-V hosts needs internet access to Azure for VM replication.</span></span> <span data-ttu-id="7ec8c-166">Jeśli uzyskujesz dostęp do Internetu za pośrednictwem serwera proxy, skonfiguruj go w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="7ec8c-166">If you're accessing the internet through a proxy, set it up as follows:</span></span>

1. <span data-ttu-id="7ec8c-167">Otwórz przystawkę MMC usługi Microsoft Azure Backup na hoście funkcji Hyper-V.</span><span class="sxs-lookup"><span data-stu-id="7ec8c-167">Open the Microsoft Azure Backup MMC snap-in on the Hyper-V host.</span></span> <span data-ttu-id="7ec8c-168">Domyślnie skrót do usługi Microsoft Azure Backup jest dostępny na pulpicie lub w folderze C:\Program Files\Microsoft Azure Recovery Services Agent\bin\wabadmin.</span><span class="sxs-lookup"><span data-stu-id="7ec8c-168">By default, a shortcut for Microsoft Azure Backup is available on the desktop or in C:\Program Files\Microsoft Azure Recovery Services Agent\bin\wabadmin.</span></span>
2. <span data-ttu-id="7ec8c-169">W przystawce kliknij pozycję **Zmień właściwości**.</span><span class="sxs-lookup"><span data-stu-id="7ec8c-169">In the snap-in, click **Change Properties**.</span></span>
3. <span data-ttu-id="7ec8c-170">Na karcie **Konfiguracja serwera proxy** podaj informacje dotyczące serwera proxy.</span><span class="sxs-lookup"><span data-stu-id="7ec8c-170">On the **Proxy Configuration** tab, specify proxy server information.</span></span>

    ![Rejestracja agenta MARS](./media/vmm-to-azure-walkthrough-source-target/mars-proxy.png)
4. <span data-ttu-id="7ec8c-172">Upewnij się, że agent może osiągnąć adresy URL opisane w [wymaganiach wstępnych](#on-premises-prerequisites).</span><span class="sxs-lookup"><span data-stu-id="7ec8c-172">Check that the agent can reach the URLs described in the [prerequisites](#on-premises-prerequisites).</span></span>

## <a name="set-up-the-target-environment"></a><span data-ttu-id="7ec8c-173">Konfigurowanie środowiska docelowego</span><span class="sxs-lookup"><span data-stu-id="7ec8c-173">Set up the target environment</span></span>
<span data-ttu-id="7ec8c-174">Określ konto magazynu Azure do wykorzystania podczas replikacji i sieć platformy Azure, z którą maszyny wirtualne Azure będą się łączyć po przejściu w tryb failover.</span><span class="sxs-lookup"><span data-stu-id="7ec8c-174">Specify the Azure storage account to be used for replication, and the Azure network to which Azure VMs will connect after failover.</span></span>

1. <span data-ttu-id="7ec8c-175">Kliknij pozycję **Przygotowywanie infrastruktury** > **Cel**, a następnie wybierz subskrypcję i grupę zasobów, w której chcesz utworzyć maszyny wirtualne w trybie failover.</span><span class="sxs-lookup"><span data-stu-id="7ec8c-175">Click **Prepare infrastructure** > **Target**, select the subscription and the resource group where you want to create the failed over virtual machines.</span></span> <span data-ttu-id="7ec8c-176">Wybierz model wdrażania, którego chcesz użyć na platformie Azure (model usługi Resource Manager lub model klasyczny) dla maszyn wirtualnych w trybie failover.</span><span class="sxs-lookup"><span data-stu-id="7ec8c-176">Choose the deployment model that you want to use in Azure (classic or resource management) for the failed over virtual machines.</span></span>

    ![Magazyn](./media/vmm-to-azure-walkthrough-source-target/enablerep3.png)

2. <span data-ttu-id="7ec8c-178">Usługa Site Recovery sprawdza, czy masz co najmniej jedno zgodne konto magazynu Azure i co najmniej jedną sieć platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="7ec8c-178">Site Recovery checks that you have one or more compatible Azure storage accounts and networks.</span></span>

    ![Magazyn](./media/vmm-to-azure-walkthrough-source-target/compatible-storage.png)

3. <span data-ttu-id="7ec8c-180">Jeśli nie utworzono konta magazynu, a chcesz je utworzyć przy użyciu usługi Resource Manager, kliknij pozycję **+ Konto magazynu**, aby zrobić to w tym miejscu.</span><span class="sxs-lookup"><span data-stu-id="7ec8c-180">If you haven't created a storage account, and you want to create one using Resource Manager, click **+Storage account** to do that inline.</span></span>  <span data-ttu-id="7ec8c-181">W bloku **Utwórz konto magazynu** określ nazwę konta, jego typ, subskrypcję i lokalizację.</span><span class="sxs-lookup"><span data-stu-id="7ec8c-181">On the **Create storage account** blade specify an account name, type, subscription, and location.</span></span> <span data-ttu-id="7ec8c-182">Konto powinno znajdować się w tej samej lokalizacji co magazyn Usług odzyskiwania.</span><span class="sxs-lookup"><span data-stu-id="7ec8c-182">The account should be in the same location as the Recovery Services vault.</span></span>

   ![Magazyn](./media/vmm-to-azure-walkthrough-source-target/gs-createstorage.png)


   * <span data-ttu-id="7ec8c-184">Jeśli chcesz utworzyć konto magazynu przy użyciu modelu klasycznego, należy to zrobić w witrynie Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="7ec8c-184">If you want to create a storage account using the classic model, do that in the Azure portal.</span></span> [<span data-ttu-id="7ec8c-185">Dowiedz się więcej</span><span class="sxs-lookup"><span data-stu-id="7ec8c-185">Learn more</span></span>](../storage/common/storage-create-storage-account.md)
   * <span data-ttu-id="7ec8c-186">Jeśli używasz konta usługi Premium Storage dla replikowanych danych, skonfiguruj dodatkowe, standardowe konto magazynu do przechowywania dzienników replikacji, które przechwytują zachodzące zmiany w danych lokalnych.</span><span class="sxs-lookup"><span data-stu-id="7ec8c-186">If you’re using a premium storage account for replicated data, set up an additional standard storage account, to store replication logs that capture ongoing changes to on-premises data.</span></span>
5. <span data-ttu-id="7ec8c-187">Jeśli nie utworzono sieci platformy Azure, a chcesz ją utworzyć przy użyciu usługi Resource Manager, kliknij pozycję **+ Sieć**, aby zrobić to w tym miejscu.</span><span class="sxs-lookup"><span data-stu-id="7ec8c-187">If you haven't created an Azure network, and you want to create one using Resource Manager, click **+Network** to do that inline.</span></span> <span data-ttu-id="7ec8c-188">W bloku **Utwórz sieć wirtualną** określ nazwę sieciową, zakres adresów, szczegóły podsieci, subskrypcję i lokalizację.</span><span class="sxs-lookup"><span data-stu-id="7ec8c-188">On the **Create virtual network** blade specify a network name, address range, subnet details, subscription, and location.</span></span> <span data-ttu-id="7ec8c-189">Sieć powinna znajdować się w tej samej lokalizacji co magazyn Usług odzyskiwania.</span><span class="sxs-lookup"><span data-stu-id="7ec8c-189">The network should be in the same location as the Recovery Services vault.</span></span>

   ![Sieć](./media/vmm-to-azure-walkthrough-source-target/gs-createnetwork.png)

   <span data-ttu-id="7ec8c-191">Jeśli chcesz utworzyć sieć przy użyciu modelu klasycznego, zrób to w witrynie Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="7ec8c-191">If you want to create a network using the classic model, do that in the Azure portal.</span></span> <span data-ttu-id="7ec8c-192">[Dowiedz się więcej](../virtual-network/virtual-networks-create-vnet-classic-pportal.md).</span><span class="sxs-lookup"><span data-stu-id="7ec8c-192">[Learn more](../virtual-network/virtual-networks-create-vnet-classic-pportal.md).</span></span>





## <a name="next-steps"></a><span data-ttu-id="7ec8c-193">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="7ec8c-193">Next steps</span></span>

<span data-ttu-id="7ec8c-194">Przejdź do [krok 9: Konfigurowanie mapowania sieci](vmm-to-azure-walkthrough-network-mapping.md)</span><span class="sxs-lookup"><span data-stu-id="7ec8c-194">Go to [Step 9: Configure network mapping](vmm-to-azure-walkthrough-network-mapping.md)</span></span>
