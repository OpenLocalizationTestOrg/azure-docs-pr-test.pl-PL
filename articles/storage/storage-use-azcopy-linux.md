---
title: "aaaCopy lub przenoszenia danych tooAzure magazynu z narzędzia AzCopy w systemie Linux | Dokumentacja firmy Microsoft"
description: "Witaj AzCopy w systemie Linux narzędzie toomove lub kopiowania danych tooor z obiektu blob i zawartości pliku. Kopiowanie danych tooAzure magazynu z lokalnych plików, lub danych w ramach urządzeń magazynujących lub między kontami magazynu. Łatwo przeprowadzić migrację z tooAzure danych magazynu."
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
ms.date: 05/11/2017
ms.author: seguler
ms.openlocfilehash: dccb03c9e8cc3ea661494e7834f307b0e3e30cb9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="transfer-data-with-azcopy-on-linux"></a>Transfer danych za pomocą narzędzia AzCopy w systemie Linux
AzCopy w systemie Linux to narzędzie wiersza polecenia przeznaczone do kopiowania tooand danych z magazynu obiektów Blob Microsoft Azure i plików przy użyciu prostych poleceń z optymalną wydajnością. Możesz skopiować dane z jednego obiektu tooanother w ramach konta magazynu lub między kontami magazynu.

Istnieją dwie wersje programu AzCopy, który można pobrać. W systemie Linux azcopy jest z platformy .NET Core Framework, który jest przeznaczony dla platformy Linux oferty styl POSIX opcje wiersza polecenia. [Narzędzie AzCopy w systemie Windows](storage-use-azcopy.md) jest oparty na platformie .NET Framework i oferuje opcje wiersza polecenia Styl systemu Windows. W tym artykule omówiono AzCopy w systemie Linux.

## <a name="download-and-install-azcopy"></a>Pobierz i zainstaluj narzędzie AzCopy
### <a name="installation-on-linux"></a>Instalacja w systemie Linux

Narzędzie AzCopy w systemie Linux wymaga platformy .NET Core framework na platformie hello. Zobacz instrukcje dotyczące instalacji hello na powitania [.NET Core](https://www.microsoft.com/net/core#linuxubuntu) strony.

Na przykład załóżmy Zainstaluj oprogramowanie .NET Core na Ubuntu 16.10. Hello najnowsze Przewodnik instalacji, odwiedź stronę [.NET Core w systemie Linux](https://www.microsoft.com/net/core#linuxubuntu) strona instalacji.


```bash
sudo sh -c 'echo "deb [arch=amd64] https://apt-mo.trafficmanager.net/repos/dotnet-release/ yakkety main" > /etc/apt/sources.list.d/dotnetdev.list' 
sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys 417A0893
sudo apt-get update
sudo apt-get install dotnet-dev-1.0.3
```

Po zainstalowaniu platformy .NET Core, Pobierz i zainstaluj narzędzia AzCopy.

```bash
wget -O azcopy.tar.gz https://aka.ms/downloadazcopyprlinux
tar -xf azcopy.tar.gz
sudo ./install.sh
```

Po zainstalowaniu narzędzia AzCopy w systemie Linux, możesz usunąć pliki hello wyodrębnione. Alternatywnie, jeśli nie masz uprawnień administratora, można również uruchomić AzCopy za pomocą skryptu powłoki hello "azcopy" hello wyodrębnionego folderu. 

### <a name="alternative-installation-on-ubuntu"></a>Alternatywne instalacji na Ubuntu

**Ubuntu 14.04**

Dodawanie źródła stanie dla platformy .net Core:

```bash
sudo sh -c 'echo "deb [arch=amd64] https://apt-mo.trafficmanager.net/repos/dotnet-release/ trusty main" > /etc/apt/sources.list.d/dotnetdev.list' 
sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys 417A0893
```

Dodaj stanie źródło repozytorium produktu Linux firmy Microsoft i zainstalować narzędzia AzCopy:

```bash
curl https://packages.microsoft.com/config/ubuntu/14.04/prod.list > ./microsoft-prod.list
sudo cp ./microsoft-prod.list /etc/apt/sources.list.d/
curl https://packages.microsoft.com/keys/microsoft.asc | gpg --dearmor > microsoft.gpg
sudo cp ./microsoft.gpg /etc/apt/trusted.gpg.d/
```

```bash
sudo apt-get update
sudo apt-get install azcopy
```

**Ubuntu 16.04**

Dodawanie źródła stanie dla platformy .net Core:

```bash
sudo sh -c 'echo "deb [arch=amd64] https://apt-mo.trafficmanager.net/repos/dotnet-release/ xenial main" > /etc/apt/sources.list.d/dotnetdev.list' 
sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys 417A0893
```

Dodaj stanie źródło repozytorium produktu Linux firmy Microsoft i zainstalować narzędzia AzCopy:

```bash
curl https://packages.microsoft.com/config/ubuntu/16.04/prod.list > ./microsoft-prod.list
sudo cp ./microsoft-prod.list /etc/apt/sources.list.d/
curl https://packages.microsoft.com/keys/microsoft.asc | gpg --dearmor > microsoft.gpg
sudo cp ./microsoft.gpg /etc/apt/trusted.gpg.d/
```

```bash
sudo apt-get update
sudo apt-get install azcopy
```

**Ubuntu 16.10**

Dodawanie źródła stanie dla platformy .net Core:

```bash
sudo sh -c 'echo "deb [arch=amd64] https://apt-mo.trafficmanager.net/repos/dotnet-release/ yakkety main" > /etc/apt/sources.list.d/dotnetdev.list' 
sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys 417A0893
```

Dodaj stanie źródło repozytorium produktu Linux firmy Microsoft i zainstalować narzędzia AzCopy:

```bash
curl https://packages.microsoft.com/config/ubuntu/16.10/prod.list > ./microsoft-prod.list
sudo cp ./microsoft-prod.list /etc/apt/sources.list.d/
curl https://packages.microsoft.com/keys/microsoft.asc | gpg --dearmor > microsoft.gpg
sudo cp ./microsoft.gpg /etc/apt/trusted.gpg.d/
```

```bash
sudo apt-get update
sudo apt-get install azcopy
```

## <a name="writing-your-first-azcopy-command"></a>Pisanie pierwszego polecenia AzCopy
Podstawowa składnia polecenia AzCopy Hello jest:

```azcopy
azcopy --source <source> --destination <destination> [Options]
```

Witaj następujące przykłady pokazują różne scenariusze kopiowania tooand danych z programu Microsoft Azure blob i plików. Zobacz toohello `azcopy --help` menu, aby uzyskać szczegółowy opis hello parametrami używanymi w każdej próbki.

## <a name="blob-download"></a>Obiekt blob: Pobierz
### <a name="download-single-blob"></a>Pobieranie pojedynczego obiektu blob

```azcopy
azcopy \
    --source https://myaccount.blob.core.windows.net/mycontainer \
    --destination /mnt/myfiles \
    --source-key <key> \
    --include "abc.txt"
```

Jeśli hello folder `/mnt/myfiles` nie istnieje, narzędzie AzCopy tworzy go i pobiera `abc.txt ` do nowego folderu hello.

### <a name="download-single-blob-from-secondary-region"></a>Pobieranie pojedynczego obiektu blob z regionu pomocniczego

```azcopy
azcopy \
    --source https://myaccount-secondary.blob.core.windows.net/mynewcontainer \
    --destination /mnt/myfiles \
    --source-key <key> \
    --include "abc.txt"
```

Należy pamiętać, że użytkownik musi mieć dostęp do odczytu magazynu geograficznie nadmiarowego włączone.

### <a name="download-all-blobs"></a>Pobierz wszystkie obiekty BLOB

```azcopy
azcopy \
    --source https://myaccount.blob.core.windows.net/mycontainer \
    --destination /mnt/myfiles \
    --source-key <key> \
    --recursive
```

Załóżmy następujące hello obiekty BLOB znajdują się w określonym kontenerze hello:  

```
abc.txt
abc1.txt
abc2.txt
vd1/a.txt
vd1/abcd.txt
```

Po wykonaniu operacji pobierania hello hello katalogu `/mnt/myfiles` obejmuje hello następujące pliki:

```
/mnt/myfiles/abc.txt
/mnt/myfiles/abc1.txt
/mnt/myfiles/abc2.txt
/mnt/myfiles/vd1/a.txt
/mnt/myfiles/vd1/abcd.txt
```

Jeśli nie zostanie określona opcja `--recursive`, nie obiektu blob zostaną pobrane.

### <a name="download-blobs-with-specified-prefix"></a>Pobieranie obiektów blob z określonego prefiksu

```azcopy
azcopy \
    --source https://myaccount.blob.core.windows.net/mycontainer \
    --destination /mnt/myfiles \
    --source-key <key> \
    --include "a" \
    --recursive
```

Załóżmy następujące hello obiekty BLOB znajdują się w określonym kontenerze hello. Wszystkie obiekty BLOB rozpoczynający się od prefiksu powitania `a` zostaną pobrane.

```
abc.txt
abc1.txt
abc2.txt
xyz.txt
vd1\a.txt
vd1\abcd.txt
```

Po wykonaniu operacji pobierania hello hello folderu `/mnt/myfiles` obejmuje hello następujące pliki:

```
/mnt/myfiles/abc.txt
/mnt/myfiles/abc1.txt
/mnt/myfiles/abc2.txt
```

Prefiks Hello dotyczy katalogu wirtualnego toohello, który stanowi hello pierwsza część hello nazwa obiektu blob. W powyższym przykładzie hello hello katalogu wirtualnego jest niezgodny hello określonego prefiksu, nie obiektu blob jest pobierana. Ponadto, jeśli hello opcji `--recursive` nie zostanie określony, narzędzie AzCopy nie pobiera wszystkie obiekty BLOB.

### <a name="set-hello-last-modified-time-of-exported-files-toobe-same-as-hello-source-blobs"></a>Ustawianie czasu ostatniej modyfikacji hello z toobe eksportowanych plików tak samo jak hello źródła obiektów blob

```azcopy
azcopy \
    --source https://myaccount.blob.core.windows.net/mycontainer \
    --destination "/mnt/myfiles" \
    --source-key <key> \
    --preserve-last-modified-time
```

Można również wykluczyć obiekty BLOB z operacji pobierania hello na podstawie ich czasu ostatniej modyfikacji. Na przykład, jeśli chcesz tooexclude obiektów blob, których godzina ostatniej modyfikacji jest hello taką samą lub nowszą niż plik docelowy hello, dodać hello `--exclude-newer` opcji:

```azcopy
azcopy \
    --source https://myaccount.blob.core.windows.net/mycontainer \
    --destination /mnt/myfiles \
    --source-key <key> \
    --preserve-last-modified-time \
    --exclude-newer
```

Lub tooexclude obiektów blob, których godzina ostatniej modyfikacji jest hello tego samego lub starsze niż hello pliku docelowego, należy dodać hello `--exclude-older` opcji:

```azcopy
azcopy \
    --source https://myaccount.blob.core.windows.net/mycontainer \
    --destination /mnt/myfiles \
    --source-key <key> \
    --preserve-last-modified-time \
    --exclude-older
```

## <a name="blob-upload"></a>Obiekt blob: Przekaż
### <a name="upload-single-file"></a>Przekaż pojedynczy plik

```azcopy
azcopy \
    --source /mnt/myfiles \
    --destination https://myaccount.blob.core.windows.net/mycontainer \
    --dest-key <key> \
    --include "abc.txt"
```

Jeśli hello docelowy określony kontener nie istnieje, AzCopy tworzy go i przekazywanie hello pliku do niego.

### <a name="upload-single-file-toovirtual-directory"></a>Przekaż pojedynczy plik toovirtual katalogu

```azcopy
azcopy \
    --source /mnt/myfiles \
    --destination https://myaccount.blob.core.windows.net/mycontainer \
    --dest-key <key> \
    --include "abc.txt"
```

Jeśli hello określony katalog wirtualny nie istnieje, narzędzie AzCopy przekazuje hello pliku tooinclude hello katalogu wirtualnego w nazwie obiektu blob hello (*np.*, `vd/abc.txt` w powyższym przykładzie hello).

### <a name="upload-all-files"></a>Przekaż wszystkie pliki

```azcopy
azcopy \
    --source /mnt/myfiles \
    --destination https://myaccount.blob.core.windows.net/mycontainer \
    --dest-key <key> \
    --recursive
```

Określenie opcji `--recursive` przekazywanie zawartości hello hello określony rekursywnie magazynu tooBlob katalogu, co oznacza, jak również przekazać wszystkie podfoldery i pliki. Na przykład załóżmy następujące hello pliki znajdują się w folderze `/mnt/myfiles`:

```
/mnt/myfiles/abc.txt
/mnt/myfiles/abc1.txt
/mnt/myfiles/abc2.txt
/mnt/myfiles/subfolder/a.txt
/mnt/myfiles/subfolder/abcd.txt
```

Po wykonaniu operacji przekazywania hello hello kontener zawiera hello następujące pliki:

```
abc.txt
abc1.txt
abc2.txt
subfolder/a.txt
subfolder/abcd.txt
```

Gdy hello opcja `--recursive` nie jest określona, tylko hello następujące trzy pliki są przesyłane:

```
abc.txt
abc1.txt
abc2.txt
```

### <a name="upload-files-matching-specified-pattern"></a>Przekazywanie plików zgodnych z określonym wzorcem

```azcopy
azcopy \
    --source /mnt/myfiles \
    --destination https://myaccount.blob.core.windows.net/mycontainer \
    --dest-key <key> \
    --include "a*" \
    --recursive
```

Załóżmy następujące hello pliki znajdują się w folderze `/mnt/myfiles`:

```
/mnt/myfiles/abc.txt
/mnt/myfiles/abc1.txt
/mnt/myfiles/abc2.txt
/mnt/myfiles/xyz.txt
/mnt/myfiles/subfolder/a.txt
/mnt/myfiles/subfolder/abcd.txt
```

Po wykonaniu operacji przekazywania hello hello kontener zawiera hello następujące pliki:

```
abc.txt
abc1.txt
abc2.txt
subfolder/a.txt
subfolder/abcd.txt
```

Gdy hello opcji `--recursive` nie zostanie określony, narzędzie AzCopy pomija pliki, które są w katalogach podrzędnych:

```
abc.txt
abc1.txt
abc2.txt
```

### <a name="specify-hello-mime-content-type-of-a-destination-blob"></a>Określ typ zawartości MIME hello z docelowego obiektu blob
Domyślnie narzędzie AzCopy ustawia typ zawartości hello docelowego obiektu blob zbyt`application/octet-stream`. Jednak jawnie określić typ zawartości hello przy użyciu opcji hello `--set-content-type [content-type]`. Ta składnia ustawia hello typ zawartości dla wszystkich obiektów blob w operacji przekazywania.

```azcopy
azcopy \
    --source /mnt/myfiles \
    --destination https://myaccount.blob.core.windows.net/myContainer/ \
    --dest-key <key> \
    --include "ab" \
    --set-content-type "video/mp4"
```

Jeśli hello opcję `--set-content-type` jest określony bez wartości, a następnie ustawia AzCopy każdy obiekt blob lub pliku do typu zawartości zgodnie z tooits rozszerzenie pliku.

```azcopy
azcopy \
    --source /mnt/myfiles \
    --destination https://myaccount.blob.core.windows.net/myContainer/ \
    --dest-key <key> \
    --include "ab" \
    --set-content-type
```

## <a name="blob-copy"></a>Obiekt blob: kopiowania
### <a name="copy-single-blob-within-storage-account"></a>Skopiuj pojedynczego obiektu blob w ramach konta magazynu

```azcopy
azcopy \
    --source https://myaccount.blob.core.windows.net/mycontainer1 \
    --destination https://myaccount.blob.core.windows.net/mycontainer2 \
    --source-key <key> \
    --dest-key <key> \
    --include "abc.txt"
```

Podczas kopiowania obiektu blob bez — opcja synchronizacji kopii [po stronie serwera kopii](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx) operacja została wykonana.

### <a name="copy-single-blob-across-storage-accounts"></a>Skopiuj pojedynczego obiektu blob na kontach magazynu

```azcopy
azcopy \
    --source https://sourceaccount.blob.core.windows.net/mycontainer1 \
    --destination https://destaccount.blob.core.windows.net/mycontainer2 \
    --source-key <key1> \
    --dest-key <key2> \
    --include "abc.txt"
```

Podczas kopiowania obiektu blob bez — opcja synchronizacji kopii [po stronie serwera kopii](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx) operacja została wykonana.

### <a name="copy-single-blob-from-secondary-region-tooprimary-region"></a>Skopiuj pojedynczego obiektu blob z regionu pomocniczego tooprimary regionu

```azcopy
azcopy \
    --source https://myaccount1-secondary.blob.core.windows.net/mynewcontainer1 \
    --destination https://myaccount2.blob.core.windows.net/mynewcontainer2 \
    --source-key <key1> \
    --dest-key <key2> \
    --include "abc.txt"
```

Należy pamiętać, że użytkownik musi mieć dostęp do odczytu magazynu geograficznie nadmiarowego włączone.

### <a name="copy-single-blob-and-its-snapshots-across-storage-accounts"></a>Skopiuj pojedynczego obiektu blob i jego migawek wielu kont magazynu

```azcopy
azcopy \
    --source https://sourceaccount.blob.core.windows.net/mycontainer1 \
    --destination https://destaccount.blob.core.windows.net/mycontainer2 \
    --source-key <key1> \
    --dest-key <key2> \
    --include "abc.txt" \
    --include-snapshot
```

Po wykonaniu operacji kopiowania hello kontenera docelowego hello obejmuje hello obiektów blob i jego migawek. Witaj kontener zawiera następujące hello jego migawki i obiektów blob:

```
abc.txt
abc (2013-02-25 080757).txt
abc (2014-02-21 150331).txt
```

### <a name="synchronously-copy-blobs-across-storage-accounts"></a>Synchronicznie skopiować wielu kont magazynu obiektów blob
Narzędzie AzCopy domyślnie kopiuje dane między dwoma punktami końcowymi magazynu asynchronicznie. W związku z tym jest kopiowana hello kopiowania operacji działa w tle hello przy użyciu pojemności nieużywanej przepustowości ma umowy dotyczącej poziomu usług pod względem sposobu szybkiego obiektu blob. 

Witaj `--sync-copy` opcji gwarantuje, że operacji kopiowania hello pobiera spójne szybkości. AzCopy wykonuje synchroniczne kopiowania hello pobierać obiekty BLOB hello toocopy z hello określone źródło toolocal pamięci, a następnie przekazywanie ich miejsce docelowe magazynu obiektów Blob toohello.

```azcopy
azcopy \
    --source https://myaccount1.blob.core.windows.net/myContainer/ \
    --destination https://myaccount2.blob.core.windows.net/myContainer/ \
    --source-key <key1> \
    --dest-key <key2> \
    --include "ab" \
    --sync-copy
```

`--sync-copy`może generować dodatkowe wyjście koszt w porównaniu tooasynchronous kopiowania. Witaj zalecane podejście jest toouse tej opcji w maszynie Wirtualnej platformy Azure, który znajduje się w hello tego samego regionu koszt wyjście tooavoid konta magazynu źródłowego.

## <a name="file-download"></a>Plik: Pobierz
### <a name="download-single-file"></a>Pobierz pojedynczy plik

```azcopy
azcopy \
    --source https://myaccount.file.core.windows.net/myfileshare/myfolder1/ \
    --destination /mnt/myfiles \
    --source-key <key> \
    --include "abc.txt"
```

Jeśli hello określone źródło jest udział plików na platformę Azure, a następnie należy określić hello dokładnej nazwy pliku, (*np.* `abc.txt`) toodownload pojedynczy plik, lub określ opcję `--recursive` toodownload wszystkie pliki w udziale hello rekursywnie. Próba toospecify zarówno wzorzec pliku, jak i opcja `--recursive` razem powoduje błąd.

### <a name="download-all-files"></a>Pobierz wszystkie pliki

```azcopy
azcopy \
    --source https://myaccount.file.core.windows.net/myfileshare/ \
    --destination /mnt/myfiles \
    --source-key <key> \
    --recursive
```

Należy pamiętać, że puste foldery nie zostaną pobrane.

## <a name="file-upload"></a>Plik: Przekaż
### <a name="upload-single-file"></a>Przekaż pojedynczy plik

```azcopy
azcopy \
    --source /mnt/myfiles \
    --destination https://myaccount.file.core.windows.net/myfileshare/ \
    --dest-key <key> \
    --include abc.txt
```

### <a name="upload-all-files"></a>Przekaż wszystkie pliki

```azcopy
azcopy \
    --source /mnt/myfiles \
    --destination https://myaccount.file.core.windows.net/myfileshare/ \
    --dest-key <key> \
    --recursive
```

Należy pamiętać, że wszystkie puste foldery nie zostały przekazane.

### <a name="upload-files-matching-specified-pattern"></a>Przekazywanie plików zgodnych z określonym wzorcem

```azcopy
azcopy \
    --source /mnt/myfiles \
    --destination https://myaccount.file.core.windows.net/myfileshare/ \
    --dest-key <key> \
    --include "ab*" \
    --recursive
```

## <a name="file-copy"></a>Plik: kopiowania
### <a name="copy-across-file-shares"></a>Kopiowanie między udziałami plików

```azcopy
azcopy \
    --source https://myaccount1.file.core.windows.net/myfileshare1/ \
    --destination https://myaccount2.file.core.windows.net/myfileshare2/ \
    --source-key <key1> \
    --dest-key <key2> \
    --recursive
```
Podczas kopiowania plików między udziałami plików [po stronie serwera kopii](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx) operacja została wykonana.

### <a name="copy-from-file-share-tooblob"></a>Kopiowanie z tooblob udziału plików

```azcopy
azcopy \ 
    --source https://myaccount1.file.core.windows.net/myfileshare/ \
    --destination https://myaccount2.blob.core.windows.net/mycontainer/ \
    --source-key <key1> \
    --dest-key <key2> \
    --recursive
```
Podczas kopiowania pliku z tooblob udziału pliku, [po stronie serwera kopii](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx) operacja została wykonana.

### <a name="copy-from-blob-toofile-share"></a>Kopiowanie z udziału toofile obiektów blob

```azcopy
azcopy \
    --source https://myaccount1.blob.core.windows.net/mycontainer/ \
    --destination https://myaccount2.file.core.windows.net/myfileshare/ \
    --source-key <key1> \
    --dest-key <key2> \
    --recursive
```
Podczas kopiowania pliku z udziału toofile obiektów blob, [po stronie serwera kopii](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx) operacja została wykonana.

### <a name="synchronously-copy-files"></a>Synchronicznie kopiować pliki
Można określić hello `--sync-copy` synchronicznie opcję toocopy danych z magazynem tooFile magazynu, Magazyn plików tooBlob magazynu oraz tooFile magazynu obiektów Blob magazynu. AzCopy uruchamia pobieranie hello źródła danych toolocal pamięci, a następnie przekazać go toodestination tej operacji. W tym przypadku standardowe wyjście koszt dotyczy.

```azcopy
azcopy \
    --source https://myaccount1.file.core.windows.net/myfileshare1/ \
    --destination https://myaccount2.file.core.windows.net/myfileshare2/ \
    --source-key <key1> \
    --dest-key <key2> \
    --recursive \
    --sync-copy
```

Podczas kopiowania z pliku magazynu tooBlob magazynu, typu obiektu blob domyślne hello jest blokowych obiektów blob, użytkownik może określić opcję `/BlobType:page` toochange hello docelowego obiektu blob.

Należy pamiętać, że `--sync-copy` może generować wyjście dodatkowych kosztów porównaniem tooasynchronous kopiowania. Witaj zalecane podejście jest toouse tej opcji w maszynie Wirtualnej platformy Azure, który znajduje się w hello tego samego regionu koszt wyjście tooavoid konta magazynu źródłowego.

## <a name="other-azcopy-features"></a>Inne funkcje AzCopy
### <a name="only-copy-data-that-doesnt-exist-in-hello-destination"></a>Tylko skopiować dane, które nie istnieje w docelowym hello
Witaj `--exclude-older` i `--exclude-newer` parametrów pozwalają tooexclude starszej lub nowszej źródła zasobów zapobiega kopiowaniu odpowiednio. Jeśli chcesz tylko toocopy źródła zasobów, które nie istnieje w docelowym hello, można określić obu tych parametrów w hello polecenia programu AzCopy:

    --source http://myaccount.blob.core.windows.net/mycontainer --destination /mnt/myfiles --source-key <sourcekey> --recursive --exclude-older --exclude-newer

    --source /mnt/myfiles --destination http://myaccount.file.core.windows.net/myfileshare --dest-key <destkey> --recursive --exclude-older --exclude-newer

    --source http://myaccount.blob.core.windows.net/mycontainer --destination http://myaccount.blob.core.windows.net/mycontainer1 --source-key <sourcekey> --dest-key <destkey> --recursive --exclude-older --exclude-newer

### <a name="use-a-configuration-file-toospecify-command-line-parameters"></a>Użyj konfiguracji parametry wiersza polecenia toospecify pliku

```azcopy
azcopy --config-file "azcopy-config.ini"
```

Parametry wiersza polecenia AzCopy można uwzględnić w pliku konfiguracji. Procesy AzCopy hello parametrów w pliku hello tak, jakby były one określone w wierszu polecenia hello, wykonywanie bezpośrednich podstawienia z zawartością hello hello pliku.

Załóżmy plik konfiguracji o nazwie `copyoperation`, który zawiera następujące wiersze hello. Każdy parametr narzędzia AzCopy można określić w jednym wierszu.

    --source http://myaccount.blob.core.windows.net/mycontainer --destination /mnt/myfiles --source-key <sourcekey> --recursive --quiet

lub na oddzielnych wierszach:

    --source http://myaccount.blob.core.windows.net/mycontainer
    --destination /mnt/myfiles
    --source-key<sourcekey>
    --recursive
    --quiet

Narzędzie AzCopy wynik negatywny, jeśli parametr hello można podzielić na dwa wiersze, jak pokazano poniżej, aby uzyskać hello `--source-key` parametru:

    http://myaccount.blob.core.windows.net/mycontainer
    /mnt/myfiles
    --sourcekey
    <sourcekey>
    --recursive
    --quiet

### <a name="specify-a-shared-access-signature-sas"></a>Określ sygnatury dostępu współdzielonego (SAS)

```azcopy
azcopy \
    --source https://myaccount.blob.core.windows.net/mycontainer1 \
    --destination https://myaccount.blob.core.windows.net/mycontainer2 \
    --source-sas <SAS1> \
    --dest-sas <SAS2> \
    --include abc.txt
```

Można również określić sygnatury dostępu Współdzielonego w kontenerze hello identyfikatora URI:

```azcopy
azcopy \
    --source https://myaccount.blob.core.windows.net/mycontainer1/?SourceSASToken \
    --destination /mnt/myfiles \
    --recursive
```

Należy pamiętać, że narzędzie AzCopy aktualnie obsługuje tylko hello [SAS konta](https://docs.microsoft.com/en-us/azure/storage/storage-dotnet-shared-access-signature-part-1).

### <a name="journal-file-folder"></a>Folder plików dziennika
Zawsze, gdy wystawiać tooAzCopy polecenia, sprawdza czy istnieje plik dziennika w folderze domyślnym hello, lub czy istnieje w folderze określonej za pomocą tej opcji. Jeśli plik dziennika hello nie istnieje w każdym miejscu, AzCopy traktuje operacji hello jako nowy i generuje nowy plik dziennika.

Jeśli istnieje plik dziennika hello, AzCopy sprawdza, czy hello wiersza polecenia, które możesz wpisać zgodny hello wiersza polecenia w pliku dziennika hello. Jeśli dwa wiersze polecenia hello są zgodne, AzCopy wznawia hello nieukończone działania. Jeśli nie są zgodne, AzCopy monituje użytkownika tooeither Zastąp hello dziennika pliku toostart nowej operacji lub toocancel hello bieżącej operacji.

Jeśli chcesz, aby toouse hello domyślna lokalizacja pliku dziennika hello:

```azcopy
azcopy \
    --source /mnt/myfiles \
    --destination https://myaccount.blob.core.windows.net/mycontainer \
    --dest-key <key> \
    --resume
```

Jeśli pominięto opcję `--resume`, lub określ opcję `--resume` bez ścieżki folderu hello, jak pokazano powyżej, AzCopy tworzy plik dziennika hello w hello domyślnej lokalizacji, która jest `~\Microsoft\Azure\AzCopy`. Jeśli plik dziennika hello już istnieje, AzCopy wznawia operację hello na podstawie hello pliku dziennika.

Jeśli chcesz, aby toospecify niestandardową lokalizację pliku dziennika hello:

```azcopy
azcopy \
    --source /mnt/myfiles \
    --destination https://myaccount.blob.core.windows.net/mycontainer \
    --dest-key key \
    --resume "/mnt/myjournal"
```

W tym przykładzie tworzy plik dziennika hello, jeśli jeszcze nie istnieje. Jeśli istnieje, narzędzie AzCopy wznawia operacji hello na podstawie hello pliku dziennika.

Tooresume operacji AzCopy, powtórz hello tego samego polecenia. Narzędzie AzCopy w systemie Linux następnie wyświetli monit o potwierdzenie:

```azcopy
Incomplete operation with same command line detected at hello journal directory "/home/myaccount/Microsoft/Azure/AzCopy", do you want tooresume hello operation? Choose Yes tooresume, choose No toooverwrite hello journal toostart a new operation. (Yes/No)
```

### <a name="output-verbose-logs"></a>Dzienniki pełne dane wyjściowe

```azcopy
azcopy \
    --source /mnt/myfiles \
    --destination https://myaccount.blob.core.windows.net/mycontainer \
    --dest-key <key> \
    --verbose
```

### <a name="specify-hello-number-of-concurrent-operations-toostart"></a>Określ liczbę hello toostart jednoczesnych operacji
Opcja `--parallel-level` określa liczbę hello operacje kopiowania współbieżnych. Domyślnie narzędzie AzCopy uruchamia określoną liczbę jednoczesnych operacji tooincrease hello danych przeniesienie przepływności. Witaj liczba jednoczesnych operacji osiem godzin hello liczbę procesorów, masz. Jeśli używasz narzędzia AzCopy w niskiej przepustowości sieci, można określić mniejszą liczbę dla — poziom równoległe tooavoid niepowodzenie spowodowane przez konkurencji zasobów.

[!TIP]
>tooview hello pełną listę parametrów narzędzia AzCopy, zapoznaj się z "azcopy--pomocy" menu.

## <a name="known-issues-and-best-practices"></a>Znane problemy i najlepsze rozwiązania
### <a name="error-net-core-is-not-found-in-hello-system"></a>Błąd: Nie znaleziono .NET Core w systemie hello.
Jeśli wystąpią komunikat o błędzie informujący, że oprogramowanie .NET Core nie jest zainstalowany w systemie hello hello ścieżki toohello .NET Core binary `dotnet` może brakować.

W kolejności tooaddress ten problem, Znajdź hello binary .NET Core w systemie hello:
```bash
sudo find / -name dotnet
```

To polecenie zwróci hello ścieżki toohello dotnet binarnego. 

    /opt/rh/rh-dotnetcore11/root/usr/bin/dotnet
    /opt/rh/rh-dotnetcore11/root/usr/lib64/dotnetcore/dotnet
    /opt/rh/rh-dotnetcore11/root/usr/lib64/dotnetcore/shared/Microsoft.NETCore.App/1.1.2/dotnet

Teraz Dodaj zmiennej PATH toohello tej ścieżki. Sudo Edytuj secure_path toocontain hello ścieżki toohello dotnet binarne:
```bash 
sudo visudo
### Append hello path found in hello preceding example too'secure_path' variable
```

W tym przykładzie zmienna secure_path odczytuje jako:

```
secure_path = /sbin:/bin:/usr/sbin:/usr/bin:/opt/rh/rh-dotnetcore11/root/usr/bin/
```

Dla bieżącego użytkownika hello Edytuj.bash_profile/.profile tooinclude hello ścieżki toohello dotnet binarne w zmiennej PATH 
```bash
vi ~/.bash_profile
### Append hello path found in hello preceding example too'PATH' variable
```

Sprawdź, czy oprogramowanie .NET Core jest w ŚCIEŻCE:
```bash
which dotnet
sudo which dotnet
```

### <a name="error-installing-azcopy"></a>Błąd podczas instalowania narzędzia AzCopy
Jeśli wystąpią problemy z instalacją AzCopy, możesz spróbować toorun wyodrębnione narzędzie AzCopy przy użyciu skryptu bash hello w hello `azcopy` folderu.

```bash
cd azcopy
./azcopy
```

### <a name="limit-concurrent-writes-while-copying-data"></a>Limit równoczesnych zapisów podczas kopiowania danych
Podczas kopiowania obiektów blob lub pliki z narzędzia AzCopy, należy pamiętać, że inna aplikacja może być modyfikowanie hello danych podczas kopiowania go. Jeśli to możliwe upewnij się, że hello dane, które są kopiowane nie jest modyfikowana podczas operacji kopiowania hello. Na przykład podczas kopiowania wirtualnego dysku twardego skojarzonego z maszyny wirtualnej platformy Azure, upewnij się, że żadne inne aplikacje nie są obecnie zapisywania toohello wirtualnego dysku twardego. Toodo dobrze to jest dzierżawa toobe zasobów hello skopiowane. Alternatywnie można najpierw Utwórz migawkę hello wirtualnego dysku twardego, a następnie skopiuj hello migawki.

Jeśli nie można zapobiec innych aplikacji z zapisywania tooblobs lub plików podczas kopiowane są następnie pamiętać przez zadanie hello czasu hello zakończy, hello kopiowanych zasobów mogą już pełnej zgodności z hello źródła zasobów.

### <a name="run-one-azcopy-instance-on-one-machine"></a>Uruchom jedno wystąpienie AzCopy na jednej maszynie.
Narzędzie AzCopy jest zaprojektowana toomaximize hello wykorzystania transferu danych hello tooaccelerate zasobów maszyny, zaleca się uruchomić tylko jedno wystąpienie AzCopy na jednej maszynie i określ opcję hello `--parallel-level` Jeśli potrzebujesz więcej jednoczesnych operacji. Aby uzyskać więcej informacji, wpisz `AzCopy --help parallel-level` hello wiersza polecenia.

## <a name="next-steps"></a>Następne kroki
Aby uzyskać więcej informacji na temat usługi Azure Storage i AzCopy zobacz następujące zasoby hello:

### <a name="azure-storage-documentation"></a>Dokumentacja magazynu Azure:
* [Wprowadzenie tooAzure magazynu](storage-introduction.md)
* [Tworzenie konta magazynu](storage-create-storage-account.md)
* [Zarządzanie obiektów blob z Eksploratora usługi Storage](https://docs.microsoft.com/en-us/azure/vs-azure-tools-storage-explorer-blobs)
* [Przy użyciu hello 2.0 interfejsu wiersza polecenia platformy Azure z usługą Azure Storage](storage-azure-cli.md)
* [Jak toouse magazynu obiektów Blob w języku C++](storage-c-plus-plus-how-to-use-blobs.md)
* [Jak toouse magazynu obiektów Blob w języku Java](storage-java-how-to-use-blob-storage.md)
* [Jak toouse magazynu obiektów Blob w oprogramowaniu Node.js](storage-nodejs-how-to-use-blob-storage.md)
* [Jak toouse magazynu obiektów Blob w języku Python](storage-python-how-to-use-blob-storage.md)

### <a name="azure-storage-blog-posts"></a>Wpisy blogu magazynu Azure:
* [Anonsowanie AzCopy w wersji zapoznawczej systemu Linux](https://azure.microsoft.com/en-in/blog/announcing-azcopy-on-linux-preview/)
* [Wprowadzenie Podgląd Biblioteka przepływu danych usługi Azure Storage](https://azure.microsoft.com/blog/introducing-azure-storage-data-movement-library-preview-2/)
* [AzCopy: Wprowadzenie do kopiowania synchroniczne i dostosowane typ zawartości](http://blogs.msdn.com/b/windowsazurestorage/archive/2015/01/13/azcopy-introducing-synchronous-copy-and-customized-content-type.aspx)
* [Narzędzie AzCopy: Announcing ogólne dostępności 3.0 AzCopy oraz wersji zapoznawczej AzCopy 4.0 z tabeli i plik pomocy technicznej](http://blogs.msdn.com/b/windowsazurestorage/archive/2014/10/29/azcopy-announcing-general-availability-of-azcopy-3-0-plus-preview-release-of-azcopy-4-0-with-table-and-file-support.aspx)
* [Narzędzie AzCopy: Zoptymalizowana pod kątem scenariuszy kopii na dużą skalę](http://go.microsoft.com/fwlink/?LinkId=507682)
* [AzCopy: Obsługa dostęp do odczytu magazynu geograficznie nadmiarowego](http://blogs.msdn.com/b/windowsazurestorage/archive/2014/04/07/azcopy-support-for-read-access-geo-redundant-account.aspx)
* [Narzędzie AzCopy: Transfer danych za pomocą trybu ponownego uruchamiania i tokenu sygnatury dostępu Współdzielonego](http://blogs.msdn.com/b/windowsazurestorage/archive/2013/09/07/azcopy-transfer-data-with-re-startable-mode-and-sas-token.aspx)
* [Narzędzia AzCopy: Blob kopiowania między konta przy użyciu](http://blogs.msdn.com/b/windowsazurestorage/archive/2013/04/01/azcopy-using-cross-account-copy-blob.aspx)
* [Narzędzie AzCopy: Przekazywanie pobieranie plików dla obiektów blob Azure](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/12/03/azcopy-uploading-downloading-files-for-windows-azure-blobs.aspx)

