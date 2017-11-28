---
title: "tooset maszyny aaaPrepare zapasowej odzyskiwania po awarii między regiony platformy Azure po migracji tooAzure przy użyciu usługi Site Recovery | Dokumentacja firmy Microsoft"
description: "W tym artykule opisano, jak tooprepare maszyny tooset zapasowej odzyskiwania po awarii między regiony platformy Azure po tooAzure migracji za pomocą usługi Azure Site Recovery."
services: site-recovery
documentationcenter: 
author: ponatara
manager: abhemraj
editor: 
ms.assetid: 9126f5e8-e9ed-4c31-b6b4-bf969c12c184
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/22/2017
ms.author: ponatara
ms.openlocfilehash: b6274e3df210c1d8a7b8289cc85868ee6414e523
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="replicate-azure-vms-tooanother-region-after-migration-tooazure-by-using-azure-site-recovery"></a><span data-ttu-id="bce3f-103">Replikowanie maszyn wirtualnych platformy Azure region tooanother po tooAzure migracji za pomocą usługi Azure Site Recovery</span><span class="sxs-lookup"><span data-stu-id="bce3f-103">Replicate Azure VMs tooanother region after migration tooAzure by using Azure Site Recovery</span></span>

>[!NOTE]
> <span data-ttu-id="bce3f-104">Azure Site Recovery replikacji maszyn wirtualnych platformy Azure (VM) jest obecnie w przeglądzie.</span><span class="sxs-lookup"><span data-stu-id="bce3f-104">Azure Site Recovery replication for Azure virtual machines (VMs) is currently in preview.</span></span>

## <a name="overview"></a><span data-ttu-id="bce3f-105">Omówienie</span><span class="sxs-lookup"><span data-stu-id="bce3f-105">Overview</span></span>

<span data-ttu-id="bce3f-106">Ten artykuł pomaga przygotować maszyn wirtualnych platformy Azure dla replikacji między dwóch regionach platformy Azure, po przeprowadzeniu migracji te maszyny z tooAzure środowiska lokalnego przy użyciu usługi Azure Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="bce3f-106">This article helps you prepare Azure virtual machines for replication between two Azure regions after these machines have been migrated from an on-premises environment tooAzure by using Azure Site Recovery.</span></span>

## <a name="disaster-recovery-and-compliance"></a><span data-ttu-id="bce3f-107">Odzyskiwanie po awarii i zgodność</span><span class="sxs-lookup"><span data-stu-id="bce3f-107">Disaster recovery and compliance</span></span>
<span data-ttu-id="bce3f-108">Obecnie coraz więcej przedsiębiorstw przenosisz tooAzure ich obciążeń.</span><span class="sxs-lookup"><span data-stu-id="bce3f-108">Today, more and more enterprises are moving their workloads tooAzure.</span></span> <span data-ttu-id="bce3f-109">Z przedsiębiorstw przenoszenia produkcji krytycznym lokalnymi tooAzure obciążenia, konfigurowanie odzyskiwania po awarii dla tych zadań jest wymagana przez zgodności i toosafeguard przed jakichkolwiek potencjalnych zakłóceń w regionie platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="bce3f-109">With enterprises moving mission-critical on-premises production workloads tooAzure, setting up disaster recovery for these workloads is mandatory for compliance and toosafeguard against any disruptions in an Azure region.</span></span>

## <a name="steps-for-preparing-migrated-machines-for-replication"></a><span data-ttu-id="bce3f-110">Kroki przygotowania zmigrowanych maszyn do replikacji</span><span class="sxs-lookup"><span data-stu-id="bce3f-110">Steps for preparing migrated machines for replication</span></span>
<span data-ttu-id="bce3f-111">tooprepare zmigrowane maszyny do konfigurowania replikacji tooanother region platformy Azure:</span><span class="sxs-lookup"><span data-stu-id="bce3f-111">tooprepare migrated machines for setting up replication tooanother Azure region:</span></span>

1. <span data-ttu-id="bce3f-112">Kończenie migracji.</span><span class="sxs-lookup"><span data-stu-id="bce3f-112">Complete migration.</span></span>
2. <span data-ttu-id="bce3f-113">Zainstaluj hello Azure agenta, jeśli to konieczne.</span><span class="sxs-lookup"><span data-stu-id="bce3f-113">Install hello Azure agent if needed.</span></span>
3. <span data-ttu-id="bce3f-114">Usuń hello usługi mobilności.</span><span class="sxs-lookup"><span data-stu-id="bce3f-114">Remove hello Mobility service.</span></span>  
4. <span data-ttu-id="bce3f-115">Uruchom ponownie hello maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="bce3f-115">Restart hello VM.</span></span>

<span data-ttu-id="bce3f-116">Te kroki są opisane bardziej szczegółowo w hello następujące sekcje.</span><span class="sxs-lookup"><span data-stu-id="bce3f-116">These steps are described in more detail in hello following sections.</span></span>

### <a name="step-1-migrate-workloads-running-on-hyper-v-vms-vmware-vms-and-physical-servers-toorun-on-azure-vms"></a><span data-ttu-id="bce3f-117">Krok 1: Migracji obciążeń uruchomionych na maszynach wirtualnych funkcji Hyper-V, maszyn wirtualnych VMware i toorun serwerów fizycznych na maszynach wirtualnych Azure</span><span class="sxs-lookup"><span data-stu-id="bce3f-117">Step 1: Migrate workloads running on Hyper-V VMs, VMware VMs, and physical servers toorun on Azure VMs</span></span>

<span data-ttu-id="bce3f-118">tooset Konfigurowanie replikacji i migrację z lokalnej funkcji Hyper-V, VMware i tooAzure obciążeń fizycznych, wykonaj hello kroki opisane w hello [maszyn wirtualnych IaaS platformy Azure migracji między regiony platformy Azure z usługą Azure Site Recovery](site-recovery-migrate-to-azure.md) artykułu.</span><span class="sxs-lookup"><span data-stu-id="bce3f-118">tooset up replication and migrate your on-premises Hyper-V, VMware, and physical workloads tooAzure, follow hello steps in hello [Migrate Azure IaaS virtual machines between Azure regions with Azure Site Recovery](site-recovery-migrate-to-azure.md) article.</span></span> 

<span data-ttu-id="bce3f-119">Po migracji nie należy toocommit lub usunąć awarię.</span><span class="sxs-lookup"><span data-stu-id="bce3f-119">After migration, you don't need toocommit or delete a failover.</span></span> <span data-ttu-id="bce3f-120">Zamiast tego należy wybrać hello **przeprowadzenia migracji** opcji dla każdego komputera ma toomigrate:</span><span class="sxs-lookup"><span data-stu-id="bce3f-120">Instead, select hello **Complete Migration** option for each machine you want toomigrate:</span></span>
1. <span data-ttu-id="bce3f-121">W **elementy replikowane**, kliknij prawym przyciskiem myszy hello maszyny Wirtualnej i kliknij przycisk **przeprowadzenia migracji**.</span><span class="sxs-lookup"><span data-stu-id="bce3f-121">In **Replicated Items**, right-click hello VM, and click **Complete Migration**.</span></span> <span data-ttu-id="bce3f-122">Kliknij przycisk **OK** toocomplete hello kroku.</span><span class="sxs-lookup"><span data-stu-id="bce3f-122">Click **OK** toocomplete hello step.</span></span> <span data-ttu-id="bce3f-123">Możesz śledzić postępy hello właściwości maszyny Wirtualnej, monitorując hello zadanie przeprowadzenia migracji w **zadania usługi Site Recovery**.</span><span class="sxs-lookup"><span data-stu-id="bce3f-123">You can track progress in hello VM properties by monitoring hello Complete Migration job in **Site Recovery jobs**.</span></span>
2. <span data-ttu-id="bce3f-124">Witaj **przeprowadzenia migracji** akcji kończy proces migracji hello spowoduje usunięcie replikacji dla maszyny hello i zatrzymuje usługi Site Recovery rozliczeń hello maszyny.</span><span class="sxs-lookup"><span data-stu-id="bce3f-124">hello **Complete Migration** action completes hello migration process, removes replication for hello machine, and stops Site Recovery billing for hello machine.</span></span>

   ![pełna_migracja](./media/site-recovery-hyper-v-site-to-azure/migrate.png)

### <a name="step-2-install-hello-azure-vm-agent-on-hello-virtual-machine"></a><span data-ttu-id="bce3f-126">Krok 2: Zainstaluj agenta maszyny Wirtualnej Azure hello na maszynie wirtualnej hello</span><span class="sxs-lookup"><span data-stu-id="bce3f-126">Step 2: Install hello Azure VM agent on hello virtual machine</span></span>
<span data-ttu-id="bce3f-127">Hello Azure [agenta maszyny Wirtualnej](../virtual-machines/windows/classic/agents-and-extensions.md#azure-vm-agents-for-windows-and-linux) musi być zainstalowany na maszynie wirtualnej powitania dla toowork rozszerzenia usługi Site Recovery hello i toohelp chronić hello maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="bce3f-127">hello Azure [VM agent](../virtual-machines/windows/classic/agents-and-extensions.md#azure-vm-agents-for-windows-and-linux) must be installed on hello virtual machine for hello Site Recovery extension toowork and toohelp protect hello VM.</span></span>

>[!IMPORTANT]
><span data-ttu-id="bce3f-128">Począwszy od wersji 9.7.0.0, maszynach wirtualnych Windows hello mobilności usługi Instalator instaluje również hello najnowszych dostępnych agenta maszyny Wirtualnej Azure.</span><span class="sxs-lookup"><span data-stu-id="bce3f-128">Beginning with version 9.7.0.0, on Windows virtual machines, hello Mobility service installer also installs hello latest available Azure VM agent.</span></span> <span data-ttu-id="bce3f-129">Na migracji maszyny wirtualnej hello spełnia wymagań wstępnych dla przy użyciu dowolnego rozszerzenia maszyny Wirtualnej, tym rozszerzenie usługi Site Recovery hello instalacji agenta.</span><span class="sxs-lookup"><span data-stu-id="bce3f-129">On migration, hello virtual machine meets the agent installation prerequisite for using any VM extension, including hello Site Recovery extension.</span></span> <span data-ttu-id="bce3f-130">Hello maszyny Wirtualnej Azure agenta potrzeb toobe ręcznie zainstalować tylko wtedy, gdy hello usługi mobilności zainstalowane na powitania zmigrowaną maszynę jest wersja 9.6 lub starszym.</span><span class="sxs-lookup"><span data-stu-id="bce3f-130">hello Azure VM agent needs toobe manually installed only if hello Mobility service installed on hello migrated machine is version 9.6 or earlier.</span></span>

<span data-ttu-id="bce3f-131">Witaj Poniższa tabela zawiera dodatkowe informacje na temat instalowania agenta maszyny Wirtualnej hello i weryfikacji, że została zainstalowana:</span><span class="sxs-lookup"><span data-stu-id="bce3f-131">hello following table provides additional information about installing hello VM agent and validating that it was installed:</span></span>

| <span data-ttu-id="bce3f-132">**Operacja**</span><span class="sxs-lookup"><span data-stu-id="bce3f-132">**Operation**</span></span> | <span data-ttu-id="bce3f-133">**Windows**</span><span class="sxs-lookup"><span data-stu-id="bce3f-133">**Windows**</span></span> | <span data-ttu-id="bce3f-134">**Linux**</span><span class="sxs-lookup"><span data-stu-id="bce3f-134">**Linux**</span></span> |
| --- | --- | --- |
| <span data-ttu-id="bce3f-135">Instalowanie agenta maszyny Wirtualnej hello</span><span class="sxs-lookup"><span data-stu-id="bce3f-135">Installing hello VM agent</span></span> |<span data-ttu-id="bce3f-136">Pobierz i zainstaluj hello [pliku MSI agenta](http://go.microsoft.com/fwlink/?LinkID=394789&clcid=0x409).</span><span class="sxs-lookup"><span data-stu-id="bce3f-136">Download and install hello [agent MSI](http://go.microsoft.com/fwlink/?LinkID=394789&clcid=0x409).</span></span> <span data-ttu-id="bce3f-137">Potrzebujesz instalacji hello toocomplete uprawnienia administratora.</span><span class="sxs-lookup"><span data-stu-id="bce3f-137">You need administrator privileges toocomplete hello installation.</span></span> |<span data-ttu-id="bce3f-138">Zainstaluj najnowsze hello [agenta systemu Linux](../virtual-machines/linux/agent-user-guide.md).</span><span class="sxs-lookup"><span data-stu-id="bce3f-138">Install hello latest [Linux agent](../virtual-machines/linux/agent-user-guide.md).</span></span> <span data-ttu-id="bce3f-139">Potrzebujesz instalacji hello toocomplete uprawnienia administratora.</span><span class="sxs-lookup"><span data-stu-id="bce3f-139">You need administrator privileges toocomplete hello installation.</span></span> <span data-ttu-id="bce3f-140">Zaleca się zainstalowanie agenta hello z repozytorium dystrybucji.</span><span class="sxs-lookup"><span data-stu-id="bce3f-140">We recommend installing hello agent from your distribution repository.</span></span> <span data-ttu-id="bce3f-141">Firma Microsoft *nie jest zalecane* Instalowanie agenta maszyny Wirtualnej systemu Linux hello bezpośrednio z usługi GitHub.</span><span class="sxs-lookup"><span data-stu-id="bce3f-141">We *do not recommend* installing hello Linux VM agent directly from GitHub.</span></span>  |
| <span data-ttu-id="bce3f-142">Sprawdzanie poprawności instalacji agenta hello maszyny Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="bce3f-142">Validating hello VM agent installation</span></span> |<span data-ttu-id="bce3f-143">1. Przeglądaj toohello C:\WindowsAzure\Packages folderu w hello maszyny Wirtualnej platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="bce3f-143">1. Browse toohello C:\WindowsAzure\Packages folder in hello Azure VM.</span></span> <span data-ttu-id="bce3f-144">Powinny pojawić się hello WaAppAgent.exe pliku.</span><span class="sxs-lookup"><span data-stu-id="bce3f-144">You should see hello WaAppAgent.exe file.</span></span> <br><span data-ttu-id="bce3f-145">2. Kliknij prawym przyciskiem myszy plik hello znajduje się zbyt**właściwości**, a następnie wybierz hello **szczegóły** hello kartę **wersji produktu** pole powinno być 2.6.1198.718 lub nowszej.</span><span class="sxs-lookup"><span data-stu-id="bce3f-145">2. Right-click hello file, go too**Properties**, and then select hello **Details** tab. hello **Product Version** field should be 2.6.1198.718 or higher.</span></span> |<span data-ttu-id="bce3f-146">Nie dotyczy</span><span class="sxs-lookup"><span data-stu-id="bce3f-146">N/A</span></span> |


### <a name="step-3-remove-hello-mobility-service-from-hello-migrated-virtual-machine"></a><span data-ttu-id="bce3f-147">Krok 3: Usuń hello usługi mobilności ze hello zmigrowaną maszynę wirtualną</span><span class="sxs-lookup"><span data-stu-id="bce3f-147">Step 3: Remove hello Mobility service from hello migrated virtual machine</span></span>

<span data-ttu-id="bce3f-148">W przypadku migracji z lokalnych maszyn VMware lub serwerów fizycznych w systemie Windows/Linux, potrzebna usługa Usuń/odinstalowywanie mobilności hello toomanually z hello zmigrowane maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="bce3f-148">If you have migrated your on-premises VMware machines or physical servers on Windows/Linux, you need toomanually remove/uninstall hello Mobility service from hello migrated virtual machine.</span></span>

>[!IMPORTANT]
><span data-ttu-id="bce3f-149">Ten krok nie jest wymagane dla tooAzure zmigrowanych maszyn wirtualnych funkcji Hyper-V.</span><span class="sxs-lookup"><span data-stu-id="bce3f-149">This step is not required for Hyper-V VMs migrated tooAzure.</span></span>

#### <a name="uninstall-hello-mobility-service-on-a-windows-server-vm"></a><span data-ttu-id="bce3f-150">Odinstaluj hello usługi mobilności na maszynie Wirtualnej systemu Windows Server</span><span class="sxs-lookup"><span data-stu-id="bce3f-150">Uninstall hello Mobility service on a Windows Server VM</span></span>
<span data-ttu-id="bce3f-151">Użyj jednej z hello następujące usługi mobilności hello toouninstall metod na komputerze z systemem Windows Server.</span><span class="sxs-lookup"><span data-stu-id="bce3f-151">Use one of hello following methods toouninstall hello Mobility service on a Windows Server computer.</span></span>

##### <a name="uninstall-by-using-hello-windows-ui"></a><span data-ttu-id="bce3f-152">Odinstaluj za pomocą interfejsu użytkownika systemu Windows hello</span><span class="sxs-lookup"><span data-stu-id="bce3f-152">Uninstall by using hello Windows UI</span></span>
1. <span data-ttu-id="bce3f-153">Hello Panelu sterowania, wybierz **programy**.</span><span class="sxs-lookup"><span data-stu-id="bce3f-153">In hello Control Panel, select **Programs**.</span></span>
2. <span data-ttu-id="bce3f-154">Wybierz **Microsoft Azure Site odzyskiwania mobilności usługi/główny serwer docelowy**, a następnie wybierz **Odinstaluj**.</span><span class="sxs-lookup"><span data-stu-id="bce3f-154">Select **Microsoft Azure Site Recovery Mobility Service/Master Target server**, and then select **Uninstall**.</span></span>

##### <a name="uninstall-at-a-command-prompt"></a><span data-ttu-id="bce3f-155">Odinstaluj w wierszu polecenia</span><span class="sxs-lookup"><span data-stu-id="bce3f-155">Uninstall at a command prompt</span></span>
1. <span data-ttu-id="bce3f-156">Otwórz okno wiersza polecenia z uprawnieniami administratora.</span><span class="sxs-lookup"><span data-stu-id="bce3f-156">Open a Command Prompt window as an administrator.</span></span>
2. <span data-ttu-id="bce3f-157">toouninstall hello usługi mobilności, uruchom następujące polecenie hello:</span><span class="sxs-lookup"><span data-stu-id="bce3f-157">toouninstall hello Mobility service, run hello following command:</span></span>

   ```
   MsiExec.exe /qn /x {275197FC-14FD-4560-A5EB-38217F80CBD1} /L+*V "C:\ProgramData\ASRSetupLogs\UnifiedAgentMSIUninstall.log"
   ```

#### <a name="uninstall-hello-mobility-service-on-a-linux-computer"></a><span data-ttu-id="bce3f-158">Odinstaluj usługę mobilności hello na komputerze z systemem Linux</span><span class="sxs-lookup"><span data-stu-id="bce3f-158">Uninstall hello Mobility service on a Linux computer</span></span>
1. <span data-ttu-id="bce3f-159">Na serwerze Linux, zaloguj się jako **głównego** użytkownika.</span><span class="sxs-lookup"><span data-stu-id="bce3f-159">On your Linux server, sign in as a **root** user.</span></span>
2. <span data-ttu-id="bce3f-160">W terminalu Przejdź zbyt/użytkownik/lokalnej/funkcja automatycznego odzyskiwania systemu.</span><span class="sxs-lookup"><span data-stu-id="bce3f-160">In a terminal, go too/user/local/ASR.</span></span>
3. <span data-ttu-id="bce3f-161">toouninstall hello usługi mobilności, uruchom następujące polecenie hello:</span><span class="sxs-lookup"><span data-stu-id="bce3f-161">toouninstall hello Mobility service, run hello following command:</span></span>

   ```
   uninstall.sh -Y
   ```

### <a name="step-4-restart-hello-vm"></a><span data-ttu-id="bce3f-162">Krok 4: Hello ponownego uruchomienia maszyny Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="bce3f-162">Step 4: Restart hello VM</span></span>

<span data-ttu-id="bce3f-163">Po odinstalowaniu usługi mobilności hello hello ponownego uruchomienia maszyny Wirtualnej przed Konfigurowanie replikacji tooanother region platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="bce3f-163">After you uninstall hello Mobility service, restart hello VM before you set up replication tooanother Azure region.</span></span>


## <a name="next-steps"></a><span data-ttu-id="bce3f-164">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="bce3f-164">Next steps</span></span>
- <span data-ttu-id="bce3f-165">Włączyć ochronę obciążeń przez [replikowanie maszyn wirtualnych platformy Azure](site-recovery-azure-to-azure.md).</span><span class="sxs-lookup"><span data-stu-id="bce3f-165">Start protecting your workloads by [replicating Azure virtual machines](site-recovery-azure-to-azure.md).</span></span>
- <span data-ttu-id="bce3f-166">Dowiedz się więcej o [wskazówki dotyczące replikowanie maszyn wirtualnych platformy Azure networking](site-recovery-azure-to-azure-networking-guidance.md).</span><span class="sxs-lookup"><span data-stu-id="bce3f-166">Learn more about [networking guidance for replicating Azure virtual machines](site-recovery-azure-to-azure-networking-guidance.md).</span></span>
