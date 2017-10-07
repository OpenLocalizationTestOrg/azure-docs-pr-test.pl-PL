---
title: "aaaUsing Import/Eksport Azure tootransfer danych tooand z magazynu obiektów blob | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toocreate importowanie i eksportowanie zadań w hello portalu Azure do przesyłania danych tooand z magazynu obiektów blob."
author: muralikk
manager: syadav
editor: tysonn
services: storage
documentationcenter: 
ms.assetid: 668f53f2-f5a4-48b5-9369-88ec5ea05eb5
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/17/2017
ms.author: muralikk
ms.openlocfilehash: 0be486a4badf2127b4613f3e9664e4cd308d3298
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-microsoft-azure-importexport-service-tootransfer-data-tooblob-storage"></a>Użyj hello Import/Eksport Microsoft Azure service tootransfer tooblob pamięci masowej
Witaj usługi Import/Eksport Azure umożliwia toosecurely transfer dużych ilości danych magazynu obiektów blob tooAzure przez wysyłanie centrum danych Azure tooan dysków twardych. Można również użyć tych danych tootransfer usługi z stacje dysków toohard magazynu obiektów blob platformy Azure i dostarczać tooyour lokacji lokalnej. Ta usługa jest odpowiednie w sytuacjach, w których ma tootransfer kilka terabajtów (TB) danych tooor z platformy Azure, ale przekazanie lub pobranie przez sieć hello jest praktyce powodu toolimited przepustowości lub wysokie koszty sieci.

Usługa Hello wymaga, że dyski twarde powinny być szyfrowane ze względów bezpieczeństwa hello danych funkcji BitLocker. Usługa Hello obsługuje zarówno hello klasycznym oraz usługi Azure Resource Manager kont magazynu (warstwy standardowa i chłodnego) występuje we wszystkich regionach hello publicznej platformy Azure. Musi być tooone dysków twardych z hello obsługiwane lokalizacje określone w dalszej części tego artykułu.

W tym artykule możesz dowiedzieć się więcej o usłudze Import/Eksport Azure hello i jak dyski tooship kopiowania tooand Twojego danych z magazynu obiektów Blob platformy Azure.

## <a name="when-should-i-use-hello-azure-importexport-service"></a>Kiedy używać usługi Import/Eksport Azure hello?
Należy rozważyć użycie usługi Import/Eksport Azure podczas przekazywania pobierania danych przez sieć hello jest zbyt wolno lub pobieranie dodatkowej przepustowości sieci jest drogie.

Tej usługi można użyć w scenariuszach takich jak:

* Migrowanie danych w chmurze toohello: szybkie przenoszenie dużych ilości danych tooAzure i tańszy sposób.
* Dystrybucję zawartości: szybko wysłać tooyour danych lokacji klienta.
* Kopia zapasowa: Wykonać kopie zapasowe toostore danych z lokalnego magazynu obiektów blob platformy Azure.
* Odzyskiwanie danych: odzyskać dużą ilość danych przechowywanych w magazynie obiektów blob i została ona wydana tooyour lokalizacji lokalnej.

## <a name="prerequisites"></a>Wymagania wstępne
W tej sekcji możemy listy hello wymagania wstępne wymagane toouse tej usługi. Przejrzyj je uważnie przed dostarczeniem dysków.

### <a name="storage-account"></a>Konto magazynu
Musi mieć istniejącej subskrypcji platformy Azure i co najmniej jednego konta toouse hello Import/Eksport usługi magazynu. Każde zadanie może być używane tootransfer tooor danych z tylko jednego konta magazynu. Innymi słowy zadanie pojedynczego importu/eksportu nie może obejmować wielu wielu kont magazynu. Aby uzyskać informacje dotyczące tworzenia nowego konta magazynu, zobacz [jak tooCreate konta magazynu](storage-create-storage-account.md#create-a-storage-account).

### <a name="blob-types"></a>Typy obiektów blob
Można użyć danych toocopy usługi Import/Eksport Azure zbyt**bloku** obiektów blob lub **strony** obiektów blob. Z drugiej strony, można wyeksportować tylko **bloku** obiektów blob, **strony** obiektów blob lub **Append** obiekty BLOB z usługi Azure storage przy użyciu tej usługi.

### <a name="job"></a>Zadanie
proces hello toobegin importowania tooor eksportowanie z magazynu obiektów Blob, należy najpierw utworzyć zadanie. Zadania mogą być zadania importu lub eksportu:

* Utwórz zadania importu danych tootransfer ma lokalnego tooblobs na koncie magazynu Azure.
* Utwórz zadanie eksportu danych tootransfer przechowywane jako obiekty BLOB w dysków toohard konta magazynu, które są dostarczane tooyou.s podczas tworzenia zadania, należy powiadomić hello Import/Eksport usługi, że będzie wysyłania jedną lub więcej twardych dysków tooan Azure Centrum danych.

* Dla zadania importu będzie wysyłania dyski twarde zawierające dane.
* Dla zadania eksportu zostanie wysyłania pustych dysków twardych.
* Można wysłać się too10 dyski twarde na zadanie.

Można utworzyć importu lub eksportu przy użyciu portalu Azure hello lub hello zadania [interfejsu API REST usługi Azure Storage importu/eksportu](/rest/api/storageimportexport).

### <a name="waimportexport-tool"></a>Narzędzie WAImportExport
pierwszy krok Hello tworzenia **zaimportować** zadania jest tooprepare dysków, które zostaną dostarczone do importu. tooprepare dysków, musisz połączyć go tooa lokalnego serwera i hello Uruchom narzędzie WAImportExport na powitania serwera lokalnego. To narzędzie WAImportExport ułatwia kopiowanie dysku toohello danych, szyfrowanie danych hello na powitania dysku za pomocą funkcji BitLocker i generowanie plików dziennika na dysku hello.

pliki dziennika Hello przechowują podstawowe informacje o zadaniu i dysku, takich jak numer seryjny dysk i nazwa konta magazynu. Ten plik dziennika nie jest przechowywana na dysku hello. Jest on używany podczas tworzenia zadania importu. Krok po kroku szczegóły zadania tworzenia znajduje się w dalszej części tego artykułu.

Narzędzie WAImportExport Hello jest zgodna tylko z 64-bitowym systemie operacyjnym Windows. Zobacz hello [systemu operacyjnego](#operating-system) sekcji dla określonych wersji systemu operacyjnego, obsługiwany.

Pobieranie najnowszej wersji hello hello [narzędzie WAImportExport](http://download.microsoft.com/download/3/6/B/36BFF22A-91C3-4DFC-8717-7567D37D64C5/WAImportExportV2.zip). Więcej informacji o używaniu hello narzędzia WAImportExport, można znaleźć hello [hello używanie narzędzia WAImportExport](storage-import-export-tool-how-to.md).

>[!NOTE]
>**Poprzednia wersja:** można [Pobierz WAImportExpot V1](http://download.microsoft.com/download/0/C/D/0CD6ABA7-024F-4202-91A0-CE2656DCE413/WaImportExportV1.zip) wersji hello narzędzia i odwoływać się za[Podręcznik użycia WAImportExpot V1](storage-import-export-tool-how-to-v1.md). WAImportExpot V1 wersję narzędzia hello zapewniają obsługę **przygotowywania dysków, gdy zapisywane są dane już wstępnie dysku toohello**. Również należy toouse WAImportExpot V1 narzędzia w przypadku klucza tylko hello dostępne klucza sygnatury dostępu Współdzielonego.

>

### <a name="hard-disk-drives"></a>Dyski twarde
Tylko 2,5 SSD lub 2,5-calowe lub 3,5" SATA II lub III wewnętrzny dysk twardy można używać z hello usługi Import/Eksport. Zadania importu/eksportu pojedynczego może mieć maksymalnie 10 HDD/SSD, a każdy dysk twardy poszczególnych/SSD może być o dowolnym rozmiarze. Duża liczba dysków można było ich rozmieszczenie wielu zadań i nie ma żadnych limitów hello liczby zadań, które mogą zostać utworzone. 

Dla zadania importu tylko hello pierwszy danych wolumin na dysku hello będą przetwarzane. ilość danych Hello musi być sformatowany jako NTFS.

> [!IMPORTANT]
> Zewnętrzne stacje dysków twardych dołączonych do wbudowanych adaptera USB nie są obsługiwane przez tę usługę. Nie można również używać dysku hello wewnątrz hello wielkość liter w wyrazie zewnętrzny dysk twardy; Nie wysyłaj zewnętrznych dysków twardych.
> 
> 

Poniżej znajduje się lista zewnętrznej karty USB używane toocopy danych toointernal dysków twardych. Anker 68UPSATAA - 02BU Anker 68UPSHHDS BU Startech SATADOCK22UE Orico 6628SUS3-C-BK (seria 6628) Thermaltake BlacX gorąca wymiany SATA zewnętrznych twardych dysków stacji dokującej (USB 2.0 & eSATA)

### <a name="encryption"></a>Szyfrowanie
Witaj danych na dysku hello musi być szyfrowana przy użyciu szyfrowania dysków funkcją BitLocker. Chroni dane, gdy są przesyłane.

Dla zadania importu istnieją dwa sposoby tooperform hello szyfrowania. Pierwszy sposób Hello jest toospecify hello opcją w przypadku przy użyciu pliku CSV zestawu danych podczas uruchamiania narzędzia WAImportExport hello podczas przygotowywania dysków. Hello drugim sposobem jest szyfrowanie funkcją BitLocker tooenable ręcznie na powitania dysku i określ klucz szyfrowania hello w hello driveset CSV, podczas uruchamiania wiersza polecenia narzędzia WAImportExport podczas przygotowywania dysków.

Dla zadań eksportu po Twoje dane są dyski skopiowanych toohello hello usługi będzie szyfrowania dysku hello za pomocą funkcji BitLocker przed dostarczeniem go tooyou Wstecz. klucz szyfrowania Hello zapewnia tooyou za pośrednictwem hello portalu Azure.  

### <a name="operating-system"></a>System operacyjny
Można użyć jednego powitania po 64-bitowych systemów operacyjnych tooprepare hello dysku twardego za pomocą hello narzędzia WAImportExport przed dostarczeniem hello tooAzure dysku:

Windows 7 Enterprise i Ultimate systemu Windows 7, Windows 8 Pro, Windows 8 Enterprise, Windows 8.1 Pro, Windows 8.1 Enterprise, Windows 10<sup>1</sup>, Windows Server 2008 R2, Windows Server 2012, Windows Server 2012 R2. Wszystkie systemy operacyjne obsługują szyfrowanie dysków funkcją BitLocker.

### <a name="locations"></a>Lokalizacje
Witaj usługi Import/Eksport Azure obsługuje kopiowania danych tooand wszystkie konta magazynu Azure publicznego. Mogą być tooone dysków twardych z następujących lokalizacji hello. Jeśli Twoje konto magazynu znajduje się w lokalizacji publicznej platformy Azure, która nie jest określana w tym miejscu lokalizacji alternatywnej wysyłki zapewnia się podczas tworzenia hello zadania za pomocą polecenia hello portalu Azure lub hello importowania i eksportowania interfejsu API REST.

Obsługiwane lokalizacje wysyłki:

* Wschodnie stany USA
* Zachodnie stany USA
* Wschodnie stany USA 2
* Zachodnie stany USA 2
* Środkowe stany USA
* Środkowo-północne stany USA
* Środkowo-południowe stany USA
* Środkowo-zachodnie stany USA
* Europa Północna
* Europa Zachodnia
* Azja Wschodnia
* Azja Południowo-Wschodnia
* Australia Wschodnia
* Australia Południowo-Wschodnia
* Japonia Zachodnia
* Japonia Wschodnia
* Indie Środkowe
* Indie Południowe
* Indie Zachodnie
* Kanada Środkowa
* Kanada Wschodnia
* Brazylia Południowa
* Korea Środkowa
* Administracja USA — Wirginia
* Administracja USA — Iowa
* US DoD — wschodnie stany
* US DoD — środkowe stany
* Chiny Wschodnie
* Chiny Północne
* Południowe Zjednoczone Królestwo

### <a name="shipping"></a>Wysyłania
**Wysyłanie dyski toohello centrum danych:**

Podczas tworzenia zadania importu lub eksportu, zostaną wyświetlone adres wysyłkowy jednego hello obsługiwane lokalizacje tooship dysków. Podany adres wysyłkowy Hello zależy od lokalizacji hello konta magazynu, ale może nie być hello takie same jak lokalizacja konta magazynu.

Można użyć nośników, takich jak FedEx, DHL w sprawie, UPS lub hello poczty amerykańskiej tooship Twojego toohello dysków adres wysyłkowy.

**Dyski wysyłki z centrum danych hello:**

Podczas tworzenia zadania importu lub eksportu, podaj adres zwrotny dla Microsoft toouse podczas dysków hello wysyłanie kopii po zakończeniu zadania. Upewnij się, że Podaj prawidłowy zwrotny adres tooavoid opóźnienia w przetwarzaniu.

Operator wybranym można użyć w kolejności tooforward statku hello dysku. Operator Hello powinny mieć odpowiedni śledzenia w kolejności toomaintain łańcuch nadzoru. Należy również podać prawidłowy operator FedEx lub przez firmę DHL toobe numer konta używane przez firmę Microsoft do wysyłania hello dyski ponownie. Numer konta FedEx jest wymagany dla wysyłania dysków z hello USA i Europy lokalizacji kopii. Numer konta przez firmę DHL jest wymagany dla wysyłania dysków z lokalizacji Azja i klientów w Australii. Można utworzyć [FedEx](http://www.fedex.com/us/oadr/) (dla Stanów Zjednoczonych i Europie) lub [przez firmę DHL](http://www.dhl.com/) konta operatora (Azja i klientów w Australii) Jeśli nie mają. Jeśli masz już operator numer konta, sprawdź, czy jest prawidłowa.

W wysyłania pakietów, należy wykonać warunki hello na [warunki usługi Microsoft Azure](https://azure.microsoft.com/support/legal/services-terms/).

> [!IMPORTANT]
> Należy pamiętać, że hello nośnik fizyczny, który jest dostarczany może być konieczne toocross innych krajach. Ponosisz odpowiedzialność za zapewnienie, że nośnik fizyczny i danych użytkownika są zaimportowane i/lub wyeksportować zgodnie z hello obowiązujących przepisów. Przed dostarczeniem hello nośnik fizyczny, skontaktuj się z Twojego tooverify doradcy że nośnik i danych legalnie może być wysłane toohello zidentyfikowane centrum danych. Dzięki temu tooensure osiągnie firmy Microsoft, w odpowiednim czasie. Na przykład dowolnego pakietu, który będzie między granicami musi toobe faktury, wraz z pakietem hello (z wyjątkiem Jeśli przekraczaniu granic w Unii Europejskiej). Można wydrukować kopię wypełniony hello faktury z operatora witryny sieci Web. Przykład faktur handlowych są [faktury DHL w sprawie](http://invoice-template.com/wp-content/uploads/dhl-commercial-invoice-template.pdf) i [faktury FedEx](http://images.fedex.com/downloads/shared/shipdocuments/blankforms/commercialinvoice.pdf). Upewnij się, Microsoft nie zostały wskazane jako hello eksportera.
> 
> 

## <a name="how-does-hello-azure-importexport-service-work"></a>Jak działa hello usługi Import/Eksport Azure?
Za przesyłanie danych między lokacją lokalną i magazynu obiektów blob Azure za pomocą usługi Import/Eksport Azure hello zadań tworzenia i wysyłania centrum danych Azure tooan dysków twardych. Każdy dysk twardy, który jest skojarzony z jednym zadaniu. Każde zadanie jest skojarzone z kontem magazynu jednego. Przejrzyj hello [sekcji wymagania wstępne](#pre-requisites) dokładnie toolearn o specyfice hello tej usługi, takie jak obsługiwane typy obiektów blob, typów dysków, lokalizacji i wysyłania.

W tej sekcji możemy opisano w wysokiego poziomu hello etapy podczas importowania i wyeksportować zadań. Dalszej części hello [Szybki Start sekcji](#quick-start), firma Microsoft Podaj toocreate instrukcje importu i eksportu zadania.

### <a name="inside-an-import-job"></a>Wewnątrz zadania importu
Na wysokim poziomie zadania importu obejmuje hello następujące kroki:

* Określić toobe danych hello zaimportowane i hello liczba dysków, które mają być.
* Zidentyfikuj hello docelowego obiektu blob danych w magazynie obiektów Blob.
* Użyj hello toocopy narzędzie WAImportExport Twojego tooone danych lub więcej dysków twardych i szyfrowanie funkcją BitLocker.
* Utwórz zadania importu na koncie magazynu docelowego przy użyciu portalu Azure hello lub hello importowania i eksportowania interfejsu API REST. Jeśli używasz hello portalu Azure, należy przekazać pliki dziennika dysku hello.
* Podaj adres zwrotny hello i toobe numer konta operator używany do wysyłania tooyou wstecz hello dysków.
* Toohello dyski twarde hello dostarczać adres podany podczas tworzenia zadania wysyłania.
* Zaktualizuj dostarczania hello numer w szczegółach zadania importu hello śledzenia i przesłać zadanie importu hello.
* Dyski są odbierane i przetwarzane na powitania centrum danych Azure.
* Dyski są dostarczane przy użyciu operatora konta toohello adres zwrotny w hello zadania importu.
  
    ![Rysunek 1:Import przepływu pracy](./media/storage-import-export-service/importjob.png)

### <a name="inside-an-export-job"></a>Wewnątrz zadania eksportu
Na wysokim poziomie zadania eksportu obejmuje hello następujące kroki:

* Określ toobe danych hello wyeksportowany i hello liczba dysków, które mają być.
* Określ obiekty BLOB źródła hello lub ścieżki kontenera danych w magazynie obiektów Blob.
* Utwórz zadanie eksportu na koncie magazynu źródłowego przy użyciu portalu Azure hello lub hello importowania i eksportowania interfejsu API REST.
* Określ hello źródła obiektów blob lub ścieżki kontenera danych w hello zadanie eksportowania.
* Podaj hello zwrotny adres i operatora numer konta toobe używany do wysyłania tooyou wstecz hello dysków.
* Toohello dyski twarde hello dostarczać adres podany podczas tworzenia zadania wysyłania.
* Zaktualizuj dostarczania hello numer w szczegółach zadania eksportu hello śledzenia i przesłać zadanie eksportu hello.
* dyski Hello są odbierane i przetwarzane na powitania centrum danych Azure.
* dyski Hello są szyfrowane za pomocą funkcji BitLocker; Witaj klucze są dostępne za pośrednictwem hello portalu Azure.  
* dyski Hello są dostarczane przy użyciu operatora konta toohello adres zwrotny w hello zadania importu.
  
    ![Rysunek 2:Export przepływu pracy](./media/storage-import-export-service/exportjob.png)

### <a name="viewing-your-job-and-drive-status"></a>Wyświetlanie stan zadania i dysku
Można śledzić stan hello importowanie lub eksportowanie zadań z hello portalu Azure. Kliknij przycisk hello **importu/eksportu** kartę. Na stronie powitania zostanie wyświetlona lista zadań.

![Widok stanu zadania](./media/storage-import-export-service/jobstate.png)

Zobaczysz jednego hello następujące stany zadania, w zależności od tego, w którym dysk jest w procesie hello.

| Stan zadania | Opis |
|:--- |:--- |
| Tworzenie | Po utworzeniu zadania, jego stan jest ustawiony tooCreating. Hello zadania w trakcie hello Tworzenie stanu, hello usługi Import/Eksport zakłada hello dyski nie zostały jeszcze wysłane toohello centrum danych. Zadanie może pozostawać w stanie tworzenie hello dla się tootwo tygodni, po których zostanie on automatycznie usunięty przez usługę hello. |
| Wysyłania | Po wysyłasz do pakietu, należy zaktualizować hello śledzenie informacji w hello portalu Azure.  To spowoduje wyłączenie hello zadania na "Wysyłki". zadania Hello pozostanie w hello stan wysyłki się tootwo tygodni. 
| Odebrano | Po wszystkie dyski zostały odebrane w centrum danych hello, stan zadania hello zostanie ustawiona toohello odebrane. |
| Transferowanie | Po rozpoczęciu przetwarzania co najmniej jeden dysk hello stan zadania zostanie ustawiona toohello transferowanie. Zobacz stany stacji hello sekcji poniżej, aby uzyskać szczegółowe informacje. |
| Tworzenie pakietów | Po zakończeniu wszystkich dysków przetwarzania, hello zadania zostaną umieszczone w stanie pakietów hello dopóki hello dyski są wysłane tooyou Wstecz. |
| ukończone | Po wszystkie dyski zostały wysłane toohello wstecz klienta, jeśli hello zadanie zostało ukończone bez błędów, następnie zadania hello zostanie ustawiona toohello stanu ukończone. Hello zadania zostaną automatycznie usunięte po 90 dniach w hello stanu ukończone. |
| zamknięte | Po wszystkie dyski zostały wysłane toohello wstecz klienta, jeśli pojawiły się błędy podczas przetwarzania hello hello zadania, następnie zadania hello zostanie ustawiona toohello stanie zamkniętym. Witaj zadania zostaną automatycznie usunięte po 90 dniach w stanie zamkniętym hello. |

Witaj w poniższej tabeli opisano hello cyklu życia poszczególnych dyskach przejścia go za pomocą zadania importu lub eksportu. bieżący stan każdego dysku w ramach zadania Hello jest teraz widoczne z hello portalu Azure.
Witaj poniższej tabeli opisano każdy stan każdego dysku w ramach zadania mogą przechodzić przez.

| Stan stacji | Opis |
|:--- |:--- |
| Określona | Po utworzeniu zadania hello z hello portalu Azure, dla zadania importu hello stan początkowy dla dysku jest hello określony stan. Dla zadania eksportu ponieważ dysk nie zostanie wskazany po utworzeniu zadania hello hello dysk początkowy stan jest hello stanie Received. |
| Odebrano | gdy operator usługi Import/Eksport hello przetworzył hello dysków, które zostały odebrane z hello wysyłania firmy dla zadania importu, Hello dysk przechodzi toohello stanie Received. Dla zadania eksportu hello dysk początkowy stan jest hello stanie Received. |
| NeverReceived | Hello dysku zostanie przesunięty toohello NeverReceived stanu, gdy dociera hello pakietu dla zadania, ale hello pakiet nie zawiera hello dysku. Dysk można również przenosić w tym stanie, jeśli został dwa tygodnie od momentu hello usługa odebrała hello wysyłanie informacji, ale pakiet hello ma nie dotarły jeszcze w centrum danych hello. |
| Transferowanie | Dysk zostanie przesunięty toohello transferowanie stanu, gdy usługa hello rozpoczyna tootransfer danych z tooWindows dysku hello Azure Storage. |
| ukończone | Dysk zostanie przesunięty toohello stanu ukończone hello usługi został pomyślnie przesyłana wszystkie dane hello bez błędów.
| CompletedMoreInfo | Dysk zostanie przesunięty toohello CompletedMoreInfo stan, gdy usługa hello napotkał problemy podczas kopiowania danych z lub toohello dysku. informacje Hello mogą zawierać błędy, ostrzeżenia lub komunikaty informacyjne o zastępowaniu obiektów blob.
| ShippedBack | Hello dysku zostanie przesunięty toohello ShippedBack stanu, gdy została wysłana z adres zwrotny toohello wstecz centrum danych hello. |

Ten obraz z portalu Azure hello Wyświetla stan dysku hello zadania przykładzie:

![Wyświetl stan stacji](./media/storage-import-export-service/drivestate.png)

Witaj poniższej tabeli opisano stanów awarii dysku hello i hello akcje wykonywane dla każdego stanu.

| Stan stacji | Wydarzenie | Rozdzielczość / następny krok |
|:--- |:--- |:--- |
| NeverReceived | Dysk, który jest oznaczony jako NeverReceived (ponieważ nie została odebrana jako część zadania hello wydania) dociera do innego wydania. | zespół operacyjny Hello przeniesie hello dysku toohello stanie Received. |
| Nie dotyczy | Dysk, który nie jest częścią wszystkie zadania dociera hello centrum danych w ramach innego zadania. | dysk Hello zostaną oznaczone jako dodatkowy dysk i zostanie zwrócony toohello klienta po zakończeniu zadania hello skojarzonego z pakietem oryginalnego hello. |

### <a name="time-tooprocess-job"></a>Czas tooprocess zadania
Hello ilość czasu tooprocess zadania importu/eksportu może być różna w zależności od różnych czynników, takich jak czas dostawy, typ zadania, wpisz i rozmiaru hello kopiowanych danych i hello dyskach hello podany rozmiar. Hello usługi Import/Eksport nie ma umowy dotyczącej poziomu usług, ale po otrzymaniu dysków hello usługi hello dokłada wszelkich starań, toocomplete hello kopiowania w ciągu 7 dni too10. Postęp zadania hello tootrack interfejsu API REST hello można użyć lepiej. Istnieje procentu ukończenia parametr w hello operacji listę zadań, która wskazuje postęp kopii. Dotrzeć toous, jeśli potrzebujesz toocomplete szacowania zadanie krytyczne importu/eksportu czasu.

### <a name="pricing"></a>Cennik
**Opłata obsługę dysku**

Brak opłatą Obsługa dysku dla każdego dysku przetwarzane jako część import lub zadanie eksportowania. Zobacz szczegóły hello na powitania [cennik Import/Eksport Azure](https://azure.microsoft.com/pricing/details/storage-import-export/).

**Koszty wysyłki**

Podczas wydawania tooAzure dysków płacisz hello wysyłania koszt toohello wysyłki operatora. Po powrocie z Microsoft hello dysków tooyou hello koszt wysyłki jest pobierana toohello operator konta, które dostępnych na powitania czasu utworzenia zadania.

**Koszty transakcji**

Brak Brak kosztów transakcji podczas importowania danych do magazynu obiektów blob. opłaty za wyjście standardowe Hello są stosowane, gdy dane są eksportowane z magazynu obiektów blob. Więcej szczegółów kosztów transakcji, zobacz [ceny transferu danych.](https://azure.microsoft.com/pricing/details/data-transfers/)

## <a name="quick-start"></a>Szybki start
W tej sekcji udostępniamy instrukcje tworzenia, importowania i eksportowania zadania. Upewnij się, spełnia wszystkie hello [wstępne](#pre-requisites) przed przeniesieniem do przodu.

> [!IMPORTANT]
> Usługa Hello obsługuje jedno konto magazynu w warstwie standardowa na import lub zadanie eksportowania i nie obsługuje kont magazynu w warstwie premium. 
> 
> 
## <a name="create-an-import-job"></a>Utwórz zadania importu
Utwórz tooyour danych toocopy zadania importu kontem magazynu platformy Azure z dysków twardych poprzez wysyłanie jeden lub więcej dysków zawierających Centrum określone dane toohello danych. Witaj zadania importu przekazuje szczegółowe informacje o dyskach twardych, toobe danych kopiowane, docelowe konto magazynu i wysyłania informacji usługi Import/Eksport Azure toohello. Tworzenie zadania importu jest procesem trzech etapów. Najpierw przygotować dyski za pomocą narzędzia WAImportExport hello. Po drugie przesłać zadania importu za pomocą hello portalu Azure. Trzecie wysyłki toohello dysków hello podane podczas zadania tworzenia i aktualizacji hello wysyłania informacji w szczegóły zadania adres wysyłkowy.   

### <a name="prepare-your-drives"></a>Przygotowanie dysków
Witaj pierwszym krokiem podczas importowania danych za pomocą usługi Import/Eksport Azure hello jest tooprepare dysków za pomocą narzędzia WAImportExport hello. Wykonaj kroki hello poniżej tooprepare dysków.

1. Zidentyfikuj toobe danych hello zaimportowane. Może to być katalogów i plików autonomicznych na powitania serwera lokalnego lub w udziale sieciowym.  
2. Określ hello liczba dysków, należy wykonać w zależności od całkowity rozmiar danych hello. Uzyskaj hello wymagana liczba 2,5 dysków SSD i 2,5-calowe lub 3,5" stacje dysków twardych SATA II lub III.
3. Zidentyfikuj hello docelowe konto magazynu, kontenera, katalogów wirtualnych i obiektów blob.
4.  Określ hello katalogów i/lub plików autonomicznych, które zostaną skopiowane tooeach dysku twardym.
5.  Tworzenie plików CSV dla zestawu danych i driveset hello.
    
    **Plik CSV zestawu danych**
    
    Poniżej znajduje się przykładowa przykład pliku CSV zestawu danych:
    
    ```
    BasePath,DstBlobPathOrPrefix,BlobType,Disposition,MetadataFile,PropertiesFile
    "F:\50M_original\100M_1.csv.txt","containername/100M_1.csv.txt",BlockBlob,rename,"None",None
    "F:\50M_original\","containername/",BlockBlob,rename,"None",None 
    ```
   
    W hello powyżej przykładzie 100M_1.csv.txt będzie skopiowany toohello głównego hello kontenera o nazwie "containername". Jeśli nazwa kontenera hello "containername" nie istnieje, zostanie utworzony. Wszystkie pliki i foldery w obszarze 50M_original będzie toocontainername rekursywnie skopiować. Struktura folderów będzie przechowywany.

    Dowiedz się więcej o [przygotowania pliku CSV zestawu danych hello](storage-import-export-tool-preparing-hard-drives-import.md#prepare-the-dataset-csv-file).
    
    **Należy pamiętać,**: domyślnie hello danych zostanie zaimportowana jako blokowych obiektów blob. Witaj BlobType tooimport wartości pola danych można użyć jako stronicowych obiektów blob. Na przykład jeśli są importowane pliki VHD, na których zostanie zainstalowany jako dyski na maszynie Wirtualnej platformy Azure, należy je zaimportować jako stronicowych obiektów blob.

    **Plik Driveset CSV**

    wartość Hello driveset hello, Flaga jest pliku CSV, który zawiera listę hello litery dysków hello toowhich dyski są mapowane w kolejności dla toocorrectly narzędzie hello wybierz hello Lista dysków toobe przygotowane. 

    Poniżej znajduje się przykład Witaj driveset pliku CSV:
    
    ```
    DriveLetter,FormatOption,SilentOrPromptOnFormat,Encryption,ExistingBitLockerKey
    G,AlreadyFormatted,SilentMode,AlreadyEncrypted,060456-014509-132033-080300-252615-584177-672089-411631 |
    H,Format,SilentMode,Encrypt,
    ```

    W hello powyżej przykładzie zakłada się, że są dołączone dwa dyski i woluminy NTFS podstawowe G:\ litery woluminu i H:\ zostały utworzone. Narzędzie Hello formatowania i szyfrowania hello dysk, który jest hostem H:\ i nie będzie formatu lub szyfrowania dysku hello hosting woluminu G:\.

    Dowiedz się więcej o [przygotowania pliku CSV driveset hello](storage-import-export-tool-preparing-hard-drives-import.md#prepare-initialdriveset-or-additionaldriveset-csv-file).

6.  Użyj hello [narzędzie WAImportExport](http://download.microsoft.com/download/3/6/B/36BFF22A-91C3-4DFC-8717-7567D37D64C5/WAImportExport.zip) toocopy Twojego tooone danych lub większej liczby dysków twardych.
7.  W polu szyfrowania w drivset CSV tooenable funkcją BitLocker na dysku twardym powitania można określić "Szyfruj". Alternatywnie można również włączyć szyfrowanie funkcją BitLocker ręcznie na dysku twardym powitania i określ "AlreadyEncrypted" i podaj klucz hello w hello driveset CSV podczas uruchamiania narzędzia hello.

8. Nie należy modyfikować danych hello na powitania dysków twardych lub pliku dziennika hello po zakończeniu przygotowywania dysku.

> [!IMPORTANT]
> Każdy dysk twardy, które należy przygotować spowoduje w pliku dziennika. Podczas tworzenia zadania importu hello przy użyciu hello portalu Azure, należy przesłać wszystkie pliki dziennika hello hello dysków, które są częścią tego zadania importu. Dyski bez arkusza, pliki nie zostaną przetworzone.
> 
>

Poniżej są hello poleceń i przykłady dotyczące przygotowywanie dysku twardym powitania przy użyciu narzędzia WAImportExport.

Narzędzie WAImportExport polecenie PrepImport dla hello najpierw skopiować sesji toocopy katalogów i/lub pliki w nowej sesji kopiowania:

```
WAImportExport.exe PrepImport /j:<JournalFile> /id:<SessionId> [/logdir:<LogDirectory>] [/sk:<StorageAccountKey>] [/silentmode] [/InitialDriveSet:<driveset.csv>] DataSet:<dataset.csv>
```

**Przykład importu 1**

```
WAImportExport.exe PrepImport /j:JournalTest.jrn /id:session#1  /sk:************* /InitialDriveSet:driveset-1.csv /DataSet:dataset-1.csv /logdir:F:\logs
```

W kolejności zbyt**dodawanie kolejnych dysków**, co można utworzyć nowego pliku driveset i uruchom polecenie hello zgodnie z poniższymi instrukcjami. Dla kolejnych kopii sesji toohello różnych dysków niż określona w pliku CSV InitialDriveset Określ plik CSV driveset i podać go jako wartość parametru toohello "AdditionalDriveSet". Użyj hello **tego samego pliku dziennika** nazwy i podaj **nowy identyfikator sesji**. format pliku AdditionalDriveset CSV Hello jest taki sam jak InitialDriveSet format.

```
WAImportExport.exe PrepImport /j:<JournalFile> /id:<SessionId> /AdditionalDriveSet:<driveset.csv>
```

**Przykład importu 2**
```
WAImportExport.exe PrepImport /j:JournalTest.jrn /id:session#3  /AdditionalDriveSet:driveset-2.csv
```

W kolejności tooadd dodatkowe dane toohello driveset tego samego narzędzia WAImportExport PrepImport polecenia można wywołać dla kolejnych kopii sesji toocopy dodatkowe pliki lub katalogu: dla kolejnych kopii sesji toohello stacje dysków twardych tego samego określone w CSV InitialDriveset pliku, określ hello **tego samego pliku dziennika** nazwy i podaj **nowy identyfikator sesji**; klucz konta magazynu należy tooprovide hello nie istnieje.

```
WAImportExport PrepImport /j:<JournalFile> /id:<SessionId> /j:<JournalFile> /id:<SessionId> [/logdir:<LogDirectory>] DataSet:<dataset.csv>
```

**Przykład importu 3**

```
WAImportExport.exe PrepImport /j:JournalTest.jrn /id:session#2  /DataSet:dataset-2.csv
```

Dowiedz się więcej o używaniu narzędzia WAImportExport hello w [przygotowywania dysków twardych do importu](storage-import-export-tool-preparing-hard-drives-import.md).

Ponadto można znaleźć toohello [przykładowy przepływ pracy tooprepare dyski twarde dla zadania importu](storage-import-export-tool-sample-preparing-hard-drives-import-job-workflow.md) Aby uzyskać szczegółowe instrukcje krok po kroku.  

### <a name="create-hello-import-job"></a>Utwórz zadania importu hello
1. Po przygotowaniu dysku, przejdź tooyour konta magazynu w portalu Azure hello i wyświetlić hello pulpitu nawigacyjnego. W obszarze **szybki przegląd**, kliknij przycisk **Tworzenie zadania importu**. Przejrzyj kroki hello i wybierz hello wyboru tooindicate przygotowaniu dysku i że masz dostępny plik dziennika dysku hello.
2. W kroku 1. Podaj informacje kontaktowe hello osoba odpowiedzialna za tego zadania importu i nieprawidłowy adres zwrotny. Jeśli chcesz toosave danych pełnego dziennika dla zadania importu hello, zaznacz opcję hello zbyt**Zapisz hello pełnego dziennika w kontenerze obiektów blob Mój "waimportexport"**.
3. W kroku 2 należy przekazać pliki dziennika na dysku hello uzyskane w kroku przygotowania hello dysku. Dla każdego dysku, które zostały przygotowane należy tooupload jeden plik.
   
   ![Utwórz zadania importu — krok 3](./media/storage-import-export-service/import-job-03.png)
4. W kroku 3 wprowadź nazwę opisową hello zadania importu. Należy pamiętać, że wprowadzona nazwa hello może zawierać tylko małe litery, cyfry, łączniki i podkreślenia, musi zaczynać się literą i nie może zawierać spacji. Nazwa hello wybierzesz tootrack zadaniach gdy są one w toku, a po zakończeniu będzie używana.
   
   Następnie wybierz region centrum danych z listy hello. obszaru roboczego danych Hello wskaże danych hello Wyśrodkowanie i adres toowhich muszą dostarczać pakietu. Zobacz hello FAQ poniżej, aby uzyskać więcej informacji.
5. W kroku 4 Wybierz z listy hello zwracany operatora i wprowadź numer swojego konta operatora. Firma Microsoft będzie używać tego konta tooship hello dysków wstecz tooyou po zakończeniu zadania importu.
   
   Jeśli numer identyfikacyjny, wybierz z listy hello operatora dostarczania i wprowadź swój numer śledzenia.
   
   Jeśli nie masz śledzenia number jeszcze, wybierz **po I dostarczono Mój pakiet zostanie jest Podaj informacje o moim dostawy dla tego zadania importu**, następnie Zakończ proces importowania hello.
6. Zwraca numer identyfikacyjny po zostały dostarczone do pakietu tooenter toohello **importu/eksportu** dla konta magazynu w portalu Azure hello strony, wybierz z listy hello zadania i wybierz **wysyłania informacji o**. Przejdź przez kreatora hello i wprowadź swój numer śledzenia w kroku 2.
   
    Jeśli hello numer śledzenia nie jest aktualizowany w ciągu 2 tygodni tworzenia zadania hello, hello zadanie wygaśnie.
   
    Jeśli zadanie hello jest w stanie tworzenie, wysyłki i transferowanie hello, możesz zaktualizować operatora numer konta w kroku 2 hello kreatora. Gdy zadanie hello jest w stanie pakietów hello, nie można zaktualizować numer operatora konta dla tego zadania.
7. Postęp zadania można śledzić na powitania pulpitu nawigacyjnego portalu. Zobacz, każdy stan zadania w poprzedniej sekcji hello oznacza przez [wyświetlanie stan zadania](#viewing-your-job-status).

## <a name="create-an-export-job"></a>Utwórz zadanie eksportu
Utwórz hello toonotify zadania eksportu usługi Import/eksport, czy użytkownik będzie wysyłać jednego lub większej ilości danych toohello pustych dysków Centrum, dzięki czemu dane można eksportować z dysków toohello konta magazynu i dyski hello następnie dostarczonym tooyou.

### <a name="prepare-your-drives"></a>Przygotowanie dysków
Następujące testy wstępne są zalecane w przypadku przygotowywania dysków dla zadania eksportu:

1. Sprawdź hello liczba dysków wymaganych przy użyciu narzędzia WAImportExport hello PreviewExport polecenia. Aby uzyskać więcej informacji, zobacz [przeglądania użycia dysków dla zadania eksportu](https://msdn.microsoft.com/library/azure/dn722414.aspx). Pomaga użycia dysków dla obiektów blob hello, które wybrano w wersji preview, na podstawie rozmiaru hello dysków hello ma toouse.
2. Sprawdź, czy użytkownik może odczytu/zapisu toohello dysku twardym, który ma zostać wysłane dla zadania eksportu hello.

### <a name="create-hello-export-job"></a>Utwórz zadanie eksportu hello
1. toocreate zadanie eksportu Przejdź tooyour konta magazynu w portalu Azure hello i wyświetlić hello pulpitu nawigacyjnego. W obszarze **szybki przegląd**, kliknij przycisk **tworzenia zadania Eksportuj** i postępuj zgodnie z instrukcjami kreatora hello.
2. W kroku 2 Podaj informacje kontaktowe hello osoba odpowiedzialna za to zadanie eksportu. Jeśli chcesz toosave danych pełnego dziennika dla zadania eksportu hello, zaznacz opcję hello zbyt**Zapisz hello pełnego dziennika w kontenerze obiektów blob Mój "waimportexport"**.
3. W kroku 3 określić które obiektu blob danych mają tooexport z Twojej pusty tooyour konta magazynu dysków lub dysków. Można wybrać tooexport wszystkie dane obiektów blob na koncie magazynu hello, lub można określić, które obiekty BLOB lub zestawów tooexport obiektów blob.
   
   toospecify tooexport obiektów blob, użyj hello **równe** selektora i określ hello blob toohello ścieżki względnej, począwszy od nazwy kontenera hello. Użyj *$root* toospecify hello nadrzędny kontener.
   
   toospecify wszystkich obiektów blob, począwszy od prefiksu, użyj hello **rozpoczyna się od** selektora i określ prefiks hello, rozpoczynający się od ukośnika "/". Prefiks Hello może być hello prefiks nazwy kontenera hello, nazwa kontenera pełną hello lub hello kontenera pełną nazwę hello prefiks nazwy obiektu blob hello.
   
   Witaj w poniższej tabeli przedstawiono przykłady ścieżek nieprawidłowy obiekt blob:
   
   | Selektor | Ścieżka obiektu blob | Opis |
   | --- | --- | --- |
   | Rozpoczyna się od |/ |Eksportuje wszystkie obiekty BLOB na koncie magazynu hello |
   | Rozpoczyna się od |/$root / |Eksportuje wszystkie obiekty BLOB w kontenerze głównego hello |
   | Rozpoczyna się od |/Book |Eksportuje wszystkie obiekty BLOB w dowolnym kontenerze, który rozpoczyna się od prefiksu **książki** |
   | Rozpoczyna się od |/Music/ |Eksportuje wszystkie obiekty BLOB w kontenerze **utworów muzycznych** |
   | Rozpoczyna się od |/ music/love |Eksportuje wszystkie obiekty BLOB w kontenerze **utworów muzycznych** się od prefiksu **lubisz** |
   | Zbyt równa|$root/logo.bmp |Eksportowanie obiektów blob **logo.bmp** w kontenerze głównego hello |
   | Zbyt równa|videos/Story.mp4 |Eksportowanie obiektów blob **story.mp4** w kontenerze **wideo** |
   
   Należy podać hello ścieżki obiektu blob w prawidłowe formaty tooavoid błędy podczas przetwarzania, jak pokazano w tym zrzucie ekranu pokazano.
   
   ![Utwórz zadanie eksportu — krok 3](./media/storage-import-export-service/export-job-03.png)
4. W kroku 4 wprowadź nazwę opisową hello zadanie eksportu. Wprowadzona nazwa Hello może zawierać tylko małe litery, cyfry, łączniki i podkreślenia, musi zaczynać się literą i nie może zawierać spacji.
   
   obszaru roboczego danych Hello wskaże toowhich centrum danych hello muszą dostarczać pakietu. Zobacz hello FAQ poniżej, aby uzyskać więcej informacji.
5. W kroku 5 wybierz z listy hello zwracany operatora, a następnie wprowadź numer swojego konta operator. Firma Microsoft będzie używać tego konta tooship dysków kopii tooyou po zakończeniu zadania eksportu.
   
   Jeśli numer identyfikacyjny, wybierz z listy hello operatora dostarczania i wprowadź swój numer śledzenia.
   
   Jeśli nie masz śledzenia number jeszcze, wybierz **po I dostarczono Mój pakiet zostanie jest Podaj informacje o moim dostawy dla tego zadania eksportu**, następnie ukończyć proces eksportu hello.
6. Zwraca numer identyfikacyjny po zostały dostarczone do pakietu tooenter toohello **importu/eksportu** dla konta magazynu w portalu Azure hello strony, wybierz z listy hello zadania i wybierz **wysyłania informacji o**. Przejdź przez kreatora hello i wprowadź swój numer śledzenia w kroku 2.
   
    Jeśli hello numer śledzenia nie jest aktualizowany w ciągu 2 tygodni tworzenia zadania hello, hello zadanie wygaśnie.
   
    Jeśli zadanie hello jest w stanie tworzenie, wysyłki i transferowanie hello, możesz zaktualizować operatora numer konta w kroku 2 hello kreatora. Gdy zadanie hello jest w stanie pakietów hello, nie można zaktualizować numer operatora konta dla tego zadania.
   
   > [!NOTE]
   > Jeśli wyeksportowany toobe obiektu blob hello jest używany w czasie hello kopiowania toohard dysku, usługi Import/Eksport Azure zostanie utworzenie migawki hello obiektów blob i skopiuj hello migawki.
   > 
   > 
7. Postęp zadania można śledzić na pulpicie nawigacyjnym hello w hello portalu Azure. Zobacz, każdy stan zadania oznacza w poprzedniej sekcji hello na "Wyświetlanie stan zadania".
8. Po otrzymaniu hello dysków z wyeksportowane dane, można wyświetlać i kopiowanie kluczy funkcji BitLocker hello generowane przez usługę hello stacji dysków. Przejdź tooyour konta magazynu w hello portalu Azure, a następnie kliknij kartę importu/eksportu hello. Wybierz z listy hello zadanie eksportu i kliknij przycisk Wyświetl klucze hello. klucze funkcji BitLocker Hello są wyświetlane, jak pokazano poniżej:
   
   ![Wyświetl klucze funkcji BitLocker dla zadania eksportu](./media/storage-import-export-service/export-job-bitlocker-keys.png)

Przeczytaj poniższą sekcję Często zadawane pytania dotyczące hello jako obejmuje hello często zadawane pytania napotykanych przez klientów podczas korzystania z tej usługi.

## <a name="frequently-asked-questions"></a>Często zadawane pytania

**Czy można kopiować za pomocą usługi Import/Eksport Azure hello usługi Magazyn plików Azure?**

Nie, hello usługi Import/Eksport Azure obsługuje tylko blokowe i stronicowe obiekty BLOB. Wszystkie inne typy magazynu w tym magazynu plików Azure, Magazyn tabel i magazyn kolejek nie są obsługiwane.

**Usługa Import/Eksport Azure hello jest dostępne dla dostawcy usług Kryptograficznych subskrypcji?**

Usługa Import/Eksport Azure obsługuje subskrypcje dostawcy usług Kryptograficznych.

**Można pominąć krok przygotowania dysku powitania dla zadania importu lub czy można przygotować dysku bez kopiowania?**

Każdy dysk ma tooship importowania danych muszą być przygotowane za pomocą narzędzia Azure WAImportExport hello. Należy użyć dysku toohello hello WAImportExport narzędzie toocopy danych.

**Należy tooperform żadnych przygotowanie dysku podczas tworzenia zadania eksportu?**

Wstępne sprawdzanie nie, ale niektóre są zalecane. Sprawdź hello liczba dysków wymaganych przy użyciu narzędzia WAImportExport hello PreviewExport polecenia. Aby uzyskać więcej informacji, zobacz [przeglądania użycia dysków dla zadania eksportu](https://msdn.microsoft.com/library/azure/dn722414.aspx). Pomaga użycia dysków dla obiektów blob hello, które wybrano w wersji preview, na podstawie rozmiaru hello dysków hello ma toouse. Sprawdź, czy można odczytywać i zapisu toohello dysku twardego dostarczonej dla hello także eksportować w zadania.

**Wymagania systemowe co się stanie, jeśli dysk twardy, który nie jest zgodna z toohello wysłać przypadkowo?**

Centrum danych Azure Hello zwróci hello dysk, który nie jest zgodna z tooyou wymagania toohello obsługiwane. Jeśli tylko niektóre dyski hello w pakiecie hello wymagań hello pomocy technicznej, tych dysków będą przetwarzane i hello dyski, które nie spełniają wymagań hello zostanie zwrócony tooyou.

**Czy można anulować Moje zadanie?**

Można anulować zadania, gdy jego stan to tworzenie lub wysyłki.

**Jak długo wyświetlić stan hello zakończonych zadań w hello portalu Azure**

Można wyświetlić stan hello zakończonych zadań dla się too90 dni. Zakończonych zadań zostaną usunięte po 90 dniach.

**Czy chcesz tooimport lub wyeksportować więcej niż 10 dysków, co należy zrobić?**

Jeden importu lub eksportu zadanie może odwoływać się tylko 10 dysków w jednym zadaniu usługi Import/Eksport hello. Jeśli chcesz tooship więcej niż 10 dysków, można utworzyć wiele zadań. Dyski, które są skojarzone z powitalne samo zadanie zostanie wysłana razem w hello tego samego pakietu.
Firma Microsoft oferuje wskazówki i pomoc w przypadku możliwości danych obejmuje wiele dysków zadania importu. Skontaktuj się z bulkimport@microsoft.com Aby uzyskać więcej informacji

**Wykonuje hello usługi hello dyski w formacie przed zwróceniem?**

Nie. Wszystkie dyski są szyfrowane za pomocą funkcji BitLocker.

**Firma Microsoft może zakupić dysków dla zadania importu/eksportu?**

Nie. Konieczne będzie tooship dysków dla obu importowanie i eksportowanie zadań.

** Jak mają dostęp do danych zaimportowanych przez usługę **

dane Hello na koncie magazynu Azure są dostępne za pośrednictwem portalu Azure hello lub za pomocą narzędzia Autonomiczny wywołana Eksploratora usługi Storage. https://docs.microsoft.com/en-us/Azure/VS-Azure-Tools-Storage-Manage-with-Storage-Explorer 

**Po zakończeniu zadania importu hello będzie moich danych jak wygląda na koncie magazynu hello? Zostaną zachowane Moje hierarchii katalogów?**

Podczas przygotowywania dysk twardy dla zadania importu, docelowy hello jest określany przez hello DstBlobPathOrPrefix pole w zestawie danych CSV. Jest to hello docelowy kontener w hello toowhich konta magazynu, który kopiowaniu danych z dysku twardego hello. W tym docelowy kontener katalogi wirtualne są tworzone foldery na dysku twardym powitania i obiekty BLOB są tworzone dla plików. 

**Jeśli dysk hello ma plików, które już istnieją w moim koncie magazynu, usługa hello zastąpi istniejące obiekty BLOB w moim koncie magazynu?**

Podczas przygotowywania hello dysku, można określić czy pliki docelowe hello powinny zostać zastąpione lub ignorowane za pomocą pola hello w pliku CSV zestawu danych o nazwie dyspozycji: < zmienić | zastąpić nie | zastąpić >. Domyślnie usługa hello będzie zmienić hello nowych plików zamiast zastąpić istniejące obiekty BLOB.

**Narzędzie WAImportExport hello jest zgodny z 32-bitowych systemach operacyjnych?**
Nie. Narzędzie WAImportExport Hello jest zgodna tylko z 64-bitowych systemach operacyjnych Windows. Można znaleźć w sekcji systemów operacyjnych toohello hello [wstępne](#pre-requisites) pełną listę obsługiwanych wersji systemu operacyjnego.

**Należy umieszczać innym niż dysk twardy hello w moim pakiecie?**

Wyślij tylko dyski twarde. Nie dołączaj elementy, takie jak power przewodów zasilania lub USB.

**Czy mam tooship Moje dysków przy użyciu FedEx lub przez firmę DHL?**

Mogą być centrum danych toohello dysków za pomocą dowolnego znanego operatora jak FedEx, DHL w sprawie, UPS lub poczty amerykańskiej. Jednak w wysyłanie hello dysków wstecz tooyou hello centrum danych, należy określić liczbę konta FedEx w hello USA i Europa lub liczbą konta przez firmę DHL w regionach Australii i hello Azja.

**Czy istnieją ograniczeń z wysyłki za granicę dysk?**

Należy pamiętać, że hello nośnik fizyczny, który jest dostarczany może być konieczne toocross innych krajach. Ponosisz odpowiedzialność za zapewnienie, że nośnik fizyczny i danych użytkownika są zaimportowane i/lub wyeksportować zgodnie z hello obowiązujących przepisów. Przed dostarczeniem hello nośnik fizyczny, skontaktuj się z Twojego tooverify doradcy że nośnik i danych legalnie może być wysłane toohello zidentyfikowane centrum danych. Dzięki temu tooensure osiągnie firmy Microsoft, w odpowiednim czasie.

**Podczas tworzenia zadania, adres wysyłkowy hello jest lokalizacji, która różni się od Moje Lokalizacja konta magazynu. Co zrobić?**

Niektóre lokalizacje konta magazynu są mapowane tooalternate wysyłania lokalizacji. Wcześniej lokalizacje dostępne wysyłania można też lokalizacje tooalternate tymczasowo mapowane. Zawsze sprawdzaj hello wysyłania adres podany podczas tworzenia zadania przed dostarczeniem dysków.

**Podczas wysyłania dysk, operator hello wyświetlona prośba o hello data center kontaktu adres i numer telefonu. Co należy zapewnić?**

Witaj, numer telefonu i kontroler domeny adresów jest dostępna w ramach zadania tworzenia.

**Czy można użyć skrzynki pocztowe PST toocopy usługi Import/Eksport Azure hello i SharePoint tooO365 danych?**

Zobacz zbyt[PST importowanie plików lub SharePoint danych tooOffice 365](https://technet.microsoft.com/library/ms.o365.cc.ingestionhelp.aspx).

**Można użyć toocopy usługi Import/Eksport Azure hello Mój toohello w trybie offline z kopii zapasowych usługi Kopia zapasowa Azure?**

Zobacz zbyt[przepływu pracy w trybie Offline z kopii zapasowej w programie Kopia zapasowa Azure](../../backup/backup-azure-backup-import-export.md).

**Co to jest hello maksymalne liczby dysk twardy dla jednego wydania?**

Można dowolną liczbę dysków twardych w jednym wydaniu i jeśli hello dyski należy toomultiple zadań zalecane jest zbyt) są dyski hello etykietą hello nazwy zadania. b) zadania hello aktualizacji z liczbą śledzenia sufiks na -1,-2 itd.
  
**Co to jest hello maksymalną blokowych obiektów Blob i rozmiar obiektu Blob strony obsługiwane przez dysk importu/eksportu?**

Rozmiar maksymalny blokowych obiektów Blob to około 4.768TB lub 5,000,000 MB.
Rozmiar obiektu Blob strony maksymalna liczba wynosi 1TB.

**Dysk importu/eksportu obsługuje szyfrowania AES 256?**

Usługa Import/Eksport Azure domyślnie szyfruje za pomocą szyfrowania AES 128 funkcji bitlocker, ale może to być zwiększona tooAES 256 szyfrując ręcznie za pomocą funkcji bitlocker przed skopiowaniem danych. 

Jeśli przy użyciu [WAImportExpot V1](http://download.microsoft.com/download/0/C/D/0CD6ABA7-024F-4202-91A0-CE2656DCE413/WaImportExportV1.zip), poniżej przedstawiono przykład polecenia
```
WAImportExport PrepImport /sk:<StorageAccountKey> /csas:<ContainerSas> /t: <TargetDriveLetter> [/format] [/silentmode] [/encrypt] [/bk:<BitLockerKey>] [/logdir:<LogDirectory>] /j:<JournalFile> /id:<SessionId> /srcdir:<SourceDirectory> /dstdir:<DestinationBlobVirtualDirectory> [/Disposition:<Disposition>] [/BlobType:<BlockBlob|PageBlob>] [/PropertyFile:<PropertyFile>] [/MetadataFile:<MetadataFile>] 
```
Jeśli przy użyciu [narzędzie WAImportExport](http://download.microsoft.com/download/3/6/B/36BFF22A-91C3-4DFC-8717-7567D37D64C5/WAImportExport.zip) określ "AlreadyEncrypted" i podaj klucz hello w hello driveset CSV.
```
DriveLetter,FormatOption,SilentOrPromptOnFormat,Encryption,ExistingBitLockerKey
G,AlreadyFormatted,SilentMode,AlreadyEncrypted,060456-014509-132033-080300-252615-584177-672089-411631 |
```
## <a name="next-steps"></a>Następne kroki

* [Trwa konfigurowanie narzędzia WAImportExport hello](storage-import-export-tool-how-to.md)
* [Transfer danych za pomocą hello wiersza polecenia azcopy](storage-use-azcopy.md)
* [Przykładowe interfejsu API REST wyeksportować importu platformy Azure](https://azure.microsoft.com/documentation/samples/storage-dotnet-import-export-job-management/)

