---
title: aaaInstall karty StorSimple dla programu SharePoint | Dokumentacja firmy Microsoft
description: "Opisuje sposób tooinstall i skonfigurować lub usunąć hello karty StorSimple dla programu SharePoint w farmie serwerów programu SharePoint."
services: storsimple
documentationcenter: NA
author: SharS
manager: timlt
editor: 
ms.assetid: 36c20b75-f2e5-4184-a6b5-9c5e618f79b2
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 06/06/2017
ms.author: v-sharos
ms.openlocfilehash: 9a7347232fb80156d93212e6382cdd4fab98a2d6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="install-and-configure-hello-storsimple-adapter-for-sharepoint"></a>Instalowanie i konfigurowanie hello karty StorSimple dla programu SharePoint
## <a name="overview"></a>Omówienie
Witaj karty StorSimple dla programu SharePoint jest składnikiem, który umożliwia elastyczne magazynu Microsoft Azure StorSimple i farm serwerów tooSharePoint ochrony danych. Możesz użyć hello karty toomove dużych obiektu binarnego (BLOB) zawartości z hello programu SQL Server baz danych zawartości toohello Microsoft Azure StorSimple hybrydowe chmury magazynu urządzenia.

Witaj karty StorSimple dla programu SharePoint działa jako dostawca magazynu obiektów BLOB zdalnego (SPZ) i używa hello toostore funkcji zdalnego magazynu obiektów BLOB SQL Server bez struktury zawartości programu SharePoint (w formie hello obiektów blob) na serwerze plików, który nie jest obsługiwana przez urządzenia StorSimple.

> [!NOTE]
> Witaj karty StorSimple dla programu SharePoint obsługuje SharePoint Server 2010 zdalnego obiektu BLOB magazynu (SPZ). Nie obsługuje programu SharePoint Server 2010 zewnętrznego obiektu BLOB magazynu (EBS).


* toodownload hello karty StorSimple dla programu SharePoint, przejdź zbyt[karty StorSimple dla programu SharePoint] [ 1] w hello Microsoft Download Center.
* Informacje o planowaniu SPZ i SPZ ograniczenia, przejdź zbyt[podejmowania decyzji o toouse SPZ w SharePoint 2013] [ 2] lub [planowanie SPZ (SharePoint Server 2010)] [3].

Witaj końca ten przegląd zawiera krótki opis roli hello hello karty StorSimple dla programu SharePoint i hello pojemności programu SharePoint i ograniczeń wydajności, że należy wiedzieć przed zainstalowaniem i skonfigurowaniem hello karty. Po przejrzeniu tych informacji, przejdź zbyt[kartę StorSimple dla instalacji programu SharePoint](#storsimple-adapter-for-sharepoint-installation) toobegin konfigurowania hello karty.

### <a name="storsimple-adapter-for-sharepoint-benefits"></a>Karta StorSimple korzyści programu SharePoint
W witrynie programu SharePoint zawartość jest przechowywana jako bez struktury danych obiektów BLOB w jedną lub więcej baz danych zawartości. Domyślnie te bazy danych są obsługiwane na komputerach z programem SQL Server, które znajdują się w farmie serwerów SharePoint hello. Obiekty BLOB można szybko wzrost rozmiaru zużywa duże ilości magazynu lokalnego. Z tego powodu może być toofind mniej kosztowne, pamięci masowej. Program SQL Server stanowi mechanizmu zdalnego obiektu Blob magazynu (SPZ), która umożliwia przechowywanie zawartości obiektu BLOB w systemie plików hello, poza hello bazy danych SQL Server. SPZ obiekty BLOB może znajdować się w systemie plików hello na powitania komputera, na którym działa program SQL Server, lub mogą być przechowywane w systemie plików hello na innym serwerze.

SPZ wymaga użycia dostawcy SPZ, takich jak hello karty StorSimple dla programu SharePoint, tooenable SPZ w programie SharePoint. Hello karty StorSimple dla programu SharePoint współpracuje z SPZ, co pozwala na przeniesienie serwera tooa obiekty BLOB kopii zapasowej przez system Microsoft Azure StorSimple hello. Microsoft Azure StorSimple następnie przechowuje dane obiektów BLOB hello lokalnie lub w chmurze hello na podstawie użycia. Obiekty BLOB, które są bardzo aktywny (zazwyczaj określony tooas warstwy 1 lub gorących danych) znajdują się lokalnie. Mniej aktywne dane i dane archiwalne znajdują się w chmurze hello. Po włączeniu SPZ na bazę danych zawartości, zawartość obiektu BLOB utworzone w programie SharePoint są przechowywane na urządzeniu StorSimple hello, a nie w hello bazy danych zawartości.

implementacja Microsoft Azure StorSimple Hello SPZ zapewnia hello następujące korzyści:

* Przez przenoszenie obiektów BLOB zawartości tooa oddzielny serwer można zmniejszyć obciążenie zapytaniami hello na serwerze SQL można zwiększyć czas odpowiedzi serwera SQL. 
* Azure StorSimple używa kompresji i deduplikacji rozmiar danych tooreduce.
* Azure StorSimple zapewnia ochronę danych w formie hello lokalne i migawki w chmurze. Ponadto jeśli hello bazy danych na urządzeniu StorSimple hello, można tworzyć kopie zapasowe bazy danych zawartości hello i obiektów blob razem w awaria spójny sposób. (Urządzenia toohello Przenoszenie bazy danych zawartości hello jest obsługiwana tylko dla urządzenia serii StorSimple 8000 hello. Ta funkcja nie jest obsługiwana dla serii hello 5000 i 7000.)
* Azure StorSimple obejmuje funkcje odzyskiwania po awarii, w tym tryb failover, odzyskiwanie plików i woluminów (w tym testowe odzyskiwanie) i szybkie przywrócenie danych.
* Oprogramowanie odzyskiwania danych, takich jak Kroll Ontrack PowerControls, służy z StorSimple migawki obiektu BLOB danych tooperform elementu odzyskiwanie na poziomie zawartości programu SharePoint. (To oprogramowanie odzyskiwania danych jest oddzielnego zakupu).
* Hello karty StorSimple dla programu SharePoint podłącza się do portalu Administracja centralna programu SharePoint hello, dzięki czemu toomanage całego rozwiązania programu SharePoint z centralnej lokalizacji.

Przenoszenie zawartości toohello obiektów BLOB w systemie plików może zapewnić innych kosztach i korzyści. Na przykład przy użyciu SPZ można ograniczyć potrzebę hello tańsze magazynowanie warstwy 1 i, ponieważ jej zmniejsza hello bazy danych zawartości, SPZ może zmniejszyć hello liczba baz danych w farmie serwerów SharePoint hello wymagane. Jednak inne czynniki, takie jak limity rozmiaru bazy danych i hello ilości zawartości z systemem innym niż SPZ, może również wpływać na wymagania dotyczące magazynu. Aby uzyskać więcej informacji na temat hello kosztów i korzyści wynikające ze stosowania SPZ zobacz [planowanie SPZ (SharePoint Foundation 2010)] [ 4] i [podejmowania decyzji o toouse SPZ w SharePoint 2013] [ 5].

### <a name="capacity-and-performance-limits"></a>Limity pojemności i wydajności
Przed uznaniem przy użyciu SPZ rozwiązania programu SharePoint, należy zwrócić uwagę hello przetestować wydajność i limity pojemności programu SharePoint Server 2010 i SharePoint Server 2013 oraz powiązań tooacceptable wydajności przez te limity. Aby uzyskać więcej informacji, zobacz [granic oprogramowania i limity dla programu SharePoint 2013](https://technet.microsoft.com/library/cc262787.aspx).

Przed skonfigurowaniem SPZ, należy przejrzeć następujące hello:

* Upewnij się, łączny rozmiar hello tego hello zawartości (hello rozmiar bazy danych zawartości) oraz rozmiar hello wszystkie skojarzone obiekty BLOB externalized nie przekracza limit rozmiaru SPZ hello obsługiwane przez program SharePoint. To ograniczenie jest 200 GB. 
  
    **Baza danych zawartości toomeasure i rozmiar obiektu BLOB**
  
  1. Uruchom to zapytanie na powitania WFE administracji centralnej. Uruchom hello powłoki zarządzania programu SharePoint, a następnie wprowadź hello następującego środowiska Windows PowerShell polecenia tooget hello rozmiar baz danych zawartości hello:
     
     `Get-SPContentDatabase | Select-Object -ExpandProperty DiskSizeRequired`
     
      Ten krok pobiera rozmiar hello hello bazy danych zawartości na powitania dysku.
  2. Uruchom jedno z hello następującej kwerendy SQL w programie SQL Management Studio na powitania okno serwera SQL w każdej bazie danych zawartości, a następnie dodaj numer toohello wynik hello uzyskane w kroku 1.
     
     W bazach danych zawartości programu SharePoint 2013 wprowadź:
     
     `SELECT SUM([Size]) FROM [ContentDatabaseName].[dbo].[DocStreams] WHERE [Content] IS NULL`
     
     W bazach danych zawartości programu SharePoint 2010 wprowadź:
     
     `SELECT SUM([Size]) FROM [ContentDatabaseName].[dbo].[AllDocs] WHERE [Content] IS NULL`
     
     Ten krok pobiera rozmiar hello hello obiektów blob, które zostały externalized.
* Firma Microsoft zaleca przechowywania wszystkich obiektów BLOB i bazy danych zawartości lokalnie na urządzeniu StorSimple hello. urządzenie StorSimple Hello jest dwa węzły klastra w celu zapewnienia wysokiej dostępności. Umieszczenie bazy danych zawartości hello i obiekty BLOB na urządzeniu StorSimple hello zapewnia wysoką dostępność.
  
    Użyj tradycyjnych programu SQL Server migracji najlepszych praktyk toomove hello bazy danych zawartości toohello urządzenia StorSimple. Przenieś hello bazy danych tylko wtedy, gdy cała zawartość obiektu BLOB z bazy danych hello został przeniesiony toohello udziału plików za pośrednictwem SPZ. Jeśli wybierzesz urządzenia StorSimple toohello toomove hello bazy danych zawartości, zaleca się konfigurowanie hello magazynu bazy danych zawartości na urządzeniu powitania jako podstawowego wolumin.
* W programie Microsoft Azure StorSimple, jeśli przy użyciu woluminów warstwowych nie istnieje sposób tooguarantee zawartości przechowywany lokalnie na urządzeniu StorSimple hello nie będą tooMicrosoft warstwowych magazynu w chmurze Azure. W związku z tym zaleca się korzystanie z woluminów StorSimple przypięty lokalnie w połączeniu z SPZ programu SharePoint. To zapewnia, że cała zawartość obiektu BLOB pozostaje lokalnie na urządzeniu StorSimple hello i nie jest przenoszone tooMicrosoft Azure.
* Jeśli hello baz danych zawartości nie są przechowywane na urządzeniu StorSimple hello, stosować tradycyjnych programu SQL Server wysokiej dostępności najlepsze rozwiązania obsługujące SPZ. Klaster programu SQL Server obsługuje SPZ, podczas SQL Server dublowanie nie. 

> [!WARNING]
> Jeśli nie włączono SPZ, nie zaleca się przenoszenie urządzenia StorSimple toohello bazy danych zawartości hello. To jest Konfiguracja zastosowaniem.

## <a name="storsimple-adapter-for-sharepoint-installation"></a>Karta StorSimple dla instalacji programu SharePoint
Przed zainstalowaniem hello karty StorSimple dla programu SharePoint, należy skonfigurować urządzenie StorSimple hello i upewnij się, że farmy serwerów programu SharePoint hello i wystąpienia programu SQL Server spełniają wszystkie wymagania wstępne. W tym samouczku opisano wymagania dotyczące konfiguracji, a także procedury dotyczące instalowania i uaktualniania hello karty StorSimple dla programu SharePoint.

## <a name="configure-prerequisites"></a>Konfigurowanie wymagań wstępnych
Przed zainstalowaniem hello karty StorSimple dla programu SharePoint, upewnij się, że urządzenia StorSimple hello, farmy programu SharePoint server i wystąpienia serwera SQL spełniają następujące wymagania wstępne hello.

### <a name="system-requirements"></a>Wymagania systemowe
Witaj karty StorSimple dla programu SharePoint działa z hello następującego sprzętu i oprogramowania:

* Obsługiwany system operacyjny — Windows Server 2008 R2 z dodatkiem SP1, Windows Server 2012 lub Windows Server 2012 R2
* Obsługiwane wersje programu SharePoint — SharePoint Server 2010 lub SharePoint Server 2013
* Obsługiwane wersje programu SQL Server — SQL Server 2008 Enterprise Edition, SQL Server 2008 R2 Enterprise Edition lub SQL Server 2012 Enterprise Edition
* Obsługiwane urządzenia StorSimple — z serii StorSimple 8000, StorSimple 7000 serii lub z serii StorSimple 5000.

### <a name="storsimple-device-configuration-prerequisites"></a>Wymagania wstępne dotyczące konfiguracji urządzenia StorSimple
urządzenia StorSimple Hello jest urządzeniem bloku i jako takie wymaga serwera plików, na którym hello danych może być obsługiwany. Zalecane jest użycie osobnego serwera, a nie z istniejącego serwera z hello farmy programu SharePoint. Ten serwer plików musi być na hello tej samej sieci lokalnej (LAN) jako komputer serwera SQL hello hostujących hello zawartości bazy danych.

> [!TIP]
> * Jeśli możesz skonfigurować farmę programu SharePoint w celu zapewnienia wysokiej dostępności, należy wdrożyć także hello serwer plików na potrzeby wysokiej dostępności.
> * Jeśli hello bazy danych zawartości nie są przechowywane na urządzeniu StorSimple hello, użyj tradycyjnych wysokiej dostępności najlepsze rozwiązania, które obsługują SPZ. Klaster programu SQL Server obsługuje SPZ, podczas SQL Server dublowanie nie. 


Upewnij się, że urządzenia StorSimple jest poprawnie skonfigurowany i że toosupport odpowiednich woluminów wdrożeniu programu SharePoint są skonfigurowane i dostępne z komputera programu SQL Server. Przejdź za[wdrażanie lokalnego urządzenia StorSimple](storsimple-8000-deployment-walkthrough-u2.md) Jeśli nie zostały jeszcze wdrożone i skonfigurowane na urządzeniu StorSimple. Należy zwrócić uwagę hello adres IP urządzenia StorSimple hello; będą one potrzebne podczas karty StorSimple dla instalacji programu SharePoint.

Ponadto upewnij się, że ten toobe woluminu hello używany dla obiekt BLOB externalization spełnia hello następujące wymagania:

* musi być sformatowany Hello woluminu o rozmiarze jednostki alokacji 64 KB.
* Fronton sieci web (WFE), a serwery aplikacji musi być możliwe tooaccess hello woluminu za pomocą ścieżki Universal Naming Convention (UNC).
* Farma serwerów SharePoint Hello musi być skonfigurowany toowrite toohello woluminu.

> [!NOTE]
> Po zainstalowaniu i skonfigurowaniu karty hello, wszystkie externalization obiektu BLOB musi przechodzić przez urządzenia StorSimple hello (hello urządzenia będą stanowić tooSQL woluminów powitania serwera i zarządzać nimi hello warstw magazynowania). Nie można użyć innych celów externalization obiektu BLOB.


Jeśli planujesz toouse StorSimple Snapshot Manager tootake migawek hello obiektów BLOB z bazy danych, można się tooinstall StorSimple Snapshot Manager na serwerze bazy danych hello, dzięki czemu można użyć hello tooimplement składnik zapisywania usługi SQL hello kopiowania woluminów w tle systemu Windows Usługi (w tle VSS).

> [!IMPORTANT]
> StorSimple Snapshot Manager nie obsługuje hello składnik zapisywania usługi VSS programu SharePoint i nie można wykonać spójnych z aplikacją migawki danych programu SharePoint. W przypadku programu SharePoint StorSimple Snapshot Manager zapewnia tylko spójna w razie awarii kopie zapasowe.


## <a name="sharepoint-farm-configuration-prerequisites"></a>Wymagania wstępne dotyczące konfiguracji farmy programu SharePoint
Upewnij się, że farmę programu SharePoint server został poprawnie skonfigurowany, w następujący sposób:

* Sprawdź, czy farmy serwerów programu SharePoint jest w dobrej kondycji i sprawdź następujące hello:
* Wszystkie WFE programu SharePoint i zarejestrowanych w farmie hello serwerów aplikacji są uruchomione i reaguje na operację ping z serwera hello, na którym będzie instalowany hello karty StorSimple dla programu SharePoint.
* Witaj Usługa czasomierza programu SharePoint (SPTimerV3 lub SPTimerV4) jest uruchomiona na każdym serwerze WFE i aplikacji.
* Zarówno hello Usługa czasomierza programu SharePoint i pula aplikacji usług IIS hello zgodnie z którymi hello działa witryny Administracja centralna programu SharePoint należy mieć uprawnienia administratora.
* Upewnij się, że kontekst zabezpieczeń rozszerzone Eksploratora Internet (nazywana konfiguracją IE ESC) jest wyłączona. Wykonaj te kroki toodisable IE ESC:
  
  1. Zamknij wszystkie wystąpienia programu Internet Explorer.
  2. Uruchom hello Menedżera serwera.
  3. W okienku po lewej stronie powitania kliknij **lokalnego serwera**.
  4. Na powitania kliknij prawym przyciskiem myszy okienko, obok zbyt**Konfiguracja zwiększonych zabezpieczeń**, kliknij przycisk **na**.
  5. W obszarze **Administratorzy**, kliknij przycisk **poza**.
  6. Kliknij przycisk **OK**.

## <a name="remote-blob-storage-rbs-prerequisites"></a>Zdalnego magazynu obiektów BLOB (SPZ) wymagania wstępne
Upewnij się, że używasz obsługiwanej wersji programu SQL Server. Tylko hello następujące wersje są obsługiwane i stanie toouse SPZ:

* SQL Server 2008 Enterprise Edition
* SQL Server 2008 R2 Enterprise Edition
* SQL Server 2012 Enterprise Edition

Obiekty BLOB można externalized na, tylko na tych woluminach, które hello urządzenia StorSimple przedstawia tooSQL serwera. Nie innych elementów docelowych dla obiekt BLOB externalization są obsługiwane.

Po zakończeniu wszystkich kroków konfiguracji wymagania wstępnego Przejdź zbyt[hello instalacji karty StorSimple dla programu SharePoint](#install-the-storsimple-adapter-for-sharepoint).

## <a name="install-hello-storsimple-adapter-for-sharepoint"></a>Zainstaluj hello karty StorSimple dla programu SharePoint
Użyj hello następujące kroki tooinstall hello karty StorSimple dla programu SharePoint. Jeśli instalujesz oprogramowanie hello, zobacz [uaktualnić lub ponownie zainstalować hello karty StorSimple dla programu SharePoint](#upgrade-or-reinstall-the-storsimple-adapter-for-sharepoint). Hello czas wymagany do instalacji hello zależy od hello łączna liczba baz danych programu SharePoint w farmie serwerów programu SharePoint.

[!INCLUDE [storsimple-install-sharepoint-adapter](../../includes/storsimple-install-sharepoint-adapter.md)]

## <a name="configure-rbs"></a>Skonfiguruj SPZ
Po zainstalowaniu hello karty StorSimple dla programu SharePoint, należy skonfigurować SPZ zgodnie z opisem w hello procedury.

> [!TIP]
> Hello karty StorSimple dla programu SharePoint podłącza się do strony Administracja centralna programu SharePoint hello, umożliwiając toobe SPZ włączać lub wyłączać dla każdej bazy danych zawartości hello farmy programu SharePoint. Jednak włączenie lub wyłączenie SPZ na powitania bazy danych zawartości powoduje resetowanie usług IIS, która w zależności od konfiguracji farmy, na chwilę może zakłócać hello dostępność hello SharePoint frontonu sieci web (WFE). (Czynników, takich jak hello korzystanie z usługi równoważenia obciążenia frontonu, hello bieżące obciążenie serwera i tak dalej, można ograniczyć lub wyeliminować ten przerw w działaniu.) tooprotect użytkownikom zakłócenia, firma Microsoft zaleca, że można włączyć lub wyłączyć SPZ tylko podczas okna zaplanowanej konserwacji.


[!INCLUDE [storsimple-sharepoint-adapter-configure-rbs](../../includes/storsimple-sharepoint-adapter-configure-rbs.md)]

## <a name="configure-garbage-collection"></a>Skonfiguruj wyrzucanie elementów bezużytecznych
Usunięcie obiektów z witryny programu SharePoint nie automatycznie są usuwane z hello SPZ wolumin magazynu. Zamiast tego asynchroniczna, oddzielone obiekty BLOB usuwa tła konserwacji programu z hello pliku magazynu. Administratorzy systemu można zaplanować tego procesu toorun okresowo lub można ją w razie konieczności uruchamiania.

Ten program obsługi (Microsoft.Data.SqlRemoteBlobs.Maintainer.exe) jest automatycznie instalowany na wszystkich serwerów WFE programu SharePoint i serwerów aplikacji, po włączeniu SPZ. Hello program jest zainstalowany w następującej lokalizacji hello: *dysk rozruchowy*: \Program Files\Microsoft 10.50\Maintainer\ zdalnego magazynu obiektów Blob SQL

Aby uzyskać informacje o konfigurowaniu i używaniu programu obsługi hello, zobacz [Obsługa SPZ w SharePoint Server 2013][8].

> [!IMPORTANT]
> program Element utrzymujący SPZ Hello jest ilości zasobów. Należy zaplanować jego toorun tylko podczas okresów niewielka aktywność na powitania farmy programu SharePoint.


### <a name="delete-orphaned-blobs-immediately"></a>Natychmiast usunąć osierocone obiekty BLOB
Obiekty BLOB toodelete oddzielona od razu, należy służy hello, postępując zgodnie z instrukcjami. Należy pamiętać, że te instrukcje są przykładem jak można to zrobić w środowisku programu SharePoint 2013 z hello następujące składniki:

* Nazwa bazy danych zawartości Hello jest WSS_Content.
* Nazwa serwera SQL Hello jest SHRPT13 SQL12\SHRPT13.
* Nazwa aplikacji sieci web Hello jest program SharePoint — 80.

[!INCLUDE [storsimple-sharepoint-adapter-garbage-collection](../../includes/storsimple-sharepoint-adapter-garbage-collection.md)]

## <a name="upgrade-or-reinstall-hello-storsimple-adapter-for-sharepoint"></a>Uaktualnić lub ponownie zainstalować hello karty StorSimple dla programu SharePoint
Użyj hello następujące procedury tooupgrade programu SharePoint server, a następnie ponownie zainstalować karty StorSimple do uaktualnienia programu SharePoint lub toosimply lub zainstalować ponownie adapter hello w istniejącej farmy serwerów programu SharePoint.

> [!IMPORTANT]
> Przejrzyj następujące informacje, przed podjęciem próby tooupgrade hello oprogramowania SharePoint i/lub uaktualnienia lub ponownego zainstalowania hello karty StorSimple dla programu SharePoint:
> 
> * Wszystkie pliki, które wcześniej zostały przeniesione tooexternal magazynu za pośrednictwem SPZ nie będą dostępne dopiero po zakończeniu hello ponownej instalacji i hello SPZ funkcji ponownego włączenia. Użytkownik toolimit wpływ, wszelkie uaktualnienia lub ponownej instalacji w oknie zaplanowanej konserwacji.
> * Witaj czas wymagany do uaktualnienia hello jego ponowna instalacja jest zależna od hello łączna liczba baz danych programu SharePoint w farmie serwerów SharePoint hello.
> * Po zakończeniu uaktualniania hello jego ponowna instalacja należy tooenable SPZ hello baz danych zawartości. Zobacz [skonfigurować SPZ](#configure-rbs) Aby uzyskać więcej informacji.
> * Jeśli konfigurujesz SPZ dla farmy programu SharePoint, który jest bardzo duża liczba baz danych (większe niż 200), hello **Administracja centralna programu SharePoint** strony może upłynął limit czasu. Jeśli to miejsce, Odśwież stronę hello. Nie dotyczy to proces konfiguracji hello.


[!INCLUDE [storsimple-upgrade-sharepoint-adapter](../../includes/storsimple-upgrade-sharepoint-adapter.md)]

## <a name="storsimple-adapter-for-sharepoint-removal"></a>Karta StorSimple do usunięcia programu SharePoint
Hello zgodnie z procedurami opisano, jak toomove obiekty BLOB hello kopii toohello baz danych zawartości programu SQL Server, a następnie odinstaluj hello karty StorSimple dla programu SharePoint. 

> [!IMPORTANT]
> Masz toomove hello obiekty BLOB wstecz toohello baz danych zawartości przed odinstalowaniem hello karty oprogramowania.


### <a name="before-you-begin"></a>Przed rozpoczęciem
Zbierz następujące informacje przed przeniesieniem danych hello kopii bazy danych zawartości programu SQL Server toohello i rozpocząć proces usuwania karty hello hello:

* nazwy wszystkich hello baz danych, dla których włączono SPZ Hello
* ścieżka UNC Hello hello skonfigurowane magazynu obiektów BLOB

### <a name="move-hello-blobs-back-toohello-content-databases"></a>Przenoszenie baz danych zawartości wstecz toohello obiekty BLOB hello
Przed odinstalowaniem hello karty StorSimple dla oprogramowania SharePoint, należy przeprowadzić migrację wszystkich hello obiektów blob, które zostały externalized toohello wstecz baz danych zawartości programu SQL Server. Jeśli hello toouninstall karty StorSimple dla programu SharePoint przed przeniesieniem wszystkich hello obiekty BLOB wstecz toohello baz danych zawartości, zobaczysz powitania po komunikat ostrzegawczy.

![Komunikat ostrzegawczy](./media/storsimple-adapter-for-sharepoint/sasp1.png)

#### <a name="toomove-hello-blobs-back-toohello-content-databases"></a>toomove hello obiekty BLOB wstecz toohello baz danych zawartości
1. Każdy z obiektów hello externalized Pobierz.
2. Otwórz hello **Administracja centralna programu SharePoint** strony, a następnie przejdź zbyt**ustawienia systemu**.
3. W obszarze **Azure StorSimple**, kliknij przycisk **skonfigurować karty StorSimple**.
4. Na powitania **skonfigurować karty StorSimple** kliknij przycisk hello **wyłączyć** znajdujący się poniżej wszystkich, które mają tooremove z magazynu obiektów BLOB zewnętrznych baz danych zawartości hello. 
5. Usuwanie obiektów hello z programu SharePoint i przekazać je ponownie.

Alternatywnie można użyć hello Microsoft` RBS Migrate()` polecenia cmdlet programu PowerShell dołączony do programu SharePoint. Aby uzyskać więcej informacji, zobacz [migrowania zawartości do lub wychodzący SPZ](https://technet.microsoft.com/library/ff628255.aspx).

Po przeniesieniu bazy danych zawartości wstecz toohello obiekty BLOB hello Przejdź toohello następnego kroku: [Odinstaluj hello karty](#uninstall-the-adapter).

### <a name="uninstall-hello-adapter"></a>Odinstalowanie karty hello
Po przeniesieniu hello obiekty BLOB wstecz toohello programu SQL Server baz danych zawartości, użyj jednej z hello następujące opcje toouninstall hello karty StorSimple dla programu SharePoint.

#### <a name="toouse-hello-installation-program-toouninstall-hello-adapter"></a>toouse hello instalacji programu toouninstall hello karty
1. Użyj konta z toolog uprawnienia administratora na serwerze (WFE) frontonu sieci web toohello.
2. Instalator programu SharePoint, kliknij dwukrotnie hello karty StorSimple. Uruchamia Hello Kreatora instalacji.
   
    ![Kreator instalacji](./media/storsimple-adapter-for-sharepoint/sasp2.png)
3. Kliknij przycisk **Dalej**. pojawia się po stronie powitania.
   
    ![Usuń Kreatora instalacji](./media/storsimple-adapter-for-sharepoint/sasp3.png)
4. Kliknij przycisk **Usuń** proces usuwania hello tooselect. pojawia się po stronie powitania.
   
    ![Strona potwierdzenia Kreatora instalacji](./media/storsimple-adapter-for-sharepoint/sasp4.png)
5. Kliknij przycisk **Usuń** tooconfirm hello usuwania. zostanie wyświetlone powitania po stronie Postęp.
   
    ![Strona postępu Kreatora konfiguracji](./media/storsimple-adapter-for-sharepoint/sasp5.png)
6. Po zakończeniu usuwania hello zostanie wyświetlona strona Zakończ hello. Kliknij przycisk **Zakończ** hello tooclose Kreatora instalacji.

#### <a name="toouse-hello-control-panel-toouninstall-hello-adapter"></a>toouse hello Panelu sterowania toouninstall hello karty
1. Otwórz hello Panelu sterowania, a następnie kliknij przycisk **programy i funkcje**.
2. Wybierz **karty StorSimple dla programu SharePoint**, a następnie kliknij przycisk **Odinstaluj**.

## <a name="next-steps"></a>Następne kroki
[Dowiedz się więcej o StorSimple](storsimple-overview.md).

<!--Reference links-->
[1]: https://www.microsoft.com/download/details.aspx?id=44073
[2]: https://technet.microsoft.com/library/ff628583(v=office.15).aspx
[3]: https://technet.microsoft.com/library/ff628583(v=office.14).aspx
[4]: https://technet.microsoft.com/library/ff628569(v=office.14).aspx
[5]: https://technet.microsoft.com/library/ff628583(v=office.15).aspx
[8]: https://technet.microsoft.com/en-us/library/ff943565.aspx
