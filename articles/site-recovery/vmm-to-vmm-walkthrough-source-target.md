---
title: "aaaSet hello źródłowego i docelowego dla lokacji dodatkowej tooa replikacji funkcji Hyper-V z usługą Azure Site Recovery | Dokumentacja firmy Microsoft"
description: "Opisuje sposób tooset Konfigurowanie hello źródłowego i docelowego podczas replikowania maszyn wirtualnych funkcji Hyper-V toosecondary VMM lokacji z usługi Azure Site Recovery."
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: fa7809f1-7633-425f-b25d-d10d004e8d0b
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/30/2017
ms.author: raynew
ms.openlocfilehash: 451cb4413ca5c09777a7faf512b1c8ea43e695f7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="step-6-set-up-hello-replication-source-and-target"></a><span data-ttu-id="471f3-103">Krok 6: Konfigurowanie hello replikacji źródłowa i docelowa</span><span class="sxs-lookup"><span data-stu-id="471f3-103">Step 6: Set up hello replication source and target</span></span>


<span data-ttu-id="471f3-104">Po utworzeniu usługi odzyskiwania magazynu dla funkcji Hyper-V replikacji tooa lokacja dodatkowa programu VMM z [usługi Azure Site Recovery](site-recovery-overview.md), użyj tego artykułu tooset hello źródła i docelowe lokalizacje replikacji.</span><span class="sxs-lookup"><span data-stu-id="471f3-104">After creating a Recovery Services vault for Hyper-V replication tooa secondary VMM site with [Azure Site Recovery](site-recovery-overview.md), use this article tooset up hello source and target replication locations.</span></span> 

<span data-ttu-id="471f3-105">Po przeczytaniu tego artykułu, post wszelkie komentarze u dołu hello, lub na powitania [Forum usług odzyskiwania Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="471f3-105">After reading this article, post any comments at hello bottom, or on hello [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>




## <a name="set-up-hello-source-environment"></a><span data-ttu-id="471f3-106">Konfigurowanie środowiska źródłowego hello</span><span class="sxs-lookup"><span data-stu-id="471f3-106">Set up hello source environment</span></span>

<span data-ttu-id="471f3-107">Zainstalować hello dostawcy usługi Azure Site Recovery na serwerach VMM i Odnajdź i Zarejestruj serwer w magazynie hello.</span><span class="sxs-lookup"><span data-stu-id="471f3-107">Install hello Azure Site Recovery Provider on VMM servers, and discover and register servers in hello vault.</span></span>

1. <span data-ttu-id="471f3-108">Kliknij przycisk **krok 1: Przygotowanie infrastruktury** > **źródła**.</span><span class="sxs-lookup"><span data-stu-id="471f3-108">Click **Step 1: Prepare Infrastructure** > **Source**.</span></span>

    ![Konfiguracja źródła](./media/vmm-to-vmm-walkthrough-source-target/goals-source.png)
2. <span data-ttu-id="471f3-110">W **Przygotuj źródło**, kliknij przycisk **+ VMM** tooadd serwera programu VMM.</span><span class="sxs-lookup"><span data-stu-id="471f3-110">In **Prepare source**, click **+ VMM** tooadd a VMM server.</span></span>

    ![Konfiguracja źródła](./media/vmm-to-vmm-walkthrough-source-target/set-source1.png)
3. <span data-ttu-id="471f3-112">W **Dodaj serwer**, sprawdź, czy **serwera programu System Center VMM** pojawia się w **typ serwera** , że serwer VMM hello spełnia hello [wymagania wstępne](#prerequisites).</span><span class="sxs-lookup"><span data-stu-id="471f3-112">In **Add Server**, check that **System Center VMM server** appears in **Server type** and that hello VMM server meets hello [prerequisites](#prerequisites).</span></span>
4. <span data-ttu-id="471f3-113">Pobierz plik instalacyjny dostawcy usługi Azure Site Recovery hello.</span><span class="sxs-lookup"><span data-stu-id="471f3-113">Download hello Azure Site Recovery Provider installation file.</span></span>
5. <span data-ttu-id="471f3-114">Pobierz klucz rejestracji hello.</span><span class="sxs-lookup"><span data-stu-id="471f3-114">Download hello registration key.</span></span> <span data-ttu-id="471f3-115">Będzie on potrzebny po uruchomieniu Instalatora.</span><span class="sxs-lookup"><span data-stu-id="471f3-115">You need this when you run setup.</span></span> <span data-ttu-id="471f3-116">klucz Hello jest ważny przez pięć dni po jego wygenerowaniu.</span><span class="sxs-lookup"><span data-stu-id="471f3-116">hello key is valid for five days after you generate it.</span></span>

    ![Konfiguracja źródła](./media/vmm-to-vmm-walkthrough-source-target/set-source3.png)
6. <span data-ttu-id="471f3-118">Zainstaluj hello dostawcy usługi Azure Site Recovery na serwerze VMM hello.</span><span class="sxs-lookup"><span data-stu-id="471f3-118">Install hello Azure Site Recovery Provider on hello VMM server.</span></span> <span data-ttu-id="471f3-119">Nie ma potrzeby tooexplicitly należy już nic instalować na serwerach hostów funkcji Hyper-V.</span><span class="sxs-lookup"><span data-stu-id="471f3-119">You don't need tooexplicitly install anything on Hyper-V host servers.</span></span>


## <a name="install-hello-azure-site-recovery-provider"></a><span data-ttu-id="471f3-120">Zainstaluj hello dostawcy usługi Azure Site Recovery</span><span class="sxs-lookup"><span data-stu-id="471f3-120">Install hello Azure Site Recovery Provider</span></span>

1. <span data-ttu-id="471f3-121">Uruchom plik Instalatora dostawcy hello na każdym serwerze programu VMM.</span><span class="sxs-lookup"><span data-stu-id="471f3-121">Run hello Provider setup file on each VMM server.</span></span> <span data-ttu-id="471f3-122">Jeśli program VMM jest wdrożony w klastrze, wykonaj powitania po pierwszym instalowanym hello:</span><span class="sxs-lookup"><span data-stu-id="471f3-122">If VMM is deployed in a cluster, do hello following hello first time you install:</span></span>
    -  <span data-ttu-id="471f3-123">Zainstaluj dostawcę hello na aktywnym węźle i Zakończ hello instalacji tooregister hello serwer VMM w magazynie hello.</span><span class="sxs-lookup"><span data-stu-id="471f3-123">Install hello provider on an active node, and finish hello installation tooregister hello VMM server in hello vault.</span></span>
    - <span data-ttu-id="471f3-124">Następnie należy zainstalować hello dostawcy na powitania innych węzłów.</span><span class="sxs-lookup"><span data-stu-id="471f3-124">Then, install hello Provider on hello other nodes.</span></span> <span data-ttu-id="471f3-125">Węzły klastra należy uruchomić hello tę samą wersję programu hello dostawcy.</span><span class="sxs-lookup"><span data-stu-id="471f3-125">Cluster nodes should all run hello same version of hello Provider.</span></span>
2. <span data-ttu-id="471f3-126">Instalator uruchamia kilka wymagań wstępnych i żądania usługi VMM hello toostop uprawnienia.</span><span class="sxs-lookup"><span data-stu-id="471f3-126">Setup runs a few prerequisite checks, and requests permission toostop hello VMM service.</span></span> <span data-ttu-id="471f3-127">Witaj usługi programu VMM zostanie automatycznie uruchomiona po zakończeniu instalacji.</span><span class="sxs-lookup"><span data-stu-id="471f3-127">hello VMM service will be restarted automatically when setup finishes.</span></span> <span data-ttu-id="471f3-128">Po zainstalowaniu na klastrze programu VMM, możesz roli klastra hello toostop zostanie wyświetlony monit o.</span><span class="sxs-lookup"><span data-stu-id="471f3-128">If you install on a VMM cluster, you're prompted toostop hello Cluster role.</span></span>
3. <span data-ttu-id="471f3-129">W **Microsoft Update**, można włączyć toospecify czy aktualizacje dostawcy były instalowane zgodnie z zasadami Microsoft Update.</span><span class="sxs-lookup"><span data-stu-id="471f3-129">In **Microsoft Update**, you can opt in toospecify that provider updates are installed in accordance with your Microsoft Update policy.</span></span>
4. <span data-ttu-id="471f3-130">W **instalacji**, Zaakceptuj lub zmodyfikuj hello domyślna lokalizacja instalacji, a następnie kliknij przycisk **zainstalować**.</span><span class="sxs-lookup"><span data-stu-id="471f3-130">In **Installation**, accept or modify hello default installation location, and click **Install**.</span></span>

    ![Lokalizacja instalacji](./media/vmm-to-vmm-walkthrough-source-target/provider-location.png)
5. <span data-ttu-id="471f3-132">Po zakończeniu instalacji kliknij przycisk **zarejestrować** tooregister powitania serwera w magazynie hello.</span><span class="sxs-lookup"><span data-stu-id="471f3-132">After installation is complete, click **Register** tooregister hello server in hello vault.</span></span>

    ![Lokalizacja instalacji](./media/vmm-to-vmm-walkthrough-source-target/provider-register.png)
6. <span data-ttu-id="471f3-134">W **nazwę magazynu**, sprawdź nazwę hello hello magazynu, w którym hello serwer zostanie zarejestrowany.</span><span class="sxs-lookup"><span data-stu-id="471f3-134">In **Vault name**, verify hello name of hello vault in which hello server will be registered.</span></span> <span data-ttu-id="471f3-135">Kliknij przycisk *Dalej*.</span><span class="sxs-lookup"><span data-stu-id="471f3-135">Click *Next*.</span></span>

    ![Rejestracja serwera](./media/vmm-to-vmm-walkthrough-source-target/vaultcred.png)
7. <span data-ttu-id="471f3-137">W **połączenia internetowego**, określ, jak dostawca hello uruchomiony na serwerze VMM hello łączy tooAzure.</span><span class="sxs-lookup"><span data-stu-id="471f3-137">In **Internet Connection**, specify how hello provider running on hello VMM server connects tooAzure.</span></span>

    ![Ustawienia internetowe](./media/vmm-to-vmm-walkthrough-source-target/proxydetails.png)

   - <span data-ttu-id="471f3-139">Można określić, tego dostawcy hello należy łączyć bezpośrednio toohello internet, lub za pośrednictwem serwera proxy.</span><span class="sxs-lookup"><span data-stu-id="471f3-139">You can specify that hello provider should connect directly toohello internet, or via a proxy.</span></span>
   - <span data-ttu-id="471f3-140">Określ ustawienia serwera proxy, jeśli to konieczne.</span><span class="sxs-lookup"><span data-stu-id="471f3-140">Specify proxy settings if needed.</span></span>
   - <span data-ttu-id="471f3-141">Jeśli używasz serwera proxy konto Uruchom jako programu VMM (DRAProxyAccount) jest tworzony automatycznie przy użyciu hello określonych poświadczeń serwera proxy.</span><span class="sxs-lookup"><span data-stu-id="471f3-141">If you use a proxy, a VMM RunAs account (DRAProxyAccount) is created automatically using hello specified proxy credentials.</span></span> <span data-ttu-id="471f3-142">Konfiguracja serwera proxy hello, dzięki czemu to konto mogło być pomyślnie uwierzytelnione.</span><span class="sxs-lookup"><span data-stu-id="471f3-142">Configure hello proxy server so that this account can authenticate successfully.</span></span> <span data-ttu-id="471f3-143">Witaj ustawienia konta Uruchom jako można modyfikować w konsoli programu VMM hello > **ustawienia** > **zabezpieczeń** > **konta Uruchom jako**.</span><span class="sxs-lookup"><span data-stu-id="471f3-143">hello RunAs account settings can be modified in hello VMM console > **Settings** > **Security** > **Run As Accounts**.</span></span> <span data-ttu-id="471f3-144">Uruchom ponownie zmiany tooupdate usługi VMM hello.</span><span class="sxs-lookup"><span data-stu-id="471f3-144">Restart hello VMM service tooupdate changes.</span></span>
8. <span data-ttu-id="471f3-145">W **klucz rejestracji**, zaznacz klucz hello pobrany z usługi Azure Site Recovery, a następnie skopiować toohello serwera VMM.</span><span class="sxs-lookup"><span data-stu-id="471f3-145">In **Registration Key**, select hello key that you downloaded from Azure Site Recovery and copied toohello VMM server.</span></span>
9. <span data-ttu-id="471f3-146">ustawienie szyfrowania Hello jest używana tylko w przypadku replikacji maszyn wirtualnych funkcji Hyper-V w tooAzure chmur programu VMM.</span><span class="sxs-lookup"><span data-stu-id="471f3-146">hello encryption setting is only used when you're replicating Hyper-V VMs in VMM clouds tooAzure.</span></span> <span data-ttu-id="471f3-147">Jeśli replikujesz tooa lokacji dodatkowej nie jest używane.</span><span class="sxs-lookup"><span data-stu-id="471f3-147">If you're replicating tooa secondary site it's not used.</span></span>
10. <span data-ttu-id="471f3-148">W **nazwy serwera**, określ serwer VMM hello tooidentify przyjazną nazwę w magazynie hello.</span><span class="sxs-lookup"><span data-stu-id="471f3-148">In **Server name**, specify a friendly name tooidentify hello VMM server in hello vault.</span></span> <span data-ttu-id="471f3-149">W konfiguracji klastra Określ nazwę roli klastra VMM hello.</span><span class="sxs-lookup"><span data-stu-id="471f3-149">In a cluster configuration specify hello VMM cluster role name.</span></span>
11. <span data-ttu-id="471f3-150">W **Synchronizuj metadane chmury**, wybierz, czy dla wszystkich chmur na powitania serwera VMM w magazynie hello toosynchronize metadanych.</span><span class="sxs-lookup"><span data-stu-id="471f3-150">In **Synchronize cloud metadata**, select whether you want toosynchronize metadata for all clouds on hello VMM server with hello vault.</span></span> <span data-ttu-id="471f3-151">Ta akcja wymaga tylko toohappen raz na każdym serwerze.</span><span class="sxs-lookup"><span data-stu-id="471f3-151">This action only needs toohappen once on each server.</span></span> <span data-ttu-id="471f3-152">Jeśli nie chcesz toosynchronize wszystkich chmur, można zaznaczać tego ustawienia i synchronizować poszczególne chmury indywidualnie WE hello właściwości chmury w konsoli programu VMM hello.</span><span class="sxs-lookup"><span data-stu-id="471f3-152">If you don't want toosynchronize all clouds, you can leave this setting unchecked, and synchronize each cloud individually in hello cloud properties in hello VMM console.</span></span>
12. <span data-ttu-id="471f3-153">Kliknij przycisk **dalej** toocomplete hello procesu.</span><span class="sxs-lookup"><span data-stu-id="471f3-153">Click **Next** toocomplete hello process.</span></span> <span data-ttu-id="471f3-154">Po rejestracji metadane z serwera VMM hello są pobierane przez usługę Azure Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="471f3-154">After registration, metadata from hello VMM server is retrieved by Azure Site Recovery.</span></span> <span data-ttu-id="471f3-155">Serwer Hello jest wyświetlany na powitania **serwery VMM** kartę na powitania **serwerów** strony w magazynie hello.</span><span class="sxs-lookup"><span data-stu-id="471f3-155">hello server is displayed on hello **VMM Servers** tab on hello **Servers** page in hello vault.</span></span>

    ![Serwer](./media/vmm-to-vmm-walkthrough-source-target/provider13.png)
13. <span data-ttu-id="471f3-157">Po hello serwer jest dostępny w konsoli usługi Site Recovery hello w **źródła** > **Przygotuj źródło** wybierz serwer VMM hello i wybierz hello chmury, w których hello funkcji Hyper-V znajduje się host.</span><span class="sxs-lookup"><span data-stu-id="471f3-157">After hello server is available in hello Site Recovery console, in **Source** > **Prepare source** select hello VMM server, and select hello cloud in which hello Hyper-V host is located.</span></span> <span data-ttu-id="471f3-158">Następnie kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="471f3-158">Then click **OK**.</span></span>

<span data-ttu-id="471f3-159">Dostawca hello można także zainstalować z wiersza polecenia hello:</span><span class="sxs-lookup"><span data-stu-id="471f3-159">You can also install hello provider from hello command line:</span></span>

[!INCLUDE [site-recovery-rw-provider-command-line](../../includes/site-recovery-rw-provider-command-line.md)]


## <a name="set-up-hello-target-environment"></a><span data-ttu-id="471f3-160">Konfigurowanie środowiska docelowego hello</span><span class="sxs-lookup"><span data-stu-id="471f3-160">Set up hello target environment</span></span>

<span data-ttu-id="471f3-161">Wybierz hello docelowym serwerze VMM i w chmurze:</span><span class="sxs-lookup"><span data-stu-id="471f3-161">Select hello target VMM server and cloud:</span></span>

1. <span data-ttu-id="471f3-162">Kliknij przycisk **przygotowanie infrastruktury** > **docelowego**i wybierz hello docelowym serwerze VMM ma toouse.</span><span class="sxs-lookup"><span data-stu-id="471f3-162">Click **Prepare infrastructure** > **Target**, and select hello target VMM server you want toouse.</span></span>
2. <span data-ttu-id="471f3-163">Pojawi się na serwerze hello chmury, które są synchronizowane z usługą Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="471f3-163">Clouds on hello server that are synchronized with Site Recovery will be displayed.</span></span> <span data-ttu-id="471f3-164">Wybierz chmurę docelową hello.</span><span class="sxs-lookup"><span data-stu-id="471f3-164">Select hello target cloud.</span></span>

   ![docelowy](./media/vmm-to-vmm-walkthrough-source-target/target-vmm.png)



## <a name="next-steps"></a><span data-ttu-id="471f3-166">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="471f3-166">Next steps</span></span>

<span data-ttu-id="471f3-167">Przejdź za[kroku 7: Konfigurowanie mapowania sieci](vmm-to-vmm-walkthrough-network-mapping.md).</span><span class="sxs-lookup"><span data-stu-id="471f3-167">Go too[Step 7: Configure network mapping](vmm-to-vmm-walkthrough-network-mapping.md).</span></span>
