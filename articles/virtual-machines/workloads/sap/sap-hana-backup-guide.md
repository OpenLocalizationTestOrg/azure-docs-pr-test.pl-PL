---
title: Przewodnik aaaBackup SAP HANA na maszynach wirtualnych platformy Azure | Dokumentacja firmy Microsoft
description: "Podręcznik tworzenia kopii zapasowej programu SAP HANA udostępnia dwie główne możliwości tworzenia kopii zapasowej dla SAP HANA na maszynach wirtualnych Azure"
services: virtual-machines-linux
documentationcenter: 
author: hermanndms
manager: timlt
editor: 
ms.service: virtual-machines-linux
ms.devlang: NA
ms.topic: article
ums.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 3/13/2017
ms.author: rclaus
ms.openlocfilehash: e651091bb5da2698ec8bf80cad405bfce5b192cf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="backup-guide-for-sap-hana-on-azure-virtual-machines"></a>Przewodnik po wykonywaniu kopii zapasowych dla oprogramowania SAP HANA w usłudze Azure Virtual Machines

## <a name="getting-started"></a>Wprowadzenie

Witaj przewodniku kopia zapasowa dla SAP HANA uruchomionych na maszynach wirtualnych Azure tylko opisano tematy specyficzne dla platformy Azure. Ogólne SAP HANA kopii zapasowej elementów pokrewnych, zapoznaj się z dokumentacją SAP HANA hello (zobacz _dokumentacji kopii zapasowej SAP HANA_ dalszej części tego artykułu).

Witaj ten artykuł koncentruje się na dwie główne kopii zapasowej możliwości SAP HANA na maszynach wirtualnych Azure:

- System plików kopii zapasowej toohello HANA w maszynie wirtualnej systemu Linux platformy Azure (zobacz [SAP HANA kopia zapasowa Azure na poziomie plików](sap-hana-backup-file-level.md))
- HANA kopii zapasowej na podstawie migawki magazynu ręcznie przy użyciu funkcji migawki obiektu blob magazynu Azure hello lub usługa Kopia zapasowa Azure (zobacz [SAP HANA kopii zapasowych oparte na magazynu migawek](sap-hana-backup-storage-snapshots.md))

SAP HANA oferuje kopii zapasowej interfejsu API, który umożliwia toointegrate narzędzia tworzenia kopii zapasowych innych firm bezpośrednio z programu SAP HANA. (To nie jest w zakresie hello tego przewodnika.) Nie ma żadnych bezpośrednia integracja SAP HANA z prawej dostępna teraz oparta na ten interfejs API usługi Azure Backup.

SAP HANA jest oficjalnie obsługiwana dla typu maszyny Wirtualnej Azure GS5 jako pojedyncze wystąpienie z obciążeniami tooOLAP dodatkowe ograniczenia (zobacz [Znajdź certyfikowane platform IaaS](https://global.sap.com/community/ebook/2014-09-02-hana-hardware/enEN/iaas.html) w witrynie sieci Web hello SAP). Ten artykuł zostanie zaktualizowany po nowych ofert dla SAP HANA na platformie Azure staną się dostępne.

Brak dostępnej również SAP HANA hybrydowego na platformie Azure, w którym SAP HANA działa niezwirtualizowanych na serwerach fizycznych. Jednak w tym przewodniku kopia zapasowa SAP HANA Azure dotyczą czystego środowiska platformy Azure, gdzie SAP HANA działa w maszynie Wirtualnej platformy Azure, nie SAP HANA systemem &quot;dużych wystąpień.&quot; Zobacz [omówienie SAP HANA (duże wystąpień) i architektury na platformie Azure](hana-overview-architecture.md) Aby uzyskać więcej informacji o tym rozwiązaniu kopii zapasowej na &quot;dużych wystąpień&quot; oparty na pamięci masowej migawki.

Ogólne informacje o produktach SAP obsługiwane na platformie Azure można znaleźć w [1928533 Uwaga SAP](https://launchpad.support.sap.com/#/notes/1928533).

Witaj poniższe rysunki trzy Przypisz omówienie hello SAP HANA opcje tworzenia kopii zapasowej za pomocą natywnej funkcji Azure obecnie i również wyświetlane trzy możliwe scenariusze tworzenia kopii zapasowej przyszłych. Witaj innych pokrewnych artykułach [SAP HANA kopia zapasowa Azure na poziomie plików](sap-hana-backup-file-level.md) i [SAP HANA kopii zapasowych oparte na magazynu migawek](sap-hana-backup-storage-snapshots.md) opisano te opcje bardziej szczegółowo, uwzględniając rozmiaru i wydajności dla SAP HANA kopie zapasowe, które są multi terabajtów.

![Na poniższym rysunku przedstawiono dwie możliwości zapisywania hello bieżący stan maszyny Wirtualnej](media/sap-hana-backup-guide/image001.png)

Na poniższym rysunku pokazano hello możliwość zapisywania hello bieżący stan maszyny Wirtualnej, za pośrednictwem usługi Azure Backup lub ręcznego migawek dysków maszyny Wirtualnej. Z tą metodą, co &#39; nie ma tworzenia kopii zapasowych toomanage SAP HANA. Żądanie hello scenariusza migawki dysku hello jest spójności systemu plików i stan dysku spójnych z aplikacją. temat spójności Hello została szczegółowo opisana w sekcji hello _spójność danych SAP HANA podejmując magazynu migawek_ dalszej części tego artykułu. Ograniczenia usługi Kopia zapasowa Azure i możliwości związanych z kopii zapasowych HANA tooSAP również zostały omówione w dalszej części tego artykułu.

![Poniższy rysunek przedstawia opcje pobierania SAP HANA plików kopii zapasowej wewnątrz hello maszyny Wirtualnej](media/sap-hana-backup-guide/image002.png)

Na poniższym rysunku pokazano opcje kopii zapasowej pliku SAP HANA wewnątrz hello maszyny Wirtualnej, a następnie zapisanie jej pliki kopii zapasowej HANA innym else przy użyciu różnych narzędzi. Utworzenie kopii zapasowej HANA wymaga więcej czasu niż rozwiązanie tworzenia kopii zapasowej migawki, ale ma zalety dotyczące integralności i spójność. Bardziej szczegółowe informacje znajdują się w dalszej części tego artykułu.

![Na poniższym rysunku pokazano potencjalnych przyszłych SAP HANA kopii zapasowej scenariusza](media/sap-hana-backup-guide/image003.png)

Na poniższym rysunku przedstawiono potencjalne przyszłych scenariusz tworzenia kopii zapasowej SAP HANA. SAP HANA dozwolone wykonywania kopii zapasowych z replikacji dodatkowej, czy dodać dodatkowe opcje strategii tworzenia kopii zapasowych. Obecnie nie jest możliwe zgodnie z tooa post w hello SAP HANA Wiki:

_&quot;Jest to możliwe tootake wykonywanie kopii zapasowych na stronie dodatkowej hello?_

_Nie, obecnie można tylko pobierają dane i kopii zapasowych na głównej stronie powitania dziennika. Jeśli włączono tworzenie kopii zapasowej dziennika automatyczne po stronie dodatkowej toohello przejęcia, kopie zapasowe dziennika hello automatycznie zostanie zapisany istnieje.&quot;_

## <a name="sap-resources-for-hana-backup"></a>Zasoby SAP HANA kopii zapasowej

### <a name="sap-hana-backup-documentation"></a>SAP HANA dokumentacji kopii zapasowej

- [Wprowadzenie tooSAP HANA administracji](https://help.sap.com/viewer/6b94445c94ae495c83a19646e7c3fd56/2.0.00/en-US)
- [Planowanie z kopią zapasową i strategii odzyskiwania](https://help.sap.com/saphelp_hanaplatform/helpdata/en/ef/085cd5949c40b788bba8fd3c65743e/content.htm)
- [Planowanie kopii zapasowej HANA przy użyciu ABAP DBACOCKPIT](http://www.hanatutorials.com/p/schedule-hana-backup-using-abap.html)
- [Harmonogram kopii zapasowych danych (SAP HANA Panelu sterowania)](http://help.sap.com/saphelp_hanaplatform/helpdata/en/6d/385fa14ef64a6bab2c97a3d3e40292/frameset.htm)
- Często zadawane pytania dotyczące SAP HANA kopii zapasowej w [1642148 Uwaga SAP](https://launchpad.support.sap.com/#/notes/1642148)
- Często zadawane pytania dotyczące migawek magazynu i bazy danych SAP HANA w [2039883 Uwaga SAP](https://launchpad.support.sap.com/#/notes/2039883)
- Systemy plików nieodpowiednie sieci kopii zapasowych i odzyskiwania w [1820529 Uwaga SAP](https://launchpad.support.sap.com/#/notes/1820529)

### <a name="why-sap-hana-backup"></a>Dlaczego SAP HANA kopii zapasowej?

Magazyn Azure oferuje dostępność i niezawodność fabrycznej hello (zobacz [tooMicrosoft wprowadzenie usługi Azure Storage](../../../storage/common/storage-introduction.md) Aby uzyskać więcej informacji na temat usługi Azure storage).

Witaj minimum dla &quot;kopii zapasowej&quot; jest toorely na powitania umowy SLA platformy Azure, hello porządkowania SAP HANA danych i plików dziennika na serwerze SAP HANA dołączonych toohello Azure wirtualne dyski twarde maszyny Wirtualnej. Ta metoda obejmuje błędy maszyny Wirtualnej, ale nie potencjalne szkody toohello SAP HANA danych i pliki dziennika lub błędów logicznych, takich jak usuwanie danych lub plików przypadkowo. Kopie zapasowe są również wymagane dla zgodności lub z przyczyn prawnych. Innymi słowy zawsze konieczne jest kopii zapasowych SAP HANA.

### <a name="how-tooverify-correctness-of-sap-hana-backup"></a>Jak poprawności tooverify SAP HANA kopii zapasowej
Podczas korzystania z magazynu migawek, zalecane jest uruchomienie przywracania testu w innym systemie. Metoda ta umożliwia tooensure sposób, że kopia zapasowa jest prawidłowe i wewnętrznych procesów pracy i przywracania kopii zapasowej zgodnie z oczekiwaniami. Jest to znaczny próg wykluczający lokalnych, podając tymczasowo zasoby niezbędne do tego celu jest znacznie łatwiejsze tooaccomplish w chmurze hello.

Zachowaj pamiętać, że ten proste przywracanie i sprawdzania, czy działa HANA i uruchomiona jest niewystarczająca. Najlepiej co powinno być ono uruchomione toobe Sprawdzanie spójności tabeli się, że jest poprawnie hello przywrócić bazy danych. SAP HANA oferuje kilka rodzajów sprawdzenie spójności z opisem w temacie [1977584 Uwaga SAP](https://launchpad.support.sap.com/#/notes/1977584).

Informacje o sprawdzanie spójności tabeli hello można znaleźć w witrynie sieci Web hello SAP w [tabeli i sprawdzania spójności katalogu](http://help.sap.com/saphelp_hanaplatform/helpdata/en/25/84ec2e324d44529edc8221956359ea/content.htm#loio9357bf52c7324bee9567dca417ad9f8b).

Standardowy plik kopii zapasowych przywracania testu nie jest konieczne. Istnieją dwa narzędzia SAP HANA, które pomagają toocheck, których kopia zapasowa może służyć do przywracania: hdbbackupdiag i hdbbackupcheck. Zobacz [ręcznie sprawdzanie, czy odzyskiwanie jest możliwe](https://help.sap.com/saphelp_hanaplatform/helpdata/en/77/522ef1e3cb4d799bab33e0aeb9c93b/content.htm) uzyskać więcej informacji o tych narzędzi.

### <a name="pros-and-cons-of-hana-backup-versus-storage-snapshot"></a>Zalet i wad HANA tworzenia kopii zapasowej i pamięci masowej migawki

SAP &#39; t podać preferencji tooeither HANA tworzenia kopii zapasowej i przechowywania migawki. Wyświetlane ich zalet i wad, są tak jedną można określić, które toouse w zależności od sytuacji hello i technologii dostępnej pamięci (zobacz [planowania Your kopii zapasowej i odzyskiwania strategii](https://help.sap.com/saphelp_hanaplatform/helpdata/en/ef/085cd5949c40b788bba8fd3c65743e/content.htm)).

Na platformie Azure, należy pamiętać o hello fakt, że hello funkcja migawki obiektu blob systemu Azure &#39; t zagwarantowania spójności systemu plików (zobacz [migawki obiektu blob korzystanie z programu PowerShell](https://blogs.msdn.microsoft.com/cie/2016/05/17/using-blob-snapshots-with-powershell/)). Witaj w następnej sekcji _spójność danych SAP HANA podejmując magazynu migawek_, omówiono pewne kwestie dotyczące tej funkcji.

Ponadto jedna ma toounderstand hello rozliczeń efekty podczas pracy często z migawki obiektu blob, zgodnie z opisem w tym artykule: [zrozumienia sposobu migawki Naliczanie opłat](/rest/api/storageservices/understanding-how-snapshots-accrue-charges)— go nie jest &#39; t tak oczywiste jako za pomocą platformy Azure dyski wirtualne.

### <a name="sap-hana-data-consistency-when-taking-storage-snapshots"></a>Spójność danych SAP HANA podejmując pamięci masowej migawki

Zgodność aplikacji i systemu plików jest złożonych problemów podczas wykonywania migawki magazynu. Hello Najprostszym sposobem tooavoid problemów może być tooshut dół SAP HANA lub może nawet hello całej maszyny wirtualnej. Zamknięcie systemu może być doable pokaz lub prototypu lub nawet programistycznej, ale nie jest opcją systemu produkcji.

Na platformie Azure co ma tookeep pamiętać, że hello funkcja migawki obiektu blob systemu Azure &#39; t zagwarantowania spójności systemu plików. Współpracuje jednak za pomocą hello SAP HANA migawki funkcji, dopóki dotyczy tylko jednego dysku wirtualnego. Ale nawet w przypadku jednego dysku, dodatkowe elementy toobe zaznaczone. [SAP 2039883 Uwaga](https://launchpad.support.sap.com/#/notes/2039883) zawiera ważne informacje dotyczące kopii zapasowych SAP HANA za pomocą magazynu migawek. Na przykład informacje o, przy użyciu systemu plików XFS hello, jest konieczne toorun **xfs\_freeze** przed rozpoczęciem magazynu migawek spójności tooguarantee (zobacz [xfs\_freeze(8) - man systemu Linux Strona](https://linux.die.net/man/8/xfs_freeze) szczegółowe informacje na temat **xfs\_Zablokuj**).

temat Hello spójności staje się nawet trudniejsze w przypadku, gdy system pojedynczy plik obejmuje wiele dysków/woluminów. Na przykład za pomocą mdadm lub LVM i stosowanie. Witaj Uwaga SAP wymienione powyżej stany:

_&quot;Jednak należy pamiętać, że system przechowywania hello ma spójności tooguarantee We/Wy podczas tworzenia migawki magazynu dla każdego woluminu danych SAP HANA, tj. musi ona mieć niepodzielną operację tworzenia migawek woluminu specyficznych dla usług danych SAP HANA.&quot;_

Zakładając, że jest system plików XFS obejmującej cztery dyski wirtualne platformy Azure, hello poniższe kroki zawierają migawki spójne, która reprezentuje obszar danych HANA hello:

- Przygotowanie HANA migawki
- Zablokuj hello systemu plików (na przykład użyć **xfs\_Zablokuj**)
- Utwórz wszystkie migawki obiektu blob konieczne na platformie Azure
- Odblokuj hello systemu plików
- Potwierdź hello HANA migawki

Zalecane jest procedurą hello toouse powyżej w wszystkich przypadków toobe po stronie bezpieczne hello, niezależnie od tego, który system plików. Lub, jeśli jest to jeden dysk lub rozkładanie za pośrednictwem mdadm lub LVM na wielu dyskach.

Jest ważne tooconfirm hello HANA migawka. Z powodu toohello &quot;kopii przy zapisie,&quot; SAP HANA nie mogą wymagać dodatkowego miejsca na dysku w tym trybie przygotowania migawki. &#39; s również nie jest możliwe toostart nowych kopii zapasowych do momentu hello SAP HANA migawki został potwierdzony.

Usługa Kopia zapasowa Azure korzysta z maszyny Wirtualnej Azure rozszerzenia tootake nad spójności systemu plików hello. Te rozszerzenia maszyny Wirtualnej nie są dostępne do użycia autonomicznego. Jeden z nich ma nadal toomanage spójności SAP HANA. Zobacz artykuł pokrewne hello [SAP HANA Azure Backup na poziomie plików](sap-hana-backup-file-level.md) Aby uzyskać więcej informacji.

### <a name="sap-hana-backup-scheduling-strategy"></a>SAP HANA strategii harmonogramu wykonywania kopii zapasowych

Artykuł SAP HANA Hello [planowania Your kopii zapasowej i odzyskiwania strategii](https://help.sap.com/saphelp_hanaplatform/helpdata/en/ef/085cd5949c40b788bba8fd3c65743e/content.htm) stanów a basic Planowanie kopii zapasowych toodo:

- Magazynu migawek (dziennie)
- Kopia zapasowa pełnych danych przy użyciu formatu pliku lub bacint (raz w tygodniu)
- Kopie zapasowe dziennika automatyczne

Opcjonalnie co można przejść całkowicie bez migawek magazynu; mogły one zostać zastąpione przez kopie zapasowe delta HANA, na przykład przyrostowa lub różnicowej kopii zapasowych (zobacz [różnicowe kopie zapasowe](https://help.sap.com/saphelp_hanaplatform/helpdata/en/c3/bb7e33bb571014a03eeabba4e37541/content.htm)).

Przewodnik administracji HANA Hello zawiera przykładową listę. Sugeruje jedną odzyskać SAP HANA tooa określonego punktu w czasie przy użyciu powitania po sekwencji kopii zapasowych:

1. Pełne kopie zapasowe
2. Różnicowej kopii zapasowej
3. Przyrostowa kopia zapasowa 1
4. Przyrostowa kopia zapasowa 2
5. Kopie zapasowe dziennika

Dotyczące dokładnego harmonogram jako toowhen i jak często określonego typu kopii zapasowej powinno się zdarzyć, nie jest możliwe toogive ogólne wytyczne — jest zbyt właściwe dla klienta i zależy od liczby zmian danych występują w systemie hello. Jeden podstawowe zalecenie stronie SAP, które są widoczne jako ogólne wskazówki, jest jeden HANA pełnej toomake w kopii zapasowej raz w tygodniu.
Dotyczące kopii zapasowych dziennika, zobacz dokumentację SAP HANA hello [kopie zapasowe dziennika](https://help.sap.com/saphelp_hanaplatform/helpdata/en/c3/bb7e33bb571014a03eeabba4e37541/content.htm).

SAP zaleca, wykonanie niektórych celów hello tookeep katalogu kopii zapasowej z rośnie nieograniczonej (zobacz [Housekeeping katalogu kopii zapasowej i przechowywania kopii zapasowych](http://help.sap.com/saphelp_hanaplatform/helpdata/en/ca/c903c28b0e4301b39814ef41dbf568/content.htm)).

### <a name="sap-hana-configuration-files"></a>Pliki konfiguracji SAP HANA

Jak wspomniano w hello — często zadawane pytania w [1642148 Uwaga SAP](https://launchpad.support.sap.com/#/notes/1642148), pliki konfiguracji SAP HANA hello nie są częścią standardowej HANA kopii zapasowej. Nie są one niezbędne toorestore systemu. Hello HANA konfiguracji można zmienić ręcznie po przywróceniu hello. W przypadku, gdy jeden chcieliby tooget hello tej samej konfiguracji niestandardowej w procesie przywracania hello jest konieczne tooback się pliki konfiguracji HANA hello oddzielnie.

Gdy standardowe HANA kopie zapasowe będą tooa dedykowanego HANA pliku kopii zapasowej systemu, co można również skopiować toohello pliki konfiguracji hello sam kopii zapasowej systemu plików, a następnie skopiuj wszystkie miejscem docelowym magazynu ostatnim razem toohello, takich jak cool magazynu obiektów blob.

### <a name="sap-hana-cockpit"></a>SAP HANA w Panelu sterowania

SAP HANA w Panelu sterowania oferuje możliwość hello monitorowanie i zarządzanie SAP HANA za pośrednictwem przeglądarki. Umożliwia również obsługę kopii zapasowych SAP HANA i dlatego mogą być używane jako alternatywne tooSAP HANA Studio i ABAP DBACOCKPIT (zobacz [SAP HANA w Panelu sterowania](https://help.sap.com/saphelp_hanaplatform/helpdata/en/73/c37822444344f3973e0e976b77958e/content.htm) Aby uzyskać więcej informacji).

![Na poniższym rysunku pokazano hello ekranu administracyjnego bazy danych SAP HANA Panelu sterowania](media/sap-hana-backup-guide/image004.png)

Ten rysunek przedstawia hello ekranu administracyjnego bazy danych SAP HANA Panelu sterowania, a hello Kafelek tworzenia kopii zapasowej na powitania po lewej. Oglądanie kafelka kopii zapasowej hello wymaga odpowiednich uprawnień użytkowników dla konta logowania.

![Kopie zapasowe mogą być monitorowane w Panelu sterowania programu SAP HANA, gdy są one uruchomione](media/sap-hana-backup-guide/image005.png)

Kopie zapasowe mogą być monitorowane w Panelu sterowania programu SAP HANA, gdy są uruchomione, a po zakończeniu wszystkich szczegółów tworzenia kopii zapasowej hello są dostępne.

![Przykład za pomocą przeglądarki Firefox na SLES 12 maszyny Wirtualnej platformy Azure przy użyciu pulpitu Gnome](media/sap-hana-backup-guide/image006.png)

wprowadzono Hello poprzednich zrzutach ekranu z maszyny Wirtualnej systemu Windows Azure. Ten zestaw jest na przykład za pomocą przeglądarki Firefox na SLES 12 maszyny Wirtualnej platformy Azure przy użyciu Gnome pulpitu. Pokazuje harmonogramy tworzenia kopii zapasowej SAP HANA toodefine opcji hello w Panelu sterowania programu SAP HANA. Zgodnie z jedną można również sprawdzić, sugeruje daty/godziny jako prefiksu hello plików kopii zapasowej. W systemie SAP HANA Studio prefiks domyślne hello jest &quot;COMPLETE\_danych\_kopii zapasowej&quot; podczas wykonywania kopii zapasowej całego pliku. Zaleca się użycie unikatowy prefiks.

### <a name="sap-hana-backup-encryption"></a>SAP HANA szyfrowania kopii zapasowych

SAP HANA oferuje szyfrowania danych i dziennika. Jeśli nie są zaszyfrowane SAP HANA danych i dziennika, następnie hello kopii zapasowych również nie są szyfrowane. Jest zapasowej toouse klienta toohello jakiegoś rozwiązań innych firm tooencrypt hello SAP HANA tworzenia kopii zapasowych. Zobacz [danych i szyfrowania woluminu dziennika](https://help.sap.com/saphelp_hanaplatform/helpdata/en/dc/01f36fbb5710148b668201a6e95cf2/content.htm) toofind więcej informacji na temat szyfrowania SAP HANA.

W systemie Microsoft Azure klient może wykorzystać hello tooencrypt funkcji szyfrowania maszyn wirtualnych IaaS. Na przykład jeden można użyć danych dedykowanych dysków dołączonych toohello maszyny Wirtualnej, które są używane toostore SAP HANA kopii zapasowych, a następnie kopie tych dysków.

Usługa Kopia zapasowa Azure może obsługiwać maszyny wirtualne/dyskach zaszyfrowanych (zobacz [jak tooback zapasowej i przywracania szyfrowane maszyn wirtualnych w usłudze Kopia zapasowa Azure](../../../backup/backup-azure-vms-encryption.md)).

Inną opcją czy hello toomaintain SAP HANA wirtualna i jej dyski bez szyfrowania i przechowywania plików kopii zapasowych SAP HANA hello na koncie magazynu, dla którego włączono szyfrowania (zobacz [szyfrowanie usługi Magazyn Azure dla danych magazynowanych](../../../storage/common/storage-service-encryption.md)) .

## <a name="test-setup"></a>Ustawienia testu

### <a name="test-virtual-machine-on-azure"></a>Testowej maszyny wirtualnej na platformie Azure

Instalacja SAP HANA w maszynie Wirtualnej platformy Azure GS5 została użyta dla hello następujące testy wykonywania kopii zapasowej i przywracania.

![Na poniższym rysunku pokazano część hello Azure omówienie portalu hello HANA testowej maszyny Wirtualnej](media/sap-hana-backup-guide/image007.png)

Na poniższym rysunku pokazano część hello Azure omówienie portalu hello HANA testowej maszyny Wirtualnej.

### <a name="test-backup-size"></a>Rozmiar kopii zapasowej testu

![Tę wartość została pobrana z kopii zapasowej konsoli hello w HANA Studio i przedstawia rozmiar pliku kopii zapasowej hello 229 GB dla serwera indeksu HANA hello](media/sap-hana-backup-guide/image008.png)

Fikcyjny tabeli został wypełniony tooget danych rozmiar kopii zapasowej danych ogólnych, ponad 200 GB tooderive realistyczne danych dotyczących wydajności. Rysunek Hello została pobrana z kopii zapasowej konsoli hello w HANA Studio i przedstawia rozmiar pliku kopii zapasowej hello 229 GB dla serwera indeksu HANA hello. Dla testów hello hello domyślnego tworzenia kopii zapasowej prefiksu "COMPLETE_DATA_BACKUP" w SAP HANA Studio została użyta. W systemach rzeczywistej produkcji lepszym rozwiązaniem prefiks powinien być zdefiniowany. Panel sterowania programu SAP HANA sugeruje daty/godziny.

### <a name="test-tool-toocopy-files-directly-tooazure-storage"></a>Toocopy narzędzie Test bezpośrednio pliki tooAzure magazynu

pliki kopii zapasowej SAP HANA tootransfer bezpośrednio tooAzure magazynu obiektów blob lub udziały plików platformy Azure, hello blobxfer narzędzie użyto ponieważ obsługuje ona zarówno elementy docelowe i można łatwo zintegrować skryptów automatyzacji powodu tooits interfejsu wiersza polecenia. Narzędzie blobxfer Hello jest dostępne na [GitHub](https://github.com/Azure/blobxfer).

### <a name="test-backup-size-estimation"></a>Szacowanie rozmiaru kopii zapasowej testu

Jest ważne tooestimate hello rozmiar kopii zapasowej programu SAP HANA. Ta Szacowana pomaga tooimprove wydajności, definiując hello rozmiar maksymalny pliku kopii zapasowej dla liczby plików kopii zapasowej z powodu tooparallelism podczas kopiowania plików. (Te szczegóły opisano szczegółowo w dalszej części tego artykułu). Co należy również postanowić, czy toodo pełnej kopii zapasowej lub różnicowej kopii zapasowej (przyrostowe lub różnicowa).

Na szczęście istnieje prostej instrukcji SQL szacowany rozmiar hello pliki kopii zapasowej hello: **wybierz \* z M\_kopii zapasowej\_rozmiar\_uzyskać szacunkowe wartości** (zobacz [ Szacowana hello miejsca potrzebne w hello systemu plików dla kopii zapasowej danych](https://help.sap.com/saphelp_hanaplatform/helpdata/en/7d/46337b7a9c4c708d965b65bc0f343c/content.htm)).

![dane wyjściowe Hello tej instrukcji SQL odpowiada prawie dokładnie hello rzeczywisty rozmiar hello pełne dane z kopii zapasowej na dysku](media/sap-hana-backup-guide/image009.png)

Dla systemu testowego hello hello dane wyjściowe w instrukcji SQL zgodne prawie dokładnie hello rzeczywisty rozmiar hello pełne dane z kopii zapasowej na dysku.

### <a name="test-hana-backup-file-size"></a>Rozmiar pliku kopii zapasowej HANA testu

![Konsola kopii zapasowej HANA Studio Hello pozwala jeden toorestrict hello maksymalny rozmiar plików HANA kopii zapasowej](media/sap-hana-backup-guide/image010.png)

Konsola kopii zapasowej HANA Studio Hello pozwala jeden toorestrict hello maksymalny rozmiar plików HANA kopii zapasowej. W środowisku próbki hello tej funkcji umożliwia możliwe tooget pliki kopii zapasowej na mniejsze wielu zamiast jeden plik kopii zapasowej 230 GB. Pliki mają mniejszy rozmiar, ma znaczący wpływ na wydajność (zobacz artykuł pokrewne hello [SAP HANA Azure Backup na poziomie plików](sap-hana-backup-file-level.md)).

## <a name="summary"></a>Podsumowanie

Na podstawie hello wyników testu hello następujące tabele Pokaż zalet i wad tooback rozwiązań zapasowych uruchomionych na maszynach wirtualnych Azure bazy danych SAP HANA.

**Utwórz kopię zapasową systemu plików toohello SAP HANA i skopiuj pliki kopii zapasowej później toohello miejsce docelowe kopii zapasowej końcowego**

|Rozwiązanie                                           |Specjaliści                                 |Wady                                  |
|---------------------------------------------------|-------------------------------------|--------------------------------------|
|Zachowaj kopie zapasowe HANA dysków maszyny Wirtualnej                      |Nie działań na dodatkowe Zarządzanie     |Eats miejsca na dysku lokalnym maszyny Wirtualnej           |
|Blobxfer narzędzia toocopy pliki kopii zapasowej tooblob magazynu |Równoległość toocopy wielu plików, wybór toouse chłodnych obiektu blob magazynu | Konserwacja dodatkowe narzędzia i skrypty niestandardowe | 
|Kopiowanie obiektów blob za pośrednictwem programu Powershell lub interfejsu wiersza polecenia                    |Dodatkowe narzędzia niezbędne, można osiągnąć za pomocą programu Azure Powershell lub interfejsu wiersza polecenia |ręczny proces, klient ma tootake nad wykonywania skryptów i zarządzania skopiowane obiekty BLOB do odtworzenia|
|Skopiuj tooNFS udziału                                  |Przetwarzanie końcowe kopii zapasowej plików na innych maszyn wirtualnych bez wpływu na serwerze HANA hello|Powolne proces kopiowania|
|Blobxfer kopiowania tooAzure usługi plików                |Nie będzie jeść miejsca na dyskach lokalnych maszyn wirtualnych|Nie bezpośrednio zapisać pomocy technicznej przez HANA kopii zapasowej, ograniczenie rozmiaru udziału plików dla 5 TB|
|Agent usługi Kopia zapasowa Azure                                 | Byłoby preferowaną rozwiązania         | Obecnie nie jest dostępna w systemie Linux    |



**Kopia zapasowa SAP HANA oparty na pamięci masowej migawki**

|Rozwiązanie                                           |Specjaliści                                 |Wady                                  |
|---------------------------------------------------|-------------------------------------|--------------------------------------|
|Usługa Kopia zapasowa Azure                               | Zezwala na podstawie kopii zapasowej maszyny Wirtualnej na migawki obiektu blob | Używając nie przywracania na poziomie plików, wymaga hello Tworzenie nowej maszyny Wirtualnej dla procesu przywracania hello, który następnie pociąga za sobą konieczność hello klucza licencji SAP HANA|
|Migawki obiektu blob ręcznie                              | Elastyczność toocreate i Przywróć określone dysków maszyny Wirtualnej bez zmieniania hello Unikatowy identyfikator maszyny Wirtualnej|Wszystkie czynności ręcznych, którego toobe programach powitania klienta|

## <a name="next-steps"></a>Następne kroki
* [SAP HANA kopia zapasowa Azure na poziomie plików](sap-hana-backup-file-level.md) opisuje hello opartych na plikach opcję tworzenia kopii zapasowej.
* [Kopia zapasowa SAP HANA oparte na magazynu migawek](sap-hana-backup-storage-snapshots.md) opisuje hello magazynu związanych z migawką opcję tworzenia kopii zapasowej.
* toolearn jak tooestablish wysokiej dostępności i planu odzyskiwania po awarii programu SAP HANA na platformie Azure (wystąpienia duże), zobacz [SAP HANA (duże wystąpień) wysokiej dostępności i odzyskiwania po awarii na platformie Azure](hana-overview-high-availability-disaster-recovery.md).
