---
title: "aaaCopy lub przenoszenia danych tooAzure magazynu z narzędzia AzCopy w systemie Windows | Dokumentacja firmy Microsoft"
description: "Witaj AzCopy w systemie Windows narzędzie toomove lub kopiowania danych tooor z obiektu blob, tabel i zawartości pliku. Kopiowanie danych tooAzure magazynu z lokalnych plików, lub danych w ramach urządzeń magazynujących lub między kontami magazynu. Łatwo przeprowadzić migrację z tooAzure danych magazynu."
services: storage
documentationcenter: 
author: seguler
manager: jahogg
editor: tysonn
ms.assetid: aa155738-7c69-4a83-94f8-b97af4461274
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/14/2017
ms.author: seguler
ms.openlocfilehash: a063a0380b7b8e6b212d0cec276f7d0f421936ac
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="transfer-data-with-hello-azcopy-on-windows"></a>Transfer danych za pomocą narzędzia AzCopy hello w systemie Windows
Narzędzie AzCopy to narzędzie wiersza polecenia przeznaczone do kopiowania tooand danych z magazynu obiektów Blob Microsoft Azure, plików i tabeli przy użyciu prostych poleceń z optymalną wydajnością. Możesz skopiować dane z jednego obiektu tooanother w ramach konta magazynu lub między kontami magazynu.

Istnieją dwie wersje programu AzCopy, który można pobrać. AzCopy w systemie Windows jest oparty na platformie .NET Framework i oferuje opcje wiersza polecenia Styl systemu Windows. [Narzędzie AzCopy w systemie Linux](storage-use-azcopy-linux.md) wbudowana w .NET Framework Core, który jest przeznaczony dla platformy Linux oferty styl POSIX opcje wiersza polecenia. W tym artykule omówiono AzCopy w systemie Windows.

## <a name="download-and-install-azcopy"></a>Pobierz i zainstaluj narzędzie AzCopy
### <a name="azcopy-on-windows"></a>Narzędzie AzCopy w systemie Windows
Pobierz hello [najnowszą wersję programu AzCopy w systemie Windows](http://aka.ms/downloadazcopy).

#### <a name="installation-on-windows"></a>Instalacja w systemie Windows
Po zainstalowaniu narzędzia AzCopy w systemie Windows za pomocą Instalatora hello, Otwórz okno polecenia i przejdź katalog instalacyjny AzCopy toohello na komputerze — w przypadku gdy hello `AzCopy.exe` wykonywalny znajduje się. W razie potrzeby można dodać ścieżki systemu tooyour lokalizacji instalacji hello AzCopy. Domyślnie program AzCopy jest zainstalowany za`%ProgramFiles(x86)%\Microsoft SDKs\Azure\AzCopy` lub `%ProgramFiles%\Microsoft SDKs\Azure\AzCopy`.

## <a name="writing-your-first-azcopy-command"></a>Pisanie pierwszego polecenia AzCopy
Podstawowa składnia polecenia AzCopy Hello jest:

```azcopy
AzCopy /Source:<source> /Dest:<destination> [Options]
```

Witaj następujące przykłady pokazują różnych scenariuszy kopiowania tooand danych z programu Microsoft Azure blob, tabel i plików. Zobacz toohello [parametrów narzędzia AzCopy](#azcopy-parameters) sekcji, aby uzyskać szczegółowy opis hello parametrami używanymi w każdej próbki.

## <a name="blob-download"></a>Obiekt blob: Pobierz
### <a name="download-single-blob"></a>Pobieranie pojedynczego obiektu blob

```azcopy
AzCopy /Source:https://myaccount.blob.core.windows.net/mycontainer /Dest:C:\myfolder /SourceKey:key /Pattern:"abc.txt"
```

Należy pamiętać, że jeśli hello folder `C:\myfolder` nie istnieje, tworzy AzCopy i pobierania `abc.txt ` do nowego folderu hello.

### <a name="download-single-blob-from-secondary-region"></a>Pobieranie pojedynczego obiektu blob z regionu pomocniczego

```azcopy
AzCopy /Source:https://myaccount-secondary.blob.core.windows.net/mynewcontainer /Dest:C:\myfolder /SourceKey:key /Pattern:abc.txt
```

Należy pamiętać, że użytkownik musi mieć dostęp do odczytu magazynu geograficznie nadmiarowego włączone.

### <a name="download-all-blobs"></a>Pobierz wszystkie obiekty BLOB

```azcopy
AzCopy /Source:https://myaccount.blob.core.windows.net/mycontainer /Dest:C:\myfolder /SourceKey:key /S
```

Załóżmy następujące hello obiekty BLOB znajdują się w określonym kontenerze hello:  

    abc.txt
    abc1.txt
    abc2.txt
    vd1\a.txt
    vd1\abcd.txt

Po wykonaniu operacji pobierania hello hello katalogu `C:\myfolder` obejmuje hello następujące pliki:

    C:\myfolder\abc.txt
    C:\myfolder\abc1.txt
    C:\myfolder\abc2.txt
    C:\myfolder\vd1\a.txt
    C:\myfolder\vd1\abcd.txt

Jeśli nie zostanie określona opcja `/S`, są pobierane nie obiekty BLOB.

### <a name="download-blobs-with-specified-prefix"></a>Pobieranie obiektów blob z określonego prefiksu

```azcopy
AzCopy /Source:https://myaccount.blob.core.windows.net/mycontainer /Dest:C:\myfolder /SourceKey:key /Pattern:a /S
```

Załóżmy następujące hello obiekty BLOB znajdują się w określonym kontenerze hello. Wszystkie obiekty BLOB rozpoczynający się od prefiksu powitania `a` są pobierane:

    abc.txt
    abc1.txt
    abc2.txt
    xyz.txt
    vd1\a.txt
    vd1\abcd.txt

Po wykonaniu operacji pobierania hello hello folderu `C:\myfolder` obejmuje hello następujące pliki:

    C:\myfolder\abc.txt
    C:\myfolder\abc1.txt
    C:\myfolder\abc2.txt

Prefiks Hello dotyczy katalogu wirtualnego toohello, który stanowi hello pierwsza część hello nazwa obiektu blob. W powyższym przykładzie hello hello katalogu wirtualnego nie pasuje hello określony prefiks, więc nie zostanie pobrana. Ponadto, jeśli hello opcji `\S` nie zostanie określony, narzędzie AzCopy nie pobiera wszystkie obiekty BLOB.

### <a name="set-hello-last-modified-time-of-exported-files-toobe-same-as-hello-source-blobs"></a>Ustawianie czasu ostatniej modyfikacji hello z toobe eksportowanych plików tak samo jak hello źródła obiektów blob

```azcopy
AzCopy /Source:https://myaccount.blob.core.windows.net/mycontainer /Dest:C:\myfolder /SourceKey:key /MT
```

Można również wykluczyć obiekty BLOB z operacji pobierania hello na podstawie ich czasu ostatniej modyfikacji. Na przykład, jeśli chcesz tooexclude obiektów blob, których godzina ostatniej modyfikacji jest hello taką samą lub nowszą niż plik docelowy hello, dodać hello `/XN` opcji:

```azcopy
AzCopy /Source:https://myaccount.blob.core.windows.net/mycontainer /Dest:C:\myfolder /SourceKey:key /MT /XN
```

Lub tooexclude obiektów blob, których godzina ostatniej modyfikacji jest hello tego samego lub starsze niż hello pliku docelowego, należy dodać hello `/XO` opcji:

```azcopy
AzCopy /Source:https://myaccount.blob.core.windows.net/mycontainer /Dest:C:\myfolder /SourceKey:key /MT /XO
```

## <a name="blob-upload"></a>Obiekt blob: Przekaż
### <a name="upload-single-file"></a>Przekaż pojedynczy plik

```azcopy
AzCopy /Source:C:\myfolder /Dest:https://myaccount.blob.core.windows.net/mycontainer /DestKey:key /Pattern:"abc.txt"
```

Jeśli hello docelowy określony kontener nie istnieje, AzCopy tworzy go i przekazywanie hello pliku do niego.

### <a name="upload-single-file-toovirtual-directory"></a>Przekaż pojedynczy plik toovirtual katalogu

```azcopy
AzCopy /Source:C:\myfolder /Dest:https://myaccount.blob.core.windows.net/mycontainer/vd /DestKey:key /Pattern:abc.txt
```

Jeśli hello określony katalog wirtualny nie istnieje, narzędzie AzCopy przekazuje hello pliku tooinclude hello katalogu wirtualnego w swojej nazwy (*np.*, `vd/abc.txt` w powyższym przykładzie hello).

### <a name="upload-all-files"></a>Przekaż wszystkie pliki

```azcopy
AzCopy /Source:C:\myfolder /Dest:https://myaccount.blob.core.windows.net/mycontainer /DestKey:key /S
```

Określenie opcji `/S` przekazywanie zawartości hello hello określony rekursywnie magazynu tooBlob katalogu, co oznacza, jak również przekazać wszystkie podfoldery i pliki. Na przykład załóżmy następujące hello pliki znajdują się w folderze `C:\myfolder`:

    C:\myfolder\abc.txt
    C:\myfolder\abc1.txt
    C:\myfolder\abc2.txt
    C:\myfolder\subfolder\a.txt
    C:\myfolder\subfolder\abcd.txt

Po wykonaniu operacji przekazywania hello hello kontener zawiera hello następujące pliki:

    abc.txt
    abc1.txt
    abc2.txt
    subfolder\a.txt
    subfolder\abcd.txt

Jeśli nie zostanie określona opcja `/S`, AzCopy nie przekazuje rekursywnie. Po wykonaniu operacji przekazywania hello hello kontener zawiera hello następujące pliki:

    abc.txt
    abc1.txt
    abc2.txt

### <a name="upload-files-matching-specified-pattern"></a>Przekazywanie plików zgodnych z określonym wzorcem

```azcopy
AzCopy /Source:C:\myfolder /Dest:https://myaccount.blob.core.windows.net/mycontainer /DestKey:key /Pattern:a* /S
```

Załóżmy następujące hello pliki znajdują się w folderze `C:\myfolder`:

    C:\myfolder\abc.txt
    C:\myfolder\abc1.txt
    C:\myfolder\abc2.txt
    C:\myfolder\xyz.txt
    C:\myfolder\subfolder\a.txt
    C:\myfolder\subfolder\abcd.txt

Po wykonaniu operacji przekazywania hello hello kontener zawiera hello następujące pliki:

    abc.txt
    abc1.txt
    abc2.txt
    subfolder\a.txt
    subfolder\abcd.txt

Jeśli nie zostanie określona opcja `/S`, AzCopy przekazuje tylko obiekty BLOB, które nie znajdują się w katalogu wirtualnym:

    C:\myfolder\abc.txt
    C:\myfolder\abc1.txt
    C:\myfolder\abc2.txt

### <a name="specify-hello-mime-content-type-of-a-destination-blob"></a>Określ typ zawartości MIME hello z docelowego obiektu blob
Domyślnie narzędzie AzCopy ustawia typ zawartości hello docelowego obiektu blob zbyt`application/octet-stream`. Począwszy od wersji 3.1.0, można jawnie określić typ zawartości hello przy użyciu opcji hello `/SetContentType:[content-type]`. Ta składnia ustawia hello typ zawartości dla wszystkich obiektów blob w operacji przekazywania.

```azcopy
AzCopy /Source:C:\myfolder\ /Dest:https://myaccount.blob.core.windows.net/myContainer/ /DestKey:key /Pattern:ab /SetContentType:video/mp4
```

Jeśli określisz `/SetContentType` bez wartości, AzCopy ustawia każdy obiekt blob lub typ zawartości pliku, zgodnie z tooits rozszerzenie pliku.

```azcopy
AzCopy /Source:C:\myfolder\ /Dest:https://myaccount.blob.core.windows.net/myContainer/ /DestKey:key /Pattern:ab /SetContentType
```

## <a name="blob-copy"></a>Obiekt blob: kopiowania
### <a name="copy-single-blob-within-storage-account"></a>Skopiuj pojedynczego obiektu blob w ramach konta magazynu

```azcopy
AzCopy /Source:https://myaccount.blob.core.windows.net/mycontainer1 /Dest:https://myaccount.blob.core.windows.net/mycontainer2 /SourceKey:key /DestKey:key /Pattern:abc.txt
```

Podczas kopiowania obiektu blob w ramach konta magazynu, [po stronie serwera kopii](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx) operacja została wykonana.

### <a name="copy-single-blob-across-storage-accounts"></a>Skopiuj pojedynczego obiektu blob na kontach magazynu

```azcopy
AzCopy /Source:https://sourceaccount.blob.core.windows.net/mycontainer1 /Dest:https://destaccount.blob.core.windows.net/mycontainer2 /SourceKey:key1 /DestKey:key2 /Pattern:abc.txt
```

Podczas kopiowania obiektu blob na kontach magazynu, [po stronie serwera kopii](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx) operacja została wykonana.

### <a name="copy-single-blob-from-secondary-region-tooprimary-region"></a>Skopiuj pojedynczego obiektu blob z regionu pomocniczego tooprimary regionu

```azcopy
AzCopy /Source:https://myaccount1-secondary.blob.core.windows.net/mynewcontainer1 /Dest:https://myaccount2.blob.core.windows.net/mynewcontainer2 /SourceKey:key1 /DestKey:key2 /Pattern:abc.txt
```

Należy pamiętać, że użytkownik musi mieć dostęp do odczytu magazynu geograficznie nadmiarowego włączone.

### <a name="copy-single-blob-and-its-snapshots-across-storage-accounts"></a>Skopiuj pojedynczego obiektu blob i jego migawek wielu kont magazynu

```azcopy
    AzCopy /Source:https://sourceaccount.blob.core.windows.net/mycontainer1 /Dest:https://destaccount.blob.core.windows.net/mycontainer2 /SourceKey:key1 /DestKey:key2 /Pattern:abc.txt /Snapshot
```

Po wykonaniu operacji kopiowania hello kontenera docelowego hello obejmuje hello obiektów blob i jego migawek. Zakładając, że blob hello w powyższym przykładzie hello ma dwa migawki, kontener hello obejmuje następujące hello migawki i obiektów blob:

    abc.txt
    abc (2013-02-25 080757).txt
    abc (2014-02-21 150331).txt

### <a name="synchronously-copy-blobs-across-storage-accounts"></a>Synchronicznie skopiować wielu kont magazynu obiektów blob
Narzędzie AzCopy domyślnie kopiuje dane między dwoma punktami końcowymi magazynu asynchronicznie. W związku z tym hello kopiowania operacji działa w tle hello przy użyciu pojemności nieużywanej przepustowości ma umowy dotyczącej poziomu usług pod względem sposobu szybkiego obiektu blob jest kopiowany i AzCopy okresowo sprawdza stan kopiowania hello dopóki hello Kopiowanie zakończone lub nie powiodło się.

Witaj `/SyncCopy` opcji gwarantuje, że operacji kopiowania hello pobiera spójne szybkości. AzCopy wykonuje synchroniczne kopiowania hello pobierać obiekty BLOB hello toocopy z hello określone źródło toolocal pamięci, a następnie przekazywanie ich miejsce docelowe magazynu obiektów Blob toohello.

```azcopy
AzCopy /Source:https://myaccount1.blob.core.windows.net/myContainer/ /Dest:https://myaccount2.blob.core.windows.net/myContainer/ /SourceKey:key1 /DestKey:key2 /Pattern:ab /SyncCopy
```

`/SyncCopy`może generować wyjście dodatkowych kosztów kopiowania porównaniu tooasynchronous hello zalecane podejście jest toouse tej opcji w maszynie Wirtualnej platformy Azure, który znajduje się w hello tego samego regionu koszt wyjście tooavoid konta magazynu źródłowego.

## <a name="file-download"></a>Plik: Pobierz
### <a name="download-single-file"></a>Pobierz pojedynczy plik

```azcopy
AzCopy /Source:https://myaccount.file.core.windows.net/myfileshare/myfolder1/ /Dest:C:\myfolder /SourceKey:key /Pattern:abc.txt
```

Jeśli hello określone źródło jest udział plików na platformę Azure, a następnie należy określić hello dokładnej nazwy pliku, (*np.* `abc.txt`) toodownload pojedynczy plik, lub określ opcję `/S` toodownload wszystkie pliki w udziale hello rekursywnie. Próba toospecify zarówno wzorzec pliku, jak i opcja `/S` razem powoduje błąd.

### <a name="download-all-files"></a>Pobierz wszystkie pliki

```azcopy
AzCopy /Source:https://myaccount.file.core.windows.net/myfileshare/ /Dest:C:\myfolder /SourceKey:key /S
```

Należy pamiętać, że puste foldery nie zostaną pobrane.

## <a name="file-upload"></a>Plik: Przekaż
### <a name="upload-single-file"></a>Przekaż pojedynczy plik

```azcopy
AzCopy /Source:C:\myfolder /Dest:https://myaccount.file.core.windows.net/myfileshare/ /DestKey:key /Pattern:abc.txt
```

### <a name="upload-all-files"></a>Przekaż wszystkie pliki

```azcopy
AzCopy /Source:C:\myfolder /Dest:https://myaccount.file.core.windows.net/myfileshare/ /DestKey:key /S
```

Należy pamiętać, że wszystkie puste foldery nie zostały przekazane.

### <a name="upload-files-matching-specified-pattern"></a>Przekazywanie plików zgodnych z określonym wzorcem

```azcopy
AzCopy /Source:C:\myfolder /Dest:https://myaccount.file.core.windows.net/myfileshare/ /DestKey:key /Pattern:ab* /S
```

## <a name="file-copy"></a>Plik: kopiowania
### <a name="copy-across-file-shares"></a>Kopiowanie między udziałami plików

```azcopy
AzCopy /Source:https://myaccount1.file.core.windows.net/myfileshare1/ /Dest:https://myaccount2.file.core.windows.net/myfileshare2/ /SourceKey:key1 /DestKey:key2 /S
```
Podczas kopiowania plików między udziałami plików [po stronie serwera kopii](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx) operacja została wykonana.

### <a name="copy-from-file-share-tooblob"></a>Kopiowanie z tooblob udziału plików

```azcopy
AzCopy /Source:https://myaccount1.file.core.windows.net/myfileshare/ /Dest:https://myaccount2.blob.core.windows.net/mycontainer/ /SourceKey:key1 /DestKey:key2 /S
```
Podczas kopiowania pliku z tooblob udziału pliku, [po stronie serwera kopii](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx) operacja została wykonana.


### <a name="copy-from-blob-toofile-share"></a>Kopiowanie z udziału toofile obiektów blob

```azcopy
AzCopy /Source:https://myaccount1.blob.core.windows.net/mycontainer/ /Dest:https://myaccount2.file.core.windows.net/myfileshare/ /SourceKey:key1 /DestKey:key2 /S
```
Podczas kopiowania pliku z udziału toofile obiektów blob, [po stronie serwera kopii](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx) operacja została wykonana.

### <a name="synchronously-copy-files"></a>Synchronicznie kopiować pliki
Można określić hello `/SyncCopy` opcję toocopy danych z magazynu plików tooFile magazynu, z pliku magazynu tooBlob magazynu i z magazynu obiektów Blob tooFile magazynu synchronicznie, AzCopy przez pobieranie hello źródła danych toolocal pamięci i przekaż go ponownie toodestination. Stosuje standardowe wyjście kosztów.

```azcopy
AzCopy /Source:https://myaccount1.file.core.windows.net/myfileshare1/ /Dest:https://myaccount2.file.core.windows.net/myfileshare2/ /SourceKey:key1 /DestKey:key2 /S /SyncCopy
```

Podczas kopiowania z pliku magazynu tooBlob magazynu, typu obiektu blob domyślne hello jest blokowych obiektów blob, użytkownik może określić opcję `/BlobType:page` toochange hello docelowego obiektu blob.

Należy pamiętać, że `/SyncCopy` może generować wyjście dodatkowych kosztów porównaniem kopiowania tooasynchronous, hello Zalecanym podejściem jest toouse maszyny Wirtualnej platformy Azure, który znajduje się w hello hello tej opcji, w tym samym regionie co koszt wyjście tooavoid konta magazynu źródłowego.

## <a name="table-export"></a>Tabela: eksportowanie
### <a name="export-table"></a>Eksportowanie tabeli

```azcopy
AzCopy /Source:https://myaccount.table.core.windows.net/myTable/ /Dest:C:\myfolder\ /SourceKey:key
```

Narzędzie AzCopy zapisuje folder docelowy określony toohello pliku manifestu. Plik manifestu Hello jest używany w hello importu procesu toolocate hello niezbędnych danych plików i sprawdzania poprawności danych. Plik manifestu Hello korzysta z następującą konwencją domyślnie hello:

    <account name>_<table name>_<timestamp>.manifest

Użytkownik może również określić opcję hello `/Manifest:<manifest file name>` nazwa pliku manifestu hello tooset.

```azcopy
AzCopy /Source:https://myaccount.table.core.windows.net/myTable/ /Dest:C:\myfolder\ /SourceKey:key /Manifest:abc.manifest
```

### <a name="split-export-into-multiple-files"></a>Eksport podzielonego na wiele plików

```azcopy
AzCopy /Source:https://myaccount.table.core.windows.net/mytable/ /Dest:C:\myfolder /SourceKey:key /S /SplitSize:100
```

Korzysta z narzędzia AzCopy *indeksu woluminu* w hello podział danych nazwę pliku toodistinguish wielu plików. Indeks woluminu Hello składa się z dwóch części *indeksu zakresem kluczy partycji* i *podziału pliku indeksu*. Zarówno indeksy są liczony od zera.

Indeks zakresem kluczy partycji Hello wynosi 0, jeśli użytkownik hello nie określono opcji `/PKRS`.

Na przykład, załóżmy, że AzCopy generuje dwa pliki danych po hello użytkownika określa opcję `/SplitSize`. Witaj wynikowa nazwy pliku danych może być:

    myaccount_mytable_20140903T051850.8128447Z_0_0_C3040FE8.json
    myaccount_mytable_20140903T051850.8128447Z_0_1_0AB9AC20.json

Należy pamiętać, że hello minimalnej możliwej wartości dla opcji `/SplitSize` wynosi 32 MB. Jeśli hello określone miejsce docelowe jest magazyn obiektów Blob, AzCopy dzieli hello danych pliku po jego rozmiary przez nią miejsce osiągnie limit rozmiaru obiektu blob hello (200GB), niezależnie od tego, czy opcja `/SplitSize` został określony przez użytkownika hello.

### <a name="export-table-toojson-or-csv-data-file-format"></a>Eksportowanie tabeli tooJSON lub dane w formacie pliku CSV
Narzędzie AzCopy domyślnie eksportuje pliki danych tooJSON tabel. Można określić opcję hello `/PayloadFormat:JSON|CSV` tabele hello tooexport jako JSON lub CSV.

```azcopy
AzCopy /Source:https://myaccount.table.core.windows.net/myTable/ /Dest:C:\myfolder\ /SourceKey:key /PayloadFormat:CSV
```

Podczas określania format ładunku hello CSV, AzCopy także generuje plik schematu z rozszerzeniem pliku `.schema.csv` dla każdego pliku danych.

### <a name="export-table-entities-concurrently"></a>Eksportowanie tabeli jednocześnie jednostek

```azcopy
AzCopy /Source:https://myaccount.table.core.windows.net/myTable/ /Dest:C:\myfolder\ /SourceKey:key /PKRS:"aa#bb"
```

AzCopy rozpoczyna się jednostek tooexport jednoczesnych operacji, gdy użytkownik hello Określa opcję `/PKRS`. Każda operacja eksportuje jednym zakresem kluczy partycji.

Należy pamiętać, że hello liczba jednoczesnych operacji również jest kontrolowane przez opcję `/NC`. AzCopy używa hello liczba rdzeni procesorów jako wartość domyślną hello `/NC` podczas kopiowania jednostek tabeli, nawet jeśli `/NC` nie została określona. Gdy użytkownik hello Określa opcję `/PKRS`, AzCopy używa hello mniejszych Witaj dwie wartości - partycji zakresami kluczy i określona jawnie lub niejawnie jednoczesnych operacji - toodetermine hello liczby jednoczesnych operacji toostart. Aby uzyskać więcej informacji, wpisz `AzCopy /?:NC` hello wiersza polecenia.

### <a name="export-table-tooblob"></a>Eksportowanie tabeli tooblob

```azcopy
AzCopy /Source:https://myaccount.table.core.windows.net/myTable/ /Dest:https://myaccount.blob.core.windows.net/mycontainer/ /SourceKey:key1 /Destkey:key2
```

Narzędzie AzCopy generuje plik danych JSON do kontenera obiektów blob hello z następującą konwencją:

    <account name>_<table name>_<timestamp>_<volume index>_<CRC>.json

plik danych JSON Hello wygenerowany w formacie hello ładunku dla minimalne metadane. Aby uzyskać więcej informacji na ten format ładunku, zobacz [Format ładunku dla operacji usługi tabeli](http://msdn.microsoft.com/library/azure/dn535600.aspx).

Należy pamiętać, że podczas eksportowania tooblobs tabel, AzCopy hello tabeli jednostek toolocal tymczasowe pliki danych i następnie pobiera blob toohello tych jednostek. Te dane tymczasowe pliki są umieszczane w folderze dziennika hello o hello domyślnej ścieżki "<code>%LocalAppData%\Microsoft\Azure\AzCopy</code>", można określić opcję/toochange [arkusza pliku folder] Z: hello folder plików dziennika i w związku z tym zmienić lokalizację plików tymczasowych danych hello. Witaj dane tymczasowe, który rozmiaru plików zadecyduje o jednostek tabeli i rozmiar hello, określony /SplitSize opcji hello, chociaż plik danych tymczasowych hello dysku lokalnego jest usuwane natychmiast po został przekazany toohello obiektów blob, upewnij się, że masz za mało lokalnego dysku toostore miejsca te dane tymczasowe pliki przed usunięciem.

## <a name="table-import"></a>Tabela: Import
### <a name="import-table"></a>Importowanie tabeli

```azcopy
AzCopy /Source:C:\myfolder\ /Dest:https://myaccount.table.core.windows.net/mytable1/ /DestKey:key /Manifest:"myaccount_mytable_20140103T112020.manifest" /EntityOperation:InsertOrReplace
```

Witaj opcja `/EntityOperation` wskazuje sposób jednostek tooinsert do hello tabeli. Możliwe wartości:

* `InsertOrSkip`: Pomija istniejącej jednostki lub wstawia nową jednostkę, jeśli nie istnieje w tabeli hello.
* `InsertOrMerge`: Scala istniejącej jednostki lub wstawia nową jednostkę, jeśli nie istnieje w tabeli hello.
* `InsertOrReplace`: Zastępuje istniejące jednostki i wstawia nową jednostkę, jeśli nie istnieje w tabeli hello.

Zauważ, że nie można określić opcji `/PKRS` w scenariuszu importu hello. W odróżnieniu od hello eksportu scenariusz, w którym należy określić opcję `/PKRS` toostart jednoczesnych operacji AzCopy jest uruchamiany jednoczesnych operacji domyślnie podczas importowania tabeli. Hello domyślna liczba jednoczesnych operacji uruchomiona jest równy toohello liczba procesorów; jednak można określić różne liczby równoczesnych z opcją `/NC`. Aby uzyskać więcej informacji, wpisz `AzCopy /?:NC` hello wiersza polecenia.

Należy pamiętać, że narzędzie AzCopy obsługuje wyłącznie importowanie do formatu JSON, CSV nie. AzCopy nie obsługuje importowania tabeli z JSON utworzonych przez użytkownika i pliki manifestu. Oba te pliki muszą pochodzić z narzędzia AzCopy tabeli eksportu. błędy tooavoid nie Modyfikuj hello wyeksportowane JSON lub pliku manifestu.

### <a name="import-entities-tootable-using-blobs"></a>Importowanie jednostek tootable przy użyciu obiektów blob
Założono kontenera obiektów Blob zawiera następujące hello: plik A JSON reprezentujący tabel Azure i jego towarzyszący plik manifestu.

    myaccount_mytable_20140103T112020.manifest
    myaccount_mytable_20140103T112020_0_0_0AF395F1DC42E952.json

Można uruchomić powitania po polecenie tooimport jednostek do tabeli za pomocą pliku manifestu hello w danym kontenerze obiektów blob:

```azcopy
AzCopy /Source:https://myaccount.blob.core.windows.net/mycontainer /Dest:https://myaccount.table.core.windows.net/mytable /SourceKey:key1 /DestKey:key2 /Manifest:"myaccount_mytable_20140103T112020.manifest" /EntityOperation:"InsertOrReplace"
```

## <a name="other-azcopy-features"></a>Inne funkcje AzCopy
### <a name="only-copy-data-that-doesnt-exist-in-hello-destination"></a>Tylko skopiować dane, które nie istnieje w docelowym hello
Witaj `/XO` i `/XN` parametrów pozwalają tooexclude starszej lub nowszej źródła zasobów zapobiega kopiowaniu odpowiednio. Jeśli chcesz tylko toocopy źródła zasobów, które nie istnieje w docelowym hello, można określić obu tych parametrów w hello polecenia programu AzCopy:

    /Source:http://myaccount.blob.core.windows.net/mycontainer /Dest:C:\myfolder /SourceKey:<sourcekey> /S /XO /XN

    /Source:C:\myfolder /Dest:http://myaccount.file.core.windows.net/myfileshare /DestKey:<destkey> /S /XO /XN

    /Source:http://myaccount.blob.core.windows.net/mycontainer /Dest:http://myaccount.blob.core.windows.net/mycontainer1 /SourceKey:<sourcekey> /DestKey:<destkey> /S /XO /XN

Należy pamiętać, że to nie jest obsługiwana podczas hello źródłowe lub docelowe jest tabelą.

### <a name="use-a-response-file-toospecify-command-line-parameters"></a>Użyj parametrów pliku odpowiedzi toospecify wiersza polecenia

```azcopy
AzCopy /@:"C:\responsefiles\copyoperation.txt"
```

Parametry wiersza polecenia AzCopy można umieścić w pliku odpowiedzi. Procesy AzCopy hello parametrów w pliku hello tak, jakby były one określone w wierszu polecenia hello, wykonywanie bezpośrednich podstawienia z zawartością hello hello pliku.

Załóżmy plik odpowiedzi o nazwie `copyoperation.txt`, który zawiera następujące wiersze hello. Każdy parametr narzędzia AzCopy można określić w jednym wierszu

    /Source:http://myaccount.blob.core.windows.net/mycontainer /Dest:C:\myfolder /SourceKey:<sourcekey> /S /Y

lub na oddzielnych wierszach:

    /Source:http://myaccount.blob.core.windows.net/mycontainer
    /Dest:C:\myfolder
    /SourceKey:<sourcekey>
    /S
    /Y

Narzędzie AzCopy wynik negatywny, jeśli parametr hello można podzielić na dwa wiersze, jak pokazano poniżej, aby uzyskać hello `/sourcekey` parametru:

    http://myaccount.blob.core.windows.net/mycontainer
     C:\myfolder
    /sourcekey:
    <sourcekey>
    /S
    /Y

### <a name="use-multiple-response-files-toospecify-command-line-parameters"></a>Użyj wielu odpowiedzi plików toospecify parametry wiersza polecenia
Załóżmy, plik odpowiedzi o nazwie `source.txt` , który określa kontener źródła:

    /Source:http://myaccount.blob.core.windows.net/mycontainer

I plik odpowiedzi o nazwie `dest.txt` określający folderu docelowego w systemie plików hello:

    /Dest:C:\myfolder

I plik odpowiedzi o nazwie `options.txt` , który określa opcje narzędzia AzCopy:

    /S /Y

toocall AzCopy z tych plików odpowiedzi, które znajdują się w katalogu `C:\responsefiles`, użyj tego polecenia:

```azcopy
AzCopy /@:"C:\responsefiles\source.txt" /@:"C:\responsefiles\dest.txt" /SourceKey:<sourcekey> /@:"C:\responsefiles\options.txt"   
```

Narzędzie AzCopy przetwarza to polecenie tak samo, jak gdyby uwzględnione wszystkie parametry poszczególnych hello hello w wierszu polecenia:

```azcopy
AzCopy /Source:http://myaccount.blob.core.windows.net/mycontainer /Dest:C:\myfolder /SourceKey:<sourcekey> /S /Y
```

### <a name="specify-a-shared-access-signature-sas"></a>Określ sygnatury dostępu współdzielonego (SAS)

```azcopy
AzCopy /Source:https://myaccount.blob.core.windows.net/mycontainer1 /Dest:https://myaccount.blob.core.windows.net/mycontainer2 /SourceSAS:SAS1 /DestSAS:SAS2 /Pattern:abc.txt
```

Można również określić sygnatury dostępu Współdzielonego w kontenerze hello identyfikatora URI:

```azcopy
AzCopy /Source:https://myaccount.blob.core.windows.net/mycontainer1/?SourceSASToken /Dest:C:\myfolder /S
```

### <a name="journal-file-folder"></a>Folder plików dziennika
Zawsze, gdy wystawiać tooAzCopy polecenia, sprawdza czy istnieje plik dziennika w folderze domyślnym hello, lub czy istnieje w folderze określonej za pomocą tej opcji. Jeśli plik dziennika hello nie istnieje w każdym miejscu, AzCopy traktuje operacji hello jako nowy i generuje nowy plik dziennika.

Jeśli istnieje plik dziennika hello, AzCopy sprawdza, czy hello wiersza polecenia, które możesz wpisać zgodny hello wiersza polecenia w pliku dziennika hello. Jeśli dwa wiersze polecenia hello są zgodne, AzCopy wznawia hello nieukończone działania. Jeśli nie są zgodne, to zostanie wyświetlony monit o tooeither Zastąp hello dziennika pliku toostart nowej operacji lub toocancel hello bieżącej operacji.

Jeśli chcesz, aby toouse hello domyślna lokalizacja pliku dziennika hello:

```azcopy
AzCopy /Source:C:\myfolder /Dest:https://myaccount.blob.core.windows.net/mycontainer /DestKey:key /Z
```

Jeśli pominięto opcję `/Z`, lub określ opcję `/Z` bez ścieżki folderu hello, jak pokazano powyżej, AzCopy tworzy plik dziennika hello w hello domyślnej lokalizacji, która jest `%SystemDrive%\Users\%username%\AppData\Local\Microsoft\Azure\AzCopy`. Jeśli plik dziennika hello już istnieje, AzCopy wznawia operację hello na podstawie hello pliku dziennika.

Jeśli chcesz, aby toospecify niestandardową lokalizację pliku dziennika hello:

```azcopy
AzCopy /Source:C:\myfolder /Dest:https://myaccount.blob.core.windows.net/mycontainer /DestKey:key /Z:C:\journalfolder\
```

W tym przykładzie tworzy plik dziennika hello, jeśli jeszcze nie istnieje. Jeśli istnieje, narzędzie AzCopy wznawia operacji hello na podstawie hello pliku dziennika.

Jeśli chcesz, aby tooresume operacji AzCopy:

```azcopy
AzCopy /Z:C:\journalfolder\
```

W tym przykładzie wznawia hello ostatniej operacji, które toocomplete zakończyła się niepowodzeniem.

### <a name="generate-a-log-file"></a>Wygenerowanie pliku dziennika

```azcopy
AzCopy /Source:C:\myfolder /Dest:https://myaccount.blob.core.windows.net/mycontainer /DestKey:key /V
```

Jeśli określono opcję `/V` bez podawania pliku dziennika pełne ścieżki toohello, następnie AzCopy tworzy plik dziennika hello w hello domyślnej lokalizacji, która jest `%SystemDrive%\Users\%username%\AppData\Local\Microsoft\Azure\AzCopy`.

W przeciwnym razie należy utworzyć plik dziennika w lokalizacji niestandardowej:

```azcopy
AzCopy /Source:C:\myfolder /Dest:https://myaccount.blob.core.windows.net/mycontainer /DestKey:key /V:C:\myfolder\azcopy1.log
```

Należy pamiętać, że jeśli Określ ścieżkę względną po opcji `/V`, takich jak `/V:test/azcopy1.log`, a następnie hello pełnego dziennika jest tworzony w bieżącym katalogu roboczym hello w podfolderze o nazwie `test`.

### <a name="specify-hello-number-of-concurrent-operations-toostart"></a>Określ liczbę hello toostart jednoczesnych operacji
Opcja `/NC` określa liczbę hello operacje kopiowania współbieżnych. Domyślnie narzędzie AzCopy uruchamia określoną liczbę jednoczesnych operacji tooincrease hello danych przeniesienie przepływności. Dla operacji tabeli hello liczba jednoczesnych operacji jest równy toohello liczbę procesorów, które masz. Dla operacji obiektu Blob i plik hello liczba jednoczesnych operacji jest równa 8 godzin hello liczbę procesorów, które masz. Jeśli używasz narzędzia AzCopy w niskiej przepustowości sieci, można określić mniejszą liczbę /NC tooavoid niepowodzenia spowodowane konkurencji zasobów.

### <a name="run-azcopy-against-azure-storage-emulator"></a>Uruchom narzędzie AzCopy dla emulatora magazynu Azure
Możesz uruchamiać narzędzia AzCopy na powitania [emulatora magazynu Azure](storage-use-emulator.md) dla obiektów blob:

```azcopy
AzCopy /Source:https://127.0.0.1:10000/myaccount/mycontainer/ /Dest:C:\myfolder /SourceKey:key /SourceType:Blob /S
```

i tabele:

```azcopy
AzCopy /Source:https://127.0.0.1:10002/myaccount/mytable/ /Dest:C:\myfolder /SourceKey:key /SourceType:Table
```

## <a name="azcopy-parameters"></a>Parametry AzCopy
Poniżej opisano parametry narzędzia AzCopy. Możesz także wpisać jedną z poniższych poleceń z wiersza polecenia hello, aby uzyskać pomoc przy użyciu narzędzia AzCopy hello:

* Aby uzyskać szczegółową pomoc wiersza polecenia AzCopy:`AzCopy /?`
* Szczegółowe informacje o żadnych parametrów narzędzia AzCopy:`AzCopy /?:SourceKey`
* Przykłady wiersza polecenia:`AzCopy /?:Samples`

### <a name="sourcesource"></a>/ Źródła: "source"
Określa hello źródła danych z którego toocopy. Źródło Hello może być katalogu w systemie plików, kontenera obiektów blob, katalog wirtualny obiektów blob, udział pliku magazynu, katalog pliku magazynu lub tabeli platformy Azure.

**Dotyczy:** obiektów blob, plików, tabel

### <a name="destdestination"></a>/ Dest: "miejsce docelowe"
Określa hello toocopy docelowego do. Hello docelowym może być katalogu w systemie plików, kontenera obiektów blob, katalog wirtualny obiektów blob, udział pliku magazynu, katalog pliku magazynu lub tabeli platformy Azure.

**Dotyczy:** obiektów blob, plików, tabel

### <a name="patternfile-pattern"></a>/ Wzorca: "wzorzec pliku"
Określa wzorzec pliku, która wskazuje, które toocopy pliki. zachowanie Hello hello /Pattern parametru zależy od lokalizacji hello hello źródła danych i hello obecność cyklicznego hello w trybie. Za pomocą opcji opcji/s. jest określony tryb cykliczne

Jeśli określone źródło hello jest katalogu w systemie plików hello, obowiązują standardowe symbole wieloznaczne i podać wzorzec pliku hello jest dopasowywana do plików w katalogu hello. Jeśli opcja określeniu, następnie AzCopy również wzorcem hello określony względem wszystkich plików w wszystkie podfoldery znajdujące się poniżej katalogu hello.

W przypadku określonego źródła hello kontenera obiektów blob lub katalogu wirtualnego, symbole wieloznaczne nie są stosowane. Jeśli opcja/s jest określana, następnie AzCopy interpretuje hello określonego pliku wzorca jako prefiks obiektu blob. Jeśli opcja /S nie zostanie określony, następnie AzCopy wzorcem hello pliku nazwami dokładne obiektu blob.

Jeśli hello określone źródło jest udział plików na platformę Azure, a następnie należy określić nazwę pliku dokładne hello (np. abc.txt) toocopy pojedynczy plik, lub określ opcję /S toocopy wszystkie pliki w hello rekursywnie udziału. Próba toospecify zarówno pliku wzorca i opcja /S razem powoduje błąd.

AzCopy korzysta z uwzględnieniem wielkości liter dopasowania, gdy hello/Source jest kontenera obiektów blob lub katalogu wirtualnego obiektów blob i używa bez uwzględniania wielkości liter dopasowanie wszystkich hello innych przypadkach.

Witaj wzorzec pliku domyślne używane, jeśli nie określono żadnych wzorzec pliku jest *.* dla lokalizacji systemu plików lub pustego prefiksu lokalizacji magazynu Azure. Nie można określać wielu wzorców pliku.

**Dotyczy:** obiektów blob, pliki

### <a name="destkeystorage-key"></a>/ DestKey: "klucz magazynu"
Określa klucz konta magazynu hello hello zasobu docelowego.

**Dotyczy:** obiektów blob, plików, tabel

### <a name="destsassas-token"></a>/ DestSAS: "tokenu sygnatury dostępu współdzielonego"
Określa dostępu sygnatury dostępu Współdzielonego z uprawnieniami odczytu i zapisu dla miejsca docelowego hello (jeśli dotyczy). Ująć hello SAS z cudzysłowami podwójnymi, jak mogą zawiera znaki specjalne wiersza polecenia.

W przypadku zasobu docelowego hello kontenera obiektów blob, udziału plików lub tabeli, można określić tej opcji, a po niej tokenu sygnatury dostępu Współdzielonego hello lub jako część hello docelowy kontener obiektów blob, udziału plików lub identyfikator URI tabeli, jeśli ta opcja nie można określić hello SAS.

Jeśli hello źródłowy i docelowy są oba obiekty BLOB, a następnie hello docelowego obiektu blob musi znajdować się w obrębie hello same konta magazynu jako hello źródłowego obiektu blob.

**Dotyczy:** obiektów blob, plików, tabel

### <a name="sourcekeystorage-key"></a>/ SourceKey: "klucz magazynu"
Określa klucz konta magazynu hello hello źródła zasobu.

**Dotyczy:** obiektów blob, plików, tabel

### <a name="sourcesassas-token"></a>/ SourceSAS: "tokenu sygnatury dostępu współdzielonego"
Określa sygnaturę dostępu współdzielonego z uprawnieniami odczytu i listy hello źródła (jeśli dotyczy). Ująć hello SAS z cudzysłowami podwójnymi, jak mogą zawiera znaki specjalne wiersza polecenia.

Jeśli zasób źródła hello jest kontenera obiektów blob, a podano klucz ani sygnatury dostępu Współdzielonego, hello kontenera obiektów blob jest odczytu za pośrednictwem dostęp anonimowy.

Jeśli źródło hello jest udział plików lub tabeli, należy podać klucz lub sygnatury dostępu Współdzielonego.

**Dotyczy:** obiektów blob, plików, tabel

### <a name="s"></a>/ S
Określa tryb cyklicznych operacji kopiowania. W trybie cykliczne AzCopy kopiuje wszystkie obiekty BLOB lub pliki, które jest zgodny z wzorcem określonego pliku hello, włącznie z zawartymi w podfolderach.

**Dotyczy:** obiektów blob, pliki

### <a name="blobtypeblock--page--append"></a>/ BlobType: "block" | "page" | "Dołącz"
Określa, czy hello docelowego obiektu blob jest blokowych obiektów blob i stronicowych obiektów blob, uzupełnialny obiekt blob. Ta opcja ma zastosowanie tylko wtedy, gdy przekazujesz obiektu blob. W przeciwnym razie zostanie wygenerowany błąd. Jeśli docelowy hello jest obiektem blob, a ta opcja nie jest określona, domyślnie AzCopy tworzy blokowych obiektów blob.

**Dotyczy:** obiektów blob

### <a name="checkmd5"></a>/ CheckMD5
Oblicza Skrót MD5 pobrane dane i weryfikuje, czy skrót MD5 hello przechowywane w obiekcie blob hello lub właściwość Content-MD5 pliku odpowiada hello obliczana wyznaczania wartości skrótu. Hello MD5 wyboru jest domyślnie wyłączona, należy określić opcję tooperform hello MD5 sprawdzanie podczas pobierania danych.

Należy pamiętać, że usługi Azure Storage nie gwarantuje tego hello wyznaczania wartości skrótu MD5 przechowywanych dla obiekt blob hello, lub plik jest aktualny. Klienta odpowiedzialność tooupdate hello MD5 jest zawsze, gdy obiekt blob hello lub plik jest modyfikowany.

Narzędzie AzCopy zawsze ustawia właściwość Content-MD5 hello obiektów blob platformy Azure lub plik po przekazać go toohello usługi.  

**Dotyczy:** obiektów blob, pliki

### <a name="snapshot"></a>/ Migawki
Wskazuje, czy tootransfer migawki. Ta opcja jest prawidłowy tylko w przypadku, gdy źródło hello jest obiektu blob.

Witaj migawki obiektu blob przekazanych zostały zmienione w następującym formacie: .extension nazwy obiektów blob (migawka time)

Domyślnie nie są kopiowane migawki.

**Dotyczy:** obiektów blob

### <a name="vverbose-log-file"></a>/ V: [plików pełnego dziennika]
Komunikaty stanu pełne dane wyjściowe do pliku dziennika.

Domyślnie program hello pełny plik dziennika ma nazwę AzCopyVerbose.log w `%LocalAppData%\Microsoft\Azure\AzCopy`. Jeśli określisz istniejącej lokalizacji plików dla tej opcji, hello pełnego dziennika jest dołączany toothat pliku.  

**Dotyczy:** obiektów blob, plików, tabel

### <a name="zjournal-file-folder"></a>/ Z: [arkusza pliku folder]
Określa folder plików dziennika dla wznawia działanie.

Narzędzie AzCopy zawsze obsługuje wznawianie, jeśli operacja została przerwana.

Jeśli ta opcja nie jest określony lub został określony bez ścieżki folderu, następnie AzCopy tworzy plik dziennika hello w domyślnej lokalizacji hello, czyli % LocalAppData%\Microsoft\Azure\AzCopy.

Zawsze, gdy wystawiać tooAzCopy polecenia, sprawdza czy istnieje plik dziennika w folderze domyślnym hello, lub czy istnieje w folderze określonej za pomocą tej opcji. Jeśli plik dziennika hello nie istnieje w każdym miejscu, AzCopy traktuje operacji hello jako nowy i generuje nowy plik dziennika.

Jeśli istnieje plik dziennika hello, AzCopy sprawdza, czy hello wiersza polecenia, które możesz wpisać zgodny hello wiersza polecenia w pliku dziennika hello. Jeśli dwa wiersze polecenia hello są zgodne, AzCopy wznawia hello nieukończone działania. Jeśli nie są zgodne, to zostanie wyświetlony monit o tooeither Zastąp hello dziennika pliku toostart nowej operacji lub toocancel hello bieżącej operacji.

plik dziennika Hello jest usuwany po pomyślnym zakończeniu operacji hello.

Należy pamiętać, że wznawia działanie z pliku dziennika utworzonego przez poprzednią wersję programu AzCopy nie jest obsługiwany.

**Dotyczy:** obiektów blob, plików, tabel

### <a name="parameter-file"></a>/@:"parameter-File"
Określa plik, który zawiera parametry. Procesy AzCopy hello parametrów w pliku hello, tak jakby były one określone w wierszu polecenia hello.

W pliku odpowiedzi można określić wiele parametrów w jednym wierszu lub określ każdego parametru w osobnym wierszu. Należy pamiętać, że poszczególne parametru nie może obejmować wiele wierszy.

Pliki odpowiedzi może zawierać wiersze z symbolem # hello komentarze.

Można określić wiele plików odpowiedzi. Jednak należy pamiętać, że narzędzie AzCopy nie obsługuje zagnieżdżone pliki odpowiedzi.

**Dotyczy:** obiektów blob, plików, tabel

### <a name="y"></a>/ Y
Pomija wszystkie monity potwierdzenie narzędzia AzCopy.

**Dotyczy:** obiektów blob, plików, tabel

### <a name="l"></a>/L
Określa listę operację. dane nie zostaną skopiowane.

AzCopy interpretuje hello przy użyciu programu tę opcję symulacji dla uruchomionego hello wiersza polecenia bez stosowania tej opcji /L i liczby obiektów ile zostaną skopiowane, możesz określić opcję /V na powitania sam czas toocheck obiekty, które są kopiowane w hello pełnego dziennika.

zachowanie Hello tej opcji również jest określana przez hello lokalizacji hello źródła danych i hello obecności hello cykliczne opcji/s i pliku wzorca w trybie /Pattern.

Narzędzie AzCopy musi mieć uprawnienie listy i odczytu tej lokalizacji źródła przy użyciu tej opcji.

**Dotyczy:** obiektów blob, pliki

### <a name="mt"></a>/ MT
Ustawia czas ostatniej modyfikacji hello pobrany plik toobe hello takie same jak hello źródłowego obiektu blob lub pliku.

**Dotyczy:** obiektów blob, pliki

### <a name="xn"></a>/XN
Wyklucza nowszej zasobów źródła. Hello zasobu nie jest kopiowana, jeśli hello godzina ostatniej modyfikacji źródła hello jest hello taką samą lub nowszą niż docelowy.

**Dotyczy:** obiektów blob, pliki

### <a name="xo"></a>/XO
Wyklucza starszych zasobów źródła. Hello zasobu nie jest kopiowana, jeśli hello godzina ostatniej modyfikacji źródła hello jest hello tego samego lub starsze niż docelowy.

**Dotyczy:** obiektów blob, pliki

### <a name="a"></a>/A
Wysyła tylko pliki, które mają ustawiony atrybut archiwum hello.

**Dotyczy:** obiektów blob, pliki

### <a name="iarashcnetoi"></a>/ IA: [RASHCNETOI]
Przekazywanie tylko pliki, które nie ma żadnej z hello określony zestaw atrybutów.

Dostępne atrybuty obejmują:

* R = plików tylko do odczytu
* = Plik gotowy do archiwizacji
* S = System plików
* H = ukryte pliki
* C = pliki skompresowane
* N = normalne pliki
* E = zaszyfrowane pliki
* T = pliki tymczasowe
* O = plików trybu Offline
* I = indeksowane inne niż pliki

**Dotyczy:** obiektów blob, pliki

### <a name="xarashcnetoi"></a>/ XA: [RASHCNETOI]
Wyklucza pliki, które nie ma żadnej z hello określony zestaw atrybutów.

Dostępne atrybuty obejmują:

* R = plików tylko do odczytu
* = Plik gotowy do archiwizacji
* S = System plików
* H = ukryte pliki
* C = pliki skompresowane
* N = normalne pliki
* E = zaszyfrowane pliki
* T = pliki tymczasowe
* O = plików trybu Offline
* I = indeksowane inne niż pliki

**Dotyczy:** obiektów blob, pliki

### <a name="delimiterdelimiter"></a>/ Ogranicznik: "ogranicznika"
Wskazuje, że znak ogranicznika hello używane toodelimit katalogów wirtualnych w nazwie obiektu blob.

Domyślnie używa narzędzia AzCopy / jako znak ogranicznika hello. AzCopy obsługuje jednak przy użyciu znaków wspólnych (takich jak @, # lub %) jako ogranicznik. Należy tooinclude jedną z tych znaków specjalnych w wierszu polecenia hello należy ująć hello nazwę pliku z cudzysłowami podwójnymi.

Ta opcja ma zastosowanie tylko do pobrania obiektów blob.

**Dotyczy:** obiektów blob

### <a name="ncnumber-of-concurrent-operations"></a>/ NC: "numer--równoczesnych operacji"
Określa hello liczbę jednoczesnych operacji.

Narzędzie AzCopy domyślnie uruchamia określoną liczbę jednoczesnych operacji tooincrease hello danych przeniesienie przepływności. Należy pamiętać, że dużą liczbą jednoczesnych operacji w środowisku niskiej przepustowości może przeciąży hello połączenie sieciowe i zapobiec operacji hello pełni ukończenie. Ograniczenie przepustowości jednoczesnych operacji oparte na rzeczywiste dostępnej przepustowości sieci.

Hello górny limit liczby jednoczesnych operacji wynosi 512.

**Dotyczy:** obiektów blob, plików, tabel

### <a name="sourcetypeblob--table"></a>/ Źródłowa: "Blob" | "Tabela"
Określa, że hello `source` zasób jest dostępny w środowisku projektowym lokalne powitania, uruchamianie w emulatorze magazynu hello obiektu blob.

**Dotyczy:** obiektów blob, tabel

### <a name="desttypeblob--table"></a>/ DestType: "Blob" | "Tabela"
Określa, że hello `destination` zasób jest dostępny w środowisku projektowym lokalne powitania, uruchamianie w emulatorze magazynu hello obiektu blob.

**Dotyczy:** obiektów blob, tabel

### <a name="pkrskey1key2key3"></a>/ PKRS: "key1 klucz&#2; klucz&#3;..."
Podziały hello tooenable zakresem kluczy partycji eksportowania danych z tabeli równolegle, co spowoduje zwiększenie szybkości hello hello operacji eksportowania.

Jeśli ta opcja nie jest określona, narzędzie AzCopy używa jednostek tabeli tooexport jednego wątku. Na przykład, jeśli hello użytkownika określa /PKRS: "aa #bb", a następnie AzCopy uruchamia trzy jednoczesnych operacji.

Każda operacja eksportuje jednego z trzech zakresów klucza partycji, jak pokazano poniżej:

  [pierwszej partycji klucza, aa)

  [aa, bb)

  [bb, ostatnie partycji klucza]

**Dotyczy:** tabel

### <a name="splitsizefile-size"></a>/ SplitSize: "rozmiar pliku"
Określa hello wyeksportowany plik podzielić rozmiar w MB, hello minimalnego dozwolona wartość to 32.

Jeśli ta opcja nie jest określona, narzędzie AzCopy pojedynczy plik eksportuje tooa danych tabeli.

Jeśli dane tabeli hello jest tooa wyeksportowany obiekt blob, a hello wyeksportowany plik rozmiar osiągnie limit 200 GB hello rozmiar obiektu blob, następnie AzCopy dzieli hello wyeksportowany plik, nawet wtedy, gdy ta opcja nie jest określona.

**Dotyczy:** tabel

### <a name="entityoperationinsertorskip--insertormerge--insertorreplace"></a>/ EntityOperation: "InsertOrSkip" | "InsertOrMerge" | "InsertOrReplace"
Określa zachowanie importu danych hello w tabeli.

* InsertOrSkip - pomija istniejącej jednostki lub wstawia nową jednostkę, jeśli nie istnieje w tabeli hello.
* InsertOrMerge - scala istniejącej jednostki lub wstawia nową jednostkę, jeśli nie istnieje w tabeli hello.
* InsertOrReplace - zastępuje istniejącej jednostki lub wstawia nową jednostkę, jeśli nie istnieje w tabeli hello.

**Dotyczy:** tabel

### <a name="manifestmanifest-file"></a>/ Manifest: "w pliku manifestu"
Określa plik manifestu hello tabeli hello eksportować i importować operacji.

Ta opcja jest opcjonalny podczas operacji eksportowania hello, AzCopy generuje plik manifestu z wstępnie zdefiniowanej nazwy, jeśli ta opcja nie jest określona.

Ta opcja jest wymagana podczas operacji importowania hello do lokalizowania hello pliki danych.

**Dotyczy:** tabel

### <a name="synccopy"></a>/ SyncCopy
Wskazuje, czy toosynchronously kopiowania obiektów blob lub plików między dwoma punktami końcowymi usługi Azure Storage.

Narzędzie AzCopy domyślnie używa kopii asynchronicznych po stronie serwera. Określ to opcja tooperform synchronicznego skopiować, który pobiera obiektów blob lub pliki toolocal pamięci i przekazuje je po tooAzure magazynu.

Tej opcji można użyć podczas kopiowania plików w magazynie obiektów Blob, Magazyn plików, lub z obiektu Blob magazynu tooFile magazynu lub na odwrót.

**Dotyczy:** obiektów blob, pliki

### <a name="setcontenttypecontent-type"></a>/ SetContentType: "content-type"
Określa typ zawartości MIME hello obiekty BLOB docelowego lub plików.

Zestawy AzCopy hello typ zawartości dla obiekt blob lub pliku domyślnie tooapplication/octet-stream. Jawne określenie wartości dla tej opcji można ustawić hello typ zawartości dla wszystkich obiektów blob lub plików.

Jeśli zostanie określona opcja bez wartości, AzCopy ustawia każdy obiekt blob lub typ zawartości pliku, zgodnie z tooits rozszerzenie pliku.

**Dotyczy:** obiektów blob, pliki

### <a name="payloadformatjson--csv"></a>/ PayloadFormat: "JSON" | "CSV"
Określa format hello hello tabeli wyeksportowany plik danych.

Jeśli ta opcja nie jest określona, domyślnie AzCopy eksportuje plik danych tabeli w formacie JSON.

**Dotyczy:** tabel

## <a name="known-issues-and-best-practices"></a>Znane problemy i najlepsze rozwiązania
### <a name="limit-concurrent-writes-while-copying-data"></a>Limit równoczesnych zapisów podczas kopiowania danych
Podczas kopiowania obiektów blob lub pliki z narzędzia AzCopy, należy pamiętać, że inna aplikacja może być modyfikowanie hello danych podczas kopiowania go. Jeśli to możliwe upewnij się, że hello dane, które są kopiowane nie jest modyfikowana podczas operacji kopiowania hello. Na przykład podczas kopiowania wirtualnego dysku twardego skojarzonego z maszyny wirtualnej platformy Azure, upewnij się, że żadne inne aplikacje nie są obecnie zapisywania toohello wirtualnego dysku twardego. Toodo dobrze to jest dzierżawa toobe zasobów hello skopiowane. Alternatywnie można najpierw Utwórz migawkę hello wirtualnego dysku twardego, a następnie skopiuj hello migawki.

Jeśli nie można zapobiec innych aplikacji z zapisywania tooblobs lub plików podczas kopiowane są następnie pamiętać przez zadanie hello czasu hello zakończy, hello kopiowanych zasobów mogą już pełnej zgodności z hello źródła zasobów.

### <a name="run-one-azcopy-instance-on-one-machine"></a>Uruchom jedno wystąpienie AzCopy na jednej maszynie.
Narzędzie AzCopy jest zaprojektowana toomaximize hello wykorzystania transferu danych hello tooaccelerate zasobów maszyny, zaleca się uruchomić tylko jedno wystąpienie AzCopy na jednej maszynie i określ opcję hello `/NC` Jeśli potrzebujesz więcej jednoczesnych operacji. Aby uzyskać więcej informacji, wpisz `AzCopy /?:NC` hello wiersza polecenia.

### <a name="enable-fips-compliant-md5-algorithms-for-azcopy-when-you-use-fips-compliant-algorithms-for-encryption-hashing-and-signing"></a>Włącz algorytmów MD5 FIPS dla narzędzia AzCopy podczas możesz "Użyj FIPS algorytmów szyfrowania, tworzenia skrótu i podpisywania".
AzCopy domyślnie używa .NET MD5 implementacji toocalculate hello MD5 podczas kopiowania obiektów, ale niektóre narzędzia AzCopy tooenable FIPS zgodne MD5 ustawienie wymagań zabezpieczeń.

Można utworzyć pliku app.config `AzCopy.exe.config` z właściwością `AzureStorageUseV1MD5` i umieszcza je Zarezerwuj z AzCopy.exe.

    <?xml version="1.0" encoding="utf-8" ?>
    <configuration>
      <appSettings>
        <add key="AzureStorageUseV1MD5" value="false"/>
      </appSettings>
    </configuration>

Dla właściwości "AzureStorageUseV1MD5" • hello wartość domyślną, AzCopy używa True - .NET MD5 implementacji.
• False — AzCopy używa algorytmu MD5 zgodnego ze standardem FIPS.

Należy pamiętać, że zgodnych algorytmów FIPS jest domyślnie wyłączony na komputerze z systemem Windows można wpisać secpol.msc w oknie Uruchamianie i sprawdzić tego przełącznika na ustawienia zabezpieczeń -> Zabezpieczenia -> Zasady lokalne Opcje -> Kryptografia systemu: Użyj zgodnych algorytmów FIPS dla celów szyfrowania, mieszania i podpisywania.

## <a name="next-steps"></a>Następne kroki
Aby uzyskać więcej informacji na temat usługi Azure Storage i AzCopy zobacz następujące zasoby hello:

### <a name="azure-storage-documentation"></a>Dokumentacja magazynu Azure:
* [Wprowadzenie tooAzure magazynu](../storage-introduction.md)
* [Jak toouse magazynu obiektów Blob w .NET](../blobs/storage-dotnet-how-to-use-blobs.md)
* [Jak toouse magazynu plików w .NET](../storage-dotnet-how-to-use-files.md)
* [Jak toouse magazynu tabel w .NET](../../cosmos-db/table-storage-how-to-use-dotnet.md)
* [Jak toocreate, zarządzania i usuwania konta magazynu](../storage-create-storage-account.md)
* [Transfer danych za pomocą narzędzia AzCopy w systemie Linux](storage-use-azcopy-linux.md)

### <a name="azure-storage-blog-posts"></a>Wpisy blogu magazynu Azure:
* [Wprowadzenie Podgląd Biblioteka przepływu danych usługi Azure Storage](https://azure.microsoft.com/blog/introducing-azure-storage-data-movement-library-preview-2/)
* [AzCopy: Wprowadzenie do kopiowania synchroniczne i dostosowane typ zawartości](http://blogs.msdn.com/b/windowsazurestorage/archive/2015/01/13/azcopy-introducing-synchronous-copy-and-customized-content-type.aspx)
* [Narzędzie AzCopy: Announcing ogólne dostępności 3.0 AzCopy oraz wersji zapoznawczej AzCopy 4.0 z tabeli i plik pomocy technicznej](http://blogs.msdn.com/b/windowsazurestorage/archive/2014/10/29/azcopy-announcing-general-availability-of-azcopy-3-0-plus-preview-release-of-azcopy-4-0-with-table-and-file-support.aspx)
* [Narzędzie AzCopy: Zoptymalizowana pod kątem scenariuszy kopii na dużą skalę](http://go.microsoft.com/fwlink/?LinkId=507682)
* [AzCopy: Obsługa dostęp do odczytu magazynu geograficznie nadmiarowego](http://blogs.msdn.com/b/windowsazurestorage/archive/2014/04/07/azcopy-support-for-read-access-geo-redundant-account.aspx)
* [Narzędzie AzCopy: Transfer danych za pomocą jej ponownie uruchomić tryb i tokenu sygnatury dostępu Współdzielonego](http://blogs.msdn.com/b/windowsazurestorage/archive/2013/09/07/azcopy-transfer-data-with-re-startable-mode-and-sas-token.aspx)
* [Narzędzia AzCopy: Blob kopiowania między konta przy użyciu](http://blogs.msdn.com/b/windowsazurestorage/archive/2013/04/01/azcopy-using-cross-account-copy-blob.aspx)
* [Narzędzie AzCopy: Przekazywanie pobieranie plików dla obiektów blob Azure](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/12/03/azcopy-uploading-downloading-files-for-windows-azure-blobs.aspx)

