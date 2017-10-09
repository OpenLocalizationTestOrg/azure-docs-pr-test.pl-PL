---
title: "serwery aaaRemove i Wyłącz ochronę | Dokumentacja firmy Microsoft"
description: "W tym artykule opisano, jak magazyn toounregister serwerów z usługi Site Recovery i toodisable ochrony dla maszyn wirtualnych i serwerów fizycznych."
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: cfreeman
editor: 
ms.assetid: ef1f31d5-285b-4a0f-89b5-0123cd422d80
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 03/27/2017
ms.author: raynew
ms.openlocfilehash: 95f20433f782c93685ad4bae93c6bc0e2d2f2356
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="remove-servers-and-disable-protection"></a><span data-ttu-id="0220e-103">Usuwanie serwerów i wyłączanie ochrony</span><span class="sxs-lookup"><span data-stu-id="0220e-103">Remove servers and disable protection</span></span>

<span data-ttu-id="0220e-104">Witaj usługi Azure Site Recovery przyczynia się tooyour ciągłość i strategia odzyskiwania (BCDR).</span><span class="sxs-lookup"><span data-stu-id="0220e-104">hello Azure Site Recovery service contributes tooyour business continuity and disaster recovery (BCDR) strategy.</span></span> <span data-ttu-id="0220e-105">Usługa Hello uruchamia replikacji, trybu failover i odzyskiwania maszyn wirtualnych i serwerów fizycznych.</span><span class="sxs-lookup"><span data-stu-id="0220e-105">hello service orchestrates replication, failover and recovery of virtual machines and physical servers.</span></span> <span data-ttu-id="0220e-106">Maszyny można replikowanych tooAzure lub tooa dodatkowej w lokalnym centrum danych.</span><span class="sxs-lookup"><span data-stu-id="0220e-106">Machines can be replicated tooAzure, or tooa secondary on-premises data center.</span></span> <span data-ttu-id="0220e-107">Aby zapoznać się z szybkim omówieniem, przeczytaj temat [Co to jest usługa Azure Site Recovery?](site-recovery-overview.md)</span><span class="sxs-lookup"><span data-stu-id="0220e-107">For a quick overview read [What is Azure Site Recovery?](site-recovery-overview.md)</span></span>

<span data-ttu-id="0220e-108">W tym artykule opisano sposób toounregister serwerów usług odzyskiwania magazynu w portalu Azure hello i jak toodisable ochrony maszyn chronione przez usługę Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="0220e-108">This article describes how toounregister servers from a Recovery Services vault in hello Azure portal, and how toodisable protection for machines protected by Site Recovery.</span></span>

<span data-ttu-id="0220e-109">Zamieść wszelkie komentarze lub pytania u dołu hello w tym artykule, albo na powitania [Forum usług odzyskiwania Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="0220e-109">Post any comments or questions at hello bottom of this article, or on hello [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>

## <a name="unregister-a-connected-configuration-server"></a><span data-ttu-id="0220e-110">Wyrejestruj serwer konfiguracji połączenia</span><span class="sxs-lookup"><span data-stu-id="0220e-110">Unregister a connected configuration server</span></span>

<span data-ttu-id="0220e-111">Jeśli replikujesz maszyny wirtualne VMware lub tooAzure serwerach fizycznych systemu Windows i Linux, serwer konfiguracji połączonych z magazynu można wyrejestrować w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="0220e-111">If you replicate VMware VMs or Windows/Linux physical servers tooAzure, you can unregister a connected configuration server from a vault as follows:</span></span>

1. <span data-ttu-id="0220e-112">Wyłącz ochronę maszyny.</span><span class="sxs-lookup"><span data-stu-id="0220e-112">Disable machine protection.</span></span> <span data-ttu-id="0220e-113">W **chronione elementy** > **elementy replikowane**, kliknij prawym przyciskiem myszy hello maszyny > **usunąć**.</span><span class="sxs-lookup"><span data-stu-id="0220e-113">In **Protected Items** > **Replicated Items**, right-click hello machine > **Delete**.</span></span>
2. <span data-ttu-id="0220e-114">Usuń skojarzenie żadnych zasad.</span><span class="sxs-lookup"><span data-stu-id="0220e-114">Disassociate any policies.</span></span> <span data-ttu-id="0220e-115">W **infrastruktura usługi Site Recovery** > **dla VMWare i maszyn fizycznych** > **zasady replikacji**, kliknij dwukrotnie hello skojarzonych zasad.</span><span class="sxs-lookup"><span data-stu-id="0220e-115">In **Site Recovery Infrastructure** > **For VMWare & Physical Machines** > **Replication Policies**, double-click hello associated policy.</span></span> <span data-ttu-id="0220e-116">Serwer konfiguracji powitania kliknij prawym przyciskiem myszy > **usuwanie skojarzenia**.</span><span class="sxs-lookup"><span data-stu-id="0220e-116">Right-click hello configuration server > **Disassociate**.</span></span>
3. <span data-ttu-id="0220e-117">Usuń wszelkie dodatkowe lokalnymi procesu lub głównych serwerów docelowych.</span><span class="sxs-lookup"><span data-stu-id="0220e-117">Remove any additional on-premises process or master target servers.</span></span> <span data-ttu-id="0220e-118">W **infrastruktura usługi Site Recovery** > **dla VMWare i maszyn fizycznych** > **serwery konfiguracji**, kliknij prawym przyciskiem myszy powitania serwera > **Usunąć**.</span><span class="sxs-lookup"><span data-stu-id="0220e-118">In **Site Recovery Infrastructure** > **For VMWare & Physical Machines** > **Configuration Servers**, right-click hello server > **Delete**.</span></span>
4. <span data-ttu-id="0220e-119">Usuń powitania serwera konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="0220e-119">Delete hello configuration server.</span></span>
5. <span data-ttu-id="0220e-120">Ręcznie odinstalować usługi mobilności hello uruchomionej na powitania główny serwer docelowy (są to albo oddzielnym serwerze lub uruchomiona na serwerze konfiguracji hello).</span><span class="sxs-lookup"><span data-stu-id="0220e-120">Manually uninstall hello Mobility service running on hello master target server (this will be either a separate server, or running on hello configuration server).</span></span>
6. <span data-ttu-id="0220e-121">Odinstaluj wszystkie serwery dodatkowych procesów.</span><span class="sxs-lookup"><span data-stu-id="0220e-121">Uninstall any additional process servers.</span></span>
7. <span data-ttu-id="0220e-122">Odinstaluj powitania serwera konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="0220e-122">Uninstall hello configuration server.</span></span>
8. <span data-ttu-id="0220e-123">Na serwerze konfiguracji hello odinstalować hello wystąpienie MySQL, która została zainstalowana przez usługę Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="0220e-123">On hello configuration server, uninstall hello instance of MySQL that was installed by Site Recovery.</span></span>
9. <span data-ttu-id="0220e-124">W rejestrze hello powitania serwera konfiguracji należy usunąć klucz hello ``HKEY_LOCAL_MACHINE\Software\Microsoft\Azure Site Recovery``.</span><span class="sxs-lookup"><span data-stu-id="0220e-124">In hello registry of hello configuration server delete hello key ``HKEY_LOCAL_MACHINE\Software\Microsoft\Azure Site Recovery``.</span></span>

## <a name="unregister-a-unconnected-configuration-server"></a><span data-ttu-id="0220e-125">Wyrejestruj serwer odłączony konfiguracji</span><span class="sxs-lookup"><span data-stu-id="0220e-125">Unregister a unconnected configuration server</span></span>

<span data-ttu-id="0220e-126">Jeśli replikujesz maszyny wirtualne VMware lub tooAzure serwerach fizycznych systemu Windows i Linux można wyrejestrować serwera konfiguracji odłączony z magazynu w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="0220e-126">If you replicate VMware VMs or Windows/Linux physical servers tooAzure, you can unregister an unconnected configuration server from a vault as follows:</span></span>

1. <span data-ttu-id="0220e-127">Wyłącz ochronę maszyny.</span><span class="sxs-lookup"><span data-stu-id="0220e-127">Disable machine protection.</span></span> <span data-ttu-id="0220e-128">W **chronione elementy** > **elementy replikowane**, kliknij prawym przyciskiem myszy hello maszyny > **usunąć**.</span><span class="sxs-lookup"><span data-stu-id="0220e-128">In **Protected Items** > **Replicated Items**, right-click hello machine > **Delete**.</span></span> <span data-ttu-id="0220e-129">Wybierz **zatrzymywanie zarządzania hello maszyny**.</span><span class="sxs-lookup"><span data-stu-id="0220e-129">Select **Stop managing hello machine**.</span></span>
2. <span data-ttu-id="0220e-130">Usuń wszelkie dodatkowe lokalnymi procesu lub głównych serwerów docelowych.</span><span class="sxs-lookup"><span data-stu-id="0220e-130">Remove any additional on-premises process or master target servers.</span></span> <span data-ttu-id="0220e-131">W **infrastruktura usługi Site Recovery** > **dla VMWare i maszyn fizycznych** > **serwery konfiguracji**, kliknij prawym przyciskiem myszy powitania serwera > **Usunąć**.</span><span class="sxs-lookup"><span data-stu-id="0220e-131">In **Site Recovery Infrastructure** > **For VMWare & Physical Machines** > **Configuration Servers**, right-click hello server > **Delete**.</span></span>
3. <span data-ttu-id="0220e-132">Usuń powitania serwera konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="0220e-132">Delete hello configuration server.</span></span>
4. <span data-ttu-id="0220e-133">Ręcznie odinstalować usługi mobilności hello uruchomionej na powitania główny serwer docelowy (są to albo oddzielnym serwerze lub uruchomiona na serwerze konfiguracji hello).</span><span class="sxs-lookup"><span data-stu-id="0220e-133">Manually uninstall hello Mobility service running on hello master target server (this will be either a separate server, or running on hello configuration server).</span></span>
5. <span data-ttu-id="0220e-134">Odinstaluj wszystkie serwery dodatkowych procesów.</span><span class="sxs-lookup"><span data-stu-id="0220e-134">Uninstall any additional process servers.</span></span>
6. <span data-ttu-id="0220e-135">Odinstaluj powitania serwera konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="0220e-135">Uninstall hello configuration server.</span></span>
7. <span data-ttu-id="0220e-136">Na serwerze konfiguracji hello odinstalować hello wystąpienie MySQL, która została zainstalowana przez usługę Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="0220e-136">On hello configuration server, uninstall hello instance of MySQL that was installed by Site Recovery.</span></span>
8. <span data-ttu-id="0220e-137">W rejestrze hello powitania serwera konfiguracji należy usunąć klucz hello ``HKEY_LOCAL_MACHINE\Software\Microsoft\Azure Site Recovery``.</span><span class="sxs-lookup"><span data-stu-id="0220e-137">In hello registry of hello configuration server delete hello key ``HKEY_LOCAL_MACHINE\Software\Microsoft\Azure Site Recovery``.</span></span>

## <a name="unregister-a-connected-vmm-server"></a><span data-ttu-id="0220e-138">Wyrejestruj połączony z serwerem VMM</span><span class="sxs-lookup"><span data-stu-id="0220e-138">Unregister a connected VMM server</span></span>

<span data-ttu-id="0220e-139">Jako najlepsze rozwiązanie zaleca się wyrejestrować serwera VMM hello, gdy jest podłączone tooAzure.</span><span class="sxs-lookup"><span data-stu-id="0220e-139">As a best practice, we recommend that you unregister hello VMM server when it's connected tooAzure.</span></span> <span data-ttu-id="0220e-140">Daje to pewność, że ustawienia na serwerach VMM hello (i na innych serwerach VMM z pary chmur) są prawidłowo czyszczone.</span><span class="sxs-lookup"><span data-stu-id="0220e-140">This ensures that settings on hello VMM servers (and on other VMM servers with paired clouds) are cleaned up properly.</span></span> <span data-ttu-id="0220e-141">Odłączony serwer należy usunąć tylko wtedy, gdy stałe problem z łącznością.</span><span class="sxs-lookup"><span data-stu-id="0220e-141">You should only remove an unconnected server if there's a permanent issue with connectivity.</span></span> <span data-ttu-id="0220e-142">Jeśli serwer VMM hello nie jest połączony, konieczne będzie toomanually Uruchom skrypt tooclean ustawień.</span><span class="sxs-lookup"><span data-stu-id="0220e-142">If hello VMM server isn’t connected, you will need toomanually run a script tooclean up settings.</span></span>

1. <span data-ttu-id="0220e-143">Zatrzymaj replikowanie maszyn wirtualnych w chmurach na powitania serwera VMM ma tooremove.</span><span class="sxs-lookup"><span data-stu-id="0220e-143">Stop replicating VMs in clouds on hello VMM server you want tooremove.</span></span>
2. <span data-ttu-id="0220e-144">Usuń wszystkie używane przez chmury na powitania serwera VMM ma toodelete mapowania sieci.</span><span class="sxs-lookup"><span data-stu-id="0220e-144">Delete any network mappings used by clouds on hello VMM server you want toodelete.</span></span> <span data-ttu-id="0220e-145">W **infrastruktura usługi Site Recovery** > **dla programu System Center VMM** > **mapowania sieci**, kliknij prawym przyciskiem myszy mapowania sieci hello >  **Usuń**.</span><span class="sxs-lookup"><span data-stu-id="0220e-145">In **Site Recovery Infrastructure** > **For System Center VMM** > **Network Mapping**, right-click hello network mapping > **Delete**.</span></span>
3. <span data-ttu-id="0220e-146">Usuń skojarzenia zasad replikacji z chmury na powitania serwera VMM ma tooremove.</span><span class="sxs-lookup"><span data-stu-id="0220e-146">Disassociate replication policies from clouds on hello VMM server you want tooremove.</span></span>  <span data-ttu-id="0220e-147">W **infrastruktura usługi Site Recovery** > **dla programu System Center VMM** >  **zasady replikacji**, kliknij dwukrotnie hello skojarzonych zasad.</span><span class="sxs-lookup"><span data-stu-id="0220e-147">In **Site Recovery Infrastructure** > **For System Center VMM** >  **Replication Policies**, double-click hello associated policy.</span></span> <span data-ttu-id="0220e-148">Kliknij prawym przyciskiem myszy chmury hello > **usuwanie skojarzenia**.</span><span class="sxs-lookup"><span data-stu-id="0220e-148">Right-click hello cloud > **Disassociate**.</span></span>
4. <span data-ttu-id="0220e-149">Usuń serwer VMM hello lub aktywny węzeł programu VMM.</span><span class="sxs-lookup"><span data-stu-id="0220e-149">Delete hello VMM server or active VMM node.</span></span> <span data-ttu-id="0220e-150">W **infrastruktura usługi Site Recovery** > **dla programu System Center VMM** > **serwery VMM**, kliknij prawym przyciskiem myszy serwer hello >  **Usuń**.</span><span class="sxs-lookup"><span data-stu-id="0220e-150">In **Site Recovery Infrastructure** > **For System Center VMM** > **VMM Servers**, right-click hello server > **Delete**.</span></span>
5. <span data-ttu-id="0220e-151">Odinstaluj hello dostawcy ręcznie na serwerze VMM hello.</span><span class="sxs-lookup"><span data-stu-id="0220e-151">Uninstall hello Provider manually on hello VMM server.</span></span> <span data-ttu-id="0220e-152">Jeśli masz klaster, Usuń z dowolnych węzłów.</span><span class="sxs-lookup"><span data-stu-id="0220e-152">If you have a cluster, remove from all nodes.</span></span>
6. <span data-ttu-id="0220e-153">Jeśli replikujesz tooAzure, Usuń ręcznie agenta usług odzyskiwania Microsoft hello z hostów funkcji Hyper-V w chmurach hello usunięte.</span><span class="sxs-lookup"><span data-stu-id="0220e-153">If you're replicating tooAzure, manually remove hello Microsoft Recovery Services agent from Hyper-V hosts in hello deleted clouds.</span></span>



### <a name="unregister-an-unconnected-vmm-server"></a><span data-ttu-id="0220e-154">Wyrejestruj odłączony serwer programu VMM</span><span class="sxs-lookup"><span data-stu-id="0220e-154">Unregister an unconnected VMM server</span></span>

1. <span data-ttu-id="0220e-155">Zatrzymaj replikowanie maszyn wirtualnych w chmurach na powitania serwera VMM ma tooremove.</span><span class="sxs-lookup"><span data-stu-id="0220e-155">Stop replicating VMs in clouds on hello VMM server you want tooremove.</span></span>
2. <span data-ttu-id="0220e-156">Usuń wszystkie używane przez chmury na serwerze VMM hello, które mają toodelete mapowania sieci.</span><span class="sxs-lookup"><span data-stu-id="0220e-156">Delete any network mappings used by clouds on hello VMM server that you want toodelete.</span></span> <span data-ttu-id="0220e-157">W **infrastruktura usługi Site Recovery** > **dla programu System Center VMM** > **mapowania sieci**, kliknij prawym przyciskiem myszy mapowania sieci hello >  **Usuń**.</span><span class="sxs-lookup"><span data-stu-id="0220e-157">In **Site Recovery Infrastructure** > **For System Center VMM** > **Network Mapping**, right-click hello network mapping > **Delete**.</span></span>
3. <span data-ttu-id="0220e-158">Należy pamiętać, identyfikator hello powitania serwera VMM.</span><span class="sxs-lookup"><span data-stu-id="0220e-158">Note hello ID of hello VMM server.</span></span>
4. <span data-ttu-id="0220e-159">Usuń skojarzenia zasad replikacji z chmury na powitania serwera VMM ma tooremove.</span><span class="sxs-lookup"><span data-stu-id="0220e-159">Disassociate replication policies from clouds on hello VMM server you want tooremove.</span></span>  <span data-ttu-id="0220e-160">W **infrastruktura usługi Site Recovery** > **dla programu System Center VMM** >  **zasady replikacji**, kliknij dwukrotnie hello skojarzonych zasad.</span><span class="sxs-lookup"><span data-stu-id="0220e-160">In **Site Recovery Infrastructure** > **For System Center VMM** >  **Replication Policies**, double-click hello associated policy.</span></span> <span data-ttu-id="0220e-161">Kliknij prawym przyciskiem myszy chmury hello > **usuwanie skojarzenia**.</span><span class="sxs-lookup"><span data-stu-id="0220e-161">Right-click hello cloud > **Disassociate**.</span></span>
5. <span data-ttu-id="0220e-162">Usuń serwer VMM hello lub aktywnego węzła.</span><span class="sxs-lookup"><span data-stu-id="0220e-162">Delete hello VMM server or active node.</span></span> <span data-ttu-id="0220e-163">W **infrastruktura usługi Site Recovery** > **dla programu System Center VMM** > **serwery VMM**, kliknij prawym przyciskiem myszy serwer hello >  **Usuń**.</span><span class="sxs-lookup"><span data-stu-id="0220e-163">In **Site Recovery Infrastructure** > **For System Center VMM** > **VMM Servers**, right-click hello server > **Delete**.</span></span>
6. <span data-ttu-id="0220e-164">Pobierz i uruchom hello [skrypt czyszczący](http://aka.ms/asr-cleanup-script-vmm) na powitania serwera VMM.</span><span class="sxs-lookup"><span data-stu-id="0220e-164">Download and run hello [cleanup script](http://aka.ms/asr-cleanup-script-vmm) on hello VMM server.</span></span> <span data-ttu-id="0220e-165">Otwórz program PowerShell z hello **Uruchom jako Administrator** opcji zasad wykonywania hello toochange hello zakresu domyślne (LocalMachine).</span><span class="sxs-lookup"><span data-stu-id="0220e-165">Open PowerShell with hello **Run as Administrator** option, toochange hello execution policy for hello default (LocalMachine) scope.</span></span> <span data-ttu-id="0220e-166">W skrypcie hello Określ identyfikator hello powitania serwera VMM ma tooremove.</span><span class="sxs-lookup"><span data-stu-id="0220e-166">In hello script, specify hello ID of hello VMM server you want tooremove.</span></span> <span data-ttu-id="0220e-167">skrypt Hello usuwa rejestrację i informacji o serwerze hello parowania w chmurze.</span><span class="sxs-lookup"><span data-stu-id="0220e-167">hello script removes registration and cloud pairing information from hello server.</span></span>
5. <span data-ttu-id="0220e-168">Uruchom skrypt czyszczący hello na innych serwerach VMM, które zawierają chmury, które są skojarzone z chmury na powitania serwera VMM ma tooremove.</span><span class="sxs-lookup"><span data-stu-id="0220e-168">Run hello cleanup script on any other VMM servers that contain clouds that are paired with clouds on hello VMM server you want tooremove.</span></span>
6. <span data-ttu-id="0220e-169">Uruchom skrypt czyszczący hello na inne pasywnych węzłach klastra VMM, których powitalne zainstalowany dostawca.</span><span class="sxs-lookup"><span data-stu-id="0220e-169">Run hello  cleanup script on any other passive VMM cluster nodes that have hello Provider installed.</span></span>
7. <span data-ttu-id="0220e-170">Odinstaluj hello dostawcy ręcznie na serwerze VMM hello.</span><span class="sxs-lookup"><span data-stu-id="0220e-170">Uninstall hello Provider manually on hello VMM server.</span></span> <span data-ttu-id="0220e-171">Jeśli masz klaster, Usuń z dowolnych węzłów.</span><span class="sxs-lookup"><span data-stu-id="0220e-171">If you have a cluster, remove from all nodes.</span></span>
8. <span data-ttu-id="0220e-172">Jeśli użytkownik replikacji tooAzure, można usunąć agenta usług odzyskiwania Microsoft hello z hostów funkcji Hyper-V w chmurach hello usunięte.</span><span class="sxs-lookup"><span data-stu-id="0220e-172">If you replicating tooAzure, you can remove hello Microsoft Recovery Services agent from Hyper-V hosts in hello deleted clouds.</span></span>

## <a name="unregister-a-hyper-v-host-in-a-hyper-v-site"></a><span data-ttu-id="0220e-173">Wyrejestruj hosta funkcji Hyper-V w lokacji funkcji Hyper-V</span><span class="sxs-lookup"><span data-stu-id="0220e-173">Unregister a Hyper-V host in a Hyper-V Site</span></span>

<span data-ttu-id="0220e-174">Hosty funkcji Hyper-V, które nie są zarządzane przez program VMM są zbierane w lokacji funkcji Hyper-V.</span><span class="sxs-lookup"><span data-stu-id="0220e-174">Hyper-V hosts that aren't managed by VMM are gathered into a Hyper-V site.</span></span> <span data-ttu-id="0220e-175">Usuń hosta w lokacji funkcji Hyper-V w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="0220e-175">Remove a host in a Hyper-V site as follows:</span></span>

1. <span data-ttu-id="0220e-176">Wyłącz replikację dla maszyn wirtualnych funkcji Hyper-V znajdujących się na hoście hello.</span><span class="sxs-lookup"><span data-stu-id="0220e-176">Disable replication for Hyper-V VMs located on hello host.</span></span>
2. <span data-ttu-id="0220e-177">Usuń skojarzenie zasad hello lokacji funkcji Hyper-V.</span><span class="sxs-lookup"><span data-stu-id="0220e-177">Disassociate policies for hello Hyper-V site.</span></span> <span data-ttu-id="0220e-178">W **infrastruktura usługi Site Recovery** > **dla Lokacje funkcji Hyper-V** >  **zasady replikacji**, kliknij dwukrotnie hello skojarzonych zasad.</span><span class="sxs-lookup"><span data-stu-id="0220e-178">In **Site Recovery Infrastructure** > **For Hyper-V Sites** >  **Replication Policies**, double-click hello associated policy.</span></span> <span data-ttu-id="0220e-179">Kliknij prawym przyciskiem myszy witrynę hello > **usuwanie skojarzenia**.</span><span class="sxs-lookup"><span data-stu-id="0220e-179">Right-click hello site > **Disassociate**.</span></span>
3. <span data-ttu-id="0220e-180">Usuwanie hostów funkcji Hyper-V.</span><span class="sxs-lookup"><span data-stu-id="0220e-180">Delete Hyper-V hosts.</span></span> <span data-ttu-id="0220e-181">W **infrastruktura usługi Site Recovery** > **dla programu System Center VMM** > **hosty funkcji Hyper-V**, kliknij prawym przyciskiem myszy serwer hello >  **Usuń**.</span><span class="sxs-lookup"><span data-stu-id="0220e-181">In **Site Recovery Infrastructure** > **For System Center VMM** > **Hyper-V Hosts**, right-click hello server > **Delete**.</span></span>
4. <span data-ttu-id="0220e-182">Usuń lokację hello funkcji Hyper-V, po wszystkie hosty zostały usunięte z niej.</span><span class="sxs-lookup"><span data-stu-id="0220e-182">Delete hello Hyper-V site after all hosts have been removed from it.</span></span> <span data-ttu-id="0220e-183">W **infrastruktura usługi Site Recovery** > **dla programu System Center VMM** > **Lokacje funkcji Hyper-V**, kliknij prawym przyciskiem myszy witrynę hello >  **Usuń**.</span><span class="sxs-lookup"><span data-stu-id="0220e-183">In **Site Recovery Infrastructure** > **For System Center VMM** > **Hyper-V Sites**, right-click hello site > **Delete**.</span></span>
5. <span data-ttu-id="0220e-184">Uruchom hello następującego skryptu na każdym hoście funkcji Hyper-V, które zostało usunięte.</span><span class="sxs-lookup"><span data-stu-id="0220e-184">Run hello following script on each Hyper-V host that you removed.</span></span> <span data-ttu-id="0220e-185">skrypt Hello czyści ustawienia na serwerze hello i wyrejestrowuje je z magazynu hello.</span><span class="sxs-lookup"><span data-stu-id="0220e-185">hello script cleans up settings on hello server, and unregisters it from hello vault.</span></span>


        `` pushd .
        try
        {
             $windowsIdentity=[System.Security.Principal.WindowsIdentity]::GetCurrent()
             $principal=new-object System.Security.Principal.WindowsPrincipal($windowsIdentity)
             $administrators=[System.Security.Principal.WindowsBuiltInRole]::Administrator
             $isAdmin=$principal.IsInRole($administrators)
             if (!$isAdmin)
             {
                "Please run hello script as an administrator in elevated mode."
                $choice = Read-Host
                return;       
             }

            $error.Clear()    
            "This script will remove hello old Azure Site Recovery Provider related properties. Do you want toocontinue (Y/N) ?"
            $choice =  Read-Host

            if (!($choice -eq 'Y' -or $choice -eq 'y'))
            {
            "Stopping cleanup."
            return;
            }

            $serviceName = "dra"
            $service = Get-Service -Name $serviceName
            if ($service.Status -eq "Running")
            {
                "Stopping hello Azure Site Recovery service..."
                net stop $serviceName
            }

            $asrHivePath = "HKLM:\SOFTWARE\Microsoft\Azure Site Recovery"
            $registrationPath = $asrHivePath + '\Registration'
            $proxySettingsPath = $asrHivePath + '\ProxySettings'
            $draIdvalue = 'DraID'

            if (Test-Path $asrHivePath)
            {
                if (Test-Path $registrationPath)
                {
                    "Removing registration related registry keys."    
                    Remove-Item -Recurse -Path $registrationPath
                }

                if (Test-Path $proxySettingsPath)
            {
                    "Removing proxy settings"
                    Remove-Item -Recurse -Path $proxySettingsPath
                }

                $regNode = Get-ItemProperty -Path $asrHivePath
                if($regNode.DraID -ne $null)
                {            
                    "Removing DraId"
                    Remove-ItemProperty -Path $asrHivePath -Name $draIdValue
                }
                "Registry keys removed."
            }

            # First retrive all hello certificates toobe deleted
            $ASRcerts = Get-ChildItem -Path cert:\localmachine\my | where-object {$_.friendlyname.startswith('ASR_SRSAUTH_CERT_KEY_CONTAINER') -or $_.friendlyname.startswith('ASR_HYPER_V_HOST_CERT_KEY_CONTAINER')}
            # Open a cert store object
            $store = New-Object System.Security.Cryptography.X509Certificates.X509Store("My","LocalMachine")
            $store.Open('ReadWrite')
            # Delete hello certs
            "Removing all related certificates"
            foreach ($cert in $ASRcerts)
            {
                $store.Remove($cert)
            }
        }catch
        {    
            [system.exception]
            Write-Host "Error occured" -ForegroundColor "Red"
            $error[0]
            Write-Host "FAILED" -ForegroundColor "Red"
        }
        popd``



## <a name="disable-protection-for-a-vmware-vm-or-physical-server"></a><span data-ttu-id="0220e-186">Wyłącz ochronę dla maszyny Wirtualnej VMware lub serwerów fizycznych</span><span class="sxs-lookup"><span data-stu-id="0220e-186">Disable protection for a VMware VM or physical server</span></span>

1. <span data-ttu-id="0220e-187">W **chronione elementy** > **elementy replikowane**, kliknij prawym przyciskiem myszy hello maszyny > **usunąć**.</span><span class="sxs-lookup"><span data-stu-id="0220e-187">In **Protected Items** > **Replicated Items**, right-click hello machine > **Delete**.</span></span>
2. <span data-ttu-id="0220e-188">W **Usuń maszyny**, wybierz jedną z następujących opcji:</span><span class="sxs-lookup"><span data-stu-id="0220e-188">In **Remove Machine**, select one of these options:</span></span>
    - <span data-ttu-id="0220e-189">**Wyłącz ochronę maszyny hello (zalecane)**.</span><span class="sxs-lookup"><span data-stu-id="0220e-189">**Disable protection for hello machine (recommended)**.</span></span> <span data-ttu-id="0220e-190">Użyj tego toostop opcji replikacji hello maszyny.</span><span class="sxs-lookup"><span data-stu-id="0220e-190">Use this option toostop replicating hello machine.</span></span> <span data-ttu-id="0220e-191">Ustawienia odzyskiwania lokacji zostaną automatycznie wyczyszczone.</span><span class="sxs-lookup"><span data-stu-id="0220e-191">Site Recovery settings will be cleaned up automatically.</span></span> <span data-ttu-id="0220e-192">Zobaczysz tę opcję w hello w następujących okolicznościach:</span><span class="sxs-lookup"><span data-stu-id="0220e-192">You will only see this option in hello following circumstances:</span></span>
        - <span data-ttu-id="0220e-193">**Hello wirtualna woluminu został zmieniony**— podczas zmiany rozmiaru woluminu hello wirtualnych maszyny przechodzi w stan krytyczny.</span><span class="sxs-lookup"><span data-stu-id="0220e-193">**You've resized hello VM volume**—When you resize a volume hello virtual machine goes into a critical state.</span></span> <span data-ttu-id="0220e-194">Wybierz tę ochronę toodisables opcji Zachowaj punkty odzyskiwania na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="0220e-194">Select this option toodisables protection while retaining recovery points in Azure.</span></span> <span data-ttu-id="0220e-195">Po włączeniu ochrony dla maszyny hello ponownie dane hello hello zmiany rozmiaru woluminu zostaną przeniesione tooAzure.</span><span class="sxs-lookup"><span data-stu-id="0220e-195">When you enable protection for hello machine again, hello data for hello resized volume will be transferred tooAzure.</span></span>
        - <span data-ttu-id="0220e-196">**Ostatnio uruchomiono trybu failover**— po uruchomieniu tootest pracy awaryjnej środowisku, wybierz ten toostart opcji ochrony maszyn lokalnych ponownie.</span><span class="sxs-lookup"><span data-stu-id="0220e-196">**You've recently run a failover**—After you've run a failover tootest your environment, select this option toostart protecting on-premises machines again.</span></span> <span data-ttu-id="0220e-197">Wyłącza on funkcję każdej maszyny wirtualnej, a następnie potrzebna tooenable ochrona je ponownie.</span><span class="sxs-lookup"><span data-stu-id="0220e-197">It disables each virtual machine, and then you need tooenable protection for them again.</span></span> <span data-ttu-id="0220e-198">Wyłączenie maszyny hello tego ustawienia nie wpływa na powitania maszyny wirtualnej repliki na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="0220e-198">Disabling hello machine with this setting doesn't affect hello replica virtual machine in Azure.</span></span> <span data-ttu-id="0220e-199">Nie należy odinstalować usługi mobilności hello z komputera hello.</span><span class="sxs-lookup"><span data-stu-id="0220e-199">Don't uninstall hello Mobility service from hello machine.</span></span>
    - <span data-ttu-id="0220e-200">**Zatrzymywanie zarządzania hello maszyny**.</span><span class="sxs-lookup"><span data-stu-id="0220e-200">**Stop managing hello machine**.</span></span> <span data-ttu-id="0220e-201">Jeśli wybierzesz tę opcję, hello maszyny tylko zostaną usunięte z magazynu hello.</span><span class="sxs-lookup"><span data-stu-id="0220e-201">If you select this option, hello machine will only be removed from hello vault.</span></span> <span data-ttu-id="0220e-202">Nie będzie mieć wpływ na ustawienia ochrony lokalne powitania maszyny.</span><span class="sxs-lookup"><span data-stu-id="0220e-202">On-premises protection settings for hello machine won’t be affected.</span></span> <span data-ttu-id="0220e-203">Ustawienia tooremove na komputerze hello i tooremove hello maszyny z hello subskrypcji platformy Azure, należy tooclean hello ustawień przez odinstalowanie hello usługi mobilności.</span><span class="sxs-lookup"><span data-stu-id="0220e-203">tooremove settings on hello machine, and tooremove hello machine from hello Azure subscription, you need tooclean hello settings by uninstalling hello Mobility service.</span></span>

## <a name="disable-protection-for-a-hyper-v-vm-in-a-vmm-cloud"></a><span data-ttu-id="0220e-204">Wyłącz ochronę dla maszyny Wirtualnej funkcji Hyper-V w chmurze VMM</span><span class="sxs-lookup"><span data-stu-id="0220e-204">Disable protection for a Hyper-V VM in a VMM cloud</span></span>

1. <span data-ttu-id="0220e-205">W **chronione elementy** > **elementy replikowane**, kliknij prawym przyciskiem myszy hello maszyny > **usunąć**.</span><span class="sxs-lookup"><span data-stu-id="0220e-205">In **Protected Items** > **Replicated Items**, right-click hello machine > **Delete**.</span></span>
2. <span data-ttu-id="0220e-206">W **Usuń maszyny**, wybierz jedną z następujących opcji:</span><span class="sxs-lookup"><span data-stu-id="0220e-206">In **Remove Machine**, select one of these options:</span></span>

    - <span data-ttu-id="0220e-207">**Wyłącz ochronę maszyny hello (zalecane)**.</span><span class="sxs-lookup"><span data-stu-id="0220e-207">**Disable protection for hello machine (recommended)**.</span></span> <span data-ttu-id="0220e-208">Użyj tego toostop opcji replikacji hello maszyny.</span><span class="sxs-lookup"><span data-stu-id="0220e-208">Use this option toostop replicating hello machine.</span></span> <span data-ttu-id="0220e-209">Ustawienia odzyskiwania lokacji zostaną automatycznie wyczyszczone.</span><span class="sxs-lookup"><span data-stu-id="0220e-209">Site Recovery settings will be cleaned up automatically.</span></span>
    - <span data-ttu-id="0220e-210">**Zatrzymywanie zarządzania hello maszyny**.</span><span class="sxs-lookup"><span data-stu-id="0220e-210">**Stop managing hello machine**.</span></span> <span data-ttu-id="0220e-211">Jeśli wybierzesz tę opcję, hello maszyny tylko zostaną usunięte z magazynu hello.</span><span class="sxs-lookup"><span data-stu-id="0220e-211">If you select this option, hello machine will only be removed from hello vault.</span></span> <span data-ttu-id="0220e-212">Nie będzie mieć wpływ na ustawienia ochrony lokalne powitania maszyny.</span><span class="sxs-lookup"><span data-stu-id="0220e-212">On-premises protection settings for hello machine won’t be affected.</span></span> <span data-ttu-id="0220e-213">Ustawienia tooremove na komputerze hello i tooremove hello maszyny z hello subskrypcji platformy Azure, należy tooclean hello ustawienia się ręcznie, przy użyciu instrukcji hello poniżej.</span><span class="sxs-lookup"><span data-stu-id="0220e-213">tooremove settings on hello machine, and tooremove hello machine from hello Azure subscription, you need tooclean hello settings up manually, using hello instructions below.</span></span> <span data-ttu-id="0220e-214">Należy zwrócić uwagę, jeśli zostanie wybrana maszyna wirtualna hello toodelete i jej dyski twarde, zostanie usunięcia z hello lokalizacji docelowej.</span><span class="sxs-lookup"><span data-stu-id="0220e-214">Note that if you select toodelete hello virtual machine and its hard disks, they'll be removed from hello target location.</span></span>

### <a name="clean-up-protection-settings---replication-tooa-secondary-vmm-site"></a><span data-ttu-id="0220e-215">Wyczyść ustawienia ochrony — lokacja dodatkowa programu VMM tooa replikacji</span><span class="sxs-lookup"><span data-stu-id="0220e-215">Clean up protection settings - replication tooa secondary VMM site</span></span>

<span data-ttu-id="0220e-216">W przypadku wybrania **zatrzymywanie zarządzania hello maszyny** i możesz replikowanie tooa lokacji dodatkowej, uruchom ten skrypt na powitania serwera podstawowego tooclean ustawienia hello hello głównej maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="0220e-216">If you selected **Stop managing hello machine** and you replicating tooa secondary site, run this script on hello primary server tooclean up hello settings for hello primary virtual machine.</span></span> <span data-ttu-id="0220e-217">W konsoli programu VMM powitania kliknij konsoli programu VMM PowerShell hello tooopen hello PowerShell przycisk.</span><span class="sxs-lookup"><span data-stu-id="0220e-217">In hello VMM console click hello PowerShell button tooopen hello VMM PowerShell console.</span></span> <span data-ttu-id="0220e-218">Zamień SQLVM1 hello nazwę maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="0220e-218">Replace SQLVM1 with hello name of your virtual machine.</span></span>

         ``$vm = get-scvirtualmachine -Name "SQLVM1"
         Set-SCVirtualMachine -VM $vm -ClearDRProtection``
2. <span data-ttu-id="0220e-219">Uruchom ten skrypt tooclean hello ustawień dla pomocniczej maszyny wirtualnej hello na powitania pomocniczy serwer programu VMM:</span><span class="sxs-lookup"><span data-stu-id="0220e-219">On hello secondary VMM server run this script tooclean up hello settings for hello secondary virtual machine:</span></span>

        ``$vm = get-scvirtualmachine -Name "SQLVM1"
        Remove-SCVirtualMachine -VM $vm -Force``
3. <span data-ttu-id="0220e-220">Na powitania pomocniczy serwer programu VMM Odśwież hello maszyn wirtualnych na serwerze hosta funkcji Hyper-V hello, dzięki czemu hello dodatkowej maszyny Wirtualnej pobiera wykryte ponownie w konsoli programu VMM hello.</span><span class="sxs-lookup"><span data-stu-id="0220e-220">On hello secondary VMM server, refresh hello virtual machines on hello Hyper-V host server, so that hello secondary VM gets detected again in hello VMM console.</span></span>
4. <span data-ttu-id="0220e-221">Wyczyść Hello powyżej kroki hello ustawienia replikacji na serwerze VMM hello.</span><span class="sxs-lookup"><span data-stu-id="0220e-221">hello above steps clear up hello replication settings on hello VMM server.</span></span> <span data-ttu-id="0220e-222">Jeśli chcesz, aby toostop replikacji dla maszyny wirtualnej hello, uruchom następujące skryptu Niestety hello hello głównych i dodatkowych maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="0220e-222">If you want toostop replication for hello virtual machine, run hello following script oh hello primary and secondary VMs.</span></span> <span data-ttu-id="0220e-223">Zamień SQLVM1 hello nazwę maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="0220e-223">Replace SQLVM1 with hello name of your virtual machine.</span></span>

        ``Remove-VMReplication –VMName “SQLVM1”``

### <a name="clean-up-protection-settings---replication-tooazure"></a><span data-ttu-id="0220e-224">Wyczyść ustawienia ochrony - tooAzure replikacji</span><span class="sxs-lookup"><span data-stu-id="0220e-224">Clean up protection settings - replication tooAzure</span></span>

1. <span data-ttu-id="0220e-225">W przypadku wybrania **zatrzymywanie zarządzania hello maszyny** i replikowane tooAzure, uruchom ten skrypt na powitania źródłowy serwer VMM przy użyciu programu PowerShell z konsoli programu VMM hello.</span><span class="sxs-lookup"><span data-stu-id="0220e-225">If you selected **Stop managing hello machine** and you replicate tooAzure, run this script on hello source VMM server, using PowerShell from hello VMM console.</span></span>
        ``$vm = get-scvirtualmachine -Name "SQLVM1"
        Set-SCVirtualMachine -VM $vm -ClearDRProtection``
2. <span data-ttu-id="0220e-226">Witaj powyżej kroki wyczyść hello ustawienia replikacji na serwerze VMM hello.</span><span class="sxs-lookup"><span data-stu-id="0220e-226">hello above steps clear hello replication settings on hello VMM server.</span></span> <span data-ttu-id="0220e-227">Replikacja toostop hello maszynę wirtualną działającą na serwerze hosta funkcji Hyper-V hello, uruchom ten skrypt.</span><span class="sxs-lookup"><span data-stu-id="0220e-227">toostop replication for hello virtual machine running on hello Hyper-V host server, run this script.</span></span> <span data-ttu-id="0220e-228">Zamień SQLVM1 hello nazwę maszyny wirtualnej, a host01.contoso.com o nazwie powitania serwera hosta funkcji Hyper-V hello.</span><span class="sxs-lookup"><span data-stu-id="0220e-228">Replace SQLVM1 with hello name of your virtual machine, and host01.contoso.com with hello name of hello Hyper-V host server.</span></span>

        ``$vmName = "SQLVM1"
        $hostName  = "host01.contoso.com"
        $vm = Get-WmiObject -Namespace "root\virtualization\v2" -Query "Select * From Msvm_ComputerSystem Where ElementName = '$vmName'" -computername $hostName
        $replicationService = Get-WmiObject -Namespace "root\virtualization\v2"  -Query "Select * From Msvm_ReplicationService"  -computername $hostName
        $replicationService.RemoveReplicationRelationship($vm.__PATH)``


## <a name="disable-protection-for-a-hyper-v-vm-in-a-hyper-v-site"></a><span data-ttu-id="0220e-229">Wyłącz ochronę dla maszyny Wirtualnej funkcji Hyper-V w lokacji funkcji Hyper-V</span><span class="sxs-lookup"><span data-stu-id="0220e-229">Disable protection for a Hyper-V VM in a Hyper-V Site</span></span>

<span data-ttu-id="0220e-230">Użyj tej procedury, Jeśli replikujesz tooAzure maszyn wirtualnych funkcji Hyper-V bez serwera VMM.</span><span class="sxs-lookup"><span data-stu-id="0220e-230">Use this procedure if you're replicating Hyper-V VMs tooAzure without a VMM server.</span></span>

1. <span data-ttu-id="0220e-231">W **chronione elementy** > **elementy replikowane**, kliknij prawym przyciskiem myszy hello maszyny > **usunąć**.</span><span class="sxs-lookup"><span data-stu-id="0220e-231">In **Protected Items** > **Replicated Items**, right-click hello machine > **Delete**.</span></span>
2. <span data-ttu-id="0220e-232">W **Usuń maszyny**, możesz wybrać hello następujące opcje:</span><span class="sxs-lookup"><span data-stu-id="0220e-232">In **Remove Machine**, you can select hello following options:</span></span>

   - <span data-ttu-id="0220e-233">**Wyłącz ochronę maszyny hello (zalecane)**.</span><span class="sxs-lookup"><span data-stu-id="0220e-233">**Disable protection for hello machine (recommended)**.</span></span> <span data-ttu-id="0220e-234">Użyj tego toostop opcji replikacji hello maszyny.</span><span class="sxs-lookup"><span data-stu-id="0220e-234">Use this option toostop replicating hello machine.</span></span> <span data-ttu-id="0220e-235">Ustawienia odzyskiwania lokacji zostaną automatycznie wyczyszczone.</span><span class="sxs-lookup"><span data-stu-id="0220e-235">Site Recovery settings will be cleaned up automatically.</span></span>
   - <span data-ttu-id="0220e-236">**Zatrzymywanie zarządzania hello maszyny**.</span><span class="sxs-lookup"><span data-stu-id="0220e-236">**Stop managing hello machine**.</span></span> <span data-ttu-id="0220e-237">Jeśli ta opcja jest zaznaczona maszyna hello tylko zostanie usunięta z magazynu hello.</span><span class="sxs-lookup"><span data-stu-id="0220e-237">If you select this option hello machine will only be removed from hello vault.</span></span> <span data-ttu-id="0220e-238">Nie będzie mieć wpływ na ustawienia ochrony lokalne powitania maszyny.</span><span class="sxs-lookup"><span data-stu-id="0220e-238">On-premises protection settings for hello machine won’t be affected.</span></span> <span data-ttu-id="0220e-239">Ustawienia tooremove na komputerze hello i tooremove hello maszyny wirtualnej na podstawie hello subskrypcji platformy Azure, należy ustawienia hello tooclean się ręcznie.</span><span class="sxs-lookup"><span data-stu-id="0220e-239">tooremove settings on hello machine, and tooremove hello virtual machine from hello Azure subscription, you need tooclean hello settings up manually.</span></span> <span data-ttu-id="0220e-240">W przypadku wybrania maszyny wirtualnej hello toodelete i jej dyski twarde zostaną one usunięte z lokalizacji docelowej hello.</span><span class="sxs-lookup"><span data-stu-id="0220e-240">If you select toodelete hello virtual machine and its hard disks they will be removed from hello target location.</span></span>
3. <span data-ttu-id="0220e-241">W przypadku wybrania **zatrzymywanie zarządzania hello maszyny**, uruchom ten skrypt na serwerze hosta funkcji Hyper-V źródła hello, replikacja tooremove hello maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="0220e-241">If you selected **Stop managing hello machine**, run this script on hello source Hyper-V host server, tooremove replication for hello virtual machine.</span></span> <span data-ttu-id="0220e-242">Zamień SQLVM1 hello nazwę maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="0220e-242">Replace SQLVM1 with hello name of your virtual machine.</span></span>

        $vmName = "SQLVM1"
        $vm = Get-WmiObject -Namespace "root\virtualization\v2" -Query "Select * From Msvm_ComputerSystem Where ElementName = '$vmName'"
        $replicationService = Get-WmiObject -Namespace "root\virtualization\v2"  -Query "Select * From Msvm_ReplicationService"
        $replicationService.RemoveReplicationRelationship($vm.__PATH)
