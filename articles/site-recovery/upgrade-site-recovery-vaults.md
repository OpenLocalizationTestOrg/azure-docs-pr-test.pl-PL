---
title: "Magazyn usług odzyskiwania Azure tooan aaaUpgrade magazynu usługi Site Recovery"
description: "Dowiedz się, jak tooupgrade magazynie usługi Azure Site Recovery tooa magazyn usług odzyskiwania"
documentationcenter: 
author: rajani-janaki-ram
manager: rochakm
editor: 
ms.assetid: 
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 07/31/2017
ms.author: rajani-janaki-ram
ms.openlocfilehash: a18a923ee3bad91873e654c9b9b5bf8b83acc123
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="upgrade-a-site-recovery-vault-tooan-azure-resource-manager-based-recovery-services-vault"></a>Uaktualnij magazynu usług odzyskiwania Azure Resource Manager tooan magazynu usługi Site Recovery

W tym artykule opisano, jak tooupgrade usługi Azure Site Recovery magazyny Magazyny usług odzyskiwania Resource Manager tooAzure bez wpływu na trwającej replikacji. Aby uzyskać więcej informacji na temat usługi Azure Resource Manager funkcje i korzyści, zobacz [Omówienie usługi Azure Resource Manager](../azure-resource-manager/resource-group-overview.md).

## <a name="introduction"></a>Wprowadzenie
Magazyn usług odzyskiwania jest zasobem usługi Azure Resource Manager do zarządzania kopii zapasowej i odzyskiwanie po awarii w chmurze hello. Jest ujednoliconego magazyn, którego można użyć w hello nowego portalu Azure, i zastępuje hello zapasową magazynów usługi Site Recovery.

Magazyny usług odzyskiwania oferują tablicę funkcje, takie jak:

* Pomoc techniczna platformy Azure Resource Manager: można chronić i pracy awaryjnej z maszyn wirtualnych i maszyn fizycznych do stosu usługi Azure Resource Manager.

* Wykluczanie dysku: Jeśli masz pliki tymczasowe lub wiele zmian danych, że nie chcesz toouse Twojego przepustowości dla woluminów można wykluczyć z replikacji. Ta funkcja została włączona w obecnie *VMware tooAzure* i *tooAzure funkcji Hyper-V* i rozszerzeniu również tooother scenariuszy.

* Obsługa premium i Magazyn lokalnie nadmiarowy: mogą teraz chronić serwery w magazynie premium konta, które umożliwiają klientom wyższy tooprotect aplikacji za pomocą operacji wejścia/wyjścia na sekundę (IOPS). Ta funkcja jest obecnie włączona w *VMware tooAzure*.

* Uproszczone środowisko — wprowadzenie: hello rozszerzone — wprowadzenie środowisko zostało zaprojektowane Instalator odzyskiwania po awarii toomake łatwe.

* Kopii zapasowych i odzyskiwania lokacji zarządzania z tym samym magazynie hello: można teraz chronić serwerów na potrzeby odzyskiwania po awarii lub wykonaj kopię zapasową z hello tego samego magazynu, co może zmniejszyć nakłady znacznie z zarządzania.

Aby uzyskać więcej informacji na temat funkcji i doświadczeń uaktualniony hello Zobacz hello [blogu magazynu kopii zapasowej i odzyskiwania](https://azure.microsoft.com/blog/azure-site-recovery-now-available-in-a-new-experience-with-support-for-arm-and-csp/).

## <a name="salient-features"></a>Najważniejsze funkcje

* Bez wpływu na trwająca replikacja: trwającej replikacji kontynuować bez przerwy podczas i po uaktualnieniu.

* Bez dodatkowych kosztów: Pobierz całego zestawu funkcji zaktualizowane bez ponoszenia dodatkowych kosztów.

* Brak utraty danych: ponieważ ten proces jest uaktualnienie i nie migracji, istniejących punktów odzyskiwania replikacji i ustawienia pozostaną nienaruszone podczas i po uaktualnieniu hello.


## <a name="what-happens-during-hello-vault-upgrade"></a>Co się dzieje podczas uaktualniania magazynu hello?

Podczas uaktualniania hello nie można wykonać operacji, takich jak rejestrowanie nowego serwera oraz włączania replikacji dla maszyny wirtualnej (VM). Operacje, które wymagają Odczyt danych z lub zapisywania w magazynie toohello danych, takich jak trwającej replikacji magazynu toohello chronione elementy, nadal przerwana.

### <a name="changes-tooautomation-and-tooling-after-hello-upgrade"></a>Zmienia tooautomation i narzędzi po uaktualnieniu hello
Po uaktualnieniu hello magazynu typ z modelu wdrażania usługi Resource Manager toohello hello wdrażania klasycznego modelu aktualizacji istniejącej automatyzacji hello lub nadal toowork, po uaktualnieniu hello tooensure narzędzi.

### <a name="prepare-your-environment-for-hello-upgrade"></a>Przygotowywanie środowiska dla uaktualnienia hello

* [Instalowanie programu PowerShell lub ją uaktualnić tooversion 5 lub nowszy](https://www.microsoft.com/download/details.aspx?id=50395)
* [Zainstaluj najnowszą wersję hello Azure PowerShell msi](https://github.com/Azure/azure-powershell/releases)
* [Pobierz hello skryptów uaktualniania magazynu usług odzyskiwania](https://aka.ms/vaultupgradescript)

### <a name="prerequisites"></a>Wymagania wstępne
Magazyny usług odzyskiwania Resource Manager tooAzure magazyny tooupgrade z usługi Site Recovery, musi spełniać następujące wymagania hello:

* Wersja minimalna agenta: hello Azure dostawcy usługi Site Recovery na serwerze musi być 5.1.1700.0 lub nowszym.

* Obsługiwana konfiguracja: nie można skonfigurować Magazyn sieci magazynowania (SAN) lub grup dostępności AlwaysOn programu SQL Server. Inne konfiguracje są obsługiwane.

    >[!NOTE]
    >Po uaktualnieniu hello można zarządzać mapowania przechowywania tylko przy użyciu programu PowerShell.

* Scenariusz wdrażania obsługiwanych: Magazyn nie powinien być hello *VMware tooAzure* modelu wdrażania starszej wersji. Aby kontynuować, należy najpierw przenieść toohello wdrożenia rozszerzonego modelu.

* Operacje płaszczyzny żadnych aktywnych działań zainicjowane przez użytkownika, które obejmują zarządzanie: ponieważ płaszczyzny zarządzania toohello dostęp jest ograniczony podczas uaktualniania, wykonanie wszystkich akcji płaszczyzny zarządzania przed wyzwoleniem hello uaktualnienia. Ten proces nie zawiera trwającej replikacji.

## <a name="frequently-asked-questions"></a>Często zadawane pytania

**To uaktualnienie wpływa na mój trwającej replikacji?**

Nie. Twoje bieżące replikacja jest kontynuowana przerwana podczas i po uaktualnieniu hello.

**Co się stanie toonetwork ustawienia, takie jak ustawienia IP i sieci VPN typu lokacja lokacja?**

uaktualnienie Hello nie wpływa na powitania ustawienia sieciowe. Wszystkie połączenia Azure do lokalne pozostaną nienaruszone.

**Co w przypadku magazynów toomy nie należy zaplanować tooupgrade w hello niemal przyszłości?**

Obsługa magazynu usługi Site Recovery w portalu Azure starego hello zostaną wycofane uruchamianie września 2017 r. Zdecydowanie zaleca się użycie hello funkcja uaktualnienia toomove toohello nowego portalu.

**Co oznacza ten plan migracji dla moich istniejących narzędzi?**  

Aktualizowanie modelu wdrażania usługi Resource Manager toohello narzędzi jest jednym z hello najważniejszych zmian, które należy uwzględnić w planów uaktualnienia. Magazyny usług odzyskiwania Hello są oparte na modelu wdrażania usługi Resource Manager hello. 

**Jak długo hello przestoju płaszczyzny zarządzania ostatnio?**

uaktualnienie Hello zwykle trwa około 15 minut too30 i może potrwać tooa maksymalnie jedną godzinę.

**I przywrócić po uaktualnieniu?**

Nie. Wycofanie nie jest obsługiwana po hello zasoby zostały pomyślnie uaktualnione.

**Można sprawdzania poprawności mojej subskrypcji lub toosee zasobów czy można uaktualnić?**

Tak. W hello obsługiwane platformy opcję uaktualniania hello pierwszym krokiem podczas uaktualnienia hello jest toovalidate czy hello zasoby są w stanie uaktualnienia. W przypadku niepowodzenia weryfikacji hello otrzymasz odpowiednie komunikaty o błędach i ostrzeżenia.

**Jak zgłosić problem związany z uaktualnieniem hello?**

Jeśli wystąpią zakończą się niepowodzeniem podczas uaktualniania hello, należy pamiętać, identyfikator operacji hello wyświetlanej na liście błędów hello. Microsoft Support aktywnego będą działać na rozwiązanie problemu hello. Może także kontaktować z zespołem pomocy technicznej hello z Identyfikatorem subskrypcji, nazwę magazynu, a identyfikator operacji. Obsługa będzie działać możliwie jak najszybciej tooresolve hello problem. Nie próbuj ponownie operację hello o ile nie zostaną jawnie instrukcją toodo tak przez firmę Microsoft.

## <a name="run-hello-script"></a>Uruchom skrypt hello

W programie PowerShell uruchom następujące polecenie hello:

    PS > .\RecoveryServicesVaultUpgrade-1.0.0.ps1 -SubscriptionID <subscriptionID>  -VaultName <vaultname> -Location <location> -ResourceType HyperVRecoveryManagerVault -TargetResourceGroupName <rgname>

* Identyfikator subskrypcji: hello identyfikator subskrypcji, który został skojarzony z magazynem hello, że w przypadku uaktualniania.

* VaultName: Nazwa hello hello magazynu, który w przypadku uaktualniania.

* Lokalizacja: hello lokalizacja magazynu hello, że w przypadku uaktualniania.

* Typ zasobu: Magazyny HyperVRecoveryManagerVault Site Recovery.

* TargetResourceGroupName: hello grupy zasobów, do której ma zostać hello uaktualnione umieszczone toobe magazynu. TargetResourceGroupName może być istniejącej grupy zasobów w usłudze Azure Resource Manager lub nowy. Jeśli hello TargetResourceGroupName, która jest dostarczana nie istnieje, go jest tworzony w ramach uaktualnienia hello w hello sam lokalizacji co magazyn hello. Aby uzyskać więcej informacji, zobacz sekcję "Grupy zasobów" hello [Omówienie usługi Azure Resource Manager](../azure-resource-manager/resource-group-overview.md#resource-groups).

    >[!NOTE]
    >Nazwy grupy zasobów jest ograniczenia toocertain podmiotu. Magazyn tooprevent uaktualnić awarii, należy starannie czy hello tooobserve konwencji nazewnictwa.
    >
    >Na przykład:
    >
    >.\RecoveryServicesVaultUpgrade-1.0.0.ps1 SubscriptionId - 1234-54123-354354-56416-8645 - VaultName gen2dr — lokalizacja "Europa Północna" hypervrecoverymanagervault - ResourceType - TargetResourceGroupName abc

Alternatywnie możesz uruchomić hello następującego skryptu. Wprowadź wartości hello hello wymaganych parametrów.

    PS > .\RecoveryServicesVaultUpgrade-1.0.0.ps1
    cmdlet RecoveryServicesVaultUpgrade-1.0.0.ps1 at command pipeline position 1

    Supply values for hello following parameters:
    SubscriptionId:
    VaultName:
    Location:
    ResourceType:
    TargetResourceGroupName:

1. Hello skrypt programu PowerShell wyświetli monit możesz tooenter swoje poświadczenia. Wprowadź je dwukrotnie raz hello wdrażania klasycznego modelu oraz raz hello konta usługi Azure Resource Manager.

2. Po wprowadzeniu poświadczeń hello skrypt jest uruchamiany toodetermine Sprawdź, czy Twoje hello spełnia instalacji infrastruktury powyżej wymagań.

3. Po hello wymagania wstępne zostały sprawdzone i potwierdzone, jest monitem tooproceed hello uaktualniania magazynu. rozpocznie się proces uaktualniania Hello uaktualniania magazynu. Hello całego uaktualnienia może zająć 15 toocomplete minut too30.

4. Po uaktualnieniu hello pomyślnie, można uzyskać dostępu do hello uaktualnionego magazynu w hello nowego portalu Azure.

## <a name="post-upgrade-vault-management"></a>Zarządzanie magazynem po uaktualnieniu

### <a name="replicate-by-using-azure-site-recovery-in-hello-recovery-services-vault"></a>Replikacja za pomocą usługi Azure Site Recovery w hello magazyn usług odzyskiwania

* Maszyny wirtualne Azure mogą teraz chronić z jednego regionu tooanother. Aby uzyskać więcej informacji, zobacz [replikowanie maszyn wirtualnych platformy Azure między regionami z usługą Azure Site Recovery](site-recovery-azure-to-azure.md).

* Aby uzyskać więcej informacji na temat replikowania maszyn wirtualnych VMware tooAzure, zobacz [tooAzure replikowanie maszyn wirtualnych VMware z usługą Site Recovery](vmware-walkthrough-overview.md).

* Aby uzyskać więcej informacji na temat replikowania maszyn wirtualnych funkcji Hyper-V (bez VMM) tooAzure, zobacz [tooAzure maszyn wirtualnych (bez VMM) replikacji funkcji Hyper-V](hyper-v-site-walkthrough-overview.md).

* Aby uzyskać więcej informacji o replikacji tooAzure maszyn wirtualnych funkcji Hyper-V (w programie VMM), zobacz [maszyn wirtualnych funkcji Hyper-V replikacji w tooAzure chmur programu VMM przy użyciu usługi Site Recovery w hello portalu Azure](vmm-to-azure-walkthrough-overview.md).

* Aby uzyskać więcej informacji o replikacji lokacji dodatkowej tooa funkcji Hyper-VMs (w programie VMM), zobacz [replikacji funkcji Hyper-V maszyn wirtualnych VMM chmur tooa dodatkowej VMM lokacji przy użyciu hello portalu Azure](site-recovery-vmm-to-vmm.md).

* Aby uzyskać więcej informacji o replikacji lokacji dodatkowej tooa maszyn wirtualnych VMware, zobacz [Replikowanie lokalnych maszyn wirtualnych VMware lub serwerów fizycznych tooa lokacji dodatkowej w klasycznym portalu Azure hello](site-recovery-vmware-to-vmware.md).

### <a name="view-your-replicated-items"></a>Wyświetl elementy replikowane

Witaj poniższy obraz przedstawia hello usług odzyskiwania magazynu pulpitu nawigacyjnego strona, wyświetlająca kluczy jednostek hello magazynu. Wybierz tooview listę chronionych jednostki w magazynie hello **usługi Site Recovery** > **elementy replikowane**.


![Zreplikowanych elementów](./media/upgrade-site-recovery-vaults/replicateditems.png)

Witaj Poniższa ilustracja przedstawia przykładowy przepływ pracy hello wyświetlanie Twoich zreplikowanych elementów i hello **pracy awaryjnej** polecenia inicjowania pracy awaryjnej.

![Zreplikowanych elementów](./media/upgrade-site-recovery-vaults/failover.png)

### <a name="view-your-replication-settings"></a>Wyświetl ustawienia replikacji

W magazynie usługi Site Recovery hello każdej grupy ochrony jest konfigurowana częstotliwość kopiowania, przechowywania punktu odzyskiwania, częstotliwość migawek spójności aplikacji i innych ustawień replikacji. W magazynie usług odzyskiwania hello te ustawienia są skonfigurowane jako zasady replikacji. Nazwa Hello zasad hello jest hello hello grupy ochrony lub hello *primarycloud_Policy*.

Aby uzyskać więcej informacji na temat zasad replikacji, zobacz [zarządzać zasadami replikacji VMware tooAzure](site-recovery-setup-replication-settings-vmware.md).
