---
title: "aaaInstall SAP HANA na SAP HANA na platformie Azure (wystąpienia duże) | Dokumentacja firmy Microsoft"
description: "Jak tooinstall SAP HANA na SAP HANA na platformie Azure (wystąpienia duże)."
services: virtual-machines-linux
documentationcenter: 
author: hermanndms
manager: timlt
editor: 
ms.service: virtual-machines-linux
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 12/01/2016
ms.author: rclaus
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: b2fe242270a1166cabcfae2f9249a8dd70ff3b93
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooinstall-and-configure-sap-hana-large-instances-on-azure"></a>Jak tooinstall i skonfigurować SAP HANA (duże wystąpień) w systemie Azure

Poniżej przedstawiono niektóre ważne definicje tooknow przed przeczytaniem tego przewodnika. W [omówienie SAP HANA (duże wystąpień) i architektury na platformie Azure](https://docs.microsoft.com/azure/virtual-machines/workloads/sap/hana-overview-architecture) wprowadzono dwóch różnych klas jednostek HANA dużych wystąpienie:

- S72, S72m S144, S144m, S192 i S192m, które firma Microsoft można znaleźć hello tooas I klasy typu jednostek magazynowych.
- S384, S384m S384xm, S576, S768 i S960, które firma Microsoft można znaleźć tooas Witaj "class typu II' SKU.

Specyfikator klasy Hello jest toobe będzie używane w całym hello HANA wystąpienia dużych tooeventually dokumentację można znaleźć możliwości toodifferent i wymagania odpowiednio jednostki SKU HANA dużych wystąpienia.

Inne definicje, często używanych są:
- **Sygnatura wystąpienia dużych:** stos infrastruktury sprzętu SAP HANA TDI certyfikowane i wystąpień SAP HANA toorun w obrębie platformy Azure w wersji dedykowanej.
- **SAP HANA na platformie Azure (duże wystąpienia):** oficjalną nazwą języka dla oferty hello Azure toorun HANA wystąpień w na SAP HANA TDI certyfikowanego sprzętu, które zostało wdrożone w dużych wystąpienia sygnatury w różnych regionach platformy Azure. Witaj powiązane termin **wystąpienia dużych HANA** jest skrót SAP HANA na platformie Azure (wystąpienia duże) i jest powszechnie używany ten przewodnik wdrożenia technicznego.


Hello instalacji programu SAP HANA odpowiada i działania hello można uruchomić po przekazaniem nowe SAP HANA na serwerze Azure (wystąpienia duże). I po ustanowieniu otrzymano hello łączności między Azure VNet(s) i hello HANA dużych wystąpienia jednostki. 

> [!Note]
> Dla poszczególnych zasad SAP hello instalacji programu SAP HANA musi zostać wykonana przez osoby certyfikowane tooperform instalacje SAP HANA. Osoba, przeszedł hello egzaminu certyfikowane skojarzyć technologii SAP, egzaminu certyfikacji SAP HANA instalację, lub integratora systemów SAP (SI).

Sprawdź ponownie, szczególnie w przypadku planowania tooinstall HANA 2.0 [&#2235581; SAP Obsługa Uwaga - SAP HANA: systemy operacyjne obsługiwane](https://launchpad.support.sap.com/#/notes/2235581/E) w kolejności toomake się tym hello jest obsługiwana przez system operacyjny z hello SAP HANA wersji należy zadecydować tooinstall. Okazuje się, że hello obsługiwany system operacyjny HANA 2.0 jest bardziej ograniczony hello systemu operacyjnego, obsługiwany HANA 1.0. 

## <a name="first-steps-after-receiving-hello-hana-large-instance-units"></a>Pierwsze kroki po otrzymaniu hello HANA dużych wystąpienia jednostki

**Pierwszy krok** od momentu odebrania hello wystąpienia dużych HANA i ustaleniu wystąpień toohello dostępu i połączeń, jest tooregister hello systemu operacyjnego wystąpienia hello u swojego dostawcy systemu operacyjnego. Ten krok obejmuje rejestrowanie system operacyjny SUSE Linux w wystąpieniu SMT SUSE, wymagającym toohave wdrożone na maszynie wirtualnej na platformie Azure. Witaj HANA dużych wystąpienia jednostki można połączyć toothis SMT wystąpienia (patrz niżej w tej dokumentacji). System operacyjny RedHat musi toobe zarejestrowany hello Red Hat subskrypcji Menedżera, należy tooconnect do lub. Zobacz także uwagi w tym [dokumentu](https://docs.microsoft.com/azure/virtual-machines/linux/sap-hana-overview-architecture?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json). Ten krok jest także niezbędne toobe toopatch stanie hello systemu operacyjnego. Zadanie, które jest odpowiedzialny za hello powitania klienta. Aby uzyskać SUSE, Znajdź tooinstall dokumentacji i skonfiguruj SMT [tutaj](https://www.suse.com/documentation/sles-12/book_smt/data/smt_installation.html).

**W drugim kroku** jest toocheck nowe poprawki i poprawki hello określonego systemu operacyjnego/wersji. Sprawdź, czy poziom poprawki hello hello wystąpienia dużych HANA na powitania najnowszy stan. W oparciu o czas na obrazu systemu operacyjnego poprawki/wersje i zmiany toohello przez Microsoft można wdrożyć, może być przypadki, w którym hello najnowsze poprawki nie może być włączony. Stąd jest obowiązkowy krok po podjęciu przez jednostkę wystąpienia dużych HANA toocheck czy poprawki dotyczące zabezpieczeń, funkcji, dostępności i wydajności zostały wydane w tym samym czasie przez hello określonego dostawcy systemu Linux i wymagają toobe zastosowane.

**Trzeci krok** jest istotne uwagi SAP toocheck limit hello instalowania i konfigurowania na powitania określonych wersji systemu operacyjnego wersji/SAP HANA. Powodu toochanging zalecenia lub zmiany tooSAP notatki lub konfiguracje, które są zależne od instalacji poszczególnych scenariuszy Microsoft nie zawsze będą mogli toohave jednostkę wystąpienia dużych HANA skonfigurowane dokładnie. Dlatego jest niezbędne do klientów, tooread hello uwagi SAP pokrewne tooSAP HANA na Twoje dokładnej wersji systemu Linux. Również Sprawdź konfiguracje hello hello systemu operacyjnego/wersji niezbędne i zastosować ustawienia konfiguracji hello w przypadku, gdy nie jest jeszcze wykonane.

W określonej hello wyboru następujące parametry i ostatecznie dostosowana do:

- NET.Core.rmem_max = 16777216
- NET.Core.wmem_max = 16777216
- NET.Core.rmem_default = 16777216
- NET.Core.wmem_default = 16777216
- NET.Core.optmem_max = 16777216
- NET.IPv4.tcp_rmem = 65536 16777216 16777216
- NET.IPv4.tcp_wmem = 65536 16777216 16777216

Począwszy od SLES12 z dodatkiem SP1 i RHEL 7.2, te należy ustawić parametry w pliku konfiguracji w katalogu /etc/sysctl.d hello. Na przykład można utworzyć plik konfiguracji o nazwie hello 91-NetApp-HANA.conf. W starszych wersjach SLES i RHEL te parametry muszą być in/etc/sysctl.conf zestawu.

Dla wszystkich RHEL zwalnia, a począwszy od SLES12 hello 
- sunrpc.tcp_slot_table_entries = 128

Parametr musi być ustawiony in/etc/modprobe.d/sunrpc-local.conf. Jeśli hello plik nie istnieje, należy go najpierw utworzyć przez dodanie hello wejścia: 
- Opcje sunrpc tcp_max_slot_table_entries = 128

**Czwarty krok** jest czas systemowy hello toocheck HANA dużych wystąpienia jednostki. wystąpienia Hello zostały wdrożone za pomocą reprezentować lokalizację hello Witaj Witaj region platformy Azure, HANA dużych sygnatura wystąpienia jest umieszczony w strefy czasowej systemu. Jesteś czas systemowy hello wolnego toochange lub strefy czasowej wystąpień hello, którego jesteś właścicielem. Dzięki temu i kolejność więcej wystąpień w dzierżawie, można go przygotować konieczność strefy czasowej hello tooadapt hello nowo dostarczyć wystąpień. Operacje firmy Microsoft mają nie wgląd w strefie czasowej systemu hello się skonfigurowanie wystąpieniami powitania po przekazanie hello. Dlatego nowo wdrożonym wystąpień może nie być ustawiona w hello sam strefy czasowej jako hello jedną zmieniony na. W związku z tym go odpowiada jako toocheck klienta i w razie potrzeby dostosować strefy czasowej hello wystąpień: hello przekazywany. 

**Piąty krok** jest toocheck etc/hosts. Jak uzyskać przekazywany bloków hello, mają one różne adresy IP przypisane do różnych celów (zobacz następną sekcję). Sprawdź plik etc/hosts hello. W przypadkach, gdy jednostki są dodawane do istniejącej dzierżawy nie powinien toohave itp/hostów hello nowo wdrożonych systemów obsługiwane poprawnie z adresami IP hello wcześniej dostarczonego systemów. Dlatego jest w przypadku jako klienta toocheck hello poprawne ustawienia, czy nowo wdrożone wystąpienie mogą współpracować i rozpoznawania nazw hello jednostek wcześniej wdrożonej w dzierżawie. 

## <a name="networking"></a>Sieć
Przyjęto założenie, że zostały wykonane hello zalecenia w projektowaniu sieciom wirtualnym platformy Azure i łączenia tych sieci wirtualnych toohello HANA dużych wystąpień, zgodnie z opisem w tych dokumentach:

- [Architektura na platformie Azure i SAP HANA (duże wystąpienia) — omówienie](https://docs.microsoft.com/azure/virtual-machines/workloads/sap/hana-overview-architecture)
- [Infrastruktura SAP HANA (duże wystąpień) i łączność na platformie Azure](hana-overview-infrastructure-connectivity.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

Brak niektórych szczegółów warto toomention dotyczących sieci hello hello jednej jednostki. Każda jednostka HANA dużych wystąpienia jest dostarczany z dwóch lub trzech adresów IP, które są przypisane tootwo lub trzech portów kart hello jednostki. Trzy adresy IP są używane w konfiguracji skalowania w poziomie HANA i hello scenariusz HANA replikacji systemu. Jeden z adresów IP hello przypisane toohello kart jednostki hello jest poza hello puli adresów IP serwera, który został opisany w hello [omówienie SAP HANA (duże wystąpienia) i architektury na platformie Azure](https://docs.microsoft.com/azure/virtual-machines/workloads/sap/hana-overview-architecture).

powinna wyglądać Hello dystrybucji dla jednostek o dwa adresy IP:

- eth0.xx powinny mieć przypisanego adresu IP spoza hello czy przesłane tooMicrosoft zakres adresów puli adresów IP serwera. Ten adres IP są używane do przechowywania w Hosts hello systemu operacyjnego.
- eth1.xx powinny mieć przypisanego adresu IP używanego do komunikacji tooNFS. W związku z tym, czy te adresy **nie** muszą toobe utrzymywane w itp/hosty w kolejności tooallow wystąpienia tooinstance ruchu w ramach dzierżawy hello.

W przypadku wdrażania replikacji systemu HANA lub HANA skalowalnych w poziomie Konfiguracja bloku o dwa adresy IP nie jest odpowiedni. Jeśli po dwa adresy IP tylko i pożądane toodeploy takiej konfiguracji, skontaktuj się z SAP HANA na tooget zarządzania usługą Azure innej adresów IP w innej sieci VLAN przypisane. Wystąpienia dużych HANA w przypadku urządzeń mających trzy adresy IP przypisane do trzech portów kart hello użycia mają zastosowanie następujące reguły:

- eth0.xx powinny mieć przypisanego adresu IP spoza hello czy przesłane tooMicrosoft zakres adresów puli adresów IP serwera. Dlatego ten adres IP nie stosuje się do przechowywania w Hosts hello systemu operacyjnego.
- eth1.xx powinny mieć przypisanego adresu IP używanego do przechowywania tooNFS komunikacji. Dlatego adresów tego typu nie powinna być utrzymywana w etc/hosts.
- eth2.xx powinny być przechowywane w itp/hostów do komunikacji między różnymi wystąpieniami hello wyłącznie używane toobe. Te adresy również będą hello adresy IP, które wymagają toobe utrzymywane w konfiguracjach HANA skalowalnego w poziomie jako adresy IP, które używa HANA hello między węzłami konfiguracji.



## <a name="storage"></a>Magazyn

Witaj układu magazynu dla SAP HANA na platformie Azure (wystąpienia duże) jest konfigurowana przy SAP HANA na zarządzania usługą Azure za pośrednictwem SAP zalecane zasady, zgodnie z opisem w [SAP HANA przestrzeni dyskowej jest potrzebne](http://go.sap.com/documents/2015/03/74cdb554-5a7c-0010-82c7-eda71af511fa.html) oficjalny dokument. Witaj nierównej rozmiarów woluminów różnych hello z hello różnych SKU HANA dużych wystąpień pobrano udokumentowane w [omówienie SAP HANA (duże wystąpienia) i architektury na platformie Azure](hana-overview-architecture.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

konwencje nazewnictwa Hello woluminów magazynu hello są wymienione w hello w poniższej tabeli:

| Użycie magazynu | Nazwa instalacji | Nazwa woluminu | 
| --- | --- | ---|
| HANA danych | /Hana/Data/SID/mnt0000<m> | Magazyn IP: / hana_data_SID_mnt00001_tenant_vol |
| HANA dziennika | /Hana/log/SID/mnt0000<m> | Magazyn IP: / hana_log_SID_mnt00001_tenant_vol |
| Kopia zapasowa dziennika HANA | /Hana/log/Backups | Magazyn IP: / hana_log_backups_SID_mnt00001_tenant_vol |
| HANA udostępnionych | /Hana/Shared/SID | Magazyn IP: / hana_shared_SID_mnt00001_tenant_vol/udostępnionych |
| usr/sap | /usr/SAP/SID | Magazyn IP: / hana_shared_SID_mnt00001_tenant_vol/usr_sap |

Gdzie SID = hello HANA instance ID systemu 

I dzierżawcy = wewnętrzny wyliczenie operacje podczas wdrażania dzierżawcy.

Jak widać, udostępnianie HANA udostępnionego i usr/sap hello na tym samym woluminie. nomenklatura Hello hello punkty instalacji obejmują hello identyfikator systemu hello HANA wystąpienia, a także numer instalacji hello. W przypadku dużych wdrożeń jest tylko jeden instalacji, takich jak mnt00001. We wdrożeniu skalowalnego w poziomie można zobaczyć tyle instalacji, należy mieć węzłów procesu roboczego i wzorzec. Hello środowiska skalowalnego w poziomie, danych dziennika woluminach kopii zapasowej dziennika są węzła tooeach dołączonych i udostępnionych w hello skalowania konfiguracji. W przypadku konfiguracji uruchamianie wielu wystąpień SAP inny zestaw woluminów jest utworzony i dołączone toohello HAN dużych wystąpienia jednostki.

Przeczytaj dokument hello i Szukaj jednostki HANA dużych wystąpienia, można zrealizować jednostki hello pochodzić HANA/danych z woluminu dysku zamiast atrakcyjne i że mamy woluminu HANA / / kopii zapasowej dziennika. Przyczyna Hello Dlaczego możemy o rozmiarze hello HANA/danych tak duża, to czy hello magazynu migawek, które są oferowane dla klientów w przypadku korzystania hello na tym samym woluminie dysku. Oznacza to hello więcej magazynu migawek, które należy wykonać, powitalne więcej miejsca jest używane przez migawek w woluminach przydzielonych magazynu. Witaj HANA / / kopii zapasowej dziennika wolumin jest nie myśl toobe hello tooput kopie zapasowe bazy danych w. Jest rozmiarze toobe używane jako wolumin kopii zapasowej dla hello kopie zapasowe dziennika transakcji HANA. W przyszłych wersji hello magazynu migawek migawki częste samoobsługowe, firma Microsoft będzie obowiązywać tego więcej toohave określonego woluminu. I z tym częstsze lokacja odzyskiwania po awarii toohello replikacje Jeśli wymagasz toooption w funkcji odzyskiwania po awarii hello hello wystąpienia dużych HANA infrastruktury. Zobacz szczegóły w [SAP HANA (duże wystąpień) wysokiej dostępności i odzyskiwania po awarii na platformie Azure](hana-overview-high-availability-disaster-recovery.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) 

Dodatkowo podana toohello magazynu, możesz kupić dodatkowej pojemności w przyrostach 1 TB. Ten dodatkowy magazyn może zostać dodana jako nowe woluminy tooa HANA dużych wystąpień.

Podczas dołączania z SAP HANA na zarządzanie usługami Azure, powitania klienta Określa identyfikator użytkownika (UID) i identyfikator grupy (GID) dla grupy użytkowników i sapsys sidadm hello (przykład: 1000,500) jest, że podczas instalacji systemu SAP HANA hello, te same wartości są używane. Można dowolnie toodeploy wiele wystąpień HANA jednostki, należy pobrać wiele zestawów woluminów (jeden zestaw dla każdego wystąpienia). W związku z tym w czasie wdrażania należy toodefine:

- Witaj SID hello różnymi wystąpieniami HANA (sidadm pochodzi od niego).
- Rozmiary pamięci hello różnymi wystąpieniami HANA. Ponieważ hello rozmiar pamięci na wystąpień definiuje hello rozmiaru woluminów hello w każdym zestawie poszczególnych woluminów.

Na podstawie zaleceń dostawcy magazynu hello następujące opcje instalacji są skonfigurowane dla wszystkich zainstalowanych woluminów (z wykluczeniem rozruchu LUN):

- NFS rw ver = 4, twardych, timeo = 600, rsize = 1048576, wsize = 1048576, grupa, noatime, zablokować 0 0

Te instalacji punkty są skonfigurowane w/etc/fstab, jak pokazano na powitania po grafiki:

![fstab zainstalowane woluminy w jednostce HANA dużych wystąpienia](./media/hana-installation/image1_fstab.PNG)

dane wyjściowe Hello hello polecenia df -h w jednostce S72m HANA dużych wystąpienia wyglądałyby tak jak:

![fstab zainstalowane woluminy w jednostce HANA dużych wystąpienia](./media/hana-installation/image2_df_output.PNG)


Hello kontrolera magazynu i węzłów w hello dużych wystąpienia sygnatury są synchronizowane tooNTP serwerów. Tobie synchronizowanie hello SAP HANA jednostek Azure (wystąpienia duże) i maszyny wirtualne Azure względem serwera NTP nie powinno być nie sytuacji odejście długiego czasu między hello infrastruktury i jednostek obliczeń hello Azure lub duże wystąpienia sygnatury.

W kolejności toooptimize SAP HANA toohello magazynu używane poniżej należy również ustawić następujące parametry konfiguracji SAP HANA hello:

- max_parallel_io_requests 128
- async_read_submit na
- async_write_submit_active na
- wszystkie async_write_submit_blocks
 
Wersje programu SAP HANA 1.0 się tooSPS12, te parametry można ustawić podczas instalacji hello bazy danych SAP HANA hello, zgodnie z opisem w [SAP Uwaga #2267798 - konfiguracji hello bazy danych SAP HANA](https://launchpad.support.sap.com/#/notes/2267798)

Także można skonfigurować parametrów powitania po instalacji bazy danych SAP HANA hello przy użyciu hello hdbparam framework. 

SAP HANA 2.0 z hello hdbparam framework jest przestarzała. W związku z tym hello należy ustawić parametry za pomocą polecenia SQL. Aby uzyskać więcej informacji, zobacz [&#2399079; Uwaga SAP: eliminacji hdbparam 2 HANA](https://launchpad.support.sap.com/#/notes/2399079).


## <a name="operating-system"></a>System operacyjny

Obszar wymiany z hello dostarczony obraz systemu operacyjnego jest ustawiona zgodnie z toohello GB too2 [&#1999997; SAP Obsługa Uwaga — często zadawane pytania: SAP HANA pamięci](https://launchpad.support.sap.com/#/notes/1999997/E). Wszystkie różne ustawienia żądaną wymaga toobe ustawione przez klienta.

[SUSE Linux Enterprise Server 12 SP1 dla programu SAP aplikacji](https://www.suse.com/products/sles-for-sap/hana) jest hello dystrybucji systemu Linux zainstalowane dla SAP HANA na platformie Azure (wystąpienia duże). Tej konkretnej dystrybucji zapewnia możliwości specyficznych dla programu SAP &quot;fabrycznej hello&quot; (w tym systemie SAP SLES skutecznie wstępnie ustawionymi parametrów).

Zobacz [zasobów biblioteki/oficjalne dokumenty](https://www.suse.com/products/sles-for-sap/resource-library#white-papers) w witrynie sieci Web hello SUSE i [SAP w systemie SUSE](https://wiki.scn.sap.com/wiki/display/ATopics/SAP+on+SUSE) na hello SAP społeczności sieci (SCN) toodeploying SAP HANA na SLES (takie jak hello konfiguracji związanych z kilku przydatne zasoby o wysokiej dostępności, operacje określonych tooSAP wzmocnienie zabezpieczeń i inne).

Dodatkowe i przydatne SAP SUSE związane z łącza:

- [SAP HANA w systemie SUSE Linux lokacji](https://wiki.scn.sap.com/wiki/display/ATopics/SAP+on+SUSE)
- [Najlepsze praktyki dla SAP: umieścić w kolejce replikacji — SAP NetWeaver w systemie SUSE Linux Enterprise 12](https://www.suse.com/docrepcontent/container.jsp?containerId=9113).
- [ClamSAP — ochrony przed wirusami SLES dla SAP](http://scn.sap.com/community/linux/blog/2014/04/14/clamsap--suse-linux-enterprise-server-integrates-virus-protection-for-sap) (w tym SLES 12 SAP aplikacji).

SAP tooimplementing odpowiednie informacje pomocy technicznej SAP HANA na SLES 12:

- [Uwaga Obsługa SAP #1944799 — SAP HANA wskazówki dotyczące instalacji systemu operacyjnego SLES](http://go.sap.com/documents/2016/05/e8705aae-717c-0010-82c7-eda71af511fa.html).
- [Uwaga Obsługa SAP #2205917 — SAP HANA DB zalecane ustawienia systemu operacyjnego dla SLES 12 aplikacje SAP](https://launchpad.support.sap.com/#/notes/2205917/E).
- [Uwaga Obsługa SAP #1984787 — SUSE Linux Enterprise Server 12: Informacje o instalacji](https://launchpad.support.sap.com/#/notes/1984787).
- [Uwaga Obsługa SAP #171356 — oprogramowania SAP w systemie Linux: ogólne informacje](https://launchpad.support.sap.com/#/notes/1984787).
- [Uwaga Obsługa SAP #1391070 — rozwiązania Linux UUID](https://launchpad.support.sap.com/#/notes/1391070).

[Red Hat Enterprise Linux dla programu SAP HANA](https://www.redhat.com/en/resources/red-hat-enterprise-linux-sap-hana) jest inną ofertę do uruchamiania w wystąpieniach dużych HANA SAP HANA. Dostępne są wersje RHEL 6.7 i 7.2. 

Dodatkowe i przydatne SAP Red Hat łączy pokrewnych:
- [SAP HANA na Red Hat Linux lokacji](https://wiki.scn.sap.com/wiki/display/ATopics/SAP+on+Red+Hat).

SAP tooimplementing odpowiednie informacje pomocy technicznej SAP HANA na Red Hat:

- [Uwaga Obsługa SAP &#2009879; - SAP HANA wytyczne dotyczące systemu operacyjnego systemu Red Hat Enterprise Linux (RHEL)](https://launchpad.support.sap.com/#/notes/2009879/E).
- [Uwaga Obsługa SAP &#2292690; - SAP HANA DB: Ustawienia zalecane systemu operacyjnego dla systemów RHEL 7](https://launchpad.support.sap.com/#/notes/2292690).
- [Uwaga Obsługa SAP &#2247020; - SAP HANA DB: OS zalecane ustawienia dla RHEL 6.7](https://launchpad.support.sap.com/#/notes/2247020).
- [Uwaga Obsługa SAP #1391070 — rozwiązania Linux UUID](https://launchpad.support.sap.com/#/notes/1391070).
- [Uwaga Obsługa SAP #2228351 - Linux: SAP HANA bazy danych SPS 11 poprawki 110 (lub nowszej) na RHEL 6 lub SLES 11](https://launchpad.support.sap.com/#/notes/2228351).
- [Uwaga Obsługa SAP #2397039 — często zadawane pytania: SAP na RHEL](https://launchpad.support.sap.com/#/notes/2397039).
- [Uwaga Obsługa SAP &#1496410; - Red Hat Enterprise Linux 6.x: instalacji i uaktualniania](https://launchpad.support.sap.com/#/notes/1496410).
- [Uwaga Obsługa SAP &#2002167; - Red Hat Enterprise Linux 7.x: instalacji i uaktualniania](https://launchpad.support.sap.com/#/notes/2002167).

## <a name="time-synchronization"></a>Czas synchronizacji

W przypadku hello różne składniki wchodzące w skład hello systemu SAP poufnych na różnice czasu jest oparty na powitania architektura SAP NetWeaver aplikacje SAP. Krótki ABAP SAP zrzuty z tytułu błąd hello ZDATE\_DUŻY\_czasu\_Różnicowy są prawdopodobnie znany, jak te zrzuty krótkich wyglądała hello czas systemowy na różnych serwerach lub maszyn wirtualnych przemieszcza się zbyt daleko od siebie.

SAP HANA na platformie Azure (duże wystąpień) w Azure &#39; synchronizację czasu t zastosować toohello obliczeniowe jednostki w hello dużych wystąpienia sygnatury. Synchronizacji nie ma zastosowania do uruchamiania aplikacji SAP w macierzysty maszynach wirtualnych platformy Azure, jak Azure zapewnia system &#39; s czasu jest odpowiednio zsynchronizowane. W związku z tym oddzielny czasu można skonfigurować serwera, które mogą być używane przez serwery aplikacji SAP uruchomione na maszynach wirtualnych platformy Azure i hello SAP HANA bazy danych uruchomionych w wystąpieniach dużych HANA wystąpień. Witaj infrastruktury magazynu w dużych wystąpienia sygnatury jest czas synchronizowane z serwerami NTP.

## <a name="setting-up-smt-server-for-suse-linux"></a>Konfigurowanie serwera SMT SUSE Linux
SAP HANA dużych wystąpień nie ma toohello bezpośrednie połączenie internetowe. Dlatego nie jest dość proste tooregister jednostki z dostawcą systemu operacyjnego hello i toodownload i stosowania poprawek. W przypadku hello SUSE Linux jedno rozwiązanie może być tooset SMT serwera w maszynie Wirtualnej platformy Azure. Witaj maszyny Wirtualnej Azure powinna toobe hostowanych w sieci wirtualnej platformy Azure, który jest połączony toohello wystąpienia dużych HANA. Z takiego serwera SMT hello HANA dużych wystąpienia jednostki można zarejestrować i pobrania poprawek. 

SUSE zawiera większego przewodnika po po ich [subskrypcji narzędzia do zarządzania z dodatkiem SP2 SLES 12](https://www.suse.com/documentation/sles-12/pdfdoc/book_smt/book_smt.pdf). 

Jako warunek wstępny dla instalacji powitania serwera SMT spełniającego zadań hello HANA dużych wystąpienia musisz:

- Sieć wirtualną platformy Azure będący połączonych toohello HANA dużych wystąpienia ER obwodu.
- Konto SUSE, który jest skojarzony z organizacji. Natomiast hello organizacji potrzebny toohave niektórych ważnej subskrypcji SUSE.

### <a name="installation-of-smt-server-on-azure-vm"></a>Instalacja serwera SMT na maszynie Wirtualnej Azure

W tym kroku należy zainstalować serwer SMT hello w maszynie Wirtualnej platformy Azure. pierwszym środkiem Hello jest toolog w toohello [SUSE Centrum klientów](https://scc.suse.com/)

Jako użytkownik jest zalogowany, przejdź tooOrganization--> poświadczeń organizacji. Witaj poświadczenia, które są niezbędne tooset hello SMT serwera powinien znajdować się w tej sekcji.

trzeci krok Hello jest tooinstall maszyny Wirtualnej systemu Linux SUSE w hello sieci wirtualnej platformy Azure. Witaj toodeploy maszyny Wirtualnej, zająć obraz z dodatkiem SP2 SLES 12 galerii Azure. W procesie wdrażania hello nie definiuje nazwy DNS i nie należy używać statycznych adresów IP, jak pokazano w tym zrzucie ekranu.

![wdrożenia maszyny wirtualnej dla serwera SMT](./media/hana-installation/image3_vm_deployment.png)

Witaj wdrożonej maszyny Wirtualnej było mniejsze maszyny Wirtualnej i uzyskano hello wewnętrznego adresu IP w sieci wirtualnej platformy Azure z 10.34.1.4 hello. Nazwa hello wirtualna miała smtserver. Po zakończeniu instalacji hello zaznaczono hello łączności toohello HANA dużych wystąpienia jednostki. Zależy sposób organizowania rozpoznawania nazw może być konieczne rozpoznawania tooconfigure hello HANA dużych wystąpienia jednostek w itp/hosty hello maszyny Wirtualnej platformy Azure. Dodaj dodatkowy dysk toohello maszynę Wirtualną, która będzie toobe używanych toohold hello poprawki. samego dysku rozruchowego Hello może być za mały. W przypadku hello przedstawiona dysku hello otrzymano zainstalowanego za/srv/www/htdocs pokazane na powitania po zrzut ekranu. Dysk 100 GB powinny wystarczyć.

![wdrożenia maszyny wirtualnej dla serwera SMT](./media/hana-installation/image4_additional_disk_on_smtserver.PNG)

Zaloguj się za toohello HANA wystąpienia dużych jednostek, obsługa/etc/hosts i sprawdź, czy można uzyskać dostęp do maszyny Wirtualnej platformy Azure, który ma toorun hello SMT serwera za pośrednictwem sieci hello hello.

Po ten test zakończy się pomyślnie, należy toolog w toohello maszyny Wirtualnej platformy Azure, które powinno być ono uruchomione hello SMT serwera. Jeśli używasz programu putty toolog w toohello maszyny Wirtualnej, należy tooexecute ta sekwencja poleceń w oknie bash:

```
cd ~
echo "export NCURSES_NO_UTF8_ACS=1" >> .bashrc
```

Po wykonaniu tych poleceń, uruchom ponownie ustawienia hello tooactivate bash. Następnie uruchom YAST.

W YAST Przejdź tooSoftware konserwacji i wyszukaj smt. Wybierz smt, który automatycznie zmienia tooyast2 smt, jak pokazano poniżej

![SMT w yast](./media/hana-installation/image5_smt_in_yast.PNG)


Zaakceptuj wybór hello do instalacji na powitania smtserver. Po zainstalowaniu go toohello SMT serwera konfiguracji, a następnie wprowadź poświadczenia organizacyjnej hello z hello Centrum klientów SUSE został wcześniej pobrany. Również wprowadzić nazwy hosta z maszyny Wirtualnej platformy Azure jako hello SMT adres URL serwera. W tej prezentacji było https://smtserver wyświetlaną w hello dalej grafiki.

![Konfiguracja serwera SMT](./media/hana-installation/image6_configuration_of_smtserver1.png)

Następnym krokiem jest konieczne tootest czy działa Centrum hello połączenia toohello SUSE klientów. Jak widać w powitania po grafiki, w przypadku pokaz hello rozwiązało problemu.

![Test połączenia Centrum klientów tooSUSE](./media/hana-installation/image7_test_connect.png)

Raz hello SMT Instalator zostanie uruchomiony, należy tooprovide hasła bazy danych. Ponieważ chodzi o nowej instalacji, należy toodefine to hasło, jak pokazano w hello dalej grafiki.

![Określić hasło dla bazy danych](./media/hana-installation/image8_define_db_passwd.PNG)

Hello interakcji dalej posiadanego jest tworzona pobiera certyfikat. Przejdź za pomocą okna dialogowego hello, jak pokazano w następnym i krok hello powinno być kontynuowane.

![Utworzenie certyfikatu serwera SMT](./media/hana-installation/image9_certificate_creation.PNG)

Może istnieć kilka minut spędzony w kroku hello "Uruchom sprawdzanie synchronizacji" na końcu hello hello konfiguracji. Po hello instalacji i konfiguracji serwera SMT hello, należy odnaleźć hello katalogu repozytorium pod hello instalacji punktu /srv/www/htdocs/plus niektórych podkatalogów w repozytorium. 

Uruchom ponownie serwer SMT hello i jej powiązane usługi przy użyciu następujących poleceń.

```
rcsmt restart
systemctl restart smt.service
systemctl restart apache2
```

### <a name="download-of-packages-onto-smt-server"></a>Pobierz pakietów na serwerze SMT

Po wszystkich hello ponownego uruchomienia usług, wybierz hello odpowiednie pakiety zarządzania SMT przy użyciu Yast. Wybór pakietów Hello zależy od obrazu systemu operacyjnego hello hello HANA dużych wystąpienia serwera nie powitalne SLES wersji lub wersji serwera SMT hello uruchomionej maszyny Wirtualnej hello. Poniżej przedstawiono przykład ekranu wyboru hello.

![Wybierz pakiety](./media/hana-installation/image10_select_packages.PNG)

Po zakończeniu wybór pakietów hello należy toostart hello początkową kopię hello Wybierz pakiety toohello SMT serwera skonfigurowanego. Ta kopia zostanie wywołany w powłoce hello przy użyciu hello polecenia smt dublowania w sposób przedstawiony poniżej


![Pobierz pakiety tooSMT serwera](./media/hana-installation/image11_download_packages.PNG)

Jak widać powyżej, pakietów hello powinien pobrać kopiowane do katalogów hello utworzone na podstawie hello instalacji punktu /srv/www/htdocs. Ten proces może trochę potrwać. Zależne od liczby pakietów, należy wybrać, może potrwać tooone godzinę lub dłużej.
Jako zakończenie tego procesu, należy toomove toohello SMT instalacji. 

### <a name="set-up-hello-smt-client-on-hana-large-instance-units"></a>Konfigurowanie klienta SMT hello na wystąpienie dużych HANA jednostki

w takim przypadku Hello klientów są hello HANA dużych wystąpienia jednostki. Konfiguracja serwera SMT Hello kopiowane hello clientSetup4SMT.sh skryptu do hello maszyny Wirtualnej platformy Azure. Skopiuj tego skryptu, za pośrednictwem toohello jednostki wystąpienia dużych HANA tooconnect tooyour SMT serwer. Uruchom skrypt hello z opcją -h hello i nadaj mu jako nazwa parametru hello SMT serwera. W tym smtserver przykład.

![Konfigurowanie klienta SMT](./media/hana-installation/image12_configure_client.PNG)

Może to być scenariusz, w którym hello obciążenia hello certyfikatu z serwera hello przez powitania klienta zakończyło się pomyślnie, ale hello rejestracja nie powiodła się, jak pokazano poniżej.

![Rejestracja klienta nie powiedzie się.](./media/hana-installation/image13_registration_failed.PNG)

Jeśli rejestracja hello nie powiodła się, przeczytaj [SUSE obsługuje dokumentu](https://www.suse.com/de-de/support/kb/doc/?id=7006024) i wykonywanie hello opisane istnieje.

> [!IMPORTANT] 
> Jako nazwę serwera należy tooprovide nazwę hello hello maszyny Wirtualnej, w tej sprawy smtserver, bez hello pełną nazwę domeny. Po prostu hello maszyny Wirtualnej nazwy działania. 

Po zostały wykonane następujące kroki, należy hello tooexecute następujące polecenia na powitania HANA dużych wystąpienia jednostki

```
SUSEConnect –cleanup
```

> [!Note] 
> Nasze testy zawsze było toowait kilka minut po wykonaniu tego kroku. Witaj clientSetup4SMT.sh natychmiastowego wykonania po hello działania naprawcze opisanego w hello artykułu SUSE zakończył się z wiadomości powitania certyfikatu nie jest prawidłowym jeszcze. Oczekiwanie na 5 – 10 minut zazwyczaj i wykonywania clientSetup4SMT.sh zostało zakończone w konfiguracji klienta powiodło się.

Wystąpił problem hello, który potrzebne toofix oparte na powitania kroki hello SUSE artykułu, należy najpierw clientSetup4SMT.sh toorestart w jednostce wystąpienia dużych HANA hello ponownie. Teraz go powinna zakończyć się pomyślnie, jak pokazano poniżej.

![Rejestracja klienta powiodło się.](./media/hana-installation/image14_finish_client_config.PNG)

Ten krok należy skonfigurować powitania klienta SMT hello HANA dużych wystąpienia jednostki tooconnect przed hello SMT serwera została zainstalowana w hello maszyny Wirtualnej platformy Azure. Teraz można podjąć "zypper się" lub "zypper w" tooinstall systemu operacyjnego poprawki wystąpień dużych tooHANA lub zainstalować dodatkowe pakiety. Przyjmuje się, że tylko ci poprawki pobrane przed na serwerze SMT hello.


## <a name="example-of-an-sap-hana-installation-on-hana-large-instances"></a>Przykład instalacji SAP HANA na HANA dużych wystąpień
W tej części przedstawiono sposób tooinstall SAP HANA HANA dużych wystąpienia jednostki. Stan początkowy Hello będziemy mieć następującą postać:

- Podane Microsoft wszystkich toodeploy danych hello można instancji dużych SAP HANA.
- Hello SAP HANA dużych wystąpienia jest otrzymanych od firmy Microsoft.
- Możesz utworzyć sieć wirtualną platformy Azure, która jest siecią lokalną tooyour połączonych.
- Połączone hello obwodu ExpressRotue dla toohello HANA dużych wystąpień tej samej sieci wirtualnej platformy Azure.
- Zainstalowano maszyny Wirtualnej platformy Azure są używane jako okno przeskoku HANA dużych wystąpień.
- Wprowadzone należy się upewnić, że można się połączyć z hello skok pole tooyour HANA dużych wystąpienia jednostki i na odwrót.
- Należy sprawdzić czy hello wszystkich wymaganych pakietów i poprawki są instalowane.
- Możesz przeczytać hello SAP uwagi i dokumenty dotyczące instalacji HANA na powitania systemu operacyjnego jest używany i upewnienie się, że wersji HANA hello wybór jest obsługiwana w wersji hello systemu operacyjnego.

Co to jest wyświetlany w sekwencjach dalej hello jest pobierania hello hello HANA instalacji pakietów toohello skok pola uruchomionych maszyn wirtualnych, w tym przypadku na systemu operacyjnego, hello kopię hello pakiety toohello HANA dużych wystąpienia jednostki i sekwencji hello hello instalacji.

### <a name="download-of-hello-sap-hana-installation-bits"></a>Pobieranie usługi bits instalacji SAP HANA hello
Ponieważ hello HANA dużych wystąpienia jednostki nie zawierają one toohello bezpośrednie połączenie między Internetu, nie można bezpośrednio pobrać pakietów instalacyjnych hello z toohello SAP HANA dużych wirtualna wystąpienia. tooovercome hello Brak bezpośrednie połączenie z Internetem, należy hello okno przeskoku. Możesz pobrać hello pakiety toohello skok pole maszyny Wirtualnej.

W kolejności toodownload hello HANA pakietów instalacyjnych należy użytkownik S SAP lub innego użytkownika, dzięki czemu możesz tooaccess hello SAP Marketplace. Po zalogowaniu, przejdź do tej sekwencji ekrany:

Przejdź za[Marketplace usługi SAP](https://support.sap.com/en/index.html) > kliknij przycisk Pobierz oprogramowanie > instalacje i uaktualnienia > przez indeks alfabetyczny > w obszarze H — SAP HANA platformy Edition > SAP HANA platformy wersji 2.0 > instalacji > hello pobierania następujące pliki

![Pobierz HANA instalacji](./media/hana-installation/image16_download_hana.PNG)

W przypadku pokaz hello pobraliśmy pakietów instalacyjnych SAP HANA 2.0. Na powitania okno przeskoku platformy Azure maszyny Wirtualnej rozwiń węzeł hello samowyodrębniający archiwa do katalogu hello, jak pokazano poniżej.

![Wyodrębnij HANA instalacji](./media/hana-installation/image17_extract_hana.PNG)

Zgodnie z archiwami hello są wyodrębniane, skopiuj katalog hello utworzony przez wyodrębniania hello, w przypadku hello powyżej 51052030, toohello HANA dużych wystąpienia jednostki w hello /hana/shared wolumin do katalogu, który został utworzony.

> [!Important]
> Nie kopiowania pakietów instalacyjnych hello do głównego hello lub rozruch jednostki LUN, ponieważ miejsca jest ograniczona i musi toobe używana przez inne procesy, jak również.


### <a name="install-sap-hana-on-hello-hana-large-instance-unit"></a>Zainstaluj SAP HANA na powitania HANA dużych wystąpienia jednostki
W kolejności tooinstall SAP HANA należy toolog w jako użytkownik główny. Tylko główny ma za mało tooinstall uprawnienia SAP HANA.
najpierw Hello należy toodo jest tooset uprawnień w katalogu hello kopiowane do/hana/udostępnionych. uprawnienia Hello muszą tooset, takich jak

```
chmod –R 744 <Installation bits folder>
```

Jeśli chcesz tooinstall SAP HANA przy użyciu graficznego hello Instalatora, hello toobe potrzeb pakietu gtk2 zainstalowane na powitania HANA dużych wystąpień. Sprawdź, czy jest zainstalowany za pomocą polecenia hello

```
rpm –qa | grep gtk2
```

W dalszych krokach możemy są prezentacja hello SAP HANA Instalatorowi hello graficznego interfejsu użytkownika. Następnego kroku przejdź do katalogu instalacyjnego hello i przejdź do katalogu sub hello HDB_LCM_LINUX_X86_64. Uruchamianie

```
./hdblcmgui 
```
z tego katalogu. Teraz pobierania zapoznasz się sekwencję ekrany wymagających danych hello tooprovide hello instalacji. W przypadku hello wykazać firma Microsoft jest instalowany serwer bazy danych SAP HANA hello i składniki klienta hello SAP HANA. W związku z tym naszej zaznaczenie jest "Bazy danych SAP HANA", jak pokazano poniżej

![Wybierz HANA w instalacji](./media/hana-installation/image18_hana_selection.PNG)

W następnym ekranie powitania wybierz opcję hello "Instalacji nowego systemu"

![Wybierz opcję HANA nowa instalacja](./media/hana-installation/image19_select_new.PNG)

Po wykonaniu tego kroku należy tooselect między kilka dodatkowych składników, które mogą być instalowane Ponadto serwer bazy danych SAP HANA toohello.

![Wybierz dodatkowe składniki HANA](./media/hana-installation/image20_select_components.PNG)

W tej dokumentacji w celu hello możemy została wybrana hello SAP HANA klienta i hello SAP HANA Studio. Możemy również zainstalować wystąpienie skalowanie w pionie. Dlatego w następnym ekranie powitania należy toochoose "Jednego hosta System" 

![Wybierz opcję instalacji skalowanie w pionie](./media/hana-installation/image21_single_host.PNG)

W następnym ekranie powitania muszą tooprovide niektórych danych

![Podaj SAP HANA SID](./media/hana-installation/image22_provide_sid.PNG)

> [!Important]
> Jako HANA systemu (SID), należy tooprovide hello sam identyfikator SID, podane firmy Microsoft, gdy uporządkowane hello wystąpienia dużych HANA wdrożenia. Wybieranie innym identyfikatorem SID sprawia, że instalacja hello zakończyć się niepowodzeniem ze względu na problemy związane z uprawnieniami tooaccess na różnych woluminach hello

Jako katalog instalacyjny, możesz użyć hello /hana/shared katalogu. W następnym kroku hello należy hello HANA danych plików i plików dziennika HANA hello tooprovide hello lokalizacji


![Podaj lokalizację dziennika HANA](./media/hana-installation/image23_provide_log.PNG)

> [!Note]
> Należy zdefiniować jako plików danych i dziennika hello woluminów, które już dołączone hello punkty instalacji, które zawierają hello SID wybrano w zaznaczeniu ekranie powitania przed tego ekranu. Jeśli hello SID niezgodność z hello, co zostało wpisane w, na ekranie powitania przed, przejdź wstecz i dostosować hello wartość toohello identyfikatora SID przez Ciebie na powitania punktów instalacji.

W następnym kroku hello Przejrzyj hello nazwy hosta i ostatecznie Popraw go. 

![Przejrzyj nazwy hosta](./media/hana-installation/image24_review_host_name.PNG)

W następnym kroku hello potrzebne są także dane tooretrieve należy nadać tooMicrosoft, gdy uporządkowane hello wystąpienia dużych HANA wdrożenia. 

![Podaj użytkownika systemu identyfikatorów UID i GID](./media/hana-installation/image25_provide_guid.PNG)

> [!Important]
> Należy tooprovide hello tego samego Identyfikatora użytkownika systemu i Identyfikatora grupy użytkowników, podane firmy Microsoft, jak zamówienia hello jednostki wdrożenia. Jeśli nie zostanie toogive hello bardzo takich samych identyfikatorów, hello na instalację programu SAP HANA hello HANA dużych wystąpienia jednostki kończy się niepowodzeniem.

W dwóch następnych ekranach hello, które firma Microsoft nie są wyświetlane w tej dokumentacji, potrzebne tooprovide hello hasło dla użytkownika SYSTEM hello bazy danych SAP HANA hello i hello hasła dla użytkownika sapadm hello, który służy do hello SAP agenta hosta, które są instalowane jako część Witaj wystąpienie bazy danych SAP HANA.

Po zdefiniowaniu hello hasła, ekran potwierdzenia jest wyświetlane. Sprawdź wszystkie dane hello się na liście i kontynuuj instalację hello. Zostanie wyświetlona dokumenty hello postęp instalacji, takich jak hello jedną poniżej ekran postępu

![Sprawdź postęp instalacji](./media/hana-installation/image27_show_progress.PNG)

Zgodnie z zakończeniem instalacji hello, powinien obraz, takich jak powitania po jednym

![Instalacja została zakończona](./media/hana-installation/image28_install_finished.PNG)

W tym momencie wystąpienia SAP HANA hello powinna być maksymalnie i działa prawidłowo i gotowe do użycia. Powinno być możliwe tooconnect tooit z SAP HANA Studio. Upewnij się również wyszukać hello najnowsze poprawki programu SAP HANA i stosować te poprawki.
























































 







 




