---
title: dyski twarde aaaPreparing dla Import/Eksport Azure Importuj zadanie - v1 | Dokumentacja firmy Microsoft
description: "Dowiedz się, jak dyski twarde tooprepare przy użyciu hello WAImportExport v1 narzędzia toocreate zadania importu hello usługi Import/Eksport Azure."
author: muralikk
manager: syadav
editor: tysonn
services: storage
documentationcenter: 
ms.assetid: 3d818245-8b1b-4435-a41f-8e5ec1f194b2
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/15/2017
ms.author: muralikk
ms.openlocfilehash: 1eb0c3c51e984e2869b5268254f468d4b43e9d85
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="preparing-hard-drives-for-an-import-job"></a>Przygotowywanie dysków twardych do zadania importu
tooprepare jednego lub większej liczby dysków twardych dla zadania importu, wykonaj następujące kroki:

-   Zidentyfikuj tooimport danych hello na powitania usługi Blob

-   Zidentyfikować katalogi wirtualne docelowego i obiektów blob w hello usługi Blob

-   Jak wiele dysków, należy określić

-   Skopiuj tooeach danych hello dysków twardych

 Dla przykładowego przepływu pracy, zobacz [tooPrepare przykładowym przepływie pracy dyski twarde dla zadania importu](storage-import-export-tool-sample-preparing-hard-drives-import-job-workflow-v1.md).

## <a name="identify-hello-data-toobe-imported"></a>Zidentyfikuj toobe danych hello zaimportowany
 Witaj pierwszy krok toocreating zadania importu jest toodetermine które katalogi i pliki będą tooimport. Może to być lista katalogów, lista plików unikatowy lub kombinacji tych dwóch. Jeśli katalog, wszystkie pliki w katalogu hello i jego podkatalogach będzie częścią hello zadania importu.

> [!NOTE]
>  Ponieważ podkatalogi są dołączone rekursywnie gdy katalog nadrzędny jest uwzględniona, należy określić tylko hello katalogu nadrzędnego. Nie należy również określać jego podkatalogach.
>
>  Obecnie hello narzędzia importu/eksportu pakietu Microsoft Azure ma następujące ograniczenia hello: Jeśli katalog zawiera więcej danych niż dysk twardy może zawierać, następnie hello katalog musi toobe dzielony na mniejsze katalogów. Na przykład jeśli katalog zawiera 2,5 TB danych i hello miejsca na dysku twardym jest tylko 2TB, a następnie należy toobreak hello 2,5 TB katalogu w mniejszych katalogów. To ograniczenie zostaną rozwiązane w nowszej wersji narzędzia hello.

## <a name="identify-hello-destination-locations-in-hello-blob-service"></a>Zidentyfikować lokalizacje docelowe hello hello usługi blob
 Dla każdego katalogu lub pliku, który jest importowany należy tooidentify katalog wirtualny docelowego lub obiektu blob w hello usługi obiektów Blob platformy Azure. Jako dane wejściowe toohello narzędzie importu/eksportu Azure, zostanie użyty następujących elementów docelowych. Należy pamiętać, że katalogi powinien rozdzielone znakiem ukośnika hello "/".

 Witaj w poniższej tabeli przedstawiono kilka przykładów elementów docelowych obiektów blob:

|Pliku lub katalogu źródłowego|Docelowego obiektu blob lub katalogu wirtualnego|
|------------------------------|-------------------------------------------|
|H:\Video|https://mystorageaccount.blob.Core.Windows.NET/Video|
|H:\Photo|https://mystorageaccount.blob.Core.Windows.NET/Photo|
|K:\Temp\FavoriteVideo.ISO|https://mystorageaccount.blob.Core.Windows.NET/favorite/FavoriteVideo.ISO|
|\\\myshare\john\music|https://mystorageaccount.blob.Core.Windows.NET/Music|

## <a name="determine-how-many-drives-are-needed"></a>Określ liczbę dysków są potrzebne
 Następnie należy toodetermine:

-   Witaj liczba dysków twardych potrzebnych danych hello toostore.

-   Witaj katalogów i/lub plików autonomicznych, które zostaną skopiowane tooeach dysku twardego.

 Upewnij się, że masz hello liczbę dysków twardych, konieczne będzie toostore hello dane, które są transferu.

## <a name="copy-data-tooyour-hard-drive"></a>Kopiowanie dysku twardego tooyour danych
 W tej sekcji opisano, jak toocall hello narzędzie importu/eksportu Azure toocopy Twojego tooone danych lub większej liczby dysków twardych. Zawsze należy wywołać hello Azure narzędzie importu/eksportu, możesz utworzyć nową *skopiuj sesji*. Utwórz co najmniej jedną kopię sesji dla każdego dysku toowhich kopiowania danych. w niektórych przypadkach może wymagać więcej niż jedną kopię sesji toocopy wszystkich stacji toosingle danych. Poniżej przedstawiono przyczyny, że wiele kopii sesji może być konieczne:

-   Należy utworzyć dla każdego dysku, który został skopiowany do sesji osobnej kopii.

-   Sesja kopii można skopiować jeden katalog lub dysk toohello pojedynczego obiektu blob. Jeśli kopiujesz wiele katalogów, wiele obiektów blob lub obie te grupy, należy toocreate wiele sesji kopiowania.

-   Można określić właściwości i metadanych, które zostaną ustawione na obiekty BLOB hello zaimportowana jako część zadania importu. właściwości Hello lub metadane, które można określić dla sesji kopiowania zastosuje obiekty BLOB tooall określone w tej sesji kopiowania. Jeśli chcesz toospecify inne właściwości lub metadanych dla niektórych obiektów blob, należy toocreate oddzielnie skopiować sesji. Zobacz [metadanych podczas procesu importowania hello i ustawienie właściwości](storage-import-export-tool-setting-properties-metadata-import-v1.md)Aby uzyskać więcej informacji.

> [!NOTE]
>  Jeśli masz wiele komputerów, które spełniają wymagania hello opisane w temacie [Setting Up hello Azure narzędzie importu/eksportu](storage-import-export-tool-setup-v1.md), można skopiować danych toomultiple dyski równolegle uruchomione wystąpienie tego narzędzia na każdym komputerze.

 Dla każdego dysku twardym, którego można przygotować z hello Azure narzędzie importu/eksportu hello narzędzie utworzy plik jednego arkusza. Pliki dziennika hello należy ze wszystkich zadania importu hello toocreate dysków. Hello pliku dziennika można także przygotowanie stacji tooresume używane, jeśli narzędzie hello zostanie przerwana.

### <a name="azure-importexport-tool-syntax-for-an-import-job"></a>Azure Składnia narzędzia importu/eksportu dla zadania importu
 tooprepare dysków dla zadania importu wywołać hello Azure narzędzie importu/eksportu z hello **PrepImport** polecenia. Parametry, które możesz uwzględnić zależy od tego, czy jest to hello pierwszego kopiowania sesji lub sesji kolejnych kopii.

 Witaj pierwszej sesji kopii dysku wymaga niektóre dodatkowe parametry toospecify hello klucz konta magazynu; litera dysku docelowym Hello; Określa, czy dysk hello musi być sformatowany; Określa, czy dysk hello muszą być szyfrowane i jeśli tak, hello klucza funkcji BitLocker; i hello katalogu dziennika. Oto składnia hello toocopy sesji kopii początkowej, katalogu lub pojedynczym plikiem:

 **Najpierw skopiować toocopy sesji jednego katalogu**

 `WAImportExport PrepImport /sk:<StorageAccountKey> /csas:<ContainerSas> /t: <TargetDriveLetter> [/format] [/silentmode] [/encrypt] [/bk:<BitLockerKey>] [/logdir:<LogDirectory>] /j:<JournalFile> /id:<SessionId> /srcdir:<SourceDirectory> /dstdir:<DestinationBlobVirtualDirectory> [/Disposition:<Disposition>] [/BlobType:<BlockBlob|PageBlob>] [/PropertyFile:<PropertyFile>] [/MetadataFile:<MetadataFile>]`

 **Najpierw skopiować toocopy sesji pojedynczego pliku**

 `WAImportExport PrepImport /sk:<StorageAccountKey> /csas:<ContainerSas> /t: <TargetDriveLetter> [/format] [/silentmode] [/encrypt] [/bk:<BitLockerKey>] [/logdir:<LogDirectory>] /j:<JournalFile> /id:<SessionId> /srcfile:<SourceFile> /dstblob:<DestinationBlobPath> [/Disposition:<Disposition>] [/BlobType:<BlockBlob|PageBlob>] [/PropertyFile:<PropertyFile>] [/MetadataFile:<MetadataFile>]`

 W kolejnych kopii sesji nie trzeba parametrów początkowych hello toospecify. Oto składnia hello toocopy sesji kolejnych kopii katalog lub pojedynczy plik:

 **Kopiuj kolejne sesje toocopy jednego katalogu**

 `WAImportExport PrepImport /j:<JournalFile> /id:<SessionId> /srcdir:<SourceDirectory> /dstdir:<DestinationBlobVirtualDirectory> [/Disposition:<Disposition>] [/BlobType:<BlockBlob|PageBlob>] [/PropertyFile:<PropertyFile>] [/MetadataFile:<MetadataFile>]`

 **Kopia kolejne sesje toocopy pojedynczego pliku**

 `WAImportExport PrepImport /j:<JournalFile> /id:<SessionId> /srcfile:<SourceFile> /dstblob:<DestinationBlobPath> [/Disposition:<Disposition>] [/BlobType:<BlockBlob|PageBlob>] [/PropertyFile:<PropertyFile>] [/MetadataFile:<MetadataFile>]`

### <a name="parameters-for-hello-first-copy-session-for-a-hard-drive"></a>Parametry hello najpierw skopiować sesji na dysku twardym
 Każdym uruchomieniu hello Azure narzędzie importu/eksportu toocopy plików dysku twardego toohello hello narzędzie tworzy sesję kopiowania. Każdej sesji kopiowania Kopiuje jeden katalog lub dysk twardy tooa pojedynczego pliku. Stan Hello hello kopiowania sesji jest zapisywany toohello pliku dziennika. Jeśli sesji kopiowania zostanie przerwana (na przykład powodu utraty zasilania systemu tooa), może zostać wznowiony ponownie uruchomić narzędzie hello i określając hello pliku dziennika w wierszu polecenia hello.

> [!WARNING]
>  Jeśli określisz hello **/format** parametr hello pierwszej sesji kopiowania, hello dysku zostanie sformatowane i wszystkie dane na dysku hello zostaną wymazane. Zaleca się używania puste dysków tylko dla sesji kopiowania.

 Hello polecenie hello pierwszego kopiowania sesji dla każdego dysku wymaga różnych parametrów niż hello polecenia kopiowania kolejnych sesjach. Witaj poniższej tabeli wymieniono hello dodatkowe parametry, które są dostępne dla hello pierwszego kopiowania sesji:

|Parametr wiersza polecenia|Opis|
|-----------------------------|-----------------|
|**/SK:**< StorageAccountKey\>|`Optional.`klucz konta magazynu Hello hello magazynu konta toowhich hello danych zostaną zaimportowane. Należy uwzględnić **/sk:**< StorageAccountKey\> lub **/csas:**< ContainerSas\> w poleceniu hello.|
|**/csas:**< ContainerSas\>|`Optional`. kontener Hello konta magazynu toohello SAS toouse tooimport danych. Należy uwzględnić **/sk:**< StorageAccountKey\> lub **/csas:**< ContainerSas\> w poleceniu hello.<br /><br /> Hello wartość tego parametru musi zaczynać się od nazwy kontenera hello, następuje znak zapytania (?) i tokenu sygnatury dostępu Współdzielonego hello. Na przykład:<br /><br /> `mycontainer?sv=2014-02-14&sr=c&si=abcde&sig=LiqEmV%2Fs1LF4loC%2FJs9ZM91%2FkqfqHKhnz0JM6bqIqN0%3D&se=2014-11-20T23%3A54%3A14Z&sp=rwdl`<br /><br /> uprawnienia Hello, czy określona w adresie URL hello lub w zasadach dostępu przechowywane, musi zawierać odczytu, zapisu i usuwania dla zadania importu i odczytu, zapisu i listy zadań eksportu.<br /><br /> Jeśli ten parametr jest określony, toobe wszystkie obiekty BLOB, zaimportować lub wyeksportować musi znajdować się w hello kontenerem określonymi we hello sygnatury dostępu współdzielonego.|
|**/ t:**< TargetDriveLetter\>|`Required.`litera dysku Hello hello docelowy dysk twardy hello bieżącej kopii sesji, bez hello kończyć dwukropkiem.|
|**/ Format**|`Optional.`Określ ten parametr, gdy hello potrzebuje toobe sformatowana; w przeciwnym razie Pomiń go. Zanim narzędzie hello formatuje dysk hello, pojawi się monit o potwierdzenie z konsoli. toosuppress hello potwierdzenia, określ parametr /silentmode hello.|
|**/silentmode**|`Optional.`Określ ten parametr toosuppress hello potwierdzenie formatowania dysku targert hello.|
|**/ szyfrowania**|`Optional.`Ten parametr należy określić, gdy hello dysku nie ma jeszcze szyfrowane z funkcją BitLocker i potrzeb toobe szyfrowane przez narzędzie hello. Jeśli dysk hello już został zaszyfrowany za pomocą funkcji BitLocker, Pomiń ten parametr i określ hello `/bk` parametru, zapewniając hello istniejącego klucza funkcji BitLocker.<br /><br /> Jeśli określisz hello `/format` parametru, możesz także określić hello `/encrypt` parametru.|
|**/BK:**< BitLockerKey\>|`Optional.`Jeśli `/encrypt` jest określony, Pomiń ten parametr. Jeśli `/encrypt` jest pominięty, należy toohave już być zaszyfrowany dysk hello za pomocą funkcji BitLocker. Użyj tego parametru toospecify hello funkcji BitLocker klucza. Szyfrowanie funkcją BitLocker jest wymagany dla wszystkich dysków twardych dla zadania importu.|
|**/ logdir:**< LogDirectory\>|`Optional.`Katalog dziennika Hello określa toobe katalogu używane toostore dzienniki pełne, jak również tymczasowe pliki manifestu. Jeśli nie zostanie określony, bieżący katalog hello będzie używany jako katalog dziennika hello.|

### <a name="parameters-required-for-all-copy-sessions"></a>Parametry wymagane we wszystkich sesjach kopiowania
 plik dziennika Hello zawiera stan hello we wszystkich sesjach kopiowania na dysku twardym. Zawiera także informacje hello potrzebne toocreate hello Importuj zadanie. Zawsze należy określić w pliku dziennika, gdy uruchomiona hello Azure narzędzie importu/eksportu, a także identyfikator sesji kopii:

|||
|-|-|
|Parametr wiersza polecenia|Opis|
|**/j:**< JournalFile\>|`Required.`Witaj ścieżki pliku dziennika toohello. Każdy dysk musi mieć dokładnie jeden plik dziennika. Należy zauważyć, że ten plik dziennika hello nie muszą znajdować się na dysku docelowego hello. rozszerzenie pliku dziennika Hello jest `.jrn`.|
|**/ Identyfikator:**< identyfikator sesji\>|`Required.`Identyfikator sesji Hello identyfikuje sesję kopiowania. Jest używane tooensure odzyskiwania dokładne kopiowania przerwania sesji. Pliki, które są kopiowane w ramach sesji kopiowania są przechowywane w katalogu o nazwie po hello identyfikator sesji na dysku docelowym hello.|

### <a name="parameters-for-copying-a-single-directory"></a>Parametry w celu kopiowania jednego katalogu
 Po skopiowaniu jednego katalogu, zastosuj następujące hello wymaganych i opcjonalnych parametrów:

|Parametr wiersza polecenia|Opis|
|----------------------------|-----------------|
|**/srcdir:**< SourceDirectory\>|`Required.`katalog źródłowy Hello, który zawiera pliki toobe kopiowane toohello dysk docelowy. Ścieżka katalogu Hello musi być ścieżką bezwzględną (nie ścieżkę względną).|
|**/dstdir:**< DestinationBlobVirtualDirectory\>|`Required.`Hello ścieżka toohello wirtualny katalog docelowy na koncie magazynu systemu Windows Azure. katalog wirtualny Hello może lub już nie istnieje.<br /><br /> Możesz określić kontener lub prefiks obiektu blob, takich jak `music/70s/`. Witaj katalog docelowy musi rozpoczynać się od nazwy kontenera hello, następuje ukośnik "/" i opcjonalnie mogą obejmować katalogu wirtualnego obiektów blob, w którym kończy się wyrazem "/".<br /><br /> Witaj kontenera docelowego jest hello nadrzędny kontener, należy jawnie określić, hello nadrzędny kontener, łącznie z ukośnikiem hello, jako `$root/`. Ponieważ nie może zawierać obiekty BLOB w kontenerze głównego hello "/" w nazwach, podkatalogów w katalogu źródłowym hello nie zostaną skopiowane, gdy katalog docelowy hello jest hello nadrzędny kontener.<br /><br /> Można toouse się, że nazwy prawidłowego kontenera podczas określania katalogu wirtualnego w docelowym lub obiektów blob. Należy pamiętać, że nazwy kontenerów muszą być małymi literami. Kontener nazewnictwa reguł, zobacz [nazewnictwa i odwołuje się do kontenerów, obiektów blob i metadanych](/rest/api/storageservices/naming-and-referencing-containers--blobs--and-metadata).|
|**/ Dyspozycji:**< zmienić &#124; zastąpić nie &#124; zastąpić >|`Optional.`Określa zachowanie hello obiektu blob z hello określony adres już istnieje. Prawidłowe wartości tego parametru to: `rename`, `no-overwrite` i `overwrite`. Należy pamiętać, że te wartości jest rozróżniana wielkość liter. Jeśli nie określono wartości, domyślną hello jest `rename`.<br /><br /> wartość określona dla tego parametru dotyczy wszystkich plików hello w katalogu hello określonym przez hello Hello `/srcdir` parametru.|
|**/ BlobType:**< BlockBlob &#124; PageBlob >|`Optional.`Określa typ obiektu blob hello hello docelowego blob. Prawidłowe wartości to: `BlockBlob` i `PageBlob`. Należy pamiętać, że te wartości jest rozróżniana wielkość liter. Jeśli nie określono wartości, domyślną hello jest `BlockBlob`.<br /><br /> W większości przypadków `BlockBlob` jest zalecane. Jeśli określisz `PageBlob`, długość hello poszczególnych plików w katalogu hello musi być wielokrotnością 512, hello rozmiar strony dla stronicowych obiektów blob.|
|**/ PropertyFile:**< PropertyFile\>|`Optional.`Ścieżka pliku właściwości toohello dla obiektów blob docelowego hello. Zobacz [Import/Eksport usługi metadanych i Format pliku właściwości](../storage-import-export-file-format-metadata-and-properties.md) Aby uzyskać więcej informacji.|
|**/ MetadataFile:**< MetadataFile\>|`Optional.`Ścieżka pliku metadanych toohello hello docelowego blob. Zobacz [Import/Eksport usługi metadanych i Format pliku właściwości](../storage-import-export-file-format-metadata-and-properties.md) Aby uzyskać więcej informacji.|

### <a name="parameters-for-copying-a-single-file"></a>Parametry w celu kopiowania pojedynczego pliku
 Podczas kopiowania pojedynczy plik, hello następujących wymaganych i opcjonalnych parametrów zastosowania:

|Parametr wiersza polecenia|Opis|
|----------------------------|-----------------|
|**/srcfile:**< SourceFile\>|`Required.`Witaj Pełna ścieżka toohello pliku toobe skopiowane. Ścieżka katalogu Hello musi być ścieżką bezwzględną (nie ścieżkę względną).|
|**/dstblob:**< DestinationBlobPath\>|`Required.`Witaj ścieżki toohello docelowego obiektu blob na koncie magazynu systemu Windows Azure. Obiekt blob Hello może lub już nie istnieje.<br /><br /> Określ początku nazwy obiektu blob hello o nazwie kontenera hello. Nazwa obiektu blob Hello nie może rozpoczynać się od "/" lub nazwa konta magazynu hello. W przypadku reguł nazewnictwa obiektów blob, zobacz [nazewnictwa i odwołuje się do kontenerów, obiektów blob i metadanych](/rest/api/storageservices/naming-and-referencing-containers--blobs--and-metadata).<br /><br /> Hello kontenera docelowego jest hello nadrzędny kontener, należy jawnie określić `$root` jako hello kontenera, takich jak `$root/sample.txt`. Należy pamiętać, że obiekty BLOB w kontenerze głównego hello nie może zawierać "/" w ich nazwy.|
|**/ Dyspozycji:**< zmienić &#124; zastąpić nie &#124; zastąpić >|`Optional.`Określa zachowanie hello obiektu blob z hello określony adres już istnieje. Prawidłowe wartości tego parametru to: `rename`, `no-overwrite` i `overwrite`. Należy pamiętać, że te wartości jest rozróżniana wielkość liter. Jeśli nie określono wartości, domyślną hello jest `rename`.|
|**/ BlobType:**< BlockBlob &#124; PageBlob >|`Optional.`Określa typ obiektu blob hello hello docelowego blob. Prawidłowe wartości to: `BlockBlob` i `PageBlob`. Należy pamiętać, że te wartości jest rozróżniana wielkość liter. Jeśli nie określono wartości, domyślną hello jest `BlockBlob`.<br /><br /> W większości przypadków `BlockBlob` jest zalecane. Jeśli określisz `PageBlob`, długość hello poszczególnych plików w katalogu hello musi być wielokrotnością 512, hello rozmiar strony dla stronicowych obiektów blob.|
|**/ PropertyFile:**< PropertyFile\>|`Optional.`Ścieżka pliku właściwości toohello dla obiektów blob docelowego hello. Zobacz [Import/Eksport usługi metadanych i Format pliku właściwości](../storage-import-export-file-format-metadata-and-properties.md) Aby uzyskać więcej informacji.|
|**/ MetadataFile:**< MetadataFile\>|`Optional.`Ścieżka pliku metadanych toohello hello docelowego blob. Zobacz [Import/Eksport usługi metadanych i Format pliku właściwości](../storage-import-export-file-format-metadata-and-properties.md) Aby uzyskać więcej informacji.|

### <a name="resuming-an-interrupted-copy-session"></a>Wznawianie sesji przerwania kopiowania
 Jeśli sesja kopiowania zostanie przerwana jakiejkolwiek przyczyny, będzie możliwe wznowienie, uruchamiając narzędzie hello z tylko hello dziennika określonego pliku:

```
WAImportExport.exe PrepImport /j:<JournalFile> /id:<SessionId> /ResumeSession
```

 Tylko hello najnowszej kopii, jeśli zakończył się nienormalnie, można można wznowić sesji.

> [!IMPORTANT]
>  Po wznowieniu sesji kopiowania, nie należy modyfikować hello źródła danych plików i katalogów przez dodanie lub usunięcie plików.

### <a name="aborting-an-interrupted-copy-session"></a>Trwa przerywanie sesji przerwania kopiowania
 Jeśli sesja kopiowania zostanie przerwana i nie jest możliwe tooresume (na przykład, jeżeli katalog źródłowy niedostępny), użytkownik musi przerwać hello bieżącej sesji, dzięki czemu można wycofać Wstecz i następnych sesjach kopiowania, może zostać uruchomiona:

```
WAImportExport.exe PrepImport /j:<JournalFile> /id:<SessionId> /AbortSession
```

 Tylko hello ostatniej sesji kopii, jeśli została zakończona nieprawidłowo, może przerwana. Należy pamiętać, że użytkownik nie można przerwać hello pierwszej sesji kopii dysku. Zamiast tego należy ponownie uruchomić hello kopiowania sesji przy użyciu nowego pliku dziennika.

## <a name="next-steps"></a>Następne kroki

* [Definiowanie hello Azure narzędzie importu/eksportu](storage-import-export-tool-setup-v1.md)
* [Ustawianie właściwości i metadanych podczas hello importowania](storage-import-export-tool-setting-properties-metadata-import-v1.md)
* [Przykładowy przepływ pracy tooprepare dysków dla zadania importu](storage-import-export-tool-sample-preparing-hard-drives-import-job-workflow-v1.md)
* [Krótki przewodnik dla często używanych poleceń](storage-import-export-tool-quick-reference-v1.md) 
* [Sprawdzanie stanu zadania za pomocą plików dziennika kopiowania](storage-import-export-tool-reviewing-job-status-v1.md)
* [Naprawianie zadania importu](storage-import-export-tool-repairing-an-import-job-v1.md)
* [Naprawianie zadania eksportu](storage-import-export-tool-repairing-an-export-job-v1.md)
* [Rozwiązywanie problemów z hello Azure narzędzie importu/eksportu](storage-import-export-tool-troubleshooting-v1.md)
