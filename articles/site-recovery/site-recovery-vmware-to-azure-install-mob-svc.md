---
title: "Zainstaluj usługę mobilności (VMware lub fizycznych do platformy Azure) | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak zainstalować usługi mobilności agenta do ochrony komputerów lokalnych."
services: site-recovery
documentationcenter: 
author: AnoopVasudavan
manager: gauravd
ms.service: site-recovery
ms.topic: article
ms.date: 01/11/2018
ms.author: anoopkv
ms.openlocfilehash: 939115aedd624dde637f00c02865b1adab47c7c4
ms.sourcegitcommit: 7edfa9fbed0f9e274209cec6456bf4a689a4c1a6
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 01/17/2018
---
# <a name="install-mobility-service-vmware-or-physical-to-azure"></a>Zainstaluj usługę mobilności (VMware lub fizycznych do platformy Azure)
Usługa mobilności Azure Site Recovery przechwytywania zapisów danych na komputerze, a następnie przekazuje je do serwera przetwarzania. Wdrażanie usługi mobilności na każdym komputerze (maszyny Wirtualnej VMware lub serwerów fizycznych), który chcesz replikować do platformy Azure. Usługa mobilności można wdrożyć na serwerach, które mają być chronione przy użyciu następujących metod:


* [Zainstaluj usługę mobilności przy użyciu narzędzia wdrażania oprogramowania takich jak System Center Configuration Manager](site-recovery-install-mobility-service-using-sccm.md)
* [Zainstaluj usługę mobilności przy użyciu usługi Automatyzacja Azure i konfiguracji żądanego stanu (DSC automatyzacji)](site-recovery-automate-mobility-service-install.md)
* [Ręcznie zainstalować usługi mobilności przy użyciu graficznego interfejsu użytkownika (GUI)](site-recovery-vmware-to-azure-install-mob-svc.md#install-mobility-service-manually-by-using-the-gui)
* [Ręcznie zainstalować usługi mobilności w wierszu polecenia](site-recovery-vmware-to-azure-install-mob-svc.md#install-mobility-service-manually-at-a-command-prompt)
* [Zainstaluj usługę mobilności przez instalację wypychaną z usługi Site Recovery](site-recovery-vmware-to-azure-install-mob-svc.md#install-mobility-service-by-push-installation-from-azure-site-recovery)


>[!IMPORTANT]
> Począwszy od wersji 9.7.0.0, na maszynach wirtualnych systemu Windows (VM), usługa mobilności Instalator instaluje również najnowszym dostępnym [agenta maszyny Wirtualnej Azure](../virtual-machines/windows/extensions-features.md#azure-vm-agent). W przypadku awarii komputera za pośrednictwem Azure komputer spełnia wymagań wstępnych dla dowolnego rozszerzenia maszyny Wirtualnej instalacji agenta.

## <a name="prerequisites"></a>Wymagania wstępne
Wykonaj następujące kroki wymagań wstępnych, aby ręcznie zainstalować usługi mobilności na serwerze:
1. Zaloguj się do konfiguracji serwera, a następnie otwórz okno wiersza polecenia z uprawnieniami administratora.
2. Zmień katalog na bin folder, a następnie utwórz plik hasło:

    ```
    cd %ProgramData%\ASR\home\svsystems\bin
    genpassphrase.exe -v > MobSvc.passphrase
    ```
3. Przechowuj plik hasła w bezpiecznym miejscu. Możesz użyć pliku podczas instalacji usługi mobilności.
4. Instalatorzy usługę mobilności dla wszystkich obsługiwanych systemów operacyjnych znajdują się w folderze %ProgramData%\ASR\home\svsystems\pushinstallsvc\repository.

### <a name="mobility-service-installer-to-operating-system-mapping"></a>Mapowanie systemu Instalator działania usługi mobilności

| Nazwa szablonu pliku Instalatora| System operacyjny |
|---|--|
|Microsoft-ASR\_UA\*Windows\*release.exe | Windows Server 2008 R2 z dodatkiem SP1 (64-bitowe) </br> Windows Server 2012 (64-bitowe) </br> Windows Server 2012 R2 (64-bitowe) </br> Windows Server 2016 (64-bitowe) |
|Microsoft-ASR\_UA\*RHEL6-64*release.tar.gz| Red Hat Enterprise Linux (RHEL) 6.4, 6.5, 6.6, 6.7, 6.8, 6,9 (tylko wersja 64-bitowa) </br> CentOS 6.4, 6.5, 6.6, 6.7, 6.8, 6,9 (tylko wersja 64-bitowa) |
|Microsoft-ASR\_UA\*RHEL7-64\*release.tar.gz | Red Hat Enterprise Linux (RHEL) 7.1, 7.2, 7.3 (tylko wersja 64-bitowa) </br> CentOS 7.0, 7.1, 7.2, 7.3 (tylko wersja 64-bitowa) |
|Microsoft-ASR\_UA\*SLES11-SP3-64\*release.tar.gz| SUSE Linux Enterprise Server 11 z dodatkiem SP3 (tylko wersja 64-bitowa)|
|Microsoft-ASR\_UA\*SLES11-SP4-64\*release.tar.gz| SUSE Linux Enterprise Server 11 z dodatkiem SP4 (tylko wersja 64-bitowa)|
|Microsoft-ASR\_UA\*OL6-64\*release.tar.gz | Oracle Linux przedsiębiorstwa 6.4, 6.5 (tylko wersja 64-bitowa)|
|Microsoft-ASR\_UA\*UBUNTU-14.04-64\*release.tar.gz | Ubuntu Linux 14.04 (tylko wersja 64-bitowa)|
|Microsoft-ASR\_UA\*UBUNTU-16.04-64\*release.tar.gz | Ubuntu Linux 16.04 LTS serwera (tylko wersja 64-bitowa)|
|Microsoft-ASR_UA\*DEBIAN7-64\*release.tar.gz | Debian 7 (tylko wersja 64-bitowa)|
|Microsoft-ASR_UA\*DEBIAN8-64\*release.tar.gz | Debian 8 (tylko wersja 64-bitowa)|


## <a name="install-mobility-service-manually-by-using-the-gui"></a>Ręcznie zainstalować usługi mobilności przy użyciu graficznego interfejsu użytkownika

>[!IMPORTANT]
> Jeśli używasz **serwera konfiguracji** replikacji **maszyny wirtualne Azure IaaS** z jednego Azure subskrypcji/regionu do innego następnie **używać opartego na wierszu polecenia instalacji** — metoda

[!INCLUDE [site-recovery-install-mob-svc-gui](../../includes/site-recovery-install-mob-svc-gui.md)]

## <a name="install-mobility-service-manually-at-a-command-prompt"></a>Ręcznie zainstalować usługi mobilności w wierszu polecenia

### <a name="command-line-installation-on-a-windows-computer"></a>Instalacja wiersza polecenia na komputerze z systemem Windows
[!INCLUDE [site-recovery-install-mob-svc-win-cmd](../../includes/site-recovery-install-mob-svc-win-cmd.md)]

### <a name="command-line-installation-on-a-linux-computer"></a>Instalacja wiersza polecenia na komputerze z systemem Linux
[!INCLUDE [site-recovery-install-mob-svc-lin-cmd](../../includes/site-recovery-install-mob-svc-lin-cmd.md)]


## <a name="install-mobility-service-by-push-installation-from-azure-site-recovery"></a>Zainstaluj usługę mobilności przez instalację wypychaną z usługi Azure Site Recovery
Przeprowadzenie instalacji wypychanej usługi mobilności przy użyciu usługi Site Recovery, wszystkich komputerach docelowych musi spełniać następujące wymagania wstępne:

[!INCLUDE [site-recovery-prepare-push-install-mob-svc-win](../../includes/site-recovery-prepare-push-install-mob-svc-win.md)]

[!INCLUDE [site-recovery-prepare-push-install-mob-svc-lin](../../includes/site-recovery-prepare-push-install-mob-svc-lin.md)]


> [!NOTE]
Po zainstalowaniu usługi mobilności w portalu Azure wybierz **+ Replikuj** przycisk, aby rozpocząć ochronę tych maszyn wirtualnych.

## <a name="update-mobility-service"></a>Aktualizacja usługi mobilności

> [!WARNING]
> Sprawdź, czy serwer konfiguracji, skalowalnych w poziomie serwerów przetwarzania i główny cel serwery są częścią wdrożenia aktualizacji przed rozpoczęciem aktualizacji usługi Mobility na chronionych serwerach.

1. W portalu Azure przejdź na <Your Vault> -> Wyświetl elementy replikowane.
2. Jeśli **serwera konfiguracji** został już zaktualizowany do najnowszej wersji, a następnie powinny pojawić się powiadomienie, które odczytuje *jest dostępna aktualizacja agenta replikacji odzyskiwania nowej lokacji. Kliknij, aby zainstalować*

     ![ReplicatedItems](.\media\site-recovery-vmware-to-azure-install-mob-svc\replicated-item-notif.png)
3. Kliknij powiadomienie, aby otworzyć stronę wyboru maszyny wirtualnej.
4. Wybierz maszyny wirtualne, które chcesz uaktualnić usługi mobilności na & kliknij przycisk OK.

     ![ReplicatedItemsVMList](.\media\site-recovery-vmware-to-azure-install-mob-svc\update-okpng.png)
5. Spowoduje to uruchomienie zadania usługi mobilności aktualizacji dla każdej z wybranych maszyn wirtualnych.

> [!NOTE]
> [Dowiedz się więcej](site-recovery-vmware-to-azure-manage-configuration-server.md) o sposobie aktualizowania hasła dla konta używanego do zainstalowania usługi mobilności

## <a name="uninstall-mobility-service-on-a-windows-server-computer"></a>Odinstalować usługi mobilności na komputerze z systemem Windows Server
Użyj jednej z następujących metod można odinstalować usługi mobilności na komputerze z systemem Windows Server.

### <a name="uninstall-by-using-the-gui"></a>Odinstalować przy użyciu graficznego interfejsu użytkownika
1. W Panelu sterowania, wybierz **programy**.
2. Wybierz **Microsoft Azure Site odzyskiwania mobilności usługi/główny serwer docelowy**, a następnie wybierz **Odinstaluj**.

### <a name="uninstall-at-a-command-prompt"></a>Odinstaluj w wierszu polecenia
1. Otwórz okno wiersza polecenia z uprawnieniami administratora.
2. Aby odinstalować usługi mobilności, uruchom następujące polecenie:

```
MsiExec.exe /qn /x {275197FC-14FD-4560-A5EB-38217F80CBD1} /L+*V "C:\ProgramData\ASRSetupLogs\UnifiedAgentMSIUninstall.log"
```

## <a name="uninstall-mobility-service-on-a-linux-computer"></a>Odinstalować usługi mobilności na komputerze z systemem Linux
1. Na serwerze Linux, zaloguj się jako **głównego** użytkownika.
2. W terminalu przejdź do /user/local/ASR.
3. Aby odinstalować usługi mobilności, uruchom następujące polecenie:

```
uninstall.sh -Y
```
