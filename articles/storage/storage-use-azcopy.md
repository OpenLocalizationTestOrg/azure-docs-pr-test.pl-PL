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
ms.openlocfilehash: a77db84c3a3e06f0ad4e87d02b14a5c62ed8d9ad
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="transfer-data-with-hello-azcopy-on-windows"></a><span data-ttu-id="4ec04-105">Transfer danych za pomocą narzędzia AzCopy hello w systemie Windows</span><span class="sxs-lookup"><span data-stu-id="4ec04-105">Transfer data with hello AzCopy on Windows</span></span>
<span data-ttu-id="4ec04-106">Narzędzie AzCopy to narzędzie wiersza polecenia przeznaczone do kopiowania tooand danych z magazynu obiektów Blob Microsoft Azure, plików i tabeli przy użyciu prostych poleceń z optymalną wydajnością.</span><span class="sxs-lookup"><span data-stu-id="4ec04-106">AzCopy is a command-line utility designed for copying data tooand from Microsoft Azure Blob, File, and Table storage using simple commands with optimal performance.</span></span> <span data-ttu-id="4ec04-107">Możesz skopiować dane z jednego obiektu tooanother w ramach konta magazynu lub między kontami magazynu.</span><span class="sxs-lookup"><span data-stu-id="4ec04-107">You can copy data from one object tooanother within your storage account, or between storage accounts.</span></span>

<span data-ttu-id="4ec04-108">Istnieją dwie wersje programu AzCopy, który można pobrać.</span><span class="sxs-lookup"><span data-stu-id="4ec04-108">There are two versions of AzCopy that you can download.</span></span> <span data-ttu-id="4ec04-109">AzCopy w systemie Windows jest oparty na platformie .NET Framework i oferuje opcje wiersza polecenia Styl systemu Windows.</span><span class="sxs-lookup"><span data-stu-id="4ec04-109">AzCopy on Windows is built with .NET Framework, and offers Windows style command-line options.</span></span> <span data-ttu-id="4ec04-110">[Narzędzie AzCopy w systemie Linux](storage-use-azcopy-linux.md) wbudowana w .NET Framework Core, który jest przeznaczony dla platformy Linux oferty styl POSIX opcje wiersza polecenia.</span><span class="sxs-lookup"><span data-stu-id="4ec04-110">[AzCopy on Linux](storage-use-azcopy-linux.md) is built with .NET Core Framework which targets Linux platforms offering POSIX style command-line options.</span></span> <span data-ttu-id="4ec04-111">W tym artykule omówiono AzCopy w systemie Windows.</span><span class="sxs-lookup"><span data-stu-id="4ec04-111">This article covers AzCopy on Windows.</span></span>

## <a name="download-and-install-azcopy"></a><span data-ttu-id="4ec04-112">Pobierz i zainstaluj narzędzie AzCopy</span><span class="sxs-lookup"><span data-stu-id="4ec04-112">Download and install AzCopy</span></span>
### <a name="azcopy-on-windows"></a><span data-ttu-id="4ec04-113">Narzędzie AzCopy w systemie Windows</span><span class="sxs-lookup"><span data-stu-id="4ec04-113">AzCopy on Windows</span></span>
<span data-ttu-id="4ec04-114">Pobierz hello [najnowszą wersję programu AzCopy w systemie Windows](http://aka.ms/downloadazcopy).</span><span class="sxs-lookup"><span data-stu-id="4ec04-114">Download hello [latest version of AzCopy on Windows](http://aka.ms/downloadazcopy).</span></span>

#### <a name="installation-on-windows"></a><span data-ttu-id="4ec04-115">Instalacja w systemie Windows</span><span class="sxs-lookup"><span data-stu-id="4ec04-115">Installation on Windows</span></span>
<span data-ttu-id="4ec04-116">Po zainstalowaniu narzędzia AzCopy w systemie Windows za pomocą Instalatora hello, Otwórz okno polecenia i przejdź katalog instalacyjny AzCopy toohello na komputerze — w przypadku gdy hello `AzCopy.exe` wykonywalny znajduje się.</span><span class="sxs-lookup"><span data-stu-id="4ec04-116">After installing AzCopy on Windows using hello installer, open a command window and navigate toohello AzCopy installation directory on your computer - where hello `AzCopy.exe` executable is located.</span></span> <span data-ttu-id="4ec04-117">W razie potrzeby można dodać ścieżki systemu tooyour lokalizacji instalacji hello AzCopy.</span><span class="sxs-lookup"><span data-stu-id="4ec04-117">If desired, you can add hello AzCopy installation location tooyour system path.</span></span> <span data-ttu-id="4ec04-118">Domyślnie program AzCopy jest zainstalowany za`%ProgramFiles(x86)%\Microsoft SDKs\Azure\AzCopy` lub `%ProgramFiles%\Microsoft SDKs\Azure\AzCopy`.</span><span class="sxs-lookup"><span data-stu-id="4ec04-118">By default, AzCopy is installed too`%ProgramFiles(x86)%\Microsoft SDKs\Azure\AzCopy` or `%ProgramFiles%\Microsoft SDKs\Azure\AzCopy`.</span></span>

## <a name="writing-your-first-azcopy-command"></a><span data-ttu-id="4ec04-119">Pisanie pierwszego polecenia AzCopy</span><span class="sxs-lookup"><span data-stu-id="4ec04-119">Writing your first AzCopy command</span></span>
<span data-ttu-id="4ec04-120">Podstawowa składnia polecenia AzCopy Hello jest:</span><span class="sxs-lookup"><span data-stu-id="4ec04-120">hello basic syntax for AzCopy commands is:</span></span>

```azcopy
AzCopy /Source:<source> /Dest:<destination> [Options]
```

<span data-ttu-id="4ec04-121">Witaj następujące przykłady pokazują różnych scenariuszy kopiowania tooand danych z programu Microsoft Azure blob, tabel i plików.</span><span class="sxs-lookup"><span data-stu-id="4ec04-121">hello following examples demonstrate a variety of scenarios for copying data tooand from Microsoft Azure Blobs, Files, and Tables.</span></span> <span data-ttu-id="4ec04-122">Zobacz toohello [parametrów narzędzia AzCopy](#azcopy-parameters) sekcji, aby uzyskać szczegółowy opis hello parametrami używanymi w każdej próbki.</span><span class="sxs-lookup"><span data-stu-id="4ec04-122">Refer toohello [AzCopy Parameters](#azcopy-parameters) section for a detailed explanation of hello parameters used in each sample.</span></span>

## <a name="blob-download"></a><span data-ttu-id="4ec04-123">Obiekt blob: Pobierz</span><span class="sxs-lookup"><span data-stu-id="4ec04-123">Blob: Download</span></span>
### <a name="download-single-blob"></a><span data-ttu-id="4ec04-124">Pobieranie pojedynczego obiektu blob</span><span class="sxs-lookup"><span data-stu-id="4ec04-124">Download single blob</span></span>

```azcopy
AzCopy /Source:https://myaccount.blob.core.windows.net/mycontainer /Dest:C:\myfolder /SourceKey:key /Pattern:"abc.txt"
```

<span data-ttu-id="4ec04-125">Należy pamiętać, że jeśli hello folder `C:\myfolder` nie istnieje, utworzy on i Pobierz AzCopy `abc.txt ` do nowego folderu hello.</span><span class="sxs-lookup"><span data-stu-id="4ec04-125">Note that if hello folder `C:\myfolder` does not exist, AzCopy will create it and download `abc.txt ` into hello new folder.</span></span>

### <a name="download-single-blob-from-secondary-region"></a><span data-ttu-id="4ec04-126">Pobieranie pojedynczego obiektu blob z regionu pomocniczego</span><span class="sxs-lookup"><span data-stu-id="4ec04-126">Download single blob from secondary region</span></span>

```azcopy
AzCopy /Source:https://myaccount-secondary.blob.core.windows.net/mynewcontainer /Dest:C:\myfolder /SourceKey:key /Pattern:abc.txt
```

<span data-ttu-id="4ec04-127">Należy pamiętać, że użytkownik musi mieć dostęp do odczytu magazynu geograficznie nadmiarowego włączone.</span><span class="sxs-lookup"><span data-stu-id="4ec04-127">Note that you must have read-access geo-redundant storage enabled.</span></span>

### <a name="download-all-blobs"></a><span data-ttu-id="4ec04-128">Pobierz wszystkie obiekty BLOB</span><span class="sxs-lookup"><span data-stu-id="4ec04-128">Download all blobs</span></span>

```azcopy
AzCopy /Source:https://myaccount.blob.core.windows.net/mycontainer /Dest:C:\myfolder /SourceKey:key /S
```

<span data-ttu-id="4ec04-129">Załóżmy następujące hello obiekty BLOB znajdują się w określonym kontenerze hello:</span><span class="sxs-lookup"><span data-stu-id="4ec04-129">Assume hello following blobs reside in hello specified container:</span></span>  

    abc.txt
    abc1.txt
    abc2.txt
    vd1\a.txt
    vd1\abcd.txt

<span data-ttu-id="4ec04-130">Po wykonaniu operacji pobierania hello hello katalogu `C:\myfolder` uwzględni hello następujące pliki:</span><span class="sxs-lookup"><span data-stu-id="4ec04-130">After hello download operation, hello directory `C:\myfolder` will include hello following files:</span></span>

    C:\myfolder\abc.txt
    C:\myfolder\abc1.txt
    C:\myfolder\abc2.txt
    C:\myfolder\vd1\a.txt
    C:\myfolder\vd1\abcd.txt

<span data-ttu-id="4ec04-131">Jeśli nie zostanie określona opcja `/S`, nie obiekty BLOB zostaną pobrane.</span><span class="sxs-lookup"><span data-stu-id="4ec04-131">If you do not specify option `/S`, no blobs will be downloaded.</span></span>

### <a name="download-blobs-with-specified-prefix"></a><span data-ttu-id="4ec04-132">Pobieranie obiektów blob z określonego prefiksu</span><span class="sxs-lookup"><span data-stu-id="4ec04-132">Download blobs with specified prefix</span></span>

```azcopy
AzCopy /Source:https://myaccount.blob.core.windows.net/mycontainer /Dest:C:\myfolder /SourceKey:key /Pattern:a /S
```

<span data-ttu-id="4ec04-133">Załóżmy następujące hello obiekty BLOB znajdują się w określonym kontenerze hello.</span><span class="sxs-lookup"><span data-stu-id="4ec04-133">Assume hello following blobs reside in hello specified container.</span></span> <span data-ttu-id="4ec04-134">Wszystkie obiekty BLOB rozpoczynający się od prefiksu powitania `a` zostaną pobrane:</span><span class="sxs-lookup"><span data-stu-id="4ec04-134">All blobs beginning with hello prefix `a` will be downloaded:</span></span>

    abc.txt
    abc1.txt
    abc2.txt
    xyz.txt
    vd1\a.txt
    vd1\abcd.txt

<span data-ttu-id="4ec04-135">Po wykonaniu operacji pobierania hello hello folderu `C:\myfolder` uwzględni hello następujące pliki:</span><span class="sxs-lookup"><span data-stu-id="4ec04-135">After hello download operation, hello folder `C:\myfolder` will include hello following files:</span></span>

    C:\myfolder\abc.txt
    C:\myfolder\abc1.txt
    C:\myfolder\abc2.txt

<span data-ttu-id="4ec04-136">Prefiks Hello dotyczy katalogu wirtualnego toohello, który stanowi hello pierwsza część hello nazwa obiektu blob.</span><span class="sxs-lookup"><span data-stu-id="4ec04-136">hello prefix applies toohello virtual directory, which forms hello first part of hello blob name.</span></span> <span data-ttu-id="4ec04-137">W powyższym przykładzie hello hello katalogu wirtualnego nie pasuje hello określony prefiks, więc nie zostanie pobrana.</span><span class="sxs-lookup"><span data-stu-id="4ec04-137">In hello example shown above, hello virtual directory does not match hello specified prefix, so it is not downloaded.</span></span> <span data-ttu-id="4ec04-138">Ponadto, jeśli hello opcji `\S` nie zostanie określony, narzędzie AzCopy nie będzie pobierał żadnych obiektów blob.</span><span class="sxs-lookup"><span data-stu-id="4ec04-138">In addition, if hello option `\S` is not specified, AzCopy will not download any blobs.</span></span>

### <a name="set-hello-last-modified-time-of-exported-files-toobe-same-as-hello-source-blobs"></a><span data-ttu-id="4ec04-139">Ustawianie czasu ostatniej modyfikacji hello z toobe eksportowanych plików tak samo jak hello źródła obiektów blob</span><span class="sxs-lookup"><span data-stu-id="4ec04-139">Set hello last-modified time of exported files toobe same as hello source blobs</span></span>

```azcopy
AzCopy /Source:https://myaccount.blob.core.windows.net/mycontainer /Dest:C:\myfolder /SourceKey:key /MT
```

<span data-ttu-id="4ec04-140">Można również wykluczyć obiekty BLOB z operacji pobierania hello na podstawie ich czasu ostatniej modyfikacji.</span><span class="sxs-lookup"><span data-stu-id="4ec04-140">You can also exclude blobs from hello download operation based on their last-modified time.</span></span> <span data-ttu-id="4ec04-141">Na przykład, jeśli chcesz tooexclude obiektów blob, których godzina ostatniej modyfikacji jest hello taką samą lub nowszą niż plik docelowy hello, dodać hello `/XN` opcji:</span><span class="sxs-lookup"><span data-stu-id="4ec04-141">For example, if you want tooexclude blobs whose last modified time is hello same or newer than hello destination file, add hello `/XN` option:</span></span>

```azcopy
AzCopy /Source:https://myaccount.blob.core.windows.net/mycontainer /Dest:C:\myfolder /SourceKey:key /MT /XN
```

<span data-ttu-id="4ec04-142">Lub tooexclude obiektów blob, których godzina ostatniej modyfikacji jest hello tego samego lub starsze niż hello pliku docelowego, należy dodać hello `/XO` opcji:</span><span class="sxs-lookup"><span data-stu-id="4ec04-142">Or if you want tooexclude blobs whose last modified time is hello same or older than hello destination file, add hello `/XO` option:</span></span>

```azcopy
AzCopy /Source:https://myaccount.blob.core.windows.net/mycontainer /Dest:C:\myfolder /SourceKey:key /MT /XO
```

## <a name="blob-upload"></a><span data-ttu-id="4ec04-143">Obiekt blob: Przekaż</span><span class="sxs-lookup"><span data-stu-id="4ec04-143">Blob: Upload</span></span>
### <a name="upload-single-file"></a><span data-ttu-id="4ec04-144">Przekaż pojedynczy plik</span><span class="sxs-lookup"><span data-stu-id="4ec04-144">Upload single file</span></span>

```azcopy
AzCopy /Source:C:\myfolder /Dest:https://myaccount.blob.core.windows.net/mycontainer /DestKey:key /Pattern:"abc.txt"
```

<span data-ttu-id="4ec04-145">Jeśli hello docelowy określony kontener nie istnieje, narzędzie AzCopy będzie go utworzyć i przekazywanie pliku hello do niego.</span><span class="sxs-lookup"><span data-stu-id="4ec04-145">If hello specified destination container does not exist, AzCopy will create it and upload hello file into it.</span></span>

### <a name="upload-single-file-toovirtual-directory"></a><span data-ttu-id="4ec04-146">Przekaż pojedynczy plik toovirtual katalogu</span><span class="sxs-lookup"><span data-stu-id="4ec04-146">Upload single file toovirtual directory</span></span>

```azcopy
AzCopy /Source:C:\myfolder /Dest:https://myaccount.blob.core.windows.net/mycontainer/vd /DestKey:key /Pattern:abc.txt
```

<span data-ttu-id="4ec04-147">Jeśli hello określony katalog wirtualny nie istnieje, narzędzie AzCopy przekaże hello pliku tooinclude hello katalogu wirtualnego w swojej nazwy (*np.*, `vd/abc.txt` w powyższym przykładzie hello).</span><span class="sxs-lookup"><span data-stu-id="4ec04-147">If hello specified virtual directory does not exist, AzCopy will upload hello file tooinclude hello virtual directory in its name (*e.g.*, `vd/abc.txt` in hello example above).</span></span>

### <a name="upload-all-files"></a><span data-ttu-id="4ec04-148">Przekaż wszystkie pliki</span><span class="sxs-lookup"><span data-stu-id="4ec04-148">Upload all files</span></span>

```azcopy
AzCopy /Source:C:\myfolder /Dest:https://myaccount.blob.core.windows.net/mycontainer /DestKey:key /S
```

<span data-ttu-id="4ec04-149">Określenie opcji `/S` przekazywanie zawartości hello hello określony rekursywnie magazynu tooBlob katalogu, co oznacza, że wszystkie podfoldery i pliki zostaną przekazane również.</span><span class="sxs-lookup"><span data-stu-id="4ec04-149">Specifying option `/S` uploads hello contents of hello specified directory tooBlob storage recursively, meaning that all subfolders and their files will be uploaded as well.</span></span> <span data-ttu-id="4ec04-150">Na przykład załóżmy następujące hello pliki znajdują się w folderze `C:\myfolder`:</span><span class="sxs-lookup"><span data-stu-id="4ec04-150">For instance, assume hello following files reside in folder `C:\myfolder`:</span></span>

    C:\myfolder\abc.txt
    C:\myfolder\abc1.txt
    C:\myfolder\abc2.txt
    C:\myfolder\subfolder\a.txt
    C:\myfolder\subfolder\abcd.txt

<span data-ttu-id="4ec04-151">Po wykonaniu operacji przekazywania hello kontenera hello obejmuje hello następujące pliki:</span><span class="sxs-lookup"><span data-stu-id="4ec04-151">After hello upload operation, hello container will include hello following files:</span></span>

    abc.txt
    abc1.txt
    abc2.txt
    subfolder\a.txt
    subfolder\abcd.txt

<span data-ttu-id="4ec04-152">Jeśli nie zostanie określona opcja `/S`, AzCopy nie przekaże rekursywnie.</span><span class="sxs-lookup"><span data-stu-id="4ec04-152">If you do not specify option `/S`, AzCopy will not upload recursively.</span></span> <span data-ttu-id="4ec04-153">Po wykonaniu operacji przekazywania hello kontenera hello obejmuje hello następujące pliki:</span><span class="sxs-lookup"><span data-stu-id="4ec04-153">After hello upload operation, hello container will include hello following files:</span></span>

    abc.txt
    abc1.txt
    abc2.txt

### <a name="upload-files-matching-specified-pattern"></a><span data-ttu-id="4ec04-154">Przekazywanie plików zgodnych z określonym wzorcem</span><span class="sxs-lookup"><span data-stu-id="4ec04-154">Upload files matching specified pattern</span></span>

```azcopy
AzCopy /Source:C:\myfolder /Dest:https://myaccount.blob.core.windows.net/mycontainer /DestKey:key /Pattern:a* /S
```

<span data-ttu-id="4ec04-155">Załóżmy następujące hello pliki znajdują się w folderze `C:\myfolder`:</span><span class="sxs-lookup"><span data-stu-id="4ec04-155">Assume hello following files reside in folder `C:\myfolder`:</span></span>

    C:\myfolder\abc.txt
    C:\myfolder\abc1.txt
    C:\myfolder\abc2.txt
    C:\myfolder\xyz.txt
    C:\myfolder\subfolder\a.txt
    C:\myfolder\subfolder\abcd.txt

<span data-ttu-id="4ec04-156">Po wykonaniu operacji przekazywania hello kontenera hello obejmuje hello następujące pliki:</span><span class="sxs-lookup"><span data-stu-id="4ec04-156">After hello upload operation, hello container will include hello following files:</span></span>

    abc.txt
    abc1.txt
    abc2.txt
    subfolder\a.txt
    subfolder\abcd.txt

<span data-ttu-id="4ec04-157">Jeśli nie zostanie określona opcja `/S`, AzCopy przekaże tylko obiekty BLOB, które nie znajdują się w katalogu wirtualnym:</span><span class="sxs-lookup"><span data-stu-id="4ec04-157">If you do not specify option `/S`, AzCopy will only upload blobs that don't reside in a virtual directory:</span></span>

    C:\myfolder\abc.txt
    C:\myfolder\abc1.txt
    C:\myfolder\abc2.txt

### <a name="specify-hello-mime-content-type-of-a-destination-blob"></a><span data-ttu-id="4ec04-158">Określ typ zawartości MIME hello z docelowego obiektu blob</span><span class="sxs-lookup"><span data-stu-id="4ec04-158">Specify hello MIME content type of a destination blob</span></span>
<span data-ttu-id="4ec04-159">Domyślnie narzędzie AzCopy ustawia typ zawartości hello docelowego obiektu blob zbyt`application/octet-stream`.</span><span class="sxs-lookup"><span data-stu-id="4ec04-159">By default, AzCopy sets hello content type of a destination blob too`application/octet-stream`.</span></span> <span data-ttu-id="4ec04-160">Począwszy od wersji 3.1.0, można jawnie określić typ zawartości hello przy użyciu opcji hello `/SetContentType:[content-type]`.</span><span class="sxs-lookup"><span data-stu-id="4ec04-160">Beginning with version 3.1.0, you can explicitly specify hello content type via hello option `/SetContentType:[content-type]`.</span></span> <span data-ttu-id="4ec04-161">Ta składnia ustawia hello typ zawartości dla wszystkich obiektów blob w operacji przekazywania.</span><span class="sxs-lookup"><span data-stu-id="4ec04-161">This syntax sets hello content type for all blobs in an upload operation.</span></span>

```azcopy
AzCopy /Source:C:\myfolder\ /Dest:https://myaccount.blob.core.windows.net/myContainer/ /DestKey:key /Pattern:ab /SetContentType:video/mp4
```

<span data-ttu-id="4ec04-162">Jeśli określisz `/SetContentType` bez wartości, następnie AzCopy ustawi każdy obiekt blob lub typ zawartości pliku, zgodnie z tooits rozszerzenie pliku.</span><span class="sxs-lookup"><span data-stu-id="4ec04-162">If you specify `/SetContentType` without a value, then AzCopy will set each blob or file's content type according tooits file extension.</span></span>

```azcopy
AzCopy /Source:C:\myfolder\ /Dest:https://myaccount.blob.core.windows.net/myContainer/ /DestKey:key /Pattern:ab /SetContentType
```

## <a name="blob-copy"></a><span data-ttu-id="4ec04-163">Obiekt blob: kopiowania</span><span class="sxs-lookup"><span data-stu-id="4ec04-163">Blob: Copy</span></span>
### <a name="copy-single-blob-within-storage-account"></a><span data-ttu-id="4ec04-164">Skopiuj pojedynczego obiektu blob w ramach konta magazynu</span><span class="sxs-lookup"><span data-stu-id="4ec04-164">Copy single blob within Storage account</span></span>

```azcopy
AzCopy /Source:https://myaccount.blob.core.windows.net/mycontainer1 /Dest:https://myaccount.blob.core.windows.net/mycontainer2 /SourceKey:key /DestKey:key /Pattern:abc.txt
```

<span data-ttu-id="4ec04-165">Podczas kopiowania obiektu blob w ramach konta magazynu, [po stronie serwera kopii](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx) operacja została wykonana.</span><span class="sxs-lookup"><span data-stu-id="4ec04-165">When you copy a blob within a Storage account, a [server-side copy](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx) operation is performed.</span></span>

### <a name="copy-single-blob-across-storage-accounts"></a><span data-ttu-id="4ec04-166">Skopiuj pojedynczego obiektu blob na kontach magazynu</span><span class="sxs-lookup"><span data-stu-id="4ec04-166">Copy single blob across Storage accounts</span></span>

```azcopy
AzCopy /Source:https://sourceaccount.blob.core.windows.net/mycontainer1 /Dest:https://destaccount.blob.core.windows.net/mycontainer2 /SourceKey:key1 /DestKey:key2 /Pattern:abc.txt
```

<span data-ttu-id="4ec04-167">Podczas kopiowania obiektu blob na kontach magazynu, [po stronie serwera kopii](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx) operacja została wykonana.</span><span class="sxs-lookup"><span data-stu-id="4ec04-167">When you copy a blob across Storage accounts, a [server-side copy](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx) operation is performed.</span></span>

### <a name="copy-single-blob-from-secondary-region-tooprimary-region"></a><span data-ttu-id="4ec04-168">Skopiuj pojedynczego obiektu blob z regionu pomocniczego tooprimary regionu</span><span class="sxs-lookup"><span data-stu-id="4ec04-168">Copy single blob from secondary region tooprimary region</span></span>

```azcopy
AzCopy /Source:https://myaccount1-secondary.blob.core.windows.net/mynewcontainer1 /Dest:https://myaccount2.blob.core.windows.net/mynewcontainer2 /SourceKey:key1 /DestKey:key2 /Pattern:abc.txt
```

<span data-ttu-id="4ec04-169">Należy pamiętać, że użytkownik musi mieć dostęp do odczytu magazynu geograficznie nadmiarowego włączone.</span><span class="sxs-lookup"><span data-stu-id="4ec04-169">Note that you must have read-access geo-redundant storage enabled.</span></span>

### <a name="copy-single-blob-and-its-snapshots-across-storage-accounts"></a><span data-ttu-id="4ec04-170">Skopiuj pojedynczego obiektu blob i jego migawek wielu kont magazynu</span><span class="sxs-lookup"><span data-stu-id="4ec04-170">Copy single blob and its snapshots across Storage accounts</span></span>

```azcopy
    AzCopy /Source:https://sourceaccount.blob.core.windows.net/mycontainer1 /Dest:https://destaccount.blob.core.windows.net/mycontainer2 /SourceKey:key1 /DestKey:key2 /Pattern:abc.txt /Snapshot
```

<span data-ttu-id="4ec04-171">Po wykonaniu operacji kopiowania hello kontenera docelowego hello uwzględni hello obiektów blob i jego migawek.</span><span class="sxs-lookup"><span data-stu-id="4ec04-171">After hello copy operation, hello target container will include hello blob and its snapshots.</span></span> <span data-ttu-id="4ec04-172">Zakładając, że blob hello w powyższym przykładzie hello ma dwa migawki, kontener hello będzie zawierać następujące hello migawki i obiektów blob:</span><span class="sxs-lookup"><span data-stu-id="4ec04-172">Assuming hello blob in hello example above has two snapshots, hello container will include hello following blob and snapshots:</span></span>

    abc.txt
    abc (2013-02-25 080757).txt
    abc (2014-02-21 150331).txt

### <a name="synchronously-copy-blobs-across-storage-accounts"></a><span data-ttu-id="4ec04-173">Synchronicznie skopiować wielu kont magazynu obiektów blob</span><span class="sxs-lookup"><span data-stu-id="4ec04-173">Synchronously copy blobs across Storage accounts</span></span>
<span data-ttu-id="4ec04-174">Narzędzie AzCopy domyślnie kopiuje dane między dwoma punktami końcowymi magazynu asynchronicznie.</span><span class="sxs-lookup"><span data-stu-id="4ec04-174">AzCopy by default copies data between two storage endpoints asynchronously.</span></span> <span data-ttu-id="4ec04-175">W związku z tym uruchomi hello operacji kopiowania w tle hello przy użyciu pojemności nieużywanej przepustowości ma nie SLA pod względem sposobu szybkiego obiektu blob zostaną skopiowane, a AzCopy okresowo sprawdzać stan kopiowania hello, dopóki hello Kopiowanie zakończone lub nie powiodło się.</span><span class="sxs-lookup"><span data-stu-id="4ec04-175">Therefore, hello copy operation will run in hello background using spare bandwidth capacity that has no SLA in terms of how fast a blob will be copied, and AzCopy will periodically check hello copy status until hello copying is completed or failed.</span></span>

<span data-ttu-id="4ec04-176">Witaj `/SyncCopy` opcji gwarantuje, że operacji kopiowania hello otrzyma spójne szybkości.</span><span class="sxs-lookup"><span data-stu-id="4ec04-176">hello `/SyncCopy` option ensures that hello copy operation will get consistent speed.</span></span> <span data-ttu-id="4ec04-177">AzCopy wykonuje synchroniczne kopiowania hello pobierać obiekty BLOB hello toocopy z hello określone źródło toolocal pamięci, a następnie przekazywanie ich miejsce docelowe magazynu obiektów Blob toohello.</span><span class="sxs-lookup"><span data-stu-id="4ec04-177">AzCopy performs hello synchronous copy by downloading hello blobs toocopy from hello specified source toolocal memory, and then uploading them toohello Blob storage destination.</span></span>

```azcopy
AzCopy /Source:https://myaccount1.blob.core.windows.net/myContainer/ /Dest:https://myaccount2.blob.core.windows.net/myContainer/ /SourceKey:key1 /DestKey:key2 /Pattern:ab /SyncCopy
```

<span data-ttu-id="4ec04-178">`/SyncCopy`może generować wyjście dodatkowych kosztów kopiowania porównaniu tooasynchronous hello zalecane podejście jest toouse tej opcji w maszynie Wirtualnej platformy Azure, który znajduje się w hello tego samego regionu koszt wyjście tooavoid konta magazynu źródłowego.</span><span class="sxs-lookup"><span data-stu-id="4ec04-178">`/SyncCopy` might generate additional egress cost compared tooasynchronous copy, hello recommended approach is toouse this option in an Azure VM that is in hello same region as your source storage account tooavoid egress cost.</span></span>

## <a name="file-download"></a><span data-ttu-id="4ec04-179">Plik: Pobierz</span><span class="sxs-lookup"><span data-stu-id="4ec04-179">File: Download</span></span>
### <a name="download-single-file"></a><span data-ttu-id="4ec04-180">Pobierz pojedynczy plik</span><span class="sxs-lookup"><span data-stu-id="4ec04-180">Download single file</span></span>

```azcopy
AzCopy /Source:https://myaccount.file.core.windows.net/myfileshare/myfolder1/ /Dest:C:\myfolder /SourceKey:key /Pattern:abc.txt
```

<span data-ttu-id="4ec04-181">Jeśli hello określone źródło jest udział plików na platformę Azure, a następnie należy określić hello dokładnej nazwy pliku, (*np.* `abc.txt`) toodownload pojedynczy plik, lub określ opcję `/S` toodownload wszystkie pliki w udziale hello rekursywnie.</span><span class="sxs-lookup"><span data-stu-id="4ec04-181">If hello specified source is an Azure file share, then you must either specify hello exact file name, (*e.g.* `abc.txt`) toodownload a single file, or specify option `/S` toodownload all files in hello share recursively.</span></span> <span data-ttu-id="4ec04-182">Próba toospecify zarówno wzorzec pliku, jak i opcja `/S` razem spowoduje wystąpienie błędu.</span><span class="sxs-lookup"><span data-stu-id="4ec04-182">Attempting toospecify both a file pattern and option `/S` together will result in an error.</span></span>

### <a name="download-all-files"></a><span data-ttu-id="4ec04-183">Pobierz wszystkie pliki</span><span class="sxs-lookup"><span data-stu-id="4ec04-183">Download all files</span></span>

```azcopy
AzCopy /Source:https://myaccount.file.core.windows.net/myfileshare/ /Dest:C:\myfolder /SourceKey:key /S
```

<span data-ttu-id="4ec04-184">Uwaga puste foldery nie zostaną pobrane.</span><span class="sxs-lookup"><span data-stu-id="4ec04-184">Note that any empty folders will not be downloaded.</span></span>

## <a name="file-upload"></a><span data-ttu-id="4ec04-185">Plik: Przekaż</span><span class="sxs-lookup"><span data-stu-id="4ec04-185">File: Upload</span></span>
### <a name="upload-single-file"></a><span data-ttu-id="4ec04-186">Przekaż pojedynczy plik</span><span class="sxs-lookup"><span data-stu-id="4ec04-186">Upload single file</span></span>

```azcopy
AzCopy /Source:C:\myfolder /Dest:https://myaccount.file.core.windows.net/myfileshare/ /DestKey:key /Pattern:abc.txt
```

### <a name="upload-all-files"></a><span data-ttu-id="4ec04-187">Przekaż wszystkie pliki</span><span class="sxs-lookup"><span data-stu-id="4ec04-187">Upload all files</span></span>

```azcopy
AzCopy /Source:C:\myfolder /Dest:https://myaccount.file.core.windows.net/myfileshare/ /DestKey:key /S
```

<span data-ttu-id="4ec04-188">Uwaga puste foldery nie zostaną przekazane.</span><span class="sxs-lookup"><span data-stu-id="4ec04-188">Note that any empty folders will not be uploaded.</span></span>

### <a name="upload-files-matching-specified-pattern"></a><span data-ttu-id="4ec04-189">Przekazywanie plików zgodnych z określonym wzorcem</span><span class="sxs-lookup"><span data-stu-id="4ec04-189">Upload files matching specified pattern</span></span>

```azcopy
AzCopy /Source:C:\myfolder /Dest:https://myaccount.file.core.windows.net/myfileshare/ /DestKey:key /Pattern:ab* /S
```

## <a name="file-copy"></a><span data-ttu-id="4ec04-190">Plik: kopiowania</span><span class="sxs-lookup"><span data-stu-id="4ec04-190">File: Copy</span></span>
### <a name="copy-across-file-shares"></a><span data-ttu-id="4ec04-191">Kopiowanie między udziałami plików</span><span class="sxs-lookup"><span data-stu-id="4ec04-191">Copy across file shares</span></span>

```azcopy
AzCopy /Source:https://myaccount1.file.core.windows.net/myfileshare1/ /Dest:https://myaccount2.file.core.windows.net/myfileshare2/ /SourceKey:key1 /DestKey:key2 /S
```
<span data-ttu-id="4ec04-192">Podczas kopiowania plików między udziałami plików [po stronie serwera kopii](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx) operacja została wykonana.</span><span class="sxs-lookup"><span data-stu-id="4ec04-192">When you copy a file across file shares, a [server-side copy](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx) operation is performed.</span></span>

### <a name="copy-from-file-share-tooblob"></a><span data-ttu-id="4ec04-193">Kopiowanie z tooblob udziału plików</span><span class="sxs-lookup"><span data-stu-id="4ec04-193">Copy from file share tooblob</span></span>

```azcopy
AzCopy /Source:https://myaccount1.file.core.windows.net/myfileshare/ /Dest:https://myaccount2.blob.core.windows.net/mycontainer/ /SourceKey:key1 /DestKey:key2 /S
```
<span data-ttu-id="4ec04-194">Podczas kopiowania pliku z tooblob udziału pliku, [po stronie serwera kopii](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx) operacja została wykonana.</span><span class="sxs-lookup"><span data-stu-id="4ec04-194">When you copy a file from file share tooblob, a [server-side copy](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx) operation is performed.</span></span>


### <a name="copy-from-blob-toofile-share"></a><span data-ttu-id="4ec04-195">Kopiowanie z udziału toofile obiektów blob</span><span class="sxs-lookup"><span data-stu-id="4ec04-195">Copy from blob toofile share</span></span>

```azcopy
AzCopy /Source:https://myaccount1.blob.core.windows.net/mycontainer/ /Dest:https://myaccount2.file.core.windows.net/myfileshare/ /SourceKey:key1 /DestKey:key2 /S
```
<span data-ttu-id="4ec04-196">Podczas kopiowania pliku z udziału toofile obiektów blob, [po stronie serwera kopii](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx) operacja została wykonana.</span><span class="sxs-lookup"><span data-stu-id="4ec04-196">When you copy a file from blob toofile share, a [server-side copy](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx) operation is performed.</span></span>

### <a name="synchronously-copy-files"></a><span data-ttu-id="4ec04-197">Synchronicznie kopiować pliki</span><span class="sxs-lookup"><span data-stu-id="4ec04-197">Synchronously copy files</span></span>
<span data-ttu-id="4ec04-198">Można określić hello `/SyncCopy` opcję toocopy danych z magazynu plików tooFile magazynu, z pliku magazynu tooBlob magazynu i z magazynu obiektów Blob tooFile magazynu synchronicznie, AzCopy przez pobieranie hello źródła danych toolocal pamięci i przekaż go ponownie toodestination.</span><span class="sxs-lookup"><span data-stu-id="4ec04-198">You can specify hello `/SyncCopy` option toocopy data from File Storage tooFile Storage, from File Storage tooBlob Storage and from Blob Storage tooFile Storage synchronously, AzCopy does this by downloading hello source data toolocal memory and upload it again toodestination.</span></span> <span data-ttu-id="4ec04-199">Wyjście standardowe koszt będą stosowane.</span><span class="sxs-lookup"><span data-stu-id="4ec04-199">Standard egress cost will apply.</span></span>

```azcopy
AzCopy /Source:https://myaccount1.file.core.windows.net/myfileshare1/ /Dest:https://myaccount2.file.core.windows.net/myfileshare2/ /SourceKey:key1 /DestKey:key2 /S /SyncCopy
```

<span data-ttu-id="4ec04-200">Podczas kopiowania z pliku magazynu tooBlob magazynu, typu obiektu blob domyślne hello jest blokowych obiektów blob, użytkownik może określić opcję `/BlobType:page` toochange hello docelowego obiektu blob.</span><span class="sxs-lookup"><span data-stu-id="4ec04-200">When copying from File Storage tooBlob Storage, hello default blob type is block blob, user can specify option `/BlobType:page` toochange hello destination blob type.</span></span>

<span data-ttu-id="4ec04-201">Należy pamiętać, że `/SyncCopy` może generować wyjście dodatkowych kosztów porównaniem kopiowania tooasynchronous, hello Zalecanym podejściem jest toouse maszyny Wirtualnej platformy Azure, który znajduje się w hello hello tej opcji, w tym samym regionie co koszt wyjście tooavoid konta magazynu źródłowego.</span><span class="sxs-lookup"><span data-stu-id="4ec04-201">Note that `/SyncCopy` might generate additional egress cost comparing tooasynchronous copy, hello recommended approach is toouse this option in hello Azure VM which is in hello same region as your source storage account tooavoid egress cost.</span></span>

## <a name="table-export"></a><span data-ttu-id="4ec04-202">Tabela: eksportowanie</span><span class="sxs-lookup"><span data-stu-id="4ec04-202">Table: Export</span></span>
### <a name="export-table"></a><span data-ttu-id="4ec04-203">Eksportowanie tabeli</span><span class="sxs-lookup"><span data-stu-id="4ec04-203">Export table</span></span>

```azcopy
AzCopy /Source:https://myaccount.table.core.windows.net/myTable/ /Dest:C:\myfolder\ /SourceKey:key
```

<span data-ttu-id="4ec04-204">Narzędzie AzCopy zapisuje folder docelowy określony toohello pliku manifestu.</span><span class="sxs-lookup"><span data-stu-id="4ec04-204">AzCopy writes a manifest file toohello specified destination folder.</span></span> <span data-ttu-id="4ec04-205">Plik manifestu Hello jest używany w hello importu procesu toolocate hello niezbędnych danych plików i sprawdzania poprawności danych.</span><span class="sxs-lookup"><span data-stu-id="4ec04-205">hello manifest file is used in hello import process toolocate hello necessary data files and perform data validation.</span></span> <span data-ttu-id="4ec04-206">Plik manifestu Hello korzysta z następującą konwencją domyślnie hello:</span><span class="sxs-lookup"><span data-stu-id="4ec04-206">hello manifest file uses hello following naming convention by default:</span></span>

    <account name>_<table name>_<timestamp>.manifest

<span data-ttu-id="4ec04-207">Użytkownik może również określić opcję hello `/Manifest:<manifest file name>` nazwa pliku manifestu hello tooset.</span><span class="sxs-lookup"><span data-stu-id="4ec04-207">User can also specify hello option `/Manifest:<manifest file name>` tooset hello manifest file name.</span></span>

```azcopy
AzCopy /Source:https://myaccount.table.core.windows.net/myTable/ /Dest:C:\myfolder\ /SourceKey:key /Manifest:abc.manifest
```

### <a name="split-export-into-multiple-files"></a><span data-ttu-id="4ec04-208">Eksport podzielonego na wiele plików</span><span class="sxs-lookup"><span data-stu-id="4ec04-208">Split export into multiple files</span></span>

```azcopy
AzCopy /Source:https://myaccount.table.core.windows.net/mytable/ /Dest:C:\myfolder /SourceKey:key /S /SplitSize:100
```

<span data-ttu-id="4ec04-209">Korzysta z narzędzia AzCopy *indeksu woluminu* w hello podział danych nazwę pliku toodistinguish wielu plików.</span><span class="sxs-lookup"><span data-stu-id="4ec04-209">AzCopy uses a *volume index* in hello split data file names toodistinguish multiple files.</span></span> <span data-ttu-id="4ec04-210">Indeks woluminu Hello składa się z dwóch części *indeksu zakresem kluczy partycji* i *podziału pliku indeksu*.</span><span class="sxs-lookup"><span data-stu-id="4ec04-210">hello volume index consists of two parts, a *partition key range index* and a *split file index*.</span></span> <span data-ttu-id="4ec04-211">Zarówno indeksy są liczony od zera.</span><span class="sxs-lookup"><span data-stu-id="4ec04-211">Both indexes are zero-based.</span></span>

<span data-ttu-id="4ec04-212">Indeks zakresem kluczy partycji Hello będzie równa 0, jeśli użytkownik nie określi opcji `/PKRS`.</span><span class="sxs-lookup"><span data-stu-id="4ec04-212">hello partition key range index will be 0 if user does not specify option `/PKRS`.</span></span>

<span data-ttu-id="4ec04-213">Na przykład, załóżmy, że AzCopy generuje dwa pliki danych po hello użytkownika określa opcję `/SplitSize`.</span><span class="sxs-lookup"><span data-stu-id="4ec04-213">For instance, suppose AzCopy generates two data files after hello user specifies option `/SplitSize`.</span></span> <span data-ttu-id="4ec04-214">Witaj wynikowa nazwy pliku danych może być:</span><span class="sxs-lookup"><span data-stu-id="4ec04-214">hello resulting data file names might be:</span></span>

    myaccount_mytable_20140903T051850.8128447Z_0_0_C3040FE8.json
    myaccount_mytable_20140903T051850.8128447Z_0_1_0AB9AC20.json

<span data-ttu-id="4ec04-215">Należy pamiętać, że hello minimalnej możliwej wartości dla opcji `/SplitSize` wynosi 32 MB.</span><span class="sxs-lookup"><span data-stu-id="4ec04-215">Note that hello minimum possible value for option `/SplitSize` is 32MB.</span></span> <span data-ttu-id="4ec04-216">Jeśli hello określone miejsce docelowe jest magazyn obiektów Blob, AzCopy będzie podzielić hello danych pliku po jego rozmiary osiągnie hello blob limit rozmiaru (200GB), niezależnie od tego, czy opcja `/SplitSize` został określony przez użytkownika hello.</span><span class="sxs-lookup"><span data-stu-id="4ec04-216">If hello specified destination is Blob storage, AzCopy will split hello data file once its sizes reaches hello blob size limitation (200GB), regardless of whether option `/SplitSize` has been specified by hello user.</span></span>

### <a name="export-table-toojson-or-csv-data-file-format"></a><span data-ttu-id="4ec04-217">Eksportowanie tabeli tooJSON lub dane w formacie pliku CSV</span><span class="sxs-lookup"><span data-stu-id="4ec04-217">Export table tooJSON or CSV data file format</span></span>
<span data-ttu-id="4ec04-218">Narzędzie AzCopy domyślnie eksportuje pliki danych tooJSON tabel.</span><span class="sxs-lookup"><span data-stu-id="4ec04-218">AzCopy by default exports tables tooJSON data files.</span></span> <span data-ttu-id="4ec04-219">Można określić opcję hello `/PayloadFormat:JSON|CSV` tabele hello tooexport jako JSON lub CSV.</span><span class="sxs-lookup"><span data-stu-id="4ec04-219">You can specify hello option `/PayloadFormat:JSON|CSV` tooexport hello tables as JSON or CSV.</span></span>

```azcopy
AzCopy /Source:https://myaccount.table.core.windows.net/myTable/ /Dest:C:\myfolder\ /SourceKey:key /PayloadFormat:CSV
```

<span data-ttu-id="4ec04-220">Podczas określania format ładunku hello CSV, AzCopy również wygeneruje plik schematu z rozszerzeniem pliku `.schema.csv` dla każdego pliku danych.</span><span class="sxs-lookup"><span data-stu-id="4ec04-220">When specifying hello CSV payload format, AzCopy will also generate a schema file with file extension `.schema.csv` for each data file.</span></span>

### <a name="export-table-entities-concurrently"></a><span data-ttu-id="4ec04-221">Eksportowanie tabeli jednocześnie jednostek</span><span class="sxs-lookup"><span data-stu-id="4ec04-221">Export table entities concurrently</span></span>

```azcopy
AzCopy /Source:https://myaccount.table.core.windows.net/myTable/ /Dest:C:\myfolder\ /SourceKey:key /PKRS:"aa#bb"
```

<span data-ttu-id="4ec04-222">AzCopy rozpocznie jednostek tooexport jednoczesnych operacji po opcji przez użytkownika hello `/PKRS`.</span><span class="sxs-lookup"><span data-stu-id="4ec04-222">AzCopy will start concurrent operations tooexport entities when hello user specifies option `/PKRS`.</span></span> <span data-ttu-id="4ec04-223">Każda operacja eksportuje jednym zakresem kluczy partycji.</span><span class="sxs-lookup"><span data-stu-id="4ec04-223">Each operation exports one partition key range.</span></span>

<span data-ttu-id="4ec04-224">Należy pamiętać, że hello liczba jednoczesnych operacji również jest kontrolowane przez opcję `/NC`.</span><span class="sxs-lookup"><span data-stu-id="4ec04-224">Note that hello number of concurrent operations is also controlled by option `/NC`.</span></span> <span data-ttu-id="4ec04-225">AzCopy używa hello liczba rdzeni procesorów jako wartość domyślną hello `/NC` podczas kopiowania jednostek tabeli, nawet jeśli `/NC` nie została określona.</span><span class="sxs-lookup"><span data-stu-id="4ec04-225">AzCopy uses hello number of core processors as hello default value of `/NC` when copying table entities, even if `/NC` was not specified.</span></span> <span data-ttu-id="4ec04-226">Gdy użytkownik hello Określa opcję `/PKRS`, AzCopy używa hello mniejszych Witaj dwie wartości - partycji zakresami kluczy i określona jawnie lub niejawnie jednoczesnych operacji - toodetermine hello liczby jednoczesnych operacji toostart.</span><span class="sxs-lookup"><span data-stu-id="4ec04-226">When hello user specifies option `/PKRS`, AzCopy uses hello smaller of hello two values - partition key ranges versus implicitly or explicitly specified concurrent operations - toodetermine hello number of concurrent operations toostart.</span></span> <span data-ttu-id="4ec04-227">Aby uzyskać więcej informacji, wpisz `AzCopy /?:NC` hello wiersza polecenia.</span><span class="sxs-lookup"><span data-stu-id="4ec04-227">For more details, type `AzCopy /?:NC` at hello command line.</span></span>

### <a name="export-table-tooblob"></a><span data-ttu-id="4ec04-228">Eksportowanie tabeli tooblob</span><span class="sxs-lookup"><span data-stu-id="4ec04-228">Export table tooblob</span></span>

```azcopy
AzCopy /Source:https://myaccount.table.core.windows.net/myTable/ /Dest:https://myaccount.blob.core.windows.net/mycontainer/ /SourceKey:key1 /Destkey:key2
```

<span data-ttu-id="4ec04-229">Narzędzie AzCopy wygeneruje plik danych JSON do kontenera obiektów blob hello z następującą konwencją:</span><span class="sxs-lookup"><span data-stu-id="4ec04-229">AzCopy will generate a JSON data file into hello blob container with following naming convention:</span></span>

    <account name>_<table name>_<timestamp>_<volume index>_<CRC>.json

<span data-ttu-id="4ec04-230">plik danych JSON Hello wygenerowany w formacie hello ładunku dla minimalne metadane.</span><span class="sxs-lookup"><span data-stu-id="4ec04-230">hello generated JSON data file follows hello payload format for minimal metadata.</span></span> <span data-ttu-id="4ec04-231">Aby uzyskać więcej informacji na ten format ładunku, zobacz [Format ładunku dla operacji usługi tabeli](http://msdn.microsoft.com/library/azure/dn535600.aspx).</span><span class="sxs-lookup"><span data-stu-id="4ec04-231">For details on this payload format, see [Payload Format for Table Service Operations](http://msdn.microsoft.com/library/azure/dn535600.aspx).</span></span>

<span data-ttu-id="4ec04-232">Należy pamiętać, że podczas eksportowania tooblobs tabel, AzCopy będzie Pobierz hello tabeli jednostek toolocal tymczasowe pliki danych, a następnie przekaż blob toohello tych jednostek.</span><span class="sxs-lookup"><span data-stu-id="4ec04-232">Note that when exporting tables tooblobs, AzCopy will download hello Table entities toolocal temporary data files and then upload those entities toohello blob.</span></span> <span data-ttu-id="4ec04-233">Te dane tymczasowe pliki są umieszczane w folderze dziennika hello o hello domyślnej ścieżki "<code>%LocalAppData%\Microsoft\Azure\AzCopy</code>", można określić opcję/toochange [arkusza pliku folder] Z: hello folder plików dziennika i w związku z tym zmienić lokalizację plików tymczasowych danych hello.</span><span class="sxs-lookup"><span data-stu-id="4ec04-233">These temporary data files are put into hello journal file folder with hello default path "<code>%LocalAppData%\Microsoft\Azure\AzCopy</code>", you can specify option /Z:[journal-file-folder] toochange hello journal file folder location and thus change hello temporary data files location.</span></span> <span data-ttu-id="4ec04-234">Hello dane tymczasowe, które rozmiaru plików zadecyduje o jednostek tabeli i rozmiar hello, określony /SplitSize opcji hello, chociaż plik danych tymczasowych hello dysku lokalnego jest usuwany natychmiast po został przekazany toohello obiektów blob, upewnij się, zostanie te dane tymczasowe pliki przed usunięciem ma za mało toostore miejsca na dysku lokalnym.</span><span class="sxs-lookup"><span data-stu-id="4ec04-234">hello temporary data files' size is decided by your table entities' size and hello size you specified with hello option /SplitSize, although hello temporary data file in local disk will be deleted instantly once it has been uploaded toohello blob, please make sure you have enough local disk space toostore these temporary data files before they are deleted.</span></span>

## <a name="table-import"></a><span data-ttu-id="4ec04-235">Tabela: Import</span><span class="sxs-lookup"><span data-stu-id="4ec04-235">Table: Import</span></span>
### <a name="import-table"></a><span data-ttu-id="4ec04-236">Importowanie tabeli</span><span class="sxs-lookup"><span data-stu-id="4ec04-236">Import table</span></span>

```azcopy
AzCopy /Source:C:\myfolder\ /Dest:https://myaccount.table.core.windows.net/mytable1/ /DestKey:key /Manifest:"myaccount_mytable_20140103T112020.manifest" /EntityOperation:InsertOrReplace
```

<span data-ttu-id="4ec04-237">Witaj opcja `/EntityOperation` wskazuje sposób jednostek tooinsert do hello tabeli.</span><span class="sxs-lookup"><span data-stu-id="4ec04-237">hello option `/EntityOperation` indicates how tooinsert entities into hello table.</span></span> <span data-ttu-id="4ec04-238">Możliwe wartości:</span><span class="sxs-lookup"><span data-stu-id="4ec04-238">Possible values are:</span></span>

* <span data-ttu-id="4ec04-239">`InsertOrSkip`: Pomija istniejącej jednostki lub wstawia nową jednostkę, jeśli nie istnieje w tabeli hello.</span><span class="sxs-lookup"><span data-stu-id="4ec04-239">`InsertOrSkip`: Skips an existing entity or inserts a new entity if it does not exist in hello table.</span></span>
* <span data-ttu-id="4ec04-240">`InsertOrMerge`: Scala istniejącej jednostki lub wstawia nową jednostkę, jeśli nie istnieje w tabeli hello.</span><span class="sxs-lookup"><span data-stu-id="4ec04-240">`InsertOrMerge`: Merges an existing entity or inserts a new entity if it does not exist in hello table.</span></span>
* <span data-ttu-id="4ec04-241">`InsertOrReplace`: Zastępuje istniejące jednostki i wstawia nową jednostkę, jeśli nie istnieje w tabeli hello.</span><span class="sxs-lookup"><span data-stu-id="4ec04-241">`InsertOrReplace`: Replaces an existing entity or inserts a new entity if it does not exist in hello table.</span></span>

<span data-ttu-id="4ec04-242">Zauważ, że nie można określić opcji `/PKRS` w scenariuszu importu hello.</span><span class="sxs-lookup"><span data-stu-id="4ec04-242">Note that you cannot specify option `/PKRS` in hello import scenario.</span></span> <span data-ttu-id="4ec04-243">W odróżnieniu od hello eksportu scenariusz, w którym należy określić opcję `/PKRS` toostart jednoczesnych operacji AzCopy domyślnie rozpocznie jednoczesnych operacji importowania tabeli.</span><span class="sxs-lookup"><span data-stu-id="4ec04-243">Unlike hello export scenario, in which you must specify option `/PKRS` toostart concurrent operations, AzCopy will by default start concurrent operations when you import a table.</span></span> <span data-ttu-id="4ec04-244">Hello domyślna liczba jednoczesnych operacji uruchomiona jest równy toohello liczba procesorów; jednak można określić różne liczby równoczesnych z opcją `/NC`.</span><span class="sxs-lookup"><span data-stu-id="4ec04-244">hello default number of concurrent operations started is equal toohello number of core processors; however, you can specify a different number of concurrent with option `/NC`.</span></span> <span data-ttu-id="4ec04-245">Aby uzyskać więcej informacji, wpisz `AzCopy /?:NC` hello wiersza polecenia.</span><span class="sxs-lookup"><span data-stu-id="4ec04-245">For more details, type `AzCopy /?:NC` at hello command line.</span></span>

<span data-ttu-id="4ec04-246">Należy pamiętać, że narzędzie AzCopy obsługuje wyłącznie importowanie do formatu JSON, CSV nie.</span><span class="sxs-lookup"><span data-stu-id="4ec04-246">Note that AzCopy only supports importing for JSON, not CSV.</span></span> <span data-ttu-id="4ec04-247">AzCopy nie obsługuje importowania tabeli z JSON utworzonych przez użytkownika i pliki manifestu.</span><span class="sxs-lookup"><span data-stu-id="4ec04-247">AzCopy does not support table imports from user-created JSON and manifest files.</span></span> <span data-ttu-id="4ec04-248">Oba te pliki muszą pochodzić z narzędzia AzCopy tabeli eksportu.</span><span class="sxs-lookup"><span data-stu-id="4ec04-248">Both of these files must come from an AzCopy table export.</span></span> <span data-ttu-id="4ec04-249">błędy tooavoid nie Modyfikuj hello wyeksportowane JSON lub pliku manifestu.</span><span class="sxs-lookup"><span data-stu-id="4ec04-249">tooavoid errors, please do not modify hello exported JSON or manifest file.</span></span>

### <a name="import-entities-tootable-using-blobs"></a><span data-ttu-id="4ec04-250">Importowanie jednostek tootable przy użyciu obiektów blob</span><span class="sxs-lookup"><span data-stu-id="4ec04-250">Import entities tootable using blobs</span></span>
<span data-ttu-id="4ec04-251">Założono kontenera obiektów Blob zawiera następujące hello: plik A JSON reprezentujący tabel Azure i jego towarzyszący plik manifestu.</span><span class="sxs-lookup"><span data-stu-id="4ec04-251">Assume a Blob container contains hello following: A JSON file representing an Azure Table and its accompanying manifest file.</span></span>

    myaccount_mytable_20140103T112020.manifest
    myaccount_mytable_20140103T112020_0_0_0AF395F1DC42E952.json

<span data-ttu-id="4ec04-252">Można uruchomić powitania po polecenie tooimport jednostek do tabeli za pomocą pliku manifestu hello w danym kontenerze obiektów blob:</span><span class="sxs-lookup"><span data-stu-id="4ec04-252">You can run hello following command tooimport entities into a table using hello manifest file in that blob container:</span></span>

```azcopy
AzCopy /Source:https://myaccount.blob.core.windows.net/mycontainer /Dest:https://myaccount.table.core.windows.net/mytable /SourceKey:key1 /DestKey:key2 /Manifest:"myaccount_mytable_20140103T112020.manifest" /EntityOperation:"InsertOrReplace"
```

## <a name="other-azcopy-features"></a><span data-ttu-id="4ec04-253">Inne funkcje AzCopy</span><span class="sxs-lookup"><span data-stu-id="4ec04-253">Other AzCopy features</span></span>
### <a name="only-copy-data-that-doesnt-exist-in-hello-destination"></a><span data-ttu-id="4ec04-254">Tylko skopiować dane, które nie istnieje w docelowym hello</span><span class="sxs-lookup"><span data-stu-id="4ec04-254">Only copy data that doesn't exist in hello destination</span></span>
<span data-ttu-id="4ec04-255">Witaj `/XO` i `/XN` parametrów pozwalają tooexclude starszej lub nowszej źródła zasobów zapobiega kopiowaniu odpowiednio.</span><span class="sxs-lookup"><span data-stu-id="4ec04-255">hello `/XO` and `/XN` parameters allow you tooexclude older or newer source resources from being copied, respectively.</span></span> <span data-ttu-id="4ec04-256">Jeśli chcesz tylko toocopy źródła zasobów, które nie istnieje w docelowym hello, można określić obu tych parametrów w hello polecenia programu AzCopy:</span><span class="sxs-lookup"><span data-stu-id="4ec04-256">If you only want toocopy source resources that don't exist in hello destination, you can specify both parameters in hello AzCopy command:</span></span>

    /Source:http://myaccount.blob.core.windows.net/mycontainer /Dest:C:\myfolder /SourceKey:<sourcekey> /S /XO /XN

    /Source:C:\myfolder /Dest:http://myaccount.file.core.windows.net/myfileshare /DestKey:<destkey> /S /XO /XN

    /Source:http://myaccount.blob.core.windows.net/mycontainer /Dest:http://myaccount.blob.core.windows.net/mycontainer1 /SourceKey:<sourcekey> /DestKey:<destkey> /S /XO /XN

<span data-ttu-id="4ec04-257">Należy pamiętać, że to nie jest obsługiwana podczas hello źródłowe lub docelowe jest tabelą.</span><span class="sxs-lookup"><span data-stu-id="4ec04-257">Note that this is not supported when either hello source or destination is a table.</span></span>

### <a name="use-a-response-file-toospecify-command-line-parameters"></a><span data-ttu-id="4ec04-258">Użyj parametrów pliku odpowiedzi toospecify wiersza polecenia</span><span class="sxs-lookup"><span data-stu-id="4ec04-258">Use a response file toospecify command-line parameters</span></span>

```azcopy
AzCopy /@:"C:\responsefiles\copyoperation.txt"
```

<span data-ttu-id="4ec04-259">Parametry wiersza polecenia AzCopy można umieścić w pliku odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="4ec04-259">You can include any AzCopy command-line parameters in a response file.</span></span> <span data-ttu-id="4ec04-260">Procesy AzCopy hello parametrów w pliku hello tak, jakby były one określone w wierszu polecenia hello, wykonywanie bezpośrednich podstawienia z zawartością hello hello pliku.</span><span class="sxs-lookup"><span data-stu-id="4ec04-260">AzCopy processes hello parameters in hello file as if they had been specified on hello command line, performing a direct substitution with hello contents of hello file.</span></span>

<span data-ttu-id="4ec04-261">Załóżmy plik odpowiedzi o nazwie `copyoperation.txt`, który zawiera następujące wiersze hello.</span><span class="sxs-lookup"><span data-stu-id="4ec04-261">Assume a response file named `copyoperation.txt`, that contains hello following lines.</span></span> <span data-ttu-id="4ec04-262">Każdy parametr narzędzia AzCopy można określić w jednym wierszu</span><span class="sxs-lookup"><span data-stu-id="4ec04-262">Each AzCopy parameter can be specified on a single line</span></span>

    /Source:http://myaccount.blob.core.windows.net/mycontainer /Dest:C:\myfolder /SourceKey:<sourcekey> /S /Y

<span data-ttu-id="4ec04-263">lub na oddzielnych wierszach:</span><span class="sxs-lookup"><span data-stu-id="4ec04-263">or on separate lines:</span></span>

    /Source:http://myaccount.blob.core.windows.net/mycontainer
    /Dest:C:\myfolder
    /SourceKey:<sourcekey>
    /S
    /Y

<span data-ttu-id="4ec04-264">Narzędzie AzCopy zakończy się niepowodzeniem, jeśli parametr hello można podzielić na dwa wiersze, jak pokazano poniżej, aby uzyskać hello `/sourcekey` parametru:</span><span class="sxs-lookup"><span data-stu-id="4ec04-264">AzCopy will fail if you split hello parameter across two lines, as shown here for hello `/sourcekey` parameter:</span></span>

    http://myaccount.blob.core.windows.net/mycontainer
     C:\myfolder
    /sourcekey:
    <sourcekey>
    /S
    /Y

### <a name="use-multiple-response-files-toospecify-command-line-parameters"></a><span data-ttu-id="4ec04-265">Użyj wielu odpowiedzi plików toospecify parametry wiersza polecenia</span><span class="sxs-lookup"><span data-stu-id="4ec04-265">Use multiple response files toospecify command-line parameters</span></span>
<span data-ttu-id="4ec04-266">Załóżmy, plik odpowiedzi o nazwie `source.txt` , który określa kontener źródła:</span><span class="sxs-lookup"><span data-stu-id="4ec04-266">Assume a response file named `source.txt` that specifies a source container:</span></span>

    /Source:http://myaccount.blob.core.windows.net/mycontainer

<span data-ttu-id="4ec04-267">I plik odpowiedzi o nazwie `dest.txt` określający folderu docelowego w systemie plików hello:</span><span class="sxs-lookup"><span data-stu-id="4ec04-267">And a response file named `dest.txt` that specifies a destination folder in hello file system:</span></span>

    /Dest:C:\myfolder

<span data-ttu-id="4ec04-268">I plik odpowiedzi o nazwie `options.txt` , który określa opcje narzędzia AzCopy:</span><span class="sxs-lookup"><span data-stu-id="4ec04-268">And a response file named `options.txt` that specifies options for AzCopy:</span></span>

    /S /Y

<span data-ttu-id="4ec04-269">toocall AzCopy z tych plików odpowiedzi, które znajdują się w katalogu `C:\responsefiles`, użyj tego polecenia:</span><span class="sxs-lookup"><span data-stu-id="4ec04-269">toocall AzCopy with these response files, all of which reside in a directory `C:\responsefiles`, use this command:</span></span>

```azcopy
AzCopy /@:"C:\responsefiles\source.txt" /@:"C:\responsefiles\dest.txt" /SourceKey:<sourcekey> /@:"C:\responsefiles\options.txt"   
```

<span data-ttu-id="4ec04-270">Narzędzie AzCopy przetwarza to polecenie tak samo, jak gdyby uwzględnione wszystkie parametry poszczególnych hello hello w wierszu polecenia:</span><span class="sxs-lookup"><span data-stu-id="4ec04-270">AzCopy processes this command just as it would if you included all of hello individual parameters on hello command line:</span></span>

```azcopy
AzCopy /Source:http://myaccount.blob.core.windows.net/mycontainer /Dest:C:\myfolder /SourceKey:<sourcekey> /S /Y
```

### <a name="specify-a-shared-access-signature-sas"></a><span data-ttu-id="4ec04-271">Określ sygnatury dostępu współdzielonego (SAS)</span><span class="sxs-lookup"><span data-stu-id="4ec04-271">Specify a shared access signature (SAS)</span></span>

```azcopy
AzCopy /Source:https://myaccount.blob.core.windows.net/mycontainer1 /Dest:https://myaccount.blob.core.windows.net/mycontainer2 /SourceSAS:SAS1 /DestSAS:SAS2 /Pattern:abc.txt
```

<span data-ttu-id="4ec04-272">Można również określić sygnatury dostępu Współdzielonego w kontenerze hello identyfikatora URI:</span><span class="sxs-lookup"><span data-stu-id="4ec04-272">You can also specify a SAS on hello container URI:</span></span>

```azcopy
AzCopy /Source:https://myaccount.blob.core.windows.net/mycontainer1/?SourceSASToken /Dest:C:\myfolder /S
```

### <a name="journal-file-folder"></a><span data-ttu-id="4ec04-273">Folder plików dziennika</span><span class="sxs-lookup"><span data-stu-id="4ec04-273">Journal file folder</span></span>
<span data-ttu-id="4ec04-274">Zawsze, gdy wystawiać tooAzCopy polecenia, sprawdza czy istnieje plik dziennika w folderze domyślnym hello, lub czy istnieje w folderze określonej za pomocą tej opcji.</span><span class="sxs-lookup"><span data-stu-id="4ec04-274">Each time you issue a command tooAzCopy, it checks whether a journal file exists in hello default folder, or whether it exists in a folder that you specified via this option.</span></span> <span data-ttu-id="4ec04-275">Jeśli plik dziennika hello nie istnieje w każdym miejscu, AzCopy traktuje operacji hello jako nowy i generuje nowy plik dziennika.</span><span class="sxs-lookup"><span data-stu-id="4ec04-275">If hello journal file does not exist in either place, AzCopy treats hello operation as new and generates a new journal file.</span></span>

<span data-ttu-id="4ec04-276">Jeśli istnieje plik dziennika hello, AzCopy sprawdzi, czy hello wiersza polecenia, które możesz wpisać zgodny hello wiersza polecenia w pliku dziennika hello.</span><span class="sxs-lookup"><span data-stu-id="4ec04-276">If hello journal file does exist, AzCopy will check whether hello command line that you input matches hello command line in hello journal file.</span></span> <span data-ttu-id="4ec04-277">Jeśli dwa wiersze polecenia hello są zgodne, AzCopy wznawia hello nieukończone działania.</span><span class="sxs-lookup"><span data-stu-id="4ec04-277">If hello two command lines match, AzCopy resumes hello incomplete operation.</span></span> <span data-ttu-id="4ec04-278">Jeśli nie są zgodne, będzie zostanie wyświetlony monit o tooeither Zastąp hello dziennika pliku toostart nowej operacji lub toocancel hello bieżącej operacji.</span><span class="sxs-lookup"><span data-stu-id="4ec04-278">If they do not match, you will be prompted tooeither overwrite hello journal file toostart a new operation, or toocancel hello current operation.</span></span>

<span data-ttu-id="4ec04-279">Jeśli chcesz, aby toouse hello domyślna lokalizacja pliku dziennika hello:</span><span class="sxs-lookup"><span data-stu-id="4ec04-279">If you want toouse hello default location for hello journal file:</span></span>

```azcopy
AzCopy /Source:C:\myfolder /Dest:https://myaccount.blob.core.windows.net/mycontainer /DestKey:key /Z
```

<span data-ttu-id="4ec04-280">Jeśli pominięto opcję `/Z`, lub określ opcję `/Z` bez ścieżki folderu hello, jak pokazano powyżej, AzCopy tworzy plik dziennika hello w hello domyślnej lokalizacji, która jest `%SystemDrive%\Users\%username%\AppData\Local\Microsoft\Azure\AzCopy`.</span><span class="sxs-lookup"><span data-stu-id="4ec04-280">If you omit option `/Z`, or specify option `/Z` without hello folder path, as shown above, AzCopy creates hello journal file in hello default location, which is `%SystemDrive%\Users\%username%\AppData\Local\Microsoft\Azure\AzCopy`.</span></span> <span data-ttu-id="4ec04-281">Jeśli plik dziennika hello już istnieje, AzCopy wznawia operację hello na podstawie hello pliku dziennika.</span><span class="sxs-lookup"><span data-stu-id="4ec04-281">If hello journal file already exists, then AzCopy resumes hello operation based on hello journal file.</span></span>

<span data-ttu-id="4ec04-282">Jeśli chcesz, aby toospecify niestandardową lokalizację pliku dziennika hello:</span><span class="sxs-lookup"><span data-stu-id="4ec04-282">If you want toospecify a custom location for hello journal file:</span></span>

```azcopy
AzCopy /Source:C:\myfolder /Dest:https://myaccount.blob.core.windows.net/mycontainer /DestKey:key /Z:C:\journalfolder\
```

<span data-ttu-id="4ec04-283">W tym przykładzie tworzy plik dziennika hello, jeśli jeszcze nie istnieje.</span><span class="sxs-lookup"><span data-stu-id="4ec04-283">This example creates hello journal file if it does not already exist.</span></span> <span data-ttu-id="4ec04-284">Jeśli istnieje, narzędzie AzCopy wznawia operacji hello na podstawie hello pliku dziennika.</span><span class="sxs-lookup"><span data-stu-id="4ec04-284">If it does exist, then AzCopy resumes hello operation based on hello journal file.</span></span>

<span data-ttu-id="4ec04-285">Jeśli chcesz, aby tooresume operacji AzCopy:</span><span class="sxs-lookup"><span data-stu-id="4ec04-285">If you want tooresume an AzCopy operation:</span></span>

```azcopy
AzCopy /Z:C:\journalfolder\
```

<span data-ttu-id="4ec04-286">W tym przykładzie wznawia hello ostatniej operacji, które toocomplete zakończyła się niepowodzeniem.</span><span class="sxs-lookup"><span data-stu-id="4ec04-286">This example resumes hello last operation, which may have failed toocomplete.</span></span>

### <a name="generate-a-log-file"></a><span data-ttu-id="4ec04-287">Wygenerowanie pliku dziennika</span><span class="sxs-lookup"><span data-stu-id="4ec04-287">Generate a log file</span></span>

```azcopy
AzCopy /Source:C:\myfolder /Dest:https://myaccount.blob.core.windows.net/mycontainer /DestKey:key /V
```

<span data-ttu-id="4ec04-288">Jeśli określono opcję `/V` bez podawania pliku dziennika pełne ścieżki toohello, następnie AzCopy tworzy plik dziennika hello w hello domyślnej lokalizacji, która jest `%SystemDrive%\Users\%username%\AppData\Local\Microsoft\Azure\AzCopy`.</span><span class="sxs-lookup"><span data-stu-id="4ec04-288">If you specify option `/V` without providing a file path toohello verbose log, then AzCopy creates hello log file in hello default location, which is `%SystemDrive%\Users\%username%\AppData\Local\Microsoft\Azure\AzCopy`.</span></span>

<span data-ttu-id="4ec04-289">W przeciwnym razie należy utworzyć plik dziennika w lokalizacji niestandardowej:</span><span class="sxs-lookup"><span data-stu-id="4ec04-289">Otherwise, you can create an log file in a custom location:</span></span>

```azcopy
AzCopy /Source:C:\myfolder /Dest:https://myaccount.blob.core.windows.net/mycontainer /DestKey:key /V:C:\myfolder\azcopy1.log
```

<span data-ttu-id="4ec04-290">Należy pamiętać, że jeśli Określ ścieżkę względną po opcji `/V`, takich jak `/V:test/azcopy1.log`, a następnie hello pełnego dziennika jest tworzony w bieżącym katalogu roboczym hello w podfolderze o nazwie `test`.</span><span class="sxs-lookup"><span data-stu-id="4ec04-290">Note that if you specify a relative path following option `/V`, such as `/V:test/azcopy1.log`, then hello verbose log is created in hello current working directory within a subfolder named `test`.</span></span>

### <a name="specify-hello-number-of-concurrent-operations-toostart"></a><span data-ttu-id="4ec04-291">Określ liczbę hello toostart jednoczesnych operacji</span><span class="sxs-lookup"><span data-stu-id="4ec04-291">Specify hello number of concurrent operations toostart</span></span>
<span data-ttu-id="4ec04-292">Opcja `/NC` określa liczbę hello operacje kopiowania współbieżnych.</span><span class="sxs-lookup"><span data-stu-id="4ec04-292">Option `/NC` specifies hello number of concurrent copy operations.</span></span> <span data-ttu-id="4ec04-293">Domyślnie narzędzie AzCopy uruchamia określoną liczbę jednoczesnych operacji tooincrease hello danych przeniesienie przepływności.</span><span class="sxs-lookup"><span data-stu-id="4ec04-293">By default, AzCopy starts a certain number of concurrent operations tooincrease hello data transfer throughput.</span></span> <span data-ttu-id="4ec04-294">Dla operacji tabeli hello liczba jednoczesnych operacji jest równy toohello liczbę procesorów, które masz.</span><span class="sxs-lookup"><span data-stu-id="4ec04-294">For Table operations, hello number of concurrent operations is equal toohello number of processors you have.</span></span> <span data-ttu-id="4ec04-295">Dla operacji obiektu Blob i plik hello liczba jednoczesnych operacji jest równa 8 godzin hello liczbę procesorów, które masz.</span><span class="sxs-lookup"><span data-stu-id="4ec04-295">For Blob and File operations, hello number of concurrent operations is equal 8 times hello number of processors you have.</span></span> <span data-ttu-id="4ec04-296">Jeśli używasz narzędzia AzCopy w niskiej przepustowości sieci, można określić mniejszą liczbę /NC tooavoid niepowodzenia spowodowane konkurencji zasobów.</span><span class="sxs-lookup"><span data-stu-id="4ec04-296">If you are running AzCopy across a low-bandwidth network, you can specify a lower number for /NC tooavoid failure caused by resource competition.</span></span>

### <a name="run-azcopy-against-azure-storage-emulator"></a><span data-ttu-id="4ec04-297">Uruchom narzędzie AzCopy dla emulatora magazynu Azure</span><span class="sxs-lookup"><span data-stu-id="4ec04-297">Run AzCopy against Azure Storage Emulator</span></span>
<span data-ttu-id="4ec04-298">Możesz uruchamiać narzędzia AzCopy na powitania [emulatora magazynu Azure](storage-use-emulator.md) dla obiektów blob:</span><span class="sxs-lookup"><span data-stu-id="4ec04-298">You can run AzCopy against hello [Azure Storage Emulator](storage-use-emulator.md) for Blobs:</span></span>

```azcopy
AzCopy /Source:https://127.0.0.1:10000/myaccount/mycontainer/ /Dest:C:\myfolder /SourceKey:key /SourceType:Blob /S
```

<span data-ttu-id="4ec04-299">i tabele:</span><span class="sxs-lookup"><span data-stu-id="4ec04-299">and Tables:</span></span>

```azcopy
AzCopy /Source:https://127.0.0.1:10002/myaccount/mytable/ /Dest:C:\myfolder /SourceKey:key /SourceType:Table
```

## <a name="azcopy-parameters"></a><span data-ttu-id="4ec04-300">Parametry AzCopy</span><span class="sxs-lookup"><span data-stu-id="4ec04-300">AzCopy Parameters</span></span>
<span data-ttu-id="4ec04-301">Poniżej opisano parametry narzędzia AzCopy.</span><span class="sxs-lookup"><span data-stu-id="4ec04-301">Parameters for AzCopy are described below.</span></span> <span data-ttu-id="4ec04-302">Możesz także wpisać jedną z poniższych poleceń z wiersza polecenia hello, aby uzyskać pomoc przy użyciu narzędzia AzCopy hello:</span><span class="sxs-lookup"><span data-stu-id="4ec04-302">You can also type one of hello following commands from hello command line for help in using AzCopy:</span></span>

* <span data-ttu-id="4ec04-303">Aby uzyskać szczegółową pomoc wiersza polecenia AzCopy:`AzCopy /?`</span><span class="sxs-lookup"><span data-stu-id="4ec04-303">For detailed command-line help for AzCopy: `AzCopy /?`</span></span>
* <span data-ttu-id="4ec04-304">Szczegółowe informacje o żadnych parametrów narzędzia AzCopy:`AzCopy /?:SourceKey`</span><span class="sxs-lookup"><span data-stu-id="4ec04-304">For detailed help with any AzCopy parameter: `AzCopy /?:SourceKey`</span></span>
* <span data-ttu-id="4ec04-305">Przykłady wiersza polecenia:`AzCopy /?:Samples`</span><span class="sxs-lookup"><span data-stu-id="4ec04-305">For command-line examples: `AzCopy /?:Samples`</span></span>

### <a name="sourcesource"></a><span data-ttu-id="4ec04-306">/ Źródła: "source"</span><span class="sxs-lookup"><span data-stu-id="4ec04-306">/Source:"source"</span></span>
<span data-ttu-id="4ec04-307">Określa hello źródła danych z którego toocopy.</span><span class="sxs-lookup"><span data-stu-id="4ec04-307">Specifies hello source data from which toocopy.</span></span> <span data-ttu-id="4ec04-308">Źródło Hello może być katalogu w systemie plików, kontenera obiektów blob, katalog wirtualny obiektów blob, udział pliku magazynu, katalog pliku magazynu lub tabeli platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="4ec04-308">hello source can be a file system directory, a blob container, a blob virtual directory, a storage file share, a storage file directory, or an Azure table.</span></span>

<span data-ttu-id="4ec04-309">**Dotyczy:** obiektów blob, plików, tabel</span><span class="sxs-lookup"><span data-stu-id="4ec04-309">**Applicable to:** Blobs, Files, Tables</span></span>

### <a name="destdestination"></a><span data-ttu-id="4ec04-310">/ Dest: "miejsce docelowe"</span><span class="sxs-lookup"><span data-stu-id="4ec04-310">/Dest:"destination"</span></span>
<span data-ttu-id="4ec04-311">Określa hello toocopy docelowego do.</span><span class="sxs-lookup"><span data-stu-id="4ec04-311">Specifies hello destination toocopy to.</span></span> <span data-ttu-id="4ec04-312">Hello docelowym może być katalogu w systemie plików, kontenera obiektów blob, katalog wirtualny obiektów blob, udział pliku magazynu, katalog pliku magazynu lub tabeli platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="4ec04-312">hello destination can be a file system directory, a blob container, a blob virtual directory, a storage file share, a storage file directory, or an Azure table.</span></span>

<span data-ttu-id="4ec04-313">**Dotyczy:** obiektów blob, plików, tabel</span><span class="sxs-lookup"><span data-stu-id="4ec04-313">**Applicable to:** Blobs, Files, Tables</span></span>

### <a name="patternfile-pattern"></a><span data-ttu-id="4ec04-314">/ Wzorca: "wzorzec pliku"</span><span class="sxs-lookup"><span data-stu-id="4ec04-314">/Pattern:"file-pattern"</span></span>
<span data-ttu-id="4ec04-315">Określa wzorzec pliku, która wskazuje, które toocopy pliki.</span><span class="sxs-lookup"><span data-stu-id="4ec04-315">Specifies a file pattern that indicates which files toocopy.</span></span> <span data-ttu-id="4ec04-316">zachowanie Hello hello /Pattern parametru zależy od lokalizacji hello hello źródła danych i hello obecność cyklicznego hello w trybie.</span><span class="sxs-lookup"><span data-stu-id="4ec04-316">hello behavior of hello /Pattern parameter is determined by hello location of hello source data, and hello presence of hello recursive mode option.</span></span> <span data-ttu-id="4ec04-317">Za pomocą opcji opcji/s. jest określony tryb cykliczne</span><span class="sxs-lookup"><span data-stu-id="4ec04-317">Recursive mode is specified via option /S.</span></span>

<span data-ttu-id="4ec04-318">Jeśli określone źródło hello jest katalogu w systemie plików hello, obowiązują standardowe symbole wieloznaczne i podać wzorzec pliku hello jest dopasowywana do plików w katalogu hello.</span><span class="sxs-lookup"><span data-stu-id="4ec04-318">If hello specified source is a directory in hello file system, then standard wildcards are in effect, and hello file pattern provided is matched against files within hello directory.</span></span> <span data-ttu-id="4ec04-319">Jeśli opcja określeniu, następnie AzCopy również wzorcem hello określony względem wszystkich plików w wszystkie podfoldery znajdujące się poniżej katalogu hello.</span><span class="sxs-lookup"><span data-stu-id="4ec04-319">If option /S is specified, then AzCopy also matches hello specified pattern against all files in any subfolders beneath hello directory.</span></span>

<span data-ttu-id="4ec04-320">W przypadku określonego źródła hello kontenera obiektów blob lub katalogu wirtualnego, symbole wieloznaczne nie są stosowane.</span><span class="sxs-lookup"><span data-stu-id="4ec04-320">If hello specified source is a blob container or virtual directory, then wildcards are not applied.</span></span> <span data-ttu-id="4ec04-321">Jeśli opcja/s jest określana, następnie AzCopy interpretuje hello określonego pliku wzorca jako prefiks obiektu blob.</span><span class="sxs-lookup"><span data-stu-id="4ec04-321">If option /S is specified, then AzCopy interprets hello specified file pattern as a blob prefix.</span></span> <span data-ttu-id="4ec04-322">Jeśli opcja /S nie zostanie określony, następnie AzCopy wzorcem hello pliku nazwami dokładne obiektu blob.</span><span class="sxs-lookup"><span data-stu-id="4ec04-322">If option /S is not specified, then AzCopy matches hello file pattern against exact blob names.</span></span>

<span data-ttu-id="4ec04-323">Jeśli hello określone źródło jest udział plików na platformę Azure, a następnie należy określić nazwę pliku dokładne hello (np. abc.txt) toocopy pojedynczy plik, lub określ opcję /S toocopy wszystkie pliki w hello rekursywnie udziału.</span><span class="sxs-lookup"><span data-stu-id="4ec04-323">If hello specified source is an Azure file share, then you must either specify hello exact file name, (e.g. abc.txt) toocopy a single file, or specify option /S toocopy all files in hello share recursively.</span></span> <span data-ttu-id="4ec04-324">Próba toospecify zarówno wzorzec pliku, jak i opcja /S razem spowoduje błąd.</span><span class="sxs-lookup"><span data-stu-id="4ec04-324">Attempting toospecify both a file pattern and option /S together will result in an error.</span></span>

<span data-ttu-id="4ec04-325">AzCopy korzysta z uwzględnieniem wielkości liter dopasowania, gdy hello/Source jest kontenera obiektów blob lub katalogu wirtualnego obiektów blob i używa bez uwzględniania wielkości liter dopasowanie wszystkich hello innych przypadkach.</span><span class="sxs-lookup"><span data-stu-id="4ec04-325">AzCopy uses case-sensitive matching when hello /Source is a blob container or blob virtual directory, and uses case-insensitive matching in all hello other cases.</span></span>

<span data-ttu-id="4ec04-326">Witaj wzorzec pliku domyślne używane, jeśli nie określono żadnych wzorzec pliku jest *.*</span><span class="sxs-lookup"><span data-stu-id="4ec04-326">hello default file pattern used when no file pattern is specified is *.*</span></span> <span data-ttu-id="4ec04-327">dla lokalizacji systemu plików lub pustego prefiksu lokalizacji magazynu Azure.</span><span class="sxs-lookup"><span data-stu-id="4ec04-327">for a file system location or an empty prefix for an Azure Storage location.</span></span> <span data-ttu-id="4ec04-328">Nie można określać wielu wzorców pliku.</span><span class="sxs-lookup"><span data-stu-id="4ec04-328">Specifying multiple file patterns is not supported.</span></span>

<span data-ttu-id="4ec04-329">**Dotyczy:** obiektów blob, pliki</span><span class="sxs-lookup"><span data-stu-id="4ec04-329">**Applicable to:** Blobs, Files</span></span>

### <a name="destkeystorage-key"></a><span data-ttu-id="4ec04-330">/ DestKey: "klucz magazynu"</span><span class="sxs-lookup"><span data-stu-id="4ec04-330">/DestKey:"storage-key"</span></span>
<span data-ttu-id="4ec04-331">Określa klucz konta magazynu hello hello zasobu docelowego.</span><span class="sxs-lookup"><span data-stu-id="4ec04-331">Specifies hello storage account key for hello destination resource.</span></span>

<span data-ttu-id="4ec04-332">**Dotyczy:** obiektów blob, plików, tabel</span><span class="sxs-lookup"><span data-stu-id="4ec04-332">**Applicable to:** Blobs, Files, Tables</span></span>

### <a name="destsassas-token"></a><span data-ttu-id="4ec04-333">/ DestSAS: "tokenu sygnatury dostępu współdzielonego"</span><span class="sxs-lookup"><span data-stu-id="4ec04-333">/DestSAS:"sas-token"</span></span>
<span data-ttu-id="4ec04-334">Określa dostępu sygnatury dostępu Współdzielonego z uprawnieniami odczytu i zapisu dla miejsca docelowego hello (jeśli dotyczy).</span><span class="sxs-lookup"><span data-stu-id="4ec04-334">Specifies a Shared Access Signature (SAS) with READ and WRITE permissions for hello destination (if applicable).</span></span> <span data-ttu-id="4ec04-335">Ująć hello SAS z cudzysłowami podwójnymi, jak mogą zawiera znaki specjalne wiersza polecenia.</span><span class="sxs-lookup"><span data-stu-id="4ec04-335">Surround hello SAS with double quotes, as it may contains special command-line characters.</span></span>

<span data-ttu-id="4ec04-336">W przypadku zasobu docelowego hello kontenera obiektów blob, udziału plików lub tabeli, można określić tej opcji, a po niej tokenu sygnatury dostępu Współdzielonego hello lub jako część hello docelowy kontener obiektów blob, udziału plików lub identyfikator URI tabeli, jeśli ta opcja nie można określić hello SAS.</span><span class="sxs-lookup"><span data-stu-id="4ec04-336">If hello destination resource is a blob container, file share or table, you can either specify this option followed by hello SAS token, or you can specify hello SAS as part of hello destination blob container, file share or table's URI, without this option.</span></span>

<span data-ttu-id="4ec04-337">Jeśli hello źródłowy i docelowy są oba obiekty BLOB, a następnie hello docelowego obiektu blob musi znajdować się w obrębie hello same konta magazynu jako hello źródłowego obiektu blob.</span><span class="sxs-lookup"><span data-stu-id="4ec04-337">If hello source and destination are both blobs, then hello destination blob must reside within hello same storage account as hello source blob.</span></span>

<span data-ttu-id="4ec04-338">**Dotyczy:** obiektów blob, plików, tabel</span><span class="sxs-lookup"><span data-stu-id="4ec04-338">**Applicable to:** Blobs, Files, Tables</span></span>

### <a name="sourcekeystorage-key"></a><span data-ttu-id="4ec04-339">/ SourceKey: "klucz magazynu"</span><span class="sxs-lookup"><span data-stu-id="4ec04-339">/SourceKey:"storage-key"</span></span>
<span data-ttu-id="4ec04-340">Określa klucz konta magazynu hello hello źródła zasobu.</span><span class="sxs-lookup"><span data-stu-id="4ec04-340">Specifies hello storage account key for hello source resource.</span></span>

<span data-ttu-id="4ec04-341">**Dotyczy:** obiektów blob, plików, tabel</span><span class="sxs-lookup"><span data-stu-id="4ec04-341">**Applicable to:** Blobs, Files, Tables</span></span>

### <a name="sourcesassas-token"></a><span data-ttu-id="4ec04-342">/ SourceSAS: "tokenu sygnatury dostępu współdzielonego"</span><span class="sxs-lookup"><span data-stu-id="4ec04-342">/SourceSAS:"sas-token"</span></span>
<span data-ttu-id="4ec04-343">Określa sygnaturę dostępu współdzielonego z uprawnieniami odczytu i listy hello źródła (jeśli dotyczy).</span><span class="sxs-lookup"><span data-stu-id="4ec04-343">Specifies a Shared Access Signature with READ and LIST permissions for hello source (if applicable).</span></span> <span data-ttu-id="4ec04-344">Ująć hello SAS z cudzysłowami podwójnymi, jak mogą zawiera znaki specjalne wiersza polecenia.</span><span class="sxs-lookup"><span data-stu-id="4ec04-344">Surround hello SAS with double quotes, as it may contains special command-line characters.</span></span>

<span data-ttu-id="4ec04-345">Jeśli zasób źródła hello jest kontenera obiektów blob, a podano klucz ani sygnatury dostępu Współdzielonego, za pomocą anonimowego dostępu do odczytu jest hello kontenera obiektów blob.</span><span class="sxs-lookup"><span data-stu-id="4ec04-345">If hello source resource is a blob container, and neither a key nor a SAS is provided, then hello blob container will be read via anonymous access.</span></span>

<span data-ttu-id="4ec04-346">Jeśli źródło hello jest udział plików lub tabeli, należy podać klucz lub sygnatury dostępu Współdzielonego.</span><span class="sxs-lookup"><span data-stu-id="4ec04-346">If hello source is a file share or table, a key or a SAS must be provided.</span></span>

<span data-ttu-id="4ec04-347">**Dotyczy:** obiektów blob, plików, tabel</span><span class="sxs-lookup"><span data-stu-id="4ec04-347">**Applicable to:** Blobs, Files, Tables</span></span>

### <a name="s"></a><span data-ttu-id="4ec04-348">/ S</span><span class="sxs-lookup"><span data-stu-id="4ec04-348">/S</span></span>
<span data-ttu-id="4ec04-349">Określa tryb cyklicznych operacji kopiowania.</span><span class="sxs-lookup"><span data-stu-id="4ec04-349">Specifies recursive mode for copy operations.</span></span> <span data-ttu-id="4ec04-350">W trybie cykliczne AzCopy zostaną skopiowane wszystkie obiekty BLOB lub pliki, które jest zgodny z wzorcem określonego pliku hello, włącznie z zawartymi w podfolderach.</span><span class="sxs-lookup"><span data-stu-id="4ec04-350">In recursive mode, AzCopy will copy all blobs or files that match hello specified file pattern, including those in subfolders.</span></span>

<span data-ttu-id="4ec04-351">**Dotyczy:** obiektów blob, pliki</span><span class="sxs-lookup"><span data-stu-id="4ec04-351">**Applicable to:** Blobs, Files</span></span>

### <a name="blobtypeblock--page--append"></a><span data-ttu-id="4ec04-352">/ BlobType: "block" | "page" | "Dołącz"</span><span class="sxs-lookup"><span data-stu-id="4ec04-352">/BlobType:"block" | "page" | "append"</span></span>
<span data-ttu-id="4ec04-353">Określa, czy hello docelowego obiektu blob jest blokowych obiektów blob i stronicowych obiektów blob, uzupełnialny obiekt blob.</span><span class="sxs-lookup"><span data-stu-id="4ec04-353">Specifies whether hello destination blob is a block blob, a page blob, or an append blob.</span></span> <span data-ttu-id="4ec04-354">Ta opcja ma zastosowanie tylko wtedy, gdy przekazujesz obiektu blob.</span><span class="sxs-lookup"><span data-stu-id="4ec04-354">This option is applicable only when you are uploading a blob.</span></span> <span data-ttu-id="4ec04-355">W przeciwnym razie zostanie wygenerowany błąd.</span><span class="sxs-lookup"><span data-stu-id="4ec04-355">Otherwise, an error is generated.</span></span> <span data-ttu-id="4ec04-356">Jeśli docelowy hello jest obiektem blob, a ta opcja nie jest określona, domyślnie AzCopy tworzy blokowych obiektów blob.</span><span class="sxs-lookup"><span data-stu-id="4ec04-356">If hello destination is a blob and this option is not specified, by default, AzCopy creates a block blob.</span></span>

<span data-ttu-id="4ec04-357">**Dotyczy:** obiektów blob</span><span class="sxs-lookup"><span data-stu-id="4ec04-357">**Applicable to:** Blobs</span></span>

### <a name="checkmd5"></a><span data-ttu-id="4ec04-358">/ CheckMD5</span><span class="sxs-lookup"><span data-stu-id="4ec04-358">/CheckMD5</span></span>
<span data-ttu-id="4ec04-359">Oblicza Skrót MD5 pobrane dane i weryfikuje, czy skrót MD5 hello przechowywane w obiekcie blob hello lub właściwość Content-MD5 pliku odpowiada hello obliczana wyznaczania wartości skrótu.</span><span class="sxs-lookup"><span data-stu-id="4ec04-359">Calculates an MD5 hash for downloaded data and verifies that hello MD5 hash stored in hello blob or file's Content-MD5 property matches hello calculated hash.</span></span> <span data-ttu-id="4ec04-360">Hello MD5 wyboru jest domyślnie wyłączona, należy określić opcję tooperform hello MD5 sprawdzanie podczas pobierania danych.</span><span class="sxs-lookup"><span data-stu-id="4ec04-360">hello MD5 check is turned off by default, so you must specify this option tooperform hello MD5 check when downloading data.</span></span>

<span data-ttu-id="4ec04-361">Należy pamiętać, że usługi Azure Storage nie gwarantuje tego hello wyznaczania wartości skrótu MD5 przechowywanych dla obiekt blob hello, lub plik jest aktualny.</span><span class="sxs-lookup"><span data-stu-id="4ec04-361">Note that Azure Storage doesn't guarantee that hello MD5 hash stored for hello blob or file is up-to-date.</span></span> <span data-ttu-id="4ec04-362">Klienta odpowiedzialność tooupdate hello MD5 jest zawsze, gdy obiekt blob hello lub plik jest modyfikowany.</span><span class="sxs-lookup"><span data-stu-id="4ec04-362">It is client's responsibility tooupdate hello MD5 whenever hello blob or file is modified.</span></span>

<span data-ttu-id="4ec04-363">Narzędzie AzCopy zawsze ustawia właściwość Content-MD5 hello obiektów blob platformy Azure lub plik po przekazać go toohello usługi.</span><span class="sxs-lookup"><span data-stu-id="4ec04-363">AzCopy always sets hello Content-MD5 property for an Azure blob or file after uploading it toohello service.</span></span>  

<span data-ttu-id="4ec04-364">**Dotyczy:** obiektów blob, pliki</span><span class="sxs-lookup"><span data-stu-id="4ec04-364">**Applicable to:** Blobs, Files</span></span>

### <a name="snapshot"></a><span data-ttu-id="4ec04-365">/ Migawki</span><span class="sxs-lookup"><span data-stu-id="4ec04-365">/Snapshot</span></span>
<span data-ttu-id="4ec04-366">Wskazuje, czy tootransfer migawki.</span><span class="sxs-lookup"><span data-stu-id="4ec04-366">Indicates whether tootransfer snapshots.</span></span> <span data-ttu-id="4ec04-367">Ta opcja jest prawidłowy tylko w przypadku, gdy źródło hello jest obiektu blob.</span><span class="sxs-lookup"><span data-stu-id="4ec04-367">This option is only valid when hello source is a blob.</span></span>

<span data-ttu-id="4ec04-368">Witaj migawki obiektu blob przekazanych zostały zmienione w następującym formacie: .extension nazwy obiektów blob (migawka time)</span><span class="sxs-lookup"><span data-stu-id="4ec04-368">hello transferred blob snapshots are renamed in this format: blob-name (snapshot-time).extension</span></span>

<span data-ttu-id="4ec04-369">Domyślnie nie są kopiowane migawki.</span><span class="sxs-lookup"><span data-stu-id="4ec04-369">By default, snapshots are not copied.</span></span>

<span data-ttu-id="4ec04-370">**Dotyczy:** obiektów blob</span><span class="sxs-lookup"><span data-stu-id="4ec04-370">**Applicable to:** Blobs</span></span>

### <a name="vverbose-log-file"></a><span data-ttu-id="4ec04-371">/ V: [plików pełnego dziennika]</span><span class="sxs-lookup"><span data-stu-id="4ec04-371">/V:[verbose-log-file]</span></span>
<span data-ttu-id="4ec04-372">Komunikaty stanu pełne dane wyjściowe do pliku dziennika.</span><span class="sxs-lookup"><span data-stu-id="4ec04-372">Outputs verbose status messages into a log file.</span></span>

<span data-ttu-id="4ec04-373">Domyślnie program hello pełny plik dziennika ma nazwę AzCopyVerbose.log w `%LocalAppData%\Microsoft\Azure\AzCopy`.</span><span class="sxs-lookup"><span data-stu-id="4ec04-373">By default, hello verbose log file is named AzCopyVerbose.log in `%LocalAppData%\Microsoft\Azure\AzCopy`.</span></span> <span data-ttu-id="4ec04-374">Jeśli określisz istniejącej lokalizacji plików dla tej opcji, pełny dziennik hello będzie toothat dołączany plik.</span><span class="sxs-lookup"><span data-stu-id="4ec04-374">If you specify an existing file location for this option, hello verbose log will be appended toothat file.</span></span>  

<span data-ttu-id="4ec04-375">**Dotyczy:** obiektów blob, plików, tabel</span><span class="sxs-lookup"><span data-stu-id="4ec04-375">**Applicable to:** Blobs, Files, Tables</span></span>

### <a name="zjournal-file-folder"></a><span data-ttu-id="4ec04-376">/ Z: [arkusza pliku folder]</span><span class="sxs-lookup"><span data-stu-id="4ec04-376">/Z:[journal-file-folder]</span></span>
<span data-ttu-id="4ec04-377">Określa folder plików dziennika dla wznawia działanie.</span><span class="sxs-lookup"><span data-stu-id="4ec04-377">Specifies a journal file folder for resuming an operation.</span></span>

<span data-ttu-id="4ec04-378">Narzędzie AzCopy zawsze obsługuje wznawianie, jeśli operacja została przerwana.</span><span class="sxs-lookup"><span data-stu-id="4ec04-378">AzCopy always supports resuming if an operation has been interrupted.</span></span>

<span data-ttu-id="4ec04-379">Jeśli ta opcja nie jest określony lub został określony bez ścieżki folderu, AzCopy zostanie utworzony plik dziennika hello w domyślnej lokalizacji hello, czyli % LocalAppData%\Microsoft\Azure\AzCopy.</span><span class="sxs-lookup"><span data-stu-id="4ec04-379">If this option is not specified, or it is specified without a folder path, then AzCopy will create hello journal file in hello default location, which is %LocalAppData%\Microsoft\Azure\AzCopy.</span></span>

<span data-ttu-id="4ec04-380">Zawsze, gdy wystawiać tooAzCopy polecenia, sprawdza czy istnieje plik dziennika w folderze domyślnym hello, lub czy istnieje w folderze określonej za pomocą tej opcji.</span><span class="sxs-lookup"><span data-stu-id="4ec04-380">Each time you issue a command tooAzCopy, it checks whether a journal file exists in hello default folder, or whether it exists in a folder that you specified via this option.</span></span> <span data-ttu-id="4ec04-381">Jeśli plik dziennika hello nie istnieje w każdym miejscu, AzCopy traktuje operacji hello jako nowy i generuje nowy plik dziennika.</span><span class="sxs-lookup"><span data-stu-id="4ec04-381">If hello journal file does not exist in either place, AzCopy treats hello operation as new and generates a new journal file.</span></span>

<span data-ttu-id="4ec04-382">Jeśli istnieje plik dziennika hello, AzCopy sprawdzi, czy hello wiersza polecenia, które możesz wpisać zgodny hello wiersza polecenia w pliku dziennika hello.</span><span class="sxs-lookup"><span data-stu-id="4ec04-382">If hello journal file does exist, AzCopy will check whether hello command line that you input matches hello command line in hello journal file.</span></span> <span data-ttu-id="4ec04-383">Jeśli dwa wiersze polecenia hello są zgodne, AzCopy wznawia hello nieukończone działania.</span><span class="sxs-lookup"><span data-stu-id="4ec04-383">If hello two command lines match, AzCopy resumes hello incomplete operation.</span></span> <span data-ttu-id="4ec04-384">Jeśli nie są zgodne, będzie zostanie wyświetlony monit o tooeither Zastąp hello dziennika pliku toostart nowej operacji lub toocancel hello bieżącej operacji.</span><span class="sxs-lookup"><span data-stu-id="4ec04-384">If they do not match, you will be prompted tooeither overwrite hello journal file toostart a new operation, or toocancel hello current operation.</span></span>

<span data-ttu-id="4ec04-385">plik dziennika Hello jest usuwany po pomyślnym zakończeniu operacji hello.</span><span class="sxs-lookup"><span data-stu-id="4ec04-385">hello journal file is deleted upon successful completion of hello operation.</span></span>

<span data-ttu-id="4ec04-386">Należy pamiętać, że wznawia działanie z pliku dziennika utworzonego przez poprzednią wersję programu AzCopy nie jest obsługiwany.</span><span class="sxs-lookup"><span data-stu-id="4ec04-386">Note that resuming an operation from a journal file created by a previous version of AzCopy is not supported.</span></span>

<span data-ttu-id="4ec04-387">**Dotyczy:** obiektów blob, plików, tabel</span><span class="sxs-lookup"><span data-stu-id="4ec04-387">**Applicable to:** Blobs, Files, Tables</span></span>

### <a name="parameter-file"></a><span data-ttu-id="4ec04-388">/@:"parameter-File"</span><span class="sxs-lookup"><span data-stu-id="4ec04-388">/@:"parameter-file"</span></span>
<span data-ttu-id="4ec04-389">Określa plik, który zawiera parametry.</span><span class="sxs-lookup"><span data-stu-id="4ec04-389">Specifies a file that contains parameters.</span></span> <span data-ttu-id="4ec04-390">Procesy AzCopy hello parametrów w pliku hello, tak jakby były one określone w wierszu polecenia hello.</span><span class="sxs-lookup"><span data-stu-id="4ec04-390">AzCopy processes hello parameters in hello file just as if they had been specified on hello command line.</span></span>

<span data-ttu-id="4ec04-391">W pliku odpowiedzi można określić wiele parametrów w jednym wierszu lub określ każdego parametru w osobnym wierszu.</span><span class="sxs-lookup"><span data-stu-id="4ec04-391">In a response file, you can either specify multiple parameters on a single line, or specify each parameter on its own line.</span></span> <span data-ttu-id="4ec04-392">Należy pamiętać, że poszczególne parametru nie może obejmować wiele wierszy.</span><span class="sxs-lookup"><span data-stu-id="4ec04-392">Note that an individual parameter cannot span multiple lines.</span></span>

<span data-ttu-id="4ec04-393">Pliki odpowiedzi może zawierać wiersze z symbolem # hello komentarze.</span><span class="sxs-lookup"><span data-stu-id="4ec04-393">Response files can include comments lines that begin with hello # symbol.</span></span>

<span data-ttu-id="4ec04-394">Można określić wiele plików odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="4ec04-394">You can specify multiple response files.</span></span> <span data-ttu-id="4ec04-395">Jednak należy pamiętać, że narzędzie AzCopy nie obsługuje zagnieżdżone pliki odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="4ec04-395">However, note that AzCopy does not support nested response files.</span></span>

<span data-ttu-id="4ec04-396">**Dotyczy:** obiektów blob, plików, tabel</span><span class="sxs-lookup"><span data-stu-id="4ec04-396">**Applicable to:** Blobs, Files, Tables</span></span>

### <a name="y"></a><span data-ttu-id="4ec04-397">/ Y</span><span class="sxs-lookup"><span data-stu-id="4ec04-397">/Y</span></span>
<span data-ttu-id="4ec04-398">Pomija wszystkie monity potwierdzenie narzędzia AzCopy.</span><span class="sxs-lookup"><span data-stu-id="4ec04-398">Suppresses all AzCopy confirmation prompts.</span></span>

<span data-ttu-id="4ec04-399">**Dotyczy:** obiektów blob, plików, tabel</span><span class="sxs-lookup"><span data-stu-id="4ec04-399">**Applicable to:** Blobs, Files, Tables</span></span>

### <a name="l"></a><span data-ttu-id="4ec04-400">/L</span><span class="sxs-lookup"><span data-stu-id="4ec04-400">/L</span></span>
<span data-ttu-id="4ec04-401">Określa listę operację. dane nie zostaną skopiowane.</span><span class="sxs-lookup"><span data-stu-id="4ec04-401">Specifies a listing operation only; no data is copied.</span></span>

<span data-ttu-id="4ec04-402">Narzędzie AzCopy zinterpretuje hello przy użyciu tej opcji jako symulacji dla uruchomionego hello wiersza polecenia bez stosowania tej opcji /L i liczba ile obiekty zostaną skopiowane, można określić opcję /V na powitania sam czas toocheck obiekty, które zostaną skopiowane hello pełnego dziennika.</span><span class="sxs-lookup"><span data-stu-id="4ec04-402">AzCopy will interpret hello using of this option as a simulation for running hello command line without this option /L and count how many objects will be copied, you can specify option /V at hello same time toocheck which objects will be copied in hello verbose log.</span></span>

<span data-ttu-id="4ec04-403">zachowanie Hello tej opcji również jest określana przez hello lokalizacji hello źródła danych i hello obecności hello cykliczne opcji/s i pliku wzorca w trybie /Pattern.</span><span class="sxs-lookup"><span data-stu-id="4ec04-403">hello behavior of this option is also determined by hello location of hello source data and hello presence of hello recursive mode option /S and file pattern option /Pattern.</span></span>

<span data-ttu-id="4ec04-404">Narzędzie AzCopy musi mieć uprawnienie listy i odczytu tej lokalizacji źródła przy użyciu tej opcji.</span><span class="sxs-lookup"><span data-stu-id="4ec04-404">AzCopy requires LIST and READ permission of this source location when using this option.</span></span>

<span data-ttu-id="4ec04-405">**Dotyczy:** obiektów blob, pliki</span><span class="sxs-lookup"><span data-stu-id="4ec04-405">**Applicable to:** Blobs, Files</span></span>

### <a name="mt"></a><span data-ttu-id="4ec04-406">/ MT</span><span class="sxs-lookup"><span data-stu-id="4ec04-406">/MT</span></span>
<span data-ttu-id="4ec04-407">Ustawia czas ostatniej modyfikacji hello pobrany plik toobe hello takie same jak hello źródłowego obiektu blob lub pliku.</span><span class="sxs-lookup"><span data-stu-id="4ec04-407">Sets hello downloaded file's last-modified time toobe hello same as hello source blob or file's.</span></span>

<span data-ttu-id="4ec04-408">**Dotyczy:** obiektów blob, pliki</span><span class="sxs-lookup"><span data-stu-id="4ec04-408">**Applicable to:** Blobs, Files</span></span>

### <a name="xn"></a><span data-ttu-id="4ec04-409">/XN</span><span class="sxs-lookup"><span data-stu-id="4ec04-409">/XN</span></span>
<span data-ttu-id="4ec04-410">Wyklucza nowszej zasobów źródła.</span><span class="sxs-lookup"><span data-stu-id="4ec04-410">Excludes a newer source resource.</span></span> <span data-ttu-id="4ec04-411">Witaj zasobów nie zostaną skopiowane, jeśli hello godzina ostatniej modyfikacji źródła hello jest hello taką samą lub nowszą niż docelowy.</span><span class="sxs-lookup"><span data-stu-id="4ec04-411">hello resource will not be copied if hello last modified time of hello source is hello same or newer than destination.</span></span>

<span data-ttu-id="4ec04-412">**Dotyczy:** obiektów blob, pliki</span><span class="sxs-lookup"><span data-stu-id="4ec04-412">**Applicable to:** Blobs, Files</span></span>

### <a name="xo"></a><span data-ttu-id="4ec04-413">/XO</span><span class="sxs-lookup"><span data-stu-id="4ec04-413">/XO</span></span>
<span data-ttu-id="4ec04-414">Wyklucza starszych zasobów źródła.</span><span class="sxs-lookup"><span data-stu-id="4ec04-414">Excludes an older source resource.</span></span> <span data-ttu-id="4ec04-415">Witaj zasobów nie zostaną skopiowane, jeśli hello godzina ostatniej modyfikacji źródła hello jest hello tego samego lub starsze niż docelowy.</span><span class="sxs-lookup"><span data-stu-id="4ec04-415">hello resource will not be copied if hello last modified time of hello source is hello same or older than destination.</span></span>

<span data-ttu-id="4ec04-416">**Dotyczy:** obiektów blob, pliki</span><span class="sxs-lookup"><span data-stu-id="4ec04-416">**Applicable to:** Blobs, Files</span></span>

### <a name="a"></a><span data-ttu-id="4ec04-417">/A</span><span class="sxs-lookup"><span data-stu-id="4ec04-417">/A</span></span>
<span data-ttu-id="4ec04-418">Wysyła tylko pliki, które mają ustawiony atrybut archiwum hello.</span><span class="sxs-lookup"><span data-stu-id="4ec04-418">Uploads only files that have hello Archive attribute set.</span></span>

<span data-ttu-id="4ec04-419">**Dotyczy:** obiektów blob, pliki</span><span class="sxs-lookup"><span data-stu-id="4ec04-419">**Applicable to:** Blobs, Files</span></span>

### <a name="iarashcnetoi"></a><span data-ttu-id="4ec04-420">/ IA: [RASHCNETOI]</span><span class="sxs-lookup"><span data-stu-id="4ec04-420">/IA:[RASHCNETOI]</span></span>
<span data-ttu-id="4ec04-421">Przekazywanie tylko pliki, które nie ma żadnej z hello określony zestaw atrybutów.</span><span class="sxs-lookup"><span data-stu-id="4ec04-421">Uploads only files that have any of hello specified attributes set.</span></span>

<span data-ttu-id="4ec04-422">Dostępne atrybuty obejmują:</span><span class="sxs-lookup"><span data-stu-id="4ec04-422">Available attributes include:</span></span>

* <span data-ttu-id="4ec04-423">R = plików tylko do odczytu</span><span class="sxs-lookup"><span data-stu-id="4ec04-423">R = Read-only files</span></span>
* <span data-ttu-id="4ec04-424">= Plik gotowy do archiwizacji</span><span class="sxs-lookup"><span data-stu-id="4ec04-424">A = Files ready for archiving</span></span>
* <span data-ttu-id="4ec04-425">S = System plików</span><span class="sxs-lookup"><span data-stu-id="4ec04-425">S = System files</span></span>
* <span data-ttu-id="4ec04-426">H = ukryte pliki</span><span class="sxs-lookup"><span data-stu-id="4ec04-426">H = Hidden files</span></span>
* <span data-ttu-id="4ec04-427">C = pliki skompresowane</span><span class="sxs-lookup"><span data-stu-id="4ec04-427">C = Compressed files</span></span>
* <span data-ttu-id="4ec04-428">N = normalne pliki</span><span class="sxs-lookup"><span data-stu-id="4ec04-428">N = Normal files</span></span>
* <span data-ttu-id="4ec04-429">E = zaszyfrowane pliki</span><span class="sxs-lookup"><span data-stu-id="4ec04-429">E = Encrypted files</span></span>
* <span data-ttu-id="4ec04-430">T = pliki tymczasowe</span><span class="sxs-lookup"><span data-stu-id="4ec04-430">T = Temporary files</span></span>
* <span data-ttu-id="4ec04-431">O = plików trybu Offline</span><span class="sxs-lookup"><span data-stu-id="4ec04-431">O = Offline files</span></span>
* <span data-ttu-id="4ec04-432">I = indeksowane inne niż pliki</span><span class="sxs-lookup"><span data-stu-id="4ec04-432">I = Non-indexed files</span></span>

<span data-ttu-id="4ec04-433">**Dotyczy:** obiektów blob, pliki</span><span class="sxs-lookup"><span data-stu-id="4ec04-433">**Applicable to:** Blobs, Files</span></span>

### <a name="xarashcnetoi"></a><span data-ttu-id="4ec04-434">/ XA: [RASHCNETOI]</span><span class="sxs-lookup"><span data-stu-id="4ec04-434">/XA:[RASHCNETOI]</span></span>
<span data-ttu-id="4ec04-435">Wyklucza pliki, które nie ma żadnej z hello określony zestaw atrybutów.</span><span class="sxs-lookup"><span data-stu-id="4ec04-435">Excludes files that have any of hello specified attributes set.</span></span>

<span data-ttu-id="4ec04-436">Dostępne atrybuty obejmują:</span><span class="sxs-lookup"><span data-stu-id="4ec04-436">Available attributes include:</span></span>

* <span data-ttu-id="4ec04-437">R = plików tylko do odczytu</span><span class="sxs-lookup"><span data-stu-id="4ec04-437">R = Read-only files</span></span>
* <span data-ttu-id="4ec04-438">= Plik gotowy do archiwizacji</span><span class="sxs-lookup"><span data-stu-id="4ec04-438">A = Files ready for archiving</span></span>
* <span data-ttu-id="4ec04-439">S = System plików</span><span class="sxs-lookup"><span data-stu-id="4ec04-439">S = System files</span></span>
* <span data-ttu-id="4ec04-440">H = ukryte pliki</span><span class="sxs-lookup"><span data-stu-id="4ec04-440">H = Hidden files</span></span>
* <span data-ttu-id="4ec04-441">C = pliki skompresowane</span><span class="sxs-lookup"><span data-stu-id="4ec04-441">C = Compressed files</span></span>
* <span data-ttu-id="4ec04-442">N = normalne pliki</span><span class="sxs-lookup"><span data-stu-id="4ec04-442">N = Normal files</span></span>
* <span data-ttu-id="4ec04-443">E = zaszyfrowane pliki</span><span class="sxs-lookup"><span data-stu-id="4ec04-443">E = Encrypted files</span></span>
* <span data-ttu-id="4ec04-444">T = pliki tymczasowe</span><span class="sxs-lookup"><span data-stu-id="4ec04-444">T = Temporary files</span></span>
* <span data-ttu-id="4ec04-445">O = plików trybu Offline</span><span class="sxs-lookup"><span data-stu-id="4ec04-445">O = Offline files</span></span>
* <span data-ttu-id="4ec04-446">I = indeksowane inne niż pliki</span><span class="sxs-lookup"><span data-stu-id="4ec04-446">I = Non-indexed files</span></span>

<span data-ttu-id="4ec04-447">**Dotyczy:** obiektów blob, pliki</span><span class="sxs-lookup"><span data-stu-id="4ec04-447">**Applicable to:** Blobs, Files</span></span>

### <a name="delimiterdelimiter"></a><span data-ttu-id="4ec04-448">/ Ogranicznik: "ogranicznika"</span><span class="sxs-lookup"><span data-stu-id="4ec04-448">/Delimiter:"delimiter"</span></span>
<span data-ttu-id="4ec04-449">Wskazuje, że znak ogranicznika hello używane toodelimit katalogów wirtualnych w nazwie obiektu blob.</span><span class="sxs-lookup"><span data-stu-id="4ec04-449">Indicates hello delimiter character used toodelimit virtual directories in a blob name.</span></span>

<span data-ttu-id="4ec04-450">Domyślnie używa narzędzia AzCopy / jako znak ogranicznika hello.</span><span class="sxs-lookup"><span data-stu-id="4ec04-450">By default, AzCopy uses / as hello delimiter character.</span></span> <span data-ttu-id="4ec04-451">AzCopy obsługuje jednak przy użyciu znaków wspólnych (takich jak @, # lub %) jako ogranicznik.</span><span class="sxs-lookup"><span data-stu-id="4ec04-451">However, AzCopy supports using any common character (such as @, #, or %) as a delimiter.</span></span> <span data-ttu-id="4ec04-452">Należy tooinclude jedną z tych znaków specjalnych w wierszu polecenia hello należy ująć hello nazwę pliku z cudzysłowami podwójnymi.</span><span class="sxs-lookup"><span data-stu-id="4ec04-452">If you need tooinclude one of these special characters on hello command line, enclose hello file name with double quotes.</span></span>

<span data-ttu-id="4ec04-453">Ta opcja ma zastosowanie tylko do pobrania obiektów blob.</span><span class="sxs-lookup"><span data-stu-id="4ec04-453">This option is only applicable for downloading blobs.</span></span>

<span data-ttu-id="4ec04-454">**Dotyczy:** obiektów blob</span><span class="sxs-lookup"><span data-stu-id="4ec04-454">**Applicable to:** Blobs</span></span>

### <a name="ncnumber-of-concurrent-operations"></a><span data-ttu-id="4ec04-455">/ NC: "numer--równoczesnych operacji"</span><span class="sxs-lookup"><span data-stu-id="4ec04-455">/NC:"number-of-concurrent-operations"</span></span>
<span data-ttu-id="4ec04-456">Określa hello liczbę jednoczesnych operacji.</span><span class="sxs-lookup"><span data-stu-id="4ec04-456">Specifies hello number of concurrent operations.</span></span>

<span data-ttu-id="4ec04-457">Narzędzie AzCopy domyślnie uruchamia określoną liczbę jednoczesnych operacji tooincrease hello danych przeniesienie przepływności.</span><span class="sxs-lookup"><span data-stu-id="4ec04-457">AzCopy by default starts a certain number of concurrent operations tooincrease hello data transfer throughput.</span></span> <span data-ttu-id="4ec04-458">Należy pamiętać, że dużą liczbą jednoczesnych operacji w środowisku niskiej przepustowości może przeciąży hello połączenie sieciowe i zapobiec operacji hello pełni ukończenie.</span><span class="sxs-lookup"><span data-stu-id="4ec04-458">Note that large number of concurrent operations in a low-bandwidth environment may overwhelm hello network connection and prevent hello operations from fully completing.</span></span> <span data-ttu-id="4ec04-459">Ograniczenie przepustowości jednoczesnych operacji oparte na rzeczywiste dostępnej przepustowości sieci.</span><span class="sxs-lookup"><span data-stu-id="4ec04-459">Throttle concurrent operations based on actual available network bandwidth.</span></span>

<span data-ttu-id="4ec04-460">Hello górny limit liczby jednoczesnych operacji wynosi 512.</span><span class="sxs-lookup"><span data-stu-id="4ec04-460">hello upper limit for concurrent operations is 512.</span></span>

<span data-ttu-id="4ec04-461">**Dotyczy:** obiektów blob, plików, tabel</span><span class="sxs-lookup"><span data-stu-id="4ec04-461">**Applicable to:** Blobs, Files, Tables</span></span>

### <a name="sourcetypeblob--table"></a><span data-ttu-id="4ec04-462">/ Źródłowa: "Blob" | "Tabela"</span><span class="sxs-lookup"><span data-stu-id="4ec04-462">/SourceType:"Blob" | "Table"</span></span>
<span data-ttu-id="4ec04-463">Określa, że hello `source` zasób jest dostępny w środowisku projektowym lokalne powitania, uruchamianie w emulatorze magazynu hello obiektu blob.</span><span class="sxs-lookup"><span data-stu-id="4ec04-463">Specifies that hello `source` resource is a blob available in hello local development environment, running in hello storage emulator.</span></span>

<span data-ttu-id="4ec04-464">**Dotyczy:** obiektów blob, tabel</span><span class="sxs-lookup"><span data-stu-id="4ec04-464">**Applicable to:** Blobs, Tables</span></span>

### <a name="desttypeblob--table"></a><span data-ttu-id="4ec04-465">/ DestType: "Blob" | "Tabela"</span><span class="sxs-lookup"><span data-stu-id="4ec04-465">/DestType:"Blob" | "Table"</span></span>
<span data-ttu-id="4ec04-466">Określa, że hello `destination` zasób jest dostępny w środowisku projektowym lokalne powitania, uruchamianie w emulatorze magazynu hello obiektu blob.</span><span class="sxs-lookup"><span data-stu-id="4ec04-466">Specifies that hello `destination` resource is a blob available in hello local development environment, running in hello storage emulator.</span></span>

<span data-ttu-id="4ec04-467">**Dotyczy:** obiektów blob, tabel</span><span class="sxs-lookup"><span data-stu-id="4ec04-467">**Applicable to:** Blobs, Tables</span></span>

### <a name="pkrskey1key2key3"></a><span data-ttu-id="4ec04-468">/ PKRS: "key1 klucz&#2; klucz&#3;..."</span><span class="sxs-lookup"><span data-stu-id="4ec04-468">/PKRS:"key1#key2#key3#..."</span></span>
<span data-ttu-id="4ec04-469">Podziały hello tooenable zakresem kluczy partycji eksportowania danych z tabeli równolegle, co spowoduje zwiększenie szybkości hello hello operacji eksportowania.</span><span class="sxs-lookup"><span data-stu-id="4ec04-469">Splits hello partition key range tooenable exporting table data in parallel, which increases hello speed of hello export operation.</span></span>

<span data-ttu-id="4ec04-470">Jeśli ta opcja nie jest określona, narzędzie AzCopy używa jednostek tabeli tooexport jednego wątku.</span><span class="sxs-lookup"><span data-stu-id="4ec04-470">If this option is not specified, then AzCopy uses a single thread tooexport table entities.</span></span> <span data-ttu-id="4ec04-471">Na przykład, jeśli hello użytkownika określa /PKRS: "aa #bb", a następnie AzCopy uruchamia trzy jednoczesnych operacji.</span><span class="sxs-lookup"><span data-stu-id="4ec04-471">For example, if hello user specifies /PKRS:"aa#bb", then AzCopy starts three concurrent operations.</span></span>

<span data-ttu-id="4ec04-472">Każda operacja eksportuje jednego z trzech zakresów klucza partycji, jak pokazano poniżej:</span><span class="sxs-lookup"><span data-stu-id="4ec04-472">Each operation exports one of three partition key ranges, as shown below:</span></span>

  <span data-ttu-id="4ec04-473">[pierwszej partycji klucza, aa)</span><span class="sxs-lookup"><span data-stu-id="4ec04-473">[first-partition-key, aa)</span></span>

  <span data-ttu-id="4ec04-474">[aa, bb)</span><span class="sxs-lookup"><span data-stu-id="4ec04-474">[aa, bb)</span></span>

  <span data-ttu-id="4ec04-475">[bb, ostatnie partycji klucza]</span><span class="sxs-lookup"><span data-stu-id="4ec04-475">[bb, last-partition-key]</span></span>

<span data-ttu-id="4ec04-476">**Dotyczy:** tabel</span><span class="sxs-lookup"><span data-stu-id="4ec04-476">**Applicable to:** Tables</span></span>

### <a name="splitsizefile-size"></a><span data-ttu-id="4ec04-477">/ SplitSize: "rozmiar pliku"</span><span class="sxs-lookup"><span data-stu-id="4ec04-477">/SplitSize:"file-size"</span></span>
<span data-ttu-id="4ec04-478">Określa hello wyeksportowany plik podzielić rozmiar w MB, hello minimalnego dozwolona wartość to 32.</span><span class="sxs-lookup"><span data-stu-id="4ec04-478">Specifies hello exported file split size in MB, hello minimal value allowed is 32.</span></span>

<span data-ttu-id="4ec04-479">Jeśli ta opcja nie jest określona, narzędzie AzCopy będzie eksportować plik toosingle danych tabeli.</span><span class="sxs-lookup"><span data-stu-id="4ec04-479">If this option is not specified, AzCopy will export table data toosingle file.</span></span>

<span data-ttu-id="4ec04-480">Jeśli dane tabeli hello jest tooa wyeksportowany obiekt blob, a hello wyeksportowany plik rozmiar osiągnie limit 200 GB hello rozmiar obiektu blob, następnie AzCopy podzieli hello wyeksportowany plik, nawet wtedy, gdy ta opcja nie jest określona.</span><span class="sxs-lookup"><span data-stu-id="4ec04-480">If hello table data is exported tooa blob, and hello exported file size reaches hello 200 GB limit for blob size, then AzCopy will split hello exported file, even if this option is not specified.</span></span>

<span data-ttu-id="4ec04-481">**Dotyczy:** tabel</span><span class="sxs-lookup"><span data-stu-id="4ec04-481">**Applicable to:** Tables</span></span>

### <a name="entityoperationinsertorskip--insertormerge--insertorreplace"></a><span data-ttu-id="4ec04-482">/ EntityOperation: "InsertOrSkip" | "InsertOrMerge" | "InsertOrReplace"</span><span class="sxs-lookup"><span data-stu-id="4ec04-482">/EntityOperation:"InsertOrSkip" | "InsertOrMerge" | "InsertOrReplace"</span></span>
<span data-ttu-id="4ec04-483">Określa zachowanie importu danych hello w tabeli.</span><span class="sxs-lookup"><span data-stu-id="4ec04-483">Specifies hello table data import behavior.</span></span>

* <span data-ttu-id="4ec04-484">InsertOrSkip - pomija istniejącej jednostki lub wstawia nową jednostkę, jeśli nie istnieje w tabeli hello.</span><span class="sxs-lookup"><span data-stu-id="4ec04-484">InsertOrSkip - Skips an existing entity or inserts a new entity if it does not exist in hello table.</span></span>
* <span data-ttu-id="4ec04-485">InsertOrMerge - scala istniejącej jednostki lub wstawia nową jednostkę, jeśli nie istnieje w tabeli hello.</span><span class="sxs-lookup"><span data-stu-id="4ec04-485">InsertOrMerge - Merges an existing entity or inserts a new entity if it does not exist in hello table.</span></span>
* <span data-ttu-id="4ec04-486">InsertOrReplace - zastępuje istniejącej jednostki lub wstawia nową jednostkę, jeśli nie istnieje w tabeli hello.</span><span class="sxs-lookup"><span data-stu-id="4ec04-486">InsertOrReplace - Replaces an existing entity or inserts a new entity if it does not exist in hello table.</span></span>

<span data-ttu-id="4ec04-487">**Dotyczy:** tabel</span><span class="sxs-lookup"><span data-stu-id="4ec04-487">**Applicable to:** Tables</span></span>

### <a name="manifestmanifest-file"></a><span data-ttu-id="4ec04-488">/ Manifest: "w pliku manifestu"</span><span class="sxs-lookup"><span data-stu-id="4ec04-488">/Manifest:"manifest-file"</span></span>
<span data-ttu-id="4ec04-489">Określa plik manifestu hello tabeli hello eksportować i importować operacji.</span><span class="sxs-lookup"><span data-stu-id="4ec04-489">Specifies hello manifest file for hello table export and import operation.</span></span>

<span data-ttu-id="4ec04-490">Ta opcja jest opcjonalny podczas operacji eksportowania hello, AzCopy wygeneruje plik manifestu z wstępnie zdefiniowanej nazwy, jeśli ta opcja nie jest określona.</span><span class="sxs-lookup"><span data-stu-id="4ec04-490">This option is optional during hello export operation, AzCopy will generate a manifest file with predefined name if this option is not specified.</span></span>

<span data-ttu-id="4ec04-491">Ta opcja jest wymagana podczas operacji importowania hello do lokalizowania hello pliki danych.</span><span class="sxs-lookup"><span data-stu-id="4ec04-491">This option is required during hello import operation for locating hello data files.</span></span>

<span data-ttu-id="4ec04-492">**Dotyczy:** tabel</span><span class="sxs-lookup"><span data-stu-id="4ec04-492">**Applicable to:** Tables</span></span>

### <a name="synccopy"></a><span data-ttu-id="4ec04-493">/ SyncCopy</span><span class="sxs-lookup"><span data-stu-id="4ec04-493">/SyncCopy</span></span>
<span data-ttu-id="4ec04-494">Wskazuje, czy toosynchronously kopiowania obiektów blob lub plików między dwoma punktami końcowymi usługi Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="4ec04-494">Indicates whether toosynchronously copy blobs or files between two Azure Storage endpoints.</span></span>

<span data-ttu-id="4ec04-495">Narzędzie AzCopy domyślnie używa kopii asynchronicznych po stronie serwera.</span><span class="sxs-lookup"><span data-stu-id="4ec04-495">AzCopy by default uses server-side asynchronous copy.</span></span> <span data-ttu-id="4ec04-496">Określ to opcja tooperform synchronicznego skopiować, który pobiera obiektów blob lub pliki toolocal pamięci i przekazuje je po tooAzure magazynu.</span><span class="sxs-lookup"><span data-stu-id="4ec04-496">Specify this option tooperform a synchronous copy, which downloads blobs or files toolocal memory and then uploads them tooAzure Storage.</span></span>

<span data-ttu-id="4ec04-497">Tej opcji można użyć podczas kopiowania plików w magazynie obiektów Blob, Magazyn plików, lub z obiektu Blob magazynu tooFile magazynu lub na odwrót.</span><span class="sxs-lookup"><span data-stu-id="4ec04-497">You can use this option when copying files within Blob storage, within File storage, or from Blob storage tooFile storage or vice versa.</span></span>

<span data-ttu-id="4ec04-498">**Dotyczy:** obiektów blob, pliki</span><span class="sxs-lookup"><span data-stu-id="4ec04-498">**Applicable to:** Blobs, Files</span></span>

### <a name="setcontenttypecontent-type"></a><span data-ttu-id="4ec04-499">/ SetContentType: "content-type"</span><span class="sxs-lookup"><span data-stu-id="4ec04-499">/SetContentType:"content-type"</span></span>
<span data-ttu-id="4ec04-500">Określa typ zawartości MIME hello obiekty BLOB docelowego lub plików.</span><span class="sxs-lookup"><span data-stu-id="4ec04-500">Specifies hello MIME content type for destination blobs or files.</span></span>

<span data-ttu-id="4ec04-501">Zestawy AzCopy hello typ zawartości dla obiekt blob lub pliku domyślnie tooapplication/octet-stream.</span><span class="sxs-lookup"><span data-stu-id="4ec04-501">AzCopy sets hello content type for a blob or file tooapplication/octet-stream by default.</span></span> <span data-ttu-id="4ec04-502">Jawne określenie wartości dla tej opcji można ustawić hello typ zawartości dla wszystkich obiektów blob lub plików.</span><span class="sxs-lookup"><span data-stu-id="4ec04-502">You can set hello content type for all blobs or files by explicitly specifying a value for this option.</span></span>

<span data-ttu-id="4ec04-503">Jeśli zostanie określona opcja bez wartości, AzCopy zostanie ustawiony, każdy obiekt blob lub typu zawartości pliku, zgodnie z tooits rozszerzenie pliku.</span><span class="sxs-lookup"><span data-stu-id="4ec04-503">If you specify this option without a value, then AzCopy will set each blob or file's content type according tooits file extension.</span></span>

<span data-ttu-id="4ec04-504">**Dotyczy:** obiektów blob, pliki</span><span class="sxs-lookup"><span data-stu-id="4ec04-504">**Applicable to:** Blobs, Files</span></span>

### <a name="payloadformatjson--csv"></a><span data-ttu-id="4ec04-505">/ PayloadFormat: "JSON" | "CSV"</span><span class="sxs-lookup"><span data-stu-id="4ec04-505">/PayloadFormat:"JSON" | "CSV"</span></span>
<span data-ttu-id="4ec04-506">Określa format hello hello tabeli wyeksportowany plik danych.</span><span class="sxs-lookup"><span data-stu-id="4ec04-506">Specifies hello format of hello table exported data file.</span></span>

<span data-ttu-id="4ec04-507">Jeśli ta opcja nie jest określona, domyślnie AzCopy eksportuje plik danych tabeli w formacie JSON.</span><span class="sxs-lookup"><span data-stu-id="4ec04-507">If this option is not specified, by default AzCopy exports table data file in JSON format.</span></span>

<span data-ttu-id="4ec04-508">**Dotyczy:** tabel</span><span class="sxs-lookup"><span data-stu-id="4ec04-508">**Applicable to:** Tables</span></span>

## <a name="known-issues-and-best-practices"></a><span data-ttu-id="4ec04-509">Znane problemy i najlepsze rozwiązania</span><span class="sxs-lookup"><span data-stu-id="4ec04-509">Known Issues and Best Practices</span></span>
### <a name="limit-concurrent-writes-while-copying-data"></a><span data-ttu-id="4ec04-510">Limit równoczesnych zapisów podczas kopiowania danych</span><span class="sxs-lookup"><span data-stu-id="4ec04-510">Limit concurrent writes while copying data</span></span>
<span data-ttu-id="4ec04-511">Podczas kopiowania obiektów blob lub pliki z narzędzia AzCopy, należy pamiętać, że inna aplikacja może być modyfikowanie hello danych podczas kopiowania go.</span><span class="sxs-lookup"><span data-stu-id="4ec04-511">When you copy blobs or files with AzCopy, keep in mind that another application may be modifying hello data while you are copying it.</span></span> <span data-ttu-id="4ec04-512">Jeśli to możliwe upewnij się, że hello dane, które są kopiowane nie jest modyfikowana podczas operacji kopiowania hello.</span><span class="sxs-lookup"><span data-stu-id="4ec04-512">If possible, ensure that hello data you are copying is not being modified during hello copy operation.</span></span> <span data-ttu-id="4ec04-513">Na przykład podczas kopiowania wirtualnego dysku twardego skojarzonego z maszyny wirtualnej platformy Azure, upewnij się, że żadne inne aplikacje nie są obecnie zapisywania toohello wirtualnego dysku twardego.</span><span class="sxs-lookup"><span data-stu-id="4ec04-513">For example, when copying a VHD associated with an Azure virtual machine, make sure that no other applications are currently writing toohello VHD.</span></span> <span data-ttu-id="4ec04-514">Toodo dobrze to jest dzierżawa toobe zasobów hello skopiowane.</span><span class="sxs-lookup"><span data-stu-id="4ec04-514">A good way toodo this is by leasing hello resource toobe copied.</span></span> <span data-ttu-id="4ec04-515">Alternatywnie można najpierw Utwórz migawkę hello wirtualnego dysku twardego, a następnie skopiuj hello migawki.</span><span class="sxs-lookup"><span data-stu-id="4ec04-515">Alternately, you can create a snapshot of hello VHD first and then copy hello snapshot.</span></span>

<span data-ttu-id="4ec04-516">Jeśli nie można zapobiec innych aplikacji z zapisywania tooblobs lub plików podczas kopiowane są następnie pamiętać przez zadanie hello czasu hello zakończy, hello kopiowanych zasobów mogą już pełnej zgodności z hello źródła zasobów.</span><span class="sxs-lookup"><span data-stu-id="4ec04-516">If you cannot prevent other applications from writing tooblobs or files while they are being copied, then keep in mind that by hello time hello job finishes, hello copied resources may no longer have full parity with hello source resources.</span></span>

### <a name="run-one-azcopy-instance-on-one-machine"></a><span data-ttu-id="4ec04-517">Uruchom jedno wystąpienie AzCopy na jednej maszynie.</span><span class="sxs-lookup"><span data-stu-id="4ec04-517">Run one AzCopy instance on one machine.</span></span>
<span data-ttu-id="4ec04-518">Narzędzie AzCopy jest zaprojektowana toomaximize hello wykorzystania transferu danych hello tooaccelerate zasobów maszyny, zaleca się uruchomić tylko jedno wystąpienie AzCopy na jednej maszynie i określ opcję hello `/NC` Jeśli potrzebujesz więcej jednoczesnych operacji.</span><span class="sxs-lookup"><span data-stu-id="4ec04-518">AzCopy is designed toomaximize hello utilization of your machine resource tooaccelerate hello data transfer, we recommend you run only one AzCopy instance on one machine, and specify hello option `/NC` if you need more concurrent operations.</span></span> <span data-ttu-id="4ec04-519">Aby uzyskać więcej informacji, wpisz `AzCopy /?:NC` hello wiersza polecenia.</span><span class="sxs-lookup"><span data-stu-id="4ec04-519">For more details, type `AzCopy /?:NC` at hello command line.</span></span>

### <a name="enable-fips-compliant-md5-algorithms-for-azcopy-when-you-use-fips-compliant-algorithms-for-encryption-hashing-and-signing"></a><span data-ttu-id="4ec04-520">Włącz algorytmów MD5 FIPS dla narzędzia AzCopy podczas możesz "Użyj FIPS algorytmów szyfrowania, tworzenia skrótu i podpisywania".</span><span class="sxs-lookup"><span data-stu-id="4ec04-520">Enable FIPS compliant MD5 algorithms for AzCopy when you "Use FIPS compliant algorithms for encryption, hashing and signing".</span></span>
<span data-ttu-id="4ec04-521">AzCopy domyślnie używa .NET MD5 implementacji toocalculate hello MD5 podczas kopiowania obiektów, ale niektóre narzędzia AzCopy tooenable FIPS zgodne MD5 ustawienie wymagań zabezpieczeń.</span><span class="sxs-lookup"><span data-stu-id="4ec04-521">AzCopy by default uses .NET MD5 implementation toocalculate hello MD5 when copying objects, but there are some security requirements that need AzCopy tooenable FIPS compliant MD5 setting.</span></span>

<span data-ttu-id="4ec04-522">Można utworzyć pliku app.config `AzCopy.exe.config` z właściwością `AzureStorageUseV1MD5` i umieszcza je Zarezerwuj z AzCopy.exe.</span><span class="sxs-lookup"><span data-stu-id="4ec04-522">You can create an app.config file `AzCopy.exe.config` with property `AzureStorageUseV1MD5` and put it aside with AzCopy.exe.</span></span>

    <?xml version="1.0" encoding="utf-8" ?>
    <configuration>
      <appSettings>
        <add key="AzureStorageUseV1MD5" value="false"/>
      </appSettings>
    </configuration>

<span data-ttu-id="4ec04-523">Dla właściwości "AzureStorageUseV1MD5" • wartość True — wartość domyślną hello AzCopy użyje implementacji .NET MD5.</span><span class="sxs-lookup"><span data-stu-id="4ec04-523">For property "AzureStorageUseV1MD5" • True - hello default value, AzCopy will use .NET MD5 implementation.</span></span>
<span data-ttu-id="4ec04-524">• False — AzCopy będzie używać algorytmu MD5 zgodnego ze standardem FIPS.</span><span class="sxs-lookup"><span data-stu-id="4ec04-524">• False – AzCopy will use FIPS compliant MD5 algorithm.</span></span>

<span data-ttu-id="4ec04-525">Należy pamiętać, że zgodnych algorytmów FIPS jest domyślnie wyłączony na komputerze z systemem Windows można wpisać secpol.msc w oknie Uruchamianie i sprawdzić tego przełącznika na ustawienia zabezpieczeń -> Zabezpieczenia -> Zasady lokalne Opcje -> Kryptografia systemu: Użyj zgodnych algorytmów FIPS dla celów szyfrowania, mieszania i podpisywania.</span><span class="sxs-lookup"><span data-stu-id="4ec04-525">Note that FIPS compliant algorithms is disabled by default on your Windows machine, you can type secpol.msc in your Run window and check this switch at Security Setting->Local Policy->Security Options->System cryptography: Use FIPS compliant algorithms for encryption, hashing and signing.</span></span>

## <a name="next-steps"></a><span data-ttu-id="4ec04-526">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="4ec04-526">Next steps</span></span>
<span data-ttu-id="4ec04-527">Aby uzyskać więcej informacji na temat usługi Azure Storage i narzędzia AzCopy można znaleźć toohello następujące zasoby.</span><span class="sxs-lookup"><span data-stu-id="4ec04-527">For more information about Azure Storage and AzCopy, refer toohello following resources.</span></span>

### <a name="azure-storage-documentation"></a><span data-ttu-id="4ec04-528">Dokumentacja magazynu Azure:</span><span class="sxs-lookup"><span data-stu-id="4ec04-528">Azure Storage documentation:</span></span>
* [<span data-ttu-id="4ec04-529">Wprowadzenie tooAzure magazynu</span><span class="sxs-lookup"><span data-stu-id="4ec04-529">Introduction tooAzure Storage</span></span>](storage-introduction.md)
* [<span data-ttu-id="4ec04-530">Jak toouse magazynu obiektów Blob w .NET</span><span class="sxs-lookup"><span data-stu-id="4ec04-530">How toouse Blob storage from .NET</span></span>](storage-dotnet-how-to-use-blobs.md)
* [<span data-ttu-id="4ec04-531">Jak toouse magazynu plików w .NET</span><span class="sxs-lookup"><span data-stu-id="4ec04-531">How toouse File storage from .NET</span></span>](storage-dotnet-how-to-use-files.md)
* [<span data-ttu-id="4ec04-532">Jak toouse magazynu tabel w .NET</span><span class="sxs-lookup"><span data-stu-id="4ec04-532">How toouse Table storage from .NET</span></span>](storage-dotnet-how-to-use-tables.md)
* [<span data-ttu-id="4ec04-533">Jak toocreate, zarządzania i usuwania konta magazynu</span><span class="sxs-lookup"><span data-stu-id="4ec04-533">How toocreate, manage, or delete a storage account</span></span>](storage-create-storage-account.md)
* [<span data-ttu-id="4ec04-534">Transfer danych za pomocą narzędzia AzCopy w systemie Linux</span><span class="sxs-lookup"><span data-stu-id="4ec04-534">Transfer data with AzCopy on Linux</span></span>](storage-use-azcopy-linux.md)

### <a name="azure-storage-blog-posts"></a><span data-ttu-id="4ec04-535">Wpisy blogu magazynu Azure:</span><span class="sxs-lookup"><span data-stu-id="4ec04-535">Azure Storage blog posts:</span></span>
* [<span data-ttu-id="4ec04-536">Wprowadzenie Podgląd Biblioteka przepływu danych usługi Azure Storage</span><span class="sxs-lookup"><span data-stu-id="4ec04-536">Introducing Azure Storage Data Movement Library Preview</span></span>](https://azure.microsoft.com/blog/introducing-azure-storage-data-movement-library-preview-2/)
* [<span data-ttu-id="4ec04-537">AzCopy: Wprowadzenie do kopiowania synchroniczne i dostosowane typ zawartości</span><span class="sxs-lookup"><span data-stu-id="4ec04-537">AzCopy: Introducing synchronous copy and customized content type</span></span>](http://blogs.msdn.com/b/windowsazurestorage/archive/2015/01/13/azcopy-introducing-synchronous-copy-and-customized-content-type.aspx)
* [<span data-ttu-id="4ec04-538">Narzędzie AzCopy: Announcing ogólne dostępności 3.0 AzCopy oraz wersji zapoznawczej AzCopy 4.0 z tabeli i plik pomocy technicznej</span><span class="sxs-lookup"><span data-stu-id="4ec04-538">AzCopy: Announcing General Availability of AzCopy 3.0 plus preview release of AzCopy 4.0 with Table and File support</span></span>](http://blogs.msdn.com/b/windowsazurestorage/archive/2014/10/29/azcopy-announcing-general-availability-of-azcopy-3-0-plus-preview-release-of-azcopy-4-0-with-table-and-file-support.aspx)
* [<span data-ttu-id="4ec04-539">Narzędzie AzCopy: Zoptymalizowana pod kątem scenariuszy kopii na dużą skalę</span><span class="sxs-lookup"><span data-stu-id="4ec04-539">AzCopy: Optimized for Large-Scale Copy Scenarios</span></span>](http://go.microsoft.com/fwlink/?LinkId=507682)
* [<span data-ttu-id="4ec04-540">AzCopy: Obsługa dostęp do odczytu magazynu geograficznie nadmiarowego</span><span class="sxs-lookup"><span data-stu-id="4ec04-540">AzCopy: Support for read-access geo-redundant storage</span></span>](http://blogs.msdn.com/b/windowsazurestorage/archive/2014/04/07/azcopy-support-for-read-access-geo-redundant-account.aspx)
* [<span data-ttu-id="4ec04-541">Narzędzie AzCopy: Transfer danych za pomocą jej ponownie uruchomić tryb i tokenu sygnatury dostępu Współdzielonego</span><span class="sxs-lookup"><span data-stu-id="4ec04-541">AzCopy: Transfer data with re-startable mode and SAS token</span></span>](http://blogs.msdn.com/b/windowsazurestorage/archive/2013/09/07/azcopy-transfer-data-with-re-startable-mode-and-sas-token.aspx)
* [<span data-ttu-id="4ec04-542">Narzędzia AzCopy: Blob kopiowania między konta przy użyciu</span><span class="sxs-lookup"><span data-stu-id="4ec04-542">AzCopy: Using cross-account Copy Blob</span></span>](http://blogs.msdn.com/b/windowsazurestorage/archive/2013/04/01/azcopy-using-cross-account-copy-blob.aspx)
* [<span data-ttu-id="4ec04-543">Narzędzie AzCopy: Przekazywanie pobieranie plików dla obiektów blob Azure</span><span class="sxs-lookup"><span data-stu-id="4ec04-543">AzCopy: Uploading/downloading files for Azure Blobs</span></span>](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/12/03/azcopy-uploading-downloading-files-for-windows-azure-blobs.aspx)

