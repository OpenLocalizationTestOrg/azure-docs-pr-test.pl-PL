---
title: "aaaBackup i odzyskiwanie po awarii dla dysków IaaS platformy Azure | Dokumentacja firmy Microsoft"
description: "W tym artykule Wyjaśnijmy, jak tooplan kopii zapasowych i odzyskiwania awaryjnego (DR) maszyn wirtualnych IaaS (VM) i dyski na platformie Azure. W tym dokumencie opisano zarówno zarządzane i niezarządzane dysków"
services: storage
cloud: Azure
documentationcenter: na
author: luywang
manager: kavithag
ms.assetid: 
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: luywang
ms.openlocfilehash: 17c697bc411fb47c4b7483b59829af1c40732ac1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="backup-and-disaster-recovery-for-azure-iaas-disks"></a>Kopia zapasowa i odzyskiwanie po awarii dla dysków IaaS platformy Azure

W tym artykule Wyjaśnijmy, jak tooplan kopii zapasowych i odzyskiwania awaryjnego (DR) maszyn wirtualnych IaaS (VM) i dyski na platformie Azure. W tym dokumencie opisano zarówno zarządzane i niezarządzane dysków.

Zostanie najpierw omawianiu hello wbudowanych usterek tolerancji możliwości w hello platformy Azure umożliwiające ochronę przed awariami lokalnego. Następnie omówiono powitania po awarii scenariusze nie są w pełni objęte hello wbudowanych możliwości, czyli hello tematem głównym opisany w tym dokumencie. Poniżej opisano również kilka przykładowe scenariusze obciążenie, gdzie może stosować inną uwagi dotyczące tworzenia kopii zapasowych i odzyskiwania po awarii. Firma Microsoft może przejrzeć możliwych rozwiązań dla odzyskiwania po awarii dysków IaaS. 

## <a name="introduction"></a>Wprowadzenie

Hello platformy Azure używa różne metody dla nadmiarowość i odporność na uszkodzenia toohelp ochrony klientów przed awariami sprzętu zlokalizowanego, które mogą wystąpić. Błędy lokalne mogą obejmować problemy z maszyną serwera usługi Azure storage przechowujący część danych hello dysku wirtualnego lub w przypadku awarii dysków SSD i HDD na tym serwerze. Takie błędy składnika izolowanego sprzętu może się zdarzyć, podczas wykonywania normalnych operacji i platforma hello jest zaprojektowana toobe odporność toothese błędów. Główne awarii może spowodować błędy lub inaccessibility dużej liczby serwerów magazynu lub całe centrum danych. Maszyn wirtualnych i dyski są zwykle chronione zlokalizowanych awarii, dodatkowe kroki są niezbędne tooprotect obciążenie region na poziomie awarii krytycznego (na przykład poważnej awarii), które mogą wpłynąć na Twojej maszyny Wirtualnej i dysków.

Ponadto możliwość toohello błędów platformy, za pomocą powitania klienta aplikacji lub danych mogą wystąpić problemy. Na przykład nowa wersja aplikacji mogą przypadkowo należy podziału, Zmień dane toohello. W takim przypadku można aplikacji hello toorevert i hello danych tooa wcześniejsze niż wersja zawierającego hello ostatniego znanego dobrego stanu. Wymagane jest utrzymanie regularnych kopii zapasowych.

Regionalnej awarii należy wykonać kopię zapasową maszyn wirtualnych IaaS dysków tooa innego regionu. 

Zanim przyjrzymy opcje tworzenia kopii zapasowych i odzyskiwania po awarii umożliwia recap kilku dostępnych metod obsługi zlokalizowanych awarii.

### <a name="azure-iaas-resiliency"></a>Odporność IaaS platformy Azure

*Odporność* odwołuje się tolerancji toohello normalne błędów występujących w składników sprzętowych. Odporność jest hello toorecover możliwości od awarii i kontynuować toofunction. Nie jest o unikanie błędów, ale odpowiadać toofailures w taki sposób, który pozwala uniknąć przestoju lub utraty danych. Celem Hello odporności jest tooreturn hello tooa pełni funkcjonalnej stan aplikacji w przypadku awarii. Azure maszyn wirtualnych i dyski są błędów sprzętu odporność toocommon toobe zaprojektowane. Daj nam przyjrzeć się, jak hello Azure IaaS platformy zapewnia to elastyczność.

Maszyna wirtualna składa się głównie z dwóch części: (1) A obliczeniowe serwera i dyski stałe hello (2). Wpływ zarówno na hello odporność na uszkodzenia maszyny wirtualnej.

Jeśli powitania serwera hosta obliczeń platformy Azure, która przechowuje maszyny Wirtualnej błędów sprzętu (która jest rzadko), Azure jest zaprojektowana tooautomatically hello przywracania maszyny Wirtualnej na innym serwerze. W takim przypadku wystąpią ponowne uruchomienie komputera, a hello maszyny Wirtualnej musi być Utwórz kopię zapasową po pewnym czasie. Azure automatycznie wykrywa takie awarie sprzętu i wykonuje odzyskiwanie toohelp upewnij się, klient hello maszyny Wirtualnej będzie dostępna tak szybko, jak to możliwe.

Dotyczących dysków IaaS trwałości danych ma kluczowe znaczenie dla platformy magazynu trwałego hello. Azure klienci mają ważnymi aplikacji uruchomionych na IaaS i są one zależne od trwałości hello hello danych. Projekty platformy Azure ochrony tych dysków IaaS przy użyciu trzech nadmiarowe kopie dane przechowywane lokalnie, zapewniając wysoką trwałością przed awariami lokalnego. W przypadku niepowodzenia co hello składniki sprzętowe, które przechowuje dysku maszyny Wirtualnej nie ma wpływu na ponieważ istnieją dwie kopie dodatkowe toosupport dysku żądania. Działa on prawidłowo nawet wtedy, gdy dwa składniki sprzętowe obsługujące dysku się nie powieść w hello takie same (co jest bardzo rzadko). toohelp upewnij się, firma Microsoft zachowuje zawsze trzy repliki, hello usługi Magazyn Azure automatycznie spowoduje utworzenie nowej kopii danych w tle hello Jeśli jeden z trzech kopii hello jest niedostępny. W związku z tym nie ma potrzeby toouse RAID z dyskami Azure odporności na uszkodzenia. Proste RAID 0 konfiguracji powinny być wystarczające stosowanie hello dysków, jeśli niezbędne toocreate większych woluminów.

Z powodu tej architektury **Azure spójnie wydał korporacyjnej trwałości dla IaaS z branży dysków ZERO % [firmie częstość niepowodzeń](https://en.wikipedia.org/wiki/Annualized_failure_rate).**

Błędy sprzętu zlokalizowanych na powitania obliczeniowe hosta lub w magazynie hello platformy może czasem spowodować tymczasowej niedostępności hello maszyny Wirtualnej, która jest objęta hello [umowy SLA platformy Azure](https://azure.microsoft.com/support/legal/sla/virtual-machines/) dostępności maszyny Wirtualnej. Platforma Azure udostępnia również branży umowa SLA dla pojedynczego wystąpień maszyn wirtualnych, które używają dysków magazyn w warstwie Premium.

toosafeguard obciążeń aplikacji z przestoju powodu tymczasowej niedostępności toohello dysku lub maszyny Wirtualnej, klienci mogą korzystać z [zestawów dostępności](../virtual-machines/windows/manage-availability.md). Co najmniej dwie maszyny wirtualne w zestawie dostępności zapewnia nadmiarowość dla aplikacji hello. Azure utworzy tych maszyn wirtualnych i dyski w domenach awarii oddzielne z różnych składników zasilania, sieci i serwera. W związku z tym awarie sprzętowe zlokalizowanego zwykle nie mają wpływu na wiele maszyn wirtualnych w hello na powitania tym samym czasie, zapewniając wysoką dostępność aplikacji. Uznaje się, że ustawia dostępności toouse dobrym rozwiązaniem, gdy wymagana jest wysoka dostępność. Aby uzyskać więcej informacji zobacz aspekty odzyskiwania po awarii hello opisanymi poniżej.

### <a name="backup-and-disaster-recovery"></a>Kopii zapasowych i odzyskiwania po awarii

Odzyskiwania awaryjnego (DR) jest toorecover możliwości powitania od zdarzenia, ale rzadko głównych: błędy z systemem innym niż przejściowy, całej skali, takie jak zakłócenia, która wpływa na całą regionu. Odzyskiwanie po awarii obejmuje kopii zapasowej danych i archiwizowania i może zawierać ręcznej interwencji, takich jak przywracanie z kopii zapasowej bazy danych.

Witaj platformy Azure wbudowaną ochronę przed awariami zlokalizowanych mogą nie pełni chronić hello maszyny wirtualne/dysków, w przypadku hello głównych awarii, co może powodować awarie na dużą skalę. W tym krytycznego zdarzenia, takie jak trafienia huragan, trzęsienia ziemi, fire lub awarie jednostki sprzętowe dużą skalę centrum danych. Ponadto mogą wystąpić błędy ze względu na problemy z tooapplication lub danych.

toohelp chronić obciążeń IaaS z awarii, należy zaplanować odzyskiwania tooenable nadmiarowości i kopii zapasowych. Podczas odzyskiwania po awarii należy zaplanować nadmiarowości i tworzenie kopii zapasowych w innej lokalizacji geograficznej hello głównej witryny. Pomaga to zapewnić kopii zapasowej nie ma wpływu na powitania tego samego zdarzenia, który pierwotnie wpływ na powitania maszyny Wirtualnej lub dysków. Aby uzyskać więcej informacji, zobacz [odzyskiwania po awarii dla aplikacji w oparciu Azure](https://docs.microsoft.com/azure/architecture/resiliency/disaster-recovery-azure-applications).

Uwagi dotyczące programu DR mogą obejmować hello następujące aspekty:

1. Wysokiej dostępności (HA) jest zdolność hello hello toocontinue aplikacji uruchomionych w dobrej kondycji, bez przestojów znaczące. Przez "dobrej kondycji," oznacza możemy aplikacja hello jest elastyczny, a użytkownicy mogą połączyć toohello aplikacji i korzystać z niego. Niektórych kluczowych aplikacji i baz danych może być wymagane toobe dostępny zawsze, nawet wtedy, gdy występują błędy hello platformy. Dla tych zadań może być konieczne tooplan nadmiarowości na potrzeby aplikacji hello, a także hello danych.

2. Trwałość danych: W niektórych przypadkach uwagę głównego hello jest zapewnienie, że dane hello są zachowywane w przypadku awarii hello. Dlatego może być konieczne kopii zapasowej danych w innej lokacji. W przypadku takich obciążeń mogą nie być potrzebne pełne nadmiarowości na potrzeby aplikacji hello, ale także regularne tworzenie kopii zapasowych dysków hello.

## <a name="backup-and-dr-scenarios"></a>Kopia zapasowa i scenariuszy odzyskiwania po awarii

Oto kilka przykładów typowych scenariuszy obciążenia aplikacji i hello zagadnienia dotyczące planowania odzyskiwania po awarii.

### <a name="scenario-1-major-database-solutions"></a>Scenariusz 1: Głównej bazy danych rozwiązania

Rozważ serwer produkcyjny bazy danych, takich jak SQL Server lub Oracle, który może obsługiwać wysokiej dostępności. Krytyczne produkcji aplikacji i użytkowników są zależne od tej bazy danych. Witaj planu odzyskiwania po awarii dla tego systemu może być konieczne hello toosupport następujące wymagania:

1. Dane muszą być chronione i możliwe do odzyskania.
2.  Serwer musi być dostępny do użycia.

Może to wymagać utrzymania repliki bazy danych hello w innym regionie jako kopii zapasowej. W zależności od wymagań hello dostępność serwera i odzyskiwanie danych hello rozwiązania może należeć do zakresu od aktywny-aktywny lub aktywny / pasywny repliki lokacji tooperiodic tworzenie kopii zapasowych danych hello. Relacyjnych baz danych, takich jak SQL Server i Oracle zapewniają różne opcje replikacji. Dla programu SQL Server [programu SQL Server zawsze włączonych grup dostępności](https://msdn.microsoft.com/library/hh510230.aspx) można użyć w celu zapewnienia wysokiej dostępności.

Bazy danych NoSQL, takie jak bazy danych MongoDB obsługują również [replik](https://docs.mongodb.com/manual/replication/) nadmiarowości. można replik Hello wysokiej dostępności.

### <a name="scenario-2-a-cluster-of-redundant-vms"></a>Scenariusz 2: Klastra nadmiarowe maszyny wirtualne

Należy wziąć pod uwagę obciążenia obsługiwane przez klaster maszyn wirtualnych, które zapewniają nadmiarowość i równoważenie obciążenia. Przykładem jest klastra Cassandra wdrożone w regionie. Ten typ architektury już zapewnia wysoki poziom nadmiarowości w tym regionie. Jednak obciążenia hello tooprotect regionalnej awarii poziomu, należy rozważyć rozpraszania klastra hello dwóch regionach lub wprowadzeniem region tooanother okresowe kopie zapasowe.

### <a name="scenario-3-iaas-application-workload"></a>Scenariusz 3: IaaS aplikacji obciążenia

Może to być typowe produkcji pracą maszyny Wirtualnej platformy Azure. Na przykład może być serwerem sieci web lub serwera plików zawartości hello i innych zasobów w lokacji. Może to być również aplikacji biznesowej niestandardowej uruchomione na maszynie Wirtualnej, które przechowywane jego dane, zasobów i stan aplikacji hello dysków maszyny Wirtualnej. W takim przypadku jest ważne toomake się, że możesz korzystać z kopii zapasowych na bieżąco. Częstotliwość wykonywania kopii zapasowych powinny być oparte na powitania rodzaj hello obciążenie maszyny Wirtualnej. Na przykład jeśli aplikacja hello jest uruchamiana codziennie i modyfikuje danych, następnie hello kopii zapasowej należy podjąć co godzinę.

Innym przykładem jest serwer raportowania ściągania danych z innych źródeł i generuje raporty zagregowanych. Utraty tej maszyny Wirtualnej lub dysków spowoduje utratę toohello hello raportów. Jednak może być możliwe toorerun hello raportowania procesu i dane wyjściowe regenerate hello. W takim przypadku naprawdę masz utraty danych, nawet jeśli serwer raportowania hello o awarii, dlatego może mieć wyższy poziom tolerancji utraty części danych hello na powitania serwera raportowania. W takim przypadku mniej częste wykonywanie kopii zapasowych jest opcja tooreduce hello kosztów.

### <a name="scenario-4-iaas-application-data-issues"></a>Scenariusz 4: Problemy z danych aplikacji IaaS

Masz aplikację, która oblicza, przechowuje i służy krytyczne komercyjnych danych, takie jak informacje o cenach. Nowa wersja aplikacji ma niepoprawnie obliczana hello ceny i uszkodzony hello istniejących danych commerce obsługiwane przez platformę hello usterki oprogramowania. W tym miejscu hello najlepsze rozwiązanie byłoby toorevert toohello starszej wersji aplikacji hello i danych hello pierwszy. tooenable, podejmij okresowe kopie zapasowe systemu.

## <a name="disaster-recovery-solution-azure-backup-service"></a>Rozwiązanie odzyskiwania po awarii: Usługa Kopia zapasowa Azure

[Usługa Kopia zapasowa Azure](https://azure.microsoft.com/services/backup/) może służyć do tworzenia kopii zapasowych i odzyskiwania po awarii, a w przypadku [dysków zarządzanych](storage-managed-disks-overview.md) oraz [niezarządzane dysków](storage-about-disks-and-vhds-windows.md#unmanaged-disks). Zadanie tworzenia kopii zapasowej można utworzyć na podstawie czasu tworzenia kopii zapasowych, łatwe przywrócenie maszyny Wirtualnej i zasady przechowywania kopii zapasowych. 

Jeśli używasz [dysków Premium Storage](storage-premium-storage.md), [dysków zarządzanych](storage-managed-disks-overview.md), lub innych typów dysku z hello [magazyn lokalnie nadmiarowy (LRS)](storage-redundancy.md#locally-redundant-storage) opcji jest szczególnie ważne tooleverage okresowe DR kopie zapasowe. Kopia zapasowa Azure przechowuje dane hello w magazynie usług odzyskiwania do przechowywania długoterminowego. Wybierz hello [magazyn geograficznie nadmiarowy (GRS)](storage-redundancy.md#geo-redundant-storage) opcji dla magazyn usług odzyskiwania hello kopii zapasowej. Który będzie upewnij się, że kopie zapasowe są replikowane tooa innym regionie Azure zabezpieczenia z regionalnej awarii.

Dla [niezarządzane dysków](storage-about-disks-and-vhds-windows.md#unmanaged-disks), można użyć typu magazynu LRS hello dysków IaaS, ale upewnij się, że kopia zapasowa Azure jest włączone w hello GRS opcję hello magazynu usług odzyskiwania.

**Jeśli używasz hello [GRS](storage-redundancy.md#geo-redundant-storage)/[RA-GRS](storage-redundancy.md#read-access-geo-redundant-storage) opcji dla niezarządzanego dysków, można nadal konieczne migawek spójnych kopii zapasowych i odzyskiwania po awarii.** Należy użyć jednego [usługi Kopia zapasowa Azure](https://azure.microsoft.com/services/backup/) lub [migawki spójne z](#alternative-solution-consistent-snapshots).

Witaj poniżej znajduje się podsumowanie rozwiązania dla odzyskiwania po awarii.

| Scenariusz | Automatyczne replikacji | Rozwiązanie odzyskiwania po awarii |
| --- | --- | --- |
| *Dyski magazynu w warstwie Premium* | Lokalne ([LRS](storage-redundancy.md#locally-redundant-storage)) | [Azure Backup](https://azure.microsoft.com/services/backup/) |
| *Managed Disks* | Lokalne ([LRS](storage-redundancy.md#locally-redundant-storage)) | [Azure Backup](https://azure.microsoft.com/services/backup/) |
| *Niezarządzane LRS dysków* | Lokalne ([LRS](storage-redundancy.md#locally-redundant-storage)) | [Azure Backup](https://azure.microsoft.com/services/backup/) |
| *Niezarządzane grs w warstwie dysków* | Krzyżowe region ([GRS](storage-redundancy.md#geo-redundant-storage)) | [Azure Backup](https://azure.microsoft.com/services/backup/)<br/>[Migawki spójne z](#alternative-solution-consistent-snapshots) |
| *Niezarządzane RA-GRS dysków* | Krzyżowe region ([RA-GRS](storage-redundancy.md#read-access-geo-redundant-storage)) | [Azure Backup](https://azure.microsoft.com/services/backup/)<br/>[Migawki spójne z](#alternative-solution-consistent-snapshots) |

Wysokiej dostępności najlepiej można spełnić przez przy użyciu hello dysków zarządzanych w zestawie dostępności wraz z usługą kopia zapasowa Azure. Jeśli używane są niezarządzane dysków, można nadal używać kopia zapasowa Azure do odzyskiwania po awarii. Jeśli toouse kopia zapasowa Azure, następnie biorąc [migawek spójnych](#alternative-solution-consistent-snapshots) zgodnie z opisem w dalszej części artykułu to alternatywne rozwiązanie tworzenia kopii zapasowych i odzyskiwania po awarii.

Opcje wysokiej dostępności, tworzenie kopii zapasowej i odzyskiwania po awarii na poziomie aplikacji lub infrastruktury może być reprezentowany jako poniżej:

| *Poziom* | Wysoka dostępność   | Kopii zapasowej / odzyskiwania po awarii |
| --- | --- | --- |
| *Aplikacji* | Zawsze włączone SQL | Azure Backup |
| *Infrastruktury*  | Zestaw dostępności  | GRS z migawki spójne z |

### <a name="using-hello-azure-backup-service"></a>Przy użyciu hello usługi Kopia zapasowa Azure

[Kopia zapasowa Azure](../backup/backup-azure-vms-introduction.md) może wykonywać kopie zapasowe maszyn wirtualnych z systemem Windows lub Linux toohello magazynu usług odzyskiwania Azure. Wykonywanie kopii zapasowej i przywracanie danych biznesowych o znaczeniu krytycznym jest skomplikowany hello fakt, że strategicznych danych biznesowych musi kopii zapasowej podczas aplikacji hello, które wywołują powitalne danych są uruchomione. tooaddress, to kopia zapasowa Azure zapewnia spójnych z aplikacją kopii zapasowych obciążeń firmy Microsoft przy użyciu hello tooensure woluminów usługi w tle (VSS), czy dane są zapisywane poprawnie toostorage. Dla maszyn wirtualnych systemu Linux tylko plik spójne kopie zapasowe są możliwe, ponieważ systemu Linux nie ma tooVSS równoważne funkcje.

![][1]

Jeśli kopia zapasowa Azure inicjuje zadania tworzenia kopii zapasowej w czasie hello zaplanowane, wyzwala zapasowy numer wewnętrzny hello zainstalowane w hello wirtualna tootake migawki punktu w czasie. Migawki w połączeniu z usługi VSS tooget migawki spójne hello dysków w maszynie wirtualnej hello bez konieczności tooshut go w dół. zapasowy numer wewnętrzny Hello w hello wirtualna opróżnia wszystkie zapisy przed wykonaniem migawki dotyczącej spójności hello wszystkich dysków hello. Po migawki hello hello dane są przesyłane przez kopia zapasowa Azure toohello magazynu kopii zapasowych. toomake hello procesu tworzenia kopii zapasowej bardziej efektywne hello usługa identyfikuje i transferuje tylko hello bloki danych, które uległy zmianie od czasu ostatniej kopii zapasowej hello.


toorestore, możesz wyświetlić hello dostępnych kopii zapasowych za pomocą usługi Kopia zapasowa Azure i inicjuje operację przywracania. Możesz utworzyć i przywracania kopii zapasowych Azure za pośrednictwem hello [portalu Azure](https://portal.azure.com/), [przy użyciu programu PowerShell](../backup/backup-azure-vms-automation.md ), lub za pomocą hello [interfejsu wiersza polecenia Azure](https://docs.microsoft.com/azure/xplat-cli-install). Aby uzyskać więcej informacji zobacz Kopia zapasowa Azure.

### <a name="steps-tooenable-backup"></a>TooEnable kroki tworzenia kopii zapasowej

Witaj poniższe kroki są najczęściej używanymi tooenable kopii zapasowych maszyn wirtualnych przy użyciu hello [Azure Portal](https://portal.azure.com/). Będą różne wersje, w zależności od danego scenariusza dokładne. Zobacz toohello [kopia zapasowa Azure](../backup/backup-azure-vms-introduction.md) dokumentacji, aby uzyskać szczegółowe informacje. Azure Backup również [obsługuje maszyny wirtualne z dyskami zarządzane](https://azure.microsoft.com/blog/azure-managed-disk-backup/).

1.  Tworzenie magazynu usług odzyskiwania dla maszyny Wirtualnej przy użyciu hello następujące kroki:

    a.  Przy użyciu hello [portalu Azure](https://portal.azure.com/), Przeglądaj wszystkie zasoby i odnaleźć "Magazyny usług odzyskiwania".

    b.  Na powitania menu Magazyny usług odzyskiwania, kliknij przycisk Dodaj i wykonaj hello kroki toocreate nowy magazyn w hello tego samego regionu hello maszyny Wirtualnej. Na przykład jeśli maszyna wirtualna znajduje się w regionie zachodnie stany USA, wybierz zachodnie stany USA hello magazynu.

2.  Sprawdź hello replikacji magazynu dla hello nowo utworzonego magazynu. toodo tego vault hello dostępu z hello usług odzyskiwania magazynów bloku, a następnie przejść toohello ustawienia lub tworzenia kopii zapasowej konfiguracji. Upewnij się, że hello GRS opcja jest domyślnie zaznaczona. Daje to pewność, że magazyn jest automatycznie replikowane tooa centrum danych dodatkowej. Na przykład magazynu w zachodnie stany USA będzie automatycznie replikowane tooEast Stanów Zjednoczonych.

3.  Skonfiguruj zasady tworzenia kopii zapasowej hello i wybierz hello maszyny Wirtualnej z hello sam interfejs użytkownika.

4.  Upewnij się, że hello, Agent usługi Kopia zapasowa jest zainstalowana na powitania maszyny Wirtualnej. Jeśli maszyna wirtualna została utworzona przy użyciu obrazu galerii Azure, agent usługi Kopia zapasowa hello już jest zainstalowany. W przeciwnym razie (Jeśli używasz niestandardowego obrazu), za pomocą instrukcji[hello Zainstaluj agenta maszyny Wirtualnej na maszynie wirtualnej hello](../backup/backup-azure-arm-vms-prepare.md#install-the-vm-agent-on-the-virtual-machine).

5.  Upewnij się, że tej maszyny Wirtualnej hello umożliwia łączności sieciowej hello toofunction usługi tworzenia kopii zapasowej. Wykonaj te instrukcje dla [połączeń sieciowych](../backup/backup-azure-arm-vms-prepare.md#network-connectivity).

6.  Po wykonaniu hello powyżej kroki hello kopii zapasowej zostanie uruchomiony w regularnych odstępach czasu określonych w hello zasad tworzenia kopii zapasowej. W razie potrzeby możesz wyzwolić hello pierwszej kopii zapasowej ręcznie z pulpitem nawigacyjnym magazynu hello na powitania portalu Azure.

Automatyzacja kopia zapasowa Azure za pomocą skryptów, można znaleźć w artykule zbyt[poleceń cmdlet programu PowerShell dla kopii zapasowej maszyny Wirtualnej](../backup/backup-azure-vms-automation.md).

### <a name="steps-for-recovery"></a>Procedura odzyskiwania

Jeśli konieczne toorepair lub skompiluj ponownie Maszynę wirtualną, można przywrócić hello maszyny Wirtualnej za pomocą dowolnego hello punktów odzyskiwania kopii zapasowej w magazynie hello. Istnieje kilka różnych opcji dla przeprowadzania odzyskiwania hello:

1.  Można utworzyć nowej maszyny Wirtualnej jako punktu w czasie reprezentacji kopii zapasowej maszyny wirtualnej.

2.  Można przywrócić hello dysków, a następnie użyć szablonu hello hello toocustomize maszyny Wirtualnej i Odbuduj hello przywrócić maszyny Wirtualnej. 

Zobacz instrukcje zbyt[maszyny wirtualne Azure Użyj portalu toorestore](../backup/backup-azure-arm-restore-vms.md#restoring-a-vm-during-azure-datacenter-disaster). dokument Hello wyjaśniono również hello wykonania określonych kroków przywracania kopii zapasowej maszyn wirtualnych toohello centrum danych sparowanego przy użyciu geograficznie nadmiarowego magazynu kopii zapasowych w przypadku awarii w centrum danych podstawowych hello hello. W takim przypadku kopia zapasowa Azure używa usługi obliczeniowe hello z maszyny wirtualnej hello region pomocniczy toocreate hello przywrócona.

Można również użyć programu PowerShell dla [przywracanie maszyny Wirtualnej](../backup/backup-azure-vms-automation.md#restore-an-azure-vm) lub [tworzenia nowej maszyny Wirtualnej z przywrócić dysków](../backup/backup-azure-vms-automation.md#create-a-vm-from-restored-disks).

## <a name="alternative-solution-consistent-snapshots"></a>Alternatywnych rozwiązań: Migawki spójne

Jeśli toouse hello Azure usługi tworzenia kopii zapasowej, można zaimplementować własny mechanizm tworzenia kopii zapasowej przy użyciu migawek. Jest skomplikowane toocreate migawki spójne z dla wszystkich dysków używanych przez Maszynę wirtualną i region tooanother te migawki są następnie replikowane. Z tego powodu Azure uwzględnia korzystanie z usług hello usługi Kopia zapasowa lepszym rozwiązaniem niż Tworzenie niestandardowego rozwiązania. Jeśli używasz RA-GRS/GRS magazynu dla dysków migawki są automatycznie replikowane tooa centrum danych dodatkowej. Jeśli używasz magazynu LRS w przypadku dysków, konieczne będzie tooreplicate hello danych samodzielnie. Aby uzyskać więcej informacji, zobacz [kopia zapasowa Azure niezarządzane dysków maszyny Wirtualnej z migawkami przyrostowe](storage-incremental-snapshots.md).

Migawka jest reprezentację obiektu w określonym punkcie w czasie. Migawki będą naliczane rozliczeń dla hello rozmiar przyrostowej danych hello go blokad. Aby uzyskać więcej informacji, zobacz [utworzenia migawki obiektu blob](storage-blob-snapshots.md).

### <a name="creating-snapshots-while-hello-vm-is-running"></a>Tworzenie migawki, natomiast hello wirtualna jest uruchomiona.

Można utworzyć migawkę w dowolnym momencie, jeśli hello maszyna wirtualna jest uruchomiona, jest nadal dane przesyłane strumieniowo toohello dysków, i hello migawki może zawierać częściowe operacje, które zostały w locie. Ponadto jeśli kilka dysków są zaangażowane, migawek hello różnych dysków może wystąpić w różnym czasie, co oznacza, że te migawki nie może być skoordynowany sposób. Jest to szczególnie kłopotliwe w sytuacji dla woluminów rozłożonych, którego pliki mogą zostać uszkodzone, jeśli trwa zmian podczas tworzenia kopii zapasowej.

tooavoid takiej sytuacji hello procesu tworzenia kopii zapasowej musi implementować hello następujące kroki:

1.  Zablokuj wszystkie dyski hello

2.  Flush hello wszystkich oczekujących operacji zapisu

3.  Następnie [utworzenia migawki obiektu blob](storage-blob-snapshots.md) dla wszystkich hello dysków

Niektóre aplikacje systemu Windows, takich jak SQL Server mechanizm skoordynowany sposób tworzenia kopii zapasowej za pośrednictwem spójnych z aplikacją kopii zapasowych VSS toocreate. W systemie Linux można użyć narzędzia, takiego jak fsfreeze koordynacji hello dysków, co zapewnia spójne z plikami kopii zapasowych, ale nie migawki spójne z aplikacjami. Ten proces jest skomplikowane, więc i należy rozważyć użycie [kopia zapasowa Azure](../backup/backup-azure-vms-introduction.md) lub rozwiązanie tworzenia kopii zapasowych innych firm, które już wdrożyć.

Kolekcja skoordynowanego migawek dla wszystkich dysków maszyny Wirtualnej hello, reprezentujący określonego punktu w czasie widok hello maszyny Wirtualnej spowoduje Hello powyżej procesu. To jest punkt przywracania kopii zapasowej hello maszyny Wirtualnej. Możesz powtarzać proces hello w zaplanowanych odstępach czasu toocreate okresowe kopie zapasowe. Poniżej zamieszczono kroki hello zbyt[kopiowania hello kopii zapasowych tooanother regionu](#copy-the-snapshots-to-another-region) do odzyskiwania po awarii.

### <a name="creating-snapshots-while-hello-vm-is-offline"></a>Tworzenie migawki, natomiast hello maszyna wirtualna jest w trybie offline

Inną opcję toocreate spójne tworzenie kopii zapasowych jest zamykana hello maszyny Wirtualnej i obiektów blob z argumentami migawki każdego dysku. To jest łatwiejsze niż koordynujący migawki uruchomionej maszyny wirtualnej, ale wymaga to kilka minut przestoju. Dla tego procesu wykonaj następujące kroki:

1. Zamknij hello maszyny Wirtualnej.

2. Utwórz migawkę każdej blob dysku VHD, który zajmuje tylko kilka sekund.

    toocreate migawki, można użyć [PowerShell](storage-powershell-guide-full.md#how-to-manage-azure-blob-snapshots), hello [interfejsu API Rest magazynu Azure](https://msdn.microsoft.com/library/azure/ee691971.aspx), [interfejsu wiersza polecenia Azure](https://docs.microsoft.com/azure/xplat-cli-install), lub jeden z biblioteki klienta magazynu Azure hello takich jak [ Witaj biblioteki klienta usługi Storage dla platformy .NET](https://msdn.microsoft.com/library/azure/hh488361.aspx).

3. Uruchom hello maszyny Wirtualnej, która kończy hello przestoju. Zwykle hello cały proces zostanie zakończony w ciągu kilku minut.

Ten proces zapewnia zbiór migawki spójne z dla wszystkich dysków hello, podając punktu przywracania hello maszyny Wirtualnej. Poniżej zamieszczono hello kroki toocopy hello migawki tooanother region do odzyskiwania po awarii.

### <a name="copy-hello-snapshots-tooanother-region"></a>Skopiuj hello migawki tooanother regionu

Tworzenie migawek hello wyłącznie nie może być wystarczające do odzyskiwania po awarii. Muszą także replikować hello migawek kopii zapasowych tooanother regionu.

Jeśli używasz GRS lub RA-GRS dla dysków, następnie hello migawki są replikowane toohello region pomocniczy automatycznie. Może istnieć kilka minut opóźnienie przed hello replikacji, a jeśli Centrum danych podstawowych hello ulegnie awarii, przed migawki hello Zakończ replikacji, nie będzie możliwe tooaccess hello migawek z centrum danych dodatkowej hello. to prawdopodobieństwo Hello jest mała.

> [!Note] 
> Tylko o hello dysków w ramach konta GRS lub RA-GRS nie chroni hello maszyny Wirtualnej po awarii. Należy również tworzenie migawek skoordynowanego albo użyć kopia zapasowa Azure. Jest to wymagane toorecover spójne tooa maszyny Wirtualnej.

Jeśli używasz LRS, należy skopiować natychmiast po utworzeniu migawki hello hello migawki tooa innego konta magazynu. docelowy kopiowania Hello może być konta magazynu LRS w innym regionie, co powoduje kopiowania hello znajdujące się w regionie zdalnego. Można również skopiować konta magazynu RA-GRS tooan migawki hello hello tego samego regionu. W takim przypadku migawki hello będzie zdalnego regionie dodatkowym opóźnieniem replikowanych toohello. Kopia zapasowa jest chronione przed awarii w lokacji głównej powitania po zakończeniu kopiowania hello i replikacji.

toocopy Twojego przyrostowe migawki do odzyskiwania po awarii, przejrzeć instrukcje hello w [kopia zapasowa Azure niezarządzane dysków maszyny Wirtualnej z migawkami przyrostowe](storage-incremental-snapshots.md).

![][2]

### <a name="recovery-from-snapshots"></a>Odzyskiwanie z migawki

tooretrieve migawkę, skopiuj go toomake nowego obiektu blob. Jeśli kopiujesz hello migawki z kontem podstawowym hello, możesz skopiować hello migawki za pośrednictwem podstawowego obiektu blob toohello hello migawki, w związku z tym podczas przywracania hello dysku toohello migawki; jest to nazywane podwyższania poziomu hello migawki. Jeśli kopia zapasowa migawki hello są kopiowane z pomocniczego konta (w przypadku hello RA-GRS), musi on być kopiowane tooa kontem podstawowym. Możesz skopiować migawki [przy użyciu programu PowerShell](storage-powershell-guide-full.md#how-to-copy-a-snapshot-of-a-blob) lub za pomocą narzędzia AzCopy hello. Aby uzyskać więcej informacji, zobacz [Transfer danych za pomocą wiersza polecenia Azcopy hello](storage-use-azcopy.md).

W przypadku hello maszyn wirtualnych z wieloma dyskami, należy skopiować wszystkie hello migawek, które są częścią hello koordynowane przez sam punkt przywracania. Po skopiowaniu hello obiekty BLOB dysków VHD toowritable dla migawki można użyć toorecreate obiekty BLOB hello maszyny Wirtualnej przy użyciu szablonu hello na powitania maszyny Wirtualnej.

## <a name="other-options"></a>Inne opcje

### <a name="sql-server"></a>Oprogramowanie SQL Server

Program SQL Server uruchomiony na maszynie wirtualnej ma własną toobackup wbudowanych możliwości tooAzure bazy danych programu SQL Server magazynu obiektów Blob lub udziału plików. Konto magazynu hello jest GRS lub RA-GRS, można przejść do tych kopii zapasowych w centrum danych pomocniczego konta magazynu hello w razie awarii, hello z hello takie same ograniczenia jak wspomniano wcześniej. Aby uzyskać więcej informacji, zobacz [kopii zapasowej i przywracania dla programu SQL Server w usłudze Azure Virtual Machines](../virtual-machines/windows/sql/virtual-machines-windows-sql-backup-recovery.md). Dodanie toobackup i przywracanie [programu SQL Server zawsze włączonych grup dostępności](../virtual-machines/windows/sql/virtual-machines-windows-sql-high-availability-dr.md) można zachować w replikach pomocniczych baz danych toogreatly skrócić czas odzyskiwania po awarii hello.

## <a name="other-considerations"></a>Inne zagadnienia

Ten artykuł został omówiony sposób toobackup lub wykonaj migawki maszyn wirtualnych i ich odzyskiwania po awarii dysków toosupport i w jaki sposób toouse tych toorecover. Model usługi Azure Resource Manager hello wiele osób za pomocą szablonów toocreate ich maszyn wirtualnych i pozostałą infrastrukturą na platformie Azure. Można użyć szablonu toocreate maszynę Wirtualną, która ma hello tej samej konfiguracji zawsze. Jeśli używasz niestandardowych obrazów do tworzenia maszyn wirtualnych, należy również upewnić się, obrazy są chronione przy użyciu toostore kont RA-GRS je.

W rezultacie procesu tworzenia kopii zapasowej może być kombinacją dwie czynności:

1. Witaj kopii zapasowej danych (dyski)
2. Konfiguracja kopii zapasowej hello (szablony, niestandardowe obrazy)

W zależności od hello opcję tworzenia kopii zapasowej, można wybrać może mieć kopii zapasowej hello toohandle hello danych i konfiguracji hello, lub hello usługi tworzenia kopii zapasowej może obsługiwać to wszystko dla Ciebie.

## <a name="appendix---understanding-hello-impact-of-lrs-grs-and-ra-grs"></a>Dodatek - zrozumienie wpływu hello LRS, GRS i RA-GRS

Dla konta magazynu na platformie Azure, istnieją trzy typy nadmiarowość danych, które należy wziąć pod uwagę dotyczące odzyskiwania po awarii — magazyn lokalnie nadmiarowy (LRS), geograficznie nadmiarowego (GRS), lub odczytu z magazynu geograficznie nadmiarowego z dostępu (RA-GRS). 

Lokalnie magazyn geograficznie nadmiarowy (LRS) przechowuje trzy kopie danych hello w hello tym samym centrum danych. Podczas zapisywania danych hello, wszystkie trzy kopie są aktualizowane przed zwróceniem Powodzenie toohello wywołującego, dlatego wiadomo, że są one identyczne. Na dysku jest chronione przed błędy lokalne, ponieważ jest on bardzo mało prawdopodobne, że wszystkie trzy kopie będzie mieć wpływ na na powitania tym samym czasie. W przypadku hello LRS nie nie nadmiarowość geograficzna, więc hello dysku nie jest chroniony poważnej awarii, które mogą mieć wpływ na jednostkę Centrum lub magazynu danych.

Z GRS i RA-GRS trzy kopie danych są przechowywane w regionie podstawowym hello (wybrane przez użytkownika), a więcej trzy kopie danych są przechowywane w odpowiedni region pomocniczy (ustawione przez platformę Azure). Na przykład jeśli dane są przechowywane w zachodnie stany USA, hello dane zostaną zreplikowane tooEast Stanów Zjednoczonych. Odbywa się asynchronicznie, a istnieje małe opóźnienia między toohello aktualizacje podstawowego i pomocniczego. Repliki hello dyski w lokacji dodatkowej hello są zgodne na podstawie na dysku (z opóźnieniem hello), ale replik wielu aktywnych dysków mogą nie być zsynchronizowane **ze sobą**. toohave repliki spójnej na wielu dyskach, migawek spójnych są wymagane.

Witaj podstawowa różnica między GRS i RA-GRS polega na tym, że z RA-GRS, możesz przeczytać hello pomocniczej kopii w dowolnym momencie. W przypadku problemu, który renderuje hello danych w regionie podstawowym hello jest niedostępny, hello Azure zespołu spowoduje, że każdy dostępu toorestore nakładu pracy. Gdy hello podstawowej nie działa, jeśli masz RA-GRS włączone, można dostęp do danych hello w centrum danych dodatkowej hello. W związku z tym jeśli planujesz tooread z repliki hello, gdy hello podstawowy jest niedostępny, następnie RA-GRS należy rozważyć.

Jeśli okaże się toobe znaczne awarii, hello Azure zespołu może wyzwolić awarię replikacji geograficznej — warstwa i zmień hello głównej DNS wpisy toopoint toosecondary magazynu. W tym momencie masz albo GRS lub RA-GRS włączona, można przejść do hello danych w regionie hello, używany hello toobe dodatkowej. Innymi słowy Twoje konto magazynu GRS i występuje problem, można przejść do magazynu pomocniczego hello tylko wtedy, gdy geograficznie trybu failover.

Aby uzyskać więcej informacji, zobacz [jakie toodo w przypadku wystąpienia awarii usługi Azure Storage](storage-disaster-recovery-guidance.md). 

Należy pamiętać, że Microsoft kontroluje, czy do pracy awaryjnej. Tryb failover nie są kontrolowane na konto magazynu, w związku z tym nie zdecydowano poszczególnych odbiorców. tooimplement odzyskiwania po awarii dla określonego magazynu kont lub dysków maszyny wirtualnej, należy użyć hello techniki opisane wcześniej w tym artykule.



[1]: ./media/storage-backup-and-disaster-recovery-for-azure-iaas-disks/backup-and-disaster-recovery-for-azure-iaas-disks-1.png
[2]: ./media/storage-backup-and-disaster-recovery-for-azure-iaas-disks/backup-and-disaster-recovery-for-azure-iaas-disks-2.png