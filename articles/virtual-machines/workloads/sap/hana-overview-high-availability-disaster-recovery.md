---
title: "aaaHigh dostępności i odzyskiwania po awarii programu SAP HANA na platformie Azure (wystąpienia duże) | Dokumentacja firmy Microsoft"
description: "Ustal wysokiej dostępności i planu odzyskiwania po awarii programu SAP HANA na platformie Azure (wystąpienia duże)."
services: virtual-machines-linux
documentationcenter: 
author: RicksterCDN
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
ms.openlocfilehash: 0c0967f54cf29bbb275eb7cda9d36608488add9e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="sap-hana-large-instances-high-availability-and-disaster-recovery-on-azure"></a>SAP HANA (duże wystąpień) wysokiej dostępności i odzyskiwania po awarii na platformie Azure 

Wysoka dostępność i odzyskiwanie po awarii są ważne kwestie związane z uruchomionych z kluczowych SAP HANA na serwerach Azure (wystąpienia duże). Jego ważne toowork z SAP, system integrator lub Microsoft tooproperly architektów i wdrożenie hello strategii prawo wysoki dostępności/odzyskiwania po awarii. Istnieje również cel punktu odzyskiwania hello tooconsider ważne i celu czasu odzyskiwania, które są tooyour określonego środowiska.

## <a name="high-availability"></a>Wysoka dostępność

Firma Microsoft zapewnia metody wysokiej dostępności SAP HANA "poza pole hello", które obejmują:

- **Replikacja magazynu:** hello tooreplicate możliwości system przechowywania wszystkich lokalizacji tooanother danych (w ramach, lub oddzielnie od hello tym samym centrum danych). SAP HANA działa niezależnie od tej metody.
- **Replikacji systemu HANA:** hello replikacji wszystkich danych w oddzielnym systemie SAP HANA tooa SAP HANA. celu czasu odzyskiwania Hello jest zminimalizowany do replikacji danych w regularnych odstępach czasu. SAP HANA obsługuje asynchroniczne, synchronicznej tryby w pamięci i synchroniczne (zalecane tylko dla SAP HANA hello systemów, które znajdują się w tym samym centrum danych lub mniej niż 100 KM od siebie). Hello bieżącego projektu HANA dużych wystąpienia sygnatur w HANA replikacji systemu może służyć tylko wysokiej dostępności.
- **Host trybu failover automatycznego:** toouse rozwiązania lokalnego odzyskiwania usterek, jako alternatywnej toosystem replikacji. Gdy węzeł główny hello staje się niedostępny, co najmniej jeden węzeł rezerwy SAP HANA są skonfigurowane w trybie skalowalnego w poziomie i SAP HANA automatycznie przełącza tooanother węzła.

Aby uzyskać więcej informacji na temat SAP HANA wysokiej dostępności Zobacz hello następujących informacji SAP:

- [Oficjalny dokument programu SAP HANA wysokiej dostępności](http://go.sap.com/documents/2016/05/f8e5eeba-737c-0010-82c7-eda71af511fa.html)
- [Przewodnik administracji programu SAP HANA](http://help.sap.com/hana/SAP_HANA_Administration_Guide_en.pdf)
- [Akademia SAP wideo na replikacji systemu SAP HANA](http://scn.sap.com/community/hana-in-memory/blog/2015/05/19/sap-hana-system-replication)
- [Obsługa Uwaga #1999880 — często zadawane pytania dotyczące replikacji systemu SAP HANA SAP](https://bcs.wdf.sap.corp/sap/support/notes/1999880)
- [Obsługa Uwaga #2165547 — SAP HANA tworzenia kopii zapasowej i przywracania w środowisku replikacji programu SAP HANA systemu SAP](https://websmp230.sap-ag.de/sap(bD1lbiZjPTAwMQ==)/bc/bsp/sno/ui_entry/entry.htm?param=69765F6D6F64653D3030312669765F7361706E6F7465735F6E756D6265723D3231363535343726)
- [SAP Uwaga Obsługa #1984882 — za pomocą replikacji systemu SAP HANA wymiany sprzętu przestojów minimalna/Zero](https://websmp230.sap-ag.de/sap(bD1lbiZjPTAwMQ==)/bc/bsp/sno/ui_entry/entry.htm?param=69765F6D6F64653D3030312669765F7361706E6F7465735F6E756D6265723D3139383438383226)

## <a name="disaster-recovery"></a>Odzyskiwanie po awarii

SAP HANA na platformie Azure (wystąpienia duże) jest oferowana w dwóch regionach platformy Azure w regionie geograficznymi. Między hello dwóch dużych wystąpienia sygnatury o dwóch różnych regionach jest bezpośrednie łączność do replikacji danych podczas odzyskiwania po awarii. Replikacja Hello danych hello jest na podstawie infrastruktury magazynu. Witaj replikacji nie jest wykonywana domyślnie. Została ona wysłana dla konfiguracji klienta hello, uporządkowanych hello odzyskiwania po awarii. Hello bieżącego projektu w HANA system replikacji nie może służyć do odzyskiwania po awarii.

Jednak zaletą tootake hello odzyskiwania po awarii, dlatego należy toostart toodesign hello sieci łączności toohello dwóch różnych regionach platformy Azure. toodo, należy więc połączenie obwodu Azure ExpressRoute z lokalnymi główny region platformy Azure i inne obwodu połączenie z lokalnymi tooyour odzyskiwania po awarii regionu. To jest miara obejmowałoby sytuacji, w którym pełną regionu Azure, łącznie z lokalizacji Microsoft enterprise krawędzi routera (MSEE) wystąpił problem.

Jako druga Metryka używana można połączyć wszystkie sieci wirtualne Azure łączących tooSAP HANA na platformie Azure (duże wystąpień) w jednym z tooboth regionów hello tych obwody usługi ExpressRoute. To jest miara dotyczy przypadku, gdy tylko jeden lokalizacji MSEE hello łączącego Twojej lokalizacji lokalnej z Azure przechodzi nieczynne.

Witaj poniższej ilustracji przedstawiono hello konfiguracją optymalną dla odzyskiwania po awarii:

![Konfiguracją optymalną dla odzyskiwania po awarii](./media/hana-overview-high-availability-disaster-recovery/image1-optimal-configuration.png)

Witaj optymalne przypadek konfiguracji odzyskiwania po awarii sieci hello jest toohave dwa obwody usługi ExpressRoute z lokalnymi toohello dwóch różnych regionach platformy Azure. Jeden obwód przechodzi tooregion #1, na którym uruchomiono wystąpienie produkcji. drugi obwodu ExpressRoute Hello przechodzi tooregion #2 uruchamianie niektórych wystąpień HANA nieprodukcyjnych. (Jest to ważne, jeśli cały region platformy Azure, tym hello MSEE i sygnatury dużych wystąpienia wychodzeniu hello siatki.)

Jako druga Metryka hello różnych sieci wirtualnych są połączone toohello różnych obwody usługi ExpressRoute, które są połączone tooSAP HANA na platformie Azure (wystąpienia duże). Hello lokalizacji, gdzie MSEE kończy się niepowodzeniem, lub można obniżyć hello cel punktu odzyskiwania podczas odzyskiwania po awarii, można pominąć, ponieważ omówiono później.

Witaj dalej wymagania dotyczące konfiguracji odzyskiwania po awarii są:

- Na jednostki SKU Azure (wystąpienia duże) z hello sam rozmiar jako jednostki SKU produkcyjnego i wdrożyć je w hello region odzyskiwania po awarii należy zamówić SAP HANA. Te wystąpienia może być używane toorun testu, piaskownicy lub wystąpień HANA pytań i odpowiedzi.
- Należy zamówić profilu odzyskiwania po awarii dla każdego z programu SAP HANA na jednostki SKU Azure (wystąpienia duże), które mają toorecover w lokacji odzyskiwania po awarii hello, jeśli to konieczne. Ta akcja prowadzi toohello Alokacja magazynu woluminy, które są docelowy hello hello replikacji magazynu z Twoim regionie produkcji w hello region odzyskiwania po awarii.

Po hello poprzedzających wymagania zostały spełnione, jest ona z replikacji magazynu hello toostart odpowiedzialności. W infrastrukturze magazynu hello używany dla SAP HANA na platformie Azure (wystąpienia duże) podstawą hello replikacji magazynu jest magazynu migawek. toostart hello odzyskiwania po awarii replikacji, należy tooperform:

- Migawka rozruchowych jednostki LUN, zgodnie z wcześniejszym opisem.
- Migawka woluminów powiązane HANA, zgodnie z wcześniejszym opisem.

Po wykonaniu te migawki początkowej repliki woluminów hello jest rozpoczęta hello woluminach, które są skojarzone z danym profilem odzyskiwania po awarii w regionie odzyskiwania po awarii hello.

Następnie hello najnowszych migawki magazynu jest używana co godzinę delty hello tooreplicate, których tworzenie aplikacji na powitania woluminów magazynu.

Witaj cel punktu odzyskiwania, które odbywa się w tej konfiguracji jest od 60 minut too90. tooachieve lepsze odzyskiwania cel w przypadku odzyskiwania po awarii hello kopiowania hello HANA kopie zapasowe dziennika transakcji z SAP HANA na toohello Azure (wystąpienia duże) punktu inny region platformy Azure. tooachieve ten cel punktu odzyskiwania hello następujące:

1. Utwórz kopię zapasową transakcji HANA hello Zaloguj się jako często, jak to możliwe za/hana / / kopii zapasowej dziennika.
2. Kopiowanie hello kopie zapasowe dziennika transakcji, jeśli są Zakończono tooan maszyny wirtualnej platformy Azure (VM), który znajduje się w sieci wirtualnej, który został podłączony toohello SAP HANA na serwerze Azure (wystąpienia duże).
3. Z tej maszyny Wirtualnej skopiuj hello tooa kopii zapasowej maszyny Wirtualnej, który znajduje się w sieci wirtualnej w regionie odzyskiwania po awarii hello.
4. Zachowaj kopie zapasowe dziennika transakcji hello, regionu w hello maszyny Wirtualnej.

W razie awarii po hello odzyskiwania po awarii profil został wdrożony na używanego serwera, skopiować hello kopie zapasowe dziennika transakcji z hello wirtualna toohello SAP HANA na platformie Azure (wystąpienia duże) jest teraz serwerem podstawowym hello w regionie odzyskiwania po awarii hello, i przywrócenie tych kopii zapasowych. Odzyskiwanie jest możliwe, ponieważ stan hello HANA na dyskach odzyskiwania po awarii hello jest to, że migawki HANA. To jest punkt przesunięcia hello dalsze operacje przywracania z kopii zapasowej dziennika transakcji.

## <a name="backup-and-restore"></a>Tworzenie kopii zapasowej i przywracanie

Jest jednej z baz danych hello najważniejszych aspektów toooperating upewnienie się, że hello bazy danych mogą być chronione od różnych zdarzeń losowych. Te zdarzenia może być spowodowane przez coś z klęski żywiołowej toosimple użytkownika błędów.

Tworzenie kopii zapasowej bazy danych, z toorestore możliwości hello go tooany punktu w czasie (takich jak przed ktoś usunął kluczowe dane), umożliwia przywrócenie tooa stanu jak, jak to możliwe sposób toohello był przed wystąpieniem hello przerw w działaniu.

Dwa typy kopii zapasowych należy wykonać w celu uzyskania najlepszych wyników:

- Kopie zapasowe bazy danych
- Kopie zapasowe dziennika transakcji

Ponadto toofull kopie zapasowe bazy danych wykonywane na poziomie aplikacji, można jeszcze bardziej szczegółowej, wykonując kopie zapasowe z magazynu migawek. Wykonywanie kopii zapasowych dziennika są też ważne przywracania bazy danych hello (i dzienniki hello tooempty już zatwierdzone transakcje).

SAP HANA na platformie Azure (wystąpienia duże) oferuje dwie opcje tworzenia kopii zapasowej i przywracania:

- Należy ją samodzielnie (DIY). Po tooensure obliczyć miejsca na dysku, należy wykonać pełne kopie zapasowe bazy danych i dziennika przy użyciu metody wykonywania kopii zapasowej dysku (toothose dyski). Wraz z upływem czasu hello kopie zapasowe są tooan skopiowanych kontem magazynu platformy Azure (po skonfigurowaniu serwera plików z systemem Azure z magazynem nieograniczoną) lub Użyj magazynu usługi Kopia zapasowa Azure lub usługi Azure storage chłodni. Innym rozwiązaniem jest toouse narzędzia ochrony danych innych firm, takich jak Commvault, kopie zapasowe hello toostore po ich skopiowane tooa konta magazynu. Witaj DIY opcję tworzenia kopii zapasowej może być także konieczne dla danych, które wymagałyby toobe przechowywane przez dłuższy czas, zgodności i inspekcji.
- Użyj hello kopii zapasowej i przywracania funkcji hello podstawowej infrastruktury SAP HANA na platformie Azure (wystąpienia duże) zawiera. Ta opcja spełnia potrzeby hello kopii zapasowych, a także udostępnia ręcznego tworzenia kopii zapasowych niemal przestarzałe (z wyjątkiem przypadków, gdy kopie zapasowe danych są wymagane do celów zgodności). Hello pozostałej części tej sekcji adresy hello kopii zapasowej i przywracania funkcje, które jest oferowany z HANA (duże wystąpień).

> [!NOTE]
> Hello migawki technologia, która jest używana przez hello podstawowej infrastruktury HANA (duże wystąpień) ma zależność na migawki SAP HANA. Migawki SAP HANA nie działają w połączeniu z kontenerami bazy danych programu SAP HANA wielodostępnej. W związku z tym ta metoda tworzenia kopii zapasowej nie może być używane toodeploy SAP HANA wielodostępnej bazy danych kontenerów.

### <a name="using-storage-snapshots-of-sap-hana-on-azure-large-instances"></a>Przy użyciu magazynu migawek SAP HANA na platformie Azure (wystąpienia duże)

Infrastruktura magazynu Hello bazowy SAP HANA na platformie Azure (wystąpienia duże) obsługuje pojęcie hello migawki woluminów magazynu. Zarówno kopii zapasowej i przywracania dla określonego woluminu są obsługiwane przez hello następujące zagadnienia:

- Zamiast kopii zapasowych bazy danych wykonywane na częste migawek woluminu magazynu.
- migawki magazynu Hello inicjuje migawki SAP HANA przed rozpoczęciem wykonywania hello pamięci masowej migawki. Ta migawka SAP HANA jest punkt instalacji hello operacje przywracania dziennika ostatecznego po odzyskaniu hello pamięci masowej migawki.
- W momencie hello gdzie hello pamięci masowej migawki jest wykonywane prawidłowo hello SAP HANA migawka jest usuwana.
- Kopie zapasowe dziennika często zarejestrowane i przechowywane w woluminie kopii zapasowej dziennika hello lub na platformie Azure.
- Jeśli należy przywrócić bazę hello tooa niektórych punktu w czasie, żądań pomocy technicznej platformy Azure (awarii w środowisku produkcyjnym) lub SAP HANA tooMicrosoft na tooa toorestore zarządzania usługą Azure niektórych magazynu migawek (na przykład planowane Przywracanie systemu piaskownicy tooits pierwotnego stanu).
- Witaj SAP HANA migawki, która była dostępna w migawce magazynu hello jest punktem przesunięcia stosowania kopie zapasowe dziennika, które zostały wykonane i przechowywane po hello pamięci masowej migawki.
- Te kopie zapasowe dziennika są pobierane toorestore tooa wstecz hello bazy danych, niektóre punktu w czasie.

Określanie hello kopii zapasowej\_nazwa tworzy migawkę hello następujące woluminy:

- Hana/danych
- Hana/dziennika
- Hana/log\_kopii zapasowej (zainstalowany jako kopii zapasowej do hana/log)
- Hana/udostępnionych

### <a name="storage-snapshot-considerations"></a>Zagadnienia dotyczące magazynu migawki

>[!NOTE]
>Migawki magazynu są _nie_ dostarczony bezpłatnie, ponieważ musi być przydzielona dodatkowego miejsca.

Hello mechanika określonego magazynu migawek dla SAP HANA na platformie Azure (wystąpienia duże) obejmują:

- Migawki określonego magazynu (w momencie hello w czasie, gdy jest zajęty) zużywa bardzo mało pamięci masowej.
- Jako dane zmiany zawartości i hello zawartości w danych SAP HANA zmienić plików na woluminie magazynu hello migawki hello musi toostore hello oryginalnej zawartości bloku.
- migawki magazynu Hello wzrost rozmiaru. istnieje Hello dłużej hello migawki, staje się hello większych hello pamięci masowej migawki.
- Witaj więcej zmian toohello woluminie bazy danych SAP HANA okresu istnienia hello migawki magazynu, staje się hello większych hello użycie miejsca na powitania pamięci masowej migawki.

SAP HANA na platformie Azure (wystąpienia duże) jest dostarczany z stały wolumin rozmiary hello wolumin danych i dziennika SAP HANA. Wykonywanie migawek woluminy eats do ilość miejsca na woluminie, więc jest Twoje odpowiedzialność tooschedule magazynu migawek (w ramach hello SAP HANA na proces Azure [dużych wystąpień]).

Witaj poniższe sekcje zawierają informacje dotyczące wykonywania migawek, w tym ogólne zalecenia:

- Chociaż hello sprzętu może wytrzymać 255 migawek dla każdego woluminu, zdecydowanie zaleca się to zapewnić, że również pod ten numer.
- Przed wykonaniem migawki pamięci masowej, monitorować i śledzić ilość wolnego miejsca.
- Mniejszą hello liczbę migawek magazynu oparte na wolnego miejsca. Może być konieczne toolower hello liczby migawek, które są stale lub może być tooextend hello woluminów. (W jednostkach 1 TB można zamówić dodatkowego miejsca do magazynowania).
- Podczas działania, takie jak przenoszenie danych do programu SAP HANA z narzędzi migracji systemu (bez R3load lub przez Przywracanie z kopii zapasowej bazy danych SAP HANA) zaleca się nie wykonać wszystkie migawki magazynu. (Jeśli migracja systemu jest wykonywana na nowego systemu SAP HANA, magazynu migawek nie musi wykonać toobe.)
- Podczas większych reorganizacji SAP HANA tabel Jeśli to możliwe należy unikać magazynu migawek.
- Migawki magazynu są możliwości odzyskiwania po awarii hello wymagań wstępnych tooengaging SAP HANA na platformie Azure (wystąpienia duże).

### <a name="setting-up-storage-snapshots"></a>Konfigurowanie magazynu migawek

1. Upewnij się, że Perl jest zainstalowana w systemie operacyjnym Linux hello na serwerze (duże wystąpień) HANA hello.
2. Modyfikowanie/etc/ssh/ssh\_config tooadd hello wiersza _Mac hmac-sha1_.
3. W węźle głównym powitania dla każdego wystąpienia SAP HANA, na którym jest uruchomiony (jeśli dotyczy), należy utworzyć konto użytkownika kopii zapasowej SAP HANA.
4. Hello SAP HANA HDB klienta musi być zainstalowana na wszystkich serwerach (duże wystąpień) SAP HANA.
5. Na powitania pierwszego serwera SAP HANA (duże wystąpień) każdego regionu klucza publicznego musi zostać utworzony hello tooaccess podstawowej infrastruktury magazynu, który kontroluje Tworzenie migawki.
6. Skopiuj skrypt hello azure\_hana\_backup.pl z lokalizacji toohello/skrypty **hdbsql** z hello instalacji SAP HANA.
7. Hello kopiowania HANABackupDetails.txt plik z toohello/skrypty sam lokalizacji jako hello skryptów języka Perl.
8. Zmodyfikuj hello HANABackupDetails.txt zgodnie z potrzebami dla hello specyfikacjami odpowiedniego klienta.

### <a name="step-1-install-sap-hana-hdbclient"></a>Krok 1: Instalowanie SAP HANA HDBClient

Hello systemu Linux w systemie SAP HANA na platformie Azure (wystąpienia duże) obejmuje foldery hello i skrypty niezbędne tooexecute SAP HANA magazynu migawek dla celów tworzenia kopii zapasowych i odzyskiwania po awarii. Warto jednak tooinstall Twojego odpowiedzialność SAP HANA HDBclient podczas instalowania SAP HANA. (Microsoft Instaluje hello HDBclient ani SAP HANA.)

### <a name="step-2-change-etcsshsshconfig"></a>Krok 2: Zmień/etc/ssh/ssh\_konfiguracji

Zmień/etc/ssh/ssh\_konfiguracji przez dodanie _Mac hmac-sha1_ wiersz w sposób pokazany poniżej:
```
#   RhostsRSAAuthentication no
#   RSAAuthentication yes
#   PasswordAuthentication yes
#   HostbasedAuthentication no
#   GSSAPIAuthentication no
#   GSSAPIDelegateCredentials no
#   GSSAPIKeyExchange no
#   GSSAPITrustDNS no
#   BatchMode no
#   CheckHostIP yes
#   AddressFamily any
#   ConnectTimeout 0
#   StrictHostKeyChecking ask
#   IdentityFile ~/.ssh/identity
#   IdentityFile ~/.ssh/id_rsa
#   IdentityFile ~/.ssh/id_dsa
#   Port 22
Protocol 2
#   Cipher 3des
#   Ciphers aes128-ctr,aes192-ctr,aes256-ctr,arcfour256,arcfour128,aes128-cbc,3des-cbc
#   MACs hmac-md5,hmac-sha1,umac-64@openssh.com,hmac-ripemd160
MACs hmac-sha1
#   EscapeChar ~
#   Tunnel no
#   TunnelDevice any:any
#   PermitLocalCommand no
#   VisualHostKey no
#   ProxyCommand ssh -q -W %h:%p gateway.example.com
```

### <a name="step-3-create-a-public-key"></a>Krok 3: Tworzenie klucza publicznego

Na powitania pierwszy SAP HANA na serwerze Azure (duże wystąpień) w każdym regionie Azure, tworzenie infrastruktury magazynu hello tooaccess publicznego klucza toobe używany, dzięki czemu można utworzyć migawki. klucz publiczny Hello zapewnia, że hasło nie jest wymagane toosign w magazynie toohello i poświadczenia hasła nie są zachowywane. W systemie Linux na powitania serwera SAP HANA (duże wystąpienia) wykonaj powitania po klucz publiczny hello toogenerate polecenia:
```
  ssh-keygen –t dsa –b 1024
```
Nowa lokalizacja Hello jest _/root/.ssh/id\_dsa.pub. Nie wpisuj rzeczywiste hasło, w przeciwnym razie wymagane tooenter hello hasło będzie zawsze możesz się zalogować. Zamiast tego, naciśnij klawisz **Enter** dwukrotnie tooremove hello należy wprowadzić wymaganie hasła do logowania.

Sprawdź toomake się, że klucz publiczny hello został rozwiązany, zgodnie z oczekiwaniami, zmieniając too/root/.ssh/ folderów, a następnie wykonywanie hello **ls** polecenia. Jeśli klucz hello jest obecny, można go skopiować, uruchamiając następujące polecenie hello:

![Klucz publiczny jest kopiowany przez uruchomienie tego polecenia](./media/hana-overview-high-availability-disaster-recovery/image2-public-key.png)

W tym momencie skontaktuj się z SAP HANA na zarządzania usługą Azure i podanie hello klucza. Witaj działu obsługi używa publicznego klucza tooregister hello w hello podstawowej infrastruktury magazynu.

### <a name="step-4-create-an-sap-hana-user-account"></a>Krok 4: Tworzenie konta użytkownika SAP HANA

Tworzenie konta użytkownika SAP HANA poziomu SAP HANA Studio do wykonywania kopii zapasowych. To konto musi mieć następujące uprawnienia hello: _administratora kopii zapasowych_ i _odczytu katalogu_. W tym przykładzie hello username SCADMIN jest tworzony.

![Tworzenie użytkownika w HANA Studio](./media/hana-overview-high-availability-disaster-recovery/image3-creating-user.png)

### <a name="step-5-authorize-hello-sap-hana-user-account"></a>Krok 5: Autoryzowanie konta użytkownika SAP HANA hello

Autoryzacja konta użytkownika SAP HANA hello (używane przez skrypty hello bez autoryzacji w każdym uruchomieniu skryptu hello toobe). polecenie SAP HANA Hello `hdbuserstore` umożliwia tworzenie hello SAP HANA klucza użytkownika, który jest przechowywany na co najmniej jeden węzeł SAP HANA. klucz użytkownika Hello umożliwia także hello użytkownika tooaccess SAP HANA bez hasła toomanage z hello skryptów omówiono w dalszej części procesu.

>[!IMPORTANT]
>Uruchom hello następujące polecenie jako `_root_`. W przeciwnym razie hello skryptu nie może działać poprawnie.

Wprowadź hello `hdbuserstore` polecenia w następujący sposób:

![Wprowadź polecenie hdbuserstore hello](./media/hana-overview-high-availability-disaster-recovery/image4-hdbuserstore-command.png)

W hello poniższy przykład, gdy użytkownik hello jest SCADMIN01 i hello nazwa hosta jest lhanad01, polecenie hello jest:
```
hdbuserstore set SCADMIN01 lhanad01:30115 <backup username> <password>
```
Zarządzanie wszystkie skrypty z jednego serwera do skalowania w poziomie HANA wystąpień. W tym przykładzie należy zmienić klucz SAP HANA hello SCADMIN01 dla każdego hosta w sposób zapewniający odzwierciedla hello hosta, który jest powiązane toohello klucza. Oznacza to, hello konto kopii zapasowej SAP HANA zmienia się z liczbą wystąpień hello hello HANA DB **lhanad**. klucz Hello musi mieć uprawnienia administracyjne na hoście hello, który jest przypisany do, a hello użytkownika kopii zapasowej dla skalowalnego w poziomie musi mieć wystąpień SAP HANA tooall praw dostępu.
```
hdbuserstore set SCADMIN01 lhanad:30015 SCADMIN <password>
hdbuserstore set SCADMIN02 lhanad:30115 SCADMIN <password>
hdbuserstore set SCADMIN03 lhanad:30215 SCADMIN <password>
```

### <a name="step-6-copy-items-from-hello-scripts-folder"></a>Krok 6: Kopiowanie elementów z folderu/skrypty hello

Kopia hello następujących elementów z hello/skrypty katalogu roboczego toohello folderu (znajdującego się na powitania złoty obraz instalacji hello) **hdbsql**. W przypadku bieżącej instalacji HANA ten katalog jest /hana/shared/D01/exe/linuxx86\_64/hdb.
```
azure\_hana\_backup.pl
testHANAConnection.pl
testStorageSnapshotConnection.pl
removeTestStorageSnapshot.pl
HANABackupCustomerDetails.txt
```
Skopiuj hello poniższych elementach, jeśli są na nich uruchomione skalowalnego w poziomie lub OLAP:
```
azure\_hana\_backup\_bw.pl
testHANAConnectionBW.pl
testStorageSnapshotConnectionBW.pl
removeTestStorageSnapshotBW.pl
HANABackupCustomerDetailsBW.txt
```
Plik HANABackupCustomerDetails.txt Hello jest można modyfikować w następujący sposób w przypadku wdrożenia skalowania w górę. Jest hello kontroli i pliku konfiguracji dla hello skryptu, który uruchamia hello magazynu migawek. Powinna zostać odebrana hello _nazwę magazynu kopii zapasowej_ i _adres IP magazynu_ z SAP HANA na zarządzanie usługami Azure, gdy wdrożono swoich wystąpień. Nie można zmodyfikować sekwencji hello porządkowanie lub odstępy zmienne hello lub skryptu hello nie działa prawidłowo.

W przypadku wdrożenia skalowania w górę pliku konfiguracji hello wyglądałyby tak jak:
```
#Provided by Microsoft Service Management
Storage Backup Name: lhanad01backup
Storage IP Address: 10.250.20.21
#Created by customer using hdbuserstore
HANA Backup Name: SCADMIND01
```
Do skalowania konfiguracji pliku HANABackupCustomerDetailsBW.txt hello wyglądałyby tak jak:
```
#Provided by Microsoft Service Management
Storage Backup Name: lhanad01backup
Storage IP Address: 10.250.20.21
#Node IP addresses, instance numbers, and HANA backup name
#provided by customer.  HANA backup name created using
#hdbuserstore utility.
Node 1 IP Address: 10.254.15.21
Node 1 HANA instance number: 01
Node 1 HANA Backup Name: SCADMIN01
Node 2 IP Address: 10.254.15.22
Node 2 HANA instance number: 02
Node 2 HANA Backup Name: SCADMIN02
Node 3 IP Address: 10.254.15.23
Node 3 HANA instance number: 03
Node 3 HANA Backup Name: SCADMIN03
Node 4 IP Address: 10.254.15.24
Node 4 HANA instance number: 04
Node 4 HANA Backup Name: SCADMIN04
Node 5 IP Address: 10.254.15.25
Node 5 HANA instance number: 05
Node 5 HANA Backup Name: SCADMIN05
Node 6 IP Address: 10.254.15.26
Node 6 HANA instance number: 06
Node 6 HANA Backup Name: SCADMIN06
Node 7 IP Address: 10.254.15.27
Node 7 HANA instance number: 07
Node 7 HANA Backup Name: SCADMIN07
Node 8 IP Address: 10.254.15.28
Node 8 HANA instance number: 08
Node 8 HANA Backup Name: SCADMIN08
```
>[!NOTE]
>Obecnie tylko szczegóły dotyczące węzła 1 są używane w hello rzeczywiste HANA pamięci masowej migawki skryptu. Zaleca się przetestowanie tooor dostęp ze wszystkich węzłów HANA tak, aby w przypadku węzła głównego kopii zapasowej hello kiedykolwiek zmiany, już zapewnieniu innym węźle może zająć jego miejsce, modyfikując szczegóły hello w węźle 1.

toocheck dla hello właściwej konfiguracji w pliku konfiguracji hello lub wystąpień HANA toohello odpowiednie połączenie, uruchom dowolne z hello następujące skrypty:
- Do konfiguracji skalowania w górę (niezależnie od obciążenia SAP):

 ```
testHANAConnection.pl
```
- Do skalowania konfiguracji:

 ```
testHANAConnectionBW.pl
```

Upewnij się, że to wystąpienie hello wzorca HANA ma serwerów HANA tooall wymaganego dostępu. Nie ma żadnych parametrów toohello skryptu, ale należy wykonać odpowiednie HANABackupCustomerDetails hello / HANABackupCustomerDetailsBW pliku toorun skryptu hello poprawnie. Ponieważ zwracane są tylko hello powłoki poleceń kody błędów, nie jest możliwe dla hello skryptu tooerror wyboru każde wystąpienie. Mimo tego skryptu hello podanie niektórych przydatne uwagi toodouble wyboru.

skrypt hello toorun:
```
 ./testHANAConnection.pl
```
 Skrypt hello pomyślnie uzyska stan hello hello HANA wystąpienia, wyświetla komunikat o pomyślnym hello HANA połączenia.

Ponadto istnieje drugi typ skryptu za pomocą toocheck hello HANA wystąpienia serwera głównego na możliwości toosign w magazynie toohello. Przed wykonaniem hello azure\_hana\_kopii zapasowej (\_bw) .pl skryptu, należy wykonać hello dalej skryptu. Jeśli wolumin nie zawiera żadnych migawek, czy wolumin hello jest po prostu pusty lub nie jest niemożliwe toodetermine ssh hello tooobtain awarii migawki szczegóły. Z tego powodu hello skrypt jest wykonywany, należy wykonać dwie czynności:

- Sprawdzi, czy hello konsoli magazynu jest dostępne.
- Tworzy migawkę testu lub manekina, dla każdego woluminu przez wystąpienie HANA.

Z tego powodu hello HANA wystąpienia jest włączony jako argument. Ponownie nie jest możliwe tooprovide sprawdzanie błędów dotyczących połączenia z magazynem hello, ale hello skrypt zawiera wskazówki przydatne, jeśli hello wykonanie nie powiedzie się.

Witaj skrypt jest uruchamiany jako:
```
 ./testStorageSnapshotConnection.pl <hana instance>
```
Lub jest uruchamiany jako:
```
./testStorageSnapshotConnectionBW.pl <hana instance>
```
skrypt Hello wyświetla również komunikatem, że są możliwe toosign w odpowiednio tooyour wdrożone magazynu dzierżawy, którym skupiono hello jednostki logicznej LUN używanych przez hello wystąpienia serwera, którego jesteś właścicielem.

Przed wykonaniem hello pierwszy magazynu na podstawie migawki kopii zapasowych, należy uruchomić hello dalej skrypty toomake upewnić się, że konfiguracja hello jest poprawna.

Po uruchomieniu tych skryptów, można usunąć, wykonując migawki hello:
```
./removeTestStorageSnapshot.pl <hana instance>
```
Lub
```
./removeTestStorageSnapshot.pl <hana instance>
```

### <a name="step-7-perform-on-demand-snapshots"></a>Krok 7: Wykonaj migawki na żądanie

Wykonaj migawki na żądanie (a także zaplanować regularne migawki za pomocą usługi cron) zgodnie z opisem w tym miejscu.

W przypadku konfiguracji skalowania w górę należy wykonać hello następującego skryptu:
```
./azure_hana_backup.pl lhanad01 customer 20
```
W przypadku konfiguracji skalowania w poziomie wykonaj hello następującego skryptu:
```
./azure_hana_backup_bw.pl lhanad01 customer 20
```
skrypt skalowalnego w poziomie Hello wykonuje pewne dodatkowe sprawdzanie toomake się, że wszystkie serwery HANA są dostępne, i wszystkich wystąpień HANA Zwróć odpowiedni stan wystąpienia hello przed kontynuowaniem tworzenie migawek SAP HANA lub magazynu.

wymagane są Hello następujące argumenty:

- Witaj HANA wystąpienia wymagające kopii zapasowej.
- Prefiks migawki Hello hello pamięci masowej migawki.
- Liczba Hello toobe migawki zachowane do sprecyzowanego prefiksu hello.

```
./azure_hana_backup.pl lhanad01 customer 20
```

wykonywanie skryptu hello Hello tworzy migawkę magazynu hello w tych fazach:

- Wykonaj migawkę HANA.
- Wykonaj migawkę magazynu.
- Usuń hello HANA migawki.

Uruchom skrypt hello wywołując z hello HDB wykonywalnego folderu, który został skopiowany do. Jego kopię zapasową co najmniej hello następujące woluminy, ale również tworzy kopię zapasową woluminu, który ma hello jawna nazwa wystąpienia SAP HANA w hello nazwa woluminu.
```
hana_data_<hana instance>_prod_t020_vol
hana_log_<hana instance>_prod_t020_vol
hana_log_backup_<hana instance>_prod_t020_vol
hana_shared_<hana instance>_prod_t020_vol
```
okres przechowywania Hello jest ściśle zarządzane hello liczby migawek przekazany jako parametr podczas wykonywania skryptu hello (na przykład 20 pokazano wcześniej). Dlatego hello ilość czasu jest funkcją hello okres wykonywania i hello liczby migawek w wywołaniu hello hello skryptu. Jeśli hello liczby migawek, które są zachowane przekracza liczbę hello, które są nazywane jako parametr w wywołaniu hello hello skryptu, hello najstarsza migawka magazynu tej etykiety (w tym przypadku poprzednich _niestandardowych_) zostanie usunięte przed jest nową migawkę wykonywane. Oznacza to numer hello, dawać hello ostatniego parametru wywołania hello jest numer hello można używać toocontrol hello liczby migawek.

>[!NOTE]
>Jak zmienić etykiety hello, zliczania hello jest uruchamiana ponownie.

Należy tooinclude hello HANA wystąpienia nazwą dostarczoną przez SAP HANA na zarządzania usługą Azure jako argument ich tworzenia migawek w środowiskach z wieloma węzłami. W środowiskach z jednym węzłem nazwa hello hello SAP HANA w jednostce Azure (wystąpienia duże) jest wystarczająca, ale nazwa wystąpienia HANA hello nadal jest zalecane.

Ponadto możesz można wykonać kopię zapasową volumes\LUNs rozruch przy użyciu hello takie same skryptu. Użytkownik należy wykonać kopię zapasową woluminu rozruchowego co najmniej raz przy pierwszym uruchomieniu HANA, mimo że firma Microsoft zaleca co tydzień lub co noc harmonogram tworzenia kopii zapasowych do rozruchu w cron. Zamiast niż dodać nazwę wystąpienia SAP HANA, Wstaw _rozruchu_ jako hello argument do skryptu hello w następujący sposób:
```
./azure_hana_backup boot customer 20
```
Witaj tych samych zasad przechowywania zapewniona jest również wolumin rozruchowy toohello. Przy użyciu migawek na żądanie, zgodnie z opisem wcześniej dla przypadków specjalnych, takich jak podczas uaktualniania pakietu (EHP) ulepszenie SAP lub gdy będziesz potrzebować toocreate migawki różne magazynu.

Firma Microsoft zachęca tooperform zaplanowane magazynu migawek, za pomocą usługi cron i zalecane jest użycie hello skryptu takie same dla wszystkich kopii zapasowych i odzyskiwania po awarii potrzeb (modyfikowanie hello skryptu wejść toomatch hello różnych żądany czas tworzenia kopii zapasowej). Te są wszystkie zaplanowane inaczej w cron w zależności od ich czas wykonywania: co godzinę, 12-godzinnym, codziennie lub co tydzień. Harmonogram cron Hello jest zaprojektowana toocreate magazynu migawek, zgodne hello wspomnianej wcześniej przechowywania etykietowania dla długoterminowych kopii zapasowych poza nim. skrypt Hello zawiera polecenia tooback zapasowe wszystkich woluminów produkcji, w zależności od ich żądanej częstotliwość (plików danych i dziennika kopie zapasowe są tworzone co godzinę, podczas gdy wolumin rozruchowy hello jest wykonywana kopia zapasowa codziennie).

wpisy Hello w hello następującego skryptu cron uruchamiane co godzinę, o hello dziesiątego minutę, co 12 godzin w hello dziesiątego minutę i codziennie w hello dziesiątego minutę. cron Hello, które zadania są tworzone w taki sposób, ją tylko jeden magazyn SAP HANA odbywa się podczas dowolnej określonej godziny, dzięki czemu hello co godzinę i codziennych kopii zapasowych nie występują na powitania się, że sama czasu (00:10:00). toohelp optymalizacji sieci Tworzenie migawki i replikacji, SAP HANA na zarządzania usługą Azure zapewnia hello zalecany czas można toorun kopii zapasowych.

Planowanie w /etc/crontab cron domyślne Hello jest następujący:
```
10 1-11,13-23 * * * ./azure_hana_backup.pl lhanad01 hourly 66
10 12 * * *  ./azure_hana_backup.pl lhanad01 12hour 14
```
W poprzednich instrukcji cron hello hello HANA woluminów (bez wolumin rozruchowy) uzyskać co godzinę migawki z etykietą hello. Te migawek 66 zostaną zachowane. Ponadto 14 migawki z etykietą 12-godzinnym hello są zachowywane. Potencjalnie uzyskać co godzinę migawek dla trzech dni, a także migawki 12-godzinnym o czterech dni, które umożliwia cały tydzień migawek.

Planowanie w ramach usługi cron może być trudne, ponieważ tylko jeden skrypt powinien być wykonywany w dowolnym momencie w szczególności, chyba że skrypty hello są rozłożone za kilka minut. Jeśli chcesz codzienne wykonywanie kopii zapasowych w celu przechowywania długoterminowego dziennej migawki są przechowywane wraz z migawki 12-godzinnym (z licznikiem przechowywania siedmiu każdego) lub hello co godzinę migawka jest rozłożona tootake miejsce 10 minutach. Tylko jeden codziennych migawek jest przechowywany w hello wielkości produkcji.
```
10 1-11,13-23 * * * ./azure_hana_backup.pl lhanad01 hourly 66
10 12 * * *  ./azure_hana_backup.pl lhanad01 12hour 7
10 0 * * * ./azure_hana_backup.pl lhanad01 daily 7
```
częstotliwości Hello wymienione w tym miejscu są tylko przykładowe. tooderive optymalną liczbę migawek, hello Użyj następujących kryteriów:

- Wymagania w celu czasu odzyskiwania do punktu w czasie odzyskiwania.
- Użycie miejsca.
- Wymagania dotyczące odzyskiwania punktu cel i celu czasu odzyskiwania do potencjalnego odzyskiwania po awarii.
- Wykonanie ostatecznego HANA pełnej bazy danych z kopii zapasowych na dyskach. Zawsze, gdy kopii zapasowej pełnej bazy danych na dyskach, lub _backint_ interfejsu, jest wykonywana, niepowodzenia wykonywania hello magazynu migawek. Jeśli planujesz tooexecute pełnej bazy danych tworzenie kopii zapasowych na górze magazynu migawek, upewnij się, że hello wykonywania migawek magazynu jest wyłączone w tym czasie.

>[!IMPORTANT]
> Użyj Hello magazynu migawek kopii zapasowych SAP HANA jest prawidłowa tylko wtedy, gdy hello migawek są wykonywane w połączeniu z kopii zapasowych dziennika SAP HANA. Te dziennika kopii zapasowych należy toobe toocover stanie hello okresy między hello magazynu migawek. Jeśli ustawiono toousers zadeklarowanej w momencie odzyskiwania 30 dni, należy hello następujące czynności:

- Możliwość tooaccess magazynu migawek, czyli 30 dni.
- Kopie zapasowe dziennika ciągłe za pośrednictwem hello ostatnich 30 dni.

W zakresie hello kopie zapasowe dziennika należy utworzyć migawkę również hello dziennika kopii zapasowej woluminu. Jednak można się tooperform dziennika regularne tworzenie kopii zapasowych, co pozwala:

- Kopie zapasowe dziennika ciągłe hello potrzeby tooperform w momencie przywracania.
- Wolumin dziennika SAP HANA hello uniemożliwić brakiem miejsca.

Jeden z kroków ostatniego hello jest tooschedule SAP HANA dzienniki kopii zapasowych w SAP HANA Studio. Witaj SAP HANA kopii zapasowej dziennika docelowej jest hello utworzony specjalnie hana/log\_wolumin kopii zapasowych z hello punkt instalacji /hana/log/backups.

![Planowanie tworzenia kopii zapasowych dzienników SAP HANA w SAP HANA Studio](./media/hana-overview-high-availability-disaster-recovery/image5-schedule-backup.png)

Możesz wybrać tworzenie kopii zapasowych, które są częściej niż co 15 minut. W przypadku niektórych użytkowników nawet wykonywać kopie zapasowe dziennika co minutę, chociaż nie zalecamy będzie _za pośrednictwem_ 15 minut.

Ostatnim krokiem Hello jest tooperform na podstawie pliku kopii zapasowej (po początkowej instalacji hello systemu SAP HANA) toocreate jednego wpisu kopii zapasowej, który musi istnieć w katalogu kopii zapasowej hello. W przeciwnym razie SAP HANA nie można zainicjować kopii zapasowych określony dziennik.

![Należy toocreate kopii zapasowej pliku pojedynczy wpis tworzenia kopii zapasowej](./media/hana-overview-high-availability-disaster-recovery/image6-make-backup.png)

### <a name="monitoring-hello-number-and-size-of-snapshots-on-hello-disk-volume"></a>Monitorowanie hello liczby i rozmiaru migawek na woluminie dysku hello

Na woluminie magazynujące można monitorować hello liczbę migawek i użyciu przestrzeni dyskowej hello migawek. Witaj `ls` polecenie nie wyświetla hello migawki katalog lub pliki. Jednak hello polecenia systemu operacyjnego Linux `du` robi, hello następującego polecenia:

- `du –sh .snapshot`zawiera sumę wszystkich migawek w katalogu migawki hello.
- `du –sh --max-depth=1`Wyświetla listę wszystkich migawek, które są zapisywane w folderze .snapshot hello i hello rozmiar każdej migawki.
- `du –hc`zawiera łączny rozmiar hello używane przez wszystkie migawki.

Użyj tych czy migawki hello, zarejestrowane i przechowywane zużywają nie wszystkie magazyny hello na woluminach hello toomake poleceń.

### <a name="reducing-hello-number-of-snapshots-on-a-server"></a>Zmniejszanie hello liczby migawek na serwerze

Zgodnie z opisem, można zmniejszyć liczbę hello niektórych etykiety migawek, które są przechowywane. Witaj ostatnie dwa parametry tooinitiate polecenia hello migawki są etykiety i hello liczby migawek, które mają tooretain.
```
./azure_hana_backup.pl lhanad01 customer 20
```
W poprzednim przykładzie hello etykieta migawki hello jest _klienta_ i hello liczby migawek z tej toobe etykiety zachowane _20_. W odpowiedzi wykorzystanie miejsca toodisk, może być tooreduce hello liczba migawek przechowywanych. łatwe Hello tooreduce hello liczby migawek jest skrypt hello toorun hello ostatniego parametru zestawu too5:
```
./azure_hana_backup.pl lhanad01 customer 5
```
W wyniku uruchamianie skryptu hello to ustawienie jest hello liczby migawek, w tym hello nowego magazynu migawek, _5_.

 >[!NOTE]
 > Ten skrypt powoduje zmniejszenie hello liczby migawek tylko wtedy, gdy więcej niż jedną godzinę hello najnowszych poprzednią migawkę. skrypt Hello nie powoduje usunięcia migawki, które są mniej niż jedną godzinę.

Ograniczenia te są powiązane toohello funkcje opcjonalne odzyskiwania po awarii.

Toomaintain zestawem migawki z tym prefiksem nie są już potrzebne, można wykonać skryptu hello _0_ jako hello przechowywania number tooremove wszystkie migawki dopasowania tego prefiksu. Jednak usunięcie wszystkich migawek może wpływać na powitania możliwości odzyskiwania po awarii.

### <a name="recovering-toohello-most-recent-hana-snapshot"></a>Odzyskiwanie toohello najnowszych HANA migawki

W przypadku hello wystąpi produkcyjnym rozwijanej scenariusza, hello proces przywracania z migawki magazynu może być inicjowane jako zdarzeniem klienta z SAP HANA na zarządzania usługą Azure. Nieoczekiwany scenariusz może być sprawa wysoka pilność, jeśli dane zostały usunięte w produkcji systemu i hello tylko sposób tooretrieve hello danych jest toorestore hello produkcyjną bazę danych.

Na powitania drugiej strony, w momencie odzyskiwania może być niski pilność i planowane na dni wcześniej. Można zaplanować na zarządzania usługą Azure to odzyskiwanie z programu SAP HANA zamiast wywoływanie problem o wysokim priorytecie. Na przykład może być planowania tootry uaktualnienie oprogramowania SAP hello stosując nowy pakiet rozszerzenia, a następnie należy utworzyć kopię toorevert tooa migawki, która reprezentuje stan hello przed uaktualnieniem hello EHP.

Przed wydaniem żądania hello należy toodo pewne przygotowania. SAP HANA zespołu zarządzania usługą Azure, a następnie obsługi żądania hello i udostępnienia hello przywrócić woluminów. W efekcie to maksymalnie tooyou toorestore hello HANA bazy danych na podstawie hello migawki. Oto jak tooprepare dla hello żądania:

>[!NOTE]
>Interfejs użytkownika mogą się różnić od powitania po zrzuty ekranu, w zależności od hello wersji SAP HANA, którego używasz.

1. Zdecyduj, które toorestore migawki. Czy można przywrócić tylko hello hana/danych woluminu, chyba że są poinstruowany.

2. Zamknij hello HANA wystąpienia.

 ![Zamknij hello HANA wystąpienia](./media/hana-overview-high-availability-disaster-recovery/image7-shutdown-hana.png)

3. Odinstaluj woluminy danych hello w każdym węźle bazy danych HANA. Przywracanie Hello hello migawki nie powiedzie się, jeśli nie są odinstalowane hello woluminów danych.

 ![Odinstaluj woluminy danych hello w każdym węźle bazy danych HANA](./media/hana-overview-high-availability-disaster-recovery/image8-unmount-data-volumes.png)

4. Otwórz Pomoc techniczna platformy Azure żądania tooinstruct hello przywrócenie określoną migawkę.

 - Podczas przywracania hello: SAP HANA z zarządzania usługi Azure może poprosić o tooattend tooensure połączenia, który jest poczucia zagubienia żadne dane.

 - Po przywróceniu hello: SAP HANA na zarządzania usługą Azure sygnalizuje hello magazynu migawka została przywrócona.

5. Po ukończeniu procesu przywracania hello Zainstaluj wszystkie woluminy danych.

 ![Zainstaluj wszystkie woluminy danych](./media/hana-overview-high-availability-disaster-recovery/image9-remount-data-volumes.png)

6. Wybierz opcje odzyskiwania w ramach SAP HANA Studio, jeśli nie automatycznie pochodzą po ponownym tooHANA bazy danych za pomocą programu SAP HANA Studio. Witaj poniższy przykład przedstawia przywracania toohello ostatniego HANA migawki. Jeśli przywracasz toohello najnowszych magazynu migawek, należy hello najnowszych HANA migawki i Migawka magazynu osadza jedną migawkę HANA. (Jeśli przywracasz tooolder magazynu migawek, należy toolocate hello HANA oparte na powitania czasu hello pamięci masowej migawki migawki.)

 ![Wybierz opcje odzyskiwania w ramach SAP HANA Studio](./media/hana-overview-high-availability-disaster-recovery/image10-recover-options-a.png)

7. Wybierz **Odzyskaj hello migawki bazy danych tooa określonych danych kopii zapasowej lub magazynu**.

 ![okno "Określ typ odzyskiwania" Hello](./media/hana-overview-high-availability-disaster-recovery/image11-recover-options-b.png)

8. Wybierz **Określ tworzenia kopii zapasowej bez katalogu**.

 ![okno "Określ lokalizację kopii zapasowej" Hello](./media/hana-overview-high-availability-disaster-recovery/image12-recover-options-c.png)

9. W hello **typ docelowy** listy, wybierz **migawki**.

 ![okno "Określ hello kopii zapasowej tooRecover" Hello](./media/hana-overview-high-availability-disaster-recovery/image13-recover-options-d.png)

10. Kliknij przycisk **Zakończ** proces odzyskiwania hello toostart.

 ![Kliknij przycisk "Zakończ", proces odzyskiwania hello toostart](./media/hana-overview-high-availability-disaster-recovery/image14-recover-options-e.png)

11. bazy danych HANA Hello jest przywracany i odzyskać toohello HANA migawki, która znajduje się w hello pamięci masowej migawki.

 ![Baza danych HANA jest toohello przywrócona i odzyskane HANA migawki](./media/hana-overview-high-availability-disaster-recovery/image15-recover-options-f.png)

### <a name="recovering-toohello-most-recent-state"></a>Odzyskiwanie stanu ostatniej toohello

Witaj następujący proces przywraca hello HANA migawki, która znajduje się w hello pamięci masowej migawki. Przywraca następnie hello transakcji dziennika kopii zapasowych toohello ostatniego stanu hello bazy danych przed przywróceniem hello pamięci masowej migawki.

>[!IMPORTANT]
>Przed kontynuowaniem upewnij się, że masz pełne, jak i ciągłe łańcuch kopii zapasowej dziennika transakcji. Bez tych kopii zapasowych nie można przywrócić bieżącego stanu hello hello bazy danych.

1. Wykonaj kroki 1 – 6 hello poprzedzające procedury "Odzyskiwanie toohello najnowszych HANA migawki."

2. Wybierz **odzyskać stan ostatniej hello bazy danych tooits**.

 ![Wybierz opcję "Odzyskać stan ostatniej tooits hello bazy danych"](./media/hana-overview-high-availability-disaster-recovery/image16-recover-database-a.png)

3. Określ lokalizację hello kopie zapasowe hello najnowszych HANA dziennika. Lokalizacja Hello musi toocontain wszystkie HANA kopie zapasowe dziennika transakcji z stan ostatniej toohello hello HANA migawki.

 ![Określ lokalizację hello kopie zapasowe hello najnowszych HANA dzienników](./media/hana-overview-high-availability-disaster-recovery/image17-recover-database-b.png)

4. Wybierz kopię zapasową jako podstawa z hello toorecover bazy danych. W naszym przykładzie jest to hello HANA migawki, która została uwzględniona w hello pamięci masowej migawki. (Tylko jedna migawka znajduje się w powitania po zrzut ekranu).

 ![Wybierz kopię zapasową jako podstawa z bazy danych hello toorecover](./media/hana-overview-high-availability-disaster-recovery/image18-recover-database-c.png)

5. Wyczyść hello **kopii zapasowych Delta użyj** pole wyboru, jeśli nie istnieją różnice między czasem hello hello HANA migawki i stan ostatniej hello.

 ![Witaj wyczyść pole wyboru "Użyj różnicowe kopie zapasowe" Jeśli nie istnieją żadne delty](./media/hana-overview-high-availability-disaster-recovery/image19-recover-database-d.png)

6. Na ekranie Podsumowanie powitania kliknij **Zakończ** procedury przywracania hello toostart.

 ![Na ekranie Podsumowanie powitania kliknij przycisk "Zakończ"](./media/hana-overview-high-availability-disaster-recovery/image20-recover-database-e.png)

### <a name="recovering-tooanother-point-in-time"></a>Odzyskiwanie tooanother punktu w czasie
toorecover tooa punktu w czasie między migawki HANA hello (dołączone do migawki magazynu hello) i jedną, która jest nowsza niż hello HANA migawki odzyskiwania w momencie hello następujące:

1. Upewnij się, że wszystkie kopie zapasowe dziennika transakcji z ma toorecover hello HANA migawki toohello czasu.
2. Rozpocznij procedurę hello w obszarze "Stan ostatniej odzyskiwanie toohello."
3. W kroku 2 procedury hello w hello **typu odzyskiwania określ** wybierz **Odzyskaj hello bazy danych toohello następujące punktu w czasie**Określ hello punktu w czasie, a następnie wykonaj kroki od 3 do 6.

## <a name="monitoring-hello-execution-of-snapshots"></a>Monitorowanie hello wykonywania migawek

Konieczne jest wykonanie hello toomonitor magazynu migawek. Witaj skrypt, który wykonuje migawkę magazynu zapisuje plik wyjściowy tooa, a następnie zapisuje on toohello tej samej lokalizacji co skryptów języka Perl hello. Oddzielny plik jest przeznaczony dla każdej migawki. dane wyjściowe każdego pliku Hello jasno wskazuje hello różnych faz, które wykonuje hello migawki skryptu:

- Znajdowanie hello woluminów, które wymagają toocreate migawki
- Znajdowanie migawki hello pobranych z tych woluminów
- Usuwanie ewentualne istniejące migawki toomatch hello liczby migawek określona
- Tworzenie migawek HANA
- Utworzenie migawki magazynu hello za pośrednictwem hello woluminów
- Usunięcie migawki HANA hello
- Zmiana nazwy hello najnowszych migawki zbyt**.0**

Witaj najważniejszy element skryptu hello są następujące:
```
**********************Creating HANA snapshot**********************
Creating hello HANA snapshot with command: "./hdbsql -n localhost -i 01 -U SCADMIN01 "backup data create snapshot"" ...
HANA snapshot created successfully.
**********************Creating Storage snapshot**********************
Taking snapshot hourly.recent for hana_data_lhanad01_t020_vol ...
Snapshot created successfully.
Taking snapshot hourly.recent for hana_log_backup_lhanad01_t020_vol ...
Snapshot created successfully.
Taking snapshot hourly.recent for hana_log_lhanad01_t020_vol ...
Snapshot created successfully.
Taking snapshot hourly.recent for hana_shared_lhanad01_t020_vol ...
Snapshot created successfully.
Taking snapshot hourly.recent for sapmnt_lhanad01_t020_vol ...
Snapshot created successfully.
**********************Deleting HANA snapshot**********************
Deleting hello HANA snapshot with command: "./hdbsql -n localhost -i 01 -U SCADMIN01 "backup data drop snapshot"" ...
HANA snapshot deletion successfully.
```
W tym przykładzie widać, jak rekordy skryptu hello hello tworzenia migawki HANA hello. W przypadku skalowania w poziomie hello ten proces jest inicjowana na powitania węzła głównego. węzeł główny Hello inicjuje hello synchroniczne tworzenie migawek hello na każdym z węzłów procesu roboczego hello. Następnie hello pamięci masowej migawki. Po pomyślnym wykonaniu hello hello magazynu migawek hello HANA migawka jest usuwana.
