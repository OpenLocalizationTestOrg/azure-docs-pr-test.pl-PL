---
title: "Omówienie rozwiązania serii aaaStorSimple 8000 | Dokumentacja firmy Microsoft"
description: "W tym artykule opisano obsługę poziomów StorSimple, urządzenia hello urządzenia wirtualnego, usług i zarządzania magazynem i wprowadza kluczowe terminy używane w StorSimple."
services: storsimple
documentationcenter: NA
author: SharS
manager: timlt
editor: 
ms.assetid: 7144d218-db21-4495-88fb-e3b24bbe45d1
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 07/10/2017
ms.author: v-sharos@microsoft.com
ms.openlocfilehash: 0891841186dcd4c46f48d13ed829b98fab7bdf67
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="storsimple-8000-series-a-hybrid-cloud-storage-solution"></a>Z serii StorSimple 8000: rozwiązania magazynu hybrydowego chmury
## <a name="overview"></a>Omówienie
Zapraszamy tooMicrosoft Azure StorSimple, zintegrowane pamięci masowej zarządzanego zadań magazynu między urządzeniami lokalnymi i magazynu w chmurze Microsoft Azure. StorSimple to rozwiązanie sieci SAN obszaru wydajne, ekonomiczne i łatwością zarządzać magazynu, które eliminuje wiele problemów hello i koszty związane z ochroną magazyn i dane przedsiębiorstwa. Go używa urządzenia serii StorSimple 8000 zastrzeżonych hello integruje się z usługami w chmurze i udostępnia zestaw narzędzi do zarządzania dla bezproblemowego widoku wszystkie magazynu przedsiębiorstwa, w tym magazynie w chmurze. (hello StorSimple informacje na temat wdrażania publikowane w witrynie sieci Web Microsoft Azure hello dotyczy tooStorSimple 8000 serii tylko urządzenia. Jeśli używasz urządzenia z serii StorSimple 5000/7000, przejdź zbyt[pomocy StorSimple](http://onlinehelp.storsimple.com/).)

Używa StorSimple [warstwy magazynowania](#automatic-storage-tiering) toomanage przechowywanych danych na różnych nośnikach magazynowania. Bieżący zestaw roboczy Hello jest przechowywanego lokalnie na dyskach półprzewodnikowych (SSD), rzadziej używane dane są przechowywane na dyskach twardych (HDD) i dane archiwalne spoczywa toohello chmury. Ponadto StorSimple używa deduplikacji i korzysta z kompresji tooreduce hello ilość pamięci, która hello danych. Aby uzyskać więcej informacji, przejdź zbyt[kompresji i deduplikacji](#deduplication-and-compression). Definicje inne kluczowe terminy i pojęcia używane w dokumentacji serii StorSimple 8000 hello Przejdź zbyt[terminologii StorSimple](#storsimple-terminology) na końcu hello w tym artykule.

Ponadto zarządzanie toostorage funkcji ochrony danych StorSimple włączyć możesz toocreate na żądanie i zaplanowanych kopii zapasowych, a następnie magazynu, który je lokalnie lub w hello w chmurze. Kopie zapasowe są pobierane w formie hello przyrostowe migawki, co oznacza, że można je utworzyć i szybko przywrócić. Migawki w chmurze może być bardzo ważny w scenariuszach odzyskiwania po awarii, ponieważ zastąpić systemy dodatkowej magazynu (na przykład kopii zapasowej na taśmie) i umożliwić toorestore danych tooyour centrum danych lub tooalternate witryn w razie potrzeby.

![ikona wideo](./media/storsimple-overview/video_icon.png) Obejrzyj film hello na szybkie wprowadzenie tooMicrosoft Azure StorSimple.

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/StorSimple-Hybrid-Cloud-Storage-Solution/player]

## <a name="why-use-storsimple"></a>Dlaczego warto używać StorSimple?
Witaj poniższej tabeli opisano niektóre najważniejsze zalety hello, dostępnych w Microsoft Azure StorSimple.

| Funkcja | Korzyść |
| --- | --- |
| Integracja przezroczyste |Używa protokołu iSCSI hello tooinvisibly urządzeń magazynu danych łącza. To zapewnia, że danych przechowywanych w chmurze hello, w centrum danych hello, lub na serwerach zdalnych pojawia się toobe przechowywane w jednym miejscu. |
| Magazyn zmniejszenie kosztów |Przydziela wystarczające lokalnej lub bieżące wymagania związane z przechowywaniem toomeet w chmurze i rozszerza magazynu w chmurze tylko wtedy, gdy jest to konieczne. Dodatkowo zmniejsza wymagania dotyczące magazynu i kosztów przez wyeliminowanie nadmiarowe wersje hello tych samych danych (deduplikacji) i przy użyciu kompresji. |
| Uproszczone zarządzanie magazynem |Udostępnia tooconfigure narzędzi administracyjnych systemu i zarządzanie nimi dane przechowywane lokalnie, na zdalnym serwerze i w chmurze hello. Ponadto można zarządzać kopii zapasowej i przywracanie z przystawką Microsoft Management Console (MMC).|
| Ulepszonych funkcji odzyskiwania i zgodność |Nie wymaga godzina rozszerzoną odzyskiwania. Zamiast tego należy go przywraca dane, jest wymagana. Oznacza to, że minimalnego przerw w działaniu można kontynuować wykonywania normalnych operacji. Ponadto można skonfigurować harmonogramy tworzenia kopii zapasowej toospecify zasad i przechowywania danych. |
| Przenoszenia danych |Dane przekazane tooMicrosoft chmury Azure, które usługi są dostępne z innych witryn do celów odzyskiwania i migracji. Ponadto można użyć urządzenia chmury StorSimple tooconfigure StorSimple na maszynach wirtualnych (VM) działają na platformie Microsoft Azure. Witaj maszyn wirtualnych może następnie używać urządzeń wirtualnych tooaccess przechowywanych danych do celów testu lub odzyskiwania. |
| Ciągłość działalności biznesowej |Umożliwia urządzeniu serii StorSimple 8000 tooa danych toomigrate użytkowników serii 5000 7000 StorSimple. |
| Dostępność w hello Portal Azure dla instytucji rządowych |StorSimple jest dostępna w hello Portal Azure dla instytucji rządowych. Aby uzyskać więcej informacji, zobacz [wdrażanie lokalnego urządzenia StorSimple w hello Portal dla instytucji rządowych](storsimple-8000-deployment-walkthrough-gov-u2.md). |
| Ochrona danych i dostępność |Witaj z serii StorSimple 8000 obsługuje strefy nadmiarowego magazynu (ZRS), w tooLocally dodanie magazyn geograficznie nadmiarowy (LRS) i magazynu geograficznie nadmiarowego (GRS). Odwołuje się zbyt[w tym artykule na temat usługi Azure Storage nadmiarowość opcji](https://azure.microsoft.com/documentation/articles/storage-redundancy/) szczegółowe ZRS. |
| Obsługa kluczowych aplikacji |StorSimple umożliwia identyfikowanie odpowiednich woluminów, co przypięty lokalnie zapewnia który z kolei, że dane wymagane przez aplikacje krytyczne nie jest toohello warstwowych chmury. Woluminów przypiętych lokalnie nie są opóźnienia toocloud podmiotu lub problemów z łącznością. Aby uzyskać więcej informacji na temat woluminów przypiętych lokalnie, zobacz [korzysta z woluminów toomanage usługi Menedżer StorSimple urządzenia hello](storsimple-8000-manage-volumes-u2.md). |
| Małe opóźnienia i wysokiej wydajności |Można utworzyć chmury urządzenia, które korzystają z hello wysoka wydajność, małe opóźnienia funkcji magazynu Azure premium. Aby uzyskać więcej informacji na temat StorSimple premium chmury urządzenia, zobacz [wdrażanie i zarządzanie nimi urządzenia StorSimple chmury Azure](storsimple-8000-cloud-appliance-u2.md). |


## <a name="storsimple-components"></a>Składniki StorSimple
Witaj rozwiązania Microsoft Azure StorSimple obejmuje hello następujące składniki:

* **Microsoft Azure StorSimple urządzenia** — lokalnej tablicy magazynu hybrydowego zawierający dyski SSD i dysków twardych, wraz z nadmiarowe kontrolery i funkcji automatycznej pracy awaryjnej. Witaj kontrolerów zarządzania magazynem warstwy, umieszczania aktualnie używane (lub gorących) danych w magazynie lokalnym (w hello urządzenia lub lokalnych serwerów), podczas przenoszenia toohello rzadziej używanych danych w chmurze.
* **Urządzenia chmury StorSimple** — znanej także jako hello urządzenie wirtualne StorSimple, jest wersję oprogramowania hello urządzenia StorSimple, który replikuje architektura hello i większość możliwości urządzenia magazynu fizycznego hybrydowego hello. Witaj urządzenia chmury StorSimple działa w jednym węźle w maszynie wirtualnej platformy Azure. Urządzeń wirtualnych Premium, których skorzystać z magazynu Azure premium, są dostępne w wersji Update 2 lub nowszy.
* **Usługa Menedżera urządzeń StorSimple** — jako rozszerzenie hello portal Azure, który umożliwia zarządzanie za pomocą jednej sieci web interfejsu urządzenia StorSimple lub urządzenia do chmury StorSimple. Można użyć toocreate usługi Menedżer StorSimple urządzenia hello i zarządzania usługami, wyświetlać i zarządzać urządzeniami, wyświetlać alerty, zarządzanie woluminami i wyświetlić i zarządzanie zasadami tworzenia kopii zapasowej i hello katalogu kopii zapasowej.
* **Program Windows PowerShell dla StorSimple** — interfejsu wiersza polecenia, których można używać toomanage hello urządzenia StorSimple. Program Windows PowerShell dla StorSimple zawiera funkcje, które pozwalają tooregister urządzenia StorSimple, skonfiguruj interfejs sieciowy hello na urządzeniu zainstalować niektórych typów aktualizacji, rozwiązywania problemów z urządzeniem, uzyskując dostęp do sesji pomocy technicznej hello i zmienić hello Stan urządzenia. Połączenia konsoli szeregowej toohello lub przy użyciu komunikacji zdalnej programu Windows PowerShell miały dostęp do programu Windows PowerShell dla StorSimple.
* **Polecenia cmdlet systemu Azure PowerShell StorSimple** — zbiór poleceń cmdlet programu Windows PowerShell, które pozwalają tooautomate poziomu usługi oraz zadania migracji z wiersza polecenia hello. Aby uzyskać więcej informacji na temat hello poleceń cmdlet programu Azure PowerShell dla urządzenia StorSimple Przejdź toohello [dokumentacji poleceń cmdlet](/powershell/module/azure/?view=azuresmps-3.7.0#azure).
* **StorSimple Snapshot Manager** — przystawki programu MMC, korzysta z grup woluminu i kopii zapasowych spójnych z aplikacją toogenerate usługi kopiowania woluminów w tle Windows hello. Ponadto można użyć programu StorSimple Snapshot Manager toocreate harmonogramy tworzenia kopii zapasowej i w klonowania lub Przywracanie woluminów.
* **Karta StorSimple dla programu SharePoint** — narzędzie, rozszerzający niewidocznie Microsoft Azure StorSimple magazynu i ochronę danych farm serwerów tooSharePoint, podczas tworzenia magazynu StorSimple można przeglądać i łatwiejsze w zarządzaniu z hello centralna programu SharePoint Portalu administracyjnego.

Poniższy diagram Hello zawiera ogólny widok hello Microsoft Azure StorSimple architektury i składników.

![Architektura StorSimple](./media/storsimple-overview/overview-big-picture.png)

Witaj poniższych sekcjach opisano każdy z tych składników bardziej szczegółowo i wyjaśniono sposób rozwiązania hello rozmieszcza danych przydziela magazynu i ułatwia zarządzanie magazynami i ochrony danych. Ostatnia sekcja Hello zawiera definicje dla niektórych hello ważne terminy i pojęcia tooStorSimple pokrewne składniki oraz zarządzania nimi.

## <a name="storsimple-device"></a>Urządzenia StorSimple
urządzenia Microsoft Azure StorSimple Hello jest tablicą magazynu hybrydowego lokalnymi, zapewniający podstawowego magazynu i zapisaniu na nim toodata dostępu iSCSI. Zarządza komunikacją z magazynu w chmurze i pomaga tooensure hello zabezpieczeń i poufności wszystkich danych przechowywanych na powitania rozwiązania Microsoft Azure StorSimple.

urządzenia StorSimple Hello zawiera dyski SSD i HDD dyski twarde, a także obsługę klastrowania i automatycznej pracy awaryjnej. Zawiera on procesora udostępnionego, Magazyn udostępniony i dwa kontrolery dublowany. Każdy kontroler zawiera następujące hello:

* Komputer hosta tooa połączenia
* Zapasowej toosix sieci porty tooconnect toohello sieci lokalnej (LAN)
* Monitorowanie sprzętu
* Pamięci RAM non-volatile (NVRAM), który zachowuje informacje, nawet jeśli zasilania zostało przerwane
* Typu cluster-aware aktualizowania toomanage aktualizacje oprogramowania na serwerach w klastrze trybu failover, dzięki czemu hello aktualizacje mają minimalnego lub nie mają wpływu na dostępność usługi
* Usługa klastrowania, który działa podobnie jak klaster zaplecza, wysokiej dostępności oraz minimalizując niepożądanych, które mogą wystąpić, jeśli dysk twardy lub dysk SSD ulegnie awarii lub zostanie przełączony w tryb offline

Tylko jeden kontroler jest aktywny w dowolnym momencie w czasie. W przypadku niepowodzenia hello aktywnym kontrolerze hello drugiego kontrolera automatycznie staje się aktywny.

Aby uzyskać więcej informacji, przejdź zbyt[StorSimple składniki sprzętowe i stan](storsimple-8000-monitor-hardware-status.md).

## <a name="storsimple-cloud-appliance"></a>Urządzenie StorSimple w chmurze
Możesz użyć toocreate StorSimple urządzenia chmury, replikowane hello architektury i możliwościami urządzenia magazynu fizycznego hybrydowego hello. Hello urządzenia chmury StorSimple (znanej także jako hello urządzenie wirtualne StorSimple) jest uruchamiany w jednym węźle w maszynie wirtualnej platformy Azure. (Urządzenia chmury można tworzyć tylko na maszynie wirtualnej platformy Azure. Nie można utworzyć na urządzeniu StorSimple lub serwera lokalnego.)

urządzenia chmury Hello ma hello następujące funkcje:

* Zachowuje się jak urządzenia fizycznego, a mogą oferować iSCSI maszyny toovirtual interfejsu w chmurze hello.
* Można utworzyć nieograniczoną liczbę urządzeń chmury w chmurze hello i włączyć je włączać i wyłączać zgodnie z potrzebami.
* Mogą pomóc symulowania środowisk lokalnego odzyskiwania po awarii, rozwoju i scenariusze testowania i może pomóc w poziomie elementu pobierania z kopii zapasowych.

Witaj urządzenia chmury StorSimple jest dostępny w dwóch modeli: urządzenie hello 8010 (wcześniej znane jako model hello 1100) i urządzenia hello 8020. Witaj urządzenie 8010 ma maksymalnej pojemności 30 TB. urządzenie 8020 Hello, który korzysta z magazynu Azure premium, ma maksymalną pojemność 64 TB. (W warstwach lokalnych magazynu Azure premium przechowuje dane na dyskach SSD należy magazynu w warstwie standardowa przechowuje dane na dyskach HDD.) Należy pamiętać, że użytkownik musi mieć Azure premium magazynu konta toouse magazyn w warstwie premium. Aby uzyskać więcej informacji na temat magazyn w warstwie premium, przejdź zbyt[magazyn w warstwie Premium: magazyn o wysokiej wydajności dla obciążeń maszyny wirtualnej Azure](../storage/common/storage-premium-storage.md).

Aby uzyskać więcej informacji na temat hello urządzenia chmury StorSimple Przejdź zbyt[wdrażanie i zarządzanie nimi urządzenia StorSimple chmury Azure](storsimple-8000-cloud-appliance-u2.md).

## <a name="storsimple-device-manager-service"></a>Usługa menedżera urządzenia StorSimple
Microsoft Azure StorSimple udostępnia interfejs użytkownika sieci web (hello usługi Menedżer StorSimple urządzenia), umożliwiającą toocentrally zarządzania Centrum danych i magazynu w chmurze. Program hello Menedżera urządzeń StorSimple usługi tooperform hello następujące zadania:

* Skonfiguruj ustawienia systemu dla urządzenia StorSimple.
* Konfigurowanie i zarządzanie ustawieniami zabezpieczeń urządzenia StorSimple.
* Konfigurowanie poświadczeń w chmurze i właściwości.
* Konfigurowanie i zarządzanie nimi woluminów na serwerze.
* Konfigurowanie grup woluminu.
* Tworzenie kopii zapasowej i przywracania danych.
* Monitorowanie wydajności.
* Przejrzyj ustawienia systemu i identyfikowania potencjalnych problemów.

Możesz użyć tooperform usługi Menedżer StorSimple urządzenia hello wszystkich zadań administracyjnych, z wyjątkiem tych, które wymagają systemu czasie, takiej jak początkowej konfiguracji i instalację aktualizacji.

Aby uzyskać więcej informacji, przejdź zbyt[Użyj hello tooadminister usługi Menedżera urządzeń StorSimple, urządzenia StorSimple](storsimple-8000-manager-service-administration.md).

## <a name="windows-powershell-for-storsimple"></a>Program Windows PowerShell dla StorSimple
Program Windows PowerShell dla StorSimple udostępnia interfejs wiersza polecenia, że można użyć toocreate i zarządzanie usługą Microsoft Azure StorSimple hello i skonfigurować i monitorować urządzenia StorSimple. Jest oparte na środowisku Windows PowerShell, interfejsu wiersza polecenia, zawierającą dedykowanych polecenia cmdlet do zarządzania urządzeniem StorSimple. Program Windows PowerShell dla StorSimple zawiera funkcje, które pozwalają na:

* Zarejestruj urządzenie.
* Skonfiguruj interfejs sieciowy hello na urządzeniu.
* Zainstalować niektórych typów aktualizacji.
* Po zalogowaniu się do sesji pomocy technicznej hello rozwiązywania problemów z urządzeniem.
* Zmienianie stanu urządzenia hello.

Środowisko Windows PowerShell dla urządzenia StorSimple można korzystać z konsoli szeregowej (na hoście, komputer połączony bezpośrednio urządzenia toohello) lub zdalnie przy użyciu komunikacji zdalnej programu Windows PowerShell. Należy pamiętać, że niektóre środowiska Windows PowerShell dla StorSimple zadania, takie jak Rejestracja wstępna urządzenia jest możliwe tylko na konsoli szeregowej hello.

Aby uzyskać więcej informacji, przejdź zbyt[Użyj środowiska Windows PowerShell dla StorSimple tooadminister urządzenia](storsimple-8000-windows-powershell-administration.md).

## <a name="azure-powershell-storsimple-cmdlets"></a>Polecenia cmdlet programu PowerShell StorSimple systemu Azure
polecenia cmdlet programu Azure PowerShell StorSimple Hello są zbiór poleceń cmdlet programu Windows PowerShell, które umożliwiają tooautomate poziomu usługi i zadania migracji z wiersza polecenia hello. Aby uzyskać więcej informacji na temat hello poleceń cmdlet programu Azure PowerShell dla urządzenia StorSimple Przejdź toohello [dokumentacji poleceń cmdlet](/powershell/module/azure/?view=azuresmps-3.7.0).

## <a name="storsimple-snapshot-manager"></a>StorSimple Snapshot Manager
StorSimple Snapshot Manager jest przystawki programu Microsoft Management Console (MMC) służy toocreate spójny, w momencie kopii lokalnej i w chmurze danych. Przystawka Hello działa na hoście z systemem Windows Server. Można użyć programu StorSimple Snapshot Manager do:

* Konfigurowanie, tworzenie kopii zapasowej i usuwanie woluminów.
* Skonfiguruj wolumin tooensure grupy, którego kopię zapasową danych jest spójne z aplikacjami.
* Zarządzanie zasad tworzenia kopii zapasowych, tak aby dane kopii zapasowej na uprzednio określonym harmonogramem i przechowywane w wyznaczonym lokalizacji (lokalnie lub w chmurze hello).
* Przywracanie woluminów i poszczególnych plików.

Kopie zapasowe są przechwytywane jako migawki, które rejestrowania tylko hello zmian, ponieważ została wykonana ostatnia migawka hello i wymaga znacznie mniej miejsca niż pełne kopie zapasowe. Można utworzyć harmonogramy tworzenia kopii zapasowej lub korzystać z bezpośrednim kopii zapasowych zgodnie z potrzebami. Ponadto można użyć zasad przechowywania tooestablish StorSimple Snapshot Manager tego formantu, ile migawki zostaną zapisane. Jeśli później konieczne toorestore dane z kopii zapasowej, umożliwia StorSimple Snapshot Manager wybierz z wykazu hello lokalnych lub migawki w chmurze. 

W przypadku katastrofy lub poważnej awarii lub jeśli potrzebujesz toorestore danych z innego powodu, StorSimple Snapshot Manager przywracania go przyrostowo jest wymagana. Przywracanie danych nie wymaga zamknąć hello całego systemu podczas przywrócić plik, zastępowanie sprzętu lub przenieść operacje tooanother lokacji.

Aby uzyskać więcej informacji, przejdź zbyt[co to jest StorSimple Snapshot Manager?](storsimple-what-is-snapshot-manager.md)

## <a name="storsimple-adapter-for-sharepoint"></a>Adapter usługi StorSimple dla programu SharePoint
Microsoft Azure StorSimple obejmuje hello karty StorSimple dla programu SharePoint, opcjonalny składnik, rozszerzający niewidocznie StorSimple magazynu i ochronę danych farm serwerów tooSharePoint funkcji. Karta Hello współpracuje z dostawcy zdalnego magazynu obiektów Blob (SPZ) i funkcja SQL Server SPZ hello, dzięki czemu możesz toomove obiekty BLOB tooa serwera kopii zapasowej przez system Microsoft Azure StorSimple hello. Microsoft Azure StorSimple następnie przechowuje dane obiektów BLOB hello lokalnie lub w chmurze hello na podstawie użycia.

Witaj karty StorSimple dla programu SharePoint są obsługiwane w systemie hello Administracja centralna programu SharePoint portalu. W rezultacie pozostanie scentralizowanego zarządzania programu SharePoint, a wszystkie magazyny wyświetlane toobe w farmie programu SharePoint hello.

Aby uzyskać więcej informacji, przejdź zbyt[karty StorSimple dla programu SharePoint](storsimple-adapter-for-sharepoint.md). 

## <a name="storage-management-technologies"></a>Technologie magazynowania zarządzania
Ponadto toohello dedykowane urządzenia StorSimple, urządzenie wirtualne i inne składniki, Microsoft Azure StorSimple używa hello następującego oprogramowania technologii tooprovide szybki dostęp toodata i tooreduce użycia magazynu:

* [Warstwy magazynowania automatyczne](#automatic-storage-tiering) 
* [Alokowanie elastyczne](#thin-provisioning) 
* [Na potrzeby deduplikacji i kompresji](#deduplication-and-compression) 

### <a name="automatic-storage-tiering"></a>Warstwy magazynowania automatyczne
Microsoft Azure StorSimple automatycznie rozmieszcza danych w warstwach logiczną na podstawie bieżącego użycia, wieku i dane tooother relacji. Dane, które są najbardziej aktywnych jest przechowywany lokalnie, natomiast mniej aktywne i nieaktywne dane są automatycznie migrowane toohello chmury. powitania po diagram ilustruje takie podejście magazynu.

![Warstwy magazynowania StorSimple](./media/storsimple-overview/hcs-data-services-storsimple-components-tiers.png)

tooenable szybki dostęp StorSimple przechowuje bardzo aktywnych danych (gorących danych) na dyskach SSD w hello urządzenia StorSimple. Przechowuje dane, które jest czasami używana (ogrzewać danych) na dysków twardych w urządzeniu hello lub na serwerach w hello centrum danych. Powoduje przeniesienie nieaktywnych, dane kopii zapasowej, a dane przechowywane przez archiwizacji lub zgodności celów toohello chmury. 

> [!NOTE]
> W wersji Update 2 lub nowszym można określić wolumin przypięty lokalnie, w takim przypadku hello danych pozostaje na urządzeniu lokalne powitania, a nie do warstwy toohello chmury. 


StorSimple można dostosować i Reorganizuje dane i zmień przydziałów magazynowania jako wzorców użycia. Na przykład niektóre informacje mogą stać się mniej aktywne w czasie. Ponieważ staje się stopniowo mniej aktywne, jest migrowana z tooHDDs dysków SSD, a następnie toohello chmury. Jeśli tego samego danych stanie się ponownie aktywna, to urządzenie magazynujące migrowanych toohello Wstecz.

proces warstw magazynu Hello przebiega w następujący sposób:

1. Administrator systemu konfiguruje konto magazynu w chmurze Microsoft Azure.
2. Hello administrator używa hello serial konsoli i hello Menedżera urządzeń StorSimple usługi (uruchomionej w hello portalu Azure) tooconfigure hello urządzenie i plik serwera, tworzenie zasad ochrony woluminy i dane. Maszyny lokalnej (na przykład serwery plików) używają urządzenia StorSimple hello hello Internet Small Computer System Interface (iSCSI) tooaccess.
3. Początkowo StorSimple przechowuje dane na powitania szybkiego warstwy dysków SSD hello urządzenia.
4. Jako hello pojemności podejścia do warstwy dysków SSD StorSimple deduplicates kompresuje hello najstarsze bloki danych i przenosi je warstwy dysków HDD toohello.
5. Jako hello pojemność podejścia do warstwy dysków HDD StorSimple szyfruje bloki danych najstarsze hello i wysyła je bezpiecznie toohello konta magazynu Microsoft Azure za pośrednictwem protokołu HTTPS.
6. Microsoft Azure tworzy wiele replik hello danych w swoim centrum danych i zdalnego centrum danych, zapewniając, że w przypadku awarii można odzyskać dane hello.
7. Gdy serwer plików hello żąda danych przechowywanych w chmurze hello, StorSimple zwraca go bezproblemowo i przechowywanie kopii na powitania warstwy dysków SSD hello urządzenia StorSimple.

#### <a name="how-storsimple-manages-cloud-data"></a>Jak StorSimple zarządza danych w chmurze

StorSimple deduplicates danych klienta we wszystkich migawek hello i hello głównej danych (napisane przez hostów). Podczas deduplikacji jest doskonały dla wydajność magazynu, ułatwia hello pytanie "co to jest w chmurze hello" skomplikowane. Witaj warstwowych danych podstawowych i dane migawki hello nakładają się na siebie. Pojedynczy fragmentów danych w chmurze hello mogą być użyte jako warstwowych danych podstawowych i się też odwoływać linie kilka migawki. Każdy migawka w chmurze zapewnia, że kopię wszystkich danych w chwili hello jest zablokowany w chmurze hello, aż do usunięcia tej migawki.

Danych jest tylko usunąć z chmury hello, gdy nie są żadne dane toothat odwołania. Na przykład, jeśli traktujemy migawkę chmury wszystkie dane hello, który znajduje się w urządzeniu StorSimple hello, a następnie usuń niektóre podstawowe dane będą widzimy hello _danych podstawowych_ porzucić natychmiast. Witaj _danych w chmurze_ w tym hello warstwowych dane i hello kopii zapasowych, pozostaje hello takie same. Jest tak, ponieważ nadal odwołuje się do danych w chmurze hello migawki. Po chmurze hello migawka jest usuwana (i innych migawki, która odwołuje się do hello tych samych danych) w chmurze porzucania zużycia. Przed usuwamy danych w chmurze, sprawdzamy, czy nie migawki nadal odwołują się dane. Ten proces jest nazywany _wyrzucanie elementów bezużytecznych_ i działa usługa tła na powitania urządzenia. Usunięcie danych w chmurze nie jest bezpośrednim, ponieważ usługa kolekcji garbage hello sprawdza inne odwołania toothat danych przed usunięciem hello. hello całkowitej liczby migawek i hello łączna ilość danych zależy od szybkości Hello operacji wyrzucania elementów bezużytecznych. Zazwyczaj danych w chmurze hello jest czyszczona w mniej niż tydzień.


### <a name="thin-provisioning"></a>Alokowanie elastyczne
Alokowanie elastyczne jest technologii wirtualizacji, w której dostępny magazyn pojawia się tooexceed zasobów fizycznych. Zamiast z wyprzedzeniem rezerwowania wystarczającej ilości miejsca, StorSimple używa alokowania tooallocate inicjowania obsługi administracyjnej wystarczającego miejsca toomeet bieżące wymagania. Hello elastycznej rodzaj magazynu w chmurze ułatwia takie podejście, ponieważ StorSimple można zwiększyć lub zmniejszyć chmury magazynu toomeet zmieniających się potrzeb.

> [!NOTE]
> Woluminów przypiętych lokalnie nie są alokowane udostępnione. Magazyn przydzielony tooa tylko lokalne woluminu jest obsługiwana w całości, podczas tworzenia woluminu hello.


### <a name="deduplication-and-compression"></a>Na potrzeby deduplikacji i kompresji
Microsoft Azure StorSimple używa deduplikacji i toofurther kompresji danych zmniejszyć wymagania dotyczące magazynu.

Deduplikacji zmniejsza hello ogólną ilość danych przechowywanych przez wyeliminowanie nadmiarowości w zestawie danych hello przechowywane. Informacje zmian, StorSimple ignoruje hello bez zmian danych i przechwytywania hello tylko zmiany. Ponadto StorSimple zmniejsza hello ilość przechowywanych danych identyfikowanie i usuwanie niepotrzebnych informacji. 

> [!NOTE]
> Dane dotyczące woluminów przypiętych lokalnie nie jest deduplikowany lub skompresowane. Jednak kopii zapasowych woluminów przypiętych lokalnie jest deduplikowany i skompresowane.


## <a name="storsimple-workload-summary"></a>Podsumowanie obciążenia StorSimple
Podsumowanie obciążenia StorSimple hello obsługiwane są przedstawione w poniższej tabeli.

| Scenariusz | Obciążenie | Obsługiwane | Ograniczenia | Wersja |
| --- | --- | --- | --- | --- |
| Współpraca |Udostępnianie plików |Tak | |Wszystkie wersje |
| Współpraca |Udostępnianie plików rozproszonych |Tak | |Wszystkie wersje |
| Współpraca |Sharepoint |Tak* |Obsługiwane tylko w przypadku woluminów przypiętych lokalnie |Aktualizacja 2 lub nowszej |
| Archiwizacja |Archiwizowanie pliku prostego |Tak | |Wszystkie wersje |
| Wirtualizacja |Maszyny wirtualne |Tak* |Obsługiwane tylko w przypadku woluminów przypiętych lokalnie |Aktualizacja 2 lub nowszej |
| Database (Baza danych) |SQL |Tak* |Obsługiwane tylko w przypadku woluminów przypiętych lokalnie |Aktualizacja 2 lub nowszej |
| Monitorowania wideo |Monitorowania wideo |Tak* |Obsługiwane, gdy urządzenie StorSimple jest dedykowany tylko obciążenia toothis |Aktualizacja 2 lub nowszej |
| Tworzenie kopii zapasowych |Podstawowy docelowy kopii zapasowej |Tak* |Obsługiwane, gdy urządzenie StorSimple jest dedykowany tylko obciążenia toothis |Aktualizacja 3 lub nowszym |
| Tworzenie kopii zapasowych |Dodatkowej docelowy kopii zapasowej |Tak* |Obsługiwane, gdy urządzenie StorSimple jest dedykowany tylko obciążenia toothis |Aktualizacja 3 lub nowszym |

*Tak &#42; -Ograniczenia i wskazówki dotyczące rozwiązania powinny być stosowane.*

Witaj następujące obciążenia nie są obsługiwane przez urządzenia z serii StorSimple 8000. Jeśli wdrażana na StorSimple, te obciążenia spowoduje nieobsługiwaną konfiguracją.

* Medyczne imaging
* Exchange
* VDI
* Oracle
* SAP
* Dane Big Data
* Dystrybucja zawartości
* Rozruch z SCSI

Poniżej znajduje się lista składników infrastruktury hello StorSimple obsługiwane.

| Scenariusz | Obciążenie | Obsługiwane | Ograniczenia | Wersja |
| --- | --- | --- | --- | --- |
| Ogólne |ExpressRoute |Tak | |Wszystkie wersje |
| Ogólne |DataCore FC |Tak* |Obsługiwane z DataCore SANsymphony |Wszystkie wersje |
| Ogólne |DFSR |Tak* |Obsługiwane tylko w przypadku woluminów przypiętych lokalnie |Wszystkie wersje |
| Ogólne |Indeksowanie |Tak* |Dla woluminów warstwowych, jest obsługiwane tylko metadane indeksowania (a nie dane).<br>Dla woluminów przypiętych lokalnie pełną indeksowania jest obsługiwane. |Wszystkie wersje |
| Ogólne |Oprogramowanie antywirusowe |Tak* |Dla woluminów warstwowych jest obsługiwane tylko skanowanie podczas otwierania i zamknij.<br> Dla woluminów przypiętych lokalnie pełne skanowanie jest obsługiwane. |Wszystkie wersje |

*Tak &#42; -Ograniczenia i wskazówki dotyczące rozwiązania powinny być stosowane.*

Poniżej znajduje się lista innego oprogramowania, które są używane z rozwiązaniami toobuild StorSimple.

| Typ obciążenia | Oprogramowanie używane z StorSimple | Obsługiwane wersje|Przewodnik toosolution łącza| 
| --- | --- | --- | --- |
| Miejsce docelowe kopii zapasowej |Veeam |V Veeam 9 lub nowszy |[StorSimple jako miejsce docelowe kopii zapasowej z Veaam](storsimple-configure-backup-target-veeam.md)|
| Miejsce docelowe kopii zapasowej |Exec VERITAS kopii zapasowej |Exec kopii zapasowej 16 i nowsze |[StorSimple jako miejsce docelowe kopii zapasowej z kopii zapasowej Exec](storsimple-configure-backup-target-using-backup-exec.md)|
| Miejsce docelowe kopii zapasowej |VERITAS NetBackup |NetBackup 7.7.x i nowsze  |[StorSimple jako miejsce docelowe kopii zapasowej z NetBackup](storsimple-configure-backuptarget-netbackup.md)|
| Udostępnianie plików globalne <br></br> Współpraca |Talon  |[StorSimple z Talon](https://www.talonstorage.com/products/fast-deployment-azure-storsimple) | |

## <a name="storsimple-terminology"></a>Terminologia StorSimple
Przed wdrożeniem rozwiązania Microsoft Azure StorSimple, firma Microsoft zaleca przejrzenie hello następujące warunki.

### <a name="key-terms-and-definitions"></a>Kluczowe terminy i definicje
| Termin (akronim lub skrót) | Opis |
| --- | --- |
| rekord kontroli dostępu (ACR) |Rekord skojarzony z woluminu na urządzenia Microsoft Azure StorSimple, który określa, które hosty mogą się łączyć tooit. Witaj opiera się na powitania iSCSI kwalifikowana nazwa (IQN) hostów hello (zawarte w hello ACR) łączących tooyour urządzenia StorSimple. |
| AES 256 |Algorytm Advanced Encryption (Standard AES) 256-bitowego szyfrowania danych tooand przesyłane z chmury hello. |
| rozmiar jednostki alokacji (AUS) |Witaj najmniejsza ilość miejsca na dysku, które mogą być przydzielone toohold pliku w systemie plików z systemem Windows. Jeśli rozmiar pliku nie jest wielokrotnością rozmiaru klastra hello, dodatkowe miejsce musi być plikiem hello toohold używanych (się toohello dalej wielokrotnością rozmiaru klastra hello) co spowoduje utratę miejsca i fragmentacji dysku twardego hello. <br>Witaj zalecane AUS woluminów Azure StorSimple to 64 KB, ponieważ działa z algorytmami deduplikacji hello. |
| warstwy magazynowania automatycznych |Automatyczne przenoszenie danych mniej aktywne z tooHDDs dysków SSD, a następnie warstwy tooa w chmurze hello, a następnie włączenie zarządzania wszystkie magazyny z interfejsem użytkownika centralnej. |
| Katalog kopii zapasowej |Kolekcja kopii zapasowych, zwykle powiązane według typu aplikacji hello, który został użyty. Ta kolekcja zostanie wyświetlona w bloku katalogu kopii zapasowej hello hello usługi Menedżer StorSimple urządzenia interfejsu użytkownika. |
| Plik kopii zapasowej katalogu |Plik zawierający listę dostępnych migawek przechowywanych obecnie we hello kopii zapasowej bazy danych programu StorSimple Snapshot Manager. |
| zasady tworzenia kopii zapasowej |Wybór woluminów, typ kopii zapasowej i harmonogram, umożliwiająca toocreate kopii zapasowych na wstępnie zdefiniowanego harmonogramu. |
| duże obiekty binarne (BLOB) |Kolekcja przechowywane jako pojedynczej jednostki w system zarządzania bazami danych binarnych. Obiekty BLOB są zwykle obrazy, audio lub inne obiekty multimedialne, chociaż czasami binarnego kodu wykonywalnego są przechowywane jako obiekt BLOB. |
| Protokół uwierzytelniania typu Challenge Handshake (CHAP) |Protokół używany tooauthenticate hello równorzędnego połączenia oparte na równorzędnej hello udostępnianie hasła lub klucza tajnego. Protokół CHAP mogą być jednokierunkowe lub wzajemnego. Za pomocą jednokierunkowego protokołu CHAP docelowy hello uwierzytelnia inicjatora. Wzajemne CHAP wymaga hello docelowy uwierzytelniania inicjatora hello i tego inicjatora hello uwierzytelnia hello docelowej. |
| klonowania |Duplikat woluminu. |
| Chmura warstwy (CaaT) |Magazyn zintegrowana warstwy w hello Architektura magazynu, dzięki czemu wszystkie magazyny są widoczne toobe część jednego przedsiębiorstwa sieć magazynu w chmurze. |
| dostawcy usług w chmurze (CSP) |Dostawca rozwiązań usług w chmurze. |
| Migawka w chmurze |W momencie kopię wolumin danych przechowywanych w chmurze hello. Migawka w chmurze jest równoważna migawki tooa replikowane w systemie magazynu innych, poza nim. Migawki w chmurze są szczególnie przydatne w scenariuszach odzyskiwania po awarii. |
| klucz szyfrowania magazynu w chmurze |Hasło lub klucz używany przez dane zaszyfrowane hello tooaccess urządzenia StorSimple wysyłanych przez urządzenia toohello chmury. |
| Aktualizacja typu cluster-aware |Zarządzanie aktualizacje oprogramowania na serwerach w klastrze pracy awaryjnej, aby aktualizacje hello ma minimalny lub nie mają wpływu na dostępność usługi. |
| ścieżki danych |Kolekcja jednostki organizacyjne, które wykonują operacje wzajemnie połączonych przetwarzania danych. |
| Dezaktywowanie |Trwałe, że podziały hello połączenie między hello urządzenia StorSimple i hello skojarzone usługi w chmurze. Migawki w chmurze urządzenia powitania po ten proces i można sklonować lub używanych na potrzeby odzyskiwania po awarii. |
| dublowanie dysków |Replikacji woluminów dysku logicznego na oddzielnym twardych dysków w czasie rzeczywistym tooensure ciągłej dostępności. |
| dublowanie dysku dynamicznego |Replikacja dysku logicznego woluminów dysków dynamicznych. |
| dyski dynamiczne |Format wolumin dysku, że używa hello toostore Menedżera dysków logicznych (LDM) danych i zarządzać nimi na wielu dyskach fizycznych. Dyski dynamiczne mogą być powiększony tooprovide więcej wolnego miejsca. |
| Rozszerzone obudowa grupy dysków (EBOD) |Dodatkowej obudowy urządzenia Microsoft Azure StorSimple, który zawiera dyski dodatkowego dysku twardego dla dodatkowego miejsca do magazynowania. |
| Inicjowanie obsługi administracyjnej FAT |Konwencjonalne Inicjowanie obsługi administracyjnej magazynu w magazynie, które przydzielone miejsce na podstawie przewidywanych potrzeb (i zazwyczaj znajduje się poza zapotrzebowania hello). Zobacz też *alokowanie*. |
| dysk twardy (HDD) |Dysk, który używa obracania płyt toostore danych. |
| Magazyn w chmurze hybrydowej |Architektura magazynu, która używa zasobów lokalnych i poza nim, w tym magazynie w chmurze. |
| Internet Small Computer System Interface (iSCSI) |Magazynu opartego na protokole IP standard sieciowy do łączenia urządzeń magazynu danych lub urządzeń. |
| Inicjator iSCSI |Składnik oprogramowania, który umożliwia komputer hosta sieci zewnętrznych magazynu opartego na protokole iSCSI tooan tooconnect systemu Windows. |
| iSCSI kwalifikowana nazwa (IQN) |Unikatowa nazwa identyfikująca obiektów docelowych iSCSI lub inicjatora. |
| obiekt docelowy iSCSI |Składnik oprogramowania, który zapewnia scentralizowane iSCSI podsystemów dysków w sieci magazynowania. |
| na żywo archiwizacji |Podejście magazynu, w którym dane archiwalne jest dostępny cały czas hello (nie są przechowywane wcześniejsze jego na taśmie, na przykład). Microsoft Azure StorSimple używa archiwizacji na żywo. |
| woluminu przypiętego lokalnie |wolumin, który znajduje się na urządzeniu hello i nigdy nie jest do warstwy toohello chmury. |
| Migawka lokalna |W momencie kopia danych woluminu, który jest przechowywany na urządzeniu Microsoft Azure StorSimple hello. |
| Microsoft Azure StorSimple |Niezwykle wydajnym rozwiązaniem, składające się z urządzenie magazynu centrum danych i oprogramowania, które pozwala tooleverage organizacje IT magazynu w chmurze tak, jakby była centrach danych. StorSimple upraszcza ochrony danych i zarządzanie danymi, ograniczając jednocześnie koszty. rozwiązanie Hello konsoliduje podstawową odzyskiwania pamięci masowej, archiwum kopii zapasowej i po awarii (DR) za pośrednictwem bezproblemową integrację z chmurą hello. Połączenie SAN zarządzanie danymi i magazynu w chmurze na platformie klasy korporacyjnej, urządzenia StorSimple umożliwić szybkości, prostota i niezawodność wszystkie potrzeby związane z magazynowaniem. |
| Zasilania i chłodzenia modułu (PCM) |Składniki sprzętowe urządzenia StorSimple hello zasilacze i hello wentylatora, dlatego hello modułu zasilania i Cooling nazwy. Obudowa głównej Hello hello urządzenia ma dwa PCMs 764W hello obudowa EBOD ma dwa PCMs 580W. |
| Obudowa podstawowego |Główne Obudowa urządzenia StorSimple, który zawiera kontrolery platformy aplikacji hello. |
| Celu czasu odzyskiwania (RTO) |pełni po przywróceniu Hello maksymalną ilość czasu, który powinien czyszcząca przed proces biznesowy lub systemu po awarii. |
| magistrali Serial attached SCSI (SAS) |Typ stacji dysków twardych (HDD). |
| klucz szyfrowania danych usługi |Klucz wprowadzone tooany dostępne nowe urządzenia StorSimple, która rejestruje hello usługi Menedżer StorSimple urządzenia. dane konfiguracji Hello przesyłanych między hello usługi Menedżer urządzenia StorSimple oraz urządzenia hello jest szyfrowana przy użyciu klucza publicznego i następnie mogły być odszyfrowane tylko na urządzeniu hello przy użyciu klucza prywatnego. Klucz szyfrowania danych usługi umożliwia tooobtain usługi hello klucz prywatny do odszyfrowywania. |
| klucz rejestracji usługi |Klucz, który pomaga zarejestrować urządzenia StorSimple hello z hello usługi Menedżer StorSimple urządzenia tak, aby był wyświetlany w hello portalu Azure, aby uzyskać dodatkowe akcje zarządzania. |
| Small Computer System Interface (SCSI) |Zestaw standardy dotyczące fizycznego łączenia komputerów i przekazywania danych między nimi. |
| dysków półprzewodnikowych (SSD) |Dysk, który nie zawiera żadnych części przenoszenie; na przykład dysku flash. |
| Konto magazynu |Zestaw poświadczeń dostępu do połączonego konta magazynu tooyour dla określonej chmury dostawcy usług. |
| Adapter usługi StorSimple dla programu SharePoint |Składnik Microsoft Azure StorSimple, rozszerzający niewidocznie StorSimple magazynu i ochronę danych farm serwerów tooSharePoint. |
| Usługa menedżera urządzenia StorSimple |Rozszerzenie hello portalu Azure, która pozwala toomanage Azure StorSimple lokalnie, a urządzenia wirtualnego. |
| StorSimple Snapshot Manager |Microsoft Management Console (MMC) przystawki do zarządzania operacje tworzenia kopii zapasowej i przywracania w Microsoft Azure StorSimple. |
| Pobierz kopię zapasową |Funkcja, która umożliwia hello tootake użytkownika interaktywnego kopii zapasowej woluminu. Jest to alternatywny sposób podjęcia ręcznego wykonywania kopii zapasowej woluminu jako min. tootaking automatyczne kopie zapasowe za pośrednictwem zdefiniowane zasady. |
| Alokowanie elastyczne |Metoda optymalizacji wydajności hello, z których hello dostępne miejsce jest używana w systemów pamięci masowej. W alokacji elastycznej magazynu hello jest przydzielany przez wielu użytkowników oparte na powitania minimalny odstęp wymagane przez każdego użytkownika w danym momencie. Zobacz też *fat inicjowania obsługi administracyjnej*. |
| Obsługa poziomów |Organizowanie danych w logiczne grupy na podstawie bieżącego użycia, wieku i dane tooother relacji. StorSimple automatycznie rozmieszcza danych w warstwach. |
| Wolumin |Przedstawione w formie hello dysków obszary logicznej magazynu. Woluminy StorSimple odpowiada woluminów toohello zainstalowanych przez hosta hello, łącznie z tymi wykryte za pomocą hello iSCSI i urządzenia StorSimple. |
| kontener woluminów |Grupowanie woluminów i ustawienia hello toothem. Wszystkie woluminy w urządzeniu StorSimple są pogrupowane w kontenery woluminów. Ustawienia kontenera woluminów obejmują kont magazynu, ustawień szyfrowania dla danych wysyłane toocloud skojarzonych kluczy i przepustowości operacji dotyczących hello chmury. |
| grupy woluminu |W StorSimple Snapshot Manager grupy woluminu jest kolekcją przetwarzania kopii zapasowych woluminów skonfigurowane toofacilitate. |
| Usługa kopiowania woluminów w tle (VSS) |Usługa systemu operacyjnego Windows Server, która ułatwia komunikując się z obsługującym usługę VSS tworzenie aplikacji toocoordinate hello przyrostowe migawek spójności aplikacji. Usługa VSS zapewnia, że aplikacji hello są tymczasowo nieaktywne, przy tworzeniu migawek woluminów. |
| Program Windows PowerShell dla StorSimple |Interfejs wiersza polecenia opartego na programie Windows PowerShell używany toooperate i zarządzania urządzeniem StorSimple. Przy zachowaniu niektórych hello podstawowe funkcje programu Windows PowerShell, ten interfejs ma dodatkowe dedykowanych poleceń cmdlet, które są przeznaczone dla zarządzania urządzeniem StorSimple. |

## <a name="next-steps"></a>Następne kroki
Dowiedz się więcej o [zabezpieczenia usługi StorSimple](storsimple-8000-security.md).

