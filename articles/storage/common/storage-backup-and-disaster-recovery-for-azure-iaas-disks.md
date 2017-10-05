---
title: "Kopia zapasowa i odzyskiwanie po awarii dla dysków IaaS platformy Azure | Dokumentacja firmy Microsoft"
description: "W tym artykule Wyjaśnijmy, jak planowanie tworzenia kopii zapasowych i odzyskiwania awaryjnego (DR) maszyn wirtualnych IaaS (maszyny wirtualne) oraz dyski na platformie Azure. W tym dokumencie opisano zarówno zarządzane i niezarządzane dysków"
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
ms.openlocfilehash: 03d38bc3383b5fd39eca5ca67c315b34b98f0c39
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
# <a name="backup-and-disaster-recovery-for-azure-iaas-disks"></a>Kopia zapasowa i odzyskiwanie po awarii dla dysków IaaS platformy Azure

W tym artykule Wyjaśnijmy, jak planowanie tworzenia kopii zapasowych i odzyskiwania awaryjnego (DR) maszyn wirtualnych IaaS (maszyny wirtualne) oraz dyski na platformie Azure. W tym dokumencie opisano zarówno zarządzane i niezarządzane dysków.

Zostanie najpierw omawianiu wbudowanych usterek tolerancji możliwości platformy Azure umożliwiające ochronę przed awariami lokalnego. Następnie omówiono w scenariuszach po awarii nie są w pełni objęte wbudowanych możliwości, który jest opisany w tym dokumencie tematem głównym. Poniżej opisano również kilka przykładowe scenariusze obciążenie, gdzie może stosować inną uwagi dotyczące tworzenia kopii zapasowych i odzyskiwania po awarii. Firma Microsoft może przejrzeć możliwych rozwiązań dla odzyskiwania po awarii dysków IaaS. 

## <a name="introduction"></a>Wprowadzenie

Platforma Azure korzysta różne metody nadmiarowość i odporność na uszkodzenia w celu ochrony klientów przed awariami sprzętu zlokalizowanego, które mogą wystąpić. Błędy lokalne mogą obejmować problemy z maszyną serwera magazynu Azure, która przechowuje dane dla dysku wirtualnego lub w przypadku awarii dysków SSD i HDD na tym serwerze. Takie błędy składnika izolowanego sprzętu może się zdarzyć, podczas wykonywania normalnych operacji i platforma zaprojektowano w celu zapewnienie odporności na awarie tych. Główne awarii może spowodować błędy lub inaccessibility dużej liczby serwerów magazynu lub całe centrum danych. Maszyn wirtualnych i dyski są zwykle chronione zlokalizowanych awarii, dodatkowe kroki są niezbędne do ochrony obciążenia region na poziomie awarii krytycznego (na przykład poważnej awarii), które mogą wpłynąć na Twojej maszyny Wirtualnej i dysków.

Oprócz możliwości platformy błędów mogą wystąpić problemy z aplikacją klienta lub danych. Na przykład nowa wersja aplikacji mogą przypadkowo należy podziału, Zmień dane. W takim przypadku można przywrócić aplikacji i danych do poprzednich wersji zawierający ostatniego znanego dobrego stanu. Wymagane jest utrzymanie regularnych kopii zapasowych.

Regionalnej awarii należy wykonać kopię zapasową dysków maszyn wirtualnych IaaS w innym regionie. 

Zanim przyjrzymy opcje tworzenia kopii zapasowych i odzyskiwania po awarii umożliwia recap kilku dostępnych metod obsługi zlokalizowanych awarii.

### <a name="azure-iaas-resiliency"></a>Odporność IaaS platformy Azure

*Odporność* odwołuje się do uszkodzenia normalne błędów występujących w składników sprzętowych. Odporność jest możliwość skutków błędów i kontynuować działanie. Nie jest o unikanie błędów, ale odpowiadać na awarie w taki sposób, który pozwala uniknąć przestoju lub utraty danych. Celem odporności jest do zwrócenia aplikacji w pełni funkcjonalnej stan w przypadku awarii. Azure maszyn wirtualnych i dyski mają na celu zapewnienie odporności na typowych błędów sprzętu. Daj nam przyjrzeć się, jak platforma Azure IaaS zapewnia to elastyczność.

Maszyna wirtualna składa się głównie z dwóch części: (1) A obliczeniowe serwera i (2) dyski stałe. Wpływ zarówno na odporność na uszkodzenia maszyny wirtualnej.

Jeśli serwer hosta obliczeń platformy Azure, która przechowuje maszyny Wirtualnej błędów sprzętu (która jest rzadko), Azure jest przeznaczona na automatyczne przywracanie maszyny Wirtualnej na innym serwerze. W takim przypadku wystąpią ponowne uruchomienie komputera, a maszyna wirtualna musi być Utwórz kopię zapasową po pewnym czasie. Azure automatycznie wykrywa takie awarie sprzętu i wykonuje odzyskiwanie, aby pomóc, upewnij się, że klient maszyna wirtualna będzie dostępna tak szybko, jak to możliwe.

Dotyczących dysków IaaS trwałości danych ma kluczowe znaczenie dla platformy magazynu trwałego. Azure klienci mają ważnymi aplikacji uruchomionych na IaaS i są one zależne od trwałość danych. Projekty platformy Azure ochrony tych dysków IaaS przy użyciu trzech nadmiarowe kopie dane przechowywane lokalnie, zapewniając wysoką trwałością przed awariami lokalnego. W przypadku niepowodzenia jednym ze składników sprzętu, które przechowuje dysku maszyny Wirtualnej nie ma wpływu na ponieważ istnieją dwie kopie dodatkowe do obsługi żądań dysku. Działa dobrze nawet w przypadku awarii dwóch składniki sprzętowe obsługujące dysku w tym samym czasie (co jest bardzo rzadko). Aby ułatwić, upewnij się, że firma Microsoft zachowuje zawsze trzy repliki, usługi Magazyn Azure automatycznie spowoduje utworzenie nowej kopii w tle dane, jeśli jeden z trzech kopii stał się niedostępny. W związku z tym nie należy używać RAID z dyskami Azure odporności na uszkodzenia. Proste RAID 0 konfiguracji powinny być wystarczające stosowanie dysków, jeśli jest to niezbędne do utworzenia większych woluminów.

Z powodu tej architektury **Azure spójnie wydał korporacyjnej trwałości dla IaaS z branży dysków ZERO % [firmie częstość niepowodzeń](https://en.wikipedia.org/wiki/Annualized_failure_rate).**

Usterki sprzętu zlokalizowanych na mocy obliczeniowej hosta lub w platformie magazynu mogą czasami doprowadzi do tymczasowej niedostępności dla maszyny Wirtualnej, która jest objęta [umowy SLA platformy Azure](https://azure.microsoft.com/support/legal/sla/virtual-machines/) dostępności maszyny Wirtualnej. Platforma Azure udostępnia również branży umowa SLA dla pojedynczego wystąpień maszyn wirtualnych, które używają dysków magazyn w warstwie Premium.

Aby chronić obciążeń aplikacji z przestoju z powodu tymczasowej niedostępności dysku lub maszyny Wirtualnej, klienci mogą korzystać z [zestawów dostępności](../../virtual-machines/windows/manage-availability.md). Co najmniej dwie maszyny wirtualne w zestawie dostępności zapewnia nadmiarowość dla aplikacji. Azure utworzy tych maszyn wirtualnych i dyski w domenach awarii oddzielne z różnych składników zasilania, sieci i serwera. W związku z tym awarie sprzętowe zlokalizowanego zwykle nie wpływają na wiele maszyn wirtualnych w zestawie w tym samym czasie, zapewnienie wysokiej dostępności dla aplikacji. Jest on uznawany za dobrą praktyką jest korzystanie z zestawów dostępności, gdy wymagana jest wysoka dostępność. Aby uzyskać więcej informacji zobacz aspekty odzyskiwania po awarii opisanymi poniżej.

### <a name="backup-and-disaster-recovery"></a>Kopii zapasowych i odzyskiwania po awarii

Odzyskiwania awaryjnego (DR) jest możliwość odzyskania z zdarzeń, ale rzadko głównych: błędy z systemem innym niż przejściowy, całej skali, takie jak zakłócenia, która wpływa na całą regionu. Odzyskiwanie po awarii obejmuje kopii zapasowej danych i archiwizowania i może zawierać ręcznej interwencji, takich jak przywracanie z kopii zapasowej bazy danych.

Platforma Azure wbudowaną ochronę przed awariami zlokalizowanych mogą nie pełni chronić maszyny wirtualne/dysków w przypadku awarii głównych, co może powodować awarie na dużą skalę. W tym krytycznego zdarzenia, takie jak trafienia huragan, trzęsienia ziemi, fire lub awarie jednostki sprzętowe dużą skalę centrum danych. Ponadto mogą wystąpić błędy z powodu problemy dotyczące danych lub aplikacji.

Aby lepiej chronić obciążeń IaaS z awarii, należy zaplanować nadmiarowości i kopie zapasowe, aby włączyć odzyskiwanie. Podczas odzyskiwania po awarii należy zaplanować nadmiarowości i tworzenie kopii zapasowych w innej lokalizacji geograficznej od lokacji głównej. Dzięki temu, upewnij się, że kopia zapasowa nie ma wpływu na tego samego zdarzenia, który pierwotnie wpływ na maszynie Wirtualnej lub dysków. Aby uzyskać więcej informacji, zobacz [odzyskiwania po awarii dla aplikacji w oparciu Azure](https://docs.microsoft.com/azure/architecture/resiliency/disaster-recovery-azure-applications).

Uwagi dotyczące programu DR mogą obejmować następujące aspekty:

1. Wysokiej dostępności (HA) to funkcja aplikacji kontynuowanie działania w dobrej kondycji, bez przestojów znaczące. Przez "dobrej kondycji," oznacza możemy aplikacji jest elastyczny i użytkownicy mogą połączyć się z aplikacją i korzystać z niego. Niektórych kluczowych aplikacji i baz danych może być musi być dostępny zawsze, nawet jeśli błędy występują w platformie. Dla tych zadań może być konieczne planowanie nadmiarowości na potrzeby aplikacji, a także dane.

2. Trwałość danych: W niektórych przypadkach głównym zagadnieniem jest zapewnienie, że dane zostaną zachowane w przypadku awarii. Dlatego może być konieczne kopii zapasowej danych w innej lokacji. W przypadku takich obciążeń mogą nie być potrzebne pełne nadmiarowości na potrzeby aplikacji, ale także regularne tworzenie kopii zapasowych dysków.

## <a name="backup-and-dr-scenarios"></a>Kopia zapasowa i scenariuszy odzyskiwania po awarii

Oto kilka przykładów typowych scenariuszy obciążenia aplikacji oraz zagadnienia dotyczące planowania odzyskiwania po awarii.

### <a name="scenario-1-major-database-solutions"></a>Scenariusz 1: Głównej bazy danych rozwiązania

Rozważ serwer produkcyjny bazy danych, takich jak SQL Server lub Oracle, który może obsługiwać wysokiej dostępności. Krytyczne produkcji aplikacji i użytkowników są zależne od tej bazy danych. Plan odzyskiwania po awarii dla tego systemu może być konieczne obsługuje następujące wymagania:

1. Dane muszą być chronione i możliwe do odzyskania.
2.  Serwer musi być dostępny do użycia.

Może to wymagać utrzymania repliki bazy danych w innym regionie jako kopii zapasowej. W zależności od wymagań dotyczących dostępności serwera i odzyskiwanie danych rozwiązanie może należeć do zakresu od aktywny-aktywny lub aktywny / pasywny lokacji repliki do okresowe tworzenie kopii zapasowych danych. Relacyjnych baz danych, takich jak SQL Server i Oracle zapewniają różne opcje replikacji. Dla programu SQL Server [programu SQL Server zawsze włączonych grup dostępności](https://msdn.microsoft.com/library/hh510230.aspx) można użyć w celu zapewnienia wysokiej dostępności.

Bazy danych NoSQL, takie jak bazy danych MongoDB obsługują również [replik](https://docs.mongodb.com/manual/replication/) nadmiarowości. Można replik wysokiej dostępności.

### <a name="scenario-2-a-cluster-of-redundant-vms"></a>Scenariusz 2: Klastra nadmiarowe maszyny wirtualne

Należy wziąć pod uwagę obciążenia obsługiwane przez klaster maszyn wirtualnych, które zapewniają nadmiarowość i równoważenie obciążenia. Przykładem jest klastra Cassandra wdrożone w regionie. Ten typ architektury już zapewnia wysoki poziom nadmiarowości w tym regionie. Jednak aby chronić obciążenia w przypadku regionalnej awarii poziomu, należy rozważyć rozpraszania klastra w dwóch regionach lub wprowadzanie okresowe kopie zapasowe w innym regionie.

### <a name="scenario-3-iaas-application-workload"></a>Scenariusz 3: IaaS aplikacji obciążenia

Może to być typowe produkcji pracą maszyny Wirtualnej platformy Azure. Na przykład może być serwerem sieci web lub serwera plików zawartości i innych zasobów w lokacji. Może to być również aplikacji biznesowej niestandardowej uruchomione na maszynie Wirtualnej, które przechowywane jego dane, zasobów i stan aplikacji dysków maszyny Wirtualnej. W takim przypadku koniecznie upewnij się, że możesz korzystać z kopii zapasowych na bieżąco. Częstotliwość wykonywania kopii zapasowych powinny być oparte na rodzaju obciążenia maszyny Wirtualnej. Na przykład jeśli aplikacja jest uruchamiana codziennie i modyfikuje danych, następnie kopii zapasowej należy podjąć co godzinę.

Innym przykładem jest serwer raportowania ściągania danych z innych źródeł i generuje raporty zagregowanych. Utraty tej maszyny Wirtualnej lub dysków doprowadzi do utraty raporty. Jednak może być możliwe ponownie uruchomić proces raportowania i ponownie wygenerować danych wyjściowych. W takim przypadku naprawdę masz utraty danych, nawet jeśli serwer raportowania o awarii, tak aby można było wyższy poziom tolerancji utraty części danych na serwerze raportowania. W takim przypadku mniej częste wykonywanie kopii zapasowych jest opcję, aby zmniejszyć koszty.

### <a name="scenario-4-iaas-application-data-issues"></a>Scenariusz 4: Problemy z danych aplikacji IaaS

Masz aplikację, która oblicza, przechowuje i służy krytyczne komercyjnych danych, takie jak informacje o cenach. Nowa wersja aplikacji ma usterki oprogramowania niepoprawnie obliczana ceny i uszkodzone dane commerce obsługiwane przez platformę. W tym miejscu będą najlepszy plan działania do przywrócenia starszej wersji aplikacji i danych. Aby włączyć tę opcję, należy wykonać okresowe kopie zapasowe systemu.

## <a name="disaster-recovery-solution-azure-backup-service"></a>Rozwiązanie odzyskiwania po awarii: Usługa Kopia zapasowa Azure

[Usługa Kopia zapasowa Azure](https://azure.microsoft.com/services/backup/) może służyć do tworzenia kopii zapasowych i odzyskiwania po awarii, a w przypadku [dysków zarządzanych](../../virtual-machines/windows/managed-disks-overview.md) oraz [niezarządzane dysków](../../virtual-machines/windows/about-disks-and-vhds.md#unmanaged-disks). Zadanie tworzenia kopii zapasowej można utworzyć na podstawie czasu tworzenia kopii zapasowych, łatwe przywrócenie maszyny Wirtualnej i zasady przechowywania kopii zapasowych. 

Jeśli używasz [dysków Premium Storage](storage-premium-storage.md), [dysków zarządzanych](../../virtual-machines/windows/managed-disks-overview.md), lub innych typów dysku z [magazyn lokalnie nadmiarowy (LRS)](storage-redundancy.md#locally-redundant-storage) opcji jest szczególnie ważne wykorzystać okresowe DR kopie zapasowe. Kopia zapasowa Azure przechowuje dane w magazynie usług odzyskiwania do przechowywania długoterminowego. Wybierz [magazyn geograficznie nadmiarowy (GRS)](storage-redundancy.md#geo-redundant-storage) opcji magazynu usług odzyskiwania kopii zapasowej. Który będzie upewnij się, że kopie zapasowe są replikowane w innym regionie Azure, zabezpieczenia z regionalnej awarii.

Dla [niezarządzane dysków](../../virtual-machines/windows/about-disks-and-vhds.md#unmanaged-disks), można użyć typu magazynu LRS dysków IaaS, ale upewnij się, że kopia zapasowa Azure jest włączone z opcją grs w warstwie magazynu usług odzyskiwania.

**Jeśli używasz [GRS](storage-redundancy.md#geo-redundant-storage)/[RA-GRS](storage-redundancy.md#read-access-geo-redundant-storage) opcji dla niezarządzanego dysków, można nadal konieczne migawek spójnych kopii zapasowych i odzyskiwania po awarii.** Należy użyć jednego [usługi Kopia zapasowa Azure](https://azure.microsoft.com/services/backup/) lub [migawki spójne z](#alternative-solution-consistent-snapshots).

Poniżej znajduje się podsumowanie rozwiązania dla odzyskiwania po awarii.

| Scenariusz | Automatyczne replikacji | Rozwiązanie odzyskiwania po awarii |
| --- | --- | --- |
| *Dyski magazynu w warstwie Premium* | Lokalne ([LRS](storage-redundancy.md#locally-redundant-storage)) | [Azure Backup](https://azure.microsoft.com/services/backup/) |
| *Managed Disks* | Lokalne ([LRS](storage-redundancy.md#locally-redundant-storage)) | [Azure Backup](https://azure.microsoft.com/services/backup/) |
| *Niezarządzane LRS dysków* | Lokalne ([LRS](storage-redundancy.md#locally-redundant-storage)) | [Azure Backup](https://azure.microsoft.com/services/backup/) |
| *Niezarządzane grs w warstwie dysków* | Krzyżowe region ([GRS](storage-redundancy.md#geo-redundant-storage)) | [Azure Backup](https://azure.microsoft.com/services/backup/)<br/>[Migawki spójne z](#alternative-solution-consistent-snapshots) |
| *Niezarządzane RA-GRS dysków* | Krzyżowe region ([RA-GRS](storage-redundancy.md#read-access-geo-redundant-storage)) | [Azure Backup](https://azure.microsoft.com/services/backup/)<br/>[Migawki spójne z](#alternative-solution-consistent-snapshots) |

Wysokiej dostępności najlepiej można spełnić przez przy użyciu dysków zarządzanych w zestawie dostępności wraz z usługą kopia zapasowa Azure. Jeśli używane są niezarządzane dysków, można nadal używać kopia zapasowa Azure do odzyskiwania po awarii. Jeśli nie można użyć usługi Kopia zapasowa Azure, następnie biorąc [migawek spójnych](#alternative-solution-consistent-snapshots) zgodnie z opisem w dalszej części artykułu to alternatywne rozwiązanie tworzenia kopii zapasowych i odzyskiwania po awarii.

Opcje wysokiej dostępności, tworzenie kopii zapasowej i odzyskiwania po awarii na poziomie aplikacji lub infrastruktury może być reprezentowany jako poniżej:

| *Poziom* | Wysoka dostępność   | Kopii zapasowej / odzyskiwania po awarii |
| --- | --- | --- |
| *Aplikacji* | Zawsze włączone SQL | Azure Backup |
| *Infrastruktury*  | Zestaw dostępności  | GRS z migawki spójne z |

### <a name="using-the-azure-backup-service"></a>Za pomocą usługi tworzenia kopii zapasowej systemu Azure

[Kopia zapasowa Azure](../../backup/backup-azure-vms-introduction.md) może wykonywać kopie zapasowe maszyn wirtualnych systemem Windows lub Linux do magazynu usług odzyskiwania Azure. Tworzenie kopii zapasowej i przywracanie danych biznesowych o znaczeniu krytycznym skomplikowane jest fakt, że strategicznych danych biznesowych kopie zapasowe uruchomionej aplikacji, które tworzą dane. Aby rozwiązać ten problem, kopia zapasowa Azure udostępnia spójnych z aplikacją kopii zapasowych dla obciążeń firmy Microsoft przy użyciu woluminów w tle Service (VSS) do zapewnienia poprawnie zapisywania danych do magazynu. Dla maszyn wirtualnych systemu Linux tylko plik spójne kopie zapasowe są możliwe, ponieważ systemu Linux nie ma funkcji odpowiednikiem VSS.

![](./media/storage-backup-and-disaster-recovery-for-azure-iaas-disks/backup-and-disaster-recovery-for-azure-iaas-disks-1.png)   

Jeśli kopia zapasowa Azure inicjuje zadania tworzenia kopii zapasowej w zaplanowanym terminie, wyzwala kopii zapasowej rozszerzenia zainstalowane na maszynie wirtualnej, aby utworzyć migawkę punktu w czasie. Migawki w połączeniu z usługi VSS można pobrać migawki spójne z dysków w maszynie wirtualnej bez konieczności go zamknąć. Zapasowy numer wewnętrzny w maszynie Wirtualnej opróżnienia wszystkich zapisy przed wykonaniem migawki dotyczącej spójności wszystkich dysków. Po migawki, dane są przesyłane przez kopię zapasową Azure do magazynu kopii zapasowych. Aby proces tworzenia kopii zapasowej bardziej wydajne, usługa identyfikuje i transferuje tylko bloki danych, które uległy zmianie od czasu ostatniej kopii zapasowej.


Aby przywrócić, można wyświetlić dostępnych kopii zapasowych za pomocą usługi Kopia zapasowa Azure i inicjuje operację przywracania. Możesz utworzyć i przywracania kopii zapasowych Azure za pośrednictwem [portalu Azure](https://portal.azure.com/), [przy użyciu programu PowerShell](../../backup/backup-azure-vms-automation.md ), lub za pomocą [interfejsu wiersza polecenia Azure](https://docs.microsoft.com/azure/xplat-cli-install). Aby uzyskać więcej informacji zobacz Kopia zapasowa Azure.

### <a name="steps-to-enable-backup"></a>Kroki w celu włączenia kopii zapasowej

Poniższe kroki są zwykle używane do włączenia kopii zapasowych maszyn wirtualnych przy użyciu [Azure Portal](https://portal.azure.com/). Będą różne wersje, w zależności od danego scenariusza dokładne. Zapoznaj się [kopia zapasowa Azure](../../backup/backup-azure-vms-introduction.md) dokumentacji, aby uzyskać szczegółowe informacje. Azure Backup również [obsługuje maszyny wirtualne z dyskami zarządzane](https://azure.microsoft.com/blog/azure-managed-disk-backup/).

1.  Tworzenie magazynu usług odzyskiwania dla maszyny Wirtualnej, wykonując następujące czynności:

    a.  Przy użyciu [portalu Azure](https://portal.azure.com/), Przeglądaj wszystkie zasoby i odnaleźć "Magazyny usług odzyskiwania".

    b.  W menu Magazyny usług odzyskiwania kliknij przycisk Dodaj, a następnie wykonaj kroki, aby utworzyć nowy magazyn, w tym samym regionie co maszyna wirtualna. Na przykład jeśli maszyna wirtualna znajduje się w regionie zachodnie stany USA, wybierz zachodnie stany USA magazynu.

2.  Sprawdź replikacji magazynu dla nowo utworzonego magazynu. Aby to zrobić, uzyskać dostęp do magazynu w bloku Magazyny usług odzyskiwania i przejdź do ustawień lub tworzenia kopii zapasowej konfiguracji. Upewnij się, że jest zaznaczona opcja GRS domyślnie. Daje to pewność, że magazynu są automatycznie replikowane do centrum danych pomocniczych. Na przykład magazynu w zachodnie stany USA będą automatycznie replikowane do wschodnie stany USA.

3.  Konfigurowanie zasad tworzenia kopii zapasowej, a następnie wybierz maszynę Wirtualną z tego samego interfejsu użytkownika.

4.  Upewnij się, że zainstalowano agenta kopii zapasowej na maszynie Wirtualnej. Jeśli maszyna wirtualna została utworzona przy użyciu obrazu galerii Azure, agent kopii zapasowej już jest zainstalowany. W przeciwnym razie (Jeśli używasz niestandardowego obrazu), użyj instrukcji do [Zainstaluj agenta maszyny Wirtualnej na maszynie wirtualnej](../../backup/backup-azure-arm-vms-prepare.md#install-the-vm-agent-on-the-virtual-machine).

5.  Upewnij się, że maszyna wirtualna zezwala na połączenie sieciowe dla usługi tworzenia kopii zapasowej do funkcji. Wykonaj te instrukcje dla [połączeń sieciowych](../../backup/backup-azure-arm-vms-prepare.md#network-connectivity).

6.  Po wykonaniu powyższych czynności tworzenie kopii zapasowej zostanie uruchomiony w regularnych odstępach czasu określonych w zasadach tworzenia kopii zapasowej. W razie potrzeby możesz wyzwolić pierwszej kopii zapasowej ręcznie z pulpitem nawigacyjnym magazynu w portalu Azure.

Automatyzacja kopia zapasowa Azure za pomocą skryptów, można znaleźć na stronie [poleceń cmdlet programu PowerShell dla kopii zapasowej maszyny Wirtualnej](../../backup/backup-azure-vms-automation.md).

### <a name="steps-for-recovery"></a>Procedura odzyskiwania

Jeśli musisz naprawić lub ponownie skompiluj maszyny Wirtualnej, można przywrócić maszyny Wirtualnej z żadnym z punktów odzyskiwania kopii zapasowej w magazynie. Istnieje kilka różnych opcji do wykonania odzyskiwania:

1.  Można utworzyć nowej maszyny Wirtualnej jako punktu w czasie reprezentacji kopii zapasowej maszyny wirtualnej.

2.  Można przywrócić dyski, a następnie dostosować i skompiluj ponownie przywróconą maszyną Wirtualną przy użyciu szablonu maszyny wirtualnej. 

Zobacz instrukcje, aby [portal Azure używany do przywrócenia maszyn wirtualnych](../../backup/backup-azure-arm-restore-vms.md#restoring-a-vm-during-azure-datacenter-disaster). Dokument wyjaśniono również wykonania określonych kroków do przywrócenia kopii zapasowej maszyn wirtualnych do centrum danych sparowanego w centrum danych podstawowych za pomocą geograficznie nadmiarowego magazynu kopii zapasowych w przypadku awarii. W takim przypadku kopia zapasowa Azure korzysta z usługi obliczeniowe z regionu pomocniczego do tworzenia przywróconej maszyny wirtualnej.

Można również użyć programu PowerShell dla [przywracanie maszyny Wirtualnej](../../backup/backup-azure-vms-automation.md#restore-an-azure-vm) lub [tworzenia nowej maszyny Wirtualnej z przywrócić dysków](../../backup/backup-azure-vms-automation.md#create-a-vm-from-restored-disks).

## <a name="alternative-solution-consistent-snapshots"></a>Alternatywnych rozwiązań: Migawki spójne

Jeśli nie możesz korzystać z usługi Kopia zapasowa Azure, możesz wdrożyć własny mechanizm tworzenia kopii zapasowej przy użyciu migawek. Jest skomplikowane, aby utworzyć migawki spójne z dla wszystkich dysków używanych przez Maszynę wirtualną, a te migawki są następnie replikowane do innego regionu. Z tego powodu Azure bierze pod uwagę wykorzystanie lepszym rozwiązaniem niż tworzenia niestandardowych rozwiązań usługi Kopia zapasowa. Jeśli używasz magazynu RA-GRS/GRS dysków migawki są automatycznie replikowane do centrum danych w dodatkowej. Użycie magazynu LRS w przypadku dysków, musisz samodzielnie replikowane dane. Aby uzyskać więcej informacji, zobacz [kopia zapasowa Azure niezarządzane dysków maszyny Wirtualnej z migawkami przyrostowe](../../virtual-machines/windows/incremental-snapshots.md).

Migawka jest reprezentację obiektu w określonym punkcie w czasie. Migawki będą naliczane rozliczeń dla przyrostowych rozmiar danych go blokad. Aby uzyskać więcej informacji, zobacz [utworzenia migawki obiektu blob](../blobs/storage-blob-snapshots.md).

### <a name="creating-snapshots-while-the-vm-is-running"></a>Tworzenie migawek uruchomionej maszyny Wirtualnej

W dowolnym momencie można utworzyć migawkę, jeśli maszyna wirtualna jest uruchomiona, jest nadal dane przesyłane strumieniowo na dyskach, i migawki może zawierać częściowe operacje, które zostały w locie. Ponadto jeśli są zaangażowane kilka dysków, migawek różnych dysków może wystąpić w różnym czasie, co oznacza, że te migawki nie może być skoordynowany sposób. Jest to szczególnie kłopotliwe w sytuacji dla woluminów rozłożonych, którego pliki mogą zostać uszkodzone, jeśli trwa zmian podczas tworzenia kopii zapasowej.

Aby tego uniknąć, proces tworzenia kopii zapasowej musi implementować następujące czynności:

1.  Zablokuj wszystkie dyski

2.  Flush wszystkie oczekujące operacje zapisu

3.  Następnie [utworzenia migawki obiektu blob](../blobs/storage-blob-snapshots.md) dla wszystkich dysków

Niektóre aplikacje systemu Windows, takich jak SQL Server mechanizm skoordynowany sposób tworzenia kopii zapasowej za pomocą usługi VSS tworzenie kopii zapasowych spójnych z aplikacją. W systemie Linux można użyć narzędzia, takiego jak fsfreeze koordynacji dysków, co zapewnia spójne z plikami kopii zapasowych, ale nie migawki spójne z aplikacjami. Ten proces jest skomplikowane, więc i należy rozważyć użycie [kopia zapasowa Azure](../../backup/backup-azure-vms-introduction.md) lub rozwiązanie tworzenia kopii zapasowych innych firm, które już wdrożyć.

Proces powyżej spowoduje kolekcji skoordynowanego migawek dla wszystkich dysków maszyny Wirtualnej, reprezentujący widok w momencie określonej maszyny wirtualnej. To jest punkt przywracania kopii zapasowej dla maszyny Wirtualnej. Proces można powtarzać w zaplanowanych odstępach czasu, aby utworzyć okresowe kopie zapasowe. Wymienione poniżej, aby uzyskać instrukcje dotyczące [skopiuj kopie zapasowe do innego regionu](#copy-the-snapshots-to-another-region) do odzyskiwania po awarii.

### <a name="creating-snapshots-while-the-vm-is-offline"></a>Tworzenie migawek, podczas gdy maszyna wirtualna jest w trybie offline

Inną opcją utworzyć spójne tworzenie kopii zapasowych jest zamykanie maszyny Wirtualnej i tworzenie migawek blob każdego dysku. To jest łatwiejsze niż koordynujący migawki uruchomionej maszyny wirtualnej, ale wymaga to kilka minut przestoju. Dla tego procesu wykonaj następujące kroki:

1. Zamknij maszynę Wirtualną.

2. Utwórz migawkę każdej blob dysku VHD, który zajmuje tylko kilka sekund.

    Aby utworzyć migawkę, można użyć [programu PowerShell](storage-powershell-guide-full.md#how-to-manage-azure-blob-snapshots), [interfejsu API Rest magazynu Azure](https://msdn.microsoft.com/library/azure/ee691971.aspx), [interfejsu wiersza polecenia Azure](https://docs.microsoft.com/azure/xplat-cli-install), lub jeden z biblioteki klienta magazynu Azure, takich jak [ Biblioteka klienta usługi Storage dla platformy .NET](https://msdn.microsoft.com/library/azure/hh488361.aspx).

3. Uruchom maszynę Wirtualną, która kończy przestoju. Zwykle cały proces zostanie zakończony w ciągu kilku minut.

Ten proces zapewnia zbiór migawki spójne z dla wszystkich dysków, zapewniając punktu przywracania dla maszyny Wirtualnej. Wymienione poniżej czynności skopiować migawki do innego regionu do odzyskiwania po awarii.

### <a name="copy-the-snapshots-to-another-region"></a>Kopiowanie migawek do innego regionu

Tworzenie migawek wyłącznie nie może być wystarczające do odzyskiwania po awarii. Kopie zapasowe migawek również muszą być replikowane do innego regionu.

Jeśli używasz GRS lub RA-GRS dla dysków, a następnie migawki są automatycznie replikowane w regionie pomocniczym. Może istnieć kilka minut opóźnienie przed replikacji, a jeśli Centrum danych podstawowych przestanie działać, zanim migawki Zakończ replikacji, nie będzie dostęp do migawek w centrum danych w dodatkowej. Prawdopodobieństwo to jest mała.

> [!Note] 
> Tylko o dyski w ramach konta GRS lub RA-GRS nie chroni maszyny Wirtualnej po awarii. Należy również tworzenie migawek skoordynowanego albo użyć kopia zapasowa Azure. Jest to wymagane, aby odzyskać Maszynę wirtualną do stanu spójności.

Jeśli używasz LRS, należy skopiować migawki do innego konta magazynu, natychmiast po utworzeniu migawki. Element docelowy kopiowania może być konta magazynu LRS w innym regionie, co powoduje kopiowania w regionie zdalnego. Można także skopiować migawki do konta magazynu RA-GRS, w tym samym regionie. W takim przypadku migawki będą opóźnieniem replikowane do zdalnego regionie pomocniczym. Kopia zapasowa jest chronione przed awarii w lokacji głównej raz kopiowania i replikacji zostanie zakończone.

Aby skopiować wydajnie Twojej przyrostowe migawki do odzyskiwania po awarii, zapoznaj się z instrukcjami wyświetlanymi w [kopia zapasowa Azure niezarządzane dysków maszyny Wirtualnej z migawkami przyrostowe](../../virtual-machines/windows/incremental-snapshots.md).

![](./media/storage-backup-and-disaster-recovery-for-azure-iaas-disks/backup-and-disaster-recovery-for-azure-iaas-disks-2.png)   

### <a name="recovery-from-snapshots"></a>Odzyskiwanie z migawki

Aby pobrać migawki, skopiuj go do utworzyć nowego obiektu blob. Jeśli kopiujesz migawki z kontem podstawowym, można skopiować migawki za pośrednictwem do podstawowego obiektu blob migawki, w związku z tym przywracania dysku migawki; jest to nazywane podwyższania poziomu migawki. Jeśli kopiujesz migawki kopii zapasowej z pomocniczego konta (w przypadku RA-GRS), należy skopiować do podstawowego konta. Możesz skopiować migawki [przy użyciu programu PowerShell](storage-powershell-guide-full.md#how-to-copy-a-snapshot-of-a-blob) lub przy użyciu narzędzia AzCopy. Aby uzyskać więcej informacji, zobacz [Transfer danych za pomocą wiersza polecenia Azcopy](storage-use-azcopy.md).

W przypadku maszyn wirtualnych z wieloma dyskami należy skopiować wszystkie migawki, które są częścią tego samego punktu przywracania w skoordynowany sposób. Po skopiowaniu migawki zapisywalny obiekty BLOB dysków VHD, można użyć obiektów blob można odtworzyć maszyny Wirtualnej przy użyciu szablonu maszyny wirtualnej.

## <a name="other-options"></a>Inne opcje

### <a name="sql-server"></a>Oprogramowanie SQL Server

Program SQL Server uruchomiony na maszynie wirtualnej ma własną wbudowanych możliwości, aby utworzyć kopię zapasową bazy danych SQL Server do magazynu obiektów Blob platformy Azure lub udziału plików. W przypadku konta magazynu GRS lub RA-GRS, zgodnie z opisem wcześniej dostępne kopie zapasowe w centrum danych pomocniczego konta magazynu w przypadku awarii, z ograniczeniami. Aby uzyskać więcej informacji, zobacz [kopii zapasowej i przywracania dla programu SQL Server w usłudze Azure Virtual Machines](../../virtual-machines/windows/sql/virtual-machines-windows-sql-backup-recovery.md). Oprócz tworzenia kopii zapasowej i przywracania [programu SQL Server zawsze włączonych grup dostępności](../../virtual-machines/windows/sql/virtual-machines-windows-sql-high-availability-dr.md) można zachować replikach pomocniczych baz danych, aby znacznie skrócić czas odzyskiwania po awarii.

## <a name="other-considerations"></a>Inne zagadnienia

Ten artykuł ma omówiono sposób wykonania kopii zapasowej lub migawek maszyn wirtualnych i ich dyski, która obsługuje odzyskiwanie po awarii i sposobie ich użyć do odzyskania. Model usługi Azure Resource Manager wiele osób za pomocą szablonów do tworzenia ich maszyn wirtualnych i innych infrastruktury na platformie Azure. Szablon służy do tworzenia maszyny Wirtualnej, który ma taką samą konfigurację zawsze. Jeśli używasz niestandardowych obrazów do tworzenia maszyn wirtualnych, należy również upewnić się, że obrazy są chronione przy użyciu konta RA-GRS je przechowywać.

W rezultacie procesu tworzenia kopii zapasowej może być kombinacją dwie czynności:

1. Kopie zapasowe danych (dyski)
2. Wykonaj kopię zapasową konfiguracji (szablony, niestandardowe obrazy)

W zależności od wybranej opcji tworzenia kopii zapasowej może mieć do obsługi kopii zapasowych danych i konfiguracji lub usługi tworzenia kopii zapasowej może obsługiwać to wszystko dla Ciebie.

## <a name="appendix---understanding-the-impact-of-lrs-grs-and-ra-grs"></a>Dodatek - zrozumienie wpływu LRS, GRS i RA-GRS

Dla konta magazynu na platformie Azure, istnieją trzy typy nadmiarowość danych, które należy wziąć pod uwagę dotyczące odzyskiwania po awarii — magazyn lokalnie nadmiarowy (LRS), geograficznie nadmiarowego (GRS), lub odczytu z magazynu geograficznie nadmiarowego z dostępu (RA-GRS). 

Lokalnie magazyn geograficznie nadmiarowy (LRS) przechowuje trzy kopie danych w tym samym centrum danych. Podczas zapisywania danych, wszystkie trzy kopie są aktualizowane przed zwróceniem Powodzenie do wywołującego, dlatego wiadomo, że są one identyczne. Dysk jest zabezpieczony błędy lokalne, ponieważ jest on bardzo mało prawdopodobne, że wszystkie trzy kopie może występować w tym samym czasie. W przypadku LRS nie nie nadmiarowość geograficzna, więc dysk nie jest chroniony poważnej awarii, które mogą mieć wpływ na jednostkę Centrum lub magazynu danych.

Z GRS i RA-GRS trzy kopie danych są przechowywane w regionie podstawowym (wybrane przez użytkownika), a więcej trzy kopie danych są przechowywane w odpowiedni region pomocniczy (ustawione przez platformę Azure). Na przykład jeśli dane są przechowywane w zachodnie stany USA, dane będą replikowane do wschodnie stany USA. Jest to realizowane asynchronicznie, a istnieje małe opóźnienie między aktualizacji do serwera podstawowego i pomocniczego. Repliki dyski w lokacji dodatkowej są spójne na podstawie na dysku (z opóźnieniem), ale replik wielu aktywnych dysków mogą nie być zsynchronizowane **ze sobą**. Aby były spójne replik na wielu dyskach, potrzebne są migawki spójne.

Podstawowa różnica między GRS i RA-GRS to, że z RA-GRS, możesz przeczytać pomocniczej kopii w dowolnym momencie. Jeśli występuje problem, który renderuje dane w regionie podstawowym niedostępny, zespół Azure będzie wszelkich starań, aby przywrócić dostęp. Gdy podstawowej nie działa, jeśli masz RA-GRS włączone, można dostępu do danych w centrum danych w dodatkowej. W związku z tym jeśli planujesz do odczytu z repliki, gdy podstawowy jest niedostępny, następnie RA-GRS należy rozważyć.

Jeśli okaże się być istotne awarii zespół Azure może wyzwolić geograficznie trybu failover i zmień głównej wpisy DNS, aby wskazywał pomocniczego magazynu. W tym momencie w albo GRS lub RA-GRS włączone, ma dostęp do danych w regionie, które było pomocniczej. Innymi słowy Jeśli Twoje konto magazynu jest GRS i występuje problem, są dostępne magazynu pomocniczego tylko wtedy, gdy geograficznie trybu failover.

Aby uzyskać więcej informacji, zobacz [co robić w przypadku wystąpienia awarii usługi Azure Storage](storage-disaster-recovery-guidance.md). 

Należy pamiętać, że Microsoft kontroluje, czy do pracy awaryjnej. Tryb failover nie są kontrolowane na konto magazynu, w związku z tym nie zdecydowano poszczególnych odbiorców. Aby zaimplementować odzyskiwania po awarii dla określonego magazynu kont lub dysków maszyny wirtualnej, należy użyć metod opisanych wcześniej w tym artykule.
