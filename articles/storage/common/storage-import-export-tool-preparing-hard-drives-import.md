---
title: dyski twarde aaaPreparing dla Import/Eksport Azure Importuj zadanie | Dokumentacja firmy Microsoft
description: "Dowiedz się, jak dyski twarde tooprepare przy użyciu hello WAImportExport narzędzie toocreate zadania importu dla hello usługi Import/Eksport Azure."
author: muralikk
manager: syadav
editor: tysonn
services: storage
documentationcenter: 
ms.assetid: 
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/29/2017
ms.author: muralikk
ms.openlocfilehash: dc4f4f580f70dbd504317f59df142b3e4c48cb66
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="preparing-hard-drives-for-an-import-job"></a>Przygotowywanie dyski twarde dla zadania importu

Witaj WAImportExport jest narzędzie przygotowania dysku hello i narzędzia do naprawy używanej w hello [usługi Import/Eksport Microsoft Azure](../storage-import-export-service.md). Można użyć tego narzędzia toocopy danych toohello dyski twarde ma tooan tooship centrum danych Azure. Po zakończeniu zadania importu można toorepair to narzędzie żadnych obiektów blob, które zostały uszkodzone, brakuje lub konflikt z innymi obiektami blob. Po otrzymaniu hello dysków z zadania eksportu ukończone, można użyć toorepair tego narzędzia, wszystkie pliki, które zostały uszkodzone lub brakujące na dyskach hello. W tym artykule rozszerzana za pośrednictwem hello Użyj tego narzędzia.

## <a name="prerequisites"></a>Wymagania wstępne

### <a name="requirements-for-waimportexportexe"></a>Wymagania dotyczące WAImportExport.exe

- **Konfiguracja maszyny**
  - Windows 7, Windows Server 2008 R2 lub nowszego systemu operacyjnego Windows
  - Musi być zainstalowany program .NET framework 4. Zobacz [— często zadawane pytania](#faq) na temat toocheck czy .net Framework jest zainstalowana na komputerze hello.
- **Klucz konta magazynu** — należy co najmniej jeden z kluczy konta hello hello konta magazynu.

### <a name="preparing-disk-for-import-job"></a>Przygotowywanie dysku dla zadania importu

- **BitLocker —** na hello maszyny uruchomione narzędzie WAImportExport hello musi być włączona funkcja BitLocker. Zobacz hello [— często zadawane pytania](#faq) jak tooenable funkcji BitLocker.
- **Dyski** dostępny z komputera, na którym jest uruchamiane narzędzie WAImportExport. Zobacz [— często zadawane pytania](#faq) do określenia dysku.
- **Pliki źródłowe** — planowanie tooimport pliki hello musi być dostępny z komputera kopiowania hello, czy znajdują się w udziale sieciowym lub na lokalnym dysku twardym.

### <a name="repairing-a-partially-failed-import-job"></a>Naprawianie zadania importu częściowo nie powiodło się

- **Kopiuj plik dziennika** generowany po usługi Import/Eksport Azure umożliwia skopiowanie danych między konta magazynu i dysku. Znajduje się na koncie magazynu docelowego.

### <a name="repairing-a-partially-failed-export-job"></a>Naprawianie zadania eksportu częściowo nie powiodło się

- **Kopiuj plik dziennika** generowany po usługi Import/Eksport Azure umożliwia skopiowanie danych między konta magazynu i dysku. Znajduje się na koncie magazynu źródłowego.
- **Plik manifestu** -znajdują się [opcjonalnie] na dysku wyeksportowany, który został zwrócony przez firmę Microsoft.

## <a name="download-and-install-waimportexport"></a>Pobierz i zainstaluj WAImportExport

Pobierz hello [najnowszej wersji WAImportExport.exe](https://www.microsoft.com/download/details.aspx?id=55280). Wyodrębnij hello zip tooa zawartości katalogu na komputerze.

Następnym zadaniem jest toocreate plików CSV.

## <a name="prepare-hello-dataset-csv-file"></a>Przygotowanie pliku CSV hello zestawu danych

### <a name="what-is-dataset-csv"></a>Co to jest zestaw danych CSV

Plik CSV zestawu danych jest hello wartość flagi /dataset jest plik CSV, który zawiera listę katalogów i/lub listę dysków tootarget toobe kopiowane pliki. Witaj pierwszy krok toocreating zadania importu jest toodetermine które katalogi i pliki będą tooimport. Może to być lista katalogów, lista plików unikatowy lub kombinacji tych dwóch. Jeśli katalog, wszystkie pliki w katalogu hello i jego podkatalogach będzie częścią hello zadania importu.

Dla każdego pliku lub katalogu toobe zaimportowane należy określić katalog wirtualny docelowego lub obiektu blob w hello usługi obiektów Blob platformy Azure. Jako dane wejściowe toohello WAImportExport narzędzia użyje następujących elementów docelowych. Katalogi powinien rozdzielone znakiem ukośnika hello "/".

Witaj w poniższej tabeli przedstawiono kilka przykładów elementów docelowych obiektów blob:

| Pliku lub katalogu źródłowego | Docelowego obiektu blob lub katalogu wirtualnego |
| --- | --- |
| H:\Video | https://mystorageaccount.blob.Core.Windows.NET/Video |
| H:\Photo | https://mystorageaccount.blob.Core.Windows.NET/Photo |
| K:\Temp\FavoriteVideo.ISO | https://mystorageaccount.blob.Core.Windows.NET/favorite/FavoriteVideo.ISO |
| \\myshare\john\music | https://mystorageaccount.blob.Core.Windows.NET/Music |

### <a name="sample-datasetcsv"></a>Dataset.csv próbki

```
BasePath,DstBlobPathOrPrefix,BlobType,Disposition,MetadataFile,PropertiesFile
"F:\50M_original\100M_1.csv.txt","containername/100M_1.csv.txt",BlockBlob,rename,"None",None
"F:\50M_original\","containername/",BlockBlob,rename,"None",None
```

### <a name="dataset-csv-file-fields"></a>Pola z pliku CSV zestawu danych

| Pole | Opis |
| --- | --- |
| Nieistniejący | **[Wymagane]**<br/>Hello wartość tego parametru reprezentuje źródło hello, gdzie znajduje się toobe danych hello zaimportowane. Narzędzie Hello będzie rekursywnie kopię wszystkich danych znajdujących się w tej ścieżce.<br><br/>**Dozwolone wartości**: to ma toobe prawidłową ścieżkę na komputerze lokalnym lub prawidłową ścieżką udziału i powinna być dostępna przez użytkownika hello. Ścieżka katalogu Hello musi być ścieżką bezwzględną (nie ścieżkę względną). Jeśli ścieżka hello kończy się wyrazem "\\", reprezentuje ścieżkę, kończenie bez katalogu else"\\" reprezentuje plik.<br/>Nie wyrażenia regularnego jest dozwolony w tym polu. Jeśli ścieżka hello zawiera spacje, umieść ją w "".<br><br/>**Przykład**: "c:\Directory\c\Directory\File.txt"<br>"\\\\FBaseFilesharePath.domain.net\sharename\directory\"  |
| DstBlobPathOrPrefix | **[Wymagane]**<br/> Hello ścieżka toohello wirtualny katalog docelowy na koncie magazynu systemu Windows Azure. katalog wirtualny Hello może lub już nie istnieje. Jeśli nie istnieje, zostanie utworzyć usługi Import/Eksport.<br/><br/>Można toouse się, że nazwy prawidłowego kontenera podczas określania katalogu wirtualnego w docelowym lub obiektów blob. Należy pamiętać, że nazwy kontenerów muszą być małymi literami. Kontener nazewnictwa reguł, zobacz [nazewnictwa i odwołuje się do kontenerów, obiektów blob i metadanych](/rest/api/storageservices/naming-and-referencing-containers--blobs--and-metadata). Głównego jest określony, jeśli tylko struktura katalogów hello źródła hello są replikowane w hello docelowy kontener obiektów blob. Jeśli wymagane jest struktury katalogu innego niż hello jednego źródła, wiele wierszy mapowania w formacie CSV<br/><br/>Można określić kontener lub prefiks obiektu blob, jak muzyka/70s /. Witaj katalog docelowy musi rozpoczynać się od nazwy kontenera hello, następuje ukośnik "/" i opcjonalnie mogą obejmować katalogu wirtualnego obiektów blob, w którym kończy się wyrazem "/".<br/><br/>Witaj kontenera docelowego jest hello nadrzędny kontener, należy jawnie określić, hello głównego kontenera, w tym hello ukośnik, jako $root /. Ponieważ nie może zawierać obiekty BLOB w kontenerze głównego hello "/" w nazwach, podkatalogów w katalogu źródłowym hello nie zostaną skopiowane, gdy katalog docelowy hello jest hello nadrzędny kontener.<br/><br/>**Przykład**<br/>Jeśli hello docelowego obiektu blob https://mystorageaccount.blob.core.windows.net/video, wartość hello to pole może być wideo /  |
| BlobType | **[Opcjonalnie]**  bloku &#124; strony<br/>Obecnie usługa Import/Eksport obsługuje 2 rodzaje obiektów blob. Strona obiekty BLOB i domyślne BlobsBy bloku wszystkie pliki zostaną zaimportowane jako blokowych obiektów blob. I \*VHD i \*vhdx zostanie zaimportowana jako BlobsThere strony jest ograniczeniem hello — obiekt blob blokowy i dozwolony rozmiar obiektu blob na stronie. Zobacz [wartości docelowe skalowalności magazynu](storage-scalability-targets.md#scalability-targets-for-blobs-queues-tables-and-files) Aby uzyskać więcej informacji.  |
| Dyspozycji | **[Opcjonalnie]**  zmienić &#124; zastąpić nie &#124; zastąpić <br/> To pole określa hello kopiowania — zachowanie podczas importowania tj gdy dane są przekazywane toohello konta magazynu z dysku hello. Dostępne są następujące opcje: Zmień nazwę &#124; czy chcesz go zastąpić &#124; zastąpić nie. Ustawienia domyślne zbyt "rename" Jeśli nie określono. <br/><br/>**Zmień nazwę**: obiekt o tej samej nazwie jest obecny, tworzona jest kopia w lokalizacji docelowej.<br/>Zastąp: zastępuje pliku hello nowszy plik. Plik Hello z ostatniej modyfikacji usługi wins.<br/>**Zastąp nr**: pomija zapisywania hello plików, jeśli jeszcze nie istnieje.|
| MetadataFile | **[Opcjonalnie]** <br/>pole toothis wartość Hello jest hello pliku metadanych, który może zostać podany, jeśli hello, co wymaga metadanych hello toopreserve obiektów hello lub podaj niestandardowych metadanych. Ścieżka pliku metadanych toohello hello docelowego blob. Zobacz [Import/Eksport usługi metadanych i Format pliku właściwości](../storage-import-export-file-format-metadata-and-properties.md) Aby uzyskać więcej informacji |
| PropertiesFile | **[Opcjonalnie]** <br/>Ścieżka pliku właściwości toohello dla obiektów blob docelowego hello. Zobacz [Import/Eksport usługi metadanych i Format pliku właściwości](../storage-import-export-file-format-metadata-and-properties.md) Aby uzyskać więcej informacji. |

## <a name="prepare-initialdriveset-or-additionaldriveset-csv-file"></a>Przygotuj plik InitialDriveSet lub AdditionalDriveSet CSV

### <a name="what-is-driveset-csv"></a>Co to jest driveset CSV

Witaj wartość flagi /InitialDriveSet lub /AdditionalDriveSet hello jest plik CSV zawierający hello Lista dysków, które litery dysków hello toowhich są mapowane tak, aby hello narzędzia można poprawnie pobrać hello Lista dysków toobe przygotowane. Rozmiar danych hello jest większy niż rozmiar pojedynczego dysku, narzędzie WAImportExport hello roześle hello danych na wielu dyskach zarejestrowany w tym pliku CSV w sposób zoptymalizowane.

Brak limitu hello liczby dysków hello danych mogą być zapisywane tooin w jednej sesji. Narzędzie Hello przeprowadził dystrybucję danych na podstawie rozmiaru dysku i rozmiar folderu. Będzie wybierać dysku hello większości zoptymalizowane pod kątem rozmiar obiektu hello. Witaj danych po przekazaniu toohello konta magazynu będzie konwergentnej toohello wstecz struktury katalogów, która została określona w pliku zestawu danych. W kolejności toocreate driveset CSV wykonaj poniższe kroki hello.

### <a name="create-basic-volume-and-assign-drive-letter"></a>Tworzenie woluminu podstawowego i przypisz literę dysku

W kolejności toocreate woluminu podstawowego i przypisać literę dysku, wykonując następujące instrukcje hello "Łatwiejsze tworzenie partycji" podany w [omówienie zarządzania dyskami](https://technet.microsoft.com/library/cc754936.aspx).

### <a name="sample-initialdriveset-and-additionaldriveset-csv-file"></a>Plik przykładowy InitialDriveSet i AdditionalDriveSet CSV

```
DriveLetter,FormatOption,SilentOrPromptOnFormat,Encryption,ExistingBitLockerKey
G,AlreadyFormatted,SilentMode,AlreadyEncrypted,060456-014509-132033-080300-252615-584177-672089-411631
H,Format,SilentMode,Encrypt,
```

### <a name="driveset-csv-file-fields"></a>Pola z pliku Driveset CSV

| Pola | Wartość |
| --- | --- |
| Litera dysku | **[Wymagane]**<br/> Każdy dysk, który jest świadczona narzędzia toohello jako miejsce docelowe hello musi mieć prosty wolumin NTFS na nim i tooit przypisać literę dysku.<br/> <br/>**Przykład**: R lub r |
| FormatOption | **[Wymagane]**  Format &#124; AlreadyFormatted<br/><br/> **Format**: określenie tej sformatuje wszystkie dane hello hello dysku. <br/>**AlreadyFormatted**: narzędzie hello pominie formatowanie, gdy ta wartość jest określona. |
| SilentOrPromptOnFormat | **[Wymagane]**  SilentMode &#124; PromptOnFormat<br/><br/>**SilentMode**: podanie tej wartości spowoduje włączenie narzędzie hello toorun użytkownika w trybie dyskretnym. <br/>**PromptOnFormat**: hello narzędzie wyświetli monit o hello tooconfirm użytkownika, czy hello naprawdę akcja w każdym format.<br/><br/>Jeśli nie jest ustawiona, polecenie przerwania i wyświetlony komunikat o błędzie: "Nieprawidłowa wartość parametru SilentOrPromptOnFormat: none" |
| Szyfrowanie | **[Wymagane]**  Szyfrowania &#124; AlreadyEncrypted<br/> Witaj wartość tego pola decyduje o tym, które tooencrypt dysku, które nie. <br/><br/>**Szyfrowanie**: narzędzie sformatuje dysk hello. Jeśli jest wartość pola "FormatOption", "Format" Ta wartość jest wymagana toobe "Szyfruj". Jeśli "AlreadyEncrypted" jest określona w tym przypadku, spowoduje wystąpił błąd "W przypadku Format Szyfruj należy także określić".<br/>**AlreadyEncrypted**: narzędzie powoduje odszyfrowania dysku hello za pomocą hello BitLockerKey pole "ExistingBitLockerKey". Jeśli wartość pola "FormatOption" to "AlreadyFormatted", następnie ta wartość może być "Szyfruj" lub "AlreadyEncrypted" |
| ExistingBitLockerKey | **[Wymagane]**  Jeśli wartość pola "Szyfrowanie" to "AlreadyEncrypted"<br/> Hello wartość tego pola jest hello funkcji BitLocker klucz, który jest skojarzony z hello określonego dysku. <br/><br/>To pole powinno pozostać puste, jeśli wartość pola "Szyfrowanie" hello "Szyfruj".  W takim przypadku określono klucza funkcji BitLocker, go spowoduje wystąpił błąd "Nie należy określać klucza funkcji Bitlocker".<br/>  **Przykład**: 060456-014509-132033-080300-252615-584177-672089-411631|

##  <a name="preparing-disk-for-import-job"></a>Przygotowywanie dysku dla zadania importu

Narzędzie WAImportExport hello z hello wywołać tooprepare dysków dla zadania importu **PrepImport** polecenia. Parametry, które możesz uwzględnić zależy od tego, czy jest to hello pierwszego kopiowania sesji lub sesji kolejnych kopii.

### <a name="first-session"></a>Pierwsza sesja

Pierwszy tooCopy sesji kopiowania katalogu Single/Multiple tooa pojedynczej/wiele WAImportExport dysku (w zależności od tego, co jest określony w pliku CSV) Narzędzie polecenie PrepImport dla hello najpierw skopiować sesji toocopy katalogów i/lub pliki w nowej sesji kopiowania:

```
WAImportExport.exe PrepImport /j:<JournalFile> /id:<SessionId> [/logdir:<LogDirectory>] [/sk:<StorageAccountKey>] [/silentmode] [/InitialDriveSet:<driveset.csv>] DataSet:<dataset.csv>
```

**Przykład:**

```
WAImportExport.exe PrepImport /j:JournalTest.jrn /id:session#1  /sk:\*\*\*\*\*\*\*\*\*\*\*\*\* /InitialDriveSet:driveset-1.csv /DataSet:dataset-1.csv /logdir:F:\logs
```

### <a name="add-data-in-subsequent-session"></a>Dodawanie danych w kolejnych sesji

W kolejnych kopii sesji nie trzeba parametrów początkowych hello toospecify. Należy toouse hello tego samego pliku dziennika w kolejności dla tooremember narzędzie hello gdzie pozostawiany w hello poprzedniej sesji. Stan Hello hello kopiowania sesji jest zapisywany toohello pliku dziennika. Oto składnia hello kolejnych kopii sesji toocopy dodatkowe katalogi i pliki:

```
WAImportExport.exe PrepImport /j:<SameJournalFile> /id:<DifferentSessionId>  [DataSet:<differentdataset.csv>]
```

**Przykład:**

```
WAImportExport.exe PrepImport /j:JournalTest.jrn /id:session#2  /DataSet:dataset-2.csv
```

### <a name="add-drives-toolatest-session"></a>Dodawanie dysków toolatest sesji

Jeśli hello dane nie mieszczą się w określone dyski w InitialDriveset, jeden Użyj hello narzędzia tooadd dodatkowych dysków toosame kopiowania sesji. 

>[!NOTE] 
>Identyfikator sesji Hello powinna odpowiadać hello identyfikator poprzedniej sesji. Plik dziennika powinien być zgodny hello określona w poprzedniej sesji.
>
```
WAImportExport.exe PrepImport /j:<SameJournalFile> /id:<SameSessionId> /AdditionalDriveSet:<newdriveset.csv>
```

**Przykład:**

```
WAImportExport.exe PrepImport /j:SameJournalTest.jrn /id:session#2  /AdditionalDriveSet:driveset-2.csv
```

### <a name="abort-hello-latest-session"></a>Przerwij hello najnowszych sesji:

Jeśli sesja kopiowania zostanie przerwana i nie jest możliwe tooresume (na przykład, jeżeli katalog źródłowy niedostępny), użytkownik musi przerwać hello bieżącej sesji, dzięki czemu można wycofać Wstecz i następnych sesjach kopiowania, może zostać uruchomiona:

```
WAImportExport.exe PrepImport /j:<SameJournalFile> /id:<SameSessionId> /AbortSession
```

**Przykład:**

```
WAImportExport.exe PrepImport /j:JournalTest.jrn /id:session#2  /AbortSession
```

Tylko hello ostatniej sesji kopii, jeśli została zakończona nieprawidłowo, może przerwana. Należy pamiętać, że użytkownik nie można przerwać hello pierwszej sesji kopii dysku. Zamiast tego należy ponownie uruchomić hello kopiowania sesji przy użyciu nowego pliku dziennika.

### <a name="resume-a-latest-interrupted-session"></a>Wznów najnowszych przerwania sesji

Jeśli sesja kopiowania zostanie przerwana jakiejkolwiek przyczyny, będzie możliwe wznowienie, uruchamiając narzędzie hello z tylko hello dziennika określonego pliku:

```
WAImportExport.exe PrepImport /j:<SameJournalFile> /id:<SameSessionId> /ResumeSession
```

**Przykład:**

```
WAImportExport.exe PrepImport /j:JournalTest.jrn /id:session#2 /ResumeSession
```

> [!IMPORTANT] 
> Po wznowieniu sesji kopiowania, nie należy modyfikować hello źródła danych plików i katalogów przez dodanie lub usunięcie plików.

## <a name="waimportexport-parameters"></a>Parametry WAImportExport

| Parametry | Opis |
| --- | --- |
|     /j:&lt;JournalFile&gt;  | **Wymagane**<br/> Ścieżka pliku dziennika toohello. W pliku dziennika śledzi zestaw dysków i rekordy hello postęp w celu przygotowania tych dysków. zawsze należy określać Hello pliku dziennika.  |
|     / logdir:&lt;LogDirectory&gt;  | **Opcjonalnie**. Katalog dziennika Hello.<br/> Pliki dziennika pełne, jak również niektórych plików tymczasowych zostanie zapisany toothis katalogu. Jeśli nie jest określony, bieżącego katalogu będzie używany jako katalog dziennika hello. Witaj katalog dziennika można określić tylko raz dla hello tego samego pliku dziennika.  |
|     / Identyfikator:&lt;SessionId&gt;  | **Wymagane**<br/> sesji Hello identyfikator jest używany tooidentify sesję kopiowania. Jest używane tooensure odzyskiwania dokładne kopiowania przerwania sesji.  |
|     / ResumeSession  | Opcjonalny. Jeśli hello ostatniej sesji kopiowania zostało nieprawidłowo zakończone, ten parametr może być określony tooresume hello sesji.   |
|     / AbortSession  | Opcjonalny. Jeśli hello ostatniej sesji kopiowania zostało nieprawidłowo zakończone, ten parametr może być określony tooabort hello sesji.  |
|     /SN:&lt;StorageAccountName&gt;  | **Wymagane**<br/> Dotyczy tylko RepairImport i RepairExport. Nazwa Hello hello konta magazynu.  |
|     /SK:&lt;StorageAccountKey&gt;  | **Wymagane**<br/> klucz Hello hello konta magazynu. |
|     / InitialDriveSet:&lt;driveset.csv&gt;  | **Wymagane** podczas uruchamiania hello pierwszego kopiowania sesji<br/> Plik CSV, który zawiera listę dysków tooprepare.  |
|     / AdditionalDriveSet:&lt;driveset.csv&gt; | **Wymagane**. Podczas dodawania dysków toocurrent kopiowania sesji. <br/> Plik CSV, który zawiera listę dodatkowych dysków toobe dodane.  |
|      / r:&lt;RepairFile&gt; | **Wymagane** dotyczy tylko RepairImport i RepairExport.<br/> Ścieżka pliku toohello śledzenie postępu naprawy. Każdy dysk musi mieć jeden i tylko jeden plik naprawy.  |
|     / d:&lt;TargetDirectories&gt; | **Wymagane**. Dotyczy tylko RepairImport i RepairExport. Dla RepairImport jeden lub więcej katalogów średnikami toorepair; Dla RepairExport, toorepair jeden katalog, np. główny katalog hello dysku.  |
|     / CopyLogFile:&lt;DriveCopyLogFile&gt; | **Wymagane** dotyczy tylko RepairImport i RepairExport. Plik dziennika kopii dysku toohello ścieżki (pełne lub błędów).  |
|     / ManifestFile:&lt;DriveManifestFile&gt; | **Wymagane** dotyczy tylko RepairExport.<br/> Toohello ścieżki dysku pliku manifestu.  |
|     / PathMapFile:&lt;DrivePathMapFile&gt; | **Opcjonalnie**. Dotyczy tylko RepairImport.<br/> Ścieżka pliku toohello zawierające mapowania pliku ścieżki względnej toohello dysku głównego toolocations rzeczywiste plików (rozdzielany znakami tabulacji). W przypadku najpierw go zostanie wypełniona ścieżki plików z obiektami docelowymi puste, co oznacza nie zostały znalezione w TargetDirectories, odmowa dostępu, o nieprawidłowej nazwie albo istnieją w wielu katalogach. Witaj ścieżki mapy pliku mogą być ręcznie edytowane tooinclude hello docelowy o poprawnej ścieżki i ponownie dla ścieżki plików hello hello narzędzia tooresolve poprawnie określona.  |
|     / ExportBlobListFile:&lt;ExportBlobListFile&gt; | **Wymagane**. Dotyczy tylko PreviewExport.<br/> Ścieżka toohello XML pliku zawierającego listę obiektów blob ścieżek lub obiektu blob prefiksy ścieżki dla toobe obiekty BLOB hello wyeksportowane. format pliku Hello jest sama hello hello blob listę obiektów blob formatu w hello zawiesić zadanie działanie interfejsu API REST usługi Import/Eksport hello.  |
|     / DriveSize:&lt;DriveSize&gt; | **Wymagane**. Dotyczy tylko PreviewExport.<br/>  Rozmiar dysków toobe używany do eksportu. Na przykład, 500 GB, 1,5 TB. Uwaga: 1 GB = 1 000 000 000 bytes1 TB = 1,000,000,000,000 bajtów  |
|     / DataSet:&lt;dataset.csv&gt; | **Wymagane**<br/> Pliku CSV, który zawiera listę katalogów i/lub listę toobe pliki kopiowane tootarget dysków.  |
|     /silentmode  | **Opcjonalnie**.<br/> Jeśli nie zostanie określony, będzie to przypomnienie hello wymaganie dysków i wymagają toocontinue Twojego potwierdzenia.  |

## <a name="tool-output"></a>Dane wyjściowe narzędzia

### <a name="sample-drive-manifest-file"></a>Przykładowy plik manifestu dysku

```xml
<?xml version="1.0" encoding="UTF-8"?>
<DriveManifest Version="2011-MM-DD">
   <Drive>
      <DriveId>drive-id</DriveId>
      <StorageAccountKey>storage-account-key</StorageAccountKey>
      <ClientCreator>client-creator</ClientCreator>
      <!-- First Blob List -->
      <BlobList Id="session#1-0">
         <!-- Global properties and metadata that applies tooall blobs -->
         <MetadataPath Hash="md5-hash">global-metadata-file-path</MetadataPath>
         <PropertiesPath Hash="md5-hash">global-properties-file-path</PropertiesPath>
         <!-- First Blob -->
         <Blob>
            <BlobPath>blob-path-relative-to-account</BlobPath>
            <FilePath>file-path-relative-to-transfer-disk</FilePath>
            <ClientData>client-data</ClientData>
            <Length>content-length</Length>
            <ImportDisposition>import-disposition</ImportDisposition>
            <!-- page-range-list-or-block-list -->
            <!-- page-range-list -->
            <PageRangeList>
               <PageRange Offset="1073741824" Length="512" Hash="md5-hash" />
               <PageRange Offset="1073741824" Length="512" Hash="md5-hash" />
            </PageRangeList>
            <!-- block-list -->
            <BlockList>
               <Block Offset="1073741824" Length="4194304" Id="block-id" Hash="md5-hash" />
               <Block Offset="1073741824" Length="4194304" Id="block-id" Hash="md5-hash" />
            </BlockList>
            <MetadataPath Hash="md5-hash">metadata-file-path</MetadataPath>
            <PropertiesPath Hash="md5-hash">properties-file-path</PropertiesPath>
         </Blob>
      </BlobList>
   </Drive>
</DriveManifest>
```

### <a name="sample-journal-file-xml-for-each-drive"></a>Przykładowy plik dziennika (XML) dla każdego dysku

```xml
[BeginUpdateRecord][2016/11/01 21:22:25.379][Type:ActivityRecord]
ActivityId: DriveInfo
DriveState: [BeginValue]
<?xml version="1.0" encoding="UTF-8"?>
<Drive>
   <DriveId>drive-id</DriveId>
   <BitLockerKey>*******</BitLockerKey>
   <ManifestFile>\DriveManifest.xml</ManifestFile>
   <ManifestHash>D863FE44F861AE0DA4DCEAEEFFCCCE68</ManifestHash> </Drive>
[EndValue]
SaveCommandOutput: Completed
[EndUpdateRecord]
```

### <a name="sample-journal-file-jrn-for-session-that-records-hello-trail-of-sessions"></a>Przykładowy plik dziennika (JRN) dla sesji, który rejestruje hello dziennik sesji

```
[BeginUpdateRecord][2016/11/02 18:24:14.735][Type:NewJournalFile]
VocabularyVersion: 2013-02-01
[EndUpdateRecord]
[BeginUpdateRecord][2016/11/02 18:24:14.749][Type:ActivityRecord]
ActivityId: PrepImportDriveCommandContext
LogDirectory: F:\logs
[EndUpdateRecord]
[BeginUpdateRecord][2016/11/02 18:24:14.754][Type:ActivityRecord]
ActivityId: PrepImportDriveCommandContext
StorageAccountKey: *******
[EndUpdateRecord]
```

## <a name="faq"></a>Często zadawane pytania

### <a name="general"></a>Ogólne

#### <a name="what-is-waimportexport-tool"></a>Co to jest narzędzie WAImportExport?

Narzędzie WAImportExport Hello jest przygotowanie stacji hello i narzędzia do naprawy używanej w hello usługi Import/Eksport Microsoft Azure. Można użyć tego narzędzia toocopy danych toohello dyski twarde ma centrum danych Azure tooan tooship. Po zakończeniu zadania importu można toorepair to narzędzie żadnych obiektów blob, które zostały uszkodzone, brakuje lub konflikt z innymi obiektami blob. Po otrzymaniu hello dysków z zadania eksportu ukończone, można użyć toorepair tego narzędzia, wszystkie pliki, które zostały uszkodzone lub brakujące na dyskach hello.

#### <a name="how-does-hello-waimportexport-tool-work-on-multiple-source-dir-and-disks"></a>Jak ma hello WAImportExport narzędzia działają w wielu dir źródła i dyski?

Jeśli rozmiar danych hello jest większy niż rozmiar dysku hello, narzędzie WAImportExport hello dystrybucji hello danych na dyskach hello w sposób zoptymalizowane. dyski toomultiple kopiowania danych Hello może odbywać się równolegle lub sekwencyjnie. Brak limitu hello liczby dysków hello danych mogą być zapisywane toosimultaneously. Narzędzie Hello przeprowadził dystrybucję danych na podstawie rozmiaru dysku i rozmiar folderu. Będzie wybierać dysku hello większości zoptymalizowane pod kątem rozmiar obiektu hello. Witaj danych po przekazaniu toohello konta magazynu będzie można ponownie zbieżność toohello określonej struktury katalogów.

#### <a name="where-can-i-find-previous-version-of-waimportexport-tool"></a>Gdzie można znaleźć wcześniejszej wersji narzędzia WAImportExport?

Narzędzie WAImportExport zawiera wszystkie funkcje, których zastosowano narzędzie WAImportExport V1. WAImportExport pozwala użytkownikom toospecify wielu źródeł i dyski toomultiple zapisu. Ponadto jedną łatwe zarządzanie wiele lokalizacji źródłowej, z których dane hello muszą toobe skopiowany w pojedynczym pliku CSV. Jednak w przypadku należy SAS obsługi lub mają toocopy jednego źródła toosingle dysku, możesz [narzędzie można pobrać WAImportExport V1] (http://go.microsoft.com/fwlink/? LinkID = 301900&amp;clcid = 0x409) i odwoływać się za[odwołania V1 WAImportExport](storage-import-export-tool-how-to-v1.md) Aby uzyskać pomoc dotyczącą użycia WAImportExport V1.

#### <a name="what-is-a-session-id"></a>Co to jest identyfikator sesji?

Narzędzie Hello oczekuje hello kopiowania sesji (/ id) toobe parametru hello takie same, jeśli celem użycia hello toospread hello dane na wielu dyskach. Obsługa hello sama nazwa sesji kopiowania hello spowoduje włączenie użytkownika toocopy danych z jednego lub wielu lokalizacji źródłowej do jednego lub wielu dysków/katalogów docelowych. Obsługa tego samego identyfikatora sesji umożliwia toopick narzędzie hello hello kopię plików, których ona pozostawało hello czas ostatniego.

Jednak tej samej sesji kopiowania nie może być kont magazynu toodifferent tooimport używane w danych.

Gdy nazwa sesji kopiowania jest taka sama na wiele przebiegów narzędzia hello, hello pliku dziennika (/ logdir) i klucz konta magazynu (/ sk) jest również oczekiwanego toobe hello takie same.

SessionId może składać się z liter, 0 ~ 9, understore (\_), myślnik (-) lub skrótu (#), a jego długość musi wynosić 3 ~ 30.

np. 1 sesji lub sesji #1 lub sesji\_1

#### <a name="what-is-a-journal-file"></a>Co to jest plik dziennika?

Zawsze, gdy Uruchom hello WAImportExport narzędzie toocopy pliki toohello dysk twardy, narzędzie hello tworzy sesji kopiowania. Stan Hello hello kopiowania sesji jest zapisywany toohello pliku dziennika. Jeśli sesji kopiowania zostanie przerwana (na przykład powodu utraty zasilania systemu tooa), może zostać wznowiony ponownie uruchomić narzędzie hello i określając hello pliku dziennika w wierszu polecenia hello.

Dla każdego dysku twardym, którego można przygotować z hello Azure narzędzie importu/eksportu, hello narzędzie utworzy plik dziennika jednego o nazwie "&lt;Identyfikator_dysku&gt;XML" w przypadku, gdy dysk identyfikator jest numer seryjny hello skojarzone dysk toohello hello Narzędzie odczytuje z Witaj dysku. Pliki dziennika hello należy ze wszystkich zadania importu hello toocreate dysków. Hello pliku dziennika można także przygotowanie stacji tooresume używane, jeśli narzędzie hello zostanie przerwana.

#### <a name="what-is-a-log-directory"></a>Co to jest katalog dziennika?

Katalog dziennika Hello określa toobe katalogu używane toostore dzienniki pełne, jak również tymczasowe pliki manifestu. Jeśli nie zostanie określony, bieżący katalog hello będzie używany jako katalog dziennika hello. Dzienniki Hello są pełne dzienniki.

### <a name="prerequisites"></a>Wymagania wstępne

#### <a name="what-are-hello-specifications-of-my-disk"></a>Co to są hello specyfikacji dysku?

Pusty SATA II o 2,5 cala lub 3,5 cala lub III lub SSD twardych dysków podłączonych toohello kopiowania maszyny.

#### <a name="how-can-i-enable-bitlocker-on-my-machine"></a>Jak włączyć funkcję BitLocker na moim komputerze?

Prosty sposób toocheck jest klikając prawym przyciskiem myszy na dysku systemowym. Przedstawiono w nim opcje przez funkcję Bitlocker, jeśli jest włączona funkcja hello. Jeśli jest wyłączone, nie zobaczysz go.

![Sprawdź funkcji BitLocker](./media/storage-import-export-tool-preparing-hard-drives-import/BitLocker.png)

Oto artykułu na [jak tooenable funkcji BitLocker](https://technet.microsoft.com/library/cc766295.aspx)

Istnieje możliwość, że ten komputer nie ma moduł TPM. Jeśli nie są dane wyjściowe na podstawie tpm.msc, przyjrzeć się dalej hello — często zadawane pytania.

#### <a name="how-toodisable-trusted-platform-module-tpm-in-bitlocker"></a>Jak toodisable zaufane Platform Module (TPM) w funkcji BitLocker?
> [!NOTE]
> Tylko wtedy, gdy w swoich serwerów nie ma żadnych modułu TPM, należy toodisable zasady modułu TPM. Nie jest konieczne toodisable modułu TPM w przypadku zaufanej modułu TPM na serwerze przez użytkownika. 
> 

W kolejności toodisable modułu TPM w funkcji BitLocker go za pośrednictwem hello następujące kroki:<br/>
1. Uruchom **Edytor zasad grupy** , wpisując w wierszu polecenia gpedit.msc. Jeśli **Edytor zasad grupy** toobe pojawi się niedostępny, najpierw włączenia funkcji BitLocker. Zobacz poprzednie — często zadawane pytania.
2. Otwórz **lokalnych zasad komputera &gt; Konfiguracja komputera &gt; Szablony administracyjne &gt; składniki systemu Windows&gt; szyfrowanie dysków funkcją BitLocker &gt; dyski z systemem operacyjnym**.
3. Edytuj **wymaga dodatkowego uwierzytelniania przy uruchamianiu** zasad.
4. Ustawienie zasad hello zbyt**włączone** i upewnij się, że **Zezwalaj na funkcję BitLocker bez zgodny moduł TPM** jest zaznaczony.

####  <a name="how-toocheck-if-net-4-or-higher-version-is-installed-on-my-machine"></a>Jak toocheck, jeśli na komputerze jest zainstalowany .NET 4 lub nowszej wersji?

Wszystkie wersje programu Microsoft .NET Framework są zainstalowane w następującym katalogu: %windir%\Microsoft.NET\Framework\

Przejdź toohello wyżej wymienione części na komputerze docelowym, z którym narzędzie hello musi toorun. Wyszukaj nazwę folderu, począwszy od wersji "4". Brak takiego katalogu oznacza, że .NET 4 nie jest zainstalowany na tym komputerze. Możesz pobrać .net 4 na przy użyciu maszyny [Microsoft .NET Framework 4 (Instalator internetowy)](https://www.microsoft.com/download/details.aspx?id=17851).

### <a name="limits"></a>Limity

#### <a name="how-many-drives-can-i-preparesend-at-hello-same-time"></a>Jak wiele dysków może I przygotowanie/Wyślij na powitania jednocześnie?

Brak limitu hello liczby dysków, które hello narzędzia można przygotować. Jednak narzędzie hello oczekuje litery dysku jako dane wejściowe. Który ogranicza ją too25 przygotowywania dysków jednocześnie. Pojedyncze zadanie może obsługiwać maksymalnie 10 dysków jednocześnie. Przygotowując dyski więcej niż 10 elementów docelowych hello tego samego konta magazynu, hello dyski mogą być rozproszone na wielu zadań.

#### <a name="can-i-target-more-than-one-storage-account"></a>Czy mogę wskazać więcej niż jedno konto magazynu?

Może zostać przesłane tylko jedno konto magazynu, na zadanie i w sesji pojedynczej kopii.

### <a name="capabilities"></a>Możliwości

#### <a name="does-waimportexportexe-encrypt-my-data"></a>WAImportExport.exe szyfrują dane?

Tak. Szyfrowanie funkcją BitLocker jest włączona i jest wymagane dla tego procesu.

#### <a name="what-will-be-hello-hierarchy-of-my-data-when-it-appears-in-hello-storage-account"></a>Jaki będzie hierarchii hello dane, gdy pojawi się on na koncie magazynu hello?

Mimo że dane są przesyłane na dyskach, hello danych po przekazaniu toohello konta magazynu będzie zbieżność kopii toohello struktury katalogów, określone w pliku CSV hello zestawu danych.

#### <a name="how-many-of-hello-input-disks-will-have-active-io-in-parallel-when-copy-is-in-progress"></a>Ile hello wejściowej dysków będą mieć aktywne we/wy równolegle, podczas kopiowania jest w toku?

Narzędzie Hello dystrybuuje danych na dyskach wejściowego hello na podstawie rozmiaru hello hello plików wejściowych. Inaczej mówiąc, hello liczba aktywnych dysków równolegle całkowicie delends na powitania rodzaj hello danych wejściowych. W zależności od rozmiaru hello poszczególnych plików w zestawie danych wejściowych hello co najmniej jednego dysku mogą być wyświetlane we/wy active równolegle. Zobacz następne pytanie, aby uzyskać więcej informacji.

#### <a name="how-does-hello-tool-distribute-hello-files-across-hello-disks"></a>Jak narzędzie hello rozpowszechniają pliki hello hello dyski?

Narzędzie WAImportExport odczytuje i zapisuje pliki partiami, jedna partia zawiera maksymalnie 100000 plików. Oznacza to, że maksymalna 100000 można zapisywać pliki równoległe. Toosimultaneously, jeśli te pliki 100000 są dystrybuowane toomulti dyski są zapisywane wiele dysków. Jednak czy narzędzie hello zapisuje dysków toomultiple jednocześnie lub hello całkowity rozmiar partii hello zależy od jednego dysku. Na przykład w przypadku mniejszych plików po są wszystkie pliki 10,0000 stanie toofit w pojedynczej stacji, narzędzie zapisze tooonly jednego dysku podczas przetwarzania hello tej partii.

### <a name="waimportexport-output"></a>Dane wyjściowe WAImportExport

#### <a name="there-are-two-journal-files-which-one-should-i-upload-tooazure-portal"></a>Istnieją dwa pliki dziennika, które z nich powinien I Przekaż tooAzure portal?

**.XML** — dla każdego dysku twardym, którego można przygotować narzędziem WAImportExport hello, hello narzędzie utworzy plik dziennika jednego o nazwie `<DriveID>.xml` w przypadku Identyfikator_dysku numer seryjny hello skojarzone dysk toohello hello Narzędzie odczytuje z hello dysku. Pliki dziennika hello należy ze wszystkich dysków toocreate hello importu zadania hello portalu Azure. Ten plik dziennika można także przygotowanie stacji tooresume używane, jeśli narzędzie hello zostanie przerwana.

**.jrn** -hello pliku dziennika z sufiksem `.jrn` zawiera stan hello we wszystkich sesjach kopiowania na dysku twardym. Zawiera także informacje hello potrzebne toocreate hello Importuj zadanie. Zawsze należy określić w pliku dziennika, gdy uruchomione narzędzie WAImportExport hello, a także sesji kopii identyfikatora.

## <a name="next-steps"></a>Następne kroki

* [Definiowanie hello Azure narzędzie importu/eksportu](storage-import-export-tool-setup.md)
* [Ustawianie właściwości i metadanych podczas hello importowania](storage-import-export-tool-setting-properties-metadata-import.md)
* [Przykładowy przepływ pracy tooprepare dysków dla zadania importu](storage-import-export-tool-sample-preparing-hard-drives-import-job-workflow.md)
* [Krótki przewodnik dla często używanych poleceń](storage-import-export-tool-quick-reference.md) 
* [Sprawdzanie stanu zadania za pomocą plików dziennika kopiowania](storage-import-export-tool-reviewing-job-status-v1.md)
* [Naprawianie zadania importu](storage-import-export-tool-repairing-an-import-job-v1.md)
* [Naprawianie zadania eksportu](storage-import-export-tool-repairing-an-export-job-v1.md)
* [Rozwiązywanie problemów z hello Azure narzędzie importu/eksportu](storage-import-export-tool-troubleshooting-v1.md)
