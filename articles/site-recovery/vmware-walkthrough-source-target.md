---
title: "aaaSet hello źródła i celu tooAzure replikacji VMware z usługą Azure Site Recovery | Dokumentacja firmy Microsoft"
description: "Podsumowanie tooset kroki hello źródłowa i docelowa ustawień replikacji maszyn wirtualnych VMware tooAzure magazynu z usługą Azure Site Recovery"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: d99e422e-daf7-4fa8-af3c-af2340340136
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/27/2017
ms.author: raynew
ms.openlocfilehash: ef33a44bc5da17afb0442be63f576925f5b9a8b2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="step-8-set-up-hello-source-and-target-for-vmware-replication-tooazure"></a><span data-ttu-id="20822-103">Krok 8: Konfigurowanie hello źródłowa i docelowa dla tooAzure replikacji VMware</span><span class="sxs-lookup"><span data-stu-id="20822-103">Step 8: Set up hello source and target for VMware replication tooAzure</span></span>

<span data-ttu-id="20822-104">W tym artykule opisano sposób tooconfigure źródłowa i docelowa ustawień podczas replikowania lokalnie tooAzure maszyny wirtualne VMware, za pomocą hello [usługi Azure Site Recovery](site-recovery-overview.md) w hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="20822-104">This article describes how tooconfigure source and target settings when replicating on-premises VMware virtual machines tooAzure, using hello [Azure Site Recovery](site-recovery-overview.md) service in hello Azure portal.</span></span>

<span data-ttu-id="20822-105">Opublikuj komentarze i pytania u dołu hello w tym artykule, albo na powitania [Forum usług odzyskiwania Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="20822-105">Post comments and questions at hello bottom of this article, or on hello [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>


## <a name="set-up-hello-source-environment"></a><span data-ttu-id="20822-106">Konfigurowanie środowiska źródłowego hello</span><span class="sxs-lookup"><span data-stu-id="20822-106">Set up hello source environment</span></span>

<span data-ttu-id="20822-107">Konfigurowanie serwera konfiguracji hello, zarejestruj go w magazynie hello i odnajdywanie maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="20822-107">Set up hello configuration server, register it in hello vault, and discover VMs.</span></span>

1. <span data-ttu-id="20822-108">Kliknij przycisk **lokacji odzyskiwania** > **krok 1: Przygotowanie infrastruktury** > **źródła**.</span><span class="sxs-lookup"><span data-stu-id="20822-108">Click **Site Recovery** > **Step 1: Prepare Infrastructure** > **Source**.</span></span>
2. <span data-ttu-id="20822-109">Jeśli nie masz serwera konfiguracji, kliknij przycisk **+ serwer konfiguracji**.</span><span class="sxs-lookup"><span data-stu-id="20822-109">If you don’t have a configuration server, click **+Configuration server**.</span></span>
3. <span data-ttu-id="20822-110">W **Dodaj serwer**, sprawdź, czy **serwera konfiguracji** pojawia się w **typ serwera**.</span><span class="sxs-lookup"><span data-stu-id="20822-110">In **Add Server**, check that **Configuration Server** appears in **Server type**.</span></span>
4. <span data-ttu-id="20822-111">Pobierz plik instalacyjny instalacja Unified usługi Site Recovery hello.</span><span class="sxs-lookup"><span data-stu-id="20822-111">Download hello Site Recovery Unified Setup installation file.</span></span>
5. <span data-ttu-id="20822-112">Pobierz klucz rejestracji magazynu hello.</span><span class="sxs-lookup"><span data-stu-id="20822-112">Download hello vault registration key.</span></span> <span data-ttu-id="20822-113">Należy to po uruchomieniu Instalatora Unified.</span><span class="sxs-lookup"><span data-stu-id="20822-113">You need this when you run Unified Setup.</span></span> <span data-ttu-id="20822-114">klucz Hello jest ważny przez pięć dni po jego wygenerowaniu.</span><span class="sxs-lookup"><span data-stu-id="20822-114">hello key is valid for five days after you generate it.</span></span>

   ![Konfiguracja źródła](./media/vmware-walkthrough-source-target/set-source2.png)


## <a name="register-hello-configuration-server-in-hello-vault"></a><span data-ttu-id="20822-116">Zarejestruj serwer konfiguracji hello w magazynie hello</span><span class="sxs-lookup"><span data-stu-id="20822-116">Register hello configuration server in hello vault</span></span>

<span data-ttu-id="20822-117">Następujące hello przed start, a następnie uruchom serwer konfiguracji hello tooinstall Unified instalacji, powitania serwera przetwarzania i hello główny serwer docelowy.</span><span class="sxs-lookup"><span data-stu-id="20822-117">Do hello following before you start, then run Unified Setup tooinstall hello configuration server, hello process server, and hello master target server.</span></span>
    - <span data-ttu-id="20822-118">Uzyskać szybkie omówienie wideo</span><span class="sxs-lookup"><span data-stu-id="20822-118">Get a quick video overview</span></span>

        > [!VIDEO https://channel9.msdn.com/Series/Azure-Site-Recovery/VMware-to-Azure-with-ASR-Video1-Source-Infrastructure-Setup/player]

    - <span data-ttu-id="20822-119">Upewnij się, że hello zegar systemowy jest zsynchronizowany z na powitania serwera konfiguracji maszyny Wirtualnej, [serwer czasu](https://technet.microsoft.com/windows-server-docs/identity/ad-ds/get-started/windows-time-service/windows-time-service).</span><span class="sxs-lookup"><span data-stu-id="20822-119">On hello configuration server VM, make sure that hello system clock is synchronized with a [Time Server](https://technet.microsoft.com/windows-server-docs/identity/ad-ds/get-started/windows-time-service/windows-time-service).</span></span> <span data-ttu-id="20822-120">Powinna być zgodna.</span><span class="sxs-lookup"><span data-stu-id="20822-120">It should match.</span></span> <span data-ttu-id="20822-121">Jeśli jest 15 minut przed lub za, Instalator może zakończyć się niepowodzeniem.</span><span class="sxs-lookup"><span data-stu-id="20822-121">If it's 15 minutes in front or behind, setup might fail.</span></span>
    - <span data-ttu-id="20822-122">Uruchom instalację jako Administrator lokalny na serwerze konfiguracji hello maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="20822-122">Run setup as a Local Administrator on hello configuration server VM.</span></span>
    - <span data-ttu-id="20822-123">Upewnij się, że włączono protokołu TLS 1.0 na powitania maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="20822-123">Make sure TLS 1.0 is enabled on hello VM.</span></span>


[!INCLUDE [site-recovery-add-configuration-server](../../includes/site-recovery-add-configuration-server.md)]

> [!NOTE]
> <span data-ttu-id="20822-124">można również zainstalować serwer konfiguracji Hello [z wiersza polecenia hello](http://aka.ms/installconfigsrv).</span><span class="sxs-lookup"><span data-stu-id="20822-124">hello configuration server can also be installed [from hello command line](http://aka.ms/installconfigsrv).</span></span>



## <a name="connect-toovmware-servers"></a><span data-ttu-id="20822-125">Połącz serwery tooVMware</span><span class="sxs-lookup"><span data-stu-id="20822-125">Connect tooVMware servers</span></span>

<span data-ttu-id="20822-126">tooallow usługi Azure Site Recovery toodiscover maszyn wirtualnych działających w środowisku lokalnym, potrzebujesz tooconnect Twojego programu VMware vCenter Server lub hostach ESXi vSphere z usługą Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="20822-126">tooallow Azure Site Recovery toodiscover virtual machines running in your on-premises environment, you need tooconnect your VMware vCenter Server or vSphere ESXi hosts with Site Recovery.</span></span> <span data-ttu-id="20822-127">Przed rozpoczęciem należy zwrócić uwagę hello poniżej:</span><span class="sxs-lookup"><span data-stu-id="20822-127">Note hello following before you start:</span></span>

- <span data-ttu-id="20822-128">Po dodaniu serwera vCenter hello lub tooSite hostami vSphere odzyskiwania przy użyciu konta bez uprawnień administratora na serwerze hello hello konto na potrzeby następujące uprawnienia:</span><span class="sxs-lookup"><span data-stu-id="20822-128">If you add hello vCenter server or vSphere hosts tooSite Recovery with an account without administrator privileges on hello server, hello account needs these privileges enabled:</span></span>
    - <span data-ttu-id="20822-129">Centrum danych, Magazyn danych, Folder, hosta, sieci, zasobów, wirtualnej maszyny, vSphere rozproszonego przełącznika.</span><span class="sxs-lookup"><span data-stu-id="20822-129">Datacenter, Datastore, Folder, Host, Network, Resource, Virtual machine, vSphere Distributed Switch.</span></span>
    - <span data-ttu-id="20822-130">Serwer vCenter Hello musi mieć uprawnienia widoków magazynu.</span><span class="sxs-lookup"><span data-stu-id="20822-130">hello vCenter server needs Storage views permissions.</span></span>
- <span data-ttu-id="20822-131">Po dodaniu tooSite serwerów VMware odzyskiwania może zająć 15 minut lub dłużej, aby je tooappear w portalu hello.</span><span class="sxs-lookup"><span data-stu-id="20822-131">When you add VMware servers tooSite Recovery, it can take 15 minutes or longer for them tooappear in hello portal.</span></span>

### <a name="add-hello-account-for-automatic-discovery"></a><span data-ttu-id="20822-132">Dodaj konto hello automatycznego wykrywania</span><span class="sxs-lookup"><span data-stu-id="20822-132">Add hello account for automatic discovery</span></span>

[!INCLUDE [site-recovery-add-vcenter-account](../../includes/site-recovery-add-vcenter-account.md)]

### <a name="set-up-a-connection"></a><span data-ttu-id="20822-133">Konfigurowanie połączenia</span><span class="sxs-lookup"><span data-stu-id="20822-133">Set up a connection</span></span>

<span data-ttu-id="20822-134">Połącz tooservers w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="20822-134">Connect tooservers as follows:</span></span>

1. <span data-ttu-id="20822-135">Wybierz **+ vCenter** toostart łączenie programu VMware vCenter server lub VMware vSphere ESXi hosta.</span><span class="sxs-lookup"><span data-stu-id="20822-135">Select **+vCenter** toostart connecting a VMware vCenter server or a VMware vSphere ESXi host.</span></span>
2. <span data-ttu-id="20822-136">W **dodać vCenter**, określ przyjazną nazwę dla serwera hosta lub vCenter vSphere hello, a następnie określ hello adres IP lub nazwę FQDN serwera hello.</span><span class="sxs-lookup"><span data-stu-id="20822-136">In **Add vCenter**, specify a friendly name for hello vSphere host or vCenter server, and then specify hello IP address or FQDN of hello server.</span></span>
3. <span data-ttu-id="20822-137">Pozostaw hello portu 443, chyba że VMware serwery są skonfigurowane toolisten na innym porcie żądań.</span><span class="sxs-lookup"><span data-stu-id="20822-137">Leave hello port as 443 unless your VMware servers are configured toolisten for requests on a different port.</span></span> <span data-ttu-id="20822-138">Wybierz konto hello tooconnect toohello VMware vCenter lub vSphere ESXi serwera.</span><span class="sxs-lookup"><span data-stu-id="20822-138">Select hello account that is tooconnect toohello VMware vCenter or vSphere ESXi server.</span></span> <span data-ttu-id="20822-139">Kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="20822-139">Click **OK**.</span></span>
4. <span data-ttu-id="20822-140">Usługa Site Recovery łączy serwery tooVMware przy użyciu hello określone ustawienia i odnajduje maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="20822-140">Site Recovery connects tooVMware servers using hello specified settings, and discovers VMs.</span></span>

> [!NOTE]
> <span data-ttu-id="20822-141">W przypadku dodawania serwera lub hosta przy użyciu konta, który nie ma uprawnień administratora na serwerze vCenter lub hosta hello, upewnij się, że konto hello ma te uprawnienia: centrum danych, Magazyn danych, Folder, hosta, sieci, zasobów, w przypadku maszyny wirtualnej i vSphere rozproszonego przełącznika.</span><span class="sxs-lookup"><span data-stu-id="20822-141">If you're adding a server or host with an account that doesn't have administrator privileges on hello vCenter or host server, make sure that hello account has these privileges enabled: Datacenter, Datastore, Folder, Host, Network, Resource, Virtual machine, and vSphere Distributed Switch.</span></span> <span data-ttu-id="20822-142">Ponadto hello programu VMware vCenter server musi widoków magazynu hello włączone uprawnienia.</span><span class="sxs-lookup"><span data-stu-id="20822-142">In addition, hello VMware vCenter server needs hello Storage Views privilege enabled.</span></span>


## <a name="set-up-hello-target-environment"></a><span data-ttu-id="20822-143">Konfigurowanie środowiska docelowego hello</span><span class="sxs-lookup"><span data-stu-id="20822-143">Set up hello target environment</span></span>

<span data-ttu-id="20822-144">Aby skonfigurować środowisko docelowe hello, upewnij się, że masz konto magazynu Azure i konfigurowanie sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="20822-144">Before you set up hello target environment, make sure you have an Azure storage account and virtual network set up.</span></span>

1. <span data-ttu-id="20822-145">Kliknij przycisk **przygotowanie infrastruktury** > **docelowego**, i wybierz hello ma toouse subskrypcji platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="20822-145">Click **Prepare infrastructure** > **Target**, and select hello Azure subscription you want toouse.</span></span>
2. <span data-ttu-id="20822-146">Określ, czy docelowy modelu wdrażania jest oparte na Menedżera zasobów albo klasycznego.</span><span class="sxs-lookup"><span data-stu-id="20822-146">Specify whether your target deployment model is Resource Manager-based, or classic.</span></span>
3. <span data-ttu-id="20822-147">Usługa Site Recovery sprawdza, czy masz co najmniej jedno zgodne konto magazynu Azure i co najmniej jedną sieć platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="20822-147">Site Recovery checks that you have one or more compatible Azure storage accounts and networks.</span></span>

   ![docelowy](./media/vmware-walkthrough-source-target/gs-target.png)
4. <span data-ttu-id="20822-149">Jeśli nie utworzono konta magazynu lub sieci, kliknij przycisk **+ konto magazynu** lub **+ sieć**, toocreate wbudowanego konta lub sieci Menedżera zasobów.</span><span class="sxs-lookup"><span data-stu-id="20822-149">If you haven't created a storage account or network, click **+Storage account** or **+Network**, toocreate a Resource Manager account or network inline.</span></span>

## <a name="next-steps"></a><span data-ttu-id="20822-150">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="20822-150">Next steps</span></span>

<span data-ttu-id="20822-151">Przejdź do zbyt[krok 9: Konfigurowanie zasad replikacji](vmware-walkthrough-replication.md)</span><span class="sxs-lookup"><span data-stu-id="20822-151">Go too[Step 9: Set up a replication policy](vmware-walkthrough-replication.md)</span></span>
