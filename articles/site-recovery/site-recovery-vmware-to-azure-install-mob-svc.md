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
# <a name="install-mobility-service-vmware-or-physical-tooazure"></a>Zainstaluj usługę mobilności (VMware lub fizycznych tooAzure)
Usługa mobilności Azure Site Recovery przechwytywania zapisów danych na komputerze i przekazuje je po toohello serwera przetwarzania. Wdrażanie usługi mobilności tooevery komputera (maszyny Wirtualnej VMware lub serwerów fizycznych), które mają tooreplicate tooAzure. Można wdrożyć serwery toohello usługi mobilności, które mają tooprotect przy użyciu hello następujące metody:


* [Zainstaluj usługę mobilności przy użyciu narzędzia wdrażania oprogramowania takich jak System Center Configuration Manager](site-recovery-install-mobility-service-using-sccm.md)
* [Zainstaluj usługę mobilności przy użyciu usługi Automatyzacja Azure i konfiguracji żądanego stanu (DSC automatyzacji)](site-recovery-automate-mobility-service-install.md)
* [Ręcznie zainstalować usługi mobilności przy użyciu hello graficzny interfejs użytkownika (GUI)](site-recovery-vmware-to-azure-install-mob-svc.md#install-mobility-service-manually-by-using-the-gui)
* [Ręcznie zainstalować usługi mobilności w wierszu polecenia](site-recovery-vmware-to-azure-install-mob-svc.md#install-mobility-service-manually-at-a-command-prompt)
* [Zainstaluj usługę mobilności przez instalację wypychaną z usługi Azure Site Recovery](site-recovery-vmware-to-azure-install-mob-svc.md#install-mobility-service-by-push-installation-from-azure-site-recovery)


>[!IMPORTANT]
> Począwszy od wersji 9.7.0.0, na maszynach wirtualnych systemu Windows (VM), hello usługi mobilności Instalator instaluje również hello najnowszych dostępnych [agenta maszyny Wirtualnej Azure](../virtual-machines/windows/extensions-features.md#azure-vm-agent). W przypadku awarii komputera za pośrednictwem tooAzure hello komputer spełnia instalacji agenta hello wymagań wstępnych dla dowolnego rozszerzenia maszyny Wirtualnej.

## <a name="prerequisites"></a>Wymagania wstępne
Wykonaj następujące kroki wymagań wstępnych, aby ręcznie zainstalować usługi mobilności na serwerze:
1. Zaloguj się tooyour konfiguracji serwera, a następnie otwórz okno wiersza polecenia z uprawnieniami administratora.
2. Zmień folder bin toohello hello w katalogu, a następnie utwórz plik hasło:

    ```
    cd %ProgramData%\ASR\home\svsystems\bin
    genpassphrase.exe -v > MobSvc.passphrase
    ```
3. Plik hasło hello należy przechowywać w bezpiecznej lokalizacji. Korzystanie z pliku hello podczas hello instalacji usługi mobilności.
4. Instalatorzy usługę mobilności dla wszystkich obsługiwanych systemów operacyjnych znajdują się w folderze %ProgramData%\ASR\home\svsystems\pushinstallsvc\repository hello.

### <a name="mobility-service-installer-to-operating-system-mapping"></a>Mapowanie systemu Instalator działania usługi mobilności

| Nazwa szablonu pliku Instalatora| System operacyjny |
|---|--|
|Usługa ASR Microsoft\_UA\*Windows\*release.exe | Windows Server 2008 R2 z dodatkiem SP1 (64-bitowe) </br> Windows Server 2012 (64-bitowe) </br> Windows Server 2012 R2 (64-bitowe) |
|Usługa ASR Microsoft\_UA\*RHEL6 64*release.tar.gz| Red Hat Enterprise Linux (RHEL) 6.4, 6.5, 6.6, 6.7, 6.8 (tylko wersja 64-bitowa) </br> CentOS 6.4, 6.5, 6.6, 6.7, 6.8 (tylko wersja 64-bitowa) |
|Usługa ASR Microsoft\_UA\*RHEL7 64\*release.tar.gz | Red Hat Enterprise Linux (RHEL) 7.1, 7.2 (tylko wersja 64-bitowa) </br> CentOS 7.0, 7.1, 7.2 (tylko wersja 64-bitowa)</br> CentOs 7.3 (migracja) |
|Usługa ASR Microsoft\_UA\*SLES11-SP3-64\*release.tar.gz| SUSE Linux Enterprise Server 11 z dodatkiem SP3 (tylko wersja 64-bitowa)|
|Usługa ASR Microsoft\_UA\*SLES11-SP4-64\*release.tar.gz| SUSE Linux Enterprise Server 11 z dodatkiem SP4 (tylko wersja 64-bitowa)|
|Usługa ASR Microsoft\_UA\*OL6 64\*release.tar.gz | Oracle Linux przedsiębiorstwa 6.4, 6.5 (tylko wersja 64-bitowa)|
|Usługa ASR Microsoft\_UA\*UBUNTU-14.04-64\*release.tar.gz | Ubuntu Linux 14.04 (tylko wersja 64-bitowa)|


## <a name="install-mobility-service-manually-by-using-hello-gui"></a>Ręcznie zainstalować usługi mobilności za pomocą interfejsu GUI hello

>[!IMPORTANT]
> Jeśli używasz **serwera konfiguracji** tooreplicate **maszyny wirtualne Azure IaaS** z jednego tooanother następnie wybrano subskrypcji Azure **użyć wiersza polecenia instalacji opartą na powitania**  — metoda

[!INCLUDE [site-recovery-install-mob-svc-gui](../../includes/site-recovery-install-mob-svc-gui.md)]

## <a name="install-mobility-service-manually-at-a-command-prompt"></a>Ręcznie zainstalować usługi mobilności w wierszu polecenia

### <a name="command-line-installation-on-a-windows-computer"></a>Instalacja wiersza polecenia na komputerze z systemem Windows
[!INCLUDE [site-recovery-install-mob-svc-win-cmd](../../includes/site-recovery-install-mob-svc-win-cmd.md)]

### <a name="command-line-installation-on-a-linux-computer"></a>Instalacja wiersza polecenia na komputerze z systemem Linux
[!INCLUDE [site-recovery-install-mob-svc-lin-cmd](../../includes/site-recovery-install-mob-svc-lin-cmd.md)]


## <a name="install-mobility-service-by-push-installation-from-azure-site-recovery"></a>Zainstaluj usługę mobilności przez instalację wypychaną z usługi Azure Site Recovery
toodo instalacji wypychanej usługi mobilności przy użyciu usługi Site Recovery, wszystkich komputerach docelowych musi spełniać następujące wymagania wstępne hello.

[!INCLUDE [site-recovery-prepare-push-install-mob-svc-win](../../includes/site-recovery-prepare-push-install-mob-svc-win.md)]

[!INCLUDE [site-recovery-prepare-push-install-mob-svc-lin](../../includes/site-recovery-prepare-push-install-mob-svc-lin.md)]


> [!NOTE]
Po zainstalowaniu usługi mobilności w hello portalu Azure, wybierz hello **replikować** toostart przycisk ochrony tych maszyn wirtualnych.

## <a name="uninstall-mobility-service-on-a-windows-server-computer"></a>Odinstalować usługi mobilności na komputerze z systemem Windows Server
Użyj jednej z hello następujące metody toouninstall usługi mobilności na komputerze z systemem Windows Server.

### <a name="uninstall-by-using-hello-gui"></a>Odinstaluj za pomocą interfejsu GUI hello
1. W Panelu sterowania, wybierz **programy**.
2. Wybierz **Microsoft Azure Site odzyskiwania mobilności usługi/główny serwer docelowy**, a następnie wybierz **Odinstaluj**.

### <a name="uninstall-at-a-command-prompt"></a>Odinstaluj w wierszu polecenia
1. Otwórz okno wiersza polecenia z uprawnieniami administratora.
2. toouninstall usługi mobilności, uruchom następujące polecenie hello:

```
MsiExec.exe /qn /x {275197FC-14FD-4560-A5EB-38217F80CBD1} /L+*V "C:\ProgramData\ASRSetupLogs\UnifiedAgentMSIUninstall.log"
```

## <a name="uninstall-mobility-service-on-a-linux-computer"></a>Odinstalować usługi mobilności na komputerze z systemem Linux
1. Na serwerze Linux, zaloguj się jako **głównego** użytkownika.
2. W terminalu Przejdź zbyt/użytkownik/lokalnej/funkcja automatycznego odzyskiwania systemu.
3. toouninstall usługi mobilności, uruchom następujące polecenie hello:

```
uninstall.sh -Y
```
