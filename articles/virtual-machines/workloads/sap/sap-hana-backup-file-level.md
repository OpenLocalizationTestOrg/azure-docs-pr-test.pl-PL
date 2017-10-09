---
title: "Kopia zapasowa Azure HANA na poziomie plików aaaSAP | Dokumentacja firmy Microsoft"
description: "Istnieją dwa główne kopii zapasowej możliwości SAP HANA na maszynach wirtualnych Azure, w tym artykule omówiono SAP HANA kopia zapasowa Azure na poziomie plików"
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
ms.openlocfilehash: d5a55de5634ac7724e7fd0fa3760c6c408c3db74
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="sap-hana-azure-backup-on-file-level"></a>SAP HANA Azure Backup na poziomie plików

## <a name="introduction"></a>Wprowadzenie

To jest częścią serii trzyczęściowej pokrewne artykuły kopii zapasowej SAP HANA. [Podręcznik tworzenia kopii zapasowej programu SAP HANA na maszynach wirtualnych Azure](./sap-hana-backup-guide.md) zawiera omówienie i informacje wprowadzające, i [SAP HANA kopii zapasowych oparte na magazynu migawek](./sap-hana-backup-storage-snapshots.md) obejmuje hello magazynu związanych z migawką opcję tworzenia kopii zapasowej.

Spojrzenie na powitania rozmiary maszyn wirtualnych Azure, co Zobacz, czy GS5 umożliwia 64 dysków dołączonych danych. W dużych systemach SAP HANA już być wykonana plików danych i dziennika, prawdopodobnie w połączeniu z oprogramowaniem RAID dla dysku optymalną wydajność We/Wy duża liczba dysków. następnie pytanie Hello jest, gdzie toostore SAP HANA kopii zapasowej plików, które może zapełnić danych hello dołączone dyski w czasie? Zobacz [rozmiary maszyn wirtualnych systemu Linux na platformie Azure](../../linux/sizes.md) hello maszyny Wirtualnej Azure rozmiar tabel.

W tej chwili dostępne w usłudze Kopia zapasowa Azure jest integracja kopii zapasowej nie SAP HANA. standardowy sposób Hello toomanage wykonywania kopii zapasowej/przywracania na poziomie pliku hello jest z kopii zapasowej za pomocą programu SAP HANA Studio lub za pomocą instrukcji SAP HANA SQL opartych na plikach. Zobacz [SAP HANA SQL i odwołanie widoków systemu](https://help.sap.com/hana/SAP_HANA_SQL_and_System_Views_Reference_en.pdf) Aby uzyskać więcej informacji.

![Poniższy rysunek pokazuje okno dialogowe hello elementu menu kopii zapasowej hello w SAP HANA Studio](media/sap-hana-backup-file-level/image022.png)

Na poniższym rysunku pokazano okna dialogowego hello elementu menu kopii zapasowej hello w SAP HANA Studio. W przypadku wybrania typu &quot;pliku&quot; jeden ma toospecify ścieżki w systemie plików hello gdzie SAP HANA zapisuje hello pliki kopii zapasowej. Przywracanie działa hello tak samo.

Chociaż ten wybór wydaje się proste i bezpośrednio do przodu, istnieją pewne zagadnienia. Jak wspomniano wcześniej, maszyny Wirtualnej platformy Azure obowiązuje ograniczenie liczby dysków z danymi, które można dołączyć. Być może pliki kopii zapasowej SAP HANA toostore pojemności dla systemów plików hello hello maszyny Wirtualnej, w zależności od wielkości hello hello bazy danych i dysku przepływności wymagań, które mogą dotyczyć oprogramowania RAID przy użyciu stosowanie w danych w wielu dysków. Różne opcje przenoszenia tych plików kopii zapasowej i zarządzanie ograniczenia rozmiaru plików i wydajności podczas obsługi terabajtów danych, znajdują się w dalszej części tego artykułu.

Inną opcją, który zapewnia większą swobodę dotyczące całkowitej pojemności, jest magazynu obiektów blob platformy Azure. Podczas pojedynczego obiektu blob jest również ograniczony too1 TB, całkowita pojemność hello kontenera pojedynczego obiektu blob jest obecnie 500 TB. Ponadto udostępnia klientom hello choice tooselect tak zwane &quot;chłodnych&quot; obiektu blob magazynu, który ma kosztów korzyści. Zobacz [usługi Azure Blob Storage: Hot i cool warstw magazynowania](../../../storage/blobs/storage-blob-storage-tiers.md) szczegółowe informacje na temat magazynu chłodnego obiektów blob.

Dla dodatkowego bezpieczeństwa należy użyć magazynu z replikacją geograficzną konta toostore hello SAP HANA tworzenia kopii zapasowych. Zobacz [replikacja usługi Azure Storage](../../../storage/common/storage-redundancy.md) szczegółowe informacje o replikacji konta magazynu.

Co można umieścić dedykowanych dysków VHD dla kopii zapasowych SAP HANA w konto dedykowanych dla magazynu kopii zapasowej, które jest replikacją geograficzną. W przeciwnym razie jedną można skopiować hello wirtualne dyski twarde, które przechowują kopie zapasowe SAP HANA hello konta magazynu z replikacją geograficzną tooa lub tooa konta magazynu, który znajduje się w innym regionie.

## <a name="azure-backup-agent"></a>Agent usługi Kopia zapasowa Azure

Toonot opcja hello Azure oferuje kopii zapasowej kopię zapasową tylko pełną maszyn wirtualnych, ale również plików i katalogów za pomocą agenta kopii zapasowej hello, którym został zainstalowany na system operacyjny gościa hello toobe. Jednak począwszy od grudnia 2016 r. Ten agent jest obsługiwana tylko w systemie Windows (zobacz [kopia zapasowa systemu Windows Server lub klienta tooAzure, przy użyciu modelu wdrażania usługi Resource Manager hello](../../../backup/backup-configure-vault.md)).

Obejście tego problemu jest kopią toofirst SAP HANA tooa pliki kopii zapasowej maszyny Wirtualnej systemu Windows Azure (na przykład za pośrednictwem udziału SAMBA), a następnie użyj hello Azure agenta kopii zapasowej z tego miejsca. Chociaż jest technicznie możliwe, go czy zwiększenia złożoności i spowolnić hello kopii zapasowej lub przywracania sobą powodu kopiowania toohello między hello systemu Linux i hello maszyny Wirtualnej systemu Windows. Nie jest zalecane toofollow tej metody.

## <a name="azure-blobxfer-utility-details"></a>Szczegóły narzędzia Azure blobxfer

toostore katalogów i plików w magazynie Azure, co można użyć interfejsu wiersza polecenia lub programu PowerShell lub Opracuj narzędzie przy użyciu jednej z hello [zestawów SDK usługi Azure](https://azure.microsoft.com/downloads/). Również jest gotowe do użycia narzędzie AzCopy, kopiowania danych tooAzure magazynu, ale jest tylko systemu Windows (zobacz [Transfer danych za pomocą narzędzia wiersza polecenia AzCopy hello](../../../storage/common/storage-use-azcopy.md)).

W związku z tym blobxfer została użyta do kopiowania plików kopii zapasowej SAP HANA. Jest typu open source, używane przez wielu klientów w środowisku produkcyjnym i dostępne w [GitHub](https://github.com/Azure/blobxfer). To narzędzie umożliwia jednego toocopy danych bezpośrednio tooeither Azure blob magazynu lub udział plików na platformę Azure. Oferuje szeroką gamę przydatne funkcje, takie jak wyznaczania wartości skrótu md5 lub automatyczne równoległości podczas kopiowania katalogu z wieloma plikami.

## <a name="sap-hana-backup-performance"></a>SAP HANA wydajności tworzenia kopii zapasowych

![Jest to zrzut ekranu konsoli hello SAP HANA kopii zapasowej w SAP HANA Studio](media/sap-hana-backup-file-level/image023.png)

Ten zrzut ekranu jest hello SAP HANA kopii zapasowej w konsoli programu SAP HANA Studio. Zajęło około 42 minut toodo hello tworzenia kopii zapasowej z hello 230 GB na dysk pojedynczy Azure standardowy magazyn dołączony toohello HANA maszyny Wirtualnej przy użyciu systemu plików XFS.

![Ten zrzut ekranu jest YaST na powitania SAP HANA testowej maszyny Wirtualnej](media/sap-hana-backup-file-level/image024.png)

Ten zrzut ekranu jest YaST na powitania SAP HANA testowej maszyny Wirtualnej. Jak wspomniano wcześniej, jeden Zobacz hello 1 TB jednego dysku do utworzenia kopii zapasowej SAP HANA. Zajęło około 42 minut toobackup 230 GB. Ponadto zostały dołączone pięć dysków 200 GB i md0 RAID oprogramowania utworzona zastosowanie rozkładania na podstawie tych pięciu dysków danych Azure.

![Powtarzanie hello sam kopii zapasowej na oprogramowaniem RAID z rozkładanie przez pięć dołączone dyski danych usługi Azure standard storage](media/sap-hana-backup-file-level/image025.png)

Hello powtarzających się sam kopii zapasowej na oprogramowaniem RAID z rozkładanie przez pięć podłączone wykonywania kopii zapasowej hello dysków przełączony w tryb danych usługi Azure standard storage 42 minut dół too10 minut. bez buforowania toohello maszyny Wirtualnej zostały dołączone dyski Hello. Dlatego jest oczywiste jak ważna przepływność zapisu dysku jest hello czas tworzenia kopii zapasowej. Jeden można następnie przełącznika tooAzure premium magazynu toofurther przyspieszenia procesu hello, aby uzyskać optymalną wydajność. Ogólnie rzecz biorąc magazynu Azure premium powinien być używany dla systemów produkcyjnych.

## <a name="copy-sap-hana-backup-files-tooazure-blob-storage"></a>Skopiuj SAP HANA pliki kopii zapasowej tooAzure obiektu blob magazynu

Zgodnie z grudnia 2016 r. hello najlepiej pliki kopii zapasowej SAP HANA opcja tooquickly magazynu jest magazynu obiektów blob platformy Azure. Jeden kontener pojedynczego obiektu blob jest objęta limitem 500 TB, wystarczająca dla większości systemów SAP HANA, uruchomione na maszynie wirtualnej GS5 na platformie Azure, kopie zapasowe tookeep wystarczające SAP HANA. Klienci mają hello wybór między &quot;gorących&quot; i &quot;zimnych&quot; magazynu obiektów blob (zobacz [usługi Azure Blob Storage: Hot i cool warstw magazynowania](../../../storage/blobs/storage-blob-storage-tiers.md)).

Za pomocą narzędzia blobxfer hello jest łatwe toocopy pliki kopii zapasowej SAP HANA hello bezpośrednio tooAzure magazynu obiektów blob.

![W tym miejscu jedną Zobacz pliki hello pełnej kopii zapasowej pliku SAP HANA](media/sap-hana-backup-file-level/image026.png)

W tym miejscu jedną Zobacz pliki hello pełnej kopii zapasowej pliku SAP HANA. Istnieją cztery pliki i hello największych z nich ma około 230 GB.

![Zajęło około 3000 sekund 230 GB hello toocopy tooan kontenera obiektów blob konta magazynu Azure w warstwie standardowa](media/sap-hana-backup-file-level/image027.png)

Nie używa skrótu md5 w teście początkowej hello, zajęło około 3000 sekund kontenera obiektów blob konta usługi Azure standard storage tooan toocopy hello 230 GB.

![Na tym zrzucie ekranu pokazano co Zobacz, jak wygląda na powitania portalu Azure](media/sap-hana-backup-file-level/image028.png)

Na tym zrzucie ekranu pokazano co Zobacz, jak wygląda na powitania portalu Azure. Kontener obiektu blob o nazwie &quot;sap hana kopie zapasowe&quot; został utworzony i zawiera obiekty BLOB hello czterech, które zawierają pliki kopii zapasowej hello SAP HANA. Jeden z nich ma rozmiar około 230 GB.

Konsola kopii zapasowej HANA Studio Hello pozwala jeden toorestrict hello maksymalny rozmiar plików HANA kopii zapasowej. W środowisku próbki hello wyższą wydajność dzięki czemu możliwe toohave wielu mniejszych kopii zapasowej plików, zamiast jednego dużego pliku 230 GB.

![Ustawienie limitu rozmiaru pliku kopii zapasowej hello na powitania HANA po stronie &#39; t zwiększyć czas tworzenia kopii zapasowej hello](media/sap-hana-backup-file-level/image029.png)

Ustawienie limitu rozmiaru pliku kopii zapasowej hello na powitania HANA po stronie &#39; t zwiększyć hello wykonywania kopii zapasowej, ponieważ hello pliki są zapisywane po kolei, jak pokazano na poniższym rysunku. limit rozmiaru pliku Hello ustawiono too60 GB, więc pojedynczy plik utworzona kopia zapasowa hello cztery duże pliki danych zamiast hello 230 GB.

![Równoległość tootest hello blobxfer narzędzia, hello maksymalny rozmiar HANA kopii zapasowych następnie ustawiono too15 GB](media/sap-hana-backup-file-level/image030.png)

Równoległość tootest hello blobxfer narzędzia, hello maksymalny rozmiar HANA kopii zapasowych następnie ustawiono too15 GB, co spowodowało 19 pliki kopii zapasowej. Ta konfiguracja wprowadzane hello czas dla magazynu obiektów blob tooAzure blobxfer toocopy hello 230 GB od 3000 sekund w dół too875 sekund.

Ten wynik jest powodu toohello limit 60 MB/s do zapisywania obiektów blob platformy Azure. Równoległość za pomocą wielu obiektów blob rozwiązuje "wąskie gardło" hello, ale wadą interfejsu: zwiększanie wydajności hello blobxfer narzędzie toocopy wszystkie te tooAzure pliki kopii zapasowej HANA magazynu obiektów blob umieszcza obciążenia na powitania HANA maszyny Wirtualnej i hello sieci. Staje się negatywny wpływ na działanie systemu HANA.

## <a name="blob-copy-of-dedicated-azure-data-disks-in-backup-software-raid"></a>Kopiowania obiektu blob danych Azure dedykowanych dysków w oprogramowania kopii zapasowej RAID

W odróżnieniu od hello ręczne danych dysku kopii zapasowej maszyny Wirtualnej w tej metody, co nie kopię zapasową wszystkich dysków danych hello na wirtualna toosave hello całej SAP instalacji, włącznie z danymi HANA HANA rejestruje plików i plików konfiguracji. Zamiast tego pomysł hello to oprogramowanie w wersji dedykowanej toohave RAID z rozkładanie przez wielu danych Azure wirtualne dyski twarde do przechowywania pełnej kopii zapasowej pliku SAP HANA. Kopiuje jeden tylko te dyski, których kopia zapasowa SAP HANA hello. Można łatwo zachowane w dedykowane konto magazynu kopii zapasowych HANA lub dołączony tooa dedykowanego &quot;kopii zapasowej maszyny Wirtualnej zarządzania&quot; dla dalszego przetwarzania.

![Wszystkie dyski VHD, które są zaangażowane zostały skopiowane przy użyciu hello ** start-azurestorageblobcopy ** polecenia programu PowerShell](media/sap-hana-backup-file-level/image031.png)

Po oprogramowania lokalne powitania toohello kopii zapasowej RAID, wszystkie wirtualne dyski twarde zaangażowany zostały skopiowane przy użyciu hello **start azurestorageblobcopy** polecenia programu PowerShell (zobacz [Start AzureStorageBlobCopy](/powershell/module/azure.storage/start-azurestorageblobcopy)). Ponieważ wpływa tylko na hello dedykowanego systemu plików do przechowywania plików kopii zapasowej hello, nie ma żadnych problemów dotyczących SAP HANA spójności pliku danych lub dziennika na dysku hello. Zaletą tego polecenia jest to działa podczas hello maszyny Wirtualnej pozostaje w trybie online. toobe niektórych się, że żaden proces zapisuje zestawu kopii zapasowych rozłożonego toohello, należy się toounmount przed hello kopiowania obiektu blob i zainstalować go ponownie później. Lub jeden można użyć odpowiednich zbyt&quot;Zablokuj&quot; hello systemu plików. Na przykład za pomocą xfs\_zablokować systemu plików XFS hello.

![Ten zrzut ekranu przedstawia hello listę obiektów blob w kontenerze wirtualne dyski twarde hello na powitania portalu Azure](media/sap-hana-backup-file-level/image032.png)

Ten zrzut ekranu przedstawia hello listę obiektów blob w hello &quot;wirtualne dyski twarde&quot; kontenera na powitania portalu Azure. Hello zrzut ekranu przedstawia hello pięć wirtualne dyski twarde, które zostały dołączone tooserve maszyny Wirtualnej serwera SAP HANA toohello hello oprogramowania RAID tookeep SAP HANA kopii zapasowej plików. Przedstawiono również hello pięć kopii, które zostały pobrane za pomocą polecenia kopiowania obiektu blob hello.

![Do celów testowych, hello kopie dysków RAID oprogramowania kopii zapasowej SAP HANA hello zostały dołączone toohello serwera aplikacji maszyny Wirtualnej](media/sap-hana-backup-file-level/image033.png)

Do celów testowych, hello kopie dysków RAID oprogramowania kopii zapasowej SAP HANA hello zostały dołączone toohello serwera aplikacji maszyny Wirtualnej.

![Serwer aplikacji Hello maszyny Wirtualnej został zamknięty kopii dysku hello tooattach](media/sap-hana-backup-file-level/image034.png)

Serwer aplikacji Hello maszyny Wirtualnej został zamknięty kopii dysku hello tooattach. Po uruchomieniu hello maszyny Wirtualnej, dyski hello i hello RAID odkryto poprawnie (zainstalowany za pomocą identyfikatora UUID). Tylko punkt instalacji hello brakowało, który został utworzony za pomocą partycjonera YaST hello. Następnie kopii pliku kopii zapasowej SAP HANA hello stały się widoczne na poziomie systemu operacyjnego.

## <a name="copy-sap-hana-backup-files-toonfs-share"></a>Skopiuj pliki kopii zapasowej SAP HANA tooNFS wspólne

toolessen hello potencjalnego wpływu na powitania systemu SAP HANA z wydajnością lub dysku, co może warto przechowywać hello SAP HANA kopii zapasowej plików w udziale NFS. Technicznie działa, ale oznacza przy użyciu drugiej maszyny Wirtualnej platformy Azure jako host hello powitalne udziału NFS. Nie należy mały rozmiar maszyny Wirtualnej, ze względu na przepustowość sieci VM toohello. Może to spowodować znaczeniu, a następnie tooshut dół to &quot;kopii zapasowej maszyny Wirtualnej&quot; i przełączyć go tylko do wykonywania kopii zapasowej SAP HANA hello. Zapisywanie w systemie plików NFS udziału umieszcza obciążenia w sieci hello wpływ hello systemu SAP HANA, ale tylko Zarządzanie hello pliki kopii zapasowej później na powitania &quot;kopii zapasowej maszyny Wirtualnej&quot; czy wpłynęło na wszystkich hello systemu SAP HANA.

![Udziału NFS z innej maszyny Wirtualnej platformy Azure został zainstalowany toohello serwera SAP HANA maszyny Wirtualnej](media/sap-hana-backup-file-level/image035.png)

przypadek użycia hello tooverify systemu plików NFS, udziału NFS z innej maszyny Wirtualnej platformy Azure został zainstalowany toohello serwera SAP HANA maszyny Wirtualnej. Nie znaleziono żadnych specjalnych systemu plików NFS dostrajania stosowany.

![Kopia zapasowa hello toodo 1 godzinę i 46 minut zajęło bezpośrednio](media/sap-hana-backup-file-level/image036.png)

udziału NFS Hello jest szybkie rozłożony, takich jak hello jedną na powitania serwera SAP HANA. Niemniej jednak zajęło 1 godziny i minuty 46 toodo hello kopii zapasowej bezpośrednio w udziale NFS hello zamiast 10 minut, podczas zapisywania lokalnych tooa zestawem.

![alternatywne Hello nie znacznie szybsza, bo na 1 i godz.](media/sap-hana-backup-file-level/image037.png)

alternatywne Hello wykonywania kopii zapasowej tooa lokalnego rozłożony i kopiowanie toohello udziału NFS na poziomie systemu operacyjnego (prosty **cp - avr** polecenia) nie została znacznie szybciej. Zajęło 1 i godz..

Dlatego działa, ale wydajność nie został dobrej hello 230 GB kopii zapasowej testu. Będzie ona wyglądać większe dla wielu terabajtów.

## <a name="copy-sap-hana-backup-files-tooazure-file-service"></a>Skopiuj SAP HANA pliki kopii zapasowej tooAzure pliku usługi

Jest możliwe toomount udział plików Azure wewnątrz maszyny Wirtualnej systemu Linux na platformie Azure. Artykuł Hello [jak toouse magazyn plików Azure z systemem Linux](../../../storage/files/storage-how-to-use-files-linux.md) zawiera szczegółowe informacje na temat toodo go. Należy pamiętać, że jest obecnie limit przydziału 5 TB jeden udział plików na platformę Azure, a limit rozmiaru pliku o rozmiarze 1 TB na plik. Zobacz [cele dotyczące wydajności i skalowalności magazynu Azure](../../../storage/common/storage-scalability-targets.md) dla informacji na temat limitów magazynu.

Badania wykazały, jednak bez tworzenia kopii zapasowej SAP HANA &#39; t obecnie pracować bezpośrednio z tego rodzaju CIFS instalacji. Również jest podany w [1820529 Uwaga SAP](https://launchpad.support.sap.com/#/notes/1820529) który CIFS nie jest zalecane.

![Na poniższym rysunku pokazano wystąpił błąd w hello okna dialogowego kopii zapasowej w SAP HANA Studio](media/sap-hana-backup-file-level/image038.png)

Tej ilustracji przedstawiono wystąpił błąd w hello okna dialogowego kopii zapasowej w systemie SAP HANA Studio podczas próby tooback się bezpośrednio udział plików na platformę Azure zainstalowane CIFS tooa. Dzięki jedną ma toodo standardowe SAP HANA kopii zapasowej w systemie plików maszyny Wirtualnej najpierw, a następnie pliki kopii zapasowej hello z tooAzure występują usługa plików.

![Na poniższym rysunku pokazano zajęło o 929 sekund toocopy 19 SAP HANA pliki kopii zapasowej](media/sap-hana-backup-file-level/image039.png)

Na poniższym rysunku pokazano, że zajęło o toocopy 929 sekund 19 SAP HANA pliki kopii zapasowej o całkowitym rozmiarze około 230 GB udziału plików na platformę Azure toohello.

![struktury katalogów źródła Hello na powitania SAP HANA wirtualna został skopiowany toohello udziału plików na platformę Azure](media/sap-hana-backup-file-level/image040.png)

W tego zrzutu ekranu, co można zobaczyć, że struktury katalogów źródła hello na powitania SAP HANA wirtualna został skopiowany toohello udziału plików na platformę Azure: jeden katalog (hana\_kopii zapasowej\_fsl\_15 gb) i 19 poszczególnych plików kopii zapasowej.

Przechowywanie plików kopii zapasowej SAP HANA na pliki Azure mogą być interesujące opcja w przyszłości hello, gdy kopie zapasowe plików SAP HANA obsługuje go bezpośrednio. Lub gdy staje się możliwe toomount Azure pliki za pomocą systemu plików NFS i hello maksymalny limit przydziału jest znacznie większa niż 5 TB.

## <a name="next-steps"></a>Następne kroki
* [Podręcznik tworzenia kopii zapasowej programu SAP HANA na maszynach wirtualnych Azure](sap-hana-backup-guide.md) zapewnia przegląd oraz informacje o wprowadzenie.
* [Kopia zapasowa SAP HANA oparte na magazynu migawek](sap-hana-backup-storage-snapshots.md) opisuje hello magazynu związanych z migawką opcję tworzenia kopii zapasowej.
* toolearn jak tooestablish wysokiej dostępności i planu odzyskiwania po awarii programu SAP HANA na platformie Azure (wystąpienia duże), zobacz [SAP HANA (duże wystąpień) wysokiej dostępności i odzyskiwania po awarii na platformie Azure](hana-overview-high-availability-disaster-recovery.md).
