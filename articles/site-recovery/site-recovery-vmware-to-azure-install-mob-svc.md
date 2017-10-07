---
title: "aaaInstall usługi mobilności (VMware lub fizycznych tooAzure) | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak tooinstall hello tooprotect agent usługi mobilności komputerów lokalnych."
services: site-recovery
documentationcenter: 
author: AnoopVasudavan
manager: gauravd
editor: 
ms.assetid: 
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: backup-recovery
ms.date: 06/29/2017
ms.author: anoopkv
ms.openlocfilehash: f7836e6b35d3838bae1eff927838ce4b245b9f56
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="install-mobility-service-vmware-or-physical-tooazure"></a><span data-ttu-id="72175-103">Zainstaluj usługę mobilności (VMware lub fizycznych tooAzure)</span><span class="sxs-lookup"><span data-stu-id="72175-103">Install Mobility Service (VMware or physical tooAzure)</span></span>
<span data-ttu-id="72175-104">Usługa mobilności Azure Site Recovery przechwytywania zapisów danych na komputerze i przekazuje je po toohello serwera przetwarzania.</span><span class="sxs-lookup"><span data-stu-id="72175-104">Azure Site Recovery Mobility Service captures data writes on a computer, and then forwards them toohello process server.</span></span> <span data-ttu-id="72175-105">Wdrażanie usługi mobilności tooevery komputera (maszyny Wirtualnej VMware lub serwerów fizycznych), które mają tooreplicate tooAzure.</span><span class="sxs-lookup"><span data-stu-id="72175-105">Deploy Mobility Service tooevery computer (VMware VM or physical server) that you want tooreplicate tooAzure.</span></span> <span data-ttu-id="72175-106">Można wdrożyć serwery toohello usługi mobilności, które mają tooprotect przy użyciu hello następujące metody:</span><span class="sxs-lookup"><span data-stu-id="72175-106">You can deploy Mobility Service toohello servers that you want tooprotect by using hello following methods:</span></span>


* [<span data-ttu-id="72175-107">Zainstaluj usługę mobilności przy użyciu narzędzia wdrażania oprogramowania takich jak System Center Configuration Manager</span><span class="sxs-lookup"><span data-stu-id="72175-107">Install Mobility Service by using software deployment tools like System Center Configuration Manager</span></span>](site-recovery-install-mobility-service-using-sccm.md)
* [<span data-ttu-id="72175-108">Zainstaluj usługę mobilności przy użyciu usługi Automatyzacja Azure i konfiguracji żądanego stanu (DSC automatyzacji)</span><span class="sxs-lookup"><span data-stu-id="72175-108">Install Mobility Service by using Azure Automation and Desired State Configuration (Automation DSC)</span></span>](site-recovery-automate-mobility-service-install.md)
* [<span data-ttu-id="72175-109">Ręcznie zainstalować usługi mobilności przy użyciu hello graficzny interfejs użytkownika (GUI)</span><span class="sxs-lookup"><span data-stu-id="72175-109">Install Mobility Service manually by using hello graphical user interface (GUI)</span></span>](site-recovery-vmware-to-azure-install-mob-svc.md#install-mobility-service-manually-by-using-the-gui)
* [<span data-ttu-id="72175-110">Ręcznie zainstalować usługi mobilności w wierszu polecenia</span><span class="sxs-lookup"><span data-stu-id="72175-110">Install Mobility Service manually at a command prompt</span></span>](site-recovery-vmware-to-azure-install-mob-svc.md#install-mobility-service-manually-at-a-command-prompt)
* [<span data-ttu-id="72175-111">Zainstaluj usługę mobilności przez instalację wypychaną z usługi Azure Site Recovery</span><span class="sxs-lookup"><span data-stu-id="72175-111">Install Mobility Service by push installation from Azure Site Recovery</span></span>](site-recovery-vmware-to-azure-install-mob-svc.md#install-mobility-service-by-push-installation-from-azure-site-recovery)


>[!IMPORTANT]
> <span data-ttu-id="72175-112">Począwszy od wersji 9.7.0.0, na maszynach wirtualnych systemu Windows (VM), hello usługi mobilności Instalator instaluje również hello najnowszych dostępnych [agenta maszyny Wirtualnej Azure](../virtual-machines/windows/extensions-features.md#azure-vm-agent).</span><span class="sxs-lookup"><span data-stu-id="72175-112">Beginning with version 9.7.0.0, on Windows virtual machines (VMs), hello Mobility Service installer also installs hello latest available [Azure VM agent](../virtual-machines/windows/extensions-features.md#azure-vm-agent).</span></span> <span data-ttu-id="72175-113">W przypadku awarii komputera za pośrednictwem tooAzure hello komputer spełnia instalacji agenta hello wymagań wstępnych dla dowolnego rozszerzenia maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="72175-113">When a computer fails over tooAzure, hello computer meets hello agent installation prerequisite for using any VM extension.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="72175-114">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="72175-114">Prerequisites</span></span>
<span data-ttu-id="72175-115">Wykonaj następujące kroki wymagań wstępnych, aby ręcznie zainstalować usługi mobilności na serwerze:</span><span class="sxs-lookup"><span data-stu-id="72175-115">Complete these prerequisite steps before you manually install Mobility Service on your server:</span></span>
1. <span data-ttu-id="72175-116">Zaloguj się tooyour konfiguracji serwera, a następnie otwórz okno wiersza polecenia z uprawnieniami administratora.</span><span class="sxs-lookup"><span data-stu-id="72175-116">Sign in tooyour configuration server, and then open a Command Prompt window as an administrator.</span></span>
2. <span data-ttu-id="72175-117">Zmień folder bin toohello hello w katalogu, a następnie utwórz plik hasło:</span><span class="sxs-lookup"><span data-stu-id="72175-117">Change hello directory toohello bin folder, and then create a passphrase file:</span></span>

    ```
    cd %ProgramData%\ASR\home\svsystems\bin
    genpassphrase.exe -v > MobSvc.passphrase
    ```
3. <span data-ttu-id="72175-118">Plik hasło hello należy przechowywać w bezpiecznej lokalizacji.</span><span class="sxs-lookup"><span data-stu-id="72175-118">Store hello passphrase file in a secure location.</span></span> <span data-ttu-id="72175-119">Korzystanie z pliku hello podczas hello instalacji usługi mobilności.</span><span class="sxs-lookup"><span data-stu-id="72175-119">You use hello file during hello Mobility Service installation.</span></span>
4. <span data-ttu-id="72175-120">Instalatorzy usługę mobilności dla wszystkich obsługiwanych systemów operacyjnych znajdują się w folderze %ProgramData%\ASR\home\svsystems\pushinstallsvc\repository hello.</span><span class="sxs-lookup"><span data-stu-id="72175-120">Mobility Service installers for all supported operating systems are in hello %ProgramData%\ASR\home\svsystems\pushinstallsvc\repository folder.</span></span>

### <a name="mobility-service-installer-to-operating-system-mapping"></a><span data-ttu-id="72175-121">Mapowanie systemu Instalator działania usługi mobilności</span><span class="sxs-lookup"><span data-stu-id="72175-121">Mobility Service installer-to-operating system mapping</span></span>

| <span data-ttu-id="72175-122">Nazwa szablonu pliku Instalatora</span><span class="sxs-lookup"><span data-stu-id="72175-122">Installer file template name</span></span>| <span data-ttu-id="72175-123">System operacyjny</span><span class="sxs-lookup"><span data-stu-id="72175-123">Operating system</span></span> |
|---|--|
|<span data-ttu-id="72175-124">Usługa ASR Microsoft\_UA\*Windows\*release.exe</span><span class="sxs-lookup"><span data-stu-id="72175-124">Microsoft-ASR\_UA\*Windows\*release.exe</span></span> | <span data-ttu-id="72175-125">Windows Server 2008 R2 z dodatkiem SP1 (64-bitowe)</span><span class="sxs-lookup"><span data-stu-id="72175-125">Windows Server 2008 R2 SP1 (64-bit)</span></span> </br> <span data-ttu-id="72175-126">Windows Server 2012 (64-bitowe)</span><span class="sxs-lookup"><span data-stu-id="72175-126">Windows Server 2012 (64-bit)</span></span> </br> <span data-ttu-id="72175-127">Windows Server 2012 R2 (64-bitowe)</span><span class="sxs-lookup"><span data-stu-id="72175-127">Windows Server 2012 R2 (64-bit)</span></span> |
|<span data-ttu-id="72175-128">Usługa ASR Microsoft\_UA\*RHEL6 64*release.tar.gz</span><span class="sxs-lookup"><span data-stu-id="72175-128">Microsoft-ASR\_UA\*RHEL6-64*release.tar.gz</span></span>| <span data-ttu-id="72175-129">Red Hat Enterprise Linux (RHEL) 6.4, 6.5, 6.6, 6.7, 6.8 (tylko wersja 64-bitowa)</span><span class="sxs-lookup"><span data-stu-id="72175-129">Red Hat Enterprise Linux (RHEL) 6.4, 6.5, 6.6, 6.7, 6.8 (64-bit only)</span></span> </br> <span data-ttu-id="72175-130">CentOS 6.4, 6.5, 6.6, 6.7, 6.8 (tylko wersja 64-bitowa)</span><span class="sxs-lookup"><span data-stu-id="72175-130">CentOS 6.4, 6.5, 6.6, 6.7, 6.8 (64-bit only)</span></span> |
|<span data-ttu-id="72175-131">Usługa ASR Microsoft\_UA\*RHEL7 64\*release.tar.gz</span><span class="sxs-lookup"><span data-stu-id="72175-131">Microsoft-ASR\_UA\*RHEL7-64\*release.tar.gz</span></span> | <span data-ttu-id="72175-132">Red Hat Enterprise Linux (RHEL) 7.1, 7.2 (tylko wersja 64-bitowa)</span><span class="sxs-lookup"><span data-stu-id="72175-132">Red Hat Enterprise Linux (RHEL) 7.1, 7.2 (64-bit only)</span></span> </br> <span data-ttu-id="72175-133">CentOS 7.0, 7.1, 7.2 (tylko wersja 64-bitowa)</span><span class="sxs-lookup"><span data-stu-id="72175-133">CentOS 7.0, 7.1, 7.2 (64-bit only)</span></span></br> <span data-ttu-id="72175-134">CentOs 7.3 (migracja)</span><span class="sxs-lookup"><span data-stu-id="72175-134">CentOs 7.3 (migration only)</span></span> |
|<span data-ttu-id="72175-135">Usługa ASR Microsoft\_UA\*SLES11-SP3-64\*release.tar.gz</span><span class="sxs-lookup"><span data-stu-id="72175-135">Microsoft-ASR\_UA\*SLES11-SP3-64\*release.tar.gz</span></span>| <span data-ttu-id="72175-136">SUSE Linux Enterprise Server 11 z dodatkiem SP3 (tylko wersja 64-bitowa)</span><span class="sxs-lookup"><span data-stu-id="72175-136">SUSE Linux Enterprise Server 11 SP3 (64-bit only)</span></span>|
|<span data-ttu-id="72175-137">Usługa ASR Microsoft\_UA\*SLES11-SP4-64\*release.tar.gz</span><span class="sxs-lookup"><span data-stu-id="72175-137">Microsoft-ASR\_UA\*SLES11-SP4-64\*release.tar.gz</span></span>| <span data-ttu-id="72175-138">SUSE Linux Enterprise Server 11 z dodatkiem SP4 (tylko wersja 64-bitowa)</span><span class="sxs-lookup"><span data-stu-id="72175-138">SUSE Linux Enterprise Server 11 SP4 (64-bit only)</span></span>|
|<span data-ttu-id="72175-139">Usługa ASR Microsoft\_UA\*OL6 64\*release.tar.gz</span><span class="sxs-lookup"><span data-stu-id="72175-139">Microsoft-ASR\_UA\*OL6-64\*release.tar.gz</span></span> | <span data-ttu-id="72175-140">Oracle Linux przedsiębiorstwa 6.4, 6.5 (tylko wersja 64-bitowa)</span><span class="sxs-lookup"><span data-stu-id="72175-140">Oracle Enterprise Linux 6.4, 6.5 (64-bit only)</span></span>|
|<span data-ttu-id="72175-141">Usługa ASR Microsoft\_UA\*UBUNTU-14.04-64\*release.tar.gz</span><span class="sxs-lookup"><span data-stu-id="72175-141">Microsoft-ASR\_UA\*UBUNTU-14.04-64\*release.tar.gz</span></span> | <span data-ttu-id="72175-142">Ubuntu Linux 14.04 (tylko wersja 64-bitowa)</span><span class="sxs-lookup"><span data-stu-id="72175-142">Ubuntu Linux 14.04 (64-bit only)</span></span>|


## <a name="install-mobility-service-manually-by-using-hello-gui"></a><span data-ttu-id="72175-143">Ręcznie zainstalować usługi mobilności za pomocą interfejsu GUI hello</span><span class="sxs-lookup"><span data-stu-id="72175-143">Install Mobility Service manually by using hello GUI</span></span>

>[!IMPORTANT]
> <span data-ttu-id="72175-144">Jeśli używasz **serwera konfiguracji** tooreplicate **maszyny wirtualne Azure IaaS** z jednego tooanother następnie wybrano subskrypcji Azure **użyć wiersza polecenia instalacji opartą na powitania**  — metoda</span><span class="sxs-lookup"><span data-stu-id="72175-144">If you are using a **Configuration Server** tooreplicate **Azure IaaS virtual machines** from one Azure Subscription/Region tooanother then **use hello Command-line based installation** method</span></span>

[!INCLUDE [site-recovery-install-mob-svc-gui](../../includes/site-recovery-install-mob-svc-gui.md)]

## <a name="install-mobility-service-manually-at-a-command-prompt"></a><span data-ttu-id="72175-145">Ręcznie zainstalować usługi mobilności w wierszu polecenia</span><span class="sxs-lookup"><span data-stu-id="72175-145">Install Mobility Service manually at a command prompt</span></span>

### <a name="command-line-installation-on-a-windows-computer"></a><span data-ttu-id="72175-146">Instalacja wiersza polecenia na komputerze z systemem Windows</span><span class="sxs-lookup"><span data-stu-id="72175-146">Command-line installation on a Windows computer</span></span>
[!INCLUDE [site-recovery-install-mob-svc-win-cmd](../../includes/site-recovery-install-mob-svc-win-cmd.md)]

### <a name="command-line-installation-on-a-linux-computer"></a><span data-ttu-id="72175-147">Instalacja wiersza polecenia na komputerze z systemem Linux</span><span class="sxs-lookup"><span data-stu-id="72175-147">Command-line installation on a Linux computer</span></span>
[!INCLUDE [site-recovery-install-mob-svc-lin-cmd](../../includes/site-recovery-install-mob-svc-lin-cmd.md)]


## <a name="install-mobility-service-by-push-installation-from-azure-site-recovery"></a><span data-ttu-id="72175-148">Zainstaluj usługę mobilności przez instalację wypychaną z usługi Azure Site Recovery</span><span class="sxs-lookup"><span data-stu-id="72175-148">Install Mobility Service by push installation from Azure Site Recovery</span></span>
<span data-ttu-id="72175-149">toodo instalacji wypychanej usługi mobilności przy użyciu usługi Site Recovery, wszystkich komputerach docelowych musi spełniać następujące wymagania wstępne hello.</span><span class="sxs-lookup"><span data-stu-id="72175-149">toodo a push installation of Mobility Service by using Site Recovery, all target computers must meet hello following prerequisites.</span></span>

[!INCLUDE [site-recovery-prepare-push-install-mob-svc-win](../../includes/site-recovery-prepare-push-install-mob-svc-win.md)]

[!INCLUDE [site-recovery-prepare-push-install-mob-svc-lin](../../includes/site-recovery-prepare-push-install-mob-svc-lin.md)]


> [!NOTE]
<span data-ttu-id="72175-150">Po zainstalowaniu usługi mobilności w hello portalu Azure, wybierz hello **replikować** toostart przycisk ochrony tych maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="72175-150">After Mobility Service is installed, in hello Azure portal, select hello **Replicate** button toostart protecting these VMs.</span></span>

## <a name="uninstall-mobility-service-on-a-windows-server-computer"></a><span data-ttu-id="72175-151">Odinstalować usługi mobilności na komputerze z systemem Windows Server</span><span class="sxs-lookup"><span data-stu-id="72175-151">Uninstall Mobility Service on a Windows Server computer</span></span>
<span data-ttu-id="72175-152">Użyj jednej z hello następujące metody toouninstall usługi mobilności na komputerze z systemem Windows Server.</span><span class="sxs-lookup"><span data-stu-id="72175-152">Use one of hello following methods toouninstall Mobility Service on a Windows Server computer.</span></span>

### <a name="uninstall-by-using-hello-gui"></a><span data-ttu-id="72175-153">Odinstaluj za pomocą interfejsu GUI hello</span><span class="sxs-lookup"><span data-stu-id="72175-153">Uninstall by using hello GUI</span></span>
1. <span data-ttu-id="72175-154">W Panelu sterowania, wybierz **programy**.</span><span class="sxs-lookup"><span data-stu-id="72175-154">In Control Panel, select **Programs**.</span></span>
2. <span data-ttu-id="72175-155">Wybierz **Microsoft Azure Site odzyskiwania mobilności usługi/główny serwer docelowy**, a następnie wybierz **Odinstaluj**.</span><span class="sxs-lookup"><span data-stu-id="72175-155">Select **Microsoft Azure Site Recovery Mobility Service/Master Target server**, and then select **Uninstall**.</span></span>

### <a name="uninstall-at-a-command-prompt"></a><span data-ttu-id="72175-156">Odinstaluj w wierszu polecenia</span><span class="sxs-lookup"><span data-stu-id="72175-156">Uninstall at a command prompt</span></span>
1. <span data-ttu-id="72175-157">Otwórz okno wiersza polecenia z uprawnieniami administratora.</span><span class="sxs-lookup"><span data-stu-id="72175-157">Open a Command Prompt window as an administrator.</span></span>
2. <span data-ttu-id="72175-158">toouninstall usługi mobilności, uruchom następujące polecenie hello:</span><span class="sxs-lookup"><span data-stu-id="72175-158">toouninstall Mobility Service, run hello following command:</span></span>

```
MsiExec.exe /qn /x {275197FC-14FD-4560-A5EB-38217F80CBD1} /L+*V "C:\ProgramData\ASRSetupLogs\UnifiedAgentMSIUninstall.log"
```

## <a name="uninstall-mobility-service-on-a-linux-computer"></a><span data-ttu-id="72175-159">Odinstalować usługi mobilności na komputerze z systemem Linux</span><span class="sxs-lookup"><span data-stu-id="72175-159">Uninstall Mobility Service on a Linux computer</span></span>
1. <span data-ttu-id="72175-160">Na serwerze Linux, zaloguj się jako **głównego** użytkownika.</span><span class="sxs-lookup"><span data-stu-id="72175-160">On your Linux server, sign in as a **root** user.</span></span>
2. <span data-ttu-id="72175-161">W terminalu Przejdź zbyt/użytkownik/lokalnej/funkcja automatycznego odzyskiwania systemu.</span><span class="sxs-lookup"><span data-stu-id="72175-161">In a terminal, go too/user/local/ASR.</span></span>
3. <span data-ttu-id="72175-162">toouninstall usługi mobilności, uruchom następujące polecenie hello:</span><span class="sxs-lookup"><span data-stu-id="72175-162">toouninstall Mobility Service, run hello following command:</span></span>

```
uninstall.sh -Y
```
