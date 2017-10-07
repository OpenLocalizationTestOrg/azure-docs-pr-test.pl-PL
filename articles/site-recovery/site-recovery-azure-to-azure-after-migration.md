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
# <a name="replicate-azure-vms-tooanother-region-after-migration-tooazure-by-using-azure-site-recovery"></a>Replikowanie maszyn wirtualnych platformy Azure region tooanother po tooAzure migracji za pomocą usługi Azure Site Recovery

>[!NOTE]
> Azure Site Recovery replikacji maszyn wirtualnych platformy Azure (VM) jest obecnie w przeglądzie.

## <a name="overview"></a>Omówienie

Ten artykuł pomaga przygotować maszyn wirtualnych platformy Azure dla replikacji między dwóch regionach platformy Azure, po przeprowadzeniu migracji te maszyny z tooAzure środowiska lokalnego przy użyciu usługi Azure Site Recovery.

## <a name="disaster-recovery-and-compliance"></a>Odzyskiwanie po awarii i zgodność
Obecnie coraz więcej przedsiębiorstw przenosisz tooAzure ich obciążeń. Z przedsiębiorstw przenoszenia produkcji krytycznym lokalnymi tooAzure obciążenia, konfigurowanie odzyskiwania po awarii dla tych zadań jest wymagana przez zgodności i toosafeguard przed jakichkolwiek potencjalnych zakłóceń w regionie platformy Azure.

## <a name="steps-for-preparing-migrated-machines-for-replication"></a>Kroki przygotowania zmigrowanych maszyn do replikacji
tooprepare zmigrowane maszyny do konfigurowania replikacji tooanother region platformy Azure:

1. Kończenie migracji.
2. Zainstaluj hello Azure agenta, jeśli to konieczne.
3. Usuń hello usługi mobilności.  
4. Uruchom ponownie hello maszyny Wirtualnej.

Te kroki są opisane bardziej szczegółowo w hello następujące sekcje.

### <a name="step-1-migrate-workloads-running-on-hyper-v-vms-vmware-vms-and-physical-servers-toorun-on-azure-vms"></a>Krok 1: Migracji obciążeń uruchomionych na maszynach wirtualnych funkcji Hyper-V, maszyn wirtualnych VMware i toorun serwerów fizycznych na maszynach wirtualnych Azure

tooset Konfigurowanie replikacji i migrację z lokalnej funkcji Hyper-V, VMware i tooAzure obciążeń fizycznych, wykonaj hello kroki opisane w hello [maszyn wirtualnych IaaS platformy Azure migracji między regiony platformy Azure z usługą Azure Site Recovery](site-recovery-migrate-to-azure.md) artykułu. 

Po migracji nie należy toocommit lub usunąć awarię. Zamiast tego należy wybrać hello **przeprowadzenia migracji** opcji dla każdego komputera ma toomigrate:
1. W **elementy replikowane**, kliknij prawym przyciskiem myszy hello maszyny Wirtualnej i kliknij przycisk **przeprowadzenia migracji**. Kliknij przycisk **OK** toocomplete hello kroku. Możesz śledzić postępy hello właściwości maszyny Wirtualnej, monitorując hello zadanie przeprowadzenia migracji w **zadania usługi Site Recovery**.
2. Witaj **przeprowadzenia migracji** akcji kończy proces migracji hello spowoduje usunięcie replikacji dla maszyny hello i zatrzymuje usługi Site Recovery rozliczeń hello maszyny.

   ![pełna_migracja](./media/site-recovery-hyper-v-site-to-azure/migrate.png)

### <a name="step-2-install-hello-azure-vm-agent-on-hello-virtual-machine"></a>Krok 2: Zainstaluj agenta maszyny Wirtualnej Azure hello na maszynie wirtualnej hello
Hello Azure [agenta maszyny Wirtualnej](../virtual-machines/windows/classic/agents-and-extensions.md#azure-vm-agents-for-windows-and-linux) musi być zainstalowany na maszynie wirtualnej powitania dla toowork rozszerzenia usługi Site Recovery hello i toohelp chronić hello maszyny Wirtualnej.

>[!IMPORTANT]
>Począwszy od wersji 9.7.0.0, maszynach wirtualnych Windows hello mobilności usługi Instalator instaluje również hello najnowszych dostępnych agenta maszyny Wirtualnej Azure. Na migracji maszyny wirtualnej hello spełnia wymagań wstępnych dla przy użyciu dowolnego rozszerzenia maszyny Wirtualnej, tym rozszerzenie usługi Site Recovery hello instalacji agenta. Hello maszyny Wirtualnej Azure agenta potrzeb toobe ręcznie zainstalować tylko wtedy, gdy hello usługi mobilności zainstalowane na powitania zmigrowaną maszynę jest wersja 9.6 lub starszym.

Witaj Poniższa tabela zawiera dodatkowe informacje na temat instalowania agenta maszyny Wirtualnej hello i weryfikacji, że została zainstalowana:

| **Operacja** | **Windows** | **Linux** |
| --- | --- | --- |
| Instalowanie agenta maszyny Wirtualnej hello |Pobierz i zainstaluj hello [pliku MSI agenta](http://go.microsoft.com/fwlink/?LinkID=394789&clcid=0x409). Potrzebujesz instalacji hello toocomplete uprawnienia administratora. |Zainstaluj najnowsze hello [agenta systemu Linux](../virtual-machines/linux/agent-user-guide.md). Potrzebujesz instalacji hello toocomplete uprawnienia administratora. Zaleca się zainstalowanie agenta hello z repozytorium dystrybucji. Firma Microsoft *nie jest zalecane* Instalowanie agenta maszyny Wirtualnej systemu Linux hello bezpośrednio z usługi GitHub.  |
| Sprawdzanie poprawności instalacji agenta hello maszyny Wirtualnej |1. Przeglądaj toohello C:\WindowsAzure\Packages folderu w hello maszyny Wirtualnej platformy Azure. Powinny pojawić się hello WaAppAgent.exe pliku. <br>2. Kliknij prawym przyciskiem myszy plik hello znajduje się zbyt**właściwości**, a następnie wybierz hello **szczegóły** hello kartę **wersji produktu** pole powinno być 2.6.1198.718 lub nowszej. |Nie dotyczy |


### <a name="step-3-remove-hello-mobility-service-from-hello-migrated-virtual-machine"></a>Krok 3: Usuń hello usługi mobilności ze hello zmigrowaną maszynę wirtualną

W przypadku migracji z lokalnych maszyn VMware lub serwerów fizycznych w systemie Windows/Linux, potrzebna usługa Usuń/odinstalowywanie mobilności hello toomanually z hello zmigrowane maszyny wirtualnej.

>[!IMPORTANT]
>Ten krok nie jest wymagane dla tooAzure zmigrowanych maszyn wirtualnych funkcji Hyper-V.

#### <a name="uninstall-hello-mobility-service-on-a-windows-server-vm"></a>Odinstaluj hello usługi mobilności na maszynie Wirtualnej systemu Windows Server
Użyj jednej z hello następujące usługi mobilności hello toouninstall metod na komputerze z systemem Windows Server.

##### <a name="uninstall-by-using-hello-windows-ui"></a>Odinstaluj za pomocą interfejsu użytkownika systemu Windows hello
1. Hello Panelu sterowania, wybierz **programy**.
2. Wybierz **Microsoft Azure Site odzyskiwania mobilności usługi/główny serwer docelowy**, a następnie wybierz **Odinstaluj**.

##### <a name="uninstall-at-a-command-prompt"></a>Odinstaluj w wierszu polecenia
1. Otwórz okno wiersza polecenia z uprawnieniami administratora.
2. toouninstall hello usługi mobilności, uruchom następujące polecenie hello:

   ```
   MsiExec.exe /qn /x {275197FC-14FD-4560-A5EB-38217F80CBD1} /L+*V "C:\ProgramData\ASRSetupLogs\UnifiedAgentMSIUninstall.log"
   ```

#### <a name="uninstall-hello-mobility-service-on-a-linux-computer"></a>Odinstaluj usługę mobilności hello na komputerze z systemem Linux
1. Na serwerze Linux, zaloguj się jako **głównego** użytkownika.
2. W terminalu Przejdź zbyt/użytkownik/lokalnej/funkcja automatycznego odzyskiwania systemu.
3. toouninstall hello usługi mobilności, uruchom następujące polecenie hello:

   ```
   uninstall.sh -Y
   ```

### <a name="step-4-restart-hello-vm"></a>Krok 4: Hello ponownego uruchomienia maszyny Wirtualnej

Po odinstalowaniu usługi mobilności hello hello ponownego uruchomienia maszyny Wirtualnej przed Konfigurowanie replikacji tooanother region platformy Azure.


## <a name="next-steps"></a>Następne kroki
- Włączyć ochronę obciążeń przez [replikowanie maszyn wirtualnych platformy Azure](site-recovery-azure-to-azure.md).
- Dowiedz się więcej o [wskazówki dotyczące replikowanie maszyn wirtualnych platformy Azure networking](site-recovery-azure-to-azure-networking-guidance.md).
