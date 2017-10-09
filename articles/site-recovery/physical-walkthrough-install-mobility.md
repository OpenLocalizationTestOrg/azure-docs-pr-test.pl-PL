---
title: "Witaj aaaInstall usługę mobilności dla serwera fizycznego tooAzure replikacji | Dokumentacja firmy Microsoft"
description: "W tym artykule opisano, jak tooinstall hello agent usługi mobilności na serwerach fizycznych replikowanie tooAzure z usługą Azure Site Recovery hello."
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: 3189fbcd-6b5b-4ffb-b5a9-e2080c37f9d9
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 06/27/2017
ms.author: raynew
ms.openlocfilehash: 48fd2c0ffe67875ed446c8167c2ae7f90d3f537c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="step-9-install-hello-mobility-service"></a>Krok 9: Instalowanie usługi mobilności hello


W tym artykule opisano sposób tooinstall hello składnika usługi Mobility podczas replikowania lokalnych tooAzure serwerach fizycznych systemu Windows i Linux, przy użyciu hello [usługi Azure Site Recovery](site-recovery-overview.md) w hello portalu Azure.

Hello usługi mobilności przechwytywania zapisów danych na maszynie i przekazuje je toohello serwera przetwarzania. Na każdym serwerze, można zainstalować, które mają tooreplicate tooAzure.

Można ręcznie zainstalować usługi mobilności hello, lub za pomocą instalacji wypychanej hello Site Recovery przetworzyć serwera po włączeniu replikacji lub za pomocą narzędzi takich jak System Center Configuration Manager. Jeśli używasz instalacji wypychanej usługa hello jest zainstalowana na serwerze powitania po włączeniu replikacji.

Opublikuj komentarze i pytania u dołu hello w tym artykule, albo na powitania [Forum usług odzyskiwania Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).

## <a name="install-manually"></a>Instalowanie ręczne

1. Sprawdź hello [wymagania wstępne](site-recovery-vmware-to-azure-install-mob-svc.md#prerequisites) dla instalacji ręcznej.
2. Postępuj zgodnie z [tych instrukcji](site-recovery-vmware-to-azure-install-mob-svc.md#install-mobility-service-manually-by-using-the-gui) dotyczące ręcznej instalacji przy użyciu portalu hello.
3. Jeśli wolisz tooinstall z wiersza polecenia hello wykonaj [tych instrukcji](site-recovery-vmware-to-azure-install-mob-svc.md#install-mobility-service-manually-at-a-command-prompt).

## <a name="install-from-hello-process-server"></a>Zainstaluj z serwera przetwarzania hello

Jeśli chcesz hello toopush instalacji usługi mobilności z serwera przetwarzania powitania po włączeniu replikacji dla maszyny, należy konta, które mogą być używane przez hello procesu serwera tooaccess hello maszyny. Konto Hello jest używana tylko dla instalacji wypychanej hello.

1. Jeśli nie utworzono konta, to zrobić przy użyciu poniższych wskazówek:

    - Korzystając z domeny lub lokalnego konta
    - W systemie Windows Jeśli nie używasz konta domeny, należy toodisable kontroli dostępu użytkownika zdalnego na komputerze lokalnym hello. toodo, hello rejestrowania w obszarze **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\System**, Dodaj wpis DWORD hello **LocalAccountTokenFilterPolicy**, o wartości 1.
    - Wpis rejestru hello tooadd dla systemu Windows z interfejsu wiersza polecenia, wpisz:

        ```
        REG ADD HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\System /v LocalAccountTokenFilterPolicy /t REG_DWORD /d 1.
        ```

    - Dla systemu Linux hello konto powinno być głównym urzędem certyfikacji na serwerze Linux źródłowym hello.

2. Następnie postępuj zgodnie z [tych instrukcji](site-recovery-vmware-to-azure-install-mob-svc.md#install-mobility-service-by-push-installation-from-azure-site-recovery) Jeśli chcesz, aby usługa mobilności hello toopush na maszynach wirtualnych z systemem Windows lub Linux.

## <a name="other-installation-methods"></a>Inne metody instalacji

- [Dowiedz się więcej o](site-recovery-install-mobility-service-using-sccm.md) Instalowanie usługi mobilności hello przy użyciu programu Configuration Manager
- [Dowiedz się więcej o](site-recovery-automate-mobility-service-install.md) instalacji z usługi Konfiguracja DSC automatyzacji Azure.


## <a name="next-steps"></a>Następne kroki

Przejdź do zbyt[kroku 10: Włączanie replikacji](physical-walkthrough-enable-replication.md)
